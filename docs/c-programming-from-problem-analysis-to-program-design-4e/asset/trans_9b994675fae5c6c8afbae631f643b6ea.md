
```csharp
for (int i = 0; i < countOfScores; i++)
{
    Console.Write("Enter score {0}: ", i+1);
    inValue = Console.ReadLine();
    examScore[i] = int.Parse(inValue);
    totalScores += examScore[i];
}

averageTestScore = totalScores /
                   countOfScores;
Console.WriteLine("Average is {0}",
                  averageTestScore);
}
catch
{
    Console.WriteLine("Problem with scores - " +
                      "Cannot compute average");
}
Console.ReadKey();
}
}
}
```

如果运行该应用程序，并且用户输入非数字字符，例如值 9U（图 12-14 中显示为为第 3 个分数输入的内容），程序不会崩溃。相反，会执行 catch 块中的异常处理程序代码，并提醒用户发生了错误。

![](img/36e48639a06772bcb0fa1ea2525b33a3_835_0.png)

**图 12-14** 通用 catch 块处理异常

## 通用 catch 捕获

使用通用 `catch` 来避免异常终止的问题在于，由于 catch 代码会处理任何类型的异常，你永远无法十分确定是什么导致异常被抛出。以图 12-15 中所示的两个输出列表为例。

![](img/36e48639a06772bcb0fa1ea2525b33a3_836_0.png)

**图 12-15** 因除零和程序员错误而抛出的异常

是什么导致这些异常被抛出？图 12-15 中的第一个输出是因为尝试除以零而产生的。第二个抛出了“Index was outside the bounds of the array”异常。针对程序中的 bug，并没有显示“Index was outside the bounds of the array”的消息。当示例 12-2 中计算平均值的语句被改为示例 12-3 所示的语句时，该异常被抛出。

### 示例 12.3

```csharp
averageTestScore = totalScores / examScore[10]; // Invalid
```

不存在 examScore[10]。示例 12-2 中的算术语句是正确的；除数应该是 countOfScores。

```csharp
averageTestScore = totalScores / countOfScores; // Correct
```

> **注意** 修改该计算是为了说明程序员的错误（bug）可能导致异常被抛出。

尽管可以使用通用 catch 子句防止程序异常终止，但如果你知道是什么导致异常被抛出，调试会更容易。仅仅显示一条表示存在问题的消息帮助不大。

## 异常对象

当使用 .NET 语言引发异常时，会创建一个对象来表示该异常。所有异常对象都继承自异常基类，该基类名为 Exception。它是 System 命名空间的一部分。异常对象与其他对象一样，具有属性 and 行为（方法）。catch 子句可以列出一个异常类名，并在 catch 关键字后面的括号内列出一个对象标识符，如示例 12-4 所示。实际上，要使用所创建异常对象的任何属性，你必须有一个对象名。使用不带异常类型的 `catch { }` 不会让你访问对象。

Exception 基类的属性之一是 Message。Message 返回一个描述该异常的字符串。因为它是基类的属性，所以可用于任何异常对象。示例 12-4 在 catch 子句的参数列表中包含了 Exception 类。对象标识符 e 用于命名该类的对象。现在，对象 e 可用于 Exception 类的任何属性或方法。与对象 e 关联的 Message 属性在 catch 子句内用于显示描述该异常的消息。

> **注意** 没有对象，就不能使用 Message 属性或该类的任何其他成员。这也是需要包含参数列表 (System.Exception e) 的原因之一。

### 示例 12.4

```csharp
catch (System.Exception e)
{
    Console.Error.WriteLine("Problem with scores - " +
    "Cannot compute average");
    Console.Error.WriteLine(e.Message);
}
```

> **注意** 在参数列表中添加 (System.Exception e) 不会对异常进行任何筛选。此方法中抛出的任何异常都会被捕获，因为所有异常都派生自这个基类 System.Exception。在 catch 后面键入参数列表的优点是，你有一个对象标识符（例如 e），可用于属性。

在示例 12-4 中，除了显示程序员提供的、指示存在问题的消息外，还显示了一个附加字符串“Index was outside the bounds of the array”。那是对象 e 的 Message 属性的当前值。这两个字符串都显示在 Error 输出设备上。现在，如果再次运行该应用程序，并且它仍然包含之前输入的程序员错误，则输出窗口会列出导致异常被抛出的原因，如图 12-16 所示。

![](img/36e48639a06772bcb0fa1ea2525b33a3_838_0.png)

**图 12-16** 将 Message 属性与异常对象一起使用

> **注意** 调用 `Console.Error.WriteLine()` 方法是为了说明将错误消息显示到 Error 输出设备可能更合适。默认情况下，其输出会像 `Console` 类输出一样发送到控制台屏幕。不过，Error 输出设备可以改为显示到其他设备。

通常包含参数列表是为了筛选异常。通过指定多个异常筛选器，你可以在 `catch` 子句中编写特定于所抛出异常的代码。要做到这一点，你必须进一步了解构成 .NET Framework 类库的不同异常类，下一节将讨论其中一些。

## 异常类

当错误发生时，通过创建并抛出与所抛出异常的具体类型相对应的对象来报告该错误。该对象包含有关错误的信息。可以抛出许多不同类型的异常。

### 基异常类的派生类

表 12-1 显示了基 Exception 类的一些派生类。ApplicationException 和 SystemException 类构成运行时异常的基础，并在表 12-1 之后讨论。

**表 12-1** 基 Exception 类的派生类

| 继承自 Exception 的类 |
| --- |
| Microsoft.Build.BuildEngine.InvalidProjectFileException |
| Microsoft.WindowsMobile.DirectX.DirectXException |
| System.ApplicationException |
| System.ComponentModel.Design.ExceptionCollection |
| System.Configuration.SettingsPropertyIsReadOnlyException |
| System.IO.IsolatedStorage.IsolatedStorageException |
| System.Runtime.Remoting.MetadataServices.SUDSGeneratorException |
| System.Runtime.Remoting.MetadataServices.SUDSParserException |
| System.SystemException |
| System.Windows.Forms.AxHost.InvalidActiveXStateException |

> **注意**
>
> 从表 12-1 中可以看出，两个值得关注的异常类是 `ApplicationException` 和 `SystemException` 类。表中列出的其他类本章不讨论；不过，建议你查阅 MSDN 文档以进一步了解它们。

### ApplicationException 类

你可以编写自己的异常类，也可以使用 .NET 提供的众多异常类之一。.NET 的设计者加入了 ApplicationException 异常，以便区分用户定义的异常和系统定义的异常。如果你编写自己的异常，它们应当派生自 ApplicationException。ApplicationException 异常由用户程序抛出，而不是由 CLR 抛出。

### SystemException 类

系统提供的运行时异常类主要派生自 SystemException 类。SystemException 没有为类增加任何功能。除了构造函数之外，SystemException 类没有除继承自 Exception 和 Object 类的属性或方法之外的其他属性或方法。Exception 类有几个属性。你已经看到了其中两个属性的结果——Message 和 StackTrace。StackTrace 返回一个包含方法调用跟踪的字符串。Message 属性提供有关异常原因的详细信息。Exception 类的另一个属性 HelpLink 可以包含指向帮助文件的 URL，该帮助文件可以提供有关异常原因的附加信息。Source 属性获取或设置导致错误的应用程序或对象的名称，TargetSite 属性获取抛出异常的方法。

有 70 多个类派生自 SystemException 类。表 12-2 列出了其中一些较常见的、会被抛出的异常。你可能需要考虑添加处理程序来捕获其中的许多异常。

**表 12-2** SystemException 的派生类

| 从 SystemException 类派生的异常类 | 导致抛出异常的情况说明 |
| --- | --- |
| System.ArgumentException | 提供给方法的某个参数无效。 |
| System.ArithmeticException | 算术、强制转换或转换操作中存在错误。具有派生成员 System.DivideByZeroException 和 System.OverflowException。 |
| System.ArrayTypeMismatchException | 尝试在数组中存储类型错误的元素。 |
| System.FormatException | 参数的格式不符合参数规范。 |
| System.IndexOutOfRangeException | 尝试使用超出数组边界的索引访问数组元素。 |
| System.InvalidCastException | 存在无效的强制转换或显式转换。 |

