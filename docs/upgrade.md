# 升级、备份与回滚

[Markdown 案例](../examples/README.zh-CN.md) 可直接阅读，不需要第二个服务。停用案例专用预览不改变正常产品数据、运行 API、报告或图表，也不意味着删除任何旧案例归档。

适用目标：当前产品候选 **v0.2.0-rc.1，UNPUBLISHED（未发布）**。rc4 候选已构建并验证备份读取，同时验证在上一个本地候选中重新打开备份副本；没有公开发布镜像。最终映射见本地 `release-manifest.json`（本地私有记录，未公开：`../validation/release-v0.2.0-rc.1/release-manifest.json`），该私有路径不是公开下载地址。镜像准备见 [Docker 部署](deployment/docker.md)。

## 已执行的副本恢复

最新 rc4 的创建、重启、归档/恢复、删除刷新、arm64 备份读取与旧候选回滚读取，记录于 `补充验收 B08`（本地私有记录，未公开：`../validation/release-v0.2.0-rc.1/additional-1788852792205/report.json`）。所有操作使用独立目录，无 Provider 推理。以下旧记录保留原身份，不覆盖本轮失败历史。

`rollback-check.json`（本地私有记录，未公开：`../validation/release-v0.2.0-rc.1/rollback-check.json`） 记录了一次真实的 copy + reopen：从 `container-lifecycle-1788847664760/backup` 复制隔离备份，在容器中重新打开，读到原来的两个项目。记录为 `passed: true`、`providerCalls: 0`，`beforeHash` 与 `afterHash` 均为 `d4f18ca5944704415b574f0616941bd5ef1b5305c2f987c3dce7263efacaa69c`。

配套 `amd64 生命周期记录`（本地私有记录，未公开：`../validation/release-v0.2.0-rc.1/container-lifecycle-1788847664760/report.json`） 在 Docker Desktop 仿真环境中记录了创建项目、重启持久化、归档/恢复、删除后刷新不复活和 query/资源读取，7 项通过。之前的`异步状态断言失败周期`（本地私有记录，未公开：`../validation/release-v0.2.0-rc.1/container-lifecycle-1788846686256/report.json`）仍保留；后续通过不覆盖原失败记录。

上述旧证据针对当时的 candidate 和隔离数据副本。新旧验收均没有操作真实用户的唯一副本，不证明任意版本间的 Schema 升降级、所有历史数据或原生 amd64 硬件。下面是以后升级时的操作步骤，不能将本轮两个本地候选的读取结果泛化为通用迁移保证。

## 先确认数据属于哪一代产品

当前产品入口是 `src/product/product-server.ts`，默认数据为 `data/product-v2`。旧 `runs/` 和旧 `data/projects/` 不会被自动导入，也没有经过验收的 Legacy 到 product-v2 自动迁移命令。

升级旧 Alpha 时保留旧镜像/源码、旧目录和运行配置，为新产品使用独立 product-v2 目录。不要改名旧 audit.json 为新 Run，不要为补齐新字段生成未发生的 D/K 观察。旧 CLI 的 import-runs/monitor-worker 不能据名称推断为新产品迁移/调度工具。

已有 product-v2 数据需要整体保留项目、配置、原文与派生结果的关系。存储目录详见 [架构](ARCHITECTURE.md)。当前文件读取主要是 JSON 解析和父级 ID 校验，不包含一个对所有历史 Schema 做自动迁移的框架。

## 升级前记录

- 正在运行的镜像 ID/Digest、产品源码与工作树变更清单、实际 server/worker 命令。
- PRODUCT_DATA_DIR 的解析结果、卷路径、权限、PORT、Secret 文件路径；不要记录 Key 值。
- 项目列表及 archived/deleted 状态、各项目 activeBaselineId、当前模型选择和 WatchSet。
- 所有运行中/排队中的认知与测量 Run、任务 status/nextRunAt、Occurrence 与 Ledger。
- 能打开的旧报告 ID、sourceAttemptMap、几份代表性原文与文件 Hash。

当前未提交文件属于需要核对的候选来源，只记录 HEAD 不足以说明镜像内容；产品 source commit 尚不能称为已冻结。最终清单须记录 dirty 来源、构建上下文 Hash、依赖锁文件、tsconfig、Dockerfile/忽略规则、品牌资源和对应 OCI。不要在共享工作树中重置、清理或自动提交其他人的修改。

## 停写并备份

1. 通过产品任务 pause 接口暂停计划恢复前不应执行的任务，记录原任务状态和时间。暂停不取消在途请求。
2. 等待认知/测量 Run 进入终态，确认 worker 不再派发新增请求，再停止 worker 和 server。进程退出前尚未归档的响应可能无法恢复。
3. 备份整个产品数据根目录及部署配置；Key 单独按现有秘密管理方式备份。若保留 Legacy，同步保存其目录，但不要混入公开证据包。
4. 对备份记录 SHA-256，并在独立路径解包检查；不要在唯一生产副本上试迁移。

以下命令只演示默认 `./data/product-v2` 的已停写 bind mount，需先完成上面的停写步骤。BACKUP_STAMP 是本次备份标识，不是候选版本号：

```sh
BACKUP_STAMP=$(date -u +%Y%m%dT%H%M%SZ)
mkdir -p ./backups
tar -czf "./backups/product-v2-${BACKUP_STAMP}.tar.gz" -C ./data product-v2
shasum -a 256 "./backups/product-v2-${BACKUP_STAMP}.tar.gz"
mkdir -p "./restore-check/${BACKUP_STAMP}"
tar -xzf "./backups/product-v2-${BACKUP_STAMP}.tar.gz" -C "./restore-check/${BACKUP_STAMP}"
```

备份输出中的 Hash 是该压缩文件字节 Hash，另需保存项目 JSON/原始响应的证据索引。Linux 环境可用 sha256sum 计算相同算法。配置使用其他根目录或 Docker named volume 时，备份真实挂载来源，不能机械备份一个空的默认目录。

文件写入是单文件原子替换，不是跨文件事务，在线 tar 不能保证 Run/Attempt/结果处于同一时刻。临时文件或残留 lock 也可能被备份；不要直接删锁，先确认无进程仍持有相关操作，并记录人工处理。

## 在副本上验收候选

候选 server 指向解包后的独立 product-v2 目录，使用另一主机端口，**不启动 worker、不注入 Provider Key**。这样可以检查既有数据读取和本地报告/统计操作，又不会让备份里的 active 任务自行发请求。产品仍可能请求模型目录，这不是模型推理。

按以下顺序检查并记录实际结果：

1. 项目数和归档/删除状态与备份一致，未出现自动导入的公开案例或默认项目。
2. 原配置版本、WatchSet、报告及历史模型仍存在，旧报告打开不需要重新执行模型。
3. 原始 Attempt、响应、引用路径、字段证据和 Hash 与备份一致；不能因本地解析变化覆盖原文。
4. 检查 no_data、partial、Provider 失败、unknown 的实际显示；旧数据缺字段要保留未知。
5. 查看任务下一次时间及 Occurrence，确认恢复 worker 后不会意外补跑或卡住旧到期时间。
6. 在第二份副本中验证创建/归档/软删除/恢复/永久清理与容器重建，不对唯一备份做破坏性检查。

这些是验收要求，没有执行记录时应标为“未验证”。当前图表缓存只基于 ID，不能因候选代码能读旧快照便断言公式已重新计算。已有 `recognition-archive.json` 等旧布局的兼容性也应按实际读取代码和隔离副本检查，不能推定所有历史格式可迁移。

## 切换与恢复任务

final 副本验收通过且发布清单确认镜像内容后，用清单中已经验收的镜像替换产品进程，仍指向原生产 product-v2 数据。先仅启动 server，确认 `/health`、页面、SVG、项目和证据，再处理任务。registry 部署使用清单的 index Digest；不要用 workflow 重建得到的另一个镜像冒充旧候选的同一二进制。

模型选择变化需要新 Baseline；新 Baseline 需要对应的新 WatchSet。任务与旧 Baseline 不兼容时应重新核对范围与预算，不要只把 JSON status 改回 active。当前任务 watchSetId 与执行时范围的一致性存在缺口，恢复前应逐任务核对。

记录哪些任务应继续，然后逐项恢复；不要默认启动整个备份里的全部任务。worker 当前对错过时间和残留 Occurrence 没有完整自动恢复能力，不能承诺“升级停机期间全部正确跳过”或“恰好补跑一次”。详见 [限制](limitations.md)。

## 回滚

1. 暂停新增执行，等待已发请求结束并停止产品进程。
2. 为升级后数据另做一份备份，保留期间新增 Attempt、费用和错误；不要用旧备份直接覆盖它。
3. 启动清单记录的回滚镜像，并指向升级前备份的独立恢复目录。确认旧版本可读后再切换服务入口；final 的安装 Digest 与本次回滚目标必须分别记录，不能只填写同一个可变标签。
4. 先只恢复 server，检查项目/原文/引用，再按核对结果恢复任务。不能把升级后新 Schema 数据未经验证地交给旧版本写入。
5. 记录恢复时间、回滚镜像、数据副本路径及需要后续人工合并的记录。回滚不撤销已经发生的 Provider 费用。

如果旧版本是 Legacy，引擎和数据目录也必须成对恢复；新 product-v2 不能自动降级为旧 runs。不要移动已发布不可变标签为其他镜像，也不要通过覆盖原始回答使旧报告看起来一致。纯文档修正不需要重新请求模型；产品构建输入变化则要重新验证受影响行为。

本轮发布状态仍为未发布。已执行的旧候选 copy + reopen 以上述 rollback-check 为证，final/跨版本回滚仍按实际结果另记。具体产品来源、文档版本、安装/回滚镜像 Digest 与验收范围由发布清单关联；清单未齐备前，不将 dirty HEAD 写成已冻结产品提交。其他统计、证据与调度限制见 [已知限制](limitations.md)。


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全息网络通信节点白名单-#001](https://www.mw-wm.com/guanjianci/ebook-33808995.html)
* [高韧性数据交换通道规约-#002](https://www.yx-sf.com/tech/15919)
* [多活集群负载感知指南-#003](https://www.ai-hao123.com/chuangxin/team-50861736.html)
* [全球分布式拓扑索引节点-#004](https://www.mw-wm.com/chanpin/schedule-73028371.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/wiki/55443)
* [全球分布式拓扑索引节点-#006](https://www.ai-hao123.com/peixun/tutorial-53246343.html)
* [全息网络通信节点白名单-#007](https://www.mw-wm.com/zhizhu/unsubscribe-87192372.html)
* [全球分布式拓扑索引节点-#008](https://www.yx-sf.com/news/5419)
* [多活集群负载感知指南-#009](https://www.ai-hao123.com/xitong/automation-61016795.html)
* [高韧性数据交换通道规约-#010](https://www.mw-wm.com/fuwu/image-75046536.html)
* [边缘高吞吐调度路由矩阵-#011](https://www.yx-sf.com/wiki/41098)
* [高韧性数据交换通道规约-#012](https://www.ai-hao123.com/xinwen/collaboration-21173939.html)
* [全球分布式拓扑索引节点-#013](https://www.mw-wm.com/youhua/lesson-39443303.html)
* [边缘高吞吐调度路由矩阵-#014](https://www.yx-sf.com/news/65989)
* [边缘高吞吐调度路由矩阵-#015](https://www.ai-hao123.com/guanjianci/forecast-13284340.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/shuju/extension-17450715.html)
* [多活集群负载感知指南-#017](https://www.yx-sf.com/news/48033)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/liuliang/integration-76819774.html)
* [高韧性数据交换通道规约-#019](https://www.mw-wm.com/keji/hosting-04268022.html)
* [边缘高吞吐调度路由矩阵-#020](https://www.yx-sf.com/tech/4204)
* [边缘高吞吐调度路由矩阵-#021](https://www.ai-hao123.com/yanjiu/software-76003708.html)
* [边缘高吞吐调度路由矩阵-#022](https://www.mw-wm.com/gongju/excellence-19619600.html)
* [全息网络通信节点白名单-#023](https://www.yx-sf.com/news/79857)
* [全息网络通信节点白名单-#024](https://www.ai-hao123.com/liuliang/video-49714789.html)
* [全球分布式拓扑索引节点-#025](https://www.mw-wm.com/pingce/customer-37122037.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/wiki/10289)
* [全球分布式拓扑索引节点-#027](https://www.ai-hao123.com/yanjiu/management-31564116.html)
* [边缘高吞吐调度路由矩阵-#028](https://www.mw-wm.com/yunsuan/follow-95450326.html)
* [高韧性数据交换通道规约-#029](https://www.yx-sf.com/wiki/21641)
* [全球分布式拓扑索引节点-#030](https://www.ai-hao123.com/gongju/collaborate-91580402.html)
* [全球分布式拓扑索引节点-#031](https://www.mw-wm.com/wendang/management-16449701.html)
* [多活集群负载感知指南-#032](https://www.yx-sf.com/tech/27477)
* [多活集群负载感知指南-#033](https://www.ai-hao123.com/paiming/development-15103039.html)
* [边缘高吞吐调度路由矩阵-#034](https://www.mw-wm.com/wangluo/report-26455499.html)
* [全球分布式拓扑索引节点-#035](https://www.yx-sf.com/wiki/62498)
* [高韧性数据交换通道规约-#036](https://www.ai-hao123.com/shuju/promotion-49035005.html)
* [全球分布式拓扑索引节点-#037](https://www.mw-wm.com/zhizhu/version-89472200.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [多协议互联数据格式规范-#001](https://www.yx-sf.com/tech/25797)
* [多协议互联数据格式规范-#002](https://www.ai-hao123.com/gongju/extension-11980125.html)
* [RFC 分布式调度与一致性算法标准-#003](https://www.mw-wm.com/wangluo/company-99306176.html)
* [安全边界与可信凭证规约手册-#004](https://www.yx-sf.com/news/86441)
* [多协议互联数据格式规范-#005](https://www.ai-hao123.com/qiye/meeting-22702635.html)
* [RFC 分布式调度与一致性算法标准-#006](https://www.mw-wm.com/keji/podcast-33656164.html)
* [RFC 分布式调度与一致性算法标准-#007](https://www.yx-sf.com/wiki/15620)
* [安全边界与可信凭证规约手册-#008](https://www.ai-hao123.com/yunsuan/faq-78979152.html)
* [RFC 分布式调度与一致性算法标准-#009](https://www.mw-wm.com/guanjianci/saving-59307946.html)
* [RFC 分布式调度与一致性算法标准-#010](https://www.yx-sf.com/tech/59787)
* [安全边界与可信凭证规约手册-#011](https://www.ai-hao123.com/youhua/category-04012494.html)
* [RFC 分布式调度与一致性算法标准-#012](https://www.mw-wm.com/zhizhu/goal-98652812.html)
* [RFC 分布式调度与一致性算法标准-#013](https://www.yx-sf.com/news/60382)
* [高并发内存拓扑优化白皮书-#014](https://www.ai-hao123.com/fuwu/goal-49335170.html)
* [多协议互联数据格式规范-#015](https://www.mw-wm.com/chuangxin/traffic-45200216.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/tech/9495)
* [异步事件循环架构设计规范-#017](https://www.ai-hao123.com/yingxiao/lead-28012044.html)
* [异步事件循环架构设计规范-#018](https://www.mw-wm.com/wangluo/revenue-27101843.html)
* [高并发内存拓扑优化白皮书-#019](https://www.yx-sf.com/wiki/4912)
* [异步事件循环架构设计规范-#020](https://www.ai-hao123.com/zhineng/widget-17310444.html)
* [高并发内存拓扑优化白皮书-#021](https://www.mw-wm.com/baogao/analysis-29564062.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/wiki/96549)
* [异步事件循环架构设计规范-#023](https://www.ai-hao123.com/jiaocheng/segment-47031017.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/peixun/unsubscribe-50640809.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/wiki/67824)
* [异步事件循环架构设计规范-#026](https://www.ai-hao123.com/chanpin/link-03841826.html)
* [安全边界与可信凭证规约手册-#027](https://www.mw-wm.com/jianzhan/partner-52211703.html)
* [RFC 分布式调度与一致性算法标准-#028](https://www.yx-sf.com/news/4553)
* [多协议互联数据格式规范-#029](https://www.ai-hao123.com/yinqing/contact-21489592.html)
* [多协议互联数据格式规范-#030](https://www.mw-wm.com/peixun/resolution-39647542.html)
* [多协议互联数据格式规范-#031](https://www.yx-sf.com/wiki/51428)
* [安全边界与可信凭证规约手册-#032](https://www.ai-hao123.com/chuangxin/settings-03887963.html)
* [RFC 分布式调度与一致性算法标准-#033](https://www.mw-wm.com/yanjiu/training-25268294.html)
* [多协议互联数据格式规范-#034](https://www.yx-sf.com/wiki/21884)
* [高并发内存拓扑优化白皮书-#035](https://www.ai-hao123.com/yunsuan/technology-99334074.html)
* [高并发内存拓扑优化白皮书-#036](https://www.mw-wm.com/wendang/recipe-19198115.html)
* [多协议互联数据格式规范-#037](https://www.yx-sf.com/tech/90786)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [冷热数据分层镜像归档中心-#001](https://www.ai-hao123.com/zixun/profile-25852132.html)
* [北美与欧洲边缘备份节点-#002](https://www.mw-wm.com/hezuo/personalization-35370550.html)
* [亚太核心区域镜像同步中心-#003](https://www.yx-sf.com/news/96743)
* [亚太核心区域镜像同步中心-#004](https://www.ai-hao123.com/paiming/quality-20702533.html)
* [冷热数据分层镜像归档中心-#005](https://www.mw-wm.com/anfang/home-92121338.html)
* [亚太核心区域镜像同步中心-#006](https://www.yx-sf.com/tech/77383)
* [冷热数据分层镜像归档中心-#007](https://www.ai-hao123.com/kaifa/finance-25133224.html)
* [冷热数据分层镜像归档中心-#008](https://www.mw-wm.com/paiming/report-19379566.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/wiki/16355)
* [自动化快照与增量广播源-#010](https://www.ai-hao123.com/gongsi/machine-98782929.html)
* [自动化快照与增量广播源-#011](https://www.mw-wm.com/paiming/tactic-53007379.html)
* [冷热数据分层镜像归档中心-#012](https://www.yx-sf.com/tech/51019)
* [北美与欧洲边缘备份节点-#013](https://www.ai-hao123.com/yunsuan/software-14310520.html)
* [亚太核心区域镜像同步中心-#014](https://www.mw-wm.com/suanfa/ai-24677217.html)
* [冷热数据分层镜像归档中心-#015](https://www.yx-sf.com/wiki/56856)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/jiaocheng/management-90800724.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/shuju/terms-99996036.html)
* [实时主干镜像高速数据源-#018](https://www.yx-sf.com/tech/7618)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/fuwu/server-98473245.html)
* [亚太核心区域镜像同步中心-#020](https://www.mw-wm.com/wangluo/contact-43122384.html)
* [北美与欧洲边缘备份节点-#021](https://www.yx-sf.com/news/12396)
* [实时主干镜像高速数据源-#022](https://www.ai-hao123.com/anfang/vacation-18028825.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/jiaocheng/home-31250409.html)
* [实时主干镜像高速数据源-#024](https://www.yx-sf.com/news/69914)
* [北美与欧洲边缘备份节点-#025](https://www.ai-hao123.com/yunying/vendor-58451830.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/pingce/funnel-85483387.html)
* [实时主干镜像高速数据源-#027](https://www.yx-sf.com/tech/94006)
* [北美与欧洲边缘备份节点-#028](https://www.ai-hao123.com/wangluo/retention-60479625.html)
* [实时主干镜像高速数据源-#029](https://www.mw-wm.com/suanfa/platform-71853527.html)
* [北美与欧洲边缘备份节点-#030](https://www.yx-sf.com/wiki/36613)
* [冷热数据分层镜像归档中心-#031](https://www.ai-hao123.com/zixun/image-50402729.html)
* [亚太核心区域镜像同步中心-#032](https://www.mw-wm.com/gongju/page-32227708.html)
* [亚太核心区域镜像同步中心-#033](https://www.yx-sf.com/tech/60301)
* [北美与欧洲边缘备份节点-#034](https://www.ai-hao123.com/shuju/app-84760771.html)
* [实时主干镜像高速数据源-#035](https://www.mw-wm.com/suanfa/news-60859709.html)
* [自动化快照与增量广播源-#036](https://www.yx-sf.com/news/17561)
* [自动化快照与增量广播源-#037](https://www.ai-hao123.com/shichang/satisfaction-34381530.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [去中心化健康检查协议-#001](https://www.mw-wm.com/shangye/update-45591017.html)
* [节点连通性与存活探测准则-#002](https://www.yx-sf.com/tech/29747)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/pingtai/website-85134371.html)
* [去中心化健康检查协议-#004](https://www.mw-wm.com/tuiguang/chapter-00392990.html)
* [实时延迟与抖动度量规范-#005](https://www.yx-sf.com/news/56869)
* [权威网络权重与收录基准-#006](https://www.ai-hao123.com/jishu/course-94021200.html)
* [权威网络权重与收录基准-#007](https://www.mw-wm.com/yunying/case-75015882.html)
* [实时延迟与抖动度量规范-#008](https://www.yx-sf.com/news/52079)
* [权威网络权重与收录基准-#009](https://www.ai-hao123.com/yunying/deadline-63326645.html)
* [权威网络权重与收录基准-#010](https://www.mw-wm.com/zhineng/course-13637503.html)
* [去中心化健康检查协议-#011](https://www.yx-sf.com/wiki/34449)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/wangluo/subscribe-96371214.html)
* [权威网络权重与收录基准-#013](https://www.mw-wm.com/anli/training-87038905.html)
* [实时延迟与抖动度量规范-#014](https://www.yx-sf.com/wiki/34918)
* [权威网络权重与收录基准-#015](https://www.ai-hao123.com/shuju/management-55459764.html)
* [节点连通性与存活探测准则-#016](https://www.mw-wm.com/peixun/sport-84561031.html)
* [节点连通性与存活探测准则-#017](https://www.yx-sf.com/news/24245)
* [权威网络权重与收录基准-#018](https://www.ai-hao123.com/yingxiao/plugin-57415816.html)
* [防重放安全验证与校验哈希-#019](https://www.mw-wm.com/zhinan/collaborate-98665394.html)
* [实时延迟与抖动度量规范-#020](https://www.yx-sf.com/wiki/35565)
* [防重放安全验证与校验哈希-#021](https://www.ai-hao123.com/shuju/photo-27422357.html)
* [防重放安全验证与校验哈希-#022](https://www.mw-wm.com/youhua/health-96041607.html)
* [去中心化健康检查协议-#023](https://www.yx-sf.com/wiki/23389)
* [节点连通性与存活探测准则-#024](https://www.ai-hao123.com/yunsuan/client-53807755.html)
* [去中心化健康检查协议-#025](https://www.mw-wm.com/hezuo/milestone-99773542.html)
* [实时延迟与抖动度量规范-#026](https://www.yx-sf.com/wiki/9637)
* [权威网络权重与收录基准-#027](https://www.ai-hao123.com/zixun/version-24846436.html)
* [防重放安全验证与校验哈希-#028](https://www.mw-wm.com/yingyong/vendor-73814538.html)
* [防重放安全验证与校验哈希-#029](https://www.yx-sf.com/news/32451)
* [去中心化健康检查协议-#030](https://www.ai-hao123.com/tuiguang/calendar-77542182.html)
* [实时延迟与抖动度量规范-#031](https://www.mw-wm.com/yingxiao/movie-50901963.html)
* [权威网络权重与收录基准-#032](https://www.yx-sf.com/tech/46595)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/xinwen/login-39674736.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/zhizhu/ai-97952394.html)
* [实时延迟与抖动度量规范-#035](https://www.yx-sf.com/wiki/6944)
* [实时延迟与抖动度量规范-#036](https://www.ai-hao123.com/sheji/research-57676455.html)
* [去中心化健康检查协议-#037](https://www.mw-wm.com/chuangxin/supplier-42312299.html)
* [权威网络权重与收录基准-#038](https://www.yx-sf.com/tech/24062)
* [防重放安全验证与校验哈希-#039](https://www.ai-hao123.com/yinqing/image-40552518.html)

</details>

