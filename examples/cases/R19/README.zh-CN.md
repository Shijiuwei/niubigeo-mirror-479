# R19 · n8n.io

[English](./README.md) · [全部案例](../../README.zh-CN.md)

## 本次实际结果

一个联网回答没列竞争对象；“开源软件”关键词存在第一名冲突。

初始 D：3/3 条当前回答可分析；测量 D：3/3 条首次回答可分析；K：4/6 条首次回答可分析。这些是回答覆盖计数，不是认识率或产品指标分母。

执行状态: **部分完成**.

**该指标存在一致性冲突，暂不用于排名比较。** 下列唯一第一名字段仍保留原始值，不选择冠军，也不解释为并列。

- [firstMentionState · 4da15ebb-7308-4388-bde7-c8f7cf3dbcc6](../../../docs/known-issues.md#conflict-4da15ebb-7308-4388-bde7-c8f7cf3dbcc6-firstmentionstate)

![n8n.io：各模型域名认知结果](../../../assets/screenshots/v0.2.0-rc.1/R19-models.png)

R19 · n8n.io · D · 3 条归档尝试 · openai/gpt-4o-mini（off）、google/gemini-2.5-flash-lite（off）、openai/gpt-4.1-mini（provider_native） · 2026-09-08T06:13:55.945Z 至 2026-09-08T06:13:55.945Z。保留原始失败状态。 截图时间: 2026-09-08T07:19:14.726Z.

## 测试条件

输入域名: n8n.io. 回答语言: zh.

协议: D = domain-recognition/v1; K = keyword-discovery/v1.

D 只接收域名、语言、固定协议与模型配置。K 只接收已冻结的中性关键词。分类标签不发送给模型。

- openai/gpt-4o-mini · off
- google/gemini-2.5-flash-lite · off
- openai/gpt-4.1-mini · provider_native

## 各模型的描述

### Google: Gemini 2.5 Flash Lite

**运行时间:** 2026-09-08T06:13:55.945Z

domainRecognition: recognized · analysisStatus: recognized · localAnalysis: complete.

Attempt: 3ff409be-7003-4ce2-90dc-d2c3669b1fbb · completed · executionMode: unverified.

品牌: n8n

业务: 一个开源的、可扩展的工作流自动化工具，允许用户连接各种应用程序和服务，并自动化重复性任务。

原文位置: UTF-16 [185, 230) · [打开完整回答](#attempt-3ff409be-7003-4ce2-90dc-d2c3669b1fbb)

类别: 工作流自动化

目标关键词: 工作流自动化, 开源, 节点式编程, 集成

竞争对象:

- Zapier · zapier.com: 一个流行的集成平台，允许用户连接不同的Web应用程序并自动化工作流程。. 关键词: 工作流自动化, 应用集成
- Make (formerly Integromat) · make.com: 一个强大的可视化自动化平台，用于连接应用程序和创建复杂的工作流程。. 关键词: 工作流自动化, 可视化编程
- IFTTT · ifttt.com: 一个简单的服务，用于连接应用程序和设备，创建基于触发器的自动化。. 关键词: 工作流自动化, 物联网

无法确认: —


<a id="attempt-3ff409be-7003-4ce2-90dc-d2c3669b1fbb"></a>

<details><summary>查看模型原始回答</summary>

<pre>{
  "domainRecognition": "recognized",
  "analysisStatus": "recognized",
  "recognizedBrand": {
    "value": "n8n",
    "citationUrls": []
  },
  "businessDescription": {
    "value": "一个开源的、可扩展的工作流自动化工具，允许用户连接各种应用程序和服务，并自动化重复性任务。",
    "citationUrls": []
  },
  "productCategory": {
    "value": "工作流自动化",
    "citationUrls": []
  },
  "competitors": [
    {
      "name": "Zapier",
      "domain": "zapier.com",
      "businessDescription": "一个流行的集成平台，允许用户连接不同的Web应用程序并自动化工作流程。",
      "productCategory": "工作流自动化",
      "keywords": [
        {
          "keyword": "工作流自动化",
          "citationUrls": []
        },
        {
          "keyword": "应用集成",
          "citationUrls": []
        }
      ],
      "citationUrls": []
    },
    {
      "name": "Make (formerly Integromat)",
      "domain": "make.com",
      "businessDescription": "一个强大的可视化自动化平台，用于连接应用程序和创建复杂的工作流程。",
      "productCategory": "工作流自动化",
      "keywords": [
        {
          "keyword": "工作流自动化",
          "citationUrls": []
        },
        {
          "keyword": "可视化编程",
          "citationUrls": []
        }
      ],
      "citationUrls": []
    },
    {
      "name": "IFTTT",
      "domain": "ifttt.com",
      "businessDescription": "一个简单的服务，用于连接应用程序和设备，创建基于触发器的自动化。",
      "productCategory": "工作流自动化",
      "keywords": [
        {
          "keyword": "工作流自动化",
          "citationUrls": []
        },
        {
          "keyword": "物联网",
          "citationUrls": []
        }
      ],
      "citationUrls": []
    }
  ],
  "brandKeywords": [
    {
      "keyword": "工作流自动化",
      "citationUrls": []
    },
    {
      "keyword": "开源",
      "citationUrls": []
    },
    {
      "keyword": "节点式编程",
      "citationUrls": []
    },
    {
      "keyword": "集成",
      "citationUrls": []
    }
  ],
  "unknowns": []
}</pre>

</details>

SHA-256: `630ae8f7e5cf49bdb793bbfc3547b75917f00011a9371a209fb189c46c3ff440`

[原始回答、字段位置与尝试记录](./public-evidence.json) · SHA-256: `630ae8f7e5cf49bdb793bbfc3547b75917f00011a9371a209fb189c46c3ff440`

<details><summary>关键词与原文位置</summary>

| 归属 | 关键词 | 原文 / UTF-16 位置 |
|---|---|---|
| n8n | 工作流自动化 | 工作流自动化 [195, 201) |
| n8n | 开源 | 开源 [187, 189) |
| n8n | 节点式编程 | 节点式编程 [1689, 1694) |
| n8n | 集成 | 集成 [449, 451) |
| Zapier | 工作流自动化 | 工作流自动化 [195, 201) |
| Zapier | 应用集成 | 应用集成 [650, 654) |
| Make (formerly Integromat) | 工作流自动化 | 工作流自动化 [195, 201) |
| Make (formerly Integromat) | 可视化编程 | 可视化编程 [1049, 1054) |
| IFTTT | 工作流自动化 | 工作流自动化 [195, 201) |
| IFTTT | 物联网 | 物联网 [1428, 1431) |

</details>

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

此 Attempt 未归档正文 URL。

### OpenAI: GPT-4.1 Mini

**运行时间:** 2026-09-08T06:13:55.945Z

domainRecognition: recognized · analysisStatus: recognized · localAnalysis: complete.

Attempt: be7daa2f-b34d-43b3-8380-d981df4c0926 · completed · executionMode: native.

品牌: n8n

业务: n8n是一款可扩展的工作流自动化工具，允许用户通过开放模型将任何事物连接到一切。

原文位置: UTF-16 [164, 204) · [打开完整回答](#attempt-be7daa2f-b34d-43b3-8380-d981df4c0926)

类别: 工作流自动化平台

目标关键词: 工作流自动化, 可扩展

竞争对象:

本次未列出竞争对象；这不表示现实中没有。

无法确认: —


<a id="attempt-be7daa2f-b34d-43b3-8380-d981df4c0926"></a>

<details><summary>查看模型原始回答</summary>

<pre>{"domainRecognition":"recognized","analysisStatus":"recognized","recognizedBrand":{"value":"n8n","citationUrls":["https://n8n.io"]},"businessDescription":{"value":"n8n是一款可扩展的工作流自动化工具，允许用户通过开放模型将任何事物连接到一切。","citationUrls":["https://n8n.io"]},"productCategory":{"value":"工作流自动化平台","citationUrls":["https://n8n.io"]},"competitors":[],"brandKeywords":[{"keyword":"工作流自动化","citationUrls":["https://n8n.io"]},{"keyword":"可扩展","citationUrls":["https://n8n.io"]}],"unknowns":[]}</pre>

</details>

SHA-256: `dfe15c40b5928f95125ad1272062656166e50d86e502d291fa3a47259aabe01f`

[原始回答、字段位置与尝试记录](./public-evidence.json) · SHA-256: `dfe15c40b5928f95125ad1272062656166e50d86e502d291fa3a47259aabe01f`

<details><summary>关键词与原文位置</summary>

| 归属 | 关键词 | 原文 / UTF-16 位置 |
|---|---|---|
| n8n | 工作流自动化 | 工作流自动化 [174, 180) |
| n8n | 可扩展 | 可扩展 [170, 173) |

</details>

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

- [https://n8n.io/](<https://n8n.io/>)

### OpenAI: GPT-4o-mini

**运行时间:** 2026-09-08T06:13:55.945Z

domainRecognition: recognized · analysisStatus: recognized · localAnalysis: complete.

Attempt: c923f080-0b05-42e5-9135-df8aa461ac3c · completed · executionMode: unverified.

品牌: n8n

业务: 开源自动化工作流工具

原文位置: UTF-16 [148, 158) · [打开完整回答](#attempt-c923f080-0b05-42e5-9135-df8aa461ac3c)

类别: 自动化软件

目标关键词: 开源, 工作流自动化

竞争对象:

- Zapier · zapier.com: 在线自动化工具. 关键词: 自动化, 工作流
- Integromat · integromat.com: 在线自动化平台. 关键词: 自动化, 集成

无法确认: —


<a id="attempt-c923f080-0b05-42e5-9135-df8aa461ac3c"></a>

<details><summary>查看模型原始回答</summary>

<pre>{"domainRecognition":"recognized","analysisStatus":"recognized","recognizedBrand":{"value":"n8n","citationUrls":[]},"businessDescription":{"value":"开源自动化工作流工具","citationUrls":[]},"productCategory":{"value":"自动化软件","citationUrls":[]},"competitors":[{"name":"Zapier","domain":"zapier.com","businessDescription":"在线自动化工具","productCategory":"自动化软件","keywords":[{"keyword":"自动化","citationUrls":[]},{"keyword":"工作流","citationUrls":[]}],"citationUrls":[]},{"name":"Integromat","domain":"integromat.com","businessDescription":"在线自动化平台","productCategory":"自动化软件","keywords":[{"keyword":"自动化","citationUrls":[]},{"keyword":"集成","citationUrls":[]}],"citationUrls":[]}],"brandKeywords":[{"keyword":"开源","citationUrls":[]},{"keyword":"工作流自动化","citationUrls":[]}],"unknowns":[]}</pre>

</details>

SHA-256: `a60dd0d52ec026cffc717c9ae5603821f07788ed77918e9847ff3b986da57bd6`

[原始回答、字段位置与尝试记录](./public-evidence.json) · SHA-256: `a60dd0d52ec026cffc717c9ae5603821f07788ed77918e9847ff3b986da57bd6`

<details><summary>关键词与原文位置</summary>

| 归属 | 关键词 | 原文 / UTF-16 位置 |
|---|---|---|
| n8n | 开源 | 开源 [148, 150) |
| n8n | 工作流自动化 | 工作流自动化 [722, 728) |
| Zapier | 自动化 | 自动化 [150, 153) |
| Zapier | 工作流 | 工作流 [153, 156) |
| Integromat | 自动化 | 自动化 [150, 153) |
| Integromat | 集成 | 集成 [614, 616) |

</details>

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

此 Attempt 未归档正文 URL。

## 中性关键词测试

工作流自动化, 开源

K valid 仅指首次 Attempt 的回答可分析，不是产品指标分母。各指标使用归档统计点的 samples、included 和 judgment；后续成功重试不替换此覆盖计数。

筛选记录、原文位置和排除理由见证据文件。每个同条件回答同时观察目标和其他实体，不把离线与联网差异解释为模型优劣。

### 工作流自动化 · openai/gpt-4.1-mini

keywordId: watch-keyword-36c2f8cbc226e0eb5473ee97 · runId: 63f6121d-fe18-42e0-8d0e-390cc64d3abf · probeId: 20342b8e-4cd8-40f3-a110-763ae16935fd

provider_native · failed · firstAttemptId: 1198351c-76a2-4261-8e96-493d1796f12b

analysisStatus: analysis_failed · resultAttemptId: 1198351c-76a2-4261-8e96-493d1796f12b

- mentionJudgment: unknown
- recommendationJudgment: unknown


无法确认: Unterminated string in JSON at position 3327 (line 1 column 3328)

[实际请求与原文证据](./public-evidence.json)

#### Attempt 1198351c-76a2-4261-8e96-493d1796f12b

analysis_failed · 时间: 2026-09-08T06:14:13.565Z · 首次 Attempt

requestedSearch: provider_native · used: true · executionMode: native

OpenRouter metadata confirmed provider-native web search.

错误: analysis_failed · Unterminated string in JSON at position 3327 (line 1 column 3328)

finish_reason: stop

<a id="attempt-1198351c-76a2-4261-8e96-493d1796f12b"></a>

<details><summary>查看模型原始回答</summary>

<pre>{"analysisStatus":"completed","mentions":[{"name":"Power Automate","domain":"www.microsoft.com","recommendation":"mentioned","mentionQuote":"Power Automate：业务流程工作流自动化 | Microsoft Power Platform","recommendationQuote":"Power Automate：业务流程工作流自动化 | Microsoft Power Platform","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Slickflow","domain":"www.slickflow.com","recommendation":"mentioned","mentionQuote":"Slickflow - AI多智能体工作流引擎 | LLM · RAG · Agent","recommendationQuote":"Slickflow - AI多智能体工作流引擎 | LLM · RAG · Agent","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"FlowSpark","domain":"flowspark.net","recommendation":"mentioned","mentionQuote":"FlowSpark - 企业级AI智能体 | 智能工作流自动化平台","recommendationQuote":"FlowSpark - 企业级AI智能体 | 智能工作流自动化平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Atlassian","domain":"www.atlassian.com","recommendation":"mentioned","mentionQuote":"自动化 - 内置于 Atlassian 平台 | Atlassian","recommendationQuote":"自动化 - 内置于 Atlassian 平台 | Atlassian","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Zoho Flow","domain":"www.zoho.com.cn","recommendation":"mentioned","mentionQuote":"Zoho Flow：自动化工作流的集成平台","recommendationQuote":"Zoho Flow：自动化工作流的集成平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"IBM","domain":"www.ibm.com","recommendation":"mentioned","mentionQuote":"工作流自动化解决方案：利用 AI 优化业务流程与运营效率 | IBM","recommendationQuote":"工作流自动化解决方案：利用 AI 优化业务流程与运营效率 | IBM","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"n8n","domain":"n8n.io","recommendation":"mentioned","mentionQuote":"n8n：开源自动化工作流平台","recommendationQuote":"n8n：开源自动化工作流平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Make","domain":"www.make.com","recommendation":"mentioned","mentionQuote":"Make：可视化多步骤自动化平台","recommendationQuote":"Make：可视化多步骤自动化平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Zapier","domain":"zapier.com","recommendation":"mentioned","mentionQuote":"Zapier：自动化工作流平台","recommendationQuote":"Zapier：自动化工作流平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Activepieces","domain":"www.activepieces.com","recommendation":"mentioned","mentionQuote":"Activepieces：开源自动化平台","recommendationQuote":"Activepieces：开源自动化平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"IFTTT","domain":"ifttt.com","recommendation":"mentioned","mentionQuote":"IFTTT：自动化工作流平台","recommendationQuote":"IFTTT：自动化工作流平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"F2BPM","domain":"www.f2bpm.com","recommendation":"mentioned","mentionQuote":"F2BPM工作流引擎-产品","recommendationQuote":"F2BPM工作</pre>

</details>

SHA-256: `27399a6f21eaedfa9e25563106c5d1c9c9f17e4b56821239f7073f574ddf0207`

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

此 Attempt 未归档正文 URL。

### 开源 · openai/gpt-4.1-mini

keywordId: watch-keyword-5cfe28a6c05be5db74ab8acb · runId: 63f6121d-fe18-42e0-8d0e-390cc64d3abf · probeId: c3a249cc-3ad9-45f0-b9a4-c6ae20e88ac6

provider_native · failed · firstAttemptId: 02ee613a-5e8d-461e-a3e4-eedf5c4662d2

analysisStatus: analysis_failed · resultAttemptId: 02ee613a-5e8d-461e-a3e4-eedf5c4662d2

- mentionJudgment: unknown
- recommendationJudgment: unknown


无法确认: Unterminated string in JSON at position 2676 (line 1 column 2677)

[实际请求与原文证据](./public-evidence.json)

#### Attempt 02ee613a-5e8d-461e-a3e4-eedf5c4662d2

analysis_failed · 时间: 2026-09-08T06:14:24.167Z · 首次 Attempt

requestedSearch: provider_native · used: true · executionMode: native

OpenRouter metadata confirmed provider-native web search.

错误: analysis_failed · Unterminated string in JSON at position 2676 (line 1 column 2677)

finish_reason: stop

<a id="attempt-02ee613a-5e8d-461e-a3e4-eedf5c4662d2"></a>

<details><summary>查看模型原始回答</summary>

<pre>{"analysisStatus":"completed","mentions":[{"name":"ByteZoneX","domain":"www.bytezonex.com","recommendation":"mentioned","mentionQuote":"ByteZoneX 提供了按用途、平台、部署方式和开源状态筛选开源工具与软件的功能。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"多码网","domain":"www.somanycode.com","recommendation":"mentioned","mentionQuote":"多码网是一个免费公益的代码项目分享网站，收录了 52,489+ 个开源源码项目与 663+ 个 Awesome 精选合集。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"云图AI","domain":"www.yuntusuo.com","recommendation":"mentioned","mentionQuote":"云图AI 聚合 AI 工具、Agent 框架、Workflow、数据库、DevOps 与云原生软件，提供项目介绍、GitHub 数据、官方下载地址、替代产品和 Docker 部署指南。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"GitHubStore","domain":"githubstore.cc","recommendation":"mentioned","mentionQuote":"GitHubStore 精选 AI 工具、智能体与 MCP 技能，实时评分与趋势追踪。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"ReelOS.ai","domain":"www.reelos.ai","recommendation":"mentioned","mentionQuote":"ReelOS.ai 提供了一个开源方案库，收录了 1158 个开源与部分开源项目，涵盖 11 个领域。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"B3log","domain":"b3log.org","recommendation":"mentioned","mentionQuote":"B3log 是一个开源社区，已开源了多款产品，如 Sym、Solo、Pipe、Vditor、Lute、思源笔记等。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"约会开源","domain":"ossdate.com","recommendation":"mentioned","mentionQuote":"约会开源提供了开源软件的文档，包括 CMS、静态站点生成器、博客、个人主页导航、知识管理、项目管理、运维管理等分类。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"酷特喵","domain":"www.kutmd.com","recommendation":"mentioned","mentionQuote":"酷特喵是专业 AI 工具导航平台，汇集 AI 聊天、绘画、编程、办公等 20+ 热门分类，覆盖写作、视频、数据分析等实用工具。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"开源空间","domain":"opensource.zone","recommendation":"mentioned","mentionQuote":"开源空间提供了精选开源替代方案，包括项目管理、文档协作、开发工具等常用 SaaS 的免费与自托管替代方案。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"思</pre>

</details>

SHA-256: `852d008cb370bc973b3bf56b8ec207b5040c14b88fcf9896835a5a0bc78458cf`

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

此 Attempt 未归档正文 URL。

### 工作流自动化 · google/gemini-2.5-flash-lite

keywordId: watch-keyword-36c2f8cbc226e0eb5473ee97 · runId: 63f6121d-fe18-42e0-8d0e-390cc64d3abf · probeId: 799dbba5-391d-47e5-98a1-755f9d6a5ae1

off · completed · firstAttemptId: d569e043-86b9-4e98-a33e-5e7fbc692d55

analysisStatus: completed · resultAttemptId: d569e043-86b9-4e98-a33e-5e7fbc692d55

- mentionJudgment: adjudicable
- recommendationJudgment: adjudicable

- 工作流自动化: mentioned · mention: 工作流自动化 · recommendation: — · attemptId: d569e043-86b9-4e98-a33e-5e7fbc692d55

无法确认: —

[实际请求与原文证据](./public-evidence.json)

#### Attempt d569e043-86b9-4e98-a33e-5e7fbc692d55

completed · 时间: 2026-09-08T06:14:07.050Z · 首次 Attempt

requestedSearch: off · used: false · executionMode: unverified

finish_reason: stop

<a id="attempt-d569e043-86b9-4e98-a33e-5e7fbc692d55"></a>

<details><summary>查看模型原始回答</summary>

<pre>{
  "analysisStatus": "completed",
  "mentions": [
    {
      "name": "工作流自动化",
      "domain": null,
      "recommendation": "mentioned",
      "mentionQuote": "工作流自动化",
      "recommendationQuote": null,
      "firstMentionOffset": 0,
      "firstRecommendationOffset": null,
      "firstMentionState": "unique",
      "firstRecommendationState": "none"
    }
  ],
  "unknowns": []
}</pre>

</details>

SHA-256: `91fe71ebd2dfa0e1f91db29174a309f9eed85ff1498cf660bf3e527f901b3138`

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

此 Attempt 未归档正文 URL。

### 开源 · google/gemini-2.5-flash-lite

keywordId: watch-keyword-5cfe28a6c05be5db74ab8acb · runId: 63f6121d-fe18-42e0-8d0e-390cc64d3abf · probeId: 9a6c55ac-4ff4-443a-b8dc-fea4ffd7470c

off · completed · firstAttemptId: 38cf6f46-9cc5-41bb-95c6-a6be8031a438

analysisStatus: completed · resultAttemptId: 38cf6f46-9cc5-41bb-95c6-a6be8031a438

- mentionJudgment: adjudicable
- recommendationJudgment: adjudicable

- 开源: mentioned · mention: 开源 · recommendation: — · attemptId: 38cf6f46-9cc5-41bb-95c6-a6be8031a438

无法确认: —

[实际请求与原文证据](./public-evidence.json)

#### Attempt 38cf6f46-9cc5-41bb-95c6-a6be8031a438

completed · 时间: 2026-09-08T06:14:14.955Z · 首次 Attempt

requestedSearch: off · used: false · executionMode: unverified

finish_reason: stop

<a id="attempt-38cf6f46-9cc5-41bb-95c6-a6be8031a438"></a>

<details><summary>查看模型原始回答</summary>

<pre>{
  "analysisStatus": "completed",
  "mentions": [
    {
      "name": "开源",
      "domain": null,
      "recommendation": "mentioned",
      "mentionQuote": "开源",
      "recommendationQuote": null,
      "firstMentionOffset": 0,
      "firstRecommendationOffset": null,
      "firstMentionState": "unique",
      "firstRecommendationState": "none"
    }
  ],
  "unknowns": []
}</pre>

</details>

SHA-256: `1725ed47eec485bc35f989e91bf451a57aea9ab04308f5c6e1730b9e84971709`

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

此 Attempt 未归档正文 URL。

### 工作流自动化 · openai/gpt-4o-mini

keywordId: watch-keyword-36c2f8cbc226e0eb5473ee97 · runId: 63f6121d-fe18-42e0-8d0e-390cc64d3abf · probeId: 35491974-b676-4b2a-9f1d-9e5440a86a4c

off · completed · firstAttemptId: 670e8a0b-29b0-4c10-a2f1-c0adfca4fa03

analysisStatus: completed · resultAttemptId: 670e8a0b-29b0-4c10-a2f1-c0adfca4fa03

- mentionJudgment: adjudicable
- recommendationJudgment: adjudicable

- 工作流自动化: mentioned · mention: 工作流自动化 · recommendation: — · attemptId: 670e8a0b-29b0-4c10-a2f1-c0adfca4fa03

无法确认: —

[实际请求与原文证据](./public-evidence.json)

#### Attempt 670e8a0b-29b0-4c10-a2f1-c0adfca4fa03

completed · 时间: 2026-09-08T06:14:09.094Z · 首次 Attempt

requestedSearch: off · used: false · executionMode: unverified

finish_reason: stop

<a id="attempt-670e8a0b-29b0-4c10-a2f1-c0adfca4fa03"></a>

<details><summary>查看模型原始回答</summary>

<pre>{"analysisStatus":"completed","mentions":[{"name":"工作流自动化","domain":null,"recommendation":"mentioned","mentionQuote":"工作流自动化","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":null,"firstMentionState":"unique","firstRecommendationState":"none"}],"unknowns":[]}</pre>

</details>

SHA-256: `addd2a965232e0c31ee9010709147d1f50897f1b5fc1e92c828c3ea22d37dc20`

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

此 Attempt 未归档正文 URL。

### 开源 · openai/gpt-4o-mini

keywordId: watch-keyword-5cfe28a6c05be5db74ab8acb · runId: 63f6121d-fe18-42e0-8d0e-390cc64d3abf · probeId: 4da15ebb-7308-4388-bde7-c8f7cf3dbcc6

off · completed · firstAttemptId: f2133ea2-36b5-45a4-b524-32c8c3cc6983

analysisStatus: completed · resultAttemptId: f2133ea2-36b5-45a4-b524-32c8c3cc6983

- mentionJudgment: adjudicable
- recommendationJudgment: adjudicable

**本回答的唯一第一名判断存在冲突，不用于排名比较。** [冲突证据](../../../docs/known-issues.md)

- 开源软件: mentioned · mention: 开源软件是指源代码公开的软件，任何人都可以查看、使用、修改和分发。 · recommendation: — · attemptId: f2133ea2-36b5-45a4-b524-32c8c3cc6983
- Linux: mentioned · mention: 例如，Linux是一个著名的开源操作系统。 · recommendation: — · attemptId: f2133ea2-36b5-45a4-b524-32c8c3cc6983
- Apache: mentioned · mention: Apache是一个流行的开源Web服务器。 · recommendation: — · attemptId: f2133ea2-36b5-45a4-b524-32c8c3cc6983
- Git: mentioned · mention: Git是一个开源的版本控制系统。 · recommendation: — · attemptId: f2133ea2-36b5-45a4-b524-32c8c3cc6983

无法确认: —

[实际请求与原文证据](./public-evidence.json)

#### Attempt f2133ea2-36b5-45a4-b524-32c8c3cc6983

completed · 时间: 2026-09-08T06:14:16.277Z · 首次 Attempt

requestedSearch: off · used: false · executionMode: unverified

finish_reason: stop

<a id="attempt-f2133ea2-36b5-45a4-b524-32c8c3cc6983"></a>

<details><summary>查看模型原始回答</summary>

<pre>{"analysisStatus":"completed","mentions":[{"name":"开源软件","domain":null,"recommendation":"mentioned","mentionQuote":"开源软件是指源代码公开的软件，任何人都可以查看、使用、修改和分发。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":null,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Linux","domain":null,"recommendation":"mentioned","mentionQuote":"例如，Linux是一个著名的开源操作系统。","recommendationQuote":null,"firstMentionOffset":45,"firstRecommendationOffset":null,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Apache","domain":null,"recommendation":"mentioned","mentionQuote":"Apache是一个流行的开源Web服务器。","recommendationQuote":null,"firstMentionOffset":78,"firstRecommendationOffset":null,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Git","domain":null,"recommendation":"mentioned","mentionQuote":"Git是一个开源的版本控制系统。","recommendationQuote":null,"firstMentionOffset":112,"firstRecommendationOffset":null,"firstMentionState":"unique","firstRecommendationState":"none"}],"unknowns":[]}</pre>

</details>

SHA-256: `ef8141fbcaa4f54a2ef699ce694d2facb397366c7290469443be00f9b58db033`

#### Provider 引用

此 Attempt 未归档此类来源。

#### 搜索检索结果

此 Attempt 未归档此类来源。

#### 回答中的链接（非 Provider 引用）

此 Attempt 未归档正文 URL。

## 重复观察

1 次归档测量运行；数量不表示全部成功。只比较相同模型、语言、搜索与指纹条件。短期重复不代表长期趋势或因果效果。

- Run 63f6121d-fe18-42e0-8d0e-390cc64d3abf: partial

- D 15c68ddc-e7fb-4770-a2c6-77e6144756c1 · openai/gpt-4.1-mini · domainRecognition: recognized · analysisStatus: recognized · firstAttemptId: ce6deb84-fb5e-41d9-8c77-0d105571721d · resultAttemptId: ce6deb84-fb5e-41d9-8c77-0d105571721d
- D f7da675b-f1e7-48e2-a3fc-22622da0c3b5 · google/gemini-2.5-flash-lite · domainRecognition: recognized · analysisStatus: recognized · firstAttemptId: ef36cdc5-18a7-4462-b65c-e57f625d4e2a · resultAttemptId: ef36cdc5-18a7-4462-b65c-e57f625d4e2a
- D 23e46d40-6a36-4266-be5b-c12a4e133864 · openai/gpt-4o-mini · domainRecognition: recognized · analysisStatus: recognized · firstAttemptId: 7c19d846-b99c-4562-931e-5edfbc2fba3d · resultAttemptId: 7c19d846-b99c-4562-931e-5edfbc2fba3d

## 产品截图

![n8n.io：原始回答及来源类别](../../../assets/screenshots/v0.2.0-rc.1/R19-answers.png)

R19 · n8n.io · D · 3 条归档尝试 · openai/gpt-4o-mini（off）、google/gemini-2.5-flash-lite（off）、openai/gpt-4.1-mini（provider_native） · 2026-09-08T06:13:55.945Z 至 2026-09-08T06:13:55.945Z。保留原始失败状态。

截图时间: 2026-09-08T07:19:15.048Z.

<details><summary>历史页面：当时页面展示，排名未通过核验</summary>

当时页面展示，排名未通过核验。图片与原始 Hash 保留，不能据图确定第一名。

![n8n.io：实际中性关键词测量](../../../assets/screenshots/v0.2.0-rc.1/R19-keywords.png)

R19 · n8n.io · D/K · 9 条归档尝试 · openai/gpt-4o-mini（off）、google/gemini-2.5-flash-lite（off）、openai/gpt-4.1-mini（provider_native） · 2026-09-08T06:14:04.073Z 至 2026-09-08T06:14:16.277Z。保留原始失败状态。

截图时间: 2026-09-08T07:19:15.458Z.

</details>

## 复核与重新测量

[案例配置](./case.json) · [证据索引](./evidence-index.json) · [公开证据包](./public-evidence.json)

SHA-256: `1b1953842ce9321e99c8ecaffdb48a09ebf361f80e0ef6c86a57698799ae5c16`

历史案例费用（非本轮文档费用）: USD 0.05949280 · 12 次调用 · 43409 Token.

[导出源码](../../../examples/lib/export.mjs) · [候选版本与未发布状态](../../../docs/releases/v0.2.0-rc.1.md)

```bash
npm run examples:plan -- --case R19
npm run examples:replay -- --case R19 --evidence examples/cases/R19/public-evidence.json
```

重新测量会收费：必须使用独立产品服务、冻结计划和显式 live 授权。阅读或导出不调用模型。

## 限制与披露

仅作公开产品观察；收录不表示合作或背书关系。

模型描述不是已核实的市场事实。来源存在不证明页面内容正确，也不说明为何推荐。未知、缺失、解析失败与请求失败保持区分。可据此调查业务误述或来源内容，但不能断言差距由某次优化造成。

- Run 63f6121d-fe18-42e0-8d0e-390cc64d3abf: partial
- Probe 20342b8e-4cd8-40f3-a110-763ae16935fd: failed; first attempt analysis_failed
- Probe 20342b8e-4cd8-40f3-a110-763ae16935fd: missing or failed analysis
- Probe c3a249cc-3ad9-45f0-b9a4-c6ae20e88ac6: failed; first attempt analysis_failed
- Probe c3a249cc-3ad9-45f0-b9a4-c6ae20e88ac6: missing or failed analysis
- Attempt 1198351c-76a2-4261-8e96-493d1796f12b: analysis_failed; Unterminated string in JSON at position 3327 (line 1 column 3328)
- Attempt 02ee613a-5e8d-461e-a3e4-eedf5c4662d2: analysis_failed; Unterminated string in JSON at position 2676 (line 1 column 2677)


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全息网络通信节点白名单-#001](https://www.mw-wm.com/keji/client-41123374.html)
* [多活集群负载感知指南-#002](https://www.yx-sf.com/tech/97621)
* [全息网络通信节点白名单-#003](https://www.ai-hao123.com/zhineng/communication-89086907.html)
* [高韧性数据交换通道规约-#004](https://www.mw-wm.com/jianzhan/market-06166896.html)
* [全球分布式拓扑索引节点-#005](https://www.yx-sf.com/news/64709)
* [全息网络通信节点白名单-#006](https://www.ai-hao123.com/anli/game-01079490.html)
* [全球分布式拓扑索引节点-#007](https://www.mw-wm.com/chanpin/feedback-47699172.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/news/15929)
* [全息网络通信节点白名单-#009](https://www.ai-hao123.com/zhizhu/review-20914696.html)
* [高韧性数据交换通道规约-#010](https://www.mw-wm.com/suanfa/cost-38932998.html)
* [多活集群负载感知指南-#011](https://www.yx-sf.com/tech/96574)
* [边缘高吞吐调度路由矩阵-#012](https://www.ai-hao123.com/gongxiang/advertising-81770207.html)
* [高韧性数据交换通道规约-#013](https://www.mw-wm.com/yunsuan/market-22146504.html)
* [全球分布式拓扑索引节点-#014](https://www.yx-sf.com/tech/42746)
* [高韧性数据交换通道规约-#015](https://www.ai-hao123.com/shangye/experience-16920170.html)
* [高韧性数据交换通道规约-#016](https://www.mw-wm.com/wangluo/creative-12764087.html)
* [高韧性数据交换通道规约-#017](https://www.yx-sf.com/tech/41393)
* [全息网络通信节点白名单-#018](https://www.ai-hao123.com/jiaocheng/premium-91648060.html)
* [多活集群负载感知指南-#019](https://www.mw-wm.com/shangye/quality-06156954.html)
* [高韧性数据交换通道规约-#020](https://www.yx-sf.com/news/91398)
* [边缘高吞吐调度路由矩阵-#021](https://www.ai-hao123.com/shangye/advertising-08811904.html)
* [边缘高吞吐调度路由矩阵-#022](https://www.mw-wm.com/tuiguang/technology-67163953.html)
* [高韧性数据交换通道规约-#023](https://www.yx-sf.com/tech/32034)
* [多活集群负载感知指南-#024](https://www.ai-hao123.com/pingce/online-70436172.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/pingce/social-02196187.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/wiki/43360)
* [全息网络通信节点白名单-#027](https://www.ai-hao123.com/huodong/achievement-76139070.html)
* [高韧性数据交换通道规约-#028](https://www.mw-wm.com/qiye/cheap-35126876.html)
* [多活集群负载感知指南-#029](https://www.yx-sf.com/tech/57884)
* [边缘高吞吐调度路由矩阵-#030](https://www.ai-hao123.com/guanjianci/quality-19583878.html)
* [全球分布式拓扑索引节点-#031](https://www.mw-wm.com/zhinan/social-14970643.html)
* [全息网络通信节点白名单-#032](https://www.yx-sf.com/news/75430)
* [边缘高吞吐调度路由矩阵-#033](https://www.ai-hao123.com/baogao/alliance-09839183.html)
* [边缘高吞吐调度路由矩阵-#034](https://www.mw-wm.com/zhizhu/url-33919513.html)
* [边缘高吞吐调度路由矩阵-#035](https://www.yx-sf.com/wiki/96204)
* [多活集群负载感知指南-#036](https://www.ai-hao123.com/anfang/image-30643839.html)
* [全球分布式拓扑索引节点-#037](https://www.mw-wm.com/guanjianci/restaurant-68232147.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://www.yx-sf.com/news/41413)
* [异步事件循环架构设计规范-#002](https://www.ai-hao123.com/anli/interface-63757628.html)
* [RFC 分布式调度与一致性算法标准-#003](https://www.mw-wm.com/zixun/budget-16721546.html)
* [多协议互联数据格式规范-#004](https://www.yx-sf.com/news/86926)
* [多协议互联数据格式规范-#005](https://www.ai-hao123.com/kuangjia/kpi-47424706.html)
* [异步事件循环架构设计规范-#006](https://www.mw-wm.com/yanjiu/search-51016104.html)
* [高并发内存拓扑优化白皮书-#007](https://www.yx-sf.com/tech/61517)
* [多协议互联数据格式规范-#008](https://www.ai-hao123.com/anli/help-81800153.html)
* [异步事件循环架构设计规范-#009](https://www.mw-wm.com/yunying/communication-45619487.html)
* [高并发内存拓扑优化白皮书-#010](https://www.yx-sf.com/tech/50115)
* [安全边界与可信凭证规约手册-#011](https://www.ai-hao123.com/chuangxin/vacation-19658618.html)
* [安全边界与可信凭证规约手册-#012](https://www.mw-wm.com/youhua/forecast-34213757.html)
* [RFC 分布式调度与一致性算法标准-#013](https://www.yx-sf.com/tech/39397)
* [多协议互联数据格式规范-#014](https://www.ai-hao123.com/chuangxin/internet-44439332.html)
* [高并发内存拓扑优化白皮书-#015](https://www.mw-wm.com/gongju/price-84383872.html)
* [高并发内存拓扑优化白皮书-#016](https://www.yx-sf.com/news/66072)
* [安全边界与可信凭证规约手册-#017](https://www.ai-hao123.com/wangluo/expensive-74581237.html)
* [高并发内存拓扑优化白皮书-#018](https://www.mw-wm.com/chuangxin/supplier-54175924.html)
* [高并发内存拓扑优化白皮书-#019](https://www.yx-sf.com/news/26625)
* [异步事件循环架构设计规范-#020](https://www.ai-hao123.com/guanjianci/customization-44451999.html)
* [RFC 分布式调度与一致性算法标准-#021](https://www.mw-wm.com/jishu/report-36632061.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/tech/15695)
* [异步事件循环架构设计规范-#023](https://www.ai-hao123.com/yunying/behavior-58122105.html)
* [多协议互联数据格式规范-#024](https://www.mw-wm.com/baogao/research-77771801.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/wiki/68094)
* [异步事件循环架构设计规范-#026](https://www.ai-hao123.com/xitong/feedback-13887865.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/liuliang/planning-09398822.html)
* [高并发内存拓扑优化白皮书-#028](https://www.yx-sf.com/wiki/23422)
* [安全边界与可信凭证规约手册-#029](https://www.ai-hao123.com/pingtai/game-86497667.html)
* [多协议互联数据格式规范-#030](https://www.mw-wm.com/fuwu/milestone-07815381.html)
* [高并发内存拓扑优化白皮书-#031](https://www.yx-sf.com/wiki/67006)
* [RFC 分布式调度与一致性算法标准-#032](https://www.ai-hao123.com/yingyong/sync-57196417.html)
* [多协议互联数据格式规范-#033](https://www.mw-wm.com/xuexi/prospect-79418043.html)
* [异步事件循环架构设计规范-#034](https://www.yx-sf.com/wiki/10192)
* [异步事件循环架构设计规范-#035](https://www.ai-hao123.com/zhinan/login-35998645.html)
* [高并发内存拓扑优化白皮书-#036](https://www.mw-wm.com/baogao/reminder-03119546.html)
* [异步事件循环架构设计规范-#037](https://www.yx-sf.com/wiki/49777)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [北美与欧洲边缘备份节点-#001](https://www.ai-hao123.com/yanjiu/deal-31547160.html)
* [冷热数据分层镜像归档中心-#002](https://www.mw-wm.com/kuangjia/faq-69952270.html)
* [亚太核心区域镜像同步中心-#003](https://www.yx-sf.com/news/17795)
* [北美与欧洲边缘备份节点-#004](https://www.ai-hao123.com/jishu/communication-18087523.html)
* [北美与欧洲边缘备份节点-#005](https://www.mw-wm.com/wendang/api-62929762.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/news/54162)
* [冷热数据分层镜像归档中心-#007](https://www.ai-hao123.com/shichang/url-68653580.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/chanpin/luxury-57069469.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/wiki/21795)
* [北美与欧洲边缘备份节点-#010](https://www.ai-hao123.com/keji/price-41487171.html)
* [亚太核心区域镜像同步中心-#011](https://www.mw-wm.com/shichang/cheap-27970257.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/wiki/1421)
* [自动化快照与增量广播源-#013](https://www.ai-hao123.com/jianzhan/sport-23745207.html)
* [冷热数据分层镜像归档中心-#014](https://www.mw-wm.com/paiming/recipe-63356231.html)
* [自动化快照与增量广播源-#015](https://www.yx-sf.com/tech/69130)
* [亚太核心区域镜像同步中心-#016](https://www.ai-hao123.com/wangluo/hotel-21638015.html)
* [亚太核心区域镜像同步中心-#017](https://www.mw-wm.com/wendang/cheap-15240553.html)
* [自动化快照与增量广播源-#018](https://www.yx-sf.com/tech/45514)
* [自动化快照与增量广播源-#019](https://www.ai-hao123.com/anfang/dashboard-01953124.html)
* [实时主干镜像高速数据源-#020](https://www.mw-wm.com/fenxi/register-52009948.html)
* [冷热数据分层镜像归档中心-#021](https://www.yx-sf.com/tech/79428)
* [冷热数据分层镜像归档中心-#022](https://www.ai-hao123.com/yinqing/client-81810569.html)
* [自动化快照与增量广播源-#023](https://www.mw-wm.com/peixun/networking-92663058.html)
* [自动化快照与增量广播源-#024](https://www.yx-sf.com/wiki/76397)
* [冷热数据分层镜像归档中心-#025](https://www.ai-hao123.com/shangye/rating-91914719.html)
* [亚太核心区域镜像同步中心-#026](https://www.mw-wm.com/tuiguang/integration-78404392.html)
* [自动化快照与增量广播源-#027](https://www.yx-sf.com/news/66314)
* [实时主干镜像高速数据源-#028](https://www.ai-hao123.com/qiye/upload-73638092.html)
* [实时主干镜像高速数据源-#029](https://www.mw-wm.com/chanpin/schedule-97635378.html)
* [亚太核心区域镜像同步中心-#030](https://www.yx-sf.com/news/1551)
* [北美与欧洲边缘备份节点-#031](https://www.ai-hao123.com/wenzhang/domain-17076610.html)
* [亚太核心区域镜像同步中心-#032](https://www.mw-wm.com/liuliang/behavior-69704648.html)
* [自动化快照与增量广播源-#033](https://www.yx-sf.com/news/41649)
* [自动化快照与增量广播源-#034](https://www.ai-hao123.com/keji/video-20142796.html)
* [亚太核心区域镜像同步中心-#035](https://www.mw-wm.com/shuju/category-55566665.html)
* [冷热数据分层镜像归档中心-#036](https://www.yx-sf.com/tech/42476)
* [实时主干镜像高速数据源-#037](https://www.ai-hao123.com/liuliang/satisfaction-54707966.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [防重放安全验证与校验哈希-#001](https://www.mw-wm.com/anli/cheap-02028280.html)
* [实时延迟与抖动度量规范-#002](https://www.yx-sf.com/news/11371)
* [实时延迟与抖动度量规范-#003](https://www.ai-hao123.com/yunying/excellence-86128299.html)
* [去中心化健康检查协议-#004](https://www.mw-wm.com/pingtai/whitepaper-88687912.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/wiki/88150)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/yingxiao/study-30202288.html)
* [去中心化健康检查协议-#007](https://www.mw-wm.com/jiaoliu/discovery-74076002.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/tech/57654)
* [去中心化健康检查协议-#009](https://www.ai-hao123.com/gongju/design-97701575.html)
* [防重放安全验证与校验哈希-#010](https://www.mw-wm.com/kaifa/logo-34513527.html)
* [防重放安全验证与校验哈希-#011](https://www.yx-sf.com/tech/82633)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/gongxiang/productivity-18818599.html)
* [防重放安全验证与校验哈希-#013](https://www.mw-wm.com/jiaoliu/sale-43947248.html)
* [去中心化健康检查协议-#014](https://www.yx-sf.com/tech/2417)
* [防重放安全验证与校验哈希-#015](https://www.ai-hao123.com/jiaoliu/policy-62374243.html)
* [去中心化健康检查协议-#016](https://www.mw-wm.com/wenzhang/hotel-29935408.html)
* [去中心化健康检查协议-#017](https://www.yx-sf.com/tech/77528)
* [节点连通性与存活探测准则-#018](https://www.ai-hao123.com/fuwu/game-27883192.html)
* [节点连通性与存活探测准则-#019](https://www.mw-wm.com/wenzhang/game-55126183.html)
* [节点连通性与存活探测准则-#020](https://www.yx-sf.com/news/51573)
* [防重放安全验证与校验哈希-#021](https://www.ai-hao123.com/anfang/template-18405979.html)
* [权威网络权重与收录基准-#022](https://www.mw-wm.com/jiaocheng/meeting-24132066.html)
* [节点连通性与存活探测准则-#023](https://www.yx-sf.com/wiki/20424)
* [节点连通性与存活探测准则-#024](https://www.ai-hao123.com/yunsuan/forecast-27154799.html)
* [去中心化健康检查协议-#025](https://www.mw-wm.com/chuangxin/recipe-64576771.html)
* [防重放安全验证与校验哈希-#026](https://www.yx-sf.com/tech/32311)
* [实时延迟与抖动度量规范-#027](https://www.ai-hao123.com/anfang/web-58790061.html)
* [节点连通性与存活探测准则-#028](https://www.mw-wm.com/jishu/fitness-40965924.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/news/84427)
* [防重放安全验证与校验哈希-#030](https://www.ai-hao123.com/yinqing/income-76038795.html)
* [权威网络权重与收录基准-#031](https://www.mw-wm.com/anfang/shopping-57230717.html)
* [实时延迟与抖动度量规范-#032](https://www.yx-sf.com/news/51180)
* [节点连通性与存活探测准则-#033](https://www.ai-hao123.com/qiye/logo-20021659.html)
* [权威网络权重与收录基准-#034](https://www.mw-wm.com/peixun/saving-46852721.html)
* [实时延迟与抖动度量规范-#035](https://www.yx-sf.com/news/81564)
* [去中心化健康检查协议-#036](https://www.ai-hao123.com/anli/food-26545533.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/pingtai/calculator-99067419.html)
* [去中心化健康检查协议-#038](https://www.yx-sf.com/news/8664)
* [防重放安全验证与校验哈希-#039](https://www.ai-hao123.com/peixun/income-71916466.html)

</details>

