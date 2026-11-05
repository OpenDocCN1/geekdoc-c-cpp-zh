
否则会被处理。在被处理为跳过区段的条件区段内，任何嵌套的条件区段（包含在嵌套的 #if...#endif 和 #region...#endregion 构造中）也将被处理为跳过区段。

以下示例说明了条件编译指令如何嵌套：

```
#define Debug    // Debugging on
#undef Trace    // Tracing off
class PurchaseTransaction
{
    void Commit() {
        #if Debug
        CheckConsistency();
        #if Trace
        writeToLog(this.ToString());
        #endif
        #endif
        CommitHelper();
    }
}
```

除预处理指令外，被跳过的源代码不进行词法分析。例如，尽管 #else 部分中存在未终止的注释，以下内容仍然有效：

```
#define Debug    // Debugging on
class PurchaseTransaction
{
    void Commit() {
        #if Debug
        CheckConsistency();
        #else
        /* Do something else
        #endif
    }
}
```

然而请注意，即使在源代码的跳过区段中，预处理指令也必须在词法上正确。

预处理指令在出现在多行输入元素内部时不会被处理。例如，程序：

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

在特殊情况下，被处理的预处理指令集合可能取决于 pp 表达式的求值。示例：

```
#if X
/*
#else
/* */ class Q { }
#endif
```

始终产生相同的标记流（class Q {}），无论 X 是否定义。如果 X 已定义，则由于多行注释，唯一被处理的指令是 #if 和 #endif。如果 X 未定义，则三个指令（#if、#else、#endif）都是指令集的一部分。

### 2.5.5 诊断指令

诊断指令用于显式生成错误和警告消息，这些消息的报告方式与其他编译时错误和警告相同。

```
pp-diagnostic:
    whitespace_opt # whitespace_opt error pp-message
    whitespace_opt # whitespace_opt warning pp-message

pp-message:
    new-line
    whitespace input-characters_opt new-line
```

示例：

```
#warning Code review needed before check-in
#if Debug && Retail
#error A build can't be both debug and retail
#endif
class Test {...}
```

始终会产生一个警告（"Code review needed before check-in"），并且如果条件符号 Debug 和 Retail 同时被定义，则会产生编译时错误（"A build can't be both debug and retail"）。请注意，pp-message 可以包含任意文本；具体来说，它不必包含格式良好的标记，正如 can't 这个词中的单引号所示。

### 2.5.6 区域指令

区域指令用于显式标记源代码的区域。

```
pp-region:
    pp-start-region conditional-section_opt pp-end-region
pp-start-region:
    whitespace_opt # whitespace_opt region pp-message
pp-end-region:
    whitespace_opt # whitespace_opt endregion pp-message
```

区域不附加任何语义含义；区域旨在供程序员或自动化工具用来标记源代码的某一部分。#region 或 #endregion 指令中指定的消息同样没有语义含义；它仅用于标识该区域。匹配的 #region 和 #endregion 指令可能具有不同的 pp-message。

区域的词法处理：

```
#region
...
#endregion
```

完全对应于以下形式的条件编译指令的词法处理：

```
#if true
...
#endif
```

### 2.5.7 行指令

行指令可用于更改编译器在警告和错误等输出中报告的行号和源文件名。

行指令最常用于从其他文本输入生成 C# 源代码的元编程工具中。

```
pp-line:
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line
line-indicator:
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden
file-name:
    " file-name-characters "
file-name-characters:
    file-name-character
    file-name-characters file-name-character
file-name-character:
    Any input-character except "
```

当不存在 #line 指令时，编译器在输出中报告真实的行号和源文件名。当处理包含非 default 的 line-indicator 的 #line 指令时，编译器将该指令后的行视为具有给定的行号（以及如果指定则为文件名）。

#line default 指令会逆转所有先前 #line 指令的效果。编译器对后续行报告真实的行信息，就好像没有处理过 #line 指令一样。

#line hidden 指令对错误消息中报告的文件和行号没有影响，但会影响源代码级别的调试。在调试时，#line hidden 指令与下一个（不是 #line hidden 的）#line 指令之间的所有行都没有行号信息。在调试器中单步执行代码时，这些行将被完全跳过。

请注意，file-name 与普通字符串文字的不同之处在于转义字符不会被处理；'\' 字符仅在 file-name 内表示普通的反斜杠字符。

### 2.5.8 Pragma 指令

#pragma 预处理指令用于向编译器指定可选的上下文信息。#pragma 指令中提供的信息永远不会改变程序语义。

```
pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line
pragma-body:
    pragma-warning-body
```

C# 提供了 #pragma 指令来控制编译器警告。语言的未来版本可能包含额外的 #pragma 指令。为了确保与其他 C# 编译器的互操作性，Microsoft C# 编译器不会对未知的 #pragma 指令发出编译错误；不过此类指令会生成警告。

### 2.5.8.1 Pragma warning

#pragma warning 指令用于在后续程序文本的编译期间禁用或恢复全部或特定集合的警告消息。

```
pragma-warning-body:
    warning whitespace warning-action
    warning whitespace warning-action whitespace warning-list
warning-action:
    disable
    restore
warning-list:
    decimal-digits
    warning-list whitespace_opt , whitespace_opt decimal-digits
```

省略警告列表的 #pragma warning 指令会影响所有警告。包含警告列表的 #pragma warning 指令仅影响列表中指定的那些警告。

#pragma warning disable 指令会禁用全部或给定的警告集合。

#pragma warning restore 指令会将全部或给定的警告集合恢复到编译单元开始时生效的状态。请注意，如果某个警告在外部被禁用，则 #pragma warning restore（无论是全部还是特定警告）都不会重新启用该警告。

以下示例展示了如何使用 #pragma warning 暂时禁用引用已过时成员时报告的警告，使用的是来自 Microsoft C# 编译器的警告编号。

```
using System;
class Program
{
    [Obsolete]
    static void Foo() {}
    static void Main() {
#pragma warning disable 612
        Foo();
#pragma warning restore 612
    }
}
```

## 3. 基本概念

### 3.1 应用程序启动

具有入口点的程序集称为应用程序。当应用程序运行时，会创建一个新的应用程序域。同一台机器上可能同时存在应用程序的多个不同实例，每个实例都有自己的应用程序域。

应用程序域通过充当应用程序状态的容器来实现应用程序隔离。应用程序域充当应用程序中定义的类型及其使用的类库的容器和边界。加载到一个应用程序域中的类型与加载到另一个应用程序域中的相同类型是不同的，并且对象实例不会在应用程序域之间直接共享。例如，每个应用程序域都有这些类型的静态变量的自己的副本，并且类型的静态构造函数每个应用程序域最多运行一次。实现可以自由提供创建和销毁应用程序域的实现特定策略或机制。

应用程序启动发生在执行环境调用指定方法时，该方法称为应用程序的入口点。此入口点方法始终命名为 Main，并且可以具有以下签名之一：

```
static void Main() {...}
static void Main(string[] args) {...}
static int Main() {...}
static int Main(string[] args) {...}
```

如所示，入口点可以可选地返回 int 值。此返回值用于应用程序终止（§3.2）

入口点可以可选地有一个形式参数。参数可以有任何名称，但参数的类型必须是 string[]。如果存在形式参数，执行环境会创建并传递一个包含启动应用程序时指定的命令行参数的 string[] 参数。string[] 参数永远不会为 null，但如果未指定命令行参数，则其长度可能为零。

由于 C# 支持方法重载，类或结构可以包含某个方法的多个定义，前提是每个定义具有不同的签名。然而，在单个程序中，任何类或结构都不能包含多于一个名为 Main 的方法，其定义使其有资格用作应用程序入口点。但是，其他重载版本的 Main 是允许的，前提是它们具有多个参数，或者它们的唯一参数类型不是 string[]。

应用程序可以由多个类或结构组成。这些类或结构中的多个可能包含名为 Main 的方法，其定义使其有资格用作应用程序入口点。在这种情况下，必须使用外部机制（例如命令行编译器选项）来选择其中一个 Main 方法作为入口点。

在 C# 中，每个方法都必须定义为类或结构成员。通常，方法的声明可访问性（§3.5.1）由其声明中指定的访问修饰符（§10.3.5）决定，类似地，类型的声明可访问性由其声明中指定的访问修饰符决定。为了使给定类型的给定方法可调用，类型和成员都必须可访问。然而，应用程序入口点是一个特例。具体来说，执行环境可以访问应用程序的
