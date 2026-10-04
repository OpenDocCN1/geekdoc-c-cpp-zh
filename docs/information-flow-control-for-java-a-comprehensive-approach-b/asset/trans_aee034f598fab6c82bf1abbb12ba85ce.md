

## CHAPTER 信息流控制

相反，可以在计算摘要去分类节点的 security levels 时利用专门的摘要边算法。结果可见于算法 8 和 9，它们将向后 IFC 传播纳入了 Reps 等人提出的算法 [RHSR94] 中，如第 35 页的算法 2 所示。

作为示例，考虑 pathEdge 中的图 4.1。这里，算法 8 首先将节点 15 作为 (15, 15, false) 添加到 pathEdge。注意该元组的第三个元素为 false，它是一个去分类节点。当该元组从 workList 中移除时，15 的所有前驱都会被处理，特别是节点 14。对于该节点，extendPathEdge 在 pathEdge 中找不到之前的元组，因此没有 $\gamma$、resp. v 的元素。由于节点 15 在 $d$ 中，$f' = \Gamma(R(15))$ 且 $R(f') = f' = false$，由此得到 pathedge 元组 (14, 14, confidential)。对于其前驱 13，我们将得到 pathedge 元组 (13, 13, confidential)，并且没有其他路径通向 13。由于 13 是一个 formal-in 节点，addSummaries 将添加一个摘要去分类节点 $d$，其中 $R(d) = confidential$ 且 $P(d) = \perp$，依据相应的属性类 4、6、8 和 10，正如我们在上一节中定义这些节点一样。

**定理 4.10.** 由算法 8 和 9 确定的带摘要去分类节点的 IFC 是 sound 且 precise 的。

**证明.** 我们证明算法 8 和 9 的结果是为所有可达的 interprocedural 路径生成的约束的超集。这保证了 soundness。为了证明这一点，我们表明通过选择所有摘要去分类节点 $d$ 的 $P(d) = \perp$，附加的约束是平凡满足的，从而不改变 fixedpoint。由于这些是 [HRB90, RHSR94] 中提出的算法的直接扩展，我们可以假设这些算法通过递归调用遍历 formal-in 和 formal-out 边之间的所有可 interprocedurally 实现的路径。对于 soundness，我们需要证明两个目标：

+   1. 如果同一调用的 formal-in 和 formal-out 成员之间存在一条可 interprocedurally 实现的路径且不包含去分类节点，则算法只会生成传统的 summary edge，而不会生成 summary declassification。由于该路径上的信息流传递性，summary 信息必须保守地遵守 overacity。算法 9 使用第 59 行中的标志 f 遵守这一要求。对 pathEdge 长度的归纳可以证明这一点：

如果 pathEdge 的长度为 0 $(x = y)$，第 9 行断言如果 $x \in D$ 则标志 $f$ 为 false，true。于是假设 $f$ 正确表示 pathEdge $(x, y, f)$ 是否不包含去分类。则第 50 行断言在扩展的 pathEdge $(w, y, f')$ 中 $f'$ 为 true（即路径 $w \to y$ 上没有去分类），如果 $w \notin D \land f$ 成立。注意如果 $w$ 和 $y$ 之间已有其他路径被探索过（第 40 行的条件成立），我们仅通过第 50 行中的析取记住是否存在一条没有去分类的路径。

## 4.8. 改进的 interprocedural 去分类

2. 否则，如果同一调用点 formal-in 和 formal-out 参数的所有路径都包含一个去分类，我们需要证明对于每条可 interprocedurally 到达的路径，HRB 算法计算出的约束是该路径生成的约束的超集。由于未遍历参数边，约束 S(act-in) ≤ S(form-in) 并未由算法 7 直接生成，因此必须由摘要去分类节点 d 强加。由于 R(d) 的值是通过与算法 7 相同的约束计算 S(form-in) 得出的，我们只需要证明 S(form-out) ≤ S(act-out) 由 HRB 算法生成。但这源于 S(form-in) 和 S(form-out) 的独立性，因为两者之间的每条路径都包含一个去分类节点，该节点不对边 w → v 的 S(w) ≤ S(v) 施加约束

### 4.8.3 超越 PDGs

SDG 精度通过持续研究稳步提高，精度也可以通过非 SDG 方法来提高，如程序分析中所开发的那样。

例如，片段

```
"if (h > h) then l = 0"
```

朴素切片作为 security type 会假设 h 到 1 的传递依赖，即使该体是死代码。这违反了 [SS05] 中提出的语义分析。这与定理 4.1 不矛盾，但源于分析精度。

幸运的是，今天的 SDGs 与为代码优化而开发的其他分析打包在一起，例如 interprocedural 常量传播、静态单赋值形式、符号求值和死代码消除。这些强大的分析在 SDG 构建开始之前执行，并将消除一系列虚假流。利用此类分析最简单的方法是从字节码构建 SDG。例如，任何优化编译器都会从机器代码或字节码中删除整个语句，因为它是死代码。注意字节码必须被视为程序含义的最终定义，经过所有复杂优化后在字节码中剩余的流必须被更认真对待。

此外，我们在 SDGs 之上提出了一种更强的机制，称为路径条件（见第 5 章）。路径条件对于流 x → y 是必要且精确的，并以程序变量的形式揭示流的详细情况。如果约束求解器能为程序的输入变量求解路径条件，将该解输入程序即可直接使非法流可见；此特性称为 witness。

```
1 [i+3] = x;
2 if (i>10)
3 y = a[2*j-42];
```

这里，流 $x \rightarrow^*$ y 的必要条件为 $\exists i, j. (i > 10) \wedge (i+3 = 2j-42) = false$，证明该流不可能发生，即使 PDG 表明否则。

## 4.9 相关工作

### 4.9.1 SDGs 和 IFC

已有若干论文论述了 SDGs 和 Java 的切片器，但据我们所知，只有 Indus 切片器 [JRH05] ——除其他外——完全实现并能处理 Java。Indus 可定制，嵌入 Eclipse，并具有非常漂亮的 GUI，但精度不如我们的切片器。特别是，它不支持完全的 context-sensitivity 而仅支持 k-limiting of contexts，并且允许对程序进行时间跟踪。

本文所述的工作改进了我们之前的算法 [HKS06]，该算法无法精确处理 classified 过程中的去分类。然而，该工作还为 Java PDGs 生成了路径条件的使用（即两个节点之间信息流的必要条件），可以揭示安全违规可能发生的精确情况。

虽然 IFC 与数据分析之间的密切联系很早就被注意到 [BC85]，但 Abudi 等人 [ABH99] 最早将切片与非干扰联系起来，但仅限于 $\lambda$-calculus 的基于类型的切片。令人惊讶的是，我们第 4.3 节的定理 4.3（适用于命令式语言及其 PDGs）并未更早被发现。只有 Anderson 等人 [ART03] 提出了 chopping 可能独立的示例。他们并未使用 security lattice，

Yokomori 等人 [YOT02] 很可能是第一个为过程语言提出并实现基于程序切片的 IFC 分析的人。它检查传统的非干扰，并支持最小格 $Low < High$ high。他们的分析是流敏感的，但既非 context-sensitive 也非 object-sensitive。

Hammer 等人结合了静态和动态 PDG 分析以检测非法信息流 [HG06]。它允许对表现出意外行为的程序进行事后分析，并计算重建非法信息流的精确 witness。

### 4.9.2 Security type systems

Volpano 和 Smith [VS97] 提出了第一个用于 IFC 的 security type system。他们扩展了传统类型系统以检查具有过程调用的简单语言中的纯非干扰。过程相对于 security classes 是多态的，允许 context-sensitive 分析。对多线程语言的证明见 [SV98]。

Myers [ML00] 定义了 JIF，即带信息流类型系统的 Java 语言扩展。JIF 编译器 [MCN+] 实现该语言。我们已在第 4.3 节讨论过类型系统精度较低，

