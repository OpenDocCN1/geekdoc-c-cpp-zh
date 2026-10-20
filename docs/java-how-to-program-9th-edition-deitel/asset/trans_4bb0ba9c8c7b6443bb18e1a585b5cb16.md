

## 第 8.10 节 垃圾回收与 finalize 方法
- Java 中的每个类都有类 `Object` 的方法，其中之一是 `finalize` 方法。
- Java 虚拟机 (JVM) 执行自动垃圾回收（p. 334）以回收不再使用的对象占用的内存。当一个对象不再有引用时，该对象即可被垃圾回收。当 JVM 执行其垃圾回收器时，此类对象的内存可以被回收。
- `finalize` 方法（p. 334）在垃圾回收器回收对象的内存之前被调用。方法 `finalize` 不接受参数且返回类型为 `void`。
- 垃圾回收器（p. 334）在程序终止前可能永远不会执行。因此，不清楚方法 `finalize` 是否会被调用，或何时会被调用。

## 第 8.11 节 static 类成员
- static 变量（p. 334）表示在类的对象之间共享的类范围信息。
- static 变量具有类作用域。类的 `public static` 成员可以通过对该类的任何对象的引用访问，或者可以通过将成员名与类名和点（`.`）限定来访问。客户端代码只能通过该类的 方法 访问类的 `private static` 类成员。
- `static` 类成员在类被加载到内存时就已存在。
- 声明为 `static` 的方法无法访问非 static 类成员，因为 static 方法即使在尚未实例化该类的对象时也可以被调用。
- `this` 引用不能在 static 方法中使用。

## 第 8.12 节 static 导入
- static 导入声明（p. 338）使你能够在不使用类名和点（`.`）的情况下引用导入的 static 成员。单个 static 导入声明导入一个 static 成员，而按需 static 导入则导入一个类的所有 static 成员。

## 第 8.13 节 final 实例变量
- 在应用程序的上下文中，最小权限原则（p. 339）指出，代码应仅被授予完成其指定任务所需的权限和访问量。
- 关键字 `final` 指定变量不可修改。此类变量必须在声明时初始化或由类的每个构造函数初始化。

## 第 8.14 节 Time 类案例研究：创建包
- Java API 中的每个类都属于包含一组相关类的包。包有助于管理应用程序组件的复杂性并促进软件重用。
- 包提供了一种唯一类名的约定，有助于防止类名冲突（p. 342）。
- 在一个类可以被导入到多个应用程序之前，它必须被放置在包中。每个 Java 源代码文件只能有一个包声明（p. 340），并且它必须位于文件中的所有其他声明和语句之前。
- 每个包名都应以你的 Internet 域名反向开头。反转域名后，你可以为你的包选择任何其他名称。
- 在编译包中的类时，`javac` 命令行选项 `-d`（p. 342）指定存储包的位置，并导致编译器在不存在时创建包的目录。
- 包名是完全限定类名（p. 342）的一部分。这有助于防止名称冲突。
- 单类型导入声明（p. 344）指定要导入的一个类。类型按需导入声明（p. 344）仅导入程序从特定包中使用的类。
- 编译器使用类加载器（p. 344）在类路径中定位它需要的类。类路径由一系列目录或归档文件组成，每个目录之间用目录分隔符分隔（p. 344）。
- 编译器和 JVM 的类路径可以通过向 javac 或 java 命令提供 -classpath 选项（p. 345）来指定，也可以通过设置 CLASSPATH 环境变量来指定。如果类必须从当前目录加载，请在类路径中包含一个点（.）。

## 第 8.15 节 包访问
- 如果在类中声明方法或变量时未指定访问修饰符，则该方法或变量被认为具有包访问权限（p. 345）。

## 自测练习
### 8.1 填空，完成以下每条陈述：
- a) 在编译包中的类时，javac 命令行选项 ______ 指定存储包的位置，并导致编译器在不存在时创建包的目录。
- b) String 类 static 方法 ______ 与方法 System.out.printf 类似，但返回格式化的 String 而不是在命令窗口中显示 String。
- c) 如果一个方法包含一个与其中一个类字段同名的局部变量，则局部变量 ______ 该方法作用域中的字段。
- d) ______ 方法在垃圾回收器回收对象的内存之前被调用。
- e) 一个 ______ 声明指定要导入的一个类。
- f) 如果一个类声明了构造函数，编译器将不会创建 ______。
- g) 对象的 ______ 方法在对象出现在需要 String 的代码中时会被隐式调用。
- h) Get 方法通常称为 ______ 或 ______。
- i) 一个 ______ 方法测试条件是否为真或假。
- j) 对于每个枚举，编译器都会生成一个名为 ______ 的 static 方法，该方法按声明顺序返回枚举常量的数组。
- k) 组合有时被称为 ______ 关系。
- l) 一个 ______ 声明包含以逗号分隔的常量列表。
- m) 一个 ______ 变量表示由该类的所有对象共享的类范围信息。
- n) 一个 ______ 声明导入一个 static 成员。
- o) ______ 指出代码应仅被授予完成其指定任务所需的权限和访问量。
- p) 关键字 ______ 指定变量不可修改。
- q) Java 源代码文件只能有一个 ______，并且它必须位于文件中的所有其他声明和语句之前。
- r) 一个 ______ 声明仅导入程序从特定包中使用的类。
- s) 编译器使用一个 ______ 在类路径中定位它需要的类。
- t) 编译器和 JVM 的类路径可以通过 ______ 选项指定给 javac 或 java 命令，或通过设置 ______ 环境变量来指定。
- u) Set 方法通常称为 ______，因为它们通常会更改值。
- v) 一个 ______ 导入一个类的所有 static 成员。
- w) 一个类的 public 方法也称为该类的 ______ 或 ______。

## 自测练习答案
### 8.1
a) -d. b) format. c) shadows. d) finalize. e) single-type-import. f) default constructor. g) toString. h) accessor methods, query methods. i) predicate. j) values. k) has-a. l) enum. m) static. n) single static import. o) principle of least privilege. p) final. q) package declaration. r) type-import-on-demand. s) class loader. t) -classpath, CLASSPATH. u) mutator methods. v) static import-on-demand. w) public services, public interface.

## 练习
8.2 解释 Java 中包访问的概念。解释包访问的负面影响。

8.3 当为构造函数指定返回类型，即使是 void，会发生什么？

8.4 （Rectangle 类）创建一个类 Rectangle，其属性 length 和 width 默认为 1。提供计算矩形周长和面积的方法。它对 length 和 width 都有 set 和 get 方法。set 方法应验证 length 和 width 都是大于 0.0 且小于 20.0 的浮点数。编写一个程序来测试类 Rectangle。

8.5 （修改类的内部数据表示）Time2 类 Fig. 8.5 完全可以合理地将时间内部表示为午夜以来的秒数，而不是三个整数值 hour、minute 和 second。客户端可以使用相同的 public 方法并获得相同的结果。修改 Fig. 8.5 的 Time2 类，将 Time2 实现为午夜以来的秒数，并展示客户端看不到任何变化。

8.6 （储蓄账户类）创建类 SavingsAccount。使用 static 变量 annualInterestRate 存储所有账户持有者的年利率。类的每个对象包含一个私有实例变量 savingsBalance，表示储户当前存款金额。提供方法 calculateMonthlyInterest，通过将 savingsBalance 乘以 annualInterestRate 除以 12 来计算月利息——该利息应加到 savingsBalance。提供 static 方法 modifyInterestRate，将 annualInterestRate 设置为新值。编写一个程序来测试类 SavingsAccount。实例化两个 savingsAccount 对象 saver1 和 saver2，余额分别为 $2000.00 和 $3000.00。将 annualInterestRate 设置为 4%，然后计算每个 12 个月的月利息并打印两个储户的新余额。接下来，将 annualInterestRate 设置为 5%，计算下个月的利息并打印两个储户的新余额。

8.7 （增强类 Time2）修改 Fig. 8.5 的类 Time2，使其包含一个 tick 方法，该方法将 Time2 对象中存储的时间增加一秒。提供方法 incrementMinute 将分钟增加一，以及方法 incrementHour 将小时增加一。编写一个程序测试 tick 方法、incrementMinute 方法和 incrementHour 方法以确保它们工作正确。务必测试以下情况：
a) 增加到下一分钟，
b) 增加到下一小时和
c) 增加到下一天（即 11:59:59 PM 到 12:00:00 AM）。

8.8 （增强类 Date）修改 Fig. 8.7 的类 Date，对实例变量 month、day 和 year 的初始化值进行错误检查（目前它仅验证月份和日期）。提供方法 nextDay 将日期增加一天。编写一个程序在循环中测试方法 nextDay，在每次迭代中打印日期以说明该方法工作正确。测试以下情况：
a) 增加到下一个月和
b) 增加到下一年。

8.9 重写 Fig. 8.14 中的代码，使用单独的导入声明导入示例中使用的类 Math 的每个 static 成员。

