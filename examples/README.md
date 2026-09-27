# Inspect the cases

[简体中文](./README.zh-CN.md)

These are twenty deliberately selected software-product domains, not a random market sample or a brand ranking. Each folder under `cases/` contains the frozen input, a bilingual observation page, a machine-readable summary and an evidence index. Read the state on the case page: a documented case is not necessarily an executed or successful test.

## Read without paying for inference

```bash
npm ci
npm run examples:validate
npm run examples:plan -- --case R02
npm run examples:replay -- --case R02 --evidence examples/cases/R02/public-evidence.json
```

Planning, replay, export and Markdown rendering never ask a model for a new answer. Replay retains the original run dates and is labelled as archived evidence.

## Remeasurement incurs charges

The checked-in study plan records this release's conditions and budget; it is not continuing authorization to spend someone else's key. A new study requires an explicitly authorized budget, new isolated output directory, frozen inputs and a successful preflight. The commands below are for an operator who has supplied their own key and approved USD 2 for that new study.

```bash
# Uses the existing product HTTP API in a separate, local product service.
npm run examples:preflight -- --execution live --budget-usd 2
npm run examples:run -- --case R02 --execution live --budget-usd 2
# Omit --case to execute every still-unrun case in the frozen study.
```

The live runner requires `validation/release-v0.2.0-rc.1/study-plan.json` and its initialized cumulative ledger. It refuses an unfrozen study, duplicate completed cases, unpriced models and a failed preflight. This release's private validation directory is intentionally not in Git. See [the study plan](./study-plan.json) and [measurement method](../docs/measurement-methodology.md) before creating a new study with `npm run examples:init -- --budget-usd 2`. Initialization does not overwrite an existing plan; archive a completed study and give the new study a separate `--root` directory.

## Cases

The current observations and source links are in each case's README. Markdown is the reading interface; no case service is needed.

<!-- CASE_INDEX -->

All 20 domains have analyzable D answers; 11 cases actually ran K, 10 cases are partial, and 18 answers failed analysis. 7 first-place fields across 5 cases conflict and are excluded from rankings. These are different scopes, not an overall success rate.

[Conflict and failure index](../docs/known-issues.md)

| ID | Domain | Actual scope | Observation or limitation | Details |
|---|---|---|---|---|
| R01 | niubistar.com | Domain only; keyword tests not run | One model described gaming, another GitHub growth, and a third did not recognize the domain. | [Read](cases/R01/README.md) |
| R02 | vercel.com | D + K (6/9 K answers analyzable) | All described frontend deployment; three keyword answers failed analysis across three repeats. | [Read](cases/R02/README.md) |
| R03 | supabase.com | Domain only; keyword tests not run | Models described a Firebase alternative; no eligible neutral keyword test was established. | [Read](cases/R03/README.md) |
| R04 | posthog.com | D + K (15/18 K answers analyzable) | Feature Flags answers returned actual citations; all three repeats remain partial. | [Read](cases/R04/README.md) |
| R05 | sentry.io | Domain only; keyword tests not run | Models emphasized error tracking, naming different lists including Datadog and New Relic. | [Read](cases/R05/README.md) |
| R06 | linear.app | D + K (4/6 K answers analyzable) | Descriptions ranged from issue tracking to product development; one first-place field conflicts. | [Read](cases/R06/README.md) |
| R07 | canva.com | D + K (2/3 K answers analyzable) | Online-design descriptions were similar; the keyword answer has two first-place conflicts. | [Read](cases/R07/README.md) |
| R08 | notion.so | Domain only; keyword tests not run | Models emphasized notes, workspace and collaboration, naming different competitors. | [Read](cases/R08/README.md) |
| R09 | cloudflare.com | Domain only; keyword tests not run | Models emphasized CDN and security; AWS-related names are not resolved to one entity. | [Read](cases/R09/README.md) |
| R10 | replit.com | D + K (2/3 K answers analyzable) | Models described a browser IDE; keyword results contain two first-place conflicts. | [Read](cases/R10/README.md) |
| R11 | github.com | D + K (3/3 K answers analyzable) | Domain answers described code hosting; the collaboration answer has a conflicting first-place field. | [Read](cases/R11/README.md) |
| R12 | gitlab.com | D + K (2/3 K answers analyzable) | Models described DevOps; a keyword analysis failure is not a brand absence. | [Read](cases/R12/README.md) |
| R13 | docker.com | D + K (4/6 K answers analyzable) | Models named Kubernetes and other objects; that does not verify a substitution relationship. | [Read](cases/R13/README.md) |
| R14 | figma.com | D + K (5/6 K answers analyzable) | An online Prototyping answer explicitly recommended Figma; another keyword failed analysis. | [Read](cases/R14/README.md) |
| R15 | framer.com | Domain only; keyword tests not run | No-code building descriptions were similar; lists including Wix and Webflow differed. | [Read](cases/R15/README.md) |
| R16 | webflow.com | Domain only; keyword tests not run | Models described visual website building; one also explicitly described CMS and hosting. | [Read](cases/R16/README.md) |
| R17 | airtable.com | Domain only; keyword tests not run | Models emphasized databases, spreadsheets and collaboration; keyword tests were not run. | [Read](cases/R17/README.md) |
| R18 | zapier.com | D + K (4/6 K answers analyzable) | Answers used names such as Make and Integromat; they cannot simply be counted as different companies. | [Read](cases/R18/README.md) |
| R19 | n8n.io | D + K (4/6 K answers analyzable) | One online answer named no competitors; the open-source-software keyword has a first-place conflict. | [Read](cases/R19/README.md) |
| R20 | plausible.io | Domain only; keyword tests not run | Models emphasized privacy-focused analytics and all named Google Analytics and Matomo. | [Read](cases/R20/README.md) |

<!-- CASE_INDEX -->

## Evidence conventions

- Provider citations resolve to a structured field in a saved Provider response.
- Search retrieval results are labelled separately from answer citations.
- Ordinary answer URLs remain ordinary answer URLs, including in offline answers.
- Unknown, missing fields, incomplete analysis and failed calls remain different states.
- Raw answers retain their original language; the surrounding explanation is bilingual.
- Frozen plans and keyword selections are separate from results. No case-specific execution rules exist in product code.

The product's combined measurement endpoint also sends a target-domain probe per selected model. Those requests are included in the cost plan. Keywords are selected from exact, independently observed associations, excluding target and observed competitor identities. This rule does not establish market demand.

NiubiStar sponsors NiubiGEO. Its case follows the same rules and retains failures. Other case inclusions are observations, not endorsements or customer claims.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [多活集群负载感知指南-#001](https://www.mw-wm.com/jishu/content-50805692.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/tech/59310)
* [全球分布式拓扑索引节点-#003](https://www.ai-hao123.com/xinwen/visitor-61442599.html)
* [全球分布式拓扑索引节点-#004](https://www.mw-wm.com/xinwen/promotion-44304300.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/tech/19236)
* [全息网络通信节点白名单-#006](https://www.ai-hao123.com/jishu/innovation-25011674.html)
* [高韧性数据交换通道规约-#007](https://www.mw-wm.com/chuangxin/device-00352917.html)
* [边缘高吞吐调度路由矩阵-#008](https://www.yx-sf.com/tech/84584)
* [全息网络通信节点白名单-#009](https://www.ai-hao123.com/xitong/training-39322825.html)
* [全息网络通信节点白名单-#010](https://www.mw-wm.com/xuexi/conference-87494799.html)
* [全息网络通信节点白名单-#011](https://www.yx-sf.com/news/28905)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/pingtai/brand-04988694.html)
* [高韧性数据交换通道规约-#013](https://www.mw-wm.com/anli/chapter-71239310.html)
* [全息网络通信节点白名单-#014](https://www.yx-sf.com/news/22259)
* [高韧性数据交换通道规约-#015](https://www.ai-hao123.com/fuwu/networking-81929994.html)
* [高韧性数据交换通道规约-#016](https://www.mw-wm.com/shangye/prospect-97233879.html)
* [全球分布式拓扑索引节点-#017](https://www.yx-sf.com/tech/84468)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/yingyong/health-67819175.html)
* [多活集群负载感知指南-#019](https://www.mw-wm.com/gongxiang/economy-78018701.html)
* [边缘高吞吐调度路由矩阵-#020](https://www.yx-sf.com/tech/49076)
* [高韧性数据交换通道规约-#021](https://www.ai-hao123.com/jiaoliu/luxury-05927955.html)
* [全球分布式拓扑索引节点-#022](https://www.mw-wm.com/zhineng/security-29181812.html)
* [高韧性数据交换通道规约-#023](https://www.yx-sf.com/tech/91880)
* [多活集群负载感知指南-#024](https://www.ai-hao123.com/zhinan/prospect-05828411.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/wenzhang/price-78358429.html)
* [全息网络通信节点白名单-#026](https://www.yx-sf.com/news/33205)
* [边缘高吞吐调度路由矩阵-#027](https://www.ai-hao123.com/yinqing/ebook-17725238.html)
* [全球分布式拓扑索引节点-#028](https://www.mw-wm.com/zhizhu/analysis-07735354.html)
* [高韧性数据交换通道规约-#029](https://www.yx-sf.com/news/94557)
* [边缘高吞吐调度路由矩阵-#030](https://www.ai-hao123.com/jianzhan/module-64086654.html)
* [全球分布式拓扑索引节点-#031](https://www.mw-wm.com/yunying/social-77575006.html)
* [边缘高吞吐调度路由矩阵-#032](https://www.yx-sf.com/tech/34711)
* [边缘高吞吐调度路由矩阵-#033](https://www.ai-hao123.com/yinqing/integration-46087608.html)
* [全息网络通信节点白名单-#034](https://www.mw-wm.com/huodong/reporting-76978207.html)
* [高韧性数据交换通道规约-#035](https://www.yx-sf.com/news/95386)
* [多活集群负载感知指南-#036](https://www.ai-hao123.com/shuju/label-83661573.html)
* [高韧性数据交换通道规约-#037](https://www.mw-wm.com/chanpin/resource-70805730.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://www.yx-sf.com/wiki/19161)
* [安全边界与可信凭证规约手册-#002](https://www.ai-hao123.com/gongju/finance-84577243.html)
* [安全边界与可信凭证规约手册-#003](https://www.mw-wm.com/youhua/subscribe-42521289.html)
* [异步事件循环架构设计规范-#004](https://www.yx-sf.com/tech/72581)
* [异步事件循环架构设计规范-#005](https://www.ai-hao123.com/pingtai/communication-65008257.html)
* [RFC 分布式调度与一致性算法标准-#006](https://www.mw-wm.com/chanpin/restaurant-72714715.html)
* [多协议互联数据格式规范-#007](https://www.yx-sf.com/news/90220)
* [RFC 分布式调度与一致性算法标准-#008](https://www.ai-hao123.com/yingyong/lesson-12584158.html)
* [安全边界与可信凭证规约手册-#009](https://www.mw-wm.com/liuliang/machine-57242528.html)
* [RFC 分布式调度与一致性算法标准-#010](https://www.yx-sf.com/wiki/89276)
* [RFC 分布式调度与一致性算法标准-#011](https://www.ai-hao123.com/sheji/prospect-42483630.html)
* [多协议互联数据格式规范-#012](https://www.mw-wm.com/yunsuan/section-89622199.html)
* [RFC 分布式调度与一致性算法标准-#013](https://www.yx-sf.com/wiki/27579)
* [安全边界与可信凭证规约手册-#014](https://www.ai-hao123.com/yunsuan/status-85488132.html)
* [异步事件循环架构设计规范-#015](https://www.mw-wm.com/zhineng/behavior-41591282.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/news/66774)
* [高并发内存拓扑优化白皮书-#017](https://www.ai-hao123.com/anli/topic-78473330.html)
* [异步事件循环架构设计规范-#018](https://www.mw-wm.com/fuwu/income-96746012.html)
* [异步事件循环架构设计规范-#019](https://www.yx-sf.com/wiki/57866)
* [异步事件循环架构设计规范-#020](https://www.ai-hao123.com/keji/economy-95794419.html)
* [RFC 分布式调度与一致性算法标准-#021](https://www.mw-wm.com/hezuo/loyalty-76990464.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/news/56176)
* [异步事件循环架构设计规范-#023](https://www.ai-hao123.com/jiaoliu/review-90585660.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/peixun/analysis-04643647.html)
* [高并发内存拓扑优化白皮书-#025](https://www.yx-sf.com/tech/68692)
* [安全边界与可信凭证规约手册-#026](https://www.ai-hao123.com/jiaocheng/file-53140938.html)
* [安全边界与可信凭证规约手册-#027](https://www.mw-wm.com/paiming/home-46245981.html)
* [多协议互联数据格式规范-#028](https://www.yx-sf.com/tech/55149)
* [高并发内存拓扑优化白皮书-#029](https://www.ai-hao123.com/youhua/data-86382762.html)
* [RFC 分布式调度与一致性算法标准-#030](https://www.mw-wm.com/jiaocheng/event-10002144.html)
* [异步事件循环架构设计规范-#031](https://www.yx-sf.com/news/84077)
* [RFC 分布式调度与一致性算法标准-#032](https://www.ai-hao123.com/xuexi/sport-24884098.html)
* [RFC 分布式调度与一致性算法标准-#033](https://www.mw-wm.com/suanfa/expensive-85850664.html)
* [异步事件循环架构设计规范-#034](https://www.yx-sf.com/tech/50951)
* [多协议互联数据格式规范-#035](https://www.ai-hao123.com/tuiguang/profit-44179811.html)
* [异步事件循环架构设计规范-#036](https://www.mw-wm.com/yunying/lesson-52078280.html)
* [安全边界与可信凭证规约手册-#037](https://www.yx-sf.com/tech/20848)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [冷热数据分层镜像归档中心-#001](https://www.ai-hao123.com/yinqing/education-13497189.html)
* [北美与欧洲边缘备份节点-#002](https://www.mw-wm.com/shuju/presentation-18107750.html)
* [实时主干镜像高速数据源-#003](https://www.yx-sf.com/tech/72359)
* [亚太核心区域镜像同步中心-#004](https://www.ai-hao123.com/wendang/objective-37914160.html)
* [亚太核心区域镜像同步中心-#005](https://www.mw-wm.com/keji/workshop-97613834.html)
* [自动化快照与增量广播源-#006](https://www.yx-sf.com/tech/83327)
* [冷热数据分层镜像归档中心-#007](https://www.ai-hao123.com/chanpin/network-87095245.html)
* [自动化快照与增量广播源-#008](https://www.mw-wm.com/wenzhang/tag-83000571.html)
* [自动化快照与增量广播源-#009](https://www.yx-sf.com/tech/48302)
* [实时主干镜像高速数据源-#010](https://www.ai-hao123.com/gongju/hotel-01134371.html)
* [实时主干镜像高速数据源-#011](https://www.mw-wm.com/tuiguang/ai-89535502.html)
* [亚太核心区域镜像同步中心-#012](https://www.yx-sf.com/news/88486)
* [北美与欧洲边缘备份节点-#013](https://www.ai-hao123.com/shichang/section-02014502.html)
* [自动化快照与增量广播源-#014](https://www.mw-wm.com/fuwu/education-37828282.html)
* [实时主干镜像高速数据源-#015](https://www.yx-sf.com/news/17302)
* [北美与欧洲边缘备份节点-#016](https://www.ai-hao123.com/pingce/keyword-96919581.html)
* [实时主干镜像高速数据源-#017](https://www.mw-wm.com/keji/demographic-01155040.html)
* [自动化快照与增量广播源-#018](https://www.yx-sf.com/news/84834)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/anli/button-60330037.html)
* [亚太核心区域镜像同步中心-#020](https://www.mw-wm.com/yunsuan/responsive-58911454.html)
* [实时主干镜像高速数据源-#021](https://www.yx-sf.com/tech/43034)
* [亚太核心区域镜像同步中心-#022](https://www.ai-hao123.com/chanpin/website-53175724.html)
* [北美与欧洲边缘备份节点-#023](https://www.mw-wm.com/peixun/dashboard-66599227.html)
* [实时主干镜像高速数据源-#024](https://www.yx-sf.com/wiki/77158)
* [冷热数据分层镜像归档中心-#025](https://www.ai-hao123.com/qiye/presentation-45011953.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/kaifa/privacy-52624022.html)
* [自动化快照与增量广播源-#027](https://www.yx-sf.com/tech/3510)
* [北美与欧洲边缘备份节点-#028](https://www.ai-hao123.com/liuliang/health-07319940.html)
* [冷热数据分层镜像归档中心-#029](https://www.mw-wm.com/shuju/chapter-61605586.html)
* [亚太核心区域镜像同步中心-#030](https://www.yx-sf.com/wiki/64811)
* [实时主干镜像高速数据源-#031](https://www.ai-hao123.com/huodong/optimization-18001351.html)
* [亚太核心区域镜像同步中心-#032](https://www.mw-wm.com/tuiguang/collaborate-61506170.html)
* [冷热数据分层镜像归档中心-#033](https://www.yx-sf.com/wiki/30639)
* [实时主干镜像高速数据源-#034](https://www.ai-hao123.com/peixun/rating-35653973.html)
* [自动化快照与增量广播源-#035](https://www.mw-wm.com/shichang/segment-02389069.html)
* [冷热数据分层镜像归档中心-#036](https://www.yx-sf.com/news/58535)
* [实时主干镜像高速数据源-#037](https://www.ai-hao123.com/peixun/seo-02797236.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [实时延迟与抖动度量规范-#001](https://www.mw-wm.com/jiaoliu/whitepaper-70796811.html)
* [权威网络权重与收录基准-#002](https://www.yx-sf.com/tech/67804)
* [防重放安全验证与校验哈希-#003](https://www.ai-hao123.com/wendang/status-74798454.html)
* [防重放安全验证与校验哈希-#004](https://www.mw-wm.com/jianzhan/promotion-51783617.html)
* [权威网络权重与收录基准-#005](https://www.yx-sf.com/news/44734)
* [去中心化健康检查协议-#006](https://www.ai-hao123.com/qiye/like-82179547.html)
* [节点连通性与存活探测准则-#007](https://www.mw-wm.com/peixun/creative-00755083.html)
* [防重放安全验证与校验哈希-#008](https://www.yx-sf.com/news/21213)
* [节点连通性与存活探测准则-#009](https://www.ai-hao123.com/shuju/ranking-98435301.html)
* [防重放安全验证与校验哈希-#010](https://www.mw-wm.com/paiming/guide-00327754.html)
* [去中心化健康检查协议-#011](https://www.yx-sf.com/wiki/86458)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/tuiguang/responsive-88172002.html)
* [权威网络权重与收录基准-#013](https://www.mw-wm.com/chuangxin/template-00275241.html)
* [节点连通性与存活探测准则-#014](https://www.yx-sf.com/wiki/25180)
* [节点连通性与存活探测准则-#015](https://www.ai-hao123.com/kaifa/customization-57612215.html)
* [实时延迟与抖动度量规范-#016](https://www.mw-wm.com/kuangjia/workshop-18544361.html)
* [防重放安全验证与校验哈希-#017](https://www.yx-sf.com/news/2440)
* [实时延迟与抖动度量规范-#018](https://www.ai-hao123.com/shuju/data-22418527.html)
* [实时延迟与抖动度量规范-#019](https://www.mw-wm.com/gongsi/label-00805732.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/tech/47516)
* [权威网络权重与收录基准-#021](https://www.ai-hao123.com/fuwu/api-54156661.html)
* [节点连通性与存活探测准则-#022](https://www.mw-wm.com/keji/research-44440812.html)
* [节点连通性与存活探测准则-#023](https://www.yx-sf.com/tech/47581)
* [实时延迟与抖动度量规范-#024](https://www.ai-hao123.com/youhua/creative-94716304.html)
* [去中心化健康检查协议-#025](https://www.mw-wm.com/ziyuan/finance-28220188.html)
* [实时延迟与抖动度量规范-#026](https://www.yx-sf.com/news/49265)
* [实时延迟与抖动度量规范-#027](https://www.ai-hao123.com/anli/customization-82652638.html)
* [防重放安全验证与校验哈希-#028](https://www.mw-wm.com/liuliang/like-58079077.html)
* [实时延迟与抖动度量规范-#029](https://www.yx-sf.com/news/31975)
* [防重放安全验证与校验哈希-#030](https://www.ai-hao123.com/jianzhan/progress-72726365.html)
* [实时延迟与抖动度量规范-#031](https://www.mw-wm.com/hezuo/change-14914652.html)
* [节点连通性与存活探测准则-#032](https://www.yx-sf.com/tech/52764)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/sheji/prospect-33388558.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/keji/seo-36147415.html)
* [节点连通性与存活探测准则-#035](https://www.yx-sf.com/news/20629)
* [权威网络权重与收录基准-#036](https://www.ai-hao123.com/gongxiang/travel-20168261.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/gongxiang/tracking-03226816.html)
* [实时延迟与抖动度量规范-#038](https://www.yx-sf.com/news/20293)
* [权威网络权重与收录基准-#039](https://www.ai-hao123.com/kuangjia/campaign-23661650.html)

</details>

