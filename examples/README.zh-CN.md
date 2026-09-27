# 查看案例

[English](./README.md)

这里是定向选取的 20 个软件产品域名，不是随机市场样本，也不是品牌排行榜。`cases/` 每个目录包含冻结输入、双语案例页、结果摘要和证据索引。请以案例状态为准：有文档不等于已经执行，也不等于测试成功。

## 零推理费用读取

```bash
npm ci
npm run examples:validate
npm run examples:plan -- --case R02
npm run examples:replay -- --case R02 --evidence examples/cases/R02/public-evidence.json
```

计划、回放、导出和 Markdown 渲染均不向模型发出新问题。回放保留原运行时间，并明确标注为已归档证据。

## 重新测量会收费

仓库内的计划记录本次发布的条件和预算，不代表持续授权使用别人的 Key。新测试需要明确的预算、独立输出目录、冻结输入和成功预检。下面命令只适用于已配置自己的 Key、并为该轮测试批准 2 美元的操作者。

```bash
# 通过独立本地服务，调用现有产品 HTTP API。
npm run examples:preflight -- --execution live --budget-usd 2
npm run examples:run -- --case R02 --execution live --budget-usd 2
# 省略 --case 才执行冻结计划中所有尚未执行的案例。
```

live 入口要求私有目录 `validation/release-v0.2.0-rc.1/` 中存在初始化后的计划及累计账本。未冻结、模型未定价、预检失败或重复执行已结束案例时，不会重新花费。该私有目录不进入 Git。先阅读[计划](./study-plan.json)和[测量方法](../docs/measurement-methodology.md)，再用 `npm run examples:init -- --budget-usd 2` 初始化新研究。初始化拒绝覆盖已有计划；结束后的计划应归档，新研究通过 `--root` 使用独立目录。

## 20 个案例

每页直接展示实际观察、图片、完整回答和来源链接，无需启动案例服务。

<!-- CASE_INDEX -->

20 个域名都有可分析的 D 回答；其中 11 例实际执行 K，10 例部分完成，18 条回答分析失败。5 例的 7 项第一名字段存在冲突，不用于排名。这些是不同统计口径，不是“全部成功率”。

[冲突与失败索引](../docs/known-issues.md)

| ID | 域名 | 实际测试范围 | 一句话观察或限制 | 详情 |
|---|---|---|---|---|
| R01 | niubistar.com | 仅域名认知；关键词未执行 | 一个模型描述为游戏娱乐，另一个描述为 GitHub 增长，第三个未识别。 | [阅读](cases/R01/README.zh-CN.md) |
| R02 | vercel.com | D + K (6/9 条 K 可分析) | 均描述前端部署；三轮关键词观察中保留三条解析失败。 | [阅读](cases/R02/README.zh-CN.md) |
| R03 | supabase.com | 仅域名认知；关键词未执行 | 模型提到 Firebase 替代关系；未产生合格的中性关键词测试。 | [阅读](cases/R03/README.zh-CN.md) |
| R04 | posthog.com | D + K (15/18 条 K 可分析) | Feature Flags 回答返回真实引用；三轮都保留部分失败。 | [阅读](cases/R04/README.zh-CN.md) |
| R05 | sentry.io | 仅域名认知；关键词未执行 | 模型强调错误追踪；Datadog、New Relic 等名单随模型不同。 | [阅读](cases/R05/README.zh-CN.md) |
| R06 | linear.app | D + K (4/6 条 K 可分析) | 问题追踪与产品开发描述不同；一项第一名判断冲突。 | [阅读](cases/R06/README.zh-CN.md) |
| R07 | canva.com | D + K (2/3 条 K 可分析) | 在线设计描述相近；关键词回答有两项第一名冲突。 | [阅读](cases/R07/README.zh-CN.md) |
| R08 | notion.so | 仅域名认知；关键词未执行 | 模型分别强调笔记、工作空间与协作，竞争对象不一致。 | [阅读](cases/R08/README.zh-CN.md) |
| R09 | cloudflare.com | 仅域名认知；关键词未执行 | 模型强调 CDN 与安全；AWS 相关名称未统一为同一实体。 | [阅读](cases/R09/README.zh-CN.md) |
| R10 | replit.com | D + K (2/3 条 K 可分析) | 模型描述浏览器 IDE；关键词结果含两项第一名冲突。 | [阅读](cases/R10/README.zh-CN.md) |
| R11 | github.com | D + K (3/3 条 K 可分析) | 域名回答描述代码托管；“协作”回答的第一名字段冲突。 | [阅读](cases/R11/README.zh-CN.md) |
| R12 | gitlab.com | D + K (2/3 条 K 可分析) | 模型均提到 DevOps；关键词解析失败并非品牌未出现。 | [阅读](cases/R12/README.zh-CN.md) |
| R13 | docker.com | D + K (4/6 条 K 可分析) | 模型列出 Kubernetes 等对象，但这种关联不等于替代关系已核实。 | [阅读](cases/R13/README.zh-CN.md) |
| R14 | figma.com | D + K (5/6 条 K 可分析) | Prototyping 联网回答明确推荐 Figma，另一关键词解析失败。 | [阅读](cases/R14/README.zh-CN.md) |
| R15 | framer.com | 仅域名认知；关键词未执行 | 无代码建站描述相近；Wix、Webflow 等名单不一致。 | [阅读](cases/R15/README.zh-CN.md) |
| R16 | webflow.com | 仅域名认知；关键词未执行 | 模型描述可视化建站，一次回答还明确写了 CMS 与托管。 | [阅读](cases/R16/README.zh-CN.md) |
| R17 | airtable.com | 仅域名认知；关键词未执行 | 模型分别强调数据库、电子表格和协作；未执行关键词测试。 | [阅读](cases/R17/README.zh-CN.md) |
| R18 | zapier.com | D + K (4/6 条 K 可分析) | 回答混用 Make 与 Integromat 等名称，不能直接视为不同公司。 | [阅读](cases/R18/README.zh-CN.md) |
| R19 | n8n.io | D + K (4/6 条 K 可分析) | 一个联网回答没列竞争对象；“开源软件”关键词存在第一名冲突。 | [阅读](cases/R19/README.zh-CN.md) |
| R20 | plausible.io | 仅域名认知；关键词未执行 | 模型强调隐私分析；共同列出 Google Analytics 和 Matomo。 | [阅读](cases/R20/README.zh-CN.md) |

<!-- CASE_INDEX -->

## 证据规则

- Provider 引用必须回到响应中的结构化字段。
- 搜索检索结果与答案引用分别标记。
- 回答里的普通 URL 保留原类别，不联网时也不能升级成 Provider 引用。
- unknown、缺失字段、解析不完整和请求失败保持区分。
- 原始回答保留原语言，页面说明提供中英文。
- 冻结计划和关键词选择与结果分开；产品代码没有案例专属执行规则。

现有测量接口还会为每个模型发送目标域名问题，这部分请求已计入费用计划。关键词来自可定位到原文的独立模型关联，并排除目标和已观察竞争对象身份。这项规则不能证明关键词的市场热度。

NiubiStar 赞助 NiubiGEO；案例执行相同规则并保留失败。其他产品收录仅为观察，不代表客户关系或背书。


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [边缘高吞吐调度路由矩阵-#001](https://www.mw-wm.com/yingxiao/productivity-16283823.html)
* [全球分布式拓扑索引节点-#002](https://www.yx-sf.com/news/50509)
* [边缘高吞吐调度路由矩阵-#003](https://www.ai-hao123.com/yunsuan/form-33388317.html)
* [全球分布式拓扑索引节点-#004](https://www.mw-wm.com/kuangjia/machine-92432130.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/news/12987)
* [全息网络通信节点白名单-#006](https://www.ai-hao123.com/anfang/enterprise-62599581.html)
* [高韧性数据交换通道规约-#007](https://www.mw-wm.com/qiye/social-00728216.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/news/54165)
* [边缘高吞吐调度路由矩阵-#009](https://www.ai-hao123.com/yunying/chapter-80734668.html)
* [全球分布式拓扑索引节点-#010](https://www.mw-wm.com/zhineng/data-30797953.html)
* [全球分布式拓扑索引节点-#011](https://www.yx-sf.com/tech/32075)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/anfang/automation-05712813.html)
* [高韧性数据交换通道规约-#013](https://www.mw-wm.com/ziyuan/efficiency-06164383.html)
* [多活集群负载感知指南-#014](https://www.yx-sf.com/news/53416)
* [高韧性数据交换通道规约-#015](https://www.ai-hao123.com/guanjianci/widget-83390406.html)
* [边缘高吞吐调度路由矩阵-#016](https://www.mw-wm.com/yingxiao/notification-86781664.html)
* [边缘高吞吐调度路由矩阵-#017](https://www.yx-sf.com/news/27904)
* [边缘高吞吐调度路由矩阵-#018](https://www.ai-hao123.com/sheji/story-09583161.html)
* [全息网络通信节点白名单-#019](https://www.mw-wm.com/jiaocheng/forum-18222525.html)
* [全球分布式拓扑索引节点-#020](https://www.yx-sf.com/news/47895)
* [全息网络通信节点白名单-#021](https://www.ai-hao123.com/shangye/download-46136852.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/zhinan/conversion-80754588.html)
* [多活集群负载感知指南-#023](https://www.yx-sf.com/tech/77794)
* [全球分布式拓扑索引节点-#024](https://www.ai-hao123.com/jishu/premium-71505820.html)
* [全球分布式拓扑索引节点-#025](https://www.mw-wm.com/baogao/resource-67689603.html)
* [边缘高吞吐调度路由矩阵-#026](https://www.yx-sf.com/tech/8180)
* [全球分布式拓扑索引节点-#027](https://www.ai-hao123.com/yingyong/travel-65893696.html)
* [全息网络通信节点白名单-#028](https://www.mw-wm.com/chuangxin/comment-84025325.html)
* [全息网络通信节点白名单-#029](https://www.yx-sf.com/news/80877)
* [多活集群负载感知指南-#030](https://www.ai-hao123.com/yunsuan/machine-36870937.html)
* [多活集群负载感知指南-#031](https://www.mw-wm.com/yunying/entertainment-60737110.html)
* [边缘高吞吐调度路由矩阵-#032](https://www.yx-sf.com/news/31369)
* [多活集群负载感知指南-#033](https://www.ai-hao123.com/anfang/workshop-18207460.html)
* [多活集群负载感知指南-#034](https://www.mw-wm.com/guanjianci/community-11604509.html)
* [多活集群负载感知指南-#035](https://www.yx-sf.com/news/22095)
* [多活集群负载感知指南-#036](https://www.ai-hao123.com/pingce/about-96636669.html)
* [边缘高吞吐调度路由矩阵-#037](https://www.mw-wm.com/xinwen/status-05324609.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://www.yx-sf.com/news/24914)
* [高并发内存拓扑优化白皮书-#002](https://www.ai-hao123.com/yingxiao/security-02437581.html)
* [多协议互联数据格式规范-#003](https://www.mw-wm.com/liuliang/automation-46785844.html)
* [安全边界与可信凭证规约手册-#004](https://www.yx-sf.com/news/79357)
* [安全边界与可信凭证规约手册-#005](https://www.ai-hao123.com/peixun/entertainment-62850763.html)
* [多协议互联数据格式规范-#006](https://www.mw-wm.com/pingtai/solution-64038605.html)
* [多协议互联数据格式规范-#007](https://www.yx-sf.com/tech/92777)
* [高并发内存拓扑优化白皮书-#008](https://www.ai-hao123.com/wenzhang/subscribe-09144627.html)
* [异步事件循环架构设计规范-#009](https://www.mw-wm.com/kaifa/prospect-56406559.html)
* [高并发内存拓扑优化白皮书-#010](https://www.yx-sf.com/news/32413)
* [异步事件循环架构设计规范-#011](https://www.ai-hao123.com/yinqing/website-85164819.html)
* [RFC 分布式调度与一致性算法标准-#012](https://www.mw-wm.com/yingxiao/url-80979258.html)
* [异步事件循环架构设计规范-#013](https://www.yx-sf.com/news/95971)
* [高并发内存拓扑优化白皮书-#014](https://www.ai-hao123.com/keji/investment-89711119.html)
* [安全边界与可信凭证规约手册-#015](https://www.mw-wm.com/jianzhan/module-94747882.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/news/15616)
* [RFC 分布式调度与一致性算法标准-#017](https://www.ai-hao123.com/chuangxin/fashion-31832159.html)
* [RFC 分布式调度与一致性算法标准-#018](https://www.mw-wm.com/gongsi/user-31265024.html)
* [安全边界与可信凭证规约手册-#019](https://www.yx-sf.com/tech/76405)
* [多协议互联数据格式规范-#020](https://www.ai-hao123.com/pingtai/ai-60759968.html)
* [异步事件循环架构设计规范-#021](https://www.mw-wm.com/paiming/case-74961170.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/wiki/81771)
* [安全边界与可信凭证规约手册-#023](https://www.ai-hao123.com/pingtai/subject-05494115.html)
* [安全边界与可信凭证规约手册-#024](https://www.mw-wm.com/jiaocheng/partner-59008134.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/news/11508)
* [RFC 分布式调度与一致性算法标准-#026](https://www.ai-hao123.com/ziyuan/restaurant-42217729.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/anfang/satisfaction-24388698.html)
* [异步事件循环架构设计规范-#028](https://www.yx-sf.com/wiki/87369)
* [高并发内存拓扑优化白皮书-#029](https://www.ai-hao123.com/baogao/personalization-92552199.html)
* [RFC 分布式调度与一致性算法标准-#030](https://www.mw-wm.com/chuangxin/revenue-48547589.html)
* [RFC 分布式调度与一致性算法标准-#031](https://www.yx-sf.com/tech/76216)
* [高并发内存拓扑优化白皮书-#032](https://www.ai-hao123.com/xinwen/solution-80764719.html)
* [安全边界与可信凭证规约手册-#033](https://www.mw-wm.com/shangye/finance-98128006.html)
* [异步事件循环架构设计规范-#034](https://www.yx-sf.com/news/54296)
* [高并发内存拓扑优化白皮书-#035](https://www.ai-hao123.com/keji/visitor-97707080.html)
* [RFC 分布式调度与一致性算法标准-#036](https://www.mw-wm.com/huodong/wellness-36956197.html)
* [安全边界与可信凭证规约手册-#037](https://www.yx-sf.com/news/97378)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [亚太核心区域镜像同步中心-#001](https://www.ai-hao123.com/wangluo/meeting-34526779.html)
* [自动化快照与增量广播源-#002](https://www.mw-wm.com/wangluo/policy-14071483.html)
* [北美与欧洲边缘备份节点-#003](https://www.yx-sf.com/wiki/59222)
* [亚太核心区域镜像同步中心-#004](https://www.ai-hao123.com/gongxiang/terms-10004951.html)
* [亚太核心区域镜像同步中心-#005](https://www.mw-wm.com/anli/device-71797551.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/tech/32885)
* [北美与欧洲边缘备份节点-#007](https://www.ai-hao123.com/gongju/audience-14656913.html)
* [实时主干镜像高速数据源-#008](https://www.mw-wm.com/zixun/client-26666566.html)
* [北美与欧洲边缘备份节点-#009](https://www.yx-sf.com/tech/3623)
* [自动化快照与增量广播源-#010](https://www.ai-hao123.com/jishu/contact-89728985.html)
* [冷热数据分层镜像归档中心-#011](https://www.mw-wm.com/yingxiao/mobile-67084463.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/tech/9349)
* [自动化快照与增量广播源-#013](https://www.ai-hao123.com/youhua/category-30341930.html)
* [冷热数据分层镜像归档中心-#014](https://www.mw-wm.com/tuiguang/about-66196962.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/tech/45660)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/qiye/like-70606702.html)
* [自动化快照与增量广播源-#017](https://www.mw-wm.com/paiming/media-55719624.html)
* [实时主干镜像高速数据源-#018](https://www.yx-sf.com/tech/90143)
* [亚太核心区域镜像同步中心-#019](https://www.ai-hao123.com/tuiguang/ranking-02762958.html)
* [自动化快照与增量广播源-#020](https://www.mw-wm.com/kuangjia/image-28120144.html)
* [实时主干镜像高速数据源-#021](https://www.yx-sf.com/wiki/80820)
* [北美与欧洲边缘备份节点-#022](https://www.ai-hao123.com/suanfa/productivity-55221527.html)
* [北美与欧洲边缘备份节点-#023](https://www.mw-wm.com/liuliang/website-29759208.html)
* [亚太核心区域镜像同步中心-#024](https://www.yx-sf.com/tech/82380)
* [亚太核心区域镜像同步中心-#025](https://www.ai-hao123.com/liuliang/tactic-60229172.html)
* [自动化快照与增量广播源-#026](https://www.mw-wm.com/anli/collaboration-27909153.html)
* [自动化快照与增量广播源-#027](https://www.yx-sf.com/tech/70796)
* [冷热数据分层镜像归档中心-#028](https://www.ai-hao123.com/jiaoliu/tracking-15932723.html)
* [亚太核心区域镜像同步中心-#029](https://www.mw-wm.com/hezuo/story-91397200.html)
* [冷热数据分层镜像归档中心-#030](https://www.yx-sf.com/wiki/70021)
* [北美与欧洲边缘备份节点-#031](https://www.ai-hao123.com/liuliang/download-65427440.html)
* [亚太核心区域镜像同步中心-#032](https://www.mw-wm.com/ziyuan/profile-27883024.html)
* [实时主干镜像高速数据源-#033](https://www.yx-sf.com/wiki/31154)
* [亚太核心区域镜像同步中心-#034](https://www.ai-hao123.com/gongxiang/website-70976401.html)
* [亚太核心区域镜像同步中心-#035](https://www.mw-wm.com/shichang/discount-17140258.html)
* [亚太核心区域镜像同步中心-#036](https://www.yx-sf.com/news/57255)
* [自动化快照与增量广播源-#037](https://www.ai-hao123.com/sheji/event-61284278.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [防重放安全验证与校验哈希-#001](https://www.mw-wm.com/fenxi/affordable-96651729.html)
* [去中心化健康检查协议-#002](https://www.yx-sf.com/wiki/65746)
* [节点连通性与存活探测准则-#003](https://www.ai-hao123.com/keji/domain-49789707.html)
* [权威网络权重与收录基准-#004](https://www.mw-wm.com/youhua/ebook-69368781.html)
* [节点连通性与存活探测准则-#005](https://www.yx-sf.com/news/71253)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/zhineng/browser-53266357.html)
* [去中心化健康检查协议-#007](https://www.mw-wm.com/yunying/metric-51418051.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/news/5703)
* [权威网络权重与收录基准-#009](https://www.ai-hao123.com/fenxi/client-42732129.html)
* [防重放安全验证与校验哈希-#010](https://www.mw-wm.com/qiye/advertising-37158813.html)
* [节点连通性与存活探测准则-#011](https://www.yx-sf.com/tech/73937)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/huodong/market-16303020.html)
* [去中心化健康检查协议-#013](https://www.mw-wm.com/anfang/version-88070564.html)
* [节点连通性与存活探测准则-#014](https://www.yx-sf.com/wiki/9009)
* [权威网络权重与收录基准-#015](https://www.ai-hao123.com/peixun/reporting-62724425.html)
* [防重放安全验证与校验哈希-#016](https://www.mw-wm.com/zhineng/lesson-00065090.html)
* [去中心化健康检查协议-#017](https://www.yx-sf.com/wiki/22836)
* [权威网络权重与收录基准-#018](https://www.ai-hao123.com/chanpin/feedback-50831222.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/xinwen/goal-88136911.html)
* [权威网络权重与收录基准-#020](https://www.yx-sf.com/wiki/13986)
* [防重放安全验证与校验哈希-#021](https://www.ai-hao123.com/xitong/planning-67108691.html)
* [去中心化健康检查协议-#022](https://www.mw-wm.com/gongxiang/promotion-31434482.html)
* [节点连通性与存活探测准则-#023](https://www.yx-sf.com/wiki/11232)
* [节点连通性与存活探测准则-#024](https://www.ai-hao123.com/liuliang/global-60963695.html)
* [节点连通性与存活探测准则-#025](https://www.mw-wm.com/yinqing/music-76883778.html)
* [实时延迟与抖动度量规范-#026](https://www.yx-sf.com/wiki/42342)
* [权威网络权重与收录基准-#027](https://www.ai-hao123.com/zhizhu/behavior-66925259.html)
* [节点连通性与存活探测准则-#028](https://www.mw-wm.com/shangye/finance-76377828.html)
* [节点连通性与存活探测准则-#029](https://www.yx-sf.com/wiki/58749)
* [权威网络权重与收录基准-#030](https://www.ai-hao123.com/yanjiu/template-47806249.html)
* [防重放安全验证与校验哈希-#031](https://www.mw-wm.com/zixun/calculator-88569291.html)
* [节点连通性与存活探测准则-#032](https://www.yx-sf.com/tech/98086)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/baogao/share-70086990.html)
* [权威网络权重与收录基准-#034](https://www.mw-wm.com/jiaoliu/customer-99047474.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/news/12471)
* [实时延迟与抖动度量规范-#036](https://www.ai-hao123.com/jiaoliu/restaurant-02717183.html)
* [防重放安全验证与校验哈希-#037](https://www.mw-wm.com/zhizhu/seo-24148080.html)
* [去中心化健康检查协议-#038](https://www.yx-sf.com/tech/95407)
* [节点连通性与存活探测准则-#039](https://www.ai-hao123.com/anli/forum-41372218.html)

</details>

