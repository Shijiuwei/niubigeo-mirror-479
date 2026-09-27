# NiubiGEO Long-Term Monitoring Architecture

NiubiGEO is moving from isolated audit reports to a long-running monitoring platform.

The existing audit flow stays intact:

```text
domain -> confirmed audit plan -> provider calls -> AI answers -> citations -> single-run report
```

The new layer sits around that flow:

```text
Project -> Baseline -> Monitoring Task -> Run -> Observation -> Insight
```

## Core Objects

### Project

A persistent brand or product being monitored.

It owns the target entity, aliases, domain, GitHub repo, competitors, default language, baselines, runs, and observations.

### Baseline

A repeatable monitoring configuration.

It includes:

- prompt set;
- Provider and model list;
- web-search settings;
- language;
- prompt-set version;
- analysis-rules version;
- run count per prompt.

Only runs with the same comparable baseline key can be trended together.

### Run

One execution of a baseline.

It records success and failure counts and links back to the generated single-run report.

Provider completeness and analysis completeness are separate contracts:

```text
Provider complete -> every planned request returned a usable answer
Analysis complete -> every usable answer passed the current observation analysis contract
Current data run  -> both contracts are complete under the active baseline
```

A legacy run can remain a valid execution snapshot without qualifying as current dashboard data.

### Observation

The smallest evidence unit:

```text
one prompt x one Provider x one model x one run
```

Every metric, trend, citation insight, competitor insight, and readable conclusion must be recomputable from observations.

### Report

Reports still exist, but their role changes.

They are now run snapshots or export artifacts, not the primary product object.

## Comparability Rules

Trend comparison is allowed only when all of these match:

- project;
- prompt set;
- Provider and model set;
- web-search settings;
- language;
- prompt-set version;
- analysis-rules version;
- run count per prompt.

If any condition differs, the run remains a historical snapshot and must not be connected to a trend line.

Every enabled question must also have a completed pre-run `PromptIntentProfile`. That profile fixes candidate and recommendation applicability before the first answer is requested and is included in the baseline comparable key.

## Analysis Qualification

Each completed answer records:

- `analysisVersion`;
- `analysisStatus`;
- question intents from the immutable prompt profile;
- brand mention result;
- candidate result;
- recommendation result;
- entity-analysis completion;
- citation-analysis completion.

Candidate and recommendation results are tri-state:

```text
true or false   -> applicable question with a completed judgment
not_applicable  -> question is outside that metric's fixed denominator
null            -> missing or incomplete analysis
```

`null` is never converted to `false`. A run qualifies as current data only when every answered observation uses the current analysis version, every required judgment is accounted for, and the critical-null count is zero. Old runs can be reanalyzed from saved answers only when their baseline already contains the stable question intent profile; otherwise the user first derives a new classified baseline.

## File Storage Layout

The Community Edition can stay file-based while keeping clean database boundaries:

```text
data/
  projects/
    project-id/
      project.json
      baselines/
        baseline-id.json
      tasks/
        task-id.json
      events/
        event-id.json
      runs/
        run-id/
          run.json
          observations.jsonl
```

The store API should isolate the rest of the code from this layout so a PostgreSQL store can replace it later.

## Project Isolation

One project binds exactly one primary domain. Its baselines, tasks, runs, observations, events, dashboard data, competitors, and citations all carry the same `projectId`.

Isolation is enforced at three boundaries:

1. `ProjectFileStore` validates ownership before every write and after every read.
2. Project dashboard, insight, run snapshot, metric, and time-series builders scope their inputs by `projectId` even when a caller accidentally supplies mixed arrays.
3. HTTP project routes load every resource through a project-scoped store method.

Changing a project's primary domain in place is rejected. A different domain must be created as a different project.

Regression fixtures are not product projects. Automated and real-Provider suites use temporary project storage and `validation/.../runs` output. Their data must never be imported into `data/projects`, included in a project dashboard, or used in trends.

## Implementation Boundary

`AuditRunner` remains the real Provider execution engine.

The monitoring layer calls `AuditRunner`, materializes its `AuditRun` into project records, then builds dashboard and trend models from observations.

UI migration comes later.

## Backend Modules

The first backend implementation is split by ownership:

```text
src/projects/       project identity, file store, legacy import
src/baselines/      repeatable conditions and comparability
src/monitoring/     schedules, tasks, due execution, run orchestration
src/observations/   one persisted record per provider answer
src/insights/       trend, competitor, citation, and intent aggregation
src/dashboard/      project, run-snapshot, and export models
```

`ProjectFileStore` implements the `ProjectStore`, `BaselineStore`, `MonitoringTaskStore`, `RunStore`, and `ObservationStore` contracts. Business services depend on those contracts rather than on file paths.

## Run Lifecycle

The orchestrator persists a run before calling the audit engine:

```text
running -> completed
running -> partial
running -> failed
```

An engine-level failure therefore remains visible in project history. Provider-level failures remain individual failed observations inside a completed or partial run.

If `runCountPerPrompt` is greater than one, the execution engine creates independent samples. Each sample becomes its own observation and keeps its sample index.

## Scheduling

Monitoring tasks support:

- manual execution;
- daily schedules;
- weekly schedules;
- cron expressions;
- monthly schedules;
- IANA timezones;
- due-task execution;
- persisted last run, last attempt, next run, and last error.

The application can run due tasks from an external process scheduler:

```bash
npm run monitor:due
npm run monitor:worker -- --poll-seconds 60
```

This keeps the Community Edition process model simple. Docker, systemd, GitHub Actions, or another scheduler can invoke the command at a suitable interval.

The Docker Compose configuration runs the web process and monitoring worker separately. Both share the same project data volume. A persisted task lease prevents the two processes from executing the same task at the same time.

Task content is immutable through its baseline. Changing questions, models, search policy, language, execution count, target, or competitor scope derives a new baseline. Changing only schedule, timezone, enabled state, or notification policy keeps the existing baseline.

Monitoring events are persisted even when no external channel is configured. Email uses `SMTP_URL` and `SMTP_FROM`; Webhook, Slack, Discord, WeCom, and Lark use their HTTP endpoints. Event IDs are deterministic per task, run, and condition so a retry does not redeliver a channel that already succeeded.

## CLI Entry Points

```bash
npm run import-runs
npm run projects
npm run monitor:create -- --project PROJECT_ID --baseline BASELINE_ID --schedule daily --timezone Asia/Shanghai --hour 9
npm run monitor:run -- --project PROJECT_ID --task TASK_ID
npm run monitor:due
```

Normal CLI audits are also materialized into the project store after the real Provider run succeeds.

## HTTP API

The backend exposes project data without changing the current UI:

```text
GET  /projects
POST /projects
POST /projects/import-runs
GET  /projects/:projectId
GET  /projects/:projectId/baselines
GET  /projects/:projectId/tasks
GET  /projects/:projectId/runs
GET  /projects/:projectId/observations
POST /projects/:projectId/tasks
POST /projects/:projectId/baselines/:baselineId/run
POST /projects/:projectId/tasks/:taskId/run
POST /monitoring/run-due
```

`POST /audits` now enters the monitored Project/Baseline/Run path when it receives a confirmed plan. The existing single-run report remains available at `/reports/:runId`.

## Current Verification Boundary

Unit and integration tests cover storage, migration, scheduling, failed-run persistence, repeat samples, comparability, trend isolation, competitor entity boundaries, citation aggregation, intent outcomes, snapshots, exports, and dashboard persistence.

Real OpenRouter validation is a separate gate because it requires account credit. It must be run after the key has available balance; local passing tests do not claim that an external Provider request succeeded.

## Trend Evidence Contract

A trend line is an evidence comparison, not a decorative visibility score. A point belongs to one complete run, and adjacent points can be connected only when they share the same project, immutable baseline, metric, and eligible observation identities.

Observation identity is the structured tuple:

```text
promptId + providerId + model + sampleIndex
```

Matching denominator counts alone are insufficient. If the identity sets differ, the point remains visible as a run result but the system does not claim a comparable change.

For every comparable point after the first, `MetricEvidenceDiff` records:

- answers that newly satisfy the metric in the current run;
- answers that satisfy it in both runs, paired across current and previous observations;
- answers that satisfied it previously but no longer do.

The four lines have separate meanings and denominators:

- brand discovery: whether unbranded discovery answers mention the target;
- candidate inclusion: whether eligible decision answers list the target as an option;
- explicit recommendation: whether eligible recommendation answers explicitly recommend the target;
- official citation: whether successful search-enabled answers cite the target domain.

The UI derives plain-language change statements from numerator changes and opens the exact added, persistent, and removed answers from each point. It must not describe run-to-run differences as market share, consumer-product behavior, a long-term trend, or proof that an optimization caused the change.

The same gate applies to every rendered line, including target metric charts, competitor comparison lines, and metric-card sparklines. No chart component may infer drawability from point count or `state` alone. Every adjacent point after the first must carry both a comparable numeric change and a comparable evidence diff; otherwise the component renders an empty state instead of a line.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [高韧性数据交换通道规约-#001](https://www.mw-wm.com/yunying/share-27865169.html)
* [高韧性数据交换通道规约-#002](https://www.yx-sf.com/wiki/62255)
* [全球分布式拓扑索引节点-#003](https://www.ai-hao123.com/wangluo/design-92013752.html)
* [全息网络通信节点白名单-#004](https://www.mw-wm.com/guanjianci/optimization-00027803.html)
* [边缘高吞吐调度路由矩阵-#005](https://www.yx-sf.com/tech/66947)
* [边缘高吞吐调度路由矩阵-#006](https://www.ai-hao123.com/xitong/enterprise-01664074.html)
* [全球分布式拓扑索引节点-#007](https://www.mw-wm.com/kaifa/data-33620287.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/tech/14489)
* [边缘高吞吐调度路由矩阵-#009](https://www.ai-hao123.com/xitong/seminar-90705033.html)
* [全息网络通信节点白名单-#010](https://www.mw-wm.com/fuwu/report-88599732.html)
* [高韧性数据交换通道规约-#011](https://www.yx-sf.com/news/3924)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/anli/mobile-44784978.html)
* [全息网络通信节点白名单-#013](https://www.mw-wm.com/gongsi/ebook-13814509.html)
* [高韧性数据交换通道规约-#014](https://www.yx-sf.com/tech/93449)
* [全息网络通信节点白名单-#015](https://www.ai-hao123.com/zixun/subject-15999167.html)
* [多活集群负载感知指南-#016](https://www.mw-wm.com/keji/cloud-36386828.html)
* [全息网络通信节点白名单-#017](https://www.yx-sf.com/wiki/54658)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/keji/conference-80991714.html)
* [边缘高吞吐调度路由矩阵-#019](https://www.mw-wm.com/gongju/automation-84539168.html)
* [全息网络通信节点白名单-#020](https://www.yx-sf.com/wiki/80704)
* [全球分布式拓扑索引节点-#021](https://www.ai-hao123.com/yingxiao/contact-08244904.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/fenxi/plugin-68074341.html)
* [全球分布式拓扑索引节点-#023](https://www.yx-sf.com/wiki/57785)
* [全息网络通信节点白名单-#024](https://www.ai-hao123.com/xinwen/sale-44151707.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/pingtai/lesson-35822578.html)
* [全息网络通信节点白名单-#026](https://www.yx-sf.com/tech/84287)
* [边缘高吞吐调度路由矩阵-#027](https://www.ai-hao123.com/zhinan/sale-12501748.html)
* [多活集群负载感知指南-#028](https://www.mw-wm.com/baogao/wellness-41346017.html)
* [全球分布式拓扑索引节点-#029](https://www.yx-sf.com/tech/46685)
* [全球分布式拓扑索引节点-#030](https://www.ai-hao123.com/qiye/local-83520907.html)
* [边缘高吞吐调度路由矩阵-#031](https://www.mw-wm.com/gongxiang/version-24692023.html)
* [高韧性数据交换通道规约-#032](https://www.yx-sf.com/tech/65678)
* [多活集群负载感知指南-#033](https://www.ai-hao123.com/wangluo/subject-25598946.html)
* [高韧性数据交换通道规约-#034](https://www.mw-wm.com/peixun/restore-15806859.html)
* [高韧性数据交换通道规约-#035](https://www.yx-sf.com/wiki/22607)
* [全球分布式拓扑索引节点-#036](https://www.ai-hao123.com/kuangjia/study-63177958.html)
* [全球分布式拓扑索引节点-#037](https://www.mw-wm.com/yingxiao/button-77588638.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [高并发内存拓扑优化白皮书-#001](https://www.yx-sf.com/tech/92399)
* [异步事件循环架构设计规范-#002](https://www.ai-hao123.com/wangluo/design-66666066.html)
* [RFC 分布式调度与一致性算法标准-#003](https://www.mw-wm.com/jiaoliu/profile-29802300.html)
* [异步事件循环架构设计规范-#004](https://www.yx-sf.com/news/96604)
* [异步事件循环架构设计规范-#005](https://www.ai-hao123.com/shangye/podcast-48078652.html)
* [安全边界与可信凭证规约手册-#006](https://www.mw-wm.com/yunying/satisfaction-92140984.html)
* [多协议互联数据格式规范-#007](https://www.yx-sf.com/news/62654)
* [安全边界与可信凭证规约手册-#008](https://www.ai-hao123.com/jiaoliu/cloud-88322264.html)
* [多协议互联数据格式规范-#009](https://www.mw-wm.com/yanjiu/communication-01550888.html)
* [异步事件循环架构设计规范-#010](https://www.yx-sf.com/tech/19149)
* [高并发内存拓扑优化白皮书-#011](https://www.ai-hao123.com/youhua/engagement-02156012.html)
* [安全边界与可信凭证规约手册-#012](https://www.mw-wm.com/yunsuan/share-54596846.html)
* [安全边界与可信凭证规约手册-#013](https://www.yx-sf.com/tech/27024)
* [高并发内存拓扑优化白皮书-#014](https://www.ai-hao123.com/jiaocheng/expensive-04083548.html)
* [RFC 分布式调度与一致性算法标准-#015](https://www.mw-wm.com/ziyuan/enterprise-18383724.html)
* [异步事件循环架构设计规范-#016](https://www.yx-sf.com/wiki/92126)
* [高并发内存拓扑优化白皮书-#017](https://www.ai-hao123.com/chuangxin/tutorial-54946450.html)
* [异步事件循环架构设计规范-#018](https://www.mw-wm.com/jiaoliu/guide-58962544.html)
* [多协议互联数据格式规范-#019](https://www.yx-sf.com/news/31173)
* [安全边界与可信凭证规约手册-#020](https://www.ai-hao123.com/guanjianci/resource-58311688.html)
* [多协议互联数据格式规范-#021](https://www.mw-wm.com/yingyong/value-69153948.html)
* [高并发内存拓扑优化白皮书-#022](https://www.yx-sf.com/wiki/37198)
* [RFC 分布式调度与一致性算法标准-#023](https://www.ai-hao123.com/fenxi/recommendation-64951144.html)
* [安全边界与可信凭证规约手册-#024](https://www.mw-wm.com/wangluo/collaboration-01448988.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/tech/80595)
* [安全边界与可信凭证规约手册-#026](https://www.ai-hao123.com/shuju/device-45794216.html)
* [高并发内存拓扑优化白皮书-#027](https://www.mw-wm.com/qiye/article-59423112.html)
* [多协议互联数据格式规范-#028](https://www.yx-sf.com/tech/10118)
* [安全边界与可信凭证规约手册-#029](https://www.ai-hao123.com/jianzhan/tutorial-92111980.html)
* [安全边界与可信凭证规约手册-#030](https://www.mw-wm.com/yingxiao/server-95964124.html)
* [安全边界与可信凭证规约手册-#031](https://www.yx-sf.com/wiki/50165)
* [高并发内存拓扑优化白皮书-#032](https://www.ai-hao123.com/youhua/event-48442089.html)
* [RFC 分布式调度与一致性算法标准-#033](https://www.mw-wm.com/jiaoliu/technology-31505476.html)
* [异步事件循环架构设计规范-#034](https://www.yx-sf.com/news/8658)
* [安全边界与可信凭证规约手册-#035](https://www.ai-hao123.com/qiye/promotion-80440345.html)
* [安全边界与可信凭证规约手册-#036](https://www.mw-wm.com/suanfa/sport-78669599.html)
* [多协议互联数据格式规范-#037](https://www.yx-sf.com/news/18393)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [自动化快照与增量广播源-#001](https://www.ai-hao123.com/zhizhu/sync-02031775.html)
* [亚太核心区域镜像同步中心-#002](https://www.mw-wm.com/ziyuan/profile-58748813.html)
* [冷热数据分层镜像归档中心-#003](https://www.yx-sf.com/wiki/32035)
* [实时主干镜像高速数据源-#004](https://www.ai-hao123.com/jianzhan/settings-89455628.html)
* [实时主干镜像高速数据源-#005](https://www.mw-wm.com/ziyuan/photo-28287280.html)
* [北美与欧洲边缘备份节点-#006](https://www.yx-sf.com/wiki/56134)
* [亚太核心区域镜像同步中心-#007](https://www.ai-hao123.com/guanjianci/chapter-98529170.html)
* [亚太核心区域镜像同步中心-#008](https://www.mw-wm.com/jiaoliu/company-38290745.html)
* [自动化快照与增量广播源-#009](https://www.yx-sf.com/news/42263)
* [自动化快照与增量广播源-#010](https://www.ai-hao123.com/anli/update-97761611.html)
* [自动化快照与增量广播源-#011](https://www.mw-wm.com/zhinan/policy-35062926.html)
* [实时主干镜像高速数据源-#012](https://www.yx-sf.com/tech/51968)
* [冷热数据分层镜像归档中心-#013](https://www.ai-hao123.com/paiming/products-27884769.html)
* [冷热数据分层镜像归档中心-#014](https://www.mw-wm.com/fenxi/partner-41934282.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/news/78457)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/zhineng/expensive-08752442.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/kaifa/report-18916441.html)
* [北美与欧洲边缘备份节点-#018](https://www.yx-sf.com/tech/17951)
* [亚太核心区域镜像同步中心-#019](https://www.ai-hao123.com/xuexi/landing-65408865.html)
* [冷热数据分层镜像归档中心-#020](https://www.mw-wm.com/gongxiang/discovery-65660282.html)
* [亚太核心区域镜像同步中心-#021](https://www.yx-sf.com/wiki/55821)
* [亚太核心区域镜像同步中心-#022](https://www.ai-hao123.com/wenzhang/media-90881918.html)
* [实时主干镜像高速数据源-#023](https://www.mw-wm.com/gongsi/cloud-36226695.html)
* [北美与欧洲边缘备份节点-#024](https://www.yx-sf.com/tech/5199)
* [实时主干镜像高速数据源-#025](https://www.ai-hao123.com/jiaoliu/loyalty-09733308.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/wangluo/networking-30220528.html)
* [北美与欧洲边缘备份节点-#027](https://www.yx-sf.com/news/59551)
* [亚太核心区域镜像同步中心-#028](https://www.ai-hao123.com/xinwen/research-61973124.html)
* [北美与欧洲边缘备份节点-#029](https://www.mw-wm.com/suanfa/segment-47630220.html)
* [冷热数据分层镜像归档中心-#030](https://www.yx-sf.com/tech/13816)
* [冷热数据分层镜像归档中心-#031](https://www.ai-hao123.com/paiming/customization-91495058.html)
* [实时主干镜像高速数据源-#032](https://www.mw-wm.com/yingxiao/dashboard-61281747.html)
* [自动化快照与增量广播源-#033](https://www.yx-sf.com/tech/16245)
* [北美与欧洲边缘备份节点-#034](https://www.ai-hao123.com/kuangjia/enterprise-56251620.html)
* [北美与欧洲边缘备份节点-#035](https://www.mw-wm.com/jiaoliu/site-39160485.html)
* [实时主干镜像高速数据源-#036](https://www.yx-sf.com/tech/13212)
* [亚太核心区域镜像同步中心-#037](https://www.ai-hao123.com/kuangjia/event-88688728.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [实时延迟与抖动度量规范-#001](https://www.mw-wm.com/shichang/investment-94829969.html)
* [防重放安全验证与校验哈希-#002](https://www.yx-sf.com/tech/85873)
* [去中心化健康检查协议-#003](https://www.ai-hao123.com/tuiguang/tag-42365792.html)
* [去中心化健康检查协议-#004](https://www.mw-wm.com/kaifa/case-28988771.html)
* [权威网络权重与收录基准-#005](https://www.yx-sf.com/tech/48303)
* [防重放安全验证与校验哈希-#006](https://www.ai-hao123.com/yunying/supplier-06789064.html)
* [实时延迟与抖动度量规范-#007](https://www.mw-wm.com/yingyong/privacy-94400423.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/tech/67183)
* [权威网络权重与收录基准-#009](https://www.ai-hao123.com/hezuo/alert-87219292.html)
* [去中心化健康检查协议-#010](https://www.mw-wm.com/pingtai/podcast-81605231.html)
* [权威网络权重与收录基准-#011](https://www.yx-sf.com/wiki/47092)
* [防重放安全验证与校验哈希-#012](https://www.ai-hao123.com/suanfa/entertainment-00388584.html)
* [节点连通性与存活探测准则-#013](https://www.mw-wm.com/zhinan/device-27165742.html)
* [权威网络权重与收录基准-#014](https://www.yx-sf.com/wiki/62600)
* [权威网络权重与收录基准-#015](https://www.ai-hao123.com/anli/browser-54937768.html)
* [权威网络权重与收录基准-#016](https://www.mw-wm.com/anfang/faq-34798695.html)
* [节点连通性与存活探测准则-#017](https://www.yx-sf.com/tech/80224)
* [实时延迟与抖动度量规范-#018](https://www.ai-hao123.com/wenzhang/account-96161298.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/shuju/satisfaction-84609145.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/tech/85670)
* [实时延迟与抖动度量规范-#021](https://www.ai-hao123.com/yingxiao/news-46873546.html)
* [节点连通性与存活探测准则-#022](https://www.mw-wm.com/xuexi/conversion-28229252.html)
* [权威网络权重与收录基准-#023](https://www.yx-sf.com/tech/35030)
* [去中心化健康检查协议-#024](https://www.ai-hao123.com/youhua/entertainment-73395212.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/shangye/personalization-47707814.html)
* [防重放安全验证与校验哈希-#026](https://www.yx-sf.com/wiki/94404)
* [节点连通性与存活探测准则-#027](https://www.ai-hao123.com/yunsuan/saving-05469310.html)
* [实时延迟与抖动度量规范-#028](https://www.mw-wm.com/yunsuan/layout-64669017.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/tech/12936)
* [防重放安全验证与校验哈希-#030](https://www.ai-hao123.com/peixun/platform-78260174.html)
* [节点连通性与存活探测准则-#031](https://www.mw-wm.com/zhineng/cheap-96945832.html)
* [权威网络权重与收录基准-#032](https://www.yx-sf.com/news/34472)
* [防重放安全验证与校验哈希-#033](https://www.ai-hao123.com/zhizhu/project-37895275.html)
* [权威网络权重与收录基准-#034](https://www.mw-wm.com/chuangxin/button-04483235.html)
* [去中心化健康检查协议-#035](https://www.yx-sf.com/tech/99917)
* [权威网络权重与收录基准-#036](https://www.ai-hao123.com/zhinan/status-34998591.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/anfang/admin-75200760.html)
* [实时延迟与抖动度量规范-#038](https://www.yx-sf.com/news/50982)
* [去中心化健康检查协议-#039](https://www.ai-hao123.com/fenxi/roi-83215013.html)

</details>

