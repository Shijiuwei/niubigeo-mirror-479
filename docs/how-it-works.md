# 工作原理：从域名到证据

适用于当前 `src/product` 实现；计划版本 **v0.2.0-rc.1，UNPUBLISHED**。本文说明产品怎样取得和处理回答，不代表 Phase 6 的真实调用、截图或发布验收已经完成。

**打破 SEO / GEO 报告黑盒，把证据交还给用户。** 当前测量 AI 回答和引用，不提供传统搜索排名监测。

输入一个域名，查看不同 AI 如何描述你、提到哪些竞争对象、关联哪些关键词，以及回答中实际返回了哪些来源。每一次比较，都能回到对应模型的原始回答。

我们公开的是本次回答及其证据，无法据此读出模型内部的思考过程，也不能保证再次运行得到完全相同的答案。

## 本文案例的状态

以 [R02：vercel.com](../examples/cases/R02/README.md) 作为流程阅读入口。它是运行前选定的应用部署案例，保存了三个模型的初始 D 回答和三次后续测量。九条 K 观察中三条结构化解析失败，失败原文仍保留；三次运行均为部分完成，不能写成三次全部成功。至少一次由真实到期任务触发，验收后任务已暂停。各次请求、词表来源、费用、截图与原文见案例证据。

案例分类用于索引，不发送给模型。[研究计划](../examples/study-plan.json) 固定 20 个输入、两路离线模型和一路联网模型，R02/R04 各执行三次持续测量。R02 回答语言为 en。原文和结论以案例目录的版本化结果与证据为准；本轮没有将旧 Alpha、测试 Fixture 或历史案例改名后计为新实测。完整调用上界与筛选规则见 [测量方法](measurement-methodology.md)。

## 1. 保存项目与测试条件

创建项目会规范化域名，保存品牌显示名、别名和默认回答语言。当前 `primaryDomain` 本身也是规范化后的值，所以研究计划还应独立保留用户原始输入。创建项目不抓取官网，不发模型推理。

从实际模型目录选择 OpenRouter 路由和 `off`（不联网）或 `provider_native`（Provider 原生联网）。模型目录能力表示允许选择的配置，不保证下一次请求可用。随后保存一个 Baseline，即监测配置快照；后续运行记录其 ID 和版本。

当前一个模型 ID 在同一份模型选择中只能出现一次；同一模型的联网/不联网对照需使用不同配置或运行，并明确保留各自条件。参数默认 temperature 为 0、maxTokens 为 900。temperature 为 0 也不构成逐字重现保证。

## 2. 域名认知 D：点名后的描述

D 的内部协议名为 `domain-recognition/v1`。模型收到规范化域名、语言和固定协议指令；项目品牌名、别名、竞品名单、官网正文、案例分类以及其他模型回答不进入这个 Prompt。

域名已被点名，所以 D 回答复述域名不能证明“自然发现”或“关键词推荐”。联网 D 允许 Provider 自己搜索；调用方仍不注入官网介绍。

初始认知运行按模型分别保存：

- 域名识别声明 `domainRecognition`，包括 recognized、not_recognized、unknown。
- 本次输出的完整性/确定性 `analysisStatus`，以及缺失或不合法字段记录 `fieldIssues`。
- 品牌、业务、类别、实际列出的竞品、目标关键词和逐竞品关键词。
- Provider 返回的引用、回答中出现的普通 URL、引用与字段的可追溯关联。
- 实际模型、请求参数、搜索执行信息、原始响应、原始回答、用量、费用或费用未知、时间和错误。

这些是一次 API 回答中的观察，不是经过事实核查的公司资料。空竞品数组只表示这次没有列出竞品；某词被关联也不是搜索热度或商业价值。

## 3. 回答、解析和报告各自保存

初始认知服务先写入含原文的 `response_saved` Attempt，再解析结构化内容。请求失败、响应截断、字段缺失、解析失败和模型明确回答 unknown 是不同状态。不能把“仅恢复出部分字段”写成“模型部分认识品牌”。

有原文时，可以本地重新分析并产生 AnalysisRevision；这不重新调用 Provider。需要重新请求时会新增 Attempt，可能产生费用。当前初始认知在解析失败且 Provider 明确标记截断时，还会自动用 2000 输出上限再请求一次；两次请求条件不同、都必须计入账本。

认知报告从终态 Run 中每个模型的当前 Attempt 生成，保留 `sourceAttemptMap` 和记录 Hash。竞品按规范化名称与 host 精确分组；报告不访问官网、不调用其他模型写结论。一个模型失败不会抹去其他模型的原文。

认知详情页可以显示最新本地分析修订，但报告构建当前仍读取原始 Attempt 归档。重新分析后不能直接假定报告已采用修订，需核对报告来源。见 [证据模型](evidence-model.md)。

## 4. 从认知报告建立待测范围

WatchSet 是版本化的对象和关键词集合。初次建议来自项目中每个认知 Run 的最新已保存报告：目标对象来自项目配置，竞品来自报告竞品分组，关键词来自目标品牌关键词分组。每项保留来源记录 ID。没有域名的竞品保留为待确认身份，不发独立竞品域名 D。

当前 WatchSet 关键词检查把大小写/首尾空白规范化后，排除包含监测对象名称、别名或域名的词。它并未完成通用的歧义判断，也没有自动“每案例至多两个关键词”的研究规则。Phase 6 在 [案例层](../examples/lib/study.mjs) 另按至少两个不同模型的同词关联、精确原文证据、身份子串排除与确定性排序筛选，K 前冻结每例词表；不能把这层保障当作默认 WatchSet 服务的能力。

已有 active WatchSet 时，新草稿从原范围复制，避免无提示引入后来报告里的新词；它并不会自动合并新发现。模型或配置改变后需确认新范围。没有合格词时保留 D 结果，K 应说明“本次没有足够信息建立关键词测试”。

## 5. 关键词选型 K：未点名时出现谁

K 协议为 `keyword-discovery/v1`。请求只包含一个冻结关键词、语言和中性产品选型指令，不发送目标或竞品的名字、域名、别名和期待答案。

模型返回结构化 mentions，包含产品/组织名称、域名、提及或推荐关系，以及证据片段和先后状态。本地在回答返回后按名称/别名或域名精确匹配 WatchSet；只能唯一匹配时赋予 `matchedObjectId`。范围外对象保留在明细中，不强行归入某个竞品。

“提及”不等于“正面推荐”。“首先提到/推荐”只描述回答中报告的顺序，不能解释为模型内部首先想到谁。当前正面关系和 unique/tied 等状态由被测模型结构化输出提供，指标还没有强制要求片段与偏移全部核验成功；阅读顺序结论时需要查看原文。

持续测量的一个 Run，会对选中模型分别执行所有有确认域名的对象 D，以及所有合格词 K，再乘以 repetitions。**它不是只运行 K 的接口**；初始 D 也不会自动成为这个 Run 的图表样本。不要把“一例一个目标域名”误算成“一例仅一次请求”。

## 6. 一个回答怎样进入图表

路径为 `MeasurementRun → MeasurementModelRun → ProbeRun → ProbeAttempt → 协议结果 → MeasurementMetricPoint`。一份 K 回答可以同时支持目标与竞品的多个指标；不能按被提及对象数放大回答样本量。

每个点记录 `numerator`、`denominator`、`planned`、`failed`、`value`、`samples`。样本明细同时列出命中、未命中与排除项，可以沿 `probeRunId` 和 `attemptId` 打开原文。没有可判定分母通常为 null；真实未命中才是有效分母下的 0%。关键词关联次数有单独的计数显示规则，见 [完整公式](measurement-methodology.md)。

初始认知报告不直接变成测量曲线，图表统计来自 `measurements/` 中的独立 D/K Probe。D 的 unknown 与 K 的 unknown 在当前代码中分母处理不同，不应使用一个通用“成功样本率”替代。

测量的设计意图是一项计划探针只取第一次尝试，重试不增加样本。当前实现仍存在首次 Attempt 与按 Probe 覆盖的结果/引用混用风险；统计缓存和图表断线也有已知缺口。因此不能仅凭曲线形状声称已经完成严格的首次尝试统计验收。

## 7. 重复、调度与模型变化

手工测量和定时测量复用同一个测量服务。调度器到期先保存 Occurrence，再建立 source 为 scheduled 的 Run。真实定时证据至少需要任务配置、计划时间、唯一 Occurrence、实际 Run、Attempt 和最终状态；手动点击运行或一次 scheduler HTTP 200 都不能替代这条证据链。

添加模型后可单独测量从未出现在历史 modelScope 的模型；新模型没有历史补点。移除选择不会删除旧报告或原始证据，但只有保存新 Baseline 后，默认后续运行才使用新的模型集合。旧任务遇到配置变化可进入 incompatible；范围变更和错过时间的调度行为仍有缺口，见 [限制](limitations.md)。

图表时间取实际 Run 开始时间，当前长期筛选是滚动 7/30/90 天或全部时间，没有每日自动去重。三次同条件观察只说明那三次及其时间跨度，不证明统计稳定、品牌排名或 GEO 优化的因果效果。

## 复核与重新测量

复核是读取既有原文、参数、引用路径、Hash 与公式；重新测量是再次请求模型，两者应分别标记。读取报告、构建本地统计、重新分析已存回答均无需模型推理，但构建报告/统计会写入派生文件，读取模型目录仍可能访问外网。

当前公开案例数据缺失时，任何公式演示都应保留空状态，不以示例数值填充实测。技术定位见 [架构](ARCHITECTURE.md)，安装与费用边界见 [Docker 部署](deployment/docker.md)。


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [边缘高吞吐调度路由矩阵-#001](https://www.mw-wm.com/fuwu/personalization-45077139.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/tech/85734)
* [多活集群负载感知指南-#003](https://www.ai-hao123.com/yingyong/extension-10480803.html)
* [多活集群负载感知指南-#004](https://www.mw-wm.com/shangye/case-31913759.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/news/15776)
* [全球分布式拓扑索引节点-#006](https://www.ai-hao123.com/wendang/marketing-12597159.html)
* [全球分布式拓扑索引节点-#007](https://www.mw-wm.com/qiye/quality-15526296.html)
* [边缘高吞吐调度路由矩阵-#008](https://www.yx-sf.com/tech/39840)
* [全息网络通信节点白名单-#009](https://www.ai-hao123.com/fenxi/social-90181989.html)
* [边缘高吞吐调度路由矩阵-#010](https://www.mw-wm.com/yinqing/development-36634758.html)
* [边缘高吞吐调度路由矩阵-#011](https://www.yx-sf.com/news/14890)
* [边缘高吞吐调度路由矩阵-#012](https://www.ai-hao123.com/wenzhang/reminder-32910212.html)
* [多活集群负载感知指南-#013](https://www.mw-wm.com/gongju/price-97768099.html)
* [全息网络通信节点白名单-#014](https://www.yx-sf.com/tech/57229)
* [全球分布式拓扑索引节点-#015](https://www.ai-hao123.com/shuju/creative-30605363.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/jishu/products-79092741.html)
* [边缘高吞吐调度路由矩阵-#017](https://www.yx-sf.com/news/21222)
* [全息网络通信节点白名单-#018](https://www.ai-hao123.com/gongxiang/price-58315973.html)
* [多活集群负载感知指南-#019](https://www.mw-wm.com/gongju/sport-86247840.html)
* [边缘高吞吐调度路由矩阵-#020](https://www.yx-sf.com/news/48007)
* [全息网络通信节点白名单-#021](https://www.ai-hao123.com/gongsi/notification-89862026.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/pingtai/status-61852852.html)
* [全息网络通信节点白名单-#023](https://www.yx-sf.com/tech/65082)
* [边缘高吞吐调度路由矩阵-#024](https://www.ai-hao123.com/zhineng/vacation-88371146.html)
* [高韧性数据交换通道规约-#025](https://www.mw-wm.com/pingce/integration-37298186.html)
* [全息网络通信节点白名单-#026](https://www.yx-sf.com/news/9947)
* [全球分布式拓扑索引节点-#027](https://www.ai-hao123.com/jianzhan/news-23718325.html)
* [高韧性数据交换通道规约-#028](https://www.mw-wm.com/zhizhu/server-71986976.html)
* [多活集群负载感知指南-#029](https://www.yx-sf.com/news/53199)
* [高韧性数据交换通道规约-#030](https://www.ai-hao123.com/xitong/reminder-64244031.html)
* [多活集群负载感知指南-#031](https://www.mw-wm.com/gongxiang/software-96783501.html)
* [多活集群负载感知指南-#032](https://www.yx-sf.com/wiki/67279)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/sheji/cloud-02482883.html)
* [全息网络通信节点白名单-#034](https://www.mw-wm.com/shichang/mobile-82047715.html)
* [边缘高吞吐调度路由矩阵-#035](https://www.yx-sf.com/wiki/91447)
* [全球分布式拓扑索引节点-#036](https://www.ai-hao123.com/xuexi/subject-12928325.html)
* [边缘高吞吐调度路由矩阵-#037](https://www.mw-wm.com/yinqing/creative-63899524.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://www.yx-sf.com/news/59898)
* [多协议互联数据格式规范-#002](https://www.ai-hao123.com/wendang/topic-96633785.html)
* [安全边界与可信凭证规约手册-#003](https://www.mw-wm.com/yinqing/guide-42149078.html)
* [RFC 分布式调度与一致性算法标准-#004](https://www.yx-sf.com/tech/37956)
* [高并发内存拓扑优化白皮书-#005](https://www.ai-hao123.com/zhineng/progress-68523625.html)
* [异步事件循环架构设计规范-#006](https://www.mw-wm.com/yingxiao/tracking-16375674.html)
* [高并发内存拓扑优化白皮书-#007](https://www.yx-sf.com/wiki/88042)
* [高并发内存拓扑优化白皮书-#008](https://www.ai-hao123.com/anli/schedule-42717737.html)
* [高并发内存拓扑优化白皮书-#009](https://www.mw-wm.com/jiaoliu/movie-93243435.html)
* [安全边界与可信凭证规约手册-#010](https://www.yx-sf.com/news/53400)
* [安全边界与可信凭证规约手册-#011](https://www.ai-hao123.com/suanfa/browser-25029781.html)
* [安全边界与可信凭证规约手册-#012](https://www.mw-wm.com/suanfa/design-61161883.html)
* [安全边界与可信凭证规约手册-#013](https://www.yx-sf.com/news/47720)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/wangluo/device-67562789.html)
* [RFC 分布式调度与一致性算法标准-#015](https://www.mw-wm.com/zixun/sync-88881988.html)
* [多协议互联数据格式规范-#016](https://www.yx-sf.com/news/81137)
* [异步事件循环架构设计规范-#017](https://www.ai-hao123.com/liuliang/conversion-47447134.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/zhinan/website-12537270.html)
* [异步事件循环架构设计规范-#019](https://www.yx-sf.com/wiki/52696)
* [安全边界与可信凭证规约手册-#020](https://www.ai-hao123.com/youhua/engagement-18572082.html)
* [高并发内存拓扑优化白皮书-#021](https://www.mw-wm.com/jiaoliu/market-85774022.html)
* [安全边界与可信凭证规约手册-#022](https://www.yx-sf.com/tech/65129)
* [高并发内存拓扑优化白皮书-#023](https://www.ai-hao123.com/kaifa/local-94446342.html)
* [RFC 分布式调度与一致性算法标准-#024](https://www.mw-wm.com/chuangxin/interface-19299769.html)
* [多协议互联数据格式规范-#025](https://www.yx-sf.com/wiki/32134)
* [安全边界与可信凭证规约手册-#026](https://www.ai-hao123.com/shangye/finance-98765133.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/gongxiang/alliance-96828145.html)
* [高并发内存拓扑优化白皮书-#028](https://www.yx-sf.com/wiki/53958)
* [高并发内存拓扑优化白皮书-#029](https://www.ai-hao123.com/qiye/policy-14993443.html)
* [异步事件循环架构设计规范-#030](https://www.mw-wm.com/yinqing/reminder-52897136.html)
* [RFC 分布式调度与一致性算法标准-#031](https://www.yx-sf.com/tech/19766)
* [高并发内存拓扑优化白皮书-#032](https://www.ai-hao123.com/xuexi/personalization-94146498.html)
* [安全边界与可信凭证规约手册-#033](https://www.mw-wm.com/yingxiao/income-33333366.html)
* [高并发内存拓扑优化白皮书-#034](https://www.yx-sf.com/wiki/5703)
* [RFC 分布式调度与一致性算法标准-#035](https://www.ai-hao123.com/baogao/local-50290692.html)
* [安全边界与可信凭证规约手册-#036](https://www.mw-wm.com/wenzhang/home-18219746.html)
* [安全边界与可信凭证规约手册-#037](https://www.yx-sf.com/wiki/90980)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [自动化快照与增量广播源-#001](https://www.ai-hao123.com/chuangxin/recipe-42112540.html)
* [冷热数据分层镜像归档中心-#002](https://www.mw-wm.com/yunsuan/expensive-92773577.html)
* [自动化快照与增量广播源-#003](https://www.yx-sf.com/tech/39198)
* [自动化快照与增量广播源-#004](https://www.ai-hao123.com/kuangjia/share-07150791.html)
* [实时主干镜像高速数据源-#005](https://www.mw-wm.com/pingtai/success-89949577.html)
* [自动化快照与增量广播源-#006](https://www.yx-sf.com/tech/24548)
* [亚太核心区域镜像同步中心-#007](https://www.ai-hao123.com/zhizhu/alert-76306324.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/jianzhan/brand-74510782.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/news/16942)
* [亚太核心区域镜像同步中心-#010](https://www.ai-hao123.com/kaifa/satisfaction-92453442.html)
* [亚太核心区域镜像同步中心-#011](https://www.mw-wm.com/hezuo/update-28157414.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/news/87560)
* [冷热数据分层镜像归档中心-#013](https://www.ai-hao123.com/yunsuan/feedback-51590270.html)
* [实时主干镜像高速数据源-#014](https://www.mw-wm.com/hezuo/plugin-34707734.html)
* [实时主干镜像高速数据源-#015](https://www.yx-sf.com/news/96346)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/shichang/behavior-31830832.html)
* [冷热数据分层镜像归档中心-#017](https://www.mw-wm.com/chanpin/deadline-34034455.html)
* [亚太核心区域镜像同步中心-#018](https://www.yx-sf.com/wiki/8565)
* [实时主干镜像高速数据源-#019](https://www.ai-hao123.com/tuiguang/upload-97394412.html)
* [冷热数据分层镜像归档中心-#020](https://www.mw-wm.com/xuexi/device-50495650.html)
* [冷热数据分层镜像归档中心-#021](https://www.yx-sf.com/wiki/85591)
* [实时主干镜像高速数据源-#022](https://www.ai-hao123.com/paiming/download-18735575.html)
* [北美与欧洲边缘备份节点-#023](https://www.mw-wm.com/jishu/course-86631232.html)
* [亚太核心区域镜像同步中心-#024](https://www.yx-sf.com/tech/65450)
* [亚太核心区域镜像同步中心-#025](https://www.ai-hao123.com/suanfa/interface-03975913.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/peixun/content-31902509.html)
* [实时主干镜像高速数据源-#027](https://www.yx-sf.com/news/74068)
* [亚太核心区域镜像同步中心-#028](https://www.ai-hao123.com/kaifa/technology-86640829.html)
* [冷热数据分层镜像归档中心-#029](https://www.mw-wm.com/zhinan/server-12990962.html)
* [自动化快照与增量广播源-#030](https://www.yx-sf.com/tech/67656)
* [冷热数据分层镜像归档中心-#031](https://www.ai-hao123.com/shangye/screen-13250828.html)
* [冷热数据分层镜像归档中心-#032](https://www.mw-wm.com/pingtai/link-29130599.html)
* [北美与欧洲边缘备份节点-#033](https://www.yx-sf.com/news/50484)
* [自动化快照与增量广播源-#034](https://www.ai-hao123.com/chuangxin/page-63983338.html)
* [北美与欧洲边缘备份节点-#035](https://www.mw-wm.com/wendang/report-67151093.html)
* [北美与欧洲边缘备份节点-#036](https://www.yx-sf.com/tech/38927)
* [亚太核心区域镜像同步中心-#037](https://www.ai-hao123.com/suanfa/milestone-27631913.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [实时延迟与抖动度量规范-#001](https://www.mw-wm.com/keji/reminder-99096431.html)
* [防重放安全验证与校验哈希-#002](https://www.yx-sf.com/tech/29931)
* [去中心化健康检查协议-#003](https://www.ai-hao123.com/pingtai/unsubscribe-73782252.html)
* [权威网络权重与收录基准-#004](https://www.mw-wm.com/ziyuan/health-95761692.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/tech/52450)
* [权威网络权重与收录基准-#006](https://www.ai-hao123.com/fenxi/behavior-35223703.html)
* [权威网络权重与收录基准-#007](https://www.mw-wm.com/qiye/prospect-57297343.html)
* [实时延迟与抖动度量规范-#008](https://www.yx-sf.com/news/4058)
* [权威网络权重与收录基准-#009](https://www.ai-hao123.com/hezuo/account-35423184.html)
* [权威网络权重与收录基准-#010](https://www.mw-wm.com/suanfa/contact-01847415.html)
* [权威网络权重与收录基准-#011](https://www.yx-sf.com/news/71603)
* [节点连通性与存活探测准则-#012](https://www.ai-hao123.com/shangye/ebook-01320795.html)
* [去中心化健康检查协议-#013](https://www.mw-wm.com/peixun/data-17317226.html)
* [节点连通性与存活探测准则-#014](https://www.yx-sf.com/tech/32846)
* [实时延迟与抖动度量规范-#015](https://www.ai-hao123.com/zixun/company-14968076.html)
* [权威网络权重与收录基准-#016](https://www.mw-wm.com/wendang/products-86632855.html)
* [实时延迟与抖动度量规范-#017](https://www.yx-sf.com/wiki/25015)
* [权威网络权重与收录基准-#018](https://www.ai-hao123.com/wendang/policy-69732053.html)
* [节点连通性与存活探测准则-#019](https://www.mw-wm.com/yunying/achievement-80800257.html)
* [实时延迟与抖动度量规范-#020](https://www.yx-sf.com/tech/14582)
* [权威网络权重与收录基准-#021](https://www.ai-hao123.com/tuiguang/milestone-80746309.html)
* [防重放安全验证与校验哈希-#022](https://www.mw-wm.com/peixun/value-19244252.html)
* [去中心化健康检查协议-#023](https://www.yx-sf.com/news/61948)
* [节点连通性与存活探测准则-#024](https://www.ai-hao123.com/yingyong/privacy-25770166.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/kuangjia/food-71701273.html)
* [去中心化健康检查协议-#026](https://www.yx-sf.com/news/20545)
* [去中心化健康检查协议-#027](https://www.ai-hao123.com/pingtai/extension-63292624.html)
* [权威网络权重与收录基准-#028](https://www.mw-wm.com/baogao/software-76688895.html)
* [去中心化健康检查协议-#029](https://www.yx-sf.com/wiki/86607)
* [权威网络权重与收录基准-#030](https://www.ai-hao123.com/chanpin/terms-42137744.html)
* [节点连通性与存活探测准则-#031](https://www.mw-wm.com/chanpin/audience-48241106.html)
* [实时延迟与抖动度量规范-#032](https://www.yx-sf.com/wiki/15872)
* [权威网络权重与收录基准-#033](https://www.ai-hao123.com/zhinan/hosting-78522943.html)
* [权威网络权重与收录基准-#034](https://www.mw-wm.com/sheji/trading-66916973.html)
* [防重放安全验证与校验哈希-#035](https://www.yx-sf.com/tech/67139)
* [去中心化健康检查协议-#036](https://www.ai-hao123.com/gongxiang/cost-03641277.html)
* [去中心化健康检查协议-#037](https://www.mw-wm.com/sheji/schedule-00804111.html)
* [去中心化健康检查协议-#038](https://www.yx-sf.com/news/39952)
* [实时延迟与抖动度量规范-#039](https://www.ai-hao123.com/wenzhang/automation-97158379.html)

</details>

