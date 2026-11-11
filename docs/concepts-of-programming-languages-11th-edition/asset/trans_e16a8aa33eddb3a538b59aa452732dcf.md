
- 8. 声明式语义的基本概念是什么？
- 9. 一种语言是非过程式的，这意味着什么？
- 10. Prolog 项的三种形式是什么？
- 11. 什么是未实例化变量？
- 12. Prolog 中事实和规则语句的语法形式及用法是什么？
- 13. 什么是合取？
- 14. 解释在数据库中匹配目标与事实的两种方法。
- 15. 在讨论多个目标如何满足时，解释深度优先搜索和广度优先搜索之间的区别。
- 16. 解释 Prolog 中回溯是如何工作的。
- 17. 解释 Prolog 语句 X is X + 1 有什么问题。
- 18. Prolog 程序员在归结过程中可以通过哪两种方式控制模式匹配的顺序？
- 19. 解释 Prolog 中的生成-测试编程策略。
- 20. 解释 Prolog 使用的封闭世界假设。为什么这是一个局限？
- 21. 解释 Prolog 的否定问题。为什么这是一个局限？
- 22. 解释自动定理证明与 Prolog 推理过程之间的联系。
- 23. 解释过程式语言和非过程式语言之间的区别。
- 24. 解释为什么 Prolog 系统必须进行回溯。
- 25. 在 Prolog 中，归结与合一之间的关系是什么？

## 习题集

- 1. 比较 C# 与 Prolog 中数据类型的概念。
- 2. 描述如何使用多处理器机器来实现归结。按当前的定义，Prolog 能否使用这种方法？
- 3. 用 Prolog 编写你的家谱描述（仅基于事实），向上追溯到你的祖父母，并包括所有后代。务必包含所有关系。
- 4. 编写一组家庭关系规则，包括从祖父母到其后两代的所有关系。然后将这些规则添加到问题 3 的事实中，并尽量删除其中的事实。
- 5. 将以下英语条件语句写成以 Prolog 头部（head）表示的 Horn 子句：
  - a. 如果弗雷德是迈克的父亲，那么弗雷德是迈克的祖先。
  - b. 如果迈克是乔的父亲，并且迈克是玛丽的父亲，那么玛丽是乔的姐妹。
  - c. 如果迈克是弗雷德的兄弟，并且弗雷德是玛丽的父亲，那么迈克是玛丽的叔叔。
- 6. 解释 Scheme 和 Prolog 的列表处理能力相似的两种方式。
- 7. Scheme 和 Prolog 的列表处理能力在哪些方面不同？
- 8. 写一篇 Prolog 与 ML 的比较，包括两个相似点和两个不同点。
- 9. 从一本关于 Prolog 的书中了解并写出关于出现（occurrence）问题的描述。为什么 Prolog 允许该问题存在于其实现中？
- 10. 查找关于 Skolem 范式的良好资料源，并写出简短而清晰的解释。

## 编程练习

- 1. 使用结构 `parent(X, Y)`、`male(X)` 和 `female(X)`，编写一个定义 `mother(X, Y)` 的结构。
- 2. 使用结构 `parent(X, Y)`、`male(X)` 和 `female(X)`，编写一个定义 `sister(X, Y)` 的结构。
- 3. 编写一个 Prolog 程序，找出数字列表的最大值。
- 4. 编写一个 Prolog 程序，当两个给定列表参数的交集为空时成功。
- 5. 编写一个 Prolog 程序，返回包含两个给定列表元素并集的列表。
- 6. 编写一个 Prolog 程序，返回给定列表的最后一个元素。
- 7. 编写一个实现快速排序（quicksort）的 Prolog 程序。

- Backus, J. (1959) “苏黎世 ACM-GAMM 会议上提出的国际代数语言的语法与语义。” 载于《国际信息处理会议论文集》。UNESCO，巴黎，第 125-132 页。

- Backus, J. (1978) “编程能否摆脱冯·诺依曼风格？一种函数式风格及其程序代数。” Commun. ACM，第 21 卷，第 8 期，第 613-641 页。

- Backus, J., F. L. Bauer, J. Green, C. Katz, J. McCarthy, P. Naur, A. J. Perlis, H. Rutishauser, K. Samelson, B. Vauquois, J. H. Wegstein, A. van Wijngaarden, and M. Woodger. (1963) “关于算法语言 ALGOL 60 的修订报告。” Commun. ACM，第 6 卷，第 1 期，第 1-17 页。

- Balena, F. (2003) 《Microsoft Visual Basic .NET 2003 版程序设计》，Microsoft Press，雷德蒙德，华盛顿州。

- Ben-Ari, M. (1982) 《并发程序设计原理》，Prentice-Hall，新泽西州恩格尔伍德克利夫斯。

- Birtwistle, G. M., O.-J. Dahl, B. Myhrhaug, and K. Nygaard. (1973) 《SIMULA 入门》，Van Nostrand Reinhold，纽约。

- Boehm, J. M., L. Bradley, K. Kanda, D. Litle, and U. F. Pleban. (1982) “基于指称语义的实验性编译器生成器的经验。” ACM SIGPLAN Notices，第 17 卷，第 6 期，第 216-229 页。

- Bohm, C., and G. Jacopini. (1966) “流程图、图灵机与仅含有两种形成规则的语言。” Commun. ACM，第 9 卷，第 5 期，第 366-371 页。

- Bolsky, M., and D. Korn. (1995) 《新 KornShell 命令与编程语言》，Prentice-Hall，新泽西州恩格尔伍德克利夫斯。

- Booch, G. (1987) 《使用 Ada 的软件工程（第二版）》，Benjamin/Cummings，加利福尼亚州雷德伍德城。

- Bradley, J. C. (1989) 《使用模块化结构的 QuickBASIC 与 QBASIC》，W. C. Brown，艾奥瓦州迪比克。

- Brinch Hansen, P. (1973) 《操作系统原理》，Prentice-Hall，新泽西州恩格尔伍德克利夫斯。

- Brinch Hansen, P. (1975) “编程语言 Concurrent-Pascal。” IEEE Transactions on Software Engineering，第 1 卷，第 2 期，第 199-207 页。

- Brinch Hansen, P. (1977) 《并发程序的结构》，Prentice-Hall，新泽西州恩格尔伍德克利夫斯。

- Brinch Hansen, P. (1978) “分布式进程：一种并发程序设计概念。” Commun. ACM，第 21 卷，第 11 期，第 934-941 页。

- Brown, J. A., S. Pakin, and R. P. Polivka. (1988) 《APL2 一览》，Prentice-Hall，新泽西州恩格尔伍德克利夫斯。

- Campione, M., K. Walrath, and A. Huml. (2001) 《Java 教程（第三版）》，Addison-Wesley，马萨诸塞州雷丁。

- Cardelli, L., J. Donahue, L. Glassman, M. Jordan, B. Kalsow, and G. Nelson. (1989) 《Modula-3 报告（修订版）》，数字系统研究中心，加利福尼亚州帕洛阿尔托。

- Chambers, C., and D. Ungar. (1991) “让纯面向对象语言变得切实可行。” SIGPLAN Notices，第 26 卷，第 1 期，第 1-15 页。

- Chomsky, N. (1956) “描述语言的三种模型。” IRE Transactions on Information Theory，第 2 卷，第 3 期，第 113-124 页。

- Chomsky, N. (1959) “关于文法的某些形式性质。” Information and Control，第 2 卷，第 2 期，第 137-167 页。

- Christiansen, T., B. D. Foy, and L. Wall with J. Orwant. (2013) 《Perl 编程（第四版）》，O'Reilly & Associates，加利福尼亚州塞瓦斯托波尔。

- Church, A. (1941) 《数学研究年刊：λ 转换演算，第 6 卷》。普林斯顿大学出版社，新泽西州普林斯顿。1965 年由 Kraus Reprint Corporation 在纽约重印。

- Clark, K. L., and F. G. McCabe. (1984) 《Micro-PROLOG：逻辑程序设计》，Prentice-Hall，新泽西州恩格尔伍德克利夫斯。

- Clarke, L. A., J. C. Wileden, and A. L. Wolf. (1980) “Ada 中的嵌套没什么用。” ACM SIGPLAN Notices，第 15 卷，第 11 期，第 139-145 页。

- Cleveland, J. C. (1986) 《数据类型导论》，Addison-Wesley，马萨诸塞州雷丁。

- Cleaveland, J. C., and R. C. Uzgalis. (1976) 《编程语言的文法：每个程序员都应了解的文法知识》，American Elsevier，纽约。

- Clocksin, W. F., and C. S. Mellish. (2013) 《Prolog 编程：使用 ISO 标准》，Springer-Verlag，纽约。

- Cohen, J. (1981) “链式数据结构的垃圾收集。” ACM Computing Surveys，第 13 卷，第 3 期，第 341-368 页。

- Converse, T., and J. Park. (2000) 《PHP 4 宝典》，IDG Books，纽约。

- Conway, M. E. (1963) “可分离转换图编译器的设计。” Commun. ACM，第 6 卷，第 7 期，第 396-408 页。

- Conway, R., and R. Constable. (1976) “PL/CS——PL/I 的一种受约束子集。” 技术报告 TR76/293。康奈尔大学计算机科学系，纽约州伊萨卡。

- Cornell University. (1977) 《PL/C 用户指南，7.6 版》。康奈尔大学计算机科学系，纽约州伊萨卡。

- Correa, N. (1992) “空范畴、链绑定与句法分析。” 载于《基于原则的句法分析》，R. C. Berwick、S. P. Abney 和 C. Tenny 编。Kluwer Academic Publishers，波士顿，第 83-121 页。

- Cousineau, G., M. Mauny, and K. Callaway. (1998) 《函数式编程方法》，Cambridge University Press，英国剑桥。

- Dahl, O-J., E. W. Dijkstra, and C. A. R. Hoare. (1972) 《结构化程序设计》，Academic Press，纽约。

- Dahl, O-J., and K. Nygaard. (1967) 《SIMULA 67 公共基础提案》，挪威计算中心文档，奥斯陆。

- Deitel, H. M., D. J. Deitel, and T. R. Nieto. (2002) 《Visual Basic .NET：如何编程（第二版）》，Prentice-Hall，新泽西州上鞍河。

- Deliyanni, A., and R. A. Kowalski. (1979) “逻辑与语义网络。” Commun. ACM，第 22 卷，第 3 期，第 184-192 页。

- Department of Defense. (1960) 《COBOL：面向商业通用语言的初始规范》。美国国防部，华盛顿特区。

- Department of Defense. (1961) 《COBOL—1961：面向商业通用语言的修订规范》。美国国防部，华盛顿特区。

- Department of Defense. (1962) 《COBOL—1961 扩展：面向商业通用语言的扩展规范》。美国国防部，华盛顿特区。

- Department of Defense. (1975a) 《高级程序设计语言需求：STRAWMAN》。7 月。美国国防部，华盛顿特区。

- Department of Defense. (1975b) 《高级程序设计语言需求：WOODENMAN》。8 月。美国国防部，华盛顿特区。

- Department of Defense. (1976) 《高级程序设计语言需求：TINMAN》。6 月。美国国防部，华盛顿特区。

- Department of Defense. (1977) 《高级程序设计语言需求：IRONMAN》。1 月。美国国防部，华盛顿特区。

- Department of Defense. (1978) 《高级程序设计语言需求：STEELMAN》。6 月。美国国防部，华盛顿特区。

- Department of Defense. (1980a) 《高级程序设计语言需求：STONEMAN》。2 月。美国国防部，华盛顿特区。
