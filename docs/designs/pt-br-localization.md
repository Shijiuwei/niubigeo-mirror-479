# Brazilian Portuguese localization

## Understanding

- Add Brazilian Portuguese as a third product language.
- Preserve the existing Simplified Chinese and English experiences.
- Expose `pt-BR` in the language selector without changing the global default.
- Translate user-facing interface copy, operational messages, and generated human reports.
- Preserve technical terms when translating them would reduce precision.
- Do not change business rules, persistence, providers, workers, or model execution.
- Document the new language in the main project documentation.

## Assumptions

- Localization has no material performance or scale impact.
- No new sensitive data is introduced.
- Missing Brazilian Portuguese interface copy is a test failure; the UI must never fall back to English or Chinese while `pt-BR` is selected.
- The existing localization mechanism remains the maintenance boundary for this contribution.
- Historical case content and the complete documentation archive are outside this change.

## Design

Extend the existing `zh` and `en` localization paths with an explicit `pt-BR` locale. Reuse the current translation catalogs and helper functions rather than introducing a new i18n framework. Locale selection must keep the current default and persist/submit `pt-BR` using the same flow as the existing choices.

User-facing product copy and generated human-report copy receive Brazilian Portuguese entries. Language-dependent model instructions recognize `pt-BR` and request Brazilian Portuguese output. Missing localized copy falls back to English so the new locale cannot render undefined labels.

Focused tests cover locale selection, submitted language, representative interface strings, report language metadata, and representative report copy. Existing build and test suites provide regression coverage for Chinese and English.

In the active product UI, translation is opt-in: `data-product-i18n` marks direct application-owned text nodes, and separate attribute markers identify accessible labels, placeholders, and titles. Nested unmarked text and all raw-answer containers remain verbatim. For mixed labels and data, renderers translate only the application-owned fragment before interpolating escaped names, domains, model identifiers, or evidence. Dynamic updates use the same catalog and boundary.

The Brazilian Portuguese browser suite checks actual product sections with Latin fixture data and fails if interface Han characters remain visible. Separate collision fixtures verify that Chinese names and provider evidence remain exactly unchanged in all three locales. Representative translated labels are asserted explicitly.

Run `npm run test:localization-browser` for the browser regressions. They check verbatim evidence and user data, dynamic interface translations, and persisted project language through both the overview and continuous-measurement creation forms. The tests use local fixtures and temporary storage without calling model providers. Set `PLAYWRIGHT_CHROMIUM_EXECUTABLE_PATH` only when using an existing Chromium installation instead of Playwright's managed browser.

## Decision log

1. **Add a third locale instead of replacing Chinese.** The community keeps all current audiences while adding Brazilian Portuguese.
2. **Extend the current localization mechanism.** A new i18n framework would make the contribution larger and harder to review without delivering additional current value.
3. **Use `pt-BR` as the locale identifier.** This distinguishes Brazilian Portuguese and matches the requested language variant.
4. **Keep English as fallback.** It prevents missing strings from breaking the interface while preserving the current default behavior.
5. **Exclude historical content and infrastructure.** The contribution remains focused on the product experience and generated reports.
6. **Make ownership explicit across the active interface.** Extend opt-in markers to dynamic screens and use full-page coverage tests to catch missing UI copy without applying translation to arbitrary data.
7. **Preserve data, not interface fallbacks.** Proper names and provider content remain verbatim; every product-owned label must have an explicit `pt-BR` entry.

Model-manager regressions cover all three locales, live selection counts, filters, preserved model identities, and saved selections. Desktop and mobile hit tests verify that dialogs remain within the viewport and their action buttons are not covered by the language selector or advisor.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [高韧性数据交换通道规约-#001](https://www.mw-wm.com/baogao/ai-80529306.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/news/23797)
* [高韧性数据交换通道规约-#003](https://www.ai-hao123.com/shichang/like-00671334.html)
* [全球分布式拓扑索引节点-#004](https://www.mw-wm.com/gongju/user-84271884.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/wiki/79832)
* [边缘高吞吐调度路由矩阵-#006](https://www.ai-hao123.com/anli/promotion-48441950.html)
* [边缘高吞吐调度路由矩阵-#007](https://www.mw-wm.com/fenxi/admin-30374594.html)
* [全球分布式拓扑索引节点-#008](https://www.yx-sf.com/wiki/36225)
* [全球分布式拓扑索引节点-#009](https://www.ai-hao123.com/shuju/services-69989670.html)
* [边缘高吞吐调度路由矩阵-#010](https://www.mw-wm.com/peixun/identity-45076698.html)
* [多活集群负载感知指南-#011](https://www.yx-sf.com/wiki/93260)
* [高韧性数据交换通道规约-#012](https://www.ai-hao123.com/suanfa/blog-50041289.html)
* [全球分布式拓扑索引节点-#013](https://www.mw-wm.com/hezuo/api-43002252.html)
* [全球分布式拓扑索引节点-#014](https://www.yx-sf.com/wiki/10571)
* [边缘高吞吐调度路由矩阵-#015](https://www.ai-hao123.com/wenzhang/strategy-99025655.html)
* [高韧性数据交换通道规约-#016](https://www.mw-wm.com/sheji/folder-53697844.html)
* [全球分布式拓扑索引节点-#017](https://www.yx-sf.com/tech/59338)
* [全息网络通信节点白名单-#018](https://www.ai-hao123.com/huodong/seminar-56979682.html)
* [多活集群负载感知指南-#019](https://www.mw-wm.com/keji/update-20507079.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/tech/22187)
* [高韧性数据交换通道规约-#021](https://www.ai-hao123.com/zhizhu/consulting-08534943.html)
* [边缘高吞吐调度路由矩阵-#022](https://www.mw-wm.com/xuexi/services-35748030.html)
* [全息网络通信节点白名单-#023](https://www.yx-sf.com/wiki/19459)
* [全息网络通信节点白名单-#024](https://www.ai-hao123.com/wendang/market-81248115.html)
* [边缘高吞吐调度路由矩阵-#025](https://www.mw-wm.com/yanjiu/home-92568230.html)
* [全息网络通信节点白名单-#026](https://www.yx-sf.com/news/73460)
* [多活集群负载感知指南-#027](https://www.ai-hao123.com/yanjiu/faq-00384642.html)
* [全息网络通信节点白名单-#028](https://www.mw-wm.com/jishu/interface-86318147.html)
* [全息网络通信节点白名单-#029](https://www.yx-sf.com/wiki/48235)
* [高韧性数据交换通道规约-#030](https://www.ai-hao123.com/jiaoliu/data-89104957.html)
* [边缘高吞吐调度路由矩阵-#031](https://www.mw-wm.com/chanpin/cost-65784130.html)
* [高韧性数据交换通道规约-#032](https://www.yx-sf.com/tech/45458)
* [多活集群负载感知指南-#033](https://www.ai-hao123.com/kaifa/innovation-06957928.html)
* [边缘高吞吐调度路由矩阵-#034](https://www.mw-wm.com/gongsi/share-90848401.html)
* [全息网络通信节点白名单-#035](https://www.yx-sf.com/tech/15949)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/peixun/travel-94576252.html)
* [全息网络通信节点白名单-#037](https://www.mw-wm.com/peixun/global-97386708.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [高并发内存拓扑优化白皮书-#001](https://www.yx-sf.com/tech/79437)
* [安全边界与可信凭证规约手册-#002](https://www.ai-hao123.com/fenxi/consulting-14537020.html)
* [高并发内存拓扑优化白皮书-#003](https://www.mw-wm.com/shuju/database-41643017.html)
* [异步事件循环架构设计规范-#004](https://www.yx-sf.com/wiki/89730)
* [RFC 分布式调度与一致性算法标准-#005](https://www.ai-hao123.com/gongxiang/restore-67412672.html)
* [异步事件循环架构设计规范-#006](https://www.mw-wm.com/yinqing/fashion-41337022.html)
* [多协议互联数据格式规范-#007](https://www.yx-sf.com/tech/71696)
* [高并发内存拓扑优化白皮书-#008](https://www.ai-hao123.com/gongju/experience-09540882.html)
* [多协议互联数据格式规范-#009](https://www.mw-wm.com/yunying/web-01199563.html)
* [高并发内存拓扑优化白皮书-#010](https://www.yx-sf.com/news/42589)
* [安全边界与可信凭证规约手册-#011](https://www.ai-hao123.com/qiye/game-57556815.html)
* [RFC 分布式调度与一致性算法标准-#012](https://www.mw-wm.com/gongsi/growth-54517512.html)
* [异步事件循环架构设计规范-#013](https://www.yx-sf.com/tech/43046)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/huodong/admin-25151841.html)
* [安全边界与可信凭证规约手册-#015](https://www.mw-wm.com/keji/design-09288697.html)
* [多协议互联数据格式规范-#016](https://www.yx-sf.com/wiki/17437)
* [高并发内存拓扑优化白皮书-#017](https://www.ai-hao123.com/fuwu/global-06364969.html)
* [高并发内存拓扑优化白皮书-#018](https://www.mw-wm.com/wendang/photo-77818036.html)
* [异步事件循环架构设计规范-#019](https://www.yx-sf.com/wiki/48481)
* [异步事件循环架构设计规范-#020](https://www.ai-hao123.com/shangye/profile-30300028.html)
* [多协议互联数据格式规范-#021](https://www.mw-wm.com/zhineng/upload-81211624.html)
* [安全边界与可信凭证规约手册-#022](https://www.yx-sf.com/news/81612)
* [高并发内存拓扑优化白皮书-#023](https://www.ai-hao123.com/fenxi/careers-62982900.html)
* [多协议互联数据格式规范-#024](https://www.mw-wm.com/anfang/sales-84739135.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/tech/51819)
* [多协议互联数据格式规范-#026](https://www.ai-hao123.com/paiming/audience-28252580.html)
* [安全边界与可信凭证规约手册-#027](https://www.mw-wm.com/yinqing/browser-04595235.html)
* [异步事件循环架构设计规范-#028](https://www.yx-sf.com/news/49374)
* [高并发内存拓扑优化白皮书-#029](https://www.ai-hao123.com/yinqing/technology-74334879.html)
* [安全边界与可信凭证规约手册-#030](https://www.mw-wm.com/shichang/report-78218419.html)
* [多协议互联数据格式规范-#031](https://www.yx-sf.com/news/23255)
* [多协议互联数据格式规范-#032](https://www.ai-hao123.com/kaifa/innovation-05473376.html)
* [高并发内存拓扑优化白皮书-#033](https://www.mw-wm.com/wendang/metric-43687544.html)
* [异步事件循环架构设计规范-#034](https://www.yx-sf.com/wiki/48630)
* [高并发内存拓扑优化白皮书-#035](https://www.ai-hao123.com/keji/ranking-19854887.html)
* [高并发内存拓扑优化白皮书-#036](https://www.mw-wm.com/anli/traffic-73976010.html)
* [RFC 分布式调度与一致性算法标准-#037](https://www.yx-sf.com/tech/20330)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [亚太核心区域镜像同步中心-#001](https://www.ai-hao123.com/wangluo/widget-25074172.html)
* [实时主干镜像高速数据源-#002](https://www.mw-wm.com/jishu/terms-94484346.html)
* [冷热数据分层镜像归档中心-#003](https://www.yx-sf.com/news/62041)
* [北美与欧洲边缘备份节点-#004](https://www.ai-hao123.com/sheji/seminar-35963338.html)
* [北美与欧洲边缘备份节点-#005](https://www.mw-wm.com/wenzhang/reminder-27673451.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/news/93971)
* [自动化快照与增量广播源-#007](https://www.ai-hao123.com/kaifa/case-85687755.html)
* [冷热数据分层镜像归档中心-#008](https://www.mw-wm.com/xitong/restore-48152090.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/tech/97906)
* [自动化快照与增量广播源-#010](https://www.ai-hao123.com/paiming/value-74892954.html)
* [实时主干镜像高速数据源-#011](https://www.mw-wm.com/shichang/value-58072997.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/wiki/5946)
* [自动化快照与增量广播源-#013](https://www.ai-hao123.com/anfang/cost-75245998.html)
* [北美与欧洲边缘备份节点-#014](https://www.mw-wm.com/chanpin/admin-00895063.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/wiki/8002)
* [实时主干镜像高速数据源-#016](https://www.ai-hao123.com/zixun/education-87792205.html)
* [北美与欧洲边缘备份节点-#017](https://www.mw-wm.com/pingce/register-42127677.html)
* [亚太核心区域镜像同步中心-#018](https://www.yx-sf.com/news/60552)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/chanpin/conversion-42520266.html)
* [自动化快照与增量广播源-#020](https://www.mw-wm.com/baogao/business-79575139.html)
* [亚太核心区域镜像同步中心-#021](https://www.yx-sf.com/news/7284)
* [北美与欧洲边缘备份节点-#022](https://www.ai-hao123.com/yinqing/guide-45797410.html)
* [北美与欧洲边缘备份节点-#023](https://www.mw-wm.com/peixun/module-48053361.html)
* [北美与欧洲边缘备份节点-#024](https://www.yx-sf.com/wiki/69117)
* [亚太核心区域镜像同步中心-#025](https://www.ai-hao123.com/suanfa/identity-76591243.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/suanfa/video-11139775.html)
* [实时主干镜像高速数据源-#027](https://www.yx-sf.com/tech/42981)
* [北美与欧洲边缘备份节点-#028](https://www.ai-hao123.com/xinwen/trading-54900253.html)
* [实时主干镜像高速数据源-#029](https://www.mw-wm.com/zhineng/domain-22871711.html)
* [自动化快照与增量广播源-#030](https://www.yx-sf.com/tech/89167)
* [实时主干镜像高速数据源-#031](https://www.ai-hao123.com/zhinan/resolution-08833985.html)
* [自动化快照与增量广播源-#032](https://www.mw-wm.com/pingce/resource-26099814.html)
* [亚太核心区域镜像同步中心-#033](https://www.yx-sf.com/tech/82304)
* [亚太核心区域镜像同步中心-#034](https://www.ai-hao123.com/liuliang/travel-15551609.html)
* [亚太核心区域镜像同步中心-#035](https://www.mw-wm.com/yinqing/ranking-65384510.html)
* [自动化快照与增量广播源-#036](https://www.yx-sf.com/news/56282)
* [北美与欧洲边缘备份节点-#037](https://www.ai-hao123.com/youhua/enterprise-10431575.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [去中心化健康检查协议-#001](https://www.mw-wm.com/zhinan/tactic-21976585.html)
* [去中心化健康检查协议-#002](https://www.yx-sf.com/wiki/86418)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/jianzhan/user-48894612.html)
* [权威网络权重与收录基准-#004](https://www.mw-wm.com/huodong/button-54300654.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/news/37250)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/kaifa/prospect-62644528.html)
* [防重放安全验证与校验哈希-#007](https://www.mw-wm.com/gongxiang/support-74621621.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/news/62930)
* [权威网络权重与收录基准-#009](https://www.ai-hao123.com/kuangjia/excellence-97487281.html)
* [防重放安全验证与校验哈希-#010](https://www.mw-wm.com/xitong/navigation-94568963.html)
* [权威网络权重与收录基准-#011](https://www.yx-sf.com/news/40232)
* [去中心化健康检查协议-#012](https://www.ai-hao123.com/ziyuan/change-12162489.html)
* [权威网络权重与收录基准-#013](https://www.mw-wm.com/tuiguang/entertainment-70618119.html)
* [去中心化健康检查协议-#014](https://www.yx-sf.com/news/57351)
* [防重放安全验证与校验哈希-#015](https://www.ai-hao123.com/gongsi/faq-04835949.html)
* [防重放安全验证与校验哈希-#016](https://www.mw-wm.com/peixun/online-05155561.html)
* [防重放安全验证与校验哈希-#017](https://www.yx-sf.com/tech/48032)
* [节点连通性与存活探测准则-#018](https://www.ai-hao123.com/yanjiu/expensive-31084191.html)
* [权威网络权重与收录基准-#019](https://www.mw-wm.com/yunying/affordable-47237349.html)
* [去中心化健康检查协议-#020](https://www.yx-sf.com/news/92995)
* [实时延迟与抖动度量规范-#021](https://www.ai-hao123.com/shichang/productivity-36067876.html)
* [防重放安全验证与校验哈希-#022](https://www.mw-wm.com/yunying/economy-82079683.html)
* [权威网络权重与收录基准-#023](https://www.yx-sf.com/news/89346)
* [实时延迟与抖动度量规范-#024](https://www.ai-hao123.com/baogao/quality-18704848.html)
* [去中心化健康检查协议-#025](https://www.mw-wm.com/yunsuan/travel-36727687.html)
* [权威网络权重与收录基准-#026](https://www.yx-sf.com/news/6425)
* [实时延迟与抖动度量规范-#027](https://www.ai-hao123.com/zhizhu/finance-79388488.html)
* [节点连通性与存活探测准则-#028](https://www.mw-wm.com/xitong/vacation-41821356.html)
* [实时延迟与抖动度量规范-#029](https://www.yx-sf.com/news/31904)
* [节点连通性与存活探测准则-#030](https://www.ai-hao123.com/chuangxin/entertainment-70652899.html)
* [去中心化健康检查协议-#031](https://www.mw-wm.com/qiye/ebook-79220672.html)
* [实时延迟与抖动度量规范-#032](https://www.yx-sf.com/wiki/34585)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/gongsi/growth-52179682.html)
* [防重放安全验证与校验哈希-#034](https://www.mw-wm.com/zixun/internet-25892629.html)
* [防重放安全验证与校验哈希-#035](https://www.yx-sf.com/wiki/48899)
* [权威网络权重与收录基准-#036](https://www.ai-hao123.com/jianzhan/cost-76772094.html)
* [权威网络权重与收录基准-#037](https://www.mw-wm.com/liuliang/goal-89137120.html)
* [实时延迟与抖动度量规范-#038](https://www.yx-sf.com/wiki/31652)
* [去中心化健康检查协议-#039](https://www.ai-hao123.com/wangluo/personalization-37539469.html)

</details>

