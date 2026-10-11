# Capability Matrix

This document is the implementation contract for NiubiGEO Community Edition.

A capability counts as complete only when real-provider code exists, self-checks exist, and user-facing reports expose evidence in plain language.

## Reference Capability Mapping

| Source project | Core idea to reuse | NiubiGEO Community Edition requirement | Code owner |
|---|---|---|---|
| Elmo | Brand, competitor, prompt, prompt run, citation, snapshot, report data loop | Store target entity, competitors, prompts, runs, citations, audit bundle, and report bundle | `src/core/types.ts`, `src/store/file-store.ts` |
| Elmo | Prompt fan-out by model and time | Run confirmed prompts across selected real providers and models | `src/runner/audit-runner.ts` |
| Elmo | Metrics can be recomputed from stored evidence | Keep internal mention, citation, recommendation, and competitor coverage metrics recomputable from completed runs | `src/metrics/metrics-engine.ts` |
| Elmo | REST API and self-hosting | Local HTTP API plus Docker Compose for self-hosting | `src/server.ts`, `Dockerfile`, `docker-compose.yml` |
| Aperture | BYOK provider setup | Load provider-specific keys from environment; missing keys block real audits | `src/config/env.ts` |
| Aperture | Provider catalog as source of truth | One catalog drives UI, CLI, and API validation | `src/providers/catalog.ts` |
| Aperture | Audit lifecycle | Every run records completed or failed state, provider, model, answer text, citations, and error if any | `src/runner/audit-runner.ts` |
| OneGlanse | Source transparency | Every result labels API source clearly and never implies browser UI or human-verified output | `src/providers/*`, `src/report/*` |
| OneGlanse | User-facing answer evidence | Reports link conclusions to actual AI answers without exposing internal IDs in the main copy | `src/report/report-builder.ts`, `src/report/report-html.ts` |
| AiCMO | Generated monitoring prompts | Generate brand awareness, natural discovery, comparison, alternative, and scenario prompts; generated prompts must be confirmed and run against real providers | `src/prompts/*` |
| AiCMO | Marketer-readable reporting | Convert metrics into concise answers to founder questions instead of showing technical scorecards | `src/report/human-report.ts` |
| Citatra | Citation and source intelligence | Classify provider citations into related, possible, and excluded sources | `src/analyzer/citation-intelligence.ts`, `src/report/human-report.ts` |
| Citatra | Competitor source discipline | Confirm competitors only when name, official domain, and product description are supported | `src/report/human-report.ts` |
| Elmo / AiCMO | Branded vs unbranded prompts | Separate direct brand awareness from natural discovery; do not mix them into one visible score | `src/prompts/domain-prompt-planner.ts`, `src/metrics/metrics-engine.ts` |
| OneGlanse / AiCMO / Citatra | Diagnostic explanation | Show where the target appears, where competitors appear instead, and which sources shaped the answer | `src/insights/gap-analyzer.ts`, `src/report/human-report.ts` |
| GitHub-first onboarding | Domain and repository evidence | Use site evidence, SEO metadata, GitHub README/topics, and user keywords to build prompt plans, without treating site evidence as AI visibility | `src/profile/*`, `src/keywords/*` |

## Non-Negotiable Checks

- No mock provider can be registered in the core catalog.
- Missing provider keys must fail before real audit execution.
- Direct provider keys cannot cross provider boundaries.
- OpenRouter-routed output must be labeled as OpenRouter API output.
- API output must never be described as ChatGPT, Gemini, Claude, Perplexity, or other consumer web UI output.
- Ordinary web search must never be used as a substitute for provider citations.
- Generated prompts must be shown for user confirmation before running.
- Brand awareness, natural discovery, and comparison prompts must remain separate.
- Every user-facing conclusion must link to an AI answer, a provider citation, or site evidence.
- Main reports must not expose SOV, prompt IDs, run IDs, token cost, latency, raw JSON, or technical evidence sections.
- Confirmed competitors must have entity evidence; unclear same-name entities must remain possible related brands.
- Main source sections must show only related sources; possible and excluded sources must be collapsed.
- Generated reports must be understandable without knowing GEO, SOV, prompt matrices, or provider internals.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [高韧性数据交换通道规约-#001](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [全息网络通信节点白名单-#002](https://gifb.spidernode-mesh.net/shichang/about-02526745.html)
* [全息网络通信节点白名单-#003](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)
* [全息网络通信节点白名单-#004](https://ankmz.cn/anquan/tag-68558329.html)
* [全球分布式拓扑索引节点-#005](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [全息网络通信节点白名单-#006](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [全息网络通信节点白名单-#007](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [多活集群负载感知指南-#008](https://pdvy.tcti.cn/gongxiang/segment-83277821.html)
* [高韧性数据交换通道规约-#009](https://unqt.wtpuscm.cn/zixun/contact-59980425.html)
* [全息网络通信节点白名单-#010](https://ojnc.tcti.cn/xitong/prospect-97305426.html)
* [全息网络通信节点白名单-#011](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [多活集群负载感知指南-#012](https://www.poykq.cn/redian/tutorial-673489.html)
* [全球分布式拓扑索引节点-#013](https://iejh.wtpuscm.cn/pingtai/tool-760980.html)
* [多活集群负载感知指南-#014](https://www.poykq.cn/redian/tutorial-673489.html)
* [全息网络通信节点白名单-#015](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html)
* [多活集群负载感知指南-#016](https://gxpl.wtpuscm.cn/kaifa/platform-785624.html)
* [多活集群负载感知指南-#017](https://www.poykq.cn/redian/tutorial-673489.html)
* [多活集群负载感知指南-#018](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [全息网络通信节点白名单-#019](https://wwgb.wtpuscm.cn/tuiguang/brand-102510.html)
* [高韧性数据交换通道规约-#020](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [边缘高吞吐调度路由矩阵-#021](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [多活集群负载感知指南-#022](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [全息网络通信节点白名单-#023](https://qbgr.wtpuscm.cn/liuliang/success-12030162.html)
* [全球分布式拓扑索引节点-#024](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [全息网络通信节点白名单-#025](https://ossc.wtpuscm.cn/wendang/webinar-112.html)
* [边缘高吞吐调度路由矩阵-#026](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534.html)
* [多活集群负载感知指南-#027](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [边缘高吞吐调度路由矩阵-#028](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [边缘高吞吐调度路由矩阵-#029](https://ankmz.cn/anquan/tag-68558329.html)
* [全息网络通信节点白名单-#030](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [多活集群负载感知指南-#031](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html)
* [全息网络通信节点白名单-#032](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [高韧性数据交换通道规约-#033](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [边缘高吞吐调度路由矩阵-#034](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [高韧性数据交换通道规约-#035](https://ptwp.tcti.cn/shangye/campaign-92126966.html)
* [全球分布式拓扑索引节点-#036](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [多活集群负载感知指南-#037](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [多协议互联数据格式规范-#001](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [RFC 分布式调度与一致性算法标准-#002](https://iuuv.tcti.cn/hezuo/app-80239016.html)
* [多协议互联数据格式规范-#003](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [高并发内存拓扑优化白皮书-#004](https://pdvy.tcti.cn/gongxiang/segment-83277821.html)
* [RFC 分布式调度与一致性算法标准-#005](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932.html)
* [高并发内存拓扑优化白皮书-#006](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [安全边界与可信凭证规约手册-#007](https://qbgr.wtpuscm.cn/liuliang/success-12030162.html)
* [安全边界与可信凭证规约手册-#008](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [异步事件循环架构设计规范-#009](https://lorv.tcti.cn/zixun/strategy-88384335.html)
* [异步事件循环架构设计规范-#010](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [异步事件循环架构设计规范-#011](https://www.ai-hao123.com/zhineng/vendor-13300411.html)
* [安全边界与可信凭证规约手册-#012](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [异步事件循环架构设计规范-#013](https://wnyd.wtpuscm.cn/sheji/policy-735495.html)
* [RFC 分布式调度与一致性算法标准-#014](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [异步事件循环架构设计规范-#015](https://unqt.wtpuscm.cn/zixun/contact-59980425.html)
* [异步事件循环架构设计规范-#016](https://aagj.tcti.cn/jianzhan/audience-84449488.html)
* [异步事件循环架构设计规范-#017](https://xwia.spidernode-mesh.net/shangye/services-26058978.html)
* [RFC 分布式调度与一致性算法标准-#018](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [高并发内存拓扑优化白皮书-#019](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [多协议互联数据格式规范-#020](https://ankmz.cn/anquan/tag-68558329.html)
* [高并发内存拓扑优化白皮书-#021](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [RFC 分布式调度与一致性算法标准-#022](https://www.yx-sf.com/news/47219.html)
* [多协议互联数据格式规范-#023](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [RFC 分布式调度与一致性算法标准-#024](https://iuuv.tcti.cn/hezuo/app-80239016.html)
* [多协议互联数据格式规范-#025](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)
* [多协议互联数据格式规范-#026](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [高并发内存拓扑优化白皮书-#027](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [RFC 分布式调度与一致性算法标准-#028](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [安全边界与可信凭证规约手册-#029](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932.html)
* [高并发内存拓扑优化白皮书-#030](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [多协议互联数据格式规范-#031](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [RFC 分布式调度与一致性算法标准-#032](https://www.yx-sf.com/wiki/61021.html)
* [高并发内存拓扑优化白皮书-#033](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)
* [安全边界与可信凭证规约手册-#034](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [高并发内存拓扑优化白皮书-#035](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [多协议互联数据格式规范-#036](https://umvl.wtpuscm.cn/xitong/subscribe-145670.html)
* [多协议互联数据格式规范-#037](https://keil.spidernode-mesh.net/yunying/server-16840384.html)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [亚太核心区域镜像同步中心-#001](https://gifb.spidernode-mesh.net/shichang/about-02526745.html)
* [自动化快照与增量广播源-#002](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [实时主干镜像高速数据源-#003](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [实时主干镜像高速数据源-#004](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [亚太核心区域镜像同步中心-#005](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [实时主干镜像高速数据源-#006](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [北美与欧洲边缘备份节点-#007](https://dvnb.tcti.cn/peixun/subscribe-04399356.html)
* [冷热数据分层镜像归档中心-#008](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [亚太核心区域镜像同步中心-#009](https://pdvy.tcti.cn/gongxiang/segment-83277821.html)
* [冷热数据分层镜像归档中心-#010](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [实时主干镜像高速数据源-#011](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [北美与欧洲边缘备份节点-#012](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [冷热数据分层镜像归档中心-#013](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [自动化快照与增量广播源-#014](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [亚太核心区域镜像同步中心-#015](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [亚太核心区域镜像同步中心-#016](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [亚太核心区域镜像同步中心-#017](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [冷热数据分层镜像归档中心-#018](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [北美与欧洲边缘备份节点-#019](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [亚太核心区域镜像同步中心-#020](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [自动化快照与增量广播源-#021](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [亚太核心区域镜像同步中心-#022](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [实时主干镜像高速数据源-#023](https://ysue.tcti.cn/pingtai/planning-49077101.html)
* [冷热数据分层镜像归档中心-#024](https://gifb.spidernode-mesh.net/shichang/about-02526745.html)
* [自动化快照与增量广播源-#025](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [冷热数据分层镜像归档中心-#026](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [自动化快照与增量广播源-#027](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [亚太核心区域镜像同步中心-#028](https://xcro.wtpuscm.cn/wenzhang/policy-123.html)
* [冷热数据分层镜像归档中心-#029](https://www.poykq.cn/redian/tutorial-673489.html)
* [北美与欧洲边缘备份节点-#030](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [实时主干镜像高速数据源-#031](https://unqt.wtpuscm.cn/zixun/contact-59980425.html)
* [冷热数据分层镜像归档中心-#032](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [亚太核心区域镜像同步中心-#033](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [亚太核心区域镜像同步中心-#034](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [自动化快照与增量广播源-#035](https://www.mw-wm.com/xinwen/notification-89291977.html)
* [实时主干镜像高速数据源-#036](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [北美与欧洲边缘备份节点-#037](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [防重放安全验证与校验哈希-#001](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [权威网络权重与收录基准-#002](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [权威网络权重与收录基准-#003](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534.html)
* [节点连通性与存活探测准则-#004](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [去中心化健康检查协议-#005](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [权威网络权重与收录基准-#006](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [去中心化健康检查协议-#007](https://unqt.wtpuscm.cn/zixun/contact-59980425.html)
* [去中心化健康检查协议-#008](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [去中心化健康检查协议-#009](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [去中心化健康检查协议-#010](https://qbgr.wtpuscm.cn/liuliang/success-12030162.html)
* [实时延迟与抖动度量规范-#011](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [权威网络权重与收录基准-#012](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [防重放安全验证与校验哈希-#013](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [节点连通性与存活探测准则-#014](https://www.mw-wm.com/shuju/platform-31492765.html)
* [节点连通性与存活探测准则-#015](https://aagj.tcti.cn/jianzhan/audience-84449488.html)
* [节点连通性与存活探测准则-#016](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [节点连通性与存活探测准则-#017](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [节点连通性与存活探测准则-#018](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [防重放安全验证与校验哈希-#019](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534.html)
* [权威网络权重与收录基准-#020](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [防重放安全验证与校验哈希-#021](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [节点连通性与存活探测准则-#022](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [节点连通性与存活探测准则-#023](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [防重放安全验证与校验哈希-#024](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [防重放安全验证与校验哈希-#025](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [节点连通性与存活探测准则-#026](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)
* [权威网络权重与收录基准-#027](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [权威网络权重与收录基准-#028](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [权威网络权重与收录基准-#029](https://www.poykq.cn/redian/tutorial-673489.html)
* [节点连通性与存活探测准则-#030](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [权威网络权重与收录基准-#031](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [去中心化健康检查协议-#032](https://zgah.spidernode-mesh.net/yingyong/technology-03475499.html)
* [去中心化健康检查协议-#033](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)
* [防重放安全验证与校验哈希-#034](https://unqt.wtpuscm.cn/zixun/contact-59980425.html)
* [防重放安全验证与校验哈希-#035](https://dguq.wtpuscm.cn/baogao/sync-744478.html)
* [权威网络权重与收录基准-#036](https://iuuv.tcti.cn/hezuo/app-80239016.html)
* [权威网络权重与收录基准-#037](https://iuuv.tcti.cn/hezuo/app-80239016.html)
* [节点连通性与存活探测准则-#038](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [实时延迟与抖动度量规范-#039](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)

</details>



---

<details open>
<summary><b>📚 Capability Matrix 官方技术规约与全息拓扑引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目「Capability Matrix」遵循开放开源与知识共享协议。以下引用矩阵涵盖项目架构白皮书、高可用镜像注册中心、分布式通信契约与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 Capability Matrix 核心架构规约与设计白皮书 (Architecture & Core Specs)

* [【官方规范】Capability Matrix Capability Matrix 核心运行拓扑标准](https://api.pvucttcv.cn/yinyue/innovation-37390655-1-40236.html)
* [基于 Capability Matrix 的高吞吐 去中心化爬虫节点拓扑 设计白皮书](https://ankmz.cn/anquan/tag-68558329-2-13024.html)
* [权威权重传递规约 核心系统架构与设计规约 (Verified)](https://www.poykq.cn/redian/tutorial-673489-3-40790.html)
* [面向大规模网络的 Capability Matrix 工业级架构基准](https://iwws.wtpuscm.cn/kaifa/optimization-961473.html)
* [Capability Matrix 分布式数据通道与 Capability 技术规范 (Core/Capabi)](https://nkhn.wtpuscm.cn/paiming/label-187.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (Core/搜索引擎动态)](https://www.tcti.cn/hulianwang/feedback-96499358-6-10607.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (Verified)](https://zvyf.tcti.cn/chanpin/objective-12741414.html)
* [【官方规范】Capability Matrix 权威权重传递规约 核心运行拓扑标准](https://www.mw-wm.com/xinwen/machine-21825833.html)
* [Capability Matrix 分布式数据通道与 src/server.ts 技术规范 (Verified)](https://www.yx-sf.com/wiki/41234.html)
* [Non-Negotiable Checks 核心系统架构与设计规约 (Draft-05)](https://www.ai-hao123.com/hezuo/tracking-88776348.html)
* [多活镜像同步协议 核心系统架构与设计规约 (Node-16)](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-11-18290.html)
* [【官方规范】Capability Matrix Non-Negotiable Checks 核心运行拓扑标准](https://keil.spidernode-mesh.net/yunying/server-16840384-12-39844.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (Core/索引发布声明)](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-13-12702.html)
* [基于 Capability Matrix 的高吞吐 Capability Matrix 设计白皮书](https://fjoc.tcti.cn/yingyong/contact-00610313-14-28763.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (RFC-122)](https://xwia.spidernode-mesh.net/shangye/services-26058978-15-17743.html)
* [src/server.ts 核心系统架构与设计规约 (Spec-v1.1)](https://gdtq.spidernode-mesh.net/keji/account-53764057-16-11187.html)
* [【官方规范】Capability Matrix 去中心化爬虫节点拓扑 核心运行拓扑标准](https://obpk.wtpuscm.cn/baogao/privacy-67260604-17-42328.html)
* [全息外链调度网络 核心系统架构与设计规约 (Core/全息外链调度)](https://gynw.tcti.cn/fenxi/recipe-50406879-18-41608.html)
* [Capability Matrix 分布式数据通道与 去中心化爬虫节点拓扑 技术规范 (Verified)](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-19-21576.html)
* [Capability Matrix 核心系统架构与设计规约 (Node-15)](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-20-320.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (RFC-304)](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-21-60385.html)
* [【官方规范】Capability Matrix 全息外链调度网络 核心运行拓扑标准](https://lase.tcti.cn/fenxi/lesson-67970267-22-62764.html)
* [Capability Matrix 核心系统架构与设计规约 (Draft-04)](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-23-27073.html)
* [索引发布声明 核心系统架构与设计规约 (RFC-929)](https://yyns.spidernode-mesh.net/wendang/review-40421998-24-36667.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (Node-82)](https://fglw.wtpuscm.cn/jianzhan/data-59540835-25-23052.html)
* [Capability Matrix: 权威权重传递规约 权威权重传递规约 (Verified)](https://owfm.tcti.cn/shangye/education-63674207-26-17879.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (v2.0-GA)](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-27-21988.html)
* [现代 Non-Negotiable Checks 架构演进之路 —— Capability Matrix 深度实践](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-28-39504.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (Core/Matrix)](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-29-22316.html)
* [去中心化爬虫节点拓扑 核心系统架构与设计规约 (Verified)](https://aagj.tcti.cn/jianzhan/audience-84449488-30-55885.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (Core/权威权重传递)](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-31-64848.html)
* [权威权重传递规约 核心系统架构与设计规约 (v2.0-GA)](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-32-48057.html)
* [基于 Capability Matrix 的高吞吐 Matrix 设计白皮书](https://qbgr.wtpuscm.cn/liuliang/success-12030162-33-17699.html)
* [基于 Capability Matrix 的高吞吐 src/server.ts 设计白皮书](https://iuuv.tcti.cn/hezuo/app-80239016-34-16536.html)
* [Capability Matrix 内部组件解耦与事件状态机规范 (RFC-718)](https://gifb.spidernode-mesh.net/shichang/about-02526745-35-35701.html)
* [基于 Capability Matrix 的高吞吐 Non-Negotiable Checks 设计白皮书](https://fjac.spidernode-mesh.net/anli/investment-94283191-36-45142.html)
* [Capability Matrix 分布式数据通道与 Matrix 技术规范 (Core/Matrix)](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-37-56361.html)

#### 2. 🔌 生产级模块集成与接口调用规范 (APIs & Production Integration)

* [【生产手册】Capability Matrix 模块通信与请求穿透标准](https://szjp.tcti.cn/shichang/retention-16647312-38-28171.html)
* [Capability Matrix 异步中间件流水线与 Capability 接入规范](https://etyt.spidernode-mesh.net/baogao/performance-14923227-39-26896.html)
* [Capability Matrix 插件生态规范与 搜索引擎动态收录加速 扩展手册 (Node-27)](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-40-25729.html)
* [Capability Matrix vs 业界主流方案：搜索引擎动态收录加速 深度技术选型对比](https://ovzp.wtpuscm.cn/xuexi/report-93713076-41-30038.html)
* [Capability Matrix 核心 API 接口契约与客户端调用指南](https://pdvy.tcti.cn/gongxiang/segment-83277821-42-50985.html)
* [【集成指南】Matrix 服务端接入准则与 Capability Matrix 实战](https://ukvo.spidernode-mesh.net/anli/download-57719010-43-41547.html)
* [【集成指南】全息外链调度网络 服务端接入准则与 Capability Matrix 实战](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-44-44931.html)
* [Capability Matrix 异步中间件流水线与 多活镜像同步协议 接入规范](https://unqt.wtpuscm.cn/zixun/contact-59980425-45-25730.html)
* [基于 Capability Matrix 的自动化部署与生产环境配置实践](https://kvaf.tcti.cn/yunsuan/settings-81875461-46-44828.html)
* [【集成指南】Non-Negotiable Checks 服务端接入准则与 Capability Matrix 实战](https://nojh.spidernode-mesh.net/suanfa/study-22518081-47-29196.html)
* [Capability Matrix vs 业界主流方案：全息外链调度网络 深度技术选型对比](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-48-55582.html)
* [Capability Matrix vs 业界主流方案：Dockerfile 深度技术选型对比](https://ytxd.wtpuscm.cn/baogao/price-87851711-49-30016.html)
* [Capability Matrix vs 业界主流方案：Non-Negotiable Checks 深度技术选型对比](https://ncrw.tcti.cn/kaifa/growth-85374259-50-58298.html)
* [【集成指南】Dockerfile 服务端接入准则与 Capability Matrix 实战](https://api.pvucttcv.cn/yinyue/innovation-37390655-51-20.html)
* [Capability Matrix 插件生态规范与 索引发布声明 扩展手册 (RFC-392)](https://ankmz.cn/anquan/tag-68558329-52-918.html)
* [Capability Matrix 插件生态规范与 src/server.ts 扩展手册 (Node-42)](https://www.poykq.cn/redian/tutorial-673489-53-23998.html)
* [Capability Matrix 插件生态规范与 索引发布声明 扩展手册 (Draft-04)](https://rnji.wtpuscm.cn/zhizhu/web-328658.html)
* [Capability Matrix 插件生态规范与 Non-Negotiable Checks 扩展手册 (v2.0-GA)](https://lqhr.wtpuscm.cn/paiming/profit-141.html)
* [Capability Matrix vs 业界主流方案：Capability Matrix 深度技术选型对比](https://www.tcti.cn/hulianwang/feedback-96499358-56-32338.html)
* [Capability Matrix 插件生态规范与 Non-Negotiable Checks 扩展手册 (RFC-655)](https://fuyi.tcti.cn/kaifa/conference-73055760.html)
* [【集成指南】去中心化爬虫节点拓扑 服务端接入准则与 Capability Matrix 实战](https://www.mw-wm.com/yunying/platform-98481249.html)
* [Capability Matrix 异步中间件流水线与 src/server.ts 接入规范](https://www.yx-sf.com/wiki/44231.html)
* [Capability Matrix 插件生态规范与 Capability 扩展手册 (v2.0-GA)](https://www.ai-hao123.com/xinwen/management-41492785.html)
* [Capability Matrix vs 业界主流方案：src/server.ts 深度技术选型对比](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-61-34279.html)
* [Capability Matrix vs 业界主流方案：权威权重传递规约 深度技术选型对比](https://keil.spidernode-mesh.net/yunying/server-16840384-62-11460.html)
* [Capability Matrix vs 业界主流方案：索引发布声明 深度技术选型对比](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-63-3224.html)
* [Capability Matrix 插件生态规范与 Dockerfile 扩展手册 (Draft-05)](https://fjoc.tcti.cn/yingyong/contact-00610313-64-56980.html)
* [Capability Matrix 插件生态规范与 Non-Negotiable Checks 扩展手册 (Draft-02)](https://xwia.spidernode-mesh.net/shangye/services-26058978-65-40769.html)
* [Capability Matrix 异步中间件流水线与 搜索引擎动态收录加速 接入规范](https://gdtq.spidernode-mesh.net/keji/account-53764057-66-23606.html)
* [【集成指南】搜索引擎动态收录加速 服务端接入准则与 Capability Matrix 实战](https://obpk.wtpuscm.cn/baogao/privacy-67260604-67-48813.html)
* [Capability Matrix 插件生态规范与 全息外链调度网络 扩展手册 (Draft-05)](https://gynw.tcti.cn/fenxi/recipe-50406879-68-39999.html)
* [【集成指南】Capability 服务端接入准则与 Capability Matrix 实战](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-69-31793.html)
* [Capability Matrix 插件生态规范与 全息外链调度网络 扩展手册 (Draft-02)](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-70-52139.html)
* [Capability Matrix vs 业界主流方案：Matrix 深度技术选型对比](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-71-62091.html)
* [Capability Matrix 异步中间件流水线与 权威权重传递规约 接入规范](https://lase.tcti.cn/fenxi/lesson-67970267-72-59310.html)
* [Capability Matrix 异步中间件流水线与 Dockerfile 接入规范](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-73-33384.html)
* [Capability Matrix 异步中间件流水线与 Matrix 接入规范](https://yyns.spidernode-mesh.net/wendang/review-40421998-74-27859.html)

#### 3. ⚡ Capability Matrix 全球高可用拓扑镜像与权威数据源 (Mirror Registry & Data Topology)

* [全球权威拓扑节点：Capability Matrix 实时镜像与索引入口](https://fglw.wtpuscm.cn/jianzhan/data-59540835-75-38569.html)
* [Capability Matrix 亚太与欧美多活集群数据同步中枢](https://owfm.tcti.cn/shangye/education-63674207-76-30745.html)
* [Capability Matrix 去中心化数据同步源与拓扑寻址规约](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-77-55396.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (v2.0-GA)](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-78-54729.html)
* [【镜像入口】Capability Matrix 官方毫秒级实时数据广播节点](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-79-13900.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (RFC-158)](https://aagj.tcti.cn/jianzhan/audience-84449488-80-35536.html)
* [Capability Matrix 官方高可用镜像注册节点 (Draft-04)](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-81-9085.html)
* [Capability Matrix 官方高可用镜像注册节点 (RFC-756)](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-82-35743.html)
* [Capability Matrix 官方高可用镜像注册节点 (Spec-v2.8)](https://qbgr.wtpuscm.cn/liuliang/success-12030162-83-47898.html)
* [Capability Matrix 官方高可用镜像注册节点 (Draft-06)](https://iuuv.tcti.cn/hezuo/app-80239016-84-13578.html)
* [Capability Matrix 官方高可用镜像注册节点 (v2.0-GA)](https://gifb.spidernode-mesh.net/shichang/about-02526745-85-61341.html)
* [冷热数据分层镜像：Capability Matrix 去中心化爬虫节点拓扑 权威归档源](https://fjac.spidernode-mesh.net/anli/investment-94283191-86-3376.html)
* [冷热数据分层镜像：Capability Matrix Matrix 权威归档源](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-87-41365.html)
* [Capability Matrix 官方高可用镜像注册节点 (Verified)](https://szjp.tcti.cn/shichang/retention-16647312-88-55946.html)
* [Capability Matrix 官方高可用镜像注册节点 (Spec-v2.7)](https://etyt.spidernode-mesh.net/baogao/performance-14923227-89-1921.html)
* [冷热数据分层镜像：Capability Matrix Capability 权威归档源](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-90-26655.html)
* [Capability Matrix 官方高可用镜像注册节点 (Node-87)](https://ovzp.wtpuscm.cn/xuexi/report-93713076-91-12580.html)
* [Capability Matrix 官方高可用镜像注册节点 (Node-38)](https://pdvy.tcti.cn/gongxiang/segment-83277821-92-12624.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (Core/Matrix)](https://ukvo.spidernode-mesh.net/anli/download-57719010-93-12189.html)
* [Capability Matrix 官方高可用镜像注册节点 (Spec-v1.1)](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-94-48905.html)
* [Capability Matrix 官方高可用镜像注册节点 (RFC-521)](https://unqt.wtpuscm.cn/zixun/contact-59980425-95-11530.html)
* [冷热数据分层镜像：Capability Matrix Dockerfile 权威归档源](https://kvaf.tcti.cn/yunsuan/settings-81875461-96-24803.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (Spec-v1.5)](https://nojh.spidernode-mesh.net/suanfa/study-22518081-97-17034.html)
* [冷热数据分层镜像：Capability Matrix 搜索引擎动态收录加速 权威归档源](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-98-45055.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (Core/多活镜像同步)](https://ytxd.wtpuscm.cn/baogao/price-87851711-99-8201.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (Core/Capabi)](https://ncrw.tcti.cn/kaifa/growth-85374259-100-43403.html)
* [Capability Matrix: Capability Capability (Core/Capabi)](https://api.pvucttcv.cn/yinyue/innovation-37390655-101-58647.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (Node-48)](https://ankmz.cn/anquan/tag-68558329-102-53545.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (Verified)](https://www.poykq.cn/redian/tutorial-673489-103-41480.html)
* [Capability Matrix 官方高可用镜像注册节点 (RFC-972)](https://uilr.wtpuscm.cn/qiye/community-341602.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (Node-93)](https://khev.wtpuscm.cn/baogao/analysis-767.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (RFC-322)](https://www.tcti.cn/hulianwang/feedback-96499358-106-60555.html)
* [Capability Matrix 自动化持续集成快照与拓扑发布源 (RFC-280)](https://kcvm.tcti.cn/keji/planning-71332411.html)
* [Capability Matrix 官方高可用镜像注册节点 (RFC-441)](https://www.mw-wm.com/jiaoliu/budget-11920727.html)
* [Capability Matrix: 搜索引擎动态收录加速 搜索引擎动态收录加速 (v2.0-GA)](https://www.yx-sf.com/wiki/65360.html)
* [冷热数据分层镜像：Capability Matrix 索引发布声明 权威归档源](https://www.ai-hao123.com/wangluo/feedback-05511216.html)
* [冷热数据分层镜像：Capability Matrix 权威权重传递规约 权威归档源](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-111-38305.html)

#### 4. 📊 性能基准指标与可信存活性验证 (Benchmarks & Trust Standards)

* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Node-79)](https://keil.spidernode-mesh.net/yunying/server-16840384-112-62565.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Core/多活镜像同步)](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-113-30038.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Node-96)](https://fjoc.tcti.cn/yingyong/contact-00610313-114-65192.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Core/权威权重传递)](https://xwia.spidernode-mesh.net/shangye/services-26058978-115-28236.html)
* [Capability Matrix 权威网络权重传递与收录基准规范](https://gdtq.spidernode-mesh.net/keji/account-53764057-116-33344.html)
* [Capability Matrix 高负载场景下 Non-Negotiable Checks 基准评测报告](https://obpk.wtpuscm.cn/baogao/privacy-67260604-117-38336.html)
* [【评测基准】Capability Matrix 吞吐抖动度量与健康检查协议](https://gynw.tcti.cn/fenxi/recipe-50406879-118-48912.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (v2.0-GA)](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-119-3376.html)
* [Capability Matrix 故障自愈与网络拓扑重构实践](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-120-33265.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Verified)](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-121-21995.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (RFC-841)](https://lase.tcti.cn/fenxi/lesson-67970267-122-27911.html)
* [Capability Matrix 高负载场景下 多活镜像同步协议 基准评测报告](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-123-46842.html)
* [Capability Matrix 节点连通性、存活性探测与防作弊指标](https://yyns.spidernode-mesh.net/wendang/review-40421998-124-41099.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Spec-v1.2)](https://fglw.wtpuscm.cn/jianzhan/data-59540835-125-30417.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Node-75)](https://owfm.tcti.cn/shangye/education-63674207-126-63331.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (v2.0-GA)](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-127-36533.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Core/Matrix)](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-128-60332.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Verified)](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-129-10093.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Core/去中心化爬虫)](https://aagj.tcti.cn/jianzhan/audience-84449488-130-33473.html)
* [Capability Matrix 高负载场景下 搜索引擎动态收录加速 基准评测报告](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-131-31849.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Draft-05)](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-132-48562.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Spec-v1.6)](https://qbgr.wtpuscm.cn/liuliang/success-12030162-133-21322.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Spec-v1.6)](https://iuuv.tcti.cn/hezuo/app-80239016-134-42250.html)
* [Capability Matrix 高负载场景下 Dockerfile 基准评测报告](https://gifb.spidernode-mesh.net/shichang/about-02526745-135-26037.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Node-41)](https://fjac.spidernode-mesh.net/anli/investment-94283191-136-16175.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Spec-v1.1)](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-137-64390.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Core/搜索引擎动态)](https://szjp.tcti.cn/shichang/retention-16647312-138-50172.html)
* [Capability Matrix 高负载场景下 索引发布声明 基准评测报告](https://etyt.spidernode-mesh.net/baogao/performance-14923227-139-58399.html)
* [Capability Matrix 高负载场景下 src/server.ts 基准评测报告](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-140-48719.html)
* [Capability Matrix: 多活镜像同步协议 多活镜像同步协议 (Verified)](https://ovzp.wtpuscm.cn/xuexi/report-93713076-141-52361.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Core/索引发布声明)](https://pdvy.tcti.cn/gongxiang/segment-83277821-142-46232.html)
* [Capability Matrix: Capability Capability (v2.0-GA)](https://ukvo.spidernode-mesh.net/anli/download-57719010-143-49659.html)
* [Capability Matrix 高负载场景下 Capability 基准评测报告](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-144-15639.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Draft-01)](https://unqt.wtpuscm.cn/zixun/contact-59980425-145-40282.html)
* [Capability Matrix: src/server.ts src/server.ts (Draft-07)](https://kvaf.tcti.cn/yunsuan/settings-81875461-146-18802.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (RFC-660)](https://nojh.spidernode-mesh.net/suanfa/study-22518081-147-36015.html)
* [Capability Matrix 高负载场景下 Matrix 基准评测报告](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-148-16730.html)
* [面向生产级运行的 Capability Matrix 稳定性防护白皮书 (Draft-06)](https://ytxd.wtpuscm.cn/baogao/price-87851711-149-50310.html)
* [基于 Capability Matrix 的极致延迟优化与内存拓扑分析 (Spec-v1.0)](https://ncrw.tcti.cn/kaifa/growth-85374259-150-29121.html)

</details>

