

最后，我们统计数据库中 {Chicken, Clothes, Milk} 的出现频率，并将其存储在 F3 中，前提是其支持度大于最小支持度。

F3: {{Chicken, Clothes, Milk}:3}。

请注意，由于 F3 中只有一个频繁项集，算法停止，因为我们至少需要两个频繁项集才能为 C4 生成候选项集。Apriori 算法只是过去 20 年中开发的大量关联规则挖掘算法的代表之一。更多算法请参见 [19]。

## STEP2: Association Rule Generation

正如我们前面提到的，Apriori 算法可以生成所有频繁项集以及所有置信的关联规则。有趣的是，与频繁项集生成相比，生成关联规则相当直接。事实上，我们从频繁项集中生成所有关联规则。对于每个频繁项集 f，我们使用其所有非空子集来生成关联规则。特别地，对于每个这样的子集 β，β ⊆ f，如果满足公式 5.6 中的置信度条件，我们输出规则 5.5。

(f − β) → β, (5.5)

confidence = f.count / (f − β).count ≥ minconf (5.6)

请注意 f.count 和 (f − β).count 分别是项集 f 和项集 (f − β) 的支持计数。根据公式 5.3，我们的规则支持度为 f.count / n，其中 n 是事务集 T 中的事务总数。显然，如果 f 是频繁的，那么根据向下封闭性，其所有非空子集也是频繁的。此外，公式 5.6 中置信度计算所需的所有支持计数，即 f.count 和 (f − β).count，在挖掘过程中已经记录了所有频繁项集的支持，例如使用 Apriori 算法。因此，关联规则生成不需要额外的数据库扫描。

## 5.3.2 Mining Class Association Rules

使用 Apriori 算法挖掘的关联规则是通用且灵活的。项可以作为规则条件的一部分，也可以作为规则结论的一部分。然而，在某些实际应用中，用户更感兴趣的是那些右手边具有固定目标项（或类标签）的规则。显然，这类规则对于基于规则的分类模型非常有用。

例如，银行通常维护一个客户数据库，其中包含个人客户的人口统计和财务信息（如性别、年龄、种族、地址、就业状态、薪水、房屋所有权、当前贷款信息等），以及目标特征，如是否偿还贷款或违约。使用关联规则挖掘技术，我们可以调查哪种类型的客户更可能偿还（良好信用风险）或违约（不良信用风险）——两者都是目标特征值，以便银行可以根据其个人人口统计和财务信息提前预测可能违约的客户，从而降低贷款违约率。换句话说，我们对一组特殊规则感兴趣，其结论仅为那些目标特征——这些规则称为类关联规则（CARs），其中我们要求只有目标特征值作为规则的结论，尽管条件可以是来自财务和人口统计信息的任意项或其组合。

设 T 是一个包含 n 个事务的事务数据集。T 中的每个事务都已用类 y 标记（y ∈ Y；Y 是所有类标签或目标特征/项的集合）。设 I 是 T 中所有项的集合，且 I ∩ Y = ∅。这里我们将标签集 Y 与标准项 I 不同对待，它们之间没有重叠。类关联规则（CAR）是以下形式的蕴含：

X → y, where X ⊆ I, and y ∈ Y. (5.7)

支持度和置信度的定义与标准关联规则相同。然而，类关联规则与标准关联规则在以下两点不同：

- 1. CAR 的结论只有一个项，而标准关联规则的结论可以有任意数量的项。
- 2. CAR 的结论 y 必须仅来自类标签集 Y，即 y ∈ Y。项 I 中的任何项都不能作为结论出现，且任何类标签都不能作为规则条件。相比之下，标准关联规则的条件或结论可以是任何项。

显然，挖掘 CAR 的主要目标是自动生成满足用户指定的最小支持度约束（minsup）和最小置信度（minconf）约束的完整 CAR 集合。

直观上，我们可以通过首先应用 Apriori 算法获取所有规则，然后进行后处理以仅选择那些类关联规则来挖掘给定的事务数据，因为 CAR 是以目标作为结论的关联规则的一种特殊类型。然而，由于组合爆炸，这是不高效的。现在，我们介绍一种专门为挖掘 CAR 设计的高效挖掘算法。

该算法可以单步挖掘 CAR。关键操作是找到支持度高于给定 minsup 的所有 ruleitems。ruleitem 是一个具有 condset 和类标签 y 的对，即 (condset, y)，其中 condset ⊆ I 是一个项集，且 y ∈ Y 是一个类标签。condset 的支持计数（称为 condsupCount）是 T 中包含该 condset 的事务数。ruleitem 的支持计数（称为 rulesupCount）是 T 中包含 condset 且与类 y 相关联的事务数。每个 ruleitem (condset, y) 表示一个规则：

condset → y,

其支持度为 (rulesupCount/n)，其中 n 是 T 中的事务总数，其置信度为 (rulesupCount/condsupCount)。

满足 minsup 的 ruleitems 称为频繁 ruleitems，而其余的称为非频繁 ruleitems。类似地，满足 minconf 的 ruleitems 称为置信 ruleitems，对应的规则是置信的。

规则生成算法称为 CAR-Apriori，给出在下面的伪代码中。CAR-Apriori 算法基于 Apriori 算法，通过多次遍历数据库生成所有频繁 ruleitems。特别是，它在第一次遍历中为每个仅在其 condset 中包含一个项的 1-ruleitem 计算支持计数（步骤 1）。所有 1-候选 ruleitems，即将 I 中的一个项与一个类标签配对，都存储在集合 C₁ 中。

C₁ = {({i}, y) | i ∈ I, and y ∈ Y} (5.8)

然后，步骤 2 选择频繁 1-ruleitems（并存储到 F₁ 中），其支持计数大于或等于给定的 minsup 值。从频繁 1-ruleitems，我们在步骤 3 中生成 1-condition CARs——仅有一个条件的规则。在随后的遍历中，假设为 k（k ≥ 2），它以在第 (k-1) 次遍历中找到的 (k-1) 个频繁 ruleitems 的种子集 Fₖ₋₁ 开始，并使用该种子集生成新的可能频繁 k-ruleitems，称为候选 k-ruleitems（步骤 5 中的 Cₖ）。在数据扫描期间（步骤 6-13），对于每个候选 k-ruleitem，condsupCount 和 rulesupCount 的实际支持计数都会更新。在数据扫描结束时，它确定 Cₖ 中的哪些候选 k-ruleitems 实际上是频繁的（步骤 14）。从频繁 k-ruleitems 中，步骤 15 生成 k-condition CARs，即具有 k 个条件的类关联规则。

## Algorithm CAR-Apriori(T)

- 1. C₁ ← init-pass(T); // the first pass over T
- 2. F₁ ← {f | f ∈ C₁, f.rulesupCount / f.condsupCount ≥ minsup}; // n is the no. of transactions in T;
- 3. CAR₁ ← {f | f ∈ F₁, f.rulesupCount / n ≥ minconf}; // n is the no. of transactions in T;
- 4. For (k = 2; Fₖ₋₁ ≠ ∅; k++) do
- 5.   Cₖ ← CARcandidate-gen(Fₖ₋₁);
- 6.   For each transaction t ∈ T do
- 7.     For each candidate c ∈ Cₖ do
- 8.       If c.condset is contained in t then // c is a subset of t
- 9.         c.condsupCount ++;
- 10.        if t.class = c.class then
- 11.          c.rulesupCount ++;
- 12.      EndFor
- 13.  EndFor
- 14.  Fₖ ← {c ∈ Cₖ | c.rulesupCount / n ≥ minsup}
- 15.  CARₖ ← {f | f ∈ Fₖ, f.rulesupCount / f.condsupCount ≥ minconf};
- 16. EndFor
- 17. Output CAR ← ∪ₖ CARₖ.

关于 ruleitem 生成的一个重要观察是，如果一个 ruleitem/规则的置信度为 100%，那么通过添加更多条件扩展该 ruleitem，即向其 condset 添加项，也会产生置信度为 100% 的规则，尽管其支持度可能会随着额外项的增加而下降。在某些应用中，我们可能认为这些具有更多条件的后续规则是冗余的，因为这些额外条件不会为分类提供更多信息。因此，我们不应在下一级的候选生成中扩展此类 ruleitems（从 k-1 到 k），这可以显著减少生成的规则数量。当然，如果需要，可以很容易地在 CAR-Apriori 算法中添加冗余处理过程以停止不必要的扩展过程。

最后，CARcandidate-gen() 函数与 Apriori 算法中的 candidate-gen() 函数非常相似，因此此处未包含。主要区别在于，在 CARcandidate-gen() 中，具有相同类标签的 ruleitems 通过连接它们的 condsets 来合并。

我们现在给出一个例子来说明 CAR 的有用性。表 5.2 显示了来自银行的一个样本贷款申请数据集，其具有四个属性，即 Age、Has_job、Own_house 和 Credit_rating。第一个属性 Age 有三个可能的值，即 young、middle 和 old。第二个属性 Has_Job 表示申请人是否有工作，二值：true（有工作）和 false（没有工作）。第三个属性 Own_house 显示申请人是否拥有房屋（同样有两个值，用 true 和 false 表示）。第四个属性 Credit_rating 有三个可能的值：fair、good 和 excellent。最后一列是类/目标属性，显示银行是否批准了每个贷款申请（用 Yes 表示）或未批准（用 No 表示）。

假设用户指定的最小支持度 minsup = 2/15 = 13.3% 和最小置信度 minconf = 70%，我们可以挖掘上述数据集以找到满足两个约束的以下规则：
Own_house = false, Has_job = true → Class = Yes [sup=3/15, conf=3/3]
Own_house = true → Class = Yes [sup=6/15, conf=6/6]
Own_house = false, Has_job = true → Class = Yes [sup=3/15, conf=3/3]

