

## 良好编程实践 6.2

使用枚举常量（如 Status.WON、Status.LOST 和 Status.CONTINUE）而不是字面值（如 0、1 和 2）使程序更易于阅读和维护。

## main 方法的逻辑

main 中的第 26 行调用 rollDice，该方法从 1 到 6 中随机选取两个值，显示第一个骰子、第二个骰子的值以及它们的和，并返回这个和。接着，main 方法进入 switch 语句（第 29–45 行），该语句使用第 26 行的 sumOfDice 值来判断游戏是赢了、输了，还是应该继续再掷一次。在第一次掷骰子时导致赢或输的值在第 14–18 行被声明为 public static final int 常量。这些标识符名称使用赌场用语来表示这些和。这些常量与枚举常量一样，按照惯例全部使用大写字母声明，使它们在程序中更加醒目。第 31–34 行判断玩家是否以 SEVEN（7）或 YO_LEVEN（11）在第一次掷骰子时获胜。第 35–39 行判断玩家是否以 SNAKE_EYES（2）、TREY（3）或 BOX_CARS（12）在第一次掷骰子时输掉。第一次掷骰子后，如果游戏尚未结束，default 分支（第 40–44 行）将 gameStatus 设置为 Status.CONTINUE，将 sumOfDice 保存在 myPoint 中，并显示该点数。

如果我们仍在尝试“达到目标点数”（即游戏正在从之前的一次掷骰中继续），则执行第 48–58 行。第 50 行再次掷骰子。如果 sumOfDice 与 myPoint 匹配（第 53 行），第 54 行将 gameStatus 设置为 Status.WON，然后循环终止，因为游戏完成。如果 sumOfDice 是 SEVEN（第 56 行），第 57 行将 gameStatus 设置为 Status.LOST，循环终止，因为游戏完成。游戏结束时，第 61–64 行显示一条消息，指出玩家是赢了还是输了，然后程序终止。

该程序使用了我们讨论过的各种程序控制机制。Craps 类使用了两个方法——main 和 rollDice（从 main 中调用了两次）——以及 switch、while、if...else 和嵌套 if 控制语句。还要注意在 switch 语句中使用了多个 case 标签，以便对 SEVEN 和 YO_LEVEN 的和（第 31–32 行）以及 SNAKE_EYES、TREY 和 BOX_CARS 的和（第 35–37 行）执行相同的语句。

## 为什么某些常量未定义为 enum 常量

你可能想知道为什么我们将骰子的和声明为 public final static int 常量，而不是 enum 常量。原因是程序必须将 int 变量 sumOfDice（第 26 行）与这些常量进行比较，以确定每次掷骰的结果。假设我们声明一个枚举 Sum，其中包含代表游戏中使用的五个和的常量（例如 Sum.SNAKE_EYES），然后在 switch 语句（第 29–45 行）中使用这些常量。这样做会阻止我们将 sumOfDice 用作 switch 语句的控制表达式，因为 Java 不允许将 int 与枚举常量进行比较。要实现与当前程序相同的功能，我们必须使用一个类型为 Sum 的变量 currentSum 作为 switch 的控制表达式。不幸的是，Java 没有提供一种简单的方法将 int 值转换为特定的枚举常量。这可以通过一个单独的 switch 语句来完成。显然这会很繁琐，并且不会提高程序的可读性（从而违背了使用 enum 的目的）。

## 6.11 声明的作用域

你已经见过各种 Java 实体的声明，例如类、方法、变量和参数。声明引入了一些名称，可以用来引用这些 Java 实体。声明的作用域是程序中可以按名称引用被声明实体的部分。这样的实体被称为在该部分程序中“在作用域内”。本节介绍几个重要的作用域问题。

基本作用域规则如下：

- 1. 参数声明的作用域是声明所在的方法体。
- 2. 局部变量声明的作用域是从声明出现的位置到该块的末尾。
- 3. 出现在 for 语句头初始化部分中的局部变量声明，其作用域是 for 语句体以及头中的其他表达式。
- 4. 方法或字段的作用域是整个类体。这使类的非静态方法可以使用该类的字段和其他方法。

任何块都可以包含变量声明。如果方法中的局部变量或参数与类的字段同名，则该字段在块执行结束之前会被“隐藏”——这称为遮蔽（shadowing）。在第 8 章中，我们将讨论如何访问被遮蔽的字段。

## 错误预防提示 6.3

为字段和局部变量使用不同的名称，有助于防止在方法被调用且方法的局部变量遮蔽类中的字段时发生的细微逻辑错误。

图 6.9 演示了字段和局部变量的作用域问题。第 7 行声明字段 x 并将其初始化为 1。该字段在任何声明名为 x 的局部变量的块（或方法）中被遮蔽（隐藏）。main 方法（第 11–23 行）在第 13 行声明局部变量 x 并将其初始化为 5。输出该局部变量的值，以表明字段 x（其值为 1）在 main 中被遮蔽。程序还声明了另外两个方法——useLocalVariable（第 26–35 行）和 useField（第 38–45 行）——它们都不带参数且不返回结果。main 方法调用每个方法各两次（第 17–20 行）。useLocalVariable 方法在第 28 行声明局部变量 x。当第一次调用 useLocalVariable（第 17 行）时，它创建局部变量 x 并将其初始化为 25（第 28 行），输出 x 的值（第 30–31 行），递增 x（第 32 行），然后再次输出 x 的值（第 33–34 行）。当第二次调用 useLocalVariable（第 19 行）时，它重新创建局部变量 x 并重新初始化为 25，因此每次 useLocalVariable 调用的输出是相同的。

图 6.9 | Scope 类演示字段和局部变量的作用域。（第 1 部分，共 2 部分）

```
// Fig. 6.9: Scope.java
// Scope class demonstrates field and local variable scopes.

public class Scope
{
    // field that is accessible to all methods of this class
    private static int x = 1;

// method main creates and initializes local variable x
// and calls methods useLocalVariable and useField
public static void main( String[] args )
{
    int x = 5; // method's local variable x shadows field x

    System.out.printf( "local x in main is %d\n", x );

    useLocalVariable(); // useLocalVariable has local x
    useField(); // useField uses class Scope's field x
    useLocalVariable(); // useLocalVariable reinitializes local x
    useField(); // class Scope's field x retains its value

    System.out.printf( "\nlocal x in main is %d\n", x );
} // end main

// create and initialize local variable x during each call
public static void useLocalVariable()
{
    int x = 25; // initialized each time useLocalVariable is called

    System.out.printf(
        "\nlocal x on entering method useLocalVariable is %d\n", x );
    ++x; // modifies this method's local variable x
    System.out.printf(
        "local x before exiting method useLocalVariable is %d\n", x );
} // end method useLocalVariable

// modify class Scope's field x during each call
public static void useField()
{
    System.out.printf(
        "\nfield x on entering method useField is %d\n", x );
    x *= 10; // modifies class Scope's field x
    System.out.printf(
        "field x before exiting method useField is %d\n", x );
} // end method useField
} // end class Scope
```

```
local x in main is 5

local x on entering method useLocalVariable is 25
local x before exiting method useLocalVariable is 26

field x on entering method useField is 1
field x before exiting method useField is 10

local x on entering method useLocalVariable is 25
local x before exiting method useLocalVariable is 26

field x on entering method useField is 10
field x before exiting method useField is 100

local x in main is 5
```

图 6.9 | Scope 类演示字段和局部变量的作用域。（第 2 部分，共 2 部分）

