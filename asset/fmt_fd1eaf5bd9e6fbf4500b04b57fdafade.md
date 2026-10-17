
如前所述，我关注出现在 `LOCRA` 中的词性动词词干。为了同时分析动词类型和词形（tokens），三个子语料库均使用 `WMatrix`（Rayson 2009）并结合成分似然性自动词性标记系统（`CLAWS7`）（Gardside and Smith 1997）进行了词干化和词性标注。由于目标包含每个动词形式的不同性标记（例如，基础形式为 `VV`，过去式为 `VVD`），因此应用了 `Perl` 程序处理 `CLAWS` 输出，以简化这些动词标记并将它们合并为单一 `VV` 标记（参见 Granger and Paquet 2009a）。

### 2.2 词汇提取方法

为了识别 `LOCRA` 中使用的学术动词，我探索并结合了两种此前作为各种列表基础的词汇提取方法：(1) 基于统计分析的特征法（Scott 1997）（例如：学术词汇列表、Paquet 2010；跨学科科学词汇、Drouin 2010）以及 (2) 主要基于相对频率分析的总频率分析（例如：通用列表、West 1957；大学词汇列表、Xue and Nation 1984；学术词汇列表、Coxhead 2000）。第 2.2.1 节和 2.2.2 节描述了这两种方法以及产生的不同类型的结果。

#### 2.2.1 特征分析

为了识别出现在 `LOCRA` 中的特征动词，我复制了 Granger 和 Paquet 在通用学术动词研究（2009a）中使用的方法。然而，虽然他们的研究只关注核心的 `EAP` 特征动词，但我使用了相同的方法来分析出现在 `LOCRA` 中所有的特征动词。

特征分析包括提取所有“在给定文本中与参考语料库相比出现频率异常”的单词（Scott 2001: 236）。换句话说，该方法的目标是通过识别在该特定语料库中频率显著高于参考语料库的单词，生成一个给定语料库的典型单词列表。在本文中，该方法用于识别可以被视为典型学术英语的动词。通过一个由虚构写作（fiction writing）构成的“强对比参考语料库”（Tribble 2001: 396），我将三个小说子语料库与婴儿英国国家语料库（`Baby British National Corpus`）中 10 亿词的小说子语料库对比，理由是典型的 `EAP` 动词在该参考语料库中的出现频率不会如此高（Granger and Paquet 2009a）。

具体来说，三个子语料库中的每一个都被提交给 `WordSmith Tools 5` 列表（Scott 2008）。该程序为每个子语料库生成了一个特征列表。这三个列表经过人工编辑，以创建特征动词列表。生成的动词列表进行了清理，删除了被 `WMatrix` 错误标记为动词的词汇。

在观察特征分析产生的动词类型时（见表 3），发现该方法提取了大量的学术动词（可能是跨学科的），以及较少的特定学科动词。表 3. 学术动词列表

| N | BUS | LING | MED |
| :--- | :--- | :--- | :--- |
| 1 | PROVIDE | USE | |
| 2 | USE | PROVIDE | |
| 3 | SUGGEST | OCCUR |
| 4 | EXAMINE | |
| 5 | | | |
| 6 | | | |
| 7 | | | |
| 8 | | | |
| 9 | | | |
| 10 | | | |
| ... | ... | ... | ... |
| 200 | COOPER | RELY | |
| 201 | OUTSOURCE | REFLECT | |
| 202 | IMPLEMENT | | |
| 203 | RECORD | | |
| 204 | CHOOSE | | |
| 205 | FORM | | |
| 206 | REGARD | | |
| 207 | JUDGE | | |
| 208 | EXPORT | | |
| 209 | STRUCTURE | | |
| 210 | FAVOR | | |
| 211 | INDUCE | | |

#### 2.2.2 频率分析

相对频率的分析允许识别语料库中最频繁使用的动词。为了识别学术动词，我对三个子语料库使用了 `WordSmith Tools 5` 程序（Scott 2008）。该程序为每个子语料库生成了频率动词列表。生成的动词列表经过人工编辑，以与非学术动词区分开来。这种方法提取了大量的可能是跨学科的动词以及较少的特定学科动词。

表 4. `LOCRA` 中的高频动词

| | BUS | LING | MED | FICTION |
| :--- | :--- | :--- | :--- | :--- |
| 类型 | 300 | 333 | 269 | 366 |
| 百比 | 11.6% | 10.3% | 11.3% | 8.3% |
| 类型总数 | 2,578 | 3,233 | 2,366 | 4,413 |
| 高频词形数量 | 79,861 | 75,815 | 62,456 | 106,383 |
| 百比 | 80% | 80% | 80% | 80% |
| 词形总数 | 100,089 | 95,018 | 78,973 | 132,979 |

在本研究中，我选择了总数的 80% 作为截止点来识别高频动词。这意味着占据 80% 词形的动词被认为是高频的。将从 `LOCRA` 获得的结果与参考语料库进行对比时发现，为了达到 80% 的覆盖率，`LOCRA` 需要的动词类型比例比小说高（`LOCRA`：在 10.3% 到 11.6% 之间）。换句话说，这意味着小说使用了比 `LOCRA` 中识别出的更频繁的高频动词类型，因为达到 80% 时需要的词类型比例较小。

对 `LOCRA` 的三个子语料库进行对比显示，语言学达到 80% 覆盖率时需要的动词比例小于其他两个学科，这表明语言使用了比商学和医学识别出的更频繁的高频动词。这种差异在

244 Natassia Schutz

频率表明，语言学可能会使用一些在另外两个子语料库中未使用的高频动词。

`LOCRA` 三个子语料库频率列表中出现的大量动词似乎是通过关键性分析（keyness analysis）识别出的动词（例如 suggest, develop 或 compare）（见表5）。在这些动词旁边，还有许多未被关键性法识别的其他高频动词，如 say, make, see, take, find, give 和 seem（见表5中加粗的动词）。由于动词在小说参考语料库中出现非常频繁，显然它们被关键性法忽略了；由于关键性法的作用是提取在给定语料库中比参考语料库频率显著更高的单词，因此，在两个语料库中都是高频的词没有被纳入考虑。

表 5. `LOCRA` 和小说中的前20 个动词（`RF` = 相对频率/1000 词）

| N | 动词 | RF | 动词 | RF | 动词 | RF | 小说动词 | RF |
|---|---|---|---|---|---|---|---|---|
| 1 | USE | 2.28 | | 2.35 | | 2.96 | SAY | 6.72 |
| 2 | SUGGEST | 1.48 | SEE | 1.82 | SHOW | 2.24 | | 3.62 |
| 3 | FIND | 1.47 | SHOW | 1.52 | COMPARE | 1.40 | GO | 3.39 |
| 4 | PROVIDE | 1.35 | MAKE | 1.29 | ASSOCIATE | 1.05 | GET | 3.13 |
| 5 | MAKE | 1.28 | TAKE | 1.09 | SUGGEST | 0.98 | SEE | 2.96 |
| 6 | SHOW | 1.02 | FIND | 0.96 | PERFORM | 0.85 | THINK | 2.84 |
| 7 | SEE | 0.92 | SUGGEST | 0.94 | INCREASE | 0.85 | LOOK | 2.72 |
| 8 | DEVELOP | 0.89 | GIVE | 0.91 | RECEIVE | 0.80 | COME | 2.67 |
| 9 | EXAMINE | 0.87 | PROVIDE | 0.90 | REPORT | 0.79 | MAY | 2.16 |
| 10 | RELATE | 0.80 | OCCUR | 0.88 | INDICATE | 0.78 | TAKE | 2.15 |
| 11 | BASE | 0.85 | APPEAR | | DETERMINE | 0.77 | WANT | 1.83 |
| 12 | INCLUDE | 0.84 | SAY | 0.71 | FIND | | TELL | 1.70 |
| 13 | TAKE | 0.83 | FOLLOW | 0.70 | DESCRIBE | 0.73 | ASK | 1.30 |
| 14 | INDICATE | 0.78 | CONSIDER | 0.67 | OBSERVE | 0.72 | FEEL | 1.26 |
| 15 | INFLUENCE | 0.75 | INVOLVE | 0.64 | EXPRESS | 0.69 | FIND | 1.26 |

脱离语境，这些动词与学术英语（`EAP`）并不十分相关。为了评估 find 和 make 等动词是否具有学术用途，从而对 `EAP` 学习者具有意义，利用 `SketchEngine` 的 `WordSketch` 选项对 find 和 make 的短语用法进行了一项初步研究（Kilgarriff et al. 2004）。该程序能够提取“自动基于语料库的单词语法和搭配行为的摘要”（同上）。换句话说，该程序使用统计学 logDice 指标，

## 学术英语的特定性有多强？

自动提取特定节点的搭配词，并根据语法功能进行排序。结果显示 find 和 make 具有 `EAP` 的短语模式，证明了它们因此应该被纳入 `EAP` 动词列表中。表 6 提供了小说中 find 和 make 的搭配汇总；find + correlation（示例 1 到 3）和 make + contribution（示例 4 到 6）在语境中的也表明，这些高频动词在 `LOCRA` 的三个学科中可能具有相同的模式和含义。

表 6. 小说和 `LOCRA` 中 find 和 make 的搭配

| 搭配词 | FIND | MAKE |
|---|---|---|
| | 小说 LOCRA | 小说 LOCRA |
| 宾语 | corpse, job, pot, place, something, money, seat, reason, work, woman | correlation, effect, difference, evidence, result | love, noise, money, tea, gesture, note, call, use, judgment, observation |
| 主语 | somebody, people, man, research(er), study | someone, woman, man, study |

- (1) `LOCRA BUS` ... 发现跨文化培训与表现之间存在正相关性。
- (2) `LOCRA LING` 也发现了负相关性。
- (3) `LOCRA MED` 我们发现。
- (4) `LOCRA BUS` 这做出了重要的贡献。
- (5) `LOCRA LING` 我们发现。
- (6) `LOCRA MED` 这。

## 3. 结果

### 3.1 合并关键性和频率动词

本研究使用的两种方法——关键性法和频率分析——存在差异。关键性法基于统计，提取在给定语料库中比参考语料库频率显著更高的单词；而频率分析则识别语料库中频率最高的单词。

## 学术英语的特定性有多强？

表 7. 合并关键列表和频率列表

| BUS | LING | MED |
|---|---|---|
| 关键动词 | 高频动词 | 关键动词 | 高频动词 | 关键动词 | 高频动词 |
| 289 | 300 | 277 | 333 | 240 | 269 |
| 重叠: 203 | 重叠: 209 | 重叠: 185 |
| 最终 BUS | 最终 LING | 最终 MED |
|---|---|---|
| 学术动词列表 | 学术列表 | 学术列表 |
| 386 | 401 | 324 |

表 8. `LOCRA` 中的学术动词

| | | LING | MED |
|---|---|---|---|
| 词类数 LOCRA 动词类型 | 386 | 401 | 324 |
| | | 14.9% | 12.4% | 13.7% |
| 动词类型总数 | 2,578 | 3,233 | 2,366 |
| 词元数 LOCRA 动词标记 | 84,553 | 79,418 | 65,550 |
| | | 84.4% | 83.6% | 83% |
| 动词标记总数 | 100,089 | 95,018 | 78,973 |

## 3.2 `LOCRA` 学术动词的分布

为了更好地理解 `EGAP` 和 `ESAP` 动词在 `LOCRA` 中代表什么，必须对本文识别的所有学术动词的分布进行两种不同的分析方法。首先，为了区分潜在的 `EGAP` 动词（即三个学科共有且可能在学科间具有相似用法的动词）和 `ESAP` 动词（即学科特定的动词），需要对学术动词列表进行比较，以识别哪些词出现在三个学科中，哪些出现在两个学科，哪些仅出现在一个学科中（3.2.1 节）。只有在进行了这种一般的分布分析之后，才能衡量 `EGAP` 和 `ESAP` 动词在每个学科中的权重（即占动词类型和标记总数的比例）（3.2.2 节）。

### 3.2.1 跨学科分布

在将三个学术动词列表合并后，`LOCRA` 中总共有 609 个学术动词。总体分布分析结果显示，这些学术动词中，29% 被三个学科共同使用，24.3% 被两个学科共有，而 46.6% 是学科特定的（见表 9）。

表 9. `LOCRA` 学术动词的通用的分布

| 学术动词 | 示例 | 动词数量 | 比例 |
| --- | --- | --- | --- |
| 3 个学科共有 | BUS 和 LING | compare, focus, show | 177 | 29% |
| | | enable, tend | 107 | |
| 2 个学科共有 | BUS 和 MED 和 MED | exceed, induce, persist | 23 | 24.3% |
| | | activate, encode, record | 18 | |
| 学科特定 | BUS LING MED | cost, finance, trust | 79 | |
| | | convey, inflict, omit | 99 | 46.6% |
| | | amplify, detect, inject | 106 | |
| 总计 | | 609 | 100% |

表 9 还显示，语言学和商务是共享学术动词最多的学科。除了三个学科共有的 177 个动词外，语言学和商务还共享最少的 107 个学术动词。相比之下，医学学科最少（与商务共有 23 个，与语言学共有 18 个），且拥有最多的学科特定动词。

如果我们放大观察，在 177 个动词中，有 141 个被关键性分析识别出来（见表 10 中普通格式的动词），36 个得益于相对频率分析（见表 10 中加粗的动词）。快速查看这 36 个高频动词发现，它们大部分需要在语文中呈现，因为它们与 `EGAP` 的相关性并不显而易见（例如 carry, find, gain, make 或 take）。这一点将在 4 节进一步阐述。尽管如此，可能的 `EGAP` 动词列表说明了关键性分析与相对频率分析是如何完美互补的，因为相对频率分析捕捉到了许多具有典型 `EGAP` 用法但未被关键性分析捕捉到的高频动词（例如 to carry out a study, to find a correlation, to gain insights 或 to take into account）。

学术英语有多特殊性？

表 10. 潜在的 `EGAP` 动词列表（关键性 + 高频动词）

ACCOUNT, ACHIEVE, ACQUIRE, ACT, ADD, ADDRESS, AFFECT,

ALLOW, ANALYZE, APPEAR, APPLY, ASK, ASSESS, ASSIGN,

ASSOCIATE, ASSUME, ATTRIBUTE, BASE, BECOME, BEGIN,

BELIEVE, CALCULATE, CARRY, CATEGORIZE, CAUSE, CHANGE,

CHARACTERIZE, CHOOSE, CLASSIFY, COLLECT, COMBINE,

COMPARE, COMPLETE, COMPRISE, CONFIRM, CONDUCT,

CONSIDER, CONSIST, CONSTITUTE, CONSTRUCT, CONTAIN,

CONTINUE, CONTRIBUTE, CONTROL, CORRELATE,

CORRESPOND, DEFINE, DEMONSTRATE, DENOTE,

DEPEND, DEPICT, DERIVE, DESCRIBE, DESIGN, DIVIDE,

DETERMINE, DEVELOP, DIFFER, DIFFERENTATE, DISTINGUISH,

DOCUMENT, ELIMINATE, ENHANCE, ENTER, ESTABLISH,

ESTIMATE, EVALUATE, EXCLUDE, EXHIBIT, EXPECT,

EXPERIENCE, PLAIN, EXPRESS, EXTEND,

FACILITATE, FAIL, FAVOR, FIND, FOCUS, FOLLOW, FORM, GAIN,

GENERATE, GIVE, HYPOTHESIZE, IDENTIFY, IMPLEMENT,

IMPROVE, INCLUDE, INCORPORATE, INCREASE, INDICATE,

INFLUENCE, INITIATE, INTERACT, INTERPRET, INVESTIGATE,

INVOLVE, KNOW, LACK, LEAD, LIMIT, LINK, LIVE, LOCATE,
