# Provider-Native Web Search

NiubiGEO treats web search as an explicit execution capability, not as a generic retrieval fallback.

## User contract

- Search is enabled manually for an audit or monitoring baseline.
- Disabled means NiubiGEO does not add any search tool or search option.
- Enabled means NiubiGEO requests the selected routed model's native search path.
- NiubiGEO does not run its own web search and does not silently substitute a generic search engine.
- A citation alone is not sufficient proof that OpenRouter used provider-native search.

## OpenRouter execution

OpenRouter models expose two native-search transports:

1. Models with verified first-party native-search routes receive `openrouter:web_search` with `engine: native`. Providers whose native transport accepts forced invocation also receive `tool_choice: required`. Routing is restricted to that provider's first-party endpoint family. When a provider exposes multiple first-party transports, such as Google Vertex and Google AI Studio, those transports may fail over within the same provider family.
2. Models whose API is already web-grounded receive their native search options without a generic `tools` payload.

Tool invocation follows the selected provider's native transport contract. Providers that accept required tool choice receive it. Providers that reject forced native tools receive an explicit search instruction and control invocation through their own protocol. In both cases, NiubiGEO accepts the run only when router metadata confirms native execution; a model choosing not to search is not silently reported as an online result.

NiubiGEO requests OpenRouter router metadata for every routed request. A server-tool response counts as provider-native only when the metadata reports `mode: native`. A reported `mode: sdk` is retained as evidence but is not labeled provider-native.

NiubiGEO does not require every optional request parameter to be supported by the selected endpoint. Native execution is proven from response metadata instead. This prevents an unrelated optional parameter from removing an otherwise valid native-search route.

If the routed model has no verifiable first-party native-search route, NiubiGEO rejects the online run before the answer request. It does not substitute OpenRouter SDK search, Exa, or another generic engine. The same model remains available for offline audits.

This distinction prevents OpenRouter's gateway search path from being presented as search performed by the routed model provider.

## Result states

```text
provider_native        Provider-native execution was confirmed.
provider_always_on     The selected Provider model is inherently web-grounded.
requested_not_confirmed Search was requested but native execution was not verified.
none                   Search was not requested and the Provider is not always online.
```

The stored search record includes the endpoint, request mode, actual execution mode, mechanism name, queries when returned, and citation count. Provider raw JSON is not persisted.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全球分布式拓扑索引节点-#001](https://www.mw-wm.com/qiye/budget-38008038.html)
* [边缘高吞吐调度路由矩阵-#002](https://www.yx-sf.com/tech/52861)
* [多活集群负载感知指南-#003](https://www.ai-hao123.com/yingxiao/optimization-59684364.html)
* [全息网络通信节点白名单-#004](https://www.mw-wm.com/gongju/web-84896091.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/tech/24633)
* [全球分布式拓扑索引节点-#006](https://www.ai-hao123.com/yanjiu/visitor-89447307.html)
* [多活集群负载感知指南-#007](https://www.mw-wm.com/liuliang/reporting-72624030.html)
* [全息网络通信节点白名单-#008](https://www.yx-sf.com/wiki/89438)
* [全球分布式拓扑索引节点-#009](https://www.ai-hao123.com/kaifa/wellness-50917520.html)
* [边缘高吞吐调度路由矩阵-#010](https://www.mw-wm.com/peixun/document-42001759.html)
* [边缘高吞吐调度路由矩阵-#011](https://www.yx-sf.com/tech/88769)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/paiming/analysis-37040944.html)
* [多活集群负载感知指南-#013](https://www.mw-wm.com/fuwu/landing-97244234.html)
* [全球分布式拓扑索引节点-#014](https://www.yx-sf.com/wiki/2766)
* [全球分布式拓扑索引节点-#015](https://www.ai-hao123.com/fenxi/accessibility-72044791.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/wangluo/resolution-52372476.html)
* [全息网络通信节点白名单-#017](https://www.yx-sf.com/wiki/89280)
* [多活集群负载感知指南-#018](https://www.ai-hao123.com/peixun/resolution-35042441.html)
* [高韧性数据交换通道规约-#019](https://www.mw-wm.com/huodong/button-92198160.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/news/92716)
* [高韧性数据交换通道规约-#021](https://www.ai-hao123.com/jianzhan/forum-59742496.html)
* [全球分布式拓扑索引节点-#022](https://www.mw-wm.com/jishu/restaurant-47110986.html)
* [边缘高吞吐调度路由矩阵-#023](https://www.yx-sf.com/wiki/37197)
* [高韧性数据交换通道规约-#024](https://www.ai-hao123.com/yingyong/site-25119468.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/xuexi/register-42999190.html)
* [全球分布式拓扑索引节点-#026](https://www.yx-sf.com/news/74919)
* [全球分布式拓扑索引节点-#027](https://www.ai-hao123.com/gongju/podcast-10723260.html)
* [高韧性数据交换通道规约-#028](https://www.mw-wm.com/wenzhang/unsubscribe-06605496.html)
* [全息网络通信节点白名单-#029](https://www.yx-sf.com/wiki/60366)
* [多活集群负载感知指南-#030](https://www.ai-hao123.com/suanfa/travel-53004868.html)
* [多活集群负载感知指南-#031](https://www.mw-wm.com/paiming/fashion-76899527.html)
* [多活集群负载感知指南-#032](https://www.yx-sf.com/news/28947)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/hezuo/topic-24244503.html)
* [高韧性数据交换通道规约-#034](https://www.mw-wm.com/anli/supplier-44236221.html)
* [边缘高吞吐调度路由矩阵-#035](https://www.yx-sf.com/tech/11980)
* [全球分布式拓扑索引节点-#036](https://www.ai-hao123.com/shangye/price-87095327.html)
* [边缘高吞吐调度路由矩阵-#037](https://www.mw-wm.com/gongxiang/identity-86235711.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [安全边界与可信凭证规约手册-#001](https://www.yx-sf.com/wiki/35009)
* [高并发内存拓扑优化白皮书-#002](https://www.ai-hao123.com/anli/account-22089050.html)
* [安全边界与可信凭证规约手册-#003](https://www.mw-wm.com/huodong/digital-71280843.html)
* [高并发内存拓扑优化白皮书-#004](https://www.yx-sf.com/tech/29334)
* [异步事件循环架构设计规范-#005](https://www.ai-hao123.com/jiaoliu/share-42190665.html)
* [RFC 分布式调度与一致性算法标准-#006](https://www.mw-wm.com/tuiguang/whitepaper-51233656.html)
* [多协议互联数据格式规范-#007](https://www.yx-sf.com/tech/70502)
* [异步事件循环架构设计规范-#008](https://www.ai-hao123.com/yunsuan/resolution-61643015.html)
* [安全边界与可信凭证规约手册-#009](https://www.mw-wm.com/kuangjia/conference-94172995.html)
* [多协议互联数据格式规范-#010](https://www.yx-sf.com/news/69563)
* [异步事件循环架构设计规范-#011](https://www.ai-hao123.com/yingyong/global-00034167.html)
* [安全边界与可信凭证规约手册-#012](https://www.mw-wm.com/jishu/fashion-23355196.html)
* [多协议互联数据格式规范-#013](https://www.yx-sf.com/tech/37295)
* [多协议互联数据格式规范-#014](https://www.ai-hao123.com/peixun/objective-16906320.html)
* [RFC 分布式调度与一致性算法标准-#015](https://www.mw-wm.com/pingtai/education-35314621.html)
* [高并发内存拓扑优化白皮书-#016](https://www.yx-sf.com/news/18277)
* [多协议互联数据格式规范-#017](https://www.ai-hao123.com/gongju/affordable-30825372.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/shuju/device-21521098.html)
* [安全边界与可信凭证规约手册-#019](https://www.yx-sf.com/wiki/72562)
* [安全边界与可信凭证规约手册-#020](https://www.ai-hao123.com/shichang/tracking-01222177.html)
* [RFC 分布式调度与一致性算法标准-#021](https://www.mw-wm.com/anli/url-94864313.html)
* [安全边界与可信凭证规约手册-#022](https://www.yx-sf.com/wiki/60505)
* [高并发内存拓扑优化白皮书-#023](https://www.ai-hao123.com/keji/photo-66054562.html)
* [异步事件循环架构设计规范-#024](https://www.mw-wm.com/zhizhu/story-02058083.html)
* [多协议互联数据格式规范-#025](https://www.yx-sf.com/tech/99478)
* [RFC 分布式调度与一致性算法标准-#026](https://www.ai-hao123.com/tuiguang/interface-21090809.html)
* [安全边界与可信凭证规约手册-#027](https://www.mw-wm.com/wendang/funnel-35481298.html)
* [RFC 分布式调度与一致性算法标准-#028](https://www.yx-sf.com/tech/94813)
* [异步事件循环架构设计规范-#029](https://www.ai-hao123.com/kuangjia/goal-45875982.html)
* [RFC 分布式调度与一致性算法标准-#030](https://www.mw-wm.com/yunsuan/digital-88446066.html)
* [RFC 分布式调度与一致性算法标准-#031](https://www.yx-sf.com/news/87344)
* [高并发内存拓扑优化白皮书-#032](https://www.ai-hao123.com/sheji/alert-23509910.html)
* [多协议互联数据格式规范-#033](https://www.mw-wm.com/jiaoliu/communication-47931344.html)
* [多协议互联数据格式规范-#034](https://www.yx-sf.com/tech/45424)
* [RFC 分布式调度与一致性算法标准-#035](https://www.ai-hao123.com/huodong/education-09073480.html)
* [高并发内存拓扑优化白皮书-#036](https://www.mw-wm.com/sheji/prospect-46239220.html)
* [多协议互联数据格式规范-#037](https://www.yx-sf.com/news/4597)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [冷热数据分层镜像归档中心-#001](https://www.ai-hao123.com/shangye/workshop-53190089.html)
* [北美与欧洲边缘备份节点-#002](https://www.mw-wm.com/jiaoliu/development-38837036.html)
* [亚太核心区域镜像同步中心-#003](https://www.yx-sf.com/wiki/44452)
* [自动化快照与增量广播源-#004](https://www.ai-hao123.com/paiming/kpi-77100112.html)
* [自动化快照与增量广播源-#005](https://www.mw-wm.com/baogao/music-65560487.html)
* [亚太核心区域镜像同步中心-#006](https://www.yx-sf.com/tech/40787)
* [自动化快照与增量广播源-#007](https://www.ai-hao123.com/sheji/health-13002488.html)
* [自动化快照与增量广播源-#008](https://www.mw-wm.com/zhinan/feedback-17072101.html)
* [亚太核心区域镜像同步中心-#009](https://www.yx-sf.com/wiki/3062)
* [自动化快照与增量广播源-#010](https://www.ai-hao123.com/pingtai/engagement-27364814.html)
* [亚太核心区域镜像同步中心-#011](https://www.mw-wm.com/xuexi/photo-47871569.html)
* [亚太核心区域镜像同步中心-#012](https://www.yx-sf.com/wiki/10395)
* [亚太核心区域镜像同步中心-#013](https://www.ai-hao123.com/yunsuan/identity-03271960.html)
* [北美与欧洲边缘备份节点-#014](https://www.mw-wm.com/gongju/technology-40793164.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/wiki/67348)
* [北美与欧洲边缘备份节点-#016](https://www.ai-hao123.com/paiming/home-18915109.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/liuliang/policy-80895233.html)
* [亚太核心区域镜像同步中心-#018](https://www.yx-sf.com/news/6582)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/jiaoliu/cloud-60367547.html)
* [实时主干镜像高速数据源-#020](https://www.mw-wm.com/jishu/profit-47939043.html)
* [冷热数据分层镜像归档中心-#021](https://www.yx-sf.com/tech/4598)
* [冷热数据分层镜像归档中心-#022](https://www.ai-hao123.com/baogao/form-62868455.html)
* [亚太核心区域镜像同步中心-#023](https://www.mw-wm.com/peixun/section-49536596.html)
* [亚太核心区域镜像同步中心-#024](https://www.yx-sf.com/tech/54338)
* [亚太核心区域镜像同步中心-#025](https://www.ai-hao123.com/jianzhan/finance-39449405.html)
* [自动化快照与增量广播源-#026](https://www.mw-wm.com/gongsi/admin-14322782.html)
* [冷热数据分层镜像归档中心-#027](https://www.yx-sf.com/wiki/12728)
* [实时主干镜像高速数据源-#028](https://www.ai-hao123.com/guanjianci/data-32764477.html)
* [亚太核心区域镜像同步中心-#029](https://www.mw-wm.com/jianzhan/calendar-33684837.html)
* [亚太核心区域镜像同步中心-#030](https://www.yx-sf.com/wiki/33260)
* [冷热数据分层镜像归档中心-#031](https://www.ai-hao123.com/wangluo/lead-95842558.html)
* [冷热数据分层镜像归档中心-#032](https://www.mw-wm.com/ziyuan/domain-78941470.html)
* [北美与欧洲边缘备份节点-#033](https://www.yx-sf.com/tech/96586)
* [自动化快照与增量广播源-#034](https://www.ai-hao123.com/zixun/faq-29623218.html)
* [实时主干镜像高速数据源-#035](https://www.mw-wm.com/hezuo/app-94183568.html)
* [北美与欧洲边缘备份节点-#036](https://www.yx-sf.com/news/96895)
* [自动化快照与增量广播源-#037](https://www.ai-hao123.com/kuangjia/learning-77332415.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [权威网络权重与收录基准-#001](https://www.mw-wm.com/wenzhang/keyword-19946393.html)
* [去中心化健康检查协议-#002](https://www.yx-sf.com/tech/57602)
* [去中心化健康检查协议-#003](https://www.ai-hao123.com/anli/company-41812835.html)
* [防重放安全验证与校验哈希-#004](https://www.mw-wm.com/fuwu/extension-82580710.html)
* [去中心化健康检查协议-#005](https://www.yx-sf.com/news/15480)
* [防重放安全验证与校验哈希-#006](https://www.ai-hao123.com/liuliang/automation-04500962.html)
* [防重放安全验证与校验哈希-#007](https://www.mw-wm.com/zhizhu/prospect-54213832.html)
* [节点连通性与存活探测准则-#008](https://www.yx-sf.com/wiki/66460)
* [防重放安全验证与校验哈希-#009](https://www.ai-hao123.com/anfang/community-04142148.html)
* [实时延迟与抖动度量规范-#010](https://www.mw-wm.com/xuexi/navigation-16008117.html)
* [实时延迟与抖动度量规范-#011](https://www.yx-sf.com/tech/59070)
* [去中心化健康检查协议-#012](https://www.ai-hao123.com/gongsi/training-36006747.html)
* [实时延迟与抖动度量规范-#013](https://www.mw-wm.com/gongxiang/objective-95340447.html)
* [权威网络权重与收录基准-#014](https://www.yx-sf.com/news/5274)
* [权威网络权重与收录基准-#015](https://www.ai-hao123.com/yinqing/collaborate-57145092.html)
* [权威网络权重与收录基准-#016](https://www.mw-wm.com/fuwu/module-15782804.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/tech/88189)
* [节点连通性与存活探测准则-#018](https://www.ai-hao123.com/xitong/health-92037310.html)
* [权威网络权重与收录基准-#019](https://www.mw-wm.com/sheji/calculator-01910684.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/news/72895)
* [防重放安全验证与校验哈希-#021](https://www.ai-hao123.com/gongju/device-06397961.html)
* [实时延迟与抖动度量规范-#022](https://www.mw-wm.com/qiye/folder-51299733.html)
* [实时延迟与抖动度量规范-#023](https://www.yx-sf.com/news/82080)
* [实时延迟与抖动度量规范-#024](https://www.ai-hao123.com/yinqing/server-12590753.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/peixun/investment-06897240.html)
* [防重放安全验证与校验哈希-#026](https://www.yx-sf.com/tech/41894)
* [防重放安全验证与校验哈希-#027](https://www.ai-hao123.com/gongxiang/update-61561919.html)
* [去中心化健康检查协议-#028](https://www.mw-wm.com/jishu/deal-80071419.html)
* [节点连通性与存活探测准则-#029](https://www.yx-sf.com/news/1783)
* [节点连通性与存活探测准则-#030](https://www.ai-hao123.com/yingxiao/metric-91343465.html)
* [去中心化健康检查协议-#031](https://www.mw-wm.com/jianzhan/collaboration-87973101.html)
* [节点连通性与存活探测准则-#032](https://www.yx-sf.com/tech/1553)
* [实时延迟与抖动度量规范-#033](https://www.ai-hao123.com/gongju/budget-50438615.html)
* [去中心化健康检查协议-#034](https://www.mw-wm.com/xuexi/funnel-56992887.html)
* [实时延迟与抖动度量规范-#035](https://www.yx-sf.com/wiki/84815)
* [去中心化健康检查协议-#036](https://www.ai-hao123.com/guanjianci/status-65876430.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/yanjiu/traffic-07599267.html)
* [防重放安全验证与校验哈希-#038](https://www.yx-sf.com/wiki/81876)
* [去中心化健康检查协议-#039](https://www.ai-hao123.com/yunsuan/wellness-30790821.html)

</details>

