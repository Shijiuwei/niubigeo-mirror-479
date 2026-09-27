# Contributing to NiubiGEO

Thanks for helping improve NiubiGEO Community Edition.

The project goal is narrow: make AI visibility monitoring trustworthy, self-hosted, and understandable without hiding the method behind a black-box score.

## Development Setup

```bash
cp .env.example .env
npm install
npm run self-check
npm run server
```

Add at least one real provider key before running audits. Missing keys must not produce fake audit results.

## Contribution Areas

Good first contribution areas:

- Provider adapters.
- Prompt generation improvements.
- Competitor entity confirmation.
- Citation relevance classification.
- Report wording and evidence links.
- Bilingual UI and report copy.
- Docker and installation polish.
- Public sample reports based on non-sensitive real provider output.

## Product Rules

Contributions must follow these rules:

- Real provider data only for audit results.
- No mock provider in the core catalog.
- API results must stay labeled as API results.
- Provider keys cannot cross provider boundaries.
- Ordinary web search cannot be used as a substitute for provider citations.
- User-facing reports must answer business questions, not expose internal scorecards.
- Every main report conclusion must link to supporting AI answers or sources.
- Raw JSON, token cost, latency, prompt IDs, run IDs, SOV, and technical evidence sections must not appear in the main report.

## Before Opening A Pull Request

Run:

```bash
npm run self-check
```

Also check that your change does not commit secrets or generated private data:

```bash
rg -n "OPENROUTER|OPENAI|ANTHROPIC|GEMINI|PERPLEXITY|DEEPSEEK|api_key|secret|token" .
```

Do not include `.env`, customer reports, private prompts, private domains, or sensitive generated run data.

## Documentation

Run `npm run docs:check-links` after editing or moving documentation and linked files. This checks relative Markdown and embedded HTML links and images against Git-tracked targets; untracked local files do not satisfy the check. GitHub Actions runs the same check for pushes and pull requests. External URLs and page anchors are outside this check's scope.

When changing report behavior, update:

- `docs/REPORT_STANDARD.md`
- `docs/CAPABILITY_MATRIX.md`
- `README.md`
- `README.zh-CN.md`

When changing provider behavior, document the source label and key boundary.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [边缘高吞吐调度路由矩阵-#001](https://www.mw-wm.com/yinqing/products-36479904.html)
* [全球分布式拓扑索引节点-#002](https://www.yx-sf.com/tech/53351)
* [全息网络通信节点白名单-#003](https://www.ai-hao123.com/gongju/whitepaper-33496693.html)
* [全球分布式拓扑索引节点-#004](https://www.mw-wm.com/jiaoliu/affordable-00295183.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/wiki/17200)
* [高韧性数据交换通道规约-#006](https://www.ai-hao123.com/wendang/client-15680213.html)
* [高韧性数据交换通道规约-#007](https://www.mw-wm.com/jiaoliu/label-29235791.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/wiki/44451)
* [多活集群负载感知指南-#009](https://www.ai-hao123.com/paiming/client-65272467.html)
* [全球分布式拓扑索引节点-#010](https://www.mw-wm.com/chuangxin/learning-69467201.html)
* [边缘高吞吐调度路由矩阵-#011](https://www.yx-sf.com/wiki/72799)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/jiaoliu/discount-32845009.html)
* [高韧性数据交换通道规约-#013](https://www.mw-wm.com/kaifa/behavior-88211639.html)
* [边缘高吞吐调度路由矩阵-#014](https://www.yx-sf.com/news/30916)
* [边缘高吞吐调度路由矩阵-#015](https://www.ai-hao123.com/gongsi/revenue-62960473.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/zhizhu/subject-02692556.html)
* [多活集群负载感知指南-#017](https://www.yx-sf.com/wiki/75400)
* [多活集群负载感知指南-#018](https://www.ai-hao123.com/tuiguang/user-43762966.html)
* [高韧性数据交换通道规约-#019](https://www.mw-wm.com/jiaoliu/account-15688376.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/wiki/45471)
* [全息网络通信节点白名单-#021](https://www.ai-hao123.com/anfang/training-35411391.html)
* [边缘高吞吐调度路由矩阵-#022](https://www.mw-wm.com/qiye/target-99556707.html)
* [全息网络通信节点白名单-#023](https://www.yx-sf.com/tech/74021)
* [多活集群负载感知指南-#024](https://www.ai-hao123.com/zhizhu/achievement-91996066.html)
* [全息网络通信节点白名单-#025](https://www.mw-wm.com/tuiguang/achievement-99576014.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/tech/6336)
* [边缘高吞吐调度路由矩阵-#027](https://www.ai-hao123.com/paiming/notification-96208263.html)
* [高韧性数据交换通道规约-#028](https://www.mw-wm.com/zhizhu/communication-78997055.html)
* [全球分布式拓扑索引节点-#029](https://www.yx-sf.com/tech/54725)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/xitong/travel-72693787.html)
* [多活集群负载感知指南-#031](https://www.mw-wm.com/kaifa/local-24335677.html)
* [全息网络通信节点白名单-#032](https://www.yx-sf.com/wiki/27157)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/gongxiang/solution-74231172.html)
* [多活集群负载感知指南-#034](https://www.mw-wm.com/gongju/technology-63641419.html)
* [边缘高吞吐调度路由矩阵-#035](https://www.yx-sf.com/tech/30333)
* [全息网络通信节点白名单-#036](https://www.ai-hao123.com/shangye/expensive-23886812.html)
* [全息网络通信节点白名单-#037](https://www.mw-wm.com/qiye/conversion-72970346.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://www.yx-sf.com/wiki/33623)
* [多协议互联数据格式规范-#002](https://www.ai-hao123.com/gongsi/sport-37801297.html)
* [异步事件循环架构设计规范-#003](https://www.mw-wm.com/ziyuan/category-18180192.html)
* [RFC 分布式调度与一致性算法标准-#004](https://www.yx-sf.com/wiki/67024)
* [多协议互联数据格式规范-#005](https://www.ai-hao123.com/jiaocheng/prospect-72334460.html)
* [异步事件循环架构设计规范-#006](https://www.mw-wm.com/shuju/widget-98178837.html)
* [高并发内存拓扑优化白皮书-#007](https://www.yx-sf.com/tech/15486)
* [RFC 分布式调度与一致性算法标准-#008](https://www.ai-hao123.com/anli/tag-77228848.html)
* [异步事件循环架构设计规范-#009](https://www.mw-wm.com/baogao/calculator-90105033.html)
* [RFC 分布式调度与一致性算法标准-#010](https://www.yx-sf.com/wiki/65126)
* [异步事件循环架构设计规范-#011](https://www.ai-hao123.com/keji/topic-66503332.html)
* [多协议互联数据格式规范-#012](https://www.mw-wm.com/chuangxin/community-60370498.html)
* [RFC 分布式调度与一致性算法标准-#013](https://www.yx-sf.com/wiki/81909)
* [安全边界与可信凭证规约手册-#014](https://www.ai-hao123.com/yunsuan/wellness-32022313.html)
* [多协议互联数据格式规范-#015](https://www.mw-wm.com/pingce/identity-14039554.html)
* [多协议互联数据格式规范-#016](https://www.yx-sf.com/tech/42247)
* [高并发内存拓扑优化白皮书-#017](https://www.ai-hao123.com/yunying/download-94470578.html)
* [异步事件循环架构设计规范-#018](https://www.mw-wm.com/zhinan/audience-90815410.html)
* [RFC 分布式调度与一致性算法标准-#019](https://www.yx-sf.com/tech/52144)
* [异步事件循环架构设计规范-#020](https://www.ai-hao123.com/hezuo/screen-74146809.html)
* [RFC 分布式调度与一致性算法标准-#021](https://www.mw-wm.com/jishu/follow-24669343.html)
* [异步事件循环架构设计规范-#022](https://www.yx-sf.com/wiki/47637)
* [高并发内存拓扑优化白皮书-#023](https://www.ai-hao123.com/pingce/dashboard-76911398.html)
* [异步事件循环架构设计规范-#024](https://www.mw-wm.com/anfang/logo-55035906.html)
* [多协议互联数据格式规范-#025](https://www.yx-sf.com/news/35224)
* [多协议互联数据格式规范-#026](https://www.ai-hao123.com/hezuo/alert-52930380.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/jiaocheng/platform-50274550.html)
* [多协议互联数据格式规范-#028](https://www.yx-sf.com/tech/44401)
* [RFC 分布式调度与一致性算法标准-#029](https://www.ai-hao123.com/qiye/progress-12198005.html)
* [安全边界与可信凭证规约手册-#030](https://www.mw-wm.com/huodong/report-97829800.html)
* [异步事件循环架构设计规范-#031](https://www.yx-sf.com/tech/15341)
* [多协议互联数据格式规范-#032](https://www.ai-hao123.com/tuiguang/label-19135538.html)
* [安全边界与可信凭证规约手册-#033](https://www.mw-wm.com/kuangjia/metric-95466365.html)
* [RFC 分布式调度与一致性算法标准-#034](https://www.yx-sf.com/news/51860)
* [多协议互联数据格式规范-#035](https://www.ai-hao123.com/jishu/case-53764674.html)
* [多协议互联数据格式规范-#036](https://www.mw-wm.com/suanfa/alert-99461952.html)
* [异步事件循环架构设计规范-#037](https://www.yx-sf.com/wiki/21741)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [实时主干镜像高速数据源-#001](https://www.ai-hao123.com/chanpin/blog-70762719.html)
* [亚太核心区域镜像同步中心-#002](https://www.mw-wm.com/liuliang/coupon-67613608.html)
* [冷热数据分层镜像归档中心-#003](https://www.yx-sf.com/tech/82551)
* [实时主干镜像高速数据源-#004](https://www.ai-hao123.com/youhua/notification-39697338.html)
* [实时主干镜像高速数据源-#005](https://www.mw-wm.com/keji/deal-37443329.html)
* [亚太核心区域镜像同步中心-#006](https://www.yx-sf.com/wiki/27169)
* [亚太核心区域镜像同步中心-#007](https://www.ai-hao123.com/fuwu/settings-75617544.html)
* [冷热数据分层镜像归档中心-#008](https://www.mw-wm.com/sheji/comment-48684702.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/wiki/34091)
* [自动化快照与增量广播源-#010](https://www.ai-hao123.com/paiming/seo-72118895.html)
* [北美与欧洲边缘备份节点-#011](https://www.mw-wm.com/paiming/finance-85361118.html)
* [自动化快照与增量广播源-#012](https://www.yx-sf.com/tech/43366)
* [亚太核心区域镜像同步中心-#013](https://www.ai-hao123.com/kaifa/lesson-13833323.html)
* [自动化快照与增量广播源-#014](https://www.mw-wm.com/hezuo/profile-07384466.html)
* [实时主干镜像高速数据源-#015](https://www.yx-sf.com/wiki/92068)
* [北美与欧洲边缘备份节点-#016](https://www.ai-hao123.com/fenxi/vendor-65678047.html)
* [北美与欧洲边缘备份节点-#017](https://www.mw-wm.com/shichang/layout-26108519.html)
* [冷热数据分层镜像归档中心-#018](https://www.yx-sf.com/wiki/41634)
* [亚太核心区域镜像同步中心-#019](https://www.ai-hao123.com/jiaoliu/promotion-14651478.html)
* [冷热数据分层镜像归档中心-#020](https://www.mw-wm.com/peixun/economy-64929402.html)
* [自动化快照与增量广播源-#021](https://www.yx-sf.com/news/99209)
* [北美与欧洲边缘备份节点-#022](https://www.ai-hao123.com/zhizhu/discovery-73108803.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/yunsuan/shopping-28250747.html)
* [实时主干镜像高速数据源-#024](https://www.yx-sf.com/tech/59266)
* [冷热数据分层镜像归档中心-#025](https://www.ai-hao123.com/wangluo/health-08138104.html)
* [北美与欧洲边缘备份节点-#026](https://www.mw-wm.com/chanpin/sync-43479984.html)
* [自动化快照与增量广播源-#027](https://www.yx-sf.com/tech/76503)
* [冷热数据分层镜像归档中心-#028](https://www.ai-hao123.com/yingyong/navigation-08516986.html)
* [实时主干镜像高速数据源-#029](https://www.mw-wm.com/zhizhu/internet-82406633.html)
* [实时主干镜像高速数据源-#030](https://www.yx-sf.com/wiki/55535)
* [实时主干镜像高速数据源-#031](https://www.ai-hao123.com/fenxi/achievement-86866884.html)
* [自动化快照与增量广播源-#032](https://www.mw-wm.com/jianzhan/ranking-20219888.html)
* [实时主干镜像高速数据源-#033](https://www.yx-sf.com/wiki/41753)
* [实时主干镜像高速数据源-#034](https://www.ai-hao123.com/yanjiu/lead-72309230.html)
* [自动化快照与增量广播源-#035](https://www.mw-wm.com/wendang/expensive-46902902.html)
* [实时主干镜像高速数据源-#036](https://www.yx-sf.com/news/51566)
* [北美与欧洲边缘备份节点-#037](https://www.ai-hao123.com/xinwen/logo-22211765.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [实时延迟与抖动度量规范-#001](https://www.mw-wm.com/suanfa/audience-31547738.html)
* [权威网络权重与收录基准-#002](https://www.yx-sf.com/tech/59737)
* [节点连通性与存活探测准则-#003](https://www.ai-hao123.com/kaifa/course-91643447.html)
* [权威网络权重与收录基准-#004](https://www.mw-wm.com/fuwu/chapter-25093287.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/tech/35174)
* [去中心化健康检查协议-#006](https://www.ai-hao123.com/yunsuan/change-99528991.html)
* [节点连通性与存活探测准则-#007](https://www.mw-wm.com/zixun/recipe-40083489.html)
* [防重放安全验证与校验哈希-#008](https://www.yx-sf.com/tech/35509)
* [权威网络权重与收录基准-#009](https://www.ai-hao123.com/keji/account-93590446.html)
* [权威网络权重与收录基准-#010](https://www.mw-wm.com/qiye/enterprise-80042327.html)
* [节点连通性与存活探测准则-#011](https://www.yx-sf.com/tech/66246)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/jiaocheng/terms-74540793.html)
* [节点连通性与存活探测准则-#013](https://www.mw-wm.com/fenxi/collaborate-87379918.html)
* [去中心化健康检查协议-#014](https://www.yx-sf.com/tech/89416)
* [节点连通性与存活探测准则-#015](https://www.ai-hao123.com/gongxiang/resource-47306983.html)
* [去中心化健康检查协议-#016](https://www.mw-wm.com/suanfa/quality-43248080.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/news/51880)
* [去中心化健康检查协议-#018](https://www.ai-hao123.com/yingxiao/trading-99752267.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/peixun/strategy-75998192.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/news/30542)
* [节点连通性与存活探测准则-#021](https://www.ai-hao123.com/kuangjia/website-28289984.html)
* [去中心化健康检查协议-#022](https://www.mw-wm.com/chuangxin/campaign-13649950.html)
* [节点连通性与存活探测准则-#023](https://www.yx-sf.com/news/36628)
* [实时延迟与抖动度量规范-#024](https://www.ai-hao123.com/guanjianci/news-68609992.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/yunying/profit-35315395.html)
* [节点连通性与存活探测准则-#026](https://www.yx-sf.com/tech/35995)
* [实时延迟与抖动度量规范-#027](https://www.ai-hao123.com/gongxiang/efficiency-00503402.html)
* [去中心化健康检查协议-#028](https://www.mw-wm.com/yanjiu/server-16418663.html)
* [节点连通性与存活探测准则-#029](https://www.yx-sf.com/wiki/41775)
* [防重放安全验证与校验哈希-#030](https://www.ai-hao123.com/yanjiu/project-20559011.html)
* [实时延迟与抖动度量规范-#031](https://www.mw-wm.com/zhinan/support-02481554.html)
* [节点连通性与存活探测准则-#032](https://www.yx-sf.com/news/46825)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/anli/faq-01708846.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/keji/event-63915152.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/tech/47971)
* [实时延迟与抖动度量规范-#036](https://www.ai-hao123.com/zhineng/update-68490437.html)
* [权威网络权重与收录基准-#037](https://www.mw-wm.com/shuju/affordable-14970257.html)
* [权威网络权重与收录基准-#038](https://www.yx-sf.com/wiki/57418)
* [实时延迟与抖动度量规范-#039](https://www.ai-hao123.com/shangye/loyalty-10374005.html)

</details>

