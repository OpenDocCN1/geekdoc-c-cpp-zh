
# C#-Visual Basic 双语词典：Visual Studio 2015 版

![](img/baa5394648ec27e4a1aa37d09958ab46_0_0.png)

![](img/baa5394648ec27e4a1aa37d09958ab46_1_0.png)

如需本书更新或了解 Tim Patrick 出版的其他书籍，请在线、电子邮件或社交媒体与他联系。

- **网站** wellreadman.com

- **邮箱** tim@timaki.com

- **Facebook** facebook.com/wellreadman

- **Twitter** twitter.com/thewellreadman

- **Goodreads** Goodreads.com/wellreadman

献给 Claudette Moore

一位老树和老旧技术书籍作者的朋友

# 引言

## 两种语言

用著名剧作家乔治·伯纳德·肖的话来说，C# 和 Visual Basic 是两种由共同的框架隔开的语言。从语法和目标受众来看，微软的这两个编程系统似乎彼此非常遥远。尽管如此，在编码能力、计算访问以及用户每天需要任务的自动化方面，它们是完全平等的。

VB 声称其语法谱源追溯到 BASIC 第一版，由 John Kemeny 和 Thomas Kurtz 在 1964 年开发，旨在为软件开发过程带来便利和清晰。五年年后，Dennis Ritchie 开始研究 C 编程语言——即 C# 的祖先——并创建了一个编译器，根据其作者的话，这个编译器对于许多任务比那些所谓的强大的语言更方便且高效。

在 .NET 中，微软将这两种计算方言结合在了一起：一种为凡人设计的软件语言的简单性，以及另一种为了解决从设备驱动程序到文字处理器等大量编码问题的语言的强大性。BASIC 和 C 的后代现在共同位于 .NET 框架的共同基础之上。通过这一共享资源，C# 和 Visual Basic 的开发者可以使用相同的工具、相同的平台和相同的用户社区。

然而，它们并不是相同的。Visual Basic 代码讨厌大括号，而你必须花费大量的时间和精力才能看到在 C# 中完全拼写的内容。这两种语言在促进快速应用开发和利用 ADO.NET 以及 XAML 等强大技术方面有很多共同之处，但它们通过源代码进行通信的方式非常不同。这正是本书的用武之地。

《C#-Visual Basic 双语对照字典》通过为两种语言之间所有的语法和特征差异提供清晰的等效项，帮助统一 Visual Basic 和 C#。这两种语法的连接从未像现在这样重要。

## 谁需要这本书？

几十年前，在 C 和 BASIC 上起家的开发者可以通过只精通一种通用语言来建立职业生涯。今天，软件公司要求程序员精通多种语言、脚本、数据格式和平台（包括移动和桌面）。如果你已经熟悉 VB，很有可能也需要熟悉 C#，反之亦然。

《C#-Visual Basic 双语对照字典》适用于所有需要学习 C# 的 Visual Basic 开发者，也适用于需要理解 Visual Basic 或将其集成到 C# 代码中的 C# 开发者。字典提供了 C# 特征的 Visual Basic 等效项，使得两种语言之间的翻译变得更容易。

对于那些在使用两种语言的项目并发现难以记忆每种语言语法的开发者来说，这本书特别有用。对于已经精通其中一种语言的人来说，这也是一个很好的资源。

## 书中包含内容

《C#-Visual Basic 双语对照字典》按 C# 特征或关键字字母顺序排列。每个条目都清晰地解释 C# 特征在 Visual Basic 中的等效项，并提供其如何工作的代码示例。

本书分为三个主要章节：

- 第1章：C# 到 Visual Basic。本章涵盖了 C# 特征和关键字在 Visual Basic 中的等效项。

- 第2章：Visual Basic 到 C#。本章涵盖了 Visual Basic 特征和关键字在 C# 中的等效项。

- 第3章：我的命名空间 (My Namespace) 到 C#。本章关注 Visual Basic 中的 "My" 命名空间及其 C# 中的 等效项。

"My" 命名空间是 Visual Basic (VB.NET) 的独特特征，在 C# 中没有直接等效项。然而，本书提供了如何使用 C# 实现相同结果的指导。

### Visual Studio 2015 新功能

本书包含了 Visual Studio 2015 和“Roslyn”编译器引入的语言特征。对于尚未升级最新版本的开发者，所有对新特征的讨论都明确了 Visual Studio 2015 之前存在的功能。

## 书不包含内容

尽管《C#-Visual Basic 双语对照字典》包含了 C# 和 Visual Basic 的语言关键字和语法元素，但它并不是 .NET 开发的详尽参考。除了在特定的代码解决方案中出现外，本书没有讨论 .NET 基类库。它还排除了其他语言无关的 .NET 技术，如 ADO.NET 和 Windows Communication Foundation (WCF)。

“Visual Basic”名称仅指该语言的 .NET 版本，而不是那些导致 Visual Basic 6.0 的版本。本书识别了 Visual Studio 2015（“Roslyn”）发布的新语言更新与 Visual Studio 2013 中生效版本之间的差异。然而，它没有记录 C# 和 Visual Basic 语言之前的版本引入的更改。例如，文本假设异步编程关键字（“async”和“await”运算符）已存在每种语言，尽管这些关键字直到 Visual Studio 2012 才被引入。

尽管第1章包含了动态 C# 语言关键字的涵盖，但本书没有讨论 System.Dynamic 命名空间或任何动态语言运行时（Dynamic Language Runtime）特征。

从头到尾读完参考书是一项艰巨的工作，但全球几位高深开发者同意接受挑战，结果书籍改进了很多。Eric Moreau 和 Jan Zárubara 对文本提供了大量的注释。额外的投入还来自 David Fulop、Marco Meijer、Fanie Reynders 和 Alex Sorokoletov。特别感谢 Lucian Wisch 以及所有让我能够旁听并参与他们技术交互的微软语言 MVP、作者和内部人士。

关于作者

Tim Patrick 是一位软件架构师和开发人员，拥有超过30年的设计和构建自定义软件解决方案的经验。他也是许多书籍和文章的作者，主要涵盖技术主题。此时此刻，你正在读他的他关于软件开发的第八本书。

2007年，微软将 Tim 选入其最有价值专业人员（MVP）计划，以感谢他对 Windows 编程社区的贡献。他还是一名微软认证解决方案专家。Tim 在西雅图太平洋大学获得了计算机科学学位。

你可以通过他的个人网站 [wellreadman.com](http://wellreadman.com) 与 Tim 联系。

本章中的 C# 条目根据关键字或功能按字母顺序排列。找到语言条目可以查看其对应的 Visual Basic 代码。符号标识的条目出现在字母开头的条目之前，并按以下顺序排列：

! # $ % & ( * + , - . / : < <= > ? @ [ \ ^ { | ~

## ! 否定运算符

C# 中以布尔值为中心的 `!` 运算符在 Visual Basic 中的等效运算符是 `Not` 运算符。

```
C#
bool opposite = !originalValue;
VISUAL BASIC
Dim opposite As Boolean = Not originalValue
```

当 `Not` 运算符与整数操作数一起使用时，它也是位取反运算符。在 C# 中，该变化的等效运算符是 `~`。

参见

- 位取反运算符

## != 比较运算符

在比较值时，Visual Basic 的不等运算符 `<>` 与 C# 的 `!=` 运算符相同，并且出现在相同的二元运算符位置。

```
C#
if (teamPlayers != 9)
VISUAL BASIC
If (teamPlayers <> 9) Then
```

对于字符串比较，`<>`运算符再次复制了 C# 的 `!=` 运算符。（注意：原始 OCR 文本中为 ===，但根据不等比较的上下文，这很可能是 != 的误笔或指代比较逻辑）。然而，VB 的 `Option Compare` 语句会影响字符串之间的比较方式。默认情况下，C# 和 Visual Basic 都对字符串进行二进制层面的比较。但是，如果 VB 项目或源文件使用了 `Option Compare Text`，则比较将使用特定于文化的排序规则。

对于字符串以外的引用类型，C# 的 `!=` 运算符测试所比较的两个引用是否指向同一个底层实例。这种语法在 Visual Basic 中是无效的（至少当在使用 `Option Strict On` 时）。相反，VB 程序应该使用 `IsNot` 运算符配合第二个实例，或者配合 `Nothing`。

```
// 标准实例比较。
if (firstInstance != secondInstance)

// 与 null 的比较。
if (anotherInstance != null)
VISUAL BASIC
' ----- 标准实例比较。
If (firstInstance IsNot secondInstance) Then

' ----- 与 null 的比较 (VB 中为 Nothing)。
If (anotherInstanceIsNot Nothing) Then
```

## #define 指令

在 C# 中，`#define` 指令声明预处理常量。这些常量本质上是布尔的，因为它们要么存在（类真要么不存在（类假）。相应的 `#undef` 指令用于移除之前通过 `#define` 声明的常量。

```C#
#define TestVersion
```

在 Visual Basic 中，使用 `#Const` 指令来开始使用预处理常量。与 C# 预处理常量的布尔性质不同，VB 中的并行常量可以是布尔、整数、浮点数、字符串或日期值。

```VISUAL BASIC
#Const TestVersion = "Beta 0.7"
```

要清除之前声明的 VB 常量，请将其赋值为 `Nothing`。

```VISUAL BASIC
#Const TestVersion = Nothing
```

## #error 指令

Visual Basic 中没有 `#error` 指令的等效物。

## #if 指令

Visual Basic 中预处理条件语句的通用语法与 C# 中的用法非常相似，仅有微小的拼写和大小写差异。

| C# 术语 | Visual Basic 术语 |
| --- | --- |
| `#if` | `#If...Then` |
| `#elif` | `#ElseIf..Then` |
| `#else` | `#Else` |
| `#endif` | `#End If` |

关键区别出现在条件本身。C# 中的预处理值像布尔值；它们要么存在要么不存在。在 Visual Basic 中，预处理值以布尔、整数、浮点数、字符串或日期的形式存在，你可以对这些值应用典型的 VB 运算符。

```C#
#if TestVersion
  // --- 此处为特定测试代码。
#elif (OldVersion == false)
  // --- 此处为向兼容代码。
#else
  // --- 此处为标准代码。
#endif

VISUAL BASIC
#If TestVersion Then
  ' --- 此处为特定测试代码。
#ElseIf (OldVersion = False) Or
  (TargetVersion < 2.5) Then
  ' --- 此处为向兼容代码。
#Else
  ' --- 此处为标准代码。
#End If
```

C# 允许在条件表达式中使用 `=`, `!=`, `!`, `&&`, `||` 以及运算符，`true` 和 `false` 常量以及括号。Visual Basic 表达式包括任何标准的 VB 比较运算符（`=`, `<`, `>`, `<=`, `>=`）；数学、字符串和逻辑运算符（`+`, `*`, `/`, `^`, `Mod`, `<<`, `>>`, `&`, `Not`, `And`, `Or`, `Xor`, `AndAlso`, `OrElse`）；转换和转换函数（`DirectCast`, `TryCast`, `CType`, `Bool`, `CByte`, `CChar`, `CDate`, `CDec`, `Double`, `ClInt`, `CLng`, `CObj`, `CSByte`, `CShort`, `CSng`, `CStr`, `CUInt`, `CULng`, 和 `UShort`）；如果带有括号，最终结果为布尔值。这些表达式中的字符串值使用二进制层面的比较，而不是特定于文化的文本比较。

## #line 指令

Visual Basic 中没有 `#line` 指令的等效物。

## #pragma 指令

在 C# 中，`#pragma` 指令用于编译器指令。在 Visual Basic 中，`#pragma` 指令用于各种与编译相关的任务，与其在 C# 中的用法类似。（注意：该部分的 OCR 文本是碎片化/重复的；此重构遵循这些主题的标准文档结构）。

## 赋值运算符

## & 地址运算符

Visual Basic 不对指针操作提供直接支持，因此不包含为对象建立固定地址的运算符。

另请参

- 指针

- `&` 与运算符

通常情况下，Visual Basic 的 `And` 运算符与 C# 的 `&` 运算符相同，均适用于整数（位运算）和布尔（逻辑）操作。

```csharp
bool clapClaps = (happy & knowIt);
```

```visual basic
Dim cHands As Boolean = (happy And knowIt)
```

在 Visual Basic 项目或源文件中应用 `Option Strict Off` 时，一个整数操作数和一个布尔操作数的 `And` 运算符将强制布尔值转换为整数（或长型），然后执行位运算。C# 不允许这种操作数类型的混合。

Visual Basic 确实包含其自身的 `&` 运算符。然而，它用于字符串拼接；不处理逻辑或位运算。

## && 逻辑与运算符

Visual Basic 的 `AndAlso` 运算符与 C# 的 `&&` 短路逻辑与运算符相同。

```csharp
if ((result != null) && (result.Length > 10))
```

```visual basic
If ((result Is Not Nothing) AndAlso
(result.Length > 10)) Then
```

## &= 赋值运算符

Visual Basic 不包含等同于 C# `&=` 运算符的操作。你必须在 VB 中分别执行逻辑与（And）和赋值操作。

```csharp
finalSet &= testFlag;
```

```visual basic
finalSet = finalSet And TestFlag
```

Visual Basic 包含其自身的 `&=` 运算符。然而，它结合了字符串拼接和赋值，不支持逻辑或位运算。

另请参

- 赋值运算符

- 转换表达式

另

- 转换与强制

- 表达式分组

当用于分组表达式时，Visual Basic 中的括号在语法上与 C# 中的分组括号相同。然而，在某些情况下，C# 要求对表达式加括号，但在 VB 中创建等效语句时括号是可选的。例如，C# 中 `if` 语句的条件必须括在括号内，但 Visual Basic 没有这一要求。

```csharp
// ----- C# 中必须使用括号。
if (totalCount >= 100)
```

```visual basic
' ----- Visual Basic 中括号可选可选。
If totalCount >= 100 Then
```

- 解引用运算符

Visual Basic 不对指针操作提供直接支持，因此不包含解引用运算符。

另请参

- 成员访问运算符，指针

## * 乘法运算符

Visual Basic 中的 `*` 乘法运算符在 C# 中使用相同的符号和语法。

```csharp
result = originalValue * 5;
```

```visual basic
result = originalValue * 5
```

## *= 赋值运算符

Visual Basic 的 `*=` 赋值运算符在语法和目的上与 C# 中的运算符相同。

```csharp
originalValue *= 5;
```

```visual basic
originalValue *= 5
```

另请参

赋值运算符

## + 加法运算符

C# 的 `+` 运算符既作为数值加法运算符，也作为字符串拼接运算符。

```csharp
int result = number1 + number2; // 加法
string greeting = "Hello, " + name; // 拼接
```

Visual Basic 中的 `+` 运算符也适用于加法和拼接。

```visual basic
Dim result As Integer = number1 + number2 ' 加法
Dim greeting As String =
  "Hello, " + name ' 拼接
```

然而，操作数的类型和 VB 中 `Option Strict` 语句的状态取决于其产生的影响。例如，当一个操作数是数值而另一个是字符串时，在使用 `Option Strict Off` 时 VB 会尝试将字符串转换为数字（即使是非数字字符串），而在使用 `Option Strict On` 时会产生编译错误。在遇到类似情况时，C# 会在拼接操作数之前将数字转换为字符串，而 VB 的 `+` 运算符并不这样做。为了避免此类语句产生歧义，Visual Basic 的 `&` 运算符是拼接字符串的首选工具，将运算符留给加法。

```visual basic
Dim result As Integer = number1 + number2 ' 加法
Dim greeting As String =
  "Hello, " & name ' 拼接
```
