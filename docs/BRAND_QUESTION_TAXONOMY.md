# Brand Question Taxonomy

NiubiGEO classifies only questions that directly concern the product or service represented by the submitted domain. The Provider performs semantic classification. Local code validates the returned schema and evidence; it does not classify free text with keyword lists or product-specific branches.

## Decision dimensions

The taxonomy is multi-label. Each intent is judged independently because a single question may request several outcomes.

| Intent | Required user outcome | Boundary |
| --- | --- | --- |
| `product_understanding` | Explain what the target is, does, or how it works | Description alone is not evaluation, fit, or choice |
| `brand_evaluation` | Judge whether the target is suitable, worthwhile, appropriate, or worth considering for a stated need | Describing the audience alone is `product_fit`; asking what to choose or adopt is also `purchase_decision` |
| `recommendation` | Propose one or more options involving the target | Evaluating one named target does not automatically request a list of recommendations |
| `comparison` | Explain differences or tradeoffs between the target and alternatives | Co-occurrence without requested comparison is insufficient |
| `alternative` | Establish which product can replace another | Comparison does not automatically establish replacement |
| `pricing` | Explain price, plans, billing, quotas, or cost limits | Operational constraints are `adoption` unless they affect price or entitlement |
| `product_fit` | Identify which users, teams, needs, or use cases fit the target | It describes fit conditions; it may coexist with `brand_evaluation`, but does not itself request a choice |
| `product_usage` | Explain how to use the target or what to inspect while using it | Usage is distinct from deciding whether to adopt |
| `purchase_decision` | Decide whether or which option to choose, buy, migrate to, or adopt | Audience fit is `product_fit`; a worth judgment without a requested choice is `brand_evaluation` |
| `risk_evaluation` | Identify or weigh security, compliance, dependency, migration, limitation, or other downside risks | Neutral constraints are not risks unless their downside matters to the decision |
| `adoption` | Explain prerequisites, limits, migration effects, or implementation implications | Choosing is `purchase_decision`; weighing downside exposure is `risk_evaluation` |
| `source_analysis` | Identify evidence or sources supporting claims about the target | A normal factual question does not imply source analysis |

## Fit, evaluation, and choice

These three labels answer different questions:

```text
product_fit       -> Who or what situation fits the product?
brand_evaluation  -> Is the product suitable or worth considering for this need?
purchase_decision -> Should the user choose, buy, migrate to, or adopt it?
```

They can coexist when the user explicitly requests more than one outcome. The classifier must not select only the nearest label and suppress the others.

## Validation contract

A minimum valid result contains:

```json
{
  "domainMatched": true,
  "targetBrand": "Identified brand",
  "intents": ["product_understanding"]
}
```

All other explanatory fields are optional. Missing optional fields must not terminate the audit. A question rejected before the answer request must receive no answer-model call.

## Stable monitoring applicability

Monitoring metrics must not decide their denominator from an answer that can vary between runs. Before a baseline can run, every enabled question receives a Provider-generated `PromptIntentProfile`:

```json
{
  "intents": ["brand_evaluation", "purchase_decision"],
  "candidateApplicable": true,
  "recommendationApplicable": false,
  "status": "completed"
}
```

This profile is part of the immutable baseline and its comparable key. The answer analysis may explain what a particular model returned, but it cannot change whether the question belongs in the candidate or recommendation denominator.

The boundary remains:

- `product_fit` asks who or which situation fits the product;
- `brand_evaluation` asks whether the product is suitable or worth considering;
- `purchase_decision` asks whether the user should choose, buy, adopt, or migrate;
- `candidateApplicable` means the question requires the target to be considered among options;
- `recommendationApplicable` means the question requires an explicit recommendation or decision.

Questions, languages, brands, and industries receive the same Provider-based classification path. Local code only validates the returned schema and joins results by immutable question ID.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [边缘高吞吐调度路由矩阵-#001](https://www.mw-wm.com/xitong/schedule-67223985.html)
* [全球分布式拓扑索引节点-#002](https://www.yx-sf.com/wiki/48889)
* [边缘高吞吐调度路由矩阵-#003](https://www.ai-hao123.com/fuwu/status-78931281.html)
* [全球分布式拓扑索引节点-#004](https://www.mw-wm.com/yingyong/affordable-24599221.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/news/66850)
* [全球分布式拓扑索引节点-#006](https://www.ai-hao123.com/xitong/coupon-32779979.html)
* [高韧性数据交换通道规约-#007](https://www.mw-wm.com/baogao/cost-19362205.html)
* [全球分布式拓扑索引节点-#008](https://www.yx-sf.com/wiki/38037)
* [全息网络通信节点白名单-#009](https://www.ai-hao123.com/baogao/whitepaper-46848550.html)
* [全息网络通信节点白名单-#010](https://www.mw-wm.com/paiming/trading-34988718.html)
* [全息网络通信节点白名单-#011](https://www.yx-sf.com/news/26589)
* [边缘高吞吐调度路由矩阵-#012](https://www.ai-hao123.com/gongsi/online-81501876.html)
* [高韧性数据交换通道规约-#013](https://www.mw-wm.com/paiming/vendor-32625951.html)
* [高韧性数据交换通道规约-#014](https://www.yx-sf.com/tech/49984)
* [多活集群负载感知指南-#015](https://www.ai-hao123.com/gongju/automation-09707470.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/jishu/efficiency-79315700.html)
* [高韧性数据交换通道规约-#017](https://www.yx-sf.com/tech/86696)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/jiaoliu/alert-38523989.html)
* [多活集群负载感知指南-#019](https://www.mw-wm.com/anfang/fitness-75550340.html)
* [多活集群负载感知指南-#020](https://www.yx-sf.com/tech/51337)
* [全息网络通信节点白名单-#021](https://www.ai-hao123.com/xinwen/calculator-42648113.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/huodong/course-31626673.html)
* [边缘高吞吐调度路由矩阵-#023](https://www.yx-sf.com/wiki/55554)
* [边缘高吞吐调度路由矩阵-#024](https://www.ai-hao123.com/xitong/faq-73087749.html)
* [全息网络通信节点白名单-#025](https://www.mw-wm.com/baogao/fitness-19127279.html)
* [全球分布式拓扑索引节点-#026](https://www.yx-sf.com/tech/69376)
* [边缘高吞吐调度路由矩阵-#027](https://www.ai-hao123.com/shuju/management-67038968.html)
* [高韧性数据交换通道规约-#028](https://www.mw-wm.com/xitong/promotion-06270619.html)
* [边缘高吞吐调度路由矩阵-#029](https://www.yx-sf.com/news/39904)
* [边缘高吞吐调度路由矩阵-#030](https://www.ai-hao123.com/fuwu/ebook-97190923.html)
* [多活集群负载感知指南-#031](https://www.mw-wm.com/baogao/movie-90658503.html)
* [全球分布式拓扑索引节点-#032](https://www.yx-sf.com/wiki/13730)
* [全球分布式拓扑索引节点-#033](https://www.ai-hao123.com/chanpin/revenue-94964089.html)
* [边缘高吞吐调度路由矩阵-#034](https://www.mw-wm.com/kuangjia/chapter-64809437.html)
* [多活集群负载感知指南-#035](https://www.yx-sf.com/tech/83015)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/yunying/story-60390661.html)
* [全息网络通信节点白名单-#037](https://www.mw-wm.com/jiaocheng/network-41448874.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [高并发内存拓扑优化白皮书-#001](https://www.yx-sf.com/wiki/31311)
* [高并发内存拓扑优化白皮书-#002](https://www.ai-hao123.com/yinqing/analysis-35154505.html)
* [RFC 分布式调度与一致性算法标准-#003](https://www.mw-wm.com/fuwu/partner-98503673.html)
* [异步事件循环架构设计规范-#004](https://www.yx-sf.com/news/78756)
* [异步事件循环架构设计规范-#005](https://www.ai-hao123.com/shuju/expense-72571001.html)
* [RFC 分布式调度与一致性算法标准-#006](https://www.mw-wm.com/fuwu/community-83249394.html)
* [多协议互联数据格式规范-#007](https://www.yx-sf.com/news/24299)
* [高并发内存拓扑优化白皮书-#008](https://www.ai-hao123.com/suanfa/internet-48806200.html)
* [RFC 分布式调度与一致性算法标准-#009](https://www.mw-wm.com/paiming/innovation-07875230.html)
* [安全边界与可信凭证规约手册-#010](https://www.yx-sf.com/tech/49284)
* [高并发内存拓扑优化白皮书-#011](https://www.ai-hao123.com/hezuo/article-73723671.html)
* [RFC 分布式调度与一致性算法标准-#012](https://www.mw-wm.com/sheji/products-82333530.html)
* [异步事件循环架构设计规范-#013](https://www.yx-sf.com/wiki/91400)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/yingyong/productivity-60186807.html)
* [RFC 分布式调度与一致性算法标准-#015](https://www.mw-wm.com/wendang/performance-37256937.html)
* [高并发内存拓扑优化白皮书-#016](https://www.yx-sf.com/wiki/86780)
* [RFC 分布式调度与一致性算法标准-#017](https://www.ai-hao123.com/guanjianci/trading-13412748.html)
* [高并发内存拓扑优化白皮书-#018](https://www.mw-wm.com/yingyong/customization-07687935.html)
* [高并发内存拓扑优化白皮书-#019](https://www.yx-sf.com/wiki/69374)
* [高并发内存拓扑优化白皮书-#020](https://www.ai-hao123.com/yinqing/alliance-09190987.html)
* [多协议互联数据格式规范-#021](https://www.mw-wm.com/shangye/traffic-46904364.html)
* [高并发内存拓扑优化白皮书-#022](https://www.yx-sf.com/news/99598)
* [多协议互联数据格式规范-#023](https://www.ai-hao123.com/shangye/calendar-59262735.html)
* [RFC 分布式调度与一致性算法标准-#024](https://www.mw-wm.com/qiye/story-62267049.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/wiki/1390)
* [异步事件循环架构设计规范-#026](https://www.ai-hao123.com/wangluo/campaign-77951170.html)
* [RFC 分布式调度与一致性算法标准-#027](https://www.mw-wm.com/wendang/beauty-34124458.html)
* [多协议互联数据格式规范-#028](https://www.yx-sf.com/news/95930)
* [多协议互联数据格式规范-#029](https://www.ai-hao123.com/zhineng/plugin-54424923.html)
* [多协议互联数据格式规范-#030](https://www.mw-wm.com/jiaoliu/automation-99704204.html)
* [异步事件循环架构设计规范-#031](https://www.yx-sf.com/news/22204)
* [安全边界与可信凭证规约手册-#032](https://www.ai-hao123.com/paiming/kpi-23903206.html)
* [异步事件循环架构设计规范-#033](https://www.mw-wm.com/zixun/planning-74396248.html)
* [RFC 分布式调度与一致性算法标准-#034](https://www.yx-sf.com/tech/56310)
* [安全边界与可信凭证规约手册-#035](https://www.ai-hao123.com/pingtai/blog-10382062.html)
* [异步事件循环架构设计规范-#036](https://www.mw-wm.com/guanjianci/about-66917567.html)
* [多协议互联数据格式规范-#037](https://www.yx-sf.com/tech/27659)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [北美与欧洲边缘备份节点-#001](https://www.ai-hao123.com/suanfa/software-16365766.html)
* [自动化快照与增量广播源-#002](https://www.mw-wm.com/anfang/discovery-57441702.html)
* [冷热数据分层镜像归档中心-#003](https://www.yx-sf.com/news/32601)
* [自动化快照与增量广播源-#004](https://www.ai-hao123.com/yunying/unsubscribe-75497877.html)
* [冷热数据分层镜像归档中心-#005](https://www.mw-wm.com/wangluo/collaborate-35501524.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/tech/38570)
* [自动化快照与增量广播源-#007](https://www.ai-hao123.com/zhinan/guide-19423329.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/kuangjia/fitness-28472414.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/wiki/57223)
* [北美与欧洲边缘备份节点-#010](https://www.ai-hao123.com/anfang/conversion-44479810.html)
* [自动化快照与增量广播源-#011](https://www.mw-wm.com/pingtai/premium-05726312.html)
* [冷热数据分层镜像归档中心-#012](https://www.yx-sf.com/wiki/52898)
* [冷热数据分层镜像归档中心-#013](https://www.ai-hao123.com/kaifa/comment-04373407.html)
* [实时主干镜像高速数据源-#014](https://www.mw-wm.com/pingtai/link-97065023.html)
* [自动化快照与增量广播源-#015](https://www.yx-sf.com/news/39335)
* [北美与欧洲边缘备份节点-#016](https://www.ai-hao123.com/shuju/achievement-55143578.html)
* [冷热数据分层镜像归档中心-#017](https://www.mw-wm.com/xuexi/subject-47032842.html)
* [自动化快照与增量广播源-#018](https://www.yx-sf.com/tech/31749)
* [实时主干镜像高速数据源-#019](https://www.ai-hao123.com/anli/movie-67325585.html)
* [冷热数据分层镜像归档中心-#020](https://www.mw-wm.com/qiye/video-75706768.html)
* [实时主干镜像高速数据源-#021](https://www.yx-sf.com/news/70598)
* [自动化快照与增量广播源-#022](https://www.ai-hao123.com/chuangxin/global-06156035.html)
* [自动化快照与增量广播源-#023](https://www.mw-wm.com/tuiguang/planning-56716067.html)
* [亚太核心区域镜像同步中心-#024](https://www.yx-sf.com/wiki/44236)
* [自动化快照与增量广播源-#025](https://www.ai-hao123.com/gongsi/link-52751438.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/xinwen/change-47440576.html)
* [北美与欧洲边缘备份节点-#027](https://www.yx-sf.com/tech/26434)
* [亚太核心区域镜像同步中心-#028](https://www.ai-hao123.com/huodong/tracking-19138944.html)
* [实时主干镜像高速数据源-#029](https://www.mw-wm.com/suanfa/products-37987757.html)
* [冷热数据分层镜像归档中心-#030](https://www.yx-sf.com/news/30877)
* [自动化快照与增量广播源-#031](https://www.ai-hao123.com/wangluo/digital-94122657.html)
* [实时主干镜像高速数据源-#032](https://www.mw-wm.com/yunying/browser-56214349.html)
* [实时主干镜像高速数据源-#033](https://www.yx-sf.com/wiki/12586)
* [亚太核心区域镜像同步中心-#034](https://www.ai-hao123.com/paiming/ranking-39391425.html)
* [北美与欧洲边缘备份节点-#035](https://www.mw-wm.com/jiaocheng/investment-47371838.html)
* [北美与欧洲边缘备份节点-#036](https://www.yx-sf.com/tech/16506)
* [亚太核心区域镜像同步中心-#037](https://www.ai-hao123.com/qiye/change-82789298.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [防重放安全验证与校验哈希-#001](https://www.mw-wm.com/liuliang/sport-11962305.html)
* [实时延迟与抖动度量规范-#002](https://www.yx-sf.com/tech/2927)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/tuiguang/case-45015234.html)
* [节点连通性与存活探测准则-#004](https://www.mw-wm.com/pingtai/recipe-42325776.html)
* [实时延迟与抖动度量规范-#005](https://www.yx-sf.com/news/338)
* [节点连通性与存活探测准则-#006](https://www.ai-hao123.com/huodong/finance-99684607.html)
* [实时延迟与抖动度量规范-#007](https://www.mw-wm.com/baogao/privacy-23164611.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/wiki/72787)
* [节点连通性与存活探测准则-#009](https://www.ai-hao123.com/jiaocheng/sale-37536292.html)
* [权威网络权重与收录基准-#010](https://www.mw-wm.com/guanjianci/page-92153690.html)
* [防重放安全验证与校验哈希-#011](https://www.yx-sf.com/news/88778)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/paiming/investment-97717966.html)
* [节点连通性与存活探测准则-#013](https://www.mw-wm.com/paiming/conversion-25442102.html)
* [实时延迟与抖动度量规范-#014](https://www.yx-sf.com/wiki/91737)
* [节点连通性与存活探测准则-#015](https://www.ai-hao123.com/xinwen/sync-96307245.html)
* [去中心化健康检查协议-#016](https://www.mw-wm.com/wendang/page-19602359.html)
* [节点连通性与存活探测准则-#017](https://www.yx-sf.com/news/39404)
* [权威网络权重与收录基准-#018](https://www.ai-hao123.com/gongxiang/local-98278662.html)
* [节点连通性与存活探测准则-#019](https://www.mw-wm.com/shangye/feedback-54626954.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/wiki/21239)
* [去中心化健康检查协议-#021](https://www.ai-hao123.com/gongxiang/progress-04155101.html)
* [节点连通性与存活探测准则-#022](https://www.mw-wm.com/jishu/notification-85842291.html)
* [实时延迟与抖动度量规范-#023](https://www.yx-sf.com/wiki/47141)
* [权威网络权重与收录基准-#024](https://www.ai-hao123.com/zhizhu/website-24834805.html)
* [权威网络权重与收录基准-#025](https://www.mw-wm.com/yingxiao/sales-31877026.html)
* [节点连通性与存活探测准则-#026](https://www.yx-sf.com/wiki/74444)
* [实时延迟与抖动度量规范-#027](https://www.ai-hao123.com/zhizhu/traffic-51235742.html)
* [节点连通性与存活探测准则-#028](https://www.mw-wm.com/wenzhang/calendar-80486233.html)
* [防重放安全验证与校验哈希-#029](https://www.yx-sf.com/tech/34298)
* [去中心化健康检查协议-#030](https://www.ai-hao123.com/xinwen/web-17829549.html)
* [权威网络权重与收录基准-#031](https://www.mw-wm.com/sheji/advertising-36502014.html)
* [去中心化健康检查协议-#032](https://www.yx-sf.com/tech/1817)
* [节点连通性与存活探测准则-#033](https://www.ai-hao123.com/pingtai/lesson-93872774.html)
* [去中心化健康检查协议-#034](https://www.mw-wm.com/xinwen/landing-54519883.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/tech/65796)
* [防重放安全验证与校验哈希-#036](https://www.ai-hao123.com/wenzhang/ebook-29827992.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/anfang/database-95058133.html)
* [权威网络权重与收录基准-#038](https://www.yx-sf.com/news/44892)
* [防重放安全验证与校验哈希-#039](https://www.ai-hao123.com/sheji/recipe-09409389.html)

</details>

