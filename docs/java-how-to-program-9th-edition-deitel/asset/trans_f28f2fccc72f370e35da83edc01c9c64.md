

发送给外部实体——它们很重要，因为它们与我们的 ATM 系统交互，但我们不需要在 ATM 软件中将它们建模为类。请回忆，我们将 ATM 用户（即银行客户）建模为图 12.4 中用例图中的参与者。

我们不将“$20 钞票”或“存款信封”建模为类。这些是现实世界中的物理对象，但它们不是被自动化的部分。我们可以用建模现金分配器的类的一个属性来充分表示钞票在系统中的存在。（我们在第 12.4 节中为 ATM 系统的类分配属性。）例如，现金分配器维护其包含的钞票数量的计数。需求文档没有说明系统在收到存款信封后应对其做什么。我们可以假设仅仅确认收到信封——由建模存款槽的类执行的操作——就足以表示信封在系统中的存在。我们在第 12.6 节中为 ATM 系统的类分配操作。

在我们简化的 ATM 系统中，将各种“货币”金额，包括账户的“余额”表示为类的属性似乎最合适。同样，名词“账号”和“PIN”代表 ATM 系统中的重要信息。它们是银行账户的重要属性。它们不表现出行为。因此，我们最合适地将它们建模为账户类的属性。

尽管需求文档经常以一般意义描述“交易”，但我们目前不建模金融交易的广泛概念。相反，我们将三种类型的交易（即“余额查询”、“取款”和“存款”）建模为单独的类。这些类拥有执行它们所代表的交易所需的特定属性。例如，取款需要知道取款金额。余额查询 however 不需要除账号之外的任何额外数据。此外，三种交易类表现出独特的行为。取款包括向用户发放现金，而存款涉及从用户接收存款信封。在第 13.3 节中，我们使用面向对象的继承概念将所有交易的共同特征提取到一个通用的“交易”类中。

我们根据图 12.5 中剩余的名词和名词短语确定系统的类。其中每一个都指以下之一：

- ATM
- screen
- keypad
- cash dispenser
- deposit slot
- account
- bank database
- balance inquiry
- withdrawal
- deposit

此列表中的元素可能是我们实现系统时需要的类。

我们现在可以根据我们创建的列表对系统中的类进行建模。我们在设计过程中将类名大写——这是 UML 惯例——正如我们编写时一样

| Symbol | Meaning |
| --- | --- |
| 0 | None |
| 1 | One |
| m | An integer value |
| 0..1 | Zero or one |
| m, n | m or n |
| m..n | At least m, but not more than n |
| * | Any nonnegative integer (zero or more) |
| 0..* | Zero or more (identical to *) |
| 1..* | One or more |

Fig. 12.8 | Multiplicity types.

关联可以命名。例如，图 12.7 中连接类 ATM 和 Withdrawal 的线条上方单词 Executes 表示该关联的名称。该图的一部分读作“一个 ATM 类的对象执行零个或一个 Withdrawal 类的对象”。关联名称是方向性的，如实心箭头所示——因此，例如，将前述关联从右到左读作“零个或一个 Withdrawal 类的对象执行一个 ATM 类的对象”是不合适的。

图 12.7 中关联线在 Withdrawal 端的单词 currentTransaction 是一个角色名，标识 Withdrawal 对象在其与 ATM 的关系中扮演的角色。角色名通过标识类在关联上下文中扮演的角色，为类之间的关联增添意义。一个类可以在同一系统中扮演多个角色。例如，在学校人员系统中，一个人在与学生关系时可能扮演“教授”的角色。同一个人可能在与另一位教授的关联中扮演“同事”的角色，并在指导学生运动员时扮演“教练”的角色。在图 12.7 中，角色名 currentTransaction 表明参与与 ATM 类对象 Executes 关联的 Withdrawal 对象代表 ATM 当前正在处理的交易。在其他上下文中，Withdrawal 对象可能承担其他角色（例如，“上一笔交易”）。请注意，我们没有为 Executes 关联的 ATM 端指定角色名。当关联的含义无需它们即可明确时，类图中的角色名通常会被省略。

除了表示简单关系外，关联还可以指定更复杂的关系，例如一个类的对象由其他类的对象组成。考虑一台真实的自动取款机。制造商组装哪些“部件”来构建一台可用的 ATM？我们的需求文档告诉我们，ATM 由屏幕、键盘、现金分配器和存款槽组成。

在图 12.9 中，附加到 ATM 类关联线的实心菱形表示 ATM 与类 Screen、Keypad、CashDispenser 和 DepositSlot 具有组合关系。组合意味着整体/部分关系。关联线一端具有组合符号（实心菱形）的类是整体（在本例中为 ATM），而关联线另一端的类是部分——在本例中为 Screen、Keypad、CashDispenser 和 DepositSlot。图 12.9 中的组合表示 ATM 类的对象由一个 Screen 类的对象、一个 CashDispenser 类的对象、一个 Keypad 类的对象和一个 DepositSlot 类的对象构成。ATM 有一个屏幕、一个键盘、一个现金分配器和一个存款槽。（正如我们在第 9 章中看到的，is-a 关系定义了继承。我们将在第 13.3 节中看到 ATM 系统设计中使用继承的良好机会。）

of class CashDispenser, one object of class Keypad and one object of class DepositSlot. The ATM has a screen, a keypad, a cash dispenser and a deposit slot. (As we saw in Chapter 9, the is-a relationship defines inheritance. We’ll see in Section 13.3 that there’s a nice opportunity to use inheritance in the ATM system design.)

![](img/009e962758dcc71dbc43a493362e6dc0_519_0.png)

Fig. 12.9 | Class diagram showing composition relationships.

根据 UML 规范（www.omg.org/technology/documents/formal/uml1.htm），组合关系具有以下属性：

- 1. 关系中只有一个类可以代表整体（即菱形只能放在关联线的一端）。例如，要么屏幕是 ATM 的一部分，要么 ATM 是屏幕的一部分，但屏幕和 ATM 不能在关系中同时代表整体。
- 2. 组合关系中的部分仅在整体存在时才存在，并且整体负责其部分的创建和销毁。例如，构建 ATM 的行为包括制造其部件。此外，如果 ATM 被销毁，其屏幕、键盘、现金分配器和存款槽也将被销毁。
- 3. 一个部分在同一时间只能属于一个整体，尽管它可以被移除并附加到另一个整体，后者随后承担对该部分的责任。

我们类图中的实心菱形表示满足这些属性的组合关系。如果 has-a 关系不满足其中一个或多个标准，UML 规定在关联线的末端附加空心菱形以表示聚合——一种较弱的组合形式。例如，个人电脑和电脑显示器参与聚合关系——电脑有一个显示器，但这两个部件可以独立存在，并且同一个显示器可以同时连接到多台电脑，从而违反了组合的第二和第三属性。

图 12.10 显示了 ATM 系统的类图。该图建模了我们已识别的大多数类，以及我们可以从需求文档推断出的它们之间的关联。类 BalanceInquiry 和 Deposit 参与与类 Withdrawal 类似的关联，因此我们选择将其从此图中省略以保持简洁。在第 13.3 节中，我们扩展我们的类图以包含 ATM 系统中的所有类。

