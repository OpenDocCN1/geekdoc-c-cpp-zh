

- 10. 正确重载的方法必须具有相同的 ________。
- a. 返回类型 c. 参数列表
- b. 标识符 d. 以上均对。

- 11. 当方法在以下什么情况下时，它们是歧义的？
- a. 被重载时
- b. 以混淆的方式编写时
- c. 编译器无法区分时
- d. 参数类型与返回类型相同

- 12. 下面一组方法声明中，哪一组正确地重载了方法？
- a. private static void MethodA(int a)
  private static void MethodA(int b, double c)
- b. private static void MethodB(double d)
  private static void MethodB()
- c. private static double MethodC(int e)
  private static double MethodD(int f)
- d. 以上有两组是正确重载的方法。

- 13. 下面一组方法声明中，哪一组代表了正确重载的方法？
- a. private static void Method(int a)
  private static void Method(int b)
- b. private static void Method(double d)
  private static int Method()
- c. private static double Method(int e)
  private static int Method(int f)
- d. 以上有两组是正确重载的方法。

- 14. 确定执行哪个重载版本的方法的过程称为重载 ________
- a. 混淆 c. 革命
- b. 注入 d. 解析（决议）

- 15. 当方法的某个参数是可选的时，意味着 ________
- a. 调用该方法时不需要任何参数
- b. 如果没有发送参数，则将为该参数分配一个默认值
- c. 默认值将覆盖任何发送给它的参数参数值
- d. 你不需要在方法体内部使用该参数

- 16. 下面哪一个是非法的方法声明？
- a. private static void createState(int acctNum, double balance = 0.0)
- b. private static void createStatement(int acctNum = 0, double balance)
- c. private static void createState(int acctNum = 0, double balance = 0)
- d. 以上都是合法的。

- 17. 假设你声明了如下方法：
  private static double ComputeBill(int acct, double price, double discount = 0)
- 下面哪一个是是合法的方法调用？
- a. ComputeBill();
- b. ComputeBill(1001);
- c. ComputeBill(1001, 200.00);
- d. 以上均不合法。

- 18. 假设你声明了如下方法：
  private static double CalculateDiscount(int acct = 0, double price = 0, double discount = 0)
- 下面哪一个是合法的方法调用？
- a. CalculateDiscount();
- b. CalculatedDiscount(200.00);
- c. CalculatedDiscount(3000.0, 0.02);
- d. 以上均不合法。

- 19. 假设你声明了如下方法：
  private static double DisplayData(string name = "XX", double amount = -10.0)
- 下面哪一个是非法的方法调用？
- a. DisplayData(name : "Albert");
- b. DisplayData(amount : 200, name : "Albert");
- c. DisplayData(amount : 900.0);
- d. 以上都是合法的。

# 练习

## 编程练习

- 20. 假设你声明了一个名为 scores 的整数，并执行了以下方法调用：
  TotalScores(scores, num : 1);
  在重载的方法定义中，哪一个会被执行？
- a. private static void TotalScores(int[] scores)
- b. private static void TotalScores(int[] scores, int num)
- c. private static void TotalScores(int[] scores, int num = 10, int code = 10)
- d. 程序将无法编译。

- a. 创建一个名为 Reverse3 的程序，其 Main() 方法声明了三个整数 firstInt、middleInt 和 lastInt。为这些变量赋值，显示它们，然后将它们传递给一个接受引用变量的方法，将第一个值放在 lastInt 变量中，将最后一个值放在 firstInt 变量中。在 Main() 方法中再次显示这三个变量，证明它们的位置已被反转。

- b. 创建一个名为 Reverse4 的程序，其中包含一个反转四个值位置的方法。编写一个 Main() 方法来演示该方法正常工作。

- 2. 创建一个名为 IntegerFacts 的程序，其 Main() 方法声明了一个包含 10 个整数的数组。调用一个方法来交互式填充数组，输入最多 10 个值，直到输入哨兵值为止。如果输入的项不是整数，则提示用户。调用第二个方法，输出数组中最大值、最小值、数组中数值之和以及算术平均值的参数。在 Main() 方法中显示所有统计数据。

- 3. 创建一个用于“小镇地区机场航班”（Smalltown Regional Airport Flights）的程序，接受来自图 8-33 选项的整数或字符串代码。将用户的输入传递给两个重载的 GetFlightInfo() 方法之一，然后显示包含所有航班详情的返回字符串。接受整数的版本查找机场代码、名称和飞行时间；接受字符串描述的版本查找航班、机场名称和时间。

| 航班号 | 机场名称 | 时间 |
| :--- | :--- | :--- |
| 201 | Austin | 0710 |
| 321 | Corpus Christi | 0830 |
| 510 | DFW | 0915 |
| 633 | HOU | 1140 |

图 8-33 小镇地区机场航班

- 4. 创建一个名为 Auction（拍卖）的程序，接受整数数量或图 8-33 选项中的字符串代码。将用户的输入传递给两个重载 GetFlightInfo() 方法之一，然后显示包含所有航班信息的返回字符串。接受整数的版本查找机场代码、名称和时间；接受字符串描述的版本查找航班、机场名称和时间。如果未找到，则显示一个带有 $ 符号的错误信息。

- 5. 创建一个名为 TipCalculation（计算计算）的程序，其中包含两个重载方法：一个接受 double 类型的价格和小费（例如 30.00 和 20），另一个接受 double 类型的价格和整数类型的小费（例如 20% 5）。每个方法应显示价格、按比例的小费以及总计。

- 6. 编写一个名为 InputMethod2 的程序，消除 InputMethod() 中的重复代码，使其仅包含两个语句：
  one = DataEntry("first");
  two = DataEntry("second");

- 7. 编写一个名为 Averages（平均值）的程序，其中一个方法接受任意数量的数字参数，显示它们并显示平均值。在传递一个、两个或三个数字时演示该方法正常工作。

- 8. 编写一个名为 SortWords 的程序，包含一个接受任意数量单词并按字母顺序排序的方法。在传递、两个、五个或十个单词时演示。

- 9. 编写一个名为 Movie 的程序，包含一个接受两个参数的方法：字符串名称和整数运行时间。为时间提供一个默认值，以便如果不带参数调用方法，则时间设置为 90。编写一个 Main() 方法证明你可以只带字符串以及字符串和整数。

- 10. 在“斗牌”（War）的游戏中，扑牌被分成两个玩家，其中一个是计算机。每次为电脑和玩家各展示出一张牌，点值大的人得两分（在这个游戏中，国王是最大的，之后是女王和将，然后是数字 10 到 2，最后是王牌）。如果电脑和玩家展示的牌值相等，则各得一分。游戏结束时，所有 52 张牌都只用过一次，总分数为 52。
- 使用一个包含 52 个整数的数组来存储每张牌的唯一值。编写一个方法 F11Deck()，将 52 个唯一值放入该数组中。另一个名为 SelectCard() 的方法，你在每回合中调用两次，为每个玩家选择一张唯一的牌，且 26 轮中牌不重复（要在每回合牌之间暂停播放，请调用 ReadLine()）。

| 轮次 | 电脑 | 玩家 | 分数 |
| :--- | :--- | :--- | :--- |
| 1 | 红桃国王 | 黑桃5 | 电脑: 2, 玩家: 0 |
| 2 | 桃梅7 | 红心4 | 电脑: 4, 玩家: 0 |
| 3 | 方梅5 | 黑桃6 | 电脑: 4, 玩家: 0 |

图 8-34 的第一部分显示了控制台界面和 GUI WarCardGame 程序的典型执行。（警告：这是一个困难的练习！）

