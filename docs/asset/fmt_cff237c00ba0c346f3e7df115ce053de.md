
```csharp
string result = Environment.GetEnvironmentVariable("PATH");
```

`Environ` 还可以添加一个从 1 开始的数值值，返回该位置的变量。在 C# 中，你必须检索所有元素并定位正确的项。

# VISUAL BASIC

```vb
result = Environ(oneBasedPosition)
```

# C#

```csharp
System.Collections.SortedList allVars =
new System.Collections.SortedList(
Environment.GetEnvironmentVariables());
if (oneBasedPosition <= allVars.Count)
    result = allVars[oneBasedPosition - 1].ToString();
```

# EOF 方法

Visual Basic 的 `EOF` 方法表示打开打开文件的当前读取或写入位置是否为该文件的末尾。

# VISUAL BASIC

```vb
Dim atEndFile As Boolean = EOF(fileNumber)
```

C# 并不包含与 VB 相同的文件管理功能。相反，通常是使用 `System.IO.FileStream` 类来读写文件。该类不包含 `EOF` 方法的直接等价物。相反，你可以比较文件长度与其当前位置（o-position），或者尝试从文件中读取数据。

# C#

```csharp
// --- 比较位置与长度。
bool atEndFile = (openedStream.Position >=
openedStream.Length);
```

```csharp
// --- 尝试读取更多数据。
int nextByte = openedStream.ReadByte();
atEndFile = (nextByte == -1);
```

如果你使用 `System.IO.StreamReader` 打开文件，`TextReader` 实例包含一个 `Peek` 方法，可以用它来检查文件末尾。

# C#

```csharp
atEndFile = (openedReader.Peek() == -1);
```

另请参

## FileOpen 方法

# Erase 语句

C# 没有类似于 Visual Basic `Erase` 语句的专用语句，你可以通过给数组赋值为 `null` 值来释放数组。

# VISUAL BASIC

```vb
Erase arrayOfData
```

# C#

```csharp
arrayOfData = null;
```

# Erl 属性

C# 方法不允许数字行标签，因此该语言没有 Visual Basic `Erl` 属性的对应项。

## Err 对象

Visual Basic 的 `Err` 对象用于识别错误详细信息，作为该语言非结构化错误处理系统的一部分。由于 C# 只包含结构化错误处理，因此它不包含 `Err` 的等价物。然而，由于 `Err` 内部使用对活动结构化 `Exception` 的引用，将你的非结构化错误处理代码转换为结构化等价物将为你提供类似的错误访问能力。

```vb
On Error GoToErrorHandler
  '----- 稍后...
ErrorHandler:
  LogError(Err.Description)
  Resume Next
```

```csharp
try {
  // ----- 这里是出错的代码。
}
catch (System.Exception ex)
{
  LogError(ex.Message);
}
```

另请参

- *On Error 语句*

## Err 属性

Visual Basic 的 `Err` 属性作为语言非结构化错误处理系统的一部分呈现最近的错误。C# 只包含对结构化错误处理的支持。`Err` 属性最接近等价物是 `try` 语句 `catch` 子句包含的异常。

```vb
On Error GoToErrorHandler
  '----- 在同一方法的稍后。
ErrorHandler:
  LogError(Err)
  Resume Next
```

```csharp
try {
  // ----- 这里是出错的语句。
}
catch (System.Exception ex)
{
  LogError (ex);
}
```

## 错误处理

查看

`Err` 对象，`Error` 语句，`On Error` 语句，`Resume` 语句，

`Throw` 语句，`Try` 语句

## Error 语句

Visual Basic 的 `Error` 语句仅为了向后兼容而存在。Visual Studio 文档建议用 `Err.Raise` 方法代替它。C# 中既没有 `Error` 也没有 `Err.Raise`。相反，请使用 C# 的 `throw` 语句在代码中抛出错误条件。

```vb
-- 已弃。
-- Error vbErrors.FileNotFound ' 或 53

-- 较新的等价物。
-- Err.Raise (vbErrors.FileNotFound)
```

```csharp
throw new System.IO.FileNotFoundException();
```

## ErrorToString 方法

Visual Basic 的 `ErrorToString` 方法根据数字代码返回错误消息。C# 不支持这种数字代码列表，因此不包含 `ErrorToString` 方法的等价物。最接近的等价物是 `System.Exception` 类或派生类的 `Message` 属性。

## Event 语句

与 Visual Basic 一样，C# 支持基于委托的事件声明。它的语句在此种用法下，与 VB 的 `event` 语句的功能非常相似。

```vb
Public Delegate Sub SampleEventHandler(
ByVal sender As Object, ByVal e As SampleEventArgs)
Public Event SampleEvent As SampleEventHandler
```

```csharp
public delegate void SampleEventHandler(
object sender, EventArgs e);
public event SampleEventHandler SampleEvent;
```

Visual Basic 还支持一种组合语法，委托的签名包含在事件声明中。

# VISUAL BASIC

```vb
Public Event SampleEvent(ByVal sender As Object,
ByVal e As SampleEventArgs)
```

这种独立语法在 C# 中可用。相反，你必须在事件语句中使用它之前声明委托。

事件在每种语言中都支持以下修饰符。

| Visual Basic 修饰符 | C# 修饰符 |
|---|---|
| Friend | internal |
| Private | private |
| Protected | protected |
| Protected Friend | protected internal |
| Public | public |
| Shadows | new |
| Shared | static |
| Not supported | abstract |
| Not supported | extern |
| Not supported | override |
| Not supported | sealed |
| Not supported | virtual |

异常

查看

`Err` 对象，`Error` 语句，`On Error` 语句，`Resume` 语句，

`Throw` 语句，`Try` 语句

Exit 语句

Visual Basic 的各种 `Exit` 语句允许你的代码退出块，例如循环或方法。下表显示了相应的 C# 语句。

| Visual Basic 语句 | C# 语句 |
|---|---|
| Exit Do | break |
| Exit For | break |
| Exit Function | return |
| Exit Property | return |
| Exit Select | break |
| Exit Sub | return |
| Exit Try | Not supported |
| Exit While | break |

通常，C# 的 `return` 语句退出方法和属性，而 `break` 语句退出其他块。要在 C# 中退出 `try` 块，你需要 `goto` 语句跳转到外部标签；C# 没有 `Exit Try` 的直接等价物。

在 Visual Basic `Case` 语句中，使用 `Exit Select` 跳出 `Case` 块是可选的。仅当你需要提前退出块时才使用该语句。在 C# 中，你必须始终使用 `break` 语句（或其他退出语句，如 `return` 语句）来离开每个 `Case` 块。

- 在这些块中都不需要 `Exit Select`。

Select Case customerType

  Case Custype.New

    message = "Welcome!"

  Case Custype.Existing

    message = "Welcome back!"

End Select

# C#

// 两个块都需要 break。

switch (customerType)

{

  case Custype.New:

    message = "Welcome!"

    break;

  case Custype.Existing:

    message = "Welcome back!"

    break;

}

```

由于 Visual Basic 允许识别特定的退出类型，因此可以同时退出某些类型的嵌套结构。

# VISUAL BASIC

```vb

For counter As Integer = 0 To 9

  Do While (content.Length > 0)

    --- 这将同时退出两个循环

  Exit For

Loop

```

C# 的组合 `break` 语句不支持这种级别的跳转。相反，对于使用 `break` 退出代码块的结构，你必须使用其他方法（例如 `goto` 语句）来立即退出多个结构。

```csharp

C# for (int counter = 0; counter < 10; counter++)

{

  while (content.Length > 0)

  {

    // --- "break" 语句只会退出
    // while 循环。请使用 "goto" 代替。
    goto AfterAllLoops;

  }

}

```

## AfterAllLoops 方法

在 Visual Basic 中，扩展方法始终出现在 `Module` 语句中。该方法必须标记有 `Extension` 特性（来自 `System.Runtime.CompilerServices`）。虽然没有标记任何特殊的修饰符，但方法的第一个参数是扩展的目标。

# VISUAL BASIC

```vb

--- 假设：导入 System.Runtime.CompilerServices

Friend Module LocalExtensions

<Extension> Public Function DigitsOnly(

ByVal originalText As String) As String

  --- 返回一个字符串结果。

End Function

End Module

```

在 C# 中，扩展方法出现在静态类（类似于 VB 模块），并使用此修饰符来指示被扩展的目标类型。

```csharp

C# internal static class LocalExtensions

{

  public static string DigitsOnly(

    this string originalText)

  {

    // ----- 返回一个字符串结果。

  }

}

```

## False 布尔字面量

C# 的 `false` 字面量与 Visual Basic 的 `False` 字面量相同。

字段是在类或结构体（以及 Visual Basic 中的模块）内部、任何方法外部声明的变量。其语法与局部变量声明非常相似。（更多声明细节请参见本章的“变量”条目。）

> VISUAL BASIC
> ' ---- 使用初始化器声明的字段。
> Private MonitoredValue As Integer = 0

> ' "Dim" 关键字是可选的，但在没有使用访问修饰符时是必须的。
> Dim AnotherValue As Integer

```csharp

// --- 使用初始化器声明的字段。

private int MonitoredValue = 0;

```

字段声明中的访问修饰符是可选的。如果缺失，Visual Basic 类和模块中的访问级别默认为 `Private`，而结构体中默认为 `Public`。在 C# 类和结构体中，字段默认是 `private`。

字段在每种语言中支持以下修饰符：

| Visual Basic 修饰符 | C# 修饰符 |
|---|---|
| Friend | internal |
| Private | private |
| Protected | protected |
| Protected Friend | protected internal |
| Public | public |
| ReadOnly | readonly |
| Shadows | new |
| Shared | static |
| WithEvents | 不支持 |
| 不支持 | volatile |

另

- 数组声明、访问修饰符、标识符、初始化器、New 运算符、Shared 修饰符、变量

## FileAttr 方法

Visual Basic 的 `FileAttr` 方法指示了最初用于通过 `FileOpen` 方法打开文件的 `OpenMode` 枚举。可能的值有 `Append`、`Binary`、`Input`、`Output` 或 `Random`。

```vb

VISUAL BASIC

Dim whichMode As OpenMode = FileAttr(fileNumber)

```

C# 不包含与 VB 相同的文件管理功能。相反，通常使用 `System.IO.Stream` 类来读写文件。该类不包含 `FileAttr` 方法的直接等价物。它确实包含了 `CanRead`、`CanSeek` 和 `CanWrite` 属性，这些属性可能提供与 `FileAttr` 方法相似的有限信息。

另

- FileOpen 方法

## FileClose 方法

Visual Basic 的 `FileClose` 方法关闭之前通过 `FileOpen` 方法打开的一个、一些或所有文件。关闭方法接受零或多个文件编号，指示要关闭的文件。

```vb

VISUAL BASIC

FileClose()        ' 所有文件

FileClose(1)      ' 仅限 #1 号文件

FileClose(2, 3)   ' #2 和 #3 号文件

```

C# 不包含与 VB 相同的文件管理功能。相反，通常使用 `System.IO.Stream` 类来读写文件。要关闭已打开的文件流，请调用其 `Close` 方法。

```csharp

openedStream.Close();

```

另

- FileOpen 方法

## FileCopy 方法

`System.IO.File.Copy` 方法提供了与 Visual Basic 的 `FileCopy` 方法提供的文件复制服务。

```vb

VISUAL BASIC

FileCopy (sourcePath, destinationPath)

```

```csharp

// C# 第三个参数是“overwrite”（覆盖）参数。
// Visual Basic 的 FileCopy 方法总是覆盖。

System.IO.File.Copy(sourcePath, destinationPath, true);

```

当使用 `FileCopy` 时，原始文件的属性将保留在新文件中。Visual Basic 的 `FileCopy` 方法会清除目标文件的属性，仅设置归档标记（archive）。以下 C# 语句在复制后使用时，可以模拟 VB 的行为。

```csharp

// C# System.IO.File.SetAttributes(destinationPath, FileAttributes.Archive);

```

## DateTime 方法

在 C# 中，使用 `System.IO.FileInfo` 类的 `LastWriteTime` 属性返回与 Visual Basic 的 `DateTime` 方法相同的信息。

# VISUAL BASIC

```vb

Dim updateDate As Date = DateTime(pathToFile)

```

```csharp

C# new FileInfo(pathToFile).LastWriteTime;
```
