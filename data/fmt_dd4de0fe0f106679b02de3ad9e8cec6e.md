
`rel' = [(ag,s,s') | (ag,s,s') <- rel, s' `elem` states', s' `elem` states']`

这使用了在给定关系和代理列表的情况下状态列表的闭包：

# 13.7 认识论模型检查

```haskell
closure :: Ord state => [(Agent,state,state)] ->
[Agent] -> [state] -> [state]
closure rel agents xs = lfp f where
f ys = (sort.nub) concat (map snd ys)
```

在给定状态 $S$ 和代理集合 $B$ 的情况下，关系 $R$ 的扩展由 $\{t \mid s_tR, s \in S\}$ 给出。以下是实现：

```haskell
expand :: Ord state => [(Agent,state,state)] ->
[Agent] -> [state] -> [state]
expand rel agents ys = (sort.nub) concat (map snd ys)
```

状态 $s$ 下代理 $a$ 的认识论备选是从 $s$ 可达的状态 $R_a s$：

```haskell
alternatives :: Eq state => [(Agent,state,state)] ->
Agent -> state -> [state]
alternatives rel ag current = [s' | (a,s,s') <- rel, a == ag, s == current]
```

认识论模型检查器的实现结束。为了展示如何使用它，我们演示了一个脏脸场景的检查。我们模拟了有四个孩子 Alice、Bob、Carol 和 Dave 的情况，其中 Carol 和 Dave 是脏脸。我们使用命题 $p1, p2, p3, p4$ 来表示第一个、第二个、第三个或第四个孩子是脏脸。初始认识论模型有 16 个世界，代理 $a$ 无法区分 $p1$ 的值，代理 $b$ 无法区分 $p2$ 的值，代理 $c$ 无法区分 $p3$ 的值，代理 $d$ 无法区分 $p4$ 的值。这完全决定了可达关系。

```haskell
computeAcc :: [(Agent,Integer,Integer)] ->
[Integer] -> [Prop]
computeAcc rel states = [(ag,y) | (ag,x,y) <- rel, x `elem` states]
```

当 $p1, p2, p3$ 为真时，给出了 `initMuddy` 的定义：

```haskell
initMuddy :: EpistM Integer
initMuddy = Mo states val rels actual
where
states = [0..15]
```

$a$ 无法区分 $p1$ 的值，代理 $b$ 无法区分 $p2$ 的值，代理 $c$ 无法区分 $p3$ 的值，代理 $d$ 无法区分 $p4$ 的值。这给出了以下结果：

```haskell
CAIA> displayS5 initMuddy
[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]
[[0,[]], (1,[p]), (2,[q]), (3,[p,q]), (4,[p]), (5,[p,q]), (6,[q]), (7,[p,q]), (8,[p]), (9,[p,q]), (10,[q]), (11,[p,q]), (12,[p]), (13,[p,q]), (14,[q]), (15,[])]
(a,[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15])
(b,[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15])
(c,[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15])
(d,[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15])
[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]]
```

在第一轮中，他们说他们不知道自己的状态：

```haskell
m2 = convert (upd_pa initMuddy (Conj [Neg aK,Neg bK,Neg cK,Neg dK]))
```

这是结果：

```haskell
CAIA> displayM2
[0,1,2,3,4,5,6,7,8,9,10]
[[0,[p3,p4]], [1,[p2,p4]], [2,[p2,p3]], [3,[p2,p4]],
[4,[p1,p4]], [5,[p1,p3]], [6,[p1,p4]], [7,[p1,p2]],
[8,[p1,p2,p4]], [9,[p1,p2,p3]], [10,[p1,p2,p3,p4]]]
[a,[0,0],[1,8],[2,9],[3,10],[4],[5],[7]]
[b,[0,3],[1,2],[4,8],[5,9],[6,10],[7]]
[c,[0,0],[1,3],[2,[4,6],[5],[7,9],[8,10]]
[d,[0,0],[1,2],[2,3],[4,5],[6,7],[8,9,10]]
```

# 通信作为信息性行为

[3]

在第二轮中，他们再次说他们并不知道自己的状态：

```
m3 = convert (upd_pa m2 (Conj Neg aK,Neg bK,Neg cK,Neg dK))
```

结果是：

```
GAIA> displayS5 m3
[0,1,2,3,4]
[[0,[p2,p3,p4]), (1,[p1,p3,p4]), (2,[p1,p2,p4]),
(3,[p1,p2,p3]), (4,[p1,p2,p3,p4]])
(a,[[0,4],[1],[2],[3]])
b(b,[[0],[1,4],[2],[3]])
c(c,[[0],[1],[2,4],[3]])
d(d,[[0],[1],[2],[3,4]])
[0]
```

在第三轮中，a 仍然不知道，但 b, c, d 知道自己的状态。

```
m4 = convert (upd_pa m3 (Conj Neg aK, bK, cK, dK))
```

这一轮之后，一切都是已知的：

```
GAIA> displayS5 m4
[0]
[[0,[p2,p3,p4]])
(a,[[0]])
(b,[[0]])
(c,[[0]])
(d,[[0]])
[0]
```

**练习 13.9** 为智智者谜题执行模型检查过程。

**练习 13.10** 为“Jan 是一个单身汉”更新的预设执行模型检查过程。检查如果在此之前发布一个关于“Jan 是男性”的公共公告会发生什么。

**练习 13.11** 为是/否问题执行模型检查过程。尝试为一个问题找到尽可能多的不同答案。实现一个检查，判断什么构成了特定问题的适当答案。

## 13.8 延伸阅读

**练习 13.12** 实现从语言中移除公共公告算子的翻译。类型为 `tr1 :: Form -> tr2 :: EE -> EE`。接下来，执行若干检查以测试翻译是否符合语义化。

**练习 13.13** 实现从语言中移除公共变化算子的翻译。类型为 `tr3 :: Form -> tr4 :: EE -> EE`。接下来，执行若干检查以测试翻译是否符合语义化。

关于认识逻辑的教材 [FHMV95] 和较近的 [DvdHK07]。动态认识逻辑不仅分析知识，还分析通信的认识效应。一篇性论文是 [BM598]。一种非常动态的认识逻辑的优雅版本可以在 [BVE06] 中找到。动态认识建模是计算认识更新效应的艺术。一个用 Haskell 实现的工具是 DEMO；详见文档 [Ei07a]。

Chwe 关于社会仪式在创建共同知识中作用的启发性分析见于《理性仪式》[Chw01]。《社会软件论述》[EV09] 提供了许多关于（共同）知识在社会互动中作用的例子。

基于共同知识的预设分析是基于 [EU07]，而对问题和答案恰当性的分析灵感源于 [UG08]。

## 后记

现在，亲爱的读到这里的读者，在我们离开之前，让我们花几分钟对你说几。你确实走了很远的路。你起初只是想了解自然语言语义的一一二，看看你现在处于哪里。在本书的最后，你发现自己正处于精通函数式编程的途中。此外，你在自然语言语义和语用分析中形式化工具的应用积累了相当经验。可以说，还有很多可以学习的东西，但现在是时候放松并为你所取得的成就感到自豪了。至少请喝杯啤酒吧。我们认为你值得。

## 参考文献

[Als92] H. Alshawi, 编辑. *核心语言引擎 (The Core Language Engine)*. MIT Press, Cambridge, Mass., and London, England, 1992.

[AS96] H. Abelson and G.J. Sussman. *计算机程序的结构与解释（第二版） (Structure and Interpretation of Computer Programs).* MIT Press, 1996.

[AU72] A.V. Aho and J.D. Ullman. *解析、翻译与编译理论，第一卷：解析 (Theory of Parsing, Translation and Compiling, volume I: Parsing)*. Englewood Cliffs, NJ, 1972.

[Bar84] H. Barendregt. *λ 演算：其语法与语义（第二版） (The Lambda Calculus: Its Syntax and Semantics (Second edition).* North-Holland, Amsterdam, 1984.

[Bar02] Chris Barker. 延续与量化的性质. *自然语言语义，延续 (Natural Language Semantics, Continuations)*, 241–242, 2002.

[Bar04] Chris Barker. 自然语言中的延续。在 H. Thielecke 编辑，CW'04: *第四届 ACM SIGPLAN 研讨会论文 (Proceedings of the 4th ACM SIGPLAN workshop)*. 技术报告 CSR-04-1, 第 1–11 页。伯明翰大学计算机学院。

[BAW07] Ben-Ai and Yon Winter. 内涵化的语义。在 Rein-hard Muskens 编，《类型理论语法法新方向研讨会 (Workshop on New Directions in Type-Theoretic Grammars)*, 98–112.

[BB00] H. Barendregt and E. Barendregt. λ 演算导论，修订版. 技术报告，内梅根大学，2000年3月。可通过 `http://ftp.knij.nl/Comp/lambda.pdf` 获取。

[BB05] P. Blackburn and J. *自然语言的表示与推理：语义入门课程 (Representation and Inference for Natural Language: A First Course in Semantics)*. 2005.

[BC81] J. Barwise and R. Cooper. 广量词与自然语言. *语言学与哲学 (Linguistics and Philosophy)*, 4:159–219, 1981.

[BCM02] F. Baader, D. Dalver, N. Nardi, and P. Patel, 编辑. *描述逻辑 (The Description Logic)*. Cambridge Press, 2002.

[BE82] J. van Benthem and J. van Eijk. 交互动力学 (The dynamics of interaction). *语义学学 (Journal of Semantics)*, 1(3):1–30, 1982.

[Ben86] J. van Benthem. *逻辑语义论文 (Essays in Logical Semantics)*. 1986.

[Ben88] Johan van Benthem. 内涵化策略。在 I. Bodna, A. Mat, 和 L. Pöl 编，《纪念 Imre Ruza 65 周岁：逻辑与方法 (Logic and Methodology: To Imre Ruza on his 65th birthday)*, 41–59, 1988.

[GGM93] ., ,,,, ..............  ,, ..        ( of of of of of of of of,)*, 37–29, 1993.

[Cho81] N. Chomsky. *辖与约束讲义 (Lectures on Government and Binding)*. Foris, Dordrecht, 1981.

[Cho92] N. Chomsky. *极简主义计划 (Minimalist Program)*. MIT Press, 1992.

[Bir04] Chris Barker. 公共公告的形式化。在 H. Thielecke 编，CW'04: *第四届 ACM SIGPLAN 研讨会论文 (Proceedings of the 4th ACM SIGPLAN workshop)*. 技术报告 CSR-04-1, 第 1–11 页。伯明翰大学计算机学院。

[BM97] J. van Benthem and A. Terulen. *逻辑与语言手册*. Elsevier, 1997.

[Bur98] Stanley N. *数学与科学的逻辑 (Logic for Mathematics and Science)*. Prentice Hall, 1998.

[Bur03] D. Buring. *约束理论 (Binding Theory)*. Cambridge Textbooks in Linguistics. Cambridge University Press, 2005.

[BVE06] J. V. Benthem, J. van Eijk, and B. Kooi. 通信的变化. *信息与计算 (Information and Computation)*, 204(11):1620–1662, 2006.

[Cam08] Geoffrey Campbell. *谋的语义 (The Semantics of Murder)*. Serpent's Tail, 2008.

[Cho57] N. Chomsky. *句法结构 (Syntactic Structures)*. Mouton, The Hague/Paris, 1957.

[Cho59] N. Chomsky. 关于语法的形式形式。在 *语言与控制 (Language and Control)*, 3:137–167, 1959.

[Cho94] D. Buring. 还原性的刻化。在 M. Kamazawa 和 C. Schneider 编，《逻辑、有限性 (Logic and Finiteness)*, 147–171, 1994.

[Chu36] A. Church. 初等数论中的一个不可解问题. *美国数学杂志 (American Journal of Mathematics)*, 58:345–363, 1936.

[Chw01] Michael-Chong Yue. *理性 (Rationality)*. Princeton University Press, Princeton and Oxford, 2001.

[CK97] J. Cole and C. Kisseberth. 限制多级约束：元音和谐中的规则交互。在 K. Suzuki 和 D. Elgin 编，《亚利桑那语音学会议 (Proceedings of the Arizona Phonology Conference)*, 18–38, 1997.

[Coo75] R. Cooper. *蒙太格语义理论与转换句法 (Montague's Semantic Theory and Transformational Syntax)*. 博士论文，马萨诸塞大学阿姆斯特分校，1975.

[Coo83] R. Cooper. 量化与句法理论 (Quantification and Syntactic Theory). Reid, Dordrecht, 1983.

[Dal83] D. van Dalen. *逻辑与结构（第二版） (Logic and Structure (Second edition))*. Springer, Berlin, 1983.

[DE04-DE04] Kees Doets and Jan van Eijk. *Haskell 逻辑、数学与编程之路 (The Haskell Road to Logic, Maths and Programming)*, 计算文本系列第 4 卷。College Publications, London, 2004.

# 参考文献 391

[Dek03] P. Dekker. 此同时，在弗雷格边界内。《语言与哲学》(Linguistics and Philosophy)，26:547–556, 2003。

[d04] Philippe de Grote. 迈蒙格动力学理论。在《语义与语言理论第 XVI 次会议论文集》，CLC Publications, 2004。

[DI07] Ha Daume III. 另一个一个 Haskell 教程，wikibooks.org, 2007。

[Dow89] D. R. Downey. 关于“论题角色”的语义内容。在 B. Partie, G. Chiesa 和 R. Turner 编，《属性、类型与意义》，第 2 卷，69–130。Klaumer, 杜德勒赫特, 1989。

[DP90] B. A. Davey 和 H. A Priest. 格与序关系绪论（第二版）。剑桥大学出版社, 2002（第一版，1990）。
