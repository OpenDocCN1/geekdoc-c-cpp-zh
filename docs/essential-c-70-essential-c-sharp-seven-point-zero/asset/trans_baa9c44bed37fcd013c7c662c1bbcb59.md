

## 列表 4.23：没有代码块的 if 语句

```
if(input < 9)
    System.Console.WriteLine("Exiting");
```

然而，使用花括号，我们可以将语句合并为一个称为**块语句**或**代码块**的单一语句，从而允许将多个语句分组为一个作为结果的单一语句。例如，请参见列表 4.24 中半径计算中高亮的代码块。

## 列表 4.24：后跟代码块的 if 语句

```
class CircleAreaCalculator
{
    static void Main()
    {
        double radius;    // Declare a variable to store the radius
        double area;      // Declare a variable to store the area

        System.Console.Write("Enter the radius of the circle: ");

        // double.Parse converts the ReadLine()
        // return to a double
        radius = double.Parse(System.Console.ReadLine());
        if(radius >= 0)
        {
            // Calculate the area of the circle
            area = Math.PI * radius * radius;
            System.Console.WriteLine(
                $"The area of the circle is: { area :0.00 }");
        }
        else
        {
            System.Console.WriteLine(
                $"{ radius } is not a valid radius.");
        }
    }
}
```

输出 4.14 展示了列表 4.24 的结果。

## 输出 4.14

```
Enter the radius of the circle: 3
The area of the circle is: 28.27
```

在此示例中，*if* 语句检查半径是否为正数。如果是，则计算并显示圆的面积；否则，显示无效半径的消息。

请注意，在此示例中，第一条 *if* 语句后面跟随两个语句。然而，这两个语句出现在花括号内。花括号将这些语句组合成一个代码块，该代码块本身是一个单一语句。

如果在列表 4.24 中省略创建代码块的花括号，则只有紧跟在布尔表达式后面的语句才会根据条件执行。后续的语句将无论 *if* 语句的布尔表达式如何都会执行。无效代码如列表 4.25 所示。

## 列表 4.25：依赖缩进，导致无效代码

```
if(radius >= 0)
    area = Math.PI * radius * radius;
    System.Console.WriteLine(
        $"The area of the circle is: { area:0.00}");
```

在 C# 中，缩进仅用于增强代码可读性。编译器会忽略它，因此上述代码在语义上等同于列表 4.26。

## 列表 4.26：带花括号且与列表 4.25 语义等效

```
if(radius >= 0)
{
    area = Math.PI * radius * radius;
}
System.Console.WriteLine(
    $"The area of the circle is: { area:0.00}");
```

程序员应格外小心以避免此类细微的 bug，甚至可能走到始终在控制流语句之后包含代码块的程度，即使只有一个语句。一个被广泛接受的编码准则是避免省略花括号，除了最简单的单行 *if* 语句可能例外。

虽然不寻常，但确实可能存在在词法上不是控制流语句直接部分的代码块。换句话说，单独放置花括号（例如，没有条件或循环）是合法的语法。

在列表 4.25 和 4.26 中，圆周率值由 System.Math 类中的 PI 常量表示。不要硬编码 $\tau$ 和 e（自然对数的底）的值，代码应使用 `System.Math.PI` 和 `System.Math.E`。

> **准则**
> - 避免省略花括号，除了最简单的单行 `if` 语句。

## 代码块、作用域和声明空间

代码块通常被称为*作用域*，但这两个术语并不完全可互换。**作用域**是指命名实体的区域，在该区域内可以使用非限定名称合法地引用该实体。例如，局部变量的作用域正是包围它的代码块文本，这解释了为什么通常将代码块称为作用域。

作用域经常与声明空间混淆。**声明空间**是命名实体的逻辑容器，其中两个实体不能有相同的名称。代码块不仅定义了一个作用域，还定义了一个局部变量声明空间。在同一声明空间中出现两个具有相同名称的局部变量声明是非法的。同样，不可能在同一个类中声明两个签名均为 `Main()` 的方法。（此规则对于方法略有放宽：只要它们具有不同的签名，两个方法可以在声明空间内具有相同的名称。方法的签名包括其名称以及参数的数量和类型。）在块内，可以通过名称引用局部变量，并且它必须是块内以该名称声明的唯一实体。在声明块之外，无法通过名称引用局部变量；局部变量在块之外被认为是“超出作用域”。

*总之*，作用域用于确定名称引用的是什么实体；声明空间确定何时两个以相同名称声明的实体会相互冲突。在列表 4.27 中，在嵌入 *if* 语句的块语句内部声明局部变量 `message` 将其作用域限制为仅该块语句；当稍后在方法中使用其名称时，该局部变量超出了作用域。为避免错误，必须在块外部声明变量。

## 列表 4.27：在作用域外部无法访问的变量

```csharp
class Program
{
    static void Main(string[] args)
    {
        int playerCount;
        System.Console.Write(
            "Enter the number of players (1 or 2):");
        playerCount = int.Parse(System.Console.ReadLine());
        if (playerCount != 1 && playerCount != 2)
        {
            string message =
                "You entered an invalid number of players.";
        }
        else
        {
            // ...
        }
        // Error: message is not in scope
        System.Console.WriteLine(message);
    }
}
```

输出 4.15 展示了列表 4.27 的结果。

## 输出 4.15

```
...
....\Program.cs(18,26): error CS0103: The name 'message' does not exist in the current context
```

局部变量名称必须唯一的声明空间涵盖了文本上封闭在最初声明该局部变量的块内的所有子代码块。C# 编译器防止在方法代码块内直接声明（或作为参数）的局部变量名称在子代码块内被重用。在列表 4.27 中，由于 args 和 playerCount 是在方法代码块内声明的，因此不能在方法内的任何地方再次声明它们。

名称 message 在整个局部变量的作用域内都指向这个局部变量——也就是说，直接包围声明的块。同样，playerCount 在包含声明的块内（包括 *if* 语句的后果和备选分支这两个子块内）都指向同一个变量。

### 语言对比：C++——局部变量作用域

在 C++ 中，在块中声明的局部变量从声明语句点开始到块结束都在作用域内。因此，试图在其声明前引用局部变量会失败，因为该变量不在作用域内。如果另一个具有该名称的实体“在作用域内”，C++ 语言会将名称解析为该实体，这可能不是你所期望的。在 C# 中，规则略有不同：局部变量在整个声明它的块中都在作用域内，但在其声明前引用局部变量是非法的。也就是说，查找局部变量的尝试会成功，然后该使用将被视为错误。这只是 C# 的众多规则之一，旨在防止 C++ 程序中常见的错误。

## 布尔表达式

if 语句中的括号条件是**布尔表达式**。在列表 4.28 中，条件被高亮显示。

## 列表 4.28：布尔表达式

```csharp
if (input < 9)
{
    // Input is less than 9
    System.Console.WriteLine(
        $"Tic-tac-toe has more than { input }" +
        " maximum turns.");
}
// ...
```

布尔表达式出现在许多控制流语句中。它们的关键特征是始终求值为 true 或 false。为了使 `input < 9` 作为布尔表达式被允许，它必须结果为 `bool`。编译器不允许 `x = 42`，例如，因为该表达式为 `x` 赋值，结果是被赋值的值，而不是检查变量的值是否为 42。

