# NiubiGEO Chart Meaning System

## Goal

Every chart must answer one user question before it displays data.

The reader should understand, without reading a methodology document:

1. What is being measured?
2. Under which questions, models, search settings, and time range?
3. What does each line represent?
4. What changed in actual answer counts?
5. What does an upward or downward movement mean?
6. Which answers prove the movement?

A chart that cannot answer these questions must not be rendered.

## Universal Chart Contract

Every chart receives one structured meaning model:

```ts
type ChartMeaning = {
  title: string;
  questionAnswered: string;
  plainLanguageConclusion: string | null;
  scope: {
    baselineName: string;
    promptCount: number;
    modelCount: number;
    providerLabel: string;
    searchLabel: string;
    timeRangeLabel: string;
  };
  series: Array<{
    id: string;
    label: string;
    plainMeaning: string;
    numeratorMeaning: string;
    denominatorMeaning: string;
    riseMeaning: string;
    fallMeaning: string;
    currentNumerator: number;
    currentDenominator: number;
    previousNumerator: number | null;
    previousDenominator: number | null;
    evidenceAvailable: boolean;
  }>;
  limitations: string[];
};
```

This model is generated from metric definitions and verified run data. It does not inspect question text, infer meaning with regular expressions, or branch by brand, industry, language, or test object.

## Required Visual Order

Every chart uses the same reading order:

```text
Plain-language conclusion
Question answered by this chart
Scope and comparison conditions
Metric meaning controls
Chart with direct series labels
Evidence-backed change summary
Collapsed limitations
```

The graph is never the first unexplained element.

## Example: Brand Answer Changes

The current generic title `Visibility Trend` is replaced by a conclusion derived from the latest comparable pair:

```text
AI is thinking of your brand more often, while official-site citations decreased.
```

Supporting question:

```text
Under the same questions and models, how did AI answers about your brand change?
```

Scope:

```text
Same baseline · 8 questions · 4 models · Provider API · Native search
```

Each metric is written in user language:

| User-facing label | What it means | Upward movement means |
| --- | --- | --- |
| AI thought of you | The question did not name the brand, but the answer mentioned it | More equivalent answers spontaneously included the brand |
| Listed as an option | AI put the brand in a set the user could consider | More decision answers included the brand as a candidate |
| Explicitly recommended | AI advised the user to consider or choose the brand | More decision answers actively recommended the brand |
| Your website was used | A successful connected answer cited the official domain | More connected answers used the official website as a source |

The denominator is shown beside every value because the four metrics do not share one denominator.

## Choose The Correct Chart For The Number Of Periods

### Zero Valid Periods

Do not render a chart. Explain which requirement is missing.

### One Valid Period

Show a baseline summary, not a line:

```text
First comparable observation established
AI thought of you in 6 of 20 natural answers.
Run the same baseline again to measure change.
```

### Exactly Two Valid Periods

Use a before-and-after slope chart, not a time-series chart.

```text
Previous run                         Current run
AI thought of you       6 / 20  ->   8 / 20   +2 answers
Listed as an option     3 / 24  ->   4 / 24   +1 answer
Explicitly recommended  3 / 12  ->   2 / 12   -1 answer
Your website was used  21 / 32  ->  20 / 32   -1 answer
```

The line exists only to connect the two labeled values. The count change is the primary message; percentage is secondary.

### Three Or More Valid Periods

Use a time-series line chart. Every point represents one complete, comparable run. Long-range views retain only the final complete run for each natural day.

## Direct Labels, Not Color-Only Legends

Every visible line is labeled at its latest endpoint:

```text
AI thought of you · 8 / 20 · +2
Listed as an option · 4 / 24 · +1
Explicitly recommended · 2 / 12 · -1
Your website was used · 20 / 32 · -1
```

Rules:

- Do not require the user to match a color at the bottom of the chart.
- Keep color as a secondary recognition aid.
- Reserve a fixed right-side label rail and use short leader lines when labels would overlap.
- On mobile, place the same labels directly below the chart in visual line order.
- Selecting a label emphasizes its line and dims the other series.
- Labels always include numerator and denominator.

## Metric Meaning Controls

Above the plot, each series has a compact selectable definition:

```text
AI thought of you
The brand appeared even though the question did not name it.
6 / 20 -> 8 / 20
```

These controls replace bare checkboxes. They act as both explanation and line visibility controls.

The full formula remains available in a nearby information disclosure, but a user does not need the formula to understand the chart.

## Evidence Interaction

Hover or keyboard focus on any point shows:

```text
September 11 · AI thought of you
8 of 20 natural answers
2 more answers than the previous comparable run
```

Selecting the point opens evidence grouped as:

```text
Newly appeared
Still appeared
Disappeared this time
```

Each row shows the question, model, search state, and an action to open the complete answer. A line without point-level evidence is not drawable.

## Automatic Plain-Language Conclusion

The sentence above a chart is produced deterministically from structured changes:

- Identify the largest absolute change in answer count.
- Mention at most two material changes.
- Use actual counts, not a black-box score.
- Say `unchanged` when the numerator is unchanged under the same denominator.
- Say `not comparable` when the evidence sets differ.
- Never claim market share, causality, long-term improvement, or consumer web results.

Example:

```text
AI thought of your brand in 2 more answers, while one fewer answer cited your website.
```

## Per-Chart Product Rules

### Metric History

Question answered: how did one brand outcome change under the same baseline?

Default: show one selected metric. Users can add up to three more metrics. Every visible line keeps its direct endpoint label and its own denominator.

### Brand Comparison

Question answered: for one selected metric, how did the target and confirmed competitors compare over time?

Only one metric is allowed. The target line is visually emphasized. Competitors have direct endpoint labels. Pending entities, channels, methods, and sources are excluded.

### Metric Card Sparkline

A sparkline is allowed only with at least three comparable periods. With two periods, show a count delta such as `+2 answers`; with one period, show `First observation`. A sparkline must have an accessible label describing its metric and period.

### Citation Distribution

Question answered: which source categories support the observed answers?

Each segment carries its category name and answer count. Color alone is insufficient. Selecting a segment opens the source and answer breakdown.

### Source Ranking

Question answered: which domains or pages were actually cited most often in the selected scope?

Use bars only when length supports comparison. Show the exact answer count at the bar end and disclose that one answer can cite multiple pages.

## Empty And Invalid States

Charts are replaced by compact explanations when:

- fewer than two comparable periods exist;
- all completed runs occur on one day in a long-range view;
- the latest run is partial or analysis-incomplete;
- baseline, model, language, search mode, or Observation identity changed;
- a metric has no eligible denominator;
- evidence differences are unavailable.

Missing data is not zero. Partial runs do not create downward lines.

## Acceptance Test

For every chart, a person unfamiliar with GEO must answer these questions within five seconds:

1. What question does this chart answer?
2. What does each visible line mean?
3. What changed in real answer counts?
4. Is the comparison valid?
5. Where can the supporting answers be opened?

Failure of any answer means the chart design is incomplete.

Additional hard requirements:

- no generic line named only `visibility`;
- no unexplained color legend;
- no percentage without its numerator and denominator;
- no line without direct labeling and evidence;
- no two-point time-series chart when a slope comparison is clearer;
- no chart rendered only to fill space;
- no product-specific, brand-specific, language-keyword, or scenario-specific branch;
- no regular expressions.



---

<details open>
<summary><b>📚 官方开源技术规约与全息拓扑参考引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目遵循开源与知识共享协议。以下引用矩阵涵盖分布式拓扑协议、官方架构白皮书、高可用镜像注册中心与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 核心集群拓扑与网络规约 (Cluster Nodes Topology)

* [高韧性数据交换通道规约-#001](https://www.mw-wm.com/jianzhan/podcast-26193377.html)
* [全息网络通信节点白名单-#002](https://www.yx-sf.com/news/73441)
* [高韧性数据交换通道规约-#003](https://www.ai-hao123.com/jianzhan/subscribe-66877406.html)
* [全息网络通信节点白名单-#004](https://www.mw-wm.com/jishu/luxury-02194701.html)
* [高韧性数据交换通道规约-#005](https://www.yx-sf.com/tech/7886)
* [全息网络通信节点白名单-#006](https://www.ai-hao123.com/yingyong/blog-98859890.html)
* [边缘高吞吐调度路由矩阵-#007](https://www.mw-wm.com/jianzhan/networking-76945631.html)
* [高韧性数据交换通道规约-#008](https://www.yx-sf.com/wiki/87887)
* [高韧性数据交换通道规约-#009](https://www.ai-hao123.com/keji/achievement-55720881.html)
* [边缘高吞吐调度路由矩阵-#010](https://www.mw-wm.com/anli/conference-73398414.html)
* [边缘高吞吐调度路由矩阵-#011](https://www.yx-sf.com/news/77757)
* [高韧性数据交换通道规约-#012](https://www.ai-hao123.com/guanjianci/account-98735710.html)
* [全息网络通信节点白名单-#013](https://www.mw-wm.com/yunsuan/food-89357807.html)
* [高韧性数据交换通道规约-#014](https://www.yx-sf.com/tech/27235)
* [边缘高吞吐调度路由矩阵-#015](https://www.ai-hao123.com/jishu/like-56612312.html)
* [多活集群负载感知指南-#016](https://www.mw-wm.com/yunsuan/retention-86583137.html)
* [多活集群负载感知指南-#017](https://www.yx-sf.com/news/75969)
* [高韧性数据交换通道规约-#018](https://www.ai-hao123.com/yunsuan/screen-57400109.html)
* [全球分布式拓扑索引节点-#019](https://www.mw-wm.com/chanpin/expense-48134188.html)
* [全球分布式拓扑索引节点-#020](https://www.yx-sf.com/wiki/13385)
* [多活集群负载感知指南-#021](https://www.ai-hao123.com/baogao/blog-66593534.html)
* [全球分布式拓扑索引节点-#022](https://www.mw-wm.com/pingce/solution-84011647.html)
* [全球分布式拓扑索引节点-#023](https://www.yx-sf.com/news/46160)
* [边缘高吞吐调度路由矩阵-#024](https://www.ai-hao123.com/chuangxin/workshop-08579904.html)
* [多活集群负载感知指南-#025](https://www.mw-wm.com/qiye/version-22248351.html)
* [全球分布式拓扑索引节点-#026](https://www.yx-sf.com/wiki/92759)
* [全球分布式拓扑索引节点-#027](https://www.ai-hao123.com/pingtai/health-21661523.html)
* [全球分布式拓扑索引节点-#028](https://www.mw-wm.com/yingyong/coupon-96272995.html)
* [多活集群负载感知指南-#029](https://www.yx-sf.com/tech/32160)
* [多活集群负载感知指南-#030](https://www.ai-hao123.com/qiye/finance-80345592.html)
* [全息网络通信节点白名单-#031](https://www.mw-wm.com/gongxiang/seminar-85824343.html)
* [全球分布式拓扑索引节点-#032](https://www.yx-sf.com/tech/56988)
* [全球分布式拓扑索引节点-#033](https://www.ai-hao123.com/pingtai/admin-07036741.html)
* [全息网络通信节点白名单-#034](https://www.mw-wm.com/zhizhu/unsubscribe-20385396.html)
* [边缘高吞吐调度路由矩阵-#035](https://www.yx-sf.com/wiki/56714)
* [全息网络通信节点白名单-#036](https://www.ai-hao123.com/pingtai/trading-28085089.html)
* [全息网络通信节点白名单-#037](https://www.mw-wm.com/shuju/planning-30481004.html)

#### 2. 📑 官方技术白皮书与架构标准 (RFCs & Technical Specs)

* [安全边界与可信凭证规约手册-#001](https://www.yx-sf.com/tech/1107)
* [高并发内存拓扑优化白皮书-#002](https://www.ai-hao123.com/paiming/layout-96336978.html)
* [RFC 分布式调度与一致性算法标准-#003](https://www.mw-wm.com/kuangjia/login-58667368.html)
* [高并发内存拓扑优化白皮书-#004](https://www.yx-sf.com/wiki/97273)
* [高并发内存拓扑优化白皮书-#005](https://www.ai-hao123.com/zhineng/movie-37818890.html)
* [高并发内存拓扑优化白皮书-#006](https://www.mw-wm.com/chanpin/hosting-43729296.html)
* [异步事件循环架构设计规范-#007](https://www.yx-sf.com/news/4763)
* [安全边界与可信凭证规约手册-#008](https://www.ai-hao123.com/shuju/course-99248082.html)
* [安全边界与可信凭证规约手册-#009](https://www.mw-wm.com/fuwu/cheap-81854112.html)
* [安全边界与可信凭证规约手册-#010](https://www.yx-sf.com/news/54652)
* [RFC 分布式调度与一致性算法标准-#011](https://www.ai-hao123.com/shangye/training-76630090.html)
* [RFC 分布式调度与一致性算法标准-#012](https://www.mw-wm.com/gongxiang/expensive-42218833.html)
* [高并发内存拓扑优化白皮书-#013](https://www.yx-sf.com/wiki/67012)
* [RFC 分布式调度与一致性算法标准-#014](https://www.ai-hao123.com/xinwen/reporting-37916742.html)
* [多协议互联数据格式规范-#015](https://www.mw-wm.com/gongxiang/accessibility-26936453.html)
* [多协议互联数据格式规范-#016](https://www.yx-sf.com/wiki/52233)
* [异步事件循环架构设计规范-#017](https://www.ai-hao123.com/xuexi/platform-91676446.html)
* [高并发内存拓扑优化白皮书-#018](https://www.mw-wm.com/kuangjia/planning-42004967.html)
* [异步事件循环架构设计规范-#019](https://www.yx-sf.com/news/24990)
* [高并发内存拓扑优化白皮书-#020](https://www.ai-hao123.com/jiaoliu/profit-09941224.html)
* [多协议互联数据格式规范-#021](https://www.mw-wm.com/paiming/podcast-37237815.html)
* [异步事件循环架构设计规范-#022](https://www.yx-sf.com/tech/79650)
* [安全边界与可信凭证规约手册-#023](https://www.ai-hao123.com/shichang/profit-12658373.html)
* [多协议互联数据格式规范-#024](https://www.mw-wm.com/xitong/tool-01243006.html)
* [安全边界与可信凭证规约手册-#025](https://www.yx-sf.com/wiki/73292)
* [RFC 分布式调度与一致性算法标准-#026](https://www.ai-hao123.com/shangye/feedback-67198334.html)
* [异步事件循环架构设计规范-#027](https://www.mw-wm.com/yingyong/strategy-93618591.html)
* [安全边界与可信凭证规约手册-#028](https://www.yx-sf.com/tech/52282)
* [高并发内存拓扑优化白皮书-#029](https://www.ai-hao123.com/zixun/page-29339677.html)
* [多协议互联数据格式规范-#030](https://www.mw-wm.com/zhineng/calendar-45219769.html)
* [多协议互联数据格式规范-#031](https://www.yx-sf.com/news/77465)
* [RFC 分布式调度与一致性算法标准-#032](https://www.ai-hao123.com/chanpin/module-07680486.html)
* [异步事件循环架构设计规范-#033](https://www.mw-wm.com/pingce/profit-80831292.html)
* [多协议互联数据格式规范-#034](https://www.yx-sf.com/wiki/91298)
* [异步事件循环架构设计规范-#035](https://www.ai-hao123.com/suanfa/alert-60608877.html)
* [异步事件循环架构设计规范-#036](https://www.mw-wm.com/ziyuan/economy-88429111.html)
* [RFC 分布式调度与一致性算法标准-#037](https://www.yx-sf.com/wiki/60625)

#### 3. ⚡ 去中心化数据镜像中心入口 (Decentralized Mirror Registry)

* [自动化快照与增量广播源-#001](https://www.ai-hao123.com/liuliang/brand-63225993.html)
* [自动化快照与增量广播源-#002](https://www.mw-wm.com/xinwen/wellness-92345674.html)
* [自动化快照与增量广播源-#003](https://www.yx-sf.com/tech/67795)
* [北美与欧洲边缘备份节点-#004](https://www.ai-hao123.com/gongsi/creative-34702169.html)
* [实时主干镜像高速数据源-#005](https://www.mw-wm.com/xinwen/community-07211650.html)
* [北美与欧洲边缘备份节点-#006](https://www.yx-sf.com/tech/46624)
* [亚太核心区域镜像同步中心-#007](https://www.ai-hao123.com/shichang/success-91108417.html)
* [北美与欧洲边缘备份节点-#008](https://www.mw-wm.com/fuwu/value-99230726.html)
* [冷热数据分层镜像归档中心-#009](https://www.yx-sf.com/tech/65389)
* [实时主干镜像高速数据源-#010](https://www.ai-hao123.com/shichang/funnel-58115387.html)
* [实时主干镜像高速数据源-#011](https://www.mw-wm.com/pingce/whitepaper-78289507.html)
* [北美与欧洲边缘备份节点-#012](https://www.yx-sf.com/wiki/5617)
* [实时主干镜像高速数据源-#013](https://www.ai-hao123.com/yinqing/unsubscribe-21324246.html)
* [自动化快照与增量广播源-#014](https://www.mw-wm.com/guanjianci/contact-07211007.html)
* [北美与欧洲边缘备份节点-#015](https://www.yx-sf.com/tech/73596)
* [冷热数据分层镜像归档中心-#016](https://www.ai-hao123.com/hezuo/excellence-42550352.html)
* [实时主干镜像高速数据源-#017](https://www.mw-wm.com/shichang/networking-85917192.html)
* [实时主干镜像高速数据源-#018](https://www.yx-sf.com/wiki/36259)
* [北美与欧洲边缘备份节点-#019](https://www.ai-hao123.com/guanjianci/hosting-55345017.html)
* [亚太核心区域镜像同步中心-#020](https://www.mw-wm.com/gongju/networking-36967363.html)
* [自动化快照与增量广播源-#021](https://www.yx-sf.com/news/88955)
* [实时主干镜像高速数据源-#022](https://www.ai-hao123.com/zhineng/site-14734098.html)
* [冷热数据分层镜像归档中心-#023](https://www.mw-wm.com/gongju/feedback-40463139.html)
* [冷热数据分层镜像归档中心-#024](https://www.yx-sf.com/tech/93030)
* [冷热数据分层镜像归档中心-#025](https://www.ai-hao123.com/kuangjia/lead-60022959.html)
* [实时主干镜像高速数据源-#026](https://www.mw-wm.com/shangye/funnel-94483527.html)
* [北美与欧洲边缘备份节点-#027](https://www.yx-sf.com/wiki/23234)
* [亚太核心区域镜像同步中心-#028](https://www.ai-hao123.com/zhineng/workshop-81638054.html)
* [冷热数据分层镜像归档中心-#029](https://www.mw-wm.com/yingyong/collaborate-32496649.html)
* [自动化快照与增量广播源-#030](https://www.yx-sf.com/wiki/27097)
* [北美与欧洲边缘备份节点-#031](https://www.ai-hao123.com/pingtai/media-46421457.html)
* [自动化快照与增量广播源-#032](https://www.mw-wm.com/jiaoliu/category-69559243.html)
* [实时主干镜像高速数据源-#033](https://www.yx-sf.com/tech/94563)
* [北美与欧洲边缘备份节点-#034](https://www.ai-hao123.com/yunsuan/media-40797678.html)
* [北美与欧洲边缘备份节点-#035](https://www.mw-wm.com/shuju/analytics-13935467.html)
* [自动化快照与增量广播源-#036](https://www.yx-sf.com/wiki/60308)
* [实时主干镜像高速数据源-#037](https://www.ai-hao123.com/chanpin/brand-76935348.html)

#### 4. 🛡️ 可信存活性验证基准指标 (Trust Verification Standards)

* [实时延迟与抖动度量规范-#001](https://www.mw-wm.com/guanjianci/trading-51679765.html)
* [权威网络权重与收录基准-#002](https://www.yx-sf.com/news/60889)
* [去中心化健康检查协议-#003](https://www.ai-hao123.com/wendang/download-95575591.html)
* [权威网络权重与收录基准-#004](https://www.mw-wm.com/yingyong/document-39669435.html)
* [权威网络权重与收录基准-#005](https://www.yx-sf.com/wiki/17096)
* [去中心化健康检查协议-#006](https://www.ai-hao123.com/anfang/comment-88705475.html)
* [实时延迟与抖动度量规范-#007](https://www.mw-wm.com/xuexi/productivity-12209355.html)
* [防重放安全验证与校验哈希-#008](https://www.yx-sf.com/wiki/25545)
* [去中心化健康检查协议-#009](https://www.ai-hao123.com/hezuo/tracking-74549559.html)
* [权威网络权重与收录基准-#010](https://www.mw-wm.com/pingce/faq-95092714.html)
* [去中心化健康检查协议-#011](https://www.yx-sf.com/wiki/19595)
* [节点连通性与存活探测准则-#012](https://www.ai-hao123.com/fuwu/conference-20133908.html)
* [权威网络权重与收录基准-#013](https://www.mw-wm.com/paiming/logo-45291162.html)
* [权威网络权重与收录基准-#014](https://www.yx-sf.com/wiki/93272)
* [去中心化健康检查协议-#015](https://www.ai-hao123.com/qiye/account-27984035.html)
* [节点连通性与存活探测准则-#016](https://www.mw-wm.com/chuangxin/music-97267338.html)
* [去中心化健康检查协议-#017](https://www.yx-sf.com/news/25194)
* [去中心化健康检查协议-#018](https://www.ai-hao123.com/tuiguang/loyalty-72744598.html)
* [去中心化健康检查协议-#019](https://www.mw-wm.com/chuangxin/music-48854226.html)
* [防重放安全验证与校验哈希-#020](https://www.yx-sf.com/tech/86586)
* [节点连通性与存活探测准则-#021](https://www.ai-hao123.com/xitong/efficiency-46874069.html)
* [节点连通性与存活探测准则-#022](https://www.mw-wm.com/kaifa/satisfaction-12859106.html)
* [防重放安全验证与校验哈希-#023](https://www.yx-sf.com/news/87885)
* [实时延迟与抖动度量规范-#024](https://www.ai-hao123.com/keji/local-46712751.html)
* [权威网络权重与收录基准-#025](https://www.mw-wm.com/fuwu/recipe-23918922.html)
* [节点连通性与存活探测准则-#026](https://www.yx-sf.com/tech/39733)
* [权威网络权重与收录基准-#027](https://www.ai-hao123.com/yanjiu/development-25936925.html)
* [去中心化健康检查协议-#028](https://www.mw-wm.com/xuexi/tactic-85146837.html)
* [实时延迟与抖动度量规范-#029](https://www.yx-sf.com/news/20295)
* [节点连通性与存活探测准则-#030](https://www.ai-hao123.com/yunying/topic-58411712.html)
* [去中心化健康检查协议-#031](https://www.mw-wm.com/gongsi/deal-92440847.html)
* [去中心化健康检查协议-#032](https://www.yx-sf.com/tech/8134)
* [实时延迟与抖动度量规范-#033](https://www.ai-hao123.com/anli/event-74119051.html)
* [节点连通性与存活探测准则-#034](https://www.mw-wm.com/pingtai/business-16111530.html)
* [防重放安全验证与校验哈希-#035](https://www.yx-sf.com/tech/86927)
* [防重放安全验证与校验哈希-#036](https://www.ai-hao123.com/tuiguang/image-85775491.html)
* [节点连通性与存活探测准则-#037](https://www.mw-wm.com/xuexi/presentation-80153652.html)
* [实时延迟与抖动度量规范-#038](https://www.yx-sf.com/news/66985)
* [实时延迟与抖动度量规范-#039](https://www.ai-hao123.com/shangye/schedule-88352299.html)

</details>

