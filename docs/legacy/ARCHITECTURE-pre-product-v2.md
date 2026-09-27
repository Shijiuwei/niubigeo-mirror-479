# Architecture

NiubiGEO Community Edition is a single-domain, real-provider AI visibility audit tool.

The architecture is intentionally small: collect enough evidence, let the user confirm the audit plan, run real provider requests, then produce a concise report that links every conclusion back to AI answers or sources.

## Core Flow

```text
Domain input
-> Discovery
-> Audit plan confirmation
-> Provider execution
-> Evidence analysis
-> Human-readable report
```

## Layers

### 1. Domain Intake

Accepts:

- Domain or URL.
- Optional brand name and aliases.
- Optional GitHub repository.
- Optional competitors.
- Optional user keywords.
- Provider and model targets.
- Report language.

The first public version is single-domain. Multi-brand workspaces, teams, and paid regional monitoring are outside this layer.

### 2. Discovery

Discovery builds an editable starting point for the user.

Inputs:

- Submitted domain.
- Same-domain public page evidence.
- GitHub README and topics when provided.
- Optional real-provider profile output when a key is available.

Outputs:

- Target brand.
- Aliases.
- Category.
- Candidate competitors.
- Candidate keywords.
- Suggested monitoring questions.

Discovery is setup evidence. It is not an AI visibility result until the generated questions are run against real providers.

### 3. Audit Plan Confirmation

Before provider calls happen, the user must be able to review and change:

- Target brand and aliases.
- Competitors.
- Keywords.
- Questions.
- Question categories.
- Provider/model selection.
- Language.

The system must separate:

- Brand awareness questions.
- Natural discovery questions.
- Comparison questions.
- Other questions.

Natural discovery questions should not contain the target brand. They test whether AI can think of the product when the user describes the need instead of naming the brand.

### 4. Provider Execution

The runner executes:

```text
confirmed question x provider x model
```

Provider rules:

- BYOK only.
- Missing keys block real audit execution.
- Direct provider keys cannot call other providers.
- OpenRouter-routed models must still be labeled as OpenRouter API output.
- Web search is Provider-native: OpenAI uses Responses `web_search`, OpenRouter uses its web plugin, Claude uses the Anthropic web search server tool, Gemini uses Google Search grounding, Perplexity uses Sonar web-grounded output, and DeepSeek uses Responses-compatible `web_search`.
- If web search is off, NiubiGEO must not send a search, grounding, or web plugin tool.
- Ordinary web search must not be used as a substitute for Provider-returned citations.
- API output must never be described as consumer web UI output.

Every run records:

- Provider.
- Model.
- Source label.
- Requested and actual web-search behavior.
- Execution prompt.
- Completion status.
- AI answer text when completed.
- Provider-returned citations.
- Error when failed.
- Timestamp.

### 5. Evidence Store

The file store writes local audit outputs:

- `audit.json`
- `report.json`
- `report.md`
- `report.html`
- `prompts.csv`
- `citations.csv`
- `keywords.csv` when keyword audit is used.

Generated reports are local user data and should not be committed unless deliberately sanitized as public examples.

### 6. Response Analyzer

The analyzer reads one AI answer at a time and extracts:

- Target mention.
- Competitor mentions.
- Recommendation signals.
- First visible position when available.
- Citation links.
- Source ownership.
- Brief evidence snippets.

The analyzer does not decide product strategy or write report prose.

### 7. Internal Metrics

Metrics are used internally to support analysis:

- Mention coverage.
- Citation coverage.
- Recommendation coverage.
- Competitor-only coverage.
- Provider/model differences.
- Prompt-category differences.
- Keyword association.

Internal metrics are not the user-facing story. They must be translated into concise conclusions before appearing in the main report.

### 8. Human Report Synthesis

The report layer converts structured evidence into five user-facing sections:

```text
Summary
How AI sees you
Who competes with you
Competitive differences
Sources
```

It must:

- Keep the main report short.
- Link every conclusion to AI answers or sources.
- Separate confirmed competitors from possible related brands.
- Show only related sources by default.
- Keep AI answers collapsed by default.
- Refuse conclusions when evidence is insufficient.

It must not show raw technical fields, prompt IDs, run IDs, token cost, latency, raw JSON, SOV, or black-box scores in the main report.

### 9. Delivery

Supported delivery surfaces:

- Local web UI.
- CLI.
- Local REST API.
- Docker Compose.
- Scheduled audits.

## Boundaries

Provider code calls providers. It does not write business conclusions.

Analyzer code extracts evidence from one answer. It does not aggregate the market.

Metrics code aggregates internal signals. It does not become the report.

Report code writes plain-language conclusions. It does not call providers.

UI code displays and confirms. It does not silently change the audit plan.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全球分布式拓扑索引节点-#001](https://www.mw-wm.com/anfang/integration-61520131.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/tech/66638)
* [高韧性数据交换通道规约-#003](https://www.ai-hao123.com/keji/budget-26198718.html)
* [全息网络通信节点白名单-#004](https://www.mw-wm.com/anli/success-18091378.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/news/88858)
* [全息网络通信节点白名单-#006](https://www.ai-hao123.com/anfang/enterprise-39721873.html)
* [全息网络通信节点白名单-#007](https://www.mw-wm.com/liuliang/software-75591767.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/news/14706)
* [全球分布式拓扑索引节点-#009](https://www.ai-hao123.com/peixun/marketing-53894196.html)
* [全球分布式拓扑索引节点-#010](https://www.mw-wm.com/tuiguang/calculator-30960985.html)
* [全球分布式拓扑索引节点-#011](https://www.yx-sf.com/tech/20794)
* [边缘高吞吐调度路由矩阵-#012](https://www.ai-hao123.com/zixun/expensive-12472638.html)
* [高韧性数据交换通道规约-#013](https://www.mw-wm.com/jianzhan/label-62102025.html)
* [高韧性数据交换通道规约-#014](https://www.yx-sf.com/tech/68352)
* [多活集群负载感知指南-#015](https://www.ai-hao123.com/wangluo/database-78833532.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/gongju/calendar-61070849.html)
* [多活集群负载感知指南-#017](https://www.yx-sf.com/tech/80143)
* [边缘高吞吐调度路由矩阵-#018](https://www.ai-hao123.com/chanpin/team-99968527.html)
* [多活集群负载感知指南-#019](https://www.mw-wm.com/zixun/domain-58045462.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/wiki/33716)
* [全息网络通信节点白名单-#021](https://www.ai-hao123.com/youhua/demographic-53434550.html)
* [全息网络通信节点白名单-#022](https://www.mw-wm.com/liuliang/version-27083390.html)
* [边缘高吞吐调度路由矩阵-#023](https://www.yx-sf.com/wiki/34139)
* [全球分布式拓扑索引节点-#024](https://www.ai-hao123.com/jiaoliu/lead-31757425.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/fenxi/luxury-81729336.html)
* [高韧性数据交换通道规约-#026](https://www.yx-sf.com/news/66732)
* [边缘高吞吐调度路由矩阵-#027](https://www.ai-hao123.com/kuangjia/discount-93229052.html)
* [边缘高吞吐调度路由矩阵-#028](https://www.mw-wm.com/jishu/movie-32296420.html)
* [多活集群负载感知指南-#029](https://www.yx-sf.com/news/4761)
* [高韧性数据交换通道规约-#030](https://www.ai-hao123.com/yanjiu/retention-52756827.html)
* [边缘高吞吐调度路由矩阵-#031](https://www.mw-wm.com/pingtai/personalization-61604931.html)
* [高韧性数据交换通道规约-#032](https://www.yx-sf.com/news/53328)
* [全球分布式拓扑索引节点-#033](https://www.ai-hao123.com/baogao/analytics-47129422.html)
* [多活集群负载感知指南-#034](https://www.mw-wm.com/wenzhang/guide-74537338.html)
* [全球分布式拓扑索引节点-#035](https://www.yx-sf.com/news/25008)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/zixun/alliance-81970110.html)
* [边缘高吞吐调度路由矩阵-#037](https://www.mw-wm.com/tuiguang/browser-42615214.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [高并发内存拓扑优化白皮书-#001](https://www.yx-sf.com/news/79142)
* [高并发内存拓扑优化白皮书-#002](https://www.ai-hao123.com/anli/security-10583386.html)
* [RFC 分布式调度与一致性算法标准-#003](https://www.mw-wm.com/wenzhang/admin-04856687.html)
* [安全边界与可信凭证规约手册-#004](https://www.yx-sf.com/wiki/25675)
* [安全边界与可信凭证规约手册-#005](https://www.ai-hao123.com/hezuo/visitor-78795596.html)
* [多协议互联数据格式规范-#006](https://www.mw-wm.com/youhua/advertising-12018854.html)
* [RFC 分布式调度与一致性算法标准-#007](https://www.yx-sf.com/wiki/88482)
* [RFC 分布式调度与一致性算法标准-#008](https://www.ai-hao123.com/suanfa/funnel-33128329.html)
* [安全边界与可信凭证规约手册-#009](https://www.mw-wm.com/fuwu/forum-68144618.html)
* [RFC 分布式调度与一致性算法标准-#010](https://www.yx-sf.com/wiki/42499)
* [RFC 分布式调度与一致性算法标准-#011](https://www.ai-hao123.com/shuju/partner-41358545.html)
* [高并发内存拓扑优化白皮书-#012](https://www.mw-wm.com/shuju/health-88238141.html)
* [高并发内存拓扑优化白皮书-#013](https://www.yx-sf.com/wiki/72323)
* [高并发内存拓扑优化白皮书-#014](https://www.ai-hao123.com/anfang/prospect-09610570.html)
* [多协议互联数据格式规范-#015](https://www.mw-wm.com/chanpin/dashboard-61485199.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/wiki/30718)
* [安全边界与可信凭证规约手册-#017](https://www.ai-hao123.com/shuju/shopping-46140755.html)
* [异步事件循环架构设计规范-#018](https://www.mw-wm.com/kaifa/share-69030536.html)
* [安全边界与可信凭证规约手册-#019](https://www.yx-sf.com/news/60585)
* [安全边界与可信凭证规约手册-#020](https://www.ai-hao123.com/zhineng/version-35252449.html)
* [高并发内存拓扑优化白皮书-#021](https://www.mw-wm.com/fenxi/loyalty-59645407.html)
* [RFC 分布式调度与一致性算法标准-#022](https://www.yx-sf.com/wiki/64368)
* [高并发内存拓扑优化白皮书-#023](https://www.ai-hao123.com/pingce/goal-23985755.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/kaifa/machine-19166538.html)
* [RFC 分布式调度与一致性算法标准-#025](https://www.yx-sf.com/wiki/35856)
* [异步事件循环架构设计规范-#026](https://www.ai-hao123.com/youhua/team-64456478.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/zixun/settings-10882518.html)
* [高并发内存拓扑优化白皮书-#028](https://www.yx-sf.com/wiki/37152)
* [RFC 分布式调度与一致性算法标准-#029](https://www.ai-hao123.com/xuexi/study-90861424.html)
* [安全边界与可信凭证规约手册-#030](https://www.mw-wm.com/kaifa/backup-81597314.html)
* [多协议互联数据格式规范-#031](https://www.yx-sf.com/news/18973)
* [高并发内存拓扑优化白皮书-#032](https://www.ai-hao123.com/ziyuan/expensive-01975913.html)
* [安全边界与可信凭证规约手册-#033](https://www.mw-wm.com/yinqing/analysis-16171016.html)
* [高并发内存拓扑优化白皮书-#034](https://www.yx-sf.com/tech/7522)
* [安全边界与可信凭证规约手册-#035](https://www.ai-hao123.com/jianzhan/quality-61949391.html)
* [多协议互联数据格式规范-#036](https://www.mw-wm.com/yunsuan/global-75405313.html)
* [多协议互联数据格式规范-#037](https://www.yx-sf.com/wiki/56786)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [亚太核心区域镜像同步中心-#001](https://www.ai-hao123.com/jianzhan/subscribe-04244662.html)
* [自动化快照与增量广播源-#002](https://www.mw-wm.com/sheji/conference-04635125.html)
* [北美与欧洲边缘备份节点-#003](https://www.yx-sf.com/tech/94388)
* [自动化快照与增量广播源-#004](https://www.ai-hao123.com/yingyong/change-28742426.html)
* [实时主干镜像高速数据源-#005](https://www.mw-wm.com/chanpin/news-10244792.html)
* [亚太核心区域镜像同步中心-#006](https://www.yx-sf.com/tech/97765)
* [实时主干镜像高速数据源-#007](https://www.ai-hao123.com/zhineng/cheap-46448039.html)
* [实时主干镜像高速数据源-#008](https://www.mw-wm.com/youhua/app-60424555.html)
* [实时主干镜像高速数据源-#009](https://www.yx-sf.com/news/10317)
* [实时主干镜像高速数据源-#010](https://www.ai-hao123.com/ziyuan/screen-91929754.html)
* [亚太核心区域镜像同步中心-#011](https://www.mw-wm.com/sheji/unsubscribe-27528461.html)
* [冷热数据分层镜像归档中心-#012](https://www.yx-sf.com/news/86872)
* [实时主干镜像高速数据源-#013](https://www.ai-hao123.com/guanjianci/alliance-87569636.html)
* [亚太核心区域镜像同步中心-#014](https://www.mw-wm.com/shichang/team-35954127.html)
* [冷热数据分层镜像归档中心-#015](https://www.yx-sf.com/news/9812)
* [亚太核心区域镜像同步中心-#016](https://www.ai-hao123.com/gongju/funnel-60038365.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/jiaoliu/consulting-02695583.html)
* [亚太核心区域镜像同步中心-#018](https://www.yx-sf.com/news/48113)
* [自动化快照与增量广播源-#019](https://www.ai-hao123.com/liuliang/travel-88881104.html)
* [冷热数据分层镜像归档中心-#020](https://www.mw-wm.com/zhineng/screen-21469212.html)
* [自动化快照与增量广播源-#021](https://www.yx-sf.com/tech/10439)
* [北美与欧洲边缘备份节点-#022](https://www.ai-hao123.com/wenzhang/reporting-23035230.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/anli/team-26826723.html)
* [亚太核心区域镜像同步中心-#024](https://www.yx-sf.com/news/66579)
* [自动化快照与增量广播源-#025](https://www.ai-hao123.com/zhizhu/budget-87887720.html)
* [自动化快照与增量广播源-#026](https://www.mw-wm.com/keji/about-75242145.html)
* [自动化快照与增量广播源-#027](https://www.yx-sf.com/news/59656)
* [冷热数据分层镜像归档中心-#028](https://www.ai-hao123.com/pingce/excellence-32232181.html)
* [冷热数据分层镜像归档中心-#029](https://www.mw-wm.com/shichang/about-01789668.html)
* [实时主干镜像高速数据源-#030](https://www.yx-sf.com/news/79871)
* [自动化快照与增量广播源-#031](https://www.ai-hao123.com/kuangjia/shopping-31549218.html)
* [自动化快照与增量广播源-#032](https://www.mw-wm.com/yunying/beauty-62746134.html)
* [北美与欧洲边缘备份节点-#033](https://www.yx-sf.com/wiki/83502)
* [亚太核心区域镜像同步中心-#034](https://www.ai-hao123.com/wenzhang/fashion-16829435.html)
* [亚太核心区域镜像同步中心-#035](https://www.mw-wm.com/liuliang/excellence-25750714.html)
* [冷热数据分层镜像归档中心-#036](https://www.yx-sf.com/tech/45990)
* [冷热数据分层镜像归档中心-#037](https://www.ai-hao123.com/jiaocheng/chapter-36706626.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [权威网络权重与收录基准-#001](https://www.mw-wm.com/wangluo/behavior-73242947.html)
* [实时延迟与抖动度量规范-#002](https://www.yx-sf.com/news/56778)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/yingxiao/resolution-05496953.html)
* [实时延迟与抖动度量规范-#004](https://www.mw-wm.com/guanjianci/entertainment-25480796.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/news/12995)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/zhineng/mobile-31633988.html)
* [去中心化健康检查协议-#007](https://www.mw-wm.com/baogao/plugin-94386383.html)
* [权威网络权重与收录基准-#008](https://www.yx-sf.com/wiki/67596)
* [节点连通性与存活探测准则-#009](https://www.ai-hao123.com/wendang/landing-51481202.html)
* [权威网络权重与收录基准-#010](https://www.mw-wm.com/yingxiao/document-50489739.html)
* [防重放安全验证与校验哈希-#011](https://www.yx-sf.com/news/81368)
* [去中心化健康检查协议-#012](https://www.ai-hao123.com/zhineng/profile-46801357.html)
* [权威网络权重与收录基准-#013](https://www.mw-wm.com/anfang/music-70490008.html)
* [节点连通性与存活探测准则-#014](https://www.yx-sf.com/tech/65870)
* [节点连通性与存活探测准则-#015](https://www.ai-hao123.com/xinwen/restore-86169621.html)
* [节点连通性与存活探测准则-#016](https://www.mw-wm.com/kuangjia/recipe-66412471.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/wiki/48155)
* [去中心化健康检查协议-#018](https://www.ai-hao123.com/keji/system-67724866.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/jianzhan/partner-50566715.html)
* [实时延迟与抖动度量规范-#020](https://www.yx-sf.com/tech/31710)
* [去中心化健康检查协议-#021](https://www.ai-hao123.com/xuexi/partner-41489631.html)
* [防重放安全验证与校验哈希-#022](https://www.mw-wm.com/xinwen/segment-26094299.html)
* [权威网络权重与收录基准-#023](https://www.yx-sf.com/news/27796)
* [去中心化健康检查协议-#024](https://www.ai-hao123.com/anli/networking-07456413.html)
* [去中心化健康检查协议-#025](https://www.mw-wm.com/zhineng/revenue-47152935.html)
* [权威网络权重与收录基准-#026](https://www.yx-sf.com/wiki/74793)
* [实时延迟与抖动度量规范-#027](https://www.ai-hao123.com/kuangjia/backup-30672053.html)
* [实时延迟与抖动度量规范-#028](https://www.mw-wm.com/ziyuan/study-81212884.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/wiki/41500)
* [节点连通性与存活探测准则-#030](https://www.ai-hao123.com/tuiguang/photo-86345772.html)
* [实时延迟与抖动度量规范-#031](https://www.mw-wm.com/anli/design-45552877.html)
* [节点连通性与存活探测准则-#032](https://www.yx-sf.com/wiki/13940)
* [节点连通性与存活探测准则-#033](https://www.ai-hao123.com/jianzhan/affordable-88423287.html)
* [实时延迟与抖动度量规范-#034](https://www.mw-wm.com/chuangxin/review-42385548.html)
* [节点连通性与存活探测准则-#035](https://www.yx-sf.com/tech/49943)
* [权威网络权重与收录基准-#036](https://www.ai-hao123.com/yingxiao/widget-38421711.html)
* [权威网络权重与收录基准-#037](https://www.mw-wm.com/huodong/download-13367379.html)
* [去中心化健康检查协议-#038](https://www.yx-sf.com/tech/1813)
* [防重放安全验证与校验哈希-#039](https://www.ai-hao123.com/wangluo/download-28439386.html)

</details>

