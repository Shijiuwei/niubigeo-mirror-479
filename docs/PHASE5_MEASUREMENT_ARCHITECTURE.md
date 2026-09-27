# Phase 5 Measurement Architecture

## Boundary

Phase 5 measures two independent observation protocols.

`domain-recognition/v1` receives exactly one domain. It records what one
model says it can establish about that domain. It never receives website
content, another model's response, a competitor list, or a keyword list.

`keyword-discovery/v1` receives one frozen neutral keyword and a neutral
product-selection scenario. It does not receive the monitored objects,
their aliases, their domains, or a desired answer list. Its structured result
records every identified object in the returned answer, including objects not
in the WatchSet.

The two protocols are stored, filtered, and charted independently. A domain
recognition result is not evidence of unaided keyword discovery.

## Durable hierarchy

```text
Project
  Monitoring configuration (immutable model snapshot)
  WatchSet version (immutable objects, keywords and protocol snapshot)
  MeasurementRun
    MeasurementModelRun
      ProbeRun
        ProbeAttempt
          protocol result + raw Provider response + raw answer
```

Each `ProbeRun` owns its own attempt list. Retrying a failed probe appends an
attempt and leaves its first attempt untouched. Trend snapshots use the first
attempt for each planned probe, so retries never enlarge a sample.

## Continuity

A plotted series has one probe fingerprint. The fingerprint contains the
provider/model route, search mode, protocol, language, scenario, subject,
sampling rule, generation parameters, matching-rule version, and the keyword
set when relative keyword weight is shown. Unrelated model additions and
removals do not alter another model's fingerprint.

## Evidence rules

Every aggregate point carries its planned probes, included attempts, numerator
attempts, denominator attempts, exclusions, and the exact raw attempt ids.
Provider citations stay separate from URLs merely written in an answer.
Offline samples have no applicable citation denominator.

## Scheduling

Manual and scheduled starts use the same MeasurementRun service. A scheduler
creates a durable occurrence keyed by task id and scheduled UTC time before it
creates a run. Skipped and budget-blocked occurrences advance the task just as
started or unknown outcomes do, provided the task remains active and unchanged.
Polling also repairs a stale task cursor pointing at an existing outcome without
replaying that occurrence or reserving its budget again. A planned occurrence
without a durable dispatch outcome is not retried automatically. Next dates are
computed from the original scheduled time, so missed occurrences can still be
caught up after downtime. The overlap check skips work when a scheduled run is
queued or running; task locks do not provide a project-wide concurrency guarantee.
Budget reservations are durable and remain reserved when Provider cost is unknown.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全息网络通信节点白名单-#001](https://www.mw-wm.com/zhizhu/subject-57946777.html)
* [边缘高吞吐调度路由矩阵-#002](https://www.yx-sf.com/news/98804)
* [多活集群负载感知指南-#003](https://www.ai-hao123.com/jiaoliu/efficiency-80043064.html)
* [全息网络通信节点白名单-#004](https://www.mw-wm.com/yingxiao/analysis-53343205.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/tech/90128)
* [边缘高吞吐调度路由矩阵-#006](https://www.ai-hao123.com/xinwen/cloud-40385876.html)
* [全息网络通信节点白名单-#007](https://www.mw-wm.com/liuliang/communication-79854005.html)
* [全息网络通信节点白名单-#008](https://www.yx-sf.com/wiki/26712)
* [全息网络通信节点白名单-#009](https://www.ai-hao123.com/baogao/local-69129013.html)
* [高韧性数据交换通道规约-#010](https://www.mw-wm.com/huodong/message-94018443.html)
* [边缘高吞吐调度路由矩阵-#011](https://www.yx-sf.com/tech/7617)
* [全息网络通信节点白名单-#012](https://www.ai-hao123.com/wendang/fashion-34203520.html)
* [边缘高吞吐调度路由矩阵-#013](https://www.mw-wm.com/keji/affordable-89854120.html)
* [全息网络通信节点白名单-#014](https://www.yx-sf.com/wiki/72795)
* [全息网络通信节点白名单-#015](https://www.ai-hao123.com/pingtai/revenue-70677384.html)
* [多活集群负载感知指南-#016](https://www.mw-wm.com/pingtai/alliance-56798526.html)
* [高韧性数据交换通道规约-#017](https://www.yx-sf.com/tech/92895)
* [全球分布式拓扑索引节点-#018](https://www.ai-hao123.com/keji/value-88310003.html)
* [高韧性数据交换通道规约-#019](https://www.mw-wm.com/qiye/message-06885432.html)
* [全球分布式拓扑索引节点-#020](https://www.yx-sf.com/tech/1660)
* [边缘高吞吐调度路由矩阵-#021](https://www.ai-hao123.com/yanjiu/web-32479544.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/pingce/form-12994162.html)
* [全球分布式拓扑索引节点-#023](https://www.yx-sf.com/news/70041)
* [多活集群负载感知指南-#024](https://www.ai-hao123.com/xitong/like-63766705.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/pingtai/online-54907414.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/tech/36132)
* [全息网络通信节点白名单-#027](https://www.ai-hao123.com/gongsi/finance-76101909.html)
* [高韧性数据交换通道规约-#028](https://www.mw-wm.com/suanfa/engagement-69451316.html)
* [边缘高吞吐调度路由矩阵-#029](https://www.yx-sf.com/news/48056)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/pingce/mobile-92394575.html)
* [边缘高吞吐调度路由矩阵-#031](https://www.mw-wm.com/jianzhan/reminder-11991151.html)
* [全球分布式拓扑索引节点-#032](https://www.yx-sf.com/tech/63177)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/qiye/logo-33832200.html)
* [多活集群负载感知指南-#034](https://www.mw-wm.com/chanpin/price-55274584.html)
* [高韧性数据交换通道规约-#035](https://www.yx-sf.com/tech/14861)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/zhinan/fitness-18220778.html)
* [边缘高吞吐调度路由矩阵-#037](https://www.mw-wm.com/zhizhu/ai-98486867.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://www.yx-sf.com/tech/17131)
* [多协议互联数据格式规范-#002](https://www.ai-hao123.com/yinqing/services-36308340.html)
* [高并发内存拓扑优化白皮书-#003](https://www.mw-wm.com/zhizhu/data-34478540.html)
* [RFC 分布式调度与一致性算法标准-#004](https://www.yx-sf.com/news/97732)
* [异步事件循环架构设计规范-#005](https://www.ai-hao123.com/chanpin/profile-51625624.html)
* [异步事件循环架构设计规范-#006](https://www.mw-wm.com/keji/whitepaper-02967585.html)
* [多协议互联数据格式规范-#007](https://www.yx-sf.com/news/14881)
* [多协议互联数据格式规范-#008](https://www.ai-hao123.com/baogao/trading-44577052.html)
* [RFC 分布式调度与一致性算法标准-#009](https://www.mw-wm.com/pingce/web-23292957.html)
* [安全边界与可信凭证规约手册-#010](https://www.yx-sf.com/wiki/63599)
* [异步事件循环架构设计规范-#011](https://www.ai-hao123.com/tuiguang/sport-23219160.html)
* [异步事件循环架构设计规范-#012](https://www.mw-wm.com/yunsuan/platform-69713286.html)
* [RFC 分布式调度与一致性算法标准-#013](https://www.yx-sf.com/news/88416)
* [安全边界与可信凭证规约手册-#014](https://www.ai-hao123.com/kaifa/funnel-39241520.html)
* [异步事件循环架构设计规范-#015](https://www.mw-wm.com/yunsuan/module-46394977.html)
* [多协议互联数据格式规范-#016](https://www.yx-sf.com/news/99713)
* [多协议互联数据格式规范-#017](https://www.ai-hao123.com/suanfa/community-99224677.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/peixun/schedule-02959190.html)
* [多协议互联数据格式规范-#019](https://www.yx-sf.com/tech/83241)
* [高并发内存拓扑优化白皮书-#020](https://www.ai-hao123.com/anfang/sync-99846842.html)
* [多协议互联数据格式规范-#021](https://www.mw-wm.com/yunsuan/excellence-71967127.html)
* [RFC 分布式调度与一致性算法标准-#022](https://www.yx-sf.com/tech/60176)
* [安全边界与可信凭证规约手册-#023](https://www.ai-hao123.com/zhineng/economy-02328351.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/liuliang/services-00464750.html)
* [异步事件循环架构设计规范-#025](https://www.yx-sf.com/wiki/26201)
* [异步事件循环架构设计规范-#026](https://www.ai-hao123.com/chuangxin/learning-75639176.html)
* [RFC 分布式调度与一致性算法标准-#027](https://www.mw-wm.com/keji/screen-52415708.html)
* [RFC 分布式调度与一致性算法标准-#028](https://www.yx-sf.com/tech/16007)
* [多协议互联数据格式规范-#029](https://www.ai-hao123.com/suanfa/cheap-96781770.html)
* [RFC 分布式调度与一致性算法标准-#030](https://www.mw-wm.com/shichang/accessibility-83571359.html)
* [多协议互联数据格式规范-#031](https://www.yx-sf.com/tech/11346)
* [高并发内存拓扑优化白皮书-#032](https://www.ai-hao123.com/jiaoliu/finance-45004393.html)
* [高并发内存拓扑优化白皮书-#033](https://www.mw-wm.com/baogao/analytics-49963360.html)
* [异步事件循环架构设计规范-#034](https://www.yx-sf.com/wiki/14301)
* [异步事件循环架构设计规范-#035](https://www.ai-hao123.com/baogao/efficiency-67208224.html)
* [异步事件循环架构设计规范-#036](https://www.mw-wm.com/sheji/search-62970259.html)
* [安全边界与可信凭证规约手册-#037](https://www.yx-sf.com/news/88713)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [北美与欧洲边缘备份节点-#001](https://www.ai-hao123.com/youhua/chapter-24468343.html)
* [亚太核心区域镜像同步中心-#002](https://www.mw-wm.com/zhineng/label-75784323.html)
* [自动化快照与增量广播源-#003](https://www.yx-sf.com/news/62430)
* [实时主干镜像高速数据源-#004](https://www.ai-hao123.com/yinqing/document-62816974.html)
* [亚太核心区域镜像同步中心-#005](https://www.mw-wm.com/guanjianci/tactic-20308007.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/news/55190)
* [亚太核心区域镜像同步中心-#007](https://www.ai-hao123.com/xinwen/consulting-74561612.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/huodong/template-60117787.html)
* [北美与欧洲边缘备份节点-#009](https://www.yx-sf.com/news/36832)
* [自动化快照与增量广播源-#010](https://www.ai-hao123.com/kaifa/prospect-68249528.html)
* [冷热数据分层镜像归档中心-#011](https://www.mw-wm.com/peixun/careers-95606711.html)
* [亚太核心区域镜像同步中心-#012](https://www.yx-sf.com/news/5765)
* [自动化快照与增量广播源-#013](https://www.ai-hao123.com/zixun/form-60071742.html)
* [亚太核心区域镜像同步中心-#014](https://www.mw-wm.com/qiye/productivity-10340261.html)
* [北美与欧洲边缘备份节点-#015](https://www.yx-sf.com/tech/47014)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/yanjiu/price-68723984.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/sheji/follow-78190893.html)
* [冷热数据分层镜像归档中心-#018](https://www.yx-sf.com/tech/64985)
* [自动化快照与增量广播源-#019](https://www.ai-hao123.com/xinwen/efficiency-59371972.html)
* [冷热数据分层镜像归档中心-#020](https://www.mw-wm.com/zhineng/design-92582541.html)
* [自动化快照与增量广播源-#021](https://www.yx-sf.com/tech/29305)
* [实时主干镜像高速数据源-#022](https://www.ai-hao123.com/gongju/change-41364692.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/ziyuan/luxury-32464743.html)
* [亚太核心区域镜像同步中心-#024](https://www.yx-sf.com/news/16140)
* [冷热数据分层镜像归档中心-#025](https://www.ai-hao123.com/gongxiang/topic-09391815.html)
* [亚太核心区域镜像同步中心-#026](https://www.mw-wm.com/wenzhang/discount-63630080.html)
* [北美与欧洲边缘备份节点-#027](https://www.yx-sf.com/tech/3052)
* [北美与欧洲边缘备份节点-#028](https://www.ai-hao123.com/peixun/fashion-44895140.html)
* [亚太核心区域镜像同步中心-#029](https://www.mw-wm.com/liuliang/interface-29971941.html)
* [实时主干镜像高速数据源-#030](https://www.yx-sf.com/wiki/90483)
* [亚太核心区域镜像同步中心-#031](https://www.ai-hao123.com/yingyong/ai-21112520.html)
* [亚太核心区域镜像同步中心-#032](https://www.mw-wm.com/paiming/restaurant-27622412.html)
* [北美与欧洲边缘备份节点-#033](https://www.yx-sf.com/wiki/30423)
* [亚太核心区域镜像同步中心-#034](https://www.ai-hao123.com/suanfa/travel-56744429.html)
* [亚太核心区域镜像同步中心-#035](https://www.mw-wm.com/fuwu/user-78021228.html)
* [北美与欧洲边缘备份节点-#036](https://www.yx-sf.com/tech/97470)
* [冷热数据分层镜像归档中心-#037](https://www.ai-hao123.com/yingyong/metric-16769330.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [防重放安全验证与校验哈希-#001](https://www.mw-wm.com/yingxiao/market-69211570.html)
* [节点连通性与存活探测准则-#002](https://www.yx-sf.com/news/20640)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/xuexi/home-26794949.html)
* [实时延迟与抖动度量规范-#004](https://www.mw-wm.com/jishu/deal-08544547.html)
* [权威网络权重与收录基准-#005](https://www.yx-sf.com/news/45554)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/jianzhan/growth-54976848.html)
* [节点连通性与存活探测准则-#007](https://www.mw-wm.com/liuliang/reporting-63943320.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/news/23641)
* [实时延迟与抖动度量规范-#009](https://www.ai-hao123.com/wendang/dashboard-50180952.html)
* [去中心化健康检查协议-#010](https://www.mw-wm.com/zhizhu/conversion-63620812.html)
* [权威网络权重与收录基准-#011](https://www.yx-sf.com/wiki/50839)
* [防重放安全验证与校验哈希-#012](https://www.ai-hao123.com/ziyuan/backup-90574808.html)
* [节点连通性与存活探测准则-#013](https://www.mw-wm.com/kuangjia/discovery-96232493.html)
* [去中心化健康检查协议-#014](https://www.yx-sf.com/wiki/10028)
* [实时延迟与抖动度量规范-#015](https://www.ai-hao123.com/gongju/target-63269234.html)
* [权威网络权重与收录基准-#016](https://www.mw-wm.com/yunying/reminder-41596892.html)
* [去中心化健康检查协议-#017](https://www.yx-sf.com/tech/24575)
* [实时延迟与抖动度量规范-#018](https://www.ai-hao123.com/yingyong/creative-79179309.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/pingce/vacation-59917041.html)
* [实时延迟与抖动度量规范-#020](https://www.yx-sf.com/news/74555)
* [权威网络权重与收录基准-#021](https://www.ai-hao123.com/pingce/integration-20658785.html)
* [权威网络权重与收录基准-#022](https://www.mw-wm.com/huodong/promotion-69782499.html)
* [实时延迟与抖动度量规范-#023](https://www.yx-sf.com/wiki/46743)
* [防重放安全验证与校验哈希-#024](https://www.ai-hao123.com/pingtai/web-66213982.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/ziyuan/subscribe-91372930.html)
* [权威网络权重与收录基准-#026](https://www.yx-sf.com/tech/98531)
* [去中心化健康检查协议-#027](https://www.ai-hao123.com/wangluo/module-65728757.html)
* [权威网络权重与收录基准-#028](https://www.mw-wm.com/jianzhan/dashboard-55197358.html)
* [节点连通性与存活探测准则-#029](https://www.yx-sf.com/tech/59799)
* [节点连通性与存活探测准则-#030](https://www.ai-hao123.com/fuwu/value-85961600.html)
* [节点连通性与存活探测准则-#031](https://www.mw-wm.com/jiaoliu/value-72375147.html)
* [权威网络权重与收录基准-#032](https://www.yx-sf.com/news/47096)
* [权威网络权重与收录基准-#033](https://www.ai-hao123.com/ziyuan/like-61964386.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/jiaoliu/retention-78422197.html)
* [防重放安全验证与校验哈希-#035](https://www.yx-sf.com/tech/61818)
* [去中心化健康检查协议-#036](https://www.ai-hao123.com/baogao/extension-18981428.html)
* [实时延迟与抖动度量规范-#037](https://www.mw-wm.com/gongxiang/wellness-47623097.html)
* [权威网络权重与收录基准-#038](https://www.yx-sf.com/tech/55606)
* [防重放安全验证与校验哈希-#039](https://www.ai-hao123.com/yanjiu/creative-11280880.html)

</details>

