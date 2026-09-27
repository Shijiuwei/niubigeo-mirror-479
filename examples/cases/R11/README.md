# R11 · github.com

[简体中文](./README.zh-CN.md) · [All cases](../../README.md)

## Observed result

Domain answers described code hosting; the collaboration answer has a conflicting first-place field.

Initial D: 3/3 analyzable current answers. Measurement D: 3/3 analyzable first answers. K: 3/3 analyzable first answers. These are answer-coverage counts, not recognition rates or product metric denominators.

Execution status: **completed**.

**These metrics have consistency conflicts and are excluded from ranking comparisons.** Original values remain unchanged; no winner or tie is inferred.

- [firstMentionState · 3d3f3f2c-c458-4b4c-85d1-048ecd2bafdb](../../../docs/known-issues.md#conflict-3d3f3f2c-c458-4b4c-85d1-048ecd2bafdb-firstmentionstate)

![github.com: individual domain recognition results](../../../assets/screenshots/v0.2.0-rc.1/R11-models.png)

R11 · github.com · D · 3 archived attempts · openai/gpt-4o-mini (off), google/gemini-2.5-flash-lite (off), openai/gpt-4.1-mini (provider_native) · 2026-09-08T06:10:01.788Z to 2026-09-08T06:10:01.788Z. Original failures remain visible. Captured: 2026-09-08T07:19:06.381Z.

## Conditions

Input domain: github.com. Answer language: zh.

Protocols: D = domain-recognition/v1; K = keyword-discovery/v1.

D receives the domain, language, fixed protocol and model settings. K receives a frozen neutral keyword. Browsing categories are not sent to models.

- openai/gpt-4o-mini · off
- google/gemini-2.5-flash-lite · off
- openai/gpt-4.1-mini · provider_native

## Model observations

### Google: Gemini 2.5 Flash Lite

**Observed at:** 2026-09-08T06:10:01.788Z

domainRecognition: recognized · analysisStatus: recognized · localAnalysis: complete.

Attempt: 6e78161a-74b2-4f24-9181-f3a948627d97 · completed · executionMode: unverified.

Brand: GitHub

Business: 一个基于云的代码托管服务平台，提供版本控制、代码审查、项目管理和协作工具。

Original span: UTF-16 [188, 225) · [Full answer](#attempt-6e78161a-74b2-4f24-9181-f3a948627d97)

Category: 软件开发工具

Brand keywords: 代码托管, 版本控制, 软件开发, 开源社区, 协作

Competitors named by this model:

- GitLab · gitlab.com: 一个提供软件开发生命周期中所有功能的集成平台，包括项目规划、代码管理、CI/CD、监控和安全。. Keywords: 代码托管, 版本控制, CI/CD
- Bitbucket · bitbucket.org: 一个由 Atlassian 提供的基于 Git 的代码托管服务，支持私有和公共仓库，并与 Jira 等其他 Atlassian 产品集成。. Keywords: 代码托管, 版本控制, 项目管理

Uncertain: —


<a id="attempt-6e78161a-74b2-4f24-9181-f3a948627d97"></a>

<details><summary>Read the original answer</summary>

<pre>{
  "domainRecognition": "recognized",
  "analysisStatus": "recognized",
  "recognizedBrand": {
    "value": "GitHub",
    "citationUrls": []
  },
  "businessDescription": {
    "value": "一个基于云的代码托管服务平台，提供版本控制、代码审查、项目管理和协作工具。",
    "citationUrls": []
  },
  "productCategory": {
    "value": "软件开发工具",
    "citationUrls": []
  },
  "competitors": [
    {
      "name": "GitLab",
      "domain": "gitlab.com",
      "businessDescription": "一个提供软件开发生命周期中所有功能的集成平台，包括项目规划、代码管理、CI/CD、监控和安全。",
      "productCategory": "软件开发工具",
      "keywords": [
        {
          "keyword": "代码托管",
          "citationUrls": []
        },
        {
          "keyword": "版本控制",
          "citationUrls": []
        },
        {
          "keyword": "CI/CD",
          "citationUrls": []
        }
      ],
      "citationUrls": []
    },
    {
      "name": "Bitbucket",
      "domain": "bitbucket.org",
      "businessDescription": "一个由 Atlassian 提供的基于 Git 的代码托管服务，支持私有和公共仓库，并与 Jira 等其他 Atlassian 产品集成。",
      "productCategory": "软件开发工具",
      "keywords": [
        {
          "keyword": "代码托管",
          "citationUrls": []
        },
        {
          "keyword": "版本控制",
          "citationUrls": []
        },
        {
          "keyword": "项目管理",
          "citationUrls": []
        }
      ],
      "citationUrls": []
    }
  ],
  "brandKeywords": [
    {
      "keyword": "代码托管",
      "citationUrls": []
    },
    {
      "keyword": "版本控制",
      "citationUrls": []
    },
    {
      "keyword": "软件开发",
      "citationUrls": []
    },
    {
      "keyword": "开源社区",
      "citationUrls": []
    },
    {
      "keyword": "协作",
      "citationUrls": []
    }
  ],
  "unknowns": []
}</pre>

</details>

SHA-256: `1c52d159f46ec56a1561e467bfd226f60a76b72333afab1670b3a50005e62677`

[Answer, field offsets and attempts](./public-evidence.json) · SHA-256: `1c52d159f46ec56a1561e467bfd226f60a76b72333afab1670b3a50005e62677`

<details><summary>Keyword provenance and original spans</summary>

| Owner | Keyword | Original text / UTF-16 span |
|---|---|---|
| GitHub | 代码托管 | 代码托管 [194, 198) |
| GitHub | 版本控制 | 版本控制 [205, 209) |
| GitHub | 软件开发 | 软件开发 [293, 297) |
| GitHub | 开源社区 | 开源社区 [1560, 1564) |
| GitHub | 协作 | 协作 [220, 222) |
| GitLab | 代码托管 | 代码托管 [194, 198) |
| GitLab | 版本控制 | 版本控制 [205, 209) |
| GitLab | CI/CD | CI/CD [474, 479) |
| Bitbucket | 代码托管 | 代码托管 [194, 198) |
| Bitbucket | 版本控制 | 版本控制 [205, 209) |
| Bitbucket | 项目管理 | 项目管理 [215, 219) |

</details>

#### Provider citations

No sources of this type were archived for this attempt.

#### Search retrieval results

No sources of this type were archived for this attempt.

#### Links in the answer (not Provider citations)

No answer URLs were archived for this attempt.

### OpenAI: GPT-4o-mini

**Observed at:** 2026-09-08T06:10:01.788Z

domainRecognition: recognized · analysisStatus: recognized · localAnalysis: complete.

Attempt: 4d7070e8-c3db-409c-a891-050834389a04 · completed · executionMode: unverified.

Brand: GitHub

Business: 一个用于版本控制和协作的软件开发平台

Original span: UTF-16 [151, 169) · [Full answer](#attempt-4d7070e8-c3db-409c-a891-050834389a04)

Category: 代码托管和版本控制

Brand keywords: 开源, 协作, 开发者

Competitors named by this model:

- GitLab · gitlab.com: 一个提供代码托管和CI/CD的开发平台. Keywords: 代码托管, CI/CD
- Bitbucket · bitbucket.org: 一个用于代码托管和版本控制的服务. Keywords: 代码托管, 版本控制

Uncertain: —


<a id="attempt-4d7070e8-c3db-409c-a891-050834389a04"></a>

<details><summary>Read the original answer</summary>

<pre>{"domainRecognition":"recognized","analysisStatus":"recognized","recognizedBrand":{"value":"GitHub","citationUrls":[]},"businessDescription":{"value":"一个用于版本控制和协作的软件开发平台","citationUrls":[]},"productCategory":{"value":"代码托管和版本控制","citationUrls":[]},"competitors":[{"name":"GitLab","domain":"gitlab.com","businessDescription":"一个提供代码托管和CI/CD的开发平台","productCategory":"代码托管和版本控制","keywords":[{"keyword":"代码托管","citationUrls":[]},{"keyword":"CI/CD","citationUrls":[]}],"citationUrls":[]},{"name":"Bitbucket","domain":"bitbucket.org","businessDescription":"一个用于代码托管和版本控制的服务","productCategory":"代码托管和版本控制","keywords":[{"keyword":"代码托管","citationUrls":[]},{"keyword":"版本控制","citationUrls":[]}],"citationUrls":[]}],"brandKeywords":[{"keyword":"开源","citationUrls":[]},{"keyword":"协作","citationUrls":[]},{"keyword":"开发者","citationUrls":[]}],"unknowns":[]}</pre>

</details>

SHA-256: `f8c475cef3c0cde920721a23d317af6925790303c574df74956699a391a9719d`

[Answer, field offsets and attempts](./public-evidence.json) · SHA-256: `f8c475cef3c0cde920721a23d317af6925790303c574df74956699a391a9719d`

<details><summary>Keyword provenance and original spans</summary>

| Owner | Keyword | Original text / UTF-16 span |
|---|---|---|
| GitHub | 开源 | 开源 [735, 737) |
| GitHub | 协作 | 协作 [160, 162) |
| GitHub | 开发者 | 开发者 [805, 808) |
| GitLab | 代码托管 | 代码托管 [218, 222) |
| GitLab | CI/CD | CI/CD [334, 339) |
| Bitbucket | 代码托管 | 代码托管 [218, 222) |
| Bitbucket | 版本控制 | 版本控制 [155, 159) |

</details>

#### Provider citations

No sources of this type were archived for this attempt.

#### Search retrieval results

No sources of this type were archived for this attempt.

#### Links in the answer (not Provider citations)

No answer URLs were archived for this attempt.

### OpenAI: GPT-4.1 Mini

**Observed at:** 2026-09-08T06:10:01.788Z

domainRecognition: recognized · analysisStatus: recognized · localAnalysis: complete.

Attempt: b19ef1a0-d73b-4ae6-a730-d9b6ffd58cd0 · completed · executionMode: native.

Brand: GitHub

Business: GitHub是一个在线软件源代码托管服务平台，提供版本控制和协作功能，供开发者创建、存储、管理和分享代码。

Original span: UTF-16 [151, 204) · [Full answer](#attempt-b19ef1a0-d73b-4ae6-a730-d9b6ffd58cd0)

Category: 在线软件源代码托管服务平台

Brand keywords: GitHub

Competitors named by this model:

- GitLab · gitlab.com: GitLab是一个基于Web的Git仓库管理工具，提供源代码管理、CI/CD和DevOps功能。. Keywords: GitLab

Uncertain: —


<a id="attempt-b19ef1a0-d73b-4ae6-a730-d9b6ffd58cd0"></a>

<details><summary>Read the original answer</summary>

<pre>{"domainRecognition":"recognized","analysisStatus":"recognized","recognizedBrand":{"value":"GitHub","citationUrls":[]},"businessDescription":{"value":"GitHub是一个在线软件源代码托管服务平台，提供版本控制和协作功能，供开发者创建、存储、管理和分享代码。","citationUrls":[]},"productCategory":{"value":"在线软件源代码托管服务平台","citationUrls":[]},"competitors":[{"name":"GitLab","domain":"gitlab.com","businessDescription":"GitLab是一个基于Web的Git仓库管理工具，提供源代码管理、CI/CD和DevOps功能。","productCategory":"在线软件源代码托管服务平台","keywords":[{"keyword":"GitLab","citationUrls":[]}],"citationUrls":[]}],"brandKeywords":[{"keyword":"GitHub","citationUrls":[]}],"unknowns":[]}</pre>

</details>

SHA-256: `a3bc3c48cce79dec017a4c8436c0b79b5e2c2ad76e80ec456fbeb156f4168ae4`

[Answer, field offsets and attempts](./public-evidence.json) · SHA-256: `a3bc3c48cce79dec017a4c8436c0b79b5e2c2ad76e80ec456fbeb156f4168ae4`

<details><summary>Keyword provenance and original spans</summary>

| Owner | Keyword | Original text / UTF-16 span |
|---|---|---|
| GitHub | GitHub | GitHub [92, 98) |
| GitLab | GitLab | GitLab [311, 317) |

</details>

#### Provider citations

No sources of this type were archived for this attempt.

#### Search retrieval results

No sources of this type were archived for this attempt.

#### Links in the answer (not Provider citations)

No answer URLs were archived for this attempt.

## Neutral keyword tests

协作

K valid counts analyzable first-attempt answers only, not product metric denominators. Inspect archived metric samples, included flags and judgments. A later successful retry does not replace this coverage count.

Selection records, exact quotes and exclusions are in the evidence file. Each answer observes the target and other entities under the same conditions; offline and online differences are not model rankings.

### 协作 · google/gemini-2.5-flash-lite

keywordId: watch-keyword-cc73f0095680242c2e350fa0 · runId: 86ca2562-66e4-41c6-aa14-7d9f8fa82838 · probeId: 868de90c-0e10-493d-b14f-58e00332ef8c

off · completed · firstAttemptId: 8c1f8b78-1921-458f-a724-bba1f027243a

analysisStatus: completed · resultAttemptId: 8c1f8b78-1921-458f-a724-bba1f027243a

- mentionJudgment: adjudicable
- recommendationJudgment: adjudicable

- 协作: mentioned · mention: 协作 · recommendation: — · attemptId: 8c1f8b78-1921-458f-a724-bba1f027243a

Uncertain: —

[Actual request and answer evidence](./public-evidence.json)

#### Attempt 8c1f8b78-1921-458f-a724-bba1f027243a

completed · Observed at: 2026-09-08T06:10:18.897Z · First attempt

requestedSearch: off · used: false · executionMode: unverified

finish_reason: stop

<a id="attempt-8c1f8b78-1921-458f-a724-bba1f027243a"></a>

<details><summary>Read the original answer</summary>

<pre>{
  "analysisStatus": "completed",
  "mentions": [
    {
      "name": "协作",
      "domain": null,
      "recommendation": "mentioned",
      "mentionQuote": "协作",
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

SHA-256: `620f0193b6aac7d5825e025528779c953ab7cb48f37268a6a868921521da28b1`

#### Provider citations

No sources of this type were archived for this attempt.

#### Search retrieval results

No sources of this type were archived for this attempt.

#### Links in the answer (not Provider citations)

No answer URLs were archived for this attempt.

### 协作 · openai/gpt-4.1-mini

keywordId: watch-keyword-cc73f0095680242c2e350fa0 · runId: 86ca2562-66e4-41c6-aa14-7d9f8fa82838 · probeId: 3d3f3f2c-c458-4b4c-85d1-048ecd2bafdb

provider_native · completed · firstAttemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb

analysisStatus: completed · resultAttemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb

- mentionJudgment: adjudicable
- recommendationJudgment: adjudicable

**This answer has conflicting unique-first judgments; do not use it for rankings.** [Evidence](../../../docs/known-issues.md)

- 彩漩PPT: mentioned · mention: 彩漩PPT ｜一站式 PPT 协作分享平台 · recommendation: 彩漩PPT ｜一站式 PPT 协作分享平台 · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- WPS协作: mentioned · mention: WPS协作 · recommendation: WPS协作 · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- Atlassian: mentioned · mention: Atlassian Cloud 平台 · recommendation: Atlassian Cloud 平台 · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- Boardmix博思白板: mentioned · mention: Boardmix博思白板 · recommendation: Boardmix博思白板 · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- Zoom Workplace: mentioned · mention: Zoom Workplace · recommendation: Zoom Workplace · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- CoDesign设计协作平台: mentioned · mention: CoDesign设计协作平台 · recommendation: CoDesign设计协作平台 · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- WorkCraft: mentioned · mention: WorkCraft · recommendation: WorkCraft · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- AceTeamwork: mentioned · mention: AceTeamwork · recommendation: AceTeamwork · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- FlowUs息流: mentioned · mention: FlowUs息流 · recommendation: FlowUs息流 · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb
- BeeWorks: mentioned · mention: BeeWorks 企业数字协同平台 · recommendation: BeeWorks 企业数字协同平台 · attemptId: 8ed46717-df44-46cb-a4a8-c0fd326720fb

Uncertain: —

[Actual request and answer evidence](./public-evidence.json)

#### Attempt 8ed46717-df44-46cb-a4a8-c0fd326720fb

completed · Observed at: 2026-09-08T06:10:15.667Z · First attempt

requestedSearch: provider_native · used: true · executionMode: native

OpenRouter metadata confirmed provider-native web search.

finish_reason: stop

<a id="attempt-8ed46717-df44-46cb-a4a8-c0fd326720fb"></a>

<details><summary>Read the original answer</summary>

<pre>{"analysisStatus":"completed","mentions":[{"name":"彩漩PPT","domain":"caixuan.cc","recommendation":"mentioned","mentionQuote":"彩漩PPT ｜一站式 PPT 协作分享平台","recommendationQuote":"彩漩PPT ｜一站式 PPT 协作分享平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"WPS协作","domain":"kimxz.com","recommendation":"mentioned","mentionQuote":"WPS协作","recommendationQuote":"WPS协作","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Atlassian","domain":"atlassian.com","recommendation":"mentioned","mentionQuote":"Atlassian Cloud 平台","recommendationQuote":"Atlassian Cloud 平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Boardmix博思白板","domain":"boardmix.cn","recommendation":"mentioned","mentionQuote":"Boardmix博思白板","recommendationQuote":"Boardmix博思白板","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"Zoom Workplace","domain":"zoom.com","recommendation":"mentioned","mentionQuote":"Zoom Workplace","recommendationQuote":"Zoom Workplace","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"CoDesign设计协作平台","domain":"cloud.tencent.com","recommendation":"mentioned","mentionQuote":"CoDesign设计协作平台","recommendationQuote":"CoDesign设计协作平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"WorkCraft","domain":"work-craft.com","recommendation":"mentioned","mentionQuote":"WorkCraft","recommendationQuote":"WorkCraft","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"AceTeamwork","domain":"aceteamwork.com","recommendation":"mentioned","mentionQuote":"AceTeamwork","recommendationQuote":"AceTeamwork","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"FlowUs息流","domain":"flowus.cn","recommendation":"mentioned","mentionQuote":"FlowUs息流","recommendationQuote":"FlowUs息流","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"},{"name":"BeeWorks","domain":"beeworks.cn","recommendation":"mentioned","mentionQuote":"BeeWorks 企业数字协同平台","recommendationQuote":"BeeWorks 企业数字协同平台","firstMentionOffset":0,"firstRecommendationOffset":0,"firstMentionState":"unique","firstRecommendationState":"none"}],"unknowns":[]}</pre>

</details>

SHA-256: `1e6976a2f9638897e1d470a21f1bf8ae353a1a289afecd78f68ab43b41cb9dc3`

#### Provider citations

No sources of this type were archived for this attempt.

#### Search retrieval results

No sources of this type were archived for this attempt.

#### Links in the answer (not Provider citations)

No answer URLs were archived for this attempt.

### 协作 · openai/gpt-4o-mini

keywordId: watch-keyword-cc73f0095680242c2e350fa0 · runId: 86ca2562-66e4-41c6-aa14-7d9f8fa82838 · probeId: 87dacc6c-d928-4662-a1e3-60a6f32cd5f9

off · completed · firstAttemptId: 226cdb7d-678b-4e73-bdb2-d4568823c68e

analysisStatus: completed · resultAttemptId: 226cdb7d-678b-4e73-bdb2-d4568823c68e

- mentionJudgment: adjudicable
- recommendationJudgment: adjudicable

- 协作工具: mentioned · mention: 在现代工作环境中，协作工具变得越来越重要。 · recommendation: — · attemptId: 226cdb7d-678b-4e73-bdb2-d4568823c68e

Uncertain: —

[Actual request and answer evidence](./public-evidence.json)

#### Attempt 226cdb7d-678b-4e73-bdb2-d4568823c68e

completed · Observed at: 2026-09-08T06:10:13.200Z · First attempt

requestedSearch: off · used: false · executionMode: unverified

finish_reason: stop

<a id="attempt-226cdb7d-678b-4e73-bdb2-d4568823c68e"></a>

<details><summary>Read the original answer</summary>

<pre>{"analysisStatus":"completed","mentions":[{"name":"协作工具","domain":null,"recommendation":"mentioned","mentionQuote":"在现代工作环境中，协作工具变得越来越重要。","recommendationQuote":null,"firstMentionOffset":0,"firstRecommendationOffset":null,"firstMentionState":"unique","firstRecommendationState":"none"}],"unknowns":[]}</pre>

</details>

SHA-256: `d1ba83fd564a7485ce4dd258743b4020840d8ac27673dd1e1188e6fbabd49338`

#### Provider citations

No sources of this type were archived for this attempt.

#### Search retrieval results

No sources of this type were archived for this attempt.

#### Links in the answer (not Provider citations)

No answer URLs were archived for this attempt.

## Repeated observations

1 archived measurement runs; this count does not imply all succeeded. Compare only identical model, language, search and fingerprint conditions. Short repeats do not establish a long-term trend or a causal effect.

- Run 86ca2562-66e4-41c6-aa14-7d9f8fa82838: completed

- D 271e557a-7d27-466b-a12a-18699e70b06d · google/gemini-2.5-flash-lite · domainRecognition: recognized · analysisStatus: recognized · firstAttemptId: c6aa5ab5-6b77-4ef4-a5fb-d5920d961ea0 · resultAttemptId: c6aa5ab5-6b77-4ef4-a5fb-d5920d961ea0
- D 5a1b1934-3c21-4db2-a8e7-eef7fd66c4a4 · openai/gpt-4.1-mini · domainRecognition: recognized · analysisStatus: recognized · firstAttemptId: 50b57c86-fad4-4a7f-9268-6130b04364e5 · resultAttemptId: 50b57c86-fad4-4a7f-9268-6130b04364e5
- D 65dc78bd-144f-4d31-a8d4-d0c425f34d37 · openai/gpt-4o-mini · domainRecognition: recognized · analysisStatus: recognized · firstAttemptId: 1582e7d6-9e31-4b00-9c67-c7bf1ef55bba · resultAttemptId: 1582e7d6-9e31-4b00-9c67-c7bf1ef55bba

## Product screenshots

![github.com: original answers and source categories](../../../assets/screenshots/v0.2.0-rc.1/R11-answers.png)

R11 · github.com · D · 3 archived attempts · openai/gpt-4o-mini (off), google/gemini-2.5-flash-lite (off), openai/gpt-4.1-mini (provider_native) · 2026-09-08T06:10:01.788Z to 2026-09-08T06:10:01.788Z. Original failures remain visible.

Captured: 2026-09-08T07:19:06.688Z.

<details><summary>Historical display: rankings were not validated</summary>

Rankings shown at capture time were not validated. The original image and hash are retained; the image cannot establish a winner.

![github.com: actual neutral keyword measurements](../../../assets/screenshots/v0.2.0-rc.1/R11-keywords.png)

R11 · github.com · D/K · 6 archived attempts · openai/gpt-4o-mini (off), google/gemini-2.5-flash-lite (off), openai/gpt-4.1-mini (provider_native) · 2026-09-08T06:10:09.864Z to 2026-09-08T06:10:13.200Z. Original failures remain visible.

Captured: 2026-09-08T07:19:07.009Z.

</details>

## Inspect or remeasure

[Case configuration](./case.json) · [Evidence index](./evidence-index.json) · [Public evidence bundle](./public-evidence.json)

SHA-256: `7e50c79f64eb01b7c980d21385c55b761c10ee295bcdda7d93ace59b0db95f99`

Historical case cost (not this documentation update): USD 0.04360795 · 9 calls · 32270 Token.

[Export source](../../../examples/lib/export.mjs) · [Candidate provenance and unpublished status](../../../docs/releases/v0.2.0-rc.1.md)

```bash
npm run examples:plan -- --case R11
npm run examples:replay -- --case R11 --evidence examples/cases/R11/public-evidence.json
```

Remeasurement incurs costs and requires an isolated product service, a frozen plan and explicit live authorization. Reading and exporting do not call models.

## Limits and disclosure

This is a public-product observation. Inclusion does not imply a partnership or endorsement.

Model descriptions are not verified market facts. A returned source does not establish that its content is correct or caused a recommendation. Unknown, missing, analysis failure and request failure remain separate. Use the evidence to investigate descriptions or sources, not to assert optimization caused a difference.



---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [边缘高吞吐调度路由矩阵-#001](https://www.mw-wm.com/zhinan/report-49385461.html)
* [高韧性数据交换通道规约-#002](https://www.yx-sf.com/news/30309)
* [全息网络通信节点白名单-#003](https://www.ai-hao123.com/xitong/products-01880127.html)
* [边缘高吞吐调度路由矩阵-#004](https://www.mw-wm.com/yanjiu/register-98407278.html)
* [边缘高吞吐调度路由矩阵-#005](https://www.yx-sf.com/tech/60132)
* [多活集群负载感知指南-#006](https://www.ai-hao123.com/shichang/premium-87751803.html)
* [边缘高吞吐调度路由矩阵-#007](https://www.mw-wm.com/anfang/forum-97946744.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/news/28527)
* [高韧性数据交换通道规约-#009](https://www.ai-hao123.com/gongxiang/register-93459371.html)
* [全球分布式拓扑索引节点-#010](https://www.mw-wm.com/yingxiao/account-20787411.html)
* [全息网络通信节点白名单-#011](https://www.yx-sf.com/tech/3841)
* [多活集群负载感知指南-#012](https://www.ai-hao123.com/yunsuan/recipe-04178497.html)
* [边缘高吞吐调度路由矩阵-#013](https://www.mw-wm.com/zhineng/collaborate-40547503.html)
* [全息网络通信节点白名单-#014](https://www.yx-sf.com/tech/20217)
* [全球分布式拓扑索引节点-#015](https://www.ai-hao123.com/gongju/topic-39445263.html)
* [高韧性数据交换通道规约-#016](https://www.mw-wm.com/qiye/deadline-80428944.html)
* [高韧性数据交换通道规约-#017](https://www.yx-sf.com/news/18125)
* [全息网络通信节点白名单-#018](https://www.ai-hao123.com/keji/development-23117407.html)
* [全息网络通信节点白名单-#019](https://www.mw-wm.com/youhua/study-84211601.html)
* [全息网络通信节点白名单-#020](https://www.yx-sf.com/news/16521)
* [边缘高吞吐调度路由矩阵-#021](https://www.ai-hao123.com/hezuo/recipe-96965004.html)
* [边缘高吞吐调度路由矩阵-#022](https://www.mw-wm.com/zhizhu/profile-16837780.html)
* [多活集群负载感知指南-#023](https://www.yx-sf.com/news/15252)
* [全息网络通信节点白名单-#024](https://www.ai-hao123.com/ziyuan/form-87359111.html)
* [全球分布式拓扑索引节点-#025](https://www.mw-wm.com/gongju/update-43532551.html)
* [全息网络通信节点白名单-#026](https://www.yx-sf.com/tech/24141)
* [全息网络通信节点白名单-#027](https://www.ai-hao123.com/chanpin/finance-89668744.html)
* [多活集群负载感知指南-#028](https://www.mw-wm.com/sheji/notification-00757553.html)
* [全球分布式拓扑索引节点-#029](https://www.yx-sf.com/wiki/45439)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/keji/target-72994518.html)
* [全息网络通信节点白名单-#031](https://www.mw-wm.com/liuliang/lesson-44036109.html)
* [全球分布式拓扑索引节点-#032](https://www.yx-sf.com/wiki/66737)
* [高韧性数据交换通道规约-#033](https://www.ai-hao123.com/shuju/local-84278548.html)
* [多活集群负载感知指南-#034](https://www.mw-wm.com/jiaoliu/value-71724017.html)
* [全球分布式拓扑索引节点-#035](https://www.yx-sf.com/tech/54928)
* [多活集群负载感知指南-#036](https://www.ai-hao123.com/jiaocheng/loyalty-17144050.html)
* [高韧性数据交换通道规约-#037](https://www.mw-wm.com/youhua/coupon-29644702.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [安全边界与可信凭证规约手册-#001](https://www.yx-sf.com/wiki/45127)
* [异步事件循环架构设计规范-#002](https://www.ai-hao123.com/yingxiao/automation-13115510.html)
* [安全边界与可信凭证规约手册-#003](https://www.mw-wm.com/pingtai/tutorial-21974107.html)
* [多协议互联数据格式规范-#004](https://www.yx-sf.com/tech/24441)
* [异步事件循环架构设计规范-#005](https://www.ai-hao123.com/youhua/dashboard-53013105.html)
* [RFC 分布式调度与一致性算法标准-#006](https://www.mw-wm.com/yunying/file-10489159.html)
* [安全边界与可信凭证规约手册-#007](https://www.yx-sf.com/wiki/95651)
* [RFC 分布式调度与一致性算法标准-#008](https://www.ai-hao123.com/jiaoliu/extension-20880321.html)
* [RFC 分布式调度与一致性算法标准-#009](https://www.mw-wm.com/yinqing/accessibility-22736248.html)
* [安全边界与可信凭证规约手册-#010](https://www.yx-sf.com/news/99038)
* [高并发内存拓扑优化白皮书-#011](https://www.ai-hao123.com/jiaoliu/case-41782956.html)
* [异步事件循环架构设计规范-#012](https://www.mw-wm.com/chanpin/admin-81654529.html)
* [异步事件循环架构设计规范-#013](https://www.yx-sf.com/tech/90186)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/yingxiao/site-46002859.html)
* [多协议互联数据格式规范-#015](https://www.mw-wm.com/gongsi/website-64943406.html)
* [安全边界与可信凭证规约手册-#016](https://www.yx-sf.com/tech/80507)
* [安全边界与可信凭证规约手册-#017](https://www.ai-hao123.com/liuliang/campaign-80328386.html)
* [异步事件循环架构设计规范-#018](https://www.mw-wm.com/fuwu/share-27394295.html)
* [多协议互联数据格式规范-#019](https://www.yx-sf.com/wiki/89471)
* [RFC 分布式调度与一致性算法标准-#020](https://www.ai-hao123.com/huodong/course-50166005.html)
* [异步事件循环架构设计规范-#021](https://www.mw-wm.com/huodong/education-30673664.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/tech/26920)
* [安全边界与可信凭证规约手册-#023](https://www.ai-hao123.com/kaifa/products-99841871.html)
* [高并发内存拓扑优化白皮书-#024](https://www.mw-wm.com/zhizhu/template-48158427.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/news/50577)
* [安全边界与可信凭证规约手册-#026](https://www.ai-hao123.com/peixun/section-64712897.html)
* [多协议互联数据格式规范-#027](https://www.mw-wm.com/xinwen/backup-93986268.html)
* [安全边界与可信凭证规约手册-#028](https://www.yx-sf.com/tech/71480)
* [多协议互联数据格式规范-#029](https://www.ai-hao123.com/jishu/interface-94716310.html)
* [高并发内存拓扑优化白皮书-#030](https://www.mw-wm.com/shichang/behavior-52566145.html)
* [异步事件循环架构设计规范-#031](https://www.yx-sf.com/tech/70768)
* [RFC 分布式调度与一致性算法标准-#032](https://www.ai-hao123.com/wenzhang/optimization-39120741.html)
* [高并发内存拓扑优化白皮书-#033](https://www.mw-wm.com/baogao/engagement-60599792.html)
* [高并发内存拓扑优化白皮书-#034](https://www.yx-sf.com/news/73003)
* [安全边界与可信凭证规约手册-#035](https://www.ai-hao123.com/jiaoliu/demographic-08679276.html)
* [多协议互联数据格式规范-#036](https://www.mw-wm.com/peixun/music-85287736.html)
* [RFC 分布式调度与一致性算法标准-#037](https://www.yx-sf.com/news/84561)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [实时主干镜像高速数据源-#001](https://www.ai-hao123.com/jishu/review-67683745.html)
* [冷热数据分层镜像归档中心-#002](https://www.mw-wm.com/jiaocheng/faq-48529976.html)
* [实时主干镜像高速数据源-#003](https://www.yx-sf.com/tech/25219)
* [实时主干镜像高速数据源-#004](https://www.ai-hao123.com/guanjianci/services-64394214.html)
* [冷热数据分层镜像归档中心-#005](https://www.mw-wm.com/hezuo/account-16306587.html)
* [实时主干镜像高速数据源-#006](https://www.yx-sf.com/wiki/10196)
* [实时主干镜像高速数据源-#007](https://www.ai-hao123.com/fuwu/study-28341021.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/huodong/creative-63664582.html)
* [自动化快照与增量广播源-#009](https://www.yx-sf.com/tech/24650)
* [亚太核心区域镜像同步中心-#010](https://www.ai-hao123.com/gongju/sport-09610204.html)
* [自动化快照与增量广播源-#011](https://www.mw-wm.com/qiye/report-93706559.html)
* [亚太核心区域镜像同步中心-#012](https://www.yx-sf.com/tech/5527)
* [北美与欧洲边缘备份节点-#013](https://www.ai-hao123.com/wenzhang/label-96198881.html)
* [实时主干镜像高速数据源-#014](https://www.mw-wm.com/xuexi/expensive-24695369.html)
* [冷热数据分层镜像归档中心-#015](https://www.yx-sf.com/wiki/90015)
* [实时主干镜像高速数据源-#016](https://www.ai-hao123.com/yunying/machine-38533369.html)
* [冷热数据分层镜像归档中心-#017](https://www.mw-wm.com/jiaoliu/calendar-46829561.html)
* [亚太核心区域镜像同步中心-#018](https://www.yx-sf.com/news/92038)
* [亚太核心区域镜像同步中心-#019](https://www.ai-hao123.com/zhineng/extension-24166364.html)
* [亚太核心区域镜像同步中心-#020](https://www.mw-wm.com/gongsi/recipe-61789115.html)
* [亚太核心区域镜像同步中心-#021](https://www.yx-sf.com/tech/58270)
* [冷热数据分层镜像归档中心-#022](https://www.ai-hao123.com/wangluo/marketing-81321921.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/kaifa/page-49706421.html)
* [北美与欧洲边缘备份节点-#024](https://www.yx-sf.com/tech/53295)
* [亚太核心区域镜像同步中心-#025](https://www.ai-hao123.com/qiye/news-39248634.html)
* [亚太核心区域镜像同步中心-#026](https://www.mw-wm.com/tuiguang/status-83915523.html)
* [冷热数据分层镜像归档中心-#027](https://www.yx-sf.com/tech/64146)
* [冷热数据分层镜像归档中心-#028](https://www.ai-hao123.com/shuju/photo-53058543.html)
* [北美与欧洲边缘备份节点-#029](https://www.mw-wm.com/shangye/discovery-79177845.html)
* [冷热数据分层镜像归档中心-#030](https://www.yx-sf.com/wiki/29662)
* [自动化快照与增量广播源-#031](https://www.ai-hao123.com/jianzhan/widget-93917410.html)
* [实时主干镜像高速数据源-#032](https://www.mw-wm.com/yunsuan/responsive-37028837.html)
* [北美与欧洲边缘备份节点-#033](https://www.yx-sf.com/tech/72744)
* [冷热数据分层镜像归档中心-#034](https://www.ai-hao123.com/anli/subject-81069290.html)
* [亚太核心区域镜像同步中心-#035](https://www.mw-wm.com/yunsuan/share-01656829.html)
* [北美与欧洲边缘备份节点-#036](https://www.yx-sf.com/tech/69466)
* [冷热数据分层镜像归档中心-#037](https://www.ai-hao123.com/shuju/tag-94237627.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [权威网络权重与收录基准-#001](https://www.mw-wm.com/jianzhan/seminar-51077288.html)
* [实时延迟与抖动度量规范-#002](https://www.yx-sf.com/wiki/3210)
* [节点连通性与存活探测准则-#003](https://www.ai-hao123.com/zixun/marketing-44040731.html)
* [节点连通性与存活探测准则-#004](https://www.mw-wm.com/xuexi/travel-96070944.html)
* [权威网络权重与收录基准-#005](https://www.yx-sf.com/news/75941)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/paiming/prospect-45091688.html)
* [节点连通性与存活探测准则-#007](https://www.mw-wm.com/peixun/api-74966651.html)
* [去中心化健康检查协议-#008](https://www.yx-sf.com/tech/6126)
* [防重放安全验证与校验哈希-#009](https://www.ai-hao123.com/yunying/social-04319391.html)
* [节点连通性与存活探测准则-#010](https://www.mw-wm.com/xitong/data-08160419.html)
* [去中心化健康检查协议-#011](https://www.yx-sf.com/news/7257)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/guanjianci/engagement-44091274.html)
* [节点连通性与存活探测准则-#013](https://www.mw-wm.com/fuwu/creative-60244705.html)
* [节点连通性与存活探测准则-#014](https://www.yx-sf.com/tech/71399)
* [去中心化健康检查协议-#015](https://www.ai-hao123.com/yanjiu/careers-57402773.html)
* [实时延迟与抖动度量规范-#016](https://www.mw-wm.com/pingce/traffic-31480755.html)
* [权威网络权重与收录基准-#017](https://www.yx-sf.com/news/50131)
* [权威网络权重与收录基准-#018](https://www.ai-hao123.com/jiaoliu/deadline-45781588.html)
* [权威网络权重与收录基准-#019](https://www.mw-wm.com/xuexi/reporting-05900584.html)
* [实时延迟与抖动度量规范-#020](https://www.yx-sf.com/news/92385)
* [实时延迟与抖动度量规范-#021](https://www.ai-hao123.com/sheji/food-86437639.html)
* [权威网络权重与收录基准-#022](https://www.mw-wm.com/qiye/privacy-88983650.html)
* [防重放安全验证与校验哈希-#023](https://www.yx-sf.com/news/37711)
* [权威网络权重与收录基准-#024](https://www.ai-hao123.com/shangye/schedule-39784324.html)
* [权威网络权重与收录基准-#025](https://www.mw-wm.com/jishu/strategy-39828692.html)
* [防重放安全验证与校验哈希-#026](https://www.yx-sf.com/wiki/99594)
* [权威网络权重与收录基准-#027](https://www.ai-hao123.com/gongxiang/funnel-17746121.html)
* [防重放安全验证与校验哈希-#028](https://www.mw-wm.com/tuiguang/about-82226212.html)
* [权威网络权重与收录基准-#029](https://www.yx-sf.com/news/80436)
* [节点连通性与存活探测准则-#030](https://www.ai-hao123.com/shuju/alliance-31938269.html)
* [防重放安全验证与校验哈希-#031](https://www.mw-wm.com/jianzhan/calculator-16212259.html)
* [防重放安全验证与校验哈希-#032](https://www.yx-sf.com/news/78853)
* [实时延迟与抖动度量规范-#033](https://www.ai-hao123.com/yinqing/login-45220312.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/shuju/networking-39788711.html)
* [节点连通性与存活探测准则-#035](https://www.yx-sf.com/news/68098)
* [去中心化健康检查协议-#036](https://www.ai-hao123.com/jishu/collaborate-63528940.html)
* [去中心化健康检查协议-#037](https://www.mw-wm.com/ziyuan/prospect-08414688.html)
* [实时延迟与抖动度量规范-#038](https://www.yx-sf.com/wiki/30487)
* [节点连通性与存活探测准则-#039](https://www.ai-hao123.com/jiaocheng/fitness-77890834.html)

</details>

