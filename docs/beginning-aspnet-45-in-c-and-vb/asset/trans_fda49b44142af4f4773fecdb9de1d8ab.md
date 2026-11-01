

尽管这两种语言使用的语法差异很大，但两个代码示例执行的操作是相同的：它们都在 Label 控件上写出从 1 到 10 的数字。也就是说，循环从将 1 赋值给变量 loopCount 开始。接着，该值被转换为 String 并赋值给 Label 控件。然后 loopCount 增加 1，循环继续。这一过程一直持续到 loopCount 为 10，随后循环结束。在这个示例中，使用的是硬编码的数字。不过，你可以将开始和结束条件替换为来自变量或其他对象的动态值。例如，如果你正在处理前面看到的 roles 数组，你可以像这样写出数组中的每个角色：

```
VB.NET
For loopCount As Integer = 0 To roles.Length - 1
    Label1.Text &= roles(loopCount) & "<br />"
Next
```

```
C#
for (int loopCount = 0; loopCount < roles.Length; loopCount++)
{
    Label1.Text += roles[loopCount] + "<br />";
}
```

由于数组是从零开始索引的，所以你需要用 VB.NET 中的 roles(0) 和 C# 中的 roles[0] 来访问第一个元素。这也意味着循环需要从 0 开始。数组的 Length 属性返回数组中包含的元素总数。因此，当数组中有三个角色时，Length 返回 3。所以，在 VB.NET 中，代码从 Length 中减去 1，并将该值用作循环的结束条件，使循环从 0 运行到 2，从而访问所有三个元素。

不过，C# 示例并没有从 Length 中减去 1。相反，它使用了表达式：

```
loopCount < roles.Length;
```

因此，只要 loopCount 小于数组的长度，循环就会继续。同样，这会使循环访问从 0 到 2 的所有三个元素。

前面的示例在每次迭代时都会将 loopCount 变量加 1。若要使用更大的步进增量，你可以在 VB.NET 中使用 Step 关键字，而 C# 则允许你直接在步进定义中指定步长：

```
VB.NET
For loopCount As Integer = 0 To 10 Step 2
    Label1.Text &= loopCount.ToString() & "<br />"
Next
```

```
C#
for (int loopCount = 0; loopCount <= 10; loopCount = loopCount + 2)
{
    Label1.Text += loopCount.ToString() + "<br />";
}
```

这个循环会将 0 到 10 之间的偶数赋值给 Label 控件。

如果你正在遍历一个数组或数据集合，还有一种更易于阅读和使用的循环可供选择：For Each 或 foreach 循环。

为了避免 While 循环造成无限循环，通常最好添加一个条件，在尝试一定次数后终止循环。例如，如果邮件服务器宕机，下面的代码有助于避免无限循环：

VB.NET

```
Dim success As Boolean = False
Dim loopCount As Integer = 0
While Not success AndAlso loopCount < 3
    success = SendEmailMessage()
    loopCount = loopCount + 1
End While
```

C#

```
bool success = false;
int loopCount = 0;
while (!success && loopCount < 3)
{
    success = SendEmailMessage();
    loopCount = loopCount + 1;
}
```

使用这段代码，变量 loopCount 负责在尝试调用 SendEmailMessage 三次后退出循环。除了使用 loopCount = loopCount + 1 之外，你还可以使用组合的拼接和赋值运算符，如下所示：

VB.NET

```
loopCount += 1
```

C#

```
loopCount += 1;

// 此外，C# 还允许你这样写：
loopCount++;
```

所有示例的结果都相同：loopCount 的值增加 1，然后将新的总和重新赋值给 loopCount。

除了 While 循环之外，你还有其他几种选择，例如 Do While 循环（C# 中的 do while），它确保要执行的代码至少执行一次；还有 Do Until 循环（C# 中没有），它会一直执行直到某个条件为真，而不是像 While 循环那样在某个条件为真时持续循环。

## 提前退出循环

通常需要在循环完全结束之前退出循环。你可以使用 VB.NET 中的 Exit For 和 C# 中的 break 来实现，如下所示：

VB.NET

```
For loopCount As Integer = 1 To 10
    If loopCount = 5 Then
Exit For
End If
Label1.Text &= loopCount.ToString() & "<br />"
Next
```

C#

```
for (int loopCount = 1; loopCount <= 10; loopCount++)
{
    if (loopCount == 5)
    {
        break;
    }
    Label1.Text += loopCount.ToString() + "<br />";
}
```

使用这段代码，标签将只显示数字 1 到 4，因为一旦 loopCount 达到 5，循环就会退出。请注意：这个示例在实际应用中并不常见，因为你可以将代码重写为只循环四次，但它很好地展示了这个概念。

你可以使用 VB 中的 Continue For 和 C# 中的 continue 来停止处理当前迭代，并在有下一个迭代时继续执行。

到目前为止，你所看到的代码都是由简短而简单的示例组成的，可以直接放置在网页的 Code Behind 中；例如，放在你之前见过的 Page_Load 或 Button 的 Click 事件处理程序中。然而，在真实的网站中，你可能希望对代码进行更多的结构和组织。在下一节中，你将看到实现这一目标的不同方法。

## 组织代码

当你开始为网站添加多个页面时，几乎肯定会出现一些可以在多个页面中复用的代码。例如，你可能有一些从 Web.config 文件中读取设置的代码，而多个文件都需要用到它。或者你想从不同的页面发送包含用户详细信息的电子邮件。因此，你需要找到一种方法来集中管理你的代码。要在 ASP.NET 网站中实现这一点，你可以使用函数和子程序，接下来将讨论这些内容。为了让这些函数和子程序对网站中的所有页面都可用，你需要在某个特殊位置创建它们，这一点稍后会进行讨论。

### 方法：函数和子程序

函数和子程序（subs）非常相似；两者都能让你创建可复用的代码块，并从应用程序中的其他位置调用它们。函数和子程序之间的区别在于，函数可以返回数据，而子程序不能。函数和子程序统称为方法。你会在本章最后讨论面向对象的部分再次看到这个术语。

为了让函数和子程序更有用，可以为它们添加参数。也就是说，你可以传入可在函数或子程序内部使用的附加信息。函数和子程序通常采用以下格式：

VB.NET

```
' 定义一个函数
Public Function FunctionName ([parameterList]) As DataType

End Function

' 定义一个子程序
Public Sub SubName ([parameterList])

End Sub
```

C#

```
// 定义一个函数
public DataType FunctionName([parameterList])
{
}

// 定义一个子程序
public void SubName([parameterList])
{
}
```

以 Public 开头的完整第一行被称为方法签名，因为它定义了函数的外观，包括其名称和参数。Public 关键字（C# 中的 public）被称为访问修饰符，它定义了其他网页或代码文件可以在多大程度上看到此方法。本章稍后会详细讨论这一点。现在，你应该认识到 Public 具有最大的可见性，因此该方法对任何调用代码都是可见的。

函数名称后面跟着括号，括号内可以包含一个可选的参数列表。这些代码示例中的斜体部分将在你的代码中被替换为实际值。方括号（[ ]）之间的部分是可选的。为了让内容更具体一些，下面是一些函数和子程序的示例：

VB.NET

```
Public Function Add(a As Integer, b As Integer) As Integer
    Return a + b
End Function

Public Sub SendEmailMessage(emailAddress As String)
    ' 此处放置发送电子邮件的代码
End Sub
```

C#

```
public int Add(int a, int b)
{
    return a + b;
}

public void SendEmailMessage(string emailAddress)
{
```

