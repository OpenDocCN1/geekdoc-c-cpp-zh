

除了 For 和 For Each 循环之外，还有一个循环需要你关注：While 循环。

## While 循环

顾名思义，While 循环能够在某个条件为真时循环。与另外两种循环不同，它们通常会自行结束，而 While 循环如果不小心处理可能会无限循环下去。它也可能在条件从未满足时一次也不执行。下面的示例展示了如何使用 While 循环：

```
VB.NET
Dim success As Boolean = False
While Not success
    success = SendEmailMessage()
End While
```

```
C#
bool success = false;
{
    success = SendEmailMessage();
}
```

这段代码尝试使用虚构的 SendMessage 方法发送电子邮件，并且会一直尝试直到成功为止——也就是说，只要 success 的值为 False（C# 中为 false）。请注意，Not 和 ! 用于反转 success 的值。SendEmail 方法 supposed to return True when it calls SendEmailMessage。如果它返回 False 则不然。如果一切按计划进行，代码进入循环并调用 SendEmailMessage。循环条件不再满足，循环结束。然而，当 SendEmailMessage 返回 False 时，例如因为邮件服务器宕机，循环会继续并再次调用 SendEmail。

为了避免 While 循环出现无限循环，最好使用一个计数器，在尝试一定次数后终止循环。例如，下面的代码有助于避免邮件服务器宕机时的无限循环：

```
VB.NET
Dim success As Boolean = False
Dim loopCount As Integer = 0
While Not success AndAlso loopCount < 3
    success = SendEmailMessage()
    loopCount = loopCount + 1
End While
```

```
C#
bool success = false;
int loopCount = 0;
while (!success && loopCount < 3)
{
    success = SendEmailMessage();
    loopCount = loopCount + 1;
}
```

使用此代码，变量 loopCount 负责在尝试调用 SendEmailMessage 三次后退出循环。除了使用 loopCount = loopCount + 1，你也可以使用组合的连接和赋值运算符，如下所示：

### VB.NET

```
loopCount += 1
```

### C#

```
loopCount += 1;
```

```
// Alternatively C# enables you to do this:
loopCount++;
```

所有示例的结果都相同：loopCount 值增加一，然后将新总数赋给 loopCount。

除了循环之外，你还有其他几种选择，例如 Do While 循环（C# 中为 do while），它确保代码至少执行一次，以及 Do Until 循环（C# 中没有），它会一直进行直到某个条件为真，就像 While 循环一样。

## 提前退出循环

在循环尚未完全结束之前就退出循环的需求很常见。你可以用 VB.NET 中的 Exit 和 C# 中的 break 来实现，如下所示：

### VB.NET

```
For loopCount As Integer = 1 To 10
    If loopCount = 5 Then
        Exit For
    End If
Labell.Text &= loopCount.ToString() & "<br />"
Next
```

### C#

```
for (int loopCount = 1; loopCount <= 10; loopCount++)
{
    if (loopCount == 5)
{
        break;
    }
    Labell.Text += loopCount.ToString() + "<br />";
}
```

使用这段代码，标签只会显示 1 到 4 的数字，因为 loopCount 已达到 5 的值。注意：此示例在现实世界中并没有太多实际用途，因为你会重写代码使其循环四次，但它很好地展示了概念。

你可以使用 VB 中的 Continue 和 C# 中的 continue 来停止处理当前迭代并继续下一个迭代（如果有）。

到目前为止，你看到的代码都由可以放在网页的 Code Behind 中的简短简单示例组成；例如，在 Page_Load 或在你之前见过的按钮的 Click 处理程序中。然而，在现实世界的网站中，你可能希望对代码进行更多结构化和组织。在下一节中，你将看到实现此目的的不同方法。

## 组织代码

当你开始为网站添加不止几个页面时，你几乎肯定会遇到在多个页面中重复使用的代码。例如，你可能有一些从 web.config 文件读取设置的代码，需要在多个文件中用到。或者你想从不同页面发送包含详细信息的电子邮件。因此你需要找到一种集中代码的方法。要在 ASP.NET 网站中实现这一点，你可以使用函数和子程序，接下来会讨论这些。要使这些函数和子程序对站点中的所有页面可用，你需要在特殊位置创建它们，之后会讨论。

## 方法：函数和子程序

函数和子程序（subs）非常相似；两者都使你能够创建可重用的代码块，可以从应用程序中的其他位置调用。函数和子程序之间的区别在于函数可以返回数据，而子程序不能。函数和子程序合在一起被称为方法。你将在本章最后一部分涉及面向对象时再次看到这一点。

为了使函数和子程序更有用，它们可以被参数化。也就是说，你可以传入可在函数或子程序内部使用的附加信息。函数和子程序通常采用以下格式：

```
VB.NET
' Define a function
Public Function FunctionName([parameterList]) As DataType

End Function

' Define a subroutine
Public Sub SubName([parameterList])

End Sub

C#
// Define a function
public DataType FunctionName([parameterList])
{
}

// Define a subroutine
public void SubName([parameterList])
{
}
```

从 Public 开始的完整行被称为方法签名，因为它定义了函数的用途，包括其名称和参数。Public 关键字（C# 中为 public）称为访问修饰符，定义了其他页面或代码文件可以看到的程度。这将在本章后面详细讨论。现在，你应该意识到 Public 具有最大的可见性，因此该方法对任何调用方都可见

函数名称后面跟着参数，而参数又可以包含可选的参数列表。这些代码示例中斜体化的部分将在你的代码中被实际值替换。方括号（[]）是可选的。为了更具体一些，这里有一些函数和子程序的示例：

### VB.NET

```
Public Function Add(a As Integer, b As Integer) As Integer
Return a + b
```

```
Sub SendEmail(emailAddress As String)
' Code to send an e-mail goes here
End Sub
```

### C#

```
public int Add(int a, int b)
{
    return a + b;
}
```

```
public void SendEmailMessage(string emailAddress)
{
    // Code to send an e-mail goes here
}
```

在这些代码示例中很明显函数会返回值，而子程序不会。Add 方法使用 Return 关键字（C# 中全部小写的 return）返回 a 和 b 的和。VB.NET 中的 Sub 和 C# 中的方法不需要 Return 关键字，尽管你可以使用它在不指定值的情况下提前退出方法。

最后，函数和子程序都有参数列表，使你能够定义变量的名称和类型。在方法内部，你可以像普通变量一样访问这些变量。以 Add 方法为例，你有两个参数：一个用于加法的左侧，一个用于右侧。SendEmailMessage 只有一个参数：String 持有用户的电子邮件地址。

在 VB.NET 的早期版本中，你会在参数列表的每个参数中使用 ByVal 关键字。这是所有参数的默认类型，因此 VS 不再为你添加它。ByVal 的相反是 ByRef。当你指定 ByVal 时，会复制变量。方法内部对它的任何更改在方法结束时就会丢失。相比之下，如果你指定 ByRef，则会将变量的引用发送到方法。对传入变量的任何更改也会反映在原始变量上。下面的简短示例演示了其工作原理：

