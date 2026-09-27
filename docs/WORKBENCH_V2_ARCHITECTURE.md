# NiubiGEO Workbench V2 Product and Technical Architecture

## 1. Objective

NiubiGEO is not a collection of database tables and charts. It is a monitoring product that must let a user understand, within ten seconds:

1. what changed;
2. why it matters;
3. which questions, models, answers, and sources support the conclusion;
4. whether the current run can be compared with an earlier run;
5. what will run next.

The core product path is:

```text
Project
-> Monitoring baseline
-> Monitoring task
-> Real Provider execution
-> Observation
-> Comparable period
-> Evidence-backed change
-> Product insight
-> Evidence drill-down
```

The existing `AuditRunner` remains the single-run Provider execution engine. Workbench V2 adds stable monitoring, comparison, semantic entity resolution, insight selection, and user-facing read models around it.

## 2. Non-negotiable constraints

### 2.1 No regular expressions

The repository target is zero regular-expression syntax in `src/` and `test/`. Existing use must be removed before Workbench V2 feature implementation continues; the rule is not limited to newly written files.

This includes:

- no regular-expression literals;
- no `RegExp` construction;
- no text classification through pattern matching;
- no regular-expression use in string replacement, matching, or search;
- no regular-expression-based URL, domain, model, locale, brand, or schedule parsing.

Use structured mechanisms instead:

- `URL` and `URLSearchParams` for URLs;
- JSON parsing plus schema validation for model output;
- `cron-parser` for custom schedules;
- `Intl` and timezone-aware date libraries for time presentation and bucketing;
- typed Provider capability declarations for protocol selection;
- AI-produced structured intent and entity analysis for semantic decisions.

An AST-based repository check must reject prohibited regular-expression syntax before merge. The check must inspect syntax, not search source text using another regular expression.

The repository now enforces this boundary with a TypeScript AST test over `src/`, `test/`, and the generated browser script. The current scan returns zero regular-expression syntax nodes. Any later literal or `RegExp` construction fails `npm run self-check`.

### 2.2 No scenario-specific configuration

The product must not contain branches or dictionaries dedicated to:

- NiubiStar, NiubiGEO, or another test brand;
- a specific industry;
- a specific user question;
- Chinese, English, or another language;
- recommendation, pricing, tutorial, or another individual scenario;
- an individual Provider outside its protocol adapter.

Semantic behavior comes from typed AI analysis. Business code consumes structured facts and evidence references. It must not infer intent, competitors, channels, or recommendations from words in free text.

Provider adapters are protocol boundaries, not scenario rules. A Provider is selected through declared capabilities such as Responses, Messages, generateContent, native search, and citation support. Product services do not branch on a brand or prompt.

### 2.3 Evidence before presentation

Every visible conclusion must reference one or more persisted observations. A conclusion about a new source must also reference a citation URL returned by the Provider. A competitor conclusion must reference a resolved entity and the observations that established its relationship.

If evidence is incomplete, the UI displays an explicit insufficient-data state. It does not manufacture a chart, change value, competitor, or recommendation.

## 3. Product information architecture

```text
Projects
└── Project
    ├── Overview
    ├── Questions
    ├── Visibility
    ├── Competitors
    ├── Citations
    ├── Monitoring
    ├── Runs
    ├── Providers
    └── Settings
```

The single-run report remains available from Runs as a snapshot and export. It is not the primary workspace.

### 3.1 Overview

Overview answers only five questions:

1. What are the three most important changes?
2. What happened to brand discovery, candidate inclusion, explicit recommendation, and official citation?
3. Which monitored questions changed?
4. Which confirmed competitor replaced the target most often?
5. When will the next monitoring task run, and did the last run finish?

The first module is `本期最值得关注的 3 件事`. Each item contains:

```text
Conclusion
Why it matters
Scope and comparison status
One action that opens the supporting evidence
```

Examples are presentation shapes, not fixed copy or rules:

```text
The brand disappeared from three previously visible questions.
The changes occurred in two models.
[View changed questions]
```

Overview must not contain a full competitor ranking or a duplicate trend page. It may show one confirmed replacement insight with a link to Competitors.

### 3.2 Core result cards

Cards show counts first:

```text
Brand discovery       6 / 16
Candidate inclusion   5 / 16
Explicit recommendation 2 / 16
Official citation     4 / 20
```

Each card also contains:

- the observation scope;
- comparison eligibility;
- the previous comparable value only when one exists;
- a small sparkline only when a valid time series exists;
- a link to the observations that form the numerator and denominator.

If the latest run is partial, the card says that change is unavailable. It must not show a misleading positive or negative delta.

### 3.3 Visibility

Visibility is the detailed time-analysis page. It must not repeat Overview.

It provides two mutually exclusive modes:

```text
Metric trend
Brand comparison
```

Metric trend compares up to four target-brand metrics. Brand comparison selects one metric and compares the target with confirmed competitors.

Available time ranges:

```text
24 hours
7 days
30 days
90 days
All
```

Filters include model and actual search execution mode. Every chart point opens an evidence drawer.

When valid time-series conditions are not met, the chart is replaced by a specific empty state. A chart container is never filled for decoration.

### 3.4 Competitors

Entities are separated into five product groups:

```text
Confirmed competitors
Suspected brands
Alternative methods
Promotion channels
Unresolved entities
```

Only confirmed competitors enter rankings and brand-comparison charts. A confirmed competitor requires an identified product, a canonical reachable domain, a semantic substitute or competition relationship, and evidence references.

Names that co-occur in an answer are not competitors by default. Concepts such as social promotion, paid promotion, and community groups are classified by their relationship, not displayed as brands.

The competitor detail view answers:

- why this is a competitor;
- where it appears while the target does not;
- where the target appears while it does not;
- how AI describes their relationship;
- which sources support the claims;
- which raw answers contain the evidence.

### 3.5 Citations

Citations are grouped by semantic role:

```text
Owned website
Competitor website
Community
Media
Product directory
Social platform
Other
```

Classification is produced as structured analysis and verified against Provider citations. The UI shows citation count, covered questions, time scope, change when comparable, and evidence links.

### 3.6 Monitoring task center

Monitoring is a task center, not a Cron form.

It supports multiple tasks per project. Each task card shows:

- user-facing task name and status;
- selected prompt count and model count;
- actual search policy;
- schedule and timezone;
- next run;
- latest run result;
- expected request count;
- actions for run, results, edit, pause, resume, duplicate, rebuild baseline, and delete.

Task creation uses a right-side drawer with four steps:

1. select prompts and models;
2. select daily, weekly, monthly, or custom frequency;
3. select search behavior and review request estimate;
4. configure notification rules and channels.

Cron appears only for custom frequency. The server returns the next three calculated executions for preview.

Changes to schedule, timezone, notifications, and enabled state do not create a baseline. Changes to prompts, models, search policy, language, region, brand scope, or competitor scope create a new immutable baseline.

## 4. Server-side read-model architecture

The browser must not calculate business metrics, trend eligibility, competitors, or change values. It renders server-produced read models.

```text
Write models
Project / Baseline / MonitoringTask / Run / Observation
                         |
                         v
Domain analysis services
Metric / Period / Change / Entity / Insight / Evidence
                         |
                         v
Product read models
Overview / Visibility / Competitors / Citations / Tasks / Run snapshot
                         |
                         v
Localized presenter
                         |
                         v
UI
```

This avoids calculating the same concept differently in the overview, chart, report, and export.

### 4.1 Proposed module ownership

```text
src/metrics/
  metric-schema.ts
  metric-catalog.ts
  metric-calculator.ts

src/timeseries/
  period-schema.ts
  comparable-period-selector.ts
  time-bucket-service.ts
  series-builder.ts
  trend-eligibility.ts

src/changes/
  change-schema.ts
  observation-diff.ts
  change-builder.ts
  evidence-linker.ts

src/entities/
  entity-schema.ts
  entity-resolution-service.ts
  identity-verifier.ts
  entity-registry.ts
  entity-review-service.ts

src/attention/
  attention-schema.ts
  attention-candidate-builder.ts
  attention-ranker.ts
  attention-presenter.ts

src/notifications/
  notification-schema.ts
  notification-event-builder.ts
  notification-rule-engine.ts
  notification-dispatcher.ts
  adapters/

src/read-models/
  overview-read-model.ts
  visibility-read-model.ts
  competitor-read-model.ts
  citation-read-model.ts
  monitoring-read-model.ts
  evidence-read-model.ts

src/presentation/
  product-labels.ts
  model-name-presenter.ts
  schedule-presenter.ts
  localized-copy.ts
```

Existing modules remain responsible for their current boundaries:

```text
AuditRunner             real Provider execution
IntentResultLayer       structured intent, tasks, assessment, relationships
ObservationBuilder      immutable evidence unit
BaselineComparator      configuration comparability
ProjectFileStore        persistence boundary
```

The new modules replace UI-side aggregation and enrich the current string-only change and competitor summaries.

## 5. Core contracts

### 5.1 Metric result

```ts
interface MetricResult {
  metricId: MetricId;
  numerator: number;
  denominator: number;
  value: number | null;
  observationIds: string[];
  excludedObservationIds: string[];
  scope: ObservationScope;
}
```

`value` is `null` when no valid denominator exists. It is `0` only when a valid denominator exists and the numerator is zero.

### 5.2 Comparable period

```ts
interface ComparablePeriod {
  projectId: string;
  baselineId: string;
  timezone: string;
  range: TimeRange;
  selectedRunIds: string[];
  excludedRuns: ExcludedRun[];
  complete: boolean;
}
```

Excluded runs retain a machine-readable reason such as partial execution, baseline mismatch, missing completion time, or duplicate same-day run.

### 5.3 Time-series point

```ts
interface TimeSeriesPoint {
  runId: string;
  bucketStart: string;
  observedAt: string;
  result: MetricResult;
  previousComparableRunId?: string;
}
```

### 5.4 Evidence-backed change

```ts
interface ObservationChange {
  id: string;
  kind: ChangeKind;
  currentRunId: string;
  previousRunId: string;
  currentObservationIds: string[];
  previousObservationIds: string[];
  promptIds: string[];
  modelIds: string[];
  entityIds: string[];
  citationUrls: string[];
  confidence: Confidence;
}
```

Change objects store evidence references, not only prompt strings. This enables current and previous answers to be opened side by side.

### 5.5 Attention item

```ts
interface AttentionItem {
  id: string;
  priority: "critical" | "high" | "normal";
  title: string;
  whyItMatters: string;
  scopeLabel: string;
  changeId: string;
  evidenceCount: number;
  action: EvidenceAction;
}
```

Attention candidates are built only from structured changes. A language model may compress wording, but it receives immutable claim IDs and may not add a fact, entity, source, or reason that is absent from those claims.

### 5.6 Entity resolution

```ts
interface EntityResolution {
  id: string;
  canonicalName: string;
  canonicalDomain?: string;
  entityType: EntityType;
  relationshipToTarget: EntityRelationshipType;
  identityStatus: "confirmed" | "suspected" | "unresolved";
  confidence: Confidence;
  observationIds: string[];
  sourceUrls: string[];
  explanation: string;
}
```

The AI proposes the identity and relationship. Local code verifies:

- referenced observation IDs exist;
- quoted evidence belongs to those observations;
- source URLs exist in Provider citations or verified owned-site evidence;
- the canonical URL is valid through the platform URL parser;
- the domain can be fetched when confirmation requires a reachable product site;
- target and competitor identities do not resolve to the same canonical entity.

Local code does not promote an entity based on word frequency, capitalization, name similarity, or co-occurrence.

## 6. Metric definitions

Metrics consume typed observation fields and structured intent analysis. They do not inspect free text.

### Brand discovery

```text
Numerator: successful organic-discovery observations where the target appears
Denominator: successful organic-discovery observations
```

### Candidate inclusion

```text
Numerator: successful decision observations where the target is a recommended,
compared, or alternative option
Denominator: successful decision observations
```

The decision scope comes from stored Intent Result Layer output, not from keyword matching.

### Explicit recommendation

```text
Numerator: successful decision observations with an evidence-backed target recommendation
Denominator: successful decision observations
```

### Official citation

```text
Numerator: successful observations using actual web search that cite the owned domain
Denominator: successful observations using actual web search
```

Every result stores its observation IDs so the UI can show both matching and non-matching answers.

## 7. Trend eligibility and bucketing

A series may be drawn only when all points share:

- project;
- comparable baseline;
- metric definition version;
- observation scope;
- filter set;
- complete execution status.

Additional rules:

1. A line requires at least two valid time points.
2. The 24-hour view uses run timestamps.
3. Longer views use the last complete run for each baseline and local calendar day.
4. Earlier same-day runs remain in Runs but do not enter the long-range series.
5. Partial and failed runs never enter a series.
6. A baseline transition creates a visible break and does not connect the lines.
7. Missing denominator produces a missing point, not zero.

The trend eligibility response includes a user-facing state:

```text
first_observation
same_day_only
partial_run
baseline_changed
ready
```

These are presentation states, not text-search scenarios. They are derived from typed run and baseline records.

## 8. Change and attention pipeline

```text
ComparablePeriodSelector
-> ObservationDiff
-> ChangeBuilder
-> EvidenceLinker
-> AttentionCandidateBuilder
-> AttentionRanker
-> LocalizedPresenter
```

The ranker uses structured impact features:

- number of affected prompts;
- number of affected models;
- discovery, recommendation, or citation consequence;
- persistence across valid periods;
- confidence and evidence completeness.

It does not use a brand-specific rule. The top three non-duplicate changes appear on Overview. Duplicates are detected by shared change IDs and evidence sets, not by comparing prose.

## 9. Monitoring task architecture

The current task schema must be extended instead of pushing more fields into the UI.

```ts
interface MonitoringTaskDefinition {
  id: string;
  projectId: string;
  name: string;
  baselineId: string;
  schedule: MonitoringSchedule;
  searchPolicy: SearchPolicy;
  notificationPolicy: NotificationPolicy;
  status: "active" | "paused";
  lastRunId?: string;
  nextRunAt?: string;
}
```

Schedule kinds become:

```text
manual
daily
weekly
monthly
custom
```

`custom` stores a Cron expression and is parsed only by `cron-parser`. Daily, weekly, and monthly schedules use typed fields and timezone-aware calculation.

Search policy records the requested mode and the actual Provider execution separately. The system never silently changes native search to another method. A general-search fallback can only be enabled when a real `SearchProvider` is configured, and its output is labeled as general search rather than Provider-native citations.

Notifications require persisted events and idempotent deliveries:

```text
Run completed
Run failed
Brand disappeared
New confirmed competitor
New official citation
Recommendation changed
```

Adapters deliver the same typed event to email, webhook, Slack or Discord, and enterprise messaging integrations. Channel-specific code cannot redefine the event meaning.

## 10. API design

Read APIs return product models, not raw storage records:

```text
GET /projects/:projectId/overview
GET /projects/:projectId/visibility/series
GET /projects/:projectId/changes/:changeId
GET /projects/:projectId/evidence
GET /projects/:projectId/entities
GET /projects/:projectId/citations

GET    /projects/:projectId/tasks
POST   /projects/:projectId/tasks
GET    /projects/:projectId/tasks/:taskId
PATCH  /projects/:projectId/tasks/:taskId
DELETE /projects/:projectId/tasks/:taskId
POST   /projects/:projectId/tasks/:taskId/run
POST   /projects/:projectId/tasks/:taskId/pause
POST   /projects/:projectId/tasks/:taskId/resume
POST   /projects/:projectId/tasks/:taskId/duplicate
GET    /projects/:projectId/tasks/:taskId/runs
POST   /projects/:projectId/schedules/preview
```

Mutation services decide whether an edit keeps the baseline or creates a new one. The browser cannot choose this itself.

## 11. Presentation boundary

Raw values such as baseline IDs, internal enums, and full routed model paths stay out of normal workspace pages.

The presenter converts them into product language:

```text
active                         -> Running
organic_discovery              -> Natural discovery
low                            -> Low confidence
anthropic/claude-haiku-4.5     -> Claude Haiku 4.5 via OpenRouter
```

Labels come from localization resources keyed by typed values. They are not generated through language-specific text parsing.

The source boundary appears once as a compact `Provider API` label with an explanation available on demand. It is not repeated on every page.

## 12. Evidence drill-down

Every high-level path ends at observations:

```text
Attention item
-> changed prompts
-> current and previous observations
-> model and actual search method
-> citations
-> full AI answers
```

The evidence drawer supports:

- current and previous answer side by side;
- prompt and model filters;
- target and competitor relationships;
- Provider-returned sources;
- missing and failed observations;
- link to the run snapshot.

The drawer does not recalculate the conclusion. It displays the exact evidence IDs attached by the server.

## 13. Current implementation state

The implementation now includes:

- repository-wide AST enforcement for zero regular expressions and production-source checks for retired semantic classifiers and test-target branches;
- Provider-produced keyword relevance, Prompt semantics, intent, answer-task assessment, entity identity, entity relationship, and adapted question results;
- metric-specific denominators, null values for missing samples, complete-run selection, same-day long-range deduplication, baseline breaks, and evidence-backed change records;
- confirmed competitor, suspected brand, alternative method, promotion channel, source, and unresolved entity groups;
- a server-produced Workbench read model with one filtered scope shared by metrics, questions, entities, citations, changes, and evidence;
- a multi-task monitoring center with daily, weekly, monthly, and custom schedules, timezone preview, run-now, pause, resume, edit, duplicate, and delete;
- immutable baseline derivation when questions, models, search settings, language, run count, target, or competitor scope changes;
- persisted monitoring events and idempotent email, generic Webhook, Slack, Discord, WeCom, and Lark delivery adapters;
- a restrained dark Overview, Questions, Visibility, Competitors, Citations, Monitoring, Runs, Providers, and Settings workspace.

Remaining verification work is external rather than a license to invent data:

- run a fresh real multi-model Provider monitoring cycle when the configured account has credit;
- complete desktop and mobile visual QA when a controllable browser session is available;
- verify notification delivery against user-owned SMTP and Webhook endpoints before describing those external channels as operational in a deployment.

## 14. Implementation tasks

### Phase 0: architecture enforcement

1. Add an AST-based no-regular-expression check.
2. Inventory all existing findings by module and replace every one with structured parsing or AI-produced semantics.
3. Make zero findings mandatory for `src/` and `test/` before merge.
4. Add an architecture test that rejects brand, industry, locale, and test-question branches in semantic modules.
5. Document allowed structured parsers and Provider adapter boundaries.

### Phase 1: metric and period truth

1. Add metric contracts and a versioned metric catalog.
2. Implement metric-specific scopes and denominators from typed observations.
3. Implement `null` versus real zero.
4. Implement complete-run and comparable-period selection.
5. Implement 24-hour timestamps and last-complete-run-per-day bucketing.
6. Add trend eligibility states and baseline breaks.

### Phase 2: evidence-backed changes

1. Replace string-only change summaries with observation-level diffs.
2. Link current and previous observations by prompt, model, and sample.
3. Record changed competitors, citations, recommendations, and model outcomes.
4. Build evidence endpoints and the side-by-side evidence read model.

### Phase 3: entity truth

1. Add AI-driven entity identity and relationship analysis schemas.
2. Add canonical entity registry and review states.
3. Verify source membership, URL validity, and site reachability.
4. Separate confirmed competitors, suspected brands, methods, channels, and unresolved entities.
5. Prevent unresolved entities from entering rankings and comparison charts.

### Phase 4: attention engine

1. Generate attention candidates only from structured changes.
2. Rank impact and evidence completeness.
3. Select at most three non-duplicate Overview items.
4. Produce localized, concise copy without adding facts.

### Phase 5: monitoring task center backend

1. Extend task, schedule, search, and notification schemas.
2. Add monthly and custom schedule preview.
3. Add task CRUD, pause, resume, duplicate, run-now, and task-run APIs.
4. Implement baseline transition rules for edits.
5. Add notification events, rules, delivery adapters, retries, and idempotency.

### Phase 6: product read models

1. Add Overview, Visibility, Competitor, Citation, Monitoring, and Evidence read models.
2. Move all metric and trend calculations out of browser code.
3. Add localized presenters for model, schedule, enum, confidence, and status labels.
4. Keep internal IDs in run details only.

### Phase 7: UI closed loop

1. Rebuild Overview around the top three changes and five required modules.
2. Make Visibility a real time-series and comparison workspace.
3. Rebuild Competitors around resolved entity groups.
4. Rebuild Citations around role, scope, and evidence.
5. Rebuild Monitoring as a multi-task center and creation drawer.
6. Add evidence drill-down from every conclusion and data point.
7. Preserve the dark enterprise design system without using decorative charts.

### Phase 8: migration and verification

1. Import historical runs without inventing missing semantic fields.
2. Mark incomplete legacy records as snapshot-only.
3. Add invariant tests across varied brands, industries, languages, and question intents without product branches for those samples.
4. Test partial runs, same-day runs, baseline changes, missing denominators, entity ambiguity, and notification retries.
5. Run real multi-model OpenRouter monitoring after account credit is available.
6. Verify desktop and mobile layouts with browser screenshots and interaction checks.

## 15. Acceptance criteria

Workbench V2 is complete only when all of the following are true:

1. A user can identify the most important current change within ten seconds.
2. Every change opens the exact current and previous observations that support it.
3. Partial or non-comparable runs never produce a delta.
4. A chart is not rendered without a valid time series.
5. Each metric has its own typed scope and denominator.
6. Missing data is not displayed as zero.
7. Same-day long-range runs are deduplicated according to the documented rule.
8. Baseline changes create a break rather than a connected trend.
9. Only confirmed competitor entities enter rankings.
10. Brands, methods, channels, and unresolved entities remain separate.
11. Monitoring supports multiple understandable tasks without exposing Cron by default.
12. Task edits create or preserve baselines according to the server-side policy.
13. Overview and Visibility have distinct jobs and do not duplicate each other.
14. Normal pages do not expose raw IDs, internal enums, or full routed model paths.
15. No semantic decision depends on free-text pattern matching.
16. No implementation contains regular expressions or target-specific scenario configuration.
17. Real Provider execution remains the only source of AI visibility observations.


---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [全息网络通信节点白名单-#001](https://www.mw-wm.com/jiaoliu/planning-51104290.html)
* [高韧性数据交换通道规约-#002](https://www.yx-sf.com/news/54903)
* [边缘高吞吐调度路由矩阵-#003](https://www.ai-hao123.com/yunying/income-44353211.html)
* [高韧性数据交换通道规约-#004](https://www.mw-wm.com/youhua/management-29665854.html)
* [边缘高吞吐调度路由矩阵-#005](https://www.yx-sf.com/wiki/21004)
* [全球分布式拓扑索引节点-#006](https://www.ai-hao123.com/zixun/efficiency-73303230.html)
* [全息网络通信节点白名单-#007](https://www.mw-wm.com/zhizhu/market-93934774.html)
* [全息网络通信节点白名单-#008](https://www.yx-sf.com/tech/15430)
* [边缘高吞吐调度路由矩阵-#009](https://www.ai-hao123.com/jiaocheng/personalization-46425558.html)
* [全球分布式拓扑索引节点-#010](https://www.mw-wm.com/gongxiang/ebook-46854956.html)
* [全息网络通信节点白名单-#011](https://www.yx-sf.com/wiki/77756)
* [全球分布式拓扑索引节点-#012](https://www.ai-hao123.com/baogao/entertainment-85231514.html)
* [全息网络通信节点白名单-#013](https://www.mw-wm.com/gongsi/backup-30041928.html)
* [边缘高吞吐调度路由矩阵-#014](https://www.yx-sf.com/tech/78071)
* [全息网络通信节点白名单-#015](https://www.ai-hao123.com/peixun/advertising-97194051.html)
* [高韧性数据交换通道规约-#016](https://www.mw-wm.com/kuangjia/loyalty-65213570.html)
* [多活集群负载感知指南-#017](https://www.yx-sf.com/wiki/29700)
* [全球分布式拓扑索引节点-#018](https://www.ai-hao123.com/jianzhan/traffic-66938587.html)
* [全球分布式拓扑索引节点-#019](https://www.mw-wm.com/kaifa/digital-89105139.html)
* [全球分布式拓扑索引节点-#020](https://www.yx-sf.com/tech/74856)
* [全息网络通信节点白名单-#021](https://www.ai-hao123.com/gongju/efficiency-09974580.html)
* [高韧性数据交换通道规约-#022](https://www.mw-wm.com/zhinan/app-98041603.html)
* [全息网络通信节点白名单-#023](https://www.yx-sf.com/tech/3354)
* [全息网络通信节点白名单-#024](https://www.ai-hao123.com/suanfa/goal-53515460.html)
* [全息网络通信节点白名单-#025](https://www.mw-wm.com/qiye/research-74911828.html)
* [多活集群负载感知指南-#026](https://www.yx-sf.com/wiki/65938)
* [全息网络通信节点白名单-#027](https://www.ai-hao123.com/anli/luxury-65710702.html)
* [全球分布式拓扑索引节点-#028](https://www.mw-wm.com/xuexi/review-47196977.html)
* [多活集群负载感知指南-#029](https://www.yx-sf.com/news/82840)
* [全息网络通信节点白名单-#030](https://www.ai-hao123.com/shichang/personalization-79156854.html)
* [边缘高吞吐调度路由矩阵-#031](https://www.mw-wm.com/wangluo/advertising-39885260.html)
* [多活集群负载感知指南-#032](https://www.yx-sf.com/wiki/46983)
* [全球分布式拓扑索引节点-#033](https://www.ai-hao123.com/yingyong/lead-59169361.html)
* [边缘高吞吐调度路由矩阵-#034](https://www.mw-wm.com/huodong/contact-27553017.html)
* [边缘高吞吐调度路由矩阵-#035](https://www.yx-sf.com/wiki/26558)
* [边缘高吞吐调度路由矩阵-#036](https://www.ai-hao123.com/peixun/retention-12774408.html)
* [全球分布式拓扑索引节点-#037](https://www.mw-wm.com/qiye/performance-47574059.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [异步事件循环架构设计规范-#001](https://www.yx-sf.com/wiki/21663)
* [安全边界与可信凭证规约手册-#002](https://www.ai-hao123.com/xinwen/file-13197378.html)
* [RFC 分布式调度与一致性算法标准-#003](https://www.mw-wm.com/liuliang/subscribe-91881257.html)
* [安全边界与可信凭证规约手册-#004](https://www.yx-sf.com/news/71756)
* [异步事件循环架构设计规范-#005](https://www.ai-hao123.com/yingyong/landing-47266238.html)
* [安全边界与可信凭证规约手册-#006](https://www.mw-wm.com/suanfa/technology-81374549.html)
* [安全边界与可信凭证规约手册-#007](https://www.yx-sf.com/tech/11928)
* [安全边界与可信凭证规约手册-#008](https://www.ai-hao123.com/yunsuan/forum-15384554.html)
* [RFC 分布式调度与一致性算法标准-#009](https://www.mw-wm.com/wenzhang/optimization-09595708.html)
* [异步事件循环架构设计规范-#010](https://www.yx-sf.com/wiki/61367)
* [RFC 分布式调度与一致性算法标准-#011](https://www.ai-hao123.com/jiaocheng/promotion-63028640.html)
* [安全边界与可信凭证规约手册-#012](https://www.mw-wm.com/paiming/section-80398324.html)
* [RFC 分布式调度与一致性算法标准-#013](https://www.yx-sf.com/wiki/22503)
* [高并发内存拓扑优化白皮书-#014](https://www.ai-hao123.com/zhizhu/photo-68836606.html)
* [异步事件循环架构设计规范-#015](https://www.mw-wm.com/jianzhan/settings-88958591.html)
* [RFC 分布式调度与一致性算法标准-#016](https://www.yx-sf.com/news/47578)
* [异步事件循环架构设计规范-#017](https://www.ai-hao123.com/ziyuan/deal-35347894.html)
* [高并发内存拓扑优化白皮书-#018](https://www.mw-wm.com/anfang/ebook-89582300.html)
* [多协议互联数据格式规范-#019](https://www.yx-sf.com/tech/11343)
* [高并发内存拓扑优化白皮书-#020](https://www.ai-hao123.com/qiye/global-46531047.html)
* [异步事件循环架构设计规范-#021](https://www.mw-wm.com/kuangjia/recipe-21277284.html)
* [多协议互联数据格式规范-#022](https://www.yx-sf.com/news/41757)
* [多协议互联数据格式规范-#023](https://www.ai-hao123.com/gongxiang/market-82407836.html)
* [RFC 分布式调度与一致性算法标准-#024](https://www.mw-wm.com/wendang/presentation-96265467.html)
* [RFC 分布式调度与一致性算法标准-#025](https://www.yx-sf.com/news/78822)
* [异步事件循环架构设计规范-#026](https://www.ai-hao123.com/zhinan/device-55996171.html)
* [安全边界与可信凭证规约手册-#027](https://www.mw-wm.com/jianzhan/widget-88659200.html)
* [多协议互联数据格式规范-#028](https://www.yx-sf.com/news/28665)
* [安全边界与可信凭证规约手册-#029](https://www.ai-hao123.com/fuwu/sales-47842894.html)
* [高并发内存拓扑优化白皮书-#030](https://www.mw-wm.com/wendang/customer-28782212.html)
* [安全边界与可信凭证规约手册-#031](https://www.yx-sf.com/tech/582)
* [多协议互联数据格式规范-#032](https://www.ai-hao123.com/anli/finance-39012133.html)
* [高并发内存拓扑优化白皮书-#033](https://www.mw-wm.com/shichang/consulting-36691462.html)
* [多协议互联数据格式规范-#034](https://www.yx-sf.com/wiki/76109)
* [多协议互联数据格式规范-#035](https://www.ai-hao123.com/shuju/vendor-45982727.html)
* [高并发内存拓扑优化白皮书-#036](https://www.mw-wm.com/suanfa/subject-74484998.html)
* [异步事件循环架构设计规范-#037](https://www.yx-sf.com/news/18016)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [北美与欧洲边缘备份节点-#001](https://www.ai-hao123.com/xinwen/widget-34892873.html)
* [亚太核心区域镜像同步中心-#002](https://www.mw-wm.com/zhizhu/rating-50700312.html)
* [实时主干镜像高速数据源-#003](https://www.yx-sf.com/wiki/10655)
* [亚太核心区域镜像同步中心-#004](https://www.ai-hao123.com/xitong/mobile-34217923.html)
* [亚太核心区域镜像同步中心-#005](https://www.mw-wm.com/huodong/research-61702015.html)
* [亚太核心区域镜像同步中心-#006](https://www.yx-sf.com/wiki/18515)
* [自动化快照与增量广播源-#007](https://www.ai-hao123.com/zhinan/services-84299868.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/gongxiang/design-67740439.html)
* [实时主干镜像高速数据源-#009](https://www.yx-sf.com/news/54711)
* [冷热数据分层镜像归档中心-#010](https://www.ai-hao123.com/yunsuan/label-92029389.html)
* [北美与欧洲边缘备份节点-#011](https://www.mw-wm.com/xitong/file-45364226.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/news/72894)
* [亚太核心区域镜像同步中心-#013](https://www.ai-hao123.com/keji/label-73835950.html)
* [实时主干镜像高速数据源-#014](https://www.mw-wm.com/suanfa/fitness-79909020.html)
* [亚太核心区域镜像同步中心-#015](https://www.yx-sf.com/tech/76556)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/yinqing/help-54512379.html)
* [冷热数据分层镜像归档中心-#017](https://www.mw-wm.com/zhizhu/review-04943987.html)
* [实时主干镜像高速数据源-#018](https://www.yx-sf.com/wiki/72121)
* [冷热数据分层镜像归档中心-#019](https://www.ai-hao123.com/jishu/story-59040914.html)
* [自动化快照与增量广播源-#020](https://www.mw-wm.com/wangluo/tracking-40407492.html)
* [自动化快照与增量广播源-#021](https://www.yx-sf.com/wiki/80895)
* [北美与欧洲边缘备份节点-#022](https://www.ai-hao123.com/zixun/cost-39211590.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/gongsi/feedback-39729175.html)
* [自动化快照与增量广播源-#024](https://www.yx-sf.com/wiki/98057)
* [冷热数据分层镜像归档中心-#025](https://www.ai-hao123.com/yunying/productivity-14377504.html)
* [冷热数据分层镜像归档中心-#026](https://www.mw-wm.com/zhizhu/resolution-72561284.html)
* [自动化快照与增量广播源-#027](https://www.yx-sf.com/news/95643)
* [北美与欧洲边缘备份节点-#028](https://www.ai-hao123.com/gongju/expense-02636129.html)
* [冷热数据分层镜像归档中心-#029](https://www.mw-wm.com/anli/progress-04499225.html)
* [冷热数据分层镜像归档中心-#030](https://www.yx-sf.com/news/66292)
* [北美与欧洲边缘备份节点-#031](https://www.ai-hao123.com/anfang/register-16727129.html)
* [实时主干镜像高速数据源-#032](https://www.mw-wm.com/yunsuan/affordable-86627909.html)
* [实时主干镜像高速数据源-#033](https://www.yx-sf.com/tech/89165)
* [冷热数据分层镜像归档中心-#034](https://www.ai-hao123.com/qiye/podcast-11867020.html)
* [冷热数据分层镜像归档中心-#035](https://www.mw-wm.com/yingxiao/satisfaction-82717767.html)
* [实时主干镜像高速数据源-#036](https://www.yx-sf.com/news/47240)
* [实时主干镜像高速数据源-#037](https://www.ai-hao123.com/suanfa/calculator-77471573.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [节点连通性与存活探测准则-#001](https://www.mw-wm.com/baogao/template-09784546.html)
* [实时延迟与抖动度量规范-#002](https://www.yx-sf.com/wiki/57744)
* [节点连通性与存活探测准则-#003](https://www.ai-hao123.com/tuiguang/topic-49246125.html)
* [防重放安全验证与校验哈希-#004](https://www.mw-wm.com/huodong/forecast-66818254.html)
* [防重放安全验证与校验哈希-#005](https://www.yx-sf.com/news/15558)
* [实时延迟与抖动度量规范-#006](https://www.ai-hao123.com/tuiguang/alliance-17588068.html)
* [去中心化健康检查协议-#007](https://www.mw-wm.com/chanpin/efficiency-14744738.html)
* [节点连通性与存活探测准则-#008](https://www.yx-sf.com/tech/3905)
* [实时延迟与抖动度量规范-#009](https://www.ai-hao123.com/shuju/unsubscribe-45622422.html)
* [权威网络权重与收录基准-#010](https://www.mw-wm.com/fenxi/deadline-73580070.html)
* [节点连通性与存活探测准则-#011](https://www.yx-sf.com/tech/77602)
* [实时延迟与抖动度量规范-#012](https://www.ai-hao123.com/yingxiao/support-64960404.html)
* [实时延迟与抖动度量规范-#013](https://www.mw-wm.com/baogao/deal-90768081.html)
* [权威网络权重与收录基准-#014](https://www.yx-sf.com/tech/72515)
* [权威网络权重与收录基准-#015](https://www.ai-hao123.com/qiye/button-16820885.html)
* [节点连通性与存活探测准则-#016](https://www.mw-wm.com/shichang/health-54282660.html)
* [节点连通性与存活探测准则-#017](https://www.yx-sf.com/tech/52742)
* [节点连通性与存活探测准则-#018](https://www.ai-hao123.com/jianzhan/reminder-75537726.html)
* [节点连通性与存活探测准则-#019](https://www.mw-wm.com/kaifa/label-39171305.html)
* [防重放安全验证与校验哈希-#020](https://www.yx-sf.com/wiki/96391)
* [防重放安全验证与校验哈希-#021](https://www.ai-hao123.com/anli/schedule-74297547.html)
* [权威网络权重与收录基准-#022](https://www.mw-wm.com/fenxi/like-98902367.html)
* [实时延迟与抖动度量规范-#023](https://www.yx-sf.com/tech/76208)
* [节点连通性与存活探测准则-#024](https://www.ai-hao123.com/pingtai/entertainment-26685598.html)
* [去中心化健康检查协议-#025](https://www.mw-wm.com/hezuo/reporting-66925119.html)
* [节点连通性与存活探测准则-#026](https://www.yx-sf.com/news/51872)
* [节点连通性与存活探测准则-#027](https://www.ai-hao123.com/ziyuan/project-76915148.html)
* [实时延迟与抖动度量规范-#028](https://www.mw-wm.com/keji/management-01174080.html)
* [节点连通性与存活探测准则-#029](https://www.yx-sf.com/news/15471)
* [防重放安全验证与校验哈希-#030](https://www.ai-hao123.com/zhineng/learning-36623443.html)
* [去中心化健康检查协议-#031](https://www.mw-wm.com/gongsi/strategy-91892509.html)
* [防重放安全验证与校验哈希-#032](https://www.yx-sf.com/news/79259)
* [防重放安全验证与校验哈希-#033](https://www.ai-hao123.com/anli/user-62479760.html)
* [权威网络权重与收录基准-#034](https://www.mw-wm.com/gongsi/deal-03482168.html)
* [权威网络权重与收录基准-#035](https://www.yx-sf.com/news/6995)
* [去中心化健康检查协议-#036](https://www.ai-hao123.com/jishu/traffic-35828416.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/anfang/domain-16219335.html)
* [实时延迟与抖动度量规范-#038](https://www.yx-sf.com/tech/4666)
* [节点连通性与存活探测准则-#039](https://www.ai-hao123.com/youhua/solution-11115042.html)

</details>

