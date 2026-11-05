# C# 语言规范 - ECMA-334，第 5 版，2017 年 12 月








## 前言

本规范取代了 ECMA-334:2006。相较于上一版的变更包括以下内容：

- 新增
  - `default` 和隐藏选项在 #line 预处理指令上
  - 不安全代码中的定长缓冲区
  - 自动实现的属性
  - 隐式类型的局部变量和数组
  - 对象和集合初始化器
  - 匿名类型
  - Lambda 表达式
  - 表达式树
  - 改进的类型推断
  - 扩展方法
  - 查询表达式
  - 可选参数
  - 命名参数
  - 泛型协变
  - 动态绑定
  - 异步函数
  - 调用方信息特性

- 删除
  - 空类型的概念

- 集成
  - 可空值类型
  - 泛型类型和函数
  - 迭代器

## 引言

本规范基于 Hewlett-Packard、Intel 和 Microsoft 提交的材料，该材料描述了一种名为 C# 的语言，该语言在 Microsoft 内部开发。该语言的主要发明者是 Anders Hejlsberg、Scott Wiltamuth 和 Peter Golde。C# 的第一个广泛分发的实现由 Microsoft 于 2000 年 7 月发布，作为其 .NET Framework 计划的一部分。

Ecma 技术委员会 39 (TC39) 工作组 2 (TG2) 于 2000 年 9 月成立，以制定 C# 标准。另一个工作组 TG3 也在当时成立，以制定一个名为通用语言基础结构 (CLI) 的库和执行环境的标准。（CLI 基于 .NET Framework 的子集。）尽管 Microsoft 对 C# 的实现依赖 CLI 提供库和运行时支持，但其他 C# 实现不必如此，前提是它们支持获取本 C# 标准（参见附录 C）所需的最小 CLI 功能的替代方式。

随着 C# 定义的演进，其设计中使用了以下目标：

- C# 旨在成为一种简单、现代、通用、面向对象的编程语言。
- 该语言及其实现应支持软件工程原则，例如强类型检查、数组边界检查、检测使用未初始化变量的尝试以及自动垃圾回收。软件的健壮性、持久性和程序员生产力很重要。
- 该语言旨在用于开发适合部署在分布式环境中的软件组件。
- 源代码可移植性非常重要，程序员可移植性也很重要，尤其是对于那些已经熟悉 C 和 C++ 的程序员。
- 国际化支持非常重要。
- C# 旨在适用于为托管和嵌入式系统编写应用程序，从使用复杂操作系统的非常大的系统，到具有专用功能的非常小的系统。
- 尽管 C# 应用程序旨在在内存和处理能力需求方面经济高效，但该语言并非旨在在性能和大小方面直接与 C 或汇编语言竞争。

## 1. 范围

本规范描述了用 C# 编程语言编写的程序的形式并确立了其解释。它描述了

- C# 程序的表示；
- C# 语言的语法和约束；
- 解释 C# 程序的语义规则；
- 符合 C# 的实现所施加的限制和限制。

本规范不描述

- C# 程序被转换以供数据处理系统使用的机制；
- C# 应用程序被调用以供数据处理系统使用的机制；
- 输入数据被转换以供 C# 应用程序使用的机制；
- 输出数据在由 C# 应用程序生成后被转换的机制；
- 程序及其数据的大小或复杂性超过任何特定数据处理系统或特定处理器容量的情况；
- 能够支持符合实现的数据处理系统的所有最低要求。

*符合程序*是指可被符合实现接受的程序。（此类程序允许包含扩展或条件性规范特性。）

## 2. 规范性引用文件

以下规范性文件包含条款，通过本文档中的引用，这些条款构成本规范的条款。对于有日期的引用，任何这些出版物的后续修正或修订均不适用。然而，基于本规范达成协议的各方应被鼓励调查应用下面指出的规范性文件最新版本的可行性。对于无日期的引用，适用的规范性文件为所引用的最新版本。ISO 和 IEC 维护当前有效规范的登记册。

- ISO/IEC 23271:2012, *通用语言基础结构 (CLI)，第 IV 部分：基类库 (BCL)、扩展数值库和扩展数组库。*
- ISO 31.11:1992, *量和单位 — 第 11 部分：用于物理科学和技术的数学符号和符号。*
- ISO/IEC 2382.1:1993, *信息技术 — 词汇 — 第 1 部分：基本术语。*
- ISO/IEC 10646（所有部分），*信息技术 — 通用多八位编码字符集（UCS）。*
- IEC 60559:1989, *微处理器系统的二进制浮点运算*（原指定为 IEC 559:1989）。（该标准以其美国国家指定名称 ANSI/IEEE 标准 754-1985 广为人知，*IEEE 二进制浮点运算标准*。）
- Unicode 联盟。Unicode 标准，http://www.unicode.org/standard/standard.html

## 4. 术语和定义

为本规范的目的，以下定义适用。其他术语在以 *斜体* 形式出现或出现在语法规则左侧时定义。本规范中明确定义的术语不应被推定为隐含指代其他地方定义的类似术语。本规范中未定义的术语应根据 ISO/IEC 2382.1 解释。本规范中未定义的数学符号应根据 ISO 31.11 解释。

- 4.1
  **应用程序**
  具有入口点的程序集

- 4.2
  **应用程序域**
  通过充当应用程序状态的容器来启用应用程序隔离的实体

- 4.3
  **参数**
  方法或实例构造函数调用表达式中由括号包围的逗号分隔列表中的表达式，或元素访问表达式中由方括号包围的表达式

- 4.4
  **程序集**
  编译器作为程序编译结果输出的一个或多个文件

- 4.5
  **行为**
  外部表现或动作

- 4.6
  **行为，实现定义**
  未指定的行为，其中每个实现都记录了如何做出选择

- 4.7
  **行为，未定义**
  在使用不可移植或错误的构造或错误数据时出现的行为，本规范对此不作任何要求

- 4.8
  **行为，未指定**
  本规范提供两种或多种可能性且不对任何实例中选择哪一种作出进一步要求的行为

- 4.9
  **字符**（在使用时未加限定词）
  a) 在非 Unicode 编码的上下文中——该编码中字符的含义；或
  b) 在字符字面量或类型为 char 的值的上下文中——范围为 U+0000 到 U+FFFF 的 Unicode 代码点（包括代理代码点），即 UTF-16 代码单元；或
  c) 否则——Unicode 代码点



### 4.10 类库
可供其他程序集使用的程序集

### 4.11 诊断消息
属于实现的输出消息中由实现定义的子集的消息

### 4.12 编译时错误
在程序翻译期间报告的错误

### 4.13 异常
在程序执行期间报告的异常条件

### 4.14 实现
特定软件集合（在特定控制选项下、特定翻译环境中运行），它为特定执行环境翻译程序并支持在该执行环境中执行方法

### 4.15 命名空间
对相关程序元素进行分组的逻辑组织系统

### 4.16 参数
作为方法、实例构造函数、运算符或索引器定义的一部分声明的变量，在进入该函数成员时获得值

### 4.17 程序
提供给编译器的一个或多个源文件

### 4.18 有效程序
根据语法规则和可诊断语义规则构造的 C# 程序

### 4.19 程序实例化
应用程序的执行

### 4.20 源文件
Unicode 字符的有序序列

### 4.21 不安全代码
允许执行诸如声明和操作指针、在指针与整型之间转换以及获取变量地址等较低级操作的代码

### 4.22 编译时警告
在程序翻译期间报告的信息性消息，旨在标识对程序元素的可能有问题用法

## 5. 缩略语和缩写

**本条为资料性。**

本规范通篇使用以下缩略语和缩写：

BCL — 基类库，提供用于表示 CLI 内置数据类型、简单文件访问、自定义特性、安全特性、字符串操作、格式化、流和集合的类型。

CLI — 公共语言基础结构

CLS — 公共语言规范

IEC — 国际电工委员会

IEEE — 电气电子工程师学会

ISO — 国际标准化组织

C# 名称读作“C Sharp”。

C# 名称写作拉丁大写字母 C（U+0043）后跟数字符号 #（U+0023）。

以下类型出现在本规范通篇。这些类型的完整名称（包括全局命名空间限定符）列于下方以供参考。在本规范通篇，这些类型将以完全限定名（省略全局命名空间限定符）或简单非限定类型名（省略命名空间）的形式出现。例如，本规范中使用的类型 ICollection<T> 始终表示类型 global::System.Collections.Generic.ICollection<T>。

- global::System.Action
- global::System.ArgumentException
- global::System.ArithmeticException
- global::System.Array
- global::System.ArrayTypeMismatchException
- global::System.Attribute
- global::System.AttributeTargets
- global::System.AttributeUsageAttribute
- global::System.Boolean
- global::System.Byte
- global::System.Char
- global::System.Collections.Generic.ICollection<T>
- global::System.Collections.Generic.IEnumerable<T>
- global::System.Collections.Generic.IEnumerator<T>
- global::System.Collections.Generic.IList<T>
- global::System.Collections.Generic.IReadOnlyCollection<out T>
- global::System.Collections.Generic.IReadOnlyList<out T>
- global::System.Collections.ICollection
- global::System.Collections.IEnumerable
- global::System.Collections.IList
- global::System.Collections.IEnumerator
- global::System.Decimal
- global::System.Delegate
- global::System.Diagnostics.ConditionalAttribute
- global::System.DivideByZeroException
- global::System.Double
- global::System.Enum
- global::System.Exception
- global::System.GC
- global::System.ICollection
- global::System.IDisposable
- global::System.IEnumerable
- global::System.IEnumerable<out T>
- global::System.IList
- global::System.IndexOutOfRangeException
- global::System.Int16
- global::System.Int32
- global::System.Int64
- global::System.IntPtr
- global::System.InvalidCastException
- global::System.InvalidOperationException
- global::System.Linq.Expressions.Expression<TDelegate>
- global::System.MemberInfo
- global::System.NotSupportedException
- global::System.Nullable<T>
- global::System.NullReferenceException
- global::System.Object
- global::System.ObsoleteAttribute
- global::System.OutOfMemoryException
- global::System.OverflowException
- global::System.Runtime.CompilerServices.CallerFileAttribute
- global::System.Runtime.CompilerServices.CallerLineNumberAttribute
- global::System.Runtime.CompilerServices.CallerMemberNameAttribute
- global::System.Runtime.CompilerServices.ICriticalNotifyCompletion
- global::System.Runtime.CompilerServices.IndexerNameAttribute
- global::System.Runtime.CompilerServices.INotifyCompletion
- global::System.Runtime.CompilerServices.TaskAwaiter
- global::System.Runtime.CompilerServices.TaskAwaiter<T>
- global::System.SByte
- global::System.Single
- global::System.StackOverflowException
- global::System.String
- global::System.SystemException
- global::System.Threading.Monitor
- global::System.Threading.Tasks.Task
- global::System.Threading.Tasks.Task<TResult>
- global::System.Type
- global::System.TypeInitializationException
- global::System.UInt16
- global::System.UInt32
- global::System.UInt64
- global::System.UIntPtr
- global::System.ValueType

资料性文本结束。

## 6. 一般说明

**本文为资料性。**

本规范旨在供实现者、学者和应用程序员使用。因此，它包含大量解释性材料，严格来说，这些材料在正式语言规范中并非必需。

本标准分为以下部分：

- 1. 前置内容（第 1—6 条）；
- 2. 语言语法、约束和语义（第 7—23 条）；
- 3. 附录

提供示例以说明所述构造的可能形式。引用用于指向相关条款。注释用于向实现者或程序员提供建议或指导。附录提供附加信息，并总结本规范中包含的信息。

第 1—4 条、第 6 条的一部分、第 7—22 条、第 23 条的开头以及附录 D 的大部分构成本标准的规范性部分。除开头部分外，第 23 条全部为有条件规范性。前言、引言、第 5 条、第 6 条的一部分、附录 A、B、C、附录 D、E 和 F 的一部分、注释和示例均为资料性。

**资料性文本结束。**

资料性文本通过以下方式表示：

- 1. 由“本条/本文为资料性”和“资料性文本结束”界定的完整或部分条款或附录。
- 2. [示例：以下示例……代码片段，可能带有一些叙述……示例结束]
- 3. [注：叙述……注结束]

所有未标记为资料性的文本均为规范性文本。

## 7. 词法结构

### 7.1 程序

C# 程序由一个或多个源文件组成，正式称为编译单元（§14.2）。源文件是 Unicode 字符的有序序列。源文件通常与文件系统中的文件一一对应，但不要求这种对应关系。

从概念上讲，程序通过三个步骤进行编译：

- 1. 转换：将文件从特定字符集和编码方案转换为 Unicode 字符序列。
- 2. 词法分析：将 Unicode 输入字符流转换为标记流。
- 3. 句法分析：将标记流转换为可执行代码。

符合要求的实现应接受以 UTF-8 编码形式（如 Unicode 标准所定义）编码的 Unicode 源文件，并将其转换为 Unicode 字符序列。

实现可以选择接受并转换其他字符编码方案（例如 UTF-16、UTF-32 或非 Unicode 字符映射）。

[注：Unicode NULL 字符（U+0000）的处理方式取决于具体实现。为了可移植性和可读性，强烈建议开发人员避免在源代码中使用该字符。当字符或字符串字面量中需要该字符时，可以改用转义序列 \0 或 \u0000。注结束]

[注：定义使用非 Unicode 字符表示的文件如何转换为 Unicode 字符序列超出了本标准的范围。不过，在此类转换过程中，建议将其他字符集中的常用行分隔字符（或序列）转换为由 Unicode 回车字符（U+000D）后跟 Unicode 换行字符（U+000A）组成的两字符序列。在大多数情况下，这种转换不会产生可见影响；但是，它会影响逐字字符串字面量标记（§7.4.5.6）的解释。该建议的目的是：当源文件在支持不同非 Unicode 字符集的系统之间移动时，特别是那些使用不同行分隔字符序列的系统之间移动时，允许逐字字符串字面量生成相同的字符序列。注结束]

### 7.2 语法

#### 7.2.1 概述

本规范使用两种语法来呈现 C# 编程语言的语法。词法语法（§7.2.2）定义如何组合 Unicode 字符以形成行终止符、空白、注释、标记和预处理指令。句法语法（§7.2.4）定义如何组合由词法语法产生的标记以形成 C# 程序。

#### 7.2.2 语法表示法

词法语法和句法语法使用语法产生式表示。每个语法产生式定义一个非终结符，以及该非终结符可展开为非终结符或终结符序列的可能方式。在语法产生式中，非终结符以斜体显示，终结符以固定宽度字体显示。

语法产生式的第一行是所定义非终结符的名称，后跟一个或两个冒号。句法语法中的产生式使用一个冒号，两个冒号用于一个

词法文法中的产生式。每个后续缩进行包含该非终结符的一种可能展开，该展开由非终结符或终结符符号的序列给出。[示例：产生式：

```
while-statement:
    while ( boolean-expression ) embedded-statement
```

定义 while-statement 由标记 while 组成，后跟标记“(”，后跟布尔表达式，后跟标记“)”，后跟嵌入语句。结束示例]

当非终结符符号存在多于一种可能展开时，备选项会分行列出。[示例：产生式：

```
statement-list:
    statement
    statement-list statement
```

定义 statement-list 要么由一个语句组成，要么由 statement-list 后跟一个语句组成。换言之，该定义是递归的，并规定语句列表由一个或多个语句组成。结束示例]

下标后缀“opt”用于表示可选符号。[示例：产生式：

```
block:
    { statement-list_opt }
```

是以下内容的简写：

```
block:
    { }
    { statement-list }
```

并定义 block 由括在“{”和“}”标记中的可选 statement-list 组成。结束示例]

备选项通常分行列出，但在备选项很多的情况下，短语“one of”可以位于单行列出的展开列表之前。这只是将每个备选项分别列在一行上的简写。[示例：产生式：

```
real-type-suffix:: one of
    F f D d M m
```

是以下内容的简写：

```
real-type-suffix::
    F
    f
    D
    d
    M
    m
```

结束示例]

所有终结符字符应理解为范围 U+0020 到 U+007F 中的相应 Unicode 字符，而不是其他 Unicode 字符范围中任何外观相似的字符。

#### 7.2.3 词法文法

C# 的词法文法在 §7.3、§7.4 和 §7.5 中给出。词法文法的终结符是 Unicode 字符集的字符，词法文法规定如何将字符合并成标记（§7.4）、空白（§7.3.4）、注释（§7.3.3）和预处理指令（§7.5）。

C# 程序中的每个源文件都应符合词法文法的 input 产生式（§7.3.1）。

#### 7.2.4 句法文法

C# 的句法文法在本子条款之后的各条款、子条款和附录中给出。句法文法的终结符是由词法文法定义的标记，句法文法规定如何将标记组合成 C# 程序。

C# 程序中的每个源文件都应符合句法文法的编译单元产生式（§14.2）。

#### 7.2.5 文法歧义

简单名（§12.7.3）和成员访问（§12.7.5）的产生式可能在表达式文法中引起歧义。[示例：语句：

```
F(G<A, B>(7));
```

可解释为对 F 的调用，该调用有两个参数：G < A 和 B > (7)。或者，也可解释为对 F 的调用，该调用有一个参数，而这个参数是对泛型方法 G 的调用，G 具有两个类型参数和一个常规参数。结束示例]

如果标记序列可以（在上下文中）分析为以类型参数列表（§9.4.2）结尾的简单名（§12.7.3）、成员访问（§12.7.5）或指针成员访问（§23.6.3），则检查紧跟在闭合 > 标记之后的标记。如果它是以下之一

- `(`
- `)`
- `]`
- `:`
- `;`
- `,`
- `.`
- `?`
- `==`
- `!=`

则保留该类型参数列表，作为简单名、成员访问或指针成员访问的一部分，并丢弃该标记序列的任何其他可能分析。否则，即使该标记序列没有其他可能分析，也不将类型参数列表视为简单名、成员访问或指针成员访问的一部分。[注意：在分析命名空间或类型名（§8.8）中的类型参数列表时，不应用这些规则。结束注意] [示例：语句：

```
F(G<A, B>(7));
```

根据此规则，将被解释为对 F 的调用，该调用有一个参数，而这个参数是对泛型方法 G 的调用，G 具有两个类型参数和一个常规参数。语句

```
F(G<A, B>7);
F(G<A, B>>7);
```

将分别被解释为对 F 的调用，该调用有两个参数。语句

```
x = F<A> + y;
```

### 7.3 词法分析

#### 7.3.1 概述

input 产生式定义 C# 源文件的词法结构。C# 程序中的每个源文件都应符合此词法文法产生式。

```
input::
    input-section_opt

input-section::
    input-section-part
    input-section input-section-part

input-section-part::
    input-elements_opt new-line
    pp-directive

input-elements::
    input-element
    input-elements input-element

input-element::
    whitespace
    comment
    token
```

五个基本元素构成 C# 源文件的词法结构：行终止符（§7.3.2）、空白（§7.3.4）、注释（§7.3.3）、标记（§7.4）和预处理指令（§7.5）。在这些基本元素中，只有标记在 C# 程序的句法文法（§7.2.4）中是有意义的，除非 > 标记与另一个标记组合形成单个运算符（§7.4.6）。

C# 源文件的词法处理包括将文件归约为标记序列，该序列成为句法分析的输入。行终止符、空白和注释可用于分隔标记，预处理指令可使源文件的部分内容被跳过，但除此之外，这些词法元素对 C# 程序的句法结构没有影响。

当多个词法文法产生式匹配源文件中的字符序列时，词法处理总是形成尽可能长的词法元素。[示例：字符序列 // 被处理为单行注释的开头，因为该词法元素比单个 / 标记更长。结束示例]

#### 7.3.2 行终止符

行终止符将 C# 源文件的字符划分为行。

```
new-line::
    Carriage return character (U+000D)
    Line feed character (U+000A)
    Carriage return character (U+000D) followed by line feed character (U+000A)
    Next line character (U+0085)
    Line separator character (U+2028)
    Paragraph separator character (U+2029)
```

为了与添加文件尾标记的源代码编辑工具兼容，并使源文件能够被视为由正确终止的行组成的序列，对 C# 程序中的每个源文件按顺序应用以下转换：

- 如果源文件的最后一个字符是 Control-Z 字符（U+001A），则删除该字符。
- 如果源文件非空，且源文件的最后一个字符不是回车（U+000D）、换行（U+000A）、下一行字符（U+0085）、行分隔符（U+2028）或段落分隔符（U+2029），则在源文件末尾添加回车字符（U+000D）。[注意：额外的回车允许程序以没有终止换行符的 pp 指令（§7.5）结束。结束注意]

#### 7.3.3 注释

支持两种形式的注释：分隔注释和单行注释。

分隔注释以字符 /* 开头，以字符 */ 结尾。分隔注释可以占据一行的一部分、单行或多行。[示例：该示例

注释不嵌套。字符序列 /* 和 */ 在单行注释中没有特殊含义，字符序列 // 和 /* 在分隔注释中没有特殊含义。

在字符字面量和字符串字面量中不处理注释。

[注意：必须仔细解释这些规则。例如，在下面的示例中，从 A 之前开始的分隔注释在 B 和 C() 之间结束。原因是

```
// B */ C();
```

实际上并不是单行注释，因为 // 在分隔注释中没有特殊含义，因此 */ 在该行中确实具有其通常的特殊含义。

同样，从 D 之前开始的分隔注释在 E 之前结束。原因是 "D */ " 实际上并不是字符串字面量，因为它出现在分隔注释内部。

/* 和 */ 在单行注释中没有特殊含义的一个有用结果是，可以通过在每一行开头放置 // 来注释掉一块源代码行。一般来说，将 /* 放在这些行之前、将 */ 放在它们之后并不可行，因为这不能正确地将块中的分隔注释封装起来，而且通常可能会完全改变此类分隔注释的结构。

示例代码：

```
static void Main() {
    /* A
    // B */ C();
    Console.WriteLine(/* "D */ "E");
}
```

结束注意]

#### 7.3.4 空白

空白定义为 Unicode 类 Zs 的任何字符（包括空格字符），以及水平制表符、垂直制表符和换页符。

```
whitespace::
    whitespace-character
    whitespace whitespace-character

whitespace-character::
    Any character with Unicode class Zs
    Horizontal tab character (U+0009)
    Vertical tab character (U+000B)
    Form feed character (U+000C)
```

### 7.4 标记

#### 7.4.1 概述

标记有几种：标识符、关键字、字面量、运算符和标点符号。空白和注释不是标记，尽管它们充当标记的分隔符。

```
token::
    identifier
    keyword
    integer-literal
    real-literal
    character-literal
    string-literal
    operator-or-punctuator
```



#### 7.4.2 Unicode 字符转义序列

一个 Unicode 转义序列表示一个 Unicode 代码点。Unicode 转义序列在标识符 (§7.4.3)、字符字面量 (§7.4.5) 和常规字符串字面量 (§7.4.5.6) 中被处理。Unicode 转义序列在任何其他位置都不被处理（例如，用于形成运算符、标点符号或关键字）。

```
unicode-escape-sequence::
    \u hex-digit hex-digit hex-digit hex-digit
    \U hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit
```

一个 Unicode 字符转义序列表示由 "\u" 或 "\U" 字符后跟的十六进制数字形成的单个 Unicode 代码点。由于 C# 在字符和字符串值中使用 Unicode 代码点的 16 位编码，范围为 U+10000 到 U+10FFFF 的 Unicode 代码点使用两个 Unicode 代理代码单元表示。字符字面量中不允许使用大于 U+FFFF 的 Unicode 代码点。大于 U+10FFFF 的 Unicode 代码点无效且不受支持。

多次转换不会执行。例如，字符串字面量 "\u005C\u005C" 等价于 "\u005C"，而不是 "\"。[注意：Unicode 值 \u005C 是字符 "\"。结束注释]

[示例] 示例

```
class Class1
{
    static void Test(bool \u0066) {
        char c = '\u0066';
        if (\u0066)
            System.Console.WriteLine(c.ToString());
    }
}
```

显示了 \u0066 的几种用法，它是字母 "f" 的转义序列。该程序等价于

```
class Class1
{
    static void Test(bool f) {
        char c = 'f';
        if (f)
            System.Console.WriteLine(c.ToString());
    }
}
```

结束示例]

#### 7.4.3 标识符

本小节中给出的标识符规则与 Unicode 标准附录 15 中推荐的规则完全对应，只是允许下划线作为初始字符（这是 C 编程语言中的传统做法）。标识符中允许使用 Unicode 转义序列，并且允许使用 "@" 字符作为前缀以使关键字可作为标识符使用。

```
identifier::
    available-identifier
    @ identifier-or-keyword

available-identifier::
    An identifier-or-keyword that is not a keyword

identifier-or-keyword::
    identifier-start-character identifier-part-characters_opt

identifier-start-character::
    letter-character
    underscore-character
```

underscore-character::
_（下划线字符 U+005F）
表示字符 U+005F 的 unicode-escape-sequence

identifier-part-characters::
identifier-part-character
identifier-part-characters identifier-part-character

identifier-part-character::
letter-character
decimal-digit-character
connecting-character
combining-character
formatting-character

letter-character::
A Unicode character of classes Lu, Ll, Lt, Lm, Lo, or Nl
表示类为 Lu、Ll、Lt、Lm、Lo 或 Nl 的字符的 unicode-escape-sequence

combining-character::
A Unicode character of classes Mn or Mc
表示类为 Mn 或 Mc 的字符的 unicode-escape-sequence

decimal-digit-character::
A Unicode character of the class Nd
表示类为 Nd 的字符的 unicode-escape-sequence

connecting-character::
A Unicode character of the class Pc
表示类为 Pc 的字符的 unicode-escape-sequence

formatting-character::
A Unicode character of the class Cf
表示类为 Cf 的字符的 unicode-escape-sequence

> [注意：有关上面提到的 Unicode 字符类的信息，请参阅《Unicode 标准》。结束注释]

> [示例：有效标识符的示例包括“identifier1”、“_identifier2”和“@if”。结束示例]

符合规范的程序中的标识符应采用 Unicode 标准附录 15 中定义的 Unicode 正规化形式 C 定义的规范格式。遇到不在正规化形式 C 中的标识符时的行为是实现定义的；然而，不要求诊断。

前缀“@”使关键字可作为标识符使用，这在与其他编程语言接口时很有用。字符 @ 实际上不是标识符的一部分，因此该标识符在其他语言中可能被视为普通标识符，而没有前缀。带 @ 前缀的标识符称为逐字标识符。[注意：对非关键字的标识符使用 @ 前缀是允许的，但作为风格问题强烈不建议。结束注释]

> [示例：示例：

```
class @class
{
  public static void @static(bool @bool) {
    if (@bool)
      System.Console.WriteLine("true");
    else
      System.Console.WriteLine("false");
  }
}
```

```
class Class1
{
    static void M() {
        cl\u0061ss.st\u0061tic(true);
    }
}
```

定义了一个名为“Class”的类，其中有一个名为“static”的静态方法，参数名为“bool”。请注意，由于关键字中不允许使用 Unicode 转义，因此标记“cl\u0061ss”是一个标识符，与“@class”是同一个标识符。*结束示例*

如果在应用以下转换后两个标识符相同，则认为它们是同一个标识符，按顺序：

- 如果使用，则删除前缀“@”。
- 每个 *Unicode 转义序列* 转换为其对应的 Unicode 字符。
- 删除任何 *格式字符*。

包含两个连续下划线字符（U+005F）的标识符保留供实现使用；然而，如果定义了此类标识符，则不要求诊断。[注意：例如，实现可能提供以两个下划线开头的扩展关键字。*结束注释*]

#### 7.4.4 关键字

*关键字* 是类似标识符的字符序列，被保留，除非以 @ 字符为前缀，否则不能用作标识符。

```
keyword: one of
    abstract    as         base       bool       break
    byte        case       catch      char       checked
    class       const      continue   decimal    default
    delegate    do         double     else       enum
    event       explicit   extern     false      finally
    fixed       float      for        foreach    goto
    if          implicit   in         int        interface
    internal    is         lock       long       namespace
    new         null       object     operator   out
    override    params     private    protected  public
    readonly    ref        return     sbyte      sealed
    short       sizeof     stackalloc static     string
    struct      switch     this       throw      true
    try         typeof     uint       ulong      unchecked
    unsafe      ushort     using      virtual    void
    volatile    while
```

*上下文关键字* 是类似标识符的字符序列，在某些上下文中具有特殊含义，但未被保留，可以在这些上下文之外以及以 @ 字符为前缀时用作标识符。

```
contextual-keyword: one of the following identifiers
    add        alias      ascending  async      await
    by         descending dynamic    equals     from
    get        global     group      into       join
    let        orderby    partial    remove     select
    set        value      var        where      yield
```

在大多数情况下，上下文关键字的语法位置使其永远不会与普通标识符用法混淆。例如，在属性声明中，“get”和“set”标识符具有特殊含义 (§15.7.3)。在这些位置不允许使用 get 或 set 以外的标识符，因此这种用法不会与将这些词用作标识符的用法冲突。

在某些情况下，语法不足以区分上下文关键字用法和标识符。在所有此类情况下，将指定如何在这两者之间进行区分。例如，在隐式类型局部变量声明 (§13.6.2) 中，上下文关键字 var 可能与名为 var 的声明类型冲突，在这种情况下，声明的名称优先于标识符作为上下文关键字的用法。

这种消歧的另一个示例是上下文关键字 await (§12.8.8.1)，它仅在声明为 async 的方法内部时才被视为关键字，但在其他地方可以用作标识符。

与关键字一样，上下文关键字也可以通过在其前面加上 @ 字符来用作普通标识符。

> [注意：当用作上下文关键字时，这些标识符不能包含 unicode-escape-sequences。结束注释]。

#### 7.4.5 字面量

##### 7.4.5.1 通用

字面量 (§12.7.2) 是值的源代码表示。

```
literal::
    boolean-literal
    integer-literal
    real-literal
    character-literal
    string-literal
    null-literal
```

##### 7.4.5.2 布尔字面量

有两个布尔字面量值：true 和 false。

```
boolean-literal::
    true
    false
```

boolean-literal 的类型是 bool。

##### 7.4.5.3 整数字面量

整数字面量用于编写 int、uint、long 和 ulong 类型的值。整数字面量有两种可能形式：十进制和十六进制。




```
hex-digits::
    hex-digit
    hex-digits hex-digit

hex-digit:: one of
    0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f
```

整型字面量的类型按如下方式确定：

- 如果字面量没有后缀，则其类型为能够表示其值的这些类型中的第一个：int、uint、long、ulong。
- 如果字面量带有后缀 U 或 u，则其类型为能够表示其值的这些类型中的第一个：uint、ulong。
- 如果字面量带有后缀 L 或 l，则其类型为能够表示其值的这些类型中的第一个：long、ulong。
- 如果字面量带有后缀 UL、Ul、uL、ul、LU、Lu、lU 或 lu，则其类型为 ulong。

如果整型字面量表示的值超出 ulong 类型的范围，则发生编译时错误。

> [注意：从风格上考虑，建议在书写 long 类型字面量时使用“L”而不是“l”，因为字母“l”很容易与数字“1”混淆。注意结束]

为了允许将尽可能最小的 int 和 long 值写成整型字面量，存在以下两条规则：

- 当表示值 2147483648（2^31）且没有整型类型后缀的整型字面量作为一元减号运算符标记（§12.8.3）之后紧邻的标记出现时，结果（两个标记的结果）是类型为 int、值为 -2147483648（-2^31）的常量。在所有其他情况下，这种整型字面量的类型为 uint。
- 当表示值 9223372036854775808（2^63）且没有整型类型后缀或整型类型后缀为 L 或 l 的整型字面量作为一元减号运算符标记（§12.8.3）之后紧邻的标记出现时，结果（两个标记的结果）是类型为 long、值为 -9223372036854775808（-2^63）的常量。在所有其他情况下，这种整型字面量的类型为 ulong。

##### 7.4.5.4 实数字面量

实数字面量用于书写 float、double 和 decimal 类型的值。

```
real-literal::
    decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
    . decimal-digits exponent-part_opt real-type-suffix_opt
    decimal-digits exponent-part real-type-suffix_opt
    decimal-digits real-type-suffix

exponent-part::
    e sign_opt decimal-digits
    E sign_opt decimal-digits

sign:: one of
    + -

real-type-suffix:: one of
    F f D d M m
```

如果未指定实型类型后缀，则实数字面量的类型为 double。否则，实型类型后缀决定实数字面量的类型，如下所示：

- 带有后缀 F 或 f 的实数字面量类型为 float。[示例：字面量 1f、1.5f、1e10f 和 123.456F 均为 float 类型。示例结束]
- 带有后缀 D 或 d 的实数字面量类型为 double。[示例：字面量 1d、1.5d、1e10d 和 123.456D 均为 double 类型。示例结束]
- 带有后缀 M 或 m 的实数字面量类型为 decimal。[示例：字面量 1m、1.5m、1e10m 和 123.456M 均为 decimal 类型。示例结束] 此字面量通过取精确值转换为 decimal 值，如有必要，使用银行家舍入法（§9.3.8）舍入到最接近的可表示值。除非值被舍入，否则字面量中出现的任何小数位数都会保留。[注意：因此，字面量 2.900m 将被解析为符号为 0、系数为 2900、小数位数为 3 的 decimal。注意结束]

如果指定字面量的量级太大，无法在指示的类型中表示，则发生编译时错误。[注意：特别地，实数字面量永远不会产生浮点无穷大。但是，非零实数字面量可能会被舍入为零。注意结束]

float 或 double 类型的实数字面量的值通过使用 IEC 60559“舍入到最接近”模式确定，其中平局打破为“偶数”（最低有效位为零的值），并且所有数字均视为有效。

[注意：在实数字面量中，小数点后始终需要十进制数字。例如，1.3F 是实数字面量，但 1.F 不是。注意结束]

##### 7.4.5.5 字符字面量

字符字面量表示单个字符，由引号中的字符组成，如 'a'。

```
character-literal::
  ' character '

character::
  single-character
  simple-escape-sequence
  hexadecimal-escape-sequence
  unicode-escape-sequence

single-character::
  Any character except ' (U+0027), \ (U+005C), and new-line-character

simple-escape-sequence:: one of
  \' \" \\ \0 \a \b \f \n \r \t \v

hexadecimal-escape-sequence::
  \x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt
```

[注意：字符字面量中反斜杠字符（\\）之后的字符必须是以下字符之一：'、\"、\\、0、a、b、f、n、r、t、u、U、x、v。否则，发生编译时错误。注意结束]

> [注意：使用 \x 十六进制转义序列产生式可能容易出错且难以阅读，因为 \x 后面的十六进制数字位数可变。例如，在以下代码中：
string good = "\x9Good text";
string bad = "\x9Bad text";
乍看之下，两个字符串中的前导字符可能相同（U+0009，制表符）。实际上第二个字符串以 U+9BAD 开头，因为单词“Bad”中的所有三个字母都是有效的十六进制数字。从风格上考虑，建议避免使用 \x，而使用特定转义序列（本例中为 \t）或固定长度的 \u 转义序列。注意结束]

十六进制转义序列表示单个 Unicode UTF-16 代码单元，其值由“\x”后面的十六进制数字构成。

如果字符字面量表示的值大于 U+FFFF，则发生编译时错误。

字符字面量中的 Unicode 转义序列（§7.4.2）应处于 U+0000 到 U+FFFF 的范围内。

```
verbatim-string-literal::
  @" verbatim-string-literal-characters_opt "
verbatim-string-literal-characters::
  verbatim-string-literal-character
  verbatim-string-literal-characters verbatim-string-literal-character
verbatim-string-literal-character::
  single-verbatim-string-literal-character
  quote-escape-sequence
single-verbatim-string-literal-character::
  Any character except "
quote-escape-sequence::
  ""
```

```
[Example: The example
string a = "Happy birthday, Joel";      // Happy birthday, Joel
string b = @"Happy birthday, Joel";     // Happy birthday, Joel
string c = "hello \t world";            // hello    world
string d = @"hello \t world";           // hello \t world
string e = "Joe said \"Hello\" to me";  // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me"; // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt"; // \\server\share\file.txt
string h = @"\\server\share\file.txt";   // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

展示了各种字符串字面量。最后一个字符串字面量 j 是跨多行的逐字字符串字面量。引号之间的字符（包括换行符等空白）均逐字保留，每一对双引号字符替换为一个这样的字符。示例结束

> [注意：逐字字符串字面量中的任何换行都是结果字符串的一部分。如果用于形成换行的确切字符对应用程序具有语义相关性，那么任何将源代码中的换行转换为不同格式（例如在“\n”和“\r\n”之间）的工具都会改变应用程序行为。开发人员在此类情况下应小心。注意结束]

> [注意：由于十六进制转义序列可以有可变数量的十六进制数字，字符串字面量 "\x123" 包含一个十六进制值为 123 的单个字符。要创建包含十六进制值为 12 的字符后跟字符 3 的字符串，可以改为写 "\x00123" 或 "\x12" + "3"。注意结束]

字符串字面量的类型为 string。

每个字符串字面量不一定都会产生新的字符串实例。当两个或多个根据字符串相等运算符（§12.11.8）等价的字符串字面量出现在同一程序集中时，这些字符串字面量引用同一个字符串实例。[示例：例如，由以下代码产生的输出

```
class Test
{
  static void Main() {
    object a = "hello";
    object b = "hello";
    System.Console.WriteLine(a == b);
  }
}
```

为 True，因为这两个字面量引用同一个字符串实例。示例结束]



##### 7.4.5.6 空字面量

```
    null-literal::
        null
```

一个空字面量表示空值。它没有类型，但可以通过空字面量转换（§11.2.6）转换为任何引用类型或可空值类型。

#### 7.4.6 运算符和标点符号

有几种类型的运算符和标点符号。运算符用于在表达式中描述涉及一个或多个操作数的操作。*[示例：表达式 a + b 使用 + 运算符将两个操作数 a 和 b 相加。结束示例]* 标点符号用于分组和分隔。

```
    operator-or-punctuator:: one of
    {     }     [     ]     (     )     .     ,     :     ;
    +     -     *     /     %     &     |     ^     !     ~
    =     <     >     ?     ??    ::    ++    --    &&    ||
    ->    ==    !=    <=    >=    +=    -=    *=    /=    %=
    &=    |=    ^=    <<    <<=   >>    >>=
```

```
    right-shift::
        > >
```

```
    right-shift-assignment::
        > >=
```

*右移* 由两个标记 > 和 > 组成。类似地，*右移赋值* 由两个标记 > 和 >= 组成。与语法规范中的其他产生式不同，在这些产生式的每个中，两个标记之间不允许有任何字符（甚至空白）。这些产生式被特殊处理，以便能够正确处理类型参数列表（§15.2.3）。*[注释：在向 C# 添加泛型之前，>> 和 >>= 都是单个标记。然而，泛型的语法使用 < 和 > 字符来分隔类型参数和类型参数。经常希望使用嵌套的构造类型，例如 `List<Dictionary<string, int>>`。而不是要求程序员用空格分隔 > 和 >，这两个运算符或标点的定义被更改了。结束注释]*

### 7.5 预处理指令

#### 7.5.1 通用

预处理指令提供有条件地跳过源文件部分、报告错误和警告条件以及划分源代码不同区域的能力。*[注释：术语“预处理指令”仅用于与 C 和 C++ 编程语言保持一致。在 C# 中没有单独的预处理步骤；预处理指令作为词法分析阶段的一部分进行处理。结束注释]*

```
    pp-directive::
        pp-declaration
        pp-conditional
        pp-line
        pp-diagnostic
        pp-region
        pp-pragma
```

以下预处理指令可用：

- `#define` 和 `#undef`，分别用于定义和取消定义条件编译符号（§7.5.4）。
- #if、#elif、#else 和 #endif，用于有条件地跳过源代码部分（§7.5.5）。
- #line，用于控制为错误和警告发出的行号（§7.5.8）。
- #error，用于发出错误（§7.5.6）。
- #region 和 #endregion，用于显式标记源代码部分（§7.5.7）。
- #pragma，用于向编译器指定可选的上下文信息（§7.5.9）。

一个预处理指令始终占用源代码的单独一行，并且始终以 # 字符和预处理指令名称开头。在 # 字符之前以及 # 字符和指令名称之间可能出现空白。

包含 #define、#undef、#if、#elif、#else、#endif、#line 或 #endregion 指令的源行可以以单行注释结束。定界注释（/* */ 风格的注释）在包含预处理指令的源行上是不允许的。

预处理指令不是标记，也不是 C# 语法规范的一部分。然而，预处理指令可用于包含或排除标记序列，从而以这种方式影响 C# 程序的含义。[示例：当编译时，程序

```
#define A
#undef B
class C
{
#if A
void F() {}
#else
void G() {}
#endif

#if B
void H() {}
#else
void I() {}
#endif
}
```

结果与程序

```
class C
{
    void F() {}
    void I() {}
}
```

相同。因此，在词法上，这两个程序截然不同，在语法上，它们是相同的。结束示例]

#### 7.5.2 条件编译符号

#if、#elif、#else 和 #endif 指令提供的条件编译功能通过预处理表达式（§7.5.3）和条件编译符号控制。

conditional-symbol::
除 true 或 false 之外的任何标识符或关键字

如果两个条件编译符号在应用以下转换后相同，则被视为相同，按顺序：

- 每个 unicode-escape-sequence 转换为其对应的 Unicode 字符。
- 任何格式字符都被删除。

一个条件编译符号有两个可能的状态：已定义或未定义。在源文件的词法处理开始时，条件编译符号未定义，除非它已被外部机制（例如命令行编译器选项）显式定义。当处理 #define 指令时，该指令中命名的条件编译符号在该
源文件中变为已定义。该符号保持已定义状态，直到处理了针对同一符号的 #undef 指令，或直到到达源文件的末尾为止。其含义之一是，一个源文件中的 #define 和 #undef 指令对同一程序中的其他源文件没有影响。

当在预处理表达式（§7.5.3）中引用时，已定义的条件编译符号具有布尔值 true，未定义的条件编译符号具有布尔值 false。条件编译符号在预处理表达式中被引用之前不需要显式声明。相反，未声明的符号 simply 未定义，因此其值为 false。

条件编译符号的命名空间与 C# 程序中的所有其他命名实体是不同且独立的。条件编译符号只能在 #define 和 #undef 指令以及预处理表达式中引用。

#### 7.5.3 预处理表达式

预处理表达式可以出现在 #if 和 #elif 指令中。运算符 !、==、!=、&& 和 || 在预处理表达式中允许使用，并且可以使用括号进行分组。

```
pp-expression:::
    whitespace_opt pp-or-expression whitespace_opt
pp-or-expression:::
    pp-and-expression
    pp-or-expression whitespace_opt || whitespace_opt pp-and-expression
pp-and-expression:::
    pp-equality-expression
    pp-and-expression whitespace_opt && whitespace_opt pp-equality-expression
pp-equality-expression:::
    pp-unary-expression
    pp-equality-expression whitespace_opt == whitespace_opt pp-unary-expression
    pp-equality-expression whitespace_opt != whitespace_opt pp-unary-expression
pp-unary-expression:::
    pp-primary-expression
    ! whitespace_opt pp-unary-expression
pp-primary-expression:::
    true
    false
    conditional-symbol
    ( whitespace_opt pp-expression whitespace_opt )
```

当在预处理表达式中引用时，已定义的条件编译符号具有布尔值 true，未定义的条件编译符号具有布尔值 false。

预处理表达式的求值始终产生布尔值。预处理表达式的求值规则与常量表达式（§12.20）的规则相同，只是唯一可以引用的用户定义实体是条件编译符号。

#### 7.5.4 定义指令

定义指令用于定义或取消定义条件编译符号。

```
pp-declaration:::
    whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
    whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line
pp-new-line:::
    whitespace_opt single-line-comment_opt new-line
```



处理 `#define` 指令会使给定的条件编译符号从该指令之后的源代码行开始被定义。同样地，处理 `#undef` 指令会使给定的条件编译符号从该指令之后的源代码行开始被取消定义。

源文件中的任何 `#define` 和 `#undef` 指令都必须出现在源文件中的第一个标记 (§7.4) 之前；否则会发生编译时错误。直观地说，`#define` 和 `#undef` 指令必须位于源文件中的任何“实际代码”之前。

[示例：示例：

```
#define Enterprise
#if Professional || Enterprise
#define Advanced
#endif
namespace Megacorp.Data
{
#if Advanced
    class PivotTable {...}
#endif
}
```

是有效的，因为 `#define` 指令位于源文件中第一个标记（命名空间关键字）之前。

示例结束

[示例：以下示例因 `#define` 出现在实际代码之后而导致编译时错误：

```
#define A
namespace N
{
#define B
#if B
class Class1 {}
#endif
}
```

示例结束

`#define` 可以定义一个已经定义的条件编译符号，而无需对该符号进行 intervening `#undef`。 [示例：下面的示例定义了一个条件编译符号 A，然后再次定义它。
#define A
#define A
对于允许将条件编译符号作为编译选项定义的编译器，此类重定义发生的另一种方式是同时将符号作为编译器选项以及在源中定义。 示例结束
`#undef` 可以“取消定义”未定义的条件编译符号。 [示例：下面的示例定义了一个条件编译符号 A，然后两次取消定义它；尽管第二次 `#undef` 没有任何效果，但它仍然有效。
#define A
#undef A
#undef A
示例结束

#### 7.5.5 条件编译指令

条件编译指令用于有条件地包含或排除源文件的一部分。

```
pp-conditional::
  pp-if-section  pp-elif-sections_opt  pp-else-section_opt  pp-endif
pp-if-section::
  whitespace_opt # whitespace_opt if whitespace pp-expression  pp-new-line
  conditional-section_opt
pp-elif-sections::
  pp-elif-section
  pp-elif-sections pp-elif-section
pp-elif-section::
  whitespace_opt # whitespace_opt elif whitespace pp-expression  pp-new-line
  conditional-section_opt
pp-else-section::
  whitespace_opt # whitespace_opt else pp-new-line  conditional-section_opt
pp-endif::
  whitespace_opt # whitespace_opt endif pp-new-line
conditional-section::
  input-section
  skipped-section
skipped-section::
  skipped-section-part
  skipped-section  skipped-section-part
skipped-section-part::
  skipped-characters_opt  new-line
  pp-directive
skipped-characters::
  whitespace_opt  not-number-sign  input-characters_opt
not-number-sign::
  Any input-character except #
```

[注意：正如语法所示，条件编译指令应作为一组按顺序编写，由 `#if` 指令、零个或多个 `#elif` 指令、零个或一个 `#else` 指令以及一个 `#endif` 指令组成。指令之间是源代码的条件部分。每个部分由紧接其前的指令控制。条件部分本身可以包含嵌套的条件编译指令，前提是这些指令形成完整的集合。 注意结束]

`pp-conditional` 最多选择其中一个包含的条件部分进行正常词法处理：

- `#if` 和 `#elif` 指令的 `pp-expression` 按顺序求值，直到有一个产生 true。如果表达式产生 true，则选择对应指令的条件部分。
- 如果所有 `pp-expression` 都产生 false，并且存在 `#else` 指令，则选择 `#else` 指令的条件部分。
- 否则，不选择任何条件部分。

如果有选择的条件部分，则将其作为正常的 input-section 处理：该部分中包含的源代码必须符合词法语法；从该部分中的源代码生成标记；并且该部分中的预处理指令具有规定的效果。

如果有剩余的条件部分，则将其作为 skipped-section 处理：除预处理指令外，该部分中的源代码不必符合词法语法；不会从该部分中的源代码生成标记；并且该部分中的预处理指令在词法上必须正确，但不会被进一步处理。在正在作为 skipped-section 处理的条件部分内，

任何嵌套的条件部分（包含在嵌套的 `#if...#endif` 和 `#region...#endregion` 构造中）也作为 skipped-section 处理。

[示例：以下示例说明了条件编译指令如何嵌套：]

```
#define Debug    // Debugging on
#undef Trace    // Tracing off
class PurchaseTransaction
{
    void Commit() {
#if Debug
    CheckConsistency();
#if Trace
    WriteToLog(this.ToString());
#endif
#endif
    CommitHelper();
    }
    ...
}
```

除预处理指令外，被跳过的源代码不受词法分析的约束。例如，尽管 `#else` 部分中存在未终止的注释，以下内容仍然有效：

```
#define Debug    // Debugging on
class PurchaseTransaction
{
    void Commit() {
#if Debug
        CheckConsistency();
#else /* Do something else
#endif
    }
    ...
}
```

然而，预处理指令即使在被跳过的源代码部分中也必须在词法上正确。

当预处理指令出现在多行输入元素内部时，不会对其进行处理。例如，程序：

```
class Hello
{
    static void Main() {
        System.Console.WriteLine(@"hello,
#if Debug
world
#else
Nebraska
#endif
");
    }
}
```

结果输出为：

```
hello,
#if Debug
world
#else
Nebraska
#endif
```

在特殊情况下，处理的预处理指令集可能取决于 `pp-expression` 的求值。示例：

```
#if X
/*
#else
/* */ class Q { }
#endif
```

始终产生相同的标记流（`class Q { }`），无论 X 是否定义。如果定义了 X，则由于多行注释，仅处理 `#if` 和 `#endif`。如果 X 未定义，则三个指令（`#if`、`#else`、`#endif`）都是指令集的一部分。 示例结束

#### 7.5.6 诊断指令

诊断指令用于显式生成错误和警告消息，这些消息以与其他编译时错误和警告相同的方式报告。

```
pp-diagnostic::
    whitespace_opt # whitespace_opt error pp-message
    whitespace_opt # whitespace_opt warning pp-message
```

```
pp-message::
    new-line
    whitespace input-characters_opt new-line
```

[示例：示例

```
#if Debug && Retail
#error A build can't be both debug and retail
#endif
class Test {...}
```

如果同时定义了条件编译符号 Debug 和 Retail，则会产生编译时错误（“A build can't be both debug and retail”）。请注意，`pp-message` 可以包含任意文本；具体来说，它不必包含格式良好的标记，正如单词 can't 中的单引号所示。 示例结束

#### 7.5.7 区域指令

区域指令用于显式标记源代码的区域。

```
pp-region::
    pp-start-region conditional-section_opt pp-end-region

pp-start-region::
    whitespace_opt # whitespace_opt region pp-message

pp-end-region::
    whitespace_opt # whitespace_opt endregion pp-message
```

区域不附加任何语义含义；区域 intended for use by the programmer or by automated tools to mark a section of source code。`#region` 或 `#endregion` 指令中指定的消息同样没有任何语义含义；它仅用于标识该区域。匹配的 `#region` 和 `#endregion` 指令可能具有不同的 `pp-message`。

区域的词法处理：

```
#region
...
#endregion
```

与以下形式的条件编译指令的词法处理完全对应：

```
#if true
#endif
```




#### 7.5.8 行指令

行指令可用于更改编译器在警告和错误等输出中报告的行号和源文件名。这些值也由调用方信息特性（§22.5.5）使用。

> [注意：行指令最常用于从其他文本输入生成 C# 源代码的元编程工具中。注意结束]

```
pp-line::
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line

line-indicator::
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden

file-name::
    " file-name-characters "

file-name-characters::
    file-name-character
    file-name-character file-name-character

file-name-character::
    Any input-character except " (U+0022), and new-line-character
```

当不存在任何 #line 指令时，编译器在其输出中报告真实的行号和源文件名。当处理包含非 default 的 line-indicator 的 #line 指令时，编译器将该指令之后的行视为具有给定的行号（以及文件名，如果指定了的话）。

`#line default` 指令会撤销所有前面的 `#line` 指令的效果。编译器为后续行报告真实的行信息，完全就像未处理过任何 `#line` 指令一样。

`#line hidden` 指令对错误消息中报告的文件和行号，或通过使用 `CallerLineNumberAttribute`（§22.5.2）产生的文件和行号没有影响。它旨在影响源级调试工具，使得在调试时，`#line hidden` 指令与后续 `#line` 指令（不是 `#line hidden`）之间的所有行都没有行号信息，并且在单步执行代码时被完全跳过。

> [注意：注意，file-name 与常规字符串字面量的不同之处在于不处理转义字符；`'\'` 字符在 file-name 中仅表示普通的反斜杠字符。注意结束]

#### 7.5.9 pragma 指令

`#pragma` 预处理指令用于向编译器指定上下文信息。[注意：例如，编译器可能提供 #pragma 指令，这些指令

- 在编译后续代码时启用或禁用特定的警告消息。
- 指定要应用于后续代码的优化。
- 指定供调试器使用的信息。

```
pp-pragma::
    whitespace_opt # whitespace_opt pragma pp-pragma-text

pp-pragma-text::
    new-line
    whitespace input-characters_opt new-line
```

*pp-pragma-text* 中的 *input-characters* 由编译器以实现定义的方式解释。`#pragma` 指令中提供的信息不得改变程序语义。`#pragma` 指令只应改变超出本语言规范范围的编译器行为。如果编译器无法解释 *input-characters*，编译器可以生成警告；但是，它不得产生编译时错误。

[注意：*pp-pragma-text* 可以包含任意文本；具体而言，它不需要包含格式良好的标记。*注意结束*]

## 8. 基本概念

### 8.1 应用程序启动

程序可以编译为*类库*，以用作其他应用程序的一部分；也可以编译为可直接启动的*应用程序*。确定此编译模式的机制是特定于实现的，并且不在本规范范围内。

编译为应用程序的程序应至少包含一个符合入口点条件的方法，该方法满足以下要求：

- 它应具有名称 `Main`。
- 它应为静态的。
- 它不应是泛型的。
- 它应声明在非泛型类型中。如果声明该方法的类型是嵌套类型，则其任何封闭类型都不能是泛型类型。
- 它不应具有 `async` 修饰符。
- 返回类型应为 void 或 int。
- 它不应是没有实现的分部方法（§15.6.9）。
- 形参列表应为空，或具有一个类型为 `string[]` 的值参数。

如果在一个程序中声明了多个符合入口点条件的方法，则可以使用外部机制来指定哪个方法被视为应用程序的实际入口点。如果程序编译为应用程序时没有恰好一个入口点，则这是编译时错误。编译为类库的程序可以包含符合应用程序入口点条件的方法，但生成的库没有入口点。

通常，方法的声明可访问性（§8.5.2）由其声明中指定的访问修饰符（§15.3.6）确定；类似地，类型的声明可访问性由其声明中指定的访问修饰符确定。为了使给定类型的给定方法可调用，该类型和该成员都应可访问。然而，应用程序入口点是特殊情况。具体而言，执行环境可以访问应用程序的入口点，而不管其声明的可访问性如何，也不管其封闭类型声明的声明可访问性如何。

当应用程序运行时，会创建一个新的*应用程序域*。同一台机器上可以同时存在一个应用程序的多个不同实例化，并且每个实例化都有自己的应用程序域。应用程序域通过充当应用程序状态的容器来实现应用程序隔离。应用程序域充当应用程序中定义的类型及其使用的类库的容器和边界。加载到一个应用程序域中的类型与加载到另一个应用程序域中的相同类型不同，并且对象实例不会在应用程序域之间直接共享。例如，每个应用程序域都有这些类型的静态变量的自己的副本，并且类型的静态构造函数在每个应用程序域中最多运行一次。实现可以自由地提供特定于实现的策略或机制来创建和销毁应用程序域。

应用程序启动发生在执行环境调用应用程序的入口点时。如果入口点声明了参数，则在应用程序启动期间，实现应确保参数的初始值是指向字符串数组的非 null 引用。此数组应由指向字符串的非 null 引用组成，这些字符串称为应用程序参数，由宿主环境在应用程序启动之前赋予实现定义的值。其意图是向应用程序提供在应用程序启动之前从宿主环境中的其他地方确定的信息。[注意：在支持命令行的系统上，应用程序参数对应于通常所称的命令行参数。[注意：... 注意结束]

如果入口点的返回类型是 int 而不是 void，则执行环境调用该方法所得到的返回值用于应用程序终止（§8.2）。

除上述情况外，入口点方法在各方面都与非入口点方法的行为相同。特别地，如果在应用程序生存期内的任何其他时间点调用入口点（例如通过常规方法调用），则不会对该方法进行特殊处理：如果有参数，其初始值可以为 null，也可以是指向包含 null 引用的数组的非 null 值。同样，入口点的返回值除了在执行环境调用时之外没有特殊意义。

### 8.2 应用程序终止

应用程序终止会将控制权返回给执行环境。

如果应用程序入口点方法的返回类型是 int，则返回的值用作应用程序的终止状态代码。此代码的用途是允许向执行环境传达成功或失败。

如果入口点方法的返回类型是 void，则到达终止该方法的右大括号（}），或执行不带表达式的 return 语句，会得到终止状态代码 0。如果入口点方法因异常（§21.4）而终止，则退出代码是特定于实现的。此外，实现可以提供用于指定退出代码的替代 API。

在应用程序终止之前，实现应尽一切合理努力调用其所有尚未被垃圾回收的对象的终结器（§15.13），除非此类清理已被抑制（例如，通过调用库方法 `GC.SuppressFinalize`）。实现应记录无法保证此行为的任何条件。

### 8.3 声明

C# 程序中的声明定义程序的构成元素。C# 程序使用命名空间进行组织。命名空间通过命名空间声明（§14）引入，其中可以包含类型声明和嵌套命名空间声明。类型声明（§14.7）用于定义类（§15）、结构（§16）、接口（§18）、枚举（§19）和委托（§20）。类型声明中允许的成员种类取决于类型声明的形式。例如，类声明可以包含常量（§15.4）、字段（§15.5）、方法（§15.6）、属性（§15.7）、事件（§15.8）、索引器（§15.9）、运算符（§15.10）、实例构造函数（§15.11）、静态构造函数（§15.12）、终结器（§15.13）和嵌套类型（§15.3.9）的声明。

声明在其所属的声明空间中定义一个名称。在一个声明空间中，如果两个或多个声明引入具有相同名称的成员，则这是编译时错误，但以下情况除外：

- 同一声明空间中允许有两个或多个同名命名空间声明。此类命名空间声明会聚合形成单个逻辑命名空间，并共享单个声明空间。
- 不同程序中但位于同一命名空间声明空间中的声明允许共享同一名称。[注意：但是，如果将这些声明包含在同一应用程序中，它们可能会引入歧义。注意结束]
- 同一声明空间中允许有两个或多个同名但签名不同的方法（§8.6）。
- 同一声明空间中允许有两个或多个同名但类型参数数量不同的类型声明（§8.8.2）。




- 同一声明空间中带 `partial` 修饰符的两个或更多类型声明可以共享相同名称、相同数量的类型参数和相同分类（`class`、`struct` 或 `interface`）。在此情况下，这些类型声明贡献给单一类型，并且它们自身聚合以形成单一声明空间（§15.2.7）。
- 同一声明空间中的命名空间声明和类型声明可以共享相同名称，只要该类型声明至少有一个类型参数（§8.8.2）。

声明空间有若干不同类型，如下所述。

- 在程序的所有*源文件*中，不带外围*命名空间声明*的*命名空间成员声明*是名为**全局声明空间**的单一组合声明空间的成员。
- 在程序的所有*源文件*中，位于具有相同完全限定命名空间名称的*命名空间声明*内的*命名空间成员声明*是单一组合声明空间的成员。
- 每个*编译单元*和*命名空间体*都有一个**别名声明空间**。*编译单元*或*命名空间体*的每个*外部别名指令*和 *using 别名指令*都会向该别名声明空间贡献一个成员（§14.5.2）。
- 每个非分部类、结构或接口声明都会创建一个新声明空间。每个分部类、结构或接口声明都贡献给同一程序中所有匹配部分共享的声明空间（§16.2.3）。名称通过*类成员声明*、*结构成员声明*、*接口成员声明*或*类型参数*引入此声明空间。除重载的实例构造函数声明和静态构造函数声明外，类或结构不能包含与类或结构同名的成员声明。类、结构或接口允许声明重载的方法和索引器。此外，类或结构允许声明重载的实例构造函数和运算符。例如，类、结构或接口可以包含多个同名方法声明，前提是这些方法声明的签名不同（§8.6）。注意，基类不贡献给类的声明空间，基接口不贡献给接口的声明空间。因此，派生类或接口允许声明与继承成员同名的成员。这样的成员称为*隐藏*继承成员。
- 每个委托声明都会创建一个新声明空间。名称通过形参（*固定参数*和*参数数组*）和*类型参数*引入此声明空间。
- 每个枚举声明都会创建一个新声明空间。名称通过*枚举成员声明*引入此声明空间。
- 每个方法声明、属性声明、属性访问器声明、索引器声明、索引器访问器声明、运算符声明、实例构造函数声明和匿名函数都会创建一个称为**局部变量声明空间**的新声明空间。名称通过形参（*固定参数*和*参数数组*）和*类型参数*引入此声明空间。属性或索引器的 `set` 访问器将 `value` 名称作为形参引入。函数成员或匿名函数的主体（如果有）被视为嵌套在局部变量声明空间内。局部变量声明空间和嵌套的局部变量声明空间包含同名元素是错误的。因此，在嵌套声明空间内，不可能声明与外围声明空间中的局部变量或常量同名的局部变量或常量。两个声明空间可以包含同名元素，只要任一声明空间都不包含另一个。
- 每个*块*或*switch 块*，以及 *for*、*foreach* 和 *using* 语句，都会为局部变量和局部常量创建局部变量声明空间。名称通过*局部变量声明*和*局部常量声明*引入此声明空间。注意，作为函数成员或匿名函数的主体出现或位于其内的块，嵌套在这些函数为其参数所声明的局部变量声明空间内。因此，例如，方法中的局部变量与参数同名是错误的。
- 每个*块*或*switch 块*都会为标签创建一个单独的声明空间。名称通过*带标签语句*引入此声明空间，并通过 *goto 语句*引用这些名称。块的*标签声明空间*包括任何嵌套块。因此，在嵌套块内不可能声明与外围块中的标签同名的标签。

名称声明的文本顺序通常无关紧要。特别地，对于命名空间、常量、方法、属性、事件、索引器、运算符、实例构造函数、终结器、静态构造函数和类型的声明与使用，文本顺序无关紧要。声明顺序在以下方面很重要：

- 字段声明的声明顺序决定其初始化器（如果有）的执行顺序（§15.5.6.2、§15.5.6.3）。
- 局部变量应在使用之前定义（§8.7）。
- 当省略*常量表达式*值时，枚举成员声明（§19.4）的声明顺序很重要。

[示例：命名空间的声明空间是“开放式的”，具有相同完全限定名称的两个命名空间声明贡献给同一声明空间。例如

```
namespace Megacorp.Data
{
    class Customer
    {
        ...
    }
}

namespace Megacorp.Data
{
    class Order
    {
        ...
    }
}
```

上述两个命名空间声明贡献给同一声明空间，在此情况下声明了完全限定名称为 Megacorp.Data.Customer 和 Megacorp.Data.Order 的两个类。由于这两个声明贡献给同一声明空间，如果各自包含同名类的声明，就会导致编译时错误。示例结束]

[注意：如上所述，块的声明空间包括任何嵌套块。因此，在以下示例中，F 和 G 方法会导致编译时错误，因为名称 i 在外层块中声明，不能在内部块中重新声明。但是，H 和 I 方法是有效的，因为两个 i 分别声明在独立的非嵌套块中。

```
class A
{
    void F() {
        int i = 0;
        if (true) {
            int i = 1;
        }
    }

    void G() {
        if (true) {
            int i = 0;
        }
        int i = 1;
    }

    void H() {
        if (true) {
            int i = 0;
        }
        if (true) {
            int i = 1;
        }
    }

    void I() {
        for (int i = 0; i < 10; i++)
            H();
        for (int i = 0; i < 10; i++)
            H();
    }
}
```

注意结束]

## 8.4 成员

### 8.4.1 概述

命名空间和类型具有*成员*。[注意：实体的成员通常可通过使用限定名来访问，该限定名以对实体的引用开头，后跟“.”标记，再跟成员名称。注意结束]

类型的成员要么在类型声明中声明，要么从该类型的基类*继承*。当类型从基类继承时，基类的所有成员（实例构造函数、终结器和静态构造函数除外）都成为派生类型的成员。基类成员声明的可访问性不控制该成员是否被继承——继承扩展到任何不是实例构造函数、静态构造函数或终结器的成员。[注意：但是，继承成员在派生类型中可能不可访问，例如由于其声明的可访问性（§8.5.2）。注意结束]

### 8.4.2 命名空间成员

没有外围命名空间的命名空间和类型是*全局命名空间*的成员。这直接对应于全局声明空间中声明的名称。

在命名空间内声明的命名空间和类型是该命名空间的成员。这直接对应于该命名空间的声明空间中声明的名称。

命名空间没有访问限制。不可能声明私有、受保护或内部命名空间，并且命名空间名称始终可公开访问。

### 8.4.3 结构成员

结构的成员是在结构中声明的成员，以及从该结构的直接基类 System.ValueType 和间接基类 object 继承的成员。

简单类型的成员直接对应于该简单类型所别名的结构类型的成员（§9.3.5）。

### 8.4.4 枚举成员

枚举的成员是在枚举中声明的常量，以及从该枚举的直接基类 System.Enum 和间接基类 System.ValueType 和 object 继承的成员。

### 8.4.5 类成员

类的成员是在类中声明的成员以及从基类继承的成员（类 object 除外，它没有基类）。从基类继承的成员包括基类的常量、字段、方法、属性、事件、索引器、运算符和类型，但不包括



根据成员声明发生的上下文，只允许某些类型的声明可访问性。此外，当成员声明不包含任何访问修饰符时，声明发生的上下文决定默认声明的可访问性。

- 命名空间隐式具有公共声明可访问性。不允许在命名空间声明上使用访问修饰符。
- 直接在编译单元或命名空间中声明的类型（与在其他类型内部相对）可以具有公共或内部声明可访问性，并默认为内部声明可访问性。
- 类成员可以具有五种声明可访问性中的任何一种，并默认为私有声明可访问性。 [Note: 作为类的成员声明的类型可以具有五种声明可访问性中的任何一种，而作为命名空间的成员声明的类型只能具有公共或内部声明可访问性。 end note]
- 结构体成员可以具有公共、内部或私有声明可访问性，并由于结构体是隐式密封的而默认为私有声明可访问性。在结构体中引入的结构体成员（即该结构体未继承的成员）不能具有 protected 或 protected internal 声明可访问性。 [Note: 作为结构体的成员声明的类型可以具有公共、内部或私有声明可访问性，而作为命名空间的成员声明的类型只能具有公共或内部声明可访问性。 end note]
- 接口成员隐式具有公共声明可访问性。不允许在接口成员声明上使用访问修饰符。
- 枚举成员隐式具有公共声明可访问性。不允许在枚举成员声明上使用访问修饰符。

## 8.5.3 可访问性域

成员的可访问性域由允许访问该成员的（可能不相交的）程序文本部分组成。为了定义成员的可访问性域，如果成员未在类型内声明，则称其为顶层成员；如果成员在另一个类型内声明，则称其为嵌套成员。此外，程序的程序文本定义为程序所有源文件中包含的所有程序文本，而类型的程序文本定义为该类型类型声明中包含的所有程序文本（可能包括嵌套在该类型内的类型）。

预定义类型（如 object、int 或 double）的可访问性域是无限的。

在程序 P 中声明的顶层非绑定类型 T（§9.4.4）的可访问性域定义如下：

- 如果 T 的声明可访问性为 public，则 T 的可访问性域为 P 的程序文本以及引用 P 的任何程序。
- 如果 T 的声明可访问性为 internal，则 T 的可访问性域为 P 的程序文本。

[Note: 由这些定义可知，顶层非绑定类型的可访问性域始终至少为声明该类型的程序的程序文本。 end note]

构造类型 T<A1, ..., An> 的可访问性域是未绑定泛型类型 T 的可访问性域与类型参数 A1, ..., An 的可访问性域的交集。

在程序 P 内的类型 T 中声明的嵌套成员 M 的可访问性域定义如下（注意 M 本身可能是一个类型）：

- 如果 M 的声明可访问性为 public，则 M 的可访问性域为 T 的可访问性域。
- 如果 M 的声明可访问性为 protected internal，则令 D 为 P 的程序文本与在 P 外声明的从 T 派生的任何类型的程序文本的并集。M 的可访问性域为 T 的可访问性域与 D 的交集。
- 如果 M 的声明可访问性为 protected，则令 D 为 T 的程序文本与从 T 派生的任何类型的程序文本的并集。M 的可访问性域为 T 的可访问性域与 D 的交集。
- 如果 M 的声明可访问性为 internal，则 M 的可访问性域为 T 的可访问性域与 P 的程序文本的交集。
- 如果 M 的声明可访问性为 private，则 M 的可访问性域为 T 的程序文本。

> [Note: 由这些定义可知，嵌套成员的可访问性域始终至少为声明该成员的类型的程序文本。此外，可知成员的可访问性域永远不会比声明该成员的类型的可访问性域更宽泛。 end note]

> [Note: 直观地说，当访问类型或成员 M 时，会评估以下步骤以确保允许访问：
> - 首先，如果 M 在类型内声明（而不是编译单元或命名空间），如果该类型不可访问，则会发生编译时错误。
> - 然后，如果 M 为 public，则允许访问。
> - 否则，如果 M 为 protected internal，则如果访问发生在声明 M 的程序内，或如果访问发生在从声明 M 的类派生的类内并且通过派生类类型进行（§8.5.4），则允许访问。
> - 否则，如果 M 为 protected，则如果访问发生在声明 M 的类内，或如果访问发生在从声明 M 的类派生的类内并且通过派生类类型进行（§8.5.4），则允许访问。
> - 否则，如果 M 为 internal，则如果访问发生在声明 M 的程序内，则允许访问。
> - 否则，如果 M 为 private，则如果访问发生在声明 M 的类型内，则允许访问。
> - 否则，类型或成员不可访问，并发生编译时错误。
> end note]

[Example: 以下代码中

```
public class A
{
    public static int X;
    internal static int Y;
    private static int Z;
}

internal class B
{
    public static int X;
    internal static int Y;
    private static int Z;
    public class C
    {
        public static int X;
        internal static int Y;
        private static int Z;
    }

    private class D
    {
        public static int X;
        internal static int Y;
        private static int Z;
    }
}
```

类和成员具有以下可访问性域：

- A 和 A.X 的可访问性域是无限的。
- A.Y、B.X、B.Y、B.C、B.C.X 和 B.C.Y 的可访问性域为包含程序的程序文本。
- A.Z 的可访问性域为 A 的程序文本。
- B.Z 和 B.D 的可访问性域为 B 的程序文本，包括 B.C 和 B.D 的程序文本。
- B.C.Z 的可访问性域为 B.C 的程序文本。
- B.D.X 和 B.D.Y 的可访问性域为 B 的程序文本，包括 B.C 和 B.D 的程序文本。
- B.D.Z 的可访问性域为 B.D 的程序文本。

正如示例所示，成员的可访问性域永远不会大于包含类型的可访问性域。例如，尽管所有 X 成员都具有 public 声明可访问性，但除 A.X 外，其余的都具有受包含类型约束的可访问性域。 end example]

如 §8.4 中所述，除了实例构造函数、终结器和静态构造函数之外，基类的所有成员都由派生类型继承。这甚至包括基类的私有成员。然而，私有成员的可访问性域仅包括声明该成员的类型的程序文本。 [Example: 以下代码中

```
class A
{
    int x;
    static void F(B b) {
        b.x = 1;    // ok
    }
}

class B: A
{
    static void F(B b) {
        b.x = 1;    // Error, x not accessible
    }
}
```

B 类从 A 类继承私有成员 x。由于该成员为私有，因此它只能在 A 的类体内部访问。因此，对 b.x 的访问在 A.F 方法中成功，但在 B.F 方法中失败。 end example]

## 8.5.4 受保护访问

当在声明它的类的程序文本之外访问受保护的实例成员时，以及当在声明它的程序的程序文本之外访问受保护内部的实例成员时，访问必须在从声明它的类派生的类声明内进行。此外，访问必须通过该派生类类型的一个实例或从其构造的类类型进行。此限制防止一个派生类访问其他派生类的受保护成员，即使这些成员是从同一个基类继承的。

设 B 为声明受保护实例成员 M 的基类，设 D 为从 B 派生的类。在 D 的类体内，对 M 的访问可以采用以下形式之一：

- 无限定类型名或形式为 M 的主表达式。
- 形式为 E.M 的主表达式，前提是 E 的类型为 T 或从 T 派生的类，其中 T 为类 D，或从 D 构造的类类型。
- 形式为 base.M 的主表达式。

除了这些访问形式外，派生类还可以在构造函数初始值设定项中访问基类的受保护实例构造函数（§15.11.2）。

[Example: 以下代码中

```



```
public class A
{
    protected int x;
    static void F(A a, B b) {
        a.x = 1;    // Ok
        b.x = 1;    // Ok
    }
}
public class B: A
{
    static void F(A a, B b) {
        a.x = 1;    // Error, must access through instance of B
        b.x = 1;    // Ok
    }
}
```

在 A 内，可以通过 A 和 B 两者的实例访问 x，因为无论哪种情况，访问都通过 A 的实例或从 A 派生的类的实例进行。然而，在 B 内，不能通过 A 的实例访问 x，因为 A 不派生自 B。示例结束]

[示例：

```
class C<T>
{
    protected T x;
}
class D<T>: C<T>
{
    static void F() {
        D<T> dt = new D<T>();
        D<int> di = new D<int>();
        D<string> ds = new D<string>();
        dt.x = default(T);
        di.x = 123;
        ds.x = "test";
    }
}
```

这里，对 x 的三次赋值都是允许的，因为它们都通过由该泛型类型构造的类类型的实例进行。示例结束]

[注意：在泛型类中声明的受保护成员的可访问域（§8.5.3）包括从该泛型类构造的任何类型派生的所有类声明的程序文本。在示例中：

```
class C<T>
{
    protected static T x;
}
class D: C<string>
{
    static void Main() {
        C<int>.x = 5;
    }
}
```

在 D 中对受保护成员 C<int>.x 的引用是有效的，即使类 D 派生自 C<string>。注意结束]

## 8.5.5 可访问性约束

C# 语言中的若干构造要求某个类型至少与某个成员或另一个类型一样可访问。如果类型 T 的可访问域是成员或类型 M 的可访问域的超集，则称类型 T 至少与成员或类型 M 一样可访问。换言之，如果 T 在 M 可访问的所有上下文中都可访问，则 T 至少与 M 一样可访问。

存在以下可访问性约束：

- 类类型的直接基类应至少与该类类型本身一样可访问。
- 接口类型的显式基接口应至少与该接口类型本身一样可访问。
- 委托类型的返回类型和参数类型应至少与该委托类型本身一样可访问。
- 常量的类型应至少与该常量本身一样可访问。
- 字段的类型应至少与该字段本身一样可访问。
- 方法的返回类型和参数类型应至少与该方法本身一样可访问。
- 属性的类型应至少与该属性本身一样可访问。
- 事件的类型应至少与该事件本身一样可访问。
- 索引器的类型和参数类型应至少与该索引器本身一样可访问。
- 运算符的返回类型和参数类型应至少与该运算符本身一样可访问。
- 实例构造函数的参数类型应至少与该实例构造函数本身一样可访问。

[示例：在以下代码中
```
class A {...}
public class B: A {...}
```
B 类会导致编译时错误，因为 A 并不至少与 B 一样可访问。示例结束]

[示例：同样，在以下代码中
```
class A {...}
public class B
{
    A F() {...}
    internal A G() {...}
    public A H() {...}
}
```
B 中的 H 方法会导致编译时错误，因为返回类型 A 并不至少与该方法的可访问性相同。示例结束]

## 8.6 签名与重载

方法、实例构造函数、索引器和运算符由其签名来表征：

- 方法的签名由方法名称、类型参数数目，以及每个形参的类型和参数传递模式（值、引用或输出）组成，按从左到右的顺序考虑。为此，方法中出现在形参类型中的任何类型参数，不按其名称标识，而按其在方法类型参数列表中的序号位置标识。方法的签名具体不包括返回类型、参数名称、类型参数名称、类型参数约束、params 或 this 参数修饰符，也不包括参数是必需还是可选。
- 实例构造函数的签名由每个形参的类型和参数传递模式（值、引用或输出）组成，按从左到右的顺序考虑。该

```
void F<S,T>(S s);        // F<'0','1>('0)
void F<T,S>(S s);        // F<'0','1>('1)  ok
}
```

请注意，任何 ref 和 out 参数修饰符（§15.6.2）都是签名的一部分。因此，F(int)、F(ref int) 和 F(out int) 都是不同的签名。然而，F(ref int) 和 F(out int) 不能在同一接口中声明，因为它们的签名仅因 ref 和 out 而不同。另外，请注意返回类型和 params 修饰符不是签名的一部分，因此不可能仅根据返回类型或根据是否包含 params 修饰符来进行重载。因此，上面标识的方法 F(int) 和 F(params string[]) 的声明会导致编译时错误。示例结束

## 8.7 作用域

### 8.7.1 概述

名称的作用域是程序文本中的区域，在该区域内可以不限定名称而引用该名称所声明的实体。作用域可以嵌套，内层作用域可以重新声明外层作用域中某个名称的含义。（但这并不解除 §8.3 施加的限制：在嵌套块中，不能声明与封闭块中的局部变量或局部常量同名的局部变量或局部常量。）此时，外层作用域中的名称被称为在内层作用域所覆盖的程序文本区域中被隐藏，并且只有通过限定该名称才能访问外层名称。

- 由没有封闭命名空间声明的命名空间成员声明（§14.6）所声明的命名空间成员，其作用域是整个程序文本。
- 由命名空间声明内的命名空间成员声明所声明的命名空间成员，若该命名空间声明的完全限定名为 N，则其作用域是每个完全限定名为 N 或以 N 后跟一个句点开头的命名空间声明的命名空间体。
- 由 extern 别名指令（§14.4）定义的名称，其作用域覆盖该指令直接所在的编译单元或命名空间体中的 using 指令、全局特性和命名空间成员声明。extern 别名指令不会向基础声明空间贡献任何新成员。换言之，extern 别名指令不是传递性的，而只影响其所在的编译单元或命名空间体。
- 由 using 指令（§14.5）定义或导入的名称，其作用域覆盖该 using 指令所在的编译单元或命名空间体中的全局特性和命名空间成员声明。using 指令可使零个或多个命名空间或类型名称在特定编译单元或命名空间体内可用，但不会向基础声明空间贡献任何新成员。换言之，using 指令不是传递性的，而只影响其所在的编译单元或命名空间体。
- 由类声明（§15.2）上的类型参数列表所声明的类型参数，其作用域是该类声明的类基、类型参数约束子句和类体。[注意：与类的成员不同，此作用域不延伸到派生类。注意结束]
- 由结构声明（§16.2）上的类型参数列表所声明的类型参数，其作用域是该结构声明的结构接口、类型参数约束子句和结构体。
- 由接口声明（§18.2）上的类型参数列表所声明的类型参数，其作用域是该接口声明的接口基、类型参数约束子句和接口体。
- 由委托声明（§20.2）上的类型参数列表所声明的类型参数，其作用域是该委托声明的返回类型、形参列表和类型参数约束子句。
- 由方法声明（§15.6.1）上的类型参数列表所声明的类型参数，其作用域是该方法声明。




```csharp
void G() {
    int j = (j = 1);      // Valid
}
void H() {
    int a = 1, b = ++a;   // Valid
}
}
```

在上面的 F 方法中，对 i 的第一次赋值特指不引用在外部作用域中声明的字段。相反，它引用的是局部变量，并且由于它在文本上先于变量的声明，因此会导致编译时错误。在 G 方法中，j 在 j 的声明的初始化器中的使用是有效的，因为该使用不先于局部变量声明符。在 H 方法中，后续的局部变量声明符正确地引用了在同一局部变量声明中较早的局部变量声明符中声明的局部变量。end example]

[Note: 局部变量和局部常量的作用域规则旨在保证在块内在表达式上下文中使用的名称的含义始终相同。如果局部变量的作用域仅从其声明延伸到块的末尾，那么在上面的示例中，第一次赋值将赋值给实例变量，而第二次赋值将赋值给局部变量，如果稍后重新排列块的语句，可能会导致编译时错误。]

块内名称的含义可能因名称使用的上下文而异。在示例

```csharp
using System;
class A {}
class Test
{
    static void Main() {
        string A = "hello, world";
        string s = A;                  // expression context
        Type t = typeof(A);            // type context
        Console.WriteLine(s);          // writes "hello, world"
        Console.WriteLine(t);          // writes "A"
    }
}
```

名称 A 在表达式上下文中用于引用局部变量 A，而在类型上下文中用于引用类 A。end note]

## 8.7.2 名称隐藏

### 8.7.2.1 通用

实体的作用域通常涵盖的程序文本比实体的声明空间更多。特别是，实体的作用域可能包括引入包含同名实体的新声明空间的声明。此类声明会导致原始实体变得*隐藏*。相反，当实体未被隐藏时，称其为*可见*。

名称隐藏发生在作用域通过嵌套重叠以及作用域通过继承重叠时。两种隐藏类型的特征在以下小节中描述。

### 8.7.2.2 通过嵌套隐藏

通过嵌套的名称隐藏可能由于在命名空间内嵌套命名空间或类型、由于在类或结构中嵌套类型，以及由于参数、局部变量和局部常量声明而发生。[Example: 在以下代码

```csharp
class A
{
    int i = 0;
    void F() {
        int i = 1;
    }
    void G() {
        i = 1;
    }
}
```

在 F 方法内，实例变量 i 被局部变量 i 隐藏，但在 G 方法内，i 仍然引用实例变量。end example]

当内部作用域中的名称隐藏外部作用域中的名称时，它会隐藏该名称的所有重载出现。[Example: 在以下代码

```csharp
class Outer
{
    static void F(int i) {}
    static void F(string s) {}
    class Inner
    {
        static void F(long l) {}
        void G() {
            F(1);        // Invokes Outer.Inner.F
            F("Hello");  // Error
        }
    }
}
```

调用 F(1) 引发在 Inner 中声明的 F，因为所有外部出现的 F 都被内部声明隐藏。出于同样的原因，调用 F("Hello") 会导致编译时错误。end example]

### 8.7.2.3 通过继承隐藏

通过继承的名称隐藏发生在类或结构重新声明从基类继承的名称时。此种名称隐藏采用以下形式之一：

- 在类或结构中引入的常量、字段、属性、事件或类型会隐藏所有同名基类成员。
- 在类或结构中引入的方法会隐藏所有同名非方法基类成员，以及所有具有相同签名 (§8.6) 的基类方法。
- 在类或结构中引入的索引器会隐藏所有具有相同签名 (§8.6) 的基类索引器。

运算符声明的规则 (§15.10) 使派生类无法声明与基类中运算符具有相同签名的运算符。因此，运算符永远不会相互隐藏。

与从外部作用域隐藏名称相反，从继承作用域隐藏可见名称会导致报告警告。[Example: 在以下代码

```csharp
class Base
{
    public void F() {}
}

class Derived: Base
{
    public void F() {}    // warning, hiding an inherited name
}
```

Derived 中 F 的声明会导致报告警告。隐藏继承的名称 specifically 不是错误，因为那样会阻止基类的独立演进。例如，上述情况可能是因为 Base 的较新版本引入了 F 方法，而该方法在类的早期版本中不存在。end example]

- I
- I<A1, ..., Ak>
- N.I
- N.I<A1, ..., Ak>

其中 I 是一个标识符，N 是一个命名空间或类型名称，<A1, ..., Ak> 是一个可选的类型参数列表。当未指定类型参数列表时，将 K 视为零。

命名空间或类型名称的含义确定如下：

- 如果命名空间或类型名称是 qualified-alias-member，则其含义如 §14.8.1 中所述。
- 否则，如果命名空间或类型名称的形式为 I 或 I<A1, ..., Ak>：
  - 如果 K 为零且命名空间或类型名称出现在泛型方法声明 (§15.6) 内但在方法头的属性之外，并且该声明包含名称为 I 的类型参数 (§15.2.3)，则命名空间或类型名称引用该类型参数。
  - 否则，如果命名空间或类型名称出现在类型声明内，则对于每个实例类型 T (§15.3.2)，从该类型声明的实例类型开始，继续每个封闭的类或结构声明（如果有）的实例类型：
    - 如果 K 为零且 T 的声明包含名称为 I 的类型参数，则命名空间或类型名称引用该类型参数。
  - 否则，如果命名空间或类型名称出现在类型声明的主体中，并且 T 或其任何基类型包含具有名称 I 和 K 个类型参数的嵌套可访问类型，则命名空间或类型名称引用使用给定类型参数构造的该类型。如果存在多个此类类型，则选择在更派生的类型中声明的类型。[Note: 在确定命名空间或类型名称的含义时，非类型成员（常量、字段、方法、属性、索引器、运算符、实例构造函数、终结器和静态构造函数）以及类型参数数量不同的类型成员将被忽略。end note]
  - 否则，对于每个命名空间 N，从命名空间或类型名称出现的命名空间开始，继续每个封闭的命名空间（如果有），并以全局命名空间结束，以下步骤将被评估直到找到一个实体：
    - 如果 K 为零且 I 是 N 中的命名空间的名称，则：
      - 如果命名空间或类型名称出现的位置被 N 的命名空间声明所包含，并且命名空间声明包含将名称 I 与命名空间或类型关联的 extern-alias-directive 或 using-alias-directive，则命名空间或类型名称是不明确的，并且会发生编译时错误。
      - 否则，命名空间或类型名称引用 N 中名为 I 的命名空间。
    - 否则，如果 N 包含具有名称 I 和 K 个类型参数的可访问类型，则：
      - 如果 K 为零且命名空间或类型名称出现的位置被 N 的命名空间声明所包含，并且命名空间声明包含将名称 I 与命名空间或类型关联的 extern-alias-directive 或 using-alias-directive，则命名空间或类型名称是不明确的，并且会发生编译时错误。
      - 否则，命名空间或类型名称引用使用给定类型参数构造的类型。
  - 否则，如果命名空间或类型名称出现的位置被 N 的命名空间声明所包含：

- 如果 K 为零，且命名空间声明包含将名称 I 与导入的命名空间或类型关联的 *外部别名指令* 或 *using 别名指令*，则该 *命名空间或类型名称* 引用该命名空间或类型。
- 否则，如果该命名空间声明的 *using 命名空间指令* 所导入的命名空间中恰好包含一个名称为 I 且具有 K 个类型参数的类型，则该 *命名空间或类型名称* 引用使用给定类型参数构造的类型。
- 否则，如果该命名空间声明的 *using 命名空间指令* 所导入的命名空间中包含多个名称为 I 且具有 K 个类型参数的类型，则该 *命名空间或类型名称* 存在歧义，并发生错误。
- 否则，该 *命名空间或类型名称* 未定义，并发生编译时错误。

否则，该 *命名空间或类型名称* 的形式为 N.I 或 N.I<A1, ..., Ak>。首先将 N 解析为 *命名空间或类型名称*。如果 N 的解析不成功，则发生编译时错误。否则，按如下方式解析 N.I 或 N.I<A1, ..., Ak>：

- 如果 K 为零，N 引用命名空间，并且 N 包含名称为 I 的嵌套命名空间，则该 *命名空间或类型名称* 引用该嵌套命名空间。
- 否则，如果 N 引用命名空间，并且 N 包含名称为 I 且具有 K 个类型参数的可访问类型，则该 *命名空间或类型名称* 引用使用给定类型参数构造的类型。
- 否则，如果 N 引用（可能是构造的）类或结构类型，并且 N 或其任何基类包含名称为 I 且具有 K 个类型参数的可访问嵌套类型，则该 *命名空间或类型名称* 引用使用给定类型参数构造的类型。如果存在多个此类类型，则选择在派生程度更高的类型中声明的类型。[注意：如果 N.I 的含义是在解析 N 的基类规范时确定的，则 N 的直接基类视为 object（§15.2.4.2）。注记结束]
- 否则，N.I 是无效的 *命名空间或类型名称*，并发生编译时错误。

*命名空间或类型名称* 仅允许引用静态类（§15.2.2.4），前提是：

- 该 *命名空间或类型名称* 是形式为 T.I 的 *命名空间或类型名称* 中的 T，或
- 该 *命名空间或类型名称* 是形式为 typeof(T) 的 *typeof 表达式*（§12.7.12）中的 T

### 8.8.2 非限定名称

每个命名空间声明和类型声明都有一个 *非限定名称*，其确定方式如下：

- 对于命名空间声明，非限定名称是声明中指定的 *限定标识符*。
- 对于没有 *类型参数列表* 的类型声明，非限定名称是声明中指定的 *标识符*。
- 对于具有 K 个类型参数的类型声明，非限定名称是声明中指定的 *标识符*，后跟 K 个类型参数的 *泛型维度说明符*（§12.7.12）。

### 8.8.3 完全限定名称

每个命名空间和类型声明都有一个 *完全限定名称*，它在程序中的所有其他声明中唯一标识该命名空间或类型声明。具有非限定名称 N 的命名空间或类型声明的完全限定名按如下方式确定：

- 如果 N 是全局命名空间的成员，则其完全限定名为 N。
- 否则，其完全限定名为 S.N，其中 S 是在其中声明 N 的命名空间或类型声明的完全限定名。

换句话说，N 的完全限定名是自全局命名空间开始，通向 N 的标识符和泛型维度说明符的完整层次路径。由于命名空间或类型的每个成员都应具有唯一名称，因此命名空间或类型声明的完全限定名始终是唯一的。同一完全限定名引用两个不同的实体是编译时错误。具体而言：

- 命名空间声明和类型声明具有相同的完全限定名是错误的。
- 两种不同种类的类型声明具有相同的完全限定名是错误的（例如，结构和类声明具有相同的完全限定名）。
- 没有 partial 修饰符的类型声明与另一个类型声明具有相同的完全限定名是错误的（§15.2.7）。

[示例：下面的示例展示了几个命名空间和类型声明及其关联的完全限定名。

```
class A {}                  // A
namespace X                 // X
{
    class B                 // X.B
    {
        class C {}          // X.B.C
    }
    namespace Y             // X.Y
    {
        class D {}          // X.Y.D
    }
}
namespace X.Y               // X.Y
{
    class E {}              // X.Y.E
    class G<T> {            // X.Y.G<>
        class H {}          // X.Y.G<>.H
    }
    class G<S,T> {          // X.Y.G<,>
        class H<U> {}       // X.Y.G<,>.H<>
    }
}
```

示例结束]

## 8.9 自动内存管理

C# 采用自动内存管理，使开发人员无需手动分配和释放对象所占用的内存。自动内存管理策略由垃圾回收器实现。对象的内存管理生命周期如下：

- 1. 创建对象时，为其分配内存，运行构造函数，并认为该对象为活动状态。
- 2. 如果对象或其任何实例字段都无法通过任何可能的执行延续（终结器的运行除外）来访问，则认为该对象不再使用，并有资格进行终结。[注意：C# 编译器和垃圾回收器可能会选择分析代码，以确定将来可能使用对象的哪些引用。例如，如果作用域内的局部变量是对象的唯一现有引用，但在过程当前执行点之后的任何可能的执行延续中都从未引用该局部变量，则垃圾回收器可以（但并非必须）将该对象视为不再使用。注记结束]
- 3. 一旦对象有资格进行终结，在稍后的某个未指定时间，将运行该对象的终结器（§15.13）（如果有）。在正常情况下，对象的终结器只运行一次，但实现特定的 API 可能允许覆盖此行为。
- 4. 一旦对象的终结器运行，如果对象或其任何实例字段都无法通过任何可能的执行延续（包括终结器的运行）来访问，则认为该对象 *不可访问*，并有资格进行回收。[*注意：以前无法访问的对象可能会因终结器而再次变得可访问。下面提供了一个示例。注记结束*]
- 5. 最后，在对象有资格进行回收后的某个时间，垃圾回收器释放与该对象关联的内存。

垃圾回收器维护有关对象使用情况的信息，并利用这些信息做出内存管理决策，例如在内存中的哪个位置放置新创建的对象、何时重定位对象，以及对象何时不再使用或不可访问。

与其他假定存在垃圾回收器的语言一样，C# 的设计使垃圾回收器可以实现广泛的内存管理策略。C# 要求终结器在对象有资格被回收之时到应用程序退出之间 的某个时间运行，但既未指定该时间段内的时间限制，也未指定终结器的运行顺序。

垃圾回收器的行为可以在一定程度上通过 System.GC 类的静态方法进行控制。此类可用于请求执行回收、运行（或不运行）终结器等。

[示例：由于垃圾回收器在决定何时回收对象和运行终结器方面被赋予了很大的自由度，因此符合规范的实现产生的输出可能与以下代码所示不同。程序

```
using System;
class A
{
  ~A() {
    Console.WriteLine("Finalize instance of A");
  }
}
class B
{
  object Ref;
  public B(object o) {
    Ref = o;
  }
  ~B() {
    Console.WriteLine("Finalize instance of B");
  }
}
class Test
{
  static void Main() {
    B b = new B(new A());
    b = null;
    GC.Collect();
    GC.WaitForPendingFinalizers();
  }
}
```

创建了类 A 的一个实例和类 B 的一个实例。当变量 b 被赋值为 null 后，这些对象便有资格进行垃圾回收，因为在此之后，任何用户编写的代码都无法再访问它们。输出可能是

终结 A 的实例
终结 B 的实例

或

终结 B 的实例
终结 A 的实例

因为语言对对象被垃圾回收的顺序不施加任何限制。

在微妙的情况下，“可终结”和“可回收”之间的区别可能很重要。例如，

```
using System;
class A
{
    ~A() {
        Console.WriteLine("Finalize instance of A");
    }
    public void F() {
        Console.WriteLine("A.F");
        Test.RefA = this;
    }
}
class B
{
    public A Ref;
    ~B() {
        Console.WriteLine("Finalize instance of B");
        Ref.F();
    }
}
class Test
{
    public static A RefA;
    public static B RefB;
    static void Main() {
        RefB = new B();
        RefA = new A();
        RefB.Ref = RefA;
        RefB = null;
        RefA = null;

        // A and B now eligible for finalization
        GC.Collect();
        GC.WaitForPendingFinalizers();
        // B now eligible for collection, but A is not
        if (RefA != null)
            Console.WriteLine("RefA is not null");
    }
}
```

在上面的程序中，如果垃圾收集器选择先运行 A 的终结器再运行 B 的终结器，则该程序的输出可能是：

Finalize instance of A
Finalize instance of B
A.F
RefA is not null

请注意，尽管 A 的实例未被使用并且 A 的终结器已运行，但 A 的方法（在本例中为 F）仍可能从另一个终结器中被调用。此外，请注意，终结器的运行可能会导致对象再次从主程序中可用。在本例中，B 的终结器的运行导致之前未被使用的 A 的实例通过活动引用 Test.RefA 变得可访问。在调用 WaitForPendingFinalizers 之后，B 的实例可供回收，但 A 的实例不可回收，因为存在引用 Test.RefA。 end example

## 8.10 执行顺序

执行 C# 程序的方式使得每个执行线程的副作用在关键执行点得以保留。**副作用**定义为对易失字段的读取或写入、对非易失变量的写入、对外部资源的写入以及异常的抛出。应保留这些副作用顺序的关键执行点是对易失字段的引用 (§15.5.4)、lock 语句 (§13.13) 以及线程的创建和终止。执行环境可以更改 C# 程序的执行顺序，但须遵守以下约束：

- 数据依赖在执行线程内得以保留。也就是说，每个变量的值是按所有语句似乎按原始程序顺序执行来计算的。
- 初始化排序规则得以保留 (§15.5.5, §15.5.6)。
- 相对于易失性读取和写入，副作用的排序得以保留 (§15.5.4)。

此外，执行环境无需评估表达式的一部分，如果它能推断出该表达式的值未被使用且未产生所需的副作用（包括通过调用方法或访问易失字段引起的副作用）。当程序执行被异步事件中断时（如另一个线程抛出的异常），不能保证可观察到的副作用以原始程序顺序可见。

## 9 类型

### 9.1 通用

C# 语言的类型分为两个主要类别：引用类型和值类型。值类型和引用类型都可能是泛型类型，它们接受一个或多个类型参数。类型参数可以指定值类型和引用类型。

+   type:
+     reference-type
+     value-type
+     type-parameter

第三类类型指针仅在不安全代码中可用 (§23.3)。

值类型与引用类型的区别在于值类型的变量直接包含其数据，而引用类型的变量存储对其数据的引用，后者称为对象。使用引用类型时，两个变量可能引用同一个对象，因此对一个变量的操作可能会影响另一个变量引用的对象。使用值类型时，每个变量都有自己数据的副本，不可能对一个变量的操作影响另一个变量。 [Note: 当变量是 ref 或 out 参数时，它没有自己的存储，而是引用另一个变量的存储。在这种情况下，ref 或 out 变量有效地是另一个变量的别名，而不是一个不同的变量。 end note]

C# 的类型系统是统一的，使得任何类型的值都可以被视为对象。C# 中的每个类型直接或间接派生自 object 类类型，且 object 是所有类型的终极基类。引用类型的值通过将值视为 object 类型来简单地被视为对象。值类型的值通过执行装箱和拆箱操作 (§9.3.12) 被视为对象。

### 9.2 引用类型

### 9.2.1 通用

引用类型是类类型、接口类型、数组类型、委托类型或 dynamic 类型。

+   reference-type:
+     class-type
+     interface-type
+     array-type
+     delegate-type
+     dynamic

+   class-type:
+     type-name
+     object
+     string

+   interface-type:
+     type-name

+   array-type:
+     non-array-type rank-specifiers

```
non-array-type:
    value-type
    class-type
    interface-type
    delegate-type
    dynamic
    type-parameter

rank-specifiers:
    rank-specifier
    rank-specifiers rank-specifier

rank-specifier:
    [ dim-separators_opt ]

dim-separators:
    ,
    dim-separators ,

delegate-type:
    type-name
```

引用类型值是对该类型实例的引用，后者称为 *object*。特殊值 *null* 与所有引用类型兼容，表示实例的缺失。

### 9.2.2 类类型

类类型定义一个包含数据成员（常量和字段）、函数成员（方法、属性、事件、索引器、运算符、实例构造函数、终结器和静态构造函数）以及嵌套类型的数据结构。类类型支持继承，派生类可以扩展和特化基类的机制。类类型的实例使用 *object-creation-expressions* (§12.7.11.2) 创建。

类类型在 §15 中描述。

某些预定义类类型在 C# 语言中有特殊含义，如下表所述。

| 类类型 | 描述 |
|---|---|
| System.Object | 所有其他类型的终极基类。参见 §9.2.3。 |
| System.String | C# 语言的字符串类型。参见 §9.2.5。 |
| System.ValueType | 所有值类型的基类。参见 9.3.2。 |
| System.Enum | 所有枚举类型的基类。参见 §19.5。 |
| System.Array | 所有数组类型的基类。参见 §17.2.2。 |
| System.Delegate | 所有委托类型的基类。参见 §20.1。 |
| System.Exception | 所有异常类型的基类。参见 §21.3。 |

### 9.2.3 object 类型

*object* 类类型是所有其他类型的终极基类。C# 中的每个类型直接或间接派生自 *object* 类类型。

关键字 *object* 只是预定义类 System.Object 的别名。

### 9.2.4 dynamic 类型

*dynamic* 类型与 *object* 一样，可以引用任何对象。当对 *dynamic* 类型表达式应用操作时，其解析会推迟到程序运行时。因此，如果操作不能合法地应用于引用对象，编译期间不会给出错误。相反，当操作解析在运行时失败时，将抛出异常。

dynamic 类型在 §9.7 中进一步描述，dynamic 绑定在 §12.3.1 中。

### 9.2.5 string 类型

string 类型是一个密封的类类型，直接继承自 object。string 类的实例表示 Unicode 字符字符串。

string 类型的值可以写为字符串字面量 (§7.4.5.6)。

关键字 string 只是预定义类 System.String 的别名。

### 9.2.6 接口类型

接口定义一个契约。实现接口的类或结构必须遵守其契约。接口可以从多个基接口继承，类或结构可以实现多个接口。

接口类型在 §18 中描述。

### 9.2.7 数组类型

数组是一个包含零个或多个变量的数据结构，通过计算的索引访问。数组中包含的变量，也称为数组的元素，都具有相同的类型，该类型称为数组的元素类型。

数组类型在 §17 中描述。

### 9.2.8 委托类型

委托是一个引用一个或多个方法的数据结构。对于实例方法，它还引用其对应的对象实例。

[Note: 委托在 C 或 C++ 中的最接近等价物是函数指针，但函数指针只能引用静态函数，而委托可以引用静态和实例方法。在后一种情况下，委托不仅存储方法的入口点引用，还存储在该对象实例上调用方法的对象实例引用。 end note]

委托类型在 §20 中描述。

### 9.3 值类型

### 9.3.1 通用

值类型是结构类型或枚举类型。C# 提供了一组预定义的结构类型，称为简单类型。简单类型通过关键字识别。

+   value-type:
+     struct-type
+     enum-type
+   
+   struct-type:
+     type-name
+     simple-type
+     nullable-value-type
+   
+   simple-type:
+     numeric-type
+     bool

-   对于结构体类型，默认值是通过将所有值类型字段设置为其默认值并将所有引用类型字段设为 null 而产生的值。
-   对于可空值类型，默认值是一个 HasValue 属性为 false 的实例。默认值也称为可空值类型的空值。尝试读取此类值的 Value 属性会导致抛出类型为 System.InvalidOperationException 的异常 (§9.3.11)。

与任何其他实例构造函数一样，值类型的默认构造函数使用 new 运算符调用。 [Note: 出于效率原因，此要求并不意味着实际让实现生成构造函数调用。对于值类型，默认值表达式 (§12.7.15) 产生的结果与使用默认构造函数相同。 end note] [Example: 在下面的代码中，变量 i、j 和 k 都被初始化为零。

```
class A
{
    void F() {
        int i = 0;
        int j = new int();
        int k = default(int);
    }
}
```

end example]

因为每个值类型都隐式具有一个公共无参数实例构造函数，所以结构体类型不能包含无参数构造函数的显式声明。然而，结构体类型允许声明带参数的实例构造函数 (§16.4.9)。

## 9.3.4 结构体类型

结构体类型是一种值类型，可以声明常量、字段、方法、属性、事件、索引器、运算符、实例构造函数、静态构造函数和嵌套类型。结构体类型的声明在 §16 中描述。

## 9.3.5 简单类型

C# 提供了一组预定义的结构体类型，称为简单类型。简单类型通过关键字标识，但这些关键字只是 System 命名空间中预定义结构体类型的别名，如下表所述。

| Keyword | Aliased type |
|---|---|
| sbyte | System.SByte |
| byte | System.Byte |
| short | System.Int16 |
| ushort | System.UInt16 |
| int | System.Int32 |
| uint | System.UInt32 |
| long | System.Int64 |
| ulong | System.UInt64 |
| char | System.Char |
| float | System.Single |
| double | System.Double |
| bool | System.Boolean |
| decimal | System.Decimal |

因为简单类型是结构体类型的别名，所以每个简单类型都有成员。 [Example: int 具有 System.Int32 中声明的成员以及从 System.Object 继承的成员，并且以下语句是允许的：

```
int i = int.MaxValue;          // System.Int32.MaxValue constant
string s = i.ToString();       // System.Int32.ToString() instance method
string t = 123.ToString();     // System.Int32.ToString() instance method
```

*end example*] [Note: 简单类型与其它结构体类型不同之处在于它们允许某些额外操作：

-   大多数简单类型允许通过编写 *literals* (§7.4.5) 来创建值。 [Example: 123 是 int 类型的字面量，'a' 是 char 类型的字面量。 *end example*] C# 对结构体类型的字面量没有一般性规定。
-   当表达式的操作数都是简单类型常量时，编译器可以对表达式进行编译时求值。这样的表达式称为 *constant-expression* (§12.20)。涉及其它结构体类型定义的运算符的表达式不被视为常量表达式。
-   通过 const 声明，可以声明简单类型的常量 (§15.4)。不能有其它结构体类型的常量，但类似的效果由 static readonly 字段提供。
-   涉及简单类型的转换可以参与其它结构体类型定义的转换运算符的求值，但用户定义的转换运算符永远不能参与另一个用户定义的转换运算符的求值 (§11.5.3)。 *end note*

### 9.3.6 整数类型

C# 支持九种整数类型：sbyte、byte、short、ushort、int、uint、long、ulong 和 char。整数类型具有以下大小和值范围：

-   sbyte 类型表示有符号 8 位整数，取值范围为 -128 到 127，包含边界。
-   byte 类型表示无符号 8 位整数，取值范围为 0 到 255，包含边界。
-   short 类型表示有符号 16 位整数，取值范围为 -32768 到 32767，包含边界。
-   ushort 类型表示无符号 16 位整数，取值范围为 0 到 65535，包含边界。
-   int 类型表示有符号 32 位整数，取值范围为 -2147483648 到 2147483647，包含边界。
-   uint 类型表示无符号 32 位整数，取值范围为 0 到 4294967295，包含边界。
-   long 类型表示有符号 64 位整数，取值范围为 -9223372036854775808 到 9223372036854775807，包含边界。
-   ulong 类型表示无符号 64 位整数，取值范围为 0 到 18446744073709551615，包含边界。
-   char 类型表示无符号 16 位整数，取值范围为 0 到 65535，包含边界。char 类型的可能取值集合对应于 Unicode 字符集。 [Note: 虽然 char 与 ushort 具有相同的表示，但在一个类型上允许的操作并不全部在另一个类型上允许。 *end note*]

整数类型的单目和双目运算符始终以有符号 32 位精度、无符号 32 位精度、有符号 64 位精度或无符号 64 位精度操作，详情见 §12.4.7。

char 类型被归类为整数类型，但它在两方面与其他整数类型不同：

-   不存在从其它类型到 char 类型的预定义隐式转换。特别是，尽管 byte 和 ushort 类型的取值范围完全可以用 char 类型表示，但从 sbyte、byte 或 ushort 到 char 的隐式转换并不存在。
-   char 类型的常量应写成字符字面量，或写成整数字面量并结合对 char 类型的强制转换。 [Example: (char)10 与 '\x000A' 相同。 *end example*]

checked 和 unchecked 运算符和语句用于控制整数类型算术运算和转换的溢出检查 (§12.7.14)。在 checked 上下文中，溢出会产生编译时错误或导致抛出 System.OverflowException。在 unchecked 上下文中，溢出会被忽略，任何不适合目标类型的最高位都会被丢弃。

## 9.3.7 浮点类型

C# 支持两种浮点类型：`float` 和 `double`。`float` 和 `double` 类型使用 32 位单精度和 64 位双精度 IEC 60559 格式表示，提供以下值集合：

-   正零和负零。在大多数情况下，正零和负零作为简单的零值表现相同，但某些操作会区分两者 (§12.9.3)。
-   正无穷大和负无穷大。无穷大由诸如将非零数除以零之类的操作产生。 [Example: `1.0 / 0.0` 得到正无穷大，而 `–1.0 / 0.0` 得到负无穷大。 end example]
-   *Not-a-Number* 值，通常缩写为 NaN。NaN 由无效的浮点运算产生，例如用零除零。
-   形式为 `s × m × 2^e` 的非零有限集合，其中 *s* 为 1 或 –1，而 *m* 和 *e* 由特定的浮点类型决定：对于 `float`，0 < *m* < 2^24 且 –149 ≤ *e* ≤ 104，对于 `double`，0 < *m* < 2^53 且 –1075 ≤ *e* ≤ 970。非规格化浮点数被视为有效的非零值。C# 既不要求也不禁止符合的实现支持非规格化浮点数。

`float` 类型可以表示从大约 `1.5 × 10^-45` 到 `3.4 × 10^38` 的值，精度为 7 位数字。

`double` 类型可以表示从大约 `5.0 × 10^-324` 到 `1.7 × 10^308` 的值，精度为 15–16 位数字。

如果二元运算符的任一操作数是浮点类型，则应用标准数值提升，如 §12.4.7 所述，并且操作以 `float` 或 `double` 精度执行。

浮点运算符，包括赋值运算符，从不产生异常。相反，在异常情况下，浮点运算会产生零、无穷大或 NaN，如下所述：

-   浮点运算的结果会四舍五入到目标格式中最接近的可表示值。
-   如果浮点运算结果的幅值对于目标格式来说太小，则运算结果变为正零或负零。
-   如果浮点运算结果的幅值对于目标格式来说太大，则运算结果变为正无穷大或负无穷大。
-   如果浮点运算无效，则运算结果变为 NaN。
-   如果浮点运算的一个或两个操作数是 NaN，则运算结果变为 NaN。

浮点运算可以使用比运算结果类型更高的精度执行。 [Example: 某些硬件架构支持“扩展”或“long double”浮点类型，其范围和精度高于 `double` 类型，并隐式使用这种更高精度的类型执行所有浮点运算。只有以极大的性能成本才能使此类硬件架构以 *less* 精度执行浮点运算，而 C# 允许对所有浮点运算使用更高精度的类型，而不是要求实现同时放弃性能和精度。除了提供更精确的结果外，这很少有可衡量的影响。然而，在形式为 `x * y / z` 的表达式中，其中乘法产生的结果超出 `double` 范围，但随后的除法将临时结果带回 `double` 范围，表达式在更高范围格式中求值的事实可能导致产生有限结果而不是 an

infinity. 要强制浮点类型的数值精确到其类型的精确度，可以使用显式转换。 end example]

## 9.3.8 decimal 类型

decimal 类型是一种适合金融和货币计算的 128 位数据类型。decimal 类型可以表示包括至少在 −7.9 × 10^28 到 7.9 × 10^28 范围内的值，精度至少为 28 位。

decimal 类型的有限值集合的形式为 (−1)^s × c × 10^e，其中符号 s 为 0 或 1，系数 c 满足 0 ≤ c < Cmax，且比例因子 e 满足 Emin ≤ e ≤ Emax，其中 Cmax 至少为 1 × 10^28，Emin ≤ 0，且 Emax ≥ 28。decimal 类型不一定支持带符号零、无穷大或 NaN。

decimal 以十的幂缩放的整数表示。对于绝对值小于 1.0m 的 decimal，其值精确到至少小数点后第 28 位。对于绝对值大于或等于 1.0m 的 decimal，其值精确到至少 28 位数字。与 float 和 double 数据类型相反，像 0.1 这样的 decimal 小数可以在 decimal 表示中精确表示。在 float 和 double 表示中，此类数字通常具有非终止的二进制展开，使得这些表示更容易产生舍入误差。

如果二元运算符的任一操作数是 decimal 类型，则应用标准数值提升，如 §12.4.7 所述，并且操作以 decimal 精度执行。

对 decimal 类型值进行操作的结果是先计算精确结果（保留比例，如每个运算符所定义）然后舍入以适应表示所得到的结果。结果舍入到最接近的可表示值，并且当结果与两个可表示值 equally close 时，舍入到最低有效数字位置为偶数的那个值（这称为“银行家舍入”）。也就是说，结果精确到至少小数点后第 28 位。请注意，舍入可能会将非零值产生为零值。

如果 decimal 算术操作产生的结果的绝对值对于 decimal 格式来说过大，则会抛出 System.OverflowException。

decimal 类型具有更高的精度，但范围可能小于浮点类型。因此，从浮点类型到 decimal 的转换可能会产生溢出异常，而从 decimal 到浮点类型的转换可能会导致精度损失或溢出异常。出于这些原因，浮点类型与 decimal 之间不存在隐式转换，并且如果没有显式转换，在同一表达式中直接混合浮点和 decimal 操作数时会发生编译时错误。

## 9.3.9 bool 类型

bool 类型表示布尔逻辑量。bool 类型的可能值是 true 和 false。

bool 与其他值类型之间不存在标准转换。特别是，bool 类型与整型是不同且独立的，bool 值不能用作整型值，反之亦然。

> [Note: 在 C 和 C++ 语言中，零的整数或浮点值，或空指针可以转换为布尔值 false，非零的整数或浮点值，或非空指针可以转换为布尔值 true。在 C# 中，此类转换是通过显式将整数或浮点值与零进行比较，或显式将对象引用与 null 进行比较来完成的。 end note]

## 9.3.10 枚举类型

枚举类型是一种具有命名常量的独立类型。每个枚举类型都有一个底层类型，该类型应为 byte、sbyte、short、ushort、int、uint、long 或 ulong。枚举类型的取值集合与底层类型的取值集合相同。枚举类型的值不受命名常量的限制。枚举类型通过枚举声明 (§19.2) 定义。

## 9.3.11 可空值类型

可空值类型可以表示其底层类型的所有值加上一个额外的 null 值。可空值类型写为 T?，其中 T 是底层类型。此语法是 System.Nullable<T> 的简写，两者形式可以互换使用。

相反，非可空值类型是除 System.Nullable<T> 及其简写 T?（对于任意 T）之外的任何值类型，加上任何被约束为非可空值类型的类型参数（即具有值类型约束 (§15.2.5) 的任何类型参数）。System.Nullable<T> 类型为 T 指定值类型约束，这意味着可空值类型的底层类型可以是任何非可空值类型。可空值类型的底层类型不能是可空值类型或引用类型。例如，int?? 和 string? 是无效类型。

可空值类型 T? 的实例有两个公共只读属性：

- 一个类型为 bool 的 HasValue 属性
- 一个类型为 T 的 Value 属性

HasValue 为 true 的实例称为非空。非空实例包含一个已知值，Value 返回该值。

HasValue 为 false 的实例称为 null。null 实例具有未定义的值。尝试读取 null 实例的 Value 会导致抛出 System.InvalidOperationException。访问可空实例的 Value 属性的过程称为解包。

除了默认构造函数外，每个可空值类型 T? 都有一个带单个类型为 T 参数的公共构造函数。给定类型为 T 的值 x，形式为

```
new T?(x)
```

的构造函数调用
创建一个 Value 属性为 x 的 T? 的非空实例。为给定值创建可空值类型的非空实例的过程称为包装。

从 null 字面量到 T? (§11.2.6) 以及从 T 到 T? (§11.2.5) 存在隐式转换。

可空类型 T? 不实现任何接口 (§18)。特别是，这意味着它不实现底层类型 T 实现的任何接口。

## 9.3.12 装箱和拆箱

装箱和拆箱的概念通过允许值类型的任何值在 type object 之间相互转换，为值类型和引用类型之间提供了一座桥梁。装箱和拆箱使得类型系统具有统一的视图，其中任何类型的值最终都可以作为对象处理。

装箱在 §11.2.8 中有更详细的描述，拆箱在 §11.3.6 中有描述。

## 9.4 构造类型

### 9.4.1 通用

通用类型声明本身表示一个未绑定通用类型，该类型用作“蓝图”，通过应用类型参数形成许多不同的类型。类型参数写在尖括号（< 和 >）内，紧跟在通用类型名称之后。包含至少一个类型参数的类型称为构造类型。构造类型可以在语言中类型名称可以出现的大多数位置中使用。未绑定通用类型只能在 typeof 表达式 (§12.7.12) 中使用。

- 数组类型是开放类型当且仅当其元素类型是开放类型。
- 构造类型是开放类型当且仅当其一个或多个类型参数是开放类型。构造的嵌套类型是开放类型当且仅当其一个或多个类型参数或其包含类型(们)的类型参数是开放类型。

封闭类型是指不是开放类型的类型。

在运行时，通用类型声明内的所有代码都在通过将类型参数应用于通用声明而创建的封闭构造类型的上下文中执行。通用类型中的每个类型参数都绑定到特定的运行时类型。所有语句和表达式的运行时处理始终使用封闭类型进行，而开放类型仅在编译时处理期间出现。

每个封闭构造类型都有自己的一组静态变量，这些变量不会与其他封闭构造类型共享。由于开放类型在运行时不存在，因此开放类型没有关联的静态变量。如果两个封闭构造类型是从同一个未绑定通用类型构造的，并且它们对应的类型参数是相同类型，则它们是同一类型。

### 9.4.4 绑定类型和未绑定类型

术语未绑定类型指的是非通用类型或未绑定通用类型。术语绑定类型指的是非通用类型或构造类型。

未绑定类型指的是类型声明所声明的实体。未绑定通用类型本身不是一种类型，不能用作变量、参数或返回值的类型，也不能用作基类型。未绑定通用类型只能在 typeof 表达式 (§12.7.12) 中被引用。

### 9.4.5 满足约束

每当引用构造类型或通用方法时，所提供的类型参数都会与通用类型或方法上声明的类型参数约束 (§15.2.5) 进行检查。对于每个 where 子句，对应于命名类型参数的类型参数 A 会按如下方式与每个约束进行检查：

- 如果约束是类类型、接口类型或类型参数，则令 C 表示该约束，其中约束中出现的任何类型参数都替换为所提供的类型参数。为了满足约束，类型 A 必须能够通过以下其中一种方式转换为类型 C：
  - 恒等转换 (§11.2.2)
  - 隐式引用转换 (§11.2.7)
  - 装箱转换 (§11.2.8)，前提是类型 A 是非可空值类型。
  - 从类型参数 A 到 C 的隐式引用、装箱或类型参数转换。
- 如果约束是引用类型约束（class），则类型 A 必须满足以下其中之一：
  - A 是接口类型、类类型、委托类型、数组类型或 dynamic 类型。[Note: System.ValueType 和 System.Enum 是满足此约束的引用类型。 end note]
  - A 是已知为引用类型的类型参数 (§9.2)。
- 如果约束是值类型约束（struct），则类型 A 必须满足以下其中之一：
  - A 是 struct 类型或 enum 类型，但不是可空值类型。[Note: System.ValueType 和 System.Enum 是不满足此约束的引用类型。 end note]
  - A 是具有值类型约束的类型参数 (§15.2.5)。
- 如果约束是构造函数约束 new()，则类型 A 不应为抽象类型，并且应具有公共无参数构造函数。如果以下任一条件为真，则满足此约束：
  - A 是值类型，因为所有值类型都有公共默认构造函数 (§9.3.3)。
  - A 是具有构造函数约束的类型参数 (§15.2.5)。




- A 是具有值类型约束（§15.2.5）的类型参数。
- A 是一个非抽象类，并且包含一个显式声明的无参数公共构造函数。
- A 不是抽象的，并且具有默认构造函数（§15.11.5）。

如果给定的类型实参不满足类型参数的一个或多个约束，则发生编译时错误。

由于类型参数不被继承，约束也从不被继承。[示例：在下面的代码中，D 需要指定其类型参数 T 上的约束，以便 T 满足基类 B<T> 施加的约束。相比之下，类 E 不需要指定约束，因为 List<T> 对任意 T 都实现 IEnumerable。

```
class B<T> where T: IEnumerable {...}
class D<T>: B<T> where T: IEnumerable {...}
class E<T>: B<List<T>> {...}
```

示例结束

## 9.5 类型参数

类型参数是一个标识符，用于指定该参数在运行时绑定到的值类型或引用类型。

```
type-parameter:
    identifier
```

由于类型参数可以用许多不同的类型实参来实例化，因此类型参数具有与其他类型略有不同的操作和限制。[注意：这些包括：

- 类型参数不能直接用于声明基类（§15.2.4.2）或接口（§18.2.4）。
- 对类型参数进行成员查找的规则取决于应用于该类型参数的约束（如果有）。它们在 §12.5 中详细说明。
- 类型参数可用的转换取决于应用于该类型参数的约束（如果有）。它们在 §11.2.11 和 §11.3.8 中详细说明。
- 除非已知类型参数是引用类型（§11.2.11），否则不能将字面量 null 转换为由类型参数给定的类型。但是，可以改用默认表达式（§12.7.15）。此外，除非类型参数具有值类型约束，否则可以使用 == 和 != 将由类型参数给定类型的值与 null 进行比较（§12.11.7）。
- 只有当类型参数受构造函数约束或值类型约束（§15.2.5）约束时，new 表达式（§12.7.11.2）才能与类型参数一起使用。
- 类型参数不能在特性中的任何位置使用。
- 类型参数不能用于成员访问（§12.7.5）或类型名称（§8.8）中，以标识静态成员或嵌套类型。
- 类型参数不能用作非托管类型（§23.3）。

注意结束

作为一种类型，类型参数纯粹是编译时构造。在运行时，每个类型参数都绑定到运行时类型，该类型通过在泛型类型声明中提供类型实参来指定。因此，用类型参数声明的变量在运行时将是封闭构造类型（§9.4.3）。涉及类型参数的所有语句和表达式的运行时执行都使用作为该参数的类型实参提供的类型。

## 9.6 表达式树类型

表达式树允许将 lambda 表达式表示为数据结构，而不是可执行代码。表达式树是形式为 `System.Linq.Expressions.Expression<TDelegate>` 的表达式树类型的值，其中 `TDelegate` 是任意委托类型。在本规范的其余部分中，我们将使用简写 `Expression<TDelegate>` 来指代这些类型。

如果存在从 lambda 表达式到委托类型 `D` 的转换，则也存在到表达式树类型 `Expression<TDelegate>` 的转换。将 lambda 表达式转换为委托类型会生成一个引用该 lambda 表达式可执行代码的委托，而转换为表达式树类型则创建该 lambda 表达式的表达式树表示。

表达式树是 lambda 表达式高效的内存数据表示，并使 lambda 表达式的结构透明且显式。

就像委托类型 `D` 一样，`Expression<TDelegate>` 被认为具有参数类型和返回类型，且与 `D` 的相同。

> [示例：以下程序将 lambda 表达式同时表示为可执行代码和表达式树。由于存在到 `Func<int, int>` 的转换，因此也存在到 `Expression<Func<int, int>>` 的转换：

```
    Func<int, int> del = x => x + 1;            // Code
    Expression<Func<int, int>> exp = x => x + 1; // Data
```

> 在这些赋值之后，委托 `del` 引用一个返回 `x + 1` 的方法，而表达式树 `exp` 引用一个描述表达式 `x => x + 1` 的数据结构。示例结束]

泛型类型 `Expression<TDelegate>` 的确切定义，以及当 lambda 表达式转换为表达式树类型时构造表达式树的精确规则，都依赖于实现。

有两点需要明确说明：

- 并非所有 lambda 表达式都能转换为表达式树。例如，具有语句体的 lambda 表达式以及包含赋值表达式的 lambda 表达式无法表示。在这些情况下，转换仍然存在，但会在编译时失败。这些例外在 §11.7.3 中详细说明。
- `Expression<TDelegate>` 提供一个实例方法 `Compile`，该方法生成类型为 `TDelegate` 的委托：

```
      Func<int, int> del2 = exp.Compile();
```

    调用此委托会导致执行由表达式树表示的代码。因此，给定上述定义，`del1` 和 `del2` 是等效的，并且以下两个语句将具有相同的效果：

```
      int i1 = del1();
      int i2 = del2(1);
```

    执行此代码后，`i1` 和 `i2` 的值都将为 2。

## 9.7 动态类型

类型 `dynamic` 在 C# 中具有特殊含义。其目的是允许动态绑定，这在 §12.3.2 中详细描述。

`dynamic` 被认为与 `object` 相同，但在以下方面除外：

- 对 `dynamic` 类型表达式的操作可以进行动态绑定（§12.3.3）。
- 如果 `dynamic` 和 `object` 都是候选，类型推断（§12.6.3）将优先选择 `dynamic` 而不是 `object`。
- `dynamic` 不能用作
  - `object` 创建表达式中的类型（§12.7.11.2）
  - 成员访问中的预定义类型（§12.7.5.1）
  - typeof 运算符的操作数
  - 特性实参
  - 约束
  - 扩展方法类型
  - struct-interfaces（§16.2.4）或 interface-type-list（§15.2.4.1）内类型实参的任何部分。

由于这种等效性，以下成立：

- 在 object 和 dynamic 之间，以及在将 dynamic 替换为 object 时相同的构造类型之间，存在隐式恒等转换
- 到 object 和从 object 的隐式与显式转换也适用于到 dynamic 和从 dynamic。
- 将 dynamic 替换为 object 时相同的签名被视为相同签名
- 类型 dynamic 在运行时与 object 无法区分。
- 类型为 dynamic 的表达式称为**动态表达式**。

## 10. 变量

### 10.1 概述

变量表示存储位置。每个变量都有一个类型，该类型确定可以存储在变量中的值。C# 是一种类型安全的语言，并且 C# 编译器保证存储在变量中的值始终具有适当的类型。变量的值可以通过赋值或使用 ++ 和 -- 运算符来更改。

在可以获取变量的值之前，该变量应已明确赋值（§10.4）。

如下列子条款所述，变量要么是初始已赋值，要么是初始未赋值。初始已赋值的变量具有定义明确的初始值，并且始终被视为明确赋值。初始未赋值的变量没有初始值。要使初始未赋值的变量在某个位置被视为明确赋值，在通向该位置的每条可能执行路径中都必须对该变量进行赋值。

### 10.2 变量类别

### 10.2.1 概述

C# 定义了七种变量类别：静态变量、实例变量、数组元素、值参数、引用参数、输出参数和局部变量。后续子条款描述这些类别中的每一种。

[示例：在以下代码中

```
class A
{
    public static int x;
    int y;
    void F(int[] v, int a, ref int b, out int c) {
        int i = 1;
        c = a + b++;
    }
}
```

x 是静态变量，y 是实例变量，v[0] 是数组元素，a 是值参数，b 是引用参数，c 是输出参数，i 是局部变量。示例结束

### 10.2.2 静态变量

使用 static 修饰符声明的字段称为静态变量。静态变量在其包含类型的静态构造函数（§15.12）执行之前开始存在，并在关联的应用程序域停止存在时停止存在。

静态变量的初始值是该变量类型的默认值（§10.3）。

为了明确赋值检查的目的，静态变量被视为初始已赋值。

### 10.2.3 实例变量

### 10.2.3.1 概述

未使用 static 修饰符声明的字段称为实例变量。




### 10.2.3.2 类中的实例变量

类的实例变量在创建该类的新实例时产生，并在对该实例没有任何引用且该实例的终结器（如果有）执行完毕后停止存在。

类的实例变量的初始值是变量类型默认值（§10.3）。

为确定性赋值检查的目的，类的实例变量被视为初始已赋值。

### 10.2.3.3 结构体中的实例变量

结构体的实例变量与所属的结构体变量具有完全相同的生命周期。换句话说，当结构体类型的变量产生或停止存在时，该结构体的实例变量也同样如此。

结构体实例变量的初始赋值状态与包含它的结构体变量相同。换句话说，当结构体变量被视为初始已赋值时，其实例变量也被视为已赋值；当结构体变量被视为初始未赋值时，其实例变量也同样未赋值。

## 10.2.4 数组元素

数组的元素在创建数组实例时产生，并在对该数组实例没有任何引用时停止存在。

数组的每个元素的初始值是数组元素类型默认值（§10.3）。

为确定性赋值检查的目的，数组元素被视为初始已赋值。

## 10.2.5 值参数

未使用 ref 或 out 修饰符声明的参数是值参数。

值参数在所属的函数成员（方法、实例构造函数、访问器或运算符）或匿名函数被调用时产生，并使用调用中给出的参数值进行初始化。值参数通常在函数体执行完成时停止存在。但是，如果值参数被匿名函数（§12.16.6.2）捕获，其生命周期至少会延长至从该匿名函数创建的委托或表达式树可供垃圾回收为止。

## 10.2.6 引用参数

使用 ref 修饰符声明的参数是引用参数。

引用参数不会创建新的存储位置。相反，引用参数表示函数成员或匿名函数调用中作为参数给出的变量的同一存储位置。因此，引用参数的值始终与底层变量相同。

以下确定性赋值规则适用于引用参数。[Note: 输出参数的规则不同，描述在 §10.2.7 中。end note]

- 变量在作为函数成员或委托调用中的引用参数传递之前必须已确定性赋值（§10.4）。
- 在函数成员或匿名函数内部，引用参数被视为初始已赋值。

对于结构体类型，在实例方法或实例访问器（§12.2.1）或带有构造函数初始值设定项的实例构造函数内部，this 关键字完全表现得像结构体类型的引用参数（§12.7.8）。

## 10.2.7 输出参数

使用 out 修饰符声明的参数是输出参数。

输出参数不会创建新的存储位置。相反，输出参数表示函数成员或委托调用中作为参数给出的变量的同一存储位置。因此，输出参数的值始终与底层变量相同。

以下确定性赋值规则适用于输出参数。[Note: 引用参数的规则不同，描述在 §10.2.6 中。end note]

- 变量在作为函数成员或委托调用中的输出参数传递之前不必已确定性赋值。
- 在函数成员或委托调用正常完成后，作为输出参数传递的每个变量在该执行路径中都被视为已赋值。
- 在函数成员或匿名函数内部，输出参数被视为初始未赋值。
- 函数成员或匿名函数的每个输出参数在函数成员或匿名函数正常返回之前必须已确定性赋值（§10.4）。

在结构体类型的实例构造函数内部，this 关键字的行为完全像结构体类型的输出参数或引用参数，具体取决于构造函数声明是否包含构造函数初始值设定项（§12.7.8）。

## 10.2.8 局部变量

局部变量由局部变量声明、foreach 语句或 try 语句的 specific-catch 子句声明。对于 foreach 语句，局部变量是迭代变量（§13.9.5）。对于 specific-catch 子句，局部变量是异常变量（§13.11）。由 foreach 语句或 specific-catch 子句声明的局部变量被视为初始已赋值。

局部变量声明可以出现在块、for 语句、switch 块或 using 语句中。

局部变量的生命周期是程序执行期间为其保证保留存储的部分。该生命周期从进入与其关联的作用域开始，至少持续到该作用域以某种方式结束为止。（进入封闭块、调用方法或从迭代器块产生值会暂停，但不会结束当前作用域的执行。）如果局部变量被匿名函数（§12.16.6.2）捕获，其生命周期至少会延长至从匿名函数创建的委托或表达式树以及任何引用捕获变量的其他对象可供垃圾回收为止。如果父作用域被递归或迭代进入，每次都会创建局部变量的新实例，并且其局部变量初始值设定项（如果有）每次都会被求值。[Note: 每次进入其作用域时都会实例化一个局部变量。此行为对包含匿名方法的用户代码可见。end note] [Note: 由 foreach 语句声明的迭代变量（§13.9.5）的生命周期是该语句的一次迭代。每次迭代都会创建一个新变量。end note] [Note: 局部变量的实际生命周期取决于实现。例如，编译器可能静态确定块中的局部变量仅在该块的一小部分中使用。利用此分析，编译器可以生成导致变量存储的生命周期短于其包含块的代码。end note]

局部引用变量所引用的存储与该局部引用变量的生命周期独立回收（§8.9）。end note

通过局部变量声明引入的局部变量不会自动初始化，因此没有默认值。这样的局部变量被视为初始未赋值。[Note: 包含局部变量初始值设定项的局部变量声明仍然是初始未赋值。声明的执行与对变量的赋值（§10.4.4.5）完全相同。可以在不执行其局部变量初始值设定项的情况下使用变量；例如，在初始值设定项表达式本身内或通过使用 goto 语句绕过初始化：

```
goto L;
int x = 1; // never executed
L: x += 1; // error: x not definitely assigned
```

end note

在局部变量的作用域内，在文本位置上在其局部变量声明符之前引用该局部变量是编译时错误。

## 10.3 默认值

以下类别的变量会自动初始化为其默认值：

- 静态变量。
- 类实例的实例变量。
- 数组元素。

变量的默认值取决于变量的类型，并按如下方式确定：

- 对于值类型的变量，默认值与值类型默认构造函数（§9.3.3）计算的值相同。
- 对于引用类型的变量，默认值是 null。

> [Note: 初始化为默认值通常通过让内存管理器或垃圾收集器在内存分配使用前将其初始化为全位零来完成。因此，使用全位零来表示空引用很方便。end note]

## 10.4 确定性赋值

### 10.4.1 一般

在函数成员或匿名函数的可执行代码中的给定位置，如果编译器可以通过特定的静态流分析（§10.4.4）证明变量已被自动初始化或已被至少一次赋值的目标，则称该变量已确定性赋值。[Note: 非正式地说，确定性赋值的规则是：

- 初始已赋值的变量（§10.4.2）始终被视为确定性赋值。
- 初始未赋值的变量（§10.4.3）在给定位置被视为确定性赋值，如果通向该位置的所有可能执行路径都包含以下至少一项：
  - 变量为左操作数的简单赋值（§12.18.2）。
  - 将变量作为输出参数传递的调用表达式（§12.7.6）或对象创建表达式（§12.7.11.2）。
  - 对于局部变量，包含变量初始值设定项的变量的局部变量声明（§13.6.2）。

上述非正式规则的正式规范描述在 §10.4.2、§10.4.3 和 §10.4.4 中。end note

结构体类型变量的实例变量的确定性赋值状态既单独跟踪也集体跟踪。除上述规则外，以下规则适用于结构体类型变量及其实例变量：

- 如果其包含的结构体类型变量被视为确定性赋值，则实例变量被视为确定性赋值。



- 如果结构类型变量的每个实例变量都被视为确定赋值，则该结构类型变量被视为确定赋值。

在以下上下文中，确定赋值是一项要求：

- 在获取变量值的每个位置，该变量都应是确定赋值的。[注意：这确保永远不会出现未定义值。结束注意] 变量在表达式中的出现被视为获取该变量的值，但以下情况除外：
  - 该变量是简单赋值的左操作数；
  - 该变量作为输出参数传递；或
  - 该变量是结构类型变量，并作为成员访问的左操作数出现。
- 在将变量作为引用参数传递的每个位置，该变量都应是确定赋值的。[注意：这确保被调用的函数成员可以将该引用参数视为初始已赋值。结束注意]
- 函数成员的所有输出参数在函数成员返回的每个位置（通过返回语句，或通过执行到达函数成员主体的末尾）都应是确定赋值的。[注意：这确保函数成员不会在输出参数中返回未定义值，从而使编译器能够将接受变量作为输出参数的函数成员调用视为对该变量的赋值。结束注意]
- 结构类型实例构造函数的 this 变量在该实例构造函数返回的每个位置都应是确定赋值的。

## 10.4.2 初始已赋值变量

以下类别的变量被归类为初始已赋值：

- 静态变量。
- 类实例的实例变量。
- 初始已赋值的结构变量的实例变量。
- 数组元素。
- 值参数。
- 引用参数。
- 在 catch 子句或 foreach 语句中声明的变量。

## 10.4.3 初始未赋值变量

以下类别的变量被归类为初始未赋值：

- 初始未赋值的结构变量的实例变量。
- 输出参数，包括没有构造函数初始化器的结构实例构造函数的 this 变量。
- 局部变量，但在 catch 子句或 foreach 语句中声明的变量除外。

## 10.4.4 判定确定赋值的精确规则

### 10.4.4.1 概述

为了判定每个使用的变量都是确定赋值的，编译器应使用与本子条款所述过程等效的过程。

编译器处理每个具有一个或多个初始未赋值变量的函数成员的主体。对于每个初始未赋值变量 v，编译器在函数成员中的以下每个点确定 v 的确定赋值状态：

- 每条语句的开头
- 每条语句的结束点（§13.2）
- 每条将控制转移到另一条语句或某条语句结束点的弧上
- 每个表达式的开头
- 每个表达式的末尾

v 的确定赋值状态可以是以下之一：

- 确定赋值。这表示在通往此点的所有可能控制流上，v 都已被赋值。
- 未确定赋值。对于 bool 类型表达式末尾处变量的状态，未确定赋值的变量状态可能（但不一定）属于以下子状态之一：
  - 在表达式为 true 后确定赋值。此状态表示如果布尔表达式的求值结果为 true，则 v 是确定赋值的；但如果布尔表达式的求值结果为 false，则不一定赋值。
  - 在表达式为 false 后确定赋值。此状态表示如果布尔表达式的求值结果为 false，则 v 是确定赋值的；但如果布尔表达式的求值结果为 true，则不一定赋值。

以下规则规定在每个位置如何确定变量 v 的状态。

### 10.4.4.2 语句的一般规则

- v 在函数成员主体的开头不是确定赋值的。
- v 在任何其他语句开头的确定赋值状态，通过检查所有以该语句开头为目标的控制流转移上 v 的确定赋值状态来确定。当且仅当 v 在所有此类控制流转移上都是确定赋值的，v 在该语句开头才是确定赋值的。可能的控制流转移集合按照与检查语句可达性（§13.2）相同的方式确定。
- v 在块语句、checked 语句、unchecked 语句、if 语句、while 语句、do 语句、for 语句、foreach 语句、lock 语句、using 语句或 switch 语句的结束点处的确定赋值状态，通过检查所有以该语句结束点为目标控制流转移上 v 的确定赋值状态来确定。如果 v 在所有此类控制流转移上都是确定赋值的，则 v 在该语句的结束点处是确定赋值的。否则，v 在该语句的结束点处不是确定赋值的。可能的控制流转移集合按照与检查语句可达性（§13.2）相同的方式确定。[注意：由于不存在通往不可达语句的控制路径，因此在任何不可达语句的开头，v 都是确定赋值的。结束注意]

### 10.4.4.3 块语句、checked 语句和 unchecked 语句

v 在控制转移到块中语句列表的第一条语句（或者，如果语句列表为空，则转移到块的结束点）时的确定赋值状态，与 v 在块语句、checked 语句或 unchecked 语句之前的确定赋值状态相同。

### 10.4.4.4 表达式语句

对于由表达式 expr 构成的表达式语句 stmt：

- v 在 expr 开头的确定赋值状态与在 stmt 开头的确定赋值状态相同。
- 如果 v 在 expr 末尾是确定赋值的，则它在 stmt 的结束点是确定赋值的；否则，它在 stmt 的结束点不是确定赋值的。

### 10.4.4.5 声明语句

- 如果 stmt 是不带初始值设定项的声明语句，则 v 在 stmt 结束点的确定赋值状态与在 stmt 开头的确定赋值状态相同。
- 如果 stmt 是带初始值设定项的声明语句，则确定 v 的确定赋值状态的方式，就好像 stmt 是一个语句列表，其中每个带初始值设定项的声明对应一个赋值语句（按声明顺序）。

### 10.4.4.6 if 语句

对于形式如下的 if 语句 stmt：

```
if ( expr ) then-stmt else else-stmt
```

- v 在 expr 开头的确定赋值状态与在 stmt 开头的确定赋值状态相同。
- 如果 v 在 expr 末尾是确定赋值的，则在控制流转移到 then-stmt 时，以及转移到 else-stmt（如果没有 else 子句，则转移到 stmt 的结束点）时，v 是确定赋值的。
- 如果 v 在 expr 末尾具有状态“在表达式为 true 后确定赋值”，则它在控制流转移到 then-stmt 时是确定赋值的，而在控制流转移到 else-stmt（如果没有 else 子句，则转移到 stmt 的结束点）时不是确定赋值的。
- 如果 v 在 expr 末尾具有状态“在表达式为 false 后确定赋值”，则它在控制流转移到 else-stmt 时是确定赋值的，而在控制流转移到 then-stmt 时不是确定赋值的。当且仅当 v 在 then-stmt 的结束点是确定赋值的，v 才在 stmt 的结束点是确定赋值的。
- 否则，在控制流转移到 then-stmt 或 else-stmt（如果没有 else 子句，则转移到 stmt 的结束点）时，v 被视为不是确定赋值的。

### 10.4.4.7 switch 语句

在具有控制表达式 expr 的 switch 语句 stmt 中：

- v 在 expr 开头的确定赋值状态与 v 在 stmt 开头的状态相同。
- v 在控制流转移到可到达的 switch 块语句列表时的确定赋值状态，与 v 在 expr 末尾的确定赋值状态相同。

### 10.4.4.8 while 语句

对于形式如下的 while 语句 stmt：

```
while ( expr ) while-body
```

- v 在 expr 开头的确定赋值状态与在 stmt 开头的确定赋值状态相同。
- 如果 v 在 expr 末尾是确定赋值的，则在控制流转移到 while-body 和转移到 stmt 的结束点时，v 是确定赋值的。
- 如果 v 在 expr 末尾具有状态“在表达式为 true 后确定赋值”，则它在控制流转移到 while-body 时是确定赋值的，但在 stmt 的结束点不是确定赋值的。
- 如果 v 在 expr 末尾具有状态“在表达式为 false 后确定赋值”，则它在控制流转移到 stmt 的结束点时是确定赋值的，但在控制流转移到 while-body 时不是确定赋值的。

### 10.4.4.9 do 语句

对于形式如下的 do 语句 stmt：

```
do do-body while ( expr ) ;
```

- v 在控制流从 stmt 开头转移到 do-body 时的确定赋值状态，与在 stmt 开头的确定赋值状态相同。
- v 在 expr 开头的确定赋值状态与在 do-body 结束点的确定赋值状态相同。
- 如果 v 在 expr 末尾是确定赋值的，则它在控制流转移到 stmt 的结束点时是确定赋值的。
- 如果 v 在 expr 末尾具有状态“在表达式为 false 后确定赋值”，则它在控制流转移到 stmt 的结束点时是确定赋值的，但在控制流转移到 do-body 时不是确定赋值的。



## 10.4.4.10 For 语句

For 语句的确定性赋值检查形式为：

```
for ( for-initializer ; for-condition ; for-iterator ) embedded-statement
```

按如下语句编写的方式进行：

```
{
    for-initializer ;
    while ( for-condition ) {
        embedded-statement ;
    LLoop:        for-iterator ;
    }
}
```

continue 语句以 for 语句为目标时，被翻译为以标签 LLoop 为目标的 goto 语句。如果 for 语句中省略了 for-condition，则确定性赋值的求值按在上述展开中将 for-condition 替换为 true 的方式进行。

## 10.4.4.11 Break、continue 和 goto 语句

由 break、continue 或 goto 语句引起的控制流转移上变量 v 的确定性赋值状态，与该语句开始时变量 v 的确定性赋值状态相同。

## 10.4.4.12 Throw 语句

对于形式为

```
throw expr ;
```

的语句 stmt，expr 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。

## 10.4.4.13 Return 语句

对于形式为

```
return expr ;
```

的语句 stmt：

- expr 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- 如果 v 是输出参数，则它必须在以下任一位置被确定性赋值：
    - expr 之后
    - 或在包含 return 语句的 try-finally 或 try-catch-finally 的 finally 块结束时。

对于形式为：

```
return ;
```

的语句 stmt：

- 如果 v 是输出参数，则它必须在以下任一位置被确定性赋值：
    - stmt 之前
    - 或在包含 return 语句的 try-finally 或 try-catch-finally 的 finally 块结束时。

## 10.4.4.14 Try-catch 语句

对于形式为：

```
try try-block
catch ( ... ) catch-block-1
...
catch ( ... ) catch-block-n
```

的语句 stmt：

- try-block 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- catch-block-i（任意 i）开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- stmt 的结束点上变量 v 被确定性赋值当且仅当变量 v 在 try-block 的结束点以及每个 catch-block-i（从 1 到 n 的每个 i）都被确定性赋值。

## 10.4.4.15 Try-finally 语句

对于形式为：

```
try try-block finally finally-block
```

的 try 语句 stmt：

- try-block 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- finally-block 开始时变量 v 的确定性赋值状态与 stmt 开始时变量 v 的确定性赋值状态相同。
- stmt 的结束点上变量 v 被确定性赋值当且仅当以下至少一个为真：
    - try-block 结束点上变量 v 被确定性赋值
    - finally-block 结束点上变量 v 被确定性赋值

如果进行控制流转移（例如 goto 语句），该转移开始于 try-block 内并结束于 try-block 外，则如果 finally-block 结束点上变量 v 被确定性赋值，则在此控制流转移上变量 v 也被视为确定性赋值。（这不是仅有的条件——如果由于其他原因在此控制流转移上变量 v 被确定性赋值，则它仍被视为确定性赋值。）

## 10.4.4.16 Try-catch-finally 语句

对于形式为：

```
try try-block
catch ( ... ) catch-block-1
...
catch ( ... ) catch-block-n
finally finally-block
```

的 try-catch-finally 语句的确定性赋值分析，按如下语句进行，即一个包围 try-catch 语句的 try-finally 语句：

```
try {
    try try-block
    catch ( ... ) catch-block-1
    ...
    catch ( ... ) catch-block-n
}
finally finally-block
```

[示例：以下示例演示了 try 语句（§13.11）的不同块如何影响确定性赋值。

```
class A
{
    static void F() {
        int i, j;
        try {
            goto LABEL;
            // neither i nor j definitely assigned
            i = 1;
            // i definitely assigned
        }
        catch {
            // neither i nor j definitely assigned
            i = 3;
            // i definitely assigned
        }
        finally {
            // neither i nor j definitely assigned
            j = 5;
            // j definitely assigned
        }
        // i and j definitely assigned
LABEL:
        // j definitely assigned
    }
}
end example]

## 10.4.4.17 Foreach 语句

对于形式为：

```
foreach ( *type identifier* in *expr* ) *embedded-statement*
```

的 foreach 语句 *语句*：

- *表达式* 开始时 *v* 的确定性赋值状态与 *语句* 开始时 *v* 的状态相同。
- 对 *嵌入语句* 或 *语句* 结束点的控制流转移上 *v* 的确定性赋值状态与 *表达式* 结束时 *v* 的状态相同。

## 10.4.4.18 Using 语句

对于形式为：

```
using ( *resource-acquisition* ) *embedded-statement*
```

的 using 语句 *语句*：

- *资源获取* 开始时 *v* 的确定性赋值状态与 *语句* 开始时 *v* 的状态相同。
- 对 *嵌入语句* 的控制流转移上 *v* 的确定性赋值状态与 *资源获取* 结束时 *v* 的状态相同。

## 10.4.4.19 Lock 语句

对于形式为：

```
lock ( *expr* ) *embedded-statement*
```

的 lock 语句 *语句*：

- *表达式* 开始时 *v* 的确定性赋值状态与 *语句* 开始时 *v* 的状态相同。
- 对 *嵌入语句* 的控制流转移上 *v* 的确定性赋值状态与 *表达式* 结束时 *v* 的状态相同。

## 10.4.4.20 Yield 语句

对于形式为：

```
yield return *expr* ;
```

的 yield return 语句 *语句*：

- *表达式* 开始时 *v* 的确定性赋值状态与 *语句* 开始时 *v* 的状态相同。
- *语句* 结束时 *v* 的确定性赋值状态与 *表达式* 结束时 *v* 的状态相同。

yield break 语句对确定性赋值状态没有影响。

- expr_i（i 大于 1）开始时变量 v 的确定性赋值状态与 expr_{i-1} 结束时的确定性赋值状态相同。
- expr 结束时变量 v 的确定性赋值状态与 expr_n 结束时的确定性赋值状态相同。

## 10.4.4.24 调用表达式和对象创建表达式

如果要调用的方法是没有任何实现部分方法声明的部分方法，或是调用被省略的条件方法（§22.5.3.2），则调用后变量 v 的确定性赋值状态与调用前变量 v 的确定性赋值状态相同。否则适用以下规则：

对于形式为：

```
primary-expression ( arg₁, arg₂, ... , argₙ )
```

或对象创建表达式 expr 形式为：

```
new type ( arg₁, arg₂, ... , argₙ )
```

- 对于调用表达式，primary-expression 之前变量 v 的确定性赋值状态与 expr 之前变量 v 的状态相同。
- 对于调用表达式，argᵢ 之前变量 v 的确定性赋值状态与 primary-expression 之后变量 v 的状态相同。
- 对于对象创建表达式，argᵢ 之前变量 v 的确定性赋值状态与 expr 之前变量 v 的状态相同。
- 对于每个参数 argᵢ，argᵢ 之后变量 v 的确定性赋值状态由正常表达式规则确定，忽略任何 ref 或 out 修饰符。
- 对于每个参数 argᵢ，对于大于 1 的任意 i，argᵢ 之前变量 v 的确定性赋值状态与 argᵢ₋₁ 之后变量 v 的状态相同。
- 如果变量 v 作为 out 参数（即形式为 "out v" 的参数）在任一参数中传递，则 expr 之后变量 v 的状态被确定性赋值。否则，expr 之后变量 v 的状态与 argₙ 之后变量 v 的状态相同。
- 对于数组初始值设定项（§12.7.11.5）、对象初始值设定项（12.7.11.3）、集合初始值设定项（§12.7.11.4）和匿名对象初始值设定项（§12.7.11.7），确定性赋值状态由这些构造所定义展开的方式确定。

## 10.4.4.25 简单赋值表达式

对于形式为 w = expr-rhs 的表达式 expr：

- w 之前变量 v 的确定性赋值状态与 expr 之前变量 v 的确定性赋值状态相同。
- expr-rhs 之前变量 v 的确定性赋值状态与 w 之后变量 v 的确定性赋值状态相同。
- 如果 w 与 v 相同变量，则 expr 之后变量 v 的确定性赋值状态被确定性赋值。否则，expr 之后变量 v 的确定性赋值状态与 expr-rhs 之后变量 v 的确定性赋值状态相同。

[示例：在以下代码中

```
class A
{
    static void F(int[] arr) {
        int x;
        arr[x = 1] = x;  // ok
    }
}
```

在 `arr[x = 1]` 作为第二个简单赋值的左侧求值之后，变量 x 被视为明确赋值。示例结束]

## 10.4.4.26 && 表达式

对于形式为 expr-first && expr-second 的表达式 expr：

- v 在 expr-first 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- v 在 expr-second 之前的明确赋值状态为明确赋值，当且仅当 v 在 expr-first 之后的状态为明确赋值或“true 表达式后明确赋值”。否则，它不是明确赋值。
- v 在 expr 之后的状态由以下规则确定：
    - 如果 v 在 expr-first 之后的状态为明确赋值，则 v 在 expr 之后的状态为明确赋值。
    - 否则，如果 v 在 expr-second 之后的状态为明确赋值，且 v 在 expr-first 之后的状态为“false 表达式后明确赋值”，则 v 在 expr 之后的状态为明确赋值。
    - 否则，如果 v 在 expr-second 之后的状态为明确赋值或“true 表达式后明确赋值”，则 v 在 expr 之后的状态为“true 表达式后明确赋值”。
    - 否则，如果 v 在 expr-first 之后的状态为“false 表达式后明确赋值”，且 v 在 expr-second 之后的状态为“false 表达式后明确赋值”，则 v 在 expr 之后的状态为“false 表达式后明确赋值”。
    - 否则，v 在 expr 之后的状态不是明确赋值。

[示例：在以下代码中

```
class A
{
    static void F(int x, int y) {
        int i;
        if (x >= 0 && (i = y) >= 0) {
            // i definitely assigned
        }
        else {
            // i not definitely assigned
        }
        // i not definitely assigned
    }
}
```

在 if 语句的一个嵌入语句中，变量 i 被视为明确赋值，但在另一个嵌入语句中则不是。在方法 F 的 if 语句中，变量 i 在第一个嵌入语句中是明确赋值的，因为表达式 (i = y) 的执行总是先于该嵌入语句的执行。相反，变量 i 在第二个嵌入语句中不是明确赋值的，因为 x >= 0 可能被测试为 false，从而导致变量 i 未赋值。示例结束]

## 10.4.4.27 || 表达式

对于形式为 expr-first || expr-second 的表达式 expr：

- v 在 expr-first 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- v 在 expr-second 之前的明确赋值状态为明确赋值，当且仅当 v 在 expr-first 之后的状态为明确赋值或“false 表达式后明确赋值”。否则，它不是明确赋值。
- v 在 expr 之后的状态由以下规则确定：
    - 如果 v 在 expr-first 之后的状态为明确赋值，则 v 在 expr 之后的状态为明确赋值。
    - 否则，如果 v 在 expr-second 之后的状态为明确赋值，且 v 在 expr-first 之后的状态为“true 表达式后明确赋值”，则 v 在 expr 之后的状态为明确赋值。
    - 否则，如果 v 在 expr-second 之后的状态为明确赋值或“false 表达式后明确赋值”，则 v 在 expr 之后的状态为“false 表达式后明确赋值”。
    - 否则，如果 v 在 expr-first 之后的状态为“true 表达式后明确赋值”，且 v 在 expr-second 之后的状态为“true 表达式后明确赋值”，则 v 在 expr 之后的状态为“true 表达式后明确赋值”。
    - 否则，v 在 expr 之后的状态不是明确赋值。

[示例：在以下代码中

```
class A
{
    static void G(int x, int y) {
        int i;
        if (x >= 0 || (i = y) >= 0) {
            // i not definitely assigned
        } else {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```

在 if 语句的一个嵌入语句中，变量 i 被视为明确赋值，但在另一个嵌入语句中则不是。在方法 G 的 if 语句中，变量 i 在第二个嵌入语句中是明确赋值的，因为表达式 (i = y) 的执行总是先于该嵌入语句的执行。相反，变量 i 在第一个嵌入语句中不是明确赋值的，因为 x >= 0 可能被测试为 true，从而导致变量 i 未赋值。示例结束]

## 10.4.4.28 ! 表达式

对于形式为 ! expr-operand 的表达式 expr：

- v 在 expr-operand 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- v 在 expr 之后的状态由以下规则确定：
    - 如果 v 在 expr-operand 之后的状态为明确赋值，则 v 在 expr 之后的状态为明确赋值。
    - 否则，如果 v 在 expr-operand 之后的状态为“false 表达式后明确赋值”，则 v 在 expr 之后的状态为“true 表达式后明确赋值”。
    - 否则，如果 v 在 expr-operand 之后的状态为“true 表达式后明确赋值”，则 v 在 expr 之后的状态为“false 表达式后明确赋值”。
    - 否则，v 在 expr 之后的状态不是明确赋值。

## 10.4.4.29 ?? 表达式

对于形式为 expr-first ?? expr-second 的表达式 expr：

- v 在 expr-first 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- v 在 expr-second 之前的明确赋值状态与 v 在 expr-first 之后的明确赋值状态相同。
- v 在 expr 之后的状态由以下规则确定：
    - 如果 expr-first 是值为 null 的常量表达式（§12.20），则 v 在 expr 之后的状态与 v 在 expr-second 之后的状态相同。
    - 否则，v 在 expr 之后的状态与 v 在 expr-first 之后的明确赋值状态相同。

## 10.4.4.30 ?: 表达式

对于形式为 expr-cond ? expr-true : expr-false 的表达式 expr：

- v 在 expr-cond 之前的明确赋值状态与 v 在 expr 之前的状态相同。
- 如果 v 在 expr-cond 之后的状态为明确赋值或“true 表达式后明确赋值”，则 v 在 expr-true 之前的明确赋值状态为明确赋值。
- 如果 v 在 expr-cond 之后的状态为明确赋值或“false 表达式后明确赋值”，则 v 在 expr-false 之前的明确赋值状态为明确赋值。
- v 在 expr 之后的状态由以下规则确定：
    - 如果 expr-cond 是值为 true 的常量表达式（§12.20），则 v 在 expr 之后的状态与 v 在 expr-true 之后的状态相同。
    - 否则，如果 expr-cond 是值为 false 的常量表达式（§12.20），则 v 在 expr 之后的状态与 v 在 expr-false 之后的状态相同。
    - 否则，如果 v 在 expr-true 之后的状态为明确赋值，且 v 在 expr-false 之后的状态为明确赋值，则 v 在 expr 之后的状态为明确赋值。
    - 否则，v 在 expr 之后的状态不是明确赋值。

## 10.4.4.31 匿名函数

对于带有主体 body（块或表达式）的 lambda 表达式或匿名方法表达式 expr：

- 参数的明确赋值状态与命名方法的参数相同（§10.2.6、§10.2.7）。
- 外部变量 v 在 body 之前的明确赋值状态与 v 在 expr 之前的状态相同。也就是说，外部变量的明确赋值状态继承自匿名函数的上下文。
- 外部变量 v 在 expr 之后的明确赋值状态与 v 在 expr 之前的状态相同。

[示例：示例

```
delegate bool Filter(int i);
void F() {
    int max;
    // Error, max is not definitely assigned
    Filter f = (int n) => n < max;
    max = 5;
    DoWork(f);
}
```

会在编译时生成错误，因为在声明匿名函数的位置，max 不是明确赋值的。示例结束]

[示例：示例

```
delegate void D();
void F() {
    int n;
    D d = () => { n = 1; };
    d();
    // Error, n is not definitely assigned
    Console.WriteLine(n);
}
```



also generates a compile-time error since the assignment to n in the anonymous function has no effect on the definite assignment state of n outside the anonymous function. end example]

## 10.5 变量引用

变量引用是一个被归类为变量的表达式。变量引用表示一个存储位置，可以同时访问以获取当前值并存储新值。

```
variable-reference:
    expression
```

> [注意：在 C 和 C++ 中，变量引用被称为左值。end note]

## 10.6 变量引用的原子性

以下数据类型的读取和写入应是原子的：bool、char、byte、sbyte、short、ushort、uint、int、float 以及引用类型。此外，具有前述列表中底层类型的枚举类型的读取和写入也应是原子的。其他类型的读取和写入，包括 long、ulong、double 和 decimal 以及用户定义的类型，无需是原子的。除为此目的设计的库函数外，读-改-写操作的原子性不予保证，例如增量或减量的情况。

## 11. 转换

## 11.1 通用

转换会导致表达式被转换为特定类型，或被视为特定类型；在前一种情况下，转换可能涉及表示形式的更改。转换可以是隐式的或显式的，这决定了是否需要显式转换。[示例：例如，从类型 int 到类型 long 的转换是隐式的，因此 int 类型的表达式可以隐式地被视为 long 类型。相反的转换，从 long 类型到 int 类型是显式的，因此需要显式转换。

```
int a = 123;
long b = a;    // implicit conversion from int to long
int c = (int) b; // explicit conversion from long to int
```

end example] 一些转换由语言定义。程序也可以定义自己的转换 (§11.5)。

语言中的一些转换是从表达式到类型定义的，其他的是从类型到类型定义的。从类型进行的转换适用于所有具有该类型的表达式。[示例：

```
enum Color { Red, Blue, Green }
color c0 = 0; // The expression 0 converts implicitly to enum types
color c1 = (Color)1; // other int expressions need explicit conversion
string x = null; // Conversion from null expression (no type) to String
Func<int, int> square = x => x * x; // Conversion from lambda expression to delegate type
```

end example]

## 11.2 隐式转换

## 11.2.1 通用

以下转换被归类为隐式转换：

- 标识转换
- 隐式数值转换
- 隐式枚举转换
- 隐式引用转换
- 装箱转换
- 隐式动态转换
- 隐式类型参数转换
- 隐式常量表达式转换
- 用户定义的隐式转换
- 匿名函数转换
- 方法组转换
- 空字面量转换
- 隐式可空转换
- 提升的用户定义隐式转换

隐式转换可以在多种情况下发生，包括函数成员调用 (§12.6.6)、转换表达式 (§12.8.7) 和赋值 (§12.18)。

预定义的隐式转换总是成功，并且永远不会引发异常。[注意：设计良好的用户定义的隐式转换也应表现出这些特性。end note]

对于转换而言，类型 object 和 dynamic 被视为等价。

然而，动态转换 (§11.2.9 和 §11.3.7) 仅适用于类型为 dynamic 的表达式 (§9.2.4)。

### 11.2.2 标识转换

标识转换将任意类型转换为同一类型。此转换存在的一个原因是，可以说类型 T 或类型为 T 的表达式可转换为其自身。

由于 object 和 dynamic 被视为等价，因此 object 与 dynamic 之间存在标识转换，并且在将 dynamic 的所有出现替换为 object 后相同的构造类型之间也存在标识转换。

在大多数情况下，标识转换在运行时没有效果。然而，由于浮点运算可能以高于其类型规定的精度执行 (§9.3.7)，对其结果的赋值可能导致精度损失，而显式转换保证将精度降低到类型规定的精度。

### 11.2.3 隐式数值转换

隐式数值转换如下：

- 从 sbyte 到 short、int、long、float、double 或 decimal。
- 从 byte 到 short、ushort、int、uint、long、ulong、float、double 或 decimal。
- 从 short 到 int、long、float、double 或 decimal。
- 从 ushort 到 int、uint、long、ulong、float、double 或 decimal。
- 从 int 到 long、float、double 或 decimal。
- 从 uint 到 long、ulong、float、double 或 decimal。
- 从 long 到 float、double 或 decimal。
- 从 ulong 到 float、double 或 decimal。
- 从 char 到 ushort、int、uint、long、ulong、float、double 或 decimal。
- 从 float 到 double。

从 int、uint、long 或 ulong 到 float 的转换以及从 long 或 ulong 到 double 的转换可能会导致精度损失，但永远不会导致量级损失。其他隐式数值转换永远不会丢失任何信息。

没有预定义的到 char 类型的隐式转换，因此其他整型的值不会自动转换为 char 类型。

### 11.2.4 隐式枚举转换

隐式枚举转换允许十进制整数字面量 0（或 0L 等）转换为任何枚举类型以及底层类型为枚举类型的任何可空值类型。在后一种情况下，转换通过转换为底层枚举类型并包装结果来求值 (§9.3.11)。

### 11.2.5 隐式可空转换

隐式可空转换是源自隐式预定义转换的可空转换 (§11.6.1)。

### 11.2.6 空字面量转换

从空字面量到任何引用类型或可空值类型存在隐式转换。如果目标类型是引用类型，则此转换产生空引用，或给定可空值类型的空值 (§9.3.11)。

### 11.2.7 隐式引用转换

隐式引用转换如下：

- 从任何引用类型到 object 和 dynamic。
- 从任何类类型 S 到任何类类型 T，前提是 S 派生自 T。
- 从任何类类型 S 到任何接口类型 T，前提是 S 实现 T。
- 从任何接口类型 S 到任何接口类型 T，前提是 S 派生自 T。
- 从元素类型为 S_E 的任何数组类型 S 到元素类型为 T_E 的数组类型 T，前提是以下所有条件都为真：
  - S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同数量的维度。
  - 从 S_E 到 T_E 存在隐式引用转换。
- 从单维数组类型 S[] 到 System.Collections.Generic.IList<T>、System.Collections.Generic.IReadOnlyList<T> 及其基接口，前提是从 S 到 T 存在隐式标识或引用转换。
- 从任何数组类型到 System.Array 及其实现的接口。
- 从任何委托类型到 System.Delegate 及其实现的接口。
- 从空字面量 (§7.4.5.7) 到任何引用类型。
- 从任何引用类型到引用类型 T，如果它具有到引用类型 T0 的隐式标识或引用转换，并且 T0 具有到 T 的标识转换。
- 从任何引用类型到接口或委托类型 T，如果它具有到接口或委托类型 T0 的隐式标识或引用转换，并且 T0 可方差转换为 (§18.2.3.3) T。
- 涉及已知为引用类型的类型参数的隐式转换。有关涉及类型参数的隐式转换的更多详细信息，请参阅 §11.2.11。

隐式引用转换是可在编译时证明总是成功的引用类型之间的转换，因此在运行时不需要检查。

引用转换，无论是隐式还是显式，从不改变被转换对象的引用标识。[注意：换句话说，虽然引用转换可以更改引用的类型，但它永远不会更改所引用对象的类型或值。end note]

### 11.2.8 装箱转换

装箱转换允许值类型隐式转换为引用类型。以下装箱转换存在：

- 从任何值类型到类型 object。
- 从任何值类型到类型 System.ValueType。
- 从任何枚举类型到类型 System.Enum。
- 从任何非可空值类型到该非可空值类型实现的任何接口类型。
- 从任何非可空值类型到接口类型 I，前提是从该非可空值类型到另一个接口类型 I0 存在装箱转换，并且 I0 具有到 I 的标识转换。
- 从任何非可空值类型到接口类型 I，前提是从该非可空值类型到另一个接口类型 I0 存在装箱转换，并且 I0 可方差转换为 (§18.2.3.3) I。
- 从任何可空值类型到任何引用类型，前提是从该可空值类型的底层类型到该引用类型存在装箱转换。
- 从已知不是引用类型的类型参数到任何类型，前提是转换由 §11.2.11 允许。

对非可空值类型的值进行装箱包括分配一个对象实例并将值复制到该实例中。

对可空值类型的值进行装箱，如果它是空值（HasValue 为 false），则产生空引用，否则产生解包并装箱底层值的结果。

[注意：装箱过程可以想象为每个值类型都存在一个装箱类。例如，考虑一个实现接口 I 的结构体 S，其装箱类名为 S_Boxing。]



```
interface I
{
    void M();
}
struct S : I
{
    public void M() { ... }
}
sealed class S_Boxing : I
{
    S value;
    public S_Boxing(S value) {
        this.value = value;
    }
    public void M() {
        value.M();
    }
}
```

将类型为 S 的值 V 装箱现在相当于执行表达式 new S_Boxing(v) 并将 resulting instance 作为转换的目标类型的值返回。于是，下列语句

```
S s = new S();
object box = s;
```

可视为与以下类似：

```
S s = new S();
object box = new S_Boxing(s);
```

上面描述的想象中的装箱类型实际上并不存在。相反，类型为 S 的装箱值具有运行时类型 S，而使用 is 运算符进行运行时类型检查时，若右操作数为值类型，则会测试左操作数是否为右操作数的装箱版本。例如，

```
int i = 123;
object box = i;
if (box is int) {
    Console.Write("Box contains an int");
}
```

将在控制台输出字符串 "Box contains an int"。

装箱转换意味着复制被装箱的值。这与将引用类型转换为 object 类型不同，在后者中，值继续引用同一个实例，只是被视为派生程度更低的类型 object。例如，给定声明

```
struct Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

下列语句

```
Point p = new Point(10, 10);
object box = p;
p.x = 20;
Console.Write(((Point)box).x);
```

将在控制台输出值 10，因为将 p 赋给 box 时发生的隐式装箱操作会导致 p 的值被复制。如果 Point 被声明为类而不是结构体，则会输出值 20，因为 p 和 box 将引用同一个实例。

装箱类的类比不应被用作超过帮助理解装箱概念性工作原理的有用工具。本规范描述的行为与按此方式精确实现装箱所产生的行为之间存在诸多细微差异。end note]

### 11.2.9 隐式动态转换

从类型为 dynamic 的表达式到任意类型 T 存在隐式动态转换。该转换是动态绑定的（§12.3.3），这意味着在运行时会从表达式的运行时类型到 T 寻找隐式转换。如果找不到转换，则会抛出运行时异常。

这种隐式转换似乎违反了 §11.2 开头提出的建议，即隐式转换绝不应导致异常。然而，导致异常的并非转换本身，而是寻找转换的过程。运行时异常的风险是使用动态绑定的固有特性。如果不希望转换进行动态绑定，则可以先将表达式转换为 object，然后再转换为所需类型。

[示例：以下说明隐式动态转换：

```
object o = "object";
dynamic d = "dynamic";
string s1 = o; // Fails at compile-time - no conversion exists
string s2 = d; // Compiles and succeeds at run-time
int i = d; // Compiles but fails at run-time - no conversion exists
```

对 s2 和 i 的赋值都采用了隐式动态转换，其中操作的绑定被推迟到运行时。在运行时，会从 d 的运行时类型 —— string —— 到目标类型寻找隐式转换。可以找到到 string 的转换，但找不到到 int 的转换。end example]

### 11.2.10 隐式常量表达式转换

隐式常量表达式转换允许以下转换：

- 类型为 int 的常量表达式（§12.20）可以转换为类型 sbyte、byte、short、ushort、uint 或 ulong，前提是常量表达式的值在目标类型的范围内。
- 类型为 long 的常量表达式可以转换为类型 ulong，前提是常量表达式的值不为负。

### 11.2.11 涉及类型参数的隐式转换

对于已知为引用类型（§15.2.5）的类型参数 T，存在以下隐式引用转换（11.2.7）：

- 从 T 到其有效基类 C，从 T 到 C 的任何基类，以及从 T 到 C 实现的任何接口。
- 从 T 到 T 有效接口集中的接口类型 I，以及从 T 到 I 的任何基接口。
- 从 T 到类型参数 U，前提是 T 依赖于 U（§15.2.5）。[注：由于 T 已知为引用类型，在 T 的作用域内，U 的运行时类型始终为引用类型，即使在编译时 U 未知为引用类型。end note]
- 从 null 字面量（§7.4.5.7）到 T。

对于未知为引用类型（§15.2.5）的类型参数 T，涉及 T 的以下转换在编译时被视为装箱转换（11.2.8）。在运行时，如果 T 是值类型，则转换作为装箱转换执行。在运行时，如果 T 是引用类型，则转换作为隐式引用转换或恒等转换执行。

- 从 T 到其有效基类 C，从 T 到 C 的任何基类，以及从 T 到 C 实现的任何接口。[注：C 将是 System.Object、System.ValueType 或 System.Enum 中的一种类型（否则 T 将已知为引用类型）。end note]
- 从 T 到 T 有效接口集中的接口类型 I，以及从 T 到 I 的任何基接口。

对于未知为引用类型的类型参数 T，如果 T 依赖于 U，则存在从 T 到类型参数 U 的隐式转换。在运行时，如果 T 是值类型且 U 是引用类型，则转换作为装箱转换执行。在运行时，如果 T 和 U 都是值类型，则 T 和 U 必然是同一类型且不执行转换。在运行时，如果 T 是引用类型，则 U 必然也是引用类型，且转换作为隐式引用转换或恒等转换执行（§15.2.5）。

对于给定的类型参数 T，还存在以下隐式转换：

- 如果 T 具有到引用类型 S0 的隐式转换且 S0 具有到 S 的恒等转换，则从 T 到引用类型 S。在运行时，转换的执行方式与转换到 S0 相同。
- 如果 T 具有到接口类型 I0 的隐式转换，且 I0 可方差转换为 I（§18.2.3.3），则从 T 到接口类型 I。在运行时，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。

在所有情况下，规则确保转换仅在运行时从值类型到引用类型时才作为装箱转换执行。

### 11.2.12 用户定义的隐式转换

用户定义的隐式转换由可选的标准隐式转换组成，其后执行用户定义的隐式转换运算符，再后跟另一个可选的标准隐式转换。评估用户定义的隐式转换的确切规则在 §11.5.4 中描述。

### 11.2.13 匿名函数转换和方法组转换

匿名函数和方法组本身没有类型，但它们可以隐式转换为委托类型。此外，一些 lambda 表达式可以隐式转换为表达式树类型。匿名函数转换在 §11.7 中有更详细的描述，方法组转换在 §11.8 中描述。

## 11.3 显式转换

### 11.3.1 通用

以下转换被归类为显式转换：

- 所有隐式转换
- 显式数值转换
- 显式枚举转换
- 显式可空转换。
- 显式引用转换
- 显式接口转换
- 解箱转换
- 显式类型参数转换
- 显式动态转换

显式转换可以出现在强制转换表达式中（§12.8.7）。

显式转换的集合包括所有隐式转换。[注：这意味着允许冗余的强制转换表达式。end note]

不是隐式转换的显式转换是无法证明总是会成功的转换、已知可能丢失信息的转换，以及跨越类型域足够不同以值得显式表示的转换。



## 11.3.2 显式数值转换

显式数值转换是从一种数值类型到另一种数值类型，而隐式数值转换 (§11.2.3) 并不已存在的转换：

- 从 sbyte 到 byte、ushort、uint、ulong 或 char。
- 从 byte 到 sbyte 或 char。
- 从 short 到 sbyte、byte、ushort、uint、ulong 或 char。
- 从 ushort 到 sbyte、byte、short 或 char。
- 从 int 到 sbyte、byte、short、ushort、uint、ulong 或 char。
- 从 uint 到 sbyte、byte、short、ushort、int 或 char。
- 从 long 到 sbyte、byte、short、ushort、int、uint、ulong 或 char。
- 从 ulong 到 sbyte、byte、short、ushort、int、uint、long 或 char。
- 从 char 到 sbyte、byte 或 short。
- 从 float 到 sbyte、byte、short、ushort、int、uint、long、ulong、char 或 decimal。
- 从 double 到 sbyte、byte、short、ushort、int、uint、long、ulong、char 或 decimal。
- 从 decimal 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 double。

因为显式转换包括所有隐式和显式数值转换，所以始终可以使用强制转换表达式 (§12.8.7) 将任何数值类型转换为任何其他数值类型。

显式数值转换可能会丢失信息或可能导致抛出异常。显式数值转换的处理如下：

- 对于从一种整型到另一种整型的转换，处理取决于转换发生的溢出检查上下文 (§12.7.14)：
  - 在有检查的上下文中，如果源操作数的值在目标类型的范围内，则转换成功；但如果源操作数的值超出目标类型的范围，则抛出 System.OverflowException。
  - 在无检查的上下文中，转换总是成功，并按如下方式进行。
    - 如果源类型大于目标类型，则通过丢弃其“额外”的最显著位来截断源值。然后将结果视为目标类型的值。
    - 如果源类型小于目标类型，则源值会被符号扩展或零扩展，使其与目标类型大小相同。如果源类型是有符号的，则使用符号扩展；如果源类型是无符号的，则使用零扩展。然后将结果视为目标类型的值。
    - 如果源类型与目标类型大小相同，则源值被视为目标类型的值。
- 对于从 decimal 到整型的转换，源值会向零舍入到最近的整数值，并且该整数值成为转换的结果。如果所得整数值超出目标类型的范围，则抛出 System.OverflowException。
- 对于从 float 或 double 到整型的转换，处理取决于转换发生的溢出检查上下文 (§12.7.14)：
  - 在有检查的上下文中，转换按如下方式进行：
    - 如果操作数的值为 NaN 或无穷大，则抛出 System.OverflowException。
    - 否则，源操作数会向零舍入到最近的整数值。如果该整数值在目标类型的范围内，则该值是转换的结果。
  - 否则，抛出 System.OverflowException。
  - 在无检查的上下文中，转换总是成功，并按如下方式进行。
    - 如果操作数的值为 NaN 或无穷大，则转换的结果是目标类型的未指定值。
    - 否则，源操作数会向零舍入到最近的整数值。如果该整数值在目标类型的范围内，则该值是转换的结果。
    - 否则，转换的结果是目标类型的未指定值。
- 对于从 double 到 float 的转换，double 值会舍入到最近的 float 值。如果 double 值太小而无法表示为 float，则结果变为与该值符号相同的零。如果 double 值的大小太大而无法表示为 float，则结果变为与该值符号相同的无穷大。如果 double 值为 NaN，则结果也是 NaN。
- 对于从 float 或 double 到 decimal 的转换，源值会转换为 decimal 表示，并在需要时舍入到最接近的数字 (§9.3.8)。
  - 如果源值太小而无法表示为 decimal，则结果变为零，如果 decimal 支持有符号零值，则保留原始值的符号。
  - 如果源值的大小太大而无法表示为 decimal，或该值为无穷大，则结果为保留原始值符号的无穷大，如果 decimal 表示支持无穷大；否则抛出 System.OverflowException。
  - 如果源值为 NaN，则如果 decimal 表示支持 NaN，则结果为 NaN；否则抛出 System.OverflowException。
- 对于从 decimal 到 float 或 double 的转换，decimal 值会舍入到最近的 double 或 float 值。如果源值的大小太大而无法在目标类型中表示，或该值为无穷大，则结果为保留原始值符号的无穷大。如果源值为 NaN，则结果为 NaN。虽然此转换可能会丢失精度，但永远不会导致抛出异常。

[Note: decimal 类型不需要支持无穷大或 NaN 值，但可以支持；其范围可能小于 float 和 double 的范围，但并非 guaranteed。对于没有无穷大或 NaN 值且范围小于 float 的 decimal 表示，从 decimal 到 float 或 double 的转换结果永远不会是无穷大或 NaN。end note]

## 11.3.3 显式枚举转换

显式枚举转换是：

- 从 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal 到任何枚举类型。
- 从任何枚举类型到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal。
- 从任何枚举类型到任何其他枚举类型。

两个类型之间的显式枚举转换通过将参与的任何枚举类型视为该枚举类型的底层类型，然后在所得类型之间执行隐式或显式数值转换来处理。[Example: 给定底层类型为 int 的枚举类型 E，从 E 到 byte 的转换被处理为从 int 到 byte 的显式数值转换 (§11.3.2)，而从 byte 到 E 的转换被处理为从 byte 到 int 的隐式数值转换 (§11.2.3)。end example]

## 11.3.4 显式可空转换

显式可空转换是那些源自显式和隐式预定义转换的可空转换 (§11.6.1)。

## 11.3.5 显式引用转换

显式引用转换是：

- 从 object 和 dynamic 到任何其他引用类型。
- 从任何类类型 S 到任何类类型 T，前提是 S 是 T 的基类。
- 从任何类类型 S 到任何接口类型 T，前提是 S 未被密封并且 S 未实现 T。
- 从任何接口类型 S 到任何类类型 T，前提是 T 未被密封或 T 实现了 S。
- 从任何接口类型 S 到任何接口类型 T，前提是 S 未派生自 T。
- 从元素类型为 Se 的数组类型 S 到元素类型为 Te 的数组类型 T，前提是以下所有条件都为真：
  - S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同的维度数。
  - 从 Se 到 Te 存在显式引用转换。
- 从 System.Array 及其实现的接口到任何数组类型。
- 从单维数组类型 S[] 到 System.Collections.Generic.IList<T>、System.Collections.Generic.IReadOnlyList<T> 及其基接口，前提是存在从 S 到 T 的恒等转换或显式引用转换。
- 从 System.Collections.Generic.IList<S>、System.Collections.Generic.IReadOnlyList<S> 及其基接口到单维数组类型 T[]，前提是存在从 S 到 T 的恒等转换或显式引用转换。
- 从 System.Delegate 及其实现的接口到任何委托类型。
- 从引用类型 S 到引用类型 T，如果它从 S 到引用类型 T0 存在显式引用转换，并且从 T0 到 T 存在显式引用转换，并且存在从 T0 到 T 的恒等转换。
- 从引用类型 S 到接口或委托类型 T，如果存在从 S 到接口或委托类型 T0 的显式引用转换，并且 T0 可以方差转换为 T 或 T 可以方差转换为 T0 (§18.2.3)。
- 从 D<S1...Sn> 到 D<T1...Tn>，其中 D<X1...Xn> 是泛型委托类型，D<S1...Sn> 与 D<T1...Tn> 不兼容或不相同，并且对于 D 的每个类型参数 Xi 均满足以下条件：
  - 如果 Xi 是不变的，则 Si 与 Ti 相同。
  - 如果 Xi 是协变的，则存在从 Si 到 Ti 的恒等转换、隐式引用转换或显式引用转换。
  - 如果 Xi 是逆变的，则 Si 和 Ti 相同或均为引用类型。
- 涉及已知为引用类型的类型参数的显式转换。有关涉及类型参数的显式转换的更多详细信息，请参阅 §11.3.8。

显式引用转换是那些在运行时需要检查以确保其正确性的引用类型之间的转换。

要使显式引用转换在运行时成功，源操作数的值应为 null，或者源操作数引用的对象的类型应为可通过隐式引用转换 (§11.2.7) 转换为目标类型的类型。如果显式引用转换失败，则抛出 System.InvalidCastException。

引用转换，无论是隐式还是显式，从不改变正在转换的对象的引用同一性。[Note: 换句话说，虽然引用转换可以改变引用的类型，但它永远不会改变所引用对象的类型或值。end note]




### 11.3.6 拆箱转换

拆箱转换允许将*引用类型*显式转换为*值类型*。存在以下拆箱转换：

- 从类型 `object` 到任意*值类型*。
- 从类型 `System.ValueType` 到任意*值类型*。
- 从类型 `System.Enum` 到任意*枚举类型*。
- 从任意*接口类型*到实现该*接口类型*的任意*非 nullable 值类型*。
- 从任意*接口类型* I 到任意*非 nullable 值类型*，其中存在从*接口类型* I0 到该*非 nullable 值类型*的拆箱转换，并且 I 到 I0 存在标识转换。
- 从任意*接口类型* I 到任意*非 nullable 值类型*，其中存在从*接口类型* I0 到该*非 nullable 值类型*的拆箱转换，并且 I0 可变性转换为 I，或 I 可变性转换为 I0（§18.2.3.3）。
- 从任意*引用类型*到任意*可空值类型*，其中存在从*引用类型*到该*可空值类型*的基础*非 nullable 值类型*的拆箱转换。
- 从一个已知不属于值类型的类型参数到任意类型，前提是该转换符合 §11.3.8 的规定。

到*非 nullable 值类型*的拆箱操作，首先检查对象实例是否是给定*非 nullable 值类型*的装箱值，然后将值从该实例中复制出来。

拆箱为*可空值类型*时，如果源操作数为 *null*，则生成该*可空值类型*的 null 值；否则，将对象实例拆箱为该*可空值类型*的基础类型，并生成包装后的结果。

> [注：参照 §11.2.8 中描述的假想装箱类，将对象箱拆箱为*值类型* S 的拆箱转换，相当于执行表达式 `((S_Boxing)box).value`。因此，语句
>
> ```
> object box = new S();
> S s = (S)box;
> ```
>
> 在概念上对应于
>
> ```
> object box = new S_Boxing(new S());
> S s = ((S_Boxing)box).value;
> ```
>
> 注结束]

要使到给定*非 nullable 值类型*的拆箱转换在运行时成功，源操作数的值必须是对该*非 nullable 值类型*的装箱值的引用。如果源操作数为 *null*，则会引发 *System.NullReferenceException*。如果源操作数是对不兼容对象的引用，则会引发 *System.InvalidCastException*。

要使到给定*可空值类型*的拆箱转换在运行时成功，源操作数的值必须为 *null*，或必须是对该*可空值类型*的基础*非 nullable 值类型*的装箱值的引用。如果源操作数是对不兼容对象的引用，则会引发 *System.InvalidCastException*。

### 11.3.7 显式动态转换

存在从类型为 *dynamic* 的表达式到任意类型 T 的显式动态转换。该转换会进行动态绑定（§12.3.3），这意味着将在运行时尝试将表达式的运行时类型显式转换为 T。如果找不到转换，则会引发运行时异常。

如果不希望对该转换进行动态绑定，可以先将表达式转换为 *object*，然后再转换为所需类型。

[示例：假设定义了以下类：

```
class C
{
    int i;
    public C(int i) { this.i = i; }
    public static explicit operator C(string s)
    {
        return new C(int.Parse(s));
    }
}
```

以下示例演示了显式动态转换：

```
object o = "1";
dynamic d = "2";
var c1 = (C)o; // Compiles, but explicit reference conversion fails
var c2 = (C)d; // Compiles and user defined conversion succeeds
```

在编译时，o 到 C 的最佳转换被确定为显式引用转换。该转换在运行时失败，因为 `"1"` 实际上并不是 C。然而，d 到 C 的转换是显式动态转换，会被推迟到运行时执行；此时可以找到从 d 的运行时类型（即 string）到 C 的用户定义转换，并且转换成功。示例结束]

### 11.3.8 涉及类型参数的显式转换

对于已知为引用类型（§15.2.5）的类型参数 T，存在以下显式引用转换（§11.3.5）：

- 从 T 的有效基类 C 到 T，以及从 C 的任意基类到 T。
- 从任意接口类型到 T。
- 从 T 到任意接口类型 I，前提是 T 到 I 尚不存在隐式引用转换。
- 从类型参数 U 到 T，前提是 T 依赖于 U（§15.2.5）。[注：由于已知 T 是引用类型，因此在 T 的作用域内，U 的运行时类型始终是引用类型，即使在编译时并不知道 U 是引用类型。注结束]

对于未知是否为引用类型（§15.2.5）的类型参数 T，以下涉及 T 的转换在编译时被视为拆箱转换（§11.3.6）。在运行时，如果 T 是值类型，则该转换按拆箱转换执行；在运行时，如果 T 是引用类型，则该转换按显式引用转换或标识转换执行。

- 从 T 的有效基类 C 到 T，以及从 C 的任意基类到 T。[注：C 将是 System.Object、System.ValueType 或 System.Enum 这几种类型之一（否则 T 将已知为引用类型）。注结束]
- 从任意接口类型到 T。

对于未知是否为引用类型（§15.2.5）的类型参数 T，存在以下显式转换：

- 从 T 到任意接口类型 I，前提是 T 到 I 尚不存在隐式转换。该转换由以下步骤组成：先将 T 隐式装箱转换（§11.2.8）为 object，然后将 object 显式引用转换为 I。在运行时，如果 T 是值类型，则该转换按装箱转换后接显式引用转换执行；如果 T 是引用类型，则该转换按显式引用转换执行。
- 从类型参数 U 到 T，前提是 T 依赖于 U（§15.2.5）。在运行时，如果 T 是值类型且 U 是引用类型，则该转换按拆箱转换执行。在运行时，如果 T 和 U 都是值类型，则 T 和 U 必然是同一类型，不执行任何转换。在运行时，如果 T 是引用类型，则 U 也必然是引用类型，并且该转换按显式引用转换或标识转换执行。

在所有情况下，这些规则都确保：当且仅当运行时的转换是从引用类型到值类型时，该转换才按拆箱转换执行。

上述规则不允许从不受约束的类型参数直接显式转换为非接口类型，这一点可能令人意外。制定此规则的原因是避免混淆，并明确此类转换的语义。[示例：考虑以下声明：

```
class X<T>
{
    public static long F(T t) {
        return (long)t;        // Error
    }
}
```

如果允许将 t 直接显式转换为 long，人们可能很容易预期 `X<int>.F(7)` 会返回 7L。然而，实际并非如此，因为只有在绑定时已知类型为数值类型时，才会考虑标准数值转换。为了明确语义，上面的示例必须改写为：

```
class X<T>
{
    public static long F(T t) {
        return (long)(object)t;    // ok, but will only work when T is long
    }
}
```

现在这段代码可以编译，但执行 `X<int>.F(7)` 时会在运行时引发异常，因为装箱后的 int 不能直接转换为 long。示例结束]

### 11.3.9 用户定义的显式转换

用户定义的显式转换由以下部分组成：可选的标准显式转换，随后执行用户定义的隐式或显式转换运算符，再随后执行另一个可选的标准显式转换。评估用户定义显式转换的确切规则见 §11.5.5。

## 11.4 标准转换

### 11.4.1 概述

标准转换是可作为用户定义转换一部分发生的预定义转换。

### 11.4.2 标准隐式转换

以下隐式转换被归类为标准隐式转换：

- 标识转换（§11.2.2）
- 隐式数值转换（§11.2.3）
- 隐式可空转换（§11.2.5）
- null 字面量转换（§11.2.6）
- 隐式引用转换（§11.2.7）
- 装箱转换（§11.2.8）
- 隐式常量表达式转换（§11.2.10）
- 涉及类型参数的隐式转换（§11.2.11）

标准隐式转换明确不包括用户定义的隐式转换。

### 11.4.3 标准显式转换

标准显式转换包括所有标准隐式转换，以及显式转换中存在反向标准隐式转换的那一部分。[注：换句话说，如果一个标准



如果从类型 A 到类型 B 存在隐式转换，则从类型 A 到类型 B 以及从类型 B 到类型 A 都存在标准显式转换。 end note]

## 11.5 用户定义的转换

### 11.5.1 通用

C# 允许通过 **用户定义的转换** 来扩展预定义的隐式和显式转换。用户定义的转换是通过在类和结构体类型中声明转换运算符 (§15.10.4) 引入的。

### 11.5.2 允许的用户定义转换

C# 只允许声明某些用户定义的转换。特别是，不可能重新定义已存在的隐式或显式转换。

对于给定的源类型 S 和目标类型 T，如果 S 或 T 是可空值类型，则令 S₀ 和 T₀ 引用其底层类型，否则 S₀ 和 T₀ 分别等于 S 和 T。仅当以下所有条件都为真时，类或结构体才允许声明从源类型 S 到目标类型 T 的转换：

- S₀ 和 T₀ 是不同的类型。
- S₀ 或 T₀ 中的一个是运算符声明所在的类或结构体类型。
- S₀ 和 T₀ 都不是 *接口类型*。
- 排除用户定义的转换，从 S 到 T 或从 T 到 S 不存在转换。

适用于用户定义转换的限制在 §15.10.4 中指定。

### 11.5.3 用户定义转换的求值

用户定义的转换将可能具有源类型的 **源表达式** 转换为另一种类型，称为 **目标类型**。用户定义转换的求值集中于为源表达式和目标类型找到 **最具体的** 用户定义转换运算符。此确定分为几个步骤：

- 找到将考虑用户定义转换运算符的类和结构体的集合。此集合由源类型及其基类（如果源类型存在）以及目标类型及其基类组成。为此目的，假定只有类和结构体可以声明用户定义运算符，并且非类类型没有基类。此外，如果源类型或目标类型是可空值类型，则使用其底层类型代替。
- 从该类型集合中，确定哪些用户定义和提升的转换运算符适用。对于转换运算符要适用，必须能够执行从源表达式到运算符的操作数类型的标准转换 (§11.4)，并且必须能够执行从运算符的结果类型到目标类型的标准转换。
- 从适用的用户定义运算符集合中，确定哪个运算符无歧义地是最具体的。总体而言，最具体的运算符是其操作数类型“最接近”源表达式且其结果类型“最接近”目标类型的运算符。用户定义的转换运算符优先于提升的转换运算符。确定最具体的用户定义转换运算符的确切规则在以下小节中定义。

一旦确定了最具体的用户定义转换运算符，用户定义转换的实际执行涉及最多三个步骤：

- 首先，如果需要，执行从源表达式到用户定义或提升的转换运算符的操作数类型的标准转换。
- 接下来，调用用户定义或提升的转换运算符以执行转换。
- 最后，如果需要，执行从用户定义转换运算符的结果类型到目标类型的标准转换。

用户定义转换的求值永远不会涉及多于一个用户定义或提升的转换运算符。换句话说，从类型 S 到类型 T 的转换永远不会首先执行从 S 到 X 的用户定义转换，然后再执行从 X 到 T 的用户定义转换。

- 用户定义隐式或显式转换的求值的精确定义在以下小节中给出。定义使用了以下术语：
- 如果从类型 A 到类型 B 存在标准隐式转换 (§11.4.2)，并且 A 和 B 都不是 *接口类型*，则称 A **被包含于** B，且 B **包含** A。
- 如果从表达式 E 到类型 B 存在标准隐式转换 (§11.4.2)，并且 B 和 E 的类型（如果有）都不是 *接口类型*，则称 E **被包含于** B，且 B **包含** E。
- 某组类型中的 **最包容的类型** 是包含该集合中所有其他类型的那一个类型。如果没有单个类型包含所有其他类型，则该集合没有最包容的类型。更直观地说，最包容的类型是该集合中的“最大”类型——可以隐式转换为该类型的每个其他类型。
- 某组类型中的 **最被包含的类型** 是被该集合中所有其他类型所包含的那一个类型。如果没有单个类型被所有其他类型所包含，则该集合没有最被包含的类型。更直观地说，最被包含的类型是该集合中的“最小”类型——可以隐式转换为每个其他类型的那一个类型。

### 11.5.4 用户定义的隐式转换

从表达式 E 到类型 T 的用户定义隐式转换按如下方式处理：

- 确定类型 S、S₀ 和 T₀。
  - 如果 E 有类型，则令 S 为该类型。
  - 如果 S 或 T 是可空值类型，则令 Sᵤ 和 Tᵤ 为其底层类型，否则令 Sᵤ 和 Tᵤ 分别为 S 和 T。
  - 如果 Sᵤ 或 Tᵤ 是类型参数，则令 S₀ 和 T₀ 为其有效基类，否则令 S₀ 和 T₀ 分别为 Sᵤ 和 Tᵤ。
- 找到将考虑用户定义转换运算符的类型集合 D。此集合由 S₀（如果 S₀ 存在且为类或结构体）、S₀ 的基类（如果 S₀ 存在且为类）以及 T₀（如果 T₀ 为类或结构体）组成。仅当不存在到集合中已包含的另一类型的恒等转换时，才将类型添加到集合 D。
- 找到适用的用户定义和提升的转换运算符集合 U。此集合由 D 中的类或结构体声明的用户定义和提升的隐式转换运算符组成，这些运算符从包含 E 的类型转换为被 T 包含的类型。如果 U 为空，则转换未定义并发生编译时错误。
- 找到 U 中运算符的最具体源类型 Sₓ：
  - 如果 S 存在并且 U 中的任何运算符从 S 转换，则 Sₓ 为 S。
  - 否则，Sₓ 为 U 中运算符的源类型组合集合中的最被包含的类型。如果找不到唯一的最被包含的类型，则转换不明确并发生编译时错误。
- 找到 U 中运算符的最具体目标类型 Tₓ：
  - 如果 U 中的任何运算符转换为 T，则 Tₓ 为 T。
  - 否则，Tₓ 为 U 中运算符的目标类型组合集合中的最包容的类型。如果找不到唯一的最包容的类型，则转换不明确并发生编译时错误。
- 找到最具体的转换运算符：
  - 如果 U 包含恰好一个从 Sₓ 到 Tₓ 的用户定义转换运算符，则此为最具体的转换运算符。
  - 否则，如果 U 包含恰好一个从 Sₓ 到 Tₓ 的提升转换运算符，则此为最具体的转换运算符。
  - 否则，转换不明确并发生编译时错误。
- 最后，应用转换：
  - 如果 E 尚不具有类型 Sₓ，则执行从 E 到 Sₓ 的标准隐式转换。
  - 调用最具体的转换运算符将 Sₓ 转换为 Tₓ。
  - 如果 Tₓ 不是 T，则执行从 Tₓ 到 T 的标准隐式转换。

如果从类型 S 的变量到 T 存在用户定义隐式转换，则从类型 S 到类型 T 存在用户定义隐式转换。

### 11.5.5 用户定义的显式转换

从表达式 E 到类型 T 的用户定义显式转换按如下方式处理：

- 确定类型 S、S₀ 和 T₀。
  - 如果 E 有类型，则令 S 为该类型。
  - 如果 S 或 T 是可空值类型，则令 Sᵤ 和 Tᵤ 为其底层类型，否则令 Sᵤ 和 Tᵤ 分别为 S 和 T。
  - 如果 Sᵤ 或 Tᵤ 是类型参数，则令 S₀ 和 T₀ 为其有效基类，否则令 S₀ 和 T₀ 分别为 Sᵤ 和 Tᵤ。
- 找到将考虑用户定义转换运算符的类型集合 D。此集合由 S₀（如果 S₀ 存在且为类或结构体）、S₀ 的基类（如果 S₀ 存在且为类）、T₀（如果 T₀ 为类或结构体）以及 T₀ 的基类（如果 T₀ 为类）组成。仅当不存在到集合中已包含的另一类型的恒等转换时，才将类型添加到集合 D。
- 找到适用的用户定义和提升的转换运算符集合 U。此集合由 D 中的类或结构体声明的用户定义和提升的隐式或显式转换运算符组成，这些运算符从包含 E 的类型或被 S 包含的类型（如果存在）转换为包含或被 T 包含的类型。如果 U 为空，则转换未定义并发生编译时错误。
- 找到 U 中运算符的最具体源类型 Sₓ：
  - 如果 S 存在并且 U 中的任何运算符从 S 转换，则 Sₓ 为 S。
  - 否则，如果 U 中的任何运算符从包含 E 的类型转换，则 Sₓ 为这些运算符的源类型组合集合中的最被包含的类型。如果找不到最被包含的类型，则转换不明确并发生编译时错误。
  - 否则，Sₓ 为 U 中运算符的源类型组合集合中的最包容的类型。如果找不到唯一的最包容的类型，则转换不明确并发生编译时错误。
- 找到 U 中运算符的最具体目标类型 Tₓ：
  - 如果 U 中的任何运算符转换为 T，则 Tₓ 为 T。
  - 否则，如果 U 中的任何运算符转换为被 T 包含的类型，则 Tₓ 为这些运算符的目标类型组合集合中的最包容的类型。如果找不到唯一的最包容的类型，则转换不明确并发生编译时错误。




否则，Tx 是 U 中运算符的目标类型集合中包含范围最广的类型。如果找不到包含范围最广的类型，则转换不明确并会发生编译时错误。

- 查找最具体的转换运算符：
  - 如果 U 恰好包含一个从 Sx 转换到 Tx 的用户定义转换运算符，则此为最具体的转换运算符。
  - 否则，如果 U 恰好包含一个从 Sx 转换到 Tx 的提升转换运算符，则此为最具体的转换运算符。
  - 否则，转换不明确并会发生编译时错误。

- 最后，应用转换：
  - 如果 E 尚不具有类型 Sx，则执行从 E 到 Sx 的标准显式转换。
  - 调用最具体的用户定义转换运算符将 Sx 转换为 Tx。
  - 如果 Tx 不是 T，则执行从 Tx 到 T 的标准显式转换。

如果存在从类型 S 的变量到 T 的用户定义显式转换，则存在从类型 S 到类型 T 的用户定义显式转换。

## 11.6 涉及可空类型的转换

### 11.6.1 可空转换

可空转换允许对非可空值类型操作的预定义转换也适用于这些类型的可空形式。对于从非可空值类型 S 到非可空值类型 T 的每种预定义隐式或显式转换（§11.2.2、§11.2.3、§11.2.4、§11.2.10、§11.3.2 和 §11.3.3），存在以下可空转换：

- 从 S? 到 T? 的隐式或显式转换
- 从 S 到 T? 的隐式或显式转换
- 从 S? 到 T 的显式转换

可空转换本身被归类为隐式或显式转换。某些可空转换被归类为标准转换，并且可以在用户定义转换的一部分中出现。具体来说，所有隐式可空转换都被归类为标准隐式转换（§11.4.2），而满足 §11.4.3 要求的那些显式可空转换被归类为标准显式转换。基于从 S 到 T 的底层转换对可空转换的求值如下进行：

- 如果可空转换是从 S? 到 T?：
  - 如果源值为 null（HasValue 属性为 false），结果为类型 T? 的 null 值。
  - 否则，转换被求值为空包从 S? 到 S，随后是 S 到 T 的底层转换，随后是从 T 到 T? 的包装。
- 如果可空转换是从 S 到 T?，则转换被求值为空底层转换从 S 到 T，随后是从 T 到 T? 的包装。
- 如果可空转换是从 S? 到 T，则转换被求值为空包从 S? 到 S，随后是 S 到 T 的底层转换。

### 11.6.2 提升转换

给定一个从非可空值类型 S 到非可空值类型 T 的用户定义转换运算符，存在一个从 S? 到 T? 的提升转换运算符。此提升转换运算符执行从 S? 到 S 的解包，随后是 S 到 T 的用户定义转换，随后是从 T 到 T? 的包装，除了 null 值的 S? 直接转换为 null 值的 T?。提升转换运算符具有与其底层用户定义转换运算符相同的隐式或显式分类。

## 11.7 匿名函数转换

### 11.7.1 通用

匿名方法表达式或 lambda 表达式被归类为匿名函数（§12.16）。该表达式没有类型，但可以隐式转换为兼容的委托类型。某些 lambda 表达式也可以隐式转换为兼容的表达式树类型。

为简洁起见，本小节使用任务类型 Task 和 Task<T> 的简写形式（§15.15.1）。

具体来说，匿名函数 F 与委托类型 D 兼容，前提是：

- 如果 F 包含匿名函数签名，则 D 和 F 具有相同数量的参数。
- 如果 F 不包含匿名函数签名，则 D 可以有零个或多个任意类型的参数，只要 D 的参数没有 out 参数修饰符即可。
- 如果 F 具有显式类型的参数列表，则 D 中的每个参数与 F 中对应参数具有相同的类型和修饰符。
- 如果 F 具有隐式类型的参数列表，则 D 没有 ref 或 out 参数。
- 如果 F 的主体是一个表达式，并且 D 具有 void 返回类型或 F 为 async 且 D 具有返回类型 Task，则当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是一个有效的表达式（关于 §12），该表达式可作为语句表达式（§13.7）被允许。
- 如果 F 的主体是一个语句块，并且 D 具有 void 返回类型或 F 为 async 且 D 具有返回类型 Task，则当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是一个有效的语句块（关于 §13.3），其中没有 return 语句指定表达式。
- 如果 F 的主体是一个表达式，并且 F 为非 async 且 D 具有非 void 返回类型 T，或 F 为 async 且 D 具有返回类型 Task<T>，则当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是一个有效的表达式（关于 §12），该表达式可隐式转换为 T。
- 如果 F 的主体是一个语句块，并且 F 为非 async 且 D 具有非 void 返回类型 T，或 F 为 async 且 D 具有返回类型 Task<T>，则当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是一个有效的语句块（关于 §13.3），其末端不可达，其中每个 return 语句指定一个可隐式转换为 T 的表达式。

[示例：以下示例说明了这些规则：

```csharp
delegate void D(int x);
D d1 = delegate { }; // Ok
D d2 = delegate() { }; // Error, signature mismatch
D d3 = delegate(long x) { }; // Error, signature mismatch
D d4 = delegate(int x) { }; // Ok
D d5 = delegate(int x) { return; }; // Ok
D d6 = delegate(int x) { return x; }; // Error, return type mismatch
delegate void E(out int x);
E e1 = delegate { }; // Error, E has an out parameter
E e2 = delegate(out int x) { x = 1; }; // Ok
E e3 = delegate(ref int x) { x = 1; }; // Error, signature mismatch
delegate int P(params int[] a);
P p1 = delegate { }; // Error, end of block reachable
P p2 = delegate { return; }; // Error, return type mismatch
P p3 = delegate { return 1; }; // Ok
P p4 = delegate { return "Hello"; }; // Error, return type mismatch
P p5 = delegate(int[] a) { return a[0]; }; // Ok
P p6 = delegate(params int[] a) { return a[0]; }; // Error, params modifier
P p7 = delegate(int[] a) { if (a.Length > 0) return a[0]; return "Hello"; }; // Error, return type mismatch
delegate object Q(params int[] a);
Q q1 = delegate(int[] a) { if (a.Length > 0) return a[0]; return "Hello"; }; // Ok
```

示例结束

[示例：以下示例使用通用委托类型 Func<A,R>，它表示一个接受类型 A 的参数并返回类型 R 的值 的函数：

```csharp
delegate R Func<A,R>(A arg);
```

在赋值中

```csharp
Func<int,int> f1 = x => x + 1; // Ok
Func<int,double> f2 = x => x + 1; // Ok
Func<double,int> f3 = x => x + 1; // Error
Func<int, Task<int>> f4 = async x => x + 1; // Ok
```

每个匿名函数的参数和返回类型都是从匿名函数被赋值的变量的类型确定的。第一个赋值成功地将匿名函数转换为委托类型 Func<int,int>，因为当 x 被赋予类型 int 时，x + 1 是一个有效表达式，可隐式转换为类型 int。同样，第二个赋值成功地将匿名函数转换为委托类型 Func<int,double>，因为 x + 1 的结果（类型为 int）可隐式转换为类型 double。然而，第三个赋值是编译时错误，因为当 x 被赋予类型 double 时，x + 1 的结果（类型为 double）不可隐式转换为类型 int。第四个赋值成功地将匿名 async 函数转换为委托类型 Func<int, Task<int>>，因为 x + 1 的结果（类型为 int）可隐式转换为 async lambda 的有效返回类型 int，而该 lambda 的返回类型为 Task<int>。示例结束

lambda 表达式 F 与表达式树类型 Expression<D> 兼容，如果 F 与委托类型 D 兼容。这不适用于匿名方法，仅适用于 lambda 表达式。

某些 lambda 表达式不能转换为表达式树类型：即使转换存在，它也会在编译时失败。如果 lambda 表达式满足以下情况，则会出现这种情况：

- 具有块主体
- 包含简单或复合赋值运算符
- 包含动态绑定表达式
- 为 async


匿名函数可能会影响重载解析，并参与类型推断。有关详细信息，请参阅§12.6。

## 11.7.2 将匿名函数转换为委托类型的求值

将匿名函数转换为委托类型会生成一个委托实例，该实例引用匿名函数以及在求值时处于活动状态的（可能为空的）捕获外部变量集合。当委托被调用时，匿名函数的主体将被执行。主体中的代码使用委托引用的捕获外部变量集合执行。委托创建表达式（§12.7.11.6）可作为将匿名方法转换为委托类型的替代语法。

由匿名函数生成的委托的调用列表包含单个条目。委托的确切目标对象和目标方法未指定。特别是，委托的目标对象是 null、封闭函数成员的 this 值还是其他对象，均未指定。

将语义相同的匿名函数（具有相同的（可能为空的）捕获外部变量实例集合）转换为相同的委托类型时，允许（但不要求）返回相同的委托实例。此处语义相同是指在所有情况下，给定相同的参数，匿名函数的执行将产生相同的效果。该规则允许对如下代码进行优化。

```
delegate double Function(double x);
class Test
{
    static double[] Apply(double[] a, Function f) {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }

    static void F(double[] a, double[] b) {
        a = Apply(a, (double x) => Math.Sin(x));
        b = Apply(b, (double y) => Math.Sin(y));
        ...
    }
}
```

由于这两个匿名函数委托具有相同的（空）捕获外部变量集合，并且由于匿名函数语义相同，因此编译器允许委托引用相同的目标方法。事实上，编译器允许从两个匿名函数表达式返回完全相同的委托实例。

## 11.7.3 将匿名函数转换为表达式树类型的求值

将匿名函数转换为表达式树类型会生成一个表达式树（§9.6）。更精确地说，匿名函数转换的求值会生成一个对象结构，该结构表示匿名函数本身的结构。表达式树的精确结构以及创建它的确切过程都是实现定义的。

## 11.8 方法组转换

从方法组（§12.2）到兼容的委托类型（§20.4）存在隐式转换。如果 D 是委托类型，且 E 是被分类为方法组的表达式，则 D 与 E 兼容当且仅当 E 包含至少一个方法，该方法在其常规形式（§12.6.4.2）下适用于任何参数列表（§12.6.2），其类型和修饰符与 D 的参数类型和修饰符匹配，如下所述。

从方法组 E 到委托类型 D 的转换的编译时应用如下所述。请注意，从 E 到 D 的隐式转换的存在并不保证转换的编译时应用能够在没有错误的情况下成功。

- 选择单个方法 M，对应于形式为 E(A) 的方法调用（§12.7.6.2），并进行以下修改：
  - 参数列表 A 是表达式列表，每个表达式被分类为变量，并且具有 D 的形式参数列表中对应参数的类型和修饰符（ref 或 out）——除 dynamic 类型的参数外，对应表达式的类型为 object 而不是 dynamic。
  - 考虑的候选方法仅限于在其常规形式下适用且不省略任何可选参数的方法（§12.6.4.2）。因此，如果候选方法仅在其扩展形式下适用，或者其一个或多个可选参数在 D 中没有对应参数，则忽略该候选方法。
- 如果 §12.7.6.2 的算法产生具有与 D 相同参数数量的单个最佳方法 M，则认为存在转换。
- 即使转换存在，如果所选方法 M 与委托类型 D 不兼容（§20.4），仍会发生编译时错误。
- 如果所选方法 M 是实例方法，则与 E 关联的实例表达式决定委托的目标对象。
- 如果所选方法 M 是通过在实例表达式上进行成员访问而表示的扩展方法，则该实例表达式决定委托的目标对象。
- 转换的结果是类型为 D 的值，即引用所选方法和目标对象的委托。

[示例：以下演示方法组转换：

```
delegate string D1(object o);
delegate object D2(string s);
delegate object D3();
delegate string D4(object o, params object[] a);
delegate string D5(int i);
class Test
{
    static string F(object o) {...}
    static void G() {
        D1 d1 = F;        // Ok
        D2 d2 = F;        // Ok
        D3 d3 = F;        // Error - not applicable
        D4 d4 = F;        // Error - not applicable in normal form
        D5 d5 = F;        // Error - applicable but not compatible
    }
}
```

将 d1 赋值隐式地将方法组 F 转换为类型为 D1 的值。

将 d2 赋值展示了如何创建指向具有较少派生（逆变）参数类型和更派生（协变）返回类型的方法的委托。

将 d3 赋值展示了如果方法不适用则不存在转换的情况。

将 d4 赋值展示了方法必须在其常规形式下适用。

将 d5 赋值展示了委托和方法参数类型和返回类型仅允许对引用类型不同。

结束示例]

与所有其他隐式和显式转换一样，可以使用强制转换运算符显式执行特定转换。[示例：因此，示例

```
object obj = new EventHandler(myDialog.OkClick);
```

可以改写为

```
object obj = (EventHandler)myDialog.OkClick;
```

结束示例]

方法组转换可以引用泛型方法，要么在 E 中显式指定类型参数，要么通过类型推断（§12.6.3）。如果使用类型推断，则委托的参数类型用作推断过程中的参数类型。委托的返回类型不用于推断。无论类型参数是指定还是推断，它们都是方法组转换过程的一部分；这些是调用结果委托时用于调用目标方法的类型参数。[示例：

```
delegate int D(string s, int i);
delegate int E();
class X
{
    public static T F<T>(string s, T t) {...}
    public static T G<T>() {...}
    static void Main() {
        D d1 = F<int>;   // Ok, type argument given explicitly
        D d2 = F;        // Ok, int inferred as type argument
        E e1 = G<int>;   // Ok, type argument given explicitly
        E e2 = G;        // Error, cannot infer from return type
    }
}
```

结束示例]

方法组可能会影响重载解析，并参与类型推断。有关详细信息，请参阅§12.6。

方法组转换的运行时求值按如下方式进行：

- 如果在编译时选定的方法是实例方法，或者是通过作为实例方法访问的扩展方法，则委托的目标对象由与 E 关联的实例表达式确定：
  - 对实例表达式进行求值。如果此求值导致异常，则不执行后续步骤。
  - 如果实例表达式为引用类型，则实例表达式计算得到的值成为目标对象。如果所选方法是实例方法且目标对象为 null，则抛出 System.NullReferenceException 且不执行后续步骤。
  - 如果实例表达式为值类型，则执行装箱操作（§11.2.8）将值转换为对象，并且该对象成为目标对象。
- 否则，所选方法属于静态方法调用，委托的目标对象为 null。
- 获取委托类型 D 的委托实例，其中包含对编译时确定的方法的引用以及对上述计算得到的目标对象的引用，如下所示：
  - 允许（但不要求）转换使用已包含这些引用的现有委托实例。



- 如果未重用现有实例，则创建新实例（§20.5）。如果没有足够的内存可用于分配新实例，则引发 System.OutOfMemoryException。否则，使用给定的引用初始化该实例。

## 12. 表达式

### 12.1 概述

表达式是运算符和操作数的序列。本条款定义表达式的语法、操作数和运算符的求值顺序以及表达式的含义。

### 12.2 表达式分类

### 12.2.1 概述

表达式分类为以下之一：

- 值。每个值都有一个关联类型。
- 变量。每个变量都有一个关联类型，即该变量的声明类型。
- 命名空间。具有此分类的表达式只能出现在成员访问（§12.7.5）的左侧。在任何其他上下文中，分类为命名空间的表达式会导致编译时错误。
- 类型。具有此分类的表达式只能出现在成员访问（§12.7.5）的左侧。在任何其他上下文中，分类为类型的表达式会导致编译时错误。
- 方法组，它是成员查找（§12.5）产生的一组重载方法。方法组可以具有关联的实例表达式和关联的类型实参列表。当调用实例方法时，计算实例表达式的结果将成为由 this（§12.7.8）表示的实例。方法组允许出现在调用表达式（§12.7.6）或委托创建表达式（§12.7.11.6）中，并且可以隐式转换为兼容的委托类型（§11.8）。在任何其他上下文中，分类为方法组的表达式会导致编译时错误。
- null 字面量。具有此分类的表达式可以隐式转换为引用类型或可为 null 的值类型。
- 匿名函数。具有此分类的表达式可以隐式转换为兼容的委托类型或表达式树类型。
- 属性访问。每个属性访问都有相关联的类型，即属性的类型。此外，属性访问可以具有关联的实例表达式。当调用实例属性访问的访问器（get 或 set 块）时，计算实例表达式的结果将成为由 this（§12.7.8）表示的实例。
- 事件访问。每个事件访问都有相关联的类型，即事件的类型。此外，事件访问可以具有关联的实例表达式。事件访问可以出现在 += 和 -= 运算符（§12.18.4）的左侧操作数。在任何其他上下文中，分类为事件访问的表达式会导致编译时错误。当调用实例事件访问的访问器（add 或 remove 块）时，计算实例表达式的结果将成为由 this（§12.7.8）表示的实例。
- 索引器访问。每个索引器访问都有相关联的类型，即索引器的元素类型。此外，索引器访问具有关联的实例表达式和关联的实参列表。当调用索引器访问的访问器（get 或 set 块）时，计算实例表达式的结果将成为由 this（§12.7.8）表示的实例，而计算实参列表的结果将成为调用的形参列表。
- Nothing。当表达式是对返回类型为 void 的方法的调用时，会出现这种情况。分类为 Nothing 的表达式仅在语句表达式（§13.7）的上下文中有效。

表达式的最终结果绝不会是命名空间、类型、方法组或事件访问。相反，如上所述，这些表达式类别是仅在某些上下文中允许的中间构造。

属性访问或索引器访问始终通过调用 get 访问器或 set 访问器重新分类为值。具体访问器由属性或索引器访问的上下文确定：如果该访问是赋值的目标，则调用 set 访问器以分配新值（§12.18.2）。否则，调用 get 访问器以获取当前值（§12.2.2）。

实例访问器是对实例的属性访问、对实例的事件访问或索引器访问。

### 12.2.2 表达式的值

大多数涉及表达式的构造最终都要求该表达式表示一个值。在这种情况下，如果实际表达式表示命名空间、类型、方法组或 Nothing，则会发生编译时错误。但是，如果表达式表示属性访问、索引器访问或变量，则隐式替换为该属性、索引器或变量的值：

- 变量的值就是当前存储在该变量所标识的存储位置中的值。在获取变量的值之前，该变量应被视为已明确赋值（§10.4），否则会发生编译时错误。
- 属性访问表达式的值通过调用属性的 get 访问器获得。如果属性没有 get 访问器，则发生编译时错误。否则，执行函数成员调用（§12.6.6），并且调用的结果成为属性访问表达式的值。
- 索引器访问表达式的值通过调用索引器的 get 访问器获得。如果索引器没有 get 访问器，则发生编译时错误。否则，使用与索引器访问表达式关联的实参列表执行函数成员调用（§12.6.6），并且调用的结果成为索引器访问表达式的值。

### 12.3 静态绑定和动态绑定

### 12.3.1 概述

绑定是根据表达式（实参、操作数、接收方）的类型或值确定操作所引用内容的过程。例如，方法调用的绑定根据接收方和实参的类型确定。运算符的绑定根据其操作数的类型确定。

在 C# 中，操作的绑定通常在编译时根据其子表达式的编译时类型确定。同样，如果表达式包含错误，则该错误由编译器检测并报告。这种方法称为静态绑定。

但是，如果表达式是动态表达式（即类型为 dynamic），则这表明其参与的任何绑定都应基于其运行时类型，而不是其在编译时具有的类型。因此，此类操作的绑定会推迟到程序运行期间要执行该操作时。这称为动态绑定。

当操作被动态绑定时，编译器执行的检查很少或根本不执行。相反，如果运行时绑定失败，错误会在运行时作为异常报告。

C# 中的以下操作受绑定约束：

- 成员访问：e.M
- 方法调用：e.M(e1,...,en)
- 委托调用：e(e1,...,en)
- 元素访问：e[e1,...,en]
- 对象创建：new C(e1,...,en)
- 重载一元运算符：+, -, !, ~, ++, --, true, false
- 重载二元运算符：+, -, *, /, %, &, &&, |, ||, ?, ?, ^, <<, >>, ==, !=, >, >=, <, <=
- 赋值运算符：=, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=
- 隐式和显式转换

当不涉及动态表达式时，C# 默认采用静态绑定，这意味着在选择过程中使用子表达式的编译时类型。但是，当上述操作中的某个子表达式是动态表达式时，该操作将改为动态绑定。

### 12.3.2 绑定时间

静态绑定发生在编译时，而动态绑定发生在运行时。在以下小节中，术语“绑定时间”指编译时或运行时，具体取决于绑定发生的时间。

> [示例：以下说明了静态绑定和动态绑定以及绑定时间的概念：
> ```
> object o = 5;
> dynamic d = 5;
> Console.WriteLine(5); // static binding to Console.WriteLine(int)
> Console.WriteLine(o); // static binding to Console.WriteLine(object)
> Console.WriteLine(d); // dynamic binding to Console.WriteLine(int)
> ```
> 前两个调用是静态绑定的：Console.WriteLine 的重载根据其参数的编译时类型选择。因此，绑定时间是编译时。
> 
> 第三个调用是动态绑定的：Console.WriteLine 的重载根据其参数的运行时类型选择。这是因为该参数是动态表达式——其编译时类型为 dynamic。因此，第三个调用的绑定时间是运行时。示例结束]

### 12.3.3 动态绑定

本小节为资料性内容。

动态绑定允许 C# 程序与动态对象交互，即不遵循 C# 类型系统常规规则的对象。动态对象可能是来自具有不同类型系统的其他编程语言的对象，也可能是通过编程方式设置以为不同操作实现其自身绑定语义的对象。

### 12.3.4 子表达式的类型

当操作被静态绑定时，子表达式（例如接收方、实参、索引或操作数）的类型始终被视为该表达式的编译时类型。




当操作是动态绑定的时，子表达式的类型取决于子表达式的编译时类型而以不同的方式确定：

- 编译时类型为 dynamic 的子表达式被认为具有该表达式在运行时求值时实际值的类型
- 编译时类型为类型参数的子表达式被认为具有该类型参数在运行时绑定的类型
- 否则，子表达式被认为具有其编译时类型。

## 12.4 运算符

### 12.4.1 通用

表达式由操作数和运算符构造。表达式的运算符指示要对操作数应用哪些操作。[Example: 运算符的示例包括 +, -, *, /, 和 new。操作数的示例包括字面量、字段、局部变量和表达式。end example]

存在三种类型的运算符：

- 一元运算符。一元运算符接受一个操作数，并使用前缀表示法（如 -x）或后缀表示法（如 x++）。
- 二元运算符。二元运算符接受两个操作数，且全部使用中缀表示法（如 x + y）。
- 三元运算符。只有一个三元运算符 ? :；它接受三个操作数并使用中缀表示法（c ? x : y）。

表达式中运算符的求值顺序由运算符的优先级和结合性决定（§12.4.2）。

表达式中的操作数按从左到右的顺序求值。[Example: 在 F(i) + G(i++) * H(i) 中，方法 F 使用 i 的旧值被调用，然后方法 G 使用 i 的旧值被调用，最后方法 H 使用 i 的新值被调用。这与运算符优先级无关且是独立的。end example]

某些运算符可以被重载。运算符重载（§12.4.3）允许为一个或两个操作数属于用户定义类或结构体类型的情况指定用户定义的运算符实现。

### 12.4.2 运算符优先级和结合性

当表达式包含多个运算符时，运算符的优先级控制各个运算符求值的顺序。[Note: 例如，表达式 x + y * z 被求值为 x + (y * z)，因为 * 运算符的优先级高于二元 + 运算符。end note] 运算符的优先级由其相关语法产生的定义确定。[Note: 例如，additive-expression 由一系列用 + 或 - 运算符分隔的 multiplicative-expressions 组成，从而使 + 和 - 运算符的优先级低于 *、/ 和 % 运算符。end note]

[Note: 下表按从高到低的顺序总结了所有运算符：

| 小节 | 类别 | 运算符 |
|---|---|---|
| §12.7 | 主 | x.y f(x) a[x] x++ x-- new typeof default checked unchecked delegate |
| §12.8 | 一元 | + - ! ~ ++x --x (T)x await x |
| §12.9 | 乘法 | * / % |
| §12.9 | 加法 | + - |
| §12.10 | 移位 | << >> |
| §12.11 | 关系和类型测试 | < > <= >= is as |
| §12.11 | 相等 | == != |
| §12.12 | 逻辑与 | & |
| §12.12 | 逻辑异或 | ^ |
| §12.12 | 逻辑或 | \| |
| §12.13 | 条件与 | && |
| §12.13 | 条件或 | \|\| |
| §12.14 | 空合并 | ?? |
| §12.15 | 条件 | ?: |
| §12.18 and §12.16 | 赋值和 lambda 表达式 | = *= /= %= += -= <<= >>= &= ^= \|= => |

end note]

当一个操作数出现在具有相同优先级的两个运算符之间时，运算符的结合性控制操作的执行顺序：

- 除赋值运算符和空合并运算符外，所有二元运算符都是左结合的，这意味着操作从左到右执行。[Example: x + y + z 被求值为 (x + y) + z。end example]
- 赋值运算符、空合并运算符和条件运算符 (?:) 是右结合的，这意味着操作从右到左执行。[Example: x = y = z 被求值为 x = (y = z)。end example]

优先级和结合性可以使用括号来控制。[Example: x + y * z 首先将 y 乘以 z 然后将结果加到 x 上，但 (x + y) * z 首先将 x 和 y 相加然后将结果乘以 z。end example]

### 12.4.3 运算符重载

所有一元和二元运算符都有预定义实现，可在任何表达式中自动使用。除了预定义实现之外，还可以通过在类和结构体中包含运算符声明（§15.10）来引入用户定义实现。用户定义的运算符实现始终优先于预定义的运算符实现：只有在不存在适用的用户定义运算符实现时，才会考虑预定义的运算符实现，如 §12.4.4 和 §12.4.5 中所述。

可重载的一元运算符是：

```
+  -  !  ~  ++  --  true  false
```

[Note: 尽管 true 和 false 在表达式中没有显式使用（因此未包含在 §12.4.2 的优先级表中），但它们被视为运算符，因为它们在多个表达式上下文中被调用：布尔表达式（§12.21）以及涉及条件（§12.15）和条件逻辑运算符（§12.13）的表达式。end note]

**可重载的二元运算符** 是：

```
+  -  *  /  %  &  |  ^  <<  >>  ==  !=  >  <  >=  <=
```

只有上面列出的运算符可以被重载。特别是，不可能重载成员访问、方法调用，或 =, &&, ||, ??, ?., =>, checked, unchecked, new, typeof, default, as 和 is 运算符。

当二元运算符被重载时，对应的复合赋值运算符（如果有）也会被隐式重载。[Example: 运算符 * 的重载也是运算符 *= 的重载。这在 §12.18 中进一步描述。end example] 赋值运算符本身 (=) 不能被重载。赋值始终将值简单地存储到变量中（§12.18.2）。

强制转换操作，如 (T)x，通过提供用户定义转换（§11.5）来重载。[Note: 用户定义转换不影响 is 或 as 运算符的行为。end note]

元素访问，如 a[x]，不被视为可重载运算符。相反，用户定义的索引通过索引器（§15.9）支持。

在表达式中，运算符使用运算符表示法引用，在声明中，运算符使用函数表示法引用。下表显示了一元和二元运算符的运算符表示法与函数表示法之间的关系。在第一个条目中，op 表示任何可重载的一元前缀运算符。在第二个条目中，op 表示一元后缀 ++ 和 -- 运算符。在第三个条目中，op 表示任何可重载的二元运算符。[Note: 关于重载 ++ 和 -- 运算符的示例，请参见 §15.10.2。end note]

| 运算符表示法 | 函数表示法 |
|---|---|
| op x | operator op(x) |
| x op | operator op(x) |
| x op y | operator op(x, y) |

用户定义的运算符声明始终要求至少一个参数为包含运算符声明的类或结构体类型。[Note: 因此，用户定义的运算符不可能具有与预定义运算符相同的签名。end note]

用户定义的运算符声明不能修改运算符的语法、优先级或结合性。[Example: / 运算符始终是二元运算符，始终具有 §12.4.2 中指定的优先级级别，并且始终是左结合的。end example]

[Note: 虽然用户定义的运算符可以执行任何它喜欢的计算，但产生除直观预期之外的结果的实现强烈不被鼓励。例如，运算符 == 的实现应比较两个操作数的相等性并返回适当的 bool 结果。end note]

§12.8 至 §12.18 中对各个运算符的描述指定了运算符的预定义实现以及适用于每个运算符的任何附加规则。描述使用了术语一元运算符重载解析、二元运算符重载解析、数值提升和提升运算符，其定义可在以下小节中找到。



## 12.4.4 一元运算符重载解析

形式为 `op x` 或 `x op` 的操作，其中 `op` 为可重载的一元运算符，`x` 为类型为 `X` 的表达式，按如下方式处理：

- 由 `X` 提供的用于操作 `operator op(x)` 的候选用户定义运算符集合根据 §12.4.6 的规则确定。
- 如果候选用户定义运算符集合非空，则该集合成为该操作候选运算符集合。否则，预定义一元运算符 `op` 的实现，包括其提升形式，成为该操作候选运算符集合。给定运算符的预定义实现在运算符的描述中指定。枚举或委托类型提供的预定义运算符仅在任一操作数的绑定时类型——或如果是可空类型则为其基础类型——为该枚举或委托类型时才包含在此集合中。
- §12.6.4 的重载解析规则应用于候选运算符集合，以相对于参数列表 `(x)` 选择最佳运算符，并且该运算符成为重载解析过程的结果。如果重载解析无法选择唯一的最佳运算符，则会发生绑定时错误。

## 12.4.5 二元运算符重载解析

形式为 `x op y` 的操作，其中 `op` 为可重载的二元运算符，`x` 为类型为 `X` 的表达式，`y` 为类型为 `Y` 的表达式，按如下方式处理：

- 由 `X` 和 `Y` 提供的用于操作 `operator op(x, y)` 的候选用户定义运算符集合确定。该集合由 `X` 提供的候选运算符与 `Y` 提供的候选运算符的并集组成，各自均使用 §12.4.6 的规则确定。对于合并后的集合，候选项按如下方式合并：
  - 如果 `X` 和 `Y` 为同一类型，或如果 `X` 和 `Y` 派生自共同基类型，则共享的候选运算符在合并后的集合中仅出现一次。
  - 如果 `X` 和 `Y` 之间存在恒等转换，由 `Y` 提供的运算符 `opY` 的返回类型与由 `X` 提供的 `opX` 相同，并且 `opY` 的操作数字段到 `opX` 的对应操作数字段存在恒等转换，则集合中仅出现 `opX`。
- 如果候选用户定义运算符集合非空，则该集合成为该操作候选运算符集合。否则，预定义二元运算符 `op` 的实现，包括其提升形式，成为该操作候选运算符集合。给定运算符的预定义实现在运算符的描述中指定。对于预定义枚举和委托运算符，仅考虑由操作数之一的绑定时类型为枚举或委托类型的枚举或委托类型提供的运算符。
- §12.6.4 的重载解析规则应用于候选运算符集合，以相对于参数列表 `(x, y)` 选择最佳运算符，并且该运算符成为重载解析过程的结果。如果重载解析无法选择唯一的最佳运算符，则会发生绑定时错误。

## 12.4.6 候选用户定义运算符

给定类型 `T` 和操作 `operator op(A)`，其中 `op` 为可重载运算符且 `A` 为参数列表，由 `T` 为 `operator op(A)` 提供的候选用户定义运算符集合确定如下：

- 确定类型 `T0`。如果 `T` 为可空值类型，则 `T0` 为其基础类型；否则 `T0` 等于 `T`。
- 对于 `T0` 中所有 `operator op` 声明以及此类运算符的所有提升形式，如果至少有一个运算符相对于参数列表 `A` 是适用的（§12.6.4.2），则候选运算符集合由 `T0` 中所有此类适用运算符组成。
- 否则，如果 `T0` 为 `object`，则候选运算符集合为空。
- 否则，由 `T0` 提供的候选运算符集合为 `T0` 的直接基类提供的候选运算符集合，或如果 `T0` 为类型参数则为 `T0` 的有效基类提供的候选运算符集合。

## 12.4.7 数值提升

### 12.4.7.1 一般

**本小节为说明性内容。**

数值提升包括自动执行预定义一元和二元数值运算符的操作数的某些隐式转换。数值提升不是一个独立的机制，而是将重载解析应用于预定义运算符的效果。数值提升具体不影响用户定义运算符的求值，尽管用户定义运算符可以实现以表现出类似的效果。

作为数值提升的示例，考虑二元 `*` 运算符的预定义实现：

```
int operator *(int x, int y);
uint operator *(uint x, uint y);
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
float operator *(float x, float y);
double operator *(double x, double y);
decimal operator *(decimal x, decimal y);
```

当将重载解析规则（§12.6.4）应用于此运算符集合时，其效果是选择操作数字段存在隐式转换的运算符中的第一个。[示例：对于操作 `b * s`，其中 `b` 为 `byte` 且 `s` 为 `short`，重载解析选择 `operator *(int, int)` 作为最佳运算符。因此，效果是 `b` 和 `s` 被转换为 `int`，并且结果的类型为 `int`。同样，对于操作 `i * d`，其中 `i` 为 `int` 且 `d` 为 `double`，重载解析选择 `operator *(double, double)` 作为最佳运算符。示例结束]

**说明性文本结束。**

### 12.4.7.2 一元数值提升

**本小节为说明性内容。**

一元数值提升发生在预定义 `+`、`-` 和 `~` 一元运算符的操作数上。一元数值提升仅包括将类型为 `sbyte`、`byte`、`short`、`ushort` 或 `char` 的操作数转换为类型 `int`。此外，对于一元 `-` 运算符，一元数值提升将类型为 `uint` 的操作数转换为类型 `long`。

**说明性文本结束。**

### 12.4.7.3 二元数值提升

**本小节为说明性内容。**

二元数值提升发生在预定义 `+`、`-`、`*`、 `/`、`%`、`&`、`|`、`^`、`==`、`!=`、`>`、`<`、`>=` 和 `<=` 二元运算符的操作数上。二元数值提升隐式将两个操作数转换为共同类型，对于非关系运算符，该类型也成为操作的结果类型。二元数值提升包括按此处出现的顺序应用以下规则：

- 如果任一操作数为类型 `decimal`，则另一操作数转换为类型 `decimal`，或如果另一操作数为类型 `float` 或 `double` 则发生绑定时错误。
- 否则，如果任一操作数为类型 `double`，则另一操作数转换为类型 `double`。
- 否则，如果任一操作数为类型 `float`，则另一操作数转换为类型 `float`。
- 否则，如果任一操作数为类型 `ulong`，则另一操作数转换为类型 `ulong`，或如果另一操作数为类型 `sbyte`、`short`、`int` 或 `long` 则发生绑定时错误。
- 否则，如果任一操作数为类型 `long`，则另一操作数转换为类型 `long`。

为非空时，提升运算符将解包操作数并应用基础运算符以产生 `bool` 结果。

对于关系运算符 `< > <= >=`，如果操作数字段均为非可空值类型并且结果类型为 `bool`，则存在运算符的提升形式。提升形式是通过向每个操作数字段添加单个 `?` 修饰符构造的。提升运算符在任一或两个操作数为 null 时产生值 `false`。否则，提升运算符将解包操作数并应用基础运算符以产生 `bool` 结果。

## 12.5 成员查找

### 12.5.1 一般

成员查找是确定名称在类型上下文中的含义的过程。成员查找可以作为在表达式中求值简单名称（§12.7.3）或成员访问（§12.7.5）的一部分而发生。如果简单名称或成员访问作为调用表达式（§12.7.6.2）的 primary-expression 出现，则该成员被视为被调用。

如果成员是方法或事件，或者它是委托类型（§20）或类型 `dynamic`（§9.2.4）的常量、字段或属性，则该成员被视为可调用的。

成员查找不仅考虑成员的名称，还考虑成员具有的类型参数数量以及成员是否可访问。对于成员查找的目的，泛型方法和嵌套泛型类型具有在其各自声明中指示的类型参数数量，而所有其他成员具有零个类型参数。

在类型 `T` 中对名称 `N` 具有 `K` 个类型参数的成员查找按如下方式处理：

- 首先，确定一组可访问的名称为 `N` 的成员：
  - 如果 `T` 为类型参数，则该集合为指定为 `T` 的主约束或次要约束（§15.2.5）之一的类型中可访问的名称为 `N` 的成员集合的并集，以及 `object` 中可访问的名称为 `N` 的成员集合。
  - 否则，该集合由 `T` 中所有可访问的（§8.5）名称为 `N` 的成员组成，包括继承成员和 `object` 中可访问的名称为 `N` 的成员。如果 `T` 为构造类型，则成员集合通过 §15.3.3 中描述的类型参数替换获得。包含 `override` 修饰符的成员从集合中排除。
- 接下来，如果 `K` 为零，则删除所有声明中包含类型参数的嵌套类型。如果 `K` 不为零，则删除所有类型参数数量不同的成员。当 `K` 为零时，方法不会因具有类型参数而被删除，因为类型推断过程（§12.6.3）可能能够推断类型参数。
- 接下来，如果成员被调用，则从集合中删除所有不可调用成员。
- 接下来，从集合中删除被其他成员隐藏的成员。对于集合中每个成员 `S.M`，其中 `S` 为成员 `M` 声明的类型，应用以下规则：
  - 如果 `M` 为常量、字段、属性、事件或枚举成员，则从集合中删除在 `S` 的基类型中声明的所有成员。
  - 如果 `M` 为类型声明，则从集合中删除在 `S` 的基类型中声明的所有非类型，以及在 `S` 的基类型中声明的与 `M` 具有相同类型参数数量的所有类型声明。
  - 如果 `M` 为方法，则从集合中删除在 `S` 的基类型中声明的所有非方法成员。
- 接下来，删除被类成员隐藏的接口成员。此步骤仅在 `T` 为类型参数并且 `T` 具有除 `object` 之外的有效基类并且 `T` 具有


非空有效接口集 (§15.2.5)。对于集合中的每个成员 S.M，其中 S 是声明成员 M 的类型，如果 S 是 object 之外的类声明，则应用以下规则：

- 如果 M 是常量、字段、属性、事件、枚举成员或类型声明，则从集合中删除所有在接口声明中声明的成员。
- 如果 M 是方法，则从集合中删除所有在接口声明中声明的非方法成员，并且删除所有与 M 具有相同签名的在接口声明中声明的方法。

最后，在删除隐藏成员后，确定查找的结果：

- 如果集合仅由一个非方法成员组成，则该成员是查找的结果。
- 否则，如果集合仅包含方法，则该方法组是查找的结果。
- 否则，查找是不明确的，并且会发生绑定时错误。

对于类型参数和接口之外的类型的成员查找，以及对于严格单继承的接口的成员查找（继承链中的每个接口恰好有零个或一个直接基接口），查找规则的效果仅仅是派生成员隐藏具有相同名称或签名的基成员。此类单继承查找永远不会产生歧义。可能由多继承接口中的成员查找引起的歧义在 §18.4.6 中描述。[注：此阶段仅考虑一种歧义。如果成员查找导致方法组，方法组的进一步使用可能因歧义而失败，例如在 §12.6.4.1 和 §12.6.6.2 中所述。结束注]

## 12.5.2 基类型

为成员查找目的，类型 T 被认为具有以下基类型：

- 如果 T 是 object 或 dynamic，则 T 没有基类型。
- 如果 T 是枚举类型，则 T 的基类型是类类型 System.Enum、System.ValueType 和 object。
- 如果 T 是结构体类型，则 T 的基类型是类类型 System.ValueType 和 object。[注：可空值类型是结构体类型 (§9.3.1)。结束注]
- 如果 T 是类类型，则 T 的基类型是 T 的基类，包括类类型 object。
- 如果 T 是接口类型，则 T 的基类型是 T 的基接口和类类型 object。
- 如果 T 是数组类型，则 T 的基类型是类类型 System.Array 和 object。
- 如果 T 是委托类型，则 T 的基类型是类类型 System.Delegate 和 object。

## 12.6 函数成员

### 12.6.1 通用

函数成员是包含可执行语句的成员。函数成员始终是类型的成员，不能是命名空间的成员。C# 定义了以下类别的函数成员：

- 方法
- 属性
- 事件
- 索引器
- 用户定义运算符
- 实例构造函数
- 静态构造函数
- 析构函数

除析构函数和静态构造函数（不能显式调用）外，函数成员中包含的语句通过函数成员调用执行。编写函数成员调用的实际语法取决于特定的函数成员类别。

函数成员调用的参数列表 (§12.6.2) 为函数成员的参数提供实际值或变量引用。

泛型方法的调用可以使用类型推断来确定要传递给方法的类型参数集合。此过程在 §12.6.3 中描述。

方法、索引器、运算符和实例构造函数的调用采用重载解析来确定要调用的候选函数成员集合中的哪一个。此过程在 §12.6.4 中描述。

一旦在绑定时（可能通过重载解析）识别出特定的函数成员，则调用函数成员的实际运行时过程在 §12.6.6 中描述。

[注：下表总结了涉及可显式调用的六类函数成员的构造中发生处理的。表中，e、x、y 和 value 表示分类为变量或值的表达式，T 表示分类为类型的表达式，F 是方法的简单名称，P 是属性的简单名称。]

| 构造 | 示例 | 描述 |
|---|---|---|
| 方法调用 | F(x, y) | 重载解析应用于选择包含类或结构体中的最佳方法 F。方法使用参数列表 (x, y) 被调用。如果方法不是静态的，则实例表达式为 this。 |
| 方法调用 | T.F(x, y) | 重载解析应用于选择类或结构体 T 中的最佳方法 F。如果方法不是静态的，则会发生绑定时错误。方法使用参数列表 (x, y) 被调用。 |
| 方法调用 | e.F(x, y) | 重载解析应用于选择由 e 的类型给出的类、结构体或接口中的最佳方法 F。如果方法为静态，则会发生绑定时错误。方法使用实例表达式 e 和参数列表 (x, y) 被调用。 |
| 属性访问 | P | 调用包含类或结构体中属性 P 的 get 访问器。如果 P 为仅写，则会发生编译时错误。如果 P 不是静态的，则实例表达式为 this。 |
| 属性访问 | P = value | 使用参数列表 (value) 调用包含类或结构体中属性 P 的 set 访问器。如果 P 为只读，则会发生编译时错误。如果 P 不是静态的，则实例表达式为 this。 |
| 属性访问 | T.P | 调用类或结构体 T 中属性 P 的 get 访问器。如果 P 不是静态的或 P 为仅写，则会发生编译时错误。 |
| 属性访问 | T.P = value | 使用参数列表 (value) 调用类或结构体 T 中属性 P 的 set 访问器。如果 P 不是静态的或 P 为只读，则会发生编译时错误。 |

结束注]

### 12.6.2 参数列表

### 12.6.2.1 通用

每个函数成员和委托调用都包括一个参数列表，该列表为函数成员的参数提供实际值或变量引用。指定函数成员调用的参数列表的语法取决于函数成员类别：

- 对于实例构造函数、方法、索引器和委托，参数指定为 *参数列表*，如下所述。对于索引器，在调用 *set* 访问器时，参数列表 additionally 包括指定为赋值运算符右操作数的表达式。[注：此额外参数不用于重载解析，仅在调用 set 访问器期间使用。结束注]
- 对于属性，在调用 *get* 访问器时参数列表为空，在调用 *set* 访问器时参数列表由指定为赋值运算符右操作数的表达式组成。
- 对于事件，参数列表由指定为 *+=* 或 *-=* 运算符右操作数的表达式组成。
- 对于用户定义运算符，参数列表由一元运算符的单个操作数或二元运算符的两个操作数组成。

属性 (§15.7)、事件 (§15.8) 和用户定义运算符 (§15.10) 的参数始终作为值参数 (§15.6.2.2) 传递。索引器 (§15.9) 的参数始终作为值参数 (§15.6.2.2) 或参数数组 (§15.6.2.5) 传递。对于这些类别的函数成员，不支持引用参数和输出参数。

实例构造函数、方法、索引器或委托调用的参数指定为 *参数列表*：

```
argument-list:
    argument
    argument-list , argument

argument:
    argument-nameopt argument-value

argument-name:
    identifier :

argument-value:
    expression
    ref variable-reference
    out variable-reference
```

一个 *参数列表* 由一个或多个 *参数* 组成，用逗号分隔。每个参数由可选的 *参数名* 后跟 *参数值* 组成。具有 *参数名* 的参数称为 *命名参数*，而没有 *参数名* 的参数为 *位置参数*。在 *参数列表* 中，位置参数出现在命名参数之后是错误。

*参数值* 可以采用以下形式之一：

- 一个 *表达式*，表示参数作为值参数 (§15.6.2.2) 传递。
- 关键字 *ref* 后跟 *变量引用* (§10.5)，表示参数作为引用参数 (§15.6.2.3) 传递。变量在作为引用参数传递之前必须被明确赋值 (§10.4)。




- 关键字 out 后跟变量引用（§10.5），表示该实参作为输出参数传递（§15.6.2.4）。在将该变量作为输出参数传递的函数成员调用之后，该变量被视为明确赋值（§10.4）。

该形式分别决定实参的参数传递模式：值、引用或输出。

将 volatile 字段（§15.5.4）作为引用参数或输出参数传递会导致警告，因为被调用的方法可能不会将该字段视为 volatile。

## 12.6.2.2 对应参数

对于实参列表中的每个实参，被调用的函数成员或委托中必须有一个对应的形参。

下文中使用的参数列表按如下方式确定：

- 对于类中定义的虚方法和索引器，参数列表取自以下过程中找到的函数成员的第一个声明或重写：从接收方的静态类型开始，并搜索其基类。
- 对于分部方法，使用定义分部方法声明的参数列表。
- 对于所有其他函数成员和委托，只有一个参数列表，即所使用的那个参数列表。

实参或形参的位置定义为在实参列表或形参列表中位于其前面的实参或形参的数目。

函数成员实参的对应形参按如下方式建立：

- 实例构造函数、方法、索引器和委托的实参列表中的实参：
  - 当形参出现在参数列表中的同一位置时，该位置实参对应该形参，除非该形参是参数数组且该函数成员以其展开形式调用。
  - 对于带参数数组且以其展开形式调用的函数成员，位于参数列表中参数数组位置处或之后的按位置实参，对应于该参数数组中的一个元素。
  - 命名实参对应于参数列表中同名的形参。
  - 对于索引器，调用 set 访问器时，指定为赋值运算符右操作数的表达式对应于该 set 访问器声明的隐式 value 形参。
- 对于属性，调用 get 访问器时没有实参。调用 set 访问器时，指定为赋值运算符右操作数的表达式对应于该 set 访问器声明的隐式 value 形参。
- 对于用户定义的一元运算符（包括转换），单个操作数对应于该运算符声明的单个形参。
- 对于用户定义的二元运算符，左操作数对应于该运算符声明的第一个形参，右操作数对应于第二个形参。

## 12.6.2.3 实参列表的运行时求值

在函数成员调用（§12.6.6）的运行时处理期间，实参列表中的表达式或变量引用按从左到右的顺序求值，如下所示：

- 对于值参数，求值实参表达式，并执行到对应形参类型的隐式转换（§11.2）。结果值成为函数成员调用中该值参数的初始值。

如果每个提供的实参并非恰好对应于该方法中的一个形参（§12.6.2.2），或者存在没有对应实参的非可选形参，则推断立即失败。否则，假定泛型方法具有以下签名：

T_R M<X1...Xn>(T1 p1 ... Tm pm)

对于形式为 M<E1 ... En> 的方法调用，类型推断的任务是为每个类型参数 X1...Xn 找到唯一的类型实参 S1...Sn，使得调用 M<S1...Sn>(E1...En) 变得有效。

下面将类型推断过程描述为一种算法。符合规范的编译器可以使用替代方法实现，只要它在所有情况下都得到相同的结果。

在推断过程中，每个类型参数 Xi 要么固定为特定类型 Si，要么未固定并关联一组界限。每个界限都是某个类型 T。最初，每个类型变量 Xi 都是未固定的，并具有空界限集。

类型推断分阶段进行。每个阶段都会根据前一阶段的发现尝试为更多类型变量推断类型实参。第一阶段进行一些初始的界限推断，而第二阶段将类型变量固定为特定类型并推断更多界限。第二阶段可能需要重复多次。

[注意：类型推断不仅发生在调用泛型方法时。方法组转换的类型推断在 §12.6.3.14 中描述，而查找一组表达式的最佳公共类型在 §12.6.3.15 中描述。结束注意]

## 12.6.3.2 第一阶段

对于每个方法实参 Ei：

- 如果 Ei 是匿名函数，则从 Ei 到 Ti 进行显式参数类型推断（§12.6.3.8）。
- 否则，如果 Ei 具有类型 U 且 Xi 是值参数（§15.6.2.2），则从 U 到 Ti 进行下界推断（§12.6.3.10）。
- 否则，如果 Ei 具有类型 U 且 Xi 是引用参数（§15.6.2.3）或输出参数（§15.6.2.4），则从 U 到 Ti 进行精确推断（§12.6.3.9）。
- 否则，不对此实参进行推断。

## 12.6.3.3 第二阶段

第二阶段按如下方式进行：

- 所有不依赖于（§12.6.3.6）任何 Xj 的未固定类型变量 Xi 都被固定（§12.6.3.12）。
- 如果不存在这样的类型变量，则所有满足以下全部条件的未固定类型变量 Xi 都被固定：
  - 至少存在一个依赖于 Xi 的类型变量 Xj。
  - Xi 具有非空界限集。
- 如果不存在这样的类型变量且仍有未固定类型变量，则类型推断失败。
- 否则，如果不存在更多未固定类型变量，则类型推断成功。
- 否则，对于所有具有对应形参类型 Ti 的实参 Ei，如果输出类型（§12.6.3.5）包含未固定类型变量 Xi 而输入类型（§12.6.3.4）不包含，则从 Ei 到 Ti 进行输出类型推断（§12.6.3.7）。然后重复第二阶段。

## 12.6.3.4 输入类型

如果 E 是方法组或隐式类型匿名函数，且 T 是委托类型或表达式树类型，则 T 的所有参数类型都是 E 在类型 T 下的输入类型。

## 12.6.3.5 输出类型

如果 E 是方法组或匿名函数，且 T 是委托类型或表达式树类型，则 T 的返回类型是 E 在类型 T 下的输出类型。

## 12.6.3.6 依赖

如果对于某个具有类型 T_k 的实参 E_k，X_j 出现在 E_k 在类型 T_k 下的输入类型中，且 X_i 出现在 E_k 在类型 T_k 下的输出类型中，则未固定类型变量 X_i 直接依赖于未固定类型变量 X_j。

如果 X_j 直接依赖于 X_i，或者如果 X_i 直接依赖于 X_k 且 X_k 依赖于 X_j，则 X_j 依赖于 X_i。因此，“依赖于”是“直接依赖于”的传递但非自反闭包。

## 12.6.3.7 输出类型推断

从表达式 E 到类型 T 的输出类型推断按如下方式进行：

- 如果 E 是具有推断返回类型 U（§12.6.3.13）的匿名函数，且 T 是具有返回类型 T_b 的委托类型或表达式树类型，则从 U 到 T_b 进行下界推断（§12.6.3.10）。
- 否则，如果 E 是方法组，且 T 是具有参数类型 T_1...T_k 和返回类型 T_b 的委托类型或表达式树类型，并且使用类型 T_1...T_k 对 E 进行重载解析得到具有返回类型 U 的单个方法，则从 U 到 T_b 进行下界推断。
- 否则，如果 E 是具有类型 U 的表达式，则从 U 到 T 进行下界推断。
- 否则，不进行推断。

## 12.6.3.8 显式参数类型推断

从表达式 E 到类型 T 的显式参数类型推断按如下方式进行：

- 如果 E 是具有参数类型 U_1...U_k 的显式类型匿名函数，且 T 是具有参数类型 V_1...V_k 的委托类型或表达式树类型，则对于每个 U_i，从 U_i 到对应的 V_i 进行精确推断（§12.6.3.9）。

## 12.6.3.9 精确推断

从类型 U 到类型 V 的精确推断按如下方式进行：

- 如果 V 是未固定的 X_i 之一，则将 U 添加到 X_i 的精确界限集中。
- 否则，通过检查以下任一情况是否适用来确定集合 V_1...V_k 和 U_1...U_k：
  - V 是数组类型 V_1[...]，且 U 是相同秩的数组类型 U_1[...]
  - V 是类型 V_i?，且 U 是类型 U_i?
  - V 是构造类型 C<V_1...V_k>，且 U 是构造类型 C<U_1...U_k>
  如果这些情况中的任一情况适用，则从每个 U_i 到对应的 V_i 进行精确推断。
- 否则，不进行推断。

## 12.6.3.10 下界推断

从类型 U 到类型 V 的下界推断按如下方式进行：

- 如果 V 是未固定的 X_i 之一，则将 U 添加到 X_i 的下界集中。
- 否则，如果 V 是类型 V_1?，且 U 是类型 U_1?，则从 U_1 到 V_1 进行下界推断。
- 否则，通过检查以下任一情况是否适用来确定集合 U_1...U_k 和 V_1...V_k：
  - V 是数组类型 V_1[...]，且 U 是相同秩的数组类型 U_1[...]



- V 是 IEnumerable<V1>、ICollection<V1>、IReadOnlyList<V1>、IReadOnlyCollection<V1> 或 IList<V1> 之一，且 U 是单维数组类型 U1[]
- V 是构造的类、结构体、接口或委托类型 C<V1...Vk>，并且存在唯一的 C<U1...Uk> 类型，使得 U（或，如果 U 是类型参数，则其有效基类或其有效接口集的任何成员）与 C<U1...Uk> 相同、继承自（直接或间接）或实现（直接或间接）C<U1...Uk>。
- （“唯一性”限制意味着在接口 C<T>{} 类 U: C<X>, C<Y>{} 的情况下，从 U 推断到 C<T> 时不进行推断，因为 U1 可能是 X 或 Y。）

如果适用上述任一情况，则按如下方式从每个 U_i 推断到对应的 V_i：

- 如果 U_i 不被已知为引用类型，则进行精确推断
- 否则，如果 U 是数组类型，则进行下界推断
- 否则，如果 V 是 C<V1...Vk>，则推断取决于 C 的第 i 个类型参数：
  - 如果它是协变的，则进行下界推断。
  - 如果它是逆变的，则进行上界推断。
  - 如果它是不可变的，则进行精确推断。
- 否则，不进行推断。

### 12.6.3.11 上界推断

从类型 U 到类型 V 的上界推断按如下方式进行：

- 如果 V 是未固定的 X_i 之一，则将 U 添加到 X_i 的上界集合中。
- 否则，如果适用以下任一情况，则确定集合 V1...Vk 和 U1...Uk：
  - U 是数组类型 U1[...] 且 V 是相同秩的数组类型 V1[...]
  - U 是 IEnumerable<U>、ICollection<U>、IReadOnlyList<U>、IReadOnlyCollection<U> 或 IList<U> 之一，且 V 是单维数组类型 V1[]
  - U 是类型 U? 且 V 是类型 V1?
  - U 是构造的类、结构体、接口或委托类型 C<U1...Uk>，且 V 是类、结构体、接口或委托类型，该类型与唯一的 C<V1...Vk> 类型相同、继承自（直接或间接）或实现（直接或间接）该类型
  - （“唯一性”限制意味着如果我们有接口 C<T>{} 类 V<Z>: C<X<Z>>, C<Y<Z>>{}，则从 C<U1> 推断到 V<Q> 时不进行推断。不会从 U1 推断到 X<Q> 或 Y<Q>。）

如果适用上述任一情况，则按如下方式从每个 U_i 推断到对应的 V_i：

- 如果 U_i 不被已知为引用类型，则进行精确推断
- 否则，如果 V 是数组类型，则进行上界推断
- 否则，如果 U 是 C<U1...Uk>，则推断取决于 C 的第 i 个类型参数：
  - 如果它是协变的，则进行上界推断。
  - 如果它是逆变的，则进行下界推断。
  - 如果它是不可变的，则进行精确推断。
- 否则，不进行推断。

### 12.6.3.12 固定

具有一组边界的未固定类型变量 X_i 按如下方式固定：

- 候选类型 U_j 的集合最初是 X_i 的边界集合中的所有类型的集合。
- 然后我们依次检查 X_i 的每个边界：对于 X_i 的每个精确边界 U，从候选集合中移除所有不与 U 相同的类型 U_j。对于 X_i 的每个下界 U，从候选集合中移除所有不存在从 U 到其的隐式转换的类型 U_j。对于 X_i 的每个上界 U，从候选集合中移除所有不存在到 U 的隐式转换的类型 U_j。
- 如果在剩余的候选类型 U_j 中存在唯一的类型 V，使得从所有其他候选类型到 V 存在隐式转换，则将 X_i 固定为 V。
- 否则，类型推断失败。

### 12.6.3.13 推断的返回类型

匿名函数 F 的推断返回类型在类型推断和重载解析期间使用。推断返回类型只能在所有参数类型已知的情况下确定，即参数类型是显式给出的、通过匿名函数转换提供的，或在封闭的泛型方法调用的类型推断期间推断出来的。

推断的有效返回类型按如下方式确定：

- 如果 F 的主体是一个具有类型的表达式，则 F 的推断有效返回类型是该表达式的类型。
- 如果 F 的主体是一个块，并且块的 return 语句中的表达式集合具有最佳公共类型 T（§12.6.3.15），则 F 的推断有效返回类型为 T。
- 否则，无法为 F 推断有效返回类型。

推断的返回类型按如下方式确定：

- 如果 F 是 async 且 F 的主体是被分类为 nothing 的表达式（§12.2），或没有 return 语句带有表达式的语句块，则推断的返回类型为 System.Threading.Tasks.Task
- 如果 F 是 async 且具有推断的有效返回类型 T，则推断的返回类型为 System.Threading.Tasks.Task<T>。
- 如果 F 是非 async 且具有推断的有效返回类型 T，则推断的返回类型为 T。
- 否则，无法为 F 推断返回类型。

[示例：作为涉及匿名函数的类型推断的示例，考虑在 System.Linq.Enumerable 类中声明的 Select 扩展方法：

```csharp
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource,TResult>(
            this IEnumerable<TSource> source,
            Func<TSource,TResult> selector)
        {
            foreach (TSource element in source) yield return
            selector(element);
        }
    }
}
```

假设已通过 using 命名空间指令导入 System.Linq 命名空间，并且给定一个 Name 属性类型为 string 的 Customer 类，Select 方法可用于选择客户列表的名称：

```csharp
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

Select 的扩展方法调用（§12.7.6.3）通过将调用重写为静态方法调用来处理：

```csharp
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

由于未显式指定类型参数，因此使用类型推断来推断类型参数。首先，将 customers 参数与 source 参数关联，推断 TSource 为 Customer。然后，使用上面描述的匿名函数类型推断过程，c 被赋予 Customer 类型，并且表达式 c.Name 与 selector 参数的返回类型关联，推断 TResult 为 string。因此，该调用等价于

```csharp
Enumerable.Select<Customer,string>(customers, ((Customer c) => c.Name))
```

并且结果的类型为 IEnumerable<string>。

以下示例演示了匿名函数类型推断如何允许类型信息在泛型方法调用的参数之间“流动”。给定方法：

```csharp
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2) {
    return f2(f1(value));
}
```

对以下调用的类型推断：

```csharp
double_seconds = F("1:15:30", s => TimeSpan.Parse(s), t =>
    t.TotalSeconds);
```

按如下方式进行：首先，将参数 "1:15:30" 与 value 参数关联，推断 X 为 string。然后，将第一个匿名函数的参数 s 赋予推断的类型 string，并且表达式 TimeSpan.Parse(s) 与 f1 的返回类型关联，推断 Y 为 System.TimeSpan。最后，将第二个匿名函数的参数 t 赋予推断的类型 System.TimeSpan，并且表达式 t.TotalSeconds 与 f2 的返回类型关联，推断 Z 为 double。因此，该调用的结果类型为 double。 end example]

### 12.6.3.14 方法组转换的类型推断

与泛型方法的调用类似，当包含泛型方法的 方法组 M 被转换为给定的委托类型 D（§11.8）时，也应应用类型推断。给定方法

```csharp
T_r M<X1...Xn>(T1 x1 ... Tn xn)
```

并且方法组 M 被赋给委托类型 D，类型推断的任务是找到类型参数 S1...Sn，使得表达式：

```csharp
M<S1...Sn>
```

与 D 兼容（§20.2）。

与泛型方法调用的类型推断算法不同，在这种情况下，只有参数类型，没有参数表达式。特别是，没有匿名函数，因此不需要多阶段推断。

相反，所有 X_i 都被视为未固定，并且从 D 的每个参数类型 U_j 到 M 的对应参数类型 T_j 进行下界推断。如果对于任何 X_i 未找到边界，则类型推断失败。否则，所有 X_i 都被固定为对应的 S_i，即类型推断的结果。

### 12.6.3.15 查找表达式集合的最佳公共类型

在某些情况下，需要为一组表达式推断一个公共类型。特别是，隐式类型数组的元素类型和具有块主体的匿名函数的返回类型就是这样找到的。

表达式集合 E1...Em 的最佳公共类型按如下方式确定：

- 引入一个新的未固定类型变量 X。



- 对每个表达式 Ei 执行一次 *输出类型推断* (§12.6.3.7) 从它到 X。
- X 被 *固定* (§12.6.3.12)，如果可能，结果类型为最佳公共类型。
- 否则推断失败。

> [注意：直观上此推断等价于调用一个方法
>
> `void M<X>(X x1 ... X xn)`
>
> 并将 Ei 作为参数并推断 X。*结束注意*]

## 12.6.4 重载解析

### 12.6.4.1 通用

重载解析是一种绑定时机制，用于在给定参数列表和一组候选函数成员的情况下选择要调用的最佳函数成员。重载解析在 C# 内的以下不同上下文中选择要调用的函数成员：

- 在 *调用表达式* (§12.7.6) 中命名的方法的调用。
- 在 *对象创建表达式* (§12.7.11.2) 中命名的实例构造函数的调用。
- 通过 *元素访问* (§12.7.7) 调用索引器访问器。
- 在表达式中引用的预定义或用户定义运算符的调用 (§12.4.4 和 §12.4.5)。

这些上下文各自以其独特的方式定义候选函数成员的集合和参数列表。例如，方法调用的候选集合不包括标记为 override 的方法 (§12.5)，并且如果派生类中的任何方法适用，则基类中的方法不是候选 (§12.7.6.2)。

一旦确定了候选函数成员和参数列表，在所有情况下选择最佳函数成员的方式都相同：

- 首先，将候选函数成员的集合缩小为相对于给定参数列表适用的那些函数成员 (§12.6.4.2)。如果此缩小后的集合为空，则会发生编译时错误。
- 然后，从适用候选函数成员的集合中定位最佳函数成员。如果集合仅包含一个函数成员，则该函数成员为最佳函数成员。否则，最佳函数成员是相对于给定参数列表优于所有其他函数成员的那个函数成员，前提是使用 §12.6.4.3 中的规则将每个函数成员与所有其他函数成员进行比较。如果没有恰好一个函数成员优于所有其他函数成员，则函数调用不明确并发生绑定时错误。

以下小节定义了术语 *适用函数成员* 和 *更好函数成员* 的确切含义。

### 12.6.4.2 适用函数成员

当满足以下所有条件时，函数成员被称为相对于参数列表 A 的 *适用函数成员*：

- 参数列表 A 中的每个参数都对应于函数成员声明中描述的 §12.6.2.2 中的一个参数，最多一个参数对应于每个参数，并且任何没有参数对应的参数都是可选参数。
- 对于参数列表 A 中的每个参数，参数的传递模式与对应参数的传递模式相同，并且
  - 对于值参数或参数数组，参数表达式到对应参数类型的隐式转换 (§11.2) 存在，或
  - 对于 ref 或 out 参数，参数表达式的类型与对应参数的类型之间存在恒等转换

对于包含参数数组的函数成员，如果函数成员根据上述规则适用，则称其在其 **正常形式** 下适用。如果包含参数数组的函数成员在其正常形式下不适用，则该函数成员可能在其 **扩展形式** 下适用：

- 扩展形式是通过用参数数组元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中的固定参数数量，则无法构造该函数成员的扩展形式，因此不适用。
- 否则，扩展形式适用如果对于参数列表 A 中的每个参数，参数的传递模式与对应参数的传递模式相同，并且
  - 对于固定的值参数或由扩展创建的值参数，参数表达式到对应参数类型的隐式转换 (§11.2) 存在，或
  - 对于 ref 或 out 参数，参数表达式的类型与对应参数的类型相同。

### 12.6.4.3 更好函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在扩展形式下适用，则使用扩展形式。
- 没有对应参数的可选参数从参数列表中移除。
- 参数被重新排序，使其出现在参数列表中对应参数的相同位置。

给定参数列表 A，其参数表达式集合为 { E₁, E₂, ..., Eₙ }，以及两个适用函数成员 Mₚ 和 M_q，其参数类型分别为 { P₁, P₂, ..., Pₙ } 和 { Q₁, Q₂, ..., Qₙ }，如果满足以下条件，则 Mₚ 被定义为比 M_q **更好函数成员**：

- 对于每个参数，从 Eₓ 到 Qₓ 的隐式转换不优于从 Eₓ 到 Pₓ 的隐式转换，并且
- 对于至少一个参数，从 Eₓ 到 Pₓ 的转换优于从 Eₓ 到 Qₓ 的转换。

如果参数类型序列 { P₁, P₂, ..., Pₙ } 和 { Q₁, Q₂, ..., Qₙ } 相等（即每个 P_i 到对应 Q_i 存在恒等转换），则按顺序应用以下平局打破规则来确定更好的函数成员。

- 如果 Mₚ 是非泛型方法而 M_q 是泛型方法，则 Mₚ 优于 M_q。
- 否则，如果 Mₚ 在其正常形式下适用，而 M_q 具有 params 数组且仅在扩展形式下适用，则 Mₚ 优于 M_q。
- 否则，如果两个方法都有 params 数组且仅在其扩展形式下适用，并且 Mₚ 的 params 数组元素少于 M_q 的 params 数组，则 Mₚ 优于 M_q。
- 否则，如果 Mₚ 的参数类型比 M_q 更具体，则 Mₚ 优于 M_q。设 { R₁, R₂, ..., Rₙ } 和 { S₁, S₂, ..., Sₙ } 表示 Mₚ 和 M_q 的未实例化和未扩展参数类型。如果对于每个参数，Rₓ 不比 Sₓ 更不具体，并且对于至少一个参数，Rₓ 比 Sₓ 更具体，则 Mₚ 的参数类型比 M_q 更具体：
  - 类型参数比非类型参数更不具体。
  - 递归地，构造类型比另一个构造类型（具有相同数量的类型参数）更具体，如果至少一个类型参数更具体，并且没有类型参数比另一个中的对应类型参数更不具体。
  - 数组类型比另一个数组类型（具有相同数量的维度）更具体，如果第一个的元素类型比第二个的元素类型更具体。
- 否则，如果一个成员是非提升运算符而另一个是提升运算符，则非提升的更好。
- 如果没有函数成员被发现更好，并且 Mₚ 的所有参数都有对应参数，而 M_q 中至少一个可选参数需要使用默认值替代，则 Mₚ 优于 M_q。否则，没有函数成员更好。

### 12.6.4.4 从表达式的更好转换

给定隐式转换 C1 将表达式 E 转换为类型 T1，以及隐式转换 C2 将表达式 E 转换为类型 T2，如果满足以下至少一个条件，则 C1 是比 C2 更好的转换：

- E 具有类型 S，并且从 S 到 T1 存在恒等转换但从 S 到 T2 不存在
- E 不是匿名函数且 T1 是比 T2 更好的转换目标 (§12.6.4.6)
- E 是匿名函数，T1 是委托类型 D1 或表达式树类型 `Expression<D1>`，T2 是委托类型 D2 或表达式树类型 `Expression<D2>`，并且满足以下之一：
  - D1 是比 D2 更好的转换目标
  - D1 和 D2 具有相同的参数列表，并且满足以下之一：
    - D1 具有返回类型 Y1，D2 具有返回类型 Y2，在该参数列表的上下文中 E 存在推断返回类型 X (§12.6.3.13)，并且从 X 到 Y1 的转换优于从 X 到 Y2 的转换
    - E 是 async，D1 具有返回类型 `Task<Y1>`，D2 具有返回类型 `Task<Y2>`，在该参数列表的上下文中 E 存在推断返回类型 X (§12.6.3.13)，并且从 X 到 Y1 的转换优于从 X 到 Y2 的转换
    - D1 具有返回类型 Y1，而 D2 返回 void

### 12.6.4.5 从类型的更好转换

给定转换 C1 将类型 S 转换为类型 T1，以及转换 C2 将类型 S 转换为类型 T2，如果满足以下至少一个条件，则 C1 是比 C2 更好的转换：

- 从 S 到 T1 存在恒等转换但从 S 到 T2 不存在
- T1 是比 T2 更好的转换目标 (§12.6.4.6)

### 12.6.4.6 更好的转换目标

给定两个不同的类型 T1 和 T2，如果满足以下至少一个条件，则 T1 是比 T2 更好的转换目标：

- 从 T1 到 T2 存在隐式转换，且从 T2 到 T1 不存在隐式转换
- T1 是有符号整数类型而 T2 是无符号整数类型。具体来说：
  - T1 是 sbyte 且 T2 是 byte、ushort、uint 或 ulong
  - T1 是 short 且 T2 是 ushort、uint 或 ulong




- T1 是 int，且 T2 是 uint 或 ulong
- T1 是 long，且 T2 是 ulong

## 12.6.4.7 泛型类中的重载

[注：虽然声明的签名应是唯一的（§9.6），但类型实参的替换可能导致相同的签名。在这种情况下，重载决策将选择原始签名（替换类型实参之前）中最具体的签名（§12.6.4.3）（如果存在），否则报告错误。结束注]

[示例：以下示例展示了根据此规则有效和无效的重载：]

```
interface I1<T> {...}
interface I2<T> {...}
class G1<U>
{
    int F1(U u);    // Overload resolution for G<int>.F1
    int F1(int i);  // will pick non-generic
    void F2(I1<U> a); // valid overload
    void F2(I2<U> a);
}
class G2<U,V>
{
    void F3(U u, V v);    // Valid, but overload resolution for
    void F3(V v, U u);    // G2<int,int>.F3 will fail
    void F4(U u, I1<V> v); // Valid, but overload resolution for
    void F4(I1<V> v, U u); // G2<I1<int>,int>.F4 will fail
    void F5(U u1, I1<V> v2); // valid overload
    void F5(V u1, U u2);
    void F6(ref U u); // valid overload
    void F6(out V v);
}
```

结束示例]

## 12.6.5 动态成员调用的编译时检查

尽管动态绑定操作的重载决策在运行时进行，但有时在编译时能够知道重载将从中选择的函数成员列表：

- 对于委托调用（§12.7.6.4），该列表是单个函数成员，其参数列表与调用的委托类型相同
- 对于对类型或静态类型不是 dynamic 的值进行的方法调用（§12.7.6.2），方法组中可访问的方法集在编译时是已知的。
- 对于对象创建表达式（§12.7.11.2），类型中可访问的构造函数集在编译时是已知的。
- 对于索引器访问（§12.7.7.3），接收者中可访问的索引器集在编译时是已知的。

在这些情况下，会对已知函数成员集中的每个成员执行有限的编译时检查，以确定是否可以确定该成员永远不会在运行时被调用。对于每个函数成员 F，会构造修改后的参数列表和实参列表：

- 首先，如果 F 是泛型方法且提供了类型实参，则用这些类型实参替换参数列表中的类型参数。但是，如果未提供类型实参，则不会进行这种替换。

- 然后，任何类型为开放类型（即包含类型参数；参见 §9.4.3）的参数连同其对应的参数一起被省略。

为使 F 通过检查，以下所有条件都必须成立：

- 按照 §12.6.4.2，F 的修改后参数列表适用于修改后的实参列表。
- 修改后参数列表中的所有构造类型都满足其约束（§9.4.5）。
- 如果在上一步中替换了 F 的类型参数，则满足它们的约束。
- 如果 F 是静态方法，则该方法组不得来自这样的成员访问：其接收者在编译时已知为变量或值。
- 如果 F 是实例方法，则该方法组不得来自这样的成员访问：其接收者在编译时已知为类型。

如果没有候选成员通过此测试，则发生编译时错误。

## 12.6.6 函数成员调用

### 12.6.6.1 概述

本子条款描述在运行时调用特定函数成员所发生的过程。假定绑定期过程已经确定了要调用的特定成员，可能是通过对一组候选函数成员应用重载决策来确定的。

为了描述调用过程，函数成员分为两类：

- 静态函数成员。这些是静态方法、静态属性访问器和用户定义运算符。静态函数成员始终是非虚的。
- 实例函数成员。这些是实例方法、实例构造函数、实例属性访问器和索引器访问器。实例函数成员要么是非虚的，要么是虚的，并且始终在特定实例上调用。该实例由实例表达式计算，并在函数成员内以 this（§12.7.8）的形式可访问。对于实例构造函数，实例表达式被视为新分配的对象。

函数成员调用的运行时处理包括以下步骤，其中 M 是函数成员；如果 M 是实例成员，则 E 是实例表达式：

- 如果 M 是静态函数成员：
  - 实参列表按 §12.6.2 所述求值。
  - 调用 M。
- 否则，如果 E 的类型是值类型 V，并且 M 在 V 中声明或重写：
  - 对 E 求值。如果此求值导致异常，则不执行后续步骤。对于实例构造函数，此求值包括为新对象分配存储（通常从执行栈分配）。在这种情况下，E 被归类为变量。
  - 如果 E 未被归类为变量，则创建 E 的类型的临时局部变量，并将 E 的值赋给该变量。然后 E 被重新归类为对该临时局部变量的引用。该临时变量在 M 内可作为 this 访问，但不能以任何其他方式访问。因此，只有当 E 是真正的变量时，调用方才可能观察到 M 对 this 所做的更改。
  - 实参列表按 §12.6.2 所述求值。
  - 调用 M。E 所引用的变量成为 this 所引用的变量。
- 否则：
  - 对 E 求值。如果此求值导致异常，则不执行后续步骤。
  - 实参列表按 §12.6.2 所述求值。
  - 如果 E 的类型是值类型，则执行装箱转换（§11.2.8）以将 E 转换为类类型，并且在后续步骤中 E 被视为该类型。如果该值类型是枚举类型，则该类类型为 System.Enum；否则为 System.ValueType。
  - 检查 E 的值是否有效。如果 E 的值为 null，则抛出 System.NullReferenceException，并且不执行后续步骤。
  - 确定要调用的函数成员实现：
    - 如果 E 的绑定期类型是接口，则要调用的函数成员是 E 所引用实例的运行时类型所提供的 M 的实现。该函数成员通过应用接口映射规则（§18.6.5）来确定，以确定 E 所引用实例的运行时类型所提供的 M 的实现。
    - 否则，如果 M 是虚函数成员，则要调用的函数成员是 E 所引用实例的运行时类型所提供的 M 的实现。该函数成员通过应用确定 M 相对于 E 所引用实例的运行时类型的最派生实现（§15.6.4）的规则来确定。
    - 否则，M 是非虚函数成员，要调用的函数成员就是 M 本身。
  - 调用上一步中确定的函数成员实现。E 所引用的对象成为 this 所引用的对象。

实例构造函数（§12.7.11.2）的调用结果是所创建的值。任何其他函数成员的调用结果是从其主体返回的值（如果有）（§13.10.5）。

### 12.6.6.2 对装箱实例的调用

在以下情况下，可以通过该值类型的装箱实例调用在值类型中实现的函数成员：

- 当函数成员是继承自类类型的方法的重写，并且通过该类的实例表达式调用时。[注：该类类型将始终是 System.Object、System.ValueType 或 System.Enum 之一。结束注]
- 当函数成员是接口函数成员的实现，并且通过接口类型的实例表达式调用时。
- 当函数成员通过委托调用时。

在这些情况下，装箱实例被视为包含该值类型的变量，并且该变量成为函数成员调用内由 this 引用的变量。[注：特别地，这意味着当对装箱实例调用函数成员时，该函数成员可以修改装箱实例中包含的值。结束注]

## 12.7 主表达式

### 12.7.1 概述

主表达式包括最简单的表达式形式。

主表达式：
主非数组创建表达式
数组创建表达式




```
primary-no-array-creation-expression:
    literal
    simple-name
    parenthesized-expression
    member-access
    invocation-expression
    element-access
    this-access
    base-access
    post-increment-expression
    post-decrement-expression
    object-creation-expression
    delegate-creation-expression
    anonymous-object-creation-expression
    typeof-expression
    sizeof-expression
    checked-expression
    unchecked-expression
    default-value-expression
    anonymous-method-expression
```

主表达式分为 *数组创建表达式* 和 *不创建数组的主表达式*。以这种方式处理 *数组创建表达式*，而不是将其与其他简单表达式形式一起列出，使得语法能够禁止可能令人困惑的代码，例如

```
object o = new int[3][1];
```

which would otherwise be interpreted as

```
object o = (new int[3])[1];
```

## 12.7.2 字面量

一个 *主表达式* 由 *字面量* (§7.4.5) 组成时，被归类为值。

## 12.7.3 简单名称

### 12.7.3.1 通用

一个 *简单名称* 由一个标识符组成，可选择后跟一个类型参数列表：

```
simple-name:
    identifier type-argument-list_opt
```

一个 *简单名称* 要么是形式为 I，要么是形式为 I<A1 , ... , Ak>，其中 I 是一个单一标识符，<A1 , ... , Ak> 是一个可选的 *类型参数列表*。当未指定 *类型参数列表* 时，将 K 视为零。*简单名称* 的求值和分类如下：

- 如果 K 为零且 *简单名称* 出现在一个 *块* 中，并且该 *块*（或外围 *块*）的局部变量声明空间 (§8.3) 包含名称为 I 的局部变量、参数或常量，则该 *简单名称* 引用该局部变量、参数或常量，并被归类为变量或值。
- 如果 K 为零且 *简单名称* 出现在泛型方法声明中但在其 *方法头* 的属性之外，并且该声明包含名称为 I 的类型参数，则 *简单名称* 引用该类型参数。
- 否则，对于每个实例类型 T (§15.3.2)，从最内层封闭类型声明的实例类型开始，继续每个封闭类或结构体声明（如果有）的实例类型：
  - 如果 K 为零且 T 的声明包含名称为 I 的类型参数，则 *简单名称* 引用该类型参数。
  - 否则，如果在 T 中对 I 进行具有 K 个类型参数的成员查找 (§12.5) 产生匹配：
    - 如果 T 是最内层封闭类或结构体类型的实例类型，并且查找识别出一个或多个方法，则结果是一个方法组，其关联的实例表达式为 *this*。如果指定了类型参数列表，则在调用泛型方法 (§12.7.6.2) 时使用它。
    - 否则，如果 T 是最内层封闭类或结构体类型的实例类型，如果查找识别出一个实例成员，并且如果引用出现在实例构造函数、实例方法或实例访问器 (§12.2.1) 的 *块* 内，则结果与形式为 *this*.I 的成员访问 (§12.7.5) 相同。这只能在 K 为零时发生。
    - 否则，结果与形式为 T.I 或 T.I<A1, ..., Ak> 的成员访问 (§12.7.5) 相同。在这种情况下，*简单名称* 引用实例成员是绑定时错误。
- 否则，对于每个命名空间 N，从 *简单名称* 出现的命名空间开始，继续每个封闭命名空间（如果有），并以全局命名空间结束，以下步骤被评估直到定位到一个实体：
  - 如果 K 为零且 I 是 N 中的命名空间的名称，则：
    - 如果 *简单名称* 出现的位置被 N 的命名空间声明所包围，并且命名空间声明包含一个将名称 I 与命名空间或类型关联的 *extern-alias-directive* 或 *using-alias-directive*，则 *简单名称* 是模糊的并且会发生编译时错误。
    - 否则，*简单名称* 引用 N 中名为 I 的命名空间。
  - 否则，如果 N 包含一个名称为 I 且具有 K 个类型参数的可访问类型，则：
    - 如果 K 为零且 *简单名称* 出现的位置被 N 的命名空间声明所包围，并且命名空间声明包含一个将名称 I 与命名空间或类型关联的 *extern-alias-directive* 或 *using-alias-directive*，则 *简单名称* 是模糊的并且会发生编译时错误。
    - 否则，*命名空间或类型名称* 引用使用给定类型参数构造的类型。
  - 否则，如果 *简单名称* 出现的位置被 N 的命名空间声明所包围：
    - 如果 K 为零且命名空间声明包含一个将名称 I 与导入的命名空间或类型关联的 *extern-alias-directive* 或 *using-alias-directive*，则 *简单名称* 引用该命名空间或类型。
    - 否则，如果命名空间声明的 *using-namespace-directives* 导入的命名空间恰好包含一个名称为 I 且具有 K 个类型参数的类型，则 *简单名称* 引用使用给定类型参数构造的该类型。
    - 否则，如果命名空间声明的 *using-namespace-directives* 导入的命名空间包含多于一个名称为 I 且具有 K 个类型参数的类型，则 *简单名称* 是模糊的并且会发生编译时错误。
  [Note: 整个步骤与处理 *命名空间或类型名称* (§8.8) 时对应的步骤完全平行。 end note]
- 否则，*简单名称* 未定义并且会发生编译时错误。

### 12.7.3.2 块中的不变含义

对于作为完整简单名称（不带类型参数列表）的给定标识符的每次出现，在表达式或声明符中，在紧邻包围该出现的局部变量声明空间 (§8.3) 内，同一标识符作为完整简单名称在表达式或声明符中的每次其他出现都应引用同一实体。 [Note: 此规则确保名称的含义在给定的块、switch 块、for-、foreach- 或 using- 语句或匿名函数中始终相同。 end note]

[Example: 示例

```
class Test
{
    double x;
    void F(bool b) {
        x = 1.0;
        if (b) {
            int x;
            x = 1;
        }
    }
}
```

导致编译时错误，因为 x 在外部块（其范围包括 if 语句中的嵌套块）内引用了不同的实体。相比之下，示例

```
class Test
{
    double x;
    void F(bool b) {
        if (b) {
            x = 1.0;
        }
        else {
            int x;
            x = 1;
        }
    }
}
```

是允许的，因为名称 x 在外部块中从未被使用。 end example]

[Note: 不变含义规则仅适用于简单名称。完全可以让同一个标识符作为简单名称具有一种含义，而作为成员访问 (§12.7.5) 的右操作数具有另一种含义。 end note] [Example:

```
struct Point
{
    int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

上述示例说明了在实例构造函数中使用字段名称作为参数名称的常见模式。在示例中，简单名称 x 和 y 引用参数，但这并不会阻止成员访问表达式 this.x 和 this.y 访问字段。 end example]

## 12.7.4 圆括号表达式

一个 *圆括号表达式* 由用括号括起来的表达式组成。

```
parenthesized-expression:
( expression )
```

- 如果引用出现在事件声明所在的类或结构体内部，并且事件是在没有 *事件访问器声明* (§15.8.1) 的情况下声明的，则 E . I 被处理得就像 I 是一个静态字段一样。
- 否则，结果是一个没有关联实例表达式的事件访问。
  - 如果 I 标识一个常量，则结果是一个值，即该常量的值。
  - 如果 I 标识一个枚举成员，则结果是一个值，即该枚举成员的值。
  - 否则，E . I 是一个无效的成员引用，并且会发生编译时错误。
- 如果 E 是属性访问、索引器访问、变量或值，其类型为 T，并且在 T 中对 I 进行具有 K 个类型参数的成员查找 (§12.5) 产生匹配，则 E . I 的求值和分类如下：
  - 首先，如果 E 是属性或索引器访问，则获取属性或索引器访问的值 (§12.2.2) 并且 E 被重新分类为值。
  - 如果 I 标识一个或多个方法，则结果是一个方法组，其关联的实例表达式为 E。
  - 如果 I 标识一个实例属性，则结果是一个属性访问，其关联的实例表达式为 E 并且关联的类型是该属性的类型。如果 T 是类类型，则关联的类型是从以 T 开始并搜索其基类时找到的属性的第一个声明或重写中选取的。
  - 如果 T 是 *类类型* 且 I 标识该 *类类型* 的实例字段：
    - 如果 E 的值为空，则抛出 System.NullReferenceException。
    - 否则，如果字段是只读并且引用出现在声明该字段的类的实例构造函数之外，则结果是一个值，即由 E 引用的对象中字段 I 的值。
    - 否则，结果是一个变量，即由 E 引用的对象中的字段 I。
  - 如果 T 是 *结构体类型* 且 I 标识该 *结构体类型* 的实例字段：
    - 如果 E 是一个值，或者如果字段是只读并且引用出现在声明该字段的结构体的实例构造函数之外，则结果是一个值，即由 E 给出的结构体实例中字段 I 的值。
    - 否则，结果是一个变量，即由 E 给出的结构体实例中的字段 I。
  - 如果 I 标识一个实例事件：
    - 如果引用出现在事件声明所在的类或结构体内部，并且事件是在没有 *事件访问器声明* (§15.8.1) 的情况下声明的，并且引用未作为 += 或 -= 运算符的左手侧出现，则 E . I 被处理得就像 I 是一个实例字段一样。
    - 否则，结果是一个事件访问，其关联的实例表达式为 E。
- 否则，会尝试将 E . I 作为扩展方法调用 (§12.7.6.3) 处理。如果失败，则 E . I 是一个无效的成员引用，并且会发生绑定时错误。

### 12.7.5.2 相同的简单名称和类型名称

在形式为 E . I 的成员访问中，如果 E 是一个单一标识符，并且 E 作为 *简单名称* (§12.7.3) 的含义是一个常量、字段、属性、局部变量或参数，其类型与 E 作为 *类型名称* (§8.8.1) 的含义相同，则 E 的两种可能含义均被允许。E . I 的成员查找永远不会模糊，因为在两种情况下 I 必然是类型 E 的成员。换句话说，


规则仅允许访问 E 的静态成员和嵌套类型，而在这种情况下原本会发生编译时错误。[示例：

```
struct Color
{
    public static readonly Color white = new Color(...);
    public static readonly Color Black = new Color(...);
    public Color Complement() {...}
}
class A
{
    public Color Color;            // Field Color of type Color
    void F() {
        Color = Color.Black;       // Refs Color.Black static member
        Color = Color.Complement(); // Invokes Complement() on Color field
    }
    static void G() {
        Color c = Color.White;     // Refs Color.White static member
    }
}
```

在 A 类中，引用 Color 类型的 Color 标识符的出现被下划线标记，而引用 Color 字段的则没有下划线。end example]

## 12.7.6 调用表达式

### 12.7.6.1 通用

调用表达式用于调用方法。

```
invocation-expression:
    primary-expression ( argument-list_opt )
```

调用表达式是动态绑定的 (§12.3.3)，如果满足以下至少一个条件：

- primary-expression 的编译时类型为 dynamic。
- 可选 argument-list 的至少一个参数的编译时类型为 dynamic。

在这种情况下，编译器将调用表达式归类为类型为 dynamic 的值。下面用于确定调用表达式含义的规则随后在运行时应用，使用运行时类型代替具有编译时类型 dynamic 的 primary-expression 和参数的编译时类型。如果 primary-expression 没有编译时类型 dynamic，则方法调用会进行如 §12.6.5 所述的有限编译时检查。

调用表达式的 primary-expression 必须是方法组或 delegate-type 的值。如果 primary-expression 是方法组，则调用表达式是方法调用 (§12.7.6.2)。如果 primary-expression 是 delegate-type 的值，则调用表达式是委托调用 (§12.7.6.4)。如果 primary-expression 既不是方法组也不是 delegate-type 的值，则会发生绑定时错误。

可选的 argument-list (§12.6.2) 为方法参数提供值或变量引用。

求值调用表达式的结果分类如下：

- 如果调用表达式调用的方法或委托返回 void，则结果为空。被分类为空的表达式仅允许在语句表达式 (§13.7) 的上下文中或作为 lambda 表达式 (§12.16) 的主体出现。否则会发生绑定时错误。
- 否则，结果是一个值，其关联类型为方法或委托的返回类型。如果调用的是实例方法，并且接收者是类类型 T，则关联类型是从以 T 开始并搜索其基类时找到的方法的第一个声明或重写中选取的。

### 12.7.6.2 方法调用

对于方法调用，*调用表达式*的 *primary-expression* 必须是方法组。方法组标识要调用的单个方法，或从中选择特定方法调用的重载方法集合。在后一种情况下，要调用的具体方法的确定基于 *argument-list* 中参数类型提供的上下文。

形式为 M(A) 的方法调用的绑定时处理，其中 M 是方法组（可能包括 *type-argument-list*），A 是可选的 *argument-list*，包括以下步骤：

- 构造方法调用的候选方法集合。对于与方法组 M 关联的每个方法 F：
  - 如果 F 是非泛型的，则当满足以下条件时 F 是候选方法：
    - M 没有类型参数列表，且
    - F 相对于 A 是适用的 (§12.6.4.2)。
  - 如果 F 是泛型的且 M 没有类型参数列表，则当满足以下条件时 F 是候选方法：
    - 类型推断 (§12.6.3) 成功，推断出调用的类型参数列表，且
    - 一旦将推断出的类型参数替换为相应的方法类型参数，F 的参数列表中的所有构造类型都满足其约束 (§9.4.5)，并且 F 的参数列表相对于 A 是适用的 (§12.6.4.2)。
  - 如果 F 是泛型的且 M 包含类型参数列表，则当满足以下条件时 F 是候选方法：
    - F 的方法类型参数数量与类型参数列表中提供的数量相同，且
    - 一旦将类型参数替换为相应的方法类型参数，F 的参数列表中的所有构造类型都满足其约束 (§9.4.5)，并且 F 的参数列表相对于 A 是适用的 (§12.6.4.2)。
- 候选方法集合被缩减为仅包含来自最派生类型的 方法：对于集合中的每个方法 C.F，其中 C 是声明方法 F 的类型，所有在 C 的基类型中声明的方法都从集合中移除。此外，如果 C 是 object 以外的类类型，则所有在接口类型中声明的方法都从集合中移除。[注意：此后一条规则仅在方法组是针对具有除 object 以外的有效基类且非空有效接口集的类型参数进行成员查找的结果时才有效。 end note]
- 如果得到的候选方法集合为空，则放弃后续步骤的处理，而是尝试将调用作为扩展方法调用 (§12.7.6.3) 处理。如果此操作失败，则不存在适用的方法，并发生绑定时错误。
- 使用 §12.6.4 的重载解析规则识别候选方法集合中的最佳方法。如果无法识别出单一的最佳方法，则方法调用不明确，并发生绑定时错误。执行重载解析时，泛型方法的参数在将类型参数（提供或推断）替换为相应的方法类型参数后才被考虑。
- 对选定的最佳方法进行最终验证：
  - 在方法组的上下文中验证方法：如果最佳方法是一个静态方法，则方法组应源自 *simple-name* 或通过类型进行的 *member-access*。如果最佳方法是一个实例方法，则方法组应源自 *simple-name*、通过变量或值进行的 member-access，或 base-access。如果这些要求都不成立，则发生绑定时错误。
  - 如果最佳方法是一个泛型方法，则检查类型参数（提供或推断）是否满足泛型方法上声明的约束 (§9.4.5)。如果任何类型参数不满足类型参数上的相应约束，则发生绑定时错误。

一旦通过上述步骤在绑定时选择并验证了方法，实际的运行时调用将根据 §12.6.6 中描述的函数成员调用规则进行处理。

> [注意：上述解析规则的直观效果如下：要定位方法调用所调用的特定方法，从方法调用指示的类型开始，并沿继承链向上查找，直到找到至少一个适用、可访问、非重写的方法声明。然后对该类型中声明的适用、可访问、非重写方法集合执行类型推断和重载解析，并调用由此选定的方法。如果未找到方法，则尝试将其作为扩展方法调用进行处理。 end note]

### 12.7.6.3 扩展方法调用

在形式为以下之一的方法调用 (§12.6.6.2) 中

```
expr . identifier ( )
expr . identifier ( args )
expr . identifier < typeargs > ( )
expr . identifier < typeargs > ( args )
```

如果调用的正常处理未找到适用的方法，则会尝试将该构造作为扩展方法调用进行处理。如果 expr 或任何 args 的编译时类型为 dynamic，则扩展方法不适用。

目标是找到最佳类型名 C，以便可以进行相应的静态方法调用：

```
C . identifier ( expr )
C . identifier ( expr , args )
C . identifier < typeargs > ( expr )
C . identifier < typeargs > ( expr , args )
```

扩展方法 C₁ . Mⱼ 符合条件，如果：

- C₁ 是一个非泛型、非嵌套类
- Mⱼ 的名称是 identifier
- Mⱼ 在作为上述所示的静态方法应用于参数时是可访问且适用的
- 从 expr 到 Mⱼ 的第一个参数的类型存在隐式恒等、引用或装箱转换。

对 C 的搜索按如下进行：

- 从最近的封闭命名空间声明开始，继续每个封闭命名空间声明，并以包含的编译单元结束，依次尝试找到扩展方法的候选集合：
  - 如果给定的命名空间或编译单元直接包含具有符合条件的扩展方法 Mⱼ 的非泛型类型声明 C₁，则这些扩展方法的集合即为候选集合。



- 如果通过 using 命名空间指令在给定命名空间或编译单元中导入的命名空间直接包含带有合格扩展方法 M_j 的非泛型类型声明 C_i，则这些扩展方法的集合就是候选集。
- 如果在任何封闭命名空间声明或编译单元中都找不到候选集，则发生编译时错误。
- 否则，如 §12.6.4 所述对候选集应用重载解析。如果找不到唯一最佳方法，则发生编译时错误。
- C 是其中将最佳方法声明为扩展方法的类型。

然后，以 C 为目标，将该方法调用作为静态方法调用处理（§12.6.6）。[注意：与实例方法调用不同，当 expr 求值为空引用时不会引发异常。相反，此空值将像通过常规静态方法调用那样传递给扩展方法。扩展方法实现负责决定如何响应此类调用。结束注意]

前面的规则意味着：实例方法优先于扩展方法；内部命名空间声明中可用的扩展方法优先于外部命名空间声明中可用的扩展方法；直接在命名空间中声明的扩展方法优先于通过 using 命名空间指令导入到同一命名空间中的扩展方法。（示例：）

```
public static class E
{
    public static void F(this object obj, int i) { }
    public static void F(this object obj, string s) { }
}
class A { }
class B
{
    public void F(int i) { }
}
class C
{
    public void F(object obj) { }
}
class X
{
    static void Test(A a, B b, C c) {
        a.F(1);        // E.F(object, int)
        a.F("hello");  // E.F(object, string)
        b.F(1);        // B.F(int)
        b.F("hello");  // E.F(object, string)
        c.F(1);        // C.F(object)
        c.F("hello");  // C.F(object)
    }
}
```

在该示例中，B 的方法优先于第一个扩展方法，而 C 的方法优先于两个扩展方法。

```csharp
public static class C
{
    public static void F(this int i) { Console.WriteLine("C.F({0})", i); }
    public static void G(this int i) { Console.WriteLine("C.G({0})", i); }
    public static void H(this int i) { Console.WriteLine("C.H({0})", i); }
}
namespace N1
{
    public static class D
    {
        public static void F(this int i) { Console.WriteLine("D.F({0})", i); }
        public static void G(this int i) { Console.WriteLine("D.G({0})", i); }
    }
}
namespace N2
{
    using N1;
    public static class E
    {
        public static void F(this int i) { Console.WriteLine("E.F({0})", i); }
        class Test
        {
            static void Main(string[] args)
            {
                1.F();
                2.G();
                3.H();
            }
        }
    }
}
```

此示例的输出为：

```
E.F(1)
D.G(2)
C.H(3)
```

D.G 优先于 C.G，而 E.F 优先于 D.F 和 C.F。结束示例]

### 12.7.6.4 委托调用

对于委托调用，*调用表达式* 的 *主表达式* 应为 *委托类型* 的值。此外，将 *委托类型* 视为具有与 *委托类型* 相同参数列表的函数成员时，*委托类型* 应相对于 *调用表达式* 的 *参数列表* 是适用的（§12.6.4.2）。

形式为 D(A) 的委托调用的运行时处理（其中 D 是 *委托类型* 的 *主表达式*，A 是可选 *参数列表*）由以下步骤组成：

- 计算 *D*。如果此计算导致异常，则不执行后续步骤。
- 计算参数列表 *A*。如果此计算导致异常，则不执行后续步骤。
- 检查 *D* 的值是否有效。如果 *D* 的值为 `null`，则引发 `System.NullReferenceException`，并且不执行后续步骤。
- 否则，*D* 是对委托实例的引用。对委托的调用列表中的每个可调用实体执行函数成员调用（§12.6.6）。对于由实例和实例方法组成的可调用实体，用于调用的实例是包含在该可调用实体中的实例。

有关不带参数的多个调用列表的详细信息，请参见 §20.6。

## 12.7.7 元素访问

### 12.7.7.1 概述

*元素访问* 由 *主非数组创建表达式*、后跟 "[" 标记、后跟 *参数列表*、后跟 "]" 标记组成。*参数列表* 由一个或多个 *参数* 组成，参数之间用逗号分隔。

```
element-access:
    primary-no-array-creation-expression [ argument-list ]
```

*元素访问* 的 *参数列表* 不允许包含 *ref* 或 *out* 参数。

如果以下条件至少之一成立，则 *元素访问* 是动态绑定的（§12.3.3）：

- *主非数组创建表达式* 的编译时类型为 *dynamic*。
- *参数列表* 中至少一个表达式的编译时类型为 *dynamic*，且 *主非数组创建表达式* 不具有数组类型。

在这种情况下，编译器将 *元素访问* 归类为 *dynamic* 类型的值。然后，在运行时应用下面用于确定 *元素访问* 含义的规则，并对那些编译时类型为 *dynamic* 的 *主非数组创建表达式* 和 *参数列表* 表达式使用运行时类型而非编译时类型。如果 *主非数组创建表达式* 不具有编译时类型 *dynamic*，则元素访问将经历 §12.6.5 所述的有限编译时检查。

如果 *元素访问* 的 *主非数组创建表达式* 是 *数组类型* 的值，则 *元素访问* 是数组访问（§12.7.7.2）。否则，*主非数组创建表达式* 应是具有一个或多个索引器成员的类、结构或接口类型的变量或值，在这种情况下，*元素访问* 是索引器访问（§12.7.7.3）。

### 12.7.7.2 数组访问

对于数组访问，*元素访问* 的 *主非数组创建表达式* 应为 *数组类型* 的值。此外，数组访问的 *参数列表* 不允许包含命名参数。*参数列表* 中的表达式数量应与 *数组类型* 的秩相同，并且每个表达式应具有类型 *int*、*uint*、*long*、*ulong*，或者应可隐式转换为这些类型中的一种或多种。

数组访问的求值结果是数组的元素类型的变量，即由 *参数列表* 中表达式的值所选择的数组元素。

形式为 P[A] 的数组访问的运行时处理（其中 P 是 *数组类型* 的 *主非数组创建表达式*，A 是 *参数列表*）由以下步骤组成：

- 计算 P。如果此计算导致异常，则不执行后续步骤。
- 按从左到右的顺序计算 *参数列表* 的索引表达式。在计算每个索引表达式之后，执行到以下类型之一的隐式转换（§11.2）：*int*、*uint*、*long*、*ulong*。选择此列表中存在隐式转换的第一个类型。例如，如果索引表达式的类型为 *short*，则执行到 *int* 的隐式转换，因为从 *short* 到 *int* 以及从 *short* 到 *long* 的隐式转换都是可能的。如果索引表达式的求值或后续隐式转换导致异常，则不计算其他索引表达式，并且不执行后续步骤。
- 检查 P 的值是否有效。如果 P 的值为 *null*，则引发 *System.NullReferenceException*，并且不执行后续步骤。
- 将 *参数列表* 中每个表达式的值与 P 引用的数组实例的每个维度的实际边界进行核对。如果一个或多个值超出范围，则引发 *System.IndexOutOfRangeException*，并且不执行后续步骤。



计算由索引表达式所给出的数组元素的位置，该位置成为数组访问的结果。

## 12.7.7.3 索引器访问

对于索引器访问，*元素访问* 的 *非数组创建主表达式* 应为类、结构或接口类型的变量或值，并且该类型应实现一个或多个相对于 *元素访问* 的 *参数列表* 适用的索引器。

对形式为 P [A] 的索引器访问（其中 P 是类、结构或接口类型 T 的 *非数组创建主表达式*，A 是 *参数列表*）进行的绑定时间处理包括以下步骤：

- 构造由 T 提供的索引器集合。该集合包含在 T 或 T 的基类型中声明的、不是 *重写* 声明且在当前上下文中可访问的所有索引器（§8.5）。
- 将该集合缩减为适用且未被其他索引器隐藏的索引器。对于集合中的每个索引器 S . I，应用以下规则，其中 S 是声明索引器 I 的类型：
  - 如果 I 相对于 A 不适用（§12.6.4.2），则将 I 从集合中移除。
  - 如果 I 相对于 A 适用（§12.6.4.2），则将 S 的基类型中声明的所有索引器从集合中移除。
  - 如果 I 相对于 A 适用（§12.6.4.2）且 S 是 *object* 以外的类类型，则将接口中声明的所有索引器从集合中移除。
- 如果生成的候选索引器集合为空，则不存在适用的索引器，会发生绑定时间错误。
- 使用 §12.6.4 的重载决策规则确定候选索引器集合中的最佳索引器。如果无法确定唯一的最佳索引器，则索引器访问具有歧义，会发生绑定时间错误。
- *参数列表* 的索引表达式按从左到右的顺序进行计算。处理索引器访问的结果是一个被归类为索引器访问的表达式。该索引器访问表达式引用上一步确定的索引器，并具有关联的 P 实例表达式、关联的 A 参数列表，以及关联的索引器类型。如果 T 是类类型，则从自 T 开始搜索其基类时找到的该索引器的第一个声明或重写中选择关联类型。

根据其使用上下文，索引器访问会调用索引器的 *get 访问器* 或 *set 访问器*。如果索引器访问是赋值的目标，则调用 *set 访问器* 来赋新值（§12.18.2）。在所有其他情况下，调用 *get 访问器* 来获取当前值（§12.2.2）。

## 12.7.8 this 访问

*this 访问* 由关键字 *this* 组成。

```
this-access:
    this
```

*this 访问* 仅允许出现在实例构造函数、实例方法、实例访问器（§12.2.1）或终结器的 *块* 中。它具有以下含义之一：

- 当 *this* 用于类的实例构造函数中的 *主表达式* 时，它被归类为值。该值的类型是使用它的类的实例类型（§15.3.2），该值是对正在构造的对象的引用。
- 当 *this* 用于类的实例方法或实例访问器中的 *主表达式* 时，它被归类为值。该值的类型是使用它的类的实例类型（§15.3.2），该值是对调用该方法或访问器所针对的对象的引用。
- 当 this 用于结构的实例构造函数中的主表达式时，它被归类为变量。该变量的类型是使用它的结构的实例类型（§15.3.2），该变量表示正在构造的结构。
  - 如果构造函数声明没有构造函数初始化程序，则 this 变量的行为与结构类型的 out 参数完全相同。特别是，这意味着该变量必须在实例构造函数的每个执行路径中被明确赋值。
  - 否则，this 变量的行为与结构类型的 ref 参数完全相同。特别是，这意味着该变量被视为初始已赋值。
- 当 this 用于结构的实例方法或实例访问器中的主表达式时，它被归类为变量。该变量的类型是使用它的结构的实例类型（§15.3.2）。
  - 如果该方法或访问器不是迭代器（§15.14）或异步函数（§15.15），则 this 变量表示调用该方法或访问器所针对的结构，其行为与结构类型的 ref 参数完全相同。
  - 如果该方法或访问器是迭代器或异步函数，则 this 变量表示调用该方法或访问器所针对的结构的一个副本，其行为与结构类型的值参数完全相同。

在上述列出的上下文之外，在主表达式中使用 this 是编译时错误。特别是，不能在静态方法、静态属性访问器或字段声明的变量初始化程序中引用 this。

## 12.7.9 base 访问

base 访问由关键字 base 后跟“.”标记、标识符和可选类型参数列表，或后跟括在方括号中的参数列表组成：

```
base-access:
    base . identifier type-argument-list_opt
    base [ argument-list ]
```

base 访问用于访问被当前类或结构中同名成员隐藏的基类成员。base 访问仅允许出现在实例构造函数、实例方法、实例访问器（§12.2.1）或终结器的块中。当 base . I 出现在类或结构中时，I 应表示该类或结构的基类的成员。同样，当 base[E] 出现在类中时，基类中应存在适用的索引器。

在绑定时间，形式为 base . I 和 base[E] 的 base 访问表达式在计算时完全等同于写成 ((B)this).I 和 ((B)this)[E]，其中 B 是该构造所在的类或结构的基类。因此，base . I 和 base[E] 对应于 this . I 和 this[E]，不同之处在于 this 被视为基类的一个实例。

当 base 访问引用虚函数成员（方法、属性或索引器）时，确定在运行时调用哪个函数成员的方式（§12.6.6）会发生变化。所调用的函数成员是通过查找该函数成员相对于 B 的最派生实现（§15.6.4）来确定的（而不是像非 base 访问中通常那样相对于 this 的运行时类型）。因此，在虚函数成员的重写中，可以使用 base 访问来调用该函数成员的继承实现。如果 base 访问引用的函数成员是抽象的，则会发生绑定时间错误。

> [注意：与 this 不同，base 本身不是表达式。它只是用于 base 访问或构造函数初始化程序（§15.11.2）上下文中的关键字。结束注释]

## 12.7.10 后缀递增和递减运算符

```
post-increment-expression:
    primary-expression ++

post-decrement-expression:
    primary-expression --
```

后缀递增或递减运算的操作数应当是归类为变量、属性访问或索引器访问的表达式。运算结果是与操作数类型相同的值。

如果主表达式具有编译时类型 dynamic，则该运算符是动态绑定的（§12.3.3），后缀递增表达式或后缀递减表达式具有编译时类型 dynamic，并在运行时使用主表达式的运行时类型应用以下规则。

如果后缀递增或递减运算的操作数是属性访问或索引器访问，则该属性或索引器应同时具有 get 和 set 访问器。如果不是这种情况，则会发生绑定时间错误。

应用一元运算符重载决策（§12.4.4）来选择特定的运算符实现。预定义的 ++ 和 -- 运算符存在于以下类型：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 以及任何枚举类型。预定义的 ++ 运算符返回将操作数加 1 产生的值，预定义的 -- 运算符返回将操作数减 1 产生的值。在 checked 上下文中，如果此加法或减法的结果超出结果类型的范围，并且结果类型是整型或枚举类型，则抛出 System.OverflowException。

从所选一元运算符的返回类型到主表达式的类型必须存在隐式转换，否则会发生编译时错误。

对形式为 x++ 或 x-- 的后缀递增或递减运算的运行时处理包括以下步骤：

- 如果 x 被归类为变量：
  - 计算 x 以生成该变量。
  - 保存 x 的值。
  - 将 x 的已保存值转换为所选运算符的操作数类型，并以该值作为其参数调用运算符。
  - 将运算符返回的值转换为 x 的类型，并存储到先前计算 x 时给出的位置。
  - x 的已保存值成为运算结果。
- 如果 x 被归类为属性访问或索引器访问：
  - 计算与 x 关联的实例表达式（如果 x 不是静态的）和参数列表（如果 x 是索引器访问），结果用于后续的 get 和 set 访问器调用。
  - 调用 x 的 get 访问器并保存返回的值。
  - 将 x 的已保存值转换为所选运算符的操作数类型，并以该值作为其参数调用运算符。
  - 将运算符返回的值转换为 x 的类型，并以该值作为其 value 参数调用 x 的 set 访问器。
  - x 的已保存值成为运算结果。

++ 和 -- 运算符也支持前缀表示法（§12.8.6）。通常，x++ 或 x-- 的结果是运算前 x 的值，而 ++x 或 --x 的结果是运算后 x 的值。无论哪种情况，x 本身在运算后都具有相同的值。



运算符 ++ 或运算符 -- 实现可以使用后缀或前缀表示法调用。
无法为这两种表示法分别提供运算符实现。

## 12.7.11 new 运算符

### 12.7.11.1 概述

new 运算符用于创建类型的新实例。

new 表达式有三种形式：

- 对象创建表达式和匿名对象创建表达式用于创建类类型和值类型的新实例。
- 数组创建表达式用于创建数组类型的新实例。
- 委托创建表达式用于获取委托类型的实例。

new 运算符意味着创建类型的实例，但不一定意味着分配内存。特别是，值类型的实例除了其所在的变量之外不需要额外的内存，并且当使用 new 创建值类型的实例时不会发生分配。

> [注意：委托创建表达式并不总是创建新实例。当该表达式以与方法组转换（§11.8）或匿名函数转换（§11.7）相同的方式处理时，这可能导致重用现有的委托实例。结束注意]

### 12.7.11.2 对象创建表达式

对象创建表达式用于创建类类型或值类型的新实例。

```
object-creation-expression:
  new type ( argument-list_opt ) object-or-collection-initializer_opt
  new type object-or-collection-initializer

object-or-collection-initializer:
  object-initializer
  collection-initializer
```

对象创建表达式的类型应为类类型、值类型或类型参数。该类型不能是抽象或静态类类型。

- 如果未为 T 指定值类型约束或构造函数约束（§15.2.5），则发生绑定期错误。
- 对象创建表达式的结果是类型参数所绑定到的运行时类型的值，即调用该类型的默认构造函数的结果。运行时类型可以是引用类型或值类型。

- 否则，如果 T 是类类型或结构类型：
  - 如果 T 是抽象或静态类类型，则发生编译时错误。
  - 要调用的实例构造函数使用 §12.6.4 的重载解析规则确定。候选实例构造函数集由 T 中声明的所有可访问实例构造函数组成，这些构造函数相对于 A 是适用的（§12.6.4.2）。如果候选实例构造函数集为空，或无法标识单个最佳实例构造函数，则发生绑定期错误。
  - 对象创建表达式的结果是类型 T 的值，即调用上述步骤中确定的实例构造函数所生成的值。
  - 否则，对象创建表达式无效，并发生绑定期错误。

即使对象创建表达式是动态绑定的，编译时类型仍为 T。

形式为 new T(A) 的对象创建表达式的运行时处理（其中 T 是类类型或结构类型，A 是可选参数列表）由以下步骤组成：

- 如果 T 是类类型：
  - 分配类 T 的新实例。如果没有足够的内存可用于分配新实例，则引发 System.OutOfMemoryException，并且不执行后续步骤。
  - 新实例的所有字段都初始化为其默认值（§10.3）。
  - 根据函数成员调用规则（§12.6.6）调用实例构造函数。对新分配实例的引用会自动传递给实例构造函数，并且可以在该构造函数内作为 this 访问该实例。

- 如果 T 是结构类型：
  - 通过分配临时局部变量创建类型 T 的实例。由于结构类型的实例构造函数必须为所创建实例的每个字段明确赋值，因此不需要初始化临时变量。
  - 根据函数成员调用规则（§12.6.6）调用实例构造函数。对新分配实例的引用会自动传递给实例构造函数，并且可以在该构造函数内作为 this 访问该实例。

### 12.7.11.3 对象初始值设定项

对象初始值设定项指定对象的零个或多个字段或属性的值。

```
object-initializer:
    { member-initializer-list_opt }
    { member-initializer-list , }

member-initializer-list:
    member-initializer
    member-initializer-list , member-initializer

member-initializer:
    identifier = initializer-value

initializer-value:
    expression
    object-or-collection-initializer
```

对象初始值设定项由一系列成员初始值设定项组成，这些成员初始值设定项用 { 和 } 标记括起并用逗号分隔。每个成员初始值设定项应命名正在初始化的对象的可访问字段或属性，后跟等号以及表达式、对象初始值设定项或集合初始值设定项。对象初始值设定项为同一字段或属性包含多个成员初始值设定项是错误的。对象初始值设定项不可能引用其正在初始化的新创建对象。

在等号后指定表达式的成员初始值设定项，其处理方式与对字段或属性的赋值（§12.18.2）相同。

在等号后指定对象初始值设定项的成员初始值设定项是嵌套对象初始值设定项，即嵌入对象的初始化。嵌套对象初始值设定项中的赋值不是为字段或属性赋予新值，而是被视为对字段或属性成员的赋值。嵌套对象初始值设定项不能应用于具有值类型的属性，也不能应用于具有值类型的只读字段。

在等号后指定集合初始值设定项的成员初始值设定项是嵌入集合的初始化。不是将新集合赋给字段或属性，而是将初始值设定项中给定的元素添加到字段或属性引用的集合中。该字段或属性应为满足 §12.7.11.4 中指定要求的集合类型。

[示例：以下类表示具有两个坐标的点：

```
public class Point
{
    int x, y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

Point 的实例可以如下创建并初始化：

```
Point a = new Point { X = 0, Y = 1 };
```

其效果与以下相同

```
Point __a = new Point();
__a.X = 0;
__a.Y = 1;
Point a = __a;
```

其中 __a 是其他情况下不可见且不可访问的临时变量。以下类表示由两个点创建的矩形：

```
public class Rectangle
{
    Point p1, p2;
    public Point P1 { get { return p1; } set { p1 = value; } }
    public Point P2 { get { return p2; } set { p2 = value; } }
}
```

Rectangle 的实例可以如下创建并初始化：

```
Rectangle r = new Rectangle {
    P1 = new Point { X = 0, Y = 1 },
    P2 = new Point { X = 2, Y = 3 }
};
```

其效果与以下相同

```
Rectangle __r = new Rectangle();
Point __p1 = new Point();
__p1.X = 0;
__p1.Y = 1;
__r.P1 = __p1;
Point __p2 = new Point();
__p2.X = 2;
__p2.Y = 3;
__r.P2 = __p2;
Rectangle r = __r;
```

其中 __r、__p1 和 __p2 是其他情况下不可见且不可访问的临时变量。

如果 Rectangle 的构造函数分配两个嵌入的 Point 实例

```
public class Rectangle
{
    Point p1 = new Point();
    Point p2 = new Point();
    public Point P1 { get { return p1; } }
    public Point P2 { get { return p2; } }
}
```

则可以使用以下构造来初始化嵌入的 Point 实例，而不是赋予新实例：

```
Rectangle r = new Rectangle {
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```

其效果与以下相同

```
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

结束示例]

### 12.7.11.4 集合初始值设定项

集合初始值设定项指定集合的元素。

```
collection-initializer:
    { element-initializer-list }
    { element-initializer-list , }

element-initializer-list:
    element-initializer
    element-initializer-list , element-initializer

element-initializer:
    non-assignment-expression
    { expression-list }

expression-list:
    expression
    expression-list , expression
```

集合初始值设定项由一系列元素初始值设定项组成，这些元素初始值设定项用 { 和 } 标记括起并用逗号分隔。每个元素初始值设定项指定要添加到正在初始化的集合对象中的元素，并由用 { 和 } 标记括起并用逗号分隔的表达式列表组成。单表达式元素初始值设定项可以在不带大括号的情况下编写，但此时不能是赋值



第一种形式的数组创建表达式分配一个数组实例，其类型由从表达式列表中删除各个表达式后得到。[示例：数组创建表达式 new int[10,20] 生成一个类型为 int[,] 的数组实例，而数组创建表达式 new int[10] [,] 生成一个类型为 int[][] 的数组实例。示例结束] 表达式列表中的每个表达式应具有类型 int、uint、long 或 ulong，或者可隐式转换为这些类型中的一种或多种。每个表达式的值确定新分配数组实例中对应维度的长度。由于数组维度的长度应为非负，因此在表达式列表中包含值为负的常量表达式是编译时错误。

除在不安全上下文（§23.2）中以外，数组的布局未指定。

如果第一种形式的数组创建表达式包含数组初始值设定项，则表达式列表中的每个表达式应为常量，并且表达式列表指定的秩和维度长度应与数组初始值设定项的秩和维度长度匹配。

在第二种或第三种形式的数组创建表达式中，指定数组类型的秩或秩说明符应与数组初始值设定项的秩匹配。各个维度长度从数组初始值设定项中每个对应嵌套层级的元素数量推断出来。因此，表达式

```
new int[,] {{0, 1}, {2, 3}, {4, 5}}
```

完全对应于

```
new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}
```

第三种形式的数组创建表达式称为隐式类型数组创建表达式。它与第二种形式类似，不同之处在于数组的元素类型不是显式给出的，而是确定为数组初始值设定项中表达式集合的最佳公共类型（§12.6.3.15）。对于多维数组，即秩说明符包含至少一个逗号的数组，该集合包括嵌套数组初始值设定项中找到的所有表达式。

数组初始值设定项在 §17.7 中进一步描述。

计算数组创建表达式的结果被归类为值，即对新分配数组实例的引用。数组创建表达式的运行时处理包括以下步骤：

- 表达式列表的维度长度表达式按从左到右的顺序计算。在计算每个表达式之后，执行到以下类型之一的隐式转换（§11.2）：int、uint、long、ulong。选择此列表中存在隐式转换的第一种类型。如果计算表达式或后续隐式转换导致异常，则不再计算其他表达式，也不再执行后续步骤。
- 按如下方式验证计算出的维度长度值：如果一个或多个值小于零，则引发 System.OverflowException，并且不再执行后续步骤。
- 分配具有给定维度长度的数组实例。如果没有足够的内存可用于分配新实例，则引发 System.OutOfMemoryException，并且不再执行后续步骤。
- 新数组实例的所有元素都初始化为其默认值（§10.3）。
- 如果数组创建表达式包含数组初始值设定项，则计算数组初始值设定项中的每个表达式，并将其赋给对应的数组元素。计算和赋值按表达式在数组初始值设定项中编写的顺序执行——换句话说，元素按递增的索引顺序初始化，其中最右侧维度最先递增。如果计算给定表达式或后续对相应数组元素的赋值导致异常，则不再初始化其他元素（因此其余元素将具有其默认值）。

数组创建表达式允许实例化元素为数组类型的数组，但此类数组的元素应手动初始化。[示例：语句

```
int[][] a = new int[100][];
```

创建一个包含 100 个 int[] 类型元素的一维数组。每个元素的初始值为 null。同一个数组创建表达式不可能同时实例化子数组，而语句

```
int[][] a = new int[100][5];    // Error
```

会导致编译时错误。子数组的实例化可以改为手动执行，如下所示

```
int[][] a = new int[100][];
for (int i = 0; i < 100; i++) a[i] = new int[5];
```

示例结束

[注意：当数组的数组具有“矩形”形状，即所有子数组长度相同时，使用多维数组更高效。在上面的示例中，实例化数组的数组会创建 101 个对象——一个外部数组和 100 个子数组。相反，int[,] a = new int[100, 5]; 只创建一个对象，即一个二维数组，并在单条语句中完成分配。注意结束]

[示例：以下是隐式类型数组创建表达式的示例：

```
var a = new[] { 1, 10, 100, 1000 };                  // int[]
var b = new[] { 1.5, 2, 2.5 };                       // double[]
var c = new[, ] { { "hello", null }, { "world", "!" } }; // string[,]
var d = new[] { 1, "one", 2, "two" };                // Error
```

最后一个表达式导致编译时错误，因为 int 和 string 都不能隐式转换为对方，因此不存在最佳公共类型。在这种情况下必须使用显式类型数组创建表达式，例如指定类型为 object[]。或者，可以将其中一个元素强制转换为公共基类型，然后该类型将成为推断出的元素类型。示例结束

隐式类型数组创建表达式可以与匿名对象初始值设定项（§12.7.11.7）组合，以创建匿名类型的数据结构。[示例：

```
var contacts = new[] {
    new {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0101", "425-882-8080" }
    },
    new {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

示例结束

## 12.7.11.6 委托创建表达式

委托创建表达式用于获取委托类型的实例。

```
delegate-creation-expression:
    new delegate-type ( expression )
```

委托创建表达式的参数应为方法组、匿名函数，或者编译时类型 dynamic 或委托类型的值。如果参数是方法组，则它标识方法；对于实例方法，还标识要为其创建委托的对象。如果参数是匿名函数，则它直接定义委托目标的参数和方法体。如果参数是值，则它标识要创建其副本的委托实例。

如果表达式的编译时类型为 dynamic，则委托创建表达式进行动态绑定（§12.7.11.6），并且下面的规则在运行时使用表达式的运行时类型来应用。否则，这些规则在编译时应用。

形式为 new D(E) 的委托创建表达式（其中 D 是委托类型，E 是表达式）的绑定期处理包括以下步骤：

- 如果 E 是方法组，则委托创建表达式的处理方式与从 E 到 D 的方法组转换（§11.8）相同。
- 如果 E 是匿名函数，则委托创建表达式的处理方式与从 E 到 D 的匿名函数转换（§11.7）相同。
- 如果 E 是值，则 E 应与 D 兼容（§20.2），并且结果是对新创建的委托的引用，该委托具有调用 E 的单条目调用列表。

形式为 new D(E) 的委托创建表达式（其中 D 是委托类型，E 是表达式）的运行时处理包括以下步骤：

- 如果 E 是方法组，则委托创建表达式作为从 E 到 D 的方法组转换（§11.8）来计算。
- 如果 E 是匿名函数，则委托创建作为从 E 到 D 的匿名函数转换（§11.7）来计算。
- 如果 E 是委托类型的值：
  - 计算 E。如果此计算导致异常，则不再执行后续步骤。
  - 如果 E 的值为 null，则引发 System.NullReferenceException，并且不再执行后续步骤。
  - 分配委托类型 D 的新实例。如果没有足够的内存可用于分配新实例，则引发 System.OutOfMemoryException，并且不再执行后续步骤。
  - 新委托实例使用调用 E 的单条目调用列表初始化。

委托的调用列表在委托实例化时确定，然后在委托的整个生存期内保持不变。换句话说，一旦创建了委托，就不可能更改该委托的目标可调用实体。[注意：请记住，当两个委托组合或从一个委托中移除另一个委托时，会产生一个新的委托；任何现有委托的内容都不会改变。注意结束]

不可能创建引用属性、索引器、用户定义运算符、实例构造函数、终结器或静态构造函数的委托。

[示例：如上所述，当从方法组创建委托时，委托的形参列表和返回类型决定选择哪个重载方法。在下面的示例中

```
delegate double DoubleFunc(double x);
class A
{
    DoubleFunc f = new DoubleFunc(Square);
    static float Square(float x) {
        return x * x;
    }
    static double Square(double x) {
        return x * x;
    }
}
```

A.f 字段使用引用第二个 Square 方法的委托初始化，因为该方法与 DoubleFunc 的形参列表和返回类型完全匹配。如果第二个 Square 方法不存在，则会发生编译时错误。示例结束]



## 12.7.11.7 匿名对象创建表达式

匿名对象创建表达式用于创建匿名类型的对象。

```
anonymous-object-creation-expression:
    new anonymous-object-initializer

anonymous-object-initializer:
    { member-declarator-list_opt }
    { member-declarator-list , }

member-declarator-list:
    member-declarator
    member-declarator-list , member-declarator

member-declarator:
    simple-name
    member-access
    base-access
    identifier = expression
```

匿名对象初始化器声明一个匿名类型并返回该类型的实例。匿名类型是一种无名类类型，直接继承自 object。匿名类型的成员是从用于创建该类型实例的匿名对象初始化器推断出来的一系列只读属性。具体来说，形式为的匿名对象初始化器

```
new { p1 = e1 , p2 = e2 , ... pn = en }
```

声明形式为的匿名类型

```
class __Anonymous1
{
    private readonly T1 f1 ;
    private readonly T2 f2 ;
    ...
    private readonly Tn fn ;
    public __Anonymous1(T1 a1, T2 a2,..., Tn an) {
        f1 = a1 ;
        f2 = a2 ;
        ...
        fn = an ;
    }
    public T1 p1 { get { return f1 ; } }
    public T2 p2 { get { return f2 ; } }
    ...
    public Tn pn { get { return fn ; } }
    public override bool Equals(object __o) { ... }
    public override int GetHashCode() { ... }
}
```

其中每个 T_i 是对应表达式 e_i 的类型。member-declarator 中使用的表达式必须具有类型。因此，member-declarator 中的表达式为 null 或匿名函数是编译时错误。表达式具有不安全类型也是编译时错误。

匿名类型的名称及其 Equals 方法的参数名称由编译器自动生成，不能在程序文本中引用。

在同一程序中，指定相同名称且编译时类型相同且顺序相同的属性序列的两个匿名对象初始化器将产生同一匿名类型的实例。

[Example: 在示例中

```
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```

最后一行的赋值是允许的，因为 p1 和 p2 是同一匿名类型的。结束示例

匿名类型上的 Equals 和 GetHashCode 方法重写了从 object 继承的方法，并根据属性的 Equals 和 GetHashCode 定义，因此同一匿名类型的两个实例相等当且仅当它们的所有属性都相等。

member declarator 可以缩写为 simple name (§12.7.3)、member access (§12.7.5) 或 base access (§12.7.9)。这称为投影初始化器，是对具有相同名称的属性的声明和赋值的简写。具体来说，形式为的 member declarators

identifier          expr . identifier

分别精确等价于以下内容：

identifier = identifier          identifier = expr . identifier

因此，在投影初始化器中，identifier 同时选择值以及要将值赋给的字段或属性。直观地说，投影初始化器不仅投影值，还投影值的名称。

## 12.7.12 typeof 运算符

typeof 运算符用于获取类型的 System.Type 对象。

```
typeof-expression:
    typeof ( type )
    typeof ( unbound-type-name )
    typeof ( void )

unbound-type-name:
    identifier generic-dimension-specifieropt
    identifier :: identifier generic-dimension-specifieropt
    unbound-type-name . identifier generic-dimension-specifieropt

generic-dimension-specifier:
    < commasopt >
commas:
    ,
    commas ,
```

typeof-expression 的第一种形式由 typeof 关键字后跟带括号的类型组成。此形式表达式的结果是所指示类型的 System.Type 对象。任何给定类型只有一个 System.Type 对象。这意味着对于类型 T，typeof(T) == typeof(T) 始终为 true。类型不能是 dynamic。

第二种形式由 typeof 关键字后跟带括号的 unbound-type-name 组成。[注意：unbound-type-name 与 type-name (§8.8) 非常相似，只是 unbound-type-name 包含 generic-dimension-specifiers 而 type-name 包含 type-argument-lists。结束注释] 当 typeof-expression 的操作数是同时满足 unbound-type-name 和 type-name 文法的标记序列时，即当它既不包含 generic-dimension-specifier 也不包含

type-argument-list 时，该标记序列被视为 type-name。unbound-type-name 的含义确定如下：

- 将标记序列转换为 type-name，用具有相同数量逗号且每个 type-argument 均为关键字 object 的 type-argument-list 替换每个 generic-dimension-specifier。
- 在忽略所有类型参数约束的同时求值 resulting type-name。
- unbound-type-name 解析为与 resulting constructed type 关联的 unbound generic type (§9.4)。

typeof-expression 的结果是 resulting unbound generic type 的 System.Type 对象。

第三种形式由 typeof 关键字后跟带括号的 void 关键字组成。此形式表达式的结果是表示类型缺失的 System.Type 对象。typeof(void) 返回的类型对象与为任何类型返回的类型对象不同。[注意：此特殊类型对象在允许对语言中方法进行反射的类库中很有用，其中这些方法希望用 System.Type 的实例来表示任何方法的返回类型，包括 void 方法。结束注释]

typeof 运算符可用于类型参数。结果是绑定到类型参数的运行时类型的 System.Type 对象。typeof 运算符也可以用于 constructed type 或 unbound generic type (§9.4.4)。unbound generic type 的 System.Type 对象与 instance type (§15.3.2) 的 System.Type 对象不同。instance type 在运行时始终是 closed constructed type，因此其 System.Type 对象取决于正在使用的运行时类型参数。另一方面，unbound generic type 没有类型参数，并且无论运行时类型参数如何都产生相同的 System.Type 对象。

[Example: 示例

```
using System;
class X<T>
{
  public static void PrintTypes() {
    Type[] t = {
      typeof(int),
      typeof(System.Int32),
      typeof(string),
      typeof(double[]),
      typeof(void),
      typeof(T),
      typeof(X<T>),
      typeof(X<<T>>),
      typeof(X<>)
    };
    for (int i = 0; i < t.Length; i++) {
      Console.WriteLine(t[i]);
    }
  }
}
class Test
{
  static void Main() {
    X<int>.PrintTypes();
  }
}
```

产生以下输出：

```
System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X<T>[System.Int32]
X<T>[X<T>[System.Int32]]
X<T>
```

请注意 int 和 System.Int32 是同一类型。

typeof(X<>) 的结果不依赖于类型参数，但 typeof(X<T>) 的结果依赖于类型参数。

结束示例

## 12.7.13 sizeof 运算符

sizeof 运算符返回给定类型变量占用的 8 位字节数。作为 sizeof 操作数的类型必须是 unmanaged-type (§23.3)。

对于某些预定义类型，sizeof 运算符产生如下表所示的常量 int 值：

| 表达式 | 结果 |
|---|---|
| sizeof(sbyte) | 1 |
| sizeof(byte) | 1 |
| sizeof(short) | 2 |
| sizeof(ushort) | 2 |
| sizeof(int) | 4 |
| sizeof(uint) | 4 |
| sizeof(long) | 8 |
| sizeof(ulong) | 8 |
| sizeof(char) | 2 |
| sizeof(float) | 4 |
| sizeof(double) | 8 |
| sizeof(bool) | 1 |
| sizeof(decimal) | 16 |

对于枚举类型 T，表达式 sizeof(T) 的结果是等于其基础类型的大小的常量值，如上所述。对于所有其他操作数类型，sizeof 运算符在 §23.6.9 中指定。

## 12.7.14 checked 和 unchecked 运算符

checked 和 unchecked 运算符用于控制整数类型算术运算和转换的溢出检查上下文。

```
checked-expression:
    checked ( expression )

unchecked-expression:
    unchecked ( expression )
```

checked 运算符在 checked 上下文中求值包含的表达式，而 unchecked 运算符在 unchecked 上下文中求值包含的表达式。checked-expression 或 unchecked-expression 与带括号的表达式 (§12.7.4) 完全对应，只是包含的表达式在给定的溢出检查上下文中求值。



溢出检查上下文也可以通过 checked 和 unchecked 语句来控制 (§13.12)。

以下操作会受到 checked 和 unchecked 运算符和语句所建立的溢出检查上下文的影响：

-   预定义的 ++ 和 -- 运算符 (§12.7.10 和 §12.8.6)，当操作数为整型或枚举类型时。
-   预定义的 − 一元运算符 (§12.8.3)，当操作数为整型时。
-   预定义的 +, −, *, 和 / 二元运算符 (§12.9)，当两个操作数均为整型或枚举类型时。
-   显式数值转换 (§11.3.2)，从一种整型或枚举类型到另一种整型或枚举类型，或从 float 或 double 到整型或枚举类型。

当上述任一操作产生的结果太大而无法在目标类型中表示时，执行该操作的上下文控制所得行为：

-   在 checked 上下文中，如果该操作是常量表达式 (§12.20)，则会发生编译时错误。否则，当操作在运行时执行时，会抛出 System.OverflowException。
-   在 unchecked 上下文中，结果会通过丢弃不适合目标类型的任何高位来截断。

对于未被任何 checked 或 unchecked 运算符或语句包围的非常量表达式 (§12.20)（在运行时求值的表达式），默认的溢出检查上下文为 unchecked，除非外部因素（如编译器开关和执行环境配置）要求进行 checked 评估。

对于常量表达式 (§12.20)（可在编译时完全求值的表达式），默认的溢出检查上下文始终为 checked。除非常量表达式被显式置于 unchecked 上下文中，否则在表达式编译时求值期间发生的溢出始终会导致编译时错误。

匿名函数的函数体不受匿名函数所在 checked 或 unchecked 上下文的影响。

[示例：在以下代码中

```
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;
    static int F() {
        return checked(x * y);    // Throws OverflowException
    }
    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }
    static int H() {
        return x * y;             // Depends on default
    }
}
```

未报告编译时错误，因为这两个表达式都无法在编译时求值。在运行时，F 方法抛出 System.OverflowException，而 G 方法返回 -727379968（超出范围结果的低 32 位）。H 方法的行为取决于编译的默认溢出检查上下文，但它要么与 F 相同，要么与 G 相同。 end example

[示例：在以下代码中

```
class Test
{
    const int x = 1000000;
    const int y = 1000000;
    static int F() {
        return checked(x * y);    // Compile-time error, overflow
    }
    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }
    static int H() {
        return x * y;             // Compile-time error, overflow
    }
}
```

在 F 和 H 中求值常量表达式时发生的溢出会导致报告编译时错误，因为这些表达式是在 checked 上下文中求值的。在 G 中求值常量表达式时也会发生溢出，但由于求值是在 unchecked 上下文中进行的，因此不会报告溢出。 end example

checked 和 unchecked 运算符仅影响在 "(" 和 ")" 标记内文本包含的那些操作的溢出检查上下文。运算符对因求值包含的表达式而被调用的函数成员没有影响。 [示例：在以下代码中

```
class Test
{
    static int Multiply(int x, int y) {
        return x * y;
    }
    static int F() {
        return checked(Multiply(1000000, 1000000));
    }
}
```

在 F 中使用 checked 不会影响 Multiply 中 x * y 的求值，因此 x * y 是在默认溢出检查上下文中求值的。 end example

unchecked 运算符在以十六进制表示法编写有符号整型常数时很方便。 [示例：]

```
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

上述两个十六进制常量均为 uint 类型。因为这些常量超出了 int 范围，所以如果没有 unchecked 运算符，强制转换为 int 将会产生编译时错误。 end example

[注意：checked 和 unchecked 运算符和语句允许程序员控制某些数值计算的某些方面。然而，某些数值运算符的行为取决于其操作数的数据类型。例如，即使在显式的 unchecked 构造中相乘两个 decimal 也始终会在溢出时导致异常。同样，即使在显式的 checked 构造中相乘两个 float 也永远不会在溢出时导致异常。此外，其他运算符不受检查模式的影响，无论是默认还是显式。 end note]

### 12.7.15 默认值表达式

默认值表达式用于获取类型默认值 (§10.3)。通常默认值表达式用于类型参数，因为可能不知道类型参数是值类型还是引用类型。（除非已知类型参数是引用类型 (§9.2)，否则不存在从 null 字面量 (§7.4.5.7) 到类型参数的转换。）

```
default-value-expression:
  default ( type )
```

如果 default-value-expression 中的类型在运行时求值为引用类型，则结果为转换为该类型的 null。如果 default-value-expression 中的类型在运行时求值为值类型，则结果为该值类型的默认值 (§9.3.3)。

如果 type 是引用类型或已知为引用类型的类型参数 (§9.2)，则 default-value-expression 是常量表达式 (§12.20)。此外，如果 type 是以下值类型之一，则 default-value-expression 也是常量表达式：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool，或任何枚举类型。

### 12.7.16 匿名方法表达式

匿名方法表达式是定义匿名函数的两种方式之一。它们在 §12.16 中进一步描述。

## 12.8 一元运算符

### 12.8.1 通用

+、-、!、~、++、--、cast 和 await 运算符称为一元运算符。

```
unary-expression:
  primary-expression
  + unary-expression
  - unary-expression
  ! unary-expression
  ~ unary-expression
  pre-increment-expression
  pre-decrement-expression
  cast-expression
  await-expression
```

如果 unary-expression 的操作数具有编译时类型 dynamic，则它会被动态绑定 (§12.3.3)。在这种情况下，unary-expression 的编译时类型为 dynamic，并且下面描述的解析将在运行时使用操作数的运行时类型进行。

### 12.8.2 一元加运算符

对于形式为 +x 的操作，将应用一元运算符重载解析 (§12.4.4) 来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。预定义的一元加运算符为：

```
int operator +(int x);
uint operator +(uint x);
long operator +(long x);
ulong operator +(ulong x);
float operator +(float x);
double operator +(double x);
decimal operator +(decimal x);
```

对于这些运算符中的每一个，结果只是操作数的值。

上述定义的未提升预定义一元加运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.8.3 一元减运算符

对于形式为 -x 的操作，将应用一元运算符重载解析 (§12.4.4) 来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。预定义的一元减运算符为：

-   整数取反：

```
int operator -(int x);
long operator -(long x);
```

结果是通过从零中减去 x 计算得出的。如果 x 的值是操作数类型的最小可表示值（int 为 −2³¹ 或 long 为 −2⁶³），则 x 的数学否定在操作数类型内不可表示。如果这发生在 checked 上下文中，则会抛出 System.OverflowException；如果这发生在 unchecked 上下文中，则结果为操作数的值且不报告溢出。

如果取反运算符的操作数为 uint 类型，则它会被转换为 long 类型，结果的类型为 long。例外是允许 int 值 −2147483648 (−2³¹) 作为十进制整数字面量编写的规则 (§7.4.5.3)。

如果取反运算符的操作数为 ulong 类型，则会发生编译时错误。例外是允许 long 值 −9223372036854775808 (−2⁶³) 作为十进制整数字面量编写的规则 (§7.4.5.3)。

-   浮点取反：

```
float operator -(float x);
double operator -(double x);
```

结果是 x 的值符号反转。如果 x 为 NaN，则结果也为 NaN。

-   十进制取反：

```
decimal operator -(decimal x);
```

结果是通过从零中减去 x 计算得出的。十进制取反等同于使用类型 System.Decimal 的一元减运算符。

上述定义的未提升预定义一元减运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.8.4 逻辑否定运算符

### 12.8.5 按位取反运算符



对于这些运算符中的每一个，运算结果都是对 x 的按位求补。

每个枚举类型 E 都隐式提供以下按位求补运算符：

```
E operator ~(E x);
```

对 ~x 进行求值的结果（其中 x 是枚举类型 E 的一个表达式，其基础类型为 U）与对 (E)(~(U)x) 进行求值完全相同，只是到 E 的转换始终按照如同在未检查上下文（§12.7.14）中执行的方式进行。

上面定义的非提升的预定义按位求补运算符的提升形式（§12.4.8）也是预定义的。

## 12.8.6 前缀增量和减量运算符

```
pre-increment-expression:
    ++ unary-expression

pre-decrement-expression:
    -- unary-expression
```

前缀增量或减量运算的操作数应为分类为变量、属性访问或索引器访问的表达式。运算结果是与该操作数类型相同的值。

如果前缀增量或减量运算的操作数是属性或索引器访问，则该属性或索引器应同时具有 get 和 set 访问器。如果不是这种情况，则会发生绑定时间错误。

应用一元运算符重载决策（§12.4.4）来选择特定的运算符实现。对于以下类型存在预定义的 ++ 和 -- 运算符：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 以及任何枚举类型。预定义的 ++ 运算符返回操作数加 1 所产生的值，预定义的 -- 运算符返回操作数减 1 所产生的值。在已检查上下文中，如果此加法或减法的结果超出结果类型的范围，并且结果类型是整型或枚举类型，则抛出 System.OverflowException。

从所选一元运算符的返回类型到主表达式的类型应存在隐式转换，否则会发生编译时错误。

形式为 ++x 或 --x 的前缀增量或减量运算的运行时处理包括以下步骤：

- 如果 x 被分类为变量：
  - 对 x 进行求值以生成该变量。
  - 将 x 的值转换为所选运算符的操作数类型，并以该值作为参数调用运算符。
  - 将运算符返回的值转换为 x 的类型。生成的该值存储在对 x 求值所得到的位置中。
  - 该值成为操作的结果。
- 如果 x 被分类为属性或索引器访问：
  - 将与 x 关联的实例表达式（如果 x 不是静态的）和参数列表（如果 x 是索引器访问）进行求值，并将结果用于随后的 get 和 set 访问器调用。
  - 调用 x 的 get 访问器。
  - 将 get 访问器返回的值转换为所选运算符的操作数类型，并以该值作为参数调用运算符。
  - 将运算符返回的值转换为 x 的类型。调用 x 的 set 访问器，并将此值作为其 value 参数。
- 该值也成为操作的结果。

++ 和 -- 运算符还支持后缀表示法（§12.7.10）。通常，x++ 或 x-- 的结果是操作 *之前* x 的值，而 ++x 或 --x 的结果是操作 *之后* x 的值。在任何一种情况下，x 本身在操作后具有相同的值。

operator ++ 或 operator -- 的实现可以使用后缀或前缀表示法调用。不可能为这两种表示法分别提供运算符实现。

上面定义的非提升的预定义前缀增量和减量运算符的提升形式（§12.4.8）也是预定义的。

## 12.8.7 强制转换表达式

*强制转换表达式* 用于将表达式显式转换为给定的类型。

```
cast-expression:
    ( type ) unary-expression
```

形式为 (T)E 的 *强制转换表达式*（其中 T 是 *类型*，E 是 *一元表达式*）执行将 E 的值显式转换（§11.3）为 *类型* T。如果不存在从 E 到 T 的显式转换，则发生绑定时间错误。否则，结果为显式转换生成的值。结果始终分类为值，即使 E 表示变量。

*强制转换表达式* 的语法会导致某些语法歧义。[示例：表达式 (x)–y 既可以解释为 *强制转换表达式*（将 –y 强制转换为 *类型* x），也可以解释为 *加法表达式* 与 *带括号的表达式* 的组合（计算值 x – y）。结束示例]

为了消除 *强制转换表达式* 的歧义，存在以下规则：仅当以下条件中至少一个为真时，一个或多个用括号括起来的 *标记*（§7.4）序列才被视为 *强制转换表达式* 的开头：

- 标记序列是 *类型* 的正确语法，但不是 *表达式* 的正确语法。
- 标记序列是 *类型* 的正确语法，并且紧跟右括号之后的标记是标记“~”、标记“!”、标记“(”、*标识符*（§7.4.3）、*字面量*（§7.4.5）或除 **as** 和 **is** 之外的任何 *关键字*（§7.4.4）。

上面的术语“正确语法”仅指标记序列应符合特定的语法产生式。它特别不考虑任何组成标识符的实际含义。[示例：如果 x 和 y 是标识符，则 x.y 是 *类型* 的正确语法，即使 x.y 实际上并不表示类型。结束示例]

[注意：根据消歧规则，如果 x 和 y 是标识符，则 (x)y、(x)(y) 和 (x)(-y) 是 *强制转换表达式*，但 (x)-y 不是，即使 x 表示一个类型。但是，如果 x 是表示预定义类型（如 int）的关键字，则所有四种形式都是 *强制转换表达式*（因为这样的关键字本身不可能是一个表达式）。结束注释]

## 12.8.8 await 表达式

### 12.8.8.1 一般性说明

*await* 运算符用于挂起对包含它的 *async* 函数的求值，直到操作数所表示的异步操作完成。

```
await-expression:
    await unary-expression
```

*await 表达式* 只允许出现在 *async* 函数（§15.15）的主体中。在最近的外围 *async* 函数中，*await 表达式* 不得出现在以下位置：

- 在嵌套的（*非 async*）匿名函数内
- 在 *try 语句* 的 catch 或 finally 块中
- 在 *lock 语句* 的块内
- 在匿名函数转换为表达式树类型（§11.7.3）时
- 在不安全上下文中

[注意：*await 表达式* 不能出现在 *查询表达式* 中的大多数位置，因为这些位置在语法上会被转换为使用非 async lambda 表达式。结束注释]

在 async 函数内，*await* 不得用作 *可用标识符*，但可以使用逐字标识符 *@await*。因此，await 表达式与涉及标识符的各种表达式之间没有语法歧义。在 async 函数外部，*await* 作为普通标识符使用。

*await 表达式* 的操作数称为 *任务*。它表示一个异步操作，该操作在求值 *await 表达式* 时可能已完成，也可能未完成。await 运算符的目的是挂起包含它的 async 函数的执行，直到所等待的任务完成，然后获取其结果。

### 12.8.8.2 可等待的表达式

await 表达式的任务必须是 *可等待的*。如果满足以下条件之一，则表达式 *t* 是可等待的：

- *t* 的编译时类型为 *dynamic*
- *t* 具有可访问的、名为 *GetAwaiter* 的实例方法或扩展方法，该方法没有参数且没有类型参数，并且其返回类型 *A* 满足以下所有条件：
  - *A* 实现接口 *System.Runtime.CompilerServices.INotifyCompletion*（以下简称为 *INotifyCompletion*）
  - *A* 具有可访问的、可读的 *bool* 类型实例属性 *IsCompleted*
  - *A* 具有可访问的实例方法 *GetResult*，该方法没有参数且没有类型参数

*GetAwaiter* 方法的目的是为任务获取一个 *等待器*。类型 *A* 称为 await 表达式的 *等待器类型*。

*IsCompleted* 属性的目的是确定任务是否已经完成。如果是，则无需挂起求值。

*INotifyCompletion.OnCompleted* 方法的目的是为任务注册一个“延续”；即一个委托（类型为 *System.Action*），该委托将在任务完成时被调用。

*GetResult* 方法的目的是在任务完成后获取任务的结果。该结果可能是成功完成，可能带有结果值，也可能是由 *GetResult* 方法抛出的异常。

### 12.8.8.3 await 表达式的分类

表达式 *await t* 与表达式 *(t).GetAwaiter().GetResult()* 的分类方式相同。因此，如果 *GetResult* 的返回类型是 *void*，则 *await 表达式* 被分类为无。如果它有非 void 返回类型 *T*，则 *await 表达式* 被分类为 *T* 类型的值。

### 12.8.8.4 await 表达式的运行时求值

在运行时，表达式 *await t* 按如下方式求值：

- 通过对表达式 *(t).GetAwaiter()* 求值获取等待器 *a*。
- 通过对表达式 *(a).IsCompleted* 求值获取 *bool* 值 *b*。



在检查上下文中，如果乘积超出结果类型的范围，则会抛出 System.OverflowException。在未检查上下文中，不会报告溢出，并且结果类型范围之外的任何重要高位都被丢弃。

- 浮点乘法：
```
float operator *(float x, float y);
double operator *(double x, double y);
```

乘积是根据 IEC 60559 算术规则计算的。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为正有限值。z 是 x * y 的结果，四舍五入到最接近的可表示值。如果结果的幅值对于目标类型来说太大，则 z 为无穷大。由于舍入，z 可能为零，即使 x 和 y 都不为零。

| | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +X | +Z | -Z | +0 | -0 | +∞ | -∞ | NaN |
| -X | -Z | +Z | -0 | +0 | -∞ | +∞ | NaN |
| +0 | +0 | -0 | +0 | -0 | NaN | NaN | NaN |
| -0 | -0 | +0 | -0 | +0 | NaN | NaN | NaN |
| +∞ | +∞ | -∞ | NaN | NaN | +∞ | -∞ | NaN |
| -∞ | -∞ | +∞ | NaN | NaN | -∞ | +∞ | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

（除非另有说明，在 §12.9.2–§12.9.6 中的浮点表中，“+”的使用表示该值为正；“-”的使用表示该值为负；缺少符号表示该值可能为正或负或没有符号（NaN）。）

- 十进制乘法：
```
decimal operator *(decimal x, decimal y);
```

如果结果值的幅值太大而无法以十进制格式表示，则会抛出 System.OverflowException。由于舍入，结果可能为零，即使两个操作数都不为零。舍入之前的结果精度是两个操作数精度的总和。

十进制乘法等价于使用类型 System.Decimal 的乘法运算符。

上述定义的未提升预定义乘法运算符的提升形式（§12.4.8）也是预定义的。

## 12.9.3 除法运算符

对于形式为 x / y 的操作，将应用二进制运算符重载解析（§12.4.5）来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。

- 整数除法：
```
int operator /(int x, int y);
uint operator /(uint x, uint y);
long operator /(long x, long y);
ulong operator /(ulong x, ulong y);
```
如果右操作数的值为零，则会抛出 System.DivideByZeroException。

除法将结果向零舍入。因此结果的绝对值是小于或等于两个操作数商的绝对值的最大可能整数。当两个操作数符号相同时，结果为零或正；当两个操作数符号相反时，结果为零或负。

如果左操作数是最小的可表示 int 或 long 值且右操作数为 -1，则会发生溢出。在检查上下文中，这会导致抛出 System.ArithmeticException（或其子类）。在未检查上下文中，是否抛出 System.ArithmeticException（或其子类）或溢出未被报告且结果值为左操作数的值是实现定义的。

- 浮点除法：
```
float operator /(float x, float y);
double operator /(double x, double y);
```

商是根据 IEC 60559 算术规则计算的。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为正有限值。z 是 x / y 的结果，四舍五入到最接近的可表示值。

|  | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +X | +Z | -Z | +∞ | -∞ | +0 | -0 | NaN |
| -X | -Z | +Z | -∞ | +∞ | -0 | +0 | NaN |
| +0 | +0 | -0 | NaN | NaN | +0 | -0 | NaN |
| -0 | -0 | +0 | NaN | NaN | -0 | +0 | NaN |
| +∞ | +∞ | -∞ | +∞ | -∞ | NaN | NaN | NaN |
| -∞ | -∞ | +∞ | -∞ | +∞ | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制除法：
```
decimal operator /(decimal x, decimal y);
```

如果右操作数的值为零，则会抛出 System.DivideByZeroException。如果结果值的幅值太大而无法以十进制格式表示，则会抛出 System.OverflowException。由于舍入，结果可能为零，即使第一个操作数不为零。舍入之前的结果精度是最接近首选精度且能保持结果等于精确结果的精度。首选精度是 x 的精度减去 y 的精度。

十进制除法等价于使用类型 System.Decimal 的除法运算符。

上述定义的未提升预定义除法运算符的提升形式（§12.4.8）也是预定义的。

## 12.9.4 余数运算符

对于形式为 x % y 的操作，将应用二进制运算符重载解析（§12.4.5）来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。

预定义的余数运算符列于下文。所有运算符都计算 x 和 y 之间除法的余数。

- 整数余数：
```
int operator %(int x, int y);
uint operator %(uint x, uint y);
long operator %(long x, long y);
ulong operator %(ulong x, ulong y);
```

x % y 的结果是由 x - (x / y) * y 产生的值。如果 y 为零，则会抛出 System.DivideByZeroException。

如果左操作数是最小的 int 或 long 值且右操作数为 -1，则仅当 x / y 会抛出异常时才会抛出 System.OverflowException。

- 浮点余数：
```
float operator %(float x, float y);
double operator %(double x, double y);
```

下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为正有限值。z 是 x % y 的结果，计算方式为 x - n * y，其中 n 是小于或等于 x / y 的最大可能整数。这种计算余数的方法类似于用于整数操作数的方法，但与 IEC 60559 定义不同（其中 n 是最接近 x / y 的整数）。

| | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | +z | NaN | NaN | +X | +X | NaN |
| -x | -z | -z | NaN | NaN | -X | -X | NaN |
| +0 | +0 | +0 | NaN | NaN | +0 | +0 | NaN |
| -0 | -0 | -0 | NaN | NaN | -0 | -0 | NaN |
| +∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| -∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制余数：
```
decimal operator %(decimal x, decimal y);
```

如果右操作数的值为零，则会抛出 System.DivideByZeroException。抛出 System.ArithmeticException（或其子类）的时间是实现定义的。符合规范的实现不得在 x / y 不抛出异常的任何情况下为 x % y 抛出异常。舍入之前的结果精度是两个操作数精度中的较大者，且结果的符号（如果非零）与 x 相同。

十进制余数等价于使用类型 System.Decimal 的余数运算符。

> [注意：这些规则确保对于所有类型，结果永远不会与左操作数符号相反。结束注释]

上述定义的未提升预定义余数运算符的提升形式（§12.4.8）也是预定义的。

## 12.9.5 加法运算符

对于形式为 x + y 的操作，将应用二进制运算符重载解析（§12.4.5）来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。

预定义的加法运算符列于下文。对于数值类型和枚举类型，预定义的加法运算符计算两个操作数的和。当一个或两个操作数为 string 类型时，预定义的加法运算符连接操作数的字符串表示形式。

- 整数加法：
```
int operator +(int x, int y);
uint operator +(uint x, uint y);
long operator +(long x, long y);
ulong operator +(ulong x, ulong y);
```

在已检查上下文中，如果和超出结果类型的范围，则引发 System.OverflowException。在未检查上下文中，不报告溢出，并且丢弃结果类型范围之外的任何有效高阶位。

- 浮点加法：

```
float operator +(float x, float y);
double operator +(double x, double y);
```

和按照 IEC 60559 算术规则计算。下表列出了非零有限值、零、无穷和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值，z 是 x + y 的结果。如果 x 和 y 具有相同的数值大小但符号相反，则 z 为正零。如果 x + y 太大而无法在目标类型中表示，则 z 为与 x + y 符号相同的无穷大。

|  | y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|
| x | z | x | x | +∞ | -∞ | NaN |
| +0 | y | +0 | +0 | +∞ | -∞ | NaN |
| -0 | y | +0 | -0 | +∞ | -∞ | NaN |
| +∞ | +∞ | +∞ | +∞ | +∞ | NaN | NaN |
| -∞ | -∞ | -∞ | -∞ | NaN | -∞ | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制加法：

```
decimal operator +(decimal x, decimal y);
```

如果结果值的大小太大，无法以 decimal 格式表示，则引发 System.OverflowException。结果的小数位数（在进行任何舍入之前）是两个操作数的小数位数中的较大者。

十进制加法等效于使用 System.Decimal 类型的加法运算符。

- 枚举加法：每个枚举类型隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：

```
E operator +(E x, U y);
E operator +(U x, E y);
```

在运行时，这些运算符完全按照 (E)((U)x + (U)y) 求值。

- 字符串串联：

```
string operator +(string x, string y);
string operator +(string x, object y);
string operator +(object x, string y);
```

二元 + 运算符的这些重载执行字符串串联。如果字符串串联的一个操作数为 null，则替换为空字符串。否则，任何非字符串操作数都将通过调用从 object 类型继承的虚 ToString 方法来转换为其字符串表示形式。如果 ToString 返回 null，则替换为空字符串。[示例: using System;

```csharp
class Test
{
    static void Main() {
        string s = null;
        Console.WriteLine("s = " + s + ""); // displays s = <>
        int i = 1;
        Console.WriteLine("i = " + i);          // displays i = 1
        float f = 1.2300E+15F;
        Console.WriteLine("f = " + f);          // displays f = 1.23E+15
        decimal d = 2.900m;
        Console.WriteLine("d = " + d);          // displays d = 2.900
    }
}
```

注释中显示的输出是美式英语系统上的典型结果。精确输出可能取决于执行环境的区域设置。字符串串联运算符本身在各种情况下的行为相同，但在执行过程中隐式调用的 ToString 方法可能受区域设置影响。结束示例]

字符串串联运算符的结果是一个字符串，由左操作数的字符后跟右操作数的字符组成。字符串串联运算符从不返回 null 值。如果没有足够的内存来分配结果字符串，则可能引发 System.OutOfMemoryException。

- 委托组合。每个委托类型隐式提供以下预定义运算符，其中 D 是委托类型：

```
D operator +(D x, D y);
```

如果第一个操作数为 null，则操作的结果是第二个操作数的值（即使它也是 null）。否则，如果第二个操作数为 null，则操作的结果是第一个操作数的值。否则，操作的结果是一个新的委托实例，其调用列表由第一个操作数的调用列表中的元素后跟第二个操作数的调用列表中的元素组成。也就是说，结果委托的调用列表是两个操作数的调用列表的串联。[注意：有关委托组合的示例，请参阅 §12.9.6 和 §20.6。由于 System.Delegate 不是委托类型，因此未为其定义运算符 +。结束注释]

上述非提升的预定义加法运算符的提升（§12.4.8）形式也是预定义的。

## 12.9.6 减法运算符

对于形式为 x − y 的操作，将应用二元运算符重载决策（§12.4.5）来选择特定的运算符实现。操作数将转换为所选运算符的参数类型，结果的类型是该运算符的返回类型。

下面列出了预定义的减法运算符。这些运算符都从 x 中减去 y。

- 整数减法：

```csharp
int operator -(int x, int y);
uint operator -(uint x, uint y);
long operator -(long x, long y);
ulong operator -(ulong x, ulong y);
```

在已检查上下文中，如果差超出结果类型的范围，则引发 System.OverflowException。在未检查上下文中，不报告溢出，并且丢弃结果类型范围之外的任何有效高阶位。

- 浮点减法：

```csharp
float operator -(float x, float y);
double operator -(double x, double y);
```

差按照 IEC 60559 算术规则计算。下表列出了非零有限值、零、无穷和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值，z 是 x - y 的结果。如果 x 和 y 相等，则 z 为正零。如果 x - y 太大而无法在目标类型中表示，则 z 为与 x - y 符号相同的无穷大。

|  | y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|
| x | z | x | x | -∞ | +∞ | NaN |
| +0 | -y | +0 | +0 | -∞ | +∞ | NaN |
| -0 | -y | -0 | +0 | -∞ | +∞ | NaN |
| +∞ | +∞ | +∞ | +∞ | NaN | +∞ | NaN |
| -∞ | -∞ | -∞ | -∞ | -∞ | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN |

（在上表中，-y 条目表示对 y 取反，而不是该值为负数。）

- 十进制减法：

```
decimal operator -(decimal x, decimal y);
```

如果结果值的大小太大，无法以 decimal 格式表示，则引发 System.OverflowException。结果的小数位数（在进行任何舍入之前）是两个操作数的小数位数中的较大者。

十进制减法等效于使用 System.Decimal 类型的减法运算符。

- 枚举减法。每个枚举类型隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：

```
U operator -(E x, E y);
```

该运算符完全按照 (U)((U)x - (U)y) 求值。换句话说，该运算符计算 x 和 y 的序数值之间的差，结果的类型是枚举的基础类型。

```
E operator -(E x, U y);
```

该运算符完全按照 (E)((U)x - y) 求值。换句话说，该运算符从枚举的基础类型中减去一个值，生成一个枚举值。

- 委托移除。每个委托类型隐式提供以下预定义运算符，其中 D 是委托类型：

```
D operator -(D x, D y);
```

如果第一个操作数为 null，则操作的结果为 null。否则，如果第二个操作数为 null，则操作的结果是第一个操作数的值。否则，两个操作数都表示具有一个或多个条目的调用列表（§20.2），结果是一个新的调用列表，由第一个操作数的列表移除第二个操作数的条目后构成，前提是第二个操作数的列表是第一个列表的严格连续子列表。（为了确定子列表相等性，相应条目按照委托相等运算符（§12.11.9）进行比较。）否则，结果是左操作数的值。在此过程中，两个操作数的列表都不会被更改。如果第二个操作数的列表与第一个操作数的列表中的多个连续条目子列表匹配，则移除最右边的匹配连续条目子列表。如果移除导致空列表，则结果为 null。（示例：


- 右移：
```
int operator >>(int x, int count);
uint operator >>(uint x, int count);
long operator >>(long x, int count);
ulong operator >>(ulong x, int count);
```

`>>` 运算符将 `x` 向右移动若干位，移动位数的计算方式如下所述。

当 `x` 的类型为 `int` 或 `long` 时，`x` 的低位被丢弃，剩余位向右移动；如果 `x` 为非负数，则高位空出的位设置为零；如果 `x` 为负数，则高位空出的位设置为一。

当 `x` 的类型为 `uint` 或 `ulong` 时，`x` 的低位被丢弃，剩余位向右移动，高位空出的位设置为零。

对于预定义运算符，移动位数按以下方式计算：

- 当 `x` 的类型为 `int` 或 `uint` 时，移动计数由 `count` 的低五位给出。换句话说，移动计数根据 `count & 0x1F` 计算。
- 当 `x` 的类型为 `long` 或 `ulong` 时，移动计数由 `count` 的低六位给出。换句话说，移动计数根据 `count & 0x3F` 计算。

如果计算出的移动计数为零，移位运算符将直接返回 `x` 的值。移位运算永远不会导致溢出，并且在 checked 和 unchecked 上下文中产生相同的结果。

当 `>>` 运算符的左操作数为有符号整型时，该运算符执行算术右移，即将操作数最高有效位（符号位）的值传播到高位空出的位中。当 `>>` 运算符的左操作数为无符号整型时，该运算符执行逻辑右移，即高位空出的位始终设置为零。若要执行与根据操作数类型推断出的操作相反的操作，可以使用显式转换。[示例：如果 `x` 是 `int` 类型的变量，则操作 `unchecked((int)((uint)x >> y))` 会对 `x` 执行逻辑右移。示例结束]

上述非提升预定义移位运算符的提升形式（§12.4.8）也属于预定义运算符。

## 12.11 关系运算符和类型测试运算符

### 12.11.1 一般规则

`==`、`!=`、`<`、`>`、`<=`、`>=`、`is` 和 `as` 运算符称为关系运算符和类型测试运算符。

relational-expression:
    shift-expression
    relational-expression < shift-expression
    relational-expression > shift-expression
    relational-expression <= shift-expression
    relational-expression >= shift-expression
    relational-expression is type
    relational-expression as type

equality-expression:
    relational-expression
    equality-expression == relational-expression
    equality-expression != relational-expression

`is` 运算符的说明见 §12.11.11，`as` 运算符的说明见 §12.11.12。

`==`、`!=`、`<`、`>`、`<=` 和 `>=` 运算符是比较运算符。

如果比较运算符的某个操作数的编译时类型为 `dynamic`，则表达式将进行动态绑定（§12.3.3）。在这种情况下，表达式的编译时类型为 `dynamic`，并且下面所述的解析将在运行时进行，此时将使用那些编译时类型为 `dynamic` 的操作数的运行时类型。

对于 `x op y` 形式的操作（其中 `op` 为比较运算符），将应用重载解析（§12.4.5）来选择特定的运算符实现。操作数将转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。如果相等表达式的两个操作数都是 null 字面量，则不会执行重载解析，并且表达式将根据运算符是 `==` 还是 `!=`，计算为 `true` 或 `false` 常量值。

预定义比较运算符将在以下子条款中进行说明。所有预定义比较运算符都返回 `bool` 类型的结果，如下表所述。

| 操作 | 结果 |
|---|---|
| x == y | 如果 x 等于 y，则为 true；否则为 false |
| x != y | 如果 x 不等于 y，则为 true；否则为 false |
| x < y | 如果 x 小于 y，则为 true；否则为 false |
| x > y | 如果 x 大于 y，则为 true；否则为 false |
| x <= y | 如果 x 小于或等于 y，则为 true；否则为 false |
| x >= y | 如果 x 大于或等于 y，则为 true；否则为 false |

### 12.11.2 整数比较运算符

预定义的整数比较运算符如下：

```
bool operator ==(int x, int y);
bool operator ==(uint x, uint y);
bool operator ==(long x, long y);
bool operator ==(ulong x, ulong y);

bool operator !=(int x, int y);
bool operator !=(uint x, uint y);
bool operator !=(long x, long y);
bool operator !=(ulong x, ulong y);

bool operator <(int x, int y);
bool operator <(uint x, uint y);
bool operator <(long x, long y);
bool operator <(ulong x, ulong y);

bool operator >(int x, int y);
bool operator >(uint x, uint y);
bool operator >(long x, long y);
bool operator >(ulong x, ulong y);

bool operator <=(int x, int y);
bool operator <=(uint x, uint y);
bool operator <=(long x, long y);
bool operator <=(ulong x, ulong y);

bool operator >=(int x, int y);
bool operator >=(uint x, uint y);
bool operator >=(long x, long y);
bool operator >=(ulong x, ulong y);
```

每个运算符都会比较两个整型操作数的数值，并返回一个 `bool` 值，指示相应关系为 true 还是 false。

上述非提升预定义整数比较运算符的提升形式（§12.4.8）也属于预定义运算符。

### 12.11.3 浮点比较运算符

预定义的浮点比较运算符如下：

```
bool operator ==(float x, float y);
bool operator ==(double x, double y);
bool operator !=(float x, float y);
bool operator !=(double x, double y);
bool operator <(float x, float y);
bool operator <(double x, double y);
bool operator >(float x, float y);
bool operator >(double x, double y);
bool operator <=(float x, float y);
bool operator <=(double x, double y);
bool operator >=(float x, float y);
bool operator >=(double x, double y);
```

这些运算符按照 IEC 60559 标准的规则比较操作数：

如果任一操作数为 NaN，则除 `!=` 之外的所有运算符的结果均为 false，而 `!=` 的结果为 true。对于任意两个操作数，`x != y` 始终产生与 `!(x == y)` 相同的结果。但是，当一个或两个操作数为 NaN 时，`<`、`<=` 和 `>=` 运算符产生的结果并不等同于相反运算符的逻辑否定。[示例：如果 `x` 和 `y` 中任一个为 NaN，则 `x < y` 为 false，但 `!(x >= y)` 为 true。示例结束]

- 当两个操作数都不是 NaN 时，运算符根据以下顺序比较两个浮点操作数的值：

-∞ < -max < ... < -min < -0.0 == +0.0 < +min < ... < +max < +∞

其中，`min` 和 `max` 分别是在给定浮点格式中可以表示的最小和最大的正有限值。该顺序的显著影响包括：

- 负零和正零被视为相等。
- 负无穷小于所有其他值，但与另一个负无穷相等。
- 正无穷大于所有其他值，但与另一个正无穷相等。

上述非提升预定义浮点比较运算符的提升形式（§12.4.8）也属于预定义运算符。

### 12.11.4 Decimal 比较运算符

预定义的 Decimal 比较运算符如下：

```
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

每个运算符都会比较两个 Decimal 操作数的数值，并返回一个 `bool` 值，指示相应关系为 true 还是 false。每个 Decimal 比较都等效于使用 `System.Decimal` 类型中相应的关系运算符或相等运算符。

上述非提升预定义 Decimal 比较运算符的提升形式（§12.4.8）也属于预定义运算符。

### 12.11.5 布尔相等运算符

预定义的布尔相等运算符如下：


- 使用预定义的引用类型相等运算符比较在绑定时已知不同的两个引用是绑定时错误。例如，如果操作数的绑定时类型是两个类类型，并且两者互不派生，则这两个操作数不可能引用同一个对象。因此，该操作被视为绑定时错误。
- 预定义的引用类型相等运算符不允许比较值类型操作数（类型参数与 null 比较时除外，后者有特殊处理）。
- 预定义引用类型相等运算符的操作数永远不会被装箱。执行此类装箱操作是没有意义的，因为对新分配的装箱实例的引用必然与所有其他引用不同。

对于形式为 x == y 或 x != y 的操作，如果存在任何适用的用户定义 operator == 或 operator !=，则运算符重载解析规则（§12.4.5）将选择该运算符而不是预定义的引用类型相等运算符。始终可以通过显式将一个或两个操作数强制转换为 object 类型来选择预定义的引用类型相等运算符。end note

[示例：以下示例检查无约束类型参数类型的参数是否为 null。

```
class C<T>
{
    void F(T x) {
        if (x == null) throw new ArgumentNullException();
        ...
    }
}
```

x == null 构造是允许的，即使 T 可能表示不可空值类型，结果也简单地定义为当 T 为不可空值类型时为 false。end example

对于形式为 x == y 或 x != y 的操作，如果存在任何适用的 operator == 或 operator !=，则运算符重载解析（§12.4.5）规则将选择该运算符而不是预定义的引用类型相等运算符。[注意：始终可以通过显式将两个操作数都强制转换为 object 类型来选择预定义的引用类型相等运算符。end note]

[示例：示例

```
using System;
class Test
{
    static void Main() {
        string s = "Test";
        string t = string.Copy(s);
        Console.WriteLine(s == t);
        Console.WriteLine((object)s == (object)t);
        Console.WriteLine((object)s == t);
        Console.WriteLine((object)s == (object)t);
    }
}
```

生成输出

True
False
False
False

s 和 t 变量引用包含相同字符的两个不同的字符串实例。第一个比较输出 True，因为当两个操作数均为 string 类型时，选择了预定义的字符串相等运算符（§12.11.8）。其余比较都输出 False，因为当任一操作数的绑定时类型为 object 时，string 类型中 operator== 的重载不适用。

请注意，上述技术对于值类型没有意义。示例

```
class Test
{
    static void Main() {
        int i = 123;
        int j = 123;
        System.Console.WriteLine((object)i == (object)j);
    }
}
```

输出 False，因为这些强制转换创建了指向两个单独的装箱 int 值实例的引用。end example

## 12.11.8 字符串相等运算符

预定义的字符串相等运算符是：

```
bool operator ==(string x, string y);
bool operator !=(string x, string y);
```

当满足以下任一条件时，两个字符串值被认为相等：

- 两个值均为 null。
- 两个值均为非空引用，指向字符串实例，且长度相同且每个字符位置的字符相同。

字符串相等运算符比较的是字符串值而不是字符串引用。当两个单独的字符串实例包含完全相同的字符序列时，字符串的值相等，但引用不同。[注意：如 §12.11.7 中所述，可以使用引用类型相等运算符来比较字符串引用而不是字符串值。end note]

## 12.11.9 委托相等运算符

预定义的委托相等运算符是：

```
bool operator ==(System.Delegate x, System.Delegate y);
bool operator !=(System.Delegate x, System.Delegate y);
```

否则，操作的结果等价于求值 E != null。

- 否则，如果从 C 到 T 存在显式引用转换（§11.3.5）或拆箱转换（§11.3.6），或者 C 或 T 是开放类型（§9.4.3），则必须执行如上所述的运行时检查。
- 否则，不可能将 E 转换为类型 T 的引用、装箱、包装或解包装转换，操作结果为 false。

编译器可以根据编译时类型实现优化。end note]

## 12.11.12 as 运算符

as 运算符用于将值显式转换为给定的引用类型或可空值类型。与强制转换表达式（§12.8.7）不同，as 运算符永远不会抛出异常。相反，如果指示的转换不可行，则结果值为 null。

在形式为 E as T 的操作中，E 必须是一个表达式，T 必须是一个引用类型、已知为引用类型的类型参数，或可空值类型。此外，以下至少一项必须为真，否则会发生编译时错误：

- 从 E 到 T 存在恒等（§11.2.2）、隐式可空（§11.2.5）、隐式引用（§11.2.7）、装箱（§11.2.8）、显式可空（§11.3.4）、显式引用（§11.3.5）或包装（§9.3.11）转换。
- E 或 T 的类型是开放类型。
- E 是 null 字面量。

如果 E 的编译时类型不是 dynamic，则操作 E as T 产生的结果与以下相同：

E is T ? (T)E : (T)null

只是 E 仅被求值一次。编译器可以预期优化 E as T 以最多执行一次运行时类型检查，而上述展开隐含了两次运行时类型检查。

如果 E 的编译时类型是 dynamic，与 cast 运算符不同，as 运算符不是动态绑定的（§12.3.3）。因此，在这种情况下的展开为：

E is T ? (T)(object)E : (T)null

请注意，某些转换，例如用户定义转换，不能使用 as 运算符进行，而应使用强制转换表达式进行。

[示例：在示例中

```
class X
{
    public string F(object o) {
        return o as string;    // OK, string is a reference type
    }
    public T G<T>(object o) where T: Attribute {
        return o as T;    // Ok, T has a class constraint
    }
    public U H<U>(object o) {
        return o as U;    // Error, U is unconstrained
    }
}
```

G 的类型参数 T 已知为引用类型，因为它具有类约束。然而 H 的类型参数 U 不是；因此在 H 中使用 as 运算符是不允许的。end example]

## 12.12 逻辑运算符

### 12.12.1 通用

&、^ 和 | 运算符称为逻辑运算符。

```
and-expression:
  equality-expression
  and-expression & equality-expression

exclusive-or-expression:
  and-expression
  exclusive-or-expression ^ and-expression

inclusive-or-expression:
  exclusive-or-expression
  inclusive-or-expression | exclusive-or-expression
```

如果逻辑运算符的操作数具有编译时类型 dynamic，则表达式是动态绑定的（§12.3.3）。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将使用具有编译时类型 dynamic 的那些操作数的运行时类型在运行时进行。

对于形式为 x op y 的操作，其中 op 是逻辑运算符之一，将应用重载解析（§12.4.5）来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。

预定义的逻辑运算符在以下小节中描述。

### 12.12.2 整数逻辑运算符

预定义的整数逻辑运算符是：

```
int operator &(int x, int y);
uint operator &(uint x, uint y);
long operator &(long x, long y);
ulong operator &(ulong x, ulong y);

int operator |(int x, int y);
uint operator |(uint x, uint y);
long operator |(long x, long y);
ulong operator |(ulong x, ulong y);

int operator ^(int x, int y);
uint operator ^(uint x, uint y);
long operator ^(long x, long y);
ulong operator ^(ulong x, ulong y);
```

& 运算符计算两个操作数的按位逻辑与，| 运算符计算两个操作数的按位逻辑或，^ 运算符计算两个操作数的按位逻辑异或。这些操作不可能发生溢出。

上述未提升的预定义整数逻辑运算符的提升形式（§12.4.8）也是预定义的。

### 12.12.3 枚举逻辑运算符

每个枚举类型 E 隐式提供以下预定义逻辑运算符：

```
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```

求值 x op y 的结果，其中 x 和 y 是具有底层类型 U 的枚举类型 E 的表达式，且 op 是逻辑运算符之一，与求值 (E)((U)x op (U)y) 完全相同。换句话说，枚举类型逻辑运算符只是对两个操作数的底层类型执行逻辑操作。

上述未提升的预定义枚举逻辑运算符的提升形式（§12.4.8）也是预定义的。



### 12.12.4 布尔逻辑运算符

预定义的布尔逻辑运算符为：

```
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```

如果 x 和 y 都为 true，则 x & y 的结果为 true。否则，结果为 false。

如果 x 或 y 为 true，则 x | y 的结果为 true。否则，结果为 false。

如果 x 为 true 且 y 为 false，或者 x 为 false 且 y 为 true，则 x ^ y 的结果为 true。否则，结果为 false。当操作数类型为 bool 时，^ 运算符计算的结果与 != 运算符相同。

### 12.12.5 可空布尔 & 和 | 运算符

可空布尔类型 bool? 可以表示三个值：true、false 和 null。

与其他二元运算符一样，逻辑运算符 & 和 |（§12.12.4）的提升形式也是预定义的：

```
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

提升后的 & 和 | 运算符的语义由下表定义：

| x | y | x & y | x \| y |
|---|---|---|---|
| true | true | true | true |
| true | false | false | true |
| true | null | null | true |
| false | true | false | true |
| false | false | false | false |
| false | null | false | null |
| null | true | null | true |
| null | false | false | null |
| null | null | null | null |

> [注意：bool? 类型在概念上类似于 SQL 中用于布尔表达式的三值类型。上表遵循与 SQL 相同的语义，而将 §12.4.8 的规则应用于 & 和 | 运算符则不会得到相同结果。§12.4.8 的规则已经为提升后的 ^ 运算符提供了类似 SQL 的语义。结束注意]

## 12.13 条件逻辑运算符

### 12.13.1 概述

&& 和 || 运算符称为条件逻辑运算符。它们也称为“短路”逻辑运算符。

conditional-and-expression:
  inclusive-or-expression
  conditional-and-expression && inclusive-or-expression
conditional-or-expression:
  conditional-and-expression
  conditional-or-expression || conditional-and-expression

&& 和 || 运算符是 & 和 | 运算符的条件版本：

- 运算 x && y 对应于运算 x & y，不同之处在于仅当 x 不为 false 时才计算 y。
- 运算 x || y 对应于运算 x | y，不同之处在于仅当 x 不为 true 时才计算 y。

> [注意：短路使用“非 true”和“非 false”条件的原因，是为了让用户定义的条件运算符能够定义何时适用短路。用户定义类型可能处于这样一种状态：运算符 true 返回 false，且运算符 false 返回 false。在这些情况下，&& 和 || 都不会短路。结束注意]

如果条件逻辑运算符的操作数具有编译时类型 dynamic，则该表达式采用动态绑定（§12.3.3）。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的重载决策将在运行时使用那些具有编译时类型 dynamic 的操作数的运行时类型来进行。

形式为 x && y 或 x || y 的运算按如下方式处理：像该运算写成 x & y 或 x | y 一样应用重载决策（§12.4.5）。然后，

- 如果重载决策未能找到单个最佳运算符，或者重载决策选择了某个预定义的整数逻辑运算符或可空布尔逻辑运算符（§12.12.5），则发生绑定期错误。
- 否则，如果所选运算符是某个预定义的布尔逻辑运算符（§12.12.4），则按 §12.13.2 中所述处理该运算。
- 否则，所选运算符是用户定义运算符，并按 §12.13.3 中所述处理该运算。

无法直接重载条件逻辑运算符。但是，由于条件逻辑运算符是依据常规逻辑运算符来求值的，因此常规逻辑运算符的重载在特定限制下也被视为条件逻辑运算符的重载。§12.13.3 对此作了进一步描述。

### 12.13.2 布尔条件逻辑运算符

当 && 或 || 的操作数为 bool 类型，或者操作数的类型未定义适用的运算符 & 或运算符 |，但定义了到 bool 的隐式转换时，该运算按如下方式处理：

- 运算 x && y 按 x ? y : false 求值。换句话说，首先计算 x 并转换为 bool 类型。然后，如果 x 为 true，则计算 y 并转换为 bool 类型，该值成为运算结果。否则，运算结果为 false。
- 运算 x || y 按 x ? true : y 求值。换句话说，首先计算 x 并转换为 bool 类型。然后，如果 x 为 true，则运算结果为 true。否则，计算 y 并转换为 bool 类型，该值成为运算结果。

### 12.13.3 用户定义的条件逻辑运算符

当 && 或 || 的操作数所属类型声明了适用的用户定义运算符 & 或运算符 | 时，以下两项均须为真，其中 T 是声明所选运算符的类型：

- 所选运算符的返回类型和每个参数的类型均应为 T。换句话说，该运算符应计算两个 T 类型操作数的逻辑 AND 或逻辑 OR，并返回 T 类型的结果。
- T 应包含运算符 true 和运算符 false 的声明。

如果这两项要求中的任一项不满足，则发生绑定期错误。否则，通过将用户定义的运算符 true 或运算符 false 与所选用户定义运算符组合，来计算 && 或 || 运算：

- 运算 x && y 按 T.false(x) ? x : T.&(x, y) 求值，其中 T.false(x) 是对 T 中声明的运算符 false 的调用，T.&(x, y) 是对所选运算符 & 的调用。换句话说，首先计算 x，并对结果调用运算符 false，以确定 x 是否肯定为 false。然后，如果 x 肯定为 false，则运算结果为先前为 x 计算的值。否则，计算 y，并对先前为 x 计算的值和为 y 计算的值调用所选运算符 &，以产生运算结果。
- 运算 x || y 按 T.true(x) ? x : T.|(x, y) 求值，其中 T.true(x) 是对 T 中声明的运算符 true 的调用，T.|(x, y) 是对所选运算符 | 的调用。换句话说，首先计算 x，并对结果调用运算符 true，以确定 x 是否肯定为 true。然后，如果 x 肯定为 true，则运算结果为先前为 x 计算的值。否则，计算 y，并对先前为 x 计算的值和为 y 计算的值调用所选运算符 |，以产生运算结果。

在这两种运算中的任一种中，由 x 给出的表达式只计算一次，而由 y 给出的表达式要么不计算，要么恰好计算一次。

## 12.14 null 合并运算符

?? 运算符称为 null 合并运算符。

```
null-coalescing-expression:
    conditional-or-expression
    conditional-or-expression ?? null-coalescing-expression
```

形式为 a ?? b 的 null 合并表达式要求 a 为 null 字面量（§7.4.5.7），或者为可空值类型或引用类型。如果 a 非 null，则 a ?? b 的结果为 a；否则，结果为 b。

仅当 a 为 null 时，该运算才计算 b。

null 合并运算符是右结合的，这意味着运算从右到左分组。[示例：形式为 a ?? b ?? c 的表达式按 a ?? (b ?? c) 求值。一般来说，形式为 E1 ?? E2 ?? ... ?? EN 的表达式返回操作数中第一个非 null 的操作数；如果所有操作数都为 null，则返回 null。结束示例]

表达式 a ?? b 的类型取决于操作数上可用的隐式转换。按优先顺序，a ?? b 的类型为 A0、A 或 B，其中 A 是 a 的类型（前提是 a 具有类型），B 是 b 的类型（前提是 b 具有类型），并且如果 A 是可空值类型，则 A0 是 A 的基础类型；否则 A0 为 A。具体而言，a ?? b 按如下方式处理：

- 如果 A 存在且不是可空值类型或引用类型，则发生编译时错误。
- 如果 b 是动态表达式，则结果类型为 dynamic。运行时，首先计算 a。如果 a 不为 null，则将 a 转换为 dynamic，并以此作为结果。否则，计算 b，并以此作为结果。
- 否则，如果 A 存在且为可空值类型，并且存在从 b 到 A0 的隐式转换，则结果类型为 A0。运行时，首先计算 a。如果 a 不为 null，则将 a 解包为 A0 类型，并以此作为结果。否则，计算 b 并将其转换为 A0 类型，并以此作为结果。
- 否则，如果 A 存在且存在从 b 到 A 的隐式转换，则结果类型为 A。运行时，首先计算 a。如果 a 不为 null，则 a 成为结果。否则，计算 b 并将其转换为 A 类型，并以此作为结果。
- 否则，如果 A 存在且为可空值类型，b 具有类型 B 且存在从 A0 到 B 的隐式转换，则结果类型为 B。运行时，首先计算 a。如果 a 不为 null，则将 a 解包为 A0 类型并转换为 B 类型，并以此作为结果。否则，计算 b 并以此作为结果。
- 否则，如果 b 具有类型 B 且存在从 a 到 B 的隐式转换，则结果类型为 B。运行时，首先计算 a。如果 a 不为 null，则将 a 转换为 B 类型，并以此作为结果。否则，计算 b 并以此作为结果。




否则，a 和 b 不兼容，并且会发生编译时错误。

## 12.15 条件运算符

?: 运算符称为条件运算符。有时也称为三元运算符。

```
conditional-expression:
null-coalescing-expression
null-coalescing-expression ? expression : expression
```

形式为 b ? x : y 的条件表达式首先计算条件 b。然后，如果 b 为 true，则计算 x 并成为该操作的结果。否则，计算 y 并成为该操作的结果。条件表达式永远不会同时计算 x 和 y。

条件运算符是右结合的，这意味着操作是从右到左分组的。[示例：形式为 a ? b : c ? d : e 的表达式被求值为 a ? b : (c ? d : e)。结束示例]

?: 运算符的第一个操作数应为可隐式转换为 bool 的表达式，或实现 operator true 的类型的表达式。如果不满足这些要求中的任何一个，则会发生编译时错误。

?: 运算符的第二个和第三个操作数 x 和 y 控制条件表达式的类型。

- 如果 x 的类型为 X 且 y 的类型为 Y，则
  - 如果 X 和 Y 是同一类型，则这是条件表达式的类型。
  - 否则，如果存在从 X 到 Y 的隐式转换 (§11.2)，但不存在从 Y 到 X 的隐式转换，则 Y 是条件表达式的类型。
  - 否则，如果存在从 X 到 Y 的隐式枚举转换 (§11.2.4)，则 Y 是条件表达式的类型。
  - 否则，如果存在从 Y 到 X 的隐式枚举转换 (§11.2.4)，则 X 是条件表达式的类型。
  - 否则，如果存在从 Y 到 X 的隐式转换 (§11.2)，但不存在从 X 到 Y 的隐式转换，则 X 是条件表达式的类型。
  - 否则，无法确定表达式类型，并且会发生编译时错误。
- 如果 x 和 y 中只有一个具有类型，并且 x 和 y 都可隐式转换为该类型，则该类型即为条件表达式的类型。
- 否则，无法确定表达式类型，并且会发生编译时错误。

形式为 b ? x : y 的条件表达式的运行时处理包括以下步骤：

- 首先，计算 b，并确定 b 的 bool 值：
  - 如果存在从 b 的类型到 bool 的隐式转换，则执行此隐式转换以生成 bool 值。
  - 否则，调用 b 的类型定义的 operator true 以生成 bool 值。
- 如果上述步骤产生的 bool 值为 true，则计算 x 并将其转换为条件表达式的类型，这成为条件表达式的结果。
- 否则，计算 y 并将其转换为条件表达式的类型，这成为条件表达式的结果。

## 12.16 匿名函数表达式

### 12.16.1 通用

匿名函数是一个表示“内联”方法定义的表达式。匿名函数本身没有值或类型，但可以转换为兼容的委托或表达式树类型。匿名函数转换的求值取决于转换的目标类型：如果目标类型是委托类型，则转换求值为引用匿名函数定义的方法的委托值。如果目标类型是表达式树类型，则转换求值为表示方法结构的对象结构表达式树。

> [注意：出于历史原因，匿名函数有两种语法形式，即 lambda 表达式和匿名方法表达式。对于几乎所有目的而言，lambda 表达式比匿名方法表达式更简洁、更具表达力，而匿名方法表达式则为向后兼容而保留在语言中。结束注意]

```
lambda-expression:
    async_opt anonymous-function-signature => anonymous-function-body

anonymous-method-expression:
    async_opt delegate explicit-anonymous-function-signature_opt block

anonymous-function-signature:
    explicit-anonymous-function-signature
    implicit-anonymous-function-signature

explicit-anonymous-function-signature:
    ( explicit-anonymous-function-parameter-listopt )

explicit-anonymous-function-parameter-list:
    explicit-anonymous-function-parameter
    explicit-anonymous-function-parameter-list , explicit-anonymous-function-parameter

explicit-anonymous-function-parameter:
    anonymous-function-parameter-modifier_opt type identifier

anonymous-function-parameter-modifier:
    ref
    out

implicit-anonymous-function-signature:
    ( implicit-anonymous-function-parameter-listopt )
    implicit-anonymous-function-parameter

implicit-anonymous-function-parameter-list:
    implicit-anonymous-function-parameter
    implicit-anonymous-function-parameter-list , implicit-anonymous-function-parameter

implicit-anonymous-function-parameter:
    identifier

anonymous-function-body:
    expression
    block
```

=> 运算符的优先级与赋值 (=) 相同，并且是右结合的。

带有 async 修饰符的匿名函数是 async 函数，并遵循 §15.15 中描述的规则。

lambda 表达式形式的匿名函数的参数可以显式或隐式键入。在显式类型参数列表中，每个参数的类型被明确声明。在隐式类型列表中，参数的类型是从匿名函数出现的上下文中推断出来的——具体来说，当匿名函数转换为兼容的委托类型或表达式树类型时，该类型提供参数类型 (§11.7)。

在具有单个隐式类型参数的 lambda 表达式中，参数列表中的括号可以省略。换句话说，形式为

```
( param ) => expr
```

的匿名函数可以简写为

```
param => expr
```

匿名方法表达式形式的匿名函数的参数列表是可选的。如果给出，参数应为显式类型。如果没有给出，匿名函数可以转换为不包含 out 参数的任何参数列表的委托。

匿名函数的块体始终可达 (§13.2)。

[示例：下面是一些匿名函数的示例：

```
x => x + 1 // Implicitly typed, expression body
x => { return x + 1; } // Implicitly typed, statement body
(int x) => x + 1 // Explicitly typed, expression body
(int x) => { return x + 1; } // Explicitly typed, statement body
(x, y) => x * y // Multiple parameters
() => Console.WriteLine() // No parameters
async (t1,t2) => await t1 + await t2 // Async
delegate (int x) { return x + 1; } // Anonymous method expression
delegate { return 1 + 1; } // Parameter list omitted
```

结束示例]

lambda 表达式和匿名方法表达式的行为相同，除了以下几点：

- 匿名方法表达式允许完全省略参数列表，从而可转换为任何值参数列表的委托类型。
- lambda 表达式允许省略参数类型并进行推断，而匿名方法表达式要求参数类型必须显式声明。
- lambda 表达式的主体可以是表达式或语句块，而匿名方法表达式的主体必须是语句块。
- 只有 lambda 表达式才具有到兼容表达式树类型的转换 (§9.6)。

### 12.16.2 匿名函数签名

匿名函数的 anonymous-function-signature 定义了匿名函数的形参的名称以及可选的类型。匿名函数参数的作用域是 anonymous-function-body (§8.7)。与参数列表（如果给出）一起，anonymous-method-body 构成一个声明空间 (§8.3)。因此，匿名函数参数的名称与包含匿名方法表达式或 lambda 表达式的作用域的局部变量、局部常量或参数的名称相匹配是编译时错误。

如果匿名函数具有 explicit-anonymous-function-signature，则兼容的委托类型和表达式树类型的集合仅限于具有相同参数类型和修饰符且顺序相同者 (§11.7)。与方法组转换 (§11.8) 相比，不支持匿名函数参数类型的逆变。如果匿名函数没有 anonymous-function-signature，则兼容的委托类型和表达式树类型的集合仅限于不具有 out 参数者。



请注意，匿名函数签名不能包含特性或参数数组。尽管如此，匿名函数签名可能与参数列表包含参数数组的委托类型兼容。

请注意，即使兼容，转换为表达式树类型在编译时仍可能失败（§9.6）。

## 12.16.3 匿名函数体

匿名函数的体（表达式或块）受以下规则约束：

- 如果匿名函数包含签名，则签名中指定的参数可在体中使用。如果匿名函数没有签名，它可以转换为具有参数的委托类型或表达式类型（§11.7），但参数无法在体中访问。
- 除最近的封闭匿名函数签名（如果有）中指定的 ref 或 out 参数外，体访问 ref 或 out 参数是编译时错误。
- 当 this 的类型为结构体类型时，体访问 this 是编译时错误。无论访问是显式的（如 this.s_x）还是隐式的（如 x，其中 x 是结构体的实例成员），此规则均适用。该规则仅禁止此类访问，不影响成员查找是否得到结构体的成员。
- 体可访问匿名函数的外部变量（§12.16.6）。访问外部变量将引用在 lambda 表达式或匿名方法表达式被求值时（§12.16.7）处于活动状态的变量实例。
- 如果体包含 goto 语句、break 语句或 continue 语句，且其目标位于体之外或位于包含的匿名函数的体之内，则为编译时错误。
- 体中的 return 语句将控制权返回给最近的封闭匿名函数的调用，而不是封闭的函数成员。

是否可以通过 lambda 表达式或匿名方法表达式的求值和调用之外的方式执行匿名函数的块，明确未指定。特别是，编译器可以选择通过合成一个或多个命名方法或类型来实现匿名函数。此类合成元素的名称应采用为编译器使用保留的形式（§7.4.3）。

## 12.16.4 重载解析

参数列表中的匿名函数参与类型推断和重载解析。有关确切规则，请参阅 §12.6.3 和 §12.6.4。

[示例：以下示例说明了匿名函数对重载解析的影响。

```csharp
class ItemList<T>: List<T>
{
    public int Sum(Func<T,int> selector) {
        int sum = 0;
        foreach (T item in this) sum += selector(item);
        return sum;
    }

    public double Sum(Func<T,double> selector) {
        double sum = 0;
        foreach (T item in this) sum += selector(item);
        return sum;
    }
}
```

ItemList<T> 类有两个 Sum 方法。每个方法都接受一个选择器参数，该参数从列表项中提取要求和的值。提取的值可以是 int 也可以是 double，结果求和同样是 int 或 double。

例如，Sum 方法可用于从订单的明细行列表中计算总和。

```csharp
class Detail
{
    public int UnitCount;
    public double UnitPrice;
    ...
}
void ComputeSums() {
    ItemList<Detail> orderDetails = GetOrderDetails(...);
    int totalUnits = orderDetails.Sum(d => d.UnitCount);
    double orderTotal = orderDetails.Sum(d => d.UnitPrice * d.UnitCount);
}
...
```

在对 orderDetails.Sum 的第一次调用中，两个 Sum 方法都适用，因为匿名函数 d => d.UnitCount 与 Func<Detail,int> 和 Func<Detail,double> 都兼容。然而，重载解析选择第一个 Sum 方法，因为转换为 Func<Detail,int> 比转换为 Func<Detail,double> 更好。

在对 orderDetails.Sum 的第二次调用中，只有第二个 Sum 方法适用，因为匿名函数 d => d.UnitPrice * d.UnitCount 生成的类型为 double 的值。因此，重载解析为该调用选择第二个 Sum 方法。示例结束]

## 12.16.5 匿名函数与动态绑定

匿名函数不能是动态绑定操作的接收者、参数或操作数。

## 12.16.6 外部变量

### 12.16.6.1 通用

任何作用域包含 lambda 表达式或匿名方法表达式的局部变量、值参数或参数数组都称为匿名函数的外部变量。在类的实例函数成员中，this 值被视为值参数，是该函数成员中包含的任何匿名函数的外部变量。

### 12.16.6.2 被捕获的外部变量

当匿名函数引用外部变量时，称该外部变量已被匿名函数捕获。通常，局部变量的生命周期仅限于与其关联的块或语句的执行（§10.2.8）。然而，被捕获的外部变量的生命周期至少会延长到从匿名函数创建的委托或表达式树有资格进行垃圾回收为止。

[示例：在示例中

```csharp
using System;
delegate int D();
class Test
{
    static D F() {
        int x = 0;
        D result = () => ++x;
        return result;
    }

    static void Main() {
        D d = F();
        Console.WriteLine(d());
        Console.WriteLine(d());
        Console.WriteLine(d());
    }
}
```

局部变量 x 被匿名函数捕获，且 x 的生命周期至少会延长到从 F 返回的委托有资格进行垃圾回收为止。由于对匿名函数的每次调用都操作 x 的同一实例，因此示例的输出为：

- 1
- 2
- 3

示例结束]

当局部变量或值参数被匿名函数捕获时，该局部变量或参数不再被视为固定变量（§23.4），而是被视为可移动变量。然而，被捕获的外部变量不能在 fixed 语句中使用（§23.7），因此无法获取被捕获外部变量的地址。

> [注意：与未捕获变量不同，被捕获的局部变量可以同时暴露给多个执行线程。结束注意]

### 12.16.6.3 局部变量的实例化

当执行进入变量的作用域时，局部变量被视为 *实例化*。

[示例：例如，当以下方法被调用时，局部变量 x 被实例化并初始化三次——每次循环迭代一次。

```csharp
static void F() {
    for (int i = 0; i < 3; i++) {
        int x = i * 2 + 1;
    } ...
}
```

然而，将 x 的声明移出循环会导致 x 仅被实例化一次：

```csharp
static void F() {
    int x;
    for (int i = 0; i < 3; i++) {
        x = i * 2 + 1;
    } ...
}
```

示例结束]

当未被捕获时，无法观察局部变量被实例化的确切次数——因为实例化的生命周期是分离的，每个实例化可能只是简单地使用相同的存储位置。然而，当匿名函数捕获局部变量时，实例化的影响变得明显。

[示例：示例

```csharp
using System;
delegate void D();

class Test
{
    static D[] F() {
        D[] result = new D[3];
        for (int i = 0; i < 3; i++) {
            int x = i * 2 + 1;
            result[i] = () => { Console.WriteLine(x); };
        }
        return result;
    }
    static void Main() {
        foreach (D d in F()) d();
    }
}
```

产生输出：

```
1
3
5
```

然而，当 x 的声明被移出循环时：

```csharp
static D[] F() {
    D[] result = new D[3];
    int x;
    for (int i = 0; i < 3; i++) {
        x = i * 2 + 1;
        result[i] = () => { Console.WriteLine(x); };
    }
    return result;
}
```

输出为：

```
5
5
5
```

请注意，编译器允许（但不是必须）将三次实例化优化为单个委托实例（§11.7.2）。

示例结束]

如果 for 循环声明了迭代变量，则该变量本身被视为在循环外部声明。[示例：因此，如果示例被更改为捕获迭代变量本身：

```csharp
static D[] F() {
    D[] result = new D[3];
    for (int i = 0; i < 3; i++) {
        result[i] = () => { Console.WriteLine(i); };
    }
    return result;
}
```

仅捕获迭代变量的一个实例，这会产生输出：

```
3
3
3
```

示例结束]

匿名函数委托可能共享某些被捕获的变量，同时对其他变量具有单独的实例。[示例：例如，如果 F 被更改为

```
static D[] F() {
    D[] result = new D[3];
    int x = 0;
    for (int i = 0; i < 3; i++) {
        int y = 0;
        result[i] = () => { Console.WriteLine("{0} {1}", ++x, ++y); };
    }
    return result;
}
```

三个委托捕获同一个 x 的实例但 y 的实例是分开的，输出为：

1 1
2 1
3 1

示例结束

分离的匿名函数可以捕获同一个外部变量的实例。[示例：在示例中：

```
using System;
delegate void Setter(int value);
delegate int Getter();
class Test
{
    static void Main() {
        int x = 0;
        Setter s = (int value) => { x = value; };
        Getter g = () => { return x; };
        s(5);
        Console.WriteLine(g());
        s(10);
        Console.WriteLine(g());
    }
}
```

两个匿名函数捕获同一个局部变量 x 的实例，因此它们可以通过该变量“通信”。示例的输出为：

5
10

示例结束

## 12.16.7 匿名函数表达式的求值

匿名函数 F 始终应被转换为委托类型 D 或表达式树类型 E，要么直接转换，要么通过执行委托创建表达式 new D(F)。此转换决定了匿名函数的结果，如所述 in §11.7。

## 12.16.8 实现示例

### 本小节为说明性内容。

本小节描述了用其他 C# 构造实现匿名函数转换的一种可能实现。此处描述的实现基于商业 C# 编译器所使用的相同原则，但它绝不是强制性的实现，也不是唯一可能的实现。它仅简要提及到表达式树的转换，因为其确切语义超出了本规范的范围。

本小节的其余部分给出了包含具有不同特征的匿名函数的若干代码示例。对于每个示例，都提供了使用仅其他 C# 构造的相应翻译。在示例中，标识符 D 假定表示以下委托类型：

```
public delegate void D();
```

匿名函数的最简单形式是不捕获任何外部变量的形式：

```
class Test
{
    static void F() {
        D d = () => { Console.WriteLine("test"); };
    }
}
```

这可以被翻译为对委托实例化的引用，该实例化引用编译器生成的静态方法，其中放置了匿名函数的代码：

```
class Test
{
    static void F() {
        D d = new D(__Method1);
    }

    static void __Method1() {
        Console.WriteLine("test");
    }
}
```

在下面的示例中，匿名函数引用 this 的实例成员：

```
class Test
{
    int x;

    void F() {
        D d = () => { Console.WriteLine(x); };
    }
}
```

这可以被翻译为包含匿名函数代码的编译器生成的实例方法：

```
class Test
{
    int x;

    void F() {
        D d = new D(__Method1);
    }

    void __Method1() {
        Console.WriteLine(x);
    }
}
```

在此示例中，匿名函数捕获一个局部变量：

```
class Test
{
    void F() {
        int y = 123;
        D d = () => { Console.WriteLine(y); };
    }
}
```

局部变量的生命周期现在必须至少延长到匿名函数委托的生命周期。这可以通过将局部变量“提升”到编译器生成的类的字段中来实现。局部变量的实例化（§12.16.6.3）然后对应于创建编译器生成的类的实例，而访问局部变量对应于访问编译器生成的类实例中的字段。此外，匿名函数成为编译器生成类的实例方法：

```
class Test
{
    void F() {
        __locals1 = new __Locals1();
        __locals1.y = 123;
        D d = new D(__locals1.__Method1);
    }

    class __Locals1
    {
        public int y;
        public void __Method1() {
            Console.WriteLine(y);
        }
    }
}
```

最后，以下匿名函数捕获 this 以及具有不同生命周期的两个局部变量：

```
class Test
{
    int x;
    void F() {
        int y = 123;
        for (int i = 0; i < 10; i++) {
            int z = i * 2;
            D d = () => { Console.WriteLine(x + y + z); };
        }
    }
}
```

在这里，为捕获局部变量的每个语句块创建了一个编译器生成的类，以便不同块中的局部变量可以具有独立的生命周期。__Locals2 的实例，即内部语句块的编译器生成类，包含局部变量 z 和引用 __Locals1 实例的字段。__Locals1 的实例，即外部语句块的编译器生成类，包含局部变量 y 和引用封闭函数成员的 this 的字段。有了这些数据结构，就可以通过一个 __Local2 的实例访问所有捕获的外部变量，因此匿名函数的代码可以作为该类的实例方法实现。

```
class Test
{
    void F() {
        __locals1 = new __Locals1();
        __locals1.__this = this;
        __locals1.y = 123;
        for (int i = 0; i < 10; i++) {
            __locals2 = new __Locals2();
            __locals2.__locals1 = __locals1;
            __locals2.z = i * 2;
            D d = new D(__locals2.__Method1);
        }
    }
}

class __Locals1
{
    public Test __this;
    public int y;
}

class __Locals2
{
    public __Locals1 __locals1;
    public int z;
}
```

```
public void __Method1() {
    Console.WriteLine(__locals1.__this.x + __locals1.y + z);
}
}
```

这里用于捕获局部变量的相同技术也可以在将匿名函数转换为表达式树时使用：对编译器生成对象的引用可以存储在表达式树中，并且对局部变量的访问可以表示为对这些对象的字段访问。这种方法的优点是它允许“提升”的局部变量在委托和表达式树之间共享。

**信息性文本结束。**

## 12.17 查询表达式

### 12.17.1 总则

*查询表达式* 提供了一种语言集成的查询语法，其类似于 SQL 和 XQuery 等关系和分层查询语言。

```
query-expression:
    from-clause query-body

from-clause:
    from type_opt identifier in expression

query-body:
    from-clause query-body-clauses_opt select-or-group-clause query-continuation_opt

query-body-clauses:
    query-body-clause
    query-body-clauses query-body-clause

query-body-clause:
    from-clause
    let-clause
    where-clause
    join-clause
    join-into-clause
    orderby-clause

let-clause:
    let identifier = expression

where-clause:
    where boolean-expression

join-clause:
    join type_opt identifier in expression on expression equals expression

join-into-clause:
    join type_opt identifier in expression on expression equals expression into identifier

orderby-clause:
    orderby orderings

orderings:
    ordering
    orderings , ordering

ordering:
    expression ordering-direction_opt
```

```
ordering-direction:
    ascending
    descending

select-or-group-clause:
    select-clause
    group-clause

select-clause:
    select expression

group-clause:
    group expression by expression

query-continuation:
    into identifier query-body
```

查询表达式以 from 子句开始，以 select 或 group 子句结束。初始的 from 子句后可以跟零个或多个 from、let、where、join 或 orderby 子句。每个 from 子句是一个生成器，引入一个范围变量，该变量遍历序列的元素。每个 let 子句引入一个范围变量，表示通过先前的范围变量计算得到的值。每个 where 子句是一个过滤器，从结果中排除项目。每个 join 子句将源序列的指定键与另一个序列的键进行比较，产生匹配的对。每个 orderby 子句根据指定的条件重新排序项目。最后的 select 或 group 子句指定结果的形状，以范围变量表示。最后，可以使用 into 子句通过将一个查询的结果作为后续查询中的生成器来“拼接”查询。

### 12.17.2 查询表达式中的歧义

查询表达式使用若干上下文关键字（§7.4.4）：ascending、by、descending、equals、from、group、into、join、let、on、orderby、select 和 where。

为避免因这些标识符既用作关键字又用作简单名称而可能产生的歧义，这些标识符在查询表达式内的任何位置都被视为关键字，除非它们前面加上“@”（§7.4.4），在这种情况下它们被视为标识符。为此目的，查询表达式是任何以“from identifier”开头后跟除“；”、“=”或“，”以外的任何标记的表达式。

### 12.17.3 查询表达式翻译

### 12.17.3.1 总则

C# 语言未指定查询表达式的执行语义。相反，查询表达式被翻译为遵循查询表达式模式（§12.17.4）的方法的调用。具体来说，查询表达式被翻译为名为 where、Select、SelectMany、Join、GroupJoin、OrderBy、OrderByDescending、ThenBy、ThenByDescending、GroupBy 和 Cast 的方法的调用。这些方法预计具有特定的签名和返回类型，如 §12.17.4所述。这些方法可以是被查询对象的实例方法，也可以是对象外部的扩展方法。这些方法实现了查询的实际执行。

从查询表达式到方法调用的翻译是在执行任何类型绑定或重载解析之前发生的语法映射。在翻译查询表达式之后， resulting 方法调用被作为常规方法调用处理，这反过来可能会发现编译时错误。这些错误条件包括但不限于不存在的方法、错误类型的参数以及类型推断失败的泛型方法。

查询表达式通过反复应用以下翻译进行处理，直到不再可能进行进一步的简化。翻译按应用顺序列出：每个部分假设前面的部分的翻译已彻底执行，并且一旦耗尽，在同一查询表达式的处理中将不再重新访问该部分。




对于查询表达式来说，将赋值操作包含在范围变量中，或将范围变量用作 ref 或 out 参数的参数，是编译时错误。

某些转换会注入用 * 表示的透明标识符的范围变量。它们在 §12.17.3.8 中进一步描述。

## 12.17.3.2 select 和 group ... by 子句中的延续

使用 y 的属性 Prop 的 group 子句的查询表达式，且查询体 Q 包含如下形式的延续：

```
from y in S group y by y.Prop into x Q
```

被翻译为：

```
from x in ( from y in S group y by y.Prop ) Q
```

以下各节中的转换假定查询中没有 into 延续。

[示例：示例：

```
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```

被翻译为：

```
from g in
(from c in customers
    group c by c.Country)
select new { Country = g.Key, CustCount = g.Count() }
```

其最终翻译为：

```
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

示例结束]

## 12.17.3.3 显式的范围变量类型

显式指定范围变量类型的 from 子句

```
from T x in e
```

被翻译为

```
from x in ( e ) . Cast < T > ( )
```

显式指定范围变量类型的 join 子句

```
join T x in e on k1 equals k2
```

被翻译为

```
join x in ( e ) . Cast < T > ( ) on k1 equals k2
```

以下各节中的转换假定查询中没有显式的范围变量类型。

[示例：示例

```
from Customer c in customers
where c.City == "London"
select c
```

被翻译为

```
from c in (customers).Cast<Customer>()
where c.City == "London"
select c
```

其最终翻译为

```
customers.
Cast<Customer>().
Where(c => c.City == "London")
```

示例结束]

[注意：显式的范围变量类型对于查询实现非泛型 IEnumerable 接口但未实现泛型 IEnumerable<T> 接口的集合很有用。在上面的示例中，如果 customers 的类型为 ArrayList，则会是这种情况。 示例结束]

## 12.17.3.4 退化的查询表达式

形式为的查询表达式

```
from x in e select x
```

被翻译为

```
( e ) . Select ( x => x )
```

[示例：示例

```
from c in customers
select c
```

被翻译为

```
(customers).Select(c => c)
```

示例结束]

退化的查询表达式是指对源元素进行平凡选择的表达式。

## 12.17.3.5 From、let、where、join 和 orderby 子句

带有第二个 from 子句后跟 select 子句的查询表达式

```
from x1 in e1
from x2 in e2
select v
```

被翻译为

```
( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => v )
```

带有第二个 from 子句后跟包含非空查询体子句集的查询体 Q 的查询表达式：

```
from x1 in e1
from x2 in e2
Q
```

被翻译为

```
from * in ( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => new { x1 , x2 } )
Q
```

[示例：示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

被翻译为

```
from * in (customers).
SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

其最终翻译为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.OrderID, x.o.Total })
```

其中 x 是编译器生成的标识符，否则不可见且无法访问。 示例结束

let 表达式及其前面的 from 子句：

```
from x in e
let y = f
...
```

被翻译为

```
from * in ( e ) . Select ( x => new { x , y = f } )
...
```

[示例：示例

```
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```

被翻译为

```
from * in (orders).
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000
select new { o.OrderID, Total = t }
```

其最终翻译为

```
orders.
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) }).
Where(x => x.t >= 1000).
Select(x => new { x.o.OrderID, Total = x.t })
```

其中 x 是编译器生成的标识符，否则不可见且无法访问。 示例结束

where 表达式及其前面的 from 子句：

```
from x in e
where f
...
```

被翻译为

```
from x in ( e ) . Where ( x => f )
...
```

紧跟 select 子句的 join 子句

```
from x1 in e1
join x2 in e2 on k1 equals k2
select v
```

被翻译为

```
( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => v )
```

[示例：示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
select new { c.Name, o.OrderDate, o.Total }
```

被翻译为

```
(customers).Join(orders, c => c.CustomerID, o => o.CustomerID,
(c, o) => new { c.Name, o.OrderDate, o.Total })
```

示例结束

后跟查询体子句的 join 子句：

```
from x1 in e1
join x2 in e2 on k1 equals k2
...
```

被翻译为

```
from * in ( e1 ) . Join(
 e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => new { x1 , x2 })
...
```

紧跟 select 子句的 join-into 子句

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
select v
```

被翻译为

```
from * in ( e1 ) . GroupJoin(
 e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => new { x1 , x2 })
select v
```

[示例：示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID into co
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```

被翻译为

```
from * in (customers).
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
(c, co) => new { c, co })
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```

其最终翻译为

```
customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
(c, co) => new { c, co }).
Select(x => new { x, n = x.co.Count() }).
Where(y => y.n >= 10).
Select(y => new { y.x.c.Name, OrderCount = y.n })
```

其中 x 和 y 是编译器生成的标识符，否则不可见且无法访问。 示例结束

orderby 子句及其前面的 from 子句：

```
from x in e
orderby k1 , k2 , ... , kn
...
```

被翻译为

```
from x in ( e ).
OrderBy ( x => k1 ).
ThenBy ( x => k2 ).
...
ThenBy ( x => kn )
```

如果排序子句指定了降序方向指示符，则会生成 OrderByDescending 或 ThenByDescending 的调用。

[示例：示例

```
from o in orders
orderby o.Customer.Name, o.Total descending
select o
```

其最终翻译为

```
(orders).
OrderBy(o => o.Customer.Name).
ThenByDescending(o => o.Total)
```

示例结束

以下转换假定没有 let、where、join 或 orderby 子句，并且每个查询表达式中最多只有一个初始 from 子句。

## 12.17.3.6 Select 子句

形式为的查询表达式

```
from x in e select v
```

被翻译为

```
( e ) . Select ( x => v )
```

除非 v 是标识符 x，翻译仅为

```
( e )
```

> [示例：示例
> 
>     from c in customers.Where(c => c.City == "London")
>     select c
> 
> 仅被翻译为
> 
>     (customers).Where(c => c.City == "London")
> 
> 示例结束]

## 12.17.3.7 Group 子句

group 子句

```
from x in e group v by k
```

被翻译为

```
( e ) . GroupBy ( x => k , x => v )
```

除非 v 是标识符 x，翻译为

```
( e ) . GroupBy ( x => k )
```

> [示例：示例
> 
>     from c in customers
>     group c.Name by c.Country
> 
> 被翻译为
> 
>     (customers).
>     GroupBy(c => c.Country, c => c.Name)
> 
> 示例结束]

## 12.17.3.8 透明标识符

某些转换会注入用 * 表示的透明标识符的范围变量。透明标识符仅作为查询表达式转换过程中的中间步骤存在。

当查询转换注入透明标识符时，后续的转换步骤会将透明标识符传播到匿名函数和匿名对象初始化器中。在这些上下文中，透明标识符具有以下行为：

- 当透明标识符作为匿名函数的参数出现时，相关匿名类型的成员会在匿名函数体中自动进入作用域。
- 当带有透明标识符的成员在作用域内时，该成员的成员也在作用域内。
- 当透明标识符作为匿名对象初始化器中的成员声明符出现时，它会引入一个具有透明标识符的成员。

在上述描述的转换步骤中，透明标识符始终与匿名类型一起引入，其目的是将多个范围变量作为单个对象的成员捕获。C# 的实现可以使用不同于匿名类型的机制来将多个范围变量组合在一起。以下转换示例假定使用匿名类型，并展示了透明标识符的一种可能转换。

[示例：示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```

被翻译为

```
from * in (customers).
    SelectMany(c => c.Orders, (c,o) => new { c, o })
    orderby o.Total descending
    select new { c.Name, o.Total }
```

进一步被翻译为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(* => o.Total).
Select(* => new { c.Name, o.Total })
```

当透明标识符被擦除时，等价于

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.Total })
```

其中 x 是一个编译器生成的标识符，否则不可见且无法访问。

示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```

被翻译为

```
from * in (customers).
    Join(orders, c => c.CustomerID, o => o.CustomerID,
    (c, o) => new { c, o })
    join d in details on o.OrderID equals d.OrderID
    join p in products on d.ProductID equals p.ProductID
    select new { c.Name, o.OrderDate, p.ProductName }
```

进一步简化为

```
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o }).
Join(details, * => o.OrderID, d => d.OrderID, (*, d) => new { *, d }).
Join(products, * => d.ProductID, p => p.ProductID, (*, p) => new { *, p }).
Select(* => new { c.Name, o.OrderDate, p.ProductName })
```

其最终翻译为

```
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID,
    (c, o) => new { c, o }).
Join(details, x => x.o.OrderID, d => d.OrderID,
    (x, d) => new { x, d }).
Join(products, y => y.d.ProductID, p => p.ProductID,
    (y, p) => new { y, p }).
Select(z => new { z.y.x.c.Name, z.y.x.o.OrderDate, z.p.ProductName })
```

其中 x、y 和 z 是编译器生成的标识符，否则不可见且无法访问。

[end example]

### 12.17.4 查询表达式模式

查询表达式模式建立了一组方法模式，类型可以实现这些模式来支持查询表达式。

一个泛型类型 C<T> 支持查询表达式模式，如果其公共成员方法和可公开访问的扩展方法可以被以下类定义所替代。成员和可访问的扩展方法被称为泛型类型 C<T> 的“形状”。使用泛型类型是为了说明参数类型和返回类型之间的正确关系，但也可以为非泛型类型实现该模式。

```
delegate R Func<T1,R>(T1 arg1);
delegate R Func<T1,T2,R>(T1 arg1, T2 arg2);
class C
{
    public C<T> Cast<T>();
}
class C<T> : C
{
    public C<T> Where(Func<T,bool> predicate);
    public C<U> Select<U>(Func<T,U> selector);
    public C<V> SelectMany<U,V>(Func<T,U> selector, Func<T,U,V> resultSelector);
    public C<V> Join<U,K,V>(C<U> inner, Func<T,K> outerKeySelector, Func<U,K> innerKeySelector, Func<T,U,V> resultSelector);
    public C<V> GroupJoin<U,K,V>(C<U> inner, Func<T,K> outerKeySelector, Func<U,K> innerKeySelector, Func<T,U,V> resultSelector);
    public O<T> OrderBy<K>(Func<T,K> keySelector);
    public O<T> OrderByDescending<K>(Func<T,K> keySelector);
    public C<G<K,T>> GroupBy<K>(Func<T,K> keySelector);
    public C<G<K,E>> GroupBy<K,E>(Func<T,K> keySelector, Func<T,K,E> elementSelector);
}
class O<T> : C<T>
{
    public O<T> ThenBy<K>(Func<T,K> keySelector);
    public O<T> ThenByDescending<K>(Func<T,K> keySelector);
}
class G<K,T> : C<T>
{
    public K Key { get; }
}
```

上述方法使用泛型委托类型 Func<T1, R> 和 Func<T1,T2,R>，但它们同样可以使用具有相同参数和返回类型关系的其他委托或表达式树类型。

> [Note: 建议的 C<T> 与 O<T> 之间的关系可确保 ThenBy 和 ThenByDescending 方法仅在 OrderBy 或 OrderByDescending 的结果上可用。 end note]

> [Note: GroupBy 结果的推荐形状是一个序列的序列，其中每个内部序列都有一个额外的 Key 属性。 end note]

> [Note: 因为查询表达式是通过语法映射转换为方法调用，所以类型在实现查询表达式模式的任何部分时具有相当大的灵活性。例如，模式的方法可以实现为实例方法或扩展方法，因为两者具有相同的调用语法，并且方法可以请求委托或表达式树，因为匿名函数可以转换为两者。仅实现查询表达式模式部分的类型仅支持映射到该类型支持的方法的查询表达式转换。 end note]

[Note: System.Linq 命名空间为实现 System.Collections.Generic.IEnumerable<T> 接口的任何类型提供了查询表达式模式的实现。 end note]

## 12.18 赋值运算符

### 12.18.1 通用

赋值运算符为变量、属性、事件或索引器元素分配新值。

```
assignment:
    unary-expression  assignment-operator  expression

assignment-operator:
    =
    +=
    -=
    *=
    /=
    %=
    &=
    |=
    ^=
    <<=
    right-shift-assignment
```

赋值的左操作数应为被归类为变量、属性访问、索引器访问或事件访问的表达式。

= 运算符称为简单赋值运算符。它将右操作数的值赋给左操作数指定的变量、属性或索引器元素。简单赋值运算符的左操作数不得为事件访问（§15.8.2所述情况除外）。简单赋值运算符在 §12.18.2 中描述。

除 = 运算符之外的赋值运算符称为复合赋值运算符。这些运算符对两个操作数执行指示的操作，然后将结果值赋给左操作数指定的变量、属性或索引器元素。复合赋值运算符在 §12.18.3 中描述。

具有事件访问表达式作为左操作数的 += 和 -= 运算符称为事件赋值运算符。没有其他赋值运算符在左操作数为事件访问时有效。事件赋值运算符在 §12.18.4 中描述。

赋值运算符是右结合的，这意味着操作从右到左分组。[示例：形式为 a = b = c 的表达式被求值为 a = (b = c)。 end example]

### 12.18.2 简单赋值

= 运算符称为简单赋值运算符。

如果简单赋值的左操作数形式为 E.P 或 E[Ei] 且 E 的编译时类型为 dynamic，则赋值是动态绑定的（§12.3.3）。在这种情况下，赋值表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时基于 E 的运行时类型进行。如果左操作数形式为 E[Ei] 且 Ei 中的至少一个元素具有编译时类型 dynamic，并且 E 的编译时类型不是数组，则 resulting 索引器访问是动态绑定的，但具有有限的编译时检查（§12.6.5）。

在简单赋值中，右操作数应为可隐式转换为左操作数类型的表达式。操作将右操作数的值赋给左操作数指定的变量、属性或索引器元素。

简单赋值表达式的结果是赋给左操作数的值。结果具有与左操作数相同的类型，并且始终被归类为值。

如果左操作数是属性或索引器访问，则属性或索引器应具有可访问的 set 访问器。如果不是，则会发生绑定时错误。

形式为 x = y 的简单赋值的运行时处理包括以下步骤：

- 如果 x 被归类为变量：
    - x 被求值以产生变量。
    - y 被求值，并在需要时通过隐式转换（§11.2）转换为 x 的类型。
    - 如果 x 给出的变量是引用类型的数组元素，则会执行运行时检查，以确保为 y 计算的值与 x 所属的数组实例兼容。检查在 y 为 null 时成功，或当从 y 引用的实例的类型到包含 x 的数组实例的实际元素类型存在隐式引用转换（§11.2.7）时成功。否则，将抛出 System.ArrayTypeMismatchException。
    - y 的求值和转换结果存储到 x 的求值所给出的位置中。
- 如果 x 被归类为属性或索引器访问：
    - 与 x 关联的实例表达式（如果 x 不是静态的）和参数列表（如果 x 是索引器访问）被求值，结果用于随后的 set 访问器调用。
    - y 被求值，并在需要时通过隐式转换（§11.2）转换为 x 的类型。
    - x 的 set 访问器被调用，其值参数为为 y 计算的值。

[Note: 如果 x 的编译时类型为 dynamic 且 y 的编译时类型到 dynamic 存在隐式转换，则不需要运行时解析。 end note]

[Note: 数组协变规则（§17.6）允许数组类型 A[] 的值引用数组类型 B[] 的实例，前提是从 B 到 A 存在隐式引用转换。由于这些规则，对引用类型的数组元素的赋值需要运行时检查，以确保被赋的值与数组实例兼容。在示例中

```
string[] sa = new string[10];
object[] oa = sa;
oa[0] = null;        // Ok
oa[1] = "Hello";     // Ok
oa[2] = new ArrayList(); // ArrayTypeMismatchException
```

最后一次赋值会抛出 System.ArrayTypeMismatchException，因为对 ArrayList 的引用不能存储在 string[] 的元素中。 end note]

当在 struct 类型中声明的属性或索引器是赋值的目标时，与属性或索引器访问关联的实例表达式应被归类为变量。如果实例表达式被归类为值，则会发生绑定时错误。[Note: 由于 §12.7.5，相同的规则也适用于字段。 end note]

[Example: 给定声明：

```
struct Point
{
    int x, y;
```




```csharp
public Point(int x, int y) {
    this.x = x;
    this.y = y;
}
public int X {
    get { return x; }
    set { x = value; }
}
public int Y {
    get { return y; }
    set { y = value; }
}
struct Rectangle
{
    Point a, b;
    public Rectangle(Point a, Point b) {
        this.a = a;
        this.b = b;
    }
    public Point A {
        get { return a; }
        set { a = value; }
    }
    public Point B {
        get { return b; }
        set { b = value; }
    }
}
```

在示例中

```csharp
Point p = new Point();
p.X = 100;
p.Y = 100;
Rectangle r = new Rectangle();
r.A = new Point(10, 10);
r.B = p;
```

对 p.X、p.Y、r.A 和 r.B 的赋值是允许的，因为 p 和 r 是变量。然而，在示例中

```csharp
Rectangle r = new Rectangle();
r.A.X = 10;
r.A.Y = 10;
r.B.X = 100;
r.B.Y = 100;
```

这些赋值全部无效，因为 r.A 和 r.B 不是变量。示例结束

## 12.18.3 复合赋值

如果复合赋值的左操作数形式为 E.P 或 E[E1]，其中 E 的编译时类型为 dynamic，则该赋值是动态绑定的（§12.3.3）。在这种情况下，赋值表达式的编译时类型为 dynamic，下述解析过程将在运行时根据 E 的运行时类型进行。如果左操作数形式为 E[E1]，其中 E1 中至少有一个元素的编译时类型为 dynamic，且 E 的编译时类型不是数组，则所产生的索引器访问是动态绑定的，但只进行有限的编译时检查（§12.6.5）。

形式为 x op= y 的操作通过应用二元运算符重载解析（§12.4.5）进行处理，就如同该操作写作 x op y 一样。然后：

- 如果所选运算符的返回类型可隐式转换为 x 的类型，则操作按 x = x op y 计算，但 x 仅求值一次。
- 否则，如果所选运算符是预定义运算符，且所选运算符的返回类型可显式转换为 x 的类型，并且 y 可隐式转换为 x 的类型或该运算符是移位运算符，则操作按 x = (T)(x op y) 计算，其中 T 是 x 的类型，但 x 仅求值一次。
- 否则，复合赋值无效，并发生绑定时间错误。

术语“仅求值一次”指的是：在计算 x op y 时，x 的任何构成表达式的结果会被临时保存，然后在执行对 x 的赋值时重新使用。[示例：在赋值语句 A() [B()] += C() 中，A 是返回 int[] 的方法，B 和 C 是返回 int 的方法，这些方法仅被调用一次，调用顺序为 A、B、C。示例结束]

当复合赋值的左操作数是属性访问或索引器访问时，该属性或索引器必须同时具有 get 访问器和 set 访问器。否则，将发生绑定时间错误。

上述第二条规则允许在某些情况下将 x op= y 计算为 x = (T)(x op y)。该规则的存在是为了使预定义运算符在左操作数为 sbyte、byte、short、ushort 或 char 类型时能够用作复合运算符。即使两个参数都属于这些类型之一，预定义运算符也会生成 int 类型的结果，如 §12.4.7.3 所述。因此，如果没有强制转换，就不可能将结果赋值给左操作数。

预定义运算符规则的直观效果就是：如果 x op y 和 x = y 均被允许，那么 x op= y 就被允许。[示例：在以下代码中

```csharp
byte b = 0;
char ch = '\0';
int i = 0;

b += 1;    // Ok
b += 1000; // Error, b = 1000 not permitted
b += i;    // Error, b = i not permitted
b += (byte)i; // Ok
ch += 1;   // Error, ch = 1 not permitted
ch += (char)1; // Ok
```

每个错误的直观原因是对应的简单赋值也会是错误的。示例结束

[注意：这也意味着复合赋值操作支持提升运算符。由于复合赋值 x op= y 被计算为 x = x op y 或 x = (T)(x op y)，求值规则隐式覆盖了提升运算符。注意结束]

## 12.18.4 事件赋值

如果 += 或 -= 运算符的左操作数被分类为事件访问，则按如下方式计算该表达式：

- 计算事件访问的实例表达式（如果有）。
- 计算 += 或 -= 运算符的右操作数，并在需要时通过隐式转换（§11.2）转换为左操作数的类型。
- 调用该事件的事件访问器，参数列表由上一步计算出的值组成。如果运算符是 +=，则调用 add 访问器；如果运算符是 -=，则调用 remove 访问器。

事件赋值表达式不产生值。因此，事件赋值表达式仅在语句表达式（§13.7）的上下文中有效。

## 12.19 表达式

表达式要么是非赋值表达式，要么是赋值。

```
expression:
  non-assignment-expression
  assignment
```

```
non-assignment-expression:
  conditional-expression
  lambda-expression
  query-expression
```

## 12.20 常量表达式

常量表达式是应在编译时完全计算的表达式。

```
constant-expression:
  expression
```

常量表达式可以是值类型或引用类型。如果常量表达式是值类型，则它必须是以下类型之一：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool 或任何枚举类型。如果常量表达式是引用类型，则它必须是 string 类型、某个引用类型的默认值表达式（§12.7.15），或者表达式的值必须为 null。

常量表达式中仅允许以下构造：

- 字面量（包括 null 字面量）。
- 对类和结构体类型的 const 成员的引用。
- 对枚举类型成员的引用。
- 对 const 参数或局部变量的引用。
- 括号子表达式，其本身是常量表达式。
- 强制转换表达式。
- checked 和 unchecked 表达式。
- 预定义的 +、-、!、~ 一元运算符。
- 预定义的 +、-、*、/、%、<<、>>、&、|、^、&&、||、==、!=、<、>、<= 和 >= 二元运算符。
- ?: 条件运算符。
- sizeof 表达式，前提是非托管类型是 §23.6.9 中指定的类型之一，对于这些类型，sizeof 返回常量值。
- 默认值表达式，前提是该类型是上面列出的类型之一。

常量表达式中允许以下转换：

- 恒等转换
- 数值转换
- 枚举转换
- 常量表达式转换
- 隐式和显式引用转换，前提是转换的源是计算结果为 null 值的常量表达式。

> [注意：其他转换，包括装箱、拆箱以及非 null 值的隐式引用转换，不允许出现在常量表达式中。注意结束]

[示例：在以下代码中

```
class C {
    const object i = 5; // error: boxing conversion not permitted
    const object str = "hello"; // error: implicit reference conversion
}
```

i 的初始化是错误的，因为需要装箱转换。str 的初始化是错误的，因为需要从非 null 值进行隐式引用转换。示例结束]

每当表达式满足上述要求时，该表达式都会在编译时计算。即使该表达式是包含非常量构造的更大表达式中的子表达式，也是如此。

常量表达式的编译时计算使用与非常量表达式的运行时计算相同的规则，只不过在运行时计算会引发异常的地方，编译时计算会导致发生编译时错误。

除非常量表达式被显式放置在 unchecked 上下文中，否则在表达式编译时计算期间，整型算术运算和转换中发生的溢出总是会导致编译时错误（§12.7.14）。

在下面列出的上下文中需要常量表达式，这通过语法中的 constant-expression 来表示。在这些上下文中，如果表达式无法在编译时完全计算，则会发生编译时错误。

- 常量声明（§15.4）
- 枚举成员声明（§19.4）
- 形参列表的默认参数（§15.6.2）
- switch 语句的 case 标签（§13.8.3）。
- goto case 语句（§13.10.4）
- 包含初始化器的数组创建表达式中的维度长度（§12.7.11.5）
- 特性（§22）

隐式常量表达式转换（§11.2.10）允许将 int 类型的常量表达式转换为 sbyte、byte、short、ushort、uint 或 ulong，前提是该常量表达式的值在目标类型的范围内。

## 12.21 布尔表达式

布尔表达式是产生 bool 类型结果的表达式；要么直接产生，要么在如下指定的某些上下文中通过应用 true 运算符来产生：

```
boolean-expression:
    expression
```

if 语句（§13.8.2）、while 语句（§13.9.2）、do 语句（§13.9.3）或 for 语句（§13.9.4）的控制条件表达式是布尔表达式。?: 运算符（§12.15）的控制条件表达式遵循与布尔表达式相同的规则，但由于运算符优先级的原因，被分类为条件或表达式。

要求布尔表达式 E 能够产生 bool 类型的值，如下所示：

- 如果 E 可隐式转换为 bool，则在运行时应用该隐式转换。
- 否则，使用一元运算符重载解析（§12.4.4）在 E 上查找唯一最佳的 true 运算符实现，并在运行时应用该实现。
- 如果找不到此类运算符，则发生绑定时间错误。




## 13. 语句

### 13.1 通用

C# 提供了多种语句。 [Note: 其中大多数语句对曾使用 C 和 C++ 进行编程的开发人员来说都很熟悉。 end note]

- statement:
  - labeled-statement
  - declaration-statement
  - embedded-statement
- embedded-statement:
  - block
  - empty-statement
  - expression-statement
  - selection-statement
  - iteration-statement
  - jump-statement
  - try-statement
  - checked-statement
  - unchecked-statement
  - lock-statement
  - using-statement
  - yield-statement

embedded-statement 非终结符用于出现在其他语句内的语句。使用 embedded-statement 而不是 statement 排除了在这些上下文中使用声明语句和标记语句。 [Example: The code

```
void F(bool b) {
    if (b)
        int i = 44;
}
```

导致编译时错误，因为 if 语句要求其 if 分支使用 embedded-statement 而不是 statement。如果允许这段代码，则变量 i 将被声明，但它永远无法使用。注意，通过将 i 的声明放在块中，该示例是有效的。 end example]

### 13.2 终点和可达性

每个语句都有一个终点。直观地说，语句的终点是紧跟在该语句之后的位置。复合语句（包含嵌入语句的语句）的执行规则指定了当控制到达嵌入语句的终点时采取的动作。 [Example: 当控制到达块中语句的终点时，控制会转移到块中的下一个语句。 end example]

如果语句可以通过执行到达，则称该语句是可达的。相反，如果语句不可能被执行，则称该语句是不可达的。

[Example: In the following code

```
void F() {
    Console.WriteLine("reachable");
    goto Label;
    Console.WriteLine("unreachable");
    Label:
    Console.WriteLine("reachable");
}
```

第二个 Console.WriteLine 调用是不可达的，因为该语句不可能被执行。 end example]

如果编译器确定某个语句不可达，则会报告警告。特别地，语句不可达并不是错误。

[Note: 为了确定特定语句或终点是否可达，编译器会根据为每个语句定义的<|message|> 可达性规则执行流分析。流分析会考虑控制语句行为的常量表达式 (§12.20) 的值，但不考虑非常量表达式的可能值。换句话说，就控制流分析而言，给定类型的非常量表达式被认为具有该类型的任何可能值。

In the example

```
void F() {
    const int i = 1;
    if (i == 2) Console.WriteLine("unreachable");
}
```

if 语句的布尔表达式是常量表达式，因为 == 运算符的两个操作数都是常量。由于常量表达式在编译时求值，产生值 false，因此 Console.WriteLine 调用被认为不可达。然而，如果将 i 改为局部变量

```
void F() {
    int i = 1;
    if (i == 2) Console.WriteLine("reachable");
}
```

则 Console.WriteLine 调用被认为可达，即使实际上它永远不会被执行。 end note]

函数成员或匿名函数的块始终被认为可达。通过依次评估块中每个语句的可达性规则，可以确定任何给定语句的可达性。

[Example: In the following code

```
void F(int x) {
    Console.WriteLine("start");
    if (x < 0) Console.WriteLine("negative");
}
```

第二个 Console.WriteLine 的可达性确定如下：

- 第一个 Console.WriteLine 表达式语句是可达的，因为 F 方法的块是可达的 (§13.3)。
- 第一个 Console.WriteLine 表达式语句的终点是可达的，因为该语句是可达的 (§13.7 和 §13.3)。
- if 语句是可达的，因为第一个 Console.WriteLine 表达式语句的终点是可达的 (§13.7 和 §13.3)。
- 第二个 Console.WriteLine 表达式语句是可达的，因为 if 语句的布尔表达式不具有常量值 false。

end example]

存在两种情况，如果语句的终点可达，则为编译时错误：

- 因为 switch 语句不允许 switch 部分“贯穿”到下一个 switch 部分，所以 switch 部分的语句列表的终点可达是编译时错误。如果发生此错误，通常表示缺少 break 语句。
- 函数成员或计算值的匿名函数的块的终点可达是编译时错误。如果发生此错误，通常表示缺少 return 语句 (§13.10.5)。

### 13.3 块

#### 13.3.1 通用

块允许在只允许单个语句的上下文中编写多个语句。

```
block:
    { statement-list_opt }
```

块由可选的语句列表 (§13.3.2) 组成，用大括号括起来。如果省略语句列表，则块称为空块。

块可以包含声明语句 (§13.6)。在块中声明的局部变量或常量的作用域是该块。

在块内，在表达式上下文中使用的名称的含义始终相同 (§12.7.3.2)。

块的执行如下：

- 如果块为空，则控制转移到块的终点。
- 如果块不为空，则控制转移到语句列表。当且仅当控制到达语句列表的终点时，控制转移到块的终点。

如果块本身可达，则块的语句列表可达。

如果块为空或语句列表的终点可达，则块的终点可达。

包含一个或多个 yield 语句 (§13.15) 的块称为迭代器块。迭代器块用于将函数成员实现为迭代器 (§15.14)。迭代器块适用一些额外的限制：

- 在迭代器块中出现 return 语句是编译时错误（但允许 yield return 语句）。
- 迭代器块包含不安全上下文 (§23.2) 是编译时错误。迭代器块始终定义安全上下文，即使其声明嵌套在不安全上下文中。

#### 13.3.2 语句列表

语句列表由按顺序编写的一个或多个语句组成。语句列表出现在块 (§13.3) 和 switch 块 (§13.8.3) 中。

```
statement-list:
    statement
    statement-list statement
```

语句列表的执行是通过将控制转移到第一个语句。当且仅当控制到达某个语句的终点时，控制转移到下一个语句。当且仅当控制到达最后一个语句的终点时，控制转移到语句列表的终点。

如果满足以下条件之一，则语句列表中的语句是可达的：

- 该语句是第一个语句且语句列表本身可达。
- 前一个语句的终点可达。
- 该语句是标记语句且标签被可达的 goto 语句引用。

如果列表中最后一个语句的终点可达，则语句列表的终点可达。

### 13.4 空语句

empty-statement 不执行任何操作。

```
empty-statement:
    ;
```

当需要在需要语句的上下文中不执行任何操作时使用空语句。

空语句的执行只是将控制转移到该语句的终点。因此，如果空语句可达，则空语句的终点可达。

[Example: An empty statement can be used when writing a while statement with a null body:

```
bool ProcessMessage() {...}
void ProcessMessages() {
    while (ProcessMessage())
        ;
}
```

Also, an empty statement can be used to declare a label just before the closing “}” of a block:

```
void F() {
    ...
    if (done) goto exit;
    ...
    exit: ;
}
```

end example]

### 13.5 标记语句

labeled-statement 允许语句前面加上标签。标记语句允许在块中出现，但不允许作为嵌入语句。

```
labeled-statement:
    identifier : statement
```

标记语句使用标识符给出的名称声明一个标签。标签的作用域是声明该标签的整个块，包括任何嵌套块。两个具有相同名称的标签具有重叠作用域是编译时错误。

标签可以在标签作用域内从 goto 语句 (§13.10.4) 引用。 [Note: This means that goto statements can transfer control within blocks and out of blocks, but never into blocks. end note]

标签具有自己的声明空间，并且不会干扰其他标识符。 [Example: The example

```
int F(int x) {
    if (x >= 0) goto x;
    x = -x;
    x: return x;
}
```

is valid and uses the name x as both a parameter and a label. end example]

标记语句的执行完全对应于标签后语句的执行。




除了正常控制流提供的可达性之外，如果某个标签被一个可达的 goto 语句引用，则带标签的语句是可达的，除非该 goto 语句位于一个 try 语句的 try 块或 catch 块内，而该 try 语句包含一个终点不可达的 finally 块，并且该带标签的语句位于该 try 语句之外。

## 13.6 声明语句

### 13.6.1 概述

声明语句声明局部变量或常量。声明语句允许出现在块中，但不允许作为嵌入语句。

```
declaration-statement:
    local-variable-declaration ;
    local-constant-declaration ;
```

### 13.6.2 局部变量声明

局部变量声明声明一个或多个局部变量。

```
local-variable-declaration:
    local-variable-type local-variable-declarators

local-variable-type:
    type
    var

local-variable-declarators:
    local-variable-declarator
    local-variable-declarators , local-variable-declarator

local-variable-declarator:
    identifier
    identifier = local-variable-initializer

local-variable-initializer:
    expression
    array-initializer
```

局部变量声明的 local-variable-type 要么直接指定该声明所引入变量的类型，要么用标识符 var 指示应根据初始值推断类型。类型之后是局部变量声明符列表，每个声明符引入一个新变量。局部变量声明符由一个命名该变量的标识符组成，后面可选地跟一个“=”标记和一个给出该变量初始值的 local-variable-initializer。

在局部变量声明的上下文中，标识符 var 充当上下文关键字（§7.4.4）。当 local-variable-type 指定为 var，且作用域中没有名为 var 的类型时，该声明是隐式类型的局部变量声明，其类型从关联的初始值设定项表达式的类型推断。隐式类型的局部变量声明受以下限制：

- 该局部变量声明不能包含多个 local-variable-declarator。
- 该 local-variable-declarator 应包含一个 local-variable-initializer。
- 该 local-variable-initializer 应为表达式。
- 该初始值设定项表达式应具有编译时类型。
- 该初始值设定项表达式不能引用所声明的变量自身。

[示例：以下是不正确的隐式类型局部变量声明：

```
var x; // Error, no initializer to infer type from
var y = {1, 2, 3}; // Error, array initializer not permitted
var z = null; // Error, null does not have a type
var u = x => x + 1; // Error, anonymous functions do not have a type
var v = v++; // Error, initializer cannot refer to v itself
```

示例结束]

局部变量的值在表达式中通过简单名称（§12.7.3）获取，局部变量的值通过赋值（§12.18）修改。在获取局部变量值的每个位置，该局部变量都应明确赋值（§10.4）。

在局部变量声明中声明的局部变量，其作用域是声明所在的块。在文本位置上先于该局部变量的 local-variable-declarator 引用该局部变量是错误的。在局部变量的作用域内，声明另一个同名局部变量或常量是编译时错误。

声明多个变量的局部变量声明等价于多个具有相同类型的单变量声明。此外，局部变量声明中的变量初始值设定项完全对应于紧接在声明之后插入的赋值语句。

[示例：以下示例

```
void F() {
    int x = 1, y, z = x * 2;
}
```

完全对应于

```
void F() {
    int x; x = 1;
    int y;
    int z; z = x * 2;
}
```

示例结束]

在隐式类型的局部变量声明中，所声明局部变量的类型被视为与用于初始化该变量的表达式的类型相同。[示例：]

```
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
```

上面的隐式类型局部变量声明完全等价于以下显式类型声明：

```
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
```

### 13.6.3 局部常量声明

局部常量声明声明一个或多个局部常量。

```
local-constant-declaration:
    const type constant-declarators

constant-declarators:
    constant-declarator
    constant-declarators , constant-declarator

constant-declarator:
    identifier = constant-expression
```

局部常量声明的类型指定该声明所引入常量的类型。

类型之后是常量声明符列表，每个声明符引入一个新常量。常量声明符由一个命名该常量的标识符组成，后面跟一个“=”标记，再跟一个给出该常量值的常量表达式（§12.20）。

局部常量声明的类型和常量表达式应遵循与常量成员声明（§15.4）相同的规则。

局部常量的值在表达式中通过简单名称（§12.7.3）获取。

局部常量的作用域是声明所在的块。在文本位置上先于其 constant-declarator 末尾引用该局部常量是错误的。在局部常量的作用域内，声明另一个同名局部变量或常量是编译时错误。

声明多个常量的局部常量声明等价于多个具有相同类型的单常量声明。

## 13.7 表达式语句

表达式语句计算给定表达式。该表达式计算出的值（如果有）将被丢弃。

```
expression-statement:
    statement-expression ;
```

```
statement-expression:
    invocation-expression
    object-creation-expression
    assignment
    post-increment-expression
    post-decrement-expression
    pre-increment-expression
    pre-decrement-expression
    await-expression
```

并非所有表达式都允许作为语句。[注意：特别是像 x + y 和 x == 1 这样仅仅计算一个值（该值将被丢弃）的表达式，不允许作为语句。注意结束]

执行表达式语句会计算其中包含的表达式，然后将控制转移到该表达式语句的终点。如果该表达式语句可达，则该表达式语句的终点可达。

## 13.8 选择语句

### 13.8.1 概述

选择语句根据某个表达式的值，从若干可能的语句中选择一个执行。

```
selection-statement:
    if-statement
    switch-statement
```

### 13.8.2 if 语句

if 语句根据布尔表达式的值选择要执行的语句。

```
if-statement:
    if ( boolean-expression ) embedded-statement
    if ( boolean-expression ) embedded-statement else embedded-statement
```

else 部分与语法允许的词法上最近的前面一个 if 相关联。[示例：因此，形式如下的 if 语句

```
if (x) if (y) F(); else G();
```

等价于

```
if (x) {
    if (y) {
        F();
    }
    else {
        G();
    }
}
```

示例结束]

if 语句的执行方式如下：

- 计算布尔表达式（§12.21）。
- 如果布尔表达式产生 true，则控制转移到第一个嵌入语句。当且如果控制到达该语句的终点，则控制转移到 if 语句的终点。
- 如果布尔表达式产生 false 且存在 else 部分，则控制转移到第二个嵌入语句。当且如果控制到达该语句的终点，则控制转移到 if 语句的终点。
- 如果布尔表达式产生 false 且不存在 else 部分，则控制转移到 if 语句的终点。

如果 if 语句可达且布尔表达式不具有常量值 false，则 if 语句的第一个嵌入语句可达。

如果存在 if 语句的第二个嵌入语句，则当 if 语句可达且布尔表达式不具有常量值 true 时，该第二个嵌入语句可达。

如果 if 语句的至少一个嵌入语句的终点可达，则该 if 语句的终点可达。此外，如果 if 语句可达且布尔表达式不具有常量值 true，则没有 else 部分的 if 语句的终点可达。

### 13.8.3 switch 语句

switch 语句选择执行一个语句列表，该语句列表具有与 switch 表达式的值相对应的关联 switch 标签。

```
switch-statement:
    switch ( expression ) switch-block

switch-block:
    { switch-sections_opt }

switch-sections:
    switch-section
    switch-sections switch-section

switch-section:
    switch-labels statement-list
```


```
switch-labels:
    switch-label
    switch-labels switch-label

switch-label:
    case constant-expression :
    default :
```

switch 语句由关键字 switch 组成，后跟一个带括号的表达式（称为 switch 表达式），后跟一个 switch 块。switch 块由零个或多个用大括号括起来的 switch 部分组成。每个 switch 部分由一个或多个 switch 标签后跟一个语句列表（§13.3.2）组成。

switch 语句的控制类型由 switch 表达式确定。

- 如果 switch 表达式的类型是 sbyte、byte、short、ushort、int、uint、long、ulong、char、bool、string 或 enum 类型，或者是这些类型之一对应的可空值类型，则该类型就是 switch 语句的控制类型。
- 否则，从 switch 表达式的类型到以下可能的控制类型之一必须存在且仅存在一个用户定义的隐式转换：sbyte、byte、short、ushort、int、uint、long、ulong、char、string，或这些类型之一对应的可空值类型。
- 否则，会发生编译时错误。

每个 case 标签的常量表达式应表示一种类型的值，该类型可隐式转换为 switch 语句的控制类型（§11.2）。如果同一个 switch 语句中两个或多个 case 标签指定了相同的常量值，则会发生编译时错误。

switch 语句中最多只能有一个 default 标签。

switch 语句的执行方式如下：

- 计算 switch 表达式并将其转换为控制类型。
- 如果同一个 switch 语句中某个 case 标签指定的常量之一等于 switch 表达式的值，则控制转移到匹配的 case 标签之后的语句列表。
- 如果同一个 switch 语句中 case 标签指定的常量均不等于 switch 表达式的值，且存在 default 标签，则控制转移到 default 标签之后的语句列表。
- 如果同一个 switch 语句中 case 标签指定的常量均不等于 switch 表达式的值，且不存在 default 标签，则控制转移到 switch 语句的终点。

如果 switch 部分的语句列表的终点可达，则会发生编译时错误。这被称为“禁止贯穿执行”规则。[示例：示例

```
switch (j) {
    case 0:
        CaseZero();
        break;
    case 1:
        CaseOne();
        break;
    default:
        CaseOthers();
        break;
}
```

是有效的，因为没有任何 switch 部分具有可达的终点。与 C 和 C++ 不同，不允许 switch 部分的执行“贯穿”到下一个 switch 部分，并且示例

```
switch (i) {
    case 0:
        CaseZero();
    case 1:
        CaseZeroOrOne();
    default:
        CaseAny();
}
```

会导致编译时错误。当 switch 部分的执行需要随后执行另一个 switch 部分时，应使用显式的 goto case 或 goto default 语句：

```
switch (i) {
    case 0:
        CaseZero();
        goto case 1;
    case 1:
        CaseZeroOrOne();
        goto default;
    default:
        CaseAny();
        break;
}
```

结束示例]

switch 部分中允许使用多个标签。[示例：示例

```
switch (i) {
    case 0:
        CaseZero();
        break;
    case 1:
        CaseOne();
        break;
    case 2:
    default:
        CaseTwo();
        break;
}
```

是有效的。示例未违反“禁止贯穿执行”规则，因为标签 case 2: 和 default: 是同一 switch 部分的一部分。结束示例]

[注意： “禁止贯穿执行”规则可防止 C 和 C++ 中因意外省略 break 语句而导致的一类常见错误。例如，上述 switch 语句的部分可以反转而不影响语句的行为：

```
switch (i) {
    default:
        CaseAny();
        break;
    case 1:
        CaseZeroOrOne();
        goto default;
    case 0:
        CaseZero();
        goto case 1;
}
```

结束注意]

[注意：switch 部分的语句列表通常以 break、goto case 或 goto default 语句结束，但任何使语句列表终点不可达的构造都是允许的。例如，由布尔表达式 true 控制的 while 语句已知永远不会到达其终点。同样，throw 或 return 语句总是将控制转移到其他地方，永远不会到达其终点。因此，以下示例是有效的：

```
switch (i) {
    case 0:
        while (true) F();
    case 1:
        throw new ArgumentException();
    case 2:
        return;
}
```

结束注意]

[示例：switch 语句的控制类型可以是类型 string。例如：

```
void DoCommand(string command) {
    switch (command.ToLower()) {
        case "run":
            DoRun();
            break;
        case "save":
            DoSave();
            break;
        case "quit":
            DoQuit();
            break;
        default:
            InvalidCommand(command);
            break;
    }
}
```

结束示例]

> > [注意：与字符串相等运算符（§12.11.8）类似，switch 语句区分大小写，并且
> > 仅当 switch 表达式字符串与 case 标签常量完全匹配时才会执行给定的 switch 部分。
> > 结束注意]

当 switch 语句的控制类型为 string 或可空值类型时，值 null 可作为 case 标签常量使用。

switch 块的语句列表中可以包含声明语句（§13.6）。在 switch 块中声明的局部变量或常量的作用域为 switch 块。

在 switch 块内，在表达式上下文中使用的名称的含义始终相同（§12.7.3.2）。

如果 switch 语句可达且以下至少一项为真，则给定 switch 部分的语句列表可达：

- switch 表达式是非常量值。
- switch 表达式是常量值且与 switch 部分中的 case 标签匹配。
- switch 表达式是常量值且与任何 case 标签都不匹配，并且 switch 部分包含 default 标签。
- switch 部分的 switch 标签被可达的 goto case 或 goto default 语句引用。

如果以下至少一项为真，则 switch 语句的终点可达：

- switch 语句包含一个可达的 break 语句，该语句退出 switch 语句。
- switch 语句可达，switch 表达式是非常量值，且不存在 default 标签。
- switch 语句可达，switch 表达式是常量值且与任何 case 标签都不匹配，且不存在 default 标签。

## 13.9 迭代语句

### 13.9.1 通用

迭代语句重复执行嵌入的语句。

```
iteration-statement:
  while-statement
  do-statement
  for-statement
  foreach-statement
```

### 13.9.2 while 语句

while 语句有条件地执行嵌入的语句零次或多次。

```
while-statement:
  while ( boolean-expression ) embedded-statement
```

while 语句的执行方式如下：

- 计算 boolean-expression（§12.21）。
- 如果布尔表达式产生 true，则控制转移到嵌入的语句。当且仅当控制到达嵌入语句的终点（可能来自 continue 语句的执行）时，控制转移到 while 语句的开头。
- 如果布尔表达式产生 false，则控制转移到 while 语句的终点。

在 while 语句的嵌入语句内，可以使用 break 语句（§13.10.2）将控制转移到 while 语句的终点（从而结束嵌入语句的迭代），并且可以使用 continue 语句（§13.10.3）将控制转移到嵌入语句的终点（从而执行 while 语句的另一次迭代）。

如果 while 语句可达且布尔表达式不具有常量值 false，则 while 语句的嵌入语句可达。

如果以下至少一项为真，则 while 语句的终点可达：

- while 语句包含一个可达的 break 语句，该语句退出 while 语句。
- while 语句可达且布尔表达式不具有常量值 true。

### 13.9.3 do 语句

do 语句有条件地执行嵌入的语句一次或多次。

```
do-statement:
  do embedded-statement while ( boolean-expression ) ;
```

do 语句的执行方式如下：

- 控制转移到嵌入的语句。
- 当且仅当控制到达嵌入语句的终点（可能来自 continue 语句的执行）时，计算 boolean-expression（§12.21）。如果布尔表达式产生 true，则控制转移到 do 语句的开头。否则，控制转移到 do 语句的终点。

在 do 语句的嵌入语句内，可以使用 break 语句（§13.10.2）将控制转移到 do 语句的终点（从而结束嵌入语句的迭代），并且可以使用 continue 语句（§13.10.3）将控制转移到嵌入语句的终点（从而执行 do 语句的另一次迭代）。

如果 do 语句可达，则 do 语句的嵌入语句可达。

如果以下至少一项为真，则 do 语句的终点可达：


- for 语句包含一个可到达的 break 语句，该语句退出 for 语句。
- for 语句是可到达的，并且存在 for 条件，且该条件不具有常量值 true。

## 13.9.5 foreach 语句

foreach 语句枚举集合的元素，并对集合中的每个元素执行一个嵌入语句。

```
foreach-statement:
    foreach ( local-variable-type identifier in expression ) embedded-statement
```

foreach 语句的 local-variable-type 和 identifier 声明该语句的迭代变量。如果将 var 标识符作为 local-variable-type 给出，并且作用域中没有名为 var 的类型，则称该迭代变量为隐式类型迭代变量，其类型按如下所述取为 foreach 语句的元素类型。迭代变量对应于一个只读局部变量，其作用域覆盖嵌入语句。在执行 foreach 语句期间，迭代变量表示当前正在对其进行迭代的集合元素。如果嵌入语句试图修改迭代变量（通过赋值或者 ++ 和 -- 运算符）或者将迭代变量作为 ref 或 out 参数传递，则发生编译时错误。

为简洁起见，下文中的 IEnumerable、IEnumerator、IEnumerable<T> 和 IEnumerator<T> 指代命名空间 System.Collections 和 System.Collections.Generic 中的对应类型。

foreach 语句的编译时处理首先确定表达式的集合类型、枚举器类型和元素类型。该确定过程如下：

- 如果表达式的类型 X 是数组类型，则存在从 X 到 IEnumerable 接口的隐式引用转换（因为 System.Array 实现此接口）。集合类型为 IEnumerable 接口，枚举器类型为 IEnumerator 接口，元素类型为数组类型 X 的元素类型。
- 如果表达式的类型 X 是 dynamic，则存在从表达式到 IEnumerable 接口的隐式转换（§11.2.9）。集合类型为 IEnumerable 接口，枚举器类型为 IEnumerator 接口。如果将 var 标识符作为 local-variable-type 给出，则元素类型为 dynamic；否则为 object。
- 否则，确定类型 X 是否具有适当的 GetEnumerator 方法：
  - 在类型 X 上使用标识符 GetEnumerator 且不带类型实参执行成员查找。如果成员查找未产生匹配，或产生二义性，或产生的匹配不是方法组，则按下面所述检查可枚举接口。建议在成员查找产生的结果不是方法组或没有匹配时发出警告。
  - 使用得到的方法组和空参数列表执行重载决策。如果重载决策没有找到适用方法、产生二义性，或者只找到一个最佳方法但该方法为静态方法或不是公共方法，则按下面所述检查可枚举接口。建议在重载决策产生的结果不是无二义性的公共实例方法或没有适用方法时发出警告。
  - 如果 GetEnumerator 方法的返回类型 E 不是类、结构或接口类型，则产生错误，并且不再执行后续步骤。
  - 在 E 上使用标识符 Current 且不带类型实参执行成员查找。如果成员查找没有产生匹配、结果为错误，或者结果不是允许读取的公共实例属性，则产生错误，并且不再执行后续步骤。
- 在 E 上使用标识符 MoveNext 且不带类型实参执行成员查找。如果成员查找没有产生匹配、结果为错误，或者结果不是方法组，则产生错误，并且不再执行后续步骤。
- 使用空参数列表对该方法组执行重载决策。如果重载决策没有找到适用方法、产生二义性，或者只找到一个最佳方法但该方法为静态方法、不是公共方法，或者其返回类型不是 bool，则产生错误，并且不再执行后续步骤。
- **集合类型**为 X，**枚举器类型**为 E，**元素类型**为 Current 属性的类型。
- 否则，检查可枚举接口：
  - 如果在所有存在从 X 到 IEnumerable<T_i> 的隐式转换的类型 T_i 中，存在唯一类型 T，使得 T 不是 dynamic，并且对于所有其他 T_i，都存在从 IEnumerable<T> 到 IEnumerable<T_i> 的隐式转换，则**集合类型**为接口 IEnumerable<T>，**枚举器类型**为接口 IEnumerator<T>，**元素类型**为 T。
  - 否则，如果这样的类型 T 多于一个，则产生错误，并且不再执行后续步骤。
  - 否则，如果存在从 X 到 System.Collections.IEnumerable 接口的隐式转换，则**集合类型**为该接口，**枚举器类型**为接口 System.Collections.IEnumerator，**元素类型**为 object。
  - 否则，产生错误，并且不再执行后续步骤。

上述步骤如果成功，将明确产生集合类型 C、枚举器类型 E 和元素类型 T。形式如下的 foreach 语句

```
foreach (V v in x) embedded-statement
```

随后展开为：

```
{
    E e = ((C)(x)).GetEnumerator();
    try {
        while (e.MoveNext()) {
            V v = (T)e.Current;
            embedded-statement
        }
    }
    finally {
        ... // Dispose e
    }
}
```

变量 e 对表达式 x、嵌入语句或程序的任何其他源代码不可见也不可访问。变量 v 在嵌入语句中是只读的。如果不存在从 T（元素类型）到 V（foreach 语句中的 local-variable-type）的显式转换（§11.2.13），则产生错误，并且不再执行后续步骤。[注意：如果 x 的值为 null，则运行时将引发 System.NullReferenceException。注意结束]

允许实现以不同方式实现给定的 foreach 语句；例如，出于性能原因，只要其行为与上述展开一致即可。

v 放在 while 循环内部的位置很重要，因为它决定了嵌入语句中出现的任何匿名函数如何捕获（§12.16.6.2）它。

[示例：]

```csharp
int[] values = { 7, 9, 13 };
Action f = null;
foreach (var value in values)
{
    if (f == null) f = () => Console.WriteLine("First value: " + value);
    f();
}
```

如果展开形式中的 v 声明在 while 循环之外，那么它将在所有迭代之间共享，并且它在 for 循环之后的值将是最终值 13，这也是调用 f 时会打印的内容。相反，由于每次迭代都有自己的变量 v，第一次迭代中由 f 捕获的变量将继续保持值 7，这也正是会打印的内容。（请注意，早期版本的 C# 将 v 声明在 while 循环之外。）*示例结束*

finally 块的主体按照以下步骤构造：

- 如果存在从 E 到 `System.IDisposable` 接口的隐式转换，则
  - 如果 E 是不可为 null 的值类型，则 finally 子句展开为以下语义等价形式：
    ```csharp
    finally {
        ((System.IDisposable)e).Dispose();
    }
    ```
  - 否则，finally 子句展开为以下语义等价形式：
    ```csharp
    finally {
        System.IDisposable d = e as System.IDisposable;
        if (d != null) d.Dispose();
    }
    ```
    但有一种情况例外：如果 E 是值类型，或者实例化为值类型的类型参数，则将 e 转换为 `System.IDisposable` 不得导致装箱发生。
- 否则，如果 E 是密封类型，则 finally 子句展开为空块：
  ```csharp
  finally {
  }
  ```
- 否则，finally 子句展开为：
  ```csharp
  finally {
      System.IDisposable d = e as System.IDisposable;
      if (d != null) d.Dispose();
  }
  ```

局部变量 d 对任何用户代码不可见也不可访问。特别地，它不会与作用域包含该 finally 块的任何其他变量冲突。

foreach 遍历数组元素的顺序如下：对于一维数组，元素按索引递增顺序遍历，从索引 0 开始，到索引 Length – 1 结束。对于多维数组，遍历元素时，最右侧维度的索引先递增，然后向左下一维度递增，依此类推。

[示例：以下示例按元素顺序打印二维数组中的每个值：

```csharp
using System;
class Test
{
    static void Main() {
        double[,] values = {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };
        foreach (double elementValue in values)
            Console.Write("{0} ", elementValue);
        Console.WriteLine();
    } }
```

生成的输出如下：

```
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

示例结束]

[示例：在以下示例中

```
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
```

推断出 n 的类型为 int，即 numbers 的元素类型。

示例结束]

## 13.10 跳转语句

### 13.10.1 概述

跳转语句无条件地转移控制。

```
jump-statement:
  break-statement
  continue-statement
  goto-statement
  return-statement
  throw-statement
```

跳转语句将控制转移到的位置称为该跳转语句的目标。

当跳转语句出现在某个块内，而该跳转语句的目标在该块之外时，称该跳转语句退出该块。虽然跳转语句可以将控制转移到块外，但它永远不能将控制转移到块内。

跳转语句的执行会因中间存在 try 语句而变得复杂。如果不存在此类 try 语句，则跳转语句无条件地将控制从该跳转语句转移到其目标。如果存在此类中间 try 语句，则执行会更复杂。如果跳转语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。

[示例：在以下代码中

```
using System;
class Test
{
    static void Main() {
        while (true) {
            try {
                try {
                    Console.WriteLine("Before break");
                    break;
                }
                finally {
                    Console.WriteLine("Innermost finally block");
                }
            }
            finally {
                Console.WriteLine("Outermost finally block");
            }
        }
        Console.WriteLine("After break");
    }
}
```

与两个 try 语句关联的 finally 块会在控制转移到跳转语句的目标之前执行。

生成的输出如下：

```
Before break
Innermost finally block
Outermost finally block
After break
```

示例结束]

### 13.10.2 break 语句

break 语句退出最近封闭的 switch、while、do、for 或 foreach 语句。

```
break-statement:
    break ;
```

break 语句的目标是最近封闭的 switch、while、do、for 或 foreach 语句的结束点。如果 break 语句未被 switch、while、do、for 或 foreach 语句封闭，则会发生编译时错误。

当多个 switch、while、do、for 或 foreach 语句相互嵌套时，break 语句仅应用于最内层语句。若要跨多个嵌套层级转移控制，应使用 goto 语句（§13.10.4）。

break 语句不能退出 finally 块（§13.11）。当 break 语句出现在 finally 块内时，break 语句的目标应位于同一个 finally 块内；否则会发生编译时错误。

break 语句的执行方式如下：

- 如果 break 语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。
- 控制转移到 break 语句的目标。

由于 break 语句无条件地将控制转移到其他位置，因此 break 语句的结束点永远不可到达。

### 13.10.3 continue 语句

continue 语句开始最近封闭的 while、do、for 或 foreach 语句的新迭代。

```
continue-statement:
    continue ;
```

continue 语句的目标是最近封闭的 while、do、for 或 foreach 语句的嵌入语句的结束点。如果 continue 语句未被 while、do、for 或 foreach 语句封闭，则会发生编译时错误。

当多个 while、do、for 或 foreach 语句相互嵌套时，continue 语句仅应用于最内层语句。若要跨多个嵌套层级转移控制，应使用 goto 语句（§13.10.4）。

continue 语句不能退出 finally 块（§13.11）。当 continue 语句出现在 finally 块内时，continue 语句的目标应位于同一个 finally 块内；否则会发生编译时错误。

continue 语句的执行方式如下：

- 如果 continue 语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。
- 控制转移到 continue 语句的目标。

由于 continue 语句无条件地将控制转移到其他位置，因此 continue 语句的结束点永远不可到达。

### 13.10.4 goto 语句

goto 语句将控制转移到由标签标记的语句。

```
goto-statement:
    goto identifier ;
    goto case constant-expression ;
    goto default ;
```

goto 标识符语句的目标是具有给定标签的带标签语句。如果当前函数成员中不存在具有给定名称的标签，或者 goto 语句不在该标签的作用域内，则会发生编译时错误。[注意：此规则允许使用 goto 语句将控制转移到嵌套作用域之外，但不能转入嵌套作用域。在以下示例中

```
using System;
class Test
{
    static void Main(string[] args) {
        string[,] table = {
            {"Red", "Blue", "Green"},
            {"Monday", "Wednesday", "Friday"}
        };
        foreach (string str in args) {
            int row, colm;
            for (row = 0; row <= 1; ++row)
                for (colm = 0; colm <= 2; ++colm)
                    if (str == table[row,colm])
                        goto done;
            Console.WriteLine("{0} not found", str);
            continue;
        done:
            Console.WriteLine("Found {0} at [{1}][{2}]", str, row, colm);
        }
    }
}
```

使用 goto 语句将控制转移到嵌套作用域之外。注意结束]

goto case 语句的目标是直接封闭的 switch 语句（§13.8.3）中包含具有给定常量值的 case 标签的语句列表。如果 goto case 语句未被 switch 语句封闭，如果常量表达式不能隐式转换（§11.2）为最近封闭的 switch 语句的控制类型，或者如果最近封闭的 switch 语句不包含具有给定常量值的 case 标签，则会发生编译时错误。

goto default 语句的目标是直接封闭的 switch 语句（§13.8.3）中包含 default 标签的语句列表。如果 goto default 语句未被 switch 语句封闭，或者如果最近封闭的 switch 语句不包含 default 标签，则会发生编译时错误。

goto 语句不能退出 finally 块（§13.11）。当 goto 语句出现在 finally 块内时，goto 语句的目标应位于同一个 finally 块内，否则会发生编译时错误。

goto 语句的执行方式如下：

- 如果 goto 语句退出一个或多个带有关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。
- 控制转移到 goto 语句的目标。

由于 goto 语句无条件地将控制转移到其他位置，因此 goto 语句的结束点永远不可到达。

### 13.10.5 return 语句

return 语句将控制返回给出现该 return 语句的函数成员的当前调用方。

```
    return-statement:
        return expression_opt ;
```

如果函数成员是具有非 void 结果类型（§15.6.11）的方法、属性或索引器的 get 访问器，或者用户定义运算符，则称该函数成员**计算值**。不计算值的函数成员是有效返回类型为 void 的方法、属性和索引器的 set 访问器、事件的 add 和 remove 访问器、实例构造函数、静态构造函数和终结器。

在函数成员内，仅当该函数成员不计算值时，才能使用不带表达式的 return 语句。在函数成员内，仅当该函数成员计算值时，才能使用带表达式的 return 语句。如果 return 语句包含表达式，则必须存在从该表达式的类型到包含该 return 语句的函数成员的有效返回类型的隐式转换（§11.2）。

return 语句也可用于匿名函数表达式（§12.16）的主体中，并参与确定这些函数存在哪些转换（§11.7.1）。

return 语句出现在 finally 块（§13.11）中属于编译时错误。

return 语句的执行方式如下：

- 如果 return 语句指定了表达式，则计算该表达式，并通过隐式转换将其值转换为包含该语句的函数成员的有效返回类型。转换结果成为该函数生成的结果值。
- 如果 return 语句被一个或多个带有关联 finally 块的 try 或 catch 块封闭，则控制最初转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的结束点（如果到达），控制会转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有封闭 try 语句的 finally 块都已执行。
- 如果包含该语句的函数不是异步函数，则控制连同结果值（如果有）一起返回给包含该函数的调用方。
- 如果包含该语句的函数是异步函数，则控制返回给当前调用方，并且结果值（如果有）按（§15.15.2）中所述记录在返回任务中。

由于 return 语句无条件地将控制转移到其他位置，因此 return 语句的结束点永远不可到达。




### 13.10.6 throw 语句

throw 语句抛出异常。

```
throw-statement:
    throw expression_opt ;
```

带表达式的 throw 语句会抛出通过求值表达式产生的异常。表达式应可隐式转换为 `System.Exception`，并且在抛出之前，求值表达式的结果会被转换为 `System.Exception`。如果转换结果为 `null`，则会改为抛出 `System.NullReferenceException`。

不带表达式的 throw 语句只能在 `catch` 块中使用，在这种情况下，该语句会重新抛出当前正由该 `catch` 块处理的异常。

由于 throw 语句无条件地将控制权转移到别处，因此 throw 语句的终点永远不可达。

当抛出异常时，控制权会转移到能够处理该异常的外层 `try` 语句中的第一个 `catch` 子句。异常从被抛出点到控制权转移到合适的异常处理程序为止所发生的过程称为 *异常传播*。异常的传播包括反复评估以下步骤，直到找到匹配该异常的 `catch` 子句为止。在此描述中，*抛出点* 最初是异常被抛出的位置。

- 在当前函数成员中，会检查每个包含抛出点的 `try` 语句。对于每个语句 S，从最内层的 `try` 语句开始，到最外层的 `try` 语句结束，按顺序评估以下步骤：
  - 如果 S 的 `try` 块包含抛出点并且 S 具有一个或多个 `catch` 子句，则按出现顺序检查 `catch` 子句以定位异常的合适处理程序。第一个指定异常类型 T（或在运行时表示异常类型 T 的类型参数）的 `catch` 子句，只要运行时类型 E 派生自 T，就被视为匹配。一般 `catch`（§13.11）子句被视为与任何异常类型匹配。如果找到匹配的 `catch` 子句，则通过将控制权转移到该 `catch` 子句的块来完成异常传播。
  - 否则，如果 S 的 `try` 块或 `catch` 块包含抛出点并且 S 具有 `finally` 块，则控制权会转移到 `finally` 块。如果 `finally` 块抛出另一个异常，则当前异常的处理将被终止。否则，当控制权到达 `finally` 块的终点时，当前异常的处理会继续。
- 如果在当前函数调用中未找到异常处理程序，则函数调用将被终止，并发生以下情况之一：
  - 如果当前函数是非 async，则以上步骤会针对调用该函数的调用者重复执行，抛出点对应于调用该函数成员的语句。
  - 如果当前函数是 async 且返回 task，则异常会被记录在返回的 task 中，该 task 会被置于故障或取消状态，如 §15.15.2 中所述。
  - 如果当前函数是 async 且返回 void，则当前线程的同步上下文会按 §15.15.3 中所述进行通知。
- 如果异常处理终止了当前线程中的所有函数成员调用，表明该线程没有处理该异常的处理程序，则该线程本身将被终止。此类终止的影响由实现定义。

## 13.11 try 语句

try 语句提供了一种在块执行期间捕获异常的机制。此外，try 语句还提供了指定在控制权离开 try 语句时始终执行的代码块的能力。

```
try-statement:
    try block catch-clauses
    try block catch-clauses_opt finally-clause

catch-clauses:
    specific-catch-clauses
    specific-catch-clauses_opt general-catch-clause

specific-catch-clauses:
    specific-catch-clause
    specific-catch-clauses specific-catch-clause

specific-catch-clause:
    catch ( type identifier_opt ) block

general-catch-clause:
    catch block

finally-clause:
    finally block
```

try 语句有三种可能的形式：

- 后跟一个或多个 catch 块的 try 块。
- 后跟 finally 块的 try 块。
- 后跟一个或多个 catch 块再跟 finally 块的 try 块。

当 catch 子句指定一个类型时，该类型应为 System.Exception 或派生自 System.Exception 的类型。当 catch 子句指定类型参数时，它应为有效基类为或派生自 System.Exception 的类型参数类型。

当 catch 子句同时指定类类型和标识符时，会声明给定名称和类型的异常变量。异常变量对应于作用域扩展到 catch 块上的局部变量。在 catch 块执行期间，异常变量表示当前正在处理的异常。就确定性赋值检查而言，异常变量在其整个作用域内被视为已确定赋值。

除非 catch 子句包含异常变量名，否则在 catch 块中无法访问异常对象。

不指定异常类型也不指定异常变量名的 catch 子句称为一般 catch 子句。try 语句只能有一个一般 catch 子句，如果存在，则它必须是最后一个 catch 子句。

> [注：某些编程语言可能支持无法表示为派生自 System.Exception 的对象的异常，尽管此类异常永远不会由 C# 代码生成。一般 catch 子句可能用于捕获此类异常。因此，一般 catch 子句在语义上不同于指定类型 System.Exception 的子句，因为前者还可能捕获来自其他语言的异常。结束注]

为了定位异常的处理程序，catch 子句会按词法顺序检查。如果 catch 子句指定的类型与同一 try 的 earlier catch 子句中指定的类型相同或派生自该类型，则会发生编译时错误。[注：没有此限制，就可能编写不可达的 catch 子句。结束注]

在 catch 块内，可以使用不带表达式的 throw 语句（§13.10.6）重新抛出该 catch 块捕获的异常。对异常变量的赋值不会改变被重新抛出的异常。

[示例：在以下代码

```
using System;
class Test
{
    static void F() {
        try {
            G();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw; // re-throw
        }
    }
    static void G() {
        throw new Exception("G");
    }
    static void Main() {
        try {
            F();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in Main: " + e.Message);
        }
    }
}
```

方法 F 捕获异常，将一些诊断信息写入控制台，修改异常变量，然后重新抛出异常。被重新抛出的异常是原始异常，因此产生的输出为：

```
Exception in F: G
Exception in Main: G
```

如果第一个 catch 块抛出 e 而不是重新抛出当前异常，则产生的输出将如下所示：

```
Exception in F: G
Exception in Main: F
```

结束示例]

对于 break、continue 或 goto 语句将控制权转移出 finally 块而言是编译时错误。当 break、continue 或 goto 语句出现在 finally 块中时，该语句的目标必须在同一 finally 块内，否则会发生编译时错误。

在 finally 块中出现 return 语句是编译时错误。

try 语句的执行如下：

- 控制权转移到 try 块。
- 当且仅当控制权到达 try 块的终点时：
  - 如果 try 语句具有 finally 块，则执行 finally 块。
  - 控制权转移到 try 语句的终点。
- 如果在 try 块执行期间异常传播到 try 语句：
  - 如果有的话，按出现顺序检查 catch 子句以定位异常的合适处理程序。第一个指定异常类型或异常的基类型的 catch 子句

类型被视为匹配。通用 catch 子句被视为与任何异常类型匹配。如果找到匹配的 catch 子句：

-   如果匹配的 catch 子句声明了异常变量，则异常对象将被赋给该异常变量。
-   控制权转移到匹配的 catch 块。
-   当且仅当控制流到达 catch 块的结束点时：
  -   如果 try 语句有 finally 块，则执行 finally 块。
  -   控制权转移到 try 语句的结束点。
-   如果在 catch 块执行期间异常被传播到 try 语句：
  -   如果 try 语句有 finally 块，则执行 finally 块。
  -   异常被传播到下一个外层 try 语句。
-   如果 try 语句没有 catch 子句或没有 catch 子句与异常匹配：
  -   如果 try 语句有 finally 块，则执行 finally 块。
  -   异常被传播到下一个外层 try 语句。

finally 块的语句在控制流离开 try 语句时始终执行。这无论控制转移是由于正常执行、执行 break、continue、goto 或 return 语句的结果，还是由于将异常从 try 语句传播出来而发生的结果都是如此。

如果在 finally 块执行期间抛出异常，并且未在同一 finally 块内捕获，则该异常将被传播到下一个外层 try 语句。如果另一个异常正在被传播过程中，则该异常会丢失。传播异常的过程在 throw 语句的描述（§13.10.6）中进一步讨论。

如果 try 语句可达，则 try 语句的 try 块可达。如果 try 语句可达，则 try 语句的 catch 块可达。如果 try 语句可达，则 try 语句的 finally 块可达。try 语句的结束点可达当且仅当以下两个条件都为真时：

-   try 块的结束点可达或至少一个 catch 块的结束点可达。
-   如果存在 finally 块，则 finally 块的结束点可达。

## 13.12 checked 和 unchecked 语句

checked 和 unchecked 语句用于控制积分类型算术运算和转换的溢出检查上下文。

```
checked-statement:
    checked block

unchecked-statement:
    unchecked block
```

checked 语句导致块中的所有表达式在 checked 上下文中求值，而 unchecked 语句导致块中的所有表达式在 unchecked 上下文中求值。checked 和 unchecked 语句与 checked 和 unchecked 运算符（§12.7.14）精确等效，只是它们对块而不是表达式进行操作。

## 13.13 lock 语句

lock 语句为给定对象获取互斥锁，执行语句，然后释放锁。

```
lock-statement:
    lock ( expression ) embedded-statement
```

lock 语句的表达式必须表示已知为引用的类型的值。lock 语句的表达式永远不会执行隐式装箱转换（§11.2.8），因此表达式表示值类型的值是编译时错误。

形式为

```
lock ( x ) ...
```

的 lock 语句，其中 x 是引用类型的表达式，精确等效于：

```
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, ref __lockWasTaken);  ...
}
finally {
    if (__lockWasTaken) System.Threading.Monitor.Exit(x);
}
```

只是 x 只被求值一次。

在持有互斥锁期间，同一执行线程中执行的代码也可以获取和释放锁。然而，其他线程中执行的代码在锁被释放之前无法获取锁。

## 13.14 using 语句

using 语句获取一个或多个资源，执行语句，然后释放资源。

```
using-statement:
    using ( resource-acquisition ) embedded-statement
resource-acquisition:
    local-variable-declaration
    expression
```

资源是实现 System.IDisposable 接口的类或结构体，该接口包含一个名为 Dispose 的无参数方法。使用资源时，代码可以调用 dispose 来表示资源不再需要。

形式为

```
using (ResourceType resource = expression) statement
```

的 using 语句对应于三种可能的展开之一。当 ResourceType 是不可为空的值类型或具有值类型约束的类型参数（§15.2.5）时，展开在语义上等效于

```
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        ((IDisposable)resource).Dispose();
    }
}
```

只是 resource 到 System.IDisposable 的强制转换不得导致装箱发生。

否则，当 ResourceType 为 dynamic 时，展开为

```
{
    ResourceType resource = expression;
    IDisposable d = resource;
    try {
        statement;
    }
    finally {
        if (d != null) d.Dispose();
    }
}
```

否则，展开为

```
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        IDisposable d = (IDisposable)resource;
        if (d != null) d.Dispose();
    }
}
```

在任何展开中，资源变量在嵌入语句中为只读，且 d 变量在嵌入语句中不可访问且对嵌入语句不可见。

实现可以以不同的方式实现给定的 using 语句，例如出于性能原因，只要行为与上述展开一致即可。

形式为：

```
using (expression) statement
```

的 using 语句具有相同的三种可能的展开。在这种情况下，ResourceType 隐式为表达式的编译时类型（如果有）。否则，接口 IDisposable 本身用作 ResourceType。资源变量在嵌入语句中不可访问且对嵌入语句不可见。

当 *resource-acquisition* 采用 *local-variable-declaration* 的形式时，可以获取给定类型的多个资源。形式为

```
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) statement
```

的 using 语句精确等效于一系列嵌套的 using 语句：

```
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```

[示例：下面的示例创建一个名为 log.txt 的文件并向文件中写入两行文本。然后示例打开同一文件进行读取并将包含的行复制到控制台。

```
using System;
using System.IO;

class Test
{
    static void Main() {
        using (TextWriter w = File.CreateText("log.txt")) {
            w.WriteLine("This is line one");
            w.WriteLine("This is line two");
        }

        using (TextReader r = File.OpenText("log.txt")) {
            string s;
            while ((s = r.ReadLine()) != null) {
                Console.WriteLine(s);
            }
        }
    }
}
```

由于 TextWriter 和 TextReader 类实现了 IDisposable 接口，示例可以使用 using 语句确保在写入或读取操作后底层文件被正确关闭。*示例结束*]

## 13.15 yield 语句

yield 语句用于在迭代器块（§13.3）中向迭代器的枚举器对象（§15.14.5）或可枚举对象（§15.14.6）产生值，或表示迭代结束。

```
yield-statement:
    yield return expression ;
    yield break ;
```

yield 是上下文关键字（§7.4.4），只有在紧跟 return 或 break 关键字时才具有特殊含义。

yield 语句可以出现的位置有若干限制，如下所述。

-   如果 yield 语句（任一形式）出现在 *method-body*、*operator-body* 或 *accessor-body* 之外，则为编译时错误。
-   如果 yield 语句（任一形式）出现在匿名函数内部，则为编译时错误。
-   如果 yield 语句（任一形式）出现在 try 语句的 finally 子句中，则为编译时错误。
-   如果 yield return 语句出现在包含任何 catch 子句的 try 语句中的任何位置，则为编译时错误。

[示例：下面的示例显示了 yield 语句的一些有效和无效用法。

```
delegate IEnumerable<int> D();
```



## 14. 命名空间

### 14.1 总则

C# 程序使用命名空间进行组织。命名空间既用作程序的“内部”组织系统，也用作“外部”组织系统——一种呈现程序中暴露给其他程序的元素的方式。

使用指令 (§14.5) 用于方便命名空间的使用。

### 14.2 编译单元

编译单元定义源文件的整体结构。编译单元由零个或多个 extern-alias-directives 后跟零个或多个 using-directives 后跟零个或多个 global-attributes 后跟零个或多个 namespace-member-declarations 组成。

```text
compilation-unit:
    extern-alias-directives_opt   using-directives_opt   global-attributes_opt
        namespace-member-declarations_opt
```

C# 程序由一个或多个编译单元组成，每个编译单元包含在单独的源文件中。当 C# 程序被编译时，所有编译单元都会一起处理。因此，编译单元可以相互依赖，甚至可能以循环的方式依赖。

编译单元的 extern-alias-directives 影响该编译单元的 using-directives、global-attributes 和 namespace-member-declarations，但对其他编译单元没有影响。

编译单元的 using-directives 影响该编译单元的 global-attributes 和 namespace-member-declarations，但对其他编译单元没有影响。

编译单元的 global-attributes (§22.3) 允许为目标程序集和模块指定属性。程序集和模块充当类型的物理容器。程序集可能由几个物理上分离的模块组成。

程序的每个编译单元的 namespace-member-declarations 都向称为全局命名空间的单个声明空间贡献成员。[示例：

```text
File A.cs:
    class A {}
File B.cs:
    class B {}
```

这两个编译单元贡献到单个全局命名空间，在此情况下声明了两个类，其完全限定名称分别为 A 和 B。由于这两个编译单元贡献到同一个声明空间，如果每个都包含同名成员的声明则会出错。结束示例]

### 14.3 命名空间声明

namespace-declaration 由关键字 namespace、后跟命名空间名称和主体，可选后跟分号组成。

```text
namespace-declaration:
    namespace qualified-identifier namespace-body ;_opt
```

### 14.5.2 使用别名指令

using-alias-directive 引入一个标识符，该标识符在紧邻的编译单元或命名空间主体内充当命名空间或类型的别名。

```text
using-alias-directive:
    using identifier = namespace-or-type-name ;
```

在包含 using-alias-directive 的编译单元或命名空间主体中的全局属性和成员声明中，由 using-alias-directive 引入的标识符可用于引用给定的命名空间或类型。[示例：

```csharp
namespace N1.N2
{
    class A {}
}
namespace N3
{
    using A = N1.N2.A;
    class B: A {}
}
```

以上，在 N3 命名空间中的成员声明中，A 是 N1.N2.A 的别名，因此类 N3.B 派生自类 N1.N2.A。可以通过为 N1.N2 创建别名 R 然后引用 R.A 来获得相同的效果：

```csharp
namespace N3
{
    using R = N1.N2;
    class B: R.A {}
}
```

在包含 extern-alias-directive 的编译单元或命名空间主体中的 using 指令、全局属性和成员声明中，由 extern-alias-directive 引入的标识符可用于引用关联的命名空间。[示例：例如：

```csharp
namespace N1
{
    extern alias N2;
    class B: N2::A {}
}
```

以上，在 N1 命名空间中的成员声明中，N2 是程序源代码外部定义的某个命名空间的别名。类 N1.B 派生自类 N2.A。可以通过为 N2.A 创建别名 A 然后引用 A 来获得相同的效果：

```csharp
namespace N1
{
    extern alias N2;
    using A = N2::A;
    class B: A {}
}
```

extern-alias-directive 或 using-alias-directive 使别名在特定编译单元或命名空间主体内可用，但它不会向底层声明空间贡献任何新成员。换句话说，别名指令不是传递的，而是仅影响它出现的编译单元或命名空间主体。[示例：在以下代码中

```csharp
namespace N3
{
    extern alias R1;
    using R2 = N1.N2;
}
namespace N3
{
    class B: R1::A, R2.I {}       // Error, R1 and R2 unknown
}
```

引入 R1 和 R2 的别名指令的范围仅扩展到它们所包含的命名空间主体中的成员声明，因此 R1 和 R2 在第二个命名空间声明中未知。然而，将别名指令放在包含的编译单元中会使别名在两个命名空间声明中都可用：

```csharp
extern alias R1;
using R2 = N1.N2;
namespace N3
{
    class B: R1::A, R2.I {}
}
namespace N3
{
    class C: R1::A, R2.I {}
}
```

*结束示例]*

每个 *外部别名指令* 或 *使用别名指令* 在 *编译单元* 或 *命名空间主体* 中向紧邻的 *编译单元* 或 *命名空间主体* 的 *别名声明空间* (§8.3) 贡献一个名称。别名指令的 *标识符* 在对应的别名声明空间内必须是唯一的。别名标识符不必在全局声明空间或对应命名空间的声明空间内唯一。[示例：

```csharp
extern alias A;
extern alias B;
using A = N1.N2;       // Error: alias A already exists
class B {}             // Ok
```

使用别名名为 A 导致错误，因为在同一编译单元中已存在名为 A 的别名。名为 B 的类不会与名为 B 的 extern 别名冲突，因为这些名称被添加到不同的声明空间。前者被添加到全局声明空间，后者被添加到此编译单元的别名声明空间。

当别名名称与命名空间的成员名称相同时，使用两者都必须适当限定：

```csharp
namespace N1.N2
{
    class B {}
}
namespace N3
{
    class A {}
    class B : A {}
}
namespace N3
{
    using A = N1.N2;
    using B = N1.N2.B;

    class W : B {}    // Error: B is ambiguous
    class X : A.B {}  // Error: A is ambiguous
    class Y : A::B {} // Ok: uses N1.N2.B
    class Z : N3.B {} // Ok: uses N3.B
}
```

在 N3 的第二个命名空间主体中，未限定地使用 B 会导致错误，因为 N3 包含名为 B 的成员，而命名空间主体也声明了名为 B 的别名；A 也是如此。类 N3.B 可以作为 N3.B 或 global::N3.B 引用。别名 A 可以在限定别名成员 (§14.8) 中使用，例如 A::B。别名 B 基本上是无用的。它不能在限定别名成员中使用，因为只有命名空间别名才能在限定别名成员中使用，而 B 别名的是一个类型。结束示例

就像常规成员一样，由别名指令引入的名称会被嵌套作用域中同名成员隐藏。[示例：在以下代码中

```csharp
using R = N1.N2;
namespace N3
{
    class R {}
    class B: R.A {}    // Error, R has no member A
}
```

在 B 的声明中对 R.A 的引用会导致编译时错误，因为 R 指的是 N3.R，而不是 N1.N2。结束示例

extern-alias-directives 的书写顺序没有意义。同样，using-alias-directives 的书写顺序也没有意义，但在同一编译单元或命名空间主体中，所有 using-alias-directives 必须跟在所有 extern-alias-directives 之后。由 using-alias-directive 引用的 namespace-or-type-name 的解析不受 using-alias-directive 本身或紧邻包含的编译单元或命名空间主体中的其他 using-directives 影响，但可能受紧邻包含的编译单元或命名空间主体中的 extern-alias-directives 影响。换句话说，using-alias-directive 的 namespace-or-type-name 是在假设紧邻包含的编译单元或命名空间主体没有 using-directives 但具有正确的 extern-alias-directives 集合的情况下解析的。[示例：在以下代码中

```csharp
namespace N1.N2 {}
namespace N3
{
    extern alias E;
    using R1 = E::N;    // OK
    using R2 = N1;      // OK
    using R3 = N1.N2;   // OK
    using R4 = R2.N2;   // Error, R2 unknown
}
```

最后一个 using-alias-directive 导致编译时错误，因为它不受之前的 using-alias-directive 影响。第一个 using-alias-directive 不会导致错误，因为 extern 别名 E 的作用域包括 using-alias-directive。结束示例

using-alias-directive 可以为任何命名空间或类型创建别名，包括它出现的命名空间以及该命名空间内嵌套的任何命名空间或类型。

通过别名访问命名空间或类型产生的结果与通过其声明名称访问该命名空间或类型完全相同。[示例：给定

```csharp
namespace N1.N2
{
    class A {}
}
```



```
namespace N3
{
    using R1 = N1;
    using R2 = N1.N2;

    class B
    {
        N1.N2.A a;       // refers to N1.N2.A
        R1.N2.A b;       // refers to N1.N2.A
        R2.A c;          // refers to N1.N2.A
    }
}
```

名称 N1.N2.A、R1.N2.A 和 R2.A 是等价的，并且都引用完全限定名为 N1.N2.A 的类声明。end example]

尽管 partial 类型 (§15.2.7) 的每个部分都在同一个命名空间内声明，但这些部分通常写在不同的命名空间声明中。因此，每个部分可以存在不同的 extern 别名指令和 using 指令。在解释一个部分内的简单名称 (§12.7.3) 时，仅考虑包含该部分的命名空间主体和编译单元的 extern 别名指令和 using 指令。这可能导致同一个标识符在不同的部分中具有不同的含义。[示例：

```
namespace N
{
    using List = System.Collections.ArrayList;

    partial class A
    {
        List x;          // x has type System.Collections.ArrayList
    }
}

namespace N
{
    using List = widgets.LinkedList;

    partial class A
    {
        List y;          // y has type widgets.LinkedList
    }
}
```

end example]

使用别名可以命名封闭构造的类型，但不能在不提供类型参数的情况下命名未绑定的泛型类型声明。[示例：

```
namespace N1
{
    class A<T>
    {
        class B {}
    }
}
namespace N2
{
    using W = N1.A;          // Error, cannot name unbound generic type
    using X = N1.A.B;        // Error, cannot name unbound generic type
    using Y = N1.A<int>;     // Ok, can name closed constructed type
    using Z<T> = N1.A<T>;    // Error, using alias cannot have type parameters
}
```

end example]

```
type-declaration:
  class-declaration
  struct-declaration
  interface-declaration
  enum-declaration
  delegate-declaration
```

类型声明可以作为编译单元中的顶层声明出现，也可以作为命名空间、类或结构中的成员声明出现。

当类型 T 的类型声明作为编译单元中的顶层声明出现时，该类型声明的完全限定名 (§8.8.2) 与该声明的非限定名 (§8.8.2) 相同。当类型 T 的类型声明出现在命名空间、类或结构声明内时，该类型声明的完全限定名 (§8.8.3) 为 S.N，其中 S 是包含的命名空间、类或结构声明的完全限定名，N 是该声明的非限定名。

在类或结构内部声明的类型称为嵌套类型 (§15.3.9)。

类型声明允许的访问修饰符以及默认访问级别取决于声明发生的上下文 (§8.5.2)：

- 在编译单元或命名空间中声明的类型可以具有 public 或 internal 访问级别。默认值为 internal 访问。
- 在类中声明的类型可以具有 public、protected internal、protected、internal 或 private 访问级别。默认值为 private 访问。
- 在结构中声明的类型可以具有 public、internal 或 private 访问级别。默认值为 private 访问。

## 14.8 限定别名成员

### 14.8.1 通用

命名空间别名限定符 :: 使得可以保证类型名称查找不受新类型和成员引入的影响。命名空间别名限定符始终出现在两个标识符之间，分别称为左手标识符和右手标识符。与常规的 . 限定符不同，:: 限定符的左手标识符仅作为 extern 或 using 别名进行查找。

限定别名成员提供了对全局命名空间以及可能被其他实体隐藏的 extern 或 using 别名的显式访问。

```
qualified-alias-member:
  identifier :: identifier type-argument-list_opt
```

限定别名成员可以用作命名空间或类型名 (§8.8)，或用作成员访问 (§12.7.5) 中的左操作数。

限定别名成员由两个标识符组成，分别称为左手标识符和右手标识符，由 :: 标记分隔，并可选择跟随类型参数列表。当左手标识符为 global 时，则在全局命名空间中搜索右手标识符。对于任何其他左手标识符，该标识符将作为 extern 或 using 别名进行查找 (§14.4 和 §14.5.2)。如果不存在此类别名或别名引用类型，则会发生编译时错误。如果别名引用命名空间，则在该命名空间中搜索右手标识符。

限定别名成员有两种形式之一：

- N :: I<A1, ..., Ak>，其中 N 和 I 表示标识符，<A1, ..., Ak> 是类型参数列表。（K 始终至少为 1。）
- N :: I，其中 N 和 I 表示标识符。（在这种情况下，K 被视为零。）

使用此记法，限定别名成员的含义确定如下：

- 如果 N 是标识符 `global`，则在全局命名空间中搜索 I：
  - 如果全局命名空间包含名为 I 的命名空间且 K 为零，则 *qualified-alias-member* 引用该命名空间。
  - 否则，如果全局命名空间包含名为 I 的非泛型类型且 K 为零，则 *qualified-alias-member* 引用该类型。
  - 否则，如果全局命名空间包含名为 I 且具有 K 个类型参数的类型，则 *qualified-alias-member* 引用使用给定类型参数构造的该类型。
  - 否则，*qualified-alias-member* 未定义并发生编译时错误。
- 否则，从直接包含 *qualified-alias-member* 的命名空间声明 (§14.3)（如果有）开始，继续每个封闭的命名空间声明（如果有），直至包含 *qualified-alias-member* 的编译单元，以下步骤将被评估直到定位到一个实体：
  - 如果命名空间声明或编译单元包含将 N 与类型关联的 *using-alias-directive*，则 *qualified-alias-member* 未定义并发生编译时错误。
  - 否则，如果命名空间声明或编译单元包含将 N 与命名空间关联的 *extern-alias-directive* 或 *using-alias-directive*，则：
    - 如果与 N 关联的命名空间包含名为 I 的命名空间且 K 为零，则 *qualified-alias-member* 引用该命名空间。
    - 否则，如果与 N 关联的命名空间包含名为 I 的非泛型类型且 K 为零，则 *qualified-alias-member* 引用该类型。
    - 否则，如果与 N 关联的命名空间包含名为 I 且具有 K 个类型参数的类型，则 *qualified-alias-member* 引用使用给定类型参数构造的该类型。
    - 否则，*qualified-alias-member* 未定义并发生编译时错误。
- 否则，*qualified-alias-member* 未定义并发生编译时错误。

[示例：在代码中：

```csharp
using S = System.Net.Sockets;
class A {
    public static int x;
}
class C {
    public void F(int A, object S) {
        // Use global::A.x instead of A.x
        global::A.x += A;

        // Use S::Socket instead of S.Socket
        S::Socket s = S as S::Socket;
    }
}
```

类 A 使用 global::A 引用，类型 System.Net.Sockets.Socket 使用 S::Socket 引用。如果改用 A.x 和 S.Socket，则会因 A 和 S 解析为参数而导致编译时错误。end example]

[注意：标识符 `global` 只有在用作 *qualified-alias-name* 的左手标识符时才具有特殊含义。它不是关键字，也不是别名本身；它是一个上下文关键字 (§7.4.4)。在代码中：

```csharp
class A { }
class C {
    global::A x;   // Error: global is not defined
    global::A y;   // Valid: References A in the global namespace
}
```



使用 global.A 会导致编译时错误，因为作用域中没有名为 global 的实体。如果作用域中存在某个名为 global 的实体，那么 global.A 中的 global 就会解析到该实体。

将 global 用作限定别名成员的左侧标识符时，始终会在全局命名空间中查找，即使存在名为 global 的使用别名。在以下代码中：

```
using global = MyGlobalTypes;
class A { }
class C {
    global.A x; // Valid: References MyGlobalTypes.A
    global::A y; // Valid: References A in the global namespace
}
```

global.A 解析为 MyGlobalTypes.A，而 global::A 解析为全局命名空间中的类 A。
注释结束

## 14.8.2 别名的唯一性

每个编译单元和命名空间体都有各自独立的外部别名和使用别名声明空间。因此，虽然外部别名或使用别名的名称在直接包含它的编译单元或命名空间体中所声明的外部别名和使用别名集合内必须唯一，但允许别名与类型或命名空间同名，只要它仅与 :: 限定符一起使用。

[示例：在以下代码中：

```
namespace N
{
    public class A {}
    public class B {}
}
namespace N
{
    using A = System.IO;
    class X
    {
        A.Stream s1;      // Error, A is ambiguous
        A::Stream s2;     // Ok
    }
}
```

名称 A 在第二个命名空间体中有两种可能的含义，因为类 A 和使用别名 A 都在作用域内。因此，在限定名 A.Stream 中使用 A 会产生歧义，并导致编译时错误。然而，将 A 与 :: 限定符一起使用不是错误，因为此时 A 仅作为命名空间别名进行查找。示例结束]

```
type-parameters:
  attributes_opt type-parameter
  type-parameters , attributes_opt type-parameter
```

类型参数在 §9.5 中定义。

类声明中的每个类型参数都在该类的声明空间（§8.3）中定义一个名称。因此，它不能与该类的另一个类型参数或该类中声明的成员同名。类型参数不能与类型本身同名。

两个分部泛型类型声明（在同一程序中）如果具有相同的完全限定名（该名称包含针对类型参数数量的泛型维度说明符（§12.7.12））（§8.8.3），则它们构成同一个未绑定泛型类型。两个这样的分部类型声明应按顺序为每个类型参数指定相同的名称。

## 15.2.4 类基规范

### 15.2.4.1 概述

类声明可以包含类基规范，它定义该类的直接基类以及该类直接实现的接口（§18）。

```
class-base:
  : class-type
  : interface-type-list
  : class-type , interface-type-list

interface-type-list:
  interface-type
  interface-type-list , interface-type
```

### 15.2.4.2 基类

当 class-base 中包含 class-type 时，它指定正在声明的类的直接基类。如果非分部类声明没有 class-base，或者 class-base 仅列出接口类型，则假定直接基类为 object。当分部类声明包含基类规范时，该基类规范应引用与该分部类型中所有其他包含基类规范的部分相同的类型。如果分部类的任何部分都不包含基类规范，则基类为 object。类从其直接基类继承成员，如 §15.3.4 所述。

> [示例：在以下代码中
> class A {}
> class B: A {}
> 类 A 被称为 B 的直接基类，而 B 被称为派生自 A。由于 A 未显式指定直接基类，其直接基类隐式为 object。示例结束]

对于构造类类型（包括在泛型类型声明中声明的嵌套类型（§16.3.9.7）），如果在泛型类声明中指定了基类，则构造类型的基类通过以下方式获得：对基类声明中的每个类型参数，替换为构造类型的对应类型实参。[示例：给定以下泛型类声明
class B<U,V> {...}
class G<T>: B<string,T[]> {...}
构造类型 G<int> 的基类将是 B<string,int[]>。示例结束]

类声明中指定的基类可以是构造类类型（§9.4）。基类本身不能是类型参数（§9.5），但可以涉及作用域内的类型参数。[示例：
class Base<T> {}]

```
class Extend : Base<int>    // Valid, non-constructed class with
// constructed base class
class Extend<V>: V {}        // Error, type parameter used as base class
class Extend<V> : Base<V> {} // Valid, type parameter used as type
// argument for base class
```

示例结束]

类类型的直接基类应至少与类类型本身具有相同的可访问性（§8.5.5）。例如，public 类派生自 private 或 internal 类会导致编译时错误。

类类型的直接基类不得为以下任何类型：System.Array、System.Delegate、System.Enum 或 System.ValueType。此外，泛型类声明不得将 System.Attribute 用作直接或间接基类（§22.2.1）。

在确定类 B 的直接基类规范 A 的含义时，临时假定 B 的直接基类为 object，这确保基类规范的含义不能递归地依赖于自身。[示例：以下代码

```
class X<T> {
    public class Y{}
}
class Z : X<Z.Y> {}
```

是错误的，因为在基类规范 X<Z.Y> 中，Z 的直接基类被视为 object，因此（根据 §8.8 的规则）Z 不被视为具有成员 Y。示例结束]

类的基类包括直接基类及其基类。换言之，基类集合是直接基类关系的传递闭包。[示例：在以下代码中：

```
class A {...}
class B<T>: A {...}
class C<T>: B<IComparable<T>> {...}
class D<T>: C<T[]> {...}
```

D<int> 的基类是 C<int[]>、B<IComparable<int[]>>、A 和 object。
示例结束]

除 object 类外，每个类都恰好有一个直接基类。object 类没有直接基类，并且是所有其他类的最终基类。

类依赖于自身会导致编译时错误。就本规则而言，类直接依赖于其直接基类（如果有），并直接依赖于嵌套它的最近外层类（如果有）。根据此定义，类所依赖的类的完整集合是“直接依赖于”关系的传递闭包。

[示例：以下示例

```
class A: A {}
```

是错误的，因为该类依赖于自身。同样，以下示例

```
class A: B {}
class B: C {}
class C: A {}
```

是错误的，因为这些类循环依赖于自身。最后，以下示例

```
class A: B.C {}
```

```
class B: A
{
    public class C {}
}
```

会导致编译时错误，因为 A 依赖于 B.C（其直接基类），而 B.C 依赖于 B（其直接外层类），B 又循环依赖于 A。示例结束]

类不依赖于嵌套在它内部的类。[示例：在以下代码中

```
class A
{
    class B: A {}
}
```

B 依赖于 A（因为 A 既是它的直接基类，又是它的直接外层类），但 A 不依赖于 B（因为 B 既不是 A 的基类，也不是 A 的外层类）。因此，该示例是有效的。示例结束]

不能从密封类派生。[示例：在以下代码中

```
sealed class A {}
class B: A {}    // Error, cannot derive from a sealed class
```

类 B 是错误的，因为它试图从密封类 A 派生。示例结束]

### 15.2.4.3 接口实现

类基规范可以包含接口类型列表，在这种情况下，称该类实现给定的接口类型。对于构造类类型（包括在泛型类型声明中声明的嵌套类型（§15.3.9.7）），每个实现的接口类型通过以下方式获得：对给定接口中的每个类型参数，替换为构造类型的对应类型实参。

对于在多个部分中声明的类型（§15.2.7），其接口集合是每个部分上指定的接口的并集。特定接口在每个部分上只能被命名一次，但多个部分可以命名相同的基接口。对于任何给定接口的每个成员，应只有一个实现。

```
partial class C: IA, IB {...}
partial class C: IC {...}
partial class C: IA, IB {...}
```

类 C 的基接口集合是 IA、IB 和 IC。示例结束]

通常，每个部分提供在该部分上声明的接口的实现；然而，这并不是要求。一个部分可以为在另一个不同部分上声明的接口提供实现。

```
partial class X
{
    int IComparable.CompareTo(object o) {...}
}
partial class X: IComparable
{
    ...
}
```

示例结束]

类声明中指定的基接口可以是构造接口类型（§9.4、§18.2）。基接口本身不能是类型参数，但可以涉及作用域内的类型参数。[示例：以下代码说明类如何实现和扩展构造类型：

```
class C<U, V> {}
interface II<V> {}
```

```
class D: C<string, int>, I1<string> {}
class E<T>: C<int, T>, I1<T> {}
```

结束示例]

接口实现在 §18.6 中进一步讨论。

## 15.2.5 类型参数约束

泛型类型和方法声明可以通过包含类型参数约束子句来可选地指定类型参数约束。

```
type-parameter-constraints-clauses:
    type-parameter-constraints-clause
    type-parameter-constraints-clauses type-parameter-constraints-clause

type-parameter-constraints-clause:
    where type-parameter : type-parameter-constraints

type-parameter-constraints:
    primary-constraint
    secondary-constraints
    constructor-constraint
    primary-constraint , secondary-constraints
    primary-constraint , constructor-constraint
    secondary-constraints , constructor-constraint
    primary-constraint , secondary-constraints , constructor-constraint

primary-constraint:
    class-type
    class
    struct

secondary-constraints:
    interface-type
    type-parameter
    secondary-constraints , interface-type
    secondary-constraints , type-parameter

constructor-constraint:
    new ( )
```

每个类型参数约束子句由 where 标记、类型参数名称、冒号以及该类型参数的约束列表组成。每个类型参数至多可以有一个 where 子句，并且 where 子句可以按任意顺序列出。与属性访问器中的 get 和 set 标记一样，where 标记不是关键字。

where 子句中给出的约束列表可以按此顺序包含以下任何组件：单个主约束、一个或多个次要约束以及构造函数约束 new()。

主约束可以是类类型、引用类型约束 class 或值类型约束 struct。次要约束可以是类型参数或接口类型。

引用类型约束指定用于该类型参数的类型实参应为引用类型。所有类类型、接口类型、委托类型、数组类型以及已知为引用类型（如下所定义）的类型参数都满足此约束。

具有构造函数约束的类型参数。[注意：System.Nullable\<T> 类型为 T 指定了非可空值类型约束。因此，禁止使用 T?? 和 Nullable\<Nullable\<T>> 形式的递归构造类型。结束注意]

指针类型永远不允许作为类型实参，并且不被认为满足引用类型或值类型约束。

如果约束是类类型、接口类型或类型参数，则该类型指定了用于该类型参数的每个类型实参都应支持的最小“基类型”。每当使用构造类型或泛型方法时，都会在编译时根据类型参数上的约束检查类型实参。所提供的类型实参应满足 §9.4.5 中描述的条件。

类类型约束应满足以下规则：
- 该类型应为类类型。
- 该类型不应是密封的。
- 该类型不应是以下类型之一：System.Array、System.Delegate、System.Enum 或 System.ValueType。
- 该类型不应是 object。
- 给定类型参数的约束中至多有一个可以是类类型。

指定为接口类型约束的类型应满足以下规则：
- 该类型应为接口类型。
- 在给定的 where 子句中不应多次指定一个类型。

在上述任何一种情况下，约束可以涉及关联类型或方法声明的任何类型参数，作为构造类型的一部分，并且可以涉及正在声明的类型。

指定为类型参数约束的任何类或接口类型，其可访问性（§8.5.5）应不低于所声明的泛型类型或方法。

指定为类型参数约束的类型应满足以下规则：
- 该类型应为类型参数。
- 在给定的 where 子句中不应多次指定一个类型。

此外，类型参数的依赖关系图中不应存在循环，其中依赖关系是由以下定义的传递关系：
- 如果类型参数 T 用作类型参数 S 的约束，则 S 依赖于 T。
- 如果类型参数 S 依赖于类型参数 T，并且 T 依赖于类型参数 U，则 S 依赖于 U。

根据这种关系，类型参数直接或间接地依赖自身是编译时错误。

任何约束都应在相互依赖的类型参数之间保持一致。如果类型参数 S 依赖于类型参数 T，则：
- T 不应具有值类型约束。否则，T 实际上是密封的，因此 S 将被强制为与 T 相同的类型，从而消除了对两个类型参数的需要。
- 如果 S 具有值类型约束，则 T 不应具有类类型约束。
- 如果 S 具有类类型约束 A，而 T 具有类类型约束 B，则从 A 到 B 或从 B 到 A 应存在恒等转换或隐式引用转换。
- 如果 S 还依赖于类型参数 U，并且 U 具有类类型约束 A，而 T 具有类类型约束 B，则从 A 到 B 或从 B 到 A 应存在恒等转换或隐式引用转换。

S 具有值类型约束而 T 具有引用类型约束是合法的。这实际上将 T 限制为 System.Object、System.ValueType、System.Enum 以及任何接口类型。

如果类型参数的 where 子句包含构造函数约束（其形式为 new()），则可以使用 new 运算符创建该类型的实例（§12.7.11.2）。用于具有构造函数约束的类型参数的任何类型实参应为值类型、具有公共无参构造函数的非抽象类，或具有值类型约束或构造函数约束的类型参数。

[示例：以下是约束的示例：]

```
interface IPrintable
{
    void Print();
}
interface IComparable<T>
{
    int CompareTo(T value);
}
interface IKeyProvider<T>
{
    T GetKey();
}
class Printer<T> where T: IPrintable {...}
class SortedList<T> where T: IComparable<T> {...}
class Dictionary<K,V>
    where K: IComparable<K>
    where V: IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

以下示例是错误的，因为它导致类型参数依赖关系图中的循环：

```
class Circular<S,T>
    where S: T
    where T: S    // Error, circularity in dependency graph
{
    ...
}
```

以下示例说明了其他无效情况：

```
class Sealed<S,T>
    where S: T
    where T: struct    // Error, T is sealed
{
    ...
}
class A {...}
class B {...}
class Incompat<S,T>
    where S: A, T
    where T: B    // Error, incompatible class-type constraints
{
    ...
}
class StructWithClass<S,T,U>
    where S: struct, T
    where T: U
    where U: A    // Error, A incompatible with struct
{
    ...
}
```

结束示例]

类型 C 的动态擦除是如下构造的类型 C₀：
- 如果 C 是嵌套类型 Outer.Inner，则 C₀ 是嵌套类型 Outer₀.Inner₀。
- 如果 C 是带类型实参 A¹, ..., Aⁿ 的构造类型 G<A¹, ..., Aⁿ>，则 C₀ 是构造类型 G<A¹₀, ..., Aⁿ₀>。
- 如果 C 是数组类型 E[]，则 C₀ 是数组类型 E₀[]。
- 如果 C 是指针类型 E*，则 C₀ 是指针类型 E₀*。
- 如果 C 是 dynamic，则 C₀ 是 object。
- 否则，C₀ 是 C。

类型参数 T 的有效基类定义如下：

设 R 是一个类型集合，使得：
- 对于 T 的每个是类型参数的约束，R 包含其有效基类。
- 对于 T 的每个是结构类型的约束，R 包含 System.ValueType。
- 对于 T 的每个是枚举类型的约束，R 包含 System.Enum。
- 对于 T 的每个是委托类型的约束，R 包含其动态擦除。
- 对于 T 的每个是数组类型的约束，R 包含 System.Array。
- 对于 T 的每个是类类型的约束，R 包含其动态擦除。

然后：
- 如果 T 具有值类型约束，则其有效基类是 System.ValueType。
- 否则，如果 R 为空，则有效基类是 object。
- 否则，T 的有效基类是集合 R 中包容范围最大的类型（§11.5.3）。如果该集合中没有被包容的类型，则 T 的有效基类是 object。一致性规则确保包容范围最大的类型存在。

如果类型参数是方法类型参数，且其约束继承自基方法，则在类型替换后计算有效基类。

这些规则确保有效基类始终是类类型。

类型参数 T 的有效接口集定义如下：
- 如果 T 没有次要约束，则其有效接口集为空。
- 如果 T 具有接口类型约束但没有类型参数约束，则其有效接口集是其接口类型约束的动态擦除集。
- 如果 T 没有接口类型约束但具有类型参数约束，则其有效接口集是其类型参数约束的有效接口集的并集。




- 如果 T 同时具有 *接口类型* 约束和 *类型参数* 约束，则其有效接口集是其 *接口类型* 约束的动态擦除集合与其 *类型参数* 约束的有效接口集的并集。

类型参数如果具有引用类型约束或其有效基类不是 object 或 System.ValueType，则 *已知是引用类型*。

受约束的类型参数类型的取值可用于访问约束所暗示的实例成员。[示例：在以下内容中：

```
interface IPrintable
{
    void Print();
}
class Printer<T> where T: IPrintable
{
    void PrintOne(T x) {
        x.Print();
    }
}
```

IPrintable 的方法可以直接在 x 上调用，因为 T 被约束为始终实现 IPrintable。结束示例]

当部分泛型类型声明包含约束时，约束应与包含约束的所有其它部分一致。具体而言，包含约束的每个部分都应为同一组类型参数提供约束，并且对于每个类型参数，一级、二级和构造函数约束的集合应等价。两个约束集合如果包含相同的成员则等价。如果部分泛型类型的任何部分均未指定类型参数约束，则类型参数被视为无约束。[示例：

```
partial class Map<K,V>
    where K: IComparable<K>
    where V: IKeyProvider<K>, new()
{
    ...
}
partial class Map<K,V>
    where V: IKeyProvider<K>, new()
    where K: IComparable<K>
{
    ...
}
partial class Map<K,V>
{
    ...
}
```

是正确的，因为包含约束的那些部分（前两个）有效地为同一组类型参数分别指定了相同的一级、二级和构造函数约束集合。结束示例]

## 15.2.6 类体

类的 *类体* 定义了该类的成员。

```
class-body:
    { class-member-declarations_opt }
```

## 15.2.7 部分声明

*部分* 修饰符用于在多个部分中定义类、结构或接口类型。*部分* 修饰符是一个上下文关键字 (§7.4.4)，仅在 class、struct 或 interface 关键字之一之前具有特殊含义。

部分类型声明的每个部分都应包含 partial 修饰符，并应与其它部分在相同的命名空间或包含类型中声明。partial 修饰符表示类型声明的额外部分可能存在于别处，但此类额外部分的 existence 不是要求；仅有的类型声明包含 partial 修饰符是有效的。

所有部分类型都应一起编译，以便在编译时合并各部分。Partial types specifically 不允许扩展已编译的类型。

嵌套类型可以通过使用 partial 修饰符在多个部分中声明。通常，包含类型也使用 partial 声明，并且嵌套类型的每个部分都声明在包含类型的一个不同部分中。

[示例：以下部分类在两个部分中实现，这些部分位于不同的源文件中。第一部分由数据库映射工具机器生成，而第二部分是手动编写的：

```
public partial class Customer
{
    private int id;
    private string name;
    private string address;
    private List<Order> orders;
    public Customer() {
        ...
    }
}
```

```
public partial class Customer
{
    public void SubmitOrder(Order orderSubmitted) {
        orders.Add(orderSubmitted);
    }
    public bool HasOutstandingOrders() {
        return orders.Count > 0;
    }
}
```

当上述两个部分一起编译时，结果代码的行为就好像该类被作为单个单元编写一样，如下所示：

```
public class Customer
{
    private int id;
    private string name;
    private string address;
    private List<Order> orders;
    public Customer() {
        ...
    }
    public void SubmitOrder(Order orderSubmitted) {
        orders.Add(orderSubmitted);
    }
    public bool HasOutstandingOrders() {
        return orders.Count > 0;
    }
}
```

结束示例]

不同部分的部分声明中在类型或类型参数上指定的属性的处理在 §22.3 中讨论。

## 15.3 类成员

### 15.3.1 通用

类的成员由其 class-member-declarations 引入的成员和从直接基类继承的成员组成。

```
class-member-declarations:
    class-member-declaration
    class-member-declarations class-member-declaration
```

```
class-member-declaration:
    constant-declaration
    field-declaration
    method-declaration
    property-declaration
    event-declaration
    indexer-declaration
    operator-declaration
    constructor-declaration
    finalizer-declaration
    static-constructor-declaration
    type-declaration
```

类的成员分为以下几类：

- 常量，表示与类关联的常量值 (§15.4)。
- 字段，是类的变量 (§15.5)。
- 方法，实现类可以执行的计算和操作 (§15.6)。
- 属性，定义命名特征以及读取和写入这些特征相关联的操作 (§15.7)。
- 事件，定义类可以生成的通知 (§15.8)。
- 索引器，允许类的实例以与数组相同的方式（语法上）进行索引 (§15.9)。
- 运算符，定义可应用于类实例的表达式运算符 (§15.10)。
- 实例构造函数，实现初始化类实例所需的操作 (§15.11)
- 析构函数，实现在类实例永久丢弃之前执行的操作 (§15.13)。
- 静态构造函数，实现初始化类本身所需的操作 (§15.12)。
- 类型，表示局部于类的类型 (§14.7)。

可以包含可执行代码的成员统称为类的函数成员。类的函数成员是该类的方法、属性、事件、索引器、运算符、实例构造函数、析构函数和静态构造函数。

class-declaration 创建一个新的声明空间 (§8.3)，并且 class-declaration 直接包含的类型参数和 class-member-declarations 在此声明空间中引入新的成员。以下规则适用于 class-member-declarations：

- 实例构造函数、析构函数和静态构造函数应与直接封闭类的名称相同。所有其它成员的名称应与直接封闭类的名称不同。
- 类声明的类型参数列表中的类型参数的名称应与同一类型参数列表中的所有其它类型参数的名称不同，并且应与类的名称以及类的所有成员的名称不同。
- 类型的名称应与同一类中声明的所有非类型成员的名称不同。如果两个或多个类型声明共享相同的完全限定名，则声明应具有 partial 修饰符 (§15.2.7)，并且这些声明组合起来定义单个类型。[注意：由于类型声明的完全限定名编码了类型参数的数量，因此两个不同的类型只要类型参数数量不同就可以共享相同的名称。结束注意]
- 常量、字段、属性或事件的名称应与同一类中声明的所有其它成员的名称不同。
- 方法的名称应与同一类中声明的所有其它非方法成员的名称不同。此外，方法的签名 (§8.6) 应与同一类中声明的所有其它方法的签名不同，并且同一类中声明的两个方法不应仅因 ref 和 out 而签名不同。
- 实例构造函数的签名应与同一类中声明的所有其它实例构造函数的签名不同，并且同一类中声明的两个构造函数不应仅因 ref 和 out 而签名不同。
- 索引器的签名应与同一类中声明的所有其它索引器的签名不同。
- 运算符的签名应与同一类中声明的所有其它运算符的签名不同。

类的继承成员 (§15.3.4) 不是类声明空间的一部分。[注意：因此，派生类允许声明与继承成员具有相同名称或签名的成员（这实际上隐藏了继承成员）。结束注意]

在多个部分 (§15.2.7) 中声明的类型成员的集合是各部分中声明的成员的并集。类型声明所有部分的主体共享相同的声明空间 (§8.3)，并且每个成员的范围 (§8.7) 扩展到所有部分的主体。任何成员的可访问域始终包括封闭类型的所有部分；在一个部分中声明的私有成员可以自由地从另一个部分访问。在类型的多个部分中声明同一个成员是编译时错误，除非该成员是具有 partial 修饰符的类型。[示例：

```
partial class A
{
    int x;            // Error, cannot declare x more than once
    partial class Inner  // Ok, Inner is a partial type
    {
        int y;
    }
}
partial class A
{
    int x;            // Error, cannot declare x more than once
    partial class Inner  // Ok, Inner is a partial type
    {
        int z;
    }
}
```

结束示例]

字段初始化顺序在 C# 代码中可能很重要，并且提供了一些保证，如 §15.5.6.1 中所定义。否则，类型内成员的顺序很少重要，但在与其他语言和环境交互时可能很重要。在这些情况下，在多个部分中声明的类型内成员的顺序是未定义的。

### 15.3.2 实例类型

每个类声明都有一个关联的实例类型。对于泛型类声明，实例类型是通过从类型声明创建构造类型 (§9.4) 形成的，其中提供的每个类型参数都是相应的类型参数。由于实例类型使用类型参数，因此它只能在类型参数处于作用域内时使用；即在类声明内部。实例

实例类型是类声明内部编写的代码中 `this` 的类型。对于非泛型类，实例类型就是所声明的类。[示例：下面展示了若干类声明及其实例类型：

```
class A<T> // instance type: A<T>
{
    class B {} // instance type: A<T>.B
    class C<U> {} // instance type: A<T>.C<U>
}
class D {} // instance type: D
```

结束示例]

## 15.3.3 构造类型的成员

构造类型的非继承成员是通过以下方式获得的：对于成员声明中的每个类型参数，替换为构造类型中相应的类型实参。替换过程基于类型声明的语义含义，而不是简单的文本替换。

[示例：给定泛型类声明

```
class Gen<T,U>
{
    public T[,] a;
    public void G(int i, T t, Gen<U,T> gt) {...}
    public U Prop { get {...} set {...} }
    public int H(double d) {...}
}
```

构造类型 Gen<int[],IComparable<string>> 具有以下成员：

```
public int[,][] a;
public void G(int i, int[] t, Gen<IComparable<string>,int[]> gt) {...}
public IComparable<string> Prop { get {...} set {...} }
public int H(double d) {...}
```

泛型类声明 Gen 中成员 a 的类型是“T 的二维数组”，因此上述构造类型中成员 a 的类型是“int 的一维数组的二维数组”，即 int[,][]。结束示例]

在实例函数成员中，this 的类型是包含声明的实例类型（§15.3.2）。

泛型类的所有成员都可以直接使用任何外围类的类型参数，或将其作为构造类型的一部分使用。当在运行时使用特定的封闭构造类型（§9.4.3）时，每次使用类型参数都会替换为提供给该构造类型的类型实参。[示例：

```
class C<V>
{
    public V f1;
    public C<V> f2 = null;
    public C(V x) {
        this.f1 = x;
        this.f2 = this;
    }
}
class Application
{
    static void Main() {
        C<int> x1 = new C<int>(1);
        Console.WriteLine(x1.f1); // Prints 1
    }
}
```

结束示例]

如果 M 可访问，并且不存在其他已隐藏 M 的可访问继承成员 N，则继承成员 M 被视为可用。隐式隐藏继承成员不被视为错误，但它会导致编译器发出警告，除非派生类成员的声明包含 new 修饰符，以明确指示该派生成员旨在隐藏基成员。如果嵌套类型的分部声明（§15.2.7）的一个或多个部分包含 new 修饰符，则当该嵌套类型隐藏可用的继承成员时，不会发出警告。

如果声明中包含 new 修饰符，但该声明并未隐藏可用的继承成员，则会发出相应警告。

## 15.3.6 访问修饰符

类成员声明可以具有五种可能的声明可访问性（§8.5.2）中的任意一种：public、protected internal、protected、internal 或 private。除 protected internal 组合外，指定多个访问修饰符会导致编译时错误。当类成员声明不包含任何访问修饰符时，假定为 private。

## 15.3.7 构成类型

在成员声明中使用的类型称为该成员的构成类型。可能的构成类型包括常量、字段、属性、事件或索引器的类型，方法或运算符的返回类型，以及方法、索引器、运算符或实例构造函数的参数类型。成员的构成类型应至少与该成员本身具有相同的可访问性（§8.5.5）。

## 15.3.8 静态成员和实例成员

类的成员要么是静态成员，要么是实例成员。[注意：一般来说，将静态成员视为属于类、将实例成员视为属于对象（类的实例）是有用的。结束注释]

当字段、方法、属性、事件、运算符或构造函数声明包含 static 修饰符时，它声明静态成员。此外，常量或类型声明隐式声明静态成员。静态成员具有以下特征：

- 当在形式为 E . M 的成员访问（§12.7.5）中引用静态成员 M 时，E 应表示具有成员 M 的类型。若 E 表示实例，则会导致编译时错误。
- 非泛型类中的静态字段恰好标识一个存储位置。无论创建多少个非泛型类的实例，静态字段都只有一份副本。每个不同的封闭构造类型（§9.4.3）都有自己的一组静态字段，而不管该封闭构造类型的实例数量有多少。
- 静态函数成员（方法、属性、事件、运算符或构造函数）不作用于特定实例，并且在此类函数成员中引用 this 会导致编译时错误。

当字段、方法、属性、事件、索引器、构造函数或终结器声明不包含 static 修饰符时，它声明实例成员。（实例成员有时称为非静态成员。）实例成员具有以下特征：

- 当在形式为 E . M 的成员访问（§12.7.5）中引用实例成员 M 时，E 应表示具有成员 M 的类型的实例。若 E 表示类型，则会导致绑定期错误。
- 类的每个实例都包含该类所有实例字段的单独集合。
- 实例函数成员（方法、属性、索引器、实例构造函数或终结器）作用于该类的给定实例，并且可以通过 this（§12.7.8）访问该实例。

[示例：以下示例说明了访问静态成员和实例成员的规则：

```csharp
class Test
{
    int x;
    static int y;

    void F() {
        x = 1;            // Ok, same as this.x = 1
        y = 1;            // Ok, same as Test.y = 1
    }

    static void G() {
        x = 1;            // Error, cannot access this.x
        y = 1;            // Ok, same as Test.y = 1
    }

    static void Main() {
        Test t = new Test();
        t.x = 1;            // Ok
        t.y = 1;            // Error, cannot access static member through instance
        Test.x = 1;        // Error, cannot access instance member through type
        Test.y = 1;        // Ok
    }
}
```

F 方法表明，在实例函数成员中，*简单名称*（§12.7.3）可用于访问实例成员和静态成员。G 方法表明，在静态函数成员中，通过*简单名称*访问实例成员会导致编译时错误。Main 方法表明，在*成员访问*（§12.7.5）中，实例成员应通过实例访问，静态成员应通过类型访问。*结束示例*]

## 15.3.9 嵌套类型

### 15.3.9.1 概述

在类或结构内声明的类型称为*嵌套类型*。在编译单元或命名空间内声明的类型称为*非嵌套类型*。[示例：在以下示例中：

```csharp
using System;

class A
{
    class B
    {
        static void F() {
            Console.WriteLine("A.B.F");
        }
    }
}
```

类 B 是嵌套类型，因为它声明在类 A 内；类 A 是非嵌套类型，因为它声明在编译单元内。*结束示例*]

### 15.3.9.2 完全限定名

嵌套类型声明的完全限定名（§8.8.3）是 S.N，其中 S 是声明类型 N 的类型声明的完全限定名，N 是嵌套类型声明的非限定名（§8.8.2）（包括任何*泛型维度说明符*（§12.7.12））。

### 15.3.9.3 声明的可访问性

非嵌套类型可以具有 public 或 internal 的声明可访问性，并且默认具有 internal 声明可访问性。嵌套类型也可以具有这些形式的声明可访问性，以及一种或多种其他形式的声明可访问性，具体取决于包含类型是类还是结构：

- 在类中声明的嵌套类型可以具有五种声明可访问性形式中的任意一种（public、protected internal、protected、internal 或 private），并且与其他类成员一样，默认具有 private 声明可访问性。
- 在结构中声明的嵌套类型可以具有三种声明可访问性形式中的任意一种（public、internal 或 private），并且与其他结构成员一样，默认具有 private 声明可访问性。

[示例：该示例

```csharp
public class List
{
    // Private data structure
    private class Node
    {
        public object Data;
        public Node Next;
        public Node(object data, Node next) {
            this.Data = data;
            this.Next = next;
        }
    }

    private Node first = null;
    private Node last = null;

    // Public interface
    public void AddToFront(object o) {...}
    public void AddToBack(object o) {...}
    public object RemoveFromFront() {...}
    public object RemoveFromBack() {...}
    public int Count { get {...} }
}
```

声明了一个私有嵌套类 Node。*示例结束*

## 15.3.9.4 隐藏

嵌套类型可以隐藏（§8.7.2.2）基成员。new 修饰符（§15.3.5）允许用于嵌套类型声明，以便可以显式表达隐藏。[*示例*：以下示例

```csharp
using System;

class Base
{
    public static void M() {
        Console.WriteLine("Base.M");
    }
}

class Derived: Base
{
    new public class M
    {
        public static void F() {
            Console.WriteLine("Derived.M.F");
        }
    }
}

class Test
{
    static void Main() {
        Derived.M.F();
    }
}
```

展示了一个嵌套类 M，它隐藏了在 Base 中定义的方法 M。*示例结束*]

## 15.3.9.5 this 访问

嵌套类型与其包含类型在 *this 访问*（§12.7.8）方面没有特殊关系。具体而言，嵌套类型中的 `this` 不能用于引用包含类型的实例成员。如果嵌套类型需要访问其包含类型的实例成员，可以通过将包含类型实例的 `this` 作为嵌套类型的构造函数参数来提供访问。[*示例*：以下示例

```csharp
using System;
```

~~~csharp
class C
{
    int i = 123;
    public void F() {
        Nested n = new Nested(this);
        n.G();
    }
    public class Nested
    {
        C this_c;
        public Nested(C c) {
            this_c = c;
        }
        public void G() {
            Console.WriteLine(this_c.i);
        }
    }
}
class Test
{
    static void Main() {
        C c = new C();
        c.F();
    }
}
~~~

展示了此技术。C 的实例创建一个 Nested 实例，并将自己的 this 传递给 Nested 的构造函数，以便后续访问 C 的实例成员。示例结束]

## 15.3.9.6 对包含类型的私有和受保护成员的访问

嵌套类型可以访问其包含类型可访问的所有成员，包括包含类型中具有 private 和 protected 声明可访问性的成员。[示例：以下示例

~~~csharp
using System;
class C
{
    private static void F() {
        Console.WriteLine("C.F");
    }
    public class Nested
    {
        public static void G() {
            F();
        }
    }
}
class Test
{
    static void Main() {
        C.Nested.G();
    }
}
~~~

展示了一个类 C，它包含一个嵌套类 Nested。在 Nested 内，方法 G 调用在 C 中定义的静态方法 F，而 F 具有 private 声明可访问性。示例结束]

嵌套类型还可以访问在其包含类型的基类型中定义的受保护成员。[示例：在以下代码中

~~~csharp
using System;
~~~

class Outer<T>
{
    class Inner<T>    // valid, hides Outer's T
    {
        public T t;    // Refers to Inner's T
    }
}

示例结束]

## 15.3.10 保留成员名称

### 15.3.10.1 概述

为了便于底层 C# 运行时实现，对于每个作为属性、事件或索引器的源成员声明，实现应基于成员声明的种类、名称和类型（§15.3.10.2、§15.3.10.3、§15.3.10.4）保留两个方法签名。如果程序声明的成员的签名与同一作用域中声明的成员所保留的签名匹配，则即使底层运行时实现不使用这些保留，也会产生编译时错误。

保留名称不引入声明，因此不参与成员查找。但是，声明关联的保留方法签名确实参与继承（§15.3.4），并且可以用 new 修饰符（§15.3.5）隐藏。

[注意：保留这些名称有三个目的：

- 1. 允许底层实现使用普通标识符作为方法名，以便对 C# 语言特性进行 get 或 set 访问。
- 2. 允许其他语言使用普通标识符作为方法名，以便对 C# 语言特性进行 get 或 set 访问，从而实现互操作。
- 3. 通过使保留成员名称的具体细节在所有 C# 实现中保持一致，帮助确保一个符合规范的编译器接受的源代码也能被另一个编译器接受。

注意结束]

终结器（§15.13）的声明也会导致保留一个签名（§15.3.10.5）。

### 15.3.10.2 为属性保留的成员名称

对于类型为 T 的属性 P（§15.7），保留以下签名：

```
T get_P();
void set_P(T value);
```

即使属性是只读或只写的，也会保留这两个签名。

[示例：在以下代码中

```
using System;
class A
{
    public int P {
        get { return 123; }
    }
}
class B: A
{
    new public int get_P() {
        return 456;
    }
    new public void set_P(int value) {
    }
}
```

```
class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        Console.WriteLine(a.P);
        Console.WriteLine(b.P);
        Console.WriteLine(b.get_P());
    }
}
```

类 A 定义只读属性 P，因此保留 get_P 和 set_P 方法的签名。类 B 从 A 派生并隐藏这两个保留签名。该示例产生以下输出：

```
123
123
456
```

*示例结束*]

### 15.3.10.3 为事件保留的成员名称

对于委托类型为 T 的事件 E（§15.8），保留以下签名：

```
void add_E(T handler);
void remove_E(T handler);
```

### 15.3.10.4 为索引器保留的成员名称

对于类型为 T、参数列表为 L 的索引器（§15.9），保留以下签名：

```
T get_Item(L);
void set_Item(L, T value);
```

即使索引器是只读或只写的，也会保留这两个签名。

此外，成员名称 *Item* 被保留。

### 15.3.10.5 为终结器保留的成员名称

对于包含终结器的类（§15.13），保留以下签名：

```
void Finalize();
```

## 15.4 常量

*常量*是表示常量值的类成员：该值可在编译时计算。*常量声明*引入一个或多个给定类型的常量。

```
constant-declaration:
    attributes_opt   constant-modifiers_opt   const   type   constant-declarators   ;
constant-modifiers:
    constant-modifier
    constant-modifiers   constant-modifier
constant-modifier:
    new
    public
    protected
    internal
    private
constant-declarators:
    constant-declarator
    constant-declarators   ,   constant-declarator
constant-declarator:
    identifier   =   constant-expression
```

常量声明可以包含一组特性（§22）、new 修饰符（§15.3.5）以及四个访问修饰符的有效组合（§15.3.6）。特性和修饰符应用于常量声明所声明的所有成员。尽管常量被视为静态成员，但常量声明既不要求也不允许 static 修饰符。同一修饰符在常量声明中出现多次是错误的。

常量声明的类型指定该声明所引入成员的类型。类型后跟常量声明符列表，其中每个常量声明符引入一个新成员。常量声明符由命名该成员的标识符、后跟一个“=”标记、再后跟给出该成员值的常量表达式（§12.20）组成。

常量声明中指定的类型应为 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool、string、枚举类型或引用类型。每个常量表达式应生成目标类型的值，或生成可通过隐式转换（§11.2）转换为目标类型的值。

常量的类型应至少与常量本身一样可访问（§8.5.5）。

常量的值通过在表达式中使用简单名称（§12.7.3）或成员访问（§12.7.5）来获取。

常量本身可以参与常量表达式。因此，常量可用于任何需要常量表达式的构造。[注意：此类构造的示例包括 case 标签、goto case 语句、枚举成员声明、特性以及其他常量声明。注意结束]

[注意：如 §12.20 所述，常量表达式是可在编译时完全求值的表达式。由于创建除 string 之外的引用类型的非 null 值的唯一方式是应用 new 运算符，并且常量表达式中不允许使用 new 运算符，因此除 string 之外的引用类型常量的唯一可能值是 null。注意结束]

当需要为常量值使用符号名称，但该值的类型不允许在常量声明中使用，或者该值无法通过常量表达式在编译时计算时，可以改用 readonly 字段（§15.5.3）。[注意：const 和 readonly 的版本控制语义（§15.5.3.3）。注意结束]

一个声明多个常量的常量声明，等效于多个具有相同特性、修饰符和类型的单个常量声明。[示例：

```
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```

等效于

```
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

示例结束]

常量可以依赖于同一程序中的其他常量，只要这些依赖关系不具有循环性质。编译器会自动安排以适当的顺序计算常量声明。[示例：在以下代码中

```
class A
{
    public const int X = B.Z + 1;
    public const int Y = 10;
}
```



```
class B
{
    public const int Z = A.Y + 1;
}
```

编译器首先计算 A.Y，然后计算 B.Z，最后计算 A.X，产生的值为 10、11 和 12。结束示例] 常量声明可能依赖于其他程序中的常量，但此类依赖只能单向进行。 [示例：参考上面的示例，如果 A 和 B 在单独的程序中声明，则 A.X 可能依赖于 B.Z，但 B.Z 则不能同时依赖于 A.Y。结束示例]

## 15.5 字段

### 15.5.1 通用

字段是表示与对象或类关联的变量的成员。字段声明引入一个或多个给定类型的字段。

```
field-declaration:
    attributesopt field-modifiersopt type variable-declarators ;

field-modifiers:
    field-modifier
    field-modifier field-modifier

field-modifier:
    new
    public
    protected
    internal
    private
    static
    readonly
    volatile

variable-declarators:
    variable-declarator
    variable-declarator , variable-declarator

variable-declarator:
    identifier
    identifier = variable-initializer

variable-initializer:
    expression
    array-initializer
```

字段声明可以包含一组属性 (§22)、一个 new 修饰符 (§15.3.5)、四个访问修饰符 (§15.3.6) 的有效组合以及一个 static 修饰符 (§15.5.2)。此外，字段声明可以包含 readonly 修饰符 (§15.5.3) 或 volatile 修饰符 (§15.5.4)，但不能同时包含。属性和修饰符适用于字段声明所声明的所有成员。在字段声明中同一个修饰符出现多次是错误。

字段声明的类型指定了声明引入的成员的类型。其后跟随一个 variable-declarators 列表，每个列表项引入一个新的成员。variable-declarator 由一个标识符组成，该标识符命名该成员，可选择后跟 “=” 标记和一个 variable-initializer (§15.5.6)，后者给出该成员的初始值。

字段的类型应至少与字段本身一样可访问 (§8.5.5)。

字段的值在表达式中通过 simple-name (§12.7.3)、member-access (§12.7.5) 或 base-access (§12.7.9) 获取。非只读字段的值通过赋值 (§12.18) 修改。该

```
~~~csharp
        private byte red, green, blue;
        public Color(byte r, byte g, byte b) {
            red = r;
            green = g;
            blue = b;
        }
    }
~~~
```

Black、white、Red、Green 和 Blue 成员不能声明为 const 成员，因为它们的值无法在编译时计算。然而，将它们声明为 static readonly 效果基本相同。*结束示例*]

### 15.5.3.3 常量和 static readonly 字段的版本控制

常量和只读字段具有不同的二进制版本语义。当表达式引用常量时，常量的值在编译时获取，但当表达式引用只读字段时，字段的值要到运行时才获取。[*示例：* 考虑一个由两个独立程序组成的应用程序：

```
~~~csharp
        namespace Program1
        {
            public class Utils
            {
                public static readonly int X = 1;
            }
        }
~~~
```

and

```
~~~csharp
        using System;
        namespace Program2
        {
            class Test
            {
                static void Main() {
                    Console.WriteLine(Program1.Utils.X);
                }
            }
        }
~~~
```

`Program1` 和 `Program2` 命名空间表示两个分别编译的程序。因为 `Program1.Utils.X` 被声明为 static readonly 字段，`Console.WriteLine` 语句输出的值在编译时未知，而是运行时获取。因此，如果 `X` 的值被更改并且 `Program1` 被重新编译，`Console.WriteLine` 语句将输出新值，即使 `Program2` 未被重新编译。然而，如果 `X` 是常量，则 `X` 的值将在 `Program2` 编译时获取，并且在 `Program2` 重新编译之前不受 `Program1` 更改的影响。*结束示例*]

### 15.5.4 易失字段

当 *字段声明* 包含 `volatile` 修饰符时，该声明引入的字段为 *易失字段*。对于非易失字段，重排序指令的优化技术可能导致在多线程程序中出现意外且不可预测的结果，这些程序在没有同步的情况下访问字段，例如 *lock-statement* (§13.13) 提供的同步。这些优化可以由编译器、运行时系统或硬件执行。对于易失字段，此类重排序优化受到限制：

- 对易失字段的读取称为 *易失读取*。易失读取具有“获取语义”；即保证在指令序列中在其之后出现的任何内存引用之前发生。
- 对易失字段的写入称为 *易失写入*。易失写入具有“释放语义”；即保证在指令序列中写入指令之前的任何内存引用之后发生。

这些限制确保所有线程都会按执行顺序观察到任何其他线程执行的易失写入。符合规范的实现不需要提供从所有执行线程角度看到的易失写入的单一总顺序。易失字段的类型应为以下之一：

- 引用类型。
- 已知为引用类型的类型参数 (§15.2.5)。
- 类型 byte、sbyte、short、ushort、int、uint、char、float、bool、System.IntPtr 或 System.UIntPtr。
- 枚举基类型为 byte、sbyte、short、ushort、int 或 uint 的枚举类型。

```
[Example: The example
using System;
using System.Threading;
class Test
{
    public static int result;
    public static volatile bool finished;
    static void Thread2() {
        result = 143;
        finished = true;
    }
    static void Main() {
        finished = false;
        // Run Thread2() in a new thread
        new Thread(new ThreadStart(Thread2)).Start();
        // wait for Thread2 to signal that it has a result by setting
        // finished to true.
        for (;;) {
            if (finished) {
                Console.WriteLine("result = {0}", result);
                return;
            }
        }
    }
}
```

产生输出：

result = 143

在此示例中，方法 Main 启动一个新线程运行方法 Thread2。该方法将值存储到名为 result 的非易失字段中，然后将 true 存储到易失字段 finished 中。主线程等待字段 finished 被设置为 true，然后读取字段 result。由于 finished 已声明为易失，主线程应从字段 result 读取值 143。如果字段 finished 未声明为易失，则允许对 result 的存储在主线程中对 finished 的存储之后才可见，从而主线程可能从字段 result 读取值 0。将 finished 声明为易失字段可防止此类不一致。结束示例

### 15.5.5 字段初始化

字段的初始值，无论是静态字段还是实例字段，都是字段类型默认值 (§10.3)。在默认初始化发生之前无法观察字段的值，因此字段永远不会“未初始化”。 [示例：示例

```
using System;
class Test
{
    static bool b;
    int i;
```

```
static void Main() {
    Test t = new Test();
    Console.WriteLine("b = {0}, i = {1}", b, t.i);
}
```

产生输出

b = False, i = 0

因为 b 和 i 都自动初始化为默认值。结束示例]

### 15.5.6 变量初始化器

### 15.5.6.1 通用

字段声明可以包含 variable-initializers。对于静态字段，变量初始化器对应于在类初始化期间执行的赋值语句。对于实例字段，变量初始化器对应于在创建类的实例时执行的赋值语句。

[示例：示例

```
using System;
class Test
{
    static double x = Math.Sqrt(2.0);
    int i = 100;
    string s = "Hello";
    static void Main() {
        Test a = new Test();
        Console.WriteLine("x = {0}, i = {1}, s = {2}", x, a.i, a.s);
    }
}
```

产生输出

x = 1.4142135623731, i = 100, s = Hello

因为对 x 的赋值在静态字段初始化器执行时发生，而对 i 和 s 的赋值在实例字段初始化器执行时发生。结束示例]

§15.5.5 中描述的默认值初始化适用于所有字段，包括具有变量初始化器的字段。因此，当类初始化时，该类中的所有静态字段首先初始化为默认值，然后按文本顺序执行静态字段初始化器。同样，当创建类的实例时，该实例中的所有实例字段首先初始化为默认值，然后按文本顺序执行实例字段初始化器。当同一类型的多个 partial 类型声明中存在字段声明时，各部分顺序未指定。但是，在每个部分内部，字段初始化器按顺序执行。

具有变量初始化器的静态字段可能在其默认值状态下被观察到。 [示例：然而，出于风格考虑，这强烈不被推荐。示例

```
using System;
class Test
{
    static int a = b + 1;
    static int b = a + 1;
    static void Main() {
        Console.WriteLine("a = {0}, b = {1}", a, b);
    }
}
```

表现出此行为。尽管 a 和 b 的定义是循环的，但程序是有效的。其结果输出为

a = 1, b = 2



```
class B
{
    static B() {}
    public static int Y = Test.F("Init B");
}
```

输出应为：

```
Init B
Init A
1 1
```

因为在静态构造函数执行时（定义见 §15.12）的规则规定，B 的静态构造函数（因此 B 的静态字段初始值设定项）应在 A 的静态构造函数和字段初始值设定项之前运行。结束示例]

## 15.5.6.3 实例字段初始化

类的实例字段变量初始值设定项对应于一系列赋值操作，这些赋值操作在进入该类的任何一个实例构造函数（§15.11.3）时立即执行。在部分类中，“文本顺序”的含义由 §15.5.6.1 指定。变量初始值设定项按照它们在类声明（§15.5.6.1）中出现的文本顺序执行。类实例创建和初始化过程在 §15.11 中进一步描述。

实例字段的变量初始值设定项不能引用正在创建的实例。因此，在变量初始值设定项中引用 this 会导致编译时错误，因为变量初始值设定项通过简单名称引用任何实例成员也是编译时错误。[示例：在以下代码中

```
class A
{
    int x = 1;
    int y = x + 1;    // Error, reference to instance member of this
}
```

y 的变量初始值设定项导致编译时错误，因为它引用了正在创建的实例的成员。结束示例]

## 15.6 方法

### 15.6.1 通用

方法是一个成员，它实现可由对象或类执行计算或操作。方法使用 method-declarations 声明：

```
method-declaration:
    method-header method-body

method-header:
    attributesopt method-modifiersopt partialopt return-type member-name
        type-parameter-list opt
        ( formal-parameter-list opt ) type-parameter-constraints-clausesopt

method-modifiers:
    method-modifier
    method-modifiers method-modifier
```

```
method-modifier:
  new
  public
  protected
  internal
  private
  static
  virtual
  sealed
  override
  abstract
  extern
  async

return-type:
  type
  void

member-name:
  identifier
  interface-type . identifier

method-body:
  block
  ;
```

method-declaration 可能会包含一组属性（§22）和四种访问修饰符（§15.3.6）的有效组合，以及 new（§15.3.5）、static（§15.6.3）、virtual（§15.6.4）、override（§15.6.5）、sealed（§15.6.6）、abstract（§15.6.7）、extern（§15.6.8）和 async（§15.15）修饰符。

如果满足以下所有条件，则声明具有修饰符的有效组合：

- 声明包含访问修饰符的有效组合（§15.3.6）。
- 声明不包含相同修饰符多次。
- 声明最多包含以下修饰符之一：static、virtual 和 override。
- 声明最多包含以下修饰符之一：new 和 override。
- 如果声明包含 abstract 修饰符，则声明不包含以下任何修饰符：static、virtual、sealed 或 extern。
- 如果声明包含 private 修饰符，则声明不包含以下任何修饰符：virtual、override 或 abstract。
- 如果声明包含 sealed 修饰符，则声明还包含 override 修饰符。
- 如果声明包含 partial 修饰符，则它不包含以下任何修饰符：new、public、protected、internal、private、virtual、sealed、override、abstract 或 extern。

方法声明的 return-type 指定了方法计算并返回的值的类型。如果方法不返回值，则 return-type 为 void。如果声明包含 partial 修饰符，则返回类型应为 void。

泛型方法是指其声明包含 type-parameter-list 的方法。这指定了方法的类型参数。可选的 type-parameter-constraints-clauses 指定类型参数的约束。method-declaration 除非同时具有 type-parameter-list，否则不得具有 type-parameter-constraints-clauses。显式接口成员实现的 method-declaration 不得具有任何 type-parameter-constraints-clauses。显式接口成员实现的泛型 method-declaration 从接口方法上的约束继承任何约束。同样，具有 override 修饰符的方法声明不得具有任何 type-parameter-constraints-clauses

并且方法的类型参数的约束从被重写虚拟方法继承。member-name 指定方法名称。除非方法是显式接口成员实现（§18.6.2），否则 member-name 只是标识符。对于显式接口成员实现，member-name 由 interface-type 后跟 “.” 和标识符组成。在这种情况下，声明不得包含除（可能）extern 或 async 之外的修饰符。

可选的 formal-parameter-list 指定方法参数（§15.6.2）。

方法声明的 return-type 和 formal-parameter-list 中引用的每个类型应至少与方法本身一样可访问（§8.5.5）。

对于 abstract 和 extern 方法，method-body 仅由分号组成。对于 partial 方法，method-body 可能由分号或块组成。对于所有其他方法，method-body 由块组成，该块指定在调用方法时要执行的语句。

如果 method-body 由分号组成，则声明不得包含 async 修饰符。

方法的名称、类型参数的数量和形式参数列表定义了方法签名（§8.6）。具体来说，方法的签名由其名称、其类型参数的数量以及其形式参数的数量、参数模式修饰符（§15.6.2.1）和类型组成。返回类型不是方法签名的一部分，形式参数的名称、类型参数的名称或约束也不是。 当形式参数类型引用方法的类型参数时，使用类型参数的序数位置（而不是类型参数的名称）进行类型等价。

方法的名称应与同一类中声明的所有其他非方法名称不同。此外，方法的签名应与同一类中声明的所有其他方法的签名不同，并且同一类中声明的两个方法不得仅因 ref 和 out 而签名不同。

方法的 type-parameters 在整个 method-declaration 中处于作用域内，并且可以在该作用域内的 return-type、method-body 和 type-parameter-constraints-clauses 中用于形成类型，但在属性中不能使用。

所有形式参数和类型参数应具有不同的名称。

### 15.6.2 方法参数

### 15.6.2.1 通用

方法的参数（如果有）由方法的 formal-parameter-list 声明。

```
formal-parameter-list:
    fixed-parameters
    fixed-parameters , parameter-array
    parameter-array
fixed-parameters:
    fixed-parameter
    fixed-parameters , fixed-parameter
fixed-parameter:
    attributesopt parameter-modifieropt type identifier default-argumentopt
default-argument:
    = expression
parameter-modifier:
    parameter-mode-modifier
    this
```

```
parameter-mode-modifier:
  ref
  out
```

```
parameter-array:
  attributesopt params array-type identifier
```

形式参数列表由一个或多个以逗号分隔的参数组成，其中只有最后一个可以是 parameter-array。

fixed-parameter 由可选的属性集（§22）；可选的 ref、out 或 this 修饰符；类型；标识符；以及可选的 default-argument 组成。每个 fixed-parameter 声明给定类型和给定名称的参数。this 修饰符将方法指定为扩展方法，并且仅允许在非泛型、非嵌套静态类中的静态方法的第一个参数上使用。扩展方法在 §15.6.10 中进一步描述。具有 default-argument 的 fixed-parameter 称为可选参数，而没有 default-argument 的 fixed-parameter 是必需参数。必需参数在 formal-parameter-list 中不得出现在可选参数之后。

具有 ref、out 或 this 修饰符的参数不能具有 default-argument。default-argument 中的表达式应为以下之一：

- constant-expression
- 形式为 new S() 的表达式，其中 S 是值类型
- 形式为 default(S) 的表达式，其中 S 是值类型

该表达式应可通过标识或可空转换隐式转换为参数的类型。

如果在实现 partial 方法声明（§15.6.9）、显式接口成员实现（§18.6.2）、单参数索引器声明（§15.9）或运算符声明（§15.10.1）中出现可选参数，编译器应发出警告，因为这些成员永远无法以允许省略参数的方式调用。

parameter-array 由可选的属性集（§22）、params 修饰符、array-type 和标识符组成。参数数组声明给定数组类型和给定名称的单个参数。参数数组的 array-type 应为单维数组类型（§17.2）。在方法调用中，参数数组允许指定给定数组类型的单个参数，也允许指定零个或多个数组元素类型的参数。参数数组在 §15.6.2.5 中进一步描述。

parameter-array 可能出现在可选参数之后，但不能具有默认值——对于 parameter-array 省略参数将导致创建空数组。

[示例：以下示例说明了不同种类的参数：

```
public void M(
  ref int i,
  decimal d,
  bool b = false,
  bool? n = false,
  string s = "Hello",
  object o = null,
  T t = default(T),
  params int[] a
) { }
```

在 M 的 formal-parameter-list 中，i 是必需的 ref 参数，d 是必需的值参数，b、s、o 和 t 是可选值参数，a 是参数数组。结束示例

方法声明为参数和类型参数创建单独的声明空间（§8.3）。名称由类型参数列表和形式参数列表引入到此声明空间中

方法。方法体（如果有的话）被视为嵌套在此声明空间内。方法声明空间的两个成员具有相同名称是错误。方法声明空间与嵌套声明空间的局部变量声明空间包含具有相同名称的元素是错误。

方法调用（§12.7.6.2）会为该调用创建方法的形式参数和局部变量的特定副本，并且调用的参数列表会为新创建的形式参数分配值或变量引用。在方法块内，可以通过标识符在简单名称表达式（§12.7.3）中引用形式参数。

有四种形式参数：

- 值参数，它们是在没有任何修饰符的情况下声明的。
- 引用参数，它们是用 ref 修饰符声明的。
- 输出参数，它们是用 out 修饰符声明的。
- 参数数组，它们是用 params 修饰符声明的。

> [注意：如§8.6所述，ref 和 out 修饰符是方法签名的一部分，但 params 修饰符不是。结束注意]

## 15.6.2.2 值参数

未使用修饰符声明的参数是值参数。值参数对应于一个局部变量，其初始值来自方法调用中提供的相应参数。

当形式参数是值参数时，方法调用中的相应参数应为可隐式转换为形式参数类型（§11.2）的表达式。

方法允许为值参数分配新值。此类赋值仅影响值参数所表示的局部存储位置——它们对方法调用中给出的实际参数没有影响。

## 15.6.2.3 引用参数

使用 ref 修饰符声明的参数是引用参数。与值参数不同，引用参数不会创建新的存储位置。相反，引用参数表示与方法调用中作为参数给出的变量相同的存储位置。

> [示例：示例

```
using System;
class Test
{
    static void Swap(ref int x, ref int y) {
        int temp = x;
        x = y;
        y = temp;
    }
    static void Main() {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine("i = {0}, j = {1}", i, j);
    }
}
```

产生输出

i = 2, j = 1

对于 Main 中 Swap 的调用，x 表示 i 而 y 表示 j。因此，该调用的效果是交换 i 和 j 的值。结束示例]

在接受引用参数的方法中，可能存在多个名称表示相同的存储位置。[示例：在以下代码中

```
class A
{
    string s;
    void F(ref string a, ref string b) {
        s = "One";
        a = "Two";
        b = "Three";
    }
    void G() {
        F(ref s, ref s);
    }
}
```

G 中对 F 的调用为 a 和 b 都传递了 s 的引用。因此，对于该调用，名称 s、a 和 b 都引用相同的存储位置，并且三个赋值都修改实例字段 s。结束示例]

## 15.6.2.4 输出参数

使用 out 修饰符声明的参数是输出参数。与引用参数类似，输出参数不会创建新的存储位置。相反，输出参数表示与方法调用中作为参数给出的变量相同的存储位置。

当形式参数是输出参数时，方法调用中的相应参数应由关键字 out 后跟与形式参数类型相同类型的变量引用（§10.5）组成。变量在作为输出参数传递之前不必被明确赋值，但在变量作为输出参数传递的调用之后，该变量被认为已明确赋值。

在方法内部，就像局部变量一样，输出参数最初被视为未赋值，并且在使用其值之前必须被明确赋值。

方法的所有输出参数必须在方法返回之前被明确赋值。

声明为分部方法（§15.6.9）或迭代器（§15.14）的方法不得具有输出参数。

输出参数通常用于产生多个返回值的方法。[示例：

```
using System;
class Test
{
    static void SplitPath(string path, out string dir, out string name) {
        int i = path.Length;
        while (i > 0) {
            char ch = path[i - 1];
            if (ch == '\\' || ch == '/' || ch == ':') break;
            i--;
        }
        dir = path.Substring(0, i);
        name = path.Substring(i);
    }
    static void Main() {
        string dir, name;
        SplitPath("c:\\windows\\System\\hello.txt", out dir, out name);
        Console.WriteLine(dir);
        Console.WriteLine(name);
    }
}
```

示例产生输出：

c:\windows\System\
hello.txt

请注意，dir 和 name 变量在传递给 SplitPath 之前可以未赋值，并且在调用后被认为已明确赋值。结束示例]

## 15.6.2.5 参数数组

使用 params 修饰符声明的参数是参数数组。如果形式参数列表包含参数数组，则它应为列表中的最后一个参数，并且应为单维数组类型。

[示例：类型 string[] 和 string[][] 可用作参数数组的类型，但类型 string[,] 不可以。结束示例] 不可能将 params 修饰符与 ref 和 out 修饰符组合使用。

参数数组允许在方法调用中以两种方式指定参数：

- 可以为参数数组提供可隐式转换为参数数组类型（§11.2）的单个表达式。在这种情况下，参数数组完全像值参数一样起作用。
- 或者，调用可以为参数数组指定零个或多个参数，其中每个参数都是可隐式转换为参数数组元素类型（§11.2）的表达式。在这种情况下，调用会创建长度对应于参数数量的参数数组类型实例，用给定的参数值初始化数组实例的元素，并将新创建的数组实例用作实际参数。

除了允许调用中具有可变数量的参数外，参数数组与相同类型的价值参数（§15.6.2.2）完全等价。

[示例：示例

```
using System;
class Test
{
    static void F(params int[] args) {
        Console.Write("Array contains {0} elements:", args.Length);
        foreach (int i in args)
            Console.Write("{0}", i);
        Console.WriteLine();
    }
    static void Main() {
        int[] arr = {1, 2, 3};
        F(arr);
        F(10, 20, 30, 40);
        F();
    }
}
```

产生输出

```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

F 的第一次调用只是将数组 arr 作为值参数传递。F 的第二次调用自动创建一个包含给定元素值的四元素 int[] 并将该数组实例作为值参数传递。同样，F 的第三次调用创建一个零元素 int[] 并将该实例作为值参数传递。第二次和第三次调用与编写以下内容完全等价：

```
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

*结束示例*

在执行重载解析时，具有参数数组的方法可能适用，其形式为正常形式或扩展形式（§12.6.4.2）。方法的扩展形式只有在方法的正常形式不适用并且在同一类型中尚未声明具有与扩展形式相同签名的适用方法时才可用。

[示例：示例

```
using System;
class Test
{
    static void F(params object[] a) {
        Console.WriteLine("F(object[])");
    }
    static void F() {
        Console.WriteLine("F()");
    }
    static void F(object a0, object a1) {
        Console.WriteLine("F(object,object)");
    }
    static void Main() {
        F();
        F(1);
        F(1, 2);
        F(1, 2, 3);
        F(1, 2, 3, 4);
    }
}
```

产生输出

```
F();
F(object[]);
F(object,object);
F(object[]);
F(object[]);
```

在示例中，参数数组方法的两个可能扩展形式已作为常规方法包含在类中。因此，在执行重载解析时不会考虑这些扩展形式，第一和第三次方法调用因此选择常规方法。当类声明具有参数数组的方法时，通常也会将一些扩展形式作为常规方法包含在内。通过这样做，可以避免在调用具有参数数组的方法的扩展形式时发生的数组实例分配。结束示例

当参数数组的类型为 object[] 时，在方法的正常形式与单个对象参数的扩展形式之间会出现潜在的歧义。歧义的原因是 object[] 本身可隐式转换为 object 类型。然而，歧义不会造成问题，因为如果需要，可以通过插入强制转换来解决。

[示例：示例

```
using System;
```

```csharp
class Test
{
    static void F(params object[] args) {
        foreach (object o in args) {
            Console.Write(o.GetType().FullName);
            Console.Write(" ");
        }
        Console.WriteLine();
    }
    static void Main() {
        object[] a = {1,"Hello", 123.456};
        object o = a;
        F(a);
        F((object)a);
        F(o);
        F((object[])o);
    }
}
```

产生输出

System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double

在对 F 的第一次和最后一次调用中，F 的正常形式适用，因为参数类型到参数类型的隐式转换存在（两者都是 object[] 类型）。因此，重载解析选择 F 的正常形式，并且参数作为常规值参数传递。在第二次和第三次调用中，F 的正常形式不适用，因为参数类型到参数类型的隐式转换不存在（object 类型不能隐式转换为 object[] 类型）。然而，F 的扩展形式适用，因此被重载解析选中。结果，调用创建了一个包含一个元素的 object[]，并且数组的单个元素被初始化为给定的参数值（它本身是对 object[] 的引用）。结束示例

## 15.6.3 静态方法和实例方法

当方法声明包含 static 修饰符时，该方法称为静态方法。当没有 static 修饰符时，该方法称为实例方法。

静态方法不操作特定实例，并且在静态方法中引用 this 是编译时错误。

实例方法操作类的给定实例，并且该实例可以作为 this 访问（§12.7.8）。

静态成员和实例成员之间的差异在 §15.3.8 中进一步讨论。

## 15.6.4 虚拟方法

当实例方法声明包含 virtual 修饰符时，该方法称为虚拟方法。当没有 virtual 修饰符时，该方法称为非虚拟方法。

非虚拟方法的实现是不变的：无论方法是在声明它的类实例上调用，还是在派生类实例上调用，实现都相同。相比之下，虚拟方法的实现可以被派生类取代。将继承的虚拟方法的实现取代的过程称为重写该方法（§15.6.5）。

在虚拟方法调用中，进行该调用的实例的运行时类型决定了要调用的实际方法实现。在非虚拟方法调用中，实例的编译时类型是决定因素。精确地说，当在具有编译时类型 C 和运行时类型 R（其中 R 是 C 或派生自 C 的类）的实例上使用参数列表 A 调用名为 N 的方法时，调用按如下方式处理：

- 在绑定时，对 C、N 和 A 应用重载解析，以从声明于 C 中并由 C 继承的方法集合中选择特定方法 M。这在 §12.7.6.2 中描述。
- 然后在运行时：
  - 如果 M 是非虚拟方法，则调用 M。
  - 否则，M 是虚拟方法，并且相对于 R 调用 M 的最派生实现。

对于每个在类中声明或继承的虚拟方法，相对于该类都存在该方法的最派生实现。相对于类 R 的虚拟方法 M 的最派生实现按如下方式确定：

- 如果 R 包含 M 的引入虚拟声明，则这是相对于 R 的 M 的最派生实现。
- 否则，如果 R 包含 M 的重写，则这是相对于 R 的 M 的最派生实现。
- 否则，相对于 R 的 M 的最派生实现与相对于 R 的直接基类的 M 的最派生实现相同。

[示例：以下示例说明虚拟方法和非虚拟方法之间的差异：

```
using System;
class A
{
    public void F() { Console.WriteLine("A.F"); }
    public virtual void G() { Console.WriteLine("A.G"); }
}
class B: A
{
    new public void F() { Console.WriteLine("B.F"); };
    public override void G() { Console.WriteLine("B.G"); }
}
class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```

在示例中，A 引入了一个非虚拟方法 F 和一个虚拟方法 G。类 B 引入了一个新的非虚拟方法 F，从而隐藏了继承的 F，并且还重写了继承的方法 G。示例产生输出：

A.F
B.F
B.G
B.G

请注意，语句 a.G() 调用的是 B.G，而不是 A.G。这是因为实例的运行时类型（即 B），而不是实例的编译时类型（即 A），决定了要调用的实际方法实现。结束示例]

由于允许方法隐藏继承的方法，因此一个类可能包含多个具有相同签名的虚拟方法。这不会产生歧义问题，因为除最派生方法之外的所有方法都被隐藏。[示例：在以下代码中

```
using System;
class A
{
    public virtual void F() { Console.WriteLine("A.F"); }
}
class B: A
{
    public override void F() { Console.WriteLine("B.F"); }
}
class C: B
{
    new public virtual void F() { Console.WriteLine("C.F"); }
}
class D: C
{
    public override void F() { Console.WriteLine("D.F"); }
}
class Test
{
    static void Main() {
        D d = new D();
        A a = d;
        B b = d;
        C c = d;
        a.F();
        b.F();
        c.F();
        d.F();
    }
}
```

C 和 D 类包含两个具有相同签名的虚拟方法：一个由 A 引入，一个由 C 引入。C 引入的方法隐藏了从 A 继承的方法。因此，D 中的重写声明重写了 C 引入的方法，并且 D 不可能重写 A 引入的方法。示例产生输出：

B.F
B.F
D.F
D.F

请注意，可以通过通过未隐藏该方法的较少派生类型访问 D 的实例来调用隐藏的虚拟方法。结束示例]

## 15.6.5 重写方法

当实例方法声明包含 override 修饰符时，该方法称为重写方法。重写方法重写具有相同签名的继承的虚拟方法。虚拟方法声明引入新方法，而重写方法声明通过提供该方法的新实现来特化现有的继承虚拟方法。

由重写声明重写的方法称为被重写的基方法。对于在类 C 中声明的重写方法 M，被重写的基方法是通过检查 C 的每个基类来确定的，从 C 的直接基类开始，继续每个后续直接基类，直到在给定的基类类型中至少找到一个可访问的方法，该方法在替换类型参数后具有与 M 相同的签名。为了定位被重写的基方法，如果方法是 public、protected、protected internal，或者是 internal 且在与 C 相同的程序中声明，则认为该方法是可访问的。

除非重写声明满足以下所有条件，否则会发生编译时错误：

- 可以按照上述描述找到被重写的基方法。
- 恰好存在这样一个被重写的基方法。此限制仅在基类类型为构造类型且类型参数的替换使两个方法的签名相同的情况下才有效。
- 被重写的基方法是 virtual、abstract 或 override 方法。换句话说，被重写的基方法不能是 static 或非虚拟的。
- 被重写的基方法不是 sealed 方法。
- 被重写的基方法的返回类型与重写方法之间存在恒等转换。
- 重写声明和被重写的基方法具有相同的声明可访问性。换句话说，重写声明不能更改虚拟方法的可访问性。然而，如果被重写的基方法是 protected internal 并且它声明在与包含重写声明的程序集不同的程序集中，则重写声明的声明可访问性应为 protected。
- 重写声明不指定类型参数约束子句。相反，约束从被重写的基方法继承。被重写方法中为类型参数的约束可能被继承约束中的类型参数替换。这可能导致在显式指定时无效的约束，例如值类型或密封类型。

[示例：以下演示了泛型类的重写规则如何工作：

```csharp
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}
class D: C<string>
{
    public override string F() {...}       // ok
    public override C<string> G() {...}    // ok
    public override void H(C<T> x) {...}   // Error, should be C<string>
}
class E<T,U>: C<U>
{
    public override U F() {...}            // ok
    public override C<U> G() {...}         // ok
    public override void H(C<T> x) {...}   // Error, should be C<U>
}
```

结束示例]

重写声明可以使用 *基访问*（§12.7.9）访问被重写的基方法。[示例：在以下代码中

```csharp
class A
{
    int x;
    public virtual void PrintFields() {
        Console.WriteLine("x = {0}", x);
    }
}
class B: A
{
    int y;
```



```
public override void PrintFields() {
    base.PrintFields();
    Console.WriteLine("y = {0}", y);
}
```

B 中对 base.PrintFields() 的调用会调用在 A 中声明的 PrintFields 方法。base 访问会禁用虚拟调用机制，并简单地将基方法视为非虚拟方法。如果 B 中的调用被写成 ((A)this).PrintFields()，它将递归调用 B 中声明的 PrintFields 方法，而不是 A 中声明的方法，因为 PrintFields 是虚拟的，且 ((A)this) 的运行时类型是 B。结束示例

只有包含 override 修饰符的方法才能重写另一个方法。在所有其他情况下，与继承方法具有相同签名的 方法只是隐藏继承的方法。[示例：在以下代码中

```
class A
{
    public virtual void F() {}
}

class B : A
{
    public virtual void F() {}    // Warning, hiding inherited F()
}
```

B 中的 F 方法不包含 override 修饰符，因此不重写 A 中的 F 方法。相反，B 中的 F 方法隐藏了 A 中的方法，并且会报告警告，因为声明中不包含 new 修饰符。结束示例

[示例：在以下代码中

```
class A
{
    public virtual void F() {}
}
class B : A
{
    new private void F() {}        // Hides A.F within body of B
}
class C : B
{
    public override void F() {}    // Ok, overrides A.F
}
```

B 中的 F 方法隐藏了从 A 继承的虚拟 F 方法。由于 B 中的 new F 的访问权限为 private，其作用域仅包括 B 的类体，并不扩展到 C。因此，C 中对 F 的声明被允许重写从 A 继承的 F。结束示例

## 15.6.6 密封方法

当实例方法声明包含 sealed 修饰符时，该方法被称为密封方法。密封方法重写具有相同签名的继承的虚拟方法。密封方法也必须标记有 override 修饰符。使用 sealed 修饰符可防止派生类进一步重写该方法。

[示例：示例

```
using System;
class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }
}
public virtual void G() {
    Console.WriteLine("A.G");
}
}
class B: A
{
    public sealed override void F() {
        Console.WriteLine("B.F");
    }
    public override void G() {
        Console.WriteLine("B.G");
    }
}
class C: B
{
    public override void G() {
        Console.WriteLine("C.G");
    }
}
```

类 B 提供了两个重写方法：一个带有 sealed 修饰符的 F 方法和一个不带该修饰符的 G 方法。B 对 sealed 修饰符的使用阻止了 C 进一步重写 F。结束示例

## 15.6.7 抽象方法

当实例方法声明包含 abstract 修饰符时，该方法被称为抽象方法。虽然抽象方法隐式地也是一个虚拟方法，但它不能具有 virtual 修饰符。

抽象方法声明引入了一个新的虚拟方法，但并未提供该方法的实现。相反，非抽象派生类必须通过重写该方法来提供自己的实现。由于抽象方法不提供实际实现，抽象方法的方法体仅由一个分号组成。

抽象方法声明仅允许在抽象类中（§15.2.2.2）。

[示例：在以下代码中

```
public abstract class Shape
{
    public abstract void Paint(Graphics g, Rectangle r);
}
public class Ellipse: Shape
{
    public override void Paint(Graphics g, Rectangle r) {
        g.DrawEllipse(r);
    }
}
public class Box: Shape
{
    public override void Paint(Graphics g, Rectangle r) {
        g.DrawRect(r);
    }
}
```

Shape 类定义了可自行绘制的几何形状对象的抽象概念。Paint 方法是抽象的，因为没有有意义的默认实现。Ellipse 和 Box 类是具体的 Shape 实现。由于这些类是非抽象的，它们必须重写 Paint 方法并提供实际实现。结束示例

对抽象方法进行 base 访问（§12.7.9）是编译时错误。[示例：在以下代码中

```
[DllImport("kernel32", SetLastError=true)]
    static extern bool SetCurrentDirectory(string name);
}
```

*结束示例*

## 15.6.9 部分方法

当方法声明包含 partial 修饰符时，该方法被称为部分方法。部分方法只能声明为部分类型（§15.2.7）的成员，并受一系列限制。

部分方法可以在类型声明的一个部分中定义，并在另一部分中实现。实现是可选的；如果没有任何部分实现部分方法，则部分方法声明及其所有调用都将从组合各部分得到的类型声明中移除。

部分方法不得定义访问修饰符；它们隐式为 private。它们的返回类型必须为 void，且其参数不得具有 out 修饰符。标识符 partial 仅在方法声明中紧跟在 void 关键字之前时才被识别为上下文关键字（§7.4.4）。部分方法不能显式实现接口方法。

部分方法声明有两种类型：如果方法声明的主体是一个分号，则该声明被称为定义部分方法声明。如果主体以块形式给出，则该声明被称为实现部分方法声明。在类型声明的各部分中，对于给定的签名，只能有一个定义部分方法声明，并且只能有一个实现部分方法声明。如果给出了实现部分方法声明，则必须存在相应的定义部分方法声明，并且声明必须符合以下规定：

- 声明必须具有相同的修饰符（尽管顺序不一定相同）、方法名、类型参数数量和参数数量。
- 声明中对应的参数必须具有相同的修饰符（尽管顺序不一定相同）以及相同的类型（忽略类型参数名称的差异）。
- 声明中对应的类型参数必须具有相同的约束（忽略类型参数名称的差异）。

实现部分方法声明可以与相应的定义部分方法声明出现在同一部分中。

只有定义部分方法参与重载解析。因此，无论是否给出实现声明，调用表达式都可能解析为对部分方法的调用。由于部分方法始终返回 void，此类调用表达式始终是表达式语句。此外，由于部分方法隐式为 private，此类语句始终发生在声明该部分方法的类型声明的各部分之一之内。

如果部分类型声明的任何部分都不包含给定部分方法的实现声明，则调用它的任何表达式语句都将简单地从组合的类型声明中移除。因此，调用表达式，包括任何子表达式，在运行时没有任何效果。部分方法本身也被移除，不会成为组合类型声明的成员。

如果给定部分方法存在实现声明，则对部分方法的调用将被保留。部分方法会产生一个与实现部分方法声明类似的方法声明，但有以下例外：

- 不包含 partial 修饰符
- 结果方法声明中的属性是定义部分方法声明和实现部分方法声明的组合属性，顺序不确定。重复项不会被移除。



-   生成的方法声明的参数上的特性是定义部分方法和实现部分方法声明的对应参数的特性的组合，顺序不确定。重复项不会被移除。

如果为部分方法 M 提供了定义声明但未提供实现声明，则适用以下限制：

-   创建 M 的委托是编译时错误 (§12.7.11.6)。
-   在转换为表达式树类型的匿名函数内部引用 M 是编译时错误 (§9.6)。
-   作为 M 调用的组成部分出现的表达式不影响明确赋值状态 (§10.4)，这可能导致编译时错误。
-   M 不能作为应用程序的入口点 (§8.1)。

部分方法对于允许类型声明的一个部分自定义另一部分的行为很有用，例如由工具生成的部分。请考虑以下部分类声明：

```csharp
partial class Customer
{
    string name;
    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }
    partial void OnNameChanging(string newName);
    partial void OnNameChanged();
}
```

如果在没有其他部分的情况下编译此类，定义的部分方法声明及其调用将被移除， resulting combined class declaration 将等同于以下内容：

```csharp
class Customer
{
    string name;
    public string Name {
        get { return name; }
        set { name = value; }
    }
}
```

然而，假设提供了另一个部分，其中提供了部分方法的实现声明：

```csharp
partial class Customer
{
    partial void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }
    partial void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

那么 resulting combined class declaration 将等同于以下内容：

```
class Customer
{
    string name;
    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }
    void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }
    void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

## 15.6.10 扩展方法

当方法的第一个参数包含 this 修饰符时，该方法称为扩展方法。扩展方法只能在非泛型、非嵌套的静态类中声明。扩展方法的第一个参数除了 this 之外不得有其他修饰符，并且参数类型不能是指针类型。

[示例：以下是声明两个扩展方法的静态类的示例：]

```
public static class Extensions
{
    public static int ToInt32(this string s) {
        return Int32.Parse(s);
    }
    public static T[] Slice<T>(this T[] source, int index, int count) {
        if (index < 0 || count < 0 || source.Length - index < count)
            throw new ArgumentException();
        T[] result = new T[count];
        Array.Copy(source, index, result, 0, count);
        return result;
    }
}
```

示例结束

扩展方法是一个常规的静态方法。此外，当其封闭的静态类在作用域内时，扩展方法可以使用实例方法调用语法 (§12.7.6.3)进行调用，使用接收表达式作为第一个参数。

[示例：以下程序使用上面声明的扩展方法：]

```
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in strings.Slice(1, 2)) {
            Console.WriteLine(s.ToInt32());
        }
    }
}
```

Slice 方法在 string[] 上可用，ToInt32 方法在 string 上可用，因为它们已被声明为扩展方法。该程序的含义与以下使用普通静态方法调用的内容相同：

```
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in Extensions.Slice(strings, 1, 2)) {
            Console.WriteLine(Extensions.ToInt32(s));
        }
    }
}
```

示例结束

## 15.6.11 方法体

方法声明的方法体由块或分号组成。

抽象方法和外部方法声明不提供方法实现，因此它们的方法体仅由分号组成。对于任何其他方法，方法体是一个块 (§13.3)，其中包含在调用该方法时要执行的语句。

方法的有效返回类型为 void，如果返回类型为 void，或者方法为 async 且返回类型为 System.Threading.Tasks.Task。否则，非 async 方法的有效返回类型是其返回类型，而返回类型为 System.Threading.Tasks.Task<T> 的 async 方法的有效返回类型为 T。

当方法的有效返回类型为 void 时，该方法体中的 return 语句 (§13.10.5) 不允许指定表达式。如果 void 方法的方法体正常完成（即控制流离开方法体末尾），该方法 simply 返回给其调用者。

当方法的有效返回类型不是 void 时，该方法体中的每个 return 语句都应指定一个可隐式转换为有效返回类型的表达式。值返回方法的方法体终点不得可达。换句话说，在值返回方法中，不允许控制流离开方法体末尾。

[示例：在以下代码中

```
class A
{
    public int F() {}    // Error, return value required
    public int G() {
        return 1;
    }

    public int H(bool b) {
        if (b) {
            return 1;
        }
        else { return 0; }
    }
}
```

值返回的 F 方法导致编译时错误，因为控制可以流出方法体末尾。G 和 H 方法是正确的，因为所有可能的执行路径都以指定返回值的 return 语句结束。示例结束]

## 15.7 属性

### 15.7.1 通用

**属性** 是提供对对象或类的特征访问的成员。属性的示例包括字符串的长度、字体的大小、窗口的标题、客户的名称等等。属性是字段的自然扩展——两者都是具有关联类型的命名成员，并且访问字段和属性的语法相同。然而，与字段不同，属性不表示存储位置。相反，属性具有 **访问器**，它们指定在读取或写入其值时要执行的语句。因此，属性提供了一种将操作与对象特征的读取和写入关联起来的机制；此外，它们允许计算此类特征。

属性使用 *属性声明* 声明：

```
property-declaration:
    attributes_opt property-modifiers_opt type member-name { accessor-declarations }

property-modifiers:
    property-modifier
    property-modifiers property-modifier

property-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern
```

一个 *属性声明* 可能包含一组 *特性* (§22) 以及四个访问修饰符 (§15.3.6) 的有效组合，*new* (§15.3.5)、*static* (§15.7.2)、*virtual* (§15.6.4, §15.7.6)、*override* (§15.6.5, §15.7.6)、*sealed* (§15.6.6)、*abstract* (§15.6.7, §15.7.6) 和 *extern* (§15.6.8) 修饰符。

属性声明在修饰符的有效组合方面受与方法声明 (§15.6) 相同的规则约束。

属性声明的 *类型* 指定声明引入的属性的类型，而 *成员名* (§15.6.1) 指定属性的名称。除非属性是显式接口成员实现，否则 *成员名* 只是 *标识符*。对于显式接口成员实现 (§18.6.2)，*成员名* 由 *接口类型* 后跟一个 “.” 和一个 *标识符* 组成。

属性的 *类型* 必须至少与属性本身一样可访问 (§8.5.5)。

*访问器声明*，应被 “{” 和 “}” 标记括起来，声明属性的访问器 (§15.7.3)。访问器指定与读取和写入属性相关联的可执行语句。

即使访问属性的语法与访问字段的语法相同，属性也不被归类为变量。因此，不可能将属性作为 ref 或 out 参数传递。

当属性声明包含 *extern* 修饰符时，该属性称为 *外部属性*。由于外部属性声明不提供实际实现，其每个 *访问器声明* 都由分号组成。




## 15.7.2 静态属性和实例属性

当属性声明包含 `static` 修饰符时，该属性称为静态属性。当不存在 `static` 修饰符时，该属性称为实例属性。

静态属性不与特定实例关联，在静态属性的访问器中引用 `this` 是编译时错误。

实例属性与类的给定实例关联，在该属性的访问器中可以通过 `this`（§12.7.8）访问该实例。

静态成员与实例成员之间的区别在 §15.3.8 中进一步讨论。

## 15.7.3 访问器

属性声明的访问器声明指定了与该属性读写相关的可执行语句。

```
accessor-declarations:
    get-accessor-declaration  set-accessor-declarationopt
    set-accessor-declaration  get-accessor-declarationopt

get-accessor-declaration:
    attributesopt accessor-modifieropt get accessor-body

set-accessor-declaration:
    attributesopt accessor-modifieropt set accessor-body

accessor-modifier:
    protected
    internal
    private
    protected internal
    internal protected

accessor-body:
    block
    ;
```

访问器声明由一个 `get` 访问器声明、一个 `set` 访问器声明，或两者共同组成。每个访问器声明由可选的特性、可选的访问器修饰符、`get` 或 `set` 标记，以及随后的访问器主体组成。

访问器修饰符的使用受以下限制约束：

- 在接口或显式接口成员实现中不得使用访问器修饰符。
- 对于没有 `override` 修饰符的属性或索引器，仅当该属性或索引器同时具有 `get` 和 `set` 访问器时，才允许使用访问器修饰符，并且仅允许应用于其中一个访问器。
- 对于包含 `override` 修饰符的属性或索引器，访问器的访问器修饰符（如果有）必须与被重写的访问器的访问器修饰符匹配。
- 访问器修饰符声明的可访问性必须严格低于属性或索引器本身声明的可访问性。具体而言：
  - 如果属性或索引器声明的可访问性为 `public`，则访问器修饰符可以是 `protected internal`、`internal`、`protected` 或 `private`。
  - 如果属性或索引器声明的可访问性为 `protected internal`，则访问器修饰符可以是 `internal`、`protected` 或 `private`。
  - 如果属性或索引器声明的可访问性为 `internal` 或 `protected`，则访问器修饰符必须是 `private`。
- 如果属性或索引器声明的可访问性为 `private`，则不得使用任何访问器修饰符。

对于抽象属性和外部属性，每个指定访问器的访问器主体仅为一个分号。

非抽象、非外部属性可以是自动实现的属性，此时必须同时提供 `get` 和 `set` 访问器，且两者的主体均为分号（§15.7.4）。对于任何其他非抽象、非外部属性的访问器，访问器主体是一个块，用于指定调用相应访问器时执行的语句。

`get` 访问器对应于一个无参数方法，其返回值为属性类型。除非作为赋值的目标，当属性在表达式中被引用时，会调用该属性的 `get` 访问器来计算属性的值（§12.2.2）。`get` 访问器的主体必须符合 §15.6.11 中描述的返回值方法的规则。特别是，`get` 访问器主体中的所有 `return` 语句都必须指定一个可隐式转换为属性类型的表达式。此外，`get` 访问器的终结点不得可达。

`set` 访问器对应于一个具有单个属性类型值参数且返回类型为 `void` 的方法。`set` 访问器的隐式参数始终命名为 `value`。当属性被引用为赋值的目标（§12.18），或作为 `++` 或 `--` 的操作数（§12.7.10、12.8.6）时，将调用 `set` 访问器，并传入提供新值的参数（§12.18.2）。`set` 访问器的主体必须符合 §15.6.11 中描述的 `void` 方法的规则。特别是，`set` 访问器主体中的 `return` 语句不允许指定表达式。由于 `set` 访问器隐式具有名为 `value` 的参数，因此在 `set` 访问器中声明同名的局部变量或常量属于编译时错误。

根据 `get` 和 `set` 访问器的存在与否，属性分类如下：

- 同时包含 `get` 访问器和 `set` 访问器的属性称为读写属性。
- 仅包含 `get` 访问器的属性称为只读属性。将只读属性作为赋值目标是编译时错误。
- 仅包含 `set` 访问器的属性称为只写属性。除非作为赋值的目标，在表达式中引用只写属性属于编译时错误。[注：前缀和后缀的 `++` 和 `--` 运算符以及复合赋值运算符不能应用于只写属性，因为这些运算符在写入新值之前会读取操作数的旧值。注释结束]

[示例：在以下代码中

```
public class Button: Control
{
    private string caption;
    public string Caption {
        get {
            return caption;
        }
        set {
            if (caption != value) {
                caption = value;
                Repaint();
            }
        }
    }
    public override void Paint(Graphics g, Rectangle r) {
    } // Painting code goes here
}
```

`Button` 控件声明了一个公共的 `Caption` 属性。`Caption` 属性的 `get` 访问器返回存储在私有 `caption` 字段中的字符串。`set` 访问器检查新值是否与当前值不同，如果不同，则存储新值并重绘控件。属性通常遵循上述模式：`get` 访问器仅返回存储在私有字段中的值，而 `set` 访问器修改该私有字段，然后执行任何必要的附加操作以完全更新对象的状态。

给定上述 `Button` 类，以下是使用 `Caption` 属性的示例：

```
Button okButton = new Button();  // Invokes set accessor
okButton.Caption = "OK";
string s = okButton.Caption;       // Invokes get accessor
```

此处，通过向属性赋值来调用 `set` 访问器，通过在表达式中引用属性来调用 `get` 访问器。示例结束]

属性的 `get` 和 `set` 访问器不是不同的成员，并且不能单独声明属性的访问器。[示例：以下示例

```
class A
{
    private string name;
    public string Name {
        get { return name; }      // Error, duplicate member name
    }
    public string Name {
        set { name = value; }     // Error, duplicate member name
    }
}
```

并未声明单个读写属性。相反，它声明了两个同名的属性，一个只读，一个只写。由于同一类中声明的两个成员不能同名，因此该示例会导致编译时错误。示例结束]

当派生类声明的属性与继承的属性同名时，派生属性会在读取和写入两方面隐藏继承的属性。[示例：在以下代码中

```
class A
{
    public int P {
        set {...}
    }
}
class B: A
{
    new public int P {
        get {...}
    }
}
```

`B` 中的 `P` 属性在读取和写入两方面隐藏了 `A` 中的 `P` 属性。因此，在语句

```
B b = new B();
b.P = 1;    // Error, B.P is read-only
((A)b).P = 1;   // Ok, reference to A.P
```

中，对 `b.P` 的赋值会导致编译时错误，因为 `B` 中的只读 `P` 属性隐藏了 `A` 中的只写 `P` 属性。但请注意，可以使用强制转换来访问被隐藏的 `P` 属性。示例结束]

与公共字段不同，属性提供了对象内部状态与其公共接口之间的分离。[示例：考虑以下使用 `Point` 结构表示位置的代码：

```
class Label
{
    private int x, y;
    private string caption;
```


```csharp
public Label(int x, int y, string caption) {
    this.x = x;
    this.y = y;
    this.caption = caption;
}
public int X {
    get { return x; }
}
public int Y {
    get { return y; }
}
public Point Location {
    get { return new Point(x, y); }
}
public string Caption {
    get { return caption; }
}
}
```

这里，`Label` 类使用两个 `int` 字段 `x` 和 `y` 来存储其位置。该位置通过一个 `x` 属性和一个 `Y` 属性，以及一个 `Point` 类型的 `Location` 属性公开暴露。如果在未来版本的 `Label` 中，内部将位置存储为 `Point` 变得更方便，那么可以在不影响该类的公共接口的情况下进行此更改：

```csharp
class Label
{
    private Point location;
    private string caption;
    public Label(int x, int y, string caption) {
        this.location = new Point(x, y);
        this.caption = caption;
    }
    public int X {
        get { return location.x; }
    }
    public int Y {
        get { return location.y; }
    }
    public Point Location {
        get { return location; }
    }
    public string Caption {
        get { return caption; }
    }
}
```

如果 `x` 和 `y` 改为 `public readonly` 字段，那么就不可能对 `Label` 类做出这样的更改。*示例结束*

> > [注意：通过属性公开状态不一定比直接公开字段效率更低。特别是，当属性是非虚的且只包含少量代码时，执行环境可能会用访问器的实际代码替换对访问器的调用。此过程称为*内联*，它使属性访问与字段访问一样高效，同时保留了属性更高的灵活性。*注释结束*]

[示例：由于调用 `get` 访问器在概念上等价于读取字段的值，因此 `get` 访问器产生可观察的副作用被认为是一种糟糕的编程风格。在下面的示例中

```csharp
class Counter
{
    private int next;
}
```

~~~csharp
public int Next {
    get { return next++; }
}
~~~

Next 属性的值取决于之前访问该属性的次数。因此，访问该属性会产生可观察的副作用，该属性应改为通过方法实现。

`get` 访问器的“无副作用”约定并不意味着 `get` 访问器应始终只编写为返回存储在字段中的值。实际上，`get` 访问器通常通过访问多个字段或调用方法来计算属性的值。但是，设计良好的 `get` 访问器不会执行任何导致对象状态发生可观察更改的操作。示例结束]

属性可用于将资源的初始化延迟到首次引用它的时刻。[示例：

~~~csharp
using System.IO;
public class Console
{
    private static TextReader reader;
    private static TextWriter writer;
    private static TextWriter error;

    public static TextReader In {
        get {
            if (reader == null) {
                reader = new StreamReader(Console.OpenStandardInput());
            }
            return reader;
        }
    }

    public static TextWriter Out {
        get {
            if (writer == null) {
                writer = new StreamWriter(Console.OpenStandardOutput());
            }
            return writer;
        }
    }

    public static TextWriter Error {
        get {
            if (error == null) {
                error = new StreamWriter(Console.OpenStandardError());
            }
            return error;
        }
    }
} ...
~~~

`Console` 类包含三个属性：`In`、`Out` 和 `Error`，分别表示标准输入、标准输出和标准错误设备。通过将这些成员公开为属性，`Console` 类可以将其初始化延迟到实际使用时。例如，在首次引用 `Out` 属性时，如下所示

~~~csharp
Console.Out.WriteLine("hello, world");
~~~

则会创建输出设备的基础 `TextWriter`。但是，如果应用程序未引用 In 和 Error 属性，则不会为这些设备创建任何对象。示例结束]

## 15.7.4 自动实现的属性

当属性被指定为自动实现的属性时，会自动为该属性提供一个隐藏的支持字段，并且访问器被实现为读取和写入该支持字段。隐藏的支持字段不可访问，只能通过自动实现的属性访问器读取和写入，即使在包含类型内部也是如此。

*[示例：*

```csharp
public class Point {
    public int X { get; set; }   // automatically implemented
    public int Y { get; set; }   // automatically implemented
}
```

等价于以下声明：

```csharp
public class Point {
    private int x;
    private int y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

*示例结束]*

由于支持字段不可访问，自动实现的只读或只写属性没有意义，因此是不允许的。但是，可以分别以不同方式设置每个访问器的访问级别。因此，可以像下面这样模拟具有私有支持字段的只读属性的效果：

```csharp
public class ReadOnlyPoint {
    public int X { get; private set; }
    public int Y { get; private set; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```

### 15.7.5 可访问性

如果访问器具有*访问器修饰符*，则使用*访问器修饰符*的声明可访问性来确定该访问器的可访问域（§8.5.3）。如果访问器没有*访问器修饰符*，则根据属性或索引器的声明可访问性确定该访问器的可访问域。

*访问器修饰符*的存在绝不影响成员查找（§12.5）或重载决策（§12.6.4）。无论访问的上下文如何，属性或索引器上的修饰符始终决定绑定到哪个属性或索引器。

一旦选择了特定的属性或索引器，就会使用所涉及的特定访问器的可访问域来确定该用法是否有效：

- 如果该用法是作为值（§12.2.2），则 get 访问器必须存在且可访问。
- 如果该用法是作为简单赋值（§18.2.2）的目标，则 set 访问器必须存在且可访问。
- 如果该用法是作为复合赋值（§12.18.3）的目标，或作为 ++ 或 -- 运算符（§12.7.10、§12.8.6）的目标，则 get 访问器和 set 访问器都必须存在且可访问。

[示例：在以下示例中，属性 A.Text 被属性 B.Text 隐藏，即使在只调用 set 访问器的上下文中也是如此。相反，类 M 无法访问属性 B.Count，因此改为使用可访问的属性 A.Count。

```csharp
class A
{
    public string Text {
        get { return "hello"; }
        set { }
    }
}
```

~~~
        public int Count {
            get { return 5; }
            set { }
        }
    }
class B: A
{
    private string text = "goodbye";
    private int count = 0;

    new public string Text {
        get { return text; }
        protected set { text = value; }
    }

    new protected int Count {
        get { return count; }
        set { count = value; }
    }
}
class M
{
    static void Main() {
        B b = new B();
        b.Count = 12;           // Calls A.Count set accessor
        int i = b.Count;        // Calls A.Count get accessor
        b.Text = "howdy";       // Error, B.Text set accessor not accessible
        string s = b.Text;      // Calls B.Text get accessor
    }
}
~~~

示例结束]

用于实现接口的访问器不得具有*访问器修饰符*。如果只有一个访问器用于实现接口，则另一个访问器可以用*访问器修饰符*声明：

*[示例：*

~~~
    public interface I
    {
        string Prop { get; }
    }

    public class C: I
    {
        public string Prop {
            get { return "April"; } // Must not have a modifier here
            internal set { ... }    // Ok, because I.Prop has no set accessor
        }
    }
~~~

*示例结束]*

### 15.7.6 虚拟、密封、重写和抽象访问器

虚拟属性声明指定该属性的访问器是虚拟的。virtual 修饰符适用于属性的所有非私有访问器。当虚拟属性的访问器具有 private *访问器修饰符*时，该私有访问器隐式不是虚拟的。

抽象属性声明指定该属性的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写该属性来为访问器提供自己的实现。由于抽象属性声明的访问器不提供实际实现，其访问器体仅由一个分号组成。抽象属性不得具有私有访问器。

同时包含 abstract 和 override 修饰符的属性声明指定该属性是抽象的，并重写基属性。这种属性的访问器也是抽象的。





抽象属性声明仅允许出现在抽象类中（§15.2.2.2）。在派生类中，可以通过包含指定 override 指令的属性声明来重写继承的虚拟属性的访问器。这称为重写属性声明。重写属性声明不会声明新属性，而只是对现有虚拟属性的访问器实现进行特化。

重写属性声明应指定与继承属性完全相同的可访问性修饰符和名称，并且重写属性的类型与继承属性的类型之间应存在标识转换。如果继承属性只有一个访问器（即继承属性是只读或只写的），则重写属性只能包含该访问器。如果继承属性包含两个访问器（即继承属性是读写的），则重写属性可以包含单个访问器，也可以同时包含两个访问器。

重写属性声明可以包含 sealed 修饰符。使用该修饰符可防止派生类进一步重写该属性。sealed 属性的访问器也是 sealed 的。

除了声明和调用语法上的差异之外，virtual、sealed、override 和 abstract 访问器的行为与 virtual、sealed、override 和 abstract 方法完全相同。具体来说，§15.6.4、§15.6.5、§15.6.6 和 §15.6.7 中描述的规则同样适用，就好像访问器是相应形式的方法一样：

-   get 访问器对应于一个无参数方法，返回值为属性类型，并具有与所属属性相同的修饰符。
-   set 访问器对应于一个具有单个属性类型值参数、void 返回类型，并具有与所属属性相同的修饰符的方法。

[示例：在以下代码中

```
abstract class A
{
    int y;
    public virtual int X {
        get { return 0; }
    }
    public virtual int Y {
        get { return y; }
        set { y = value; }
    }
    public abstract int Z { get; set; }
}
```

X 是虚拟只读属性，Y 是虚拟读写属性，Z 是抽象读写属性。由于 Z 是抽象的，包含类 A 也必须声明为抽象。

下面显示了从 A 派生的类：

```
class B: A
{
    int z;
    public override int X {
        get { return base.X + 1; }
    }
    public override int Y {
        set { base.Y = value < 0 ? 0 : value; }
    }
    public override int Z {
        get { return z; }
        set { z = value; }
    }
}
```

这里，X、Y 和 Z 的声明都是重写属性声明。每个属性声明都与相应继承属性的可访问性修饰符、类型和名称完全匹配。X 的 get 访问器和 Y 的 set 访问器使用 base 关键字来访问继承的访问器。Z 的声明重写了两个抽象访问器——因此，B 中没有未实现的抽象函数成员，B 允许是非抽象类。示例结束]

当属性被声明为 override 时，任何被重写的访问器都应能被重写代码访问。此外，属性或索引器本身以及访问器的声明可访问性，都必须与被重写的成员和访问器的声明可访问性匹配。

[示例：

```
public class B
{
    public virtual int P {
        protected set {...}
        get {...}
    }
}
public class D: B
{
    public override int P {
        protected set {...}    // Must specify protected here
        get {...}              // Must not have a modifier here
    }
}
```

示例结束]

## 15.8 事件

### 15.8.1 概述

事件是一种成员，它使对象或类能够提供通知。客户端可以通过提供事件处理程序来为事件附加可执行代码。

事件使用事件声明（event-declarations）声明：

```
event-declaration:
    attributesopt event-modifiersopt event type variable-declarators ;
    attributesopt event-modifiersopt event type member-name
    { event-accessor-declarations }

event-modifiers:
    event-modifier
    event-modifiers event-modifier

event-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern

event-accessor-declarations:
    add-accessor-declaration remove-accessor-declaration
    remove-accessor-declaration add-accessor-declaration

add-accessor-declaration:
    attributesopt add block

remove-accessor-declaration:
    attributesopt remove block
```

事件声明可以包含一组特性（§22）以及四个访问修饰符（§15.3.6）、new（§15.3.5）、static（§15.6.3, §15.8.4）、virtual（§15.6.4, §15.8.5）、override（§15.6.5, §15.8.5）、sealed（§15.6.6）、abstract（§15.6.7, §15.8.5）和 extern（§15.6.8）修饰符的有效组合。

在修饰符的有效组合方面，事件声明遵循与方法声明（§15.6）相同的规则。

事件声明的类型应为委托类型（§9.2.8），并且该委托类型的可访问性应至少与事件本身（§8.5.5）相同。

事件声明可以包含事件访问器声明（event-accessor-declarations）。但是，如果未包含，对于非 extern、非 abstract 事件，编译器应自动提供它们（§15.8.2）；对于 extern 事件，访问器由外部提供。

省略 event-accessor-declarations 的事件声明会定义一个或多个事件——每个变量声明符（variable-declarator）对应一个事件。特性和修饰符适用于此类事件声明所声明的所有成员。

事件声明同时包含 abstract 修饰符和 event-accessor-declarations 是编译时错误。

当事件声明包含 extern 修饰符时，该事件称为外部事件。由于外部事件声明不提供实际实现，因此它同时包含 extern 修饰符和 event-accessor-declarations 是错误的。

带有 abstract 或 extern 修饰符的事件声明的变量声明符包含变量初始化器是编译时错误。

事件可以用作 += 和 -= 运算符的左操作数。这两个运算符分别用于向事件附加事件处理程序或从事件移除事件处理程序，并且事件的访问修饰符控制允许此类操作的上下文。

对于声明该事件的类型之外的代码，允许对事件执行的操作只有 += 和 -=。因此，此类代码虽然可以为事件添加和移除处理程序，但不能直接获取或修改底层的事件处理程序列表。

在 x += y 或 x -= y 形式的操作中，当 x 是事件时，操作结果的类型为 void（§12.18.4）（而不是像对非事件类型定义的其他 += 和 -= 运算符那样，具有 x 的类型，并返回赋值后 x 的值）。这可以防止外部代码间接检查事件的底层委托。

[示例：以下示例演示如何将事件处理程序附加到 Button 类的实例：]

```
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
}
public class LoginDialog: Form
{
    Button okButton;
    Button cancelButton;

    public LoginDialog() {
        okButton = new Button(...);
        okButton.Click += new EventHandler(OkButtonClick);
        cancelButton = new Button(...);
        cancelButton.Click += new EventHandler(CancelButtonClick);
    }
    void OkButtonClick(object sender, EventArgs e) {
        // Handle okButton.Click event
    }
    void CancelButtonClick(object sender, EventArgs e) {
        // Handle cancelButton.Click event
    }
}
```

这里，LoginDialog 实例构造函数创建了两个 Button 实例，并将事件处理程序附加到 Click 事件。示例结束

### 15.8.2 类似字段的事件

在包含事件声明的类或结构体的程序文本中，某些事件可以像字段一样使用。要以这种方式使用，事件不得是 abstract 或 extern，也不得显式包含 event-accessor-declarations。此类事件可以在任何允许字段的上下文中使用。该字段包含一个委托（§20），该委托引用已添加到事件的事件处理程序列表。如果未添加任何事件处理程序，该字段包含 null。

[示例：在以下代码中

```
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
    protected void OnClick(EventArgs e) {
        EventHandler handler = Click;
        if (handler != null)
            handler(this, e);
    }
    public void Reset() {
        Click = null;
    }
}
```

在 Button 类中，Click 被用作字段。如示例所示，该字段可以被检查、修改，并用于委托调用表达式。Button 类中的 OnClick 方法“引发”Click 事件。引发事件的概念与调用事件所表示的委托完全等价——因此，没有用于引发事件的特殊语言构造。请注意，委托调用之前会进行一项检查以确保委托非 null，并且该检查是在局部副本上进行的，以确保线程安全。

在 Button 类声明之外，Click 成员只能用在 += 和 -= 运算符的左侧，例如 `b.Click += new EventHandler(...);` 会将委托追加到 Click 事件的调用列表，而 `b.Click -= new EventHandler(...);` 会将委托从 Click 事件的调用列表中移除。示例结束

在编译类似字段的事件时，编译器会自动创建用于保存委托的存储，并为事件创建访问器，以便向委托字段添加或移除事件处理程序。添加和移除操作是线程安全的，并且可以（但不是必须）在持有锁的情况下执行。




（§10.4.4.19）对于实例事件，位于包含该事件的对象上；对于静态事件，位于类型对象（§12.7.11.7）上。

[注意：因此，如下形式的实例事件声明：

```
class X
{
    public event D Ev;
}
```

应编译为与以下代码等效的内容：

```
class X
{
    private D __Ev; // field to hold the delegate
    public event D Ev {
        add {
            /* add the delegate in a thread safe way */
        }
        remove {
            /* remove the delegate in a thread safe way */
        }
    }
}
```

在类 X 内部，对 Ev 的 += 和 -= 运算符左侧的引用会导致调用 add 和 remove 访问器。对 Ev 的所有其他引用则编译为引用隐藏字段 __Ev（§12.7.5）。名称“__Ev”是任意的；隐藏字段可以具有任何名称，也可以完全没有名称。结束注意

## 15.8.3 事件访问器

[注意：事件声明通常会省略事件访问器声明，如上面的 Button 示例。例如，如果每个事件一个字段的存储成本不可接受，则可能会包含它们。在这种情况下，类可以包含事件访问器声明，并使用私有机制存储事件处理程序列表。结束注意]

事件的事件访问器声明指定与添加和移除事件处理程序相关联的可执行语句。

访问器声明由一个添加访问器声明和一个移除访问器声明组成。每个访问器声明由 add 或 remove 标记后跟一个块组成。与添加访问器声明关联的块指定添加事件处理程序时要执行的语句，与移除访问器声明关联的块指定移除事件处理程序时要执行的语句。

每个添加访问器声明和移除访问器声明对应于一个方法，该方法具有一个事件类型的值参数和一个 void 返回类型。事件访问器的隐式参数名为 value。在事件赋值中使用事件时，会使用相应的事件访问器。具体而言，如果赋值运算符是 +=，则使用 add 访问器；如果赋值运算符是 -=，则使用 remove 访问器。无论哪种情况，赋值运算符的右操作数都用作事件访问器的实参。添加访问器声明或移除访问器声明的块应符合 §15.6.9 中描述的 void 方法规则。特别是，此类块中的 return 语句不允许指定表达式。

由于事件访问器隐式具有名为 value 的参数，因此在事件访问器中声明的局部变量或常量使用该名称会导致编译时错误。

[示例：在以下代码中

```
class Control: Component
{
    // Unique keys for events
    static readonly object mouseDownEventKey = new object();
    static readonly object mouseUpEventKey = new object();
    // Return event handler associated with key
    protected Delegate GetEventHandler(object key) {...}
    // Add event handler associated with key
    protected void AddEventHandler(object key, Delegate handler) {...}
    // Remove event handler associated with key
    protected void RemoveEventHandler(object key, Delegate handler) {...}
    // MouseDown event
    public event MouseEventHandler MouseDown {
        add { AddEventHandler(mouseDownEventKey, value); }
        remove { RemoveEventHandler(mouseDownEventKey, value); }
    }
    // MouseUp event
    public event MouseEventHandler MouseUp {
        add { AddEventHandler(mouseUpEventKey, value); }
        remove { RemoveEventHandler(mouseUpEventKey, value); }
    }
    // Invoke the MouseUp event
    protected void OnMouseUp(MouseEventArgs args) {
        MouseEventHandler handler;
        handler = (MouseEventHandler)GetEventHandler(mouseUpEventKey);
        if (handler != null)
            handler(this, args);
    }
}
```

Control 类为事件实现了一种内部存储机制。AddEventHandler 方法将委托值与键关联，GetEventHandler 方法返回当前与键关联的委托，RemoveEventHandler 方法移除作为指定事件的事件处理程序的委托。据推测，底层存储机制的设计使得将 null 委托值与键关联不会产生成本，因此未处理的事件不消耗存储空间。结束示例

## 15.8.4 静态事件和实例事件

当事件声明包含 static 修饰符时，该事件称为静态事件。当不存在 static 修饰符时，该事件称为实例事件。

静态事件不与特定实例关联，并且在静态事件的访问器中引用 this 是编译时错误。

实例事件与类的给定实例关联，并且在该事件的访问器中可以通过 this（§12.7.8）访问此实例。

静态成员和实例成员之间的差异在 §15.3.8 中进一步讨论。

## 15.8.5 虚拟、密封、重写和抽象访问器

虚拟事件声明指定该事件的访问器是虚拟的。virtual 修饰符适用于事件的两个访问器。

抽象事件声明指定该事件的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写该事件来为访问器提供自己的实现。由于抽象事件声明的访问器不提供实际实现，因此它不应提供事件访问器声明。

同时包含 abstract 和 override 修饰符的事件声明指定该事件是抽象的，并重写一个基事件。此类事件的访问器也是抽象的。

抽象事件声明只允许在抽象类中（§15.2.2.2）。

继承的虚拟事件的访问器可以在派生类中通过包含指定 override 修饰符的事件声明来重写。这称为重写事件声明。重写事件声明不声明新事件。相反，它只是特化现有虚拟事件的访问器的实现。

重写事件声明应指定与被重写事件完全相同的可访问性修饰符和名称，重写事件与被重写事件的类型之间应存在恒等转换，并且声明中应同时指定 add 和 remove 访问器。

重写事件声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该事件。密封事件的访问器也是密封的。

重写事件声明包含 new 修饰符是编译时错误。

除了声明和调用语法上的差异外，虚拟、密封、重写和抽象访问器的行为与虚拟、密封、重写和抽象方法完全相同。具体而言，§15.6.4、§15.6.5、§15.6.6 和 §15.6.7 中描述的规则适用，就像访问器是相应形式的方法一样。每个访问器对应于一个方法，该方法具有一个事件类型的值参数、一个 void 返回类型，以及与包含该事件的事件相同的修饰符。

## 15.9 索引器

索引器是一种成员，它使对象能够以与数组相同的方式进行索引。索引器使用索引器声明来声明：

```
indexer-declaration:
    attributesopt indexer-modifiersopt indexer-declarator { accessor-declarations }

indexer-modifiers:
    indexer-modifier
    indexer-modifiers indexer-modifier

indexer-modifier:
    new
    public
    protected
    internal
    private
    virtual
    sealed
    override
    abstract
    extern

indexer-declarator:
    type this [ formal-parameter-list ]
    type interface-type . this [ formal-parameter-list ]
```

索引器声明可以包含一组特性（§22）以及四个访问修饰符（§15.3.6）、new（§15.3.5）、virtual（§15.6.4）、override（§15.6.5）、sealed（§15.6.6）、abstract（§15.6.7）和 extern（§15.6.8）修饰符的有效组合。

就修饰符的有效组合而言，索引器声明受与方法声明（§15.6）相同的规则约束，唯一例外是索引器声明上不允许使用 static 修饰符。

virtual、override 和 abstract 修饰符互斥，但有一种情况例外。abstract 和 override 修饰符可以一起使用，以便抽象索引器可以重写虚拟索引器。




索引器声明的类型指定了该声明引入的索引器的元素类型。除非索引器是显式接口成员实现，否则类型后面跟关键字 `this`。对于显式接口成员实现，类型后面依次跟接口类型、一个“.”和关键字 `this`。与其他成员不同，索引器没有用户定义的名称。

形式参数列表指定索引器的参数。索引器的形式参数列表与方法的形式参数列表（§15.6.2）相对应，但必须至少指定一个参数，并且不允许使用 `this`、`ref` 和 `out` 参数修饰符。

索引器的类型以及形式参数列表中引用的每个类型，其可访问性都不得低于索引器本身（§8.5.5）。

访问器声明（§15.7.3）必须包含在“{”和“}”标记中，用于声明索引器的访问器。访问器指定了与读取和写入索引器元素相关联的可执行语句。

尽管访问索引器元素的语法与访问数组元素的语法相同，但索引器元素不被归类为变量。因此，无法将索引器元素作为 `ref` 或 `out` 参数传递。

索引器的形式参数列表定义了索引器的签名（§8.6）。具体来说，索引器的签名由其形式参数的数量和类型组成。元素类型以及形式参数的名称不属于索引器签名的一部分。

索引器的签名必须不同于同一类中声明的所有其他索引器的签名。

索引器和属性在概念上非常相似，但存在以下差异：

- 属性通过其名称进行标识，而索引器通过其签名进行标识。
- 属性通过简单名称（§12.7.3）或成员访问（§12.7.5）进行访问，而索引器元素通过元素访问（§12.7.7.3）进行访问。
- 属性可以是静态成员，而索引器始终是实例成员。
- 属性的 `get` 访问器对应于一个不带参数的方法，而索引器的 `get` 访问器对应于一个与索引器具有相同形式参数列表的方法。
- 属性的 `set` 访问器对应于一个带有单个名为 `value` 的参数的方法，而索引器的 `set` 访问器对应于一个带有与索引器相同的形式参数列表以及一个额外的名为 `value` 的参数的方法。
- 如果索引器访问器声明了一个与索引器参数同名的局部变量或局部常量，则会产生编译时错误。
- 在重写属性声明中，使用语法 `base.P` 访问继承的属性，其中 `P` 是属性名称。在重写索引器声明中，使用语法 `base[E]` 访问继承的索引器，其中 `E` 是以逗号分隔的表达式列表。

除上述差异外，§15.7.3 和 §15.7.6 中定义的所有规则同样适用于索引器访问器和属性访问器。

当索引器声明包含 `extern` 修饰符时，该索引器称为外部索引器。由于外部索引器声明不提供实际实现，因此其每个访问器声明都由分号组成。

[示例：下面的示例声明了一个 `BitArray` 类，该类实现了一个用于访问位数组中各个位的索引器。

```
using System;
class BitArray
{
    int[] bits;
    int length;
```
```csharp
public BitArray(int length) {
    if (length < 0) throw new ArgumentException();
    bits = new int[((length - 1) >> 5) + 1];
    this.length = length;
}
public int Length {
    get { return length; }
}
public bool this[int index] {
    get {
        if (index < 0 || index >= length) {
            throw new IndexOutOfRangeException();
        }
        return (bits[index >> 5] & 1 << index) != 0;
    }
    set {
        if (index < 0 || index >= length) {
            throw new IndexOutOfRangeException();
        }
        if (value) {
            bits[index >> 5] |= 1 << index;
        }
        else {
            bits[index >> 5] &= ~(1 << index);
        }
    }
}
```
```

`BitArray` 类的实例所占用的内存明显少于相应的 `bool[]`（因为前者的每个值只占一位，而后者的每个值占一个字节），但它支持与 `bool[]` 相同的操作。

下面的 `CountPrimes` 类使用 `BitArray` 和经典的“筛法”算法，计算 2 与给定最大值之间的素数数量：

```
```csharp
class CountPrimes
{
    static int Count(int max) {
        BitArray flags = new BitArray(max + 1);
        int count = 0;
        for (int i = 2; i <= max; i++) {
            if (!flags[i]) {
                for (int j = i * 2; j <= max; j += i) flags[j] = true;
                count++;
            }
        }
        return count;
    }
    static void Main(string[] args) {
        int max = int.Parse(args[0]);
        int count = Count(max);
        Console.WriteLine(
            "Found {0} primes between 2 and {1}", count, max);
    }
}
```
```

请注意，访问 `BitArray` 元素的语法与访问 `bool[]` 元素的语法完全相同。结束示例]

[示例：以下示例展示了一个 26×10 的网格类，该类具有一个带两个参数的索引器。第一个参数必须是 A-Z 范围内的大写或小写字母，第二个参数必须是 0–9 范围内的整数。

```
```csharp
using System;
```
```
class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;
    int[,] cells = new int[NumRows, NumCols];

    public int this[char row, int col]
    {
        get {
            row = Char.ToUpper(row);
            if (row < 'A' || row > 'Z') {
                throw new ArgumentOutOfRangeException("row");
            }
            if (col < 0 || col >= NumCols) {
                throw new ArgumentOutOfRangeException ("col");
            }
            return cells[row - 'A', col];
        }
        set {
            row = Char.ToUpper(row);
            if (row < 'A' || row > 'Z') {
                throw new ArgumentOutOfRangeException ("row");
            }
            if (col < 0 || col >= NumCols) {
                throw new ArgumentOutOfRangeException ("col");
            }
            cells[row - 'A', col] = value;
        }
    }
}

结束示例]
```

## 15.10 运算符

### 15.10.1 常规内容

运算符是定义可应用于类实例的表达式运算符含义的成员。运算符使用运算符声明进行声明：

operator-declaration:
    attributes_opt operator-modifiers operator-declarator operator-body
operator-modifiers:
    operator-modifier
    operator-modifiers operator-modifier
operator-modifier:
    public
    static
    extern
operator-declarator:
    unary-operator-declarator
    binary-operator-declarator
    conversion-operator-declarator
unary-operator-declarator:
    type operator overloadable-unary-operator ( fixed-parameter )
overloadable-unary-operator: one of
    +  -  !  ~  ++  --  true  false
binary-operator-declarator:
    type operator overloadable-binary-operator ( fixed-parameter , fixed-parameter )
overloadable-binary-operator: one of
  +  -  *  /  %  &  |  ^  <<  >>
  ==  !=  >  <  >=  <=

conversion-operator-declarator:
  implicit operator type ( fixed-parameter )
  explicit operator type ( fixed-parameter )

operator-body:
  block
  ;

运算符分为三类：一元运算符（§15.10.2）、二元运算符（§15.10.3）和转换运算符（§15.10.4）。

当运算符声明包含 `extern` 修饰符时，该运算符称为外部运算符。由于外部运算符不提供实际实现，其运算符体由分号组成。对于其他所有运算符，运算符体由一个代码块组成，该代码块指定调用运算符时要执行的语句。运算符的代码块必须符合 §15.6.11 中所述的有返回值方法的规则。

以下规则适用于所有运算符声明：

- 运算符声明必须同时包含 `public` 和 `static` 修饰符。
- 运算符的参数不得带有任何修饰符。
- 运算符的签名（§15.10.2、§15.10.3、§15.10.4）必须不同于同一类中声明的所有其他运算符的签名。
- 运算符声明中引用的所有类型，其可访问性都不得低于运算符本身（§8.5.5）。
- 如果同一个修饰符在运算符声明中出现多次，则会产生错误。

每个运算符类别都施加了额外限制，具体内容将在以下小节中介绍。

与其他成员一样，在基类中声明的运算符会被派生类继承。由于运算符声明始终要求声明该运算符的类或结构体参与运算符的签名，因此派生类中声明的运算符不可能隐藏基类中声明的运算符。因此，运算符声明中从不需要、也从不允许使用 `new` 修饰符。

有关一元运算符和二元运算符的其他信息，请参阅 §12.4。

有关转换运算符的其他信息，请参阅 §11.5。

### 15.10.2 一元运算符

以下规则适用于一元运算符声明，其中 `T` 表示包含运算符声明的类或结构体的实例类型：

- 一元 `+`、`-`、`!`、`~` 运算符必须接受一个类型为 `T` 或 `T?` 的参数，并且可以返回任何类型。
- 一元 `++` 或 `--` 运算符必须接受一个类型为 `T` 或 `T?` 的参数，并且必须返回相同类型或从该类型派生的类型。
- 一元 `true` 或 `false` 运算符必须接受一个类型为 `T` 或 `T?` 的参数，并且必须返回 `bool` 类型。

一元运算符的签名由运算符标记（`+`、`-`、`!`、`~`、`++`、`--`、`true` 或 `false`）以及单个形式参数的类型组成。返回类型不属于一元运算符签名的一部分，形式参数的名称也不属于签名的一部分。




true 和 false 一元运算符需要成对声明。如果类声明了这些运算符之一而未同时声明另一个，则发生编译时错误。true 和 false 运算符在 §12.21 中进一步描述。

[示例：以下示例展示了整数向量类的 operator++ 实现及其后续用法：

```csharp
public class IntVector
{
    public IntVector(int length) {...}
    public int Length { ... }  // read-only property
    public int this[int index] { ... }  // read-write indexer
    public static IntVector operator++(IntVector iv) {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
            temp[i] = iv[i] + 1;
        return temp;
    }
}
class Test
{
    static void Main() {
        IntVector iv1 = new IntVector(4);   // vector of 4 x 0
        IntVector iv2;
        iv2 = iv1++;   // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;   // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

请注意，该运算符方法返回将操作数加 1 后产生的值，就像后缀递增和递减运算符（§12.7.10）以及前缀递增和递减运算符（§12.8.6）一样。与 C++ 中不同，此方法不应直接修改其操作数的值，因为这会违反后缀递增运算符的标准语义（§12.8.6）。结束示例]

## 15.10.3 二元运算符

以下规则适用于二元运算符声明，其中 T 表示包含该运算符声明的类或结构的实例类型：

- 二元非移位运算符应接受两个参数，其中至少一个参数应具有类型 T 或 T?，并且可以返回任意类型。
- 二元 << 或 >> 运算符（§12.10）应接受两个参数，第一个参数应具有类型 T 或 T?，第二个参数应具有类型 int 或 int?，并且可以返回任意类型。

二元运算符的签名由运算符标记（+、-、*、/、%、&、|、^、<<、>>、==、!=、>、<、>= 或 <=）和两个形参的类型组成。返回类型和形参名称不属于二元运算符的签名。

某些二元运算符需要成对声明。对于一对运算符中任一运算符的每个声明，都应存在该对中另一个运算符的匹配声明。如果两个运算符声明各自的返回类型与对应参数类型之间存在恒等转换，则这两个运算符声明匹配。以下运算符需要成对声明：

- operator == 和 operator !=
- operator > 和 operator <
- operator >= 和 operator <=

## 15.10.4 转换运算符

转换运算符声明引入用户定义转换（§11.5），该转换扩充预定义的隐式转换和显式转换。

包含 implicit 关键字的转换运算符声明引入用户定义隐式转换。隐式转换可出现在多种情况下，包括函数成员调用、强制转换表达式和赋值。§11.2 对此作了进一步描述。

包含 explicit 关键字的转换运算符声明引入用户定义显式转换。显式转换可出现在强制转换表达式中，§11.3 对此作了进一步描述。

转换运算符从源类型转换为目标类型，源类型由转换运算符的参数类型指示，目标类型由转换运算符的返回类型指示。

对于给定的源类型 S 和目标类型 T，如果 S 或 T 是可空值类型，则令 S0 和 T0 指代其基础类型；否则，S0 和 T0 分别等于 S 和 T。仅当以下所有条件均成立时，才允许类或结构声明从源类型 S 到目标类型 T 的转换：

- S0 和 T0 是不同的类型。
- S0 或 T0 是包含该运算符声明的类或结构的实例类型。
- S0 和 T0 都不是接口类型。
- 除用户定义转换外，不存在从 S 到 T 或从 T 到 S 的转换。

为这些规则的目的，与 S 或 T 关联的任何类型参数都被视为与其他类型没有继承关系的唯一类型，并且忽略对这些类型参数的任何约束。

[示例：在以下代码中：

```
class C<T> {...}
class D<T>: C<T>
{
    public static implicit operator C<int>(D<T> value) {...}    // Ok
    public static implicit operator C<string>(D<T> value) {...}    // Ok
    public static implicit operator C<T>(D<T> value) {...}    // Error
}
```

前两个运算符声明是允许的，因为 T 以及 int 和 string 分别被视为没有关系的唯一类型。但是，第三个运算符是错误的，因为 C<T> 是 D<T> 的基类。结束示例]

由第二条规则可知，转换运算符应转换为声明该运算符的类或结构类型，或从该类型转换。[示例：类或结构类型 C 可以定义从 C 到 int 以及从 int 到 C 的转换，但不能定义从 int 到 bool 的转换。结束示例]

无法直接重新定义预定义转换。因此，不允许转换运算符以 object 为源或目标进行转换，因为 object 与所有其他类型之间已经存在隐式和显式转换。同样，转换的源类型和目标类型都不能是对方的基类型，因为此时转换已经存在。但是，可以在泛型类型上声明运算符，这些运算符对于特定类型实参指定了已作为预定义转换存在的转换。

[示例：

```
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```

当为 T 指定类型 object 作为类型实参时，第二个运算符声明了一个已经存在的转换（存在从任意类型到类型 object 的隐式转换，因此也存在显式转换）。结束示例]

如果两个类型之间存在预定义转换，则忽略这些类型之间的任何用户定义转换。具体而言：

- 如果存在从类型 S 到类型 T 的预定义隐式转换（§11.2），则忽略从 S 到 T 的所有用户定义转换（隐式或显式）。
- 如果存在从类型 S 到类型 T 的预定义显式转换（§11.3），则忽略从 S 到 T 的任何用户定义显式转换。此外：
  - 如果 S 或 T 是接口类型，则忽略从 S 到 T 的用户定义隐式转换。
  - 否则，仍然考虑从 S 到 T 的用户定义隐式转换。

对于除 object 之外的所有类型，上面 Convertible<T> 类型声明的运算符不与预定义转换冲突。[示例：

```
void F(int i, Convertible<int> n) {
    i = n;                 // Error
    i = (int)n;            // User-defined explicit conversion
    n = i;                 // User-defined implicit conversion
    n = (Convertible<int>)i; // User-defined implicit conversion
}
```

但是，对于类型 object，除一种情况外，预定义转换在所有情况下都会隐藏用户定义转换：

```
void F(object o, Convertible<object> n) {
    o = n;                 // Pre-defined boxing conversion
    o = (object)n;         // Pre-defined boxing conversion
    n = o;                 // User-defined implicit conversion
    n = (Convertible<object>)o; // Pre-defined unboxing conversion
}
```

结束示例]

不允许用户定义转换以接口类型为源或目标。特别是，此限制确保在转换为接口类型时不会发生用户定义转换，并且仅当被转换的对象实际实现指定接口类型时，到接口类型的转换才会成功。

转换运算符的签名由源类型和目标类型组成。（这是返回类型参与签名的唯一成员形式。）转换运算符的隐式或显式分类不属于该运算符的签名。因此，类或结构不能声明源类型和目标类型均相同的隐式转换运算符和显式转换运算符。

> 注意：一般而言，用户定义的隐式转换应设计为从不引发异常且从不丢失信息。如果用户定义转换可能引发异常（例如，因为源参数超出范围）或丢失信息（例如丢弃高位），则应将转换定义为显式转换。结束注意

[示例：在以下代码中

```
using System;
public struct Digit
{
    byte value;
    public Digit(byte value) {
        if (value < 0 || value > 9) throw new ArgumentException();
        this.value = value;
    }
    public static implicit operator byte(Digit d) {
        return d.value;
    }
    public static explicit operator Digit(byte b) {
        return new Digit(b);
    }
}
```



从 Digit 到 byte 的转换是隐式的，因为它从不抛出异常或丢失信息，但从 byte 到 Digit 的转换是显式的，因为 Digit 只能表示 byte 可能值的一个子集。示例结束]

## 15.11 实例构造函数

### 15.11.1 概述

*实例构造函数*是一种成员，它实现初始化类实例所需的活动。实例构造函数使用*构造函数声明*来声明：

```
constructor-declaration:
    attributes_opt constructor-modifiers_opt constructor-declarator constructor-body

constructor-modifiers:
    constructor-modifier
    constructor-modifiers constructor-modifier

constructor-modifier:
    public
    protected
    internal
    private
    extern

constructor-declarator:
    identifier ( formal-parameter-list_opt ) constructor-initializer_opt

constructor-initializer:
    : base ( argument-list_opt )
    : this ( argument-list_opt )

constructor-body:
    block
    ;
```

一个*构造函数声明*可以包含一组*特性*（§22）、四个访问修饰符的有效组合（§15.3.6）以及一个 *extern* 修饰符（§15.6.8）。构造函数声明不允许多次包含同一修饰符。

*构造函数声明符*的*标识符*应命名声明该实例构造函数的类。如果指定了任何其他名称，则发生编译时错误。

实例构造函数的可选*形参列表*遵循与方法（§15.6）的*形参列表*相同的规则。由于参数的 *this* 修饰符仅适用于扩展方法（§15.6.10），构造函数的*形参列表*中的任何参数都不得包含 *this* 修饰符。形参列表定义实例构造函数的签名（§8.6），并管理重载决策（§12.6.4）在调用中选择特定实例构造函数的过程。

实例构造函数的*形参列表*中引用的每个类型至少应具有与构造函数本身相同的可访问性（§8.5.5）。

可选的*构造函数初始化器*指定在执行此实例构造函数的*构造函数体*中给出的语句之前要调用的另一个实例构造函数。这将在 §15.11.2 中进一步描述。

当构造函数声明包含 *extern* 修饰符时，该构造函数称为*外部构造函数*。由于外部构造函数声明不提供实际实现，其*构造函数体*由一个分号组成。对于所有其他构造函数，*构造函数体*由一个*块*组成，该块指定用于初始化类的新实例的语句。这完全对应于返回类型为 *void* 的实例方法（§15.6.11）的*块*。

实例构造函数不被继承。因此，类除了实际在该类中声明的实例构造函数之外没有其他实例构造函数，例外情况是，如果类不包含实例构造函数声明，则自动提供默认实例构造函数（§15.11.5）。

实例构造函数由对象创建表达式（§12.7.11.2）以及通过构造函数初始化器调用。

### 15.11.2 构造函数初始化器

所有实例构造函数（类 object 的实例构造函数除外）都在构造函数体之前隐式包含对另一个实例构造函数的调用。要隐式调用的构造函数由构造函数初始化器确定：

- 形式为 `base(argument-list_opt)` 的实例构造函数初始化器会导致调用直接基类中的实例构造函数。该构造函数使用 `argument-list` 和 §12.6.4 的重载决策规则来选择。候选实例构造函数的集合由直接基类的所有可访问实例构造函数组成。如果此集合为空，或者无法标识单个最佳实例构造函数，则发生编译时错误。
- 形式为 `this(argument-list_opt)` 的实例构造函数初始化器调用同一类中的另一个实例构造函数。该构造函数使用 `argument-list` 和 §12.6.4 的重载决策规则来选择。候选实例构造函数的集合由类自身中声明的所有实例构造函数组成。如果得到的适用实例构造函数集合为空，或者无法标识单个最佳实例构造函数，则发生编译时错误。如果实例构造函数声明通过一个或多个构造函数初始化器链调用自身，则发生编译时错误。

如果实例构造函数没有构造函数初始化器，则隐式提供形式为 `base()` 的构造函数初始化器。[注意：因此，形式为 `C(...) {...}` 的实例构造函数声明完全等效于 `C(...): base() {...}` 注释结束]

实例构造函数声明的*形参列表*所给出的参数的作用域包括该声明的构造函数初始化器。因此，构造函数初始化器被允许访问构造函数的参数。[示例：

```
class A
{
    public A(int x, int y) {}
}

class B: A
{
    public B(int x, int y): base(x + y, x - y) {}
}
```

示例结束] 实例构造函数初始化器不能访问正在创建的实例。因此，在构造函数初始化器的参数表达式中引用 `this` 是编译时错误，因为参数表达式通过简单名称引用任何实例成员也是编译时错误。

### 15.11.3 实例变量初始化器

当实例构造函数没有构造函数初始化器，或者它具有形式为 `base(...)` 的构造函数初始化器时，该构造函数隐式执行其类中声明的实例字段的变量初始化器所指定的初始化。这对应于在进入构造函数后立即、在隐式调用直接基类构造函数之前执行的一系列赋值。变量初始化器按它们在类声明中出现的文本顺序执行（§15.5.6）。

### 15.11.4 构造函数执行

变量初始化器被转换为赋值语句，并且这些赋值语句在调用基类实例构造函数之前执行。此顺序确保所有实例字段在访问该实例的任何语句执行之前，由其变量初始化器初始化。[示例：给定以下内容：

```
using System;
class A
{
    public A() {
        PrintFields();
    }
    public virtual void PrintFields() {}
}
class B: A
{
    int x = 1;
    int y;
    public B() {
        y = -1;
    }
    public override void PrintFields() {
        Console.WriteLine("x = {0}, y = {1}", x, y);
    }
}
```

当使用 `new B()` 创建 B 的实例时，生成以下输出：

```
x = 1, y = 0
```

x 的值为 1，因为变量初始化器在调用基类实例构造函数之前执行。但是，y 的值为 0（int 的默认值），因为对 y 的赋值直到基类构造函数返回后才执行。

将实例变量初始化器和构造函数初始化器视为自动插入到构造函数体之前的语句是很有用的。示例

```
using System;
using System.Collections;
class A
{
    int x = 1, y = -1, count;
    public A() {
        count = 0;
    }
    public A(int n) {
        count = n;
    }
}
class B: A
{
    double sqrt2 = Math.Sqrt(2.0);
    ArrayList items = new ArrayList(100);
    int max;
    public B(): this(100) {
        items.Add("default");
    }
    public B(int n): base(n - 1) {
        max = n;
    }
}
```

包含若干变量初始化器；它还包含两种形式（`base` 和 `this`）的构造函数初始化器。该示例对应于下面显示的代码，其中每条注释指示自动插入的语句（用于自动插入的构造函数调用的语法无效，但仅用于说明该机制）。

```
using System.Collections;
class A
{
    int x, y, count;
    public A() {
        x = 1;    // Variable initializer
        y = -1;   // Variable initializer
        object(); // Invoke object() constructor
        count = 0;
    }
    public A(int n) {
        x = 1;    // Variable initializer
        y = -1;   // Variable initializer
        object(); // Invoke object() constructor
        count = n;
    }
}
class B: A
{
    double sqrt2;
    ArrayList items;
    int max;
    public B(): this(100) {
        B(100);   // Invoke B(int) constructor
        items.Add("default");
    }
    public B(int n): base(n - 1) {
        sqrt2 = Math.Sqrt(2.0); // Variable initializer
        items = new ArrayList(100); // Variable initializer
        A(n - 1); // Invoke A(int) constructor
        max = n;
    }
}
```

示例结束]

### 15.11.5 默认构造函数

如果类不包含实例构造函数声明，则自动提供默认实例构造函数。该默认构造函数只调用直接基类的构造函数，就像它具有形式为 `base()` 的构造函数初始化器一样。如果类是抽象类，则默认构造函数的声明可访问性为 protected。否则，默认构造函数的声明可访问性为 public。

> [注意：因此，默认构造函数始终采用以下形式
>
> `protected C(): base() {}`
>
> 或
>
> `public C(): base() {}`
>
> 其中 C 是类的名称。注释结束]

如果重载决策无法为基类构造函数初始化器确定唯一的最佳候选，则发生编译时错误。





[示例：在以下代码中

```
class Message
{
    object sender;
    string text;
}
```

之所以提供默认构造函数，是因为该类不包含实例构造函数声明。因此，该示例完全等价于

```
class Message
{
    object sender;
    string text;
}
public Message(): base() {}
```

结束示例]

## 15.12 静态构造函数

静态构造函数是实现初始化封闭类所需操作的成员。静态构造函数使用静态构造函数声明来声明：

```
static-constructor-declaration:
    attributes_opt static-constructor-modifiers identifier ( ) static-constructor-body
```

```
static-constructor-modifiers:
    extern_opt static
    static extern_opt
```

```
static-constructor-body:
    block
    ;
```

静态构造函数声明可以包含一组特性（§22）和一个 extern 修饰符（§15.6.8）。

静态构造函数声明的标识符应命名声明该静态构造函数所在的类。如果指定任何其他名称，则发生编译时错误。

当静态构造函数声明包含 extern 修饰符时，该静态构造函数称为外部静态构造函数。由于外部静态构造函数声明不提供实际实现，其静态构造函数体由分号组成。对于所有其他静态构造函数声明，静态构造函数体由块组成，该块指定为初始化类而执行的语句。这完全对应于返回类型为 void 的静态方法的方法体（§15.6.11）。

静态构造函数不被继承，也不能直接调用。

封闭类的静态构造函数在给定应用程序域中最多执行一次。静态构造函数的执行由应用程序域中发生的以下事件中的第一个触发：

- 创建该类的实例。
- 引用该类的任何静态成员。

如果类包含执行开始的 Main 方法（§8.1），则该类的静态构造函数在调用 Main 方法之前执行。

要初始化新的封闭类类型，首先为该特定封闭类型创建一组新的静态字段（§15.5.2）。每个静态字段都初始化为其默认值（§15.5.5）。接下来，为这些静态字段执行静态字段初始化器（§15.5.6.2）。最后，执行静态构造函数。

[示例：以下示例

```
using System;
class Test
{
    static void Main() {
        A.F();
        B.F();
    }
}
class A
{
    static A() {
        Console.WriteLine("Init A");
    }
    public static void F() {
        Console.WriteLine("A.F");
    }
}
class B
{
    static B() {
        Console.WriteLine("Init B");
    }
    public static void F() {
        Console.WriteLine("B.F");
    }
}
```

必须产生输出：

```
Init A
A.F
Init B
B.F
```

因为 A 的静态构造函数的执行由对 A.F 的调用触发，而 B 的静态构造函数的执行由对 B.F 的调用触发。*结束示例]*

可以构造循环依赖，使得具有变量初始化器的静态字段以其默认值状态被观察到。

*[示例：以下示例*

```
using System;
class A
{
    public static int X;
    static A() {
        X = B.Y + 1;
    }
}
class B
{
    public static int Y = A.X + 1;
    static B() {
        static void Main() {
            Console.WriteLine("X = {0}, Y = {1}", A.X, B.Y);
        }
    }
}
```

产生输出

```
X = 1, Y = 2
```

为了执行 Main 方法，系统首先运行 B.Y 的初始化器，先于类 B 的静态构造函数。Y 的初始化器导致 A 的静态构造函数运行，因为引用了 A.X 的值。A 的静态构造函数转而继续计算 X 的值，并在这样做时获取 Y 的默认值，即零。因此 A.X 被初始化为 1。运行 A 的静态字段初始化器和静态构造函数的过程随后完成，返回到 Y 的初始值的计算，其结果变为 2。结束示例

由于静态构造函数对于每个封闭构造类类型恰好执行一次，因此它是强制执行对类型参数的运行时检查的方便位置，这些检查无法通过约束（§15.2.5）在编译时检查。[示例：以下类型使用静态构造函数强制类型实参为枚举：

```csharp
class Gen<T> where T: struct
{
    static Gen() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enum");
        }
    }
}
```

## 15.13 终结器

> [注意：在本标准的较早版本中，现在称为“终结器”的内容被称为“析构函数”。经验表明，术语“析构函数”引起了混淆，并常常导致不正确的预期，尤其是对于了解 C++ 的程序员。在 C++ 中，析构函数以确定的方式调用，而在 C# 中，终结器不是。要从 C# 获得确定的行为，应使用 Dispose。结束注意]

终结器是实现终结类实例所需操作的成员。终结器使用终结器声明来声明：

```
finalizer-declaration:
    attributes_opt extern_opt ~ identifier ( ) finalizer-body
finalizer-body:
    block
    ;
```

终结器声明可以包含一组特性（§22）。

终结器声明符的标识符应命名声明该终结器所在的类。如果指定任何其他名称，则发生编译时错误。

当终结器声明包含 extern 修饰符时，该终结器称为外部终结器。由于外部终结器声明不提供实际实现，其终结器体由分号组成。对于所有其他终结器，终结器体由块组成，该块指定为终结类实例而执行的语句。终结器体完全对应于返回类型为 void 的实例方法的方法体（§15.6.11）。

终结器不被继承。因此，类除了可能在该类中声明的终结器之外，没有其他终结器。

[注意：由于终结器要求没有参数，因此不能重载，所以一个类最多只能有一个终结器。结束注意]

终结器自动调用，不能显式调用。当任何代码不再可能使用某个实例时，该实例就有资格进行终结。实例的终结器的执行可以在该实例有资格进行终结之后的任何时间发生（§8.9）。当实例被终结时，该实例继承链中的终结器按从最派生到最不派生的顺序调用。终结器可以在任何线程上执行。关于管理终结器何时以及如何执行的规则的进一步讨论，请参见 §8.9。

[示例：以下示例的输出

```
using System;
class A
{
    ~A() {
        Console.WriteLine("A's finalizer");
    }
}
class B: A
{
    ~B() {
        Console.WriteLine("B's finalizer");
    }
}
class Test
{
    static void Main() {
        B b = new B();
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

为

B's finalizer
A's finalizer

因为继承链中的终结器按从最派生到最不派生的顺序调用。结束示例]

终结器通过重写 System.Object 上的虚拟方法 Finalize 实现。C# 程序不允许重写此方法或直接调用它（或其重写）。[示例：例如，程序

```
class A
{
    override protected void Finalize() {} // error
    public void F() {
        this.Finalize();    // error
    }
}
```

包含两个错误。结束示例]

编译器行为如同此方法及其重写根本不存在。[示例：因此，此程序：

```
class A
{
    void Finalize() {}      // permitted
}
```

是有效的，并且所示方法隐藏了 System.Object 的 Finalize 方法。结束示例]

关于从终结器引发异常时的行为讨论，请参见 §21.4。

## 15.14 迭代器

### 15.14.1 概述

使用迭代器块（§13.3）实现的函数成员（§12.6）称为迭代器。

只要相应函数成员的返回类型是某个枚举器接口（§15.14.2）或某个可枚举


interfaces (§15.14.3)。它可以作为方法体、运算符体或访问器体出现，而事件、实例构造函数、静态构造函数和终结器则不能实现为迭代器。

当使用迭代器块实现函数成员时，若函数成员的形式参数列表指定了任何 ref 或 out 参数，则为编译时错误。

## 15.14.2 Enumerator interfaces

枚举器接口是非泛型接口 System.Collections.IEnumerator 以及泛型接口 System.Collections.Generic.IEnumerator<T> 的所有实例化。为简洁起见，在本小节及其同级小节中，这些接口分别简称为 IEnumerator 和 IEnumerator<T>。

## 15.14.3 Enumerable interfaces

可枚举接口是非泛型接口 System.Collections.IEnumerable 以及泛型接口 System.Collections.Generic.IEnumerable<T> 的所有实例化。为简洁起见，在本小节及其同级小节中，这些接口分别简称为 IEnumerable 和 IEnumerable<T>。

## 15.14.4 Yield type

迭代器产生一系列值，所有值类型相同。此类型称为迭代器的产出类型。

- 返回 IEnumerator 或 IEnumerable 的迭代器的产出类型为 object。
- 返回 IEnumerator<T> 或 IEnumerable<T> 的迭代器的产出类型为 T。

## 15.14.5 Enumerator objects

### 15.14.5.1 General

当使用迭代器块实现返回枚举器接口类型的函数成员时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建一个枚举器对象并返回。该对象封装了迭代器块中指定的代码，并且迭代器块中的代码执行发生在调用枚举器对象的 MoveNext 方法时。枚举器对象具有以下特征：

- 它实现 IEnumerator 和 IEnumerator<T>，其中 T 为迭代器的产出类型。
- 它实现 System.IDisposable。
- 它使用传递给函数成员的参数值（如果有）和实例值的副本进行初始化。
- 它有四种可能状态：before、running、suspended 和 after，并且初始处于 before 状态。

枚举器对象通常是编译器生成的枚举器类的实例，该类封装迭代器块中的代码并实现枚举器接口，但也可能采用其他实现方法。如果枚举器类由编译器生成，则该类将直接或间接嵌套在包含函数成员的类中，它将具有私有访问性，并且其名称保留供编译器使用 (§7.4.3)。

枚举器对象可能实现比上述更多的接口。

以下小节描述了枚举器对象提供的 IEnumerator 和 IEnumerator<T> 接口实现中 MoveNext、Current 和 Dispose 成员的所需行为。

枚举器对象不支持 IEnumerator.Reset 方法。调用此方法会导致抛出 System.NotSupportedException。

### 15.14.5.2 The MoveNext method

枚举器对象的 MoveNext 方法封装了迭代器块的代码。调用 MoveNext 方法会执行迭代器块中的代码并相应地设置枚举器对象的 Current 属性。MoveNext 执行的确切操作取决于调用 MoveNext 时枚举器对象的状态：

- 如果枚举器对象的状态为 before，调用 MoveNext：
  - 将状态更改为 running。
  - 将迭代器块的参数（包括 this）初始化为枚举器对象初始化时保存的参数值和实例值。
  - 从开头执行迭代器块，直到执行被中断（如下面所述）。
- 如果枚举器对象的状态为 running，调用 MoveNext 的结果是不确定的。
- 如果枚举器对象的状态为 suspended，调用 MoveNext：
  - 将状态更改为 running。
  - 将所有局部变量和参数（包括 this）的值恢复为上次暂停迭代器块执行时保存的值。[注意：这些变量引用的任何对象的内容可能自上次调用 MoveNext 以来已发生变化。结束注释]
  - 从导致执行暂停的 yield return 语句之后立即恢复迭代器块的执行，并继续执行直到执行被中断（如下面所述）。
- 如果枚举器对象的状态为 after，调用 MoveNext 返回 false。

当 MoveNext 执行迭代器块时，执行可能以四种方式被中断：通过 yield return 语句，通过 yield break 语句，通过遇到迭代器块的末尾，以及通过异常被抛出并从迭代器块中传播。

- 当遇到 yield return 语句 (§10.4.4.20) 时：
  - 语句中给出的表达式被求值，隐式转换为产出类型，并赋给枚举器对象的 Current 属性。
  - 迭代器体的执行被挂起。所有局部变量和参数（包括 this）的值被保存，yield return 语句的位置也被保存。如果 yield return 语句位于一个或多个 try 块内，则相关联的 finally 块此时不会执行。
  - 枚举器对象的状态更改为 suspended。
  - MoveNext 方法向其调用者返回 true，表示迭代成功推进到下一个值。
- 当遇到 yield break 语句 (§10.4.4.20) 时：
  - 如果 yield break 语句位于一个或多个 try 块内，则相关联的 finally 块将被执行。
  - 枚举器对象的状态更改为 after。
  - MoveNext 方法向其调用者返回 false，表示迭代已完成。
- 当遇到迭代器体的末尾时：
  - 枚举器对象的状态更改为 after。
  - MoveNext 方法向其调用者返回 false，表示迭代已完成。
- 当异常被抛出并从迭代器块中传播时：
  - 异常传播将已执行迭代器体中的适当 `finally` 块。
  - 枚举器对象的状态更改为 *after*。
  - 异常传播继续到 `MoveNext` 方法的调用者。

### 15.14.5.3 The Current property

枚举器对象的 Current 属性受迭代器块中 `yield return` 语句的影响。

当枚举器对象处于 *suspended* 状态时，Current 的值是上一次调用 `MoveNext` 时设置的值。当枚举器对象处于 *before*、*running* 或 *after* 状态时，访问 Current 的结果是不确定的。

对于产出类型不是 `object` 的迭代器，通过枚举器对象的 `IEnumerable` 实现访问 Current 的结果对应于通过枚举器对象的 `IEnumerator<T>` 实现访问 Current 并将结果强制转换为 `object`。

### 15.14.5.4 The Dispose method

`Dispose` 方法用于通过将枚举器对象带到 *after* 状态来清理迭代。

- 如果枚举器对象的状态为 *before*，调用 `Dispose` 将状态更改为 *after*。
- 如果枚举器对象的状态为 *running*，调用 `Dispose` 的结果是不确定的。
- 如果枚举器对象的状态为 *suspended*，调用 `Dispose`：
  - 将状态更改为 *running*。
  - 执行任何 finally 块，就好像最后执行的 `yield return` 语句是 `yield break` 语句一样。如果这导致异常被抛出并从迭代器体中传播，则枚举器对象的状态设置为 *after*，并且异常传播到 `Dispose` 方法的调用者。
  - 将状态更改为 *after*。
- 如果枚举器对象的状态为 *after*，调用 `Dispose` 没有任何效果。

## 15.14.6 Enumerable objects

### 15.14.6.1 General

当使用迭代器块实现返回可枚举接口类型的函数成员时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建一个 *enumerable object* 并返回。可枚举对象的 `GetEnumerator` 方法返回一个封装迭代器块中指定代码的枚举器对象，并且迭代器块中的代码执行发生在调用枚举器对象的 `MoveNext` 方法时。可枚举对象具有以下特征：

- 它实现 `IEnumerable` 和 `IEnumerable<T>`，其中 T 为迭代器的产出类型。
- 它使用传递给函数成员的参数值（如果有）和实例值的副本进行初始化。

可枚举对象通常是编译器生成的可枚举类的实例，该类封装迭代器块中的代码并实现可枚举接口，但也可能采用其他实现方法。如果可枚举类由编译器生成，则该类将被嵌套，

直接或间接地，在包含该函数成员的类中，它将具有私有可访问性，并且它将具有一个保留供编译器使用的名称（§7.4.3）。

可枚举对象可能实现比上面指定的更多的接口。[注意：例如，可枚举对象还可以实现 IEnumerable 和 IEnumerable<T>，使其既能作为可枚举对象又能作为枚举器。通常，这样的实现会在第一次调用 GetEnumerator 时返回其自身实例（以节省分配）。后续对 GetEnumerator 的调用（如果有）会返回一个新的类实例，通常属于同一个类，这样对不同枚举器实例的调用不会相互影响。即使前一个枚举器已经枚举过序列末尾，它也不能返回同一实例，因为以后所有对已耗尽枚举器的调用都必须抛出异常。注意结束]

### 15.14.6.2 GetEnumerator 方法

可枚举对象提供 IEnumerable 和 IEnumerable<T> 接口的 GetEnumerator 方法的实现。这两个 GetEnumerator 方法共享一个公共实现，该实现获取并返回一个可用的枚举器对象。枚举器对象使用初始化可枚举对象时保存的参数值和实例值进行初始化，但除此之外，枚举器对象按 §15.14.5 所述工作。

## 15.15 异步函数

### 15.15.1 概述

带有 async 修饰符的方法（§15.6）或匿名函数（§12.16）称为异步函数。一般而言，术语 async 用于描述任何具有 async 修饰符的函数。

异步函数的形参列表指定任何 ref 或 out 参数都是编译时错误。

异步方法的返回类型应为 void 或任务类型。任务类型是 System.Threading.Tasks.Task 以及由 System.Threading.Tasks.Task<T> 构造的类型。为简洁起见，本章中这些类型分别称为 Task 和 Task<T>。返回任务类型的异步方法称为返回任务的。

任务类型的准确定义由实现定义，但从语言的角度看，任务类型处于未完成、成功或出错状态之一。出错的任务记录相关异常。成功的 Task<T> 记录类型 T 的结果。任务类型是可等待的，因此任务可以是 await 表达式（§12.8.8）的操作数。

异步函数能够通过其主体中的 await 表达式（§12.8.8）暂停求值。之后可通过恢复委托在挂起的 await 表达式处恢复求值。恢复委托的类型为 System.Action，当调用它时，异步函数调用的求值将从离开处的 await 表达式恢复。如果该函数调用从未被挂起，则异步函数调用的当前调用方是原始调用方；否则是恢复委托的最近调用方。

### 15.15.2 返回任务的异步函数的求值

调用返回任务的异步函数会生成返回任务类型的实例。这称为该异步函数的返回任务。该任务最初处于未完成状态。

随后对异步函数体进行求值，直到它被挂起（通过到达 await 表达式）或终止；此时，控制权连同返回任务一起返回给调用方。

当异步函数体终止时，返回任务会脱离未完成状态：

- 如果函数体因到达 return 语句或主体末尾而终止，则任何结果值都会记录在返回任务中，该任务被置于成功状态。
- 如果函数体因未捕获异常（§13.10.6）而终止，则该异常会记录在返回任务中，该任务被置于出错状态。

### 15.15.3 返回 void 的异步函数的求值

如果异步函数的返回类型是 void，则求值与上述方式存在以下差异：由于不返回任务，函数改为将完成和异常传达给当前线程的同步上下文。同步上下文的准确定义依赖于实现，但它表示当前线程运行“位置”的一种形式。当返回 void 的异步函数的求值开始、成功完成或导致抛出未捕获异常时，会通知同步上下文。

这允许上下文跟踪有多少个返回 void 的异步函数在其下运行，并决定如何传播从它们中产生的异常。

## 16. 结构体

## 16.1 概述

结构体与类相似，因为它们表示可包含数据成员和函数成员的数据结构。然而，与类不同，结构体是值类型，不需要堆分配。结构体类型的变量直接包含结构体的数据，而类类型的变量包含对数据的引用，后者称为对象。

> [注意：结构体特别适用于具有值语义的小型数据结构。复数、坐标系中的点或字典中的键值对都是结构体的良好示例。这些数据结构的关键在于它们的数据成员很少，不需要使用继承或引用同一性，并且可以使用值语义方便地实现，其中赋值复制值而不是引用。注意结束]

如 §9.3.5 所述，C# 提供的简单类型（如 int、double 和 bool）实际上都是结构体类型。

## 16.2 结构体声明

### 16.2.1 概述

结构体声明是一种类型声明（§14.7），它声明一个新的结构体：

```
struct-declaration:
    attributesopt struct-modifiersopt partialopt struct identifier type-parameter-list opt
    struct-interfacesopt type-parameter-constraints-clausesopt struct-body ;opt
```

结构体声明由可选的一组特性（§22）组成，其后是可选的一组结构体修饰符（§16.2.2），其后是可选的 partial 修饰符（§15.2.7），其后是关键字 struct 和命名该结构体的标识符，其后是可选类型参数列表规范（§15.2.3），其后是可选结构体接口规范（§16.2.4），其后是可选类型参数约束子句规范（§15.2.5），其后是结构体主体（§16.2.5），并且可选地后跟一个分号。

除非结构体声明也提供类型参数列表，否则不得提供类型参数约束子句。

提供类型参数列表的结构体声明是泛型结构体声明。

### 16.2.2 结构体修饰符

结构体声明可以可选地包含一系列结构体修饰符：

```
struct-modifiers:
    struct-modifier
    struct-modifiers struct-modifier

struct-modifier:
    new
    public
    protected
    internal
    private
```

同一修饰符在结构体声明中多次出现是编译时错误。

结构体声明的修饰符与类声明的修饰符（§15.2.2）含义相同。

### 16.2.3 partial 修饰符

partial 修饰符指示此结构体声明是部分类型声明。在封闭命名空间或类型声明中，多个同名部分结构体声明按照 §15.2.7 指定的规则合并成一个结构体声明。

### 16.2.4 结构体接口

结构体声明可以包含结构体接口规范，在这种情况下，称该结构体直接实现给定的接口类型。对于构造的结构体类型（包括在泛型类型声明中声明的嵌套类型（§15.3.9.7）），每个实现的接口类型是通过对给定接口中的每个类型参数替换为构造类型的对应类型实参而获得的。

```
struct-interfaces:
  : interface-type-list
```

部分结构体声明（§15.2.7）多个部分上的接口处理将在 §15.2.4.3 中进一步讨论。

接口实现将在 §18.6 中进一步讨论。

### 16.2.5 结构体主体

结构体的结构体主体定义结构体的成员。

```
struct-body:
  { struct-member-declarations_opt }
```

## 16.3 结构体成员

结构体的成员由结构体成员声明引入的成员和从 System.ValueType 类型继承的成员组成。

```
struct-member-declarations:
  struct-member-declaration
```

```
struct-member-declaration:
  constant-declaration
  field-declaration
  method-declaration
  property-declaration
  event-declaration
  indexer-declaration
  operator-declaration
  constructor-declaration
  static-constructor-declaration
  type-declaration
```

[注意：除 finalizer-declaration 外的所有类成员声明也都是结构体成员声明。注意结束] 除 §16.4 指出的差异外，§15.3 至 §15.12 中提供的类成员描述也适用于结构体成员。

## 16.4 类与结构体的差异

### 16.4.1 概述

结构体在几个重要方面与类不同：

- 结构体是值类型（§16.4.2）。
- 所有结构体类型都隐式继承自 System.ValueType 类（§16.4.3）。




- 将值赋给结构体类型的变量会创建被赋值的副本 (§16.4.4)。
- 结构体的默认值是通过将所有字段设置为其默认值而产生的数值 (§16.4.5)。
- 装箱和拆箱操作用于在结构体类型与某些引用类型之间进行转换 (§16.4.6)。
- this 在结构体成员中的含义与类中不同 (§16.4.7)。
- 结构体的实例字段声明不允许包含变量初始值设定项 (§16.4.8)。
- 结构体不允许声明无参数的实例构造函数 (§16.4.9)。
- 结构体不允许声明终结器。

## 16.4.2 值语义

结构体是值类型 (§9.3)，据说具有值语义。另一方面，类是引用类型 (§9.2)，据说具有引用语义。

结构体类型的变量直接包含结构体的數據，而类类型的变量包含对包含数据的对象的引用。当结构体 B 包含类型为 A 的实例字段且 A 是结构体类型时，A 依赖于 B 或由 B 构造的类型会成为编译时错误。如果 X 包含类型为 Y 的实例字段，则结构体 X 直接依赖于结构体 Y。给定此定义，结构体所依赖的结构体的完整集合是直接依赖关系的传递闭包。

```
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```

是错误，因为 Node 包含其自身类型的实例字段。另一个示例

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

是错误，因为类型 A、B 和 C 彼此相互依赖。 end example

对于类，两个变量可能引用同一个对象，因此对一个变量的操作可能影响另一个变量所引用的对象。对于结构体，变量各自拥有数据的副本（ref 和 out 参数变量的情况除外），因此一个变量上的操作不可能影响另一个变量。此外，除非显式可空 (§9.3.11)，结构体类型的值不可能为 null。 [Note: 如果结构体包含引用类型的字段，则所引用对象的内容可以由其他操作更改。然而字段本身的值，即它引用哪个对象，不能通过对不同结构体值的修改来更改。 end note]

```
struct Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

代码片段

Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);

```
public KeyValuePair(string key, string value) {
    if (key == null || value == null) throw new ArgumentException();
    this.key = key;
    this.value = value;
}
```

用户定义的实例构造函数仅在显式调用时才防止空值。在 KeyValuePair 变量受默认值初始化的情况下，key 和 value 字段将为 null，并且结构体应准备好处理此状态。 end note]

## 16.4.6 装箱和拆箱

类类型的值可以通过在编译时将引用视为另一种类型，简单地转换为 object 类型或由该类实现的接口类型。同样，object 类型的值或接口类型的值可以转换回类类型而不会更改引用（当然，在这种情况下需要运行时类型检查）。

由于结构体不是引用类型，这些操作对于结构体类型实现方式不同。当结构体类型的值转换为某些引用类型时（定义见 §11.2.8），会发生装箱操作。同样，当某些引用类型的值（定义见 §11.3.6）转换回结构体类型时，会发生拆箱操作。与类类型上的相同操作相比，装箱和拆箱会将结构体值复制到装箱实例中或从装箱实例中复制出来这一关键区别。 [Note: 因此，在装箱或拆箱操作之后，对未装箱结构体的更改不会反映在装箱的结构体中。 end note]

有关装箱和拆箱的更多详细信息，请参阅 §11.2.8 和 §11.3.6。

## 16.4.7 this 的含义

结构体中 this 的含义与类中 this 的含义不同，如 §12.7.8 所述。当结构体类型重写从 System.ValueType 继承的虚方法时（如 Equals、GetHashCode 或 ToString），通过结构体类型的实例调用虚方法不会导致装箱发生。即使结构体用作类型参数并且调用通过类型参数类型的实例发生，也同样成立。 [Example:

```
using System;
struct Counter
{
    int value;
    public override string ToString() {
        value++;
        return value.ToString();
    }
}
class Program
{
    static void Test<T>() where T: new() {
        T x = new T();
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
    }
    static void Main() {
        Test<Counter>();
    }
}
```

程序的输出是：
1
2
3

虽然 ToString 具有副作用是不好的风格，但该示例证明了对 x.ToString() 的三次调用均未发生装箱。 end example]

同样，当在约束类型参数上访问成员时，如果该成员在值类型内实现，则永远不会隐式发生装箱。例如，假设接口 ICounter 包含一个可用于修改值的方法 Increment。如果 ICounter 用作约束，则 Increment 方法的实现会使用对调用 Increment 的变量的引用调用，而永远不是装箱的副本。 [Example:

```csharp
using System;
interface ICounter
{
    void Increment();
}
struct Counter: ICounter
{
    int value;
    public override string ToString() {
        return value.ToString();
    }
    void ICounter.Increment() {
        value++;
    }
}
class Program
{
    static void Test<T>() where T: ICounter, new() {
        T x = new T();
        Console.WriteLine(x);
        x.Increment();    // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();  // Modify boxed copy of x
        Console.WriteLine(x);
    }
    static void Main() {
        Test<Counter>();
    }
}
```

第一次调用 Increment 修改变量 x 中的值。这与第二次调用 Increment 不等价，后者修改的是 x 的装箱副本中的值。因此，程序的输出是：

0
1
1

end example]

## 16.4.8 字段初始值设定项

如 §16.4.5 所述，结构体的默认值由将所有值类型字段设置为其默认值且所有引用类型字段设置为 null 所产生的值组成。因此，结构体不允许实例字段声明包含变量初始值设定项。此限制仅适用于实例字段。结构体的静态字段允许包含变量初始值设定项。 [Example: 以下

```csharp
struct Point
{
    public int x = 1; // Error, initializer not permitted
    public int y = 1; // Error, initializer not permitted
}
```

是错误的，因为实例字段声明包含变量初始值设定项。 end example]

## 16.4.9 构造函数

与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，该构造函数始终返回将所有值类型字段设置为其默认值且所有引用类型字段设置为 null 所产生的值 (§9.3.3)。结构体可以声明具有参数的实例构造函数。 [Example:

```
struct Point
{
    int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

给定上述声明，语句

```
Point p1 = new Point();
Point p2 = new Point(0, 0);
```

都创建了一个 x 和 y 初始化为零的 Point。 end example]

结构体实例构造函数不允许包含形式为 base(argument-list) 的构造函数初始值设定项。

结构体实例构造函数的 this 参数对应于结构体类型的 out 参数。因此，this 必须在构造函数返回的每个位置都被明确赋值 (§10.4)。同样，在被明确赋值之前，不能在构造函数体中读取它（即使是隐式读取）。

如果结构体实例构造函数指定了构造函数初始值设定项，则该初始值设定项被视为对 this 的明确赋值，该赋值发生在构造函数体之前。因此，主体本身没有初始化要求。 [Example: 考虑以下实例构造函数实现：

```
struct Point
{
    int x, y;
    public int X {
        set { x = value; }
    }
    public int Y {
        set { y = value; }
    }
    public Point(int x, int y) {
        X = x;    // error, this is not yet definitely assigned
        Y = y;    // error, this is not yet definitely assigned
    }
}
```

在被构造的结构体的所有字段都被明确赋值之前，不能调用任何实例函数成员（包括属性 X 和 Y 的 set 访问器）。请注意，然而，如果 Point 是类而不是结构体，则实例构造函数实现将被允许。
end example]

## 16.4.10 静态构造函数

结构体的静态构造函数遵循与类的大多数相同规则。结构体类型的静态构造函数的执行由应用程序域内首先发生的以下事件触发：

- 引用了结构体类型的静态成员。
- 调用了结构体类型的显式声明的构造函数。





## 17. 数组
### 17.1 概述

数组是一种数据结构，包含若干通过计算索引访问的变量。数组中包含的变量也称为数组的元素，它们都具有相同的类型，该类型称为数组的元素类型。

数组具有一个秩，它决定了与每个数组元素关联的索引数量。数组的秩也称为数组的维度。秩为 1 的数组称为一维数组。秩大于 1 的数组称为多维数组。特定大小的多维数组通常称为二维数组、三维数组，以此类推。数组的每个维度都有一个关联的长度，该长度是大于或等于零的整数。维度长度不属于数组类型的一部分，而是在运行时创建数组类型实例时确立的。维度的长度决定了该维度索引的有效范围：对于长度为 N 的维度，索引范围为 0 到 N−1（含）。数组中的元素总数是数组每个维度长度的乘积。如果数组的一个或多个维度长度为零，则该数组称为空数组。

每个数组类型都是引用类型（§9.2）。数组的元素类型可以是任何类型，包括值类型和数组类型。

### 17.2 数组类型
### 17.2.1 概述

数组类型的语法产生式见 §9.2.1。

数组类型写作一个非数组类型后跟一个或多个秩说明符。

非数组类型是任何本身不是数组类型的类型。

数组类型的秩由数组类型中最左侧的秩说明符给出：秩说明符表示该数组的秩为 1 加上秩说明符中 ',' 标记的数量。

数组类型的元素类型是删除最左侧秩说明符后得到的类型：

- 形式为 `T[R]` 的数组类型是秩为 R、非数组元素类型为 T 的数组。
- 形式为 `T[R][R1]...[Rr]` 的数组类型是秩为 R、元素类型为 `T[R1]...[Rr]` 的数组。

实际上，秩说明符是在最终的非数组元素类型之前从左到右读取的。[示例：类型 `int[][ , ][ , ]` 是一个一维数组，其元素是三维数组，而这些三维数组的元素是 int 的二维数组。示例结束]

在运行时，数组类型的值可以是 null，也可以是对该数组类型实例的引用。[注意：根据 §17.6 的规则，该值也可以是对协变数组类型的引用。注意结束]

### 17.2.2 System.Array 类型

`System.Array` 类型是所有数组类型的抽象基类型。存在从任何数组类型到 `System.Array` 以及到 `System.Array` 实现的任何接口类型的隐式引用转换（§11.2.7）。存在从 `System.Array` 和 `System.Array` 实现的任何接口类型到任何数组类型的显式引用转换（§11.3.5）。`System.Array` 本身不是数组类型，而是一个类类型，所有数组类型都派生自该类类型。

在运行时，`System.Array` 类型的值可以是 null，也可以是对任何数组类型实例的引用。

### 17.2.3 数组与泛型集合接口

一维数组 `T[]` 实现接口 `System.Collections.Generic.IList<T>`（简称 `IList<T>`）及其基接口。因此，存在从 `T[]` 到 `IList<T>` 及其基接口的隐式转换。此外，如果存在从 `S` 到 `T` 的隐式引用转换，则 `S[]` 实现 `IList<T>`，并且存在从 `S[]` 到 `IList<T>` 及其基接口的隐式引用转换（§11.2.7）。如果存在从 `S` 到 `T` 的显式引用转换，则存在从 `S[]` 到 `IList<T>` 及其基接口的显式引用转换（§11.3.5）。

类似地，一维数组 `T[]` 还实现接口 `System.Collections.Generic.IReadOnlyList<T>`（简称 `IReadOnlyList<T>`）及其基接口。因此，存在从 `T[]` 到 `IReadOnlyList<T>` 及其基接口的隐式转换。此外，如果存在从 `S` 到 `T` 的隐式引用转换，则 `S[]` 实现 `IReadOnlyList<T>`，并且存在从 `S[]` 到 `IReadOnlyList<T>` 及其基接口的隐式引用转换（§11.2.7）。如果存在从 `S` 到 `T` 的显式引用转换，则存在从 `S[]` 到 `IReadOnlyList<T>` 及其基接口的显式引用转换（§11.3.5）。

[示例：例如：

```csharp
using System.Collections.Generic;
class Test
{
    static void Main()
    {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;
        IList<string> lst1 = sa;            // Ok
        IList<string> lst2 = oa1;           // Error, cast needed
        IList<object> lst3 = sa;            // Ok
        IList<object> lst4 = oa1;           // Ok
        IList<string> lst5 = (IList<string>)oa1;  // Exception
        IList<string> lst6 = (IList<string>)oa2;  // Ok

        IReadOnlyList<string> lst7 = sa;    // Ok
        IReadOnlyList<string> lst8 = oa1;   // Error, cast needed
        IReadOnlyList<object> lst9 = sa;    // Ok
        IReadOnlyList<object> lst10 = oa1;  // Ok
        IReadOnlyList<string> lst11 = (IReadOnlyList<string>)oa1; // Exception
        IReadOnlyList<string> lst12 = (IReadOnlyList<string>)oa2; // Ok
    }
}
```

赋值 `lst2 = oa1` 会产生编译时错误，因为从 `object[]` 到 `IList<string>` 的转换是显式转换，而不是隐式转换。强制转换 `(IList<string>)oa1` 会在运行时引发异常，因为 `oa1` 引用的是 `object[]` 而不是 `string[]`。但是强制转换 `(IList<string>)oa2` 不会引发异常，因为 `oa2` 引用的是 `string[]`。示例结束]

每当存在从 `S[]` 到 `IList<T>` 的隐式或显式引用转换时，也就存在从 `IList<T>` 及其基接口到 `S[]` 的显式引用转换（§11.3.5）。

当数组类型 `S[]` 实现 `IList<T>` 时，所实现接口的某些成员可能会抛出异常。接口实现的精确行为超出了本规范的范围。

### 17.3 数组创建

数组实例通过*数组创建表达式*（§12.7.11.5）或包含*数组初始值设定项*（§17.7）的字段或局部变量声明创建。数组实例也可以在计算涉及参数数组的参数列表时隐式创建（§15.6.2.5）。

创建数组实例时，每个维度的秩和长度被确立，并在实例的整个生命周期内保持不变。换句话说，无法更改现有数组实例的秩，也无法调整其维度的大小。

数组实例始终是数组类型的。`System.Array` 类型是抽象类型，无法实例化。

通过*数组创建表达式*创建的数组元素始终初始化为其默认值（§10.3）。

### 17.4 数组元素访问

数组元素使用形式为 `A[I₁, I₂, ..., Iₙ]` 的*元素访问*表达式（§12.7.7.2）访问，其中 `A` 是数组类型的表达式，每个 `Iₓ` 是类型为 `int`、`uint`、`long`、`ulong` 的表达式，或者可以隐式转换为这些类型中的一种或多种。数组元素访问的结果是一个变量，即由索引选定的数组元素。

可以使用 `foreach` 语句（§13.9.5）枚举数组的元素。

### 17.5 数组成员

每个数组类型都继承 `System.Array` 类型声明的成员。

### 17.6 数组协变

对于任意两个*引用类型* `A` 和 `B`，如果存在从 `A` 到 `B` 的隐式引用转换（§11.2.7）或显式引用转换（§11.3.4），则相同的引用转换也存在于从数组类型 `A[R]` 到数组类型 `B[R]` 之间，其中 `R` 是任意给定的*秩说明符*（但两个数组类型必须相同）。这种关系称为*数组协变*。数组协变尤其意味着，如果存在从 `B` 到 `A` 的隐式引用转换，则数组类型 `A[R]` 的值实际上可能是数组类型 `B[R]` 实例的引用。

由于数组协变，对引用类型数组元素的赋值包含一个运行时检查，该检查确保赋给数组元素的值实际上是允许的类型（§12.18.2）。

*示例：*

```csharp
class Test
{
    static void Fill(object[] array, int index, int count, object value) {
        for (int i = index; i < index + count; i++) array[i] = value;
    }
    static void Main() {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```


Fill 方法中对 array[i] 的赋值隐式包含运行时检查，该检查确保 value 要么是 null 引用，要么是对与 array 的实际元素类型兼容的类型的对象的引用。在 Main 中，前两次调用 Fill 成功，但第三次调用在第一次执行对 array[1] 的赋值时会引发 System.ArrayTypeMismatchException。发生异常是因为装箱的 int 不能存储在字符串数组中。示例结束

数组协变具体而言不扩展到值类型的数组。例如，不存在允许将 int[] 视为 object[] 的转换。

## 17.7 数组初始值设定项

数组初始值设定项可以指定在字段声明（$15.5）、局部变量声明（$13.6.2）和数组创建表达式（$12.7.11.5）中：

```
array-initializer:
    { variable-initializer-list_opt }
    { variable-initializer-list , }

variable-initializer-list:
    variable-initializer
    variable-initializer-list , variable-initializer

variable-initializer:
    expression
    array-initializer
```

数组初始值设定项由一系列变量初始值设定项组成，这些变量初始值设定项由“{”和“}”标记括起，并由“,”标记分隔。每个变量初始值设定项是一个表达式；对于多维数组，则是一个嵌套数组初始值设定项。

使用数组初始值设定项的上下文决定要初始化的数组的类型。在数组创建表达式中，数组类型紧接在初始值设定项之前，或者从数组初始值设定项中的表达式推断。在字段或变量声明中，数组类型是所声明的字段或变量的类型。当数组初始值设定项用于字段或变量声明中时，[示例：

```
int[] a = {0, 2, 4, 6, 8};
```

示例结束] 它只是等效数组创建表达式的简写：[示例：

```
int[] a = new int[] {0, 2, 4, 6, 8};
```

示例结束]

对于一维数组，数组初始值设定项应由一系列表达式组成，每个表达式都具有到数组元素类型的隐式转换（$11.2）。这些表达式按递增顺序初始化数组元素，从索引零处的元素开始。数组初始值设定项中的表达式数量决定所创建的数组实例的长度。[示例：上面的数组初始值设定项创建长度为 5 的 int[] 实例，然后用以下值初始化该实例：

```
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

示例结束]

对于多维数组，数组初始值设定项的嵌套层数应与数组的维度数相同。最外层嵌套级别对应最左侧维度，最内层嵌套级别对应最右侧维度。数组每个维度的长度由数组初始值设定项中对应嵌套级别的元素数量确定。对于每个嵌套数组初始值设定项，其元素数量应与同一级别的其他数组初始值设定项相同。[示例：以下示例：

```
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```

创建一个二维数组，其最左侧维度的长度为五，最右侧维度的长度为二：

```csharp
int[,] b = new int[5, 2];
```

然后用以下值初始化该数组实例：

```csharp
b[0, 0] = 0; b[0, 1] = 1;
b[1, 0] = 2; b[1, 1] = 3;
b[2, 0] = 4; b[2, 1] = 5;
b[3, 0] = 6; b[3, 1] = 7;
b[4, 0] = 8; b[4, 1] = 9;
```

*示例结束*

如果除最右侧维度之外的某个维度被指定为零长度，则后续维度假定也为零长度。[示例：

```csharp
int[,] c = {};
```

创建一个二维数组，其最左侧和最右侧维度的长度均为零：

```csharp
int[,] c = new int[0, 0];
```

*示例结束*

当数组创建表达式同时包含显式维度长度和数组初始值设定项时，这些长度应为常量表达式，并且每个嵌套级别的元素数量应与对应维度长度匹配。[示例：下面是一些示例：

```csharp
int i = 3;
int[,] x = new int[3] {0, 1, 2};        // OK
int[,] y = new int[i] {0, 1, 2};        // Error, i not a constant
int[,] z = new int[3] {0, 1, 2, 3};     // Error, length/initializer mismatch
```

这里，y 的初始值设定项导致编译时错误，因为维度长度表达式不是常量；z 的初始值设定项导致编译时错误，因为长度与初始值设定项中的元素数量不一致。*示例结束*]

[注意：C# 允许在数组初始值设定项的末尾出现尾随逗号。此语法为在此类列表中添加或删除成员提供了灵活性，并简化了此类列表的机器生成。*注意结束*]

## 18. 接口

### 18.1 概述

接口定义协定。实现接口的类或结构体应遵守其协定。接口可以继承多个基接口，类或结构体可以实现多个接口。

接口可以包含方法、属性、事件和索引器。接口本身不为其声明的成员提供实现。接口仅指定实现该接口的类或结构体应提供的成员。

### 18.2 接口声明

### 18.2.1 概述

接口声明是一种类型声明（§14.7），用于声明新的接口类型。

```
interface-declaration:
    attributesopt interface-modifiersopt partialopt interface
    identifier variant-type-parameter-list opt
    interface-baseopt type-parameter-constraints-clausesopt interface-body ;opt
```

接口声明由可选的一组特性（§22）、可选的一组接口修饰符（§18.2.2）、可选的 partial 修饰符（§15.2.7）、关键字 interface 和命名该接口的标识符、可选的变体类型参数列表规范（§18.2.3）、可选的接口基规范（§18.2.4）、可选类型参数约束子句规范（§15.2.5）以及接口主体（§18.3）组成，后面可选跟一个分号。

接口声明不得提供类型参数约束子句，除非它同时提供类型参数列表。

提供类型参数列表的接口声明是泛型接口声明。

### 18.2.2 接口修饰符

接口声明可以选择性地包含一系列接口修饰符：

```
interface-modifiers:
    interface-modifier
    interface-modifiers interface-modifier

interface-modifier:
    new
    public
    protected
    internal
    private
```

同一修饰符在接口声明中出现多次是编译时错误。

允许（§8.5.2）。当分部类型声明（§15.2.7）包含可访问性规范（通过 public、protected、internal 和 private 修饰符）时，适用 §15.2.2 中的规则。

### 18.2.3 变体类型参数列表

### 18.2.3.1 概述

变体类型参数列表只能出现在接口和委托类型上。与普通类型参数列表的区别在于每个类型参数上可选的变体批注。

```
variant-type-parameter-list:
    < variant-type-parameters >
variant-type-parameters:
    attributesopt variance-annotationopt type-parameter
    variant-type-parameters , attributesopt variance-annotationopt type-parameter
variance-annotation:
    in
    out
```

如果变体批注为 out，则称该类型参数是协变的。如果变体批注为 in，则称该类型参数是逆变的。如果没有变体批注，则称该类型参数是不变的。

[示例：在以下代码中：

```
interface C<out X, in Y, Z>
{
    X M(Y y);
    Z P { get; set; }
}
```

X 是协变的，Y 是逆变的，Z 是不变的。示例结束]

如果泛型接口分多个部分声明（§15.2.3），则每个分部声明应为每个类型参数指定相同的变体。

### 18.2.3.2 变体安全性

类型的类型参数列表中出现的变体批注限制了类型在类型声明中可以出现的位置。

如果满足以下条件之一，则类型 T 是输出不安全的：

- T 是逆变类型参数
- T 是元素类型为输出不安全的数组类型
- T 是由泛型类型 S<X1, ..., Xk> 构造的接口或委托类型 S<A1, ..., Ak>，其中对于至少一个 Ai，满足以下条件之一：
  - Xi 是协变或不变的，且 Ai 是输出不安全的。
  - Xi 是逆变或不变的，且 Ai 是输入不安全的。

如果满足以下条件之一，则类型 T 是输入不安全的：

- T 是协变类型参数
- T 是元素类型为输入不安全的数组类型
- T 是由泛型类型 S<X1, ..., Xk> 构造的接口或委托类型 S<A1, ..., Ak>，其中对于至少一个 Ai，满足以下条件之一：
  - Xi 是协变或不变的，且 Ai 是输入不安全的。




IComboBox 的基接口是 IControl、ITextBox 和 IListBox。换句话说，上述 IComboBox 接口继承了成员 SetText 和 SetItems 以及 Paint。结束示例]

从构造的泛型类型继承的成员在类型替换后继承。也就是说，成员中的任何构成类型都将基类声明的类型参数替换为类基规范中使用的相应类型参数。[示例：以下代码中

```
interface IBase<T>
{
    T[] Combine(T a, T b);
}
interface IDerived : IBase<string[,]>
{
    // Inherited: string[,] Combine(string[,] a, string[,] b);
}
```

接口 IDerived 在类型参数 T 被替换为 string[,] 后继承 Combine 方法。结束示例]

实现接口的类或结构也隐式地实现了该接口的所有基接口。

部分接口声明 (§15.2.7) 中接口在多个部分上的处理在 §15.2.4.3 中进一步讨论。

接口的每个基接口都应是输出安全的 (§18.2.3.2)。

## 18.3 接口体

接口的 interface-body 定义了接口的成员。

```
interface-body:
    { interface-member-declarationsopt }
```

## 18.4 接口成员

### 18.4.1 通用

接口的成员是继承自基接口的成员以及接口本身声明的成员。

```
interface-member-declarations:
    interface-member-declaration
    interface-member-declarations interface-member-declaration

interface-member-declaration:
    interface-method-declaration
    interface-property-declaration
    interface-event-declaration
    interface-indexer-declaration
```

接口声明声明零个或多个成员。接口的成员应为方法、属性、事件或索引器。接口不能包含常量、字段、运算符、实例构造函数、终结器或类型，也不能包含任何种类的静态成员。

所有接口成员隐式具有公共访问。接口成员声明包含任何修饰符是编译时错误。

interface-declaration 创建一个新的声明空间 (§8.3)，并且 interface-declaration 直接包含的类型参数和 interface-member-declarations 在此声明空间中引入新成员。以下规则适用于 interface-member-declarations：

-   接口声明的类型参数列表中的类型参数的名称应与同一类型参数列表中的所有其他类型参数的名称不同，并且应与接口的所有成员的名称不同。
-   方法的名称应与同一接口中声明的所有属性和事件的名称不同。此外，方法的签名 (§8.6) 应与同一接口中声明的所有其他方法的签名不同，并且同一接口中声明的两个方法不得仅因 ref 和 out 而签名不同。
-   属性或事件的名称应与同一接口中声明的所有其他成员的名称不同。
-   索引器的签名应与同一接口中声明的所有其他索引器的签名不同。

接口的继承成员明确不属于接口的声明空间的一部分。因此，接口允许声明与继承成员具有相同名称或签名的成员。当这种情况发生时，派生接口成员被认为隐藏了基接口成员。隐藏继承成员不被视为错误，但会导致编译器发出警告。为了抑制警告，派生接口成员的声明应包含 new 修饰符以指示派生成员旨在隐藏基成员。此主题在 §8.7.2.3 中进一步讨论。

如果在不隐藏继承成员的声明中包含 new 修饰符，则会发出相应警告。通过移除 new 修饰符可抑制此警告。

[注意：严格来说，class object 中的成员不是任何接口的成员 (§18.4)。然而，class object 中的成员可通过任何接口类型的成员查找 (§12.5) 获得。结束注意]

在多个部分 (§15.2.7) 中声明的接口的成员集合是各部分中声明的成员的并集。接口声明的所有部分的主体共享相同的声明空间 (§8.3)，并且每个成员的范围 (§8.7) 扩展到所有部分的主体。

### 18.4.2 接口方法

接口方法使用 interface-method-declarations 声明：

```
interface-method-declaration:
    attributesopt newopt return-type identifier type-parameter-listopt
        ( formal-parameter-listopt ) type-parameter-constraints-clausesopt ;
```

接口方法声明的属性、return-type、identifier 和 formal-parameter-list 与类 (§15.6) 中的方法声明具有相同的含义。接口方法声明不允许指定方法体，因此声明始终以分号结束。interface-method-declaration 除非同时具有 type-parameter-list，否则不得具有 type-parameter-constraints-clauses。

接口方法的每个形式参数类型应为输入安全 (§18.2.3.2)，并且返回类型应为 void 或输出安全。此外，任何 out 或 ref 形式参数类型也应为输出安全。[注意：即使是 out 参数也要求为输入安全，这是由于常见的实现限制。结束注意]此外，方法任何类型参数上的每个类类型约束、接口类型约束和类型参数约束都应为输入安全。

这些规则确保接口的任何协变或逆变使用仍然是类型安全的。[示例：

```
interface I<out T> { void M<U>() where U : T; }
```

是格式错误的，因为 T 作为 U 的类型参数约束上的使用不是输入安全的。

如果没有此限制，就可能以以下方式违反类型安全：

```
class B {}
class D : B {}
class E : B {}
class C : I<D> { public void M<U>() {...} }
... I<B> b = new C();
b.M<E>();
```

这实际上是对 C.M<E> 的调用。但该调用要求 E 派生自 D，因此这里的类型安全将被违反。结束示例]

### 18.4.3 接口属性

接口属性使用 interface-property-declarations 声明：

```
interface-property-declaration:
    attributesopt newopt type identifier { interface-accessors }
interface-accessors:
    attributesopt get ;
    attributesopt set ;
    attributesopt get ; attributesopt set ;
    attributesopt set ; attributesopt get ;
```

接口属性声明的属性、type 和 identifier 与类 (§15.7) 中的属性声明具有相同的含义。

接口属性声明的访问器对应于类属性声明 (§15.7.3) 的访问器，只是访问器体始终为分号。因此，访问器仅指示属性是读写、只读还是只写。

如果接口属性具有 get 访问器，则其类型应为输出安全；如果具有 set 访问器，则其类型应为输入安全。

### 18.4.4 接口事件

接口事件使用 interface-event-declarations 声明：

```
interface-event-declaration:
    attributesopt newopt event type identifier ;
```

接口事件声明的属性、type 和 identifier 与类 (§15.8) 中的事件声明具有相同的含义。

接口事件的类型应为输入安全。

### 18.4.5 接口索引器

接口索引器使用 interface-indexer-declarations 声明：

```
interface-indexer-declaration:
    attributesopt newopt type this [ formal-parameter-list ] { interface-accessors }
```

接口索引器声明的属性、type 和 formal-parameter-list 与类 (§15.9) 中的索引器声明具有相同的含义。

接口索引器声明的访问器对应于类索引器声明 (§15.9) 的访问器，只是访问器体始终为分号。因此，访问器仅指示索引器是读写、只读还是只写。

接口索引器的所有形式参数类型都应为输入安全。此外，任何 out 或 ref 形式参数类型也应为输出安全。[注意：即使是 out 参数也要求为输入安全，这是由于常见的实现限制。结束注意]




接口索引器的类型如果有 get 访问器则应为输出安全，如果有 set 访问器则应为输入安全。

### 18.4.6 接口成员访问

接口成员是通过成员访问 (§12.7.5) 和索引器访问 (§12.7.7.3) 表达式以 I.M 和 I[A] 的形式访问的，其中 I 是接口类型，M 是该接口类型的方法、属性或事件，A 是索引器参数列表。

对于严格单继承的接口（继承链中的每个接口恰好有零个或一个直接基接口），成员查找 (§12.5)、方法调用 (§12.7.6.2) 和索引器访问 (§12.7.7.3) 规则的效果与类和结构完全相同：更派生的成员会隐藏具有相同名称或签名的更低层成员。然而，对于多继承接口，当两个或多个不相关的基接口声明具有相同名称或签名的成员时，可能会出现歧义。本小节展示了若干示例，其中一些会导致歧义，而另一些则不会。在所有情况下，都可以使用显式转换来解决歧义。

[Example: 以下代码中

```csharp
interface IList
{
    int Count { get; set; }
}
interface ICounter
{
    void Count(int i);
}
interface IListCounter: IList, ICounter {}
class C
{
    void Test(IListCounter x) {
        x.Count(1);        // Error
        x.Count = 1;       // Error
        ((IList)x).Count = 1;   // Ok, invokes IList.Count.set
        ((ICounter)x).Count(1); // Ok, invokes ICounter.Count
    }
}
```

前两个语句会导致编译时错误，因为在 IListCounter 中 Count 的成员查找 (§12.5) 是不明确的。如示例所示，通过将 x 转换为适当的基接口类型可以解决歧义。此类转换没有运行时成本——它们仅在编译时将实例视为更低派生类型。 end example]

[Example: 以下代码中

```csharp
interface IInteger
{
    void Add(int i);
}
interface IDouble
{
    void Add(double d);
}
interface INumber: IInteger, IDouble {}

class C
{
    void Test(INumber n) {
        n.Add(1);            // Invokes IInteger.Add
        n.Add(1.0);          // Only IDouble.Add is applicable
        ((IInteger)n).Add(1); // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);  // Only IDouble.Add is a candidate
    }
}
```

调用 n.Add(1) 通过应用 §12.6.4 的重载解析规则选择 IInteger.Add。类似地，调用 n.Add(1.0) 选择 IDouble.Add。当插入显式转换时，只有一个候选方法，因此没有歧义。 end example]

[Example: 以下代码中

```csharp
interface IBase
{
    void F(int i);
}
interface ILeft: IBase
{
    new void F(int i);
}
interface IRight: IBase
{
    void G();
}
interface IDerived: ILeft, IRight {}
class A
{
    void Test(IDerived d) {
        d.F(1);               // Invokes ILeft.F
        ((IBase)d).F(1);      // Invokes IBase.F
        ((ILeft)d).F(1);      // Invokes ILeft.F
        ((IRight)d).F(1);     // Invokes IBase.F
    }
}
```

IBase.F 成员被 ILeft.F 成员隐藏。因此调用 d.F(1) 选择 ILeft.F，即使 IBase.F 在通过 IRight 导致访问路径中似乎未被隐藏。

多继承接口中隐藏的直观规则很简单：只要成员在任何访问路径中被隐藏，它就在所有访问路径中被隐藏。因为从 IDerived 到 ILeft 再到 IBase 的访问路径隐藏了 IBase.F，所以该成员也在从 IDerived 到 IRight 再到 IBase 的访问路径中被隐藏。 end example]

## 18.5 限定接口成员名称

接口成员有时通过其限定接口成员名称引用。接口成员的限定名称由声明该成员的接口的名称、一个点以及成员的名称组成。成员的限定名称引用声明该成员的接口。[Example: 给定以下声明

```csharp
interface IControl
{
    void Paint();
}
interface ITextBox: IControl
{
    void SetText(string text);
}
```

Paint 的限定名称为 IControl.Paint，SetText 的限定名称为 ITextBox.SetText。在上面的示例中，不可能将 Paint 引用为 ITextBox.Paint。 end example

当接口属于命名空间的一部分时，限定接口成员名称可以包含命名空间名称。[Example:

```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

在 System 命名空间内，ICloneable.Clone 和 System.ICloneable.Clone 都是 Clone 方法的限定接口成员名称。 end example]

## 18.6 接口实现

### 18.6.1 通用

接口可以由类和结构实现。为了表示类或结构直接实现接口，接口包含在该类或结构的基类列表中。[Example:

```csharp
interface ICloneable
{
    object Clone();
}
interface IComparable
{
    int CompareTo(object other);
}
class ListEntry: ICloneable, IComparable
{
    public object Clone() {...}
    public int CompareTo(object other) {...}
}
```

end example]

直接实现接口的类或结构还隐式实现该接口的所有基接口。即使类或结构在基类列表中没有显式列出所有基接口也是如此。[Example:

```csharp
interface IControl
{
    void Paint();
}
interface ITextBox: IControl
{
    void SetText(string text);
}
class TextBox: ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

在这里，类 TextBox 同时实现了 IControl 和 ITextBox。 end example]

当类 C 直接实现接口时，从 C 派生的所有类也隐式实现该接口。

类声明中指定的基接口可以是构造接口类型 (§9.4, §18.2)。

[Example: 以下代码说明了类如何实现构造接口类型：

```csharp
class C<U,V> {}
interface I1<V> {}
class D: C<string,int>, I1<string> {}
class E<U>: C<U,int>, I1<U> {}
```

end example]

泛型类声明的基接口应满足 §18.6.3 中描述的唯一性规则。

### 18.6.2 显式接口成员实现

为了实现接口的目的，类或结构可以声明显式接口成员实现。显式接口成员实现是对引用限定接口成员名称的方法、属性、事件或索引器声明。[Example:

```csharp
interface IList<T>
{
    T[] GetElements();
}
interface IDictionary<K,V>
{
    V this[K key];
    void Add(K key, V value);
}
class List<T>: IList<T>, IDictionary<int,T>
{
    public T[] GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

这里 `IDictionary<int,T>.this` 和 `IDictionary<int,T>.Add` 是显式接口成员实现。 end example]

[Example: 在某些情况下，接口成员的名称可能不适合实现类，在这种情况下，接口成员可以使用显式接口成员实现来实现。例如，实现文件抽象的类很可能会实现一个 `Close` 成员函数，其效果是释放文件资源，并使用显式接口成员实现实现 `IDisposable` 接口的 `Dispose` 方法：

```csharp
interface IDisposable
{
    void Dispose();
}
class MyFile: IDisposable
{
    void IDisposable.Dispose()
    {
        Close();
    }
    public void Close()
    {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

end example]

不可能通过其限定接口成员名称在方法调用、属性访问、事件访问或索引器访问中访问显式接口成员实现。显式接口成员实现只能通过接口实例访问，在这种情况下仅通过其成员名称引用。

如果显式接口成员实现包含除 extern 或 async 之外的任何修饰符 (§15.6)，则为编译时错误。

如果显式接口方法实现包含 *type-parameter-constraints-clauses*，则为编译时错误。泛型显式接口方法实现的约束继承自接口方法。[Note: 显式接口成员实现与其他成员具有不同的可访问性特征。因为显式接口成员实现永远无法通过方法调用或属性访问中的限定接口成员名称访问，所以在某种意义上它们是私有的。然而，由于它们可以通过接口访问，所以在某种意义上它们也与声明它们的接口一样公开。

显式接口成员实现主要有两个目的：

- 因为显式接口成员实现无法通过类或结构实例访问，所以它们允许接口实现被排除在类或结构的公共接口之外。这在类或结构实现对该类或结构的消费者不感兴趣的内部接口时特别有用。
- 显式接口成员实现允许对具有相同签名的接口成员进行消歧。没有显式接口成员实现，类或结构就不可能对具有相同签名和返回类型的接口成员具有不同的实现，因为类或结构就不可能对具有相同签名但返回类型不同的接口成员有任何实现。

end note]

对于显式接口成员实现有效，类或结构必须在其基类列表中命名一个包含成员的接口，该成员的限定接口成员名称、类型、类型参数数量和参数类型与显式接口成员实现完全匹配。如果接口函数成员具有参数数组，则相关显式接口成员实现的相应参数允许但不是必须具有 params 修饰符。如果接口函数成员没有参数数组，则相关显式接口成员实现不得具有参数数组。[Example: 因此，在以下类中

```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...}    // invalid
}
```

IComparable.CompareTo 的声明导致编译时错误，因为 IComparable 未列在 Shape 的基类列表中，也不是 ICloneable 的基接口。同样，在以下声明中

```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
}
class Ellipse: Shape
{
    object ICloneable.Clone() {...}    // invalid
}
```

Ellipse 中 ICloneable.Clone 的声明会导致编译时错误，因为 ICloneable 并未显式列在 Ellipse 的基类列表中。end example]

显式接口成员实现的限定接口成员名称应引用该成员被声明的接口。[Example: 因此，在以下声明中

```
interface IControl
{
    void Paint();
}
interface ITextBox: IControl
{
    void SetText(string text);
}
class TextBox: ITextBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
}
```

Paint 的显式接口成员实现必须写成 IControl.Paint，而不是 ITextBox.Paint。end example]

## 18.6.3 已实现接口的唯一性

泛型类型声明所实现的接口对于所有可能构造的类型都应保持唯一。没有此规则，就无法确定某些构造类型的正确调用方法。[Example: 假设允许泛型类声明写成如下形式：

```
interface I<T>
{
    void F();
}
class X<U,V>: I<U>, I<V>    // Error: I<U> and I<V> conflict
{
    void I<U>.F() {...}
    void I<V>.F() {...}
}
```

如果允许这样做，则在以下情况下将无法确定执行哪段代码：

```
I<int> x = new X<int,int>();
x.F();
```

end example]

为了确定泛型类型声明的接口列表是否有效，执行以下步骤：

- 将 L 设为在泛型类、结构或接口声明 C 中直接指定的接口列表。
- 将 L 中已存在接口的任何基接口添加到 L。
- 从 L 中删除任何重复项。
- 如果从 C 创建的任何可能构造类型在将类型参数代入 L 之后会导致 L 中的两个接口相同，则 C 的声明无效。确定所有可能的构造类型时不考虑约束声明。

[Note: 在上面的类声明 X 中，接口列表 L 由 I<U> 和 I<V> 组成。该声明无效，因为 U 和 V 为相同类型的任何构造类型都会导致这两个接口成为相同的类型。end note]

不同继承级别指定的接口可能统一：

```
interface I<T>
{
    void F();
}
class Base<U>: I<U>
{
    void I<U>.F() {...}
}
class Derived<U,V>: Base<U>, I<V>  // Ok
{
    void I<V>.F() {...}
}
```

此代码有效，即使 Derived<U,V> 同时实现了 I<U> 和 I<V>。代码

```
I<int> x = new Derived<int,int>();
x.F();
```

调用 Derived 中的方法，因为 Derived<int,int> 有效地重新实现了 I<int>（§18.6.7）。

## 18.6.4 泛型方法的实现

当泛型方法隐式实现接口方法时，每个方法类型参数给出的约束在两个声明中应等价（在用适当的类型参数替换任何接口类型参数之后），其中方法类型参数按从左到右的序数位置标识。[Example: 在以下代码中：

```
interface I<X, Y, Z>
{
    void F<T>(T t) where T: X;
    void G<T>(T t) where T: Y;
    void H<T>(T t) where T: Z;
}

class C: I<object,C,string>
{
    public void F<T>(T t) {...}          // Ok
    public void G<T>(T t) where T: C {...}   // Ok
    public void H<T>(T t) where T: string {...} // Error
}
```

方法 C.F<T> 隐式实现 I<object,C,string>.F<T>。在这种情况下，C.F<T> 不需要（也不允许）指定约束 T: object，因为 object 是所有类型参数的隐式约束。方法 C.G<T> 隐式实现 I<object,C,string>.G<T>，因为在用相应的类型参数替换接口类型参数后，约束与接口中的约束匹配。方法 C.H<T> 的约束是错误，因为密封类型（本例中为 string）不能用作约束。省略约束也是错误，因为隐式接口方法实现的约束必须匹配。因此，不可能隐式实现 I<object,C,string>.H<T>。此接口方法只能使用显式接口成员实现来实现：

```
class C: I<object,C,string>
{
    ...
    public void H<U>(U u) where U: class {...}
    void I<object,C,string>.H<T>(T t) {
        string s = t;  // Ok
        H<T>(t);
    }
}
```

在这种情况下，显式接口成员实现调用具有严格更弱约束的公共方法。从 t 到 s 的赋值是有效的，因为 T 继承了 T: string 的约束，即使该约束在源代码中无法表达。end example]

[Note: 当泛型方法显式实现接口方法时，实现方法上不允许有约束（§15.7.1, §18.6.2）end note]。

## 18.6.5 接口映射

类或结构应提供基类列表中列出的接口的所有成员的实现。在实现类或结构中查找接口成员实现的过程称为 *接口映射*。

对于类或结构 C 的接口映射，会为 C 的基类列表中指定的每个接口的每个成员定位一个实现。特定接口成员 I.M 的实现，其中 I 是声明成员 M 的接口，是通过检查每个类或结构 S 确定的，从 C 开始并对 C 的每个后续基类重复，直到找到匹配项：

- 如果 S 包含与 I 和 M 匹配的显式接口成员实现声明，则该成员是 I.M 的实现。
- 否则，如果 S 包含与 M 匹配的非静态公共成员声明，则该成员是 I.M 的实现。如果有多个成员匹配，则未指定哪个成员是 I.M 的实现。这种情况只能发生在 S 为构造类型时，其中两个成员在泛型类型中声明的签名不同，但类型参数使它们的签名相同。

如果无法为 C 的基类列表中指定的所有接口的所有成员定位实现，则会发生编译时错误。接口的成员包括从基接口继承的成员。

构造接口类型的成员被认为已将任何类型参数替换为 §15.3.3 中指定的相应类型参数。[Example: 例如，给定泛型接口声明：

```
interface I<T>
{
    T F(int x, T[,] y);
    T this[int y] { get; }
}
```

构造接口 I<string[]> 具有以下成员：

```
string[] F(int x, string[,][] y);
string[] this[int y] { get; }
```

end example

就接口映射而言，类或结构成员 A 与接口成员 B 匹配的条件为：

- A 和 B 都是方法，并且 A 和 B 的名称、类型和形式参数列表相同。
- A 和 B 都是属性，并且 A 和 B 的名称和类型相同，且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。
- A 和 B 都是事件，并且 A 和 B 的名称和类型相同。
- A 和 B 都是索引器，并且 A 和 B 的类型和形式参数列表相同，且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。

接口映射算法的显著含义是：

- 在确定实现接口成员的类或结构成员时，显式接口成员实现优先于同一类或结构中的其他成员。
- 非公共成员和静态成员均不参与接口映射。

[Example: 在以下代码中

```
interface ICloneable
{
    object Clone();
}
class C: ICloneable
{
    object ICloneable.Clone() {...}
    public object Clone() {...}
}
```

C 的 ICloneable.Clone 成员成为 ICloneable 中 Clone 的实现，因为显式接口成员实现优先于其他成员。end example]

如果类或结构实现两个或多个包含具有相同名称、类型和参数类型的成员的接口，则可以将这些接口成员中的每一个映射到单个类或结构成员。[Example:

```
interface IControl
{
    void Paint();
}
interface IForm
{
    void Paint();
}
class Page: IControl, IForm
{
    public void Paint() {...}
}
```

在这里，IControl 和 IForm 的 Paint 方法都映射到 Page 中的 Paint 方法。当然，也可以为这两种方法分别提供显式接口成员实现。end example]

如果类或结构实现包含隐藏成员的接口，则某些成员可能需要通过显式接口成员实现来实现。[Example:

```
interface IBase
{
    int P { get; }
}
interface IDerived: IBase
{
    new int P();
}
```

此接口的实现至少需要一个显式接口成员实现，并将采用以下形式之一

```
class C: IDerived
{
    int IBase.P { get {...} }
    int IDerived.P() {...}
}
class C: IDerived
{
    public int P { get {...} }
    int IDerived.P() {...}
}
class C: IDerived
{
    int IBase.P { get {...} }



    } public int P() {...}

结束示例]
当一个类实现多个具有相同基接口的接口时，基接口只能有一个实现。[示例：在以下代码中
```
interface IControl
{
    void Paint();
}
interface ITextBox: IControl
{
    void SetText(string text);
}
interface IListBox: IControl
{
    void SetItems(string[] items);
}
class ComboBox: IControl, ITextBox, IListBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
    void IListBox.SetItems(string[] items) {...}
}
```
不可能为基类列表中命名的 IControl、由 ITextBox 继承的 IControl 以及由 IListBox 继承的 IControl 分别提供实现。事实上，这些接口没有单独身份的概念。相反，ITextBox 和 IListBox 的实现共享同一个 IControl 实现，并且 ComboBox 仅被视为实现了三个接口，IControl、ITextBox 和 IListBox。结束示例]

基类成员参与接口映射。[示例：在以下代码中
```
interface Interface1
{
    void F();
}
class Class1
{
    public void F() {}
    public void G() {}
}
class Class2: Class1, Interface1
{
    new public void G() {}
}
```
Class1 中的方法 F 用于 Class2 对 Interface1 的实现中。结束示例]

## 18.6.6 接口实现继承

一个类继承其基类提供的所有接口实现。

如果不显式重新实现接口，派生类就无法以任何方式更改其从基类继承的接口映射。[示例：在以下声明中
```
interface IControl
{
    void Paint();
}
class Control: IControl
{
    public void Paint() {...}
}
class TextBox: Control
{
    new public void Paint() {...}
}
```
TextBox 中的 Paint 方法隐藏了 Control 中的 Paint 方法，但它并未更改 Control.Paint 到 IControl.Paint 的映射，并且通过类实例和接口实例对 Paint 的调用将产生以下效果
```
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();    // invokes Control.Paint();
t.Paint();    // invokes TextBox.Paint();
ic.Paint();   // invokes Control.Paint();
it.Paint();   // invokes Control.Paint();
```
结束示例]

然而，当接口方法映射到类中的虚方法时，派生类可以重写该虚方法并更改接口的实现。[示例：将上述声明重写为
```
interface IControl
{
    void Paint();
}
class Control: IControl
{
    public virtual void Paint() {...}
}
class TextBox: Control
{
    public override void Paint() {...}
}
```
现在将观察到以下效果
```
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();    // invokes Control.Paint();
t.Paint();    // invokes TextBox.Paint();
ic.Paint();   // invokes Control.Paint();
it.Paint();   // invokes TextBox.Paint();
```
结束示例]

由于显式接口成员实现不能声明为虚，因此无法重写显式接口成员实现。然而，显式接口成员实现调用另一个方法完全有效，并且该其他方法可以声明为虚以允许派生类重写它。[示例：
```
interface IControl
{
    void Paint();
}
class Control: IControl
{
    void IControl.Paint() { PaintControl(); }
    protected virtual void PaintControl() {...}
}
class TextBox: Control
{
    protected override void PaintControl() {...}
}
```
在这里，从 Control 派生的类可以通过重写 PaintControl 方法来专门化 IControl.Paint 的实现。结束示例

## 18.6.7 接口重新实现

继承接口实现的类允许通过将其包含在基类列表中来重新实现该接口。

接口的重新实现遵循与接口的初始实现完全相同的接口映射规则。因此，继承的接口映射对为接口重新实现建立的接口映射没有任何影响。[示例：在以下声明中
```
interface IControl
{
    void Paint();
}
class Control: IControl
{
    void IControl.Paint() {...}
}
class MyControl: Control, IControl
{
    public void Paint() {}
}
```
Control 将 IControl.Paint 映射到 Control.IControl.Paint 这一事实并不影响 MyControl 中的重新实现，后者将 IControl.Paint 映射到 MyControl.Paint。结束示例]

继承的公共成员声明和继承的显式接口成员声明参与重新实现接口的接口映射过程。[示例：
```
interface IMethods
{
    void F();
    void G();
    void H();
    void I();
}
class Base: IMethods
{
    void IMethods.F() {}
    void IMethods.G() {}
    public void H() {}
    public void I() {}
}
class Derived: Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```
在这里，Derived 中 IMethods 的实现将接口方法映射到 Derived.F、Base.IMethods.G、Derived.IMethods.H 和 Base.I。结束示例]

当一个类实现一个接口时，它隐式地也实现了该接口的所有基接口。同样，接口的重新实现也隐式地是对该接口的所有基接口的重新实现。[示例：
```
interface IBase
{
    void F();
}
interface IDerived: IBase
{
    void G();
}
class C: IDerived
{
    void IBase.F() {...}
    void IDerived.G() {...}
}
class D: C, IDerived
{
    public void F() {...}
    public void G() {...}
}
```
在这里，IDerived 的重新实现也重新实现了 IBase，将 IBase.F 映射到 D.F。结束示例

## 18.6.8 抽象类和接口

与非抽象类一样，抽象类应提供其基类列表中列出的接口的所有成员的实现。然而，抽象类允许将接口方法映射到抽象方法。[示例：
```
interface IMethods
{
    void F();
    void G();
}
abstract class C: IMethods
{
    public abstract void F();
    public abstract void G();
}
```
在这里，IMethods 的实现将 F 和 G 映射到抽象方法，这些方法应在派生自 C 的非抽象类中被重写。结束示例

显式接口成员实现不能是抽象的，但显式接口成员实现当然允许调用抽象方法。[示例：
```
interface IMethods
{
    void F();
    void G();
}
abstract class C: IMethods
{
    void IMethods.F() { FF(); }
    void IMethods.G() { GG(); }
    protected abstract void FF();
    protected abstract void GG();
}
```
在这里，派生自 C 的非抽象类将被要求重写 FF 和 GG，从而提供 IMethods 的实际实现。结束示例

## 19. 枚举

### 19.1 通用

枚举类型是一种不同的值类型（§9.2），它声明了一组命名常量。[示例：示例
```
enum Color
{
    Red,
    Green,
    Blue
}
```
声明了一个名为 Color 的枚举类型，其成员为 Red、Green 和 Blue。结束示例]

### 19.2 枚举声明

枚举声明声明一个新的枚举类型。枚举声明以关键字 enum 开头，并定义枚举的名称、可访问性、底层类型和成员。
```
enum-declaration:
    attributesopt enum-modifierSopt enum identifier enum-baseopt enum-body ;opt

enum-base:
    : integral-type

enum-body:
    { enum-member-declarationSopt }
    { enum-member-declarations , }
```
每个枚举类型都有一个对应的整型，称为枚举类型的底层类型。该底层类型应能够表示枚举中定义的所有枚举值。枚举声明可以显式声明底层类型为 byte、sbyte、short、ushort、int、uint、long 或 ulong。[注意：char 不能用作底层类型。结束注意] 未显式声明底层类型的枚举声明的底层类型为 int。

[示例：示例
```
enum Color: long
{
    Red,
    Green,
    Blue
}
```
声明了一个底层类型为 long 的枚举。结束示例] [注意：开发人员可能会选择使用 long 作为底层类型，如示例中所示，以便能够使用在 long 范围内但不在 int 范围内的值，或为将来保留此选项。结束注意]

[注意：C# 允许在 enum-body 中使用尾随逗号，就像它允许在数组初始化器（§17.7）中一样。结束注意]

### 19.3 枚举修饰符

enum-declaration 可选择包含一系列 enum 修饰符：
```
enum-modifiers:
    enum-modifier
    enum-modifiers enum-modifier
```




```
enum-modifier:
  new
  public
  protected
  internal
  private
```

在枚举声明中，同一修饰符多次出现属于编译时错误。

枚举声明的修饰符与类声明的修饰符含义相同（§15.2.2）。但是，枚举声明中不允许使用 `abstract`、`sealed` 和 `static` 修饰符。枚举不能是抽象的，也不允许派生。

## 19.4 枚举成员

枚举类型声明的主体定义零个或多个枚举成员，这些成员是枚举类型的命名常量。任意两个枚举成员不能具有相同的名称。

```
enum-member-declarations:
  enum-member-declaration
  enum-member-declarations , enum-member-declaration

enum-member-declaration:
  attributes_opt identifier
  attributes_opt identifier = constant-expression
```

每个枚举成员都有一个关联的常量值。该值的类型是包含它的枚举的基础类型。每个枚举成员的常量值必须位于该枚举的基础类型的范围内。[示例：下面的示例

```
enum Color: uint
{
    Red = -1,
    Green = -2,
    Blue = -3
}
```

会导致编译时错误，因为常量值 -1、-2 和 -3 不在基础整型类型 uint 的范围内。示例结束]

多个枚举成员可以共享相同的关联值。[示例：下面的示例

```
enum Color
{
    Red,
    Green,
    Blue,
    Max = Blue
}
```

展示了一个枚举，其中两个枚举成员——Blue 和 Max——具有相同的关联值。示例结束]

枚举成员的关联值是隐式或显式赋值的。如果枚举成员的声明具有常量表达式初始化器，则将该常量表达式的值隐式转换为枚举的基础类型后，即为该枚举成员的关联值。如果枚举成员的声明没有初始化器，则其关联值按如下方式隐式设置：

- 如果该枚举成员是枚举类型中声明的第一个枚举成员，则其关联值为零。
- 否则，该枚举成员的关联值通过将文本顺序上紧邻的前一个枚举成员的关联值加 1 获得。增加后的值必须位于基础类型可表示的值的范围内，否则会发生编译时错误。

[示例：下面的示例

```
using System;
enum Color
{
    Red,
    Green = 10,
    Blue
}
class Test
{
    static void Main() {
        Console.WriteLine(StringFromColor((Color.Red)));
        Console.WriteLine(StringFromColor((Color.Green)));
        Console.WriteLine(StringFromColor((Color.Blue)));
    }
    static string StringFromColor(Color c) {
        switch (c) {
            case Color.Red:
                return String.Format("Red = {0}", (int) c);
            case Color.Green:
                return String.Format("Green = {0}", (int) c);
            case Color.Blue:
                return String.Format("Blue = {0}", (int) c);
            default:
                return "Invalid color";
        }
    }
}
```

打印出枚举成员名称及其关联值。输出为：

```
Red = 0
Green = 10
Blue = 11
```

原因如下：

- 枚举成员 Red 被自动赋值为零（因为它没有初始化器，并且是第一个枚举成员）；
- 枚举成员 Green 被显式赋值为 10；
- 枚举成员 Blue 被自动赋值为文本上紧邻其前的成员值加 1。

示例结束]

枚举成员的关联值不能直接或间接使用其自身关联枚举成员的值。除了这种循环限制之外，枚举成员初始化器可以自由引用其他枚举成员初始化器，无论其文本位置如何。在枚举成员初始化器内部，其他枚举成员的值始终被视为具有其基础类型的类型，因此在引用其他枚举成员时不需要进行强制转换。

[示例：下面的示例

```
enum Circular
{
    A = B,
    B
}
```

会导致编译时错误，因为 A 和 B 的声明是循环的。A 显式依赖于 B，而 B 隐式依赖于 A。示例结束]

枚举成员的命名和作用域方式与类中的字段完全类似。枚举成员的作用域是包含它的枚举类型的主体。在该作用域内，可以通过简单名称引用枚举成员。在所有其他代码中，枚举成员的名称必须用其枚举类型的名称限定。枚举成员没有任何声明的可访问性——如果包含它的枚举类型是可访问的，则该枚举成员是可访问的。

## 19.5 System.Enum 类型

类型 System.Enum 是所有枚举类型的抽象基类（这与枚举类型的基础类型不同且不同义），从 System.Enum 继承的成员可在任何枚举类型中使用。存在从任何枚举类型到 System.Enum 的装箱转换（§11.2.8），以及从 System.Enum 到任何枚举类型的取消装箱转换（§11.3.6）。

请注意，System.Enum 本身并不是枚举类型。相反，它是一个类类型，所有枚举类型都派生自它。类型 System.Enum 继承自类型 System.ValueType（§9.3.2），而 System.ValueType 又继承自类型 object。在运行时，System.Enum 类型的值可以为 null，也可以是对任何枚举类型的装箱值的引用。

## 19.6 枚举值和运算

每个枚举类型都定义一个不同的类型；在枚举类型与整型之间，或在两个枚举类型之间进行转换时，需要进行显式枚举转换（§11.3.3）。枚举类型的值的集合与基础类型的值的集合相同，并且不限于命名常量的值。枚举的基础类型的任何值都可以强制转换为该枚举类型，并且是该枚举类型的一个不同的有效值。

枚举成员具有其包含的枚举类型的类型（在其他枚举成员初始化器内部除外：参见 §19.4）。在枚举类型 E 中声明的、关联值为 v 的枚举成员，其值为 (E)v。

以下运算符可用于枚举类型的值：

- ==、!=、<、>、<=、>=（§12.11.6）
- 二元 +（§12.9.5）
- 二元 -（§12.9.6）
- ^、&、|（§12.12.3）
- ~（§12.8.5）
- ++、--（§12.7.10 和 §12.8.6）
- sizeof（§23.6.9）

每个枚举类型都自动派生自类 System.Enum（后者又派生自 System.ValueType 和 object）。因此，该类的继承方法和属性可用于枚举类型的值。

## 20. 委托

### 20.1 概述

委托声明定义一个派生自类 System.Delegate 的类。委托实例封装一个调用列表，该列表是一个或多个方法的列表，每个方法都称为一个可调用实体。对于实例方法，可调用实体由一个实例和该实例上的一个方法组成。对于静态方法，可调用实体仅由一个方法组成。使用适当的参数集调用委托实例，会导致该委托的每个可调用实体都使用给定的参数集被调用。

> [注意：委托实例的一个有趣且有用的属性是，它不知道也不关心它所封装的方法的类；重要的是这些方法与委托的类型兼容（§20.4）。这使得委托非常适合“匿名”调用。注意结束]

### 20.2 委托声明

委托声明是一种类型声明（§14.7），用于声明新的委托类型。

```
delegate-declaration:
    attributes_opt delegate-modifiers_opt delegate return-type
    identifier variant-type-parameter-list_opt
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;
```

```
delegate-modifiers:
    delegate-modifier
    delegate-modifiers delegate-modifier
```

delegate-modifier：
- new
- public
- protected
- internal
- private

在委托声明中，同一修饰符多次出现属于编译时错误。

委托声明不得提供 type-parameter-constraints-clauses，除非它还提供了 variant-type-parameter-list。

提供 variant-type-parameter-list 的委托声明是泛型委托声明。

`new` 修饰符仅允许用于在另一个类型内声明的委托，在这种情况下，它指定该委托隐藏同名的继承成员，如 §15.3.5 所述。

`public`、`protected`、`internal` 和 `private` 修饰符控制委托类型的可访问性。根据委托声明出现的上下文，其中某些修饰符可能不被允许（§8.5.2）。

委托的类型名称是 identifier。

可选的 formal-parameter-list 指定委托的参数，return-type 指示委托的返回类型。

可选的 variant-type-parameter-list（§18.2.3）指定委托本身的类型参数。

委托类型的返回类型必须是 `void`，或者是输出安全的（§18.2.3.2）。




All the formal parameter types of a delegate type shall be input-safe. In addition, any out or ref parameter types shall also be output-safe. [Note: 即使是 out 参数也要求是输入安全的，这是由于常见的实现限制。end note]

C# 中的委托类型按名称等价，而不是按结构等价。

示例：

```csharp
delegate int D1(int i, double d);
delegate int D2(int c, double d);
```

委托类型 D1 和 D2 是两种不同的类型，因此即使它们的签名相同，也不可互换。结束示例

与其它泛型类型声明类似，需要提供类型参数来创建构造的委托类型。构造的委托类型的参数类型和返回类型是通过为委托声明中的每个类型参数替换构造的委托类型的相应类型参数而创建的。

声明委托类型的唯一方式是通过委托声明。每个委托类型都是派生自 System.Delegate 的引用类型。每个委托类型所需成员的细节在 §20.3 中说明。委托类型是隐式密封的，因此不允许从委托类型派生任何类型。也不允许声明派生自 System.Delegate 的非委托类类型。System.Delegate 本身不是委托类型；它是一个类类型，所有委托类型都派生自它。

### 20.3 委托成员

每个委托类型都继承自 Delegate 类的成员，如 §15.3.4 所描述。此外，每个委托类型必须提供一个非泛型的 Invoke 方法，其参数列表与委托声明中的形式参数列表匹配，其返回类型与委托声明中的返回类型匹配。Invoke 方法的可访问性至少应与包含的委托类型相同。在委托类型上调用 Invoke 方法在语义上等同于使用委托调用语法 (§20.6)。

实现可以在委托类型中定义额外的成员。

除实例化外，可以应用于类或类实例的任何操作也可以分别应用于委托类或实例。特别是，可以通过通常的成员访问语法访问 System.Delegate 类型的成员。

### 20.4 委托兼容性

方法或委托类型 M 与委托类型 D 兼容的条件是以下所有条件都为真：

- D 和 M 具有相同数量的参数，并且 D 中的每个参数都具有与 M 中对应参数相同的 ref 或 out 修饰符。
- 对于每个值参数（没有 ref 或 out 修饰符的参数），从 D 中的参数类型到 M 中对应参数类型存在恒等转换 (§11.2.2) 或隐式引用转换 (§11.2.7)。
- 对于每个 ref 或 out 参数，D 中的参数类型与 M 中的参数类型相同。
- 从 M 的返回类型到 D 的返回类型存在恒等转换或隐式引用转换。

此一致性定义允许返回类型的协变和参数类型的逆变。

示例：

```csharp
delegate int D1(int i, double d);
delegate int D2(int c, double d);
delegate object D3(string s);

class A
{
    public static int M1(int a, double b) {...}
}
class B
{
    public static int M1(int f, double g) {...}
    public static void M2(int k, double l) {...}
    public static int M3(int g) {...}
    public static void M4(int g) {...}
    public static object M5(string s) {...}
    public static int[] M6(object o) {...}
}
```

方法 A.M1 和 B.M1 都与委托类型 D1 和 D2 兼容，因为它们具有相同的返回类型和参数列表。方法 B.M2、B.M3 和 B.M4 与委托类型 D1 和 D2 不兼容，因为它们具有不同的返回类型或参数列表。方法 B.M5 和 B.M6 都与委托类型 D3 兼容。结束示例]

示例：

```csharp
delegate bool Predicate<T>(T value);

class X
{
    static bool F(int i) {...}
    static bool G(string s) {...}
}
```

方法 X.F 与委托类型 Predicate<int> 兼容，方法 X.G 与委托类型 Predicate<string> 兼容。结束示例]

[Note: 委托兼容性的直观含义是，如果每次委托的调用都可以用该方法调用替换而不违反类型安全，则该方法与委托类型兼容，将可选参数和参数数组视为显式参数。例如，在以下代码中：

```csharp
delegate void Action<T>(T arg);
class Test {
    static void Print(object value) {
        Console.WriteLine(value);
    }
    static void Main() {
        Action<string> log = Print;
        log("text");
    }
}
```

Print 方法与 Action<string> 委托类型兼容，因为任何 Action<string> 委托的调用也都是 Print 方法的有效调用。

如果将上述 Print 方法的签名改为例如 Print(object value, bool prependTimestamp = false)，则根据本条款的规则，Print 方法将不再与 Action<string> 兼容。end note]

### 20.5 委托实例化

委托的实例由 *委托创建表达式* (§12.7.11.6)、转换为委托类型、委托组合或委托移除创建。新建的委托实例随后引用以下一项或多项：

- *委托创建表达式* 中引用的静态方法，或
- 目标对象（不能为 *空*）和 *委托创建表达式* 中引用的实例方法，或
- 另一个委托 (§12.7.11.6)。

示例：

```csharp
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public void M2(int i) {...}
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);    // static method
        C t = new C();
        D cd2 = new D(t.M2);    // instance method
        D cd3 = new D(cd2);     // another delegate
    }
}
```

结束示例

由委托实例封装的方法集合称为 *调用列表*。当委托实例由单个方法创建时，它封装该方法，其调用列表仅包含一个条目。然而，当两个非 *空* 委托实例组合时，它们的调用列表会按左操作数然后右操作数的顺序连接，形成一个新的调用列表，其中包含两个或更多条目。

当从单个委托创建新委托时，结果的调用列表只有一个条目，即源委托 (§12.7.11.6)。

委托使用二元 + (§12.9.5) 和 += 运算符 (§12.18.3) 进行组合。委托可以使用二元 - (§12.9.6) 和 -= 运算符 (§12.18.3) 从委托组合中移除。委托可以进行相等比较 (§12.11.9)。

示例：以下示例展示了多个委托的实例化及其对应的调用列表：

```csharp
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public static void M2(int i) {...}
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);    // M1 - one entry in invocation list
        D cd2 = new D(C.M2);    // M2 - one entry
        D cd3 = cd1 + cd2;      // M1 + M2 - two entries
        D cd4 = cd3 + cd1;      // M1 + M2 + M1 - three entries
        D cd5 = cd4 + cd3;      // M1 + M2 + M1 + M1 + M2 - five entries
        D td3 = new D(cd3);     // [M1 + M2] - ONE entry in invocation
                                // list, which is itself a list of two methods.
        D td4 = td3 + cd1;      // [M1 + M2] + M1 - two entries
        D cd6 = cd4 - cd2;      // M1 + M1 - two entries in invocation list
        D td6 = td4 - cd2;      // [M1 + M2] + M1 - two entries in
                                // invocation list, but still three methods called, M2 not removed.
    }
}
```

当 cd1 和 cd2 被实例化时，它们各自封装一个方法。当 cd3 被实例化时，它具有两个方法的调用列表，分别为 M1 和 M2，按此顺序。cd4 的调用列表包含 M1、M2 和 M1，按此顺序。对于 cd5，调用列表包含 M1、M2、M1、M1 和 M2，按此顺序。

使用委托创建表达式从另一个委托创建委托时，结果的调用列表与原始列表结构不同，但会导致以相同顺序调用相同的方法。当 td3 由 cd3 创建时，其调用列表只有一个成员，但该成员是方法 M1 和 M2 的列表，并且这些方法由 td3 调用的顺序与由 cd3 调用的顺序相同。类似地，当 td4 被实例化时，其调用列表只有两个条目，但它按 M1、M2 和 M1 的顺序调用三个方法，就像 cd4 一样。

方法列表的结构会影响委托减法。委托 cd6 由从 cd4（调用 M1、M2 和 M1）中减去 cd2（调用 M2）创建，调用 M1 和 M1。然而委托 td6 由从 td4（调用 M1、M2 和 M1）中减去 cd2（调用 M2）创建，仍然按顺序调用 M1、M2 和 M1，因为 M2 不是列表中的单个条目，而是嵌套列表的成员。

有关组合（以及移除）委托的更多示例，请参阅 §20.6。结束示例

一旦实例化，委托实例始终引用相同的调用列表。[Note: 请记住，当两个委托组合或一个从另一个中移除时，会产生一个具有自己调用列表的新委托；被组合或移除的委托的调用列表保持不变。end note]

### 20.6 委托调用

C# 提供了用于调用委托的特殊语法。当调用调用列表包含一个条目的非空委托实例时，它使用相同的参数调用该方法，并返回被引用方法相同的返回值。（有关委托调用的详细信息，请参阅 §12.7.6.4。）如果在调用此类委托期间发生异常，并且该异常未在被调用的方法内捕获，则异常捕获子句的搜索将继续在调用委托的方法中，就好像该方法直接调用了该委托引用的方法一样。

调用列表包含多个条目的委托实例的调用会按顺序同步调用调用列表中的每个方法。每个被调用的方法都传递与委托实例相同的参数集。如果此类委托调用包含引用参数 (§15.6.2.3)，则每次方法调用都将使用对同一变量的引用；调用列表中一个方法对该变量的更改将对调用列表中后面的方法可见。如果委托调用包含输出参数或返回值，则其最终值来自列表中最后一个委托的调用。如果在处理此类委托的调用期间发生异常，并且该异常未在被调用的方法内捕获，则异常捕获子句的搜索将继续在调用委托的方法中，并且调用列表中后面的任何方法都不会被调用。

尝试调用值为 null 的委托实例会引发 System.NullReferenceException 类型的异常。

示例：以下示例展示了如何实例化、组合、移除和调用委托：

```csharp
using System;
```



```
delegate void D(int x);
class C
{
    public static void M1(int i) {
        Console.WriteLine("C.M1: " + i);
    }
    public static void M2(int i) {
        Console.WriteLine("C.M2: " + i);
    }

    public void M3(int i) {
        Console.WriteLine("C.M3: " + i);
    }
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);
        cd1(-1);    // call M1

        D cd2 = new D(C.M2);
        cd2(-2);    // call M2

        D cd3 = cd1 + cd2;
        cd3(10);    // call M1 then M2

        cd3 += cd1;
        cd3(20);    // call M1, M2, then M1

        C c = new C();
        D cd4 = new D(c.M3);
        cd3 += cd4;
        cd3(30);    // call M1, M2, M1, then M3

        cd3 -= cd1; // remove last M1
        cd3(40);    // call M1, M2, then M3

        cd3 -= cd4;
        cd3(50);    // call M1 then M2

        cd3 -= cd2;
        cd3(60);    // call M1
        cd3 -= cd2; // impossible removal is benign
        cd3(60);    // call M1

        cd3 -= cd1; // invocation list is empty so cd3 is null
        // cd3(70);  // System.NullReferenceException thrown
        cd3 -= cd1; // impossible removal is benign
    }
}
```

如语句 cd3 += cd1; 所示，一个委托可以在调用列表中出现多次。在这种情况下，它会按出现次数各调用一次。在此类调用列表中，当该委托被移除时，实际被移除的是调用列表中最后一次出现的位置。

在最后一条语句 cd3 -= cd1; 执行之前，委托 cd3 引用的是一个空的调用列表。尝试从空列表中移除一个委托（或从非空列表中移除一个不存在的委托）不会导致错误。

The output produced is:

```
C.M1: -1
C.M2: -2

C.M1: 10
C.M2: 10

C.M1: 20
C.M2: 20
C.M1: 20

C.M1: 30
C.M2: 30
C.M1: 30
C.M3: 30

C.M1: 40
C.M2: 40
C.M3: 40

C.M1: 50
C.M2: 50

C.M1: 60
C.M1: 60
```

end example]

## 21. 异常

### 21.1 通用

C# 中的异常提供了一种结构化、统一且类型安全的方式来处理系统级和应用级的错误条件。

### 21.2 异常的原因

异常可以通过两种不同的方式抛出。

- throw 语句 (§13.10.6) 会立即且无条件地抛出异常。控制流永远不会到达 throw 之后的下一条语句。
- 在处理 C# 语句和表达式期间出现的某些异常条件会在操作无法正常完成时在某些情况下导致异常抛出。[示例：整数除法操作 (§12.9.3) 如果分母为零则会抛出 System.DivideByZeroException。end example] 请参阅 §21.5 以了解以这种方式可能发生的各种异常的列表。

### 21.3 System.Exception 类

System.Exception 类是所有异常的基础类型。该类具有一些所有异常共有的显著属性：

- Message 是类型为 string 的只读属性，包含异常原因的可读描述。
- InnerException 是类型为 Exception 的只读属性。如果其值非 null，则引用导致当前异常的异常。（即，当前异常是在处理 InnerException 的 catch 块中引发的。）否则，其值为 null，表示此异常不是由另一个异常引起的。以这种方式链接在一起的异常对象的数量可以是任意的。

这些属性的值可以在对 System.Exception 的实例构造函数调用中指定。

### 21.4 异常如何被处理

异常由 try 语句 (§13.11) 处理。

当异常发生时，系统会根据异常的运行时类型搜索最近的可以处理该异常的 catch 子句。首先在当前方法中搜索词法上包围的 try 语句，并按顺序考虑该 try 语句关联的 catch 子句。如果失败，则在调用当前方法的方法中搜索词法上包围的 try 语句。此搜索会一直继续，直到找到可以处理当前异常的 catch 子句为止，该子句通过命名与被抛出的异常的运行时类型相同或为其基类的异常类来处理。未命名异常类的 catch 子句可以处理任何异常。

一旦找到匹配的 catch 子句，系统就会准备将控制权转移到该 catch 子句的第一条语句。在 catch 子句执行开始之前，系统首先按顺序执行与比捕获异常的 try 语句嵌套更深的 try 语句关联的任何 finally 子句。

如果没有找到匹配的 catch 子句：

- 如果搜索匹配的 catch 子句到达静态构造函数 (§15.12) 或静态字段初始化器，则会在触发静态构造函数调用的位置抛出 System.TypeInitializationException。System.TypeInitializationException 的内部异常包含最初抛出的异常。
- 否则，如果在终结器执行期间发生异常且该异常未被捕获，则行为未指定。
- 否则，如果搜索匹配的 catch 子句到达最初启动线程的代码，则线程的执行将被终止。此类终止的影响由实现定义。

### 21.5 常见异常类

以下异常由某些 C# 操作抛出。

| 异常 | 描述 |
|---|---|
| System.ArithmeticException | 用于在算术运算期间发生的异常的基类，例如 System.DivideByZeroException 和 System.OverflowException。 |
| System.ArrayTypeMismatchException | 当向数组存储失败，因为存储元素的类型与数组的类型不兼容时抛出。 |
| System.DivideByZeroException | 当尝试将整数值除以零时抛出。 |
| System.IndexOutOfRangeException | 当尝试通过小于零或超出数组边界的索引来索引数组时抛出。 |
| System.InvalidCastException | 当从基类型或接口到派生类型的显式转换在运行时失败时抛出。 |
| System.NullReferenceException | 当空引用以需要引用对象的方式使用时抛出。 |
| System.OutOfMemoryException | 当尝试分配内存（通过 new）失败时抛出。 |
| System.OverflowException | 当在检查上下文中的算术运算溢出时抛出。 |
| System.StackOverflowException | 当执行栈因挂起的调用过多而耗尽时抛出；通常表示递归非常深或无界。 |
| System.TypeInitializationException | 当静态构造函数或静态字段初始化器抛出异常且不存在 catch 子句来捕获它时抛出。 |

## 22. 属性

### 22.1 通用

C# 语言的大部分功能使程序员能够指定程序中定义的实体的声明性信息。例如，类中方法的访问性是通过用方法修饰符 public、protected、internal 和 private 对其进行装饰来指定的。

C# 使程序员能够发明新的声明性信息类型，称为属性。然后程序员可以将属性附加到各种程序实体，并在运行时环境中检索属性信息。[注意：例如，一个框架可能会定义一个 HelpAttribute 属性，该属性可以放置在某些程序元素（如类和方法）上，以提供这些程序元素与其文档之间的映射。end note]

属性是通过属性类的声明来定义的 (§22.2)，属性类可以具有位置参数和命名参数 (§22.2.3)。属性使用属性规范 (§22.3) 附加到 C# 程序中的实体，并且可以在运行时作为属性实例 (§22.4) 检索。

### 22.2 属性类

#### 22.2.1 通用

派生自抽象类 System.Attribute 的类，无论是直接还是间接，都称为属性类。属性类的声明定义了一种可以放置在程序实体上的新属性类型。根据惯例，属性类以 Attribute 为后缀命名。使用属性时可以包含或省略此后缀。

泛型类声明不得将 System.Attribute 用作直接或间接基类。[示例:
```
using System;
public class B : Attribute {}
public class C<T> : B {}  // Error - generic cannot be an attribute
```
end example]

#### 22.2.2 属性用法

属性 AttributeUsage (§22.5.2) 用于描述属性类如何被使用。

AttributeUsage 具有一个位置参数 (§22.2.3)，使属性类能够指定其可以使用的程序实体的种类。[示例：示例
```
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute
{ ... }
```



显示 Simple 属性的几种用法。虽然该属性以 SimpleAttribute 的名称定义，但在使用该属性时，可以省略 Attribute 后缀，从而得到简短名称 Simple。因此，上面的示例在语义上等价于以下内容

```
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

结束示例

AttributeUsage 有一个命名参数 (§22.2.3)，称为 AllowMultiple，用于指示属性是否可以对给定实体指定多次。如果属性类的 AllowMultiple 为 true，则该属性类为多用属性类，可以在实体上指定多次。如果属性类的 AllowMultiple 为 false 或未指定，则该属性类为单用属性类，最多只能在实体上指定一次。

[示例：示例

```
using System;
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute: Attribute
{
    private string name;
    public AuthorAttribute(string name) {
        this.name = name;
    }
    public string Name {
        get { return name; }
    }
}
```

定义了一个名为 AuthorAttribute 的多用属性类。示例

```
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1 {...}
```

显示了一个类声明，其中使用了两次 Author 属性。结束示例

AttributeUsage 还有另一个命名参数 (§22.2.3)，称为 Inherited，用于指示属性在基类上指定时是否也会被派生该基类的类继承。如果属性类的 Inherited 为 true，则该属性会被继承。如果属性类的 Inherited 为 false，则该属性不会被继承。如果未指定，其默认值是 true。

未附加 AttributeUsage 属性的属性类 X，如

```
using System;
class X: Attribute { ... }
```

等价于以下内容：

```
using System;
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute { ... }
```

## 22.2.3 位置参数和命名参数

属性类可以具有位置参数和命名参数。属性类的每个公共实例构造函数都为该属性类定义了一个有效的位置参数序列。属性类的每个非静态公共读写字段和属性都为该属性类定义一个命名参数。属性的两个访问器都需要是公共的，属性才能定义命名参数。

[示例：示例

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute: Attribute
{
    public HelpAttribute(string url) { // url is a positional parameter
    }
    public string Topic {  // Topic is a named parameter
        get {...}
        set {...}
    }
    public string Url { get {...} }
}
```

定义了一个名为 HelpAttribute 的属性类，该类有一个位置参数 url 和一个命名参数 Topic。尽管 Url 属性是非静态且公共的，但它不定义命名参数，因为它不是可读写的。

该属性类可能按如下方式使用：

```
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
}

[Help("http://www.mycompany.com/.../Misc.htm", Topic ="Class2")]
class Class2
{
}
```

结束示例]

## 22.2.4 属性参数类型

属性类的位置参数和命名参数的类型限于属性参数类型，具体为：

- 以下类型之一：bool、byte、char、double、float、int、long、sbyte、short、string、uint、ulong、ushort。
- 类型 object。
- 类型 System.Type。
- 枚举类型。
- 上述类型的单维数组。

构造函数参数或公共字段如果不具有这些类型之一，则不得在属性规范中用作位置参数或命名参数。

## 22.3 属性规范

**属性规范** 是将先前定义的属性应用于程序实体的操作。属性是为程序实体指定的额外声明性信息。属性可以在全局作用域指定（用于指定包含的程序集或模块上的属性），以及用于 *类型声明* (§14.7)、*类成员声明* (§15.3)、*接口成员声明* (§18.4)、*结构成员声明* (§16.3)、*枚举成员声明* (§19.2)、*访问器声明* (§15.7.3)、*事件访问器声明* (§15.8)、*形式参数列表* (§15.6.2) 的元素以及 *类型参数列表* (§15.2.3) 的元素。

属性在 *属性节* 中指定。属性节由一对方括号组成，其周围环绕着一个或多个属性的以逗号分隔的列表。在此类列表中指定属性的顺序，以及附加到同一程序实体的节的排列顺序，均不重要。例如，属性规范 [A] [B]、[B] [A]、[A, B] 和 [B, A] 是等价的。

```
global-attributes:
    global-attribute-sections

global-attribute-sections:
    global-attribute-section
    global-attribute-sections global-attribute-section

global-attribute-section:
    [ global-attribute-target-specifier attribute-list ]
    [ global-attribute-target-specifier attribute-list , ]

global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    identifier equal to assembly or module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-sections attribute-section

attribute-section:
    [ attribute-target-specifier_opt attribute-list ]
    [ attribute-target-specifier_opt attribute-list , ]

attribute-target-specifier:
    attribute-target :

attribute-target:
    identifier not equal to assembly or module
    keyword

attribute-list:
    attribute
    attribute-list , attribute

attribute:
    attribute-name attribute-arguments_opt

attribute-name:
    type-name
```

```
attribute-arguments:
  ( positional-argument-list_opt )
  ( positional-argument-list , named-argument-list )
  ( named-argument-list )
positional-argument-list:
  positional-argument
  positional-argument-list , positional-argument
positional-argument:
  argument-name_opt attribute-argument-expression
named-argument-list:
  named-argument
  named-argument-list , named-argument
named-argument:
  identifier = attribute-argument-expression
attribute-argument-expression:
  expression
```

对于上述产生式 global-attribute-target 和 attribute-target，以及下文中的内容，引用的相等性是指 §7.4.3 中定义的相等性。

属性由属性名和可选的位置参数和命名参数列表组成。位置参数（如果有）位于命名参数之前。位置参数由 attribute-argument-expression 组成；命名参数由名称、等号和 attribute-argument-expression 组成，其组合受与简单赋值相同的规则约束。命名参数的顺序不重要。

> [注意：为方便起见，global-attribute-section 和 attribute-section 中允许使用尾随逗号，就像在数组初始化器 (§17.7) 中允许使用一样。结束注释]

attribute-name 标识一个属性类。

当属性放置在全局级别时，需要 global-attribute-target-specifier。当 global-attribute-target 等于：

- assembly – 目标是包含的程序集
- module – 目标是包含的模块

不允许 global-attribute-target 的其他值。

标准化的 attribute-target 名称为 event、field、method、param、property、return、type 和 typevar。这些目标名称只能在以下上下文中使用：

- event — 一个事件。
- field — 一个字段。类似字段的事件（即没有访问器的事件）也可以具有此目标的属性。
- method — 构造函数、终结器、方法、运算符、属性 get 和 set 访问器、索引器 get 和 set 访问器，以及事件 add 和 remove 访问器。类似字段的事件（即没有访问器的事件）也可以具有此目标的属性。
- param — 属性 set 访问器、索引器 set 访问器、事件 add 和 remove 访问器，以及构造函数、方法、运算符中的参数。
- property — 一个属性和一个索引器。
- return — 委托、方法、运算符、属性 get 访问器和索引器 get 访问器。



- `type` — 一个委托、类、结构体、枚举和接口。
- `typevar` — 一个类型参数。

某些上下文允许在多个目标上指定属性。程序可以通过包含 *属性目标说明符* 来显式指定目标。如果没有 *属性目标说明符*，则应用默认值，但可以使用 *属性目标说明符* 来确认或覆盖默认值。上下文的解析如下：

- 对于委托声明上的属性，默认目标是委托。否则当属性目标等于时：
  - `type` — 目标是委托
  - `return` — 目标是返回值
- 对于方法声明上的属性，默认目标是方法。否则当 *属性目标* 等于时：
  - `method` — 目标是方法
  - `return` — 目标是返回值
- 对于运算符声明上的属性，默认目标是运算符。否则当 *属性目标* 等于时：
  - `method` — 目标是运算符
  - `return` — 目标是返回值
- 对于属性或索引器声明的 get 访问器声明上的属性，默认目标是相关方法。否则当 *属性目标* 等于时：
  - `method` — 目标是相关方法
  - `return` — 目标是返回值
- 对于属性或索引器声明的 set 访问器上指定的属性，默认目标是相关方法。否则当 *属性目标* 等于时：
  - `method` — 目标是相关方法
  - `param` — 目标是唯一的隐式参数
- 对于省略事件访问器声明的事件声明上指定的属性，默认目标是事件声明。否则当 *属性目标* 等于时：
  - `event` — 目标是事件声明
  - `field` — 目标是字段
  - `method` — 目标是方法
- 在事件声明未省略事件访问器声明的情况下，默认目标是方法。
  - `method` — 目标是相关方法
  - `param` — 目标是唯一的参数

在所有其他上下文中，包含 *属性目标说明符* 是允许的但不必要。[*示例:* 一个类声明可以包含或省略说明符 *类型*:]

```
[type: Author("Brian Kernighan")]
class Class1 {}
[Author("Dennis Ritchie")]
class Class2 {}
```

示例结束。

实现可以接受其他属性目标，其用途由实现定义。不识别此类属性目标的实现应发出警告并忽略包含的属性部分。

按惯例，属性类以 Attribute 为后缀命名。属性名可以包含或省略此后缀。具体而言，属性名按如下方式解析：

- 如果属性名的最右标识符是逐字标识符（§7.4.3），则属性名被解析为类型名（§8.8）。如果结果不是派生自 System.Attribute 的类型，则会发生编译时错误。
- 否则，
  - 属性名被解析为类型名（§8.8），但任何错误都被抑制。如果此解析成功并且结果是派生自 System.Attribute 的类型，则该类型是此步骤的结果。
  - 将字符 Attribute 追加到属性名中最右的标识符，并将 resulting token 字符串解析为类型名（§8.8），但任何错误都被抑制。如果此解析成功并且结果是派生自 System.Attribute 的类型，则该类型是此步骤的结果。

如果上述两个步骤中恰好有一个导致派生自 System.Attribute 的类型，则该类型是属性名的结果。否则会发生编译时错误。

[示例: 如果同时找到带有和不带此后缀的属性类，则存在歧义，并会导致编译时错误。如果属性名的拼写使得其最右标识符是逐字标识符（§7.4.3），则仅匹配不带后缀的属性，从而能够解决此类歧义。示例

```
using System;
[AttributeUsage(AttributeTargets.All)]
public class Example: Attribute
{}
[AttributeUsage(AttributeTargets.All)]
public class ExampleAttribute: Attribute
{}
[Example]          // Error: ambiguity
class Class1 {}
[ExampleAttribute]  // Refers to ExampleAttribute
class Class2 {}
[@Example]          // Refers to Example
class Class3 {}
[@ExampleAttribute]  // Refers to ExampleAttribute
class Class4 {}
```

显示了两个名为 Example 和 ExampleAttribute 的属性类。属性 [Example] 是模棱两可的，因为它可能指 Example 或 ExampleAttribute。使用逐字标识符允许在这种罕见情况下指定确切的意图。属性 [ExampleAttribute] 不存在歧义

（尽管如果存在名为 ExampleAttributeAttribute 的属性类则会存在歧义）。如果删除类 Example 的声明，则两个属性都引用名为 ExampleAttribute 的属性类，如下所示：

```
using System;
[AttributeUsage(AttributeTargets.All)]
public class ExampleAttribute: Attribute
{
}
[Example]            // Refers to ExampleAttribute
class Class1 {}
[ExampleAttribute]   // Refers to ExampleAttribute
class Class2 {}
[@Example]           // Error: no attribute named "Example"
class Class3 {}
```

示例结束

对同一实体多次使用单次使用属性类是编译时错误。[示例: 示例

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute: Attribute
{
    string value;
    public HelpStringAttribute(string value) {
        this.value = value;
    }
    public string Value { get {...} }
}
[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]
public class Class1 {}
```

会导致编译时错误，因为它尝试在 Class1 的声明上多次使用 HelpString，而 HelpString 是一个单次使用属性类。示例结束

表达式 E 是属性参数表达式当且仅当满足以下所有条件时：

- E 的类型是属性参数类型（§22.2.4）。
- 在编译时，E 的值可以解析为以下之一：
  - 一个常量值。
  - 使用 typeof 表达式（§12.7.12）获得的 System.Type 对象，该表达式指定非泛型类型、闭合构造类型（§9.4.3）或非绑定泛型类型（§9.4.4），但不是开放类型（§9.4.3）。
  - 属性参数表达式的单维数组。

[示例:

```
using System;
[AttributeUsage(AttributeTargets.Class)]
public class TestAttribute: Attribute
{
    public int P1 {
        get {...}
        set {...}
    }
}
```

```
public Type P2 {
    get {...}
    set {...}
}
public object P3 {
    get {...}
    set {...}
}
[Test(P1 = 1234, P3 = new int[]{1, 3, 5}, P2 = typeof(float))]
class MyClass {}
class C<T> {
    [My(P2 = typeof(T))]    // Error - T not a closed type.
    int x1;
    [My(P2 = typeof(C<T>))]    // Error - C<T> not a closed type.
    int x2;
    [My(P2 = typeof(C<int>))]    // Ok
    int x3;
    [My(P2 = typeof(C<>))]    // Ok
    int x4;
}
```

示例结束

声明在多个部分中的类型的属性是通过以未指定顺序组合其每个部分的属性来确定的。如果在多个部分上放置相同的属性，则等同于在该类型上多次指定该属性。[示例: 两个部分：

```
[Attr1, Attr2("hello")]
partial class A {}
[Attr3, Attr2("goodbye")]
partial class A {}
```

等同于以下单个声明：

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

示例结束

类型参数上的属性以相同方式组合。

## 22.4 属性实例

### 22.4.1 通用

属性实例是表示运行时属性的实例。属性由属性类、位置参数和命名参数定义。属性实例是属性类的实例，其使用位置参数和命名参数进行初始化。

获取属性实例涉及编译时和运行时的处理，如以下小节所述。

### 22.4.2 属性的编译

具有属性类 T、位置参数列表 P、命名参数列表 N 并指定在程序实体 E 上的属性的编译通过以下步骤编译为程序集 A：

-   遵循编译形式为 new T(P) 的对象创建表达式时的编译时处理步骤。这些步骤要么导致编译时错误，要么确定 T 上可在运行时调用的实例构造函数 C。
-   如果 C 不具有公共可访问性，则发生编译时错误。
-   对于 N 中的每个命名实参 Arg：
  -   令 Name 为命名实参 Arg 的标识符。
  -   Name 应标识 T 上的非静态可读可写公共字段或属性。如果 T 没有此类字段或属性，则发生编译时错误。
-   如果位置实参列表 P 中的任一值或命名实参列表 N 中的任一值的类型为 System.String，并且该值不符合 Unicode 标准定义的良构形式，则编译后的值是否等于检索到的运行时值（§22.4.3）由实现定义。[注意：例如，一个包含高代理项 UTF-16 代码单元且其后未紧跟低代理项代码单元的字符串不是良构的。结束注意]
-   编译器在编译包含该特性的程序后，将以下信息（用于在运行时实例化该特性）存储到程序集的输出中：特性类 T、T 上的实例构造函数 C、位置实参列表 P、命名实参列表 N 以及关联的程序实体 E，并且这些值在编译时完全解析。

### 22.4.3 特性实例的运行时检索

由 T、C、P 和 N 表示并与 E 关联的特性实例，可以在运行时使用以下步骤从程序集 A 中检索：

-   遵循执行形式为 new T(P) 的对象创建表达式时的运行时处理步骤，使用实例构造函数 C 以及编译时确定的值。这些步骤要么导致异常，要么生成 T 的实例 O。
-   按顺序对 N 中的每个命名实参 Arg：
  -   令 Name 为命名实参 Arg 的标识符。如果 Name 未标识 O 上的非静态公共可读写字段或属性，则引发异常。
  -   令 Value 为对 Arg 的特性实参表达式求值的结果。
  -   如果 Name 标识 O 上的字段，则将此字段设置为 Value。
  -   否则，Name 标识 O 上的属性。将此属性设置为 Value。
  -   结果为 O，即特性类 T 的一个实例，已用位置实参列表 P 和命名实参列表 N 初始化。

> [注意：在 A 中存储 T、C、P、N（并将其与 E 关联）的格式，以及指定 E 并从 A 中检索 T、C、P、N 的机制（并由此说明如何在运行时获得特性实例），超出了本标准的范围。结束注意]

[示例：在 CLI 的某个实现中，可通过以下程序检索由编译 §22.2.3 中的示例程序所创建的程序集中的 Help 特性实例：]

```csharp
using System;
using System.Reflection;

public sealed class InterrogateHelpUrls
{
    public static void Main(string[] args) {
        Type helpType = typeof(HelpAttribute);
        string assemblyName = args[0];
        foreach (Type t in Assembly.Load(assemblyName).GetTypes()) {
            Console.WriteLine("Type : {0}", t.ToString());
            HelpAttribute[] helpers =
                (HelpAttribute[])t.GetCustomAttributes(helpType, false);
            for (int at = 0; at != helpers.Length; at++) {
                Console.WriteLine("\tUrl  : {0}", helpers[at].Url);
            }
        }
    }
}
```

结束示例]

## 22.5 保留特性

### 22.5.1 概述

少量特性会以某种方式影响语言。这些特性包括：

-   System.AttributeUsageAttribute（§22.5.2），用于描述特性类可被使用的方式。
-   System.Diagnostics.ConditionalAttribute（§22.5.3）是一种可多次使用的特性类，用于定义条件方法和条件特性类。此特性通过测试条件编译符号来指示条件。
-   System.ObsoleteAttribute（§22.5.4），用于将成员标记为过时。
-   System.Runtime.CompilerServices.CallerLineNumberAttribute（§22.5.2）、System.Runtime.CompilerServices.CallerFilePathAttribute（§22.5.5.3）和 System.Runtime.CompilerServices.CallerMemberNameAttribute（§22.5.5.4），用于向可选参数提供有关调用上下文的信息。

执行环境可提供影响 C# 程序执行的、特定于实现的其他特性。

### 22.5.2 AttributeUsage 特性

AttributeUsage 特性用于描述特性类可被使用的方式。

用 AttributeUsage 特性修饰的类应直接或间接派生自 System.Attribute。否则，发生编译时错误。

[注意：有关使用此特性的示例，请参见 §22.2.2。结束注意]

### 22.5.3 Conditional 特性

### 22.5.3.1 概述

Conditional 特性支持定义条件方法和条件特性类。

### 22.5.3.2 条件方法

用 Conditional 特性修饰的方法是条件方法。因此，每个条件方法都与其 Conditional 特性中声明的条件编译符号关联。[示例：

```csharp
using System.Diagnostics;
class Eg
{
    [Conditional("ALPHA")]
    [Conditional("BETA")]
    public static void M() { //...
    }
}
```

将 Eg.M 声明为与两个条件编译符号 ALPHA 和 BETA 关联的条件方法。结束示例]

如果在调用点定义了一个或多个与条件方法关联的条件编译符号，则包含对该条件方法的调用；否则省略该调用。

条件方法受以下限制：

-   条件方法应是类声明或结构声明中的方法。如果在接口声明中的方法上指定 Conditional 特性，则发生编译时错误。
-   条件方法的返回类型应为 void。
-   条件方法不得用 override 修饰符标记。但条件方法可以用 virtual 修饰符标记。对此类方法的重写隐式具有条件性，并且不得显式用 Conditional 特性标记。
-   条件方法不得是接口方法的实现。否则，发生编译时错误。
-   条件方法的参数不得带有 out 修饰符。

此外，如果从条件方法创建委托，则发生编译时错误。

[示例：以下示例

```csharp
#define DEBUG
using System;
using System.Diagnostics;
class Class1
{
    [Conditional("DEBUG")]
    public static void M() {
        Console.WriteLine("Executed Class1.M");
    }
}
class Class2
{
    public static void Test() {
        Class1.M();
    }
}
```

将 Class1.M 声明为条件方法。Class2 的 Test 方法调用此方法。由于定义了条件编译符号 DEBUG，如果调用 Class2.Test，它就会调用 M。如果未定义符号 DEBUG，那么 Class2.Test 就不会调用 Class1.M。结束示例]

重要的是要理解，是否包含对条件方法的调用由调用点的条件编译符号控制。[示例：在以下代码中

```csharp
// File class1.cs
using System.Diagnostics;

class Class1
{
    [Conditional("DEBUG")]
    public static void F() {
        Console.WriteLine("Executed Class1.F");
    }
}

// File class2.cs
#define DEBUG
class Class2
{
    public static void G() {
        Class1.F();    // F is called
    }
}

// File class3.cs
#undef DEBUG
class Class3
{
    public static void H() {
        Class1.F();    // F is not called
    }
}
```

类 Class2 和 Class3 都包含对条件方法 Class1.F 的调用，该方法是否具有条件性取决于是否定义了 DEBUG。由于该符号在 Class2 的上下文中已定义，但在 Class3 中未定义，因此包含 Class2 中对 F 的调用，而省略 Class3 中对 F 的调用。结束示例]

在继承链中使用条件方法可能会令人困惑。通过 base 以 base.M 形式对条件方法进行的调用，遵循正常的条件方法调用规则。[示例：在以下代码中

```csharp
// File class1.cs
using System;
using System.Diagnostics;
class Class1
{
    [Conditional("DEBUG")]
    public virtual void M() {
        Console.WriteLine("Class1.M executed");
    }
}

// File class2.cs
using System;
class Class2 : Class1{
    public override void M() {
        Console.WriteLine("Class2.M executed");
        base.M();            // base.M is not called!
    }
}
```



// File class3.cs
#define DEBUG
using System;
class class3
{
    public static void Test() {
        Class2 c = new Class2();    // M is called
        c.M();
    }
}

Class2 包含对其基类中定义的 M 的调用。该调用被省略，因为基类方法是基于符号 DEBUG 是否存在而设定的条件方法，而 DEBUG 未定义。因此，该方法仅向控制台写入“Class2.M executed”。如果明智地使用预处理器声明，则可以消除此类问题。示例结束

## 22.5.3.3 条件特性类

一个使用一个或多个 Conditional 特性修饰的特性类（§22.2）即为条件特性类。因此，条件特性类与其 Conditional 特性中声明的条件编译符号相关联。

```
[Example:
    using System;
    using System.Diagnostics;
    [Conditional("ALPHA")]
    [Conditional("BETA")]
    public class TestAttribute : Attribute {}
```

将 TestAttribute 声明为与条件编译符号 ALPHA 和 BETA 相关联的条件特性类。示例结束

如果在规范指定点定义了条件特性的一个或多个关联条件编译符号，则包含该条件特性的特性规范（§22.3）；否则，省略该特性规范。

需要特别注意的是，条件特性类的特性规范包含还是排除，由规范指定点的条件编译符号控制。[示例：在以下示例中

```
File test.cs:
    using System;
    using System.Diagnostics;
    [Conditional("DEBUG")]
    public class TestAttribute : Attribute {}

File class1.cs:
    #define DEBUG
    [Test]    // TestAttribute is specified
    class class1 {}

File class2.cs:
    #undef DEBUG
    [Test]    // TestAttribute is not specified
class Class2 {}
```

类 Class1 和 Class2 都使用 Test 特性进行修饰，该特性是基于 DEBUG 是否定义的条件特性。由于该符号在 Class1 的上下文中已定义，而在 Class2 的上下文中未定义，因此类 Class1 上 Test 特性的规范被包含，而类 Class2 上 Test 特性的规范被省略。示例结束]

## 22.5.4 Obsolete 特性

Obsolete 特性用于标记不应再使用的类型和类型成员。

如果程序使用了以 Obsolete 特性修饰的类型或成员，编译器应发出警告或错误。具体而言，如果未提供 error 参数，或者提供了 error 参数且其值为 false，编译器应发出警告；如果指定了 error 参数且其值为 true，编译器应发出错误。

[示例：在以下代码中

```
[Obsolete("This class is obsolete; use class B instead")]
class A
{
    public void F() {}
}
class B
{
    public void F() {}
}
class Test
{
    static void Main() {
        A a = new A(); // Warning
        a.F();
    }
}
```

类 A 使用 Obsolete 特性进行修饰。在 Main 中每次使用 A 都会产生一条警告，其中包含指定的消息“This class is obsolete; use class B instead.”。示例结束]

## 22.5.5 调用方信息特性

### 22.5.5.1 概述

出于日志记录和报告等目的，函数成员有时需要获取有关调用代码的某些编译时信息。调用方信息特性提供了一种透明传递此类信息的方式。

当可选参数使用某个调用方信息特性进行注解时，在调用中省略相应的参数并不一定会导致使用默认参数值。相反，如果调用上下文的指定信息可用，则该信息将作为参数值传入。

[示例：

```
using System.Runtime.CompilerServices
...
```

如果调用跨越多行，所选行号由实现决定。

行号可能受 #line 指令（§7.5.8）的影响。

### 22.5.5.3 CallerFilePath 特性

当存在从 string 到参数类型的标准隐式转换（§11.2.2）时，System.Runtime.CompilerServices.CallerFilePathAttribute 可用于可选参数。

```
namespace System.Runtime.CompilerServices
{
    [AttributeUsageAttribute(AttributeTargets.Parameter, Inherited = false)]
    public sealed class CallerFilePathAttribute : Attribute
    {
        public CallerFilePathAttribute() {...}
    }
}
```

如果来自源代码某个位置的函数调用省略了带有 CallerFilePathAttribute 的可选参数，则使用表示该位置文件路径的字符串字面量作为调用参数，而不是使用默认参数值。

文件路径的格式由实现决定。

文件路径可能受 #line 指令（§7.5.8）的影响。

### 22.5.5.4 CallerMemberName 特性

当存在从 string 到参数类型的标准隐式转换（§11.2.2）时，System.Runtime.CompilerServices.CallerMemberNameAttribute 可用于可选参数。

```
namespace System.Runtime.CompilerServices
{
    [AttributeUsageAttribute(AttributeTargets.Parameter, Inherited = false)]
    public sealed class CallerMemberNameAttribute : Attribute
    {
        public CallerMemberNameAttribute() {...}
    }
}
```

如果函数调用发生于函数成员体内或应用于函数成员本身、其返回类型、参数或类型参数的属性中，并且该调用省略了带有 CallerMemberNameAttribute 的可选参数，则使用表示该成员名称的字符串字面量作为调用参数，而不是使用默认参数值。

对于发生在泛型方法中的调用，仅使用方法名称本身，不包含类型参数列表。

对于发生在显式接口成员实现中的调用，仅使用方法名称本身，不包含前面的接口限定。

对于发生在属性或事件访问器中的调用，使用的成员名称是属性或事件本身的名称。

对于发生在索引器访问器中的调用，使用的成员名称是索引器成员上的 IndexerNameAttribute（§）提供的名称（如果存在），否则使用默认名称 Item。

对于发生在字段或事件初始化器中的调用，使用的成员名称是被初始化的字段或事件的名称。

对于发生在实例构造函数、静态构造函数、终结器和运算符声明中的调用，使用的成员名称由实现决定。

## 22.6 用于互操作的特性

为了与其他语言进行互操作，索引器可以使用索引属性来实现。如果索引器上没有 IndexerName 特性，则默认使用名称 Item。IndexerName 特性使开发人员能够覆盖此默认设置并指定不同的名称。

```
namespace System.Runtime.CompilerServices
{
    [AttributeUsage(AttributeTargets.Property)]
    public class IndexerNameAttribute: Attribute
    {
        public IndexerNameAttribute(string indexerName) {...}
        public string Value { get {...} }
    }
}
```

## 23. 不安全代码

### 23.1 概述

不支持不安全代码的实现必须对关键字 unsafe 的任何使用进行诊断。

本条款的其余部分（包括其所有子条款）是有条件的规范性内容。

[注：如前几条款所定义，核心 C# 语言与 C 和 C++ 的一个显著区别是省略了指针作为数据类型。相反，C# 提供了引用和创建由垃圾回收器管理的对象的能力。这种设计加上其他功能，使 C# 成为一种比 C 和 C++ 安全得多的语言。在核心 C# 语言中，根本不可能出现未初始化的变量、“悬空”指针或对数组进行越界索引的表达式。因此，C 和 C++ 程序中常见的整类 bug 都被消除了。]

尽管 C 或 C++ 中几乎每个指针类型构造在 C# 中都有对应的引用类型，但仍然存在必须访问指针类型的情况。例如，与底层操作系统交互、访问内存映射设备或实现时间关键型算法，如果没有指针访问，可能无法实现或不切实际。为了满足这一需求，C# 提供了编写不安全代码的能力。

在不安全代码中，可以声明和操作指针，在指针与整型之间执行转换，获取变量的地址等。从某种意义上说，编写不安全代码就像在 C# 程序中编写 C 代码。

实际上，从开发者和用户的角度来看，不安全代码是一种“安全”的功能。不安全代码必须使用修饰符 unsafe 明确标记，这样一来，开发者就不可能意外地使用不安全功能，同时执行引擎也会确保不安全代码无法在不受信任的环境中执行。注释结束

### 23.2 不安全上下文

C# 的不安全功能仅在不安全上下文中可用。通过在类型或成员的声明中加入 unsafe 修饰符，或使用 unsafe 语句即可引入不安全上下文：

- 类、结构、接口或委托的声明可以包含 unsafe 修饰符，在这种情况下，该类型声明的整个文本范围（包括类、结构或接口的主体）都被视为不安全上下文。[注：如果类型声明是分部声明，则只有该部分是不安全上下文。注释结束]
- 字段、方法、属性、事件、索引器、运算符、实例构造函数、终结器或静态构造函数的声明可以包含 unsafe 修饰符，在这种情况下，该成员声明的整个文本范围被视为不安全上下文。
- unsafe 语句允许在块内使用不安全上下文。关联块的整个文本范围被视为不安全上下文。

相关的语法扩展如下所示。为简洁起见，省略号 (...) 用于表示前几条款中出现的产生式。

```
class-modifier:
    ...
    unsafe
```


struct-modifier:
  ...
  unsafe
interface-modifier:
  ...
  unsafe
delegate-modifier:
  ...
  unsafe
field-modifier:
  ...
  unsafe
method-modifier:
  ...
  unsafe
property-modifier:
  ...
  unsafe
event-modifier:
  ...
  unsafe
indexer-modifier:
  ...
  unsafe
operator-modifier:
  ...
  unsafe
constructor-modifier:
  ...
  unsafe
finalizer-declaration:
  attributes_opt extern_opt unsafe_opt ~ identifier ( ) finalizer-body
  attributes_opt unsafe_opt extern_opt ~ identifier ( ) finalizer-body
static-constructor-modifiers:
  extern_opt unsafe_opt static
  unsafe_opt extern_opt static
  extern_opt static unsafe_opt
  unsafe_opt static extern_opt
  static extern_opt unsafe_opt
  static unsafe_opt extern_opt
embedded-statement:
  ...
  unsafe-statement
unsafe-statement:
  unsafe block

[示例：下面的代码中

```csharp
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
```

在结构体声明中指定的 unsafe 修饰符会导致结构体声明的整个文本范围成为不安全上下文。因此，可以将 Left 和 Right 字段声明为指针类型。上面的示例也可以写成

```csharp
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

这里，字段声明中的 unsafe 修饰符会导致这些声明被视为不安全上下文。结束示例]

除建立不安全上下文（从而允许使用指针类型）之外，unsafe 修饰符对类型或成员没有任何影响。[示例：下面的代码中

```csharp
public class A
{
    public unsafe virtual void F() {
        char* p;
        ...
    }
}
public class B: A
{
    public override void F() {
        base.F();
    }
    ...
}
```

A 中 F 方法上的 unsafe 修饰符只是使 F 的文本范围成为不安全上下文，在此上下文中可以使用语言的不安全特性。在 B 中对 F 的重写中，无需重新指定 unsafe 修饰符——除非当然 B 中的 F 方法本身需要访问不安全特性。

当指针类型是方法签名的一部分时，情况略有不同

```csharp
public unsafe class A
{
    public virtual void F(char* p) {...}
}
public class B: A
{
    public unsafe override void F(char* p) {...}
}
```

这里，由于 F 的签名包含指针类型，它只能在不安全上下文中编写。但是，不安全上下文可以通过使整个类不安全（如 A 中的情况）或在方法声明中包含 unsafe 修饰符（如 B 中的情况）来引入。结束示例]

当 unsafe 修饰符用于部分类型声明（§15.2.7）时，只有该特定部分被视为不安全上下文。

## 23.3 指针类型

在不安全上下文中，类型（§9）可以是 pointer-type 以及 value-type、reference-type 或 type-parameter。在不安全上下文中，pointer-type 也可以是数组（§17）的元素类型。pointer-type 也可在不安全上下文之外用于 typeof 表达式（§12.7.12）（因为这种用法不是不安全的）。

type:
    ...
    pointer-type

non-array-type:
    ...
    pointer-type

pointer-type 是以 unmanaged-type 或关键字 void 编写，后跟 * 标记：

pointer-type:
    unmanaged-type *
    void *

unmanaged-type:
    type

在指针类型中 * 之前指定的类型称为该指针类型的引用类型。它表示指针类型的值指向的变量的类型。

pointer-type 只能在不安全上下文（§23.2）中用作 array-type。non-array-type 是本身不是 array-type 的任何类型。

在指针类型中 * 之前指定的类型称为该指针类型的引用类型。它表示指针类型的值指向的变量的类型。

与引用（引用类型的值）不同，指针不由垃圾回收器跟踪——垃圾回收器不知道指针及其指向的数据。因此，指针不允许指向引用或包含引用的结构体，并且指针的引用类型必须是 unmanaged-type。

unmanaged-type 是任何不是 reference-type、type-parameter 或 constructed type 的类型，并且不包含类型不是 unmanaged-type 的字段。换句话说，unmanaged-type 是以下之一：

- sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 或 bool。
- 任何 enum-type。
- 任何 pointer-type。
- 任何未构造且仅包含 unmanaged-type 字段的用户定义 struct-type。

混合指针和引用的直观规则是，引用的引用（对象）可以包含指针，但指针的引用不能包含引用。

[示例：下表给出了一些指针类型的示例：

| 示例 | 描述 |
|---|---|
| byte* | 指向 byte 的指针 |
| char* | 指向 char 的指针 |
| int** | 指向指向 int 的指针 |
| int*[] | 指向 int 的指针的单维数组 |
| void* | 指向未知类型的指针 |

结束示例]

对于给定的实现，所有指针类型都应具有相同的大小和表示形式。

[注意：与 C 和 C++ 不同，当在同一声明中声明多个指针时，在 C# 中 * 仅与底层类型一起编写，而不是作为每个指针名称的前缀 punctuator。例如：

```
int* pi, pj;  // NOT as int *pi, *pj;
```

结束注意]

类型为 T* 的指针的值表示类型为 T 的变量的地址。指针间接运算符 *（§23.6.2）可用于访问此变量。[示例：给定类型为 int* 的变量 P，表达式 *P 表示在 P 包含的地址处找到的 int 变量。结束示例]

与对象引用一样，指针可能为 null。对空指针应用间接运算符会导致实现定义的行为（§23.6.2）。值为 null 的指针由全零位表示。

void* 类型表示指向未知类型的指针。由于引用类型未知，不能对 void* 类型的指针应用间接运算符，也不能对这种指针执行任何算术运算。然而，void* 类型的指针可以强制转换为任何其他指针类型（反之亦然），并且可以与其它指针类型的值进行比较（§23.6.8）。

指针类型是类型的一个独立类别。与引用类型和值类型不同，指针类型不继承自 object，并且指针类型与 object 之间不存在转换。特别是，装箱和拆箱（§9.3.12）不适用于指针。然而，不同指针类型之间以及指针类型与整数类型之间的转换是允许的。这在 §23.5 中描述。

pointer-type 不能用作类型参数（§9.4），并且类型推断（§12.6.3）在会推断出类型参数为指针类型的泛型方法调用上失败。

pointer-type 不能用作动态绑定操作（§12.3.3）的子表达式的类型。

pointer-type 可用作 volatile 字段（§15.5.4）的类型。

[注意：尽管指针可以作为 ref 或 out 参数传递，但这样做可能导致未定义行为，因为指针可能被设置为指向在被调用方法返回时已不再存在的局部变量，或其曾经指向的 fixed 对象不再被固定。例如：

```
using System;
class Test
{
    static int value = 20;
    unsafe static void F(out int* pi1, ref int* pi2) {
        int i = 10;
        pi1 = &i;
        fixed (int* pj = &value) {
            //...
            pi2 = pj;
        }
    }
    static void Main() {
        int i = 10;
        unsafe {
            int* px1;
            int* px2 = &i;
            F(out px1, ref px2);
            Console.WriteLine("*px1 = {0}, *px2 = {1}", *px1, *px2); // undefined behavior
        }
    }
}
```

结束注意]




方法可以返回某种类型的值，而该类型可以是指针。[示例：给定一个指向连续 `int` 序列的指针、该序列的元素数量以及另一个 `int` 值，以下方法会在匹配成功时返回该序列中该值的地址；否则返回 null：

```
unsafe static int* Find(int* p, int size, int value) {
    for (int i = 0; i < size; ++i) {
        if (*p == value)
            return p;
        ++p;
    }
    return null;
}
```

示例结束]

在不安全上下文中，可以使用以下几种构造来操作指针：

- 一元 `*` 运算符可用于执行指针间接寻址（§23.6.2）。
- `->` 运算符可用于通过指针访问结构的成员（§23.6.3）。
- `[]` 运算符可用于对指针进行索引（§23.6.4）。
- 一元 `&` 运算符可用于获取变量的地址（§23.6.5）。
- `++` 和 `--` 运算符可用于递增和递减指针（§23.6.6）。
- 二元 `+` 和 `-` 运算符可用于执行指针算术运算（§23.6.7）。
- `==`、`!=`、`<`、`>`、`<=` 和 `>=` 运算符可用于比较指针（§23.6.8）。
- `stackalloc` 运算符可用于从调用堆栈分配内存（§23.9）。
- `fixed` 语句可用于临时固定变量，以便获取其地址（§23.7）。

## 23.4 固定变量和可移动变量

取址运算符（§23.6.5）和 `fixed` 语句（§23.7）将变量分为两类：固定变量和可移动变量。

固定变量位于不受垃圾回收器操作影响的存储位置中。（固定变量的示例包括局部变量、值参数以及通过对指针取消引用而创建的变量。）另一方面，可移动变量位于可能被垃圾回收器重新定位或释放的存储位置中。（可移动变量的示例包括对象中的字段和数组中的元素。）

`&` 运算符允许在不受限制的情况下获取固定变量的地址。但是，由于可移动变量可能会被垃圾回收器重新定位或释放，因此只能使用 `fixed` 语句（§23.7）获取可移动变量的地址，并且该地址仅在该 `fixed` 语句的持续时间内有效。

更准确地说，固定变量是以下各项之一：

- 由简单名称（§12.7.3）产生的变量，该简单名称引用局部变量、值参数或参数数组，除非该变量被匿名函数（§12.16.6.2）捕获。
- 由形如 `V.I` 的成员访问（§12.7.5）产生的变量，其中 `V` 是结构类型的固定变量。
- 由形如 `*P` 的指针间接寻址表达式（§23.6.2）、形如 `P->I` 的指针成员访问（§23.6.3）或形如 `P[E]` 的指针元素访问（§23.6.4）产生的变量。

## 23.5 指针转换

### 23.5.1 常规

在不安全上下文中，可用的隐式转换集合（§11.2）扩展为包括以下隐式指针转换：

- 从任何指针类型转换为 `void*` 类型。
- 从 null 字面量（§7.4.5.7）转换为任何指针类型。

此外，在不安全上下文中，可用的显式转换集合（§11.3）扩展为包括以下显式指针转换：

- 从任何指针类型转换为任何其他指针类型。
- 从 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 或 `ulong` 转换为任何指针类型。
- 从任何指针类型转换为 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 或 `ulong`。

最后，在不安全上下文中，标准隐式转换（§11.4.2）集合包括以下指针转换：

- 从任何指针类型转换为 `void*` 类型。
- 从 null 字面量转换为任何指针类型。

两种指针类型之间的转换永远不会改变实际的指针值。换句话说，从一种指针类型转换为另一种指针类型不会影响指针所指向的底层地址。

当一种指针类型转换为另一种指针类型时，如果所得指针未针对其指向的类型正确对齐，则在对该结果取消引用时，行为是未定义的。通常，“正确对齐”的概念具有传递性：如果指向类型 A 的指针针对指向类型 B 的指针正确对齐，而指向类型 B 的指针又针对指向类型 C 的指针正确对齐，那么指向类型 A 的指针也针对指向类型 C 的指针正确对齐。[示例：考虑以下情况，其中通过指向不同类型的指针访问具有某种类型的变量：

```
char c = 'A';
char* pc = &c;
void* pv = pc;
int* pi = (int*)pv;
int i = *pi;    // undefined
*pi = 123456;   // undefined
```

示例结束]

当指针类型转换为指向 `byte` 的指针时，所得指针指向该变量地址最低的字节。将所得指针连续递增，直到达到变量大小，即可得到指向该变量其余字节的指针。[示例：以下方法以十六进制值显示 `double` 中的八个字节：

```
using System;
class Test
{
    static void Main() {
        double d = 123.456e23;
        unsafe {
            byte* pb = (byte*)&d;
            for (int i = 0; i < sizeof(double); ++i)
                Console.Write("{0:X2} ", *pb++);
            Console.WriteLine();
        }
    }
}
```

当然，生成的输出取决于字节序。示例结束]

指针与整数之间的映射由实现定义。[注：但是，在具有线性地址空间的 32 位和 64 位 CPU 架构上，指针与整数类型之间的转换通常分别与 `uint` 或 `ulong` 值与这些整数类型之间的转换完全相同。注释结束]

### 23.5.2 指针数组

在不安全上下文中，可以使用数组创建表达式（§12.7.11.5）构造指针数组。适用于其他数组类型的转换中，只有部分转换允许用于指针数组：

- 从任何数组类型到 `System.Array` 及其所实现接口的隐式引用转换（§11.2.5）同样适用于指针数组。但是，尝试通过 `System.Array` 或其所实现的接口访问数组元素，可能会在运行时导致异常，因为指针类型无法转换为 `object`。
- 从一维数组类型 `S[]` 到 `System.Collections.Generic.IList<T>` 及其泛型基接口的隐式和显式引用转换（§11.2.5、§11.3.4）永远不适用于指针数组。
- 从 `System.Array` 及其所实现接口到任何数组类型的显式引用转换（§11.3.4）适用于指针数组。
- 从 `System.Collections.Generic.IList<S>` 及其基接口到一维数组类型 `T[]` 的显式引用转换（§11.3.4）永远不适用于指针数组，因为指针类型不能用作类型参数，并且不存在从指针类型到非指针类型的转换。

这些限制意味着，§10.4.4.17 中所述的针对数组的 `foreach` 语句展开方式不能应用于指针数组。相反，对于以下形式的 `foreach` 语句：

```
foreach (V v in x) embedded-statement
```

其中 `x` 的类型是形如 `T[,..,]` 的数组类型，`n` 是维数减 1，并且 `T` 或 `V` 是指针类型，该语句将使用如下嵌套 `for` 循环进行展开：

```
{
    T[,.., ] a = x;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
        for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
        ...
        for (int iN = a.GetLowerBound(n); iN <= a.GetUpperBound(n); iN++) {
            V v = (V)a[i0,i1,..,iN];
            embedded-statement
        }
}
```

变量 `a`、`i0`、`i1`、…… `iN` 对于 `x`、嵌入语句或程序的任何其他源代码均不可见或不可访问。变量 `v` 在嵌入语句中是只读的。如果不存在从 `T`（元素类型）到 `V` 的显式转换（§23.5），则会产生错误，并且不再执行后续步骤。如果 `x` 的值为 null，则会在运行时引发 `System.NullReferenceException`。

> [注：尽管不允许将指针类型作为类型参数，但指针数组可以用作类型参数。注释结束]

## 23.6 表达式中的指针

### 23.6.1 常规

在不安全上下文中，表达式可以产生指针类型的结果；但在不安全上下文之外，表达式具有指针类型将导致编译时错误。更准确地说，在不安全上下文之外，如果任何简单名称（§12.7.3）、成员访问（§12.7.5）、调用表达式（§12.7.6）或元素访问（§12.7.7）属于指针类型，则会发生编译时错误。




在不安全上下文中，*非数组创建基本表达式*（§12.7）和*一元表达式*（§12.8）产生式允许以下附加构造：

```text
primary-no-array-creation-expression:
    ...
    pointer-member-access
    pointer-element-access

unary-expression:
    ...
    pointer-indirection-expression
    addressof-expression
```

这些构造将在以下子条款中描述。

> > [注意：不安全运算符的优先级和结合性由文法隐含。结束注释]

### 23.6.2 指针间接寻址

*指针间接寻址表达式*由一个星号（`*`）后跟一个*一元表达式*组成。

```text
pointer-indirection-expression:
    * unary-expression
```

一元`*`运算符表示指针间接寻址，用于获取指针所指向的变量。对`*P`（其中P是指针类型`T*`的表达式）的求值结果是一个T类型的变量。将一元`*`运算符应用于`void*`类型的表达式或不是指针类型的表达式是编译时错误。

将一元`*`运算符应用于`null`指针的效果是实现定义的。特别地，不保证此操作会抛出`System.NullReferenceException`。

如果向指针赋予了无效值，则一元`*`运算符的行为未定义。

> > [注意：通过一元`*`运算符解引用指针的无效值包括：对于所指向类型而言地址未适当对齐（参见§23.5中的示例），以及变量生命周期结束后的地址。结束注释]

出于明确赋值分析的目的，通过计算`*P`形式的表达式所产生的变量被视为最初已赋值（§10.4.2）。

### 23.6.3 指针成员访问

*指针成员访问*由一个*基本表达式*、一个`"->"`标记、一个*标识符*以及一个可选的*类型参数列表*组成。

```text
pointer-member-access:
    primary-expression -> identifier type-argument-list_opt
```

在形如`P->I`的指针成员访问中，P必须是指针类型的表达式，并且I必须表示P所指向类型的可访问成员。

形如`P->I`的指针成员访问与`(*P).I`的求值完全一致。关于指针间接寻址运算符（`*`）的描述，请参阅§23.6.2。关于成员访问运算符（`.`）的描述，请参阅§12.7.5。

> > [示例：在以下代码中

```csharp
using System;
struct Point
{
    public int x;
    public int y;
    public override string ToString() {
        return "(" + x + "," + y + ")";
    }
}
class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

-> 运算符用于通过指针访问结构体的字段和调用其方法。由于操作P->I与(*P).I完全等价，Main方法同样可以写成：

```csharp
class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            (*p).x = 10;
            (*p).y = 20;
            Console.WriteLine((*p).ToString());
        }
    }
}
```

结束示例]

### 23.6.4 指针元素访问

指针元素访问由一个非数组创建基本表达式后跟一个用`[`和`]`括起来的表达式组成。

pointer-element-access:
    primary-no-array-creation-expression [ expression ]

在形如`P[E]`的指针元素访问中，P必须是指针类型（除`void*`外）的表达式，E必须是可隐式转换为`int`、`uint`、`long`或`ulong`的表达式。

形如`P[E]`的指针元素访问与`*(P + E)`的求值完全一致。关于指针间接寻址运算符（`*`）的描述，请参阅§23.6.2。关于指针加法运算符（`+`）的描述，请参阅§23.6.7。

[示例：在以下代码中

```csharp
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
        }
    }
}
```

指针元素访问用于在for循环中初始化字符缓冲区。由于操作P[E]与*(P + E)完全等价，该示例同样可以写成：

```csharp
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) *(p + i) = (char)i;
        }
    }
}
```

结束示例]

指针元素访问运算符不检查越界错误，访问越界元素时的行为未定义。[注意：这与C和C++相同。结束注释]

### 23.6.5 取地址运算符

取地址表达式由一个与号（&）后跟一个一元表达式组成。

addressof-expression:
& unary-expression

给定一个类型为T且被归类为固定变量（§23.4）的表达式E，构造`&E`计算由E给定的变量的地址。结果的类型为`T*`，并被归类为值。如果E未被归类为变量，如果E被归类为只读局部变量，或者如果E表示可移动变量，则会发生编译时错误。在最后一种情况下，可以使用fixed语句（§23.7）在获取其地址之前临时“固定”该变量。[注意：如§12.7.5所述，在定义readonly字段的结构或类的实例构造函数或静态构造函数之外，该字段被视为值，而不是变量。因此，不能获取其地址。类似地，也不能获取常量的地址。结束注释]

`&`运算符不要求其参数已被明确赋值，但在`&`操作之后，该运算符所应用的变量在执行路径中被视为已明确赋值。在这种情况下，确保变量实际确实被正确初始化是程序员的责任。

[示例：在以下代码中

```csharp
using System;
class Test
{
    static void Main() {
        int i;
        unsafe {
            int* p = &i;
            *p = 123;
        }
        Console.WriteLine(i);
    }
}
```

在用于初始化p的&i操作之后，i被视为已明确赋值。对*p的赋值实际上初始化了i，但该初始化的包含是程序员的责任，如果该赋值被移除，不会发生编译时错误。结束示例]

[注意：`&`运算符的明确赋值规则的存在是为了避免局部变量的冗余初始化。例如，许多外部API接受指向结构的指针，该结构由API填充。对这些API的调用通常传递局部结构变量的地址，如果没有此规则，则需要对该结构变量进行冗余初始化。结束注释]

[注意：当局部变量、值参数或参数数组被匿名函数（§12.7.16）捕获时，该局部变量、参数或参数数组不再被视为固定变量（§23.7），而是被视为可移动变量。因此，任何不安全代码获取已被匿名函数捕获的局部变量、值参数或参数数组的地址都是错误的。结束注释]

### 23.6.6 指针递增和递减

在不安全上下文中，`++`和`--`运算符（§12.7.10和§12.8.6）可应用于除`void*`之外的所有类型的指针变量。因此，对于每个指针类型`T*`，隐式定义了以下运算符：

```
T* operator ++(T* x);
T* operator --(T* x);
```

这些运算符分别产生与x+1和x-1相同的结果（§23.6.7）。换句话说，对于类型为`T*`的指针变量，`++`运算符将`sizeof(T)`加到变量包含的地址上，`--`运算符从变量包含的地址中减去`sizeof(T)`。

如果指针递增或递减操作溢出指针类型的域，结果是实现定义的，但不会产生异常。

### 23.6.7 指针算术

在不安全上下文中，`+`运算符（§12.9.5）和`–`运算符（§12.9.6）可应用于除`void*`之外的所有指针类型的值。因此，对于每个指针类型`T*`，隐式定义了以下运算符：

```
T* operator +(T* x, int y);
T* operator +(T* x, uint y);
T* operator +(T* x, long y);
T* operator +(T* x, ulong y);
T* operator +(int x, T* y);
T* operator +(uint x, T* y);
T* operator +(long x, T* y);
T* operator +(ulong x, T* y);
T* operator -(T* x, int y);
T* operator -(T* x, uint y);
T* operator -(T* x, long y);
T* operator -(T* x, ulong y);
long operator -(T* x, T* y);
```

给定一个指针类型`T*`的表达式P和一个类型为`int`、`uint`、`long`或`ulong`的表达式N，表达式`P + N`和`N + P`计算通过将`N * sizeof(T)`加到P给定的地址上而得到的`T*`类型的指针值。类似地，表达式`P – N`计算通过从P给定的地址中减去`N * sizeof(T)`而得到的`T*`类型的指针值。

给定指针类型`T*`的两个表达式P和Q，表达式`P – Q`计算P和Q给定的地址之间的差值，然后将该差值除以`sizeof(T)`。结果的类型总是`long`。实际上，`P – Q`的计算方式为`((long)(P) - (long)(Q)) / sizeof(T)`。

[示例：

```csharp
using System;
class Test
{
    static void Main() {
        unsafe {
            int* values = stackalloc int[20];
            int* p = &values[1];
            int* q = &values[15];
            Console.WriteLine("p - q = {0}", p - q);
            Console.WriteLine("q - p = {0}", q - p);
        }
    }
}
```

这将产生以下输出：



```
p - q = -14
q - p = 14
```

示例结束]

如果指针算术运算溢出指针类型的域，结果将以实现定义的方式截断，但不会产生异常。

## 23.6.8 指针比较

在非安全上下文中，==、!=、<、>、<= 和 >= 运算符（§12.11）可应用于所有指针类型的值。指针比较运算符包括：

```
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

由于存在从任意指针类型到 void* 类型的隐式转换，因此可以使用这些运算符比较任意指针类型的操作数。这些比较运算符将两个操作数给出的地址当作无符号整数进行比较。

## 23.6.9 sizeof 运算符

对于某些预定义类型（§12.7.13），sizeof 运算符产生一个常量 int 值。对于所有其他类型，sizeof 运算符的结果由实现定义，并被归类为值，而不是常量。

成员打包到结构体中的顺序未指定。

为了对齐，结构体的开头、结构体内部以及结构体末尾可能存在未命名的填充。用作填充的位的内容是不确定的。

当应用于具有结构体类型的操作数时，结果是该类型变量中的总字节数，包括任何填充。

## 23.7 fixed 语句

在非安全上下文中，embedded-statement（§13.1）产生式允许一种附加构造，即 fixed 语句，它用于“固定”可移动变量，使其地址在该语句执行期间保持不变。

```
embedded-statement:
  ...
  fixed-statement
fixed-statement:
  fixed ( pointer-type fixed-pointer-declarators ) embedded-statement
fixed-pointer-declarators:
  fixed-pointer-declarator
  fixed-pointer-declarators , fixed-pointer-declarator
fixed-pointer-declarator:
  identifier = fixed-pointer-initializer
fixed-pointer-initializer:
  & variable-reference
  expression
```

每个 fixed-pointer-declarator 声明一个具有给定 pointer-type 的局部变量，并用相应的 fixed-pointer-initializer 计算出的地址初始化该局部变量。在 fixed 语句中声明的局部变量，可在该变量声明右侧出现的任何 fixed-pointer-initializer 中访问，也可在该 fixed 语句的 embedded-statement 中访问。由 fixed 语句声明的局部变量被视为只读。如果嵌入语句尝试修改此局部变量（通过赋值或 ++ 和 -- 运算符），或将其作为 ref 或 out 参数传递，则发生编译时错误。

在 fixed-pointer-initializer 中使用捕获的局部变量（§12.16.6.2）、值参数或参数数组是错误的。fixed-pointer-initializer 可以是下列之一：

- 标记“&”后跟一个 variable-reference（§10.5），该引用指向非托管类型 T 的可移动变量（§23.4），前提是类型 T* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算给定变量的地址，并保证该变量在 fixed 语句执行期间保持在固定地址。
- 一个数组类型的表达式，其元素为非托管类型 T，前提是类型 T* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算数组中第一个元素的地址，并保证整个数组在 fixed 语句执行期间保持在固定地址。如果数组表达式为 null，或数组元素数为零，则 fixed 语句的行为由实现定义。
- 一个 string 类型的表达式，前提是类型 char* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算字符串中第一个字符的地址，并保证整个字符串在 fixed 语句执行期间保持在固定地址。如果字符串表达式为 null，则 fixed 语句的行为由实现定义。
- 一个 simple-name 或 member-access，它引用可移动变量的固定大小缓冲区成员，前提是该固定大小缓冲区成员的类型可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算指向固定大小缓冲区（§23.8.3）第一个元素的指针，并保证该固定大小缓冲区在 fixed 语句执行期间保持在固定地址。

对于由 fixed-pointer-initializer 计算的每个地址，fixed 语句确保该地址引用的变量在 fixed 语句执行期间不会被垃圾回收器重定位或处置。[示例：如果由 fixed-pointer-initializer 计算的地址引用对象的字段或数组实例的元素，则 fixed 语句保证包含该字段或元素的对象的实例在该语句的生存期内不会被重定位或处置。示例结束]

程序员有责任确保由 fixed 语句创建的指针在该语句执行完毕后不再存在。[示例：当由 fixed 语句创建的指针传递给外部 API 时，程序员有责任确保这些 API 不保留对这些指针的任何记忆。示例结束]

固定对象可能导致堆碎片化（因为它们无法移动）。因此，只有在绝对必要时才应固定对象，并且只应持续尽可能短的时间。

[示例：以下示例

```csharp
class Test
{
    static int x;
    int y;
    unsafe static void F(int* p) {
        *p = 1;
    }
}
```

```
static void Main() {
    Test t = new Test();
    int[] a = new int[10];
    unsafe {
        fixed (int* p = &x) F(p);
        fixed (int* p = &t.y) F(p);
        fixed (int* p = &a[0]) F(p);
        fixed (int* p = a) F(p);
    }
}
}
```

演示了 fixed 语句的若干用法。第一条语句固定并获取静态字段的地址，第二条语句固定并获取实例字段的地址，第三条语句固定并获取数组元素的地址。在每种情况下，使用常规 & 运算符都会出错，因为这些变量都被归类为可移动变量。

上例中的第三条和第四条 fixed 语句产生相同的结果。一般来说，对于数组实例 a，在 fixed 语句中指定 &a[0] 与直接指定 a 相同。下面是 fixed 语句的另一个示例，这次使用 string：

```
class Test
{
    static string name = "xx";
    unsafe static void F(char* p) {
        for (int i = 0; p[i] != '\0'; ++i)
            Console.WriteLine(p[i]);
    }
    static void Main() {
        unsafe {
            fixed (char* p = name) F(p);
            fixed (char* p = "xx") F(p);
        }
    }
}
```

示例结束]

在非安全上下文中，一维数组的数组元素按索引递增顺序存储，从索引 0 开始，到索引 Length − 1 结束。对于多维数组，数组元素的存储方式是：最右侧维度的索引先递增，然后向左下一个维度递增，依此类推。

在获取指向数组实例 a 的指针 p 的 fixed 语句中，从 p 到 p + a.Length − 1 的指针值表示数组中各元素的地址。同样，从 p[0] 到 p[a.Length − 1] 的变量表示实际的数组元素。鉴于数组的存储方式，我们可以将任意维度的数组视为线性数组。[示例：

```
using System;
class Test
{
    static void Main() {
        int[,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i) // treat as linear
                    p[i] = i;
            }
        }
    }
}
```




```
for (int i = 0; i < 2; ++i)
  for (int j = 0; j < 3; ++j) {
    for (int k = 0; k < 4; ++k) {
      Console.Write("[ {0},{1},{2}] = {3,2} ", i, j, k,
        a[i,j,k]);
      Console.WriteLine();
    }
  }
}
```

其输出为：

[0,0,0] = 1 [0,0,1] = 2 [0,0,2] = 3
[0,1,0] = 4 [0,1,1] = 5 [0,1,2] = 6 [0,1,3] = 7
[0,2,0] = 8 [0,2,1] = 9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23

示例结束]

[示例：在以下代码中

```
class Test
{
  unsafe static void Fill(int* p, int count, int value) {
    for (; count != 0; count--) *p++ = value;
  }
  static void Main() {
    int[] a = new int[100];
    unsafe {
      fixed (int* p = a) Fill(p, 100, -1);
    }
  }
}
```

使用 fixed 语句固定一个数组，以便将其地址传递给接受指针的方法。

示例结束]

通过固定字符串实例生成的 char* 值始终指向以 null 结尾的字符串。在获取指向字符串实例 s 的指针 p 的 fixed 语句中，从 p 到 p + s.Length - 1 的指针值表示字符串中字符的地址，而指针值 p + s.Length 始终指向 null 字符（值为 '\0' 的字符）。

通过固定指针修改托管类型的对象可能导致未定义行为。[注意：例如，由于字符串是不可变的，程序员有责任确保指向固定字符串的指针所引用的字符不被修改。注意结束]

[注意：当调用期望“C 风格”字符串的外部 API 时，字符串的自动 null 终止特别方便。但请注意，允许字符串实例包含 null 字符。如果存在此类 null 字符，则将该字符串视为以 null 结尾的 char* 时，它会显得被截断。注意结束]

## 23.8 固定大小缓冲区

### 23.8.1 概述

固定大小缓冲区用于将“C 风格”内联数组声明为结构体的成员，主要用于与非托管 API 对接。

### 23.8.2 固定大小缓冲区声明

固定大小缓冲区是一种成员，表示用于存储给定类型变量的固定长度缓冲区的存储。固定大小缓冲区声明引入一个或多个具有给定元素类型的固定大小缓冲区。固定大小缓冲区仅允许在结构体声明中使用，并且只能出现在 unsafe 上下文中（§23.2）。

```
struct-member-declaration:
  ...
  fixed-size-buffer-declaration
fixed-size-buffer-declaration:
  attributesopt fixed-size-buffer-modifiersopt fixed buffer-element-type
    fixed-size-buffer-declarators ;
fixed-size-buffer-modifiers:
  fixed-size-buffer-modifier
  fixed-size-buffer-modifier fixed-size-buffer-modifiers
fixed-size-buffer-modifier:
  new
  public
  protected
  internal
  private
  unsafe
buffer-element-type:
  type
fixed-size-buffer-declarators:
  fixed-size-buffer-declarator
  fixed-size-buffer-declarator , fixed-size-buffer-declarators
fixed-size-buffer-declarator:
  identifier [ constant-expression ]
```

固定大小缓冲区声明可以包含一组特性（§22）、一个 new 修饰符（§15.3.5）、四个访问修饰符（§15.3.6）的有效组合以及一个 unsafe 修饰符（§23.2）。特性和修饰符应用于该固定大小缓冲区声明所声明的所有成员。同一修饰符在固定大小缓冲区声明中多次出现属于错误。

固定大小缓冲区声明不允许包含 static 修饰符。

固定大小缓冲区声明的缓冲区元素类型指定该声明引入的缓冲区的元素类型。缓冲区元素类型应为以下预定义类型之一：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 bool。

缓冲区元素类型后跟一个固定大小缓冲区声明符列表，其中每个声明符都引入一个新成员。固定大小缓冲区声明符由一个为该成员命名的标识符，后跟一个括在 [ 和 ] 标记中的常量表达式组成。该常量表达式表示由该固定大小缓冲区声明符引入的成员中的元素数量。该常量表达式的类型应可隐式转换为 int 类型，且其值应为非零正整数。

固定大小缓冲区的元素应在内存中按顺序排列。

声明多个固定大小缓冲区的固定大小缓冲区声明，等价于多个具有相同特性和元素类型的单个固定大小缓冲区声明。[示例：

```
unsafe struct A
{
    public fixed int x[5], y[10], z[100];
}
```

等价于

```csharp
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```

*示例结束]*

### 23.8.3 表达式中的固定大小缓冲区

固定大小缓冲区成员的成员查找（§12.5）与字段的成员查找完全相同。

固定大小缓冲区可以在表达式中使用*简单名称*（§12.6.3）或*成员访问*（§12.6.5）来引用。

当固定大小缓冲区成员作为简单名称引用时，其效果与形式为 this.I 的成员访问相同，其中 I 是固定大小缓冲区成员。

在形式为 E.I 的成员访问中，如果 E 是结构体类型，并且在该结构体类型中对 I 的成员查找标识出一个固定大小成员，则按如下方式计算并分类 E.I：

- 如果表达式 E.I 不出现在 unsafe 上下文中，则发生编译时错误。
- 如果 E 被归类为值，则发生编译时错误。
- 否则，如果 E 是可移动变量（§23.4）且表达式 E.I 不是固定指针初始值设定项（§23.7），则发生编译时错误。
- 否则，E 引用一个固定变量，并且表达式的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针。结果的类型为 S*，其中 S 是 I 的元素类型，并被归类为值。

固定大小缓冲区的后续元素可以通过从第一个元素开始的指针操作来访问。与数组访问不同，访问固定大小缓冲区的元素是不安全操作，并且不进行范围检查。

*[示例：以下代码声明并使用一个带有固定大小缓冲区成员的结构体。*

```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

*示例结束]*

### 23.8.4 明确赋值检查

固定大小缓冲区不受明确赋值检查（§10.4）的约束，并且在结构类型变量的明确赋值检查中会忽略固定大小缓冲区成员。

当固定大小缓冲区成员的最外层包含结构变量是静态变量、类实例的实例变量或数组元素时，固定大小缓冲区的元素会自动初始化为其默认值（§10.3）。在所有其他情况下，固定大小缓冲区的初始内容未定义。

## 23.9 堆栈分配

在 unsafe 上下文中，局部变量声明（§13.6.2）可以包含堆栈分配初始值设定项，它从调用堆栈分配内存。

```
local-variable-initializer:
  stackalloc-initializer
stackalloc-initializer:
  stackalloc unmanaged-type [ expression ]
```

unmanaged-type 指示将存储在新分配位置中的项的类型，expression 指示这些项的数量。两者共同指定所需的分配大小。由于堆栈分配的大小不能为负，因此将项数指定为计算结果为负值的常量表达式属于编译时错误。

形式为 stackalloc T[E] 的堆栈分配初始值设定项要求 T 是非托管类型（§23.3），且 E 是可隐式转换为 int 类型的表达式。该构造从调用堆栈分配 E * sizeof(T) 个字节，并返回一个类型为 T* 的指针，指向新分配的块。如果 E 为负值，则行为未定义。如果 E 为零，则不进行分配，返回的指针由实现定义。如果没有足够的内存可用于分配给定大小的块，则引发 System.StackOverflowException。

新分配内存的内容未定义。

catch 或 finally 块（§13.11）中不允许使用堆栈分配初始值设定项。

[注意：无法显式释放使用 stackalloc 分配的内存。注意结束] 在函数成员执行期间创建的所有堆栈分配内存块都会在该函数成员返回时自动丢弃。[注意：这对应于 alloca 函数，这是 C 和 C++ 实现中常见的扩展。注意结束]

[示例：在以下代码中

```
using System;
class Test
{
    static string IntToString(int value) {
        int n = value >= 0 ? value : -value;
        unsafe {
            char* buffer = stackalloc char[16];
            char* p = buffer + 16;
            do {
                *--p = (char)(n % 10 + '0');
                n /= 10;
            } while (n != 0);
            if (value < 0) *--p = '-';
            return new string(p, 0, (int)(buffer + 16 - p));
        }
    }
    static void Main() {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```



在 `IntToString` 方法中使用 `stackalloc` 初始值设定项在栈上分配一个包含 16 个字符的缓冲区。该方法返回时，此缓冲区将自动丢弃。 [end example]

除了 `stackalloc` 运算符外，C# 不提供用于管理非垃圾回收内存的预定义构造。此类服务通常由支持类库提供，或直接从底层操作系统导入。

**条件性规范性文本结束。**

## 附录 A. 语法

本条款为资料性内容。

### A.1 概述

本附录包含主文档中出现的词法语法和句法语法摘要，以及不安全代码的语法扩展摘要。此处的语法产生式按照它们在主文档中出现的相同顺序给出。

### A.2 词法语法

```
input::
    input-section_opt
input-section::
    input-section-part
    input-section input-section-part
input-section-part::
    input-elements_opt new-line
    pp-directive
input-elements::
    input-element
    input-elements input-element
input-element::
    whitespace
    comment
    token
```

**行终止符**

```
new-line::
    Carriage return character (U+000D)
    Line feed character (U+000A)
    Carriage return character (U+000D) followed by line feed character (U+000A)
    Next line character (U+0085)
    Line separator character (U+2028)
    Paragraph separator character (U+2029)
```

**空白**

```
whitespace::
    whitespace-character
    whitespace whitespace-character
whitespace-character::
    Any character with Unicode class Zs
    Horizontal tab character (U+0009)
    Vertical tab character (U+000B)
    Form feed character (U+000C)
```

### A.2.1 注释

```
comment::
    single-line-comment
    delimited-comment

single-line-comment::
    // input-characters_opt

input-characters::
    input-character
    input-characters input-character

input-character::
    Any Unicode character except a new-line-character

new-line-character::
    Carriage return character (U+000D)
    Line feed character (U+000A)
    Next line character (U+0085)
    Line separator character (U+2028)
    Paragraph separator character (U+2029)

delimited-comment::
    /* delimited-comment-text_opt asterisks */

delimited-comment-text::
    delimited-comment-section
    delimited-comment-text delimited-comment-section

delimited-comment-section::
    /
    asterisks_opt not-slash-or-asterisk

asterisks::
    *
    asterisks *

not-slash-or-asterisk::
    Any Unicode character except / or *
```

### A.2.2 标记

```
token::
    identifier
    keyword
    integer-literal
    real-literal
    character-literal
    string-literal
    operator-or-punctuator
```

**Unicode 字符转义序列**

```
unicode-escape-sequence::
    \u hex-digit hex-digit hex-digit hex-digit
    \U hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit
```

**标识符**

```
identifier::
    available-identifier
    @ identifier-or-keyword

available-identifier::
    An identifier-or-keyword that is not a keyword

identifier-or-keyword::
    identifier-start-character identifier-part-characters_opt

identifier-start-character::
    letter-character
    underscore-character

underscore-character::
    _ (the underscore character U+005F)
    A unicode-escape-sequence representing the character U+005F

identifier-part-characters::
    identifier-part-character
    identifier-part-characters identifier-part-character

identifier-part-character::
    letter-character
    decimal-digit-character
    connecting-character
    combining-character
    formatting-character

letter-character::
    A Unicode character of classes Lu, Ll, Lt, Lm, Lo, or Nl
    A unicode-escape-sequence representing a character of classes Lu, Ll, Lt, Lm, Lo, or Nl

combining-character::
    A Unicode character of classes Mn or Mc
    A unicode-escape-sequence representing a character of classes Mn or Mc

decimal-digit-character::
    A Unicode character of the class Nd
    A unicode-escape-sequence representing a character of the class Nd

connecting-character::
    A Unicode character of the class Pc
    A unicode-escape-sequence representing a character of the class Pc

formatting-character::
    A Unicode character of the class Cf
    A unicode-escape-sequence representing a character of the class Cf
```

### A.2.3 关键字

```
keyword:: one of
    abstract as base bool break
    byte case catch char checked
    class const continue decimal default
    delegate do double else enum
    event explicit extern false finally
    fixed float for foreach goto
    if implicit in int interface
    internal is lock long namespace
    new null object operator out
    override params private protected public
    readonly ref return sbyte sealed
    short sizeof stackalloc static string
    struct switch this throw true
    try typeof uint ulong unchecked
    unsafe ushort using virtual void
    volatile while
```

**字面量**

```
literal::
    boolean-literal
    integer-literal
    real-literal
    character-literal
    string-literal
    null-literal

boolean-literal::
    true
    false

integer-literal::
    decimal-integer-literal
    hexadecimal-integer-literal

decimal-integer-literal::
    decimal-digits integer-type-suffix_opt

decimal-digits::
    decimal-digit
    decimal-digits decimal-digit

decimal-digit:: one of
    0 1 2 3 4 5 6 7 8 9

integer-type-suffix:: one of
    U u L l UL Ul uL ul LU Lu lU lu

hexadecimal-integer-literal::
    0x hex-digits integer-type-suffix_opt
    0X hex-digits integer-type-suffix_opt

hex-digits::
    hex-digit
    hex-digits hex-digit

hex-digit:: one of
    0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f

real-literal::
    decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
    . decimal-digits exponent-part_opt real-type-suffix_opt
    decimal-digits exponent-part real-type-suffix_opt
    decimal-digits real-type-suffix

exponent-part::
    e sign_opt decimal-digits
    E sign_opt decimal-digits

sign:: one of
    + -

real-type-suffix:: one of
    F f D d M m

character-literal::
    ' character '

character::
    single-character
    simple-escape-sequence
    hexadecimal-escape-sequence
    unicode-escape-sequence

single-character::
    Any character except ' (U+0027), \ (U+005C), and new-line-character

simple-escape-sequence:: one of
    \' \" \\ \0 \a \b \f \n \r \t \v

hexadecimal-escape-sequence::
    \x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt

string-literal::
    regular-string-literal
    verbatim-string-literal

regular-string-literal::
    " regular-string-literal-characters_opt "

regular-string-literal-characters::
    regular-string-literal-character
    regular-string-literal-characters regular-string-literal-character

regular-string-literal-character::
    single-regular-string-literal-character
    simple-escape-sequence
    hexadecimal-escape-sequence
    unicode-escape-sequence

single-regular-string-literal-character::
    Any character except " (U+0022), \ (U+005C), and new-line-character

verbatim-string-literal::
    @" verbatim-string-literal-characters_opt "

verbatim-string-literal-characters::
    verbatim-string-literal-character
    verbatim-string-literal-characters verbatim-string-literal-character

verbatim-string-literal-character::
    single-verbatim-string-literal-character
    quote-escape-sequence

single-verbatim-string-literal-character::
    Any character except "

quote-escape-sequence::
    """

null-literal::
    null
```

### A.2.4 运算符和标点符号

```
operator-or-punctuator:: one of
    { } [ ] ( ) . , : ;
    + - * / % & | ^ ! ~
    = < > ? ?? :: ++ -- && ||
    => == != <= >= += -= *= /= %=
    &= |= ^= << <<=

right-shift::
    > >

right-shift-assignment::
    > >=
```

### A.2.5 预处理指令

```
pp-directive::
    pp-declaration
    pp-conditional
    pp-line
    pp-diagnostic
    pp-region
    pp-pragma

conditional-symbol::
    Any identifier-or-keyword except true or false

pp-declaration::
    whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
    whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line

pp-new-line::
    whitespace_opt single-line-comment_opt new-line

pp-conditional::
    pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif

pp-if-section::
    whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line
    conditional-section_opt

pp-elif-sections::
    pp-elif-section
    pp-elif-sections pp-elif-section

pp-elif-section::
    whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line
    conditional-section_opt

pp-else-section::
    whitespace_opt # whitespace_opt else pp-new-line conditional-section_opt

pp-endif::
    whitespace_opt # whitespace_opt endif pp-new-line

conditional-section::
    input-section
    skipped-section

skipped-section::
    skipped-section-part
    skipped-section skipped-section-part

skipped-section-part::
    skipped-characters_opt new-line
    pp-directive

skipped-characters::
    whitespace_opt not-number-sign input-characters_opt

not-number-sign::
    Any input-character except #

pp-line::
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line

line-indicator::
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden

file-name::
    " file-name-characters "

file-name-characters::
    file-name-character
    file-name-characters file-name-character

file-name-character::
    Any input-character except " (U+0022) and new-line-character
```




```
pp-diagnostic::
    whitespace_opt # whitespace_opt error pp-message
    whitespace_opt # whitespace_opt warning pp-message

pp-message::
    new-line
    whitespace input-characters_opt new-line

pp-region::
    pp-start-region conditional-section_opt pp-end-region

pp-start-region::
    whitespace_opt # whitespace_opt region pp-message

pp-end-region::
    whitespace_opt # whitespace_opt endregion pp-message

pp-pragma::
    whitespace_opt # whitespace_opt pragma pp-pragma-text

pp-pragma-text::
    new-line
    whitespace input-characters_opt new-line
```

## A.3 句法文法

### A.3.1 基本概念

```
namespace-name:
    namespace-or-type-name

type-name:
    namespace-or-type-name

namespace-or-type-name:
    identifier type-argument-list_opt
    namespace-or-type-name . identifier type-argument-list_opt
    qualified-alias-member
```

### A.3.2 类型

```
type:
    reference-type
    value-type
    type-parameter

value-type:
    struct-type
    enum-type

struct-type:
    type-name
    simple-type
    nullable-value-type

simple-type:
    numeric-type
    bool
```

numeric-type:
    integral-type
    floating-point-type
    decimal

integral-type:
    sbyte
    byte
    short
    ushort
    int
    uint
    long
    ulong
    char

nullable-type:
    non-nullable-value-type ?

non-nullable-value-type:
    type

floating-point-type:
    float
    double

enum-type:
    type-name

type-argument-list:
    < type-arguments >

type-arguments:
    type-argument
    type-arguments , type-argument

type-argument:
    type

type-parameter:
    identifier

### A.3.3 变量

variable-reference:
    expression

### A.3.4 表达式

argument-list:
    argument
    argument-list , argument

argument:
    argument-name_opt argument-value

argument-name:
    identifier :

argument-value:
    expression
    ref variable-reference
    out variable-reference

```
primary-expression:
  primary-no-array-creation-expression
  array-creation-expression

primary-no-array-creation-expression:
  literal
  simple-name
  parenthesized-expression
  member-access
  invocation-expression
  element-access
  this-access
  base-access
  post-increment-expression
  post-decrement-expression
  object-creation-expression
  delegate-creation-expression
  anonymous-object-creation-expression
  typeof-expression
  sizeof-expression
  checked-expression
  unchecked-expression
  default-value-expression
  anonymous-method-expression

simple-name:
  identifier type-argument-list_opt

parenthesized-expression:
  ( expression )

member-access:
  primary-expression . identifier type-argument-list_opt
  predefined-type . identifier type-argument-list_opt
  qualified-alias-member . identifier type-argument-list_opt

predefined-type: one of
  bool byte char decimal double float int long
  object sbyte short string uint ulong ushort

invocation-expression:
  primary-expression ( argument-list_opt )

element-access:
  primary-no-array-creation-expression [ argument-list ]

expression-list:
  expression
  expression-list , expression

this-access:
  this

base-access:
  base . identifier type-argument-list_opt
  base [ argument-list ]

post-increment-expression:
  primary-expression ++

post-decrement-expression:
  primary-expression --
```

object-creation-expression:
  new type ( argument-list_opt ) object-or-collection-initializer_opt
  new type object-or-collection-initializer

object-or-collection-initializer:
  object-initializer
  collection-initializer

object-initializer:
  { member-initializer-list_opt }
  { member-initializer-list , }

member-initializer-list:
  member-initializer
  member-initializer-list , member-initializer

member-initializer:
  identifier = initializer-value

initializer-value:
  expression
  object-or-collection-initializer

collection-initializer:
  { element-initializer-list }
  { element-initializer-list , }

element-initializer-list:
  element-initializer
  element-initializer-list , element-initializer

element-initializer:
  non-assignment-expression
  { expression-list }

array-creation-expression:
  new non-array-type [ expression-list ] rank-specifiers_opt array-initializer_opt
  new array-type array-initializer
  new rank-specifier array-initializer

delegate-creation-expression:
  new delegate-type ( expression )

anonymous-object-creation-expression:
  new anonymous-object-initializer

anonymous-object-initializer:
  { member-declarator-list_opt }
  { member-declarator-list , }

member-declarator-list:
  member-declarator
  member-declarator-list , member-declarator

member-declarator:
  simple-name
  member-access
  base-access
  identifier = expression

```
typeof-expression:
    typeof ( type )
    typeof ( unbound-type-name )
    typeof ( void )

unbound-type-name:
    identifier generic-dimension-specifier_opt
    identifier :: identifier generic-dimension-specifier_opt
    unbound-type-name . identifier generic-dimension-specifier_opt

generic-dimension-specifier:
    < commas_opt >

commas:
    ,
    commas ,

checked-expression:
    checked ( expression )

unchecked-expression:
    unchecked ( expression )

default-value-expression:
    default ( type )

unary-expression:
    primary-expression
    + unary-expression
    - unary-expression
    ! unary-expression
    ~ unary-expression
    pre-increment-expression
    pre-decrement-expression
    cast-expression
    await-expression

pre-increment-expression:
    ++ unary-expression

pre-decrement-expression:
    -- unary-expression

cast-expression:
    ( type ) unary-expression

await-expression:
    await unary-expression

multiplicative-expression:
    unary-expression
    multiplicative-expression * unary-expression
    multiplicative-expression / unary-expression
    multiplicative-expression % unary-expression

additive-expression:
    multiplicative-expression
    additive-expression + multiplicative-expression
    additive-expression - multiplicative-expression
```

```
shift-expression:
  additive-expression
  shift-expression << additive-expression
  shift-expression right-shift additive-expression

relational-expression:
  shift-expression
  relational-expression < shift-expression
  relational-expression > shift-expression
  relational-expression <= shift-expression
  relational-expression >= shift-expression
  relational-expression is type
  relational-expression as type

equality-expression:
  relational-expression
  equality-expression == relational-expression
  equality-expression != relational-expression

and-expression:
  equality-expression
  and-expression & equality-expression

exclusive-or-expression:
  and-expression
  exclusive-or-expression ^ and-expression

inclusive-or-expression:
  exclusive-or-expression
  inclusive-or-expression | exclusive-or-expression

conditional-and-expression:
  inclusive-or-expression
  conditional-and-expression && inclusive-or-expression

conditional-or-expression:
  conditional-and-expression
  conditional-or-expression || conditional-and-expression

null-coalescing-expression:
  conditional-or-expression
  conditional-or-expression ?? null-coalescing-expression

conditional-expression:
  null-coalescing-expression
  null-coalescing-expression ? expression : expression

lambda-expression:
  async_opt anonymous-function-signature => anonymous-function-body

anonymous-method-expression:
  async_opt delegate explicit-anonymous-function-signature_opt block

anonymous-function-signature:
  explicit-anonymous-function-signature
  implicit-anonymous-function-signature

explicit-anonymous-function-signature:
  ( explicit-anonymous-function-parameter-list_opt )

explicit-anonymous-function-parameter-list:
  explicit-anonymous-function-parameter
  explicit-anonymous-function-parameter-list , explicit-anonymous-function-parameter
```

```
explicit-anonymous-function-parameter:
    anonymous-function-parameter-modifier_opt type identifier
anonymous-function-parameter-modifier:
    ref
    out
implicit-anonymous-function-signature:
    ( implicit-anonymous-function-parameter-list_opt )
    implicit-anonymous-function-parameter
implicit-anonymous-function-parameter-list:
    implicit-anonymous-function-parameter
    implicit-anonymous-function-parameter-list , implicit-anonymous-function-parameter
implicit-anonymous-function-parameter:
    identifier
anonymous-function-body:
    expression
    block
query-expression:
    from-clause query-body
from-clause:
    from type_opt identifier in expression
query-body:
    query-body-clauses_opt select-or-group-clause query-continuation_opt
query-body-clauses:
    query-body-clause
    query-body-clauses query-body-clause
query-body-clause:
    from-clause
    let-clause
    where-clause
    join-clause
    join-into-clause
    orderby-clause
let-clause:
    let identifier = expression
where-clause:
    where boolean-expression
join-clause:
    join type_opt identifier in expression on expression equals expression
join-into-clause:
    join type_opt identifier in expression on expression equals expression into
    identifier
orderby-clause:
    orderby orderings
orderings:
    ordering
    orderings , ordering
```


排序:
    表达式  排序方向_opt

排序方向:
    升序
    降序

选择或分组子句:
    选择子句
    分组子句

选择子句:
    选择  表达式

分组子句:
    分组  表达式  按  表达式

查询延续:
    进入  标识符  查询体

赋值:
    一元表达式  赋值运算符  表达式

赋值运算符:
    =
    +=
    -=
    *=
    /=
    %=
    &=
    |=
    ^=
    <<=
    右移赋值

表达式:
    非赋值表达式
    赋值

非赋值表达式:
    条件表达式
    lambda表达式
    查询表达式

常量表达式:
    表达式

布尔表达式:
    表达式

## A.3.5 语句

语句:
    标记语句
    声明语句
    嵌入语句

嵌入语句:
  块
  空语句
  表达式语句
  选择语句
  迭代语句
  跳转语句
  try语句
  checked语句
  unchecked语句
  lock语句
  using语句
  yield语句

块:
  { 语句列表_opt }

语句列表:
  语句
  语句列表 语句

空语句:
  ;

标记语句:
  标识符 : 语句

声明语句:
  局部变量声明 ;
  局部常量声明 ;

局部变量声明:
  局部变量类型 局部变量声明符

局部变量类型:
  类型
  var

局部变量声明符:
  局部变量声明符
  局部变量声明符 , 局部变量声明符

局部变量声明符:
  标识符
  标识符 = 局部变量初始化器

局部变量初始化器:
  表达式
  数组初始化器

局部常量声明:
  const 类型 常量声明符

常量声明符:
  常量声明符
  常量声明符 , 常量声明符

常量声明符:
  标识符 = 常量表达式

表达式语句:
  语句表达式 ;

语句表达式:
invocation-expression
object-creation-expression
assignment
post-increment-expression
post-decrement-expression
pre-increment-expression
pre-decrement-expression
await-expression

选择语句:
if语句
switch语句

if语句:
if ( 布尔表达式 ) 嵌入语句
if ( 布尔表达式 ) 嵌入语句 else 嵌入语句

switch语句:
switch ( 表达式 ) switch块

switch块:
{ switch节_opt }

switch节:
switch节
switch节 switch节

switch节:
switch标签 语句列表

switch标签:
switch标签
switch标签 switch标签

switch标签:
case 常量表达式 :
default :

迭代语句:
while语句
do语句
for语句
foreach语句

while语句:
while ( 布尔表达式 ) 嵌入语句

do语句:
do 嵌入语句 while ( 布尔表达式 ) ;

for语句:
for ( for初始化器_opt ; for条件_opt ; for迭代器_opt ) 嵌入语句

for初始化器:
局部变量声明
语句表达式列表

for条件:
布尔表达式

for迭代器:
语句表达式列表

语句表达式列表:
    语句表达式
    语句表达式列表 , 语句表达式
foreach语句:
    foreach ( 局部变量类型 标识符 in 表达式 ) 嵌入语句
跳转语句:
    break语句
    continue语句
    goto语句
    return语句
    throw语句
break语句:
    break ;
continue语句:
    continue ;
goto语句:
    goto 标识符 ;
    goto case 常量表达式 ;
    goto default ;
return语句:
    return 表达式_opt ;
throw语句:
    throw 表达式_opt ;
try语句:
    try 块 catch子句
    try 块 catch子句_opt finally子句
catch子句:
    特定catch子句
    特定catch子句_opt 通用catch子句
特定catch子句:
    特定catch子句
    特定catch子句 特定catch子句
特定catch子句:
    catch ( 类型 标识符_opt ) 块
通用catch子句:
    catch 块
finally子句:
    finally 块
checked语句:
    checked 块
unchecked语句:
    unchecked 块
lock语句:
    lock ( 表达式 ) 嵌入语句
using语句:
    using ( 资源获取 ) 嵌入语句

资源获取:
  局部变量声明
  表达式
yield语句:
  yield return 表达式 ;
  yield break ;

## A.3.6 命名空间

编译单元:
  extern别名指令_opt using指令_opt 全局属性_opt
  命名空间成员声明_opt

命名空间声明:
  namespace 限定标识符 命名空间体 ;_opt

限定标识符:
  标识符
  限定标识符 . 标识符

命名空间体:
  { extern别名指令_opt using指令_opt 命名空间成员声明_opt }

extern别名指令:
  extern别名指令
  extern别名指令 extern别名指令

extern别名指令:
  extern alias 标识符 ;

using指令:
  using指令
  using指令 using指令

using指令:
  using别名指令
  using命名空间指令

using别名指令:
  using 标识符 = 命名空间或类型名 ;

using命名空间指令:
  using 命名空间名 ;

命名空间成员声明:
  命名空间成员声明
  命名空间成员声明 命名空间成员声明

命名空间成员声明:
  命名空间声明
  类型声明

类型声明:
  类声明
  结构声明
  接口声明
  枚举声明
  委托声明

限定别名成员:
  标识符 :: 标识符 类型参数列表_opt

## A.3.7 类

类声明:
    属性_opt 类修饰符_opt partial_opt class 标识符 类型参数列表_opt
    类基_opt 类型参数约束子句_opt 类体 ;_opt

类修饰符:
    类修饰符
    类修饰符 类修饰符

类修饰符:
    new
    public
    protected
    internal
    private
    abstract
    sealed
    static

类型参数列表:
    < 类型参数 >

类型参数:
    属性_opt 类型参数
    类型参数 , 属性_opt 类型参数

类基:
    : 类类型
    : 接口类型列表
    : 类类型 , 接口类型列表

接口类型列表:
    接口类型
    接口类型列表 , 接口类型

类型参数约束子句:
    类型参数约束子句
    类型参数约束子句 类型参数约束子句

类型参数约束子句:
    where 类型参数 : 类型参数约束

类型参数约束:
    主要约束
    次要约束
    构造函数约束
    主要约束 , 次要约束
    主要约束 , 构造函数约束
    次要约束 , 构造函数约束
    主要约束 , 次要约束 , 构造函数约束

主要约束:
    类类型
    class
    struct

次要约束:
    接口类型
    类型参数
    次要约束 , 接口类型
    次要约束 , 类型参数

构造函数约束:
    new ( )
类体:
    { 类成员声明_opt }
类成员声明:
    类成员声明
    类成员声明 类成员声明
类成员声明:
    常量声明
    字段声明
    方法声明
    属性声明
    事件声明
    索引器声明
    运算符声明
    构造函数声明
    析构函数声明
    静态构造函数声明
    类型声明
常量声明:
    属性_opt 常量修饰符_opt const 类型 常量声明符 ;
常量修饰符:
    常量修饰符
    常量修饰符 常量修饰符
常量修饰符:
    new
    public
    protected
    internal
    private
常量声明符:
    常量声明符
    常量声明符 , 常量声明符
常量声明符:
    标识符 = 常量表达式
字段声明:
    属性_opt 字段修饰符_opt 类型 变量声明符 ;
字段修饰符:
    字段修饰符
    字段修饰符 字段修饰符
字段修饰符:
    new
    public
    protected
    internal
    private
    static
    readonly
    volatile

variable-declarators:
    variable-declarator
    variable-declarators , variable-declarator

variable-declarator:
    identifier
    identifier = variable-initializer

variable-initializer:
    expression
    array-initializer
method-declaration:
    method-header method-body

method-header:
    attributes_opt method-modifiers_opt partial_opt return-type member-name
    type-parameter-list_opt
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt

method-modifiers:
    method-modifier
    method-modifiers method-modifier

method-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern
    async

return-type:
    type
    void

method-body:
    block
    ;

formal-parameter-list:
    fixed-parameters
    fixed-parameters , parameter-array
    parameter-array

fixed-parameters:
    fixed-parameter
    fixed-parameters , fixed-parameter

fixed-parameter:
    attributes_opt parameter-modifier_opt type identifier default-argument_opt

default-argument:
    = expression

parameter-modifier:
    parameter-mode-modifier
    this
parameter-mode-modifier:
    ref
    out
parameter-array:
    attributes_opt params array-type identifier
property-declaration:
    attributes_opt property-modifiers_opt type member-name { accessor-declarations }
property-modifiers:
    property-modifier
    property-modifiers property-modifier
property-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern
accessor-declarations:
    get-accessor-declaration  set-accessor-declaration_opt
    set-accessor-declaration  get-accessor-declaration_opt
get-accessor-declaration:
    attributes_opt accessor-modifier_opt get accessor-body
set-accessor-declaration:
    attributes_opt accessor-modifier_opt set accessor-body
accessor-modifier:
    protected
    internal
    private
    protected internal
    internal protected
accessor-body:
    block
    ;
event-declaration:
    attributes_opt event-modifiers_opt event type variable-declarators ;
    attributes_opt event-modifiers_opt event type member-name
        { event-accessor-declarations }
event-modifiers:
    event-modifier
    event-modifiers event-modifier

event-modifier:
    new
    public
    protected
    internal
    private
    static
    virtual
    sealed
    override
    abstract
    extern

event-accessor-declarations:
    add-accessor-declaration remove-accessor-declaration
    remove-accessor-declaration add-accessor-declaration

add-accessor-declaration:
    attributes_opt add block

remove-accessor-declaration:
    attributes_opt remove block

indexer-declaration:
    attributes_opt indexer-modifiers_opt indexer-declarator { accessor-declarations }

indexer-modifiers:
    indexer-modifier
    indexer-modifiers indexer-modifier

indexer-modifier:
    new
    public
    protected
    internal
    private
    virtual
    sealed
    override
    abstract
    extern

indexer-declarator:
    type this [ formal-parameter-list ]
    type interface-type . this [ formal-parameter-list ]

operator-declaration:
    attributes_opt operator-modifiers operator-declarator operator-body

operator-modifiers:
    operator-modifier
    operator-modifiers operator-modifier

operator-modifier:
    public
    static
    extern

operator-declarator:
    unary-operator-declarator
    binary-operator-declarator
    conversion-operator-declarator

unary-operator-declarator:
    type operator overloadable-unary-operator ( fixed-parameter )

overloadable-unary-operator: 以下之一
    +  -  !  ~  ++  --  true  false

binary-operator-declarator:
    type operator overloadable-binary-operator ( fixed-parameter , fixed-parameter )

overloadable-binary-operator: 以下之一
    +  -  *  /  %  &  |  ^  <<  right-shift
    ==  !=  >  <  >=  <=

conversion-operator-declarator:
    implicit operator type ( fixed-parameter )
    explicit operator type ( fixed-parameter )

operator-body:
    block
    ;

constructor-declaration:
    attributes_opt constructor-modifiers_opt constructor-declarator constructor-body

constructor-modifiers:
    constructor-modifier
    constructor-modifiers constructor-modifier

constructor-modifier:
    public
    protected
    internal
    private
    extern

constructor-declarator:
    identifier ( formal-parameter-list_opt ) constructor-initializer_opt

constructor-initializer:
    : base ( argument-list_opt )
    : this ( argument-list_opt )

constructor-body:
    block
    ;

static-constructor-declaration:
    attributes_opt static-constructor-modifiers identifier ( ) static-constructor-body

static-constructor-modifiers:
    extern_opt static
    static extern_opt

static-constructor-body:
    block
    ;

finalizer-declaration:
    attributes_opt extern_opt ~ identifier ( ) finalizer-body
finalizer-body:
    block
    ;

## A.3.8 结构体

struct-declaration:
    attributes_opt struct-modifiers_opt partial_opt struct identifier type-parameter-list_opt
    struct-interfaces_opt type-parameter-constraints-clauses_opt struct-body ;_opt
struct-modifiers:
    struct-modifier
    struct-modifiers struct-modifier
struct-modifier:
    new
    public
    protected
    internal
    private
struct-interfaces:
    : interface-type-list
struct-body:
    { struct-member-declarations_opt }
struct-member-declarations:
    struct-member-declaration
    struct-member-declarations struct-member-declaration
struct-member-declaration:
    ...
    fixed-size-buffer-declaration

## A.3.9 数组

array-initializer:
    { variable-initializer-list_opt }
    { variable-initializer-list , }
variable-initializer-list:
    variable-initializer
    variable-initializer-list , variable-initializer
variable-initializer:
    expression
    array-initializer

## A.3.10 接口

interface-declaration:
    attributes_opt interface-modifiers_opt partial_opt interface
    identifier variant-type-parameter-list_opt
    interface-base_opt type-parameter-constraints-clauses_opt interface-body ;_opt
interface-modifiers:
    interface-modifier
    interface-modifiers interface-modifier

interface-modifier:
    new
    public
    protected
    internal
    private

variant-type-parameter-list:
    < variant-type-parameters >

variant-type-parameters:
    attributes_opt variance-annotation_opt type-parameter
    variant-type-parameters , attributes_opt variance-annotation_opt type-parameter

variance-annotation:
    in
    out

interface-base:
    : interface-type-list

interface-body:
    { interface-member-declarations_opt }

interface-member-declarations:
    interface-member-declaration
    interface-member-declarations interface-member-declaration

interface-member-declaration:
    interface-method-declaration
    interface-property-declaration
    interface-event-declaration
    interface-indexer-declaration

interface-method-declaration:
    attributes_opt new_opt return-type identifier type-parameter-list_opt
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

interface-property-declaration:
    attributes_opt new_opt type identifier { interface-accessors }

interface-accessors:
    attributes_opt get ;
    attributes_opt set ;
    attributes_opt get ; attributes_opt set ;
    attributes_opt set ; attributes_opt get ;

interface-event-declaration:
    attributes_opt new_opt event type identifier ;

interface-indexer-declaration:
    attributes_opt new_opt type this [ formal-parameter-list ] { interface-accessors }

## A.3.11 枚举

enum-declaration:
    attributes_opt enum-modifiers_opt enum identifier enum-base_opt enum-body ;_opt

enum-base:
    : integral-type

enum-body:
    { enum-member-declarations_opt }
    { enum-member-declarations , }

enum-modifiers:
    enum-modifier
    enum-modifiers enum-modifier

enum-modifier:
    new
    public
    protected
    internal
    private

enum-member-declarations:
    enum-member-declaration
    enum-member-declarations , enum-member-declaration

enum-member-declaration:
    attributes_opt identifier
    attributes_opt identifier = constant-expression

## A.3.12 委托

delegate-declaration:
    attributes_opt delegate-modifiers_opt delegate return-type
    identifier variant-type-parameter-list_opt
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

delegate-modifiers:
    delegate-modifier
    delegate-modifiers delegate-modifier

delegate-modifier:
    new
    public
    protected
    internal
    private

## A.3.13 属性

global-attributes:
    global-attribute-sections

global-attribute-sections:
    global-attribute-section
    global-attribute-sections global-attribute-section

global-attribute-section:
    [ global-attribute-target-specifier attribute-list ]
    [ global-attribute-target-specifier attribute-list , ]

global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    标识符 等于 assembly 或 module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-sections attribute-section



```bnf
attribute-section:
    [ attribute-target-specifier_opt attribute-list ]
    [ attribute-target-specifier_opt attribute-list , ]
attribute-target-specifier:
    attribute-target :
attribute-target:
    identifier not equal to assembly or module
    keyword
attribute-list:
    attribute
    attribute-list , attribute
attribute:
    attribute-name attribute-arguments_opt
attribute-name:
    type-name
attribute-arguments:
    ( positional-argument-list_opt )
    ( positional-argument-list , named-argument-list )
    ( named-argument-list )
positional-argument-list:
    positional-argument
    positional-argument-list , positional-argument
positional-argument:
    argument-name_opt attribute-argument-expression
named-argument-list:
    named-argument
    named-argument-list , named-argument
named-argument:
    identifier = attribute-argument-expression
attribute-argument-expression:
    expression
```

### A.4 不安全代码的语法扩展

```bnf
class-modifier:
    ...
    unsafe
struct-modifier:
    ...
    unsafe
interface-modifier:
    ...
    unsafe
delegate-modifier:
    ...
    unsafe
field-modifier:
    ...
    unsafe
method-modifier:
  ...
  unsafe
property-modifier:
  ...
  unsafe
event-modifier:
  ...
  unsafe
indexer-modifier:
  ...
  unsafe
operator-modifier:
  ...
  unsafe
constructor-modifier:
  ...
  unsafe
finalizer-declaration:
  attributesopt externopt unsafeopt ~ identifier ( ) finalizer-body
  attributesopt unsafeopt externopt ~ identifier ( ) finalizer-body
static-constructor-modifiers:
  externopt unsafeopt static
  unsafeopt externopt static
  externopt static unsafeopt
  unsafeopt static externopt
  static externopt unsafeopt
  static unsafeopt externopt
embedded-statement:
  ...
  unsafe-statement
unsafe-statement:
  unsafe block
type:
  ...
  pointer-type
non-array-type:
  ...
  pointer-type
pointer-type:
  unmanaged-type *
  void *
unmanaged-type:
  type
primary-no-array-creation-expression:
  ...
  pointer-member-access
  pointer-element-access
unary-expression:
  ...
  pointer-indirection-expression
  addressof-expression
pointer-indirection-expression:
  * unary-expression
pointer-member-access:
  primary-expression -> identifier type-argument-list_opt
pointer-element-access:
  primary-no-array-creation-expression [ expression ]
addressof-expression:
  & unary-expression
embedded-statement:
  ...
  fixed-statement
fixed-statement:
  fixed ( pointer-type fixed-pointer-declarators ) embedded-statement
fixed-pointer-declarators:
  fixed-pointer-declarator
  fixed-pointer-declarators , fixed-pointer-declarator
fixed-pointer-declarator:
  identifier = fixed-pointer-initializer
fixed-pointer-initializer:
  & variable-reference
  expression
struct-member-declaration:
  ...
  fixed-size-buffer-declaration
fixed-size-buffer-declaration:
  attributes_opt fixed-size-buffer-modifiers_opt fixed buffer-element-type
  fixed-size-buffer-declarators ;
fixed-size-buffer-modifiers:
  fixed-size-buffer-modifier
  fixed-size-buffer-modifier fixed-size-buffer-modifiers
fixed-size-buffer-modifier:
  new
  public
  protected
  internal
  private
  unsafe
buffer-element-type:
  type
fixed-size-buffer-declarators:
  fixed-size-buffer-declarator
  fixed-size-buffer-declarator , fixed-size-buffer-declarators
fixed-size-buffer-declarator:
  identifier [ constant-expression ]
```

- 9. 指针与整数之间的映射（§23.5.1）。
- 10. 将一元 * 运算符应用于空指针的效果（§23.6.2）。
- 11. 指针算术溢出指针类型域时的行为（§23.6.6、§23.6.7）。
- 12. 非预定义值类型的 sizeof 运算符的结果（§23.6.9）。
- 13. 如果数组表达式为 null 或数组具有零个元素，fixed 语句的行为（§23.7）。
- 14. 如果字符串表达式为 null，fixed 语句的行为（§23.7）。
- 15. 进行大小为零的堆栈分配时返回的值（§23.9）。

### B.4 未指定行为

- 1. 对象一旦符合终结条件，其终结器（如果有）运行的时间（§8.9）。
- 2. 在未检查上下文中，将超出范围的 float 或 double 值转换为整型时结果的值（§11.3.2）。
- 3. 由匿名方法表达式生成的委托的确切目标对象和目标方法（§11.7.2）。
- 4. 数组的布局，不安全上下文除外（§12.7.11.5）。
- 5. 除了通过求值和调用 lambda 表达式或匿名方法表达式之外，是否存在任何方式执行匿名函数的块（§12.16.3）。
- 6. 静态字段初始化的确切时机（§15.5.6.2）。
- 7. 枚举器对象正在运行时调用 MoveNext 的结果（§15.14.5.2）。
- 8. 枚举器对象处于 before、running 或 after 状态时访问 Current 的结果（§15.14.5.3）。
- 9. 枚举器对象处于 running 状态时调用 Dispose 的结果（§15.14.5.4）。
- 10. 在多个部分中声明的类型的特性，通过以未指定顺序合并其各个部分的特性来确定（§22.3）。
- 11. 成员打包到结构中的顺序（§23.6.9）。
- 12. 终结器执行期间发生异常，并且该执行未被捕获（§21.4）。
- 13. 如果多个成员匹配，哪个成员是 I.M 的实现（§18.6.5）。

### B.5 其他问题

- 1. 浮点表达式求值的精确结果可能因实现而异，因为允许实现使用比所需更大的范围和/或精度来求值此类表达式。（§9.3.7）
- 2. CLI 保留某些签名以兼容其他编程语言。（§15.3.9.7）

信息性文本结束。

## 附录 C. 标准库

### C.1 概述

符合规范的 C# 实现应提供一组具有特定语义的最小类型集。这里按命名空间和类型的字母顺序列出这些类型及其成员。有关这些类型及其成员的形式定义，请参考 ISO/IEC 23271:2012《公共语言基础结构（CLI）》第 IV 部分；基类库（BCL）、扩展数值库和扩展数组库，这些内容通过引用并入本规范。

**本文本为信息性内容。**

标准库旨在成为符合规范的 C# 实现所需的最小类型和成员集。因此，它仅包含 C# 语言规范明确要求的那些成员。

预期符合规范的 C# 实现将提供显著更广泛的库，以便能够编写有用的程序。例如，符合规范的实现可以通过以下方式扩展此库：

- 添加命名空间。
- 添加类型。
- 向非接口类型添加成员。
- 添加中间基类或接口。
- 让结构和类类型实现其他接口。
- 向现有类型和成员添加特性（ConditionalAttribute 除外）。

信息性文本结束。

### C.2 ISO/IEC 23271 中定义的标准库类型

```
namespace System
{
    public class ArgumentException : SystemException
    {
        public ArgumentException();
        public ArgumentException(string message);
        public ArgumentException(string message, Exception innerException);
    }
}
namespace System
{
    public delegate void Action();
}
namespace System
{
    public class ArithmeticException : Exception
    {
        public ArithmeticException();
        public ArithmeticException(string message);
        public ArithmeticException(string message, Exception innerException);
    }
}
```

```
namespace System
{
    public abstract class Array : IList, ICollection, IEnumerable
    {
        public int Length { get; }
        public int Rank { get; }
        public int GetLength(int dimension);
    }
}
```

```
namespace System
{
    public class ArrayTypeMismatchException : Exception
    {
        public ArrayTypeMismatchException();
        public ArrayTypeMismatchException(string message);
        public ArrayTypeMismatchException(string message,
            Exception innerException);
    }
}
```

```
namespace System
{
    [AttributeUsageAttribute(AttributeTargets.All, Inherited = true,
        AllowMultiple = false)]
    public abstract class Attribute
    {
        protected Attribute();
    }
}
```

```
namespace System
{
    public enum AttributeTargets
    {
        Assembly = 0x1,
        Module = 0x2,
        Class = 0x4,
        Struct = 0x8,
        Enum = 0x10,
        Constructor = 0x20,
        Method = 0x40,
        Property = 0x80,
        Field = 0x100,
        Event = 0x200,
        Interface = 0x400,
        Parameter = 0x800,
        Delegate = 0x1000,
        ReturnValue = 0x2000,
        GenericParameter = 0x4000,
        All = 0x7FFF
    }
}
```

```
namespace System
{
    [AttributeUsageAttribute(AttributeTargets.Class, Inherited = true)]
    public sealed class AttributeUsageAttribute : Attribute
    {
        public AttributeUsageAttribute(AttributeTargets validOn);
        public bool AllowMultiple { get; set; }
        public bool Inherited { get; set; }
        public AttributeTargets ValidOn { get; }
    }
}
```

namespace System
{
    public struct Boolean
    {
    }
}

namespace System
{
    public struct Byte
    {
    }
}

namespace System
{
    public struct Char
    {
    }
}

namespace System
{
    public struct Decimal
    {
    }
}

namespace System
{
    public abstract class Delegate
    {
    }
}

namespace System
{
    public class DivideByZeroException : ArithmeticException
    {
        public DivideByZeroException();
        public DivideByZeroException(string message);
        public DivideByZeroException(string message, Exception innerException);
    }
}

namespace System
{
    public struct Double
    {
    }
}

namespace System
{
    public abstract class Enum : ValueType
    {
        protected Enum();
    }
}

namespace System
{
    public class Exception
    {
        public Exception();
        public Exception(string message);
        public Exception(string message, Exception innerException);
        public sealed Exception InnerException { get; }
        public virtual string Message { get; }
    }
}

namespace System
{
    public class GC
    {
    }
}

namespace System
{
    public interface IDisposable
    {
        public void Dispose();
    }
}

namespace System
{
    public sealed class IndexOutOfRangeException : Exception
    {
        public IndexOutOfRangeException();
        public IndexOutOfRangeException(string message);
        public IndexOutOfRangeException(string message,
            Exception innerException);
    }
}

namespace System
{
    public struct Int16
    {
    }
}

namespace System
{
    public struct Int32
    {
    }
}

namespace System
{
    public struct Int64
    {
    }
}

namespace System
{
    public struct IntPtr
    {
    }
}

namespace System.Runtime.CompilerServices
{
    public sealed class IndexerNameAttribute: Attribute
    {
        public IndexerNameAttribute(String indexerName);
    }
}

namespace System.Collections.Generic
{
    public interface IReadOnlyCollection<out T> : IEnumerable<T>
    {
        int Count { get; }
    }
}

namespace System.Collections.Generic
{
    public interface IReadOnlyList<out T> : IReadOnlyCollection<T>
    {
        T this[int index] { get; }
    }
}

namespace System
{
    public class InvalidCastException : Exception
    {
        public InvalidCastException();
        public InvalidCastException(string message);
        public InvalidCastException(string message, Exception innerException);
    }
}

namespace System
{
    public class InvalidOperationException : Exception
    {
        public InvalidOperationException();
        public InvalidOperationException(string message);
        public InvalidOperationException(string message,
            Exception innerException);
    }
}

namespace System.Reflection
{
    public abstract class MemberInfo
    {
        protected MemberInfo();
    }
}

namespace System
{
    public class NotSupportedException : Exception
    {
        public NotSupportedException();
        public NotSupportedException(string message);
        public NotSupportedException(string message, Exception innerException);
    }
}

namespace System
{
    public struct Nullable<T>
    {
        public bool HasValue { get; }
        public T Value { get; }
    }
}

namespace System
{
    public class NullReferenceException : Exception
    {
        public NullReferenceException();
        public NullReferenceException(string message);
        public NullReferenceException(string message, Exception innerException);
    }
}

namespace System
{
    public class Object
    {
        public Object();
        ~Object();
        public virtual bool Equals(object obj);
        public virtual int GetHashCode();
        public Type GetType();
        public virtual string ToString();
    }
}

namespace System
{
    [AttributeUsageAttribute(AttributeTargets.Class
        | AttributeTargets.Struct
        | AttributeTargets.Enum | AttributeTargets.Interface
        | AttributeTargets.Constructor | AttributeTargets.Method
        | AttributeTargets.Property | AttributeTargets.Field
        | AttributeTargets.Event | AttributeTargets.Delegate,
        Inherited = false)]
    public sealed class ObsoleteAttribute : Attribute
    {
        public ObsoleteAttribute();
        public ObsoleteAttribute(string message);
        public ObsoleteAttribute(string message, bool error);
        public bool IsError { get; }
        public string Message { get; }
    }
}

namespace System
{
    public class OutOfMemoryException : Exception
    {
        public OutOfMemoryException();
        public OutOfMemoryException(string message);
        public OutOfMemoryException(string message, Exception innerException);
    }
}

namespace System
{
    public class OverflowException : ArithmeticException
    {
        public OverflowException();
        public OverflowException(string message);
        public OverflowException(string message, Exception innerException);
    }
}

namespace System
{
    public struct SByte
    {
    }
}

namespace System
{
    public struct Single
    {
    }
}

namespace System
{
    public sealed class StackOverflowException : Exception
    {
        public StackOverflowException();
        public StackOverflowException(string message);
        public StackOverflowException(string message, Exception innerException);
    }
}

namespace System
{
    public sealed class String : IEnumerable<char>, IEnumerable
    {
        public int Length { get; }
        public char this[int index] { get; }
    }
}

namespace System
{
    public abstract class Type : MemberInfo
    {
    }
}

namespace System
{
    public sealed class TypeInitializationException : Exception
    {
        public TypeInitializationException(string fullTypeName,
            Exception innerException);
    }
}

namespace System
{
    public struct UInt16
    {
    }
}

namespace System
{
    public struct UInt32
    {
    }
}

namespace System
{
    public struct UInt64
    {
    }
}

namespace System
{
    public struct UIntPtr
    {
    }
}

namespace System
{
    public abstract class ValueType
    {
        protected ValueType();
    }
}

namespace System.Collections
{
    public interface ICollection : IEnumerable
    {
        public int Count { get; }
        public bool IsSynchronized { get; }
        public object SyncRoot { get; }
        public void CopyTo(Array array, int index);
    }
}

namespace System.Collections
{
    public interface IEnumerable
    {
        public IEnumerator GetEnumerator();
    }
}

namespace System.Collections
{
    public interface IEnumerator
    {
        public object Current { get; }
        public bool MoveNext();
        public void Reset();
    }
}

namespace System.Collections
{
    public interface IList : ICollection, IEnumerable
    {
        public bool IsFixedSize { get; }
        public bool IsReadOnly { get; }
        public object this[int index] { get; set; }
        public int Add(object value);
        public void Clear();
        public bool Contains(object value);
        public int IndexOf(object value);
        public void Insert(int index, object value);
        public void Remove(object value);
        public void RemoveAt(int index);
    }
}

namespace System.Collections.Generic
{
    public interface ICollection<T> : IEnumerable<T>
    {
        public int Count { get; }
        public bool IsReadOnly { get; }
        public void Add(T item);
        public void Clear();
        public bool Contains(T item);
        public void CopyTo(T[] array, int arrayIndex);
        public bool Remove(T item);
    }
}

namespace System.Collections.Generic
{
    public interface IEnumerable<T> : IEnumerable
    {
        public IEnumerator<T> GetEnumerator();
    }
}

namespace System.Collections.Generic
{
    public interface IEnumerator<T> : IDisposable, IEnumerator
    {
        public T Current { get; }
    }
}

namespace System.Collections.Generic
{
    public interface IList<T> : ICollection<T>
    {
        public T this[int index] { get; set; }
        public int IndexOf(T item);
        public void Insert(int index, T item);
        public void RemoveAt(int index);
    }
}

namespace System.Diagnostics
{
    [AttributeUsageAttribute(AttributeTargets.Method
    | AttributeTargets.Class, AllowMultiple = true)]
    public sealed class ConditionalAttribute : Attribute
    {
        public ConditionalAttribute(string conditionString);
        public string ConditionString { get; }
    }
}

namespace System.Threading
{
    public static class Monitor
    {
        public static void Enter(object obj);
        public static void Exit(object obj);
    }
}





## C.3 未在 ISO/IEC 23271:2012 中定义的标准库类型

以下类型（包括列出的成员）必须在符合规范的标准库中定义。（这些类型可能会在 ISO/IEC 23271 的未来版本中定义。）预计其中许多类型将提供比所列更多的成员。

符合规范的实现可以将 Task.GetAwaiter() 和 Task<T>.GetAwaiter() 作为扩展方法提供。

```
namespace System.Runtime.CompilerServices
{
    [AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
    public sealed class CallerFilePathAttribute : Attribute
    {
        public CallerFilePathAttribute() {}
    }
}
```

```
namespace System.Runtime.CompilerServices
{
    [AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
    public sealed class CallerLineNumberAttribute : Attribute
    {
        public CallerLineNumberAttribute() {}
    }
}
```

```
namespace System.Runtime.CompilerServices
{
    [AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
    public sealed class CallerMemberNameAttribute : Attribute
    {
        public CallerMemberNameAttribute() {}
    }
}
```

```
namespace System.Linq.Expressions
{
    public sealed class Expression<TDelegate>
    {
        // See Section 12.7.3 for details on what
        // Delegate types (TDelegate) must be supported,
        // and which may be omitted.
        public TDelegate Compile();
    }
}
```

```
namespace System.Runtime.CompilerServices
{
    public interface INotifyCompletion
    {
        void OnCompleted(Action continuation);
    }
}
```

```
namespace System.Runtime.CompilerServices
{
    public interface ICriticalNotifyCompletion : INotifyCompletion
    {
        void UnsafeOnCompleted(Action continuation);
    }
}
```

```
namespace System.Threading.Tasks
{
    public class Task
    {
        public System.Runtime.CompilerServices.TaskAwaiter GetAwaiter();
    }
}
```

```
namespace System.Threading.Tasks
{
    public class Task<TResult> : System.Threading.Tasks.Task
    {
        public new System.Runtime.CompilerServices.TaskAwaiter<TResult> GetAwaiter();
    }
}
```

```
namespace System.Runtime.CompilerServices
{
    public struct TaskAwaiter : ICriticalNotifyCompletion, INotifyCompletion
    {
        public bool IsCompleted { get; }
        public void GetResult();
    }
}
```

```
namespace System.Runtime.CompilerServices
{
    public struct TaskAwaiter<T> : ICriticalNotifyCompletion, INotifyCompletion
    {
        public bool IsCompleted { get; }
        public T GetResult();
    }
}
```

## 附录 D. 文档注释

本附录是资料性的。

### D.1 概述

C# 为程序员提供了一种机制，使他们可以使用包含 XML 文本的特殊注释语法来记录其代码。在源代码文件中，具有某种形式的注释可用于指示工具根据这些注释及其前面的源代码元素生成 XML。使用此类语法的注释称为文档注释。它们必须紧挨在用户定义类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。XML 生成工具称为文档生成器。（此生成器可以是 C# 编译器本身，但不必是。）文档生成器生成的输出称为文档文件。文档文件用作文档查看器的输入，文档查看器是一种旨在以某种可视方式显示类型信息及其关联文档的工具。

不要求符合规范的 C# 编译器检查文档注释的语法；此类注释只是普通注释。但是，允许符合规范的编译器进行此类检查。

本规范建议在文档注释中使用一组标准标记，但不要求使用这些标记；如果需要，也可以使用其他标记，只要遵循格式良好的 XML 规则即可。对于面向 CLI 的 C# 实现，它还提供了有关文档生成器和文档文件格式的信息。未提供有关文档查看器的信息。

### D.2 简介

具有特殊形式的注释可用于指示工具根据这些注释及其前面的源代码元素生成 XML。此类注释是以三个斜杠（///）开头的单行注释，或以一个斜杠和两个星号（/**）开头的分隔注释。它们必须紧挨在它们所注释的用户定义类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。特性节（§22.3）被视为声明的一部分，因此文档注释必须位于应用于类型或成员的特性之前。

语法：

```
single-line-doc-comment::
/// input-characters_opt

delimited-doc-comment::
/** delimited-comment-text_opt */
```

在单行文档注释中，如果与当前单行文档注释相邻的每个单行文档注释中，在 /// 字符之后都有一个空白字符，则该空白字符不包含在 XML 输出中。

在分隔文档注释中，如果第二行上的第一个非空白字符是星号，并且在分隔文档注释内的每一行开头都重复相同的可选空白字符加星号字符的模式，则该重复模式的字符不包含在 XML 输出中。该模式可以包括星号字符之后以及之前的空白字符。

示例：

```
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
public class Point
{
    /// <summary>method <c>draw</c> renders the point.</summary>
    void draw() {...}
}
```

文档注释中的文本必须根据 XML 规则（http://www.w3.org/TR/REC-xml）是格式良好的。如果 XML 格式不正确，则会生成警告，并且文档文件将包含一条注释，说明遇到了错误。

尽管开发者可以自由创建自己的标记集，但 §D.3 定义了一组建议的标记。一些建议的标记具有特殊含义：

- `<param>` 标记用于描述参数。如果使用了此类标记，文档生成器必须验证指定的参数存在，并且所有参数都在文档注释中进行了描述。如果此类验证失败，文档生成器会发出警告。
- `cref` 属性可以附加到任何标记，以提供对代码元素的引用。文档生成器必须验证此代码元素存在。如果验证失败，文档生成器会发出警告。在查找 `cref` 属性中描述的名称时，文档生成器必须根据源代码中出现的 using 语句遵守命名空间可见性。对于泛型代码元素，不能使用常规泛型语法（例如 `"List<T>"`），因为它会产生无效的 XML。可以使用花括号代替尖括号（例如 `"List{T}"`），或者可以使用 XML 转义语法（例如 `"List&lt;T&gt;"`）。
- `<summary>` 标记旨在由文档查看器用来显示有关类型或成员的附加信息。
- `<include>` 标记包含来自外部 XML 文件的信息。

请特别注意，文档文件不提供有关类型和成员的完整信息（例如，它不包含任何类型信息）。要获取有关类型或成员的此类信息，必须将文档文件与对该类型或成员的反射结合使用。

### D.3 建议的标记

#### D.3.1 概述

文档生成器必须接受并处理任何根据 XML 规则有效的标记。以下标记提供了用户文档中的常用功能。（当然，也可以使用其他标记。）




| Tag | Reference | Purpose |
|---|---|---|
| `<c>` | §D.3.2 | 将文本设置为类似代码的字体 |
| `<code>` | §D.3.3 | 设置一行或多行源代码或程序输出 |
| `<example>` | §D.3.4 | 表示一个示例 |
| `<exception>` | §D.3.5 | 标识方法可能抛出的异常 |
| `<list>` | §D.3.7 | 创建列表或表格 |
| `<include>` | §D.3.6 | 从外部文件包含 XML |
| `<para>` | §D.3.8 | 允许向文本添加结构 |
| `<param>` | §D.3.9 | 描述方法或构造函数的参数 |
| `<paramref>` | §D.3.10 | 标识某个词是参数名 |
| `<permission>` | §D.3.11 | 记录成员的安全可访问性 |
| `<remarks>` | §D.3.12 | 描述类型的附加信息 |
| `<returns>` | §D.3.13 | 描述方法的返回值 |
| `<see>` | §D.3.14 | 指定链接 |
| `<seealso>` | §D.3.15 | 生成“另请参阅”条目 |
| `<summary>` | §D.3.16 | 描述类型或类型的成员 |
| `<typeparam>` | §D.3.17 | 描述泛型类型或方法的类型参数 |
| `<typeparamref>` | §D.3.18 | 标识某个词是类型参数名 |
| `<value>` | §D.3.19 | 描述属性 |

## D.3.2 <c>

此标签提供了一种机制，用于指示描述中的文本片段应使用特殊字体设置，例如用于代码块的字体。对于实际代码行，请使用 <code> (§D.3.3)。

### Syntax:

```
<c>text</c>
```

### Example:

```
/// <summary>class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
public class Point
{
    // ...
}
```

## D.3.3 <code>

此标签用于以某种特殊字体设置一行或多行源代码或程序输出。对于叙述中的小代码片段，请使用 <c> (§D.3.2)。

### Syntax:

```
<code>source code or program output</code>
```

### Example:

```
/// <summary>This method changes the point’s location by
/// the given x- and y- offsets.
/// <example>For example:
/// <code>
/// Point p = new Point(3,5);
/// p.Translate(-1,3);
/// </code>
/// results in <paramref name="p"/>'s having the value (2,8).
/// </example>
/// </summary>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

## D.3.4 <example>

此标签允许在注释中包含示例代码，以指定方法或其他库成员可能如何使用。通常，这也涉及使用 <code> (§D.3.3) 标签。

### Syntax:

```
<example>description</example>
```

### Example:

请参阅 <code> (§D.3.3) 以获取示例。

## D.3.5 <exception>

此标签提供了一种记录方法可能抛出的异常的方式。

### Syntax:

```
<exception cref="member">description</exception>
```

where

cref="member"
成员的名称。文档生成器检查给定的成员是否存在，并将成员翻译为文档文件中的规范元素名称。

description
抛出异常的情形的描述。

### Example:

```
public class DataBaseOperations
{
    /// <exception cref="MasterFileFormatCorruptException"></exception>
    /// <exception cref="MasterFileLockedOpenException"></exception>
    public static void ReadRecord(int flag) {
        if (flag == 1)
            throw new MasterFileFormatCorruptException();
        else if (flag == 2)
            throw new MasterFileLockedOpenException();
        } // ...
    }
```

## D.3.6 <include>

此标签允许从源代码文件外部的 XML 文档中包含信息。外部文件必须是格式良好的 XML 文档，并且会将 XPath 表达式应用于该文档以指定要包含的 XML。随后 <include> 标签将被外部文档中选定的 XML 替换。

### Syntax:

```
<include file="filename" path="xpath" />
```

where

file="filename"
外部 XML 文件的文件名。文件名相对于包含 include 标签的文件进行解释。

path="xpath"
选择外部 XML 文件中部分 XML 的 XPath 表达式。

### Example:

如果源代码包含如下声明：

```
/// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class IntList { ... }
```

并且外部文件 "docs.xml" 具有以下内容：

```
<?xml version="1.0"?>
<extradoc>
  <class name="IntList">
    <summary>
      Contains a list of integers.
    </summary>
  </class>
  <class name="StringList">
    <summary>
      Contains a list of integers.
    </summary>
  </class>
</extradoc>
```

那么输出的文档与源代码包含以下内容时相同：

```
/// <summary>
/// Contains a list of integers.
/// </summary>
public class IntList { ... }
```

## D.3.7 <list>

此标签用于创建项目列表或表格。它可以包含 <listheader> 块来定义表格或定义列表的标题行。（在定义表格时，只需在标题中提供 term 条目。）

列表中的每个项目都用 <item> 块指定。在创建定义列表时，必须同时指定 term 和 description。然而，对于表格、项目符号列表或编号列表，只需指定 description。

### Syntax:

```
<list type="bullet" | "number" | "table">
  <listheader>
    <term>term</term>
    <description>description</description>
  </listheader>
  <item>
    <term>term</term>
    <description>description</description>
  </item>
  ...
```

```
<item>
  <term>term</term>
  <description>description</description>
</item>
</list>
```

where

- *术语*
要定义的术语，其定义在 *描述* 中。

- *描述*
项目符号或编号列表中的一个项目，或 *术语* 的定义。

### Example:

```
public class MyClass
{
/// <summary>Here is an example of a bulleted list:
/// <list type="bullet">
/// <item>
/// <description>Item 1.</description>
/// </item>
/// <item>
/// <description>Item 2.</description>
/// </item>
/// </list>
/// </summary>
public static void Main () {
    // ...
}
```

## D.3.8 `<para>`

此标签用于在其他标签内部，例如 `<summary>` (§D.3.16) 或 `<returns>` (§D.3.13)，并允许向文本添加结构。

### Syntax:

```
<para>content</para>
```

where

- *内容*
段落的文本。

### Example:

```
/// <summary>This is the entry point of the Point class testing program.
/// <para>This program tests each method and operator, and
/// is intended to be run after any non-trivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // ...
}
```

## D.3.9 `<param>`

此标签用于描述方法、构造函数或索引器的参数。

### Syntax:

```
<param name="name">description</param>
```

where

- *名称*
参数的名称。

- description
参数的描述。

### Example:

```
/// <summary>This method changes the point’s location to
/// the given coordinates.</summary>
/// <param name="xor">the new x-coordinate.</param>
/// <param name="yor">the new y-coordinate.</param>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

## D.3.10 <paramref>

此标签用于指示某个词是参数。文档文件可以被处理以以某种独特方式格式化该参数。

### Syntax:

```
<paramref name="name"/>
```

where

- name
参数的名称。

### Example:

```
/// <summary>This constructor initializes the new Point to
/// (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
/// <param name="xor">the new Point's x-coordinate.</param>
/// <param name="yor">the new Point's y-coordinate.</param>
public Point(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

## D.3.11 <permission>

此标签允许记录成员的安全可访问性。

### Syntax:

```
<permission cref="member">description</permission>
```

where

- member
成员的名称。文档生成器检查给定的代码元素是否存在，并将成员翻译为文档文件中的规范元素名称。

- description
对成员访问的描述。

### Example:

```
/// <permission cref="System.Security.PermissionSet">Everyone can
/// access this method.</permission>
public static void Test() {
    // ...
}
```



### D.3.12 `<remarks>`

此标记用于指定有关类型的额外信息。使用 `<summary>`（§D.3.16）描述类型本身以及类型的成员。

**语法：**

```
    <remarks>description</remarks>
```

其中

*描述*

备注的文本。

**示例：**

```
    /// <summary>Class <c>Point</c> models a point in a
    /// two-dimensional plane.</summary>
    /// <remarks>Uses polar coordinates</remarks>
    public class Point
    {
        // ...
    }
```

### D.3.13 `<returns>`

此标记用于描述方法的返回值。

**语法：**

```
    <returns>description</returns>
```

其中

*描述*

返回值的描述。

**示例：**

```
    /// <summary>Report a point's location as a string.</summary>
    /// <returns>A string representing a point's location, in the form (x,y),
    ///     without any leading, trailing, or embedded whitespace.</returns>
    public override string ToString() {
        return "(" + X + "," + Y + ")";
    }
```

### D.3.14 `<see>`

此标记允许在文本中指定链接。使用 `<seealso>`（§D.3.15）指示要出现在“另请参阅”子句中的文本。

**语法：**

```
    <see cref="member"/>
```

其中

*成员*

成员的名称。文档生成器会检查给定的代码元素是否存在，并在生成的文档文件中将*成员*更改为该元素名称。

**示例：**

```
    /// <summary>This method changes the point's location to
    ///     the given coordinates. <see cref="Translate"/></summary>
    public void Move(int xor, int yor) {
        X = xor;
        Y = yor;
    }
```

```
/// <summary>This method changes the point's location by
/// the given x- and y-offsets. <see cref="Move"/>
/// </summary>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### D.3.15 `<seealso>`

此标记允许为“另请参阅”子句生成一个条目。使用 `<see>`（§D.3.14）指定文本中的链接。

**语法：**

```
<seealso cref="member"/>
```

其中

*成员*

成员的名称。文档生成器会检查给定的代码元素是否存在，并在生成的文档文件中将*成员*更改为该元素名称。

**示例：**

```
/// <summary>This method determines whether two Points have the same location.</summary>
/// <seealso cref="operator==" />
/// <seealso cref="operator!=" />
public override bool Equals(object o) {
    // ...
}
```

### D.3.16 `<summary>`

此标记可用于描述类型或类型的成员。使用 `<remarks>`（§D.3.12）描述类型本身。

**语法：**

```
<summary>description</summary>
```

### D.3.17 `<typeparam>`

此标记用于描述泛型类型或方法的类型参数。

**语法：**

```
<typeparam name="name">description</typeparam>
```

**示例：**

```
/// <summary>A generic_list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
public class MyList<T> {
    """
}
```

### D.3.18 `<typeparamref>`

此标记用于指示某个单词是类型参数。可以处理文档文件，以某种独特方式格式化此类型参数。

**语法：**

```
<typeparamref name="name"/>
```

其中

*名称*

类型参数的名称。

**示例：**

```
/// <summary>This method fetches data and returns a list of <typeparamref name="T" />.</summary>
/// <param name="string">query to execute</param>
public List<T> FetchData<T>(string query) {
    """
}
```

### D.3.19 `<value>`

此标记允许描述属性。

**语法：**

```
<value>property description</value>
```

其中

*属性描述*

属性的描述。

## D.4 处理文档文件

### D.4.1 概述

以下信息面向以 CLI 为目标的 C# 实现。

文档生成器会为源代码中每个带有文档注释标记的元素生成一个 ID 字符串。此 ID 字符串唯一标识一个源元素。文档查看器可以使用 ID 字符串来标识文档所适用的对应项。

文档文件不是源代码的层次结构表示；相反，它是一个平面列表，其中每个元素都有一个生成的 ID 字符串。

### D.4.2 ID 字符串格式

文档生成器在生成 ID 字符串时遵循以下规则：

- 字符串中不放置空白字符。
- 字符串的第一部分通过一个字符后跟冒号来标识所记录成员的种类。定义了以下成员种类：

| 字符 | 描述 |
|---|---|
| E | 事件 |
| F | 字段 |
| M | 方法（包括构造函数、终结器和运算符） |
| N | 命名空间 |
| P | 属性（包括索引器） |
| T | 类型（如类、委托、枚举、接口和结构） |
| ! | 错误字符串；字符串的其余部分提供有关错误的信息。例如，文档生成器会为无法解析的链接生成错误信息。 |

- 字符串的第二部分是该元素的完全限定名，从命名空间的根开始。元素名称、其所在类型和命名空间用句点分隔。如果项本身的名称包含句点，则这些句点由 #（U+0023）字符替换。（假定没有元素的名称中包含此字符。）
- 对于带参数的方法和属性，后面是参数列表，括在括号中。对于没有参数的，省略括号。参数用逗号分隔。每个参数的编码与 CLI 签名相同，如下所示：
- 参数由它们的文档名称表示，该名称基于其完全限定名，并按如下方式修改：
  - 表示泛型类型的参数会追加一个“`”字符，后跟类型参数的数量
  - 具有 out 或 ref 修饰符的参数在其类型名后带有 @。按值或通过 params 传递的参数没有特殊表示法。
  - 数组参数表示为 [ lowerbound : size , ... , lowerbound : size ]，其中逗号的数量比秩少一，并且每个维度的下界和大小（如果已知）用十进制表示。如果未指定下界或大小，则省略它。如果某个维度的下界和大小都被省略，则“:”也省略。交错数组用每层一个“[]”表示。
  - 具有除 void 之外的指针类型的参数使用类型名后的 * 表示。void 指针使用类型名 System.Void 表示。
  - 引用在类型上定义的泛型类型参数的参数使用“`”字符后跟类型参数的从零开始的索引进行编码。
  - 使用方法中定义的泛型类型参数的参数使用双反引号“``”，而不是用于类型的“`”。
  - 引用构造泛型类型的参数使用泛型类型编码，后跟“{”，再后跟以逗号分隔的类型参数列表，再后跟“}”。

### D.4.3 ID 字符串示例

以下每个示例都展示了一段 C# 代码片段，以及由每个能够带有文档注释的源元素生成的 ID 字符串：

类型使用其完全限定名表示，并附加泛型信息：

```
enum Color { Red, Blue, Green }
namespace Acme
{
    interface IProcess { ... }
    struct ValueType { ... }
    class Widget: IProcess
    {
        public class NestedClass { ... }
        public interface IMenuItem { ... }
        public delegate void Del(int i);
        public enum Direction { North, South, East, West }
    }
    class MyList<T>
    {
        class Helper<U,V>{ ... }
    }
}
```

```
"T:Color"
"T:Acme.IProcess"
"T:Acme.ValueType"
"T:Acme.Widget"
"T:Acme.Widget.NestedClass"
"T:Acme.Widget.IMenuItem"
"T:Acme.Widget.Del"
"T:Acme.Widget.Direction"
"T:Acme.MyList`1"
"T:Acme.MyList`1.Helper`2"
```

字段由其完全限定名表示。

```
namespace Acme
{
    struct ValueType
    {
        private int total;
    }
    class Widget: IProcess
    {
        public class NestedClass
        {
            private int value;
        }
        private string message;
        private static Color defaultColor;
        private const double PI = 3.14159;
        protected readonly double monthlyAverage;
        private long[] array1;
        private Widget[,] array2;
        private unsafe int *pCount;
        private unsafe float **ppValues;
    }
}
```



```text
"F:Acme.ValueType.total"
"F:Acme.Widget.NestedClass.value"
"F:Acme.Widget.message"
"F:Acme.Widget.defaultColor"
"F:Acme.Widget.PI"
"F:Acme.Widget.monthlyAverage"
"F:Acme.Widget.array1"
"F:Acme.Widget.array2"
"F:Acme.Widget.pCount"
"F:Acme.Widget.ppValues"
```

- 构造函数。

  ```csharp
  namespace Acme
  {
      class Widget: IProcess
      {
          static Widget() { ... }
          public Widget() { ... }
          public Widget(string s) { ... }
      }
  }
  ```

  "M:Acme.Widget.#ctor"
  "M:Acme.Widget.#ctor()"
  "M:Acme.Widget.#ctor(System.String)"
  
- 析构函数。

  ```csharp
  namespace Acme
  {
      class Widget: IProcess
      {
          ~Widget() { ... }
      }
  }
  ```

  "M:Acme.Widget.Finalize"
  
- 方法。

  ```csharp
  namespace Acme
  {
      struct ValueType
      {
          public void M(int i) { ... }
      }
      class Widget: IProcess
      {
          public class NestedClass
          {
              public void M(int i) { ... }
          }
          public static void M0() { ... }
          public void M1(char c, out float f, ref ValueType v) { ... }
          public void M2(short[] x1, int[,] x2, long[][] x3) { ... }
          public void M3(long[][] x3, Widget[][,] x4) { ... }
          public unsafe void M4(char *pc, Color **pf) { ... }
          public unsafe void M5(void *pv, double *[][,] pd) { ... }
          public void M6(int i, params object[] args) { ... }
      }
      class MyList<T>
      {
          public void Test(T t) { ... }
      }
  }
  ```

  ```csharp
  class UseList
  {
      public void Process(MyList<int> list) { ... }
      public MyList<T> GetValues<T>(T value) { ... }
  }
  ```

  ```text
  "M:Acme.ValueType.M(System.Int32)"
  "M:Acme.Widget.NestedClass.M(System.Int32)"
  "M:Acme.Widget.M0"
  "M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
  "M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
  "M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:][])"
  "M:Acme.Widget.M4(System.Char*,Color**)"
  "M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:][])"
  "M:Acme.Widget.M6(System.Int32,System.Object[])"
  "M:Acme.MyList`1.Test(0)"
  "M:Acme.UseList.Process(Acme.MyList<System.Int32>)"
  "M:Acme.UseList.GetValues`1(0)"
  ```

- 属性和索引器。

  ```csharp
  namespace Acme
  {
      class Widget: IProcess
      {
          public int width { get { ... } set { ... } }
          public int this[int i] { get { ... } set { ... } }
          public int this[string s, int i] { get { ... } set { ... } }
      }
  }
  ```

  ```text
  "P:Acme.Widget.width"
  "P:Acme.Widget.Item(System.Int32)"
  "P:Acme.Widget.Item(System.String,System.Int32)"
  ```

- 事件

  ```csharp
  namespace Acme
  {
      class Widget: IProcess
      {
          public event Del AnEvent;
      }
  }
  ```

  ```text
  "E:Acme.Widget.AnEvent"
  ```

- 一元运算符。

  ```csharp
  namespace Acme
  {
      class Widget: IProcess
      {
          public static Widget operator+(Widget x) { ... }
      }
  }
  ```

  ```text
  "M:Acme.Widget.op_UnaryPlus(Acme.Widget)"
  ```

  完整使用的一元运算符函数名称集合如下：op_UnaryPlus、op_UnaryNegation、op_LogicalNot、op_OnesComplement、op_Increment、op_Decrement、op_True 和 op_False。

- 二元运算符。

  ```csharp
  namespace Acme
  {
      class Widget: IProcess
      {
          public static Widget operator+(Widget x1, Widget x2) { ... }
      }
  }
  ```

  ```text
  "M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"
  ```

  完整使用的二元运算符函数名称集合如下：op_Addition、op_Subtraction、op_Multiply、op_Division、op_Modulus、op_BitwiseAnd、op_BitwiseOr、op_ExclusiveOr、op_LeftShift、op_RightShift、op_Equality、op_Inequality、op_LessThan、op_LessThanOrEqual、op_GreaterThan 和 op_GreaterThanOrEqual。

- 转换运算符在其后带有“~”，后跟返回类型。

  ```csharp
  namespace Acme
  {
      class Widget : IProcess
      {
          public static explicit operator int(Widget x) { ... }
          public static implicit operator long(Widget x) { ... }
      }
  }
  ```

  ```text
  "M:Acme.Widget.op_Explicit(Acme.Widget)->System.Int32"
  "M:Acme.Widget.op_Implicit(Acme.Widget)->System.Int64"
  ```

## D.5 示例

### D.5.1 C# 源代码

以下示例展示了 Point 类的源代码：

```csharp
namespace Graphics
{
    /// <summary>Class <c>Point</c> models a point in a two-dimensional plane.</summary>
    public class Point
    {
        /// <summary>Instance variable <c>x</c> represents the point's x-coordinate.</summary>
        private int x;
        /// <summary>Instance variable <c>y</c> represents the point's y-coordinate.</summary>
        private int y;
        /// <value>Property <c>X</c> represents the point's x-coordinate.</value>
        public int X
        {
            get { return x; }
            set { x = value; }
        }
        /// <value>Property <c>Y</c> represents the point's y-coordinate.</value>
        public int Y
        {
            get { return y; }
            set { y = value; }
        }
        /// <summary>This constructor initializes the new Point to (0,0).</summary>
        public Point() : this(0,0) {}

        /// <summary>This constructor initializes the new Point to
        /// (<paramref name="xor"/>, <paramref name="yor"/>).</summary>
        /// <param name="xor">is the new Point's x-coordinate.</param>
        /// <param name="yor">is the new Point's y-coordinate.</param>
        public Point(int xor, int yor) {
            X = xor;
            Y = yor;
        }

        /// <summary>This method changes the point's location to
        /// the given coordinates. <see cref="Translate"/></summary>
        /// <param name="xor">is the new x-coordinate.</param>
        /// <param name="yor">is the new y-coordinate.</param>
        public void Move(int xor, int yor) {
            X = xor;
            Y = yor;
        }

        /// <summary>This method changes the point's location by
        /// the given x- and y-offsets.
        /// <example>For example:
        /// <code>
        /// Point p = new Point(3,5);
        /// p.Translate(-1,3);
        /// </code>
        /// results in <c>p</c>'s having the value (2,8).
        /// <see cref="Move"/></example>
        /// </summary>
        /// <param name="xor">is the relative x-offset.</param>
        /// <param name="yor">is the relative y-offset.</param>
        public void Translate(int xor, int yor) {
            X += xor;
            Y += yor;
        }

        /// <summary>This method determines whether two Points have the same
        /// location.</summary>
        /// <param name="o">is the object to be compared to the current object.</param>
        /// <returns>True if the Points have the same location and they have the exact same type; otherwise, false.</returns>
        /// <seealso cref="operator==" />
        /// <seealso cref="operator!=" />
        public override bool Equals(object o) {
            if (o == null) {
                return false;
            }
            if (this == o) {
                return true;
            }
            if (GetType() == o.GetType()) {
                Point p = (Point)o;
                return (X == p.X) && (Y == p.Y);
            }
            return false;
        }

        /// <summary>Report a point's location as a string.</summary>
        /// <returns>A string representing a point's location, in the form (x,y), without any leading, trailing, or embedded whitespace.</returns>
        public override string ToString() {
            return "(" + X + "," + Y + ")";
        }

        /// <summary>This operator determines whether two Points have the same
        /// location.</summary>
        /// <param><c>p1</c> is the first Point to be compared.</param>
        /// <param><c>p2</c> is the second Point to be compared.</param>
        /// <returns>True if the Points have the same location and they have
        /// the exact same type; otherwise, false.</returns>
        /// <seealso cref="Equals"/>
        /// <seealso cref="operator!=" />
        public static bool operator==(Point p1, Point p2) {
            if ((object)p1 == null || (object)p2 == null) {
                return false;
            }

            if (p1.GetType() == p2.GetType()) {
                return (p1.X == p2.X) && (p1.Y == p2.Y);
            }

            return false;
        }

        /// <summary>This operator determines whether two Points have the same
        /// location.</summary>
        /// <param><c>p1</c> is the first Point to be compared.</param>
        /// <param><c>p2</c> is the second Point to be compared.</param>
        /// <returns>True if the Points do not have the same location and the
        /// exact same type; otherwise, false.</returns>
        /// <seealso cref="Equals"/>
        /// <seealso cref="operator==" />
        public static bool operator!=(Point p1, Point p2) {
            return !(p1 == p2);
        }
    }
}
```

### D.5.2 生成的 XML

以下是当向文档生成器提供上面所示的 Point 类源代码时产生的一个输出：

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
    <members>
        <member name="T:Graphics.Point">
            <summary>Class <c>Point</c> models a point in a two-dimensional plane.</summary>
        </member>
        <member name="F:Graphics.Point.x">
            <summary>Instance variable <c>x</c> represents the point's
            x-coordinate.</summary>
        </member>
        <member name="F:Graphics.Point.y">
            <summary>Instance variable <c>y</c> represents the point's
            y-coordinate.</summary>
        </member>
        <member name="M:Graphics.Point.#ctor">
            <summary>This constructor initializes the new Point to
            (0,0).</summary>
        </member>
```



<member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
<summary>此构造函数将新的 Point 初始化为
(<paramref name="x"/>, <paramref name="y"/>).</summary>
<param><c>x</c> 是新的 Point 的 x 坐标。</param>
<param><c>y</c> 是新的 Point 的 y 坐标。</param>
</member>

<member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
<summary>此方法将点的位置更改为
给定的坐标。 <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/></summary>
<param><c>x</c> 是新的 x 坐标。</param>
<param><c>y</c> 是新的 y 坐标。</param>
</member>

<member name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
<summary>此方法通过给定的 x 和 y 偏移量更改点的位置。
<example>例如：
<code>
Point p = new Point(3,5);
p.Translate(-1,3);
</code>
结果使 <c>p</c> 的值为 (2,8)。
</example>
<see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/></summary>
<param><c>x</c> 是相对 x 偏移量。</param>
<param><c>y</c> 是相对 y 偏移量。</param>
</member>

<member name="M:Graphics.Point.Equals(System.Object)">
<summary>此方法确定两个 Points 是否具有的
相同
位置。</summary>
<param><c>obj</c> 是要与当前
对象进行比较的对象。</param>
<returns>如果 Points 具有相同的位置并且它们
具有
完全相同的类型；否则为 false。</returns>
<seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>

<member name="M:Graphics.Point.ToString">
<summary>以字符串形式报告点的位置。</summary>
<returns>一个表示点位置的字符串，形式为
(x,y),
不包含任何前导、尾随或嵌入
空白字符。</returns>
</member>

<member name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"><summary>此运算符确定两个 Points 是否具有相同的位置。</summary><param><c>p1</c> 是要比较的第一个 Point。</param><param><c>p2</c> 是要比较的第二个 Point。</param><returns>如果 Points 具有相同的位置并且它们具有完全相同的类型；否则为 false。</returns><seealso cref="M:Graphics.Point.Equals(System.Object)"/><seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/></member>
<member name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"><summary>此运算符确定两个 Points 是否具有相同的位置。</summary><param><c>p1</c> 是要比较的第一个 Point。</param><param><c>p2</c> 是要比较的第二个 Point。</param><returns>如果 Points 不具有相同的位置并且类型完全相同；否则为 false。</returns><seealso cref="M:Graphics.Point.Equals(System.Object)"/><seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/></member>
<member name="M:Graphics.Point.Main"><summary>这是 Point 类测试程序的入口点。<para>此程序测试每个方法和运算符，旨在在对 Point 类进行任何非平凡维护后运行。</para></summary></member>
<member name="P:Graphics.Point.X"><value>属性 <c>X</c> 表示点的 x 坐标。</value></member>
<member name="P:Graphics.Point.Y"><value>属性 <c>Y</c> 表示点的 y 坐标。</value></member></members></doc>

End of informative text.
