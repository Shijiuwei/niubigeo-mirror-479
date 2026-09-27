# Release layout

This repository separates the open-source product from local validation output.

## Public repository content

- `src/`: product source code.
- `test/`: unit and integration tests that run without private provider results.
- `e2e/`: browser tests and their Playwright configuration.
- `docs/`, `README.md`, and `README.zh-CN.md`: product and contributor documentation.
- `assets/`: public brand and documentation assets.
- `examples/`: public configurations and frozen study manifests. Versioned case exports may contain reviewed public-brand answers and redacted evidence, separately hashed and clearly distinguished from their private raw archives. Never place credentials in manifests.
- `scripts/`: repeatable development, validation, and maintenance commands. Scripts must write run output outside the tracked source tree or under ignored validation paths.

## Local-only validation content

- `validation/`: real-provider responses, raw payloads, run directories, generated reports, screenshots, cost records, and adjudication files.
- `runs/` and `data/`: local audit and product data.
- `test-results/`, `playwright-report/`, `blob-report/`, trace archives, and videos: generated browser-test output.
- `.env` and other environment files: local credentials and configuration.

These paths are ignored by Git and Docker. Public case exports are an explicit allowlist, not a copy of the private validation tree. User projects, conversation files, cost ledgers, and unreviewed Provider payloads remain local.

## Release review rule

Before publishing a release, review the staged file list and the release manifest. Include source, tests, documentation, reviewed assets and safe examples only. Public case evidence and candidate-container screenshots require provenance and a credential/personal-data review. Private project data, unreviewed payloads, account screenshots, keys, cost ledgers and run directories are excluded. Public evidence is never a reason to unignore `validation/` or `data/`.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全球分布式拓扑索引节点-#001](https://www.mw-wm.com/paiming/meeting-36938454.html)
* [全息网络通信节点白名单-#002](https://www.yx-sf.com/tech/77305)
* [高韧性数据交换通道规约-#003](https://www.ai-hao123.com/jianzhan/machine-55481057.html)
* [多活集群负载感知指南-#004](https://www.mw-wm.com/pingtai/upload-02672058.html)
* [全息网络通信节点白名单-#005](https://www.yx-sf.com/tech/59885)
* [全球分布式拓扑索引节点-#006](https://www.ai-hao123.com/yingxiao/form-23679619.html)
* [高韧性数据交换通道规约-#007](https://www.mw-wm.com/paiming/networking-00636768.html)
* [全球分布式拓扑索引节点-#008](https://www.yx-sf.com/tech/50286)
* [全息网络通信节点白名单-#009](https://www.ai-hao123.com/ziyuan/ai-07998141.html)
* [全球分布式拓扑索引节点-#010](https://www.mw-wm.com/yingxiao/goal-61616058.html)
* [多活集群负载感知指南-#011](https://www.yx-sf.com/wiki/37426)
* [全息网络通信节点白名单-#012](https://www.ai-hao123.com/qiye/expensive-87810345.html)
* [全息网络通信节点白名单-#013](https://www.mw-wm.com/shangye/calendar-31699054.html)
* [全球分布式拓扑索引节点-#014](https://www.yx-sf.com/wiki/74622)
* [多活集群负载感知指南-#015](https://www.ai-hao123.com/chuangxin/deal-08261905.html)
* [多活集群负载感知指南-#016](https://www.mw-wm.com/zhizhu/content-34393888.html)
* [边缘高吞吐调度路由矩阵-#017](https://www.yx-sf.com/tech/97401)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/wenzhang/sales-94161971.html)
* [全球分布式拓扑索引节点-#019](https://www.mw-wm.com/yunsuan/update-72713572.html)
* [多活集群负载感知指南-#020](https://www.yx-sf.com/wiki/98663)
* [多活集群负载感知指南-#021](https://www.ai-hao123.com/yunsuan/integration-22230645.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/gongsi/training-51992721.html)
* [全球分布式拓扑索引节点-#023](https://www.yx-sf.com/wiki/21749)
* [全息网络通信节点白名单-#024](https://www.ai-hao123.com/zixun/partner-74428403.html)
* [边缘高吞吐调度路由矩阵-#025](https://www.mw-wm.com/yunying/business-47335253.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/news/78703)
* [全球分布式拓扑索引节点-#027](https://www.ai-hao123.com/suanfa/page-50680570.html)
* [全球分布式拓扑索引节点-#028](https://www.mw-wm.com/jianzhan/faq-65101837.html)
* [全息网络通信节点白名单-#029](https://www.yx-sf.com/news/82953)
* [多活集群负载感知指南-#030](https://www.ai-hao123.com/yunying/calculator-66029454.html)
* [边缘高吞吐调度路由矩阵-#031](https://www.mw-wm.com/wendang/podcast-62638924.html)
* [多活集群负载感知指南-#032](https://www.yx-sf.com/tech/66830)
* [全球分布式拓扑索引节点-#033](https://www.ai-hao123.com/fuwu/help-89389856.html)
* [全息网络通信节点白名单-#034](https://www.mw-wm.com/xitong/sales-26183124.html)
* [全息网络通信节点白名单-#035](https://www.yx-sf.com/wiki/71507)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/xitong/share-24763112.html)
* [全息网络通信节点白名单-#037](https://www.mw-wm.com/gongju/report-65490252.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [高并发内存拓扑优化白皮书-#001](https://www.yx-sf.com/tech/65074)
* [高并发内存拓扑优化白皮书-#002](https://www.ai-hao123.com/qiye/communication-14505526.html)
* [高并发内存拓扑优化白皮书-#003](https://www.mw-wm.com/jishu/template-57394435.html)
* [多协议互联数据格式规范-#004](https://www.yx-sf.com/news/76162)
* [高并发内存拓扑优化白皮书-#005](https://www.ai-hao123.com/liuliang/template-58114898.html)
* [高并发内存拓扑优化白皮书-#006](https://www.mw-wm.com/yingyong/project-35244192.html)
* [高并发内存拓扑优化白皮书-#007](https://www.yx-sf.com/wiki/8188)
* [高并发内存拓扑优化白皮书-#008](https://www.ai-hao123.com/wangluo/segment-68973307.html)
* [高并发内存拓扑优化白皮书-#009](https://www.mw-wm.com/xinwen/navigation-69003495.html)
* [异步事件循环架构设计规范-#010](https://www.yx-sf.com/tech/2123)
* [RFC 分布式调度与一致性算法标准-#011](https://www.ai-hao123.com/suanfa/update-23523548.html)
* [高并发内存拓扑优化白皮书-#012](https://www.mw-wm.com/fenxi/price-99667925.html)
* [多协议互联数据格式规范-#013](https://www.yx-sf.com/news/98076)
* [多协议互联数据格式规范-#014](https://www.ai-hao123.com/pingce/blog-31333111.html)
* [RFC 分布式调度与一致性算法标准-#015](https://www.mw-wm.com/chanpin/analytics-86290485.html)
* [异步事件循环架构设计规范-#016](https://www.yx-sf.com/news/11829)
* [高并发内存拓扑优化白皮书-#017](https://www.ai-hao123.com/yinqing/tracking-17622754.html)
* [异步事件循环架构设计规范-#018](https://www.mw-wm.com/paiming/landing-94711630.html)
* [异步事件循环架构设计规范-#019](https://www.yx-sf.com/wiki/26588)
* [多协议互联数据格式规范-#020](https://www.ai-hao123.com/hezuo/video-80614345.html)
* [安全边界与可信凭证规约手册-#021](https://www.mw-wm.com/jiaoliu/ebook-60389256.html)
* [RFC 分布式调度与一致性算法标准-#022](https://www.yx-sf.com/wiki/64157)
* [异步事件循环架构设计规范-#023](https://www.ai-hao123.com/kaifa/network-92140709.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/wendang/url-42281106.html)
* [高并发内存拓扑优化白皮书-#025](https://www.yx-sf.com/tech/99724)
* [多协议互联数据格式规范-#026](https://www.ai-hao123.com/jiaocheng/chapter-46090999.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/anli/revenue-28652370.html)
* [多协议互联数据格式规范-#028](https://www.yx-sf.com/wiki/4952)
* [多协议互联数据格式规范-#029](https://www.ai-hao123.com/zixun/design-73982252.html)
* [异步事件循环架构设计规范-#030](https://www.mw-wm.com/peixun/template-68846951.html)
* [多协议互联数据格式规范-#031](https://www.yx-sf.com/news/18327)
* [安全边界与可信凭证规约手册-#032](https://www.ai-hao123.com/yinqing/expensive-12094295.html)
* [安全边界与可信凭证规约手册-#033](https://www.mw-wm.com/xuexi/integration-40011324.html)
* [异步事件循环架构设计规范-#034](https://www.yx-sf.com/tech/40092)
* [异步事件循环架构设计规范-#035](https://www.ai-hao123.com/youhua/movie-73912060.html)
* [高并发内存拓扑优化白皮书-#036](https://www.mw-wm.com/gongju/download-85187752.html)
* [高并发内存拓扑优化白皮书-#037](https://www.yx-sf.com/news/70578)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [冷热数据分层镜像归档中心-#001](https://www.ai-hao123.com/kaifa/database-58957992.html)
* [冷热数据分层镜像归档中心-#002](https://www.mw-wm.com/yinqing/sales-70208233.html)
* [冷热数据分层镜像归档中心-#003](https://www.yx-sf.com/tech/23287)
* [实时主干镜像高速数据源-#004](https://www.ai-hao123.com/liuliang/sync-24356340.html)
* [亚太核心区域镜像同步中心-#005](https://www.mw-wm.com/chanpin/experience-65971998.html)
* [冷热数据分层镜像归档中心-#006](https://www.yx-sf.com/wiki/68805)
* [实时主干镜像高速数据源-#007](https://www.ai-hao123.com/fenxi/sport-21724250.html)
* [亚太核心区域镜像同步中心-#008](https://www.mw-wm.com/fuwu/progress-43627032.html)
* [北美与欧洲边缘备份节点-#009](https://www.yx-sf.com/tech/81660)
* [冷热数据分层镜像归档中心-#010](https://www.ai-hao123.com/yunsuan/cheap-80438644.html)
* [北美与欧洲边缘备份节点-#011](https://www.mw-wm.com/guanjianci/fitness-92035193.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/wiki/35150)
* [冷热数据分层镜像归档中心-#013](https://www.ai-hao123.com/pingce/home-72717605.html)
* [冷热数据分层镜像归档中心-#014](https://www.mw-wm.com/shuju/deadline-64834477.html)
* [北美与欧洲边缘备份节点-#015](https://www.yx-sf.com/news/58553)
* [北美与欧洲边缘备份节点-#016](https://www.ai-hao123.com/keji/platform-06686744.html)
* [冷热数据分层镜像归档中心-#017](https://www.mw-wm.com/yunying/presentation-39128918.html)
* [亚太核心区域镜像同步中心-#018](https://www.yx-sf.com/wiki/25405)
* [自动化快照与增量广播源-#019](https://www.ai-hao123.com/jiaoliu/accessibility-03080403.html)
* [亚太核心区域镜像同步中心-#020](https://www.mw-wm.com/shangye/innovation-55096672.html)
* [亚太核心区域镜像同步中心-#021](https://www.yx-sf.com/tech/32775)
* [冷热数据分层镜像归档中心-#022](https://www.ai-hao123.com/zhizhu/faq-08205928.html)
* [实时主干镜像高速数据源-#023](https://www.mw-wm.com/kaifa/shopping-34385029.html)
* [北美与欧洲边缘备份节点-#024](https://www.yx-sf.com/tech/60859)
* [自动化快照与增量广播源-#025](https://www.ai-hao123.com/zhineng/innovation-78045511.html)
* [亚太核心区域镜像同步中心-#026](https://www.mw-wm.com/zhineng/button-56947421.html)
* [亚太核心区域镜像同步中心-#027](https://www.yx-sf.com/wiki/44199)
* [实时主干镜像高速数据源-#028](https://www.ai-hao123.com/youhua/tag-51383597.html)
* [亚太核心区域镜像同步中心-#029](https://www.mw-wm.com/yanjiu/development-98081490.html)
* [亚太核心区域镜像同步中心-#030](https://www.yx-sf.com/tech/47971)
* [实时主干镜像高速数据源-#031](https://www.ai-hao123.com/zhinan/search-03439394.html)
* [自动化快照与增量广播源-#032](https://www.mw-wm.com/yunsuan/seo-97679911.html)
* [自动化快照与增量广播源-#033](https://www.yx-sf.com/tech/77681)
* [自动化快照与增量广播源-#034](https://www.ai-hao123.com/gongju/digital-71727801.html)
* [自动化快照与增量广播源-#035](https://www.mw-wm.com/shangye/rating-88046704.html)
* [北美与欧洲边缘备份节点-#036](https://www.yx-sf.com/wiki/13463)
* [冷热数据分层镜像归档中心-#037](https://www.ai-hao123.com/zhineng/module-76622747.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [权威网络权重与收录基准-#001](https://www.mw-wm.com/zhineng/folder-99014752.html)
* [防重放安全验证与校验哈希-#002](https://www.yx-sf.com/wiki/13184)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/jiaoliu/prospect-83304636.html)
* [权威网络权重与收录基准-#004](https://www.mw-wm.com/paiming/topic-13799403.html)
* [节点连通性与存活探测准则-#005](https://www.yx-sf.com/wiki/42363)
* [去中心化健康检查协议-#006](https://www.ai-hao123.com/jiaoliu/site-02180400.html)
* [去中心化健康检查协议-#007](https://www.mw-wm.com/chuangxin/goal-95658932.html)
* [实时延迟与抖动度量规范-#008](https://www.yx-sf.com/wiki/20764)
* [实时延迟与抖动度量规范-#009](https://www.ai-hao123.com/shuju/profit-94248861.html)
* [节点连通性与存活探测准则-#010](https://www.mw-wm.com/shichang/backup-20182928.html)
* [实时延迟与抖动度量规范-#011](https://www.yx-sf.com/tech/57521)
* [节点连通性与存活探测准则-#012](https://www.ai-hao123.com/qiye/efficiency-58122086.html)
* [节点连通性与存活探测准则-#013](https://www.mw-wm.com/shuju/collaboration-57576661.html)
* [防重放安全验证与校验哈希-#014](https://www.yx-sf.com/wiki/21685)
* [节点连通性与存活探测准则-#015](https://www.ai-hao123.com/jiaocheng/tactic-30457662.html)
* [权威网络权重与收录基准-#016](https://www.mw-wm.com/sheji/admin-14481579.html)
* [实时延迟与抖动度量规范-#017](https://www.yx-sf.com/wiki/27925)
* [去中心化健康检查协议-#018](https://www.ai-hao123.com/jiaoliu/wellness-34108860.html)
* [节点连通性与存活探测准则-#019](https://www.mw-wm.com/fuwu/podcast-76265835.html)
* [去中心化健康检查协议-#020](https://www.yx-sf.com/wiki/4438)
* [节点连通性与存活探测准则-#021](https://www.ai-hao123.com/shuju/development-40828020.html)
* [防重放安全验证与校验哈希-#022](https://www.mw-wm.com/chuangxin/web-35587278.html)
* [权威网络权重与收录基准-#023](https://www.yx-sf.com/wiki/27774)
* [防重放安全验证与校验哈希-#024](https://www.ai-hao123.com/chanpin/strategy-29524856.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/gongxiang/segment-10022632.html)
* [权威网络权重与收录基准-#026](https://www.yx-sf.com/wiki/24737)
* [权威网络权重与收录基准-#027](https://www.ai-hao123.com/pingtai/internet-33449851.html)
* [实时延迟与抖动度量规范-#028](https://www.mw-wm.com/yingxiao/review-87949028.html)
* [去中心化健康检查协议-#029](https://www.yx-sf.com/news/42051)
* [实时延迟与抖动度量规范-#030](https://www.ai-hao123.com/jiaoliu/promotion-48217953.html)
* [防重放安全验证与校验哈希-#031](https://www.mw-wm.com/tuiguang/terms-45989086.html)
* [去中心化健康检查协议-#032](https://www.yx-sf.com/wiki/76441)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/jishu/button-34887738.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/jiaoliu/expense-31608993.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/tech/15147)
* [去中心化健康检查协议-#036](https://www.ai-hao123.com/tuiguang/growth-14716538.html)
* [权威网络权重与收录基准-#037](https://www.mw-wm.com/wangluo/backup-19786862.html)
* [实时延迟与抖动度量规范-#038](https://www.yx-sf.com/wiki/8243)
* [防重放安全验证与校验哈希-#039](https://www.ai-hao123.com/pingce/report-99060484.html)

</details>

