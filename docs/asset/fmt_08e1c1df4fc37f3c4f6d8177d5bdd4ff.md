
## 语言对比：Java——文件名必须与类名匹配

在 Java 中，文件名必须与类名一致。在 C# 中，这个约定经常被遵循，但并不是必需的。在 C# 中，一个文件里可以有两个类，而且从 C# 2.0 开始，可以通过称为分部类的特性让一个类横跨多个文件。

## C# 语法基础

成功编译并运行 `HelloWorld` 程序后，你就可以开始剖析代码，了解它的各个部分。首先，考虑 C# 关键字以及开发人员选择的标识符。

## 初学者专题

## 关键字

为了使编译器能够解释代码，C# 中的某些词具有特殊地位和含义。它们被称为关键字，为编译器提供了解释程序员所写表达式的具体语法。在 `HelloWorld` 程序中，`class`、`static` 和 `void` 就是关键字的例子。

编译器使用关键字来识别代码的结构和组织。由于编译器赋予这些词更高的重要性，C# 要求开发人员只能将关键字放在特定位置。当程序员违反这些规则时，编译器会报错。

## C# 关键字

表 1.1 展示了 C# 关键字。

表 1.1：C# 关键字

| abstract | enum | long | static |

| add* (1) | equals* (3) | nameof* (6) | string |

| alias* (2) | event | namespace | struct |

| as | explicit | new | switch |

| ascending* (3) | extern | null | this |

| async* (5) | false | object | throw |

| await* (5) | finally | on* (3) | true |

| base | fixed | operator | try |

| bool | float |orderby* (3) | typeof |

| break | for | out | uint |

| by* (3) | foreach | override | ulong |

| byte | from* (3) | params | unchecked |

| case | get* (1) | partial* (2) | unsafe |

| catch | global* (2) | private | ushort |

| char | goto | protected | using |

| checked | group* (3) | public | value* (1) |

| class | if | readonly | var* (3) |

| const | implicit | ref | virtual |

| continue | in | remove* (1) | void |

| decimal | int | return | volatile |

| default | interface | sbyte | where* (2) |

| delegate | internal | sealed | when* (6) |

| descending* (3) | into* (3) | select* (3) | while |

| do | is | set* (1) | yield* (2) |

| double | join* (3) | short |  |

| dynamic* (4) | let* (3) | sizeof |  |

| else | lock | stackalloc |  |

* 上下文关键字

括号中的数字 (n) 标识该上下文关键字是在哪个版本中添加的。

# 第 1 章：C# 简介

C# 1.0 之后，没有新的**保留关键字**被引入 C#。然而，后续版本中的一些构造使用了**上下文关键字**，它们只在特定位置才有意义。在这些指定位置之外，上下文关键字没有特殊意义。⁵ 通过这种方法，大多数 C# 1.0 代码都与后续标准兼容。⁶

## 标识符

与其他语言一样，C# 包含**标识符**来标识程序员编码的构造。在清单 1.1 中，`HelloWorld` 和 `Main` 就是标识符的示例。分配给构造的标识符在以后会被用来引用该构造，所以开发人员分配的名称必须有意义，而不是随意编造。

敏锐地选择简洁而有指示性的名称是优秀程序员的一个重要特征，因为这意味着最终代码将更容易理解和重用。清晰与一致非常重要，.NET Framework 指南 (`http://bit.ly/dotnetguidelines`) 建议不要在标识符名称中使用缩写或缩约词，甚至建议避免使用未被广泛接受的首字母缩写词。如果一个首字母缩写词已经足够成熟（例如 `HTML`），你应该始终如一地使用它：不要时而拼出已被接受的首字母缩写词，时而不拼。通常，要求所有首字母缩写词都包含在术语表中的约束会给首字母缩写词的使用增加足够的负担，使它们不会被随意使用。最终，要选择清晰甚至冗长的名称——尤其是在团队中工作或开发供其他人编程使用的库时。

标识符有两种基本大小写格式。**Pascal 大小写**（以下简称 `PascalCase`），CLI 的创造者们这样称呼它，是因为它在

+   5. 例如，在 C# 2.0 的设计早期，语言设计者将 `yield` 指定为关键字，微软向数千名开发人员发布了 C# 2.0 编译器的 alpha 版本，其中 `yield` 被指定为关键字。然而，语言设计者最终确定，通过使用 `yield returned` 而不是 `yield`，他们最终可以避免将 `yield` 添加为关键字，因为除了紧邻 `return` 之外，它没有特殊意义。

+   

+   6. 有一些罕见且不幸的不兼容性，例如：

+   - C# 2.0 要求使用 `using` 语句实现 `IDisposable`，而不是仅使用 `Dispose()` 方法

+   - 一些罕见的泛型表达式，如 `F(G<A,B>(7))` 在 C# 1.0 中表示 `F((G<A>), (B>7))`，而在 C# 2.0 中则改为表示用参数 7 调用泛型方法 `G<A,B>`，并将结果传给 F

`Pascal` 编程语言会将标识符名称中每个单词的首字母大写；示例包括 `ComponentModel`、`Configuration` 和 `HttpFileCollection`。正如 `HttpFileCollection` 在 `HTTP` 中的演示，当使用长度超过两个字母的缩写时，仅大写第一个字母。第二种格式，驼峰命名法（以下简称 `camelCase`），遵循相同的约定，只是首字母小写；示例包括 `quotient`、`firstName`、`httpFileCollection`、`ioStream` 和 `theDreadPirateRoberts`。

## Guidelines

- 在命名标识符时，DO 优先考虑清晰度而非简洁性。

- DO NOT 在标识符名称中使用缩写或缩略形式。

- DO NOT 使用任何缩写，除非它们被广泛接受，即使如此，也仅在必要时使用。

请注意，虽然下划线是合法的，但通常标识符名称中没有下划线、连字符或其他非字母数字字符。此外，C# 不遵循其前身，即匈牙利命名法（在名称前加上数据类型缩写）不被使用。这避免了在数据类型更改时需要重命名变量，或因使用匈牙利命名法时未能调整数据类型前缀而引入的不一致。

在某些罕见情况下，一些标识符，例如 `Main`，在 C# 语言中可能具有特殊含义。

## Guidelines

- DO 将两个字符缩写的两个字符都大写，除第一个 `camelCased` 标识符的第一个单词外。

- DO 仅将三个或更多字符的缩写中的第一个字符大写，除第一个 `camelCased` 标识符的第一个单词外。

- DO NOT 将 `camelCased` 标识符开头的缩写中的任何字符大写。

- DO NOT 使用匈牙利命名法（即不要在其名称中编码变量的类型）。

## ADVANCED TOPIC

## Keywords

虽然很少见，但如果包含 “@” 作为前缀，关键字可以作为标识符使用。例如，你可以为局部变量命名为 `@return`。同样（尽管它不符合 C# 编码标准的命名约定），也可以将方法命名为 `@throw()`。

在 Microsoft 实现中还有四个未记录的保留关键字：`__arglist`、`__makeref`、`__reftype` 和 `__refvalue`。它们仅在罕见的互操作场景中才需要，对于所有实际目的都可以忽略。请注意，这四个特殊关键字以两个下划线开头。C# 的设计者保留了将任何以两个下划线开头的标识符在未来版本中变为关键字的权利；为安全起见，避免自己创建此类标识符。

## Type Definition

C# 中的所有可执行代码都出现在类型定义中，而最常见的类型定义以关键字 `class` 开始。类定义是通常以 `class identifier { ... }` 开始的代码段，如 Listing 1.2 所示。

## LISTING 1.2: Basic Class Declaration

```
class HelloWorld
{
    //...
}
```

用于类型的名称（在本例中为 `HelloWorld`）可以有所不同，但按惯例，它必须是 `PascalCased`。因此，对于此特定示例，其他可能的名称是 `Greetings`、`HelloInigoMontoya`、`Hello`，或简单地 `Program`。（当类包含 `Main()` 方法时，后文将描述，`Program` 是一个很好的约定。）

## Guidelines

- DO 使用名词或名词短语命名类。

- DO 对所有类名使用 `PascalCasing`。

通常，程序包含多个类型，每个类型包含多个方法。

## Main

## BEGINNER TOPIC

## What Is a Method?

从语法上讲，C# 中的方法是由方法声明引入的命名代码块（例如，`static void Main()`）并且（通常）后面跟着花括号内的零个或多个语句。方法执行计算和/或操作。与书面语言中的段落类似，方法提供了一种结构化和组织代码的方式，使其更具可读性。更重要的是，方法可以被重用并从多个位置调用，从而避免代码重复。方法声明引入方法并定义方法名称以及传递给方法并从方法传递的数据。在 Listing 1.3 中，`Main()` 后跟 `{ ... }` 是 C# 方法的示例。

C# 程序开始执行的位置是 `Main` 方法，它以 `static void Main()` 开始。当你在命令控制台输入 `HelloWorld.exe` 执行程序时，程序启动，解析 `Main` 的位置，并开始执行 Listing 1.3 中的第一个语句。

## LISTING 1.3: Breaking Apart HelloWorld

```
class HelloWorld
{
    static void Main()
    {
        System.Console.WriteLine("Hello, My name is Inigo Montoya");
    }
}
Method Declaration
Main
Class Definition
Statement
```

虽然 `Main` 方法声明可以有所不同，但 `static` 和方法名 `Main` 对于程序来说始终是必需的。

例如，`Main` 方法包含围绕其实现的 curly braces；在这种情况下，方法中只有一个语句。

## Statements and Statement Delimiters

`Main` 方法包含单个语句，`System.Console.WriteLine()`，用于向控制台写入一行文本。C# 通常使用分号来表示 **statement** 的结束，其中语句由代码将执行的多个操作组成。声明变量、控制程序流程和调用方法都是语句的典型用途。

> **Language Contrast: Visual Basic—Line-Based Statements**

> 

> 有些语言是基于行的，这意味着如果没有特殊注释，语句不能跨行。直到 Visual Basic 2010，Visual Basic 就是基于行的语言示例。它要求在行尾使用下划线来指示语句跨越多行。从 Visual Basic 2010 开始，引入了许多情况，其中换行符字符是可选的。

## ADVANCED TOPIC

## Statements without Semicolons

C# 中的许多编程元素以分号结尾。一个不包含分号的示例是 `switch` 语句。因为 `switch` 语句中始终包含 curly braces，所以 C# 不要求在语句后跟分号。事实上，代码块本身被视为语句（它们也由语句组成），并且它们不需要使用分号闭合。同样，在某些情况下，例如 `using` 声明，分号出现在末尾但它不是语句。

由于换行不会分隔语句，你可以将多个语句放在同一行，C# 编译器会将该行解释为包含多个指令。例如，Listing 1.5 包含

一行中的两个语句，结合起来在两行上显示 Up 和 Down。

## LISTING 1.5: Multiple Statements on One Line

```
System.Console.WriteLine("Up");System.Console.WriteLine("Down");
```

C# 还允许将语句拆分到多行。同样，C# 编译器会查找分号以指示语句的结束（参见 Listing 1.6）。

## LISTING 1.6: Splitting a Single Statement across Multiple Lines

```
System.Console.WriteLine(
"Hello. My name is Inigo Montoya.");
```

在 Listing 1.6 中，`HelloWorld` 程序中的原始 `WriteLine()` 语句被拆分到多行。

## BEGINNER TOPIC

## What Is Whitespace?

空白是制表符、空格和换行符等一个或多个连续格式字符的组合。显然，消除单词之间的所有空白很重要，正如在引号字符串中包含空白一样。

## Whitespace
