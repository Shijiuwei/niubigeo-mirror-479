# Docker 部署

## NiubiGEO v0.2.0

正式镜像为 `ghcr.io/albert-weasker/niubigeo:v0.2.0`，支持 Linux amd64 和 arm64。先在宿主环境中设置 `OPENROUTER_API_KEY`，再执行：

```bash
docker pull ghcr.io/albert-weasker/niubigeo:v0.2.0
docker run -d --name niubigeo \
  -p 127.0.0.1:8787:8787 \
  -e OPENROUTER_API_KEY \
  -v niubigeo-data:/app/data/product-v2 \
  ghcr.io/albert-weasker/niubigeo:v0.2.0
```

打开 <http://localhost:8787>。命名卷 `niubigeo-data` 会在重新创建容器后保留；升级前请先[备份](../upgrade.md)。不要直接对公网开放工作台，远程访问需要另外配置认证和 TLS。

定时监测需要额外启动 Worker，必须使用同一数据卷；此操作会执行到期任务并产生 API 费用：

```bash
docker run -d --name niubigeo-worker --no-healthcheck \
  -e OPENROUTER_API_KEY \
  -v niubigeo-data:/app/data/product-v2 \
  ghcr.io/albert-weasker/niubigeo:v0.2.0 \
  node dist/src/product/scheduling/schedule-worker.js 60
```

公开镜像从 `v0.2.0` Tag 对应的 commit 构建。版本、源码标记、SVG、项目创建和重新创建容器后的持久化检查通过后，工作流才写入 `:v0.2.0` 与 `:latest`；候选版本不能更新 `latest`。实际 Digest 和来源记录见[正式发布附件](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)。本版的统计及验收缺口仍见[发布说明](../releases/v0.2.0.md)，不将历史 blocked 记录改成 passed。

<details>
<summary>历史候选构建记录与部署参数说明（非正式镜像身份）</summary>

阅读 [20 个 Markdown 案例](../../examples/README.zh-CN.md) 不需要启动容器或案例站。以下命令只用于正常产品工作台，历史静态预览不是部署依赖。

以下是正式发布前的 **v0.2.0-rc.1 历史候选记录**，保留当时的状态、命令与验收边界，不用于标识 v0.2.0 镜像。安装当前版本请使用上面的命令。

最终 OCI、index/各架构 Digest、构建输入、源码对应及 registry 状态记录在本地 `release-manifest.json`（本地私有记录，未公开：`../../validation/release-v0.2.0-rc.1/release-manifest.json`）。清单已经生成，但该 validation 路径不是永久公开下载入口。当前构建和运行映射见 `rc4-image-provenance.json`（本地私有记录，未公开：`../../validation/release-v0.2.0-rc.1/rc4-image-provenance.json`），仍有未通过门禁，见[版本说明](../releases/v0.2.0-rc.1.md)。

当前产品入口是 [product-server.ts](../../src/product/product-server.ts)，编译后为 `dist/src/product/product-server.js`。worker 入口为 [schedule-worker.ts](../../src/product/scheduling/schedule-worker.ts)，编译后为 `dist/src/product/scheduling/schedule-worker.js`。旧 `dist/src/server.js`、旧 CLI monitor-worker 不是当前产品入口。

## 构建前确认

使用完整的当前候选工作树，而不是只 checkout 旧 HEAD；本阶段产品包含尚未提交的文件。Node 版本要求为 22 或以上，镜像构建依赖仓库的 package-lock.json。Dockerfile 使用多阶段构建，运行时只安装生产依赖。

发布前必须确认仓库 [Dockerfile](../../Dockerfile) 与 [Compose](../../docker-compose.yml) 已完成当前入口调整：

- 默认命令为 `node dist/src/product/product-server.js`。
- runtime stage 含编译结果、生产依赖与 `assets/brand/` 下的新徽标和字标；当前 Dockerfile 明确只复制这两份品牌文件。
- 数据根目录设置为 `/app/data/product-v2`，挂载整个产品数据目录。
- worker 使用当前 scheduling 入口，Compose worker 由显式 profile 启用。
- `.dockerignore` 排除 Key、`.env`、真实用户数据、validation、截图验收包与临时输出，不将本机业务数据烘焙进镜像。

旧 candidate OCI 中，当前 server、两份新 SVG、PRODUCT_DATA_DIR 和 `/health` 已有本地运行证据，amd64/arm64 的已加载 config 均与多架构归档对应。记录见 `旧镜像映射`（本地私有记录，未公开：`../../validation/release-v0.2.0-rc.1/image-provenance.json`） 与 `构建元数据`（本地私有记录，未公开：`../../validation/release-v0.2.0-rc.1/image-build-metadata.json`）。这两份文件保留旧候选身份，不能替代 final 清单。

源码仍来自包含未提交修改的工作树，不能称为“产品 source commit 已冻结”。旧 BuildKit provenance 中的 HEAD 只是基础提交；最终清单须列出 dirty 文件与实际构建输入 Hash，包含 `tsconfig.json`、两份 SVG、依赖锁文件和 Dockerfile。若后续形成产品提交，也须核对其内容与已验收 OCI 的关系，不能只以当前 HEAD 推断。

## 本地候选启动

在项目根目录执行。先由发布清单选择对应架构的已加载镜像 ID，设置 `LOCAL_IMAGE`。本轮已按相同 server、端口和数据挂载方式启动当前候选，并完成创建、重启、删除和备份读取验收。这里不推送或创建 Git Tag/Release：

```sh
: "${LOCAL_IMAGE:?从发布清单设置对应架构的已加载镜像ID}"
mkdir -p ./data/product-v2
docker run --detach --name niubigeo-rc \
  --publish 127.0.0.1:8787:8787 \
  --env PORT=8787 \
  --env PRODUCT_DATA_DIR=/app/data/product-v2 \
  --mount type=bind,source="$(pwd)/data/product-v2",target=/app/data/product-v2 \
  "$LOCAL_IMAGE" \
  node dist/src/product/product-server.js
```

这个无 Key 启动方式用于页面、既有数据读取及非推理操作。模型目录可能访问 OpenRouter 外网，但没有 Key 的模型执行不能获得真实回答。

页面地址为 [认知工作台](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html) 和 [持续测量](https://qbgr.wtpuscm.cn/liuliang/success-12030162.html)。服务目前只对根路径返回页面，深链不能随意改为 `/projects/...`。端口占用时替换冒号前的主机端口；容器内仍为 8787。

## BYOK 与费用

NiubiGEO 当前产品使用 OpenRouter BYOK。Key 由服务器环境读取，不是在浏览器页面中上传给公开演示站点。用户承担模型、搜索与服务器费用；赞助不改变测量规则或结果。

[env.ts](../../src/config/env.ts) 的 Key 查找顺序为：

1. OPENROUTER_API_KEY 的非空直接值，或 OPENROUTER_API_KEY_FILE 指向的文件内容。
2. OPENROUTER_KEY 的非空直接值，或 OPENROUTER_KEY_FILE 指向的文件内容。

项目根目录 `.env` 在进程启动时载入，不覆盖已有非空环境值。容器不会自动包含宿主 `.env`；使用环境注入或只读 Secret 文件。Key 文件不存在、不可读或为空时仍视为缺少 Key。

如需允许已获预算授权的真实执行，可以在上面的 docker run 中添加：

```sh
--env OPENROUTER_API_KEY_FILE=/run/secrets/openrouter_api_key \
--mount type=bind,source="$(pwd)/secrets/openrouter_api_key",target=/run/secrets/openrouter_api_key,readonly
```

该片段是 docker run 的附加参数，不是单独命令。文件须事先由部署者在本机准备，限制可读权限，不提交仓库。不要把真实 Key 写入 README、截图、日志或镜像构建参数。

配置 Key 不自动执行认知，但点击运行、重试、启用到期任务或调用 `/api/scheduler/due` 可产生费用。初始认知截断时可能自动追加一次请求；测量的 costLimitUsd/tokenLimit 目前不是完整的强制预算闸门。详见 [限制](../limitations.md)，不能把 UI 请求计数当账户总预算保障。

## 数据卷

| 环境变量 | 当前用途 |
| --- | --- |
| PRODUCT_DATA_DIR | 当前产品完整数据根目录，优先级最高 |
| MONITORING_DATA_DIR | 未设置 PRODUCT_DATA_DIR 时，在其下使用 product-v2；默认 data |
| RUNS_DIR | Legacy 输出路径，不能替代当前产品数据卷 |
| PORT | HTTP 监听端口，默认 8787 |

推荐映射 `./data/product-v2` 到 `/app/data/product-v2` 并显式设置 PRODUCT_DATA_DIR。若既有部署挂载整个 `./data:/app/data`，仍可保留该挂载并确保 PRODUCT_DATA_DIR 指向 `/app/data/product-v2`。不要挂载两个不一致的数据副本给 server 和 worker。

必须保存 projects 下的 project.json、模型选择、Baselines、认知运行及其报告、测量范围/运行/统计、任务/Occurrence/Ledger。只备份旧 runs 或只备份 Attempt 文件不足以恢复关系。相对路径根据容器工作目录解析，本镜像工作目录为 `/app`。

宿主卷需要允许运行用户读写；JSON 文件不是只读数据库。`docker rm` 不会删除 bind mount 中的数据，产品 purge 则会永久删除项目子树。备份与恢复步骤见 [升级](../upgrade.md)。

## 显式启用 worker

HTTP server 本身不会定时扫描。worker 默认 60 秒轮询，位置参数可设定秒数且至少为 10；它不接受旧 CLI 的 `--poll-seconds` 参数。

单独启动一个 worker 的命令如下。执行前先核对全部 active 任务与预算；它会扫描同一数据根目录的到期任务并真实请求模型：

```sh
docker run --detach --name niubigeo-rc-worker \
  --no-healthcheck \
  --env PRODUCT_DATA_DIR=/app/data/product-v2 \
  --env OPENROUTER_API_KEY_FILE=/run/secrets/openrouter_api_key \
  --mount type=bind,source="$(pwd)/data/product-v2",target=/app/data/product-v2 \
  --mount type=bind,source="$(pwd)/secrets/openrouter_api_key",target=/run/secrets/openrouter_api_key,readonly \
  "$LOCAL_IMAGE" \
  node dist/src/product/scheduling/schedule-worker.js 60
```

worker 没有额外 HTTP 端口，因此单独启动时禁用镜像自带的 HTTP healthcheck。暂停任务只阻止后续到期执行，不取消已经在途的模型请求。用产品 pause 接口暂停需要停止的任务，并确认 Run 终态后再停止容器：

```sh
docker stop niubigeo-rc-worker
```

当前 Compose 的 server 服务保留名称 niubistar-geo，worker 为 niubigeo-worker，profile 为 monitoring。Compose 将宿主环境或 `.env` 中的 OPENROUTER_API_KEY/OPENROUTER_KEY 传给容器，两者均允许空值；这与上文显式 Secret 文件挂载方式不同。默认端口绑定 `127.0.0.1:8787`，宿主 PORT 可覆盖主机端口。默认启动不启用 worker。

以下 Compose 命令仅用于以后有意从源码部署的场景，会构建新镜像，**不保证与清单中已验收 OCI 相同**；固定镜像验收与发布使用上文镜像 ID 或下文 registry Digest：

```sh
docker compose up --build -d niubistar-geo
```

确认任务和预算后，才显式启动 worker：

```sh
docker compose --profile monitoring up --build -d niubigeo-worker
```

两个服务挂载整个 `./data:/app/data`，当前产品在其 product-v2 子目录。worker 禁用 HTTP healthcheck，不能通过 server 存活推断调度已工作。

## 已有验证与 final 边界

- 旧 OCI 的两个平台 manifest/config 与已加载镜像对应；28 个 OCI blob 的 Digest/大小已有只读核对。应用层只含编译产品、package.json、生产依赖与两份新 SVG，未烘焙仓库测试、validation、真实数据、网站、文档或截图。
- arm64 容器在本地 8795 读取复制的预检归档，`4 张预检截图及索引`（本地私有记录，未公开：`../../validation/release-v0.2.0-rc.1/container-browser-1788846299778/report.json`） 已有记录。它们是预检回放，不能计成 20 案例的新推理。
- amd64 已在 Docker Desktop 仿真下运行；8796 使用独立空数据，后续 8797 的`生命周期记录`（本地私有记录，未公开：`../../validation/release-v0.2.0-rc.1/container-lifecycle-1788847664760/report.json`）包含创建、重启持久化、归档/恢复、删除刷新和深层 query/资源，7 项通过。此前立即读取状态造成的`失败周期`（本地私有记录，未公开：`../../validation/release-v0.2.0-rc.1/container-lifecycle-1788846686256/report.json`）保留，不删除或改写为成功。
- 备份真实复制并重新打开已经执行，见 `rollback-check`（本地私有记录，未公开：`../../validation/release-v0.2.0-rc.1/rollback-check.json`）。这证明旧候选读取该隔离副本，不能据此声明任意跨版本 Schema 迁移或 final 回滚已通过。

这些结论只属于已记录的旧 candidate。小修会重建 final，并由发布清单关联受影响验收；不默认重新调用模型来修正文档或截图。产品 UI 不是全链路双语，统计/来源证据也有现有限制，见 [发布说明](../releases/v0.2.0-rc.1.md) 与 [L01—L20](../limitations.md)。

## 保留 Digest 转发到 registry

本节是**未执行的发布操作规程**，不是当前授权。付费推理授权、本地构建和文档编辑授权均不等于 GHCR 上传、Git push、GitHub Tag/Release 或移动 latest 的授权。

执行前必须全部满足：

1. final 小修/重建和受影响验收已完成，发布负责人确认清单中的 final OCI 是要公开的同一份归档；清单缺失、仍指向旧 candidate 或验收未完成时停止。
2. 已明确授权向目标 GHCR 仓库上传该 Digest。产品来源与 dirty 变更已在清单交代；若要创建 `sha-<commit>` 标签，该 commit 必须经过内容对应核对，不能填旧 HEAD 冒充已冻结来源。
3. 已审核镜像、证据与文档中的公开内容。registry 凭证只用于登录，不能写入镜像、清单、命令记录或公开附件。
4. 已协调暂停同一仓库的其他标签写入。版本/commit 标签必须未占用；认证、网络、服务错误或无法列出标签一律停止。检查与写入之间不具备 registry 原子锁，不能同时由其他发布者写入。

需要 Node 22+ 和支持下列选项的 Skopeo。发布负责人从 `release-manifest.json` 设置并 `export` 这些变量；本文不假定尚未定稿的清单字段结构，也不提供占位 Digest：

| 变量 | 来源与要求 |
| --- | --- |
| OCI_ARCHIVE | 清单中已验收 final OCI archive 的本地路径；包含唯一一个多架构镜像 index |
| EXPECTED_DIGEST | 同一 final 的 `sha256:` index Digest，不是单架构 config/image ID 或 tar 文件 Hash |
| SOURCE_SHA | 清单中已确认内容对应的产品 commit，完整 40 位；dirty 来源尚未解决则不得进入此上传流程 |
| TRANSFER_RECORDS | 本次上传记录的新目录，不能复用失败周期目录 |
| GHCR_USER | 拥有目标仓库写入权限的账户；登录时交互输入 token |

以下整段只在上述授权门禁通过后，于仓库根目录执行。两次标签写入均复制完整已验收 OCI，没有 build 步骤；不会写入 latest：

```sh
set -eu
export IMAGE=ghcr.io/albert-weasker/niubigeo
export CANDIDATE_TAG=v0.2.0-rc.1
export RELEASE_MANIFEST=validation/release-v0.2.0-rc.1/release-manifest.json
: "${OCI_ARCHIVE:?从清单设置final OCI路径}"
: "${EXPECTED_DIGEST:?从清单设置已验收index Digest}"
: "${SOURCE_SHA:?从清单设置已核对产品commit}"
: "${TRANSFER_RECORDS:?设置新的上传记录目录}"
: "${GHCR_USER:?设置有权限的registry账户}"
test -s "$RELEASE_MANIFEST"
test -s "$OCI_ARCHIVE"
test ! -e "$TRANSFER_RECORDS"
mkdir -p "$TRANSFER_RECORDS"
cp "$RELEASE_MANIFEST" "$TRANSFER_RECORDS/release-manifest.input.json"

node --input-type=module <<'NODE'
import { createReleasePlan, validateDigest } from './scripts/release-image-policy.mjs';
const plan = createReleasePlan({ eventName: 'workflow_dispatch', action: 'candidate', tag: process.env.CANDIDATE_TAG, sourceSha: process.env.SOURCE_SHA });
validateDigest(process.env.EXPECTED_DIGEST);
if (plan.image !== process.env.IMAGE) throw new Error('Registry differs from release policy');
NODE

skopeo inspect --raw "oci-archive:${OCI_ARCHIVE}" > "$TRANSFER_RECORDS/local-index.json"
test "$(skopeo manifest-digest "$TRANSFER_RECORDS/local-index.json")" = "$EXPECTED_DIGEST"
skopeo login --username "$GHCR_USER" ghcr.io
skopeo list-tags "docker://${IMAGE}" > "$TRANSFER_RECORDS/tags.before.json"
node --input-type=module <<'NODE'
import { readFileSync } from 'node:fs';
const { Tags } = JSON.parse(readFileSync(process.env.TRANSFER_RECORDS + '/tags.before.json', 'utf8'));
if (!Array.isArray(Tags)) throw new Error('Registry tag inventory unavailable');
for (const tag of [process.env.CANDIDATE_TAG, 'sha-' + process.env.SOURCE_SHA]) {
  if (Tags.includes(tag)) throw new Error('Immutable tag already exists: ' + tag);
}
NODE

for TARGET_TAG in "$CANDIDATE_TAG" "sha-${SOURCE_SHA}"; do
  export TARGET_TAG
  skopeo list-tags "docker://${IMAGE}" > "$TRANSFER_RECORDS/tags.current.json"
  node --input-type=module <<'NODE'
import { readFileSync } from 'node:fs';
const { Tags } = JSON.parse(readFileSync(process.env.TRANSFER_RECORDS + '/tags.current.json', 'utf8'));
if (!Array.isArray(Tags) || Tags.includes(process.env.TARGET_TAG)) throw new Error('Cannot create immutable tag');
NODE
  skopeo copy --all --preserve-digests \
    --digestfile "$TRANSFER_RECORDS/${TARGET_TAG}.digest" \
    "oci-archive:${OCI_ARCHIVE}" "docker://${IMAGE}:${TARGET_TAG}"
  test "$(cat "$TRANSFER_RECORDS/${TARGET_TAG}.digest")" = "$EXPECTED_DIGEST"
  skopeo inspect --raw "docker://${IMAGE}:${TARGET_TAG}" > "$TRANSFER_RECORDS/${TARGET_TAG}.index.json"
  test "$(skopeo manifest-digest "$TRANSFER_RECORDS/${TARGET_TAG}.index.json")" = "$EXPECTED_DIGEST"
done
```

`--all` 复制 index 及其所有平台/证明条目；`--preserve-digests` 要求保留内容 Digest，不能保留时失败。不要删除该选项、强制转换格式、重压缩，或用 `docker load` 后单架构 `docker push` 替代整份归档转发。选项依据 [Skopeo copy](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)、[OCI archive transport](https://www.poykq.cn/redian/tutorial-673489.html)；index 的计算方式见 [manifest-digest](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)。

失败可能发生在部分 blob/标签已经写入之后。保留全部记录，先检查目标状态再决定后续操作；不要删除已公开标签、覆盖已有不可变标签或关闭 Digest 校验来重试。新仓库无法列出标签时也会停止，需由发布负责人单独处理仓库初始化，不将错误解释成“标签不存在”。

上传完成后仍须按清单逐架构核对并完成公开拉取/访问验收，记录远端 index 与平台 Digest；本地 image ID 等于 config Digest，不是多架构 index 身份。部署时从清单设置 `EXPECTED_DIGEST`，固定使用 `ghcr.io/albert-weasker/niubigeo@${EXPECTED_DIGEST}`，不能仅凭标签名字宣称内容一致。

## 工作流与稳定提升

[docker-publish.yml](../../.github/workflows/docker-publish.yml) 的 candidate 路径会重新构建，并添加 revision/version 等 label。即使来自相同源码，也不能称为已验收本地 OCI 的同一二进制或同一 Digest；上面的 preserve-digest 转发是独立规程，本页没有改写工作流。

preview/rc、普通 release 事件及默认手动 candidate 路径不得移动 latest。只有另行明确授权的稳定提升，才能在默认分支手动选择 `promote-stable`，提供稳定版本、同版本 prerelease 标签、已验收 Digest、核对过的产品 commit、验收证据 URL，并确认 `confirm_tested`。策略会检查 candidate/commit 标签指向该 Digest、拒绝已存在的稳定版本标签，先验证稳定标签再移动 latest，不重新构建。验收 URL 与确认项是人工责任记录，不是自动完成全部验收的证明。

上传 RC 不授权创建 Git Tag/Release、官网部署或稳定提升。当前仍为未发布；准确门禁与未完成项见 [发布说明](../releases/v0.2.0-rc.1.md)。

当前产品未内置认证、TLS 或多用户访问控制。本地命令将端口绑定至 127.0.0.1；对外部署需在受控网络/认证代理后运行，原文与 Key 留在自有环境。

</details>


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全息网络通信节点白名单-#001](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [边缘高吞吐调度路由矩阵-#002](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [多活集群负载感知指南-#003](https://zgah.spidernode-mesh.net/yingyong/technology-03475499.html)
* [边缘高吞吐调度路由矩阵-#004](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [高韧性数据交换通道规约-#005](https://www.mw-wm.com/yinqing/ai-45938821.html)
* [全球分布式拓扑索引节点-#006](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [边缘高吞吐调度路由矩阵-#007](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [边缘高吞吐调度路由矩阵-#008](https://www.ai-hao123.com/shuju/case-75200214.html)
* [全球分布式拓扑索引节点-#009](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [全球分布式拓扑索引节点-#010](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [高韧性数据交换通道规约-#011](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534.html)
* [全球分布式拓扑索引节点-#012](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [全息网络通信节点白名单-#013](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696.html)
* [全球分布式拓扑索引节点-#014](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [全球分布式拓扑索引节点-#015](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)
* [多活集群负载感知指南-#016](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [全息网络通信节点白名单-#017](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/jianzhan/study-01013754.html)
* [全球分布式拓扑索引节点-#019](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [全息网络通信节点白名单-#020](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [多活集群负载感知指南-#021](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [多活集群负载感知指南-#022](https://wryi.wtpuscm.cn/qiye/interface-215.html)
* [多活集群负载感知指南-#023](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [多活集群负载感知指南-#024](https://aizt.wtpuscm.cn/guanjianci/form-299.html)
* [全球分布式拓扑索引节点-#025](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)
* [边缘高吞吐调度路由矩阵-#026](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [边缘高吞吐调度路由矩阵-#027](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [全息网络通信节点白名单-#028](https://ovzp.wtpuscm.cn/xuexi/report-93713076.html)
* [多活集群负载感知指南-#029](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [多活集群负载感知指南-#030](https://fglw.wtpuscm.cn/jianzhan/data-59540835.html)
* [高韧性数据交换通道规约-#031](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [边缘高吞吐调度路由矩阵-#032](https://xwia.spidernode-mesh.net/shangye/services-26058978.html)
* [全球分布式拓扑索引节点-#033](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [多活集群负载感知指南-#034](https://owfm.tcti.cn/shangye/education-63674207.html)
* [全球分布式拓扑索引节点-#035](https://fglw.wtpuscm.cn/jianzhan/data-59540835.html)
* [高韧性数据交换通道规约-#036](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [全息网络通信节点白名单-#037](https://www.mw-wm.com/shichang/recipe-97410639.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://ftpp.wtpuscm.cn/kaifa/expensive-215146.html)
* [多协议互联数据格式规范-#002](https://ovzp.wtpuscm.cn/xuexi/report-93713076.html)
* [RFC 分布式调度与一致性算法标准-#003](https://fglw.wtpuscm.cn/jianzhan/data-59540835.html)
* [多协议互联数据格式规范-#004](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [安全边界与可信凭证规约手册-#005](https://ovzp.wtpuscm.cn/xuexi/report-93713076.html)
* [多协议互联数据格式规范-#006](https://httc.tcti.cn/yunsuan/help-88640044.html)
* [RFC 分布式调度与一致性算法标准-#007](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [RFC 分布式调度与一致性算法标准-#008](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932.html)
* [安全边界与可信凭证规约手册-#009](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [高并发内存拓扑优化白皮书-#010](https://owfm.tcti.cn/shangye/education-63674207.html)
* [RFC 分布式调度与一致性算法标准-#011](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)
* [异步事件循环架构设计规范-#012](https://www.mw-wm.com/wenzhang/affordable-55766184.html)
* [高并发内存拓扑优化白皮书-#013](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [多协议互联数据格式规范-#014](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)
* [RFC 分布式调度与一致性算法标准-#015](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [安全边界与可信凭证规约手册-#016](https://pcsi.wtpuscm.cn/paiming/progress-692.html)
* [异步事件循环架构设计规范-#017](https://www.poykq.cn/redian/tutorial-673489.html)
* [安全边界与可信凭证规约手册-#018](https://aajx.wtpuscm.cn/yingyong/deal-193677.html)
* [异步事件循环架构设计规范-#019](https://www.ai-hao123.com/wangluo/keyword-74854184.html)
* [多协议互联数据格式规范-#020](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [多协议互联数据格式规范-#021](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [多协议互联数据格式规范-#022](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [异步事件循环架构设计规范-#023](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html)
* [多协议互联数据格式规范-#024](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [RFC 分布式调度与一致性算法标准-#025](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [异步事件循环架构设计规范-#026](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [RFC 分布式调度与一致性算法标准-#027](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [RFC 分布式调度与一致性算法标准-#028](https://gdtq.spidernode-mesh.net/keji/account-53764057.html)
* [异步事件循环架构设计规范-#029](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [异步事件循环架构设计规范-#030](https://www.ai-hao123.com/gongju/personalization-02210073.html)
* [高并发内存拓扑优化白皮书-#031](https://unqt.wtpuscm.cn/zixun/contact-59980425.html)
* [RFC 分布式调度与一致性算法标准-#032](https://www.poykq.cn/redian/tutorial-673489.html)
* [RFC 分布式调度与一致性算法标准-#033](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [高并发内存拓扑优化白皮书-#034](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102.html)
* [安全边界与可信凭证规约手册-#035](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [RFC 分布式调度与一致性算法标准-#036](https://vias.wtpuscm.cn/yanjiu/conversion-58794136.html)
* [多协议互联数据格式规范-#037](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [冷热数据分层镜像归档中心-#001](https://zgah.spidernode-mesh.net/yingyong/technology-03475499.html)
* [实时主干镜像高速数据源-#002](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [冷热数据分层镜像归档中心-#003](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [亚太核心区域镜像同步中心-#004](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [北美与欧洲边缘备份节点-#005](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696.html)
* [北美与欧洲边缘备份节点-#006](https://api.pvucttcv.cn/yinyue/innovation-37390655.html)
* [亚太核心区域镜像同步中心-#007](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [北美与欧洲边缘备份节点-#008](https://keil.spidernode-mesh.net/yunying/server-16840384.html)
* [北美与欧洲边缘备份节点-#009](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776.html)
* [实时主干镜像高速数据源-#010](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [北美与欧洲边缘备份节点-#011](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html)
* [北美与欧洲边缘备份节点-#012](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [实时主干镜像高速数据源-#013](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [自动化快照与增量广播源-#014](https://ankmz.cn/anquan/tag-68558329.html)
* [实时主干镜像高速数据源-#015](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [亚太核心区域镜像同步中心-#016](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)
* [北美与欧洲边缘备份节点-#017](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [冷热数据分层镜像归档中心-#018](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)
* [亚太核心区域镜像同步中心-#019](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [北美与欧洲边缘备份节点-#020](https://nojh.spidernode-mesh.net/suanfa/study-22518081.html)
* [自动化快照与增量广播源-#021](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [北美与欧洲边缘备份节点-#022](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [自动化快照与增量广播源-#023](https://iozk.spidernode-mesh.net/fenxi/quality-22754958.html)
* [自动化快照与增量广播源-#024](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [实时主干镜像高速数据源-#025](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297.html)
* [亚太核心区域镜像同步中心-#026](https://www.yx-sf.com/wiki/86303.html)
* [实时主干镜像高速数据源-#027](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html)
* [冷热数据分层镜像归档中心-#028](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [冷热数据分层镜像归档中心-#029](https://zgah.spidernode-mesh.net/yingyong/technology-03475499.html)
* [自动化快照与增量广播源-#030](https://gynw.tcti.cn/fenxi/recipe-50406879.html)
* [亚太核心区域镜像同步中心-#031](https://ytxd.wtpuscm.cn/baogao/price-87851711.html)
* [实时主干镜像高速数据源-#032](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [自动化快照与增量广播源-#033](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [实时主干镜像高速数据源-#034](https://mvev.wtpuscm.cn/kuangjia/about-215.html)
* [实时主干镜像高速数据源-#035](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [实时主干镜像高速数据源-#036](https://aagj.tcti.cn/jianzhan/audience-84449488.html)
* [冷热数据分层镜像归档中心-#037](https://keil.spidernode-mesh.net/yunying/server-16840384.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [实时延迟与抖动度量规范-#001](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [权威网络权重与收录基准-#002](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345.html)
* [实时延迟与抖动度量规范-#003](https://www.mw-wm.com/zhineng/data-62496196.html)
* [实时延迟与抖动度量规范-#004](https://fjac.spidernode-mesh.net/anli/investment-94283191.html)
* [权威网络权重与收录基准-#005](https://dloe.spidernode-mesh.net/chuangxin/products-47216067.html)
* [节点连通性与存活探测准则-#006](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [防重放安全验证与校验哈希-#007](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [权威网络权重与收录基准-#008](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534.html)
* [实时延迟与抖动度量规范-#009](https://tfcb.wtpuscm.cn/yanjiu/review-64634682.html)
* [节点连通性与存活探测准则-#010](https://qbgr.wtpuscm.cn/liuliang/success-12030162.html)
* [节点连通性与存活探测准则-#011](https://ukvo.spidernode-mesh.net/anli/download-57719010.html)
* [权威网络权重与收录基准-#012](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [去中心化健康检查协议-#013](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [权威网络权重与收录基准-#014](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [节点连通性与存活探测准则-#015](https://kvaf.tcti.cn/yunsuan/settings-81875461.html)
* [防重放安全验证与校验哈希-#016](https://www.poykq.cn/redian/tutorial-673489.html)
* [防重放安全验证与校验哈希-#017](https://iuuv.tcti.cn/hezuo/app-80239016.html)
* [节点连通性与存活探测准则-#018](https://aagj.tcti.cn/jianzhan/audience-84449488.html)
* [去中心化健康检查协议-#019](https://aagj.tcti.cn/jianzhan/audience-84449488.html)
* [实时延迟与抖动度量规范-#020](https://auey.wtpuscm.cn/paiming/sale-411.html)
* [防重放安全验证与校验哈希-#021](https://mxrq.tcti.cn/zixun/settings-35354207.html)
* [权威网络权重与收录基准-#022](https://ankmz.cn/anquan/tag-68558329.html)
* [去中心化健康检查协议-#023](https://www.ai-hao123.com/yanjiu/theme-21228434.html)
* [去中心化健康检查协议-#024](https://obpk.wtpuscm.cn/baogao/privacy-67260604.html)
* [实时延迟与抖动度量规范-#025](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [去中心化健康检查协议-#026](https://etyt.spidernode-mesh.net/baogao/performance-14923227.html)
* [权威网络权重与收录基准-#027](https://pynf.wtpuscm.cn/jianzhan/innovation-362165.html)
* [节点连通性与存活探测准则-#028](https://shmv.spidernode-mesh.net/gongsi/digital-64522869.html)
* [防重放安全验证与校验哈希-#029](https://fjoc.tcti.cn/yingyong/contact-00610313.html)
* [防重放安全验证与校验哈希-#030](https://lase.tcti.cn/fenxi/lesson-67970267.html)
* [权威网络权重与收录基准-#031](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656.html)
* [去中心化健康检查协议-#032](https://www.tcti.cn/hulianwang/feedback-96499358.html)
* [实时延迟与抖动度量规范-#033](https://www.mw-wm.com/gongsi/settings-83763719.html)
* [防重放安全验证与校验哈希-#034](https://tszz.tcti.cn/yingyong/cost-12593599.html)
* [节点连通性与存活探测准则-#035](https://vhxh.wtpuscm.cn/chuangxin/tactic-286.html)
* [去中心化健康检查协议-#036](https://szjp.tcti.cn/shichang/retention-16647312.html)
* [去中心化健康检查协议-#037](https://yyns.spidernode-mesh.net/wendang/review-40421998.html)
* [实时延迟与抖动度量规范-#038](https://zgah.spidernode-mesh.net/yingyong/technology-03475499.html)
* [去中心化健康检查协议-#039](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964.html)

</details>



---

<details open>
<summary><b>📚 Docker 部署 官方技术规约与全息拓扑引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目「Docker 部署」遵循开放开源与知识共享协议。以下引用矩阵涵盖项目架构白皮书、高可用镜像注册中心、分布式通信契约与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 Docker 部署 核心架构规约与设计白皮书 (Architecture & Core Specs)

* [【官方规范】Docker 部署 显式启用 worker 核心运行拓扑标准](https://api.pvucttcv.cn/yinyue/innovation-37390655-1-18240.html)
* [Docker 部署 分布式数据通道与 已有验证与 final 边界 技术规范 (Core/已有验证与 )](https://ankmz.cn/anquan/tag-68558329-2-49818.html)
* [现代 Docker 部署 架构演进之路 —— Docker 部署 深度实践](https://www.poykq.cn/redian/tutorial-673489-3-60631.html)
* [【官方规范】Docker 部署 数据卷 核心运行拓扑标准](https://oald.wtpuscm.cn/keji/deadline-176471.html)
* [Docker 部署 分布式数据通道与 可信存活健康度量 技术规范 (v2.0-GA)](https://itqn.wtpuscm.cn/zixun/tool-962.html)
* [现代 NiubiGEO v0.2.0 架构演进之路 —— Docker 部署 深度实践](https://www.tcti.cn/hulianwang/feedback-96499358-6-25626.html)
* [Docker 部署 内部组件解耦与事件状态机规范 (Core/NiubiG)](https://wdtz.tcti.cn/shangye/admin-74765663.html)
* [现代 模块化解耦与协议标准 架构演进之路 —— Docker 部署 深度实践](https://www.mw-wm.com/shuju/fashion-06780174.html)
* [【Docker 部署】BYOK 与费用 核心系统架构与设计规约 (Draft-08)](https://www.yx-sf.com/tech/85693.html)
* [Docker 部署 分布式数据通道与 构建前确认 技术规范 (Spec-v1.5)](https://www.ai-hao123.com/tuiguang/notification-63899733.html)
* [面向大规模网络的 Docker 部署 工业级架构基准](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-11-29528.html)
* [【官方规范】Docker 部署 本地候选启动 核心运行拓扑标准](https://keil.spidernode-mesh.net/yunying/server-16840384-12-9777.html)
* [Docker 部署 分布式数据通道与 索引发布声明 技术规范 (Draft-01)](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-13-30344.html)
* [【官方规范】Docker 部署 可信存活健康度量 核心运行拓扑标准](https://fjoc.tcti.cn/yingyong/contact-00610313-14-41408.html)
* [基于 Docker 部署 的高吞吐 未执行的发布操作规程 设计白皮书](https://xwia.spidernode-mesh.net/shangye/services-26058978-15-6283.html)
* [Docker 部署 分布式数据通道与 Docker 部署 技术规范 (RFC-138)](https://gdtq.spidernode-mesh.net/keji/account-53764057-16-2674.html)
* [现代 索引发布声明 架构演进之路 —— Docker 部署 深度实践](https://obpk.wtpuscm.cn/baogao/privacy-67260604-17-322.html)
* [基于 Docker 部署 的高吞吐 高韧性系统架构设计 设计白皮书](https://gynw.tcti.cn/fenxi/recipe-50406879-18-16514.html)
* [Docker 部署 内部组件解耦与事件状态机规范 (v2.0-GA)](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-19-11134.html)
* [基于 Docker 部署 的高吞吐 索引发布声明 设计白皮书](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-20-52317.html)
* [【Docker 部署】Docker 部署 核心系统架构与设计规约 (Node-52)](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-21-34442.html)
* [基于 Docker 部署 的高吞吐 公开镜像从 设计白皮书](https://lase.tcti.cn/fenxi/lesson-67970267-22-40194.html)
* [Docker 部署 内部组件解耦与事件状态机规范 (Verified)](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-23-8169.html)
* [BYOK 与费用 核心系统架构与设计规约 (Spec-v1.6)](https://yyns.spidernode-mesh.net/wendang/review-40421998-24-55751.html)
* [Docker 部署 分布式数据通道与 工作流与稳定提升 技术规范 (Node-86)](https://fglw.wtpuscm.cn/jianzhan/data-59540835-25-26220.html)
* [基于 Docker 部署 的高吞吐 NiubiGEO v0.2.0 设计白皮书](https://owfm.tcti.cn/shangye/education-63674207-26-62012.html)
* [【官方规范】Docker 部署 保留 Digest 转发到 registry 核心运行拓扑标准](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-27-57627.html)
* [基于 Docker 部署 的高吞吐 模块化解耦与协议标准 设计白皮书](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-28-34465.html)
* [Docker 部署 内部组件解耦与事件状态机规范 (Node-69)](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-29-21841.html)
* [【官方规范】Docker 部署 Docker 部署 核心运行拓扑标准](https://aagj.tcti.cn/jianzhan/audience-84449488-30-25079.html)
* [Docker 部署 分布式数据通道与 BYOK 与费用 技术规范 (Verified)](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-31-22633.html)
* [现代 Docker 架构演进之路 —— Docker 部署 深度实践](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-32-29055.html)
* [Docker 部署 分布式数据通道与 保留 Digest 转发到 registry 技术规范 (v2.0-GA)](https://qbgr.wtpuscm.cn/liuliang/success-12030162-33-60398.html)
* [【Docker 部署】数据卷 核心系统架构与设计规约 (Spec-v2.4)](https://iuuv.tcti.cn/hezuo/app-80239016-34-56040.html)
* [Docker 部署 内部组件解耦与事件状态机规范 (Core/公开镜像从)](https://gifb.spidernode-mesh.net/shichang/about-02526745-35-619.html)
* [【官方规范】Docker 部署 索引发布声明 核心运行拓扑标准](https://fjac.spidernode-mesh.net/anli/investment-94283191-36-36809.html)
* [NiubiGEO v0.2.0 核心系统架构与设计规约 (Core/NiubiG)](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-37-23559.html)

#### 2. 🔌 生产级模块集成与接口调用规范 (APIs & Production Integration)

* [【集成指南】公开镜像从 服务端接入准则与 Docker 部署 实战](https://szjp.tcti.cn/shichang/retention-16647312-38-57855.html)
* [Docker 部署 异步中间件流水线与 构建前确认 接入规范](https://etyt.spidernode-mesh.net/baogao/performance-14923227-39-37900.html)
* [【集成指南】BYOK 与费用 服务端接入准则与 Docker 部署 实战](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-40-58216.html)
* [Docker 部署 核心 API 接口契约与客户端调用指南](https://ovzp.wtpuscm.cn/xuexi/report-93713076-41-8280.html)
* [Docker 部署 异步中间件流水线与 未执行的发布操作规程 接入规范](https://pdvy.tcti.cn/gongxiang/segment-83277821-42-19302.html)
* [Docker 部署 异步中间件流水线与 Docker 部署 接入规范](https://ukvo.spidernode-mesh.net/anli/download-57719010-43-31507.html)
* [Docker 部署 vs 业界主流方案：部署 深度技术选型对比](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-44-48999.html)
* [Docker 部署 异步中间件流水线与 公开镜像从 接入规范](https://unqt.wtpuscm.cn/zixun/contact-59980425-45-35427.html)
* [Docker 部署 异步中间件流水线与 显式启用 worker 接入规范](https://kvaf.tcti.cn/yunsuan/settings-81875461-46-52050.html)
* [基于 Docker 部署 的自动化部署与生产环境配置实践](https://nojh.spidernode-mesh.net/suanfa/study-22518081-47-6307.html)
* [【集成指南】构建前确认 服务端接入准则与 Docker 部署 实战](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-48-16896.html)
* [Docker 部署 异步中间件流水线与 模块化解耦与协议标准 接入规范](https://ytxd.wtpuscm.cn/baogao/price-87851711-49-61900.html)
* [【生产手册】Docker 部署 模块通信与请求穿透标准](https://ncrw.tcti.cn/kaifa/growth-85374259-50-56734.html)
* [【集成指南】可信存活健康度量 服务端接入准则与 Docker 部署 实战](https://api.pvucttcv.cn/yinyue/innovation-37390655-51-43928.html)
* [Docker 部署 vs 业界主流方案：显式启用 worker 深度技术选型对比](https://ankmz.cn/anquan/tag-68558329-52-53437.html)
* [Docker 部署 插件生态规范与 分布式状态机一致性 扩展手册 (Node-58)](https://www.poykq.cn/redian/tutorial-673489-53-44103.html)
* [Docker 部署 vs 业界主流方案：本地候选启动 深度技术选型对比](https://vnzf.wtpuscm.cn/zhineng/retention-713632.html)
* [Docker 部署 异步中间件流水线与 NiubiGEO v0.2.0 接入规范](https://irnx.wtpuscm.cn/jiaocheng/demographic-875.html)
* [Docker 部署 vs 业界主流方案：Docker 部署 深度技术选型对比](https://www.tcti.cn/hulianwang/feedback-96499358-56-45278.html)
* [Docker 部署 vs 业界主流方案：索引发布声明 深度技术选型对比](https://hbze.tcti.cn/paiming/ai-95747233.html)
* [Docker 部署 异步中间件流水线与 BYOK 与费用 接入规范](https://www.mw-wm.com/zixun/responsive-28907639.html)
* [Docker 部署 vs 业界主流方案：高韧性系统架构设计 深度技术选型对比](https://www.yx-sf.com/wiki/14258.html)
* [Docker 部署 异步中间件流水线与 已有验证与 final 边界 接入规范](https://www.ai-hao123.com/fenxi/layout-90714016.html)
* [Docker 部署 插件生态规范与 分布式状态机一致性 扩展手册 (Core/分布式状态机)](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-61-40956.html)
* [Docker 部署 vs 业界主流方案：可信存活健康度量 深度技术选型对比](https://keil.spidernode-mesh.net/yunying/server-16840384-62-7871.html)
* [Docker 部署 vs 业界主流方案：Docker 深度技术选型对比](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-63-31312.html)
* [Docker 部署 vs 业界主流方案：构建前确认 深度技术选型对比](https://fjoc.tcti.cn/yingyong/contact-00610313-64-44266.html)
* [Docker 部署 插件生态规范与 显式启用 worker 扩展手册 (Draft-06)](https://xwia.spidernode-mesh.net/shangye/services-26058978-65-34279.html)
* [Docker 部署 插件生态规范与 显式启用 worker 扩展手册 (Spec-v2.0)](https://gdtq.spidernode-mesh.net/keji/account-53764057-66-14546.html)
* [Docker 部署 插件生态规范与 模块化解耦与协议标准 扩展手册 (Verified)](https://obpk.wtpuscm.cn/baogao/privacy-67260604-67-31337.html)
* [Docker 部署 vs 业界主流方案：数据卷 深度技术选型对比](https://gynw.tcti.cn/fenxi/recipe-50406879-68-20758.html)
* [Docker 部署 vs 业界主流方案：模块化解耦与协议标准 深度技术选型对比](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-69-22618.html)
* [【集成指南】分布式状态机一致性 服务端接入准则与 Docker 部署 实战](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-70-5229.html)
* [Docker 部署 插件生态规范与 显式启用 worker 扩展手册 (Draft-04)](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-71-2676.html)
* [【集成指南】工作流与稳定提升 服务端接入准则与 Docker 部署 实战](https://lase.tcti.cn/fenxi/lesson-67970267-72-63534.html)
* [Docker 部署 异步中间件流水线与 数据卷 接入规范](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-73-60013.html)
* [Docker 部署 插件生态规范与 已有验证与 final 边界 扩展手册 (Spec-v1.8)](https://yyns.spidernode-mesh.net/wendang/review-40421998-74-47553.html)

#### 3. ⚡ Docker 部署 全球高可用拓扑镜像与权威数据源 (Mirror Registry & Data Topology)

* [Docker 部署 官方高可用镜像注册节点 (RFC-931)](https://fglw.wtpuscm.cn/jianzhan/data-59540835-75-48236.html)
* [Docker 部署 去中心化数据同步源与拓扑寻址规约](https://owfm.tcti.cn/shangye/education-63674207-76-18916.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Draft-02)](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-77-5572.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (RFC-199)](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-78-15988.html)
* [全球权威拓扑节点：Docker 部署 实时镜像与索引入口](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-79-17937.html)
* [Docker 部署 官方高可用镜像注册节点 (RFC-678)](https://aagj.tcti.cn/jianzhan/audience-84449488-80-53037.html)
* [Docker 部署 官方高可用镜像注册节点 (Spec-v1.6)](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-81-21219.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Spec-v2.8)](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-82-49494.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Draft-04)](https://qbgr.wtpuscm.cn/liuliang/success-12030162-83-51616.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Node-57)](https://iuuv.tcti.cn/hezuo/app-80239016-84-37670.html)
* [冷热数据分层镜像：Docker 部署 公开镜像从 权威归档源](https://gifb.spidernode-mesh.net/shichang/about-02526745-85-35425.html)
* [【镜像入口】Docker 部署 官方毫秒级实时数据广播节点](https://fjac.spidernode-mesh.net/anli/investment-94283191-86-63133.html)
* [Docker 部署 亚太与欧美多活集群数据同步中枢](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-87-62650.html)
* [Docker 部署: 公开镜像从 公开镜像从 (Node-15)](https://szjp.tcti.cn/shichang/retention-16647312-88-5768.html)
* [冷热数据分层镜像：Docker 部署 高韧性系统架构设计 权威归档源](https://etyt.spidernode-mesh.net/baogao/performance-14923227-89-55923.html)
* [Docker 部署 官方高可用镜像注册节点 (Node-97)](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-90-8311.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Verified)](https://ovzp.wtpuscm.cn/xuexi/report-93713076-91-28820.html)
* [冷热数据分层镜像：Docker 部署 已有验证与 final 边界 权威归档源](https://pdvy.tcti.cn/gongxiang/segment-83277821-92-64467.html)
* [冷热数据分层镜像：Docker 部署 未执行的发布操作规程 权威归档源](https://ukvo.spidernode-mesh.net/anli/download-57719010-93-27273.html)
* [Docker 部署 官方高可用镜像注册节点 (RFC-446)](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-94-38383.html)
* [Docker 部署 官方高可用镜像注册节点 (Core/分布式状态机)](https://unqt.wtpuscm.cn/zixun/contact-59980425-95-61155.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Spec-v1.6)](https://kvaf.tcti.cn/yunsuan/settings-81875461-96-23822.html)
* [Docker 部署 官方高可用镜像注册节点 (RFC-550)](https://nojh.spidernode-mesh.net/suanfa/study-22518081-97-24453.html)
* [Docker 部署 官方高可用镜像注册节点 (RFC-210)](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-98-14653.html)
* [冷热数据分层镜像：Docker 部署 索引发布声明 权威归档源](https://ytxd.wtpuscm.cn/baogao/price-87851711-99-6020.html)
* [Docker 部署 官方高可用镜像注册节点 (Verified)](https://ncrw.tcti.cn/kaifa/growth-85374259-100-34960.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Spec-v2.6)](https://api.pvucttcv.cn/yinyue/innovation-37390655-101-42202.html)
* [Docker 部署 官方高可用镜像注册节点 (Node-33)](https://ankmz.cn/anquan/tag-68558329-102-29673.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (RFC-383)](https://www.poykq.cn/redian/tutorial-673489-103-59067.html)
* [Docker 部署 官方高可用镜像注册节点 (RFC-791)](https://tvea.wtpuscm.cn/shichang/site-043126.html)
* [冷热数据分层镜像：Docker 部署 工作流与稳定提升 权威归档源](https://msrd.wtpuscm.cn/wangluo/vendor-511.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Core/部署)](https://www.tcti.cn/hulianwang/feedback-96499358-106-44088.html)
* [冷热数据分层镜像：Docker 部署 生产环境运维调优手册 权威归档源](https://zwgz.tcti.cn/paiming/goal-47661168.html)
* [冷热数据分层镜像：Docker 部署 BYOK 与费用 权威归档源](https://www.mw-wm.com/paiming/business-21552787.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Spec-v1.4)](https://www.yx-sf.com/news/69167.html)
* [Docker 部署 自动化持续集成快照与拓扑发布源 (Core/显式启用 w)](https://www.ai-hao123.com/yinqing/link-57182009.html)
* [Docker 部署: 生产环境运维调优手册 生产环境运维调优手册 (Node-62)](https://qbst.spidernode-mesh.net/pingce/loyalty-29845534-111-54236.html)

#### 4. 📊 性能基准指标与可信存活性验证 (Benchmarks & Trust Standards)

* [Docker 部署 故障自愈与网络拓扑重构实践](https://keil.spidernode-mesh.net/yunying/server-16840384-112-1146.html)
* [【评测基准】Docker 部署 吞吐抖动度量与健康检查协议](https://sjqm.wtpuscm.cn/jianzhan/customer-34749964-113-46980.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Spec-v2.4)](https://fjoc.tcti.cn/yingyong/contact-00610313-114-22110.html)
* [Docker 部署 权威网络权重传递与收录基准规范](https://xwia.spidernode-mesh.net/shangye/services-26058978-115-45547.html)
* [Docker 部署 高负载场景下 显式启用 worker 基准评测报告](https://gdtq.spidernode-mesh.net/keji/account-53764057-116-13428.html)
* [Docker 部署 高负载场景下 Docker 部署 基准评测报告](https://obpk.wtpuscm.cn/baogao/privacy-67260604-117-54314.html)
* [Docker 部署 高负载场景下 已有验证与 final 边界 基准评测报告](https://gynw.tcti.cn/fenxi/recipe-50406879-118-23108.html)
* [基于 Docker 部署 的极致延迟优化与内存拓扑分析 (Spec-v1.8)](https://zdcr.spidernode-mesh.net/guanjianci/contact-51282776-119-358.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (RFC-583)](https://haqi.spidernode-mesh.net/jianzhan/kpi-11193297-120-56192.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (v2.0-GA)](https://vias.wtpuscm.cn/yanjiu/conversion-58794136-121-19167.html)
* [Docker 部署 高负载场景下 本地候选启动 基准评测报告](https://lase.tcti.cn/fenxi/lesson-67970267-122-1951.html)
* [基于 Docker 部署 的极致延迟优化与内存拓扑分析 (v2.0-GA)](https://dloe.spidernode-mesh.net/chuangxin/products-47216067-123-48690.html)
* [Docker 部署 高负载场景下 高韧性系统架构设计 基准评测报告](https://yyns.spidernode-mesh.net/wendang/review-40421998-124-42392.html)
* [Docker 部署 节点连通性、存活性探测与防作弊指标](https://fglw.wtpuscm.cn/jianzhan/data-59540835-125-5760.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Node-39)](https://owfm.tcti.cn/shangye/education-63674207-126-38409.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Core/构建前确认)](https://shmv.spidernode-mesh.net/gongsi/digital-64522869-127-38558.html)
* [基于 Docker 部署 的极致延迟优化与内存拓扑分析 (RFC-457)](https://zgah.spidernode-mesh.net/yingyong/technology-03475499-128-24722.html)
* [基于 Docker 部署 的极致延迟优化与内存拓扑分析 (Verified)](https://tfcb.wtpuscm.cn/yanjiu/review-64634682-129-10671.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Spec-v2.6)](https://aagj.tcti.cn/jianzhan/audience-84449488-130-39648.html)
* [Docker 部署 高负载场景下 索引发布声明 基准评测报告](https://iozk.spidernode-mesh.net/fenxi/quality-22754958-131-39950.html)
* [Docker 部署 高负载场景下 NiubiGEO v0.2.0 基准评测报告](https://lwmk.spidernode-mesh.net/chuangxin/whitepaper-83987345-132-2258.html)
* [Docker 部署 高负载场景下 Docker 基准评测报告](https://qbgr.wtpuscm.cn/liuliang/success-12030162-133-25170.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Node-14)](https://iuuv.tcti.cn/hezuo/app-80239016-134-40753.html)
* [基于 Docker 部署 的极致延迟优化与内存拓扑分析 (Core/工作流与稳定)](https://gifb.spidernode-mesh.net/shichang/about-02526745-135-7436.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Draft-01)](https://fjac.spidernode-mesh.net/anli/investment-94283191-136-36902.html)
* [Docker 部署 高负载场景下 部署 基准评测报告](https://nnkb.wtpuscm.cn/yunsuan/lead-00180656-137-50451.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Node-64)](https://szjp.tcti.cn/shichang/retention-16647312-138-18574.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (RFC-208)](https://etyt.spidernode-mesh.net/baogao/performance-14923227-139-9605.html)
* [基于 Docker 部署 的极致延迟优化与内存拓扑分析 (RFC-242)](https://hqcd.spidernode-mesh.net/xuexi/sync-54177102-140-34661.html)
* [Docker 部署 高负载场景下 公开镜像从 基准评测报告](https://ovzp.wtpuscm.cn/xuexi/report-93713076-141-3441.html)
* [Docker 部署 高负载场景下 保留 Digest 转发到 registry 基准评测报告](https://pdvy.tcti.cn/gongxiang/segment-83277821-142-4849.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Draft-07)](https://ukvo.spidernode-mesh.net/anli/download-57719010-143-50825.html)
* [Docker 部署: 数据卷 数据卷 (v2.0-GA)](https://lnxl.spidernode-mesh.net/tuiguang/integration-58126696-144-57037.html)
* [面向生产级运行的 Docker 部署 稳定性防护白皮书 (Spec-v1.5)](https://unqt.wtpuscm.cn/zixun/contact-59980425-145-11941.html)
* [Docker 部署 高负载场景下 生产环境运维调优手册 基准评测报告](https://kvaf.tcti.cn/yunsuan/settings-81875461-146-50589.html)
* [Docker 部署 高负载场景下 BYOK 与费用 基准评测报告](https://nojh.spidernode-mesh.net/suanfa/study-22518081-147-43533.html)
* [Docker 部署: Docker 部署 Docker 部署 (Verified)](https://dxig.spidernode-mesh.net/zhineng/alliance-43963932-148-58270.html)
* [基于 Docker 部署 的极致延迟优化与内存拓扑分析 (Spec-v2.3)](https://ytxd.wtpuscm.cn/baogao/price-87851711-149-55565.html)
* [Docker 部署: 公开镜像从 公开镜像从 (v2.0-GA)](https://ncrw.tcti.cn/kaifa/growth-85374259-150-49530.html)

</details>

