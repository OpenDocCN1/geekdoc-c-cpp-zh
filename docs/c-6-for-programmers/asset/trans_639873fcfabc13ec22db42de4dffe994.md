
我们使用强制类型转换运算符将 sumOfDice 中的 int 值转换为类型 DiceNames，并将其与 DiceNames 中的每个常量进行比较。第 35–36 行判断玩家在第一次掷骰时是否以 Seven（7）或 YoLeven（11）获胜。第 39–41 行判断玩家在第一次掷骰时是否以 SnakeEyes（2）、Trey（3）或 BoxCars（12）落败。第一次掷骰后，如果游戏尚未结束，则默认情况（第 44–48 行）将 sumOfDice 保存到 myPoint（第 46 行）中并显示点数（第 47 行）。

### 骰子的额外掷骰
如果我们仍在尝试“达到我们的点数”（即游戏从之前的掷骰继续进行），则第 52–69 行的循环会执行。第 54 行再次掷骰。如果第 57 行中 sumOfDice 与 myPoint 匹配，则第 59 行将 gameStatus 设置为 Status.Won，并且循环终止，因为游戏已完成。第 64 行，我们使用强制类型转换运算符 (int) 获取 DiceNames.Seven 的底层值，以便将其与 sumOfDice 进行比较。如果 sumOfDice 等于 Seven（7），则第 66 行将 gameStatus 设置为 Status.Lost，并且循环终止，因为游戏已结束。游戏完成后，第 72–79 行显示一条消息，指示玩家是赢还是输，并且应用程序终止。

### Craps 示例中的控制语句
请注意我们所讨论的各种程序控制机制的使用。Craps 类使用两个方法——Main 和 RollDice（从 Main 中调用两次）——以及 switch、while、if...else 和嵌套 if 控制语句。此外，请注意我们在 switch 语句中使用多个 case 标签，以便对 Seven 和 YoLeven 的和（第 35–36 行）以及 SnakeEyes、Trey 和 BoxCars 的和（第 39–41 行）执行相同的语句。

### 用于自动实现属性的代码片段
Visual Studio 具有一个名为代码片段的功能，允许您将预定义的代码模板插入源代码中。其中一个片段使您能够轻松创建针对枚举类型所有可能值的 switch 语句的 case。 在 C# 代码中键入 switch 然后按两次 Tab。如果在 switch 语句的表达式中指定枚举类型的变量并按 Enter，则会为每个枚举常量自动生成一个 case。

要获取所有可用代码片段的列表，请键入 Ctrl + k、Ctrl + x。这将在代码编辑器中显示“插入代码片段”窗口。您可以使用鼠标浏览 Visual C# 代码片段文件夹以查看代码片段。此功能还可以通过在源代码编辑器中右键单击并选择“插入代码片段...”菜单项来访问。

## 7.10 声明的作用域
您已经看到 C# 实体（如类、方法、属性、变量和参数）的声明。声明引入了可用于引用此类 C# 实体的名称。声明的作用域是应用程序中可以通过其非限定名称引用已声明实体的部分。这样的实体对于应用程序的该部分来说被称为“在作用域内”。本节介绍几个重要的作用域问题。基本作用域规则如下：

- 1. 参数声明的作用域是声明所在方法的体。
- 2. 局部变量声明的作用域是从声明出现的位置到包含该声明的块的末尾。
- 3. for 语句头初始化部分中出现的局部变量声明的作用域是 for 语句的体以及头中的其他表达式。
- 4. 类的方法、属性或字段的作用域是类的整个体。这使得类的非静态方法和属性可以使用类的任何字段、方法和属性，而不管它们的声明顺序如何。类似地，静态方法和属性可以使用类的任何静态成员。

任何块都可能包含变量声明。如果方法中的局部变量或参数与字段具有相同的名称，则该字段在块终止之前会被隐藏——在第 10 章中，我们将讨论如何访问隐藏的字段。如果方法中的嵌套块包含与该方法外部块中的局部变量同名的变量，则会发生编译错误。图 7.8 中的应用程序演示了字段和局部变量的作用域问题。

### 错误预防提示 7.1
使用不同的名称为字段和局部变量，以帮助防止在方法被调用且该方法的局部变量隐藏了类中同名字段时发生的微妙逻辑错误。

```
// Fig. 7.8: Scope.cs
// Scope class demonstrates static- and local-variable scopes.
using System;

class Scope
{
    // static variable that's accessible to all methods of this class
    private static int x = 1;

    // Main creates and initializes local variable x
    // and calls methods UseLocalVariable and UseStaticVariable
    static void Main()
    {
        int x = 5; // method's local variable x hides static variable x

        Console.WriteLine("local x in method Main is {x}");

        // UseLocalVariable has its own local x
        UseLocalVariable();

        // UseStaticVariable uses class Scope's static variable x
        UseStaticVariable();

        // UseLocalVariable reinitializes its own local x
        UseLocalVariable();

        // class Scope's static variable x retains its value
        UseStaticVariable();
    }
}
```

图 7.8 | Scope 类演示静态变量和局部变量的作用域。（第 1 部分，共 2 部分。）

```csharp
29     Console.WriteLine($"\nlocal x in method Main is {x}");
30 }
31
32     // create and initialize local variable x during each call
33     static void UseLocalVariable()
34     {
35         int x = 25; // initialized each time UseLocalVariable is called
36
37         Console.WriteLine(
38             $"\nlocal x on entering method UseLocalVariable is {x}");
39         ++x; // modifies this method's local variable x
40         Console.WriteLine(
41             $"local x before exiting method UseLocalVariable is {x}");
42     }
43
44     // modify class Scope's static variable x during each call
45     static void UseStaticVariable()
46     {
47         Console.WriteLine("static variable x on entering method " +
48             $"UseStaticVariable is {x}");
49         x *= 10; // modifies class Scope's static variable x
50         Console.WriteLine("static variable x before exiting " +
51             $"method UseStaticVariable is {x}");
52     }
53 }
54
```

```text
local x in method Main is 5

local x on entering method UseLocalVariable is 25
local x before exiting method UseLocalVariable is 26

static variable x on entering method UseStaticVariable is 1
static variable x before exiting method UseStaticVariable is 10

local x on entering method UseLocalVariable is 25
local x before exiting method UseLocalVariable is 26

static variable x on entering method UseStaticVariable is 10
static variable x before exiting method UseStaticVariable is 100

local x in method Main is 5
```

图 7.8 | Scope 类演示静态变量和局部变量的作用域。（第 2 部分，共 2 部分。）

第 8 行声明并初始化静态变量 x 为 1。此静态变量在声明了名为 x 的局部变量的任何块（或方法）中都会被隐藏。方法 Main（第 12–31 行）声明局部变量 x（第 14 行）并将其初始化为 5。此局部变量的值被输出以显示静态变量 x（其值为 1）在方法 Main 中被隐藏。应用程序声明了另外两个方法——UseLocalVariable（第 34–43 行）和 UseStaticVariable（第 46–53 行）——它们均不接受参数也不返回结果。方法 Main 两次调用每个方法（第 19–28 行）。方法 UseLocalVariable 声明局部变量 x（第 36 行）。当 UseLocalVariable 第一次被调用（第 19 行）时，它创建局部变量 x 并

另一个方法，新的方法调用的栈帧只是被 *压入* 调用栈。因此，新调用的方法返回到其调用者所需返回地址现在位于栈的 *顶部*。

## 7.11.3 局部变量和栈帧
栈帧还有另一个重要职责。大多数方法都有局部变量——参数以及方法声明的任何局部变量。局部变量需要在方法执行期间存在。如果方法调用其他方法，它们需要保持活动状态。但当被调用方法返回到其调用者时，被调用方法的局部变量需要“消失”。被调用方法的栈帧是为被调用方法的局部变量保留内存的理想位置。只要被调用方法处于活动状态，该栈帧就存在。当该方法返回并且不再需要其局部变量时，其栈帧会被从栈中 *弹出*，并且这些局部变量不再存在。

## 7.11.4 栈溢出
当然，计算机中的内存量是有限的，因此只能使用一定量的内存来在方法调用栈上存储激活记录。如果发生的方法调用多于可以在方法调用栈上存储其激活记录的数量，则会发生一种致命错误，称为栈溢出——通常由无限递归引起（第 7.16 节）。

## 7.11.5 方法调用栈的实际操作
现在让我们考虑调用栈如何支持由 Main（第 8–12 行）调用的 Square 方法（图 7.9 的第 15–18 行）的操作。

```csharp
// Fig. 7.9: SquareTest.cs
// Square method used to demonstrate the method
// call stack and activation records.
using System;

class Program
{
    static void Main()
    {
        int x = 10; // value to square (local variable in main)
        Console.WriteLine($"x squared: {Square(x)}");
    }

    // returns the square of an integer
    static int Square(int y) // y is a local variable
    {
        return y * y; // calculate square of y and return result
    }
}
```

**图 7.9** | 用于演示方法调用栈和激活记录的 Square 方法。（第 1 部分，共 2 部分）

2. 这就是网站 stackoverflow.com 得名的方式。这是一个流行的网站，用于获取编程问题的答案。
