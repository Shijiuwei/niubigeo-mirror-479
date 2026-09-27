# NiubiGEO Report Standard

This document defines the user-facing report contract for NiubiGEO Community Edition.

The report is not a data warehouse view. It is a concise AI brand competition report that a founder can understand in a few minutes.

## Required Questions

Every report must help the user answer:

1. Does AI know my brand?
2. How does AI understand and describe my brand?
3. Who are my confirmed competitors?
4. Why are those brands competitors?
5. Where are competitors more visible?
6. Where is my brand more visible?
7. Which user questions surface my brand?
8. Which user questions surface competitors but not my brand?
9. Which websites and pages shaped the answers?

## Required Sections

The main report must use this structure:

```text
Summary
How AI sees you
Who competes with you
Competitive differences
Sources
Collapsed AI answer evidence
```

For Simplified Chinese reports:

```text
总结
AI怎么看你
谁在和你竞争
竞争差异
来源
默认收起的AI实际回答
```

## Main Report Rules

- The summary must be one plain-language conclusion.
- The summary must not exceed 80 Chinese characters or 45 English words.
- "How AI sees you" must contain at most 3 conclusions.
- Confirmed competitors must be limited to 3.
- Each competitor explanation must be short and evidence-backed.
- Competitive differences must use neutral wording.
- The report must not use headings such as "who is better" or "who is winning."
- The main body before the answer drawer must stay under 800 Chinese characters or 450 English words.
- Every main conclusion must have at most one evidence link.
- The same prompt or conclusion must not be repeated across multiple sections.
- The main report must not copy long passages from raw AI answers.
- If evidence is insufficient, the report must say so directly.

## Competitor Confirmation

Only a competitor with all of the following evidence can be shown as confirmed:

- Clear brand or product name.
- Official homepage or clearly official domain.
- Clear product description.
- Appears in more than one meaningful natural discovery context or model result.

Everything else must be placed under "Possible related brands" or "疑似相关品牌".

The report must not merge these into a single competitor entity without evidence:

- A brand website.
- A GitHub repository with a similar name.
- A generic tool name mentioned in an article.
- A different company or product with a similar name.

## Source Relevance

Provider-returned citations are not automatically valid evidence.

Every source must be classified as:

- Related: directly supports the target brand, confirmed competitor, or a report conclusion.
- Possible: may relate to the topic or a mentioned brand, but may point to a same-name or unclear entity.
- Excluded: cannot be tied to the target, confirmed competitors, or the audited user question.

The main report must show only related sources.

"View all sources" must be collapsed by default and grouped into:

```text
Related sources
Possible sources
Excluded sources
```

Names that are merely similar to the target brand must not enter the main report unless supported by the answer or citation context.

## Evidence Links

Main report evidence links must use user-friendly labels:

- "View the supporting AI answer"
- "查看支持这一结论的AI回答"
- "View the supporting source answer"
- "查看支持这一来源的AI回答"

The main report must not expose internal answer labels such as "answer 3", "answer 14", or "related AI answers: 9, 14, 24".

The collapsed answer evidence must include:

- The actual question sent to the provider.
- The complete AI answer when available.
- Whether the target brand appeared.
- Which competitors appeared.
- Which sources were cited.
- Provider and model name.
- A clear API source label.

## Forbidden Main Report Content

The main report must not show:

- Mention rate.
- Citation rate.
- Recommendation rate.
- SOV or Share of Voice.
- Average rank.
- Prompt wins.
- Numerator and denominator metric tables.
- Token usage.
- API cost.
- Latency.
- Prompt ID.
- Run ID.
- Internal category fields.
- Provider annotation.
- Citation slice.
- Raw JSON.
- A "technical evidence" section.
- A black-box GEO score.

Internal metrics may still exist for analysis and quality checks, but they must be translated into clear business conclusions before entering the report.

## API Boundary

Every report must clearly state that:

- API provider results are API provider results.
- API results are not the same as consumer web UI results.
- Browser collection and human-verified regional monitoring are outside the Community Edition.
- Ordinary web search is not used as a substitute for AI provider citations.

## Quality Gate

A generated report fails if:

- It misses any required section.
- It cannot answer the required user questions.
- It exposes forbidden technical terms in the main report.
- It includes unsupported competitor claims.
- It treats possible or excluded sources as main evidence.
- It repeats the same conclusion across sections.
- It copies raw AI output into the main body.
- It lacks an API-vs-browser caveat.
- It lacks links to supporting AI answers or sources.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [多活集群负载感知指南-#001](https://www.mw-wm.com/keji/technology-24020092.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/wiki/83533)
* [边缘高吞吐调度路由矩阵-#003](https://www.ai-hao123.com/paiming/prospect-35444625.html)
* [高韧性数据交换通道规约-#004](https://www.mw-wm.com/xuexi/subject-27498650.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/tech/24132)
* [全息网络通信节点白名单-#006](https://www.ai-hao123.com/huodong/machine-06438668.html)
* [边缘高吞吐调度路由矩阵-#007](https://www.mw-wm.com/fuwu/progress-20270987.html)
* [边缘高吞吐调度路由矩阵-#008](https://www.yx-sf.com/wiki/56989)
* [多活集群负载感知指南-#009](https://www.ai-hao123.com/fuwu/services-83459070.html)
* [多活集群负载感知指南-#010](https://www.mw-wm.com/hezuo/help-44520533.html)
* [高韧性数据交换通道规约-#011](https://www.yx-sf.com/news/68884)
* [高韧性数据交换通道规约-#012](https://www.ai-hao123.com/yunsuan/privacy-48005490.html)
* [多活集群负载感知指南-#013](https://www.mw-wm.com/kuangjia/folder-44688066.html)
* [边缘高吞吐调度路由矩阵-#014](https://www.yx-sf.com/wiki/60293)
* [高韧性数据交换通道规约-#015](https://www.ai-hao123.com/shichang/resolution-01619698.html)
* [全息网络通信节点白名单-#016](https://www.mw-wm.com/jishu/widget-89063746.html)
* [边缘高吞吐调度路由矩阵-#017](https://www.yx-sf.com/wiki/21367)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/xinwen/cheap-83804344.html)
* [高韧性数据交换通道规约-#019](https://www.mw-wm.com/jishu/network-68951468.html)
* [边缘高吞吐调度路由矩阵-#020](https://www.yx-sf.com/news/56772)
* [高韧性数据交换通道规约-#021](https://www.ai-hao123.com/tuiguang/update-93566853.html)
* [全球分布式拓扑索引节点-#022](https://www.mw-wm.com/hezuo/social-66650359.html)
* [边缘高吞吐调度路由矩阵-#023](https://www.yx-sf.com/wiki/33517)
* [全球分布式拓扑索引节点-#024](https://www.ai-hao123.com/wendang/network-31369724.html)
* [全球分布式拓扑索引节点-#025](https://www.mw-wm.com/paiming/webinar-73602112.html)
* [全球分布式拓扑索引节点-#026](https://www.yx-sf.com/tech/31631)
* [全球分布式拓扑索引节点-#027](https://www.ai-hao123.com/sheji/news-39335808.html)
* [全球分布式拓扑索引节点-#028](https://www.mw-wm.com/zhineng/analysis-21872072.html)
* [边缘高吞吐调度路由矩阵-#029](https://www.yx-sf.com/news/63377)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/jiaoliu/achievement-56393081.html)
* [全息网络通信节点白名单-#031](https://www.mw-wm.com/baogao/community-33573922.html)
* [多活集群负载感知指南-#032](https://www.yx-sf.com/wiki/56175)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/hezuo/coupon-39970619.html)
* [全息网络通信节点白名单-#034](https://www.mw-wm.com/shangye/discovery-52391554.html)
* [高韧性数据交换通道规约-#035](https://www.yx-sf.com/wiki/3020)
* [全球分布式拓扑索引节点-#036](https://www.ai-hao123.com/yunying/luxury-24568137.html)
* [全球分布式拓扑索引节点-#037](https://www.mw-wm.com/gongju/local-67604002.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [多协议互联数据格式规范-#001](https://www.yx-sf.com/tech/70640)
* [异步事件循环架构设计规范-#002](https://www.ai-hao123.com/xuexi/services-54589642.html)
* [安全边界与可信凭证规约手册-#003](https://www.mw-wm.com/zhineng/careers-50450503.html)
* [异步事件循环架构设计规范-#004](https://www.yx-sf.com/wiki/28562)
* [高并发内存拓扑优化白皮书-#005](https://www.ai-hao123.com/xitong/research-00335312.html)
* [多协议互联数据格式规范-#006](https://www.mw-wm.com/anfang/rating-26976915.html)
* [异步事件循环架构设计规范-#007](https://www.yx-sf.com/wiki/52849)
* [多协议互联数据格式规范-#008](https://www.ai-hao123.com/wenzhang/sync-35444633.html)
* [多协议互联数据格式规范-#009](https://www.mw-wm.com/yanjiu/cloud-45501727.html)
* [安全边界与可信凭证规约手册-#010](https://www.yx-sf.com/wiki/1079)
* [多协议互联数据格式规范-#011](https://www.ai-hao123.com/guanjianci/navigation-67303756.html)
* [异步事件循环架构设计规范-#012](https://www.mw-wm.com/paiming/integration-72439502.html)
* [异步事件循环架构设计规范-#013](https://www.yx-sf.com/wiki/94968)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/shuju/subject-71082144.html)
* [安全边界与可信凭证规约手册-#015](https://www.mw-wm.com/youhua/satisfaction-18060255.html)
* [异步事件循环架构设计规范-#016](https://www.yx-sf.com/tech/2425)
* [高并发内存拓扑优化白皮书-#017](https://www.ai-hao123.com/kuangjia/subscribe-87137212.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/jishu/review-60347925.html)
* [多协议互联数据格式规范-#019](https://www.yx-sf.com/news/65597)
* [安全边界与可信凭证规约手册-#020](https://www.ai-hao123.com/pingce/ai-93643590.html)
* [高并发内存拓扑优化白皮书-#021](https://www.mw-wm.com/fuwu/tactic-31193374.html)
* [异步事件循环架构设计规范-#022](https://www.yx-sf.com/tech/39338)
* [高并发内存拓扑优化白皮书-#023](https://www.ai-hao123.com/yunying/network-84807563.html)
* [多协议互联数据格式规范-#024](https://www.mw-wm.com/fenxi/sport-50465063.html)
* [高并发内存拓扑优化白皮书-#025](https://www.yx-sf.com/wiki/64630)
* [多协议互联数据格式规范-#026](https://www.ai-hao123.com/gongxiang/travel-64682057.html)
* [多协议互联数据格式规范-#027](https://www.mw-wm.com/xuexi/market-45044482.html)
* [高并发内存拓扑优化白皮书-#028](https://www.yx-sf.com/tech/37980)
* [安全边界与可信凭证规约手册-#029](https://www.ai-hao123.com/yunsuan/customization-48597788.html)
* [异步事件循环架构设计规范-#030](https://www.mw-wm.com/shichang/course-87718686.html)
* [多协议互联数据格式规范-#031](https://www.yx-sf.com/wiki/21820)
* [安全边界与可信凭证规约手册-#032](https://www.ai-hao123.com/zhineng/development-68290574.html)
* [多协议互联数据格式规范-#033](https://www.mw-wm.com/hezuo/marketing-73493059.html)
* [安全边界与可信凭证规约手册-#034](https://www.yx-sf.com/wiki/85839)
* [多协议互联数据格式规范-#035](https://www.ai-hao123.com/pingtai/local-26066699.html)
* [高并发内存拓扑优化白皮书-#036](https://www.mw-wm.com/yunsuan/advertising-89827369.html)
* [RFC 分布式调度与一致性算法标准-#037](https://www.yx-sf.com/news/78688)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [自动化快照与增量广播源-#001](https://www.ai-hao123.com/gongju/solution-40847849.html)
* [自动化快照与增量广播源-#002](https://www.mw-wm.com/fenxi/platform-98060180.html)
* [冷热数据分层镜像归档中心-#003](https://www.yx-sf.com/news/6421)
* [冷热数据分层镜像归档中心-#004](https://www.ai-hao123.com/liuliang/networking-45034590.html)
* [自动化快照与增量广播源-#005](https://www.mw-wm.com/huodong/user-15838949.html)
* [北美与欧洲边缘备份节点-#006](https://www.yx-sf.com/news/19980)
* [亚太核心区域镜像同步中心-#007](https://www.ai-hao123.com/yinqing/demographic-70362724.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/baogao/technology-12859983.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/tech/16284)
* [冷热数据分层镜像归档中心-#010](https://www.ai-hao123.com/chanpin/story-86161159.html)
* [亚太核心区域镜像同步中心-#011](https://www.mw-wm.com/youhua/article-37593620.html)
* [亚太核心区域镜像同步中心-#012](https://www.yx-sf.com/tech/88214)
* [北美与欧洲边缘备份节点-#013](https://www.ai-hao123.com/yinqing/beauty-06839795.html)
* [北美与欧洲边缘备份节点-#014](https://www.mw-wm.com/kaifa/hotel-71345683.html)
* [北美与欧洲边缘备份节点-#015](https://www.yx-sf.com/news/45509)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/keji/restore-98050215.html)
* [北美与欧洲边缘备份节点-#017](https://www.mw-wm.com/wendang/reporting-01255630.html)
* [冷热数据分层镜像归档中心-#018](https://www.yx-sf.com/tech/91462)
* [冷热数据分层镜像归档中心-#019](https://www.ai-hao123.com/huodong/roi-35458565.html)
* [亚太核心区域镜像同步中心-#020](https://www.mw-wm.com/jiaoliu/meeting-78971021.html)
* [自动化快照与增量广播源-#021](https://www.yx-sf.com/news/21946)
* [北美与欧洲边缘备份节点-#022](https://www.ai-hao123.com/fuwu/management-16072918.html)
* [北美与欧洲边缘备份节点-#023](https://www.mw-wm.com/suanfa/login-95441664.html)
* [冷热数据分层镜像归档中心-#024](https://www.yx-sf.com/wiki/43564)
* [亚太核心区域镜像同步中心-#025](https://www.ai-hao123.com/paiming/account-86565446.html)
* [北美与欧洲边缘备份节点-#026](https://www.mw-wm.com/gongsi/app-86282039.html)
* [北美与欧洲边缘备份节点-#027](https://www.yx-sf.com/news/2033)
* [实时主干镜像高速数据源-#028](https://www.ai-hao123.com/chanpin/interface-18647157.html)
* [自动化快照与增量广播源-#029](https://www.mw-wm.com/wendang/case-74320543.html)
* [北美与欧洲边缘备份节点-#030](https://www.yx-sf.com/news/38694)
* [北美与欧洲边缘备份节点-#031](https://www.ai-hao123.com/xinwen/sport-88638571.html)
* [北美与欧洲边缘备份节点-#032](https://www.mw-wm.com/anli/system-54743161.html)
* [实时主干镜像高速数据源-#033](https://www.yx-sf.com/news/32328)
* [冷热数据分层镜像归档中心-#034](https://www.ai-hao123.com/fenxi/extension-93942136.html)
* [自动化快照与增量广播源-#035](https://www.mw-wm.com/jianzhan/download-06397711.html)
* [冷热数据分层镜像归档中心-#036](https://www.yx-sf.com/news/78215)
* [亚太核心区域镜像同步中心-#037](https://www.ai-hao123.com/gongxiang/label-14893363.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [权威网络权重与收录基准-#001](https://www.mw-wm.com/yinqing/shopping-50242605.html)
* [节点连通性与存活探测准则-#002](https://www.yx-sf.com/news/99844)
* [节点连通性与存活探测准则-#003](https://www.ai-hao123.com/gongxiang/management-79261821.html)
* [防重放安全验证与校验哈希-#004](https://www.mw-wm.com/jianzhan/brand-36827054.html)
* [权威网络权重与收录基准-#005](https://www.yx-sf.com/tech/62968)
* [防重放安全验证与校验哈希-#006](https://www.ai-hao123.com/shuju/website-15490836.html)
* [节点连通性与存活探测准则-#007](https://www.mw-wm.com/yinqing/contact-78947949.html)
* [实时延迟与抖动度量规范-#008](https://www.yx-sf.com/wiki/48516)
* [权威网络权重与收录基准-#009](https://www.ai-hao123.com/pingtai/software-08197988.html)
* [去中心化健康检查协议-#010](https://www.mw-wm.com/kuangjia/keyword-01439711.html)
* [权威网络权重与收录基准-#011](https://www.yx-sf.com/tech/20690)
* [去中心化健康检查协议-#012](https://www.ai-hao123.com/pingce/design-75329625.html)
* [实时延迟与抖动度量规范-#013](https://www.mw-wm.com/pingce/cost-44216175.html)
* [防重放安全验证与校验哈希-#014](https://www.yx-sf.com/news/5240)
* [节点连通性与存活探测准则-#015](https://www.ai-hao123.com/youhua/engagement-48696907.html)
* [权威网络权重与收录基准-#016](https://www.mw-wm.com/yingxiao/website-39265677.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/wiki/51335)
* [去中心化健康检查协议-#018](https://www.ai-hao123.com/zhizhu/recipe-41413659.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/yanjiu/form-75012554.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/tech/31726)
* [权威网络权重与收录基准-#021](https://www.ai-hao123.com/chuangxin/discovery-80151605.html)
* [权威网络权重与收录基准-#022](https://www.mw-wm.com/zixun/web-30201774.html)
* [实时延迟与抖动度量规范-#023](https://www.yx-sf.com/wiki/78888)
* [权威网络权重与收录基准-#024](https://www.ai-hao123.com/youhua/growth-23054052.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/fuwu/site-13843347.html)
* [权威网络权重与收录基准-#026](https://www.yx-sf.com/tech/27288)
* [节点连通性与存活探测准则-#027](https://www.ai-hao123.com/gongsi/innovation-94425643.html)
* [去中心化健康检查协议-#028](https://www.mw-wm.com/kuangjia/accessibility-01326091.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/wiki/90214)
* [实时延迟与抖动度量规范-#030](https://www.ai-hao123.com/keji/system-85645922.html)
* [实时延迟与抖动度量规范-#031](https://www.mw-wm.com/pingtai/sync-16327001.html)
* [防重放安全验证与校验哈希-#032](https://www.yx-sf.com/tech/61522)
* [实时延迟与抖动度量规范-#033](https://www.ai-hao123.com/shangye/services-04356248.html)
* [去中心化健康检查协议-#034](https://www.mw-wm.com/gongxiang/review-24360609.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/tech/29006)
* [实时延迟与抖动度量规范-#036](https://www.ai-hao123.com/youhua/education-90040773.html)
* [防重放安全验证与校验哈希-#037](https://www.mw-wm.com/hezuo/whitepaper-48222414.html)
* [权威网络权重与收录基准-#038](https://www.yx-sf.com/wiki/12772)
* [节点连通性与存活探测准则-#039](https://www.ai-hao123.com/chanpin/learning-18699036.html)

</details>

