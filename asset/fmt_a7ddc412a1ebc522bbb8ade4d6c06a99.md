
# Michaelis Lippert C 6.0 精髓

To my family: Elisabeth, Benjamin, Hanna, and Abigail.

You have sacrificed a husband and daddy for countless hours of writing,
frequently at times when he was needed most.

Thanks!

## Figures

+   FIGURE 2.1: *值类型直接包含数据* 62
+   FIGURE 2.2: *引用类型指向堆* 63
+   
+   FIGURE 3.1: *对应的占位符值* 128
+   FIGURE 3.2: *计算无符号字节的值* 129
+   FIGURE 3.3: *计算有符号字节的值* 129
+   FIGURE 3.4: *数字 12 和 7 在二进制中的表示* 131
+   FIGURE 3.5: *Microsoft Visual Studio .NET 中的折叠区域* 159
+   
+   FIGURE 4.1: *异常处理程序流* 206
+   
+   FIGURE 5.1: *类层次结构* 220
+   
+   FIGURE 6.1: *重构为基类* 291
+   FIGURE 6.2: *使用聚合模拟多重继承* 300
+   
+   FIGURE 7.1: *使用聚合和接口解决单继承限制* 345
+   
+   FIGURE 8.1: *值类型直接包含数据* 352
+   FIGURE 8.2: *引用类型指向堆* 354
+   
+   FIGURE 9.1: *标识* 390
+   FIGURE 9.2: *Visual Studio IDE 中的 XML 注释提示* 414
FIGURE 12.1: Delegate Types Object Model 513
FIGURE 12.2: Anonymous Function Terminology 516
FIGURE 12.3: The Lambda Expression Tree Type 536
FIGURE 12.4: Unary and Binary Expression Tree Types 537
FIGURE 13.1: Delegate Invocation Sequence Diagram 553
FIGURE 13.2: Multicast Delegates Chained Together 555
FIGURE 13.3: Delegate Invocation with Exception Sequence Diagram 556
FIGURE 14.1: A Class Diagram of IEnumerator<T> and IEnumerator Interfaces 584
FIGURE 14.2: Sequence of Operations Invoking Lambda Expressions 599
FIGURE 14.3: Venn Diagram of Inventor and Patent Collections 603
FIGURE 16.1: Generic Collection Interface Hierarchy 645
FIGURE 16.2: List<> Class Diagrams 647
FIGURE 16.3: Dictionary Class Diagrams 654
FIGURE 16.4: SortedList<> and SortedDictionary<> Class Diagrams 661
FIGURE 16.5: Stack<T> Class Diagram 662
FIGURE 16.6: Queue<T> Class Diagram 662
FIGURE 16.7: LinkedList<T> and LinkedListNode<T> Class Diagrams 663
FIGURE 16.8: Sequence Diagram with yield return 672
FIGURE 17.1: MemberInfo Derived Classes 691
FIGURE 17.2: BinaryFormatter Does Not Encrypt Data 715
FIGURE 18.1: Clock Speeds over Time 732
FIGURE 18.2: CancellationTokenSource and CancellationToken Class Diagrams 771
FIGURE 20.1: Pointers Contain the Address of the Data 864
FIGURE 21.1: Compiling C# to Machine Code 882
FIGURE 21.2: Assemblies with the Modules and Files They Reference 890
FIGURE C.1: APM Parameter Distribution 912
FIGURE C.2: Delegate Parameter Distribution to BeginInvoke() and EndInvoke() 925

## Tables

+   TABLE 1.1: C# Keywords 5
+   TABLE 1.2: C# Comment Types 24
+   TABLE 1.3: C# and .NET Versions 29
+   TABLE 2.1: Integer Types 36
+   TABLE 2.2: Floating-Point Types 38
+   TABLE 2.3: decimal Type 38
+   TABLE 2.4: Escape Characters 47
+   TABLE 2.5: string Static Methods 52
+   TABLE 2.6: string Methods 52
+   TABLE 2.7: Array Highlights 73
+   TABLE 2.8: Common Array Coding Errors 86
+   TABLE 3.1: Control Flow Statements 108
+   TABLE 3.2: Relational and Equality Operators 120
+   TABLE 3.3: Conditional Values for the XOR Operator 122
+   TABLE 3.4: Preprocessor Directives 153
+   TABLE 3.5: Operator Order of Precedence 160
+   TABLE 4.1: Common Namespaces 165
+   TABLE 4.2: Common Exception Types 210
+   TABLE 6.1: Why the New Modifier? 308
+   TABLE 6.2: Members of System.Object 320
+   - TABLE 7.1: Comparing Abstract Classes and Interfaces 348
+   - TABLE 8.1: Boxing Code in CIL 363
+   - TABLE 9.1: Accessibility Modifiers 409
+   - TABLE 12.1: Lambda Expression Notes and Examples 521
+   - TABLE 14.1: Simpler Standard Query Operators 618
+   - TABLE 14.2: Aggregate Functions on System.Linq.Enumerable 618
+   - TABLE 17.1: Deserialization of a New Version Throws an Exception 717
+   - TABLE 18.1: List of Available TaskContinuationOptions Enums 758
+   - TABLE 18.2: Control Flow within Each Task 785
+   - TABLE 19.1: Sample Pseudocode Execution 818
+   - TABLE 19.2: Interlocked’s Synchronization-Related Methods 829
+   - TABLE 19.3: Execution Path with ManualResetEvent Synchronization 838
+   - TABLE 19.4: Concurrent Collection Classes 840
+   - TABLE 21.1: Primary C# Compilers 880
+   - TABLE 21.2: Common C#-Related Acronyms 895

## Foreword

欢迎来到 C# 书籍世界中你能梦想到的最伟大的合作之一——可能远不止于此！Mark Michaelis 的 *Essential C#* 系列在与著名 C# 博主 Eric Lippert 联手撰写前一版时已是经典之作，这堪称一次神来之笔。

你可能认为 Eric 写博客，Mark 写书，但这并不是我初次认识他们的方式。

2005 年 LINQ（Language Integrated Query）公布时，我刚加入微软不久，有幸参加了 PDC 大会上的隆重发布。尽管我对这项技术几乎没有贡献，我仍然完全沉浸在 hype 中。演讲座无虚席，印刷传单像热蛋糕一样飞快售罄。那是 C# 和 .NET 的大日子，我玩得很开心。

不过动手实验室区域却相当安静，那里人们可以用漂亮的脚本化演练亲自尝试技术预览。就在那里我遇到了 Mark。毋庸置疑，他没有按脚本走。他在做自己的实验，翻阅文档，与其他人交谈，并忙着拼凑出自己的理解。

作为 C# 社区的新人，我想我在那次大会上可能第一次认识了很多后来与我建立了良好关系的人。但说实话，我不记得了——一切都模糊了。我唯一记得的是 Mark。原因如下：当我问他是否喜欢这些新东西时，他并没有加入狂欢。他非常冷静：“*我还不知道。我还没有对它做出决定。*”他想要吸收并理解整个方案，在此之前他不会让任何人告诉他该怎么想。

所以，与其说我得到了一次我可能期望的快速肯定糖 rush，不如说我进行了一次坦诚而充实的对话——这是多年以来多次对话中的第一次——关于这项新技术的细节、后果和担忧。从那时起一直如此：Mark 对我们语言设计者来说是一个极其宝贵的社区成员，因为他超级聪明，坚持要从根本上理解一切，并且对事物如何影响真正的开发者有惊人的洞察力。但也许最重要的是因为他直言不讳，从不害怕说出自己的想法。如果某件事通过了“Mark 测试”，那么我们就可以开始对它感到相当满意了！

这些正是使 Mark 成为如此优秀作家的品质。他直指本质，以极大的诚信沟通，没有粉饰，善于发现实用价值和现实问题。

Eric 当然是我在 C# 团队共事七年的前同事。他在我之前待得更久，我第一次对他的印象是，他在向团队解释如何解开一团意大利面。更准确地说，当时我们的 C# 编译器代码库急需一些严重的架构 TLC，添加新功能变得异常困难——而这正是我们使用 LINQ 时迫切需要做到的。Eric 正在研究我们应该采用什么样的架构（阶段！我们甚至几乎没有这些！），更重要的是，如何一步步从这里到那里。令人惊讶的是，这个问题如此复杂，而我又是团队和代码库的新人，我立刻明白他在说什么！

你可能从他的博客中认识到他对问题的超清晰、结构良好的梳理、令人信服的解决方案列举，以及偶尔的无节制幽默。好吧，你还不知道全部！每当 Eric 处理一个复杂问题并与团队分享他的想法时，他关于此的邮件同样细致入微，幽默感也丝毫不减。你根本无法忽视 Eric 提出的问题，因为你迫不及待想读他的文章。它们甚至还是紫色的！所以我基本上得以持续享用相当于他博客未出版的连载，以及当然，他作为 C# 编译器团队和语言设计团队成员的愉快而富有洞察力的存在。在离开微软后，Eric 继续成为一位了不起、富有洞察力的声音，对我们的决策产生了比他自己可能知道的还要多的影响。

总之，我非常感激能定期与这两位了不起的人一起工作：Eric 帮助我保持意图并纠正这种情况。在本书的后续章节中，你将了解到额外的技术方法，例如基于接口的编程、LINQ 及其对集合 API 的改造，以及最终在第 17 章通过属性实现声明式编程的 rudimentary 形式。

本书有三个主要功能：

- 它对 C# 语言提供了全面覆盖，超越了教程，并提供了一个基础，以便你开始有效的软件开发项目。
- 对于已经熟悉 C# 的读者，它提供了对一些更复杂编程范式的深入见解，并对最新语言版本 C# 6.0 和 .NET Framework 4.6 中引入的功能进行了深入介绍。
- 它作为一个永恒的参考，即使你在语言上变得熟练后仍然适用。

成功学习 C# 的关键是尽快开始编码。不要等到你在理论上成为“专家”——立即开始编写软件。作为迭代开发的信奉者，我希望这本书能让即使是初学者程序员也能在第 2 章结束时开始编写基本的 C# 代码。

本书未涵盖一些主题。你不会找到诸如 ASP.NET、Entity Framework、智能客户端开发如 WPF、分布式编程等主题的介绍。虽然这些主题与 .NET Framework 相关，但要做到公正需要各自的书籍。幸运的是，Addison-Wesley 的 .NET Development Series 为这些主题提供了丰富的著作。Essential C# 6.0 专注于 C# 和基类库中的类型。阅读本书将为你准备好专注于并在该系列涵盖的任何领域发展专业知识。

## 本书的目标读者

我在这本书中面临的挑战是让高级开发者保持清醒，同时不使用诸如 assembly、link、chain、thread 和 fusion 之类的术语来抛弃初学者，仿佛该主题更适合铁匠而不是程序员。本书的主要受众是希望为自己的工具库增添另一种语言的经验丰富的开发者——可以说是在他们的箭袋中再添一支箭。然而，我精心组装了这本书，以为各层次的开发者提供显著价值。

- 初学者：如果您是编程新手，本书可作为资源，帮助您从初级程序员过渡到 C# 开发者——能够从容应对抛给您的任何 C# 编程任务。本书不仅教授您语法，还训练您良好的编程实践，这将在您的编程生涯中为您提供良好服务。
- 结构化程序员：正如最好通过沉浸式学习外语一样，学习计算机语言最有效的方法是在了解其所有复杂性之前就开始使用该语言。基于此，本书以教程开始，对于熟悉结构化编程的人来说会很舒适，到第 4 章结束时，此类开发者应能自如地编写基本的控制流程序。然而，C# 开发者的卓越关键不仅仅在于记忆语法。相反，要从简单程序过渡到企业开发，C# 开发者必须以对象及其关系为原生思维。为此，第 5 章的初学者主题介绍了类和面向对象开发。历史上结构化编程语言如 C、COBOL 和 FORTRAN 所扮演的角色仍然重要但在缩小，因此软件工程师有必要熟悉面向对象开发。C# 是实现这一转变的理想语言，因为它在设计时将面向对象开发作为其核心原则之一。
- 基于对象和面向对象的开发者：C++ 和 Java 程序员，以及许多经验丰富的 Visual Basic 程序员，都属于这一类。你们中的许多人已经完全习惯了分号和大括号。对第 1 章代码的简要浏览显示，在其核心，C# 与您已知的 C 和 C++ 风格语言相似。
- C# 专业人士：对于已经精通 C# 的人来说，本书提供了不常用语法的便捷参考。此外，它提供了很少涉及的语言细节和细微差别方面的答案。最重要的是，它提出了编写健壮且可维护代码的指导方针和模式。本书也有助于教授他人 C# 的任务。随着 C# 3.0、4.0、5.0 以及现在 6.0 的出现，其中一些最突出的增强功能如下：
  - 隐式类型变量（见第 2 章）
  - 扩展方法（见第 5 章）
  - 部分方法（见第 5 章）
  - 匿名类型（见第 11 章）
  - 泛型（见第 11 章）
  - Lambda 语句和表达式（见第 12 章）
  - 表达式树（见第 12 章）
  - 标准查询运算符（见第 14 章）
  - 查询表达式（见第 15 章）
  - 动态编程（第 17 章）
  - 使用任务并行库和 async 的多线程编程（第 18 章）
  - 使用 PLINQ 的并行查询处理（第 18 章）
  - 并发集合（第 19 章）

这些主题对那些不熟悉的人进行了详细讲解。对高级 C# 开发也很相关的是第 21 章中指针的主题。经常，即使是经验丰富的 C# 开发者也不太理解这个主题。

## 本书的特色

Essential C# 6.0 是一本语言书籍，遵循核心 C# 语言 6.0 规范。为了帮助您理解各种 C# 构造，它提供了大量示例来演示每个特性。每个概念都附有指导方针和最佳实践，确保代码编译、避免可能的风险并实现最大可维护性。

为了提高可读性，代码经过特殊格式化，并且章节使用思维导图进行概述。

## C# 编码指导方针

Essential C# 6.0 中更重要的功能之一是包含 C# 编码指导方针，如以下取自第 16 章的示例所示：

### Guidelines

- DO 确保相等对象具有相等的哈希码。
- DO 确保对象的哈希码在它位于哈希表中的时间内永不改变。
- DO 确保哈希算法能快速产生分布良好的哈希。
- DO 确保哈希算法在任何可能的对象状态下都稳健。

## 代码示例

这些准则是在区分只会语法的程序员和能够根据实际情况判断最有效代码编写方式的专家之间的关键。这样的专家不仅能让代码编译通过，而且在遵循最佳实践的同时最大限度地减少错误，并便于在未来进行维护。编码准则突出了读者需要确保将其纳入开发过程中的一些关键原则。
