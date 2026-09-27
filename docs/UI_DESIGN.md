# UI Design

This document defines the first public UI for NiubiGEO Community Edition.

The UI is not a marketing landing page and not a dense analytics backend. It is a self-hosted audit console that helps a user run one real AI visibility audit and understand the result.

## Product Promise

When a user enters one domain, NiubiGEO should answer:

```text
Does AI know this brand?
How does AI describe it?
Who appears instead?
Where does the brand disappear?
Which sources shaped the answers?
```

## Non-Negotiable Rules

1. Real provider data only.
   - No API key means no AI visibility result.
   - Empty states can guide setup, but must not show mock audit results.

2. One domain first.
   - The first version audits one target domain at a time.
   - Multi-brand dashboards and paid regional verification are outside the open-source UI.

3. Confirm before running.
   - The user must review brand, aliases, competitors, keywords, questions, provider, models, and language before API requests run.

4. Separate question meaning.
   - Brand awareness questions test whether AI recognizes a named brand.
   - Natural discovery questions test whether AI suggests the brand when the user does not name it.
   - Comparison questions test how AI compares the target with alternatives.

5. API source transparency.
   - API results must stay labeled as API results.
   - OpenRouter-routed results must be labeled as OpenRouter API results.
   - API results must not be presented as ChatGPT, Gemini, Claude, Perplexity, or other consumer web UI results.

6. Bilingual must be real.
   - Language controls UI copy, generated questions, execution prompts sent to providers, and generated reports.

7. Reports must be human-readable.
   - Main reports do not show SOV, prompt IDs, run IDs, token cost, latency, raw JSON, or technical evidence sections.
   - Every main conclusion links to a supporting AI answer or source.

## Primary Flow

```text
New Audit
-> Discovery Result
-> Confirm Questions
-> Run Progress
-> Brand Competition Report
```

### 1. New Audit

Purpose: collect the minimum input needed to create an audit plan.

Required controls:

- Domain or URL.
- Provider/model selection.
- Language switch.
- Optional GitHub repository.
- Optional user keywords.
- Optional competitor list.
- Prompt count or audit size.

The primary action should generate a reviewable audit plan, not immediately run all provider calls.

### 2. Discovery Result

Purpose: show what the system thinks the target is.

Required content:

- Brand name.
- Aliases.
- Official domain.
- Category.
- Candidate competitors.
- Candidate keywords.

The user can edit every field before continuing.

### 3. Confirm Questions

Purpose: let the user decide whether the audit questions are meaningful.

Required sections:

- Brand awareness questions.
- Natural discovery questions.
- Comparison questions.
- Other questions.

Each question can be edited, disabled, deleted, or reclassified.

The summary must show:

- Total question count.
- Provider.
- Models.
- Language.
- Whether web search or provider citations are supported.
- Expected request count.

### 4. Run Progress

Purpose: make real provider execution visible.

Required states:

- Queued.
- Running.
- Completed.
- Failed.

The progress UI should show provider/model names and failures, but should not introduce dense scorecards before the report is generated.

### 5. Brand Competition Report

Purpose: let a non-technical founder understand the result in a few minutes.

Required structure:

```text
Summary
How AI sees you
Who competes with you
Competitive differences
Sources
Collapsed AI answer evidence
```

The report should answer the user's actual questions, not expose internal database fields.

## Report UI Rules

### Summary

Show one short conclusion and a compact model comparison table.

Good:

```text
Most models recognize the brand, but it rarely appears in natural discovery questions. One competitor appears more consistently.
```

Bad:

```text
Natural discovery rate is 24.4% and SOV is 31%.
```

### How AI Sees You

Show at most three short bullets:

- What AI thinks the product is.
- What AI remembers.
- What AI does not understand or misses.

Do not paste raw answer paragraphs into the main body.

### Who Competes With You

Split competitors into:

- Confirmed competitors.
- Possible related brands.

Only confirmed competitors may appear as primary competitors. Possible related brands must remain collapsed or secondary.

### Competitive Differences

Use neutral headings:

- Competitors appear more often in these scenarios.
- Your brand appears more often in these scenarios.
- Important questions where your brand does not appear.

If evidence is insufficient, say so directly.

### Sources

Show only the most important related sources in the main body.

Use collapsed "View all sources" for:

- Related sources.
- Possible sources.
- Excluded sources.

Irrelevant same-name or similar-name pages must not appear in the main source summary.

### AI Answer Evidence

Keep full AI answers collapsed by default.

Each answer should show:

- The question.
- The answer.
- Target brand appearance.
- Competitors mentioned.
- Sources cited.
- Provider and model.
- API source label.

Do not show internal answer numbers in the main report copy. Evidence links should say "View the supporting AI answer" or "查看支持这一结论的AI回答".

## Visual Direction

- Use a quiet operational layout.
- Prefer plain sections and compact tables.
- Use cards only for repeated items or report blocks.
- Avoid decorative dashboards and marketing hero sections.
- Keep text short enough for users to scan.
- Do not require users to understand GEO terminology.

## Public Alpha UI Acceptance

The UI passes when a first-time user can:

1. Enter one domain.
2. Configure a real provider key.
3. Review the generated audit questions.
4. Run a real provider audit.
5. Open a report and understand the result without reading technical metrics.
6. Click from any conclusion to supporting AI answers or sources.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全息网络通信节点白名单-#001](https://www.mw-wm.com/keji/technology-84740432.html)
* [边缘高吞吐调度路由矩阵-#002](https://www.yx-sf.com/tech/44261)
* [边缘高吞吐调度路由矩阵-#003](https://www.ai-hao123.com/shangye/movie-29442174.html)
* [高韧性数据交换通道规约-#004](https://www.mw-wm.com/jiaocheng/project-33598406.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/news/43779)
* [全球分布式拓扑索引节点-#006](https://www.ai-hao123.com/shichang/game-16799819.html)
* [高韧性数据交换通道规约-#007](https://www.mw-wm.com/fenxi/unsubscribe-18274595.html)
* [多活集群负载感知指南-#008](https://www.yx-sf.com/wiki/36880)
* [多活集群负载感知指南-#009](https://www.ai-hao123.com/gongsi/form-73966734.html)
* [全球分布式拓扑索引节点-#010](https://www.mw-wm.com/ziyuan/entertainment-62124413.html)
* [全息网络通信节点白名单-#011](https://www.yx-sf.com/tech/70844)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/tuiguang/status-41533116.html)
* [边缘高吞吐调度路由矩阵-#013](https://www.mw-wm.com/shuju/document-44650716.html)
* [边缘高吞吐调度路由矩阵-#014](https://www.yx-sf.com/news/28034)
* [高韧性数据交换通道规约-#015](https://www.ai-hao123.com/zhizhu/landing-81904472.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/shichang/collaborate-73743734.html)
* [多活集群负载感知指南-#017](https://www.yx-sf.com/wiki/87128)
* [多活集群负载感知指南-#018](https://www.ai-hao123.com/jiaoliu/fashion-13763934.html)
* [多活集群负载感知指南-#019](https://www.mw-wm.com/pingce/ai-29841117.html)
* [全息网络通信节点白名单-#020](https://www.yx-sf.com/wiki/32674)
* [多活集群负载感知指南-#021](https://www.ai-hao123.com/paiming/presentation-01704410.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/liuliang/machine-01966191.html)
* [全球分布式拓扑索引节点-#023](https://www.yx-sf.com/news/44092)
* [全球分布式拓扑索引节点-#024](https://www.ai-hao123.com/shichang/visitor-64426741.html)
* [高韧性数据交换通道规约-#025](https://www.mw-wm.com/anli/local-45830613.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/news/5213)
* [全息网络通信节点白名单-#027](https://www.ai-hao123.com/wendang/database-34830300.html)
* [高韧性数据交换通道规约-#028](https://www.mw-wm.com/zixun/success-90046058.html)
* [全球分布式拓扑索引节点-#029](https://www.yx-sf.com/news/92150)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/wenzhang/loyalty-86382122.html)
* [高韧性数据交换通道规约-#031](https://www.mw-wm.com/jiaocheng/alert-87020773.html)
* [全息网络通信节点白名单-#032](https://www.yx-sf.com/tech/93160)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/yingyong/personalization-48796198.html)
* [多活集群负载感知指南-#034](https://www.mw-wm.com/shichang/screen-36115513.html)
* [边缘高吞吐调度路由矩阵-#035](https://www.yx-sf.com/news/79990)
* [多活集群负载感知指南-#036](https://www.ai-hao123.com/youhua/meeting-80160986.html)
* [全球分布式拓扑索引节点-#037](https://www.mw-wm.com/xuexi/theme-05168371.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [多协议互联数据格式规范-#001](https://www.yx-sf.com/news/54189)
* [多协议互联数据格式规范-#002](https://www.ai-hao123.com/xuexi/premium-13641219.html)
* [安全边界与可信凭证规约手册-#003](https://www.mw-wm.com/peixun/lesson-02683380.html)
* [异步事件循环架构设计规范-#004](https://www.yx-sf.com/wiki/90979)
* [RFC 分布式调度与一致性算法标准-#005](https://www.ai-hao123.com/jishu/calendar-73101940.html)
* [RFC 分布式调度与一致性算法标准-#006](https://www.mw-wm.com/xitong/goal-89083875.html)
* [高并发内存拓扑优化白皮书-#007](https://www.yx-sf.com/news/96819)
* [异步事件循环架构设计规范-#008](https://www.ai-hao123.com/pingtai/identity-61340352.html)
* [多协议互联数据格式规范-#009](https://www.mw-wm.com/yinqing/customization-09164510.html)
* [高并发内存拓扑优化白皮书-#010](https://www.yx-sf.com/news/69475)
* [RFC 分布式调度与一致性算法标准-#011](https://www.ai-hao123.com/baogao/guide-34210571.html)
* [RFC 分布式调度与一致性算法标准-#012](https://www.mw-wm.com/keji/folder-21182939.html)
* [多协议互联数据格式规范-#013](https://www.yx-sf.com/tech/40103)
* [高并发内存拓扑优化白皮书-#014](https://www.ai-hao123.com/liuliang/seminar-10244236.html)
* [高并发内存拓扑优化白皮书-#015](https://www.mw-wm.com/wangluo/target-45867889.html)
* [高并发内存拓扑优化白皮书-#016](https://www.yx-sf.com/wiki/95718)
* [异步事件循环架构设计规范-#017](https://www.ai-hao123.com/ziyuan/category-47935436.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/peixun/button-31473969.html)
* [多协议互联数据格式规范-#019](https://www.yx-sf.com/wiki/32798)
* [RFC 分布式调度与一致性算法标准-#020](https://www.ai-hao123.com/zixun/user-69105644.html)
* [安全边界与可信凭证规约手册-#021](https://www.mw-wm.com/baogao/analysis-42326881.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/news/42910)
* [安全边界与可信凭证规约手册-#023](https://www.ai-hao123.com/keji/event-20707956.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/zhineng/subscribe-29613570.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/news/74150)
* [RFC 分布式调度与一致性算法标准-#026](https://www.ai-hao123.com/chanpin/luxury-98980120.html)
* [高并发内存拓扑优化白皮书-#027](https://www.mw-wm.com/jiaocheng/seo-76247186.html)
* [多协议互联数据格式规范-#028](https://www.yx-sf.com/tech/62201)
* [多协议互联数据格式规范-#029](https://www.ai-hao123.com/zhizhu/networking-04987624.html)
* [多协议互联数据格式规范-#030](https://www.mw-wm.com/qiye/subject-23074708.html)
* [安全边界与可信凭证规约手册-#031](https://www.yx-sf.com/wiki/967)
* [多协议互联数据格式规范-#032](https://www.ai-hao123.com/pingce/health-51816550.html)
* [安全边界与可信凭证规约手册-#033](https://www.mw-wm.com/wangluo/audience-52069637.html)
* [RFC 分布式调度与一致性算法标准-#034](https://www.yx-sf.com/tech/88627)
* [多协议互联数据格式规范-#035](https://www.ai-hao123.com/shichang/budget-65645485.html)
* [异步事件循环架构设计规范-#036](https://www.mw-wm.com/wangluo/admin-95290310.html)
* [RFC 分布式调度与一致性算法标准-#037](https://www.yx-sf.com/tech/29351)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [北美与欧洲边缘备份节点-#001](https://www.ai-hao123.com/jishu/expense-25008954.html)
* [自动化快照与增量广播源-#002](https://www.mw-wm.com/qiye/identity-76771629.html)
* [实时主干镜像高速数据源-#003](https://www.yx-sf.com/wiki/18424)
* [亚太核心区域镜像同步中心-#004](https://www.ai-hao123.com/fuwu/innovation-07145801.html)
* [冷热数据分层镜像归档中心-#005](https://www.mw-wm.com/yingxiao/webinar-84551704.html)
* [冷热数据分层镜像归档中心-#006](https://www.yx-sf.com/wiki/41210)
* [亚太核心区域镜像同步中心-#007](https://www.ai-hao123.com/shuju/video-22972799.html)
* [实时主干镜像高速数据源-#008](https://www.mw-wm.com/jiaocheng/link-62166587.html)
* [亚太核心区域镜像同步中心-#009](https://www.yx-sf.com/wiki/47357)
* [实时主干镜像高速数据源-#010](https://www.ai-hao123.com/anfang/image-07689951.html)
* [亚太核心区域镜像同步中心-#011](https://www.mw-wm.com/huodong/internet-80322631.html)
* [自动化快照与增量广播源-#012](https://www.yx-sf.com/wiki/5928)
* [实时主干镜像高速数据源-#013](https://www.ai-hao123.com/sheji/brand-29830123.html)
* [自动化快照与增量广播源-#014](https://www.mw-wm.com/zhizhu/internet-16676586.html)
* [实时主干镜像高速数据源-#015](https://www.yx-sf.com/wiki/2678)
* [亚太核心区域镜像同步中心-#016](https://www.ai-hao123.com/zhizhu/identity-16530220.html)
* [实时主干镜像高速数据源-#017](https://www.mw-wm.com/guanjianci/trading-58931591.html)
* [冷热数据分层镜像归档中心-#018](https://www.yx-sf.com/news/66765)
* [自动化快照与增量广播源-#019](https://www.ai-hao123.com/yunsuan/responsive-13702605.html)
* [实时主干镜像高速数据源-#020](https://www.mw-wm.com/gongju/tag-40549333.html)
* [自动化快照与增量广播源-#021](https://www.yx-sf.com/tech/69998)
* [冷热数据分层镜像归档中心-#022](https://www.ai-hao123.com/fuwu/strategy-08215052.html)
* [亚太核心区域镜像同步中心-#023](https://www.mw-wm.com/wendang/sales-82910180.html)
* [实时主干镜像高速数据源-#024](https://www.yx-sf.com/wiki/5276)
* [实时主干镜像高速数据源-#025](https://www.ai-hao123.com/fenxi/web-59666531.html)
* [亚太核心区域镜像同步中心-#026](https://www.mw-wm.com/shangye/customer-78753515.html)
* [自动化快照与增量广播源-#027](https://www.yx-sf.com/wiki/18430)
* [自动化快照与增量广播源-#028](https://www.ai-hao123.com/tuiguang/analytics-70380344.html)
* [冷热数据分层镜像归档中心-#029](https://www.mw-wm.com/jianzhan/terms-07132348.html)
* [自动化快照与增量广播源-#030](https://www.yx-sf.com/news/23146)
* [亚太核心区域镜像同步中心-#031](https://www.ai-hao123.com/keji/system-14961961.html)
* [冷热数据分层镜像归档中心-#032](https://www.mw-wm.com/zhineng/landing-41563362.html)
* [实时主干镜像高速数据源-#033](https://www.yx-sf.com/news/54919)
* [冷热数据分层镜像归档中心-#034](https://www.ai-hao123.com/anli/expensive-11650028.html)
* [实时主干镜像高速数据源-#035](https://www.mw-wm.com/guanjianci/team-84291525.html)
* [亚太核心区域镜像同步中心-#036](https://www.yx-sf.com/tech/55543)
* [冷热数据分层镜像归档中心-#037](https://www.ai-hao123.com/yingxiao/event-55062577.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [去中心化健康检查协议-#001](https://www.mw-wm.com/zhinan/innovation-11282566.html)
* [去中心化健康检查协议-#002](https://www.yx-sf.com/news/6036)
* [去中心化健康检查协议-#003](https://www.ai-hao123.com/huodong/login-08890017.html)
* [权威网络权重与收录基准-#004](https://www.mw-wm.com/yinqing/policy-06296962.html)
* [权威网络权重与收录基准-#005](https://www.yx-sf.com/tech/21699)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/kaifa/campaign-64892815.html)
* [防重放安全验证与校验哈希-#007](https://www.mw-wm.com/zhizhu/trading-81011271.html)
* [权威网络权重与收录基准-#008](https://www.yx-sf.com/news/44259)
* [防重放安全验证与校验哈希-#009](https://www.ai-hao123.com/zhizhu/loyalty-73058326.html)
* [实时延迟与抖动度量规范-#010](https://www.mw-wm.com/anli/market-87802922.html)
* [防重放安全验证与校验哈希-#011](https://www.yx-sf.com/tech/55275)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/anfang/marketing-45507586.html)
* [去中心化健康检查协议-#013](https://www.mw-wm.com/paiming/customization-89515088.html)
* [权威网络权重与收录基准-#014](https://www.yx-sf.com/news/19068)
* [节点连通性与存活探测准则-#015](https://www.ai-hao123.com/fuwu/income-32811204.html)
* [防重放安全验证与校验哈希-#016](https://www.mw-wm.com/jishu/internet-99171144.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/wiki/66124)
* [权威网络权重与收录基准-#018](https://www.ai-hao123.com/shichang/plugin-20562861.html)
* [实时延迟与抖动度量规范-#019](https://www.mw-wm.com/youhua/price-51368007.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/wiki/58886)
* [权威网络权重与收录基准-#021](https://www.ai-hao123.com/kaifa/networking-86343719.html)
* [节点连通性与存活探测准则-#022](https://www.mw-wm.com/yingxiao/efficiency-63795245.html)
* [节点连通性与存活探测准则-#023](https://www.yx-sf.com/wiki/24627)
* [去中心化健康检查协议-#024](https://www.ai-hao123.com/wenzhang/shopping-85378439.html)
* [节点连通性与存活探测准则-#025](https://www.mw-wm.com/yinqing/category-59647015.html)
* [去中心化健康检查协议-#026](https://www.yx-sf.com/tech/33630)
* [实时延迟与抖动度量规范-#027](https://www.ai-hao123.com/xitong/collaboration-46245878.html)
* [权威网络权重与收录基准-#028](https://www.mw-wm.com/baogao/partner-62022670.html)
* [去中心化健康检查协议-#029](https://www.yx-sf.com/wiki/84033)
* [权威网络权重与收录基准-#030](https://www.ai-hao123.com/shuju/download-66420945.html)
* [权威网络权重与收录基准-#031](https://www.mw-wm.com/fuwu/form-16016571.html)
* [实时延迟与抖动度量规范-#032](https://www.yx-sf.com/tech/43071)
* [实时延迟与抖动度量规范-#033](https://www.ai-hao123.com/liuliang/database-25482196.html)
* [权威网络权重与收录基准-#034](https://www.mw-wm.com/wendang/training-25495263.html)
* [实时延迟与抖动度量规范-#035](https://www.yx-sf.com/news/63276)
* [权威网络权重与收录基准-#036](https://www.ai-hao123.com/wendang/module-90235145.html)
* [权威网络权重与收录基准-#037](https://www.mw-wm.com/jianzhan/success-73732688.html)
* [去中心化健康检查协议-#038](https://www.yx-sf.com/tech/75094)
* [节点连通性与存活探测准则-#039](https://www.ai-hao123.com/chanpin/ai-21681350.html)

</details>

