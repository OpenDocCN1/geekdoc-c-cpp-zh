

## 2.2 程序切片

算法 2 计算摘要边的边的伪代码

```
1 function ComputeSummaryEdges
2 Input: G 是一个 SDG
3 Output: SummaryEdge 摘要边集合
4 declare PathEdge, SummaryEdge, WorkList: 边集合
5 declare FragmentPath: 从顶点到边集的映射
6 begin
7 PathEdge := ∅; SummaryEdge := ∅; WorkList := ∅
8 foreach v in FormalOutNodes(G) do
9 insert (w → w) into PathEdge
10 insert (w → w) into WorkList
11 od
12 while WorkList ≠ ∅ do
13 select and remove each edge v → w from WorkList
14 switch v
15 case v in ActualOutNodes(G) do
16 foreach each a x → v ∈ SummaryEdge v x → ed v in G do
17 Propagate(x → ed)
18 od
19 esac
20 case v in FormalInNodes(G) do
21 foreach c ∈ {G | c ∈ (Entry(w)) ∈ E} do
22 let x = CorrespondingActualIn(c, v)
23 y = CorrespondingActualOut(c, v) in
24 insert x → y into SummaryEdge
25 for each a that y → a in fragmentPath(y) do
26 Propagate(x → a)
27 od
28 end let
29 od
30 esac
31 default :
32 foreach each a x → _dd v ∈ G ∨ x → _ed v ∈ G do
33 if x → _dd v or v are not both parameter nodes then // 排除对象树
34 Propagate(x → w)
35 fi
36 od
37 switch
38 od
39 return(SummaryEdge)
40 end
42 procedure Propagate(e: edge (v → w))
43 begin
44 if e ∈ PathEdge then
45 insert e into PathEdge
46 insert e into WorkList
47 if v ∈ ActualOutNodes(G) do
48 insert e into fragmentPath(w)
49 fi
50 fi
51 end
```

![](img/27c6595637bae6b27613772d7079f8a2_49_0.png)

# 基于图的切片的正确性

Horwitz 等人 [HPR88] 表明 PDG（对于包含数组的语言）足以表示程序的执行行为：如果两个程序的 PDG 是同构的，那么对于给定的输入，这两个程序要么都发散，要么以所有变量的相同值终止。基于简单 while 语言的 PDG 的反向过程内切片在 [RY88] 中被证明是正确的。他们的切片定理（Slice Theorem）证明了，对于程序终止的任意初始状态，该程序及其切片对切片中的每个元素计算出相同的一序列值序列。这一结果被 Brinkley 等人 [BHR89] 扩展到 SDG，并扩展到带有堆分配存储（基于 LISP 风格的控制操作符）和指针的程序 [PS91]，遵循了 [HPR89] 的精神。众周知的是，这种操作符足以建模复杂的堆甚至类 Java 的对象。我们在 2.5 节中对 SDG 的扩展将与过程间数据依赖参数传递的正确性论证一起给出。存在无结构化控制流时的语法保持切片已由 Ball 和 Horwitz [BH93] 以及 Choi 和 Ferrate [CF94] 独立解决。两种解决方案都包含了正确性证明。Harman 和 Danihani [HD98] 扩展了 Agrawal [Agr94] 的解决方案并提出了正确性证明。

## 2.3 指向分析 (Points-to-Analysis)

指针分析是分析堆操作语言的主要前提。对于面向对象的语言，它回答了给定指针或引用在运行时可能指向哪些对象的问题。

| 1 Object o1; | |
| :--- | :--- |
| 2 String o2; | |
| 3 o1 = new Object(); | o2 → new Object() |
| 4 o2 = new String(); | |
| 5 if (...) | | |
| 6 o1 = o2; | new String() → new Object() |

图 2.7：代码片段和可能的指向图

基于此分析可以导出相关的关系，例如可能使用（may-using），即两个变量是否引用内存中的相同位置——因此是同一个对象，在某些条件下也是必须使用（must-using），即两个变量是否始终指向同一个对象。

自从基础技术由 Andersen [And94] 和 Steensgaard [Ste96] 提出以来，已有数百论文针对这一问题（例如 [SS00b, RMR01, LLS01, MRG02, NRO03, LL03, WL04, LH08]），并以此完善了该技术，使得如今指向分析对于真实的编程语言和程序具有良好的扩展性。然而，尽管指向分析在约 [Hin01] 年前就为人知，但各大主要会议上仍有关于该主题的论文在改进精确性和扩展性问题。

指向分析通常通过基于约束的程序分析来解决：从控制流图中提取若干由于程序语义而必须满足的约束。这些约束可以被求解，并产生一个指向关系的保守解。约束系统传统上表示为图，其中：
- 每个指针有一个节点
- 每个分配点有一个节点
- 如果 p 可能指向 q，则存在边 p → q
- 如果 p 必须指向 q，则存在边 p → q

作为一个示例，考虑图 2.7，其中展示了指向图。每个变量 o1 和 o2 有节点。第 3 行和第 4 行的赋值产生了边。第 6 行的赋值产生了另一条边。

![](img/27c6595637bae6b27613772d7079f8a2_51_0.png)

# 第 2 章 面对象语言的依赖图与切片

## 2.3.1 基于包含 vs 并并分析

确定指向的两种基本方法已被提出：Stegaard [Ste96] 提出了一种基于合并的方法，指针要么别名要么指向相同的对象集合。其优势是近线性的复杂度 $O(n\alpha(n))$，其中 $\alpha$ 是反阿克函数，基于 Leis-Tarjan 算法 [LT79]。在图 2.7 的示例中，最右侧的图对应于方法。由于合并意味着 o1 的指向等于 o2 的指向，节点之间双向连接。不幸的是，将此方法应用于 Java 会产生若干不可理想的属性。Streckbench [SS00b] 发现像 Java 这样强类型的语言使用基于合并的方法会丢失类型安全，如图 2.8 所示，一个 String 类型的引用被确定可能指向声明类型 Object。这对动态绑定的近似产生了巨大影响，因为调用的方法取决于目标对象：当 o2 上调用 char() 时，分析无法确定 java.lang.Object 中的哪个方法。由于缺乏类型信息，现在不清楚是分析存在 Bug，还是仅仅是由于过度近似。这导致了多年对基于包含方法的扩展性的研究。

Andersen 的指针包含包含方法仅在赋值的指针之间插入单向边。这种方法只会生成遵守类型安全的约束，这更贴合赋值的语义，如图 2.7 所示。在这里，只有 o1 可能指向 o2，反之则不然。指向关系比基于合并的方法更精确（见图 2.8 的左图）。然而，求解约束系统的代价为 $O(n^3)$，其中 $n$ 是程序中的语句数量。尽管如此，基于包含的分析在过去几年中占据主地位，这归于近期研究中运行时 BDD 的进展，例如使用更好的数据结构 [WL04, LH08]。

