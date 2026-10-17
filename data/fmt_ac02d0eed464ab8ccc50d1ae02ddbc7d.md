
由于大多数面向的方法都是简单的，因此方法级别的测试也同样（或应该是）简单。这从两个方面转移了负担：面向代码的单元测试应该在类级别进行，而且集成测试对于面向代码变得越来越重要。

### 表 12.4 过程化与面向对象实现的比较

| 过程化 | 面向对象 |

|---|---|

| 单元数量 | 6 | 5 个类，17 个方法 |

| 单元复杂度之和 | 14 | 40 |

| 代码行数 | 90 | 119 |

| 消息数量 | 7 | 25 |

# 279 ■ 集成测试

![](img/c1598a96323013dee46c70ada02ae41b_301_0.png)

图 12.21 实现 Java 版本 `integrationNextDate` 的五个类的程序图。

### 表 12.5 NextDate 在面向对象实现中的消息

| 消息 | 源 | 目的 | 行号 |

|---|---|---|---|

| msg 1 | DateTest | Date | 3 |

| msg 2 | DateTest | date.getDate() | 4 |

| msg 3 | DateTest | date.nextDate() | 5 |

| msg 4 | DateTest | date.getDate() | 6 |

| msg 5 | Date | Year | 13 |

| msg 6 | Date | Month | 14 |

| msg 7 | Date | Day | 15 |

| msg 8 | Date.getDate | month.getMonth() | 18 |

| msg 9 | Date.getDate | day.getDay() | 18 |

| msg 10 | Date.getDate | year.OfYear() | 18 |

| msg 11 | Date.nextDate | day.getNextDay() | 21 |

| msg 12 | Date.nextDate | nextDay.getMonth() | 22 |

| msg 13 | Date.nextDate | month.OfYear() | 23 |

| msg 14 | Date.nextDate | month.getMonth() | 24 |

| msg 15 | Date.nextDate | nextDay.getDay() | 24 |

| msg 16 | Date.nextDate | year.OfYear() | 24 |

| msg 17 | Date.getNextDay | month.numberOfDays() | 38 |

| msg 18 | Date.getNextDay | Day(day+1,month) | 39 |

| msg 19 | Date.getNextDay | month.getMonth() | 41 |

| msg 20 | Month.numberOfDays | year.isLeapYear() | 79 |

| msg 21 | Month.getNextMonth() | Month(month+1,year) | 90 |

| msg 22 | Month.getNextMonth() | Month() | 92 |

| msg 23 | Month.getNextMonth() | Month(year.getNextYear()) | 92 |

| msg 24 | Year.getNextYear() | Year(year+1) | 117 |

## 12.6 基于模型的集成测试

在本节中，我们将基于代码的集成测试思想扩展到基于模型的测试（Model-Based Testing）层面。例如，请参考附录 B：Bookies Wish List Web 应用程序。我们的起点是模型之间基于消息的交互，在本例中是有限状态机。为了方便起见，图 B.2 在此处重复作为图 12.24。它是我们在本章之前查看过的调用图（Call Graph）的直接类比。

![](img/c1598a96323013dee46c70ada02ae41b_303_0.png)

### 12.6.1 消息通信

基于模型的集成测试的最简单形式是验证每条消息都发送到了正确的接收者并被其接收。图 12.21 显示了支持八个有限状态机之间通信的 38 条消息。这种级别的测试最容易通过 JUnit 等特定语言程序来完成。`ASSERT` 语句可以检查每条消息的发送端和接收端。我们可以假设这些简单的测试覆盖率指标：

- 测试覆盖 1：每条消息都发送到了正确的接收者

- 测试覆盖 2：每条消息都被正确的接收者接收

![](img/c1598a96323013dee46c70ada02ae41b_304_0.png)

图 12.23 2020 年 5 月 27 日的消息流。

### 12.6.2 两两集成

在图 12.24 中有八对共享消息的有限状态机（不包括通过信用卡接口的外部通信）。两两集成（Pairwise Integration）检查每一对共享消息的有限状态机。在这里，我们仔细查看包含账户创建（Account Creation）和管理（Administration）的这一对组合。它们使用消息 `m7`、`m11`、`m12`、`m13` 和 `m16` 进行通信。第 12.6.1 节描述的消息通信将显示，这五条消息中的每条都已正确地发送和接收。这种检查级别与基于程序图的单元测试良好类比，在那种测试中，测试用例没有“语义内容”。事实上，消息 `m7` 有两种响应：消息 `m11` 和 `m12`，取决于 `m` 是否传了一个了一个新的 `userID`。两两集成开始回答“为什么”会发送响应消息——这显然正在朝着增强语义内容的方向迈进。

![](img/c1598a96323013dee46c70ada02ae41b_305_0.png)

图 12.24 有限状态机之间的消息通信。

我们可以进一步观察到，只有在 `UserID` 被消息 `m11` 批准后，才能发送新的身份密码（PIN）。为了测试这一点，我们需要两个对象：`CreateAccountDriver`（用于向账户创建提供用户输入）和 `FoodieDBStub`（用于响应从管理 fsm 发送到 FoodieDB 的消息）。我们可以通过仅关注由账户创建开始的消息（图 12.25 中的精简状态机）来使用 `FoodieDBStub`。`CreateAccountDriver` 需要向 `AccountCreation` 有限状态机发送输入事件 `e11`、`e12` 和 `e13`（img/c1598a96323013dee46c70ada02ae41b_305_1.png：图 12.25 精简的 Foodie 状态机）。`FoodieDBStub` 将向管理层发送消息 `m9`、`m10` 和 `m15`。给定这四个类，我们可以测试更长的、语义正确的消息序列。需要注意的是，存在类似于我们在基于程序图的单元测试中看到的不可行路径的类比。查看附录 B 中 Foodie List 消息的描述，来自 Admin 的消息 `m12` 拒绝了提议的 `userID`。任何包含 `<m12, m13>` 的序列在逻辑上都是可能的。为了识别两两集成测试用例，我们从单个 fms 开始，如图 12.25 所示。从状态 `S1`（Open）开始，消息 `m1` 移动到 `AccountCreation` 中的状态 `S10`。我们需要 `AccountCreationDriver` 生成事件 `e1`（进入 `UserID`），这导致转换到状态 `S1` 并向 `Admin` 发送消息 `m7`（提议的 `userID`）。由于 `Admin` 不知道这是否是原始 `userID`，`FoodieDBStub` 将发送消息 `m9`、`m10` 和 `m15` 到管理层。

在图 12.24 中有八对共享消息的有限状态机（不包括通过信用卡接口的外部通信）。两两集成（Pairwise Integration）检查每一对共享消息的有限状态机。在这里，我们仔细查看包含账户创建（Account Creation）和管理（Administration）的这一对组合。它们使用消息 `m7`、`m11`、`m12`、`m13` 和 `m16` 进行通信。第 12.6.1 节描述的消息通信将显示，这五条消息中的每条都已正确地发送和接收。这种检查级别与基于程序图的单元测试良好类比，在那种测试中，测试用例没有“语义内容”。事实上，消息 `m7` 有两种响应：消息 `m11` 和 `m12`，取决于 `m` 是否传了一个新的 `userID`。两两集成开始回答“为什么”会发送响应消息——这显然正在朝着增强语义内容的方向迈进。

# 集成测试 287

![](img/c1598a96323013dee46c70ada02ae41b_309_0.png)

图 12.26 场景 1 中的消息和状态流。

对于这一讨论，我们假设有一种集成测试工具，它允许测试人员“执行”通过一组通信的有限状态机的路径。`CAUSE`（触发）和 `VERIFY`（验证）动词用法如下。 `CAUSE` 语句可以执行以下任何操作：

- 触发 fsm 本地事件（例如 `e11`），

- 触发向相邻 fsm 发送消息，并根据需要带有参数，

- 触发状态转换。

以几乎对称的方式，`VERIFY` 语句可以：

- 识别发生时 fsm 的当前状态，

- 报告当前状态的名称，

- 验证 `VERIFY` 参数的值

通过这些 `CAUSE` 和 `VERIFY` 能力，集成测试人员可以定义一个 FSM/M 路径的集成测试程序。表 12.7 衍生自图 12.26。表 12.6 中的第 1 到 4 步将表示为表 12.7 中的测试程序。

## 练习题

1. 在 `DateTest` 类中找到源节点和汇节点。

2. 考虑 MM-路径的一些可能的复杂度指标：

- `V(G) = e - n`

- `V(G) = 0.5e - n + 2`

- 节点出度的总和

- 节点之和加上边之和

# 288 软件工程

### 表 12.6 场景 1 FSM/M 路径描述

| 步骤 | 所在状态 | CAUSE 事件/消息 | 下一状态 | VERIFY (结果) |

|---|---|---|---|--|

| 1 | S1 | m1 | S10 | 在 AccountCreation |

| 2 | S10 | e11 | S11 | 在 AccountCreation |

| 3 | S10 | m7: propose UserID = 'Paul' | S41 | 在 Admin; UserID = 'Paul' |

| 4 | S41 | m7 | S42 | 在 Admin; |

| 5 | S41 | m8 | S60 | 在 FoodDB; UserID = 'Paul' |

| 6 | S60 | m8 | S61 | 在 FoodDB; |

| 7 | S61 | e61 | S62 | 在 FoodDB; |

| 8 | S61 | m9: Approve UserID = 'Paul' | S42 | 在 Admin, UserID = 'Paul' OK |

| 9 | S42 | m9 | S43 | 在 Admin |

| 10 | S42 | m11 | S11 | 在 AccountCreation |

| 11 | S11 | m11 | S12 | UserID = 'Paul' approved |

| 12 | S12 | e12 | S14 | 在 AccountCreation |

| 13 | S12 | m13: UserPIN defined | S43 | 在 Admin; 传递 UserPIN |

| 14 | S43 | m14: UserPIN to FoodieDB | S62 | UserPIN 存储在 FoodDB |

| 15 | S62 | m15: Confirm UserPIN | S45 | 在 Admin |

| 16 | S45 | m15 | S46 | 在 Admin |

| 17 | S45 | m16: Define PIN accepted | S14 | 在 AccountCreation |

| 18 | S46 | e44 | S41 | 在 Admin Home |

| 19 | S14 | m16: Define PIN accepted | S1 | 在 Foodie Home |

### 表 12.7 部分 FSM/M 测试程序

| 步骤 | 描述 |

|---|--|

| 1 | VERIFY(InStateS1) |

| 2 | CAUSE (SendMessage(m1)) |

| 3 | VERIFY(InStateS10)) |

| 4 | VERIFY (StateName = AccountCreation) |

| 5 | | CAUSE (InputEvent(e11)) |

| 6 | VERIFY(InStateS11) |

| 7 | CAUSE (SendMessage(m7) UserID = 'Paul') |

| 8 | VERIFY (InState(S41)) |

| 9 | VERIFY (UserID = 'Paul') |

将这些应用到图 12.22 中的第二个 MM-路径（以消息 `msg2` 开始）。

它们有任何解释价值吗？

3. 编写几个测试用例，将其解释为 MM-路径，然后看看你的 MM-路径遍历了图 12.20 中单元程序图的哪些部分。以此为基于 MM 路径的集成测试设计一种“覆盖率指标”。

4. 集成测试的目标之一是在测试用例导致失败时能够隔离故障。考虑对用过程语言编写的程序进行集成测试。对以下集成策略的相对故障隔离能力排序：

A = 基于分解的自顶向下集成。

B = 基于分解的自底向上集成。

C = 基于分解的层明治式集成。

D = 基于分解的“轰炸式”集成。

E = 基于调用图的成对集成。

F = 基于调用图的邻域集成（半径 = 2）。

G = 基于调用图的邻域集成（半径 = 1）。

通过将字母放在图 12.27 的连续体上显示你的评分。例如，假设策略 X 和 Y 效果相等但无效，而策略 Z 非常有效。

![](img/c1598a96323013dee46c70ada02ae41b_311_0.png)

图 12.27 故障隔离的连续体。

5. 考虑编写重要论文（例如正式论文）的过程。在（文字处理器出现之前的）时代，学生被鼓励制定详细的大纲，然后写出草稿，进行修改，最后打出最终版本。讨论技术如何改变这一过程，你能想到其他从瀑布模型转向不同的生命周期来改进过程的情况吗？

## 参考文献

- Matthew Ford, *Elementary Testing*, The Associated Press, Oct 1, 1999; 以及 http://mars.nasa.gov/msp98/news/co93.html.

- Michael S. Deutsch, *Software Verification and Validation-Realistic Approaches*, Prentice-Hall, Englewood Cliffs, NJ. 1982.
