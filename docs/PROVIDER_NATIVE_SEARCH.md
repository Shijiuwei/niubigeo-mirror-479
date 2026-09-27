# Provider-Native Web Search

NiubiGEO treats web access as a Provider execution concern, not as a report decoration.

The goal is to capture what the user receives from each selected AI Provider API. If a Provider has a native search or grounding feature, NiubiGEO sends that Provider's own tool configuration and records what was actually used.

## Flow

```text
User selects Provider, model, and web search setting
-> ProviderCatalog declares native web-search capability
-> Provider adapter builds the Provider-specific request
-> AnswerResult.search records the actual execution
-> PromptRun stores the same search metadata
-> Reports show simple source facts beside each AI answer
```

## Provider Paths

| Provider | Native path | Current behavior |
|---|---|---|
| OpenAI | Responses API + `web_search` | Sends `tools: [{ type: "web_search" }]` when enabled |
| OpenRouter | Chat Completions + web plugin | Sends `plugins: [{ id: "web" }]` when enabled |
| Anthropic Claude | Messages API + Claude web search server tool | Sends `tools: [{ type: "web_search_20250305", name: "web_search" }]` when enabled |
| Google Gemini | generateContent + Google Search grounding | Sends `tools: [{ google_search: {} }]` when enabled |
| Perplexity | Sonar web-grounded answers | Recorded as Provider web-grounded by design |
| DeepSeek | Responses-compatible `/responses` + `web_search` | Sends `tools: [{ type: "web_search" }]` when enabled |
| OpenAI-compatible | Custom Base URL + Responses-compatible `/responses` | Requires `OPENAI_COMPATIBLE_BASE_URL` and `OPENAI_COMPATIBLE_API_KEY` |

## Rules

- Web search off means no search, grounding, or web plugin tool is sent by NiubiGEO.
- Web search on means the Provider adapter must use the native Provider path.
- Ordinary web search results must not be counted as Provider citations.
- OpenRouter-routed models remain labeled as `Source: OpenRouter API`.
- Perplexity Sonar is marked as `provider_always_on`, because the Provider API is web-grounded by design.
- Custom OpenAI-compatible endpoints must fail clearly if their `/responses` endpoint does not support `web_search`; NiubiGEO must not silently fake the result.

## Stored Metadata

Each completed run can store:

```json
{
  "requested": true,
  "requestMode": "auto",
  "used": false,
  "usedMode": "requested_not_confirmed",
  "endpointKind": "official_api",
  "endpointProtocol": "responses",
  "endpointUrl": "https://api.openai.com/v1/responses",
  "toolName": "web_search",
  "webQueries": [],
  "citationCount": 0
}
```

`requested` means the provider-native search option was sent. `used` is true only when the response contains search evidence, except for providers that are always web-grounded such as Perplexity. If a provider accepts the option but returns no search evidence, the report shows `Search unconfirmed`.

This metadata is for source transparency. The user-facing report should explain the distinction in plain language such as `No web search`, `Search unconfirmed`, `Provider-native web search`, or `Provider web-grounded`.

## Empty token-limited structured responses

The Chat Completions adapter preserves an empty JSON-schema response with `finish_reason: length` only when the caller explicitly enables `preserveEmptyStructuredTruncation` and handles recovery. The recognition service enables this option for its own calls to retain the raw response, usage, cost, and search metadata and use its existing bounded recovery: one retry from 900 to 2000 output tokens. A second empty response remains an analysis failure. Other callers, including measurements that share the recognition executor, retain `empty_answer` errors and their existing failure or retry behavior; ordinary text, JSON-object, and function-tool empty responses still raise `empty_answer` even with the option enabled.

This does not substitute reasoning text for an answer or fabricate citations. OpenRouter requests continue to use only the OpenRouter key and retain `Source: OpenRouter API` labeling.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [边缘高吞吐调度路由矩阵-#001](https://www.mw-wm.com/tuiguang/podcast-39605519.html)
* [高韧性数据交换通道规约-#002](https://www.yx-sf.com/tech/3040)
* [多活集群负载感知指南-#003](https://www.ai-hao123.com/fenxi/study-20385032.html)
* [多活集群负载感知指南-#004](https://www.mw-wm.com/yinqing/feedback-70514303.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/news/88213)
* [多活集群负载感知指南-#006](https://www.ai-hao123.com/yinqing/conversion-49781634.html)
* [高韧性数据交换通道规约-#007](https://www.mw-wm.com/sheji/rating-91939561.html)
* [边缘高吞吐调度路由矩阵-#008](https://www.yx-sf.com/news/63373)
* [边缘高吞吐调度路由矩阵-#009](https://www.ai-hao123.com/peixun/communication-66127544.html)
* [高韧性数据交换通道规约-#010](https://www.mw-wm.com/hezuo/excellence-47031327.html)
* [多活集群负载感知指南-#011](https://www.yx-sf.com/news/90543)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/youhua/alliance-38296994.html)
* [高韧性数据交换通道规约-#013](https://www.mw-wm.com/zhineng/success-95641362.html)
* [高韧性数据交换通道规约-#014](https://www.yx-sf.com/wiki/88672)
* [多活集群负载感知指南-#015](https://www.ai-hao123.com/peixun/file-76141666.html)
* [多活集群负载感知指南-#016](https://www.mw-wm.com/kaifa/review-87720549.html)
* [全球分布式拓扑索引节点-#017](https://www.yx-sf.com/wiki/20455)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/jishu/contact-45307005.html)
* [高韧性数据交换通道规约-#019](https://www.mw-wm.com/yanjiu/productivity-99627765.html)
* [边缘高吞吐调度路由矩阵-#020](https://www.yx-sf.com/news/20948)
* [全球分布式拓扑索引节点-#021](https://www.ai-hao123.com/gongsi/creative-66370457.html)
* [多活集群负载感知指南-#022](https://www.mw-wm.com/yingxiao/community-03492471.html)
* [边缘高吞吐调度路由矩阵-#023](https://www.yx-sf.com/tech/18129)
* [全球分布式拓扑索引节点-#024](https://www.ai-hao123.com/wangluo/success-67049141.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/gongsi/conversion-39390132.html)
* [高韧性数据交换通道规约-#026](https://www.yx-sf.com/news/95176)
* [全球分布式拓扑索引节点-#027](https://www.ai-hao123.com/jishu/alert-43539191.html)
* [高韧性数据交换通道规约-#028](https://www.mw-wm.com/zhizhu/cloud-79928047.html)
* [多活集群负载感知指南-#029](https://www.yx-sf.com/wiki/76501)
* [多活集群负载感知指南-#030](https://www.ai-hao123.com/chanpin/machine-47219592.html)
* [全息网络通信节点白名单-#031](https://www.mw-wm.com/zixun/beauty-27067731.html)
* [高韧性数据交换通道规约-#032](https://www.yx-sf.com/tech/84506)
* [全息网络通信节点白名单-#033](https://www.ai-hao123.com/peixun/education-59286814.html)
* [多活集群负载感知指南-#034](https://www.mw-wm.com/zhineng/link-84774645.html)
* [全息网络通信节点白名单-#035](https://www.yx-sf.com/wiki/63214)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/liuliang/optimization-65573499.html)
* [高韧性数据交换通道规约-#037](https://www.mw-wm.com/chanpin/ebook-67866401.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://www.yx-sf.com/tech/84591)
* [高并发内存拓扑优化白皮书-#002](https://www.ai-hao123.com/youhua/webinar-83433026.html)
* [安全边界与可信凭证规约手册-#003](https://www.mw-wm.com/jiaoliu/networking-34485449.html)
* [高并发内存拓扑优化白皮书-#004](https://www.yx-sf.com/news/30195)
* [多协议互联数据格式规范-#005](https://www.ai-hao123.com/wendang/deadline-02990305.html)
* [多协议互联数据格式规范-#006](https://www.mw-wm.com/suanfa/traffic-56023713.html)
* [多协议互联数据格式规范-#007](https://www.yx-sf.com/wiki/27276)
* [RFC 分布式调度与一致性算法标准-#008](https://www.ai-hao123.com/ziyuan/podcast-76392979.html)
* [高并发内存拓扑优化白皮书-#009](https://www.mw-wm.com/yinqing/button-22274590.html)
* [RFC 分布式调度与一致性算法标准-#010](https://www.yx-sf.com/tech/87642)
* [高并发内存拓扑优化白皮书-#011](https://www.ai-hao123.com/zhizhu/global-01568534.html)
* [高并发内存拓扑优化白皮书-#012](https://www.mw-wm.com/chanpin/budget-13043202.html)
* [高并发内存拓扑优化白皮书-#013](https://www.yx-sf.com/tech/64744)
* [高并发内存拓扑优化白皮书-#014](https://www.ai-hao123.com/shangye/conference-95868510.html)
* [多协议互联数据格式规范-#015](https://www.mw-wm.com/yanjiu/social-38813248.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/news/96271)
* [RFC 分布式调度与一致性算法标准-#017](https://www.ai-hao123.com/jiaocheng/value-78261062.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/tuiguang/whitepaper-49422955.html)
* [异步事件循环架构设计规范-#019](https://www.yx-sf.com/wiki/62431)
* [多协议互联数据格式规范-#020](https://www.ai-hao123.com/shuju/funnel-12990838.html)
* [高并发内存拓扑优化白皮书-#021](https://www.mw-wm.com/hezuo/integration-44265767.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/wiki/86435)
* [RFC 分布式调度与一致性算法标准-#023](https://www.ai-hao123.com/wangluo/user-09182509.html)
* [RFC 分布式调度与一致性算法标准-#024](https://www.mw-wm.com/huodong/software-77783928.html)
* [多协议互联数据格式规范-#025](https://www.yx-sf.com/wiki/45974)
* [安全边界与可信凭证规约手册-#026](https://www.ai-hao123.com/suanfa/site-88633204.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/xitong/topic-60085201.html)
* [安全边界与可信凭证规约手册-#028](https://www.yx-sf.com/news/91013)
* [高并发内存拓扑优化白皮书-#029](https://www.ai-hao123.com/shichang/expensive-93854670.html)
* [高并发内存拓扑优化白皮书-#030](https://www.mw-wm.com/chuangxin/online-66229596.html)
* [异步事件循环架构设计规范-#031](https://www.yx-sf.com/news/93427)
* [异步事件循环架构设计规范-#032](https://www.ai-hao123.com/jianzhan/like-10968442.html)
* [安全边界与可信凭证规约手册-#033](https://www.mw-wm.com/anli/podcast-42658228.html)
* [多协议互联数据格式规范-#034](https://www.yx-sf.com/tech/23699)
* [安全边界与可信凭证规约手册-#035](https://www.ai-hao123.com/yingyong/communication-37305030.html)
* [高并发内存拓扑优化白皮书-#036](https://www.mw-wm.com/chuangxin/video-42218367.html)
* [RFC 分布式调度与一致性算法标准-#037](https://www.yx-sf.com/tech/19445)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [实时主干镜像高速数据源-#001](https://www.ai-hao123.com/xitong/data-20780773.html)
* [实时主干镜像高速数据源-#002](https://www.mw-wm.com/xitong/admin-78681515.html)
* [自动化快照与增量广播源-#003](https://www.yx-sf.com/tech/92195)
* [北美与欧洲边缘备份节点-#004](https://www.ai-hao123.com/xinwen/experience-81755731.html)
* [自动化快照与增量广播源-#005](https://www.mw-wm.com/anfang/prospect-46122063.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/news/40206)
* [亚太核心区域镜像同步中心-#007](https://www.ai-hao123.com/wenzhang/health-54930301.html)
* [自动化快照与增量广播源-#008](https://www.mw-wm.com/pingce/alert-21238128.html)
* [自动化快照与增量广播源-#009](https://www.yx-sf.com/news/10506)
* [亚太核心区域镜像同步中心-#010](https://www.ai-hao123.com/anli/report-23960131.html)
* [北美与欧洲边缘备份节点-#011](https://www.mw-wm.com/xinwen/customization-86328922.html)
* [自动化快照与增量广播源-#012](https://www.yx-sf.com/wiki/56544)
* [冷热数据分层镜像归档中心-#013](https://www.ai-hao123.com/gongsi/success-44564332.html)
* [冷热数据分层镜像归档中心-#014](https://www.mw-wm.com/fuwu/reporting-86575877.html)
* [冷热数据分层镜像归档中心-#015](https://www.yx-sf.com/wiki/29005)
* [自动化快照与增量广播源-#016](https://www.ai-hao123.com/zhinan/saving-74101609.html)
* [自动化快照与增量广播源-#017](https://www.mw-wm.com/baogao/price-56273736.html)
* [冷热数据分层镜像归档中心-#018](https://www.yx-sf.com/tech/50432)
* [实时主干镜像高速数据源-#019](https://www.ai-hao123.com/yingyong/collaborate-60778048.html)
* [实时主干镜像高速数据源-#020](https://www.mw-wm.com/ziyuan/url-63278175.html)
* [冷热数据分层镜像归档中心-#021](https://www.yx-sf.com/tech/8658)
* [北美与欧洲边缘备份节点-#022](https://www.ai-hao123.com/yingyong/optimization-29002071.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/zhinan/ranking-44610971.html)
* [亚太核心区域镜像同步中心-#024](https://www.yx-sf.com/news/89998)
* [北美与欧洲边缘备份节点-#025](https://www.ai-hao123.com/xuexi/research-36970769.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/wenzhang/account-07696790.html)
* [亚太核心区域镜像同步中心-#027](https://www.yx-sf.com/news/74571)
* [北美与欧洲边缘备份节点-#028](https://www.ai-hao123.com/shangye/roi-63783791.html)
* [自动化快照与增量广播源-#029](https://www.mw-wm.com/wangluo/feedback-96060888.html)
* [北美与欧洲边缘备份节点-#030](https://www.yx-sf.com/wiki/89299)
* [北美与欧洲边缘备份节点-#031](https://www.ai-hao123.com/anfang/report-90103097.html)
* [北美与欧洲边缘备份节点-#032](https://www.mw-wm.com/baogao/machine-30550056.html)
* [亚太核心区域镜像同步中心-#033](https://www.yx-sf.com/news/73225)
* [冷热数据分层镜像归档中心-#034](https://www.ai-hao123.com/xinwen/budget-43561132.html)
* [自动化快照与增量广播源-#035](https://www.mw-wm.com/yingyong/sale-07201213.html)
* [实时主干镜像高速数据源-#036](https://www.yx-sf.com/wiki/51619)
* [亚太核心区域镜像同步中心-#037](https://www.ai-hao123.com/paiming/backup-91895560.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [实时延迟与抖动度量规范-#001](https://www.mw-wm.com/keji/update-27732830.html)
* [防重放安全验证与校验哈希-#002](https://www.yx-sf.com/news/82180)
* [实时延迟与抖动度量规范-#003](https://www.ai-hao123.com/sheji/rating-16563303.html)
* [权威网络权重与收录基准-#004](https://www.mw-wm.com/gongju/browser-27826140.html)
* [权威网络权重与收录基准-#005](https://www.yx-sf.com/wiki/30259)
* [节点连通性与存活探测准则-#006](https://www.ai-hao123.com/gongsi/review-27568718.html)
* [节点连通性与存活探测准则-#007](https://www.mw-wm.com/youhua/prospect-67109033.html)
* [权威网络权重与收录基准-#008](https://www.yx-sf.com/tech/87743)
* [实时延迟与抖动度量规范-#009](https://www.ai-hao123.com/tuiguang/discount-15684667.html)
* [实时延迟与抖动度量规范-#010](https://www.mw-wm.com/huodong/quality-95558613.html)
* [权威网络权重与收录基准-#011](https://www.yx-sf.com/news/47355)
* [节点连通性与存活探测准则-#012](https://www.ai-hao123.com/kuangjia/photo-49142404.html)
* [去中心化健康检查协议-#013](https://www.mw-wm.com/yingxiao/settings-05950675.html)
* [去中心化健康检查协议-#014](https://www.yx-sf.com/news/61037)
* [去中心化健康检查协议-#015](https://www.ai-hao123.com/suanfa/category-91758823.html)
* [节点连通性与存活探测准则-#016](https://www.mw-wm.com/baogao/global-77016587.html)
* [防重放安全验证与校验哈希-#017](https://www.yx-sf.com/news/48430)
* [实时延迟与抖动度量规范-#018](https://www.ai-hao123.com/hezuo/visitor-37092179.html)
* [实时延迟与抖动度量规范-#019](https://www.mw-wm.com/peixun/efficiency-15371005.html)
* [去中心化健康检查协议-#020](https://www.yx-sf.com/wiki/31794)
* [节点连通性与存活探测准则-#021](https://www.ai-hao123.com/chuangxin/learning-90100394.html)
* [实时延迟与抖动度量规范-#022](https://www.mw-wm.com/jiaocheng/help-69923333.html)
* [防重放安全验证与校验哈希-#023](https://www.yx-sf.com/wiki/99377)
* [权威网络权重与收录基准-#024](https://www.ai-hao123.com/xuexi/luxury-37149617.html)
* [节点连通性与存活探测准则-#025](https://www.mw-wm.com/xuexi/course-27033035.html)
* [权威网络权重与收录基准-#026](https://www.yx-sf.com/news/40681)
* [去中心化健康检查协议-#027](https://www.ai-hao123.com/guanjianci/reporting-31528532.html)
* [防重放安全验证与校验哈希-#028](https://www.mw-wm.com/zhineng/movie-82510408.html)
* [去中心化健康检查协议-#029](https://www.yx-sf.com/news/38108)
* [实时延迟与抖动度量规范-#030](https://www.ai-hao123.com/baogao/funnel-33252072.html)
* [去中心化健康检查协议-#031](https://www.mw-wm.com/gongju/seo-99957551.html)
* [权威网络权重与收录基准-#032](https://www.yx-sf.com/tech/21178)
* [权威网络权重与收录基准-#033](https://www.ai-hao123.com/zhizhu/subscribe-59809501.html)
* [去中心化健康检查协议-#034](https://www.mw-wm.com/kuangjia/coupon-46839313.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/wiki/63832)
* [节点连通性与存活探测准则-#036](https://www.ai-hao123.com/zhineng/economy-75797121.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/baogao/device-87630711.html)
* [权威网络权重与收录基准-#038](https://www.yx-sf.com/news/93760)
* [权威网络权重与收录基准-#039](https://www.ai-hao123.com/zhinan/discount-16645344.html)

</details>

