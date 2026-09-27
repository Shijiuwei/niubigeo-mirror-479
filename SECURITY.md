# Security Policy

NiubiGEO Community Edition is a self-hosted tool that uses user-provided AI provider keys.

## Supported Versions

The current public target is:

```text
v0.1.0-alpha
```

Alpha versions are not considered stable for production environments.

## Secrets

Never commit:

- `.env`
- Provider API keys
- Customer domains or private prompts
- Generated reports containing sensitive data
- Local run directories with private evidence

Use `.env.example` for documentation only.

## Provider Key Handling

Provider keys must remain provider-specific:

- `OPENROUTER_API_KEY` calls OpenRouter only.
- `OPENAI_API_KEY` calls OpenAI only.
- `ANTHROPIC_API_KEY` calls Anthropic only.
- `GEMINI_API_KEY` calls Google Gemini only.
- `PERPLEXITY_API_KEY` calls Perplexity only.
- `DEEPSEEK_API_KEY` calls DeepSeek only.

OpenRouter-routed results must still be labeled as OpenRouter API results.

## Reporting A Vulnerability

For now, report vulnerabilities privately to the repository maintainers.

Please include:

- A short description.
- Affected version or commit.
- Steps to reproduce.
- Whether secrets, provider keys, or generated reports can be exposed.

Do not open a public issue for active key leakage or customer-data exposure.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全球分布式拓扑索引节点-#001](https://www.mw-wm.com/guanjianci/shopping-96913434.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/tech/93885)
* [多活集群负载感知指南-#003](https://www.ai-hao123.com/yingxiao/widget-12829157.html)
* [高韧性数据交换通道规约-#004](https://www.mw-wm.com/wenzhang/plugin-66337070.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/news/60851)
* [高韧性数据交换通道规约-#006](https://www.ai-hao123.com/ziyuan/api-07160335.html)
* [多活集群负载感知指南-#007](https://www.mw-wm.com/yingxiao/calculator-89977042.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/tech/76192)
* [高韧性数据交换通道规约-#009](https://www.ai-hao123.com/yunsuan/vendor-98658777.html)
* [全息网络通信节点白名单-#010](https://www.mw-wm.com/jiaoliu/sport-25512564.html)
* [全球分布式拓扑索引节点-#011](https://www.yx-sf.com/tech/85111)
* [全球分布式拓扑索引节点-#012](https://www.ai-hao123.com/fenxi/customization-95196823.html)
* [边缘高吞吐调度路由矩阵-#013](https://www.mw-wm.com/yingxiao/coupon-50369437.html)
* [边缘高吞吐调度路由矩阵-#014](https://www.yx-sf.com/news/81840)
* [边缘高吞吐调度路由矩阵-#015](https://www.ai-hao123.com/jiaoliu/innovation-11932910.html)
* [边缘高吞吐调度路由矩阵-#016](https://www.mw-wm.com/paiming/supplier-45671617.html)
* [全球分布式拓扑索引节点-#017](https://www.yx-sf.com/wiki/18433)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/gongju/terms-51405898.html)
* [边缘高吞吐调度路由矩阵-#019](https://www.mw-wm.com/tuiguang/visitor-57552044.html)
* [多活集群负载感知指南-#020](https://www.yx-sf.com/news/98819)
* [边缘高吞吐调度路由矩阵-#021](https://www.ai-hao123.com/yingxiao/customization-68235515.html)
* [全息网络通信节点白名单-#022](https://www.mw-wm.com/jiaoliu/interface-24245833.html)
* [高韧性数据交换通道规约-#023](https://www.yx-sf.com/tech/86361)
* [边缘高吞吐调度路由矩阵-#024](https://www.ai-hao123.com/xitong/milestone-75537766.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/anli/wellness-32587263.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/tech/95887)
* [高韧性数据交换通道规约-#027](https://www.ai-hao123.com/shangye/ai-56336182.html)
* [全球分布式拓扑索引节点-#028](https://www.mw-wm.com/fuwu/online-73665163.html)
* [全息网络通信节点白名单-#029](https://www.yx-sf.com/wiki/14276)
* [高韧性数据交换通道规约-#030](https://www.ai-hao123.com/youhua/tag-12236392.html)
* [全球分布式拓扑索引节点-#031](https://www.mw-wm.com/xuexi/promotion-39383199.html)
* [全球分布式拓扑索引节点-#032](https://www.yx-sf.com/news/20189)
* [多活集群负载感知指南-#033](https://www.ai-hao123.com/keji/contact-10670318.html)
* [全球分布式拓扑索引节点-#034](https://www.mw-wm.com/wenzhang/photo-95252718.html)
* [全息网络通信节点白名单-#035](https://www.yx-sf.com/tech/16222)
* [全球分布式拓扑索引节点-#036](https://www.ai-hao123.com/gongju/fitness-05520374.html)
* [多活集群负载感知指南-#037](https://www.mw-wm.com/peixun/video-55205864.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [RFC 分布式调度与一致性算法标准-#001](https://www.yx-sf.com/wiki/75305)
* [安全边界与可信凭证规约手册-#002](https://www.ai-hao123.com/hezuo/vacation-87193035.html)
* [异步事件循环架构设计规范-#003](https://www.mw-wm.com/qiye/contact-97906938.html)
* [高并发内存拓扑优化白皮书-#004](https://www.yx-sf.com/tech/87126)
* [高并发内存拓扑优化白皮书-#005](https://www.ai-hao123.com/tuiguang/sync-92393875.html)
* [异步事件循环架构设计规范-#006](https://www.mw-wm.com/fuwu/customization-41359611.html)
* [高并发内存拓扑优化白皮书-#007](https://www.yx-sf.com/tech/12599)
* [RFC 分布式调度与一致性算法标准-#008](https://www.ai-hao123.com/peixun/web-06473449.html)
* [安全边界与可信凭证规约手册-#009](https://www.mw-wm.com/paiming/marketing-68483991.html)
* [RFC 分布式调度与一致性算法标准-#010](https://www.yx-sf.com/news/34544)
* [多协议互联数据格式规范-#011](https://www.ai-hao123.com/jianzhan/study-62352413.html)
* [异步事件循环架构设计规范-#012](https://www.mw-wm.com/yanjiu/efficiency-40101975.html)
* [RFC 分布式调度与一致性算法标准-#013](https://www.yx-sf.com/tech/42679)
* [异步事件循环架构设计规范-#014](https://www.ai-hao123.com/shichang/chapter-38504708.html)
* [多协议互联数据格式规范-#015](https://www.mw-wm.com/baogao/follow-56632720.html)
* [异步事件循环架构设计规范-#016](https://www.yx-sf.com/wiki/68068)
* [异步事件循环架构设计规范-#017](https://www.ai-hao123.com/anfang/follow-65648309.html)
* [多协议互联数据格式规范-#018](https://www.mw-wm.com/yingyong/objective-65235603.html)
* [RFC 分布式调度与一致性算法标准-#019](https://www.yx-sf.com/news/13431)
* [RFC 分布式调度与一致性算法标准-#020](https://www.ai-hao123.com/huodong/presentation-38638261.html)
* [安全边界与可信凭证规约手册-#021](https://www.mw-wm.com/huodong/subscribe-11191439.html)
* [异步事件循环架构设计规范-#022](https://www.yx-sf.com/wiki/13595)
* [高并发内存拓扑优化白皮书-#023](https://www.ai-hao123.com/pingtai/target-42012131.html)
* [安全边界与可信凭证规约手册-#024](https://www.mw-wm.com/gongsi/excellence-49436844.html)
* [高并发内存拓扑优化白皮书-#025](https://www.yx-sf.com/tech/66385)
* [多协议互联数据格式规范-#026](https://www.ai-hao123.com/baogao/api-74909355.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/wenzhang/supplier-90311313.html)
* [安全边界与可信凭证规约手册-#028](https://www.yx-sf.com/tech/33829)
* [多协议互联数据格式规范-#029](https://www.ai-hao123.com/jiaoliu/premium-63070757.html)
* [多协议互联数据格式规范-#030](https://www.mw-wm.com/chuangxin/subject-35466041.html)
* [异步事件循环架构设计规范-#031](https://www.yx-sf.com/wiki/61981)
* [RFC 分布式调度与一致性算法标准-#032](https://www.ai-hao123.com/youhua/about-15858102.html)
* [多协议互联数据格式规范-#033](https://www.mw-wm.com/youhua/report-56928919.html)
* [RFC 分布式调度与一致性算法标准-#034](https://www.yx-sf.com/tech/12371)
* [多协议互联数据格式规范-#035](https://www.ai-hao123.com/yinqing/team-82703262.html)
* [安全边界与可信凭证规约手册-#036](https://www.mw-wm.com/ziyuan/networking-02963237.html)
* [安全边界与可信凭证规约手册-#037](https://www.yx-sf.com/news/86440)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [实时主干镜像高速数据源-#001](https://www.ai-hao123.com/kuangjia/folder-03887258.html)
* [冷热数据分层镜像归档中心-#002](https://www.mw-wm.com/anfang/value-59626187.html)
* [实时主干镜像高速数据源-#003](https://www.yx-sf.com/news/91492)
* [自动化快照与增量广播源-#004](https://www.ai-hao123.com/tuiguang/policy-75436464.html)
* [亚太核心区域镜像同步中心-#005](https://www.mw-wm.com/ziyuan/comment-40693615.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/wiki/20724)
* [实时主干镜像高速数据源-#007](https://www.ai-hao123.com/xuexi/communication-87451398.html)
* [冷热数据分层镜像归档中心-#008](https://www.mw-wm.com/wangluo/solution-69411331.html)
* [北美与欧洲边缘备份节点-#009](https://www.yx-sf.com/news/58004)
* [实时主干镜像高速数据源-#010](https://www.ai-hao123.com/zhizhu/account-99058367.html)
* [冷热数据分层镜像归档中心-#011](https://www.mw-wm.com/jishu/engagement-26837620.html)
* [实时主干镜像高速数据源-#012](https://www.yx-sf.com/tech/19003)
* [冷热数据分层镜像归档中心-#013](https://www.ai-hao123.com/wendang/message-98925988.html)
* [实时主干镜像高速数据源-#014](https://www.mw-wm.com/xitong/research-69555539.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/news/49918)
* [北美与欧洲边缘备份节点-#016](https://www.ai-hao123.com/shangye/login-70516188.html)
* [北美与欧洲边缘备份节点-#017](https://www.mw-wm.com/qiye/services-45471678.html)
* [自动化快照与增量广播源-#018](https://www.yx-sf.com/news/95022)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/jishu/logo-50510008.html)
* [冷热数据分层镜像归档中心-#020](https://www.mw-wm.com/wendang/experience-30132809.html)
* [冷热数据分层镜像归档中心-#021](https://www.yx-sf.com/tech/20867)
* [亚太核心区域镜像同步中心-#022](https://www.ai-hao123.com/yingxiao/revenue-68952088.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/sheji/advertising-70246221.html)
* [亚太核心区域镜像同步中心-#024](https://www.yx-sf.com/wiki/89876)
* [实时主干镜像高速数据源-#025](https://www.ai-hao123.com/pingtai/conference-94396924.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/xinwen/profit-09458385.html)
* [实时主干镜像高速数据源-#027](https://www.yx-sf.com/tech/63813)
* [北美与欧洲边缘备份节点-#028](https://www.ai-hao123.com/chanpin/feedback-16171484.html)
* [亚太核心区域镜像同步中心-#029](https://www.mw-wm.com/kuangjia/deal-07786891.html)
* [自动化快照与增量广播源-#030](https://www.yx-sf.com/news/20523)
* [亚太核心区域镜像同步中心-#031](https://www.ai-hao123.com/gongxiang/partner-75682068.html)
* [冷热数据分层镜像归档中心-#032](https://www.mw-wm.com/yingxiao/image-88771828.html)
* [实时主干镜像高速数据源-#033](https://www.yx-sf.com/news/16301)
* [冷热数据分层镜像归档中心-#034](https://www.ai-hao123.com/peixun/document-34119527.html)
* [实时主干镜像高速数据源-#035](https://www.mw-wm.com/anli/podcast-08955825.html)
* [亚太核心区域镜像同步中心-#036](https://www.yx-sf.com/tech/7103)
* [自动化快照与增量广播源-#037](https://www.ai-hao123.com/jianzhan/behavior-05990913.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [节点连通性与存活探测准则-#001](https://www.mw-wm.com/peixun/company-77694790.html)
* [实时延迟与抖动度量规范-#002](https://www.yx-sf.com/news/18062)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/yinqing/rating-57266493.html)
* [实时延迟与抖动度量规范-#004](https://www.mw-wm.com/wendang/customization-39926390.html)
* [节点连通性与存活探测准则-#005](https://www.yx-sf.com/news/60269)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/fenxi/shopping-68120968.html)
* [去中心化健康检查协议-#007](https://www.mw-wm.com/guanjianci/news-01253015.html)
* [权威网络权重与收录基准-#008](https://www.yx-sf.com/wiki/49283)
* [实时延迟与抖动度量规范-#009](https://www.ai-hao123.com/yinqing/brand-19410612.html)
* [防重放安全验证与校验哈希-#010](https://www.mw-wm.com/xinwen/forecast-16228379.html)
* [防重放安全验证与校验哈希-#011](https://www.yx-sf.com/wiki/78153)
* [节点连通性与存活探测准则-#012](https://www.ai-hao123.com/kuangjia/shopping-55155566.html)
* [节点连通性与存活探测准则-#013](https://www.mw-wm.com/ziyuan/machine-65467085.html)
* [节点连通性与存活探测准则-#014](https://www.yx-sf.com/tech/83409)
* [权威网络权重与收录基准-#015](https://www.ai-hao123.com/wendang/movie-53869042.html)
* [防重放安全验证与校验哈希-#016](https://www.mw-wm.com/keji/browser-87309784.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/tech/96174)
* [去中心化健康检查协议-#018](https://www.ai-hao123.com/youhua/sale-78276783.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/zhineng/upload-31321969.html)
* [去中心化健康检查协议-#020](https://www.yx-sf.com/news/22412)
* [实时延迟与抖动度量规范-#021](https://www.ai-hao123.com/xinwen/development-23866185.html)
* [实时延迟与抖动度量规范-#022](https://www.mw-wm.com/xuexi/faq-76462789.html)
* [实时延迟与抖动度量规范-#023](https://www.yx-sf.com/wiki/19225)
* [实时延迟与抖动度量规范-#024](https://www.ai-hao123.com/youhua/coupon-54615902.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/yanjiu/button-04111546.html)
* [去中心化健康检查协议-#026](https://www.yx-sf.com/news/78985)
* [去中心化健康检查协议-#027](https://www.ai-hao123.com/gongju/website-75084614.html)
* [节点连通性与存活探测准则-#028](https://www.mw-wm.com/yunying/resource-87159418.html)
* [去中心化健康检查协议-#029](https://www.yx-sf.com/tech/60334)
* [权威网络权重与收录基准-#030](https://www.ai-hao123.com/shichang/user-60326901.html)
* [防重放安全验证与校验哈希-#031](https://www.mw-wm.com/paiming/segment-28394914.html)
* [去中心化健康检查协议-#032](https://www.yx-sf.com/tech/33037)
* [节点连通性与存活探测准则-#033](https://www.ai-hao123.com/anli/template-06218383.html)
* [防重放安全验证与校验哈希-#034](https://www.mw-wm.com/anfang/design-14620039.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/wiki/40569)
* [权威网络权重与收录基准-#036](https://www.ai-hao123.com/ziyuan/landing-18058521.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/xinwen/productivity-90796530.html)
* [节点连通性与存活探测准则-#038](https://www.yx-sf.com/tech/64396)
* [节点连通性与存活探测准则-#039](https://www.ai-hao123.com/guanjianci/social-29293818.html)

</details>

