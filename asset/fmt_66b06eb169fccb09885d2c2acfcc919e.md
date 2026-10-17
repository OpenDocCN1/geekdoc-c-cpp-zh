
Calling DoesNotThrowException
DoesNotThrowException
finally executed in DoesNotThrowException
End of DoesNotThrowException

Calling ThrowExceptionWithCatch
In ThrowExceptionWithCatch
Message: Exception in ThrowExceptionWithCatch
finally executed in ThrowExceptionWithCatch
End of ThrowExceptionWithCatch

Calling ThrowExceptionWithoutCatch
In ThrowExceptionWithoutCatch
finally executed in ThrowExceptionWithoutCatch
Caught exception from ThrowExceptionWithoutCatch in Main

Calling ThrowExceptionCatchRetrow
In ThrowExceptionCatchRetrow
Message: Exception in ThrowExceptionCatchRetrow
Wait, let me re-read... 
Calling ThrowExceptionCatchRetrow
In ThrowExceptionCatchRetrow
Message: Exception in ThrowExceptionCatchRetrow
finally executed in ThrowExceptionCatchRetrow
Caught exception from ThrowExceptionCatchRetrow in Main

图 13.4 | finally 块总是执行的，即使在没有发生异常时也是。（4 部分中的 4 部分）

Main 的第 12 行调用了方法 `DoesNotThrowException`。该方法的 `try` 块输出一条消息（第 55 行）。因为 `try` 块没有抛出任何异常，程序控制忽略 `catch` 块（第 57–60 行）并执行 `finally` 块（第 61–64 行），该块会输出一条消息。此时，程序控制继续执行 `finally` 块之后的语句（第 66 行），该语句输出一条消息，表示已到达方法末尾。然后程序控制返回 `Main`。

## 13.5.4 使用 throw 语句抛出异常

`Main` 的第 16 行调用了方法 `ThrowWithCatch`（第 70–89 行），该方法在其 `try` 块（第 73–77 行）中开始输出消息。接下来，`try` 块使用 `throw` 语句创建一个异常对象（第 76 行）。执行 `throw` 语句表示代码中发生了问题。正如前面的章节中所示，你可以使用 `throw` 语句来抛出异常。与框架类库方法和 `CLR` 抛出的异常一样，这向客户端指明发生了错误。`throw` 语句指定了要抛出的对象。传递给构造函数的 `throw` 语句的数数可以是 `Exception` 或其派生出的任何类型。

传递给构造函数的字符串将成为异常对象的错误消息。当 `try` 块中的 `throw` 语句执行时，`try` 块会立即退出，程序控制继续执行位于 `try` 块之后的第一个匹配的 `catch` 块（第 78–81 行）。在本例中，类型（`Exception`）与 `catch` 中指定的类型匹配，因此第 80 行输出一条消息，表示发生了异常。然后，`finally` 块（第 82–86 行）执行并输出一条消息。此时，程序控制继续执行 `finally` 块之后的语句（第 88 行）。程序控制返回 `Main`。在第 80 行，我们使用异常的 `message` 属性来获取与异常相关的错误消息（即传递给 `Exception` 构造函数的消息）。第 13.7 讨论了 `Exception` 类的几个属性。

`Main` 的第 23–31 行在 `Main` 中定义了一个 `try` 语句，调用方法 `ThrowWithoutCatch`（第 92–108 行）。`try` 语句允许 `Main` 捕获 `ThrowWithoutCatch` 抛出的任何异常。`ThrowWithoutCatch` 中第 95–99 行的 `try` 块开始输出一条消息。接下来，`try` 块抛出一个 `Exception`（第 98 行）并立即退出。

通常情况下，程序控制将继续执行该 `try` 块之后的第一个 `catch`。然而，此块没有任何 `catch` 块。因此，异常在 `ThrowWithoutCatch` 中没有被捕获。程序控制进入 `finally` 块（第 100–104 行），该块输出一条消息。此时，程序控制返回 `Main`，因为适当 `catch` 块中的语句（例如第 107 行）没有执行。（事实上，编译器会就此发出警告）因为第 98 行抛出的异常没有被捕获。在 `Main` 中，第 27–31 行的 `catch` 块捕获了异常并显示一条消息，表示异常在 `Main` 中被捕获。

### 13.5.4 重新抛出异常

`Main` 的第 38–46 行在 `Main` 中定义了一个 `try` 语句，调用方法 `ExceptionCatchRethrow`（第 111–136 行）。`try` 语句允许 `Main` 捕获 `ExceptionCatchRethrow` 抛出的任何异常。`ExceptionCatchRethrow` 中第 114–132 行的 `try` 语句开始输出一条消息。接下来，`try` 块抛出一个 `Exception`（第 117 行）。`try` 块立即退出，程序控制继续执行 `try` 块之后的第一个 `catch`（第 119–127 行）。在本例中，抛出的类型（`Exception`）与 `catch` 中指定的类型匹配，因此第 121 行输出一条消息表示异常发生的位置。第 124 行使用 `throw` 语句重新抛出该异常。这表示 `catch` 块对异常进行了部分处理，现在再次抛出该异常（在这种情况下，是抛回方法 `Main`）以便进一步处理。

你也可以使用 `throw` 语句的版本，通过接收捕获到的异常的引用来抛出异常。然而，重要的是，这种形式的 `throw` 语句会重置抛出点，因此原始线程的堆栈跟踪信息将会丢失。第 13.7 演示了在 `catch` 块中使用操作数使用 `throw` 语句。在该节中，你会看到在捕获异常后，你可以从 `catch` 块创建一个不同类型的异常对象，并将原始异常作为新异常对象的一部分包含其中。类库设计人员经常这样做是为了自定义从类中方法抛出的异常类型，或提供额外的调试信息。

![](img/57baed2319be0bb1b5f98674846f2711_565_0.png)

> **软件工程观察 13.2**
> 通常来说，更好的实践做法是抛出一个新异常并将原始异常传递给新异常的构造函数，而不是重新抛出原始异常。这样可以保持原始异常的所有堆栈跟踪信息。我们在 13.7 中演示了如何将现有异常传递给新异常的构造函数。

方法 `ExceptionCatch` 中的异常处理没有完成，因为第 124 行的 `throw` 语句立即终止了 `catch` 块——如果在第 124 行和块结束之间有任何代码，它们将不会执行。当第 124 行执行时，方法 `ExceptionCatch` 终止返回 `Main` 寻找适当的 `catch`。`finally` 块（第 128–132 行）在控制返回 `Main` 之前执行并输出一条消息。返回 `Main` 时，第 42–46 行的 `catch` 块捕获异常并显示表示异常已被的消息。然后程序终止。

## 13.5.5 在 finally 块后返回

`finally` 块之后执行的下一个语句取决于异常处理状态。如果 `try` 块成功完成，或者 `catch` 块捕获并处理了异常，程序继续执行 `finally` 块之后的下一个语句。然而，如果异常未被捕获，或者 `catch` 块抛出了异常，程序将在下一个外层的 `try` 块中继续执行。外层 `try` 可能在主方法或其任何一个调用者中。也可以在 `try` 块中嵌套 `try` 语句；在这种情况下，外层 `try` 语句的 `catch` 块将处理内部 `try` 语句未捕获的任何异常。如果 `try` 块执行并有一个对应的 `finally` 块，即使 `try` 块通过 `return` 语句终止，`finally` 块也会执行。返回发生在 `finally` 块执行之后。

## 常见错误 13.3

当 `finally` 块执行时，有一个未捕获的异常正在等待处理，`finally` 块会抛出一个在 `finally` 块中未被捕获的新异常，第一个异常丢失，且新异常将传递给下一个外层的 `try` 块。

# 预防技巧 13.4

在 `finally` 块中放置可能抛出异常的代码时，请将代码封装在捕获相应异常类型的 `try` 语句中。这可以防止在执行 `finally` 块之前发生的任何未捕获和重新抛出的异常丢失。

# 软件工程观察 13.3

不要在每个可能抛出异常的语句周围放置 `try` 块——这会使程序难以阅读。相反，在一个重要的代码区域周围放置一个 `try` 块，并跟上处理每个可能异常的 `catch` 块。最后跟上一个 `finally` 块。使用不同的 `try` 块来区分可能抛出相同异常类型的多个语句。

# 13.6 using 语句

通常，资源释放代码应该放置在 `finally` 块中，以确保无论在相应的 `try` 中使用资源时是否发生异常，都能释放资源。另一种表示法——`using` 语句（不要与命名空间的 `using` 指令混淆）简化了获取资源、在 `try` 块中使用资源以及在相应的 `finally` 块中释放资源的代码编写。例如，一个文件处理应用程序（第17章）可能会产生所需的文件。该资源必须是一个实现了 `IDisposable` 接口的对象，因此在不再需要时会被正确关闭，并且有一个 `Dispose` 方法。`using` 语句的通用形式为

```cs
using (var exampleObject = new ExampleClass())
{
    exampleObject.SomeMethod(); // 对 exampleObject 执行操作
}
```

其中 `ExampleClass` 是实现 `IDisposable` 接口的类。此代码创建 `ExampleClass` 类型的对象并在语句中使用它，调用其 `Dispose` 方法释放对象使用的任何资源。`using` 语句隐式地将代码放在 `try` 块体内，并配有一个相应的 `finally` 块调用对象的 `Dispose` 方法。例如，上述代码段等同于

```cs
var exampleObject = new ExampleClass();
try
{
    exampleObject.SomeMethod();
}
finally
{
    if (exampleObject != null)
    {
        exampleObject.Dispose();
    }
}
```

# 13.7 异常属性

`finally` 块中的 `if` 语句确保 `exampleObject` 不为空——即它引用了一个对象——否则，在尝试调用 `Dispose` 时会发生 `NullReferenceException`。第13.9节引入了 C# 6 的新运算符 `?`，它用于更优雅地将上述 `if` 语句表示为行代码。

正如我们在13.4节中讨论的，异常继承自 `Exception` 类，该类具有多个属性。这些属性经常被用于构建指示捕获异常的错误消息。两个重要的属性是 `Message` 和 `StackTrace`。`Message` 存储与 `Exception` 对象关联的字符串错误。此消息可以是异常类型中定义的默认消息，也可以是在异常抛出时传递给 `Exception` 对象构造函数的自定义消息。`StackTrace` 包含表示方法调用堆栈的字符串。回想，运行时维护了一个已调用但尚未返回的开放方法调用列表。`StackTrace` 代表在异常发生时始终未完成处理的一系列方法。编译器生成的调试信息对于 IDE 来说易于访问（例如，你的项目代码部分，而不仅仅是第三方库），堆栈跟踪还包含行号；行号指示了堆栈跟踪中方法所在的位置

## 13.7.1 属性 InnerException

另一个被查询的属性是 `InnerException`。当类库中发生异常时，库通常会捕获该异常，然后抛出一个包含信息的新异常，以帮助客户端代码确定异常的。。类程序员通常会将原始异常对象“包装”在新的异常对象中——这为客户端代码提供了导致异常的完整详细信息。

例如，在会计系统中实现的库可能包含账户号码处理代码，其中账号以字符串形式输入，但在代码中用 `int` 表示。`Parse` 允许程序通过 `int.Parse` 将字符串转换为 `int` 值，如果遇到无效的数字格式，它可能会抛出 `FormatException`。当这种情况发生时，库程序员可能希望显示由 `FormatException` 提供的默认错误消息，或者希望指示一个新的异常类型，例如 `InvalidAccountNumberException`。

在这些情况下，库将提供一个 `InvalidAccountNumberException` 对象来捕获 `FormatException`，然后在 `catch` 块中创建，并将原始异常对象作为 `InvalidAccountNumberException` 对象的 `InnerException`。第13.8节展示了如何创建自定义异常类。

当使用会计系统库的代码中发生 `InvalidAccountNumberException` 时，`catch` 处理程序可以通过 `InnerException` 属性引用原始异常。因此，`InvalidAccountNumberException` 既表示用户指定了无效的账号，也表示格式无效。如果 `InnerException` 属性为 `null`，则表示异常不是由另一个异常引起的。

## 13.7.2 其他异常属性

`Exception` 类提供了其他属性，包括 `HelpLink`、`Source` 和 `TargetSite`：

- 属性 `HelpLink` 指定指向描述发生问题的帮助文件的链接。如果不存在此类文件，则属性为 `null`。
- 属性 `Source` 指定导致异常的程序集（即应用程序或库）的方法。
- 属性 `TargetSite` 指定异常起源产生的方法。

## 13.7.3 演示异常属性和堆栈回溯

我们的下一个示例（图13.5）演示了 `Exception` 类的 `Message`、`StackTrace` 和 `InnerException` 属性。此外，示例引入了堆栈回溯——当异常在特定作用范围内抛出但未被捕获时，方法调用会被“回溯”，并尝试在下一个 `try` 块中捕获异常。在我们讨论 `StackTrace` 和堆栈回溯机制时，我们会跟踪调用堆栈上的方法。要看到正确的堆栈跟踪，你应该按照与第13.2节所示类似的步骤执行此程序。

```cs
// 图 13.5: Properties.cs
// 堆栈回溯和 Exception 类属性。
// 演示使用属性 Message, StackTrace 和 InnerException。
using System;
class Properties
{
static void Main()
{
// 调用 Method1();生成的任何 Exception 将在
// 后的 catch 块中捕获
try
{
Method1();
}
catch (Exception exceptionParameter)
{
// 输出 Exception 的字符串表示，然后输出
//属性 Message，StackTrace 和 InnerException
Console.WriteLine("exceptionParameter.ToString():\n" +
exceptionParameter);
Console.WriteLine("\nexceptionParameter.Message: \n" +
exceptionParameter.Message);
Console.WriteLine("\nexceptionParameter.StackTrace: \n" +
exceptionParameter.StackTrace);
Console.WriteLine("\nexceptionParameter.InnerException: \n" +
exceptionParameter.InnerException);
}
}
```

图 13.5 | 堆栈回溯和 Exception 类属性。（3部分的第部分。）

```cs
// 调用 Method2
static void Method1() {
    Method2();
}

// 调用 Method3
static void Method2() {
    Method3();
}

// 抛出一个包含 InnerException 的 Exception
static void Method3() {
    // 尝试将字符串转换为 int
    try {
        int.Parse("Not an integer");
    } catch (FormatException formatException) {
        // 将 FormatException 包装在新的 Exception 中
        throw new Exception("Exception occurred in Method3", formatException);
    }
}
```
