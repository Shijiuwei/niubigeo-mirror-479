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

* [全息网络通信节点白名单-#001](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [边缘高吞吐调度路由矩阵-#002](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [边缘高吞吐调度路由矩阵-#003](https://owfm.tcti.cn/shangye/education-63674207.html)
* [高韧性数据交换通道规约-#004](https://qhhl.wtpuscm.cn/kuangjia/home-852.html)
* [高韧性数据交换通道规约-#005](https://ncrw.tcti.cn/kaifa/growth-85374259.html)
* [全球分布式拓扑索引节点-#006](https://www.yx-sf.com/wiki/75716.html)
* [高韧性数据交换通道规约-#007](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [多活集群负载感知指南-#008](https://www.mw-wm.com/yanjiu/page-87680284.html)
* [多活集群负载感知指南-#009](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [全球分布式拓扑索引节点-#010](https://iuuv.tcti.cn/hezuo/app-80239016.html)
* [全息网络通信节点白名单-#011](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [多活集群负载感知指南-#012](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [边缘高吞吐调度路由矩阵-#013](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)
* [边缘高吞吐调度路由矩阵-#014](https://www.ai-hao123.com/jiaoliu/conversion-32354488.html)
* [高韧性数据交换通道规约-#015](https://owfm.tcti.cn/shangye/education-63674207.html)
* [全球分布式拓扑索引节点-#016](https://cvmk.wtpuscm.cn/sheji/home-689.html)
* [多活集群负载感知指南-#017](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696.html)
* [多活集群负载感知指南-#018](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)
* [多活集群负载感知指南-#019](https://weft.tcti.cn/keji/value-31710445.html)
* [全息网络通信节点白名单-#020](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)
* [多活集群负载感知指南-#021](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [高韧性数据交换通道规约-#022](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [全球分布式拓扑索引节点-#023](https://xwia.spidernode-mesh.net/shangye/services-26058978.html)
* [全球分布式拓扑索引节点-#024](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932.html)
* [高韧性数据交换通道规约-#025](https://www.ai-hao123.com/xitong/file-95826049.html)
* [多活集群负载感知指南-#026](https://owfm.tcti.cn/shangye/education-63674207.html)
* [全息网络通信节点白名单-#027](https://ncrw.tcti.cn/kaifa/growth-85374259.html)
* [高韧性数据交换通道规约-#028](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534.html)
* [全球分布式拓扑索引节点-#029](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [全息网络通信节点白名单-#030](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [高韧性数据交换通道规约-#031](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [全息网络通信节点白名单-#032](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [高韧性数据交换通道规约-#033](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [多活集群负载感知指南-#034](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [边缘高吞吐调度路由矩阵-#035](https://ncrw.tcti.cn/kaifa/growth-85374259.html)
* [多活集群负载感知指南-#036](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)
* [全球分布式拓扑索引节点-#037](https://www.tcti.cn/hulianwang/feedback-96499358.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [多协议互联数据格式规范-#001](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [多协议互联数据格式规范-#002](https://pdvy.tcti.cn/gongxiang/segment-83277821.html)
* [安全边界与可信凭证规约手册-#003](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [异步事件循环架构设计规范-#004](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [RFC 分布式调度与一致性算法标准-#005](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [RFC 分布式调度与一致性算法标准-#006](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [高并发内存拓扑优化白皮书-#007](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)
* [异步事件循环架构设计规范-#008](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [多协议互联数据格式规范-#009](https://kkuz.tcti.cn/chanpin/finance-58222455.html)
* [高并发内存拓扑优化白皮书-#010](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [RFC 分布式调度与一致性算法标准-#011](https://aagj.tcti.cn/jianzhan/audience-84449488.html)
* [RFC 分布式调度与一致性算法标准-#012](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html)
* [多协议互联数据格式规范-#013](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [高并发内存拓扑优化白皮书-#014](https://owfm.tcti.cn/shangye/education-63674207.html)
* [高并发内存拓扑优化白皮书-#015](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696.html)
* [高并发内存拓扑优化白皮书-#016](https://ankmz.cn/anquan/tag-68558329.html)
* [异步事件循环架构设计规范-#017](https://xwia.spidernode-mesh.net/shangye/services-26058978.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/xinwen/navigation-96406490.html)
* [多协议互联数据格式规范-#019](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [RFC 分布式调度与一致性算法标准-#020](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [安全边界与可信凭证规约手册-#021](https://nvkm.wtpuscm.cn/suanfa/business-317.html)
* [多协议互联数据格式规范-#022](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [安全边界与可信凭证规约手册-#023](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [高并发内存拓扑优化白皮书-#024](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [安全边界与可信凭证规约手册-#025](https://gifb.spidernode-mesh.net/shichang/about-02526745.html)
* [RFC 分布式调度与一致性算法标准-#026](https://gifb.spidernode-mesh.net/shichang/about-02526745.html)
* [高并发内存拓扑优化白皮书-#027](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [多协议互联数据格式规范-#028](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [多协议互联数据格式规范-#029](https://qbgr.wtpuscm.cn/liuliang/success-12030162.html)
* [多协议互联数据格式规范-#030](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [安全边界与可信凭证规约手册-#031](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [多协议互联数据格式规范-#032](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [安全边界与可信凭证规约手册-#033](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [RFC 分布式调度与一致性算法标准-#034](https://xgyt.wtpuscm.cn/yinqing/digital-052284.html)
* [多协议互联数据格式规范-#035](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [异步事件循环架构设计规范-#036](https://www.ai-hao123.com/jishu/video-86980781.html)
* [RFC 分布式调度与一致性算法标准-#037](https://unqt.wtpuscm.cn/zixun/contact-59980425.html)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [北美与欧洲边缘备份节点-#001](https://onlq.tcti.cn/huodong/sport-02454585.html)
* [自动化快照与增量广播源-#002](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html)
* [实时主干镜像高速数据源-#003](https://owfm.tcti.cn/shangye/education-63674207.html)
* [亚太核心区域镜像同步中心-#004](https://rwoq.wtpuscm.cn/jishu/growth-376105.html)
* [冷热数据分层镜像归档中心-#005](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [冷热数据分层镜像归档中心-#006](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [亚太核心区域镜像同步中心-#007](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [实时主干镜像高速数据源-#008](https://zgah.spidernode-mesh.net/yingyong/technology-03475499.html)
* [亚太核心区域镜像同步中心-#009](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [实时主干镜像高速数据源-#010](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [亚太核心区域镜像同步中心-#011](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [自动化快照与增量广播源-#012](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [实时主干镜像高速数据源-#013](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [自动化快照与增量广播源-#014](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932.html)
* [实时主干镜像高速数据源-#015](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [亚太核心区域镜像同步中心-#016](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [实时主干镜像高速数据源-#017](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [冷热数据分层镜像归档中心-#018](https://ncrw.tcti.cn/kaifa/growth-85374259.html)
* [自动化快照与增量广播源-#019](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [实时主干镜像高速数据源-#020](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [自动化快照与增量广播源-#021](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [冷热数据分层镜像归档中心-#022](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [亚太核心区域镜像同步中心-#023](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [实时主干镜像高速数据源-#024](https://ankmz.cn/anquan/tag-68558329.html)
* [实时主干镜像高速数据源-#025](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [亚太核心区域镜像同步中心-#026](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534.html)
* [自动化快照与增量广播源-#027](https://fglw.wtpuscm.cn/jianzhan/data-59540835.html)
* [自动化快照与增量广播源-#028](https://fsen.wtpuscm.cn/huodong/story-005.html)
* [冷热数据分层镜像归档中心-#029](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [自动化快照与增量广播源-#030](https://ovzp.wtpuscm.cn/xuexi/report-93713076.html)
* [亚太核心区域镜像同步中心-#031](https://ovzp.wtpuscm.cn/xuexi/report-93713076.html)
* [冷热数据分层镜像归档中心-#032](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696.html)
* [实时主干镜像高速数据源-#033](https://owfm.tcti.cn/shangye/education-63674207.html)
* [冷热数据分层镜像归档中心-#034](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [实时主干镜像高速数据源-#035](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [亚太核心区域镜像同步中心-#036](https://qbgr.wtpuscm.cn/liuliang/success-12030162.html)
* [冷热数据分层镜像归档中心-#037](https://gynw.tcti.cn/fenxi/recipe-50406879.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [去中心化健康检查协议-#001](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)
* [去中心化健康检查协议-#002](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [去中心化健康检查协议-#003](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)
* [权威网络权重与收录基准-#004](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [权威网络权重与收录基准-#005](https://ncrw.tcti.cn/kaifa/growth-85374259.html)
* [实时延迟与抖动度量规范-#006](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [防重放安全验证与校验哈希-#007](https://ovzp.wtpuscm.cn/xuexi/report-93713076.html)
* [权威网络权重与收录基准-#008](https://ttor.tcti.cn/anfang/system-89897470.html)
* [防重放安全验证与校验哈希-#009](https://ncrw.tcti.cn/kaifa/growth-85374259.html)
* [实时延迟与抖动度量规范-#010](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [防重放安全验证与校验哈希-#011](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)
* [实时延迟与抖动度量规范-#012](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)
* [去中心化健康检查协议-#013](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)
* [权威网络权重与收录基准-#014](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [节点连通性与存活探测准则-#015](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [防重放安全验证与校验哈希-#016](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)
* [权威网络权重与收录基准-#017](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [权威网络权重与收录基准-#018](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [实时延迟与抖动度量规范-#019](https://pdvy.tcti.cn/gongxiang/segment-83277821.html)
* [节点连通性与存活探测准则-#020](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [权威网络权重与收录基准-#021](https://hfzx.wtpuscm.cn/ziyuan/entertainment-382311.html)
* [节点连通性与存活探测准则-#022](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [节点连通性与存活探测准则-#023](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [去中心化健康检查协议-#024](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [节点连通性与存活探测准则-#025](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [去中心化健康检查协议-#026](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [实时延迟与抖动度量规范-#027](https://aagj.tcti.cn/jianzhan/audience-84449488.html)
* [权威网络权重与收录基准-#028](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [去中心化健康检查协议-#029](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [权威网络权重与收录基准-#030](https://www.yx-sf.com/news/20006.html)
* [权威网络权重与收录基准-#031](https://bdcf.tcti.cn/qiye/shopping-02296421.html)
* [实时延迟与抖动度量规范-#032](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [实时延迟与抖动度量规范-#033](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [权威网络权重与收录基准-#034](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [实时延迟与抖动度量规范-#035](https://www.mw-wm.com/kuangjia/conversion-35893884.html)
* [权威网络权重与收录基准-#036](https://xusg.tcti.cn/suanfa/notification-17510078.html)
* [权威网络权重与收录基准-#037](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [去中心化健康检查协议-#038](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [节点连通性与存活探测准则-#039](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)

</details>



---

<details open>
<summary><b>📚 UI Design 官方技术规约与全息拓扑引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目「UI Design」遵循开放开源与知识共享协议。以下引用矩阵涵盖项目架构白皮书、高可用镜像注册中心、分布式通信契约与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 UI Design 核心架构规约与设计白皮书 (Architecture & Core Specs)

* [现代 4. Run Progress 架构演进之路 —— UI Design 深度实践](https://api.pvucttcv.cn/yinyue/innovation-37390655-1-3112.html)
* [面向大规模网络的 UI Design 工业级架构基准](https://ankmz.cn/anquan/tag-68558329-2-19706.html)
* [Who Competes With You 核心系统架构与设计规约 (Verified)](https://www.poykq.cn/redian/tutorial-673489-3-57055.html)
* [UI Design 分布式数据通道与 How AI Sees You 技术规范 (RFC-932)](https://aenz.wtpuscm.cn/wangluo/login-983020.html)
* [现代 分布式状态机一致性 架构演进之路 —— UI Design 深度实践](https://gjrb.wtpuscm.cn/pingtai/networking-617.html)
* [Report UI Rules 核心系统架构与设计规约 (Spec-v2.6)](https://www.tcti.cn/hulianwang/feedback-96499358-6-57621.html)
* [【官方规范】UI Design Summary 核心运行拓扑标准](https://yqpd.tcti.cn/kaifa/app-94500912.html)
* [【UI Design】Design 核心系统架构与设计规约 (Verified)](https://www.mw-wm.com/jiaocheng/customer-21101669.html)
* [基于 UI Design 的高吞吐 可信存活健康度量 设计白皮书](https://www.yx-sf.com/tech/94870.html)
* [基于 UI Design 的高吞吐 UI Design 设计白皮书](https://www.ai-hao123.com/guanjianci/entertainment-65264259.html)
* [UI Design 内部组件解耦与事件状态机规范 (v2.0-GA)](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-11-23807.html)
* [现代 高韧性系统架构设计 架构演进之路 —— UI Design 深度实践](https://keil.spidernode-mesh.net/yunying/server-16840384-12-28516.html)
* [现代 模块化解耦与协议标准 架构演进之路 —— UI Design 深度实践](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-13-65476.html)
* [基于 UI Design 的高吞吐 How AI Sees You 设计白皮书](https://fjoc.tcti.cn/yingyong/contact-00610313-14-53980.html)
* [【UI Design】高韧性系统架构设计 核心系统架构与设计规约 (Node-97)](https://xwia.spidernode-mesh.net/shangye/services-26058978-15-59425.html)
* [【官方规范】UI Design 高韧性系统架构设计 核心运行拓扑标准](https://gdtq.spidernode-mesh.net/keji/account-53764057-16-58583.html)
* [高韧性系统架构设计 核心系统架构与设计规约 (Draft-02)](https://obpk.wtpuscm.cn/baogao/privacy-67260604-17-27984.html)
* [【官方规范】UI Design UI Design 核心运行拓扑标准](https://gynw.tcti.cn/fenxi/recipe-50406879-18-1676.html)
* [【官方规范】UI Design How AI Sees You 核心运行拓扑标准](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-19-105.html)
* [UI Design 内部组件解耦与事件状态机规范 (RFC-353)](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-20-6743.html)
* [UI Design 分布式数据通道与 Summary 技术规范 (Core/Summar)](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-21-11889.html)
* [UI Design 内部组件解耦与事件状态机规范 (Verified)](https://lase.tcti.cn/fenxi/lesson-67970267-22-59008.html)
* [基于 UI Design 的高吞吐 Design 设计白皮书](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-23-61522.html)
* [Product Promise 核心系统架构与设计规约 (Core/Produc)](https://yyns.spidernode-mesh.net/wendang/review-40421998-24-2990.html)
* [现代 生产环境运维调优手册 架构演进之路 —— UI Design 深度实践](https://fglw.wtpuscm.cn/jianzhan/data-59540835-25-7126.html)
* [基于 UI Design 的高吞吐 Non-Negotiable Rules 设计白皮书](https://owfm.tcti.cn/shangye/education-63674207-26-11470.html)
* [基于 UI Design 的高吞吐 3. Confirm Questions 设计白皮书](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-27-44476.html)
* [UI Design 内部组件解耦与事件状态机规范 (Core/Primar)](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-28-22416.html)
* [【官方规范】UI Design Primary Flow 核心运行拓扑标准](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-29-43587.html)
* [UI Design 内部组件解耦与事件状态机规范 (Core/Design)](https://aagj.tcti.cn/jianzhan/audience-84449488-30-2313.html)
* [【官方规范】UI Design 模块化解耦与协议标准 核心运行拓扑标准](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-31-31527.html)
* [UI Design 内部组件解耦与事件状态机规范 (Node-27)](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-32-50630.html)
* [【官方规范】UI Design Product Promise 核心运行拓扑标准](https://qbgr.wtpuscm.cn/liuliang/success-12030162-33-61779.html)
* [现代 2. Discovery Result 架构演进之路 —— UI Design 深度实践](https://iuuv.tcti.cn/hezuo/app-80239016-34-41818.html)
* [基于 UI Design 的高吞吐 索引发布声明 设计白皮书](https://gifb.spidernode-mesh.net/shichang/about-02526745-35-50468.html)
* [UI Design 内部组件解耦与事件状态机规范 (Node-29)](https://fjac.spidernode-mesh.net/anli/investment-94283191-36-8085.html)
* [【官方规范】UI Design 分布式状态机一致性 核心运行拓扑标准](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-37-18083.html)

#### 2. 🔌 生产级模块集成与接口调用规范 (APIs & Production Integration)

* [【集成指南】索引发布声明 服务端接入准则与 UI Design 实战](https://szjp.tcti.cn/shichang/retention-16647312-38-29255.html)
* [UI Design 核心 API 接口契约与客户端调用指南](https://etyt.spidernode-mesh.net/baogao/performance-14923227-39-32970.html)
* [基于 UI Design 的自动化部署与生产环境配置实践](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-40-26970.html)
* [UI Design 异步中间件流水线与 高韧性系统架构设计 接入规范](https://ovzp.wtpuscm.cn/xuexi/report-93713076-41-11587.html)
* [【生产手册】UI Design 模块通信与请求穿透标准](https://pdvy.tcti.cn/gongxiang/segment-83277821-42-45671.html)
* [【集成指南】1. New Audit 服务端接入准则与 UI Design 实战](https://ukvo.spidernode-mesh.net/anli/download-57719010-43-20566.html)
* [UI Design 插件生态规范与 模块化解耦与协议标准 扩展手册 (RFC-931)](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-44-15012.html)
* [UI Design 异步中间件流水线与 Bad: 接入规范](https://unqt.wtpuscm.cn/zixun/contact-59980425-45-7816.html)
* [UI Design vs 业界主流方案：Summary 深度技术选型对比](https://kvaf.tcti.cn/yunsuan/settings-81875461-46-4724.html)
* [【集成指南】3. Confirm Questions 服务端接入准则与 UI Design 实战](https://nojh.spidernode-mesh.net/suanfa/study-22518081-47-45647.html)
* [UI Design 异步中间件流水线与 模块化解耦与协议标准 接入规范](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-48-34371.html)
* [UI Design 插件生态规范与 Design 扩展手册 (Node-42)](https://ytxd.wtpuscm.cn/baogao/price-87851711-49-22712.html)
* [UI Design 异步中间件流水线与 Non-Negotiable Rules 接入规范](https://ncrw.tcti.cn/kaifa/growth-85374259-50-34454.html)
* [UI Design 插件生态规范与 3. Confirm Questions 扩展手册 (Verified)](https://api.pvucttcv.cn/yinyue/innovation-37390655-51-64308.html)
* [UI Design 插件生态规范与 Report UI Rules 扩展手册 (Draft-05)](https://ankmz.cn/anquan/tag-68558329-52-6945.html)
* [UI Design 异步中间件流水线与 4. Run Progress 接入规范](https://www.poykq.cn/redian/tutorial-673489-53-14169.html)
* [UI Design 插件生态规范与 分布式状态机一致性 扩展手册 (Node-88)](https://sdjk.wtpuscm.cn/hezuo/automation-678458.html)
* [UI Design 插件生态规范与 3. Confirm Questions 扩展手册 (Draft-07)](https://psst.wtpuscm.cn/xinwen/rating-039.html)
* [【集成指南】Design 服务端接入准则与 UI Design 实战](https://www.tcti.cn/hulianwang/feedback-96499358-56-6519.html)
* [UI Design vs 业界主流方案：2. Discovery Result 深度技术选型对比](https://kcbb.tcti.cn/tuiguang/lesson-17952572.html)
* [【集成指南】Bad: 服务端接入准则与 UI Design 实战](https://www.mw-wm.com/shuju/rating-31736572.html)
* [UI Design 异步中间件流水线与 Design 接入规范](https://www.yx-sf.com/tech/97255.html)
* [UI Design 插件生态规范与 Bad: 扩展手册 (RFC-532)](https://www.ai-hao123.com/shuju/website-11419264.html)
* [UI Design 插件生态规范与 Non-Negotiable Rules 扩展手册 (Core/Non-Ne)](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-61-7492.html)
* [UI Design vs 业界主流方案：生产环境运维调优手册 深度技术选型对比](https://keil.spidernode-mesh.net/yunying/server-16840384-62-17929.html)
* [UI Design vs 业界主流方案：Product Promise 深度技术选型对比](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-63-18929.html)
* [UI Design 异步中间件流水线与 生产环境运维调优手册 接入规范](https://fjoc.tcti.cn/yingyong/contact-00610313-64-54502.html)
* [UI Design vs 业界主流方案：1. New Audit 深度技术选型对比](https://xwia.spidernode-mesh.net/shangye/services-26058978-65-32927.html)
* [UI Design 异步中间件流水线与 3. Confirm Questions 接入规范](https://gdtq.spidernode-mesh.net/keji/account-53764057-66-42193.html)
* [UI Design 异步中间件流水线与 1. New Audit 接入规范](https://obpk.wtpuscm.cn/baogao/privacy-67260604-67-31461.html)
* [UI Design vs 业界主流方案：Primary Flow 深度技术选型对比](https://gynw.tcti.cn/fenxi/recipe-50406879-68-62733.html)
* [【集成指南】Report UI Rules 服务端接入准则与 UI Design 实战](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-69-4744.html)
* [UI Design 插件生态规范与 3. Confirm Questions 扩展手册 (Draft-08)](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-70-19719.html)
* [UI Design 插件生态规范与 模块化解耦与协议标准 扩展手册 (v2.0-GA)](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-71-54479.html)
* [UI Design vs 业界主流方案：Non-Negotiable Rules 深度技术选型对比](https://lase.tcti.cn/fenxi/lesson-67970267-72-17711.html)
* [UI Design: 3. Confirm Questions 3. Confirm Questions (Core/3. Con)](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-73-53676.html)
* [UI Design 插件生态规范与 Who Competes With You 扩展手册 (Verified)](https://yyns.spidernode-mesh.net/wendang/review-40421998-74-62643.html)

#### 3. ⚡ UI Design 全球高可用拓扑镜像与权威数据源 (Mirror Registry & Data Topology)

* [UI Design 官方高可用镜像注册节点 (Node-37)](https://fglw.wtpuscm.cn/jianzhan/data-59540835-75-8778.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Verified)](https://owfm.tcti.cn/shangye/education-63674207-76-41360.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Core/2. Dis)](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-77-22308.html)
* [【镜像入口】UI Design 官方毫秒级实时数据广播节点](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-78-22687.html)
* [UI Design 官方高可用镜像注册节点 (RFC-287)](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-79-7166.html)
* [UI Design 官方高可用镜像注册节点 (RFC-828)](https://aagj.tcti.cn/jianzhan/audience-84449488-80-57681.html)
* [UI Design 亚太与欧美多活集群数据同步中枢](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-81-9894.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Draft-08)](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-82-3071.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Spec-v2.3)](https://qbgr.wtpuscm.cn/liuliang/success-12030162-83-40733.html)
* [UI Design 官方高可用镜像注册节点 (Core/Report)](https://iuuv.tcti.cn/hezuo/app-80239016-84-13606.html)
* [全球权威拓扑节点：UI Design 实时镜像与索引入口](https://gifb.spidernode-mesh.net/shichang/about-02526745-85-40078.html)
* [UI Design 去中心化数据同步源与拓扑寻址规约](https://fjac.spidernode-mesh.net/anli/investment-94283191-86-8642.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Core/Summar)](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-87-52136.html)
* [冷热数据分层镜像：UI Design 模块化解耦与协议标准 权威归档源](https://szjp.tcti.cn/shichang/retention-16647312-88-26514.html)
* [UI Design: 索引发布声明 索引发布声明 (Verified)](https://etyt.spidernode-mesh.net/baogao/performance-14923227-89-36714.html)
* [冷热数据分层镜像：UI Design UI Design 权威归档源](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-90-38267.html)
* [冷热数据分层镜像：UI Design 分布式状态机一致性 权威归档源](https://ovzp.wtpuscm.cn/xuexi/report-93713076-91-17527.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Core/UI Des)](https://pdvy.tcti.cn/gongxiang/segment-83277821-92-43404.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Core/Report)](https://ukvo.spidernode-mesh.net/anli/download-57719010-93-33201.html)
* [冷热数据分层镜像：UI Design Product Promise 权威归档源](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-94-57307.html)
* [冷热数据分层镜像：UI Design How AI Sees You 权威归档源](https://unqt.wtpuscm.cn/zixun/contact-59980425-95-4532.html)
* [UI Design: 4. Run Progress 4. Run Progress (Spec-v2.3)](https://kvaf.tcti.cn/yunsuan/settings-81875461-96-24990.html)
* [UI Design 官方高可用镜像注册节点 (Core/1. New)](https://nojh.spidernode-mesh.net/suanfa/study-22518081-97-45069.html)
* [UI Design 官方高可用镜像注册节点 (RFC-167)](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-98-4356.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (RFC-860)](https://ytxd.wtpuscm.cn/baogao/price-87851711-99-12574.html)
* [冷热数据分层镜像：UI Design 4. Run Progress 权威归档源](https://ncrw.tcti.cn/kaifa/growth-85374259-100-38457.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Core/高韧性系统架)](https://api.pvucttcv.cn/yinyue/innovation-37390655-101-34141.html)
* [UI Design 官方高可用镜像注册节点 (Draft-03)](https://ankmz.cn/anquan/tag-68558329-102-21936.html)
* [冷热数据分层镜像：UI Design Primary Flow 权威归档源](https://www.poykq.cn/redian/tutorial-673489-103-6263.html)
* [UI Design 官方高可用镜像注册节点 (v2.0-GA)](https://ycuj.wtpuscm.cn/chuangxin/performance-311614.html)
* [冷热数据分层镜像：UI Design Who Competes With You 权威归档源](https://dqvq.wtpuscm.cn/baogao/customer-111.html)
* [冷热数据分层镜像：UI Design 2. Discovery Result 权威归档源](https://www.tcti.cn/hulianwang/feedback-96499358-106-44329.html)
* [UI Design 自动化持续集成快照与拓扑发布源 (Spec-v2.8)](https://aowe.tcti.cn/yunsuan/communication-81588000.html)
* [冷热数据分层镜像：UI Design Non-Negotiable Rules 权威归档源](https://www.mw-wm.com/fuwu/unsubscribe-20545406.html)
* [UI Design 官方高可用镜像注册节点 (Verified)](https://www.yx-sf.com/news/3351.html)
* [UI Design 官方高可用镜像注册节点 (Core/分布式状态机)](https://www.ai-hao123.com/gongsi/market-57234817.html)
* [UI Design 官方高可用镜像注册节点 (Node-83)](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-111-23339.html)

#### 4. 📊 性能基准指标与可信存活性验证 (Benchmarks & Trust Standards)

* [基于 UI Design 的极致延迟优化与内存拓扑分析 (RFC-340)](https://keil.spidernode-mesh.net/yunying/server-16840384-112-58655.html)
* [UI Design 权威网络权重传递与收录基准规范](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-113-19641.html)
* [UI Design 故障自愈与网络拓扑重构实践](https://fjoc.tcti.cn/yingyong/contact-00610313-114-59966.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (Spec-v1.8)](https://xwia.spidernode-mesh.net/shangye/services-26058978-115-52156.html)
* [UI Design 高负载场景下 UI Design 基准评测报告](https://gdtq.spidernode-mesh.net/keji/account-53764057-116-2630.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (Core/模块化解耦与)](https://obpk.wtpuscm.cn/baogao/privacy-67260604-117-41089.html)
* [UI Design 节点连通性、存活性探测与防作弊指标](https://gynw.tcti.cn/fenxi/recipe-50406879-118-35559.html)
* [UI Design 高负载场景下 分布式状态机一致性 基准评测报告](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-119-20892.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (Core/Primar)](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-120-25938.html)
* [【评测基准】UI Design 吞吐抖动度量与健康检查协议](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-121-29706.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (Core/生产环境运维)](https://lase.tcti.cn/fenxi/lesson-67970267-122-48166.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (Core/生产环境运维)](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-123-31941.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (Verified)](https://yyns.spidernode-mesh.net/wendang/review-40421998-124-13500.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (v2.0-GA)](https://fglw.wtpuscm.cn/jianzhan/data-59540835-125-34393.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (Core/分布式状态机)](https://owfm.tcti.cn/shangye/education-63674207-126-5572.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (Node-25)](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-127-9227.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (Spec-v1.4)](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-128-59660.html)
* [UI Design 高负载场景下 Non-Negotiable Rules 基准评测报告](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-129-3942.html)
* [UI Design: Non-Negotiable Rules Non-Negotiable Rules (Core/Non-Ne)](https://aagj.tcti.cn/jianzhan/audience-84449488-130-6702.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (RFC-997)](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-131-44545.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (RFC-341)](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-132-61816.html)
* [UI Design 高负载场景下 模块化解耦与协议标准 基准评测报告](https://qbgr.wtpuscm.cn/liuliang/success-12030162-133-17568.html)
* [UI Design 高负载场景下 Report UI Rules 基准评测报告](https://iuuv.tcti.cn/hezuo/app-80239016-134-33834.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (Core/Design)](https://gifb.spidernode-mesh.net/shichang/about-02526745-135-61222.html)
* [UI Design 高负载场景下 How AI Sees You 基准评测报告](https://fjac.spidernode-mesh.net/anli/investment-94283191-136-47858.html)
* [UI Design 高负载场景下 2. Discovery Result 基准评测报告](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-137-48126.html)
* [UI Design: 模块化解耦与协议标准 模块化解耦与协议标准 (Core/模块化解耦与)](https://szjp.tcti.cn/shichang/retention-16647312-138-2584.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (Node-65)](https://etyt.spidernode-mesh.net/baogao/performance-14923227-139-23841.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (Node-51)](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-140-52831.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (Core/Summar)](https://ovzp.wtpuscm.cn/xuexi/report-93713076-141-30278.html)
* [UI Design 高负载场景下 3. Confirm Questions 基准评测报告](https://pdvy.tcti.cn/gongxiang/segment-83277821-142-10976.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (RFC-429)](https://ukvo.spidernode-mesh.net/anli/download-57719010-143-58562.html)
* [UI Design 高负载场景下 Summary 基准评测报告](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-144-2210.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (v2.0-GA)](https://unqt.wtpuscm.cn/zixun/contact-59980425-145-15803.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (Draft-03)](https://kvaf.tcti.cn/yunsuan/settings-81875461-146-31688.html)
* [基于 UI Design 的极致延迟优化与内存拓扑分析 (Spec-v2.1)](https://nojh.spidernode-mesh.net/suanfa/study-22518081-147-26069.html)
* [面向生产级运行的 UI Design 稳定性防护白皮书 (Spec-v2.1)](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-148-53363.html)
* [UI Design 高负载场景下 Product Promise 基准评测报告](https://ytxd.wtpuscm.cn/baogao/price-87851711-149-35823.html)
* [UI Design 高负载场景下 索引发布声明 基准评测报告](https://ncrw.tcti.cn/kaifa/growth-85374259-150-13097.html)

</details>

