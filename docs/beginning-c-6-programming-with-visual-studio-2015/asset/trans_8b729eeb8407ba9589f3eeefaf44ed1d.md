

```csharp
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.CSharp.RuntimeBinder;
namespace Ch13Ex06
{
    class MyClass1
    {
        public int Add(int var1, int var2) => var1 + var2;
    }
    class MyClass2 {}
    class Program
    {
        static int callCount = 0;
        static dynamic GetValue()
        {
            if (callCount++ == 0)
            {
                return new MyClass1();
            }
            return new MyClass2();
        }
        static void Main(string[] args)
        {
            try
            {
                dynamic firstResult = GetValue();
                dynamic secondResult = GetValue();
                WriteLine($"firstResult is: {firstResult.ToString()}");
                WriteLine($"secondResult is: {secondResult.ToString()}");
                WriteLine($"firstResult call: {firstResult.Add(2, 3)}");
                WriteLine($"secondResult call: {secondResult.Add(2, 3)}");
            }
            catch (RuntimeBinderException ex)
            {
                WriteLine(ex.Message);
            }
            ReadKey();
        }
    }
}
```

- 3. 运行应用程序。结果如图 13-17 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_409_0.png)

图 13-17

## 工作原理

在本示例中，你使用一个返回两种对象类型之一的方法来获取动态值，然后尝试使用所获取的对象。代码可以顺利编译，但在尝试访问不存在的方法时会抛出异常（并被处理）。

首先，添加一个用于引入包含 `RuntimeBinderException` 异常的命名空间的 using 语句：

```
using Microsoft.CSharp.RuntimeBinder;
```

接下来，定义两个类 `MyClass1` 和 `MyClass2`，其中 `MyClass1` 具有 `Add()` 方法，而 `MyClass2` 不包含任何成员：

```
class MyClass1
{
    public int Add(int var1, int var2) => var1 + var2;
}
class MyClass2
{
}
```

然后，在 `Program` 类中添加一个字段（`callCount`）和一个方法（`GetValue()`），以提供获取这两个类中某个类实例的方式：

```
static int callCount = 0;
static dynamic GetValue()
{
    if (callCount++ == 0)
    {
        return new MyClass1();
    }
    return new MyClass2();
}
```

这里使用了一个简单的调用计数器，使该方法在第一次调用时返回 `MyClass1` 的实例，之后返回 `MyClass2` 的实例。请注意，`dynamic` 关键字可以用作方法的返回类型。

接下来，`Main()` 中的代码调用 `GetValue()` 方法两次，然后依次尝试对返回的两个值调用 `ToString()` 和 `Add()`。这段代码被放在 `try...catch` 块中，用于捕获可能发生的 `RuntimeBinderException` 类型的异常：

```
static void Main(string[] args)
{
    try
    {
        dynamic firstResult = GetValue();
        dynamic secondResult = GetValue();
        WriteLine($"firstResult is: {firstResult.ToString()}");
        WriteLine($"secondResult is: {secondResult.ToString()}");
        WriteLine($"firstResult call: {firstResult.Add(2, 3)}");
        WriteLine($"secondResult call: {secondResult.Add(2, 3)}");
    }
    catch (RuntimeBinderException ex)
    {
        WriteLine(ex.Message);
    }
    ReadKey();
}
```

果然，在调用 `secondResult.Add()` 时会抛出异常，因为 `MyClass2` 中不存在这样的方法。异常消息会准确地告诉你这一点。

`dynamic` 关键字还可以用于其他需要类型名称的位置，例如方法参数。你可以按如下方式重写 `Add()` 方法：

```
public int Add(dynamic var1, dynamic var2) => var1 + var2;
```

这不会对结果产生任何影响。在这种情况下，运行时会检查传递给 `var1` 和 `var2` 的值，以确定是否存在与 `+` 兼容的运算符定义。在传递两个 `int` 值的情况下，这样的运算符确实存在。如果使用了不兼容的值，则会抛出 `RuntimeBinderException` 异常。例如，如果你尝试执行：

```
WriteLine($"firstResult call: {0}", firstResult.Add("*2", 3));
```

异常消息如下：

```
Cannot implicitly convert type 'string' to 'int'
```

这里需要吸取的教训是，动态类型非常强大，但同时也需要注意其中的风险。如果使用强类型而不是动态类型，这类异常完全可以避免。对于你编写的大多数 C# 代码，应避免使用 `dynamic` 关键字。不过，如果确实遇到必须使用它的情况，那就放心使用并充分发挥它的作用吧——同时也应替过去那些无法使用这一强大工具的程序员感到一丝遗憾。

## 高级方法参数

C# 4 扩展了定义和使用方法参数时的可能性。这主要是为了解决使用外部定义的接口时出现的特定问题，例如 Microsoft Office 编程模型。在这类模型中，某些方法公开了大量参数，而这些参数并非每次调用都需要。过去，这意味着必须想办法指定缺少的参数，或者代码中会出现大量 `null`：

```
RemoteCall(var1, var2, null, null, null, null, null);
```

在这段代码中，完全无法直观地看出这些 `null` 值分别对应什么，也不清楚为什么要省略这些参数。

也许在理想情况下，应该为 `RemoteCall()` 方法提供多个重载，其中包括一个只需要两个参数的重载，如下所示：

```
RemoteCall(var1, var2);
```

假设你只想为第三个可选参数传递一个值。仅使用上一节介绍的语法时，如果不为第一个和第二个可选参数提供值，就无法做到这一点。

C# 4 还引入了命名参数，使你可以指定所需的任意参数。这不要求你对方法定义做任何特殊处理；它是一种在调用方法时使用的技术。语法如下：

```
MyMethod(
    <param1Name>: <param1Value>,
    ...
    <paramNName>: <paramNValue>);
```

只要命名参数确实存在，你就可以用这种方式指定任意数量的参数，而且参数顺序可以任意。命名参数也可以是可选的。

如果愿意，你还可以在一次方法调用中只对部分参数使用命名参数。当方法签名中有多个可选参数，但同时包含一些必需参数时，这种方式尤其有用。你可以先指定必需参数，然后以命名的可选参数结束调用。例如：

```
MyMethod(
    requiredParameter1Value,
    optionalParameter5: optionalParameter5Value);
```

不过，如果混合使用命名参数和位置参数，请注意必须先包含所有位置参数，然后才能包含命名参数。但是，只要始终使用命名参数，你也可以根据需要使用不同的顺序，如下例所示：

```
MyMethod(
    optionalParameter5: optionalParameter5Value,
    requiredParameter1: requiredParameter1Value);
```

如果这样做，则必须为所有必需参数提供值。

在下面的“动手试一试”中，你将看到如何使用命名参数和可选参数。

### 动手试一试：使用命名参数和可选参数：Ch13Ex07

- 1. 创建一个名为 `Ch13Ex07` 的新控制台应用程序，并将其保存到目录 `C:\BegVCSharp\Chapter13` 中。
- 2. 向项目中添加一个名为 `WordProcessor` 的类，并按如下方式修改其代码：

```csharp
public static class WordProcessor
{
    public static List<string> GetWords(
        string sentence,
        bool capitalizeWords = false,
        bool reverseOrder = false,
        bool reverseWords = false)
    {
        List<string> words = new List<string>(sentence.Split(' '));
        if (capitalizeWords)
            words = CapitalizeWords(words);
        if (reverseOrder)
            words = ReverseOrder(words);
        if (reverseWords)
            words = ReverseWords(words);
        return words;
    }

    private static List<string> CapitalizeWords(List<string> words)
    {
        List<string> capitalizedWords = new List<string>();
        foreach (string word in words)
        {
            if (word.Length == 0)
                continue;
            if (word.Length == 1)
                capitalizedWords.Add(
                    word[0].ToString().ToUpper());
            else
                capitalizedWords.Add(
                    word[0].ToString().ToUpper()
                    + word.Substring(1));
        }
        return capitalizedWords;
    }

    private static List<string> ReverseOrder(List<string> words)
    {
        List<string> reversedWords = new List<string>();
        for (int wordIndex = words.Count - 1;
            wordIndex >= 0; wordIndex--)
            reversedWords.Add(words[wordIndex]);
        return reversedWords;
    }

    private static List<string> ReverseWords(List<string> words)
    {
        List<string> reversedWords = new List<string>();
        foreach (string word in words)
            reversedWords.Add(ReverseWord(word));
        return reversedWords;
    }

    private static string ReverseWord(string word)
    {
        StringBuilder sb = new StringBuilder();
        for (int characterIndex = word.Length - 1;
            characterIndex >= 0; characterIndex--)
            sb.Append(word[characterIndex]);
        return sb.ToString();
    }
}
```

- 3. 按如下方式修改 `Program.cs` 中的代码：

```csharp
static void Main(string[] args)
{
```

