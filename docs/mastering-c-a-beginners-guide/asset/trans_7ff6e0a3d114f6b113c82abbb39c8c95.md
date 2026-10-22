

# 逻辑运算符

逻辑运算符用于执行逻辑操作。逻辑运算符处理布尔表达式并返回布尔值。逻辑运算符与条件运算符一起用于循环和决策语句中。

逻辑运算符及其用法。

- 逻辑与运算符
  **符号：** "&&"
  
  当两个值都为 true 时，与运算符返回 true。如果任一值为 false，则返回 false。
  
  例如，A && B 如果 A 和 B 都为 true 则返回 true，如果任一或两者为 false 则返回 false。

- 逻辑或运算符
  **符号：** "||"
  
  如果任一条件/操作数为 true，逻辑或运算符返回 true。当两个操作数都为 false 时，返回 false。
  
  例如，A || B 如果 A 或 B 的值为 true 则返回 true。如果 A 和 B 都为 false，则返回 false。

- 逻辑非运算符
  **符号：** "!"

# 赋值运算符

赋值运算符用于为变量赋值。它们通常用于算术运算符之前。

让我们看看 C# 提供的赋值运算符：

- **等于（“=”）：** 它是最简单的赋值运算符之一。它将一个操作数的值赋给另一个操作数。例如，右侧操作数的值赋给左侧操作数。
  - **示例：** a = b

- **加等于赋值运算符：** 顾名思义，它是加号“+”和等号“=”的组合。它写作“+=”，将右侧操作数加到左侧操作数，并将最终值存储在左侧操作数中。
  - **示例：** a += b 表示 (a = a + b)

- **减等于赋值运算符：** 类似于加等于，它从左侧操作数中减去右侧操作数的值，然后将值赋给左侧操作数。
  - **示例：** a -= b 表示 (a = a - b)

- **除等于赋值运算符：** 它将右侧操作数的值除以左侧操作数，然后将结果存储在左侧操作数中。
  - **示例：** a /= b 表示 (a = a / b)

- **乘等于赋值运算符：** 它将右侧操作数的值乘以左侧操作数，然后将结果存储在左侧操作数中。
  - **示例：** a *= b 表示 (a = a * b)

- **模等于赋值运算符：** 它计算左右操作数的模，并将值存储在左侧操作数中。
  - **示例：** a %= b 表示 (a = a % b)

下面给出一个程序以更清晰地说明：

```
int a = 10;
int b = 5;
a += b;            //1
Console.WriteLine(a);
a -= b;            //2
Console.WriteLine(a);
a /= b;            //3
Console.WriteLine(a);
a *= b;            //4
Console.WriteLine(a);
a %= b;            //5
Console.WriteLine(a);
```

- **输出：**
  第一个值将返回 15，即 a = a + b。
  第二个运算符将返回 10，即 a = a - b。
  第三个运算符将返回 2，即 a = a / b。
  第四个运算符将返回 50，即 a = a * b。
  第五个运算符将返回 0，即 a = a % b。

值得提及的其他运算符包括：

| 运算符 | 描述 | 示例 |
|---|---|---|
| Sizeof() | 返回指定变量的大小 | Sizeof(a)，其中 a 为整数将返回 4 |
| & | 返回变量的地址 | &a; 返回变量的实际地址 |
| * | 指向变量的指针 | *a: |
| ?: | 条件表达式 | 如果条件为真？则取 x 值：否则取 Y 值 |

用一个示例来说明：

```
/*A C Program for Misc. Operators*/
#include <stdio.h>
int main()
{
int num1 = 4;
short num2;
double num3;
int* ptr;

/* example of sizeof operator */
printf("Line 1 - Size of variable num1 = %d\n", sizeof(num1) );
printf("Line 2 - Size of variable num2 = %d\n", sizeof(num2) );
printf("Line 3 - Size of variable num3= %d\n", sizeof(num3) );
```

```
/* example of & and * operators */
ptr = &num1; /* 'ptr' now contains the address of 'num1'*/
printf("Value of num1 is %d\n", num1);
printf("*ptr is %d.\n", *ptr);

/* example of ternary operator */
num1 = 10;
num2 = (num1 == 1)? 20: 30;
printf( "Value of num2 is %d\n", num2 );
num2 = (num1 == 10)? 20: 30;
printf( "Value of num2 is %d\n", num2 );
return 0;
}
```

- **输出：**
  - num1 的值是 4。
  - *ptr 的值是 4。
  - num2 的值是 30。
  - num2 的值是 20。

# 探索用户定义类型

## 本章目录

- 类与对象
- 结构体
- 枚举
- 命名空间

在本章中，我们将学习如何使用类、结构体和枚举来创建自定义用户类型。我们将探讨类中的字段、属性、方法、索引器和构造函数是什么。我们将研究 C# 中的访问修饰符，并学习如何使用它们来定义类型和成员的可见性。

类是相似类型对象的逻辑集合。它是 C# 中最基本的类型之一。它是一种数据结构，由方法、函数和字段组成。它定义了动态实例，即需要为类创建的对象。

编程语言中的对象与现实世界中的对象几乎相似。面向对象编程是一种思想，其中程序使用一组类和对象来设计，以简化程序开发和维护。

## 类与对象

C# 中的类由关键字 class 定义，后面跟着类的标识符（名称）以及不同代码块中的数据成员和方法。

C# 中的类可以包含以下元素：

- **字段：** 特定类型的成员变量。
- **属性：** 这些是特定类型的元素，通过在类字段中提取和记录时提供额外的数据管理来扩展字段的功能。
- **方法：** 它们设计用于操作数据。

我们将给出一个 C# 类的示例，其中包含所列的元素。Cat 类模拟现实世界中的对象“猫”，并具有精确的名称和颜色属性。给定的类定义了几个方法、字段和属性。让我们看看该类的定义。

```
public class Cat
{
    // Field name
    private string name;
    // Field color
    private string color;
    public string Name
    {
        // Getter of the property "Name."
        get
        {
            return this.name;
        }
        // Setter of the property "Name"
        set
        {
            this.name = value;
        }
    }
    public string Color
    {
        // Getter of the property "Color"
        get
        {
            return this.color;
        }
        // Setter of the property "Color"
        set
        {
            this.color = value;
        }
    }
    // Default constructor
    public Cat()
    {
        this.name = "Unnamed";
        this.color = "gray";
    }
```

```
```csharp
// Constructor with parameters
public Cat (string name, string color)
{
    this.name = name;
    this.color = color;
}

// Method SayMiau
public void SayMiau()
{
    Console.WriteLine("Cat {0} said:\nMiauuuuu!", name);
}
}
```
```

示例 Cat 类解释了属性 name 和 color，这两个属性将值保存在隐藏的（私有）字段 name 和 color 中。不仅如此，为了创建 Cat 类的实例，还定义了两个构造函数，分别带参数和不带参数，以及类的方法 SayMiau()。在示例类定义之后，我们现在可以按如下方式使用它：

```
```csharp
static void Main()
{
    Cat firstCat = new Cat();
    firstCat.Name = "Tony";
    firstCat.SayMiau();

    Cat secondCat = new Cat("Pepy", "red");
    secondCat.SayMiau();
    Console.WriteLine("Cat {0} is {1}.",
        secondCat.Name, secondCat.Color);
}
```
```

如果我们运行该示例，将得到以下输出：

- Cat Tony said: Miauuuuuu!
- Cat Pepy said: Miauuuuuu!
- Cat Pepy is Red.

我们看到了一个清晰的类定义和使用示例，在“创建和使用对象”一节中，我们将详细解释如何创建对象、如何访问其属性以及如何调用其方法，这将帮助我们理解该示例的工作原理。

## 系统类

调用 System.Console 类的 Console.WriteLine(...) 方法是 C# 中系统类用法的一个示例。我们可以将系统类定义为标准库中定义的类，用于使用 C#（或其他编程语言）构建应用程序。它们可以在 .NET 应用程序（尤其是用 C# 编写的应用程序）中使用。例如，String、Math 和 Environment 等类。

我们可能已经知道，.NET Framework SDK 附带了一组编程语言（如 C# 和 VB.NET）、编译器和标准类库，提供了数千个系统类，用于完成编程中最常见的任务，如文本处理、基于控制台的输入/输出、集合类、网络、并行执行、数据库访问、数据处理，以及开发基于 Web 的图形用户界面（GUI）和移动应用程序。

