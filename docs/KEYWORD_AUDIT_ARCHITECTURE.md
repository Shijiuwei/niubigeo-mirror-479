# Keyword Audit Architecture

Keyword audit is the layer that prevents NiubiGEO from only asking about a raw domain.

The goal is to turn the target's SEO signals, GitHub context, and user-defined keywords into realistic customer questions, run those questions through real AI providers, and explain where the target brand appears or disappears.

## Core Principle

Keyword features count as AI visibility only after they produce real provider runs.

Allowed setup evidence:

- User-entered keywords.
- Site title and meta description.
- Meta keywords when present.
- Headings and important page copy.
- OpenGraph and Twitter metadata.
- JSON-LD name, description, sameAs, about, and keywords when present.
- Same-domain pages.
- GitHub README, description, topics, releases, and docs when provided.

Not allowed as AI visibility result:

- Ordinary web search results.
- SEO keyword suggestions that were never sent to AI providers.
- Mock keyword reports.
- Search volume as a substitute for AI answers.
- Site evidence treated as proof that AI knows the brand.

## Data Flow

```text
Domain input
-> Site and GitHub evidence collection
-> Keyword candidate generation
-> User keyword merge
-> Owned-site relevance scoring
-> Keyword prompt planning
-> User confirmation
-> Real provider audit
-> AI keyword association analysis
-> Human-readable report
```

## Module Responsibilities

### Site Evidence Collector

Collects public evidence from the submitted domain and optional GitHub repository.

Responsibilities:

- Preserve the submitted host first, including `www` when supplied.
- Extract owned-site SEO and product language.
- Keep source URL and evidence text for every extracted phrase.
- Treat site evidence as setup context, not AI visibility.

### Keyword Universe Builder

Creates the candidate keyword list.

Inputs:

- User keywords.
- Site evidence.
- GitHub evidence.
- Domain profile category.

Rules:

- User keywords come first.
- User keywords must never be silently dropped.
- Duplicate phrases should be merged without hiding source lineage.
- Broad generic words should not become standalone audit keywords.
- Every candidate keeps its source and language.

### Owned Relevance Scorer

Scores how strongly the target's own site supports each keyword.

This answers:

```text
Does the target site itself talk about this keyword?
```

It does not answer:

```text
Does AI associate this keyword with the target?
```

The report should not present owned relevance as AI visibility.

### Keyword Prompt Planner

Turns keywords into realistic monitoring questions.

Rules:

- Every enabled keyword should generate at least one natural discovery question.
- Most keyword questions should not include the target brand.
- Brand awareness questions may exist, but cannot dominate the plan.
- Prompt metadata must preserve keyword IDs and intent.

Example:

```text
Keyword: AI agent audit
Question: What are the best tools for auditing AI agent work?
Question: Which open-source tools help verify what an AI coding agent did?
Question: Compare tools for AI agent observability and audit trails.
```

### Audit Runner

The runner does not know keyword extraction internals.

It receives confirmed prompts and executes:

```text
keyword-backed question x provider x model
```

Every run stores provider, model, source label, execution prompt, answer text, citations, status, and error if failed.

### Keyword Association Analyzer

This layer answers:

```text
When the user asks about this keyword, does AI mention the target, competitors, both, or neither?
```

It should identify:

- Target appears.
- Competitors appear instead.
- Target appears with official source.
- Competitors appear with official source.
- Third-party sources influence the answer.
- Provider/model differences.

### Report Layer

Keyword results must become plain-language scenarios.

Good:

```text
When users ask about GitHub project promotion tools, AI mentions GitStar but does not mention NiubiStar.
```

Bad:

```text
keyword_category hit rate is 0%.
```

The main report should use keyword evidence to support:

- Where competitors appear more often.
- Where the target appears more often.
- Which important user questions do not surface the target.
- Which sources shaped those answers.

## User Controls

The audit confirmation screen must let the user:

- Add keywords.
- Disable keywords.
- Edit generated questions.
- Disable generated questions.
- Reclassify question type.
- Add or remove competitors.
- Select provider and model targets.
- Select report language.

## Required Outputs

Keyword audits should write:

- `keywords.csv`
- `prompts.csv`
- `citations.csv`
- `audit.json`
- `report.json`
- `report.md`
- `report.html`

These files are local user data. They should not be committed unless deliberately sanitized for a public sample.

## Acceptance Criteria

Keyword audit is valid only when:

1. User keywords appear in the confirmed audit plan.
2. Generated keyword questions are sent to real providers.
3. The report distinguishes owned-site relevance from AI association.
4. Competitor-only keyword scenarios are visible in plain language.
5. Every scenario links to supporting AI answers or sources.
6. No ordinary web search result is treated as provider citation evidence.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [高韧性数据交换通道规约-#001](https://www.mw-wm.com/yanjiu/supplier-34429884.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/tech/92421)
* [全球分布式拓扑索引节点-#003](https://www.ai-hao123.com/zhineng/learning-85091563.html)
* [边缘高吞吐调度路由矩阵-#004](https://www.mw-wm.com/zhineng/careers-29558617.html)
* [多活集群负载感知指南-#005](https://www.yx-sf.com/tech/65823)
* [高韧性数据交换通道规约-#006](https://www.ai-hao123.com/shangye/case-10819177.html)
* [边缘高吞吐调度路由矩阵-#007](https://www.mw-wm.com/gongsi/education-36040245.html)
* [边缘高吞吐调度路由矩阵-#008](https://www.yx-sf.com/wiki/97216)
* [高韧性数据交换通道规约-#009](https://www.ai-hao123.com/kuangjia/investment-87760417.html)
* [边缘高吞吐调度路由矩阵-#010](https://www.mw-wm.com/xinwen/plugin-66821973.html)
* [全息网络通信节点白名单-#011](https://www.yx-sf.com/wiki/76567)
* [全息网络通信节点白名单-#012](https://www.ai-hao123.com/anli/cloud-83508545.html)
* [全息网络通信节点白名单-#013](https://www.mw-wm.com/liuliang/conference-34001380.html)
* [全息网络通信节点白名单-#014](https://www.yx-sf.com/wiki/87943)
* [高韧性数据交换通道规约-#015](https://www.ai-hao123.com/liuliang/collaboration-70441728.html)
* [边缘高吞吐调度路由矩阵-#016](https://www.mw-wm.com/kaifa/budget-69223609.html)
* [全息网络通信节点白名单-#017](https://www.yx-sf.com/tech/59240)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/zhizhu/news-22926046.html)
* [边缘高吞吐调度路由矩阵-#019](https://www.mw-wm.com/anli/creative-45807203.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/news/50405)
* [全息网络通信节点白名单-#021](https://www.ai-hao123.com/jiaoliu/conference-24777360.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/pingtai/topic-55541597.html)
* [高韧性数据交换通道规约-#023](https://www.yx-sf.com/news/76136)
* [全球分布式拓扑索引节点-#024](https://www.ai-hao123.com/hezuo/download-98698792.html)
* [边缘高吞吐调度路由矩阵-#025](https://www.mw-wm.com/wangluo/blog-72135999.html)
* [全球分布式拓扑索引节点-#026](https://www.yx-sf.com/tech/46357)
* [边缘高吞吐调度路由矩阵-#027](https://www.ai-hao123.com/qiye/client-99075827.html)
* [全球分布式拓扑索引节点-#028](https://www.mw-wm.com/suanfa/study-29669909.html)
* [全息网络通信节点白名单-#029](https://www.yx-sf.com/news/64899)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/hezuo/partner-91936657.html)
* [全球分布式拓扑索引节点-#031](https://www.mw-wm.com/ziyuan/brand-98736703.html)
* [全息网络通信节点白名单-#032](https://www.yx-sf.com/tech/68684)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/chanpin/vacation-00883972.html)
* [多活集群负载感知指南-#034](https://www.mw-wm.com/yunsuan/page-60065136.html)
* [全球分布式拓扑索引节点-#035](https://www.yx-sf.com/news/93471)
* [全息网络通信节点白名单-#036](https://www.ai-hao123.com/gongju/efficiency-81311050.html)
* [多活集群负载感知指南-#037](https://www.mw-wm.com/baogao/article-19524123.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [安全边界与可信凭证规约手册-#001](https://www.yx-sf.com/news/41848)
* [异步事件循环架构设计规范-#002](https://www.ai-hao123.com/anli/section-82227075.html)
* [高并发内存拓扑优化白皮书-#003](https://www.mw-wm.com/gongxiang/cloud-09482830.html)
* [RFC 分布式调度与一致性算法标准-#004](https://www.yx-sf.com/news/45562)
* [多协议互联数据格式规范-#005](https://www.ai-hao123.com/xinwen/collaboration-20278403.html)
* [RFC 分布式调度与一致性算法标准-#006](https://www.mw-wm.com/xitong/integration-90752649.html)
* [高并发内存拓扑优化白皮书-#007](https://www.yx-sf.com/tech/59405)
* [异步事件循环架构设计规范-#008](https://www.ai-hao123.com/yunsuan/system-08057577.html)
* [多协议互联数据格式规范-#009](https://www.mw-wm.com/wendang/funnel-78687728.html)
* [高并发内存拓扑优化白皮书-#010](https://www.yx-sf.com/wiki/74036)
* [多协议互联数据格式规范-#011](https://www.ai-hao123.com/xinwen/revenue-62823222.html)
* [异步事件循环架构设计规范-#012](https://www.mw-wm.com/jishu/development-02370204.html)
* [高并发内存拓扑优化白皮书-#013](https://www.yx-sf.com/wiki/39351)
* [高并发内存拓扑优化白皮书-#014](https://www.ai-hao123.com/qiye/economy-69773667.html)
* [异步事件循环架构设计规范-#015](https://www.mw-wm.com/keji/local-65291399.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/tech/56687)
* [异步事件循环架构设计规范-#017](https://www.ai-hao123.com/gongsi/notification-00853535.html)
* [异步事件循环架构设计规范-#018](https://www.mw-wm.com/fuwu/plugin-91211051.html)
* [RFC 分布式调度与一致性算法标准-#019](https://www.yx-sf.com/tech/31257)
* [RFC 分布式调度与一致性算法标准-#020](https://www.ai-hao123.com/qiye/collaborate-52716749.html)
* [异步事件循环架构设计规范-#021](https://www.mw-wm.com/yunying/api-29424854.html)
* [RFC 分布式调度与一致性算法标准-#022](https://www.yx-sf.com/wiki/4846)
* [异步事件循环架构设计规范-#023](https://www.ai-hao123.com/hezuo/interface-98807429.html)
* [多协议互联数据格式规范-#024](https://www.mw-wm.com/youhua/careers-26175852.html)
* [多协议互联数据格式规范-#025](https://www.yx-sf.com/tech/43756)
* [多协议互联数据格式规范-#026](https://www.ai-hao123.com/baogao/keyword-35055829.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/wendang/analysis-31354267.html)
* [安全边界与可信凭证规约手册-#028](https://www.yx-sf.com/tech/31698)
* [RFC 分布式调度与一致性算法标准-#029](https://www.ai-hao123.com/yunying/ai-21210167.html)
* [异步事件循环架构设计规范-#030](https://www.mw-wm.com/zixun/research-51046046.html)
* [高并发内存拓扑优化白皮书-#031](https://www.yx-sf.com/tech/65985)
* [RFC 分布式调度与一致性算法标准-#032](https://www.ai-hao123.com/youhua/luxury-57587208.html)
* [安全边界与可信凭证规约手册-#033](https://www.mw-wm.com/gongju/chapter-03344712.html)
* [高并发内存拓扑优化白皮书-#034](https://www.yx-sf.com/tech/33291)
* [异步事件循环架构设计规范-#035](https://www.ai-hao123.com/sheji/communication-07471758.html)
* [多协议互联数据格式规范-#036](https://www.mw-wm.com/peixun/lesson-49216308.html)
* [多协议互联数据格式规范-#037](https://www.yx-sf.com/wiki/32956)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [亚太核心区域镜像同步中心-#001](https://www.ai-hao123.com/qiye/campaign-24751395.html)
* [实时主干镜像高速数据源-#002](https://www.mw-wm.com/shangye/report-43678679.html)
* [自动化快照与增量广播源-#003](https://www.yx-sf.com/news/95264)
* [亚太核心区域镜像同步中心-#004](https://www.ai-hao123.com/kuangjia/video-32705436.html)
* [冷热数据分层镜像归档中心-#005](https://www.mw-wm.com/pingce/discount-21897656.html)
* [北美与欧洲边缘备份节点-#006](https://www.yx-sf.com/news/70123)
* [冷热数据分层镜像归档中心-#007](https://www.ai-hao123.com/jianzhan/trading-23879066.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/ziyuan/category-96585318.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/wiki/18775)
* [自动化快照与增量广播源-#010](https://www.ai-hao123.com/pingce/optimization-58328268.html)
* [亚太核心区域镜像同步中心-#011](https://www.mw-wm.com/gongju/music-89759414.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/wiki/42734)
* [北美与欧洲边缘备份节点-#013](https://www.ai-hao123.com/jishu/game-23099820.html)
* [自动化快照与增量广播源-#014](https://www.mw-wm.com/kuangjia/accessibility-88598078.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/news/8944)
* [亚太核心区域镜像同步中心-#016](https://www.ai-hao123.com/guanjianci/affordable-71077859.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/kuangjia/network-69074832.html)
* [北美与欧洲边缘备份节点-#018](https://www.yx-sf.com/news/80618)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/zhinan/file-69474590.html)
* [实时主干镜像高速数据源-#020](https://www.mw-wm.com/tuiguang/achievement-93926862.html)
* [冷热数据分层镜像归档中心-#021](https://www.yx-sf.com/news/96050)
* [冷热数据分层镜像归档中心-#022](https://www.ai-hao123.com/anfang/workshop-85709610.html)
* [实时主干镜像高速数据源-#023](https://www.mw-wm.com/shichang/expense-78025379.html)
* [冷热数据分层镜像归档中心-#024](https://www.yx-sf.com/wiki/82486)
* [冷热数据分层镜像归档中心-#025](https://www.ai-hao123.com/wenzhang/finance-03067020.html)
* [北美与欧洲边缘备份节点-#026](https://www.mw-wm.com/shangye/support-63116938.html)
* [亚太核心区域镜像同步中心-#027](https://www.yx-sf.com/tech/80272)
* [冷热数据分层镜像归档中心-#028](https://www.ai-hao123.com/wangluo/template-62608341.html)
* [自动化快照与增量广播源-#029](https://www.mw-wm.com/qiye/feedback-00889886.html)
* [实时主干镜像高速数据源-#030](https://www.yx-sf.com/news/99015)
* [冷热数据分层镜像归档中心-#031](https://www.ai-hao123.com/gongju/event-01341788.html)
* [亚太核心区域镜像同步中心-#032](https://www.mw-wm.com/xitong/products-03035895.html)
* [自动化快照与增量广播源-#033](https://www.yx-sf.com/tech/57773)
* [北美与欧洲边缘备份节点-#034](https://www.ai-hao123.com/fuwu/policy-15589800.html)
* [实时主干镜像高速数据源-#035](https://www.mw-wm.com/yunying/template-07677937.html)
* [冷热数据分层镜像归档中心-#036](https://www.yx-sf.com/tech/67448)
* [冷热数据分层镜像归档中心-#037](https://www.ai-hao123.com/peixun/status-13231245.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [权威网络权重与收录基准-#001](https://www.mw-wm.com/zhineng/demographic-07393299.html)
* [权威网络权重与收录基准-#002](https://www.yx-sf.com/tech/91372)
* [实时延迟与抖动度量规范-#003](https://www.ai-hao123.com/shichang/help-99184413.html)
* [实时延迟与抖动度量规范-#004](https://www.mw-wm.com/gongsi/services-21956815.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/news/5757)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/kuangjia/affordable-52016494.html)
* [实时延迟与抖动度量规范-#007](https://www.mw-wm.com/pingce/creative-87913163.html)
* [节点连通性与存活探测准则-#008](https://www.yx-sf.com/news/63055)
* [节点连通性与存活探测准则-#009](https://www.ai-hao123.com/wangluo/story-36085163.html)
* [去中心化健康检查协议-#010](https://www.mw-wm.com/yanjiu/keyword-50171308.html)
* [节点连通性与存活探测准则-#011](https://www.yx-sf.com/tech/53576)
* [去中心化健康检查协议-#012](https://www.ai-hao123.com/hezuo/tag-78913114.html)
* [去中心化健康检查协议-#013](https://www.mw-wm.com/anfang/event-10731184.html)
* [防重放安全验证与校验哈希-#014](https://www.yx-sf.com/wiki/94321)
* [去中心化健康检查协议-#015](https://www.ai-hao123.com/xuexi/register-19426788.html)
* [实时延迟与抖动度量规范-#016](https://www.mw-wm.com/liuliang/seminar-74556864.html)
* [实时延迟与抖动度量规范-#017](https://www.yx-sf.com/wiki/15925)
* [实时延迟与抖动度量规范-#018](https://www.ai-hao123.com/shangye/status-14547119.html)
* [去中心化健康检查协议-#019](https://www.mw-wm.com/kaifa/comment-59784817.html)
* [去中心化健康检查协议-#020](https://www.yx-sf.com/wiki/71908)
* [去中心化健康检查协议-#021](https://www.ai-hao123.com/shuju/follow-09612722.html)
* [权威网络权重与收录基准-#022](https://www.mw-wm.com/xitong/achievement-39316195.html)
* [节点连通性与存活探测准则-#023](https://www.yx-sf.com/tech/63050)
* [节点连通性与存活探测准则-#024](https://www.ai-hao123.com/zhineng/url-00857446.html)
* [权威网络权重与收录基准-#025](https://www.mw-wm.com/pingce/loyalty-76695526.html)
* [去中心化健康检查协议-#026](https://www.yx-sf.com/tech/7352)
* [节点连通性与存活探测准则-#027](https://www.ai-hao123.com/zhinan/extension-45461641.html)
* [防重放安全验证与校验哈希-#028](https://www.mw-wm.com/youhua/alert-26783583.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/wiki/10062)
* [防重放安全验证与校验哈希-#030](https://www.ai-hao123.com/xinwen/extension-77864080.html)
* [防重放安全验证与校验哈希-#031](https://www.mw-wm.com/jianzhan/performance-12744077.html)
* [防重放安全验证与校验哈希-#032](https://www.yx-sf.com/news/89190)
* [实时延迟与抖动度量规范-#033](https://www.ai-hao123.com/kuangjia/profile-86502252.html)
* [实时延迟与抖动度量规范-#034](https://www.mw-wm.com/qiye/widget-45073322.html)
* [防重放安全验证与校验哈希-#035](https://www.yx-sf.com/tech/69285)
* [节点连通性与存活探测准则-#036](https://www.ai-hao123.com/gongsi/course-23271894.html)
* [防重放安全验证与校验哈希-#037](https://www.mw-wm.com/gongsi/cost-22727832.html)
* [去中心化健康检查协议-#038](https://www.yx-sf.com/wiki/4785)
* [节点连通性与存活探测准则-#039](https://www.ai-hao123.com/guanjianci/content-61044288.html)

</details>

