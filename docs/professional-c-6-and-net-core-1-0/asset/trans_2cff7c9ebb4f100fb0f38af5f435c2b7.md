
错误。或者，你也可以选择在应用程序的上下文中派生自己的自定义 Exception 对象来描述错误情况。

假设用户接下来输入了一个不在 0 到 5 之间的数字。这个数字会被 if 语句检测到，然后实例化并抛出一个 IndexOutOfRangeException 对象。此时，应用程序会立即退出 try 块，并寻找能够处理 IndexOutOfRangeException 的 catch 块。它遇到的第一个 catch 块是：

```csharp
catch (IndexOutOfRangeException ex)
{
    WriteLine($"Exception: Number should be between 0 and 5. {ex.Message}");
}
```

由于这个 catch 块接收了适当类的参数，因此 catch 块会接收异常实例并执行。在这种情况下，你会显示一条错误信息以及 Exception.Message 属性（该属性对应于传递给 IndexOutOfRangeException 构造函数的字符串）。执行完这个 catch 块后，控制权会切换到 finally 块，就像没有发生异常一样。

请注意，在示例中你还提供了另一个 catch 块：

```csharp
catch (Exception ex)
{
    WriteLine($"An exception was thrown. Message was: {ex.Message}");
}
```

如果不是因为此类异常已经被前一个 catch 块捕获，这个 catch 块本来也能够处理 IndexOutOfRangeException。对基类的引用也可以引用从它派生的任何类的实例，并且所有异常都派生自 Exception。当抛出 IndexOutOfRangeException 类型的异常时，这个 catch 块不会被执行，因为应用程序只会从可用的 catch 块列表中执行它找到的第一个合适的 catch 块。第二个 catch 块会捕获从 Exception 基类派生的其他异常。请注意，try 块中对方法的三次单独调用（Console.ReadLine、Console.Write 和 Convert.ToInt32）可能会抛出其他异常。

如果用户输入了不是数字的内容——比如 a 或 hello——Convert.ToInt32 方法会抛出 System.FormatException 类的异常，以指示传入 ToInt32 的字符串不是可以转换为 int 的格式。当这种情况发生时，应用程序会回溯方法调用，寻找能够处理此异常的处理器。你的第一个 catch 块（接收 `IndexOutOfRangeException` 的那个）不适用。然后应用程序会查看第二个 `catch` 块。这个块适用，因为 `FormatException` 派生自 `Exception`，所以 `FormatException` 实例可以在此处作为参数传入。

这个示例的结构实际上是具有多个 `catch` 块时的典型情况。你从设计用于捕获特定错误条件的 `catch` 块开始，然后以更通用的块结束，以涵盖你没有编写特定错误处理程序的所有错误。事实上，`catch` 块的顺序很重要。如果你将前面两个块按相反的顺序编写，代码将无法编译，因为第二个 `catch` 块是不可达的（`Exception catch` 块会捕获所有异常）。因此，最顶层的 `catch` 块应该是可用的最细粒度的选项，最后以最通用的选项结束。

现在你已经分析了示例的代码，可以运行它了。以下输出说明了不同输入会发生什么情况，并演示了抛出的 `IndexOutOfRangeException` 和 `FormatException`：

```text
SimpleExceptions
Input a number between 0 and 5 (or just hit return to exit)> 4
Your number was 4
Thank you

Input a number between 0 and 5 (or just hit return to exit)> 0
Your number was 0
Thank you

Input a number between 0 and 5 (or just hit return to exit)> 10
Exception: Number should be between 0 and 5. You typed in 10
Thank you

Input a number between 0 and 5 (or just hit return to exit)>
hello
An exception was thrown. Message was: Input string was not in a correct format.
Thank you

Input a number between 0 and 5 (or just hit return to exit)>
Thank you
```

## 捕获来自其他代码的异常

前面的示例演示了两种异常的处理。其中，`IndexOutOfRangeException` 是由你自己的代码抛出的，另一个 `FormatException` 是从某个基类内部抛出的。库代码在检测到问题发生，或者某个方法因被传入错误参数而被不恰当地调用时，抛出异常是非常常见的。然而，库代码很少尝试捕获异常；这被认为是客户端代码的责任。

通常，在调试时，异常会从基类库中抛出。调试的过程在某种程度上涉及确定异常为何被抛出并消除原因。你的目标应该是确保在实际发布代码时，异常只在非常特殊的情况下发生，并且如果可能，在你的代码中得到适当处理。

## System.Exception 属性

该示例仅演示了异常对象 `Message` 属性的使用。然而，`System.Exception` 中还有许多其他可用属性，如下表所示。

| 属性 | 描述 |
|---|---|
| `Data` | 允许你向异常添加键/值语句，这些语句可用于提供有关异常的额外信息。 |
| `HelpLink` | 指向提供有关异常更多信息的帮助文件的链接。 |
| `InnerException` | 如果此异常是在 `catch` 块内部抛出的，则 `InnerException` 包含使代码进入该 `catch` 块的异常对象。 |
| `Message` | 描述错误情况的文本。 |
| `Source` | 导致异常的应用程序或对象的名称。 |
| `StackTrace` | 提供有关堆栈上方法调用的详细信息（以帮助追踪抛出异常的方法）。 |

如果堆栈跟踪可用，`StackTrace` 的属性值由 .NET 运行时自动提供。`Source` 总是由 .NET 运行时填写为引发异常的程序集名称（尽管你可能希望在代码中修改该属性以提供更具体的信息），而 `Data`、`Message`、`HelpLink` 和 `InnerException` 必须由抛出异常的代码在抛出异常之前立即设置这些属性来填充。例如，抛出异常的代码可能如下所示：

```csharp
if (ErrorCondition == true)
{
    var myException = new ClassMyException("Help!!!!");
    myException.Source = "My Application Name";
    myException.HelpLink = "MyHelpFile.txt";
    myException.Data["ErrorDate"] = DateTime.Now;
    myException.Data.Add("AdditionalInfo", "Contact Bill from the Blue Team");
    throw myException;
}
```

这里，`ClassMyException` 是你正在抛出的特定异常类的名称。请注意，所有异常类的名称通常都以 `Exception` 结尾。另外，请注意 `Data` 属性有两种赋值方式。

## 异常筛选器

C# 6 的一个新功能是异常筛选器。你可以让不同的 catch 块在捕获不同类型的异常时表现出不同的行为。在某些场景下，根据异常的内容让 catch 块表现出不同的行为会很有用。例如，在使用 Windows 运行时，你经常会为各种不同类型的异常获取 COM 异常；或者在进行网络调用时，你可能会在许多不同的场景下获得网络异常——例如，服务器不可用，或提供的数据不符合预期。最好能对这些错误做出不同的反应。有些异常可以通过不同的方式恢复，而对于其他异常，用户可能需要一些信息。

以下代码示例抛出了 MyCustomException 类型的异常，并设置了该异常的 ErrorCode 属性（代码文件 ExceptionFilters/Program.cs）：

```csharp
public static void ThrowWithErrorCode(int code)
{
    throw new MyCustomException("Error in Foo") { ErrorCode = code };
}
```

在 Main 方法中，try 块使用两个 catch 块来保护方法调用。第一个 catch 块使用 when 关键字，仅筛选 ErrorCode 属性等于 405 的异常。when 子句的表达式需要返回一个布尔值。如果结果为 true，则此 catch 块处理该异常。如果为 false，则会查找其他 catch 块。向 ThrowWithErrorCode 方法传递 405 时，筛选器返回 true，第一个 catch 处理该异常。传递其他值时，筛选器返回 false，第二个 catch 处理该异常。使用筛选器，你可以有多个处理程序来处理相同的异常类型。

当然，你也可以移除第二个 catch 块，在这种情况下不处理该异常。

```csharp
try
{
    ThrowWithErrorCode(405);
}
catch (MyCustomException ex) when (ex.ErrorCode == 405)
{
    WriteLine($"Exception caught with filter {ex.Message} and {ex.ErrorCode}");
}
catch (MyCustomException ex)
{
    WriteLine($"Exception caught {ex.Message} and {ex.ErrorCode}");
}
```

## 重新抛出异常

