---
title: 在 MacBook 上塞一个湖仓，只为弄懂它到底在干嘛
date: 2026-11-02 11:00:00
tags: [Lakehouse, Docker, Iceberg, Spark, Trino]
---

湖仓（Lakehouse）的卖点一句话能说清：存储与计算解耦、ACID 事务、多引擎读写。但只看文档不动手很难有体感。这个项目用 Docker Compose 把 MinIO + Hive Metastore + Iceberg + Spark + Trino 一键拉起来，本地复现一套最小湖仓。

## 架构

```
┌─────────────┐     ┌──────────────┐     ┌──────────────┐
│   MinIO     │ ←── │ HiveMetastore│ ←── │  Spark / Trino│
│   (S3)      │     │  (元数据)     │     │  (计算引擎)    │
└─────────────┘     └──────────────┘     └──────────────┘
       ▲                                         │
       └──────────── Parquet + Iceberg ──────────┘
```

- **MinIO** 提供 S3 兼容对象存储，数据落 Parquet 文件。
- **Hive Metastore** 记录 Iceberg 表的元数据（schema、分区、当前快照）。
- **Spark** 做 ETL 批处理写入。
- **Trino** 做即席查询。

存储和计算完全分开：换引擎不用动数据。

## 分层与分区

数据按 Bronze/Silver/Gold 分层：

- **Bronze**：原始数据，几乎不清洗。
- **Silver**：去重、类型规范、关联维表。
- **Gold**：业务指标，可直接出报表。

Iceberg 表用 `dt + category` 分区。配合 Iceberg 的时间旅行与快照回滚：

```sql
SELECT * FROM orders.history;
SELECT * FROM orders FOR SYSTEM_VERSION_AS_OF 123456789;
SELECT * FROM orders FOR SYSTEM_TIME_AS_OF TIMESTAMP '2023-10-01 00:00:00';
```

写错了不用慌，回滚到上一个快照即可。

## 性能对比的笨办法

对比"未分区 / 未排序 / 小文件碎片多"的版本与优化版本，每条 SQL 重复执行 30 次取 P95。笨但诚实——平均值会被偶发长尾拉偏，P95 才是真实尾延迟。

## 数据质量：Great Expectations

每张 Gold 表配 Expectation Suite：

- 主键唯一
- 关键字段非空
- 数值范围合理（GMV > 0、AOV 在合理区间）

校验失败阻断下游写入并生成 Data Docs 可审计报告。数据问题在落地那一刻就被拦住，而不是流到报表里被业务发现。

## 关键数据

亚马逊示例数据集跑完：

- 总 GMV = 3561.2
- AOV = 296.77
- Top-4 类目按 GMV 排序可下钻
