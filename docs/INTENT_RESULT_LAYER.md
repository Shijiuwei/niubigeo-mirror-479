# Intent Result Layer

NiubiGEO's domain audit flow stays unchanged:

```text
domain
-> generated or confirmed questions
-> Provider execution
-> AI answer and citations
```

The Intent Result Layer runs after each completed Provider answer:

```text
PromptRun.result
-> Intent Analyzer
-> Task Decomposer
-> Answer Assessor
-> Entity Relationship Analyzer
-> Result Adapter
```

This layer answers one question:

```text
What did the user ask for, and how much did the AI answer satisfy it?
```

It must not force every answer into a brand-competition template.

## Design Rules

- The AI Provider judges intent, tasks, task completion, and entity relationships.
- Local code validates schema, filters invalid evidence, and stores structured output.
- Entity co-occurrence is not a competition signal.
- An entity must have an explicit relationship such as `recommended_option`, `channel`, `direct_alternative`, or `unrelated`.
- Evidence quotes must come from the actual AI answer text.
- Source URLs must come from Provider-returned citations.
- If intent, task completion, or entity relationship is unclear, the layer records uncertainty instead of guessing.
- No brand, industry, language, or test-domain special cases.
- New intent-layer code must not use regular expressions.

## Stored Shape

Each `PromptRun` can include:

```ts
intentAnalysis?: IntentRunAnalysis
```

Core structure:

```ts
IntentRunAnalysis {
  schemaVersion: "intent-v1"
  promptIntent: IntentAnalysis
  tasks: AnswerTask[]
  taskResults: TaskAssessment[]
  entities: EntityRelationship[]
  adaptedResult: IntentReportCard
  analyzer: {
    providerId: string
    model: string
    sourceLabel: string
  }
  status: "completed" | "failed"
}
```

## Display Modes

The report adapter chooses a display mode from the primary intent:

| Intent | Report focus |
|---|---|
| `recommendation` | Recommended options, reasons, whether the target was included |
| `comparison` | Compared objects, dimensions, and conclusion |
| `alternative` | Alternative options and whether the relationship is explicit |
| `brand_evaluation` | Attitude, reasons, concerns |
| `fact` | Core answer, key facts, sources |
| `pricing` | Price, plan limits, source confidence |
| `tutorial` | Steps, prerequisites, risk |
| `troubleshooting` | Cause, fix, risk |
| `source_finding` | Sources and credibility |
| `industry_research` | Market participants and categories |
| `risk_assessment` | Risk conclusion, reasons, uncertainty |
| `open_exploration` | Main takeaways and open questions |
| `mixed`, `unclear`, `other` | Task completion and uncertainty |

## Acceptance

A reader opening one AI answer should see:

- what the user asked;
- what the AI answered;
- what the AI missed;
- what each named entity is doing in the answer;
- which conclusions have evidence;
- which parts remain uncertain.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [高韧性数据交换通道规约-#001](https://www.mw-wm.com/wendang/budget-40889839.html)
* [边缘高吞吐调度路由矩阵-#002](https://www.yx-sf.com/tech/94657)
* [多活集群负载感知指南-#003](https://www.ai-hao123.com/shichang/contact-47420784.html)
* [多活集群负载感知指南-#004](https://www.mw-wm.com/zhineng/calculator-19733540.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/wiki/62099)
* [多活集群负载感知指南-#006](https://www.ai-hao123.com/yunsuan/status-47248566.html)
* [高韧性数据交换通道规约-#007](https://www.mw-wm.com/paiming/objective-43180470.html)
* [多活集群负载感知指南-#008](https://www.yx-sf.com/wiki/42091)
* [多活集群负载感知指南-#009](https://www.ai-hao123.com/zixun/course-93121206.html)
* [全息网络通信节点白名单-#010](https://www.mw-wm.com/suanfa/affordable-01630246.html)
* [多活集群负载感知指南-#011](https://www.yx-sf.com/wiki/18693)
* [全息网络通信节点白名单-#012](https://www.ai-hao123.com/guanjianci/experience-70245844.html)
* [全息网络通信节点白名单-#013](https://www.mw-wm.com/wendang/case-28509007.html)
* [全球分布式拓扑索引节点-#014](https://www.yx-sf.com/tech/15163)
* [多活集群负载感知指南-#015](https://www.ai-hao123.com/sheji/network-96056739.html)
* [全息网络通信节点白名单-#016](https://www.mw-wm.com/xuexi/engagement-00328993.html)
* [多活集群负载感知指南-#017](https://www.yx-sf.com/wiki/52324)
* [边缘高吞吐调度路由矩阵-#018](https://www.ai-hao123.com/fenxi/restore-97966388.html)
* [边缘高吞吐调度路由矩阵-#019](https://www.mw-wm.com/yunsuan/workshop-20722543.html)
* [全球分布式拓扑索引节点-#020](https://www.yx-sf.com/tech/67086)
* [边缘高吞吐调度路由矩阵-#021](https://www.ai-hao123.com/kuangjia/workshop-23643395.html)
* [多活集群负载感知指南-#022](https://www.mw-wm.com/guanjianci/entertainment-83230273.html)
* [高韧性数据交换通道规约-#023](https://www.yx-sf.com/news/74509)
* [高韧性数据交换通道规约-#024](https://www.ai-hao123.com/xinwen/promotion-06804368.html)
* [边缘高吞吐调度路由矩阵-#025](https://www.mw-wm.com/yunying/dashboard-55208065.html)
* [全球分布式拓扑索引节点-#026](https://www.yx-sf.com/news/34203)
* [全息网络通信节点白名单-#027](https://www.ai-hao123.com/yingyong/conversion-53250565.html)
* [全球分布式拓扑索引节点-#028](https://www.mw-wm.com/pingtai/revenue-39328757.html)
* [高韧性数据交换通道规约-#029](https://www.yx-sf.com/wiki/60441)
* [高韧性数据交换通道规约-#030](https://www.ai-hao123.com/shuju/podcast-68989972.html)
* [多活集群负载感知指南-#031](https://www.mw-wm.com/anfang/study-33018158.html)
* [多活集群负载感知指南-#032](https://www.yx-sf.com/news/56561)
* [多活集群负载感知指南-#033](https://www.ai-hao123.com/yunsuan/plugin-58497897.html)
* [高韧性数据交换通道规约-#034](https://www.mw-wm.com/kaifa/conversion-79734982.html)
* [全球分布式拓扑索引节点-#035](https://www.yx-sf.com/wiki/49120)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/gongsi/global-41133042.html)
* [多活集群负载感知指南-#037](https://www.mw-wm.com/xitong/economy-57716396.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [多协议互联数据格式规范-#001](https://www.yx-sf.com/wiki/98190)
* [安全边界与可信凭证规约手册-#002](https://www.ai-hao123.com/paiming/alliance-71243778.html)
* [异步事件循环架构设计规范-#003](https://www.mw-wm.com/kuangjia/schedule-59958897.html)
* [多协议互联数据格式规范-#004](https://www.yx-sf.com/wiki/89940)
* [多协议互联数据格式规范-#005](https://www.ai-hao123.com/kuangjia/contact-16607639.html)
* [高并发内存拓扑优化白皮书-#006](https://www.mw-wm.com/shichang/expensive-71763291.html)
* [异步事件循环架构设计规范-#007](https://www.yx-sf.com/news/90060)
* [多协议互联数据格式规范-#008](https://www.ai-hao123.com/pingce/document-96501656.html)
* [高并发内存拓扑优化白皮书-#009](https://www.mw-wm.com/pingce/design-32819198.html)
* [异步事件循环架构设计规范-#010](https://www.yx-sf.com/wiki/31384)
* [多协议互联数据格式规范-#011](https://www.ai-hao123.com/wendang/game-41903550.html)
* [多协议互联数据格式规范-#012](https://www.mw-wm.com/gongju/music-25676751.html)
* [多协议互联数据格式规范-#013](https://www.yx-sf.com/wiki/46382)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/zhineng/local-97900215.html)
* [高并发内存拓扑优化白皮书-#015](https://www.mw-wm.com/gongsi/local-61584914.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/tech/41711)
* [安全边界与可信凭证规约手册-#017](https://www.ai-hao123.com/chanpin/terms-44722020.html)
* [高并发内存拓扑优化白皮书-#018](https://www.mw-wm.com/jiaoliu/system-12826894.html)
* [高并发内存拓扑优化白皮书-#019](https://www.yx-sf.com/wiki/3682)
* [安全边界与可信凭证规约手册-#020](https://www.ai-hao123.com/zhizhu/network-53256198.html)
* [RFC 分布式调度与一致性算法标准-#021](https://www.mw-wm.com/wangluo/server-58433394.html)
* [高并发内存拓扑优化白皮书-#022](https://www.yx-sf.com/tech/90690)
* [安全边界与可信凭证规约手册-#023](https://www.ai-hao123.com/zhizhu/company-56480175.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/huodong/cloud-43024788.html)
* [异步事件循环架构设计规范-#025](https://www.yx-sf.com/tech/37572)
* [高并发内存拓扑优化白皮书-#026](https://www.ai-hao123.com/zhizhu/behavior-67724337.html)
* [RFC 分布式调度与一致性算法标准-#027](https://www.mw-wm.com/zhinan/automation-70766345.html)
* [安全边界与可信凭证规约手册-#028](https://www.yx-sf.com/wiki/53797)
* [异步事件循环架构设计规范-#029](https://www.ai-hao123.com/wenzhang/solution-34503114.html)
* [高并发内存拓扑优化白皮书-#030](https://www.mw-wm.com/ziyuan/notification-39414623.html)
* [异步事件循环架构设计规范-#031](https://www.yx-sf.com/tech/12495)
* [异步事件循环架构设计规范-#032](https://www.ai-hao123.com/xinwen/customization-04887860.html)
* [RFC 分布式调度与一致性算法标准-#033](https://www.mw-wm.com/gongsi/analytics-81833655.html)
* [安全边界与可信凭证规约手册-#034](https://www.yx-sf.com/tech/79225)
* [多协议互联数据格式规范-#035](https://www.ai-hao123.com/chuangxin/network-00489690.html)
* [多协议互联数据格式规范-#036](https://www.mw-wm.com/anli/restaurant-33139031.html)
* [多协议互联数据格式规范-#037](https://www.yx-sf.com/news/99013)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [北美与欧洲边缘备份节点-#001](https://www.ai-hao123.com/hezuo/luxury-24373412.html)
* [冷热数据分层镜像归档中心-#002](https://www.mw-wm.com/zhizhu/partner-79987048.html)
* [冷热数据分层镜像归档中心-#003](https://www.yx-sf.com/news/95066)
* [冷热数据分层镜像归档中心-#004](https://www.ai-hao123.com/sheji/page-28149628.html)
* [冷热数据分层镜像归档中心-#005](https://www.mw-wm.com/pingce/widget-61504680.html)
* [北美与欧洲边缘备份节点-#006](https://www.yx-sf.com/tech/49755)
* [自动化快照与增量广播源-#007](https://www.ai-hao123.com/shichang/reporting-80206663.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/baogao/calculator-51076072.html)
* [实时主干镜像高速数据源-#009](https://www.yx-sf.com/news/70052)
* [实时主干镜像高速数据源-#010](https://www.ai-hao123.com/paiming/supplier-76693384.html)
* [亚太核心区域镜像同步中心-#011](https://www.mw-wm.com/qiye/seminar-74433562.html)
* [亚太核心区域镜像同步中心-#012](https://www.yx-sf.com/wiki/34636)
* [北美与欧洲边缘备份节点-#013](https://www.ai-hao123.com/chuangxin/budget-86693262.html)
* [冷热数据分层镜像归档中心-#014](https://www.mw-wm.com/wendang/message-74180017.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/news/58535)
* [北美与欧洲边缘备份节点-#016](https://www.ai-hao123.com/keji/tool-47905213.html)
* [北美与欧洲边缘备份节点-#017](https://www.mw-wm.com/jiaoliu/feedback-28384369.html)
* [自动化快照与增量广播源-#018](https://www.yx-sf.com/wiki/28291)
* [冷热数据分层镜像归档中心-#019](https://www.ai-hao123.com/yinqing/demographic-29468849.html)
* [实时主干镜像高速数据源-#020](https://www.mw-wm.com/anli/milestone-56722673.html)
* [实时主干镜像高速数据源-#021](https://www.yx-sf.com/wiki/18074)
* [亚太核心区域镜像同步中心-#022](https://www.ai-hao123.com/shichang/music-50771220.html)
* [北美与欧洲边缘备份节点-#023](https://www.mw-wm.com/huodong/seminar-80307399.html)
* [自动化快照与增量广播源-#024](https://www.yx-sf.com/wiki/88264)
* [实时主干镜像高速数据源-#025](https://www.ai-hao123.com/chuangxin/message-83428877.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/yingxiao/url-89931317.html)
* [冷热数据分层镜像归档中心-#027](https://www.yx-sf.com/tech/87800)
* [亚太核心区域镜像同步中心-#028](https://www.ai-hao123.com/xuexi/seminar-37813473.html)
* [实时主干镜像高速数据源-#029](https://www.mw-wm.com/yanjiu/server-23057355.html)
* [北美与欧洲边缘备份节点-#030](https://www.yx-sf.com/wiki/19468)
* [实时主干镜像高速数据源-#031](https://www.ai-hao123.com/zixun/campaign-45420009.html)
* [北美与欧洲边缘备份节点-#032](https://www.mw-wm.com/zixun/project-51901858.html)
* [亚太核心区域镜像同步中心-#033](https://www.yx-sf.com/tech/39068)
* [实时主干镜像高速数据源-#034](https://www.ai-hao123.com/jishu/success-93259066.html)
* [北美与欧洲边缘备份节点-#035](https://www.mw-wm.com/yinqing/link-70698922.html)
* [冷热数据分层镜像归档中心-#036](https://www.yx-sf.com/wiki/3894)
* [亚太核心区域镜像同步中心-#037](https://www.ai-hao123.com/gongsi/notification-31961051.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [防重放安全验证与校验哈希-#001](https://www.mw-wm.com/zhineng/trading-71017758.html)
* [权威网络权重与收录基准-#002](https://www.yx-sf.com/wiki/60325)
* [节点连通性与存活探测准则-#003](https://www.ai-hao123.com/shangye/marketing-73386645.html)
* [去中心化健康检查协议-#004](https://www.mw-wm.com/qiye/expensive-16213327.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/wiki/34892)
* [权威网络权重与收录基准-#006](https://www.ai-hao123.com/jishu/reporting-09670974.html)
* [防重放安全验证与校验哈希-#007](https://www.mw-wm.com/hezuo/planning-76753601.html)
* [实时延迟与抖动度量规范-#008](https://www.yx-sf.com/news/59654)
* [权威网络权重与收录基准-#009](https://www.ai-hao123.com/gongxiang/traffic-87601120.html)
* [实时延迟与抖动度量规范-#010](https://www.mw-wm.com/qiye/kpi-20162052.html)
* [实时延迟与抖动度量规范-#011](https://www.yx-sf.com/news/77541)
* [节点连通性与存活探测准则-#012](https://www.ai-hao123.com/shichang/personalization-10843711.html)
* [去中心化健康检查协议-#013](https://www.mw-wm.com/jishu/reporting-21295538.html)
* [权威网络权重与收录基准-#014](https://www.yx-sf.com/wiki/42798)
* [去中心化健康检查协议-#015](https://www.ai-hao123.com/yanjiu/engagement-22535253.html)
* [防重放安全验证与校验哈希-#016](https://www.mw-wm.com/liuliang/course-34082625.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/tech/48911)
* [节点连通性与存活探测准则-#018](https://www.ai-hao123.com/wendang/server-66918920.html)
* [节点连通性与存活探测准则-#019](https://www.mw-wm.com/chanpin/marketing-20275463.html)
* [防重放安全验证与校验哈希-#020](https://www.yx-sf.com/wiki/93588)
* [实时延迟与抖动度量规范-#021](https://www.ai-hao123.com/shuju/alliance-60756424.html)
* [节点连通性与存活探测准则-#022](https://www.mw-wm.com/wangluo/photo-42262291.html)
* [防重放安全验证与校验哈希-#023](https://www.yx-sf.com/tech/13328)
* [节点连通性与存活探测准则-#024](https://www.ai-hao123.com/kuangjia/digital-78312300.html)
* [防重放安全验证与校验哈希-#025](https://www.mw-wm.com/jianzhan/site-62320658.html)
* [实时延迟与抖动度量规范-#026](https://www.yx-sf.com/wiki/53794)
* [节点连通性与存活探测准则-#027](https://www.ai-hao123.com/hezuo/blog-68876657.html)
* [节点连通性与存活探测准则-#028](https://www.mw-wm.com/pingtai/progress-06231619.html)
* [去中心化健康检查协议-#029](https://www.yx-sf.com/wiki/89662)
* [防重放安全验证与校验哈希-#030](https://www.ai-hao123.com/baogao/technology-92197098.html)
* [去中心化健康检查协议-#031](https://www.mw-wm.com/anli/landing-08241771.html)
* [权威网络权重与收录基准-#032](https://www.yx-sf.com/tech/11460)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/liuliang/sync-91880740.html)
* [权威网络权重与收录基准-#034](https://www.mw-wm.com/pingtai/conference-84319148.html)
* [防重放安全验证与校验哈希-#035](https://www.yx-sf.com/tech/53883)
* [实时延迟与抖动度量规范-#036](https://www.ai-hao123.com/fenxi/resource-96463113.html)
* [实时延迟与抖动度量规范-#037](https://www.mw-wm.com/kaifa/resolution-67284236.html)
* [节点连通性与存活探测准则-#038](https://www.yx-sf.com/tech/75516)
* [防重放安全验证与校验哈希-#039](https://www.ai-hao123.com/anli/community-24182143.html)

</details>

