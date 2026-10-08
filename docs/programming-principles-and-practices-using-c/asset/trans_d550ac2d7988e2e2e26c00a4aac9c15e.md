
## 22.2.3.3 Ada

Ada 编程语言被设计为一种能够满足美国国防部所有编程需求的语言。特别是，它旨在成为一种用于嵌入式系统编程，以提供可靠且易于维护代码的语言。其最直接的祖先语言是 Pascal 和 Simula（参见 §22.2.3.2 和 §22.2.4）。负责设计 Ada 的小组领导人是 Jean Ichbiah——他是 Simula 用户组的前主席。Ada 的设计强调：

- 数据抽象（但在 1995 年之前不支持继承）
- 强静态类型检查
- 直接语言支持并发

Ada 的设计旨在成为软件工程在编程语言中的化身。因此，美国国防部设计的并非语言本身，而是一个用于设计该语言的精密流程。大量的人员和组织参与了这一设计过程，该过程通过一系列竞赛推进，以产生最佳规范，进而产生体现获奖规范理念的最佳语言。这个规模庞大的 20 年项目（1975–98 年）自 1980 年起由一个名为 AJPO（Ada 联合计划办公室）的部门管理。

1979 年，由此产生的语言以奥古斯塔·阿达·拉夫莱斯女爵（Lord Byron，诗人拜伦之女）的名字命名。拉夫莱斯女爵可以被认为是现代第一位程序员（取决于对“现代”的定义），因为她在 19 世纪 40 年代与 Charles Babbage（剑桥大学卢卡斯数学教授——即牛顿的教席！）合作开发了一台革命性的机械计算机。不幸的是，Babbage 的机器未能作为实用工具取得成功。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_864_0.png)

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_864_1.png)

得益于这一精密流程，Ada 一直被认为是终极的“委员会设计”语言。获奖设计团队的首席设计师、来自法国公司 Honeywell Bull 的 Jean Ichbiah 坚决否认了这一点。然而，我怀疑（基于与他的讨论），如果他没有受到流程的如此严格限制，他本可以设计出更好的语言。

多年来，美国国防部强制要求在军事应用中使用 Ada，由此产生了一句名言：“Ada，它不仅是个好主意，它是法律！”起初，Ada 的使用只是被“强制要求”，但当许多项目获得“豁免”以使用其他语言（通常是 C++）时，美国国会通过了一项法律，要求大多数军事应用必须使用 Ada。后来，面对商业和技术现实，该法律被废止。Bjarne Stroustrup 是极少数其工作曾被美国国会禁止的人之一。

话虽如此，我们坚持认为 Ada 是一种比其声誉所暗示的更好的语言。我们怀疑，如果美国国防部在强制其使用以及使用方式（应用开发流程、软件开发工具、文档等标准）上不那么强硬，它本可以取得显著更大的成功。直到今天，Ada 在航空航天应用及类似的高级嵌入式系统应用领域仍然非常重要。

Ada 在 1980 年成为军用标准，1983 年成为 ANSI 标准（第一个实现在 1983 年完成——在第一个标准发布三年后！），1987 年成为 ISO 标准。ISO 标准在 1995 年的 ISO 标准中进行了广泛（但当然兼容的）修订。显著的改进包括并发机制的更大灵活性以及对继承的支持。

### 参考文献

- Barnes, John. *Programming in Ada 2005*. Addison-Wesley, 2006. ISBN 0321340787. Consolidated Ada Reference Manual, consisting of the international standard (ISO/IEC 8652:1995). *Information Technology – Programming Languages – Ada*, as updated by changes from *Technical Corrigendum 1* (ISO/IEC 8652:1995/TC1:2000). Ada information page: www.adaic.org. 
- Whitaker, William A. *ADA – The Project: The DoD High Order Language Working Group*. Proceedings of the ACM History of Programming Languages Conference (HOPL-2). *ACM SIGPLAN Notices*, Vol. 28 No. 3, 1993.

## 22.2.4 Simula

Simula 由 Kristen Nygaard 和 Ole-Johan Dahl 于 20 世纪 60 年代初期至中期在挪威计算中心和奥斯陆大学开发。Simula 无可争议地属于 Algol 语言家族。事实上，Simula 几乎完全是 Algol60 的超集。然而，我们选择特别关注 Simula，因为它是如今被称为“面向对象编程”的大多数基本思想的源泉。它是第一个提供继承和虚函数（virtual functions）的语言。“用户定义类型”的术语 *class*（类）和可被覆盖并通过基类提供的接口调用的函数的术语 *virtual*（虚的）都源自 Simula。

Simula 的贡献不仅限于语言特性。它还带来了一种基于在代码中对现实世界现象进行建模的思想的面向对象设计概念：

- 将思想表示为类和类对象。
- 将层次关系表示为类层次结构（继承）。

因此，程序变成了一组相互交互的对象，而非一个整体。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_866_0.png)

Kristen Nygaard——Simula67 的联合创始人（与左侧戴眼镜的 Ole-Johan Dahl 共同创立）——无论以何种标准衡量（包括身高），都是一位巨人，拥有相匹配的激情和慷慨。他构思了面向对象编程和设计的根本思想，特别是继承，并在数十年间追求其影响。他从未满足于简单、短期且短视的答案。他拥有持续数十年的积极参与社会事务。挪威没有加入欧盟，他也应该得到相当程度的功劳，因为他认为欧盟可能是一个集权且官僚主义的噩梦，对处于联盟边缘的小国——挪威的需求漠不关心。在 20 世纪 70 年代中期，Kristen Nygaard 在丹麦奥胡斯大学计算机科学系度过了大量时间（当时 Bjarne Stroustrup 正在那里攻读硕士学位）。

Kristen Nygaard 拥有奥斯陆大学的数学硕士学位。他于 2002 年去世，就在一个月前，他本应与他的终身好友 Ole-Johan Dahl 一起获得 ACM 图灵奖，这可以说是计算机科学家所能获得的最高专业荣誉。

Ole-Johan Dahl 是一位更传统的学者。他对规范语言和形式化方法非常感兴趣。1968 年，他成为奥斯陆大学第一位信息学（计算机科学）正教授。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_867_0.png)

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_867_1.png)

2000 年 8 月，Dahl 和 Nygaard 被挪威国王授予圣奥拉夫勋章司令级。即使是极客，也能在家乡获得认可！

### 参考文献

- Birrwistle, G., O-J. Dahl, B. Myhrhaug, and K. Nygaard. *SIMULA Begin*. Student-litteratur (Lund, Sweden), 1979. ISBN 9144062125.
- Holmevik, J. R. “Compiling SIMULA: A Historical Study of ‘Technological Genesis’” *IEEE Annals of the History of Computing*, Vol. 16 No. 4, 1994, pp. 25–37.
- Krogdahl, S. “The Birth of Simula.” Proceedings of the HiNC 1 Conference in Trondheim, June 2003 (IFIP WG 9.7, in cooperation with IFIP TC 3).
- Nygaard, Kristen, and Ole-Johan Dahl. “The Development of the SIMULA Languages.” *ACM SIGPLAN Notices*, Vol. 13 No. 8, 1978. Special Issue: History of Programming Languages Conference.
- SIMULA Standard. *DATA Processing – Programming Languages – SIMULA*. Swedish Standard, Stockholm, Sweden (1987). ISBN 9171622349.

## 22.2.5 C

1970 年，人们“众所周知”地认为，严肃的系统编程——特别是操作系统的实现——必须用汇编代码完成，且无法可移植地实现。这与 Fortran 出现之前科学编程的情况类似。几个个人和团体开始挑战这一正统观念。从长远来看，C 编程语言（第 27 章）是这些努力中成功得最多的。

Dennis Ritchie 在新泽西州默里山（Murray Hill）贝尔电话实验室计算机科学研究中心设计并实现了 C 编程语言。C 语言的美妙之处在于它是一门刻意保持简单的编程语言，非常贴近硬件的基本方面。目前大多数复杂性（其中大部分因兼容性原因在 C++ 中重新出现）是在其原始设计之后添加的，并且在某些情况下是在 Dennis Ritchie 反对的情况下添加的。C 的成功部分归功于其早期的广泛可用性，但其真正的优势在于语言特性到硬件设施（参见 §25.4–5）的直接映射。Dennis Ritchie 简洁地将 C 描述为“强类型但弱检查的语言”；也就是说，C 具有静态（编译时）类型系统，使用对象的方式与其定义不同的程序是不合法的。然而，C 编译器无法检查这一点。当 C 编译器需要在 48K 字节内存中运行时，这是有道理的。C 开始被使用后不久，人们开发了一个名为 lint 的程序，独立于编译器验证对类型系统的合规性。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_868_0.png)

与 Ken Thompson 一起，Dennis Ritchie 是 Unix 的联合创始人，Unix 无疑是历史上具有影响力的操作系统。C 曾经——并且现在——与 Unix 操作系统相关联，并通过 Unix 与 Linux 和开源运动相关联。

