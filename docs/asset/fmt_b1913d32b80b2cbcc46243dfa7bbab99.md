
证明。令`Δ_k`为引理中表达式`α_{k,n}`的字母，`Σ`为表示`M`抹符号的字母。令`Δ_{k,#} = Δ_k ∪ {#}`且`Σ = Σ ∪ {#}`。表达式`α_M(x)`表示：

```
Γ_M := [Σ_# / Δ_{k,#}]
```

字符串`w`属于`α_M(x)`当且仅当它不具有以下形式：

```
| b_1 | # | #^k | b_2 | # | #^k | b_3 | # | #^k | ... | b_{n-1} | # | #^k | b_m | # | #^k |
| a_1 | # | a^k | a_2 | # | a^k | a_3 | # | a^k | ... | a_{m-1} | # | #^k | a_m | # | #^k |
```

其中：

(a) 当`y`在`p_{da}(non-free(G(k-1,n)))`时，下轨道的形式为`#y`。

(b) 上轨道编码`M`在输入`x`上的填充（但未旋转）的计算。

(c) 上轨道每个配置的左标记与下轨道上的`u_0`标记成对。

(d) 上轨道上的最后一个配置是接受的。

## 第 5 章 完全语言

(7) "某些`C_{i+1}`不直接由`C_i`派导出。"

（注：原文后续部分存在大量重复，此处已按要求不再重复输出原文）

## 5.7 结语

它们分别对于`DLOG`、`NLOG`、`P`、`PSPACE`是完全的。同样，基于逻辑公式的问题`UNSAT`、`UNIT`、`SAT`、`QBF`构成了对于`NLOG`、`P`、`NP`、`PSPACE`（分别对应）的完全问题族。或者，序列中的前两个问题可以用布尔逻辑中的两个问题替换：`FVP`、`SAT`、`QBF`，其中`FVP`是公式值问题。在第 3 节中解释了`CVP`：`FVP`是一个相似的问题，不同在于我们将输入中的布尔电路替换为了布尔公式。在显示`FVP`是`NLOG`-完全的练习中，Schiefer 和 Lieber 在其他几个方向上泛化了可满足性问题。Galis 证明了对图灵机有限制的各种决策问题也构成了标准列表中各种类的问题族。此类示例可以倍数增加。这些族可以作为指示"现实世界"中问题复杂性的指南。这是因为自然问题具有相似性，当一个`L`代表多个语言的成员时，我们也可以做出推测并确认`L`在标准列表中的复杂度（见第 1 章第 8 节）。

- 2. 在接下来的图中，我们画了示例。一个自然的问题是问：无向图可达性（记为`UGAP?`）的复杂度是否介于`IGAP`和`GAP`之间，但目前尚不清楚是否属于`NLOG`。我们将在后续关于计算问题的章节中证明这一点。

- 3. 强调这一点很重要：我们对许多重要的类都有完全语言，有足够的证据表明许多其他类没有完全语言（例如，参见 [15, 31, 16]）。

- 4. 源于语言同构性研究的发展取得了有趣的进展。如果`F`是一个变换族，我们说两个语言`L`和`L'`是同构的（模`F`），如果存在变换`t, t'`使得`t(L) ⊆ L'`，`t'(L') ⊆ L`且`t, t'`是恒等变换。关于所有`NP`-完全语言同构的 Hartman-isomorphism 猜想在所有`NF`-完全语言中都得到了证实；另一方面，也有反对该猜想的证据。例如，完全语言同构性下的最后一个正向结果是 [3]，它了所有`DEXPT`的完全语言通过线性长度增长的多项式时间变换等价（参见 [35, 34]）。我们将在第 2 卷回到这个问题。

## 练习题

- (1) 在适当的归约下，证明`DTIME(2^{n^k})`和`DSPACE(2^{n^k})`的完全语言。

- (2) 设复杂度函数`f`。在什么条件下，我们可以使用`≤_m^L`拥有`XSPACE(f)`、`XTIME(f)`、`XREVERSAL(f)`的语言？这道题暗示`≤_m^L`的特殊地位主要源于我们对标准列表的特殊关注。

- [5.2] 为什么标准列表中其他类的证明未能为`P`类产生一个完全类？

- [5.3] 考虑定理 1 中`F`和其他一些类的证明。证明的轮廓可以描述如下：设`(μ, ρ, F)`为标准列表中的任意特征类，其中`μ`是资源，`F`是复杂度函数族。`MACHINES(μ, ρ, F)`有一个高效的通用模拟器`U`，其中每个模拟器在区域`p O(bound)`，`f_i ∈ F`内接受。考虑语言`L^K = {i|x#m^* : m, f(|x|)∈F, x ∈ U}`。

- [5.4] 回忆`1GAP`的定义，它由所有度数为 1 且从第一个节点到最后一个节点存在路径的同构图（通过边列表）组成。`1IGAP'`是由邻接矩阵定义的变体。证明使用`≤_m^L`-归约无法将`1GAP'`归约到`1GAP`。

- [5.5] 证明`UG`（结末中定义的无向图访问性问题）使用`≤_m^L`-归约是`DLOG`-hard。

## 第 5 章 完全语言

- [5.6] (Laaser) 证明以下问题对于`NLOG`是完全的：定义`CON`和`SCON`为形式如`(n, G)`的输入集，满足`∀m ∈ [1..n] ⇒ ∃从节点 1 到 m 的路径`。

- [5.7] 给出一个"标准"解析谬误的反例：设`C_1`和`C_2`为`CNF`公式`F`中的子句，如果`(F - {C_1, C_2}) ∪ {C}`是不可满足的，那么……哪一个方向是正确的？

- [5.8] 证明解析定理。

- [5.9] 通过测试算法的正确性证明`3UNIT`在`P`中。

- [5.10] 通过替换不包含 3 个文字的子句，证明`3UNIT`是`P`-完全的。

- [5.11] 设`M`是`s(n)`空间非确定的。对于每个长度为`n`的输入`x`，构造一个系统`S(x)`使得`S(x)`被`M`接受。提示：启动 Savitch 定理的证明。

- [5.12] (Ladner) 证明电路值问题 (`CVP`) 在对数许多归约下是`P`-完全的。为了证明它是`P`-hard，给出一个直接证明（而不是将一个`P`-hard问题归约到`CVP`）。

- [5.13] 证明公式值问题 (`FVP`) 在对数许多归约下是`NLOG`-完全的。

- [5.14] 证明`AND-OR-GAP`问题是`P`-完全的。

- [5.15] (Dobkin, Leipton) 证明线性规划 (`RLP`) 在对数许多归约下是`P`-hard。

- [5.16] 证明到`AND-OR-GAP`和`CVP`的直接归约在两个方向上。

- [5.17] (Reif) 证明以下与深度搜索相关的决策问题在对数许多归约下是`P`-完全的：给定`(G, u, v)`，`G`是顶点`[1..n]`的图，`u`和`v`是顶点。属性：在从节点 1 开始的深度搜索中，`u`在`v`之前被访问。

- [5.18] 证明`MEMBER(+)`在`P`中。

- [5.19] (Meyer, Stockmeyer) 有一类问题类似于第 4 节的问题：整数表达式使用运算符`+, ¬, ∪`，以明显的方式从 0 和 1 构建。对于`(1+1)∪(1+1) = 01`，每个表达式表示一个非负整数，0 和 1 代表零和一，`+`表示加法（不是正则表达式中的并），`¬`表示，`∪`表示集合并。`N-MEMBER(+)`是整数表达式的成员性问题。更精确地说，这是识别所有形式为`(x, a)`的问题，其中`x`是二进制数，`a`是`x ∈ L(a)`。该问题是`P`-完全的。

- [5.20] (Meyer, Stockmeyer) 证明`INQ(0, {*})`是`P`-完全的。

- [5.21] (Meyer, Stockmeyer) 证明`INQ(+)`是`P`-完全的。

- [5.22] 为判定`L(a) = Σ*`在`O(1)^{|a|}`内完成给出一个直接证明，避免对非确定有限自动机的归约。

- [5.23] (Hunt, Hopcroft) 设`NONEMPTY(Σ, Ω)`表示`Ω ≠ ∅`的表达式。注意如果`Ω ⊆ {+, *}`则`L(a) ≠ ∅`恒成立。证明`NONEMPTY(+, *)`是`PSPACE`-完全的。

- [5.24] 考虑等价问题`EQUIV(Σ, Ω)`，它由所有满足……的表达式对`(α, β)`组成。这与不等问题`INEQ(Σ, Ω)`有关系？

- [5.25] 按照第 6 节`(γ)`中的所述构造`γ`-表示`ρ_γ`。

- [5.26] (Stockmeyer) 证明`FULL(+, ~)`的复杂度是`ELEMENTARY`-hard。也就是说，你必须从第 6 节的构造中消除 Kleene 星。

- [5.27] 证明计数机执行了`O(2^n)`步。**提示：** `c_n`为计数机从 1 计数到`2^n - 1`的步数。例如，我们有：

```
1 → 10 → 100 → 101 → 110 → 111
```

其中 6 次变换需要`4+2+6+4+2=20`步，所以`c_3 = 20`。（这里我们假设头先扫描……）此外`c_1 = 0, c_2 = 12`。给出`c_n`的递归关系。

- [5.28] `FULL(+, *, ~)`复杂度的上下界并不紧密。改进对应于`g(n)`生长比`g(n) = n^2`更快的证明。例如，很容易修改我们的计数机以获得`(n^2)`构造（如何做？）。这种改进是无关痒的，因为可以使用`k`-进制计数并获得`k^n`-构造。`k`的最佳选择是什么？

- [5.29] 开发变换的理论。我们说一个变换`t : Σ_i^n → Γ_i^n`在对空间归约下对于变换族`T`是硬的，如果对于所有`t ∈ T, t : Σ_i^n → Γ_i^n`，存在对数空间变换`s_0 : Σ_i^n → Σ_0^n`和`s_1 : Γ_0^n → Γ_i^n`，使得对于所有`x ∈ Σ_i^n, s_1(s_0(x)) = t(x)`。设`T`为由确定多项式时间变换器计算的变换类。证明`T`的完全变换。

对于反或同步复杂度类的自然复杂度问题了解较少。

## 参考文献

[1] A. Adachi, S. Iwata, and T. Kasai. 某些组合游戏问题需要`ω(n^k)`时间。Journal of the ACM, 31(2):361–377, 1984.

[2] A. V. Aho, J. E. Hopcroft, and J. D. Ullman. 计算机算法的设计与分析。Addison-Wesley, 1974.

[3] L. Berman. 多项式归约与完全集。博士论文，康奈尔大学，1977. 博士论文，计算机科学。

[4] R. V. Book. 翻译引理、多项式时间与`(log n)^k`-空间。Theor. Computer Science, 12:215–226, 1976.

[5] R. V. Book. 关于空间限制预言机接受的语言。Acta Informatica, 12:177–185, 1979.

[6] A. K. Chandra and L. J. Stockmeyer. 交替。17th Proc. IEEE Symp. Found. Comput. Sci., 98–108, 1976.

[7] J. Chen and C.-K. Yap. 反转复杂度。SIAM J. Computing, 待发表，1991.

[8] S. S. Cook. 时间-存储权衡的观察。5th Proc. ACM Symp. Theory of Comp. Sci., pages 29–33, 1973.

[9] D. P. Dobkin, R. J. Lipton, and S. Reis. 线性规划对于`P`而言是`LOG-SPACE`硬的。Information Processing Letters, 8:96–97, 1979.

[10] S. Even and R. Tarjan. 一个在多项式空间内完全的组合问题。Journal of the ACM, 23:710–719, 1976.

[11] L. M. Goldschlager. 单调和平面电路值问题对于`P`是`log space`完全的。SIGACT, 9(2):25–29, 1977.

[12] L. M. Goldschlager, R. A. Shaw, and J. Staples. 最大流问题对于`P`是`log space`完全的。Computer Science, 21:105–111, 1982.

[13] R. Greenlaw, H. J. Hoover, and W. L. Ruzzo. 并行计算的限制：`P`-完全性理论。Oxford University Press, New York, 1995.

[14] J. Hartmanis. 可行计算与可能的复杂度属性。S.I.A.M., Philadelphia, Pennsylvania, 1978.

[15] J. Hartmanis and L. A. Hemachandra. 不含机器的复杂度类：关于`UP`的完全语言。Theor. Computer Science, 58:129–142, 1988.

[16] J. N. Hartmanis and N. Immerman. 关于`NP ∩ co-NP`的完全问题。12th ICALP (LNCS No. 94), pages 250–259, 1985.

[17] J. N. Hartmanis, N. Immerman, and S. Mahaney. 单向对数带归约。19th Symposium FOCS, pages 65–71, 1988.

[18] H. B. Hunt. 关于语言的时间和带带复杂度，I。5th Proc. ACM Symp. Theory of Comp. Sci., pages 10–19, 1973.

[19] N. D. Jones. 组合问题之间的空间归约性。Journal of Computers and Systems Science, 11:68–85, 1975.

[20] N. D. Jones and W. T. Laaser. 确定性多项式时间的完全问题。Theoretical Comput. Sci., 33:105–117, 1977.

[21] R. E. Lader. 电路值问题对于`P`是`log space`完全的。SIGACT News, 7(1):18–20, 1975.

[22] A. R. Meyer. 后继的弱单调二阶逻辑不是元素递归的。In Fold and E. (eds.), Logic Colloquium: Symposium on Logic Head at Boston University, 1972–73, pages 132–154. Springer-Verlag, 1975.

[23] A. R. Meyer and L. J. Stockmeyer. 带有平方的正则表达式等价性问题需要指数空间。13th Proc. Symp. Found. Comput. Sci., pages 125–129, 1972.

[24] B. Monien and I. Hull. 关于消除使用小于对数空间的图灵机的非确定性。In Lecture Notes in Computer Science, volume 71, pages 431–445, Berlin, 1998. Springer-Verlag, Proc. on Automata, Languages and Programming.

[25] J. B. Orlin. 动态语言与动态优化的复杂度。ACM Symp. of Comp. Sci., pages 218–227, 1981.

[26] C. H. Papadimitriou. 对抗自然的游戏。Journal of Computers and Systems Science, 31:288–301, 1985.

[27] R. Péter. 递归函数。Academic Press, New York, 1967.

[28] R. W. Ritchie. 可计算函数的类。Trans. AMS, 106:139–173, 1963.

[29] J. Savitch. 非确定性和确定性带复杂度的关系。Journal of Computers and Systems Science, 4:177–192, 1970.

[30] T. Schaefer. 双人完全信息游戏的复杂度。Journal of Computers and Systems Science, 16:185–225, 1978.

[31] M. Sipser. 关于相对化与完全集的性。9th ICALP (LNCS No. 140), pages 523–531, 1982.

[32] L. J. Stockmeyer. 自动机理论与逻辑决策问题的复杂度。技术报告 TR-133, MIT., 1974. 博士论文。
