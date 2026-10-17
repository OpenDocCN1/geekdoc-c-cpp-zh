
C# 在其方法签名中不需要类似于 `Optional` 的修饰符。
相反，任何包含赋值的参数都将成为调用过程的可选参数。

```csharp
// The times 参数是可选的，默认值为 2。
public string CopyText(string original, int times = 2)
```

这两种语言中关于可选参数使用的规则相似：非可选参数可以出现在可选参数之后；参数数组和可选参数不能一起使用；以此类推。

另见
- 标点符号、参数和参数、方法

# Or 逻辑析取运算符

通常情况下，C# 的析取运算符与 Visual Basic 的运算符相同，无论对于整数（位运算）还是布尔（逻辑）操作都是如此。

## VISUAL BASIC

```vb
Dim complain As Boolean = (hot Or humid)
```

```csharp
bool complain = (hot | humid);
```

当对 Visual Basic 项目或源文件应用 `Option Strict Off` 时，使用带有一个整数和一个布尔值操作数的 `Or` 运算符将强制将布尔值转换为整数（0 或 1），然后执行位运算。C# 不允许这种操作数类型的混合。

# Order By 查询表达式运算符 (LINQ)

C# 的查询表达式运算符与 Visual Basic 的 `Order By` 运算符相同。两种语言都支持用逗号分隔的排序字段列表。每个字段默认按升序排序，或显式使用 `Ascending` (VB) 或 `ascending` (C#) 选项。若要按降序排序，请使用 `Descending` (VB) 或 `descending` (C#) 选项。

## VISUAL BASIC

```vb
Dim result = From Employee OrderBy FullName Descending Select Name
```

```csharp
var result = from Employee in Employees order by Name descending select Name;
```

*(注：由于原文中大量重复的区块已根据指令剔除，仅保留核心逻辑翻译)*

```cs
partial class ComplexContent
{
    // ----- Other members defined here.
}
```

## Visual Studio 2015 新功能

Visual Basic 最初并不允许在接口声明中使用 `Partial`（部分）修饰符。此功能已从 2015 年开始添加到 VB 中，尽管在 C# 中早已就支持了。同样，从 2015 年开始，VB 的 `Partial` 修饰符也可以用于 Module（模块）类型，这一变化在 C# 中并没有对应的对应。

部分方法（Partial methods）允许你在一个文件中定义方法，并在另一个文件中提供其实现，这两个部分都属于同一个部分类。

```vb
VISUAL BASIC
' ----- 来自第一个 *.vb 文件。
Partial class ComplexContent
    ' 声明不包含任何方法体。
    ' 始终以 "Partial Private Sub." 开始。
    Private Sub RecordTraceData(ByVal data As String)
    End Sub
End Class
```

```vb
' ----- 来自第二个 *.vb 文件。
Partial class ComplexContent
    ' 实现排除了 "Partial" 修饰符。
    ' 签名必须保持一致。
    Private Sub RecordTraceData(ByVal data As String)
        ------ 在此处实现。
    End Sub
End Class
```

```csharp
// ----- 来自第一个 *.cs 文件。
partial class ComplexContent
{
    // "private" 是隐含的。
    partial void RecordTraceData(string data)
}
```

```csharp
// ----- 来自第二个 *.cs 文件。
partial class ComplexContent
{
    // ----- 相同的 "partial void" 和签名。
    partial void RecordTraceData(string data)
    {
        // ----- 在此处实现。
    }
}
```

在 VB 中，只有类支持部分方法。而 C# 允许在类和结构体中使用部分方法。

# 分区方法 (Partition Method)

C# 没有类似于 Visual Basic 的 `Partition` 方法的功能。以下代码返回与 `Partition` 类似的结果。

```csharp
public static string Partition(long number, long start,
    long stop, long interval)
{
    // 处理无效数据。
    if ((start < 0) | (stop < start) | (interval < 1))
        throw new ArgumentException();
    // 处理边界条件。
    if (number < start)
        return string.Format("{0}", start - 1);
    else if (number > stop)
        return string.Format("{0}", stop + 1);
    else if (interval == 1)
        return string.Format("{0}:{0}", stop);
    // 在有效范围内。
    for (long counter = start; counter <= stop;
        counter += interval)
    {
        if ((number >= counter) & (number <
            Math.Min(stop, counter + interval - 1)))
            return string.Format("{0}:{1}", counter,
                Math.Min(stop, counter + interval - 1)));
    }
    // 不应该无法到达。
    throw new ArgumentException();
}
```

VB 的 `Partition` 方法会对生成的值进行空格填充，以确保两个由冒号分隔的部分长度相同。这里显示的示例代码没有执行填充操作。

# Pmt 方法

参阅

# 财务方法 (Financial Methods)

# Pmt 方法

# 参见财务方法

# 预处理指令 (Preprocessing Directives)

参阅

```vb
#Const 指令, #ExternalWindow, #ExternalSource, #If, #Region
```

# Print 方法

Visual Basic 的 `Print` 方法（以及相关的 `PrintLine` 方法）输出到使用 `FileOpen` 方法打开的文件。输出可以通过 `SPC` 和 `TAB` 方法包含对齐数据。

```vb
VISUAL BASIC
' 输出一个字符串和一个数字，如：
'    Seattle 84
PrintLine(lineNumber, Tab(15), totalMatches)
```

C# 不包含 VB 中的文件管理功能。相反，通常使用 `System.IO.Stream` 来输出文本。该类提供了输出不同类型的 `Write` 和 `WriteLine` 方法。表格化输出必须手动处理。

```csharp
// 输出一个字符串和一个数字，如：
//    Seattle 84
outFile.Print(cityName)
outFile.Print(new String(' ', 15 - cityName.Length));
outFile.WriteLine(totalMatches)
```

## 参见

## FileOpen 方法

# PrintLine 方法

# Print 方法

# Private 修饰符

C# 的访问修饰符是# Visual Basic

## 参见

## 访问修饰符

# 项目属性 (Project Properties)

VB 的 Build Events 出现于 C# 属性的不同的 Build Events 选项卡中。VB 的 Build Events 出现于 C# 属性的不同的 Build Events 选项卡中。VB 的 Build Events 出现于 C# 属性的不同的 Build Events 选项卡中。VB 的 Build Events 出现于 C# 属性的不同的 Build Events 选项卡中。VB 的 Build Events 出现于 C# 属性的不同的 Build Events 选项卡中。

# 编译选项卡 (Compile Tab)

编译选项卡上的大部分功能出现在 Visual Basic 的 Build 中，尽管许多名称有所变化。在大多数情况下，你应该能够很快确定等对应的字段。两个选项卡都包含一个高级按钮，在 VB 中被认为是高级编译选项的字段（包括DEBUG、TRACE 和自定义常量）出现在 C# 的主 Build 选项卡中。

C# 的编译选项卡中没有包含 VB Option 设置（如 Option Explicit）的直接对应项。请参见本章节中的 Option 条目，如何在 C 中管理这些功能。

VB 的高级编译选项包含一个移除整数溢出检查选项。因为整数操作在 VB 中默认检查溢出/下溢，而在 C# 中默认不检查，选择这些选项会导致语言之间的行为差异。如果你在 VB 中勾选了该选项，在 C# 中应取消勾选，反之亦然。

单个 C# 源文件。

## 我的扩展选项卡
C# 不支持 Visual Basic 的 `My` 命名空间，因此没有对应的“我的扩展”选项卡。

## 属性

### 属性语句

C# 对属性的实现与 Visual Basic 的 Property 语句非常相似，尽管 C# 没有包含特定的语言关键字来标识属性声明。相反，这些声明类似于字段声明，后面紧跟在一组大括号内的 getter 和 setter 实现。

![](img/baa5394648ec27e4a1aa37d09958ab46_376_0.png)

```vb
---- 许多属性使用后备字段。
Private _maxAmount As Integer = 0
---- 这里是属性本身。
Public Property Maximum As Integer
Get
    Return Me._maxAmount
End Get
Set(ByVal value As Integer)
    ' 虽然 "value" 是默认值，
    你也可以重命名此变量。
    If (value > 100) Then
        Me._maxAmount = 100
    ElseIf (value < 0) Then
        Me._maxAmount = 0
    Else
        Me._maxAmount = value
    End If
End Set
End Property
```

```csharp
// 许多属性使用后备字段。
private int _maxAmount = 0;
// 这里是属性本身。
public int Maximum
{
    get
{
        return this._maxAmount;
    }
    set {
      // ---- 隐含了一个名为 "value" 的输入变量。
      if (value > 100)
        this._maxAmount = 100;
      else if (value < 0)
        this._maxAmount = 0;
      else
        this._maxAmount = value;
    }
}
```

除了 `Return` 语句外，你可以在 Visual Basic 属性 getter 中通过将结果赋值给属性并使用 `Exit Property` 语句来指定返回值。

```vb
Visual Basic
' ----- 在 Get 块内部。
Maximum = Me._maxAmount
Exit Property
```

C# 只支持通过 `return` 语句返回属性值，这等于 VB 属性 getter 中的 `Return` 语句。

Visual Basic 中的只读和读写属性分别包含 `ReadOnly` 和 `WriteOnly` 修饰符，并省略不需要的 getter 或 setter。在 C# 中，省略不需要的 setter 或 getter足以指示属性的只读或只写状态。不需要特殊的修饰符。

```vb
Visual Basic
Public ReadOnly Property Status As Integer
Get
  ' ----- Return 语句出现在这里。
  End Get
  ' ----- 但没有出现 setter。
End Property
```

```csharp
public int Status {
  get {
    // ----- return 语句出现在这里。
  }
  // ----- 但没有出现 setter。
}
```

在构建读写属性时，两种语言都允许你对 getter 或 setter（但不同时是两者）应用与属性本身应用的修饰符不同的访问修饰符。在 Visual Basic 类和结构体中，属性默认是 `Public`，但在 C# 类型中默认是 `private`。

```vb
Public Property Status As Integer
Get
  ' ----- 公可访问的 getter 代码。
  End Get
Private Set
  ' ----- 私有可访问的 setter 代码。
```

```csharp
public int Status
{
  get
  {
    // ----- 公可访问的 getter 代码。
  }
  private set
  {
    // ----- 私有可访问的 setter 代码。
  }
}
```

在 Visual Basic 中，当属性显式实现接口成员时，`As` 子句之后会出现一个 `implements` 子句。在 C# 中，名称被修改为包含接口名称。

```vb
Public Property Status As Integer
implements IMonitor.Status
```

```csharp
public int IMonitor.Status
```

属性在每种语言中支持以下修饰符。

| Visual Basic 修饰符 | C# 修饰符 |
|---|---|
| Default | Not supported |
| Friend | internal |
| Iterator | Not supported |
| MustOverride | abstract |
| NotOverridable | sealed |
| Overloads | Not supported |
| Overridable | virtual |
| Overrides | override |
| Private | protected |
| Protected Friend | protected |
| Public | public |
| ReadOnly | Not supported |
| Shadows | new |
| Shared | static |
| WriteOnly | Not supported |
| Not supported | extern |

Visual Basic 中的属性可以包含参数，类似于方法。参数列表出现在属性之后。

```vb
Visual Basic
Public Property Status (ByVal day As DayOfWeek) As Integer
Get
    ' ----- 特定的 status。
Set(ByVal value As Integer)
    ' ----- 将特定的 status 赋值给 value。
End
```
