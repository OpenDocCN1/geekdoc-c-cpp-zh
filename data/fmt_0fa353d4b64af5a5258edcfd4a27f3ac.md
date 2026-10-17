
```
1 influenced(dm, COLL)
2 newgoal: influenced(dm, COLL)
3 cited(dm, dm)
4 ans: cited(dsw, dm).
5 newans: influenced(dm, dsw)
6 cited(_h397, dm), influenced(_h397, COLL)) 
7 cited(_h397, dm)
8 ans: cited(dsw, dm)
9 influenced(dsw, COLL)
10 newgoal: influenced(dsw, COLL)
11 cited(COLL, dsw)
12 ans: cited(dm, dsw)
13 newans: influenced(dsw, dm)
14 ans: cited(tjg, dsw)
15 newans: influenced(dsw, tjg)
16 cited(_h795, dsw), influenced(_h795, COLL))
17 cited(_h795, dsw)
18 ans: cited(dm, COLL)
19 ans: influenced(dm, dsw) from table
20 newans: influenced(dsw, dsw)
21 ans: cited(tjg, dsw)
22 influenced(tjg, COLL)
23 newgoal: influenced(tjg, COLL, COLL)
24 cited(_h1371, tjg), influenced(_h1371, COLL))
25 cited(_h1371, tjg)
26 ans: influenced(dsw, dm) from table
27 newans: influenced(dm, dm)
28 ans: influenced(dsw, tjg) from table
29 newans: influenced(dsw, dsw) from table
30 newans: influenced(dm, tjg)
31 ans: cited(dm, dsw) from table
32 ans: influenced(dm, dm) from table
33 ans: influenced(dm, tjg) from table
34 ans: influenced(dm, dm) from table
35 ans: influenced(dm, dsw) from table
36 done
```

> 18. 如果 F 可以通过将 0 或多个变量替换为常量或其他变量从 G 推导出，则称 G 包含 F。例如，`influenced(X, Y)` 包含了 `influenced(dm, Y)`、`influenced(X, X)`、`influenced(X, Y)` 和 `influenced(dm, tj)`。
> 19. Prolog 教师在教授数据递归时，会明智地选择图，例如 `advises` 关系，这种图可以没有循环。

（注：OCR 文本似乎存在重复或碎片。我将根据提供的文本重新梳理逻辑。）

## 1.5 评估技术

### 1.5.2.2 其他自顶而下的方法

我们简要提到了旨在对 Datalog（或更通用）程序进行评估的自顶而下策略变体。Tamaki 和 Sato [1986] 引入了 OLDT 分解，这是一种迭代加深的方法，并对之前迭代的模式进行表化（tabling）。本文是第一个针对逻辑编程的自顶而下表化算法规范，但未包含实现。

扩展表（Extension Table, ET）评估机制 [Dietrich 1987, Dietrich and Warren 1988] 是表化的一种形式，可以在 Prolog 中实现。它为与其关联的谓词 $p$ 使用了两个额外结构。可以调用 `et_` 来获取扩展表。它具有与 $p$ 相同的列，用于记录之前导出的 $p$ 的事实。另一个是 `ca1_`，它包含了为止遇到的 $p$ 的子目标中使用的变量和常量模式。这些谓词记录了子目标及其答案，并在子目标被调用和答案返回时进行更新。然而，这种基于 Prolog 的简单算法并不是完备的。例如，考虑左递归定义且规则顺序反转。那么初始的、由目标引导{dn, COLL} 将立即调用自身。但此时它还没有答案，因此它必须回溯尝试其他路径来生成答案。除非以某种方式返回并重新开始那个“失败”的子目标调用，否则某些答案可能会丢失。人们可能会认为需要时可以恢复，或者必须重新生成。为了完备性，ET 算法反复迭代其计算，直到表谓词发生变化。

ET 算法的变体和扩展已在某些 Prolog系统中开发并实现，包括 Zhou 等人 [2001] 的 B-Prolog 以及 Guo 和 Gupta [2001] 的 ALS Prolog。这些技术被称为线性表化（linear tabling）。

XSB 的 SLG 算法 [Chen and Warren 1996, Swift and Warren 2011, Warren 2007] 是上述 OLDT 的扩展。它与 OLDT 的不同之处在于它会挂起子目标的计算，并在根据需要恢复，类似于第 1.5.2.1 节中的讨论。由于它会挂起和恢复计算，因此不需要像迭代方法（如 ET）那样进行重新计算，从而具有更好且更复杂的属性。XSB 还整合了一种“增量完备”算法，通过控制任务调度的顺序并跟踪子目标依赖关系，在整个计算完成之前确定子目标何时被完全评估（即它们在表中的所有答案）。这种方法能够高效地处理默认否定。

Vielle 开发了查询-子查询（Query-Sub-Query, QSQ）方法 [Vieille 1986] 专门用于 Datalog，它与表化和 ET 的区别在于具有“多目标（multigoals）”特性，即谓词中的给定位置可以包含一组绑定。（我们注意到，QSQ 的原始版本在某些程序上是不完备的——它无法找到所有答案）。后来 Negdl [1987] 和 Vielle [1987] 的工作提供了 QSQ 的完备版本。这种泛化目标可以通过组合共享相同变量模式的目标，以及以一次处理集合的方式求解目标产生。例如，考虑查询
- related(dsw, X).

使用用于 `related/2` 的第二个规则：
- related(P1, P2) :- advised(B, P1), related(B, P2).

第一个子目标将是 `advised(B, dsw)`。如果我们从 EDB 中请求所有绑定，我们将得到 `(advised(jbf, dsw), advised(wcr, dsw))`。根据结果，QSQ 将生成泛化子目标 `related{{jf, wcr}, X}`。该子目标可以与重复规则匹配，生成泛化子目标 `advised(B1, {jf, wcr})`。这个子目标说明了 QSQ 的优势之一，它可以将对 EDB 的调用合并为一个调用，这如果 EDB 由数据库系统外部管理将非常有用。求解这个泛化子目标将给出绑定集 $B1 = \{hw, dss\}$。然而，并不是创建一个新的泛化子目标 $\{hw, dss\}, P2$，而是这些绑定将与生成的泛化子目标合并
- related({jbf, wcr, hws}, X).

如果任何绑定匹配成功，则表明可能存在某些结果。QSQ 有两种类型：迭代式（QSQ）和递归式（QSQR）。两者都涉及生成新答案和创建新子目标的步骤。QSQ 优先考虑之前的答案，并挂起工作直到所有答案生成。而在 QSQR 中，当遇到一个新的子目标时，它成为焦点，并挂起当前子目标的处理。在实践中，QSQ 往往更快，因为存在重复规则 [Banc and Ramakrishnan 1986]。QSQR 与应用于无否定程序的 SLG 仍保持密切相关，但据我们所知，尚未尝试过详细的比较。

### 1.5.3 自底而上 vs 自顶而下

自底而上还是自顶而下方法更好，这个问题自然产生于：在 Datalog 中使用魔法集（Magic Sets）方法更有效。Banc and Ramakrishnan [1989] 比较了自底而上和自顶而下方法，Magic Sets 在某些模式下是有效的。由于自底而上方法可以考虑所有事实，而自顶而下方法则不然。自顶而下方法在某些程序上表现更好，在复杂度上比自底而上更简单。Ullman [1990] 的断言是自顶而下方法在某些情况下更优。Slade 和 Liu [2010] 2011 近期证明了魔法集在渐近复杂度上是优的。由于自底而上方法可以考虑所有事实，这在某些情况下是可行的。

### 1.5.4 使用数据库系统的评估方法

扩展规模的一种明显方法是使用本地数据库来管理 EDB 事实，每个谓词存储在独立的表中。数据库可能仅用于管理存储，也可能用于更通用的处理。作为前者的示例，考虑自顶而下评估查询 `related(vk, Y)`。如果我们考虑规则
- related(P1, P2) :- advised(B, P1), related(B, P2).

我们需要求解子目标 `advised(A, vk)`。如果 `advised` 存储在数据库中并对第二个位置建立索引，数据库可以快速检索事实。如果我们使用非常简单的自顶而下策略，并逐个考虑 `advised(A)`，批量获取它们可以节省 I/O 时间。作为更通用策略的示例，考虑基于规则的方法。在尝试求解 IDB 目标时，评估器可以积累 EDB 目标。然后，当列表只包含 EDB 目标时，它可以转换为数据库查询。例如，如果查询 `related(vk, Y)`，我们使用规则
- related(B, P2) :- advised(B, P1), related(B, P2).

我们得到目标列表 `advised(B, vk), related(B, Y)`。如果随后轮流使用之前的规则求解 `/2` 目标，得到的目标列表是
advised(A, vk), advised(A, B), advised(A, Y).

它由 EDB 目标组成。它可以转换为 SQL 查询
```sql
SELECT a1.AID, a2.AID, a3.SID
FROM advised a1, advised a2, advised a3
WHERE a1.SID = 'vk' AND a1.AID = a2.SID AND a2.AID = a3.AID;
```
如果有多种求解 IDB 目标的方法，就有多个数据库查询。（在递归的情况下，查询数量可能是无限的，然而）

自底而上也可以利用数据库的能力。数据库可以处理 Datalog 程序中每次 Tp 应用的所有或部分。包含一个或多个 EDB 谓词的规则可以转换为 SQL 查询。为了在从右到左的评估期间访问嵌套事实，可以在数据库中为每个 IDB 谓词创建临时表，以存储导出的 IDB 事实，让 Tp 完全在数据库内部执行。另一种，自底而上的评估器可能会将 IDB 事实保存在内存中，并使用嵌套循环方法评估每个规则，为 EDB 事实发布数据库查询，考虑到由查询之外谓词决定的每个组合。

## 1.5 评估技术 63

接下来的段落将介绍这些方法的具体实例——首先是 TD（自顶）方法，然后是 BU（自下）方法。

在具体方法方面，自顶向下的方法往往“以证明为导向，由推导驱动”，而自下向上的方法更具“语法化，基于程序规则的结构”。Reiter [1977a] 讨论了一个初始的“编译”阶段，在该阶段会查询 IDB（意图数据库），产生一组针对 EDB（扩展数据库）的查询。具体地说，他描述了将 IDB 输入定理证明器，由证明器标记 EDB 字母以备后用，而评估在关系型数据库中进行。（Reiter 注意，他的特定方法对于递归查询是不完备的）。DADM [Kellogg et al. 1977] 和 DEDUCE 2 [Chang 1977] 系统也提出了这类方法，即首先处理 IDB 规则以产生（每个阶段多个）EDB 目标，这些目标可以在关系型数据库中进行评估。Census 和 Demolombe [1998] 描述了一种累积方法，用于收集最大 EDB 谓词序列以进行数据库评估。Grant 和 Tinker [Grant and Tinker 1981] 注意，由此类方法生成的 EDB 查询将具有共享子表达式，这些表达式会被提取公因子以提高效率。Ceri 等人 [1989] 通过缓存查询结果来解决 EDB检索的重叠问题。BERMUSA 系统 [Ioannidis et al. 1988] 采取了类似的方法，收集 EDB 谓词序列供数据库评估，将结果缓存到文件中，并交由一个“加载器”组件提供对 Prolog 解释器的访问。

在自下向上的一侧，众所周知 Datalog 程序 $P$ 的即时后果算子 $T_P$ 可以转换为关系代数算式。Ceri 等人 [1986] 显示，通过用带有不动点算子的关系代数进行扩展，可以获得自下向上评估的完整翻译。Ceri 和 Tanaka [1987] 讨论了可以应用于翻译的各种优化。PRISMAS 语言 [Houtms and Apers 1992] 是一种 Datalog 扩展，它也被翻译为带有通用不动点算子的扩展关系代数，然后优化为带有传递闭的标准关系代数算式。关系代数通常在执行之前需要被转换为 SQL。Draxler [1993] 提供了逻辑语言到 SQL 的直接翻译，跳过了关系代数。NED-2 智能信息系统 [Maier et al. 2002] 引入了逻辑语言中数据库查询的特殊语法，这些查询作为 SQL 传输到 DBMS。最后，van Emde Boas 和 van Emde Boas [1986] 描述了一种用逻辑编程功能扩展关系型 DBMS（IBM 的 System 12）的方法，但尚清楚该项目是否已超出原型阶段。

# 第 1 章 Datalog：概念、历史与展望

## 1.5.5 Datalog 中的查询优化

Datalog 查询的优化也从理论角度进行了研究，主要在 20 世纪 80 年代。由于优化问题等同于寻找另一个 Datalog 程序，该程序为扩展谓词计算一组等价的事实，但评估速度更快，因此优化主要在查询等价性（或更广泛地说，查询包含性）的背景下进行。查询包含性意味着任何查询的结果都保证是另一个查询结果的子集。证明双向的包含性即可证明等价性。许多 Datalog 优化技术涉及通过删除规则或子目标来简化原始 Datalog 程序，并测试其与原始程序的等价性。遗憾的是，Datalog 查询的等价问题已被证明是不可判定的 [Shmueli 1993]。此外，查询等价性在 Datalog 的许多子类中也被证明为不可判定，例如，如果每个规则最多包含一个递归谓词 [Gaifman et al. 1993]。因此，查询包含问题可判定的 Datalog 片段引起了极大关注。特别是，Cosmadakis 等人 [1988] 显示，对于单元 Datalog（monadic Datalog，其中谓词是递归定义的），查询包含性是可判定的，并且允许二元关系递归定义。查询等价性的更强版本称为“均匀等价性”（uniform equivalence），它是关于在给定意图谓词和扩展谓词的初始事实的情况下，两个 Datalog 程序是否计算出等价事实集的决策问题。Sagiv [1987] 显示均匀等价性是可判定的，并提供了一种关于均匀等价性最小化 Datalog 规则集的算法。对于一个更简单的 Datalog 子集（带有合取查询的并集），已获得了关于查询优化的积极结果，特别是在 SQL 背景下 [Chaudhuri 1998]。最近，Vardi [2016] 显示，带有传递闭的合取查询并集的查询包含问题也是可判定的。对于涉及约束的 Datalog 优化技术，请参见第 1.4.5 节。另一类等价性关注什么样的（语法上）递归的 Datalog 程序具有非递归对应项 [Chaudhuri and Vardi 1992, Nauthem 1986]。

我们应该补充，描述逻辑 [Baader et al. 2003] 领域关注一阶逻辑不同子集的查询包含和等价性问题，这些与 Datalog 的交集有限。然而，我们尚未注意到该领域有结果在应用于它时能产生新的见解。

## 1.6 早期 Datalog 与演绎数据库系统

虽然关于 Datalog 的大部分早期工作关注评估选项、语义和扩展，但在 20 世纪 80 年代末和 90 年代初，构建了许多相当完整的演绎数据库系统实现。这些系统在几个方面有所不同。

其之一是它们如何提供有序执行。尽管 Datalog 纯逻辑语义，且（至少在理论上）程序员不需要担心规则和目标的顺序，但大多数应用程序需要具有侧效应的操作，如更新和 I/O，在这些情况下顺序是重要的。这些系统要么将声明式查询嵌入过程化语言中，要么设置某些强制执行评估的规则。

第二个变异来源是支持什么类型的 Basic Datalog 扩展，如结构化项、集合、否定和聚合。第三个方面是所采用的优化和评估策略，这在很大程度上取决于所支持的系统。我们最后指出的领域是关系是如何管理的。某些系统为 EDB 提供了磁盘存储，无论是自定义构建的还是使用现有的 DBMS 或存储系统。另一些则使用主内存数据库（可能由辅助存储支持）。

接下来的介绍并非详尽，但目的是为了说明上述的差异。我们还倾向于公开分发的系统。我们建议参考 Ramakrishnan 和 Ullman [1995] 的综述以进行更深入的比较。此外，虽然 XSB 仍被支持并广泛使用，但 LDL 中涵盖的一些技术已被纳入 [Shkapsky et al. 2013]。

### 1.6.1 LDL 和 D++

语言和实现是由微电子与技术中心（MCC）在 20 世纪 80 年代中期开发的，作为 Prolog 的替代方案。LDL 从具有声明语义的 Horn 子句开始，旨在完整应用程序，尽管可以通过过程化语言调用。LDL 保留了 Prolog 中的复杂项，例如 `date(1981, 'March')` 并用集合管理它们。集合值可以显式列出，也可以通过规则分组结果创建。例如：
- isees(AID, PID) :- advised(AID, PID).
- isees(ivk, fg).

LDL 提供了一种划分谓词，可以非确定地分割集合，以支持处理大型数据集。LDL 还通过选择谓词支持非确定性，该谓词从范围中选择特定的赋值。例如，在
- oneAdvisee(AID, PID) :- advised(AID, PID), choice((AID, PID)).
