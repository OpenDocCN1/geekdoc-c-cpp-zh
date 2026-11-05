# C# 语言规范 - ECMA-334，第7版，2023年12月

## 前言

本规范取代 ECMA-334:2022。与上一版相比，更改包括增加了以下内容：

- 二进制整数字面量
- 数值字面量中的嵌入数字分隔符
- 二进制和十六进制整数字面量中的前导数字分隔符
- `out` 变量
- 弃元
- 元组类型
- 模式匹配
- `ref` 局部变量和返回、条件 `ref` 表达式、扩展方法中带 `this` 的 `ref`，以及 `ref` 局部变量的重新赋值
- 本地函数
- 更多表达式体成员
- `throw` 表达式
- 泛化的 `async` 返回类型
- `async` `Main` 方法
- `default` 字面量表达式
- 非尾随命名实参
- `private` `protected` 访问修饰符
- `in` 参数修饰符
- `readonly` 结构
- `ref` 结构
- 无需固定的可移动固定缓冲区索引
- `stackalloc` 数组上的初始化器
- 基于模式的 `fixed` 语句
- `System.Delegate` 和 `System.Enum` 作为 `class_type` 约束。
- 附加泛型约束
- 允许表达式变量出现在更多位置
- 将特性附加到自动实现属性的后备字段
- 减少重载解析的歧义

## 引言

本规范基于惠普、英特尔和微软提交的一份材料，该材料描述了一种称为 C# 的语言，该语言在微软内部开发。该语言的主要发明者是 Anders Hejlsberg、Scott Wiltamuth 和 Peter Golde。微软于 2000 年 7 月发布了 C# 的第一个广泛分发的实现，作为其 .NET Framework 计划的一部分。

Ecma 技术委员会 39（TC39）[后更名为 TC49] 第 2 任务组（TG2）成立于 2000 年 9 月，旨在制定 C# 标准。当时还成立了另一个任务组 TG3，旨在为称为公共语言基础设施（CLI）的库和执行环境制定标准。（CLI 基于 .NET Framework 的子集。）尽管微软的 C# 实现依赖 CLI 提供库和运行时支持，但其他 C# 实现不必如此，前提是它们支持一种替代方式来获得本 C# 标准所需的最低 CLI 功能（见附录 C）。

随着 C# 定义的发展，其设计中使用的目标如下：

- C# 旨在成为一种简单、现代、通用、面向对象的编程语言。
- 该语言及其实现应支持软件工程原则，例如强类型检查、数组边界检查、检测使用未初始化变量的尝试以及自动垃圾回收。软件的健壮性、持久性和程序员生产力很重要。
- 该语言旨在用于开发适合在分布式环境中部署的软件组件。
- 源代码可移植性非常重要，程序员可移植性也同样重要，尤其是对于已经熟悉 C 和 C++ 的程序员。
- 对国际化的支持非常重要。
- C# 旨在适合为托管系统和嵌入式系统编写应用程序，范围从使用复杂操作系统的超大型系统到具有专用功能的超小型系统。
- 尽管 C# 应用程序旨在在内存和处理能力需求方面经济节约，但该语言并不打算在性能和大小上与 C 或汇编语言直接竞争。

名称 C# 读作“C Sharp”。

名称 C# 写作拉丁大写字母 C (U+0043) 后跟数字符号 # (U+0023)。

# 2. 规范性引用文件

下列规范性文件包含的条款，通过在本规范中的引用而构成本规范的条款。对于注日期的引用，这些出版物的后续修订或修订版不适用。但是，鼓励基于本规范的协议的各方调查应用下列规范性文件最新版本的可能性。对于不注日期的引用，适用所引用规范性文件的最新版本。ISO 和 IEC 成员维护当前有效规范的登记册。

- ISO/IEC 23271:2012，*公共语言基础设施（CLI），第 IV 部分：基类库（BCL）、扩展数值库和扩展数组库。*
- ISO 80000-2，*量和单位 — 第 2 部分：自然科学和技术中使用的数学符号和标志。*
- ISO/IEC 2382，*信息技术 — 词汇。*
- ISO/IEC 60559:2020，*信息技术 — 微处理器系统 — 浮点运算*
- Unicode 联盟。Unicode 标准，https://www.unicode.org/standard/standard.html

# 3. 术语和定义

就本规范而言，下列定义适用。其他术语在它们以*斜体*字体出现处或语法规则左侧定义。本规范中明确定义的术语不应被假定为隐含地指代其他地方定义的类似术语。本规范未定义的术语应按照 ISO/IEC 2382.1 解释。本规范未定义的数学符号应按照 ISO 80000-2 解释。

- **应用程序** – 具有入口点的程序集
- **应用程序域** – 通过充当应用程序状态的容器来实现应用程序隔离的实体
- **实参** – 在方法或实例构造函数调用表达式中由括号括起的逗号分隔列表中的表达式，或在元素访问表达式中由方括号括起的表达式
- **程序集** – 编译器作为程序编译结果输出的一个或多个文件
- **行为** – 外部表现或动作
- **行为，实现定义** – 未指定的行为，其中每个实现记录如何做出选择
- **行为，未定义** – 在使用不可移植或错误的构造或错误数据时，本规范对其不施加任何要求的行为
- **行为，未指定** – 本规范提供两种或更多可能性，并且对在任何实例中选择哪一种不施加进一步要求的行为
- **字符**（当不带限定符使用时）
  - 在非 Unicode 编码的上下文中，字符在该编码中的含义；或
  - 在字符字面量或 char 类型的值的上下文中，范围 U+0000 到 U+FFFF（包括代理项码点）内的 Unicode 码点，即 UTF-16 代码单元；或
  - 否则，是一个 Unicode 码点
- **类库** – 可由其他程序集使用的程序集
- **编译单元** – 输入到编译器的 Unicode 字符的有序序列
- **诊断消息** – 属于实现的输出消息中由实现定义的子集的消息
- **错误，编译时** – 在程序翻译期间报告的错误
- **异常** – 在程序执行期间报告的异常条件
- **实现** – 特定软件集（在特定控制选项下在特定翻译环境中运行），它执行程序翻译并支持在特定执行环境中执行方法




- **模块** – 由编译器生成的程序集内容。某些实现可能提供生成包含多个模块的程序集的功能。此类情况下的行为不在本规范的范围之内。
- **命名空间** – 将相关程序元素分组在一起的逻辑组织系统。
- **参数** – 在方法、实例构造函数、运算符或索引器定义中声明的变量，在进入该函数成员时获取一个值。
- **程序** – 提交给编译器并由执行环境运行或执行的一个或多个编译单元。
- **不安全代码** – 允许执行此类底层操作的代码，例如声明和操作指针、在指针与整型之间进行转换，以及获取变量的地址。
- **警告，编译时** – 程序翻译期间报告的信息性消息，旨在标识程序元素潜在可疑的用法。

# 4. 总体说明

**此文本为信息性内容。**

本规范旨在供实现者、学者和应用程序程序员使用。因此，其中包含了大量解释性材料，严格来说，这些材料在正式的语言规范中并非必需。

本规范分为以下几个部分：前置部分；语言语法、约束和语义；以及附录。

提供了示例以说明所述结构可能的形式。引用用于指代相关条款。注释用于向实现者或程序员提供建议或指导。附录提供附加信息并汇总本规范中包含的信息。

**信息性文本结束。**

信息性文本以下列方式标识：

1. 以**“此条款/文本为信息性内容”**和**“信息性文本结束”**为界的整节或部分条款或附录。
2. *示例：* 以下示例 ... 代码片段，可能附带一些叙述 ... *示例结束* 对于单段示例，*示例：* 和 *示例结束* 标记位于同一段落中。如果示例跨多个段落，则*示例结束*标记应单独成段。
3. *注释：* 叙述 ... *注释结束* 对于单段注释，*注释：* 和 *注释结束* 标记位于同一段落中。如果注释跨多个段落，则*注释结束*标记应单独成段。

所有未标记为信息性的文本均为规范性文本。

# 5. 符合性

符合性对以下受众具有意义：

- 设计、实现或维护 C# 实现的人员。
- 希望采购 C# 实现的政府或商业实体。
- 希望提供 C# 符合性测试套件的测试组织。
- 希望将代码从一种 C# 实现移植到另一种 C# 实现的程序员。
- 希望教授标准 C# 的教育工作者。
- 希望撰写关于标准 C# 的著作的作者。

因此，符合性最为重要，本规范的大部分内容旨在规定使 C# 实现和 C# 程序符合规范的特性。

本规范中规定要求的文本被视为*规范性*文本。本规范中的所有其他文本均为*信息性*文本；也就是说，仅供参考。除非另有说明，所有文本均为规范性文本。规范性文本进一步分为*必需*和*条件性*类别。*条件性规范*文本规定了某个可选功能的特性及其要求。但是，如果提供了该功能，其语法和语义必须完全符合规定。

未定义行为在本规范中仅通过“未定义行为”字样表示。

*严格符合的程序*只能使用本规范中规定为必需的语言特性。（这意味着严格符合的程序不能使用任何条件性规范特性。）它不得产生依赖于任何未指定、未定义或实现定义行为的输出。

C# 的*符合实现*应接受任何严格符合的程序。

C# 的*符合实现*应提供并支持本规范中规范性（而非条件性规范）部分所描述的所有类型、值、对象、属性、方法和程序语法与语义。

C# 的*符合实现*应按照 Unicode 标准解释字符。符合实现应接受以 UTF-8 编码形式编码的编译单元。

C# 的*符合实现*不得成功翻译包含 #error 预处理指令的源代码，除非该指令属于条件编译所跳过的组的一部分。

C# 的*符合实现*应在源程序违反任何语法规则或任何否定性要求（定义为“不得”或“错误”或“警告”要求）时产生至少一条诊断消息，除非该要求标记有“无需诊断”字样。

C# 的*符合实现*可以提供超出本规范所述范围的附加类型、值、对象、属性和方法，前提是它们不改变任何严格符合程序的行为。符合实现必须诊断那些使用根据本规范为格式错误的扩展的程序。然而，在完成诊断后，它们可以编译并执行此类程序。（拥有扩展的能力意味着符合实现除了本规范中明确保留的标识符外，不保留任何标识符。）

C# 的符合实现应附带一份文档，定义所有实现定义的特征以及所有扩展。

C# 的符合实现应支持附录 C 中记载的类库。该库通过引用包含在本规范中。

符合程序是指符合实现可接受的程序。（此类程序允许包含扩展或条件性规范特性。）

# 6. 词法结构

### 6.1 程序

C# 程序由一个或多个源文件组成，正式称为编译单元（§14.2）。尽管编译单元可能与文件系统中的文件一一对应，但并非必须如此。

从概念上讲，程序通过三个步骤进行编译：

1. 转换，将文件从特定的字符集和编码方案转换为 Unicode 字符序列。
2. 词法分析，将 Unicode 输入字符流转换为标记流。
3. 语法分析，将标记流转换为可执行代码。

符合实现应接受以 UTF-8 编码形式（如 Unicode 标准所定义）编码的 Unicode 编译单元，并将其转换为 Unicode 字符序列。实现可以选择接受和转换其他字符编码方案（如 UTF-16、UTF-32 或非 Unicode 字符映射）。

> 注释：Unicode 空字符（U+0000）的处理是实现特定的。强烈建议开发人员避免在源代码中使用此字符，以兼顾可移植性和可读性。当在字符或字符串字面量中需要该字符时，可以使用转义序列 \0 或 \u0000 代替。注释结束

> 注释：本规范不定义如何将使用非 Unicode 字符表示的文件转换为 Unicode 字符序列。然而，在此类转换过程中，建议将其他字符集中的通常换行字符（或序列）转换为由 Unicode 回车符（U+000D）后跟 Unicode 换行符（U+000A）组成的双字符序列。在大多数情况下，此转换不会产生可见影响；但是，它会影响原义字符串字面量标记（§6.4.5.6）的解释。此建议的目的是允许原义字符串字面量在其编译单元在支持不同非 Unicode 字符集的系统之间移动时产生相同的字符序列，特别是那些使用不同换行字符序列的系统。注释结束

### 6.2 语法

#### 6.2.1 总则

本规范使用两种文法来呈现 C# 编程语言的语法。词法文法（§6.2.3）定义 Unicode 字符如何组合成行终止符、空白、注释、标记和预处理指令。语法文法（§6.2.4）定义词法文法产生的标记如何组合成 C# 程序。




示例结束

如果某个标记序列在上下文中可以被解析为以 *类型实参列表*（§8.4.2）结尾的 *简单名称*（§12.8.4）、*成员访问*（§12.8.7）或 *指针成员访问*（§23.6.3），则需要检查紧跟闭合 > 标记之后的标记，看它是否是：

-   属于 ( ) ] } : ; , . ? == != | ^ && || & [ ; 之一；或
-   属于关系运算符 < > <= >= is as 之一；或
-   出现在查询表达式中的上下文查询关键字；或
-   在某些上下文中，*标识符* 被视为消歧标记。这些上下文是指：被消歧的标记序列紧接在关键字 is、case 或 out 之一的前面，或者在解析元组字面量的第一个元素时出现（此时该标记序列前面是 ( 或 :，且标识符后面跟有 ,），或者在解析元组字面量的后续元素时出现。

如果后续标记位于此列表中，或是处于此类上下文中的标识符，则 *类型实参列表* 会保留为 *简单名称*、*成员访问* 或 *指针成员访问* 的一部分，并且该标记序列的任何其他可能解析都将被丢弃。否则，即使该标记序列没有其他可能的解析，*类型实参列表* 也不会被视为 *简单名称*、*成员访问* 或 *指针成员访问* 的一部分。（这些规则不适用于在 *命名空间或类型名称*（§7.8）中解析 *类型实参列表* 的情况。）

> 注意：这些规则不适用于在 *命名空间或类型名称*（§7.8）中解析 *类型实参列表* 的情况。注意结束

示例：以下语句：

```
    F(G<A, B>(7));
```

根据此规则，这将被解释为对 F 的一次调用，调用带一个参数，该参数是对泛型方法 G 的一次调用，其中 G 有两个类型实参和一个常规实参。以下语句：

```
    F(G<A, B>7);
    F(G<A, B>>7);
```

将各自被解释为对 F 的调用，且带有两个参数。以下语句：

```
    x = F<A> + y;
```

将被解释为小于运算符、大于运算符和一元加运算符，就好像该语句写作 x = (F < A) > (+y) 一样，而不是将其解释为带有 *类型实参列表* 后跟二元加运算符的 *简单名称*。在以下语句：

```
    x = y is C<T> && z;
```

中，由于 *类型实参列表* 后存在消歧标记 &&，标记 C<T> 被解释为带有 *类型实参列表* 的 *命名空间或类型名称*。

表达式 (A < B, C > D) 是一个含有两个元素的元组，每个元素都是一个比较表达式。

表达式 (A<B,C> D, E) 是一个含有两个元素的元组，其中第一个元素是声明表达式。

调用 M(A < B, C > D, E) 有三个实参。

调用 M(out A<B,C> D, E) 有两个实参，第一个实参是一个 out 声明。

表达式 e is A<B> C 使用的是声明模式。

case 标签 case A<B> C: 使用的是声明模式。

*示例结束*

关系表达式（§12.12.1）可以具有“relational_expression is type”或“relational_expression is constant_pattern”的形式，二者都可能是限定标识符的有效解析。在这种情况下，会尝试将其作为类型（§7.8.1）进行绑定；然而，如果该尝试失败，则将其作为表达式绑定，并且结果必须是常量。

## 6.3 词法分析

### 6.3.1 概述

为方便起见，词法文法定义并引用了以下命名的词法标记：

```
DEFAULT   : 'default' ;
NULL      : 'null' ;
TRUE      : 'true' ;
FALSE     : 'false' ;
ASTERISK  : '*' ;
SLASH     : '/' ;
```

尽管这些是词法规则，但这些名称全部使用大写字母拼写，以便与普通词法规则名称区分开来。

*注意：这些便利规则是对通常不为由字面量字符串定义的标记提供显式标记名称这一惯例的例外。注意结束*

*输入* 产生式定义了 C# 编译单元的词法结构。

```
input
    : input_section?
    ;

input_section
    : input_section_part+
    ;

input_section_part
    : input_element* New_Line
    | PP_Directive
    ;

input_element
    : Whitespace
    | Comment
    | token
    ;
```

*注意：上述文法由 ANTLR 解析规则描述，它定义的是 C# 编译单元的词法结构，而非词法标记。注意结束*

五个基本元素构成了 C# 编译单元的词法结构：行终止符（§6.3.2）、空白（§6.3.4）、注释（§6.3.3）、标记（§6.4）和预处理指令（§6.5）。在这些基本元素中，只有标记在 C# 程序的语法文法（§6.2.4）中是重要的。

C# 编译单元的词法处理包括将文件缩减为标记序列，该序列成为语法分析的输入。行终止符、空白和注释可用于分隔标记，预处理指令可能导致编译单元的某些部分被跳过，但除此之外，这些词法元素对 C# 程序的语法结构没有影响。

当多个词法文法产生式与编译单元中的某个字符序列匹配时，词法处理总是形成最长的可能词法元素。

示例：字符序列 // 被处理为单行注释的开始，因为该词法元素比单个 / 标记更长。示例结束

某些标记由一组词法规则定义：一条主规则和一条或多条子规则。后者在文法中用 fragment 标记，以指示该规则定义了另一个标记的一部分。片段规则在词法规则的自上而下排序中不被考虑。

注意：在 ANTLR 中，fragment 是一个关键字，其行为与本处定义的行为相同。注意结束

### 6.3.2 行终止符

行终止符将 C# 编译单元的字符划分为行。

```
New_Line
  : New_Line_Character
  | '\u000D\u000A'  // carriage return, line feed
  ;
```

为了与添加文件结束标记的源代码编辑工具兼容，并使编译单元能够被视为一系列正确终止的行，对 C# 程序中的每个编译单元按顺序应用以下变换：

- 如果编译单元的最后一个字符是 Control-Z 字符（U+001A），则删除该字符。
- 如果编译单元非空，且最后一个字符不是回车符（U+000D）、换行符（U+000A）、下一行字符（U+0085）、行分隔符（U+2028）或段落分隔符（U+2029），则在编译单元末尾添加一个回车符（U+000D）。

注意：额外的回车符允许程序以没有终止换行符的 PP_Directive（§6.5）结束。注意结束

### 6.3.3 注释

支持两种形式的注释：分隔注释和单行注释。

分隔注释以字符 /* 开头，以字符 */ 结束。分隔注释可以占据一行的一部分、整行或多行。

示例：以下示例：

```
/* Hello, world program
   This program writes "hello, world" to the console
*/
class Hello
{
    static void Main()
    {
        System.Console.WriteLine("hello, world");
    }
}
```

包含一个分隔注释。

示例结束

单行注释以字符 // 开头，并延伸到该行末尾。

示例：以下示例：

```
// Hello, world program
// This program writes "hello, world" to the console
//
//
class Hello // any name will do for this class
{
    static void Main() // this method must be named "Main"
    {
        System.Console.WriteLine("hello, world");
    }
}
```

展示了多个单行注释。

示例结束

```
Comment
  : Single_Line_Comment
  | Delimited_Comment
  ;

fragment Single_Line_Comment
  : '//' Input_Character*
  ;

fragment Input_Character
  // anything but New_Line_Character
  : ~('\u000D' | '\u000A' | '\u0085' | '\u2028' | '\u2029')
  ;

fragment New_Line_Character
  : '\u000D' // carriage return
  | '\u000A' // line feed
  | '\u0085' // next line
  | '\u2028' // line separator
  | '\u2029' // paragraph separator
  ;

fragment Delimited_Comment
  : '/*' Delimited_Comment_Section* ASTERISK+ '/'
  ;

fragment Delimited_Comment_Section
  : SLASH
  | ASTERISK* Not_Slash_Or_Asterisk
  ;

fragment Not_Slash_Or_Asterisk
  : ~('/' | '*')  // Any except SLASH or ASTERISK
  ;
```




注释不嵌套。在单行注释中，字符序列 /* 和 */ 没有特殊含义，而在定界注释中，字符序列 // 和 /* 没有特殊含义。

注释在字符和字符串字面量中不被处理。

Note: 这些规则必须谨慎解释。例如，在下面的示例中，以 A 之前开始的定界注释在 B 和 C() 之间结束。原因是

// B * / C();

实际上并不是单行注释，因为 // 在定界注释中没有特殊含义，因此 /* 在该行中具有其通常的特殊含义。

同样，以 D 之前开始的定界注释在 E 之前结束。原因是 "D * / " 实际上并不是字符串字面量，因为初始的双引号字符出现在定界注释内部。

/* 和 */ 在单行注释中没有特殊含义的一个有用结果是，可以通过在每一行的开头放置 // 来注释掉一段源代码行。通常，不能在这些行之前放置 /* 并在之后放置 */，因为这并不能正确地封装块中的定界注释，并且通常可能会完全改变此类定界注释的结构。

示例代码：

```
static void Main()
{
    /* A
    // B */ C();
    Console.WriteLine(/* "D */ "E");
}
```

注释结束

具有特定格式的 Single_Line_Comments 和 Delimited_Comments 可用作文档注释，如 §D 中所述。

### 6.3.4 空白

空白定义为具有 Unicode 类 Zs 的任何字符（包括空格字符），以及水平制表符、垂直制表符和换页符。

```
Whitespace
  : [\p{Zs}] // any character with Unicode class Zs
  | '\u0009' // horizontal tab
  | '\u000B' // vertical tab
  | '\u000C' // form feed
  ;
```

## 6.4 标记

### 6.4.1 通用

有几种类型的标记：标识符、关键字、字面量、运算符和标点符号。空白和注释不是标记，尽管它们充当标记的分隔符。

```
token
  : identifier
  | keyword
```

```
| Integer_Literal
| Real_Literal
| Character_Literal
| String_Literal
| operator_or_punctuator
;
```

Note: 这是 ANTLR 解析器规则，它并不定义词法标记，而是标记种类的集合。注释结束

### 6.4.2 Unicode 字符转义序列

Unicode 转义序列表示一个 Unicode 代码点。Unicode 转义序列在标识符 (§6.4.3)、字符字面量 (§6.4.5.5)、常规字符串字面量 (§6.4.5.6) 和插值常规字符串表达式 (§12.8.3) 中被处理。Unicode 转义序列在其他任何位置都不被处理（例如，形成运算符、标点符号或关键字）。

```
fragment Unicode_Escape_Sequence
: '\u' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
| '\U' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
Hex_Digit Hex_Digit Hex_Digit Hex_Digit
;
```

Unicode 字符转义序列表示由 "\u" 或 "\U" 字符后跟的十六进制数字形成的单个 Unicode 代码点。由于 C# 在字符和字符串值中使用 16 位编码的 Unicode 代码点，范围为 U+10000 到 U+10FFFF 的 Unicode 代码点使用两个 Unicode 代理代码单元表示。字符字面量中不允许使用大于 U+FFFF 的 Unicode 代码点。大于 U+10FFFF 的 Unicode 代码点无效且不受支持。

不执行多次转换。例如，字符串字面量 "\u005Cu005C" 等同于 "\u005C"，而不是 "\"。

Note: Unicode 值 \u005C 是字符 "\"。注释结束

Example: 示例

```
class Class1
{
    static void Test(bool \u0066)
    {
        char c = '\u0066';
        if (\u0066)
        {
            System.Console.WriteLine(c.ToString());
        }
    }
}
```

显示了 \u0066 的几种用法，它是字母 "f" 的转义序列。该程序等价于

```
class Class1
{
    static void Test(bool f)
    {
        char c = 'f';
        if (f)
        {
            System.Console.WriteLine(c.ToString());
        }
    }
}
```

*示例结束*

### 6.4.3 标识符

本小节中给出的标识符规则与 Unicode 标准附录 15 中推荐的规则完全对应，只是下划线允许作为初始字符（如 C 编程语言传统），Unicode 转义序列允许在标识符中使用，并且允许使用 "@" 字符作为前缀以使关键字可作为标识符使用。

```
identifier
: Simple_Identifier
| contextual_keyword
;

Simple_Identifier
: Available_Identifier
| Escaped_Identifier
;

fragment Available_Identifier
// excluding keywords or contextual keywords, see note below
: Basic_Identifier
;

fragment Escaped_Identifier
// Includes keywords and contextual keywords prefixed by '@'.
// See note below.
: '@' Basic_Identifier
;

fragment Basic_Identifier
: Identifier_Start_Character Identifier_Part_Character*
;

fragment Identifier_Start_Character
: Letter_Character
| Underscore_Character
;

fragment Underscore_Character
: '_' // underscore
| '\u005f' // Unicode_Escape_Sequence for underscore
;

fragment Identifier_Part_Character
: Letter_Character
| Decimal_Digit_Character
| Connecting_Character
| Combining_Character
| Formatting_Character
;
```

```
fragment Letter_Character
// Category Letter, all subcategories; category Number, subcategory letter.
// [\p{L}]\p{Nl}]
// Only escapes for categories L & Nl allowed. See note below.
| Unicode_Escape_Sequence
;
```

```
fragment Combining_Character
// Category Mark, subcategories non-spacing and spacing combining.
// [\p{Mn}]\p{Mc}]
// Only escapes for categories Mn & Mc allowed. See note below.
| Unicode_Escape_Sequence
;
```

```
fragment Decimal_Digit_Character
// Category Number, subcategory decimal digit.
// [\p{Nd}]
// Only escapes for category Nd allowed. See note below.
| Unicode_Escape_Sequence
;
```

```
fragment Connecting_Character
// Category Punctuation, subcategory connector.
// [\p{Pc}]
// Only escapes for category Pc allowed. See note below.
| Unicode_Escape_Sequence
;
```

```
fragment Formatting_Character
// Category Other, subcategory format.
// [\p{Cf}]
// Only escapes for categories Cf allowed, see note below.
| Unicode_Escape_Sequence
;
```

Note:

- 有关上面提到的 Unicode 字符类的信息，请参阅 *Unicode 标准*。
- 片段 *Available_Identifier* 要求排除关键字和上下文关键字。如果本规范中的语法用 ANTLR 处理，则该排除由 ANTLR 的语义自动处理：
  - 关键字和上下文关键字在语法中作为字面字符串出现。
  - ANTLR 从这些字面字符串创建隐式词法标记规则。
  - ANTLR 在语法中的显式词法规则之前考虑这些隐式规则。
  - 因此片段 *Available_Identifier* 不会匹配关键字或上下文关键字，因为这些的词法规则在其之前。
- 片段 *Escaped_Identifier* 包含转义的关键字和上下文关键字，因为它们是 @ 开头的更长标记的一部分，并且词法处理始终形成最长的可能词法元素 (§6.3.1)。
- 实现如何强制执行允许的 *Unicode_Escape_Sequence* 值限制是实现问题。

注释结束

Example: 有效标识符的示例是 identifier1、_identifier2 和 @if。示例结束

符合规范的程序中的标识符应采用 Unicode 标准附录 15 中定义的 Unicode 正规化形式 C 定义的规范格式。遇到不在正规化形式 C 中的标识符时的行为是实现定义的；然而，不要求诊断。

前缀 "@" 允许将关键字用作标识符，这在与其他编程语言接口时很有用。字符 @ 实际上不是标识符的一部分，因此标识符在其他语言中可能被视为普通标识符，而没有前缀。带有 @ 前缀的标识符称为逐字标识符。

Note: 将 @ 前缀用于非关键字的标识符是允许的，但作为风格问题强烈不鼓励。注释结束

Example: 示例：

```
class @class
{
    public static void @static(bool @bool)
    {
        if (@bool)
        {
            System.Console.WriteLine("true");
        }
        else
        {
            System.Console.WriteLine("false");
        }
    }
}

class Class1
{
    static void M()
    {
        c1\u0061ss.st\u0061tic(true);
    }
}
```

定义了一个名为 "class" 的类，其中有一个名为 "static" 的静态方法，该方法接受一个名为 "bool" 的参数。请注意，由于 Unicode 转义不允许在关键字中使用，标记 "c1\u0061ss" 是一个标识符，并且与 "@class" 是同一个标识符。

示例结束

如果在应用以下转换后，两个标识符相同，则认为它们相同，按顺序如下：

- 如果使用，则删除前缀 "@"。
- 每个 *Unicode_Escape_Sequence* 转换为其对应的 Unicode 字符。
- 删除任何 *Formatting_Characters*。



名为 __ 的标识符的语义取决于它出现的上下文：

-   它可以表示一个命名的程序元素，例如变量、类或方法，或者
-   它可以表示一个弃元（§9.2.9.1）。

包含两个连续下划线字符（U+005F）的标识符保留供实现使用；但是，如果定义了此类标识符，则不要求进行诊断。

> 注：例如，实现可能提供以两个下划线开头的扩展关键字。结束注

### 6.4.4 关键字

关键字是一种类似标识符的字符序列，它是保留的，除非以 @ 字符作为前缀，否则不能用作标识符。

```
keyword
  : 'abstract' | 'as' | 'base' | 'bool' | 'break'
  | 'byte' | 'case' | 'catch' | 'char' | 'checked'
  | 'class' | 'const' | 'continue' | 'decimal' | DEFAULT
  | 'delegate' | 'do' | 'double' | 'else' | 'enum'
  | 'event' | 'explicit' | 'extern' | FALSE | 'finally'
  | 'fixed' | 'float' | 'for' | 'foreach' | 'goto'
  | 'if' | 'implicit' | 'in' | 'int' | 'interface'
  | 'internal' | 'is' | 'lock' | 'long' | 'namespace'
  | 'new' | NULL | 'object' | 'operator' | 'out'
  | 'override' | 'params' | 'private' | 'protected' | 'public'
  | 'readonly' | 'ref' | 'return' | 'sbyte' | 'sealed'
  | 'short' | 'sizeof' | 'stackalloc' | 'static' | 'string'
  | 'struct' | 'switch' | 'this' | 'throw' | TRUE
  | 'try' | 'typeof' | 'uint' | 'ulong' | 'unchecked'
  | 'unsafe' | 'ushort' | 'using' | 'virtual' | 'void'
  | 'volatile' | 'while'
  ;
```

上下文关键字是一种类似标识符的字符序列，它在某些上下文中具有特殊含义，但不是保留的，并且在这些上下文之外以及以 @ 字符作为前缀时，可以用作标识符。

```
contextual_keyword
  : 'add' | 'alias' | 'ascending' | 'async' | 'await'
  | 'by' | 'descending' | 'dynamic' | 'equals' | 'from'
  | 'get' | 'global' | 'group' | 'into' | 'join'
  | 'let' | 'nameof' | 'on' | 'orderby' | 'partial'
  | 'remove' | 'select' | 'set' | 'unmanaged' | 'value'
  | 'var' | 'when' | 'where' | 'yield'
  ;
```

> 注：keyword 和 contextual_keyword 规则是解析器规则，因为它们不引入新的标记种类。所有关键字和上下文关键字都由隐式词法规则定义，因为它们在语法中以字面量字符串出现（§6.2.3）。结束注

在大多数情况下，上下文关键字的语法位置使其永远不会与普通标识符用法混淆。例如，在属性声明中，get 和 set 标识符具有特殊含义（§15.7.3）。在这些位置中，绝不允许使用 get 或 set 以外的标识符，因此这种用法不会与将这些词用作标识符的用法冲突。

在某些情况下，语法不足以区分上下文关键字用法与标识符。在所有此类情况下，将规定如何在两者之间消除歧义。例如，隐式类型局部变量声明（§13.6.2）中的上下文关键字 var 可能与名为 var 的已声明类型冲突，在这种情况下，声明的名称优先于将该标识符用作上下文关键字。

此类消除歧义的另一个示例是上下文关键字 await（§12.9.8.1），它仅在声明为 async 的方法内部才被视为关键字，但在其他地方可以用作标识符。

与关键字一样，上下文关键字可以通过在前面加上 @ 字符来用作普通标识符。

> 注：当用作上下文关键字时，这些标识符不能包含 Unicode_Escape_Sequences。结束注

### 6.4.5 字面量

### 6.4.5.1 概述

字面量（§12.8.2）是值的源代码表示形式。

```
literal
: boolean_literal
| Integer_Literal
| Real_Literal
| Character_Literal
| String_Literal
| null_literal
;
```

> 注：literal 是解析器规则，因为它对其他标记种类进行分组，并且不引入新的标记种类。结束注

### 6.4.5.2 布尔字面量

有两个布尔字面量值：true 和 false。

```
boolean_literal
: TRUE
| FALSE
;
```

> 注：boolean_literal 是解析器规则，因为它对其他标记种类进行分组，并且不引入新的标记种类。结束注

boolean_literal 的类型是 bool。

### 6.4.5.3 整数字面量

整数字面量用于写入 int、uint、long 和 ulong 类型的值。整数字面量有三种可能的形式：十进制、十六进制和二进制。

```
Integer_Literal
: Decimal_Integer_Literal
| Hexadecimal_Integer_Literal
| Binary_Integer_Literal
;
```

```
fragment Decimal_Integer_Literal
: Decimal_Digit Decorated_Decimal_Digit* Integer_Type_Suffix?
;
```

```
fragment Decorated_Decimal_Digit
: '_' * Decimal_Digit
;
```

```
fragment Decimal_Digit
: '0'..'9'
;
```

```
fragment Integer_Type_Suffix
: 'U' | 'u' | 'L' | 'l' |
'UL' | 'UL' | 'uL' | 'ul' | 'LU' | 'Lu' | 'LU' | 'lu'
;
```

```
fragment Hexadecimal_Integer_Literal
: ('0x' | '0X') Decorated_Hex_Digit+ Integer_Type_Suffix?
;
```

```
fragment Decorated_Hex_Digit
: '_' * Hex_Digit
;
```

```
fragment Hex_Digit
: '0'..'9' | 'A'..'F' | 'a'..'f'
;
```

```
fragment Binary_Integer_Literal
: ('0b' | '0B') Decorated_Binary_Digit+ Integer_Type_Suffix?
;
```

```
fragment Decorated_Binary_Digit
: '_' * Binary_Digit
;
```

```
fragment Binary_Digit
: '0' | '1'
;
```

整数字面量的类型按如下方式确定：

-   如果字面量没有后缀，则其类型为这些类型中能够表示其值的第一个类型：int、uint、long、ulong。
-   如果字面量带有 U 或 u 后缀，则其类型为这些类型中能够表示其值的第一个类型：uint、ulong。
-   如果字面量带有 L 或 l 后缀，则其类型为这些类型中能够表示其值的第一个类型：long、ulong。
-   如果字面量带有 UL、UL、uL、ul、LU、Lu、LU 或 lu 后缀，则其类型为 ulong。

如果整数字面量表示的值超出 ulong 类型的范围，则发生编译时错误。

> 注：就风格而言，建议在写入 long 类型的字面量时使用 “L” 而不是 “l”，因为字母 “l” 很容易与数字 “1” 混淆。结束注

为了允许将尽可能小的 int 和 long 值写成整数字面量，存在以下两条规则：

-   当表示值 2147483648（2³¹）且不带 Integer_Type_Suffix 的 Integer_Literal 作为紧接在一元减号运算符标记（§12.9.3）之后的标记出现时，结果（两个标记的结果）是类型为 int、值为 −2147483648（−2³¹）的常量。在所有其他情况下，此类 Integer_Literal 的类型为 uint。
-   当表示值 9223372036854775808（2⁶³）且不带 Integer_Type_Suffix 或带有 Integer_Type_Suffix L 或 l 的 Integer_Literal 作为紧接在一元减号运算符标记（§12.9.3）之后的标记出现时，结果（两个标记的结果）是类型为 long、值为 −9223372036854775808（−2⁶³）的常量。在所有其他情况下，此类 Integer_Literal 的类型为 ulong。

示例：

```
123                  // decimal, int
10_543_765Lu         // decimal, ulong
1_2_3__4___5         // decimal, int
123_                 // not a numeric literal; identifier due to leading _
123_                 // invalid; no trailing _ allowed

0xFf                 // hex, int
0X1b_a0_44_fEl       // hex, long
0x1ade_3FE1_29AaUL   // hex, ulong
0x_abc               // hex, int
_0x123               // not a numeric literal; identifier due to leading _
0xabc_               // invalid; no trailing _ allowed

0b101                // binary, int
0B1001_1010u         // binary, uint
0b1111_1111_0000UL   // binary, ulong
0B_111               // binary, int
_0B111               // not a numeric literal; identifier due to leading _
0B111_               // invalid; no trailing _ allowed
```

示例结束

### 6.4.5.4 实数字面量

实数字面量用于写入 float、double 和 decimal 类型的值。

```
Real_Literal
  : Decimal_Digit Decorated_Decimal_Digit* '.'
    Decimal_Digit Decorated_Decimal_Digit* Exponent_Part? Real_Type_Suffix?
  | '.' Decimal_Digit Decorated_Decimal_Digit* Exponent_Part? Real_Type_Suffix?
  | Decimal_Digit Decorated_Decimal_Digit* Exponent_Part Real_Type_Suffix?
  | Decimal_Digit Decorated_Decimal_Digit* Real_Type_Suffix
  ;
```

```
fragment Exponent_Part
  : ('e' | 'E') Sign? Decimal_Digit Decorated_Decimal_Digit*
  ;
```

```
fragment Sign
```



```
: '+' | '-'
;

fragment Real_Type_Suffix
: 'F' | 'f' | 'D' | 'd' | 'M' | 'm'
;
```

如果未指定 Real_Type_Suffix，则 Real_Literal 的类型为 double。否则，Real_Type_Suffix 决定实数字面量的类型，如下所示：

- 后缀为 F 或 f 的实数字面量类型为 float。
  示例：字面量 1f、1.5f、1e10f 和 123.456F 均为 float 类型。示例结束
- 后缀为 D 或 d 的实数字面量类型为 double。
  示例：字面量 1d、1.5d、1e10d 和 123.456D 均为 double 类型。示例结束
- 后缀为 M 或 m 的实数字面量类型为 decimal。
  示例：字面量 1m、1.5m、1e10m 和 123.456M 均为 decimal 类型。示例结束
  该字面量通过取精确值转换为十进制值，并在必要时使用银行家舍入（§8.3.8）舍入到最接近的可表示值。字面量中明显的标度在值被舍入时除外，否则予以保留。
  注释：因此，字面量 2.900m 将被解析为符号为 0、系数为 2900、标度为 3 的十进制数。注释结束

如果指定字面量的大小太大而无法在指示的类型中表示，则会发生编译时错误。

> 注释：特别地，Real_Literal 永不会产生浮点无穷大。然而，非零的 Real_Literal 可能会被舍入为零。注释结束

float 或 double 类型的实数字面量的值是通过使用 IEC 60559 “round to nearest” 模式确定，其中平局时舍入到 “even”（最低有效位为零的值），并且所有数字均被视为有效。

> 注释：在实数字面量中，小数点后始终需要十进制数字。例如，1.3F 是实数字面量，但 1. F 不是。注释结束

```
Example:
1.234_567    // double
.3e5f       // float
2.345E-2_0  // double
15D         // double
19.73M      // decimal
1.F         // parsed as a member access of F due to non-digit after .
1._2F       // invalid; no trailing _ allowed in integer part
1. _234     // parsed as a member access of _234 due to non-digit after .
1._234      // invalid; no trailing _ allowed in fraction
.3e_5F      // invalid; no trailing _ allowed in exponent
.3e5_F      // invalid; no trailing _ allowed in exponent
end example
```

#### 6.4.5.5 字符字面量

字符字面量表示单个字符，由引号中的字符组成，如 'a'。

```
Character_Literal
: '\'' Character '\''
```

```
fragment Character
: Single_Character
| Simple_Escape_Sequence
| Hexadecimal_Escape_Sequence
| Unicode_Escape_Sequence
;
```

```
fragment Single_Character
// anything but ', \, and New_Line_Character
: ~['\\'\u000D\u000A\u0085\u2028\u2029]
;
```

```
fragment Simple_Escape_Sequence
: '\\'' | '\"' | '\\\\' | '\\0' | '\\a' | '\\b' |
  '\\f' | '\\n' | '\\r' | '\\t' | '\\v'
;
```

```
fragment Hexadecimal_Escape_Sequence
: '\\x' Hex_Digit Hex_Digit? Hex_Digit? Hex_Digit?
;
```

注释：在 Character 中跟在反斜杠字符（\）后面的字符必须是以下字符之一：'、"、\、0、a、b、f、n、r、t、u、U、x、v。否则，会发生编译时错误。注释结束

注释：由于 \x 后面十六进制数字的数量可变，使用 \x Hexadecimal_Escape_Sequence 产生式可能导致错误且难以阅读。例如，在代码中：

```
string good = "\x9Good text";
string bad = "\x9Bad text";
```

乍一看，两个字符串的开头字符可能相同（U+0009，一个制表符）。事实上，第二个字符串以 U+9BAD 开头，因为单词 "Bad" 中的三个字母都是有效的十六进制数字。出于风格考虑，建议避免使用 \x，而改用特定的转义序列（本例中为 \t）或固定长度的 \u 转义序列。

注释结束

十六进制转义序列表示单个 Unicode UTF-16 代码单元，其值由 "\x" 后面的十六进制数字形成。

如果字符字面量表示的值大于 U+FFFF，则会发生编译时错误。

字符字面量中的 Unicode 转义序列（§6.4.2）应位于 U+0000 到 U+FFFF 范围内。

简单转义序列表示 Unicode 字符，如下表所述。

| 转义序列 | 字符名称 | Unicode 代码点 |
|---|---|---|
| \' | Single quote | U+0027 |
| \" | Double quote | U+0022 |
| \\ | Backslash | U+005C |
| \0 | Null | U+0000 |
| \a | Alert | U+0007 |
| \b | Backspace | U+0008 |
| \f | Form feed | U+000C |
| \n | New line | U+000A |
| \r | Carriage return | U+000D |
| \t | Horizontal tab | U+0009 |
| \v | Vertical tab | U+000B |

Character_Literal 的类型为 char。

#### 6.4.5.6 字符串字面量

C# 支持两种形式的字符串字面量：常规字符串字面量和逐字字符串字面量。常规字符串字面量由双引号括起的零个或多个字符组成，如 "hello"，可以包含简单转义序列（如 \t 表示制表符），以及十六进制和 Unicode 转义序列。

逐字字符串字面量由 @ 字符后跟双引号字符、零个或多个字符以及结束的双引号字符组成。

示例：一个简单示例是 @"hello"。示例结束

在逐字字符串字面量中，定界符之间的字符按字面解释，唯一的例外是 Quote_Escape_Sequence，它表示一个双引号字符。特别是，简单转义序列以及十六进制和 Unicode 转义序列在逐字字符串字面量中不被处理。逐字字符串字面量可以跨越多行。

```
String_Literal
  : Regular_String_Literal
  | Verbatim_String_Literal
  ;

fragment Regular_String_Literal
  : "" Regular_String_Literal_Character* ""
  ;

fragment Regular_String_Literal_Character
  : Single_Regular_String_Literal_Character
  | Simple_Escape_Sequence
  | Hexadecimal_Escape_Sequence
  | Unicode_Escape_Sequence
  ;

fragment Single_Regular_String_Literal_Character
  // anything but ", \, and New_Line_Character
  : ~["\\\u000D\u000A\u0085\u2028\u2029]
  ;

fragment Verbatim_String_Literal
  : @" Verbatim_String_Literal_Character* ""
  ;

fragment Verbatim_String_Literal_Character
  : Single_Verbatim_String_Literal_Character
  | Quote_Escape_Sequence
  ;
```

```
fragment Single_Verbatim_String_Literal_Character
    : ~["\"]   // anything but quotation mark (U+0022)
    ;

fragment Quote_Escape_Sequence
    : """"
    ;
```

## 示例：示例

```
string a = "Happy birthday, Joel"; // Happy birthday, Joel
string b = @"Happy birthday, Joel"; // Happy birthday, Joel
string c = "hello \t world"; // hello world
string d = @"hello \t world"; // hello \t world
string e = "Joe said \"Hello\" to me"; // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me"; // Joe said "Hello" to me
string g = @"\\server\share\file.txt"; // \\server\share\file.txt
string h = @"\\server\share\file.txt"; // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

显示了各种字符串字面量。最后一个字符串字面量 j 是一个跨越多行的逐字字符串字面量。引号之间的字符，包括换行符等空白字符，均按字面保留，并且每对双引号字符被替换为一个这样的字符。

示例结束

注释：逐字字符串字面量内的任何换行都是结果字符串的一部分。如果应用程序对形成换行的确切字符在语义上相关，则任何在源代码中将换行从一种格式翻译为另一种格式的工具（例如在 “\n” 和 “\r\n” 之间）都会改变应用程序的行为。在这种情况下，开发人员应谨慎。注释结束

注释：由于十六进制转义序列可以有可变的十六进制数字数量，字符串字面量 “\x123” 包含一个十六进制值为 123 的单个字符。要创建包含十六进制值为 12 的字符后跟字符 3 的字符串，可以写 “\x00123” 或 “\x12" + "3” 之一。注释结束

String_Literal 的类型为 string。

每个字符串字面量不一定会产生新的字符串实例。当两个或多个根据字符串相等运算符（§12.12.8）等效的字符串字面量出现在同一程序集中时，这些字符串字面量引用同一个字符串实例。

## 示例：例如，由以下代码产生的输出

```
class Test
{
    static void Main()
    {
        object a = "hello";
        object b = "hello";
        System.Console.WriteLine(a == b);
    }
}
```

为真，因为这两个字面量引用的是同一个字符串实例。

*示例结束*

### 6.4.5.7 空字面量

```
null_literal
  : NULL
  ;
```

*注意：* null_literal 是解析器规则，因为它不会引入新的标记种类。 *注释结束*

一个 null_literal 表示空值。它没有类型，但可以通过空字面量转换（§10.2.7）转换为任何引用类型或可空值类型。

### 6.4.6 运算符和标点符号

有几种类型的运算符和标点符号。运算符用于在表达式中描述涉及一个或多个操作数的操作。

*示例：* 表达式 a + b 使用 + 运算符将两个操作数 a 和 b 相加。 *示例结束*

标点符号用于分组和分隔。

```
operator_or_punctuator
  : '{' | '}' | '[' | ']' | '(' | ')' | '.' | ',' | ':' | ';' | '+' | '-' | ASTERISK | SLASH | '%' | '&' | '|' | '^' | '!' | '~' | '=' | '<' | '>' | '?' | '::' | '++' | '--' | '&&' | '||' | '==' | '!=' | '<=' | '>=' | '??' | ':=' | '+-' | '-+' | '==' | '!=' | '=>' | '&=' | '|=' | '^=' | '<<' | '<<=' | '>>' | '>>=' | '*=' | '/=' | '%=' | '&=' | '|=' | '^=' | '!=' | ...
  ;
```

```
right_shift
  : '>' '>'
  ;
```

```
right_shift_assignment
  : '>' '>='
  ;
```

*注意：* right_shift 和 right_shift_assignment 是解析器规则，因为它们不会引入新的标记种类但表示两个标记的序列。operator_or_punctuator 规则仅用于描述目的，在语法中其他地方未使用。 *注释结束*

right_shift 由两个标记 > 和 > 组成。类似地，right_shift_assignment 由两个标记 > 和 >= 组成。与语法语法中的其他产生式不同，在这些产生式的两个标记之间不允许有任何字符（甚至空白）。这些产生式被特殊处理，以便能够正确处理类型参数列表（§15.2.3）。

*注意：* 在 C# 添加泛型之前，>> 和 >>= 都是单个标记。然而，泛型的语法使用 < 和 > 字符来分隔类型参数和类型参数。经常希望使用嵌套的构造类型，例如 List<Dictionary<string, int>>。而不是要求程序员用空格分隔 > 和 >，这两个 operator_or_punctuator 的定义被更改了。 *注释结束*

## 6.5 预处理指令

### 6.5.1 通用

预处理指令提供有条件地跳过编译单元部分、报告错误和警告条件以及划分源代码不同区域的能力。

*注意：* 术语“预处理指令”仅用于与 C 和 C++ 编程语言保持一致。在 C# 中，没有单独的预处理步骤；预处理指令作为词法分析阶段的一部分进行处理。 *注释结束*

```
PP_Directive
  : PP_Start PP_Kind PP_New_Line
  ;
```

```
fragment PP_Kind
  : PP_Declaration
  | PP_Conditional
  | PP_Line
  | PP_Diagnostic
  | PP_Region
  | PP_Pragma
  ;
```

```
// Only recognised at the beginning of a line
fragment PP_Start
  // See note below.
  : { getCharPositionInLine() == 0 }? PP_Whitespace? '#' PP_Whitespace?
  ;
```

```
fragment PP_Whitespace
  : ( [\p{Zs}]  // any character with Unicode class Zs
    | '\u0009'  // horizontal tab
    | '\u000B'  // vertical tab
    | '\u000C'  // form feed
    )+
  ;
```

```
fragment PP_New_Line
  : PP_Whitespace? Single_Line_Comment? New_Line
  ;
```

*注意：*

- 预处理器语法为所有预处理指令定义了单个词法标记 PP_Directive。每个预处理指令的语义在该语言规范中定义，但不定义如何实现它们。
- PP_Start 片段必须仅在行的开头被识别，上面 getCharPositionInLine() == 0 ANTLR 词法谓词建议了一种实现方式，仅供参考，实现可以使用不同的策略。

*注释结束*

以下预处理指令可用：

- #define 和 #undef，分别用于定义和取消定义条件编译符号（§6.5.4）。
- #if、#elif、#else 和 #endif，用于有条件地跳过源代码部分（§6.5.5）。
- #line，用于控制为错误和警告发出的行号（§6.5.8）。
- #error，用于发出错误（§6.5.6）。
- #region 和 #endregion，用于显式标记源代码部分（§6.5.7）。
- #pragma，用于向编译器指定可选的上下文信息（§6.5.9）。

预处理指令始终占用源代码的单独一行，并且始终以 # 字符和预处理指令名称开头。在 # 字符之前以及 # 字符与指令名称之间可能出现空白。

包含 #define、#undef、#if、#elif、#else、#endif、#line 或 #endregion 指令的源行可以以单行注释结束。包含预处理指令的源行上不允许使用定界注释（/* */ 风格的注释）。

预处理指令不是 C# 语法语法的一部分。然而，预处理指令可用于包含或排除标记序列，从而以这种方式影响 C# 程序的含义。

*示例：* 编译时，程序

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

结果与程序产生的标记序列完全相同

```
class C
{
    void F() {}
    void I() {}
}
```

因此，虽然在词法上这两个程序差异很大，但在语法上它们是相同的。

*示例结束*

### 6.5.2 条件编译符号

#if、#elif、#else 和 #endif 指令提供的条件编译功能通过预处理表达式（§6.5.3）和条件编译符号控制。

```
fragment PP_Conditional_Symbol
    // Must not be equal to tokens TRUE or FALSE. See note below.
    : Basic_Identifier
    ;
```

*注意：* 实现如何强制执行对允许的 *Basic_Identifier* 值的限制是实现问题。 *注释结束*

如果在应用以下转换后两个条件编译符号相同，则认为它们相同，按顺序：

- 每个 *Unicode_Escape_Sequence* 转换为其对应的 Unicode 字符。
- 任何 *Formatting_Characters* 都被移除。

条件编译符号有两种可能的状态：*已定义* 或 *未定义*。在编译单元的词法处理开始时，条件编译符号未定义，除非它已被外部机制（例如命令行编译器选项）显式定义。当处理 #define 指令时，该指令中命名的条件编译符号在该编译单元中变为已定义。该符号保持已定义状态，直到处理该相同符号的 #undef 指令，或直到达到编译单元的末尾为止。其含义是，一个编译单元中的 #define 和 #undef 指令对同一程序中的其他编译单元没有影响。

当在预处理表达式（§6.5.3）中引用时，已定义的条件编译符号具有布尔值 true，未定义的条件编译符号具有布尔值 false。条件编译符号在预处理表达式中被引用之前不需要显式声明。相反，未声明的符号 simply 未定义，因此其值为 false。

条件编译符号的命名空间与 C# 程序中的所有其他命名实体是不同的且独立的。条件编译符号只能在 #define 和 #undef 指令以及预处理表达式中引用。

### 6.5.3 预处理表达式

预处理表达式可以出现在 #if 和 #elif 指令中。运算符 !、==、!=、&& 和 || 在预处理表达式中允许使用，并且可以使用括号进行分组。

```
fragment PP_Expression
    : PP_Whitespace? PP_Or_Expression PP_Whitespace?
    ;

fragment PP_Or_Expression
    : PP_And_Expression (PP_Whitespace? '||' PP_Whitespace? PP_And_Expression)*
    ;

fragment PP_And_Expression
    : PP_Equality_Expression (PP_Whitespace? '&&' PP_Whitespace? PP_Equality_Expression)*
    ;

fragment PP_Equality_Expression
    : PP_Unary_Expression (PP_Whitespace? ('==' | '!=') PP_Whitespace? PP_Unary_Expression)*
    ;

fragment PP_Unary_Expression
```

```
: PP_Primary_Expression
| '!' PP_Whitespace? PP_Unary_Expression
;
```

fragment PP_Primary_Expression
: TRUE
| FALSE
| PP_Conditional_Symbol
| '(' PP_Whitespace? PP_Expression PP_Whitespace? ')'
;

当在预处理表达式中引用时，已定义的条件编译符号具有布尔值 true，而未定义的条件编译符号具有布尔值 false。

预处理表达式的求值始终产生布尔值。预处理表达式的求值规则与常量表达式 (§12.23) 的规则相同，只是唯一可以引用的用户定义实体是条件编译符号。

## 6.5.4 定义指令

定义指令用于定义或取消定义条件编译符号。

```
fragment PP_Declaration
: 'define' PP_Whitespace PP_Conditional_Symbol
| 'undef' PP_Whitespace PP_Conditional_Symbol
;
```

处理 #define 指令会导致给定的条件编译符号从指令之后的源代码行开始被定义。同样地，处理 #undef 指令会导致给定的条件编译符号从指令之后的源代码行开始被取消定义。

编译单元中的任何 #define 和 #undef 指令都必须出现在编译单元中的第一个标记 (§6.4) 之前；否则会发生编译时错误。直观地说，#define 和 #undef 指令必须位于编译单元中任何“实际代码”之前。

示例：示例：

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

是有效的，因为 #define 指令位于编译单元中的第一个标记（namespace 关键字）之前。

示例结束

示例：以下示例因 #define 出现在实际代码之后而导致编译时错误：

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

*示例结束*

#define 可以定义一个已经定义的条件编译符号，而无需对该符号进行中间的 #undef。

*示例：* 下面的示例定义了条件编译符号 A 然后再次定义它。

```
#define A
#define A
```

对于允许将条件编译符号作为编译选项定义的编译器，此类重定义发生的另一种方式是在源代码中以及作为编译器选项定义该符号。

*示例结束*

#undef 可以“取消定义”未定义的条件编译符号。

*示例：* 下面的示例定义了条件编译符号 A 然后两次取消定义它；尽管第二次 #undef 没有效果，但它仍然有效。

```
#define A
#undef A
#undef A
```

*示例结束*

## 6.5.5 条件编译指令

条件编译指令用于有条件地包含或排除编译单元的部分内容。

```
fragment PP_Conditional
  : PP_If_Section
  | PP_Elif_Section
  | PP_Else_Section
  | PP_Endif
  ;

fragment PP_If_Section
  : 'if' PP_Whitespace PP_Expression
  ;

fragment PP_Elif_Section
  : 'elif' PP_Whitespace PP_Expression
  ;

fragment PP_Else_Section
  : 'else'
  ;

fragment PP_Endif
  : 'endif'
  ;
```

条件编译指令应按顺序以组的形式编写，包括 #if 指令、零个或多个 #elif 指令、零个或一个 #else 指令以及一个 #endif 指令。在指令之间是源代码的条件部分。每个部分由紧邻的前一个指令控制。条件部分本身可以包含嵌套的条件编译指令，前提是这些指令构成完整的组。

最多只有一个包含的条件部分被选中进行正常的词法处理：

- #if 和 #elif 指令的 PP_Expressions 按顺序求值，直到有一个产生 true。如果表达式产生 true，则选择对应指令之后的条件部分。
- 如果所有 PP_Expressions 都产生 false，并且存在 #else 指令，则选择 #else 指令之后的条件部分。
- 否则，不选择任何条件部分。

所选条件部分（如果有）作为正常的 input_section 处理：该部分包含的源代码应遵循词法语法；从该部分中的源代码生成标记；并且该部分中的预处理指令具有规定的效果。

任何剩余的条件部分将被跳过，并且除了预处理指令之外，不会从源代码生成任何标记。因此，被跳过的源代码（预处理指令除外）可能在词法上不正确。被跳过的预处理指令在词法上必须正确，但不会被进一步处理。在被跳过的条件部分内，任何嵌套的条件部分（包含在嵌套的 #if...#endif 构造中）也将被跳过。

注意：上述语法并未涵盖预处理指令之间的条件部分可能在词法上格式错误的允许情况。因此，该语法不是 ANTLR 就绪的，因为它仅支持词法正确的输入。 注意结束

示例：以下示例说明了条件编译指令如何嵌套：

```
#define Debug // Debugging on
#undef Trace // Tracing off
class PurchaseTransaction
{
    void Commit()
    {
#if Debug
    CheckConsistency();
#if Trace
    WriteToLog(this.ToString());
#endif
#endif
    CommitHelper();
    ...
}
}
```

除了预处理指令之外，被跳过的源代码不受词法分析的约束。例如，尽管 #else 部分中存在未终止的注释，以下内容仍然有效：

```
#define Debug // Debugging on
class PurchaseTransaction
{
void Commit()
{
#if Debug
    CheckConsistency();
#else    /* Do something else
#endif
    ...
}
```

然而需要注意的是，即使在被跳过的源代码部分中，预处理指令也必须在词法上正确。

当预处理指令出现在多行输入元素内部时，不会被处理。例如，程序：

```
class Hello
{
    static void Main()
    {
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

在特殊情况下，被处理的预处理指令集合可能取决于 pp_expression 的求值。示例：

```
#if X
/*
#else
/* */ class Q { }
#endif
```

无论 X 是否定义，始终产生相同的标记流（class Q { }）。如果 X 已定义，则由于多行注释，唯一被处理的指令是 #if 和 #endif。如果 X 未定义，则三个指令（#if、#else、#endif）属于指令集。

示例结束

## 6.5.6 诊断指令

诊断指令用于显式生成错误和警告消息，这些消息以与其他编译时错误和警告相同的方式报告。

```
fragment PP_Diagnostic
: 'error' PP_Message?
| 'warning' PP_Message?
;

fragment PP_Message
: PP_Whitespace Input_Character*
;
```

示例：示例

```
#if Debug && Retail
    #error A build can't be both debug and retail
#endif
class Test {...}
```

如果条件编译符号 Debug 和 Retail 同时被定义，则会产生编译时错误（"A build can't be both debug and retail"）。请注意，PP_Message 可以包含任意文本；具体来说，它不必包含格式良好的标记，正如单词 can't 中的单引号所示。

示例结束

## 6.5.7 区域指令

区域指令用于显式标记源代码的区域。

```
fragment PP_Region
: PP_Start_Region
| PP_End_Region
;

fragment PP_Start_Region
: 'region' PP_Message?
;

fragment PP_End_Region
: 'endregion' PP_Message?
;
```

区域不附加任何语义含义；区域 intended for programmer or automated tools to mark a section of source code。必须有一个 #endregion 指令与每个 #region 指令匹配。#region 或 #endregion 指令中指定的消息同样没有语义含义；它仅用于标识区域。匹配的 #region 和 #endregion 指令可能具有不同的 PP_Messages。

区域的词法处理：

```
#region
...
#endregion
```

与以下形式的条件编译指令的词法处理完全对应：

```
#if true
...
#endif
```

> Note: 这意味着一个区域可以包含一个或多个 #if.../#endif，或包含在 #if.../#endif 内的条件部分中；但一个区域不能与 #if.../#endif 的仅一部分重叠，或在不同的条件部分中开始和结束。 end note

## 6.5.8 行指令

行指令可用于更改编译器在警告和错误等输出中报告的行号和编译单元名称。这些值也由调用信息属性 (§22.5.5) 使用。

> Note: 行指令最常用于从其他文本输入生成 C# 源代码的元编程工具中。 end note

```
fragment PP_Line
  : 'line' PP_Whitespace PP_Line_Indicator
  ;

fragment PP_Line_Indicator
  : Decimal_Digit+ PP_Whitespace PP_Compilation_Unit_Name
  | Decimal_Digit+
  | DEFAULT
  | 'hidden'
  ;

fragment PP_Compilation_Unit_Name
  : '"' PP_Compilation_Unit_Name_Character+ '"'
  ;

fragment PP_Compilation_Unit_Name_Character
  // Any Input_Character except "
  : ~('\\u000D' | '\\u000A' | '\\u0085' | '\\u2028' | '\\u2029' | '#')
  ;
```

当不存在 #line 指令时，编译器在其输出中报告真实的行号和编译单元名称。当处理包含非默认 PP_Line_Indicator 的 #line 指令时，编译器将该指令之后的行的行号视为给定行号（如果指定，则包括编译单元名称）。

最大允许的 Decimal_Digit+ 值由实现定义。

#line default 指令会撤销所有前面 #line 指令的效果。编译器对后续行报告真实的行信息，就好像没有处理过 #line 指令一样。

#line hidden 指令对错误消息中报告的编译单元和行号，或由 CallerLineNumberAttribute (§22.5.5.2) 使用产生的结果没有影响。它的目的是影响源代码级调试工具，以便在调试时，#line hidden 指令与后续 #line 指令（不是 #line hidden）之间的所有行都没有行号信息，并且在单步执行代码时完全被跳过。

> Note: 尽管 PP_Compilation_Unit_Name 可能包含看起来像转义序列的文本，但此类文本不是转义序列；在这种情况下，'\' 字符仅表示普通的反斜杠字符。 end note

## 6.5.9 Pragma 指令

#pragma 预处理指令用于向编译器指定上下文信息。

*注意：例如，编译器可能会提供 #pragma 指令，例如*
- 在编译后续代码时启用或禁用特定警告消息。
- 指定对后续代码应用哪些优化。
- 指定调试器使用的信息。
*结束注释*

```
fragment PP_Pragma
    : 'pragma' PP_Pragma_Text?
    ;

fragment PP_Pragma_Text
    : PP_Whitespace Input_Character*
    ;
```

*Input_Characters* 在 *PP_Pragma_Text* 中由编译器以实现定义的方式解释。#pragma 指令中提供的信息不得更改程序语义。#pragma 指令只能更改超出本语言规范范围的编译器行为。如果编译器无法解释 *Input_Characters*，编译器可以发出警告；但是，它不得产生编译时错误。

*注意：PP_Pragma_Text 可以包含任意文本；具体来说，它不必包含格式良好的标记。结束注释*

# 7. 基本概念

### 7.1 应用程序启动

程序可以编译为 *类库* 以作为其他应用程序的一部分使用，也可以编译为可直接启动的 *应用程序*。确定此编译模式的机制是实现特定的，并且在该规范之外。

程序编译为应用程序时，必须至少包含一个满足以下要求的方法作为入口点：
- 它的名称应为 `Main`。
- 它应为 `static`。
- 它不应是泛型的。
- 它应在非泛型类型中声明。如果声明该方法的类型是嵌套类型，则其所有封闭类型都不得是泛型的。
- 如果方法返回类型为 `System.Threading.Tasks.Task` 或 `System.Threading.Tasks.Task<int>`，则它可以具有 `async` 修饰符。
- 返回类型应为 `void`、`int`、`System.Threading.Tasks.Task` 或 `System.Threading.Tasks.Task<int>`。
- 它不得是没有实现的 partial 方法 (§15.6.9)。
- 形式参数列表应为空，或具有单个类型为 `string[]` 的值参数。

*注意：* 具有 `async` 修饰符的方法必须具有上述两个返回类型之一，才能符合入口点的条件。`async void` 方法，或返回不同可等待类型（如 `ValueTask` 或 `ValueTask<int>`）的 `async` 方法不符合入口点的条件。 *结束注释*

如果在程序中声明了多个符合入口点条件的方法，可以使用外部机制指定哪个方法被视为应用程序的实际入口点。如果找到返回类型为 `int` 或 `void` 的符合条件的方法，则返回类型为 `System.Threading.Tasks.Task` 或 `System.Threading.Tasks.Task<int>` 的任何符合条件的方法均不被视为入口点方法。将程序编译为应用程序而没有恰好一个入口点是编译时错误。编译为类库的程序可能包含符合应用程序入口点条件的方法，但生成的库没有入口点。

通常，方法的声明可访问性 (§7.5.2) 由其声明中指定的访问修饰符 (§15.3.6) 决定，类似地，类型的声明可访问性由其声明中指定的访问修饰符决定。为了使给定类型的给定方法可调用，类型和成员都应可访问。然而，应用程序入口点是一个特例。具体来说，执行环境可以访问应用程序的入口点，而不管其声明的可访问性以及其封闭类型声明的声明可访问性如何。

当入口点方法的返回类型为 System.Threading.Tasks.Task 或 System.Threading.Tasks.Task<int> 时，编译器会合成一个调用相应 Main 方法的同步入口点方法。合成的方法具有基于 Main 方法的参数和返回类型：
- 合成方法的形式参数列表与 Main 方法的形式参数列表相同
- 如果 Main 方法的返回类型为 System.Threading.Tasks.Task，则合成方法的返回类型为 void
- 如果 Main 方法的返回类型为 System.Threading.Tasks.Task<int>，则合成方法的返回类型为 int

合成方法的执行按如下方式进行：
- 合成方法调用 Main 方法，如果 Main 方法具有此类参数，则将其 string[] 参数值作为参数传递。
- 如果 Main 方法抛出异常，则异常由合成方法传播。
- 否则，合成的入口点等待返回的任务完成，对任务调用 GetAwaiter().GetResult()，使用无参数实例方法或 §C.3 中描述的扩展方法。如果任务失败，GetResult() 将抛出异常，并且该异常由合成方法传播。
- 对于返回类型为 System.Threading.Tasks.Task<int> 的 Main 方法，如果任务成功完成，则 GetResult() 返回的 int 值将从合成方法返回。

应用程序的有效入口点是程序中声明的入口点，或如上所述需要时合成的方法。因此，有效入口点的返回类型始终为 void 或 int。

当应用程序运行时，会创建一个新的应用程序域。同一台机器上可能同时存在应用程序的多个不同实例，每个实例都有自己的应用程序域。应用程序域通过充当应用程序状态的容器来实现应用程序隔离。应用程序域充当应用程序中定义的类型及其使用的类库的容器和边界。加载到一个应用程序域中的类型与加载到另一个应用程序域中的相同类型是不同的，并且对象实例不会在应用程序域之间直接共享。例如，每个应用程序域都有这些类型的静态变量的自己的副本，并且类型的静态构造函数每个应用程序域最多运行一次。实现可以自由提供创建和销毁应用程序域的实现特定策略或机制。

应用程序启动发生在执行环境调用应用程序的有效入口点时。如果有效入口点声明了一个参数，则在应用程序启动期间，实现应确保该参数的初始值为对字符串数组的非空引用。该数组应由非空的字符串引用组成，称为应用程序参数，这些参数在应用程序启动之前由主机环境赋予实现定义的值。其目的是将托管环境中在应用程序启动前确定的信息提供给应用程序。

> Note: 在支持命令行系统的系统上，应用程序参数对应于通常所知的命令行参数。 end note



如果有效入口点的返回类型为 int，则执行环境对该方法调用的返回值将在应用程序终止时使用（§7.2）。

除上述情况外，入口点方法在各方面都与非入口点方法表现相同。特别是，如果在应用程序生命周期中的其他任何时刻调用入口点，例如通过常规方法调用，则该方法不会有特殊处理：如果有参数，其初始值可能为 null，或为非空值，引用一个包含空引用的数组。同样，入口点的返回值除在执行环境调用时外，没有特殊意义。

## 7.2 应用程序终止

应用程序终止将控制权返回给执行环境。

如果应用程序的有效入口点方法的返回类型为 int 且执行在未引发异常的情况下完成，则返回的 int 值作为应用程序的终止状态码。此代码的目的是允许向执行环境传达成功或失败。如果有效入口点方法的返回类型为 void 且执行在未引发异常的情况下完成，则终止状态码为 0。

如果有效入口点方法因异常终止（§21.4），则退出代码是实现相关的。此外，实现可能提供用于指定退出代码的替代 API。

应用程序终止时是否运行终结器（§15.13）是实现相关的。

> 注：.NET Framework 实现会尽一切合理努力为所有尚未被垃圾回收的对象调用终结器（§15.13），除非此类清理已被抑制（例如通过调用库方法 GC.SuppressFinalize）。 end note

## 7.3 声明

C# 程序中的声明定义了程序的构成元素。C# 程序使用命名空间组织。这些命名空间通过命名空间声明（§14）引入，可包含类型声明和嵌套的命名空间声明。类型声明（§14.7）用于定义类（§15）、结构体（§16）、接口（§18）、枚举（§19）和委托（§20）。类型声明中允许的成员种类取决于类型声明的形式。例如，类声明可包含常量（§15.4）、字段（§15.5）、方法（§15.6）、属性（§15.7）、事件（§15.8）、索引器（§15.9）、运算符（§15.10）、实例构造函数（§15.11）、静态构造函数（§15.12）、终结器（§15.13）和嵌套类型（§15.3.9）的声明。

声明在声明所属的声明空间中定义一个名称。在声明空间中存在两个或多个引入同名成员的声明是编译时错误，除以下情况外：

- 在同一声明空间中允许存在两个或多个同名的命名空间声明。此类命名空间声明被聚合形成单个逻辑命名空间并共享单个声明空间。
- 在不同程序但同一命名空间声明空间中的声明允许共享相同的名称。

> 注：然而，如果包含在同一应用程序中，这些声明可能会引入歧义。 end note

- 在同一声明空间中允许存在两个或多个同名但签名不同的 方法（§7.6）。
- 在同一声明空间中允许存在两个或多个同名但类型参数数量不同的类型声明（§7.8.2）。
- 在同一声明空间中带有 partial 修饰符的两个或多个类型声明可以共享相同的名称、相同的类型参数数量和相同的分类（class、struct 或 interface）。在这种情况下，类型声明共同构成一个类型，并且自身被聚合形成单个声明空间（§15.2.7）。
- 同一声明空间中的命名空间声明和类型声明可以共享相同的名称，只要类型声明至少有一个类型参数（§7.8.2）。

存在几种不同类型的声明空间，如下所述。

- 在程序的所有编译单元中，没有封闭 namespace_declaration 的 namespace_member_declarations 是单个组合声明空间的成员，该空间称为全局声明空间。
- 在程序的所有编译单元中，具有相同完全限定命名空间名称的 namespace_declarations 内的 namespace_member_declarations 是单个组合声明空间的成员。
- 每个 compilation_unit 和 namespace_body 都有一个别名声明空间。compilation_unit 或 namespace_body 的每个 extern_alias_directive 和 using_alias_directive 都向别名声明空间贡献一个成员（§14.5.2）。
- 每个非 partial 的 class、struct 或 interface 声明都会创建一个新的声明空间。每个 partial class、struct 或 interface 声明都贡献给同一程序中所有匹配部分共享的声明空间（§16.2.4）。名称通过 class_member_declarations、struct_member_declarations、interface_member_declarations 或 type_parameters 引入到此声明空间中。除重载的实例构造函数声明和静态构造函数声明外，class 或 struct 不能包含与 class 或 struct 名称相同的成员声明。class、struct 或 interface 允许声明重载的方法和索引器。此外，class 或 struct 允许声明重载的实例构造函数和运算符。例如，class、struct 或 interface 可以包含多个同名的方法声明，前提是这些方法声明的签名不同（§7.6）。请注意，基类不贡献于类的声明空间，基接口不贡献于接口的声明空间。因此，派生类或接口允许声明与继承成员同名的成员。此类成员称为隐藏继承的成员。
- 每个 delegate 声明都会创建一个新的声明空间。名称通过形式参数（fixed_parameters 和 parameter_arrays）和 type_parameters 引入到此声明空间中。
- 每个枚举声明都会创建一个新的声明空间。名称通过 enum_member_declarations 引入到此声明空间中。
- 每个方法声明、属性声明、属性访问器声明、索引器声明、索引器访问器声明、运算符声明、实例构造函数声明、匿名函数和局部函数都会创建一个称为局部变量声明空间的新声明空间。名称通过形式参数（fixed_parameters 和 parameter_arrays）和 type_parameters 引入到此声明空间中。属性或索引器的 set 访问器将名称 value 作为形式参数引入。

- 在成员声明、匿名函数和局部函数内部可能出现额外的局部变量声明空间。名称通过 patterns、declaration_expressions、declaration_statements 和 exception_specifiers 引入到这些声明空间中。局部变量声明空间可以嵌套，但如果一个局部变量声明空间与其嵌套的局部变量声明空间包含同名元素，则为错误。因此，在嵌套声明空间中，不可能声明一个与封闭声明空间中的参数、类型参数、局部变量、局部函数或常量同名的局部变量、局部函数或常量。只要两个声明空间互不包含，就可能包含同名元素。局部声明空间由以下结构创建：
  - 字段和属性声明中的每个 variable_initializer 都会引入自己的局部变量声明空间，该空间不嵌套在任何其他局部变量声明空间内。
  - 函数成员、匿名函数或局部函数的体（如果有）会创建一个局部变量声明空间，该空间被视为嵌套在函数的局部变量声明空间内。
  - 每个 constructor_initializer 都会在实例构造函数声明内创建一个嵌套的局部变量声明空间。构造函数体的局部变量声明空间反过来嵌套在此局部变量声明空间内。
  - 每个 block、switch_block、specific_catch_clause、iteration_statement 和 using_statement 都会创建一个嵌套的局部变量声明空间。
  - 每个不是 statement_list 直接组成部分的 embedded_statement 都会创建一个嵌套的局部变量声明空间。
  - 每个 switch_section 都会创建一个嵌套的局部变量声明空间。然而，直接在 switch_section 的 statement_list 内声明的变量（但不在 statement_list 内的嵌套局部变量声明空间内）会直接添加到封闭 switch_block 的局部变量声明空间中，而不是 switch_section 的声明空间。
  - query_expression（§12.20.3）的语法转换可能会引入一个或多个 lambda 表达式。作为匿名函数，每个都如上所述创建局部变量声明空间。
- 每个 block 或 switch_block 都会为标签创建一个单独的声明空间。名称通过 labeled_statements 引入到此声明空间中，并通过 goto_statements 引用。块的标签声明空间包括任何嵌套块。因此，在嵌套块中，不可能声明一个与封闭块中的标签同名的标签。

名称声明的文本顺序通常无关紧要。特别是，文本顺序对于命名空间、常量、方法、属性、事件、索引器、运算符、实例构造函数、终结器、静态构造函数和类型的声明和使用并不重要。声明顺序在以下方面很重要：

- 字段声明的声明顺序决定了其初始化器（如果有）的执行顺序（§15.5.6.2、§15.5.6.3）。
- 局部变量必须在使用前定义（§7.7）。



- 当省略 *常量表达式* 值时，枚举成员声明（§19.4）的声明顺序很重要。

示例：命名空间的声明空间是“开放式的”，两个具有相同完全限定名的命名空间声明会贡献到同一个声明空间。例如

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

上面的两个命名空间声明贡献到同一个声明空间，在此例中声明了两个完全限定名分别为 Megacorp.Data.Customer 和 Megacorp.Data.Order 的类。由于这两个声明贡献到同一个声明空间，如果每个声明都包含一个同名类的声明，则会导致编译时错误。

示例结束

注意：如上所述，块的声明空间包括任何嵌套块。因此，在下面的示例中，F 和 G 方法会导致编译时错误，因为名称 i 在外层块中声明，不能在内层块中重新声明。但是，H 和 I 方法是有效的，因为两个 i 是在分开的非嵌套块中声明的。

```
class A
{
    void F()
    {
        int i = 0;
        if (true)
        {
            int i = 1;
        }
    }

    void G()
    {
        if (true)
        {
            int i = 0;
        }
        int i = 1;
    }

    void H()
    {
        if (true)
        {
            int i = 0;
        }
        if (true)
        {
            int i = 1;
        }
    }
    void I()
    {
        for (int i = 0; i < 10; i++)
        {
            H();
        }
        for (int i = 0; i < 10; i++)
        {
            H();
        }
    }
}
```

## 7.4 成员

### 7.4.1 概述

命名空间和类型具有成员。

> 注意：实体的成员通常可以通过使用限定名来访问，该限定名以对实体的引用开头，后跟一个“.”标记，再跟成员名称。注意结束

类型的成员要么在类型声明中声明，要么从该类型的基类继承。当某个类型从基类继承时，基类的所有成员（实例构造函数、终结器和静态构造函数除外）都会成为派生类型的成员。基类成员的声明可访问性并不控制该成员是否被继承——继承会扩展到任何不是实例构造函数、静态构造函数或终结器的成员。

> 注意：但是，继承成员在派生类型中可能不可访问，例如由于其声明可访问性（§7.5.2）。注意结束

### 7.4.2 命名空间成员

没有外围命名空间的命名空间和类型是全局命名空间的成员。这直接对应于在全局声明空间中声明的名称。

在某个命名空间内声明的命名空间和类型是该命名空间的成员。这直接对应于在该命名空间的声明空间中声明的名称。

命名空间没有访问限制。不能声明 private、protected 或 internal 命名空间，并且命名空间名称始终是公开可访问的。

struct（即不由该 struct 继承）不能具有 protected、protected internal 或 private protected 声明可访问性。

注意：声明为 struct 成员的类型可以具有 public、internal 或 private 声明可访问性，而声明为命名空间成员的类型只能具有 public 或 internal 声明可访问性。注意结束

- 接口成员隐式具有 public 声明可访问性。接口成员声明上不允许使用访问修饰符。
- 枚举成员隐式具有 public 声明可访问性。枚举成员声明上不允许使用访问修饰符。

### 7.5.3 可访问域

成员的可访问域由允许访问该成员的程序文本的（可能不相交的）部分组成。为了定义成员的可访问域，如果某个成员未在类型内声明，则称该成员为顶级成员；如果某个成员在另一个类型内声明，则称该成员为嵌套成员。此外，程序的程序文本定义为该程序所有编译单元中包含的所有文本，类型的程序文本定义为该类型的 type_declarations 中包含的所有文本（可能包括嵌套在该类型中的类型）。

预定义类型（如 object、int 或 double）的可访问域是无限制的。

在程序 P 中声明的顶级未绑定类型 T（§8.4.4）的可访问域定义如下：

- 如果 T 的声明可访问性是 public，则 T 的可访问域是 P 的程序文本以及任何引用 P 的程序的程序文本。
- 如果 T 的声明可访问性是 internal，则 T 的可访问域是 P 的程序文本。

注意：根据这些定义可知，顶级未绑定类型的可访问域始终至少是声明该类型的程序的程序文本。注意结束

构造类型 T<A1, ..., An> 的可访问域是未绑定泛型类型 T 的可访问域与类型实参 A1, ..., An 的可访问域的交集。

在程序 P 中的类型 T 内声明的嵌套成员 M 的可访问域定义如下（注意 M 本身可能是一个类型）：

- 如果 M 的声明可访问性是 public，则 M 的可访问域是 T 的可访问域。
- 如果 M 的声明可访问性是 protected internal，令 D 为 P 的程序文本与任何在 P 外部声明的、派生自 T 的类型的程序文本的并集。M 的可访问域是 T 的可访问域与 D 的交集。
- 如果 M 的声明可访问性是 private protected，令 D 为 P 的程序文本与任何派生自 T 的类型的程序文本的交集。M 的可访问域是 T 的可访问域与 D 的交集。
- 如果 M 的声明可访问性是 protected，令 D 为 T 的程序文本与任何派生自 T 的类型的程序文本的并集。M 的可访问域是 T 的可访问域与 D 的交集。
- 如果 M 的声明可访问性是 internal，则 M 的可访问域是 T 的可访问域与 P 的程序文本的交集。
- 如果 M 的声明可访问性是 private，则 M 的可访问域是 T 的程序文本。

注意：根据这些定义可知，嵌套成员的可访问域始终至少是声明该成员的类型程序文本。此外，成员的可访问域永远不会比声明该成员的类型可访问域包含更多内容。注意结束

注意：直观地说，当访问类型或成员 M 时，会评估以下步骤以确保允许访问：

- 首先，如果 M 是在某个类型内声明的（而不是在编译单元或命名空间内声明），并且该类型不可访问，则会发生编译时错误。
- 然后，如果 M 是 public，则允许访问。
- 否则，如果 M 是 protected internal，则当访问发生在声明 M 的程序中，或者发生在派生自声明 M 的类的类中并通过派生类类型（§7.5.4）进行时，允许访问。
- 否则，如果 M 是 protected，则当访问发生在声明 M 的类中，或者发生在派生自声明 M 的类的类中并通过派生类类型（§7.5.4）进行时，允许访问。
- 否则，如果 M 是 internal，则当访问发生在声明 M 的程序中时，允许访问。
- 否则，如果 M 是 private，则当访问发生在声明 M 的类型中时，允许访问。
- 否则，该类型或成员不可访问，并且会发生编译时错误。注意结束

示例：在以下代码中

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

```
```
}
}
```
```

类和成员具有以下可访问性域：

- `A` 和 `A.X` 的可访问性域是无限制的。
- `A.Y`、`B`、`B.X`、`B.Y`、`B.C`、`B.C.X` 和 `B.C.Y` 的可访问性域是包含程序的程序文本。
- `A.Z` 的可访问性域是 `A` 的程序文本。
- `B.Z` 和 `B.D` 的可访问性域是 `B` 的程序文本，包括 `B.C` 和 `B.D` 的程序文本。
- `B.C.Z` 的可访问性域是 `B.C` 的程序文本。
- `B.D.X` 和 `B.D.Y` 的可访问性域是 `B` 的程序文本，包括 `B.C` 和 `B.D` 的程序文本。
- `B.D.Z` 的可访问性域是 `B.D` 的程序文本。如示例所示，成员的可访问性域永远不会大于包含它的类型。例如，尽管所有 `X` 成员都具有公开声明的可访问性，但除 `A.X` 之外的所有成员的可访问性域都受到包含类型的约束。

*示例结束*

如 §7.4 中所述，基类的所有成员（实例构造函数、终结器和静态构造函数除外）都将被派生类型继承。这甚至包括基类的私有成员。然而，私有成员的可访问性域仅包括声明该成员的类型程序文本。

*示例：在以下代码中*

```csharp
class A
{
    int x;

    static void F(B b)
    {
        b.x = 1;        // Ok
    }
}

class B : A
{
    static void F(B b)
    {
        b.x = 1;        // Error, x not accessible
    }
}
```

`B` 类从 `A` 类继承了私有成员 `x`。由于该成员是私有的，它只能在 `A` 的 *类体* 内访问。因此，对 `b.x` 的访问在 `A.F` 方法中成功，但在 `B.F` 方法中失败。

*示例结束*

### 7.5.4 受保护的访问

当在声明它的类的程序文本之外访问 `protected` 或 `private protected` 实例成员时，以及当在声明它的程序的程序文本之外访问 `protected internal` 实例成员时，该访问必须在派生自声明该成员的类的类声明中进行。此外，访问必须 *通过* 该派生类类型或从其构造的类类型的实例进行。此限制防止一个派生类访问其他派生类的受保护成员，即使这些成员是从同一个基类继承的。

设 `B` 为声明受保护实例成员 `M` 的基类，设 `D` 为派生自 `B` 的类。在 `D` 的 *类体* 内，对 `M` 的访问可以采用以下形式之一：

- 未限定的 *类型名* 或形式为 `M` 的 *主表达式*。
- 形式为 `E.M` 的 *主表达式*，前提是 `E` 的类型是 `T` 或派生自 `T` 的类，其中 `T` 是类 `D`，或从 `D` 构造的类类型。
- 形式为 `base.M` 的 *主表达式*。
- 形式为 `base[argument_list]` 的 *主表达式*。

除了这些访问形式外，派生类还可以在 *构造函数初始值设定项* (§15.11.2) 中访问基类的受保护实例构造函数。

*示例：* 在以下代码中

```csharp
public class A
{
    protected int x;

    static void F(A a, B b)
    {
        a.x = 1; // Ok
        b.x = 1; // Ok
    }
}

public class B : A
{
    static void F(A a, B b)
    {
        a.x = 1; // Error, must access through instance of B
        b.x = 1; // Ok
    }
}
```

在 `A` 内部，可以通过 `A` 和 `B` 的实例访问 `x`，因为在任何一种情况下，访问都是 *通过* `A` 的实例或派生自 `A` 的类的实例进行的。然而，在 `B` 内部，不可能通过 `A` 的实例访问 `x`，因为 `A` 并未派生自 `B`。

*示例结束*

*示例：*

```csharp
class C<T>
{
    protected T x;
}

class D<T> : C<T>
{
    static void F()
    {
        D<T> dt = new D<T>();
        D<int> di = new D<int>();
        D<string> ds = new D<string>();
        dt.x = default(T);
        di.x = 123;
        ds.x = "test";
    }
}
```

这里，这三个对 x 的赋值是允许的，因为它们都通过从泛型类型构造的类类型的实例进行。

示例结束

注意： 在泛型类中声明的受保护成员的可访问性域 (§7.5.3) 包括派生自该泛型类构造的任何类型的程序文本。

在示例中：

```csharp
class C<T>
{
    protected static T x;
}

class D : C<string>
{
    static void Main()
    {
        C<int>.x = 5;
    }
}
```

对 D 中受保护成员 C<int>.x 的引用是有效的，即使类 D 派生自 C<string>。 注释结束

### 7.5.5 可访问性约束

C# 语言中的若干构造要求类型至少与成员或其他类型一样可访问。如果类型 T 的可访问性域是成员或类型 M 的可访问性域的超集，则称类型 T 至少与成员或类型 M 一样可访问。换句话说，如果 T 在 M 可访问的所有上下文中都可访问，则 T 至少与 M 一样可访问。

存在以下可访问性约束：

- 类类型的直接基类应至少与类类型本身一样可访问。
- 接口类型的显式基接口应至少与接口类型本身一样可访问。
- 委托类型的返回类型和参数类型应至少与委托类型本身一样可访问。
- 常量的类型应至少与常量本身一样可访问。
- 字段的类型应至少与字段本身一样可访问。
- 方法的返回类型和参数类型应至少与方法本身一样可访问。
- 属性的类型应至少与属性本身一样可访问。
- 事件的类型应至少与事件本身一样可访问。
- 索引器的类型和参数类型应至少与索引器本身一样可访问。
- 运算符的返回类型和参数类型应至少与运算符本身一样可访问。
- 实例构造函数的参数类型应至少与实例构造函数本身一样可访问。
- 对类型参数的接口或类类型约束应至少与声明该约束的成员一样可访问。

示例：在以下代码中

```csharp
class A {...}
public class B: A {...}
```

B 类导致编译时错误，因为 A 并非至少与 B 一样可访问。

示例结束

示例：同样，在以下代码中

```csharp
class A {...}

public class B
{
    A F() {...}
    internal A G() {...}
    public A H() {...}
}
```

B 中的 H 方法导致编译时错误，因为返回类型 A 并非至少与该方法一样可访问。

示例结束

## 7.6 签名和重载

方法、实例构造函数、索引器和运算符以其签名为特征：

- 方法的签名由方法名、类型参数的数量以及其每个形式参数的类型和参数传递模式组成，按从左到右的顺序考虑。为此目的，方法中出现在形式参数类型中的任何类型参数不是按其名称标识，而是按其在方法类型参数列表中的序数位置标识。方法的签名 specifically 不包括返回类型、参数名、类型参数名、类型参数约束、params 或 this 参数修饰符，以及参数是否必需或可选。
- 实例构造函数的签名由其每个形式参数的类型和参数传递模式组成，按从左到右的顺序考虑。实例构造函数的签名

具体而言，不包括可为最右侧参数指定的 params 修饰符。

- 索引器的签名由其每个形参的类型组成，按从左到右的顺序考虑。索引器的签名具体不包括元素类型，也不包括可为最右侧参数指定的 params 修饰符。
- 运算符的签名由运算符的名称及其每个形参的类型组成，按从左到右的顺序考虑。运算符的签名具体不包括结果类型。
- 转换运算符的签名由源类型和目标类型组成。转换运算符的隐式或显式分类不属于签名的一部分。
- 同一成员种类（方法、实例构造函数、索引器或运算符）的两个签名，如果它们具有相同的名称、类型参数数目、参数数目和参数传递模式，并且它们对应参数的类型之间存在恒等转换（§10.2.2），则被视为相同签名。

签名是类、结构和接口中成员重载得以实现的机制：

- 方法重载允许类、结构或接口声明多个同名方法，前提是这些方法在该类、结构或接口中的签名唯一。
- 实例构造函数重载允许类或结构声明多个实例构造函数，前提是这些构造函数在该类或结构中的签名唯一。
- 索引器重载允许类、结构或接口声明多个索引器，前提是这些索引器在该类、结构或接口中的签名唯一。
- 运算符重载允许类或结构声明多个同名运算符，前提是这些运算符在该类或结构中的签名唯一。

尽管 in、out 和 ref 参数修饰符被视为签名的一部分，但在单个类型中声明的成员不能仅通过 in、out 和 ref 而在签名上有所不同。如果同一类型中声明的两个成员具有这样的签名：将两个方法中所有带 out 或 in 修饰符的参数都改为 ref 修饰符后，这些签名会相同，则发生编译时错误。对于签名匹配的其他目的（例如隐藏或重写），in、out 和 ref 被视为签名的一部分，并且彼此不匹配。

> 注意：此限制是为了允许 C# 程序轻松转换为在公共语言基础结构（CLI）上运行，CLI 不提供定义仅在 in、out 和 ref 上不同的方法的方式。注释结束

比较签名时，不区分类型 object 和 dynamic。因此，不允许在单个类型中声明仅通过用 dynamic 替换 object 而不同的成员。

示例：以下示例展示了一组重载方法声明及其签名。

```csharp
interface ITest
{
    void F();
    // F()
    void F(int x);
    // F(int)
    void F(ref int x);
    // F(ref int)
    void F(out int x);
    // F(out int) error
    void F(object o);
    // F(object)
    void F(dynamic d);
    // error.
    void F(int x, int y);        // F(int, int)
    int F(string s);             // F(string)
    int F(int x);                // F(int) error
    void F(string[] a);          // F(string[])
    void F(params string[] a);   // F(string[]) error
    void F<S>(S s);              // F<>()
    void F<T>(T t);              // F<>() error
    void F<S,T>(S s);            // F<0,1>()
    void F<T,S>(S s);            // F<0,1>() ok
}
```

注意，任何 `in`、`out` 和 `ref` 参数修饰符（§15.6.2）都是签名的一部分。因此，`F(int)`、`F(in int)`、`F(out int)` 和 `F(ref int)` 都是唯一的签名。但是，`F(in int)`、`F(out int)` 和 `F(ref int)` 不能在同一接口中声明，因为它们的签名仅通过 `in`、`out` 和 `ref` 不同。另外，注意返回类型和 `params` 修饰符不是签名的一部分，因此不能仅基于返回类型或是否包含 `params` 修饰符进行重载。因此，上面标识的方法 `F(int)` 和 `F(params string[])` 的声明会导致编译时错误。*示例结束*

## 7.7 作用域

### 7.7.1 概述

名称的*作用域*是程序文本中的一个区域，在该区域内，可以在不对名称进行限定的情况下引用由该名称声明的实体。作用域可以*嵌套*，并且内部作用域可以重新声明外部作用域中名称的含义。（但是，这并不解除 §7.3 施加的限制：在嵌套块中，不能声明与封闭块中的局部变量或局部常量同名的局部变量或局部常量。）此时，称外部作用域中的名称在内部作用域所覆盖的程序文本区域中被*隐藏*，并且只能通过限定该名称来访问外部名称。

- 由没有封闭 *命名空间声明* 的 *命名空间成员声明*（§14.6）所声明的命名空间成员，其作用域是整个程序文本。
- 由 *命名空间声明* 中的 *命名空间成员声明* 所声明的命名空间成员，若该 *命名空间声明* 的完全限定名为 *N*，则其作用域是每个完全限定名为 *N* 或以 *N* 后跟一个句点开头的 *命名空间声明* 的 *命名空间主体*。
- 由 *外部别名指令*（§14.4）定义的名称，其作用域涵盖直接包含该指令的 *编译单元* 或 *命名空间主体* 的 *using 指令*、*全局特性* 和 *命名空间成员声明*。*外部别名指令* 不会向基础声明空间贡献任何新成员。换言之，*外部别名指令* 不具有传递性，而只影响其所在的 *编译单元* 或 *命名空间主体*。
- 由 *using 指令*（§14.5）定义或导入的名称，其作用域涵盖该 *using 指令* 所在的 *编译单元* 或 *命名空间主体* 的 *全局特性* 和 *命名空间成员声明*。*using 指令* 可以使零个或多个命名空间名或类型名在特定 *编译单元* 或 *命名空间主体* 中可用，但不会向基础声明空间贡献任何新成员。换言之，*using 指令* 不具有传递性，而只影响其所在的 *编译单元* 或 *命名空间主体*。
- 由 *类声明*（§15.2）上的 *类型参数列表* 所声明的类型参数，其作用域是该 *类声明* 的 *类基*、*类型参数约束子句* 和 *类体*。
  
  > 注意：与类的成员不同，此作用域不扩展到派生类。注释结束
- 由结构声明（§16.2）上的类型参数列表所声明的类型参数，其作用域是该结构声明的结构接口、类型参数约束子句和结构体。
- 由接口声明（§18.2）上的类型参数列表所声明的类型参数，其作用域是该接口声明的接口基、类型参数约束子句和接口体。
- 由委托声明（§20.2）上的类型参数列表所声明的类型参数，其作用域是该委托声明的返回类型、形参列表和类型参数约束子句。
- 由方法声明（§15.6.1）上的类型参数列表所声明的类型参数，其作用域是该方法声明。
- 由类成员声明（§15.3.1）所声明的成员，其作用域是声明所在的类体。此外，类成员的作用域扩展到那些包含在该成员可访问域（§7.5.3）中的派生类的类体。
- 由结构成员声明（§16.3）所声明的成员，其作用域是声明所在的结构体。
- 由枚举成员声明（§19.4）所声明的成员，其作用域是声明所在的枚举体。
- 在方法声明（§15.6）中声明的参数，其作用域是该方法声明的方法体或 ref 方法体。
- 在索引器声明（§15.9）中声明的参数，其作用域是该索引器声明的索引器体。
- 在运算符声明（§15.10）中声明的参数，其作用域是该运算符声明的运算符体。
- 在构造函数声明（§15.11）中声明的参数，其作用域是该构造函数声明的构造函数初始化器和块。
- 在 lambda 表达式（§12.19）中声明的参数，其作用域是该 lambda 表达式的 lambda 表达式体。
- 在匿名方法表达式（§12.19）中声明的参数，其作用域是该匿名方法表达式的块。
- 在带标签语句（§13.5）中声明的标签，其作用域是声明所在的块。
- 在局部变量声明（§13.6.2）中声明的局部变量，其作用域是声明所在的块。
- 在 switch 语句（§13.8.3）的 switch 块中声明的局部变量，其作用域是该 switch 块。
- 在 for 语句（§13.9.4）的 for 初始化器中声明的局部变量，其作用域是该 for 语句的 for 初始化器、for 条件、for 迭代器和嵌入语句。
- 在局部常量声明（§13.6.3）中声明的局部常量，其作用域是声明所在的块。在文本位置位于其常量声明符之前引用局部常量，是编译时错误。




- 作为 *foreach 语句*、*using 语句*、*lock 语句* 或 *查询表达式* 的一部分声明的变量的作用域，由给定构造的展开决定。

在命名空间、类、结构或枚举成员的作用域内，可以在文本位置上先于该成员的声明引用该成员。

*示例：*

```csharp
class A
{
    void F()
    {
        i = 1;
    }
    int i = 0;
}
```

此处，F 在 i 声明之前引用 i 是合法的。

*示例结束*

在局部变量的作用域内，在文本位置上先于其声明符引用该局部变量会导致编译时错误。

*示例：*

```csharp
class A
{
    int i = 0;
    void F()
    {
        i = 1;            // Error, use precedes declaration
        int i;
        i = 2;
    }
    void G()
    {
        int j = (j = 1);  // Valid
    }
    void H()
    {
        int a = 1, b = ++a; // Valid
    }
}
```

在上述 F 方法中，对 i 的第一个赋值明确不是引用外部作用域中声明的字段。相反，它引用的是局部变量，并且由于它在文本位置上先于该变量的声明，因此会导致编译时错误。在 G 方法中，在声明 j 的初始化器中对 j 的使用是合法的，因为该使用不先于声明符。在 H 方法中，后续的声明符正确地引用了同一 local_variable_declaration 中先前声明符所声明的局部变量。

*示例结束*

注意：局部变量和局部常量的作用域规则旨在保证在表达式上下文中使用的名称在块内的含义始终相同。如果局部变量的作用域仅从其声明延伸到块的末尾，那么在上面的示例中，第一个赋值将赋给实例变量，而第二个赋值将赋给局部变量，如果块中的语句稍后被重新排列，则可能导致编译时错误。）

块内名称的含义可能因使用该名称的上下文而异。在示例

```csharp
class A {}

class Test
{
    static void Main()
    {
        string A = "hello, world";
        string s = A;    // expression context
        Type t = typeof(A);    // type context
        Console.WriteLine(s);    // writes "hello, world"
        Console.WriteLine(t);    // writes "A"
    }
}
```

中，名称 A 在表达式上下文中用于引用局部变量 A，而在类型上下文中用于引用类 A。

注意结束

## 7.7.2 名称隐藏

### 7.7.2.1 概述

实体的作用域通常包含比实体的声明空间更多的程序文本。

特别是，实体的作用域可能包含一些声明，这些声明引入了包含同名实体的新声明空间。此类声明会导致原始实体被隐藏。相反，当实体未被隐藏时，称该实体是可见的。

当作用域通过嵌套重叠以及通过继承重叠时，就会发生名称隐藏。以下小节描述了这两种隐藏类型的特征。

### 7.7.2.2 通过嵌套隐藏

通过嵌套进行的名称隐藏可能由以下原因引起：在命名空间内嵌套命名空间或类型，在类或结构内嵌套类型，以及参数、局部变量和局部常量的声明。

示例：在下面的代码中

```csharp
class A
{
    int i = 0;
    void F()
    {
        int i = 1;
    }
    void G()
    {
        i = 1;
    }
}
```

在 F 方法中，实例变量 i 被局部变量 i 隐藏，但在 G 方法中，i 仍然引用实例变量。

示例结束

当内层作用域中的名称隐藏外层作用域中的名称时，它会隐藏该名称的所有重载形式。

示例：在下面的代码中

```csharp
class Outer
{
    static void F(int i) {}
    static void F(string s) {}

    class Inner
    {
        static void F(long l) {}

        void G()
        {
            F(1); // Invokes Outer.Inner.F
            F("Hello"); // Error
        }
    }
}
```

调用 F(1) 会调用在 Inner 中声明的 F，因为所有外部出现的 F 都被内部声明隐藏。出于同样的原因，调用 F("Hello") 会导致编译时错误。

示例结束

### 7.7.2.3 通过继承隐藏

当类或结构重新声明从基类继承的名称时，就会发生通过继承进行的名称隐藏。这种类型的名称隐藏采用以下形式之一：

- 在类或结构中引入的常量、字段、属性、事件或类型会隐藏基类中所有同名成员。
- 在类或结构中引入的方法会隐藏基类中所有同名的非方法成员，以及所有具有相同签名（§7.6）的基类方法。
- 在类或结构中引入的索引器会隐藏基类中所有具有相同签名（§7.6）的索引器。

管理运算符声明（§15.10）的规则使得派生类不可能声明与基类中运算符具有相同签名的运算符。因此，运算符永远不会相互隐藏。

与隐藏外部作用域中的名称不同，隐藏来自继承作用域的可见名称会报告警告。

示例：在下面的代码中

```csharp
class Base
{
    public void F() {}
}
class Derived : Base
{
    public void F() {} // Warning, hiding an inherited name
}
```

Derived 中 F 的声明会导致报告警告。隐藏继承的名称明确不视为错误，因为这将妨碍基类的独立演化。例如，上述情况可能是因为 Base 的后续版本引入了早期版本中不存在的 F 方法而出现的。

示例结束

通过使用 new 修饰符可以消除由隐藏继承名称引起的警告：

示例：

```csharp
class Base
{
    public void F() {}
}
class Derived : Base
{
    public new void F() {}
}
```

new 修饰符表示 Derived 中的 F 是"新的"，并且它确实旨在隐藏继承的成员。

示例结束

新成员的声明仅在新成员的作用域内隐藏继承的成员。

示例：

```csharp
class Base
{
    public static void F() {}
}
class Derived : Base
{
    private new static void F() {} // Hides Base.F in Derived only
}
class MoreDerived : Derived
{
    static void G()
    {
        F();            // Invokes Base.F
    }
}
```

在上面的示例中，Derived 中 F 的声明隐藏了从 Base 继承的 F，但由于 Derived 中新的 F 具有私有访问权限，其作用域不会扩展到 MoreDerived。因此，MoreDerived.G 中的调用 F() 是合法的，并将调用 Base.F。

*示例结束*

## 7.8 命名空间和类型名称

### 7.8.1 概述

C# 程序中的若干上下文要求指定 namespace_name 或 type_name。

```
namespace_name
  : namespace_or_type_name
  ;

type_name
  : namespace_or_type_name
  ;

namespace_or_type_name
  : identifier type_argument_list?
  | namespace_or_type_name '.' identifier type_argument_list?
  | qualified_alias_member
  ;
```

namespace_name 是引用命名空间的 namespace_or_type_name。

按照下文所述的解析，namespace_name 的 namespace_or_type_name 必须引用命名空间，否则将发生编译时错误。namespace_name 中不能包含类型实参（§8.4.2）（只有类型才能具有类型实参）。

type_name 是引用类型的 namespace_or_type_name。按照下文所述的解析，type_name 的 namespace_or_type_name 必须引用类型，否则将发生编译时错误。

如果 namespace_or_type_name 是 qualified_alias_member，则其含义如 §14.8.1 所述。否则，namespace_or_type_name 具有以下四种形式之一：

- `I`
- `I<A₁, ..., Aₓ>`
- `N.I`
- `N.I<A₁, ..., Aₓ>`

其中 I 是单个标识符，N 是 namespace_or_type_name，<A₁, ..., Aₓ> 是可选的 type_argument_list。当未指定 type_argument_list 时，将 x 视为零。

namespace_or_type_name 的含义按如下方式确定：

- 如果 namespace_or_type_name 是 qualified_alias_member，则其含义如 §14.8.1 所规定。
- 否则，如果 namespace_or_type_name 的形式为 I 或 I<A₁, ..., Aₓ>：
  - 如果 x 为零，且 namespace_or_type_name 出现在泛型方法声明（§15.6）中但在其方法头的特性之外，并且该声明包含一个类型

参数 (§15.2.3) 的名称为 I，则命名空间或类型名引用该类型参数。

- 否则，如果命名空间或类型名出现在类型声明中，则对于每个实例类型 T (§15.3.2)，从该类型声明的实例类型开始，继续每个封闭的类或结构声明（如果有）的实例类型：
  - 如果 x 为零且 T 的声明包含名称为 I 的类型参数，则命名空间或类型名引用该类型参数。
  - 否则，如果命名空间或类型名出现在类型声明的主体中，且 T 或其任何基类型包含名称为 I 且有 x 个类型参数的嵌套可访问类型，则命名空间或类型名引用使用给定类型参数构造的该类型。如果存在多个此类类型，则选择在更派生的类型中声明的类型。
  - 注意：非类型成员（常量、字段、方法、属性、索引器、运算符、实例构造函数、终结器和静态构造函数）以及类型参数数量不同的类型成员在确定命名空间或类型名的含义时将被忽略。 end note
- 否则，对于每个命名空间 N，从命名空间或类型名出现的命名空间开始，继续每个封闭的命名空间（如果有），并以全局命名空间结束，以下步骤将被评估直到找到一个实体：
  - 如果 x 为零且 I 是 N 中的命名空间的名称，则：
    - 如果命名空间或类型名出现的位置被 N 的命名空间声明所包含，并且该命名空间声明包含将名称 I 与命名空间或类型关联的 extern_alias_directive 或 using_alias_directive，则命名空间或类型名不明确且会发生编译时错误。
    - 否则，命名空间或类型名引用 N 中名为 I 的命名空间。
  - 否则，如果 N 包含名称为 I 且有 x 个类型参数的可访问类型，则：
    - 如果 x 为零且命名空间或类型名出现的位置被 N 的命名空间声明所包含，并且该命名空间声明包含将名称 I 与命名空间或类型关联的 extern_alias_directive 或 using_alias_directive，则命名空间或类型名不明确且会发生编译时错误。
    - 否则，命名空间或类型名引用使用给定类型参数构造的类型。
  - 否则，如果命名空间或类型名出现的位置被 N 的命名空间声明所包含：
    - 如果 x 为零且命名空间声明包含将名称 I 与导入的命名空间或类型关联的 extern_alias_directive 或 using_alias_directive，则命名空间或类型名引用该命名空间或类型。
    - 否则，如果命名空间声明的 using_namespace_directives 导入的命名空间恰好包含一个名称为 I 且有 x 个类型参数的类型，则命名空间或类型名引用使用给定类型参数构造的该类型。
- 否则，如果命名空间声明的 using_namespace_directives 导入的命名空间包含多个名称为 I 且有 x 个类型参数的类型，则命名空间或类型名不明确且会发生错误。
- 否则，命名空间或类型名未定义且会发生编译时错误。
- 否则，命名空间或类型名的形式为 N.I 或 N.I<A1, ..., Ax>。N 首先作为命名空间或类型名解析。如果 N 的解析不成功，则会发生编译时错误。否则，N.I 或 N.I<A1, ..., Ax> 按如下方式解析：
  - 如果 x 为零且 N 引用一个命名空间并且 N 包含名称为 I 的嵌套命名空间，则命名空间或类型名引用该嵌套命名空间。
  - 否则，如果 N 引用一个命名空间并且 N 包含名称为 I 且有 x 个类型参数的可访问类型，则命名空间或类型名引用使用给定类型参数构造的该类型。
  - 否则，如果 N 引用一个（可能已构造的）类或结构类型并且 N 或其任何基类包含名称为 I 且有 x 个类型参数的嵌套可访问类型，则命名空间或类型名引用使用给定类型参数构造的该类型。如果存在多个此类类型，则选择在更派生的类型中声明的类型。注意：如果 N.I 的含义是在解析 N 的基类规范的过程中确定的，则 N 的直接基类被视为 object (§15.2.4.2)。 end note
  - 否则，N.I 是无效的命名空间或类型名，且会发生编译时错误。

命名空间或类型名仅在以下情况下允许引用静态类 (§15.2.2.4)：
- 命名空间或类型名是形式为 T.I 的命名空间或类型名中的 T，或
- 命名空间或类型名是形式为 typeof(T) 的 typeof 表达式 (§12.8.17) 中的 T

## 7.8.2 无限定名

每个命名空间声明和类型声明都有一个按如下方式确定的无限定名：
- 对于命名空间声明，无限定名是声明中指定的 qualified_identifier。
- 对于没有 type_parameter_list 的类型声明，无限定名是声明中指定的标识符。
- 对于具有 K 个类型参数的类型声明，无限定名是声明中指定的标识符，后跟 K 个类型参数的 generic_dimension_specifier (§12.8.17)。

## 7.8.3 完全限定名

每个命名空间和类型声明都有一个完全限定名，该名称在程序中唯一标识该命名空间或类型声明。具有无限定名 N 的命名空间或类型声明的完全限定名按如下方式确定：
- 如果 N 是全局命名空间的成员，则其完全限定名为 N。
- 否则，其完全限定名为 S.N，其中 S 是声明 N 的命名空间或类型声明的完全限定名。

换句话说，N 的完全限定名是从全局命名空间开始导致 N 的标识符和 generic_dimension_specifier 的完整层次路径。因为命名空间或类型的每个成员都必须具有唯一名称，所以命名空间或类型声明的完全限定名始终是唯一的。相同的完全限定名引用两个不同实体是编译时错误。特别地：
- 命名空间声明和类型声明具有相同的完全限定名是错误。
- 两种不同类型的类型声明具有相同的完全限定名是错误（例如，如果 struct 和 class 声明具有相同的完全限定名）。
- 没有 partial 修饰符的类型声明与另一个类型声明具有相同的完全限定名是错误 (§15.2.7)。

示例：下面的示例显示了几个命名空间和类型声明以及它们关联的完全限定名。

```
class A {}              // A
namespace X              // X
{
    class B              // X.B
    {
        class C {}       // X.B.C
    }
    namespace Y          // X.Y
    {
        class D {}       // X.Y.D
    }
}
namespace X.Y            // X.Y
{
    class E {}           // X.Y.E
    class G<T>           // X.Y.G<>
    {
        class H {}       // X.Y.G<>.H
    }
    class G<S,T>         // X.Y.G<,>
    {
        class H<U> {}    // X.Y.G<,>.H<>
    }
}
```
结束示例

## 7.9 自动内存管理

C# 采用自动内存管理，使开发人员无需手动分配和释放对象占用的内存。自动内存管理策略由垃圾回收器实现。对象的内存管理生命周期如下：
- 1. 当对象被创建时，为其分配内存，运行构造函数，并且对象被视为存活。
- 2. 如果对象或其任何实例字段无法通过执行的任何可能延续访问（除运行终结器外），则对象被视为不再使用并且成为可终结的对象。

*注意：* C# 编译器和垃圾回收器可能会选择分析代码以确定对对象的哪些引用将来可能会被使用。例如，如果作用域内的局部变量是


该局部变量是对象的唯一现有引用，但该局部变量在从过程当前执行点开始的任何可能执行继续中都不再被引用，则垃圾回收器可能（但并非必须）将该对象视为不再使用。注释结束

- 3. 一旦对象符合终结条件，在稍后某个未指定的时间，该对象的终结器（§15.13）（如果有的话）将被运行。在正常情况下，对象的终结器只运行一次，但实现特定的 API 可能允许覆盖此行为。
- 4. 一旦对象的终结器运行完毕，如果无法通过任何可能的执行继续（包括终结器的运行）访问该对象或其任何实例字段，则该对象被视为不可访问，并符合回收条件。
  - 注意：以前无法访问的对象可能会由于其终结器而变得再次可访问。下面提供了一个示例。注释结束
- 5. 最后，在对象符合回收条件之后的某个时间，垃圾回收器释放与该对象关联的内存。

垃圾回收器维护有关对象使用的信息，并利用这些信息做出内存管理决策，例如在内存中的何处放置新创建的对象、何时重定位对象，以及对象何时不再使用或不可访问。

与其他假定存在垃圾回收器的语言一样，C# 的设计允许垃圾回收器实现广泛的内存管理策略。C# 既没有规定这个时间跨度内的时间约束，也没有规定终结器的运行顺序。终结器是否作为应用程序终止的一部分运行是实现特定的（§7.2）。

垃圾回收器的行为在一定程度上可以通过 System.GC 类上的静态方法来控制。该类可用于请求执行回收、运行（或不运行）终结器等。

示例：由于垃圾回收器在决定何时回收对象和运行终结器方面拥有很大的自由度，符合规范的实现可能会产生与以下代码所示不同的输出。该程序

```csharp
class A
{
    ~A()
    {
        Console.WriteLine("Finalize instance of A");
    }
}

class B
{
    object Ref;
    public B(object o)
    {
        Ref = o;
    }

    ~B()
    {
        Console.WriteLine("Finalize instance of B");
    }
}
```

```csharp
class Test
{
    static void Main()
    {
        B b = new B(new A());
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

上述代码创建了类 A 的一个实例和类 B 的一个实例。当变量 b 被赋值为 null 时，这些对象符合垃圾回收条件，因为在此之后，任何用户编写的代码都不可能再访问它们。输出可能是

Finalize instance of A
Finalize instance of B

或

Finalize instance of B
Finalize instance of A

因为该语言对对象的垃圾回收顺序没有任何限制。

在一些微妙的情况下，“符合终结条件”和“符合回收条件”之间的区别可能很重要。例如，

```csharp
class A
{
    ~A()
    {
        Console.WriteLine("Finalize instance of A");
    }

    public void F()
    {
        Console.WriteLine("A.F");
        Test.RefA = this;
    }
}

class B
{
    public A Ref;

    ~B()
    {
        Console.WriteLine("Finalize instance of B");
        Ref.F();
    }
}

class Test
{
    public static A RefA;
    public static B RefB;
```

```csharp
static void Main()
{
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
    {
        Console.WriteLine("RefA is not null");
    }
}
```

在上述程序中，如果垃圾回收器选择在 B 的终结器之前运行 A 的终结器，则该程序的输出可能为：

```
Finalize instance of A
Finalize instance of B
A.F
RefA is not null
```

请注意，尽管 A 的实例已不再使用，并且 A 的终结器已运行，但仍然可以从另一个终结器调用 A 的方法（在本例中为 F）。此外，请注意，终结器的运行可能会使对象从主线程序中再次变为可用。在这种情况下，B 的终结器的运行使先前不再使用的 A 实例从活动引用 Test.RefA 变为可访问。在调用 WaitForPendingFinalizers 之后，B 的实例符合回收条件，但 A 的实例不符合，因为存在引用 Test.RefA。

示例结束

## 7.10 执行顺序

C# 程序的执行过程保证了每个执行线程的副作用在关键执行点被保留。副作用定义为对 volatile 字段的读取或写入、对非 volatile 变量的写入、对外部资源的写入以及异常的抛出。必须保留这些副作用顺序的关键执行点包括：对 volatile 字段的引用（§15.5.4）、lock 语句（§13.13）以及线程的创建和终止。执行环境可以自由更改 C# 程序的执行顺序，但须满足以下约束：

- 在线程执行内保留数据依赖性。也就是说，每个变量的值都像线程中的所有语句按原始程序顺序执行一样进行计算。
- 保留初始化排序规则（§15.5.5、§15.5.6）。
- 关于 volatile 读取和写入，保留副作用的顺序（§15.5.4）。此外，如果执行环境能够推断出表达式的值未被使用，且不会产生所需的副作用（包括由调用方法或访问 volatile 字段引起的任何副作用），则无需计算该表达式的部分内容。当程序执行被异步事件（例如另一个线程抛出的异常）中断时，不保证可观察的副作用按原始程序顺序可见。

# 8. 类型

### 8.1 概述

C# 语言的类型分为两大类别：*引用类型*和*值类型*。值类型和引用类型都可能是*泛型类型*，其带有一个或多个*类型参数*。类型参数既可以指示值类型，也可以指示引用类型。

```
type
  : reference_type
  | value_type
  | type_parameter
  | pointer_type    // unsafe code support
  ;
```

*pointer_type*（§23.3）仅在非安全代码（§23）中可用。

值类型与引用类型的区别在于，值类型的变量直接包含其数据，而引用类型的变量存储对其数据的*引用*，后者称为*对象*。对于引用类型，两个变量可能引用同一个对象，因此对一个变量执行的操作可能会影响另一个变量所引用的对象。对于值类型，每个变量都有自己的一份数据副本，对一个变量的操作不可能影响到另一个变量。

*注意：* 当变量是 ref 或 out 参数时，它没有自己的存储，而是引用另一个变量的存储。在这种情况下，ref 或 out 变量实际上是另一个变量的别名，而不是一个独立的变量。*注释结束*

C# 的类型系统是统一的，因此*任何类型的值都可以被视为对象*。C# 中的每种类型都直接或间接地派生自 *object* 类类型，而 *object* 是所有类型的最终基类。引用类型的值只需将其视为 *object* 类型即可视为对象。值类型的值通过执行装箱和拆箱操作（§8.3.13）被视为对象。

为方便起见，在整个规范中，某些库类型名称在书写时未使用其完全限定名称。更多信息请参阅 §C.5。

### 8.2 引用类型

### 8.2.1 概述

引用类型是类类型、接口类型、数组类型、委托类型或 *dynamic* 类型。

```
reference_type
  : class_type
  | interface_type
  | array_type
  | delegate_type
  | 'dynamic'
  ;
```

```
class_type
```




```
: type_name
| 'object'
| 'string'
;

interface_type
: type_name
;

array_type
: non_array_type rank_specifier+
;

non_array_type
: value_type
| class_type
| interface_type
| delegate_type
| 'dynamic'
| type_parameter
| pointer_type    // unsafe code support
;

rank_specifier
: '[' ','* ']'
;

delegate_type
: type_name
;
```

pointer_type 仅在不安全代码中可用 (§23.3)。

引用类型的值是对类型的实例的引用，后者称为对象。特殊值 null 与所有引用类型兼容，表示实例的缺失。

### 8.2.2 类类型

类类型定义一种数据结构，包含数据成员（常量和字段）、函数成员（方法、属性、事件、索引器、运算符、实例构造函数、终结器和静态构造函数）以及嵌套类型。类类型支持继承，该机制允许派生类扩展和特化基类。类类型的实例使用 object_creation_expressions (§12.8.16.2) 创建。

类类型在 §15 中描述。

某些预定义的类类型在 C# 语言中具有特殊含义，如下表所述。

| 类类型 | 描述 |
|---|---|
| System.Object | 所有其他类型的终极基类。参见 §8.2.3。 |
| System.String | C# 语言的字符串类型。参见 §8.2.5。 |
| System.ValueType | 所有值类型的基类。参见 §8.3.2。 |
| System.Enum | 所有枚举类型的基类。参见 §19.5。 |
| System.Array | 所有数组类型的基类。参见 §17.2.2。 |
| System.Delegate | 所有委托类型的基类。参见 §20.1。 |
| System.Exception | 所有异常类型的基类。参见 §21.3。 |

### 8.2.3 object 类型

`object` 类类型是所有其他类型的终极基类。C# 中的每个类型都直接或间接派生自 `object` 类类型。

关键字 `object` 只是预定义类 `System.Object` 的别名。

### 8.2.4 dynamic 类型

`dynamic` 类型与 `object` 类似，可以引用任何对象。当操作应用于 `dynamic` 类型的表达式时，其解析会延迟到程序运行时。因此，如果操作不能合法地应用于引用的对象，编译期间不会给出错误。相反，当操作在运行时解析失败时，将抛出异常。

`dynamic` 类型在 §8.7 中进一步描述，动态绑定在 §12.3.1 中。

### 8.2.5 string 类型

`string` 类型是一个密封的类类型，直接继承自 `object`。`string` 类的实例表示 Unicode 字符字符串。

`string` 类型的值可以作为字符串字面量 (§6.4.5.6) 编写。

关键字 `string` 只是预定义类 `System.String` 的别名。

### 8.2.6 接口类型

接口定义一个契约。实现接口的类或结构必须遵守其契约。接口可以继承多个基接口，类或结构可以实现多个接口。

接口类型在 §18 中描述。

### 8.2.7 数组类型

数组是一种数据结构，包含零个或多个变量，通过计算的索引访问。数组中包含的变量，也称为数组的元素，全部为同一类型，该类型称为数组的元素类型。

数组类型在 §17 中描述。

### 8.2.8 委托类型

委托是一种数据结构，引用一个或多个方法。对于实例方法，它还引用其对应的对象实例。

> 注：委托在 C 或 C++ 中最接近的等价物是函数指针，但函数指针只能引用静态函数，而委托可以引用静态和实例方法两种。在后一种情况下，委托不仅存储对方法入口点的引用，还存储对要调用该方法的对象实例的引用。结束注记

委托类型在 §20 中描述。

## 8.3 值类型

### 8.3.1 通用

值类型要么是结构类型，要么是枚举类型。C# 提供了一组预定义的结构类型，称为 *simple types*。简单类型通过关键字标识。

```
value_type
  : non_nullable_value_type
  | nullable_value_type
  ;

non_nullable_value_type
  : struct_type
  | enum_type
  ;

struct_type
  : type_name
  | simple_type
  | tuple_type
  ;

simple_type
  : numeric_type
  | 'bool'
  ;

numeric_type
  : integral_type
  | floating_point_type
  | 'decimal'
  ;

integral_type
  : 'sbyte'
  | 'byte'
  | 'short'
  | 'ushort'
  | 'int'
  | 'uint'
  | 'long'
  | 'ulong'
  | 'char'
  ;

floating_point_type
  : 'float'
  | 'double'
  ;

tuple_type
  : '(' tuple_type_element (',' tuple_type_element)+ ')'
  ;
```

```
tuple_type_element
  : type_identifier?
  ;

enum_type
  : type_name
  ;

nullable_value_type
  : non_nullable_value_type '?'
  ;
```

与引用类型变量不同，值类型变量仅在值类型为可空值类型 (§8.3.12) 时才能包含值 null。对于每个不可空值类型，都存在一个对应的可空值类型，表示相同的取值集合加上值 null。

向值类型变量赋值会创建所赋值的副本。这与向引用类型变量赋值不同，后者复制引用但不复制引用所标识的对象。

### 8.3.2 System.ValueType 类型

所有值类型都隐式继承自类 System.ValueType，而后者又继承自类 object。任何类型都不能从值类型派生，因此值类型是隐式密封的 (§15.2.2.3)。

请注意，System.ValueType 本身不是 value_type。而是所有 value_types 自动派生的 class_type。

### 8.3.3 默认构造函数

所有值类型都隐式声明一个名为默认构造函数的公共无参数实例构造函数。默认构造函数返回一个零初始化的实例，称为该值类型的默认值：

- 对于所有 simple_types，默认值是由全零位模式产生的值：
  - 对于 sbyte、byte、short、ushort、int、uint、long 和 ulong，默认值是 0。
  - 对于 char，默认值是 '\u0000'。
  - 对于 float，默认值是 0.0f。
  - 对于 double，默认值是 0.0d。
  - 对于 decimal，默认值是 0m（即值为零且比例为 0）。
  - 对于 bool，默认值是 false。
  - 对于 enum_type E，默认值是 0，转换为类型 E。
- 对于 struct_type，默认值是通过将所有值类型字段设置为其默认值并将所有引用类型字段设置为 null 而产生的值。
- 对于 nullable_value_type，默认值是一个 HasValue 属性为 false 的实例。默认值也称为可空值类型的空值。尝试读取此类值的 Value 属性会导致抛出类型为 System.InvalidOperationException 的异常 (§8.3.12)。

与任何其他实例构造函数一样，值类型的默认构造函数使用 new 运算符调用。

> 注：出于效率原因，此要求并不意味着实际让实现生成构造函数调用。对于值类型，默认值表达式 (§12.8.20) 产生的结果与使用默认构造函数相同。结束注记

示例：下面的代码中，变量 i、j 和 k 都初始化为零。

```
class A
{
    void F()
    {
        int i = 0;
        int j = new int();
        int k = default(int);
    }
}
```

结束示例

由于每个值类型都隐式具有公共无参数实例构造函数，因此结构类型不能包含无参数构造函数的显式声明。然而，结构类型允许声明带参数的实例构造函数 (§16.4.9)。

### 8.3.4 结构类型

结构类型是一种值类型，可以声明常量、字段、方法、属性、事件、索引器、运算符、实例构造函数、静态构造函数和嵌套类型。结构类型的声明在 §16 中描述。

### 8.3.5 简单类型

C# 提供了一组预定义的结构类型，称为简单类型。简单类型通过关键字标识，但这些关键字只是 System 命名空间中预定义结构类型的别名，如下表所述。

| 关键字 | 别名类型 |
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

由于简单类型为结构类型提供别名，所以每个简单类型都具有成员。

示例：int 具有在 System.Int32 中声明的成员以及从 System.Object 继承的成员，并且允许以下语句：

```
int i = int.MaxValue;    // System.Int32.MaxValue constant
string s = i.ToString();    // System.Int32.ToString() instance method
string t = 123.ToString(); // System.Int32.ToString() instance method
```

示例结束

注意：简单类型与其他结构类型的不同之处在于，它们允许某些附加操作：

-   大多数简单类型允许通过书写字面量来创建值（§6.4.5），尽管 C# 通常不为结构类型提供字面量。示例：123 是 int 类型的字面量，'a' 是 char 类型的字面量。示例结束
-   当表达式的操作数全部为简单类型常量时，编译器可以在编译时对该表达式求值。这种表达式称为 constant_expression（§12.23）。涉及由其他结构类型定义的运算符的表达式不被视为常量表达式。
-   通过 const 声明，可以声明简单类型的常量（§15.4）。无法具有其他结构类型的常量，但 static readonly 字段可提供类似效果。
-   涉及简单类型的转换可以参与由其他结构类型定义的转换运算符的求值，但用户定义的转换运算符永远不能参与另一个用户定义的转换运算符的求值（§10.5.3）。

注意结束。

## 8.3.6 整型

C# 支持九种整型：sbyte、byte、short、ushort、int、uint、long、ulong 和 char。整型具有以下大小和值范围：

-   sbyte 类型表示有符号 8 位整数，值范围为 -128 到 127（含端点）。
-   byte 类型表示无符号 8 位整数，值范围为 0 到 255（含端点）。
-   short 类型表示有符号 16 位整数，值范围为 -32768 到 32767（含端点）。
-   ushort 类型表示无符号 16 位整数，值范围为 0 到 65535（含端点）。
-   int 类型表示有符号 32 位整数，值范围为 -2147483648 到 2147483647（含端点）。
-   uint 类型表示无符号 32 位整数，值范围为 0 到 4294967295（含端点）。
-   long 类型表示有符号 64 位整数，值范围为 -9223372036854775808 到 9223372036854775807（含端点）。
-   ulong 类型表示无符号 64 位整数，值范围为 0 到 18446744073709551615（含端点）。
-   char 类型表示无符号 16 位整数，值范围为 0 到 65535（含端点）。char 类型的可能值集合对应于 Unicode 字符集。

注意：尽管 char 与 ushort 具有相同的表示形式，但并非允许对一种类型执行的所有操作都允许对另一种类型执行。注意结束。

所有有符号整型都使用二进制补码格式表示。

integral_type 的一元和二元运算符始终以有符号 32 位精度、无符号 32 位精度、有符号 64 位精度或无符号 64 位精度运算，详见 §12.4.7。

char 类型被归类为整型，但它在两个方面与其他整型不同：

-   不存在从其他类型到 char 类型的预定义隐式转换。特别是，即使 byte 和 ushort 类型的值范围完全可以用 char 类型表示，也不存在从 sbyte、byte 或 ushort 到 char 的隐式转换。
-   char 类型的常量应写为 character_literals，或写为 integer_literals 与到 char 类型的强制转换的组合。

示例：(char)10 与 '\x000A' 相同。示例结束

checked 和 unchecked 运算符及语句用于控制整型算术运算和转换的溢出检查（§12.8.19）。在 checked 上下文中，溢出会产生编译时错误，或导致引发 System.OverflowException。在 unchecked 上下文中，溢出会被忽略，任何不适合目标类型的高位都会被丢弃。

## 8.3.7 浮点类型

C# 支持两种浮点类型：float 和 double。float 和 double 类型使用 32 位单精度和 64 位双精度 IEC 60559 格式表示，这些格式提供以下值集合：

-   正零和负零。在大多数情况下，正零和负零的行为与简单值零相同，但某些操作会区分二者（§12.10.3）。
-   正无穷大和负无穷大。无穷大由非零数除以零等操作产生。示例：1.0 / 0.0 产生正无穷大，-1.0 / 0.0 产生负无穷大。示例结束
-   非数字值，通常缩写为 NaN。NaN 由无效的浮点运算（例如零除以零）产生。
-   形式为 s × m × 2^e 的非零值的有限集合，其中 s 为 1 或 -1，m 和 e 由特定浮点类型决定：对于 float，0 < m < 2^24 且 -149 ≤ e ≤ 104；对于 double，0 < m < 2^53 且 -1075 ≤ e ≤ 970。非规格化浮点数被视为有效的非零值。C# 既不要求也不禁止符合规范的实现支持非规格化浮点数。

float 类型可表示大约从 1.5 × 10^-45 到 3.4 × 10^38 的值，精度为 7 位数字。

double 类型可表示大约从 5.0 × 10^-324 到 1.7 × 10^308 的值，精度为 15-16 位数字。

如果二元运算符的任一操作数为浮点类型，则应用标准数值提升（详见 §12.4.7），并使用 float 或 double 精度执行运算。

浮点运算符（包括赋值运算符）从不产生异常。相反，在异常情况下，浮点运算会产生零、无穷大或 NaN，如下所述：

-   浮点运算的结果会舍入为目标格式中最接近的可表示值。
-   如果浮点运算结果的量值对于目标格式而言太小，则运算结果变为正零或负零。
-   如果浮点运算结果的量值对于目标格式而言太大，则运算结果变为正无穷大或负无穷大。
-   如果浮点运算无效，则运算结果变为 NaN。
-   如果浮点运算的一个或两个操作数为 NaN，则运算结果变为 NaN。

浮点运算可以用高于该运算结果类型的精度执行。要强制浮点类型的值达到其类型的精确精度，可以使用显式强制转换（§12.9.7）。

示例：某些硬件体系结构支持一种“扩展”或“long double”浮点类型，其范围和精度均大于 double 类型，并隐式使用这种更高精度的类型执行所有浮点运算。只有付出过高的性能代价，才能让此类硬件体系结构以较低精度执行浮点运算；C# 不要求实现牺牲性能和精度，而是允许对所有浮点运算使用更高精度的类型。除了提供更精确的结果之外，这很少产生任何可测量的影响。然而，在形式为 x * y / z 的表达式中，如果乘法产生的结果超出 double 范围，但随后的除法使临时结果回到 double 范围内，那么该表达式以更高范围格式求值这一事实可能导致产生有限结果而不是无穷大。示例结束

## 8.3.8 decimal 类型

decimal 类型是一种 128 位数据类型，适用于财务和货币计算。decimal 类型可以表示至少从 -7.9 × 10⁻²⁸ 到 7.9 × 10²⁸ 范围内的值，且至少具有 28 位数字的精度。

decimal 类型的有限值集合采用 (-1)^v × c × 10⁻ᵉ 的形式，其中符号 v 为 0 或 1，系数 c 满足 0 ≤ c < Cmax，缩放因子 e 满足 Emin ≤ e ≤ Emax；其中 Cmax 至少为 1 × 10²⁸，Emin ≤ 0，且 Emax ≥ 28。decimal 类型不一定支持有符号零、无穷大或 NaN。



会舍入到最接近的可表示值；并且，当结果与两个可表示值同样接近时，舍入到最低有效数字位上为偶数的那个值（这称为“银行家舍入法”）。也就是说，结果至少精确到小数点后第 28 位。注意，舍入可能会从非零值产生零值。

如果 `decimal` 算术运算产生的结果其量级对于 `decimal` 格式来说过大，则会引发 `System.OverflowException`。

`decimal` 类型具有更高的精度，但范围可能比浮点类型更小。因此，从浮点类型到 `decimal` 的转换可能会产生溢出异常，而从 `decimal` 到浮点类型的转换可能会导致精度损失或溢出异常。由于这些原因，浮点类型与 `decimal` 之间不存在隐式转换；如果没有显式强制转换，当浮点操作数和 `decimal` 操作数在同一表达式中直接混合时，会发生编译时错误。

### 8.3.9 bool 类型

`bool` 类型表示布尔逻辑量。`bool` 类型的可能值为 `true` 和 `false`。`false` 的表示形式在 §8.3.3 中描述。尽管 `true` 的表示形式未指定，但它应与 `false` 的表示形式不同。

`bool` 与其他值类型之间不存在标准转换。特别地，`bool` 类型与整型截然不同且相互分离，`bool` 值不能用于代替整型值，反之亦然。

> 注意：在 C 和 C++ 语言中，零值整型或浮点值，或空指针，可以转换为布尔值 `false`；非零整型或浮点值，或非空指针，可以转换为布尔值 `true`。在 C# 中，此类转换通过将整型或浮点值与零进行显式比较，或将对象引用与 `null` 进行显式比较来完成。结束注

### 8.3.10 枚举类型

枚举类型是一种带命名常量的独特类型。每个枚举类型都有一个基础类型，该类型应为 `byte`、`sbyte`、`short`、`ushort`、`int`、`uint`、`long` 或 `ulong`。枚举类型的值集与基础类型的值集相同。枚举类型的值不限于命名常量的值。枚举类型通过枚举声明（§19.2）定义。

### 8.3.11 元组类型

元组类型表示一个有序的固定长度值序列，其中的值具有可选名称和单独类型。元组类型中元素的数量称为其元数。元组类型写作 (T1 I1, ..., Tn In)，其中 n ≥ 2，标识符 I1...In 是可选的元组元素名称。此语法是用 `System.ValueTuple<...>` 中的类型 T1...Tn 构造的类型的简写；`System.ValueTuple<...>` 应是一组泛型结构类型，能够直接表达元数在 2 到 7（含两端）之间的任何元组类型。不需要存在一个 `System.ValueTuple<...>` 声明，使其直接匹配任何元组类型的元数并具有相应数量的类型参数。相反，元数大于 7 的元组用泛型结构类型 `System.ValueTuple<T1, ..., T7, TRest>` 表示，该类型除元组元素外还具有一个 `Rest` 字段，其中包含其余元素的嵌套值，并使用另一个 `System.ValueTuple<...>` 类型。这种嵌套可以通过各种方式观察到，例如通过 `Rest` 字段的存在。在只需要一个额外字段的情况下，泛型结构类型

可空值类型。可空值类型的基础类型不能是可空值类型或引用类型。例如，`int??` 和 `string?` 是无效类型。

可空值类型 `T?` 的实例具有两个公共只读属性：

- 类型为 `bool` 的 `HasValue` 属性
- 类型为 `T` 的 `Value` 属性

`HasValue` 为 `true` 的实例称为非 null。非 null 实例包含一个已知值，`Value` 返回该值。

`HasValue` 为 `false` 的实例称为 null。null 实例具有未定义的值。尝试读取 null 实例的 `Value` 会导致引发 `System.InvalidOperationException`。访问可空实例的 Value 属性的过程称为*解包*。

除默认构造函数外，每个可空值类型 `T?` 都有一个公共构造函数，其单个参数的类型为 `T`。给定类型为 `T` 的值 `x`，以下形式的构造函数调用

```
new T?(x)
```

会创建 `T?` 的非 null 实例，其 `Value` 属性为 `x`。为给定值创建可空值类型的非 null 实例的过程称为*包装*。

存在从 `null` 字面量到 `T?` 的隐式转换（§10.2.7），以及从 `T` 到 `T?` 的隐式转换（§10.2.6）。

可空类型 `T?` 不实现任何接口（§18）。特别地，这意味着它不实现基础类型 `T` 所实现的任何接口。

### 8.3.13 装箱和拆箱

装箱和拆箱的概念通过在 *值类型* 和 *引用类型* 之间提供桥梁，允许任何 *值类型* 的值与类型 `object` 相互转换。装箱和拆箱使得类型系统具有统一视图，其中任何类型的值最终都可以当作 `object` 处理。

装箱在 §10.2.9 中更详细地描述，拆箱在 §10.3.7 中描述。

## 8.4 构造类型

### 8.4.1 概述

泛型类型声明本身表示一个*未绑定泛型类型*，它用作“蓝图”，通过应用*类型实参*来形成许多不同的类型。类型实参写在尖括号（`<` 和 `>`）内，紧跟泛型类型的名称之后。包含至少一个类型实参的类型称为*构造类型*。构造类型可用于语言中大多数可以出现类型名称的位置。未绑定泛型类型只能在 *typeof_expression*（§12.8.17）内使用。

构造类型也可以在表达式中用作简单名称（§12.8.4），或在访问成员时使用（§12.8.7）。

当对 *namespace_or_type_name* 求值时，只考虑具有正确数量类型参数的泛型类型。因此，只要类型具有不同数量的类型参数，就可以使用同一标识符来标识不同的类型。当在同一程序中混合泛型和非泛型类时，这很有用。

示例：

```
namespace Widgets
{
    class Queue {...}
    class Queue<TElement> {...}
}

namespace MyApplication
{
    using Widgets;

    class X
    {
        Queue q1;    // Non-generic Widgets.Queue
        Queue<int> q2; // Generic Widgets.Queue
    }
}
```

示例结束

`namespace_or_type_name` 产生式中名称查找的详细规则在 §7.8 中描述。这些产生式中歧义的消解在 §6.2.5 中描述。`type_name` 可能标识一个构造类型，即使它没有直接指定类型参数。当类型嵌套在泛型类声明中，并且包含声明的实例类型被隐式用于名称查找时（§15.3.9.7），就可能发生这种情况。

示例：

```
class Outer<T>
{
    public class Inner {...}

    public Inner i; // Type of i is Outer<T>.Inner
}
```

示例结束

非枚举构造类型不得用作 unmanaged_type（§8.8）。

### 8.4.2 类型实参

类型实参列表中的每个实参都只是一个类型。

```
type_argument_list
    : '<' type_arguments '>'
    ;

type_arguments
    : type_argument (',' type_argument)*
    ;

type_argument
    : type
    ;
```

每个类型实参应满足对应类型参数的任何约束（§15.2.5）。

### 8.4.3 开放类型和封闭类型

所有类型都可以分类为开放类型或封闭类型。开放类型是涉及类型参数的类型。更具体地说：

- 类型参数定义开放类型。
- 数组类型是开放类型，当且仅当其元素类型是开放类型。
- 构造类型是开放类型，当且仅当其一个或多个类型实参是开放类型。构造嵌套类型是开放类型，当且仅当其一个或多个类型实参或其包含类型的一个或多个类型实参是开放类型。

封闭类型是非开放类型。

在运行时，泛型类型声明内的所有代码都在封闭构造类型的上下文中执行，该封闭构造类型是通过将类型实参应用于泛型声明而创建的。泛型类型内的每个类型参数都绑定到特定的运行时类型。所有语句和表达式的运行时处理始终在封闭类型下发生，而开放类型仅出现在编译时处理期间。

每个封闭构造类型都有自己的静态变量集，这些静态变量不与任何其他封闭构造类型共享。由于开放类型在运行时不存在，因此没有与开放类型关联的静态变量。如果两个封闭构造类型由同一未绑定泛型类型构造，并且它们对应的类型实参是相同类型，则它们是相同类型。

### 8.4.4 绑定类型和未绑定类型

术语“未绑定类型”指非泛型类型或未绑定泛型类型。术语“绑定类型”指非泛型类型或构造类型。

未绑定类型指由类型声明所声明的实体。未绑定泛型类型本身不是类型，不能用作变量、参数或返回值的类型，也不能用作基类型。可以引用未绑定泛型类型的唯一构造是 typeof 表达式（§12.8.17）。

### 8.4.5 满足约束

每当引用构造类型或泛型方法时，都会将提供的类型实参对照泛型类型或方法上声明的类型参数约束进行检查（§15.2.5）。对于每个 where 子句，与命名类型参数对应的类型实参 A 都会按如下方式对照每个约束进行检查：

- 如果约束是类类型、接口类型或类型参数，则令 C 表示该约束，并用提供的类型实参替换约束中出现的任何类型参数。为满足该约束，类型 A 应能通过以下方式之一转换为类型 C：
  - 恒等转换（§10.2.2）
  - 隐式引用转换（§10.2.8）
  - 装箱转换（§10.2.9），前提是类型 A 是不可空值类型。
  - 从类型参数 A 到 C 的隐式引用转换、装箱转换或类型参数转换。
- 如果约束是引用类型约束（class），则类型 A 应满足以下之一：

- A 是接口类型、类类型、委托类型、数组类型或 dynamic 类型。
  *注意：System.ValueType 和 System.Enum 是满足此约束的引用类型。结束注意*
- A 是一个已知为引用类型的类型参数（§8.2）。
- 如果约束是值类型约束（`struct`），则类型 A 必须满足以下其中之一：
  - A 是 `struct` 类型或 `enum` 类型，但不是可空值类型。
    *注意：System.ValueType 和 System.Enum 是不满足此约束的引用类型。结束注意*
  - A 是一个具有值类型约束的类型参数（§15.2.5）。
- 如果约束是构造函数约束 `new()`，则类型 A 不应为 `abstract` 且应具有公共无参构造函数。当以下任一条件为真时即满足：
  - A 是值类型，因为所有值类型都有公共默认构造函数（§8.3.3）。
  - A 是一个具有构造函数约束的类型参数（§15.2.5）。
  - A 是一个具有值类型约束的类型参数（§15.2.5）。
  - A 是非抽象的 `class` 且包含一个显式声明的公共无参数构造函数。
  - A 不是 `abstract` 且具有 `default` 构造函数（§15.11.5）。

如果一个或多个类型参数的约束未被给定的类型参数满足，则会发生编译时错误。

由于类型参数不会被继承，因此约束也不会被继承。

示例：在下面，D 需要为其类型参数 T 指定约束，以便 T 满足基类 B<T> 施加的约束。相比之下，类 E 无需指定约束，因为 List<T> 对任何 T 都实现了 IEnumerable。

```
class B<T> where T: IEnumerable {...}
class D<T> : B<T> where T: IEnumerable {...}
class E<T> : B<List<T>> {...}
```

结束示例

## 8.5 类型参数

类型参数是标识符，表示在运行时参数绑定到的值类型或引用类型。

```
type_parameter
  : identifier
  ;
```

由于类型参数可以用许多不同的类型参数实例化，因此类型参数与其他类型相比具有略有不同的操作和限制。

注意：包括以下内容：
- 类型参数不能直接用于声明基类（§15.2.4.2）或接口（§18.2.4）。
- 对类型参数的成员查找规则取决于应用于该类型参数的约束（如果有）。详见 §12.5。
- 类型参数可用的转换取决于应用于该类型参数的约束（如果有）。详见 §10.2.12 和 §10.3.9。
- 字面量 null 不能转换为类型参数给出的类型，除非类型参数已知为引用类型（§10.2.12）。然而，可以改用默认值表达式（§12.8.20）代替。此外，具有类型参数给出类型的值可以使用 == 和 != 与 null 进行比较（§12.12.7），除非类型参数具有值类型约束。
- new 表达式（§12.8.16.2）只能与类型参数一起使用，如果该类型参数受构造函数约束或值类型约束约束（§15.2.5）。
- 类型参数不能在属性的任何位置使用。
- 类型参数不能在成员访问（§12.8.7）或类型名称（§7.8）中使用来标识静态成员或嵌套类型。
- 类型参数不能用作 unmanaged_type（§8.8）。
  结束注意

作为一种类型，类型参数纯粹是编译时构造。在运行时，每个类型参数都绑定到通过向泛型类型声明提供类型参数而指定的运行时类型。因此，用类型参数声明的变量的类型在运行时将是闭合构造类型 §8.4.3。涉及类型参数的所有语句和表达式的运行时执行使用为该参数提供的类型参数作为类型。

## 8.6 表达式树类型

**表达式树** 允许将 lambda 表达式表示为数据结构而不是可执行代码。表达式树是 **表达式树类型** 的值，其形式为 `System.Linq.Expressions.Expression<TDelegate>`，其中 `TDelegate` 是任何委托类型。在本规范的其余部分中，这些类型将使用简写 `Expression<TDelegate>` 引用。

如果存在从 lambda 表达式到委托类型 D 的转换，则也存在到表达式树类型 `Expression<TDelegate>` 的转换。而将 lambda 表达式转换为委托类型会生成一个引用 lambda 表达式可执行代码的委托，将其转换为表达式树类型会创建 lambda 表达式的表达式树表示。有关此转换的更多细节在 §10.7.3 中提供。

*示例：* 以下程序将 lambda 表达式同时表示为可执行代码和表达式树。由于存在到 `Func<int,int>` 的转换，因此也存在到 `Expression<Func<int,int>>` 的转换：

```
Func<int,int> del = x => x + 1;   // Code
Expression<Func<int,int>> exp = x => x + 1; // Data
```

执行这些赋值后，委托 del 引用一个返回 x + 1 的方法，而表达式树 exp 引用一个描述表达式 x => x + 1 的数据结构。

*结束示例*

- 当用 `object` 替换 `dynamic` 时相同的签名被视为相同签名。
- 类型 `dynamic` 在运行时与 `object` 不可区分。
- `dynamic` 类型的表达式被称为 *动态表达式*。

## 8.8 未托管类型

```
unmanaged_type
  : value_type
  | pointer_type    // unsafe code support
  ;
```

*unmanaged_type* 是任何不是 *reference_type*、*type_parameter* 或构造类型的类型，并且不包含类型不是 *unmanaged_type* 的实例字段。换句话说，*unmanaged_type* 是以下之一：

- `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double`、`decimal` 或 `bool`。
- 任何 `enum_type`。
- 任何用户定义的 `struct_type`，它不是构造类型并且仅包含 *unmanaged_types* 的实例字段

# 9. 变量

### 9.1 通用

变量表示存储位置。每个变量都有一个类型，该类型决定可以存储在变量中的值。C# 是一种类型安全的语言，C# 编译器保证存储在变量中的值始终是适当的类型。变量的值可以通过赋值或使用 ++ 和 -- 运算符来更改。

在获取变量的值之前，变量必须已 *明确赋值*（§9.4）。

如以下小节所述，变量要么是 *初始已赋值* 要么是 *初始未赋值*。初始已赋值的变量具有明确定义的初始值，并且始终被认为已明确赋值。初始未赋值的变量没有初始值。对于初始未赋值的变量，要在某个位置被视为已明确赋值，必须在通向该位置的每条可能的执行路径中对该变量进行赋值。

### 9.2 变量类别

### 9.2.1 通用

C# 定义了八个变量类别：静态变量、实例变量、数组元素、值参数、输入参数、引用参数、输出参数和局部变量。以下小节描述了这些类别中的每一个。

*示例：* 在以下代码中

```
class A
{
    public static int x;
    int y;

    void F(int[] v, int a, ref int b, out int c, in int d)
    {
        int i = 1;
        c = a + b++ + d;
    }
}
```

x 是静态变量，y 是实例变量，v[0] 是数组元素，a 是值参数，b 是引用参数，c 是输出参数，d 是输入参数，i 是局部变量。*结束示例*

### 9.2.2 静态变量

使用 *static* 修饰符声明的字段是静态变量。静态变量在包含类型的 *static* 构造函数（§15.12）执行之前存在，并在关联的应用程序域停止存在时停止存在。

静态变量的初始值是变量类型默认值（§9.3）。




为了确定性赋值检查的目的，静态变量被视为已初始赋值。

## 9.2.3 实例变量

### 9.2.3.1 一般

未声明 static 修饰符的字段是实例变量。

### 9.2.3.2 类中的实例变量

类的实例变量在创建该类的新实例时开始存在，并在对该实例没有任何引用且实例的终结器（如果有）已执行时停止存在。

类实例变量的初始值是变量类型默认值 (§9.3)。

为了确定性赋值检查的目的，类的实例变量被视为已初始赋值。

### 9.2.3.3 结构体中的实例变量

结构体的实例变量与所属的结构体变量具有完全相同的生命周期。换句话说，当结构体类型的变量开始存在或停止存在时，其实例变量也同样如此。

结构体实例变量的初始赋值状态与包含它的结构体变量相同。换句话说，当结构体变量被视为已初始赋值时，其实例变量也被视为已初始赋值；当结构体变量被视为初始未赋值时，其实例变量也同样未赋值。

## 9.2.4 数组元素

数组的元素在创建数组实例时开始存在，并在对该数组实例没有任何引用时停止存在。

数组每个元素的初始值是数组元素类型默认值 (§9.3)。

为了确定性赋值检查的目的，数组元素被视为已初始赋值。

## 9.2.5 值参数

未声明 in、out 或 ref 修饰符的参数是值参数。

值参数在调用其所属的函数成员（方法、实例构造函数、访问器或运算符）或匿名函数时开始存在，并使用调用中给出的参数值进行初始化。值参数通常在函数体执行完成时停止存在。然而，如果值参数被匿名函数捕获 (§12.19.6.2)，其生命周期至少会延长到从该匿名函数创建的委托或表达式树有资格进行垃圾回收为止。

为了确定性赋值检查的目的，值参数被视为已初始赋值。

## 9.2.6 引用参数

声明了 ref 修饰符的参数是引用参数。

引用参数是引用变量 (§9.7)，它在调用函数成员、委托、匿名函数或局部函数时开始存在，其引用对象被初始化为该调用中作为参数给出的变量。引用参数在函数体执行完成时停止存在。与值参数不同，引用参数不能被捕获 (§9.7.2.9)。

以下确定性赋值规则适用于引用参数。

注意：输出参数的规则不同，描述在 (§9.2.7)。结束注意

- 在函数成员或委托调用中将变量作为引用参数传递之前，该变量必须已确定性赋值 (§9.4)。
- 在函数成员或匿名函数内部，引用参数被视为已初始赋值。

对于结构体类型，在实例方法或实例访问器 (§12.2.1) 或带构造函数初始值设定项的实例构造函数内部，this 关键字完全表现得像结构体类型的引用参数 (§12.8.13)。

## 9.2.7 输出参数

声明了 out 修饰符的参数是输出参数。

输出参数是引用变量 (§9.7)，它在调用函数成员、委托、匿名函数或局部函数时开始存在，其引用对象被初始化为该调用中作为参数给出的变量。输出参数在函数体执行完成时停止存在。与值参数不同，输出参数不能被捕获 (§9.7.2.9)。

以下确定性赋值规则适用于输出参数。

注意：引用参数的规则不同，描述在 (§9.2.6)。结束注意

- 在函数成员或委托调用中将变量作为输出参数传递之前，该变量不必已确定性赋值。
- 在函数成员或委托调用正常完成之后，在该执行路径中，作为输出参数传递的每个变量都被视为已赋值。
- 在函数成员或匿名函数内部，输出参数被视为初始未赋值。
- 函数成员、匿名函数或局部函数的每个输出参数在函数成员、匿名函数或局部函数正常返回之前必须已确定性赋值 (§9.4)。

## 9.2.8 输入参数

声明了 in 修饰符的参数是输入参数。

输入参数是引用变量 (§9.7)，它在调用函数成员、委托、匿名函数或局部函数时开始存在，其引用对象被初始化为该调用中作为参数给出的 variable_reference。输入参数在函数体执行完成时停止存在。与值参数不同，输入参数不能被捕获 (§9.7.2.9)。

以下确定赋值规则适用于输入参数。

- 在函数成员或委托调用中将变量作为输入参数传递之前，该变量必须已确定性赋值 (§9.4)。
- 在函数成员、匿名函数或局部函数内部，输入参数被视为已初始赋值。

## 9.2.9 局部变量

局部变量由 local_variable_declaration、declaration_expression、foreach_statement 或 try_statement 的 specific_catch_clause 声明。局部变量也可以由某些类型的模式 (§11) 声明。对于 foreach_statement，局部变量是迭代变量 (§13.9.5)。对于 specific_catch_clause，局部变量是异常变量 (§13.11)。由 foreach_statement 或 specific_catch_clause 声明的局部变量被视为已初始赋值。

local_variable_declaration 可以出现在块、for_statement、switch_block 或 using_statement 中。declaration_expression 可以作为 out argument_value 出现，并作为解构赋值的目标的 tuple_element (§12.21.2)。

局部变量的生命周期是程序执行期间为其保证保留存储的部分。该生命周期从进入其关联的作用域开始，至少持续到该作用域以某种方式结束为止。（进入封闭块、调用方法或从迭代器块产生值会暂停，但不会结束当前作用域的执行。）如果局部变量被匿名函数捕获 (§12.19.6.2)，其生命周期至少会延长到从匿名函数创建的委托或表达式树以及任何引用捕获变量的其他对象有资格进行垃圾回收为止。如果父作用域被递归或迭代进入，每次都会创建局部变量的新实例，并且其初始值设定项（如果有）每次都会被求值。

> 注意：每次进入其作用域时都会实例化局部变量。这种行为对包含匿名方法的用户代码可见。结束注意

> 注意：由 foreach_statement 声明的迭代变量 (§13.9.5) 的生命周期是该语句的一次迭代。每次迭代都会创建一个新变量。结束注意

> 注意：局部变量的实际生命周期取决于实现。例如，编译器可能会静态确定块中的局部变量仅在该块的一小部分中使用。利用此分析，编译器可以生成代码，导致变量的存储生命周期短于其包含的块。
> 
> 局部引用变量所引用的存储与该局部引用变量的生命周期独立回收 (§7.9)。
> 
> 结束注意

由 local_variable_declaration 或 declaration_expression 引入的局部变量不会自动初始化，因此没有默认值。此类局部变量被视为初始未赋值。

注意：包含初始值设定项的 local_variable_declaration 仍然是初始未赋值。声明的执行与对变量的赋值 (§9.4.4.5) 完全相同。在其初始值设定项执行之前使用变量；例如，在初始值设定项表达式本身内部或通过使用绕过初始值设定项的 goto_statement；是编译时错误：

```
goto L;
int x = 1; // never executed
L: x += 1; // error: x not definitely assigned
```

在局部变量的作用域内，在文本位置早于其声明符处引用该局部变量是编译时错误。



### 9.2.9.1 弃元

*弃元*是一种没有名称的局部变量。弃元由带标识符 `_` 的声明表达式（§12.17）引入，并且要么是隐式类型化的（`_` 或 `var _`），要么是显式类型化的（`T _`）。

*注意：* 在许多形式的声明中，`_` 是有效标识符。 *结束注释*

由于弃元没有名称，因此对它所表示变量的唯一引用就是引入它的表达式。

*注意：* 然而，弃元可以作为 out 实参传递，从而允许 out 参数表示其关联的存储位置。 *结束注释*

弃元初始未赋值，因此访问其值始终是错误。

*示例：*

```
_ = "Hello".Length;
(int, int, int) M(out int i1, out int i2, out int i3) { ... }
(int _, var _, _) = M(out int _, out var _, out _);
```

该示例假定作用域中没有名称 `_` 的声明。

对 `_` 的赋值展示了一种忽略表达式结果的简单模式。对 *M* 的调用展示了元组中以及作为 out 参数时可用的不同弃元形式。

*示例结束*

## 9.3 默认值

以下类别的变量会自动初始化为其*默认*值：

- 静态变量。
- 类实例的实例变量。
- 数组元素。

变量的*默认*值取决于该变量的类型，并按如下方式确定：

- 对于*值类型*的变量，*默认*值与*值类型*的默认构造函数（§8.3.3）计算出的值相同。
- 对于*引用类型*的变量，*默认*值是 *null*。

*注意：* 初始化为默认值通常是由内存管理器或垃圾回收器在分配内存供使用之前将内存初始化为全零位来完成的。因此，用全零位表示 null 引用很方便。 *结束注释*

## 9.4 明确赋值

### 9.4.1 概述

在函数成员或匿名函数的可执行代码中的给定位置，如果编译器能够通过特定的静态流分析（§9.4.4）证明该变量已被自动初始化，或者已成为至少一次赋值的目标，则称该变量为*明确赋值*。

*注意：非正式地说，明确赋值的规则如下：*

- 初始已赋值的变量（§9.4.2）始终被视为明确赋值。
- 如果在到达给定位置的所有可能执行路径中至少包含以下一项，则初始未赋值的变量（§9.4.3）在该给定位置被视为明确赋值：
  - 一个简单赋值（§12.21.2），其中该变量是左操作数。
  - 一个调用表达式（§12.8.9）或对象创建表达式（§12.8.16.2），它将变量作为输出参数传递。
  - 对于局部变量，包含变量初始值设定项的该变量的局部变量声明（§13.6.2）。

上述非正式规则所依据的正式规范在 §9.4.2、§9.4.3 和 §9.4.4 中描述。

*结束注释*

对于*结构类型*变量，其各实例变量的明确赋值状态既单独跟踪，也整体跟踪。除上述规则外，以下规则适用于*结构类型*变量及其实例变量：

- 如果包含某实例变量的*结构类型*变量被视为明确赋值，则该实例变量被视为明确赋值。
- 如果*结构类型*变量的每个实例变量都被视为明确赋值，则该*结构类型*变量被视为明确赋值。

明确赋值在以下上下文中是一项要求：

- 在获取变量值的每个位置，该变量都应明确赋值。
  *注意：这确保永远不会出现未定义的值。结束注释*
  变量在表达式中的出现被视为获取该变量的值，但以下情况除外：
  - 该变量是简单赋值的左操作数；
  - 该变量作为输出参数传递；或
  - 该变量是*结构类型*变量，并作为成员访问的左操作数出现。
- 在将变量作为引用参数传递的每个位置，该变量都应明确赋值。
  *注意：这确保被调用的函数成员可以将引用参数视为初始已赋值。结束注释*
- 在将变量作为输入参数传递的每个位置，该变量都应明确赋值。
  *注意：这确保被调用的函数成员可以将输入参数视为初始已赋值。结束注释*
- 函数成员的所有输出参数在该函数成员返回的每个位置（通过 return 语句，或通过执行到达函数成员主体末尾）都应明确赋值。
  *注意：这确保函数成员不会在输出参数中返回未定义的值，从而使编译器能够将把变量作为输出参数的函数成员调用视为对该变量的赋值。结束注释*
- `struct_type` 实例构造函数的 `this` 变量在该实例构造函数返回的每个位置都应明确赋值。

### 9.4.2 初始已赋值的变量

以下类别的变量被归类为*初始已赋值*：

- 静态变量。
- 类*实例*的实例变量。
- *初始已赋值*结构变量的实例变量。
- 数组元素。
- 值参数。
- 引用参数。
- 输入参数。
- 在 `catch` 子句或 `foreach` 语句中声明的变量。

### 9.4.3 初始未赋值的变量

以下类别的变量被归类为*初始未赋值*：

- 初始未赋值结构变量的实例变量。
- 输出参数，包括没有构造函数初始值设定项的结构实例构造函数的 `this` 变量。
- 局部变量，但在 `catch` 子句或 `foreach` 语句中声明的变量除外。

### 9.4.4 确定明确赋值的精确规则

### 9.4.4.1 概述

为了确定每个被使用的变量都是*明确赋值*，编译器应使用与本子条款所述过程等效的过程。

编译器处理具有一个或多个初始未赋值变量的每个函数成员的主体。对于每个初始未赋值变量 *v*，编译器在函数成员中的以下每个点确定 *v* 的*明确赋值状态*：

- 在每个语句的开头
- 在每个语句的结束点（§13.2）
- 在将控制转移到另一语句或语句结束点的每条弧上
- 在每个表达式的开头
- 在每个表达式的末尾

*v* 的明确赋值状态可以是以下之一：

- 明确赋值。这表示在到达此点的所有可能控制流上，*v* 都已赋了值。
- 未明确赋值。对于 `bool` 类型表达式末尾处的变量状态，未明确赋值的变量状态可能（但不一定）属于以下子状态之一：
  - 在 true 表达式之后明确赋值。此状态表示如果布尔表达式的计算结果为 true，则 v 明确赋值；但如果布尔表达式的计算结果为 false，则 v 不一定赋值。
  - 在 false 表达式之后明确赋值。此状态表示如果布尔表达式的计算结果为 false，则 v 明确赋值；但如果布尔表达式的计算结果为 true，则 v 不一定赋值。

以下规则规定如何确定变量 v 在每个位置的状态。

### 9.4.4.2 语句的一般规则

- 在函数成员主体的开头，v 未明确赋值。
- 对于任何其他语句，v 在该语句开头处的明确赋值状态通过检查所有以该语句开头为目标控制流转移上 v 的明确赋值状态来确定。当且仅当 v 在所有此类控制流转移上均明确赋值时，v 在该语句开头处才明确赋值。可能的控制流转移集合的确定方式与检查语句可达性（§13.2）相同。
- 对于块语句、checked 语句、unchecked 语句、if 语句、while 语句、do 语句、for 语句、foreach 语句、lock 语句、using 语句或 switch 语句，v 在该语句结束点处的明确赋值状态通过检查所有以该语句结束点为目标控制流转移上 v 的明确赋值状态来确定。如果 v 在所有此类控制流转移上均明确赋值，则 v 在该语句结束点处明确赋值。否则，v 在该语句结束点处未明确赋值。可能的控制流转移集合的确定方式与检查语句可达性（§13.2）相同。

*注意：* 由于不存在通向不可达语句的控制路径，因此 v 在任何不可达语句的开头处都明确赋值。 *结束注释*

### 9.4.4.3 块语句、checked 语句和 unchecked 语句

在控制转移到块中语句列表的第一条语句（如果语句列表为空，则转移到块的结束点）时，v 的明确赋值状态与在该块语句、checked 语句或 unchecked 语句之前 v 的明确赋值状态相同。

### 9.4.4.4 表达式语句

对于由表达式 expr 组成的表达式语句 stmt：

- v 在 expr 开头处的明确赋值状态与在 stmt 开头处相同。
- 如果 v 在 expr 末尾处明确赋值，则它在 stmt 结束点处明确赋值；否则，它在 stmt 结束点处未明确赋值。

### 9.4.4.5 声明语句

- 如果 stmt 是没有初始值设定项的声明语句，则 v 在 stmt 结束点处的明确赋值状态与在 stmt 开头处相同。
- 如果 stmt 是带初始值设定项的声明语句，则 v 的明确赋值状态的确定方式就好像 stmt 是一个语句列表，其中每个带初始值设定项的声明对应一个赋值语句（按声明顺序）。



## 9.4.4.6 if 语句

对于形式如下的语句 stmt：

```
if ( «expr» ) «then_stmt» else «else_stmt»
```

- *v* 在 *expr* 开始处的确定赋值状态与在 *stmt* 开始处的相同。
- 如果 *v* 在 *expr* 结束处已确定赋值，则它在控制流转移到 *then_stmt* 时已确定赋值，并且在控制流转移到 *else_stmt* 时也已确定赋值；如果没有 else 子句，则在控制流转移到 *stmt* 的终结点时也已确定赋值。
- 如果 *v* 在 *expr* 结束处具有“真表达式后已确定赋值”状态，则它在控制流转移到 *then_stmt* 时已确定赋值，而在控制流转移到 *else_stmt* 时未确定赋值；如果没有 else 子句，则在控制流转移到 *stmt* 的终结点时也未确定赋值。
- 如果 *v* 在 *expr* 结束处具有“假表达式后已确定赋值”状态，则它在控制流转移到 *else_stmt* 时已确定赋值，而在控制流转移到 *then_stmt* 时未确定赋值。它在 *stmt* 的终结点处已确定赋值，当且仅当它在 *then_stmt* 的终结点处已确定赋值。
- 否则，*v* 被视为在控制流转移到 *then_stmt* 或 *else_stmt* 时未确定赋值；如果没有 else 子句，则在控制流转移到 *stmt* 的终结点时也未确定赋值。

## 9.4.4.7 switch 语句

对于具有控制表达式 expr 的 switch 语句 stmt：

v 在 expr 开始处的确定赋值状态与 v 在 stmt 开始处的状态相同。

v 在 case 的保护子句开始处的确定赋值状态为

- 如果 v 是在 switch_label 中声明的模式变量，则为“已确定赋值”。
- 如果包含该保护子句的 switch 标签（§13.8.3）不可到达，则为“已确定赋值”。
- 否则，v 的状态与 v 在 expr 之后的状态相同。

v 在控制流转移到可到达的 switch 块语句列表时的确定赋值状态为

- 如果控制转移是由于 'goto case' 或 'goto default' 语句，则 v 的状态与该 'goto' 语句开始处的状态相同。
- 如果控制转移是由于 switch 的 default 标签，则 v 的状态与 v 在 expr 之后的状态相同。
- 如果控制转移是由于不可到达的 switch 标签，则 v 的状态为“已确定赋值”。
- 如果控制转移是由于带保护子句的可到达 switch 标签，则 v 的状态与 v 在保护子句之后的状态相同。
- 如果控制转移是由于不带保护子句的可到达 switch 标签，则 v 的状态为
  - 如果 v 是在 switch_label 中声明的模式变量，则为“已确定赋值”。
  - 否则，v 的状态与 v 在 expr 之后的状态相同。

这些规则的一个推论是：如果某个在 switch_label 中声明的模式变量不是其节中唯一可到达的 switch 标签，则该变量在其 switch 节的语句中将处于“未确定赋值”状态。

示例：

```
public static double ComputeArea(object shape)
{
    switch (shape)
    {
        case Square s when s.Side == 0:
        case Circle c when c.Radius == 0:
        case Triangle t when t.Base == 0 || t.Height == 0:
        case Rectangle r when r.Length == 0 || r.Height == 0:
            // none of s, c, t, or r is definitely assigned
            return 0;
        case Square s:
            // s is definitely assigned
            return s.Side * s.Side;
        case Circle c:
            // c is definitely assigned
            return c.Radius * c.Radius * Math.PI;
        ...
    }
}
```

示例结束

## 9.4.4.8 while 语句

对于形式如下的语句 stmt：

```
while ( «expr» ) «while_body»
```

- v 在 expr 开始处的确定赋值状态与在 stmt 开始处的相同。
- 如果 v 在 expr 结束处已确定赋值，则它在控制流转移到 while_body 时已确定赋值，并且在控制流转移到 stmt 的终结点时也已确定赋值。
- 如果 v 在 expr 结束处具有“真表达式后已确定赋值”状态，则它在控制流转移到 while_body 时已确定赋值，但在 stmt 的终结点处未确定赋值。
- 如果 v 在 expr 结束处具有“假表达式后已确定赋值”状态，则它在控制流转移到 stmt 的终结点时已确定赋值，但在控制流转移到 while_body 时未确定赋值。

## 9.4.4.9 do 语句

对于形式如下的语句 stmt：

```
do «do_body» while ( «expr» ) ;
```

- v 在控制流从 stmt 开始处转移到 do_body 时的确定赋值状态与在 stmt 开始处的相同。
- v 在 expr 开始处的确定赋值状态与在 do_body 终结点处的相同。
- 如果 v 在 expr 结束处已确定赋值，则它在控制流转移到 stmt 的终结点时已确定赋值。
- 如果 v 在 expr 结束处具有“假表达式后已确定赋值”状态，则它在控制流转移到 stmt 的终结点时已确定赋值，但在控制流转移到 do_body 时未确定赋值。

### 9.4.4.10 for 语句

对于形式如下的语句：

```
for ( «for_initializer» ; «for_condition» ; «for_iterator» )
    «embedded_statement»
```

确定赋值检查按如下方式执行，就好像该语句写成：

```
{
    «for_initializer» ;
    while ( «for_condition» )
    {
        «embedded_statement» ;
        LLoop: «for_iterator» ;
    }
}
```

其中，以 `for` 语句为目标的 `continue` 语句被转换为以标签 `LLoop` 为目标的 `goto` 语句。如果 `for` 语句中省略了 `for_condition`，则确定赋值求值按上述展开中将 `for_condition` 替换为 `true` 的方式继续。

### 9.4.4.11 break、continue 和 goto 语句

由 `break`、`continue` 或 `goto` 语句引起的控制流转移中，`v` 的确定赋值状态与该语句开始处 `v` 的确定赋值状态相同。

### 9.4.4.12 throw 语句

对于形式如下的语句 `stmt`：

```
throw «expr» ;
```

`v` 在 `expr` 开始处的确定赋值状态与 `v` 在 `stmt` 开始处的确定赋值状态相同。

### 9.4.4.13 return 语句

对于形式如下的语句 `stmt`：

```
return «expr» ;
```

- `v` 在 `expr` 开始处的确定赋值状态与 `v` 在 `stmt` 开始处的确定赋值状态相同。
- 如果 `v` 是输出参数，则它必须已确定赋值，满足以下任一条件：
  - 在 `expr` 之后
  - 或在包含该 `return` 语句的 `try-finally` 或 `try-catch-finally` 的 `finally` 块结束处。

对于形式如下的语句 `stmt`：

```
return ;
```

- 如果 `v` 是输出参数，则它必须已确定赋值，满足以下任一条件：
  - 在 `stmt` 之前
  - 或在包含该 `return` 语句的 `try-finally` 或 `try-catch-finally` 的 `finally` 块结束处。

## 9.4.4.14 try-catch 语句

对于形式如下的语句 stmt：

```
try «try_block»
catch ( ... ) «catch_block_1»
...
catch ( ... ) «catch_block_n»
```

- v 在 try_block 开始处的确定赋值状态与 v 在 stmt 开始处的确定赋值状态相同。
- v 在 catch_block_i（对于任意 i）开始处的确定赋值状态与 v 在 stmt 开始处的确定赋值状态相同。
- v 在 stmt 的终结点处已确定赋值，当且仅当 v 在 try_block 的终结点处以及每个 catch_block_i（对于从 1 到 n 的每个 i）的终结点处都已确定赋值。

## 9.4.4.15 try-finally 语句

对于形式如下的语句 stmt：

```
try «try_block» finally «finally_block»
```

- v 在 try_block 开始处的确定赋值状态与 v 在 stmt 开始处的确定赋值状态相同。
- v 在 finally_block 开始处的确定赋值状态与 v 在 stmt 开始处的确定赋值状态相同。
- v 在 stmt 的终结点处已确定赋值，当且仅当以下至少一项为真：
  - v 在 try_block 的终结点处已确定赋值
  - v 在 finally_block 的终结点处已确定赋值

如果发生从 try_block 内开始并在 try_block 外结束的控制流转移（例如 goto 语句），并且 v 在 finally_block 的终结点处已确定赋值，则在该控制流转移中 v 也被视为已确定赋值。（这不是“仅当”——如果 v 由于其他原因在该控制流转移中已确定赋值，则它仍被视为已确定赋值。）

## 9.4.4.16 try-catch-finally 语句

对于形式如下的语句 stmt：

```
try «try_block»
catch ( ... ) «catch_block_1»
...
catch ( ... ) «catch_block_n»
finally «finally_block»
```

确定赋值分析按如下方式执行，就好像该语句是包含 try-catch 语句的 try-finally 语句：

```
try
{
    try «try_block»
    catch ( ... ) «catch_block_1»
    ...
    catch ( ... ) «catch_block_n»
```




```
}

finally «finally_block»
```

*示例：* 下面的示例演示了 `try` 语句（§13.11）的不同代码块如何影响确定赋值。

```
class A
{
    static void F()
    {
        int i, j;
        try
        {
            goto LABEL;
            // neither i nor j definitely assigned
            i = 1;
            // i definitely assigned
        }
        catch
        {
            // neither i nor j definitely assigned
            i = 3;
            // i definitely assigned
        }
        finally
        {
            // neither i nor j definitely assigned
            j = 5;
            // j definitely assigned
        }
        // i and j definitely assigned
        LABEL: ;
        // j definitely assigned
    }
}
```

*示例结束*

## 9.4.4.17 foreach 语句

对于形式如下的语句 *stmt*：

```
foreach ( «type» «identifier» in «expr» ) «embedded_statement»
```

- 在 *expr* 开始处 *v* 的确定赋值状态与 *stmt* 开始处 *v* 的状态相同。
- 在控制流转移到 *embedded_statement* 或 *stmt* 的终点时，*v* 的确定赋值状态与 *expr* 结束处 *v* 的状态相同。

## 9.4.4.18 using 语句

对于形式如下的语句 *stmt*：

`using ( «resource_acquisition» ) «embedded_statement»`

- 在 *resource_acquisition* 开始处 *v* 的确定赋值状态与 *stmt* 开始处 *v* 的状态相同。
- 在控制流转移到 *embedded_statement* 时，*v* 的确定赋值状态与 *resource_acquisition* 结束处 *v* 的状态相同。

## 9.4.4.19 lock 语句

对于形式如下的语句 *stmt*：

```
lock ( «expr» ) «embedded_statement»
```

- 在 *expr* 开始处 *v* 的确定赋值状态与 *stmt* 开始处 *v* 的状态相同。
- 在控制流转移到 *embedded_statement* 时，*v* 的确定赋值状态与 *expr* 结束处 *v* 的状态相同。

## 9.4.4.20 yield 语句

对于形式如下的语句 *stmt*：

```
yield return «expr» ;
```

- 在 *expr* 开始处 *v* 的确定赋值状态与 *stmt* 开始处 *v* 的状态相同。
- 在 *stmt* 结束处 *v* 的确定赋值状态与 *expr* 结束处 *v* 的状态相同。

yield break 语句对确定赋值状态没有影响。

## 9.4.4.21 常量表达式的一般规则

以下规则适用于任何常量表达式，并且优先于后续章节中可能适用的任何规则：

对于值为 true 的常量表达式：

- 如果 *v* 在表达式之前已确定赋值，则 *v* 在表达式之后已确定赋值。
- 否则，*v* 在表达式之后为“在 false 表达式之后已确定赋值”。

示例：

```
int x;
if (true) {}
else
{
    Console.WriteLine(x);
}
```

示例结束

对于值为 false 的常量表达式：

- 如果 *v* 在表达式之前已确定赋值，则 *v* 在表达式之后已确定赋值。
- 否则，*v* 在表达式之后为“在 true 表达式之后已确定赋值”。

示例：

```
int x;
if (false)
{
    Console.WriteLine(x);
}
```

示例结束

对于所有其他常量表达式，*v* 在表达式之后的确定赋值状态与 *v* 在表达式之前的确定赋值状态相同。

## 9.4.4.22 简单表达式的一般规则

以下规则适用于这些种类的表达式：字面量（§12.8.2）、简单名称（§12.8.4）、成员访问表达式（§12.8.7）、非索引基访问表达式（§12.8.14）、typeof 表达式（§12.8.17）、默认值表达式（§12.8.20）、nameof 表达式（§12.8.22）和声明表达式（§12.17）。

- 此类表达式结束时 *v* 的确定赋值状态与表达式开始时 *v* 的确定赋值状态相同。

## 9.4.4.23 具有嵌入表达式的表达式的一般规则

以下规则适用于这些种类的表达式：带括号的表达式（§12.8.5）、元组表达式（§12.8.6）、元素访问表达式（§12.8.11）、带索引的基访问表达式（§12.8.14）、增量和减量表达式（§12.8.15、§12.9.6）、强制转换表达式（§12.9.7）、一元 +、-、*、/、%、<<、>>、<、<=、>、>=、==、!=、is、as、&、|、^ 表达式（§12.10、§12.11、§12.12、§12.13）、复合赋值表达式（§12.21.4）、checked 和 unchecked 表达式（§12.8.19）、数组和委托创建表达式（§12.8.16）以及 await 表达式（§12.9.8）。

这些表达式中的每一个都有一个或多个子表达式，这些子表达式按固定顺序无条件求值。

示例：二元 % 运算符先计算运算符左侧，再计算右侧。索引操作先计算被索引的表达式，然后按从左到右的顺序计算每个索引表达式。示例结束

对于具有子表达式 *expr1*、*expr2*、...、*exprn*（按此顺序计算）的表达式 *expr*：

- 在 *expr1* 开始处 *v* 的确定赋值状态与在 *expr* 开始处 *v* 的确定赋值状态相同。
- 在 *expr_i*（i 大于 1）开始处 *v* 的确定赋值状态与在 *expr_{i-1}* 结束处的确定赋值状态相同。
- 在 *expr* 结束处 *v* 的确定赋值状态与在 *expr_n* 结束处的确定赋值状态相同。

## 9.4.4.24 调用表达式和对象创建表达式

如果要调用的方法是没有任何实现分部方法声明的分部方法，或者是其调用被省略的条件方法（§22.5.3.2），则调用后 *v* 的确定赋值状态与调用前 *v* 的确定赋值状态相同。否则，以下规则适用。

对于形式如下的调用表达式 *expr*：

```
«primary_expression» ( «arg1», «arg2», ... , «argn» )
```

或形式如下的对象创建表达式 *expr*：

```
new «type» ( «arg1», «arg2», ... , «argn» )
```

- 对于调用表达式，*primary_expression* 之前 *v* 的确定赋值状态与 *expr* 之前 *v* 的状态相同。
- 对于调用表达式，*arg1* 之前 *v* 的确定赋值状态与 *primary_expression* 之后 *v* 的状态相同。
- 对于对象创建表达式，*arg1* 之前 *v* 的确定赋值状态与 *expr* 之前 *v* 的状态相同。
- 对于每个参数 *argi*，*v* 在 *argi* 之后的确定赋值状态由常规表达式规则确定，忽略任何 `in`、`out` 或 `ref` 修饰符。
- 对于每个参数 *argi*，对于任何大于 1 的 *i*，*v* 在 *argi* 之前的确定赋值状态与 *v* 在 *argi−1* 之后的状态相同。
- 如果变量 *v* 作为 `out` 参数（即形式为“out v”的参数）传递给任何一个参数，则 *expr* 之后 *v* 的状态为已确定赋值。否则，*expr* 之后 *v* 的状态与 *argN* 之后 *v* 的状态相同。
- 对于数组初始值设定项（§12.8.16.5）、对象初始值设定项（§12.8.16.3）、集合初始值设定项（§12.8.16.4）和匿名对象初始值设定项（§12.8.16.7），确定赋值状态由这些构造定义所依据的扩展来确定。

## 9.4.4.25 简单赋值表达式

设表达式 *e* 中的赋值目标集合定义如下：

- 如果 *e* 是元组表达式，则 *e* 中的赋值目标是 *e* 各元素的赋值目标的并集。
- 否则，*e* 中的赋值目标就是 *e*。

对于形式如下的表达式 *expr*：

```
«expr_lhs» = «expr_rhs»
```

- *expr_lhs* 之前 *v* 的确定赋值状态与 *expr* 之前 *v* 的确定赋值状态相同。
- *expr_rhs* 之前 *v* 的确定赋值状态与 *expr_lhs* 之后 *v* 的确定赋值状态相同。
- 如果 *v* 是 *expr_lhs* 的赋值目标，则 *expr* 之后 *v* 的确定赋值状态为已确定赋值。否则，如果赋值发生在结构类型的实例构造函数内部，且 *v* 是正在构造的实例上自动实现的属性 *P* 的隐藏后备字段，并且指定 *P* 的属性访问是 *expr_lhs* 的赋值目标，则 *expr* 之后 *v* 的确定赋值状态为已确定赋值。否则，*expr* 之后 *v* 的确定赋值状态与 *expr_rhs* 之后 *v* 的确定赋值状态相同。

*示例：* 在以下代码中

```
    class A
    {
        static void F(int[] arr)
        {
            int x;
            arr[x = 1] = x; // ok
        }
    }
```

变量 `x` 在 `arr[x = 1]` 作为第二个简单赋值的左侧被计算后，被视为已确定赋值。




示例结束

## 9.4.4.26 && 表达式

对于形式为的表达式 expr：

«expr_first» && «expr_second»

- 变量 v 在 expr_first 之前的确定赋值状态与变量 v 在 expr 之前的确定赋值状态相同。
- 变量 v 在 expr_second 之前的确定赋值状态当且仅当变量 v 在 expr_first 之后的状态为确定赋值或“在真表达式后确定赋值”时为确定赋值。否则，它不是确定赋值的。
- 变量 v 在 expr 之后的确定赋值状态由以下决定：
  - 如果变量 v 在 expr_first 之后的状态为确定赋值，则变量 v 在 expr 之后的状态为确定赋值。
  - 否则，如果变量 v 在 expr_second 之后的状态为确定赋值，且变量 v 在 expr_first 之后的状态为“在假表达式后确定赋值”，则变量 v 在 expr 之后的状态为确定赋值。
  - 否则，如果变量 v 在 expr_second 之后的状态为确定赋值或“在真表达式后确定赋值”，则变量 v 在 expr 之后的状态为“在真表达式后确定赋值”。
  - 否则，如果变量 v 在 expr_first 之后的状态为“在假表达式后确定赋值”，且变量 v 在 expr_second 之后的状态为“在假表达式后确定赋值”，则变量 v 在 expr 之后的状态为“在假表达式后确定赋值”。
  - 否则，变量 v 在 expr 之后的状态不是确定赋值的。

示例：在以下代码中

```
class A
{
  static void F(int x, int y)
  {
    int i;
    if (x >= 0 && (i = y) >= 0)
    {
      // i definitely assigned
    }
    else
    {
      // i not definitely assigned
    }
    // i not definitely assigned
  }
}
```

变量 i 在 if 语句的一个嵌入语句中被认为已确定赋值，而在另一个嵌入语句中则未被确定赋值。在方法 F 中的 if 语句中，变量 i 在第一个嵌入语句中已确定赋值，因为表达式 (i = y) 的执行总是先于该嵌入语句的执行。相反，变量 i 在第二个嵌入语句中未被确定赋值，因为 x >= 0 可能测试为假，导致变量 i 未被赋值。

示例结束

## 9.4.4.27 || 表达式

对于形式为的表达式 expr：

«expr_first» || «expr_second»

- 变量 v 在 expr_first 之前的确定赋值状态与变量 v 在 expr 之前的确定赋值状态相同。
- 变量 v 在 expr_second 之前的确定赋值状态当且仅当变量 v 在 expr_first 之后的状态为确定赋值或“在真表达式后确定赋值”时为确定赋值。否则，它不是确定赋值的。
- 变量 v 在 expr 之后的确定赋值状态由以下决定：
  - 如果变量 v 在 expr_first 之后的状态为确定赋值，则变量 v 在 expr 之后的状态为确定赋值。
  - 否则，如果变量 v 在 expr_second 之后的状态为确定赋值，且变量 v 在 expr_first 之后的状态为“在真表达式后确定赋值”，则变量 v 在 expr 之后的状态为确定赋值。
  - 否则，如果变量 v 在 expr_second 之后的状态为确定赋值或“在假表达式后确定赋值”，则变量 v 在 expr 之后的状态为“在假表达式后确定赋值”。
  - 否则，如果变量 v 在 expr_first 之后的状态为“在真表达式后确定赋值”，且变量 v 在 expr_second 之后的状态为“在真表达式后确定赋值”，则变量 v 在 expr 之后的状态为“在真表达式后确定赋值”。
  - 否则，变量 v 在 expr 之后的状态不是确定赋值的。

示例：在以下代码中

```
class A
{
    static void G(int x, int y)
    {
        int i;
        if (x >= 0 || (i = y) >= 0)
        {
            // i not definitely assigned
        }
        else
        {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```

变量 i 在 if 语句的一个嵌入语句中被认为已确定赋值，而在另一个嵌入语句中则未被确定赋值。在方法 G 中的 if 语句中，变量 i 在第二个嵌入语句中已确定赋值，因为表达式 (i = y) 的执行总是先于该嵌入语句的执行。相反，变量 i 在第一个嵌入语句中未被确定赋值，因为 x >= 0 可能测试为真，导致变量 i 未被赋值。

示例结束

## 9.4.4.28 ! 表达式

对于形式为的表达式 expr：

```
! «expr_operand»
```

- 变量 v 在 expr_operand 之前的确定赋值状态与变量 v 在 expr 之前的确定赋值状态相同。
- 变量 v 在 expr 之后的确定赋值状态由以下决定：
  - 如果变量 v 在 expr_operand 之后的状态为确定赋值，则变量 v 在 expr 之后的状态为确定赋值。
  - 否则，如果变量 v 在 expr_operand 之后的状态为“在假表达式后确定赋值”，则变量 v 在 expr 之后的状态为“在真表达式后确定赋值”。
  - 否则，如果变量 v 在 expr_operand 之后的状态为“在真表达式后确定赋值”，则变量 v 在 expr 之后的状态为“在假表达式后确定赋值”。
  - 否则，变量 v 在 expr 之后的状态不是确定赋值的。

## 9.4.4.29 ?? 表达式

对于形式为的表达式 expr：

```
«expr_first» ?? «expr_second»
```

- 变量 v 在 expr_first 之前的确定赋值状态与变量 v 在 expr 之前的确定赋值状态相同。
- 变量 v 在 expr_second 之前的确定赋值状态与变量 v 在 expr_first 之后的确定赋值状态相同。
- 变量 v 在 expr 之后的确定赋值状态由以下决定：
  - 如果 expr_first 是值为 null 的常量表达式 (§12.23)，则变量 v 在 expr 之后的状态与变量 v 在 expr_second 之后的状态相同。
  - 否则，变量 v 在 expr 之后的状态与变量 v 在 expr_first 之后的确定赋值状态相同。

## 9.4.4.30 ?: 表达式

对于形式为的表达式 expr：

```
«expr_cond» ? «expr_true» : «expr_false»
```

- 变量 v 在 expr_cond 之前的确定赋值状态与变量 v 在 expr 之前的状态相同。
- 如果变量 v 在 expr_cond 之后的状态为确定赋值或“在真表达式后确定赋值”，则变量 v 在 expr_true 之前的确定赋值状态为确定赋值。
- 如果变量 v 在 expr_cond 之后的状态为确定赋值或“在假表达式后确定赋值”，则变量 v 在 expr_false 之前的确定赋值状态为确定赋值。
- 变量 v 在 expr 之后的确定赋值状态由以下决定：
  - 如果 expr_cond 是值为 true 的常量表达式 (§12.23)，则变量 v 在 expr 之后的状态与变量 v 在 expr_true 之后的状态相同。
  - 否则，如果 expr_cond 是值为 false 的常量表达式 (§12.23)，则变量 v 在 expr 之后的状态与变量 v 在 expr_false 之后的状态相同。
  - 否则，如果变量 v 在 expr_true 之后的状态为确定赋值且变量 v 在 expr_false 之后的状态为确定赋值，则变量 v 在 expr 之后的状态为确定赋值。
  - 否则，变量 v 在 expr 之后的状态不是确定赋值的。

## 9.4.4.31 匿名函数

对于具有主体（块或表达式）body 的 lambda_expression 或 anonymous_method_expression expr：

- 参数的确定赋值状态与命名方法的参数相同 (§9.2.6, §9.2.7, §9.2.8)。
- 外部变量 v 在 body 之前的确定赋值状态与变量 v 在 expr 之前的状态相同。也就是说，外部变量的确定赋值状态从匿名函数的上下文继承而来。
- 外部变量 v 在 expr 之后的确定赋值状态与变量 v 在 expr 之前的状态相同。

示例：示例

```
class A
{
    delegate bool Filter(int i);
    void F()
    {
        int max;
        // Error, max is not definitely assigned
        Filter f = (int n) => n < max;
        max = 5;
        DoWork(f);
    }
    void DoWork(Filter f) { ... }
}
```

生成编译时错误，因为在声明匿名函数的位置 max 未被确定赋值。

示例结束

示例：示例

```
class A
{
    delegate void D();
    void F()
    {
        int n;
        D d = () => { n = 1; };
        d();
        // Error, n is not definitely assigned
        Console.WriteLine(n);
    }
}
```

还会生成编译时错误，因为匿名函数中对 n 的赋值不会影响匿名函数外部 n 的确定赋值状态。

示例结束

## 9.4.4.32 throw 表达式

对于形式如下的表达式 expr：

```
throw thrown_expr
```

- 在 thrown_expr 之前，v 的确定赋值状态与在 expr 之前 v 的状态相同。
- 在 expr 之后，v 的确定赋值状态为“已确定赋值”。

## 9.4.4.33 局部函数中变量的规则

局部函数在其父方法的上下文中分析。对局部函数而言，有两条重要的控制流路径：函数调用和委托转换。

每个局部函数主体的确定赋值针对每个调用点分别定义。在每次调用时，如果局部函数捕获的变量在调用点已确定赋值，则认为这些变量已确定赋值。此时还存在一条通往局部函数主体的控制流路径，并被视为可达。在调用局部函数之后，对于在离开函数的每个控制点（return 语句、yield 语句、await 表达式）都已确定赋值的捕获变量，在调用位置之后被视为已确定赋值。

委托转换存在一条通往局部函数主体的控制流路径。如果捕获变量在转换之前已确定赋值，则它们对于该主体而言已确定赋值。由局部函数赋值的变量在转换之后不被视为已赋值。

> 注意：上述内容意味着，在每次局部函数调用或委托转换时，都会重新分析主体以进行确定赋值。不要求编译器在每次调用或委托转换时重新分析局部函数的主体。实现必须产生与该描述等效的结果。注意结束

示例：以下示例演示局部函数中捕获变量的确定赋值。如果局部函数在写入捕获变量之前读取它，则必须在调用局部函数之前已确定赋值该捕获变量。局部函数 F1 读取 s 但不赋值。如果在 s 已确定赋值之前调用 F1，则这是一个错误。F2 在读取 i 之前赋值 i。可以在 i 已确定赋值之前调用 F2。此外，可以在 F2 之后调用 F3，因为 s2 在 F2 中已确定赋值。

```
```csharp
void M()
{
    string s;
    int i;
    string s2;

    // Error: Use of unassigned local variable s:
    F1();
    // OK, F2 assigns i before reading it.
    F2();

    // OK, i is definitely assigned in the body of F2:
    s = i.ToString();

    // OK. s is now definitely assigned.
}
```
```

```
F1();
// OK, F3 reads s2, which is definitely assigned in F2.
F3();

void F1()
{
    Console.WriteLine(s);
}

void F2()
{
    i = 5;
    // OK. i is definitely assigned.
    Console.WriteLine(i);
    s2 = i.ToString();
}

void F3()
{
    Console.WriteLine(s2);
}
```

示例结束

## 9.4.4.34 is 模式表达式

对于形式如下的表达式 expr：

```
expr_operand is pattern
```

- 在 expr_operand 之前，v 的确定赋值状态与在 expr 之前 v 的确定赋值状态相同。
- 如果变量 ‘v’ 在 pattern 中声明，则在 expr 之后，‘v’ 的确定赋值状态为“为 true 时已确定赋值”。
- 否则，在 expr 之后 ‘v’ 的确定赋值状态与在 expr_operand 之后 ‘v’ 的确定赋值状态相同。

## 9.5 变量引用

变量引用是分类为变量的表达式。变量引用表示一个存储位置，既可以访问它以获取当前值，也可以存储新值。

```
variable_reference
: expression
;
```

> 注意：在 C 和 C++ 中，变量引用称为左值。注意结束

## 9.6 变量引用的原子性

对以下数据类型的读取和写入应是原子的：bool、char、byte、sbyte、short、ushort、uint、int、float 和引用类型。此外，基础类型在前述列表中的枚举类型的读取和写入也应是原子的。对其他类型（包括 long、ulong、double 和 decimal，以及用户定义类型）的读取和写入不必是原子的。除了为此目的设计的库函数外，不保证原子的读取-修改-写入，例如在递增或递减的情况下。

## 9.7 引用变量与返回

### 9.7.1 概述

*引用变量*是引用另一个变量（称为引用目标（§9.2.6））的变量。引用变量是用 ref 修饰符声明的局部变量。

引用变量存储指向其引用目标的 *变量引用*（§9.5），而不是其引用目标的值。当在需要值的地方使用引用变量时，返回其引用目标的值；类似地，当 *引用变量* 是赋值目标时，被赋值的是其引用目标。引用变量所引用的变量，即为其引用目标存储的 *变量引用*，可以使用引用赋值（= ref）更改。

*示例：* 以下示例演示一个局部引用变量，其引用目标是数组的一个元素：

```
public class C
{
    public void M()
    {
        int[] arr = new int[10];
        // element is a reference variable that refers to arr[5]
        ref int element = ref arr[5];
        element += 5; // arr[5] has been incremented by 5
    }
}
```

*示例结束*

*引用返回*是从按引用返回的方法（§15.6.1）返回的 *变量引用*。这个 *变量引用* 是该引用返回的引用目标。

*示例：* 以下示例演示一个引用返回，其引用目标是数组字段的一个元素：

```
public class C
{
    private int[] arr = new int[10];

    public ref readonly int M()
    {
        // element is a reference variable that refers to arr[5]
        ref int element = ref arr[5];
        return ref element; // return reference to arr[5];
    }
}
```

*示例结束*

### 9.7.2 引用安全上下文

### 9.7.2.1 概述

所有引用变量都遵守安全规则，确保引用变量的引用安全上下文不大于其引用目标的引用安全上下文。

> 注意：安全上下文的相关概念在（§16.4.12）中定义，并附带相关约束。注意结束

对于任何变量，该变量的引用安全上下文是指向该变量的变量引用（§9.5）有效的上下文。引用变量的引用目标必须具有至少与引用变量本身的引用安全上下文一样宽的引用安全上下文。

> 注意：编译器通过对程序文本的静态分析来确定引用安全上下文。引用安全上下文反映变量在运行时的生存期。注意结束

有三种引用安全上下文：

- **声明块：** 指向局部变量（§9.2.9）的变量引用的引用安全上下文是该局部变量的作用域（§13.6.2），包括该作用域中的任何嵌套嵌入语句。
  指向局部变量的变量引用，仅当引用变量声明在该变量的引用安全上下文内时，才是引用变量的有效引用目标。
- **函数成员：** 在函数内，指向以下任何一项的变量引用具有函数成员的引用安全上下文：
  - 函数成员声明上的值参数（§9.2.5），包括类成员函数的隐式 this；以及
  - 结构成员函数的隐式引用（ref）参数（§9.2.6）this，及其字段。
  具有函数成员引用安全上下文的变量引用，仅当引用变量声明在同一函数成员中时才是有效引用目标。
- **调用方上下文：** 在函数内，指向以下任何一项的变量引用具有调用方上下文的引用安全上下文：
  - 除结构成员函数的隐式 this 之外的引用（ref）参数（§9.2.6）；
  - 此类参数的成员字段和元素；
  - 类类型参数的成员字段；以及
  - 数组类型参数的元素。
  具有调用方上下文引用安全上下文的变量引用可以作为引用返回的引用目标。

这些值形成从最窄（声明块）到最宽（调用方上下文）的嵌套关系。每个嵌套块表示不同的上下文。

示例：以下代码展示了不同引用安全上下文的示例。这些声明展示了：当引用目标是 ref 变量的初始化表达式时，该引用目标的引用安全上下文。这些示例展示了引用返回的引用安全上下文：

```
public class C
{
    // ref safe context of arr is "caller-context".
    // ref safe context of arr[i] is "caller-context".
```



```
private int[] arr = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };

// ref safe context is "caller-context"
public ref int M1(ref int r1)
{
    return ref r1; // r1 is safe to ref return
}

// ref safe context is "function-member"
public ref int M2(int v1)
{
    return ref v1; // error: v1 isn't safe to ref return
}

public ref int M3()
{
    int v2 = 5;

    return ref arr[v2]; // arr[v2] is safe to ref return
}

public void M4(int p)
{
    int v3 = 6;

    // context of r2 is declaration-block,
    // ref safe context of p is function-member
    ref int r2 = ref p;

    // context of r3 is declaration-block,
    // ref safe context of v3 is declaration-block
    ref int r3 = ref v3;

    // context of r4 is declaration-block,
    // ref safe context of arr[v3] is caller-context
    ref int r4 = ref arr[v3];
}
```

示例结束。

示例：对于结构类型，隐式 this 参数作为 ref 参数传递。结构类型字段作为函数成员的引用安全上下文阻止通过引用返回那些字段。此规则阻止以下代码：

```
public struct S
{
    private int n;

    // Disallowed: returning ref of a field.
    public ref int GetN() => ref n;
}

class Test
{
    public ref int M()
    {
        S s = new S();
        ref int numRef = ref s.GetN();
        return ref numRef; // reference to local variable 'numRef' returned
    }
}
```

*示例结束。*

### 9.7.2.2 局部变量的引用安全上下文

对于局部变量 v：

- 如果 v 是引用变量，则其引用安全上下文与其初始化表达式的引用安全上下文相同。
- 否则，其引用安全上下文为声明块。

### 9.7.2.3 参数的引用安全上下文

对于形参 p：

- 如果 p 是 ref 或 in 参数，则其引用安全上下文为调用方上下文。如果 p 是 in 参数，则不能将其作为可写 ref 返回，但可以作为 ref readonly 返回。
- 如果 p 是 out 参数，则其引用安全上下文为调用方上下文。
- 否则，如果 p 是结构类型的 this 参数，则其引用安全上下文为函数成员。
- 否则，该参数是值参数，其引用安全上下文为函数成员。

### 9.7.2.4 字段的引用安全上下文

对于指定对字段 e.F 的引用的变量：

- 如果 e 是引用类型，则其引用安全上下文为调用方上下文。
- 否则，如果 e 是值类型，则其引用安全上下文与 e 的引用安全上下文相同。

### 9.7.2.5 运算符

条件运算符（§12.18），c ? ref e1 : ref e2，以及引用赋值运算符，= ref e（§12.21.1），以引用变量为操作数并产生一个引用变量。对于这些运算符，结果的引用安全上下文是所有 ref 操作数的引用安全上下文中最窄的上下文。

### 9.7.2.6 函数调用

对于由返回 ref 的函数调用产生的变量 c，其引用安全上下文是以下上下文中最窄的：

- 调用方上下文。
- 所有 ref、out 和 in 实参表达式的引用安全上下文（不包括接收者）。
- 对于每个 in 参数，如果存在对应的表达式且该表达式是变量，并且该变量的类型与参数的类型之间存在恒等转换，则为该变量的引用安全上下文，否则为最近的外围上下文。
- 所有实参表达式（包括接收者）的安全上下文（§16.4.12）。

*示例：最后一个要点对于处理如下代码是必要的*

```
ref int M2()
{
    int v = 5;
    // Not valid.
    // ref safe context of "v" is block.
    // Therefore, ref safe context of the return value of M() is block.
    return ref M(ref v);
}

ref int M(ref int p)
{
    return ref p;
}
```

*示例结束*

根据上述规则，属性调用和索引器调用（get 或 set）被视为对底层访问器的函数调用。局部函数调用是函数调用。

### 9.7.2.7 值

值的引用安全上下文是最近的外围上下文。

> *注意：* 这出现在诸如 M(ref d.Length) 的调用中，其中 d 的类型为 dynamic。这也与对应于 in 参数的实参一致。注意结束

### 9.7.2.8 构造函数调用

调用构造函数的新表达式遵循与方法调用（§9.7.2.6）相同的规则，该方法调用被视为返回正在构造的类型。

### 9.7.2.9 引用变量的限制

- 引用参数、输出参数、输入参数、ref 局部变量，以及 ref 结构类型的参数或局部变量，均不得由 lambda 表达式或局部函数捕获。
- 引用参数、输出参数、输入参数，以及 ref 结构类型的参数，均不得作为迭代器方法或异步方法的实参。
- ref 局部变量以及 ref 结构类型的局部变量，均不得在 yield return 语句或 await 表达式所在位置处于上下文中。
- 对于 ref 重新赋值 e1 = ref e2，e2 的引用安全上下文必须至少与 e1 的引用安全上下文一样宽。
- 对于 ref return 语句 return ref e1，e1 的引用安全上下文必须为调用方上下文。

# 10. 转换

### 10.1 概述

转换会使表达式转换为特定类型，或被视为属于特定类型；在前一种情况下，转换可能涉及表示形式的变化。转换可以是隐式的或显式的，这决定是否需要显式强制转换。

示例：例如，从类型 int 到类型 long 的转换是隐式的，因此类型 int 的表达式可以隐式地被视为类型 long。相反的转换（从类型 long 到类型 int）是显式的，因此需要显式强制转换。

```
int a = 123;
long b = a;    // implicit conversion from int to long
int c = (int) b; // explicit conversion from long to int
```

示例结束

某些转换由语言定义。程序也可以定义自己的转换（§10.5）。

语言中的某些转换是从表达式到类型的转换，另一些是从类型到类型的转换。从类型进行的转换适用于具有该类型的所有表达式。

示例：

```
enum Color { Red, Blue, Green }

// The expression 0 converts implicitly to enum types
Color c0 = 0;

// Other int expressions need explicit conversion
Color c1 = (Color)1;

// Conversion from null expression (no type) to string
string x = null;

// Conversion from lambda expression to delegate type
Func<int, int> square = x => x * x;
```

示例结束

### 10.2 隐式转换

### 10.2.1 概述

以下转换被归类为隐式转换：

- 恒等转换
- 隐式数值转换
- 隐式枚举转换
- 隐式内插字符串转换
- 隐式引用转换
- 装箱转换
- 隐式动态转换
- 隐式类型参数转换
- 隐式常量表达式转换
- 用户定义的隐式转换
- 匿名函数转换
- 方法组转换
- null 字面量转换
- 隐式可空转换
- 隐式元组转换
- 提升的用户定义隐式转换
- 默认字面量转换
- 隐式 throw 转换

隐式转换可以出现在多种情况下，包括函数成员调用（§12.6.6）、强制转换表达式（§12.9.7）和赋值（§12.21）。

预定义的隐式转换总是成功，并且永远不会导致抛出异常。

> 注意：设计良好的用户定义隐式转换也应表现出这些特征。注意结束

出于转换的目的，类型 object 和 dynamic 被视为等效。

但是，动态转换（§10.2.10 和 §10.3.8）仅适用于类型 dynamic 的表达式（§8.2.4）。

### 10.2.2 恒等转换

恒等转换从任何类型转换为相同类型。存在这种转换的一个原因是，可以称类型 T 或类型 T 的表达式可转换为 T 本身。

在某些情况下，不完全相同但被视为等效的类型之间存在恒等转换。此类恒等转换存在于：

- object 与 dynamic 之间。
- 具有相同元数的元组类型之间，当每对对应元素类型之间存在恒等转换时。
- 由同一泛型类型构造的类型之间，当每个对应类型实参之间存在恒等转换时。

在大多数情况下，恒等转换在运行时没有效果。但是，由于浮点运算可能以高于其类型所规定（§8.3.7）的精度执行，因此对其结果进行赋值可能会导致精度损失，而显式强制转换保证将精度降低到类型所规定的精度（§12.9.7）。




### 10.2.3 隐式数值转换

隐式数值转换是：

-   从 `sbyte` 到 `short`、`int`、`long`、`float`、`double` 或 `decimal`。
-   从 `byte` 到 `short`、`ushort`、`int`、`uint`、`long`、`ulong`、`float`、`double` 或 `decimal`。
-   从 `short` 到 `int`、`long`、`float`、`double` 或 `decimal`。
-   从 `ushort` 到 `int`、`uint`、`long`、`ulong`、`float`、`double` 或 `decimal`。
-   从 `int` 到 `long`、`float`、`double` 或 `decimal`。
-   从 `uint` 到 `long`、`ulong`、`float`、`double` 或 `decimal`。
-   从 `long` 到 `float`、`double` 或 `decimal`。
-   从 `ulong` 到 `float`、`double` 或 `decimal`。
-   从 `char` 到 `ushort`、`int`、`uint`、`long`、`ulong`、`float`、`double` 或 `decimal`。
-   从 `float` 到 `double`。

从 int、uint、long 或 ulong 到 float 以及从 long 或 ulong 到 double 的转换可能会导致精度损失，但永远不会导致量级损失。其他隐式数值转换永远不会丢失任何信息。

没有预定义的隐式转换到 char 类型，因此其他整型的值不会自动转换为 char 类型。

### 10.2.4 隐式枚举转换

隐式枚举转换允许将具有任意整数类型且值为零的 constant_expression (§12.23) 转换为任意 enum_type 以及底层类型为 enum_type 的任意 nullable_value_type。在后一种情况下，转换通过先转换为底层 enum_type 再包装结果 (§8.3.12) 来求值。

### 10.2.5 隐式插值字符串转换

隐式插值字符串转换允许将 interpolated_string_expression (§12.8.3) 转换为 System.IFormattable 或 System.FormattableString（实现了 System.IFormattable）。当应用此转换时，不会从插值字符串组成字符串值。相反，会创建 System.FormattableString 的实例，如 §12.8.3 进一步所述。

### 10.2.6 隐式可空转换

隐式可空转换是那些源自隐式预定义转换的 nullable 转换 (§10.6.1)。

### 10.2.7 空字面量转换

存在从 null 字面量到任何引用类型或可空值类型的隐式转换。此转换如果目标类型是引用类型则生成 null 引用，或生成给定可空值类型的 null 值 (§8.3.12)。

### 10.2.8 隐式引用转换

隐式引用转换是：

-   从任意 *引用类型* 到 `object` 和 `dynamic`。
-   从任意 *类类型* S 到任意 *类类型* T，前提是 S 派生自 T。
-   从任意 *类类型* S 到任意 *接口类型* T，前提是 S 实现了 T。
-   从任意 *接口类型* S 到任意 *接口类型* T，前提是 S 派生自 T。
-   从具有元素类型 S₁ 的 *数组类型* S 到具有元素类型 T₁ 的 *数组类型* T，前提是以下所有条件都为真：
    -   S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同的维度数。
    -   从 S₁ 到 T₁ 存在隐式引用转换。
-   从单维数组类型 S[] 到 `System.Collections.Generic.IList<T>`、`System.Collections.Generic.IReadOnlyList<T>` 及其基接口，前提是存在从 S 到 T 的隐式恒等或引用转换。
-   从任意 *数组类型* 到 `System.Array` 及其实现的接口。
-   从任意 *委托类型* 到 `System.Delegate` 及其实现的接口。
-   从 null 字面量 (§6.4.5.7) 到任意引用类型。
-   从任意 *引用类型* 到 *引用类型* T，如果它具有到 *引用类型* T₀ 的隐式恒等或引用转换，并且 T₀ 具有到 T 的恒等转换。
-   从任意 *引用类型* 到接口或委托类型 T，如果它具有到接口或委托类型 T₀ 的隐式恒等或引用转换，并且 T₀ 可方差转换为 (§18.2.3.3) T。
-   涉及已知为引用类型的类型参数的隐式转换。有关涉及类型参数的隐式转换的更多详细信息，请参阅 §10.2.12。

隐式引用转换是那些在 *引用类型* 之间可以证明总是成功，因此在运行时不需要检查的转换。

引用转换，无论是 *隐式* 还是 *显式*，永远不会改变被转换对象的引用同一性。

注：换句话说，虽然引用转换可以改变引用的类型，但它永远不会改变所引用对象的类型或值。

### 10.2.9 装箱转换

装箱转换允许将 *值类型* 隐式转换为 *引用类型*。以下装箱转换存在：

-   从任意 *值类型* 到类型 `object`。
-   从任意 *值类型* 到类型 `System.ValueType`。
-   从任意 *枚举类型* 到类型 `System.Enum`。
-   从任意 *非可空值类型* 到由 *非可空值类型* 实现的任意 *接口类型*。
-   从任意 non_nullable_value_type 到任意 interface_type I，使得存在从 non_nullable_value_type 到另一个 interface_type I₀ 的装箱转换，并且 I₀ 具有到 I 的恒等转换。
-   从任意 non_nullable_value_type 到任意 interface_type I，使得存在从 non_nullable_value_type 到另一个 interface_type I₀ 的装箱转换，并且 I₀ 可方差转换为 (§18.2.3.3) I。
-   从任意 nullable_value_type 到任意 reference_type，其中存在从 nullable_value_type 的底层类型到 reference_type 的装箱转换。
-   从一个已知不是引用类型的类型参数到任何类型，只要该转换由 §10.2.12 允许。

对非可空值类型的值进行装箱包括分配对象实例并将值复制到该实例中。

对 nullable_value_type 的值进行装箱，如果它是 null 值（HasValue 为 false），则产生 null 引用，否则产生解包并装箱底层值的結果。

注：装箱的过程可以想象为每个值类型都存在一个装箱类。例如，考虑一个实现接口 I 的 struct S，以及一个名为 S_Boxing 的装箱类。

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

    public S_Boxing(S value)
    {
        this.value = value;
    }

    public void M()
    {
        value.M();
    }
}
```

对类型为 S 的值 v 进行装箱现在包括执行表达式 new S_Boxing(v) 并将 resulting 实例作为转换的目标类型的值返回。因此，语句

```
S s = new S();
object box = s;
```

可以被认为类似于：

```
S s = new S();
object box = new S_Boxing(s);
```

上面描述的想象中的装箱类型实际上并不存在。相反，类型为 S 的装箱值的运行时类型为 S，并且使用值类型作为右操作数的 is 运算符的运行时类型检查测试左操作数是否为右操作数的装箱版本。例如，

```
int i = 123;
object box = i;
if (box is int)
{
    Console.Write("Box contains an int");
}
```

将输出以下内容：

Box contains an int

装箱转换意味着复制被装箱的值。这与将 reference_type 转换为 type object 的转换不同，在后一种转换中，值继续引用同一个实例，只是被视为较不派生的类型 object。例如，以下

```
struct Point
{
    public int x, y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class A
{
    void M()
    {
        Point p = new Point(10, 10);
        object box = p;
        p.x = 20;
        Console.Write(((Point)box).x);
    }
}
```

将在控制台输出值 10，因为在将 p 分配给 box 时发生的隐式装箱操作导致 p 的值被复制。如果 Point 被声明为类，则值 20 将被输出，因为 p 和 box 将引用同一个实例。

装箱类的类比不应被用作超过帮助理解装箱概念的有用工具的用途。此规范描述的行为与通过精确以这种方式实现装箱而产生的行为之间存在许多细微差异。

### 10.2.10 隐式动态转换

存在从类型为 dynamic 的表达式到任意类型 T 的隐式动态转换。该转换是动态绑定的 §12.3.3，这意味着隐式转换将在运行时从表达式的运行时类型到 T 进行查找。如果找不到转换，则会抛出运行时异常。



此隐式转换似乎违反了 §10.2 开头中“隐式转换绝不应引发异常”的建议。然而，并非转换本身，而是查找转换的过程导致了异常。运行时异常的风险是使用动态绑定的固有特性。如果不希望转换进行动态绑定，则可以将表达式先转换为 object，然后再转换为期望的类型。

Example: 以下说明了隐式动态转换：

```
object o = "object";
dynamic d = "dynamic";
string s1 = o;      // Fails at compile-time - no conversion exists
string s2 = d;      // Compiles and succeeds at run-time
int i = d;          // Compiles but fails at run-time - no conversion exists
```

s2 和 i 的赋值都采用了隐式动态转换，其中操作的绑定被推迟到运行时。在运行时，会从 d 的运行时类型（string）到目标类型查找隐式转换。转换到 string 被找到，但转换到 int 未找到。

end example

### 10.2.11 Implicit constant expression conversions
### 10.2.11 隐式常量表达式转换

An implicit constant expression conversion permits the following conversions:
隐式常量表达式转换允许以下转换：

- A constant_expression (§12.23) of type int can be converted to type sbyte, byte, short, ushort, uint, or ulong, provided the value of the constant_expression is within the range of the destination type.
- 类型为 int 的 constant_expression (§12.23) 可以转换为类型 sbyte、byte、short、ushort、uint 或 ulong，前提是 constant_expression 的值在目标类型的范围内。
- A constant_expression of type long can be converted to type ulong, provided the value of the constant_expression is not negative.
- 类型为 long 的 constant_expression 可以转换为类型 ulong，前提是 constant_expression 的值不为负。

### 10.2.12 Implicit conversions involving type parameters
### 10.2.12 隐式类型参数转换

For a type_parameter T that is known to be a reference type (§15.2.5), the following implicit reference conversions (§10.2.8) exist:
对于已知为引用类型 (§15.2.5) 的类型参数 T，存在以下隐式引用转换 (§10.2.8)：

- From T to its effective base class C, from T to any base class of C, and from T to any interface implemented by C.
- 从 T 到其有效基类 C，从 T 到 C 的任意基类，以及从 T 到 C 实现的任意接口。
- From T to an interface_type I in T's effective interface set and from T to any base interface of I.
- 从 T 到 T 有效接口集中的 interface_type I，以及从 T 到 I 的任意基接口。
- From T to a type parameter U provided that T depends on U (§15.2.5).
- 从 T 到类型参数 U，前提是 T 依赖于 U (§15.2.5)。
  Note: Since T is known to be a reference type, within the scope of T, the run-time type of U will always be a reference type, even if U is not known to be a reference type at compile-time. end note
  注：由于 T 已知为引用类型，在 T 的作用域内，U 的运行时类型始终为引用类型，即使在编译时 U 不被已知为引用类型。 end note
- From the null literal (§6.4.5.7) to T.
- 从 null 字面量 (§6.4.5.7) 到 T。

For a type_parameter T that is not known to be a reference type (§15.2.5), the following conversions involving T are considered to be boxing conversions (§10.2.9) at compile-time. At run-time, if T is a value type, the conversion is executed as a boxing conversion. At run-time, if T is a reference type, the conversion is executed as an implicit reference conversion or identity conversion.
对于不已知为引用类型 (§15.2.5) 的类型参数 T，涉及 T 的以下转换在编译时被视为装箱转换 (§10.2.9)。在运行时，如果 T 是值类型，则转换作为装箱转换执行。在运行时，如果 T 是引用类型，则转换作为隐式引用转换或恒等转换执行。

- From T to its effective base class C, from T to any base class of C, and from T to any interface implemented by C.
- 从 T 到其有效基类 C，从 T 到 C 的任意基类，以及从 T 到 C 实现的任意接口。
  Note: C will be one of the types System.Object, System.ValueType, or System.Enum (otherwise T would be known to be a reference type). end note
  注：C 将是 System.Object、System.ValueType 或 System.Enum 中的一种类型（否则 T 将被已知为引用类型）。 end note
- From T to an interface_type I in T's effective interface set and from T to any base interface of I.
- 从 T 到 T 有效接口集中的 interface_type I，以及从 T 到 I 的任意基接口。

For a type_parameter T that is not known to be a reference type, there is an implicit conversion from T to a type parameter U provided T depends on U. At run-time, if T is a value type and U is a reference type, the conversion is executed as a boxing conversion. At run-time, if both T and U are value types, then T and U are necessarily the same type and no conversion is performed. At run-time, if T is a reference type, then U is necessarily also a reference type and the conversion is executed as an implicit reference conversion or identity conversion (§15.2.5).
对于不已知为引用类型的类型参数 T，如果 T 依赖于 U，则存在从 T 到类型参数 U 的隐式转换。在运行时，如果 T 是值类型且 U 是引用类型，则转换作为装箱转换执行。在运行时，如果 T 和 U 都是值类型，则 T 和 U 必然是同一类型且不执行转换。在运行时，如果 T 是引用类型，则 U 必然也是引用类型，且转换作为隐式引用转换或恒等转换执行 (§15.2.5)。

The following further implicit conversions exist for a given type parameter T:
对于给定的类型参数 T，还存在以下隐式转换：

- From T to a reference type S if it has an implicit conversion to a reference type S0 and S0 has an identity conversion to S. At run-time, the conversion is executed the same way as the conversion to S0.
- 如果 T 具有到引用类型 S0 的隐式转换且 S0 具有到 S 的恒等转换，则从 T 到引用类型 S。在运行时，转换的执行方式与转换到 S0 相同。
- From T to an interface type I if it has an implicit conversion to an interface type I0, and I0 is variance-convertible to I (§18.2.3.3). At run-time, if T is a value type, the conversion is executed as a boxing conversion. Otherwise, the conversion is executed as an implicit reference conversion or identity conversion.
- 如果 T 具有到接口类型 I0 的隐式转换，且 I0 可方差转换为 I (§18.2.3.3)，则从 T 到接口类型 I。在运行时，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。

In all cases, the rules ensure that a conversion is executed as a boxing conversion if and only if at run-time the conversion is from a value type to a reference type.
在所有情况下，规则确保转换仅在运行时从值类型到引用类型时才作为装箱转换执行。

### 10.2.13 Implicit tuple conversions
### 10.2.13 隐式元组转换

An implicit conversion exists from a tuple expression E to a tuple type T if E has the same arity as T and an implicit conversion exists from each element in E to the corresponding element type in T. The conversion is performed by creating an instance of T's corresponding System.ValueTuple<...> type, and initializing each of its fields in order from left to right by evaluating the corresponding tuple element expression of E, converting it to the corresponding element type of T using the implicit conversion found, and initializing the field with the result.
如果元组表达式 E 与元组类型 T 具有相同的元数，并且 E 中的每个元素到 T 中对应元素类型存在隐式转换，则从元组表达式 E 到元组类型 T 存在隐式转换。转换通过创建 T 对应的 System.ValueTuple<...> 类型的实例来执行，并按从左到右的顺序初始化其每个字段，通过计算 E 的对应元组元素表达式，将其使用找到的隐式转换转换为 T 的对应元素类型，并用结果初始化字段。

If an element name in the tuple expression does not match a corresponding element name in the tuple type, a warning shall be issued.
如果元组表达式中的元素名称与元组类型中的对应元素名称不匹配，则应发出警告。

Example:
示例：

```
(int, string) t1 = (1, "One");
(byte, string) t2 = (2, null);
(int, string) t3 = (null, null);    // Error: No conversion
(int i, string s) t4 = (i: 4, s: "Four");
(int i, string) t5 = (x: 5, s: "Five"); // Warning: Names are ignored
```

The declarations of t1, t2, t4 and t5 are all valid, since implicit conversions exist from the element expressions to the corresponding element types. The declaration of t3 is invalid, because there is no conversion from null to int. The declaration of t5 causes a warning because the element names in the tuple expression differ from those in the tuple type.
t1、t2、t4 和 t5 的声明都有效，因为从元素表达式到对应元素类型存在隐式转换。t3 的声明无效，因为 null 到 int 没有转换。t5 的声明会发出警告，因为元组表达式中的元素名称与元组类型中的不同。

end example

### 10.2.14 User-defined implicit conversions
### 10.2.14 用户定义的隐式转换

A user-defined implicit conversion consists of an optional standard implicit conversion, followed by execution of a user-defined implicit conversion operator, followed by another optional standard implicit conversion. The exact rules for evaluating user-defined implicit conversions are described in §10.5.4.
用户定义的隐式转换由可选的标准隐式转换组成，其后执行用户定义的隐式转换运算符，其后是另一个可选的标准隐式转换。评估用户定义的隐式转换的确切规则在 §10.5.4 中描述。

### 10.2.15 Anonymous function conversions and method group conversions
### 10.2.15 匿名函数转换和方法组转换

Anonymous functions and method groups do not have types in and of themselves, but they may be implicitly converted to delegate types. Additionally, some lambda expressions may be implicitly converted to expression tree types. Anonymous function conversions are described in more detail in §10.7 and method group conversions in §10.8.
匿名函数和方法组本身没有类型，但它们可以隐式转换为委托类型。此外，一些 lambda 表达式可以隐式转换为表达式树类型。匿名函数转换在 §10.7 中有更详细的描述，方法组转换在 §10.8 中描述。

### 10.2.16 Default literal conversions
### 10.2.16 默认字面量转换

An implicit conversion exists from a default_literal (§12.8.20) to any type. This conversion produces the default value (§9.3) of the inferred type.
从 default_literal (§12.8.20) 到任意类型存在隐式转换。此转换产生推断类型的默认值 (§9.3)。

### 10.2.17 Implicit throw conversions
### 10.2.17 隐式 throw 转换

While throw expressions do not have a type, they may be implicitly converted to any type.
虽然 throw 表达式没有类型，但它们可以隐式转换为任意类型。

## 10.3 Explicit conversions
## 10.3 显式转换

### 10.3.1 General
### 10.3.1 通用

The following conversions are classified as explicit conversions:
以下转换被归类为显式转换：

- All implicit conversions
- 所有隐式转换
- Explicit numeric conversions
- 显式数值转换
- Explicit enumeration conversions
- 显式枚举转换
- Explicit nullable conversions
- 显式可空转换
- Explicit tuple conversions
- 显式元组转换
- Explicit reference conversions
- 显式引用转换
- Explicit interface conversions
- 显式接口转换
- Unboxing conversions
- 解箱转换
- Explicit type parameter conversions
- 显式类型参数转换
- Explicit dynamic conversions
- 显式动态转换
- User-defined explicit conversions
- 用户定义的显式转换

Explicit conversions can occur in cast expressions (§12.9.7).
显式转换可以在强制转换表达式 (§12.9.7) 中出现。

The set of explicit conversions includes all implicit conversions.
显式转换的集合包括所有隐式转换。

> Note: This, for example, allows an explicit cast to be used when an implicit conversion to the same type exists, in order to force the selection of a particular method overload. end note
> 注：例如，这允许在存在到同一类型的隐式转换时使用显式强制转换，以便强制选择特定的方法重载。 end note

The explicit conversions that are not implicit conversions are conversions that cannot be proven always to succeed, conversions that are known possibly to lose information, and conversions across domains of types sufficiently different to merit explicit notation.
不是隐式转换的显式转换是无法证明总是成功的转换、已知可能丢失信息的转换，以及跨越类型域足够不同以值得显式表示的转换。

### 10.3.2 Explicit numeric conversions
### 10.3.2 显式数值转换

The explicit numeric conversions are the conversions from a numeric_type to another numeric_type for which an implicit numeric conversion (§10.2.3) does not already exist:
显式数值转换是从 numeric_type 到另一个 numeric_type 的转换，其中不存在隐式数值转换 (§10.2.3)：

-   从 sbyte 到 byte、ushort、uint、ulong 或 char。
-   从 byte 到 sbyte 或 char。
-   从 short 到 sbyte、byte、ushort、uint、ulong 或 char。
-   从 ushort 到 sbyte、byte、short 或 char。
-   从 int 到 sbyte、byte、short、ushort、uint、ulong 或 char。
-   从 uint 到 sbyte、byte、short、ushort、int 或 char。
-   从 long 到 sbyte、byte、short、ushort、int、uint、ulong 或 char。
-   从 ulong 到 sbyte、byte、short、ushort、int、uint、long 或 char。
-   从 char 到 sbyte、byte 或 short。
-   从 float 到 sbyte、byte、short、ushort、int、uint、long、ulong、char 或 decimal。
-   从 double 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 decimal。
-   从 decimal 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 double。

因为显式转换包括所有隐式和显式数值转换，所以始终可以使用强制转换表达式 (§12.9.7) 将任何 numeric_type 转换为任何其他 numeric_type。

显式数值转换可能会丢失信息或可能导致抛出异常。显式数值转换的处理如下：

-   对于从一种整型到另一种整型的转换，处理取决于转换发生的溢出检查上下文 (§12.8.19)：
  -   在 checked 上下文中，如果源操作数的值在目标类型的范围内，则转换成功；但如果源操作数的值超出目标类型的范围，则抛出 System.OverflowException。
  -   在 unchecked 上下文中，转换总是成功，并按如下方式进行。
    -   如果源类型大于目标类型，则源值通过丢弃其“额外”的最高有效位来截断。然后将结果视为目标类型的值。
    -   如果源类型与目标类型大小相同，则源值被视为目标类型的值
-   对于从 decimal 到整型的转换，源值将向零舍入到最接近的整数值，并且该整数值成为转换的结果。如果得到的整数值超出目标类型的范围，则抛出 System.OverflowException。
-   对于从 float 或 double 到整型的转换，处理取决于转换发生的溢出检查上下文 (§12.8.19)：
  -   在 checked 上下文中，转换按如下方式进行：
    -   如果操作数的值为 NaN 或无穷大，则抛出 System.OverflowException。
    -   否则，源操作数将向零舍入到最接近的整数值。如果该整数值在目标类型的范围内，则该值是转换的结果。
    -   否则，抛出 System.OverflowException。
-   在 unchecked 上下文中，转换总是成功，并按如下方式进行。
  -   如果操作数的值为 NaN 或无穷大，则转换结果为目标类型的未指定值。
  -   否则，源操作数将向零舍入到最接近的整数值。如果该整数值在目标类型的范围内，则该值是转换的结果。
  -   否则，转换结果为目标类型的未指定值。
-   对于从 `double` 到 `float` 的转换，`double` 值将舍入到最接近的 `float` 值。如果 `double` 值太小而无法表示为 `float`，则结果变为与该值符号相同的零。如果 `double` 值的大小太大而无法表示为 `float`，则结果变为与该值符号相同的无穷大。如果 `double` 值为 NaN，则结果也是 NaN。
-   对于从 `float` 或 `double` 到 `decimal` 的转换，源值被转换为 `decimal` 表示形式，并在需要时舍入到最接近的数字 (§8.3.8)。
  -   如果源值太小而无法表示为 `decimal`，则结果变为零，如果 `decimal` 支持带符号的零值，则保留原始值的符号。
  -   如果源值的大小太大而无法表示为 `decimal`，或该值为无穷大，则结果为无穷大并保留原始值的符号，如果十进制表示支持无穷大；否则抛出 System.OverflowException。
  -   如果源值为 NaN，则如果十进制表示支持 NaN，则结果为 NaN；否则抛出 System.OverflowException。
-   对于从 `decimal` 到 `float` 或 `double` 的转换，`decimal` 值将舍入到最接近的 `double` 或 `float` 值。如果源值的大小太大而无法在目标类型中表示，或该值为无穷大，则结果为无穷大并保留原始值的符号。如果源值为 NaN，则结果为 NaN。虽然此转换可能会丢失精度，但它永远不会导致抛出异常。

*注意：* `decimal` 类型不需要支持无穷大或 NaN 值，但可以支持；其范围可能小于 `float` 和 `double` 的范围，但并非保证。 对于没有无穷大或 NaN 值且范围小于 `float` 的 `decimal` 表示形式，从 `decimal` 到 `float` 或 `double` 的转换结果永远不会是无穷大或 NaN。 *结束注释*

## 10.3.3 显式枚举转换

显式枚举转换如下：

-   从 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double` 或 `decimal` 到任何 `enum_type`。
-   从任何 `enum_type` 到 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double` 或 `decimal`。
-   从任何 `enum_type` 到任何其他 `enum_type`。

在两种类型之间进行显式枚举转换时，将任何参与的 `enum_type` 视为该 `enum_type` 的基础类型，然后在所得类型之间执行隐式或显式数值转换。

示例：给定一个基础类型为 int 的 enum_type E，从 E 到 byte 的转换被处理为从 int 到 byte 的显式数值转换 (§10.3.2) ，而从 byte 到 E 的转换被处理为从 byte 到 int 的隐式数值转换 (§10.2.3)。 end example

## 10.3.4 显式可空转换

显式可空转换是那些源自显式和隐式预定义转换的可空转换 (§10.6.1)。

## 10.3.5 显式引用转换

显式引用转换如下：

-   从 object 和 dynamic 到任何其他 reference_type。
-   从任何 class_type S 到任何 class_type T，前提是 S 是 T 的基类。
-   从任何 class_type S 到任何 interface_type T，前提是 S 未密封并且 S 未实现 T。
-   从任何 interface_type S 到任何 class_type T，前提是 T 未密封或 T 实现 S。
-   从任何 interface_type S 到任何 interface_type T，前提是 S 未派生自 T。
-   从具有元素类型 S₁ 的 array_type S 到具有元素类型 T₁ 的 array_type T，前提是以下所有条件都为真：
  -   S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同的维度数。
  -   从 S₁ 到 T₁ 存在显式引用转换。
-   从 System.Array 及其实现的接口到任何 array_type。
-   从单维 array_type S[] 到 System.Collections.Generic.IList<T>、System.Collections.Generic.IReadOnlyList<T> 及其基接口，前提是从 S 到 T 存在恒等转换或显式引用转换。
-   从 System.Collections.Generic.IList<S>、System.Collections.Generic.IReadOnlyList<S> 及其基接口到单维数组类型 T[]，前提是从 S 到 T 存在恒等转换或显式引用转换。
-   从 System.Delegate 及其实现的接口到任何 delegate_type。
-   如果从 S 到引用类型 T₀ 存在显式引用转换，并且从 T₀ 到 T 存在恒等转换，则从引用类型 S 到引用类型 T。
-   如果从 S 到接口或委托类型 T₀ 存在显式引用转换，并且 T₀ 可方差转换为 T 或 T 可方差转换为 T₀，则从引用类型 S 到接口或委托类型 T §18.2.3.3。
-   从 D<S₁...Sₙ> 到 D<T₁...Tₙ>，其中 D<X₁...Xₙ> 是泛型委托类型，D<S₁...Sₙ> 与 D<T₁...Tₙ> 不兼容且不相同，并且对于 D 的每个类型参数 Xᵢ，以下条件成立：
  -   如果 Xᵢ 是不变的，则 Sᵢ 与 Tᵢ 相同。
  -   如果 Xᵢ 是协变的，则从 Sᵢ 到 Tᵢ 存在恒等转换、隐式引用转换或显式引用转换。
  -   如果 Xᵢ 是逆变的，则 Sᵢ 和 Tᵢ 要么相同，要么都是引用类型。



- 涉及已知为引用类型的类型参数的显式转换。有关涉及类型参数的显式转换的更多详细信息，请参见 §10.3.9。

显式引用转换是 *引用类型* 之间需要进行运行时检查以确保其正确的转换。

为使显式引用转换在运行时成功，源操作数的值应为 `null`，或者源操作数所引用对象的类型应是通过隐式引用转换（§10.2.8）可转换为目标类型的类型。如果显式引用转换失败，则引发 `System.InvalidCastException`。

> *注意：* 引用转换（无论是隐式还是显式）从不更改引用本身的值（§8.2.1），只更改其类型；也不更改所引用对象的类型或值。*注释结束*

## 10.3.6 显式元组转换

如果元组表达式 *E* 与元组类型 *T* 具有相同的元数，并且存在从 *E* 中的每个元素到 *T* 中对应元素类型的隐式或显式转换，则存在从 *E* 到 *T* 的显式转换。该转换通过创建 *T* 对应的 `System.ValueTuple<...>` 类型的实例，并按从左到右的顺序初始化其每个字段来执行：计算 *E* 的对应元组元素表达式，使用找到的显式转换将其转换为 *T* 的对应元素类型，然后用结果初始化该字段。

## 10.3.7 拆箱转换

拆箱转换允许将 *引用类型* 显式转换为 *值类型*。存在以下拆箱转换：

- 从类型 `object` 到任何 *值类型*。
- 从类型 `System.ValueType` 到任何 *值类型*。
- 从类型 `System.Enum` 到任何 *枚举类型*。
- 从任何 *接口类型* 到实现该 *接口类型* 的任何 *非可空值类型*。
- 从任何 *接口类型* *I* 到任何 *非可空值类型*，其中存在从 *接口类型* *I₀* 到该 *非可空值类型* 的拆箱转换，并且存在从 *I* 到 *I₀* 的恒等转换。
- 从任何 *接口类型* *I* 到任何 *非可空值类型*，其中存在从 *接口类型* *I₀* 到该 *非可空值类型* 的拆箱转换，并且 *I₀* 可 *可变性可转换* 为 *I*，或 *I* 可 *可变性可转换* 为 *I₀*（§18.2.3.3）。
- 从任何 *引用类型* 到任何 *可空值类型*，其中存在从 *引用类型* 到该 *可空值类型* 的基础 *非可空值类型* 的拆箱转换。
- 从已知不是值类型的类型参数到任何类型，只要该转换被 §10.3.9 允许。

到 *非可空值类型* 的拆箱操作包括：首先检查对象实例是否为给定 *非可空值类型* 的装箱值，然后从该实例中复制出值。

到 *可空值类型* 的拆箱：如果源操作数为 `null`，则生成该 *可空值类型* 的 null 值；否则生成将该对象实例拆箱到该 *可空值类型* 的基础类型后的包装结果。

> 注意：参考 §10.2.9 中描述的假想装箱类，将对象装箱转换为值类型 S 的拆箱转换包括执行表达式 ((S_Boxing)box).value。因此，以下语句

```
    object box = new S();
    S s = (S)box;
```

概念上对应于

```
    object box = new S_Boxing(new S());
    S s = ((S_Boxing)box).value;
```

注释结束

为使到给定非可空值类型的拆箱转换在运行时成功，源操作数的值应为对该非可空值类型的装箱值的引用。如果源操作数是对不兼容对象的引用，则引发 System.InvalidCastException。

为使到给定可空值类型的拆箱转换在运行时成功，源操作数的值应为 null，或为对该可空值类型的基础非可空值类型的装箱值的引用。如果源操作数是对不兼容对象的引用，则引发 System.InvalidCastException。

## 10.3.8 显式动态转换

存在从类型为 dynamic 的表达式到任何类型 T 的显式动态转换。该转换采用动态绑定（§12.3.3），这意味着将在运行时从表达式的运行时类型到 T 寻找显式转换。如果未找到转换，则引发运行时异常。

如果不需要该转换的动态绑定，可以先将表达式转换为 object，然后再转换为所需类型。

*示例：* 假设定义了以下类：

```
    class C
    {
        int i;

        public C(int i)
        {
            this.i = i;
        }

        public static explicit operator C(string s)
        {
            return new C(int.Parse(s));
        }
    }
```

以下示例演示显式动态转换：

```
    object o = "1";
    dynamic d = "2";
    var c1 = (C)o; // Compiles, but explicit reference conversion fails
    var c2 = (C)d; // Compiles and user defined conversion succeeds
```

在编译时，o 到 C 的最佳转换被确定为显式引用转换。该转换在运行时失败，因为 "1" 实际上并不是 C。然而，d 到 C 的转换作为显式动态转换被推迟到运行时，在那里找到从 d 的运行时类型（string）到 C 的用户定义转换，并成功。

示例结束

## 10.3.9 涉及类型参数的显式转换

对于已知为引用类型（§15.2.5）的 *类型参数* T，存在以下显式引用转换（§10.3.5）：

- 从 T 的有效基类 C 到 T，以及从 C 的任何基类到 T。
- 从任何 *接口类型* 到 T。
- 从 T 到任何 *接口类型* I，前提是尚不存在从 T 到 I 的隐式引用转换。
- 从 *类型参数* U 到 T，前提是 T 依赖于 U（§15.2.5）。

注意：由于 T 已知为引用类型，因此在 T 的范围内，U 的运行时类型将始终是引用类型，即使 U 在编译时未知为引用类型。注释结束

对于未知为引用类型（§15.2.5）的 *类型参数* T，以下涉及 T 的转换在编译时被视为拆箱转换（§10.3.7）。在运行时，如果 T 是值类型，则该转换作为拆箱转换执行。在运行时，如果 T 是引用类型，则该转换作为显式引用转换或恒等转换执行。

- 从 T 的有效基类 C 到 T，以及从 C 的任何基类到 T。

注意：C 将是 System.Object、System.ValueType 或 System.Enum 类型之一（否则 T 将被已知为引用类型）。注释结束

- 从任何 *接口类型* 到 T。

对于未知为引用类型（§15.2.5）的 *类型参数* T，存在以下显式转换：

- 从 T 到任何 *接口类型* I，前提是尚不存在从 T 到 I 的隐式转换。此转换由从 T 到 object 的隐式装箱转换（§10.2.9）以及随后从 object 到 I 的显式引用转换组成。在运行时，如果 T 是值类型，则该转换作为装箱转换后接显式引用转换执行。在运行时，如果 T 是引用类型，则该转换作为显式引用转换执行。
- 从 *类型参数* U 到 T，前提是 T 依赖于 U（§15.2.5）。在运行时，如果 T 是值类型且 U 是引用类型，则该转换作为拆箱转换执行。在运行时，如果 T 和 U 都是值类型，则 T 和 U 必然是同一类型，并且不执行转换。在运行时，如果 T 是引用类型，则 U 必然也是引用类型，并且该转换作为显式引用转换或恒等转换执行。

在所有情况下，这些规则确保：当且仅当在运行时转换是从引用类型到值类型时，该转换才作为拆箱转换执行。

上述规则不允许从不受约束的类型参数到非接口类型的直接显式转换，这可能令人意外。该规则的原因是为了防止混淆，并使此类转换的语义清晰。

示例：考虑以下声明：

```
class X<T>
{
```



```csharp
    public static long F(T t)
    {
        return (long)t;            // Error
    }
```

如果允许 t 到 long 的直接显式转换，人们很容易期望 `X<int>.F(7)` 会返回 7L。然而事实并非如此，因为标准数值转换只有在绑定时已知类型为数值时才会被考虑。为了使语义明确，上面的示例必须改写为：

```csharp
class X<T>
{
    public static long F(T t)
    {
        return (long)(object)t;        // Ok, but will only work when T is long
    }
}
```

此代码现在可以编译，但执行 `X<int>.F(7)` 时会在运行时抛出异常，因为装箱的 int 不能直接转换为 long。

*示例结束*

### 10.3.10 用户定义的显式转换

用户定义的显式转换由可选的标准显式转换、随后执行用户定义的隐式或显式转换运算符，再 followed by 另一个可选的标准显式转换组成。评估用户定义的显式转换的确切规则在 §10.5.5 中描述。

## 10.4 标准转换

### 10.4.1 通用

标准转换是指可在用户定义转换的一部分中发生的预定义转换。

### 10.4.2 标准隐式转换

以下隐式转换被归类为标准隐式转换：

- 恒等转换 (§10.2.2)
- 隐式数值转换 (§10.2.3)
- 隐式可空转换 (§10.2.6)
- 空字面量转换 (§10.2.7)
- 隐式引用转换 (§10.2.8)
- 装箱转换 (§10.2.9)
- 隐式常量表达式转换 (§10.2.11)
- 涉及类型参数的隐式转换 (§10.2.12)

标准隐式转换明确排除用户定义的隐式转换。

### 10.4.3 标准显式转换

标准显式转换包括所有标准隐式转换，外加存在相反标准隐式转换的显式转换子集。

> 注：换句话说，如果从类型 A 到类型 B 存在标准隐式转换，则从类型 A 到类型 B 以及从类型 B 到类型 A 都存在标准显式转换。注释结束

## 10.5 用户定义的转换

### 10.5.1 通用

C# 允许通过用户定义的转换来扩展预定义的隐式和显式转换。用户定义的转换是通过在类和结构类型中声明转换运算符 (§15.10.4) 来引入的。

### 10.5.2 允许的用户定义转换

C# 仅允许声明某些用户定义的转换。特别是，不可能重新定义已存在的隐式或显式转换。

对于给定的源类型 S 和目标类型 T，如果 S 或 T 是可空值类型，则令 S₀ 和 T₀ 指代其底层类型，否则 S₀ 和 T₀ 分别等于 S 和 T。仅当满足以下所有条件时，类或结构才允许声明从源类型 S 到目标类型 T 的转换：

- S₀ 和 T₀ 是不同的类型。
- S₀ 或 T₀ 是运算符声明所在的类或结构类型。
- S₀ 和 T₀ 都不是接口类型。
- 排除用户定义的转换后，从 S 到 T 或从 T 到 S 不存在转换。

适用于用户定义转换的限制在 §15.10.4 中指定。

### 10.5.3 用户定义转换的求值

用户定义的转换将可能具有源类型的源表达式转换为另一种类型，称为目标类型。用户定义转换的求值集中于为源表达式和目标类型找到最具体的用户定义转换运算符。此确定分为几个步骤：

- 找到将考虑用户定义转换运算符的类和结构集合。此集合由源类型及其基类（如果源类型存在）以及目标类型及其基类组成。为此目的，假定只有类和结构可以声明用户定义运算符，并且非类类型没有基类。此外，如果源类型或目标类型是可空值类型，则使用其底层类型代替。
- 从该类型集合中确定哪些用户定义和提升的转换运算符适用。要使转换运算符适用，必须能够从源表达式对运算符的操作数类型执行标准转换 (§10.4)，并且必须能够从运算符的结果类型对目标类型执行标准转换。
- 从适用的用户定义运算符集合中确定哪个运算符无歧义地是最具体的。总体而言，最具体的运算符是其操作数类型与源表达式“最接近”且其结果类型与目标类型“最接近”的运算符。用户定义的转换运算符优先于提升的转换运算符。确定最具体的用户定义转换运算符的确切规则在以下小节中定义。

一旦确定了最具体的用户定义转换运算符，用户定义转换的实际执行涉及最多三个步骤：

- 首先，如果需要，从源表达式对用户定义或提升的转换运算符的操作数类型执行标准转换。
- 接下来，调用用户定义或提升的转换运算符来执行转换。
- 最后，如果需要，从用户定义转换运算符的结果类型对目标类型执行标准转换。

用户定义转换的求值永远不会涉及多于一个用户定义或提升的转换运算符。换句话说，从类型 S 到类型 T 的转换永远不会先执行从 S 到 X 的用户定义转换，然后再执行从 X 到 T 的用户定义转换。

- 用户定义隐式或显式转换求值的精确定义在以下小节中给出。定义使用了以下术语：
  - 如果从类型 A 到类型 B 存在标准隐式转换 (§10.4.2)，并且 A 和 B 都不是接口类型，则称 A 被 B 所包含，B 包含 A。
  - 如果从表达式 E 到类型 B 存在标准隐式转换 (§10.4.2)，并且 B 以及 E 的类型（如果有）都不是接口类型，则称 E 被 B 所包含，B 包含 E。
  - 一组类型中最包含的类型是包含该集合中所有其他类型的那一个类型。如果没有单个类型包含所有其他类型，则该集合没有最包含的类型。更直观地说，最包含的类型是该集合中的“最大”类型——每个其他类型都可以隐式转换为该类型的那一个类型。
  - 一组类型中最被包含的类型是被该集合中所有其他类型所包含的那一个类型。如果没有单个类型被所有其他类型所包含，则该集合没有最被包含的类型。更直观地说，最被包含的类型是该集合中的“最小”类型——可以隐式转换为每个其他类型的那一个类型。

### 10.5.4 用户定义的隐式转换

从表达式 E 到类型 T 的用户定义隐式转换按如下方式处理：

- 确定类型 S₀ 和 T₀ 和 Tₑ。
  - 如果 E 有类型，则令 S 为该类型。
  - 如果 S 或 T 是可空值类型，则令 S₁ 和 T₁ 为其底层类型，否则分别令 S₁ 和 T₁ 为 S 和 T。
  - 如果 S₁ 或 T₁ 是类型参数，则令 S₀ 和 T₀ 为其有效基类，否则分别令 S₀ 和 T₀ 为 S₁ 和 T₁。
- 找到类型集合 D，从中将考虑用户定义转换运算符。此集合由 S₀（如果 S₀ 存在且是类或结构）、S₀ 的基类（如果 S₀ 存在且是类）组成，

以及 Tθ（如果 Tθ 是类或结构体）。仅当不存在到集合中已包含的另一类型的恒等转换时，才将类型添加到集合 D 中。

- 查找适用的用户定义转换运算符和提升转换运算符的集合 U。此集合由 D 中的类或结构体声明的、从包含 E 的类型转换为被 T 包含的类型的用户定义和提升隐式转换运算符组成。如果 U 为空，则转换未定义，并发生编译时错误。
  - 如果 S 存在且 U 中任一运算符从 S 转换，则 Sx 为 S。
  - 否则，Sx 是 U 中运算符源类型的合并集合中最被包含的类型。如果无法找到唯一的最被包含类型，则转换有歧义，并发生编译时错误。
- 查找 U 中运算符的最特定目标类型 Tx：
  - 如果 U 中任一运算符转换为 T，则 Tx 为 T。
  - 否则，Tx 是 U 中运算符目标类型的合并集合中最包含的类型。如果无法找到唯一的最包含类型，则转换有歧义，并发生编译时错误。
- 查找最特定的转换运算符：
  - 如果 U 恰好包含一个从 Sx 转换为 Tx 的用户定义转换运算符，则这就是最特定的转换运算符。
  - 否则，如果 U 恰好包含一个从 Sx 转换为 Tx 的提升转换运算符，则这就是最特定的转换运算符。
  - 否则，转换有歧义，并发生编译时错误。
- 最后，应用该转换：
  - 如果 E 尚不具有类型 Sx，则执行从 E 到 Sx 的标准隐式转换。
  - 调用最特定的转换运算符以从 Sx 转换为 Tx。
  - 如果 Tx 不是 T，则执行从 Tx 到 T 的标准隐式转换。

如果存在从类型 S 的变量到 T 的用户定义隐式转换，则存在从类型 S 到类型 T 的用户定义隐式转换。

### 10.5.5 用户定义显式转换

从表达式 E 到类型 T 的用户定义显式转换按如下方式处理：

- 确定类型 S、Sθ 和 Tθ。
  - 如果 E 具有类型，则令 S 为该类型。
  - 如果 S 或 T 是可空值类型，则令 S1 和 T1 为其底层类型；否则令 S1 和 T1 分别为 S 和 T。
  - 如果 S1 或 T1 是类型参数，则令 Sθ 和 Tθ 为其有效基类；否则令 Sθ 和 Tθ 分别为 S1 和 T1。
- 查找将考虑用户定义转换运算符的类型集合 D。此集合由 Sθ（如果 Sθ 存在且是类或结构体）、Sθ 的基类（如果 Sθ 存在且是类）、Tθ（如果 Tθ 是类或结构体）以及 Tθ 的基类（如果 Tθ 是类）组成。仅当不存在到集合中已包含的另一类型的恒等转换时，才将类型添加到集合 D 中。
- 查找适用的用户定义转换运算符和提升转换运算符的集合 U。此集合由 D 中的类或结构体声明的、从包含 E 或由 S 包含的类型（如果 S 存在）转换为包含 T 或由 T 包含的类型的用户定义和提升隐式或显式转换运算符组成。如果 U 为空，则转换未定义，并发生编译时错误。
- 查找 U 中运算符的最特定源类型 Sx：
  - 如果 S 存在且 U 中任一运算符从 S 转换，则 Sx 为 S。
  - 否则，如果 U 中任一运算符从包含 E 的类型转换，则 Sx 是这些运算符源类型的合并集合中最被包含的类型。如果找不到最被包含的类型，则转换有歧义，并发生编译时错误。
  - 否则，Sx 是 U 中运算符源类型的合并集合中最包含的类型。如果无法找到唯一的最包含类型，则转换有歧义，并发生编译时错误。
- 查找 U 中运算符的最特定目标类型 Tx：
  - 如果 U 中任一运算符转换为 T，则 Tx 为 T。
  - 否则，如果 U 中任一运算符转换为被 T 包含的类型，则 Tx 是这些运算符目标类型的合并集合中最被包含的类型。如果找不到最被包含的类型，则转换有歧义，并发生编译时错误。
  - 否则，Tx 是 U 中运算符目标类型的合并集合中最包含的类型。如果无法找到唯一的最包含类型，则转换有歧义，并发生编译时错误。
- 查找最特定的转换运算符：
  - 如果 U 恰好包含一个从 Sx 转换为 Tx 的用户定义转换运算符，则这就是最特定的转换运算符。
  - 否则，如果 U 恰好包含一个从 Sx 转换为 Tx 的提升转换运算符，则这就是最特定的转换运算符。
  - 否则，转换有歧义，并发生编译时错误。
- 最后，应用该转换：
  - 如果 E 尚不具有类型 Sx，则执行从 E 到 Sx 的标准显式转换。
  - 调用最特定的用户定义转换运算符以从 Sx 转换为 Tx。
  - 如果 Tx 不是 T，则执行从 Tx 到 T 的标准显式转换。

如果存在从类型 S 的变量到 T 的用户定义显式转换，则存在从类型 S 到类型 T 的用户定义显式转换。

## 10.6 涉及可空类型的转换

### 10.6.1 可空转换

可空转换允许对非可空值类型执行的预定义转换也用于这些类型的可空形式。对于从非可空值类型 S 转换为非可空值类型 T 的每个预定义隐式或显式转换（§10.2.2、§10.2.3、§10.2.4、§10.2.11、§10.3.2 和 §10.3.3），存在以下可空转换：

- 从 S? 到 T? 的隐式或显式转换
- 从 S 到 T? 的隐式或显式转换
- 从 S? 到 T 的显式转换。

可空转换本身被归类为隐式转换或显式转换。

某些可空转换被归类为标准转换，并且可以作为用户定义转换的一部分出现。具体而言，所有隐式可空转换都被归类为标准隐式转换（§10.4.2），而那些满足 §10.4.3 要求的显式可空转换被归类为标准显式转换。

基于从 S 到 T 的底层转换来求值可空转换的过程如下：

- 如果可空转换是从 S? 到 T?：
  - 如果源值为 null（HasValue 属性为 false），则结果为类型 T? 的 null 值。
  - 否则，该转换按以下方式求值：从 S? 解包到 S，随后执行从 S 到 T 的底层转换，随后从 T 包装到 T?。
- 如果可空转换是从 S 到 T?，则该转换按以下方式求值：执行从 S 到 T 的底层转换，随后从 T 包装到 T?。
- 如果可空转换是从 S? 到 T，则该转换按以下方式求值：从 S? 解包到 S，随后执行从 S 到 T 的底层转换。

### 10.6.2 提升转换

给定一个从非可空值类型 S 转换为非可空值类型 T 的用户定义转换运算符，存在一个从 S? 转换为 T? 的提升转换运算符。此提升转换运算符执行以下操作：从 S? 解包到 S，随后执行从 S 到 T 的用户定义转换，随后从 T 包装到 T?；不同之处在于，值为 null 的 S? 直接转换为值为 null 的 T?。提升转换运算符具有与其底层用户定义转换运算符相同的隐式或显式分类。

## 10.7 匿名函数转换

### 10.7.1 概述

anonymous_method_expression 或 lambda_expression 被归类为匿名函数（§12.19）。该表达式没有类型，但可以隐式转换为兼容的委托类型。某些 lambda 表达式也可以隐式转换为兼容的表达式树类型。

具体而言，匿名函数 F 与委托类型 D 兼容的条件是：

- 如果 F 包含 anonymous_function_signature，则 D 和 F 具有相同数量的参数。




- 如果 F 不包含 anonymous_function_signature，则 D 可以具有零个或更多任意类型的参数，只要 D 的任何参数都不具有 out 参数修饰符。
- 如果 F 具有显式类型参数列表，则 D 中的每个参数都具有与 F 中对应参数相同的类型和修饰符。
- 如果 F 具有隐式类型参数列表，则 D 没有 ref 或 out 参数。
- 如果 F 的主体是表达式，并且 D 具有 void 返回类型，或者 F 是 async 且 D 具有 «TaskType» 返回类型（§15.15.1），那么当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是有效表达式（相对于 §12），该表达式可作为 statement_expression（§13.7）使用。
- 如果 F 的主体是块，并且 D 具有 void 返回类型，或者 F 是 async 且 D 具有 «TaskType» 返回类型，那么当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是有效块（相对于 §13.3），其中没有 return 语句指定表达式。
- 如果 F 的主体是表达式，并且 F 是非 async 且 D 具有非 void 返回类型 T，或者 F 是 async 且 D 具有 «TaskType<T>» 返回类型（§15.15.1），那么当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是有效表达式（相对于 §12），该表达式可隐式转换为 T。
- 如果 F 的主体是块，并且 F 是非 async 且 D 具有非 void 返回类型 T，或者 F 是 async 且 D 具有 «TaskType<T>» 返回类型，那么当 F 的每个参数被赋予 D 中对应参数的类型时，F 的主体是有效语句块（相对于 §13.3），其结束点不可达，并且其中每个 return 语句指定的表达式都可隐式转换为 T。

示例：以下示例说明了这些规则：

```csharp
delegate void D(int x);
D d1 = delegate { };                     // Ok
D d2 = delegate() { };                   // Error, signature mismatch
D d3 = delegate(long x) { };             // Error, signature mismatch
D d4 = delegate(int x) { };              // Ok
D d5 = delegate(int x) { return; };      // Ok
D d6 = delegate(int x) { return x; };    // Error, return type mismatch
```

```csharp
delegate void E(out int x);
E e1 = delegate { };                     // Error, E has an out parameter
E e2 = delegate(out int x) { x = 1; };   // Ok
E e3 = delegate(ref int x) { x = 1; };   // Error, signature mismatch
```

```csharp
delegate int P(params int[] a);
P p1 = delegate { };                     // Error, end of block reachable
P p2 = delegate { return; };             // Error, return type mismatch
P p3 = delegate { return 1; };           // Ok
P p4 = delegate { return "Hello"; };    // Error, return type mismatch
P p5 = delegate(int[] a)                 // Ok
{
    return a[0];
};
P p6 = delegate(params int[] a)          // Error, params modifier
{
    return a[0];
};
P p7 = delegate(int[] a)    // Error, return type mismatch
{
    if (a.Length > 0) return a[0];
    return "Hello";
};

delegate object Q(params int[] a);
Q q1 = delegate(int[] a)    // Ok
{
    if (a.Length > 0) return a[0];
    return "Hello";
};
```

示例结束

示例：以下示例使用泛型委托类型 Func<A,R>，它表示一个接受类型为 A 的参数并返回类型为 R 的值的函数：

```csharp
delegate R Func<A,R>(A arg);
```

在以下赋值中

```csharp
Func<int,int> f1 = x => x + 1; // Ok
Func<int,double> f2 = x => x + 1; // Ok
Func<double,int> f3 = x => x + 1; // Error
Func<int, Task<int>> f4 = async x => x + 1; // Ok
```

每个匿名函数的参数类型和返回类型由该匿名函数所赋值到的变量的类型确定。

第一个赋值成功地将匿名函数转换为委托类型 Func<int,int>，因为当 x 被赋予类型 int 时，x + 1 是有效表达式，可隐式转换为类型 int。

同样，第二个赋值成功地将匿名函数转换为委托类型 Func<int,double>，因为 x + 1 的结果（类型为 int）可隐式转换为类型 double。

然而，第三个赋值是编译时错误，因为当 x 被赋予类型 double 时，x + 1 的结果（类型为 double）不能隐式转换为类型 int。

第四个赋值成功地将匿名异步函数转换为委托类型 Func<int, Task<int>>，因为 x + 1 的结果（类型为 int）可隐式转换为该异步 lambda 的有效返回类型 int，而该异步 lambda 的返回类型为 Task<int>。

示例结束

lambda 表达式 F 与表达式树类型 Expression<D> 兼容，如果 F 与委托类型 D 兼容。这不适用于匿名方法，只适用于 lambda 表达式。

匿名函数可能影响重载决策，并参与类型推断。更多细节见 §12.6。

### 10.7.2 匿名函数转换为委托类型的求值

将匿名函数转换为委托类型会生成一个委托实例，该实例引用匿名函数以及在求值时处于活动状态的（可能为空的）捕获外部变量集合。调用该委托时，将执行匿名函数的主体。主体中的代码使用该委托所引用的捕获外部变量集合执行。delegate_creation_expression（§12.8.16.6）可用作将匿名方法转换为委托类型的替代语法。

由匿名函数生成的委托的调用列表包含单个条目。该委托的确切目标对象和目标方法未指定。特别是，未指定该委托的目标对象是 null、外层函数成员的 this 值，还是其他某个对象。

将具有相同（可能为空的）捕获外部变量实例集合的语义相同的匿名函数转换为相同委托类型时，允许（但不要求）返回同一个委托实例。这里的“语义相同”是指：在给定相同参数的情况下，匿名函数的执行在所有情况下都会产生相同的效果。此规则允许对如下代码进行优化。

```csharp
delegate double Function(double x);
class Test
{
    static double[] Apply(double[] a, Function f)
    {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++)
        {
            result[i] = f(a[i]);
        }
        return result;
    }

    static void F(double[] a, double[] b)
    {
        a = Apply(a, (double x) => Math.Sin(x));
        b = Apply(b, (double y) => Math.Sin(y));
        ...
    }
}
```

由于这两个匿名函数委托具有相同的（空）捕获外部变量集合，并且由于这些匿名函数语义相同，编译器可以将这些委托引用同一目标方法。实际上，编译器可以从两个匿名函数表达式返回完全相同的委托实例。

### 10.7.3 lambda 表达式转换为表达式树类型的求值

将 lambda 表达式转换为表达式树类型会生成表达式树（§8.6）。更准确地说，求值 lambda 表达式转换会生成一个对象结构，该结构表示 lambda 表达式本身的结构。

并非每个 lambda 表达式都能转换为表达式树类型。转换为兼容的委托类型总是存在，但由于实现特定的原因，可能在编译时失败。

- 注意：lambda 表达式无法转换为表达式树类型的常见原因包括：
  - 它具有块主体
  - 它具有 async 修饰符
  - 它包含赋值运算符
  - 它包含 out 或 ref 参数
  - 它包含动态绑定表达式

注意结束

## 10.8 方法组转换

存在从方法组（§12.2）到兼容委托类型（§20.4）的隐式转换。如果 D 是委托类型，并且 E 是归类为方法组的表达式，则 D 与 E 兼容，当且仅当 E 包含至少一个方法，该方法以其普通形式（§12.6.4.2）适用于任何参数列表（§12.6.2），且该参数列表的类型和修饰符与 D 的参数类型和修饰符匹配，如下所述。

从方法组 E 到委托类型 D 的转换的编译时应用如下所述。

- 选择单个方法 M，对应于形式为 E(A) 的方法调用（§12.8.9.2），但有以下修改：
  - 参数列表 A 是一个表达式列表，每个表达式归类为变量，并且具有 D 的 formal_parameter_list 中对应参数的类型和修饰符（in、out 或 ref）——类型为 dynamic 的参数除外，此时对应表达式具有类型 object 而不是 dynamic。
  - 考虑的候选方法仅限于那些以其普通形式适用且不省略任何可选参数（§12.6.4.2）的方法。因此，如果候选方法仅在其展开形式下适用，或者其一个或多个可选参数在 D 中没有对应参数，则忽略这些候选方法。
- 如果 §12.8.9.2 的算法产生一个与 D 兼容（§20.4）的单一最佳方法 M，则认为存在转换。
- 如果所选方法 M 是实例方法，则与 E 关联的实例表达式确定该委托的目标对象。
- 如果所选方法 M 是通过对实例表达式进行成员访问来表示的扩展方法，则该实例表达式确定该委托的目标对象。
- 转换的结果是类型 D 的值，即引用所选方法和目标对象的委托。

示例：以下演示方法组转换：

```csharp
delegate string D1(object o);
delegate object D2(string s);
delegate object D3();
delegate string D4(object o, params object[] a);
delegate string D5(int i);
class Test
{
    static string F(object o) {...}
    static void G()
    {
        D1 d1 = F;      // Ok
        D2 d2 = F;      // Ok
    }
}
```




```
D3 d3 = F;    // Error – not applicable
D4 d4 = F;    // Error – not applicable in normal form
D5 d5 = F;    // Error – applicable but not compatible
}
```

对 d1 的赋值隐式地将方法组 F 转换为 D1 类型的值。

对 d2 的赋值展示了如何创建一个指向方法的委托，该方法具有更少派生的（逆变）参数类型和更派生的（协变）返回类型。

对 d3 的赋值展示了如果方法不适用则不存在转换的情况。

对 d4 的赋值展示了方法必须在其正常形式下适用。

对 d5 的赋值展示了委托和方法 的参数类型和返回类型仅允许在引用类型时不同。

示例结束

与所有其他隐式和显式转换一样，转换运算符可用于显式执行特定转换。

示例：因此，示例

```
object obj = new EventHandler(myDialog.OkClick);
could instead be written
object obj = (EventHandler)myDialog.OkClick;
```

示例结束

方法组转换可以引用泛型方法，要么在 E 中显式指定类型参数，要么通过类型推断（§12.6.3）。如果使用类型推断，则委托的参数类型用作推断过程中的参数类型。委托的返回类型不用于推断。无论类型参数是指定还是推断，它们都是方法组转换过程的一部分；这些是调用 resulting delegate 时用于调用目标方法的类型参数。

示例：

```
delegate int D(string s, int i);
delegate int E();

class X
{
    public static T F<T>(string s, T t) {...}
    public static T G<T>() {...}

    static void Main()
    {
        D d1 = F<int>;    // Ok, type argument given explicitly
        D d2 = F;         // Ok, int inferred as type argument
        E e1 = G<int>;    // Ok, type argument given explicitly
        E e2 = G;         // Error, cannot infer from return type
    }
}
```

示例结束

方法组可能会影响重载解析，并参与类型推断。有关更多详细信息，请参阅 §12.6。

方法组转换的运行时求值按如下方式进行：

- 如果在编译时选择的方法是实例方法，或者它是作为实例方法访问的扩展方法，则委托的目标对象由与 E 关联的实例表达式确定：
  - 实例表达式会被求值。如果此求值导致异常，则不再执行后续步骤。
  - 如果实例表达式是 reference_type，则实例表达式计算得到的值成为目标对象。如果所选方法是实例方法且目标对象为 null，则会抛出 System.NullReferenceException，并且不再执行后续步骤。
  - 如果实例表达式是 value_type，则会执行装箱操作（§10.2.9）将值转换为对象，并且该对象成为目标对象。
- 否则，所选方法属于静态方法调用，委托的目标对象为 null。
- 使用在编译时确定的方法的引用以及上面计算得到的目标对象的引用，获得 delegate type D 的委托实例，如下所示：
  - 允许（但不是必需）使用已包含这些引用的现有委托实例。
  - 如果未重用现有实例，则会创建一个新实例（§20.5）。如果没有足够的内存来分配新实例，则会抛出 System.OutOfMemoryException。否则实例会使用给定的引用进行初始化。

# 11. 模式和模式匹配

### 11.1 通用

模式是一种语法形式，可与 is 运算符（§12.12.12）一起使用，也可在 switch_statement（§13.8.3）中使用，以表达要与传入数据进行比较的数据形状。模式会针对 switch 语句的表达式进行测试，或针对 is 运算符左侧的 relational_expression 进行测试，其中每一个都称为模式输入值。

### 11.2 模式形式

#### 11.2.1 通用

模式可能具有以下形式之一：

```
pattern
  : declaration_pattern
  | constant_pattern
  | var_pattern
  ;
```

declaration_pattern 和 var_pattern 可能导致局部变量的声明。

每个模式形式定义了模式可应用于的输入值的类型集合。如果类型 T 在模式可能匹配的值的类型中，则模式 P 可应用于类型 T。如果模式 P 在程序中出现以匹配类型为 T 的模式输入值（§11.1），而 P 不适用于 T，则为编译时错误。

每个模式形式定义了模式在运行时匹配值的取值集合。

#### 11.2.2 声明模式

declaration_pattern 用于测试值是否具有给定类型，如果测试成功，则以该类型变量的形式提供该值。

```
declaration_pattern
  : type simple_designation
  ;
simple_designation
  : single_variable_designation
  ;
single_variable_designation
  : identifier
  ;
```

值的运行时类型使用 is-type 运算符（§12.12.12.1）中指定的相同规则与模式中的类型进行测试。如果测试成功，则模式匹配该值。如果类型为可空值类型（§8.3.12），则为编译时错误。此模式形式永远不会匹配 null 值。

注意：is-type 表达式 e is T 与声明模式 e is T _ 在 T 不是可空类型时是等价的。 注意结束

给定一个模式输入值（§11.1）e，如果 simple_designation 是标识符 _，则它表示一个丢弃（§9.2.9.1），并且 e 的值不会绑定到任何内容。（尽管此时作用域中可能存在名为 _ 的已声明变量，但在该上下文中不会看到该命名变量。）如果 simple_designation 是任何其他标识符，则会引入一个由给定标识符命名的给定类型的局部变量（§9.2.9）。当模式匹配该值时，该局部变量会被赋予模式输入值的值。

模式输入值的静态类型与给定类型的某些组合被视为不兼容，并导致编译时错误。如果从 E 到 T 存在恒等转换、隐式或显式引用转换、装箱转换或拆箱转换，或者 E 或 T 中的任一个是开放类型（§8.4.3），则静态类型为 E 的值被认为是与类型 T 模式兼容。命名类型 T 的声明模式适用于 E 与 T 模式兼容的每个类型 E。

注意：对开放类型的支持在检查可能为 struct 类型或 class 类型的类型时最有用，并且应避免装箱。 注意结束

示例：声明模式对于执行引用类型的运行时类型测试很有用，并取代了以下惯用法

```
var v = expr as Type;
if (v != null) { /* code using v */ }
```

用稍微更简洁的

```
if (expr is Type v) { /* code using v */ }
```

示例结束

如果类型是可空值类型，则为错误。

示例：声明模式可用于测试可空类型的值：类型为 Nullable<T>（或装箱的 T）的值与类型模式 T2 匹配，如果该值非空且 T2 是 T，或 T 的某个基类型或接口。例如，在以下代码片段中

```
int? x = 3;
if (x is int v) { /* code using v */ }
```

if 语句的条件在运行时为真，并且变量 v 在块内保存类型为 int 的值 3。 示例结束

#### 11.2.3 常量模式

constant_pattern 用于将模式输入值（§11.1）的值与给定的常量值进行测试。

```
constant_pattern
  : constant_expression
  ;
```

如果常量表达式 P 可以隐式转换为类型 T，则常量模式 P 可应用于类型 T。

对于常量模式 P，其转换值是

- 如果模式输入值的类型是整型或枚举类型，则为模式的常量值转换为该类型；否则
- 如果模式输入值的类型是整型或枚举类型的可空版本，则为模式的常量值转换为其底层类型；否则
- 为模式的常量值的值。

给定一个模式输入值 e 和具有转换值 v 的常量模式 P，

- 如果 e 具有整型或枚举类型，或其中之一的可空形式，并且 v 具有整型，则当表达式 e == v 的结果为 true 时，模式 P 匹配值 e；否则，如果 object.Equals(e, v) 返回 true，则模式 P 匹配值 e。

示例：以下方法中的 switch 语句在其 case 标签中使用了五个常量模式。

```
static decimal GetGroupTicketPrice(int visitorCount)
{
    switch (visitorCount)
    {
        case 1: return 12.0m;
        case 2: return 20.0m;
        case 3: return 27.0m;
        case 4: return 32.0m;
        case 0: return 0.0m;
        default: throw new ArgumentException(...);
    }
}
```

示例结束

### 11.2.4 var 模式

var 模式匹配每个值。也就是说，使用 var 模式的模式匹配操作总是成功。

var 模式可应用于每种类型。

```
var_pattern
    : 'var' designation
    ;
designation
    : simple_designation
    ;
```

给定一个模式输入值 (§11.1) e，如果 designation 是标识符 _，则它表示一个丢弃 (§9.2.9.1)，并且 e 的值不会绑定到任何东西。 （尽管此时作用域中可能存在同名声明的变量，但该命名变量在此上下文中不可见。）如果 designation 是任何其他标识符，则在运行时，e 的值会被绑定到一个新引入的局部变量 (§9.2.9)，该变量的名称为 designation，其类型为 e 的静态类型，并且模式输入值会被分配给该局部变量。

如果在 var 模式使用的地方名称 var 会绑定到一个类型，则为错误。

### 11.3 模式包含

在 switch 语句中，如果某个 case 的模式被前面一组未受保护的 case (§13.8.3) 所包含，则为错误。直观地说，这意味着任何输入值都将被之前的某个 case 匹配。以下规则定义了何时一组模式包含给定的模式。

模式 P 会匹配常量 k，如果该模式运行时行为的规范是 P 匹配 k。

一组模式 Q 包含模式 P，如果满足以下任一条件：

- P 是常量模式，并且集合 Q 中的某个模式会匹配 P 的转换值
- P 是 var 模式，并且模式集合 Q 对模式输入值 (§11.1) 的类型是穷尽的 (§11.4)，并且模式输入值不是可空类型，或者 Q 中的某个模式会匹配 null。
- P 是具有类型 T 的声明模式，并且模式集合 Q 对类型 T 是穷尽的 (§11.4)。

### 11.4 模式穷尽性

直观地说，一组模式对于一种类型是穷尽的，如果该集合中的某个模式适用于该类型的每个可能值，除了 null。以下规则定义了何时一组模式对于一种类型是穷尽的：

一组模式 Q 对于类型 T 是穷尽的，如果满足以下任一条件：

- 1. T 是整型或枚举类型，或其中之一的可空版本，并且对于 T 的非可空底层类型的每个可能值，Q 中的某个模式会匹配该值；或
- 2. Q 中的某个模式是 var 模式；或
- 3. Q 中的某个模式是类型 D 的声明模式，并且从 T 到 D 存在恒等转换、隐式引用转换或装箱转换。

*示例：*

```
static void M(byte b)
{
    switch (b) {
        case 0: case 1: case 2: ... // handle every specific value of byte
            break;
        // error: the pattern 'byte other' is subsumed by the (exhaustive)
        // previous cases
        case byte other:
            break;
    }
}
```

*示例结束*

# 12. 表达式

### 12.1 通用

表达式是一系列运算符和操作数。本条款定义了表达式的语法、操作数和运算符的求值顺序以及表达式的含义。

### 12.2 表达式分类

### 12.2.1 通用

表达式的结果被归类为以下之一：

- 一个值。每个值都有一个关联的类型。
- 一个变量。除非另有说明，变量是显式类型的，并且具有关联的类型，即变量的声明类型。隐式类型变量没有关联的类型。
- 一个 null 字面量。此分类的表达式可以隐式转换为引用类型或可空值类型。
- 一个匿名函数。此分类的表达式可以隐式转换为兼容的委托类型或表达式树类型。
- 一个元组。每个元组都有固定数量的元素，每个元素都有一个表达式和一个可选的元组元素名称。
- 一个属性访问。每个属性访问都有一个关联的类型，即属性的类型。此外，属性访问可能具有关联的实例表达式。当实例属性访问的访问器被调用时，评估实例表达式的结果成为由 `this` 表示的实例 (§12.8.13)。
- 一个索引器访问。每个索引器访问都有一个关联的类型，即索引器的元素类型。此外，索引器访问具有关联的实例表达式和关联的参数列表。当索引器访问的访问器被调用时，评估实例表达式的结果成为由 `this` 表示的实例 (§12.8.13)，并且评估参数列表的结果成为调用的参数列表。
- 无。这发生在表达式是对返回类型为 `void` 的方法的调用时。分类为无的表达式仅在 `statement_expression` (§13.7) 的上下文中有效，或作为 `lambda_expression` (§12.19) 的主体。

对于作为较大表达式的子表达式出现的表达式，在所述限制下，结果还可以归类为以下之一：

- 一个命名空间。此分类的表达式只能作为 `member_access` (§12.8.7) 的左手侧出现。在任何其他上下文中，分类为命名空间的表达式会导致编译时错误。
- 一个类型。此分类的表达式只能作为 member_access (§12.8.7) 的左手侧出现。在任何其他上下文中，分类为类型的表达式会导致编译时错误。
- 一个方法组，即成员查找 (§12.5) 的结果是一组重载方法。方法组可能具有关联的实例表达式和关联的类型参数列表。当实例方法被调用时，评估实例表达式的结果成为由 this 表示的实例 (§12.8.13)。方法组允许在 invocation_expression (§12.8.9) 或 delegate_creation_expression (§12.8.16.6) 中使用，并且可以隐式转换为兼容的委托类型 (§10.8)。在任何其他上下文中，分类为方法组的表达式会导致编译时错误。
- 一个事件访问。每个事件访问都有一个关联的类型，即事件的类型。此外，事件访问可能具有关联的实例表达式。事件访问可以作为 += 和 -= 运算符 (§12.21.5) 的左操作数出现。在任何其他上下文中，分类为事件访问的表达式会导致编译时错误。当实例事件访问的访问器被调用时，评估实例表达式的结果成为由 this 表示的实例 (§12.8.13)。
- 一个 throw 表达式，可在多个上下文中使用以在表达式中抛出异常。throw 表达式可通过隐式转换转换为任何类型。

属性访问或索引器访问始终通过执行 get_accessor 或 set_accessor 的调用重新分类为值。特定访问器的确定取决于属性或索引器访问的上下文：如果访问是赋值的目标，则调用 set_accessor 以分配新值 (§12.21.2)。否则，调用 get_accessor 以获取当前值 (§12.2.2)。

实例访问器是实例上的属性访问、实例上的事件访问或索引器访问。

### 12.2.2 表达式的值

涉及表达式的大多数构造最终要求表达式表示一个值。在这种情况下，如果实际表达式表示命名空间、类型、方法组或无，则会发生编译时错误。但是，如果表达式表示属性访问、索引器访问或变量，则会隐式替换属性、索引器或变量的值：

- 变量的值只是当前存储在变量标识的存储位置中的值。在获取变量的值之前，变量应被视为已明确赋值 (§9.4)，否则会发生编译时错误。
- 属性访问表达式的值是通过调用属性的 get_accessor 获得的。如果属性没有 get_accessor，则会发生编译时错误。否则，执行函数成员调用 (§12.6.6)，并且调用的结果成为属性访问表达式的值。
- 索引器访问表达式的值是通过调用索引器的 get_accessor 获得的。如果索引器没有 get_accessor，则会发生编译时错误。否则，使用与索引器访问表达式关联的参数列表执行函数成员调用 (§12.6.6)，并且调用的结果成为索引器访问表达式的值。
- 元组表达式的值是通过将隐式元组转换 (§10.2.13) 应用于元组表达式的类型获得的。获取没有类型的元组表达式的值是错误。




## 12.3 静态绑定与动态绑定

### 12.3.1 通用

绑定是根据表达式（参数、操作数、接收者）的类型或值来确定操作所指对象的过程。例如，方法调用的绑定是根据接收者和参数的类型确定的。运算符的绑定是根据其操作数的类型确定的。

在 C# 中，操作的绑定通常在编译时确定，基于其子表达式的编译时类型。同样，如果表达式包含错误，该错误会被编译器检测并报告。这种方法称为静态绑定。

然而，如果一个表达式是动态表达式（即类型为 dynamic），则表示其参与的任何绑定都应基于其运行时类型而不是编译时类型。因此，此类操作的绑定被推迟到程序运行期间执行操作时。这被称为动态绑定。

当操作被动态绑定时，编译器几乎不进行检查。相反，如果运行时绑定失败，则错误会在运行时作为异常报告。

C# 中以下操作受绑定影响：

- Member access: `e.M`
- Method invocation: `e.M(e1, ..., ev)`
- Delegate invocation: `e(e1, ..., ev)`
- Element access: `e[e1, ..., ev]`
- Object creation: `new C(e1, ..., ev)`
- Overloaded unary operators: `+`, `-`, `!`, `~`, `++`, `--`, `true`, `false`
- Overloaded binary operators: `+`, `-`, `*`, `/`, `%`, `&`, `&&`, `|`, `||`, `??`, `^`, `<<`, `>>`, `==`, `!=`, `<`, `>`, `<=`, `>=`
- Assignment operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`
- Implicit and explicit conversions

当不涉及动态表达式时，C# 默认使用静态绑定，这意味着在选择过程中使用子表达式的编译时类型。然而，当上述操作中的一个子表达式是动态表达式时，该操作改为动态绑定。

如果方法调用被动态绑定，并且任何参数（包括接收者）具有 in 修饰符，则为编译时错误。

### 12.3.2 绑定时间

静态绑定发生在编译时，而动态绑定发生在运行时。在以下小节中，术语绑定时间指的是绑定发生时的编译时或运行时。

示例：以下说明了静态绑定、动态绑定和绑定时间的概念：

```csharp
object o = 5;
dynamic d = 5;
Console.WriteLine(5); // static binding to Console.WriteLine(int)
Console.WriteLine(o); // static binding to Console.WriteLine(object)
Console.WriteLine(d); // dynamic binding to Console.WriteLine(int)
```

前两次调用是静态绑定的：Console.WriteLine 的重载是基于其参数的编译时类型选择的。因此，绑定时间为编译时。

第三次调用是动态绑定的：Console.WriteLine 的重载是基于其参数的运行时类型选择的。这是因为参数是动态表达式——其编译时类型为 dynamic。因此，第三次调用的绑定时间为运行时。

示例结束

### 12.3.3 动态绑定

**本小节为说明性内容。**

动态绑定允许 C# 程序与动态对象交互，即不遵循 C# 类型系统正常规则的对象。动态对象可能是来自具有不同类型系统的其他编程语言的对象，也可能是以编程方式设置以实现不同操作的自身绑定语义的对象。

动态对象实现其自身语义的机制是实现定义的。动态对象实现的一个给定接口——同样是实现定义的——用于向 C# 运行时发出信号，表明它们具有特殊语义。因此，只要对动态对象的操作是动态绑定的，其自身的绑定语义，而不是本规范中指定的 C# 语义，就会接管。

虽然动态绑定的目的是允许与动态对象互操作，但 C# 允许对所有对象进行动态绑定，无论它们是否动态。这使得动态对象的集成更加顺畅，因为对其操作的結果本身可能不是动态对象，但仍是编译时程序员未知类型的对象。此外，即使涉及的对象都不是动态对象，动态绑定也可以帮助消除易出错的基于反射的代码。

### 12.3.4 子表达式的类型

当操作是静态绑定时，子表达式（例如接收者、参数、索引或操作数）的类型始终被视为该表达式的编译时类型。

当操作是动态绑定时，子表达式的类型根据子表达式的编译时类型以不同方式确定：

- 编译时类型为 dynamic 的子表达式被认为具有该表达式在运行时求值时实际值的类型
- 编译时类型为类型参数的子表达式被认为具有该类型参数在运行时绑定的类型
- 否则，子表达式被认为具有其编译时类型。

## 12.4 运算符

### 12.4.1 通用

表达式由操作数和运算符构造。表达式的运算符指示要对操作数应用哪些操作。

示例：运算符的示例包括 +、-、*、/ 和 new。操作数的示例包括字面量、字段、局部变量和表达式。示例结束

运算符有三种类型：

- 一元运算符。一元运算符接受一个操作数，并使用前缀表示法（例如 -x）或后缀表示法（例如 x++）。
- 二元运算符。二元运算符接受两个操作数，且全部使用中缀表示法（例如 x + y）。
- 三元运算符。只有一个三元运算符 ?:；它接受三个操作数并使用中缀表示法（c ? x : y）。

表达式中运算符的求值顺序由运算符的优先级和结合性决定（§12.4.2）。

表达式中的操作数按从左到右的顺序求值。

示例：在 F(i) + G(i++) * H(i) 中，方法 F 使用 i 的旧值调用，然后方法 G 使用 i 的旧值调用，最后方法 H 使用 i 的新值调用。这与运算符优先级无关且独立。示例结束

某些运算符可以重载。运算符重载（§12.4.3）允许为一个或两个操作数属于用户定义类或结构类型的操作指定用户定义的运算符实现。

### 12.4.2 运算符优先级和结合性

当表达式包含多个运算符时，运算符的优先级控制各个运算符求值的顺序。

注：例如，表达式 x + y * z 被求值为 x + (y * z)，因为 * 运算符的优先级高于二元 + 运算符。注结束

运算符的优先级由其相关语法产生的定义确定。

注：例如，additive_expression 由乘法表达式序列组成，这些表达式由 + 或 - 运算符分隔，因此 + 和 - 运算符的优先级低于 *、/ 和 % 运算符。注结束

注：下表按从高到低的顺序总结了所有运算符：

| 小节 | 类别 | 运算符 |
|---|---|---|
| §12.8 | 主 | x.y x?.y f(x) a[x] a?[x] x++ x-- new typeof default checked unchecked delegate stackalloc |
| §12.9 | 一元 | + - ! ~ ++x --x (T)x await x |
| §12.10 | 乘法 | * / % |
| §12.10 | 加法 | + - |
| §12.11 | 移位 | << >> |
| §12.12 | 关系和类型测试 | < > <= >= is as |
| §12.12 | 相等 | == != |
| §12.13 | 逻辑与 | & |
| §12.13 | 逻辑异或 | ^ |




| § | 说明 | 运算符 |
|---|---|---|
| §12.13 | 逻辑或 |  |
| §12.14 | 条件与 | && |
| §12.14 | 条件或 | \|\| |
| §12.15 和 §12.16 | 空合并与抛出表达式 | ?? throw x |
| §12.18 | 条件 | ?: |
| §12.21 和 §12.19 | 赋值与 Lambda 表达式 | = *= /= %= += -= <<= >>= &= ^= \|= => |

*结束注释*

当一个操作数出现在两个具有相同优先级的运算符之间时，运算符的*结合性*控制操作的执行顺序：

- 除赋值运算符和空合并运算符外，所有二元运算符都是*左结合*的，即操作从左向右执行。
  *示例：x + y + z 按 (x + y) + z 计算。结束示例*
- 赋值运算符、空合并运算符和条件运算符（?:）是*右结合*的，即操作从右向左执行。
  *示例：x = y = z 按 x = (y = z) 计算。结束示例*

可以使用括号控制优先级和结合性。

*示例：x + y * z 先将 y 乘以 z，然后将结果加到 x；而 (x + y) * z 先将 x 和 y 相加，然后将结果乘以 z。结束示例*

## 12.4.3 运算符重载

所有一元和二元运算符都有预定义实现。此外，可以通过在类和结构体中包含运算符声明（§15.10）来引入用户定义的实现。用户定义的运算符实现始终优先于预定义的运算符实现：只有在没有适用的用户定义运算符实现时，才会考虑预定义的运算符实现，如 §12.4.4 和 §12.4.5 所述。

可重载的一元运算符是：

```
+ - ! ~ ++ -- true false
```

*注释：尽管 true 和 false 不在表达式中显式使用（因此未包含在 §12.4.2 的优先级表中），但它们被视为运算符，因为在若干表达式上下文中会调用它们：布尔表达式（§12.24）以及涉及条件（§12.18）和条件逻辑运算符（§12.14）的表达式。结束注释*

可重载的二元运算符是：

```
+ - * / % & | ^ << >> == != > < <= >=
```

只有上面列出的运算符可以被重载。特别是，不能重载成员访问、方法调用，或 =、&&、||、??、?:、>、checked、unchecked、new、typeof、default、as 和 is 运算符。

当二元运算符被重载时，相应的复合赋值运算符（如果有）也会被隐式重载。

示例：对 operator * 的重载也是对 operator *= 的重载。这将在 §12.21 中进一步说明。结束示例

赋值运算符本身（=）不能被重载。赋值始终执行将值简单地存储到变量中的操作（§12.21.2）。

强制转换操作（如 (T)x）可通过提供用户定义的转换（§10.5）来重载。

> 注释：用户定义的转换不会影响 is 或 as 运算符的行为。结束注释

元素访问（如 a[x]）不被视为可重载的运算符。相反，用户定义的索引通过索引器（§15.9）支持。

在表达式中，运算符使用运算符表示法引用；在声明中，运算符使用函数表示法引用。下表显示了一元和二元运算符的运算符表示法与函数表示法之间的关系。在第一个条目中，「op」表示任何可重载的一元前缀运算符。在第二个条目中，「op」表示一元后缀 ++ 和 -- 运算符。在第三个条目中，「op」表示任何可重载的二元运算符。

> 注释：有关重载 ++ 和 -- 运算符的示例，请参阅 §15.10.2。结束注释

| 运算符表示法 | 函数表示法 |
|---|---|
| «op» x | operator «op»(x) |
| x «op» | operator «op»(x) |
| x «op» y | operator «op»(x, y) |

用户定义的运算符声明始终要求至少有一个参数的类型是包含该运算符声明的类或结构体类型。

> 注释：因此，用户定义的运算符不可能与预定义运算符具有相同的签名。结束注释

用户定义的运算符声明不能修改运算符的语法、优先级或结合性。

示例：/ 运算符始终是二元运算符，始终具有 §12.4.2 中规定的优先级级别，并且始终是左结合的。结束示例

> 注释：虽然用户定义的运算符可以执行任意计算，但强烈不鼓励产生与直觉预期不符的结果的实现。例如，operator == 的实现应比较两个操作数是否相等，并返回适当的 bool 结果。结束注释

§12.9 至 §12.21 中对各个运算符的描述规定了运算符的预定义实现以及适用于每个运算符的任何附加规则。这些描述使用了“一元运算符重载决策”、“二元运算符重载决策”、“数值提升”和“提升运算符”等术语，其定义见以下子条款。

## 12.4.4 一元运算符重载决策

形式为 «op» x 或 x «op» 的操作，其中 «op» 是可重载的一元运算符，x 是类型为 X 的表达式，按如下方式处理：

- 使用 §12.4.6 的规则确定 X 为操作 operator «op»(x) 提供的候选用户定义运算符集合。
- 如果候选用户定义运算符集合不为空，则该集合成为操作的候选运算符集合。否则，预定义的二元运算符 «op» 实现（包括其提升形式）成为操作的候选运算符集合。给定运算符的预定义实现在该运算符的描述中规定。仅当任一操作数的绑定期类型（如果是可空类型，则为其基础类型）是枚举或委托类型时，枚举或委托类型提供的预定义运算符才会包含在此集合中。
- 将 §12.6.4 的重载决策规则应用于候选运算符集合，以针对参数列表 (x, y) 选择最佳运算符，该运算符成为重载决策过程的结果。如果重载决策未能选择出唯一的最佳运算符，则发生绑定期错误。

## 12.4.5 二元运算符重载决策

形式为 x «op» y 的操作，其中 «op» 是可重载的二元运算符，x 是类型为 X 的表达式，y 是类型为 Y 的表达式，按如下方式处理：

- 确定 X 和 Y 为操作 operator «op»(x, y) 提供的候选用户定义运算符集合。该集合由 X 提供的候选运算符与 Y 提供的候选运算符的并集组成，每个均按 §12.4.6 的规则确定。对于合并后的集合，候选运算符按如下方式合并：
  - 如果 X 和 Y 是相同类型，或者 X 和 Y 派生自公共基类型，则共享的候选运算符在合并后的集合中只出现一次。
  - 如果 X 和 Y 之间存在恒等转换，并且 Y 提供的运算符 «op»Y 与 X 提供的 «op»X 具有相同的返回类型，且 «op»Y 的操作数类型与 «op»X 的相应操作数类型之间存在恒等转换，则集合中只出现 «op»X。
- 如果候选用户定义运算符集合不为空，则该集合成为操作的候选运算符集合。否则，预定义的二元运算符 «op» 实现（包括其提升形式）成为操作的候选运算符集合。给定运算符的预定义实现在该运算符的描述中规定。对于预定义的枚举和委托运算符，仅考虑由作为某个操作数绑定期类型的枚举或委托类型提供的运算符。
- 将 §12.6.4 的重载决策规则应用于候选运算符集合，以针对参数列表 (x, y) 选择最佳运算符，该运算符成为重载决策过程的结果。如果重载决策未能选择出唯一的最佳运算符，则发生绑定期错误。

## 12.4.6 候选用户定义运算符

给定类型 T 和操作 operator «op»(A)，其中 «op» 是可重载运算符，A 是参数列表，T 为 operator «op»(A) 提供的候选用户定义运算符集合按如下方式确定：

- 确定类型 T₀。如果 T 是可空值类型，则 T₀ 是其基础类型；否则，T₀ 等于 T。
- 对于 T₀ 中所有 operator «op» 声明以及此类运算符的所有提升形式，如果至少有一个运算符相对于参数列表 A 是可适用的（§12.6.4.2），则候选运算符集合由 T₀ 中所有此类可适用的运算符组成。
- 否则，如果 T₀ 是 object，则候选运算符集合为空。




- 否则，T₀ 所提供的候选运算符集合，是 T₀ 的直接基类所提供的候选运算符集合；如果 T₀ 是类型参数，则是 T₀ 的有效基类所提供的候选运算符集合。

## 12.4.7 数值提升

### 12.4.7.1 概述

**本子条款为资料性内容。**

§12.4.7 及其子条款是对以下内容综合效果的概述：

- 隐式数值转换的规则（§10.2.3）；
- 更好的转换规则（§12.6.4.7）；以及
- 可用的算术（§12.10）、关系（§12.12）和整型逻辑（§12.13.2）运算符。

数值提升包括自动对预定义一元和二元数值运算符的操作数执行某些隐式转换。数值提升并不是一种独立的机制，而是将重载决策应用于预定义运算符所产生的一种效果。数值提升特别不会影响用户定义运算符的求值，尽管可以实现用户定义运算符来表现出类似的效果。

作为数值提升的一个示例，请考虑二元 * 运算符的预定义实现：

```
int operator *(int x, int y);
uint operator *(uint x, uint y);
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
float operator *(float x, float y);
double operator *(double x, double y);
decimal operator *(decimal x, decimal y);
```

当重载决策规则（§12.6.4）应用于这组运算符时，其效果是选择第一个存在从操作数类型进行隐式转换的运算符。

> *示例：* 对于操作 b * s，其中 b 是 byte，s 是 short，重载决策选择运算符 *(int, int) 作为最佳运算符。因此，效果是 b 和 s 被转换为 int，且结果的类型为 int。同样，对于操作 i * d，其中 i 是 int，d 是 double，重载决策选择运算符 *(double, double) 作为最佳运算符。示例结束

**资料性文本结束。**

### 12.4.7.2 一元数值提升

**本子条款为资料性内容。**

一元数值提升发生在预定义 +、– 和 ~ 一元运算符的操作数上。一元数值提升仅仅包括将 sbyte、byte、short、ushort 或 char 类型的操作数转换为 int 类型。此外，对于一元 – 运算符，一元数值提升会将 uint 类型的操作数转换为 long 类型。

**资料性文本结束。**

### 12.4.7.3 二元数值提升

**本子条款为资料性内容。**

二元数值提升发生在预定义 +、-、*、/、%、&、|、^、==、!=、>、<、>= 和 <= 二元运算符的操作数上。二元数值提升将两个操作数隐式转换为一个公共类型；对于非关系运算符，该公共类型也会成为运算的结果类型。二元数值提升包括按以下规则出现的顺序应用这些规则：

- 如果任一操作数为 `decimal` 类型，则将另一操作数转换为 `decimal` 类型；如果另一操作数为 `float` 或 `double` 类型，则发生绑定期错误。
- 否则，如果任一操作数为 `double` 类型，则将另一操作数转换为 `double` 类型。
- 否则，如果任一操作数为 `float` 类型，则将另一操作数转换为 `float` 类型。
- 否则，如果任一操作数为 `ulong` 类型，则将另一操作数转换为 `ulong` 类型；如果另一操作数为 `sbyte`、`short`、`int` 或 `long` 类型，则发生绑定期错误。
- 否则，如果任一操作数为 `long` 类型，则将另一操作数转换为 `long` 类型。
- 否则，如果任一操作数为 `uint` 类型且另一操作数为 `sbyte`、`short` 或 `int` 类型，则两个操作数都转换为 `long` 类型。
- 否则，如果任一操作数为 `uint` 类型，则将另一操作数转换为 `uint` 类型。
- 否则，两个操作数都转换为 `int` 类型。

*注意：* 第一条规则不允许任何将 `decimal` 类型与 `double` 和 `float` 类型混合的运算。该规则源于以下事实：`decimal` 类型与 `double` 和 `float` 类型之间不存在隐式转换。*注意结束*

*注意：* 还要注意，当一个操作数为有符号整型类型时，另一个操作数不可能为 `ulong` 类型。原因在于不存在一种整型类型能够同时表示 `ulong` 的完整范围和有符号整型类型的范围。*注意结束*

在上述两种情况下，都可以使用强制转换表达式将一个操作数显式转换为与另一操作数兼容的类型。

*示例：* 在以下代码中

```csharp
decimal AddPercent(decimal x, double percent) =>
    x * (1.0 + percent / 100.0);
```

发生绑定期错误，因为 `decimal` 不能与 `double` 相乘。通过将第二个操作数显式转换为 `decimal` 可以解决该错误，如下所示：

```csharp
decimal AddPercent(decimal x, double percent) =>
    x * (decimal)(1.0 + percent / 100.0);
```

*示例结束*

**资料性文本结束。**

## 12.4.8 提升运算符

*提升运算符* 允许作用于非可空值类型的预定义运算符和用户定义运算符也用于这些类型的可空形式。提升运算符由满足特定要求的预定义运算符和用户定义运算符构造，如下所述：

- 对于一元运算符 +、++、-、--、! 和 ~，如果操作数和结果类型都是非可空值类型，则存在运算符的提升形式。提升形式通过向操作数和结果类型添加单个 ? 修饰符来构造。如果操作数为 null，则提升运算符生成 `null` 值。否则，提升运算符解包操作数，应用基础运算符，并包装结果。
- 对于二元运算符 +、-、*、/、%、&、|、^、<< 和 >>，如果操作数和结果类型均为非可空值类型，则存在运算符的提升形式。提升形式通过向每个操作数和结果类型添加单个 ? 修饰符来构造。如果一个或两个操作数为 null，则提升运算符生成 null 值（例外是 bool? 类型的 & 和 | 运算符，如 §12.13.5 所述）。否则，提升运算符解包操作数，应用基础运算符，并包装结果。
- 对于相等运算符 == 和 !=，如果操作数类型都是非可空值类型且结果类型为 bool，则存在运算符的提升形式。提升形式通过向每个操作数类型添加单个 ? 修饰符来构造。提升运算符认为两个 null 值相等，而 null 值与任何非 null 值不相等。如果两个操作数都非 null，则提升运算符解包操作数并应用基础运算符以生成 bool 结果。
- 对于关系运算符 <、>、<= 和 >=，如果操作数类型都是非可空值类型且结果类型为 bool，则存在运算符的提升形式。提升形式通过向每个操作数类型添加单个 ? 修饰符来构造。如果一个或两个操作数为 null，则提升运算符生成 false 值。否则，提升运算符解包操作数并应用基础运算符以生成 bool 结果。

## 12.5 成员查找

### 12.5.1 概述

成员查找是确定类型上下文中名称含义的过程。成员查找可以作为表达式中对 simple_name（§12.8.4）或 member_access（§12.8.7）求值的一部分发生。如果 simple_name 或 member_access 作为 invocation_expression（§12.8.9.2）的 primary_expression 出现，则称该成员被调用。

如果成员是方法或事件，或者它是委托类型（§20）或 dynamic 类型（§8.2.4）的常量、字段或属性，则称该成员可调用。

成员查找不仅考虑成员的名称，还考虑成员所具有的类型参数数量以及成员是否可访问。出于成员查找的目的，泛型方法和嵌套泛型类型具有其各自声明中所指示的类型参数数量，而所有其他成员具有零个类型参数。

在类型 T 中对具有 K 个类型实参的名称 N 进行成员查找，处理如下：

- 首先，确定一组名为 N 的可访问成员：
  - 如果 T 是类型参数，则该集合是对 T 指定为主要约束或次要约束（§15.2.5）的每个类型中名为 N 的可访问成员集合的并集，以及 object 中名为 N 的可访问成员集合。
  - 否则，该集合由 T 中所有名为 N 的可访问（§7.5）成员组成，包括继承成员以及 object 中名为 N 的可访问成员。如果 T 是构造类型，则成员集合通过按 §15.3.3 所述替换类型实参来获得。包含 override 修饰符的成员被排除在该集合之外。
- 接下来，如果 K 为零，则移除所有声明中包含类型参数的嵌套类型。如果 K 不为零，则移除所有具有不同数量类型参数的成员。当 K 为零时，

具有类型参数的方法不会被移除，因为类型推断过程（§12.6.3）可能能够推断出类型实参。

- 接下来，如果该成员被调用，则从集合中移除所有不可调用成员。
- 接下来，从集合中移除被其他成员隐藏的成员。对于集合中的每个成员 S.M（其中 S 是声明成员 M 的类型），应用以下规则：
  - 如果 M 是常量、字段、属性、事件或枚举成员，则从集合中移除在 S 的基类型中声明的所有成员。
  - 如果 M 是类型声明，则从集合中移除在 S 的基类型中声明的所有非类型声明，并且从集合中移除在 S 的基类型中声明的、与 M 具有相同类型参数数量的所有类型声明。
  - 如果 M 是方法，则从集合中移除在 S 的基类型中声明的所有非方法成员。
- 接下来，从集合中移除被类成员隐藏的接口成员。仅当 T 是类型参数，并且 T 同时具有一个不是 object 的有效基类和一个非空有效接口集（§15.2.5）时，此步骤才会生效。对于集合中的每个成员 S.M（其中 S 是声明成员 M 的类型），如果 S 是除 object 以外的类声明，则应用以下规则：
  - 如果 M 是常量、字段、属性、事件、枚举成员或类型声明，则从集合中移除在接口声明中声明的所有成员。
  - 如果 M 是方法，则从集合中移除在接口声明中声明的所有非方法成员，并且从集合中移除在接口声明中声明的与 M 具有相同签名的所有方法。
- 最后，在移除隐藏成员后，确定查找结果：
  - 如果该集合仅包含一个不是方法的成员，则该成员就是查找结果。
  - 否则，如果该集合只包含方法，则这组方法就是查找结果。
  - 否则，查找有歧义，并发生绑定时间错误。

对于除类型参数和接口以外的类型中的成员查找，以及在严格单继承的接口（继承链中的每个接口恰好有零个或一个直接基接口）中的成员查找，查找规则的效果只是派生成员隐藏具有相同名称或签名的基成员。此类单继承查找从不会有歧义。多继承接口中的成员查找可能引起的歧义在 §18.4.6 中描述。

注意：此阶段只考虑一种歧义。如果成员查找的结果是一个方法组，那么方法组的进一步使用可能会因歧义而失败，例如 §12.6.4.1 和 §12.6.2 中所述。结束注。

## 12.5.2 基类型

出于成员查找的目的，类型 T 被视为具有以下基类型：

- 如果 T 是 object 或 dynamic，则 T 没有基类型。
- 如果 T 是 enum_type，则 T 的基类型是类类型 System.Enum、System.ValueType 和 object。
- 如果 T 是 struct_type，则 T 的基类型是类类型 System.ValueType 和 object。注意：nullable_value_type 是 struct_type（§8.3.1）。结束注。
- 如果 T 是 class_type，则 T 的基类型是 T 的基类，包括类类型 object。
- 如果 T 是 interface_type，则 T 的基类型是 T 的基接口和类类型 object。
- 如果 T 是 array_type，则 T 的基类型是类类型 System.Array 和 object。
- 如果 T 是 delegate_type，则 T 的基类型是类类型 System.Delegate 和 object。

## 12.6 函数成员

### 12.6.1 概述

函数成员是包含可执行语句的成员。函数成员始终是类型的成员，不能是命名空间的成员。C# 定义了以下函数成员类别：

- 方法
- 属性
- 事件
- 索引器
- 用户定义运算符
- 实例构造函数
- 静态构造函数
- 终结器

除了终结器和静态构造函数（它们不能被显式调用）之外，函数成员中包含的语句通过函数成员调用来执行。编写函数成员调用的实际语法取决于特定的函数成员类别。

函数成员调用的实参列表（§12.6.2）为函数成员的形参提供实际值或变量引用。

泛型方法的调用可能采用类型推断来确定要传递给该方法的类型实参集。此过程在 §12.6.3 中描述。

方法、索引器、运算符和实例构造函数的调用采用重载决策来确定要调用候选函数成员集中的哪一个。此过程在 §12.6.4 中描述。

一旦在绑定时间标识出特定函数成员（可能通过重载决策），调用该函数成员的实际运行时过程在 §12.6.6 中描述。

注意：下表总结了涉及可显式调用的六类函数成员的构造中发生的处理。表中，e、x、y 和 value 表示归类为变量或值的表达式，T 表示归类为类型的表达式，F 是方法的简单名称，P 是属性的简单名称。

| 构造 | 示例 | 描述 |
|---|---|---|
| 方法调用 | F(x, y) | 应用重载决策以选择包含类或结构中的最佳方法 F。使用实参列表 (x, y) 调用该方法。如果该方法不是静态的，则实例表达式为 this。 |
| 方法调用 | T.F(x, y) | 应用重载决策以选择类或结构 T 中的最佳方法 F。如果该方法不是静态的，则发生绑定时间错误。使用实参列表 (x, y) 调用该方法。 |
| 方法调用 | e.F(x, y) | 应用重载决策以选择由 e 的类型给定的类、结构或接口中的最佳方法 F。如果该方法为静态的，则发生绑定时间错误。使用实例表达式 e 和实参列表 (x, y) 调用该方法。 |
| 属性访问 | P | 调用包含类或结构中属性 P 的 get 访问器。如果 P 是只写的，则发生编译时错误。如果 P 不是静态的，则实例表达式为 this。 |
| 属性访问 | P = value | 使用实参列表 (value) 调用包含类或结构中属性 P 的 set 访问器。如果 P 是只读的，则发生编译时错误。如果 P 不是静态的，则实例表达式为 this。 |
| 属性访问 | T.P | 调用类或结构 T 中属性 P 的 get 访问器。如果 P 不是静态的，或者 P 是只写的，则发生编译时错误。 |
| 属性访问 | T.P = value | 使用实参列表 (value) 调用类或结构 T 中属性 P 的 set 访问器。如果 P 不是静态的，或者 P 是只读的，则发生编译时错误。 |
| 属性访问 | e.P | 使用实例表达式 e 调用由 E 的类型给定的类、结构或接口中属性 P 的 get 访问器。如果 P 是静态的，或者 P 是只写的，则发生绑定时间错误。 |
| 属性访问 | e.P = value | 使用实例表达式 e 和实参列表 (value) 调用由 E 的类型给定的类、结构或接口中属性 P 的 set 访问器。如果 P 是静态的，或者 P 是只读的，则发生绑定时间错误。 |
| 事件访问 | E += value | 调用包含类或结构中事件 E 的 add 访问器。如果 E 不是静态的，则实例表达式为 this。 |
| 事件访问 | E -= value | 调用包含类或结构中事件 E 的 remove 访问器。如果 E 不是静态的，则实例表达式为 this。 |
| 事件访问 | T.E += value | 调用类或结构 T 中事件 E 的 add 访问器。如果 E 不是静态的，则发生绑定时间错误。 |




|  |  |  |
|---|---|---|
|  | T.E -= value | 调用类或结构体 T 中事件 E 的移除访问器。如果 E 不是静态的，则发生绑定期错误。 |
|  | e.E += value | 使用实例表达式 e 调用由 E 的类型给定的类、结构体或接口中事件 E 的添加访问器。如果 E 是静态的，则发生绑定期错误。 |
|  | e.E -= value | 使用实例表达式 e 调用由 E 的类型给定的类、结构体或接口中事件 E 的移除访问器。如果 E 是静态的，则发生绑定期错误。 |
| 索引器访问 | e[x, y] | 应用重载决策，以选择由 e 的类型给定的类、结构体或接口中的最佳索引器。使用实例表达式 e 和参数列表 (x, y) 调用该索引器的 get 访问器。如果索引器是只写的，则发生绑定期错误。 |
|  | e[x, y] = value | 应用重载决策，以选择由 e 的类型给定的类、结构体或接口中的最佳索引器。使用实例表达式 e 和参数列表 (x, y, value) 调用该索引器的 set 访问器。如果索引器是只读的，则发生绑定期错误。 |
| 运算符调用 | -x | 应用重载决策，以选择由 x 的类型给定的类或结构体中的最佳一元运算符。使用参数列表 (x) 调用所选运算符。 |
|  | x + y | 应用重载决策，以选择由 x 和 y 的类型给定的类或结构体中的最佳二元运算符。使用参数列表 (x, y) 调用所选运算符。 |
| 实例构造函数调用 | new T(x, y) | 应用重载决策，以选择类或结构体 T 中的最佳实例构造函数。使用参数列表 (x, y) 调用该实例构造函数。 |

*结束注释*

## 12.6.2 参数列表

### 12.6.2.1 概述

每个函数成员和委托调用都包含一个参数列表，它为函数成员的参数提供实际值或变量引用。指定函数成员调用的参数列表的语法取决于函数成员的类别：

- 对于实例构造函数、方法、索引器和委托，参数指定为参数列表，如下所述。对于索引器，当调用 set 访问器时，参数列表还包含指定为赋值运算符右操作数的表达式。*注意：* 这个附加参数不用于重载决策，仅在调用 set 访问器期间使用。*结束注释*
- 对于属性，调用 get 访问器时参数列表为空；调用 set 访问器时，参数列表由指定为赋值运算符右操作数的表达式组成。
- 对于事件，参数列表由指定为 += 或 -= 运算符右操作数的表达式组成。
- 对于用户定义运算符，参数列表由一元运算符的单个操作数或二元运算符的两个操作数组成。

属性（§15.7）和事件（§15.8）的参数始终作为值参数（§15.6.2.2）传递。用户定义运算符（§15.10）的参数始终作为值参数（§15.6.2.2）或输入参数（§9.2.8）传递。索引器（§15.9）的参数始终作为值参数（§15.6.2.2）、输入参数（§9.2.8）或参数数组（§15.6.2.6）传递。这些类别的函数成员不支持输出参数和引用参数。

实例构造函数、方法、索引器或委托调用的参数指定为 argument_list：

```
argument_list
  : argument (',' argument)*
  ;

argument
  : argument_name? argument_value
  ;

argument_name
  : identifier ':'
  ;

argument_value
  : expression
  | 'in' variable_reference
  | 'ref' variable_reference
  | 'out' variable_reference
  ;
```

argument_list 由一个或多个用逗号分隔的参数组成。每个参数由一个可选的 argument_name 后跟一个 argument_value 组成。带有 argument_name 的参数称为命名参数，而不带 argument_name 的参数是位置参数。

argument_value 可以采用以下形式之一：

- 一个表达式，表示该参数作为值参数传递，或者根据 §12.6.4.2 的确定并如 §12.6.2.3 所述，被转换为输入参数后作为输入参数传递。
- 关键字 in 后跟一个 variable_reference（§9.5），表示该参数作为输入参数（§15.6.2.3）传递。变量在作为输入参数传递之前必须明确赋值（§9.4）。
- 关键字 ref 后跟一个 variable_reference（§9.5），表示该参数作为引用参数（§15.6.2.4）传递。变量在作为引用参数传递之前必须明确赋值（§9.4）。
- 关键字 out 后跟一个 variable_reference（§9.5），表示该参数作为输出参数（§15.6.2.5）传递。在将变量作为输出参数传递的函数成员调用之后，该变量被视为已明确赋值（§9.4）。

该形式决定参数的**参数传递模式**：分别为*值、输入、引用或输出*。然而，如上所述，具有值传递模式的参数可能会被转换为具有输入传递模式的参数。

将 volatile 字段（§15.5.4）作为输入参数、输出参数或引用参数传递会导致警告，因为被调用的方法可能不会将该字段视为 volatile。

### 12.6.2.2 对应参数

对于参数列表中的每个参数，被调用的函数成员或委托中都必须有一个对应的参数。

以下使用的参数列表按如下方式确定：

- 对于在类中定义的虚方法和索引器，参数列表从以下位置选取：从接收方的静态类型开始，并搜索其基类时找到的函数成员的第一个声明或重写。
- 对于分部方法，使用定义分部方法声明的参数列表。
- 对于所有其他函数成员和委托，只有一个参数列表，即所使用的那个参数列表。

参数或形参的位置定义为在参数列表或形参列表中位于其前面的参数或形参的数量。

函数成员参数的对应参数按如下方式建立：

- **实例构造函数、方法、索引器和委托的 *参数列表* 中的参数：**
  - 位置参数若在参数列表中的相同位置存在一个参数，则该位置参数对应该参数，除非该参数是参数数组且函数成员以其展开形式调用。
  - 对于以展开形式调用的、具有参数数组的函数成员，位于参数列表中参数数组的位置处或之后的位置参数对应于该参数数组中的一个元素。
  - 命名参数对应于参数列表中具有相同名称的参数。
  - 对于索引器，当调用 set 访问器时，指定为赋值运算符右操作数的表达式对应于 set 访问器声明的隐式 *value* 参数。
- 对于属性，调用 get 访问器时没有参数。调用 set 访问器时，指定为赋值运算符右操作数的表达式对应于 set 访问器声明的隐式 *value* 参数。
- 对于用户定义的一元运算符（包括 *转换*），单个操作数对应于运算符声明的单个参数。
- 对于用户定义的二元运算符，左操作数对应于运算符声明的第一个参数，右操作数对应于第二个参数。
- 当未命名参数位于位置不当的命名参数或对应于参数数组的命名参数之后时，它不对应任何参数。
  *注意：* 这可以防止通过 `M(c: false, false);` 调用 `void M(bool a = true, bool b = true, bool c = true);`。第一个参数被位置不当使用（该参数用于第一个位置，但名为 c 的参数位于第三个位置），因此后续参数应使用命名参数形式。
  *结束注释*



named. 换句话说，非尾随命名参数仅在名称和位置导致找到同一个对应参数时才允许。 end note

## 12.6.2.3 Run-time evaluation of argument lists

在函数成员调用 (§12.6.6) 的运行时处理期间，参数列表的表达式或变量引用按从左到右的顺序进行求值，如下所示：

- 对于值参数，如果参数的传递模式为值
  - 参数表达式被求值并执行到对应参数类型的隐式转换 (§10.2)。所得值成为函数成员调用中值参数的初始值。
  - 否则，参数的传递模式为输入。如果参数是变量引用并且参数类型与参数类型之间存在恒等转换 (§10.2.2)，则所得存储位置成为函数成员调用中参数所表示的存储位置。否则，将创建与对应参数类型相同的类型的存储位置。参数表达式被求值并执行到对应参数类型的隐式转换 (§10.2)。所得值存储在该存储位置中。该存储位置由调用中的输入参数表示。

Example: 给出以下声明和方法调用：

```
static void M1(in int p1) { ... }
int i = 10;
M1(i);    // i is passed as an input argument
M1(i + 5);    // transformed to a temporary input argument
```

在 M1(i) 方法调用中，i 本身作为输入参数传递，因为它被归类为变量并且具有与输入参数相同的类型 int。在 M1(i + 5) 方法调用中，会创建一个未命名的 int 变量，用参数的值进行初始化，然后作为输入参数传递。参见 §12.6.4.2 和 §12.6.4.4。

end example

- 对于输入、输出或引用参数，变量引用被求值并且所得存储位置成为函数成员调用中参数所表示的存储位置。对于输入或引用参数，变量必须在方法调用点被明确赋值。如果作为输出或引用给出的变量引用是 reference_type 的数组元素，则会执行运行时检查以确保数组的元素类型与参数的类型相同。如果此检查失败，则会抛出 System.ArrayTypeMismatchException。

方法、索引器和实例构造函数可以将它们的最后一个参数声明为参数数组 (§15.6.2.6)。此类函数成员根据适用的情况以其正常形式或扩展形式调用 (§12.6.4.2)：

- 当具有参数数组的函数成员以其正常形式调用时，为参数数组提供的参数应为可隐式转换为 (§10.2) 参数数组类型的单个表达式。在这种情况下，参数数组完全像值参数一样起作用。
- 当具有参数数组的函数成员以其扩展形式调用时，调用应为参数数组指定零个或多个位置参数，其中每个参数都是可隐式转换为 (§10.2) 参数数组元素类型的表达式。在这种情况下，调用会创建与参数数量对应的长度的参数数组类型实例，用给定的参数值初始化数组实例的元素，并将新创建的数组实例用作实际参数。

参数列表的表达式始终按文本顺序求值。

Example: 因此，示例

```
class Test
{
    static void F(int x, int y = -1, int z = -2) =>
        Console.WriteLine($"x = {x}, y = {y}, z = {z}");

    static void Main()
    {
        int i = 0;
        F(i++, i++, i++);
        F(z: i++, x: i++);
    }
}
```

产生的输出为

x = 0, y = 1, z = 2
x = 4, y = -1, z = 3

end example

数组协变规则 (§17.6) 允许数组类型 A[] 的值引用数组类型 B[] 的实例，前提是从 B 到 A 存在隐式引用转换。由于这些规则，当 reference_type 的数组元素作为输出或引用参数传递时，需要进行运行时检查以确保数组的实际元素类型与参数的类型相同。

Example: 在以下代码中

```
class Test
{
    static void F(ref object x) {...}

    static void Main()
    {
        object[] a = new object[10];
        object[] b = new string[10];
        F(ref a[0]); // Ok
        F(ref b[1]); // ArrayTypeMismatchException
    }
}
```

第二次调用 F 会导致抛出 System.ArrayTypeMismatchException，因为 b 的实际元素类型是 string 而不是 object。

end example

当具有参数数组的函数成员以扩展形式调用并且至少有一个扩展参数时，调用的处理方式就像在扩展参数周围插入了带数组初始值设定项的数组创建表达式 (§12.8.16.5)。当参数数组没有参数时，会传递一个空数组；传递的引用是分配的新空数组还是现有空数组是未指定的。

Example: 给定声明

```
void F(int x, int y, params object[] args);
```

对该方法扩展形式进行的以下调用

```
F(10, 20, 30, 40);
F(10, 20, 1, "hello", 3.0);
```

完全对应于

```
F(10, 20, new object[] { 30, 40 });
F(10, 20, new object[] { 1, "hello", 3.0 });
```

*end example*

当从具有对应可选参数的函数成员省略参数时，函数成员声明的默认值会被隐式传递。 （这可能涉及如上所述的存储位置的创建。）

*Note:* 因为这些始终是常量，所以它们的求值不会影响剩余参数的求值。 *end note*

## 12.6.3 Type inference

### 12.6.3.1 General

当在不指定类型参数的情况下调用泛型方法时，*type inference* 过程会尝试为调用推断类型参数。类型推断的存在允许使用更方便的语法调用泛型方法，并允许程序员避免指定冗余的类型信息。

*Example:*

```
class Chooser
{
    static Random rand = new Random();

    public static T Choose<T>(T first, T second) =>
        rand.Next(2) == 0 ? first : second;
}

class A
{
    static void M()
    {
        int i = Chooser.Choose(5, 213); // Calls Choose<int>
        string s = Chooser.Choose("apple", "banana"); // Calls Choose<string>
    }
}
```

通过类型推断，类型参数 int 和 string 是从传递给方法的参数中确定的。

*end example*

类型推断是方法调用 (§12.8.9.2) 的绑定时处理的一部分，并在调用的重载解析步骤之前进行。当在方法调用中指定了特定的方法组，并且方法调用中未指定类型参数时，会对方法组中的每个泛型方法应用类型推断。如果类型推断成功，则推断出的类型参数用于确定后续重载解析的参数类型。如果重载解析选择一个泛型方法作为要调用的方法，则推断出的类型参数用作调用的类型参数。如果特定方法的类型推断失败，则该方法不参与重载解析。类型推断本身的失败不会导致绑定时错误。但是，当重载解析随后找不到任何适用方法时，它通常会导致绑定时错误。

如果每个提供的参数不对应于方法中的恰好一个参数 (§12.6.2.2)，或存在没有对应参数的非可选参数，则推断立即失败。否则，假设泛型方法具有以下签名：

T₀ M<X₁...Xₙ>(T₁ p₁ ... Tₙ pₙ)

对于形式为 M(E₁ ... Eₙ) 的方法调用，类型推断的任务是为每个类型参数 X₁...Xₙ 找到唯一的 type arguments S₁...Sₙ，使得调用 M<S₁...Sₙ>(E₁...Eₙ) 变得有效。

类型推断的过程如下所述作为算法。符合规范的编译器可以使用替代方法实现，前提是在所有情况下达到相同的结果。

在推断过程中，每个类型参数 Xᵢ 要么固定为特定类型 Sᵢ，要么未固定并具有关联的边界集合。每个边界都是某种类型 T。最初每个类型变量 Xᵢ 未固定且边界集合为空。

类型推断分阶段进行。每个阶段将尝试基于前一阶段的发现为更多类型变量推断类型参数。第一阶段进行一些边界的初始推断，而第二阶段将类型变量固定为特定类型并推断进一步的边界。第二阶段可能需要重复多次。

> Note: 类型推断也用于其他上下文，包括方法组的转换 (§12.6.3.14) 和查找一组表达式的最佳公共类型 (§12.6.3.15)。 end note

### 12.6.3.2 The first phase

对于每个方法参数 Eᵢ：

- 如果 Eᵢ 是匿名函数，则从 Eᵢ 到 Tᵢ 进行显式参数类型推断 (§12.6.3.8)
- 否则，如果 Eᵢ 具有类型 U 并且 Xᵢ 是值参数 (§15.6.2.2)，则从 U 到 Tᵢ 进行下界推断 (§12.6.3.10)。
- 否则，如果 Eᵢ 具有类型 U 并且 Xᵢ 是引用参数 (§15.6.2.4) 或输出参数 (§15.6.2.5)，则从 U 到 Tᵢ 进行精确推断 (§12.6.3.9)。
- 否则，如果 Eᵢ 具有类型 U 并且 Xᵢ 是输入参数 (§15.6.2.3) 并且 Eᵢ 是输入参数，则从 U 到 Tᵢ 进行精确推断 (§12.6.3.9)。
- 否则，如果 Eᵢ 具有类型 U 并且 Xᵢ 是输入参数 (§15.6.2.3)，则从 U 到 Tᵢ 进行下界推断 (§12.6.3.10)。
- 否则，对此参数不进行推断。

### 12.6.3.3 The second phase

第二阶段按如下方式进行：


- X₁ 具有非空的边界集合
- 如果不存在此类类型变量且仍有未固定的类型变量，则类型推断失败。
- 否则，如果不存在进一步的未固定类型变量，则类型推断成功。
- 否则，对于所有参数类型为 Tᵢ 的参数 Eᵢ，其中输出类型 (§12.6.3.5) 包含未固定的类型变量 Xₖ 但输入类型 (§12.6.3.4) 不包含，则从 Eᵢ 到 Tᵢ 进行输出类型推断 (§12.6.3.7)。然后重复第二阶段。

## 12.6.3.4 输入类型

如果 E 是方法组或隐式类型匿名函数且 T 是委托类型或表达式树类型，则 T 的所有参数类型都是类型为 T 的 E 的输入类型。

## 12.6.3.5 输出类型

如果 E 是方法组或匿名函数且 T 是委托类型或表达式树类型，则 T 的返回类型是类型为 T 的 E 的输出类型。

## 12.6.3.6 依赖

未固定的类型变量 X₁ 直接依赖于未固定的类型变量 Xₐ，如果对于某个类型为 Tᵥ 的参数 Eᵥ，Xₐ 出现在 Eᵥ 的输入类型中且类型为 Tᵥ，并且 X₁ 出现在 Eᵥ 的输出类型中且类型为 Tᵥ。

Xₐ 依赖于 X₁ 如果 Xₐ 直接依赖于 X₁ 或如果 X₁ 直接依赖于 Xᵥ，且 Xᵥ 依赖于 Xₐ。因此“依赖于”是“直接依赖于”的传递但非自反闭包。

## 12.6.3.7 输出类型推断

从表达式 E 到类型 T 的输出类型推断按以下方式进行：

- 如果 E 是具有推断返回类型 U (§12.6.3.13) 的匿名函数且 T 是具有返回类型 Tᵣ 的委托类型或表达式树类型，则从 U 到 Tᵣ 进行下界推断 (§12.6.3.10)。
- 否则，如果 E 是方法组且 T 是具有参数类型 T₁...Tᵥ 和返回类型 Tᵣ 的委托类型或表达式树类型，并且使用类型 T₁...Tᵥ 对 E 进行重载解析得到单个返回类型为 U 的方法，则从 U 到 Tᵣ 进行下界推断。
- 否则，如果 E 是类型为 U 的表达式，则从 U 到 T 进行下界推断。
- 否则，不进行推断。

## 12.6.3.8 显式参数类型推断

从表达式 E 到类型 T 的显式参数类型推断按以下方式进行：

- 如果 E 是具有参数类型 U₁...Uᵥ 的显式类型匿名函数且 T 是具有参数类型 V₁...Vᵥ 的委托类型或表达式树类型，则对每个 Uᵢ 从 Uᵢ 到对应的 Vᵢ 进行精确推断 (§12.6.3.9)。

## 12.6.3.9 精确推断

从类型 U 到类型 V 的精确推断按如下方式进行：

- 如果 V 是未固定的 Xᵢ 之一，则 U 被添加到 Xᵢ 的精确边界集合中。
- 否则，通过检查是否适用以下任一情况来确定集合 V₁...Vₑ 和 U₁...Uₑ：
  - V 是数组类型 V₁[...] 且 U 是相同秩的数组类型 U₁[...]
  - V 是类型 V_i? 且 U 是类型 U_i
  - V 是构造类型 C<V_1...V_e> 且 U 是构造类型 C<U_1...U_e>
如果适用上述任一情况，则对每个 U_i 到对应的 V_i 进行精确推断。
- 否则，不进行推断。

## 12.6.3.10 下界推断

从类型 U 到类型 V 的下界推断按如下方式进行：

- 如果 V 是未固定的 X_i 之一，则 U 被添加到 X_i 的下界集合中。
- 否则，如果 V 是类型 V_i? 且 U 是类型 U_i?，则从 U_i 到 V_i 进行下界推断。
- 否则，通过检查是否适用以下任一情况来确定集合 U_1...U_e 和 V_1...V_e：
  - V 是数组类型 V_1[...] 且 U 是相同秩的数组类型 U_1[...]
  - V 是 IEnumerable<V_i>、ICollection<V_i>、IReadOnlyList<V_i>、IReadOnlyCollection<V_i> 或 IList<V_i> 之一且 U 是单维数组类型 U_1[]
  - V 是构造的类、结构体、接口或委托类型 C<V_1...V_e> 且存在唯一的 C<U_1...U_e> 类型，使得 U（或，如果 U 是类型参数，则其有效基类或其有效接口集合的任何成员）与 C<U_1...U_e> 相同、继承自（直接或间接）或实现（直接或间接）C<U_1...U_e>。
  - {"“唯一性”限制意味着在接口 C<T>{ 类 U : C<X>, C<Y>{} 的情况下，从 U 推断到 C<T> 时不进行推断，因为 U_i 可能是 X 或 Y。"}
如果适用上述任一情况，则按如下方式对每个 U_i 到对应的 V_i 进行推断：
  - 如果 U_i 不已知为引用类型，则进行精确推断
  - 否则，如果 U 是数组类型，则进行下界推断
  - 否则，如果 V 是 C<V_1...V_e>，则推断取决于 C 的第 i 个类型参数：
    - 如果它是协变的，则进行下界推断。
    - 如果它是逆变的，则进行上界推断。
    - 如果它是不可变的，则进行精确推断。
- 否则，不进行推断。

## 12.6.3.11 上界推断

从类型 U 到类型 V 的上界推断按如下方式进行：

- 如果 V 是未固定的 X_i 之一，则 U 被添加到 X_i 的上界集合中。
- 否则，通过检查是否适用以下任一情况来确定集合 V_1...V_e 和 U_1...U_e：
  - U 是数组类型 U_1[...] 且 V 是相同秩的数组类型 V_1[...]
  - U 是 IEnumerable<U_i>、ICollection<U_i>、IReadOnlyList<U_i>、IReadOnlyCollection<U_i> 或 IList<U_i> 之一且 V 是单维数组类型 V_1[]
  - U 是类型 U_i? 且 V 是类型 V_i?
  - U 是构造的类、结构体、接口或委托类型 `C<U1...Ue>` 且 V 是与唯一类型 `C<V1...Ve>` 相同、继承自（直接或间接）或实现（直接或间接）`C<V1...Ve>` 的类、结构体、接口或委托类型
  - ('“唯一性”限制意味着给定接口 C<T>{} 类 V<Z>: C<X<Z>>, C<Y<Z>>{}，则从 C<U1> 推断到 V<Q> 时不进行推断。不会从 U1 推断到 X<Q> 或 Y<Q>。')
如果适用上述任一情况，则按如下方式对每个 U_i 到对应的 V_i 进行推断：
  - 如果 U_i 不已知为引用类型，则进行精确推断
  - 否则，如果 V 是数组类型，则进行上界推断
  - 否则，如果 U 是 C<U1...Ue>，则推断取决于 C 的第 i 个类型参数：
    - 如果它是协变的，则进行上界推断。
    - 如果它是逆变的，则进行下界推断。
    - 如果它是不可变的，则进行精确推断。
- 否则，不进行推断。

## 12.6.3.12 固定

具有边界集合的未固定类型变量 X₁ 按如下方式固定：

- 候选类型集合 Uₑ 最初为 X₁ 的边界集合中的所有类型的集合。
- 依次检查 X₁ 的每个边界：对于 X₁ 的每个精确边界 U，从候选集合中移除所有不与 U 相同的类型 Uₑ。对于 X₁ 的每个下界 U，从候选集合中移除所有不存在从 U 到其隐式转换的类型 Uₑ。对于 X₁ 的每个上界 U，从候选集合中移除所有不存在到 U 的隐式转换的类型 Uₑ。
- 如果在剩余的候选类型 Uₑ 中存在一个唯一的类型 V，使得所有其他候选类型都可以隐式转换为 V，则 X₁ 被固定为 V。
- 否则，类型推断失败。

## 12.6.3.13 推断返回类型

匿名函数 F 的推断返回类型在类型推断和重载解析期间使用。推断返回类型只能针对所有参数类型已知的匿名函数确定，这些参数类型要么是显式给出的，要么是通过匿名函数转换提供的，要么是在封闭的泛型方法调用上的类型推断期间推断出来的。

推断的有效返回类型按如下方式确定：

- 如果 F 的主体是一个具有类型的表达式，则 F 的推断有效返回类型是该表达式的类型。
- 如果 F 的主体是一个块并且块的 return 语句中表达式的集合具有最佳公共类型 T (§12.6.3.15)，则 F 的推断有效返回类型为 T。
- 否则，无法为 F 推断有效返回类型。

推断返回类型按如下方式确定：如果 F 是 async 并且 F 的主体要么是被归类为 nothing (§12.2) 的表达式，要么是没有任何 return 语句带有表达式的块，则推断返回类型为 «TaskType» (§15.15.1)。



- 如果 F 是异步的，并且具有推断出的有效返回类型 T，则推断的返回类型为 «TaskType»<T>（§15.15.1）。
- 如果 F 是非异步的，并且具有推断出的有效返回类型 T，则推断的返回类型为 T。
- 否则，无法为 F 推断返回类型。

*示例：* 作为涉及匿名函数的类型推断示例，请考虑在 System.Linq.Enumerable 类中声明的 Select 扩展方法：

```csharp
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource,TResult>(
            this IEnumerable<TSource> source,
            Func<TSource,TResult> selector)
        {
            foreach (TSource element in source)
            {
                yield return selector(element);
            }
        }
    }
}
```

假设我们通过 using 命名空间指令导入了 System.Linq 命名空间，并且有一个包含 string 类型的 Name 属性的 Customer 类，那么可以使用 Select 方法来选择客户列表中的姓名：

```csharp
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

Select 的扩展方法调用（§12.8.9.3）通过将该调用重写为静态方法调用来处理：

```csharp
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

由于未显式指定类型实参，因此使用类型推断来推断类型实参。首先，将 customers 实参与 source 参数相关联，推断出 TSource 为 Customer。然后，使用上文描述的匿名函数类型推断过程，c 被赋予类型 Customer，并将表达式 c.Name 与 selector 参数的返回类型相关联，推断出 TResult 为 string。因此，该调用等价于 Enumerable.Select<Customer,string>(customers, (Customer c) => c.Name)，其结果类型为 IEnumerable<string>。

下面的示例演示了匿名函数类型推断如何使类型信息在泛型方法调用的实参之间“流动”。给定以下方法和调用：

```csharp
class A
{
    static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2)
    {
        return f2(f1(value));
    }
}

static void M()
{
    double hours = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalHours);
}
```

该调用的类型推断过程如下：首先，将实参 "1:15:30" 与 value 参数相关联，推断出 X 为 string。然后，第一个匿名函数的参数 s 被赋予推断出的类型 string，并将表达式 TimeSpan.Parse(s) 与 f1 的返回类型相关联，推断出 Y 为 System.TimeSpan。最后，第二个匿名函数的参数 t 被赋予推断出的类型 System.TimeSpan，并将表达式 t.TotalHours 与 f2 的返回类型相关联，推断出 Z 为 double。因此，该调用的结果类型为 double。示例结束

### 12.6.3.14 方法组转换的类型推断

与泛型方法的调用类似，当包含泛型方法的方法组 M 被转换为给定的委托类型 D（§10.8）时，也应应用类型推断。给定一个方法 Tₑ M<X₁...Xₙ>(T₁ x₁ ... Tₑ xₑ) 以及被赋值给委托类型 D 的方法组 M，类型推断的任务是找到类型实参 S₁...Sᵥ，使得表达式 M<S₁...Sᵥ> 与 D 兼容（§20.2）。

与泛型方法调用的类型推断算法不同，在这种情况下，只有实参类型，没有实参表达式。特别是，没有匿名函数，因此不需要多阶段推断。

相反，所有 Xᵢ 都被视为未固定，并从 D 的每个实参类型 Uᵢ 到 M 的相应参数类型 Tᵢ 执行下界推断。如果对于任何 Xᵢ 都没有找到界限，则类型推断失败。否则，所有 Xᵢ 都被固定为相应的 Sᵢ，即类型推断的结果。

### 12.6.3.15 查找一组表达式的最佳公共类型

在某些情况下，需要为一组表达式推断一个公共类型。特别是，隐式类型数组的元素类型和带块体的匿名函数的返回类型就是通过这种方式确定的。

对于一组表达式 E₁...Eᵥ，其最佳公共类型按如下方式确定：

- 引入一个新的未固定类型变量 X。
- 对于每个表达式 Eᵢ，从它到 X 执行一次输出类型推断（§12.6.3.7）。
- 如果可能，将 X 固定（§12.6.3.12），所得类型即最佳公共类型。
- 否则推断失败。
- 注意：直观上，此推断等价于调用一个方法 `void M<X>(X x₁ ... X xᵥ)`，将 Eᵢ 作为实参传入并推断 X。注释结束

## 12.6.4 重载决策

### 12.6.4.1 概述

重载决策是一种绑定期机制，用于在给定参数列表和一组候选函数成员的情况下，选择要调用的最佳函数成员。重载决策在 C# 中的以下不同上下文中选择要调用的函数成员：

- 调用 `invocation_expression`（§12.8.9）中命名的方法。
- 调用 `object_creation_expression`（§12.8.16.2）中命名的实例构造函数。
- 通过 `element_access`（§12.8.11）调用索引器访问器。
- 调用表达式中引用的预定义或用户定义运算符（§12.4.4 和 §12.4.5）。

这些上下文各自以独特的方式定义候选函数成员集合和参数列表。例如，方法调用的候选集不包含标记为 override 的方法（§12.5），并且如果派生类中有任何方法适用，则基类中的方法不作为候选（§12.8.9.2）。

一旦确定了候选函数成员和参数列表，最佳函数成员的选择在所有情况下都是相同的：

- 首先，将候选函数成员集合缩减为相对于给定参数列表适用的那些函数成员（§12.6.4.2）。如果缩减后的集合为空，则发生编译时错误。
- 然后，从适用的候选函数成员集合中找出最佳函数成员。如果该集合只包含一个函数成员，则该函数成员就是最佳函数成员。否则，最佳函数成员是相对于给定参数列表优于所有其他函数成员的那个函数成员，前提是每个函数成员都使用 §12.6.4.3 中的规则与其他所有函数成员进行比较。如果不存在恰好一个优于所有其他函数成员的函数成员，则函数成员调用具有歧义，并发生绑定期错误。

以下子条款定义了术语“适用的函数成员”和“更好的函数成员”的确切含义。

### 12.6.4.2 适用的函数成员

当以下所有条件都成立时，称函数成员相对于参数列表 A 是适用的函数成员：

- A 中的每个实参对应于函数成员声明中的一个参数，如 §12.6.2.2 所述，每个参数最多对应一个实参，且没有实参对应的任何参数均为可选参数。
- 对于 A 中的每个实参，该实参的参数传递模式与相应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，存在从实参表达式到相应参数类型的隐式转换（§10.2），或者
  - 对于 ref 或 out 参数，实参表达式（如果有）的类型与相应参数的类型之间存在恒等转换
  - 对于 in 参数，当相应实参具有 in 修饰符时，实参表达式（如果有）的类型与相应参数的类型之间存在恒等转换
  - 对于 in 参数，当相应实参省略 in 修饰符时，存在从实参表达式到相应参数类型的隐式转换（§10.2）。

对于包含参数数组的函数成员，如果该函数成员通过上述规则适用，则称其以其正常形式适用。如果包含参数数组的函数成员在其正常形式下不适用，则该函数成员可能以其展开形式适用：

- 展开形式是通过将函数成员声明中的参数数组替换为该参数数组元素类型的零个或多个值参数来构造的，以使参数列表 A 中的实参数量与参数总数匹配。如果 A 的实参数量少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个实参，以下条件之一成立，则展开形式适用：
  - 实参的参数传递模式与相应参数的参数传递模式相同，并且
    - 对于固定值参数或由展开创建的值参数，存在从实参表达式到相应参数类型的隐式转换（§10.2），或者
    - 对于 in、out 或 ref 参数，实参表达式的类型与相应参数的类型相同。
  - 实参的参数传递模式为 value，相应参数的参数传递模式为 input，并且存在从实参表达式到相应参数类型的隐式转换（§10.2）

当从实参类型到 in 参数类型的隐式转换为动态隐式转换（§10.2.10）时，结果未定义。

示例：给定以下声明和方法调用：

```csharp
public static void M1(int p1) { ... }
public static void M1(in int p1) { ... }
public static void M2(in int p1) { ... }
public static void Test()
{
    int i = 10; uint ui = 34U;

    M1(in i);    // M1(in int) is applicable
    M1(in ui);   // no exact type match, so M1(in int) is not applicable
    M1(i);       // M1(int) and M1(in int) are applicable
    M1(i + 5);   // M1(int) and M1(in int) are applicable
    M1(100u);    // no implicit conversion exists, so M1(int) is not applicable

    M2(in i);    // M2(in int) is applicable
    M2(i);       // M2(in int) is applicable
    M2(i + 5);   // M2(in int) is applicable
}
```


*示例结束*

- 静态方法仅在方法组由通过类型的*简单名称*或*成员访问*产生时适用。
- 实例方法仅在方法组由*简单名称*、通过变量或值的*成员访问*或*基访问*产生时适用。
  - 如果方法组由*简单名称*产生，则仅当允许 `this` 访问（§12.8.13）时，实例方法才适用。
- 当方法组由*成员访问*产生，且如 §12.8.7.2 所述，该访问既可能通过*实例*也可能通过*类型*时，实例方法和静态方法均适用。
- 泛型方法的类型实参（显式指定或推断）若不能全部满足其约束，则该方法不适用。
- 在方法组转换的上下文中，从方法返回类型到委托的返回类型必须存在标识转换（§10.2.2）或隐式引用转换（§10.2.8）。否则，候选方法不适用。

## 12.6.4.3 更好的函数成员

为了确定更好的函数成员，会构造一个精简参数列表 Ā，其中仅包含实参表达式本身，且顺序与它们在原始参数列表中的出现顺序一致，并省略所有 `out` 或 `ref` 参数。

按下述方式为每个候选函数成员构造参数列表：

- 如果函数成员仅以展开形式适用，则使用展开形式。
- 没有对应实参的可选参数将从参数列表中移除。
- `ref` 和 `out` 参数将从参数列表中移除。
- 参数将被重新排序，使其与实参列表中对应实参的位置相同。

给定一个实参列表 A，其中包含一组实参表达式 {E₁, E₂, …, Eᵥ}，以及两个适用的函数成员 M₁ 和 M₂，其参数类型分别为 {P₁, P₂, …, Pᵥ} 和 {Q₁, Q₂, …, Qᵥ}，如果满足以下条件，则 M₁ 被定义为比 M₂ *更好的函数成员*：

- 对于每个实参，从 Eᵥ 到 Qᵥ 的隐式转换不优于从 Eᵥ 到 Pᵥ 的隐式转换，并且
- 至少有一个实参，从 Eᵥ 到 Pᵥ 的转换优于从 Eᵥ 到 Qᵥ 的转换。

如果参数类型序列 {P₁, P₂, …, Pᵥ} 和 {Q₁, Q₂, …, Qᵥ} 等价（即每个 Pᵢ 都能标识转换为对应的 Qᵢ），则按顺序应用以下平局决胜规则来确定更好的函数成员。

- 如果 M₁ 是非泛型方法而 M₂ 是泛型方法，则 M₁ 优于 M₂。
- 否则，如果 M₁ 以正常形式适用，而 M₂ 具有 params 数组且仅以其展开形式适用，则 M₁ 优于 M₂。
- 否则，如果两个方法都有 params 数组且仅能以展开形式适用，并且 M₁ 的 params 数组元素少于 M₂ 的 params 数组元素，则 M₁ 优于 M₂。
- 否则，如果 M_v 的参数类型比 M_w 的参数类型更具体，则 M_v 优于 M_w。令 {R1, R2, ..., Rn} 和 {S1, S2, ..., Sn} 分别表示 M_v 和 M_w 的未实例化且未展开的参数类型。如果对于每个参数，R_x 不比 S_x 更不具体，并且至少有一个参数 R_x 比 S_x 更具体，则 M_v 的参数类型比 M_w 的参数类型更具体：
  - 类型参数不如非类型参数具体。
  - 递归地，如果一个构造类型至少有一个类型实参比另一个构造类型（具有相同数量的类型实参）的对应类型实参更具体，且没有类型实参比对应的类型实参更不具体，则该构造类型比另一个构造类型更具体。
  - 如果一个数组类型的元素类型比另一个数组类型（具有相同维数）的元素类型更具体，则该数组类型比另一个数组类型更具体。
- 否则，如果一个成员是未提升的运算符，而另一个是提升的运算符，则未提升的运算符更好。
- 如果两个函数成员都未被判定为更好，并且 M_v 的所有参数都有对应的实参，而 M_w 中至少有一个可选参数需要替换为默认实参，则 M_v 优于 M_w。
- 如果对于至少一个参数，M_v 使用了比 M_w 中对应参数更好的参数传递方式选择（§12.6.4.4），且 M_w 中没有参数使用比 M_v 更好的参数传递方式选择，则 M_v 优于 M_w。
- 否则，没有更好的函数成员。

## 12.6.4.4 更好的参数传递模式

允许两个重载方法中的对应参数仅因参数传递模式不同而不同，前提是两个参数之一具有值传递模式，如下所示：

```
public static void M1(int p1) { ... }
public static void M1(in int p1) { ... }
```

给定 int i = 10;，根据 §12.6.4.2，调用 M1(i) 和 M1(i + 5) 会导致两个重载都适用。在这种情况下，具有值传递模式的方法就是更好的参数传递模式选择。

> 备注：对于输入、输出或引用传递模式的实参，无需存在此类选择，因为这些实参仅匹配完全相同的参数传递模式。结束备注

## 12.6.4.5 表达式的更好转换

给定一个将表达式 E 转换为类型 T1 的隐式转换 C1，以及一个将表达式 E 转换为类型 T2 的隐式转换 C2，如果满足以下任一条件，则 C1 是比 C2 更好的转换：

- E 完全匹配 T1 且 E 不完全匹配 T2（§12.6.4.6）
- E 完全匹配 T1 和 T2 两者，或都不匹配，且 T1 是比 T2 更好的转换目标（§12.6.4.7）
- E 是方法组（§12.2），对于转换 C1，T1 与方法组中的唯一最佳方法兼容（§20.4），而 T2 对于转换 C2 与方法组中的唯一最佳方法不兼容

## 12.6.4.6 完全匹配的表达式

给定表达式 E 和类型 T，如果满足以下任一条件，则 E 完全匹配 T：

- E 具有类型 S，并且存在从 S 到 T 的标识转换
- E 是匿名函数，T 是委托类型 D 或表达式树类型 `Expression<D>`，并且满足以下条件之一：
  - 在 D 的参数列表上下文中，存在为 E 推断的返回类型 X（§12.6.3.12），并且存在从 X 到 D 的返回类型的标识转换
  - E 是无返回值的异步 lambda，并且 S 是非泛型 «TaskType»
  - 要么 E 是非异步的且 D 具有返回类型 V，要么 E 是异步的且 D 具有返回类型 «TaskType<V>»（§15.15.1），并且满足以下条件之一：
    - E 的主体是精确匹配 Y 的表达式
    - E 的主体是一个块，其中每个 return 语句都返回精确匹配 Y 的表达式

## 12.6.4.7 更好的转换目标

给定两个类型 T₁ 和 T₂，如果满足以下任一条件，则 T₁ 是比 T₂ 更好的转换目标：

- 存在从 T₁ 到 T₂ 的隐式转换，且不存在从 T₂ 到 T₁ 的隐式转换
- T₁ 是 «TaskType<S₁>»（§15.15.1），T₂ 是 «TaskType<S₂>»，且 S₁ 是比 S₂ 更好的转换目标
- T₁ 是 «TaskType<S₁>»（§15.15.1），T₂ 是 «TaskType»，且 T₁ 比 T₂ 更专门化
- T₁ 是 S₁?，其中 S₁ 是有符号整型，T₂ 是 S₂?，其中 S₂ 是无符号整型。具体来说：
  - S₁ 是 sbyte，S₂ 是 byte、ushort、uint 或 ulong
  - S₁ 是 short，S₂ 是 ushort、uint 或 ulong
  - S₁ 是 int，S₂ 是 uint 或 ulong
  - S₁ 是 long，S₂ 是 ulong

## 12.6.4.8 泛型类中的重载

备注：虽然声明时的签名应是唯一的（§8.6），但类型实参的替换可能会导致签名相同。在这种情况下，重载决策将选择原始签名（在替换类型实参之前）中最具体的签名（§12.6.4.3）（如果存在），否则报告错误。结束备注

示例：以下示例展示了根据此规则有效和无效的重载：

```
public interface I1<T> { ... }
public interface I2<T> { ... }

public abstract class G1<U>
{
    public abstract int F1(U u);        // Overload resolution for G<int>.F1
    public abstract int F1(int i);      // will pick non-generic

    public abstract void F2(I1<U> a);   // Valid overload
    public abstract void F2(I2<U> a);
}

abstract class G2<U,V>
```




```
{
    public abstract void F3(U u, V v);    // Valid, but overload resolution for
    public abstract void F3(V v, U u);    // G2<int,int>.F3 will fail

    public abstract void F4(U u, I1<V> v); // Valid, but overload resolution for
    public abstract void F4(I1<V> v, U u); // G2<I1<int>,int>.F4 will fail

    public abstract void F5(U u1, I1<V> v2);  // Valid overload
    public abstract void F5(V v1, U u2);

    public abstract void F6(ref U u);    // Valid overload
    public abstract void F6(out V v);
}
```

*示例结束*

## 12.6.5 动态成员调用的编译时检查

即使动态绑定操作的重载决策在运行时进行，有时也可以在编译时知道将从哪些函数成员列表中选择重载：

- 对于委托调用（§12.8.9.4），该列表是单个函数成员，其参数列表与调用的 delegate_type 相同
- 对于对类型或静态类型不是 dynamic 的值进行的方法调用（§12.8.9.2），方法组中可访问的方法集在编译时已知。
- 对于对象创建表达式（§12.8.16.2），类型中可访问的构造函数集在编译时已知。
- 对于索引器访问（§12.8.11.3），接收方中可访问的索引器集在编译时已知。

在这些情况下，会对已知函数成员集合中的每个成员执行有限的编译时检查，以确定是否可以确定它在运行时绝不会被调用。对于每个函数成员 F，会构造修改后的参数列表和实参列表：

- 首先，如果 F 是泛型方法且提供了类型实参，则将这些类型实参替换参数列表中的类型形参。但是，如果未提供类型实参，则不进行此类替换。
- 然后，任何类型为开放类型（即包含类型形参；参见 §8.4.3）的参数都会被省略，其对应的参数也会一并省略。

为使 F 通过检查，必须满足以下所有条件：

- 根据 §12.6.4.2，F 的修改后参数列表适用于修改后的实参列表。
- 修改后参数列表中的所有构造类型都满足其约束（§8.4.5）。
- 如果在上一步中替换了 F 的类型形参，则满足其约束。
- 如果 F 是静态方法，则该方法组不得来自这样的 member_access：其接收方在编译时已知为变量或值。
- 如果 F 是实例方法，则该方法组不得来自这样的 member_access：其接收方在编译时已知为类型。

如果没有候选者通过此测试，则发生编译时错误。

## 12.6.6 函数成员调用

### 12.6.6.1 概述

本子条款描述在运行时调用特定函数成员所发生的过程。

假定绑定期过程已确定要调用的特定成员，可能是通过对一组候选函数成员应用重载决策来确定的。

为了描述调用过程，函数成员分为两类：

- 静态函数成员。这些是静态方法、静态属性访问器和用户定义运算符。静态函数成员始终是非虚的。
- 实例函数成员。这些是实例方法、实例构造函数、实例属性访问器和索引器访问器。实例函数成员要么是非虚的，要么是虚的，并且始终在特定实例上调用。该实例由实例表达式计算，并在函数成员内以 this 的形式可访问（§12.8.13）。对于实例构造函数，实例表达式被视为新分配的对象。

函数成员调用的运行时处理包括以下步骤，其中 M 是函数成员，并且如果 M 是实例成员，则 E 是实例表达式：

- 如果 M 是静态函数成员：
  - 实参列表按 §12.6.2 中所述进行计算。
  - 调用 M。
- 否则，如果 E 的类型是值类型 V，并且 M 在 V 中声明或重写：
  - 计算 E。如果此计算导致异常，则不执行后续步骤。对于实例构造函数，此计算包括为新对象分配存储（通常来自执行堆栈）。在这种情况下，E 被归类为变量。
  - 如果 E 未被归类为变量，或者 V 不是只读结构类型（§16.2.2），并且 E 是以下之一：
    - 输入参数（§15.6.2.3），或
    - 只读字段（§15.5.3），或
    - 只读引用变量或返回（§9.7），
    则创建 E 的类型的临时局部变量，并将 E 的值赋给该变量。E 随后被重新归类为对该临时局部变量的引用。该临时变量在 M 内以 this 的形式可访问，但不能以任何其他方式访问。因此，仅当 E 可写时，调用方才可能观察到 M 对 this 所做的更改。
  - 实参列表按 §12.6.2 中所述进行计算。
  - 调用 M。E 引用的变量成为 this 引用的变量。
- 否则：
  - 计算 E。如果此计算导致异常，则不执行后续步骤。
  - 实参列表按 §12.6.2 中所述进行计算。
  - 如果 E 的类型是值类型，则执行装箱转换（§10.2.9）以将 E 转换为类类型，并且在后续步骤中 E 被视为该类型。如果该值类型是枚举类型，则类类型为 System.Enum；否则为 System.ValueType。
  - 检查 E 的值是否有效。如果 E 的值为 null，则抛出 System.NullReferenceException，并且不执行后续步骤。
  - 确定要调用的函数成员实现：
    - 如果 E 的绑定期类型是接口，则要调用的函数成员是由 E 引用的实例的运行时类型提供的 M 的实现。通过应用接口映射规则（§18.6.5）来确定由 E 引用的实例的运行时类型提供的 M 的实现，从而确定该函数成员。
    - 否则，如果 M 是虚函数成员，则要调用的函数成员是由 E 引用的实例的运行时类型提供的 M 的实现。通过应用确定 M 相对于 E 引用的实例的运行时类型的最派生实现的规则（§15.6.4），从而确定该函数成员。
    - 否则，M 是非虚函数成员，要调用的函数成员就是 M 本身。
  - 调用在上一步中确定的函数成员实现。E 引用的对象成为 this 引用的对象。

实例构造函数（§12.8.16.2）调用的结果是所创建的值。任何其他函数成员调用的结果是从其主体返回的值（如果有）（§13.10.5）。

### 12.6.6.2 对装箱实例的调用

在以下情况下，可以通过该值类型的装箱实例调用在该值类型中实现的函数成员：

- 当该函数成员是对从类类型继承的方法的重写，并通过该类类型的实例表达式调用时。注意：该类类型将始终是 System.Object、System.ValueType 或 System.Enum 之一。结束注意
- 当该函数成员是接口函数成员的实现，并通过接口类型的实例表达式调用时。
- 当该函数成员通过委托调用时。

在这些情况下，装箱实例被视为包含该值类型的变量，并且该变量成为函数成员调用内由 this 引用的变量。

注意：特别是，这意味着当在装箱实例上调用函数成员时，该函数成员可以修改装箱实例中包含的值。结束注意

## 12.7 解构

解构是将表达式转换为由各个表达式组成的元组的过程。当简单赋值的目标是元组表达式时，使用解构来获取要赋给该元组每个元素的值。

表达式 E 按以下方式解构为具有 n 个元素的元组表达式：


- 如果 E 是一个包含 n 个元素的元组表达式，则解构的结果是表达式 E 本身。
- 否则，如果 E 具有包含 n 个元素的元组类型 (T1, ..., Tn)，则将 E 求值到临时变量 __v，解构的结果是表达式 (__v.Item1, ..., __v.Itemn)。
- 否则，如果表达式 E.Deconstruct(out var __v1, ..., out var __vn) 在编译时解析为唯一的实例方法或扩展方法，则对该表达式求值，解构的结果是表达式 (__v1, ..., __vn)。这样的方法称为解构器。
- 否则，E 不能被解构。

这里，__v 和 __v1, ..., __vn 指的是在其他情况下不可见且不可访问的临时变量。

注意：类型为 dynamic 的表达式不能被解构。注意结束。

## 12.8 基本表达式

### 12.8.1 概述

基本表达式包括最简单的表达式形式。

```
primary_expression
: primary_no_array_creation_expression
| array_creation_expression
;

primary_no_array_creation_expression
: literal
| interpolated_string_expression
| simple_name
| parenthesized_expression
| tuple_expression
| member_access
| null_conditional_member_access
| invocation_expression
| element_access
| null_conditional_element_access
| this_access
| base_access
| post_increment_expression
| post_decrement_expression
| object_creation_expression
| delegate_creation_expression
| anonymous_object_creation_expression
| typeof_expression
| sizeof_expression
| checked_expression
| unchecked_expression
| default_value_expression
| nameof_expression
| anonymous_method_expression
| pointer_member_access    // unsafe code support
| pointer_element_access  // unsafe code support
| stackalloc_expression
;
```

*注意：* 这些语法规则并非 ANTLR 就绪，因为它们是一组相互左递归规则（`primary_expression`、`primary_no_array_creation_expression`、`member_access`、`invocation_expression`、`element_access`、`post_increment_expression`、`post_decrement_expression`、`pointer_member_access` 和 `pointer_element_access`）的一部分，ANTLR 无法处理这些规则。可以使用标准技术来转换文法以消除相互左递归。这里没有这样做，因为并非所有解析策略都需要它（例如 LALR 解析器就不需要），而且这样做会模糊结构和描述。*注意结束*

*pointer_member_access*（§23.6.3）和 *pointer_element_access*（§23.6.4）仅在非安全代码（§23）中可用。

基本表达式分为 *array_creation_expressions* 和 *primary_no_array_creation_expressions*。以这种方式处理 *array_creation_expression*，而不是将它与其他简单表达式形式一起列出，使文法能够禁止可能引起混淆的代码，例如

```
object o = new int[3][1];
```

否则会被解释为

```
object o = (new int[3])[1];
```

### 12.8.2 字面量

由 *literal*（§6.4.5）组成的 *primary_expression* 归类为 *value*。

### 12.8.3 内插字符串表达式

一个 *interpolated_string_expression* 由 $ 或 $@ 后紧跟双引号（"）字符内的文本组成。在引号文本内，有零个或多个由 { 和 } 字符分隔的 *interpolations*，每个内插包含一个 *expression* 和可选的格式说明。

内插字符串表达式有两种形式：常规（*interpolated_regular_string_expression*）和逐字（*interpolated_verbatim_string_expression*）；它们在词法上类似于字符串字面量（§6.4.5.6）的两种形式，但在语义上不同。

```
interpolated_string_expression
    : interpolated_regular_string_expression
    | interpolated_verbatim_string_expression
    ;

// interpolated regular string expressions

interpolated_regular_string_expression
    : Interpolated_Regular_String_Start Interpolated_Regular_String_Mid?
    ('{' regular_interpolation '}' Interpolated_Regular_String_Mid?)*
    Interpolated_Regular_String_End
    ;

regular_interpolation
    : expression (',' interpolation_minimum_width)?
    Regular_Interpolation_Format?
    ;

interpolation_minimum_width
    : constant_expression
    ;
```

```
Interpolated_Regular_String_Start
    : '$"'
    ;

// the following three lexical rules are context sensitive, see details below

Interpolated_Regular_String_Mid
    : Interpolated_Regular_String_Element+
    ;

Regular_Interpolation_Format
    : ':' Interpolated_Regular_String_Element+
    ;

Interpolated_Regular_String_End
    : '""'
    ;

fragment Interpolated_Regular_String_Element
    : Interpolated_Regular_String_Character
    | Simple_Escape_Sequence
    | Hexadecimal_Escape_Sequence
    | Unicode_Escape_Sequence
    | Open_Brace_Escape_Sequence
    | Close_Brace_Escape_Sequence
    ;

fragment Interpolated_Regular_String_Character
    // Any character except " (U+0022), \\ (U+005C),
    // { (U+007B), } (U+007D), and New_Line_Character.
    : ~["\{\}\u000D\u000A\u005C\u2028\u2029]
    ;

// interpolated verbatim string expressions

interpolated_verbatim_string_expression
    : Interpolated_Verbatim_String_Start Interpolated_Verbatim_String_Mid?
    ('{' verbatim_interpolation '}' Interpolated_Verbatim_String_Mid?)*
    Interpolated_Verbatim_String_End
    ;

verbatim_interpolation
    : expression (',' interpolation_minimum_width)?
    Verbatim_Interpolation_Format?
    ;

Interpolated_Verbatim_String_Start
    : '$@"'
    ;

// the following three lexical rules are context sensitive, see details below

Interpolated_Verbatim_String_Mid
    : Interpolated_Verbatim_String_Element+
    ;
```

```
Verbatim_Interpolation_Format
    : ':' Interpolated_Verbatim_String_Element+
    ;
Interpolated_Verbatim_String_End
    : '""'
    ;
fragment Interpolated_Verbatim_String_Element
    : Interpolated_Verbatim_String_Character
    | Quote_Escape_Sequence
    | Open_Brace_Escape_Sequence
    | Close_Brace_Escape_Sequence
    ;
fragment Interpolated_Verbatim_String_Character
    : ~["{}"]    // Any character except " (U+0022), { (U+007B) and } (U+007D)
    ;
// lexical fragments used by both regular and verbatim interpolated strings
fragment Open_Brace_Escape_Sequence
    : '{ {'
    ;
fragment Close_Brace_Escape_Sequence
    : '}}'
    ;
```

上面定义的六条词法规则是上下文相关的，如下所示：

| 规则 | 上下文要求 |
|---|---|
| *Interpolated_Regular_String_Mid* | 仅在 *Interpolated_Regular_String_Start* 之后、任何后续内插之间以及相应的 *Interpolated_Regular_String_End* 之前被识别。 |
| *Regular_Interpolation_Format* | 仅在 *regular_interpolation* 内，并且当起始冒号 (:) 未嵌套在任何类型的括号（圆括号/大括号/方括号）内时被识别。 |
| *Interpolated_Regular_String_End* | 仅在 *Interpolated_Regular_String_Start* 之后被识别，并且仅当任何介入标记要么是 *Interpolated_Regular_String_Mids*，要么是可以作为 *regular_interpolations* 一部分的标记，包括包含在此类内插中的任何 *interpolated regular_string_expressions* 的标记。 |
| *Interpolated_Verbatim_String_Mid*<br>*Verbatim_Interpolation_Format*<br>*Interpolated_Verbatim_String_End* | 这三条规则的识别遵循上述对应规则的识别方式，只是将每个提到的 *regular* 文法规则替换为相应的 *verbatim* 规则。 |

注意：上述规则是上下文相关的，因为它们的定义与语言中其他标记的定义重叠。注意结束。

注意：由于上下文相关的词法规则，上述文法并非 ANTLR 就绪。与其他词法分析器生成器一样，ANTLR 支持上下文相关的词法规则，例如使用其词法模式，但这是一个实现细节，因此不属于本标准的一部分。注意结束。

一个 interpolated_string_expression 归类为值。如果它通过隐式内插字符串转换（§10.2.5）立即转换为 System.IFormattable 或 System.FormattableString，则该内插字符串表达式具有该类型。否则，它具有类型 string。

注意：interpolated_string_expression 可能具有的类型之间的差异可以从 System.String（§C.2）和 System.FormattableString（§C.3）的文档中确定。注意结束。

内插（包括 regular_interpolation 和 verbatim_interpolation）的含义是将表达式的值格式化为字符串，可以按照 Regular_Interpolation_Format 或 Verbatim_Interpolation_Format 指定的格式，或者按照表达式类型的默认格式。然后，格式化后的字符串由 interpolation_minimum_width（如果有）修改，以生成最终要内插到 interpolated_string_expression 中的字符串。

注意：类型的默认格式如何确定，在 System.String（§C.2）和 System.FormattableString（§C.3）的文档中有详细说明。标准格式的描述（对于 Regular_Interpolation_Format 和 Verbatim_Interpolation_Format 是相同的）可以在 System.IFormattable（§C.4）的文档以及标准库（§C）中的其他类型中找到。注意结束。

在 interpolation_minimum_width 中，constant_expression 应具有到 int 的隐式转换。设字段宽度为该 constant_expression 的绝对值，对齐方式为该 constant_expression 值的符号（正或负）：

- 如果字段宽度值小于或等于格式化字符串的长度，则不修改格式化字符串。
- 否则，用空白字符填充格式化字符串，使其长度等于字段宽度：
  - 如果对齐方式为正，则通过在开头添加填充来右对齐格式化字符串，
  - 否则，通过在末尾添加填充来左对齐。

interpolated_string_expression 的整体含义（包括上述内插的格式化和填充）通过将该表达式转换为方法调用来定义：如果表达式的类型是 System.IFormattable 或 System.FormattableString，则该方法为 System.Runtime.CompilerServices.FormattableStringFactory.Create（§C.3），它返回类型为 System.FormattableString 的值；否则，类型必须是 string，方法为 string.Format（§C.2），它返回类型为 string 的值。

在这两种情况下，调用的参数列表由一个格式字符串字面量（包含每个内插的格式说明）和与格式说明对应的每个表达式的一个参数组成。

格式字符串字面量的构造如下，其中 N 是 interpolated_string_expression 中内插的数量。格式字符串字面量按顺序包含：

- Interpolated_Regular_String_Start 或 Interpolated_Verbatim_String_Start 的字符
- Interpolated_Regular_String_Mid 或 Interpolated_Verbatim_String_Mid 的字符（如果有）





- 然后，如果 N ≥ 1，则对于从 0 到 N-1 的每个数字 I：
  - 占位符规范：
    - 一个左大括号（{）字符
    - I 的十进制表示
    - 然后，如果对应的 regular_interpolation 或 verbatim_interpolation 具有 interpolation_minimum_width，则一个逗号（,）后跟 constant_expression 的值的十进制表示
    - 对应的 regular_interpolation 或 verbatim_interpolation 的 Regular_Interpolation_Format 或 Verbatim_Interpolation_Format 字符（如果有）
    - 一个右大括号（}）字符
  - 紧随对应内插之后的 Interpolated_Regular_String_Mid 或 Interpolated_Verbatim_String_Mid 的字符（如果有）
- 最后是 Interpolated_Regular_String_End 或 Interpolated_Verbatim_String_End 的字符。

后续参数是按顺序来自内插的表达式（如果有）。

当 interpolated_string_expression 包含多个内插时，这些内插中的表达式按从左到右的文本顺序求值。

示例：

此示例使用以下格式规范特性：

- X 格式规范，它将整数格式化为大写十六进制，
- 字符串值的默认格式是该值本身，
- 正对齐值，在指定的最小字段宽度内右对齐，
- 负对齐值，在指定的最小字段宽度内左对齐，
- 为 interpolation_minimum_width 定义的常量，以及
- {{ 和 }} 分别格式化为 { 和 }。

给定：

```
string text = "red";
int number = 14;
const int width = -4;
```

然后：

| 内插字符串表达式 | 作为 string 的等价含义 | 值 |
|---|---|---|
| ${text} | string.Format("{0}", text) | "red" |
| ${{text}} | string.Format("{{text}}") | "{text}" |
| ${ text , 4 } | string.Format("{0,4}", text) | "  red" |
| ${ text , width } | string.Format("{0,-4}", text) | "red  " |
| ${number:X} | string.Format("{0:X}", number) | "E" |
| ${text + '?'} {number % 3} | string.Format("{0} {1}", text + '?', number % 3) | "red? 2" |
| ${text + $"[{number}]"} | string.Format("{0}", text + string.Format("[{0}]", number)) | "red[14]" |
| ${ (number==0?"Zero":"Non-zero") } | string.Format("{0}", (number==0?"Zero":"Non-zero")) | "Non-zero" |

*示例结束*

## 12.8.4 简单名称

simple_name 由一个标识符组成，后面可选跟一个类型参数列表：

```
simple_name
  : identifier type_argument_list?
  ;
```

simple_name 要么是 I 形式，要么是 I<A1, ..., An> 形式，其中 I 是单个标识符，而 <A1, ..., An> 是可选 type_argument_list。当未指定 type_argument_list 时，认为 K 为零。simple_name 按如下方式求值并分类：

- 如果 K 为零，并且 simple_name 出现在直接包含名为 I 的局部变量、参数或常量的局部变量声明空间（§7.3）中，则 simple_name 引用该局部变量、参数或常量，并分类为变量或值。
- 如果 K 为零，并且 simple_name 出现在泛型方法声明中但位于其 method_declaration 的特性之外，而且该声明包含名为 I 的类型参数，则 simple_name 引用该类型参数。
- 否则，对于每个实例类型 T（§15.3.2），从直接封闭类型声明的实例类型开始，并继续处理每个封闭类或结构声明的实例类型（如果有）：
  - 如果 K 为零，并且 T 的声明包含名为 I 的类型参数，则 simple_name 引用该类型参数。
  - 否则，如果对 T 中 I 进行具有 K 个类型参数的成员查找（§12.5）产生匹配：
    - 如果 T 是直接封闭类或结构类型的实例类型，并且该查找标识一个或多个方法，则结果是一个方法组，其关联的实例表达式为 this。如果指定了类型参数列表，则它用于调用泛型方法（§12.8.9.2）。
    - 否则，如果 T 是直接封闭类或结构类型的实例类型，如果该查找标识实例成员，并且如果该引用出现在实例构造函数、实例方法或实例访问器（§12.2.1）的块中，则结果与形式为 this.I 的成员访问（§12.8.7）相同。这只能在 K 为零时发生。
    - 否则，结果与形式为 T.I 或 T.I<A1, ..., An> 的成员访问（§12.8.7）相同。
- 否则，对于每个命名空间 N，从 simple_name 所在的命名空间开始，继续处理每个封闭命名空间（如果有），并以全局命名空间结束，按以下步骤求值，直到定位到某个实体：
  - 如果 K 为零，并且 I 是 N 中某个命名空间的名称，则：
    - 如果 simple_name 出现的位置被 N 的命名空间声明所包围，并且该命名空间声明包含将名称 I 与某个命名空间或类型关联的 extern_alias_directive 或 using_alias_directive，则 simple_name 有歧义，并发生编译时错误。
    - 否则，simple_name 引用 N 中名为 I 的命名空间。
  - 否则，如果 N 包含具有名称 I 和 K 个类型参数的可访问类型，则：
    - 如果 K 为零，并且 simple_name 出现的位置被 N 的命名空间声明所包围，并且该命名空间声明包含将名称 I 与某个命名空间或类型关联的 extern_alias_directive 或 using_alias_directive，则 simple_name 有歧义，并发生编译时错误。
    - 否则，simple_name 引用用给定类型参数构造的类型。
  - 否则，如果 simple_name 出现的位置被 N 的命名空间声明所包围：
    - 如果 K 为零，并且该命名空间声明包含将名称 I 与导入的命名空间或类型关联的 extern_alias_directive 或 using_alias_directive，则 simple_name 引用该命名空间或类型。
    - 否则，如果该命名空间声明的 using_namespace_directives 所导入的命名空间恰好包含一个具有名称 I 和 K 个类型参数的类型，则 simple_name 引用用给定类型参数构造的该类型。
    - 否则，如果该命名空间声明的 using_namespace_directives 所导入的命名空间包含多于一个具有名称 I 和 K 个类型参数的类型，则 simple_name 有歧义，并发生编译时错误。注意：整个步骤与处理 namespace_or_type_name（§7.8）时的对应步骤完全平行。注意结束
- 否则，如果 K 为零，并且 I 是标识符 _，则 simple_name 是简单弃元，它是声明表达式（§12.17）的一种形式。
- 否则，simple_name 未定义，并发生编译时错误。

## 12.8.5 括号表达式

parenthesized_expression 由括在括号中的一个表达式组成。

```
parenthesized_expression
  : '(' expression ')'
  ;
```

parenthesized_expression 通过求值括号内的表达式来求值。如果括号内的表达式表示命名空间或类型，则发生编译时错误。否则，parenthesized_expression 的结果就是所包含表达式的求值结果。

## 12.8.6 元组表达式

tuple_expression 表示一个元组，由两个或多个以逗号分隔且可选命名的表达式括在括号中组成。deconstruction_expression 是包含隐式类型声明表达式的元组的简写语法。

```
tuple_expression
  : '(' tuple_element (',' tuple_element)+ ')'
  | deconstruction_expression
  ;

tuple_element
  : (identifier ':')? expression
  ;

deconstruction_expression
  : 'var' deconstruction_tuple
  ;

deconstruction_tuple
  : '(' deconstruction_element (',' deconstruction_element)+ ')'
  ;

deconstruction_element
  : deconstruction_tuple
  | identifier
  ;
```

tuple_expression 分类为元组。

deconstruction_expression var (e1, ..., en) 是 tuple_expression (var e1, ..., var en) 的简写，并遵循相同的行为。这递归适用于 deconstruction_expression 中的任何嵌套 deconstruction_tuples。因此，嵌套在 deconstruction_expression 中的每个标识符都会引入一个声明表达式（§12.17）。因此，deconstruction_expression 只能出现在简单赋值的左侧。

元组表达式具有类型，当且仅当其每个元素表达式 Ei 都具有类型 Ti。该类型应为与元组表达式具有相同元数的元组类型，其中每个元素由以下方式给出：

- 如果对应位置的元组元素具有名称 Ni，则该元组类型元素应为 Ti Ni。
- 否则，如果 Ei 的形式为 Ni 或 E.Ni 或 E?.Ni，则该元组类型元素应为 Ti Ni，除非以下任一情况成立：
  - 元组表达式的另一个元素具有名称 Ni，或
  - 另一个没有名称的元组元素具有形式为 Ni 或 E.Ni 或 E?.Ni 的元组元素表达式，或
  - Ni 的形式为 ItemX，其中 X 是一个不以 0 开头的十进制数字序列，可能表示元组元素的位置，并且 X 不表示该元素的位置。
- 否则，该元组类型元素应为 Ti。

元组表达式通过从左到右按顺序求值其每个元素表达式来求值。

可以通过将元组表达式转换为元组类型（§10.2.13）、将其重新分类为值（§12.2.2），或使其成为解构赋值（§12.21.2）的目标，来从元组表达式获取元组值。

示例：

```
(int i, string) t1 = (i: 1, "One");
(long i, string) t2 = (i: 2, null);
var t3 = (i: 3, "Three");      // (int i, string)
var t4 = (i: 4, null);         // Error: no type
```


在此示例中，四个元组表达式都是有效的。前两个 t1 和 t2 不使用元组表达式的类型，而是应用隐式元组转换。对于 t2，隐式元组转换依赖于从 2 到 long 以及从 null 到 string 的隐式转换。第三个元组表达式具有类型 (int i, string)，因此可以重新分类为该类型的值。另一方面，t4 的声明是错误的：该元组表达式没有类型，因为其第二个元素没有类型。

```
if ((x, y).Equals((1, 2))) { ... };
```

此示例表明，元组有时会导致多层括号，尤其是当元组表达式是方法调用的唯一实参时。

*示例结束*

## 12.8.7 成员访问

### 12.8.7.1 概述

*member_access 由 primary_expression、predefined_type 或 qualified_alias_member 组成，后跟一个 '.' 标记，再后跟一个标识符，可选地后跟一个 type_argument_list。*

```
member_access
: primary_expression '.' identifier type_argument_list?
| predefined_type '.' identifier type_argument_list?
| qualified_alias_member '.' identifier type_argument_list?
;
```

```
predefined_type
: 'bool' | 'byte' | 'char' | 'decimal' | 'double' | 'float' | 'int'
| 'long' | 'object' | 'sbyte' | 'short' | 'string' | 'uint' | 'ulong'
| 'ushort'
;
```

qualified_alias_member 产生式在 §14.8 中定义。

*member_access 的形式为 E . I 或 E . I <A1, ..., An>，其中 E 是 primary_expression、predefined_type 或 qualified_alias_member，I 是单个标识符，<A1, ..., An> 是可选的 type_argument_list。当未指定 type_argument_list 时，将 K 视为零。*

具有 dynamic 类型的 primary_expression 的 member_access 是动态绑定的（§12.3.3）。在这种情况下，编译器将该成员访问分类为 dynamic 类型的属性访问。随后，在运行时应用以下用于确定 member_access 含义的规则，并使用 primary_expression 的运行时类型而不是编译时类型。如果此运行时分类产生方法组，则该成员访问应作为 invocation_expression 的 primary_expression。

member_access 的求值和分类如下：

- 如果 E 是命名空间，并且 E 包含名为 I 的嵌套命名空间，则结果就是该命名空间。
- 否则，如果 E 是命名空间，并且 E 包含具有名称 I 和 K 个类型参数的可访问类型，则结果是用给定类型实参构造的该类型。
- 如果 E 被分类为类型，如果 E 不是类型参数，并且对 E 中的 I 进行具有 K 个类型参数的成员查找（§12.5）产生匹配，则 E . I 的求值和分类如下：
    注意：当此类成员查找的结果是方法组且 K 为零时，该方法组可以包含具有类型参数的方法。这允许此类方法被考虑用于类型实参推断。注释结束
    - 如果 I 标识一个类型，则结果是用任意给定类型实参构造的该类型。
    - 如果 I 标识一个或多个方法，则结果是方法组，不带关联的实例表达式。
    - 如果 I 标识静态属性，则结果是属性访问，不带关联的实例表达式。
    - 如果 I 标识静态字段：
        - 如果该字段是 readonly，并且引用发生在声明该字段的类或结构的静态构造函数之外，则结果是一个值，即 E 中静态字段 I 的值。
        - 否则，结果是一个变量，即 E 中的静态字段 I。
    - 如果 I 标识静态事件：
        - 如果引用发生在声明该事件的类或结构内，并且该事件声明时没有 event_accessor_declarations（§15.8.1），则 E . I 的处理方式与 I 是静态字段时完全相同。
        - 否则，结果是事件访问，不带关联的实例表达式。
    - 如果 I 标识常量，则结果是一个值，即该常量的值。
    - 如果 I 标识枚举成员，则结果是一个值，即该枚举成员的值。
    - 否则，E . I 是无效的成员引用，并且发生编译时错误。
- 如果 E 是属性访问、索引器访问、变量或值，其类型为 T，并且对 T 中的 I 进行具有 K 个类型实参的成员查找（§12.5）产生匹配，则 E . I 的求值和分类如下：
    - 首先，如果 E 是属性或索引器访问，则获取该属性或索引器访问的值（§12.2.2），并将 E 重新分类为值。
    - 如果 I 标识一个或多个方法，则结果是方法组，其关联的实例表达式为 E。
    - 如果 I 标识实例属性，则结果是属性访问，其关联的实例表达式为 E，关联类型为该属性的类型。如果 T 是类类型，则关联类型从以 T 开始查找该属性的第一个声明或重写中选取，并搜索其基类。
    - 如果 T 是 class_type，并且 I 标识该 class_type 的实例字段：
        - 如果 E 的值为 null，则引发 System.NullReferenceException。
        - 否则，如果该字段是 readonly，并且引用发生在声明该字段的类的实例构造函数之外，则结果是一个值，即 E 所引用对象中字段 I 的值。
        - 否则，结果是一个变量，即 E 所引用对象中的字段 I。
    - 如果 T 是 struct_type，并且 I 标识该 struct_type 的实例字段：
        - 如果 E 是值，或者该字段是 readonly 且引用发生在声明该字段的结构的实例构造函数之外，则结果是一个值，即 E 所给定的结构实例中字段 I 的值。
        - 否则，结果是一个变量，即 E 所给定的结构实例中的字段 I。
    - 如果 I 标识实例事件：
        - 如果引用发生在声明该事件的类或结构内，并且该事件声明时没有 event_accessor_declarations（§15.8.1），并且该引用不作为 += 或 -= 运算符的左侧出现，则 E.I 的处理方式与 I 是实例字段时完全相同。
        - 否则，结果是事件访问，其关联的实例表达式为 E。
- 否则，尝试将 E.I 作为扩展方法调用（§12.8.9.3）处理。如果失败，则 E.I 是无效的成员引用，并且发生绑定期错误。

### 12.8.7.2 相同的简单名称和类型名称

在形式为 E.I 的成员访问中，如果 E 是单个标识符，并且 E 作为 simple_name（§12.8.4）的含义是常量、字段、属性、局部变量或参数，且其类型与 E 作为 type_name（§7.8.1）的含义相同，则允许 E 的两种可能含义。E.I 的成员查找从不会产生歧义，因为在这两种情况下，I 都必然是类型 E 的成员。换句话说，该规则只是允许访问 E 的静态成员和嵌套类型，而在其他情况下本会发生编译时错误。

示例：

```csharp
struct Color
{
    public static readonly Color White = new Color(...);
    public static readonly Color Black = new Color(...);
    public Color Complement() => new Color(...);
}

class A
{
    public «Color» Color;        // Field Color of type Color

    void F()
    {
        Color = «Color».Black;    // Refers to Color.Black static member
        Color = Color.Complement(); // Invokes Complement() on Color field
    }

    static void G()
    {
        «Color» c = «Color».White;    // Refers to Color.White static member
    }
}
```

仅出于说明目的，在 A 类内，那些引用 Color 类型的 Color 标识符出现位置用 «...» 分隔，而那些引用 Color 字段的位置则不用。

*示例结束*




## 12.8.8 空条件成员访问

null_conditional_member_access 是一个条件版本的 member_access (§12.8.7)，如果结果类型为 void，则为绑定时错误。对于结果类型可能为 void 的空条件表达式，请参见 (§12.8.10)。

null_conditional_member_access 由 primary_expression 组成，后跟两个标记 “?” 和 “.”，后跟一个带有可选 type_argument_list 的标识符，后跟零个或多个 dependent_accesses。

```
null_conditional_member_access
  : primary_expression '?' '.' identifier type_argument_list?
    dependent_access*
  ;

dependent_access
  : '.' identifier type_argument_list?   // member access
  | '[' argument_list ']'                // element access
  | '(' argument_list? ')'               // invocation
  ;

null_conditional_projection_initializer
  : primary_expression '?' '.' identifier type_argument_list?
  ;
```

null_conditional_member_access 表达式 E 的形式为 P?.A。其含义确定如下：

- 如果 P 的类型为可空值类型：
  - 设 T 为 P.Value.A 的类型。
  - 如果 T 是类型参数且无法确定为引用类型或非可空值类型，则发生编译时错误。
  - 如果 T 是非可空值类型，则 E 的类型为 T?，且 E 的含义与以下含义相同：
    ((object)P == null) ? (T?)null : P.Value.A
    除非 P 仅被求值一次。
  - 否则 E 的类型为 T，且 E 的含义与以下含义相同：
    ((object)P == null) ? (T)null : P.Value.A
    除非 P 仅被求值一次。
- 否则：
  - 设 T 为表达式 P.A 的类型。
  - 如果 T 是类型参数且无法确定为引用类型或非可空值类型，则发生编译时错误。
  - 如果 T 是非可空值类型，则 E 的类型为 T?，且 E 的含义与以下含义相同：
    ((object)P == null) ? (T?)null : P.A
    除非 P 仅被求值一次。

否则 E 的类型为 T，且 E 的含义与以下含义相同：

```
((object)P == null) ? (T)null : P.A
```

除非 P 仅被求值一次。

注意：在形式为：

```
P?.A₀?.A₁
```

则如果 P 求值为 null，则 A₀ 和 A₁ 都不会被求值。如果表达式是 null_conditional_member_access 或 null_conditional_element_access §12.8.12 操作的序列，则同样适用。

结束注意

null_conditional_projection_initializer 是 null_conditional_member_access 的限制，具有相同的语义。它仅作为匿名对象创建表达式 (§12.8.16.7) 中的投影初始化器出现。

## 12.8.9 调用表达式

### 12.8.9.1 通用

invocation_expression 用于调用方法。

```
invocation_expression
: primary_expression '(' argument_list? ')'
;
```

invocation_expression 在以下任一条件成立时为动态绑定 (§12.3.3)：

- primary_expression 的编译时类型为 dynamic。
- 可选 argument_list 的至少一个参数的编译时类型为 dynamic。

在这种情况下，编译器将 invocation_expression 分类为类型为 dynamic 的值。随后用于确定 invocation_expression 含义的规则将在运行时应用，使用运行时类型代替具有编译时类型 dynamic 的 primary_expression 和参数的编译时类型。如果 primary_expression 没有编译时类型 dynamic，则方法调用将进行如 §12.6.5 中所述的有限编译时检查。

invocation_expression 的 primary_expression 必须是一个方法组或 delegate_type 的值。如果 primary_expression 是方法组，则 invocation_expression 为方法调用 (§12.8.9.2)。如果 primary_expression 是 delegate_type 的值，则 invocation_expression 为委托调用 (§12.8.9.4)。如果 primary_expression 既不是方法组也不是 delegate_type 的值，则发生绑定时错误。

可选的 argument_list (§12.6.2) 为方法参数提供值或变量引用。

求值 invocation_expression 的结果分类如下：

- 如果 invocation_expression 调用 returns-no-value 方法 (§15.6.1) 或 returns-no-value 委托，则结果为 nothing。被分类为 nothing 的表达式仅允许在 statement_expression (§13.7) 的上下文中或作为 lambda_expression (§12.19) 的主体出现。否则，发生绑定时错误。
- 否则，如果 invocation_expression 调用 returns-by-ref 方法 (§15.6.1) 或 returns-by-ref 委托，则结果是一个变量，其关联类型为方法或委托的返回类型。如果调用的是实例方法，且接收者为类类型 T，则关联类型取自从 T 开始并搜索其基类时找到的方法的第一个声明或重写。
- 否则，invocation_expression 调用 returns-by-value 方法 (§15.6.1) 或 returns-by-value 委托，结果为一个值，其关联类型为方法或委托的返回类型。如果调用的是实例方法，且接收者为类类型 T，则关联类型取自从 T 开始并搜索其基类时找到的方法的第一个声明或重写。

### 12.8.9.2 方法调用

对于方法调用，invocation_expression 的 primary_expression 必须是一个方法组。方法组标识要调用的单个方法，或从中选择特定方法调用的重载方法集合。在后一种情况下，要调用的具体方法的确定基于 argument_list 中参数类型提供的上下文。

形式为 M(A) 的方法调用的绑定时处理，其中 M 是方法组（可能包括 type_argument_list），A 是可选 argument_list，由以下步骤组成：

- 构造方法调用的候选方法集合。对于与方法组 M 关联的每个方法 F：
  - 如果 F 是非泛型的，则当满足以下条件时 F 为候选：
    - M 没有类型参数列表，且
    - F 相对于 A 是适用的 (§12.6.4.2)。
  - 如果 F 是泛型的且 M 没有类型参数列表，则当满足以下条件时 F 为候选：
    - 类型推断 (§12.6.3) 成功，推断出调用的类型参数列表，且
    - 一旦将推断出的类型参数替换为相应的方法类型参数，F 的参数列表中的所有构造类型均满足其约束 (§8.4.5)，且 F 的参数列表相对于 A 是适用的 (§12.6.4.2)
  - 如果 F 是泛型的且 M 包含类型参数列表，则当满足以下条件时 F 为候选：
    - F 的方法类型参数数量与类型参数列表中提供的数量相同，且
    - 一旦将类型参数替换为相应的方法类型参数，F 的参数列表中的所有构造类型均满足其约束 (§8.4.5)，且 F 的参数列表相对于 A 是适用的 (§12.6.4.2)。
- 候选方法集合被缩减为仅包含来自最派生类型的 方法：对于集合中的每个方法 C.F，其中 C 是声明方法 F 的类型，所有在 C 的基类型中声明的方法都从集合中移除。此外，如果 C 是 object 以外的类类型，则所有在接口类型中声明的方法都从集合中移除。注意：此后一条规则仅在方法组是针对具有除 object 以外的有效基类且非空有效接口集合的类型参数进行的成员查找结果时才有效。结束注意
- 如果得到的候选方法集合为空，则放弃后续步骤的处理，而是尝试将调用作为扩展方法调用 (§12.8.9.3) 处理。如果失败，则不存在适用的方法，并发生绑定时错误。



如果在给定命名空间或编译单元中通过 using 命名空间指令导入的命名空间直接包含具有合格扩展方法 M_e 的非泛型类型声明 C_i，则这些扩展方法的集合即为候选集。

- 如果在任何封闭的命名空间声明或编译单元中均未找到候选集，则会发生编译时错误。
- 否则，将按照 §12.6.4 中所述对候选集应用重载解析。如果找不到唯一最佳方法，则会发生编译时错误。
- C 是最佳方法作为扩展方法声明所在的<|message|>。

使用 C 作为目标，然后将方法调用作为静态方法调用处理 (§12.6.6)。

> 注：与实例方法调用不同，当 expr 求值为 null 引用时不会抛出异常。相反，此 null 值会作为常规静态方法调用一样传递给扩展方法。如何响应此类调用由扩展方法实现决定。结束注释

前述规则意味着实例方法优先于扩展方法，内部命名空间声明中可用的扩展方法优先于外部命名空间声明中可用的扩展方法，并且直接在命名空间中声明的扩展方法优先于通过 using 命名空间指令导入到同一命名空间中的扩展方法。

示例：

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
    static void Test(A a, B b, C c)
    {
        a.F(1);          // E.F(object, int)
        a.F("hello");    // E.F(object, string)
        b.F(1);          // B.F(int)
        b.F("hello");    // E.F(object, string)
        c.F(1);          // C.F(object)
        c.F("hello");    // C.F(object)
    }
}
```

在示例中，B 的方法优先于第一个扩展方法，C 的方法优先于两个扩展方法。

```csharp
public static class C
{
    public static void F(this int i) => Console.WriteLine($"C.F({i})");
    public static void G(this int i) => Console.WriteLine($"C.G({i})");
    public static void H(this int i) => Console.WriteLine($"C.H({i})");
}
```

```csharp
namespace N1
{
    public static class D
    {
        public static void F(this int i) => Console.WriteLine($"D.F({i})");
        public static void G(this int i) => Console.WriteLine($"D.G({i})");
    }
}
```

```csharp
namespace N2
{
    using N1;

    public static class E
    {
        public static void F(this int i) => Console.WriteLine($"E.F({i})");
    }

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
```

此示例的输出为：

E.F(1)
D.G(2)
C.H(3)

D.G 优先于 C.G，E.F 优先于 D.F 和 C.F 两个。

*结束示例*

## 12.8.9.4 委托调用

对于委托调用，invocation_expression 的 primary_expression 必须是一个 delegate_type 的值。此外，将 delegate_type 视为具有与 delegate_type 相同参数列表的函数成员，delegate_type 必须相对于 invocation_expression 的 argument_list 可适用 (§12.6.4.2)。

形式为 D(A) 的委托调用的运行时处理，其中 D 是 delegate_type 的 primary_expression，A 是可选的 argument_list，包括以下步骤：

- 对 D 进行求值。如果此求值导致异常，则不执行后续步骤。
- 对参数列表 A 进行求值。如果此求值导致异常，则不执行后续步骤。
- 检查 D 的值是否有效。如果 D 的值为 null，则抛出 System.NullReferenceException 且不执行后续步骤。
- 否则，D 是对委托实例的引用。对委托的调用列表中的每个可调用实体执行函数成员调用 (§12.6.6)。对于由实例和实例方法组成的可调用实体，调用的实例是可调用实体中包含的实例。

有关无参数的多重调用列表的详细信息，请参阅 §20.6。

## 12.8.10 空条件调用表达式

null_conditional_invocation_expression 在语法上要么是 null_conditional_member_access (§12.8.8)，要么是 null_conditional_element_access (§12.8.12)，其中最终的 dependent_access 是一个调用表达式 (§12.8.9)。

null_conditional_invocation_expression 出现在 statement_expression (§13.7)、anonymous_function_body (§12.19.1) 或 method_body (§15.6.1) 的上下文中。

与语法上等效的 null_conditional_member_access 或 null_conditional_element_access 不同，null_conditional_invocation_expression 可能被分类为 nothing。

```
null_conditional_invocation_expression
  : null_conditional_member_access '(' argument_list? ')'
  | null_conditional_element_access '(' argument_list? ')'
  ;
```

null_conditional_invocation_expression 表达式 E 的形式为 P?A; 其中 A 是语法上等效的 null_conditional_member_access 或 null_conditional_element_access 的剩余部分，A 因此将以 . 或 [ 开始。令 PA 表示 P 和 A 的连接。

当 E 作为 statement_expression 出现时，E 的含义与以下语句的含义相同：

```
if ((object)P != null) PA
```

只是 P 仅求值一次。

当 E 作为 anonymous_function_body 或 method_body 出现时，E 的含义取决于其分类：

- 如果 E 被分类为 nothing 则其含义与以下块的含义相同：
  { if ((object)P != null) PA; }
  只是 P 仅求值一次。
- 否则 E 的含义与以下块的含义相同：
  { return E; }
  而此块的含义又取决于 E 是否在语法上等同于 null_conditional_member_access (§12.8.8) 或 null_conditional_element_access (§12.8.12)。

## 12.8.11 元素访问

### 12.8.11.1 一般

element_access 由 primary_no_array_creation_expression 组成，后跟 "[" 标记，后跟 argument_list，后跟 "]" 标记。argument_list 由一个或多个由逗号分隔的参数组成。

```
element_access
  : primary_no_array_creation_expression '[' argument_list ']'
  ;
```

element_access 的 argument_list 不允许包含 out 或 ref 参数。

如果满足以下任一条件，则 element_access 是动态绑定的 (§12.3.3)：

- primary_no_array_creation_expression 的编译时类型为 dynamic。
- argument_list 的至少一个表达式的编译时类型为 dynamic 且 primary_no_array_creation_expression 不具有数组类型。

在这种情况下，编译器将 element_access 分类为类型为 dynamic 的值。然后在运行时应用下面确定 element_access 含义的规则，使用运行时类型代替具有编译时类型 dynamic 的 primary_no_array_creation_expression 和 argument_list 表达式的编译时类型。如果 primary_no_array_creation_expression 不具有编译时类型 dynamic，则元素访问会进行 §12.6.5 中所述的有限编译时检查。

如果 element_access 的 primary_no_array_creation_expression 是 array_type 的值，则 element_access 是数组访问 (§12.8.11.2)。否则，primary_no_array_creation_expression 必须是一个类、结构或接口类型的变量或值，该类型具有一个或多个索引器成员，在这种情况下 element_access 是索引器访问 (§12.8.11.3)。

### 12.8.11.2 数组访问

对于数组访问，element_access 的 primary_no_array_creation_expression 必须是一个 array_type 的值。此外，数组访问的 argument_list 不允许包含命名参数。argument_list 中的表达式数量必须与 array_type 的秩相同，并且每个表达式的类型必须为 int、uint、long 或 ulong，或可隐式转换为其中一种或多种类型。

求值数组访问的结果是数组元素类型的变量，即由 argument_list 中表达式的值选择的数组元素。

形式为 P[A] 的数组访问的运行时处理，其中 P 是 array_type 的 primary_no_array_creation_expression，A 是 argument_list，包括以下步骤：

- 对 P 进行求值。如果此求值导致异常，则不执行后续步骤。
- 按从左到右的顺序求值 argument_list 的索引表达式。求值每个索引表达式后，执行一次到以下类型之一的隐式转换 (§10.2)：int、uint、long、ulong。选择列表中存在隐式转换的第一个类型。例如，如果索引表达式的类型为 short，则执行到 int 的隐式转换，因为从 short 到 int 和从 short 到 long 都存在隐式转换。如果索引表达式的求值或随后的隐式转换导致异常，则不再求值其他索引表达式且不执行后续步骤。



- `P` 的值会被检查是否有效。如果 `P` 的值是 `null`，则会抛出 `System.NullReferenceException` 且不再执行后续步骤。
- *argument_list* 中每个表达式的值会与 `P` 引用的数组实例每个维度的实际边界进行检查。如果一个或多个值超出范围，则会抛出 `System.IndexOutOfRangeException` 且不再执行后续步骤。
- 由索引表达式给出的数组元素的位置会被计算，并且该位置成为数组访问的结果。

## 12.8.11.3 索引器访问

对于索引器访问，*element_access* 的 *primary_no_array_creation_expression* 必须是一个类、结构体或接口类型的变量或值，并且该类型必须实现一个或多个相对于 *element_access* 的 *argument_list* 而适用的索引器。

形式为 `P[A]` 的索引器访问的绑定时处理，其中 `P` 是类、结构体或接口类型 `T` 的 *primary_no_array_creation_expression*，`A` 是 *argument_list*，包含以下步骤：

- 构造 `T` 提供的索引器集合。该集合由在 `T` 或 `T` 的基类型中声明的、不是重写声明且在当前上下文中可访问 (§7.5) 的所有索引器组成。
- 该集合被缩小为那些适用且未被其他索引器隐藏的索引器。对集合中每个索引器 `S.I` 应用以下规则，其中 `S` 是声明索引器 `I` 的类型：
  - 如果 `I` 相对于 `A` 不适用 (§12.6.4.2)，则 `I` 从集合中移除。
  - 如果 `I` 相对于 `A` 适用 (§12.6.4.2)，则所有在 `S` 的基类型中声明的索引器都从集合中移除。
  - 如果 `I` 相对于 `A` 适用 (§12.6.4.2) 且 `S` 是除 `object` 之外的类类型，则所有在接口中声明的索引器都从集合中移除。
- 如果候选索引器集合为空，则不存在适用的索引器，并发生绑定时错误。
- 使用 §12.6.4 的重载解析规则识别候选索引器集合中的最佳索引器。如果无法识别单一最佳索引器，则索引器访问不明确，并发生绑定时错误。
- *argument_list* 的索引表达式按从左到右的顺序求值。处理索引器访问的结果是一个被归类为索引器访问的表达式。索引器访问表达式引用上述步骤中确定的索引器，并具有关联的实例表达式 `P`、关联的参数列表 `A`，以及关联的类型即索引器的类型。如果 `T` 是类类型，则关联的类型取自从 `T` 开始并搜索其基类时找到的索引器的第一个声明或重写。

根据使用上下文，索引器访问会触发索引器的 *get_accessor* 或 *set_accessor* 的调用。如果索引器访问是赋值的目标，则调用 *set_accessor* 以分配新值 (§12.21.2)。在所有其他情况下，调用 *get_accessor* 以获取当前值 (§12.2.2)。

## 12.8.12 空条件元素访问

null_conditional_element_access 由 *primary_no_array_creation_expression* 组成，其后是两个标记 "?" 和 "["，其后是 *argument_list*，其后是 "]" 标记，其后是零个或多个 *dependent_accesses*。

```
null_conditional_element_access
    : primary_no_array_creation_expression '?' '[' argument_list ']'
      dependent_access*
    ;
```

null_conditional_element_access 是 element_access (§12.8.11) 的条件版本，如果结果类型为 void，则为绑定时错误。有关结果类型可能为 void 的空条件表达式，请参见 (§12.8.10)。

null_conditional_element_access 表达式 E 的形式为 P?[A]B；其中 B 为 *dependent_accesses*（如果有）。E 的含义如下确定：

- 如果 P 的类型为可空值类型：
  设 T 为表达式 P.Value[A]B 的类型。
  - 如果 T 是类型参数且已知既不是引用类型也不是非可空值类型，则发生编译时错误。
  - 如果 T 是非可空值类型，则 E 的类型为 T?，并且 E 的含义与以下含义相同：
    ((object)P == null) ? (?T)null : P.Value[A]B
    只是 P 仅求值一次。
  - 否则 E 的类型为 T，并且 E 的含义与以下含义相同：
    ((object)P == null) ? null : P.Value[A]B
    只是 P 仅求值一次。
- 否则：
  设 T 为表达式 P[A]B 的类型。
  - 如果 T 是类型参数且已知既不是引用类型也不是非可空值类型，则发生编译时错误。
  - 如果 T 是非可空值类型，则 E 的类型为 T?，并且 E 的含义与以下含义相同：
    ((object)P == null) ? (?T)null : P[A]B
    只是 P 仅求值一次。
  - 否则 E 的类型为 T，并且 E 的含义与以下含义相同：
    ((object)P == null) ? null : P[A]B
    只是 P 仅求值一次。

注：对于形式为：
P?[A₀]?[A₁]
的表达式，如果 P 求值为 null，则 A₀ 或 A₁ 都不会被求值。如果表达式是 null_conditional_element_access 或 null_conditional_member_access §12.8.8 操作的序列，则情况相同。

end note

## 12.8.13 This 访问

this_access 由关键字 this 组成。

```
this_access
  : 'this'
  ;
```

this_access 仅允许在实例构造函数、实例方法、实例访问器 (§12.2.1) 或终结器的块中使用。它具有以下其中一种含义：

- 当 this 在类的实例构造函数内的 *primary_expression* 中使用时，它被归类为值。该值类型为使用发生所在的类的实例类型 (§15.3.2)，并且该值是对正在构造的对象的引用。
- 当 this 在类的实例方法或实例访问器内的 *primary_expression* 中使用时，它被归类为值。该值类型为使用发生所在的类的实例类型 (§15.3.2)，并且该值是对调用该方法或访问器的对象的引用。
- 当 this 在结构体的实例构造函数内的 *primary_expression* 中使用时，它被归类为变量。该变量类型为使用发生所在的结构体的实例类型 (§15.3.2)，并且该变量表示正在构造的结构体。
  - 如果构造函数声明没有构造函数初始值设定项，则 this 变量的行为与结构体类型的 out 参数完全相同。特别是，这意味着变量必须在实例构造函数的每条执行路径中都被明确赋值。
  - 否则，this 变量的行为与结构体类型的 ref 参数完全相同。特别是，这意味着变量被视为初始已赋值。
- 当 this 在结构体的实例方法或实例访问器内的 *primary_expression* 中使用时，它被归类为变量。该变量类型为使用发生所在的结构体的实例类型 (§15.3.2)。
  - 如果方法或访问器不是迭代器 (§15.14) 或 async 函数 (§15.15)，则 this 变量表示调用该方法或访问器的结构体。
    - 如果结构体是只读结构体，则 this 变量的行为与结构体类型的 in 参数完全相同
    - 否则 this 变量的行为与结构体类型的 ref 参数完全相同
  - 如果方法或访问器是迭代器或 async 函数，则 this 变量表示调用该方法或访问器的结构体的副本，并与结构体类型的值参数的行为完全相同。

在上述列表之外的上下文中在 *primary_expression* 中使用 this 是编译时错误。特别是，不能在静态方法、静态属性访问器或字段声明的 *variable_initializer* 中引用 this。

## 12.8.14 Base 访问

base_access 由关键字 base 组成，其后是 “.” 标记和标识符以及可选的 *type_argument_list*，或用方括号括起来的 *argument_list*：

```
base_access
  : 'base' '.' identifier type_argument_list?
  | 'base' '[' argument_list ']'
  ;
```

base_access 用于访问被当前类或结构体中同名成员隐藏的基类成员。base_access 只允许出现在实例构造函数、实例方法、实例访问器（§12.2.1）或终结器的块中。当 base.I 出现在类或结构体中时，I 应表示该类或结构体的基类的成员。同样，当 base[E] 出现在类中时，基类中应存在适用的索引器。

在绑定期，形式为 base.I 和 base[E] 的 base_access 表达式会完全按照它们被写成 ((B)this).I 和 ((B)this)[E] 的方式求值，其中 B 是出现该构造的类或结构体的基类。因此，base.I 和 base[E] 对应于 this.I 和 this[E]，只不过 this 被视为基类的实例。

当 base_access 引用虚函数成员（方法、属性或索引器）时，在运行时（§12.6.6）确定要调用哪个函数成员的方式会改变。所调用的函数成员通过查找该函数成员相对于 B 的最派生实现（§15.6.4）来确定（而不是像非 base 访问中通常那样相对于 this 的运行时类型来确定）。因此，在虚函数成员的重写中，可以使用 base_access 来调用该函数成员的继承实现。如果 base_access 引用的函数成员是抽象的，则发生绑定期错误。

> 注意：与 this 不同，base 本身不是表达式。它只是一个仅用于 base_access 或 constructor_initializer（§15.11.2）上下文中的关键字。结束注释

## 12.8.15 后缀递增和递减运算符

```
post_increment_expression
  : primary_expression '++'
  ;
```

```
post_decrement_expression
  : primary_expression '--'
  ;
```

后缀递增或递减运算的操作数应为分类为变量、属性访问或索引器访问的表达式。该运算的结果是与操作数类型相同的值。

如果 primary_expression 具有编译时类型 dynamic，则该运算符进行动态绑定（§12.3.3），post_increment_expression 或 post_decrement_expression 具有编译时类型 dynamic，并且在运行时使用 primary_expression 的运行时类型应用以下规则。

如果后缀递增或递减运算的操作数是属性访问或索引器访问，则该属性或索引器应同时具有 get 访问器和 set 访问器。如果不是这种情况，则发生绑定期错误。

应用一元运算符重载决策（§12.4.4）来选择特定的运算符实现。

预定义的 ++ 和 -- 运算符适用于以下类型：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 以及任何枚举类型。预定义的 ++ 运算符返回将操作数加 1 所产生的值，预定义的 -- 运算符返回从操作数减 1 所产生的值。在 checked 上下文中，如果此加法或减法的结果超出结果类型的范围，并且结果类型为整型或枚举类型，则抛出 System.OverflowException。

从所选一元运算符的返回类型到 primary_expression 的类型应存在隐式转换，否则发生编译时错误。

形式为 x++ 或 x-- 的后缀递增或递减运算的运行时处理包括以下步骤：

- 如果 x 分类为变量：
  - 对 x 求值以产生该变量。
  - 保存 x 的值。
  - 将保存的 x 值转换为所选运算符的操作数类型，并以该值作为参数调用该运算符。
  - 将运算符返回的值转换为 x 的类型，并存储到先前对 x 求值所得的位置中。
  - 保存的 x 值成为该运算的结果。
- 如果 x 分类为属性访问或索引器访问：
  - 对与 x 关联的实例表达式（如果 x 不是 static）和参数列表（如果 x 是索引器访问）求值，并将结果用于后续的 get 和 set 访问器调用。
  - 调用 x 的 get 访问器并保存返回的值。
  - 将保存的 x 值转换为所选运算符的操作数类型，并以该值作为参数调用该运算符。
  - 将运算符返回的值转换为 x 的类型，并以该值作为 value 参数调用 x 的 set 访问器。
  - 保存的 x 值成为该运算的结果。

++ 和 -- 运算符还支持前缀表示法（§12.9.6）。通常，x++ 或 x-- 的结果是运算前 x 的值，而 ++x 或 --x 的结果是运算后 x 的值。在任一情况下，运算后 x 本身的值相同。

operator ++ 或 operator -- 实现可以使用后缀或前缀表示法调用。无法为这两种表示法分别提供不同的运算符实现。

## 12.8.16 new 运算符

### 12.8.16.1 概述

new 运算符用于创建类型的新实例。

new 表达式有三种形式：
- 对象创建表达式和匿名对象创建表达式用于创建类类型和值类型的新实例。
- 数组创建表达式用于创建数组类型的新实例。
- 委托创建表达式用于获取委托类型的实例。

new 运算符意味着创建类型的实例，但不一定意味着分配内存。特别地，值类型的实例除了其所驻留的变量之外不需要额外的内存，并且当使用 new 创建值类型的实例时不会发生分配。

> 注意：委托创建表达式并不总是创建新实例。当该表达式以与方法组转换（§10.8）或匿名函数转换（§10.7）相同的方式处理时，这可能导致重用现有的委托实例。结束注释

### 12.8.16.2 对象创建表达式

object_creation_expression 用于创建 class_type 或 value_type 的新实例。

```
object_creation_expression
  : 'new' type '(' argument_list? ')' object_or_collection_initializer?
  | 'new' type object_or_collection_initializer
  ;

object_or_collection_initializer
  : object_initializer
  | collection_initializer
  ;
```

object_creation_expression 的类型应为 class_type、value_type 或 type_parameter。该类型不能是 tuple_type，也不能是抽象或静态 class_type。

仅当类型为 class_type 或 struct_type 时，才允许使用可选的 argument_list（§12.6.2）。

对象创建表达式可以省略构造函数参数列表和封闭括号，前提是它包含对象初始值设定项或集合初始值设定项。省略构造函数参数列表和封闭括号等同于指定空参数列表。

处理包含对象初始值设定项或集合初始值设定项的对象创建表达式包括：先处理实例构造函数，然后处理由对象初始值设定项（§12.8.16.3）或集合初始值设定项（§12.8.16.4）指定的成员或元素初始化。

如果可选 argument_list 中的任何参数具有编译时类型 dynamic，则 object_creation_expression 进行动态绑定（§12.3.3），并且在运行时使用 argument_list 中那些具有编译时类型 dynamic 的参数的运行时类型应用以下规则。但是，对象创建会经历 §12.6.5 所述的有限编译时检查。

形式为 new T(A) 的 object_creation_expression 的绑定期处理（其中 T 是 class_type 或 value_type，A 是可选 argument_list）包括以下步骤：
- 如果 T 是 value_type 且 A 不存在：
  - object_creation_expression 是默认构造函数调用。object_creation_expression 的结果是类型 T 的值，即 §8.3.3 中定义的 T 的默认值。
- 否则，如果 T 是 type_parameter 且 A 不存在：
  - 如果未为 T 指定值类型约束或构造函数约束（§15.2.5），则发生绑定期错误。
  - object_creation_expression 的结果是类型参数所绑定到的运行时类型的值，即调用该类型的默认构造函数的结果。该运行时类型可以是引用类型或值类型。
- 否则，如果 T 是 class_type 或 struct_type：
  - 如果 T 是抽象或静态 class_type，则发生编译时错误。
  - 要调用的实例构造函数使用 §12.6.4 的重载决策规则确定。候选实例构造函数的集合由所有可访问的实例构造函数组成

在 T 中声明且相对于 A 适用的实例构造函数（§12.6.4.2）。如果候选实例构造函数集合为空，或者无法确定单个最佳实例构造函数，则发生绑定期错误。

- object_creation_expression 的结果是类型 T 的值，即通过调用上一步中确定的实例构造函数所生成的值。
- 否则，object_creation_expression 无效，并发生绑定期错误。

即使 object_creation_expression 是动态绑定的，其编译时类型仍然是 T。

形式为 new T(A) 的 object_creation_expression 的运行时处理（其中 T 为 class_type 或 struct_type，A 为可选的 argument_list）包括以下步骤：

- 如果 T 是 class_type：
  - 分配类 T 的新实例。如果没有足够内存来分配新实例，则引发 System.OutOfMemoryException，并且不执行后续步骤。
  - 新实例的所有字段都初始化为其默认值（§9.3）。
  - 按照函数成员调用规则（§12.6.6）调用实例构造函数。对新分配实例的引用会自动传递给实例构造函数，并且在该构造函数内可以通过 this 访问该实例。

- 如果 T 是 struct_type：
  - 通过分配临时局部变量来创建类型 T 的实例。由于 struct_type 的实例构造函数必须为所创建实例的每个字段明确赋值，因此不需要初始化临时变量。
  - 按照函数成员调用规则（§12.6.6）调用实例构造函数。对新分配实例的引用会自动传递给实例构造函数，并且在该构造函数内可以通过 this 访问该实例。

## 12.8.16.3 对象初始值设定项

对象初始值设定项指定对象的零个或多个字段、属性或索引元素的值。

```
object_initializer
: '{' member_initializer_list? '}'
| '{' member_initializer_list ',' '}'
;

member_initializer_list
: member_initializer (',' member_initializer)*
;

member_initializer
: initializer_target '=' initializer_value
;

initializer_target
: identifier
| '[' argument_list ']'
;

initializer_value
: expression
| object_or_collection_initializer
;
```

对象初始值设定项由一系列成员初始值设定项组成，这些成员初始值设定项用 { 和 } 标记括起来，并用逗号分隔。每个 member_initializer 应指定一个初始化目标。标识符应命名正在初始化的对象的一个可访问字段或属性，而用方括号括起来的 argument_list 应指定正在初始化的对象上某个可访问索引器的实参。对象初始值设定项为同一字段或属性包含多个成员初始值设定项是错误的。

> 注意：虽然不允许对象初始值设定项多次设置同一字段或属性，但对索引器没有此类限制。对象初始值设定项可以包含多个引用索引器的初始值设定项目标，甚至可以多次使用相同的索引器实参。注释结束

每个 initializer_target 后面都跟一个等号，以及一个表达式、对象初始值设定项或集合初始值设定项。对象初始值设定项内的表达式不可能引用它正在初始化的新创建对象。

在等号后指定表达式的成员初始值设定项，其处理方式与对目标进行赋值（§12.21.2）相同。

在等号后指定对象初始值设定项的成员初始值设定项是嵌套对象初始值设定项，即嵌入式对象的初始化。嵌套对象初始值设定项中的赋值不会向该字段或属性赋新值，而是被视为对该字段或属性的成员进行赋值。嵌套对象初始值设定项不能应用于值类型的属性，也不能应用于值类型的只读字段。

在等号后指定集合初始值设定项的成员初始值设定项是嵌入式集合的初始化。该初始值设定项中给出的元素会添加到目标所引用的集合中，而不是向目标字段、属性或索引器分配新集合。目标的类型应为满足 §12.8.16.4 中所指定要求的集合类型。

当初始值设定项目标引用索引器时，索引器的实参必须始终恰好求值一次。因此，即使这些实参最终从未被使用（例如，因为嵌套初始值设定项为空），也会为产生副作用而对它们求值。

示例：以下类表示具有两个坐标的点：

```
public class Point
{
    public int X { get; set; }
    public int Y { get; set; }
}
```

可以按如下方式创建并初始化 Point 的实例：

```
Point a = new Point { X = 0, Y = 1 };
```

其效果与以下代码相同：

```
Point __a = new Point();
__a.X = 0;
__a.Y = 1;
Point a = __a;
```

其中 __a 是一个在其他情况下不可见且不可访问的临时变量。

以下类展示了由两个点创建的矩形，以及 Rectangle 实例的创建和初始化：

```
public class Rectangle
{
    public Point P1 { get; set; }
    public Point P2 { get; set; }
}
```

可以按如下方式创建并初始化 Rectangle 的实例：

```
Rectangle r = new Rectangle
{
    P1 = new Point { X = 0, Y = 1 },
    P2 = new Point { X = 2, Y = 3 }
};
```

其效果与以下代码相同：

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

如果 Rectangle 的构造函数分配了这两个嵌入式 Point 实例，则可以用它们来初始化嵌入式 Point 实例，而不是分配新实例：

```
public class Rectangle
{
    public Point P1 { get; } = new Point();
    public Point P2 { get; } = new Point();
}
```

可以使用以下构造来初始化嵌入式 Point 实例，而不是分配新实例：

```
Rectangle r = new Rectangle
{
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```

其效果与以下代码相同：

```
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

示例结束

## 12.8.16.4 集合初始值设定项

集合初始值设定项指定集合的元素。

```
collection_initializer
  : '{' element_initializer_list '}'
  | '{' element_initializer_list ',' '}'
  ;

element_initializer_list
  : element_initializer (',' element_initializer)*
  ;

element_initializer
  : non_assignment_expression
  | '{' expression_list '}'
  ;

expression_list
  : expression
  | expression_list ',' expression
  ;
```

集合初始值设定项由一系列元素初始值设定项组成，这些元素初始值设定项用 { 和 } 标记括起来，并用逗号分隔。每个元素初始值设定项指定要添加到正在初始化的集合对象中的一个元素，并且由用 { 和 } 标记括起来、用逗号分隔的表达式列表组成。单表达式元素初始值设定项可以不带大括号书写，但此时不能是赋值表达式，以避免与成员初始值设定项产生歧义。non_assignment_expression 产生式在 §12.22 中定义。

示例：以下是包含集合初始值设定项的对象创建表达式的示例：

```
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

示例结束

应用集合初始值设定项的集合对象，其类型应实现 System.Collections.IEnumerable，否则发生编译时错误。对于按从左到右顺序指定的每个元素，都会应用常规成员查找来查找名为 Add 的成员。如果成员查找的结果不是方法组，则发生编译时错误。否则，以元素初始值设定项的表达式列表作为实参列表应用重载决策，并且集合初始值设定项调用结果方法。因此，对于每个元素初始值设定项，集合初始值设定项都应包含一个适用的、名为 Add 的实例方法或扩展方法。

示例：以下展示了一个表示包含姓名和电话号码列表的联系人的类，以及 List<Contact> 的创建和初始化：

```
public class Contact
{
    public string Name { get; set; }
    public List<string> PhoneNumbers { get; } = new List<string>();
}

class A
{
    static void M()
```




```
{ var contacts = new List<Contact> { new Contact { Name = "Chris Smith", PhoneNumbers = { "206-555-0101", "425-882-8080" } }, new Contact { Name = "Bob Harris", PhoneNumbers = { "650-555-0199" } } }; }
```

其效果等同于以下代码：

```
var __clist = new List<Contact>();
Contact __c1 = new Contact();
__c1.Name = "Chris Smith";
__c1.PhoneNumbers.Add("206-555-0101");
__c1.PhoneNumbers.Add("425-882-8080");
__clist.Add(__c1);
Contact __c2 = new Contact();
__c2.Name = "Bob Harris";
__c2.PhoneNumbers.Add("650-555-0199");
__clist.Add(__c2);
var contacts = __clist;
```

其中 __clist、__c1 和 __c2 是临时变量，否则它们不可见且不可访问。

示例结束

## 12.8.16.5 数组创建表达式

数组创建表达式用于创建数组类型的新实例。

```
array_creation_expression
: 'new' non_array_type '[' expression_list ']' rank_specifier* array_initializer?
| 'new' array_type array_initializer
| 'new' rank_specifier array_initializer
;
```

第一种形式的数组创建表达式分配一个数组实例，该实例的类型是通过从表达式列表中删除各个表达式后得到的类型。

示例：数组创建表达式 new int[10,20] 生成一个类型为 int[,] 的数组实例，而数组创建表达式 new int[10][,] 生成一个类型为 int[,][,] 的数组实例。示例结束

表达式列表中的每个表达式都应为 int、uint、long 或 ulong 类型，或者可隐式转换为这些类型中的一种或多种。每个表达式的值决定了新分配的数组实例中对应维度的长度。由于数组维度的长度必须为非负数，因此表达式列表中如果存在值为负的常量表达式，则会导致编译时错误。

除非在不安全上下文（§23.2）中，数组的布局是不确定的。

如果第一种形式的数组创建表达式包含数组初始值设定项，则表达式列表中的每个表达式都应为常量，并且表达式列表指定的秩和维度长度应与数组初始值设定项的秩和维度长度匹配。

在第二种或第三种形式的数组创建表达式中，指定的数组类型或秩说明符的秩应与数组初始值设定项的秩一致。各个维度的长度根据数组初始值设定项中相应嵌套级别的元素数量推断得出。因此，以下声明中的初始值设定项表达式

```
var a = new int[,] {{0, 1}, {2, 3}, {4, 5}};
```

正好对应于

```
var a = new int[3, 2] {{0, 1}, {2, 3}, {4, 5}};
```

第三种形式的数组创建表达式称为 *隐式类型数组创建表达式*。它与第二种形式类似，只是数组的元素类型不是显式给出的，而是由数组初始值设定项中的表达式集合的最佳公共类型（§12.6.3.15）确定。对于多维数组，即 *秩说明符* 至少包含一个逗号的数组，该集合包含嵌套的 *数组初始值设定项* 中的所有 *表达式*。

数组初始值设定项在 §17.7 中有进一步描述。

对数组创建表达式求值的结果被归类为值，即对新分配的数组实例的引用。数组创建表达式的运行时处理包括以下步骤：

- *表达式列表* 的维度长度表达式按从左到右的顺序求值。在每次表达式求值之后，执行到以下类型之一的隐式转换（§10.2）：`int`、`uint`、`long`、`ulong`。选择此列表中第一个存在隐式转换的类型。如果表达式求值或后续隐式转换引发异常，则不再求值任何表达式，也不执行任何后续步骤。
- 对计算出的维度长度值进行验证，如下所示：如果有一个或多个值小于零，则抛出 `System.OverflowException`，不再执行任何后续步骤。
- 分配具有给定维度长度的数组实例。如果没有足够内存来分配新实例，则抛出 `System.OutOfMemoryException`，不再执行任何后续步骤。
- 新数组实例的所有元素都初始化为其默认值（§9.3）。
- 如果数组创建表达式包含数组初始值设定项，则对数组初始值设定项中的每个表达式进行求值，并将其赋值给对应的数组元素。求值和赋值按照表达式在数组初始值设定项中的书写顺序执行——换句话说，元素按索引递增顺序初始化，最右侧维度先递增。如果给定表达式的求值或随后对相应数组元素的赋值引发异常，则不再初始化更多元素（因而剩余元素将保留其默认值）。

数组创建表达式允许实例化元素为数组类型的数组，但此类数组的元素必须手动初始化。

示例：语句

```
int[][] a = new int[100][];
```

创建一个包含 100 个 int[] 类型元素的一维数组。每个元素的初始值为 null。同一个数组创建表达式不可能同时实例化子数组，语句

```
int[][] a = new int[100][5]; // Error
```

会导致编译时错误。子数组的实例化可以改为手动执行，如下所示：

```
int[][] a = new int[100][];
for (int i = 0; i < 100; i++)
{
    a[i] = new int[5];
}
```

示例结束

注意：当数组的数组具有“矩形”形状时，即所有子数组的长度都相同，使用多维数组会更高效。在上面的示例中，实例化数组的数组会创建 101 个对象——1 个外层数组和 100 个子数组。相比之下，

```
int[,] a = new int[100, 5];
```

只创建一个对象，即一个二维数组，并且只需一条语句即可完成分配。

注意结束

示例：以下是隐式类型数组创建表达式的示例：

```
var a = new[] { 1, 10, 100, 1000 }; // int[]
var b = new[] { 1, 1.5, 2, 2.5 }; // double[]
var c = new[,] { { "hello", null }, { "world", "!" } }; // string[,]
var d = new[] { 1, "one", 2, "two" }; // Error
```

```
{
    Name = "Bob Harris",
    PhoneNumbers = new[] { "650-555-0199" }
};
```

*示例结束*

## 12.8.16.6 委托创建表达式

*委托创建表达式* 用于获取 *委托类型* 的实例。

```
delegate_creation_expression
  : 'new' delegate_type '(' expression ')'
  ;
```

委托创建表达式的参数应为方法组、匿名函数，或者为编译时类型为 *dynamic* 或 *委托类型* 的值。如果参数是方法组，则它标识方法，并且对于实例方法，还标识要为其创建委托的对象。如果参数是匿名函数，则它直接定义委托目标的参数和方法体。如果参数是一个值，则它标识要创建其副本的委托实例。

如果 *表达式* 的编译时类型为 *dynamic*，则 *委托创建表达式* 是动态绑定的（§12.8.16.6），并且以下规则在运行时使用 *表达式* 的运行时类型来应用。否则，这些规则在编译时应用。

对于形式为 new D(E) 的 *委托创建表达式*（其中 D 是一个 *委托类型*，E 是一个 *表达式*），其绑定时的处理过程包括以下步骤：

- 如果 E 是方法组，则委托创建表达式的处理方式与从 E 到 D 的方法组转换（§10.8）相同。
- 如果 E 是匿名函数，则委托创建表达式的处理方式与从 E 到 D 的匿名函数转换（§10.7）相同。
- 如果 E 是一个值，则 E 应与 D 兼容（§20.2），结果是对新建委托的引用，该委托具有一个单项调用列表，该列表调用 E。

对于形式为 new D(E) 的 *委托创建表达式*（其中 D 是一个 *委托类型*，E 是一个 *表达式*），其运行时处理过程包括以下步骤：

- 如果 E 是方法组，则委托创建表达式按从 E 到 D 的方法组转换（§10.8）进行求值。
- 如果 E 是匿名函数，则委托创建表达式按从 E 到 D 的匿名函数转换（§10.7）进行求值。
- 如果 E 是 *委托类型* 的值：
  - 对 E 进行求值。如果此求值引发异常，则不再执行任何后续步骤。
  - 如果 E 的值为 null，则抛出 System.NullReferenceException，不再执行任何后续步骤。
  - 分配委托类型 D 的新实例。如果没有足够内存来分配新实例，则抛出 System.OutOfMemoryException，不再执行任何后续步骤。
  - 新委托实例使用一个单项调用列表进行初始化，该列表调用 E。




委托的调用列表在委托实例化时确定，然后在委托的整个生命周期内保持不变。换句话说，一旦委托被创建，就无法更改其目标可调用实体。

> 注意：请记住，当两个委托组合在一起或一个委托从另一个委托中移除时，会产生一个新的委托；没有任何现有委托的内容被更改。结束注意

不可能创建引用属性、索引器、用户定义运算符、实例构造函数、终结器或静态构造函数的委托。

示例：如上所述，当从方法组创建委托时，委托的形式参数列表和返回类型决定选择哪个重载方法。在示例中

```
delegate double DoubleFunc(double x);
```

```
class A
{
    DoubleFunc f = new DoubleFunc(Square);
    static float Square(float x) => x * x;
    static double Square(double x) => x * x;
}
```

A.f 字段被初始化为引用第二个 Square 方法的委托，因为该方法与 DoubleFunc 的形式参数列表和返回类型完全匹配。如果没有第二个 Square 方法，则会发生编译时错误。

结束示例

## 12.8.16.7 匿名对象创建表达式

anonymous_object_creation_expression 用于创建匿名类型的对象。

```
anonymous_object_creation_expression
: 'new' anonymous_object_initializer
;

anonymous_object_initializer
: '{' member_declarator_list? '}'
| '{' member_declarator_list ',' '}'
;

member_declarator_list
: member_declarator (',' member_declarator)*
;

member_declarator
: simple_name
| member_access
| null_conditional_projection_initializer
| base_access
| identifier '=' expression
;
```

一个匿名对象初始化器声明一个匿名类型并返回该类型的实例。匿名类型是一个无名的类类型，直接继承自 object。匿名类型的成员是从用于创建该类型实例的匿名对象初始化器推断出来的一系列只读属性。具体来说，形式为的匿名对象初始化器

```
new { p1 = e1 , p2 = e2 , ... pn = en }
```

声明形式为的匿名类型

```
class __Anonymous1
{
    private readonly «T1» «f1»;
    private readonly «T2» «f2»;
    ...
    private readonly «Tn» «fn»;

    public __Anonymous1(«T1» «a1», «T2» «a2»,..., «Tn» «an»)
    {
        «f1» = «a1»;
        «f2» = «a2»;
        ...
        «fn» = «an»;
    }

    public «T1» «p1» { get { return «f1»; } }
    public «T2» «p2» { get { return «f2»; } }
    ...
    public «Tn» «pn» { get { return «fn»; } }
    public override bool Equals(object __o) { ... }
    public override int GetHashCode() { ... }
}
```

其中每个 «Tx» 是对应表达式 «ex» 的类型。member_declarator 中使用的表达式必须具有类型。因此，member_declarator 中的表达式为 null 或匿名函数是编译时错误。

匿名类型的名称及其 Equals 方法的参数名称由编译器自动生成，不能在程序文本中引用。

在同一程序中，指定相同名称和编译时类型且顺序相同的属性序列的两个匿名对象初始化器将生成同一匿名类型的实例。

> *示例：* 在示例中
> ```
> var p1 = new { Name = "Lawnmower", Price = 495.00 };
> var p2 = new { Name = "Shovel", Price = 26.95 };
> p1 = p2;
> ```
> 最后一行的赋值是允许的，因为 p1 和 p2 是同一匿名类型。
> *结束示例*

匿名类型上的 Equals 和 GetHashCode 方法重写了从 object 继承的方法，并根据属性的 Equals 和 GetHashCode 定义，因此同一匿名类型的两个实例相等当且仅当它们的所有属性都相等。

member declarator 可以缩写为 simple name (§12.8.4)、member access (§12.8.7)、null conditional projection initializer (§12.8.8) 或 base access (§12.8.14)。这称为 projection initializer，是对具有相同名称的属性的声明和赋值的简写。具体来说，

```
«identifier»,«expr» . «identifier» and «expr» ? . «identifier»
```

member declarators of the forms
are precisely equivalent to the following, respectively:

```
«identifier» = «identifier»,«identifier» = «expr» . «identifier» and «identifier» = «expr» ? . «identifier»
```

因此，在 projection initializer 中，identifier 同时选择值以及要将值赋给的字段或属性。直观地说，projection initializer 投影的不仅是值，还有值的名称。

## 12.8.17 typeof 运算符

typeof 运算符用于获取类型的 System.Type 对象。

```
typeof_expression
  : 'typeof' '(' 'type' ')'
  | 'typeof' '(' 'unbound_type_name' ')'
  | 'typeof' '(' 'void' ')'
  ;

unbound_type_name
  : identifier generic_dimension_specifier?
  | identifier '::' identifier generic_dimension_specifier?
  | unbound_type_name '.' identifier generic_dimension_specifier?
  ;

generic_dimension_specifier
  : '<' comma* '>'
  ;

comma
  : ','
  ;
```

typeof_expression 的第一种形式由 typeof 关键字后跟带括号的类型组成。此形式表达式的结果是所指示类型的 System.Type 对象。任何给定类型只有一个 System.Type 对象。这意味着对于类型 T，typeof(T) == typeof(T) 始终为 true。类型不能为 dynamic。

typeof_expression 的第二种形式由 typeof 关键字后跟带括号的 unbound_type_name 组成。

> 注意：unbound_type_name 与 type_name (§7.8) 非常相似，只是 unbound_type_name 包含 generic_dimension_specifiers，而 type_name 包含 type_argument_lists。结束注意

当 typeof_expression 的操作数是同时满足 unbound_type_name 和 type_name 文法的标记序列时，即当它既不包含 generic_dimension_specifier 也不包含 type_argument_list 时，该标记序列被视为 type_name。unbound_type_name 的含义确定如下：

- 将标记序列转换为 type_name，将每个 generic_dimension_specifier 替换为具有相同逗号数且每个 type_argument 均为关键字 object 的 type_argument_list。
- 在忽略所有类型参数约束的同时计算 resulting type_name。
- unbound type_name 解析为与 resulting constructed type (§8.4.4) 关联的 unbound generic type。

typeof 表达式的结果是 resulting unbound generic type 的 System.Type 对象。

typeof 表达式的第三种形式由 typeof 关键字后跟带括号的 void 关键字组成。此形式表达式的结果是表示类型缺失的 System.Type 对象。typeof(void) 返回的类型对象与为任何类型返回的类型对象不同。

> 注意：此特殊的 System.Type 对象在允许对语言中的方法进行反射的类库中很有用，在这些类库中，这些方法希望用 System.Type 的实例来表示任何方法的返回类型，包括 void 方法。结束注意

typeof 运算符可用于类型参数。结果是绑定到该类型参数的运行时类型的 System.Type 对象。typeof 运算符也可用于 constructed type 或 unbound generic type (§8.4.4)。unbound generic type 的 System.Type 对象与 instance type (§15.3.2) 的 System.Type 对象不同。instance type 在运行时始终是 closed constructed type，因此其 System.Type 对象取决于正在使用的运行时类型参数。另一方面，unbound generic type 没有类型参数，并且无论运行时类型参数如何都产生相同的 System.Type 对象。

示例：示例

```
class X<T>
{
    public static void PrintTypes()
    {
        Type[] t =
        {
            typeof(int),
            typeof(System.Int32),
            typeof(string),
            typeof(double[]),
            typeof(void),
            typeof(T),
            typeof(X<T>),
            typeof(X<X<T>>),
            typeof(X<>)
        };
        for (int i = 0; i < t.Length; i++)
        {
            Console.WriteLine(t[i]);
        }
    }
}

class Test
{
    static void Main()
{
```



```
}
    X<int>.PrintTypes();
}
```

生成以下输出：

```
System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X`1[System.Int32]
X`1[X`1[System.Int32]]
X`1[T]
```

注意 int 和 System.Int32 是同一类型。typeof(X<>) 的结果不依赖于类型参数，但 typeof(X<T>) 的结果会依赖。

*结束示例*

## 12.8.18 sizeof 运算符

sizeof 运算符返回给定类型变量所占用的 8 位字节数。作为 sizeof 操作数的类型应为 unmanaged_type (§8.8)。

```
sizeof_expression
    : 'sizeof' '(' unmanaged_type ')'
    ;
```

对于某些预定义类型，sizeof 运算符会产生如下表所示的常量 int 值：

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

对于枚举类型 T，表达式 sizeof(T) 的结果是一个常量值，等于其基础类型的大小，如上所述。对于所有其他操作数类型，sizeof 运算符在 §23.6.9 中指定。

```
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;

    static int F() => checked(x * y);    // Throws OverflowException
    static int G() => unchecked(x * y);  // Returns -727379968
    static int H() => x * y;             // Depends on default
}
```

没有报告编译时错误，因为这两个表达式都无法在编译时求值。在运行时，F 方法抛出 System.OverflowException，而 G 方法返回 –727379968（超出范围结果的低 32 位）。H 方法的行为取决于编译的默认溢出检查上下文，但它要么与 F 相同，要么与 G 相同。

*结束示例*

示例：在以下代码中

```
class Test
{
    const int x = 1000000;
    const int y = 1000000;

    static int F() => checked(x * y);    // Compile-time error, overflow
    static int G() => unchecked(x * y);  // Returns -727379968
    static int H() => x * y;             // Compile-time error, overflow
}
```

在 F 和 H 中求值常量表达式时发生的溢出会导致报告编译时错误，因为这些表达式在 checked 上下文中求值。在 G 中求值常量表达式时也会发生溢出，但由于求值是在 unchecked 上下文中进行，因此不会报告溢出。

*结束示例*

checked 和 unchecked 运算符仅影响在 “(” 和 “)” 标记内文本包含的那些操作的溢出检查上下文。这些运算符对因求值包含的表达式而被调用的函数成员没有任何影响。

示例：在以下代码中

```
class Test
{
    static int Multiply(int x, int y) => x * y;

    static int F() => checked(Multiply(1000000, 1000000));
}
```

在 F 中使用 checked 不会影响 Multiply 中 x * y 的求值，因此 x * y 在默认溢出检查上下文中求值。

*结束示例*

当以十六进制表示法编写有符号整数类型的常量时，unchecked 运算符很方便。

示例：

```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

上述两个十六进制常量都是 `uint` 类型。因为这些常量超出了 `int` 范围，所以如果没有 `unchecked` 运算符，转换到 `int` 将会产生编译时错误。

*结束示例*

*注意：* `checked` 和 `unchecked` 运算符和语句允许程序员控制某些数值计算的方面。然而，某些数值运算符的行为取决于其操作数的数据类型。例如，即使在明确的 unchecked 构造中相乘两个 decimal 也始终会在溢出时导致异常。同样，即使在明确的 checked 构造中相乘两个 float 也永远不会在溢出时导致异常。此外，其他运算符不受检查模式的影响，无论是默认还是显式。*结束注释*

## 12.8.20 默认值表达式

默认值表达式用于获取类型的默认值 (§9.3)。

```
default_value_expression
    : explicitly_typed_default
    | default_literal
    ;

explicitly_typed_default
    : 'default' '(' 'type' ')'
    ;

default_literal
    : 'default'
    ;
```

*default_literal* 表示默认值 (§9.3)。它没有类型，但可以通过默认值转换 (§10.2.16) 转换为任何类型。

*default_value_expression* 的结果是 *explicitly_typed_default* 中显式类型的默认值 (§9.3)，或 *default_value_expression* 的转换的目标类型。

- *default_value_expression* 是常量表达式 (§12.23) 如果类型是以下之一：
  - 引用类型
  - 已知为引用类型的类型参数 (§8.2)；
  - 以下值类型之一：`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double`、`decimal`、`bool`；或
  - 任何枚举类型。

## 12.8.21 栈分配

栈分配表达式从执行栈分配一块内存。*执行栈* 是存储局部变量的内存区域。执行栈不是托管堆的一部分。用于局部变量存储的内存会在当前函数返回时自动回收。

栈分配表达式的安全上下文规则在 §16.4.12.7 中描述。

```
stackalloc_expression
  : 'stackalloc' unmanaged_type '[' expression ']'
  | 'stackalloc' unmanaged_type? '[' constant_expression? ']' stackalloc_initializer
  ;

stackalloc_initializer
  : '{' stackalloc_initializer_element_list '}'
  ;

stackalloc_initializer_element_list
  : stackalloc_element_initializer (',' stackalloc_element_initializer)* ','?
  ;

stackalloc_element_initializer
  : expression
  ;
```

- 1. 局部变量声明 (§13.6.2) 的初始化表达式 E；和
- 2. 简单赋值 (§12.21.2) 的右操作数表达式 E，其本身作为表达式语句 (§13.7) 出现

在这两种上下文中，stackalloc_expression 仅允许作为以下形式出现：

- - E 的全部；或
- - 条件表达式 (§12.18) 的第二个和/或第三个操作数，其本身是 E 的全部。

unmanaged_type (§8.8) 表示将存储在新分配位置中的项的类型，而表达式表示这些项的数量。两者合在一起指定所需的分配大小。表达式的类型必须能隐式转换为 int 类型。

由于栈分配的大小不能为负，因此将项的数量指定为求值为负值的 constant_expression 是编译时错误。

在运行时，如果要分配的项数为负值，则行为未定义。如果为零，则不进行分配，并且返回的值是实现定义的。如果没有足够的内存来分配项，则会抛出 System.StackOverflowException。

当存在 stackalloc_initializer 时：

- - 如果省略 unmanaged_type，则根据 stackalloc_element_initializers 集合的最佳公共类型规则 (§12.6.3.15) 推断。
- - 如果省略 constant_expression，则推断为 stackalloc_element_initializers 的数量。
- - 如果存在 constant_expression，则它必须等于 stackalloc_element_initializers 的数量。

- - 结果的 Length 属性返回已分配的项数。
- - 结果的索引器 (§15.9) 返回对已分配块中某项的 variable_reference (§9.5)，并且会进行范围检查。

注意：当在不安全代码中出现时，stackalloc_expression 的结果可能为不同类型，参见 (§23.9)。结束注释

在 catch 或 finally 块 (§13.11) 中不允许使用栈分配初始化器。

注意：没有办法显式释放使用 stackalloc 分配的内存。结束注释

在函数成员执行期间创建的所有栈分配内存块在该函数成员返回时自动丢弃。

除了 stackalloc 运算符之外，C# 没有提供管理非垃圾回收内存的预定义结构。此类服务通常由支持的类库提供或直接从底层操作系统导入。

示例：

// Memory uninitialized
Span<int> span1 = stackalloc int[3];
// Memory initialized
Span<int> span2 = stackalloc int[3] { -10, -15, -30 };
// Type int is inferred
Span<int> span3 = stackalloc[] { 11, 12, 13 };
// Error; result is int*, not allowed in a safe context
var span4 = stackalloc[] { 11, 12, 13 };
// Error: no conversion from Span<int> to Span<long>
Span<long> span5 = stackalloc[] { 11, 12, 13 };
// Converts 11 and 13, and returns Span<long>
Span<long> span6 = stackalloc[] { 11, 121, 13 };
// Converts all and returns Span<long>
Span<long> span7 = stackalloc long[] { 11, 12, 13 };
// Implicit conversion of Span<T>
ReadOnlySpan<int> span8 = stackalloc int[] { 10, 22, 30 };
// Implicit conversion of Span<T>
Widget<double> span9 = stackalloc double[] { 1.2, 5.6 };

public class Widget<T>
{
    public static implicit operator Widget<T>(Span<double> sp) { return null; }
}
```

在 span8 的情况下，stackalloc 生成一个 Span<int>，它通过隐式运算符转换为 ReadOnlySpan<int>。同样，对于 span9，生成的 Span<double> 使用转换转换为用户定义的类型 Widget<double>，如所示。结束示例

## 12.8.22 Nameof 表达式

nameof_expression 用于以常量字符串形式获取程序实体的名称。

```
nameof_expression
  : 'nameof' '(' named_entity ')'
  ;

named_entity
```



```
named_entity
: named_entity_target ('.' identifier type_argument_list?)*
;

named_entity_target
: simple_name
| 'this'
| 'base'
| predefined_type
| qualified_alias_member
;
```

因为 nameof 不是关键字，nameof_expression 在语法上始终与简单名称 nameof 的调用存在歧义。出于兼容性原因，如果对名称 nameof 的名称查找 (§12.8.4) 成功，则该表达式被视为 invocation_expression —— 无论该调用是否有效。否则它就是一个 nameof_expression。

简单名称和成员访问查找在编译时对 named_entity 执行，遵循 §12.8.4 和 §12.8.7 中描述的规则。然而，当 §12.8.4 和 §12.8.7 中描述的查找因在静态上下文中找到了实例成员而导致错误时，nameof_expression 不会产生此类错误。

如果 named_entity 指定了一个方法组而具有 type_argument_list，则为编译时错误。named_entity_target 具有类型 dynamic 也是编译时错误。

nameof_expression 是类型为 string 的常量表达式，在运行时没有效果。具体而言，其 named_entity 不会被求值，并且在确定性赋值分析 (§9.4.4.22) 方面被忽略。其值是 named_entity 中在可选的最终 type_argument_list 之前的最后一个标识符，按以下方式转换：

- 如果使用，前缀 "@" 将被移除。
- 每个 unicode_escape_sequence 被转换为空对应的 Unicode 字符。
- 任何 formatting_characters 都将被移除。

这些是 §6.4.3 中在测试标识符相等性时应用的相同转换。

示例：以下说明了各种 nameof 表达式的结果，假设泛型类型 List<T> 在 System.Collections.Generic 命名空间内声明：

```
using TestAlias = System.String;

class Program
{
    static void Main()
    {
        var point = (x: 3, y: 4);

        string n1 = nameof(System);                 // "System"
        string n2 = nameof(System.Collections.Generic); // "Generic"
        string n3 = nameof(point);                  // "point"
        string n4 = nameof(point.x);                // "x"
        string n5 = nameof(Program);                // "Program"
        string n6 = nameof(System.Int32);           // "Int32"
        string n7 = nameof(TestAlias);              // "TestAlias"
        string n8 = nameof(List<int>);              // "List"
        string n9 = nameof(Program.InstanceMethod); // "InstanceMethod"
    }
}
```
```
string n10 = nameof(Program.GenericMethod);    // "GenericMethod"
string n11 = nameof(Program.NestedClass);      // "NestedClass"

// Invalid
// string x1 = nameof(List<>);                 // Empty type argument list
// string x2 = nameof(List<T>);                // T is not in scope
// string x3 = nameof(GenericMethod<>);        // Empty type argument list
// string x4 = nameof(GenericMethod<T>);       // T is not in scope
// string x5 = nameof(int);                    // Keywords not permitted
// Type arguments not permitted for method group
// string x6 = nameof(GenericMethod<Program>);
}

void InstanceMethod() { }

void GenericMethod<T>()
{
    string n1 = nameof(List<T>); // "List"
    string n2 = nameof(T);       // "T"
}

class NestedClass { }
}
```

此示例中可能令人惊讶的部分是 nameof(System.Collections.Generic) 解析为仅 “Generic” 而不是完整的命名空间，以及 nameof(TestAlias) 解析为 “TestAlias” 而不是 “String”。示例结束

## 12.8.23 匿名方法表达式

anonymous_method_expression 是定义匿名函数两种方式之一。这些内容在 §12.19 中进一步描述。

## 12.9 一元运算符

### 12.9.1 通用

+, -, !, ~, ++, --, cast 和 await 运算符被称为一元运算符。

```
unary_expression
    : primary_expression
    | '+' unary_expression
    | '-' unary_expression
    | '!' unary_expression
    | '~' unary_expression
    | pre_increment_expression
    | pre_decrement_expression
    | cast_expression
    | await_expression
    | pointer_indirection_expression   // unsafe code support
    | addressof_expression             // unsafe code support
    ;
```

pointer_indirection_expression (§23.6.2) 和 addressof_expression (§23.6.5) 仅在不安全代码 (§23) 中可用。

结果是通过从零减去 x 计算得出的。十进制取负等同于使用类型为 System.Decimal 的一元减运算符。

上述定义的未提升预定义一元减运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.9.4 逻辑否定运算符

对于形式为 !x 的操作，将应用一元运算符重载解析 (§12.4.4) 来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。只有一个预定义的逻辑否定运算符存在：

```
bool operator !(bool x);
```

该运算符计算操作数的逻辑否定：如果操作数为 true，结果为 false。如果操作数为 false，结果为 true。

上述定义的未提升预定义逻辑否定运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.9.5 按位补码运算符

对于形式为 ~x 的操作，将应用一元运算符重载解析 (§12.4.4) 来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。预定义的按位补码运算符为：

```
int operator ~(int x);
uint operator ~(uint x);
long operator ~(long x);
ulong operator ~(ulong x);
```

对于这些运算符中的每一个，操作的结果是 x 的按位补码。

每个枚举类型 E 隐式提供以下按位补码运算符：

```
E operator ~(E x);
```

计算 ~x 的结果，其中 x 是具有基础类型 U 的枚举类型 E 的表达式，与计算 (E)(~(U)x) 完全相同，只是转换到 E 总是作为在 unchecked 上下文中 (§12.8.19) 执行。

上述定义的未提升预定义按位补码运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.9.6 前缀递增和递减运算符

```
pre_increment_expression
  : '++' unary_expression
  ;

pre_decrement_expression
  : '--' unary_expression
  ;
```

前缀递增或递减操作的操作数应被分类为变量、属性访问或索引器访问的表达式。操作的结果是与操作数相同类型的数值。

如果前缀递增或递减操作的操作数是属性或索引器访问，则该属性或索引器应同时具有 get 和 set 访问器。如果不是这样，将发生绑定时错误。

将应用一元运算符重载解析 (§12.4.4) 来选择特定的运算符实现。预定义的 ++ 和 -- 运算符存在于以下类型：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 以及任何枚举类型。预定义的 ++ 运算符返回将 1 加到操作数后产生的值，预定义的 -- 运算符返回将 1 从操作数减去后产生的值。在 checked 上下文中，如果此加法或减法的结果超出结果类型的范围并且结果类型是整型或枚举类型，则会抛出 System.OverflowException。

必须存在从所选一元运算符的返回类型到 unary_expression 类型的隐式转换，否则会发生编译时错误。

形式为 ++x 或 --x 的前缀递增或递减操作的运行时处理包括以下步骤：

- 如果 x 被分类为变量：
  - x 被求值以产生变量。
  - x 的值被转换为所选运算符的操作数类型，并使用该值作为其参数调用运算符。
  - 运算符返回的值被转换为 x 的类型。所得值存储在由 x 的求值给出的位置中。
  - 并成为操作的结果。
- 如果 x 被分类为属性或索引器访问：
  - 与 x 关联的实例表达式（如果 x 不是 static）以及参数列表（如果 x 是索引器访问）被求值，其结果用于后续的 get 和 set 访问器调用。
  - x 的 get 访问器被调用。
  - get 访问器返回的值被转换为所选运算符的操作数类型，并使用该值作为其参数调用运算符。
  - 运算符返回的值被转换为 x 的类型。x 的 set 访问器使用该值作为其值参数被调用。
  - 该值也成为操作的结果。

++ 和 -- 运算符也支持后缀记法 (§12.8.15)。通常，x++ 或 x-- 的结果是操作前 x 的值，而 ++x 或 --x 的结果是操作后 x 的值。在任何情况下，操作后 x 本身的值都相同。

operator ++ 或 operator -- 实现可以使用后缀或前缀记法调用。不可能为这两种记法拥有单独的运算符实现。

上述定义的未提升预定义前缀递增和递减运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.9.7 强制转换表达式

cast_expression 用于显式地将表达式转换为给定类型。



```
    cast_expression
        : '(' type ')' unary_expression
        ;
```

*强制转换表达式* 的形式为 `(T)E`，其中 `T` 是类型，`E` 是 *一元表达式*，执行将 `E` 的值显式转换（§10.3）为类型 `T`。如果不存在从 `E` 到 `T` 的显式转换，则发生绑定期错误。否则，结果是由该显式转换产生的值。结果始终归类为值，即使 `E` 表示变量。

*强制转换表达式* 的语法会导致某些句法歧义。

*示例：表达式 `(x)-y` 既可以解释为强制转换表达式（将 `-y` 强制转换为类型 `x`），也可以解释为与括号表达式组合的加法表达式（计算值 `x - y`）。示例结束*

为解决 *强制转换表达式* 的歧义，存在以下规则：仅当以下至少一项为真时，括在括号中的一个或多个标记（§6.4）组成的序列才被视为 *强制转换表达式* 的开头：

- 该标记序列符合类型的语法，但不符合表达式的语法。
- 该标记序列符合类型的语法，并且紧跟在右括号之后的标记是标记“~”、标记“!”、标记“(”、标识符（§6.4.3）、字面量（§6.4.5），或除 `as` 和 `is` 之外的任何关键字（§6.4.4）。

上面的“正确语法”一词仅表示该标记序列应符合特定的语法产生式。它特别不考虑任何组成标识符的实际含义。

*示例：如果 `x` 和 `y` 是标识符，则 `x.y` 符合类型的语法，即使 `x.y` 实际上并不表示类型。示例结束*

*注意：根据消歧规则可知，如果 `x` 和 `y` 是标识符，则 `(x)y`、`(x)(y)` 和 `(x)(-y)` 是强制转换表达式，但 `(x)-y` 不是，即使 `x` 标识一个类型。然而，如果 `x` 是标识预定义类型（如 `int`）的关键字，则所有四种形式都是强制转换表达式（因为这样的关键字本身不可能是一个表达式）。注意结束*

## 12.9.8 await 表达式

### 12.9.8.1 概述

`await` 运算符用于挂起所在异步函数的求值，直到操作数所表示的异步操作完成。

```
    await_expression
        : 'await' unary_expression
        ;
```

*await 表达式* 只允许在异步函数（§15.15）的主体中使用。在最近的所在异步函数内，*await 表达式* 不得出现在以下位置：

- 嵌套的（非异步）匿名函数内部
- `lock_statement` 的块内部
- 到表达式树类型的匿名函数转换中（§10.7.3）
- 不安全上下文中

> *注意：await 表达式不能出现在 query_expression 中的大多数位置，因为这些位置在语法上会转换为使用非异步 lambda 表达式。注意结束*

在异步函数内部，await 不得用作 available_identifier，但可以使用逐字标识符 @await。因此，await 表达式与涉及标识符的各种表达式之间不存在句法歧义。在异步函数外部，await 充当普通标识符。

*await 表达式* 的操作数称为任务。它表示一个异步操作，该操作在计算 *await 表达式* 时可能已完成，也可能未完成。await 运算符的目的是挂起所在异步函数的执行，直到所等待的任务完成，然后获取其结果。

### 12.9.8.2 可等待表达式

*await 表达式* 的任务必须是可等待的。如果满足以下条件之一，则表达式 t 是可等待的：

- t 的编译时类型为 dynamic
- t 具有一个可访问的实例方法或扩展方法，名为 GetAwaiter，没有参数且没有类型参数，并且其返回类型 A 满足以下所有条件：
  - A 实现接口 System.Runtime.CompilerServices.INotifyCompletion（下文简称为 INotifyCompletion）
  - A 具有一个可访问、可读的实例属性 IsCompleted，其类型为 bool
  - A 具有一个可访问的实例方法 GetResult，没有参数且没有类型参数

GetAwaiter 方法的目的是获取任务的等待器。类型 A 称为 await 表达式的等待器类型。

IsCompleted 属性的目的是确定任务是否已完成。如果已完成，则无需挂起求值。

INotifyCompletion.OnCompleted 方法的目的是向任务注册一个“延续”；即，一个在任务完成时将被调用的委托（类型为 System.Action）。

GetResult 方法的目的是在任务完成后获取任务的结果。该结果可能是成功完成，可能带有结果值，也可能是由 GetResult 方法抛出的异常。

### 12.9.8.3 await 表达式的分类

### 12.9.8.4 await 表达式的运行时求值

在运行时，表达式 await t 的求值如下：

- 通过求值表达式 `(t).GetAwaiter()` 获得等待器 a。
- 通过求值表达式 `(a).IsCompleted` 获得 bool 值 b。
- 如果 b 为 false，则求值取决于 a 是否实现接口 System.Runtime.CompilerServices.ICriticalNotifyCompletion（下文简称为 ICriticalNotifyCompletion）。此检查在绑定时间进行；即，如果 a 的编译时类型为 `dynamic`，则在运行时进行，否则在编译时进行。令 `r` 表示恢复委托（§15.15）：
- 如果 `a` 未实现 `ICriticalNotifyCompletion`，则求值表达式 `((a) as INotifyCompletion).OnCompleted(r)`。
- 如果 `a` 实现 `ICriticalNotifyCompletion`，则求值表达式 `((a) as ICriticalNotifyCompletion).UnsafeOnCompleted(r)`。
- 然后挂起求值，并将控制权返回给异步函数的当前调用方。
- 在（如果 `b` 为 `true`）之后立即，或在稍后调用恢复委托时（如果 `b` 为 `false`），求值表达式 `(a).GetResult()`。如果它返回一个值，则该值是 `await_expression` 的结果。否则，结果为空。

等待器对接口方法 `INotifyCompletion.OnCompleted` 和 `ICriticalNotifyCompletion.UnsafeOnCompleted` 的实现应使委托 `r` 最多被调用一次。否则，所在异步函数的行为是未定义的。

## 12.10 算术运算符

### 12.10.1 概述

`*`、`/`、`%`、`+` 和 `-` 运算符称为算术运算符。

```
```
multiplicative_expression
    : unary_expression
    | multiplicative_expression '*' unary_expression
    | multiplicative_expression '/' unary_expression
    | multiplicative_expression '%' unary_expression
    ;

additive_expression
    : multiplicative_expression
    | additive_expression '+' multiplicative_expression
    | additive_expression '-' multiplicative_expression
    ;
```
```

如果算术运算符的操作数具有编译时类型 `dynamic`，则该表达式是动态绑定的（§12.3.3）。在这种情况下，表达式的编译时类型为 `dynamic`，下面描述的解析将在运行时使用那些具有编译时类型 `dynamic` 的操作数的运行时类型进行。

### 12.10.2 乘法运算符

对于形式为 `x * y` 的运算，应用二元运算符重载决策（§12.4.5）来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型是该运算符的返回类型。

预定义的乘法运算符如下所示。这些运算符都计算 `x` 与 `y` 的乘积。

- 整数乘法：

```
```
int operator *(int x, int y);
uint operator *(uint x, uint y);
```
```




```
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
```

在 checked 上下文中，如果乘积超出结果类型的范围，则引发 System.OverflowException。在 unchecked 上下文中，不报告溢出，并且丢弃结果类型范围之外的任何有效高阶位。

- 浮点乘法：

    ```
    float operator *(float x, float y);
    double operator *(double x, double y);
    ```

    乘积按照 IEC 60559 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是正有限值。z 是 x * y 的结果，舍入到最接近的可表示值。如果结果的幅值对目标类型而言过大，则 z 为无穷大。由于舍入，即使 x 和 y 均不为零，z 也可能为零。

    |  | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
    |---|---|---|---|---|---|---|---|
    | +x | +z | -z | +0 | -0 | +∞ | -∞ | NaN |
    | -x | -z | +z | -0 | +0 | -∞ | +∞ | NaN |
    | +0 | +0 | -0 | +0 | -0 | NaN | NaN | NaN |
    | -0 | -0 | +0 | -0 | +0 | NaN | NaN | NaN |
    | +∞ | +∞ | -∞ | NaN | NaN | +∞ | -∞ | NaN |
    | -∞ | -∞ | +∞ | NaN | NaN | -∞ | +∞ | NaN |
    | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

    （除非另有说明，在 §12.10.2–§12.10.6 的浮点表中，“+”表示该值为正；“-”表示该值为负；没有符号表示该值可能为正、为负或没有符号（NaN）。）

- decimal 乘法：

    ```
    decimal operator *(decimal x, decimal y);
    ```

    如果结果值的幅值过大，无法用 decimal 格式表示，则引发 System.OverflowException。由于舍入，即使两个操作数均不为零，结果也可能为零。在任何舍入之前，结果的小数位数是两个操作数的小数位数之和。decimal 乘法等效于使用 System.Decimal 类型的乘法运算符。

上述未提升的预定义乘法运算符的提升（§12.4.8）形式也是预定义的。

## 12.10.3 除法运算符

对于形式为 x / y 的运算，应用二元运算符重载决策（§12.4.5）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。

下面列出了预定义除法运算符。这些运算符都计算 x 和 y 的商。

- 整数除法：

    ```
    int operator /(int x, int y);
    uint operator /(uint x, uint y);
    long operator /(long x, long y);
    ulong operator /(ulong x, ulong y);
    ```

    如果右操作数的值为零，则引发 System.DivideByZeroException。

    除法将结果向零舍入。因此，结果的绝对值是小于或等于两个操作数之商的绝对值的最大可能整数。当两个操作数符号相同时，结果为零或正；当两个操作数符号相反时，结果为零或负。

    如果左操作数是最小的可表示 int 或 long 值，且右操作数为 -1，则发生溢出。在 checked 上下文中，这会导致引发 System.ArithmeticException（或其子类）。在 unchecked 上下文中，是引发 System.ArithmeticException（或其子类），还是不报告溢出且结果值为左操作数的值，由实现定义。

- 浮点除法：

    ```
    float operator /(float x, float y);
    double operator /(double x, double y);
    ```

    商按照 IEC 60559 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是正有限值。z 是 x / y 的结果，舍入到最接近的可表示值。

    | | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
    |---|---|---|---|---|---|---|---|
    | +x | +z | -z | +∞ | -∞ | +0 | -0 | NaN |
    | -x | -z | +z | -∞ | +∞ | -0 | +0 | NaN |
    | +0 | +0 | -0 | NaN | NaN | +0 | -0 | NaN |
    | -0 | -0 | +0 | NaN | NaN | -0 | +0 | NaN |
    | +∞ | +∞ | -∞ | +∞ | -∞ | NaN | NaN | NaN |
    | -∞ | -∞ | +∞ | -∞ | +∞ | NaN | NaN | NaN |
    | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- decimal 除法：

    ```
    decimal operator /(decimal x, decimal y);
    ```

    如果右操作数的值为零，则引发 System.DivideByZeroException。如果结果值的幅值过大，无法用 decimal 格式表示，则引发 System.OverflowException。由于舍入，即使第一个操作数不为零，结果也可能为零。在任何舍入之前，结果的小数位数是最接近首选小数位数、且能保留等于精确结果的结果的小数位数。首选小数位数是 x 的小数位数减去 y 的小数位数。

    decimal 除法等效于使用 System.Decimal 类型的除法运算符。

上述未提升的预定义除法运算符的提升（§12.4.8）形式也是预定义的。

## 12.10.4 余数运算符

对于形式为 x % y 的运算，应用二元运算符重载决策（§12.4.5）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。

下面列出了预定义余数运算符。这些运算符都计算 x 除以 y 的余数。

- 整数余数：

    ```
    int operator %(int x, int y);
    uint operator %(uint x, uint y);
    long operator %(long x, long y);
    ulong operator %(ulong x, ulong y);
    ```

    x % y 的结果是由 x - (x / y) * y 产生的值。如果 y 为零，则引发 System.DivideByZeroException。

    如果左操作数是最小的 int 或 long 值，且右操作数为 -1，则当且仅当 x / y 会引发异常时，才会引发 System.OverflowException。

- 浮点余数：

    ```
    float operator %(float x, float y);
    double operator %(double x, double y);
    ```

    下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是正有限值。z 是 x % y 的结果，按 x - n * y 计算，其中 n 是小于或等于 x / y 的最大可能整数。这种计算余数的方法类似于用于整数操作数的方法，但与 IEC 60559 定义不同（在该定义中，n 是最接近 x / y 的整数）。

    | | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
    |---|---|---|---|---|---|---|---|
    | +x | +z | +z | NaN | NaN | +x | +x | NaN |
    | -x | -z | -z | NaN | NaN | -x | -x | NaN |
    | +0 | +0 | +0 | NaN | NaN | +0 | +0 | NaN |
    | -0 | -0 | -0 | NaN | NaN | -0 | -0 | NaN |
    | +∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
    | -∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
    | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- decimal 余数：

    ```
    decimal operator %(decimal x, decimal y);
    ```

    如果右操作数的值为零，则引发 System.DivideByZeroException。何时引发 System.ArithmeticException（或其子类）由实现定义。对于 x % y，在 x / y 不引发异常的任何情况下，符合规范的实现都不应引发异常。在任何舍入之前，结果的小数位数是两个操作数的小数位数中的较大者；如果结果非零，则结果的符号与 x 的符号相同。

    decimal 余数等效于使用 System.Decimal 类型的余数运算符。

注意：这些规则确保对于所有类型，结果的符号永远不会与左操作数的符号相反。
结束注意

上述未提升的预定义余数运算符的提升（§12.4.8）形式也是预定义的。

## 12.10.5 加法运算符

对于形式为 x + y 的运算，应用二元运算符重载决策（§12.4.5）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。

下面列出了预定义加法运算符。对于数值类型和枚举类型，预定义加法运算符计算两个操作数的和。当一个或两个操作数的类型为 string 时，预定义加法运算符拼接操作数的字符串表示形式。

- 整数加法：

    ```
    int operator +(int x, int y);
    uint operator +(uint x, uint y);
    long operator +(long x, long y);
    ulong operator +(ulong x, ulong y);
    ```

    在 checked 上下文中，如果和超出结果类型的范围，则引发 System.OverflowException。在 unchecked 上下文中，不报告溢出，并且丢弃结果类型范围之外的任何有效高阶位。

- 浮点加法：

    ```
    float operator +(float x, float y);
    double operator +(double x, double y);
    ```

    和按照 IEC 60559 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值，z 是 x + y 的结果。如果 x 和 y 的幅值相同但符号相反，则 z 为正零。如果 x + y 过大而无法在目标类型中表示，则 z 为与 x + y 符号相同的无穷大。

    |  | y | +0 | -0 | +∞ | -∞ | NaN |
    |---|---|---|---|---|---|---|
    | x | z | x | x | +∞ | -∞ | NaN |
    | +0 | y | +0 | +0 | +∞ | -∞ | NaN |
    | -0 | y | +0 | -0 | +∞ | -∞ | NaN |
    | +∞ | +∞ | +∞ | +∞ | +∞ | NaN | NaN |
    | -∞ | -∞ | -∞ | -∞ | NaN | -∞ | NaN |
    | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- decimal 加法：

    ```
    decimal operator +(decimal x, decimal y);
    ```

    如果结果值的幅值过大，无法用 decimal 格式表示，则引发 System.OverflowException。在任何舍入之前，结果的小数位数是两个操作数的小数位数中的较大者。

    decimal 加法等效于使用 System.Decimal 类型的加法运算符。

- 枚举加法。每个枚举类型都隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：


```
E operator +(E x, U y);
E operator +(U x, E y);
```

在运行时，这些运算符的求值方式完全等同于 (E)((U)x + (U)y)。

- 字符串串联：

```
string operator +(string x, string y);
string operator +(string x, object y);
string operator +(object x, string y);
```

这些二元 + 运算符的重载执行字符串串联。如果字符串串联的操作数为 null，则替换为空字符串。否则，任何非字符串操作数都会通过调用从 object 类型继承的虚拟 ToString 方法转换为其字符串表示形式。如果 ToString 返回 null，则替换为空字符串。

示例：

```
class Test
{
    static void Main()
    {
        string s = null;
        Console.WriteLine("s = >" + s + "<");  // Displays s = ><

        int i = 1;
        Console.WriteLine("i = " + i);          // Displays i = 1

        float f = 1.230E+15F;
        Console.WriteLine("f = " + f);          // Displays f = 1.23E+15

        decimal d = 2.900m;
        Console.WriteLine("d = " + d);          // Displays d = 2.900
    }
}
```

注释中显示的输出是美国英语系统上的典型结果。精确输出可能取决于执行环境的区域设置。字符串串联运算符本身在每种情况下行为相同，但执行期间隐式调用的 ToString 方法可能会受区域设置影响。

示例结束

字符串串联运算符的结果是一个字符串，它由左操作数的字符后跟右操作数的字符组成。字符串串联运算符永远不会返回 null 值。如果没有足够的内存可用于分配结果字符串，则可能抛出 System.OutOfMemoryException。

- 委托组合。每个委托类型都隐式提供以下预定义运算符，其中 D 是委托类型：

```
D operator +(D x, D y);
```

如果第一个操作数为 null，则操作的结果是第二个操作数的值（即使该值也为 null）。否则，如果第二个操作数为 null，则操作的结果是第一个操作数的值。否则，操作的结果是一个新的委托实例，其调用列表由第一个操作数的调用列表中的元素后跟第二个操作数的调用列表中的元素组成。也就是说，结果委托的调用列表是两个操作数的调用列表的串联。

注意：有关委托组合的示例，请参见 §12.10.6 和 §20.6。由于 System.Delegate 不是委托类型，因此没有为它定义 operator +。注意结束

上面定义的未提升预定义加法运算符的提升（§12.4.8）形式也是预定义的。

## 12.10.6 减法运算符

对于 x - y 形式的操作，应用二元运算符重载解析（§12.4.5）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。

下面列出了预定义的减法运算符。这些运算符都从 x 中减去 y。

- 整数减法：
```
int operator -(int x, int y);
uint operator -(uint x, uint y);
long operator -(long x, long y);
ulong operator -(ulong x, ulong y);
```

在 checked 上下文中，如果差值超出结果类型的范围，则抛出 System.OverflowException。在 unchecked 上下文中，不报告溢出，并且结果类型范围之外的任何有效高位都被丢弃。

- 浮点减法：
```
float operator -(float x, float y);
double operator -(double x, double y);
```

差值根据 IEC 60559 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值，z 是 x - y 的结果。如果 x 和 y 相等，则 z 为正零。如果 x - y 太大而无法在目标类型中表示，则 z 为与 x - y 符号相同的无穷大。

|  | y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|
| x | z | x | x | -∞ | +∞ | NaN |
| +0 | -y | +0 | +0 | -∞ | +∞ | NaN |
| -0 | -y | -0 | +0 | -∞ | +∞ | NaN |
| +∞ | +∞ | +∞ | +∞ | NaN | +∞ | NaN |
| -∞ | -∞ | -∞ | -∞ | -∞ | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN |

（在上表中，-y 条目表示 y 的相反数，而不是表示该值为负数。）

- decimal 减法：
```
decimal operator -(decimal x, decimal y);
```

如果结果值的量值太大而无法用 decimal 格式表示，则抛出 System.OverflowException。结果的小数位数（在任何舍入之前）是两个操作数中小数位数较大者。

decimal 减法等效于使用 System.Decimal 类型的减法运算符。

- 枚举减法。每个枚举类型都隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的底层类型：

```
U operator -(E x, E y);
```

该运算符的求值方式完全等同于 (U)((U)x - (U)y)。换言之，该运算符计算 x 和 y 的序号值之间的差值，结果的类型为该枚举的底层类型。

```
E operator -(E x, U y);
```

该运算符的求值方式完全等同于 (E)((U)x - y)。换言之，该运算符从枚举的底层类型中减去一个值，得到该枚举的一个值。

- 委托移除。每个委托类型都隐式提供以下预定义运算符，其中 D 是委托类型：

```
D operator -(D x, D y);
```

语义如下：

- 如果第一个操作数为 null，则操作的结果为 null。
- 否则，如果第二个操作数为 null，则操作的结果是第一个操作数的值。
- 否则，两个操作数都表示非空调用列表（§20.2）。
  - 如果这些列表比较相等（由委托相等运算符（§12.12.9）确定），则操作的结果为 null。
  - 否则，如果第二个操作数的列表是第一个操作数列表的子列表，则操作的结果是一个新的调用列表，它由第一个操作数的列表移除第二个操作数的条目后组成。（为确定子列表相等性，对应条目的比较方式与委托相等运算符相同。）如果第二个操作数的列表匹配第一个操作数列表中多个连续条目的子列表，则移除最后一个匹配的连续条目子列表。
  - 否则，操作的结果是左操作数的值。

在此过程中，两个操作数的列表（如果有）都不会改变。

*示例：*

```
delegate void D(int x);

class C
{
    public static void M1(int i) { ... }
    public static void M2(int i) { ... }
}

class Test
{
    static void Main()
    {
        D cd1 = new D(C.M1);
        D cd2 = new D(C.M2);
```
```
D list = null;

list = null - cd1; // null
list = (cd1 + cd2 + cd2 + cd1) - null; // M1 + M2 + M2 + M1
list = (cd1 + cd2 + cd2 + cd1) - cd1; // M1 + M2 + M2
list = (cd1 + cd2 + cd2 + cd1) - (cd1 + cd2); // M2 + M1
list = (cd1 + cd2 + cd2 + cd1) - (cd2 + cd2); // M1 + M1
list = (cd1 + cd2 + cd2 + cd1) - (cd2 + cd1); // M1 + M2
list = (cd1 + cd2 + cd2 + cd1) - (cd1 + cd1); // M1 + M2 + M2 + M1
list = (cd1 + cd2 + cd2 + cd1) - (cd1 + cd2 + cd2 + cd1); // null
}
}
```

*示例结束*

上面定义的未提升预定义减法运算符的提升（§12.4.8）形式也是预定义的。

## 12.11 移位运算符

<< 和 >> 运算符用于执行位移操作。

```
shift_expression
  : additive_expression
  | shift_expression '<<' additive_expression
  | shift_expression right_shift additive_expression
  ;
```

如果 shift_expression 的操作数具有编译时类型 dynamic，则该表达式进行动态绑定（§12.3.3）。在这种情况下，表达式的编译时类型为 dynamic，下面描述的解析将在运行时使用那些具有编译时类型 dynamic 的操作数的运行时类型来进行。

对于 x << count 或 x >> count 形式的操作，应用二元运算符重载解析（§12.4.5）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。

声明重载移位运算符时，第一个操作数的类型必须始终是包含该运算符声明的类或结构体，第二个操作数的类型必须始终是 int。

下面列出了预定义的移位运算符。

- 左移：
```
int operator <<(int x, int count);
uint operator <<(uint x, int count);
long operator <<(long x, int count);
ulong operator <<(ulong x, int count);
```
<< 运算符按如下所述计算出的位数对 x 进行移位。
x 的结果类型范围之外的高位被丢弃，剩余位左移，低序空位被设为零。

- 右移：
```
int operator >>(int x, int count);
uint operator >>(uint x, int count);
long operator >>(long x, int count);
ulong operator >>(ulong x, int count);
```




> *注意：* 对 `is` 运算符的右操作数的查找必须首先作为类型进行测试，然后作为可能跨多个标记的表达式。在操作数为表达式的情况下，模式表达式的优先级必须至少与 `shift_expression` 一样高。结束注释

The `is` 运算符在 §12.12.12 中描述，`as` 运算符在 §12.12.13 中描述。

`==`、`!=`、`<`、`>`、`<=` 和 `>=` 运算符是比较运算符。

如果 `default_literal` (§8.20) 用作 `<`、`>`、`<=` 或 `>=` 运算符的操作数，则会发生编译时错误。如果 `default_literal` 用作 `==` 或 `!=` 运算符的两个操作数，则会发生编译时错误。如果 `default_literal` 用作 `is` 或 `as` 运算符的左操作数，则会发生编译时错误。

如果比较运算符的操作数具有编译时类型 `dynamic`，则该表达式是动态绑定的 (§12.3.3)。在这种情况下，表达式的编译时类型为 `dynamic`，下面描述的解析将在运行时使用具有编译时类型 `dynamic` 的那些操作数的运行时类型进行。

对于形式为 `x «op» y` 的操作，其中 «op» 是比较运算符，将应用重载解析 (§12.4.5) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。如果 `equality_expression` 的两个操作数都是 `null` 字面量，则不执行重载解析，并且表达式根据运算符是 `==` 还是 `!=` 求值为 `true` 或 `false` 的常量值。

预定义的比较运算符在以下小节中描述。所有预定义的比较运算符都返回 `bool` 类型的结果，如下表所述。

| 操作 | 结果 |
| --- | --- |
| x == y | 若 x 等于 y 则为 true，否则为 false |
| x != y | 若 x 不等于 y 则为 true，否则为 false |
| x < y | 若 x 小于 y 则为 true，否则为 false |
| x > y | 若 x 大于 y 则为 true，否则为 false |
| x <= y | 若 x 小于或等于 y 则为 true，否则为 false |
| x >= y | 若 x 大于或等于 y 则为 true，否则为 false |

### 12.12.2 整数比较运算符

预定义的整数比较运算符为：

```csharp
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

这些运算符中的每一个都比较两个整数操作数的数值，并返回一个 `bool` 值，指示特定关系是否为真或假。

上述未提升的预定义整数比较运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.12.3 浮点比较运算符

预定义的浮点比较运算符为：

```csharp
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

运算符根据 IEC 60559 标准规则比较操作数：

如果任一操作数为 NaN，则除 `!=` 外所有运算符的结果均为 false，而 `!=` 的结果为 true。对于任意两个操作数，`x != y` 始终产生与 `!(x == y)` 相同的结果。然而，当一个或两个操作数为 NaN 时，`<`、`>`、`<=` 和 `>=` 运算符不会产生与相反运算符的逻辑否定相同的结果。

示例：如果 `x` 和 `y` 中任一为 NaN，则 `x < y` 为 false，但 `!(x >= y)` 为 true。结束示例

当两个操作数都不是 NaN 时，运算符根据以下顺序比较两个浮点操作数的值

```
-∞ < -max < ... < -min < -0.0 == +0.0 < +min < ... < +max < +∞
```

其中 `min` 和 `max` 是在给定浮点格式中可以表示的最小和最大正有限值。此顺序的显著影响包括：

- 负零和正零被视为相等。
- 负无穷被视为小于所有其他值，但等于另一个负无穷。
- 正无穷被视为大于所有其他值，但等于另一个正无穷。

上述未提升的预定义浮点比较运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.12.4 十进制比较运算符

预定义的十进制比较运算符为：

```csharp
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

这些运算符中的每一个都比较两个十进制操作数的数值，并返回一个 `bool` 值，指示特定关系是否为 `true` 或 `false`。每个十进制比较等价于使用类型为 `System.Decimal` 的相应关系或相等运算符。

上述未提升的预定义十进制比较运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.12.5 布尔相等运算符

预定义的布尔相等运算符为：

```csharp
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

`==` 的结果为 `true`，如果 `x` 和 `y` 均为 `true`，或 `x` 和 `y` 均为 `false`。否则，结果为 `false`。

`!=` 的结果为 `false`，如果 `x` 和 `y` 均为 `true`，或 `x` 和 `y` 均为 `false`。否则，结果为 `true`。当操作数为 `bool` 类型时，`!=` 运算符产生与 `^` 运算符相同的结果。

上述未提升的预定义布尔相等运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.12.6 枚举比较运算符

每个枚举类型隐式提供以下预定义比较运算符：

```csharp
bool operator ==(E x, E y);
bool operator !=(E x, E y);

bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

计算 `x «op» y` 的结果，其中 `x` 和 `y` 是具有基础类型 `U` 的枚举类型 `E` 的表达式，且 «op» 是比较运算符之一，其结果与计算完全相同

结束注释

示例：以下示例检查无约束类型参数类型的参数是否为 null。

```csharp
class C<T>
{
    void F(T x)
    {
        if (x == null)
        {
            throw new ArgumentNullException();
        }
        ...
    }
}
```

`x == null` 构造是允许的，即使 `T` 可能表示非可空值类型，并且当 `T` 为非可空值类型时，结果简单地定义为 false。

结束示例

对于形式为 `x == y` 或 `x != y` 的操作，如果存在任何适用的 `operator ==` 或 `operator !=`，则运算符重载解析 (§12.4.5) 规则将选择该运算符而不是预定义的引用类型相等运算符。

> 注意：通过显式地将两个操作数都强制转换为类型 `object`，始终可以选定预定义的引用类型相等运算符。结束注释

示例：示例

```csharp
class Test
{
    static void Main()
    {
        string s = "Test";
        string t = string.Copy(s);
        Console.WriteLine(s == t);
        Console.WriteLine((object)s == t);
        Console.WriteLine(s == (object)t);
        Console.WriteLine((object)s == (object)t);
    }
}
```

生成输出

```
True
False
False
False
```

`s` 和 `t` 变量引用包含相同字符的两个不同的字符串实例。第一个比较输出 `True`，因为当两个操作数均为 `string` 类型时，选择了预定义的字符串相等运算符 (§12.12.8)。其余比较均输出 `False`，因为当任一操作数的绑定时类型为 `object` 时，`string` 类型中的 `operator ==` 重载不适用。

请注意，上述技术对于值类型没有意义。示例

```
class Test
{
    static void Main()
    {
        int i = 123;
        int j = 123;
        Console.WriteLine((object)i == (object)j);
    }
}
```

输出为 False，因为这些强制转换创建了指向两个单独的装箱 int 值实例的引用。

*示例结束*

## 12.12.8 字符串相等运算符

预定义的字符串相等运算符为：

```
bool operator ==(string x, string y);
bool operator !=(string x, string y);
```

两个字符串值在以下任一条件为真时被视为相等：

- 两个值均为 null。
- 两个值均为非 null 的对字符串实例的引用，且长度相同且每个字符位置的字符均相同。

字符串相等运算符比较的是字符串值而不是字符串引用。当两个独立的字符串实例包含完全相同的字符序列时，字符串的值相等，但引用不同。

> 注：如 §12.12.7 中所述，引用类型相等运算符可用于比较字符串引用而不是字符串值。结束注记

## 12.12.9 委托相等运算符

预定义的委托相等运算符为：

```
bool operator ==(System.Delegate x, System.Delegate y);
bool operator !=(System.Delegate x, System.Delegate y);
```

两个委托实例按如下方式视为相等：

- 如果任一委托实例为 null，则它们相等当且仅当两者均为 null。
- 如果委托的运行时类型不同，则它们永远不相等。
- 如果两个委托实例都有调用列表（§20.2），则这些实例相等当且仅当它们的调用列表长度相同，并且一个调用列表中的每个条目（按如下定义相等）与另一个调用列表中按顺序对应的条目相等。

以下规则规定了调用列表条目的相等性：

- 如果两个调用列表条目都引用同一个静态方法，则这些条目相等。
- 如果两个调用列表条目都引用同一个目标对象上的同一个非静态方法（按引用相等运算符定义），则这些条目相等。
- 由语义相同的匿名函数（§12.19）的求值产生的调用列表条目，如果捕获的外层变量实例集合相同（可能为空），则允许（但不要求）相等。

如果运算符重载解析解析为任一委托相等运算符，并且两个操作数的绑定时类型是 §20 中所述的委托类型而不是 System.Delegate，并且绑定类型操作数类型之间没有恒等转换，则会发生绑定时错误。

> *注：* 此规则可防止由于引用不同类型的委托实例而永远无法将非 null 值视为相等的比较。*结束注记*

## 12.12.10 可空值类型与 null 字面量之间的相等运算符

== 和 != 运算符允许一个操作数为可空值类型的值，另一个为 null 字面量，即使不存在用于该操作的预定义或用户定义运算符（以非提升或提升形式）。

对于以下形式之一的操作

```
x == null
null == x
x != null
null != x
```

其中 x 是可空值类型的表达式，如果运算符重载解析（§12.4.5）找不到适用的运算符，则结果改为从 x 的 HasValue 属性计算得出。具体而言，前两种形式被转换为 !x.HasValue，后两种形式被转换为 x.HasValue。

## 12.12.11 元组相等运算符

元组相等运算符按词法顺序成对应用于元组操作数的元素。

如果 == 或 != 运算符的每个操作数 x 和 y 被分类为元组或具有元组类型（§8.3.11）的值，则该运算符是元组相等运算符。

如果操作数 e 被分类为元组，则元素 e1...en 应当是求值元组表达式的元素表达式的结果。否则如果 e 是元组类型的值，则元素应当为 t.Item1...t.Itemn，其中 t 是求值 e 的结果。

元组相等运算符的操作数 x 和 y 必须具有相同的元数，否则会发生编译时错误。对于每个元素对 xi 和 yi，必须应用相同的相等运算符，并且必须产生类型为 bool、dynamic、具有隐式转换为 bool 的类型，或定义 true 和 false 运算符的类型的结果。

元组相等运算符 x == y 的求值如下：

- 左侧操作数 x 被求值。
- 右侧操作数 y 被求值。
- 按词法顺序对每个元素对 xi 和 yi：
  - 运算符 xi == yi 被求值，并以以下方式获得类型为 bool 的结果：
    - 如果比较产生 bool，则该结果即为结果。
    - 否则如果比较产生 dynamic，则在其上动态调用运算符 false，并用 ! 运算符对 resulting bool 值取反。
    - 否则，如果比较的类型具有隐式转换为 bool，则应用该转换。
- 否则，如果比较的类型具有运算符 `false`，则调用该运算符，并用 `!` 运算符对 resulting `bool` 值取反。
  - 如果 resulting `bool` 为 `false`，则不再进行进一步求值，元组相等运算符的结果为 `false`。
- 如果所有元素比较均产生 `true`，则元组相等运算符的结果为 `true`。

元组相等运算符 `x != y` 的求值如下：

- 左侧操作数 `x` 被求值。
- 右侧操作数 `y` 被求值。
- 按词法顺序对每个元素对 `x1` 和 `y1`：
  - 运算符 `x1 != y1` 被求值，并以以下方式获得类型为 `bool` 的结果：
    - 如果比较产生 `bool`，则该结果即为结果。
    - 否则如果比较产生 `dynamic`，则在其上动态调用运算符 `true`，并且 resulting `bool` 值即为结果。
    - 否则，如果比较的类型具有隐式转换为 `bool`，则应用该转换。
    - 否则，如果比较的类型具有运算符 `true`，则调用该运算符，并且 resulting `bool` 值即为结果。
  - 如果 resulting `bool` 为 `true`，则不再进行进一步求值，元组相等运算符的结果为 `true`。
- 如果所有元素比较均产生 `false`，则元组相等运算符的结果为 `false`。

## 12.12.12 is 运算符

`is` 运算符有两种形式。一种是 *is-type 运算符*，其右侧为类型。另一种是 *is-pattern 运算符*，其右侧为模式。

### 12.12.12.1 is-type 运算符

*is-type 运算符* 用于检查对象的运行时类型是否与给定类型兼容。该检查在运行时执行。操作 `E is T` 的结果，其中 `E` 是表达式且 `T` 是除 `dynamic` 之外的类型，是一个布尔值，表示 `E` 是否为非 null 并且可以通过引用转换、装箱转换、拆箱转换、包装转换或解包转换成功转换为类型 `T`。

该操作的求值如下：

+ 1. 如果 `E` 是匿名函数或方法组，则会发生编译时错误
+ 2. 如果 `E` 是 `null` 字面量，或 `E` 的值为 `null`，则结果为 `false`。
+ 3. 否则：
+ 4. 设 `R` 为 `E` 的运行时类型。
+ 5. 按如下方式从 `R` 派生 `D`：
+ 6. 如果 `R` 是可空值类型，则 `D` 为 `R` 的基础类型。
+ 7. 否则，`D` 为 `R`。

8. 结果取决于 D 和 T 如下：

9. 如果 T 是引用类型，则在以下情况下结果为 true：

- D 和 T 是同一类型，
- D 是引用类型并且存在从 D 到 T 的隐式引用转换，或
- 要么：D 是值类型并且存在从 D 到 T 的装箱转换。要么：D 是值类型并且 T 是由 D 实现的接口类型。

10. 如果 T 是可空值类型，则当 D 为 T 的基础类型时结果为 true。

11. 如果 T 是非可空值类型，则当 D 和 T 为同一类型时结果为 true。

12. 否则，结果为 false。

用户定义的转换不被 is 运算符考虑。

注：由于 is 运算符在运行时求值，所有类型参数已被替换，且没有需要考虑的开放类型（§8.4.3）。结束注记

注：is 运算符可按如下方式理解为编译时类型和转换，其中 C 为 E 的编译时类型：

- 如果 e 的编译时类型与 T 相同，或从 E 的编译时类型到 T 存在隐式引用转换（§10.2.8）、装箱转换（§10.2.9）、包装转换（§10.6）或显式解包转换（§10.6）：
  - 如果 C 为非可空值类型，则操作结果为 true。
  - 否则，操作结果等价于求值 E != null。
- 否则，如果从 C 到 T 存在显式引用转换（§10.3.5）或拆箱转换（§10.3.7），或 C 或 T 为开放类型（§8.4.3），则必须执行如上所述的运行时检查。
- 否则，E 到类型 T 不可能进行引用、装箱、包装或解包转换，并且操作结果为 false。编译器可基于编译时类型实现优化。

结束注记

### 12.12.12 is-pattern 运算符

is-pattern 运算符用于检查表达式计算的值是否匹配给定模式（§11）。该检查在运行时执行。如果值匹配模式，则 is-pattern 运算符的结果为 true；否则为 false。

对于形式为 E is P 的表达式，其中 E 是类型为 T 的关系表达式且 P 是模式，如果满足以下任一条件则为编译时错误：

- E 未指定值或没有类型。
- 模式 P 对类型 T 不适用（§11.2）。

## 12.12.13 as 运算符

as 运算符用于将值显式转换为给定的引用类型或可空值类型。与强制转换表达式（§12.9.7）不同，as 运算符永远不会抛出异常。相反，如果指示的转换不可行，则结果值为 null。



形式为 E as T 的运算中，E 应为表达式，T 应为引用类型、已知为引用类型的类型参数或可空值类型。此外，下列条件中至少有一项必须为真，否则将发生编译时错误：

- 存在从 E 到 T 的标识转换（§10.2.2）、隐式可空转换（§10.2.6）、隐式引用转换（§10.2.8）、装箱转换（§10.2.9）、显式可空转换（§10.3.4）、显式引用转换（§10.3.5）或包装转换（§8.3.12）。
- E 或 T 的类型是开放类型。
- E 是 null 字面量。

如果 E 的编译时类型不是 `dynamic`，则运算 E as T 产生的结果与以下表达式相同：

```
E is T ? (T)(E) : (T)null
```

不同之处在于 E 只计算一次。可以预期，编译器会将 E as T 优化为最多执行一次运行时类型检查，而不是上述展开所暗示的两次运行时类型检查。

如果 E 的编译时类型是 `dynamic`，则与强制转换运算符不同，as 运算符不是动态绑定的（§12.3.3）。因此，这种情况下的展开为：

```
E is T ? (T)(object)(E) : (T)null
```

注意，某些转换（例如用户定义转换）不能使用 as 运算符执行，而应改用强制转换表达式执行。

示例：在以下示例中

```
class X
{
    public string F(object o)
    {
        return o as string; // OK, string is a reference type
    }

    public T G<T>(object o)
        where T : Attribute
    {
        return o as T;      // Ok, T has a class constraint
    }

    public U H<U>(object o)
    {
        return o as U;      // Error, U is unconstrained
    }
}
```

G 的类型参数 T 已知为引用类型，因为它具有类约束。但 H 的类型参数 U 并非如此；因此，H 中使用 as 运算符是不允许的。

示例结束

## 12.13 逻辑运算符

### 12.13.1 概述

`&`、`^` 和 `|` 运算符称为逻辑运算符。

```
and_expression
    : equality_expression
    | and_expression '&' equality_expression
    ;

exclusive_or_expression
    : and_expression
    | exclusive_or_expression '^' and_expression
    ;

inclusive_or_expression
    : exclusive_or_expression
    | inclusive_or_expression '|' exclusive_or_expression
    ;
```

如果逻辑运算符的操作数具有编译时类型 `dynamic`，则该表达式是动态绑定的（§12.3.3）。在这种情况下，表达式的编译时类型为 `dynamic`，并且下面描述的重载解析将在运行时使用那些具有编译时类型 `dynamic` 的操作数的运行时类型来进行。

对于形式为 `x «op» y` 的运算，其中 `«op»` 是逻辑运算符之一，应用重载解析（§12.4.5）来选择特定的运算符实现。操作数将转换为所选运算符的参数类型，结果的类型是该运算符的返回类型。

以下子条款描述预定义逻辑运算符。

### 12.13.2 整数逻辑运算符

预定义的整数逻辑运算符为：

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

`&` 运算符计算两个操作数的按位逻辑与，`|` 运算符计算两个操作数的按位逻辑或，`^` 运算符计算两个操作数的按位逻辑异或。这些运算不会发生溢出。

上文定义的非提升预定义整数逻辑运算符的提升形式（§12.4.8）也是预定义的。

### 12.13.3 枚举逻辑运算符

每个枚举类型 `E` 都隐式提供以下预定义逻辑运算符：

```
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```

计算 x «op» y 的结果（其中 x 和 y 是枚举类型 E 的表达式，E 的基础类型为 U，且 «op» 是逻辑运算符之一）与计算 (E)((U)x «op» (U)y) 的结果完全相同。换言之，枚举类型逻辑运算符只是对两个操作数的基础类型执行逻辑运算。

上文定义的非提升预定义枚举逻辑运算符的提升形式（§12.4.8）也是预定义的。

### 12.13.4 布尔逻辑运算符

预定义的布尔逻辑运算符为：

```
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```

如果 x 和 y 都为 true，则 x & y 的结果为 true；否则结果为 false。

如果 x 或 y 为 true，则 x | y 的结果为 true；否则结果为 false。

如果 x 为 true 且 y 为 false，或者 x 为 false 且 y 为 true，则 x ^ y 的结果为 true；否则结果为 false。当操作数的类型为 bool 时，^ 运算符计算的结果与 != 运算符相同。

### 12.13.5 可空布尔类型与 &、| 运算符

可空布尔类型 bool? 可以表示三个值：true、false 和 null。

与其他二元运算符一样，逻辑运算符 & 和 | 的提升形式（§12.13.4）也是预定义的：

```
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

提升的 & 和 | 运算符的语义由下表定义：

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

*注意：bool? 类型在概念上类似于 SQL 中用于布尔表达式的三值类型。上表遵循与 SQL 相同的语义，而将 §12.4.8 的规则应用于 & 和 | 运算符则不会如此。§12.4.8 的规则已经为提升的 ^ 运算符提供了类似 SQL 的语义。注释结束*

## 12.14 条件逻辑运算符

### 12.14.1 概述

`&&` 和 `||` 运算符称为条件逻辑运算符。它们也称为“短路”逻辑运算符。

```
conditional_and_expression
    : inclusive_or_expression
    | conditional_and_expression '&&' inclusive_or_expression
    ;

conditional_or_expression
    : conditional_and_expression
    | conditional_or_expression '||' conditional_and_expression
    ;
```

`&&` 和 `||` 运算符是 `&` 和 `|` 运算符的条件版本：

- 运算 `x && y` 对应于运算 `x & y`，不同之处在于仅当 `x` 不为 `false` 时才计算 `y`。
- 运算 `x || y` 对应于运算 `x | y`，不同之处在于仅当 `x` 不为 `true` 时才计算 `y`。

*注意：短路使用“非 true”和“非 false”条件的原因，是为了让用户定义的条件运算符能够定义何时适用短路。用户定义类型可能处于这样一种状态：operator true 返回 false，而 operator false 返回 false。在这些情况下，&& 和 || 都不会短路。注释结束*

如果条件逻辑运算符的操作数具有编译时类型 `dynamic`，则该表达式是动态绑定的（§12.3.3）。在这种情况下，表达式的编译时类型为 `dynamic`，并且下面描述的重载解析将在运行时使用那些具有编译时类型 `dynamic` 的操作数的运行时类型来进行。

形式为 `x && y` 或 `x || y` 的运算按如下方式处理：像该运算写成 `x & y` 或 `x | y` 那样应用重载解析（§12.4.5）。然后，

- 如果重载解析未能找到唯一的最佳运算符，或者如果重载解析选择了某个预定义整数逻辑运算符或可空布尔逻辑运算符（§12.13.5），则发生绑定期错误。
- 否则，如果所选运算符是某个预定义布尔逻辑运算符（§12.13.4），则按 §12.14.2 中所述处理该运算。
- 否则，所选运算符是用户定义运算符，并按 §12.14.3 中所述处理该运算。

不能直接重载条件逻辑运算符。不过，由于条件逻辑运算符是依据常规逻辑运算符求值的，因此在某些限制下，常规逻辑运算符的重载也被视为条件逻辑运算符的重载。§12.14.3 对此做了进一步描述。




### 12.14.2 布尔条件逻辑运算符

当 && 或 || 的操作数为 bool 类型，或者当操作数所属类型未定义适用的 operator & 或 operator |，但定义了到 bool 的隐式转换时，该操作按如下方式处理：

- 操作 x && y 按 x ? y : false 求值。换言之，先对 x 求值并将其转换为 bool 类型。然后，如果 x 为 true，则对 y 求值并将其转换为 bool 类型，该值成为运算结果。否则，运算结果为 false。
- 操作 x || y 按 x ? true : y 求值。换言之，先对 x 求值并将其转换为 bool 类型。然后，如果 x 为 true，则运算结果为 true。否则，对 y 求值并将其转换为 bool 类型，该值成为运算结果。

### 12.14.3 用户定义的条件逻辑运算符

当 && 或 || 的操作数所属类型声明了适用的用户定义 operator & 或 operator | 时，以下两项均须为 true，其中 T 是所选运算符声明所在的类型：

- 所选运算符的返回类型及其每个参数的类型均应为 T。换言之，该运算符应计算两个 T 类型操作数的逻辑 AND 或逻辑 OR，并返回 T 类型的结果。
- T 应包含 operator true 和 operator false 的声明。

如果上述任一要求未满足，则发生绑定时间错误。否则，&& 或 || 运算通过将用户定义的 operator true 或 operator false 与所选用户定义运算符组合来进行求值：

- 操作 x && y 按 T.false(x) ? x : T.&(x, y) 求值，其中 T.false(x) 是对 T 中声明的 operator false 的调用，T.&(x, y) 是对所选 operator & 的调用。换言之，先对 x 求值，并对结果调用 operator false，以确定 x 是否确定为 false。然后，如果 x 确定为 false，则运算结果为先前为 x 计算的值。否则，对 y 求值，并对先前为 x 计算的值和 y 计算的值调用所选 operator &，以产生运算结果。
- 操作 x || y 按 T.true(x) ? x : T.|(x, y) 求值，其中 T.true(x) 是对 T 中声明的 operator true 的调用，T.|(x, y) 是对所选 operator | 的调用。换言之，先对 x 求值，并对结果调用 operator true，以确定 x 是否确定为 true。然后，如果 x 确定为 true，则运算结果为先前为 x 计算的值。否则，对 y 求值，并对先前为 x 计算的值和 y 计算的值调用所选 operator |，以产生运算结果。

在这两种运算中，由 x 给出的表达式只求值一次，而由 y 给出的表达式要么不求值，要么恰好求值一次。

## 12.15 空值合并运算符

?? 运算符称为空值合并运算符。

```
null_coalescing_expression
    : conditional_or_expression
conditional_or_expression '??' null_coalescing_expression
throw_expression
;
```

在形式为 a ?? b 的空值合并表达式中，如果 a 非 null，则结果为 a；否则结果为 b。仅当 a 为 null 时，该运算才会对 b 求值。

空值合并运算符是右结合的，这意味着运算从右到左分组。

*示例：形式为 a ?? b ?? c 的表达式按 a ?? (b ?? c) 求值。一般来说，形式为 E1 ?? E2 ?? ... ?? EN 的表达式返回第一个非 null 的操作数；如果所有操作数均为 null，则返回 null。示例结束*

表达式 a ?? b 的类型取决于操作数上可用的隐式转换。按优先顺序，a ?? b 的类型为 A0、A 或 B，其中 A 是 a 的类型（前提是 a 有类型），B 是 b 的类型（前提是 b 有类型），并且如果 A 是可空值类型，则 A0 是 A 的基础类型；否则 A0 为 A。具体而言，a ?? b 按如下方式处理：

- 如果 A 存在且不是可空值类型或引用类型，则发生编译时错误。
- 否则，如果 A 存在且 b 是动态表达式，则结果类型为 dynamic。在运行时，首先对 a 求值。如果 a 非 null，则将 a 转换为 dynamic，并以此作为结果。否则，对 b 求值，并以此作为结果。
- 否则，如果 A 存在且为可空值类型，并且存在从 b 到 A0 的隐式转换，则结果类型为 A0。在运行时，首先对 a 求值。如果 a 非 null，则将 a 解包为 A0 类型，并以此作为结果。否则，对 b 求值并将其转换为 A0 类型，并以此作为结果。
- 否则，如果 A 存在，并且存在从 b 到 A 的隐式转换，则结果类型为 A。在运行时，首先对 a 求值。如果 a 非 null，则 a 成为结果。否则，对 b 求值并将其转换为 A 类型，并以此作为结果。
- 否则，如果 A 存在且为可空值类型，b 具有类型 B，并且存在从 A0 到 B 的隐式转换，则结果类型为 B。在运行时，首先对 a 求值。如果 a 非 null，则将 a 解包为 A0 类型并转换为 B 类型，并以此作为结果。否则，对 b 求值，并以此作为结果。
- 否则，如果 b 具有类型 B，并且存在从 a 到 B 的隐式转换，则结果类型为 B。在运行时，首先对 a 求值。如果 a 非 null，则将 a 转换为 B 类型，并以此作为结果。否则，对 b 求值，并以此作为结果。

否则，a 和 b 不兼容，并发生编译时错误。

## 12.16 throw 表达式运算符

```
throw_expression
    : 'throw' null_coalescing_expression
    ;
```

*throw_expression* 抛出对 *null_coalescing_expression* 求值所产生的值。该表达式应可隐式转换为 System.Exception，并且在抛出之前，表达式的求值结果会转换为 System.Exception。*throw_expression* 求值在运行时的行为与 *throw statement* 的规定相同（§13.10.6）。

*throw_expression 没有类型。throw_expression 可通过隐式 throw 转换转换为所有类型。*

*throw 表达式*只能出现在以下语法上下文中：

- 作为三元条件运算符（?:）的第二个或第三个操作数。
- 作为空值合并运算符（??）的第二个操作数。
- 作为表达式主体 lambda 或表达式主体成员的主体。

## 12.17 声明表达式

声明表达式声明局部变量。

```
declaration_expression
    : local_variable_type identifier
    ;

local_variable_type
    : type
    | 'var'
    ;
```

如果简单名称查找未找到关联声明（§12.8.4），则 *simple_name* `_` 也被视为声明表达式。当用作声明表达式时，`_` 称为*简单弃元*。它在语义上等价于 `var _`，但允许出现在更多位置。

声明表达式只能出现在以下语法上下文中：

- 作为 *argument_list* 中的 out *argument_value*。
- 作为构成简单赋值左侧的简单弃元 `_`（§12.21.2）。
- 作为一个或多个递归嵌套的 *tuple_expressions* 中的 *tuple_element*，其中最外层构成解构赋值的左侧。即使声明表达式在语法上并不存在，*deconstruction_expression* 也会在此位置产生声明表达式。

*注意：* 这意味着声明表达式不能加括号。*注意结束*

使用 *declaration_expression* 声明的隐式类型化变量在其声明所在的 *argument_list* 中被引用是错误的。

使用 *declaration_expression* 声明的变量在其所在的解构赋值中被引用是错误的。

如果声明表达式是简单弃元，或者其 *local_variable_type* 是标识符 `var`，则该声明表达式归类为*隐式类型化*变量。该表达式没有类型，并且局部变量的类型根据语法上下文推断如下：

- 在 *argument_list* 中，变量的推断类型是对应参数的声明类型。
- 作为简单赋值的左侧时，变量的推断类型是该赋值右侧的类型。
- 在简单赋值左侧的 *tuple_expression* 中，变量的推断类型是该赋值右侧（解构后）对应元组元素的类型。

否则，声明表达式归类为*显式类型化*变量，并且表达式以及所声明变量的类型应为 *local_variable_type* 给定的类型。




使用标识符 _ 的声明表达式是一个丢弃（§9.2.9.1），并且不会为变量引入名称。使用除 _ 之外的标识符的声明表达式会将该名称引入最近的外层局部变量声明空间（§7.3）。

*示例：*

```csharp
string M(out int i, string s, out bool b) { ... }

var s1 = M(out int i1, "One", out var b1);
Console.WriteLine($"{i1}, {b1}, {s1}");
// Error: i2 referenced within declaring argument list
var s2 = M(out var i2, M(out i2, "Two", out bool b2), out b2);
var s3 = M(out int _, "Three", out var _);
```

s1 的声明同时展示了显式类型和隐式类型的声明表达式。b1 的推断类型为 bool，因为那是 M 中对应 out 参数的类型。随后的 WriteLine 能够访问 i1 和 b1，因为它们已被引入到外层作用域。

s2 的声明展示了在嵌套调用 M 中尝试使用 i2，这是不允许的，因为引用发生在 i2 被声明的参数列表内。另一方面，对最终参数中 b2 的引用是允许的，因为它发生在 b2 被声明的嵌套参数列表结束之后。

s3 的声明展示了既有隐式类型又有显式类型的丢弃声明表达式。因为丢弃不会声明命名变量，所以标识符 _ 的多次出现是允许的。

```csharp
(int i1, int _, (var i2, var _), _) = (1, 2, (3, 4), 5);
```

此示例展示了在解构赋值中对变量和丢弃同时使用隐式类型和显式类型的声明表达式。当找不到 _ 的声明时，simple_name _ 等同于 var _。

```csharp
void M1(out int i) { ... }

void M2(string _)
{
    M1(out _);      // Error: `_` is a string
    M1(out var _);
}
```

此示例展示了使用 var _ 来提供隐式类型的丢弃，当 _ 不可用时，因为它指定了外层作用域中的变量。

*结束示例*

## 12.18 条件运算符

?: 运算符称为条件运算符。有时也称为三元运算符。

```
conditional_expression
    : null_coalescing_expression
    | null_coalescing_expression '?' expression ':' expression
    | null_coalescing_expression '?' 'ref' variable_reference ':'
      'ref' variable_reference
    ;
```

如果存在 ref，则在条件运算符中不允许使用 throw 表达式（§12.16）。

形式为 b ? x : y 的条件表达式首先计算条件 b。然后，如果 b 为 true，则计算 x 并成为操作的结果。否则，计算 y 并成为操作的结果。条件表达式永远不会同时计算 x 和 y。

条件运算符是右结合的，这意味着操作是从右到左分组的。

示例：形式为 a ? b : c ? d : e 的表达式被求值为 a ? b : (c ? d : e)。结束示例

?: 运算符的第一个操作数应为可隐式转换为 bool 的表达式，或实现 operator true 的类型的表达式。如果不满足其中任何一个要求，将发生编译时错误。

如果存在 ref：
- 两个 variable_references 类型之间必须存在恒等转换，并且结果的类型可以是任一类型。如果任一类型为 dynamic，则类型推断优先选择 dynamic（§8.7）。如果任一类型为元组类型（§8.3.11），则当两个元组中相同序数位置的元素名称匹配时，类型推断会包含元素名称。
- 结果是一个变量引用，如果两个 variable_references 都是可写的，则它是可写的。

> *注意：* 当存在 ref 时，conditional_expression 返回一个变量引用，该引用可使用 = ref 运算符分配给引用变量，或作为引用/输入/输出参数传递。结束注意

如果不存在 ref，则 ?: 运算符的第二个和第三个操作数 x 和 y 控制条件表达式的类型：
- 如果 x 的类型为 X 且 y 的类型为 Y，则
  - 如果 X 和 Y 之间存在恒等转换，则结果为一组表达式的最佳公共类型（§12.6.3.15）。如果任一类型为 dynamic，则类型推断优先选择 dynamic（§8.7）。如果任一类型为元组类型（§8.3.11），则当两个元组中相同序数位置的元素名称匹配时，类型推断会包含元素名称。
  - 否则，如果存在从 X 到 Y 的隐式转换（§10.2），但不存在从 Y 到 X 的隐式转换，则 Y 为条件表达式的类型。
  - 否则，如果存在从 X 到 Y 的隐式枚举转换（§10.2.4），则 Y 为条件表达式的类型。
  - 否则，如果存在从 Y 到 X 的隐式枚举转换（§10.2.4），则 X 为条件表达式的类型。
  - 否则，如果存在从 Y 到 X 的隐式转换（§10.2），但不存在从 X 到 Y 的隐式转换，则 X 为条件表达式的类型。
  - 否则，无法确定表达式类型，将发生编译时错误。
- 如果只有 x 和 y 中的一个具有类型，并且 x 和 y 都可隐式转换为该类型，则该类型为条件表达式的类型。
- 否则，无法确定表达式类型，将发生编译时错误。

形式为 b ? ref x : ref y 的 ref 条件表达式的运行时处理包括以下步骤：
- 首先，`b` 被计算，并且 `b` 的 `bool` 值被确定：
  - 如果存在从 `b` 的类型到 `bool` 的隐式转换，则执行此隐式转换以生成 `bool` 值。
  - 否则，调用 `b` 的类型定义的 `true` 运算符以生成 `bool` 值。
- 如果上一步产生的 `bool` 值为 `true`，则计算 `x`，并且 resulting 变量引用成为条件表达式的结果。
- 否则，计算 `y`，并且 resulting 变量引用成为条件表达式的结果。

形式为 `b ? x : y` 的条件表达式的运行时处理包括以下步骤：
- 首先，`b` 被计算，并且 `b` 的 `bool` 值被确定：
  - 如果存在从 `b` 的类型到 `bool` 的隐式转换，则执行此隐式转换以生成 `bool` 值。
  - 否则，调用 `b` 的类型定义的 `true` 运算符以生成 `bool` 值。
- 如果上一步产生的 `bool` 值为 `true`，则计算 `x` 并将其转换为条件表达式的类型，这成为条件表达式的结果。
- 否则，计算 `y` 并将其转换为条件表达式的类型，这成为条件表达式的结果。

## 12.19 匿名函数表达式

### 12.19.1 通用

*匿名函数* 是表示“内联”方法定义的表达式。匿名函数本身没有值或类型，但可转换为兼容的委托或表达式树类型。匿名函数转换的求值取决于转换的目标类型：如果目标类型是委托类型，则转换求值为引用匿名函数定义的方法的委托值。如果目标类型是表达式树类型，则转换求值为表示方法结构为对象结构的表达式树。

> *注意：* 出于历史原因，匿名函数有两种语法风格，即 *lambda 表达式* 和 *匿名方法表达式*。对于几乎所有目的，*lambda 表达式* 比 *匿名方法表达式* 更简洁、更具表达力，而后者为向后兼容而保留在语言中。*结束注意*

```
lambda_expression
    : 'async'? anonymous_function_signature '=>' anonymous_function_body
    ;

anonymous_method_expression
    : 'async'? 'delegate' explicit_anonymous_function_signature? block
    ;

anonymous_function_signature
    : explicit_anonymous_function_signature
    | implicit_anonymous_function_signature
    ;
```

```
explicit_anonymous_function_signature
: '(' explicit_anonymous_function_parameter_list? ')'
;

explicit_anonymous_function_parameter_list
: explicit_anonymous_function_parameter
(',' explicit_anonymous_function_parameter)*
;

explicit_anonymous_function_parameter
: anonymous_function_parameter_modifier? type identifier
;

anonymous_function_parameter_modifier
: 'ref'
| 'out'
| 'in'
;

implicit_anonymous_function_signature
: '(' implicit_anonymous_function_parameter_list? ')'
| implicit_anonymous_function_parameter
;

implicit_anonymous_function_parameter_list
: implicit_anonymous_function_parameter
(',' implicit_anonymous_function_parameter)*
;

implicit_anonymous_function_parameter
: identifier
;

anonymous_function_body
: null_conditional_invocation_expression
| expression
| 'ref' variable_reference
| block
;
```

在识别*匿名函数体*时，如果*空条件调用表达式*和*表达式*这两个备选形式都适用，则应选择前者。

注意：此处各备选形式之间的重叠和优先级仅出于描述上的便利；语法规则可以进一步细化以消除重叠。ANTLR 及其他语法系统采用同样的便利做法，因此*匿名函数体*会自动具有所指定的语义。注意结束

注意：当被视为*表达式*时，如果 M 的结果类型为 void，那么诸如 x?.M() 这样的语法形式将是错误（§12.8.12）。但当被视为*空条件调用表达式*时，结果类型允许为 void。注意结束

示例：List<T>.Reverse 的结果类型为 void。在以下代码中，匿名表达式的主体是*空条件调用表达式*，因此不是错误。

```
Action<List<int>> a = x => x?.Reverse();
```

示例结束

=> 运算符与赋值（=）具有相同的优先级，并且是右结合的。

带有 async 修饰符的匿名函数是异步函数，并遵循 §15.15 中描述的规则。

以 *lambda 表达式*形式表示的匿名函数的参数可以显式或隐式类型化。在显式类型化参数列表中，每个参数的类型都显式声明。在隐式类型化参数列表中，参数类型从匿名函数出现的上下文中推断——具体而言，当匿名函数转换为兼容的委托类型或表达式树类型时，该类型提供参数类型（§10.7）。

在具有单个隐式类型化参数的 *lambda 表达式*中，参数列表中的括号可以省略。换言之，以下形式的匿名函数

```
( «param» ) => «expr»
```

可以缩写为

```
«param» => «expr»
```

以 *匿名方法表达式*形式表示的匿名函数的参数列表是可选的。如果给出，参数应显式类型化。如果未给出，则匿名函数可转换为具有任何不包含 out 参数的参数列表的委托。

匿名函数的块体始终是可到达的（§13.2）。

示例：下面给出匿名函数的一些示例：

```
x => x + 1 // Implicitly typed, expression body
x => { return x + 1; } // Implicitly typed, block body
(int x) => x + 1 // Explicitly typed, expression body
(int x) => { return x + 1; } // Explicitly typed, block body
(x, y) => x * y // Multiple parameters
() => Console.WriteLine() // No parameters
async (t1, t2) => await t1 + await t2 // Async
delegate (int x) { return x + 1; } // Anonymous method expression
delegate { return 1 + 1; } // Parameter list omitted
```

示例结束

*lambda 表达式*和*匿名方法表达式*的行为相同，但以下几点除外：

- *匿名方法表达式*允许完全省略参数列表，从而可转换为任何值参数列表的委托类型。
- *lambda 表达式*允许省略并推断参数类型，而*匿名方法表达式*要求显式声明参数类型。
- *lambda 表达式*的主体可以是表达式或块，而*匿名方法表达式*的主体必须是块。
- 只有 *lambda 表达式*具有到兼容表达式树类型的转换（§8.6）。

## 12.19.2 匿名函数签名

匿名函数的*匿名函数签名*定义该匿名函数的形式参数的名称以及可选类型。匿名函数参数的作用域是*匿名函数体*（§7.7）。与参数列表（如果给出）一起，匿名方法体构成声明空间（§7.3）。因此，匿名函数的参数名称如果与作用域包含*匿名方法表达式*或*lambda 表达式*的局部变量、局部常量或参数名称匹配，则属于编译时错误。

如果匿名函数具有*显式匿名函数签名*，则兼容的委托类型和表达式树类型的集合仅限于具有相同参数类型和修饰符且顺序相同的类型（§10.7）。与方法组转换（§10.8）不同，不支持匿名函数参数类型的逆变。如果匿名函数没有*匿名函数签名*，则兼容的委托类型和表达式树类型的集合仅限于没有 out 参数的类型。

注意，*匿名函数签名*不能包含特性或参数数组。然而，*匿名函数签名*可以与参数列表包含参数数组的委托类型兼容。

另请注意，到表达式树类型的*转换*即使兼容，仍可能在编译时失败（§8.6）。

## 12.19.3 匿名函数体

匿名函数的主体（*表达式*或*块*）遵循以下规则：

- 如果匿名函数包含签名，则签名中指定的参数可在主体中使用。如果匿名函数没有签名，它可以转换为带参数的委托类型或表达式类型（§10.7），但在主体中无法访问这些参数。
- 除最近封闭匿名函数的签名（如果有）中指定的 *in*、*out* 或 *ref* 参数外，主体访问 *in*、*out* 或 *ref* 参数属于编译时错误。
- 除最近封闭匿名函数的签名（如果有）中指定的参数外，主体访问 *ref struct* 类型的参数属于编译时错误。
- 当 *this* 的类型为结构类型时，主体访问 *this* 属于编译时错误。无论访问是显式的（如 *this.x*）还是隐式的（如 *x*，其中 *x* 是结构体的实例成员），都是如此。此规则仅禁止此类访问，不影响成员查找是否得到结构体的成员。
- 主体可以访问匿名函数的外部变量（§12.19.6）。访问外部变量将引用在求值 *lambda 表达式*或*匿名方法表达式*时处于活动状态的变量实例（§12.19.7）。
- 主体包含目标在主体之外或包含的*匿名函数*主体之内的 *goto* 语句、*break* 语句或 *continue* 语句属于编译时错误。
- 主体中的 *return* 语句从最近封闭*匿名函数*的调用返回控制，而不是从封闭的函数成员返回。

除通过求值和调用 *lambda 表达式*或*匿名方法表达式*之外，是否存在任何方式执行匿名函数的块，明确未作规定。特别是，编译器可以选择通过合成一个或多个命名方法或类型来实现匿名函数。任何此类合成元素的名称应采用保留供编译器使用的形式（§6.4.3）。



## 12.19.4 重载解析

匿名函数在参数列表中参与类型推断和重载解析。有关确切规则，请参阅 §12.6.3 和 §12.6.4。

*示例：* 下面的示例说明了匿名函数对重载解析的影响。

```
class ItemList<T> : List<T>
{
    public int Sum(Func<T, int> selector)
    {
        int sum = 0;
        foreach (T item in this)
        {
            sum += selector(item);
        }
        return sum;
    }

    public double Sum(Func<T, double> selector)
    {
        double sum = 0;
        foreach (T item in this)
        {
            sum += selector(item);
        }
        return sum;
    }
}
```

ItemList<T> 类有两个 Sum 方法。每个方法都接受一个选择器参数，该参数从列表项中提取要求和的值。提取的值可以是 int 也可以是 double，结果求和值同样是 int 或 double。

例如，Sum 方法可用于从订单中的明细行列表计算总和。

```
class Detail
{
    public int UnitCount;
    public double UnitPrice;
    ...
}
```

```
class A
{
    void ComputeSums()
    {
        ItemList<Detail> orderDetails = GetOrderDetails( ... );
        int totalUnits = orderDetails.Sum(d => d.UnitCount);
        double orderTotal = orderDetails.Sum(d => d.UnitPrice * d.UnitCount);
        ...
    }

    ItemList<Detail> GetOrderDetails( ... )
    {
        ...
    }
}
}
```

在对 orderDetails.Sum 的第一次调用中，两个 Sum 方法都适用，因为匿名函数 d => d.UnitCount 与 Func<Detail,int> 和 Func<Detail,double> 都兼容。然而，重载解析选择第一个 Sum 方法，因为转换为 Func<Detail,int> 比转换为 Func<Detail,double> 更好。

在对 orderDetails.Sum 的第二次调用中，只有第二个 Sum 方法适用，因为匿名函数 d => d.UnitPrice * d.UnitCount 产生的值类型为 double。因此，重载解析为该调用选择第二个 Sum 方法。

*结束示例*

## 12.19.5 匿名函数与动态绑定

匿名函数不能作为动态绑定操作的接收者、参数或操作数。

## 12.19.6 外部变量

### 12.19.6.1 一般

任何作用域包含 lambda_expression 或 anonymous_method_expression 的局部变量、值参数或参数数组都称为匿名函数的外部变量。在类的实例函数成员中，this 值被视为值参数，并且是该函数成员中包含的任何匿名函数的外部变量。

### 12.19.6.2 被捕获的外部变量

当匿名函数引用外部变量时，称该外部变量已被匿名函数捕获。通常，局部变量的生命周期仅限于与其关联的块或语句的执行（§9.2.9）。然而，被捕获的外部变量的生命周期至少会延长到从匿名函数创建的委托或表达式树有资格进行垃圾回收为止。

*示例：* 在下面的示例中

```csharp
delegate int D();

class Test
{
    static D F()
    {
        int x = 0;
        D result = () => ++x;
        return result;
    }

    static void Main()
    {
        D d = F();
        Console.WriteLine(d());
        Console.WriteLine(d());
        Console.WriteLine(d());
    }
}
```

局部变量 x 被匿名函数捕获，并且 x 的生命周期至少会延长到从 F 返回的委托有资格进行垃圾回收为止。由于匿名函数的每次调用都操作 x 的同一个实例，因此示例的输出为：

```
1
2
3
```

*结束示例*

当局部变量或值参数被匿名函数捕获时，该局部变量或参数不再被视为固定变量（§23.4），而是被视为可移动变量。然而，被捕获的外部变量不能在 fixed 语句（§23.7）中使用，因此不能获取被捕获外部变量的地址。

> *注意：* 与未捕获变量不同，被捕获的局部变量可以同时暴露给多个执行线程。 *结束注意*

### 12.19.6.3 局部变量的实例化

当执行进入变量的作用域时，局部变量被认为已 *实例化*。

*示例：* 例如，当以下方法被调用时，局部变量 x 会被实例化并初始化三次——每次循环迭代一次。

```csharp
static void F()
{
    for (int i = 0; i < 3; i++)
    {
        int x = i * 2 + 1;
        ...
    }
}
```

然而，将 x 的声明移出循环会导致 x 仅被实例化一次：

```csharp
static void F()
{
    int x;
    for (int i = 0; i < 3; i++)
    {
        x = i * 2 + 1;
        ...
    }
}
```

*结束示例*

当未被捕获时，没有办法精确观察局部变量被实例化的次数——因为实例化的生命周期是分离的，因此每次实例化可能只是简单地使用相同的存储位置。然而，当匿名函数捕获局部变量时，实例化的影响变得明显。

*示例：* 示例

```csharp
delegate void D();
class Test
{
    static D[] F()
    {
        D[] result = new D[3];
        for (int i = 0; i < 3; i++)
        {
            int x = i * 2 + 1;
            result[i] = () => Console.WriteLine(x);
        }
        return result;
    }

    static void Main()
    {
        foreach (D d in F())
        {
            d();
        }
    }
}
```

输出为：

```
1
3
5
```

然而，当 x 的声明被移出循环时：

```csharp
delegate void D();

class Test
{
    static D[] F()
    {
        D[] result = new D[3];
        int x;
        for (int i = 0; i < 3; i++)
        {
            x = i * 2 + 1;
            result[i] = () => Console.WriteLine(x);
        }
        return result;
    }

    static void Main()
    {
        foreach (D d in F())
        {
            d();
        }
    }
}
```

输出为：

```
5
5
5
```

请注意，编译器允许（但不是必须）将三次实例化优化为单个委托实例（§10.7.2）。

*结束示例*

如果 for 循环声明了迭代变量，则该变量本身被认为是在循环外部声明的。

*示例：* 因此，如果示例被修改为捕获迭代变量本身：

```csharp
delegate void D();

class Test
{
    static D[] F()
    {
        D[] result = new D[3];
        for (int i = 0; i < 3; i++)
        {
            result[i] = () => Console.WriteLine(i);
        }
        return result;
    }

    static void Main()
    {
        foreach (D d in F())
        {
            d();
        }
    }
}
```

仅捕获迭代变量的一个实例，这会产生以下输出：

```
3
3
3
```

*结束示例*

匿名函数委托可以共享某些被捕获的变量，同时对其他变量具有单独的实例。

*示例：* 例如，如果 F 被修改为

```csharp
static D[] F()
{
    D[] result = new D[3];
    int x = 0;
    for (int i = 0; i < 3; i++)
    {
        int y = 0;
        result[i] = () => Console.WriteLine($"{++x} {++y}");
    }
    return result;
}
```

三个委托捕获 x 的同一个实例，但 y 的单独实例，并且输出为：

```
1 1
2 1
3 1
```

*结束示例*

单独的匿名函数可以捕获外部变量的同一个实例。

*示例：* 在下面的示例中：

```csharp
delegate void Setter(int value);
delegate int Getter();

class Test
{
    static void Main()
    {
        int x = 0;
        Setter s = (int value) => x = value;
        Getter g = () => x;
        s(5);
        Console.WriteLine(g());
        s(10);
        Console.WriteLine(g());
    }
}
```

这两个匿名函数捕获局部变量 x 的同一个实例，因此它们可以通过该变量进行“通信”。示例的输出为：

```
5
10
```

*结束示例*

## 12.19.7 匿名函数表达式的求值

匿名函数 F 始终应转换为委托类型 D 或表达式树类型 E，要么直接转换，要么通过执行委托创建表达式 new D(F) 进行转换。这种转换决定了匿名函数的结果，如 §10.7 所述。

## 12.19.8 实现示例

### 本小节具有说明性。

本小节描述了以其他 C# 构造表示的匿名函数转换的一种可能实现。这里描述的实现基于商业 C# 编译器所使用的相同原则，但它绝不是强制性的实现，也不是唯一可能的实现。它仅简要提及到表达式树的转换，因为其确切语义超出了本规范的范围。

本小节的其余部分给出了包含具有不同特征的匿名函数的若干代码示例。对于每个示例，都提供了使用仅其他 C# 构造的代码的相应翻译。在示例中，标识符 D 被假定表示以下委托类型：

```csharp
public delegate void D();
```

匿名函数的最简单形式是不捕获任何外部变量的形式：

```
delegate void D();

class Test
{
    static void F()
    {
        D d = () => Console.WriteLine("test");
    }
}
```

这可以转换为一个委托实例化，该实例化引用一个编译器生成的静态方法，匿名函数的代码被放置在该方法中：

```
delegate void D();

class Test
{
    static void F()
    {
        D d = new D(__Method1);
    }

    static void __Method1()
    {
        Console.WriteLine("test");
    }
}
```

在下面的示例中，匿名函数引用了 this 的实例成员：

```
delegate void D();

class Test
{
    int x;

    void F()
    {
        D d = () => Console.WriteLine(x);
    }
}
```

这可以转换为一个编译器生成的实例方法，该方法包含匿名函数的代码：

```
delegate void D();

class Test
{
    int x;

    void F()
    {
        D d = new D(__Method1);
    }

    void __Method1()
    {
        Console.WriteLine(x);
    }
}
```

在此示例中，匿名函数捕获了一个局部变量：

```
delegate void D();

class Test
{
    void F()
    {
        int y = 123;
        D d = () => Console.WriteLine(y);
    }
}
```

现在，该局部变量的生命周期必须至少延长到匿名函数委托的生命周期。这可以通过将局部变量“提升”到编译器生成的类的字段中来实现。局部变量的实例化（§12.19.6.3）于是对应于创建编译器生成的类的一个实例，而访问局部变量则对应于访问编译器生成的类实例中的字段。此外，匿名函数成为编译器生成的类的一个实例方法：

```
delegate void D();

class Test
{
    void F()
    {
        __Locals1 __locals1 = new __Locals1();
        __locals1.y = 123;
        D d = new D(__locals1.__Method1);
    }

    class __Locals1
    {
        public int y;

        public void __Method1()
        {
            Console.WriteLine(y);
        }
    }
}
```

最后，下面的匿名函数捕获了 this 以及两个具有不同生命周期的局部变量：

```
delegate void D();

class Test
{
    int x;

    void F()
    {
        int y = 123;
        for (int i = 0; i < 10; i++)
        {
            int z = i * 2;
            D d = () => Console.WriteLine(x + y + z);
        }
    }
}
```

这里，为捕获了局部变量的每个块创建一个编译器生成的类，这样不同块中的局部变量可以具有独立的生命周期。__Locals2（内部块的编译器生成类）的一个实例包含局部变量 z 和一个引用 __Locals1 实例的字段。__Locals1（外部块的编译器生成类）的一个实例包含局部变量 y 和一个引用外层函数成员的 this 的字段。借助这些数据结构，可以通过一个 __Local2 实例访问所有被捕获的外部变量，因此匿名函数的代码可以实现为该类的一个实例方法。

```
delegate void D();

class Test
{
    int x;

    void F()
    {
        __Locals1 __locals1 = new __Locals1();
        __locals1.__this = this;
        __locals1.y = 123;
        for (int i = 0; i < 10; i++)
        {
            __Locals2 __locals2 = new __Locals2();
            __locals2.__locals1 = __locals1;
            __locals2.z = i * 2;
            D d = new D(__locals2.__Method1);
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

        public void __Method1()
        {
            Console.WriteLine(__locals1.__this.x + __locals1.y + z);
        }
    }
}
```

这里用于捕获局部变量的相同技术也可在将匿名函数转换为表达式树时使用：对编译器生成的对象的引用可以存储在表达式树中，对局部变量的访问可以表示为对这些对象的字段访问。这种方法的优势在于，它允许“提升”后的局部变量在委托和表达式树之间共享。

**信息性文本结束。**

## 12.20 查询表达式

### 12.20.1 概述

*查询表达式*为查询提供了一种语言集成的语法，类似于 SQL 和 XQuery 等关系型和层次型查询语言。

```
query_expression
    : from_clause query_body
    ;

from_clause
    : 'from' type? identifier 'in' expression
    ;

query_body
    : query_body_clauses? select_or_group_clause query_continuation?
    ;

query_body_clauses
    : query_body_clause
    | query_body_clauses query_body_clause
    ;

query_body_clause
    : from_clause
    | let_clause
    | where_clause
    | join_clause
    | join_into_clause
    | orderby_clause
    ;

let_clause
    : 'let' identifier '=' expression
    ;

where_clause
    : 'where' boolean_expression
    ;

join_clause
    : 'join' type? identifier 'in' expression 'on' expression
      'equals' expression
    ;
```

```
join_into_clause
  : 'join' type? identifier 'in' expression 'on' expression
    'equals' expression 'into' identifier
  ;

orderby_clause
  : 'orderby' orderings
  ;

orderings
  : ordering (',' ordering)*
  ;

ordering
  : expression ordering_direction?
  ;

ordering_direction
  : 'ascending'
  | 'descending'
  ;

select_or_group_clause
  : select_clause
  | group_clause
  ;

select_clause
  : 'select' expression
  ;

group_clause
  : 'group' expression 'by' expression
  ;

query_continuation
  : 'into' identifier query_body
  ;
```

查询表达式以 from 子句开始，以 select 或 group 子句结束。初始的 from 子句后面可以跟零个或多个 from、let、where、join 或 orderby 子句。每个 from 子句都是一个生成器，引入一个范围变量，该变量遍历序列中的元素。每个 let 子句引入一个范围变量，该变量表示通过先前范围变量计算出的值。每个 where 子句都是一个筛选器，将项从结果中排除。每个 join 子句将源序列的指定键与另一个序列的键进行比较，从而生成匹配的对。每个 orderby 子句根据指定条件对项进行重新排序。最后的 select 或 group 子句根据范围变量指定结果的形状。最后，into 子句可用于“拼接”查询，方法是将一个查询的结果作为后续查询中的生成器。

### 12.20.2 查询表达式中的歧义

查询表达式使用了多个上下文关键字（§6.4.4）：ascending、by、descending、equals、from、group、into、join、let、on、orderby、select 和 where。

为了避免将这些标识符同时用作关键字和简单名称可能引起的歧义，这些标识符在查询表达式中的任意位置都被视为关键字，除非它们带有“@”前缀（§6.4.4），在这种情况下它们被视为标识符。为此，查询表达式是指以“from identifier”开头、后跟除“;”、“-”或“,”之外的任何标记的任何表达式。

### 12.20.3 查询表达式转换

### 12.20.3.1 概述

C# 语言没有规定查询表达式的执行语义。查询表达式被转换为对符合查询表达式模式（§12.20.4）的方法的调用。具体来说，查询表达式被转换为对名为 Where、Select、SelectMany、Join、GroupJoin、OrderBy、OrderByDescending、ThenBy、ThenByDescending、GroupBy 和 Cast 的方法的调用。这些方法应具有特定的签名和返回类型，如 §12.20.4 所述。这些方法可以是被查询对象的实例方法，也可以是该对象外部的扩展方法。这些方法实现了查询的实际执行。

从查询表达式到方法调用的转换是一种语法映射，它在执行任何类型绑定或重载解析之前进行。查询表达式转换后，所得的方法调用将作为常规方法调用处理，这可能会进而发现编译时错误。这些错误情况包括但不限于方法不存在、实参类型错误，以及类型推断失败的泛型方法。

查询表达式通过反复应用以下转换来处理，直到无法进一步归约为止。这些转换按应用顺序列出：每个小节都假定前面小节中的转换已彻底执行，并且一旦彻底执行，在处理同一查询表达式时不会再回到该小节。

查询表达式如果包含对范围变量的赋值，或将范围变量用作 ref 或 out 参数的实参，则属于编译时错误。

某些转换会注入带有透明标识符（用 * 表示）的范围变量。这些内容将在 §12.20.3.8 中进一步描述。

### 12.20.3.2 带延续的查询表达式

查询体后带有延续的查询表达式

```
from «x1» in «e1» «b1» into «x2» «b2»
```

被转换为

```
from «x2» in ( from «x1» in «e1» «b1» ) «b2»
```

以下小节中的转换假设查询没有延续。

示例：以下示例：

```
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```

被转换为：

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

示例结束

## 12.20.3.3 显式范围变量类型

一个显式指定范围变量类型的 from 子句

```
from «T» «x» in «e»
```

翻译为

```
from «x» in ( «e» ) . Cast < «T» > ( )
```

一个显式指定范围变量类型的 join 子句

```
join «T» «x» in «e» on «k1» equals «k2»
```

翻译为

```
join «x» in ( «e» ) . Cast < «T» > ( ) on «k1» equals «k2»
```

以下各节中的翻译假定查询没有显式范围变量类型。

示例：示例

```
from Customer c in customers
where c.City == "London"
select c
```

翻译为

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

示例结束

注意：显式范围变量类型对于查询实现非泛型 IEnumerable 接口但未实现泛型 IEnumerable<T> 接口的集合很有用。在上面的示例中，如果 customers 的类型为 ArrayList，就会是这种情况。 注意结束

## 12.20.3.4 退化查询表达式

形式为的查询表达式

```
from «x» in «e» select «x»
```

翻译为

```
( «e» ) . Select ( «x» => «x» )
```

示例：示例

```
from c in customers
select c
```

翻译为

```
(customers).Select(c => c)
```

示例结束

退化查询表达式是指对源元素进行平凡选择的表达式。

> 注意：翻译的后期阶段（§12.20.3.6 和 §12.20.3.7）通过将其替换为其源来删除由其他翻译步骤引入的退化查询。然而，重要的是要确保查询表达式的结果永远不是源对象本身。否则，返回此类查询的结果可能会无意中向调用方公开私有数据（例如元素数组）。因此，此步骤通过显式地在源上调用 Select 来保护直接在源代码中编写的退化查询。然后，Select 和其他查询运算符的实现者有责任确保这些方法永远不会返回源对象本身。 注意结束

## 12.20.3.5 From、let、where、join 和 orderby 子句

带有第二个 from 子句后跟 select 子句的查询表达式

```
from «x1» in «e1»
from «x2» in «e2»
select «v»
```

翻译为

```
( «e1» ) . SelectMany( «x1» => «e2» , ( «x1» , «x2» ) => «v» )
```

示例：示例

```
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```

翻译为

```
(customers).
SelectMany(c => c.Orders,
(c,o) => new { c.Name, o.OrderID, o.Total }
)
```

示例结束

带有第二个 from 子句后跟包含非空查询主体子句集的查询主体 Q 的查询表达式：

```
from «x1» in «e1»
from «x2» in «e2»
Q
```

翻译为

```
from * in («e1») . SelectMany( «x1» => «e2» , ( «x1» , «x2» ) => new { «x1» , «x2» } )
Q
```

示例：示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

翻译为

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

其中 x 是一个编译器生成的标识符，否则不可见且无法访问。

示例结束

一个 let 表达式连同其前面的 from 子句：

```
from «x» in «e»
let «y» = «f»
...
```

翻译为

```
from * in ( «e» ) . Select ( «x» => new { «x» , «y» = «f» } )
...
```

示例：示例

```
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```

翻译为

```
from * in (orders).Select(
    o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000
select new { o.OrderID, Total = t }
```

其最终翻译为

```
orders
.Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
.Where(x => x.t >= 1000)
.Select(x => new { x.o.OrderID, Total = x.t })
```

其中 x 是一个编译器生成的标识符，否则不可见且无法访问。

示例结束

一个 where 表达式连同其前面的 from 子句：

```
from «x» in «e»
where «f»
...
```

翻译为

```
from «x» in ( «e» ) . Where ( «x» => «f» )
...
```

```
    from c in customers
    join o in orders on c.CustomerID equals o.CustomerID into co
    let n = co.Count()
    where n >= 10
    select new { c.Name, OrderCount = n }
```

翻译为

```
    from * in (customers).GroupJoin(
        orders,
        c => c.CustomerID,
        o => o.CustomerID,
        (c, co) => new { c, co })
    let n = co.Count()
    where n >= 10
    select new { c.Name, OrderCount = n }
```

其最终翻译为

```
    customers
        .GroupJoin(
            orders,
            c => c.CustomerID,
            o => o.CustomerID,
            (c, co) => new { c, co })
        .Select(x => new { x, n = x.co.Count() })
        .Where(y => y.n >= 10)
        .Select(y => new { y.x.c.Name, OrderCount = y.n })
```

其中 x 和 y 是编译器生成的标识符，否则不可见且无法访问。

*示例结束*

一个 orderby 子句及其前面的 from 子句：

```
    from «x» in «e»
    orderby «k1» , «k2» , ... , «kn»
    ...
```

翻译为

```
    from «x» in ( «e» ) .
        OrderBy ( «x» => «k1» ) .
        ThenBy ( «x» => «k2» ) .
        ...
        ThenBy ( «x» => «kn» )
        ...
```

如果排序子句指定了降序方向指示符，则会生成 OrderByDescending 或 ThenByDescending 的调用。

*示例：示例*

```
    from o in orders
    orderby o.Customer.Name, o.Total descending
    select o
```

的最终翻译为

```
(orders)
.OrderBy(o => o.Customer.Name)
.ThenByDescending(o => o.Total)
end example
```

示例结束

以下翻译假定没有 let、where、join 或 orderby 子句，并且每个查询表达式中最多只有一个初始 from 子句。

## 12.20.3.6 Select 子句

形式为的查询表达式

```
from «x» in «e» select «v»
```

翻译为

```
( «e» ) . Select ( «x» => «v» )
```

除非 «v» 是标识符 «x»，翻译仅为

```
( «e» )
```

示例：示例

```
from c in customers.Where(c => c.City == "London")
select c
```

仅翻译为

```
(customers).Where(c => c.City == "London")
```

示例结束

## 12.20.3.7 Group 子句

一个 group 子句

```
from «x» in «e» group «v» by «k»
```

翻译为

```
( «e» ) . GroupBy ( «x» => «k» , «x» => «v» )
```

除非 «v» 是标识符 «x»，翻译为

```
( «e» ) . GroupBy ( «x» => «k» )
```

示例：示例

```
from c in customers
group c.Name by c.Country
```

翻译为

```
(customers).GroupBy(c => c.Country, c => c.Name)
```

## 12.20.3.8 透明标识符

某些翻译会注入用 * 表示的透明标识符的范围变量。透明标识符仅作为查询表达式翻译过程中的中间步骤存在。

当查询翻译注入透明标识符时，后续的翻译步骤会将透明标识符传播到匿名函数和匿名对象初始化器中。在这些上下文中，透明标识符具有以下行为：

- 当透明标识符作为匿名函数的参数出现时，与之关联的匿名类型的成员会在匿名函数体中自动进入作用域。
- 当具有透明标识符的成员在作用域内时，该成员的成员也在作用域内。
- 当透明标识符作为匿名对象初始化器中的成员声明符出现时，它会引入一个具有透明标识符的成员。

在上述描述的翻译步骤中，透明标识符始终与匿名类型一起引入，其目的是将多个范围变量作为单个对象的成员捕获。C# 的实现可以使用不同于匿名类型的机制来组合多个范围变量。以下翻译示例假定使用匿名类型，并展示了透明标识符的一种可能翻译。

示例：示例

```
```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```
```

翻译为

```
```
from * in (customers).SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.Total }
```
```

进一步翻译为

```
```
customers
    .SelectMany(c => c.Orders, (c,o) => new { c, o })
    .OrderByDescending(* => o.Total)
    .Select(* => new { c.Name, o.Total })
```
```

当透明标识符被擦除时，等价于

```
```
customers
    .SelectMany(c => c.Orders, (c,o) => new { c, o })
    .OrderByDescending(x => x.o.Total)
    .Select(x => new { x.c.Name, x.o.Total })
```
```

其中 x 是一个编译器生成的标识符，否则不可见且无法访问。

示例

```
```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
```

翻译为

```
```
from * in (customers).Join(
    orders,
    c => c.CustomerID,
```



## 12.20.4 查询表达式模式

查询表达式模式建立了一种方法模式，类型可以实现这些方法以支持查询表达式。

如果泛型类型 C<T> 的公共成员方法和可公开访问的扩展方法可以被以下类定义替换，则该泛型类型支持查询表达式模式。这些成员和可访问的扩展方法称为泛型类型 C<T> 的“形状”。使用泛型类型是为了说明参数类型和返回类型之间的正确关系，但也可以为非泛型类型实现该模式。

```
delegate R Func<T1,R>(T1 arg1);
delegate R Func<T1,T2,R>(T1 arg1, T2 arg2);

class C
{
    public C<T> Cast<T>() { ... }
}

class C<T> : C
{
    public C<T> Where(Func<T,bool> predicate) { ... }
    public C<U> Select<U>(Func<T,U> selector) { ... }
    public C<U> SelectMany<U,V>(Func<T,C<U>> selector,
        Func<T,U,V> resultSelector) { ... }
    public C<U> Join<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,U,V> resultSelector) { ... }
    public C<U> GroupJoin<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,C<U>,V> resultSelector) { ... }
    public O<T> OrderBy<K>(Func<T,K> keySelector) { ... }
    public O<T> OrderByDescending<K>(Func<T,K> keySelector) { ... }
    public C<G<K,T>> GroupBy<K>(Func<T,K> keySelector) { ... }
    public C<G<K,E>> GroupBy<K,E>(Func<T,K> keySelector,
        Func<T,E> elementSelector) { ... }
}
```

```
class O<T> : C<T>
{
    public O<T> ThenBy<K>(Func<T,K> keySelector) { ... }
    public O<T> ThenByDescending<K>(Func<T,K> keySelector) { ... }
}
```

```
class G<K,T> : C<T>
{
    public K Key { get; }
}
```

上述方法使用泛型委托类型 Func<T1, R> 和 Func<T1, T2, R>，但它们同样可以使用其他委托类型或表达式树类型，只要参数类型和返回类型具有相同的关系。

> 注意：推荐的 C<T> 与 O<T> 之间的关系，确保 ThenBy 和 ThenByDescending 方法仅在 OrderBy 或 OrderByDescending 的结果上可用。

> 注意：推荐的 GroupBy 结果形状——一个序列的序列，其中每个内部序列都有一个附加的 Key 属性。

> 注意：由于查询表达式通过语法映射转换为方法调用，类型在如何实现查询表达式模式的任意部分或全部方面具有相当大的灵活性。例如，模式中的方法可以实现为实例方法或扩展方法，因为二者具有相同的调用语法；并且这些方法可以要求委托或表达式树，因为匿名函数可转换为二者。仅实现查询表达式模式部分内容的类型，仅支持映射到该类型所支持方法的查询表达式转换。

> 注意：System.Linq 命名空间为任何实现 System.Collections.Generic.IEnumerable<T> 接口的类型提供查询表达式模式的实现。

## 12.21 赋值运算符

### 12.21.1 概述

除一个之外，所有赋值运算符都会将新值赋给变量、属性、事件或索引器元素。例外的是，= ref 将变量引用（§9.5）赋给引用变量（§9.7）。

```
assignment
: unary_expression assignment_operator expression
;

assignment_operator
: '=' 'ref'? | '+=' | '-=' | '*=' | '/=' | '%=' | '&=' | '|=' | '^=' | '<<='
| right_shift_assignment
;
```

赋值的左操作数应是分类为变量的表达式，或者，除 `= ref` 外，是属性访问、索引器访问、事件访问或元组。声明表达式不能直接作为左操作数，但可以作为解构赋值求值过程中的一个步骤出现。

`=` 运算符称为*简单赋值运算符*。它将右操作数的一个或多个值赋给左操作数给出的变量、属性、索引器元素或元组元素。简单赋值运算符的左操作数不得是事件访问（§15.8.2 所述情况除外）。简单赋值运算符在 §12.21.2 中描述。

运算符 `= ref` 称为*ref 赋值运算符*。它使右操作数（必须是*变量引用*（§9.5））成为左操作数指定的引用变量的引用对象。ref 赋值运算符在 §12.21.3 中描述。

除 `=` 和 `= ref` 运算符之外的赋值运算符称为*复合赋值运算符*。这些运算符对两个操作数执行指定的操作，然后将结果值赋给左操作数给出的变量、属性或索引器元素。复合赋值运算符在 §12.21.4 中描述。

以事件访问表达式作为左操作数的 `+=` 和 `-=` 运算符称为*事件赋值运算符*。其他任何赋值运算符都不能以事件访问作为左操作数。事件赋值运算符在 §12.21.5 中描述。

赋值运算符是右结合的，这意味着操作从右到左分组。

*示例：* 形式为 `a = b = c` 的表达式按 `a = (b = c)` 求值。

### 12.21.2 简单赋值

`=` 运算符称为简单赋值运算符。

如果简单赋值的左操作数形式为 `E.P` 或 `E[E1]`，其中 `E` 具有编译时类型 `dynamic`，则该赋值进行动态绑定（§12.3.3）。在这种情况下，赋值表达式的编译时类型为 `dynamic`，并且下面描述的解析将在运行时基于 `E` 的运行时类型进行。如果左操作数形式为 `E[E1]`，其中 `E1` 的至少一个元素具有编译时类型 `dynamic`，并且 `E` 的编译时类型不是数组，则结果索引器访问进行动态绑定，但具有有限的编译时检查（§12.6.5）。

左操作数分类为元组的简单赋值也称为*解构赋值*。如果左操作数的任何元组元素具有元素名称，则发生编译时错误。如果左操作数的任何元组元素是 `declaration_expression`，而任何其他元素不是 `declaration_expression` 或简单弃元，则发生编译时错误。

简单赋值 `x = y` 的类型是将 `y` 赋给 `x` 的赋值的类型，其递归确定如下：

- 如果 `x` 是元组表达式 `(x1, ..., xn)`，并且 `y` 可以解构为具有 `n` 个元素的元组表达式 `(y1, ..., yn)`（§12.7），且将 `yi` 赋给 `xi` 的每个赋值都具有类型 `Ti`，则该赋值具有类型 `(T1, ..., Tn)`。
- 否则，如果 `x` 分类为变量，该变量不是 `readonly`，`x` 具有类型 `T`，并且 `y` 具有到 `T` 的隐式转换，则该赋值具有类型 `T`。
- 否则，如果 `x` 分类为隐式类型变量（即隐式类型声明表达式），并且 `y` 具有类型 `T`，则该变量的推断类型为 `T`，并且该赋值具有类型 `T`。




- 否则，如果 x 被归类为属性或索引器访问，该属性或索引器具有可访问的 set 访问器，x 具有类型 T，并且 y 存在到 T 的隐式转换，则赋值具有类型 T。
- 否则该赋值无效，并发生绑定时间错误。

对于形式为 `x = y`、类型为 T 的简单赋值，其运行时处理是执行向 x 赋值类型为 T 的 y，该过程由以下递归步骤组成：

- 如果 x 尚未计算，则计算 x。
- 如果 x 被归类为变量，则计算 y，并在需要时通过隐式转换（§10.2）转换为 T。
    - 如果 x 指定的变量是引用类型的数组元素，则执行运行时检查，以确保为 y 计算的值与 x 所属的数组实例兼容。如果 y 为 null，或者存在从 y 引用的实例的类型到包含 x 的数组实例的实际元素类型的隐式引用转换（§10.2.8），则检查成功。否则，引发 `System.ArrayTypeMismatchException`。
    - y 的计算和转换所得的值会存储到由 x 的计算所给定的位置，并作为赋值的结果产生。
- 如果 x 被归类为属性或索引器访问：
    - 计算 y，并在需要时通过隐式转换（§10.2）转换为 T。
    - 以 y 的计算和转换所得的值作为其 value 参数调用 x 的 set 访问器。
    - y 的计算和转换所得的值作为赋值的结果产生。
- 如果 x 被归类为元组 (x1, ..., xn)，元数为 n：
    - y 被解构为具有 n 个元素的元组表达式 e。
    - 通过使用隐式元组转换将 e 转换为 T，创建结果元组 t。
    - 对于每个 xi 按从左到右的顺序，执行对 xi 的 t.Itemi 赋值，但不会再次计算 xi。
    - t 作为赋值的结果产生。

注意：如果 x 的编译时类型为 dynamic，并且存在从 y 的编译时类型到 dynamic 的隐式转换，则不需要运行时解析。注意结束。

注意：数组协变规则（§17.6）允许数组类型 A[] 的值引用数组类型 B[] 的实例，前提是存在从 B 到 A 的隐式引用转换。由于这些规则，向引用类型的数组元素赋值需要运行时检查，以确保所赋的值与数组实例兼容。例如：

```
string[] sa = new string[10];
object[] oa = sa;
oa[0] = null;              // OK
oa[1] = "Hello";           // OK
oa[2] = new ArrayList();   // ArrayTypeMismatchException
```

最后一个赋值会引发 `System.ArrayTypeMismatchException`，因为 `ArrayList` 的引用无法存储到 `string[]` 的元素中。

注意结束。

当结构类型中声明的属性或索引器成为赋值的对象时，与该属性或索引器访问关联的实例表达式必须被归类为变量。如果实例表达式被归类为值，则发生绑定时间错误。

> 注意：由于 §12.8.7，同一规则也适用于字段。注意结束。

示例：给定以下声明：

```
struct Point
{
    int x, y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

    public int X
    {
        get { return x; }
        set { x = value; }
    }

    public int Y {
        get { return y; }
        set { y = value; }
    }
}

struct Rectangle
{
    Point a, b;

    public Rectangle(Point a, Point b)
    {
        this.a = a;
        this.b = b;
    }

    public Point A
    {
        get { return a; }
        set { a = value; }
    }

    public Point B
    {
        get { return b; }
        set { b = value; }
    }
}
```

在示例中

```
Point p = new Point();
p.X = 100;
p.Y = 100;
Rectangle r = new Rectangle();
r.A = new Point(10, 10);
r.B = p;
```

对 p.X、p.Y、r.A 和 r.B 的赋值是允许的，因为 p 和 r 是变量。然而，在示例

```
Rectangle r = new Rectangle();
r.A.X = 10;
r.A.Y = 10;
r.B.X = 100;
r.B.Y = 100;
```

中，所有赋值均无效，因为 r.A 和 r.B 不是变量。

示例结束。

### 12.21.3 ref 赋值

`= ref` 运算符称为 ref 赋值运算符。

左操作数必须是一个绑定到引用变量（§9.7）、引用参数（this 除外）、输出参数或输入参数的表达式。右操作数必须是一个产生变量引用的表达式，该变量引用指示与左操作数相同类型的值。

如果左操作数的 ref 安全上下文（§9.7.2）比右操作数的 ref 安全上下文更宽，则发生编译时错误。

在 ref 赋值的位置，右操作数必须已明确赋值。

当左操作数绑定到 out 参数时，如果该 out 参数在 ref 赋值运算符开始时尚未明确赋值，则为错误。

如果左操作数是可写 ref（即，它指示的不是 ref readonly 局部变量或 in 参数），则右操作数必须是可写的变量引用。如果右操作数变量是可写的，则左操作数可以是可写或只读的 ref。

该操作使左操作数成为右操作数变量的别名。即使右操作数变量是可写的，该别名也可以设为只读。

ref 赋值运算符产生一个所赋类型的变量引用。如果左操作数可写，则它是可写的。

ref 赋值运算符不得读取右操作数引用的存储位置。

示例：以下是使用 `= ref` 的一些示例：

```
public static int M1() { ... }
public static ref int M2() { ... }
public static ref uint M2u() { ... }
public static ref readonly int M3() { ... }
public static void Test()
{
    int v = 42;
    ref int r1 = ref v;  // OK, r1 refers to v, which has value 42
    r1 = ref M1();       // Error; M1 returns a value, not a reference
    r1 = ref M2();       // OK; makes an alias
    r1 = ref M2u();   // Error; lhs and rhs have different types
    r1 = ref M3();    // error; M3 returns a ref readonly, which r1 cannot honor
    ref readonly int r2 = ref v;  // OK; make readonly alias to ref
    r2 = ref M2();    // OK; makes an alias, adding read-only protection
    r2 = ref M3();    // OK; makes an alias and honors the read-only
    r2 = ref (r1 = ref M2()); // OK; r1 is an alias to a writable variable,
    // r2 is an alias (with read-only access) to the same variable
}
```

示例结束。

注意：在使用 `= ref` 运算符阅读代码时，很容易将 ref 部分视为操作数的一部分。当操作数是条件 `?:` 表达式时，这一点尤其令人困惑。例如，阅读 `ref int a = ref b ? ref x : ref y;` 时，重要的是将其解读为 `= ref` 是运算符，而 `b ? ref x : ref y` 是右操作数：`ref int a = ref (b ? ref x : ref y);` 重要的是，表达式 `ref b` 不是该语句的一部分，尽管乍一看可能如此。注意结束。

### 12.21.4 复合赋值

如果复合赋值的左操作数形式为 `E.P` 或 `E[E i]`，其中 E 的编译时类型为 dynamic，则该赋值是动态绑定的（§12.3.3）。在这种情况下，赋值表达式的编译时类型为 dynamic，下文所述的解析将根据 E 的运行时类型在运行时进行。如果左操作数的形式为 `E[E i]`，其中 E i 的至少一个元素具有编译时类型 dynamic，并且 E 的编译时类型不是数组，则生成的索引器访问是动态绑定的，但带有有限的编译时检查（§12.6.5）。

形式为 `x «op»= y` 的操作通过应用二元运算符重载决策（§12.4.5）进行处理，就好像该操作被写成 `x «op» y` 一样。然后，

- 如果所选运算符的返回类型可隐式转换为 x 的类型，则该操作将计算为 `x = x «op» y`，只不过 x 只计算一次。
- 否则，如果所选运算符是预定义运算符，所选运算符的返回类型可显式转换为 x 的类型，并且 y 可隐式转换为 x 的类型或该运算符是移位运算符，则该操作将计算为 `x = (T)(x «op» y)`，其中 T 是 x 的类型，只不过 x 只计算一次。
- 否则，复合赋值无效，并发生绑定时间错误。

“只计算一次”是指在对 `x «op»= y` 的求值过程中，x 的任何构成表达式的结果都会被临时保存，然后在向 x 赋值时重新使用。

示例：在赋值 `A()[B()] += C()` 中，A 是返回 `int[]` 的方法，B 和 C 是返回 int 的方法，这些方法只调用一次，顺序为 A、B、C。示例结束。

当复合赋值的左操作数是属性访问或索引器访问时，该属性或索引器必须同时具有 get 访问器和 set 访问器。如果不是这种情况，则发生绑定时间错误。




预定义运算符规则的直观效果很简单：如果 x «op» y 和 x = y 都允许，则允许 x «op»= y。

*示例：在以下代码中*

```
byte b = 0;
char ch = '\0';
int i = 0;
b += 1;            // OK
b += 1000;         // Error, b = 1000 not permitted
b += i;            // Error, b = i not permitted
b += (byte)i;      // OK
ch += 1;           // Error, ch = 1 not permitted
ch += (char)1;     // OK
```

每个错误的直观原因是，相应的简单赋值本来也会是一个错误。

*示例结束*

*注意：这也意味着复合赋值运算支持提升运算符。由于复合赋值 x «op»= y 会按 x = x «op» y 或 x = (T)(x «op» y) 求值，求值规则隐式涵盖了提升运算符。注意结束*

### 12.21.5 事件赋值

如果 `+=` 或 `-=` 运算符的左操作数被归类为事件访问，则按如下方式对该表达式求值：

- 如果事件访问有实例表达式，则对该实例表达式求值。
- 对 `+=` 或 `-=` 运算符的右操作数求值，并在需要时通过隐式转换（§10.2）转换为左操作数的类型。
- 调用该事件的事件访问器，其参数列表由前一步计算出的值组成。如果运算符为 `+=`，则调用添加访问器；如果运算符为 `-=`，则调用移除访问器。

事件赋值表达式不产生值。因此，事件赋值表达式仅在 *statement_expression*（§13.7）的上下文中有效。

## 12.22 表达式

表达式要么是 *non_assignment_expression*，要么是 *assignment*。

```
expression
    : non_assignment_expression
    | assignment
    ;

non_assignment_expression
    : declaration_expression
    | conditional_expression
    | lambda_expression
    | query_expression
    ;
```

### 12.23 常量表达式

常量表达式是必须在编译时完全求值的表达式。

```
constant_expression
    : expression
    ;
```

常量表达式可以是值类型或引用类型。如果常量表达式是值类型，则它必须是以下类型之一：`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double`、`decimal`、`bool` 或任何枚举类型。如果常量表达式是引用类型，则它必须是 `string` 类型、某种引用类型的默认值表达式（§12.8.20），或者该表达式的值必须为 `null`。

常量表达式中只允许以下构造：

- 字面量（包括 `null` 字面量）。
- 对类和结构类型的 `const` 成员的引用。
- 对枚举类型成员的引用。
- 对局部常量的引用。
- 带括号的子表达式，这些子表达式本身也是常量表达式。
- 强制转换表达式。
- `checked` 和 `unchecked` 表达式。
- `nameof` 表达式。
- 预定义的 `+`、`-`、`!` 和 `~` 一元运算符。
- 预定义的 `+`、`-`、`*`、`/`、`%`、`<<`、`>>`、`&`、`|`、`^`、`&&`、`||`、`==`、`!=`、`<`、`>`、`<=` 和 `>=` 二元运算符。
- `?:` 条件运算符。
- `sizeof` 表达式，前提是非托管类型是 §23.6.9 中指定的、`sizeof` 会为其返回常量值的类型之一。
- 默认值表达式，前提是该类型是上面列出的类型之一。

常量表达式中允许以下转换：

- 恒等转换
- 数值转换
- 枚举转换
- 常量表达式转换
- 隐式和显式引用转换，前提是转换的源是求值为 `null` 值的常量表达式。

> *注意：其他转换（包括装箱、拆箱以及对非 `null` 值的隐式引用转换）在常量表达式中是不允许的。注意结束*

*示例：* 在以下代码中

```
class C
{
const object i = 5;    // error: boxing conversion not permitted
const object str = "hello"; // error: implicit reference conversion
}
```

i 的初始化是一个错误，因为需要装箱转换。str 的初始化是一个错误，因为需要从非 null 值进行隐式引用转换。

*示例结束*

只要表达式满足上面列出的要求，该表达式就在编译时求值。即使该表达式是包含非常量构造的更大表达式的子表达式，也是如此。

常量表达式的编译时求值使用与非常量表达式的运行时求值相同的规则，不同之处在于：如果运行时求值会引发异常，则编译时求值会导致发生编译时错误。

除非常量表达式被显式置于 `unchecked` 上下文中，否则在表达式的编译时求值期间，整型算术运算和转换中发生的溢出始终会导致编译时错误（§12.8.19）。

以下上下文中要求使用常量表达式，语法中通过使用 constant_expression 来表示这一点。在这些上下文中，如果表达式不能在编译时完全求值，则会发生编译时错误。

- 常量声明（§15.4）
- 枚举成员声明（§19.4）
- 形参列表的默认参数（§15.6.2）
- switch 语句的 case 标签（§13.8.3）。
- goto case 语句（§13.10.4）
- 包含初始化器的数组创建表达式（§12.8.16.5）中的维度长度。
- 特性（§22）
- 在 constant_pattern 中（§11.2.3）

隐式常量表达式转换（§10.2.11）允许将 int 类型的常量表达式转换为 sbyte、byte、short、ushort、uint 或 ulong，前提是该常量表达式的值在目标类型的范围内。

## 12.24 布尔表达式

boolean_expression 是产生 bool 类型结果的表达式；可以直接产生，也可以在特定上下文中通过应用 operator true 产生，具体如下：

```
boolean_expression
  : expression
  ;
```

if_statement（§13.8.2）、while_statement（§13.9.2）、do_statement（§13.9.3）或 for_statement（§13.9.4）的控制条件表达式是 boolean_expression。?: 运算符（§12.18）的控制条件表达式遵循与 boolean_expression 相同的规则，但由于运算符优先级的原因，被归类为 null_coalescing_expression。

要求 `boolean_expression` E 能够产生 `bool` 类型的值，如下所示：

- 如果 E 可隐式转换为 `bool`，则在运行时应用该隐式转换。
- 否则，使用一元运算符重载解析（§12.4.4）在 E 上查找 `operator true` 的唯一最佳实现，并在运行时应用该实现。
- 如果未找到此类运算符，则发生绑定期错误。

# 13. 语句

### 13.1 概述

C# 提供了多种语句。

> *注意：* 这些语句中的大多数对于使用过 C 和 C++ 编程的开发人员来说都很熟悉。
> *注意结束*

```
statement
: labeled_statement
| declaration_statement
| embedded_statement
;
```

```
embedded_statement
: block
| empty_statement
| expression_statement
| selection_statement
| iteration_statement
| jump_statement
| try_statement
| checked_statement
| unchecked_statement
| lock_statement
| using_statement
| yield_statement
| unsafe_statement    // unsafe code support
| fixed_statement    // unsafe code support
;
```

*unsafe_statement*（§23.2）和 *fixed_statement*（§23.7）仅在不安全代码（§23）中可用。

*embedded_statement* 非终结符用于出现在其他语句内的语句。使用 *embedded_statement* 而不是 *statement*，排除了在这些上下文中使用声明语句和带标签语句。

*示例：* 以下代码

```
void F(bool b)
{
    if (b)
        int i = 44;
}
```

会导致编译时错误，因为 *if* 语句的 *if* 分支要求使用 *embedded_statement* 而不是 *statement*。如果允许这段代码，那么变量 *i* 将被声明，但永远无法使用。但请注意，将 *i* 的声明放在块中，该示例就是有效的。

*示例结束*



## 13.2 终点和可达性

每条语句都有一个 *终点*。直观地说，语句的终点是紧跟在该语句之后的位置。复合语句（包含嵌入语句的语句）的执行规则指定了当控制流到达嵌入语句的终点时采取的动作。

> *示例：* 当控制流到达块中某条语句的终点时，控制流会转移到块中的下一条语句。 *示例结束*

如果一条语句可能通过执行到达，则该语句被称为 *可达*。相反，如果一条语句不可能被执行，则该语句被称为 *不可达*。

*示例：* 在下面的代码中

```
void F()
{
    Console.WriteLine("reachable");
    goto Label;
    Console.WriteLine("unreachable");
    Label:
    Console.WriteLine("reachable");
}
```

第二次调用 Console.WriteLine 是不可达的，因为该语句不可能被执行。

*示例结束*

如果除 *抛出语句*、*块* 或 *空语句* 之外的语句不可达，则会报告警告。语句不可达本身并不是错误。

> *注意：* 为了确定特定语句或终点是否可达，编译器会根据每个语句的可达性规则执行流分析。流分析会考虑控制语句行为的常量表达式 (§12.23) 的值，但不考虑非常量表达式的可能值。换句话说，就控制流分析而言，给定类型的非常量表达式被认为具有该类型的任何可能值。

在示例中

```
void F()
{
    const int i = 1;
    if (i == 2)
        Console.WriteLine("unreachable");
}
```

if 语句的布尔表达式是一个常量表达式，因为 == 运算符的两个操作数都是常量。由于常量表达式在编译时求值，结果为 false，因此 Console.WriteLine 调用被视为不可达。然而，如果 i 被改为局部变量

```
void F()
{
    int i = 1;
    if (i == 2)
Console.WriteLine("reachable");
}
```

Console.WriteLine 调用被视为可达，即使实际上它永远不会被执行。

*注意结束*

函数成员或匿名函数的块始终被视为可达。通过依次评估块中每条语句的可达性规则，可以确定任何给定语句的可达性。

示例：在下面的代码中

```
void F(int x)
{
    Console.WriteLine("start");
    if (x < 0)
    Console.WriteLine("negative");
}
```

第二个 Console.WriteLine 的可达性确定如下：

- 第一个 Console.WriteLine 表达式语句是可达的，因为 F 方法的块是可达的 (§13.3)。
- 第一个 Console.WriteLine 表达式语句的终点是可达的，因为该语句是可达的 (§13.7 和 §13.3)。
- if 语句是可达的，因为第一个 Console.WriteLine 表达式语句的终点是可达的 (§13.7 和 §13.3)。
- 第二个 Console.WriteLine 表达式语句是可达的，因为 if 语句的布尔表达式不具有常量值 false。

*示例结束*

有两种情况会导致语句的终点可达成为编译时错误：

- 由于 switch 语句不允许 switch 部分“贯穿”到下一个 switch 部分，因此 switch 部分的语句列表的终点可达是编译时错误。如果出现此错误，通常表示缺少 break 语句。
- 对于计算值的函数成员或匿名函数的块，其终点可达是编译时错误。如果出现此错误，通常表示缺少 return 语句 (§13.10.5)。

## 13.3 块

### 13.3.1 通用

块允许在只允许单个语句的上下文中编写多个语句。

```
block
    : '{' statement_list? '}'
    ;
```

块由可选的 statement_list (§13.3.2) 组成，用大括号括起来。如果省略语句列表，则该块称为空块。

块可以包含声明语句 (§13.6)。在块中声明的局部变量或常量的作用域是该块。

块的执行方式如下：

- 如果块为空，则控制流转移到块的终点。
- 如果块不为空，则控制流转移到语句列表。当且仅当控制流到达语句列表的终点时，控制流转移到块的终点。

如果块本身可达，则块的语句列表可达。

如果块为空或语句列表的终点可达，则块的终点可达。

包含一个或多个 yield 语句 (§13.15) 的块称为迭代器块。迭代器块用于将函数成员实现为迭代器 (§15.14)。迭代器块有额外的限制：

- 在迭代器块中出现 return 语句是编译时错误（但 yield return 语句是允许的）。
- 迭代器块包含不安全上下文 (§23.2) 是编译时错误。即使其声明嵌套在不安全上下文中，迭代器块始终定义安全上下文。

### 13.3.2 语句列表

语句列表由按顺序编写的一个或多个语句组成。语句列表出现在块 (§13.3) 和 switch_blocks (§13.8.3) 中。

```
statement_list
  : statement+
  ;
```

语句列表的执行是通过将控制流转移到第一个语句来进行的。当且仅当控制流到达某条语句的终点时，控制流转移到下一条语句。当且仅当控制流到达最后一个语句的终点时，控制流转移到语句列表的终点。

语句列表中的语句在满足以下任一条件时可达：

- 该语句是第一个语句且语句列表本身可达。
- 前一条语句的终点可达。
- 该语句是有标签的语句且标签被可达的 goto 语句引用。

如果列表中最后一个语句的终点可达，则语句列表的终点可达。

## 13.4 空语句

empty_statement 不执行任何操作。

```
empty_statement
  : ';'
  ;
```

当需要在需要语句的上下文中执行无操作时，使用空语句。

空语句的执行只是将控制流转移到该语句的终点。因此，如果空语句可达，则空语句的终点可达。

示例：空语句可用于编写具有空体的 while 语句时：

```
bool ProcessMessage() {...}
void ProcessMessages()
{
    while (ProcessMessage())
    ;
}
```

此外，空语句可用于在块的闭合 "}" 之前声明标签：

```
void F(bool done)
{
    ...
    if (done)
    {
        goto exit;
    }
    ...
    exit:
    ;
}
```

示例结束

## 13.5 带标签的语句

labeled_statement 允许语句前面加上标签。带标签的语句允许在块中使用，但不允许作为嵌入语句使用。

```
labeled_statement
    : identifier ':' statement
    ;
```

带标签的语句使用标识符给出的名称声明一个标签。标签的作用域是声明该标签的整个块，包括任何嵌套块。两个具有相同名称的标签具有重叠作用域是编译时错误。

标签可以在标签的作用域内从 goto 语句 (§13.10.4) 中引用。

> 注意：这意味着 goto 语句可以在块内和块外转移控制流，但永远不会进入块。 注意结束

标签有自己的声明空间，不会干扰其他标识符。

示例：示例

```
int F(int x)
{
    if (x >= 0)
    {
        goto x;
    }
}
```



```
x = -x;
x:
    return x;
}
```

是有效的，并且将名称 x 同时用作参数和标签。

*示例结束*

带标签语句的执行完全对应于该标签之后语句的执行。

除了正常控制流提供的可达性之外，如果某个标签被一个可达的 `goto` 语句引用，则该带标签语句是可达的，除非该 `goto` 语句位于某个 try_statement 的 try 块或 catch 块中，而该 try_statement 包含一个其终点不可达的 finally 块，并且该带标签语句位于该 try_statement 之外。

## 13.6 声明语句

### 13.6.1 概述

一个 declaration_statement 声明一个或多个局部变量、一个或多个局部常量，或一个局部函数。声明语句允许出现在块和 switch 块中，但不允许作为嵌入语句。

```
declaration_statement
  : local_variable_declaration ';'
  | local_constant_declaration ';'
  | local_function_declaration
  ;
```

局部变量使用 local_variable_declaration（§13.6.2）声明。局部常量使用 local_constant_declaration（§13.6.3）声明。局部函数使用 local_function_declaration（§13.6.4）声明。

所声明的名称被引入到最近的外围声明空间（§7.3）中。

### 13.6.2 局部变量声明

- 否则，如果作用域中存在名为 var 的类型，则 implicitly_typed_local_variable_declaration 不会被视作可能的匹配。

在 local_variable_declaration 中，每个变量均由一个声明符引入；对于隐式类型、显式类型和 ref 局部变量，该声明符分别是 implicitly_typed_local_variable_declarator、explicitly_typed_local_variable_declarator 或 ref_local_variable_declarator 之一。声明符定义所引入变量的名称（标识符）以及初始值（如果有）。

如果声明中有多个声明符，则按从左到右的顺序处理它们，包括任何初始化表达式（§9.4.4.5）。

> 注意：对于不作为 for_initializer（§13.9.4）或 resource_acquisition（§13.14）出现的 local_variable_declaration，这种从左到右的顺序等价于每个声明符分别位于一个单独的 local_variable_declaration 中。例如：

```
void F()
{
    int x = 1, y, z = x * 2;
}
```

等价于：

```
void F()
{
    int x = 1;
    int y;
    int z = x * 2;
}
```

注释结束

局部变量的值在表达式中通过 simple_name（§12.8.4）获取。在获取局部变量值的每个位置，该局部变量都应已明确赋值（§9.4）。由 local_variable_declaration 引入的每个局部变量初始为未赋值（§9.4.3）。如果声明符具有初始化表达式，则所引入的局部变量在该声明符末尾被归类为已赋值（§9.4.4.5）。

由 local_variable_declaration 引入的局部变量的作用域定义如下（§7.7）：

- 如果声明作为 for_initializer 出现，则作用域为 for_initializer、for_condition、for_iterator 和 embedded_statement（§13.9.4）；
- 如果声明作为 resource_acquisition 出现，则作用域为 using_statement 的语义等价展开的最外层块（§13.14）；
- 否则，作用域为声明所在的块。

### 13.6.2.2 隐式类型局部变量声明

```
implicitly_typed_local_variable_declaration
  : 'var' implicitly_typed_local_variable_declarator
  | ref_kind 'var' ref_local_variable_declarator
  ;

implicitly_typed_local_variable_declarator
: identifier '=' expression
;
```

implicitly_typed_local_variable_declaration 引入单个局部变量 identifier。expression 或 variable_reference 必须具有编译时类型 T。第一个备选项声明一个类型为 T、初始值为 expression 的变量。第二个备选项声明一个类型为 ref T、初始值为 ref variable_reference 的 ref 变量。

示例：

```
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
ref var j = ref i;
ref readonly var k = ref i;
```

上面的隐式类型局部变量声明完全等价于以下显式类型声明：

```
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
ref int j = ref i;
ref readonly int k = ref i;
```

以下是错误的隐式类型局部变量声明：

```
var x; // Error, no initializer to infer type from
var y = {1, 2, 3}; // Error, array initializer not permitted
var z = null; // Error, null does not have a type
var u = x => x + 1; // Error, anonymous functions do not have a type
var v = v++; // Error, initializer cannot refer to v itself
```

示例结束

### 13.6.2.3 显式类型局部变量声明

```
explicitly_typed_local_variable_declaration
: type explicitly_typed_local_variable_declarators
;

explicitly_typed_local_variable_declarators
: explicitly_typed_local_variable_declarator
(',' explicitly_typed_local_variable_declarator)*
;

explicitly_typed_local_variable_declarator
: identifier ('=' local_variable_initializer)?
;

local_variable_initializer
: expression
| array_initializer
;
```

explicitly_typed_local_variable_declaration 引入一个或多个具有指定类型的局部变量。

如果存在 local_variable_initializer，则其类型必须根据简单赋值（§12.21.2）或数组初始化（§17.7）的规则是适当的，并且其值被赋为该变量的初始值。

### 13.6.2.4 ref 局部变量声明

```
ref_local_variable_declaration
  : ref_kind type ref_local_variable_declarators
  ;

ref_local_variable_declarators
  : ref_local_variable_declarator (',' ref_local_variable_declarator)*
  ;

ref_local_variable_declarator
  : identifier '=' 'ref' variable_reference
  ;
```

初始化 variable_reference 必须具有类型 type，并满足与 ref 赋值（§12.21.3）相同的要求。

如果 ref_kind 为 ref readonly，则所声明的标识符是对被视为只读的变量的引用。否则，如果 ref_kind 为 ref，则所声明的标识符是对应可写变量的引用。

在使用 method_modifier async 声明的方法内，或在迭代器（§15.14）内，声明 ref 局部变量或 ref struct 类型的变量是编译时错误。

### 13.6.3 局部常量声明

local_constant_declaration 声明一个或多个局部常量。

```
local_constant_declaration
  : 'const' type constant_declarators
  ;

constant_declarators
  : constant_declarator (',' constant_declarator)*
  ;

constant_declarator
  : identifier '=' constant_expression
  ;
```

local_constant_declaration 的类型指定该声明所引入常量的类型。该类型后跟 constant_declarators 列表，其中每个声明符引入一个新常量。constant_declarator 由一个命名该常量的标识符、后跟一个 "=" 标记、再后跟一个给出该常量值的 constant_expression（§12.23）组成。

局部常量声明的类型和 constant_expression 应遵循与常量成员声明（§15.4）相同的规则。

```
    public static IEnumerable<char> AlphabetSubset(char start, char end)
    {
        if (start < 'a' || start > 'z')
        {
            throw new ArgumentOutOfRangeException(paramName: nameof(start),
                message: "start must be a letter");
        }
        if (end < 'a' || end > 'z')
        {
            throw new ArgumentOutOfRangeException(paramName: nameof(end),
                message: "end must be a letter");
        }
        if (end <= start)
        {
            throw new ArgumentException(
                $"{nameof(end)} must be greater than {nameof(start)}");
        }
        return AlphabetSubsetImplementation();

        IEnumerable<char> AlphabetSubsetImplementation()
        {
            for (var c = start; c < end; c++)
            {
                yield return c;
            }
        }
    }
```

*示例结束*

除非下文另有说明，所有语法元素的语义均与 *method_declaration*（§15.6.1）相同，但应理解为在局部函数而不是方法的上下文中阅读。

*local_function_declaration* 的标识符在其声明的块作用域内必须唯一，包括任何外围局部变量声明空间。这样做的一个结果是，不允许重载的 *local_function_declarations*。

*local_function_declaration* 可以包含一个 `async`（§15.15）修饰符和一个 `unsafe`（§23.1）修饰符。如果声明包含 `async` 修饰符，则返回类型应为 `void` 或 `<TaskType>` 类型（§15.15.1）。`unsafe` 修饰符使用包含它的词法作用域。`async` 修饰符不使用包含它的词法作用域。*type_parameter_list* 或 *formal_parameter_list* 包含特性是编译时错误。

局部函数在块作用域中声明，并且该函数可以捕获外围作用域中的变量。如果局部函数体读取某个捕获变量，但在每次调用该函数之前该变量未明确赋值，则是编译时错误。编译器应确定在返回时哪些变量已明确赋值（§9.4.4.33）。

当 `this` 的类型为 struct 类型时，局部函数体访问 `this` 是编译时错误。无论该访问是显式的（如 `this.x` 中）还是隐式的（如 `x` 中，其中 `x` 是该 struct 的实例成员），都是如此。此规则仅禁止此类访问，不影响成员查找是否得到该 struct 的成员。

局部函数体包含目标位于该局部函数体之外的 `goto` 语句、`break` 语句或 `continue` 语句，是编译时错误。




注：以上关于 `this` 和 `goto` 的规则与 §12.19.3 中匿名函数的规则相镜像。 *end note*

局部函数可在其声明之前的词法位置被调用。然而，如果函数在词法上在其局部函数中使用的变量的声明之前被声明，则是编译时错误（§7.7）。

对于局部函数而言，以与在任何封闭局部变量声明空间中声明的名称相同的名称声明参数、类型参数或局部变量是编译时错误。

局部函数体始终可达。如果局部函数声明的开始点可达，则局部函数声明的结束点可达。

示例：在下面的示例中，`L` 的函数体是可达的，即使 `L` 的开始点不可达。因为 `L` 的开始点不可达，所以 `L` 的结束点之后的语句不可达：

```csharp
class C
{
    int M()
    {
        L();
        return 1;

        // Beginning of L is not reachable
        int L()
        {
            // The body of L is reachable
            return 2;
        }
        // Not reachable, because beginning point of L is not reachable
        return 3;
    }
}
```

换句话说，局部函数声明的位置不会影响包含函数中任何语句的可达性。 *end example*

如果局部函数的参数类型为 `dynamic`，则要调用的函数必须在编译时解析，而不是运行时。

## 13.7 表达式语句

`expression_statement` 计算给定的表达式。表达式计算得到的值（如果有）将被丢弃。

```text
expression_statement
    : statement_expression ';'
    ;

statement_expression
    : null_conditional_invocation_expression
    | invocation_expression
    | object_creation_expression
    | assignment
    | post_increment_expression
    | post_decrement_expression
    | pre_increment_expression
    | pre_decrement_expression
    | await_expression
    ;
```

并非所有表达式都允许作为语句。

> *Note:* 特别是，像 `x + y` 和 `x == 1` 这样仅计算值（将被丢弃）的表达式，不允许作为语句。 *end note*

执行 `expression_statement` 会计算包含的表达式，然后将控制转移到 `expression_statement` 的结束点。如果该 `expression_statement` 可达，则其结束点可达。

## 13.8 选择语句

### 13.8.1 通用

选择语句根据某个表达式的值从多个可能的语句中选择一个执行。

```text
selection_statement
    : if_statement
    | switch_statement
    ;
```

### 13.8.2 if 语句

`if` 语句根据布尔表达式的值选择语句执行。

```text
if_statement
    : 'if' '(' boolean_expression ')' embedded_statement
    | 'if' '(' boolean_expression ')' embedded_statement
        'else' embedded_statement
    ;
```

`else` 部分与语法允许的最接近的在词法上前面的 `if` 相关联。

示例：因此，形式为的 `if` 语句

```csharp
if (x) if (y) F(); else G();
```

等价于

```csharp
if (x)
{
    if (y)
    {
        F();
    }
    else
    {
        G();
    }
}
```

*end example*

`if` 语句的执行如下：

- 计算 `boolean_expression`（§12.24）。
- 如果布尔表达式产生 `true`，则控制转移到第一个嵌入语句。当且仅当控制到达该语句的结束点时，控制转移到 `if` 语句的结束点。
- 如果布尔表达式产生 `false` 且存在 `else` 部分，则控制转移到第二个嵌入语句。当且仅当控制到达该语句的结束点时，控制转移到 `if` 语句的结束点。
- 如果布尔表达式产生 `false` 且不存在 `else` 部分，则控制转移到 `if` 语句的结束点。

`if` 语句的第一个嵌入语句可达的条件是 `if` 语句可达且布尔表达式不具有常量值 `false`。

如果存在，`if` 语句的第二个嵌入语句可达的条件是 `if` 语句可达且布尔表达式不具有常量值 `true`。

`if` 语句的结束点可达的条件是其至少一个嵌入语句的结束点可达。此外，如果 `if` 语句可达且布尔表达式不具有常量值 `true`，则没有 `else` 部分的 `if` 语句的结束点可达。

### 13.8.3 switch 语句

`switch` 语句选择与 switch 表达式的值对应的 switch 标签相关联的语句列表执行。

```text
switch_statement
    : 'switch' '(' expression ')' switch_block
    ;

switch_block
    : '{' switch_section* '}'
    ;

switch_section
    : switch_label+ statement_list
    ;

switch_label
    : 'case' pattern case_guard? ':'
    | 'default' ':'
    ;

case_guard
    : 'when' expression
    ;
```

`switch_statement` 由关键字 `switch` 组成，后跟一个括号表达式（称为 switch 表达式），后跟 `switch_block`。`switch_block` 由零个或多个 `switch_sections` 组成，用大括号括起来。每个 `switch_section` 由一个或多个 `switch_labels` 后跟一个 `statement_list`（§13.3.2）组成。包含 `case` 的每个 `switch_label` 都有一个关联的模式（§11），switch 表达式的值将与之进行测试。如果存在 `case_guard`，其表达式应可隐式转换为类型 `bool`，并且该表达式被评估为该 case 被视为满足的附加条件。

`switch` 语句的 **governing type** 由 switch 表达式确定。

- 如果 `switch` 表达式的类型为 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`bool`、`string`，或 *enum type*，或如果它是这些类型之一对应的可空值类型，则该类型是 `switch` 语句的 governing type。
- 否则，如果从 switch 表达式的类型到以下可能的 governing type 之一存在且仅存在一个用户定义隐式转换：`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`string`，或与这些类型之一对应的可空值类型，则转换后的类型是 `switch` 语句的 governing type。
- 否则，`switch` 语句的 governing type 是 switch 表达式的类型。如果不存在此类类型，则为错误。

`switch` 语句中最多只能有一个 `default` 标签。

如果任何 switch 标签的模式对输入表达式的类型不 *applicable*（§11.2.1），则为错误。

如果任何 switch 标签的模式被（§11.3）`switch` 语句中 earlier switch 标签的模式集合 *subsumed*，则为错误，这些 earlier 标签没有 case guard 或其 case guard 是值为 `true` 的常量表达式。

示例：

```csharp
switch (shape)
{
    case var x:
        break;
    case var _: // error: pattern subsumed, as previous case always matches
        break;
    default:
        break;  // warning: unreachable, all possible values already handled.
}
```

*end example*

`switch` 语句的执行如下：

- 计算 `switch` 表达式并将其转换为 governing type。
- 根据转换后的 `switch` 表达式的值转移控制：
    - 在同一 `switch` 语句中 `case` 标签集合中词法上第一个与 switch 表达式的值匹配的模式，并且其 guard 表达式不存在或求值为 `true`，会导致控制转移到匹配的 `case` 标签之后的语句列表。
    - 否则，如果存在 `default` 标签，则控制转移到 `default` 标签之后的语句列表。
    - 否则，控制转移到 `switch` 语句的结束点。

*Note:* 模式在运行时匹配的顺序未定义。编译器允许（但不是必须）按不同顺序匹配模式，并重用已匹配模式的结果来计算其他模式匹配的结果。尽管如此，编译器必须

确定在词法上第一个匹配表达式且其 guard 子句不存在或求值为 true 的模式。结束注记

如果 switch 部分的语句列表的终点可达，则会发生编译时错误。这被称为“no fall through”规则。

示例：示例

```
switch (i)
{
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

是有效的，因为没有 switch 部分具有可达的终点。与 C 和 C++ 不同，switch 部分的执行不允许“fall through”到下一个 switch 部分，并且示例

```
switch (i)
{
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
switch (i)
{
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

结束示例

在 switch_section 中允许使用多个标签。

示例：示例

```
switch (i)
{
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

是有效的。该示例不违反 "no fall through" 规则，因为标签 case 2: 和 default: 属于同一个 switch_section。

结束示例

注记：“no fall through”规则可防止在 C 和 C++ 中因意外省略 break 语句而发生的一类常见错误。例如，上述 switch 语句的部分可以反转而不影响语句的行为：

```
switch (i)
{
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

结束注记

注记：switch 部分的语句列表通常以 break、goto case 或 goto default 语句结束，但任何使语句列表终点不可达的构造都是允许的。例如，由布尔表达式 true 控制的 while 语句已知永远不会到达其终点。同样，throw 或 return 语句总是转移控制权到别处，永远不会到达其终点。因此，以下示例是有效的：

```
switch (i)
{
    case 0:
        while (true)
        {
            F();
        }
    case 1:
        throw new ArgumentException();
    case 2:
        return;
}
```

结束注记

示例：switch 语句的控制类型可以是 string 类型。例如：

```csharp
void DoCommand(string command)
{
    switch (command.ToLower())
    {
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

*结束示例*

*注记：* 类似于字符串相等运算符（§12.12.8），`switch` 语句是区分大小写的，并且只有当 switch 表达式字符串与某个 case 标签常量完全匹配时，才会执行给定的 switch 部分。 *结束注记* 当 `switch` 语句的控制类型为 `string` 或可空值类型时，值 `null` 允许作为 `case` 标签常量。

*switch块* 的 *语句列表*s 可能包含声明语句（§13.6）。在 switch 块中声明的局部变量或常量的作用域是 switch 块。

switch 标签可达的条件是以下至少一项为真：

- switch 表达式是常量值且满足以下任一条件
  - 该标签是其模式 *会匹配* (§11.2.1) 该值的 *case*，并且标签的 guard 不存在或不是值为 false 的常量表达式；或
  - 它是 *default* 标签，并且没有任何 switch 部分包含其模式会匹配该值且 guard 不存在或为值为 true 的常量表达式的 case 标签。
- switch 表达式不是常量值且满足以下任一条件
  - 该标签是 *case* 且没有 guard 或 guard 的值不是常量 false；或
  - 它是 *default* 标签且
    - switch 语句中没有 guard 或 guard 值为常量 true 的 case 中出现的模式集合，对于 switch 控制类型来说不是 *穷尽的* (§11.4)；或
    - switch 控制类型是可空类型，并且 switch 语句中没有 guard 或 guard 值为常量 true 的 case 中出现的模式集合不包含会匹配值 null 的模式。
- switch 标签被可达的 goto *case* 或 goto *default* 语句引用。

给定 switch 部分的语句列表可达的条件是 `switch` 语句可达并且该 switch 部分包含一个可达的 switch 标签。

switch 语句的终点可达的条件是 switch 语句可达并且以下至少一项为真：

- switch 语句包含一个可达的 break 语句，该语句退出 switch 语句。
- 没有 default 标签存在且满足以下任一条件
  - switch 表达式是非常量值，并且 switch 语句中没有 guard 或 guard 值为常量 true 的 case 中出现的模式集合，对于 switch 控制类型来说不是穷尽的（§11.4）。
  - switch 表达式是可空类型的非常量值，并且 switch 语句中没有 guard 或 guard 值为常量 true 的 case 中出现的模式不会匹配值 null。
  - switch 表达式是常量值，并且没有没有 guard 或 guard 为常量 true 的 case 标签会匹配该值。

示例：以下代码展示了 when 子句的简洁用法：

```
static object CreateShape(string shapeDescription)
{
    switch (shapeDescription)
    {
        case "circle":
            return new Circle(2);
        ...
        case var o when string.IsNullOrWhiteSpace(o):
            return null;
        default:
            return "invalid shape description";
    }
}
```

var case 匹配 null、空字符串或仅包含空白字符的任何字符串。结束示例

## 13.9 迭代语句

### 13.9.1 通用

迭代语句重复执行嵌入的语句。

```
iteration_statement
    : while_statement
    | do_statement
    | for_statement
    | foreach_statement
    ;
```

### 13.9.2 while 语句

while 语句有条件地执行嵌入的语句零次或多次。

A `while` statement is executed as follows:

- *布尔表达式* (§12.24) 被求值。
- 如果布尔表达式产生 `true`，控制权转移到嵌入的语句。当且仅当控制权到达嵌入语句的终点时（可能来自 `continue` 语句的执行），控制权转移到 `while` 语句的开头。
- 如果布尔表达式产生 `false`，控制权转移到 `while` 语句的终点。

在 `while` 语句的嵌入语句内，可以使用 `break` 语句 (§13.10.2) 将控制权转移到 `while` 语句的终点（从而结束嵌入语句的迭代），并且可以使用 `continue` 语句 (§13.10.3) 将控制权转移到嵌入语句的终点（从而执行 `while` 语句的另一次迭代）。

`while` 语句的嵌入语句可达的条件是 `while` 语句可达并且布尔表达式不具有常量值 `false`。

`while` 语句的终点可达的条件是以下至少一项为真：

- `while` 语句包含一个可达的 `break` 语句，该语句退出 `while` 语句。
- `while` 语句可达并且布尔表达式不具有常量值 `true`。

### 13.9.3 do 语句

`do` 语句有条件地执行嵌入的语句一次或多次。

```
do_statement
    : 'do' embedded_statement 'while' '(' boolean_expression ')' ';'
    ;
```

`do` 语句的执行如下：

- 控制权转移到嵌入的语句。
- 当且仅当控制权到达嵌入语句的终点时（可能来自 `continue` 语句的执行），*布尔表达式* (§12.24) 被求值。如果布尔表达式产生 `true`，控制权转移到 `do` 语句的开头。否则，控制权转移到 `do` 语句的终点。

在 `do` 语句的嵌入语句内，可以使用 `break` 语句 (§13.10.2) 将控制权转移到 `do` 语句的终点（从而结束嵌入语句的迭代），并且可以使用 `continue` 语句 (§13.10.3) 将控制权转移到嵌入语句的终点（从而执行 `do` 语句的另一次迭代）。

`do` 语句的嵌入语句可达的条件是 `do` 语句可达。

`do` 语句的终点可达的条件是以下至少一项为真：

- `do` 语句包含一个可达的 `break` 语句，该语句退出 `do` 语句。
- 嵌入语句的终点可达并且布尔表达式不具有常量值 `true`。



## 13.9.4 for 语句

for 语句会求值一系列初始化表达式，然后当条件为 true 时，重复执行嵌入语句并求值一系列迭代表达式。

```
    for_statement
        : 'for' '(' for_initializer? ';' for_condition? ';' for_iterator? ')'
          embedded_statement
        ;

    for_initializer
        : local_variable_declaration
        | statement_expression_list
        ;

    for_condition
        : boolean_expression
        ;

    for_iterator
        : statement_expression_list
        ;

    statement_expression_list
        : statement_expression (',' statement_expression)*
        ;
```

如果存在 *for_initializer*，则它由 *local_variable_declaration*（§13.6.2）或以逗号分隔的 *statement_expressions*（§13.7）列表组成。由 *for_initializer* 声明的局部变量的作用域是 *for_initializer*、*for_condition*、*for_iterator* 和 *embedded_statement*。

如果存在 *for_condition*，则它应为 *boolean_expression*（§12.24）。

如果存在 *for_iterator*，则它由以逗号分隔的 *statement_expressions*（§13.7）列表组成。

*for* 语句的执行方式如下：

- 如果存在 *for_initializer*，则按书写顺序执行变量初始化器或语句表达式。此步骤仅执行一次。
- 如果存在 *for_condition*，则对其进行求值。
- 如果不存在 *for_condition*，或者求值结果为 `true`，则控制转移到嵌入语句。当控制到达嵌入语句的结束点（可能因执行 `continue` 语句而到达）时，将按顺序对 *for_iterator* 的表达式（如果有）求值，然后执行另一次迭代，并从上述步骤中对 *for_condition* 求值开始。
- 如果存在 *for_condition* 且求值结果为 `false`，则控制转移到 *for* 语句的结束点。

在 *for* 语句的嵌入语句中，可以使用 `break` 语句（§13.10.2）将控制转移到 *for* 语句的结束点（从而结束嵌入语句的迭代），也可以使用 `continue` 语句（§13.10.3）将控制转移到嵌入语句的结束点（从而执行 *for_iterator* 并执行 *for* 语句的另一次迭代，从 *for_condition* 开始）。

如果下列条件之一为 true，则 *for* 语句的嵌入语句可到达：

- for 语句可到达且不存在 for_condition。
- for 语句可到达，存在 for_condition，且其常量值不为 false。

如果下列条件至少之一为 true，则 for 语句的结束点可到达：

- for 语句包含一个可到达的 break 语句，该语句退出 for 语句。
- for 语句可到达，存在 for_condition，且其常量值不为 true。

## 13.9.5 foreach 语句

foreach 语句枚举集合的元素，并为集合中的每个元素执行嵌入语句。

```
foreach_statement
    : 'foreach' '(' ref_kind? local_variable_type identifier 'in'
      expression ')' embedded_statement
    ;
```

foreach 语句的 local_variable_type 和 identifier 声明该语句的迭代变量。如果 var 标识符作为 local_variable_type 给出，并且作用域中没有名为 var 的类型，则该迭代变量称为隐式类型化迭代变量，其类型按以下指定视为 foreach 语句的元素类型。

如果 foreach_statement 同时包含 ref 和 readonly，或二者都不包含，则迭代变量表示一个被视为只读的变量。否则，如果 foreach_statement 包含 ref 但不包含 readonly，则迭代变量表示一个应为可写的变量。

迭代变量对应于一个局部变量，其作用域延伸到嵌入语句。在执行 foreach 语句期间，迭代变量表示当前正在对其执行迭代的集合元素。如果迭代变量表示只读变量，则当嵌入语句试图修改它（通过赋值或 ++ 和 -- 运算符）或将其作为 ref 或 out 参数传递时，会发生编译时错误。

为简洁起见，下文中的 IEnumerable、IEnumerator、IEnumerable<T> 和 IEnumerator<T> 指 System.Collections 和 System.Collections.Generic 命名空间中的对应类型。

foreach 语句的编译时处理首先确定表达式的集合类型、枚举器类型和迭代类型。确定过程如下：

- 如果表达式的类型 X 是数组类型，则存在从 X 到 IEnumerable 接口的隐式引用转换（因为 System.Array 实现此接口）。集合类型是 IEnumerable 接口，枚举器类型是 IEnumerator 接口，迭代类型是数组类型 X 的元素类型。
- 如果表达式的类型 X 是 dynamic，则存在从表达式到 IEnumerable 接口的隐式转换（§10.2.10）。集合类型是 IEnumerable 接口，枚举器类型是 IEnumerator 接口。如果 var 标识符作为 local_variable_type 给出，则迭代类型是 dynamic，否则是 object。
- 否则，确定类型 X 是否具有合适的 GetEnumerator 方法：
  - 在类型 X 上使用标识符 GetEnumerator 且不带类型实参执行成员查找。如果成员查找未产生匹配、产生二义性，或产生的匹配不是方法组，则按下文所述检查可枚举接口。建议在成员查找产生除方法组或无匹配之外的任何结果时发出警告。
  - 使用得到的方法组和空实参列表执行重载决策。如果重载决策导致没有适用方法、导致二义性，或导致单个最佳方法但该方法为静态方法或不是公共方法，则按下文所述检查可枚举接口。建议在重载决策产生除无歧义的公共实例方法或无适用方法之外的任何结果时发出警告。
  - 如果 GetEnumerator 方法的返回类型 E 不是类、结构或接口类型，则产生错误，并且不采取进一步步骤。
  - 在 E 上使用标识符 Current 且不带类型实参执行成员查找。如果成员查找未产生匹配、结果为错误，或结果为除允许读取的公共实例属性之外的任何内容，则产生错误，并且不采取进一步步骤。
  - 在 E 上使用标识符 MoveNext 且不带类型实参执行成员查找。如果成员查找未产生匹配、结果为错误，或结果为除方法组之外的任何内容，则产生错误，并且不采取进一步步骤。
  - 使用空实参列表对该方法组执行重载决策。如果重载决策导致没有适用方法、导致二义性，或导致单个最佳方法但该方法为静态方法、不是公共方法，或其返回类型不是 bool，则产生错误，并且不采取进一步步骤。
  - 集合类型是 X，枚举器类型是 E，迭代类型是 Current 属性的类型。Current 属性可以包含 ref 修饰符；在这种情况下，返回的表达式是 variable_reference（§9.5），并且可选为只读。
- 否则，检查可枚举接口：
  - 如果在所有存在从 X 到 IEnumerable<T_i> 的隐式转换的类型 T_i 中，存在唯一类型 T，使得 T 不是 dynamic，并且对于所有其他 T_i，都存在从 IEnumerable<T_i> 到 IEnumerable<T> 的隐式转换，则集合类型是接口 IEnumerable<T>，枚举器类型是接口 IEnumerator<T>，迭代类型是 T。
  - 否则，如果存在多个这样的类型 T，则产生错误，并且不采取进一步步骤。
  - 否则，如果存在从 X 到 System.Collections.IEnumerable 接口的隐式转换，则集合类型是此接口，枚举器类型是接口 System.Collections.IEnumerator，迭代类型是 object。
  - 否则，产生错误，并且不采取进一步步骤。

上述步骤如果成功，将明确产生集合类型 C、枚举器类型 E 以及迭代类型 T、ref T 或 ref readonly T。形式如下的 foreach 语句

`foreach (V v in x)` «embedded_statement»

等价于：

```
{
    E e = ((C)(x)).GetEnumerator();
    try
    {
```


```
while (e.MoveNext())
{
    V v = (V)(T)e.Current;
    «embedded_statement»
}
finally
{
    ... // Dispose e
}
```

变量 e 对于表达式 x、嵌入式语句或程序中的任何其他源代码既不可见也不可访问。变量 v 在嵌入式语句中是只读的。如果不存在从 T（迭代类型）到 V（foreach 语句中的局部变量类型）的显式转换（§10.3），则会产生错误，并且不再执行后续步骤。

当迭代变量是引用变量（§9.7）时，形式为

```
foreach (ref V v in x) «embedded_statement»
```

的 foreach 语句等价于：

```
{
    E e = ((C)(x)).GetEnumerator();
    try
    {
        while (e.MoveNext())
        {
            ref V v = ref e.Current;
            «embedded_statement»
        }
    }
    finally
    {
        ... // Dispose e
    }
}
```

变量 e 对于表达式 x、嵌入式语句或程序中的任何其他源代码既不可见也不可访问。引用变量 v 在嵌入式语句中是可读写的，但不得对 v 进行 ref 重新赋值（§12.21.3）。如果不存在从 T（迭代类型）到 V（foreach 语句中的局部变量类型）的标识转换（§10.2.2），则会产生错误，并且不再执行后续步骤。

形式为 `foreach (ref readonly V v in x) «embedded_statement»` 的 foreach 语句具有类似的等价形式，但引用变量 v 在嵌入式语句中是 ref readonly 的，因此既不能进行 ref 重新赋值，也不能重新赋值。

注意：如果 x 的值为 null，则在运行时抛出 System.NullReferenceException。结束注意

允许实现以不同的方式实现给定的 foreach_statement；例如，出于性能原因，只要行为与上述展开一致即可。

v 在 while 循环内的位置对于嵌入式语句中出现的任何匿名函数如何捕获（§12.19.6.2）它非常重要。

### 示例：

```
int[] values = { 7, 9, 13 };
Action f = null;
foreach (var value in values)
{
    if (f == null)
    {
        f = () => Console.WriteLine("First value: " + value);
    }
}
f();
```

如果在展开形式中 v 是在 while 循环外部声明的，那么它将在所有迭代之间共享，并且循环结束后它的值将是最终值 13，而这正是调用 f 时打印出的值。相反，由于每次迭代都有自己的变量 v，f 在第一次迭代中捕获的那个 v 将继续保存值 7，因此打印出的结果将是 7。（注意，早期版本的 C# 是在 while 循环外部声明 v 的。）
结束示例

finally 块的主体按照以下步骤构造：

- 如果存在从 E 到 System.IDisposable 接口的隐式转换，则
  - 如果 E 是不可为 null 的值类型，则 finally 子句展开为以下语义等效形式：
  - 否则，finally 子句展开为以下语义等效形式：
    但如果 E 是值类型，或是实例化为值类型的类型参数，则将 e 转换为 System.IDisposable 不得导致装箱发生。
- 否则，如果 E 是密封类型，则 finally 子句展开为一个空块：
- 否则，finally 子句展开为：

```
finally
{
    ((System.IDisposable)e).Dispose();
}
```

```
finally
{
    System.IDisposable d = e as System.IDisposable;
    if (d != null)
    {
        d.Dispose();
    }
}
```

```
finally {}
```

局部变量 `d` 对任何用户代码既不可见也不可访问。特别是，它不会与范围包含 `finally` 块的任何其他变量冲突。

`foreach` 遍历数组元素的顺序如下：对于一维数组，元素按索引递增顺序遍历，从索引 0 开始，到索引 `Length – 1` 结束。对于多维数组，元素的遍历顺序是：最右侧维度的索引先递增，然后是左侧的下一个维度，以此类推，直到最左侧。

*示例：* 下面的示例按元素顺序打印出一个二维数组中的每个值：

```csharp
class Test
{
    static void Main()
    {
        double[,] values =
        {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };
        foreach (double elementValue in values)
        {
            Console.Write($"{elementValue} ");
        }
        Console.WriteLine();
    }
}
```

产生的输出如下：

```
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

*结束示例*

*示例：* 在下面的示例中

```csharp
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers)
{
    Console.WriteLine(n);
}
```

`n` 的类型被推断为 `int`，即 `numbers` 的迭代类型。

*结束示例*

## 13.10 跳转语句

### 13.10.1 一般

跳转语句无条件地转移控制。

```text
jump_statement
    : break_statement
    | continue_statement
    | goto_statement
    | return_statement
    | throw_statement
    ;
```

跳转语句将控制转移到的位置称为该跳转语句的目标。

当跳转语句出现在块内，并且该跳转语句的目标在该块之外时，称该跳转语句退出该块。虽然跳转语句可以将控制转移出块，但它永远不能将控制转入块。

跳转语句的执行会因存在中间的 try 语句而变得复杂。在没有此类 try 语句的情况下，跳转语句无条件地将控制从该跳转语句转移到其目标。在存在此类中间 try 语句的情况下，执行更为复杂。如果跳转语句退出了一个或多个带有相关 finally 块的 try 块，控制将首先转移到最内层 try 语句的 finally 块。当控制到达某个 finally 块的终点时（如果确实到达），控制将转移到下一个外层 try 语句的 finally 块。重复此过程，直到所有中间的 try 语句的 finally 块都已执行完毕。

示例：在下面的代码中

```csharp
class Test
{
    static void Main()
    {
        while (true)
        {
            try
            {
                try
                {
                    Console.WriteLine("Before break");
                    break;
                }
                finally
                {
                    Console.WriteLine("Innermost finally block");
                }
            }
            finally
            {
                Console.WriteLine("Outermost finally block");
            }
        }
        Console.WriteLine("After break");
    }
}
```

与两个 try 语句关联的 finally 块会在控制转移到跳转语句的目标之前执行。产生的输出如下：

```
Before break
Innermost finally block
Outermost finally block
After break
```

*结束示例*

### 13.10.2 break 语句

```
break_statement
    : 'break' ';'
    ;
```

`break` 语句的目标是最近的外层 `switch`、`while`、`do`、`for` 或 `foreach` 语句的终点。如果 `break` 语句没有被 `switch`、`while`、`do`、`for` 或 `foreach` 语句包围，则会发生编译时错误。

当多个 `switch`、`while`、`do`、`for` 或 `foreach` 语句相互嵌套时，`break` 语句仅适用于最内层的语句。要跨多个嵌套级别转移控制，应使用 `goto` 语句（§13.10.4）。

`break` 语句不能退出 `finally` 块（§13.11）。当 `break` 语句出现在 `finally` 块内时，`break` 语句的目标必须在同一个 `finally` 块内；否则会发生编译时错误。

`break` 语句的执行方式如下：

- 如果 `break` 语句退出了一个或多个带有相关 `finally` 块的 `try` 块，控制将首先转移到最内层 `try` 语句的 `finally` 块。当控制到达某个 `finally` 块的终点时（如果确实到达），控制将转移到下一个外层 `try` 语句的 `finally` 块。重复此过程，直到所有中间的 `try` 语句的 `finally` 块都已执行完毕。
- 控制被转移到 `break` 语句的目标。

由于 `break` 语句无条件地将控制转移到别处，因此 `break` 语句的终点永远不可到达。

### 13.10.3 continue 语句

`continue` 语句开始最近的外层 `while`、`do`、`for` 或 `foreach` 语句的一次新迭代。

```
continue_statement
    : 'continue' ';'
    ;
```

`continue` 语句的目标是最近的外层 `while`、`do`、`for` 或 `foreach` 语句的嵌入式语句的终点。如果 `continue` 语句没有被 `while`、`do`、`for` 或 `foreach` 语句包围，则会发生编译时错误。

当多个 `while`、`do`、`for` 或 `foreach` 语句相互嵌套时，`continue` 语句仅适用于最内层的语句。要跨多个嵌套级别转移控制，应使用 `goto` 语句（§13.10.4）。

`continue` 语句不能退出 `finally` 块（§13.11）。当 `continue` 语句出现在 `finally` 块内时，`continue` 语句的目标必须在同一个 `finally` 块内；否则会发生编译时错误。

`continue` 语句的执行方式如下：

- 如果 `continue` 语句退出了一个或多个带有相关 `finally` 块的 `try` 块，控制将首先转移到最内层 `try` 语句的 `finally` 块。当控制到达某个 `finally` 块的终点时（如果确实到达），控制将转移到下一个外层 `try` 语句的 `finally` 块。重复此过程，直到所有中间的 `try` 语句的 `finally` 块都已执行完毕。




- 控制权被转移到 continue 语句的目标。

由于 continue 语句无条件地将控制转移到其他地方，continue 语句的终结点永远不可达。

## 13.10.4 goto 语句

goto 语句将控制转移到一个由标签标记的语句。

```
goto_statement
  : 'goto' identifier ':'
  | 'goto' 'case' constant_expression ';'
  | 'goto' 'default' ';'
  ;
```

goto 标识符语句的目标是带有给定标签的带标签语句。如果当前函数成员中不存在具有给定名称的标签，或者 goto 语句不在该标签的作用域内，则会发生编译时错误。

注意：此规则允许使用 goto 语句将控制转移出嵌套作用域，但不允许转入嵌套作用域。在以下示例中：

```
class Test
{
    static void Main(string[] args)
    {
        string[,] table =
        {
            {"Red", "Blue", "Green"},
            {"Monday", "Wednesday", "Friday"}
        };
        foreach (string str in args)
        {
            int row, colm;
            for (row = 0; row <= 1; ++row)
            {
                for (colm = 0; colm <= 2; ++colm)
                {
                    if (str == table[row,colm])
                    {
                        goto done;
                    }
                }
                Console.WriteLine($"{str} not found");
                continue;
            done:
                Console.WriteLine($"Found {str} at [{row}][{colm}]");
            }
        }
    }
}
```

使用了一条 goto 语句将控制转移出嵌套作用域。

注记结束。

goto case 语句的目标是最近封闭的 switch 语句（§13.8.3）中的语句列表，该语句列表包含一个具有给定常量值的常量模式且没有保护（guard）的 case 标签。如果 goto case 语句没有被 switch 语句包围，如果最近的封闭 switch 语句不包含这样的 case，或者如果 constant_expression 不能隐式转换（§10.2）为最近封闭 switch 语句的管理类型（governing type），则会发生编译时错误。

goto default 语句的目标是最近封闭的 switch 语句（§13.8.3）中包含 default 标签的语句列表。如果 goto default 语句没有被 switch 语句包围，或者最近的封闭 switch 语句不包含 default 标签，则会发生编译时错误。

goto 语句不能退出 finally 块（§13.11）。当 goto 语句出现在 finally 块内时，goto 语句的目标必须位于同一个 finally 块内，否则会发生编译时错误。

goto 语句的执行过程如下：

- 如果 goto 语句退出一个或多个带有关联 finally 块的 try 块，控制首先被转移到最内层 try 语句的 finally 块。当控制到达 finally 块的终结点时（如果到达），控制被转移到下一个封闭 try 语句的 finally 块。此过程重复执行，直到所有中间 try 语句的 finally 块都已执行完毕。
- 控制被转移到 goto 语句的目标。

由于 goto 语句无条件地将控制转移到其他地方，goto 语句的终结点永远不可达。

## 13.10.5 return 语句

return 语句将控制权返回到 return 语句所在函数成员的当前调用方，并可以选择返回一个值或一个 variable_reference（§9.5）。

```
return_statement
  : 'return' ';'
  | 'return' expression ';'
  | 'return' 'ref' variable_reference ';'
  ;
```

不带表达式的 return_statement 称为 return-no-value；包含 ref 表达式的称为 return-by-ref；仅包含表达式的称为 return-by-value。

从声明为 returns-by-value 或 returns-by-ref（§15.6.1）的方法中使用 return-no-value 是编译时错误。

从声明为 returns-no-value 或 returns-by-value 的方法中使用 return-by-ref 是编译时错误。

从声明为 returns-no-value 或 returns-by-ref 的方法中使用 return-by-value 是编译时错误。

如果 expression 不是 variable_reference，或者引用的变量的 ref-safe-context 不是 caller-context（§9.7.2），则使用 return-by-ref 是编译时错误。

此规则同样适用于构造函数、静态构造函数和终结器。returns-by-ref 的函数成员不计算值。

对于 return-by-value，从 expression 的类型到包含该函数成员的有效返回类型（§15.6.11）必须存在隐式转换（§10.2）。对于 return-by-ref，expression 的类型与包含该函数成员的有效返回类型之间必须存在恒等转换（identity conversion）（§10.2.2）。

return 语句也可以用在匿名函数表达式（§12.19）的主体中，并参与确定这些函数存在哪些转换（§10.7.1）。

return 语句出现在 finally 块（§13.11）中是编译时错误。

return 语句的执行过程如下：

- 对于 return-by-value，计算 expression，并通过隐式转换将其值转换为包含函数的有效返回类型。转换结果成为函数产生的结果值。对于 return-by-ref，expression 所指定的变量或属性的引用成为函数产生的结果。该结果是一个变量。如果封闭方法的 return-by-ref 包含 readonly，则结果变量是只读的。
- 如果 return 语句被一个或多个带有关联 finally 块的 try 或 catch 块包围，控制首先被转移到最内层 try 语句的 finally 块。当控制到达 finally 块的终结点时（如果到达），控制被转移到下一个封闭 try 语句的 finally 块。此过程重复执行，直到所有封闭 try 语句的 finally 块都已执行完毕。
- 如果包含函数不是异步函数，则控制连同结果值（如果有）一起返回到包含函数的调用方。
- 如果包含函数是异步函数，则控制返回到当前调用方，并且结果值（如果有）按（§15.15.3）中的描述记录在返回任务（return task）中。

由于 return 语句无条件地将控制转移到其他地方，return 语句的终结点永远不可达。

## 13.10.6 throw 语句

throw 语句抛出异常。

```
throw_statement
  : 'throw' expression? ';'
  ;
```

带表达式的 throw 语句抛出通过计算表达式产生的异常。表达式必须可隐式转换为 System.Exception，并且表达式计算结果在抛出前会被转换为 System.Exception。如果转换结果为 null，则改为抛出 System.NullReferenceException。

不带表达式的 throw 语句只能在 catch 块中使用，在这种情况下，该语句重新抛出该 catch 块当前正在处理的异常。

由于 throw 语句无条件地将控制转移到其他地方，throw 语句的终结点永远不可达。

当抛出异常时，控制被转移到可处理该异常的封闭 try 语句中的第一个 catch 子句。从异常抛出点到将控制转移到合适的异常处理程序的过程称为异常传播（exception propagation）。

异常传播包括重复评估以下步骤，直到找到与异常匹配的 catch 子句。在此描述中，抛出点（throw point）最初是异常被抛出的位置。

- 在当前函数成员中，检查每个包围抛出点的 try 语句。对于每个语句 S，从最内层的 try 语句开始，一直到最外层的 try 语句，评估以下步骤：
  - 如果 S 的 try 块包围抛出点，并且 S 有一个或多个 catch 子句，则按出现顺序检查 catch 子句，以找到适合该异常的处理程序。第一个指定异常类型 T（或一个在运行时表示异常类型 T 的类型参数）且 E 的运行时类型派生自 T 的 catch 子句被视为匹配。如果该子句包含异常筛选器（exception filter），则将异常对象分配给异常变量，并计算异常筛选器。当 catch 子句包含异常筛选器时，如果异常筛选器计算结果为 true，则认为该 catch 子句匹配。通用 catch（§13.11）子句被视为与任何异常类型匹配。如果找到匹配的 catch 子句，则通过将控制转移到该 catch 子句的块来完成异常传播。
  - 否则，如果 S 的 try 块或 catch 块包围抛出点，并且 S 有 finally 块，则将控制转移到 finally 块。如果 finally 块抛出另一个异常，则终止对当前异常的处理。否则，当控制到达 finally 块的终结点时，继续处理当前异常。
- 如果在当前函数调用中未找到异常处理程序，则终止函数调用，并发生以下情况之一：
  - 如果当前函数是非异步的，则对函数的调用方重复上述步骤，抛出点对应于调用该函数成员的语句。
  - 如果当前函数是异步且返回任务的，则异常记录在返回任务中，该任务按 §15.15.3 中的描述进入 faulted 或 cancelled 状态。
  - 如果当前函数是异步且返回 void 的，则按 §15.15.4 中的描述通知当前线程的同步上下文（synchronization context）。
- 如果异常处理终止了当前线程中的所有函数成员调用，表明该线程没有用于该异常的处理程序，则该线程本身被终止。这种终止的影响由实现定义。

## 13.11 try 语句

try 语句提供了一种机制，用于捕获在执行块期间发生的异常。此外，try 语句能够指定一个代码块，当控制离开 try 语句时，该代码块总是被执行。

```
try_statement
: 'try' block catch_clauses
| 'try' block catch_clauses? finally_clause
;
```

```
catch_clauses
: specific_catch_clause+
| specific_catch_clause* general_catch_clause
```



```
specific_catch_clause
    : 'catch' exception_specifier exception_filter? block
    | 'catch' exception_filter block
    ;

exception_specifier
    : '(' 'type' identifier? ')'
    ;

exception_filter
    : 'when' '(' boolean_expression ')'
    ;

general_catch_clause
    : 'catch' block
    ;

finally_clause
    : 'finally' block
    ;
```

一个 *try 语句* 由关键字 *try* 后跟一个 *块*，然后是零个或多个 *catch 子句*，然后是一个可选的 *finally 子句*。必须至少有一个 *catch 子句* 或一个 *finally 子句*。

在 *异常说明符* 中，*类型*，或如果它是 *类型参数* 则其有效基类，必须是 System.Exception 或派生自它的类型。

当 *catch* 子句同时指定了 *类类型* 和 *标识符* 时，会声明一个具有给定名称和类型的异常变量。异常变量被引入到 *特定 catch 子句* (§7.3) 的声明空间中。在执行 *异常筛选器* 和 *catch* 块期间，异常变量表示当前正在处理的异常。对于确定性赋值检查而言，异常变量在其整个作用域内被视为已明确赋值。

除非 *catch* 子句包含异常变量名，否则无法在 *筛选器* 和 *catch* 块中访问异常对象。

既不指定异常类型也不指定异常变量名的 *catch* 子句称为通用 *catch* 子句。*try* 语句只能有一个通用 *catch* 子句，如果存在，则它必须是最后一个 *catch* 子句。

*注意：某些编程语言可能支持无法表示为派生自 System.Exception 的对象的异常，尽管此类异常永远不可能由 C# 代码生成。通用 catch 子句可能用于捕获此类异常。因此，通用 catch 子句在语义上不同于指定类型 System.Exception 的子句，因为前者也可能捕获来自其他语言的异常。结束注意*

为了定位异常的处理程序，*catch* 子句按词法顺序检查。如果 *catch* 子句指定了类型但没有异常筛选器，则对于同一 *try* 语句的后续 *catch* 子句指定与该类型相同或派生自该类型的类型是一个编译时错误。

*注意：如果没有此限制，就可能编写不可达的 catch 子句。结束注意*

在 catch 块内，可以使用不带表达式的 throw 语句 (§13.10.6) 重新抛出由 catch 块捕获的异常。对异常变量的赋值不会改变被重新抛出的异常。

示例：在以下代码中

```
class Test
{
    static void F()
    {
        try
        {
            G();
        }
        catch (Exception e)
        {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw; // re-throw
        }
    }

    static void G() => throw new Exception("G");

    static void Main()
    {
        try
        {
            F();
        }
        catch (Exception e)
        {
            Console.WriteLine("Exception in Main: " + e.Message);
        }
    }
}
```

方法 F 捕获异常，将一些诊断信息写入控制台，修改异常变量，并重新抛出异常。被重新抛出的异常是原始异常，因此产生的输出为：

Exception in F: G
Exception in Main: G

如果第一个 catch 块抛出 e 而不是重新抛出当前异常，则产生的输出如下：

Exception in F: G
Exception in Main: F

结束示例

如果 break、continue 或 goto 语句将控制权转移出 finally 块，则为编译时错误。当 break、continue 或 goto 语句出现在 finally 块中时，该语句的目标必须在同一 finally 块内，否则会发生编译时错误。

在 finally 块中出现 return 语句是编译时错误。

当执行到达 try 语句时，控制权转移到 try 块。如果控制权在未传播异常的情况下到达 try 块的终点，则如果存在 finally 块，则控制权转移到 finally 块。如果不存在 finally 块，则控制权转移到 try 语句的终点。

如果已传播异常，则如果有 catch 子句，则按词法顺序检查以寻找异常的第一个匹配项。寻找匹配的 catch 子句的过程将继续所有封闭块，如 §13.10.6 中所述。如果异常类型匹配任何 exception_specifier 且任何 exception_filter 为 true，则 catch 子句为匹配项。没有 exception_specifier 的 catch 子句匹配任何异常类型。当 exception_specifier 指定异常类型或异常类型的基类型时，异常类型匹配 exception_specifier。如果子句包含异常筛选器，则异常对象被赋给异常变量，并评估异常筛选器。

如果已传播异常并且找到了匹配的 catch 子句，则控制权转移到第一个匹配的 catch 块。如果控制权在未传播异常的情况下到达 catch 块的终点，则如果存在 finally 块，则控制权转移到 finally 块。如果不存在 finally 块，则控制权转移到 try 语句的终点。如果异常已从 catch 块传播，则如果存在 finally 块，则控制权转移到 finally 块。异常传播到下一个封闭的 try 语句。

如果已传播异常，并且未找到匹配的 catch 子句，则控制权转移到 finally 块（如果存在）。异常传播到下一个封闭的 try 语句。

finally 块的语句总是会在控制权离开 try 语句时执行。无论控制转移是由于正常执行、执行 break、continue、goto 或 return 语句的结果，还是由于将异常传播出 try 语句的结果，都为真。如果控制权在未传播异常的情况下到达 finally 块的终点，则控制权转移到 try 语句的终点。

如果在 finally 块执行期间抛出异常，并且未在同一 finally 块内捕获，则异常传播到下一个封闭的 try 语句。如果另一个异常正在被传播过程中，则该异常丢失。异常传播的过程在 throw 语句 (§13.10.6) 的描述中进一步讨论。

示例：在以下代码中

```
public class Test
{
    static void Main()
    {
        try
        {
            Method();
        }
        catch (Exception ex) when (ExceptionFilter(ex))
        {
            Console.WriteLine("Catch");
        }
    }

    bool ExceptionFilter(Exception ex)
    {
        Console.WriteLine("Filter");
        return true;
    }
}
```

```csharp
static void Method()
{
    try
    {
        throw new ArgumentException();
    }
    finally
    {
        Console.WriteLine("Finally");
    }
}
```

方法 Method 抛出异常。第一个操作是检查封闭的 catch 子句，执行任何异常筛选器。然后，Method 中的 finally 子句在控制权转移到封闭的匹配 catch 子句之前执行。 resulting output is：

Filter
Finally
Catch

*结束示例*

如果 try 语句可达，则 try 语句的 try 块可达。

如果 try 语句可达，则 try 语句的 catch 块可达。

如果 try 语句可达，则 try 语句的 finally 块可达。

如果以下两点均为真，则 try 语句的终点可达：

- try 块的终点可达或至少一个 catch 块的终点可达。
- 如果存在 finally 块，则 finally 块的终点可达。

## 13.12 checked 和 unchecked 语句

checked 和 unchecked 语句用于控制整数类型算术运算和转换的溢出检查上下文。

```
checked_statement
    : 'checked' block
    ;

unchecked_statement
    : 'unchecked' block
    ;
```

checked 语句导致块中的所有表达式在 checked 上下文中求值，而 unchecked 语句导致块中的所有表达式在 unchecked 上下文中求值。

checked 和 unchecked 语句与 checked 和 unchecked 运算符 (§12.8.19) 精确等效，只是它们操作的是块而不是表达式。

## 13.13 lock 语句

lock 语句为给定对象获取互斥锁，执行语句，然后释放锁。



```
lock_statement
: 'lock' '(' expression ')' embedded_statement
;
```

lock 语句的表达式应表示一个已知为引用类型的值。对 lock 语句的表达式绝不会执行隐式装箱转换（§10.2.9），因此，如果该表达式表示 value_type 的值，则为编译时错误。

形式如下的 lock 语句

```
lock (x) ...
```

其中 x 是 reference_type 的表达式，完全等价于：

```
bool __lockWasTaken = false;
try
{
    System.Threading.Monitor.Enter(x, ref __lockWasTaken);
    ...
}
finally
{
    if (__lockWasTaken)
    {
        System.Threading.Monitor.Exit(x);
    }
}
```

只不过 x 只计算一次。

当持有互斥锁时，在同一执行线程中执行的代码也可以获取和释放该锁。但是，在其他线程中执行的代码会被阻止获取该锁，直到该锁被释放。

## 13.14 using 语句

using 语句获取一个或多个资源，执行一个语句，然后释放该资源。

```
using_statement
: 'using' '(' resource_acquisition ')' embedded_statement
;

resource_acquisition
: local_variable_declaration
| expression
;
```

资源是实现 System.IDisposable 接口的类或结构，该接口包含一个名为 Dispose 的无参数方法。正在使用资源的代码可以调用 Dispose，以指示不再需要该资源。

如果 resource_acquisition 的形式为 local_variable_declaration，则 local_variable_declaration 的类型应为 dynamic 或可隐式转换为 System.IDisposable 的类型。如果 resource_acquisition 的形式为 expression，则该表达式应可隐式转换为 System.IDisposable。

在 resource_acquisition 中声明的局部变量是只读的，并且应包含初始值设定项。如果嵌入语句试图修改这些局部变量（通过赋值或 ++ 和 -- 运算符）、获取它们的地址，或将它们作为 ref 或 out 参数传递，则发生编译时错误。

using 语句转换为三个部分：获取、使用和释放。资源的使用隐式包含在包含 finally 子句的 try 语句中。此 finally 子句释放该资源。如果获取的资源为 null，则不调用 Dispose，也不引发异常。如果资源的类型为 dynamic，则在获取期间通过隐式动态转换（§10.2.10）将其动态转换为 IDisposable，以确保在使用和释放之前转换成功。

形式如下的 using 语句

```
using (ResourceType resource = «expression» ) «statement»
```

对应于三种可能的展开之一。当 ResourceType 为非可空值类型或具有值类型约束的类型参数（§15.2.5）时，该展开在语义上等价于

```
{
    ResourceType resource = «expression»;
    try
    {
        «statement»;
    }
    finally
    {
        ((IDisposable)resource).Dispose();
    }
}
```

只不过将 resource 强制转换为 System.IDisposable 不得导致装箱发生。

否则，当 ResourceType 为 dynamic 时，展开为

```
{
    ResourceType resource = «expression»;
    IDisposable d = resource;
    try
    {
        «statement»;
    }
    finally
    {
        if (d != null)
        {
            d.Dispose();
        }
    }
}
```

否则，展开为

```
{
    ResourceType resource = «expression»;
    try
    {
        «statement»;
    }
    finally
    {
        IDisposable d = (IDisposable)resource;
        if (d != null)
        {
            d.Dispose();
        }
    }
}
```

在任何展开中，`resource` 变量在嵌入语句中是只读的，而 `d` 变量在嵌入语句中不可访问且不可见。

允许实现以不同方式实现给定的 `using_statement`（例如出于性能原因），只要其行为与上述展开一致。

形式如下的 `using` 语句：

```
using («expression») «statement»
```

具有相同的三种可能展开。在这种情况下，如果 `expression` 具有编译时类型，则 `ResourceType` 隐式为该编译时类型。否则，接口 `IDisposable` 本身用作 `ResourceType`。`resource` 变量在嵌入的 `statement` 中不可访问且不可见。

当 `resource_acquisition` 采用 `local_variable_declaration` 的形式时，可以获取给定类型的多个资源。形式如下的 `using` 语句

```
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) «statement»
```

完全等价于一系列嵌套的 `using` 语句：

```
using (ResourceType r1 = e1)
using (ResourceType r2 = e2)
...
using (ResourceType rN = eN)
    «statement»
```

示例：下面的示例创建一个名为 `log.txt` 的文件，并向该文件写入两行文本。然后，该示例打开同一个文件进行读取，并将其中包含的文本行复制到控制台。

```csharp
class Test
{
    static void Main()
    {
        using (TextWriter w = File.CreateText("log.txt"))
        {
            w.WriteLine("This is line one");
            w.WriteLine("This is line two");
        }

        using (TextReader r = File.OpenText("log.txt"))
        {
            string s;
            while ((s = r.ReadLine()) != null)
            {
                Console.WriteLine(s);
            }
        }
    }
}
```

由于 TextWriter 和 TextReader 类实现 IDisposable 接口，该示例可以使用 using 语句来确保在写入或读取操作之后正确关闭基础文件。

*示例结束*

## 13.15 yield 语句

yield 语句用于迭代器块（§13.3）中，以向迭代器的枚举器对象（§15.14.5）或可枚举对象（§15.14.6）生成值，或发出迭代结束的信号。

```
yield_statement
  : 'yield' 'return' expression ';'
  | 'yield' 'break' ';'
  ;
```

yield 是上下文关键字（§6.4.4），仅当紧接在 return 或 break 关键字之前使用时才具有特殊含义。

yield 语句可以出现的位置有若干限制，如下所述。

- 如果 yield 语句（任一形式）出现在 method_body、operator_body 或 accessor_body 之外，则为编译时错误。
- 如果 yield 语句（任一形式）出现在匿名函数内，则为编译时错误。
- 如果 yield 语句（任一形式）出现在 try 语句的 finally 子句中，则为编译时错误。
- 如果 yield return 语句出现在包含任何 catch_clauses 的 try 语句中的任何位置，则为编译时错误。

示例：下面的示例展示 yield 语句的一些有效和无效用法。

```
delegate IEnumerable<int> D();

IEnumerator<int> GetEnumerator()
{
    try
    {
        yield return 1; // Ok
        yield break;    // Ok
    }
    finally
    {
        yield return 2; // Error, yield in finally
        yield break;    // Error, yield in finally
    }
    try
    {
        yield return 3; // Error, yield return in try/catch
        yield break;    // Ok
    }
    catch
    {
        yield return 4; // Error, yield return in try/catch
    }
}
    yield break;  // Ok
}
D d = delegate
{
    yield return 5; // Error, yield in an anonymous function
};
}
int MyMethod()
{
    yield return 1;    // Error, wrong return type for an iterator block
}
```

示例结束

从 yield return 语句中表达式的类型到迭代器的 yield 类型（§15.14.4）之间应存在隐式转换（§10.2）。

yield return 语句的执行方式如下：

- 计算语句中给定的表达式，将其隐式转换为 yield 类型，并赋给枚举器对象的 Current 属性。
- 迭代器块的执行被挂起。如果 yield return 语句位于一个或多个 try 块内，则此时不执行关联的 finally 块。
- 枚举器对象的 MoveNext 方法向其调用方返回 true，指示枚举器对象已成功前进到下一项。

对枚举器对象的 MoveNext 方法的下一次调用会从迭代器块上次挂起的位置恢复执行。

yield break 语句的执行方式如下：

- 如果 yield break 语句被一个或多个具有关联 finally 块的 try 块包围，则控制最初转移到最内层 try 语句的 finally 块。当控制到达 finally 块的结束点（如果会到达）时，控制转移到下一个外层 try 语句的 finally 块。重复此过程，直到所有外层 try 语句的 finally 块都已执行。
- 控制返回到迭代器块的调用方。这可能是枚举器对象的 MoveNext 方法或 Dispose 方法。

由于 yield break 语句无条件地将控制转移到其他位置，因此 yield break 语句的结束点永远不可到达。




# 14. 命名空间

### 14.1 概述

C# 程序使用命名空间进行组织。命名空间既用作程序的“内部”组织系统，也用作“外部”组织系统——一种将程序元素呈现给其他程序的方式。

提供 using 指令（§14.5）以方便命名空间的使用。

### 14.2 编译单元

一个 compilation_unit 由零个或多个 extern_alias_directive，后跟零个或多个 using_directive，后跟零个或一个 global_attributes，后跟零个或多个 namespace_member_declaration 组成。compilation_unit 定义了输入的总体结构。

```
compilation_unit
: extern_alias_directive* using_directive* global_attributes?
  namespace_member_declaration*
  ;
```

一个 C# 程序由一个或多个编译单元组成。当编译 C# 程序时，所有编译单元会一起处理。因此，编译单元之间可以相互依赖，甚至可能以循环方式依赖。

一个编译单元的 extern_alias_directive 会影响该编译单元的 using_directive、global_attributes 和 namespace_member_declaration，但不会影响其他编译单元。

一个编译单元的 using_directive 会影响该编译单元的 global_attributes 和 namespace_member_declaration，但不会影响其他编译单元。

编译单元的 global_attributes（§22.3）允许为目标程序集和模块指定特性。程序集和模块充当类型的物理容器。一个程序集可能由多个物理上独立的模块组成。

程序的每个编译单元的 namespace_member_declaration 会向一个称为全局命名空间的单一声明空间贡献成员。

*示例：*

```
// File A.cs:
class A {}
// File B.cs:
class B {}
```

这两个编译单元共同构成单个全局命名空间，在此例中声明了两个类，其完全限定名分别为 A 和 B。由于这两个编译单元贡献到同一个声明空间，如果各自包含同名成员的声明，则会产生错误。

*示例结束*

### 14.3 命名空间声明

一个 *namespace_declaration* 由关键字 namespace 组成，后跟命名空间名称和主体，可选地跟一个分号。

```
namespace_declaration
  : 'namespace' qualified_identifier namespace_body ';'?
  ;

qualified_identifier
  : identifier ('.' identifier)*
  ;

namespace_body
  : '{' extern_alias_directive* using_directive*
    namespace_member_declaration* '}'
  ;
```

*namespace_declaration* 可以出现在 *compilation_unit* 中作为顶级声明，也可以出现在另一个 *namespace_declaration* 内作为成员声明。当 *namespace_declaration* 作为 *compilation_unit* 中的顶级声明出现时，该命名空间成为全局命名空间的成员。当 *namespace_declaration* 出现在另一个 *namespace_declaration* 内时，内部命名空间成为外部命名空间的成员。无论哪种情况，命名空间的名称在其包含的命名空间中必须是唯一的。

命名空间隐式地 *public*，并且命名空间的声明不能包含任何访问修饰符。

在 *namespace_body* 内，可选的 *using_directive* 导入其他命名空间、类型和成员的名称，使它们可以直接引用，而无需使用限定名。可选的 *namespace_member_declaration* 向命名空间的声明空间贡献成员。注意，所有 *using_directive* 必须出现在任何成员声明之前。

*namespace_declaration* 的 *qualified_identifier* 可以是单个标识符，也可以是由“.”标记分隔的标识符序列。后一种形式允许程序定义一个嵌套命名空间，而不必在词法上嵌套多个命名空间声明。

*示例：*

```
namespace N1.N2
{
    class A {}
    class B {}
}
```

在语义上等效于

```
namespace N1
{
    namespace N2
    {
        class A {}
        class B {}
    }
}
```

*示例结束*

命名空间是开放式的，具有相同完全限定名（§7.8.2）的两个命名空间声明会贡献到同一个声明空间（§7.3）。

*示例：* 在以下代码中

```
    namespace N1.N2
    {
        class A {}
    }

    namespace N1.N2
    {
        class B {}
    }
```

上面的两个命名空间声明贡献到同一个声明空间，在此例中声明了两个类，其完全限定名分别为 N1.N2.A 和 N1.N2.B。由于这两个声明贡献到同一个声明空间，如果各自包含同名成员的声明，则会产生错误。

*示例结束*

### 14.4 外部别名指令

An extern_alias_directive 引入一个标识符作为命名空间的别名。被别名化的命名空间的规范在程序源代码之外，并且同样适用于被别名化命名空间的嵌套命名空间。

```
    extern_alias_directive
        : 'extern' 'alias' identifier ';'
        ;
```

extern_alias_directive 的作用范围覆盖其直接包含的 compilation_unit 或 namespace_body 中的 using_directive、global_attributes 和 namespace_member_declaration。

在包含 extern_alias_directive 的编译单元或命名空间主体内，可以使用该指令引入的标识符来引用被别名化的命名空间。如果该标识符是单词 global，则会产生编译时错误。

extern_alias_directive 引入的别名与 using_alias_directive 引入的别名非常相似。有关 extern_alias_directive 和 using_alias_directive 的更详细讨论，请参见 §14.5.2。

alias 是一个上下文关键字（§6.4.4），仅当它紧跟在 extern_alias_directive 中的 extern 关键字之后时才有特殊含义。

如果程序声明了一个外部别名，但没有为其提供外部定义，则会发生错误。

*示例：* 以下程序声明并使用了两个外部别名 X 和 Y，它们分别表示一个不同命名空间层次结构的根：

```
    extern alias X;
    extern alias Y;

    class Test
    {
        X::N.A a;
        X::N.B b1;
        Y::N.B b2;
        Y::N.C c;
    }
```

该程序声明了外部别名 X 和 Y 的存在，但别名的实际定义在程序外部。现在可以使用命名空间别名限定符，将同名的 N.B 类引用为 X::N.B 和 Y::N.B。

*示例结束*

### 14.5 Using 指令

#### 14.5.1 概述

Using 指令有助于使用在其他命名空间中定义的命名空间和类型。Using 指令影响 namespace_or_type_names（§7.8）和 simple_names（§12.8.4）的名称解析过程，但与声明不同，using_directive 不会向使用它们的编译单元或命名空间的底层声明空间贡献新成员。

```
using_directive
  : using_alias_directive
  | using_namespace_directive
  | using_static_directive
  ;
```

using_alias_directive（§14.5.2）为命名空间或类型引入别名。

using_namespace_directive（§14.5.3）导入命名空间的类型成员。

using_static_directive（§14.5.4）导入类型的嵌套类型和静态成员。

using_directive 的作用范围覆盖其直接包含的编译单元或命名空间主体中的 namespace_member_declaration。using_directive 的作用范围明确不包括其同级 using 指令。因此，同级 using 指令互不影响，且它们书写的顺序无关紧要。相比之下，extern_alias_directive 的作用范围包括在同一编译单元或命名空间主体中定义的 using 指令。

#### 14.5.2 Using 别名指令

A using_alias_directive 引入一个标识符，作为紧邻的编译单元或命名空间主体内某个命名空间或类型的别名。

```
using_alias_directive
  : 'using' identifier '=' namespace_or_type_name ';'
  ;
```

在包含 using_alias_directive 的编译单元或命名空间主体内的全局特性和成员声明中，可以使用该指令引入的标识符来引用给定的命名空间或类型。

*示例：*

```
namespace N1.N2
{
  class A {}
}
namespace N3
{
  using A = N1.N2.A;
}
```




```
class B: A {}
}
```

以上，在 N3 命名空间中的成员声明内，A 是 N1.N2.A 的别名，因此类 N3.B 派生自类 N1.N2.A。可以通过创建 R 对 N1.N2 的别名然后引用 R.A 来获得相同的效果：

```
namespace N3
{
    using R = N1.N2;

    class B : R.A {}
}
```

结束示例

在包含 extern_alias_directive 的编译单元或命名空间体内的 using 指令、全局属性和成员声明中，由 extern_alias_directive 引入的标识符可用于引用关联的命名空间。

示例：例如：

```
namespace N1
{
    extern alias N2;

    class B : N2::A {}
}
```

以上，在 N1 命名空间中的成员声明内，N2 是对程序源代码外部定义的某个命名空间的别名。类 N1.B 派生自类 N2.A。可以通过创建 A 对 N2.A 的别名然后引用 A 来获得相同的效果：

```
namespace N1
{
    extern alias N2;

    using A = N2::A;

    class B : A {}
}
```

结束示例

extern_alias_directive 或 using_alias_directive 使别名在特定的编译单元或命名空间体内可用，但它不会向底层声明空间贡献任何新成员。换句话说，别名指令不是传递的，而是仅影响它出现的编译单元或命名空间体。

示例：在以下代码中

```
namespace N3
{
    extern alias R1;

    using R2 = N1.N2;
}
```

```
namespace N3
{
    class B : R1::A, R2.I {} // Error, R1 and R2 unknown
}
```

引入 R1 和 R2 的别名指令的作用域仅扩展到包含它们的命名空间体中的成员声明，因此在第二个命名空间声明中 R1 和 R2 是未知的。然而，将别名指令放在包含的编译单元中会使别名在两个命名空间声明中都可用：

```
extern alias R1;
```

```
using R2 = N1.N2;
```

```
namespace N3
{
    class B : R1::A, R2.I {}
}
```

```
namespace N3
{
    class C : R1::A, R2.I {}
}
```

结束示例

编译单元或 namespace_body 中的每个 extern_alias_directive 或 using_alias_directive 都会向直接包含的编译单元或命名空间体的别名声明空间（§7.3）贡献一个名称。别名指令的标识符在相应的别名声明空间内必须是唯一的。别名标识符不必在全局声明空间或相应命名空间的声明空间内唯一。

示例：

```
extern alias X;
extern alias Y;
```

```
using X = N1.N2; // Error: alias X already exists
```

```
class Y {} // Ok
```

名为 X 的 using 别名导致错误，因为在同一个编译单元中已存在名为 X 的别名。名为 Y 的类与名为 Y 的 extern 别名不冲突，因为这些名称被添加到不同的声明空间。前者被添加到全局声明空间，后者被添加到此编译单元的别名声明空间。

当别名名称与命名空间的成员名称相同时，使用任一名称都必须适当地限定：

```
namespace N1.N2
{
    class B {}
}
```

```
namespace N3
{
    class A {}
}
```

```
class B : A {}
}
namespace N3
{
    using A = N1.N2;
    using B = N1.N2.B;
    class W : B {} // Error: B is ambiguous
    class X : A.B {} // Error: A is ambiguous
    class Y : A::B {} // Ok: uses N1.N2.B
    class Z : N3.B {} // Ok: uses N3.B
}
```

在 N3 的第二个命名空间体中，未限定的 B 用法会导致错误，因为 N3 包含一个名为 B 的成员，并且该命名空间体还声明了名为 B 的别名；A 也是如此。类 N3.B 可以作为 N3.B 或 global::N3.B 引用。别名 A 可以在限定别名成员（§14.8）中使用，例如 A::B。别名 B 基本上是无用的。它不能在 qualified_alias_member 中使用，因为只有命名空间别名才能在 qualified_alias_member 中使用，而 B 别名的是一个类型。

结束示例

就像常规成员一样，由 alias_directives 引入的名称会被嵌套作用域中同名成员隐藏

示例：在以下代码中

```
using R = N1.N2;
namespace N3
{
    class R {}
    class B: R.A {} // Error, R has no member A
}
```

在 B 的声明中对 R.A 的引用会导致编译时错误，因为 R 引用的是 N3.R，而不是 N1.N2。

结束示例

extern_alias_directives 的书写顺序无关紧要。同样，using_alias_directives 的书写顺序也无关紧要，但所有 using_alias_directives 必须在同一个编译单元或命名空间体中位于所有 extern_alias_directives 之后。由 using_alias_directive 引用的 namespace_or_type_name 的解析不受 using_alias_directive 本身或直接包含的编译单元或命名空间体中的其他 using_directives 影响，但可能受直接包含的编译单元或命名空间体中的 extern_alias_directives 影响。换句话说，using_alias_directive 的 namespace_or_type_name 的解析就像直接包含的编译单元或命名空间体没有 using_directives 但具有正确的 extern_alias_directives 集合一样。

示例：在以下代码中

```
namespace N1.N2 {}
namespace N3
{
```

```
extern alias X;

using R1 = X::N; // OK
using R2 = N1; // OK
using R3 = N1.N2; // OK
using R4 = R2.N2; // Error, R2 unknown
}
```

最后一个 using_alias_directive 导致编译时错误，因为它不受前一个 using_alias_directive 影响。第一个 using_alias_directive 不会导致错误，因为 extern 别名 X 的作用域包含 using_alias_directive。

*结束示例*

using_alias_directive 可以为任何命名空间或类型创建别名，包括它出现的命名空间以及该命名空间内嵌套的任何命名空间或类型。

通过别名访问命名空间或类型与通过其声明名称访问该命名空间或类型得到的结果完全相同。

*示例：给定*

```
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using R1 = N1;
    using R2 = N1.N2;

    class B
    {
        N1.N2.A a; // refers to N1.N2.A
        R1.N2.A b; // refers to N1.N2.A
        R2.A c; // refers to N1.N2.A
    }
}
```

名称 N1.N2.A、R1.N2.A 和 R2.A 是等价的，并且都引用完全限定名称为 N1.N2.A 的类声明。

*结束示例*

尽管 partial type（§15.2.7）的每个部分都在同一个命名空间内声明，但这些部分通常写在不同的命名空间声明中。因此，每个部分可以存在不同的 extern_alias_directives 和 using_directives。在解释一个部分内的简单名称（§12.8.4）时，仅考虑包含该部分的命名空间体和编译单元的 extern_alias_directives 和 using_directives。这可能导致同一个标识符在不同部分中具有不同的含义。

*示例：*

```
namespace N
{
    using List = System.Collections.ArrayList;
```

```
partial class A
{
    List x; // x has type System.Collections.ArrayList
}
}
```

```
namespace N
{
    using List = Widgets.LinkedList;

    partial class A
    {
        List y; // y has type Widgets.LinkedList
    }
}
```

结束示例

使用别名可以命名封闭构造类型，但不能在不提供类型参数的情况下命名未绑定泛型类型声明。

示例：

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
    using W = N1.A;      // Error, cannot name unbound generic type
    using X = N1.A.B;    // Error, cannot name unbound generic type
    using Y = N1.A<int>; // Ok, can name closed constructed type
    using Z<T> = N1.A<T>; // Error, using alias cannot have type parameters
}
```

结束示例

## 14.5.3 using 命名空间指令

using_namespace_directive 将命名空间中包含的类型导入到直接包含的编译单元或命名空间体中，使每个类型的标识符能够在不加限定的情况下使用。

```
using_namespace_directive
    : 'using' namespace_name ';'
    ;
```

在包含 using_namespace_directive 的编译单元或命名空间体中的成员声明内，可以直接引用给定命名空间中包含的类型。

示例：

```
namespace N1.N2
{
    class A {}
}
```




```
namespace N3
{
    using N1.N2;
    class B : A {}
}
```

在上面的代码中，在 N3 命名空间内的成员声明中，N1.N2 的类型成员可直接使用，因此类 N3.B 派生自类 N1.N2.A。

示例结束

using_namespace_directive 导入给定命名空间中所包含的类型，但特别地不导入嵌套命名空间。

示例：在下面的代码中

```
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using N1;
    class B : N2.A {} // Error, N2 unknown
}
```

该 using_namespace_directive 导入 N1 中包含的类型，但不导入 N1 中嵌套的命名空间。因此，在 B 的声明中对 N2.A 的引用会产生编译时错误，因为作用域内没有任何名为 N2 的成员。

示例结束

与 using_alias_directive 不同，using_namespace_directive 可以导入其标识符已在外层编译单元或命名空间主体中定义的类型。实际上，由 using_namespace_directive 导入的名称会被外层编译单元或命名空间主体中同名的成员隐藏。

示例：

```
namespace N1.N2
{
    class A {}
    class B {}
}

namespace N3
{
    using N1.N2;
    class A {}
}
```

此处，在 N3 命名空间内的成员声明中，A 指的是 N3.A 而不是 N1.N2.A。

示例结束

因为当多个导入的命名空间引入了相同的类型名称时名称可能会产生歧义，所以使用 using_alias_directive 有助于消除引用歧义。

示例：在下面的代码中

```
namespace N1
{
    class A {}
}

namespace N2
{
    class A {}
}

namespace N3
{
    using N1;
    using N2;

    class B : A {} // Error, A is ambiguous
}
```

N1 和 N2 都包含一个成员 A，由于 N3 同时导入了两者，因此在 N3 中引用 A 会产生编译时错误。在这种情况下，可以通过限定对 A 的引用来解决冲突，或者引入一条 using_alias_directive 来选定特定的 A。例如：

```
namespace N3
{
    using N1;
    using N2;
    using A = N1.A;

    class B : A {} // A means N1.A
}
```

示例结束

此外，当同一编译单元或命名空间主体中由 using_namespace_directives 或 using_static_directives 导入的多个命名空间或类型包含同名的类型或成员时，将该名称作为 simple_name 的引用将被视为有歧义。

示例：

```
namespace N1
{
    class A {}
}

class C
{
    public static int A;
}

namespace N2
{
    using N1;
    using static C;
```

```
class B
{
    void M()
    {
        A a = new A();  // Ok, A is unambiguous as a type-name
        A.Equals(2);    // Error, A is ambiguous as a simple-name
    }
}
```

N1 包含一个类型成员 A，C 包含一个静态字段 A，由于 N2 同时导入了两者，将 A 作为 simple_name 引用会产生歧义并导致编译时错误。

*示例结束*

与 using_alias_directive 一样，using_namespace_directive 不会向编译单元或命名空间的底层声明空间贡献任何新成员，而只会影响它所在的编译单元或命名空间主体。

using_namespace_directive 所引用的 namespace_name 的解析方式与 using_alias_directive 所引用的 namespace_or_type_name 相同。因此，同一编译单元或命名空间主体中的 using_namespace_directives 互不影响，可以按任意顺序编写。

## 14.5.4 using static 指令

using_static_directive 将类型声明中直接包含的嵌套类型和静态成员导入到直接封闭的编译单元或命名空间主体中，使每个成员和类型的标识符无需限定即可使用。

```
using_static_directive
    : 'using' 'static' type_name ';'
    ;
```

在包含 using_static_directive 的编译单元或命名空间主体的成员声明中，可以直接引用给定类型的声明中直接包含的可访问嵌套类型和静态成员（扩展方法除外）。

示例：

```
namespace N1
{
    class A
    {
        public class B {}
        public static B M() => new B();
    }
}

namespace N2
{
    using static N1.A;

    class C
    {
        void N()
        {
```

```
    }
}
        B b = M();
```

在前面的代码中，在 N2 命名空间内的成员声明中，N1.A 的静态成员和嵌套类型可直接使用，因此方法 N 能够引用 N1.A 的 B 和 M 成员。

示例结束

using_static_directive 特别地不会将扩展方法作为静态方法直接导入，而是使它们可用于扩展方法调用（§12.8.9.3）。

示例：

```
namespace N1
{
    static class A
    {
        public static void M(this string s){}
    }
}
namespace N2
{
    using static N1.A;

    class B
    {
        void N()
        {
            M("A");    // Error, M unknown
            "B".M();    // Ok, M known as extension method
            N1.A.M("C"); // OK, fully qualified
        }
    }
}
```

该 using_static_directive 导入 N1.A 中包含的扩展方法 M，但只是将其作为扩展方法。因此，B.N 主体中对 M 的第一个引用会产生编译时错误，因为作用域内没有任何名为 M 的成员。

示例结束

using_static_directive 只导入在给定类型中直接声明的成员和类型，而不导入在基类中声明的成员和类型。

示例：

```
namespace N1
{
    class A
    {
        public static void M(string s){}
    }

    class B : A
{
    public static void M2(string s){}
}
namespace N2
{
    using static N1.B;
    class C
    {
        void N()
        {
            M2("B");    // OK, calls B.M2
            M("C");     // Error. M unknown
        }
    }
}
```

该 using_static_directive 导入 N1.B 中包含的方法 M2，但不导入 N1.A 中包含的方法 M。因此，C.N 主体中对 M 的引用会产生编译时错误，因为作用域内没有任何名为 M 的成员。开发人员必须添加另一条 using static 指令，以指定 N1.A 中的方法也应被导入。

*示例结束*

## 14.6 命名空间成员声明

namespace_member_declaration 要么是 namespace_declaration（§14.3），要么是 type_declaration（§14.7）。

```
namespace_member_declaration
: namespace_declaration
| type_declaration
;
```

编译单元或命名空间主体可以包含 namespace_member_declarations，此类声明会向包含它们的编译单元或命名空间主体的底层声明空间贡献新成员。

## 14.7 类型声明

type_declaration 是 class_declaration（§15.2）、struct_declaration（§16.2）、interface_declaration（§18.2）、enum_declaration（§19.2）或 delegate_declaration（§20.2）。

```
type_declaration
: class_declaration
| struct_declaration
| interface_declaration
| enum_declaration
| delegate_declaration
;
```

<!-- no content -->

- 如果 N 是标识符 `global`，则在全局命名空间中搜索 I：
  - 如果全局命名空间包含名为 I 的命名空间且 e 为零，则 *qualified_alias_member* 引用该命名空间。
  - 否则，如果全局命名空间包含名为 I 的非泛型类型且 e 为零，则 *qualified_alias_member* 引用该类型。
  - 否则，如果全局命名空间包含名为 I 且具有 e 个类型形参的类型，则 *qualified_alias_member* 引用使用给定的类型实参构造的该类型。
  - 否则，*qualified_alias_member* 未定义，发生编译时错误。
- 否则，从紧邻包含 *qualified_alias_member* 的命名空间声明（§14.3）（如果有）开始，继续遍历每个外层命名空间声明（如果有），最后到包含 *qualified_alias_member* 的编译单元为止，将依次评估以下步骤，直到定位到实体：
  - 如果该命名空间声明或编译单元包含将 N 与类型关联的 *using_alias_directive*，则 *qualified_alias_member* 未定义，发生编译时错误。
  - 否则，如果该命名空间声明或编译单元包含将 N 与命名空间关联的 *extern_alias_directive* 或 *using_alias_directive*，则：
    - 如果与 N 关联的命名空间包含名为 I 的命名空间且 e 为零，则 *qualified_alias_member* 引用该命名空间。
    - 否则，如果与 N 关联的命名空间包含名为 I 的非泛型类型且 e 为零，则 *qualified_alias_member* 引用该类型。
    - 否则，如果与 N 关联的命名空间包含名为 I 且具有 e 个类型形参的类型，则 *qualified_alias_member* 引用使用给定的类型实参构造的该类型。
    - 否则，*qualified_alias_member* 未定义，发生编译时错误。
- 否则，*qualified_alias_member* 未定义，发生编译时错误。

示例：在下面的代码中：

```
using S = System.Net.Sockets;

class A
{
    public static int x;
}

class C
{
    public void F(int A, object S)
    {
        // Use global::A.x instead of A.x
        global::A.x += A;
        // Use S::Socket instead of S.Socket
        S::Socket s = S as S::Socket;
    }
}
```


类 A 使用 global::A 进行引用，类型 System.Net.Sockets.Socket 使用 S::Socket 进行引用。如果改用 A.x 和 S.Socket，则会因 A 和 S 被解析为参数而导致编译时错误。

示例结束

注意：标识符 global 只有在用作 qualified_alias_name 的左手标识符时才具有特殊含义。它不是关键字，也不是它本身的别名；它是一个上下文关键字（§6.4.4）。在代码中：

```
class A { }

class C
{
    global.A x; // Error: global is not defined
    global::A y; // Valid: References A in the global namespace
}
```

使用 global.A 会导致编译时错误，因为作用域中没有名为 global 的实体。如果作用域中存在某个名为 global 的实体，则 global.A 中的 global 将解析为该实体。

将 global 用作 qualified_alias_member 的左手标识符时，始终会在全局命名空间中进行查找，即使存在名为 global 的 using 别名。在代码中：

```
using global = MyGlobalTypes;

class A { }

class C
{
    global.A x; // Valid: References MyGlobalTypes.A
    global::A y; // Valid: References A in the global namespace
}
```

global.A 解析为 MyGlobalTypes.A，而 global::A 解析为全局命名空间中的类 A。

注释结束

## 14.8.2 别名的唯一性

每个编译单元和命名空间体都有各自的 extern 别名和 using 别名的声明空间。因此，虽然 extern 别名或 using 别名的名称在直接包含的编译单元或命名空间体中声明的 extern 别名和 using 别名集合内必须是唯一的，但只要仅与 :: 限定符一起使用，别名就可以与类型或命名空间具有相同的名称。

示例：在以下内容中：

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
        A.Stream s1; // Error, A is ambiguous
        A::Stream s2; // Ok
    }
}
```

在第二个命名空间体中，名称 A 有两种可能的含义，因为类 A 和 using 别名 A 都在作用域内。因此，在限定名 A.Stream 中使用 A 是模棱两可的，会导致编译时错误。然而，使用 :: 限定符使用 A 并不是错误，因为此时只会将 A 作为命名空间别名进行查找。

*示例结束*

# 15. 类

### 15.1 通用

类是一种数据结构，可能包含数据成员（常量和字段）、函数成员（方法、属性、事件、索引器、运算符、实例构造函数、终结器和静态构造函数）以及嵌套类型。类类型支持继承，这是一种机制，派生类可以通过该机制扩展和特化基类。

### 15.2 类声明

### 15.2.1 通用

class_declaration 是 type_declaration (§14.7)，用于声明新的类。

```
class_declaration
: attributes? class_modifier* 'partial'? 'class' identifier
  type_parameter_list? class_base? type_parameter_constraints_clause*
  class_body ';'?
```

class_declaration 由一组可选的属性 (§22) 组成，其后是可选的一组 class_modifiers (§15.2.2)，其后是可选的 partial 修饰符 (§15.2.7)，其后是关键字 class 和一个标识类的标识符，其后是可选的 type_parameter_list (§15.2.3)，其后是可选的 class_base 规范 (§15.2.4)，其后是可选的一组 type_parameter_constraints_clauses (§15.2.5)，其后是 class_body (§15.2.6)，可选择跟随一个分号。

类声明不得提供 type_parameter_constraints_clauses，除非它同时提供 type_parameter_list。

提供 type_parameter_list 的类声明是泛型类声明。此外，嵌套在泛型类声明或泛型结构声明内部的任何类本身都是泛型类声明，因为为了创建构造类型 (§8.4)，必须为包含的类型提供类型参数。

### 15.2.2 类修饰符

### 15.2.2.1 通用

class_declaration 可选择包含一系列 class 修饰符：

```
class_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| 'abstract'
| 'sealed'
| 'static'
| unsafe_modifier  // unsafe code support
;
```

unsafe_modifier (§23.2) 仅在不安全代码 (§23) 中可用。

在类声明中同一修饰符出现多次是编译时错误。

new 修饰符允许用于嵌套类。它指定类隐藏了同名的继承成员，如 §15.3.5 中所述。在不是嵌套类声明的类声明上出现 new 修饰符是编译时错误。

public、protected、internal 和 private 修饰符控制类的可访问性。根据类声明出现的上下文，其中一些修饰符可能不被允许 (§7.5.2)。

当部分类型声明 (§15.2.7) 包含可访问性规范（通过 public、protected、internal 和 private 修饰符）时，该规范必须与包含可访问性规范的所有其他部分一致。如果部分类型的任何部分都不包含可访问性规范，则类型将被赋予适当的默认可访问性 (§7.5.2)。

abstract、sealed 和 static 修饰符在以下小节中讨论。

### 15.2.2.2 抽象类

abstract 修饰符用于指示类是不完整的，并且仅 intended 用于作为基类。抽象类与非抽象类在以下方面有所不同：

- 抽象类不能直接实例化，使用 new 运算符对抽象类进行操作是编译时错误。虽然可以拥有编译时类型为抽象的变量和值，但此类变量和值必然为空，或者包含对从抽象类型派生的非抽象类实例的引用。
- 抽象类允许（但不是必须）包含抽象成员。
- 抽象类不能被密封。

当非抽象类从抽象类派生时，非抽象类必须包含所有继承的抽象成员的实际实现，从而覆盖这些抽象成员。

示例：以下代码中

```
abstract class A
{
    public abstract void F();
}

abstract class B : A
{
    public void G() {}
}

class C : B
{
    public override void F()
    {
        // Actual implementation of F
    }
}
```

抽象类 A 引入了抽象方法 F。类 B 引入了额外的方法 G，但由于它没有提供 F 的实现，因此 B 也必须声明为抽象。类 C 覆盖了 F 并提供了实际实现。由于 C 中没有抽象成员，因此 C 允许（但不是必须）为非抽象。

*示例结束*

如果类的部分类型声明 (§15.2.7) 的一个或多个部分包含 `abstract` 修饰符，则该类为抽象类。否则，该类为非抽象类。

### 15.2.2.3 密封类

`sealed` 修饰符用于防止从类派生。如果将密封类指定为另一个类的基类，则会发生编译时错误。

密封类不能同时是抽象类。

*注意：* `sealed` 修饰符主要用于防止非预期的派生，但它也能够实现某些运行时优化。特别是，由于已知密封类永远不会有派生类，因此可以将密封类实例上的虚函数成员调用转换为非虚调用。*注释结束*

如果类的部分类型声明 (§15.2.7) 的一个或多个部分包含 `sealed` 修饰符，则该类为密封类。否则，该类为非密封类。

### 15.2.2.4 静态类

### 15.2.2.4.1 通用

`static` 修饰符用于将声明的类标记为 *静态类*。静态类不得被实例化，不得用作类型，并且只能包含静态成员。只有静态类可以包含扩展方法 (§15.6.10) 的声明。

静态类声明受以下限制：

- 静态类不得包含 `sealed` 或 `abstract` 修饰符。（然而，由于静态类不能被实例化或派生，因此它表现得好像同时是密封的和抽象的。）
- 静态类不得包含 `class_base` 规范 (§15.2.4)，也不能显式指定基类或实现的接口列表。静态类隐式继承自类型 `object`。
- 静态类只能包含静态成员 (§15.3.8)。
  *注意：* 所有常量和嵌套类型都被归类为静态成员。*注释结束*
- 静态类不得具有声明可访问性为 `protected`、`private protected` 或 `protected internal` 的成员。

违反这些限制中的任何一项都是编译时错误。

静态类没有实例构造函数。不可能在静态类中声明实例构造函数，并且静态类不提供默认实例构造函数 (§15.11.5)。

静态类的成员不是自动静态的，成员声明必须显式包含 `static` 修饰符（常量和嵌套类型除外）。当一个类嵌套在静态外部类中时，除非它显式包含 `static` 修饰符，否则嵌套类不是静态类。

如果类的部分类型声明 (§15.2.7) 的一个或多个部分包含 `static` 修饰符，则该类为静态类。否则，该类不是静态类。



### 15.2.2.4 引用静态类类型

在以下情况下，允许 namespace_or_type_name（§7.8）引用静态类：

- namespace_or_type_name 是形如 T . I 的 namespace_or_type_name 中的 T，或
- namespace_or_type_name 是形如 typeof(T) 的 typeof_expression（§12.8.17）中的 T。

在以下情况下，允许 primary_expression（§12.8）引用静态类：

- primary_expression 是形如 E . I 的 member_access（§12.8.7）中的 E。

在任何其他上下文中，引用静态类都是编译时错误。

> *注意：* 例如，将静态类用作基类、成员的构成类型（§15.3.7）、泛型类型实参或类型参数约束都是错误的。同样，静态类不能用于数组类型、new 表达式、强制转换表达式、is 表达式、as 表达式、sizeof 表达式或默认值表达式。注意结束

## 15.2.3 类型参数

类型参数是一个简单标识符，表示用于创建构造类型时所提供的类型实参的占位符。相比之下，类型实参（§8.4.2）是在创建构造类型时替换类型参数的类型。

```
type_parameter_list
  : '<' type_parameters '>'
  ;

type_parameters
  : attributes? type_parameter
  | type_parameters ',' attributes? type_parameter
  ;
```

type_parameter 在 §8.5 中定义。

类声明中的每个类型参数都在该类的声明空间（§7.3）中定义一个名称。因此，它不能与该类的另一个类型参数或该类中声明的成员同名。类型参数不能与该类型本身同名。

如果两个分部泛型类型声明（在同一程序中）具有相同的完全限定名（其中包含用于表示类型参数数量的 generic_dimension_specifier（§12.8.17））（§7.8.3），则它们构成同一个未绑定泛型类型。两个这样的分部类型声明应按顺序为每个类型参数指定相同的名称。

## 15.2.4 类基类规范

### 15.2.4.1 概述

类声明可以包含 class_base 规范，该规范定义该类的直接基类以及该类直接实现的接口（§18）。

```
class_base
  : ':' class_type
  | ':' interface_type_list
  | ':' class_type ',' interface_type_list
  ;
```

```
interface_type_list
  : interface_type (',' interface_type)*
  ;
```

### 15.2.4.2 基类

当 class_base 中包含 class_type 时，它指定正在声明的类的直接基类。如果非分部类声明没有 class_base，或者 class_base 仅列出接口类型，则假定直接基类为 object。当分部类声明包含基类规范时，该基类规范应引用与该分部类型中所有其他包含基类规范的部分相同的类型。如果分部类的任何部分都不包含基类规范，则基类为 object。类从其直接基类继承成员，如 §15.3.4 所述。

*示例：在以下代码中*

```csharp
class A {}
class B : A {}
```

称类 A 是 B 的直接基类，并称 B 派生自 A。由于 A 未显式指定直接基类，因此其直接基类隐式为 object。

*示例结束*

对于构造类类型，包括在泛型类型声明（§15.3.9.7）中声明的嵌套类型，如果在泛型类声明中指定了基类，则构造类型的基类通过以下方式获得：对于基类声明中的每个 type_parameter，替换为构造类型对应的 type_argument。

*示例：给定以下泛型类声明*

```csharp
class B<U,V> {...}
class G<T> : B<string,T[]> {...}
```

则构造类型 G<int> 的基类将是 B<string,int[]>。

*示例结束*

类声明中指定的基类可以是构造类类型（§8.4）。基类本身不能是类型参数（§8.5），但可以涉及作用域内的类型参数。

*示例：*

```csharp
class Base<T> {}

// Valid, non-constructed class with constructed base class
class Extend1 : Base<int> {}

// Error, type parameter used as base class
class Extend2<V> : V {}

// Valid, type parameter used as type argument for base class
class Extend3<V> : Base<V> {}
```

*示例结束*

类类型的直接基类应至少与类类型本身具有相同的可访问性（§7.5.5）。例如，public 类派生自 private 或 internal 类是编译时错误。

类类型的直接基类不得为以下任何类型：System.Array、System.Delegate、System.Enum 或 System.ValueType。此外，泛型类声明不得将 System.Attribute 用作直接或间接基类（§22.2.1）。

类不依赖于嵌套在其内部的类。

示例：在以下代码中

```
class A
{
    class B : A {}
}
```

B 依赖于 A（因为 A 既是其直接基类，又是其直接外层类），但 A 不依赖于 B（因为 B 既不是 A 的基类，也不是 A 的外层类）。因此，该示例有效。

示例结束

无法从密封类派生。

示例：在以下代码中

```
sealed class A {}
class B : A {} // Error, cannot derive from a sealed class
```

类 B 出错，因为它试图从密封类 A 派生。

示例结束

### 15.2.4.3 接口实现

class_base 规范可以包含接口类型列表，在这种情况下，称该类实现给定的接口类型。对于构造类类型，包括在泛型类型声明（§15.3.9.7）中声明的嵌套类型，每个所实现的接口类型通过以下方式获得：对于给定接口中的每个 type_parameter，替换为构造类型对应的 type_argument。

对于在多个部分中声明的类型（§15.2.7），其接口集是各部分所指定接口的并集。特定接口在每个部分中只能命名一次，但多个部分可以命名相同的基接口。任何给定接口的每个成员应只有一个实现。

示例：在以下代码中：

```
partial class C : IA, IB {...}
partial class C : IC {...}
partial class C : IA, IB {...}
```

示例结束

类声明中指定的基接口可以是构造接口类型（§8.4、§18.2）。基接口本身不能是类型参数，但可以涉及作用域内的类型参数。

示例：以下代码演示类如何实现和扩展构造类型：

```
class <U, V> {}
interface II<V> {}
class D : C<string, int>, II<string> {}
class E<T> : C<int, T>, II<T> {}
```

示例结束

接口实现在 §18.6 中进一步讨论。

## 15.2.5 类型参数约束

泛型类型和方法声明可以通过包含 type_parameter_constraints_clauses 来选择性地指定类型参数约束。

```
type_parameter_constraints_clauses
  : type_parameter_constraints_clause
  | type_parameter_constraints_clauses type_parameter_constraints_clause
  ;

type_parameter_constraints_clause
  : 'where' type_parameter ':' type_parameter_constraints
  ;

type_parameter_constraints
  : primary_constraint
  | secondary_constraints
  | constructor_constraint
  | primary_constraint ',' secondary_constraints
  | primary_constraint ',' constructor_constraint
  | secondary_constraints ',' constructor_constraint
  | primary_constraint ',' secondary_constraints ',' constructor_constraint
  ;

primary_constraint
  : class_type
  | 'class'
  | 'struct'
  | 'unmanaged'
  ;

secondary_constraints
  : interface_type
  | type_parameter
  | secondary_constraints ',' interface_type
  | secondary_constraints ',' type_parameter
  ;

constructor_constraint
```



```
: 'new' '(' ')'
;
```

每个 type_parameter_constraints_clause 由 where 标记组成，后跟类型参数的名称，后跟冒号以及该类型参数的约束列表。每个类型参数最多只能有一个 where 子句，并且 where 子句可以按任意顺序列出。与属性访问器中的 get 和 set 标记类似，where 标记不是关键字。

where 子句中给出的约束列表可以包含以下组件，按此顺序：单个主约束、一个或多个次要约束，以及构造函数约束 new()。

主约束可以是类类型、引用类型约束 class、值类型约束 struct，或非托管类型约束 unmanaged。

次要约束可以是 type_parameter 或 interface_type。

引用类型约束规定用于类型参数的类型参数必须是引用类型。所有类类型、接口类型、委托类型、数组类型以及已知为引用类型（如下定义）的类型参数都满足此约束。

值类型约束规定用于类型参数的类型参数必须是不可空值类型。所有不可空 struct 类型、枚举类型以及具有值类型约束的类型参数都满足此约束。请注意，尽管被归类为值类型，可空值类型 (§8.3.12) 不满足值类型约束。具有值类型约束的类型参数不得同时具有 constructor_constraint，尽管它可以作为具有 constructor_constraint 的另一个类型参数的类型参数使用。

> *Note:* System.Nullable<T> 类型为 T 指定了不可空值类型约束。因此，形式为 T?? 和 Nullable<Nullable<T>> 的递归构造类型被禁止。 *end note*

因为 unmanaged 不是关键字，所以在 primary_constraint 中，unmanaged 约束在语法上始终与 class_type 存在歧义。出于兼容性原因，如果对名称 unmanaged 进行名称查找 (§12.8.4) 成功，则将其视为 class_type。否则将其视为 unmanaged 约束。

非托管类型约束规定用于类型参数的类型参数必须是不可空的非托管类型 (§8.8)。

指针类型永远不允许作为类型参数，并且不满足任何类型约束，即使是 unmanaged，也不会满足，尽管它们是非托管类型。

如果约束是类类型、接口类型或类型参数，则该类型指定了每个用于该类型参数的类型参数必须支持的最小“基类型”。每当使用构造类型或泛型方法时，类型参数都会在编译时与类型参数的约束进行检查。提供的类型参数应满足 §8.4.5 中描述的条件。

class_type 约束应满足以下规则：

- 类型应为类类型。
- 类型不得被密封。
- 类型不得为以下类型之一：System.Array 或 System.ValueType。
- 类型不得为 object。
- 对于给定的类型参数，最多只能有一个约束为类类型。

作为 interface_type 约束指定的类型应满足以下规则：

- 类型应为接口类型。
- 在给定的 where 子句中，类型不得被指定多次。

在任何一种情况下，约束都可能涉及相关类型或方法声明的任何类型参数作为构造类型的一部分，并且可能涉及正在声明的类型。

作为类型参数约束指定的任何类或接口类型，其可访问性 (§7.5.5) 至少应与正在声明的泛型类型或方法一样。

作为 type_parameter 约束指定的类型应满足以下规则：

- 类型应为类型参数。
- 在给定的 where 子句中，类型不得被指定多次。

此外，类型参数的依赖关系图中不得存在循环，其中依赖是传递关系，由以下定义：

- 如果类型参数 T 被用作类型参数 S 的约束，则 S 依赖于 T。
- 如果类型参数 S 依赖于类型参数 T 且 T 依赖于类型参数 U，则 S 依赖于 U。

给定此关系，类型参数直接或间接依赖于自身是编译时错误。

任何约束在相关类型参数之间必须一致。如果类型参数 S 依赖于类型参数 T 则：

- T 不应具有值类型约束。否则，T 在效果上被密封，因此 S 将被迫与 T 为同一类型，从而消除了使用两个类型参数的必要性。
- 如果 S 具有值类型约束，则 T 不应具有 class_type 约束。
- 如果 S 具有 class_type 约束 A 且 T 具有 class_type 约束 B，则应存在从 A 到 B 的恒等转换或隐式引用转换，或从 B 到 A 的隐式引用转换。
- 如果 S 还依赖于类型参数 U 且 U 具有 class_type 约束 A 且 T 具有 class_type 约束 B，则应存在从 A 到 B 的恒等转换或隐式引用转换，或从 B 到 A 的隐式引用转换。

S 具有值类型约束而 T 具有引用类型约束是有效的。实际上这将 T 限制为类型 System.Object、System.ValueType、System.Enum 以及任何接口类型。

如果类型参数的 where 子句包含构造函数约束（其形式为 new()），则可以使用 new 运算符创建该类型的实例 (§12.8.16.2)。任何用于具有构造函数约束的类型参数的类型参数必须是值类型、具有公共无参构造函数的非抽象类，或具有值类型约束或构造函数约束的类型参数。

对于 primary_constraint 为 struct 或 unmanaged 的 type_parameter_constraints 同时具有 constructor_constraint 是编译时错误。

示例：以下是约束的示例：

```
interface IPrintable
{
    void Print();
}
```

```
interface IComparable<T>
{
    int CompareTo(T value);
}

interface IKeyProvider<T>
{
    T GetKey();
}

class Printer<T> where T : IPrintable {...}
class SortedList<T> where T : IComparable<T> {...}

class Dictionary<K,V>
    where K : IComparable<K>
    where V : IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

以下示例因导致类型参数依赖关系图的循环而出错：

```
class Circular<S,T>
    where S: T
    where T: S // Error, circularity in dependency graph
{
    ...
}
```

以下示例说明了额外的无效情况：

```
class Sealed<S,T>
    where S : T
    where T : struct // Error, `T` is sealed
{
    ...
}

class A {...}
class B {...}

class Incompat<S,T>
    where S : A, T
    where T : B // Error, incompatible class-type constraints
{
    ...
}

class StructWithClass<S,T,U>
    where S : struct, T
    where T : U
    where U : A // Error, A incompatible with struct
{
    ...
}
```

*end example*

类型 C 的 **dynamic erasure** 是类型 `C_x`，构造如下：

- 如果 C 是嵌套类型 `Outer.Inner`，则 `C_x` 是嵌套类型 `Outer_x.Inner_x`。
- 如果 `C.C_1` 是构造类型 `G<A^1, ..., A^n>` 且类型参数为 `A^1, ..., A^n`，则 `C_x` 是构造类型 `G<A^1_x, ..., A^n_x>`。
- 如果 C 是数组类型 `E[]`，则 `C_x` 是数组类型 `E_x[]`。
- 如果 C 是 `dynamic`，则 `C_x` 是 `object`。
- 否则，`C_x` 是 C。

类型参数 T 的 **effective base class** 定义如下：

设 R 为类型集合，使得：

- 对于 T 的每个约束，如果是类型参数，则 R 包含其 effective base class。
- 对于 T 的每个约束，如果是 struct 类型，则 R 包含 `System.ValueType`。
- 对于 T 的每个约束，如果是枚举类型，则 R 包含 `System.Enum`。
- 对于 T 的每个约束，如果是委托类型，则 R 包含其 dynamic erasure。
- 对于 T 的每个约束，如果是数组类型，则 R 包含 `System.Array`。
- 对于 T 的每个约束，如果是类类型，则 R 包含其 dynamic erasure。

然后

- 如果 T 具有值类型约束，则其 effective base class 为 `System.ValueType`。
- 否则，如果 R 为空，则 effective base class 为 `object`。
- 否则，T 的 effective base class 为集合 R 的最包容类型 (§10.5.3)。如果集合没有包容类型，则 T 的 effective base class 为 `object`。一致性规则确保最包容类型存在。

如果类型参数是方法类型参数且其约束继承自基方法，则在类型替换后计算 effective base class。

这些规则确保 effective base class 总是一个 `class_type`。

类型参数 T 的 **effective interface set** 定义如下：

- 如果 T 没有 `secondary_constraints`，则其 effective interface set 为空。
- 如果 T 具有 `interface_type` 约束但没有 `type_parameter` 约束，则其 effective interface set 为其 `interface_type` 约束的 dynamic erasure 的集合。
- 如果 T 没有 `interface_type` 约束但具有 `type_parameter` 约束，则其 effective interface set 为其 `type_parameter` 约束的 effective interface sets 的并集。
- 如果 T 同时具有 `interface_type` 约束和 `type_parameter` 约束，则其 effective interface set 为其 `interface_type` 约束的 dynamic erasure 的集合与其 `type_parameter` 约束的 effective interface sets 的并集。

如果类型参数具有引用类型约束或其 effective base class 不是 `object` 或 `System.ValueType`，则该类型参数已知为引用类型。



Values of a constrained type parameter type can be used to access the instance members implied by the constraints.

Example: In the following:

```
interface IPrintable
{
    void Print();
}
```

```
class Printer<T> where T : IPrintable
{
    void PrintOne(T x) => x.Print();
}
```

the methods of IPrintable can be invoked directly on x because T is constrained to always implement IPrintable.

end example

When a partial generic type declaration includes constraints, the constraints shall agree with all other parts that include constraints. Specifically, each part that includes constraints shall have constraints for the same set of type parameters, and for each type parameter, the sets of primary, secondary, and constructor constraints shall be equivalent. Two sets of constraints are equivalent if they contain the same members. If no part of a partial generic type specifies type parameter constraints, the type parameters are considered unconstrained.

Example:

```
partial class Map<K,V>
    where K : IComparable<K>
    where V : IKeyProvider<K>, new()
{
    ...
}

partial class Map<K,V>
    where V : IKeyProvider<K>, new()
    where K : IComparable<K>
{
    ...
}

partial class Map<K,V>
{
    ...
}
```

is correct because those parts that include constraints (the first two) effectively specify the same set of primary, secondary, and constructor constraints for the same set of type parameters, respectively.

end example

## 15.2.6 类主体

The class_body of a class defines the members of that class.

```
class_body
    : '{' class_member_declaration* '}'
    ;
```

## 15.2.7 部分声明

The modifier partial is used when defining a class, struct, or interface type in multiple parts. The partial modifier is a contextual keyword (§6.4.4) and only has special meaning immediately before one of the keywords class, struct, or interface.

Each part of a partial type declaration shall include a partial modifier and shall be declared in the same namespace or containing type as the other parts. The partial modifier indicates that additional parts of the type declaration might exist elsewhere, but the existence of such additional parts is not a requirement; it is valid for the only declaration of a type to include the partial modifier.

All parts of a partial type shall be compiled together such that the parts can be merged at compile-time. Partial types specifically do not allow already compiled types to be extended.

Nested types can be declared in multiple parts by using the partial modifier. Typically, the containing type is declared using partial as well, and each part of the nested type is declared in a different part of the containing type.

Example: The following partial class is implemented in two parts, which reside in different compilation units. The first part is machine generated by a database-mapping tool while the second part is manually authored:

```
public partial class Customer
{
    private int id;
    private string name;
    private string address;
    private List<Order> orders;

    public Customer()
    {
        ...
    }
}

// File: Customer2.cs
public partial class Customer
{
    public void SubmitOrder(Order orderSubmitted) => orders.Add(orderSubmitted);

    public bool HasOutstandingOrders() => orders.Count > 0;
}
```

When the two parts above are compiled together, the resulting code behaves as if the class had been written as a single unit, as follows:

```
public class Customer
{
    private int id;
    private string name;
    private string address;
    private List<Order> orders;

public Customer()
{
    ...
}

public void SubmitOrder(Order orderSubmitted) => orders.Add(orderSubmitted);

public bool HasOutstandingOrders() => orders.Count > 0;
```

*end example*

The handling of attributes specified on the type or type parameters of different parts of a partial declaration is discussed in §22.3.

## 15.3 类成员

### 15.3.1 概述

The members of a class consist of the members introduced by its class_member_declarations and the members inherited from the direct base class.

```
class_member_declaration
  : constant_declaration
  | field_declaration
  | method_declaration
  | property_declaration
  | event_declaration
  | indexer_declaration
  | operator_declaration
  | constructor_declaration
  | finalizer_declaration
  | static_constructor_declaration
  | type_declaration
  ;
```

The members of a class are divided into the following categories:

- Constants, which represent constant values associated with the class (§15.4).
- Fields, which are the variables of the class (§15.5).
- Methods, which implement the computations and actions that can be performed by the class (§15.6).
- Properties, which define named characteristics and the actions associated with reading and writing those characteristics (§15.7).
- Events, which define notifications that can be generated by the class (§15.8).
- Indexers, which permit instances of the class to be indexed in the same way (syntactically) as arrays (§15.9).
- Operators, which define the expression operators that can be applied to instances of the class (§15.10).
- Instance constructors, which implement the actions required to initialize instances of the class (§15.11)
- Finalizers, which implement the actions to be performed before instances of the class are permanently discarded (§15.13).
- Static constructors, which implement the actions required to initialize the class itself (§15.12).
- Types, which represent the types that are local to the class (§14.7).

A *class_declaration* creates a new declaration space (§7.3), and the *type_parameters* and the *class_member_declarations* immediately contained by the *class_declaration* introduce new members into this declaration space. The following rules apply to *class_member_declarations*:

- Instance constructors, finalizers, and static constructors shall have the same name as the immediately enclosing class. All other members shall have names that differ from the name of the immediately enclosing class.
- The name of a type parameter in the *type_parameter_list* of a class declaration shall differ from the names of all other type parameters in the same *type_parameter_list* and shall differ from the name of the class and the names of all members of the class.
- The name of a type shall differ from the names of all non-type members declared in the same class. If two or more type declarations share the same fully qualified name, the declarations shall have the *partial* modifier (§15.2.7) and these declarations combine to define a single type.
- The name of a constant, field, property, or event shall differ from the names of all other members declared in the same class.
- The name of a method shall differ from the names of all other non-methods declared in the same class. In addition, the signature (§7.6) of a method shall differ from the signatures of all other methods declared in the same class, and two methods declared in the same class shall not have signatures that differ solely by *in*, *out*, and *ref*.
- The signature of an instance constructor shall differ from the signatures of all other instance constructors declared in the same class, and two constructors declared in the same class shall not have signatures that differ solely by *ref* and *out*.
- The signature of an indexer shall differ from the signatures of all other indexers declared in the same class.
- The signature of an operator shall differ from the signatures of all other operators declared in the same class.

The inherited members of a class (§15.3.4) are not part of the declaration space of a class.

> *Note:* Thus, a derived class is allowed to declare a member with the same name or signature as an inherited member (which in effect hides the inherited member). *end note*

The set of members of a type declared in multiple parts (§15.2.7) is the union of the members declared in each part. The bodies of all parts of the type declaration share the same declaration space (§7.3), and the scope of each member (§7.7) extends to the bodies of all of the parts. The accessibility domain of any member always includes all the parts of the enclosing type; a private member declared in one part is freely accessible from another part. It is a compile-time error to declare the same member in more than one part of the type, unless that member is a type having the *partial* modifier.

*Example:*


```
partial class A
{
    int x;                // Error, cannot declare x more than once
    partial class Inner   // Ok, Inner is a partial type
    {
        int y;
    }
}

partial class A
{
    int x;                // Error, cannot declare x more than once
    partial class Inner   // Ok, Inner is a partial type
    {
        int z;
    }
}
```

*示例结束*

在 C# 代码中，字段初始化顺序可能很重要，§15.5.6.1 提供了一些保证。除此之外，类型内成员顺序很少重要，但在与其他语言和环境交互时可能很重要。在这些情况下，在多个分部中声明的类型内成员顺序是不确定的。

## 15.3.2 实例类型

每个类声明都有一个关联的*实例类型*。对于泛型类声明，实例类型是通过从类型声明创建构造类型（§8.4）形成的，其中提供的每个类型实参都是相应的类型参数。由于实例类型使用类型参数，因此只能在类型参数处于作用域内的地方使用；即在类声明内部。对于在类声明内部编写的代码，实例类型是 `this` 的类型。对于非泛型类，实例类型就是所声明的类。

*示例：* 下面显示了几个类声明及其*实例类型*：

```
class A<T>                // instance type: A<T>
{
    class B {}             // instance type: A<T>.B
    class C<U> {}          // instance type: A<T>.C<U>
}
class D {}                // instance type: D
```

*示例结束*

## 15.3.3 构造类型的成员

构造类型的非继承成员是通过将成员声明中的每个*类型参数*替换为构造类型的相应*类型实参*而获得的。替换过程基于类型声明的语义，而不是简单的文本替换。

*示例：* 对于以下泛型类声明

```
class Gen<T,U>
{
    public T[, ] a;
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

泛型类声明 Gen 中成员 a 的类型是“T 的二维数组”，因此上述构造类型中成员 a 的类型是“int 的一维数组的二维数组”，或 int[,][]。

*示例结束*

在实例函数成员中，this 的类型是包含声明的实例类型（§15.3.2）。

泛型类的所有成员都可以直接使用任何封闭类中的类型参数，或者作为构造类型的一部分使用。当在运行时使用特定的封闭构造类型（§8.4.3）时，类型参数的每次使用都会被替换为提供给构造类型的类型实参。

示例：

```
class C<V>
{
    public V f1;
    public C<V> f2 = null;

    public C(V x)
    {
        this.f1 = x;
        this.f2 = this;
    }
}

class Application
{
    static void Main()
    {
        C<int> x1 = new C<int>(1);            // Prints 1
        Console.WriteLine(x1.f1);

        C<double> x2 = new C<double>(3.1415);   // Prints 3.1415
        Console.WriteLine(x2.f1);
    }
}
```

*示例结束*

## 15.3.4 继承

类继承其直接基类的成员。继承意味着类隐式包含其直接基类的所有成员，但基类的实例构造函数、终结器和静态构造函数除外。继承的一些重要方面如下：

- 继承是可传递的。如果 C 派生自 B，且 B 派生自 A，那么 C 既继承 B 中声明的成员，也继承 A 中声明的成员。
- 派生类扩展其直接基类。派生类可以在继承的成员基础上添加新成员，但不能移除继承成员的定义。
- 实例构造函数、终结器和静态构造函数不被继承，但所有其他成员都被继承，无论其声明的可访问性如何（§7.5）。但是，根据所声明的可访问性，继承的成员在派生类中可能不可访问。
- 派生类可以通过声明同名或相同签名的成员来隐藏（§7.7.2.3）继承的成员。但是，隐藏继承的成员并不会移除该成员——只是使得该成员无法直接通过派生类访问。
- 类的实例包含在该类及其基类中声明的所有实例字段集，并且存在从派生类类型到其任何基类类型的隐式转换（§10.2.8）。因此，对某个派生类实例的引用可以被视为对其任何基类实例的引用。
- 类可以声明虚方法、属性、索引器和事件，派生类可以重写这些函数成员的实现。这使类能够表现出多态行为，即函数成员调用所执行的操作因调用该函数成员所通过的实例的运行时类型而异。

构造类类型的继承成员是直接基类类型（§15.2.4.2）的成员，直接基类类型是通过将构造类型的类型实参替换到 base_class_specification 中相应类型参数的每次出现而找到的。这些成员又会通过将成员声明中的每个类型参数替换为 base_class_specification 的相应类型实参来进行转换。

示例：

```
class B<U>
{
    public U F(long index) {...}
}

class D<T> : B<T[]>
{
    public T G(string s) {...}
}
```

在上面的代码中，构造类型 D<int> 有一个非继承成员 public int G(string s)，这是通过将类型实参 int 替换类型参数 T 获得的。D<int> 还有来自类声明 B 的继承成员。该继承成员通过以下方式确定：首先，将基类规范 B<T[]> 中的 T 替换为 int，确定 D<int> 的基类类型 B<int[]>。然后，作为 B 的类型实参，将 int[] 替换 public U F(long index) 中的 U，得到继承成员 public int[] F(long index)。

示例结束

## 15.3.5 new 修饰符

class_member_declaration 允许声明与继承成员同名或相同签名的成员。发生这种情况时，称派生类成员隐藏基类成员。关于成员何时隐藏继承成员的精确规范，请参阅 §7.7.2.3。

如果继承成员 M 可访问，且不存在其他已隐藏 M 的继承可访问成员 N，则认为 M 可用。隐式隐藏继承成员不算错误，但会导致编译器发出警告，除非派生类成员的声明包含 new 修饰符以显式指示派生成员旨在隐藏基类成员。如果嵌套类型的分部声明（§15.2.7）的一个或多个部分包含 new 修饰符，则在嵌套类型隐藏可用继承成员时不发出警告。

如果在不隐藏可用继承成员的声明中包含了 new 修饰符，则会发出相应警告。

## 15.3.6 访问修饰符

class_member_declaration 可以具有所允许的任意一种声明可访问性（§7.5.2）：public、protected internal、protected、private protected、internal 或 private。除了 protected internal 和 private protected 组合之外，指定多个访问修饰符属于编译时错误。当 class_member_declaration 不包含任何访问修饰符时，默认为 private。

## 15.3.7 构成类型

在成员声明中使用的类型称为该成员的构成类型。可能的构成类型包括常量、字段、属性、事件或索引器的类型，方法或运算符的返回类型，以及方法、索引器、运算符或实例构造函数的参数类型。成员的构成类型应至少与该成员本身一样可访问（§7.5.5）。

## 15.3.8 静态成员和实例成员

类的成员要么是静态成员，要么是实例成员。

> 注意：一般来说，将静态成员视为属于类，将实例成员视为属于对象（类的实例）是有帮助的。结束备注

当字段、方法、属性、事件、运算符或构造函数声明包含 static 修饰符时，它声明一个静态成员。此外，常量或类型声明隐式声明静态成员。静态成员具有以下特征：

- 在形式为 E.M 的 member_access（§12.8.7）中引用静态成员 M 时，E 必须表示具有成员 M 的类型。若 E 表示实例，则属于编译时错误。
- 非泛型类中的静态字段恰好标识一个存储位置。无论创建多少个非泛型类的实例，静态字段始终只有一个副本。每个不同的封闭构造类型（§8.4.3）都有自己的静态字段集，无论封闭构造类型的实例数量是多少。
- 静态函数成员（方法、属性、事件、运算符或构造函数）不作用于特定实例，在此类函数成员中引用 this 属于编译时错误。

当字段、方法、属性、事件、索引器、构造函数或终结器声明不包含 static 修饰符时，它声明一个实例成员。（实例成员有时称为非静态成员。）实例成员具有以下特征：


-   当实例成员 M 在形式为 E.M 的成员访问 (§12.8.7) 中被引用时，E 必须表示具有成员 M 的类型的实例。E 表示一个类型时为绑定时错误。
-   每个类的实例都包含该类所有实例字段的单独副本。
-   实例函数成员（方法、属性、索引器、实例构造函数或终结器）在类的给定实例上操作，并且该实例可以作为 this (§12.8.13) 访问。

示例：以下示例说明了访问静态成员和实例成员的规则：

```
class Test
{
    int x;
    static int y;
    void F()
    {
        x = 1;        // Ok, same as this.x = 1
        y = 1;        // Ok, same as Test.y = 1
    }
    static void G()
    {
        x = 1;        // Error, cannot access this.x
        y = 1;        // Ok, same as Test.y = 1
    }
    static void Main()
    {
        Test t = new Test();
        t.x = 1;      // Ok
        t.y = 1;      // Error, cannot access static member through instance
        Test.x = 1;   // Error, cannot access instance member through type
        Test.y = 1;   // Ok
    }
}
```

F 方法表明，在实例函数成员中，可以使用简单名称 (§12.8.4) 来访问实例成员和静态成员。G 方法表明，在静态函数成员中，通过简单名称访问实例成员是编译时错误。Main 方法表明，在成员访问 (§12.8.7) 中，实例成员应通过实例访问，而静态成员应通过类型访问。

结束示例

## 15.3.9 嵌套类型

### 15.3.9.1 通用

在类或结构体内部声明的类型称为嵌套类型。在编译单元或命名空间内部声明的类型称为非嵌套类型。

示例：在以下示例中：

```
class A
{
    class B
    {
        static void F()
        {
            Console.WriteLine("A.B.F");
        }
    }
}
```

class B 是嵌套类型，因为它在 class A 内部声明，而 class A 是非嵌套类型，因为它在编译单元内部声明。

结束示例

### 15.3.9.2 完全限定名

嵌套类型声明的完全限定名 (§7.8.3) 为 S.N，其中 S 是声明类型 N 的类型声明的完全限定名，而 N 是嵌套类型声明的非限定名 (§7.8.2)（包括任何 generic_dimension_specifier (§12.8.17)）。

### 15.3.9.3 声明的可访问性

非嵌套类型可以具有 public 或 internal 声明的可访问性，并且默认具有 internal 声明的可访问性。嵌套类型也可以具有这些形式的声明可访问性，再加上一种或多种额外的声明可访问性形式，具体取决于包含的类型是类还是结构体：

-   声明在类中的嵌套类型可以具有任何允许的声明可访问性种类，并且与其它类成员一样，默认声明可访问性为 private。
-   声明在结构体中的嵌套类型可以具有三种声明可访问性形式中的任意一种（public、internal 或 private），并且与其它结构体成员一样，默认声明可访问性为 private。

示例：示例

```
public class List
{
    // Private data structure
    private class Node
    {
        public object Data;
        public Node Next;

        public Node(object data, Node next)
        {
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

声明了一个私有嵌套类 Node。

结束示例

### 15.3.9.4 隐藏

嵌套类型可能会隐藏 (§7.7.2.2) 基成员。new 修饰符 (§15.3.5) 允许用于嵌套类型声明，以便可以显式表达隐藏。

示例：示例

```
class Base
{
    public static void M()
    {
        Console.WriteLine("Base.M");
    }
}

class Derived: Base
{
    public new class M
    {
        public static void F()
        {
            Console.WriteLine("Derived.M.F");
        }
    }
}

class Test
{
    static void Main()
    {
        Derived.M.F();
    }
}
```

显示了一个嵌套类 M，它隐藏了在 Base 中定义的方法 M。

结束示例

### 15.3.9.5 this 访问

嵌套类型与其包含的类型在 this_access (§12.8.13) 方面没有特殊关系。具体来说，嵌套类型中的 this 不能用于引用包含类型的实例成员。在嵌套类型需要访问其包含类型的实例成员的情况下，可以通过将包含类型实例的 this 作为嵌套类型的构造函数参数来提供访问。

示例：以下示例

```
class C
{
    int i = 123;
    public void F()
    {
        Nested n = new Nested(this);
        n.G();
    }
}

public class Nested
{
    C this_c;

    public Nested(C c)
    {
        this_c = c;
    }

    public void G()
    {
        Console.WriteLine(this_c.i);
    }
}

class Test
{
    static void Main()
    {
        C c = new C();
        c.F();
    }
}
```

展示了此技术。C 的一个实例创建 Nested 的一个实例，并将其自己的 this 传递给 Nested 的构造函数，以便随后访问 C 的实例成员。

结束示例

### 15.3.9.6 访问包含类型的私有和受保护成员

嵌套类型可以访问其包含类型可访问的所有成员，包括具有 private 和 protected 声明可访问性的包含类型的成员。

示例：示例

```
class C
{
    private static void F() => Console.WriteLine("C.F");

    public class Nested
    {
        public static void G() => F();
    }
}
class Test
{
    static void Main() => C.Nested.G();
}
```

显示了一个包含嵌套类 Nested 的类 C。在 Nested 内部，方法 G 调用在 C 中定义的静态方法 F，而 F 具有 private 声明可访问性。

结束示例

嵌套类型也可以访问其包含类型的基类型中定义的受保护成员。

示例：在以下代码中

```
class Base
{
    protected void F() => Console.WriteLine("Base.F");
}

class Derived: Base
{
    public class Nested
    {
        public void G()
        {
            Derived d = new Derived();
            d.F(); // ok
        }
    }
}

class Test
{
    static void Main()
    {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```

嵌套类 Derived.Nested 通过通过 Derived 的实例调用的方式，访问在 Derived 的基类 Base 中定义的受保护方法 F。

结束示例

### 15.3.9.7 泛型类中的嵌套类型

泛型类声明可能包含嵌套类型声明。封闭类的类型参数可在嵌套类型中使用。嵌套类型声明可能包含仅适用于该嵌套类型的附加类型参数。

包含在泛型类声明中的每个类型声明都隐式为泛型类型声明。当编写对嵌套在泛型类型中的类型的引用时，必须命名包含的构造类型，包括其类型参数。然而，从外部类内部，嵌套类型可以不加限定地使用；在构造嵌套类型时，外部类的实例类型可以被隐式使用。

示例：以下显示了引用从 Inner 创建的构造类型的三种不同正确方法；前两种是等效的：

```
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }
    static void F(T t)
    {
        Outer<T>.Inner<string>.F(t, "abc");    // These two statements have
        Inner<string>.F(t, "abc");            // the same effect
        Outer<int>.Inner<string>.F(3, "abc"); // This type is different
        Outer.Inner<string>.F(t, "abc");      // Error, Outer needs type arg
    }
}
```

结束示例

尽管这是不良的编程风格，但嵌套类型中的类型参数可以隐藏在外部类型中声明的成员或类型参数。

示例：

```
class Outer<T>
{
    class Inner<T>                     // Valid, hides Outer's T
    {
        public T t;                    // Refers to Inner's T
    }
}
```

结束示例

## 15.3.10 保留成员名称

### 15.3.10.1 通用

为了便于底层 C# 运行时实现，对于每个源成员声明为属性、事件或索引器的情况，实现必须基于成员声明的种类、其名称和其类型保留两个方法签名 (§15.3.10.2、§15.3.10.3、§15.3.10.4)。如果程序声明的成员签名与同一作用域中声明的成员保留的签名匹配，则为编译时错误，即使底层运行时实现未使用这些保留。

保留的名称不引入声明，因此它们不参与成员查找。然而，声明的关联保留方法签名确实参与继承 (§15.3.4)，并且可以使用 new 修饰符 (§15.3.5) 进行隐藏。

注意：这些名称的保留服务于三个目的：

-   1. 允许底层实现使用普通标识符作为方法名，以便对 C# 语言特性进行 get 或 set 访问。
-   2. 允许其他语言使用普通标识符作为方法名，以便对 C# 语言特性进行 get 或 set 访问，从而实现互操作。
-   3. 通过使所有 C# 实现中的保留成员名称的具体细节保持一致，帮助确保一个符合规范的编译器接受的源代码会被另一个接受。

结束注意

终结器 (§15.13) 的声明也会导致一个签名被保留 (§15.3.10.5)。

### 15.3.10.2 为属性保留的成员名称

对于类型为 T 的属性 P (§15.7)，以下签名被保留：

```csharp
T get_P();
void set_P(T value);
```

即使属性是只读或只写的，这两个签名也都会保留。

*示例：在以下代码中*

```csharp
class A
{
    public int P
    {
        get => 123;
    }
}

class B : A
{
    public new int get_P() => 456;

    public new void set_P(int value)
    {
    }
}

class Test
{
    static void Main()
    {
        B b = new B();
        A a = b;
        Console.WriteLine(a.P);
        Console.WriteLine(b.P);
        Console.WriteLine(b.get_P());
    }
}
```

类 A 定义了一个只读属性 P，因此保留了 get_P 和 set_P 方法的签名。类 B 从 A 派生，并隐藏了这两个保留的签名。该示例产生以下输出：

```
123
123
456
```

*示例结束*

### 15.3.10.3 为事件保留的成员名称

对于委托类型 T 的事件 E（§15.8），保留以下签名：

```csharp
void add_E(T handler);
void remove_E(T handler);
```

### 15.3.10.4 为索引器保留的成员名称

对于类型为 T、参数列表为 L 的索引器（§15.9），保留以下签名：

```csharp
T get_Item(L);
void set_Item(L, T value);
```

即使索引器是只读或只写的，这两个签名也都会保留。

此外，成员名称 Item 是保留的。

## 15.3.10.5 为终结器保留的成员名称

对于包含终结器（§15.13）的类，保留以下签名：

```csharp
void Finalize();
```

## 15.4 常量

常量是一种类成员，它表示一个常量值：即可以在编译时计算的值。constant_declaration 引入一个或多个给定类型的常量。

```
constant_declaration
: attributes? constant_modifier* 'const' type constant_declarators ';'
;
```

```
constant_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
;
```

constant_declaration 可以包含一组特性（§22）、一个 new 修饰符（§15.3.5），以及允许的已声明可访问性中的任意一种（§15.3.6）。特性和修饰符适用于该 constant_declaration 声明的所有成员。尽管常量被视为静态成员，但 constant_declaration 既不要求也不允许使用 static 修饰符。同一个修饰符在常量声明中出现多次是错误的。

constant_declaration 的类型指定该声明引入的成员的类型。类型之后是 constant_declarators 列表（§13.6.3），其中每个声明符引入一个新成员。constant_declarator 由命名该成员的标识符、后跟一个“=”标记、再后跟一个给出该成员值的 constant_expression（§12.23）组成。

常量声明中指定的类型应为 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool、string、enum_type 或 reference_type。每个 constant_expression 应产生目标类型的值，或产生可通过隐式转换（§10.2）转换为目标类型的类型的值。

> 注意：此类构造的示例包括 case 标签、goto case 语句、枚举成员声明、特性以及其他常量声明。注结束

> 注意：如 §12.23 所述，constant_expression 是可在编译时完全求值的表达式。由于创建 string 以外的 reference_type 的非 null 值的唯一方式是应用 new 运算符，并且 constant_expression 中不允许使用 new 运算符，因此 string 以外的 reference_type 常量唯一可能的值是 null。注结束

当需要为常量值使用符号名称，但该值的类型不允许出现在常量声明中，或者该值无法由 constant_expression 在编译时计算时，可以改用只读字段（§15.5.3）。

> 注意：const 和 readonly 的版本控制语义不同（§15.5.3.3）。注结束

声明多个常量的一个常量声明等价于多个具有相同特性、修饰符和类型的单个常量声明。

示例：

```
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```

等价于

```
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

示例结束

只要依赖关系不是循环的，就允许常量依赖于同一程序中的其他常量。编译器会自动按适当的顺序安排常量声明的求值。

示例：在以下代码中

```
class A
{
    public const int X = B.Z + 1;
    public const int Y = 10;
}

class B
{
    public const int Z = A.Y + 1;
}
```

编译器先对 A.Y 求值，然后对 B.Z 求值，最后对 A.X 求值，得到的值分别为 10、11 和 12。

示例结束

常量声明可以依赖其他程序中的常量，但这种依赖只能是一个方向上的。

示例：参照上面的示例，如果 A 和 B 声明在不同的程序中，则 A.X 可以依赖 B.Z，但此时 B.Z 不能同时依赖 A.Y。示例结束

## 15.5 字段

### 15.5.1 概述

字段是一种成员，它表示与对象或类关联的变量。field_declaration 引入一个或多个给定类型的字段。

```
field_declaration
  : attributes? field_modifier* type variable_declarators ';'
  ;
```

```
field_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'static'
  | 'readonly'
  | 'volatile'
  | unsafe_modifier  // unsafe code support
  ;
```

```
variable_declarators
  : variable_declarator (',' variable_declarator)*
  ;
```

```
variable_declarator
  : identifier ('=' variable_initializer)?
  ;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

field_declaration 可以包含一组特性（§22）、一个 new 修饰符（§15.3.5）、四个访问修饰符的有效组合（§15.3.6）以及一个 static 修饰符（§15.5.2）。此外，field_declaration 可以包含 readonly 修饰符（§15.5.3）或 volatile 修饰符（§15.5.4），但不能同时包含两者。特性和修饰符适用于该 field_declaration 声明的所有成员。同一个修饰符在 field_declaration 中出现多次是错误的。

field_declaration 的类型指定该声明引入的成员的类型。类型之后是 variable_declarators 列表，其中每个声明符引入一个新成员。variable_declarator 由命名该成员的标识符组成，后面可选地跟一个“=”标记和一个给出该成员初始值的 variable_initializer（§15.5.6）。

字段的类型应至少与字段本身一样可访问（§7.5.5）。

在表达式中，可以使用 simple_name（§12.8.4）、member_access（§12.8.7）或 base_access（§12.8.14）获取字段的值。非只读字段的值使用赋值（§12.21）进行修改。

非只读字段的值既可以使用后缀递增和递减运算符（§12.8.15）获取和修改，也可以使用前缀递增和递减运算符（§12.9.6）获取和修改。

声明多个字段的一个字段声明等价于多个具有相同特性、修饰符和类型的单个字段声明。

示例：

```
class A
{
    public static int X = 1, Y, Z = 100;
}
```

等价于

```
class A
{
    public static int X = 1;
    public static int Y;
    public static int Z = 100;
}
```

示例结束

### 15.5.2 静态字段和实例字段

当字段声明包含 static 修饰符时，该声明引入的字段是静态字段。当不存在 static 修饰符时，该声明引入的字段是实例字段。静态字段和实例字段是 C# 支持的几种变量（§9）中的两种，有时分别称为静态变量和实例变量。

如 §15.3.8 所述，类的每个实例都包含该类的一整套实例字段，而每个非泛型类或封闭构造类型只有一组静态字段，无论该类或封闭构造类型有多少个实例。

### 15.5.3 只读字段

### 15.5.3.1 概述

当 field_declaration 包含 readonly 修饰符时，该声明引入的字段是只读字段。对只读字段的直接赋值只能作为该声明的一部分，或在同一个类中的实例构造函数或静态构造函数中进行。（在这些上下文中，可以对只读字段进行多次赋值。）具体而言，只有在以下上下文中才允许对只读字段进行直接赋值：

- 在引入该字段的 variable_declarator 中（通过在声明中包含 variable_initializer）。
- 对于实例字段，在包含该字段声明的类的实例构造函数中；对于静态字段，在包含该字段声明的类的静态构造函数中。这些也是唯一可以将只读字段作为 out 或 ref 参数传递的有效上下文。

在任何其他上下文中尝试对只读字段赋值或将其作为 out 或 ref 参数传递，都是编译时错误。

### 15.5.3.2 使用静态只读字段表示常量

当需要为常量值使用符号名称，但该值的类型不允许出现在 const 声明中，或者该值无法在编译时计算时，静态只读字段很有用。

示例：在以下代码中

```
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
}
```



```
public static readonly Color Red = new Color(255, 0, 0);
public static readonly Color Green = new Color(0, 255, 0);
public static readonly Color Blue = new Color(0, 0, 255);

private byte red, green, blue;

public Color(byte r, byte g, byte b)
{
    red = r;
    green = g;
    blue = b;
}
```

Black、White、Red、Green 和 Blue 成员不能声明为 const 成员，因为它们的值无法在编译时计算。不过，将它们改为声明为 static readonly 具有大致相同的效果。

*示例结束*

## 15.5.3.3 常量和静态只读字段的版本控制

常量和只读字段具有不同的二进制版本控制语义。当表达式引用常量时，常量的值在编译时获取；但当表达式引用只读字段时，字段的值要到运行时才获取。

示例：考虑一个由两个独立程序组成的应用程序：

```
namespace Program1
{
    public class Utils
    {
        public static readonly int x = 1;
    }
}

以及

namespace Program2
{
    class Test
    {
        static void Main()
        {
            Console.WriteLine(Program1.Utils.X);
        }
    }
}
```

Program1 和 Program2 命名空间表示两个分别编译的程序。由于 Program1.Utils.X 被声明为 static readonly 字段，`Console.WriteLine` 语句输出的值在编译时未知，而是在运行时获取。因此，如果 X 的值发生更改并重新编译 Program1，那么即使 Program2 未重新编译，`Console.WriteLine` 语句也会输出新值。然而，如果 X 是常量，那么 X 的值本会在编译 Program2 时获取，并且在重新编译 Program2 之前，不会受到 Program1 中更改的影响。

*示例结束*

## 15.5.4 易失字段

当字段声明（field_declaration）包含 volatile 修饰符时，该声明引入的字段为易失字段。对于非易失字段，重排指令的优化技术可能会在访问字段时未使用同步（例如 lock 语句（lock_statement）（§13.13）提供的同步）的多线程程序中导致意外且不可预测的结果。这些优化可以由编译器、运行时系统或硬件执行。对于易失字段，此类重排优化受到限制：

- 对易失字段的读取称为易失读取。易失读取具有“获取语义”（acquire semantics）；也就是说，它保证发生在指令序列中位于其后的任何内存引用之前。
- 对易失字段的写入称为易失写入。易失写入具有“释放语义”（release semantics）；也就是说，它保证发生在指令序列中位于写入指令之前的任何内存引用之后。

这些限制确保所有线程都将按照其他任何线程执行易失写入的顺序观察到这些写入。符合规范的实现不要求从所有执行线程的角度为易失写入提供单一全序。易失字段的类型应为以下之一：

- 一个引用类型（reference_type）。
- 一个已知为引用类型的类型参数（type_parameter）（§15.2.5）。
- 类型 byte、sbyte、short、ushort、int、uint、char、float、bool、System.IntPtr 或 System.UIntPtr。
- 一个枚举类型（enum_type），其枚举基类型（enum_base）为 byte、sbyte、short、ushort、int 或 uint。

示例：以下示例

```
class Test
{
    public static int result;
    public static volatile bool finished;

    static void Thread2()
    {
        result = 143;
        finished = true;
    }

    static void Main()
    {
        finished = false;

        // Run Thread2() in a new thread
        new Thread(new ThreadStart(Thread2)).Start();

        // Wait for Thread2() to signal that it has a result
        // by setting finished to true.
        for (;;)
        {
            if (finished)
            {
                Console.WriteLine($"result = {result}");
                return;
            }
        }
    }
}
```

生成输出：

```
result = 143
```

在此示例中，方法 Main 启动一个新线程来运行方法 Thread2。此方法将一个值存入名为 result 的非易失字段，然后将 true 存入易失字段 finished。主线程等待字段 finished 被设置为 true，然后读取字段 result。由于 finished 已声明为 volatile，主线程应从字段 result 读取值 143。如果字段 finished 未声明为 volatile，那么允许对 result 的存储在对 finished 的存储之后才对主线程可见，因此主线程可能从字段 result 读取值 0。将 finished 声明为易失字段可防止任何此类不一致。

*示例结束*

## 15.5.5 字段初始化

字段的初始值，无论是静态字段还是实例字段，都是该字段类型的默认值（§9.3）。在发生此默认初始化之前，不可能观察到字段的值，因此字段永远不会处于“未初始化”状态。

*示例：以下示例*

```csharp
class Test
{
    static bool b;
    int i;

    static void Main()
    {
        Test t = new Test();
        Console.WriteLine($"b = {b}, i = {t.i}");
    }
}
```

生成输出

```
b = False, i = 0
```

因为 b 和 i 都被自动初始化为默认值。

*示例结束*

## 15.5.6 变量初始化器

### 15.5.6.1 一般

字段声明可以包含 *变量初始化器*。对于静态字段，变量初始化器对应于在类初始化期间执行的赋值语句。对于实例字段，变量初始化器对应于在创建类的实例时执行的赋值语句。

示例：以下示例

```
class Test
{
    static double x = Math.Sqrt(2.0);
    int i = 100;
    string s = "Hello";

    static void Main()
    {
        Test a = new Test();
        Console.WriteLine($"x = {x}, i = {a.i}, s = {a.s}");
    }
}
```

生成输出

x = 1.4142135623730951, i = 100, s = Hello

因为对 x 的赋值在静态字段初始化器执行时发生，而对 i 和 s 的赋值在实例字段初始化器执行时发生。

示例结束

§15.5.5 中描述的默认值初始化适用于所有字段，包括具有变量初始化器的字段。因此，当初始化一个类时，该类中的所有静态字段首先初始化为其默认值，然后按文本顺序执行静态字段初始化器。同样，当创建类的实例时，该实例中的所有实例字段首先初始化为其默认值，然后按文本顺序执行实例字段初始化器。当同一类型的多个分部类型声明中存在字段声明时，各部分之间的顺序未指定。但是，在每个部分内，字段初始化器按顺序执行。

具有变量初始化器的静态字段可能会在其默认值状态下被观察到。

示例：但是，从风格上强烈不建议这样做。以下示例

```
class Test
{
    static int a = b + 1;
    static int b = a + 1;

    static void Main()
    {
        Console.WriteLine($"a = {a}, b = {b}");
    }
}
```

展示了这种行为。尽管 a 和 b 的定义存在循环，该程序仍是有效的。它产生输出

a = 1, b = 2

因为静态字段 a 和 b 在其初始化器执行之前被初始化为 0（int 的默认值）。当 a 的初始化器运行时，b 的值为零，因此 a 被初始化为 1。当 b 的初始化器运行时，a 的值已经是 1，因此 b 被初始化为 2。

*示例结束*

### 15.5.6.2 静态字段初始化

类的静态字段变量初始化器对应于一系列赋值，这些赋值按它们在类声明中出现的文本顺序执行（§15.5.6.1）。在分部类中，“文本顺序”的含义由 §15.5.6.1 规定。如果类中存在静态构造函数（§15.12），则静态字段初始化器的执行紧接在执行该静态构造函数之前发生。否则，静态字段初始化器在首次使用该类的静态字段之前的某个依赖于实现的时刻执行。

示例：以下示例

```
class Test
{
    static void Main()
    {
        Console.WriteLine($"{B.Y} {A.X}");
    }

    public static int F(string s)
    {
        Console.WriteLine(s);
        return 1;
    }
}

class A
{
    public static int X = Test.F("Init A");
}

class B
{
    public static int Y = Test.F("Init B");
}
```

可能产生以下输出之一：

Init A
Init B
1 1

或输出：

Init B
Init A
1 1

因为 X 的初始化器和 Y 的初始化器的执行可以以任意顺序发生；它们只被约束为在这些字段的引用之前发生。然而，在以下示例中：

```
class Test
{
    static void Main()
    {
        Console.WriteLine($"{B.Y} {A.X}");
    }
}
```


```
public static int F(string s)
{
    Console.WriteLine(s);
    return 1;
}
```

```
class A
{
    static A() {}
    public static int X = Test.F("Init A");
}
```

```
class B
{
    static B() {}
    public static int Y = Test.F("Init B");
}
```

输出应为：

Init B
Init A
1 1

因为静态构造函数何时执行的规则（如 §15.12 所定义）规定，B 的静态构造函数（因而 B 的静态字段初始化器）应先于 A 的静态构造函数和字段初始化器运行。

示例结束

## 15.5.6.3 实例字段初始化

类的实例字段变量初始化器对应于一系列赋值，这些赋值在进入该类的任一实例构造函数（§15.11.3）时立即执行。在分部类中，“文本顺序”的含义由 §15.5.6.1 规定。变量初始化器按其在类声明（§15.5.6.1）中出现的文本顺序执行。类实例创建和初始化过程在 §15.11 中进一步描述。

实例字段的变量初始化器不能引用正在创建的实例。因此，在变量初始化器中引用 this 是编译时错误，正如变量初始化器通过 simple_name 引用任何实例成员也是编译时错误。

示例：在以下代码中

```
class A
{
    int x = 1;
    int y = x + 1;    // Error, reference to instance member of this
}
```

y 的变量初始化器导致编译时错误，因为它引用了正在创建的实例的成员。

示例结束

## 15.6 方法

### 15.6.1 概述

**方法**是实现可由对象或类执行的计算或操作的成员。方法使用 method_declarations 声明：

```
method_declaration
    : attributes? method_modifiers return_type method_header method_body
    | attributes? ref_method_modifiers ref_kind ref_return_type method_header
      ref_method_body
    ;
```

```
method_modifiers
    : method_modifier* 'partial'?
    ;
```

```
ref_kind
    : 'ref'
    | 'ref' 'readonly'
    ;
```

```
ref_method_modifiers
    : ref_method_modifier*
    ;
```

```
method_header
    : member_name '(' formal_parameter_list? ')'
    | member_name type_parameter_list '(' formal_parameter_list? ')'
      type_parameter_constraints_clause*
    ;
```

```
method_modifier
    : ref_method_modifier
    | 'async'
    ;
```

```
ref_method_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | unsafe_modifier  // unsafe code support
    ;
```

```
return_type
    : ref_return_type
    | 'void'
    ;
```

```
ref_return_type
  : type
  ;

member_name
  : identifier
  | interface_type '.' identifier
  ;

method_body
  : block
  | '=>' null_conditional_invocation_expression ';'
  | '=>' expression ';'
  | ';'
  ;

ref_method_body
  : block
  | '=>' 'ref' variable_reference ';'
  | ';'
  ;
```

语法说明：

- unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。
- 在识别 method_body 时，如果 null_conditional_invocation_expression 和 expression 两个备选项都适用，则应选择前者。

> 注：此处各备选项的重叠及优先级仅出于描述方便；可以细化语法规则以消除重叠。ANTLR 及其他语法系统采用同样的便利方式，因此 method_body 会自动具有指定的语义。注释结束

method_declaration 可包含一组特性（§22）、所允许的声明可访问性种类之一（§15.3.6），以及 new（§15.3.5）、static（§15.6.3）、virtual（§15.6.4）、override（§15.6.5）、sealed（§15.6.6）、abstract（§15.6.7）、extern（§15.6.8）和 async（§15.15）修饰符。

如果以下所有条件均为真，则声明具有有效的修饰符组合：

- 声明包含有效的访问修饰符组合（§15.3.6）。
- 声明不多次包含同一修饰符。
- 声明最多包含以下修饰符之一：static、virtual 和 override。
- 声明最多包含以下修饰符之一：new 和 override。
- 如果声明包含 abstract 修饰符，则声明不包含以下任何修饰符：static、virtual、sealed 或 extern。
- 如果声明包含 private 修饰符，则声明不包含以下任何修饰符：virtual、override 或 abstract。
- 如果声明包含 sealed 修饰符，则声明还包含 override 修饰符。
- 如果声明包含 partial 修饰符，则它不包含以下任何修饰符：new、public、protected、internal、private、virtual、sealed、override、abstract 或 extern。

方法根据其返回内容（如果有）进行分类：

- 如果存在 ref，则该方法为按引用返回（returns-by-ref），并返回一个变量引用，该引用可选为只读；
- 否则，如果 return_type 为 void，则该方法为无值返回（returns-no-value），并且不返回值；
- 否则，该方法为按值返回（returns-by-value），并返回一个值。

按值返回或无值返回的方法声明的 return_type 指定该方法返回的结果类型（如果有）。只有无值返回方法可以包含 partial 修饰符（§15.6.9）。如果声明包含 async 修饰符，则 return_type 应为 void，或者该方法为按值返回且返回类型为任务类型（§15.15.1）。

按引用返回的方法声明的 ref_return_type 指定该方法返回的 variable_reference 所引用的变量类型。

泛型方法是其声明包含 type_parameter_list 的方法。这指定方法的类型参数。可选的 type_parameter_constraints_clauses 指定类型参数的约束。

显式接口成员实现的泛型 method_declaration 不得具有任何 type_parameter_constraints_clauses；该声明从接口方法的约束继承任何约束。

类似地，带有 override 修饰符的方法声明不得具有任何 type_parameter_constraints_clauses，并且该方法类型参数的约束从被重写的虚方法继承。

member_name 指定方法的名称。除非方法是显式接口成员实现（§18.6.2），否则 member_name 只是一个标识符。

对于显式接口成员实现，member_name 由 interface_type 后跟一个 '.' 和一个标识符组成。在这种情况下，声明除（可能的）extern 或 async 外不得包含任何修饰符。

可选的 formal_parameter_list 指定方法的参数（§15.6.2）。

方法的 return_type 或 ref_return_type，以及 formal_parameter_list 中引用的每个类型，其可访问性至少应与方法本身相同（§7.5.5）。

按值返回或无值返回的方法的 method_body 可以是分号、块体或表达式体。块体由一个块组成，该块指定调用方法时要执行的语句。表达式体由 => 后跟 null_conditional_invocation_expression 或 expression，再跟一个分号组成，表示调用方法时要执行的单个表达式。

对于 abstract 和 extern 方法，method_body 仅由分号组成。对于 partial 方法，method_body 可以由分号、块体或表达式体组成。对于所有其他方法，method_body 是块体或表达式体。

如果 method_body 由分号组成，则声明不得包含 async 修饰符。

按引用返回的方法的 ref_method_body 可以是分号、块体或表达式体。块体由一个块组成，该块指定在方法被……时要执行的语句。


被调用时。表达式主体由 `=>` 后跟 `ref`、一个变量引用（variable_reference）和一个分号组成，表示在方法被调用时要计算的单个变量引用。

对于抽象方法和外部方法，ref_method_body 仅由一个分号组成；对于所有其他方法，ref_method_body 要么是块主体，要么是表达式主体。

方法的名称、类型参数的数量和形参列表定义方法的签名（§7.6）。具体而言，方法的签名由名称、类型参数的数量，以及形参的数量、参数模式修饰符（§15.6.2.1）和形参类型组成。返回类型不属于方法签名的组成部分，形参名称、类型参数名称或约束也不属于。当形参类型引用方法的类型参数时，使用该类型参数的序号位置（而非类型参数的名称）来确定类型等效性。

方法的名称必须与同一类中声明的所有其他非方法成员的名称不同。此外，方法的签名必须与同一类中声明的所有其他方法的签名不同，并且同一类中声明的两个方法的签名不能仅因 `in`、`out` 和 `ref` 而不同。

方法的 type_parameters 在整个方法声明（method_declaration）范围内处于作用域中，并且可在该作用域内的 return_type 或 ref_return_type、method_body 或 ref_method_body 以及 type_parameter_constraints_clauses 中用于构造类型，但不能在特性（attribute）中使用。

所有形参和类型参数的名称都必须不同。

## 15.6.2 方法参数

### 15.6.2.1 概述

方法的参数（如果有）通过方法的 formal_parameter_list 声明。

```
formal_parameter_list
  : fixed_parameters
  | fixed_parameters ',' parameter_array
  | parameter_array
  ;

fixed_parameters
  : fixed_parameter (',' fixed_parameter)*
  ;

fixed_parameter
  : attributes? parameter_modifier? type identifier default_argument?
  ;

default_argument
  : '=' expression
  ;

parameter_modifier
  : parameter_mode_modifier
  | 'this'
  ;

parameter_mode_modifier
  : 'ref'
  | 'out'
  | 'in'
  ;

parameter_array
: attributes? 'params' array_type identifier
;
```

形参列表由一个或多个逗号分隔的参数组成，其中只有最后一个可以是 parameter_array。

fixed_parameter 由一组可选的特性（§22）、一个可选的 `in`、`out`、`ref` 或 `this` 修饰符、一个类型、一个标识符和一个可选的 default_argument 组成。每个 fixed_parameter 以给定名称声明一个给定类型的参数。`this` 修饰符将方法指定为扩展方法，并且仅允许出现在非泛型、非嵌套静态类中静态方法的第一个参数上。如果参数是结构类型或受结构约束的类型参数，则 `this` 修饰符可以与 `ref` 或 `in` 修饰符结合，但不能与 `out` 修饰符结合。扩展方法在 §15.6.10 中进一步描述。带 default_argument 的 fixed_parameter 称为可选参数，而不带 default_argument 的 fixed_parameter 是必需参数。在 formal_parameter_list 中，必需参数不能出现在可选参数之后。

具有 `ref`、`out` 或 `this` 修饰符的参数不能有 default_argument。具有 `in` 修饰符的参数可以有 default_argument。default_argument 中的表达式必须是以下之一：

- 一个 constant_expression（常量表达式）
- 形式为 new S() 的表达式，其中 S 是值类型
- 形式为 default(S) 的表达式，其中 S 是值类型

该表达式必须能通过恒等转换或可空转换隐式转换为参数的类型。

如果可选参数出现在实现分部方法声明（§15.6.9）、显式接口成员实现（§18.6.2）、单参数索引器声明（§15.9）或运算符声明（§15.10.1）中，编译器应给出警告，因为这些成员永远不会以允许省略参数的方式被调用。

parameter_array 由一组可选的特性（§22）、一个 `params` 修饰符、一个 array_type 和一个标识符组成。参数数组以给定名称声明一个给定数组类型的参数。参数数组的 array_type 必须是单维数组类型（§17.2）。在方法调用中，参数数组允许指定给定数组类型的单个参数，也允许指定数组元素类型的零个或多个参数。参数数组在 §15.6.2.6 中进一步描述。

parameter_array 可以出现在可选参数之后，但不能具有默认值——省略 parameter_array 的参数将导致创建一个空数组。

示例：以下代码演示不同类型的参数：

```
void M<T>(
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

在 M 的 formal_parameter_list 中，i 是必需的 ref 参数，d 是必需的值参数，b、s、o 和 t 是可选的值参数，a 是参数数组。
示例结束

方法声明为参数和类型参数创建单独的声明空间（§7.3）。名称通过方法的类型参数列表和形参列表引入此声明空间。方法的主体（如果有）被视为嵌套在此声明空间内。方法声明空间的两个成员具有相同名称是错误的。方法声明空间与嵌套声明空间的局部变量声明空间包含同名元素也是错误的。

方法调用（§12.8.9.2）会创建该方法形参和局部变量的副本，该副本特定于该调用；调用的参数列表将值或变量引用赋给新创建的形参。在方法块内，形参可以通过其标识符在 simple_name 表达式（§12.8.4）中引用。

存在以下种类的形参：
- 值参数（value parameter），声明时不带任何修饰符。
- 输入参数（input parameter），使用 `in` 修饰符声明。
- 输出参数（output parameter），使用 `out` 修饰符声明。
- 引用参数（reference parameter），使用 `ref` 修饰符声明。
- 参数数组（parameter array），使用 `params` 修饰符声明。

注意：如 §7.6 所述，`in`、`out` 和 `ref` 修饰符是方法签名的一部分，但 `params` 修饰符不是。注记结束

### 15.6.2.2 值参数

不带任何修饰符声明的参数是值参数。值参数是一种局部变量，其初始值来自方法调用中提供的相应实参。

当形参是值参数时，方法调用中对应的实参必须是可隐式转换（§10.2）为形参类型的表达式。

方法允许向值参数赋予新值。此类赋值仅影响由该值参数表示的本地存储位置，对方法调用中提供的实际实参没有影响。

### 15.6.2.3 输入参数

使用 `in` 修饰符声明的参数是输入参数。输入参数是局部引用变量（§9.7），其初始引用对象来自方法调用中提供的相应实参。该实参要么是方法调用时已存在的变量，要么是方法调用中由实现创建（§12.6.2.3）的变量。

注意：与引用变量一样，可以使用 ref 赋值（= ref）运算符更改输入参数的引用对象，但无法更改引用对象本身存储的值。注记结束



当形参是输入参数时，方法调用中对应的实参应由以下之一组成：关键字 in 后跟一个与形参类型相同的 variable_reference（§9.2.8），或者一个表达式，该实参表达式到对应参数的类型存在隐式转换（§10.2）。变量在作为输入参数传递之前必须明确赋值。

修改输入参数的值是编译时错误。

在方法内部，输入参数始终被视为已明确赋值。

声明为迭代器（§15.14）或异步函数（§15.15）的函数上不允许使用输入参数。

在采用输入参数的方法中，多个名称可能表示同一存储位置。

## 15.6.2.4 引用参数

使用 ref 修饰符声明的参数是引用参数。引用参数是局部引用变量（§9.7），其初始引用对象来自方法调用中提供的对应实参。

> 注意：与引用变量一样，引用参数的引用对象可以使用 ref 赋值（= ref）运算符更改。注释结束

当形参是引用参数时，方法调用中对应的实参应由关键字 ref 后跟一个与形参类型相同的 variable_reference（§9.5）组成。变量在作为引用参数传递之前必须明确赋值。

在方法内部，引用参数始终被视为已明确赋值。

声明为迭代器（§15.14）的方法不能有引用参数。

示例：以下示例

```
class Test
{
    static void Swap(ref int x, ref int y)
    {
        int temp = x;
        x = y;
        y = temp;
    }

    static void Main()
    {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine($"i = {i}, j = {j}");
    }
}
```

生成以下输出

i = 2, j = 1

对于 Main 中对 Swap 的调用，x 表示 i，y 表示 j。因此，该调用具有交换 i 和 j 的值的效果。

示例结束

在采用引用参数的方法中，多个名称可能表示同一存储位置。

示例：在以下代码中

```csharp
class A
{
    string s;
    void F(ref string a, ref string b)
    {
        s = "One";
        a = "Two";
        b = "Three";
    }

    void G()
    {
        F(ref s, ref s);
    }
}
```

G 中对 F 的调用为 a 和 b 都传递了对 s 的引用。因此，对于该调用，名称 s、a 和 b 都引用同一存储位置，并且这三个赋值都修改实例字段 s。

示例结束

## 15.6.2.5 输出参数

使用 out 修饰符声明的参数是输出参数。输出参数是局部引用变量（§9.7），其初始引用对象来自方法调用中提供的对应实参。

当形参是输出参数时，方法调用中对应的实参应由关键字 out 后跟一个与形参类型相同的 variable_reference（§9.5）组成。变量在作为输出参数传递之前不必明确赋值，但在将变量作为输出参数传递的调用之后，该变量被视为已明确赋值。

在方法内部，与局部变量一样，输出参数最初被视为未赋值，并且在其值被使用之前必须明确赋值。

方法的每个输出参数都必须在该方法返回之前明确赋值。

声明为分部方法（§15.6.9）或迭代器（§15.14）的方法不能有输出参数。

输出参数通常用于生成多个返回值的方法。

示例：

```csharp
class Test
{
    static void SplitPath(string path, out string dir, out string name)
    {
        int i = path.Length;
        while (i > 0)
        {
            char ch = path[i - 1];
            if (ch == '\\' || ch == '/' || ch == ':')
```

```csharp
        Console.Write($"Array contains {args.Length} elements:");
        foreach (int i in args)
        {
            Console.Write($" {i}");
        }
        Console.WriteLine();
    }

    static void Main()
    {
        int[] arr = {1, 2, 3};
        F(arr);
        F(10, 20, 30, 40);
        F();
    }
}
```

生成以下输出

```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

F 的第一次调用只是将数组 arr 作为值参数传递。F 的第二次调用会自动创建一个包含给定元素值的四元素 int[]，并将该数组实例作为值参数传递。同样，F 的第三次调用会创建一个零元素 int[]，并将该实例作为值参数传递。第二次和第三次调用完全等价于编写：

```csharp
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

*示例结束*

执行重载决策时，带有参数数组的方法可能适用，或者以其常规形式适用，或者以其展开形式（§12.6.4.2）适用。仅当该方法的常规形式不适用，并且同一类型中尚未声明与展开形式具有相同签名的适用方法时，才可使用该方法的展开形式。

*示例：以下示例*

```csharp
class Test
{
    static void F(params object[] a) =>
        Console.WriteLine("F(object[])");

    static void F() =>
        Console.WriteLine("F()");

    static void F(object a0, object a1) =>
        Console.WriteLine("F(object,object)");

    static void Main()
    {
        F();
        F(1);
        F(1, 2);
        F(1, 2, 3);
    }
}
```

```
F(1, 2, 3, 4);
}
```

生成以下输出

```
F()
F(object[])
F(object,object)
F(object[])
F(object[])
```

在示例中，带有参数数组的方法的两种可能展开形式已经作为常规方法包含在类中。因此，在执行重载决策时不会考虑这些展开形式，第一次和第三次方法调用因而选择常规方法。当类声明带有参数数组的方法时，同时将一些展开形式作为常规方法包含在内并不罕见。这样做可以避免在调用带有参数数组的方法的展开形式时发生的数组实例分配。

示例结束

数组是引用类型，因此为参数数组传递的值可以为 null。

示例：以下示例：

```
class Test
{
    static void F(params string[] array) =>
        Console.WriteLine(array == null);

    static void Main()
    {
        F(null);
        F((string) null);
    }
}
```

生成以下输出：

```
True
False
```

第二次调用生成 False，因为它等价于 F(new string[] { null })，并传递一个包含单个 null 引用的数组。

示例结束

当参数数组的类型为 object[] 时，在方法的常规形式与单个 object 参数的展开形式之间会出现潜在歧义。产生歧义的原因是 object[] 本身可隐式转换为类型 object。然而，这种歧义不会造成问题，因为如有需要，可以通过插入强制转换来解决。

示例：以下示例

```
class Test
{
    static void F(params object[] args)
    {
        foreach (object o in args)
```

```
{
    Console.Write(o.GetType().FullName);
    Console.Write(" ");
}
Console.WriteLine();
}

static void Main()
{
    object[] a = {1, "Hello", 123.456};
    object o = a;
    F(a);
    F((object)a);
    F(o);
    F((object[])o);
}
```

生成以下输出

System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double

在 F 的第一次和最后一次调用中，F 的常规形式适用，因为存在从实参类型到参数类型的隐式转换（两者均为 object[] 类型）。因此，重载决策选择 F 的常规形式，并且实参作为常规值参数传递。在第二次和第三次调用中，F 的常规形式不适用，因为不存在从实参类型到参数类型的隐式转换（类型 object 不能隐式转换为类型 object[]）。但是，F 的展开形式适用，因此由重载决策选择。结果，该调用会创建一个单元素 object[]，并且该数组的单个元素用给定的实参值初始化（该值本身是对 object[] 的引用）。

*示例结束*

## 15.6.3 静态方法和实例方法

当方法声明包含 static 修饰符时，该方法称为静态方法。当不存在 static 修饰符时，该方法称为实例方法。

静态方法不针对特定实例进行操作，在静态方法中引用 this 是编译时错误。

实例方法针对类的给定实例进行操作，并且该实例可作为 this（§12.8.13）访问。

静态成员和实例成员之间的差异在 §15.3.8 中进一步讨论。

## 15.6.4 虚方法

当实例方法声明包含 virtual 修饰符时，该方法称为虚方法。当不存在 virtual 修饰符时，该方法称为非虚方法。

非虚方法的实现是不变的：无论该方法是在声明它的类的实例上调用，还是在派生类的实例上调用，实现都相同。在

相比之下，虚方法的实现可以由派生类取代。取代继承的虚方法的实现的过程称为重写该方法（§15.6.5）。

在虚方法调用中，进行调用的实例的运行时类型决定要调用的实际方法实现。在非虚方法调用中，实例的编译时类型是决定因素。准确地说，当在编译时类型为 C 且运行时类型为 R 的实例上使用参数列表 A 调用名为 N 的方法时（其中 R 是 C 或从 C 派生的类），该调用的处理过程如下：

-   在绑定时，对 C、N 和 A 应用重载决策，从 C 声明和继承的方法集中选择特定方法 M。这在 §12.8.9.2 中描述。
-   然后在运行时：
    -   如果 M 是非虚方法，则调用 M。
    -   否则，M 是虚方法，并且调用相对于 R 的 M 的最派生实现。

对于类中声明或继承的每个虚方法，都存在相对于该类的最派生实现。相对于类 R 的虚方法 M 的最派生实现确定如下：

-   如果 R 包含 M 的引入虚声明，则这是相对于 R 的 M 的最派生实现。
-   否则，如果 R 包含 M 的重写，则这是相对于 R 的 M 的最派生实现。
-   否则，相对于 R 的 M 的最派生实现与相对于 R 的直接基类的 M 的最派生实现相同。

示例：以下示例说明了虚方法和非虚方法之间的差异：

```csharp
class A
{
    public void F() => Console.WriteLine("A.F");
    public virtual void G() => Console.WriteLine("A.G");
}

class B : A
{
    public new void F() => Console.WriteLine("B.F");
    public override void G() => Console.WriteLine("B.G");
}

class Test
{
    static void Main()
    {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```

在示例中，A 引入了一个非虚方法 F 和一个虚方法 G。类 B 引入了一个新的非虚方法 F，从而隐藏了继承的 F，并且还重写了继承的方法 G。

该示例产生以下输出：

-   A.F
-   B.F
-   B.G
-   B.G

请注意，语句 a.G() 调用的是 B.G，而不是 A.G。这是因为实例的运行时类型（即 B）决定了要调用的实际方法实现，而不是实例的编译时类型（即 A）。

示例结束

由于允许方法隐藏继承的方法，一个类可能包含多个具有相同签名的虚方法。这不会造成歧义问题，因为除了最派生方法之外的所有方法都被隐藏了。

示例：在以下代码中

```csharp
class A
{
    public virtual void F() => Console.WriteLine("A.F");
}

class B : A
{
    public override void F() => Console.WriteLine("B.F");
}

class C : B
{
    public new virtual void F() => Console.WriteLine("C.F");
}

class D : C
{
    public override void F() => Console.WriteLine("D.F");
}

class Test
{
    static void Main()
    {
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

C 和 D 类包含两个具有相同签名的虚方法：一个由 A 引入，一个由 C 引入。由 C 引入的方法隐藏了从 A 继承的方法。因此，D 中的重写声明重写了由 C 引入的方法，而 D 不可能重写由 A 引入的方法。该示例产生以下输出：

    B.F
    B.F
    D.F
    D.F

请注意，可以通过派生程度较低的类型（其中该方法未被隐藏）访问 D 的实例，从而调用被隐藏的虚方法。

示例结束

## 15.6.5 重写方法

当实例方法声明包含 override 修饰符时，该方法称为重写方法。重写方法重写具有相同签名的继承虚方法。虚方法声明引入新方法，而重写方法声明通过提供该方法的新的实现来特化现有的继承虚方法。

由重写声明重写的方法称为被重写的基方法。对于在类 C 中声明的重写方法 M，通过检查 C 的每个基类来确定被重写的基方法，从 C 的直接基类开始，并继续检查每个后续的直接基类，直到在给定的基类类型中，在替换类型参数后，至少找到一个与 M 具有相同签名的可访问方法。为了定位被重写的基方法，如果方法是 public、protected、protected internal，或者是 internal 或 private protected 并且与 C 在同一程序中声明，则认为该方法是可访问的。

除非重写声明满足以下所有条件，否则会发生编译时错误：

-   可以如上所述定位被重写的基方法。
-   这样的被重写的基方法恰好有一个。此限制仅在基类类型是构造类型且类型参数的替换使两个方法的签名相同时才有效。
-   被重写的基方法是 virtual、abstract 或 override 方法。换句话说，被重写的基方法不能是 static 或非虚方法。
-   被重写的基方法不是 sealed 方法。
-   被重写的基方法的返回类型与重写方法之间存在标识转换。
-   重写声明和被重写的基方法具有相同的声明可访问性。换句话说，重写声明不能改变虚方法的可访问性。但是，如果被重写的基方法是 protected internal，并且它在与包含重写声明的程序集不同的程序集中声明，则重写声明的声明可访问性应为 protected。
-   重写声明不指定任何 type_parameter_constraints_clauses。相反，约束继承自被重写的基方法。被重写方法中作为类型参数的约束可以被继承约束中的类型参数替换。这可能导致显式指定时无效的约束，例如值类型或密封类型。

示例：以下演示了泛型类的重写规则如何工作：

```csharp
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}

class D : C<string>
{
    public override string F() {...}    // Ok
    public override C<string> G() {...}    // Ok
    public override void H(C<T> x) {...}    // Error, should be C<string>
}

class E<T,U> : C<U>
{
    public override U F() {...}    // Ok
    public override C<U> G() {...}    // Ok
    public override void H(C<T> x) {...}    // Error, should be C<U>
}
```

示例结束

重写声明可以使用 base_access（§12.8.14）访问被重写的基方法。

示例：在以下代码中

```csharp
class A
{
    int x;
    public virtual void PrintFields() => Console.WriteLine($"x = {x}");
}

class B : A
{
    int y;
    public override void PrintFields()
    {
        base.PrintFields();
        Console.WriteLine($"y = {y}");
    }
}
```

在 B 中调用 base.PrintFields() 会调用在 A 中声明的 PrintFields 方法。base_access 禁用了虚调用机制，并简单地将基方法视为非虚方法。如果 B 中的调用写成 ((A)this).PrintFields()，它将递归调用在 B 中声明的 PrintFields 方法，而不是在 A 中声明的方法，因为 PrintFields 是虚方法，并且 ((A)this) 的运行时类型是 B。

示例结束



只有在包含 override 修饰符时，方法才能重写另一个方法。在所有其他情况下，与继承方法具有相同签名的 方法 只是隐藏了继承的方法。

示例：在以下代码中

```csharp
class A
{
    public virtual void F() {}
}

class B : A
{
    public virtual void F() {} // Warning, hiding inherited F()
}
```

B 中的 F 方法不包含 override 修饰符，因此不会重写 A 中的 F 方法。相反，B 中的 F 方法隐藏了 A 中的方法，并且会报告警告，因为声明中未包含 new 修饰符。

示例结束

示例：在以下代码中

```csharp
class A
{
    public virtual void F() {}
}

class B : A
{
    private new void F() {} // Hides A.F within body of B
}

class C : B
{
    public override void F() {} // Ok, overrides A.F
}
```

B 中的 F 方法隐藏了从 A 继承的虚方法 F。由于 B 中的 new F 的访问权限为 private，其作用域仅包括 B 的类体，不会扩展到 C。因此，C 中 F 的声明被允许重写从 A 继承的 F。

示例结束

## 15.6.6 密封方法

当实例方法声明包含 sealed 修饰符时，该方法称为密封方法。密封方法重写具有相同签名的继承虚方法。密封方法还必须标记有 override 修饰符。使用 sealed 修饰符可防止派生类进一步重写该方法。

示例：示例

```csharp
class A
{
    public virtual void F() => Console.WriteLine("A.F");
    public virtual void G() => Console.WriteLine("A.G");
}

class B : A
{
    public sealed override void F() => Console.WriteLine("B.F");
    public override void G()
        => Console.WriteLine("B.G");
}

class C : B
{
    public override void G() => Console.WriteLine("C.G");
}
```

类 B 提供了两个重写方法：一个带有 sealed 修饰符的 F 方法和一个不带该修饰符的 G 方法。B 对 sealed 修饰符的使用阻止了 C 进一步重写 F。

示例结束

## 15.6.7 抽象方法

当实例方法声明包含 abstract 修饰符时，该方法称为抽象方法。尽管抽象方法隐式地也是虚方法，但它不能具有 virtual 修饰符。

抽象方法声明引入了一个新的虚方法，但未提供该方法的实现。相反，非抽象派生类必须通过重写该方法来提供自己的实现。因为抽象方法不提供实际实现，所以抽象方法的方法体仅由一个分号组成。

抽象方法声明仅允许在抽象类中（§15.2.2.2）。

示例：在以下代码中

```csharp
public abstract class Shape
{
    public abstract void Paint(Graphics g, Rectangle r);
}

public class Ellipse : Shape
{
    public override void Paint(Graphics g, Rectangle r) => g.DrawEllipse(r);
}

public class Box : Shape
{
    public override void Paint(Graphics g, Rectangle r) => g.DrawRect(r);
}
```

Shape 类定义了几何形状对象的抽象概念，该对象可以自行绘制。Paint 方法是抽象的，因为没有有意义的默认实现。Ellipse 和 Box 类是具体的 Shape 实现。因为这些类是非抽象的，所以它们必须重写 Paint 方法并提供实际实现。

示例结束

对 base_access (§12.8.14) 引用抽象方法是一个编译时错误。

示例：在以下代码中

```csharp
abstract class A
{
    public abstract void F();
}

class B : A
{
    // Error, base.F is abstract
    public override void F() => base.F();
}
```

由于 base.F() 调用引用了抽象方法，因此报告了编译时错误。

示例结束

抽象方法声明允许重写虚方法。这允许抽象类强制在派生类中重新实现该方法，并使该方法的原始实现不可用。

示例：在以下代码中

```csharp
class A
{
    public virtual void F() => Console.WriteLine("A.F");
}

abstract class B : A
{
    public abstract override void F();
}

class C : B
{
    public override void F() => Console.WriteLine("C.F");
}
```

类 A 声明了一个虚方法，类 B 用抽象方法重写此方法，而类 C 重写抽象方法以提供自己的实现。

示例结束

## 15.6.8 外部方法

当方法声明包含 extern 修饰符时，该方法称为外部方法。

外部方法在外部实现，通常使用 C# 以外的语言。因为外部方法声明不提供实际实现，所以外部方法的方法体仅由一个分号组成。外部方法不得为泛型。

实现外部方法链接的机制由实现定义。

示例：以下示例演示了 extern 修饰符和 DllImport 属性的使用：

```csharp
class Path
{
    [DllImport("kernel32", SetLastError=true)]
    static extern bool CreateDirectory(string name, SecurityAttribute sa);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool RemoveDirectory(string name);

    [DllImport("kernel32", SetLastError=true)]
    static extern int GetCurrentDirectory(int bufsize, StringBuilder buf);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool SetCurrentDirectory(string name);
}
```

*示例结束*

## 15.6.9 部分方法

当方法声明包含 *部分* 修饰符时，该方法称为 *部分方法*。部分方法只能声明为部分类型 (§15.2.7) 的成员，并受若干限制。

部分方法可以在类型声明的一个部分中定义，并在另一部分中实现。实现是可选的；如果没有任何部分实现部分方法，则部分方法声明及其所有调用都会从组合各部分后得到的类型声明中移除。

部分方法不得定义访问修饰符；它们隐式为 *私有*。它们的返回类型应为 *void*，并且其参数不得具有 *out* 修饰符。标识符 *部分* 仅在方法声明中紧跟在 *void* 关键字之前时才被识别为上下文关键字 (§6.4.4)。部分方法不能 *显式实现接口方法*。

存在两种部分方法声明：如果方法声明的主体是一个分号，则该声明称为 *定义部分方法声明*。如果主体不是分号，则该声明称为 *实现部分方法声明*。在类型声明的各部分中，对于给定的签名只能有一个定义部分方法声明，并且只能有一个实现部分方法声明。如果提供了实现部分方法声明，则必须存在相应的定义部分方法声明，并且声明必须符合以下规定：
- 声明应具有相同的修饰符（尽管顺序不一定相同）、方法名、类型参数数量和参数数量。
- 声明中对应的参数应具有相同的修饰符（尽管顺序不一定相同）以及相同的类型（忽略类型参数名称的差异）。
- 声明中对应的类型参数应具有相同的约束（忽略类型参数名称的差异）。

实现部分方法声明可以与相应的定义部分方法声明出现在同一部分中。

只有定义部分方法参与重载解析。因此，无论是否给出实现声明，调用表达式都可能解析为对部分方法的调用。因为部分方法始终返回 *void*，所以此类调用表达式始终是表达式语句。此外，因为部分方法 *隐式为私有*，所以此类语句始终发生在声明部分方法的类型声明的各部分之一中。

*注意：* 匹配的定义部分方法声明和实现部分方法声明的定义不要求参数名称匹配。这可能在...时产生 *出人意料*，尽管 *良好定义* 的 行为 when

使用了命名实参（§12.6.2.1）。例如，在一个文件中给定 M 的定义分部方法声明，在另一个文件中给定实现分部方法声明：

```
// File P1.cs:
partial class P
{
    static partial void M(int x);
}
```

```
// File P2.cs:
partial class P
{
    static void Caller() => M(y: 0);
    static partial void M(int y) {}
}
```

是无效的，因为该调用使用的是实现分部方法声明中的参数名，而不是定义分部方法声明中的参数名。

注释结束

如果分部类型声明的任何部分都不包含针对给定分部方法的实现声明，则调用它的任何表达式语句都会从合并类型声明中移除。因此，该调用表达式（包括任何子表达式）在运行时没有效果。该分部方法本身也会被移除，并且不会成为合并类型声明的成员。

如果存在针对给定分部方法的实现声明，则保留对这些分部方法的调用。该分部方法会生成一个方法声明，类似于实现分部方法声明，但有以下不同：

- 不包含 partial 修饰符。
- 生成的方法声明中的特性是定义分部方法声明和实现分部方法声明中的特性合并，顺序未指定。重复项不会被移除。
- 生成的方法声明中参数上的特性是定义分部方法声明和实现分部方法声明中对应参数的特性合并，顺序未指定。重复项不会被移除。

如果为分部方法 M 给定了定义声明但没有给定实现声明，则适用以下限制：

- 从 M 创建委托（§12.8.16.6）是编译时错误。
- 在转换为表达式树类型的匿名函数（§8.6）中引用 M 是编译时错误。
- 作为 M 调用的一部分出现的表达式不影响明确赋值状态（§9.4），这可能导致编译时错误。
- M 不能作为应用程序的入口点（§7.1）。

分部方法有助于允许类型声明的一个部分自定义另一部分的行为，例如由工具生成的部分。考虑以下分部类声明：

```
partial class Customer
{
    string name;

    public string Name
    {
        get => name;
        set
        {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }

    partial void OnNameChanging(string newName);
    partial void OnNameChanged();
}
```

如果编译此类时没有任何其他部分，则定义分部方法声明及其调用将被移除，并且生成的合并类声明将等价于以下内容：

```
class Customer
{
    string name;

    public string Name
    {
        get => name;
        set => name = value;
    }
}
```

然而，假设给定了另一部分，它提供这些分部方法的实现声明：

```
partial class Customer
{
    partial void OnNameChanging(string newName) =>
        Console.WriteLine($"Changing {name} to {newName}");

    partial void OnNameChanged() =>
        Console.WriteLine($"Changed to {name}");
}
```

那么生成的合并类声明将等价于以下内容：

```
class Customer
{
    string name;

    public string Name
    {
        get => name;
        set
        {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }
    }
}
```

## 15.6.10 扩展方法

当方法的第一个参数包含 this 修饰符时，该方法称为扩展方法。扩展方法只能在非泛型、非嵌套的静态类中声明。扩展方法的第一个参数受以下限制：

- 仅当参数为值类型时，它才可以具有 in 参数修饰符
- 仅当参数为值类型或受约束为 struct 的泛型类型时，它才可以具有 ref 参数修饰符
- 它不得为指针类型。

示例：以下是一个声明两个扩展方法的静态类的示例：

```
public static class Extensions
{
    public static int ToInt32(this string s) => Int32.Parse(s);

    public static T[] Slice<T>(this T[] source, int index, int count)
    {
        if (index < 0 || count < 0 || source.Length - index < count)
        {
            throw new ArgumentException();
        }
        T[] result = new T[count];
        Array.Copy(source, index, result, 0, count);
        return result;
    }
}
```

*示例结束*

扩展方法是一种常规静态方法。此外，当包含它的静态类在作用域内时，可以使用实例方法调用语法（§12.8.9.3）调用扩展方法，并将接收者表达式用作第一个实参。

示例：以下程序使用上面声明的扩展方法：

```
static class Program
{
    static void Main()
    {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in strings.Slice(1, 2))
        {
            Console.WriteLine(s.ToInt32());
        }
    }
}
```

Slice 方法可在 string[] 上使用，ToInt32 方法可在 string 上使用，因为它们已声明为扩展方法。该程序的含义与以下使用普通静态方法调用的程序相同：

```
static class Program
{
    static void Main()
    {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in Extensions.Slice(strings, 1, 2))
        {
            Console.WriteLine(Extensions.ToInt32(s));
        }
    }
}
```

示例结束

## 15.6.11 方法体

方法声明的方法体由块体、表达式体或分号组成。

抽象方法和外部方法声明不提供方法实现，因此其方法体仅由分号组成。对于任何其他方法，方法体是一个块（§13.3），包含调用该方法时要执行的语句。

如果返回类型为 void，或者方法为 async 且返回类型为 «TaskType»（§15.15.1），则方法的有效返回类型为 void。否则，非 async 方法的有效返回类型是其返回类型，而返回类型为 «TaskType»<T>（§15.15.1）的 async 方法的有效返回类型为 T。

当方法的有效返回类型为 void 且具有块体时，块中的 return 语句（§13.10.5）不得指定表达式。如果 void 方法的块正常完成执行（即控制流到达方法体末尾之外），该方法只是返回到其调用方。

当方法的有效返回类型为 void 且具有表达式体时，表达式 E 应为语句表达式，并且该体完全等价于形式为 { E; } 的块体。

示例：在以下代码中

```
class A
{
    public int F() {} // Error, return value required
    public int G()
    {
        return 1;
    }
    public int H(bool b)
    {
        if (b)
        {
            return 1;
        }
        else
        {
            return 0;
        }
    }
    public int I(bool b) => b ? 1 : 0;
}
```

返回值方法 F 会导致编译时错误，因为控制流可能到达方法体末尾之外。G 和 H 方法正确，因为所有可能的执行路径都以指定返回值的 return 语句结束。I 方法正确，因为它的体等价于仅包含一个 return 语句的块。

*示例结束*

## 15.7 属性

### 15.7.1 概述

*属性*是一种成员，用于提供对对象或类的特性的访问。属性的示例包括字符串的长度、字体的大小、窗口的标题、客户的名称等。属性是字段的自然扩展——两者都是具有关联类型的命名成员，并且访问字段和属性的语法相同。然而，与字段不同，属性不表示存储位置。相反，属性具有*访问器*，用于指定读取或写入其值时要执行的语句。因此，属性提供了一种机制，将操作与对象特性的读取和写入关联起来；此外，它们允许计算此类特性。

属性使用 *属性声明* 声明：

```
property_declaration
: attributes? property_modifier* type member_name property_body
| attributes? property_modifier* ref_kind type member_name ref_property_body
;

property_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
```



```
| 'static'
| 'virtual'
| 'sealed'
| 'override'
| 'abstract'
| 'extern'
| unsafe_modifier  // unsafe code support
;
```

```
property_body
: '{' accessor_declarations '}' property_initializer?
| '=>' expression ';'
;
```

```
property_initializer
: '=' variable_initializer ';'
;
```

```
ref_property_body
: '{' ref_get_accessor_declaration '}'
| '=>' ref_variable_reference ';'
;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

property_declaration 有两种：

- 第一种声明非 ref 值属性。其值的类型为 type。此类属性可以是可读的和/或可写的。
- 第二种声明 ref 值属性。其值是一个 variable_reference（§9.5），它可能是只读的，指向类型为 type 的变量。此类属性仅可读。

property_declaration 可以包含一组特性（§22），以及所允许的任意一种已声明可访问性（§15.3.6）、new（§15.3.5）、static（§15.7.2）、virtual（§15.6.4、§15.7.6）、override（§15.6.5、§15.7.6）、sealed（§15.6.6）、abstract（§15.6.7、§15.7.6）和 extern（§15.6.8）修饰符。

就修饰符的有效组合而言，属性声明遵循与方法声明（§15.6）相同的规则。

member_name（§15.6.1）指定属性的名称。除非该属性是显式接口成员实现，否则 member_name 只是一个标识符。对于显式接口成员实现（§18.6.2），member_name 由 interface_type、后跟“.”和一个标识符组成。

属性的类型应至少与属性本身同样可访问（§7.5.5）。

property_body 可以由语句体或表达式体组成。在语句体中，accessor_declarations（应包含在“{”和“}”标记中）声明属性的访问器（§15.7.3）。访问器指定与读取和写入属性相关联的可执行语句。

在 property_body 中，由 => 后跟表达式 E 和分号组成的表达式体完全等价于语句体 { get { return E; } }，因此只能用于指定只读属性，其中 get 访问器的结果由单个表达式给出。

property_initializer 只能为自动实现的属性（§15.7.4）指定，并且会使用表达式给定的值初始化此类属性的基础字段。

ref_property_body 可以由语句体或表达式体组成。在语句体中，get_accessor_declaration 声明属性的 get 访问器（§15.7.3）。该访问器指定与读取属性相关联的可执行语句。

在 ref_property_body 中，由 => 后跟 ref、一个 variable_reference V 和分号组成的表达式体完全等价于语句体 { get { return ref V; } }。

> 注意：尽管访问属性的语法与访问字段的语法相同，但属性不归类为变量。因此，不能将属性作为 in、out 或 ref 实参传递，除非该属性是 ref 值属性，并因此返回变量引用（§9.7）。注释结束。

当属性声明包含 extern 修饰符时，该属性称为外部属性。由于外部属性声明不提供实际实现，其每个 accessor_declarations 都由一个分号组成。

## 15.7.2 静态属性和实例属性

当属性声明包含 static 修饰符时，该属性称为静态属性。当不存在 static 修饰符时，该属性称为实例属性。

静态属性不与特定实例关联，在静态属性的访问器中引用 this 是编译时错误。

实例属性与类的给定实例关联，并且可以在该属性的访问器中通过 this（§12.8.13）访问该实例。

静态成员与实例成员之间的差异将在 §15.3.8 中进一步讨论。

## 15.7.3 访问器

> 注意：本条款同时适用于属性（§15.7）和索引器（§15.9）。本条款以属性的措辞编写；在阅读索引器相关内容时，请将 property/properties 替换为 indexer/indexers，并参阅 §15.9.2 中给出的属性与索引器之间的差异列表。注释结束。

属性的 accessor_declarations 指定与写入和/或读取该属性相关联的可执行语句。

```
accessor_declarations
  : get_accessor_declaration set_accessor_declaration?
  | set_accessor_declaration get_accessor_declaration?
  ;

get_accessor_declaration
  : attributes? accessor_modifier? 'get' accessor_body
  ;

set_accessor_declaration
  : attributes? accessor_modifier? 'set' accessor_body
  ;

accessor_modifier
  : 'protected'
  | 'internal'
  | 'private'
  | 'protected' 'internal'
  | 'internal' 'protected'
  | 'protected' 'private'
  | 'private' 'protected'
  ;
```

```
accessor_body
: block
| '=>' expression ';'
| ';'
;

ref_get_accessor_declaration
: attributes? accessor_modifier? 'get' ref_accessor_body
;

ref_accessor_body
: block
| '=>' 'ref' variable_reference ';'
| ';'
;
```

accessor_declarations 由一个 get_accessor_declaration、一个 set_accessor_declaration 或两者组成。每个访问器声明由可选特性、可选 accessor_modifier、标记 get 或 set，以及后跟的 accessor_body 组成。

对于 ref 值属性，ref_get_accessor_declaration 由可选特性、可选 accessor_modifier、标记 get，以及后跟的 ref_accessor_body 组成。

accessor_modifier 的使用受以下限制约束：

- accessor_modifier 不得用于接口中或显式接口成员实现中。
- 对于没有 override 修饰符的属性或索引器，只有当该属性或索引器同时具有 get 和 set 访问器时，才允许使用 accessor_modifier，并且只允许在其中一个访问器上使用。
- 对于包含 override 修饰符的属性或索引器，访问器应匹配被重写访问器的 accessor_modifier（如果有）。
- accessor_modifier 声明的可访问性应严格限制于属性或索引器本身已声明的可访问性。具体而言：
  - 如果属性或索引器的已声明可访问性为 public，则 accessor_modifier 声明的可访问性可以是 private protected、protected internal、internal、protected 或 private。
  - 如果属性或索引器的已声明可访问性为 protected internal，则 accessor_modifier 声明的可访问性可以是 private protected、protected private、internal、protected 或 private。
  - 如果属性或索引器的已声明可访问性为 internal 或 protected，则 accessor_modifier 声明的可访问性应为 private protected 或 private。
  - 如果属性或索引器的已声明可访问性为 private protected，则 accessor_modifier 声明的可访问性应为 private。
  - 如果属性或索引器的已声明可访问性为 private，则不得使用任何 accessor_modifier。

对于 abstract 和 extern 的非 ref 值属性，所指定的每个访问器的 accessor_body 都只是一个分号。非 abstract、非 extern 的属性（但不是索引器）也可以将所有指定访问器的 accessor_body 设为分号，此时它是自动实现的属性（§15.7.4）。自动实现的属性应至少具有一个 get 访问器。对于任何其他非 abstract、非 extern 属性的访问器，accessor_body 是以下之一：

- 一个块，指定调用相应访问器时要执行的语句；或
- 一个表达式体，由 => 后跟一个表达式和分号组成，表示调用相应访问器时要执行的单个表达式。

对于 abstract 和 extern 的 ref 值属性，ref_accessor_body 只是一个分号。对于任何其他非 abstract、非 extern 属性的访问器，ref_accessor_body 是以下之一：

- 一个块，指定调用 get 访问器时要执行的语句；或
- 一个表达式体，由 => 后跟 ref、一个 variable_reference 和分号组成。变量引用在调用 get 访问器时求值。

非 ref 值属性的 get 访问器对应于一个无参数方法，其返回值为该属性的类型。除非作为赋值目标，否则在表达式中引用此类属性时，会调用其 get 访问器来计算该属性的值（§12.2.2）。

非 ref 值属性的 get 访问器体应符合 §15.6.11 中所述的值返回方法的规则。特别是，get 访问器体中的所有 return 语句都应指定一个可隐式转换为该属性类型的表达式。此外，get 访问器的端点不可到达。

ref 值属性的 get 访问器对应于一个无参数方法，其返回值为指向该属性类型的变量的 variable_reference。当在表达式中引用此类属性时，会调用其 get 访问器来计算该属性的 variable_reference 值。然后，该变量引用像任何其他变量引用一样，用于读取所引用的变量，或者在非只读 variable_reference 的情况下，根据上下文要求写入所引用的变量。

示例：以下示例说明将 ref 值属性作为赋值目标：

```csharp
class Program
{
    static int field;
    static ref int Property => ref field;

    static void Main()
    {
        field = 10;
        Console.WriteLine(Property); // Prints 10
        Property = 20;               // This invokes the getter, then assigns
                                     // via the resulting variable reference
        Console.WriteLine(field);    // Prints 20
    }
}
```

示例结束

ref 值属性的 get 访问器体应符合 §15.6.11 中所述的 ref 值方法的规则。

set 访问器对应于一个方法，该方法具有一个属性类型的值参数和 void 返回类型。set 访问器的隐式参数始终命名为 value。当属性为

作为赋值的目标（§12.21），或作为 ++ 或 -- 的操作数（§12.8.15，§12.9.6）时，将调用 set 访问器，并传入一个提供新值的参数（§12.21.2）。set 访问器的主体必须符合 §15.6.11 中描述的 void 方法规则。特别是，set 访问器主体中的 return 语句不得指定表达式。由于 set 访问器隐式具有名为 value 的参数，因此在 set 访问器中声明局部变量或常量时使用该名称会是编译时错误。

根据 get 和 set 访问器的有无，属性被分类如下：

-   包含 get 访问器和 set 访问器的属性称为 *读写属性*。
-   仅具有 get 访问器的属性称为 *只读属性*。将只读属性作为赋值的目标是编译时错误。
-   仅具有 set 访问器的属性称为 *只写属性*。除作为赋值的目标外，在表达式中引用只写属性是编译时错误。

*注意：* 前缀和后缀 ++ 和 -- 运算符以及复合赋值运算符不能应用于只写属性，因为这些运算符在写入新值之前会读取操作数的旧值。 *结束注意*

*示例：* 以下代码中

```
public class Button : Control
{
    private string caption;

    public string Caption
    {
        get => caption;
        set
        {
            if (caption != value)
            {
                caption = value;
                Repaint();
            }
        }
    }

    public override void Paint(Graphics g, Rectangle r)
    {
        // Painting code goes here
    }
}
```

Button 控件声明了一个公共的 Caption 属性。Caption 属性的 get 访问器返回存储在私有 caption 字段中的字符串。set 访问器检查新值是否与当前值不同，如果不同，则存储新值并重绘控件。属性通常遵循上图所示的模式：get 访问器仅返回存储在私有字段中的值，而 set 访问器修改该私有字段，然后执行任何必要的额外操作以完全更新对象的状态。给定上面的 Button 类，以下是 Caption 属性使用示例：

```
Button okButton = new Button();
okButton.Caption = "OK"; // Invokes set accessor
string s = okButton.Caption; // Invokes get accessor
```

这里，通过给属性赋值调用 set 访问器，通过在表达式中引用属性调用 get 访问器。

结束示例

属性的 get 和 set 访问器不是不同的成员，不可能单独声明属性的访问器。

示例：示例

```csharp
class A
{
    private string name;

    // Error, duplicate member name
    public string Name
    {
        get => name;
    }

    // Error, duplicate member name
    public string Name
    {
        set => name = value;
    }
}
```

未声明单个读写属性。相反，它声明了两个同名属性，一个只读，一个只写。由于同一个类中声明的两个成员不能同名，因此该示例会导致编译时错误。

结束示例

当派生类声明的属性与继承的属性同名时，派生属性在读取和写入方面都会隐藏继承的属性。

示例：在以下代码中

```csharp
class A
{
    public int P
    {
        set {...}
    }
}

class B : A
{
    public new int P
    {
        get {...}
    }
}
```

B 中的 P 属性在读取和写入方面都会隐藏 A 中的 P 属性。因此，在以下语句中

```csharp
B b = new B();
b.P = 1;    // Error, B.P is read-only
((A)b).P = 1;  // Ok, reference to A.P
```

对 b.P 的赋值会导致编译时错误，因为 B 中只读的 P 属性隐藏了 A 中只写的 P 属性。然而，值得注意的是，可以使用强制转换来访问隐藏的 P 属性。

*结束示例*

与公共字段不同，属性在对象的内部状态与其公共接口之间提供了分离。

*示例：* 考虑以下代码，该代码使用 Point 结构体表示位置：

```csharp
class Label
{
    private int x, y;
    private string caption;

    public Label(int x, int y, string caption)
    {
        this.x = x;
        this.y = y;
        this.caption = caption;
    }

    public int X => x;
    public int Y => y;
    public Point Location => new Point(x, y);
    public string Caption => caption;
}
```

这里，Label 类使用两个 int 字段 x 和 y 来存储其位置。位置以 X 和 Y 属性以及类型为 Point 的 Location 属性两种方式公开。如果在 Label 的未来版本中，将位置内部存储为 Point 更方便，可以在不影响类公共接口的情况下进行更改：

```csharp
class Label
{
    private Point location;
    private string caption;

    public Label(int x, int y, string caption)
    {
        this.location = new Point(x, y);
        this.caption = caption;
    }

    public int X => location.X;
    public int Y => location.Y;
    public Point Location => location;
    public string Caption => caption;
}
```

如果 x 和 y 曾经是公共只读字段，就不可能对 Label 类进行此类更改。

*结束示例*

*注意：* 通过属性公开状态并不一定比直接公开字段效率更低。特别是当属性是非虚的并且只包含少量代码时，执行环境可能会用访问器的实际代码替换对访问器的调用。此过程称为 **内联**，它使属性访问与字段访问一样高效，同时保留了属性的灵活性。结束注意

*示例：* 由于调用 get 访问器在概念上等同于读取字段的值，因此 get 访问器具有可观察的副作用被认为是不良的编程风格。在示例中

~~~csharp
class Counter
{
    private int next;

    public int Next => next++;
}
~~~

Next 属性的值取决于该属性之前被访问的次数。因此，访问该属性会产生可观察的副作用，该属性应实现为方法。

“无副作用”约定对于 get 访问器并不意味着 get 访问器应始终仅编写为返回存储在字段中的值。事实上，get 访问器通常通过访问多个字段或调用方法来计算属性的值。然而，设计良好的 get 访问器不会执行导致对象状态可观察变化的任何操作。

*结束示例*

属性可用于延迟资源的初始化，直到首次引用该资源时。

*示例：*

~~~csharp
public class Console
{
    private static TextReader reader;
    private static TextWriter writer;
    private static TextWriter error;

    public static TextReader In
    {
        get
        {
            if (reader == null)
            {
                reader = new StreamReader(Console.OpenStandardInput());
            }
            return reader;
        }
    }

    public static TextWriter Out
    {
        get
        {
            if (writer == null)
            {
                writer = new StreamReader(Console.OpenStandardOutput());
            }
            return writer;
        }
    }
    public static TextWriter Error
    {
        get
        {
            if (error == null)
            {
                error = new StreamReader(Console.OpenStandardError());
            }
            return error;
        }
    }
...
}
~~~

Console 类包含三个属性 In、Out 和 Error，分别表示标准输入、输出和错误设备。通过将这些成员作为属性公开，Console 类可以延迟它们的初始化，直到实际使用时。例如，首次引用 Out 属性时，如 Console.Out.WriteLine("hello, world");，输出设备的底层 TextWriter 就会被创建。但是，如果应用程序不引用 In 和 Error 属性，则不会为这些设备创建对象。

结束示例

## 15.7.4 自动实现的属性

自动实现的属性（简称 auto-property）是不抽象的、非 extern 的、非 ref 值属性，且访问器主体仅为分号。自动属性必须具有 get 访问器，可选择具有 set 访问器。

当属性指定为自动实现的属性时，会自动为该属性提供一个隐藏的后备字段，并且访问器实现为从该后备字段读取和写入。如果自动属性没有 set 访问器，则后备字段被视为 readonly（§15.5.3）。就像只读字段一样，只读自动属性也可以在封闭类的构造函数体中赋值。此类赋值直接赋给属性的只读后备字段。

自动属性可以可选地具有 property_initializer，它作为 variable_initializer（§17.7）直接应用于后备字段。

示例：

```
public class Point
{
    public int X { get; set; } // Automatically implemented
    public int Y { get; set; } // Automatically implemented
}
```


等同于以下声明：

```
public class Point
{
    private int x;
    private int y;

    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

示例结束

示例：在以下代码中

```
public class ReadOnlyPoint
{
    public int X { get; }
    public int Y { get; }

    public ReadOnlyPoint(int x, int y)
    {
        X = x;
        Y = y;
    }
}
```

等同于以下声明：

```
public class ReadOnlyPoint
{
    private readonly int __x;
    private readonly int __y;
    public int X { get { return __x; } }
    public int Y { get { return __y; } }

    public ReadOnlyPoint(int x, int y)
    {
        __x = x;
        __y = y;
    }
}
```

对只读字段的赋值是有效的，因为这些赋值发生在构造函数内。

示例结束

尽管后备字段是隐藏的，但可以通过自动实现属性的 property_declaration（§15.7.1）将面向字段的特性直接应用于该字段。

示例：以下代码

```
[Serializable]
public class Foo
{
    [field: NonSerialized]
    public string MySecret { get; set; }
}
```

会使字段目标特性 NonSerialized 应用于编译器生成的后备字段，就像代码编写如下所示：

```
[Serializable]
public class Foo
{
    [NonSerialized]
    private string _mySecretBackingField;
    public string MySecret
    {
        get { return _mySecretBackingField; }
        set { _mySecretBackingField = value; }
    }
}
```

*示例结束*

## 15.7.5 可访问性

如果访问器具有 accessor_modifier，则访问器的可访问域（§7.5.3）使用 accessor_modifier 的声明可访问性来确定。如果访问器没有 accessor_modifier，则访问器的可访问域根据属性或索引器的声明可访问性确定。

accessor_modifier 的存在绝不会影响成员查找（§12.5）或重载决策（§12.6.4）。属性或索引器上的修饰符始终决定绑定到哪个属性或索引器，而与访问的上下文无关。

一旦选定了特定的非 ref 值属性或非 ref 值索引器，就会使用所涉及的特定访问器的可访问域来确定该用法是否有效：

- 如果该用法是作为值（§12.2.2），则 get 访问器必须存在且可访问。
- 如果该用法是作为简单赋值（§12.21.2）的目标，则 set 访问器必须存在且可访问。
- 如果该用法是作为复合赋值（§12.21.4）的目标，或作为 ++ 或 -- 运算符（§12.8.15、§12.9.6）的目标，则 get 访问器和 set 访问器都必须存在且可访问。

*示例：*在以下示例中，属性 A.Text 被属性 B.Text 隐藏，即使在仅调用 set 访问器的上下文中也是如此。相反，类 M 无法访问属性 B.Count，因此改用可访问的属性 A.Count。

```
class A
{
    public string Text
    {
        get => "hello";
        set { }
    }

    public int Count
    {
        get => 5;
        set { }
    }
}
```

*示例结束*

## 15.7.6 虚拟、密封、重写和抽象访问器

*注意：*本条款适用于属性（§15.7）和索引器（§15.9）。本条款按属性来表述；当针对索引器阅读时，请将 property/properties 替换为 indexer/indexers，并查阅 §15.9.2 中给出的属性和索引器之间的差异列表。*注意结束*

虚拟属性声明指定该属性的访问器是虚拟的。virtual 修饰符适用于属性的所有非私有访问器。当虚拟属性的访问器具有 private accessor_modifier 时，该私有访问器隐式地不是虚拟的。

抽象属性声明指定该属性的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写该属性来为访问器提供自己的实现。由于抽象属性声明的访问器不提供实际实现，其 accessor_body 仅由一个分号组成。抽象属性不得具有私有访问器。

同时包含 abstract 和 override 修饰符的属性声明指定该属性是抽象的，并重写基属性。此类属性的访问器也是抽象的。

抽象属性声明只允许在抽象类（§15.2.2.2）中。继承的虚拟属性的访问器可以在派生类中通过包含指定 override 指令的属性声明来重写。这称为重写属性声明。重写属性声明不声明新属性。相反，它只是特化现有虚拟属性的访问器实现。

override 声明和被重写的基属性必须具有相同的声明可访问性。换句话说，override 声明不得更改基属性的可访问性。但是，如果被重写的基属性是 protected internal，并且它声明在不同于包含 override 声明的程序集的程序集中，则 override 声明的声明可访问性应为 protected。如果继承的属性只有一个访问器（即，如果继承的属性是只读或只写的），则重写属性应仅包含该访问器。如果继承的属性包含两个访问器（即，如果继承的属性是读写的），则重写属性可以包含单个访问器或两个访问器。重写属性和继承属性的类型之间必须存在恒等转换。

重写属性声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该属性。密封属性的访问器也是密封的。

除了声明和调用语法上的差异外，virtual、sealed、override 和 abstract 访问器的行为与 virtual、sealed、override 和 abstract 方法完全相同。具体而言，§15.6.4、§15.6.5、§15.6.6 和 §15.6.7 中描述的规则适用，就像访问器是对应形式的方法一样：

- get 访问器对应于无参数方法，其返回值为属性类型，并具有与包含属性相同的修饰符。
- set 访问器对应于具有一个属性类型的值参数、void 返回类型以及与包含属性相同修饰符的方法。

*示例：*在以下代码中

```
abstract class A
{
    int y;

    public virtual int X
    {
        get => 0;
    }

    public virtual int Y
    {
        get => y;
        set => y = value;
    }

    public abstract int Z { get; set; }
}
```

X 是虚拟只读属性，Y 是虚拟读写属性，Z 是抽象读写属性。由于 Z 是抽象的，包含类 A 也必须声明为抽象。

下面展示了从 A 派生的类：

```
class B : A
{
    int z;

    public override int X
    {
        get => base.X + 1;
    }

    public override int Y
    {
        set => base.Y = value < 0 ? 0: value;
    }

    public override int Z
    {
        get => z;
        set => z = value;
    }
}
```

在此，X、Y 和 Z 的声明是重写属性声明。每个属性声明都完全匹配对应继承属性的可访问性修饰符、类型和名称。X 的 get 访问器和 Y 的 set 访问器使用 base 关键字访问继承的访问器。Z 的声明重写了两个抽象访问器——因此，B 中没有未实现的抽象函数成员，B 可以是非抽象类。

示例结束

当属性声明为 override 时，任何被重写的访问器都必须可由重写代码访问。此外，属性或索引器本身以及访问器的声明可访问性都必须与被重写成员和访问器的声明可访问性匹配。

示例：

```
public class B
{
```





```
public virtual int P
{
    get {...}
    protected set {...}
}

public class D: B
{
    public override int P
    {
        get {...}    // Must not have a modifier here
        protected set {...} // Must specify protected here
    }
}
```

*示例结束*

## 15.8 事件

### 15.8.1 概述

事件是一种成员，它使对象或类能够提供通知。客户端可以通过提供事件处理程序来为事件附加可执行代码。

事件使用 event_declarations 声明：

```
event_declaration
: attributes? event_modifier* 'event' type variable_declarators ';'
| attributes? event_modifier* 'event' type member_name
    '{' event_accessor_declarations '}'
;

event_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| 'static'
| 'virtual'
| 'sealed'
| 'override'
| 'abstract'
| 'extern'
| unsafe_modifier  // 不安全代码支持
;

event_accessor_declarations
: add_accessor_declaration remove_accessor_declaration
| remove_accessor_declaration add_accessor_declaration
;

add_accessor_declaration
: attributes? 'add' block
;
remove_accessor_declaration
: attributes? 'remove' block
;
```

unsafe_modifier（§23.2）仅在不安全代码（§23）中可用。

event_declaration 可以包含一组特性（§22）以及任何允许的声明可访问性（§15.3.6）、new（§15.3.5）、static（§15.6.3、§15.8.4）、virtual（§15.6.4、§15.8.5）、override（§15.6.5、§15.8.5）、sealed（§15.6.6）、abstract（§15.6.7、§15.8.5）和 extern（§15.6.8）修饰符。

事件声明在修饰符的有效组合方面遵循与方法声明（§15.6）相同的规则。

事件声明的类型应为 delegate_type（§8.2.8），并且该 delegate_type 的可访问性至少应与事件本身相同（§7.5.5）。

事件声明可以包含 event_accessor_declarations。但是，如果未包含，则对于非 extern、非 abstract 的事件，编译器应自动提供这些访问器（§15.8.2）；对于 extern 事件，访问器由外部提供。

省略 event_accessor_declarations 的事件声明定义一个或多个事件——每个 variable_declarators 对应一个事件。特性和修饰符适用于此类 event_declaration 声明的所有成员。

如果 event_declaration 同时包含 abstract 修饰符和 event_accessor_declarations，则属于编译时错误。

当事件声明包含 extern 修饰符时，该事件称为外部事件。由于外部事件声明不提供实际实现，因此同时包含 extern 修饰符和 event_accessor_declarations 是错误的。

如果带有 abstract 或 external 修饰符的事件声明的 variable_initializer 包含变量初始化器，则属于编译时错误。

事件可以用作 `+=` 和 `-=` 运算符的左操作数。这些运算符分别用于向事件附加事件处理程序或从事件移除事件处理程序，事件的访问修饰符控制允许此类操作的上下文。

在声明事件的类型之外，代码对事件唯一允许的操作是 `+=` 和 `-=`。因此，虽然此类代码可以为事件添加和移除处理程序，但不能直接获取或修改底层的事件处理程序列表。

在形式为 `x += y` 或 `x -= y` 的操作中，当 x 是事件时，操作的结果类型为 void（§12.21.5）（而不是像非事件类型上定义的其它 `+=` 和 `-=` 运算符那样，具有 x 的类型以及赋值后 x 的值）。这可以防止外部代码间接检查事件的底层委托。

示例：以下示例展示了如何将事件处理程序附加到 Button 类的实例：

```
public delegate void EventHandler(object sender, EventArgs e);

public class Button : Control
{
    public event EventHandler Click;
}
```

```
public class LoginDialog : Form
{
    Button okButton;
    Button cancelButton;

    public LoginDialog()
    {
        okButton = new Button(...);
        okButton.Click += new EventHandler(OkButtonClick);
        cancelButton = new Button(...);
        cancelButton.Click += new EventHandler(CancelButtonClick);
    }

    void OkButtonClick(object sender, EventArgs e)
    {
        // 处理 okButton.Click 事件
    }

    void CancelButtonClick(object sender, EventArgs e)
    {
        // 处理 cancelButton.Click 事件
    }
}
```

此处，LoginDialog 实例构造函数创建了两个 Button 实例，并将事件处理程序附加到 Click 事件。

*示例结束*

### 15.8.2 类字段事件

在包含事件声明的类或结构的程序文本中，某些事件可以像字段一样使用。要以这种方式使用，事件不得是 abstract 或 extern，并且不得显式包含 event_accessor_declarations。此类事件可以在允许字段的任何上下文中使用。该字段包含一个委托（§20），该委托引用已添加到事件中的事件处理程序列表。如果尚未添加任何事件处理程序，则该字段包含 null。

示例：在以下代码中

```
public delegate void EventHandler(object sender, EventArgs e);

public class Button : Control
{
    public event EventHandler Click;

    protected void OnClick(EventArgs e)
    {
        EventHandler handler = Click;
        if (handler != null)
        {
            handler(this, e);
        }
    }
}
```

```
public void Reset() => Click = null;
}
```

在 Button 类中，Click 被用作字段。如示例所示，该字段可以被检查、修改，并用于委托调用表达式。Button 类中的 OnClick 方法“触发”Click 事件。触发事件的概念与调用事件所表示的委托完全相同——因此，没有专门的语言结构用于触发事件。请注意，委托调用之前会进行检查以确保委托非 null，并且该检查在局部副本上进行以确保线程安全。

在 Button 类声明之外，Click 成员只能用在 `+=` 和 `-=` 运算符的左侧，例如

```
b.Click += new EventHandler(...);
```

该操作将一个委托追加到 Click 事件的调用列表中，以及

```
Click -= new EventHandler(...);
```

该操作从 Click 事件的调用列表中移除一个委托。

示例结束

在编译类字段事件时，编译器会自动创建存储来保存委托，并为事件创建访问器，以向委托字段添加或移除事件处理程序。添加和移除操作是线程安全的，并且可以（但不是必须）在持有包含对象的锁（§13.13）（对于实例事件）或 System.Type 对象（§12.8.17）（对于静态事件）的情况下进行。

注意：因此，形式为：

```
class X
{
    public event D Ev;
}
```

的实例事件声明应编译为等效于：

### 15.8.3 事件访问器

注意：事件声明通常省略 event_accessor_declarations，如上面的 Button 示例所示。例如，如果为每个事件提供一个字段的存储成本不可接受，则可能包含这些访问器。在这种情况下，类可以包含 event_accessor_declarations 并使用私有机制来存储事件处理程序列表。注意结束

事件的 event_accessor_declarations 指定与添加和移除事件处理程序关联的可执行语句。

访问器声明由 add_accessor_declaration 和 remove_accessor_declaration 组成。每个访问器声明由 token `add` 或 `remove` 后跟一个 block 组成。与 add_accessor_declaration 关联的 block 指定添加事件处理程序时要执行的语句，与 remove_accessor_declaration 关联的 block 指定移除事件处理程序时要执行的语句。

每个 add_accessor_declaration 和 remove_accessor_declaration 对应一个方法，该方法具有事件类型的一个值参数和 void 返回类型。事件访问器的隐式参数名为 value。当事件用于事件赋值时，会使用相应的事件访问器。具体来说，如果赋值运算符是 `+=`，则使用 add 访问器；如果赋值运算符是 `-=`，则使用 remove 访问器。在这两种情况下，赋值运算符的右操作数都用作事件访问器的参数。add_accessor_declaration 或 remove_accessor_declaration 的 block 应符合 §15.6.9 中描述的 void 方法规则。特别是，此类 block 中的 return 语句不允许指定表达式。

由于事件访问器隐式具有名为 value 的参数，因此在事件访问器中声明的局部变量或常量不能使用该名称，否则属于编译时错误。

示例：在以下代码中

```
class Control : Component
{
    // 事件的唯一键
    static readonly object mouseDownEventKey = new object();
    static readonly object mouseUpEventKey = new object();

    // 返回与键关联的事件处理程序
    protected Delegate GetEventHandler(object key) {...}

    // 添加与键关联的事件处理程序
    protected void AddEventHandler(object key, Delegate handler) {...}

    // 移除与键关联的事件处理程序
    protected void RemoveEventHandler(object key, Delegate handler) {...}

    // MouseDown 事件
    public event MouseEventHandler MouseDown
    {
        add { AddEventHandler(mouseDownEventKey, value); }
        remove { RemoveEventHandler(mouseDownEventKey, value); }
    }

    // MouseUp 事件
    public event MouseEventHandler MouseUp
```


```
{
    add { AddEventHandler(mouseUpEventKey, value); }
    remove { RemoveEventHandler(mouseUpEventKey, value); }
}

// Invoke the MouseUp event
protected void OnMouseUp(MouseEventArgs args)
{
    MouseEventHandler handler;
    handler = (MouseEventHandler)GetEventHandler(mouseUpEventKey);
    if (handler != null)
    {
        handler(this, args);
    }
}
```

Control 类为事件实现了一种内部存储机制。AddEventHandler 方法将委托值与键关联，GetEventHandler 方法返回当前与键关联的委托，RemoveEventHandler 方法移除作为指定事件处理程序的委托。可以推测，底层存储机制的设计使得将空委托值与键关联不会产生开销，因此未处理的事件不消耗存储。

*示例结束*

## 15.8.4 静态事件和实例事件

当事件声明包含 static 修饰符时，该事件称为静态事件。当不存在 static 修饰符时，该事件称为实例事件。

静态事件不与特定实例关联，在静态事件的访问器中引用 this 属于编译时错误。

实例事件与类的给定实例关联，并且可以在该事件的访问器中通过 this（§12.8.13）访问此实例。

静态成员和实例成员之间的差异在 §15.3.8 中进一步讨论。

## 15.8.5 虚拟、密封、重写和抽象访问器

虚拟事件声明指定该事件的访问器是虚拟的。virtual 修饰符适用于事件的两个访问器。

重写事件声明不声明新事件。相反，它只是专门化现有虚拟事件的访问器的实现。

重写事件声明应指定与被重写事件完全相同的可访问性修饰符和名称，重写事件与被重写事件的类型之间应存在标识转换，并且 add 和 remove 访问器都应在该声明中指定。

重写事件声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该事件。密封事件的访问器也是密封的。

重写事件声明包含 new 修饰符属于编译时错误。

除了声明和调用语法上的差异外，虚拟、密封、重写和抽象访问器的行为与虚拟、密封、重写和抽象方法完全相同。具体而言，§15.6.4、§15.6.5、§15.6.6 和 §15.6.7 中描述的规则适用，就如同访问器是相应形式的方法一样。每个访问器对应于一个方法，该方法具有一个事件类型的值参数、一个 void 返回类型，以及与包含事件相同的修饰符。

## 15.9 索引器

### 15.9.1 概述

索引器是一种成员，它使对象能够像数组一样被索引。索引器使用 indexer_declarations 声明：

```
indexer_declaration
  : attributes? indexer_modifier* indexer_declarator indexer_body
  | attributes? indexer_modifier* ref_kind indexer_declarator ref_indexer_body
  ;

indexer_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'virtual'
  | 'sealed'
  | 'override'
  | 'abstract'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

indexer_declarator
  : type 'this' '[' formal_parameter_list ']'
  | type interface_type '.' 'this' '[' formal_parameter_list ']'
  ;

indexer_body
  : '{' accessor_declarations '}'
  | '=>' expression ';'
  ;

ref_indexer_body
  : '{' ref_get_accessor_declaration '}'
  | '=>' 'ref' variable_reference ';'
  ;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

indexer_declaration 有两种：

-   第一种声明非 ref 值索引器。其值的类型为 type。这种索引器可以是可读的和/或可写的。
-   第二种声明 ref 值索引器。其值是一个 variable_reference（§9.5），它可以是只读的，指向类型为 type 的变量。这种索引器只能读取。

indexer_declaration 可以包含一组特性（§22），以及允许的任一种已声明可访问性（§15.3.6），以及 new（§15.3.5）、virtual（§15.6.4）、override（§15.6.5）、sealed（§15.6.6）、abstract（§15.6.7）和 extern（§15.6.8）修饰符。

索引器声明在修饰符的有效组合方面遵循与方法声明（§15.6）相同的规则，唯一例外是索引器声明上不允许使用 static 修饰符。

索引器声明的类型指定该声明所引入的索引器的元素类型。

注意：由于索引器设计用于类似数组元素的情境，为数组定义的术语“元素类型”也用于索引器。注意结束。

formal_parameter_list 指定索引器的参数。索引器的形参列表对应于方法的形参列表（§15.6.2），但至少应指定一个参数，并且不允许使用 this、out 和 ref 参数修饰符。

除非索引器是显式接口成员实现，否则类型后面跟关键字 this。对于显式接口成员实现，类型后面跟一个 interface_type、一个“.”和关键字 this。与其他成员不同，索引器没有用户定义的名称。

formal_parameter_list 指定索引器的参数。索引器的形参列表对应于方法的形参列表（§15.6.2），但至少应指定一个参数，并且不允许使用 this、ref 和 out 参数修饰符。

索引器的类型以及 formal_parameter_list 中引用的每个类型，其可访问性至少应与索引器本身相同（§7.5.5）。

indexer_body 可以由语句体（§15.7.1）或表达式体（§15.6.1）组成。在语句体中，accessor_declarations（应包含在“{”和“}”标记中）声明索引器的访问器（§15.7.3）。这些访问器指定与读取和写入索引器元素相关联的可执行语句。

在 indexer_body 中，由“=>”后跟表达式 E 和分号组成的表达式体完全等价于语句体 { get { return E; } }，因此只能用于指定只读索引器，其中 get 访问器的结果由单个表达式给出。

ref_indexer_body 可以由语句体或表达式体组成。在语句体中，get_accessor_declaration 声明该属性的 get 访问器（§15.7.3）。该访问器指定与读取该属性相关联的可执行语句。

在 ref_indexer_body 中，由 => 后跟 ref、一个 variable_reference V 和分号组成的表达式体完全等价于语句体 { get { return ref V; } }。

注意：尽管访问索引器元素的语法与访问数组元素的语法相同，但索引器元素不被归类为变量。因此，除非索引器是 ref 值索引器并因此返回引用（§9.7），否则不能将索引器元素作为 in、out 或 ref 实参传递。注意结束。

索引器的 formal_parameter_list 定义索引器的签名（§7.6）。具体而言，索引器的签名由其形参的数量和类型组成。元素类型和形参名称不属于索引器签名的一部分。

索引器的签名应不同于同一类中声明的所有其他索引器的签名。

当索引器声明包含 extern 修饰符时，该索引器称为外部索引器。由于外部索引器声明不提供实际实现，其每个 accessor_declarations 都由一个分号组成。

示例：下面的示例声明一个 BitArray 类，该类实现一个索引器，用于访问位数组中的各个位。

```
class BitArray
{
    int[] bits;
    int length;

    public BitArray(int length)
    {
        if (length < 0)
        {
            throw new ArgumentException();
        }
        bits = new int[((length - 1) >> 5) + 1];
        this.length = length;
    }

    public int Length => length;

    public bool this[int index]
    {
        get
        {
            if (index < 0 || index >= length)
            {
                throw new IndexOutOfRangeException();
            }
            return (bits[index >> 5] & 1 << index) != 0;
        }
        set
        {
            if (index < 0 || index >= length)
            {
                throw new IndexOutOfRangeException();
            }
            if (value)
            {
                bits[index >> 5] |= 1 << index;
            }
        }
    }
}
```




```csharp
        else
        {
            bits[index >> 5] &= ~(1 << index);
        }
    }
}
```

`BitArray` 类的实例消耗的内存远少于相应的 `bool[]`（因为前者的每个值只占用一位，而不是后者的一个字节），但它允许与 `bool[]` 相同的操作。

以下 `CountPrimes` 类使用 `BitArray` 和经典的“筛法”算法来计算 2 到给定最大值之间的素数个数：

```csharp
class CountPrimes
{
    static int Count(int max)
    {
        BitArray flags = new BitArray(max + 1);
        int count = 0;
        for (int i = 2; i <= max; i++)
        {
            if (!flags[i])
            {
                for (int j = i * 2; j <= max; j += i)
                {
                    flags[j] = true;
                }
                count++;
            }
        }
        return count;
    }

    static void Main(string[] args)
    {
        int max = int.Parse(args[0]);
        int count = Count(max);
        Console.WriteLine($"Found {count} primes between 2 and {max}");
    }
}
```

注意，访问 `BitArray` 元素的语法与访问 `bool[]` 元素的语法完全相同。

以下示例展示了一个 26×10 网格类，它有一个带两个参数的索引器。第一个参数要求是 A–Z 范围内的大写或小写字母，第二个参数要求是 0–9 范围内的整数。

```csharp
class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;
    int[,] cells = new int[NumRows, NumCols];

    public int this[char row, int col]
    {
        get
        {
            row = Char.ToUpper(row);
            if (row < 'A' || row > 'Z')
            {
                throw new ArgumentOutOfRangeException("row");
            }
            if (col < 0 || col >= NumCols)
            {
                throw new ArgumentOutOfRangeException ("col");
            }
            return cells[row - 'A', col];
        }
        set
        {
            row = Char.ToUpper(row);
            if (row < 'A' || row > 'Z')
            {
                throw new ArgumentOutOfRangeException ("row");
            }
            if (col < 0 || col >= NumCols)
            {
                throw new ArgumentOutOfRangeException ("col");
            }
            cells[row - 'A', col] = value;
        }
    }
}
*end example*
```

## 15.9.2 索引器与属性的差异

索引器和属性在概念上非常相似，但在以下方面有所不同：

- 属性通过其名称标识，而索引器通过其签名标识。
- 属性通过 simple_name（§12.8.4）或 member_access（§12.8.7）访问，而索引器元素通过 element_access（§12.8.11.3）访问。
- 属性可以是静态成员，而索引器始终是实例成员。
- 属性的 get 访问器对应于无参数的方法，而索引器的 get 访问器对应于与索引器具有相同形参列表的方法。
- 属性的 set 访问器对应于具有名为 value 的单个参数的方法，而索引器的 set 访问器对应于与索引器具有相同形参列表并外加一个名为 value 的参数的方法。
- 如果索引器访问器声明的局部变量或局部常量与索引器参数同名，则属于编译时错误。
- 在重写属性声明中，继承的属性使用语法 base.P 访问，其中 P 是属性名。在重写索引器声明中，继承的索引器使用语法 base[E] 访问，其中 E 是以逗号分隔的表达式列表。

- 不存在“自动实现的索引器”的概念。具有分号访问器的非抽象、非外部索引器是错误的。

除这些差异外，§15.7.3、§15.7.5 和 §15.7.6 中定义的所有规则也适用于索引器访问器以及属性访问器。

> 注意：在阅读 §15.7.3、§15.7.5 和 §15.7.6 时，将 property/properties 替换为 indexer/indexers 的做法同样适用于已定义术语。例如，read-write property 变为 read-write-indexer。结束注意

## 15.10 运算符

### 15.10.1 概述

运算符是一种成员，它定义可应用于类实例的表达式运算符的含义。运算符使用 operator_declarations 声明：

```csharp
operator_declaration
  : attributes? operator_modifier+ operator_declarator operator_body
  ;

operator_modifier
  : 'public'
  | 'static'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

operator_declarator
  : unary_operator_declarator
  | binary_operator_declarator
  | conversion_operator_declarator
  ;

unary_operator_declarator
  : type 'operator' overloadable_unary_operator '(' fixed_parameter ')'
  ;

overloadable_unary_operator
  : '+' | '-' | '!' | '~' | '++' | '--' | 'true' | 'false'
  ;

binary_operator_declarator
  : type 'operator' overloadable_binary_operator
    '(' fixed_parameter ',' fixed_parameter ')'
  ;

overloadable_binary_operator
  : '+' | '-' | '*' | '/' | '%' | '&' | '|' | '^' | '<<'
  | right_shift | '==' | '!=' | '>' | '<' | '>=' | '<='
  ;

conversion_operator_declarator
  : 'implicit' 'operator' type '(' fixed_parameter ')'
  | 'explicit' 'operator' type '(' fixed_parameter ')'
```

```
;
operator_body
: block
| '=>' expression ';'
| ';'
;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

可重载运算符分为三类：一元运算符（§15.10.2）、二元运算符（§15.10.3）和转换运算符（§15.10.4）。

operator_body 是分号、块体（§15.6.1）或表达式体（§15.6.1）。块体由一个块组成，该块指定调用运算符时要执行的语句。该块应符合 §15.6.11 中所述的返回值方法规则。表达式体由 => 后跟一个表达式和分号组成，表示调用运算符时要执行的单个表达式。

对于 extern 运算符，operator_body 仅由分号组成。对于所有其他运算符，operator_body 是块体或表达式体。

以下规则适用于所有运算符声明：

- 运算符声明应同时包含 public 和 static 修饰符。
- 运算符的参数除 in 外不得带有其他修饰符。
- 运算符的签名（§15.10.2、§15.10.3、§15.10.4）应不同于同一类中声明的所有其他运算符的签名。
- 运算符声明中引用的所有类型应至少与运算符本身一样可访问（§7.5.5）。
- 同一修饰符在运算符声明中多次出现是错误的。

每个运算符类别都施加额外限制，如以下子条款所述。

与其他成员一样，基类中声明的运算符由派生类继承。由于运算符声明始终要求声明该运算符的类或结构参与运算符的签名，因此派生类中声明的运算符不可能隐藏基类中声明的运算符。因此，new 修饰符从不需要，也从不允许出现在运算符声明中。

有关一元运算符和二元运算符的更多信息，请参见 §12.4。

有关转换运算符的更多信息，请参见 §10.5。

### 15.10.2 一元运算符

以下规则适用于一元运算符声明，其中 T 表示包含该运算符声明的类或结构的实例类型：

- 一元 +、-、! 或 ~ 运算符应接受一个类型为 T 或 T? 的单个参数，并且可以返回任何类型。
- 一元 ++ 或 -- 运算符应接受一个类型为 T 或 T? 的单个参数，并且应返回该相同类型或由其派生的类型。
- 一元 true 或 false 运算符应接受一个类型为 T 或 T? 的单个参数，并且应返回 bool 类型。

一元运算符的签名由运算符标记（+、-、!、~、++、--、true 或 false）和单个形参的类型组成。返回类型不是一元运算符签名的一部分，形参名称也不是。

true 和 false 一元运算符要求成对声明。如果类声明了其中一个运算符而未同时声明另一个，则发生编译时错误。true 和 false 运算符在 §12.24 中进一步描述。

示例：以下示例展示了一个整数向量类的 operator++ 的实现及后续用法：

```csharp
public class IntVector
{
    public IntVector(int length) {...}
    public int Length { get { ... } }                     // Read-only property
    public int this[int index] { get { ... } set { ... } } // Read-write indexer

    public static IntVector operator++(IntVector iv)
    {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
        {
            temp[i] = iv[i] + 1;
        }
        return temp;
    }
}

class Test
{
    static void Main()
    {
        IntVector iv1 = new IntVector(4); // Vector of 4 x 0
        IntVector iv2;
        iv2 = iv1++;                     // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;                     // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

请注意，该运算符方法如何返回将操作数加 1 后产生的值，就像后缀递增和递减运算符（§12.8.15）以及前缀递增和递减运算符（§12.9.6）一样。与 C++ 不同，此方法不应直接修改其操作数的值，因为这会违反后缀递增运算符（§12.8.15）的标准语义。

*示例结束*

### 15.10.3 二元运算符

以下规则适用于二元运算符声明，其中 T 表示包含该运算符声明的类或结构的实例类型：

- 二元非移位运算符应接受两个参数，其中至少一个参数的类型应为 T 或 T?，并且可以返回任何类型。
- 二元 << 或 >> 运算符（§12.11）应接受两个参数，其中第一个参数的类型应为 T 或 T?，第二个参数的类型应为 int 或 int?，并且可以返回任何类型。一个……的签名

二元运算符由运算符标记（+、-、*、/、%、&、|、^、<<、>>、==、!=、>、<、>= 或 <=）和两个形参的类型组成。返回类型和形参的名称不属于二元运算符签名的一部分。

某些二元运算符要求成对声明。对于一对运算符中任一运算符的每个声明，都应当存在该对中另一运算符的匹配声明。如果两个运算符声明的返回类型之间以及相应参数类型之间存在恒等转换，则这两个运算符声明匹配。以下运算符要求成对声明：

- 运算符 == 和运算符 !=
- 运算符 > 和运算符 <
- 运算符 >= 和运算符 <=

## 15.10.4 转换运算符

转换运算符声明引入用户定义转换（§10.5），它扩充预定义的隐式和显式转换。

包含 implicit 关键字的转换运算符声明引入用户定义隐式转换。隐式转换可发生在多种情况下，包括函数成员调用、强制转换表达式和赋值。§10.2 对此作了进一步描述。

包含 explicit 关键字的转换运算符声明引入用户定义显式转换。显式转换可发生在强制转换表达式中，§10.3 对此作了进一步描述。

转换运算符从源类型（由转换运算符的参数类型指示）转换为目标类型（由转换运算符的返回类型指示）。

对于给定的源类型 S 和目标类型 T，如果 S 或 T 是可空值类型，则令 S0 和 T0 指代其基础类型；否则，S0 和 T0 分别等于 S 和 T。仅当以下所有条件均成立时，才允许类或结构声明从源类型 S 到目标类型 T 的转换：

- S0 和 T0 是不同的类型。
- S0 或 T0 是包含该运算符声明的类或结构的实例类型。
- S0 和 T0 都不是接口类型。
- 除用户定义转换外，不存在从 S 到 T 或从 T 到 S 的转换。

为这些规则的目的，与 S 或 T 关联的任何类型参数均被视为唯一类型，与其他类型没有继承关系，并且忽略对这些类型参数的任何约束。

示例：在以下内容中：

```
class C<T> { ... }

class D<T> : C<T>
{
    public static implicit operator C<int>(D<T> value) {...}  // Ok
    public static implicit operator C<string>(D<T> value) {...}  // Ok
    public static implicit operator C<T>(D<T> value) {...}  // Error
}
```

前两个运算符声明是允许的，因为 T 与 int 和 string 分别被视为没有关系的唯一类型。然而，第三个运算符是错误的，因为 C<T> 是 D<T> 的基类。

*示例结束*

由第二条规则可知，转换运算符必须转换到声明该运算符的类或结构类型，或者从该类型转换。

*示例：* 类或结构类型 C 可以定义从 C 到 int 以及从 int 到 C 的转换，但不能定义从 int 到 bool 的转换。*示例结束*

无法直接重新定义预定义转换。因此，不允许转换运算符从 object 转换或转换为 object，因为 object 与所有其他类型之间已经存在隐式和显式转换。同样，转换的源类型和目标类型都不能是对方的基础类型，因为此时转换已经存在。然而，可以在泛型类型上声明运算符，这些运算符对于特定类型实参指定已经作为预定义转换存在的转换。

*示例：*

```
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```

当类型 object 被指定为 T 的类型实参时，第二个运算符声明了一个已经存在的转换（存在从任何类型到类型 object 的隐式转换，因此也存在显式转换）。

*示例结束*

如果两个类型之间存在预定义转换，则忽略这些类型之间的任何用户定义转换。具体而言：

- 如果存在从类型 S 到类型 T 的预定义隐式转换（§10.2），则忽略从 S 到 T 的所有用户定义转换（隐式或显式）。
- 如果存在从类型 S 到类型 T 的预定义显式转换（§10.3），则忽略从 S 到 T 的任何用户定义显式转换。此外：
  - 如果 S 或 T 是接口类型，则忽略从 S 到 T 的用户定义隐式转换。
  - 否则，仍考虑从 S 到 T 的用户定义隐式转换。

对于除 object 之外的所有类型，上述 Convertible<T> 类型声明的运算符不会与预定义转换冲突。

*示例：*

```
void F(int i, Convertible<int> n)
{
    i = n;                     // Error
    i = (int)n;                // User-defined explicit conversion
    n = i;                     // User-defined implicit conversion
    n = (Convertible<int>)i;   // User-defined implicit conversion
}
```

然而，对于类型 object，预定义转换在除一种情况外的所有情况下都会隐藏用户定义转换：

```
void F(object o, Convertible<object> n)
{
    o = n;                // Pre-defined boxing conversion
    o = (object)n;        // Pre-defined boxing conversion
    n = o;                // User-defined implicit conversion
    n = (Convertible<object>)o; // Pre-defined unboxing conversion
}
```

示例结束

不允许用户定义转换从接口类型转换或转换为接口类型。特别地，此限制确保在转换为接口类型时不会发生用户定义转换，并且仅当被转换的对象实际实现指定接口类型时，到接口类型的转换才成功。

转换运算符的签名由源类型和目标类型组成。（这是返回类型参与签名的唯一成员形式。）转换运算符的隐式或显式分类不属于该运算符的签名。因此，类或结构不能声明具有相同源类型和目标类型的隐式转换运算符和显式转换运算符。

注意：通常，用户定义隐式转换应设计为从不引发异常且从不丢失信息。如果用户定义转换可能引发异常（例如，因为源参数超出范围）或丢失信息（例如丢弃高位），则该转换应定义为显式转换。注意结束

示例：在以下代码中

```
public struct Digit
{
    byte value;

    public Digit(byte value)
    {
        if (value < 0 || value > 9)
        {
            throw new ArgumentException();
        }
        this.value = value;
    }

    public static implicit operator byte(Digit d) => d.value;
    public static explicit operator Digit(byte b) => new Digit(b);
}
```

从 Digit 到 byte 的转换是隐式的，因为它从不引发异常或丢失信息；而从 byte 到 Digit 的转换是显式的，因为 Digit 只能表示 byte 可能值的一个子集。

示例结束

## 15.11 实例构造函数

### 15.11.1 概述

*实例构造函数*是一种成员，它实现初始化类实例所需的行为。实例构造函数使用*构造函数声明*来声明：

```
constructor_declaration
  : attributes? constructor_modifier* constructor_declarator constructor_body
  ;

constructor_modifier
  : 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

constructor_declarator
  : identifier '(' formal_parameter_list? ')' constructor_initializer?
  ;

constructor_initializer
  : ':' 'base' '(' argument_list? ')'
  | ':' 'this' '(' argument_list? ')'
  ;

constructor_body
  : block
  | '=>' expression ';'
  | ';'
  ;
```

*不安全修饰符*（§23.2）仅在不安全代码（§23）中可用。

*构造函数声明*可以包含一组*特性*（§22）、任一允许种类的已声明*可访问性*（§15.3.6）以及 *extern*（§15.6.8）修饰符。不允许构造函数声明多次包含同一修饰符。

*构造函数声明符*的*标识符*应当命名声明该实例构造函数的类。如果指定任何其他名称，则发生编译时错误。

实例构造函数的可选*形参列表*遵循与方法的*形参列表*相同的规则（§15.6）。由于参数的 *this* 修饰符仅适用于扩展方法（§15.6.10），构造函数*形参列表*中的任何参数都不得包含 *this* 修饰符。形参列表定义实例构造函数的签名（§7.6），并支配重载决策（§12.6.4）在调用中选择特定实例构造函数的过程。

实例构造函数*形参列表*中引用的每个类型都应当至少与构造函数本身一样可访问（§7.5.5）。





可选的构造函数初始化器指定在执行为该实例构造函数的构造函数体给定的语句之前，要调用的另一个实例构造函数。这一点将在 §15.11.2 中进一步说明。

当一个构造函数声明包含 `extern` 修饰符时，该构造函数称为外部构造函数。由于外部构造函数声明不提供实际实现，其构造函数体仅包含一个分号。对于所有其他构造函数，构造函数体由以下之一组成：

- 一个块，指定用于初始化类的新实例的语句；或
- 一个表达式体，由 `=>` 后跟表达式和分号组成，表示用单个表达式初始化类的新实例。

作为块或表达式体的构造函数体，与返回类型为 `void` 的实例方法的主体完全对应（§15.6.11）。

实例构造函数不会被继承。因此，一个类除了实际在类中声明的实例构造函数之外，没有其他实例构造函数；例外情况是，如果类不包含任何实例构造函数声明，则会自动提供一个默认实例构造函数（§15.11.5）。

实例构造函数通过 `object_creation_expressions`（§12.8.16.2）和构造函数初始化器来调用。

## 15.11.2 构造函数初始化器

所有实例构造函数（`class object` 的构造函数除外）都在构造函数体之前隐式包含对另一个实例构造函数的调用。要隐式调用的构造函数由构造函数初始化器确定：

- 形式为 `base(argument_list)` 的实例构造函数初始化器（其中 `argument_list` 是可选的）会导致调用直接基类中的某个实例构造函数。该构造函数使用 `argument_list` 和 §12.6.4 的重载解析规则进行选择。候选实例构造函数集由直接基类的所有可访问实例构造函数组成。如果该集合为空，或无法确定唯一的最佳实例构造函数，则会发生编译时错误。
- 形式为 `this(argument_list)` 的实例构造函数初始化器（其中 `argument_list` 是可选的）会调用同一个类中的另一个实例构造函数。该构造函数使用 `argument_list` 和 §12.6.4 的重载解析规则进行选择。候选实例构造函数集由类本身声明的所有实例构造函数组成。如果得到的适用实例构造函数集为空，或无法确定唯一的最佳实例构造函数，则会发生编译时错误。如果某个实例构造函数声明通过一个或多个构造函数初始化器链调用自身，则会发生编译时错误。

如果实例构造函数没有构造函数初始化器，则会隐式提供一个形式为 `base()` 的构造函数初始化器。

> 注意：因此，形式为
> C(...) {...}
> 的实例构造函数声明完全等价于
> C(...) : base() {...}
> 结束注释

实例构造函数声明的形式参数列表给出的参数的作用域包括该声明的构造函数初始化器。因此，构造函数初始化器可以访问构造函数的参数。

示例：

```
class A
{
    public A(int x, int y) {}
}

class B: A
{
    public B(int x, int y) : base(x + y, x - y) {}
}
```

示例结束

实例构造函数初始化器不能访问正在创建的实例。因此，在构造函数初始化器的参数表达式中引用 `this` 是编译时错误，同样，参数表达式通过 `simple_name` 引用任何实例成员也是编译时错误。

## 15.11.3 实例变量初始化器

当实例构造函数没有构造函数初始化器，或者具有 `base(...)` 形式的构造函数初始化器时，该构造函数会隐式执行其类中声明的实例字段的变量初始化器所指定的初始化。这对应于一序列赋值，这些赋值在进入构造函数时立即执行，并且在隐式调用直接基类构造函数之前执行。变量初始化器按照它们在类声明中出现的文本顺序执行（§15.5.6）。

## 15.11.4 构造函数执行

变量初始化器会被转换为赋值语句，并且这些赋值语句在调用基类实例构造函数之前执行。这种顺序确保所有实例字段在进行任何可访问该实例的语句执行之前，已由其变量初始化器初始化。

示例：给定以下代码：

```
class A
{
    public A()
    {
        PrintFields();
    }

    public virtual void PrintFields() {}
}
class B: A
{
    int x = 1;
    int y;

    public B()
    {
        y = -1;
    }

    public override void PrintFields() =>
        Console.WriteLine($"x = {x}, y = {y}");
}
```

当使用 `new B()` 创建 B 的实例时，会产生以下输出：

x = 1, y = 0

x 的值为 1，因为变量初始化器在基类实例构造函数被调用之前执行。然而，y 的值为 0（`int` 的默认值），因为对 y 的赋值直到基类构造函数返回之后才执行。把实例变量初始化器和构造函数初始化器看作是自动插入到构造函数体之前的语句，是很有帮助的。示例：

```
class A
{
    int x = 1, y = -1, count;

    public A()
    {
        count = 0;
    }

    public A(int n)
    {
        count = n;
    }
}

class B : A
{
    double sqrt2 = Math.Sqrt(2.0);
    ArrayList items = new ArrayList(100);
    int max;

    public B(): this(100)
    {
        items.Add("default");
    }

    public B(int n) : base(n - 1)
    {
        max = n;
    }
}
```

包含几个变量初始化器；也包含两种形式（`base` 和 `this`）的构造函数初始化器。该示例对应于下面显示的代码，其中每个注释表示一个自动插入的语句（用于自动插入的构造函数调用的语法无效，但仅用于说明该机制）。

```
class A
{
    int x, y, count;
    public A()
    {
        x = 1;    // Variable initializer
        y = -1;   // Variable initializer
        object(); // Invoke object() constructor
        count = 0;
    }

    public A(int n)
    {
        x = 1;    // Variable initializer
        y = -1;   // Variable initializer
        object(); // Invoke object() constructor
        count = n;
    }
}

class B : A
{
    double sqrt2;
    ArrayList items;
    int max;
    public B() : this(100)
    {
        B(100);               // Invoke B(int) constructor
        items.Add("default");
    }

    public B(int n) : base(n - 1)
    {
        sqrt2 = Math.Sqrt(2.0);          // Variable initializer
        items = new ArrayList(100);      // Variable initializer
        A(n - 1);                        // Invoke A(int) constructor
        max = n;
    }
}
```

示例结束

## 15.11.5 默认构造函数

如果一个类不包含任何实例构造函数声明，则会自动提供一个默认实例构造函数。该默认构造函数只是调用直接基类的某个构造函数，就好像它具有 `base()` 形式的构造函数初始化器一样。如果类是抽象类，则默认构造函数的声明可访问性是 `protected`。否则，默认构造函数的声明可访问性是 `public`。

> 注意：因此，默认构造函数总是以下形式：

```
protected C(): base() {}
```

或

```
public C(): base() {}
```

其中 C 是类名。

如果重载解析无法确定基类构造函数初始化器的唯一最佳候选，则会发生编译时错误。

示例：在以下代码中

```
class Message
{
    object sender;
    string text;
}
```

由于该类不包含任何实例构造函数声明，因此提供了一个默认构造函数。因此，该示例完全等价于：

```
class Message
{
    object sender;
    string text;
    public Message() : base() {}
}
```

示例结束

## 15.12 静态构造函数

静态构造函数是一个成员，它实现初始化封闭类所需执行的操作。静态构造函数使用 `static_constructor_declarations` 声明：

```
static_constructor_declaration
    : attributes? static_constructor_modifiers identifier '(' ')'
      static_constructor_body
    ;

static_constructor_modifiers
    : 'static'
    | 'static' 'extern' unsafe_modifier?
    | 'static' unsafe_modifier 'extern'?
    | 'extern' 'static' unsafe_modifier?
    | 'extern' unsafe_modifier 'static'?
    | unsafe_modifier 'static' 'extern'?
    | unsafe_modifier 'extern' 'static'
    ;

static_constructor_body
    : block
    | '=>' expression ';'
    | ';'
    ;
```

`unsafe_modifier`（§23.2）仅在不安全代码（§23）中可用。

`static_constructor_declaration` 可以包含一组特性（attribute）（§22）和一个 `extern` 修饰符（§15.6.8）。

`static_constructor_declaration` 的 `identifier` 必须指明声明静态构造函数所在的类。如果指定了任何其他名称，则会发生编译时错误。




当静态构造函数声明包含 extern 修饰符时，该静态构造函数被称为外部静态构造函数。由于外部静态构造函数声明不提供实际实现，其 static_constructor_body 由一个分号组成。对于所有其他静态构造函数声明，static_constructor_body 由以下之一组成：

- 一个块，指定为初始化类而执行的语句；或
- 一个表达式体，由 => 后跟一个表达式和一个分号组成，表示为初始化类而执行的一个表达式。

static_constructor_body 为块或表达式体时，与返回类型为 void 的静态方法的方法体 (§15.6.11) 完全对应。

静态构造函数不可继承，也不能直接调用。

某个封闭类的静态构造函数在一个应用程序域中最多执行一次。静态构造函数的执行由应用程序域内首先发生的以下事件触发：

- 创建了该类的一个实例。
- 引用了该类的任何静态成员。

如果某个类包含执行开始的 Main 方法 (§7.1)，则该类的静态构造函数在调用 Main 方法之前执行。

为初始化一个新的封闭类类型，首先为该特定封闭类型创建一个新的静态字段集 (§15.5.2)。每个静态字段都初始化为其默认值 (§15.5.5)。接下来，为这些静态字段执行静态字段初始值设定项 (§15.5.6.2)。最后，执行静态构造函数。

示例：以下示例

```
class Test
{
    static void Main()
    {
        A.F();
        B.F();
    }
}

class A
{
    static A()
    {
        Console.WriteLine("Init A");
    }

    public static void F()
    {
        Console.WriteLine("A.F");
    }
}

class B
{
    static B()
    {
        Console.WriteLine("Init B");
    }
    public static void F()
    {
        Console.WriteLine("B.F");
    }
}
```

必须产生以下输出：

```
Init A
A.F
Init B
B.F
```

因为 A 的静态构造函数的执行由对 A.F 的调用触发，而 B 的静态构造函数的执行由对 B.F 的调用触发。

示例结束

可以构造循环依赖，使得具有变量初始值设定项的静态字段在其默认值状态下被观察到。

示例：以下示例

```
class A
{
    public static int X;
    static A()
    {
        X = B.Y + 1;
    }
}

class B
{
    public static int Y = A.X + 1;
    static B() {}
    static void Main()
    {
        Console.WriteLine($"X = {A.X}, Y = {B.Y}");
    }
}
```

产生输出

```
X = 1, Y = 2
```

为执行 Main 方法，系统首先在类 B 的静态构造函数之前运行 B.Y 的初始值设定项。Y 的初始值设定项导致 A 的静态构造函数运行，因为引用了 A.X 的值。A 的静态构造函数进而计算 X 的值，在此过程中获取 Y 的默认值，即零。因此 A.X 被初始化为 1。运行 A 的静态字段初始值设定项和静态构造函数的过程随后完成，返回到 Y 初始值的计算，其结果变为 2。

*示例结束*

由于静态构造函数对每个封闭构造的类类型恰好执行一次，因此它是强制执行在编译时无法通过约束 (§15.2.5) 检查的类型参数的运行时检查的方便位置。

示例：以下类型使用静态构造函数强制类型参数为枚举：

```
class Gen<T> where T : struct
{
    static Gen()
    {
        if (!typeof(T).IsEnum)
        {
            throw new ArgumentException("T must be an enum");
        }
    }
}
```

*示例结束*

## 15.13 析构函数

注：在本规范的早期版本中，现在称为“finalizer”的内容曾被称为“destructor”。经验表明，“destructor”一词引起了混淆，并经常导致不正确的期望，尤其对于了解 C++ 的程序员而言。在 C++ 中，析构函数以确定的方式被调用，而在 C# 中，终结器则不会。要获得 C# 中的确定性行为，应使用 Dispose。 注结束

终结器是实现完成类实例所需操作的一个成员。终结器使用 finalizer_declaration 声明：

```
finalizer_declaration
  : attributes? '~' identifier '(' ')' finalizer_body
  | attributes? 'extern' unsafe_modifier? '~' identifier '(' ')'
    finalizer_body
  | attributes? unsafe_modifier 'extern'? '~' identifier '(' ')'
    finalizer_body
  ;

finalizer_body
  : block
  | '=>' expression ';'
  | ';'
  ;
```

unsafe_modifier (§23.2) 仅在不安全代码 (§23) 中可用。

finalizer_declaration 可能包含一组特性 (§22)。

finalizer_declarator 的标识符应命名声明终结器的类。如果指定了其他名称，则会发生编译时错误。

当终结器声明包含 extern 修饰符时，该终结器被称为外部终结器。由于外部终结器声明不提供实际实现，其 finalizer_body 由一个分号组成。对于所有其他终结器，finalizer_body 由以下之一组成：

- 一个块，指定为完成类实例而执行的语句。
- 或一个表达式体，由 => 后跟一个表达式和一个分号组成，表示为完成类实例而执行的一个表达式。

finalizer_body 为块或表达式体时，与返回类型为 void 的实例方法的方法体 (§15.6.11) 完全对应。

终结器不可继承。因此，类没有除其自身声明的终结器之外的其他终结器。

注：由于终结器要求没有参数，因此它不能被重载，所以一个类最多只能有一个终结器。 注结束

终结器是自动调用的，不能显式调用。当不再有任何代码可以使用该实例时，实例变为可终结。实例变为可终结后，其终结器的执行可能在任何时间发生 (§7.9)。当一个实例被终结时，其继承链中的终结器会按顺序调用，从最派生到最不派生。终结器可能在任何线程上执行。有关何时以及如何执行终结器的规则的进一步讨论，请参阅 §7.9。

示例：以下示例的输出

```
class A
{
    ~A()
    {
        Console.WriteLine("A's finalizer");
    }
}

class B : A
{
    ~B()
    {
        Console.WriteLine("B's finalizer");
    }
}

class Test
{
    static void Main()
    {
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

因为继承链中的终结器按顺序调用，从最派生到最不派生。

示例结束

终结器通过重写 System.Object 上的虚方法 Finalize 实现。C# 程序不允许直接重写此方法或调用它（或其重写）。

*示例*：例如，程序

```
class A
{
    override protected void Finalize() {}   // Error
    public void F()
    {
        this.Finalize();                    // Error
    }
}
```

包含两个错误。

*示例结束*

编译器表现得好像此方法及其重写根本不存在一样。

*示例*：因此，此程序：

```
class A
{
    void Finalize() {}  // Permitted
}
```

是有效的，并且所示方法隐藏了 System.Object 的 Finalize 方法。

*示例结束*

有关从终结器抛出异常时的行为讨论，请参阅 §21.4。

## 15.14 迭代器

### 15.14.1 通用

使用迭代器块 (§13.3) 实现的函数成员 (§12.6) 称为 *迭代器*。

迭代器块只要相应函数成员的返回类型是枚举器接口 (§15.14.2) 之一或可枚举接口 (§15.14.3) 之一，就可以作为函数成员的主体。它可以作为 *method_body*、*operator_body* 或 *accessor_body* 出现，而事件、实例构造函数、静态构造函数和终结器则不能实现为迭代器。

当函数成员使用迭代器块实现时，如果函数成员的形式参数列表指定了任何 *in*、*out* 或 *ref* 参数，或 *ref* 结构体类型的参数，则为编译时错误。

### 15.14.2 枚举器接口

*枚举器接口* 是非泛型接口 `System.Collections.IEnumerator` 以及泛型接口 `System.Collections.Generic.IEnumerator<T>` 的所有实例化。为简洁起见，在本小节及其兄弟小节中，这些接口分别简称为 `IEnumerator` 和 `IEnumerator<T>`。



## 15.14.3 Enumerable interfaces

可枚举接口是非泛型接口 System.Collections.IEnumerable 以及泛型接口 System.Collections.Generic.IEnumerable<T> 的所有实例化。为简洁起见，在本小节及其姊妹小节中，这些接口分别简称为 IEnumerable 和 IEnumerable<T>。

## 15.14.4 Yield type

迭代器产生一系列值，所有值类型相同。此类型称为迭代器的 yield 类型。

- 返回 IEnumerable 的迭代器的 yield 类型是 object。
- 返回 IEnumerable<T> 的迭代器的 yield 类型是 T。

## 15.14.5 Enumerator objects

### 15.14.5.1 General

当使用迭代器块实现返回枚举器接口类型的函数成员时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建一个枚举器对象并返回。该对象封装了迭代器块中指定的代码，并且迭代器块中的代码执行发生在调用枚举器对象的 MoveNext 方法时。枚举器对象具有以下特征：

- 它实现 IEnumerable 和 IEnumerable<T>，其中 T 是迭代器的 yield 类型。
- 它实现 System.IDisposable。
- 它使用传递给函数成员的参数值（如果有）和实例值的副本进行初始化。
- 它有四个可能的状态，before、running、suspended 和 after，并且初始时处于 before 状态。

枚举器对象通常是编译器生成的枚举器类的实例，该类封装了迭代器块中的代码并实现枚举器接口，但也可能采用其他实现方法。如果枚举器类由编译器生成，则该类将直接或间接嵌套在包含函数成员的类中，它将具有私有访问性，并且其名称将保留供编译器使用（§6.4.3）。

枚举器对象可能实现比上述更多的接口。

以下小节描述了枚举器对象提供的 IEnumerable 和 IEnumerable<T> 接口实现中 MoveNext、Current 和 Dispose 成员的必需行为。

枚举器对象不支持 IEnumerable.Reset 方法。调用此方法会导致抛出 System.NotSupportedException。

### 15.14.5.2 The MoveNext method

枚举器对象的 MoveNext 方法封装了迭代器块的代码。调用 MoveNext 方法会执行迭代器块中的代码并相应地设置枚举器对象的 Current 属性。MoveNext 执行的确切操作取决于调用 MoveNext 时枚举器对象的状态：

- 如果枚举器对象的状态为 before，调用 MoveNext：
  - 将状态更改为 **running**。
  - 将迭代器块的参数（包括 `this`）初始化为枚举器对象初始化时保存的参数值和实例值。
  - 从开头执行迭代器块，直到执行被中断（如下所述）。

- 如果枚举器对象的状态为 **running**，调用 `MoveNext` 的结果是不确定的。
- 如果枚举器对象的状态为 **suspended**，调用 `MoveNext`：
  - 将状态更改为 **running**。
  - 将所有局部变量和参数（包括 `this`）的值恢复为上次挂起迭代器块执行时保存的值。
  - *Note:* 这些变量引用的任何对象的内容可能自上次调用 `MoveNext` 以来已发生变化。 *end note*
  - 从导致执行挂起的 `yield return` 语句之后立即恢复迭代器块的执行，并继续执行直到执行被中断（如下所述）。
- 如果枚举器对象的状态为 **after**，调用 `MoveNext` 返回 `false`。

当 `MoveNext` 执行迭代器块时，执行可能以四种方式中断：通过 `yield return` 语句，通过 `yield break` 语句，通过遇到迭代器块的末尾，以及通过异常被抛出并传播出迭代器块。

- 当遇到 `yield return` 语句时（§9.4.4.20）：
  - 语句中给出的表达式被求值，隐式转换为 yield 类型，并赋给枚举器对象的 `Current` 属性。
  - 迭代器体的执行被挂起。所有局部变量和参数（包括 `this`）的值被保存，同时保存此 `yield return` 语句的位置。如果 `yield return` 语句位于一个或多个 `try` 块内，则相关的 `finally` 块此时不会执行。
  - 枚举器对象的状态更改为 **suspended**。
  - `MoveNext` 方法向其调用者返回 `true`，表示迭代成功推进到下一个值。

- 当遇到 `yield break` 语句时（§9.4.4.20）：
  - 如果 `yield break` 语句位于一个或多个 `try` 块内，则相关的 `finally` 块将被执行。
  - 枚举器对象的状态更改为 **after**。
  - `MoveNext` 方法向其调用者返回 `false`，表示迭代已完成。

- 当遇到迭代器体的末尾时：
  - 枚举器对象的状态更改为 **after**。
  - `MoveNext` 方法向其调用者返回 `false`，表示迭代已完成。

- 当异常被抛出并传播出迭代器块时：
  - 异常传播将已执行迭代器体中的适当 `finally` 块。
  - 枚举器对象的状态更改为 **after**。
  - 异常传播继续到 `MoveNext` 方法的调用者。

### 15.14.5.3 The Current property

枚举器对象的 `Current` 属性受迭代器块中 `yield return` 语句的影响。

当枚举器对象处于 **suspended** 状态时，`Current` 的值是上一次调用 `MoveNext` 时设置的值。当枚举器对象处于 **before**、**running** 或 **after** 状态时，访问 `Current` 的结果是不确定的。

对于 yield 类型不是 `object` 的迭代器，通过枚举器对象的 `IEnumerable` 实现访问 `Current` 的结果对应于通过枚举器对象的 `IEnumerable<T>` 实现访问 `Current` 并将结果强制转换为 `object`。

### 15.14.5.4 The Dispose method

`Dispose` 方法用于通过将枚举器对象带到 **after** 状态来清理迭代。

- 如果枚举器对象的状态为 **before**，调用 `Dispose` 将状态更改为 **after**。
- 如果枚举器对象的状态为 **running**，调用 `Dispose` 的结果是不确定的。
- 如果枚举器对象的状态为 **suspended**，调用 `Dispose`：
  - 将状态更改为 **running**。
  - 执行任何 finally 块，就好像最后执行的 `yield return` 语句是 `yield break` 语句一样。如果这导致异常被抛出并传播出迭代器体，则枚举器对象的状态设置为 **after**，并且异常传播到 `Dispose` 方法的调用者。
  - 将状态更改为 **after**。
- 如果枚举器对象的状态为 **after**，调用 `Dispose` 没有任何影响。

## 15.14.6 Enumerable objects

### 15.14.6.1 General

当使用迭代器块实现返回可枚举接口类型的函数成员时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建一个 **enumerable object** 并返回。可枚举对象的 `GetEnumerator` 方法返回一个封装了迭代器块中指定代码的枚举器对象，并且迭代器块中的代码执行发生在调用枚举器对象的 `MoveNext` 方法时。可枚举对象具有以下特征：

- 它实现 `IEnumerable` 和 `IEnumerable<T>`，其中 `T` 是迭代器的 yield 类型。
- 它使用传递给函数成员的参数值（如果有）和实例值的副本进行初始化。

可枚举对象通常是编译器生成的可枚举类的实例，该类封装了迭代器块中的代码并实现可枚举接口，但也可能采用其他实现方法。如果可枚举类由编译器生成，则该类将

直接或间接嵌套在包含该函数成员的类中时，它将具有私有可访问性，并且其名称将保留供编译器使用（§6.4.3）。

可枚举对象实现的接口可能多于上述接口。

> 备注：例如，可枚举对象还可以实现 IEnumerator 和 IEnumerator<T>，使其既能充当可枚举对象，又能充当枚举器。通常，此类实现会在第一次调用 GetEnumerator 时返回其自身实例（以节省分配）。后续对 GetEnumerator 的调用（如果有）将返回新的类实例，通常为同一个类，以便对不同枚举器实例的调用不会相互影响。即使前一个枚举器已经枚举超过序列末尾，它也不能返回同一个实例，因为之后对已耗尽枚举器的所有调用都必须抛出异常。备注结束

## 15.14.6.2 GetEnumerator 方法

可枚举对象提供 IEnumerable 和 IEnumerable<T> 接口的 GetEnumerator 方法的实现。这两个 GetEnumerator 方法共享一个公共实现，该实现获取并返回一个可用的枚举器对象。枚举器对象使用初始化可枚举对象时保存的参数值和实例值进行初始化，但除此之外，枚举器对象按照 §15.14.5 中所述的方式运作。

## 15.15 异步函数

### 15.15.1 概述

带有 async 修饰符的方法（§15.6）或匿名函数（§12.19）称为异步函数。一般而言，术语 async 用于描述任何具有 async 修饰符的函数。

如果异步函数的形式参数列表指定任何 in、out 或 ref 参数，或任何 ref struct 类型的参数，则属于编译时错误。

异步方法的返回类型应为 void 或任务类型。对于有返回值的异步方法，任务类型应为泛型。对于不返回值的异步方法，任务类型不应为泛型。在本规范中，此类类型分别称为 «TaskType<T>» 和 «TaskType»。标准库类型 System.Threading.Tasks.Task 以及由 System.Threading.Tasks.Task<TResult> 构造的类型都是任务类型；通过特性 System.Runtime.CompilerServices.AsyncMethodBuilderAttribute 与任务生成器类型关联的类、结构或接口类型也是任务类型。在本规范中，此类类型分别称为 «TaskBuilderType<T>» 和 «TaskBuilderType»。任务类型最多只能有一个类型参数，并且不能嵌套在泛型类型中。

返回任务类型的异步方法称为任务返回方法。

任务类型的确切定义可能各不相同，但从语言的角度看，任务类型处于 incomplete、succeeded 或 faulted 状态之一。处于 faulted 状态的任务记录相关异常。处于 succeeded 状态的 «TaskType<T>» 记录类型 T 的结果。任务类型是可等待的，因此任务可以是 await 表达式（§12.9.8）的操作数。

示例：任务类型 MyTask<T> 与任务生成器类型 MyTaskMethodBuilder<T> 以及等待器类型 Awaiter<T> 关联：

```csharp
using System.Runtime.CompilerServices;
[AsyncMethodBuilder(typeof(MyTaskMethodBuilder<>))]
class MyTask<T>
{
    public Awaiter<T> GetAwaiter() { ... }
}
class Awaiter<T> : INotifyCompletion
{
    public void OnCompleted(Action completion) { ... }
    public bool IsCompleted { get; }
    public T GetResult() { ... }
}
```

*示例结束*

任务生成器类型是与特定任务类型相对应的类或结构类型（§15.15.2）。

异步函数能够通过其主体中的 await 表达式（§12.9.8）暂停求值。之后可以通过恢复委托在暂停的 await 表达式处恢复求值。恢复委托的类型为 System.Action，当它被调用时，异步函数调用的求值将从其离开处的 await 表达式继续。如果函数调用从未被暂停，则异步函数调用的当前调用者是原始调用者；否则，是恢复委托的最近调用者。

### 15.15.2 任务类型生成器模式

任务生成器类型最多只能有一个类型参数，并且不能嵌套在泛型类型中。任务生成器类型应具有以下可访问成员（对于非泛型任务生成器类型，SetResult 没有参数）：

```csharp
class «TaskBuilderType»<T>
{
    public static «TaskBuilderType»<T> Create();
    public void Start<TStateMachine>(ref TStateMachine stateMachine)
        where TStateMachine : IAsyncStateMachine;
    public void SetStateMachine(IAsyncStateMachine stateMachine);
    public void SetException(Exception exception);
    public void SetResult(T result);
    public void AwaitOnCompleted<TAwaiter, TStateMachine>(
        ref TAwaiter awaiter, ref TStateMachine stateMachine)
        where TAwaiter : INotifyCompletion
        where TStateMachine : IAsyncStateMachine;
    public void AwaitUnsafeOnCompleted<TAwaiter, TStateMachine>(
        ref TAwaiter awaiter, ref TStateMachine stateMachine)
        where TAwaiter : ICriticalNotifyCompletion
        where TStateMachine : IAsyncStateMachine;
    public «TaskType»<T> Task { get; }
}
```

编译器生成使用 «TaskBuilderType» 的代码，以实现暂停和恢复异步函数求值的语义。编译器按如下方式使用 «TaskBuilderType»：

- 调用 «TaskBuilderType».Create() 创建 «TaskBuilderType» 的实例，在此列表中称为 builder。
- 调用 builder.Start(ref stateMachine) 将 builder 与编译器生成的状态机实例 stateMachine 关联。
  - builder 必须在 Start() 中或 Start() 返回后调用 stateMachine.MoveNext() 以推进状态机。
- Start() 返回后，异步方法调用 builder.Task 以获取要从异步方法返回的任务。
- 每次调用 stateMachine.MoveNext() 都会推进状态机。
- 如果状态机成功完成，则调用 builder.SetResult()，并传入方法返回值（如果有）。
- 否则，如果状态机中抛出异常 e，则调用 builder.SetException(e)。
- 如果状态机到达 await 表达式，则调用 expr.GetAwaiter()。
- 如果等待器实现 ICriticalNotifyCompletion 且 IsCompleted 为 false，则状态机调用 builder.AwaitUnsafeOnCompleted(ref awaiter, ref stateMachine)。
  - AwaitUnsafeOnCompleted() 应使用一个 Action 调用 awaiter.UnsafeOnCompleted(action)，该 Action 在等待器完成时调用 stateMachine.MoveNext()。
- 否则，状态机调用 builder.AwaitOnCompleted(ref awaiter, ref stateMachine)。
  - AwaitOnCompleted() 应使用一个 Action 调用 awaiter.OnCompleted(action)，该 Action 在等待器完成时调用 stateMachine.MoveNext()。
- 编译器生成的 IAsyncStateMachine 实现可以调用 SetStateMachine(IAsyncStateMachine)，以标识与某个状态机实例关联的 builder 实例，尤其适用于状态机实现为值类型的情况。
  - 如果 builder 调用 stateMachine.SetStateMachine(stateMachine)，则 stateMachine 将在与 stateMachine 关联的 builder 实例上调用 builder.SetStateMachine(stateMachine)。

### 15.15.3 返回任务的异步函数的求值

调用返回任务的异步函数会生成所返回任务类型的实例。这称为该异步函数的返回任务。该任务最初处于 incomplete 状态。

随后对异步函数体求值，直到它被暂停（通过到达 await 表达式）或终止；此时控制权连同返回任务一起返回给调用者。

当异步函数体终止时，返回任务会脱离 incomplete 状态：

- 如果函数体因到达 return 语句或函数体末尾而终止，则任何结果值都会记录在返回任务中，该任务会被置于 succeeded 状态。
- 如果函数体因未捕获的异常（§13.10.6）而终止，则该异常会记录在返回任务中，该任务会被置于 faulted 状态。

### 15.15.4 返回 void 的异步函数的求值

如果异步函数的返回类型为 void，则求值方式在以下方面与上述不同：由于不返回任务，函数改为向当前线程的同步上下文传达完成和异常。同步上下文的确切定义取决于实现，但它表示当前线程正在“何处”运行。当返回 void 的异步函数开始求值、成功完成或导致未捕获异常被抛出时，会通知同步上下文。




这允许上下文跟踪在其下运行着多少个返回 void 的异步函数，并决定如何传播从这些函数中产生的异常。

# 16. 结构体

### 16.1 概述

结构体与类相似，因为它们表示可以包含数据成员和函数成员的数据结构。然而，与类不同，结构体是值类型，不需要堆分配。结构体类型的变量直接包含结构体的数据，而类类型的变量包含对数据的引用，后者称为对象。

> 注意：结构体对于具有值语义的小型数据结构特别有用。复数、坐标系中的点或字典中的键值对都是结构体的良好示例。这些数据结构的要点在于它们的数据成员很少，不需要使用继承或引用语义，而是可以方便地使用值语义实现，其中赋值复制值而不是引用。结束注释

如 §8.3.5 所述，C# 提供的简单类型（例如 int、double 和 bool）实际上都是结构体类型。

### 16.2 结构体声明

### 16.2.1 概述

struct_declaration 是一种 type_declaration（§14.7），它声明一个新的结构体：

```
struct_declaration
: attributes? struct_modifier* 'ref'? 'partial'? 'struct'
identifier type_parameter_list? struct_interfaces?
type_parameter_constraints_clause* struct_body ';'?
```

struct_declaration 由可选的一组特性（§22）组成，随后是可选的一组 struct_modifiers（§16.2.2），随后是可选的 ref 修饰符（§16.2.3），随后是可选的 partial 修饰符（§15.2.7），随后是关键字 struct 和命名该结构体的标识符，随后是可选的 type_parameter_list 规范（§15.2.3），随后是可选的 struct_interfaces 规范（§16.2.5），随后是可选的 type_parameter_constraints_clauses 规范（§15.2.5），随后是 struct_body（§16.2.6），可选后跟分号。

结构体声明不得提供 type_parameter_constraints_clauses，除非它还提供 type_parameter_list。

提供 type_parameter_list 的结构体声明是泛型结构体声明。此外，在泛型类声明或泛型结构体声明中嵌套的任何结构体本身也是泛型结构体声明，因为创建构造类型（§8.4）时必须提供包含类型的类型实参。

包含 ref 关键字的结构体声明不得具有 struct_interfaces 部分。

### 16.2.2 结构体修饰符

struct_declaration 可以选择性地包含一系列 struct_modifiers：

```
struct_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'readonly'
  | unsafe_modifier  // unsafe code support
  ;
```

unsafe_modifier（§23.2）仅在 unsafe 代码（§23）中可用。

同一修饰符在结构体声明中多次出现属于编译时错误。

除 readonly 外，结构体声明的修饰符与类声明的修饰符（§15.2.2）含义相同。

readonly 修饰符指示 struct_declaration 声明一个其实例不可变的类型。

readonly 结构体具有以下约束：
- 它的每个实例字段也都应声明为 readonly。
- 它的任何实例属性都不得具有 set_accessor_declaration（§15.7.3）。
- 它不得声明任何类似字段的事件（§15.8.2）。

当 readonly 结构体的实例传递给方法时，其 this 被视为 in 实参/形参，这不允许对任何实例字段进行写访问（构造函数除外）。

### 16.2.3 ref 修饰符

ref 修饰符指示 struct_declaration 声明一个其实例分配在执行栈上的类型。这些类型称为 ref 结构体类型。ref 修饰符声明实例可以包含类似 ref 的字段，并且不得复制出其安全上下文（§16.4.12）。确定 ref 结构体安全上下文的规则在 §16.4.12 中描述。

如果 ref 结构体类型用于以下任何上下文，则属于编译时错误：
- 作为数组的元素类型。
- 作为不具有 ref 修饰符的类或结构体的字段的声明类型。
- 被装箱到 System.ValueType 或 System.Object。
- 作为类型实参。
- 作为元组元素的类型。
- 异步方法。
- 迭代器。
- 不存在从 ref 结构体类型到 object 类型或 System.ValueType 类型的转换。
- 不得将 ref 结构体类型声明为实现任何接口。
- 在 object 或 System.ValueType 中声明但未在 ref 结构体类型中重写的实例方法，不得使用该 ref 结构体类型的接收者来调用。
- ref 结构体类型的实例方法不得被方法组转换为委托类型所捕获。
- ref 结构体不得由 lambda 表达式或局部函数捕获。

> 注意：ref 结构体不得声明异步实例方法，也不得在实例方法内使用 yield return 或 yield break 语句，因为隐式 this 参数不能在这些上下文中使用。结束注释

这些约束确保 ref 结构体类型的变量不会引用不再有效的栈内存，也不会引用不再有效的变量。

### 16.2.4 partial 修饰符

partial 修饰符指示此 struct_declaration 是分部类型声明。在封闭命名空间或类型声明中，具有相同名称的多个分部结构体声明按照 §15.2.7 中指定的规则合并形成一个结构体声明。

### 16.2.5 结构体接口

结构体声明可以包含 struct_interfaces 规范，在这种情况下，称该结构体直接实现给定的接口类型。对于构造的结构体类型（包括在泛型类型声明（§15.3.9.7）中声明的嵌套类型），每个实现的接口类型都是通过以下方式获得的：对于给定接口中的每个 type_parameter，替换为构造类型对应的 type_argument。

```
struct_interfaces
  : ':' interface_type_list
  ;
```

关于分部结构体声明（§15.2.7）多个部分上的接口处理，将在 §15.2.4.3 中进一步讨论。

接口实现将在 §18.6 中进一步讨论。

### 16.2.6 结构体主体

结构体的 struct_body 定义该结构体的成员。

```
struct_body
  : '{' struct_member_declaration* '}'
  ;
```

### 16.3 结构体成员

结构体的成员由 struct_member_declarations 引入的成员以及从 System.ValueType 类型继承的成员组成。

```
struct_member_declaration
  : constant_declaration
  | field_declaration
  | method_declaration
  | property_declaration
  | event_declaration
  | indexer_declaration
  | operator_declaration
  | constructor_declaration
```

```
| static_constructor_declaration
| type_declaration
| fixed_size_buffer_declaration  // unsafe code support
;
```

fixed_size_buffer_declaration（§23.8.2）仅在 unsafe 代码（§23）中可用。

> 注意：除 finalizer_declaration 之外，所有种类的 class_member_declarations 也都是 struct_member_declarations。结束注释

除 §16.4 中指出的差异外，§15.3 至 §15.12 中提供的类成员描述也适用于结构体成员。

### 16.4 类与结构体的差异

### 16.4.1 概述

结构体在几个重要方面与类不同：
- 结构体是值类型（§16.4.2）。
- 所有结构体类型都隐式继承自 System.ValueType 类（§16.4.3）。
- 对结构体类型的变量进行赋值会创建所赋值的副本（§16.4.4）。
- 结构体的默认值是将所有字段设置为其默认值后产生的值（§16.4.5）。
- 装箱和拆箱操作用于在结构体类型与某些引用类型之间进行转换（§16.4.6）。
- this 的含义在结构体成员内有所不同（§16.4.7）。
- 结构体的实例字段声明不允许包含变量初始值设定项（§16.4.8）。
- 不允许结构体声明无参数实例构造函数（§16.4.9）。
- 不允许结构体声明终结器。

### 16.4.2 值语义

结构体是值类型（§8.3），称为具有值语义。另一方面，类是引用类型（§8.2），称为具有引用语义。

结构体类型的变量直接包含结构体的数据，而类类型的变量包含对包含该数据的对象的引用。当结构体 B 包含类型为 A 的实例字段且 A 是结构体类型时，A 依赖 B 或依赖由 B 构造的类型属于编译时错误。如果结构体 X 包含类型为 Y 的实例字段，则结构体 X 直接依赖结构体 Y。根据此定义，一个结构体所依赖的完整结构体集合是“直接依赖”关系的传递闭包。

示例：

```
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```

是错误，因为 Node 包含一个自身类型的实例字段。另一个示例

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

是错误，因为类型 A、B 和 C 相互依赖。

示例结束

对于类，两个变量可以引用同一对象，因此对一个变量的操作可能影响另一个变量所引用的对象。对于结构，每个变量都有自己的一份数据副本（in、out 和 ref 参数变量除外），对一个变量的操作不可能影响另一个变量。此外，除非显式可为空（§8.3.12），结构类型的值不可能为 null。

> 注意：如果结构包含引用类型的字段，那么被引用对象的内容可以通过其他操作更改。但是，字段本身的值，即它引用哪个对象，不能通过更改另一个结构值来改变。注意结束

示例：给定以下代码

```
struct Point
{
    public int x, y;
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class A
{
    static void Main()
    {
        Point a = new Point(10, 10);
        Point b = a;
        a.x = 100;
        Console.WriteLine(b.x);
    }
}
```

输出是 10。将 a 赋值给 b 会创建值的副本，因此 b 不受对 a.x 赋值的影响。如果 Point 改为声明为类，则输出将是 100，因为 a 和 b 将引用同一个对象。

示例结束

## 16.4.3 继承

所有结构类型都隐式继承自类 System.ValueType，而后者又继承自类 object。结构声明可以指定所实现接口的列表，但结构声明不可能指定基类。

结构类型永远不会是抽象的，并且始终是隐式密封的。因此，结构声明中不允许使用 abstract 和 sealed 修饰符。

由于结构不支持继承，结构成员的声明可访问性不能是 `protected`、`private protected` 或 `protected internal`。

结构中的函数成员不能是 abstract 或 virtual，并且仅允许使用 `override` 修饰符来重写从 System.ValueType 继承的方法。

## 16.4.4 赋值

对结构类型变量的赋值会创建所赋值的一个副本。这与对类类型变量的赋值不同，后者复制引用，但不复制该引用所标识的对象。

与赋值类似，当结构作为值参数传递或作为函数成员的结果返回时，会创建该结构的一个副本。可以使用 `in`、`out` 或 `ref` 参数，按引用将结构传递给函数成员。

当结构的属性或索引器是赋值目标时，与该属性或索引器访问关联的实例表达式应归类为变量。如果该实例表达式归类为值，则会发生编译时错误。§12.21.2 对此进行了更详细的描述。

## 16.4.5 默认值

如 §9.3 所述，若干种类的变量在创建时会自动初始化为其默认值。对于类类型和其他引用类型的变量，此默认值是 `null`。但是，由于结构是不能为 `null` 的值类型，结构的默认值是将所有值类型字段设置为其默认值、并将所有引用类型字段设置为 `null` 后产生的值。

> *示例：* 引用上面声明的 `Point` 结构，示例
> 
> ```csharp
> Point[] a = new Point[100];
> ```
> 
> 将数组中的每个 `Point` 初始化为将 x 和 y 字段设置为零后产生的值。
> 
> *示例结束*

结构的默认值对应于该结构的默认构造函数（§8.3.3）返回的值。与类不同，不允许结构声明无参数实例构造函数。相反，每个结构都隐式具有一个无参数实例构造函数，它始终返回将所有字段设置为其默认值后得到的值。

*注意：* 结构的设计应考虑将默认初始化状态视为有效状态。在示例中

```csharp
struct KeyValuePair
{
    string key;
    string value;

    public KeyValuePair(string key, string value)
    {
        if (key == null || value == null)
        {
            throw new ArgumentException();
        }

        this.key = key;
        this.value = value;
    }
}
```

用户定义的实例构造函数仅在显式调用它的地方防止 null 值。在 KeyValuePair 变量接受默认值初始化的情况下，key 和 value 字段将为 null，结构应准备好处理此状态。注意结束

## 16.4.6 装箱和拆箱

类类型的值可以转换为 object 类型或该类实现的接口类型，只需在编译时将引用视为另一种类型。同样，object 类型的值或接口类型的值可以转换回类类型，而无需更改引用（当然，在这种情况下需要运行时类型检查）。

由于结构不是引用类型，这些操作对结构类型以不同方式实现。当结构类型的值转换为某些引用类型（如 §10.2.9 所定义）时，会发生装箱操作。同样，当某些引用类型的值（如 §10.3.7 所定义）转换回结构类型时，会发生拆箱操作。与对类类型的相同操作的一个关键区别是，装箱和拆箱会将结构值复制到装箱实例中或从装箱实例中复制出来。

> 注意：因此，在装箱或拆箱操作之后，对未装箱结构所做的更改不会反映在装箱结构中。注意结束

有关装箱和拆箱的更多详细信息，请参阅 §10.2.9 和 §10.3.7。

## 16.4.7 this 的含义

结构中的 this 含义不同于类中的 this 含义，如 §12.8.13 所述。当结构类型重写从 System.ValueType 继承的虚方法（如 Equals、GetHashCode 或 ToString）时，通过该结构类型的实例调用该虚方法不会导致装箱发生。即使该结构用作类型参数，并且通过该类型参数类型的实例进行调用，也是如此。

示例：

```csharp
struct Counter
{
    int value;
    public override string ToString()
    {
        value++;
        return value.ToString();
    }
}

class Program
{
    static void Test<T>() where T : new()
    {
        T x = new T();
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
    }

    static void Main() => Test<Counter>();
}
```

程序的输出是：

1
2
3

尽管让 ToString 具有副作用是不好的风格，但该示例演示了对 x.ToString() 的三次调用没有发生装箱。

示例结束

类似地，当成员在值类型中实现时，访问受约束类型参数上的成员绝不会隐式发生装箱。例如，假设接口 ICounter 包含一个方法 Increment，可用于修改值。如果将 ICounter 用作约束，则调用 Increment 方法的实现时，会传入对调用 Increment 的变量的引用，而绝不是装箱副本。

示例：

```csharp
interface ICounter
{
    void Increment();
}

struct Counter : ICounter
{
    int value;

    public override string ToString() => value.ToString();

    void ICounter.Increment() => value++;
}

class Program
{
    static void Test<T>() where T : ICounter, new()
    {
        T x = new T();
        Console.WriteLine(x);
        x.Increment();          // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment(); // Modify boxed copy of x
        Console.WriteLine(x);
    }

    static void Main() => Test<Counter>();
}
```

第一次调用 Increment 会修改变量 x 中的值。这与第二次调用 Increment 不等价，后者修改 x 的装箱副本中的值。因此，程序的输出是：

0
1
1




## 16.4.8 字段初始值设定项

如 §16.4.5 所述，结构体的默认值由以下操作所得的值构成：将所有值类型字段设置为其默认值，并将所有引用类型字段设置为 null。因此，结构体不允许实例字段声明包含变量初始值设定项。此限制仅适用于实例字段。结构体的静态字段允许包含变量初始值设定项。

示例：以下代码

```
struct Point
{
    public int x = 1; // Error, initializer not permitted
    public int y = 1; // Error, initializer not permitted
}
```

会出错，因为实例字段声明包含变量初始值设定项。

示例结束

## 16.4.9 构造函数

与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，该构造函数始终返回以下操作所得的值：将所有值类型字段设置为其默认值，并将所有引用类型字段设置为 null（§8.3.3）。结构体可以声明带参数的实例构造函数。

示例：给定以下代码

```
struct Point
{
    int x, y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class A
{
    static void Main()
    {
        Point p1 = new Point();
        Point p2 = new Point(0, 0);
    }
}
```

这两个语句都会创建一个 Point，其 x 和 y 初始化为零。

示例结束

结构体实例构造函数不允许包含形式为 base(argument_list) 的构造函数初始值设定项，其中 argument_list 是可选的。

结构体实例构造函数的 this 参数对应于该结构体类型的 out 参数。因此，在构造函数返回的每个位置，this 都必须已明确赋值（§9.4）。同样，在明确赋值之前，不能在构造函数体中读取它（即使是隐式读取）。

如果结构体实例构造函数指定了构造函数初始值设定项，则该初始值设定项被视为在构造函数体之前发生的对 this 的明确赋值。因此，构造函数体本身没有初始化要求。

示例：考虑下面的实例构造函数实现：

```
```csharp
struct Point
{
    int x, y;

    public int X
    {
        set { x = value; }
    }

    public int Y
    {
        set { y = value; }
    }

    public Point(int x, int y)
    {
        X = x; // error, this is not yet definitely assigned
        Y = y; // error, this is not yet definitely assigned
    }
}
```
```

在正在构造的结构体的所有字段都已明确赋值之前，不能调用任何实例函数成员（包括属性 x 和 y 的 set 访问器）。但请注意，如果 Point 是类而不是结构体，则该实例构造函数实现是允许的。对此有一个例外，涉及自动实现的属性（§15.7.4）。明确赋值规则（§12.21.2）特别豁免了在该结构体类型的实例构造函数内对该结构体类型的自动属性进行赋值：此类赋值被视为对该自动属性的隐藏支持字段的明确赋值。因此，以下代码是允许的：

```
```csharp
struct Point
{
    public int X { get; set; }
    public int Y { get; set; }

    public Point(int x, int y)
    {
        X = x; // allowed, definitely assigns backing field
        Y = y; // allowed, definitely assigns backing field
    }
}
```
```

示例结束

## 16.4.10 静态构造函数

结构体的静态构造函数遵循与类的大多数相同规则。结构体类型的静态构造函数的执行由应用程序域内发生的以下第一个事件触发：

- 引用了该结构体类型的静态成员。
- 调用了该结构体类型的显式声明的构造函数。

注意：创建结构体类型的默认值（§16.4.5）不会触发静态构造函数。（例如，数组中元素的初始值。）注意结束

## 16.4.11 自动实现的属性

自动实现的属性（§15.7.4）使用隐藏的支持字段，这些字段只能由属性访问器访问。

注意：这种访问限制意味着，包含自动实现的属性的结构体中的构造函数通常需要显式构造函数初始值设定项，而在其他情况下则不需要，以满足在调用任何函数成员或构造函数返回之前所有字段都已明确赋值的要求。注意结束

## 16.4.12 安全上下文约束

### 16.4.12.1 概述

在编译时，每个表达式都与一个上下文关联，在该上下文中可以安全地访问该实例及其所有字段，即其安全上下文。安全上下文是一个包围表达式的上下文，值逃逸到该上下文是安全的。

任何编译时类型不是 ref struct 的表达式，其安全上下文为调用方上下文。

对于任何类型，默认表达式的安全上下文为调用方上下文。

对于任何编译时类型为 ref struct 的非默认表达式，其安全上下文由以下各节定义。

- 对于 return 语句 return e1，e1 的安全上下文必须是调用方上下文。
- 对于赋值 e1 = e2，e2 的安全上下文必须至少与 e1 的安全上下文一样宽。

### 16.4.12.2 参数安全上下文

ref struct 类型的形参（包括实例方法的 this 参数）的安全上下文为调用方上下文。

### 16.4.12.3 局部变量安全上下文

ref struct 类型的局部变量的安全上下文如下：

- 如果变量是 foreach 循环的迭代变量，则该变量的安全上下文与 foreach 循环的表达式的安全上下文相同。
- 否则，如果变量的声明具有初始值设定项，则该变量的安全上下文与该初始值设定项的安全上下文相同。
- 否则，该变量在声明点未初始化，其安全上下文为调用方上下文。

### 16.4.12.4 字段安全上下文

对字段 e . F 的引用（其中 F 的类型为 ref struct 类型）具有与 e 的安全上下文相同的安全上下文。

### 16.4.12.5 运算符

用户定义运算符的应用被视为方法调用（§16.4.12.6）。

对于产生值的运算符，例如 e1 + e2 或 c ? e1 : e2，结果的安全上下文是该运算符各操作数的安全上下文中最窄的上下文。因此，对于产生值的一元运算符，例如 +e，结果的安全上下文是操作数的安全上下文。

注意：条件运算符的第一个操作数是 bool，因此其安全上下文为调用方上下文。由此可知，结果的安全上下文是第二个和第三个操作数的安全上下文中最窄的。注意结束

### 16.4.12.6 方法和属性调用

由方法调用 e1.M(e2, ...) 或属性调用 e . P 产生的值，其安全上下文为以下上下文中最窄的：

- 调用方上下文。
- 所有参数表达式（包括接收方）的安全上下文。

按照上述规则，属性调用（get 或 set）被视为对基础方法的调用。

### 16.4.12.7 stackalloc

stackalloc 表达式的结果的安全上下文为函数成员上下文。

### 16.4.12.8 构造函数调用

调用构造函数的 new 表达式遵循与方法调用相同的规则，该方法调用被视为返回正在构造的类型。

此外，如果存在任何初始值设定项，则安全上下文是所有参数以及所有对象初始值设定项表达式的操作数的安全上下文（递归地）中最窄的。

注意：这些规则依赖于 Span<T> 不具有以下形式的构造函数：
public Span<T>(ref T p)
这样的构造函数会使作为字段使用的 Span<T> 实例与 ref 字段无法区分。本文档描述的安全规则依赖于 ref 字段在 C# 或 .NET 中不是有效构造。注意结束




# 17. 数组

### 17.1 通用

数组是一种数据结构，其中包含若干通过计算得到的索引进行访问的变量。包含在数组中的变量，也称为数组的元素，全部为同一类型，该类型称为数组的元素类型。

数组具有一个秩，决定了与每个数组元素关联的索引数量。数组的秩也称为数组的维度。秩为一的数组称为单维数组。秩大于一的数组称为多维数组。特定大小的多维数组通常被称为二维数组、三维数组，等等。数组的每个维度都有一个相关联的长度，该长度为大于或等于零的整数。维度的长度不是数组类型的一部分，而是当数组类型的实例在运行时创建时确定的。维度的长度决定了该维度的索引有效范围：对于长度为 N 的维度，索引的范围可以从 0 到 N - 1 包含。数组中的元素总数是数组中各维度长度的乘积。如果数组的一个或多个维度的长度为零，则该数组称为空数组。

数组的元素类型本身也可以是数组类型 (§17.2.1)。这种数组的数组与多维数组不同，可用于表示“锯齿数组”。

示例：

```csharp
int[][] pascals =
{
    new int[] {1},
    new int[] {1, 1},
    new int[] {1, 2, 1},
    new int[] {1, 3, 3, 1}
};
```

end example

每个数组类型都是引用类型 (§8.2)。数组的元素类型可以是任何类型，包括值类型和数组类型。

### 17.2 数组类型

#### 17.2.1 通用

数组类型的语法生成式在 §8.2.1 中给出。

数组类型写成 `non_array_type` 后跟一个或多个 `rank_specifier`。

`non_array_type` 是任何本身不是 `array_type` 的类型。

数组类型的秩由 `array_type` 中最左边的 `rank_specifier` 给出：`rank_specifier` 表示该数组的秩为一加上 `rank_specifier` 中 `,` 标记的数量。

数组类型的元素类型是通过删除最左边的 `rank_specifier` 得到的类型：

- 形式为 `T[R]` 的数组类型是秩为 R 且元素类型为非数组类型 T 的数组。
- 形式为 `T[R][R1]...[Rx]` 的数组类型是秩为 R 且元素类型为 `T[R1]...[Rx]` 的数组。

实际上，`rank_specifier` 是从左到右读取，位于最终的非数组元素类型之前。

示例：类型 `T[][,,][,]` 中的类型是 int 的二维数组的三维数组的单维数组。 end example

在运行时，数组类型的值可以为 null 或对该数组类型实例的引用。

注意：根据 §17.6 的规则，该值也可能是对协变数组类型的引用。 end note

#### 17.2.2 System.Array 类型

类型 System.Array 是所有数组类型的抽象基类型。从任何数组类型到 System.Array 以及 System.Array 实现的任何接口类型都存在隐式引用转换 (§10.2.8)。从 System.Array 以及 System.Array 实现的任何接口类型到任何数组类型都存在显式引用转换 (§10.3.5)。System.Array 本身不是 `array_type`。相反，它是一个 `class_type`，所有 `array_type` 均派生自它。

在运行时，System.Array 类型的值可以为 null 或对任何数组类型实例的引用。

#### 17.2.3 数组与通用集合接口

单维数组 `T[]` 实现接口 `System.Collections.Generic.IList<T>`（简称为 `IList<T>`）及其基接口。因此，从 `T[]` 到 `IList<T>` 及其基接口存在隐式转换。此外，如果从 S 到 T 存在隐式引用转换，则 `S[]` 实现 `IList<T>`，并且从 `S[]` 到 `IList<T>` 及其基接口存在隐式引用转换 (§10.2.8)。如果从 S 到 T 存在显式引用转换，则从 `S[]` 到 `IList<T>` 及其基接口存在显式引用转换 (§10.3.5)。

同样，单维数组 `T[]` 也实现接口 `System.Collections.Generic.IReadOnlyList<T>`（简称为 `IReadOnlyList<T>`）及其基接口。因此，从 `T[]` 到 `IReadOnlyList<T>` 及其基接口存在隐式转换。此外，如果从 S 到 T 存在隐式引用转换，则 `S[]` 实现 `IReadOnlyList<T>`，并且从 `S[]` 到 `IReadOnlyList<T>` 及其基接口存在隐式引用转换 (§10.2.8)。如果从 S 到 T 存在显式引用转换，则从 `S[]` 到 `IReadOnlyList<T>` 及其基接口存在显式引用转换 (§10.3.5)。

*示例：* 例如：

```csharp
class Test
{
    static void Main()
    {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;

        IList<string> lst1 = sa;  // Ok
        IList<string> lst2 = oa1; // Error, cast needed
        IList<object> lst3 = sa;  // Ok
        IList<object> lst4 = oa1; // Ok

        IList<string> lst5 = (IList<string>)oa1; // Exception
        IList<string> lst6 = (IList<string>)oa2; // Ok

        IReadOnlyList<string> lst7 = sa; // Ok
        IReadOnlyList<string> lst8 = oa1; // Error, cast needed
        IReadOnlyList<object> lst9 = sa; // Ok
        IReadOnlyList<object> lst10 = oa1; // Ok
        IReadOnlyList<string> lst11 = (IReadOnlyList<string>)oa1; // Exception
        IReadOnlyList<string> lst12 = (IReadOnlyList<string>)oa2; // Ok
    }
}
```

赋值 `lst2 = oa1` 会生成编译时错误，因为从 `object[]` 到 `IList<string>` 的转换是显式转换，而不是隐式转换。强制转换 `(IList<string>)oa1` 会在运行时抛出异常，因为 `oa1` 引用的是 `object[]` 而不是 `string[]`。然而强制转换 `(IList<string>)oa2` 不会抛出异常，因为 `oa2` 引用的是 `string[]`。

*示例结束*

每当从 `S[]` 到 `IList<T>` 存在隐式或显式引用转换时，从 `IList<T>` 及其基接口到 `S[]` 也存在显式引用转换 (§10.3.5)。

当数组类型 `S[]` 实现 `IList<T>` 时，已实现接口的某些成员可能会抛出异常。接口实现的精确行为超出了本规范的范围。

### 17.3 数组创建

数组实例由 `array_creation_expressions` (§12.8.16.5) 创建，或由包含 `array_initializer` (§17.7) 的字段或局部变量声明创建。

数组实例也可以在评估涉及参数数组的参数列表时隐式创建 (§15.6.2.6)。

当数组实例创建时，每个维度的秩和长度被确定，并且在实例整个生命周期内保持不变。换句话说，不可能更改现有数组实例的秩，也不可能调整其维度的大小。

数组实例始终为数组类型。System.Array 类型是抽象类型，不能实例化。

由 `array_creation_expressions` 创建的数组的元素始终初始化为其默认值 (§9.3)。

### 17.4 数组元素访问

数组元素使用形式为 `A[I1, I2, ..., Ix]` 的 `element_access` 表达式 (§12.8.11.2) 进行访问，其中 A 是数组类型的表达式，每个 `I_i` 是类型为 int、uint、long、ulong 的表达式，或可以隐式转换为其中一种或多种类型。数组元素访问的结果是一个变量，即由索引选定的数组元素。

数组的元素可以使用 foreach 语句 (§13.9.5) 进行枚举。

### 17.5 数组成员

每个数组类型都继承 System.Array 类型声明的成员。

### 17.6 数组协变

对于任意两个 `reference_type` A 和 B，如果从 A 到 B 存在隐式引用转换 (§10.2.8) 或显式引用转换 (§10.3.5)，则从数组类型 `A[R]` 到数组类型 `B[R]` 也存在相同的引用转换，其中 R 是任意给定的 `rank_specifier`（但对两个数组类型相同）。这种关系称为数组协变。

数组协变特别意味着，数组类型 `A[R]` 的值实际上可能是数组类型 `B[R]` 的实例的引用，前提是从 B 到 A 存在隐式引用转换。

由于数组协变，对引用类型数组元素的赋值包括运行时检查，以确保分配给数组元素的值实际上是允许的类型 (§12.21.2)。

*示例：*

```csharp
class Test
{
    static void Fill(object[] array, int index, int count, object value)
    {
        for (int i = index; i < index + count; i++)
        {
            array[i] = value;
        }
    }

    static void Main()
    {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```

Fill 方法中对 `array[i]` 的赋值隐式包含运行时检查，以确保 value 要么为空引用，要么是对与数组实际元素类型兼容的对象类型的引用。在 Main 中，Fill 的前两次调用成功，但第三次调用在执行对 `array[i]` 的第一次赋值时导致抛出 `System.ArrayTypeMismatchException`。该异常发生是因为装箱的 int 不能存储在字符串数组中。

*示例结束*

数组协变特别不扩展到 `value_type` 的数组。例如，不存在允许将 `int[]` 视为 `object[]` 的转换。

### 17.7 数组初始化器

数组初始化器可以在字段声明 (§15.5)、局部变量声明 (§13.6.2) 和数组创建表达式 (§12.8.16.5) 中指定：

```
array_initializer
: '{' variable_initializer_list? '}'
| '{' variable_initializer_list ',' '}'
;

variable_initializer_list
: variable_initializer (',' variable_initializer)*
;

variable_initializer
: expression
| array_initializer
;
```

数组初始化器由一系列变量初始化器组成，这些初始化器用“{”和“}”标记括起来，并用“,”标记分隔。每个变量初始化器是一个表达式，或者在多维数组的情况下，是一个嵌套的数组初始化器。

使用数组初始化器的上下文决定了正在初始化的数组的类型。在数组创建表达式中，数组类型紧跟在初始化器之前，或者从数组初始化器中的表达式推断出来。在字段或变量声明中，数组类型是正在声明的字段或变量的类型。当数组初始化器在字段或变量声明中使用时，

```
int[] a = {0, 2, 4, 6, 8};
```

它只是等价数组创建表达式的简写：

```
int[] a = new int[] {0, 2, 4, 6, 8};
```

对于单维数组，数组初始化器应由一系列表达式组成，每个表达式都可隐式转换为数组的元素类型（§10.2）。这些表达式按递增顺序初始化数组元素，从索引零处的元素开始。数组初始化器中表达式的数量决定了正在创建的数组实例的长度。

示例：上面的数组初始化器创建一个长度为 5 的 int[] 实例，然后用以下值初始化该实例：

```
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

对于多维数组，数组初始化器应具有与数组中维度一样多的嵌套级别。最外层的嵌套级别对应于最左侧的维度，最内层的嵌套级别对应于最右侧的维度。数组每个维度的长度由数组初始化器中相应嵌套级别处的元素数量决定。对于每个嵌套的数组初始化器，其元素数量应与同一级别的其他数组初始化器相同。

示例：示例：

```
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```

创建一个二维数组，左侧维度的长度为五，右侧维度的长度为二：

```
int[,] b = new int[5, 2];
```

然后用以下值初始化数组实例：

```
b[0, 0] = 0; b[0, 1] = 1;
b[1, 0] = 2; b[1, 1] = 3;
b[2, 0] = 4; b[2, 1] = 5;
b[3, 0] = 6; b[3, 1] = 7;
b[4, 0] = 8; b[4, 1] = 9;
```

示例结束

如果除最右侧维度之外的维度长度为零，则假定后续维度也长度为零。

示例：

```
int[,] c = {};
```

创建一个二维数组，左侧维度和右侧维度的长度均为零：

```
int[,] c = new int[0, 0];
```

示例结束

当数组创建表达式同时包含显式维度长度和数组初始化器时，长度应为常量表达式，并且每个嵌套级别的元素数量应与相应的维度长度匹配。

示例：以下是一些示例：

```
int i = 3;
int[] x = new int[3] {0, 1, 2}; // OK
int[] y = new int[i] {0, 1, 2}; // Error, i not a constant
int[] z = new int[3] {0, 1, 2, 3}; // Error, length/initializer mismatch
```

这里，y 的初始化器导致编译时错误，因为维度长度表达式不是常量，而 z 的初始化器导致编译时错误，因为长度与初始化器中的元素数量不匹配。

示例结束

注意：C# 允许在 array_initializer 末尾使用尾随逗号。此语法提供了在添加或删除此类列表中的成员时的灵活性，并简化了此类列表的机器生成。注释结束

# 18. 接口

### 18.1 通用

接口定义了一个契约。实现接口的类或结构体必须遵守其契约。接口可以继承多个基接口，类或结构体可以实现多个接口。

接口可以包含方法、属性、事件和索引器。接口本身并不为其声明的成员提供实现。接口仅指定由实现接口的类或结构体提供的成员。

### 18.2 接口声明

#### 18.2.1 通用

interface_declaration 是 type_declaration (§14.7)，它声明了一个新的接口类型。

```
interface_declaration
: attributes? interface_modifier* 'partial'? 'interface'
identifier variant_type_parameter_list? interface_base?
type_parameter_constraints_clause* interface_body ';'?
;
```

interface_declaration 由一组可选的属性 (§22) 组成，其后跟一组可选的 interface_modifiers (§18.2.2)，其后跟可选的 partial 修饰符 (§15.2.7)，其后跟关键字 interface 和一个命名接口的标识符，其后跟可选的 variant_type_parameter_list 规范 (§18.2.3)，其后跟可选的 interface_base 规范 (§18.2.4)，其后跟可选的 type_parameter_constraints_clauses 规范 (§15.2.5)，其后跟 interface_body (§18.3)， optionally 后跟分号。

接口声明不得提供 type_parameter_constraints_clauses，除非它也提供了 type_parameter_list。

提供 type_parameter_list 的接口声明是泛型接口声明。此外，嵌套在泛型类声明或泛型结构体声明内部的任何接口本身都是泛型接口声明，因为为了创建构造类型 (§8.4)，必须为包含类型提供类型参数。

#### 18.2.2 接口修饰符

interface_declaration 可选择包含一系列接口修饰符：

```
interface_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| unsafe_modifier  // unsafe code support
;
```

unsafe_modifier (§23.2) 仅在不安全代码 (§23) 中可用。

在接口声明中同一个修饰符出现多次是编译时错误。

new 修饰符仅允许在类中定义的接口上。它指定接口隐藏了同名的继承成员，如 §15.3.5 中所述。

public、protected、internal 和 private 修饰符控制接口的可访问性。根据接口声明出现的上下文，其中只有一些修饰符可能被允许 (§7.5.2)。当部分类型声明 (§15.2.7) 包含可访问性规范（通过 public、protected、internal 和 private 修饰符）时，§15.2.2 中的规则适用。

#### 18.2.3 变体类型参数列表

##### 18.2.3.1 通用

变体类型参数列表只能出现在接口和委托类型上。与普通 type_parameter_lists 的区别在于每个类型参数上的可选 variance_annotation。

```
variant_type_parameter_list
  : '<' variant_type_parameters '>'
  ;

variant_type_parameters
  : attributes? variance_annotation? type_parameter
  | variant_type_parameters ',' attributes? variance_annotation?
    type_parameter
  ;

variance_annotation
  : 'in'
  | 'out'
  ;
```

如果方差注释为 out，则该类型参数称为协变的。如果方差注释为 in，则该类型参数称为逆变的。如果没有方差注释，则该类型参数称为不变的。

示例：如下所示：

```
interface C<out X, in Y, Z>
{
    X M(Y y);
    Z P { get; set; }
}
```

X 是协变的，Y 是逆变的，Z 是不变的。

示例结束

如果泛型接口被声明为多个部分 (§15.2.3)，每个部分声明都应为每个类型参数指定相同的方差。

##### 18.2.3.2 方差安全

类型参数列表中方差注释的出现限制了类型在类型声明中可以出现的位置。

如果满足以下任一条件，则类型 T 是输出不安全的：

- T 是一个逆变类型参数



The explicit base interfaces of an interface shall be at least as accessible as the interface itself (§7.5.5).

Note: For example, it is a compile-time error to specify a private or internal interface in the interface_base of a public interface. end note

It is a compile-time error for an interface to directly or indirectly inherit from itself.

The base interfaces of an interface are the explicit base interfaces and their base interfaces. In other words, the set of base interfaces is the complete transitive closure of the explicit base interfaces, their explicit base interfaces, and so on. An interface inherits all members of its base interfaces.

Example: In the following code

```
interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}

interface IListBox : IControl
{
    void SetItems(string[] items);
}

interface IComboBox: ITextBox, IListBox {}
```

the base interfaces of IComboBox are IControl, ITextBox, and IListBox. In other words, the IComboBox interface above inherits members SetText and SetItems as well as Paint.

end example

Members inherited from a constructed generic type are inherited after type substitution. That is, any constituent types in the member have the base interface declaration's type parameters replaced with the corresponding type arguments used in the interface_base specification.

Example: In the following code

```
interface IBase<T>
{
    T[] Combine(T a, T b);
}

interface IDerived : IBase<string[,]>
{
    // Inherited: string[,][,] Combine(string[,] a, string[,] b);
}
```

the interface IDerived inherits the Combine method after the type parameter T is replaced with string[,].

end example

A class or struct that implements an interface also implicitly implements all of the interface's base interfaces.

The handling of interfaces on multiple parts of a partial interface declaration (§15.2.7) is discussed further in §15.2.4.3.

Every base interface of an interface shall be output-safe (§18.2.3.2).

## 18.3 接口体

The interface_body of an interface defines the members of the interface.

```
interface_body
  : '{' interface_member_declaration* '}'
  ;
```

## 18.4 接口成员

### 18.4.1 通用

The members of an interface are the members inherited from the base interfaces and the members declared by the interface itself.

```
interface_member_declaration
  : interface_method_declaration
  | interface_property_declaration
  | interface_event_declaration
  | interface_indexer_declaration
  ;
```

An interface declaration declares zero or more members. The members of an interface shall be methods, properties, events, or indexers. An interface cannot contain constants, fields, operators, instance constructors, finalizers, or types, nor can an interface contain static members of any kind.

All interface members implicitly have public access. It is a compile-time error for interface member declarations to include any modifiers.

An interface_declaration creates a new declaration space (§7.3), and the type parameters and interface_member_declarations immediately contained by the interface_declaration introduce new members into this declaration space. The following rules apply to interface_member_declarations:

- The name of a type parameter in the type_parameter_list of an interface declaration shall differ from the names of all other type parameters in the same type_parameter_list and shall differ from the names of all members of the interface.
- The name of a method shall differ from the names of all properties and events declared in the same interface. In addition, the signature (§7.6) of a method shall differ from the signatures of all other methods declared in the same interface, and two methods declared in the same interface may not have signatures that differ solely by in, out, and ref.
- The name of a property or event shall differ from the names of all other members declared in the same interface.
- The signature of an indexer shall differ from the signatures of all other indexers declared in the same interface.

The inherited members of an interface are specifically not part of the declaration space of the interface. Thus, an interface is allowed to declare a member with the same name or signature as an inherited member. When this occurs, the derived interface member is said to hide the base interface member.

Hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning. To suppress the warning, the declaration of the derived interface member shall include a new modifier to indicate that the derived member is intended to hide the base member. This topic is discussed further in §7.7.2.3.

If a new modifier is included in a declaration that doesn't hide an inherited member, a warning is issued to that effect. This warning is suppressed by removing the new modifier.

> Note: The members in class object are not, strictly speaking, members of any interface (§18.4). However, the members in class object are available via member lookup in any interface type (§12.5). end note

The set of members of an interface declared in multiple parts (§15.2.7) is the union of the members declared in each part. The bodies of all parts of the interface declaration share the same declaration space (§7.3), and the scope of each member (§7.7) extends to the bodies of all the parts.

### 18.4.2 接口方法

Interface methods are declared using interface_method_declarations:

```
interface_method_declaration
  : attributes? 'new'? return_type interface_method_header
  | attributes? 'new'? ref_kind ref_return_type interface_method_header
  ;

interface_method_header
  : identifier '(' formal_parameter_list? ')' ';'
  | identifier type_parameter_list '(' formal_parameter_list? ')'
    type_parameter_constraints_clause* ';'
  ;
```

The attributes, return_type, ref_return_type, identifier, and formal_parameter_list of an interface method declaration have the same meaning as those of a method declaration in a class (§15.6). An interface method declaration is not permitted to specify a method body, and the declaration therefore always ends with a semicolon.

All formal parameter types of an interface method shall be input-safe (§18.2.3.2), and the return type shall be either void or output-safe. In addition, any output or reference formal parameter types shall also be output-safe.

> Note: Output parameters are required to be input-safe due to common implementation restrictions. end note

Furthermore, each class type constraint, interface type constraint and type parameter constraint on any type parameters of the method shall be input-safe. Furthermore, each class type constraint, interface type constraint and type parameter constraint on any type parameter of the method shall be input-safe.

These rules ensure that any covariant or contravariant usage of the interface remains typesafe.

Example:

```
interface I<out T>
{
    void M<U>() where U : T;    // Error
}
```

is ill-formed because the usage of T as a type parameter constraint on U is not input-safe.

Were this restriction not in place it would be possible to violate type safety in the following manner:

```csharp
class B {}
class D : B {}
class E : B {}
class C : I<D>
{
    public void M<U>() {...}
}

...

I<B> b = new C();
b.M<E>();
```

This is actually a call to C.M<E>. But that call requires that E derive from D, so type safety would be violated here.

end example

### 18.4.3 接口属性

Interface properties are declared using interface_property_declarations:

```
interface_property_declaration
    : attributes? 'new'? type identifier '{' interface_accessors '}'
    | attributes? 'new'? ref_kind type identifier '{' ref_interface_accessor '}'
    ;

interface_accessors
    : attributes? 'get' ';'
    | attributes? 'set' ';'
    | attributes? 'get' ';' attributes? 'set' ';'
    | attributes? 'set' ';' attributes? 'get' ';'
    ;

ref_interface_accessor
    : attributes? 'get' ';'
    ;
```

The *attributes*, *type*, and *identifier* of an interface property declaration have the same meaning as those of a property declaration in a class (§15.7).

The accessors of an interface property declaration correspond to the accessors of a class property declaration (§15.7.3), except that the *accessor_body* shall always be a semicolon. Thus, the accessors simply indicate whether the property is read-write, read-only, or write-only.

The type of an interface property shall be output-safe if there is a get accessor, and shall be input-safe if there is a set accessor.

### 18.4.4 接口事件

Interface events are declared using *interface_event_declarations*:

```
interface_event_declaration
    : attributes? 'new'? 'event' type identifier ';'
    ;
```



The attributes, type, and identifier of an interface event declaration have the same meaning as those of an event declaration in a class (§15.8).

The type of an interface event shall be input-safe.

## 18.4.5 Interface indexers

Interface indexers are declared using interface_indexer_declarations:

```
interface_indexer_declaration
: attributes? 'new'? type 'this' '[' formal_parameter_list ']'
'{' interface_accessors '}'
| attributes? 'new'? ref_kind type 'this' '[' formal_parameter_list ']'
'{' ref_interface_accessor '}'
;
```

The attributes, type, and formal_parameter_list of an interface indexer declaration have the same meaning as those of an indexer declaration in a class (§15.9).

The accessors of an interface indexer declaration correspond to the accessors of a class indexer declaration (§15.9), except that the accessor_body shall always be a semicolon. Thus, the accessors simply indicate whether the indexer is read-write, read-only, or write-only.

All the formal parameter types of an interface indexer shall be input-safe (§18.2.3.2). In addition, any output or reference formal parameter types shall also be output-safe.

> 注意：由于常见的实现限制，输出参数要求为输入安全。
> 结束注意

The type of an interface indexer shall be output-safe if there is a get accessor, and shall be input-safe if there is a set accessor.

## 18.4.6 Interface member access

Interface members are accessed through member access (§12.8.7) and indexer access (§12.8.11.3) expressions of the form I.M and I[A], where I is an interface type, M is a method, property, or event of that interface type, and A is an indexer argument list.

For interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effects of the member lookup (§12.5), method invocation (§12.8.9.2), and indexer access (§12.8.11.3) rules are exactly the same as for classes and structs: More derived members hide less derived members with the same name or signature. However, for multiple-inheritance interfaces, ambiguities can occur when two or more unrelated base interfaces declare members with the same name or signature. This subclause shows several examples, some of which lead to ambiguities and others which don't. In all cases, explicit casts can be used to resolve the ambiguities.

示例：在下面的代码中

```csharp
interface IList
{
    int Count { get; set; }
}

interface ICounter
{
    void Count(int i);
}

interface IListCounter : IList, ICounter {}

class C
{
    void Test(IListCounter x)
    {
        x.Count(1);             // Error
        x.Count = 1;            // Error
        ((IList)x).Count = 1;   // Ok, invokes IList.Count.set
        ((ICounter)x).Count(1); // Ok, invokes ICounter.Count
    }
}
```

前两个语句会导致编译时错误，因为在 IListCounter 中 Count 的成员查找（§12.5）是不明确的。如示例所示，通过将 x 转换为适当的基接口类型可以解决歧义。此类转换没有运行时成本——它们仅在编译时将实例视为更少派生的类型。

结束示例

示例：在下面的代码中

```csharp
interface IInteger
{
    void Add(int i);
}

interface IDouble
{
    void Add(double d);
}

interface INumber : IInteger, IDouble {}

class C
{
    void Test(INumber n)
    {
        n.Add(1);                  // Invokes IInteger.Add
        n.Add(1.0);                // Only IDouble.Add is applicable
        ((IInteger)n).Add(1);      // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);       // Only IDouble.Add is a candidate
    }
}
```

调用 n.Add(1) 通过应用 §12.6.4 的重载解析规则选择 IInteger.Add。类似地，调用 n.Add(1.0) 选择 IDouble.Add。当插入显式转换时，只有一个候选方法，因此没有歧义。

结束示例

示例：在下面的代码中

```csharp
interface IBase
{
    void F(int i);
}

interface ILeft : IBase
{
    new void F(int i);
}

interface IRight : IBase
{
    void G();
}

interface IDerived : ILeft, IRight {}

class A
{
    void Test(IDerived d)
    {
        d.F(1);             // Invokes ILeft.F
        ((IBase)d).F(1);    // Invokes IBase.F
        ((ILeft)d).F(1);    // Invokes ILeft.F
        ((IRight)d).F(1);   // Invokes IBase.F
    }
}
```

IBase.F 成员被 ILeft.F 成员隐藏。因此调用 d.F(1) 选择 ILeft.F，即使 IBase.F 在通过 IRight 的访问路径中似乎未被隐藏。

多继承接口中隐藏的直观规则很简单：只要成员在任何访问路径中被隐藏，它就在所有访问路径中被隐藏。因为从 IDerived 到 ILeft 再到 IBase 的访问路径隐藏了 IBase.F，所以该成员也在从 IDerived 到 IRight 再到 IBase 的访问路径中被隐藏。

结束示例

## 18.5 Qualified interface member names

接口成员有时通过其限定接口成员名称引用。接口成员的限定名称由声明该成员的接口的名称、一个点以及成员的名称组成。成员的限定名称引用声明该成员的接口。

示例：给定以下声明

```csharp
interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}
```

Paint 的限定名称为 IControl.Paint，SetText 的限定名称为 ITextBox.SetText。在上面的示例中，不可能将 Paint 称为 ITextBox.Paint。

结束示例

当接口属于命名空间的一部分时，限定接口成员名称可以包含命名空间名称。

示例：

```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

在 `System` 命名空间内，`ICloneable.Clone` 和 `System.ICloneable.Clone` 都是 `Clone` 方法的限定接口成员名称。

结束示例

## 18.6 Interface implementations

### 18.6.1 General

接口可以由类和结构实现。为了表示类或结构直接实现接口，接口包含在该类或结构的基类列表中。

示例：

```csharp
interface ICloneable
{
    object Clone();
}

interface IComparable
{
    int CompareTo(object other);
}

class ListEntry : ICloneable, IComparable
{
    public object Clone() {...}
    public int CompareTo(object other) {...}
}
```

结束示例

直接实现接口的类或结构也隐式实现该接口的所有基接口。即使类或结构在基类列表中没有显式列出所有基接口，此规则也成立。

示例：

```csharp
interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}

class TextBox : ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

在这里，类 TextBox 同时实现 IControl 和 ITextBox。

结束示例

当类 C 直接实现接口时，从 C 派生的所有类也隐式实现该接口。

类声明中指定的基接口可以是构造接口类型（§8.4、§18.2）。

示例：下面的代码说明了类如何实现构造接口类型：

```csharp
class C<U, V> {}
interface II<U> {}
class D : C<string, int>, II<string> {}
class E<T> : C<int, T>, II<T> {}
```

结束示例

泛型类声明的基接口应满足 §18.6.3 中描述的唯一性规则。

### 18.6.2 Explicit interface member implementations

为了实现接口的目的，类或结构可以声明显式接口成员实现。显式接口成员实现是引用限定接口成员名称的方法、属性、事件或索引器声明。

示例：

```csharp
interface IList<T>
{
    T[] GetElements();
}

interface IDictionary<K, V>
{
    V this[K key] { get; }
    void Add(K key, V value);
}

class List<T> : IList<T>, IDictionary<int, T>
{
    T[] IList<T>.GetElements() {...}
    T IDictionary<int, T>.this[int index] {...}
    void IDictionary<int, T>.Add(int index, T value) {...}
}
```

这里 IDictionary<int,T>.this 和 IDictionary<int,T>.Add 是显式接口成员实现。

结束示例



示例：在某些情况下，接口成员的名称可能不适合实现类，此时可以使用显式接口成员实现来实现该接口成员。例如，实现文件抽象的类很可能实现一个 Close 成员函数，其效果是释放文件资源，并使用显式接口成员实现来实现 IDisposable 接口的 Dispose 方法：

```interface IDisposable
{
    void Dispose();
}
```

```class MyFile : IDisposable
{
    void IDisposable.Dispose() => Close();

    public void Close()
    {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

示例结束

在方法调用、属性访问、事件访问或索引器访问中，不可能通过显式接口成员实现的限定接口成员名来访问该实现。显式接口成员实现只能通过接口实例访问，并且在这种情况下仅通过其成员名引用。

显式接口成员实现包含除 extern 或 async 以外的任何修饰符（§15.6）都是编译时错误。

显式接口方法实现包含 type_parameter_constraints_clauses 是编译时错误。泛型显式接口方法实现的约束继承自接口方法。

> 注意：显式接口成员实现具有与其他成员不同的可访问性特征。由于显式接口成员实现永远无法在方法调用或属性访问中通过限定接口成员名访问，因此从某种意义上说它们是私有的。然而，由于可以通过接口访问它们，因此从某种意义上说，它们也与声明它们的接口一样是公共的。显式接口成员实现有两个主要用途：

- 由于显式接口成员实现不能通过类或结构实例访问，因此它们允许将接口实现从类或结构的公共接口中排除。当类或结构实现一个对该类或结构的使用者不感兴趣的内部接口时，这一点尤其有用。
- 显式接口成员实现允许消除具有相同签名的接口成员的歧义。如果没有显式接口成员实现，类或结构就不可能为具有相同签名和返回类型的接口成员提供不同的实现，也不可能为具有相同签名但返回类型不同的接口成员提供任何实现。

注意结束

为使显式接口成员实现有效，类或结构应在其基类列表中命名一个接口，该接口包含一个成员，其限定接口成员名、类型、类型参数数量和参数类型与显式接口成员实现完全匹配。如果接口函数成员具有参数数组，则关联的显式接口成员实现的对应参数允许（但非必须）具有 params 修饰符。如果接口函数成员没有参数数组，则关联的显式接口成员实现不得具有参数数组。

示例：因此，在以下类中

```class Shape : ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...} // invalid
}
```

IComparable.CompareTo 的声明会导致编译时错误，因为 IComparable 未列在 Shape 的基类列表中，并且不是 ICloneable 的基接口。同样，在以下声明中

```class Shape : ICloneable
{
    object ICloneable.Clone() {...}
}
```

```class Ellipse : Shape
{
    object ICloneable.Clone() {...} // invalid
}
```

Ellipse 中 ICloneable.Clone 的声明会导致编译时错误，因为 ICloneable 未显式列在 Ellipse 的基类列表中。

示例结束

显式接口成员实现的限定接口成员名应引用声明该成员的接口。

示例：因此，在以下声明中

```interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}

class TextBox : ITextBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
}
```

Paint 的显式接口成员实现必须写成 IControl.Paint，而不是 ITextBox.Paint。

示例结束

## 18.6.3 所实现接口的唯一性

泛型类型声明所实现的接口对于所有可能的构造类型都应当保持唯一。如果没有这条规则，对于某些构造类型就无法确定应调用哪个正确的方法。

示例：假设允许将泛型类声明写成如下形式：

```interface I<T>
{
    void F();
}

class X<U ,V> : I<U>, I<V> // Error: I<U> and I<V> conflict
{
    void I<U>.F() {...}
    void I<V>.F() {...}
}
```

如果允许这样做，那么在以下情况中就无法确定应执行哪段代码：

```I<int> x = new X<int, int>();
x.F();
```

示例结束

为了确定泛型类型声明的接口列表是否有效，需执行以下步骤：

- 令 L 为泛型类、结构或接口声明 C 中直接指定的接口列表。
- 将 L 中已有接口的任何基接口添加到 L。
- 从 L 中移除任何重复项。
- 如果由 C 创建的任一可能构造类型在将类型实参替换到 L 中之后，会导致 L 中的两个接口相同，则 C 的声明无效。在确定所有可能的构造类型时，不考虑约束声明。

注意：在上述类声明 X 中，接口列表 L 由 I<U> 和 I<V> 组成。该声明无效，因为任何将 U 和 V 指定为相同类型的构造类型都会导致这两个接口成为相同类型。注意结束

在不同继承级别指定的接口可以统一：

```interface I<T>
{
    void F();
}

class Base<U> : I<U>
{
    void I<U>.F() {...}
}

class Derived<U, V> : Base<U>, I<V> // Ok
{
    void I<V>.F() {...}
}
```

即使 Derived<U,V> 同时实现 I<U> 和 I<V>，此代码仍然有效。以下代码

```I<int> x = new Derived<int, int>();
x.F();
```

将调用 Derived 中的方法，因为 Derived<int,int>' 实际上重新实现了 I<int>（§18.6.7）。

## 18.6.4 泛型方法的实现

当泛型方法隐式实现接口方法时，为每个方法类型参数给出的约束在两个声明中应当等效（在将任何接口类型参数替换为相应的类型实参之后），其中方法类型参数按从左到右的序数位置标识。

示例：在以下代码中：

```interface I<X, Y, Z>
{
    void F<T>(T t) where T : X;
    void G<T>(T t) where T : Y;
    void H<T>(T t) where T : Z;
}

class C : I<object, C, string>
{
    public void F<T>(T t) {...}                 // Ok
    public void G<T>(T t) where T : C {...}     // Ok
    public void H<T>(T t) where T : string {...} // Error
}
```

方法 C.F<T> 隐式实现 I<object,C,string>.F<T>。在这种情况下，C.F<T> 不需要（也不允许）指定约束 T : object，因为 object 是所有类型参数上的隐式约束。方法 C.G<T> 隐式实现 I<object,C,string>.G<T>，因为在将接口类型参数替换为相应类型实参之后，其约束与接口中的约束匹配。方法 C.H<T> 的约束是错误的，因为密封类型（在此例中为 string）不能用作约束。省略该约束也会是错误的，因为隐式接口方法实现的约束要求匹配。因此，无法隐式实现 I<object,C,string>.H<T>。此接口方法只能使用显式接口成员实现来实现：

```class C : I<object, C, string>
{
    ...
    public void H<U>(U u) where U : class {...}

    void I<object, C, string>.H<T>(T t)
    {
        string s = t; // Ok
        H<T>(t);
    }
}
```



在这种情况下，显式接口成员实现调用了一个具有严格更弱约束的公共方法。从 t 到 s 的赋值是有效的，因为 T 继承了 T: string 的约束，即使该约束在源代码中无法表达。结束示例

注意：当泛型方法显式实现接口方法时，实现方法上不允许有约束（§15.7.1, §18.6.2）。结束注释

## 18.6.5 接口映射

类或结构必须为类或结构基类列表中列出的接口的所有成员提供实现。在实现类或结构中定位接口成员实现的过程称为接口映射。

对于类或结构 C 的接口映射，会为 C 的基类列表中指定的每个接口的每个成员定位一个实现。特定接口成员 I.M 的实现，其中 I 是声明成员 M 的接口，是通过检查每个类或结构 S 确定的，从 C 开始并对 C 的每个后续基类重复，直到找到匹配项：

- 如果 S 包含与 I 和 M 匹配的显式接口成员实现声明，则该成员是 I.M 的实现。
- 否则，如果 S 包含与 M 匹配的非静态公共成员声明，则该成员是 I.M 的实现。如果匹配的成员多于一个，则未指定哪个成员是 I.M 的实现。这种情况只能发生在 S 是构造类型时，其中两个成员在泛型类型中声明的签名不同，但类型参数使它们的签名相同。

如果无法为 C 的基类列表中指定的所有接口的所有成员定位实现，则会发生编译时错误。接口的成员包括从基接口继承的那些成员。

构造接口类型的成员被认为已将任何类型参数替换为 §15.3.3 中指定的相应类型参数：

示例：例如，给定泛型接口声明：

```
interface I<T>
{
    T F(int x, T[, ] y);
    T this[int y] { get; }
}
```

构造接口 I<string[]> 具有以下成员：

```
string[] F(int x, string[,][] y);
string[] this[int y] { get; }
```

结束示例

出于接口映射的目的，类或结构成员 A 与接口成员 B 匹配的条件是：

- A 和 B 都是方法，并且 A 和 B 的名称、类型和形式参数列表相同。
- A 和 B 都是属性，并且 A 和 B 的名称和类型相同，且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。
- A 和 B 都是事件，并且 A 和 B 的名称和类型相同。
- A 和 B 都是索引器，并且 A 和 B 的类型和形式参数列表相同，且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。

接口映射算法的显著含义是：

- 在确定实现接口成员的类或结构成员时，显式接口成员实现优先于同一类或结构中的其他成员。
- 非公共成员和静态成员均不参与接口映射。

*示例：* 在以下代码中

```
interface ICloneable
{
    object Clone();
}

class C : ICloneable
{
    object ICloneable.Clone() {...}
    public object Clone() {...}
}
```

C 的 ICloneable.Clone 成员成为 'ICloneable' 中 Clone 的实现，因为显式接口成员实现优先于其他成员。

*结束示例*

如果类或结构实现了两个或多个包含具有相同名称、类型和参数类型的成员的接口，则可以将这些接口成员中的每一个映射到单个类或结构成员。

*示例：*

```
interface IControl
{
    void Paint();
}

interface IForm
{
    void Paint();
}

class Page : IControl, IForm
{
    public void Paint() {...}
}
```

这里，IControl 和 IForm 的 Paint 方法都映射到 Page 中的 Paint 方法。当然，也可以为这两种方法分别提供显式的接口成员实现。

*结束示例*

如果类或结构实现了一个包含隐藏成员的接口，则某些成员可能需要通过显式接口成员实现来实现。

*示例：*

```
```csharp
interface IBase
{
    int P { get; }
}

interface IDerived : IBase
{
    new int P();
}
```
```

此接口的实现至少需要一个显式接口成员实现，并将采用以下形式之一

```
```csharp
class C1 : IDerived
{
    int IBase.P { get; }
    int IDerived.P() {...}
}
class C2 : IDerived
{
    public int P { get; }
    int IDerived.P() {...}
}
class C3 : IDerived
{
    int IBase.P { get; }
    public int P() {...}
}
```
```

*结束示例*

当类实现多个具有相同基接口的接口时，基接口只能有一个实现。

*示例：* 在以下代码中

```
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}

interface IListBox : IControl
{
    void SetItems(string[] items);
}

class ComboBox : IControl, ITextBox, IListBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
}
```

```
void IListBox.SetItems(string[] items) {...}
}
```

无法为基类列表中命名的 IControl、由 ITextBox 继承的 IControl 以及由 IListBox 继承的 IControl 分别提供实现。事实上，这些接口没有单独身份的概念。相反，ITextBox 和 IListBox 的实现共享同一个 IControl 实现，并且 ComboBox 只是被认为实现了三个接口，IControl、ITextBox 和 IListBox。

结束示例

基类的成员参与接口映射。

示例：在以下代码中

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

class Class2 : Class1, Interface1
{
    public new void G() {}
}
```

Class1 中的方法 F 用于 Class2 对 Interface1 的实现。

结束示例

## 18.6.6 接口实现继承

类继承其基类提供的所有接口实现。

在不显式重新实现接口的情况下，派生类无法以任何方式更改其从基类继承的接口映射。

示例：在声明中

```
interface IControl
{
    void Paint();
}

class Control : IControl
{
    public void Paint() {...}
}

class TextBox : Control
{
    public new void Paint() {...}
}
```

TextBox 中的 Paint 方法隐藏了 Control 中的 Paint 方法，但它不会更改 Control.Paint 到 IControl.Paint 的映射，并且通过类实例和接口实例对 Paint 的调用将产生以下效果

```
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint(); // invokes Control.Paint();
t.Paint(); // invokes TextBox.Paint();
ic.Paint(); // invokes Control.Paint();
it.Paint(); // invokes Control.Paint();
end example
```

然而，当接口方法映射到类中的虚方法时，派生类可以重写该虚方法并更改接口的实现。

示例：将上述声明重写为

```
interface IControl
{
    void Paint();
}

class Control : IControl
{
    public virtual void Paint() {...}
}

class TextBox : Control
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
c.Paint(); // invokes Control.Paint();
t.Paint(); // invokes TextBox.Paint();
ic.Paint(); // invokes Control.Paint();
it.Paint(); // invokes TextBox.Paint();
end example
```

由于显式接口成员实现不能声明为虚，因此无法重写显式接口成员实现。然而，显式接口成员实现调用另一个方法是完全有效的，并且该其他方法可以声明为虚以允许派生类重写它。

示例：

```
interface IControl
{
    void Paint();
}
```


```csharp
class Base : IMethods
{
    void IMethods.F() {}
    void IMethods.G() {}
    public void H() {}
    public void I() {}
}

class Derived : Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

这里，Derived 中 IMethods 的实现将接口方法映射到 Derived.F、Base.IMethods.G、Derived.IMethods.H 和 Base.I。

*示例结束*

当一个类实现一个接口时，它也会隐式实现该接口的所有基接口。同样，接口的重新实现也隐式地是该接口所有基接口的重新实现。

*示例：*

```csharp
interface IBase
{
    void F();
}

interface IDerived : IBase
{
    void G();
}

class C : IDerived
{
    void IBase.F() {...}
    void IDerived.G() {...}
}

class D : C, IDerived
{
    public void F() {...}
    public void G() {...}
}
```

这里，IDerived 的重新实现也重新实现了 IBase，将 IBase.F 映射到 D.F。

*示例结束*

## 18.6.8 抽象类和接口

与非抽象类一样，抽象类应提供该类的基类列表中列出的接口的所有成员的实现。但是，允许抽象类将接口方法映射到抽象方法。

示例：

```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C : IMethods
{
    public abstract void F();
    public abstract void G();
}
```

这里，IMethods 的实现将 F 和 G 映射到抽象方法，这些方法应在派生自 C 的非抽象类中重写。

示例结束

显式接口成员实现不能是抽象的，但显式接口成员实现当然可以调用抽象方法。

示例：

```csharp
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

这里，派生自 C 的非抽象类将被要求重写 FF 和 GG，从而提供 IMethods 的实际实现。

示例结束

# 19. 枚举

### 19.1 概述

*枚举类型*是一种独特的值类型（§8.3），它声明一组命名常量。

*示例：以下示例*

```csharp
enum Color
{
    Red,
    Green,
    Blue
}
```

声明了一个名为 Color 的枚举类型，其成员为 Red、Green 和 Blue。

*示例结束*

### 19.2 枚举声明

枚举声明声明一个新的枚举类型。枚举声明以关键字 `enum` 开头，并定义枚举的名称、可访问性、基础类型和成员。

```
enum_declaration
    : attributes? enum_modifier* 'enum' identifier enum_base? enum_body ';'?
    ;

enum_base
    : ':' integral_type
    | ':' integral_type_name
    ;

integral_type_name
    : type_name // Shall resolve to an integral type other than char
    ;

enum_body
    : '{' enum_member_declarations? '}'
    | '{' enum_member_declarations ',' '}'
    ;
```

每个枚举类型都有一个对应的整型，称为该枚举类型的*基础类型*。此基础类型应能够表示枚举中定义的所有枚举值。如果存在 *enum_base*，则它显式声明基础类型。基础类型应是除 `char` 之外的*整型*（§8.3.6）之一。基础类型可以通过 *integral_type*（§8.3.5）或 *integral_type_name* 指定。*integral_type_name* 的解析方式与 *type_name*（§7.8.1）相同，包括考虑任何 using 指令（§14.5）。

> *注意：* `char` 类型不能用作基础类型，无论是通过关键字还是通过 `integral_type_name`。*注意结束*

未显式声明基础类型的枚举声明，其基础类型为 int。

示例：以下示例

```csharp
enum Color : long
{
    Red,
    Green,
    Blue
}
```

声明了一个基础类型为 long 的枚举。

示例结束

注意：开发者可能选择使用 long 作为基础类型，如示例所示，以便能够使用位于 long 范围内但不在 int 范围内的值，或为将来保留此选项。注意结束

注意：C# 允许在 enum_body 中出现尾随逗号，就像它允许在 array_initializer（§17.7）中出现尾随逗号一样。注意结束

枚举声明不能包含类型参数列表，但嵌套在泛型类声明或泛型结构声明内的任何枚举都是泛型枚举声明，因为创建构造类型（§8.4）时应提供包含类型的类型实参。

### 19.3 枚举修饰符

枚举声明可以选择性地包含一系列枚举修饰符：

```
enum_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    ;
```

同一修饰符在枚举声明中出现多次是编译时错误。

枚举声明的修饰符与类声明（§15.2.2）的修饰符含义相同。但是，枚举声明中不允许使用 abstract、sealed 和 static 修饰符。枚举不能是抽象的，也不允许派生。

### 19.4 枚举成员

枚举类型声明的体定义零个或多个枚举成员，这些成员是枚举类型的命名常量。任何两个枚举成员不能具有相同名称。

```
enum_member_declarations
    : enum_member_declaration (',' enum_member_declaration)*
    ;

enum_member_declaration
    : attributes? identifier ('=' constant_expression)?
    ;
```

每个枚举成员都有一个关联的常量值。此值的类型是包含该枚举的基础类型。每个枚举成员的常量值应在该枚举的基础类型的范围内。

示例：以下示例

```
enum Color: uint
{
    Red = -1,
    Green = -2,
    Blue = -3
}
```

导致编译时错误，因为常量值 -1、-2 和 -3 不在基础整型 uint 的范围内。

示例结束

多个枚举成员可以共享相同的关联值。

示例：以下示例

```
enum Color
{
    Red,
    Green,
    Blue,
    Max = Blue
}
```

展示了一个枚举，其中两个枚举成员——Blue 和 Max——具有相同的关联值。

示例结束

枚举成员的关联值通过隐式或显式方式赋值。如果枚举成员的声明具有 constant_expression 初始值设定项，则将该常量表达式的值隐式转换为枚举的基础类型后，即为该枚举成员的关联值。如果枚举成员的声明没有初始值设定项，则其关联值按如下方式隐式设置：

- 如果该枚举成员是枚举类型中声明的第一个枚举成员，则其关联值为零。
- 否则，该枚举成员的关联值通过将文本上位于其前面的枚举成员的关联值加一获得。增加后的值应在基础类型可表示的值的范围内，否则发生编译时错误。

示例：以下示例

```csharp
enum Color
{
    Red,
    Green = 10,
    Blue
}

class Test
{
    static void Main()
    {
        Console.WriteLine(StringFromColor(Color.Red));
        Console.WriteLine(StringFromColor(Color.Green));
        Console.WriteLine(StringFromColor(Color.Blue));
    }

    static string StringFromColor(Color c)
    {
        switch (c)
        {
            case Color.Red:
                return $"Red = {(int) c}";
            case Color.Green:
                return $"Green = {(int) c}";
            case Color.Blue:
                return $"Blue = {(int) c}";
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

- 枚举成员 `Red` 被自动赋值为零（因为它没有初始值设定项，并且是第一个枚举成员）；
- 枚举成员 `Green` 被显式赋予值 `10`；
- 并且枚举成员 `Blue` 被自动赋值为比文本上位于其前面的成员大 1 的值。

*示例结束*

枚举成员的关联值不得直接或间接使用其自身关联枚举成员的值。除该循环性限制外，枚举成员初始值设定项可以自由引用其他枚举成员初始值设定项，而不论其文本位置如何。在枚举成员初始值设定项内，其他枚举成员的值始终被视为具有其基础类型，因此在引用其他枚举成员时不需要强制转换。

*示例：以下示例*

```csharp
enum Circular
{
    A = B,
    B
}
```

导致编译时错误，因为 `A` 和 `B` 的声明是循环的。`A` 显式依赖 `B`，而 `B` 隐式依赖 `A`。

*示例结束*




枚举成员的命名和作用域与类中的字段完全类似。枚举成员的作用域是其包含的枚举类型的正文。在该作用域内，枚举成员可通过其简单名称引用。从所有其他代码中，枚举成员的名称必须与其枚举类型的名称一起限定。枚举成员没有声明的可访问性——如果其包含的枚举类型可访问，则枚举成员可访问。

## 19.5 The System.Enum type

类型 `System.Enum` 是所有枚举类型的抽象基类（这与枚举类型的底层类型不同且有区别），并且从 `System.Enum` 继承的成员在任何枚举类型中都可用。存在从任何枚举类型到 `System.Enum` 的装箱转换（§10.2.9），并且存在从 `System.Enum` 到任何枚举类型的拆箱转换（§10.3.7）。

请注意，`System.Enum` 本身不是 `enum_type`。相反，它是一个 `class_type`，所有 `enum_types` 都从它派生。类型 `System.Enum` 继承自类型 `System.ValueType`（§8.3.2），而后者又继承自类型 `object`。在运行时，类型为 `System.Enum` 的值可以为 `null` 或对任何枚举类型的装箱值的引用。

## 19.6 Enum values and operations

每个枚举类型定义一个不同的类型；需要显式枚举转换（§10.3.3）将枚举类型与整型转换，或在两个枚举类型之间转换。枚举类型的取值集合与底层类型的取值集合相同，并且不受命名常量的值限制。枚举的底层类型的任何值都可以强制转换为 `enum` 类型，并且是该枚举类型的不同有效值。

枚举成员具有其包含枚举类型的类型（除在其他枚举成员初始化器内外：参见 §19.4）。在枚举类型 E 中声明且关联值为 v 的枚举成员的值为 (E) v。

以下运算符可用于枚举类型的值：

- `==, !=, <, >, <=, >=` (§12.12.6)
- `binary +` (§12.10.5)
- `binary -` (§12.10.6)
- `^, &, |` (§12.13.3)
- `~` (§12.9.5)
- `++, --` (§12.8.15 and §12.9.6)
- `sizeof` (§23.6.9)

每个枚举类型自动从类 `System.Enum` 派生（后者又派生自 `System.ValueType` 和 `object`）。因此，可以在枚举类型的值上使用此类继承的方法和属性。

## 20. Delegates

### 20.1 General

委托声明定义一个派生自类 System.Delegate 的类。委托实例封装了一个调用列表，该列表是一个包含一个或多个方法的方法列表，每个方法称为可调用实体。对于实例方法，可调用实体由一个实例和该实例上的一个方法组成。对于静态方法，可调用实体仅由一个方法组成。使用适当的一组参数调用委托实例会导致委托的每个可调用实体都使用给定的参数集被调用。

> Note: An interesting and useful property of a delegate instance is that it does not know or care about the classes of the methods it encapsulates; all that matters is that those methods be compatible (§20.4) with the delegate’s type. This makes delegates perfectly suited for "anonymous" invocation. end note

### 20.2 Delegate declarations

delegate_declaration 是 type_declaration（§14.7），它声明一个新的委托类型。

```
delegate_declaration
  : attributes? delegate_modifier* 'delegate' return_type delegate_header
  | attributes? delegate_modifier* 'delegate' ref_kind ref_return_type
    delegate_header
  ;

delegate_header
  : identifier '(' formal_parameter_list? ')' ';'
  | identifier variant_type_parameter_list '(' formal_parameter_list? ')'
    type_parameter_constraints_clause* ';'
  ;

delegate_modifier
  :
    'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | unsafe_modifier  // unsafe code support
  ;
```

unsafe_modifier 在 §23.2 中定义。

在委托声明中，同一个修饰符出现多次是编译时错误。

提供 variant_type_parameter_list 的委托声明是泛型委托声明。此外，任何嵌套在泛型类声明或泛型结构声明内部的委托本身就是泛型委托声明，因为为了创建构造类型（§8.4），必须为包含类型提供类型参数。

new 修饰符仅允许在另一个类型内声明的委托上，在这种情况下它指定此类委托隐藏具有相同名称的继承成员，如 §15.3.5 中所述。

public、protected、internal 和 private 修饰符控制委托类型的可访问性。根据委托声明出现的上下文，其中一些修饰符可能不被允许（§7.5.2）。

委托的类型名称是 identifier。

与方法（§15.6.1）一样，如果存在 ref，则委托按引用返回；否则，如果 return_type 为 void，则委托不返回值；否则，委托按值返回。

可选的 formal_parameter_list 指定委托的参数。

returns-by-value 或 returns-no-value 委托声明的 return_type 指定委托返回的结果类型（如果有）。

returns-by-ref 委托声明的 ref_return_type 指定由委托返回的 variable_reference（§9.5）引用的变量的类型。

可选的 variant_type_parameter_list（§18.2.3）指定委托本身的类型参数。

委托类型的返回类型应为 void 或 output-safe（§18.2.3.2）。

委托类型的所有形式参数类型都应为 input-safe（§18.2.3.2）。此外，任何输出或引用参数类型也应为 output-safe。

> Note: Output parameters are required to be input-safe due to common implementation restrictions.
> end note

此外，委托的任何类型参数上的每个类类型约束、接口类型约束和类型参数约束都应为 input-safe。

C# 中的委托类型按名称等价，而不是按结构等价。

Example:

```
delegate int D1(int i, double d);
delegate int D2(int c, double d);
```

委托类型 D1 和 D2 是两种不同的类型，因此它们不可互换，尽管它们的签名相同。

end example

与其它泛型类型声明一样，应给出类型参数以创建构造的委托类型。通过为委托声明中的每个类型参数替换构造的委托类型的相应类型参数，对构造的委托类型的参数类型和返回类型进行创建。

声明委托类型的唯一方法是通过 delegate_declaration。每个委托类型都是派生自 System.Delegate 的引用类型。每个委托类型所需成员的详细信息在 §20.3 中。委托类型隐式为密封，因此不允许从委托类型派生任何类型。也不允许声明派生自 System.Delegate 的非委托类类型。System.Delegate 本身不是委托类型；它是从所有委托类型派生的类类型。

### 20.3 Delegate members

每个委托类型都继承自 Delegate 类的成员，如 §15.3.4 所述。此外，每个委托类型必须提供一个非泛型的 Invoke 方法，其参数列表与委托声明中的 formal_parameter_list 匹配，其返回类型与委托声明中的 return_type 或 ref_return_type 匹配，并且对于按引用返回的委托，其 ref_kind 与委托声明中的匹配。Invoke 方法的可访问性至少应与包含的委托类型一样。调用委托类型上的 Invoke 方法在语义上等同于使用委托调用语法（§20.6）。

实现可以在委托类型中定义其他成员。

除了实例化之外，可以应用于类或类实例的任何操作也可以分别应用于委托类或实例。特别是，可以通过通常的成员访问语法访问 System.Delegate 类型的成员。

### 20.4 Delegate compatibility

方法或委托类型 M 与委托类型 D 兼容当且仅当以下所有条件为真时：

- D 和 M 具有相同数量的参数，并且 D 中的每个参数与 M 中对应的参数具有相同的 in、out 或 ref 修饰符。
- 对于每个值参数，从 D 中的参数类型到 M 中对应的参数类型存在恒等转换（§10.2.2）或隐式引用转换（§10.2.8）。
- 对于每个 in、out 或 ref 参数，D 中的参数类型与 M 中的参数类型相同。
- 以下其中之一为真：
  - D 和 M 都是 returns-no-value
  - D 和 M 都是 returns-by-value（§15.6.1、§20.2），并且从 M 的返回类型到 D 的返回类型存在恒等或隐式引用转换。
  - D 和 M 都是 returns-by-ref，M 的返回类型与 D 的返回类型之间存在恒等转换，并且两者具有相同的 ref_kind。

此兼容性定义允许返回类型的协变和参数类型的逆变。

Example:

```
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
```

```csharp
}
class Test
{
    static void Main()
    {
        D cd1 = new D(C.M1); // M1 - one entry in invocation list
        D cd2 = new D(C.M2); // M2 - one entry
        D cd3 = cd1 + cd2;   // M1 + M2 - two entries
        D cd4 = cd3 + cd1;   // M1 + M2 + M1 - three entries
        D cd5 = cd4 + cd3;   // M1 + M2 + M1 + M1 + M2 - five entries
        D td3 = new D(cd3);  // [M1 + M2] - ONE entry in invocation
                             // list, which is itself a list of two methods.
        D td4 = td3 + cd1;   // [M1 + M2] + M1 - two entries
        D cd6 = cd4 - cd2;   // M1 + M1 - two entries in invocation list
        D td6 = td4 - cd2;   // [M1 + M2] + M1 - two entries in invocation list,
                             // but still three methods called, M2 not removed.
    }
}
```

当 cd1 和 cd2 被实例化时，它们各自封装一个方法。当 cd3 被实例化时，它有一个包含两个方法 M1 和 M2 的调用列表，按此顺序。cd4 的调用列表包含 M1、M2 和 M1，按此顺序。对于 cd5，调用列表包含 M1、M2、M1、M1 和 M2，按此顺序。

使用 delegate_creation_expression 从另一个委托创建委托时，结果的调用列表结构与原始列表不同，但会导致以相同顺序调用相同的方法。当 td3 从 cd3 创建时，其调用列表只有一个成员，但该成员是方法 M1 和 M2 的列表，并且这些方法由 td3 以与 cd3 相同顺序调用。类似地，当 td4 被实例化时，其调用列表只有两个条目，但它按顺序调用三个方法 M1、M2 和 M1，就像 cd4 一样。

调用列表的结构会影响委托的减法。通过从 cd4（调用 M1、M2 和 M1）中减去 cd2（调用 M2）创建的委托 cd6 调用 M1 和 M1。然而，通过从 td4（调用 M1、M2 和 M1）中减去 cd2（调用 M2）创建的委托 td6 仍然按顺序调用 M1、M2 和 M1，因为 M2 不是列表中的单个条目，而是嵌套列表的成员。有关组合（以及移除）委托的更多示例，请参阅 §20.6。 示例结束

一旦实例化，委托实例始终引用相同的调用列表。

注意：请记住，当两个委托组合，或一个从另一个中移除时，会产生一个新的委托并拥有自己的调用列表；被组合或移除的委托的调用列表保持不变。 注释结束

## 20.6 委托调用

C# 提供了用于调用委托的特殊语法。当一个非空的委托实例，其调用列表包含一个条目，被调用时，它使用相同的参数调用该方法，并返回被引用方法相同的返回值。（有关委托调用的详细信息，请参阅 §12.8.9.4。）如果在调用此类委托期间发生异常，并且该异常未在被调用的方法内捕获，则异常捕获子句的搜索将继续在调用该委托的方法中，就好像该方法直接调用了该委托引用的方法一样。

调用包含多个条目的委托实例的调用列表时，将按顺序同步调用调用列表中的每个方法。每个被调用的方法都传递与委托实例相同的参数集。如果此类委托调用包含引用参数（§15.6.2.4），则每次方法调用都将使用对同一变量的引用；调用列表中一个方法对该变量的更改将对调用列表中后面的方法可见。如果委托调用包含输出参数或返回值，则其最终值来自列表中最后一个委托的调用。如果在处理此类委托的调用期间发生异常，并且该异常未在被调用的方法内捕获，则异常捕获子句的搜索将继续在调用该委托的方法中，并且调用列表中后面的任何方法都不会被调用。

尝试调用值为 null 的委托实例会引发 System.NullReferenceException 类型的异常。

示例：以下示例展示了如何实例化、组合、移除和调用委托：

```
delegate void D(int x);

class C
{
    public static void M1(int i) => Console.WriteLine("C.M1: " + i);
    public static void M2(int i) => Console.WriteLine("C.M2: " + i);
    public void M3(int i) => Console.WriteLine("C.M3: " + i);
}

class Test
{
    static void Main()
    {
        D cd1 = new D(C.M1);
        cd1(-1);                // call M1
        D cd2 = new D(C.M2);
        cd2(-2);                // call M2
        D cd3 = cd1 + cd2;      // call M1 then M2
        cd3(10);
        cd3 += cd1;
        cd3(20);                // call M1, M2, then M1
        C c = new C();
        D cd4 = new D(c.M3);
        cd3 += cd4;
        cd3(30);                // call M1, M2, M1, then M3
        cd3 -= cd1;             // remove last M1
        cd3(40);                // call M1, M2, then M3
        cd3 -= cd4;
        cd3(50);                // call M1 then M2
        cd3 -= cd2;
        cd3(60);                // call M1
        cd3 -= cd2;             // impossible removal is benign
        cd3(60);                // call M1
        cd3 -= cd1;    // invocation list is empty so cd3 is null
        // cd3(70);    // System.NullReferenceException thrown
        cd3 -= cd1;    // impossible removal is benign
    }
}
```

如语句 cd3 += cd1; 所示，一个委托可以在调用列表中多次出现。在这种情况下，它只是按出现次数调用一次。在这样的调用列表中，当该委托被移除时，实际被移除的是调用列表中最后一次出现。

在最终语句 cd3 -= cd1; 执行之前，委托 cd3 引用一个空的调用列表。尝试从空列表中移除委托（或从非空列表中移除不存在的委托）不是错误。

生成的输出为：

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

*示例结束*

一旦找到匹配的 catch 子句，系统就会准备将控制权转移到 catch 子句的第一个语句。在 catch 子句执行开始之前，系统首先按顺序执行与比捕获异常的 try 语句更嵌套的 try 语句相关联的任何 finally 子句。

如果没有找到匹配的 catch 子句：

- 如果搜索匹配的 catch 子句到达静态构造函数（§15.12）或静态字段初始化器，则会在触发静态构造函数调用的位置抛出 System.TypeInitializationException。System.TypeInitializationException 的内部异常包含最初抛出的异常。
- 否则，如果在终结器执行期间发生异常，并且该异常未被捕获，则行为未指定。
- 否则，如果搜索匹配的 catch 子句到达最初启动线程的代码，则线程的执行将被终止。此类终止的影响由实现定义。

## 21.5 常见异常类

以下异常由某些 C# 操作抛出。

| 异常类型 | 描述 |
|---|---|
| System.ArithmeticException | 在算术运算期间发生的异常的基类，例如 System.DivideByZeroException 和 System.OverflowException。 |
| System.ArrayTypeMismatchException | 当向数组存储失败，因为存储元素的类型与数组的类型不兼容时抛出。 |
| System.DivideByZeroException | 当尝试将整数值除以零时抛出。 |
| System.IndexOutOfRangeException | 当尝试通过小于零或超出数组边界的索引对数组进行索引时抛出。 |
| System.InvalidCastException | 当从基类型或接口到派生类型的显式转换在运行时失败时抛出。 |
| System.NullReferenceException | 当空引用被以需要引用对象的方式使用时抛出。 |
| System.OutOfMemoryException | 当尝试分配内存（通过 new）失败时抛出。 |
| System.OverflowException | 当在检查上下文中的算术运算溢出时抛出。 |
| System.StackOverflowException | 当执行栈因待处理调用过多而耗尽时抛出；通常表示非常深或无界的递归。 |
| System.TypeInitializationException | 当静态构造函数或静态字段初始化器抛出异常，且不存在捕获它的 catch 子句时抛出。 |




# 22. 特性
### 22.1 概述

C# 语言的许多部分使程序员能够指定关于程序中定义的实体的声明性信息。例如，类中方法的可访问性通过使用方法修饰符 public、protected、internal 和 private 修饰该方法来指定。

C# 使程序员能够发明新种类的声明性信息，称为特性。程序员随后可以将特性附加到各种程序实体，并在运行时环境中检索特性信息。

> 注意：例如，框架可能定义一个 HelpAttribute 特性，该特性可以放在某些程序元素（如类和方法）上，以提供从这些程序元素到其文档的映射。注释结束

特性通过声明特性类（§22.2）来定义，特性类可以具有位置参数和命名参数（§22.2.3）。特性使用特性规范（§22.3）附加到 C# 程序中的实体，并可以在运行时作为特性实例（§22.4）检索。

### 22.2 特性类
### 22.2.1 概述

从抽象类 System.Attribute 直接或间接派生的类就是特性类。特性类的声明定义了一种可以放在程序实体上的新特性。按照约定，特性类以 Attribute 后缀命名。特性的使用可以包含或省略此后缀。

泛型类声明不得将 System.Attribute 用作直接或间接基类。

```
Example:
public class B : Attribute {}
public class <T> : B {} // Error - generic cannot be an attribute
end example
```

### 22.2.2 特性的用法

特性 AttributeUsage（§22.5.2）用于描述特性类可以如何使用。

AttributeUsage 具有一个位置参数（§22.2.3），它使特性类能够指定可以在哪些种类的程序实体上使用它。

示例：以下示例定义一个名为 SimpleAttribute 的特性类，该类只能放在类声明和接口声明上，并展示 Simple 特性的若干用法。

```
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute : Attribute
{
  ...
}
```

```
[Simple] class Class1 {...}
[Simple] interface Interface1 {...}
```

尽管此特性定义时名为 SimpleAttribute，但在使用此特性时，可以省略 Attribute 后缀，从而得到短名称 Simple。因此，上面的示例在语义上等价于以下内容

```
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

*示例结束*

AttributeUsage 具有一个命名参数（§22.2.3），称为 AllowMultiple，它指示是否可以为给定实体多次指定该特性。如果特性类的 AllowMultiple 为 true，则该特性类是多次使用特性类，并且可以在一个实体上多次指定。如果特性类的 AllowMultiple 为 false 或未指定，则该特性类是单次使用特性类，并且在一个实体上最多只能指定一次。

示例：以下示例定义一个名为 AuthorAttribute 的多次使用特性类，并展示一个类声明，其中使用了两次 Author 特性：

```
[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute : Attribute
{
    public string Name { get; }
    public AuthorAttribute(string name) => Name = name;
}
```

```
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1
{
    ...
}
```

*示例结束*

AttributeUsage 还有另一个命名参数（§22.2.3），称为 Inherited，它指示当特性在基类上指定时，是否也由从该基类派生的类继承。如果特性类的 Inherited 为 true，则该特性会被继承。如果特性类的 Inherited 为 false，则该特性不会被继承。如果未指定，则其默认值为 true。

未附加 AttributeUsage 特性的特性类 X，如下所示
    class X : Attribute { ... }
等价于以下内容：

```
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true
)]
class X : Attribute { ... }
```

### 22.2.3 位置参数和命名参数

特性类可以具有*位置参数*和*命名参数*。特性类的每个公共实例构造函数为该特性类定义有效的位置参数序列。特性类的每个非静态公共可读写字段和属性为该特性类定义一个命名参数。对于要定义命名参数的属性，该属性应同时具有公共 get 访问器和公共 set 访问器。

*示例：* 以下示例定义一个名为 `HelpAttribute` 的特性类，该类具有一个位置参数 `url` 和一个命名参数 `Topic`。尽管属性 `Url` 是非静态且公共的，但它不定义命名参数，因为它不是可读写的。还展示了此特性的两个用法：

```
    [AttributeUsage(AttributeTargets.Class)]
    public class HelpAttribute : Attribute
    {
        public HelpAttribute(string url) // url is a positional parameter
        {
            ...
        }

        // Topic is a named parameter
        public string Topic
        {
            get;
            set;
        }

        public string Url { get; }
    }

    [Help("http://www.mycompany.com/xxx/Class1.htm")]
    class Class1
    {
    }

    [Help("http://www.mycompany.com/xxx/Misc.htm", Topic ="Class2")]
    class Class2
    {
    }
```

*示例结束*

### 22.2.4 特性参数类型

特性类的位置参数和命名参数的类型仅限于*特性参数类型*，即：

- 下列类型之一：bool、byte、char、double、float、int、long、sbyte、short、string、uint、ulong、ushort。
- 类型 object。
- 类型 System.Type。
- 枚举类型。
- 上述类型的一维数组。
- 不具有这些类型之一的构造函数参数或公共字段，不得在特性规范中用作位置参数或命名参数。

### 22.3 特性规范

*特性规范*是将先前定义的特性应用到程序实体。特性是为程序实体指定的一条附加声明性信息。特性可以在全局范围（以指定包含程序集或模块上的特性）以及为*类型声明*（§14.7）、*类成员声明*（§15.3）、*接口成员声明*（§18.4）、*结构成员声明*（§16.3）、*枚举成员声明*（§19.2）、*访问器声明*（§15.7.3）、*事件访问器声明*（§15.8）、*形参列表*的元素（§15.6.2）以及*类型参数列表*的元素（§15.2.3）指定。

特性在*特性节*中指定。特性节由一对英文方括号组成，方括号括住一个以逗号分隔的一个或多个特性的列表。特性在此类列表中的指定顺序，以及附加到同一程序实体的各节的排列顺序，并不重要。例如，特性规范 [A][B]、[B][A]、[A, B] 和 [B, A] 是等价的。

```
global_attributes
    : global_attribute_section+
    ;

global_attribute_section
    : '[' global_attribute_target_specifier attribute_list ']'
    | '[' global_attribute_target_specifier attribute_list ',' ']'
    ;

global_attribute_target_specifier
    : global_attribute_target ':'
    ;

global_attribute_target
    : identifier
    ;

attributes
    : attribute_section+
    ;

attribute_section
    : '[' attribute_target_specifier? attribute_list ']'
    | '[' attribute_target_specifier? attribute_list ',' ']'
    ;

attribute_target_specifier
    : attribute_target ':'
    ;

attribute_target
    : identifier
    | keyword
```



```
; 
attribute_list
  : attribute (',' attribute)*
  ;

attribute
  : attribute_name attribute_arguments?
  ;

attribute_name
  : type_name
  ;

attribute_arguments
  : '(' positional_argument_list? ')'
  | '(' positional_argument_list ',' named_argument_list ')'
  | '(' named_argument_list ')'
  ;

positional_argument_list
  : positional_argument (',' positional_argument)*
  ;

positional_argument
  : argument_name? attribute_argument_expression
  ;

named_argument_list
  : named_argument (',' named_argument)*
  ;

named_argument
  : identifier '=' attribute_argument_expression
  ;

attribute_argument_expression
  : expression
  ;
```

对于产生式 global_attribute_target，以及在下文中，标识符的拼写应等于 assembly 或 module，其中相等性按 §6.4.3 定义。对于产生式 attribute_target，以及在下文中，标识符的拼写应不等于 assembly 或 module，使用与上文相同的相等性定义。

特性由特性名和可选的按位置参数与命名参数列表组成。按位置参数（如果有）位于命名参数之前。按位置参数由特性参数表达式组成；命名参数由名称、等号以及其后的特性参数表达式组成，它们共同受与简单赋值相同的规则约束。命名参数的顺序不重要。

注意：为方便起见，global_attribute_section 和 attribute_section 中允许尾随逗号，就像 array_initializer（§17.7）中允许尾随逗号一样。结束注意。

特性名标识特性类。

- `return` — 目标是返回值
- 对于在属性或索引器声明的 set 访问器上指定的特性，默认目标是关联方法。否则，当 *特性目标* 等于：
  - `method` — 目标是关联方法
  - `param` — 目标是唯一的隐式参数
- 对于自动实现的属性声明上的特性，默认目标是该属性。否则，当 *特性目标* 等于：
  - `field` — 目标是该属性的编译器生成后备字段
- 对于在省略 `event_accessor_declarations` 的事件声明上指定的特性，默认目标是事件声明。否则，当 *特性目标* 等于：
  - `event` — 目标是事件声明
  - `field` — 目标是字段
  - `method` — 目标是这些方法
- 对于不省略 `event_accessor_declarations` 的事件声明，默认目标是方法。
  - `method` — 目标是关联方法
  - `param` — 目标是唯一参数

在所有其他上下文中，允许包含 *特性目标说明符*，但并非必要。

*示例：类声明可以包含或省略说明符 type：*

```
~~~csharp
[type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
~~~
```

*结束示例。*

实现可以接受其他 *特性目标*，其用途由实现定义。不识别此类 *特性目标* 的实现应发出警告，并忽略包含它的 *特性节*。

按照约定，特性类命名时带有后缀 `Attribute`。*特性名* 可以包含或省略此后缀。具体而言，*特性名* 的解析如下：

- 如果 *特性名* 中最右侧标识符是逐字标识符（§6.4.3），则 *特性名* 解析为 *类型名*（§7.8）。如果结果不是派生自 `System.Attribute` 的类型，则发生编译时错误。
- 否则，
  - *特性名* 解析为 *类型名*（§7.8），但任何错误都被抑制。如果此解析成功且结果为派生自 `System.Attribute` 的类型，则该类型是此步骤的结果。
  - 将字符 `Attribute` 追加到 *特性名* 中最右侧标识符，并将得到的标记字符串解析为 *类型名*（§7.8），但任何错误都

```
[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute : Attribute
{
    public HelpStringAttribute(string value)
    {
        Value = value;
    }

    public string Value { get; }
}
[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]  // multiple uses not allowed
public class Class1 {}
```

会导致编译时错误，因为它试图在 Class1 的声明上多次使用 HelpString，而 HelpString 是单次使用的特性类。

*结束示例*

如果以下所有陈述均为真，则表达式 E 是特性参数表达式：

- E 的类型是特性参数类型（§22.2.4）。
- 在编译时，E 的值可解析为以下之一：
  - 常量值。
  - 使用 typeof_expression（§12.8.17）获得的 System.Type 对象，该表达式指定非泛型类型、封闭构造类型（§8.4.3）或未绑定泛型类型（§8.4.4），但不能是开放泛型类型（§8.4.3）。
  - 一维特性参数表达式数组。

示例：

```
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Field)]
public class TestAttribute : Attribute
{
    public int P1 { get; set; }

    public Type P2 { get; set; }

    public object P3 { get; set; }
}

[Test(P1 = 1234, P3 = new int[]{1, 3, 5}, P2 = typeof(float))]
class MyClass {}

class C<T> {
    [Test(P2 = typeof(T))] // Error – T not a closed type.
    int x1;

    [Test(P2 = typeof(C<T>))] // Error – C<T>; not a closed type.
    int x2;

    [Test(P2 = typeof(C<int>))] // Ok
    int x3;
```

```
[Test(P2 = typeof(C<>))] // Ok
int x4;
}
end example
```

声明在多个部分中的类型的特性，通过以未指定的顺序合并其各个部分的特性来确定。如果同一特性放置在多个部分上，则等价于在该类型上多次指定该特性。

示例：以下两个部分：

```
[Attr1, Attr2("hello")]
partial class A {}

[Attr3, Attr2("goodbye")]
partial class A {}
```

等价于以下单个声明：

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
end example
```

类型参数上的特性以相同方式合并。

## 22.4 特性实例

### 22.4.1 概述

特性实例是表示运行时特性的实例。特性由特性类、按位置参数和命名参数定义。特性实例是用按位置参数和命名参数初始化的特性类的实例。

检索特性实例涉及编译时和运行时处理，如下列子条款所述。

### 22.4.2 特性的编译

具有特性类 T、按位置参数列表 P、命名参数列表 N 并指定在程序实体 E 上的特性的编译，通过以下步骤编译到程序集 A 中：

- 遵循编译形式为 new T(P) 的 object_creation_expression 的编译时处理步骤。这些步骤要么导致编译时错误，要么确定 T 上可在运行时调用的实例构造函数 C。
- 如果 C 不具有公共可访问性，则发生编译时错误。
- 对于 N 中的每个 named_argument Arg：
  - 令 Name 为 named_argument Arg 的标识符。
  - Name 应标识 T 上的非静态读写公共字段或属性。如果 T 没有此类字段或属性，则发生编译时错误。
- 如果 positional_argument_list P 中的任何值或 named_argument_list N 中的某个值的类型为 System.String，并且该值不是 Unicode 标准所定义的良好格式，则所编译的值是否等于运行时

检索到的值（§22.4.3）。

注：举例来说，包含一个高代理项 UTF-16 代码单元且其后未紧跟低代理项代码单元的字符串不是格式良好的。注结束。

-   将以下信息（用于特性的运行时实例化）存储在编译器编译包含该特性的程序后所生成的程序集输出中：特性类 T、T 上的实例构造函数 C、positional_argument_list P、named_argument_list N 以及关联的程序实体 E，且这些值在编译时完全解析。

### 22.4.3 特性实例的运行时检索

由 T、C、P 和 N 表示并与 E 关联的特性实例，可以在运行时使用以下步骤从程序集 A 中检索：

-   遵循执行形式为 new T(P) 的 object_creation_expression 的运行时处理步骤，使用实例构造函数 C 和在编译时确定的值。这些步骤要么导致异常，要么生成 T 的实例 O。
-   对于 N 中的每个 named_argument Arg，按顺序：
    -   令 Name 为 named_argument Arg 的标识符。如果 Name 未标识 O 上的非静态公共读写字段或属性，则引发异常。
    -   令 Value 为对 Arg 的 attribute_argument_expression 求值的结果。
    -   如果 Name 标识 O 上的字段，则将此字段设置为 Value。
    -   否则，Name 标识 O 上的属性。将此属性设置为 Value。
-   结果是 O，即已使用 positional_argument_list P 和 named_argument_list N 初始化的特性类 T 的实例。

注：在 A 中存储 T、C、P、N（并将其与 E 关联）的格式，以及指定 E 并从 A 中检索 T、C、P、N 的机制（并因此说明如何在运行时获得特性实例），超出了本规范的范围。注结束。

示例：在 CLI 的实现中，通过编译 §22.2.3 中的示例程序所创建的程序集中的 Help 特性实例，可以使用以下程序检索：

```
public sealed class InterrogateHelpUrls
{
    public static void Main(string[] args)
    {
        Type helpType = typeof(HelpAttribute);
        string assemblyName = args[0];
        foreach (Type t in Assembly.Load(assemblyName).GetTypes())
        {
            Console.WriteLine($"Type : {t}");
            var attributes = t.GetCustomAttributes(helpType, false);
            var helpers = ((HelpAttribute[]) attributes);
            foreach (var helper in helpers)
            {
                Console.WriteLine($"\tUrl : {helper.Url}");
            }
        }
    }
}
```

*示例结束*

## 22.5 保留特性

### 22.5.1 概述

少量特性会以某种方式影响语言。这些特性包括：

-   System.AttributeUsageAttribute（§22.5.2），用于描述特性类可被使用的方式。
-   System.Diagnostics.ConditionalAttribute（§22.5.3），是一个多用途特性类，用于定义条件方法和条件特性类。此特性通过测试条件编译符号来指示条件。
-   System.ObsoleteAttribute（§22.5.4），用于将成员标记为过时。
-   System.Runtime.CompilerServices.CallerLineNumberAttribute（§22.5.5.2）、System.Runtime.CompilerServices.CallerFilePathAttribute（§22.5.5.3）和 System.Runtime.CompilerServices.CallerMemberNameAttribute（§22.5.5.4），用于向可选参数提供有关调用上下文的信息。

执行环境可以提供额外的、特定于实现的特性，这些特性会影响 C# 程序的执行。

### 22.5.2 AttributeUsage 特性

AttributeUsage 特性用于描述特性类可被使用的方式。

使用 AttributeUsage 特性修饰的类应直接或间接派生自 System.Attribute。否则，发生编译时错误。

注：有关使用此特性的示例，参见 §22.2.2。注结束

### 22.5.3 Conditional 特性

### 22.5.3.1 概述

Conditional 特性允许定义条件方法和条件特性类。

### 22.5.3.2 条件方法

使用 Conditional 特性修饰的方法是条件方法。因此，每个条件方法都与其 Conditional 特性中声明的条件编译符号相关联。

示例：

```
class Eg
{
    [Conditional("ALPHA")]
    [Conditional("BETA")]
    public static void M()
    {
        // ...
    }
}
```

将 Eg.M 声明为与两个条件编译符号 ALPHA 和 BETA 关联的条件方法。

*示例结束*

如果条件方法的关联条件编译符号中有一个或多个在调用点已定义，则包含对该条件方法的调用；否则省略该调用。

条件方法受以下限制：

-   条件方法应是 `class_declaration` 或 `struct_declaration` 中的方法。如果在接口声明中的方法上指定 `Conditional` 特性，则发生编译时错误。
-   条件方法的返回类型应为 `void`。
-   条件方法不应使用 `override` 修饰符标记。但条件方法可以使用 `virtual` 修饰符标记。此类方法的重写隐式为条件方法，并且不应显式使用 `Conditional` 特性标记。
-   条件方法不应是接口方法的实现。否则，发生编译时错误。
-   条件方法的参数不应具有 `out` 修饰符。

此外，如果从条件方法创建委托，则发生编译时错误。

*示例：* 下面的示例

```csharp
#define DEBUG
using System;
using System.Diagnostics;

class Class1
{
    [Conditional("DEBUG")]
    public static void M()
    {
        Console.WriteLine("Executed Class1.M");
    }
}

class Class2
{
    public static void Test()
    {
        Class1.M();
    }
}
```

将 Class1.M 声明为条件方法。Class2 的 Test 方法调用此方法。由于定义了条件编译符号 DEBUG，因此如果调用 Class2.Test，它将调用 M。如果未定义符号 DEBUG，则 Class2.Test 将不会调用 Class1.M。

*示例结束*

重要的是要理解，对条件方法的调用是包含还是排除，由调用点的条件编译符号控制。

*示例：* 在以下代码中

```
// File Class1.cs:
using System.Diagnostics;
class Class1
{
    [Conditional("DEBUG")]
    public static void F()
    {
        Console.WriteLine("Executed Class1.F");
    }
}

// File Class2.cs:
#define DEBUG
class Class2
{
    public static void G()
    {
        Class1.F(); // F is called
    }
}

// File Class3.cs:
#undef DEBUG
class Class3
{
    public static void H()
    {
        Class1.F(); // F is not called
    }
}
```

类 Class2 和 Class3 各自包含对条件方法 Class1.F 的调用，该方法是否条件取决于是否定义了 DEBUG。由于此符号在 Class2 的上下文中已定义，而在 Class3 中未定义，因此包含 Class2 中对 F 的调用，而省略 Class3 中对 F 的调用。

示例结束

在继承链中使用条件方法可能会造成混淆。通过 base 对条件方法进行的调用（形式为 base.M）遵循正常的条件方法调用规则。

示例：在以下代码中

```
// File Class1.cs
using System.Diagnostics;
class Class1
{
    [Conditional("DEBUG")]
    public virtual void M() => Console.WriteLine("Class1.M executed");
}

// File Class2.cs
class Class2 : Class1
{
    public override void M()
    {
        Console.WriteLine("Class2.M executed");
        base.M(); // base.M is not called!
    }
}
```

// File Class3.cs
#define DEBUG
class Class3
{
    public static void Main()
    {
        Class2 c = new Class2();
        c.M(); // M is called
    }
}

Class2 包含对其基类中定义的 M 的调用。由于基方法是有条件的，取决于符号 DEBUG 的存在，而该符号未定义，因此此调用被省略。因此，该方法仅向控制台写入 "Class2.M executed"。合理使用 pp_declarations 可消除此类问题。

*结束示例*

### 22.5.3.3 条件属性类

一个用一个或多个 Conditional 属性装饰的属性类（§22.2）是条件属性类。因此，条件属性类与在其 Conditional 属性中声明的条件编译符号相关联。

示例：

```
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

声明 TestAttribute 为与条件编译符号 ALPHA 和 BETA 相关联的条件属性类。

*结束示例*

条件属性的属性规范（§22.3）如果在其关联的条件编译符号中的一个或多个在规范点被定义则包含，否则属性规范将被省略。

需要注意的是，条件属性类的属性规范的包含或排除由规范点处的条件编译符号控制。

示例：在示例中

```
// File Test.cs
using System.Diagnostics;
[Conditional("DEBUG")]
public class TestAttribute : Attribute {}

// File Class1.cs:
#define DEBUG
[Test] // TestAttribute is specified
class Class1 {}

// File Class2.cs:
#undef DEBUG
[Test] // TestAttribute is not specified
class Class2 {}
```

类 Class1 和 Class2 各自都用属性 Test 装饰，该属性取决于 DEBUG 是否定义而为条件。由于该符号在 Class1 的上下文中定义，但在 Class2 中未定义，因此 Class1 上的 Test 属性规范被包含，而 Class2 上的 Test 属性规范被省略。

*结束示例*

## 22.5.4 Obsolete 属性

Obsolete 属性用于标记不应再使用的类型和类型的成员。

如果程序使用用 Obsolete 属性装饰的类型或成员，编译器应发出警告或错误。具体而言，如果未提供 error 参数，或提供了 error 参数且其值为 false，则编译器应发出警告。如果指定了 error 参数且其值为 true，则编译器应发出错误。

*示例：在以下代码中*

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
    static void Main()
    {
        A a = new A(); // Warning
        a.F();
    }
}
```

类 A 用 Obsolete 属性装饰。Main 中对 A 的每次使用都会导致发出警告，其中包含指定的消息，"This class is obsolete; use class B instead"。

*结束示例*

## 22.5.5 调用者信息属性

### 22.5.5.1 通用

为了日志记录和报告等目的，有时函数成员获取有关调用代码的某些编译时信息是有用的。调用者信息属性提供了一种透明地传递此类信息的方式。

当可选参数用其中一个调用者信息属性注释时，在调用中省略相应的参数不一定会导致使用默认参数值代替。相反，如果有关调用上下文的指定信息可用，则该信息将作为参数值传递。

示例：

```
public void Log(
[CallerLineNumber] int line = -1,
[CallerFilePath] string path = null,
[CallerMemberName] string name = null
)
{
Console.WriteLine((line < 0) ? "No line" : "Line " + line);
Console.WriteLine((path == null) ? "No file path" : path);
Console.WriteLine((name == null) ? "No member name" : name);
}
```

对 Log() 的无参数调用将打印调用的行号和文件路径，以及发生调用的成员的名称。

结束示例

调用者信息属性可以出现在任何地方的可选参数上，包括委托声明中。然而，特定的调用者信息属性对它们可以标注的参数类型有限制，因此从替换值到参数类型的隐式转换始终存在。

在部分方法声明的定义部分和实现部分的参数上具有相同的调用者信息属性是错误。仅应用定义部分中的调用者信息属性，而仅出现在实现部分中的调用者信息属性将被忽略。

调用者信息不影响重载解析。由于带标注的可选参数在调用者的源代码中仍然被省略，重载解析忽略这些参数的方式与忽略其他省略的可选参数（§12.6.4）相同。

仅当函数在源代码中显式调用时，才会替换调用者信息。隐式调用（如隐式父构造函数调用）没有源位置，不会替换调用者信息。此外，动态绑定的调用也不会替换调用者信息。在此类情况下，如果省略了带调用者信息标注的参数，则使用该参数指定的默认值代替。

一个例外是查询表达式。这些被视为语法扩展，如果它们扩展成的调用省略了带有调用者信息属性的可选参数，则会替换调用者信息。使用的位置是生成该调用的查询子句的位置。

如果在给定参数上指定了多个调用者信息属性，则按以下顺序识别它们：CallerLineNumber、CallerFilePath、CallerMemberName。考虑以下参数声明：

```
[CallerMemberName, CallerFilePath, CallerLineNumber] object p = ...
```

CallerLineNumber 具有优先权，其他两个属性将被忽略。如果省略 CallerLineNumber，则 CallerFilePath 具有优先权，CallerMemberName 将被忽略。这些属性的词法顺序无关紧要。

### 22.5.5.2 CallerLineNumber 属性

属性 System.Runtime.CompilerServices.CallerLineNumberAttribute 允许在可选参数上使用，当存在从常量值 int.MaxValue 到参数类型的标准隐式转换（§10.4.2）时。这确保了任何不超过该值的非负行号都可以无错误地传递。

如果源代码中某位置的函数调用省略了带有 `CallerLineNumberAttribute` 的可选参数，则表示该位置行号的数字字面量将用作调用的参数，而不是默认参数值。

如果调用跨越多行，所选行取决于实现。

行号可能受 `#line` 指令（§6.5.8）影响。

### 22.5.5.3 CallerFilePath 属性

属性 `System.Runtime.CompilerServices.CallerFilePathAttribute` 允许在可选参数上使用，当存在从 `string` 到参数类型的标准隐式转换（§10.4.2）时。

如果源代码中某位置的函数调用省略了带有 `CallerFilePathAttribute` 的可选参数，则表示该位置文件路径的字符串字面量将用作调用的参数，而不是默认参数值。

文件路径的格式取决于实现。

文件路径可能受 `#line` 指令（§6.5.8）影响。

### 22.5.5.4 CallerMemberName 属性

属性 `System.Runtime.CompilerServices.CallerMemberNameAttribute` 允许在可选参数上使用，当存在从 `string` 到参数类型的标准隐式转换（§10.4.2）时。

如果源代码中函数成员体内部或应用于函数成员本身或其返回类型、参数或类型参数的属性内部的某位置的函数调用省略了带有 `CallerMemberNameAttribute` 的可选参数，则表示该成员名称的字符串字面量将用作调用的参数，而不是默认参数值。对于在泛型方法中发生的调用，仅使用方法名本身，不带类型参数列表。对于在显式接口成员实现中发生的调用，仅使用方法名本身，不带前面的接口限定。对于在属性或事件访问器中发生的调用，所使用的成员名称是属性或事件本身的名称。对于在索引器访问器中发生的调用，所使用的成员名称是由索引器成员上的 `IndexerNameAttribute`（§22.6）提供的名称（如果存在），否则为默认名称 `Item`。对于在字段或事件初始化器中发生的调用，所使用的成员名称是正在初始化的字段或事件的名称。对于在实例构造函数、静态构造函数、终结器和运算符声明中发生的调用，所使用的成员名称取决于实现。

## 22.6 用于互操作性的属性

为了与其他语言互操作，索引器可以使用索引属性实现。如果索引器没有 `IndexerName` 属性，则默认使用名称 `Item`。`IndexerName` 属性使开发人员能够覆盖此默认值并指定不同的名称。

> *示例：* 默认情况下，索引器的名称是 `Item`。这可以被覆盖，如下所示：


```csharp
[System.Runtime.CompilerServices.IndexerName("TheItem")]
public int this[int index]
{
    get { ... }
    set { ... }
}
```

现在，该索引器的名称为 TheItem。

*示例结束*

# 23. 不安全代码

### 23.1 概述

不支持不安全代码的实现必须诊断对本条中定义的语法规则的任何使用。

本条其余部分（包括其所有子条）为条件规范性内容。

注意：如前文各条所定义，核心 C# 语言与 C 和 C++ 的显著区别在于它省略了指针作为一种数据类型。相反，C# 提供引用以及创建由垃圾回收器管理的对象的能力。这种设计与其他特性相结合，使 C# 成为一种比 C 或 C++ 安全得多的语言。在核心 C# 语言中，根本不可能出现未初始化的变量、“悬空”指针或索引超出数组边界的表达式。因此，那些经常困扰 C 和 C++ 程序的整类缺陷得以消除。

尽管 C 或 C++ 中几乎每一种指针类型构造在 C# 中都有对应的引用类型，但在某些情况下，仍然必须访问指针类型。例如，与底层操作系统交互、访问内存映射设备或实现时间关键算法，在无法访问指针时可能无法实现或不切实际。为满足这一需求，C# 提供了编写不安全代码的能力。

在不安全代码中，可以声明和操作指针，在指针与整型之间执行转换，获取变量地址，等等。从某种意义上说，编写不安全代码很像在 C# 程序中编写 C 代码。

实际上，从开发人员和用户的角度来看，不安全代码是一种“安全”的特性。不安全代码应使用修饰符 unsafe 清晰标记，这样开发人员就不可能意外使用不安全特性，并且执行引擎会确保不安全代码无法在不受信任的环境中执行。

注意结束

### 23.2 不安全上下文

C# 的不安全特性仅在不安全上下文中可用。可以通过在类型、成员或局部函数的声明中包含 unsafe 修饰符，或通过使用 unsafe_statement 来引入不安全上下文：

- 类、结构、接口或委托的声明可以包含 unsafe 修饰符；在这种情况下，该类型声明的整个文本范围（包括类、结构或接口的主体）被视为不安全上下文。
  注意：如果 type_declaration 是分部声明，则只有该部分是不安全上下文。注意结束
- 字段、方法、属性、事件、索引器、运算符、实例构造函数、终结器、静态构造函数或局部函数的声明可以包含 unsafe 修饰符；在这种情况下，该成员声明的整个文本范围被视为不安全上下文。

- *unsafe_statement* 允许在 *block* 内使用不安全上下文。关联的 *block* 的整个文本范围被视为不安全上下文。在不安全上下文中声明的局部函数本身也是不安全的。

相关的语法扩展如下所示，并在后续子条中给出。

```
~~~
unsafe_modifier
    : 'unsafe'
    ;

unsafe_statement
    : 'unsafe' block
    ;
~~~
```

*示例：* 在以下代码中

```
~~~csharp
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
~~~
```

结构声明中指定的 `unsafe` 修饰符使该结构声明的整个文本范围成为不安全上下文。因此，可以将 `Left` 和 `Right` 字段声明为指针类型。上面的示例也可以写成

```
~~~csharp
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
~~~
```

这里，字段声明中的 `unsafe` 修饰符使这些声明被视为不安全上下文。

*示例结束*

除了建立不安全上下文从而允许使用指针类型之外，`unsafe` 修饰符对类型或成员没有影响。

*示例：* 在以下代码中

```
~~~csharp
public class A
{
    public unsafe virtual void F()
    {
        char* p;
        ...
    }
}

public class B : A
{
    public override void F()
    {
        base.F();
        ...
    }
}
~~~
```

A 中 F 方法上的 unsafe 修饰符只是使 F 的文本范围成为不安全上下文，在该上下文中可以使用该语言的不安全特性。在 B 中对 F 的重写中，无需重新指定 unsafe 修饰符——当然，除非 B 中的 F 方法本身需要访问不安全特性。

当指针类型是方法签名的一部分时，情况略有不同

```
public unsafe class A
{
    public virtual void F(char* p) {...}
}

public class B: A
{
    public unsafe override void F(char* p) {...}
}
```

这里，由于 F 的签名包含指针类型，因此它只能在不安全上下文中编写。不过，不安全上下文可以通过使整个类成为不安全类（如 A 中的情况）来引入，也可以通过在该方法声明中包含 unsafe 修饰符（如 B 中的情况）来引入。

示例结束

当 unsafe 修饰符用于分部类型声明（§15.2.7）时，只有该特定部分被视为不安全上下文。

### 23.3 指针类型

在不安全上下文中，类型（§8.1）可以是 pointer_type，也可以是 value_type、reference_type 或 type_parameter。在不安全上下文中，pointer_type 还可以是数组（§17）的元素类型。pointer_type 也可以在不安全上下文之外的 typeof 表达式中使用（§12.8.17）（因为这种用法并不不安全）。

pointer_type 写为 unmanaged_type（§8.8）或关键字 void，后跟一个 * 标记：

```
pointer_type
  : value_type ('*')+
  | 'void' ('*')+
  ;
```

指针类型中 * 之前指定的类型称为该指针类型的指向类型。它表示该指针类型的值所指向的变量的类型。

pointer_type 只能在不安全上下文中用于 array_type（§23.2）。non_array_type 是本身不是 array_type 的任何类型。

与引用（引用类型的值）不同，指针不受垃圾回收器跟踪——垃圾回收器不知道指针及其指向的数据。因此，不允许指针指向引用或包含引用的结构，并且指针的指向类型应为 unmanaged_type。指针类型本身是非托管类型，因此指针类型可以用作另一个指针类型的指向类型。

混合使用指针和引用的直观规则是：引用的指向对象（对象）可以包含指针，但指针的指向对象不允许包含引用。

示例：下表给出了一些指针类型的示例：

| 示例 | 描述 |
|---|---|
| `byte*` | 指向 `byte` 的指针 |
| `char*` | 指向 `char` 的指针 |
| `int**` | 指向 `int` 的指针的指针 |
| `int*[]` | 指向 `int` 的指针的一维数组 |
| `void*` | 指向未知类型的指针 |

示例结束

对于给定的实现，所有指针类型应具有相同的大小和表示形式。

注意：与 C 和 C++ 不同，在同一声明中声明多个指针时，在 C# 中 * 只与基础类型一起书写，而不作为每个指针名称的前缀标点符号。例如：

```
int* pi, pj; // NOT as int *pi, *pj;
```

注意结束

类型为 T* 的指针的值表示类型为 T 的变量的地址。可以使用指针间接寻址运算符 *（§23.6.2）来访问该变量。

示例：给定类型为 int* 的变量 P，表达式 *P 表示位于 P 所含地址处的 int 变量。示例结束

与对象引用一样，指针可以为 null。对值为 null 的指针应用间接寻址运算符会导致实现定义的行为（§23.6.2）。值为 null 的指针由全零位表示。

void* 类型表示指向未知类型的指针。由于指向类型未知，因此不能对 void* 类型的指针应用间接寻址运算符，也不能对此类指针执行任何算术运算。但是，void* 类型的指针可以强制转换为任何其他指针类型（反之亦然），并可以与其他指针类型的值进行比较（§23.6.8）。

指针类型是单独的一类类型。与引用类型和值类型不同，指针类型不继承自 object，并且指针类型与 object 之间不存在转换。特别是，指针不支持装箱和拆箱（§8.3.13）。但是，允许在不同指针类型之间以及指针类型与整型之间进行转换。这将在 §23.5 中描述。

pointer_type 不能用作类型实参（§8.4），并且对于本应将类型实参推断为指针类型的泛型方法调用，类型推断（§12.6.3）会失败。

pointer_type 不能用作动态绑定操作（§12.2.3）的子表达式的类型。

pointer_type 不能用作扩展方法（§15.6.10）中第一个参数的类型。

pointer_type 可以用作 volatile 字段的类型（§15.5.4）。

类型 E* 的动态擦除是以下指针类型：其指向类型为 E 的动态擦除。

具有指针类型的表达式不能用于在 anonymous_object_creation_expression（§12.8.16.7）内的 member_declarator 中提供值。

任何指针类型的默认值（§9.3）都是 null。




Note: Although pointers can be passed as in, ref or out parameters, doing so can cause undefined behavior, since the pointer might well be set to point to a local variable that no longer exists when the called method returns, or the fixed object to which it used to point, is no longer fixed. For example:

```
class Test
{
    static int value = 20;

    unsafe static void F(out int* pi1, ref int* pi2)
    {
        int i = 10;
        pi1 = &i;    // return address of local variable
        fixed (int* pj = &value)
        {
            // ...
            pi2 = pj;  // return address that will soon not be fixed
        }
    }

    static void Main()
    {
        int i = 15;
        unsafe
        {
            int* px1;
            int* px2 = &i;
            F(out px1, ref px2);
            int v1 = *px1; // undefined
            int v2 = *px2; // undefined
        }
    }
}
```

结束注释

A method can return a value of some type, and that type can be a pointer.

示例：当给定指向连续整数序列的指针、该序列的元素计数以及另一个整数值时，以下方法如果匹配则返回该序列中该值的地址；否则返回 null：

```
unsafe static int* Find(int* pi, int size, int value)
{
    for (int i = 0; i < size; ++i)
    {
        if (*pi == value)
        {
            return pi;
        }
        ++pi;
    }
    return null;
}
```

结束示例

在不安全上下文中，有多个构造可用于操作指针：

- 一元 * 运算符可用于执行指针间接寻址 (§23.6.2)。
- -> 运算符可用于通过指针访问结构体的成员 (§23.6.3)。
- [] 运算符可用于索引指针 (§23.6.4)。
- 一元 & 运算符可用于获取变量的地址 (§23.6.5)。
- ++ 和 -- 运算符可用于递增和递减指针 (§23.6.6)。
- 二元 + 和 - 运算符可用于执行指针算术 (§23.6.7)。
- ==、!=、<、>、<= 和 >= 运算符可用于比较指针 (§23.6.8)。
- stackalloc 运算符可用于从调用栈分配内存 (§23.9)。
- fixed 语句可用于临时固定变量以便获取其地址 (§23.7)。

## 23.4 固定变量和可移动变量

取地址运算符 (§23.6.5) 和 fixed 语句 (§23.7) 将变量分为两类：固定变量和可移动变量。

固定变量驻留在不受垃圾回收器操作影响的存储位置。（固定变量的示例包括局部变量、值参数以及通过解引用指针创建的变量。）另一方面，可移动变量驻留在可能被垃圾回收器重新定位或释放的存储位置。（可移动变量的示例包括对象中的字段和数组的元素。）

& 运算符 (§23.6.5) 允许在无限制的情况下获取固定变量的地址。然而，由于可移动变量可能被垃圾回收器重新定位或释放，可移动变量的地址只能使用 fixed 语句 (§23.7) 获取，并且该地址仅在该 fixed 语句的持续时间内有效。

精确地说，固定变量是以下之一：

- 由 simple_name (§12.8.4) 产生的变量，该 simple_name 引用局部变量、值参数或参数数组，除非该变量被匿名函数捕获 (§12.19.6.2)。
- 由 member_access (§12.8.7) 产生的变量，其形式为 V.I，其中 V 是 struct_type 的固定变量。
- 由 pointer_indirection_expression (§23.6.2) 产生的变量，其形式为 *P，或由 pointer_member_access (§23.6.3) 产生的变量，其形式为 P->I，或由 pointer_element_access (§23.6.4) 产生的变量，其形式为 P[E]。

所有其他变量均被归类为可移动变量。

静态字段被归类为可移动变量。此外，in、out 或 ref 参数被归类为可移动变量，即使为该参数提供的参数是固定变量。最后，通过解引用指针产生的变量始终被归类为固定变量。

```
double d = 123.456e23;
unsafe
{
    byte* pb = (byte*)&d;
    for (int i = 0; i < sizeof(double); ++i)
    {
        Console.Write($" {pb++:X2}");
    }
    Console.WriteLine();
}
```

当然，产生的输出取决于字节序。一个可能性是 " BA FF 51 A2 90 6C 24 45"。

*结束示例*

指针与整数之间的映射是实现定义的。

*注意：* 然而，在具有线性地址空间的 32 位和 64 位 CPU 架构上，指针与整数类型之间的转换通常与 uint 或 ulong 值分别与这些整数类型之间的转换完全相同。 *结束注释*

### 23.5.2 指针数组

在不安全上下文中，可以使用 array_creation_expression (§12.8.16.5) 构造指针数组。仅允许对指针数组应用适用于其他数组类型的部分转换：

- 从任何 array_type 到 System.Array 及其实现的接口的隐式引用转换 (§10.2.8) 也适用于指针数组。然而，通过 System.Array 或其实现的接口访问数组元素可能在运行时导致异常，因为指针类型不能转换为 object。
- 从单维数组类型 S[] 到 System.Collections.Generic.IList<T> 及其泛型基接口的隐式和显式引用转换 (§10.2.8, §10.3.5) 从不适用于指针数组。
- 从 System.Array 及其实现的接口到任何 array_type 的显式引用转换 (§10.3.5) 适用于指针数组。
- 从 System.Collections.Generic.IList<S> 及其基接口到单维数组类型 T[] 的显式引用转换 (§10.3.5) 从不适用于指针数组，因为指针类型不能用作类型参数，并且指针类型到非指针类型的转换不存在。

这些限制意味着 §9.4.4.17 中描述的对数组的 foreach 语句的展开不能应用于指针数组。相反，形式为

```
foreach (V v in x) embedded_statement
```

其中 x 的类型是形式为 T[, ,..., ] 的数组类型，n 是维度数减 1，且 T 或 V 是指针类型，则使用嵌套 for 循环展开如下：

```
{
    T[, ,..., ] a = x;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
    {
        for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
        {
            ...
            for (int in = a.GetLowerBound(n); in <= a.GetUpperBound(n); in++)
            {
                V v = (V)a[i0,i1,...,in];
                *embedded_statement*
            }
        }
    }
}
```

变量 a、i0、i1、... in 对 x、embedded_statement 或程序的任何其他源代码不可见或不可访问。变量 v 在嵌入语句中是只读的。如果不存在从 T（元素类型）到 V 的显式转换 (§23.5)，则会产生错误且不进行后续步骤。如果 x 的值为 null，则在运行时抛出 System.NullReferenceException。

注意：尽管指针类型不允许用作类型参数，但指针数组可作为类型参数使用。 结束注释

## 23.6 表达式中的指针

### 23.6.1 通用

在不安全上下文中，表达式可能产生指针类型的结果，但在不安全上下文之外，表达式为指针类型是编译时错误。精确地说，在不安全上下文之外，如果任何 simple_name (§12.8.4)、member_access (§12.8.7)、invocation_expression (§12.8.9) 或 element_access (§12.8.11) 为指针类型，则会发生编译时错误。

在不安全上下文中，primary_no_array_creation_expression (§12.8) 和 unary_expression (§12.9) 产生式允许额外的构造，这些构造在以下小节中描述。

注意：不安全运算符的优先级和结合性由语法隐含。 结束注释

### 23.6.2 指针间接寻址

pointer_indirection_expression 由星号 (*) 后跟 unary_expression 组成。

```
pointer_indirection_expression
    : '*' unary_expression
    ;
```

一元 * 运算符表示指针间接寻址，用于获取指针指向的变量。计算 *p 的结果，其中 p 是指针类型 T* 的表达式，是类型为 T 的变量。对类型为 void* 的表达式或非指针类型的表达式应用一元 * 运算符是编译时错误。

对空值指针应用一元 * 运算符的效果是实现定义的。特别是，不能保证此操作会抛出 System.NullReferenceException。

如果为指针分配了无效值，则一元 * 运算符的行为未定义。

注意：在通过一元 * 运算符解引用指针时，无效值包括为指向的类型不当对齐的地址（参见 §23.5 中的示例），以及变量生命周期结束后的地址。



为了确定性赋值分析的目的，通过求值形式为 `*P` 的表达式产生的变量被认为初始已赋值 (§9.4.2)。

## 23.6.3 指针成员访问

*pointer_member_access 由 primary_expression 组成，其后跟 “->” 标记，其后跟一个标识符和一个可选的 type_argument_list。*

```
pointer_member_access
    : primary_expression '->' identifier type_argument_list?
    ;
```

在形式为 P->I 的指针成员访问中，P 必须是一个指针类型的表达式，而 I 必须表示 P 所指向的类型的一个可访问成员。

形式为 P->I 的指针成员访问的求值结果与 `(*P).I` 完全相同。有关指针间接运算符 `(*)` 的描述，请参阅 §23.6.2。有关成员访问运算符 `(.)` 的描述，请参阅 §12.8.7。

*示例：* 在下面的代码中

```
struct Point
{
    public int x;
    public int y;
    public override string ToString() => $"({x},{y})";
}

class Test
{
    static void Main()
    {
        Point point;
        unsafe
        {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

`->` 运算符用于通过指针访问结构体的字段并调用其方法。由于操作 `P->I` 与 `(*P).I` 精确等价，`Main` 方法同样可以写成：

```
class Test
{
    static void Main()
    {
        Point point;
        unsafe
        {
            Point* p = &point;
            (*p).x = 10;
            (*p).y = 20;
            Console.WriteLine((*p).ToString());
        }
    }
}
```

*结束示例*

## 23.6.4 指针元素访问

pointer_element_access 由 primary_no_array_creation_expression 组成，其后跟用 "[" 和 "]" 括起来的表达式。

```
pointer_element_access
    : primary_no_array_creation_expression '[' expression ']'
    ;
```

在形式为 P[E] 的指针元素访问中，P 必须是一个除 void* 外的指针类型的表达式，而 E 必须是可以隐式转换为 int、uint、long 或 ulong 的表达式。

形式为 P[E] 的指针元素访问的求值结果与 *(P + E) 完全相同。有关指针间接运算符 (*) 的描述，请参阅 §23.6.2。有关指针加法运算符 (+) 的描述，请参阅 §23.6.7。

*示例：在下面的代码中*

```
class Test
{
    static void Main()
    {
        unsafe
        {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++)
            {
                p[i] = (char)i;
            }
        }
    }
}
```

指针元素访问用于在 for 循环中初始化字符缓冲区。由于操作 P[E] 与 *(P + E) 精确等价，该示例同样可以写成：

```
class Test
{
    static void Main()
    {
        unsafe
        {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++)
            {
                *(p + i) = (char)i;
            }
        }
    }
}
```

*结束示例*

指针元素访问运算符不检查越界错误，访问越界元素时的行为是未定义的。

> Note: 这与 C 和 C++ 相同。 end note

## 23.6.5 取地址运算符

addressof_expression 由一个与号 (&) 组成，其后跟一个 unary_expression。

```
addressof_expression
  : '&' unary_expression
  ;
```

给定一个类型为 T 且被归类为固定变量 (§23.4) 的表达式 E，构造 &E 计算由 E 给出的变量的地址。结果的类型为 T*，并被归类为值。如果 E 未被归类为变量，如果 E 被归类为只读局部变量，或如果 E 表示一个可移动变量，则会发生编译时错误。在最后一种情况下，可以使用 fixed 语句 (§23.7) 在获取其地址之前暂时“固定”该变量。

> Note: 如 §12.8.7 所述，在定义了 readonly 字段的结构体或类的实例构造函数或静态构造函数之外，该字段被视为值，而不是变量。因此，其地址不能被获取。同样，常量的地址也不能被获取。

& 运算符不要求其参数已确定性赋值，但在 & 操作之后，运算符所应用的变量在该操作发生的执行路径中被认为已确定性赋值。确保在此情况下变量确实得到正确初始化是程序员的责任。

示例：在下面的代码中

```
class Test
{
    static void Main()
    {
        int i;
        unsafe
        {
            int* p = &i;
            *p = 123;
        }
        Console.WriteLine(i);
    }
}
```

在使用 &i 操作初始化 p 之后，i 被认为已确定性赋值。对 *p 的赋值实际上初始化了 i，但包含此初始化是程序员的责任，如果删除该赋值也不会发生编译时错误。

*结束示例*

> Note: & 运算符的确定性赋值规则的存在是为了避免局部变量的冗余初始化。例如，许多外部 API 接受指向由 API 填充的结构体的指针。对此类 API 的调用通常传递局部结构体变量的地址，而没有该规则，则需要对结构体变量进行冗余初始化。 end note

Note: 当局部变量、值参数或参数数组被匿名函数 (§12.8.23) 捕获时，该局部变量、参数或参数数组不再被视为固定变量 (§23.7)，而是被视为可移动变量。因此，对于任何不安全代码来说，获取已被匿名函数捕获的局部变量、值参数或参数数组的地址都是错误。 End note

## 23.6.6 指针递增和递减

在不安全上下文中，++ 和 -- 运算符 (§12.8.15 和 §12.9.6) 可以应用于除 void* 外的所有类型的指针变量。因此，对于每个指针类型 T*，以下运算符被隐式定义：

```
T* operator ++(T* x);
T* operator --(T* x);
```

这些运算符分别产生与 x+1 和 x-1 相同的结果 (§23.6.7)。换句话说，对于类型为 T* 的指针变量，++ 运算符将 sizeof(T) 加到变量中包含的地址上，而 -- 运算符将 sizeof(T) 从变量中包含的地址上减去。

如果指针递增或递减操作溢出了指针类型的域，结果是实现定义的，但不会产生异常。

## 23.6.7 指针算术

在不安全上下文中，+ 运算符 (§12.10.5) 和 - 运算符 (§12.10.6) 可以应用于除 void* 外的所有指针类型的值。因此，对于每个指针类型 T*，以下运算符被隐式定义：

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

给定一个指针类型 T* 的表达式 P 和一个类型为 int、uint、long 或 ulong 的表达式 N，表达式 P + N 和 N + P 计算的类型为 T* 的指针值，该值是通过将 N * sizeof(T) 加到 P 给出的地址上得到的。同样，表达式 P - N 计算的类型为 T* 的指针值，该值是通过从 P 给出的地址上减去 N * sizeof(T) 得到的。

给定两个指针类型 T* 的表达式 P 和 Q，表达式 P - Q 计算 P 和 Q 给出的地址之间的差值，然后将该差值除以 sizeof(T)。结果的类型始终为 long。实际上，P - Q 计算为 ((long)(P) - (long)(Q)) / sizeof(T)。

示例：

```
class Test
{
    static void Main()
    {
        unsafe
        {



```csharp
int* values = stackalloc int[20];
int* p = &values[1];
int* q = &values[15];
Console.WriteLine($"p - q = {p - q}");
Console.WriteLine($"q - p = {q - p}");
}
}
```

其产生的输出为：

p - q = -14
q - p = 14

*结束示例*

如果指针算术运算溢出了指针类型的域，则结果会以实现定义的方式被截断，但不会产生异常。

## 23.6.8 指针比较

在不安全上下文中，==、!=、<、>、<= 和 >= 运算符 (§12.12) 可应用于所有指针类型的值。指针比较运算符如下：

```csharp
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

由于存在从任何指针类型到 void* 类型的隐式转换，任何指针类型的操作数都可以使用这些运算符进行比较。比较运算符将两个操作数给出的地址作为无符号整数进行比较。

## 23.6.9 sizeof 运算符

对于某些预定义类型 (§12.8.18)，sizeof 运算符会产生一个常量 int 值。对于所有其他类型，sizeof 运算符的结果是实现定义的，并被归类为值，而不是常量。

成员被打包到 struct 中的顺序是不确定的。

出于对齐目的，struct 的开头、struct 内部以及 struct 的末尾可能存在未命名的填充。用作填充的位的内容是不确定的。

当应用于具有 struct 类型操作数时，结果是该类型变量中的总字节数，包括任何填充。

## 23.7 fixed 语句

在不安全上下文中，embedded_statement (§13.1) 产生式允许一种额外的构造，即 fixed 语句，用于“固定”一个可移动变量，使其地址在语句持续期间保持不变。

```
fixed_statement
    : 'fixed' '(' pointer_type fixed_pointer_declarators ')' embedded_statement
    ;
```

```
fixed_pointer_declarators
  : fixed_pointer_declarator (','  fixed_pointer_declarator)*
  ;
```

```
fixed_pointer_declarator
  : identifier '=' fixed_pointer_initializer
  ;
```

```
fixed_pointer_initializer
  : '&' variable_reference
  | expression
  ;
```

每个 fixed_pointer_declarator 声明给定 pointer_type 的局部变量，并使用相应的 fixed_pointer_initializer 计算出的地址初始化该局部变量。在 fixed 语句中声明的局部变量可在该变量声明右侧出现的任何 fixed_pointer_initializers 中访问，也可在 fixed 语句的 embedded_statement 中访问。由 fixed 语句声明的局部变量被视为只读。如果 embedded 语句尝试修改此局部变量（通过赋值或 ++ 和 -- 运算符）或将其作为 ref 或 out 参数传递，则会发生编译时错误。

在 fixed_pointer_initializer 中使用捕获的局部变量 (§12.19.6.2)、值参数或参数数组是错误的。fixed_pointer_initializer 可以是以下之一：

- 标记“&”后跟对一个不可管理类型 T 的可移动变量 (§23.4) 的 variable_reference (§9.5)，前提是类型 T* 可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算给定变量的地址，并且该变量在 fixed 语句持续期间保证保持在固定地址。
- 一个元素为不可管理类型 T 的 array_type 的表达式，前提是类型 T* 可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算数组中第一个元素的地址，并且整个数组在 fixed 语句持续期间保证保持在固定地址。如果数组表达式为 null 或数组元素数为零，则初始化器计算的地址等于零。
- 类型为 string 的表达式，前提是类型 char* 可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算字符串中第一个字符的地址，并且整个字符串在 fixed 语句持续期间保证保持在固定地址。如果字符串表达式为 null，则 fixed 语句的行为是实现定义的。
- 类型不是 array_type 或 string 的表达式，前提是存在一个可访问的方法或可访问的扩展方法，其签名匹配 ref [readonly] T GetPinnableReference()，其中 T 是 unmanaged_type，并且 T* 可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算返回变量的地址，并且该变量在 fixed 语句持续期间保证保持在固定地址。当重载解析 (§12.6.4) 产生恰好一个函数成员并且该函数成员满足前述条件时，GetPinnableReference() 方法可被 fixed 语句使用。GetPinnableReference 方法应返回对等于零的地址的引用，例如当没有数据需要固定时由 System.Runtime.CompilerServices.Unsafe.NullRef<T>() 返回的引用。
- 一个引用可移动变量的固定大小缓冲区成员的 simple name 或 member_access，前提是固定大小缓冲区成员的类型可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算固定大小缓冲区 (§23.8.3) 的第一个元素的指针，并且固定大小缓冲区在 fixed 语句持续期间保证保持在固定地址。

对于 fixed_pointer_initializer 计算出的每个地址，fixed 语句确保在 fixed 语句持续期间，被地址引用的变量不会被垃圾回收器重新定位或释放。

*示例：如果 fixed_pointer_initializer 计算出的地址引用了对象的一个字段或数组实例的一个元素，则 fixed 语句保证在语句的生命周期内，包含的对象实例不会被重新定位或释放。结束示例*

程序员有责任确保由 fixed 语句创建的指针不会在这些语句执行结束后继续存在。

*示例：当由 fixed 语句创建的指针被传递给外部 API 时，程序员有责任确保 API 不会保留这些指针的记忆。结束示例*

固定的对象会导致堆碎片化（因为它们不能被移动）。因此，对象只有在绝对必要时才应被固定，并且只应固定最短的时间。

*示例：示例*

```csharp
class Test
{
    static int x;
    int y;

    unsafe static void F(int* p)
    {
        *p = 1;
    }

    static void Main()
    {
        Test t = new Test();
        int[] a = new int[10];
        unsafe
        {
            fixed (int* p = &x) F(p);
            fixed (int* p = &t.y) F(p);
            fixed (int* p = &a[0]) F(p);
            fixed (int* p = a) F(p);
        }
    }
}
```

演示了 fixed 语句的几种用法。第一个语句固定并获取静态字段的地址，第二个语句固定并获取实例字段的地址，第三个语句固定并获取数组元素的地址。在每种情况下，使用常规 & 运算符都会是错误，因为所有变量都被归类为可移动变量。

上面的示例中第三个和第四个 fixed 语句产生相同的结果。一般而言，对于数组实例 a，在 fixed 语句中指定 a[0] 与简单指定 a 相同。

*结束示例*

在不安全上下文中，单维数组的数组元素按递增索引顺序存储，从索引 0 开始，到索引 Length - 1 结束。对于多维数组，数组元素以这样的方式存储：最右维的索引先增加，然后是下一个左维，依此类推向左。

在获取指向数组实例 a 的指针 p 的 fixed 语句中，从 p 到 p + a.Length - 1 的指针值表示数组中元素的地址。同样，从 p[0] 到 p[a.Length - 1] 的变量表示实际的数组元素。鉴于数组的存储方式，任何维度的数组都可以被视为线性。

### 示例：

```csharp
class Test
{
    static void Main()
    {
        int[,,] a = new int[2,3,4];
        unsafe
        {
            fixed (int* p = a)
            {
                for (int i = 0; i < a.Length; ++i) // treat as linear
                {
                    p[i] = i;
                }
            }
        }
        for (int i = 0; i < 2; ++i)
        {
            for (int j = 0; j < 3; ++j)
            {
                for (int k = 0; k < 4; ++k)
                {
                    Console.Write($"[{i},{j},{k}] = {a[i,j,k],2} ");
                }
                Console.WriteLine();
            }
        }
    }
}
```

其产生的输出为：

[0,0,0] = 0 [0,0,1] = 1 [0,0,2] = 2 [0,0,3] = 3
[0,1,0] = 4 [0,1,1] = 5 [0,1,2] = 6 [0,1,3] = 7
[0,2,0] = 8 [0,2,1] = 9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23

*结束示例*

示例：在以下代码中

```csharp
class Test
{
```



unsafe static void Fill(int* p, int count, int value)
{
    for (; count != 0; count--)
    {
        *p++ = value;
    }
}

static void Main()
{
    int[] a = new int[100];
    unsafe
    {
        fixed (int* p = a) Fill(p, 100, -1);
    }
}

fixed 语句用于固定一个数组，以便其地址可以传递给接受指针的方法。

示例结束

通过固定字符串实例产生的 char* 值始终指向以 null 结尾的字符串。在获取指向字符串实例 s 的指针 p 的 fixed 语句中，从 p 到 p + s.Length - 1 范围内的指针值表示字符串中字符的地址，而指针值 p + s.Length 始终指向一个 null 字符（值为 '\0' 的字符）。

## 示例：

```
class Test
{
    static string name = "xx";

    unsafe static void F(char* p)
    {
        for (int i = 0; p[i] != '\0'; ++i)
        {
            System.Console.WriteLine(p[i]);
        }
    }

    static void Main()
    {
        unsafe
        {
            fixed (char* p = name) F(p);
            fixed (char* p = "xx") F(p);
        }
    }
}
```

示例结束

示例：以下代码展示了 fixed_pointer_initializer，其表达式的类型不是 array_type 或 string：

```
public class C
{
    private int _value;
    public C(int value) => _value = value;
    public ref int GetPinnableReference() => ref _value;
}

public class Test
{
    unsafe private static void Main()
    {
        C c = new C(10);
        fixed (int* p = c)
        {
            // ...
        }
    }
}
```

类型 C 具有可访问的 GetPinnableReference 方法，其签名正确。在 fixed 语句中，当在 c 上调用该方法时返回的 ref int 用于初始化 int* 指针 p。示例结束

通过固定指针修改托管类型的对象可能导致未定义行为。

注意：例如，由于字符串是不可变的，因此程序员有责任确保指向固定字符串的指针所引用的字符不会被修改。注释结束

注意：字符串的自动空终止在调用期望“C 风格”字符串的外部 API 时特别方便。注意，然而，字符串实例允许包含 null 字符。如果存在此类 null 字符，则在将其视为以 null 结尾的 char* 处理时，字符串将显示为被截断。注释结束

## 23.8 固定大小缓冲区

### 23.8.1 通用

固定大小缓冲区用于将“C 风格”的内联数组声明为结构体的成员，主要用于与非托管 API 接口。

### 23.8.2 固定大小缓冲区声明

固定大小缓冲区是表示给定类型变量的定长缓冲区存储的成员。固定大小缓冲区声明引入一个或多个给定元素类型的固定大小缓冲区。

注意：像数组一样，固定大小缓冲区可以被认为包含元素。因此，数组定义的术语元素类型也用于固定大小缓冲区。注释结束

固定大小缓冲区仅允许在结构体声明中使用，并且只能在 unsafe 上下文中出现（§23.2）。

```
fixed_size_buffer_declaration
: attributes? fixed_size_buffer_modifier* 'fixed' buffer_element_type
  fixed_size_buffer_declarators ';'

fixed_size_buffer_modifier
```

```
: 'new'
| 'public'
| 'internal'
| 'private'
| 'unsafe'
;
```

```
buffer_element_type
: type
;
```

```
fixed_size_buffer_declarators
: fixed_size_buffer_declarator (',' fixed_size_buffer_declarator)*
;
```

```
fixed_size_buffer_declarator
: identifier '[' constant_expression ']'
;
```

固定大小缓冲区声明可以包含一组属性（§22）、new 修饰符（§15.3.5）、与结构体成员允许的声明访问性相对应的访问修饰符（§16.4.3）以及 unsafe 修饰符（§23.2）。属性和修饰符适用于固定大小缓冲区声明声明的所有成员。固定大小缓冲区声明中同一修饰符出现多次是错误。

固定大小缓冲区声明不允许包含 static 修饰符。

固定大小缓冲区声明的缓冲区元素类型指定声明引入的缓冲区（s）的元素类型。缓冲区元素类型应为预定义类型 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 bool 之一。

缓冲区元素类型后面跟着一个固定大小缓冲区声明符列表，每个声明符引入一个新的成员。固定大小缓冲区声明符由标识成员的名称的标识符组成，后跟用 [ 和 ] 标记括起来的常量表达式。常量表达式表示该固定大小缓冲区声明符引入的成员中的元素数。常量表达式的类型应可隐式转换为 int 类型，且值应为非零正整数。

固定大小缓冲区的元素应在内存中顺序布局。

声明多个固定大小缓冲区的固定大小缓冲区声明等价于使用相同属性和元素类型的单个固定大小缓冲区声明的多个声明。

*示例：*

```
unsafe struct A
{
    public fixed int x[5], y[10], z[100];
}
```

等价于

```
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```

*示例结束*

### 23.8.3 表达式中的固定大小缓冲区

固定大小缓冲区成员的成员查找（§12.5）与字段的成员查找完全相同。

固定大小缓冲区可以通过 simple_name（§12.8.4）、member_access（§12.8.7）或 element_access（§12.8.11）引用在表达式中使用。

当固定大小缓冲区成员作为简单名称引用时，其效果与形式为 this.I 的成员访问相同，其中 I 是固定大小缓冲区成员。

在形式为 E.I 的成员访问中，其中 E 可能是隐式的 this，如果 E 是结构体类型并且在该结构体类型中对 I 的成员查找识别出一个固定大小成员，则 E.I 的求值和分类如下：

- 如果表达式 E.I 未在 unsafe 上下文中出现，则会发生编译时错误。
- 如果 E 被分类为值，则会发生编译时错误。
- 否则，如果 E 是可移动变量（§23.4），则：
  - 如果表达式 E.I 是 fixed_pointer_initializer（§23.7），则表达式的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针。
  - 否则如果表达式 E.I 是 element_access（§12.8.11）中形式为 E.I[J] 的 primary_no_array_creation_expression（§12.8.11.1），则 E.I 的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针 P，并且封闭的 element_access 然后被求值作为指针元素访问（§23.6.4）P[J]。
  - 否则会发生编译时错误。
- 否则，E 引用一个固定变量，表达式的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针。结果的类型为 S*，其中 S 是 I 的元素类型，并被分类为值。

固定大小缓冲区的后续元素可以使用从第一个元素的指针操作进行访问。与数组访问不同，固定大小缓冲区元素的访问是 unsafe 操作且不进行范围检查。

示例：以下声明并使用了一个具有固定大小缓冲区成员的结构体。

```
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize)
    {
        int len = s.Length;
        if (len > bufSize)
        {
            len = bufSize;
        }
        for (int i = 0; i < len; i++)
        {
            buffer[i] = s[i];
        }
        for (int i = len; i < bufSize; i++)
        {
            buffer[i] = (char)0;
        }
    }
    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

*示例结束*

### 23.8.4 确定性赋值检查

固定大小缓冲区不受确定性赋值检查（§9.4）的约束，并且固定大小缓冲区成员在结构体类型变量的确定性赋值检查中被忽略。

当固定大小缓冲区成员的最外层包含的结构体变量是静态变量、类实例的实例变量或数组元素时，固定大小缓冲区的元素会自动初始化为其默认值（§9.3）。在所有其他情况下，固定大小缓冲区的初始内容是未定义的。

## 23.9 栈分配

请参阅 §12.8.21 了解 stackalloc 操作符的一般信息。在此，讨论该操作符产生指针的能力。

在 unsafe 上下文中，如果 stackalloc_expression（§12.8.21）作为 local_variable_declaration（§13.6.2）的初始化表达式出现，其中 local_variable_type 为指针类型（§23.3）或推断（var），则 stackalloc_expression 的结果是指向已分配块开头的类型为 T * 的指针，其中 T 是 stackalloc_expression 的 unmanaged_type。

在所有其他方面，unsafe 上下文中 local_variable_declarations（§13.6.2）和 stackalloc_expressions（§12.8.21）的语义遵循为安全上下文定义的语义。

*示例：*

```
unsafe
{
    // Memory uninitialized
    int* p1 = stackalloc int[3];
    // Memory initialized
    int* p2 = stackalloc int[3] { -10, -15, -30 };
    // Type int is inferred
    int* p3 = stackalloc[] { 11, 12, 13 };
    // Can't infer context, so pointer result assumed
    var p4 = stackalloc[] { 11, 12, 13 };
    // Error: no conversion exists
    long* p5 = stackalloc[] { 11, 12, 13 };
    // Converts 11 and 13, and returns long*
}
```




```
long* p6 = stackalloc[] { 11, 12L, 13 };
// Converts all and returns long*
long* p7 = stackalloc long[] { 11, 12, 13 };
}
```

*示例结束*

与访问数组或 Span<T> 类型的 stackalloc 分配块不同，访问指针类型的 stackalloc 分配块的元素是不安全操作，并且不会进行范围检查。

示例：在以下代码中

```
class Test
{
    static string IntToString(int value)
    {
        if (value == int.MinValue)
        {
            return "-2147483648";
        }
        int n = value >= 0 ? value : -value;
        unsafe
        {
            char* buffer = stackalloc char[16];
            char* p = buffer + 16;
            do
            {
                *--p = (char)(n % 10 + '0');
                n /= 10;
            } while (n != 0);
            if (value < 0)
            {
                *--p = '-';
            }
            return new string(p, 0, (int)(buffer + 16 - p));
        }
    }
    static void Main()
    {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```

在 IntToString 方法中使用 stackalloc 表达式在栈上分配一个 16 字符的缓冲区。方法返回时，该缓冲区会被自动丢弃。

但请注意，IntToString 可以在安全模式下重写；也就是说，不使用指针，如下所示：

```
class Test
{
    static string IntToString(int value)
    {
        if (value == int.MinValue)
        {
            return "-2147483648";
        }
        int n = value >= 0 ? value : -value;
        Span<char> buffer = stackalloc char[16];
        int idx = 16;
        do
        {
            buffer[--idx] = (char)(n % 10 + '0');
            n /= 10;
        } while (n != 0);
        if (value < 0)
        {
            buffer[--idx] = '-';
        }
        return buffer.Slice(idx).ToString();
    }
}
```

*示例结束*

**条件规范性文本结束。**

# A. 语法

本条款为资料性内容。

### A.1 总则

本附录包含规范中出现的语法产生式，包括用于不安全代码的可选产生式。产生式在此处出现的顺序与它们在规范中出现的顺序相同。

### A.2 词法语法

```
// Source: $6.3.1 General
DEFAULT  : 'default' ;
NULL     : 'null' ;
TRUE     : 'true' ;
FALSE    : 'false' ;
ASTERISK : '*' ;
SLASH    : '/' ;

// Source: $6.3.1 General
input
  : input_section?
  ;

input_section
  : input_section_part+
  ;

input_section_part
  : input_element* New_Line
  | PP_Directive
  ;

input_element
  : Whitespace
  | Comment
  | token
  ;

// Source: $6.3.2 Line terminators
New_Line
  : New_Line Character
  | '\u000D\u000A'  // carriage return, line feed
  ;

// Source: $6.3.3 Comments
Comment
  : Single_Line_Comment
  | Delimited_Comment
;
fragment Single_Line_Comment
  : '//' Input_Character*
  ;

fragment Input_Character
  // anything but New_Line_Character
  : ~('\\u000D' | '\\u000A' | '\\u0085' | '\\u2028' | '\\u2029')
  ;

fragment New_Line_Character
  : '\\u000D' // carriage return
  | '\\u000A' // line feed
  | '\\u0085' // next line
  | '\\u2028' // line separator
  | '\\u2029' // paragraph separator
  ;

fragment Delimited_Comment
  : '/*' Delimited_Comment_Section* ASTERISK+ '/'
  ;

fragment Delimited_Comment_Section
  : SLASH
  | ASTERISK* Not_Slash_Or_Asterisk
  ;

fragment Not_Slash_Or_Asterisk
  : ~('/' | '*')  // Any except SLASH or ASTERISK
  ;

// Source: $6.3.4 White space
Whitespace
  : [p{Zs}] // any character with Unicode class Zs
  | '\\u0009' // horizontal tab
  | '\\u000B' // vertical tab
  | '\\u000C' // form feed
  ;

// Source: $6.4.1 General
token
  : identifier
  | keyword
  | Integer_Literal
  | Real_Literal
  | Character_Literal
  | String_Literal
  | operator_or_punctuator
  ;

// Source: $6.4.2 Unicode character escape sequences
fragment Unicode_Escape_Sequence
  : '\\u' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
  | '\\U' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
  | '\\U' Hex_Digit Hex_Digit Hex_Digit Hex_Digit
;

 // Source: §6.4.3 Identifiers
identifier
  : Simple_Identifier
  | contextual_keyword
  ;

Simple_Identifier
  : Available_Identifier
  | Escaped_Identifier
  ;

fragment Available_Identifier
  // excluding keywords or contextual keywords, see note below
  : Basic_Identifier
  ;

fragment Escaped_Identifier
  // Includes keywords and contextual keywords prefixed by '@'.
  // See note below.
  : '@' Basic_Identifier
  ;

fragment Basic_Identifier
  : Identifier_Start_Character Identifier_Part_Character*
  ;

fragment Identifier_Start_Character
  : Letter_Character
  | Underscore_Character
  ;

fragment Underscore_Character
  : '_'  // underscore
  | '\\u005f' // Unicode_Escape_Sequence for underscore
  ;

fragment Identifier_Part_Character
  : Letter_Character
  | Decimal_Digit_Character
  | Connecting_Character
  | Combining_Character
  | Formatting_Character
  ;

fragment Letter_Character
  // Category Letter, all subcategories; category Number, subcategory letter.
  // [\\p{L}\\p{Nl}]
  // Only escapes for categories L & Nl allowed. See note below.
  | Unicode_Escape_Sequence
  ;

fragment Combining_Character
// Category Mark, subcategories non-spacing and spacing combining.
: [\p{Mn}\p{Mc}]
// Only escapes for categories Mn & Mc allowed. See note below.
| Unicode_Escape_Sequence
;

fragment Decimal_Digit_Character
// Category Number, subcategory decimal digit.
: [\p{Nd}]
// Only escapes for category Nd allowed. See note below.
| Unicode_Escape_Sequence
;

fragment Connecting_Character
// Category Punctuation, subcategory connector.
: [\p{Pc}]
// Only escapes for category Pc allowed. See note below.
| Unicode_Escape_Sequence
;

fragment Formatting_Character
// Category Other, subcategory format.
: [\p{Cf}]
// Only escapes for category Cf allowed, see note below.
| Unicode_Escape_Sequence
;

// Source: $6.4.4 Keywords
keyword
: 'abstract' | 'as' | 'base' | 'bool' | 'break'
| 'byte' | 'case' | 'catch' | 'char' | 'checked'
| 'class' | 'const' | 'continue' | 'decimal' | DEFAULT
| 'delegate' | 'do' | 'double' | 'else' | 'enum'
| 'event' | 'explicit' | 'extern' | FALSE | 'finally'
| 'fixed' | 'float' | 'for' | 'foreach' | 'goto'
| 'if' | 'implicit' | 'in' | 'int' | 'interface'
| 'internal' | 'is' | 'lock' | 'long' | 'namespace'
| 'new' | NULL | 'object' | 'operator' | 'out'
| 'override' | 'params' | 'private' | 'protected' | 'public'
| 'readonly' | 'ref' | 'return' | 'sbyte' | 'sealed'
| 'short' | 'sizeof' | 'stackalloc' | 'static' | 'string'
| 'struct' | 'switch' | 'this' | 'throw' | TRUE
| 'try' | 'typeof' | 'uint' | 'ulong' | 'unchecked'
| 'unsafe' | 'ushort' | 'using' | 'virtual' | 'void'
| 'volatile' | 'while'
;

// Source: $6.4.4 Keywords
contextual_keyword
: 'add' | 'alias' | 'ascending' | 'async' | 'await'
| 'by' | 'descending' | 'dynamic' | 'equals' | 'from'
| 'get' | 'global' | 'group' | 'into' | 'join'
| 'let' | 'nameof' | 'on' | 'orderby' | 'partial'
| 'remove' | 'select' | 'set' | 'unmanaged' | 'value'
| 'var' | 'when' | 'where' | 'yield'
;
 // Source: $6.4.5.1 General
literal
  : boolean_literal
  | Integer_literal
  | Real_Literal
  | Character_Literal
  | String_Literal
  | null_literal
;

// Source: $6.4.5.2 Boolean literals
boolean_literal
  : TRUE
  | FALSE
;

// Source: $6.4.5.3 Integer literals
Integer_Literal
  : Decimal_Integer_Literal
  | Hexadecimal_Integer_Literal
  | Binary_Integer_Literal
;

fragment Decimal_Integer_Literal
  : Decimal_Digit Decorated_Decimal_Digit* Integer_Type_Suffix?
;

fragment Decorated_Decimal_Digit
  : '_' * Decimal_Digit
;

fragment Decimal_Digit
  : '0'..'9'
;

fragment Integer_Type_Suffix
  : 'U' | 'u' | 'L' | 'l' |
  'UL' | 'UI' | 'uL' | 'ul' | 'LU' | 'Lu' | 'lU' | 'lu'
;

fragment Hexadecimal_Integer_Literal
  : ('0x' | '0X') Decorated_Hex_Digit+ Integer_Type_Suffix?
;

fragment Decorated_Hex_Digit
  : '_' * Hex_Digit
;

fragment Hex_Digit
  : '0'..'9' | 'A'..'F' | 'a'..'f'
;

fragment Binary_Integer_Literal


: ('0b' | '0B') Decorated_Binary_Digit+ Integer_Type_Suffix?
;

fragment Decorated_Binary_Digit
: '_' * Binary_Digit
;

fragment Binary_Digit
: '0' | '1'
;

// 来源：§6.4.5.4 实数文本
Real_Literal
: Decimal_Digit Decorated_Decimal_Digit* '.'
Decimal_Digit Decorated_Decimal_Digit* Exponent_Part? Real_Type_Suffix?
| '.' Decimal_Digit Decorated_Decimal_Digit* Exponent_Part? Real_Type_Suffix?
| Decimal_Digit Decorated_Decimal_Digit* Exponent_Part Real_Type_Suffix?
| Decimal_Digit Decorated_Decimal_Digit* Real_Type_Suffix
;

fragment Exponent_Part
: ('e' | 'E') Sign? Decimal_Digit Decorated_Decimal_Digit*
;

fragment Sign
: '+' | '-'
;

fragment Real_Type_Suffix
: 'F' | 'f' | 'D' | 'd' | 'M' | 'm'
;

// 来源：§6.4.5.5 字符文本
Character_Literal
: '\'' Character '\''
;

fragment Character
: Single_Character
| Simple_Escape_Sequence
| Hexadecimal_Escape_Sequence
| Unicode_Escape_Sequence
;

fragment Single_Character
// 除 '、\ 和 New_Line_Character 之外的任何字符
: ~['\\'\u000D\u000A\u0085\u2028\u2029]
;

fragment Simple_Escape_Sequence
: '\\'' | '\\"' | '\\\\' | '\\0' | '\\a' | '\\b' |
'\\f' | '\\n' | '\\r' | '\\t' | '\\v'
;

fragment Hexadecimal_Escape_Sequence
: '\x' Hex_Digit Hex_Digit? Hex_Digit? Hex_Digit?
;

// 来源：§6.4.5.6 字符串文本
String_literal
  : Regular_String_Literal
  | Verbatim_String_Literal
;

fragment Regular_String_Literal
  : '"' Regular_String_Literal_Character* '"'
;

fragment Regular_String_Literal_Character
  : Single_Regular_String_Literal_Character
  | Simple_Escape_Sequence
  | Hexadecimal_Escape_Sequence
  | Unicode_Escape_Sequence
;

fragment Single_Regular_String_Literal_Character
  // 除 "、\ 和 New_Line_Character 之外的任何字符
  : ~["\\u000D\u000A\u0085\u2028\u2029]
;

fragment Verbatim_String_Literal
  : @" Verbatim_String_Literal_Character* '"'
;

fragment Verbatim_String_Literal_Character
  : Single_Verbatim_String_Literal_Character
  | Quote_Escape_Sequence
;

fragment Single_Verbatim_String_Literal_Character
  : ~["']   // 除引号（U+0022）之外的任何字符
;

fragment Quote_Escape_Sequence
  : '""'
;

// 来源：§6.4.5.7 null 文本
null_literal
  : NULL
;

// 来源：§6.4.6 运算符和标点符号
operator_or_punctuator
  : '{' | '}' | '[' | ']' | '(' | ')' | ',' | ';' | ':' | '?'
  | '+' | '-' | ASTERISK | SLASH | '%' | '&' | '|' | '^' | '!' | '~'
  | '=' | '<' | '>' | '?' | '==' | '!=' | '++' | '--' | '&&' | '||'
  | '=>' | '==' | '!=' | '<=' | '>=' | '?:' | '+=' | '-=' | '*=' | '/=' | '%='
  | '&=' | '|=' | '^=' | '<<' | '<<=' | '>>' | '>>='
;

right_shift
    : '>' '>'
    ;
right_shift_assignment
    : '>>='
    ;

// 来源：§6.5.1 一般
PP_Directive
    : PP_Start PP_Kind PP_New_Line
    ;

fragment PP_Kind
    : PP_Declaration
    | PP_Conditional
    | PP_Line
    | PP_Diagnostic
    | PP_Region
    | PP_Pragma
    ;

// 仅在一行的开头识别
fragment PP_Start
    // 参见下面的注释。
    : { getCharPositionInLine() == 0 }? PP_Whitespace? '#' PP_Whitespace?
    ;

fragment PP_Whitespace
    : ( [p{Zs}]  // 具有 Unicode 类别 Zs 的任何字符
      | '\u0009'  // 水平制表符
      | '\u000B'  // 垂直制表符
      | '\u000C'  // 换页符
      )+
    ;

fragment PP_New_Line
    : PP_Whitespace? Single_Line_Comment? New_Line
    ;

// 来源：§6.5.2 条件编译符号
fragment PP_Conditional_Symbol
    // 不得等于标记 TRUE 或 FALSE。参见下面的注释。
    : Basic_Identifier
    ;

// 来源：§6.5.3 预处理表达式
fragment PP_Expression
    : PP_Whitespace? PP_Or_Expression PP_Whitespace?
    ;

fragment PP_Or_Expression
    : PP_And_Expression (PP_Whitespace? '||' PP_Whitespace? PP_And_Expression)*
    ;

fragment PP_And_Expression
  : PP_Equality_Expression (PP_Whitespace? '&&' PP_Whitespace?
    PP_Equality_Expression)*
  ;

fragment PP_Equality_Expression
  : PP_Unary_Expression (PP_Whitespace? ('==' | '!=') PP_Whitespace?
    PP_Unary_Expression)*
  ;

fragment PP_Unary_Expression
  : PP_Primary_Expression
  | '!' PP_Whitespace? PP_Unary_Expression
  ;

fragment PP_Primary_Expression
  : TRUE
  | FALSE
  | PP_Conditional_Symbol
  | '(' PP_Whitespace? PP_Expression PP_Whitespace? ')'
  ;

// 来源：§6.5.4 定义指令
fragment PP_Declaration
  : 'define' PP_Whitespace PP_Conditional_Symbol
  | 'undef' PP_Whitespace PP_Conditional_Symbol
  ;

// 来源：§6.5.5 条件编译指令
fragment PP_Conditional
  : PP_If_Section
  | PP_Elif_Section
  | PP_Else_Section
  | PP_Endif
  ;

fragment PP_If_Section
  : 'if' PP_Whitespace PP_Expression
  ;

fragment PP_Elif_Section
  : 'elif' PP_Whitespace PP_Expression
  ;

fragment PP_Else_Section
  : 'else'
  ;

fragment PP_Endif
  : 'endif'
  ;

// 来源：§6.5.6 诊断指令
fragment PP_Diagnostic
: 'error' PP_Message?
| 'warning' PP_Message?
;

fragment PP_Message
: PP_Whitespace Input_Character*
;

## A 语法
// 来源：§6.5.7 区域指令
fragment PP_Region
: PP_Start_Region
| PP_End_Region
;

fragment PP_Start_Region
: 'region' PP_Message?
;

fragment PP_End_Region
: 'endregion' PP_Message?
;

// 来源：§6.5.8 行指令
fragment PP_Line
: 'line' PP_Whitespace PP_Line_Indicator
;

fragment PP_Line_Indicator
: Decimal_Digit+ PP_Whitespace PP_Compilation_Unit_Name
| Decimal_Digit+
| DEFAULT
| 'hidden'
;

fragment PP_Compilation_Unit_Name
: '"' PP_Compilation_Unit_Name_Character+ '"'
;

fragment PP_Compilation_Unit_Name_Character
: // 除 " 之外的任何 Input_Character
~('\u000D' | '\u000A' | '\u0085' | '\u2028' | '\u2029' | '#')
;

// 来源：§6.5.9 pragma 指令
fragment PP_Pragma
: 'pragma' PP_Pragma_Text?
;

fragment PP_Pragma_Text
: PP_Whitespace Input_Character*
;

## A.3 语法文法
// 来源：§7.8.1 一般
namespace_name
  : namespace_or_type_name
  ;

type_name
  : namespace_or_type_name
  ;

namespace_or_type_name
  : identifier type_argument_list?
  | namespace_or_type_name '.' identifier type_argument_list?
  | qualified_alias_member
  ;

// 来源：§8.1 一般
type
  : reference_type
  | value_type
  | type_parameter
  | pointer_type    // 不安全代码支持
  ;

// 来源：§8.2.1 一般
reference_type
  : class_type
  | interface_type
  | array_type
  | delegate_type
  | 'dynamic'
  ;

class_type
  : type_name
  | 'object'
  | 'string'
  ;

interface_type
  : type_name
  ;

array_type
  : non_array_type rank_specifier+
  ;

non_array_type
  : value_type
  | class_type
  | interface_type
  | delegate_type
  | 'dynamic'
  | type_parameter
| pointer_type    // 不安全代码支持
;

rank_specifier
  : '[' ',' '*' ']'
  ;

delegate_type
  : type_name
  ;

## A 语法
// 来源：§8.3.1 一般
value_type
  : non_nullable_value_type
  | nullable_value_type
  ;

non_nullable_value_type
  : struct_type
  | enum_type
  ;

struct_type
  : type_name
  | simple_type
  | tuple_type
  ;

simple_type
  : numeric_type
  | 'bool'
  ;

numeric_type
  : integral_type
  | floating_point_type
  | 'decimal'
  ;

integral_type
  : 'sbyte'
  | 'byte'
  | 'short'
  | 'ushort'
  | 'int'
  | 'uint'
  | 'long'
  | 'ulong'
  | 'char'
  ;

floating_point_type
  : 'float'
  | 'double'
  ;

tuple_type
  : '(' tuple_type_element (',' tuple_type_element)+ ')'
  ;

tuple_type_element
  : type identifier?
  ;

enum_type
  : type_name
  ;

nullable_value_type
  : non_nullable_value_type '?'
  ;

// 来源：§8.4.2 类型实参
type_argument_list
  : '<' type_arguments '>'
  ;

type_arguments
  : type_argument (',' type_argument)*
  ;

type_argument
  : type
  ;

// 来源：§8.5 类型形参
type_parameter
  : identifier
  ;

// 来源：§8.8 非托管类型
unmanaged_type
  : value_type
  | pointer_type    // 不安全代码支持
  ;

// 来源：§9.5 变量引用
variable_reference
  : expression
  ;

// 来源：§11.2.1 一般
pattern
  : declaration_pattern
  | constant_pattern
  | var_pattern
  ;

// 来源：§11.2.2 声明模式
declaration_pattern




## 语法

```
: type simple_designation
;
simple_designation
: single_variable_designation
;
single_variable_designation
: identifier
;

// Source: §11.2.3 Constant pattern
constant_pattern
: constant_expression
;

// Source: §11.2.4 Var pattern
var_pattern
: 'var' designation
;
designation
: simple_designation
;

// Source: §12.6.2.1 General
argument_list
: argument (',' argument)*
;

argument
: argument_name? argument_value
;

argument_name
: identifier ':'
;

argument_value
: expression
| 'in' variable_reference
| 'ref' variable_reference
| 'out' variable_reference
;

// Source: §12.8.1 General
primary_expression
: primary_no_array_creation_expression
| array_creation_expression
;

primary_no_array_creation_expression
: literal
| interpolated_string_expression
| simple_name
| parenthesized_expression
| tuple_expression
| member_access
| null_conditional_member_access
| invocation_expression
| element_access
| null_conditional_element_access
| this_access
| base_access
| post_increment_expression
| post_decrement_expression
| object_creation_expression
| delegate_creation_expression
| anonymous_object_creation_expression
| typeof_expression
| sizeof_expression
| checked_expression
| unchecked_expression
| default_value_expression
| nameof_expression
| anonymous_method_expression
| pointer_member_access    // unsafe code support
| pointer_element_access    // unsafe code support
| stackalloc_expression
| ;

// Source: §12.8.3 Interpolated string expressions
interpolated_string_expression
: interpolated_regular_string_expression
| interpolated_verbatim_string_expression
;

// interpolated regular string expressions

interpolated_regular_string_expression
: Interpolated_Regular_String_Start Interpolated_Regular_String_Mid?
('{' regular_interpolation '}' Interpolated_Regular_String_Mid?)*
Interpolated_Regular_String_End
;

regular_interpolation
: expression (',' interpolation_minimum_width)?
Regular_Interpolation_Format?
;

interpolation_minimum_width
: constant_expression
;

Interpolated_Regular_String_Start
: '$"'
;

// the following three lexical rules are context sensitive, see details below

Interpolated_Regular_String_Mid
: Interpolated_Regular_String_Element+
;

Regular_Interpolation_Format
    : ':' Interpolated_Regular_String_Element+
    ;

Interpolated_Regular_String_End
    : '""'
    ;

fragment Interpolated_Regular_String_Element
    : Interpolated_Regular_String_Character
    | Simple_Escape_Sequence
    | Hexadecimal_Escape_Sequence
    | Unicode_Escape_Sequence
    | Open_Brace_Escape_Sequence
    | Close_Brace_Escape_Sequence
    ;

fragment Interpolated_Regular_String_Character
    // Any character except " (U+0022), \\ (U+005C),
    // { (U+007B), } (U+007D), and New Line Character.
    : ~["\\{}"\u000D\u000A\u0085\u2028\u2029]
    ;

// interpolated verbatim string expressions
interpolated_verbatim_string_expression
    : Interpolated_Verbatim_String_Start Interpolated_Verbatim_String_Mid?
    ('{' verbatim_interpolation '}' Interpolated_Verbatim_String_Mid?)*
    Interpolated_Verbatim_String_End
    ;

verbatim_interpolation
    : expression (',' interpolation_minimum_width)?
    Verbatim_Interpolation_Format?
    ;

Interpolated_Verbatim_String_Start
    : '$@"'
    ;

// the following three lexical rules are context sensitive, see details below
Interpolated_Verbatim_String_Mid
    : Interpolated_Verbatim_String_Element+
    ;

Verbatim_Interpolation_Format
    : ':' Interpolated_Verbatim_String_Element+
    ;

Interpolated_Verbatim_String_End
    : '""'
    ;

fragment Interpolated_Verbatim_String_Element
  : Interpolated_Verbatim_String_Character
  | Quote_Escape_Sequence
  | Open_Brace_Escape_Sequence
  | Close_Brace_Escape_Sequence
  ;

fragment Interpolated_Verbatim_String_Character
  : ~["{}"]    // Any character except " (U+0022), { (U+007B) and } (U+007D)
  ;

// lexical fragments used by both regular and verbatim interpolated strings

fragment Open_Brace_Escape_Sequence
  : '{{'
  ;

fragment Close_Brace_Escape_Sequence
  : '}}'
  ;

// Source: §12.8.4 Simple names
simple_name
  : identifier type_argument_list?
  ;

// Source: §12.8.5 Parenthesized expressions
parenthesized_expression
  : '(' expression ')'
  ;

// Source: §12.8.6 Tuple expressions
tuple_expression
  : '(' tuple_element (',' tuple_element)+ ')'
  | deconstruction_expression
  ;

tuple_element
  : (identifier ':')? expression
  ;

deconstruction_expression
  : 'var' deconstruction_tuple
  ;

deconstruction_tuple
  : '(' deconstruction_element (',' deconstruction_element)+ ')'
  ;

deconstruction_element
  : deconstruction_tuple
  | identifier
  ;

// Source: §12.8.7.1 General
member_access
  : primary_expression '.' identifier type_argument_list?
  | predefined_type '.' identifier type_argument_list?
  | qualified_alias_member '.' identifier type_argument_list?
  ;

predefined_type
  : 'bool' | 'byte' | 'char' | 'decimal' | 'double' | 'float' | 'int'
  | 'long' | 'object' | 'sbyte' | 'short' | 'string' | 'uint' | 'ulong'
  | 'ushort'
  ;

// Source: §12.8.8 Null Conditional Member Access
null_conditional_member_access
  : primary_expression '?' '.' identifier type_argument_list?
    dependent_access*
  ;

dependent_access
  : '.' identifier type_argument_list?    // member access
  | '[' argument_list ']'    // element access
  | '(' argument_list? ')'    // invocation
  ;

null_conditional_projection_initializer
  : primary_expression '?' '.' identifier type_argument_list?
  ;

// Source: §12.8.9.1 General
invocation_expression
  : primary_expression '(' argument_list? ')'
  ;

// Source: §12.8.10 Null Conditional Invocation Expression
null_conditional_invocation_expression
  : null_conditional_member_access '(' argument_list? ')'
  | null_conditional_element_access '(' argument_list? ')'
  ;

// Source: §12.8.11.1 General
element_access
  : primary_no_array_creation_expression '[' argument_list ']'
  ;

// Source: §12.8.12 Null Conditional Element Access
null_conditional_element_access
  : primary_no_array_creation_expression '?' '[' argument_list ']'
    dependent_access*
  ;

// Source: §12.8.13 This access
this_access
  : 'this'
  ;

// Source: §12.8.14 Base access
base_access
  : 'base' '.' identifier type_argument_list?
  | 'base' '[' argument_list ']'
  ;

// Source: §12.8.15 Postfix increment and decrement operators
post_increment_expression
  : primary_expression '++'
  ;

post_decrement_expression
  : primary_expression '--'
  ;

// Source: §12.8.16.2 Object creation expressions
object_creation_expression
  : 'new' type '(' argument_list? ')' object_or_collection_initializer?
  | 'new' type object_or_collection_initializer
  ;

object_or_collection_initializer
  : object_initializer
  | collection_initializer
  ;

// Source: §12.8.16.3 Object initializers
object_initializer
  : '{' member_initializer_list? '}'
  | '{' member_initializer_list ',' '}'
  ;

member_initializer_list
  : member_initializer (',' member_initializer)*
  ;

member_initializer
  : initializer_target '=' initializer_value
  ;

initializer_target
  : identifier
  | '[' argument_list ']'
  ;

initializer_value
  : expression
  | object_or_collection_initializer
  ;

// Source: §12.8.16.4 Collection initializers
collection_initializer
  : '{' element_initializer_list '}'
  | '{' element_initializer_list ',' '}'
  ;

element_initializer_list
  : element_initializer (',' element_initializer)*
  ;
element_initializer
  : non_assignment_expression
  | '{' expression_list '}'
  ;
expression_list
  : expression
  | expression_list ',' expression
  ;
// Source: §12.8.16.5 Array creation expressions
array_creation_expression
  : 'new' non_array_type '[' expression_list ']' rank_specifier*
    array_initializer?
  | 'new' array_type array_initializer
  | 'new' rank_specifier array_initializer
  ;
// Source: §12.8.16.6 Delegate creation expressions
delegate_creation_expression
  : 'new' delegate_type '(' expression ')'
  ;
// Source: §12.8.16.7 Anonymous object creation expressions
anonymous_object_creation_expression
  : 'new' anonymous_object_initializer
  ;
anonymous_object_initializer
  : '{' member_declarator_list? '}'
  | '{' member_declarator_list ',' '}'
  ;
member_declarator_list
  : member_declarator (',' member_declarator)*
  ;
member_declarator
  : simple_name
  | member_access
  | null_conditional_projection_initializer
  | base_access
  | identifier '=' expression
  ;
// Source: §12.8.17 The typeof operator
typeof_expression
  : 'typeof' '(' type ')'
  | 'typeof' '(' unbound_type_name ')'
  | 'typeof' '(' 'void' ')'
```

;
unbound_type_name
  : identifier generic_dimension_specifier?
  | identifier '::' identifier generic_dimension_specifier?
  | unbound_type_name '.' identifier generic_dimension_specifier?
  ;

generic_dimension_specifier
  : '<' comma* '>'
  ;

comma
  : ','
  ;

## §12.8.18 sizeof 运算符
sizeof_expression
  : 'sizeof' '(' unmanaged_type ')'
  ;

## §12.8.19 checked 和 unchecked 运算符
checked_expression
  : 'checked' '(' expression ')'
  ;

unchecked_expression
  : 'unchecked' '(' expression ')'
  ;

## §12.8.20 默认值表达式
default_value_expression
  : explicitly_typed_default
  | default_literal
  ;

explicitly_typed_default
  : 'default' '(' type ')'
  ;

default_literal
  : 'default'
  ;

## §12.8.21 栈分配
stackalloc_expression
  : 'stackalloc' unmanaged_type '[' expression ']'
  | 'stackalloc' unmanaged_type? '[' constant_expression? ']' stackalloc_initializer
  ;

stackalloc_initializer
  : '{' stackalloc_initializer_element_list '}'
  ;

stackalloc_initializer_element_list
  : stackalloc_element_initializer (',' stackalloc_element_initializer)* ','?
  ;

stackalloc_element_initializer
  : expression
  ;

## §12.8.22 nameof 表达式
nameof_expression
  : 'nameof' '(' named_entity ')'
  ;

named_entity
  : named_entity_target ('.' identifier type_argument_list?)*
  ;

named_entity_target
  : simple_name
  | 'this'
  | 'base'
  | predefined_type
  | qualified_alias_member
  ;

## §12.9.1 一般
unary_expression
  : primary_expression
  | '+' unary_expression
  | '-' unary_expression
  | '!' unary_expression
  | '~' unary_expression
  | pre_increment_expression
  | pre_decrement_expression
  | cast_expression
  | await_expression
  | pointer_indirection_expression    // 不安全代码支持
  | addressof_expression              // 不安全代码支持
  ;

## §12.9.6 前缀递增和递减运算符
pre_increment_expression
  : '++' unary_expression
  ;

pre_decrement_expression
  : '--' unary_expression
  ;

## §12.9.7 转换表达式
cast_expression
  : '(' type ')' unary_expression
  ;

## §12.9.8.1 一般
await_expression
  : 'await' unary_expression
  ;

## §12.10.1 一般
multiplicative_expression
  : unary_expression
  | multiplicative_expression '*' unary_expression
  | multiplicative_expression '/' unary_expression
  | multiplicative_expression '%' unary_expression
  ;

additive_expression
  : multiplicative_expression
  | additive_expression '+' multiplicative_expression
  | additive_expression '-' multiplicative_expression
  ;

## §12.11 移位运算符
shift_expression
  : additive_expression
  | shift_expression '<<' additive_expression
  | shift_expression right_shift additive_expression
  ;

## §12.12.1 一般
relational_expression
  : shift_expression
  | relational_expression '<' shift_expression
  | relational_expression '>' shift_expression
  | relational_expression '<=' shift_expression
  | relational_expression '>=' shift_expression
  | relational_expression 'is' type
  | relational_expression 'is' pattern
  | relational_expression 'as' type
  ;

equality_expression
  : relational_expression
  | equality_expression '==' relational_expression
  | equality_expression '!=' relational_expression
  ;

## §12.13.1 一般
and_expression
  : equality_expression
  | and_expression '&' equality_expression
  ;

exclusive_or_expression
  : and_expression
  | exclusive_or_expression '^' and_expression
  ;

inclusive_or_expression
  : exclusive_or_expression
  | inclusive_or_expression '|' exclusive_or_expression
  ;

## §12.14.1 一般
conditional_and_expression
  : inclusive_or_expression
  | conditional_and_expression '&&' inclusive_or_expression
  ;

conditional_or_expression
  : conditional_and_expression
  | conditional_or_expression '||' conditional_and_expression
  ;

## §12.15 空合并运算符
null_coalescing_expression
  : conditional_or_expression
  | conditional_or_expression '??' null_coalescing_expression
  | throw_expression
  ;

## §12.16 throw 表达式运算符
throw_expression
  : 'throw' null_coalescing_expression
  ;

## §12.17 声明表达式
declaration_expression
  : local_variable_type identifier
  ;

local_variable_type
  : type
  | 'var'
  ;

## §12.18 条件运算符
conditional_expression
  : null_coalescing_expression
  | null_coalescing_expression '?' expression ':' expression
  | null_coalescing_expression '?' 'ref' variable_reference ':'
    'ref' variable_reference
  ;

## §12.19.1 一般
lambda_expression
  : 'async'? anonymous_function_signature '=>' anonymous_function_body
  ;

anonymous_method_expression
  : 'async'? 'delegate' explicit_anonymous_function_signature? block
  ;

anonymous_function_signature
    : explicit_anonymous_function_signature
    | implicit_anonymous_function_signature
    ;

explicit_anonymous_function_signature
    : '(' explicit_anonymous_function_parameter_list? ')'
    ;

explicit_anonymous_function_parameter_list
    : explicit_anonymous_function_parameter
    (',' explicit_anonymous_function_parameter)*
    ;

explicit_anonymous_function_parameter
    : anonymous_function_parameter_modifier? type identifier
    ;

anonymous_function_parameter_modifier
    : 'ref'
    | 'out'
    | 'in'
    ;

implicit_anonymous_function_signature
    : '(' implicit_anonymous_function_parameter_list? ')'
    | implicit_anonymous_function_parameter
    ;

implicit_anonymous_function_parameter_list
    : implicit_anonymous_function_parameter
    (',' implicit_anonymous_function_parameter)*
    ;

implicit_anonymous_function_parameter
    : identifier
    ;

anonymous_function_body
    : null_conditional_invocation_expression
    | expression
    | 'ref' variable_reference
    | block
    ;

## §12.20.1 一般
query_expression
    : from_clause query_body
    ;

from_clause
    : 'from' type? identifier 'in' expression
    ;

query_body

;
select_clause
: 'select' expression
;

group_clause
: 'group' expression 'by' expression
;

query_continuation
: 'into' identifier query_body
;

## §12.21.1 一般
assignment
: unary_expression assignment_operator expression
;

assignment_operator
: '=' 'ref'? | '+=' | '-=' | '*=' | '/=' | '%=' | '&=' | '|=' | '^=' | '<<='
| right_shift_assignment
;

## §12.22 表达式
expression
: non_assignment_expression
| assignment
;

non_assignment_expression
: declaration_expression
| conditional_expression
| lambda_expression
| query_expression
;

## §12.23 常量表达式
constant_expression
: expression
;

## §12.24 布尔表达式
boolean_expression
: expression
;

## §13.1 一般
statement
: labeled_statement
| declaration_statement
| embedded_statement
;

embedded_statement
: block
| empty_statement
| expression_statement
| selection_statement
| iteration_statement
| jump_statement
| try_statement
| checked_statement
| unchecked_statement
| lock_statement
| using_statement
| yield_statement
| unsafe_statement    // 不安全代码支持
| fixed_statement     // 不安全代码支持
;

## §13.3.1 一般
block
: '{' statement_list? '}'
;

## §13.3.2 语句列表
statement_list
: statement+
;

## §13.4 空语句
empty_statement
: ';'
;

## §13.5 带标签的语句
labeled_statement
: identifier ':' statement
;

## §13.6.1 一般
declaration_statement
: local_variable_declaration ';'
| local_constant_declaration ';'
| local_function_declaration
;

## §13.6.2 局部变量声明
local_variable_declaration
: implicitly_typed_local_variable_declaration
| explicitly_typed_local_variable_declaration
| ref_local_variable_declaration
;

## §13.6.2.1 隐式类型局部变量声明
implicitly_typed_local_variable_declaration
: 'var' implicitly_typed_local_variable_declarator
| ref_kind 'var' ref_local_variable_declarator
;

implicitly_typed_local_variable_declarator
  : identifier '=' expression
  ;

// Source: §13.6.2.2 显式类型局部变量声明
explicitly_typed_local_variable_declaration
  : type explicitly_typed_local_variable_declarators
  ;

explicitly_typed_local_variable_declarators
  : explicitly_typed_local_variable_declarator
    (',' explicitly_typed_local_variable_declarator)*
  ;

explicitly_typed_local_variable_declarator
  : identifier ('=' local_variable_initializer)?
  ;

local_variable_initializer
  : expression
  | array_initializer
  ;

// Source: §13.6.2.3 引用局部变量声明
ref_local_variable_declaration
  : ref_kind type ref_local_variable_declarators
  ;

ref_local_variable_declarators
  : ref_local_variable_declarator (',' ref_local_variable_declarator)*
  ;

ref_local_variable_declarator
  : identifier '=' 'ref' variable_reference
  ;

// Source: §13.6.3 局部常量声明
local_constant_declaration
  : 'const' type constant_declarators
  ;

constant_declarators
  : constant_declarator (',' constant_declarator)*
  ;

constant_declarator
  : identifier '=' constant_expression
  ;

// Source: §13.6.4 局部函数声明
local_function_declaration
  : local_function_modifier* return_type local_function_header
    local_function_body
  | ref_local_function_modifier* ref_kind ref_return_type local_function_header ref_local_function_body
  ;

local_function_header
: identifier '(' formal_parameter_list? ')'
| identifier type_parameter_list '(' formal_parameter_list? ')'
type_parameter_constraints_clause*
;

local_function_modifier
: ref_local_function_modifier
| 'async'
;

ref_local_function_modifier
: unsafe_modifier  // 不安全代码支持
;

local_function_body
: block
| '=>' null_conditional_invocation_expression ';'
| '=>' expression ';'
;

ref_local_function_body
: block
| '=>' 'ref' variable_reference ';'
;

// Source: §13.7 表达式语句
expression_statement
: statement_expression ';'
;

statement_expression
: null_conditional_invocation_expression
| invocation_expression
| object_creation_expression
| assignment
| post_increment_expression
| post_decrement_expression
| pre_increment_expression
| pre_decrement_expression
| await_expression
;

// Source: §13.8.1 通用
selection_statement
: if_statement
| switch_statement
;

// Source: §13.8.2 if 语句
if_statement
: 'if' '(' boolean_expression ')' embedded_statement
| 'if' '(' boolean_expression ')' embedded_statement
'else' embedded_statement
;

// Source: §13.8.3 switch 语句
switch_statement
: 'switch' '(' expression ')' switch_block
;

switch_block
: '{' switch_section* '}'
;

switch_section
: switch_label+ statement_list
;

switch_label
: 'case' pattern case_guard? ':'
| 'default' ':'
;

case_guard
: 'when' expression
;

// Source: §13.9.1 通用
iteration_statement
: while_statement
| do_statement
| for_statement
| foreach_statement
;

// Source: §13.9.2 while 语句
while_statement
: 'while' '(' boolean_expression ')' embedded_statement
;

// Source: §13.9.3 do 语句
do_statement
: 'do' embedded_statement 'while' '(' boolean_expression ')' ';'
;

// Source: §13.9.4 for 语句
for_statement
: 'for' '(' for_initializer? ';' for_condition? ';' for_iterator? ')'
embedded_statement
;

for_initializer
: local_variable_declaration
| statement_expression_list
;

## 语法

for_condition
    : boolean_expression
    ;

for_iterator
    : statement_expression_list
    ;

statement_expression_list
    : statement_expression (',' statement_expression)*
    ;

// Source: §13.9.5 foreach 语句
foreach_statement
    : 'foreach' '(' ref_kind? local_variable_type identifier 'in'
    expression ')' embedded_statement
    ;

// Source: §13.10.1 通用
jump_statement
    : break_statement
    | continue_statement
    | goto_statement
    | return_statement
    | throw_statement
    ;

// Source: §13.10.2 break 语句
break_statement
    : 'break' ';'
    ;

// Source: §13.10.3 continue 语句
continue_statement
    : 'continue' ';'
    ;

// Source: §13.10.4 goto 语句
goto_statement
    : 'goto' identifier ';'
    | 'goto' 'case' constant_expression ';'
    | 'goto' 'default' ';'
    ;

// Source: §13.10.5 return 语句
return_statement
    : 'return' ';'
    | 'return' expression ';'
    | 'return' 'ref' variable_reference ';'
    ;

// Source: §13.10.6 throw 语句
throw_statement
    : 'throw' expression? ';'
    ;

// Source: §13.11 try 语句
try_statement
  : 'try' block catch_clauses
  | 'try' block catch_clauses? finally_clause
  ;

catch_clauses
  : specific_catch_clause+
  | specific_catch_clause* general_catch_clause
  ;

specific_catch_clause
  : 'catch' exception_specifier exception_filter? block
  | 'catch' exception_filter block
  ;

exception_specifier
  : '(' type identifier? ')'
  ;

exception_filter
  : 'when' '(' boolean_expression ')'
  ;

general_catch_clause
  : 'catch' block
  ;

finally_clause
  : 'finally' block
  ;

// Source: §13.12 checked 和 unchecked 语句
checked_statement
  : 'checked' block
  ;

unchecked_statement
  : 'unchecked' block
  ;

// Source: §13.13 lock 语句
lock_statement
  : 'lock' '(' expression ')' embedded_statement
  ;

// Source: §13.14 using 语句
using_statement
  : 'using' '(' resource_acquisition ')' embedded_statement
  ;

resource_acquisition
  : local_variable_declaration
  | expression
  ;

## 语法

// Source: §13.15 yield 语句
yield_statement
    : 'yield' 'return' expression ';'
    | 'yield' 'break' ';'
    ;

// Source: §14.2 编译单元
compilation_unit
    : extern_alias_directive* using_directive* global_attributes?
      namespace_member_declaration*
    ;

// Source: §14.3 命名空间声明
namespace_declaration
    : 'namespace' qualified_identifier namespace_body ';'?
    ;

qualified_identifier
    : identifier ('.' identifier)*
    ;

namespace_body
    : '{' extern_alias_directive* using_directive*
      namespace_member_declaration* '}'
    ;

// Source: §14.4 extern 别名指令
extern_alias_directive
    : 'extern' 'alias' identifier ';'
    ;

// Source: §14.5.1 通用
using_directive
    : using_alias_directive
    | using_namespace_directive
    | using_static_directive
    ;

// Source: §14.5.2 using 别名指令
using_alias_directive
    : 'using' identifier '=' namespace_or_type_name ';'
    ;

// Source: §14.5.3 using 命名空间指令
using_namespace_directive
    : 'using' namespace_name ';'
    ;

// Source: §14.5.4 using static 指令
using_static_directive
    : 'using' 'static' type_name ';'
    ;

// Source: §14.6 命名空间成员声明
namespace_member_declaration
  : namespace_declaration
  | type_declaration
  ;

// Source: §14.7 类型声明
type_declaration
  : class_declaration
  | struct_declaration
  | interface_declaration
  | enum_declaration
  | delegate_declaration
  ;

// Source: §14.8.1 通用
qualified_alias_member
  : identifier ':' identifier type_argument_list?
  ;

// Source: §15.2.1 通用
class_declaration
  : attributes? class_modifier* 'partial'? 'class' identifier
    type_parameter_list? class_base? type_parameter_constraints_clause*
    class_body ';'?
  ;

// Source: §15.2.2.1 通用
class_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'abstract'
  | 'sealed'
  | 'static'
  | unsafe_modifier  // 不安全代码支持
  ;

// Source: §15.2.3 类型参数
type_parameter_list
  : '<' type_parameters '>'
  ;

type_parameters
  : attributes? type_parameter
  | type_parameters ',' attributes? type_parameter
  ;

// Source: §15.2.4.1 通用
class_base
  : ':' class_type
  | ':' interface_type_list
  | ':' class_type ',' interface_type_list
  ;



## A 语法

```text
;
interface_type_list
  : interface_type (',' interface_type)*
  ;

// Source: §15.2.5 Type parameter constraints
type_parameter_constraints_clauses
  : type_parameter_constraints_clause
  | type_parameter_constraints_clauses type_parameter_constraints_clause
  ;

type_parameter_constraints_clause
  : 'where' type_parameter ':' type_parameter_constraints
  ;

type_parameter_constraints
  : primary_constraint
  | secondary_constraints
  | constructor_constraint
  | primary_constraint ',' secondary_constraints
  | primary_constraint ',' constructor_constraint
  | secondary_constraints ',' constructor_constraint
  | primary_constraint ',' secondary_constraints ',' constructor_constraint
  ;

primary_constraint
  : class_type
  | 'class'
  | 'struct'
  | 'unmanaged'
  ;

secondary_constraints
  : interface_type
  | type_parameter
  | secondary_constraints ',' interface_type
  | secondary_constraints ',' type_parameter
  ;

constructor_constraint
  : 'new' '(' ')'
  ;

// Source: §15.2.6 Class body
class_body
  : '{' class_member_declaration* '}'
  ;

// Source: §15.3.1 General
class_member_declaration
  : constant_declaration
  | field_declaration
  | method_declaration
  | property_declaration
  | event_declaration
  | indexer_declaration
  | operator_declaration
  | constructor_declaration
  | finalizer_declaration
  | static_constructor_declaration
  | type_declaration
  ;

// Source: §15.4 Constants
constant_declaration
  : attributes? constant_modifier* 'const' type constant_declarators ';'
  ;

constant_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  ;

// Source: §15.5.1 General
field_declaration
  : attributes? field_modifier* type variable_declarators ';'
  ;

field_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'static'
  | 'readonly'
  | 'volatile'
  | unsafe_modifier  // unsafe code support
  ;

variable_declarators
  : variable_declarator (',' variable_declarator)*
  ;

variable_declarator
  : identifier ('=' variable_initializer)?
  ;

// Source: §15.6.1 General
method_declaration
  : attributes? method_modifiers return_type method_header method_body
  | attributes? ref_method_modifiers ref_kind ref_return_type method_header
    ref_method_body
  ;

method_modifiers
  : method_modifier* 'partial'?
  ;

ref_kind
  : 'ref'
  | 'ref' 'readonly'
  ;

ref_method_modifiers
  : ref_method_modifier*
  ;

method_header
  : member_name '(' formal_parameter_list? ')'
  | member_name type_parameter_list '(' formal_parameter_list? ')'
    type_parameter_constraints_clause*
  ;

method_modifier
  : ref_method_modifier
  | 'async'
  ;

ref_method_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'static'
  | 'virtual'
  | 'sealed'
  | 'override'
  | 'abstract'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

return_type
  : ref_return_type
  | 'void'
  ;

ref_return_type
  : type
  ;

member_name
  : identifier
  | interface_type '.' identifier
  ;

method_body
  : block
  | '=>' null_conditional_invocation_expression ';'
  | '=>' expression ';'
  | ';'
  ;

ref_method_body
  : block
  | '=>' 'ref' variable_reference ';'
  | ';'
  ;

// Source: §15.6.2.1 General
formal_parameter_list
  : fixed_parameters
  | fixed_parameters ',' parameter_array
  | parameter_array
  ;

fixed_parameters
  : fixed_parameter (',' fixed_parameter)*
  ;

fixed_parameter
  : attributes? parameter_modifier? type identifier default_argument?
  ;

default_argument
  : '=' expression
  ;

parameter_modifier
  : parameter_mode_modifier
  | 'this'
  ;

parameter_mode_modifier
  : 'ref'
  | 'out'
  | 'in'
  ;

parameter_array
  : attributes? 'params' array_type identifier
  ;

// Source: §15.7.1 General
property_declaration
  : attributes? property_modifier* type member_name property_body
  | attributes? property_modifier* ref_kind type member_name ref_property_body
  ;

property_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'static'
  | 'virtual'
  | 'sealed'
  | 'override'
  | 'abstract'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

property_body
  : '{' accessor_declarations '}' property_initializer?
  | '=>' expression ';'
  ;

property_initializer
  : '=' variable_initializer ';'
  ;

ref_property_body
  : '{' ref_get_accessor_declaration '}'
  | '=>' 'ref' variable_reference ';'
  ;

// Source: §15.7.3 Accessors
accessor_declarations
  : get_accessor_declaration set_accessor_declaration?
  | set_accessor_declaration get_accessor_declaration?
  ;

get_accessor_declaration
  : attributes? accessor_modifier? 'get' accessor_body
  ;

set_accessor_declaration
  : attributes? accessor_modifier? 'set' accessor_body
  ;

accessor_modifier
  : 'protected'
  | 'internal'
  | 'private'
  | 'protected' 'internal'
  | 'internal' 'protected'
  | 'protected' 'private'
  | 'private' 'protected'
  ;

accessor_body
  : block
  | '=>' expression ';'
  | ';'
  ;

ref_get_accessor_declaration
  : attributes? accessor_modifier? 'get' ref_accessor_body
  ;

ref_accessor_body
  : block
  | '=>' 'ref' variable_reference ';'
  | ';'
  ;

// Source: §15.8.1 General
event_declaration
  : attributes? event_modifier* 'event' type variable_declarators ';'
  | attributes? event_modifier* 'event' type member_name
    '{' event_accessor_declarations '}'
  ;

event_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'static'
  | 'virtual'
  | 'sealed'
  | 'override'
  | 'abstract'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

event_accessor_declarations
  : add_accessor_declaration remove_accessor_declaration
  | remove_accessor_declaration add_accessor_declaration
  ;

add_accessor_declaration
  : attributes? 'add' block
  ;

remove_accessor_declaration
  : attributes? 'remove' block
  ;

// Source: §15.9.1 General
indexer_declaration
  : attributes? indexer_modifier* indexer_declarator indexer_body
  | attributes? indexer_modifier* ref_kind indexer_declarator ref_indexer_body
  ;

indexer_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'virtual'
  | 'sealed'
  | 'override'
  | 'abstract'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

indexer_declarator
  : type 'this' '[' formal_parameter_list ']'
  | type interface_type '.' 'this' '[' formal_parameter_list ']'
  ;

indexer_body
  : '{' accessor_declarations '}'
  | '=>' expression ';'
  ;

ref_indexer_body
  : '{' ref_get_accessor_declaration '}'
  | '=>' 'ref' variable_reference ';'
  ;

// Source: §15.10.1 General
operator_declaration
  : attributes? operator_modifier+ operator_declarator operator_body
  ;

operator_modifier
  : 'public'
  | 'static'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

operator_declarator
  : unary_operator_declarator
  | binary_operator_declarator
  | conversion_operator_declarator
  ;

unary_operator_declarator
  : type 'operator' overloadable_unary_operator '(' fixed_parameter ')'
  ;

overloadable_unary_operator
  : '+' | '-' | '!' | '~' | '++' | '--' | 'true' | 'false'
  ;

binary_operator_declarator
  : type 'operator' overloadable_binary_operator
    '(' fixed_parameter ',' fixed_parameter ')'
  ;

overloadable_binary_operator
  : '+' | '-' | '*' | '/' | '%' | '&' | '|' | '^' | '<<'
  | right_shift | '==' | '!=' | '>' | '<' | '>=' | '<='
  ;

conversion_operator_declarator
  : 'implicit' 'operator' type '(' fixed_parameter ')'
  | 'explicit' 'operator' type '(' fixed_parameter ')'
  ;

operator_body
  : block
  | '=>' expression ';'
  | ';'
  ;

// Source: §15.11.1 General
constructor_declaration
  : attributes? constructor_modifier* constructor_declarator constructor_body
  ;

constructor_modifier
  : 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'extern'
  | unsafe_modifier  // unsafe code support
  ;

constructor_declarator
  : identifier '(' formal_parameter_list? ')' constructor_initializer?
  ;

constructor_initializer
  : ':' 'base' '(' argument_list? ')'
  | ':' 'this' '(' argument_list? ')'
  ;

constructor_body
  : block
  | '=>' expression ';'
  | ';'
  ;

// Source: §15.12 Static constructors
static_constructor_declaration
  : attributes? static_constructor_modifiers identifier '(' ')'
    static_constructor_body
  ;

static_constructor_modifiers
  : 'static'
  | 'static' 'extern' unsafe_modifier?
  | 'static' unsafe_modifier 'extern'?
  ;
```


| 'extern' 'static' unsafe_modifier?
| 'extern' unsafe_modifier 'static'
| unsafe_modifier 'static' 'extern'?
| unsafe_modifier 'extern' 'static'
;

static_constructor_body
: block
| '=>' expression ';'
| ';'
;

// 来源：§15.13 终结器
finalizer_declaration
: attributes? '~' identifier '(' ')' finalizer_body
| attributes? 'extern' unsafe_modifier? '~' identifier '(' ')'
finalizer_body
| attributes? unsafe_modifier 'extern'? '~' identifier '(' ')'
finalizer_body
;

finalizer_body
: block
| '=>' expression ';'
| ';'
;

// 来源：§16.2.1 一般
struct_declaration
: attributes? struct_modifier* 'ref'? 'partial'? 'struct'
identifier type_parameter_list? struct_interfaces?
type_parameter_constraints_clause* struct_body ';'?
;

// 来源：§16.2.2 结构体修饰符
struct_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| 'readonly'
| unsafe_modifier   // 不安全代码支持
;

// 来源：§16.2.5 结构体接口
struct_interfaces
: ':' interface_type_list
;

// 来源：§16.2.6 结构体主体
struct_body
: '{' struct_member_declaration* '}'
;

// 来源：§16.3 结构体成员
struct_member_declaration
  : constant_declaration
  | field_declaration
  | method_declaration
  | property_declaration
  | event_declaration
  | indexer_declaration
  | operator_declaration
  | constructor_declaration
  | static_constructor_declaration
  | type_declaration
  | fixed_size_buffer_declaration  // 不安全代码支持
  ;

// 来源：§17.7 数组初始化器
array_initializer
  : '{' variable_initializer_list? '}'
  | '{' variable_initializer_list ',' '}'
  ;

variable_initializer_list
  : variable_initializer (',' variable_initializer)*
  ;

variable_initializer
  : expression
  | array_initializer
  ;

// 来源：§18.2.1 一般
interface_declaration
  : attributes? interface_modifier* 'partial'? 'interface'
    identifier variant_type_parameter_list? interface_base?
    type_parameter_constraints_clause* interface_body ';'?
  ;

// 来源：§18.2.2 接口修饰符
interface_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | unsafe_modifier  // 不安全代码支持
  ;

// 来源：§18.2.3.1 一般
variant_type_parameter_list
  : '<' variant_type_parameters '>'
  ;

// 来源：§18.2.3.1 一般
variant_type_parameters
  : attributes? variance_annotation? type_parameter
| variant_type_parameters ',' attributes? variance_annotation?
type_parameter
;

// 来源：§18.2.3.1 一般
variance_annotation
: 'in'
| 'out'
;

// 来源：§18.2.4 基接口
interface_base
: ':' interface_type_list
;

// 来源：§18.3 接口主体
interface_body
: '{' interface_member_declaration* '}'
;

// 来源：§18.4.1 一般
interface_member_declaration
: interface_method_declaration
| interface_property_declaration
| interface_event_declaration
| interface_indexer_declaration
;

// 来源：§18.4.2 接口方法
interface_method_declaration
: attributes? 'new'? return_type interface_method_header
| attributes? 'new'? ref_kind ref_return_type interface_method_header
;

interface_method_header
: identifier '(' formal_parameter_list? ')' ';'
| identifier type_parameter_list '(' formal_parameter_list? ')'
type_parameter_constraints_clause* ';'
;

// 来源：§18.4.3 接口属性
interface_property_declaration
: attributes? 'new'? type identifier '{' interface_accessors '}'
| attributes? 'new'? ref_kind type identifier '{' ref_interface_accessor '}'
;

interface_accessors
: attributes? 'get' ';'
| attributes? 'set' ';'
| attributes? 'get' ';' attributes? 'set' ';'
| attributes? 'set' ';' attributes? 'get' ';'
;

ref_interface_accessor
: attributes? 'get' ';'
;

// 来源：§18.4.4 接口事件
interface_event_declaration
  : attributes? 'new'? 'event' type identifier ';'
  ;

// 来源：§18.4.5 接口索引器
interface_indexer_declaration
  : attributes? 'new'? type 'this' '[' formal_parameter_list ']'
    '{' interface_accessors '}'
  | attributes? 'new'? ref_kind type 'this' '[' formal_parameter_list ']'
    '{' ref_interface_accessor '}'
  ;

// 来源：§19.2 枚举声明
enum_declaration
  : attributes? enum_modifier* 'enum' identifier enum_base? enum_body ';'?
  ;

enum_base
  : ':' integral_type
  | ':' integral_type_name
  ;

integral_type_name
  : type_name // 应解析为除 char 以外的整型类型
  ;

enum_body
  : '{' enum_member_declarations? '}'
  | '{' enum_member_declarations ',' '}'
  ;

// 来源：§19.3 枚举修饰符
enum_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  ;

// 来源：§19.4 枚举成员
enum_member_declarations
  : enum_member_declaration (',' enum_member_declaration)*
  ;

// 来源：§19.4 枚举成员
enum_member_declaration
  : attributes? identifier ('=' constant_expression)?
  ;

// 来源：§20.2 委托声明
delegate_declaration
: attributes? delegate_modifier* 'delegate' return_type delegate_header
| attributes? delegate_modifier* 'delegate' ref_kind ref_return_type
delegate_header
;

delegate_header
: identifier '(' formal_parameter_list? ')' ';'
| identifier variant_type_parameter_list '(' formal_parameter_list? ')'
type_parameter_constraints_clause* ';'
;

delegate_modifier
: 'new'
| 'public'
| 'protected'
| 'internal'
| 'private'
| unsafe_modifier  // 不安全代码支持
;

// 来源：§22.3 特性规范
global_attributes
: global_attribute_section+
;

global_attribute_section
: '[' global_attribute_target_specifier attribute_list ']'
| '[' global_attribute_target_specifier attribute_list ',' ']'
;

global_attribute_target_specifier
: global_attribute_target ':'
;

global_attribute_target
: identifier
;

attributes
: attribute_section+
;

attribute_section
: '[' attribute_target_specifier? attribute_list ']'
| '[' attribute_target_specifier? attribute_list ',' ']'
;

attribute_target_specifier
: attribute_target ':'
;

attribute_target
: identifier
| keyword
;

attribute_list
  : attribute (',' attribute)*
  ;

attribute
  : attribute_name attribute_arguments?
  ;

attribute_name
  : type_name
  ;

attribute_arguments
  : '(' positional_argument_list? ')'
  | '(' positional_argument_list ',' named_argument_list ')'
  | '(' named_argument_list ')'
  ;

positional_argument_list
  : positional_argument (',' positional_argument)*
  ;

positional_argument
  : argument_name? attribute_argument_expression
  ;

named_argument_list
  : named_argument (',' named_argument)*
  ;

named_argument
  : identifier '=' attribute_argument_expression
  ;

attribute_argument_expression
  : expression
  ;

## A.4 不安全代码的语法扩展

// 来源：§23.2 不安全上下文
unsafe_modifier
  : 'unsafe'
  ;

unsafe_statement
  : 'unsafe' block
  ;

// 来源：§23.3 指针类型
pointer_type
  : value_type ('*')+
  | 'void' ('*')+
;

// 来源：§23.6.2 指针间接引用
pointer_indirection_expression
  : '*' unary_expression
  ;

// 来源：§23.6.3 指针成员访问
pointer_member_access
  : primary_expression '->' identifier type_argument_list?
  ;

// 来源：§23.6.4 指针元素访问
pointer_element_access
  : primary_no_array_creation_expression '[' expression ']'
  ;

// 来源：§23.6.5 取地址运算符
addressof_expression
  : '&' unary_expression
  ;

// 来源：§23.7 fixed 语句
fixed_statement
  : 'fixed' '(' pointer_type fixed_pointer_declarators ')' embedded_statement
  ;

fixed_pointer_declarators
  : fixed_pointer_declarator (',' fixed_pointer_declarator)*
  ;

fixed_pointer_declarator
  : identifier '=' fixed_pointer_initializer
  ;

fixed_pointer_initializer
  : '&' variable_reference
  | expression
  ;

// 来源：§23.8.2 固定大小缓冲区声明
fixed_size_buffer_declaration
  : attributes? fixed_size_buffer_modifier* 'fixed' buffer_element_type fixed_size_buffer_declarators ';'
  ;

fixed_size_buffer_modifier
  : 'new'
  | 'public'
  | 'internal'
  | 'private'
  | 'unsafe'
  ;

buffer_element_type


: type
;
fixed_size_buffer_declarators
: fixed_size_buffer_declarator (',' fixed_size_buffer_declarator)*
;
fixed_size_buffer_declarator
: identifier '[' constant_expression ']'
;

资料性文本结束。

# B. 可移植性问题

**本条款为资料性内容。**

### B.1 概述

本附录收集了本规范中出现的一些关于可移植性的信息。

### B.2 未定义行为

在以下情况下，行为是未定义的：

- 1. 当 awaiter 对接口方法 `INotifyCompletion.OnCompleted` 和 `ICriticalNotifyCompletion.UnsafeOnCompleted` 的实现未能使恢复委托至多被调用一次时，外层异步函数的行为（§12.9.8.4）。
- 2. 将指针作为 `ref` 或 `out` 参数传递（§23.3）。
- 3. 当对将一种指针类型转换为另一种指针类型的结果进行解引用，且结果指针未针对所指向类型正确对齐时（§23.5.1）。
- 4. 当一元 `*` 运算符应用于包含无效值的指针时（§23.6.2）。
- 5. 当对指针进行下标访问越界元素时（§23.6.4）。
- 6. 通过固定指针修改托管类型的对象（§23.7）。
- 7. 由 `stackalloc` 新分配的内存内容（§12.8.21）。
- 8. 尝试使用 `stackalloc` 分配负数数量的项（§12.8.21）。
- 9. 带值实参的 `in` 参数（§12.6.4.2）的隐式动态转换（§10.2.10）。

### B.3 实现定义的行为

符合规范的实现需要记录其在本子条款所列每个领域中的行为选择。以下内容为实现定义的：

- 1. 遇到不在规范化形式 C 中的标识符时的行为（§6.4.3）。
- 2. `PP_Line_Indicator` 中 `Decimal_Digit+` 允许的最大 `value`（§6.5.8）。
- 3. `#pragma` 指令的 `pp_pragma_text` 中 `input_characters` 的解释（§6.5.9）。
- 4. 应用程序启动前由宿主环境传递给 `Main` 的任何应用程序参数的值（§7.1）。
- 5. 当匿名函数转换为表达式树时，表达式树的精确结构以及创建它的确切过程（§10.7.3）。
- 6. 在 `unchecked` 上下文中，当整数除法的左操作数为最大负 int 或 long 值且右操作数为 -1 时，是引发 `System.ArithmeticException`（或其子类），还是不上报溢出并以左操作数的值作为结果值（§12.10.3）。
- 7. 执行 decimal 求余运算时引发 System.ArithmeticException（或其子类）的情况（§12.10.4）。
- 8. 当线程没有异常处理程序且该线程自身被终止时，线程终止的影响（§13.10.6）。
- 9. 当未找到与异常匹配的 catch 子句，并且执行到最初启动该线程的代码时，线程终止的影响（§21.4）。
- 10. 指针与整数之间的映射（§23.5.1）。
- 11. 将一元 * 运算符应用于 null 指针的效果（§23.6.2）。
- 12. 指针算术溢出指针类型的域时的行为（§23.6.6、§23.6.7）。
- 13. 对非预定义值类型使用 sizeof 运算符的结果（§23.6.9）。
- 14. 如果数组表达式为 null 或数组元素数为零，fixed 语句的行为（§23.7）。
- 15. 如果字符串表达式为 null，fixed 语句的行为（§23.7）。
- 16. 进行大小为零的堆栈分配时返回的值（§12.8.21）。

### B.4 未指定行为

- 1. 对象一旦有资格进行终结，其终结器（如果有）运行的时间（§7.9）。
- 2. true 的表示形式（§8.3.9）。
- 3. 在 unchecked 上下文中将超出范围的 float 或 double 值转换为整型时的结果值（§10.3.2）。
- 4. 由 anonymous_method_expression 包含内容生成的委托的确切目标对象和目标方法（§10.7.2）。
- 5. 数组的布局，但在不安全上下文中除外（§12.8.16.5）。
- 6. 除了通过求值和调用 lambda_expression 或 anonymous_method-expression 之外，是否存在任何方式执行匿名函数的块（§12.19.3）。
- 7. 静态字段初始化的确切时机（§15.5.6.2）。
- 8. 当枚举器对象处于 running 状态时调用 MoveNext 的结果（§15.14.5.2）。
- 9. 当枚举器对象处于 before、running 或 after 状态时访问 Current 的结果（§15.14.5.3）。
- 10. 当枚举器对象处于 running 状态时调用 Dispose 的结果（§15.14.5.4）。
- 11. 分部声明类型的特性通过以未指定顺序合并其各个部分的特性来确定（§22.3）。
- 12. 成员打包到结构中的顺序（§23.6.9）。
- 13. 终结器执行期间发生异常，且该异常未被捕获（§21.4）。
- 14. 如果有多个成员匹配，哪个成员是 I.M 的实现（§18.6.5）。

### B.5 其他问题

- 1. 浮点表达式求值的精确结果可能因实现而异，因为允许实现使用比所需更大的范围和/或精度来求值此类表达式（§8.3.7）。
- 2. CLI 保留某些签名以兼容其他编程语言（§15.3.10）。

资料性文本结束。

# C. 标准库

### C.1 概述

符合规范的 C# 实现应提供一组具有特定语义的最小类型集。这些类型及其成员在此按命名空间和类型的字母顺序列出。关于这些类型及其成员的形式定义，请参阅 ISO/IEC 23271:2012《公共语言基础结构（CLI）》第 IV 部分；基类库（BCL）、扩展数值库和扩展数组库，这些内容通过引用并入本规范。

**本文为资料性内容。**

标准库旨在成为符合规范的 C# 实现所需的最小类型和成员集。因此，它仅包含 C# 语言规范明确要求的那些成员。

预期符合规范的 C# 实现将提供显著更广泛的库，以便编写有用的程序。例如，符合规范的实现可以通过以下方式扩展此库：

- 添加命名空间。
- 添加类型。
- 向非接口类型添加成员。
- 添加中间基类或接口。
- 使结构和类类型实现附加接口。
- 向现有类型和成员添加特性（ConditionalAttribute 除外）。

**资料性文本结束。**

### C.2 ISO/IEC 23271 中定义的标准库类型

*注：* 下文中某些结构类型具有 readonly 修饰符。ISO/IEC 23271 发布时此修饰符尚不可用，但本规范的符合实现需要它。
*注结束*

```
namespace System
{
    public delegate void Action();
    public class ArgumentException : SystemException
    {
        public ArgumentException();
        public ArgumentException(string message);
        public ArgumentException(string message, Exception innerException);
    }
    public class ArithmeticException : Exception
{
    public ArithmeticException();
    public ArithmeticException(string message);
    public ArithmeticException(string message, Exception innerException);
}

public abstract class Array : IList, ICollection, IEnumerable
{
    public int Length { get; }
    public int Rank { get; }
    public int GetLength(int dimension);
}

public class ArrayTypeMismatchException : Exception
{
    public ArrayTypeMismatchException();
    public ArrayTypeMismatchException(string message);
    public ArrayTypeMismatchException(string message,
        Exception innerException);
}

[AttributeUsageAttribute(AttributeTargets.All, Inherited = true,
    AllowMultiple = false)]
public abstract class Attribute
{
    protected Attribute();
}

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

[AttributeUsageAttribute(AttributeTargets.Class, Inherited = true)]
public sealed class AttributeUsageAttribute : Attribute
{
    public AttributeUsageAttribute(AttributeTargets validOn);
    public bool AllowMultiple { get; set; }
    public bool Inherited { get; set; }
    public AttributeTargets ValidOn { get; }
}
```

}
public readonly struct Boolean { }
public readonly struct Byte { }
public readonly struct Char { }
public readonly struct Decimal { }
public abstract class Delegate { }

public class DivideByZeroException : ArithmeticException
{
    public DivideByZeroException();
    public DivideByZeroException(string message);
    public DivideByZeroException(string message, Exception innerException);
}

public readonly struct Double { }

public abstract class Enum : ValueType
{
    protected Enum();
}

public class Exception
{
    public Exception();
    public Exception(string message);
    public Exception(string message, Exception innerException);
    public sealed Exception InnerException { get; }
    public virtual string Message { get; }
}

public class GC { }

public interface IDisposable
{
    void Dispose();
}

public interface IFormattable { }

public sealed class IndexOutOfRangeException : Exception
{
    public IndexOutOfRangeException();
    public IndexOutOfRangeException(string message);
    public IndexOutOfRangeException(string message,
        Exception innerException);
}

public readonly struct Int16 { }
public readonly struct Int32 { }
public readonly struct Int64 { }
public readonly struct IntPtr { }

public class InvalidCastException : Exception
{
public InvalidCastException();
public InvalidCastException(string message);
public InvalidCastException(string message, Exception innerException);
}

public class InvalidOperationException : Exception
{
    public InvalidOperationException();
    public InvalidOperationException(string message);
    public InvalidOperationException(string message,
        Exception innerException);
}

public class NotSupportedException : Exception
{
    public NotSupportedException();
    public NotSupportedException(string message);
    public NotSupportedException(string message, Exception innerException);
}

public struct Nullable<T>
{
    public bool HasValue { get; }
    public T Value { get; }
}

public class NullReferenceException : Exception
{
    public NullReferenceException();
    public NullReferenceException(string message);
    public NullReferenceException(string message, Exception innerException);
}

public class Object
{
    public Object();
    ~Object();
    public virtual bool Equals(object obj);
    public virtual int GetHashCode();
    public Type GetType();
    public virtual string ToString();
}

[AttributeUsageAttribute(AttributeTargets.Class | AttributeTargets.Struct |
    AttributeTargets.Enum | AttributeTargets.Interface |
    AttributeTargets.Constructor | AttributeTargets.Method |
    AttributeTargets.Property | AttributeTargets.Field |
    AttributeTargets.Event | AttributeTargets.Delegate, Inherited = false)]
public sealed class ObsoleteAttribute : Attribute
{
    public ObsoleteAttribute();
    public ObsoleteAttribute(string message);
    public ObsoleteAttribute(string message, bool error);
    public bool IsError { get; }
    public string Message { get; }
}
public ValueTuple(T1 item1, T2 item2);
}
public struct ValueTuple<T1, T2, T3>
{
    public T1 Item1;
    public T2 Item2;
    public T3 Item3;
    public ValueTuple(T1 item1, T2 item2, T3 item3);
}
public struct ValueTuple<T1, T2, T3, T4>
{
    public T1 Item1;
    public T2 Item2;
    public T3 Item3;
    public T4 Item4;
    public ValueTuple(T1 item1, T2 item2, T3 item3, T4 item4);
}
public struct ValueTuple<T1, T2, T3, T4, T5>
{
    public T1 Item1;
    public T2 Item2;
    public T3 Item3;
    public T4 Item4;
    public T5 Item5;
    public ValueTuple(T1 item1, T2 item2, T3 item3, T4 item4, T5 item5);
}
public struct ValueTuple<T1, T2, T3, T4, T5, T6>
{
    public T1 Item1;
    public T2 Item2;
    public T3 Item3;
    public T4 Item4;
    public T5 Item5;
    public T6 Item6;
    public ValueTuple(T1 item1, T2 item2, T3 item3, T4 item4, T5 item5, T6 item6);
}
public struct ValueTuple<T1, T2, T3, T4, T5, T6, T7>
{
    public T1 Item1;
    public T2 Item2;
    public T3 Item3;
    public T4 Item4;
    public T5 Item5;
    public T6 Item6;
    public T7 Item7;
    public ValueTuple(T1 item1, T2 item2, T3 item3, T4 item4, T5 item5, T6 item6, T7 item7);
}
public struct ValueTuple<T1, T2, T3, T4, T5, T6, T7, TRest>
{
    public T1 Item1;
    public T2 Item2;
    public T3 Item3;
    public T4 Item4;
public T5 Item5;
public T6 Item6;
public T7 Item7;
public TRest Rest;
public ValueTuple(T1 item1, T2 item2, T3 item3, T4 item4, T5 item5,
    T6 item6, T7 item7, TRest rest);
}

public abstract class ValueType
{
    protected ValueType();
}
}

namespace System.Collections
{
public interface ICollection : IEnumerable
{
    int Count { get; }
    bool IsSynchronized { get; }
    object SyncRoot { get; }
    void CopyTo(Array array, int index);
}

public interface IEnumerable
{
    IEnumerator GetEnumerator();
}

public interface IEnumerator
{
    object Current { get; }
    bool MoveNext();
    void Reset();
}

public interface IList : ICollection, IEnumerable
{
    bool IsFixedSize { get; }
    bool IsReadOnly { get; }
    object this[int index] { get; set; }
    int Add(object value);
    void Clear();
    bool Contains(object value);
    int IndexOf(object value);
    void Insert(int index, object value);
    void Remove(object value);
    void RemoveAt(int index);
}
}

namespace System.Collections.Generic
{
public interface ICollection<T> : IEnumerable<T>
{
int Count { get; }
bool IsReadOnly { get; }
void Add(T item);
void Clear();
bool Contains(T item);
void CopyTo(T[] array, int arrayIndex);
bool Remove(T item);
}

public interface IEnumerable<T> : IEnumerable
{
    IEnumerator<T> GetEnumerator();
}

public interface IEnumerator<T> : IDisposable, IEnumerator
{
    T Current { get; }
}

public interface IList<T> : ICollection<T>
{
    T this [int index] { get; set; }
    int IndexOf(T item);
    void Insert(int index, T item);
    void RemoveAt(int index);
}

public interface IReadOnlyCollection<out T> : IEnumerable<T>
{
    int Count { get; }
}

public interface IReadOnlyList<out T> : IReadOnlyCollection<T>
{
    T this [int index] { get; }
}

namespace System.Diagnostics
{
    [AttributeUsageAttribute(AttributeTargets.Method | AttributeTargets.Class,
    AllowMultiple = true)]
    public sealed class ConditionalAttribute : Attribute
    {
        public ConditionalAttribute(string conditionString);
        public string ConditionString { get; }
    }
}

namespace System.Reflection
{
    public abstract class MemberInfo
    {
        protected MemberInfo();
    }
}
}
[AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
public sealed class CallerFilePathAttribute : Attribute
{
    public CallerFilePathAttribute() { }
}

[AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
public sealed class CallerLineNumberAttribute : Attribute
{
    public CallerLineNumberAttribute() { }
}

[AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
public sealed class CallerMemberNameAttribute : Attribute
{
    public CallerMemberNameAttribute() { }
}

public static class FormattableStringFactory
{
    public static FormattableString Create(string format,
        params object[] arguments);
}

public interface ICriticalNotifyCompletion : INotifyCompletion
{
    void UnsafeOnCompleted(Action continuation);
}

public interface INotifyCompletion
{
    void OnCompleted(Action continuation);
}

public readonly struct TaskAwaiter : ICriticalNotifyCompletion,
    INotifyCompletion
{
    public bool IsCompleted { get; }
    public void GetResult();
}

public readonly struct TaskAwaiter<TResult> : ICriticalNotifyCompletion,
    INotifyCompletion
{
    public bool IsCompleted { get; }
    public TResult GetResult();
}

public readonly struct ValueTaskAwaiter : ICriticalNotifyCompletion,
    INotifyCompletion
{
    public bool IsCompleted { get; }
    public void GetResult();
}


}
public readonly struct ValueTaskAwaiter<TResult>
: ICriticalNotifyCompletion, INotifyCompletion
{
    public bool IsCompleted { get; }
    public TResult GetResult();
}
}

namespace System.Threading.Tasks
{
    public class Task
    {
        public System.Runtime.CompilerServices.TaskAwaiter GetAwaiter();
    }
    public class Task<TResult> : Task
    {
        public new System.Runtime.CompilerServices.TaskAwaiter<T> GetAwaiter();
    }
    public readonly struct ValueTask : System.IEquatable<ValueTask>
    {
        public System.Runtime.CompilerServices.ValueTaskAwaiter GetAwaiter();
    }
    public readonly struct ValueTask<TResult>
    : System.IEquatable<ValueTask<TResult>>
    {
        public new System.Runtime.CompilerServices.ValueTaskAwaiter<TResult> GetAwaiter();
    }
}
namespace System
{
    public readonly ref struct ReadOnlySpan<T>
    {
        public int Length { get; }
        public ref readonly T this[int index] { get; }
    }
    public readonly ref struct Span<T>
    {
        public int Length { get; }
        public ref T this[int index] { get; }
        public static implicit operator ReadOnlySpan<T>(Span<T> span);
    }
}

## C.4 格式规范

格式的含义，如在插值字符串表达式（§12.8.3）中使用，已在 ISO/IEC 23271:2012 中定义。为方便起见，以下文本摘自 System.IFormattable 的描述。

**本文为说明性内容。**

格式是一个字符串，用于描述对象转换为字符串时的外观。可以采用标准格式或自定义格式。标准格式的形式为 Axx，其中 A 是一个称为格式说明符的单个字母字符，xx 是一个介于零和 99 之间的整数，称为精度说明符。格式说明符控制应用于作为字符串表示的值的格式类型。精度说明符控制字符串中的有效数字或小数位数，如果适用。

注：有关标准格式说明符的列表，请参阅下表。注意，给定的数据类型，例如 System.Int32，可能不支持一个或多个标准格式说明符。结束注

注：当格式包含因文化而异的符号时，例如 'C' 和 'c' 格式包含的货币符号，则格式化对象提供在字符串表示中使用的实际字符。方法可能包含一个参数以传递提供格式化对象的 System.IFormatProvider 对象，或者方法可能使用默认格式化对象，其中包含当前文化的符号定义。当前文化通常默认使用系统范围内使用的同一组符号。在基类库中，系统提供的数值类型的格式化对象是 System.Globalization.NumberFormatInfo 实例。对于 System.DateTime 实例，则使用 System.Globalization.DateTimeFormatInfo。结束注

下表描述了在基类库中与数值数据类型一起使用的标准格式说明符以及关联的格式化对象成员。

| 格式说明符 | 描述 |
|---|---|
| C c | **货币格式：** 用于包含货币值的字符串。System.Globalization.NumberFormatInfo 的 System.Globalization.NumberFormatInfo.CurrencySymbol、System.Globalization.NumberFormatInfo.CurrencyGroupSizes、System.Globalization.NumberFormatInfo.CurrencyGroupSeparator 和 System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator 成员分别提供货币符号、数字分组的大小和分隔符以及小数分隔符。System.Globalization.NumberFormatInfo.CurrencyNegativePattern 和 System.Globalization.NumberFormatInfo.CurrencyPositivePattern 确定用于表示负值和正值的符号。例如，负值可以加上减号前缀，或用括号括起来。如果省略精度说明符，则 System.Globalization.NumberFormatInfo.CurrencyDecimalDigits 确定字符串中的小数位数。必要时结果会四舍五入到最接近的可表示值。 |
| D d | **十进制格式：** （此格式仅在与整数数据类型一起指定时有效。）用于包含整数值的字符串。负数前面加上 System.Globalization.NumberFormatInfo.NegativeSign 属性指定的负数符号。精度说明符决定字符串中出现的最小位数。如果指定的精度需要的位数多于值包含的位数，则字符串会用零左填充。如果精度说明符指定的位数少于值中的位数，则忽略精度说明符。 |
| E e | **科学（工程）格式：** 用于以下其中一种形式的字符串：<br>[-]m.ddddde+xxx<br>[-]m.ddddde-xxx<br>[-]m.ddddde+xxx<br>[-]m.ddddde-xxx<br>负数符号（'-'）仅在值为负时出现，并由 System.Globalization.NumberFormatInfo.NegativeSign 属性提供。<br>恰好一个非零十进制数字（m）在小数分隔符（'.'）之前，该分隔符由 System.Globalization.NumberFormatInfo.NumberDecimalSeparator 属性提供。<br>精度说明符决定字符串中的小数位数（ddddd）。如果省略精度说明符，则字符串中包含六位小数。<br>指数（+/-xxx）由正号或负号后跟至少三位数字（xxx）组成。必要时指数会用零左填充。格式说明符的字母大小写（'E' 或 'e'）决定字符串中指数前缀使用的大小写（E 或 e）。必要时结果会四舍五入到最接近的可表示值。正数符号由 System.Globalization.NumberFormatInfo.PositiveSign 属性提供。 |
| F f | **定点格式：** 用于以下形式的字符串：<br>[-]m.dd...d<br>至少一个非零十进制数字（m）在小数分隔符（'.'）之前，该分隔符由 System.Globalization.NumberFormatInfo.NumberDecimalSeparator 属性提供。<br>负数符号（'-'）仅在值为负时位于 m 之前。此符号由 System.Globalization.NumberFormatInfo.NegativeSign 属性提供。<br>精度说明符决定字符串中的小数位数（dd...d）。如果省略精度说明符，则 System.Globalization.NumberFormatInfo.NumberDecimalDigits 决定字符串中的小数位数。必要时结果会四舍五入到最接近的可表示值。 |
| G g | **常规格式：** 字符串以定点格式（'F' 或 'f'）或科学格式（'E' 或 'e'）格式化。<br>对于整数类型：<br>如果 *指数* < 精度说明符，则使用定点格式格式化值，其中 *指数* 是值在科学格式中的指数。对于所有其他值，使用科学格式。<br>如果省略精度说明符，则使用等于显示数据类型最大值所需字段宽度的默认精度，这会导致值以定点格式格式化。整数类型的默认精度如下：<br>`System.Int16, System.UInt16 : 5`<br>`System.Int32, System.UInt32 : 10`<br>`System.Int64, System.UInt64 : 19`<br>对于 Single、Decimal 和 Double 类型：<br>如果 *指数* ≥ -4 且 *指数* < 精度说明符，则使用定点格式格式化值，其中 *指数* 是值在科学格式中的指数。对于所有其他值，使用科学格式。必要时结果会四舍五入到最接近的可表示值。<br>如果省略精度说明符，则使用以下默认精度：<br>`System.Single : 7`<br>`System.Double : 15`<br>`System.Decimal : 29`<br>对于所有类型：<br>- 结果中出现的位数（不包括指数）不会超过精度说明符的值；必要时值会被舍入。<br>- 小数点和小数点后的任何尾随零在可能的情况下会被移除。<br>- 格式说明符的字母大小写（'G' 或 'g'）决定科学格式指数前使用 'E' 还是 'e'。 |
| N n | **数字格式：** 用于以下形式的字符串：<br>`[-]d,ddd,ddd.dd...d`<br>负值的表示由 `System.Globalization.NumberFormatInfo.NumberNegativePattern` 属性决定。如果模式包含负数符号（'-'），则该符号由 `System.Globalization.NumberFormatInfo.NegativeSign` 属性提供。<br>至少一个非零十进制数字（*d*）位于小数分隔符（'.'）之前，该分隔符由 `System.Globalization.NumberFormatInfo.NumberDecimalSeparator` 属性提供。数字之间的小数点与值中最显著数字之间的数字使用 `System.Globalization.NumberFormatInfo.NumberGroupSizes` 属性指定的组大小进行分组。该组 |


| **格式说明符** | **描述** |
|---|---|
| N<br>n | 每组数字之间插入分隔符（","），并由 System.Globalization.NumberFormatInfo.NumberGroupSeparator 属性提供。<br><br>精度说明符确定小数位数（dd...d）。如果省略精度说明符，则 System.Globalization.NumberFormatInfo.NumberDecimalDigits 确定字符串中的小数位数。必要时将结果舍入到最接近的可表示值。 |
| P<br>p | **百分比格式：** 用于包含百分比的字符串。System.Globalization.NumberFormatInfo 的 System.Globalization.NumberFormatInfo.PercentSymbol、System.Globalization.NumberFormatInfo.PercentGroupSizes、System.Globalization.NumberFormatInfo.PercentGroupSeparator 和 System.Globalization.NumberFormatInfo.PercentDecimalSeparator 成员分别提供百分号、数字分组的大小和分隔符以及小数点分隔符。<br><br>System.Globalization.NumberFormatInfo.PercentNegativePattern 和 System.Globalization.NumberFormatInfo.PercentPositivePattern 确定用于表示负值和正值的符号。例如，负值可以加上负号前缀，或用括号括起来。<br><br>如果未指定精度，则结果中的小数位数由 System.Globalization.NumberFormatInfo.PercentDecimalDigits 确定。必要时将结果舍入到最接近的可表示值。<br><br>结果按 100 缩放（.99 变成 99%）。 |
| R<br>r | **往返格式：**（此格式仅在配合 System.Double 或 System.Single 指定时有效。）用于确保浮点值的字符串表示形式的精度，使得解析该字符串时与原始值相比不会导致精度损失。如果数据类型的最大精度（System.Single 为 7，System.Double 为 15）会导致精度损失，则精度增加两位小数。如果为此格式说明符提供精度说明符，则忽略它。除此之外，此格式与定点格式相同。 |
| X<br>x | **十六进制格式：**（此格式仅在配合整型数据类型指定时有效。）用于数字的基 16 字符串表示形式。精度确定字符串中的最小位数。如果精度指定的位数多于数字包含的位数，则数字左侧用零填充。格式说明符的大小写（'X' 或 'x'）决定十六进制表示中使用大写还是小写字母。 |

如果数值是值为 NaN、PositiveInfinity 或 NegativeInfinity 的 System.Single 或 System.Double，则忽略格式说明符，并返回以下之一：
System.Globalization.NumberFormatInfo.NaNSymbol,

```
System.Globalization.NumberFormatInfo.PositiveInfinitySymbol, or
System.Globalization.NumberFormatInfo.NegativeInfinitySymbol.
```

自定义格式是指任何指定为格式的字符串，只要不是上述标准格式字符串（Axx）的形式。下表描述构造自定义格式时使用的字符。

| 格式说明符 | 描述 |
|---|---|
| 0（零） | **零占位符：** 如果要格式化的值在自定义格式中出现 '0' 的位置上有数字，则该数字复制到输出字符串；否则在该位置存储零。小数点分隔符前最左侧 '0' 和小数点分隔符后最右侧 '0' 的位置确定输出字符串中始终存在的数字范围。 |
小数点分隔符后的零和/或数字占位符的数量确定小数点分隔符后出现的位数。根据需要舍入值。 |
| # | **数字占位符：** 如果要格式化的值在自定义格式中出现 '#' 的位置上有数字，则该数字复制到输出字符串；否则在该位置的输出字符串中不存储任何内容。注意，如果 '0' 不是有效数字，则此说明符从不存储 '0' 字符，即使 '0' 是字符串中唯一的数字。（如果 '0' 是有效数字，它确实会在输出字符串中显示 '0' 字符。） |
小数点分隔符后的零和/或数字占位符的数量确定小数点分隔符后出现的位数。根据需要舍入值。 |
| .（句点） | **小数点分隔符：** 格式字符串中最左侧的 '.' 字符确定格式化值中小数点分隔符的位置；任何其他 '.' 字符都被忽略。System.Globalization.NumberFormatInfo.NumberDecimalSeparator 属性确定用作小数点分隔符的符号。 |
| ,（逗号） | **组分隔符和数字缩放：** ',' 字符有两个用途。首先，如果自定义格式在两个零或数字占位符（0 或 #）之间以及小数点分隔符（如果存在）的左侧包含此字符，则输出将在小数点分隔符左侧的每组数字之间插入组分隔符。System.Globalization.NumberFormatInfo.NumberGroupSeparator 和 System.Globalization.NumberFormatInfo.NumberGroupSizes 属性分别确定用作组分隔符的符号和每组中的位数。 |
如果格式字符串在小数点分隔符的左侧紧邻一个或多个 ',' 字符，则数字将被缩放。缩放因子由小数点分隔符左侧紧邻的组分隔符字符数确定。如果有 x 个字符，则值在格式化前除以 1000^x。例如，格式字符串 '0,' 会将值除以一百万。注意，用于指示缩放的 ',' 字符的存在不会在输出字符串中插入组分隔符。因此，要将数字缩放一百万倍并插入组分隔符，请使用类似于 '#,#0.' 的自定义格式。 |
| %（百分比） | **百分比占位符：** 自定义格式中出现 '%' 字符会使数字在格式化前乘以 100。百分号插入到输出字符串中格式字符串出现 '%' 的位置。System.Globalization.NumberFormatInfo.PercentSymbol 属性确定百分号。 |
| E0
E+0
E-0
e0
e+0
e-0 | **工程格式：** 如果自定义格式中出现字符串 'E'、'E+'、'E-'、'e'、'e+' 或 'e-' 中的任何一个，并且紧随其后至少有一个 '0' 字符，则使用科学记数法格式化值。指数前缀（E 或 e）后的 '0' 字符数确定指数中的最小位数。'E+' 和 'e+' 格式表示正数或负数符号始终位于指数之前。'E'、'E-'、'e' 或 'e-' 格式表示负数符号位于负指数之前；正指数前不加符号。正数符号由 System.Globalization.NumberFormatInfo.PositiveSign 属性提供。负数符号由 System.Globalization.NumberFormatInfo.NegativeSign 属性提供。 |
| \（反斜杠） | **转义字符：** 在某些语言（如 C#）中，反斜杠字符使自定义格式中的下一个字符被解释为转义序列。它与 C 语言格式序列一起使用，例如 '\n'（换行）。在某些语言中，转义字符本身在用作字面量时需要以转义字符为前缀。否则，编译器将该字符解释为转义序列。并非所有编程语言都要求支持此转义字符。 |
| 'ABC'
"ABC" | **字面量字符串：** 用单引号或双引号括起来的字符按字面复制到输出字符串，并且不影响格式设置。 |
| ;（分号） | **节分隔符：** ';' 字符用于分隔格式字符串中正数、负数和零的节。（此功能在下面详细描述。） |
| 其他 | **所有其他字符：** 所有其他字符按其出现的位置作为字面量存储在输出字符串中。 |

请注意，对于定点格式字符串（不包含 'E0'、'E+0'、'E-0'、'e0'、'e+0' 或 'e-0' 的字符串），数字舍入到小数点分隔符右侧零或数字占位符数量所指定的小数位数。如果自定义格式不包含小数点分隔符，则数字舍入到最接近的整数。如果数字的位数多于小数点分隔符左侧的零或数字占位符数量，则多余的数字复制到输出字符串中紧邻第一个零或数字占位符之前。

自定义格式最多可以包含三个由节分隔符字符分隔的节，以分别指定正数、负数和零值的不同格式。这些节的解释如下：


-   **一节：** 自定义格式适用于所有值（正值、负值和零）。负值包含负号。
-   **两节：** 第一节适用于正值和零，第二部分适用于负值。如果要格式化的值为负，但在根据第二部分的格式舍入后变为零，则所得的零将按照第一部分进行格式化。负值不包含负号，以便完全控制负值的表示。例如，负值可以用括号表示，使用类似 '####.####;(####.####)' 的自定义格式。
-   **三节：** 第一节适用于正值，第二部分适用于负值，第三部分适用于零。第二部分可以为空（分号之间没有任何内容），在这种情况下，第一部分适用于所有非零值，且负值包含负号。如果要格式化的数字是非零的，但在根据第一或第二部分的格式舍入后变为零，则所得的零将按照第三部分进行格式化。

`System.Enum` 和 `System.DateTime` 类型也支持使用格式说明符来格式化值的字符串表示。特定格式说明符的含义根据被格式化的数据类型（数字、日期/时间、枚举）而变化。有关每种类型支持的格式说明符的完整列表，请参阅 `System.Enum` 和 `System.Globalization.DateTimeFormatInfo`。

## C.5 库类型缩写

以下库类型在本规范中被引用。包括全局命名空间限定符在内的这些类型的完整名称如下所列。在整个本规范中，这些类型出现的形式为完全限定名称；省略全局命名空间限定符；或作为简单的非限定类型名称，同时省略命名空间。例如，类型 `ICollection<T>` 在本规范中使用时，始终表示类型 `global::System.Collections.Generic.ICollection<T>`。

-   `global::System.Action`
-   `global::System.ArgumentException`
-   `global::System.ArithmeticException`
-   `global::System.Array`
-   `global::System.ArrayTypeMismatchException`
-   `global::System.Attribute`
-   `global::System.AttributeTargets`
-   `global::System.AttributeUsageAttribute`
-   `global::System.Boolean`
-   `global::System.Byte`
-   `global::System.Char`
-   `global::System.Collections.Generic.ICollection<T>`
-   `global::System.Collections.Generic.IEnumerable<T>`
-   `global::System.Collections.Generic.IEnumerator<T>`
-   `global::System.Collections.Generic.IList<T>`
-   `global::System.Collections.Generic.IReadOnlyCollection<out T>`
-   `global::System.Collections.Generic.IReadOnlyList<out T>`
-   `global::System.Collections.Generic.ICollection`
-   `global::System.Collections.IEnumerable`
-   `global::System.Collections.IList`
-   `global::System.Collections.IEnumerator`
-   `global::System.Decimal`
-   `global::System.Delegate`
-   `global::System.Diagnostics.ConditionalAttribute`
-   `global::System.DivideByZeroException`
-   `global::System.Double`
-   `global::System.Enum`
-   `global::System.Exception`
-   `global::System.GC`
-   `global::System.ICollection`
-   `global::System.IDisposable`
-   `global::System.IEnumerable`
-   `global::System.IEnumerable<out T>`
-   `global::System.IList`
-   `global::System.IndexOutOfRangeException`
-   `global::System.Int16`
-   `global::System.Int32`
-   `global::System.Int64`
-   `global::System.IntPtr`
-   `global::System.InvalidCastException`
-   `global::System.InvalidOperationException`
-   `global::System.Linq.Expressions.Expression<TDelegate>`
-   `global::System.MemberInfo`
-   `global::System.NotSupportedException`
-   `global::System.Nullable<T>`
-   `global::System.NullReferenceException`
-   `global::System.Object`
-   `global::System.ObsoleteAttribute`
-   `global::System.OutOfMemoryException`
-   `global::System.OverflowException`
-   `global::System.Runtime.CompilerServices.CallerFileAttribute`
-   `global::System.Runtime.CompilerServices.CallerLineNumberAttribute`
-   `global::System.Runtime.CompilerServices.CallerMemberNameAttribute`
-   `global::System.Runtime.CompilerServices.ICriticalNotifyCompletion`
-   `global::System.Runtime.CompilerServices.IndexerNameAttribute`
-   `global::System.Runtime.CompilerServices.INotifyCompletion`
-   `global::System.Runtime.CompilerServices.TaskAwaiter`
-   `global::System.Runtime.CompilerServices.TaskAwaiter<T>`
-   `global::System.SByte`
-   `global::System.Single`
-   `global::System.StackOverflowException`
-   `global::System.String`
-   `global::System.SystemException`
-   `global::System.Threading.Monitor`
-   `global::System.Threading.Tasks.Task`
-   `global::System.Threading.Tasks.Task<TResult>`
-   `global::System.Type`
-   `global::System.TypeInitializationException`
-   `global::System.UInt16`
-   `global::System.UInt32`
-   `global::System.UInt64`
-   `global::System.UIntPtr`
-   `global::System.ValueType`

**信息性文本结束。**

# D. 文档注释

本附录为信息性。

### D.1 总则

C# 提供了使程序员能够使用包含 XML 文本的注释语法来记录其代码的机制。在源代码文件中，具有特定形式的注释可用于指示工具从这些注释及其前面的源代码元素生成 XML。使用此类语法的注释称为文档注释。它们必须紧跟在用户定义的类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。XML 生成工具称为文档生成器。（该生成器可以是，但不必是 C# 编译器本身。）文档生成器产生的输出称为文档文件。文档文件用作文档查看器的输入；该工具旨在以某种方式可视化显示类型信息及其相关文档。

符合标准的 C# 编译器不需要检查文档注释的语法；此类注释只是普通注释。然而，符合标准的编译器允许进行此类检查。

本规范建议了一组可在文档注释中使用的标准标签，但使用这些标签不是必需的，如果需要，也可以使用其他标签，只要遵循 well-formed XML 的规则即可。对于面向 CLI 的 C# 实现，它还提供了有关文档生成器和文档文件格式的信息。未提供有关文档查看器的信息。

### D.2 引言

具有特定形式的注释可用于指示工具从这些注释及其前面的源代码元素生成 XML。此类注释是 Single-Line_Comments (§6.3.3)，以三个斜杠 (///) 开头，或 Delimited_Comments (§6.3.3)，以斜杠和两个星号 (/**) 开头。它们必须紧跟在它们注释的用户定义类型或成员之前。属性部分 (§22.3) 被视为声明的一部分，因此文档注释必须位于应用于类型或成员的属性之前。

为说明目的，文档注释的格式如下所示为两个语法规则：Single_Line_Doc_Comment 和 Delimited_Doc_Comment。然而，这些规则不是 C# 语法的一部分，而是分别代表 Single_Line_Comment 和 Delimited_Comment 词法分析规则的特定格式。

语法：

```
Single_Line_Doc_Comment
  : '///' Input_Character*
  ;

Delimited_Doc_Comment
  : '/**' Delimited_Comment_Section* ASTERISK+ '/'
  ;
```

在 Single_Line_Doc_Comment 中，如果在当前 Single_Line_Doc_Comment 相邻的每个 Single_Line_Doc_Comments 之后有 Whitespace 字符跟随 /// 字符，则该 Whitespace 字符不包含在 XML 输出中。

在 Delimited_Doc_Comment 中，如果第二行的第一个非 Whitespace 字符是 ASTERISK，并且可选 Whitespace 字符和 ASTERISK 字符的相同模式在 Delimited_Doc_Comment 内的每一行开头重复，则重复模式的字符不包含在 XML 输出中。该模式可以在 ASTERISK 字符之前以及之后包含 Whitespace 字符。

### 示例：

```
/// <summary>
/// Class <>Point</> models a point in a two-dimensional plane.
/// </summary>
public class Point
{
    /// <summary>
    /// Method <>Draw</> renders the point.
    /// </summary>
    void Draw() {...}
}
```

文档注释中的文本必须根据 XML 的规则（http://www.w3.org/TR/REC-xml）良好形成。如果 XML 格式错误，将生成警告，并且文档文件将包含一条注释，说明已遇到错误。

尽管开发人员可以自由创建自己的标签集，但 §D.3 中定义了一组推荐标签。一些推荐的标签具有特殊含义：

-   <param> 标签用于描述参数。如果使用此类标签，文档生成器必须验证指定的参数是否存在，并且所有参数都在文档注释中描述。如果此类验证失败，文档生成器将发出警告。
-   <cref> 属性可以附加到任何标签以提供对代码元素的引用。文档生成器必须验证此代码元素是否存在。如果验证失败，文档生成器将发出警告。在查找 <cref> 属性中描述的名称时，文档生成器必须根据源代码中出现的 using 语句尊重命名空间可见性。对于泛型代码元素，不能使用正常的泛型语法（例如，“List<T>”），因为它会产生无效的 XML。可以使用大括号代替方括号（例如，“List{T}”），或使用 XML 转义语法（例如，“List&lt;T&gt;”）。
-   <summary> 标签旨在由文档查看器使用，以显示有关类型或成员的附加信息。
-   <include> 标签包含来自外部 XML 文件的信息。

请注意，文档文件并不提供有关类型和成员的完整信息（例如，它不包含任何类型信息）。要获取有关类型或成员的此类信息，必须将文档文件与对该类型或成员的反射结合使用。



## D.3 推荐标签

### D.3.1 通用

文档生成器必须接受并处理根据 XML 规则有效的所有标签。以下标签在用户文档中提供常用功能。（当然，其他标签也是可能的。）

| 标签 | 参考 | 用途 |
|---|---|---|
| `<c>` | §D.3.2 | 将文本设置为类似代码的字体 |
| `<code>` | §D.3.3 | 设置一行或多行源代码或程序输出 |
| `<example>` | §D.3.4 | 指示一个示例 |
| `<exception>` | §D.3.5 | 标识方法可能抛出的异常 |
| `<include>` | §D.3.6 | 从外部文件包含 XML |
| `<list>` | §D.3.7 | 创建列表或表格 |
| `<para>` | §D.3.8 | 允许向文本添加结构 |
| `<param>` | §D.3.9 | 描述方法或构造函数的参数 |
| `<paramref>` | §D.3.10 | 标识某个词是参数名 |
| `<permission>` | §D.3.11 | 记录成员的安全可访问性 |
| `<remarks>` | §D.3.12 | 描述类型附加信息 |
| `<returns>` | §D.3.13 | 描述方法的返回值 |
| `<see>` | §D.3.14 | 指定链接 |
| `<seealso>` | §D.3.15 | 生成“另请参阅”条目 |
| `<summary>` | §D.3.16 | 描述类型或类型的成员 |
| `<typeparam>` | §D.3.17 | 描述泛型类型或方法的类型参数 |
| `<typeparamref>` | §D.3.18 | 标识某个词是类型参数名 |
| `<value>` | §D.3.19 | 描述属性 |

### D.3.2 <c>

此标签提供一种机制，用于指示描述中的文本片段应使用特殊字体设置，例如用于代码块的字体。对于实际代码行，请使用 <code> (§D.3.3)。

**Syntax:**

```
<c>text</c>
```

**Example:**

```
/// <summary>
/// Class <c>Point</c> models a point in a two-dimensional plane.
/// </summary>
public class Point
{
}
```

### D.3.3 <code>

此标签用于以某种特殊字体设置一行或多行源代码或程序输出。对于叙述中的小代码片段，请使用 <c> (§D.3.2)。

Syntax:

```
<code>source code or program output</code>
```

Example:

```
public class Point
{
    /// <summary>
    /// This method changes the point's location by the given x- and y-offsets.
    /// <example>
    /// For example:
    /// <code>
    /// Point p = new Point(3,5);
    /// p.Translate(-1,3);
    /// </code>
    /// results in <c>p</c>'s having the value (2,8).
    /// </example>
    /// </summary>
    public void Translate(int dx, int dy)
    {
        ...
    }
}
```

### D.3.4 <example>

此标签允许在注释中包含示例代码，以指定方法或其他库成员可能如何使用。通常，这也涉及使用 <code> (§D.3.3) 标签。

Syntax:

```
<example>description</example>
```

Example:

See <code> (§D.3.3) for an example.

### D.3.5 <exception>

此标签提供一种记录方法可能抛出的异常的方式。

Syntax:

```
<exception cref="member">description</exception>
```

where

- cref="member" 是成员的名称。文档生成器检查给定成员是否存在，并将 member 翻译为文档文件中的规范元素名称。
- description 是描述异常被抛出的情况的描述。

Example:

```csharp
class MasterFileFormatCorruptException : System.Exception { ... }
class MasterFileLockedOpenException : System.Exception { ... }
public class DataBaseOperations
{
    /// <exception cref="MasterFileFormatCorruptException">
    /// Thrown when the master file is corrupted.
    /// </exception>
    /// <exception cref="MasterFileLockedOpenException">
    /// Thrown when the master file is already open.
    /// </exception>
    public static void ReadRecord(int flag)
    {
        if (flag == 1)
        {
            throw new MasterFileFormatCorruptException();
        }
        else if (flag == 2)
        {
            throw new MasterFileLockedOpenException();
        }
        ...
    }
}
```

### D.3.6 <include>

此标签允许从源代码文件外部的 XML 文档中包含信息。外部文件必须是格式良好的 XML 文档，并且会应用 XPath 表达式来指定要包含的该文档中的哪些 XML。然后 <include> 标签将被外部文档中选定的 XML 替换。

**Syntax:**

```
<include file="filename" path="xpath" />
```

where

- file="filename" 是外部 XML 文件的文件名。文件名是相对于包含 include 标签的文件解释的。
- path="xpath" 是选择外部 XML 文件中部分 XML 的 XPath 表达式。

**Example:**

如果源代码包含类似以下声明：

```
/// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class IntList { ... }
```

```
<class name="StringList">
    <summary>
        Contains a list of strings.
    </summary>
</class>
</extradoc>
```

则输出的文档与源代码包含以下内容时相同：

```
/// <summary>
/// Contains a list of integers.
/// </summary>
public class IntList { ... }
```

### D.3.7 <list>

此标签用于创建项目列表或表格。它可以包含 <listheader> 块来定义表格或定义列表的标题行。（在定义表格时，只需在标题中提供 term 的条目。）

列表中的每个项目都使用 <item> 块指定。在创建定义列表时，必须同时指定 term 和 description。然而，对于表格、项目符号列表或编号列表，只需指定 description。

**Syntax:**

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
    <item>
        <term>term</term>
        <description>description</description>
    </item>
</list>
```

where

- *term* 是要定义的术语，其定义在 *description* 中。
- *description* 是项目符号或编号列表中的一个项目，或 *term* 的定义。

**Example:**

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
public static void Main()
{
    ...
}
```

### D.3.8 <para>

此标签用于其他标签内部，例如 <summary> (§D.3.16) 或 <returns> (§D.3.13)，并允许向文本添加结构。

**Syntax:**

```
<para>content</para>
```

where

- *content* 是段落的文本。

**Example:**

```
public class Point
{
    /// <summary>This is the entry point of the Point class testing program.
    /// <para>
    /// This program tests each method and operator, and
    /// is intended to be run after any non-trivial maintenance has
    /// been performed on the Point class.
    /// </para>
    /// </summary>
    public static void Main()
    {
        ...
    }
}
```

### D.3.9 <param>

此标签用于描述方法、构造函数或索引器的参数。

**Syntax:**

```
<param name="name">description</param>
```

where

- *name* 是参数的名称。
- *description* 是参数的描述。

**Example:**

```
public class Point
{
    /// <summary>
    /// This method changes the point's location to
    /// the given coordinates.
/// </summary>
/// <param name="xPosition">the new x-coordinate.</param>
/// <param name="yPosition">the new y-coordinate.</param>
public void Move(int xPosition, int yPosition)
{
    ...
}
```

### D.3.10 <paramref>

此标签用于指示某个词是参数。文档文件可以被处理以以某种独特方式格式化此参数。

**Syntax:**

```
<paramref name="name"/>
```

where

- name 是参数的名称。

**Example:**

```
public class Point
{
    /// <summary>This constructor initializes the new Point to
    /// <paramref name="xPosition"/>,<paramref name="yPosition"/>).
    /// </summary>
    /// <param name="xPosition">the new Point's x-coordinate.</param>
    /// <param name="yPosition">the new Point's y-coordinate.</param>
    public Point(int xPosition, int yPosition)
    {
        ...
    }
}
```

### D.3.11 <permission>

此标签允许记录成员的安全可访问性。

**Syntax:**

```
<permission cref="member">description</permission>
```

where

- member 是成员的名称。文档生成器检查给定的代码元素是否存在，并将 member 翻译为文档文件中的规范元素名称。
- description 是对成员访问的描述。

**Example:**

```
public class MyClass
{
    /// <permission cref="System.Security.PermissionSet">
    /// Everyone can access this method.
    /// </permission>
    public static void Test()
```



```csharp
{
    ...
}
}
```

## D.3.12 `<remarks>`

此标记用于指定关于类型的额外信息。使用 `<summary>`（§D.3.16）来描述类型本身以及类型的成员。

**语法：**

```xml
<remarks>description</remarks>
```

其中

- *描述* 是备注的文本。

**示例：**

```csharp
/// <summary>
/// Class <Point/> models a point in a two-dimensional plane.
/// </summary>
/// <remarks>
/// Uses polar coordinates
/// </remarks>
public class Point
{
    ...
}
```

## D.3.13 `<returns>`

此标记用于描述方法的返回值。

**语法：**

```xml
<returns>description</returns>
```

其中

- *描述* 是返回值的描述。

**示例：**

```csharp
public class Point
{
    /// <summary>
    /// Report a point's location as a string.
    /// </summary>
    /// <returns>
    /// A string representing a point's location, in the form (x,y),
    /// without any leading, trailing, or embedded whitespace.
    /// </returns>
    public override string ToString() => $"({X},{Y})";
    public int X { get; set; }
    public int Y { get; set; }
}
```

## D.3.14 <see>

此标记允许在文本中指定链接。使用 `<seealso>`（§D.3.15）来指示要出现在“另请参阅”子句中的文本。

语法：

```
<see cref="member" href="url" langword="keyword" />
```

其中

- *成员* 是成员的名称。文档生成器检查给定的代码元素是否存在，并在生成的文档文件中将 *成员* 更改为元素名称。
- *URL* 是对外部源的引用。
- *语言关键字* 是要以某种方式突出显示的词。

示例：

```
public class Point
{
    /// <summary>
    /// This method changes the point's location to
    /// the given coordinates. <see cref="Translate"/>
    /// </summary>
    public void Move(int xPosition, int yPosition)
    {
        ...
    }
    /// <summary>This method changes the point's location by
    /// the given x- and y-offsets. <see cref="Move"/>
    /// </summary>
    public void Translate(int dx, int dy)
    {
        ...
    }
}
```

## D.3.15 <seealso>

此标记允许为“另请参阅”子句生成一个条目。使用 `<see>`（§D.3.14）来指定文本中的链接。

语法：

```
<seealso cref="member" href="url" />
```

其中

- *成员* 是成员的名称。文档生成器检查给定的代码元素是否存在，并在生成的文档文件中将 *成员* 更改为元素名称。
- *URL* 是对外部源的引用。

示例：

```
public class Point
{
    /// <summary>
    /// This method determines whether two Points have the same location.
    /// </summary>
    /// <seealso cref="operator=="/>
    /// <seealso cref="operator!="/>
    public override bool Equals(object o)
    {
        ...
    }
}
```

## D.3.16 <summary>

此标记可用于描述类型或类型的成员。使用 `<remarks>`（§D.3.12）来指定关于类型或成员的额外信息。

### 语法：

```
<summary>description</summary>
```

其中

- *描述* 是类型或成员的摘要。

### 示例：

```
public class Point
{
    /// <summary>
    /// This constructor initializes the new Point to
    /// <paramref name="xPosition"/>,<paramref name="yPosition"/>.
    /// </summary>
    public Point(int xPosition, int yPosition)
    {
        ...
    }

    /// <summary>This constructor initializes the new Point to (0,0).</summary>
    public Point() : this(0, 0)
    {
    }
}
```

## D.3.17 <typeparam>

此标记用于描述泛型类型或方法的类型参数。

### 语法：

```
<typeparam name="name">description</typeparam>
```

其中

- *名称* 是类型参数的名称。
- *描述* 是类型参数的描述。

### 示例：

```
/// <summary>A generic list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
```

```csharp
public class MyList<T>
{
    ...
}
```

## D.3.18 <typeparamref>

此标记用于指示某个词是类型参数。可以处理文档文件，以某种独特的方式格式化此类型参数。

**语法：**

```
<typeparamref name="name"/>
```

- *名称* 是类型参数的名称。

**示例：**

```csharp
public class MyClass
{
    /// <summary>
    /// This method fetches data and returns a list of
    /// <typeparamref name="T"/>.
    /// </summary>
    /// <param name="query">query to execute</param>
    public List<T> FetchData<T>(string query)
    {
        ...
    }
}
```

## D.3.19 <value>

此标记允许描述属性。

**语法：**

```
<value>property description</value>
```

- *属性描述* 是属性的描述。

**示例：**

```csharp
public class Point
{
    /// <value>Property <c>X</c> represents the point's x-coordinate.</value>
    public int X { get; set; }
}
```

## D.4 处理文档文件

### D.4.1 概述

以下信息适用于面向 CLI 的 C# 实现。

文档生成器为源代码中带有文档注释的每个元素生成一个 ID 字符串。此 ID 字符串唯一标识一个源元素。文档查看器可以使用 ID 字符串来标识文档所适用的对应项。

文档文件不是源代码的分层表示；相反，它是一个平面列表，为每个元素生成一个 ID 字符串。

### D.4.2 ID 字符串格式

文档生成器在生成 ID 字符串时遵循以下规则：

- 字符串中不放置空白。
- 字符串的第一部分标识正在记录文档的成员种类，方式是一个单字符后跟一个冒号。定义了以下成员种类：

| 字符 | 描述 |
| E | 事件 |
| F | 字段 |
| M | 方法（包括构造函数、终结器和运算符） |
| N | 命名空间 |
| P | 属性（包括索引器） |
| T | 类型（如类、委托、枚举、接口和结构） |
| ! | 错误字符串；字符串的其余部分提供有关错误的信息。例如，文档生成器为无法解析的链接生成错误信息。 |

- 字符串的第二部分是元素的完全限定名，从命名空间的根开始。元素名称、其封闭类型和命名空间由句点分隔。如果项本身的名称包含句点，则用 #（U+0023）字符替换它们。（假定没有元素的名称中包含此字符。）
- 对于带参数的方法和属性，后面跟着参数列表，括在括号中。对于不带参数的，省略括号。参数由逗号分隔。每个参数的编码与 CLI 签名相同，如下所示：

- 参数由其文档名称表示，该名称基于其完全限定名，并按如下方式修改：
  - 表示泛型类型的参数追加一个“`”字符，后跟类型参数的数量
  - 具有 in、out 或 ref 修饰符的参数在其类型名后带有 @。按值传递或通过 params 传递的参数没有特殊表示法。
  - 数组参数表示为 [ lowerbound : size , ... , lowerbound : size ]，其中逗号的数量比秩少一，每个维度的下界和大小（如果已知）用十进制表示。如果未指定下界或大小，则省略它。如果省略了特定维度的下界和大小，则“:”也省略。交错数组每层用一个“[]”表示。

- 具有除 void 以外的指针类型的参数，在类型名后使用 * 表示。void 指针使用类型名 System.Void 表示。
- 引用类型上定义的泛型类型参数的参数，使用“~”字符后跟类型参数的从零开始的索引进行编码。
- 使用方法中定义的泛型类型参数的参数，使用双反引号 `` ` `` 代替用于类型的“~”。
- 引用构造泛型类型的参数，使用泛型类型编码，后跟“{”，后跟逗号分隔的类型实参列表，后跟“}”。

### D.4.3 ID 字符串示例

以下每个示例展示一段 C# 代码片段，以及由每个能够带有文档注释的源元素生成的 ID 字符串：

类型使用其完全限定名表示，并增补泛型信息：

```
enum Color { Red, Blue, Green }

namespace Acme
{
    interface IProcess { ... }
    struct ValueType { ... }
    class Widget : IProcess
    {
        public class NestedClass { ... }
        public interface IMenuItem { ... }
        public delegate void Del(int i);
        public enum Direction { North, South, East, West }
    }
    class MyList<T>
    {
        class Helper<U,V> { ... }
    }
}
```

ID：

- "T:Color"
- "T:Acme.IProcess"
- "T:Acme.ValueType"
- "T:Acme.Widget"
- "T:Acme.Widget.NestedClass"
- "T:Acme.Widget.IMenuItem"
- "T:Acme.Widget.Del"
- "T:Acme.Widget.Direction"
- "T:Acme.MyList`1"
- "T:Acme.MyList`1.Helper`2"

字段由其完全限定名表示。

```
namespace Acme
{
```



## D 文档注释

```
class Widget : IProcess
{
    ~Widget() { ... }
}
```

标识符：

"M:Acme.Widget.Finalize"

## 方法

```
namespace Acme
{
    struct ValueType
    {
        public void M(int i) { ... }
    }

    class Widget : IProcess
    {
        public class NestedClass
        {
            public void M(int i) { ... }
        }

        public static void M0() { ... }
        public void M1(char c, out float f, ref ValueType v, in int i) { ... }
        public void M2(short[] x1, int[,] x2, long[][] x3) { ... }
        public void M3(long[][] x3, Widget[, ,] x4) { ... }
        public unsafe void M4(char *pc, Color **pf) { ... }
        public unsafe void M5(void *pv, double *[, ] pd) { ... }
        public void M6(int i, params object[] args) { ... }
    }

    class MyList<T>
    {
        public void Test(T t) { ... }
    }

    class UseList
    {
        public void Process(MyList<int> list) { ... }
        public MyList<T> GetValues<T>(T value) { ... }
    }
}
```

标识符：

"M:Acme.ValueType.M(System.Int32)"
"M:Acme.Widget.NestedClass.M(System.Int32)"
"M:Acme.Widget.M0()"
"M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@,System.Int32@)"
"M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
"M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:,0:])"
"M:Acme.Widget.M4(System.Char*,Color***)"
"M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:][[]])"
"M:Acme.Widget.M6(System.Int32,System.Object[])"
"M:Acme.MyList`1.Test(`0)"
"M:Acme.UseList.Process(Acme.MyList<System.Int32>)"
"M:Acme.UseList.GetValues`1(`0)"

## 属性和索引器

```
namespace Acme
{
    class Widget : IProcess
    {
        public int Width { get { ... } set { ... } }
        public int this[int i] { get { ... } set { ... } }
        public int this[string s, int i] { get { ... } set { ... } }
    }
}
```

标识符：
"P:Acme.Widget.Width"
"P:Acme.Widget.Item(System.Int32)"
"P:Acme.Widget.Item(System.String,System.Int32)"

## 事件

```
namespace Acme
{
    class Widget : IProcess
    {
        public event Del AnEvent;
    }
}
```

标识符：
"E:Acme.Widget.AnEvent"

## 一元运算符

```
namespace Acme
{
    class Widget : IProcess
    {
        public static Widget operator+(Widget x) { ... }
    }
}
```

标识符：
"M:Acme.Widget.op_UnaryPlus(Acme.Widget)"

完整的一元运算符函数名称集合如下：op_UnaryPlus, op_UnaryNegation, op_LogicalNot, op_OnesComplement, op_Increment, op_Decrement, op_True, 和 op_False.

## 二元运算符

```
namespace Acme
{
    class Widget : IProcess
    {
        public static Widget operator+(Widget x1, Widget x2) { ... }
    }
}
```

标识符：

"M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"

完整的一元运算符函数名称集合如下：op_Addition, op_Subtraction, op_Multiply, op_Division, op_Modulus, op_BitwiseAnd, op_BitwiseOr, op_ExclusiveOr, op_LeftShift, op_RightShift, op_Equality, op_Inequality, op_LessThan, op_LessThanOrEqual, op_GreaterThan, 和 op_GreaterThanOrEqual.

转换运算符在其后带有 "~"，后跟返回类型。

```
namespace Acme
{
    class Widget : IProcess
    {
        public static explicit operator int(Widget x) { ... }
        public static implicit operator long(Widget x) { ... }
    }
}
```

标识符：

"M:Acme.Widget.op_Explicit(Acme.Widget)~System.Int32"
"M:Acme.Widget.op_Implicit(Acme.Widget)~System.Int64"

## D.5 示例

### D.5.1 C# 源代码

以下示例展示了 Point 类的源代码：

```
namespace Graphics
{
    /// <summary>
    /// Class <c>Point</c> models a point in a two-dimensional plane.
    /// </summary>
    public class Point
    {
        /// <value>
        /// Property <c>X</c> represents the point's x-coordinate.
        /// </value>
        public int X { get; set; }

        /// <value>
        /// Property <c>Y</c> represents the point's y-coordinate.
        /// </value>
        public int Y { get; set; }

        /// <summary>
        /// This constructor initializes the new Point to (0,0).
        /// </summary>
        public Point() : this(0, 0) {}

        /// <summary>
        /// This constructor initializes the new Point to
        /// (<paramref name="xPosition"/>,<paramref name="yPosition"/>).
        /// </summary>
        /// <param><c>xPosition</c> is the new Point's x-coordinate.</param>
        /// <param><c>yPosition</c> is the new Point's y-coordinate.</param>
        public Point(int xPosition, int yPosition)
        {
            X = xPosition;
            Y = yPosition;
        }

        /// <summary>
        /// This method changes the point's location to
        /// the given coordinates. <see cref="Translate"/>
        /// </summary>
        /// <param><c>xPosition</c> is the new x-coordinate.</param>
        /// <param><c>yPosition</c> is the new y-coordinate.</param>
        public void Move(int xPosition, int yPosition)
        {
            X = xPosition;
            Y = yPosition;
        }

        /// <summary>
        /// This method changes the point's location by
        /// the given x- and y-offsets.
        /// <example>For example:
        /// <code>
        /// Point p = new Point(3, 5);
        /// p.Translate(-1, 3);
        /// </code>
        /// results in <c>p</c>'s having the value (2, 8).
        /// <see cref="Move"/>
        /// </example>
        /// </summary>
        /// <param><c>dx</c> is the relative x-offset.</param>
        /// <param><c>dy</c> is the relative y-offset.</param>
        public void Translate(int dx, int dy)
        {
            X += dx;
            Y += dy;
        }

        /// <summary>
        /// This method determines whether two Points have the same location.
        /// </summary>
        /// <param>
        /// <c>o</c> is the object to be compared to the current object.
        /// </param>
        /// <returns>
        /// True if the Points have the same location and they have
        /// the exact same type; otherwise, false.
        /// </returns>
        /// <seealso cref="operator=="/>
        /// <seealso cref="operator!="/>
        public override bool Equals(object o)
        {
            if (o == null)
            {
                return false;
            }
            if (((object)this) == o)
            {
                return true;
            }
            if (GetType() == o.GetType())
            {
                Point p = (Point)o;
                return (X == p.X) && (Y == p.Y);
            }
            return false;
        }

        /// <summary>
        /// This method returns a Point's hashcode.
        /// </summary>
        /// <returns>
        /// The int hashcode.
        /// </returns>
        public override int GetHashCode()
        {
            return X + (Y >> 4);    // a crude version
        }

        /// <summary>Report a point's location as a string.</summary>
        /// <returns>
        /// A string representing a point's location, in the form (x,y),
        /// without any leading, trailing, or embedded whitespace.
        /// </returns>
        public override string ToString() => $"({X},{Y})";

        /// <summary>
        /// This operator determines whether two Points have the same location.
        /// </summary>
        /// <param><c>p1</c> is the first Point to be compared.</param>
        /// <param><c>p2</c> is the second Point to be compared.</param>
        /// <returns>
        /// True if the Points have the same location and they have
        /// the exact same type; otherwise, false.
        /// </returns>
        /// <seealso cref="Equals"/>
        /// <seealso cref="operator!="/>
        public static bool operator==(Point p1, Point p2)
        {
            if (((object)p1 == null || (object)p2 == null))
            {
                return false;
            }
            if (p1.GetType() == p2.GetType())
            {
                return (p1.X == p2.X) && (p1.Y == p2.Y);
            }
            return false;
        }

        /// <summary>
        /// This operator determines whether two Points have the same location.
        /// </summary>
        /// <param><c>p1</c> is the first Point to be compared.</param>
        /// <param><c>p2</c> is the second Point to be compared.</param>
        /// <returns>
        /// True if the Points do not have the same location and the
        /// exact same type; otherwise, false.
        /// </returns>
        /// <seealso cref="Equals"/>
        /// <seealso cref="operator=="/>
        public static bool operator!=(Point p1, Point p2) => !(p1 == p2);
    }
}
```

### D.5.2 生成的 XML

以下是当给定上述 Point 类的源代码时，由某个文档生成器产生的输出：

```
<?xml version="1.0"?>
<doc>
  <assembly>
    <name>Point</name>
  </assembly>
  <members>
    <member name="T:Graphics.Point">
      <summary>Class <c>Point</c> models a point in a two-dimensional plane.</summary>
    </member>
    <member name="M:Graphics.Point.#ctor">
      <summary>This constructor initializes the new Point to (0, 0).</summary>
    </member>
    <member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
      <summary>
        This constructor initializes the new Point to
        (<paramref name="xPosition"/>,<paramref name="yPosition"/>).
      </summary>
      <param><c>xPosition</c> is the new Point's x-coordinate.</param>
      <param><c>yPosition</c> is the new Point's y-coordinate.</param>
    </member>
    <member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
      <summary>
        This method changes the point's location to
        the given coordinates.
        <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
      </summary>
      <param><c>xPosition</c> is the new x-coordinate.</param>
      <param><c>yPosition</c> is the new y-coordinate.</param>
    </member>
```

<member name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
  <summary>
    此方法通过给定的 x 和 y 偏移量更改点的位置。
    <example>例如：
    <code>
    Point p = new Point(3,5);
    p.Translate(-1,3);
    </code>
    结果使 <c>p</c> 的值为 (2,8)。
    </example>
    <see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
  </summary>
  <param><c>dx</c> 是相对 x 偏移量。</param>
  <param><c>dy</c> 是相对 y 偏移量。</param>
</member>
<member name="M:Graphics.Point.Equals(System.Object)">
  <summary>
    此方法确定两个 Point 是否具有相同的位置。
  </summary>
  <param>
    <c>o</c> 是要与当前对象进行比较的对象。
  </param>
  <returns>
    如果 Points 具有相同的位置并且它们具有完全相同的类型，则为 True；否则为 false。
  </returns>
  <seealso
    cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)" />
  <seealso
    cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.ToString">
  <summary>
    将点的位置作为字符串报告。
  </summary>
  <returns>
    表示点位置的字符串，形式为 (x,y)，
    不包含任何前导、尾随或嵌入的空白。
  </returns>
</member>
<member name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
  <summary>
    此运算符确定两个 Point 是否具有相同的位置。
  </summary>
  <param><c>p1</c> 是要比较的第一个 Point。</param>
  <param><c>p2</c> 是要比较的第二个 Point。</param>
  <returns>
    如果 Points 具有相同的位置并且它们具有完全相同的类型，则为 True；否则为 false。
  </returns>
  <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
  <seealso
    cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>

<member
name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
<summary>
此运算符确定两个 Point 是否具有相同的位置。
</summary>
<param><c>p1</c> 是要比较的第一个 Point。</param>
<param><c>p2</c> 是要比较的第二个 Point。</param>
<returns>
如果 Points 不具有相同的位置并且具有完全相同的类型，则为 True；否则为 false。
</returns>
<seealso cref="M:Graphics.Point.Equals(System.Object)"/>
<seealso
cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.Main">
<summary>
这是 Point 类测试程序的入口点。
<para>
此程序测试每个方法和运算符，
并且旨在在对 Point 类进行任何非平凡维护后运行。
</para>
</summary>
</member>
<member name="P:Graphics.Point.X">
<value>
属性 <c>X</c> 表示点的 x 坐标。
</value>
</member>
<member name="P:Graphics.Point.Y">
<value>
属性 <c>Y</c> 表示点的 y 坐标。
</value>
</member>
</members>
</doc>

## 参考性文本结束。

## 参考文献

**本附录为参考性。**

- ANSI X3.274-1996, *编程语言 REXX.* (本文档有助于理解浮点十进制算术规则。)
- ISO/IEC 9075-1, *信息技术 — 数据库语言 — SQL — 第 1 部分：框架 (SQL/Framework)*
- ISO/IEC 9899, *编程语言 — C.*
- ISO/IEC 14882 *编程语言 — C++.*
- ISO 80000-1, *量和单位 — 第 1 部分：总则.* (本文档定义了“银行家舍入”。)

**参考性文本结束。**
