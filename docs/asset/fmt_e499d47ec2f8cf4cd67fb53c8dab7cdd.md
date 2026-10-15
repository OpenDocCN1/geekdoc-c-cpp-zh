
`string` `faxNumber`;

// ...

// Clear the value of `faxNumber`.

`faxNumber` = null;

// ...

```
```

将值 `null` 分配给引用类型并不等同于根本不分配它。换句话说，被赋值为 `null` 的变量仍然已被设置，而未被赋值的变量则未被设置，因此在使用前通常会导致编译错误。

将值 `null` 分配给 `string` 变量与分配空字符串 `""` 截然不同。使用 `null` 表示变量没有值，而 `""` 表示存在一个值——一个空字符串。这种区别可能非常有用。例如，编程逻辑可以将 `faxNumber` 为 `null` 解释为传真号码未知，而 `faxNumber` 的值为 `""` 则可能表示没有传真号码。

## The void “Type”

有时 C# 语法要求指定数据类型，但实际上并未传递任何数据。例如，如果方法不需要返回值，C# 允许你指定 `void` 作为数据类型而不是。HelloWorld 程序中 `Main` 的声明就是一个例子。`void` 作为返回类型的使用表示该方法不返回任何数据，并告诉编译器不要期望一个值。`void` 本身并不是一种数据类型，而是一种表示没有数据返回的指示。

### Language Contrast: C++

在 C++ 和 C# 中，`void` 有两种含义：作为方法不返回任何数据的标记，以及表示指向未知类型存储位置的指针。在 C++ 程序中，看到像 `void**` 这样的指针类型是很常见的。C# 也可以使用相同的语法表示指向未知类型存储位置的指针，但这种用法在 C# 中相对罕见，通常仅在编写与非托管代码库互操作的程序时才会遇到。

### Language Contrast: Visual Basic—Returning void Is Like Defining a Subroutine

在 C# 中返回 `void` 的 Visual Basic 等价物是定义一个子程序（`Sub/End Sub`），而不是返回值的函数。

## ADVANCED TOPIC

### Implicitly Typed Local Variables

C# 3.0 添加了一个上下文关键字 `var`，用于声明 **隐式类型局部变量**。只要代码在声明时使用类型明确的表达式初始化变量，C# 3.0 及更高版本就允许变量数据类型被推断而不是显式声明，如 Listing 2.18 所示。

```
**Listing 2.18: Working with Strings**

```csharp

class Uppercase

{

    static void Main()

    {

        System.Console.Write("Enter text: ");

        var text = System.Console.ReadLine();

        // Return a new string in uppercase

        var uppercase = text.ToUpper();

        System.Console.WriteLine(uppercase);

    }

}

```
```

此列表与 Listing 2.16 有两个不同之处。首先，而不是为声明使用显式数据类型 `string`，Listing 2.18 使用了 `var`。生成的 CIL 代码与显式使用 `string` 相同。然而，`var` 指示编译器应从分配给声明的值（`System.Console.ReadLine()`）中确定数据类型。

其次，变量 `text` 和 `uppercase` 通过其声明进行了初始化。不这样做会在编译时导致错误。如前所述，编译器确定初始化表达式的数据类型并相应地声明变量，就像程序员显式指定了类型一样。

尽管使用 `var` 而不是显式数据类型是允许的，但请考虑在数据类型已知时避免这种用法——例如，为 `text` 和 `uppercase` 的声明使用 `string`。这不仅使代码更易于理解，而且还验证了右侧表达式返回的数据类型是否为预期类型。当使用 `var` 声明的变量时，右侧的数据类型应该是显而易见的；如果不是，请考虑避免使用 `var` 声明。

对 `var` 的支持是在 C# 3.0 中添加的，以允许使用匿名类型。匿名类型是在方法内部“即时”声明的数据类型，而不是通过显式类定义，如 Listing 2.19 所示。（有关匿名类型的更多详细信息，请参阅第 14 章。）

## LISTING 2.19: Implicit Local Variables with Anonymous Types

```
class Program
{
    static void Main()
    {
        var patent1 =
            new { Title = "Bifocals", YearOfPublication = "1784" };
        var patent2 =
            new { Title = "Phonograph", YearOfPublication = "1877" };

        System.Console.WriteLine(
            $"{ patent1.Title } ({ patent1.YearOfPublication })");
        System.Console.WriteLine(
            $"{ patent2.Title } ({ patent2.YearOfPublication })");
    }
}
```

相应的输出显示在 Output 2.14 中。

## OUTPUT 2.14

```
Bifocals (1784)
Phonograph (1877)
```

Listing 2.19 演示了将匿名类型分配给隐式类型（`var`）局部变量。此类操作与 C# 3.0 对连接（关联）数据类型或将特定类型缩小为更少数据元素的支持一起提供了关键功能。

## Categories of Types

所有类型都属于两类之一：值类型和引用类型。每类类型之间的差异源于它们被复制的方式：值类型数据始终按值复制，而引用类型数据始终按引用复制。

## 值类型

到目前为止，本书中除 `string` 以外的所有预定义类型都是值类型。值类型的变量直接包含值。换句话说，变量引用的是存储该值的内存位置。因此，当给另一个变量赋值相同的值时，原始变量值的副本会被复制到新变量的位置。相同值类型的第二个变量不能引用与第一个变量相同的内存位置。因此，更改第一个变量的值不会影响第二个变量的值。图2.1演示了这一点。在图中，`number1` 引用包含值42的特定内存位置。将 `number1` 赋值给 `number2` 后，两个变量都将包含值42。但是，修改任一变量的值都不会影响另一个变量。

![](img/25683ccec0773ba5b8794b11f2b12877_100_0.png)

```csharp
//...
int number1 = 42;
char letter = 'A';
float pi = 3.14F;
int number2 = number1;
//...
```

**图2.1：** 值类型直接包含数据

类似地，将值类型传递给诸如 `Console.WriteLine()` 之类的方法也会导致内存复制，并且方法内部对参数的更改不会影响调用函数中的原始值。由于值类型需要内存复制，因此通常应将它们定义为消耗少量内存的类型；值类型的大小几乎总应小于16字节。

## 引用类型

相比之下，引用类型的值是对包含数据的存储位置的引用。引用类型存储数据所在位置的引用，而不是像值类型那样直接存储数据。因此，要访问数据，运行时将从变量中读取内存位置，然后“跳转”到包含该数据的内存位置。

引用类型所指向的数据的内存区域称为**堆**（参见图2.2）。

引用类型不需要像值类型那样复制数据本身，这使得复制引用类型比复制大型值类型高效得多。将一个引用类型变量的值赋给另一个引用类型变量时，只复制引用，而不复制所引用的数据。实际上，引用的大小总是与处理器的“本机大小”相同：32位处理器复制32位引用，64位处理器复制64位引用，依此类推。显然，将小型引用复制到大型数据块比像值类型那样复制整个数据块要快。

由于引用类型复制的是对数据的引用，两个不同的变量可以引用相同的数据。如果两个变量引用同一个对象，通过一个变量更改对象的字段后，通过另一个变量访问该字段时会看到更改的效果。这既发生在赋值中，也发生在方法调用中。因此，方法可以影响引用类型的数据，并且当控制权返回给调用者时可以观察到这种更改。因此，在定义引用类型或值类型之间进行选择时，一个关键因素是：对象在逻辑上是否像一个固定大小的不可变值（因此可能是值类型），还是像一个可以被引用的可变事物（因此很可能是引用类型）。

![](img/25683ccec0773ba5b8794b11f2b12877_101_0.png)

```csharp
//...
int number1 = 42;
char letter = 'A';
float pi = 3.14F;
int number2 = number1;
//...

using System.IO;

//...
string text =
    @"A cacophony of ramblings
    from my potpourri of notes";
StringReader reader =
    new StringReader(text);
//...
```

**图2.2：** 引用类型指向堆

除了 `string` 和任何自定义类（如 `Program`）之外，到目前为止讨论的所有类型都是值类型。然而，大多数类型都是引用类型。尽管可以定义自定义值类型，但与自定义引用类型的数量相比，这样做相对较少。

## 可空修饰符

值类型通常不能被赋值为 `null`，因为根据定义，它们不能包含引用，包括对“无”的引用。然而，这带来了一个问题，因为我们经常希望表示“缺失”的值。例如，在指定计数时，如果计数未知，你会输入什么？一种可能的解决方案是指定一个“魔法”值，如 `-1` 或 `int.MaxValue`，但这些是有效的整数。相反，最好将 `null` 赋给值类型，因为 `null` 不是有效的整数。

要声明可以存储 `null` 的值类型变量，可以使用可空修饰符 `?`。这个特性是在 C# 2.0 中引入的，如清单2.20所示。

**清单2.20：使用可空修饰符**

```csharp
static void Main()
{
    int? count = null;
    do
    {
        // ...
    }
    while(count == null);
}
```

在数据库编程中，将 `null` 赋值给值类型特别有吸引力。数据库表中的值类型列通常允许 `null` 值。检索这些列并将它们赋值给 C# 代码中的对应字段是有问题的，除非这些字段也能包含 `null`。幸运的是，可空修饰符正是专门为处理这种场景而设计的。

## 数据类型之间的转换

鉴于各种 CLI 实现中预定义了数千种类型，并且代码可以定义无限数量的类型，因此类型在合理情况下支持从一种类型到另一种类型的转换非常重要。最常见的转换操作是强制转换（casting）。

考虑两种数值类型之间的转换：将 `long` 类型的变量转换为 `int` 类型的变量。`long` 类型可以包含大到9,223,372,036,854,775,807的值；然而，`int` 的最大值是2,147,483,647。因此，这种转换可能会导致数据丢失——例如，如果 `long` 类型的变量包含的值大于 `int` 的最大值。任何可能导致数值大小丢失或因转换失败而引发异常的转换都需要显式强制转换。相反，无论操作数类型如何，都不会丢失数值大小且不会引发异常的转换操作是隐式转换。

### 显式强制转换

在 C# 中，使用强制转换运算符进行转换。通过将希望变量转换成的类型放在括号内指定，你承认如果发生显式强制转换，可能会损失精度和数据，或可能导致异常。清单2.21中的代码将 `long` 转换为 `int`，并明确告诉系统尝试该操作。

**清单2.21：显式强制转换示例**

```csharp
long longNumber = 50918309109;
int intNumber = (int)longNumber;
```

*强制转换运算符*

使用强制转换运算符，程序员基本上是在对编译器说：“相信我，我知道自己在做什么。我知道该值将适合放入

**清单2.23：一个Checked块示例**

```csharp
class Program
{
    static void Main()
    {
        checked
        {
            // int.MaxValue equals 2147483647
            int n = int.MaxValue;
            n = n + 1;
            System.Console.WriteLine(n);
        }
    }
}
```

输出2.16显示了结果。

**输出2.16**

```text
Unhandled Exception: System.OverflowException: Arithmetic operation resulted in an overflow at Program.Main() in ...Program.cs:line 12
```

结果是，如果在 `checked` 块内发生溢出赋值，运行时将抛出异常。

C# 编译器提供了一个命令行选项，可以将默认的 `checked` 行为从 `unchecked` 更改为 `checked`。C# 还支持 `unchecked` 块，该块允许数据溢出而不是为块内的赋值抛出异常（参见清单2.24）。

**清单2.24：一个Unchecked块示例**

```csharp
using System;

class Program
{
    static void Main()
    {
        unchecked
        {
            // int.MaxValue equals 2147483647
            int n = int.MaxValue;
            n = n + 1;
            System.Console.WriteLine(n);
        }
    }
}
```

**LISTING 2.25: 不使用强制转换运算符进行隐式转换**

```csharp
int intNumber = 31416;
long longNumber = intNumber;
```

即使不需要显式强制转换运算符（因为允许隐式转换），仍然可以包含强制转换运算符（参见列表 2.26）。

**LISTING 2.26: 对隐式转换使用强制转换运算符**

```csharp
int intNumber = 31416;
long longNumber = (long) intNumber;
```

## 无需强制转换的类型转换

未定义从字符串到数值类型的转换，因此需要使用诸如 `Parse()` 之类的方法。每个数值数据类型都包含一个 `Parse()` 函数，可实现从字符串到相应数值类型的转换。列表 2.27 演示了此调用。

**LISTING 2.27: 使用 int.Parse() 将字符串转换为数值数据类型**

```csharp
string text = "9.11E-31";
float kgElectronMass = float.Parse(text);
```

还有一种特殊类型可用于将一种类型转换为下一类型。此类型为 `System.Convert`，其使用示例出现在列表 2.28 中。

**LISTING 2.28: 使用 System.Convert 进行类型转换**

```csharp
string middleCText = "261.626";
double middleC = System.Convert.ToDouble(middleCText);
bool boolean = System.Convert.ToBoolean(middleC);
```

`System.Convert` 仅支持少量类型且不可扩展。它允许从 `bool`、`char`、`sbyte`、`short`、`int`、`long`、`ushort`、`uint`、`ulong`、`float`、`double`、`decimal`、`DateTime` 和 `string` 中的任何一种类型转换为这些类型中的任何其他类型。

此外，所有类型都支持 `ToString()` 方法，可用于提供类型的字符串表示形式。列表 2.29 演示了如何使用此方法。结果输出显示在输出 2.18 中。

## LISTING 2.29: 使用 ToString() 转换为字符串

```csharp
bool boolean = true;
string text = boolean.ToString();
// Display "True"
System.Console.WriteLine(text);
```

## OUTPUT 2.18

```text
True
```

对于大多数类型，`ToString()` 方法将返回数据类型名称而不是数据的字符串表示形式。只有当类型具有 `ToString()` 的显式实现时，才会返回字符串表示形式。最后一点是，可以编写自定义转换方法，并且运行时中的类提供了许多此类方法。

## ADVANCED TOPIC

## TryParse()

从 C# 2.0（.NET 2.0）开始，所有数值基元类型都包含静态 `TryParse()` 方法。此方法与 `Parse()` 方法非常相似，只是如果转换失败，`TryParse()` 方法不会抛出异常，而是返回 `false`，如列表 2.30 所演示。

## LISTING 2.30: 使用 TryParse() 代替无效强制转换异常
