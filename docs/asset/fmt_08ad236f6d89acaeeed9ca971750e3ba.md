
[Bowen and Hinney, 1995a] J. P. BOWEN AND M. G. HINNEY, "Ten Commands of Formal Methods," IEEE Computer 28 (April 1995), pp. 56–66.

[Bowen and Hinney, 1995b] J. P. BOWEN AND M. G. HINNEY, "Seven Myths of Formal Methods," IEEE Software 12 (July 1995), pp. 34–41.

[Brady, 1977] J. M. BRADY, The Theory of Computer Science, Chapman and Hall, London, 1977.

[Bruno and Marchetto, 1986] G. Bruno AND G. MARCHETTO, "Process-Transformable Petri Nets for the Rapid Prototyping of Control Systems," IEEE Transactions on Software Engineering SE-12 (February 1986), pp. 346–57.

[Chen, 1976] P. Chen, "The Entity-Relationship Model–Towards a Unified View of Data," ACM Transactions on Databases (March 1976), pp. 9–36.

[Coulahan and Russopopoulos, 1983] J. E. COULHAN, JR., AND N. ROUSSPOLLOS, "Tiring Requirements for Time-Design Systems Using Petri Nets," IEEE Transactions on Software Engineering SE-9 (September 1983), pp. 60–13.

[Dart, Ellison, and Habermann, 1987] S. A. DART, J. R. ELLISON, P. H. HELLER, AND A. N. Habermann, "Software Development," IEEE Computer 20 (November 1987), pp. 18–28.

[Delise and Garlan, 1990] N. DELISE AND D. GARLAN, "A Formal Description of an Oscilloscope," IEEE Software 7 (September 1990), pp. 29–36.

[Delise and Schwartz, 1987] N. DELISE AND M. SCHWARTZ, "A Programming Environment for CSP?" Proceedings of the Second ACM SIGSOFT/SIGPLAN Software Engineering Symposium on Practical Software Development Environments, ACM SIGPLAN Notice 22 (January 1987), pp. 34–41.

[DeMarco, 1978] T. DeMarco, Structured Analysis and Specification, Young Press, New York, 1978.

[Diller, 1994] A. Diller: An Introduction to Formal Methods, 2nd ed., John Wiley and Sons, Chichester, UK, 1994.

[Doolan, 1992] E. P. Doolan, "Experience with Inspection Method," Software—Practice and Experience 22 (February 1992), pp. 73–82.

[Fagan, 1976] M. E. Fagan, "Design and Code Inspection to Reduce Errors in Program Development," IBM Systems Journal 15 (No. 3, 1976), pp. 182–211.

[Finney, 1996] F. Finney, "Mathematical Notation in Formal Specification: Too Difficult for Masses?" IEEE Transactions on Software Engineering 22 (1996), pp. 158–59.

[Gane and Sarsen, 1979] G. GANE AND S. SARSEN, Structured Systems Analysis: Tools and Techniques, Prentice Hall, Englewood Cliffs, NJ.

# 第12章 经典分析 403

[Oest, 1986] O. N. OEST, “VDM from Research to Practice,” Proceedings of the IFIP Congress, Information Processing '86, IFIP, 1986, pp. 52–53.

[Palshikar, 2001] J. K. PALSHIKAR, “Applying Formal Specializations to Real-World Software Development,” IEEE Software 18 (November–December 2001), pp. 89–97.

[Peterson, 1981] J. L. PETERSON, Petri Net Theory and the Modeling of Systems, Prentice Hall, Englewood, Cliffs, NJ, 1981.

[Petri, 1962] C. A. PETRI, “Kommunikation mit Automaten,” Ph.D. Dissertation, University of Bonn, Germany, 1962. [德语].

[Ross, 1985] D. T. Ross, “Applications and Extensions of SAT,” IEEE Computer 18 (April 1985), pp. 25–34.

[Schiefer, 1985] P. A. SCHIEFER, A. III, and W. E. RZEPKA, “A Case Study of SREM,” IEEE Computer 18 (April 1985), pp. 47–54.

[Schwartz and Delible, 1987] M. D. SCHWARTZ and N. M DELIBLE, “Specifying a Lift Control System with CSP,” Proceedings of the Fourth International Workshop on Software Engineering and Design, Monterey, CA, April 1987, pp. 21–27.

[Silberschatz, Gavin, and Gagne, 2002] A. SILBERSCHATZ, P. B. GALVIN, and G. GAGNE, Operating System Concepts, 6th ed., Addison-Wesley, Reading, MA, 2002.

[Sobel and Clark, 2002] A. E. K. SOBEL and M. R. CLARKSON, “Formal Methods Application: An Empirical Tale of Software Development,” IEEE Transactions on Software Engineering 28 (March 2002), pp. 308–20.

[Teichroher and Hershey, 1977] D. TEICHROHER and E. A. HERSHEY III, “PSL/PSA: A Computer-Aided Technique for Structured Documentation and Analysis of Information Processing Systems,” IEEE Transactions on Software Engineering SE-3 (January 1977), pp. 41–48.

[Spive, 2001] J. M. SPIVEY, The Z Notation: A Reference Manual, 3rd ed., spivey.oriel.ox.ac.uk/~mike/zrm/.

[Wing, 1990] J. WING, “A’s Introduction to Formal Methods,” IEEE Computer 23 (September 1990), pp. 8–24.

[Woodcock, 1989] J. WOODcock, “Calculating Properties of Z Specifications,” ACM SIGSOFT-Software Engineering Notes 14 (July 1989), pp. 43–54.

[Yourdon and Constantine, 1979] E. YOURDON and L. L. CONSTANTINE, Structured Design: Fundamentals of a Discipline of Computer Program and Systems Design, Prentice Hall, Englewood Cliffs, NJ, 1979.

# 第13章

## 面向对象分析

### 学习目标

学习本章后，你应该能够：

- 执行分析工作流。
- 提取边界类、控制类和实体类。
- 执行功能建模。
- 执行类建模。
- 执行动态建模。
- 执行用例实现。

在第12章中，我们研究了各种分析技术。本章是第12章的面向对象对应部分。

面向对象分析（OOA）是一种用于面向对象范式的半形式分析技术。在第12章中，我们指出用于系统分析有许多不同的技术，且它们在本质上是等价的。同样，已经有60多种不同的技术被提出的面向对象分析。同样，所有技术在很大程度上都是等价的。本章的“延伸阅读”部分包含了各种技术的引用，以及对不同技术的已比较。

然而，正如第3.1节所示，如今统一过程 [Jacobson, Booch, and Rumbaugh, 1999] 几乎总是面向对象软件生产的首选方法。由于这个原因，本章的第一部分和最后部分致力于统一过程的分析。

面向对象分析是面向对象范式的关键组件。当执行此工作流时，会提取类。用例和类是基础。

#### 以防你想知道（信息框 13.1）

面向对象范式的大多数进展发生在1990年到1995年之间。因为新技术通常需要15年才能被接受，面向对象范式的广泛采用本早于2005年开始。然而，千年漏洞（或Y2K问题）改变了预期的时间表。

在20世纪60年代，当计算机开始广泛使用时，硬件比现在贵得多。因此，那个年代的大多数软件产品代表日期时年份仅最后两位；遗留的“19”是默认理解的。在20世纪70年代，当硬件变得便宜时，许多遗留系统需要四位数字。在20世纪80年代，许多技术已被证明是成本效益的，意味着使用了面向对象范式。在2000年临近时，Y2K问题是面向对象范式的重大催化剂。在2000年1月，许多组织被迫在截止日期前修复遗留系统。由于修改现有软件是不可能的，唯一的替代方案是从开始。面对遗留系统的问题包括许多过时的软件产品。当2000年到来时，需要新的软件。

## 13.2 提取实体类

首先考虑的是建模持久化信息的实体类。

实体类的提取由三个迭代和增量执行的步骤组成：

- 功能建模：展示所有用例的场景描述（场景是用例的实例）。
- 实体类建模：确定实体类及其属性。然后，确定实体类之间的相互关系和交互。以类图的形式展示这些信息。
- 动态建模：确定每个实体类或子类执行的操作或接受的操作。以状态图的形式展示这些信息。

然而，对于所有的迭代和增量过程，这三个步骤并不总是按照这种顺序执行；一个模型中的变化经常触发另外两个模型的相应修订。

为了展示如何操作，我们现在提取电梯问题案例研究的实体类。

### 面向对象分析：

电梯问题案例

电梯问题案例在第12章中描述。为了方便参考，此处重复了该问题。

需要安装一个产品来控制具有 `$n$` 层的建筑中的 `$n$` 台电梯。该问题涉及根据以下约束在楼层之间移动电梯所需的所需的逻辑：

- 1. 每台电梯有一组 `$m$` 个按钮，每个楼层一个。这些按钮按下后会亮起并导致电梯访问相应的楼层。当电梯访问相应的楼层时，灯亮状态取消。
- 2. 除了第一层和顶层外，每层有两个按钮，一个用于请求上行电梯，另一个用于请求下行电梯。这些按钮在按下时会亮起。当电梯访问该楼层并按所需方向移动时，灯亮状态取消。
- 3. 当电梯没有请求时，它将保持在当前楼层且电门关闭。

面向对象分析（OOA）的第一步是对用例进行建模。

### 功能建模：

电梯问题案例

用例描述了所构建的产品与参与者之间的交互，参与者是该产品的外部用户。用户与电梯之间可能的交互只有用户按下电梯按钮以召唤电梯，或用户按下楼层按钮请求电梯停在特定楼层，因此有两个用例：“按下电梯按钮”和“按下楼层按钮”。这两个用例显示在图 13.2（第11.7节）的用例图中。

图 13.2

电梯问题案例的用例图

![](img/fbae284627ff75e470d980b0ad1cc726_426_0.png)

### B 部分 软件生命周期的工作流

图 13.3 普通场景的第一次迭代（缺失的职责和被动语态的使用将在下一次迭代中修正）。

- 1. 用户 A 在 3 层按下“上”楼层按钮以请求电梯。用户 A 想要去 7 层。
- 2. “上”按钮亮起。
- 3. 一台电梯到达 3 层。电梯内有用户 B，他在 1 层进入电梯并按了 9 层的电梯按钮。
- 4. 电梯门打开。
- 5. 定计时器开始。

  用户 A 进入电梯。
- 6. 用户 A 按下 7 层的电梯按钮。
- 7. 7 层的电梯按钮亮起。
- 8. 超时后电梯门关闭。
- 9. “上”按钮熄灭。
- 10. 电梯行驶到 7 层。
- 11. 7 层的电梯按钮熄灭。
- 12. 电梯门打开允许用户 A 离开电梯。
- 13. 定计时器开始。

  用户 A 离开电梯。
- 14. 超时后电梯门关闭。
- 15. 电梯带着用户 B 继续前往 9 层。

案例（Case）对整体功能提供了通用的描述；场景（Scenario）是用例的具体实例化，就像对象是类的实例化一样。通常情况下，存在大量的场景，每个场景代表一组特定的交互。在这里，我们考虑图 13.3 的场景，它包含了两个用例的实例。

图 13.3 描述了一个普通场景；即，用户与电梯之间的一组交互，符合我们对电梯行为的理解。图 13.3 是通过仔细观察不同用户与电梯（或更准确地说，与电梯按钮和门）的交互构建的。这 15 个编号的事件描述了用户 A 与电梯系统按钮之间的两次交互（事件 1 和事件 6）以及电梯系统组件执行的操作（事件 2 到 5 以及 7 到 15）。“用户 A 进入电梯”和“用户 A 离开电梯”这两项没有编号。它们本质上是注释；用户 A 在进入或离开电梯时并不与电梯组件交互。

相比之下，图 13.4 是一个异常场景。它发生在用户 A 在 3 层按下“上”按钮但实际上下到了 1 层时。这个场景是通过观察许多用户在电梯中的行为构建的；从未用过电梯的人不太可能意识到有时会按错按钮。

图 13.3 和图 13.4 处存在一个严重的错误。记住，如第 1.9 节所述，职责驱动的设计是面向对象范式的一个特征。从生命周期的开始，即从需求开始

## 第 13 章 面向对象分析

图 13.4 异常场景（缺失的职责和被动语态的使用将在下一次迭代中修正）。

- 1. 用户 A 在 3 层按下“上”楼层按钮以请求电梯。用户 A 想要去 1 层。
- 2. “上”按钮亮起。
- 3. 一台电梯到达 3 层。电梯内有用户 B，他在 1 层进入电梯并按下 9 层的电梯按钮。
- 4. 电梯门打开。
- 5. 定计时器开始。

  用户 A 进入电梯。
- 6. 用户 A 按下 1 层的电梯按钮。
- 7. 1 层的电梯按钮亮起。
- 8. 超时后电梯门关闭。
- 9. “上”按钮熄灭。
- 10. 电梯行驶到 9 层。
- 11. 9 层的电梯按钮熄灭。
- 12. 电梯门打开允许用户 B 离开电梯。
- 13. 定计时器开始。

  用户 B 离开电梯。
- 14. 超时后电梯门关闭。
- 15. 电梯带着用户 A 继续前往 1 层。

从工作流开始，必须指定每个动作的职责。这一表述并没有考虑到图 13.3 中的事件 2，“‘上’按钮亮起”。相反，场景应该指定谁负责点亮“上楼层按钮”。案例应该声明：“系统在‘上’楼层按钮上运行”。同样，事件 4 述为“电梯门打开”。但是谁或什么负责打开门？是用户必须自己打开和关闭门的手动电梯，还是系统负责打开和关闭门的自动电梯？因此，在案例和场景（用例的实例化）中，每个动作的职责必须被明确说明。

此外，在案例、场景中使用被动语态是一种不规范。例如，事件 2，“‘上’按钮亮起”不应使用被动语态。相反，场景应该指定谁负责点亮“上楼层按钮”。案例应该声明：“系统在‘上’楼层按钮上运行”。同样，事件 4 述为“电梯门打开”。但是谁或什么负责打开门？是用户必须自己打开和关闭门的手动电梯，还是系统负责打开和关闭门的自动电梯？因此，在案例和场景（用例的实例化）中，每个动作的职责必须被明确说明。

### 13.5.1 名词提取
