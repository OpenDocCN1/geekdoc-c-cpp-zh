
以确定此类转换能够正确执行。列表 2.24 中的代码通过简单使用赋值运算符，将 `int` 转换为 `long`。

## 列表 2.24：未使用转换运算符进行隐式转换

```csharp
int intNumber = 31416;
long longNumber = intNumber;
```

即使不需要显式转换运算符（因为允许隐式转换），仍然可以包含转换运算符（参见列表 2.25）。

## 列表 2.25：使用转换运算符进行隐式转换

```csharp
int intNumber = 31416;
long longNumber = (long) intNumber;
```

## 无需转换的类型转换

从字符串到数值类型的转换未定义，因此需要使用诸如 `Parse()` 之类的方法。每种数值数据类型都包含一个 `Parse()` 函数，可用于从字符串转换为相应的数值类型。列表 2.26 演示了此调用。

## 列表 2.26：使用 `float.Parse()` 将字符串转换为数值数据类型

```csharp
string text = "9.11E-31";
float kgElectronMass = float.Parse(text);
```

还有一个特殊的类型可用于将一种类型转换为下一种类型。该类型是 `System.Convert`，其使用示例见列表 2.27。

## 列表 2.27：使用 `System.Convert` 进行类型转换

```csharp
string middleCText = "261.626";
double middleC = System.Convert.ToDouble(middleCText);
bool boolean = System.Convert.ToBoolean(middleC);
```

`System.Convert` 仅支持少量类型，且不可扩展。它允许从 `bool`、`char`、`sbyte`、`short`、`int`、`long`、`ushort`、`uint`、`ulong`、`float`、`double`、`decimal`、`DateTime` 和 `string` 中的任何类型转换为这些类型中的任何其他类型。

此外，所有类型都支持 `ToString()` 方法，该方法可用于提供类型的字符串表示。列表 2.28 演示了如何使用该方法。输出结果如输出 2.17 所示。

## 列表 2.28：使用 `ToString()` 转换为字符串

```csharp
bool boolean = true;
string text = boolean.ToString();
// Display "True"
System.Console.WriteLine(text);
```

## 输出 2.17

```
True
```

对于大多数类型，`ToString()` 方法返回数据类型的名称，而不是数据的字符串表示。只有当类型具有 `ToString()` 的显式实现时，才会返回字符串表示。最后需要指出的一点是，可以编写自定义转换方法，并且运行时中的许多类都提供了此类方法。

## 高级主题

### TryParse()

从 C# 2.0 (.NET 2.0) 开始，所有数值原始类型都包含一个静态 `TryParse()` 方法。该方法与 `Parse()` 方法类似，不同之处在于，如果转换失败，`TryParse()` 方法不会抛出异常，而是返回 `false`，如列表 2.29 所示。

## 列表 2.29：使用 `TryParse()` 替代无效转换异常

```csharp
double number;
string input;

System.Console.Write("Enter a number: ");
input = System.Console.ReadLine();
if (double.TryParse(input, out number))
{
    // Converted correctly, now use number
    // ...
}
else
{
    System.Console.WriteLine(
        "The text entered was not a valid number.");
}
```

输出 2.18 显示了列表 2.29 的结果。

## 输出 2.18

```
Enter a number: forty-two
The text entered was not a valid number.
```

代码从输入字符串中解析出的结果值通过 `out` 参数返回——在这种情况下，即为 `number`。

值得注意的是，从 C# 7.0 开始，不再需要在将变量用作 `out` 参数之前声明它。使用此特性，`number` 的声明如列表 2.30 所示。

## 列表 2.30：在 C# 7.0 中使用内联 `out` 声明调用 `TryParse()`

```csharp
// double number;
string input;

System.Console.Write("Enter a number: ");
input = System.Console.ReadLine();
if (double.TryParse(input, out double number))
{
    System.Console.WriteLine(
        $"{input} was parsed successfully to {number}.");
}
else
{
    // Note: number scope is here too (although not assigned)
    System.Console.WriteLine(
        "The text entered was not a valid number.");
}
```

请注意，`number` 的数据类型在 `out` 修饰符之后、它所声明的变量之前指定。结果是，`number` 变量在 `if` 语句的 `true` 和 `false` 分支中均可用，但在 `if` 语句外部不可用。

`Parse()` 和 `TryParse()` 之间的主要区别在于，如果 `TryParse()` 失败，它不会抛出异常。通常，从字符串到数值类型的转换取决于用户输入文本。在此类场景中，预计用户会输入无法成功解析的无效数据。通过使用 `TryParse()` 而不是 `Parse()`，可以避免在预期情况下抛出异常。（此处的预期情况是用户输入无效数据，我们试图避免在预期场景中抛出异常。）

## 总结

即使对于经验丰富的程序员，C# 也引入了几种新的编程结构。例如，作为数据类型部分的一部分，本章介绍了类型 `decimal`，可用于执行金融计算而不会浮点异常。此外，本章介绍了布尔类型 `bool` 不会隐式转换到或从整数类型这一事实，从而防止在条件表达式中错误地使用赋值运算符。C# 与其他许多前置语言的区别特征还包括 `@` 逐字字符串限定符，它强制字符串忽略转义字符；字符串插值，通过在字符串中嵌入代码使代码更易读；以及 `string` 数据类型的不可变性质。

在第 3 章中，我们将继续讨论数据类型，详细阐述两种数据类型：值类型和引用类型。此外，我们将查看如何将数据元素组合为元组和数组。

# 3 更多数据类型

在第 2 章中，我们涵盖了所有 C# 预定义类型，并简要讨论了引用类型与值类型的区别。在本章中，我们将继续讨论数据类型，进一步解释类型的类别。

![](img/ef6a8a417630b222bfb3f3b949facff0_113_0.png)

此外，我们将深入探讨将数据元素组合为元组——这是 C# 7.0 引入的一个功能——的细节，随后将数据分组为称为数组的集合。首先，让我们更深入地理解值类型和引用类型。

## 类型类别

所有类型都属于两个类别之一：值类型和引用类型。每个类别中类型的差异源于它们的复制方式：值类型数据总是按值复制，而引用类型数据总是按引用复制。

### 值类型

除了 `string` 之外，书中迄今为止介绍的所有预定义类型都是值类型。值类型的变量直接包含值。换句话说，变量引用存储值的同一内存位置。因此，当不同的变量被赋予相同的值时，原始变量的值会被复制到新变量的位置。同一值类型的第二个变量不能引用与第一个变量相同的内存位置。因此，改变第一个变量的值不会影响第二个变量的值，如图 3.1 所示。在图中，`number1` 指向内存中的特定位置，该位置包含值 42。将 `number1` 分配给 `number2` 后，两个变量都将包含值 42。但是，修改任何一个变量的值都不会影响另一个变量。

![](img/ef6a8a417630b222bfb3f3b949facff0_114_0.png)

**图 3.1：** 值类型直接包含数据

类似地，将值类型传递给诸如 `Console.WriteLine()` 之类的方法会导致内存复制，方法内对参数的任何更改都不会影响调用函数内的原始值。由于值类型需要内存复制，它们通常应定义为消耗少量内存；值类型的大小几乎总是应小于 16 字节。

## 引用类型

相比之下，引用类型变量的值是包含数据的存储位置的引用。引用类型存储数据位置的引用，而不是像值类型那样直接存储数据。

因此，为了访问数据，运行时从变量中读取内存位置，然后“跳转”到包含数据的内存位置。引用类型所指向的数据的内存区域称为**堆**（参见图 3.2）。

![](img/ef6a8a417630b222bfb3f3b949facff0_115_0.png)

## 图 3.2：引用类型指向堆

引用类型不像值类型那样需要数据的一份相同内存副本，这使得复制引用类型比复制大型值类型高效得多。将一个引用类型变量的值赋值给另一个引用类型变量时，只复制引用，而不复制所引用的数据。在实践中，引用的大小始终与处理器的“原生大小”相同：32 位处理器复制 32 位引用，64 位处理器复制 64 位引用，等等。显然，复制指向大块数据的小引用比像值类型那样复制整个数据块要快。

由于引用类型复制的是指向数据的引用，两个不同的变量可以引用同一数据。如果两个变量引用同一个对象，通过其中一个变量修改对象的字段，在通过另一个变量访问该字段时就能看到这种变化。这种情况既发生在赋值时，也发生在方法调用时。因此，方法可以影响引用类型的数据，并且当控制返回到调用者时，可以观察到这种变化。因此，在选择定义引用类型还是值类型时，一个关键因素是对象在逻辑上是否像一个固定大小的不可变值（因此可能是值类型），还是逻辑上是一个可变的、可被引用的事物（因此很可能是引用类型）。

除了字符串和诸如 `Program` 等自定义类外，到目前为止讨论的所有类型都是值类型。然而，大多数类型是引用类型。虽然可以定义自定义值类型，但与自定义引用类型的数量相比，这样做相对少见。

## 可空修饰符

值类型通常不能被赋值为 `null`，因为根据定义，它们不能包含引用，包括指向空事物的引用。然而，这带来了一个问题，因为我们经常希望表示“缺失”的值。例如，在指定数量时，如果数量未知，该输入什么？一种可能的解决方案是指定一个“魔法”值，例如 -1 或 `int.MaxValue`，但这些是有效的整数。相反，将 `null` 赋值给值类型是可取的，因为它不是一个有效的整数。

要声明可以存储 `null` 的值类型变量，请使用可空修饰符 `?`。此功能在 C# 2.0 中引入，如列表 3.1 所示。

**列表 3.1：使用可空修饰符**

```
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

将 `null` 赋值给值类型在数据库编程中尤其有吸引力。通常，数据库表中的值类型列允许 `null` 值。检索这些列并将它们赋值给 C# 代码中对应的字段会有问题，除非字段也能包含 `null`。幸运的是，可空修饰符正是为处理这种情况而设计的。

### 隐式类型局部变量

C# 3.0 添加了一个上下文关键字 `var`，用于声明**隐式类型局部变量**。只要代码在声明时用类型明确的表达式初始化变量，C# 3.0 及更高版本就允许隐含变量数据类型而不是明确说明，如列表 3.2 所示。

## 列表 3.2：操作字符串

```
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

此列表与列表 2.18 有两点不同。首先，不是使用显式数据类型 `string` 进行声明，列表 3.2 使用了 `var`。生成的 CIL 代码与显式使用 `string` 相同。然而，`var` 向编译器表明，它应该从声明中赋值的值（`System.Console.ReadLine()`）中确定数据类型。

其次，变量 `text` 和 `uppercase` 由其声明初始化。如果不这样做，将在编译时导致错误。如前所述，编译器确定初始化表达式的数据类型并相应地声明变量，就像程序员显式指定类型时所做的那样。

虽然允许使用 `var` 而不是显式数据类型，但当数据类型已知时，请考虑避免这种使用——例如，对 `text` 和 `uppercase` 的声明使用 `string`。这不仅使代码更易理解，还验证了右侧表达式返回的数据类型是否为预期类型。使用 `var` 声明的变量时，右侧的数据类型应当显而易见；如果不是，应避免使用 `var` 声明。

## 准则

除非所赋值的数据类型显而易见，否则**避免**使用隐式类型局部变量。

## 语言对比：C++/Visual Basic/JavaScript——void*、Variant 和 var

隐式类型变量并不等同于 C++ 中的 `void*`、Visual Basic 中的 `Variant` 或 JavaScript 中的 `var`。在这些情况中，变量声明的限制性不强，因为变量可以被赋值任意类型的值，就像在 C# 中使用类型为 `object` 的变量声明所做的那样。相比之下，`var` 由编译器确定类型；一旦在声明时确定，类型就不能改变，并且类型检查和成员调用在编译时进行验证。

## 高级主题

### 匿名类型

C# 3.0 在语言中添加了对 `var` 的支持，以允许使用匿名类型。匿名类型是那些在方法内部“即时”声明的数据类型，而不是通过显式的类定义，如列表 3.3 所示。（有关匿名类型的更多细节，请参见第 15 章。）

## 列表 3.3：带有匿名类型的隐式局部变量

```
class Program
{
    static void Main()
    {
        var patent1 =
            new { Title = "Bifocals",
                  YearOfPublication = "1784" };
        var patent2 =
            new { Title = "Phonograph",
                  YearOfPublication = "1877" };
        
        System.Console.WriteLine(
            "{0} ({1})", patent1.Title, patent1.YearOfPublication);
        System.Console.WriteLine(
            "{0} ({1})", patent2.Title, patent2.YearOfPublication);
    }
}
```

相应的输出如输出 3.1 所示。

## 输出 3.1

```
Bifocals (1784)
Phonograph (1877)
```

列表 3.3 演示了将匿名类型赋值给隐式类型（`var`）局部变量。这种操作与 C# 3.0 支持连接（关联）数据类型或将特定类型的大小减少到更少的数据元素的支持相结合，提供了关键功能。然而，C# 7.0 引入了元组语法，几乎取代了对匿名类型的需求。

## 元组

偶尔，你会发现将数据元素组合在一起是有用的。例如，考虑一个国家的信息，如 2017 年世界上最贫穷的国家：马拉维，其首都是利隆圭，人均 GDP 为 226.50 美元。根据我们目前建立的构造，我们可以将每个数据元素存储在单独的变量中，但结果将是这些数据元素之间没有关联。也就是说，除了可能在变量名称中共享后缀或前缀外，226.50 美元与马拉维之间没有关联。另一个选项是将所有数据合并到单个字符串中，缺点是要单独处理每个数据元素就需要将其解析出来。

C# 7.0 提供了第三种选项，即元组。元组允许你在单个语句中组合对每个变量的赋值，如下面的国家数据所示：

```
(string country, string capital, double gdpPerCapita) =
    ("Malawi", "Lilongwe", 226.50);
```

元组有几种额外的语法可能性，每个都在表 3.1 中展示。

## 表 3.1：元组声明和赋值的示例代码

| 示例 | 描述 | 示例代码 |

| :--- | :--- | :--- |

| 1. | 将元组分配给单独声明的变量。 | `(string country, string capital, double gdpPerCapital) =`<br>`("Malawi", "Lilongwe", 226.50);`<br>`System.Console.WriteLine(`<br>`$@"The poorest country in the world in 2017 was {`<br>`country}, {capital}: {gdpPerCapital}");` |
