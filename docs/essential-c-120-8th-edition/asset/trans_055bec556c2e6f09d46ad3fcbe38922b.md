
本章剩余部分将介绍匿名类型主题，以便如果你在处理 C# 7.0 之前编写的代码，仍然能够理解匿名类型这一语言特性。

# 匿名类型

匿名类型是由编译器声明的数据类型，而不是通过第 6 章中引入的显式类定义引入。与匿名函数一样，当编译器看到匿名类型时，它会为你完成相关工作，然后让你像已经显式声明过它一样使用它。列表 15.26 显示了这样的声明。对应的输出见输出 15.13。

列表 15.26：带有匿名类型的隐式局部变量

```c
using System;

public class Program
{
    public static void Main()
    {
        var patent1 = 
            new {
                Title = "Bifocals"
```

```c
Console.WriteLine();
Console.WriteLine(patent1);
Console.WriteLine(patent2);
```

```c
Console.WriteLine();
Console.WriteLine(patent3);
```

```c
}
```

# 输出 15.13

Bifocals (1784)
Phonograph (1784)
{ Title = Bifocals, YearOfPublication = 1784 }
{ Title = Phonograph, YearOfPublication = 1877 }
{ Title = Bifocals, Year = 1784 }

匿名类型纯粹是 C# 的特性，而不是运行时的一种新类型类型。当编译器遇到匿名类型语法时，它会生成一个 CIL 类，其属性与匿名类型声明中的命名值和数据类型对应。

# 初学者主题

## 复习隐式类型局部变量 (var)

由于匿名类型没有名称，因此无法将局部变量显式声明为匿名类型。相反，局部变量的类型被替换为 `var`。然而，这并不意味着隐式类型变量是无类型的。相反，它们被完全类型化为所赋值的值的数据类型。如果给隐式类型变量赋值一个匿名类型，则该局部变量声明的底层 CIL 代码类型为编译器生成的类型。同样，如果给隐式类型变量赋值一个字符串，它在底层 CIL 中的数据类型就是字符串。事实上，对于赋值值不是匿名类型（如字符串）的隐式类型变量，与使用显式类型声明的变量相比，其生成的 CIL 代码没有区别。如果声明语句文本为 `text = "This is a test of the..."`，生成的 CIL 代码与隐式类型声明 `var text = "This is a test of the..."` 是相同的。

编译器从赋值的表达式中确定隐式类型变量的数据类型。在带有初始化器的显式类型局部变量中（`string s = "hello";`），编译器首先根据左侧的声明类型确定 `s` 的类型，然后分析右侧，并验证右侧的表达式可以赋值给该类型。在隐式类型变量中，这个过程在某种程度上是反向的。首先分析右侧以确定其类型，然后在逻辑上将 `var` 替换为该类型。

尽管 C# 没有为匿名类型提供名称，但它也是强类型的。例如，该类型的属性是完全可以访问的。在列表 15.26 中，`patent1.Title` 和 `patent2.YearOfPublication` 在 `Console.WriteLine` 语句中被调用。任何调用不存在成员的尝试都将导致编译错误。即使是 Visual Studio 等 IDE 中的 IntelliSense 也能处理匿名类型。

你应该谨慎地使用隐式类型变量声明。显然，对于匿名类型，无法指定数据类型，且必须使用 `var`。然而，如果数据类型不是匿名类型，通常使用显式数据类型更好。

与通常情况一样，你应该专注于提高代码语义的可读性，同时利用编译器验证结果变量类型是否是你预期的类型。要通过隐式类型局部变量实现这一点，仅当赋值给隐式类型变量的类型完全明显时才使用它们。例如，在 `var items = new Dictionary<string, List<Account>>();` 中，生成的代码更简洁易读。相比之下，当类型不明显时（例如赋值方法的返回值时），开发者应该倾向于使用显式变量类型声明，如下：

```c
Dictionary<string, List<Account>> dictionary = GetAccounts();
```

## 使用 LINQ 选择匿名类型

最后，利用匿名类型，我们可以创建一个 `IEnumerable<T>` 集合，其中 `T` 是匿名类型（见列表 15.27 和输出 15.14）。

列表 15.27：投影到匿名类型

```c
//...
IEnumerable<string> fileList = Directory.EnumerateFiles(
    rootDirectory, searchPath);
var items = fileList.Select(
    {
        FileInfo fileInfo = new(file);
        return new
        {
            FileName = fileInfo.Name,
            Size = fileInfo.Length
        }
    });
//...
```

输出 15.14

```
{ FileName = AssemblyInfo.cs, Size = 1704 }
{ FileName = CodeAnalysisRules.xml, Size = 735 }
{ FileName = CustomDictionary.xml, Size = 199 }
{ FileName = EssentialCSharp.sln, Size = 40415 }
{ FileName = EssentialCSharp.vsmdi, Size = 454656 }
{ FileName = EssentialCSharp, Size = 499 }
{ FileName = EssentialCSharp.vssscc, Size = 256 }
{ FileName = intelliectchure.ConsoleTester.dll, Size = 24576 }
{ FileName = intelliectchure.ConsoleTester.db, Size = 30288 }
```

匿名类型的输出会自动显示由与匿名类型关联的 `ToString()` 方法生成的属性名和值。

使用 `Select()` 方法进行投影是非常强大的。我们已经看到如何使用 `Where()` 标准查询操作符垂直方向过滤集合（减少集合中的项数量）。现在，通过使用 `Select()` 标准查询操作符，我们也可以水平方向减少集合（减少列数）并完全转换数据。通过添加匿名类型，我们可以通过 `Select()` 提取任意“对象”，只需提取原始集合中当前算法需要的片段，而无需声明一个类来包含它们。

## 关于匿名类型和隐式局部变量的更多信息

在列表 15.26 中，匿名类型的成员名称通过将 `patent1` 和 `patent2` 的值赋值给名称来显式识别（例如 `Title = "Phonograph"`）。然而，如果赋值值是属性或字段调用，名称可能默认为字段或属性的名称，而不是显式指定值。例如，`patent3` 使用命名为 `Title` 的属性定义。如输出 15.13 所示，生成的属性名由编译器确定，与获取值来源的属性匹配。

`patent1` 和 `patent2` 具有相同的属性名和相同的数据类型。因此，C# 编译器为这些匿名声明只生成了一个数据类型。相比之下，`patent3` 强制编译器创建第二个匿名类型，因为年份属性名称与 `patent1` 和 `patent2` 不同。此外，如果交换了 `patent1` 和 `patent2` 的属性顺序，这两个匿名类型将不具有类型性。换句话说，两个匿名类型在同一程序集中类型兼容的要求是：属性名、数据类型和属性顺序匹配。如果满足了这些标准，即使它们出现在不同的方法或类中，类型也是兼容的。列表 15.28 展示了类型不兼容的情况。

# 列表 15.28：匿名类型的类型安全性和不可变性

```c
public class Program
{
    public static void Main()
    {
        var patent1 = 
            new{
                Title = "Bifocals",
                YearOfPublication = "1784"
            };
    }
    var patent2 =
```

