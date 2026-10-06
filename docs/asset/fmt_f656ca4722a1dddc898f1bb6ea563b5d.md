
在 C# 中，晚绑定（在该语言中通常称为“动态绑定”）通过 `dynamic` 类型声明表达式实现。

# C#

```csharp
dynamic basicValue = 20;

dynamic complexValue = new ExampleType();
```

```csharp
// ----- 此方法调用在编译时不进行检查。
complexValue.ProcessData();
```

在两种语言中，当给动态变量赋值时，由于该值在整个代码中使用，会发生装箱（boxing）和拆箱（unboxing）。

## LBound 方法

`System.Array` 类的 `GetLowerBound` 方法返回与 Visual Basic 的 `LBound` 方法相同的信息。对于多维数组，除非指定了另一个从 1 开始的维度，否则 `LBound` 假设为第一维。`GetLowerBound` 方法要求从 0 开始的维度。

```vb
VISUAL BASIC
' ----- 默认假设第一维
result = LBound(someArray)
```

```vb
' 指定了从 1 开始的维度（第三维）
result = LBound(someArray, 3)
```

```csharp
// ----- 指定了从 0 开始的维度（第三维）
result = someArray.GetLowerBound(2);
```

对于标准的 .NET 数组，任何维度的下界始终为零。

## LCase 方法

C# 中的 `char` 和 `string` 类型各包含一个 `ToLower` 方法，它是 Visual Basic 内置 `LCase` 方法的精确替代品。

```vb
result = LCase(someStringChar)
```

```csharp
result = someStringChar.ToLower();
```

## Left 方法

Visual Basic 的 `Left` 方法返回源字符串左侧的字符。使用 C# `string` 类的 `Substring` 方法返回类似的内容。

```vb
' ----- 返回前三个字符。
Dim areaCode As String = Left(phoneNumber, 3)
```

```csharp
// ----- 返回前三个字符。
string areaCode = phoneNumber.Substring(0, 3);
```

如果请求的长度超过字符串的全长度，`Left` 方法将静默返回整个字符串。在 C# 中，如果请求的长度过长，`Substring` 方法将抛出异常。在使用 `Substring` 方法之前，务必验证字符串的长度。

## Len 方法

Visual Basic 的 `Len` 方法返回字符串的长度，或值类型占用的字节数。下表显示特定 Visual Basic 数据类型表达式的返回值。

| 表达式类型 | C# 数据类型 | 返回值 |
| :--- | :--- | :--- |
| Boolean | bool | 2 |
| Byte | byte | 1 |
| Char | char | 2 |
| Char array | char array | 长度 |
| Date | DateTime | 8 |
| Double | double | 8 |
| Integer | int | 4 |
| Long | long | 8 |
| SByte | sbyte | 1 |
| Short | short | 2 |
| Single | float | 4 |
| String | string | 长度 |
| UInteger | uint | 4 |
| ULong | ulong | 8 |
| UShort | ushort | 2 |

```csharp
string notice = @"verbatim text";
```

## Visual Studio 2015 新特性

C# 的逐字字符串（verbatim strings）可以跨行边界，从而在字面量字符串中嵌入换行符。这与 Visual Basic 从 2015 版本开始的行为一致。在该版本之前，VB 中的此类换行符通常使用内置字面量（如 `vbCrLf`）包含在字符串中。

```vb
' VISUAL BASIC
' ----2015及以后。
Dim multiLineAs As String = "First Line" & "Second Line"
```

```vb
' ---- 2015 版本之前。
Dim multiLineAs As String = "First Line" & vbCrLf & "Second Line"
```

```csharp
string multiLine = @"First Line
Second Line";
```

C# 支持第二种字符串格式，并将其作为定义字符串字面量的标准方法。虽然内容仍被双引号包围，但可以包含任意数量的转义序列，每个序列都以反斜杠（`\` 字符）开头。这些字符串不使用 `@` 符号开头。

```csharp
string notice = "This is \"regular\" text.";
```

下表列出了可以在这些字符串中使用的转义序列，以及每个序列对应的最兼容 VB 内置字面量（位于 `Microsoft.VisualBasic.Constants` 中）。

| 字符 | 十六进制 | C# | Visual Basic |
| :--- | :--- | :--- | :--- |
| 警报 | 0x07 | `\a` | Chr(7) |
| 反斜杠 | 0x05c | `\\` | 文本内 |
| 退格 | 0x08 | `\b` | vbBack |
| 回车符 | 0x0d | `\r` | vbCr |
| 双引号 | 0x22 | `\"` | 文本内 `""` |
| 换符 | 0x0c | `\f` | vbFormFeed |
| 水平表符 | 0x09 | `\t` | vbTab |
| 行符 | 0x0a | `\n` | vbLf |
| MS-DOS 行结束符 | 0x0d,0x0a | `\r\n` | vbCrLf |
| 空空字符 | 0x00 | `\0` | vbNullChar |
| 单引号 | 0x027 | `\'` | 文本内 |
| 垂直表符 | 0x0b | `\v` | vbVerticalTab |

在前节中描述的 Unicode (u) 和十六进制 (x) 序列也可以出现在字符串中。

Visual Basic 中的字符字面量出现在双引号中，后跟 `c` 字符。在 C# 中，它们出现在单引号中，且没有特殊后缀。

```vb
' VISUAL BASIC
Dim oneDigit As Char = "0"c
```

```csharp
char oneDigit = '0';
```

## Visual Studio 2015 新特性

2015 年，Visual Basic 和 C# 都添加了字符串插值（string interpolation），这是一种使用字符串字面量生成格式化字符串的方法。两种语言对于此类字符串共享相同的语法，即以 `$` 符号前缀，并使用大括号 `{}` 来包含插值部分。

## 整数字面量

在 Visual Basic 中，整数字面量默认是 `Integer`，如果超过该类型的范围，则为 `Long`。在 C# 中，如果普通整数字面量符合该类型，则会被类型化为 `int`。否则，它会被强制转换为 `uint`、`long` 或 `ulong` 中的最小类型。

每种语言支持一组后缀，强制整数字面量变为特定类型。以下示例包含了每种语言中的长整数值。

```vb
' VISUAL BASIC
PassLongValue(123&)
```

```csharp
PassLongValue(123L);
```

下表列出了每种整数类型的后缀。每个后缀可以是大写、小写，或者对于包含多个字符的后缀，可以是大小写混合。

| 数据类型 | Visual Basic 后缀 | C# 后缀 |
| :--- | :--- | :--- |
| Short | S | 无后缀 |
| Unsigned Short | US | 无后缀 |
| Integer | % 或 I | 无后缀 |
| Unsigned Integer | UI | U |
| Long | & 或 L | L |
| Unsigned Long | UL | UL 或 LU |

## 浮点字面量

在两种语言中，浮点字面量默认都是 `Double`/double`。你也可以通过在字面值后附加类型后缀来更改默认值。下表列出了每种浮点类型的后缀。每个后缀可以是大写或小写。

| 数据类型 | Visual Basic 后缀 | C# 后缀 |
| :--- | :--- | :--- |
| Single | ! 或 F | F |
| Double | # 或 R | D |
| Decimal | @ 或 D | M |

C# 和 Visual Basic 也接受指数格式（科学计数法）的数字。基数或指数都可以包含一个一元 +–，并且还可以出现可选的类型字符。

```vb
' Visual Basic
bigValue = 9.24E+22# ' Double
```

```csharp
// C#
double bigValue = 9.24E+22D; // double
```

### 布尔字面量
C# 的 `true` 和 `false` 字面量是 Visual Basic `True` 和 `False` 字面量的精确替换。请参考本章中的“布尔数据类型”条目，了解语言在将真值转换为整数时的差异。

### 十六进制和八进制字面量
Visual Basic 通过 `&H` 和 `&O` 前缀提供了十六进制和八进制字面量。C# 使用 `0x` 前缀支持十六进制字面量，但不支持八进制字面量。

# Visual Basic

```vb
' VISUAL BASIC
decimal25 = &H19
decimal25 = &O31
```

```csharp
// C#
int decimal25 = 0x19;
```

### 日期字面量
Visual Basic 使用字符串字面量表示日期和时间，然后转换为 `Date` 类型。C# 没有字面量日期类型；它使用 `DateTime.Parse` 或 `DateTime` 构造函数。

### 字符串字面量
Visual Basic 使用双引号字符串字面量（插值除外）。C# 使用双引号字符串字面量，并使用 `$` 前缀进行插值。

## Main 方法

在 Visual Basic 和 C# 中，应用程序都使用 `Main` 方法作为程序的入口点。这些程序始终是 `Shared`（VB 中如果方法出现在 Module 中，则假设使用了 `Shared` 修饰符）或 `static`（C#），返回无结果（Sub 或 void）或整数，并且可以定义一个参数，即命令行字符串数组。C# 允许这些方法为私有，尽管 Visual Basic 并不允许这样做。

```vb
VISUAL BASIC
' --- 无返回值或参数的基础版本。
Shared Friend Sub Main()
End Sub
' ---- 同时包含返回代码和参数的版本。
Shared Friend Function Main(
ByVal cmdArgs() As String) As Integer
End Function
```

```csharp
// ---- 无返回值或参数的基础版本。
static void Main()
{}
 // --- 同时包含返回代码和参数的版本。
static int Main(string[] args)
{
}
```

在 Visual Basic Windows Forms 应用程序中，可以将窗定义为启动对象，在缺少 Main 方法的情况下，编译器将提供一个。在 C# 中，你必须自己提供该方法，并通过项目属性标识它。在 C# Windows Forms 应用程序中，Main 方法必须装饰有 `[STAThread]` 特性，这是 Visual Basic 编译器在后台提供的。

```csharp
[STAThread] static void Main()
```

在 C# 的 Windows Forms 应用程序中，你必须通过 Main 方法中的代码手动显示主窗体。

```csharp
static void Main()
{
    Application.Run(new Form1());
}
```

应用程序通常在到达 Main 方法结束时退出。可以使用以下功能之一让程序提前退出，按从礼貌到最直接的方式排序。注意 C# 不包含 VB End 语句的直接等效物。

- 调用 `System.Windows.Forms.Application.Exit()`
- 调用 `System.Environment.Exit(exitCode)`
- 使用 Visual Basic 的 End 语句

Visual Basic 包含了通过项目属性中的启用应用程序框架复选框激活的模型。激活后，该模型启用提供更结构化启动过程的功能，以及支持应用程序范围的未处理错误监控。C# 不包含对这些功能的项目级支持，但你可以在标准代码中模拟它。有关关于这些功能以及如何在 C# 中使用等效方案的更多信息，请参阅本书第 3 章中的以下条目：

- MinimumSplashScreenDisplayTime 属性
- NetworkAvailabilityChanged 事件 (My.Application)
- SplashScreen 属性
- Startup 事件
- StartupNextInstance 事件
- UnhandledException 事件

## Me 实例表达式

C# 的 `this` 表达式提供了对本地类型成员的访问，就像 Visual Basic 的 `Me` 表达式一样。

```vb
Class SimpleAdder
    Public Value As Integer = 0
    Public Sub Increment()
    Me.Value += 1
    End Sub
End Class
```

```csharp
class SimpleAdder
{
    public int Value = 0;
    public void Increment()
    {
        this.Value++;
    }
}
```

## 另请参阅

## MyClass 实例表达式

## 方法

Visual Basic 区分了 `Function` 和 `Sub` 语句，即区分返回值的方法和不返回值的方法。在 C# 中，这两种方法共享共同语法，主要区别在于用于退出方法的返回语句格式。

C# 中函数的语法与 Visual Basic 中出现的没有太大区别。每个函数都包含一个标识符名称，后跟一个括号内的参数列表。两种语言都支持相似的声明修饰符。在 C# 中，返回数据类型的声明从 `As` 子句移动到方法标识符正之前。

# Visual Basic

```
Public Function ParseText(ByVal timeText As String,
ByRef hours As Integer, ByRef minutes As Integer) _
As Boolean
  ' 核心逻辑，然后...
  Return success
End Function
```

# C#

```csharp
public bool ParseText(string timeText,
  ref int hours, ref int minutes)
{
  // ---- 核心逻辑，然后...
  return success;
}
```

不返回值的方法——Visual Basic 中的 `Sub` 语句——与有返回值的方法几乎完全相同。关键变化是将返回数据类型替换为 `void` 关键字。

# Visual Basic

```
Public Sub LogError(ByVal errorText As String)
  ' 可选包含此语句：
  Return
End Sub
```

# C#

```csharp
public void LogError(string errorText)
{
  // 可选包含此语句：
  return;
}
```

如示例所示，C# 方法的体位于一组大括号中。

在 Visual Basic 中实现特定接口的成员时，`Implements` 子句显式标识了方法正在实现的接口成员。

```vb
VISUAL BASIC
Public Sub Speak (ByVal textToSpeak As String) -
    Implements IVocal.Speak
```

在 C# 中，方法名以接口名称名前缀。

```csharp
public void IVocal.Speak(string textToSpeak)
{
}
```
