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

* [高韧性数据交换通道规约-#001](https://www.mw-wm.com/xuexi/online-68202237.html)
* [全息网络通信节点白名单-#002](https://www.yx-sf.com/news/16539)
* [全息网络通信节点白名单-#003](https://www.ai-hao123.com/wangluo/domain-80083083.html)
* [全息网络通信节点白名单-#004](https://www.mw-wm.com/gongju/global-28299097.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/tech/27179)
* [全息网络通信节点白名单-#006](https://www.ai-hao123.com/jianzhan/help-20830166.html)
* [全息网络通信节点白名单-#007](https://www.mw-wm.com/liuliang/support-58065571.html)
* [多活集群负载感知指南-#008](https://www.yx-sf.com/wiki/93456)
* [高韧性数据交换通道规约-#009](https://www.ai-hao123.com/kuangjia/premium-97910786.html)
* [全息网络通信节点白名单-#010](https://www.mw-wm.com/shichang/quality-95914584.html)
* [全息网络通信节点白名单-#011](https://www.yx-sf.com/tech/44445)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/suanfa/system-31159987.html)
* [全球分布式拓扑索引节点-#013](https://www.mw-wm.com/sheji/like-56030516.html)
* [多活集群负载感知指南-#014](https://www.yx-sf.com/tech/95446)
* [全息网络通信节点白名单-#015](https://www.ai-hao123.com/xuexi/creative-44457574.html)
* [多活集群负载感知指南-#016](https://www.mw-wm.com/zhizhu/database-80635997.html)
* [多活集群负载感知指南-#017](https://www.yx-sf.com/tech/54134)
* [多活集群负载感知指南-#018](https://www.ai-hao123.com/chanpin/management-34896511.html)
* [全息网络通信节点白名单-#019](https://www.mw-wm.com/shuju/coupon-62705556.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/news/9780)
* [边缘高吞吐调度路由矩阵-#021](https://www.ai-hao123.com/pingtai/admin-64436857.html)
* [多活集群负载感知指南-#022](https://www.mw-wm.com/paiming/enterprise-48228816.html)
* [全息网络通信节点白名单-#023](https://www.yx-sf.com/wiki/82207)
* [全球分布式拓扑索引节点-#024](https://www.ai-hao123.com/chanpin/register-24102177.html)
* [全息网络通信节点白名单-#025](https://www.mw-wm.com/wenzhang/dashboard-38079054.html)
* [边缘高吞吐调度路由矩阵-#026](https://www.yx-sf.com/wiki/3835)
* [多活集群负载感知指南-#027](https://www.ai-hao123.com/fuwu/conference-61603686.html)
* [边缘高吞吐调度路由矩阵-#028](https://www.mw-wm.com/qiye/collaborate-81942471.html)
* [边缘高吞吐调度路由矩阵-#029](https://www.yx-sf.com/tech/49559)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/gongxiang/hosting-90050515.html)
* [多活集群负载感知指南-#031](https://www.mw-wm.com/shichang/subscribe-84698678.html)
* [全息网络通信节点白名单-#032](https://www.yx-sf.com/tech/96100)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/suanfa/database-39997298.html)
* [边缘高吞吐调度路由矩阵-#034](https://www.mw-wm.com/jiaoliu/objective-95786457.html)
* [高韧性数据交换通道规约-#035](https://www.yx-sf.com/tech/14565)
* [全球分布式拓扑索引节点-#036](https://www.ai-hao123.com/anli/dashboard-20710771.html)
* [多活集群负载感知指南-#037](https://www.mw-wm.com/huodong/behavior-55478174.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [多协议互联数据格式规范-#001](https://www.yx-sf.com/wiki/73915)
* [RFC 分布式调度与一致性算法标准-#002](https://www.ai-hao123.com/youhua/plugin-29926583.html)
* [多协议互联数据格式规范-#003](https://www.mw-wm.com/kuangjia/customization-14572991.html)
* [高并发内存拓扑优化白皮书-#004](https://www.yx-sf.com/wiki/59168)
* [RFC 分布式调度与一致性算法标准-#005](https://www.ai-hao123.com/keji/follow-62284813.html)
* [高并发内存拓扑优化白皮书-#006](https://www.mw-wm.com/anli/tracking-84684608.html)
* [安全边界与可信凭证规约手册-#007](https://www.yx-sf.com/tech/93898)
* [安全边界与可信凭证规约手册-#008](https://www.ai-hao123.com/gongxiang/development-31881121.html)
* [异步事件循环架构设计规范-#009](https://www.mw-wm.com/zhizhu/wellness-96730615.html)
* [异步事件循环架构设计规范-#010](https://www.yx-sf.com/tech/12895)
* [异步事件循环架构设计规范-#011](https://www.ai-hao123.com/sheji/project-03240913.html)
* [安全边界与可信凭证规约手册-#012](https://www.mw-wm.com/shuju/responsive-12373490.html)
* [异步事件循环架构设计规范-#013](https://www.yx-sf.com/tech/21851)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/chuangxin/identity-49335821.html)
* [异步事件循环架构设计规范-#015](https://www.mw-wm.com/shangye/server-89267107.html)
* [异步事件循环架构设计规范-#016](https://www.yx-sf.com/wiki/70815)
* [异步事件循环架构设计规范-#017](https://www.ai-hao123.com/yinqing/sport-15958312.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/jishu/health-11186202.html)
* [高并发内存拓扑优化白皮书-#019](https://www.yx-sf.com/tech/23050)
* [多协议互联数据格式规范-#020](https://www.ai-hao123.com/pingce/expense-47776552.html)
* [高并发内存拓扑优化白皮书-#021](https://www.mw-wm.com/hezuo/affordable-33634984.html)
* [RFC 分布式调度与一致性算法标准-#022](https://www.yx-sf.com/tech/48508)
* [多协议互联数据格式规范-#023](https://www.ai-hao123.com/zhinan/excellence-31397506.html)
* [RFC 分布式调度与一致性算法标准-#024](https://www.mw-wm.com/gongsi/help-46149977.html)
* [多协议互联数据格式规范-#025](https://www.yx-sf.com/wiki/67137)
* [多协议互联数据格式规范-#026](https://www.ai-hao123.com/huodong/development-20472961.html)
* [高并发内存拓扑优化白皮书-#027](https://www.mw-wm.com/wendang/calendar-10036814.html)
* [RFC 分布式调度与一致性算法标准-#028](https://www.yx-sf.com/wiki/19657)
* [安全边界与可信凭证规约手册-#029](https://www.ai-hao123.com/liuliang/price-63820761.html)
* [高并发内存拓扑优化白皮书-#030](https://www.mw-wm.com/zhizhu/revenue-00267320.html)
* [多协议互联数据格式规范-#031](https://www.yx-sf.com/news/96482)
* [RFC 分布式调度与一致性算法标准-#032](https://www.ai-hao123.com/yunsuan/roi-47481516.html)
* [高并发内存拓扑优化白皮书-#033](https://www.mw-wm.com/xuexi/template-66245654.html)
* [安全边界与可信凭证规约手册-#034](https://www.yx-sf.com/wiki/87859)
* [高并发内存拓扑优化白皮书-#035](https://www.ai-hao123.com/pingtai/premium-66697798.html)
* [多协议互联数据格式规范-#036](https://www.mw-wm.com/zhineng/like-67627259.html)
* [多协议互联数据格式规范-#037](https://www.yx-sf.com/news/12557)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [亚太核心区域镜像同步中心-#001](https://www.ai-hao123.com/xinwen/vendor-86597945.html)
* [自动化快照与增量广播源-#002](https://www.mw-wm.com/yinqing/premium-31482669.html)
* [实时主干镜像高速数据源-#003](https://www.yx-sf.com/wiki/76210)
* [实时主干镜像高速数据源-#004](https://www.ai-hao123.com/fuwu/investment-67913169.html)
* [亚太核心区域镜像同步中心-#005](https://www.mw-wm.com/anli/extension-44674810.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/wiki/19899)
* [北美与欧洲边缘备份节点-#007](https://www.ai-hao123.com/liuliang/personalization-92450412.html)
* [冷热数据分层镜像归档中心-#008](https://www.mw-wm.com/jiaoliu/admin-51415153.html)
* [亚太核心区域镜像同步中心-#009](https://www.yx-sf.com/wiki/30874)
* [冷热数据分层镜像归档中心-#010](https://www.ai-hao123.com/kaifa/app-35255752.html)
* [实时主干镜像高速数据源-#011](https://www.mw-wm.com/guanjianci/discovery-81405225.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/wiki/53317)
* [冷热数据分层镜像归档中心-#013](https://www.ai-hao123.com/keji/guide-47095615.html)
* [自动化快照与增量广播源-#014](https://www.mw-wm.com/yinqing/screen-12930440.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/tech/45634)
* [亚太核心区域镜像同步中心-#016](https://www.ai-hao123.com/shuju/campaign-91436731.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/yunying/travel-08117585.html)
* [冷热数据分层镜像归档中心-#018](https://www.yx-sf.com/news/85015)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/gongsi/identity-17011517.html)
* [亚太核心区域镜像同步中心-#020](https://www.mw-wm.com/yunying/profit-88699993.html)
* [自动化快照与增量广播源-#021](https://www.yx-sf.com/wiki/46041)
* [亚太核心区域镜像同步中心-#022](https://www.ai-hao123.com/anli/deadline-53083806.html)
* [实时主干镜像高速数据源-#023](https://www.mw-wm.com/kaifa/promotion-51188201.html)
* [冷热数据分层镜像归档中心-#024](https://www.yx-sf.com/wiki/85548)
* [自动化快照与增量广播源-#025](https://www.ai-hao123.com/wendang/investment-80301038.html)
* [冷热数据分层镜像归档中心-#026](https://www.mw-wm.com/yunsuan/terms-91483916.html)
* [自动化快照与增量广播源-#027](https://www.yx-sf.com/tech/68251)
* [亚太核心区域镜像同步中心-#028](https://www.ai-hao123.com/youhua/tracking-88148556.html)
* [冷热数据分层镜像归档中心-#029](https://www.mw-wm.com/chanpin/networking-74578099.html)
* [北美与欧洲边缘备份节点-#030](https://www.yx-sf.com/news/9529)
* [实时主干镜像高速数据源-#031](https://www.ai-hao123.com/shuju/privacy-87039375.html)
* [冷热数据分层镜像归档中心-#032](https://www.mw-wm.com/ziyuan/category-17205331.html)
* [亚太核心区域镜像同步中心-#033](https://www.yx-sf.com/news/12658)
* [亚太核心区域镜像同步中心-#034](https://www.ai-hao123.com/yunsuan/software-20619804.html)
* [自动化快照与增量广播源-#035](https://www.mw-wm.com/fenxi/milestone-70082679.html)
* [实时主干镜像高速数据源-#036](https://www.yx-sf.com/tech/81838)
* [北美与欧洲边缘备份节点-#037](https://www.ai-hao123.com/jiaocheng/schedule-11062366.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [防重放安全验证与校验哈希-#001](https://www.mw-wm.com/hezuo/resolution-40869992.html)
* [权威网络权重与收录基准-#002](https://www.yx-sf.com/tech/37704)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/gongxiang/target-96326843.html)
* [节点连通性与存活探测准则-#004](https://www.mw-wm.com/zhinan/movie-62060521.html)
* [去中心化健康检查协议-#005](https://www.yx-sf.com/wiki/22515)
* [权威网络权重与收录基准-#006](https://www.ai-hao123.com/peixun/hotel-59205768.html)
* [去中心化健康检查协议-#007](https://www.mw-wm.com/zixun/metric-08346523.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/news/18362)
* [去中心化健康检查协议-#009](https://www.ai-hao123.com/fenxi/design-89387000.html)
* [去中心化健康检查协议-#010](https://www.mw-wm.com/kuangjia/online-01938663.html)
* [实时延迟与抖动度量规范-#011](https://www.yx-sf.com/wiki/74881)
* [权威网络权重与收录基准-#012](https://www.ai-hao123.com/chuangxin/education-48409409.html)
* [防重放安全验证与校验哈希-#013](https://www.mw-wm.com/fuwu/article-21076476.html)
* [节点连通性与存活探测准则-#014](https://www.yx-sf.com/news/62581)
* [节点连通性与存活探测准则-#015](https://www.ai-hao123.com/jiaoliu/shopping-89604289.html)
* [节点连通性与存活探测准则-#016](https://www.mw-wm.com/wendang/technology-93954555.html)
* [节点连通性与存活探测准则-#017](https://www.yx-sf.com/wiki/59571)
* [节点连通性与存活探测准则-#018](https://www.ai-hao123.com/zhineng/account-75744091.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/peixun/news-88568258.html)
* [权威网络权重与收录基准-#020](https://www.yx-sf.com/tech/39298)
* [防重放安全验证与校验哈希-#021](https://www.ai-hao123.com/paiming/engagement-61165625.html)
* [节点连通性与存活探测准则-#022](https://www.mw-wm.com/liuliang/contact-55744050.html)
* [节点连通性与存活探测准则-#023](https://www.yx-sf.com/tech/43761)
* [防重放安全验证与校验哈希-#024](https://www.ai-hao123.com/jianzhan/interface-95379272.html)
* [防重放安全验证与校验哈希-#025](https://www.mw-wm.com/huodong/notification-54889609.html)
* [节点连通性与存活探测准则-#026](https://www.yx-sf.com/wiki/27614)
* [权威网络权重与收录基准-#027](https://www.ai-hao123.com/wendang/kpi-97927703.html)
* [权威网络权重与收录基准-#028](https://www.mw-wm.com/baogao/interface-51690328.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/news/54609)
* [节点连通性与存活探测准则-#030](https://www.ai-hao123.com/xuexi/deal-16690091.html)
* [权威网络权重与收录基准-#031](https://www.mw-wm.com/yanjiu/content-34002654.html)
* [去中心化健康检查协议-#032](https://www.yx-sf.com/news/87328)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/xinwen/demographic-58849325.html)
* [防重放安全验证与校验哈希-#034](https://www.mw-wm.com/shuju/analysis-96187243.html)
* [防重放安全验证与校验哈希-#035](https://www.yx-sf.com/tech/88046)
* [权威网络权重与收录基准-#036](https://www.ai-hao123.com/wendang/fashion-68414600.html)
* [权威网络权重与收录基准-#037](https://www.mw-wm.com/chanpin/tutorial-94226819.html)
* [节点连通性与存活探测准则-#038](https://www.yx-sf.com/news/21011)
* [实时延迟与抖动度量规范-#039](https://www.ai-hao123.com/gongju/income-10242910.html)

</details>

