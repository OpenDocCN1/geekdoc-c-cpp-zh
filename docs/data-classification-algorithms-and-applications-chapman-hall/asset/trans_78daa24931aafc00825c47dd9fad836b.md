

5; 在步骤 8 将学习到的 *Rule* 插入到 *RuleList* 的末尾；在步骤 9 从 (*Pos*, *Neg*) 中移除被 *Rule* 覆盖的示例。注意，对于每个类别 *c* 的内部规则学习，步骤 4 和步骤 6 分别给出了两个停止条件——当 *Pos* 变为空或函数 Learn-One-Rule(*Pos*, *Neg*, *c*) 无法从剩余的训练数据中学习到新规则时，我们就停止为类别 *c* 的内部规则学习过程的 **while-loop**。

算法的其他部分与 CN2 算法非常相似。Learn-One-Rule() 函数将在第 5.2.2 节后面描述。

最后，应用 *RuleList* 进行分类的方式与 CN2 算法类似。唯一的区别是每个类别内所有规则的顺序不再重要，因为它们共享相同的类别标签，这将导致相同的分类结果。由于规则现在按类别排序，给定一个测试示例，我们将首先尝试最不频繁类别的规则，直到找到一条可以覆盖该测试示例的单一规则来进行分类；否则，我们必须应用 *default-class*。

## 5.2.2  Learn One Rule in Rule Learning

在上面描述的两个算法中，我们尚未详细阐述它们使用的两个重要函数，其中第一个算法使用 *Find_Best_Complex()*，第二个算法使用 learn-one-rule()。在本节中，我们解释了这两个从全部或部分训练数据中学习规则的函数的总体思想。

首先，规则从一个空的条件集开始。在第一次迭代中，只会添加一个条件。为了找到一个最佳条件可供添加，所有可能的条件都会被探索，这些条件构成了一组候选规则。条件是一个属性-值对的形式为 *Aᵢ op v*，其中 *Aᵢ* 是一个属性，*v* 是 *Aᵢ* 的一个值。特别地，对于离散属性 *v*，假设 *op* 为“=”，则条件将变为 *Aᵢ = v*。另一方面，对于连续属性，*op* ∈ {>, ≤} 且条件变为 *Aᵢ > v* 或 *Aᵢ ≤ v*。该函数随后评估所有可能的候选，以从中检测出 *best* 的一个（所有剩余候选都被丢弃）。注意 *best* 的候选条件应该是能够更好地区分不同类别的一个，例如通过熵函数，该函数已成功用于决策树学习 [4]。

接下来，在添加了第一个最佳条件后，它会以相同的方式进一步探索添加第二个条件，依此类推，直到满足某些停止条件为止。请注意，我们在这里省略了规则类别，因为它意味着被条件覆盖的训练数据的多数类别。换句话说，这意味着当我们应用规则时，我们预测的类别标签应该在大多数情况下是正确的。

显然，这是一个启发式和贪婪算法，因为在添加条件后，它不会通过回溯来更改或移除该条件 [15]。理想情况下，我们希望探索所有可能的 *属性和值的组合*。然而，这在实践中不可行，因为随着规则中条件的增加，可能性的数量呈指数增长。因此，在实践中，使用上述贪婪算法来高效地进行规则归纳。

尽管如此，与其只保留最佳条件集，我们可以通过在每次迭代中保留 *k* 个最佳条件集（*k* > 1）来稍微改进该函数。这称为 **beam search**（*k* beams），它确保探索更大的空间（更多属性和值组合），这可能比仅保留最佳条件集的标准贪婪算法产生更好的结果。

下面，我们提出了两个函数的具体实现，即 *Find_Best_Complex()* 和 learn-one-rule()，其中 *Find_Best_Complex()* 用于 CN2 算法，而 learn-one-rule() 用于 RIPPER 算法及其变体。

### Find_Best_Complex(D)

函数 Find_Best_Complex(D) 使用 beam search，其波束数为 k。该函数的细节如下所示。

# Function Find_Best_Complex(D)

+   1. BestCond ← ∅;  // rule with no condition.
+   2. candidateCondSet ← {BestCond};
+   3. attributeValuePairs ← the set of all attribute-value pairs in D of the form (Ai op v), where Ai is an attribute and v is a value or an interval;
+   4. While candidateCondSet ≠ ∅ do
+   5.   newCandidateCondSet ← ∅;
+   6.   For each candidate cond in candidateCondSet do
+   7.     For each attribute-value pair a in attributeValuePairs do
+   8.       newCond ← cond ∪ {a};
+   9.       newCandidateCondSet ← newCandidateCondSet ∪ {newCond};
+   10.    EndFor
+   11.  EndFor
+   12.  remove duplicates and inconsistencies, e.g., {Ai = v1, Ai = v2};
+   13.  For each candidate newCond in newCandidateCondSet do
+   14.    If evaluation(newCond, D) > evaluation(BestCond, D) then
+   15.      BestCond ← newCond
+   16.    EndIf
+   17.  EndFor
+   18.  candidateCondSet ← the k best members of newCandidateCondSet according to the results of the evaluation function;
+   19. EndWhile
+   20. If evaluation(BestCond, D) − evaluation(∅, D) > threshold then
+   21.   Output the rule: “BestCond → c” where is c the majority class of the data covered by BestCond
+   22. Else Output NULL
+   23. EndIf

在此函数中，集合 BestCond 存储要返回的规则的条件。类别在此省略，因为它指的是被 BestCond 覆盖的训练数据的多数类别。集合 candidateCondSet 存储当前最佳条件集（即前沿波束），其大小小于或等于 k。每个条件集包含一组由“and”（合取）连接的条件。集合 newCandidateCondSet 存储在将每个属性-值对（可能的条件）添加到 candidateCondSet 中的每个候选后得到的所有新候选条件集（步骤 5-11）。步骤 13-17 更新 BestCond。请注意，使用了一个 evaluation 函数来评估每个新候选条件集是否比现有最佳条件集 BestCond 更好（步骤 14）。如果找到了更好的新候选条件集，则它会替换当前的 BestCond（步骤 15）。步骤 18 更新 candidateCondSet，它选择 k 个最佳条件集（新波束）。

一旦找到最终的 BestCond，就会评估它是否显著优于没有任何条件（∅）的情况，使用阈值（步骤 20）。如果是，则使用 BestCond 和被 BestCond 覆盖的数据中最频繁（或多数）类别形成规则（步骤 21）。如果不是，则返回 NULL，表示未找到显著规则。

请注意，下面所示的 evaluation() 函数采用熵函数，与决策树学习中相同，用于评估 *BestCond* 的好坏。

```
**Function evaluation**(*BestCond*, *D*)

1.  *D′* ← the subset of training examples in *D* covered by *BestCond*
2.  *entropy*(*D′*) = −∑<sub>j=1</sub><sup>|C|</sup> *Pr*(*c<sub>j</sub>*) × log<sub>2</sub>*Pr*(*c<sub>j</sub>*)
3.  **Output** −*entropy*(*D′*)   // since entropy measures impurity.
```

具体来说，在 evaluation() 函数的第一步中，它获得一个示例集 *D′*，该集合由 *D* 中被 *BestCond* 覆盖的训练示例子集组成。在第二步中，它根据概率分布计算熵函数 *entropy*(*D′*) —— *Pr*(*c<sub>j</sub>*) 是数据集中类 *c<sub>j</sub>* 的概率 *D′*，定义为 *D′* 中类 *c<sub>j</sub>* 的示例数除以 *D′* 中的总示例数。在熵计算中，0 × log 0 = 0。熵的单位是比特。我们现在提供一些示例以帮助理解熵度量。

假设数据集 *D′* 只有两个类别，即正类（*c<sub>1</sub>* = *P*）和负类（*c<sub>2</sub>* = *N*）。基于以下三种不同的概率分布组合，我们可以计算它们的熵值如下：

-   1. 数据集 *D′* 有 50% 的正例（即 *Pr*(*P*) = 0.5）和 50% 的负例（即 *Pr*(*N*) = 0.5）。则，*entropy*(*D′*) = −0.5 × log₂0.5 − 0.5 × log₂0.5 = 1。
-   
-   2. 数据集 *D′* 有 20% 的正例（即 *Pr*(*P*) = 0.2）和 80% 的负例（即 *Pr*(*N*) = 0.8）。则，*entropy*(*D′*) = −0.2 × log₂0.2 − 0.8 × log₂0.8 = 0.722。
-   
-   3. 数据集 *D′* 有 100% 的正例（即 *Pr*(*P*) = 1）和没有负例（即 *Pr*(*N*) = 0）。则，*entropy*(*D′*) = −1 × log₂1 − 0 × log₂0 = 0。

从上面显示的三个场景中，我们可以观察到，当数据类别变得越来越纯（例如，所有或大多数示例都属于一个单独的类别）时，熵值变得越来越小。事实上，可以证明，对于这种二元情况（只有正类和负类），当 *Pr*(*P*) = 0.5 且 *Pr*(*N*) = 0.5 时，熵具有最大值，即 1 比特。当 *D′* 中的所有数据都属于一个类别时，熵具有最小值，即 0 比特。很明显，熵根据数据类别分布衡量不纯度。显然，我们希望规则具有较低的熵甚至为 0 比特，因为这意味着规则将导致一个主要类别，我们因此更有信心将规则应用于分类。

除了熵函数之外，还可以应用其他评估函数。请注意，当 *BestCond* = 0 时，它覆盖 *D* 中的每个示例，即 *D* = *D′*。

## Learn-One-Rule

在 Learn-One-Rule() 函数中，首先生成一条规则，然后对其进行剪枝过程。此方法首先将正负训练数据 *Pos* 和 *Neg* 分成生长集和剪枝集。生长集 *GrowPos* 和 *GrowNeg* 用于生成一条规则，称为 *BestRule*。剪枝集 *PrunePos* 和 *PruneNeg* 用于剪枝规则，因为 *BestRule* 可能因条件过多而过拟合训练数据，这可能导致对未见测试数据的预测性能较差。请注意，*PrunePos* 和 *PruneNeg* 实际上是验证集，用于访问规则的泛化能力。如果一条规则在验证集中的错误率为 50%，则它泛化得不好，因此该函数不会输出它。

