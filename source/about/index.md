---
title: 关于我
date: 2026-11-02 10:00:00
layout: "about"
---

# 郭洋 · Yang

这个站没什么宏大规划，就是把做过的事记下来。写出来的东西如果对同行有用，那更好；没人看也无所谓，主要是我自己需要找个地方整理。

平时在深圳，富途：金融后端开发工程师。钱的系统，规矩多，改一行代码要想清楚三件事：会不会少算别人的钱，会不会多扣自己的钱，出了问题能不能对上账。金融的事真的劳心劳力，我一直在想：怎么把这套东西做到全 AI 自动化——从需求理解、代码实现、对账校验到风险兜底，让人从重复的账务劳作里抽身出来，只保留在关键决策点上。

下班偶尔折腾数据的东西，本科是金融科技出身，对数字怎么变成决策这事一直有兴趣。

邮箱：mark13612911661@163.com

---

下面的内容偏正式，算是份简历。想了解我做过什么，从这往下看就行。

## 教育经历

**悉尼大学** · 计算机科学与技术 · 硕士 · 2024.2 – 2026.2
机器学习、数据挖掘、高级统计学、大数据分析、深度学习

**班戈大学（威尔士大学）** · 金融科技 · 本科 · 2019.9 – 2023.6
统计学、线性代数、数据结构与算法、Python、Spark、数据库、微观经济学

## 工作经历

### 富途网络科技（深圳） · 后端开发工程师 · 2026.2 – 至今

互联网金融，证券收费计息系统。技术栈：Go、Gin、GORM、gRPC、Protobuf、协程、WorkerPool、Redis、RocketMQ、MySQL。运用 Claude Agent 做研发流程提效。

- **证券计费计息全链路**：实现计息 → 资金冻结 → 扣费 → 解冻完整业务状态机及异常恢复机制；通过 WorkerPool 优化月末大批量计费任务，解决数据库连接争抢；对定时批处理做专项治理，完善幂等控制、失败补偿与告警；落地 JP 区域收费业务。
- **结构化票据新品类**：搭建完整收费业务链路，设计配置灰度发布与回滚方案，新业务平稳上线，规避对存量业务影响。
- **港股期权 Python → Go 迁移重构**：设计时态快照模型，依托双跑对账、灰度切流完成无感迁移；计费链路异常解耦与降级隔离，严格区分试算与真实扣费场景，强化资金风险防控。
- **计费 AI 辅助排查 Agent**：沉淀业务领域知识库，支撑规则查询与线上故障定位；资金场景多层安全防护，Agent 仅开放查询，禁止高风险资金写操作。

### 百度科技（深圳） · 数据开发实习生 · 2025.7 – 2025.11

- **播放器全链路可观测性**：从零到一构建异常诊断体系。Scala 编写 SparkSQL 模板处理日均 TB 级内核日志，在 Doris 构建涵盖异常规模（VV/UV）与异常强度（P0/P50/P90/P99 耗时）的多维指标仓库；Sugar BI 搭建交互式诊断面板，支持 AB 组 / 版本 / 机型 / OS 多维下钻，核心故障 MTTD 缩短 30%。
- **AB 实验因果推断**：应用双重稳健估计（DRE）框架解决选择偏差，显著优于传统均值比较；配对 t 检验（p < 0.01）与置换检验互证，量化核心体验分下降 0.52（95% CI 0.45–0.59），驱动版本回滚决策；LightGBM（AUC 0.95）+ SHAP 归因，定位某芯片 × OS 组合为负向主因，预计挽回 30% 体验损失。
- **数据根基治理**：主导核心指标埋点重构，采集准确率提升至 99.9%；基于 Python/Pandas/SQLAlchemy 开发元数据治理 CLI，自动排序校验、重复检测、断号修复，人工治理从 3 人天/月降至 0.5 人天。
- **自动化监控**：封装网络库 OpenAPI，研发 Python 调度脚本与 Markdown 渲染器，构建无人值守日级 KPI 监控管道，推送 500+ 次预警，分钟级触达。

### 优钱科技 · 大数据开发实习生 · 2023.9 – 2023.12

- Hive on Spark + Flink 数据治理体系；Java 开发 UDF/UDAF/UDTF 集成 Hue。
- Hive on Spark 部署调优，关键任务效率提升约 20%。
- PySpark ML 贷款信用评分模型（AUC 0.84、KS 0.46），封装 Hive UDF 上线，T+0/T+1 批量预测；Airflow 端到端工作流；上线后审核命中率 +9.8pp，人工审核 −27%。
- Flink 事件时间 / Watermark / 窗口聚合 / 维表 Join，Checkpoint + 两阶段提交保障 Exactly-Once；ZooKeeper HA 协调；Great Expectations 数据质量治理。

### 劳埃德银行（Sandwich Placement） · 数据分析师 · 2021.6 – 2021.9

- 全场景调研（贷款获客、审批转化、存量经营、复贷营销、流失预警），拆解多维度指标体系。
- 贷款客户经营主题数仓建设：ODS/DWD/DWS 分层建模，SQL ETL 整合 8 大数据源，统一客户标识与口径。
- Power Query + DAX 搭建 BI 看板，多维下钻；客户标签体系，输出潜客营销名单支撑分层运营。
- 数据质量核查机制，跟踪触达-申请-转化全链路复盘。

## 个人项目

### Docker 化 Lakehouse · 2023.3 – 2023.12

技术栈：Docker/Compose、MinIO(S3)、Hive Metastore、Apache Iceberg、Spark 3、Trino、Great Expectations

- Docker Compose 一键编排 MinIO + HiveMS + Iceberg + Spark + Trino，本地复现湖仓（存储/计算解耦、Parquet + ACID 快照、多引擎读写）。
- Bronze/Silver/Gold 分层；Iceberg dt+category 分区，支持时间旅行 / 快照回滚；重复执行 SQL 30 次取 P95。
- Spark ETL 清洗聚合写入 Iceberg；Trino 即席分析与 AS OF 查询，沉淀 GMV/AOV、Top-K、时间序列指标。
- Great Expectations 主键唯一 / 空值 / 范围校验，失败阻断写入并生成 Data Docs。关键数据：GMV 3561.2，AOV 296.77。

### 房价预测 · 2024.6 – 2024.9

- ETL 结构化处理，TFDF 构建房价预测模型。
- 超参调整 + 特征重要性分析优化性能，显著降低 RMSE。
- 对比 TFDF 与决策树、XGBoost，验证 TFDF 回归优势。

## 技能

- **后端**：Go、Gin、GORM、gRPC、Protobuf、协程、WorkerPool、MySQL、Redis、RocketMQ
- **数据**：Spark、Flink、Hive、Doris、Trino、Iceberg、PySpark ML、LightGBM、SHAP
- **工程**：Docker、Airflow、Great Expectations、ZooKeeper、SQLAlchemy、Pandas
- **方法**：分布式账务一致性、双跑对账、灰度切流、幂等与补偿、因果推断、可观测性
