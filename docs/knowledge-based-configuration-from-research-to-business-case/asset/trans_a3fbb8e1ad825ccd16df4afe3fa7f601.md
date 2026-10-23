

一个*配置*（参见 Hotz et al., 2014⁶）对于我们的示例配置任务为 \(I = \{4\text{-wheel} = \text{no},\ \text{fuel} = 41,\ \text{type} = \text{city},\ \text{skibag} = \text{no},\ \text{pdc} = \text{yes}\}\)。

## 12.3 确定冗余约束

现在让我们考虑原始约束集 \(C_{KB}\) 的一个简单改编，我们用 \(C'_{KB}\) 表示。\(C'_{KB}\) 包含一个额外的约束 \(c_a\)，该约束由知识工程师添加。

\[
C'_{KB}=\{\
\begin{aligned}
 c_a &: \text{skibag} \ne \text{no} \to \text{type}=\text{limo} \lor\\
    &\quad \text{type}=\text{combi} \lor\\
    &\quad \text{type}=\text{xdrive},\\
 c_1 &: 4\text{-wheel}=\text{yes} \to \text{type}=\text{xdrive},\\
 c_2 &: \text{skibag}=\text{yes} \to \text{type}\ne\text{city},\\
 c_3 &: \text{fuel}=41 \to \text{type}=\text{city},\\
 c_4 &: \text{fuel}=61 \to \text{type}\ne\text{xdrive},\\
 c_5 &: \text{type}=\text{city} \to \text{fuel}\ne101\}
\end{aligned}
\]

显然 \(c_a\) 是冗余的，因为它并没有进一步限制由 \(C_{KB}=\{c_1,c_2,c_3,c_4,c_5\}\) 定义的解空间。为了在更正式的层面上讨论约束*冗余*，我们引入以下定义。

**定义（冗余约束）。** 设 \(c_a\) 为配置知识库 \(C_{KB}\) 的一个约束。\(c_a\) 被称为冗余当且仅当 \(C_{KB}-\{c_a\}\models c_a\)。如果此条件不满足，则称 \(c_a\) 为*非冗余*。冗余也可以通过检查 \(C_{KB}-\{c_a\}\cup\overline{C}_{KB}\) 的一致性来分析。如果一致性成立，则 \(c_a\) 为非冗余。

该定义基于 Dechter 和 Dechter（1987）的定义。对 \(C_{KB}\) 的每个约束进行迭代，执行非冗余性检查 \(C_{KB}-\{c_a\}\cup\overline{C}_{KB}\) 并从 \(C_{KB}\) 中删除冗余约束，会得到一组非冗余约束（*最小核心*）。如果非冗余性检查失败（找不到解），则约束 \(c_a\) 是冗余的，可以从 \(C_{KB}\) 中删除。否则，\(c_a\) 是非冗余的。

**定义（最小核心）。** 设 \(C_{KB}\) 为配置知识库。\(C_{KB}\) 被称为最小核心当且仅当 \(\forall c_i\in C_{KB}: C_{KB}-\{c_i\}\cup\overline{C}_{KB}\) 是相容的。显然，\(C_{KB}\cup\overline{C}_{KB}\models\bot\)。

以下算法（SEQUENTIAL - 算法 12.1）的原理通常用于确定此类冗余（参见，例如，Boulkhad 和 Roussel, 2000；Chmeiss et al., 2008；Fourdrinoy et al., 2007；Grimm 和 Wissmann, 2011；Piette, 2008）。

### 算法 12.1 SEQUENTIAL(C_KB): Δ

```
{C_KB: configuration knowledge base}
{\overline{C_KB}: the complement of C_KB}
{Δ: set of redundant constraints}
{C_KBt: copy of C_KB used for redundancy elimination}
C_KBt ← C_KB;
for all c_i in C_KBt do
  if isInconsistent((C_KBt − {c_i}) ∪ {¬c_i}) then
    C_KBt ← C_KBt − {c_i};
  end if
end for
Δ ← C_KB − C_KBt;
return Δ;
```

SEQUENTIAL 的方法很直接（参见，例如，Boufkhad 和 Roussel, 2000；Chmeiss et al., 2008；Fourdrinoy et al., 2007；Grimm 和 Wissmann, 2011；Piette, 2008）：每个单独的约束 c_i 都通过检查 C_KB − c_i 是否仍与 \overline{C_KB} 不一致来评估其冗余性。与检查 C_KB − {c_i} ∪ \overline{C_KB} 的不一致性相比，SEQUENTIAL 系统地减少了在 \overline{C_KB} 中需要检查的约束数量。给定配置知识库 C_KB 及其补集 \overline{C_KB}，C_KB − {c_i} ∪ \overline{C_KB} 的（不）一致性检查可以简化为 C_KB' − {c_i} ∪ \overline{C_KB'} 的不一致性检查，其中 \overline{C_KB'} = {¬c_i}。如果我们假设 C_KB = {c1 ∧ c2 ∧ ... ∧ c_m ∧ c_{m+1} ∧ ... ∧ c_n}，\overline{C_KB} = {¬c1 ∨ ¬c2 ∨ ... ∨ ¬c_m ∨ ¬c_{m+1} ∨ ... ∨ ¬c_n}，且 γ = {c_{m+1} ∧ ... ∧ c_n}，则 C_KB − γ ∪ \overline{C_KB} 的一致性检查可以简化为 {c1 ∧ c2 ∧ ... ∧ c_m} ∪ {¬c_{m+1} ∨ ... ∨ ¬c_n}。在 SEQUENTIAL 算法中相应地利用了这一性质。

如果 (C_KB − {c_i}) ∪ {¬c_i} 不一致，则 c_i 可以被视为冗余。如果 C_KB − {c_i} 与 ¬c_i 相容，则 c_i 是非冗余约束，因为其删除会与 \overline{C_KB} 产生一致性。将算法 SEQUENTIAL 应用于我们的示例 C'_KB 得到 Δ = {c_a}，因为 (C_KB − {c_a}) ∪ {¬c_a} 不一致，并且没有其他约束 c_i 可以从 C_KB 中删除，使得 (C_KB − {c_a, c_i}) ∪ {¬c_i} 仍然不一致。表 12.1 显示了 SEQUENTIAL 冗余检测算法在我们的（冗余）示例配置知识库 C'_KB = {c_a, c1, c2, c3, c4, c5} 基础上的执行轨迹。

### 表 12.1 SEQUENTIAL 的示例执行轨迹。冗余约束集为 Δ = {c_a}。

| SEQUENTIAL Iteration | C_KBt | c_i |
|---|---|---|
| 1 | {c_a, c1, c2, c3, c4, c5} | c_a |
| 2 | {c1, c2, c3, c4, c5} | c1 |
| 3 | {c1, c2, c3, c4, c5} | c2 |
| 4 | {c1, c2, c3, c4, c5} | c3 |
| 5 | {c1, c2, c3, c4, c5} | c4 |
| 6 | {c1, c2, c3, c4, c5} | c5 |

## 第 12 章 配置知识中的冗余检测

检查给定约束是否可以从约束集的剩余部分推导出来的问题在一般情况下已被证明是 Co-NP-完全的（Piette, 2008）。存在替代算法，在 $C_{KB}$ 中存在大量冗余约束的情况下，其运行时间性能优于 Sequential。大量冗余约束通常出现在分布式知识工程场景中，其中大量用户指定规则，这些规则随后需要聚合为一个一致的约束集（参见，例如，Chklovski 和 Gil, 2005）。

在下一节中我们介绍 CoreDiag 算法，它是在存在大量冗余约束的情况下对 Sequential 的有价值的替代方案。在介绍 CoreDiag 之后，我们将基于金融服务知识库（第 12.5 节）分析两种算法（Sequential 和 CoreDiag）的性能。

## 12.4 CoreDiag

CoreDiag 算法（连同 CoreD；Felfernig et al., 2011）基于分而治之的原则：每当集合 $S$，它是 $C_{KB}$ 的子集，与 $\overline{C}_{KB}$ 不一致时，它是或包含一个最小核心（即保留 $C_{KB}$ 语义的约束集）。在我们的实现中，CoreD 负责确定此类最小核心，CoreDiag 返回最小核心的补集，即 $C_{KB}$ 中最大冗余约束集。CoreD 基于 QuickXPlain 原则（参见 Felfernig et al., 2014）；⁷ 因此最小核心（保留 $C_{KB}$ 语义的最小约束集）可以解释为最小冲突（即与 $C_{KB}$ 不一致的最小约束集）。

CoreD 允许确定首选的最小核心，因为该算法基于 $C_{KB}$ 中约束的严格字典序假设。在非正式层面上，首选最小核心可以表述如下：如果我们有选择最小核心的不同选项，我们会选择具有最多被认可约束的那个。有关约束严格字典序作用的更多细节，请参阅 Junker（2004）和 Felfernig et al.（2012）的工作。

CoreDiag 算法（参见算法 12.2）从 $C_{KB}$ 生成 $C'_{KB}$。然后它激活 CoreD（参见算法 12.3），CoreD 基于分而治之策略确定最小核心，该策略将 $C$ 中的约束分为两个子集（$C_1$ 和 $C_2$），目标是弄清其中一个子集是否已包含最小核心。如果 $C_2$ 包含最小核心，则 $C_1$ 不再进一步考虑。如果 $C$ 仅包含一个元素（$c_\alpha$）且 $B$ 仍然一致，则 $c_\alpha$ 是最小核心的一部分。

表 12.2 显示了 CoreDiag 冗余检测算法在我们的（冗余）示例配置知识库 $C'_{KB} = \{c_a, c_1, c_2, c_3, c_4, c_5\}$ 基础上的执行轨迹。在此上下文中，递归函数 CoreD 负责确定最小核心（如果存在）。CoreD 的基本方法是为 $C \cup B$ 识别一个最小冲突集 $CS$，使得 $CS \cup B$ 不一致。所识别的冲突集代表最小核心，而 $C - CS$ 为冗余约束集。

