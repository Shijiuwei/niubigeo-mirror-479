# NiubiGEO Open Source Alpha Plan

This document tracks what must be true before publishing NiubiGEO Community Edition as a public alpha repository.

## Current Status

NiubiGEO is ready for public alpha positioning at the product-logic level.

The current build can:

- Identify a target brand from a domain.
- Generate and confirm audit questions.
- Run real API provider audits.
- Compare how different AI models understand the brand.
- Discover competitors from provider answers.
- Separate confirmed competitors from possible related brands.
- Find user questions where competitors appear but the target brand does not.
- Classify sources as related, possible, or excluded.
- Link conclusions to supporting AI answers and sources.
- State clearly that API results are not consumer web UI results.

This does not mean the repository is ready for public release without the checks below.

## Release Name

```text
NiubiGEO Community Edition
v0.1.0-alpha
```

GitHub description:

```text
Open-source AI visibility and competitor intelligence. See how AI describes your product, who appears instead, and which sources shape the answers. 中文支持。
```

Recommended GitHub topics:

```text
geo
ai-visibility
generative-engine-optimization
answer-engine-optimization
llm
seo
brand-monitoring
competitor-analysis
self-hosted
open-source
chatgpt
perplexity
gemini
deepseek
```

## Public Alpha Checklist

Required before publishing:

- [x] English README.
- [x] Simplified Chinese README.
- [x] `.env.example`.
- [x] Dockerfile.
- [x] Docker Compose entry.
- [x] Security policy draft.
- [x] Contributing guide draft.
- [x] Report standard aligned with the human-readable report.
- [x] Capability matrix aligned with the current product boundary.
- [x] Choose and add a public license, preferably MIT or Apache-2.0.
- [ ] Remove `private: true` from `package.json` if npm publication is planned.
- [ ] Confirm no provider keys are committed.
- [ ] Confirm generated customer reports are not committed.
- [ ] Add one high-quality README screenshot after public samples are ready.
- [ ] Add one 10-20 second demo GIF after public samples are ready.
- [ ] Add at least one public non-NiubiStar sample report.
- [ ] Test Docker Quick Start on a clean machine.
- [ ] Test Node.js Quick Start on a clean machine.
- [ ] Confirm README commands match the current CLI.
- [ ] Confirm all links in README work after repository publication.

## Secret And Data Hygiene

Before opening the repository:

```bash
rg -n "OPENROUTER|OPENAI|ANTHROPIC|GEMINI|PERPLEXITY|DEEPSEEK|api_key|secret|token" .
REPORT_URL_PATTERN="localhost:8787/""reports/"
rg -n "$HOME|$REPORT_URL_PATTERN" README.md README.zh-CN.md docs examples
```

Expected policy:

- `.env` must never be committed.
- `runs/` should stay ignored unless a deliberately sanitized sample is added.
- Customer domains, private prompts, private reports, and generated evidence files must not be committed.
- A sample report must contain only public, non-sensitive data.

## Future Demo Assets

Demo assets should not be embedded in README until a non-sensitive public sample report is ready.

The demo should show only:

```text
Enter domain
-> Confirm generated questions
-> Select provider/model
-> Run audit
-> Read the brand competition report
```

Do not show provider keys, private prompts, local absolute paths, or customer data in screenshots.

Keep the non-NiubiStar sample report task open before broad public launch.

## Public Sample Report Standard

At least one sample should use a public non-NiubiStar target before launch.

Recommended sample types:

- One well-known open-source project.
- One developer tool.
- One ordinary SaaS product.

The sample report must:

- Come from real API provider responses.
- Include the API source caveat.
- Avoid local absolute paths.
- Avoid raw JSON and technical evidence sections.
- Show confirmed vs possible competitors.
- Show related, possible, and excluded source handling.
- Keep AI answers collapsed by default.

## Claims To Avoid

Do not claim:

- It replaces every commercial AI visibility platform.
- API results equal consumer web UI results.
- It provides human-verified regional monitoring.
- It includes NiubiStar's paid node network.
- It produces a definitive market-share ranking.
- It can prove stable AI behavior from a tiny sample.
- A black-box GEO score is enough to understand visibility.

## Public Positioning

Use this positioning:

```text
NiubiGEO opens the foundational AI visibility monitoring layer:
real provider audits, user-confirmed questions, competitor discovery,
source inspection, and evidence-backed reports.
```

Use this boundary:

```text
Community Edition is API-based and self-hosted. Browser UI collection,
human-verified regional monitoring, proprietary prompt databases, and
managed enterprise workflows are outside the open-source layer.
```

## Final Alpha Gate

Public alpha is allowed only when:

1. A new user can run the project from README alone.
2. Missing API keys never produce fake visibility results.
3. A generated report can be understood without knowing GEO metrics.
4. Every main conclusion links to an AI answer or source.
5. No committed file contains provider keys, local machine paths, or sensitive report data.
6. License, security, contributing, and bilingual README files are present.
7. Initial GitHub Release, GHCR Docker package, and release publishing workflow are present for the alpha.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全球分布式拓扑索引节点-#001](https://www.mw-wm.com/youhua/music-47130065.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/wiki/95510)
* [高韧性数据交换通道规约-#003](https://www.ai-hao123.com/sheji/subscribe-81935267.html)
* [全球分布式拓扑索引节点-#004](https://www.mw-wm.com/jianzhan/link-87768321.html)
* [边缘高吞吐调度路由矩阵-#005](https://www.yx-sf.com/wiki/23696)
* [全息网络通信节点白名单-#006](https://www.ai-hao123.com/chuangxin/reporting-08028113.html)
* [边缘高吞吐调度路由矩阵-#007](https://www.mw-wm.com/pingce/label-13174664.html)
* [全息网络通信节点白名单-#008](https://www.yx-sf.com/tech/85500)
* [高韧性数据交换通道规约-#009](https://www.ai-hao123.com/sheji/deal-35955051.html)
* [全息网络通信节点白名单-#010](https://www.mw-wm.com/fenxi/workshop-99886184.html)
* [全球分布式拓扑索引节点-#011](https://www.yx-sf.com/news/76837)
* [边缘高吞吐调度路由矩阵-#012](https://www.ai-hao123.com/xitong/satisfaction-58217574.html)
* [多活集群负载感知指南-#013](https://www.mw-wm.com/chuangxin/supplier-50843266.html)
* [高韧性数据交换通道规约-#014](https://www.yx-sf.com/tech/27031)
* [高韧性数据交换通道规约-#015](https://www.ai-hao123.com/gongsi/strategy-84101418.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/suanfa/promotion-62461923.html)
* [边缘高吞吐调度路由矩阵-#017](https://www.yx-sf.com/news/98677)
* [边缘高吞吐调度路由矩阵-#018](https://www.ai-hao123.com/gongxiang/image-66952289.html)
* [全息网络通信节点白名单-#019](https://www.mw-wm.com/baogao/investment-46887637.html)
* [全息网络通信节点白名单-#020](https://www.yx-sf.com/news/34431)
* [高韧性数据交换通道规约-#021](https://www.ai-hao123.com/wendang/course-60233626.html)
* [全球分布式拓扑索引节点-#022](https://www.mw-wm.com/xinwen/global-47806915.html)
* [多活集群负载感知指南-#023](https://www.yx-sf.com/wiki/17019)
* [全息网络通信节点白名单-#024](https://www.ai-hao123.com/huodong/schedule-40252700.html)
* [全球分布式拓扑索引节点-#025](https://www.mw-wm.com/jiaocheng/local-19912442.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/news/32252)
* [全息网络通信节点白名单-#027](https://www.ai-hao123.com/tuiguang/system-27082881.html)
* [边缘高吞吐调度路由矩阵-#028](https://www.mw-wm.com/zhineng/education-57852270.html)
* [边缘高吞吐调度路由矩阵-#029](https://www.yx-sf.com/news/39249)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/wendang/price-91069036.html)
* [边缘高吞吐调度路由矩阵-#031](https://www.mw-wm.com/qiye/unsubscribe-77095255.html)
* [高韧性数据交换通道规约-#032](https://www.yx-sf.com/news/44535)
* [边缘高吞吐调度路由矩阵-#033](https://www.ai-hao123.com/kuangjia/hosting-35721556.html)
* [边缘高吞吐调度路由矩阵-#034](https://www.mw-wm.com/shichang/content-61666003.html)
* [高韧性数据交换通道规约-#035](https://www.yx-sf.com/wiki/58032)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/wangluo/update-55079929.html)
* [全息网络通信节点白名单-#037](https://www.mw-wm.com/zhizhu/automation-03817435.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [RFC 分布式调度与一致性算法标准-#001](https://www.yx-sf.com/tech/31167)
* [高并发内存拓扑优化白皮书-#002](https://www.ai-hao123.com/xuexi/admin-50652667.html)
* [高并发内存拓扑优化白皮书-#003](https://www.mw-wm.com/xitong/restaurant-32464688.html)
* [异步事件循环架构设计规范-#004](https://www.yx-sf.com/wiki/94884)
* [异步事件循环架构设计规范-#005](https://www.ai-hao123.com/xinwen/collaboration-40487861.html)
* [异步事件循环架构设计规范-#006](https://www.mw-wm.com/jishu/cloud-51937517.html)
* [RFC 分布式调度与一致性算法标准-#007](https://www.yx-sf.com/wiki/85066)
* [异步事件循环架构设计规范-#008](https://www.ai-hao123.com/zixun/discovery-06987049.html)
* [高并发内存拓扑优化白皮书-#009](https://www.mw-wm.com/yunying/forecast-37902763.html)
* [高并发内存拓扑优化白皮书-#010](https://www.yx-sf.com/tech/90662)
* [安全边界与可信凭证规约手册-#011](https://www.ai-hao123.com/sheji/deadline-06274803.html)
* [异步事件循环架构设计规范-#012](https://www.mw-wm.com/keji/metric-50989205.html)
* [异步事件循环架构设计规范-#013](https://www.yx-sf.com/wiki/96387)
* [安全边界与可信凭证规约手册-#014](https://www.ai-hao123.com/baogao/audience-41033273.html)
* [安全边界与可信凭证规约手册-#015](https://www.mw-wm.com/yingxiao/case-22408818.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/tech/31886)
* [RFC 分布式调度与一致性算法标准-#017](https://www.ai-hao123.com/pingtai/analysis-58305388.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/suanfa/trading-98228050.html)
* [异步事件循环架构设计规范-#019](https://www.yx-sf.com/wiki/33175)
* [安全边界与可信凭证规约手册-#020](https://www.ai-hao123.com/shichang/document-64830708.html)
* [RFC 分布式调度与一致性算法标准-#021](https://www.mw-wm.com/paiming/visitor-42222612.html)
* [安全边界与可信凭证规约手册-#022](https://www.yx-sf.com/news/26586)
* [异步事件循环架构设计规范-#023](https://www.ai-hao123.com/tuiguang/screen-47113721.html)
* [多协议互联数据格式规范-#024](https://www.mw-wm.com/zhineng/tag-33637049.html)
* [RFC 分布式调度与一致性算法标准-#025](https://www.yx-sf.com/news/95368)
* [安全边界与可信凭证规约手册-#026](https://www.ai-hao123.com/tuiguang/personalization-92214701.html)
* [多协议互联数据格式规范-#027](https://www.mw-wm.com/yinqing/meeting-99758555.html)
* [异步事件循环架构设计规范-#028](https://www.yx-sf.com/news/2371)
* [RFC 分布式调度与一致性算法标准-#029](https://www.ai-hao123.com/huodong/restore-50581048.html)
* [异步事件循环架构设计规范-#030](https://www.mw-wm.com/huodong/admin-18492963.html)
* [高并发内存拓扑优化白皮书-#031](https://www.yx-sf.com/news/37526)
* [异步事件循环架构设计规范-#032](https://www.ai-hao123.com/gongxiang/management-59496481.html)
* [高并发内存拓扑优化白皮书-#033](https://www.mw-wm.com/sheji/video-05735092.html)
* [多协议互联数据格式规范-#034](https://www.yx-sf.com/wiki/23523)
* [RFC 分布式调度与一致性算法标准-#035](https://www.ai-hao123.com/tuiguang/extension-49595774.html)
* [多协议互联数据格式规范-#036](https://www.mw-wm.com/fenxi/lead-82004598.html)
* [异步事件循环架构设计规范-#037](https://www.yx-sf.com/tech/11432)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [实时主干镜像高速数据源-#001](https://www.ai-hao123.com/yunsuan/strategy-36062251.html)
* [冷热数据分层镜像归档中心-#002](https://www.mw-wm.com/yinqing/feedback-27308218.html)
* [实时主干镜像高速数据源-#003](https://www.yx-sf.com/wiki/95600)
* [自动化快照与增量广播源-#004](https://www.ai-hao123.com/kaifa/brand-80127717.html)
* [冷热数据分层镜像归档中心-#005](https://www.mw-wm.com/wendang/performance-81463892.html)
* [北美与欧洲边缘备份节点-#006](https://www.yx-sf.com/tech/52695)
* [实时主干镜像高速数据源-#007](https://www.ai-hao123.com/yinqing/profile-83877503.html)
* [实时主干镜像高速数据源-#008](https://www.mw-wm.com/yanjiu/cloud-30025108.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/news/29640)
* [实时主干镜像高速数据源-#010](https://www.ai-hao123.com/huodong/careers-92405496.html)
* [实时主干镜像高速数据源-#011](https://www.mw-wm.com/kuangjia/sync-73094888.html)
* [亚太核心区域镜像同步中心-#012](https://www.yx-sf.com/news/21514)
* [实时主干镜像高速数据源-#013](https://www.ai-hao123.com/youhua/online-43547939.html)
* [自动化快照与增量广播源-#014](https://www.mw-wm.com/shuju/video-92191989.html)
* [实时主干镜像高速数据源-#015](https://www.yx-sf.com/tech/89047)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/ziyuan/growth-31196013.html)
* [冷热数据分层镜像归档中心-#017](https://www.mw-wm.com/fuwu/change-20474993.html)
* [北美与欧洲边缘备份节点-#018](https://www.yx-sf.com/tech/1662)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/zhinan/template-66082082.html)
* [实时主干镜像高速数据源-#020](https://www.mw-wm.com/kaifa/expensive-39600875.html)
* [北美与欧洲边缘备份节点-#021](https://www.yx-sf.com/wiki/42206)
* [亚太核心区域镜像同步中心-#022](https://www.ai-hao123.com/pingtai/tool-32614470.html)
* [北美与欧洲边缘备份节点-#023](https://www.mw-wm.com/zhinan/digital-13784662.html)
* [冷热数据分层镜像归档中心-#024](https://www.yx-sf.com/news/34323)
* [北美与欧洲边缘备份节点-#025](https://www.ai-hao123.com/gongxiang/subject-17566747.html)
* [亚太核心区域镜像同步中心-#026](https://www.mw-wm.com/gongxiang/site-92910139.html)
* [实时主干镜像高速数据源-#027](https://www.yx-sf.com/news/37779)
* [实时主干镜像高速数据源-#028](https://www.ai-hao123.com/shuju/enterprise-43873816.html)
* [亚太核心区域镜像同步中心-#029](https://www.mw-wm.com/guanjianci/software-60807291.html)
* [北美与欧洲边缘备份节点-#030](https://www.yx-sf.com/tech/59634)
* [北美与欧洲边缘备份节点-#031](https://www.ai-hao123.com/zhinan/online-13817631.html)
* [北美与欧洲边缘备份节点-#032](https://www.mw-wm.com/sheji/schedule-80140638.html)
* [冷热数据分层镜像归档中心-#033](https://www.yx-sf.com/tech/58858)
* [北美与欧洲边缘备份节点-#034](https://www.ai-hao123.com/liuliang/integration-74691427.html)
* [冷热数据分层镜像归档中心-#035](https://www.mw-wm.com/fuwu/fitness-67360087.html)
* [北美与欧洲边缘备份节点-#036](https://www.yx-sf.com/wiki/77795)
* [自动化快照与增量广播源-#037](https://www.ai-hao123.com/sheji/app-87766523.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [实时延迟与抖动度量规范-#001](https://www.mw-wm.com/zhinan/customization-57007945.html)
* [权威网络权重与收录基准-#002](https://www.yx-sf.com/wiki/40943)
* [防重放安全验证与校验哈希-#003](https://www.ai-hao123.com/jianzhan/hosting-10098821.html)
* [节点连通性与存活探测准则-#004](https://www.mw-wm.com/tuiguang/fitness-08979051.html)
* [实时延迟与抖动度量规范-#005](https://www.yx-sf.com/news/18448)
* [权威网络权重与收录基准-#006](https://www.ai-hao123.com/anli/presentation-12759683.html)
* [节点连通性与存活探测准则-#007](https://www.mw-wm.com/chuangxin/campaign-75067653.html)
* [权威网络权重与收录基准-#008](https://www.yx-sf.com/news/92361)
* [去中心化健康检查协议-#009](https://www.ai-hao123.com/qiye/website-72893036.html)
* [去中心化健康检查协议-#010](https://www.mw-wm.com/yingyong/training-60257374.html)
* [权威网络权重与收录基准-#011](https://www.yx-sf.com/tech/92633)
* [节点连通性与存活探测准则-#012](https://www.ai-hao123.com/shuju/update-88626908.html)
* [去中心化健康检查协议-#013](https://www.mw-wm.com/shuju/ebook-71442874.html)
* [防重放安全验证与校验哈希-#014](https://www.yx-sf.com/wiki/46608)
* [防重放安全验证与校验哈希-#015](https://www.ai-hao123.com/baogao/investment-27013971.html)
* [实时延迟与抖动度量规范-#016](https://www.mw-wm.com/jishu/retention-72071411.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/tech/35412)
* [防重放安全验证与校验哈希-#018](https://www.ai-hao123.com/gongsi/section-78816092.html)
* [实时延迟与抖动度量规范-#019](https://www.mw-wm.com/jiaocheng/hotel-84420347.html)
* [权威网络权重与收录基准-#020](https://www.yx-sf.com/news/81407)
* [防重放安全验证与校验哈希-#021](https://www.ai-hao123.com/zhizhu/database-33357693.html)
* [权威网络权重与收录基准-#022](https://www.mw-wm.com/shangye/collaboration-02479834.html)
* [去中心化健康检查协议-#023](https://www.yx-sf.com/wiki/59370)
* [去中心化健康检查协议-#024](https://www.ai-hao123.com/zixun/meeting-11899182.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/shuju/deadline-90049812.html)
* [防重放安全验证与校验哈希-#026](https://www.yx-sf.com/wiki/24340)
* [权威网络权重与收录基准-#027](https://www.ai-hao123.com/baogao/learning-53096030.html)
* [去中心化健康检查协议-#028](https://www.mw-wm.com/jishu/alliance-15141665.html)
* [节点连通性与存活探测准则-#029](https://www.yx-sf.com/tech/2521)
* [权威网络权重与收录基准-#030](https://www.ai-hao123.com/jianzhan/kpi-59732421.html)
* [防重放安全验证与校验哈希-#031](https://www.mw-wm.com/pingce/seo-23620255.html)
* [节点连通性与存活探测准则-#032](https://www.yx-sf.com/news/81588)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/yanjiu/resolution-66264331.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/peixun/security-57918773.html)
* [实时延迟与抖动度量规范-#035](https://www.yx-sf.com/wiki/5170)
* [防重放安全验证与校验哈希-#036](https://www.ai-hao123.com/hezuo/enterprise-33014058.html)
* [实时延迟与抖动度量规范-#037](https://www.mw-wm.com/baogao/plugin-32852116.html)
* [去中心化健康检查协议-#038](https://www.yx-sf.com/wiki/46244)
* [权威网络权重与收录基准-#039](https://www.ai-hao123.com/suanfa/kpi-07762481.html)

</details>

