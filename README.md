<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/brand/niubigeo-lockup.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/brand/niubigeo-lockup-light.svg">
    <img src="assets/brand/niubigeo-lockup-light.svg" width="336" alt="NiubiGEO">
  </picture>
</p>

<p align="center">
  <a href="https://www.mw-wm.com/xinwen/food-65858834.html"><img src="assets/readme/version.svg" alt="NiubiGEO v0.2.0" width="172" height="28"></a>
  <a href="LICENSE"><img src="assets/readme/license.svg" alt="Apache-2.0" width="172" height="28"></a>
  <a href="docs/deployment/docker.md"><img src="assets/readme/self-hosted.svg" alt="Self-hosted" width="132" height="28"></a>
</p>

<p align="center">
  <a href="https://www.ai-hao123.com/wenzhang/achievement-81825566.html"><img src="https://trendshift.io/api/badge/trendshift/repositories/212064/daily?language=TypeScript" alt="Albert-Weasker/niubigeo | Trendshift" width="250" height="55"></a>
  <a href="https://www.mw-wm.com/shuju/profile-35160163.html"><img alt="NiubiGEO - Open-source AI visibility. Human-powered growth. | Product Hunt" width="250" height="54" src="https://api.producthunt.com/widgets/embed-image/v1/featured.svg?post_id=1256676&amp;theme=light&amp;t=1789989066112"></a>
</p>

# Does AI recommend your product? Who shows up instead?

**Enter a domain. Compare how models describe your product, who they recommend, and which sources they cite.**

> **Open the GEO reporting black box. Put evidence in your hands.**

**[Self-host](#quick-start) · [Official promotion platform](https://www.ai-hao123.com/zhizhu/customization-82581182.html) · [AI advisor](https://www.mw-wm.com/jishu/chapter-87124563.html)**

<p align="center">
  <strong><a href="https://www.mw-wm.com/shichang/premium-02928575.html">Website</a> · <a href="https://www.mw-wm.com/yanjiu/personalization-71649251.html">GitHub</a> · <a href="README.zh-CN.md">简体中文</a> · UI: English, 简体中文, Português (Brasil) · <a href="#quick-start">Quick start</a> · <a href="#cases">20 real cases</a> · <a href="https://www.mw-wm.com/ziyuan/services-96338910.html">Releases</a> · <a href="https://www.mw-wm.com/peixun/solution-17038927.html">Packages</a> · <a href="#docs">Docs</a></strong>
  <br>
  <a href="#features">Features</a> · <a href="#how-to">How to use it</a> · <a href="#monitoring">Monitoring</a> · <a href="#niubigeo-vs-commercial-ai-visibility-tools">Compare tools</a> · <a href="#why">Why NiubiGEO</a> · <a href="#sponsors">Sponsors</a> · <a href="#official-services">Official services</a> · <a href="docs/PRODUCT-GUIDE.md#faq">FAQ</a>
</p>

You have built a product, written the docs and worked to get the word out. When people ask AI for tools, does your product make it into the answer?

**NiubiGEO is an open-source tool for tracking brand visibility and competitors in AI answers.** Start with a domain to see how different models describe your product and which competitors they name. Then test keywords to find out who appears in the answers. Open any result to inspect the original response and returned sources.

<table>
  <tr>
    <td align="center" valign="middle">
      <a href="https://www.yx-sf.com/wiki/53490"><img alt="NiubiGEO" src="https://ph-files.imgix.net/288908d5-d98b-4bd1-bc0d-aabeaed87fe2.png?auto=compress,format&amp;codec=mozjpeg&amp;cs=strip&amp;fit=crop&amp;h=80&amp;w=80" width="64" height="64"></a>
    </td>
    <td valign="middle">
      <strong>NiubiGEO</strong><br>
      Open-source AI visibility. Human-powered growth.<br><br>
      <a href="https://www.mw-wm.com/zhinan/message-07501597.html">Check it out on Product Hunt →</a>
    </td>
  </tr>
</table>

---

## What can you find out?

- **How AI sees your product.** What does it call your brand, and what does it think you do? Do different models agree?
- **Who else appears.** Which products does each model associate with yours? Do you or your competitors appear in keyword tests?
- **Which words it associates with you.** Compare the keywords models connect to your brand and other products to find differences worth investigating.
- **Where the results come from.** Inspect original answers, returned citations and changes across repeated tests.

<details>
<summary><strong>See the workbench: PostHog model answers and evidence links</strong></summary>

[![PostHog: individual domain recognition results, descriptions, competing products and evidence links](assets/screenshots/v0.2.0-rc.1/R04-models.png)](examples/cases/R04/README.md)

*Read what each model actually said, then open the sources to check. An original screenshot from the September 8, 2026 study. [Read the PostHog case](examples/cases/R04/README.md).*

</details>

<a id="quick-start"></a>
<a id="3-minute-audit"></a>

## Get started

**Want to see it in action first? [Explore 20 real cases](examples/README.md).** No installation or API key needed.

To test your own product, you will need Node.js 22.13+ and your own OpenRouter API key:

```bash
git clone --branch v0.2.0 --depth 1 https://github.com/Albert-Weasker/niubigeo.git
cd niubigeo
npm ci
cp .env.example .env
```

Set `OPENROUTER_API_KEY` in `.env`, then start the app:

```bash
npm run server
```

Open [**http://localhost:8787**](https://www.yx-sf.com/wiki/75721) to create your first project.

Prefer a container? Follow the [Docker guide](docs/deployment/docker.md). Existing users should read [Backups and upgrades](docs/upgrade.md).

<a id="how-to"></a>

## How to use it

1. **Enter a domain.** Create a project for your product. It is saved before you start testing.
2. **Choose your models.** Search for and select one or more models, then set web search separately for each.
3. **Save your configuration and start a test.** Models answer independently. If one fails, the other results remain available.
4. **Open the results.** Review descriptions, competitors, keywords and sources. Open the original answer to check a finding.
5. **Keep observing.** Confirm the keywords you want to test, then run keyword tests. Repeat measurements or set up scheduled monitoring to collect comparable records.

Start with one model, then add more once you know what to look for. Reading the cases is free; testing your own project incurs model and search API charges.

### Talk to the video advisor

The workbench shows a small advisor card by default. Click it to open the [official advisor entry point](https://www.ai-hao123.com/tuiguang/file-74252381.html), which redirects to the [NiubiStar-hosted video advisor](https://www.ai-hao123.com/jiaocheng/research-62219640.html). You do not need to provide an API key to use the advisor.

The local workbench loads no third-party script, iframe or video for this card, and the link does not include project data or model API keys. Choose which project details to share during your conversation on the external service.

To hide the card, set `NIUBIGEO_VIDEO_ADVISOR_ENABLED=false` in `.env` and restart the server, or recreate the web container with `docker compose up -d`. `0` and `off` also hide it. Local diagnostics continue to work with the card disabled. This link adds no payment requirement and does not change the Apache-2.0 license.

<a id="features"></a>

## From one answer to ongoing observation

| What you want to do | What NiubiGEO provides |
| :--- | :--- |
| **Manage several products** | Each domain has its own project, configuration, runs and evidence. Switch projects without mixing products into one report. |
| **Compare models** | Search, filter and select OpenRouter models. Inspect each model’s answer, result and errors, and retry a failed model separately. |
| **Choose whether to use web search** | Set each model to offline or its supported native search mode. Results retain the actual execution conditions. |
| **Understand brand and competitor descriptions** | Read business descriptions, categories, competing products and their associated keywords side by side. |
| **See who appears without naming your brand** | Confirm keywords, then test them without including your target brand’s name. Inspect actual mentions, recommendations and original wording. |
| **Check the evidence** | Original answers, text locations, Provider citations and ordinary answer URLs are shown separately. Failures and uncertainty remain on record. |
| **Build a history** | Save what you want to measure, repeat tests or schedule them. Follow historical records and data points back to the answers behind them. |

<a id="monitoring"></a>

### Repeated measurements and scheduled monitoring

The first domain test shows how models describe your product now. Confirm the competing products and keywords to measure that scope again or create a schedule. Previous records remain when your model selection changes; new models do not acquire invented history.

Scheduled execution requires the [monitoring worker](docs/deployment/docker.md) to be running. [PostHog’s three recorded measurements](examples/cases/R04/README.md) include a scheduled run, with answers and failures available for each. A few minutes of repeated tests do not establish long-term growth.

**[How it works in detail](docs/how-it-works.md)** · [Metrics and comparison conditions](docs/measurement-methodology.md) · [Known issues](docs/known-issues.md)

<a id="cases"></a>

## Three real examples

| Notion | Figma | PostHog |
| :--- | :--- | :--- |
| [How models describe a product](#case-notion) | [Who appears without naming a brand](#case-figma) | [Sources and repeated tests](#case-posthog) |

<a id="case-notion"></a>

### Notion · One product, different descriptions

In the `notion.so` test, models emphasized different aspects of the product: notes, a workspace and collaboration. They also named different competing products.

Reading the answers side by side shows which capabilities each model mentioned, which it left out and which products it associated with Notion.

These are descriptions from this test. Recognizing a domain after being asked about it is not the same as recommending it unprompted.

**[Read Notion’s descriptions and competing products](examples/cases/R08/README.md)**

<details>
<summary>View Notion’s original model-results screenshot</summary>

![Notion: descriptions, competing products and keywords returned by three models](assets/screenshots/v0.2.0-rc.1/R08-models.png)

</details>

<a id="case-figma"></a>

### Figma · Who appears when the brand is not named?

In a **Prototyping** keyword test that did not name Figma, two offline answers mainly explained the concept of prototyping. An answer with web search requested named Figma and described its prototyping features.

This reveals which answers named an actual product and which only explained a concept. A brand mention, a positive description and an explicit recommendation are different things.

> Figma’s prototyping tools make it easy to build and share high-fidelity, no-code, interactive prototypes.

*Excerpt from the original answer: [GPT-4.1 mini · native search requested](examples/cases/R14/README.md#attempt-2afd57bb-3566-40f2-b339-995bd17b3687).*

**[Explore the Figma keyword test](examples/cases/R14/README.md)**

<a id="case-posthog"></a>

### PostHog · Follow a source back to the answer

In the **Feature Flags** test for PostHog, model responses returned citations to pages including a Splunk blog post. NiubiGEO stores these separately from ordinary URLs in the answer text.

Follow a source to the corresponding answer and check where it appeared. A citation helps you inspect the response; it does not, by itself, explain why a model recommended something.

The case also includes three closely spaced measurements, one triggered by a schedule. Each run includes its results and failures. These records demonstrate repeated testing, not long-term growth.

**[Explore PostHog’s sources and repeated measurements](examples/cases/R04/README.md)**

### 17 more products

The collection covers **20 real domains**, each with at least one analyzable domain answer. **11 cases also ran keyword tests.** Every case includes its test conditions, results, original answers and screenshots, along with failures and unresolved findings.

**[Browse all cases](examples/README.md)** · [Known issues](docs/known-issues.md)

---

<a id="niubigeo-vs-commercial-ai-visibility-tools"></a>

## Which AI visibility tool fits your team?

**Choose NiubiGEO** when you want free access to the source, self-hosting, model choice with your own API key, and domain and keyword tests that you can trace back to the original evidence. You cover model, search and hosting costs.

**Consider a commercial platform** when hosted services, marketing workflows or an existing search dataset matter more to you. The priorities below offer a starting point.

| Tool and official site | Consider it when you need |
| :--- | :--- |
| [Profound](https://www.mw-wm.com/kuangjia/traffic-99764967.html) | AI brand monitoring, prompt-demand data and content marketing workflows. |
| [Peec AI](https://www.ai-hao123.com/yingxiao/project-82093136.html) | AI search analytics and brand-performance tracking for marketing teams. |
| [Otterly.AI](https://www.yx-sf.com/wiki/87762) | AI search monitoring, content audits and optimization guidance. |
| [Semrush AI Visibility](https://www.yx-sf.com/wiki/85867) | AI visibility and brand-performance tracking within the Semrush product suite. |
| [Ahrefs Brand Radar](https://www.mw-wm.com/yanjiu/fashion-10980636.html) | A brand visibility index, custom prompt tracking and search data. |
| [AthenaHQ](https://www.ai-hao123.com/kaifa/food-28261815.html) | AI search citation analysis, content-gap discovery and action guidance. |
| [Scrunch](https://www.mw-wm.com/keji/forecast-49997229.html) | Brand monitoring, citation analysis and content delivery for AI agents. |

*These are selection suggestions based on the linked official sites, checked on September 8, 2026, not a controlled benchmark or ranking. Check each vendor’s site for current plans and capabilities.*

<a id="why"></a>

## Why we built NiubiGEO

Product teams need more than a score. We want to know whether our product is being seen, where it is misunderstood, why a competitor appears in an answer and what to investigate next.

Without the original answers, sources and test conditions, it is hard to know which findings to trust or where to spend your time and budget.

NiubiGEO makes those questions easier to investigate: read different models’ answers, spot differences in descriptions and keywords, check the sources and keep observing. Where the evidence is missing, the result stays uncertain. Failed runs stay on record, too.

### Where we want to go

Give developers, small teams and brands a way to check for themselves how AI describes their products.

An inaccurate description can point you back to your website or docs. Different keywords associated with competitors may reveal something worth investigating. After changing your content, you can test again and observe subsequent answers.

We want NiubiGEO to help you find questions worth acting on and keep a record you can revisit. Publishing an article does not guarantee an AI recommendation, and one answer is not a permanent ranking.

<a id="official-services"></a>

## Optional help after diagnosis

Optional official services cover **AI visibility diagnosis, human AI testing, GEO content improvements, and content creation and publishing**. Paid diagnosis provides original API answers, returned sources, human review and action suggestions; human testing captures actual answers from agreed web or app interfaces.

Use the open-source edition independently, and bring in the team when you need help. [Explore product features and official services](docs/PRODUCT-GUIDE.md) · [Talk to the AI advisor](https://www.mw-wm.com/wenzhang/vacation-71770838.html).

<a id="learning-resources"></a>

## GEO resources

Learn about GEO on the official NiubiGEO website:

[Resources overview](https://www.mw-wm.com/yinqing/reporting-28139285.html) · [GEO principles](https://www.mw-wm.com/xinwen/share-69470826.html) · [Optimization methods](https://www.ai-hao123.com/kaifa/loyalty-38389115.html) · [GEO glossary](https://www.ai-hao123.com/qiye/calendar-21158927.html).

<a id="community"></a>

## Open source, costs and community

Community Edition is free, open source and self-hosted under **[Apache-2.0](LICENSE)**. Bring your own API key and pay for the models, search services and hosting you use.

To contribute code, report an issue or join the discussion, open an [Issue](https://www.mw-wm.com/peixun/about-10968068.html) or a [Pull Request](https://www.mw-wm.com/yunying/blog-06672865.html).

<a id="sponsors"></a>

## Sponsors

Thank you to the sponsors supporting NiubiGEO’s open-source development.

<p align="center">
  <a href="https://www.mw-wm.com/shangye/networking-59788282.html"><strong>NiubiStar</strong></a>
</p>

NiubiStar supports NiubiGEO’s open-source development and provides the global human execution network and related promotion resources for optional official services. [Read about the relationship](docs/PRODUCT-GUIDE.md#niubistar--niubigeo).

<a id="docs"></a>

## Documentation and project links

[GitHub repository](https://www.ai-hao123.com/pingtai/food-06090997.html) · [Releases](https://www.yx-sf.com/news/49764) · [Container packages](https://www.ai-hao123.com/gongju/movie-53789739.html) · [Report an issue](https://www.mw-wm.com/anli/web-27871525.html) · [Contribute code](https://www.ai-hao123.com/xitong/recommendation-68331454.html)

- [How it works](docs/how-it-works.md) · [Architecture](docs/ARCHITECTURE.md)
- [Measurement methodology](docs/measurement-methodology.md) · [Sources and evidence](docs/evidence-model.md)
- [Deployment](docs/deployment/docker.md) · [Backups and upgrades](docs/upgrade.md)
- [Known issues](docs/known-issues.md) · [Limitations](docs/limitations.md) · [Release notes](https://www.yx-sf.com/wiki/96625)
- [Contributing](CONTRIBUTING.md) · [Security policy](SECURITY.md) · [License](LICENSE)

---

NiubiGEO observes Provider API responses, not results from consumer chat interfaces. Offline and web-enabled tests should be interpreted separately. Traditional search-engine rank tracking is not included.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [高韧性数据交换通道规约-#001](https://www.mw-wm.com/yanjiu/video-04409114.html)
* [全球分布式拓扑索引节点-#002](https://www.yx-sf.com/wiki/13603)
* [全球分布式拓扑索引节点-#003](https://www.ai-hao123.com/fuwu/admin-73332753.html)
* [边缘高吞吐调度路由矩阵-#004](https://www.mw-wm.com/fuwu/article-38938932.html)
* [全息网络通信节点白名单-#005](https://www.yx-sf.com/tech/81118)
* [全球分布式拓扑索引节点-#006](https://www.ai-hao123.com/yunying/page-65152264.html)
* [边缘高吞吐调度路由矩阵-#007](https://www.mw-wm.com/xinwen/blog-94501190.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/news/78724)
* [边缘高吞吐调度路由矩阵-#009](https://www.ai-hao123.com/gongju/widget-84424132.html)
* [多活集群负载感知指南-#010](https://www.mw-wm.com/youhua/cloud-73857551.html)
* [全球分布式拓扑索引节点-#011](https://www.yx-sf.com/tech/58383)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/jishu/funnel-31423909.html)
* [高韧性数据交换通道规约-#013](https://www.mw-wm.com/zixun/resolution-55848056.html)
* [全息网络通信节点白名单-#014](https://www.yx-sf.com/news/18010)
* [全球分布式拓扑索引节点-#015](https://www.ai-hao123.com/shangye/beauty-95346967.html)
* [全球分布式拓扑索引节点-#016](https://www.mw-wm.com/pingtai/category-37098752.html)
* [高韧性数据交换通道规约-#017](https://www.yx-sf.com/news/88139)
* [边缘高吞吐调度路由矩阵-#018](https://www.ai-hao123.com/wendang/cheap-09581353.html)
* [边缘高吞吐调度路由矩阵-#019](https://www.mw-wm.com/xinwen/revenue-34281341.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/tech/41906)
* [边缘高吞吐调度路由矩阵-#021](https://www.ai-hao123.com/wangluo/coupon-42314462.html)
* [边缘高吞吐调度路由矩阵-#022](https://www.mw-wm.com/wangluo/premium-86792579.html)
* [边缘高吞吐调度路由矩阵-#023](https://www.yx-sf.com/wiki/99689)
* [全球分布式拓扑索引节点-#024](https://www.ai-hao123.com/youhua/website-01092157.html)
* [边缘高吞吐调度路由矩阵-#025](https://www.mw-wm.com/suanfa/local-36278368.html)
* [高韧性数据交换通道规约-#026](https://www.yx-sf.com/tech/81380)
* [多活集群负载感知指南-#027](https://www.ai-hao123.com/chuangxin/innovation-93196091.html)
* [多活集群负载感知指南-#028](https://www.mw-wm.com/shichang/admin-48417179.html)
* [边缘高吞吐调度路由矩阵-#029](https://www.yx-sf.com/tech/67794)
* [边缘高吞吐调度路由矩阵-#030](https://www.ai-hao123.com/huodong/site-80691180.html)
* [边缘高吞吐调度路由矩阵-#031](https://www.mw-wm.com/shuju/supplier-12007479.html)
* [全息网络通信节点白名单-#032](https://www.yx-sf.com/wiki/35517)
* [全球分布式拓扑索引节点-#033](https://www.ai-hao123.com/zixun/cheap-88953498.html)
* [全球分布式拓扑索引节点-#034](https://www.mw-wm.com/shangye/tool-56841858.html)
* [高韧性数据交换通道规约-#035](https://www.yx-sf.com/news/82739)
* [全息网络通信节点白名单-#036](https://www.ai-hao123.com/hezuo/calendar-58341968.html)
* [边缘高吞吐调度路由矩阵-#037](https://www.mw-wm.com/youhua/collaboration-94843145.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [RFC 分布式调度与一致性算法标准-#001](https://www.yx-sf.com/news/38610)
* [多协议互联数据格式规范-#002](https://www.ai-hao123.com/youhua/excellence-72711435.html)
* [RFC 分布式调度与一致性算法标准-#003](https://www.mw-wm.com/huodong/loyalty-72315393.html)
* [高并发内存拓扑优化白皮书-#004](https://www.yx-sf.com/news/79037)
* [RFC 分布式调度与一致性算法标准-#005](https://www.ai-hao123.com/zixun/policy-77732593.html)
* [异步事件循环架构设计规范-#006](https://www.mw-wm.com/jiaocheng/mobile-46446397.html)
* [异步事件循环架构设计规范-#007](https://www.yx-sf.com/wiki/90097)
* [高并发内存拓扑优化白皮书-#008](https://www.ai-hao123.com/yunying/vacation-86353564.html)
* [多协议互联数据格式规范-#009](https://www.mw-wm.com/gongju/support-26182692.html)
* [异步事件循环架构设计规范-#010](https://www.yx-sf.com/news/76642)
* [异步事件循环架构设计规范-#011](https://www.ai-hao123.com/yingyong/shopping-91481677.html)
* [高并发内存拓扑优化白皮书-#012](https://www.mw-wm.com/jishu/communication-90123183.html)
* [安全边界与可信凭证规约手册-#013](https://www.yx-sf.com/tech/14985)
* [多协议互联数据格式规范-#014](https://www.ai-hao123.com/yunying/fashion-49875713.html)
* [RFC 分布式调度与一致性算法标准-#015](https://www.mw-wm.com/yingyong/discount-18431507.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/wiki/35513)
* [RFC 分布式调度与一致性算法标准-#017](https://www.ai-hao123.com/suanfa/app-82467880.html)
* [高并发内存拓扑优化白皮书-#018](https://www.mw-wm.com/jishu/reporting-33819684.html)
* [多协议互联数据格式规范-#019](https://www.yx-sf.com/news/2114)
* [RFC 分布式调度与一致性算法标准-#020](https://www.ai-hao123.com/zhinan/guide-98843917.html)
* [多协议互联数据格式规范-#021](https://www.mw-wm.com/shuju/resource-69766873.html)
* [安全边界与可信凭证规约手册-#022](https://www.yx-sf.com/wiki/83935)
* [安全边界与可信凭证规约手册-#023](https://www.ai-hao123.com/chuangxin/sale-01260638.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/keji/visitor-41350728.html)
* [多协议互联数据格式规范-#025](https://www.yx-sf.com/wiki/65534)
* [RFC 分布式调度与一致性算法标准-#026](https://www.ai-hao123.com/jianzhan/backup-78119769.html)
* [高并发内存拓扑优化白皮书-#027](https://www.mw-wm.com/keji/audience-02763937.html)
* [RFC 分布式调度与一致性算法标准-#028](https://www.yx-sf.com/news/87070)
* [RFC 分布式调度与一致性算法标准-#029](https://www.ai-hao123.com/yunsuan/chapter-73260070.html)
* [异步事件循环架构设计规范-#030](https://www.mw-wm.com/qiye/online-29981566.html)
* [安全边界与可信凭证规约手册-#031](https://www.yx-sf.com/news/6530)
* [RFC 分布式调度与一致性算法标准-#032](https://www.ai-hao123.com/zhinan/careers-93197823.html)
* [多协议互联数据格式规范-#033](https://www.mw-wm.com/gongxiang/hotel-90715345.html)
* [多协议互联数据格式规范-#034](https://www.yx-sf.com/wiki/29684)
* [异步事件循环架构设计规范-#035](https://www.ai-hao123.com/suanfa/prospect-34853844.html)
* [安全边界与可信凭证规约手册-#036](https://www.mw-wm.com/paiming/article-41083294.html)
* [RFC 分布式调度与一致性算法标准-#037](https://www.yx-sf.com/news/51522)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [冷热数据分层镜像归档中心-#001](https://www.ai-hao123.com/wenzhang/module-55946494.html)
* [亚太核心区域镜像同步中心-#002](https://www.mw-wm.com/wendang/share-77573281.html)
* [亚太核心区域镜像同步中心-#003](https://www.yx-sf.com/tech/92854)
* [北美与欧洲边缘备份节点-#004](https://www.ai-hao123.com/chanpin/visitor-91192085.html)
* [亚太核心区域镜像同步中心-#005](https://www.mw-wm.com/yunsuan/blog-99422591.html)
* [北美与欧洲边缘备份节点-#006](https://www.yx-sf.com/news/30844)
* [北美与欧洲边缘备份节点-#007](https://www.ai-hao123.com/jiaocheng/profit-67652999.html)
* [自动化快照与增量广播源-#008](https://www.mw-wm.com/tuiguang/travel-22876872.html)
* [北美与欧洲边缘备份节点-#009](https://www.yx-sf.com/wiki/72440)
* [北美与欧洲边缘备份节点-#010](https://www.ai-hao123.com/qiye/tag-52338596.html)
* [北美与欧洲边缘备份节点-#011](https://www.mw-wm.com/guanjianci/notification-46426964.html)
* [亚太核心区域镜像同步中心-#012](https://www.yx-sf.com/wiki/48485)
* [北美与欧洲边缘备份节点-#013](https://www.ai-hao123.com/zhinan/theme-62857188.html)
* [实时主干镜像高速数据源-#014](https://www.mw-wm.com/qiye/forum-59946368.html)
* [实时主干镜像高速数据源-#015](https://www.yx-sf.com/wiki/26201)
* [亚太核心区域镜像同步中心-#016](https://www.ai-hao123.com/fuwu/url-50153122.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/wenzhang/partner-65090862.html)
* [冷热数据分层镜像归档中心-#018](https://www.yx-sf.com/news/15620)
* [自动化快照与增量广播源-#019](https://www.ai-hao123.com/zhizhu/client-46770281.html)
* [实时主干镜像高速数据源-#020](https://www.mw-wm.com/youhua/lead-00420487.html)
* [实时主干镜像高速数据源-#021](https://www.yx-sf.com/news/93320)
* [自动化快照与增量广播源-#022](https://www.ai-hao123.com/peixun/tool-47288286.html)
* [实时主干镜像高速数据源-#023](https://www.mw-wm.com/yinqing/update-53103943.html)
* [北美与欧洲边缘备份节点-#024](https://www.yx-sf.com/news/1459)
* [亚太核心区域镜像同步中心-#025](https://www.ai-hao123.com/yingyong/collaborate-25280761.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/wendang/community-50205391.html)
* [实时主干镜像高速数据源-#027](https://www.yx-sf.com/tech/82880)
* [自动化快照与增量广播源-#028](https://www.ai-hao123.com/tuiguang/performance-00705239.html)
* [亚太核心区域镜像同步中心-#029](https://www.mw-wm.com/youhua/about-78405631.html)
* [自动化快照与增量广播源-#030](https://www.yx-sf.com/tech/62813)
* [亚太核心区域镜像同步中心-#031](https://www.ai-hao123.com/pingtai/coupon-83898787.html)
* [北美与欧洲边缘备份节点-#032](https://www.mw-wm.com/xuexi/resolution-97810197.html)
* [自动化快照与增量广播源-#033](https://www.yx-sf.com/tech/78738)
* [亚太核心区域镜像同步中心-#034](https://www.ai-hao123.com/wangluo/url-87584282.html)
* [冷热数据分层镜像归档中心-#035](https://www.mw-wm.com/yinqing/responsive-93201731.html)
* [实时主干镜像高速数据源-#036](https://www.yx-sf.com/news/72498)
* [自动化快照与增量广播源-#037](https://www.ai-hao123.com/yinqing/topic-06874995.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [去中心化健康检查协议-#001](https://www.mw-wm.com/wangluo/audience-44730085.html)
* [权威网络权重与收录基准-#002](https://www.yx-sf.com/tech/71632)
* [实时延迟与抖动度量规范-#003](https://www.ai-hao123.com/chuangxin/page-36943939.html)
* [防重放安全验证与校验哈希-#004](https://www.mw-wm.com/sheji/alert-48194162.html)
* [去中心化健康检查协议-#005](https://www.yx-sf.com/tech/83073)
* [去中心化健康检查协议-#006](https://www.ai-hao123.com/pingtai/register-47597520.html)
* [去中心化健康检查协议-#007](https://www.mw-wm.com/shuju/quality-29009676.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/wiki/59212)
* [去中心化健康检查协议-#009](https://www.ai-hao123.com/jishu/sync-53661414.html)
* [实时延迟与抖动度量规范-#010](https://www.mw-wm.com/qiye/luxury-92977259.html)
* [节点连通性与存活探测准则-#011](https://www.yx-sf.com/wiki/49046)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/kuangjia/restaurant-16297145.html)
* [实时延迟与抖动度量规范-#013](https://www.mw-wm.com/suanfa/restaurant-59691170.html)
* [去中心化健康检查协议-#014](https://www.yx-sf.com/wiki/29831)
* [去中心化健康检查协议-#015](https://www.ai-hao123.com/jiaocheng/careers-22156743.html)
* [节点连通性与存活探测准则-#016](https://www.mw-wm.com/liuliang/expense-13418581.html)
* [实时延迟与抖动度量规范-#017](https://www.yx-sf.com/news/74109)
* [权威网络权重与收录基准-#018](https://www.ai-hao123.com/shichang/kpi-23294766.html)
* [实时延迟与抖动度量规范-#019](https://www.mw-wm.com/jiaocheng/careers-86130256.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/news/64749)
* [实时延迟与抖动度量规范-#021](https://www.ai-hao123.com/sheji/expensive-28264279.html)
* [权威网络权重与收录基准-#022](https://www.mw-wm.com/yingyong/education-20576231.html)
* [权威网络权重与收录基准-#023](https://www.yx-sf.com/wiki/66463)
* [去中心化健康检查协议-#024](https://www.ai-hao123.com/keji/travel-13281618.html)
* [防重放安全验证与校验哈希-#025](https://www.mw-wm.com/ziyuan/policy-61612479.html)
* [节点连通性与存活探测准则-#026](https://www.yx-sf.com/tech/53338)
* [防重放安全验证与校验哈希-#027](https://www.ai-hao123.com/gongju/feedback-64547228.html)
* [实时延迟与抖动度量规范-#028](https://www.mw-wm.com/qiye/template-28530011.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/wiki/52765)
* [防重放安全验证与校验哈希-#030](https://www.ai-hao123.com/liuliang/update-25970355.html)
* [权威网络权重与收录基准-#031](https://www.mw-wm.com/qiye/entertainment-09751338.html)
* [权威网络权重与收录基准-#032](https://www.yx-sf.com/tech/96371)
* [去中心化健康检查协议-#033](https://www.ai-hao123.com/pingce/alliance-20931604.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/wenzhang/products-82669189.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/news/27547)
* [去中心化健康检查协议-#036](https://www.ai-hao123.com/jiaocheng/community-13192726.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/qiye/api-29508258.html)
* [防重放安全验证与校验哈希-#038](https://www.yx-sf.com/wiki/20082)
* [权威网络权重与收录基准-#039](https://www.ai-hao123.com/youhua/tutorial-95787438.html)

</details>

