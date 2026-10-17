
# 声明式逻辑编程：理论、系统与应用

![](img/820e45212e28eae9aa3922fce36_6_0.png)

![](img/820e45212e28eae9aa3922fce36_6_1.png)

books.org

www.morganclaypool.com

系列 ISSN: 2374-6679 纸质 2374-6777 电子

DOIs:

本书使用 TeX 排版

第一版

1 0 9 7 6 5 4

致 David Scott，感谢他对逻辑编程原理和系统的开创性工作

序言 vii

致谢 100

致谢 177

致谢 228

致谢 276

- 致谢 407

- 致谢 471

- 致谢 547

- 生传记 589

# 前言

本书的构想源于2012年9月在斯托尼布举行的一次研讨会，旨在庆祝 David S. Warren 在计算机科学领域的贡献。逻辑编程（LP）是人工智能、知识表示、数据库和编程语言的交汇点。逻辑程序通常是声明性的，因为它们关注的是“做什么”而不是“如何做”，这使得更容易理解和维护。

许多书籍涵盖了 LP 的基础知识，但关于实现方法的描述性综述较少。同样，对于支持 LP 的应用领域，如生物信息学、自然语言处理、验证和规划，文献也相对匮乏。虽然 Prolog 虚拟机（WAM）是大多数现代 LP 系统的基础技术，但很少涉及表化（tabling），这是 Warren 开发原始 WAM 之后的主要突破之一。

本书的目标是填补上述空白。它为 LP 的关键方面提供了若干概述，适用于研究人员、从业者以及研究生。书中包含了关于 LP 理论、系统和应用的章节。

LP 的理论基于两种不同的语义：稳定模型语义和良好基语义，导致了声明式范式。

概率与逻辑推理的结合至关重要。

本章介绍了 Warren 虚拟机（WAM），这是现代 LP 系统的主要技术。与以往对 WAM 的介绍不同，本章还描述了表化，这是 D.H.D. Warren 开发原始 WAM 之后发生的主要突破之一。

# 前言

自然语言处理（NLP）是 Prolog 开发的最初动机，它是最流行的基于逻辑的语言。本章概述了逻辑编程（LP）在 NLP 中的应用，主要基于确定子句文法（definite clause grammars）。

LP 用于许多领域和场景，但需要从更本质的方式来理解 LP 的适用性。本章对 LP 的应用进行了概述，并根据三个关键抽象及其相应的实现对其进行了分类。这些抽象分别是：连接（join）、递归（recursion）和约束（constraint）。相应的实现则是：for 循环（for-loops）、固定点（fixed points）和回溯（backtracking）。

## 致谢

祝贺章节作者们完成了这些深思熟虑的综述——所有内容都是专为本书编写的。每一份贡献都经过了仔细审查，每章至少经过四次评审。我们深表感谢评审员为完善书籍材料所付出的时间和精力的。非常感谢 ACM Books 系列主编 M. Tamer Özsu 的支持，感谢 Morgan & Claypool 的 Diane Cerra 在整个过程中提供的帮助、指导和耐心。我们幸运地拥有一个专家制作团队：Windfall Software 的 Paul Anastagnostopoulos，他消除了那些烦人的排版错误；Morgan & Claypool 的 Brent Buckley，他设计了精美且艺术化的封面；来自 Morgan & Claypool 的 Christine Killerich，她协助完成了许多出版任务。

我们感谢 NSF 在资助 CCF-0964196、CCF-1248184、CCF-1414078 和 IIS-1447549 下的支持；以及 ONR 在资助 N00014512208 下的支持。

![](img/820e45212e28eaeac9aa3922fce5fe36_19_0.png)

![](img/820e45212e28eaeac9aa3922fce5fe36_20_0.png)

# Datalog：概念、历史与展望

David Maier, K. Tuncay Tekle, Michael Kifer, David S. Warren

本章是对 Datalog 历史和主要概念的综述。我们首先介绍该语言及其在数据库定义和查询中的用途。然后，我们回顾了来自逻辑语言、数据库、人工智能和专家系统的脉络，这些脉络导致了 Datalog 的出现，并回顾了该名称的起源。我们考虑了递归与其他常见数据语言特征（如否定和聚合）的意图，并查看了其他扩展，如约束、更新和面向对象的特征。我们提供了 Datalog 评估的主要方法及其变体的概述，然后叙述了一些 Datalog 的早期实现和早期数据库系统。我们推测了该语言在 20 世纪 90 年代衰落的原因，以及后来在许多应用领域重新复兴的原因。最后，我们以几个基于或支持 Datalog 的当前系统作为结束，并简要解释了其中一些系统的性能。

## 1.1 引言

Datalog 拥有一段动宕伏的历史，在此期间它起伏不定。这个名字最初被用来指代一种类似于 Prolog 的简化 Horn 逻辑语言，但从那时起已指代对推导数据库和递归查询处理的研究。鉴于 Datalog 问世已三十多年，现在是时候探索它的根源，回顾它的早期工作，理解它在 20 世纪 90 年代的衰落，并考察近期对该语言兴趣的复兴了。本章 intended并不是 Datalog 的教程，也不是全面的研究综述；而是对 Datalog 历史发展的叙述，其中夹杂了一些个人见解。

在研究 Datalog 的根源之前，我们回顾了该语言的基础。我们从一个贯穿始终的示例数据库开始，随后是 Datalog 程序示例以及使用该数据库的查询。该数据库包含了关于博士论文和导师的信息¹。我们使用带有四个关系的模式来表示学术后裔信息：

```
person(ID, First, Last)
area(Area, Univ, Year, Area)
thesis(PID, Title, Year, PID)
advised(AID, PID)
```

`person` 关系为每个参与人员提供了标识符以及姓名。`area` 关系提供了不同领域及其详细描述。`thesis` 关系详细说明了个人论文的信息，而 `advised` 则捕捉了某人导师的信息。（如果多人共同指导某人，或者某人获得了多个博士学位，则可以有多个导师。）

一个 Datalog 程序通常由事实（facts）和规则（rules）组成。事实断言特定的元组属于某个关系。从逻辑角度来看，它代表一个谓词对于特定的值组合为真。以下是与 `thesis` 模式对应的一些 Datalog 事实。以小写字母开头的字母数字值是一个唯一符号，不等于任何其他值。如果符号以大写字母开头或包含非字母数字字符（例如空格），则用单引号括起来。根据我们看到的数据，这里表示为 David Warren 在 1979 年在 Joyce Freman 和 William Rounds 的指导下完成了关于蒙塔格尔数学家（Montague mathematicians）的博士论文。

```
person(dsw, 'David', 'Warren').
person(jbf, 'Joyce', 'Friedman'). even
person(hw, 'Hao', 'Wang').
person(vwoq, 'Willard', 'Quine').
person(anw, 'Alfred', 'Whitehead').
```

- 1. 这个示例灵感来自数学谱系项目（Mathematics Genealogy Project），http://genealogy.nd.edu/，这也是我们使用数据的来源。

```
person(dsw, 'David', 'Warren').
person(jbf, 'Joyce', 'Friedman'). 
person(wcr, 'Dana', 'Scott').
person(ac, 'Alonzo', 'Church').
person(lvk, 'Lazmik', 'Kale').
person(jmy, 'Joshua', 'Yelon').
person(fg, 'Filippo', 'Gioachin').
permission(ks, 'Konstantinos', 'Sagonas').
person(ek, 'Erik', 'Stennman').
```

Datalog 规则类似于关系系统中的视图定义。头部（head）指示要定义的元组，而主体（body）是逗号分隔的事实列表，其中逗号解释为“与”（And）。规则包含一个或多个逻辑变量，这些变量以大写字母开头。注意，在这些约定下，First 是一个变量，而 'First' 是常量。 2. Datalog 系统中另一种流行的约定是使用问号固定变量，例如 `?First, ?Area`。

理解 Datalog 规则的一种方法是通过为逻辑变量替换常量来代表其所有的基实例（ground instances）。例如，假设我们想要定义一个包含计算机科学领域获得博士学位的人员信息。我们可以使用以下 Datalog 规则：

```
csInfo(First, Last, Univ, Year) :-
    thesis(PID, Univ, Year, Area),
    person(PID, First, Last),
    area(Area, 'Computer Science').
```

规则的作用是，当主体中的所有事实之前已建立时，通过头部的事实来扩展数据库——无论这些事实是显式的事实，还是像上面那样通过相同的推理从之前的规则获取的。考虑上述两个实例，第一个建立了事实：

```
csInfo('Joyce', 'Friedman', 'Harvard', 1965)
```

因为主体中的所有事实已知为真。然而，第二个规则实例没有建立事实：

```
csInfo('Joyce', 'Hansen', 'Harvard', 1965)
```

因为事实 `person(jbf, 'Joyce', 'Hansen')` 未列在示例程序列表中（也无法通过上述规则建立）。

 3. 我们假设本章读者具备关系数据库系统的基础，例如关系代数和 SQL 查询语言。必要的背景将包含在任何入门级数据库书中，例如 Garcia-Molina 等人 [2009]。

## 1.1 简介

```sql
CREATE VIEW cslInfo AS
SELECT p.First, p.Last, t.Univ, t.Year
FROM thesis t, person p, area a
WHERE t.PID = p.ID AND t.Area = a.Area
  AND a.Long = 'Computer Science';
```

注意 Datalog 和 SQL 在范围属性上存在差异：Datalog 依赖于位置表示，而 SQL 具有显式命名。此外，在 SQL 中，变量通过关系数据库理论跨越元组；对于熟悉关系数据库理论的人来说，这种区别本质上是域演算和元组关系演算之间的区别。

Datalog 允许头部出现多个具有相同谓词的规则，在这种情况下，数据库通过任何一个规则建立的事实进行扩展。例如，如果我们想推导出与某人处于相邻代的所有人（即该人的直接导师或被指导者），我们可以使用两条规则：

```prolog
adjacent(P1, P2) :- advised(P1, P2).
adjacent(P1, P2) :- advised(P2, P1).
```

我们可以将 Datalog 程序视为在描述一个数据库，其中一些元组由事实给出，另一些由规则建立。对于针对该数据库的查询及其结果，有多种约定。目前，我们将使用单一谓词模式，带有零或多个变量，并以 `?-` 为前缀作为查询。查询的结果将是 Datalog 程序指定的数据库中所有匹配事实的集合。因此，如果我们的程序包含了之前所有的所有的事实和规则，那么查询

```prolog
?- adjacent(dsw, P2).
```

其结果为

```prolog
adjacent(dsw, lvk).
adjacent(dsw, ks).
adjacent(dsw, jbf).
adjacent(dsw, wcr).
```

其中前两个元组由第一个 `adjacent` 规则建立，另外两个由第二个规则建立。不带变量的查询充当成员性测试，如果相应的元组在 Datalog 程序的数据库中，则返回一个单元素集，否则返回空集。因此，查询

```prolog
?- adjacent(dsw, jbf).
```

![](img/820e45212e28eaeac9aa3922fce5fe36_26_0.png)

返回单元素答案

adjacent(dsw, jbf).

但查询

?- adjacent(dsw, lvk).

返回空结果。

虽然 `adjacent` 的两条规则可以通过 SQL 中使用 `UNION` 的视图来捕捉，但 Datalog 可以表示 SQL 无法表达的虚拟关系：规则中的递归。4 假设我们认为如果两个人具有共同的学术祖先，则他们之间是“相关的”。我们可以用三条规则来描述这种关系：

```prolog
related(P1, P2) :- advised(A, P1), advised(A, P2).
related(P1, P2) :- advised(B, P1), related(B, P2).
related(P1, P2) :- advised(C, P2), related(P1, C).
```

我们看到这两条规则通过其他 `related` 事实递归地建立 `related` 事实。例如，可以使用第一条规则的以下实例

```prolog
related(lvk, ks) :- advised(dsw, lvk), advised(dsw, kv).
```

来建立事实 `related(lvk, ks)`，然后使用该事实结合第二条规则的以下实例

```prolog
related(jmy, kv) :- advised(lvk, jmy), related(lvk, jmy).
```

来建立事实 `related(jmy, kv)`。注意，虽然新建立的 `related` 事实可能建立进一步的 `related` 事实，但该过程最终必须停止。每个 `related` 事实都涉及原始 `advised` 事实中的人员 ID，而此类 ID 对的数量是有限的。

更广义地说，我们找到由事实和规则组成的 Datalog 程序的含义，是不断应用规则推导出额外的事实，直到没有变化为止。在这种背景下，将 $P$ 视为一种变换（有时称为直接蕴含算子），它接受一组事实作为输入，并根据规则增加额外的事实。如果从空输入开始，$P$ 的第一次“应用”会添加 $P$ 中的所有事实。第二次应用添加了通过一条规则应用建立的事实，第三次应用添加了通过两次规则建立的事实，4 SQL:1999 引入了对有限形式递归的支持。

等等。最终，当 $P$ 的某次应用不再添加新事实时，该过程收敛。因此，我们可以将 $P$ 的含义视为在 $P$ 的规则和事实应用下得到的 $P$ 的**最小固定点**（least fixed point）[Lloyd 1993, Van Emden and Kowalski 1976]。事实证明对于 Datalog，$P$ 的含义也是**最小模型**（least model），意味着它是包含 $P$ 所有事实并使 $P$ 中的每个规则实例为真的最小事实集合。（我们稍后将看到为了处理否定必须调整这种等效性。）

注意到上述重复应用 $P$ 的过程实际上是计算 Datalog 程序的有效程序，并被称为**自下向上评估**（bottom-up evaluation）。然后对最终建立的事实集进行查询。另一种方法是**自顶向下评估**（top-down evaluation），它从一个特定的查询开始，尝试将其与 $P$ 中的事实或规则进行匹配。如果匹配，则建立了一个新答案。如果匹配规则，则规则体变为新查询，并继续尝试匹配规则体中的目标。例如，查询

- adjacent(dsw, P2).

并不直接匹配事实，但如果我们将 P1 替换为 dsw，它确实匹配规则的头部

- adjacent(P1, P2) :- advised(P1, P2).

规则体留下了新查询

- advised(dsw, P2).

它匹配两个事实

- advised(dsw, lvk).

advised(dsw, ks).

产生两个答案：

- adjacent(dsw, lvk).

将原始查询与另一个 `adjacent` 规则匹配给出两个额外的答案。我们将在 1.5 节中更详细地讨论评估技术。在离开这个 Datalog 概述之前，最后三点。

## 1.2 Datalog 的出现

作为一种评估的替代方案，它也是探索扩展的基础，以及知识表示系统的起点。我们在下面总结了这三个社区的相关趋势，随后对每个领域给出更具体的背景介绍。

逻辑编程程序员将关系型数据库视为一种重要语言的实现，并致力于将其集成到 Prolog 系统中。由于早期的 Prolog 实现假设所有规则和事实都驻留在内存中，显然，对于庞大的事实库，需要类似关系型数据库这样的技术。这种增强以关系型数据库管理系统（RDBMS）的形式出现。翻译器将 Prolog 程序的一个子集转换为 SQL 传递给 RDBMS 并进行评估。Datalog 是一个功能更强大、类 Prolog 且面向数据的 Prolog SQL 子集。Datalog 也比 Prolog 更具“声明性”，逻辑编程社区的许多人喜欢这一点。在 Prolog 中，逻辑编程理论（将程序理解为逻辑公理和演绎）与逻辑编程实践（将程序评估为 Prolog 解释器）之间存在着巨大的鸿沟。例如，对于许多非逻辑原语，由于 Prolog 解释器使用的评估策略存在局限性，许多完美的逻辑程序将无法终止。有了 Datalog，这种鸿沟几乎消失了——在产生的结果方面，演绎与评估是一致的。此外，Datalog 提供了一个基础，用于解决带否定的递归，其中某些方案可以应用于更通用的逻辑语言。
