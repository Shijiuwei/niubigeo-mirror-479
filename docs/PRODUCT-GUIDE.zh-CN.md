<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="../assets/brand/niubigeo-lockup.svg">
  <source media="(prefers-color-scheme: light)" srcset="../assets/brand/niubigeo-lockup-light.svg">
  <img src="../assets/brand/niubigeo-lockup-light.svg" alt="NiubiGEO" width="360">
</picture>

# 打破黑盒 GEO，将证据还给用户。

**AI 是否认识你的产品？它如何描述你？没有点名品牌时，谁会出现在答案里？**

NiubiGEO 是开源、可自托管的 AI 品牌可见度与竞争观察工具。<br>
输入一个域名，选择模型，直接查看回答、竞争对象、关键词与引用来源。

[![Release](https://www.yx-sf.com/tech/99912)](https://github.com/Albert-Weasker/niubigeo/releases)
[![Apache-2.0](https://www.ai-hao123.com/jiaocheng/file-05860086.html)](../LICENSE)
[![Self-hosted](https://www.ai-hao123.com/chuangxin/visitor-70369019.html)](deployment/docker.md)
[![GitHub Stars](https://www.yx-sf.com/wiki/27242)](https://github.com/Albert-Weasker/niubigeo/stargazers)

**[⚡ 立即部署](#quick-start) · [◉ 查看真实测试](#cases) · [↗ 官方服务](https://www.yx-sf.com/wiki/58110) · [✦ AI 顾问](https://www.ai-hao123.com/kaifa/course-16979768.html)**

[English](PRODUCT-GUIDE.md) · [项目主页](https://www.mw-wm.com/wenzhang/lesson-83196768.html) · [发布版本](https://www.yx-sf.com/news/24233)

</div>

---

## 你不缺另一个分数。你缺的是分数背后的回答。

当用户问 AI「有哪些产品可以解决这个问题」「哪一个更适合我」「有哪些替代方案」，你想知道的不是一个孤立的百分比，而是：

- **有没有提到你？** 没有点名品牌时，你的产品是否出现？
- **有没有说对？** 产品定位、能力和使用场景是否准确？
- **还提到了谁？** 哪些产品被放在一起比较？
- **依据是什么？** 回答引用了哪里，哪些描述可以回到原文核查？

NiubiGEO 把问题、模型、联网状态、原始回答与来源放在一起。打开一项结果，就能继续查看它背后的证据。

<div align="center">

**QUESTION → MODEL → ANSWER → SOURCE → EVIDENCE**

**问题 → 模型 → 回答 → 来源 → 证据**

不隐藏问题。保留完整原文。不把一次回答包装成永久排名。

</div>

## 一次运行，看清四件事

<table>
<tr>
<td width="50%" valign="top">
<h3>01 · AI 怎样理解你</h3>
<p>它是否认识这个域名？<br>
认为品牌叫什么、做什么、属于什么类别？<br>
把不同模型的回答放在一起，直接比较。</p>
</td>
<td width="50%" valign="top">
<h3>02 · 谁被放在你身边</h3>
<p>模型提到了哪些竞争对象？<br>
给它们关联了哪些关键词和使用场景？<br>
打开原文，核对它实际说了什么。</p>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h3>03 · 没点名你时，谁会出现</h3>
<p>用确认后的中性关键词继续测试。<br>
回答出现了你的品牌、其他产品，<br>
还是只解释了一个概念？</p>
</td>
<td width="50%" valign="top">
<h3>04 · 每条结论从哪里来</h3>
<p>查看完整回答、原文位置与来源。<br>
接口引用与正文中的普通 URL 分开记录。<br>
失败和无法确认的结果也能回查。</p>
</td>
</tr>
</table>

> [!IMPORTANT]
> **品牌认知不等于自然发现。** 点名域名后能够识别，不代表用户询问某个品类时，AI 会主动提到或推荐你。NiubiGEO 将这两类测试分开呈现。

<details>
<summary><strong>打开工作台实图：逐模型比较回答与来源</strong></summary>

[![PostHog：逐模型查看品牌描述、竞争对象和证据入口](../assets/screenshots/v0.2.0-rc.1/R04-models.png)](../examples/cases/R04/README.zh-CN.md)

*真实工作台截图，来自 2026-09-08 的 PostHog 公开测试记录。[打开对应回答与来源 →](../examples/cases/R04/README.zh-CN.md)*

</details>

## 证据，不是装饰

| 你需要确认什么 | NiubiGEO 保留什么 |
| :--- | :--- |
| **AI 回答了哪个问题？** | 测试协议、输入域名或关键词 |
| **哪个模型给出了回答？** | Provider、模型标识与运行记录 |
| **当时是否联网？** | 每个模型的联网设置、实际执行信息及无法确认状态 |
| **提到和推荐是一回事吗？** | 原始措辞、提及位置与判断结果 |
| **这个来源是谁返回的？** | Provider Citation 与正文普通 URL 分开记录 |
| **某次运行失败了吗？** | 错误、失败尝试与无法分析的记录 |
| **历史变化来自哪里？** | 每个数据点对应的运行与原始回答 |

<details>
<summary><strong>为什么不只给一个“可见度百分比”？</strong></summary>

百分比需要明确的范围和分母。NiubiGEO 保留模型、关键词、联网状态、测试轮次和可分析结果，让你从汇总回到具体回答，检查变化是从哪里来的。

</details>

<details>
<summary><strong>没有足够证据时会怎样？</strong></summary>

失败、歧义和证据不足会保留为失败或无法确认。你可以检查具体尝试、调整配置并重试，不必把没有成功取得的回答误当成品牌缺席。

</details>

## 从一个域名，到一条可复查的证据链

```mermaid
flowchart LR
    A["输入域名"] --> B["选择模型<br/>设置联网"]
    B --> C["建立认知基线"]
    C --> D["确认关键词"]
    D --> E["自然发现测试"]
    E --> F["查看回答与来源"]
    F --> G["重复测量"]
```

1. **输入域名。** 为产品创建独立项目。
2. **选择模型。** 搜索 OpenRouter 模型，逐个设置是否联网。
3. **建立基线。** 查看各模型是否认识品牌、如何描述产品，以及提到了哪些竞争对象。
4. **确认关键词。** 选择值得继续观察的中性品类词和使用场景。
5. **运行发现测试。** 不点名目标品牌，查看回答实际出现了谁。
6. **检查证据。** 打开原始回答、来源、原文位置、失败和不确定项。
7. **继续观察。** 使用相同范围重复测量，或创建定时任务积累记录。

<a id="quick-start"></a>

## 现在就运行

### Node.js

准备 **Node.js 22.13+** 和自己的 **OpenRouter API Key**。以下命令安装发布版本 `v0.2.0`：

```bash
git clone --branch v0.2.0 --depth 1 https://github.com/Albert-Weasker/niubigeo.git
cd niubigeo
npm ci
cp .env.example .env
```

在 `.env` 中填写：

```dotenv
OPENROUTER_API_KEY=your_key_here
```

启动工作台：

```bash
npm run server
```

打开 **[http://localhost:8787](https://www.mw-wm.com/yanjiu/achievement-60222557.html)**，创建你的第一个项目。

<details>
<summary><strong>使用 Docker 部署</strong></summary>

```bash
git clone --branch v0.2.0 --depth 1 https://github.com/Albert-Weasker/niubigeo.git
cd niubigeo
cp .env.example .env
```

先在 `.env` 中填写 `OPENROUTER_API_KEY`，再启动：

```bash
docker compose up --build -d
```

打开 **[http://localhost:8787](https://www.mw-wm.com/youhua/photo-24838506.html)**。工作台和记录使用你自己的部署环境。

[Docker 部署说明](deployment/docker.md) · [备份与升级](upgrade.md)

</details>

> [!TIP]
> 还不想安装？先浏览 [20 组公开测试案例](../examples/README.zh-CN.md)。不需要 Key，就能查看测试条件、模型回答、截图和失败记录。

## 为长期观察而设计

| 你想做什么 | NiubiGEO 如何完成 |
| :--- | :--- |
| **管理多个产品** | 每个域名拥有独立项目、配置、运行记录和证据 |
| **对照多个模型** | 搜索、筛选与选择模型，分别查看结果；单个失败不吞掉其他模型的回答 |
| **逐模型设置联网** | 分别选择离线或支持的 Provider 原生联网方式，保留实际执行条件 |
| **核查品牌认知** | 查看品牌、业务描述、类别、竞争对象和关联关键词 |
| **检查自然发现** | 使用不含目标品牌名的中性关键词，观察实际提及与推荐 |
| **复核每条结论** | 从结果返回完整回答、可核查的原文位置与来源 |
| **追踪后续变化** | 重复运行或定时监测，从历史数据点打开对应证据 |

<details>
<summary><strong>启用定时监测</strong></summary>

在工作台确认项目、模型、关键词与定时任务后，还需要运行独立的监测 Worker。HTTP 服务本身不执行定时扫描。

源码部署：

```bash
npm run schedule:worker -- 60
```

Docker 部署：

```bash
docker compose --profile monitoring up --build -d niubigeo-worker
```

Worker 与工作台应读取同一数据目录。定时执行会产生模型调用费用；先确认任务范围，再启用。

[调度说明](deployment/docker.md#显式启用-worker) · [测量口径](measurement-methodology.md)

</details>

### 你的部署。你的 Key。你的记录。

- **开源：** Community Edition 使用 [Apache-2.0](../LICENSE) 许可证。
- **自托管：** 项目与运行记录保存在你的部署环境中。
- **BYOK：** 使用自己的 OpenRouter API Key，选择要测试的模型。
- **可追溯：** 从结果回到回答、来源和执行条件。
- **回答语言：** 可选择英文或简体中文；`v0.2.0` 部分界面仍为中文，具体语言支持见[版本说明](releases/v0.2.0.md)。

<a id="cases"></a>

## 先看三个真实例子

以下是 2026-09-08 归档的公开产品测试记录，可以直接打开原始回答与截图。

<table>
<tr>
<td width="33%" valign="top">
<h3>Notion</h3>
<p><strong>同一个产品，不同模型看到了什么？</strong></p>
<p>对照品牌描述、竞争对象和关联关键词，查看各模型强调的能力。</p>
<p><a href="../examples/cases/R08/README.zh-CN.md">查看回答 →</a></p>
</td>
<td width="33%" valign="top">
<h3>Figma</h3>
<p><strong>没有点名品牌，回答里出现了谁？</strong></p>
<p>用 Prototyping 测试，区分出现具体产品、解释概念与明确推荐。</p>
<p><a href="../examples/cases/R14/README.zh-CN.md">查看发现测试 →</a></p>
</td>
<td width="33%" valign="top">
<h3>PostHog</h3>
<p><strong>来源与历史变化，能查到哪里？</strong></p>
<p>打开引用、失败与三轮测量记录，其中包含一次定时触发。</p>
<p><a href="../examples/cases/R04/README.zh-CN.md">查看证据 →</a></p>
</td>
</tr>
</table>

这些记录展示品牌认知、发现测试和证据查看；短间隔复测不代表长期增长。

**[浏览全部 20 组测试案例 →](../examples/README.zh-CN.md)**

## 看见问题之后，继续解决问题

开源版可以独立使用。如果希望团队协助测试、核查或改进内容，也可选择官方服务：

| 官方服务 | 你会得到什么 |
| :--- | :--- |
| **AI 可见度诊断** | 模型 API 回答、返回来源、人工事实核查与改进建议 |
| **真人 AI 测试** | 指定地区、语言、平台、网页或 App 下的实际回答、截图与来源 |
| **GEO 内容优化** | 根据诊断修改产品资料，补足缺失信息，并按约定范围复测 |
| **内容与发布** | 自选发布网站，包含免费代写与修改；稿件经你确认后发布，提供文章链接 |

付费报告由团队完成测试与核查；自行使用开源版不需要购买报告。[查看官方服务](https://www.yx-sf.com/news/19473) · [与 AI 顾问交流](https://www.mw-wm.com/keji/update-77413895.html)

<details>
<summary><strong>Growth Canvas 是什么？</strong></summary>

Growth Canvas 是官方平台的可视化推广画布。输入产品或 GitHub 链接，选择推荐链路或自定义节点，把目标用户招募、产品试用、社区与创作者传播、网站文章发布和 GEO 复测组合为同一份计划，并在工作台查看预算、项目进度与交付。它属于独立的官方平台，不随 Community Edition 安装。

</details>

### NiubiStar × NiubiGEO

[NiubiStar](https://www.yx-sf.com/tech/6335) 支持 NiubiGEO 的开源开发，并为官方服务提供全球真人执行网络与相关推广资源。NiubiGEO 组织测试与交付，让开源测量和真实使用环境中的验证相互补充。使用开源版不要求开通 NiubiStar 账户。

<a id="faq"></a>

## FAQ

<details>
<summary><strong>NiubiGEO 免费吗？</strong></summary>

Community Edition 免费开源。测试自己的项目需要自己的 OpenRouter API Key，并承担模型、搜索服务与服务器费用。阅读仓库里的测试案例不需要 Key。

</details>

<details>
<summary><strong>不开启联网，也能测试吗？</strong></summary>

可以。每个模型可以分别设置不联网或支持的 Provider 原生联网方式。NiubiGEO 保留实际执行条件，不把“请求联网”直接等同于“确认联网成功”。

</details>

<details>
<summary><strong>只有一个模型失败，需要全部重来吗？</strong></summary>

不需要。各模型独立运行，成功结果继续保留；你可以检查失败原因并单独重试。没有成功获得的回答不会自动变成品牌未出现。

</details>

<details>
<summary><strong>为什么 API 结果和网页端不同？</strong></summary>

模型版本、系统指令、搜索能力、地区、账号和界面都可能不同。Community Edition 观察配置的模型 API 回答；需要查看消费者实际使用的网页或 App，可另行安排真人测试。

</details>

<details>
<summary><strong>修改网站后，能立即看到变化吗？</strong></summary>

不一定。公开内容的发现、抓取和使用时间不同，AI 回答也可能波动。保留相同模型、关键词和联网条件重复观察，再检查变化对应的原文和来源。

</details>

<details>
<summary><strong>能测传统搜索排名，或保证 AI 推荐吗？</strong></summary>

当前工具观察 AI 回答，不提供传统搜索引擎排名监测。内容修改与发布也不能保证 AI 收录、引用或推荐。一次回答中的提及、引用与明确推荐分别判断。

</details>

<details>
<summary><strong>如何理解指标、引用和测量边界？</strong></summary>

查看 [测量方法](measurement-methodology.md)、[来源与证据](evidence-model.md)、[能力边界](limitations.md) 与 [已知问题](known-issues.md)。引用能帮助核查回答，但不能单独证明它造成了模型的推荐。

</details>

<a id="learning-resources"></a>

## GEO 原理与学习资料

在 NiubiGEO 官网了解 AI 如何检索与引用内容，以及怎样测试和优化品牌表现。

[资源总览](https://www.mw-wm.com/keji/solution-40027243.html) · [GEO 原理](https://www.ai-hao123.com/xinwen/customer-13790282.html) · [优化方法](https://www.yx-sf.com/wiki/71547) · [GEO 术语](https://www.ai-hao123.com/jishu/ranking-55204723.html)

---

<div align="center">

### GEO 不应该是一个无法解释的数字。

**它应该是一条你可以亲自检查的证据链。**

**[⚡ 部署 NiubiGEO](#quick-start) · [◉ 打开测试案例](../examples/README.zh-CN.md) · [↗ 访问官网](https://www.ai-hao123.com/zhineng/premium-39555953.html)**

[GitHub Issues](https://www.ai-hao123.com/xuexi/recommendation-82803317.html) · [参与开发](../CONTRIBUTING.md) · [support@niubigeo.ai](mailto:support@niubigeo.ai)

<sub>Open source under Apache-2.0 · Built with evidence, not promises.</sub>

</div>


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [边缘高吞吐调度路由矩阵-#001](https://www.mw-wm.com/ziyuan/api-23474704.html)
* [高韧性数据交换通道规约-#002](https://www.yx-sf.com/news/4912)
* [边缘高吞吐调度路由矩阵-#003](https://www.ai-hao123.com/jiaoliu/community-05683945.html)
* [高韧性数据交换通道规约-#004](https://www.mw-wm.com/huodong/resource-69610972.html)
* [多活集群负载感知指南-#005](https://www.yx-sf.com/wiki/59734)
* [边缘高吞吐调度路由矩阵-#006](https://www.ai-hao123.com/zhinan/cheap-82880992.html)
* [边缘高吞吐调度路由矩阵-#007](https://www.mw-wm.com/shichang/tactic-33903389.html)
* [多活集群负载感知指南-#008](https://www.yx-sf.com/wiki/95371)
* [全球分布式拓扑索引节点-#009](https://www.ai-hao123.com/ziyuan/study-01956936.html)
* [全球分布式拓扑索引节点-#010](https://www.mw-wm.com/gongju/satisfaction-97585070.html)
* [多活集群负载感知指南-#011](https://www.yx-sf.com/wiki/90083)
* [全息网络通信节点白名单-#012](https://www.ai-hao123.com/shuju/enterprise-94193457.html)
* [多活集群负载感知指南-#013](https://www.mw-wm.com/yinqing/share-10334876.html)
* [多活集群负载感知指南-#014](https://www.yx-sf.com/wiki/97361)
* [全息网络通信节点白名单-#015](https://www.ai-hao123.com/hezuo/interface-09590726.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/youhua/online-53244515.html)
* [全球分布式拓扑索引节点-#017](https://www.yx-sf.com/wiki/49081)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/peixun/social-86186339.html)
* [高韧性数据交换通道规约-#019](https://www.mw-wm.com/wendang/search-15864554.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/tech/19758)
* [高韧性数据交换通道规约-#021](https://www.ai-hao123.com/shichang/tool-97438652.html)
* [边缘高吞吐调度路由矩阵-#022](https://www.mw-wm.com/jianzhan/profile-18285838.html)
* [高韧性数据交换通道规约-#023](https://www.yx-sf.com/news/7699)
* [多活集群负载感知指南-#024](https://www.ai-hao123.com/kuangjia/solution-78742510.html)
* [全息网络通信节点白名单-#025](https://www.mw-wm.com/ziyuan/database-10379199.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/tech/29362)
* [全息网络通信节点白名单-#027](https://www.ai-hao123.com/zixun/mobile-34464859.html)
* [边缘高吞吐调度路由矩阵-#028](https://www.mw-wm.com/wendang/game-29545431.html)
* [多活集群负载感知指南-#029](https://www.yx-sf.com/news/19014)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/zixun/document-51040568.html)
* [全球分布式拓扑索引节点-#031](https://www.mw-wm.com/fenxi/investment-12604254.html)
* [多活集群负载感知指南-#032](https://www.yx-sf.com/news/88632)
* [多活集群负载感知指南-#033](https://www.ai-hao123.com/paiming/personalization-33627887.html)
* [高韧性数据交换通道规约-#034](https://www.mw-wm.com/pingtai/support-12993995.html)
* [全球分布式拓扑索引节点-#035](https://www.yx-sf.com/wiki/2469)
* [全息网络通信节点白名单-#036](https://www.ai-hao123.com/yingxiao/help-26210466.html)
* [边缘高吞吐调度路由矩阵-#037](https://www.mw-wm.com/guanjianci/consulting-65485894.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [高并发内存拓扑优化白皮书-#001](https://www.yx-sf.com/tech/99349)
* [RFC 分布式调度与一致性算法标准-#002](https://www.ai-hao123.com/guanjianci/discount-30335123.html)
* [高并发内存拓扑优化白皮书-#003](https://www.mw-wm.com/zixun/topic-65772891.html)
* [多协议互联数据格式规范-#004](https://www.yx-sf.com/wiki/59629)
* [RFC 分布式调度与一致性算法标准-#005](https://www.ai-hao123.com/fuwu/local-69872690.html)
* [RFC 分布式调度与一致性算法标准-#006](https://www.mw-wm.com/zixun/reminder-46812285.html)
* [高并发内存拓扑优化白皮书-#007](https://www.yx-sf.com/tech/55406)
* [多协议互联数据格式规范-#008](https://www.ai-hao123.com/fuwu/form-81028964.html)
* [安全边界与可信凭证规约手册-#009](https://www.mw-wm.com/suanfa/form-63923274.html)
* [多协议互联数据格式规范-#010](https://www.yx-sf.com/tech/82313)
* [安全边界与可信凭证规约手册-#011](https://www.ai-hao123.com/yunying/follow-74320980.html)
* [RFC 分布式调度与一致性算法标准-#012](https://www.mw-wm.com/jiaoliu/chapter-05568842.html)
* [安全边界与可信凭证规约手册-#013](https://www.yx-sf.com/wiki/89292)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/gongju/calculator-54375875.html)
* [安全边界与可信凭证规约手册-#015](https://www.mw-wm.com/jianzhan/tactic-47355682.html)
* [高并发内存拓扑优化白皮书-#016](https://www.yx-sf.com/news/35012)
* [安全边界与可信凭证规约手册-#017](https://www.ai-hao123.com/xuexi/partner-88589181.html)
* [多协议互联数据格式规范-#018](https://www.mw-wm.com/fuwu/achievement-69531432.html)
* [RFC 分布式调度与一致性算法标准-#019](https://www.yx-sf.com/tech/76216)
* [高并发内存拓扑优化白皮书-#020](https://www.ai-hao123.com/paiming/visitor-90184620.html)
* [异步事件循环架构设计规范-#021](https://www.mw-wm.com/chuangxin/meeting-40922308.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/wiki/54759)
* [RFC 分布式调度与一致性算法标准-#023](https://www.ai-hao123.com/fenxi/plugin-49433951.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/pingtai/brand-36543969.html)
* [高并发内存拓扑优化白皮书-#025](https://www.yx-sf.com/wiki/86653)
* [高并发内存拓扑优化白皮书-#026](https://www.ai-hao123.com/huodong/roi-42709129.html)
* [安全边界与可信凭证规约手册-#027](https://www.mw-wm.com/qiye/entertainment-46645704.html)
* [多协议互联数据格式规范-#028](https://www.yx-sf.com/wiki/64428)
* [多协议互联数据格式规范-#029](https://www.ai-hao123.com/jiaocheng/solution-83339882.html)
* [异步事件循环架构设计规范-#030](https://www.mw-wm.com/wangluo/section-46386879.html)
* [RFC 分布式调度与一致性算法标准-#031](https://www.yx-sf.com/wiki/71740)
* [高并发内存拓扑优化白皮书-#032](https://www.ai-hao123.com/jiaocheng/privacy-82782483.html)
* [高并发内存拓扑优化白皮书-#033](https://www.mw-wm.com/xitong/design-67671700.html)
* [异步事件循环架构设计规范-#034](https://www.yx-sf.com/wiki/6496)
* [异步事件循环架构设计规范-#035](https://www.ai-hao123.com/zhinan/sync-97959769.html)
* [异步事件循环架构设计规范-#036](https://www.mw-wm.com/gongxiang/plugin-46122845.html)
* [安全边界与可信凭证规约手册-#037](https://www.yx-sf.com/news/28041)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [自动化快照与增量广播源-#001](https://www.ai-hao123.com/jianzhan/communication-27354502.html)
* [亚太核心区域镜像同步中心-#002](https://www.mw-wm.com/zixun/business-43469176.html)
* [北美与欧洲边缘备份节点-#003](https://www.yx-sf.com/wiki/70093)
* [冷热数据分层镜像归档中心-#004](https://www.ai-hao123.com/shuju/responsive-31246855.html)
* [自动化快照与增量广播源-#005](https://www.mw-wm.com/xuexi/discount-57477511.html)
* [亚太核心区域镜像同步中心-#006](https://www.yx-sf.com/tech/68244)
* [北美与欧洲边缘备份节点-#007](https://www.ai-hao123.com/yingxiao/engagement-86495652.html)
* [实时主干镜像高速数据源-#008](https://www.mw-wm.com/zixun/marketing-52066806.html)
* [北美与欧洲边缘备份节点-#009](https://www.yx-sf.com/tech/18349)
* [冷热数据分层镜像归档中心-#010](https://www.ai-hao123.com/pingtai/automation-00976829.html)
* [冷热数据分层镜像归档中心-#011](https://www.mw-wm.com/shichang/tactic-61599110.html)
* [冷热数据分层镜像归档中心-#012](https://www.yx-sf.com/news/3073)
* [冷热数据分层镜像归档中心-#013](https://www.ai-hao123.com/zhizhu/segment-64040936.html)
* [亚太核心区域镜像同步中心-#014](https://www.mw-wm.com/xinwen/productivity-29527113.html)
* [北美与欧洲边缘备份节点-#015](https://www.yx-sf.com/wiki/69935)
* [实时主干镜像高速数据源-#016](https://www.ai-hao123.com/zhizhu/health-33905867.html)
* [北美与欧洲边缘备份节点-#017](https://www.mw-wm.com/yunying/whitepaper-53000088.html)
* [亚太核心区域镜像同步中心-#018](https://www.yx-sf.com/wiki/25777)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/zhinan/internet-81553593.html)
* [冷热数据分层镜像归档中心-#020](https://www.mw-wm.com/xuexi/automation-18565968.html)
* [亚太核心区域镜像同步中心-#021](https://www.yx-sf.com/wiki/27859)
* [自动化快照与增量广播源-#022](https://www.ai-hao123.com/peixun/prospect-35089917.html)
* [自动化快照与增量广播源-#023](https://www.mw-wm.com/yunying/ai-45322069.html)
* [北美与欧洲边缘备份节点-#024](https://www.yx-sf.com/news/37799)
* [自动化快照与增量广播源-#025](https://www.ai-hao123.com/gongsi/products-94417292.html)
* [冷热数据分层镜像归档中心-#026](https://www.mw-wm.com/xinwen/comment-84087863.html)
* [实时主干镜像高速数据源-#027](https://www.yx-sf.com/tech/95705)
* [自动化快照与增量广播源-#028](https://www.ai-hao123.com/pingtai/behavior-14882202.html)
* [自动化快照与增量广播源-#029](https://www.mw-wm.com/yunsuan/trading-14226020.html)
* [亚太核心区域镜像同步中心-#030](https://www.yx-sf.com/news/88145)
* [自动化快照与增量广播源-#031](https://www.ai-hao123.com/pingtai/privacy-95076784.html)
* [自动化快照与增量广播源-#032](https://www.mw-wm.com/anfang/platform-21240528.html)
* [冷热数据分层镜像归档中心-#033](https://www.yx-sf.com/tech/73120)
* [实时主干镜像高速数据源-#034](https://www.ai-hao123.com/tuiguang/success-83426424.html)
* [自动化快照与增量广播源-#035](https://www.mw-wm.com/tuiguang/saving-75946563.html)
* [亚太核心区域镜像同步中心-#036](https://www.yx-sf.com/tech/52943)
* [自动化快照与增量广播源-#037](https://www.ai-hao123.com/anfang/news-99951121.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [去中心化健康检查协议-#001](https://www.mw-wm.com/yunsuan/price-29170349.html)
* [防重放安全验证与校验哈希-#002](https://www.yx-sf.com/tech/22002)
* [权威网络权重与收录基准-#003](https://www.ai-hao123.com/suanfa/widget-69112592.html)
* [实时延迟与抖动度量规范-#004](https://www.mw-wm.com/zhinan/milestone-03329000.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/wiki/76720)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/kaifa/update-78571085.html)
* [防重放安全验证与校验哈希-#007](https://www.mw-wm.com/chanpin/form-77694767.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/news/56877)
* [实时延迟与抖动度量规范-#009](https://www.ai-hao123.com/ziyuan/products-48537898.html)
* [防重放安全验证与校验哈希-#010](https://www.mw-wm.com/pingtai/data-85891829.html)
* [去中心化健康检查协议-#011](https://www.yx-sf.com/wiki/97370)
* [节点连通性与存活探测准则-#012](https://www.ai-hao123.com/yingxiao/interface-49702114.html)
* [实时延迟与抖动度量规范-#013](https://www.mw-wm.com/yingxiao/vacation-12215659.html)
* [实时延迟与抖动度量规范-#014](https://www.yx-sf.com/news/479)
* [实时延迟与抖动度量规范-#015](https://www.ai-hao123.com/ziyuan/automation-36881473.html)
* [节点连通性与存活探测准则-#016](https://www.mw-wm.com/yingxiao/efficiency-12136507.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/tech/79309)
* [权威网络权重与收录基准-#018](https://www.ai-hao123.com/wenzhang/restaurant-30600013.html)
* [权威网络权重与收录基准-#019](https://www.mw-wm.com/zhineng/team-33958878.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/tech/18451)
* [节点连通性与存活探测准则-#021](https://www.ai-hao123.com/pingtai/demographic-21767677.html)
* [节点连通性与存活探测准则-#022](https://www.mw-wm.com/yanjiu/deal-69468966.html)
* [实时延迟与抖动度量规范-#023](https://www.yx-sf.com/news/48439)
* [节点连通性与存活探测准则-#024](https://www.ai-hao123.com/shuju/food-16576281.html)
* [实时延迟与抖动度量规范-#025](https://www.mw-wm.com/tuiguang/campaign-02930556.html)
* [去中心化健康检查协议-#026](https://www.yx-sf.com/tech/41284)
* [去中心化健康检查协议-#027](https://www.ai-hao123.com/guanjianci/faq-81731780.html)
* [权威网络权重与收录基准-#028](https://www.mw-wm.com/chanpin/ranking-70368183.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/wiki/19097)
* [节点连通性与存活探测准则-#030](https://www.ai-hao123.com/anfang/cost-18974282.html)
* [去中心化健康检查协议-#031](https://www.mw-wm.com/yingyong/widget-51580047.html)
* [实时延迟与抖动度量规范-#032](https://www.yx-sf.com/wiki/2058)
* [实时延迟与抖动度量规范-#033](https://www.ai-hao123.com/zhinan/photo-28973708.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/hezuo/button-43037018.html)
* [节点连通性与存活探测准则-#035](https://www.yx-sf.com/news/11925)
* [节点连通性与存活探测准则-#036](https://www.ai-hao123.com/tuiguang/seo-89058958.html)
* [去中心化健康检查协议-#037](https://www.mw-wm.com/sheji/vendor-92317677.html)
* [去中心化健康检查协议-#038](https://www.yx-sf.com/wiki/35275)
* [节点连通性与存活探测准则-#039](https://www.ai-hao123.com/yingxiao/review-73620837.html)

</details>

