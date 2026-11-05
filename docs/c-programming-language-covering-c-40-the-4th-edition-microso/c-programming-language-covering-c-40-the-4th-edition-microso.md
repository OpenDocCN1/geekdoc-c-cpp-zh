# C# 编程语言（涵盖 C# 4.0）第4版（Microsoft .NET 开发系列）




## 前言

自 2000 年夏天 .NET 发布以来，已经过去十年了。对我而言，.NET 的意义在于将本地执行的托管代码与程序间通信所使用的 XML 消息结合起来，形成了一个一二组合。当时我没有明显意识到，C# 将会变得如此重要。

从 .NET 诞生之初，C# 就一直是开发人员理解和使用 .NET 时所采用的主要视角。问一位普通的 .NET 开发人员值类型和引用类型有什么区别，他或她会很快回答：“结构与类”，而不是“派生自 `System.ValueType` 的类型与不派生自它的类型”。为什么？因为人们使用语言——而不是 API——来向运行时表达自己的想法和意图，更重要的是，也借此彼此交流。

一门优秀语言对于整个​​平台成功的重要性，无论如何强调都不为过。C# 起初的重要作用，是确立人们思考 .NET 的基本方式。随着 .NET 的发展，C# 变得更加重要：迭代器和真正的闭包（也称为匿名方法）等功能被作为纯粹的语言功能引入开发人员，而不是作为平台原生功能提供；这些功能由 C# 编译器实现。C# 是 .NET 创新核心这一事实，在 C# 3.0 中变得更加明显：标准化查询运算符、简洁的 Lambda 表达式、扩展方法，以及运行时访问表达式树等功能被引入——同样，这些功能都由语言和编译器的发展所推动。C# 4.0 中最重要的功能——动态调用——在很大程度上也属于语言和编译器的功能，而不是对 CLR 本身的更改。

谈论 C# 时，很难不同时谈到它的发明者和始终如一的引领者 Anders Hejlsberg。在 C# 3.0 的设计周期中，我有幸参加了几个月定期举行的 C# 设计会议，观察 Anders 的工作过程令我受益匪浅。他能够准确判断开发人员会喜欢什么、不会喜欢什么，这种直觉确实是世界级的——与此同时，Anders 对他的设计团队极其包容，并且能够促成尽可能优秀的设计。

尤其是在 C# 3.0 中，Anders 具有一种非凡的能力：他能从函数式语言社区汲取关键思想，并让这些思想被非常广泛的受众所理解和使用。这绝非易事。Guy Steele 曾这样评价 Java：“我们并不是要争取 Lisp 程序员；我们的目标是 C++ 程序员。我们成功地把其中很多人带到了距离 Lisp 大约一半的地方。”当我审视 C# 3.0 时，我觉得 C# 至少成功地把一名 C++ 开发人员（也就是我）带到了剩下路程的大部分位置。C# 4.0 又向 Lisp（以及 JavaScript、Python、Ruby 等）迈进了一步，增加了清晰编写不依赖静态类型定义的程序的能力。

C# 本身已经非常优秀，但人们仍然需要一份同时以自然语言（这里指英语）和某种形式化语言（BNF）编写的文档，才能真正理解其中的微妙之处，并确保我们对 C# 的理解和表达保持一致。你手中的这本书就是这样一份文档。根据我自己的经验，我可以放心地说，每一位读过本书的 .NET 开发人员至少都会有一次“恍然大悟”的时刻，并因此成为更优秀的开发人员。

祝阅读愉快。

Don Box  
华盛顿州雷德蒙德  
2010 年 5 月

## 前言

C# 项目始于 12 年多以前，即 1998 年 12 月，其目标是为当时尚未命名的新 .NET 平台创建一种简单、现代、面向对象且类型安全的编程语言。从那以后，C# 走过了漫长的道路。如今，这门语言已经被超过一百万名程序员使用，并且已经发布了四个版本，每个版本都增加了若干重要的新功能。

这本书也已经是第四版。它提供了 C# 编程语言的完整技术规范。这个最新版本包含两类以往版本中没有的新内容。当然，最值得注意的是，本书已经更新，可以涵盖 C# 4.0 的新功能，包括动态绑定、命名参数和可选参数，以及协变和逆变泛型类型。本次修订的总体主题，是进一步拓展 C# 与 .NET 环境之外的对象进行交互的能力。正如 C# 3.0 中的 LINQ 让用于访问外部数据源的代码具有语言集成的感觉一样，C# 4.0 的动态绑定也让与来自 Python、Ruby 和 JavaScript 等动态编程语言的对象进行交互时，感觉就像是在使用 C# 的原生功能。

本书上一版引入了由知名 C# 专家撰写的注释。我们持续收到读者对这一特色的热烈反馈，因此非常高兴能够在全书范围内提供新一轮来自新老注释作者的深入而有趣的见解、指导、背景知识和观点。我们很高兴看到这些注释继续对核心内容起到补充作用，并帮助 C# 的各项功能变得生动鲜活。

许多人都参与了 C# 语言的创建。C# 1.0 的语言设计团队由 Anders Hejlsberg、Scott Wiltamuth、Peter Golde、Peter Sollich 和 Eric Gunnerson 组成。C# 2.0 的语言设计团队由 Anders Hejlsberg、Peter Golde、Peter Hallam、Shon Katzenberger、Todd Proebsting 和 Anson Horton 组成。

此外，C# 和 .NET 公共语言运行时中的泛型设计与实现，建立在 Microsoft Research 的 Don Syme 和 Andrew Kennedy 开发的“Gyro”原型之上。C# 3.0 由 Anders Hejlsberg、Erik Meijer、Matt Warren、Mads Torgersen、Peter Hallam 和 Dinesh Kulkarni 负责设计。C# 4.0 的设计团队成员包括 Anders Hejlsberg、Matt Warren、Mads Torgersen、Eric Lippert、Jim Hugunin、Lucian Wischik 和 Neal Gafter。

我们无法一一感谢所有影响过 C# 设计的人，但我们仍然对他们所有人心怀感激。任何优秀的设计都不会凭空产生，而我们从广大且充满热情的开发人员社区中持续获得的反馈极其宝贵。

C# 一直是、并且仍然是我们参与过的最具挑战性和最令人兴奋的项目之一。我们希望你享受使用 C# 的过程，就像我们享受创建 C# 的过程一样。

Anders Hejlsberg  
Mads Torgersen  
Scott Wiltamuth  
Peter Golde  
*华盛顿州西雅图*  
*2010 年 9 月*

## 关于作者

**Anders Hejlsberg** 是一位编程界的传奇人物。他是 C# 语言的架构师，也是 Microsoft 技术院士。1996 年，他加入 Microsoft 公司。在此之前，他曾在 Borland 工作 13 年，担任 Delphi 和 Turbo Pascal 的首席架构师。

**Mads Torgersen** 是 Microsoft 公司 C# 语言项目经理，负责日常的语言设计流程，并维护语言规范。

**Scott Wiltamuth** 是 Microsoft 公司 Visual Studio Professional 团队的项目管理总监。在 Microsoft 任职期间，他参与过众多开发工具的工作，包括 OLE Automation、Visual Basic、Visual Basic for Applications、VBScript、JScript、Visual J++ 和 Visual C#。

**Peter Golde** 是最初 Microsoft C# 编译器的首席开发人员。作为负责标准化 C# 的 ECMA 委员会中的 Microsoft 首席代表，他领导了编译器的实现工作，并参与语言设计。目前，他是 Microsoft 公司的一名架构师，负责编译器相关工作。




本页有意留白

## 关于注释者

Brad Abrams 是 Microsoft Corporation 公共语言运行时（Common Language Runtime）和 .NET Framework 团队的创始成员，最近担任 WCF 和 WF 的项目管理总监。Brad 自 1998 年起一直参与设计 .NET Framework 的组成部分，当时他开始了自己的框架设计职业生涯，构建作为 .NET Framework 核心部分发布的 BCL（基类库）。Brad 于 1997 年毕业于北卡罗来纳州立大学，获得计算机科学学士学位。Brad 的出版物包括：*框架设计指南（第2版）*（Addison-Wesley，2009），以及 *.NET Framework 标准库注释参考*（第1卷和第2卷）（Addison-Wesley，2006）。

Joseph Albahari 是 *C# 4.0 速查手册*（O’Reilly，2007）、*C# 3.0 袖珍参考*（O’Reilly，2008）和 *LINQ 袖珍参考*（O’Reilly，2008）的合著者。他拥有 17 年作为高级开发人员和软件架构师的经验，涉及健康、教育和电信行业，并且是 LINQPad 的作者，该工具用于在 LINQ 中交互式查询数据库。

Krzysztof Cwalina 是 Microsoft .NET Framework 团队的首席架构师。他在 Microsoft 的职业生涯始于为 Framework 第一个版本设计 API。目前，他正在领导制定、推广并将设计和架构标准应用于 .NET Framework 开发的工作。他是 *框架设计指南*（Addison-Wesley，2005）的合著者。可通过其博客 http://blogs.msdn.com/kcwalina 联系他。

Jesse Liberty（“Silverlight 极客”）是 Microsoft 的高级项目经理，也是众多畅销编程书籍和数十篇热门文章的作者。他还是世界各地活动的常邀演讲者。他的博客 http://JesseLiberty.com 是 Silverlight、WPF 和 Windows Phone 7 开发者的必读内容。Jesse 拥有超过二十年的实际编程经验，包括在花旗银行担任副总裁以及在 AT&T 担任杰出软件工程师的经历。可通过他的博客联系他，并在 @JesseLiberty 关注他。

**Eric Lippert** 是 Microsoft C# 编译器团队的高级开发人员。他参与过 Visual Basic、VBScript、JScript 和 C# 语言以及 Visual Studio Tools For Office 的设计与实现工作。他关于上述所有主题及其他主题的博客可在 http://blogs.msdn.com/EricLippert 找到。

**Christian Nagel** 是 Microsoft 区域总监和 MVP。他是多本书的作者，包括 *.NET 4 专业 C#*（Wrox，2010）和 *.NET Framework 企业服务*（Addison-Wesley，2005）。作为 CN innovation 的创始人和 thinktecture 的合伙人，他为软件开发者教授和指导各种 Microsoft .NET 技术。可通过 http://www.cninnovation.com 联系 Christian。

**Vladimir Reshetnikov** 是 Visual C# 方向的 Microsoft MVP。他拥有超过八年的软件开发经验，以及约六年的 Microsoft .NET 和 C# 经验。可通过其博客 http://nikov-thoughts.blogspot.com 联系他。

**Marek Safar** 是 Novell C# 编译器团队的首席开发人员。过去五年中，他一直在参与 Mono C# 编译器的大部分功能开发工作。可通过其博客 http://mareksafar.blogspot.com 联系他。

**Chris Sells** 是 Microsoft Corporation 业务平台部门（即 SQL Server 部门）的项目经理。他写过多本书，包括 *WPF 编程*（O'Reilly，2007）、*Windows Forms 2.0 编程*（Addison-Wesley，2006）和 *ATL 内幕*（Addison-Wesley，1999）。业余时间，Chris 主持各种会议，并在 Microsoft 内部产品团队讨论列表中“捣乱”。关于 Chris 及其各种项目的更多信息可在 http://www.sellsbrothers.com 获取。

**Peter Sestoft** 是丹麦哥本哈根 IT 大学的软件开发教授。2003 年至 2006 年，他是 ECMA International C# 标准化委员会的成员，并且是 *C# 精粹*（MIT Press，2004）和 *Java 精粹*（MIT Press，2005）的作者。可在 http://www.itu.dk/people/sestoft 找到他。

**Jon Skeet** 是 *C# 深入解析*（Manning，2010）的作者，也是一位 C# MVP。他在伦敦的 Google 工作，业余时间撰写和演讲关于 C# 的内容。他的博客位于 http://msmvps.com/jon.skeet——或者你可以发现他大多数日子都在 Stack Overflow（http://stackoverflow.com）上回答问题。

**Bill Wagner** 是 SRT Solutions 的创始人、Microsoft 区域总监和 C# MVP。他职业生涯的绝大部分时间都在花括号之间度过。他是 *C# 高效编程*（Addison-Wesley，2005）和 *C# 高效编程（续）*（Addison-Wesley，2009）的作者，曾任 *Visual Studio 杂志* 的 C# 专栏作家，并为 MSDN 上的 C# 开发者中心撰稿。你可以在 http://srtsolutions.com/blogs/billwagner 了解他关于 C# 及其他主题不断发展的想法。

## 1. 引言

C#（读作“See Sharp”）是一种简单、现代、面向对象且类型安全的编程语言。C# 源于 C 语言家族，C、C++ 和 Java 程序员会立即熟悉它。C# 由 ECMA International 标准化为 *ECMA-334* 标准，并由 ISO/IEC 标准化为 *ISO/IEC 23270* 标准。Microsoft 针对 .NET Framework 的 C# 编译器是这两项标准的符合性实现。

C# 是一种面向对象语言，但 C# 进一步包含对 *面向组件* 编程的支持。当代软件设计越来越依赖于以自包含和自描述的功能包形式存在的软件组件。此类组件的关键在于：它们呈现一种带有属性、方法和事件的编程模型；它们具有提供组件声明式信息的特性；并且它们包含自己的文档。C# 提供语言构造来直接支持这些概念，使 C# 成为创建和使用软件组件的一种非常自然的语言。

C# 的若干特性有助于构建健壮且耐用的应用程序：*垃圾回收* 会自动回收未使用对象占用的内存；*异常处理* 提供了一种结构化且可扩展的错误检测和恢复方法；而该语言的 *类型安全* 设计使得无法读取未初始化的变量、无法索引超出数组边界，也无法执行未经检查的类型转换。

C# 具有 *统一类型系统*。所有 C# 类型，包括 int 和 double 等基元类型，都继承自单个根对象类型。因此，所有类型共享一组公共操作，任何类型的值都可以以一致的方式存储、传输和操作。此外，C# 同时支持用户定义的引用类型和值类型，允许动态分配对象以及轻量级结构的内联存储。

为确保 C# 程序和库能够以兼容的方式随时间演进，C# 的设计非常强调 *版本控制*。许多编程语言很少关注这一问题。结果，当引入依赖库的较新版本时，用这些语言编写的程序会比必要情况下更频繁地中断。C# 设计中直接受版本控制考虑影响的方面包括分开的 virtual 和 override 修饰符、方法重载解析规则，以及对显式接口成员声明的支持。

本章其余部分描述 C# 语言的基本特性。尽管后续章节会以注重细节、有时是数学化的方式描述规则和例外情况，但本章力求清晰简洁，而不追求完整性。其目的是为读者提供该语言的入门介绍，以便于编写早期程序和阅读后续章节。

> **CHRIS SELLS** 我完全愿意接受“现代、面向对象且类型安全”的说法，但 C# 已经远不像从前那么简单了。不过，鉴于该语言在 C# 2.0 中增加了泛型和匿名委托等功能，在 C# 3.0 中增加了 LINQ 相关功能，在 C# 4.0 中增加了动态值，程序本身变得更简单、更可读、更易维护——这应当成为任何编程语言的目标。

> **ERIC LIPPERT** C# 也日益成为一种函数式编程语言。类型推断、lambda 表达式和单子查询推导（monadic query comprehensions）等特性，使传统面向对象开发者能够运用函数式语言中的这些思想来提高语言的表达力。

> **CHRISTIAN NAGEL** C# 并非纯粹的面向对象语言，而是一种随时间不断扩展的语言，以便在 C# 的主要应用领域获得更高的生产力。使用 C# 3.0 编写的程序，与使用 C# 1.0 并结合函数式编程构造编写的程序，看起来可能完全不同。

> **JON SKEET** C# 的某些方面确实随着时间推移使该语言更具函数式特性——但与此同时，C# 3.0 中的自动实现属性和对象初始值设定项又鼓励了可变性。未来版本中是否会出现鼓励不可变性的特性，以及是否会对元组、模式匹配和尾递归等其他领域提供支持，将值得关注。

> **BILL WAGNER** 自 C# 规范第一版以来，本节内容没有变化。显然，该语言已经成长并增加了新的惯用法——然而 C# 仍然是一种平易近人的语言。这些高级特性始终触手可及，但并非每个程序都必须使用。即使 C# 变得越来越强大，它对经验不足的开发者仍然平易近人。




## 1. 引言

### 1.1 Hello, World

“Hello, World”程序传统上用于介绍一种编程语言。下面是 C# 中的写法：

```csharp
using System;
class Hello
{
    static void Main() {
        Console.WriteLine("Hello, World");
    }
}
```

C# 源文件通常具有 .cs 文件扩展名。假设“Hello, World”程序存储在文件 hello.cs 中，则可以使用以下命令行通过 Microsoft C# 编译器编译该程序

```
csc hello.cs
```

这会生成一个名为 hello.exe 的可执行程序集。此应用程序运行时产生的输出为

```
Hello, World
```

“Hello, World”程序以引用 System 命名空间的 using 指令开头。命名空间提供了一种分层方式来组织 C# 程序和库。命名空间包含类型和其他命名空间——例如，System 命名空间包含若干类型，如程序中引用的 Console 类，还包含若干其他命名空间，如 IO 和 Collections。引用给定命名空间的 using 指令允许非限定地使用属于该命名空间的类型。由于有 using 指令，程序可以使用 Console.WriteLine 作为 System.Console.WriteLine 的简写。

“Hello, World”程序声明的 Hello 类只有一个成员，即名为 Main 的方法。Main 方法使用 static 修饰符声明。实例方法可以使用关键字 this 引用特定的包含对象实例，而静态方法运行时不需要引用特定对象。按照约定，名为 Main 的静态方法用作程序的入口点。

程序的输出由 System 命名空间中 Console 类的 WriteLine 方法产生。该类由 .NET Framework 类库提供，默认情况下，Microsoft C# 编译器会自动引用这些类库。请注意，C# 本身没有单独的运行时库。相反，.NET Framework 就是 C# 的运行时库。

> **BRAD ABRAMS** 有趣的是，Console.WriteLine() 只是 Console.Out.WriteLine 的快捷方式。Console.Out 是一个属性，它返回 System.IO.TextWriter 基类的一个实现，该基类旨在输出到控制台。前面的示例同样可以正确地写成如下形式：
> 
> ```csharp
> using System;
> class Hello
> {
>     static void Main() {
>         Console.Out.WriteLine("Hello, World");
>     }
> }
> ```
> 
> 在框架设计的早期，我们密切关注 C# 语言规范这一部分究竟必须如何编写，以此作为语言复杂度的风向标。我们选择在 Console 上添加这个便利重载，使“Hello, World”的编写容易得多。从各方面来看，这似乎已经得到了回报。事实上，如今几乎看不到对 Console.Out.WriteLine() 的调用。

### 1.2 程序结构

C# 中的关键组织概念是*程序*、*命名空间*、*类型*、*成员*和*程序集*。C# 程序由一个或多个源文件组成。程序声明类型，类型包含成员，并且可以组织到命名空间中。类和接口是类型的示例。字段、方法、属性和事件是成员的示例。编译 C# 程序时，它们会在物理上打包到程序集中。程序集通常具有文件扩展名 *.exe* 或 *.dll*，具体取决于它们实现的是*应用程序*还是*库*。

下面的示例

```csharp
using System;

namespace Acme.Collections
{
    public class Stack
    {
        Entry top;

        public void Push(object data) {
            top = new Entry(top, data);
        }

        public object Pop() {
            if (top == null) throw new InvalidOperationException();
            object result = top.data;
            top = top.next;
            return result;
        }

        class Entry
        {
            public Entry next;
            public object data;
            public Entry(Entry next, object data) {
                this.next = next;
                this.data = data;
            }
        }
    }
}
```

在名为 Acme.Collections 的命名空间中声明一个名为 Stack 的类。此类的完全限定名为 Acme.Collections.Stack。该类包含若干成员：一个名为 top 的字段、两个名为 Push 和 Pop 的方法，以及一个名为 Entry 的嵌套类。Entry 类还包含三个成员：一个名为 next 的字段、一个名为 data 的字段和一个构造函数。假设该示例的源代码存储在文件 acme.cs 中，则以下命令行将示例编译为库（没有 Main 入口点的代码），并生成名为 acme.dll 的程序集。

```
csc /t:library acme.cs
```

程序集包含以中间语言（IL）指令形式存在的可执行代码，以及以元数据形式存在的符号信息。在执行之前，程序集中的 IL 代码会由 .NET 公共语言运行时的实时（JIT）编译器自动转换为特定于处理器的代码。

由于程序集是一个自描述的功能单元，同时包含代码和元数据，因此 C# 中不需要 #include 指令和头文件。特定程序集中包含的公共类型和成员只需在编译程序时引用该程序集，即可在 C# 程序中使用。例如，下面的程序使用 acme.dll 程序集中的 Acme.Collections.Stack 类：

```csharp
using System;
using Acme.Collections;
class Test
{
    static void Main() {
        Stack s = new Stack();
        s.Push(1);
        s.Push(10);
        s.Push(100);
        Console.WriteLine(s.Pop());
        Console.WriteLine(s.Pop());
        Console.WriteLine(s.Pop());
    }
}
```

如果该程序存储在文件 test.cs 中，则在编译 test.cs 时，可以使用编译器的 /r 选项引用 acme.dll 程序集：

```
csc /r:acme.dll test.cs
```

这会创建一个名为 test.exe 的可执行程序集；运行该程序集时，将产生以下输出：

```
100
10
1
```

C# 允许将程序的源文本存储在多个源文件中。编译多文件 C# 程序时，所有源文件会一起处理，并且源文件可以自由地相互引用——从概念上讲，就好像所有源文件在被处理之前已串联成一个大文件。C# 中永远不需要前向声明，因为除极少数例外情况外，声明顺序无关紧要。C# 不限制一个源文件只能声明一个公共类型，也不要求源文件的名称与源文件中声明的类型相匹配。

> > **ERIC LIPPERT** 这与 Java 语言不同。另外，C# 中声明顺序无关紧要这一点也与 C++ 语言不同。
>
> > **CHRIS SELLS** 请注意前一个示例中的 using Acme.Collections 语句，它看起来像 C 风格的 #include 指令，但其实不是。它只是一种命名上的便利，使编译器在遇到 Stack 时，有一组命名空间可以在其中查找该类。如果此示例使用完全限定名，编译器也会采取相同的操作：
> >
> > `Acme.Collections.Stack s = new Acme.Collections.Stack();`

### 1.3 类型和变量

C# 中有两种类型：*值类型*和*引用类型*。值类型的变量直接包含其数据，而引用类型的变量存储对其数据的引用，后者称为对象。使用引用类型时，两个变量可以引用同一个对象，因此对一个变量执行的操作可能会影响另一个变量所引用的对象。使用值类型时，每个变量都有自己的数据副本，对一个变量执行的操作不可能影响另一个变量（ref 和 out 参数变量除外）。

> **JON SKEET** 为引用类型选择“reference”这个词也许并不幸运。在考虑参数传递的按引用传递和按值传递语义之间的区别时，它导致了大量混淆（或至少是沟通不畅）。
> 
> 值类型和引用类型之间的区别可能是教 C# 初学者时最重要的一点：在理解这一点之前，几乎其他所有内容都说不通。

> **ERIC LIPPERT** 关于值类型最常见的误解大概是：它们“存储在栈上”，而引用类型“存储在堆上”。首先，这种行为是运行时的实现细节，而不是语言本身的事实。其次，这并不能向初学者说明什么。第三，这是错误的：是的，与引用类型实例关联的数据存储在堆上，但这些数据可以包含值类型的实例，因此值类型有时也存储在堆上。第四，如果值类型和引用类型之间的区别在于它们的存储细节，那么 CLR 团队就会把它们称为“栈类型”和“堆类型”。真正的区别在于：值类型按值复制，引用类型按引用复制；运行时如何分配存储来实现生存期规则，在绝大多数主流编程场景中并不重要。

> **BILL WAGNER** C# 强制你为类型做出值语义与引用语义这一重要决定。使用你的类型的开发者不能在每次使用时做出该决定（不像在 C++ 中那样）。你需要考虑类型的用法模式，并在这两种类型之间做出谨慎决定。

> **VLADIMIR RESHETNIKOV** C# 还支持不安全指针类型，本规范末尾将对此进行描述。它们被称为“不安全”，是因为疏忽使用它们可能以编译器无法捕获的方式破坏类型安全。




C# 的值类型进一步分为**简单类型**、**枚举类型**、**结构类型**和**可空类型**。C# 的引用类型进一步分为**类类型**、**接口类型**、**数组类型**和**委托类型**。

下表概述了 C# 的类型系统。

| 类别 | 子类别 | 描述 |
| --- | --- | --- |
| 值类型 | 简单类型 | 有符号整型：`sbyte`、`short`、`int`、`long` |
| 值类型 | 简单类型 | 无符号整型：`byte`、`ushort`、`uint`、`ulong` |
| 值类型 | 简单类型 | Unicode 字符：`char` |
| 值类型 | 简单类型 | IEEE 浮点数：`float`、`double` |
| 值类型 | 简单类型 | 高精度十进制：`decimal` |
| 值类型 | 简单类型 | 布尔值：`bool` |
| 值类型 | 枚举类型 | 形式为 `enum E {...}` 的用户定义类型 |
| 值类型 | 结构类型 | 形式为 `struct S {...}` 的用户定义类型 |
| 值类型 | 可空类型 | 所有其他值类型的扩展，可具有 `null` 值 |
| 引用类型 | 类类型 | 所有其他类型的最终基类：`object` |
| 引用类型 | 类类型 | Unicode 字符串：`string` |
| 引用类型 | 类类型 | 形式为 `class C {...}` 的用户定义类型 |
| 引用类型 | 接口类型 | 形式为 `interface I {...}` 的用户定义类型 |
| 引用类型 | 数组类型 | 一维和多维；例如 `int[]` 和 `int[,]` |
| 引用类型 | 委托类型 | 例如形式为 `delegate int D(...)` 的用户定义类型 |

八种整型支持 8 位、16 位、32 位和 64 位的有符号或无符号值。

> **乔恩·斯基特** 为 byte 是无符号类型而欢呼！在 Java 中，byte 是有符号的（而且没有无符号等价类型），这使得许多位操作毫无必要地容易出错。
>
> 请注意，我们完全可能都应该比现在更多地使用 uint：我确信许多开发者在需要整数类型时默认会使用 int。当然，框架设计者也不例外：为什么 String.Length 应该是有符号的呢？

> **埃里克·利珀特** 对乔恩的问题，答案是：该框架的设计目标是与公共语言规范（CLS）良好协作。CLS 定义了一组基本语言特性，所有符合 CLS 的语言都应能够使用这些特性；无符号整数不在 CLS 子集中。

两种浮点类型 float 和 double 分别使用 32 位单精度和 64 位双精度 IEEE 754 格式表示。

decimal 类型是一种 128 位数据类型，适用于财务和货币计算。

> **乔恩·斯基特** 这两段暗示 decimal 不是浮点类型。它是——它只是浮点十进制类型，而 float 和 double 是浮点二进制类型。

C# 的 bool 类型用于表示布尔值——即 true 或 false 的值。

C# 中的字符和字符串处理使用 Unicode 编码。char 类型表示一个 UTF-16 代码单元，string 类型表示一系列 UTF-16 代码单元。

下表总结了 C# 的数值类型。

| 类别 | 位数 | 类型 | 范围/精度 |
| --- | --- | --- | --- |
| 有符号整型 | 8 | sbyte | -128...127 |
| 有符号整型 | 16 | short | -32,768...32,767 |
| 有符号整型 | 32 | int | -2,147,483,648...2,147,483,647 |
| 有符号整型 | 64 | long | -9,223,372,036,854,775,808...9,223,372,036,854,775,807 |
| 无符号整型 | 8 | byte | 0...255 |
| 无符号整型 | 16 | ushort | 0...65,535 |
| 无符号整型 | 32 | uint | 0...4,294,967,295 |
| 无符号整型 | 64 | ulong | 0...18,446,744,073,709,551,615 |
| 浮点 | 32 | float | 1.5 × 10⁻⁴⁵ 到 3.4 × 10³⁸，7 位精度 |
| 浮点 | 64 | double | 5.0 × 10⁻³²⁴ 到 1.7 × 10³⁰⁸，15 位精度 |
| 十进制 | 128 | decimal | 1.0 × 10⁻²⁸ 到 7.9 × 10²⁸，28 位精度 |

> > **克里斯蒂安·纳格尔** 我们在不同平台上使用 C++ 时遇到的问题之一是，标准没有定义 short、int 和 long 所使用的位数。标准只定义了 short <= int <= long，这导致在 16 位、32 位和 64 位平台上大小不同。使用 C# 时，无论使用哪个平台，数值类型的长度都有明确定义。

C# 程序使用*类型声明*来创建新类型。类型声明指定新类型的名称和成员。C# 的类型类别中有五类可由用户定义：类类型、结构类型、接口类型、枚举类型和委托类型。

类类型定义一种数据结构，其中包含数据成员（字段）和函数成员（方法、属性及其他成员）。类类型支持单继承和多态，这些机制使派生类能够扩展和特化基类。

> > **埃里克·利珀特** 选择在类上支持单继承而非多重继承，一举消除了多重继承语言中存在的许多复杂边界情况。

结构类型与类类型相似，因为它表示一种包含数据成员和函数成员的结构。然而，与类不同，结构是值类型，不需要堆分配。结构类型不支持用户指定的继承，所有结构类型都隐式继承自 object 类型。

## 1. 引言

> > **弗拉基米尔·列舍特尼科夫** 结构间接继承自 object。它们的隐式直接基类是 `System.ValueType`，而后者直接继承自 `object`。

接口类型将契约定义为具有名称的一组公共函数成员。实现接口的类或结构必须提供该接口函数成员的实现。一个接口可以继承多个基接口，一个类或结构可以实现多个接口。

委托类型表示对具有特定参数列表和返回类型的方法的引用。委托使方法可以像实体一样被赋值给变量并作为参数传递。委托类似于其他一些语言中的函数指针概念，但与函数指针不同，委托是面向对象的且类型安全的。

类、结构、接口和委托类型都支持泛型，因此可以用其他类型进行参数化。

枚举类型是一种具有命名常量的独特类型。每个枚举类型都有一个基础类型，该类型必须是八种整型之一。枚举类型的值集与基础类型的值集相同。

> > **弗拉基米尔·列舍特尼科夫** 枚举类型不能在其声明中包含类型参数。即便如此，如果嵌套在泛型类或结构类型中，它们也可以是泛型的。此外，C# 在不安全代码中支持指向泛型枚举类型的指针。
> >
> > 在本规范中，枚举类型有时被称为“枚举类型”。这两个名称完全可以互换。

C# 支持任意类型的一维数组和多维数组。与上面列出的类型不同，数组类型无需先声明即可使用。相反，数组类型是通过在类型名称后跟方括号构造的。例如，int[] 是 int 的一维数组，int[,] 是 int 的二维数组，而 int[][] 是 int 的一维数组的一维数组。

可空类型也无需先声明即可使用。对于每个不可空值类型 T，都有一个对应的可空类型 T?，它可以额外保存 null 值。例如，int? 是一种可以保存任何 32 位整数或 null 值的类型。

> > **克里斯蒂安·纳格尔** `T?` 是 `Nullable<T>` 结构的 C# 简写表示法。

> **埃里克·利珀特** 在 C# 1.0 中，我们有可空引用类型和不可空值类型。在 C# 2.0 中，我们添加了可空值类型。但不存在不可空引用类型。如果一切重来，我们可能从一开始就把可空性和不可空性融入类型系统。不幸的是，不可空引用类型很难添加到并非为其设计的现有类型系统中。我们一直收到关于不可空引用类型的特性请求；这将是一个很棒的特性。然而，代码契约在解决不可空引用类型所解决的问题方面大有帮助；如果你想在程序中强制不可空性，可以考虑使用它们。如果你对这个主题感兴趣，可能还想了解 Spec#，这是 Microsoft Research 的一个 C# 版本，它确实支持不可空引用类型。

C# 的类型系统是统一的，因此任何类型的值都可以被视为对象。C# 中的每个类型都直接或间接派生自 object 类类型，而 object 是所有类型的最终基类。引用类型的值只需将其视为 object 类型即可当作对象处理。值类型的值通过执行装箱和拆箱操作来当作对象处理。在以下示例中，int 值被转换为 object，然后再转换回 int。

```csharp
using System;

class Test
{
    static void Main() {
        int i = 123;
        object o = i;    // Boxing
        int j = (int)o;  // Unboxing
    }
}
```

当值类型的值转换为 object 类型时，会分配一个对象实例（也称为“箱”）来保存该值，并将该值复制到该箱中。反过来，当对象引用强制转换为值类型时，会检查所引用的对象是否为正确值类型的箱；如果检查成功，则将该箱中的值复制出来。

C# 的统一类型系统实际上意味着值类型可以“按需”成为对象。由于这种统一，使用 object 类型的通用库既可用于引用类型，也可用于值类型。

C# 中有几种变量，包括字段、数组元素、局部变量和参数。变量表示存储位置，每个变量都有一个类型，该类型决定可以在变量中存储哪些值，如下表所示。



| 变量类型 | 可能内容 |
| --- | --- |
| 非可空值类型 | 该确切类型的值 |
| 可空值类型 | 空值或该确切类型的值 |
| object | 空引用、对任意引用类型对象的引用，或对任意值类型的装箱值的引用 |
| 类类型 | 空引用、对该类类型实例的引用，或对该类类型派生类的实例的引用 |
| 接口类型 | 空引用、对实现该接口类型的类类型实例的引用，或对实现该接口类型的值类型的装箱值的引用 |
| 数组类型 | 空引用、对该数组类型实例的引用，或对兼容数组类型实例的引用 |
| 委托类型 | 空引用或对该委托类型实例的引用 |

### 1.4 表达式

表达式由操作数和运算符构成。表达式的运算符指示要对操作数应用哪些运算。运算符的示例包括 +、-、*、/ 和 new。操作数的示例包括字面量、字段、局部变量和表达式。

当表达式包含多个运算符时，运算符的优先级控制各个运算符的计算顺序。例如，表达式 x + y * z 按 x + (y * z) 计算，因为 * 运算符的优先级高于 + 运算符。

> **ERIC LIPPERT** 优先级控制运算符的执行顺序，但不控制操作数的计算顺序。操作数从左到右计算，句号。在前面的示例中，会先计算 x，然后计算 y，然后计算 z，然后执行乘法，然后执行加法。操作数 x 的计算先于 y 的计算，因为 x 在 y 的左侧；乘法的计算先于加法，因为乘法具有更高的优先级。

大多数运算符都可以重载。运算符重载允许在操作数中的一个或两个为用户定义的类或结构类型时，为相应运算指定用户定义的运算符实现。

#### 1.4.1 运算符

下表汇总了 C# 的运算符，按优先级从高到低列出运算符类别。同一类别中的运算符具有相同优先级。

| 类别 | 表达式 | 说明 |
| --- | --- | --- |
| 主要 | `x.m` | 成员访问 |
| 主要 | `x(...)` | 方法和委托调用 |
| 主要 | `x[...]` | 数组和索引器访问 |
| 主要 | `x++` | 后置递增 |
| 主要 | `x--` | 后置递减 |
| 主要 | `new T(...)` | 对象和委托创建 |
| 主要 | `new T(...){...}` | 带初始化器的对象创建 |
| 主要 | `new {...}` | 匿名对象初始化器 |
| 主要 | `new T[...]` | 数组创建 |
| 主要 | `typeof(T)` | 获取 T 的 System.Type 对象 |
| 主要 | `checked(x)` | 在 checked 上下文中计算表达式 |
| 主要 | `unchecked(x)` | 在 unchecked 上下文中计算表达式 |
| 主要 | `default(T)` | 获取类型 T 的默认值 |
| 主要 | `delegate {...}` | 匿名函数（匿名方法） |
| 一元 | `+x` | 恒等 |
| 一元 | `-x` | 求负 |
| 一元 | `!x` | 逻辑求反 |
| 一元 | `~x` | 按位求反 |
| 一元 | `++x` | 前置递增 |
| 一元 | `--x` | 前置递减 |
| 一元 | `(T)x` | 将 x 显式转换为类型 T |
| 乘法 | `x * y` | 乘法 |
|  | `x / y` | 除法 |
|  | `x % y` | 求余 |
| 加法 | `x + y` | 加法、字符串串联、委托组合 |
|  | `x - y` | 减法、委托移除 |
| 移位 | `x << y` | 左移 |
|  | `x >> y` | 右移 |
| 关系和类型测试 | `x < y` | 小于 |
|  | `x > y` | 大于 |
|  | `x <= y` | 小于或等于 |
|  | `x >= y` | 大于或等于 |
|  | `x is T` | 如果 x 是 T，则返回 true，否则返回 false |
|  | `x as T` | 返回类型为 T 的 x；如果 x 不是 T，则返回 null |
| 相等 | `x == y` | 等于 |
|  | `x != y` | 不等于 |
| 逻辑 AND | `x & y` | 整数按位 AND、布尔逻辑 AND |
| 逻辑 XOR | `x ^ y` | 整数按位 XOR、布尔逻辑 XOR |
| 逻辑 OR | `x \| y` | 整数按位 OR、布尔逻辑 OR |
| 条件 AND | `x && y` | 仅当 x 为 true 时才计算 y |
| 条件 OR | `x \|\| y` | 仅当 x 为 false 时才计算 y |
| null 合并 | `x ?? y` | 如果 x 为 null，则计算结果为 y；否则为 x |
| 条件 | `x ? y : z` | 如果 x 为 true，则计算 y；如果 x 为 false，则计算 z |
| 赋值或匿名函数 | `x = y` | 赋值 |
|  | `x op= y` | 复合赋值；支持的运算符为 *= /= %= += -= <<= >>= &= ^= \|= |
|  | `(T x) => y` | 匿名函数（lambda 表达式） |

> **ERIC LIPPERT** 人们常常惊讶于 lambda 和匿名方法语法被描述为运算符。它们是不寻常的运算符。更典型的是，你会认为运算符接受表达式作为操作数，而不是形参声明。然而，从语法上看，lambda 和匿名方法语法与其他运算符一样，都是运算符。

### 1.5 语句

程序的操作使用语句来表达。C# 支持多种语句，其中一些是依据嵌入语句定义的。

块允许在只允许单个语句的上下文中编写多个语句。块由写在分隔符 { 和 } 之间的语句列表组成。

声明语句用于声明局部变量和常量。

表达式语句用于计算表达式。可用作语句的表达式包括方法调用、使用 new 运算符的对象分配、使用 = 和复合赋值运算符的赋值，以及使用 ++ 和 -- 运算符的递增和递减操作。

选择语句用于根据某个表达式的值，从多个可能的语句中选择一个来执行。此类语句包括 if 和 switch 语句。

迭代语句用于重复执行嵌入语句。此类语句包括 while、do、for 和 foreach 语句。

跳转语句用于转移控制。此类语句包括 break、continue、goto、throw、return 和 yield 语句。

try...catch 语句用于捕获执行块期间发生的异常，try...finally 语句用于指定无论是否发生异常都始终执行的最终化代码。

> **ERIC LIPPERT** 这有点不准确；当然，*finally* 块并不*总是*执行。try 块中的代码可能进入无限循环，异常可能触发“快速失败”（这会在不运行任何 *finally* 块的情况下终止进程），或者有人可能拔掉电源线。

checked 和 unchecked 语句用于控制整型算术运算和转换的溢出检查上下文。

lock 语句用于获取给定对象的互斥锁，执行一个语句，然后释放该锁。

using 语句用于获取资源，执行一个语句，然后释放该资源。

下表列出 C# 的语句，并为每种语句提供一个示例。

| 语句 | 示例 |
| --- | --- |
| 局部变量声明 | <pre><code>static void Main() {<br>    int a;<br>    int b = 2, c = 3;<br>    a = 1;<br>    Console.WriteLine(a + b + c);<br>}</code></pre> |
| 局部常量声明 | <pre><code>static void Main() {<br>    const float pi = 3.1415927f;<br>    const int r = 25;<br>    Console.WriteLine(pi * r * r);<br>}</code></pre> |
| 表达式语句 | <pre><code>static void Main() {<br>    int i;<br>    i = 123;                 // Expression statement<br>    Console.WriteLine(i);    // Expression statement<br>    i++;<br>    Console.WriteLine(i);    // Expression statement<br>}</code></pre> |




## 1. 引言

| Statement | Example |
|---|---|
| if 语句 | static void Main(string[] args) {<br>&nbsp;&nbsp;&nbsp;&nbsp;if (args.Length == 0) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine("No arguments");<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;else {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine("One or more arguments");<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |
| switch 语句 | static void Main(string[] args) {<br>&nbsp;&nbsp;&nbsp;&nbsp;int n = args.Length;<br>&nbsp;&nbsp;&nbsp;&nbsp;switch (n) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;case 0:<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine("No arguments");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;case 1:<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine("One argument");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;default:<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine("{0} arguments", n);<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |
| while 语句 | static void Main(string[] args) {<br>&nbsp;&nbsp;&nbsp;&nbsp;int i = 0;<br>&nbsp;&nbsp;&nbsp;&nbsp;while (i &lt; args.Length) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(args[i]);<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i++;<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |
| do 语句 | static void Main() {<br>&nbsp;&nbsp;&nbsp;&nbsp;string s;<br>&nbsp;&nbsp;&nbsp;&nbsp;do {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;s = Console.ReadLine();<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (s != null) Console.WriteLine(s);<br>&nbsp;&nbsp;&nbsp;&nbsp;} while (s != null);<br>} |
| for 语句 | static void Main(string[] args) {<br>&nbsp;&nbsp;for (int i = 0; i &lt; args.Length; i++) {<br>&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(args[i]);<br>&nbsp;&nbsp;}<br>} |
| foreach 语句 | static void Main(string[] args) {<br>&nbsp;&nbsp;foreach (string s in args) {<br>&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(s);<br>&nbsp;&nbsp;}<br>} |
| break 语句 | static void Main() {<br>&nbsp;&nbsp;while (true) {<br>&nbsp;&nbsp;&nbsp;&nbsp;string s = Console.ReadLine();<br>&nbsp;&nbsp;&nbsp;&nbsp;if (s == null) break;<br>&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(s);<br>&nbsp;&nbsp;}<br>} |
| continue 语句 | static void Main(string[] args) {<br>&nbsp;&nbsp;for (int i = 0; i &lt; args.Length; i++) {<br>&nbsp;&nbsp;&nbsp;&nbsp;if (args[i].StartsWith("//")) continue;<br>&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(args[i]);<br>&nbsp;&nbsp;}<br>} |
| goto 语句 | static void Main(string[] args) {<br>&nbsp;&nbsp;int i = 0;<br>&nbsp;&nbsp;goto check;<br>&nbsp;&nbsp;loop:<br>&nbsp;&nbsp;Console.WriteLine(args[i++]);<br>&nbsp;&nbsp;check:<br>&nbsp;&nbsp;if (i &lt; args.Length) goto loop;<br>} |
| return 语句 | static int Add(int a, int b) {<br>&nbsp;&nbsp;return a + b;<br>}<br>static void Main() {<br>&nbsp;&nbsp;Console.WriteLine(Add(1, 2));<br>&nbsp;&nbsp;return;<br>} |
| yield 语句 | `static IEnumerable<int> Range(int from, int to) { for (int i = from; i < to; i++) { yield return i; } yield break; } static void Main() { foreach (int x in Range(-10,10)) { Console.WriteLine(x); } }` |
| throw 和 try 语句 | `static double Divide(double x, double y) { if (y == 0) throw new DivideByZeroException(); return x / y; } static void Main(string[] args) { try { if (args.Length != 2) { throw new Exception("Two numbers required"); } double x = double.Parse(args[0]); double y = double.Parse(args[1]); Console.WriteLine(Divide(x, y)); } catch (Exception e) { Console.WriteLine(e.Message); } finally { Console.WriteLine("Good bye!"); } }` |
| checked 和 unchecked 语句 | `static void Main() { int i = int.MaxValue; checked { Console.WriteLine(i + 1); // Exception } unchecked { Console.WriteLine(i + 1); // Overflow } }` |
| lock 语句 | class Account {<br>&nbsp;&nbsp;decimal balance;<br>&nbsp;&nbsp;public void Withdraw(decimal amount) {<br>&nbsp;&nbsp;&nbsp;&nbsp;lock (this) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (amount &gt; balance) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;throw new Exception("Insufficient funds");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;balance -= amount;<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;}<br>} |
| using 语句 | static void Main() {<br>&nbsp;&nbsp;using (TextWriter w = File.CreateText("test.txt")) {<br>&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line one");<br>&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line two");<br>&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line three");<br>&nbsp;&nbsp;}<br>} |

### 1.6 类和对象

*类* 是 C# 类型中最基础的。类是一种数据结构，它将状态（字段）和操作（方法和其他函数成员）组合在单个单元中。类为动态创建的类的 *实例* 提供定义，也称为 *对象*。类支持 *继承* 和 *多态性*，通过这些机制，*派生类* 可以扩展和特化 *基类*。

新类使用类声明创建。类声明以指定类的属性和修饰符、类名、基类（如果给出）以及类实现的接口的头开始。头后面跟着类体，它由写在大括号 { 和 } 之间的成员声明列表组成。

下面是名为 Point 的简单类的声明：

```
public class Point
{
    public int x, y;
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}
```

类的实例使用 new 运算符创建，该运算符为新实例分配内存，调用构造函数初始化实例，并返回对实例的引用。以下语句创建两个 Point 对象并将对这些对象的引用存储在两个变量中：

```
Point p1 = new Point(0, 0);
Point p2 = new Point(10, 20);
```

对象占用的内存会在对象不再使用时自动回收。在 C# 中既不需要也不可能显式释放对象。

#### 1.6.1 成员

类的成员要么是静态成员，要么是实例成员。静态成员属于类，实例成员属于对象（类的实例）。

> ERIC LIPPERT  术语“static”之所以被选择，是因为它对使用类似语言的用户来说很熟悉，而不是因为它是对“由类的所有实例共享”的特别合理或描述性的术语。

> JON SKEET  我认为“shared”（如 Visual Basic 中使用）也给出了错误的印象。“Sharing”感觉像是需要一个或多个参与者，而静态成员不需要类型的任何实例。我有完美的术语来描述这种情况，但为时已晚，无法将“static”更改为“associated-with-the-type-rather-than-with-any-specific-instance-of-the-type”（连字符可选）。

下表提供了类可以包含的成员种类的概述。

| Member | Description |
|---|---|
| Constants | 与类关联的常量值 |
| Fields | 类的变量 |
| Methods | 类可以执行的计算和操作 |
| Properties | 与读取和写入类的命名属性相关联的操作 |
| Indexers | 与像数组一样索引类的实例相关联的操作 |
| Events | 类可以生成的通知 |
| Operators | 类支持的转换和表达式运算符 |
| Constructors | 初始化类的实例或类本身所需的操作 |
| Destructors | 在类的实例被永久丢弃之前执行的操作 |
| Types | 类声明的嵌套类型 |

#### 1.6.2 可访问性

类的每个成员都有一个关联的可访问性，它控制能够访问该成员的程序文本区域。以下表格总结了可访问性的五种可能形式。

| Accessibility | Meaning |
|---|---|
| public | 访问不受限制 |
| protected | 访问仅限于此类或派生自此类 |
| internal | 访问仅限于此程序 |
| protected internal | 访问仅限于此程序或派生自此类 |
| private | 访问仅限于此类 |

> **KRZYSZTOF CWALINA**  人们在使用 `public` 关键字时需要小心。C# 中的 `public` *不* 等同于 C++ 中的 `public`！在 C++ 中，它的意思是“内部于我的编译单元”。在 C# 中，它的意思是 C++ 中 extern 的含义（即每个人都可以调用它）。这是一个巨大的差异！

> **CHRISTIAN NAGEL**  我会将 internal 访问修饰符描述为“访问仅限于此程序集”，而不是“访问仅限于此程序”。如果 internal 访问修饰符在 DLL 中使用，引用该 DLL 的 EXE 无法访问它。

> **ERIC LIPPERT**  `protected internal` 证明是一个有争议且 somewhat 不幸的选择。许多使用此功能的人错误地认为 `protected internal` 的意思是“访问仅限于此程序中的派生类”。也就是说，他们认为它意味着 *更* 严格的组合，而实际上它意味着 *更* 不严格的组合。记住这种关系的办法是记住成员的“自然”状态是“private”，并且每个可访问性修饰符都会使可访问性域变大。
>
> 如果 C# 语言的假设未来版本为“protected 和 internal 的更严格组合”提供语法，那么问题就是哪种关键字组合会有意义。我坚持要么“proternal”要么“inteched”，但我怀疑我将不得不忍受失望。

> **CHRISTIAN NAGEL**  C# 定义 `protected internal` 以将访问限制为此程序集或派生自此类。CLR 还允许将访问限制为此程序集和派生自此类。C++/CLI 使用 `public private` 访问修饰符（或 `private public`——顺序无关紧要）提供此 CLR 功能。实际上，此访问修饰符很少使用。

#### 1.6.3 类型参数

类定义可以通过在类名后跟随尖括号中包含的类型参数名称列表来指定一组类型参数。然后可以在类声明的主体中使用类型参数来定义类的成员。在下面的示例中，Pair 的类型参数是 TFirst 和 TSecond：

```
public class Pair<TFirst, TSecond>
{
    public TFirst First;

    public TSecond Second;
}
```

声明为接受类型参数的类类型称为泛型类类型。结构体、接口和委托类型也可以是泛型的。



> **埃里克·利珀特**  
> 如果你需要一个二元组、三元组等等，CLR 4 版框架中定义的泛型“元组”类型是很方便的类型。

当使用泛型类时，必须为每个类型参数提供类型实参：

```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First;   // TFirst is int
string s = pair.Second; // TSecond is string
```

像上面的 Pair<int,string> 这样提供了类型实参的泛型类型称为构造类型。

#### 1.6.4 基类

类声明可以通过在类名和类型参数之后加上冒号和基类的名称来指定基类。省略基类指定与从类型 object 派生相同。在下面的示例中，Point3D 的基类是 Point，Point 的基类是 object：

```csharp
public class Point
{
    public int x, y;
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

public class Point3D : Point
{
    public int z;
    public Point3D(int x, int y, int z): base(x, y)
    {
        this.z = z;
    }
}
```

类继承其基类的成员。继承意味着一个类隐式包含其基类的所有成员，但基类的实例构造函数、静态构造函数和析构函数除外。派生类可以向其继承的成员中添加新成员，但不能移除已继承成员的定义。在前面的示例中，Point3D 从 Point 继承 x 和 y 字段，每个 Point3D 实例都包含 x、y 和 z 三个字段。

> **杰西·利伯蒂**  
> 对于 C# 来说，没有什么比继承和多态更重要的概念需要理解了。这些概念是这门语言的核心，也是面向对象编程的灵魂。请阅读本节直到理解为止，或者寻求帮助，或用额外阅读来补充，但不要跳过它——这些内容是 C# 不可或缺的要素。

存在从类类型到其任何基类类型的隐式转换。因此，类类型的变量可以引用该类的实例或任何派生类的实例。例如，给定前面的类声明，Point 类型的变量既可以引用 Point，也可以引用 Point3D：

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

#### 1.6.5 字段

字段是与类或类的实例关联的变量。

用 static 修饰符声明的字段定义*静态字段*。静态字段恰好标识一个存储位置。无论创建多少个类的实例，静态字段始终只有一份副本。

> **埃里克·利珀特**  
> 对于泛型类型，静态字段是按构造类型区分的。也就是说，如果你有
>
>     class Stack<T> {
>         public readonly static Stack<T> empty = whatever; ...
>     }
>
> 那么 Stack<int>.empty 与 Stack<string>.empty 是不同的字段。

不使用 static 修饰符声明的字段定义*实例字段*。类的每个实例都包含该类所有实例字段的单独副本。

在下面的示例中，Color 类的每个实例都有 r、g、b 实例字段的单独副本，但 Black、White、Red、Green 和 Blue 静态字段只有一份副本：

```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte r, g, b;

    public Color(byte r, byte g, byte b)
    {
        this.r = r;
        this.g = g;
        this.b = b;
    }
}
```

如前面的示例所示，*只读字段*可以用 readonly 修饰符声明。对 readonly 字段的赋值只能作为字段声明的一部分，或在同一个类的构造函数中进行。

> **布拉德·艾布拉姆斯**  
> readonly 保护字段的位置在类型构造函数之外不被更改，但不保护该位置上的值。例如，考虑以下类型：
>
> ```csharp
> public class Names
> {
>     public static readonly StringBuilder FirstBorn = new StringBuilder("Joe");
>     public static readonly StringBuilder SecondBorn = new StringBuilder("Sue");
> }
> ```
>
> 在构造函数之外，直接更改 FirstBorn 实例会导致编译器错误：
>
> ```csharp
> Names.FirstBorn = new StringBuilder("Biff");
> // Compile error
> ```
>
> 但是，我可以通过修改 StringBuilder 实例来实现完全相同的结果：
>
> ```csharp
> Names.FirstBorn.Remove(0,6).Append("Biff");
> Console.WriteLine(Names.FirstBorn);    // Outputs "Biff"
> ```
>
> 正是由于这个原因，我们强烈建议将只读字段限制为不可变类型。不可变类型没有任何公开暴露的 setter，例如 int、double 或 String。

> **比尔·瓦格纳**  
> 几种著名的设计模式利用了可变类型的只读字段。适配器（Adapter）、装饰器（Decorator）、外观（Façade）和代理（Proxy）模式是最明显的例子。当你通过组合较小的结构来创建较大的结构时，你经常会使用只读字段来表示这些较小结构的实例。可变类型的只读字段应表明正在使用这些结构模式之一。

#### 1.6.6 方法

方法是一个成员，它实现可由对象或类执行的计算或操作。静态方法通过类访问。实例方法通过类的实例访问。

方法有一个（可能为空的）参数列表，这些参数表示传递给方法的值或变量引用；方法还有一个返回类型，它指定方法计算并返回的值的类型。如果方法不返回值，则其返回类型为 void。

与类型一样，方法也可以有一组类型参数；调用方法时，必须为这些类型参数指定类型实参。与类型不同，类型实参通常可以从方法调用的实参中推断出来，而不必显式给出。

方法的签名在其声明所在的类中必须唯一。方法的签名由方法名称、类型参数数目，以及参数数目、修饰符和类型组成。方法的签名不包括返回类型。

> **埃里克·利珀特**  
> 泛型类型的一个不幸后果是，构造类型可能有两个签名完全相同的方法。例如，class C<T> { void M(T t){} void M(int t){} ...} 完全合法，但 C<int> 有两个签名完全相同的 M 方法。正如我们稍后将看到的，这种可能性会导致一些涉及重载决策和显式接口实现的有趣场景。一条好的指导原则是：不要创建会以这种方式在构造时产生歧义的泛型类型；这样的类型极其令人困惑，并可能产生意外行为。

##### 1.6.6.1 参数

参数用于将值或变量引用传递给方法。方法的参数从调用方法时指定的实参获取实际值。参数有四种：值参数、引用参数、输出参数和参数数组。

值参数用于输入参数传递。值参数对应于一个局部变量，该局部变量从为该参数传递的实参获取初始值。对值参数的修改不会影响为该参数传递的实参。

> **比尔·瓦格纳**  
> “对值参数的修改不会影响实参”这一说法可能会造成误解，因为变更器方法可能会更改引用类型参数的内容。值参数本身不会改变，但所引用对象的内容会改变。

值参数可以是可选的，方法是指定默认值，以便可以省略相应的实参。

引用参数用于输入和输出参数传递。为引用参数传递的实参必须是变量，并且在方法执行期间，引用参数表示与实参变量相同的存储位置。引用参数用 ref 修饰符声明。下面的示例展示了 ref 参数的用法。

```csharp
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
        Console.WriteLine("{0} {1}", i, j); // Outputs "2 1"
    }
}
```




> **埃里克·利珀特** 这种语法应有助于消除两个都称为“按引用传递”的事物之间的混淆。在 C# 中，引用类型之所以被称为这个名字，是因为它们是“按引用传递”的；你将一个对象实例传递给方法，方法获得对该对象实例的引用。其他一些代码也可能持有对同一对象的引用。

> 引用参数是“按引用传递”的一种略有不同的形式。在这种情况下，引用指向变量本身，而不是某个对象实例。如果该变量恰好包含值类型（如前面的示例所示），那完全合法。按引用传递的不是值，而是保存该值的变量。

> 理解引用参数的一个好方法是：引用参数成为作为实参传递的变量的别名。在前面的示例中，x 和 z 本质上是同一个变量。它们指向同一个存储位置。

*输出参数*用于输出参数传递。输出参数与引用参数类似，不同之处在于调用方提供的实参的初始值无关紧要。输出参数使用 out 修饰符声明。下面的示例展示了 out 参数的用法。

```
using System;
class Test
{
    static void Divide(int x, int y, out int result, out int remainder) {
        result = x / y;
        remainder = x % y;
    }
    static void Main() {
        int res, rem;
        Divide(10, 3, out res, out rem);
        Console.WriteLine("{0} {1}", res, rem);    // Outputs "3 1"
    }
}
```

> **埃里克·利珀特** CLR 直接只支持 ref 参数。out 参数在元数据中表示为带有特殊特性的 ref 参数，该特性向 C# 编译器表明此 ref 参数应被视为 out 参数。这解释了为什么不能有两个仅在“out/ref 性”上不同的方法；从 CLR 的角度来看，它们将是两个完全相同的方法。

*参数数组*允许将可变数量的实参传递给方法。参数数组使用 `params` 修饰符声明。只有方法的最后一个参数可以是参数数组，并且参数数组的类型必须是一维数组类型。`System.Console` 类的 `Write` 和 `WriteLine` 方法是参数数组用法的良好示例。它们的声明如下。

```csharp
public class Console
{
    public static void Write(string fmt, params object[] args) {...}
    public static void WriteLine(string fmt, params object[] args) {...}
    ...
}
```

在使用参数数组的方法内部，参数数组的行为完全像数组类型的常规参数。然而，在调用带有参数数组的方法时，既可以传递参数数组类型的单个实参，也可以传递任意数量的参数数组元素类型的实参。在后一种情况下，会自动创建一个数组实例，并用给定的实参初始化它。这个示例

```csharp
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```

等价于编写以下代码。

```csharp
string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
```

> > **布拉德·艾布拉姆斯** 你可能会注意到 `params` 与 C 编程语言中的 `varargs` 概念之间的相似性。为了保持让 C# 非常易于理解的目标，`params` 修饰符不需要特殊的调用约定或特殊的库支持。因此，事实证明它比 `varargs` 更不容易出错。
> >
> > 但请注意，C# 模型确实会在每次调用时隐式地创建一个额外的对象分配（即包含参数的数组）。这很少成为问题，但在内循环类型的场景中，它可能会变得低效，我们建议为主流情况提供重载，并仅对边缘情况使用 `params` 重载。一个例子是 `StringBuilder.AppendFormat()` 系列重载：

```csharp
public static StringBuilder AppendFormat(string format, object arg0);
public static StringBuilder AppendFormat(string format, object arg0, object arg1);
public static StringBuilder AppendFormat(string format, object arg0, object arg1, object arg2);
public static StringBuilder AppendFormat(string format, params object[] args);
```

**克里斯·塞尔斯** params 实际上只是一个可选快捷方式，这一事实的一个良好副作用是，我不必编写像下面这样疯狂的东西：

```csharp
static object[] GetArgs() { ... }

static void Main() {
    object[] args = GetArgs();
    object x = args[0];
    object y = args[1];
    object z = args[2];
    Console.WriteLine("x={0} y={1} z={2}", x, y, z);
}
```

在这里，我调用方法并把参数拆出来，只是为了编译器能再次在它们周围创建一个数组。当然，我其实应该只这样写：

```csharp
static object[] GetArgs() { ... }

static void Main() {
    Console.WriteLine("x={0} y={1} z={2}", GetArgs());
}
```

然而，如今在 .NET 中，返回数组的方法越来越少，因为大多数人更喜欢使用 IEnumerable<T> 的灵活性。这意味着你可能要编写如下代码：

```csharp
static IEnumerable<object> GetArgs() { ... }

static void Main() {
    Console.WriteLine("x={0} y={1} z={2}", GetArgs().ToArray());
}
```

如果 params 能直接“理解” IEnumerable，那会很方便。也许下次吧。

##### 1.6.6.2 方法体和局部变量

方法体指定调用方法时要执行的语句。

方法体可以声明特定于该方法调用的变量。此类变量称为局部变量。局部变量声明指定类型名、变量名，并可能指定初始值。下面的示例声明一个初始值为零的局部变量 i 和一个没有初始值的局部变量 j。

![](img/04b421b044b1254de966ab5335775a89_50_0.png)

```csharp
using System;
class Squares
{
    static void Main() {
        int i = 0;
        int j;
        while (i < 10) {
            j = i * i;
            Console.WriteLine("{0} x {0} = {1}", i, j);
            i = i + 1;
        }
    }
}
```

C# 要求局部变量在获取其值之前必须被*明确赋值*。例如，如果前面 `i` 的声明没有包含初始值，编译器会对后续使用 `i` 的地方报告错误，因为在程序中的那些位置它没有被明确赋值。

方法可以使用 return 语句将控制权返回给调用方。在返回 `void` 的方法中，return 语句不能指定表达式。在返回非 void 的方法中，return 语句必须包含计算返回值的表达式。

##### 1.6.6.3 静态方法和实例方法

使用 static 修饰符声明的方法是*静态方法*。静态方法不作用于特定实例，并且只能直接访问静态成员。

> > **埃里克·利珀特** 当然，如果静态方法碰巧手边有一个实例，那么它访问实例成员是完全合法的。

不使用 static 修饰符声明的方法是*实例方法*。实例方法作用于特定实例，并且可以访问静态成员和实例成员。调用实例方法时所针对的实例可以通过 `this` 显式访问。在静态方法中引用 `this` 是错误的。

下面的 Entity 类同时具有静态成员和实例成员。

```csharp
class Entity
{
    static int nextSerialNo;
    int serialNo;
    public Entity()
    {
    serialNo = nextSerialNo++;
    }
    public int GetSerialNo()
    {
        return serialNo;
    }
    public static int GetNextSerialNo()
    {
        return nextSerialNo;
    }
    public static void SetNextSerialNo(int value)
    {
        nextSerialNo = value;
    }
}
```

每个 Entity 实例都包含一个序列号（并且大概还包含此处未显示的其他一些信息）。Entity 构造函数（类似于实例方法）用下一个可用的序列号初始化新实例。由于构造函数是实例成员，因此允许它访问 serialNo 实例字段和 nextSerialNo 静态字段。

GetNextSerialNo 和 SetNextSerialNo 静态方法可以访问 nextSerialNo 静态字段，但它们直接访问 serialNo 实例字段会出错。

下面的示例展示了 Entity 类的用法。

```csharp
using System;
class Test
{
    static void Main() {
        Entity.SetNextSerialNo(1000);

        Entity e1 = new Entity();
        Entity e2 = new Entity();

        Console.WriteLine(e1.GetSerialNo());          // Outputs "1000"
        Console.WriteLine(e2.GetSerialNo());          // Outputs "1001"
        Console.WriteLine(Entity.GetNextSerialNo());  // Outputs "1002"
    }
}
```

请注意，SetNextSerialNo 和 GetNextSerialNo 静态方法是在类上调用的，而 GetSerialNo 实例方法是在类的实例上调用的。




## 1. 引言

### 1.6.6.4 虚拟、重写和抽象方法

当实例方法声明包含 virtual 修饰符时，该方法被称为虚拟方法。当没有 virtual 修饰符时，该方法被称为非虚拟方法。

当调用虚拟方法时，执行该调用的实例的运行时类型决定了实际要调用的方法实现。在非虚拟方法调用中，实例的编译时类型是决定因素。

虚拟方法可以在派生类中被重写。当实例方法声明包含 override 修饰符时，该方法会重写具有相同签名的继承的虚拟方法。虚拟方法声明引入了一个新方法，而 override 方法声明则通过提供该方法的新实现来特化已有的继承虚拟方法。

> **ERIC LIPPERT** 这里有一个细微的点，即被重写的虚拟方法仍然被视为引入它的类的一个方法，而不是重写它的类的成员。重载解析规则在某些情况下更倾向于更派生类型中的成员而不是基类型中的成员；重写方法并不会“移动”该方法在此层次结构中的归属位置。
>
> 在本节的开头，我们提到 C# 是在考虑版本控制的前提下设计的。这就是那些有助于防止“脆弱基类综合征”导致版本问题的特性之一。

抽象方法是一种没有实现体的虚拟方法。抽象方法使用 abstract 修饰符声明，并且仅允许在也声明为 abstract 的类中出现。抽象方法必须在每个非抽象派生类中被重写。

下面的示例声明了一个抽象类 Expression，它表示表达式树节点，以及三个派生类 Constant、VariableReference 和 Operation，它们实现了用于常量、变量引用和算术运算的表达式树节点。（这与 §4.6 中引入的表达式树类型类似，但不应混淆。）

```csharp
using System;
using System.Collections;

public abstract class Expression
{
    public abstract double Evaluate(Hashtable vars);
}

public class Constant: Expression
{
    double value;

    public Constant(double value) {
        this.value = value;
    }

    public override double Evaluate(Hashtable vars) {
        return value;
    }
}

public class VariableReference: Expression
{
    string name;

    public VariableReference(string name) {
        this.name = name;
    }

    public override double Evaluate(Hashtable vars) {
        object value = vars[name];
        if (value == null) {
            throw new Exception("Unknown variable: " + name);
        }
        return Convert.ToDouble(value);
    }
}

public class Operation: Expression
{
    Expression left;
    char op;
    Expression right;

    public Operation(Expression left, char op, Expression right) {
        this.left = left;
        this.op = op;
        this.right = right;
    }

    public override double Evaluate(Hashtable vars) {
        double x = left.Evaluate(vars);
        double y = right.Evaluate(vars);
        switch (op) {
            case '+': return x + y;
            case '-': return x - y;
            case '*': return x * y;
            case '/': return x / y;
        }
        throw new Exception("Unknown operator");
    }
}
```

前面四个类可用于建模算术表达式。例如，使用这些类的实例，表达式 x + 3 可以表示如下。

```csharp
Expression e = new Operation(
    new VariableReference("x"),
    '+',
    new Constant(3));
```

Expression 实例的 Evaluate 方法被调用以计算给定的表达式并生成一个 double 值。该方法接受一个 Hashtable 作为参数，其中包含变量名（作为条目的键）和值（作为条目的值）。Evaluate 方法是一个虚拟抽象方法，这意味着非抽象派生类必须重写它以提供实际实现。

Constant 对 Evaluate 的实现只是返回存储的常量。VariableReference 的实现在哈希表中查找变量名并返回结果值。Operation 的实现首先计算左右操作数（通过递归调用它们的 Evaluate 方法），然后执行给定的算术运算。

下面的程序使用 Expression 类对表达式 x * (y + 2) 在 x 和 y 的不同取值下进行求值。

```csharp
using System;
using System.Collections;

class Test
{
    static void Main() {
        Expression e = new Operation(
            new VariableReference("x"),
            '*',
            new Operation(
                new VariableReference("y"),
                '+',
                new Constant(2)
            )
        );

        Hashtable vars = new Hashtable();

        vars["x"] = 3;
        vars["y"] = 5;
        Console.WriteLine(e.Evaluate(vars));    // Outputs "21"

        vars["x"] = 1.5;
        vars["y"] = 9;
        Console.WriteLine(e.Evaluate(vars));    // Outputs "16.5"
    }
}
```

> **CHRIS SELLS** 虚拟函数是面向对象编程的一项主要特性，它使其区别于其他类型的编程。例如，如果你发现自己在做类似这样的事情：
>
> ```csharp
> double GetHourlyRate(Person p) {
>     if( p is Student ) { return 1.0; }
>     else if( p is Employee ) { return 10.0; }
>     return 0.0;
> }
> ```
>
> 你几乎总是应该改用虚拟方法 instead：
>
> ```csharp
> class Person {
>     public virtual double GetHourlyRate() {
>         return 0.0;
>     }
> }
> class Student {
>     public override double GetHourlyRate() {
>         return 1.0;
>     }
> }
> class Employee {
>     public override double GetHourlyRate() {
>         return 10.0;
>     }
> }
> ```

### 1.6.6.5 方法重载

方法重载允许同一个类中的多个方法具有相同的名称，只要它们的签名唯一即可。在编译重载方法的调用时，编译器使用重载解析来确定要调用的具体方法。重载解析会找到与参数最匹配的方法，或者如果找不到唯一最佳匹配则报告错误。下面的示例展示了重载解析的实际效果。Main 方法中每个调用的注释显示了实际被调用的方法。

```csharp
class Test
{
    static void F() {
        Console.WriteLine("F()");
    }
    static void F(object x) {
        Console.WriteLine("F(object)");
    }
    static void F(int x) {
        Console.WriteLine("F(int)");
    }
    static void F(double x) {
        Console.WriteLine("F(double)");
    }
    static void F<T>(T x) {
        Console.WriteLine("F<T>(T)");
    }
    static void F(double x, double y) {
        Console.WriteLine("F(double, double)");
    }
    static void Main() {
        F();                // Invokes F()
        F(1);               // Invokes F(int)
        F(1.0);             // Invokes F(double)
        F("abc");           // Invokes F(object)
        F(1d);              // Invokes F(double)
        F(object1);         // Invokes F(object)
        F<int>(1);          // Invokes F<T>(T)
        F(1, 1);            // Invokes F(double, double)
    }
}
```

如示例所示，通过显式地将参数强制转换为确切的参数类型和/或显式提供类型参数，始终可以选中特定方法。

> **BRAD ABRAMS** 方法重载特性可能会被滥用。一般来说，最好仅在所有方法在语义上做相同的事情时才使用方法重载。许多消费端开发者认为方法重载的方式是单个方法接受各种参数。事实上，更改局部变量、参数或属性的类型可能会导致调用不同的重载。开发者绝对不应看到使用重载决定的副作用。然而，对于用户来说，当同名方法做不同的事情时可能会感到惊讶。例如，在 .NET Framework 工作早期（在版本 1 发布之前），我们在 string 类上曾有这组重载：
>
> ```csharp
> public class String {
>     public int IndexOf (string value);
>     // Returns the index of value with this instance
>     public int IndexOf (char value);
>     // Returns the index of value with this instance
>     public int IndexOf (char [] value);
>     // Returns the first index of any of the
>     // characters in value within the current instance
> }
> ```

最后一个重载引发了问题，因为它做的事情不同。例如，

```
"Joshua, Hannah, Joseph".IndexOf("Hannah");// Returns 7
```

但

```
"Joshua, Hannah, Joseph".IndexOf(new char [] {'H','a','n','n','a','h'});
// Returns 3
```

在这种情况下，最好给做不同事情的重载起一个不同的名称：

```
public class String {
    public int IndexOf (string value);
    // Returns the index of value within this instance
    public int IndexOf (char value);
    // Returns the index of value within this instance
    public int IndexOfAny(char [] value);
    // Returns the first index of any of the
    // characters in value within the current instance
}
```

> > **比尔·瓦格纳** 方法重载和继承不能很好地结合。因为重载解析规则有时偏向于在派生程度最高的类中声明的方法，这有时意味着派生类中声明的方法可能会被选中，而不是基类中看起来更匹配的方法。因此，我建议不要重载基类中声明的成员。

### 1.6.7 其他函数成员

包含可执行代码的成员统称为类的函数成员。上一节介绍了方法，它是函数成员的主要类型。本节介绍 C# 支持的其他类型的函数成员：构造函数、属性、索引器、事件、运算符和析构函数。

下表展示了一个名为 List<T> 的泛型类，它实现可增长的对象列表。该类包含几种最常见的函数成员类型的示例。

| 代码 | 类别 |
|---|---|
| public class List<T> { |  |
| const int defaultCapacity = 4; | 常量 |
| T[] items;<br>int count; | 字段 |
| public List(int capacity = defaultCapacity) {<br>    items = new T[capacity];<br>} | 构造函数 |
| public int Count {<br>    get { return count; }<br>}<br>public int Capacity {<br>    get {<br>        return items.Length;<br>    }<br>    set {<br>        if (value < count) value = count;<br>        if (value != items.Length) {<br>            T[] newItems = new T[value];<br>            Array.Copy(items, 0, newItems, 0, count);<br>            items = newItems;<br>        }<br>    }<br>} | 属性 |
| public T this[int index] {<br>    get {<br>        return items[index];<br>    }<br>    set {<br>        items[index] = value;<br>        OnChanged();<br>    }<br>} | 索引器 |
| public void Add(T item) { if (count == Capacity) Capacity = count * 2; items[count] = item; count++; OnChanged(); } protected virtual void OnChanged() { if (Changed != null) Changed(this, EventArgs.Empty); } public override bool Equals(object other) { return Equals(this, other as List<T>); } static bool Equals(List<T> a, List<T> b) { if (a == null) return b == null; if (b == null || a.count != b.count) return false; for (int i = 0; i < a.count; i++) { if (!object.Equals(a.items[i], b.items[i])) { return false; } } return true; } | 方法 |
| public event EventHandler Changed; | 事件 |
| public static bool operator ==(List<T> a, List<T> b) { return Equals(a, b); } public static bool operator !=(List<T> a, List<T> b) { return !Equals(a, b); } | 运算符 |
| } |  |

### 1.6.7.1 构造函数

C# 同时支持实例构造函数和静态构造函数。实例构造函数是实现初始化类实例所需操作的成员。静态构造函数是实现首次加载时初始化类本身所需操作的成员。

构造函数的声明方式类似于没有返回值且与包含类同名的方法。如果构造函数声明包含 static 修饰符，则声明静态构造函数。否则，声明实例构造函数。

实例构造函数可以重载。例如，`List<T>` 类声明了两个实例构造函数，一个没有参数，另一个接受 int 参数。实例构造函数使用 new 运算符调用。以下语句使用 List 类的每个构造函数分别分配两个 `List<string>` 实例。

```csharp
List<string> list1 = new List<string>();
List<string> list2 = new List<string>(10);
```

与其他成员不同，实例构造函数不会被继承，并且类除了实际在该类中声明的实例构造函数之外没有其他实例构造函数。如果没有为类提供实例构造函数，则会自动提供一个没有参数的空实例构造函数。

> > **布拉德·艾布拉姆斯** 构造函数应该“懒惰”！最佳实践是在构造函数中做最少的工作——也就是说，只捕获参数以供后续使用。例如，你可能捕获文件名或数据库路径，但除非绝对必要，否则不要打开这些外部资源。这种做法有助于确保可能稀缺的资源只在尽可能短的时间内被分配。
> >
> > 我个人最近就被 Linq to Entities 中的 `DataContext` 类这个问题坑过。它会在提供的连接字符串中打开数据库，而不是等到需要时才执行该操作。对于我的测试用例，我直接提供测试可疑数据，事实上从不想打开数据库。这种不必要的活动不仅会导致性能损失，还会使场景更加复杂。

### 1.6.7.2 属性

*属性* 是字段的自然扩展。二者都是具有关联类型的命名成员，并且访问字段和属性的语法相同。然而，与字段不同，属性不表示存储位置。相反，属性具有 *访问器*，用于指定读取或写入其值时要执行的语句。

> > **杰西·利伯蒂** 对于类的创建者来说，属性看起来像一个方法，允许开发人员在设置或检索基础值之前添加行为。相比之下，对于类的客户端来说，属性看起来就像字段，通过赋值运算符提供直接、不受阻碍的访问。

**埃里克·利珀特** 一个标准的“最佳实践”是始终将类似字段的数据作为带 getter 和 setter 的属性公开，而不是公开字段。这样一来，如果你以后想为 getter 和 setter 添加功能（例如日志记录、数据绑定、安全检查），就可以轻松做到，而不会“破坏”任何可能依赖该字段始终存在的代码使用方。

尽管从某种意义上说，这种做法违反了另一条良好建议（“避免过早泛化”），但新的“自动实现的属性”功能使得使用属性而不是字段作为类型的公共接口的一部分变得非常容易且自然。

**克里斯·塞尔斯** 埃里克提出了一个很好的观点，我想展示一个示例。

永远不要将字段设为 public：

```
class Cow
{
    public int Milk; // BAD!
}
```

如果你不想在存储之外再添加任何东西，就让编译器为你实现属性：

```
class Cow
{
    public int Milk { get; set; } // Good
}
```

这样，客户端会绑定到属性的 getter 和 setter，以便以后你可以接管编译器的实现来做一些更复杂的事情：

```
class Cow {
    bool gotMilk = false;
    int milk;
    public int Milk {
        get {
            if( !gotMilk ) {
                milk = ApplyMilkingMachine();
            }
            gotMilk = true;
            return milk;
        }
        set {
            ApplyReverseMilkingMachine(value); // The cow might not like this..
            milk = value;
        }
    }
}
```

另外，对于你知道某个计算值将在程序中使用的情况，我非常喜欢下面这种写法：

```csharp
class Cow {
  public Cow() {
    Milk = ApplyMilkingMachine();
  }

  public int Milk { get; private set; }
  ...
}
```

在这种情况下，我们是在预先计算属性；如果我们不知道是否需要它，这就是一种浪费。如果我们确实知道，就可以通过消除一个标志、一些分支逻辑和存储管理，避免代码中的一些复杂性。

> > **比尔·瓦格纳** 对用户来说，属性访问看起来就像字段访问——他们自然会期望属性访问在各方面都像字段访问一样，包括性能。如果 get 访问器需要执行大量工作（例如读取文件或查询数据库），则应将其公开为方法，而不是属性。调用方会预期方法可能执行更多工作。
> >
> > 出于同样的原因，重复调用属性访问器（中间没有其他代码）应返回相同的值。DateTime.Now 是框架中极少数不遵循此建议的示例之一。

属性的声明类似于字段，不同之处在于声明以写在分隔符 { 和 } 之间的 get 访问器和/或 set 访问器结尾，而不是以分号结尾。同时具有 get 访问器和 set 访问器的属性是 *读写属性*，只有 get 访问器的属性是 *只读属性*，只有 set 访问器的属性是 *只写属性*。

get 访问器对应于一个无参数、返回值为属性类型的方法。除了作为赋值目标的情况外，当在表达式中引用属性时，会调用该属性的 get 访问器来计算属性的值。




设置访问器对应于一个具有名为 value 的单一参数且没有返回类型的方法。当属性作为赋值的目标或作为 ++ 或 -- 的操作数被引用时，将使用提供新值的参数调用设置访问器。

List<T> 类声明了两个属性，Count 和 Capacity，它们分别是只读和读写的。以下是使用这些属性的示例。

```csharp
List<string> names = new List<string>();
names.Capacity = 100;            // Invokes set accessor
int i = names.Count;             // Invokes get accessor
int j = names.Capacity;          // Invokes get accessor
```

与字段和方法类似，C# 支持实例属性和静态属性。静态属性使用 static 修饰符声明，而实例属性声明时不使用它。

属性的访问器可以是虚拟的。当属性声明包含 virtual、abstract 或 override 修饰符时，它应用于该属性的访问器。

> **VLADIMIR RESHETNIKOV** 如果虚拟属性碰巧有一个私有访问器，则该访问器在 CLR 中实现为非虚拟方法，并且不能在派生类中重写。

### 1.6.7.3 索引器

索引器是一种成员，它使对象能够像数组一样被索引。索引器的声明类似于属性，不同之处在于成员名称是 this，后跟一个写在分隔符 [ 和 ] 之间的参数列表。这些参数可在索引器的访问器中使用。与属性类似，索引器可以是读写、只读和只写的，并且索引器的访问器可以是虚拟的。

List<T> 类声明了一个接受 int 参数的读写索引器。该索引器使得可以使用 int 值来索引 List<T> 实例。例如：

```csharp
List<string> names = new List<string>();
names.Add("Liz");
names.Add("Martha");
names.Add("Beth");
for (int i = 0; i < names.Count; i++) {
    string s = names[i];
    names[i] = s.ToUpper();
}
```

索引器可以重载，这意味着只要参数的数量或类型不同，一个类就可以声明多个索引器。

### 1.6.7.4 事件

*事件*是一种成员，它使类或对象能够提供通知。事件的声明类似于字段，不同之处在于声明包含 event 关键字，并且类型必须是委托类型。

> **JESSE LIBERTY** 实际上，event 只是一个关键字，它指示 C# 限制委托的使用方式，从而防止客户端直接调用事件，或通过分配处理程序而不是添加处理程序来劫持事件。简而言之，event 关键字使委托的行为符合你对事件行为的预期。

> **CHRIS SELLS** 如果没有 event 关键字，你可以这样做：

```
delegate void WorkCompleted();

class Worker {
  public WorkCompleted Completed;  // Delegate field, not event
  ...
}

class Boss {
  public void WorkCompleted() { ... }
}

class Program {
  static void Main() {
    Worker peter = new Worker();
    Boss boss = new Boss();

    peter.Completed += boss.WorkCompleted;  // This is what you want to happen
    peter.Completed = boss.WorkCompleted;  // This is what the compiler allows
    ...
  }
}
```

不幸的是，使用 event 关键字时，Completed 只是一个委托类型的公共字段，任何想这样做的人都可以践踏它——而编译器对此没有问题。通过添加 event 关键字，你将操作限制为 += 和 -=，如下所示：

```
class Worker {
    public event WorkCompleted Completed;
    ...
}
...
peter.Completed += boss.WorkCompleted;  // Compiler still okay
peter.Completed -= boss.WorkCompleted;  // Compiler error
```

使用 event 关键字是唯一可以公开字段的场合，因为编译器将使用范围缩小到安全操作。此外，如果你想接管事件的 += 和 -= 的实现，也可以这样做。

在声明事件成员的类中，可以像访问委托类型的字段一样访问该事件（前提是该事件不是抽象的，并且未声明访问器）。该字段存储一个委托引用，该委托表示已添加到事件的事件处理程序。如果不存在事件处理程序，则该字段为 null。

List<T> 类声明了一个名为 Changed 的事件成员，它指示已向列表添加了新项。Changed 事件由 OnChanged 虚拟方法引发，该方法首先检查事件是否为 null（意味着不存在处理程序）。引发事件的概念完全等同于调用该事件所表示的委托——因此，没有用于引发事件的特殊语言构造。

客户端通过事件处理程序对事件作出反应。事件处理程序使用 += 运算符附加，并使用 -= 运算符移除。以下示例将事件处理程序附加到 List<string> 的 Changed 事件。

```
using System;

class Test
{
    static int changeCount;
    static void ListChanged(object sender, EventArgs e) {
        changeCount++;
    }
}
```

```csharp
static void Main() {
    List<string> names = new List<string>();
    names.Changed += new EventHandler(ListChanged);
    names.Add("Liz");
    names.Add("Martha");
    names.Add("Beth");
    Console.WriteLine(changeCount);        // Outputs "3"
}
```

对于希望控制事件底层存储的高级场景，事件声明可以显式提供 add 和 remove 访问器，它们与属性的设置访问器有些类似。

> **CHRIS SELLS** 从 C# 2.0 开始，不再需要显式创建委托实例来包装方法。因此，代码

```csharp
names.Changed += new EventHandler(ListChanged);
```

可以更简洁地写成

```csharp
names.Changed += ListChanged;
```

这种缩短形式不仅需要更少的输入，而且更易于阅读。

### 1.6.7.5 运算符

*运算符*是一种成员，它定义将特定表达式运算符应用于类实例的含义。可以定义三种运算符：一元运算符、二元运算符和转换运算符。所有运算符都必须声明为 public 和 static。

List<T> 类声明了两个运算符，operator == 和 operator !=，从而为将这些运算符应用于 List 实例的表达式赋予了新含义。具体而言，这些运算符将两个 List<T> 实例的相等性定义为使用每个所含对象的 Equals 方法进行比较。以下示例使用 == 运算符比较两个 List<int> 实例。

```csharp
using System;

class Test
{
    static void Main() {
        List<int> a = new List<int>();
        a.Add(1);
        a.Add(2);
        List<int> b = new List<int>();
        b.Add(1);
        b.Add(2);
        Console.WriteLine(a == b);      // Outputs "True"
        b.Add(3);
        Console.WriteLine(a == b);      // Outputs "False"
    }
}
```

第一个 Console.WriteLine 输出 True，因为两个列表包含相同数量的对象，且这些对象的值相同、顺序相同。如果 List<T> 未定义 operator ==，则第一个 Console.WriteLine 将输出 False，因为 a 和 b 引用不同的 List<int> 实例。

### 1.6.7.6 析构函数

*析构函数*是一种成员，它实现销毁类实例所需执行的操作。析构函数不能有参数，不能有可访问性修饰符，也不能被显式调用。实例的析构函数在垃圾回收期间自动调用。

垃圾回收器在决定何时回收对象和运行析构函数方面拥有很大的自由度。具体而言，析构函数调用的时机不是确定性的，并且析构函数可能在任何线程上执行。由于这些原因及其他原因，类应仅在没有其他可行解决方案时才实现析构函数。

> **VLADIMIR RESHETNIKOV** 析构函数有时被称为“终结器”。这个名称也出现在垃圾回收器 API 中——例如，GC.WaitForPendingFinalizers。

using 语句提供了一种更好的对象销毁方法。

## 1.7 结构

与类一样，*结构*是可以包含数据成员和函数成员的数据结构，但与类不同，结构是值类型，不需要堆分配。结构类型的变量直接存储结构的数据，而类类型的变量存储对动态分配对象的引用。结构类型不支持用户指定的继承，并且所有结构类型都隐式继承自 object 类型。




## 1. 引言

> **埃里克·利珀特** 结构体并不*要求*堆分配，这*并不*意味着它们*从不*进行堆分配。更多细节请参见 §1.3 的注释。

结构体对于具有值语义的小型数据结构特别有用。复数、坐标系中的点，或字典中的键值对，都是结构体的良好示例。对于小型数据结构，使用结构体而不是类，会显著影响应用程序执行的内存分配次数。例如，下面的程序创建并初始化一个包含 100 个点的数组。如果将 Point 实现为类，则会实例化 101 个独立对象——一个用于数组，另外 100 个各用于一个元素。

```csharp
class Point
{
    public int x, y;
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class Test
{
    static void Main()
    {
        Point[] points = new Point[100];
        for (int i = 0; i < 100; i++) points[i] = new Point(i, i);
    }
}
```

另一种做法是将 Point 设为结构体。

```csharp
struct Point
{
    public int x, y;
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}
```

现在只实例化一个对象——即用于数组的那个对象——而 Point 实例直接存储在数组中。

> **埃里克·利珀特** 这里的要点是：某些特定的数据密集型应用程序本来会受堆分配性能制约，而使用结构体能从中大为受益。这里要强调的要点*绝不是*“始终使用结构体，因为它们会让程序更快。”
> 
> 这里的性能优势是一种权衡：在某些场景下，结构体的分配和释放耗时可能更少，但由于每次结构体赋值都是值复制，因此复制结构体可能比复制引用耗时更多。
> 
> 始终记住：优化最慢部分之外的任何东西都没有太大意义。如果你的程序不受堆分配制约，那么为了性能而纠结该用结构体还是类，并不是有效利用时间。找出最慢的部分，然后优化它。

结构体构造函数通过 `new` 运算符调用，但这并不意味着正在分配内存。结构体构造函数不是动态分配一个对象并返回对它的引用，而是直接返回结构体值本身（通常位于栈上的临时位置），然后根据需要复制该值。

对于类，两个变量可以引用同一个对象，因此对一个变量执行的操作可能影响另一个变量所引用的对象。对于结构体，每个变量都有自己的数据副本，对一个变量执行的操作不可能影响另一个变量。例如，下面的代码片段产生的输出取决于 `Point` 是类还是结构体。

```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 20;
Console.WriteLine(b.x);
```

如果 Point 是类，则输出为 20，因为 a 和 b 引用同一个对象。如果 Point 是结构体，则输出为 10，因为将 a 赋值给 b 会创建值的副本，而这个副本不受随后对 a.x 赋值的影响。

前面的示例突出了结构体的两个限制。首先，复制整个结构体通常比复制对象引用效率更低，因此对于结构体，赋值和按值传递参数可能比引用类型开销更大。其次，除了 `ref` 和 `out` 参数外，不可能创建对结构体的引用，这排除了它们在许多情况下的使用。

> **比尔·瓦格纳** 再读一遍最后两段。它们描述了结构体与类之间最重要的设计差异。如果你并不想在所有情况下都使用值语义，就必须使用类。类可以在某些情况下实现值语义（*string* 就是一个很好的例子），但默认情况下它们遵循引用语义。对于你的设计而言，这种差异比大小或栈分配与堆分配之间的差异更重要。

### 1.8 数组

*数组*是一种数据结构，包含若干通过计算得到的索引来访问的变量。数组中包含的变量也称为数组的*元素*，它们都属于同一类型，这种类型称为数组的*元素类型*。

数组类型是引用类型，声明数组变量只是预留空间来存放对数组实例的引用。实际的数组实例在运行时使用 *new* 运算符动态创建。*new* 操作指定新数组实例的*长度*，该长度在实例的生存期内固定不变。数组元素的索引范围为 0 到 *Length* - 1。*new* 运算符会自动将数组元素初始化为其默认值；例如，所有数值类型的默认值为零，所有引用类型的默认值为 *null*。

> **埃里克·利珀特** 有些语言从 1 开始索引数组，另一些语言从 0 开始，由此造成的困惑曾让一代又一代新手程序员晕头转向。数组“索引”从 0 开始这一观念，源于对 C 语言数组语法的一种微妙误解。
> 
> 在 C 中，当写出 *myArray[x]* 时，其含义是“从数组开头开始，引用相隔 x 步的那个东西”。因此，*myArray[1]* 指的是第二个元素，因为从第一个元素开始并*移动*一步得到的就是它。
> 
> 实际上，这些引用应该称为数组*偏移量*，而不是*索引*。但由于一代代程序员现在已经内化了数组从 0 开始“索引”的观念，我们只能沿用这个术语。

下面的示例创建一个 int 元素数组，初始化该数组，并打印数组的内容。

```csharp
using System;

class Test
{
    static void Main()
    {
        int[] a = new int[10];
        for (int i = 0; i < a.Length; i++)
        {
            a[i] = i * i;
        }
        for (int i = 0; i < a.Length; i++)
        {
            Console.WriteLine("a[{0}] = {1}", i, a[i]);
        }
    }
}
```

此示例创建并操作一个一维数组。C# 还支持多维数组。数组类型的维数，也称为数组类型的秩，等于数组类型方括号之间所写逗号的数量加一。下面的示例分配一维、二维和三维数组。

```csharp
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
```

a1 数组包含 10 个元素，a2 数组包含 50（10 × 5）个元素，a3 数组包含 100（10 × 5 × 2）个元素。

> **比尔·瓦格纳** 有一条 FxCop 规则建议不要使用多维数组；它主要是指导不要将多维数组用作稀疏数组。如果你确定确实会填充数组中的所有元素，那么多维数组是没问题的。

数组的元素类型可以是任何类型，包括数组类型。元素类型为数组类型的数组有时称为交错数组，因为各元素数组的长度不必全部相同。下面的示例分配一个 int 数组的数组：

```csharp
int[][] a = new int[3][];
a[0] = new int[10];
a[1] = new int[5];
a[2] = new int[20];
```

第一行创建一个包含三个元素的数组，每个元素的类型都是 int[]，且初始值均为 null。随后的几行分别用对不同长度数组实例的引用初始化这三个元素。

*new* 运算符允许使用*数组初始值设定项*指定数组元素的初始值，该初始值设定项是写在分隔符 { 和 } 之间的一系列表达式。下面的示例分配并初始化一个包含三个元素的 int[]。

```csharp
int[] a = new int[] { 1, 2, 3 };
```

注意，数组的长度是根据 { 和 } 之间的表达式数量推断出来的。局部变量和字段声明可以进一步缩短，从而不必重新写出数组类型。

```csharp
int[] a = { 1, 2, 3 };
```

前面的两个示例都等效于以下内容：

```csharp
int[] t = new int[3];
t[0] = 1;
t[1] = 2;
t[2] = 3;
int[] a = t;
```

> **埃里克·利珀特** 到目前为止，规范在不少地方指出，某个特定的局部初始化等效于“将某个东西赋给临时变量，对临时变量做某些操作，声明一个局部变量，并将该临时变量赋给这个局部变量。”你可能会想，规范为什么要特意指出这种看似不必要的间接层。为什么不直接说该初始化等效于：
> 
>     int[] a = new int[3];
>     a[0] = 1; a[1] = 2; a[2] = 3;
> 
> 事实上，这种做法是必要的，因为要进行明确赋值分析。我们希望确保所有局部变量在使用之前都已明确赋值。特别地，我们希望诸如 `object[] arr = {arr};` 这样的表达式是非法的，因为它看起来在 `arr` 被明确赋值之前就使用了 `arr`。如果它等效于
> 
>     object[] arr = new object[1];
>     arr[0] = arr;
> 
> 那么它就会是合法的。但如果说这个表达式等效于
> 
>     object[] temp = new object[1];
>     temp[0] = arr;
>     object[] arr = temp;
> 
> 那么就能清楚地看出，`arr` 在被赋值之前就被使用了。




## 1.9 接口

一个 *接口* 定义了可由类和结构体实现的契约。接口可以包含方法、属性、事件和索引器。接口不提供其定义成员的实现——它仅仅指定实现该接口的类或结构体必须提供的成员。

接口可以采用 *多重继承*。在下面的示例中，接口 IComboBox 同时继承自 ITextBox 和 IListBox。

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

interface IComboBox : ITextBox, IListBox { }
```

类和结构体可以实现多个接口。在下面的示例中，类 EditBox 同时实现了 IControl 和 IDataBound。

```csharp
interface IDataBound
{
    void Bind(Binder b);
}

public class EditBox : IControl, IDataBound
{
    public void Paint() {...}
    public void Bind(Binder b) {...}
}
```

> **KRZYSZTOF CWALINA** 也许我用这句话引起了相当多的争议，但我相信我们类型系统中缺乏对多重继承的支持是 .NET Framework 复杂性的最大贡献者之一。在设计类型系统时，我们明确决定不添加对多重继承的支持以提供简洁性。回顾起来，这一决定产生了完全相反的效果。缺乏多重继承迫使我们添加了接口的概念，而接口反过来又导致了框架演进问题、更深的继承层次以及许多其他问题。

当类或结构体实现特定接口时，该类或结构体的实例可以隐式转换为该接口类型。例如：

```csharp
EditBox editBox = new EditBox();
IControl control = editBox;
IDataBound dataBound = editBox;
```

在实例在静态上已知实现特定接口的情况下，可以使用动态类型转换。例如，以下语句使用动态类型转换来获取对象的 IControl 和 IDataBound 接口实现。由于对象的实际类型是 EditBox，因此转换成功。

```csharp
object obj = new EditBox();
IControl control = (IControl)obj;
IDataBound dataBound = (IDataBound)obj;
```

在之前的 EditBox 类中，来自 IControl 接口的 Paint 方法和来自 IDataBound 接口的 Bind 方法使用公共成员实现。C# 还支持显式接口成员实现，通过它类或结构体可以避免将成员设为公共。显式接口成员实现使用完全限定的接口成员名称编写。例如，EditBox 类可以使用显式接口成员实现按如下方式实现 IControl.Paint 和 IDataBound.Bind 方法。

```csharp
public class EditBox : IControl, IDataBound
{
    void IControl.Paint() {...}
    void IDataBound.Bind(Binder b) {...}
}
```

显式接口成员只能通过接口类型访问。例如，之前 EditBox 类提供的 IControl.Paint 实现只能在先将 EditBox 引用转换为 IControl 接口类型后才能调用。

```csharp
EditBox editBox = new EditBox();
editBox.Paint();                          // Error: no such method
IControl control = editBox;
control.Paint();                          // Okay
```

> **VLADIMIR RESHETNIKOV** 实际上，显式实现的接口成员也可以通过受接口类型约束的类型参数访问。

## 1.10 枚举

枚举类型是一种具有一组命名常量的独立值类型。下面的示例声明并使用一个名为 Color 的枚举类型，具有三个常量值 Red、Green 和 Blue。

```csharp
using System;

enum Color
{
    Red,
    Green,
    Blue
}

class Test
{
    static void PrintColor(Color color) {
        switch (color) {
            case Color.Red:
                Console.WriteLine("Red");
                break;
            case Color.Green:
                Console.WriteLine("Green");
                break;
            case Color.Blue:
                Console.WriteLine("Blue");
                break;
            default:
                Console.WriteLine("Unknown color");
                break;
        }
    }

    static void Main() {
        Color c = Color.Red;
        PrintColor(c);
        PrintColor(Color.Blue);
    }
}
```

每个枚举类型都有一个对应的整型，称为该枚举类型的底层类型。未显式声明底层类型的枚举类型的底层类型为 int。枚举类型的存储格式和可能值的范围由其底层类型决定。枚举类型可以取的值的集合不受其枚举成员的限制。特别是，枚举的底层类型的任何值都可以强制转换为枚举类型，并且是该枚举类型的不同有效值。

下面的示例声明了一个名为 Alignment 的枚举类型，其底层类型为 sbyte。

```csharp
enum Alignment : sbyte
{
    Left = -1,
    Center = 0,
    Right = 1
}
```

> VLADIMIR RESHETNIKOV 虽然这种语法类似于基类型指定，但其含义不同。Alignment 的基类型不是 sbyte，而是 System.Enum，并且 Alignment 到 sbyte 没有隐式转换。

如前例所示，枚举成员声明可以包含指定成员值的常量表达式。每个枚举成员的常量值必须在枚举的底层类型的范围内。当枚举成员声明未显式指定值时，成员将被赋值为零（如果它是枚举类型中的第一个成员）或文本上前一个枚举成员的值加一。

枚举值可以使用类型转换相互转换为整型值，反之亦然。例如：

```csharp
int i = (int)Color.Blue;    // int i = 2;
Color c = (Color)2;          // Color c = Color.Blue;
```

> BILL WAGNER 零是枚举类型变量的默认值这一事实意味着你应始终确保零是任何枚举类型的有效成员。

任何枚举类型的默认值都是转换为枚举类型的整型值零。在变量自动初始化为默认值的情况下，这是赋予枚举类型变量的值。为了使枚举类型的默认值易于获取，字面量 0 可隐式转换为任何枚举类型。因此以下情况是允许的。

```csharp
Color c = 0;
```

> BRAD ABRAMS 我的高中第一门编程课是 Turbo Pascal（谢谢，Anders！）。在我从老师那里收回的第一份作业之一中，我在源代码中的数字 65 周围看到一个大红圈和潦草的注释，“不要使用魔法常量！！”。我的老师在向我灌输使用常量以提高可读性和可维护性的美德。枚举使这一决定变得超级容易。与某些编程语言不同，在 C# 中使用枚举不会带来任何运行时性能开销。虽然我在 API 评审中听过很多借口，但使用魔法常量而不是枚举根本没有正当理由！

## 1.11 委托

委托类型表示具有特定参数列表和返回类型的方法的引用。委托使方法能够作为可分配给变量并作为参数传递的实体来处理。委托类似于某些其他语言中存在的函数指针的概念，但与函数指针不同，委托是面向对象且类型安全的。

下面的示例声明并使用一个名为 Function 的委托类型。

```csharp
using System;

delegate double Function(double x);

class Multiplier
{
    double factor;

    public Multiplier(double factor) {
        this.factor = factor;
    }

    public double Multiply(double x) {
        return x * factor;
    }
}

class Test
{
    static double Square(double x) {
        return x * x;
    }

    static double[] Apply(double[] a, Function f) {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }

    static void Main() {
        double[] a = {0.0, 0.5, 1.0};
        double[] squares = Apply(a, Square);
        double[] sines = Apply(a, Math.Sin);
        Multiplier m = new Multiplier(2.0);
        double[] doubles = Apply(a, m.Multiply);
    }
}
```

Function 委托类型的实例可以引用任何接受 double 参数并返回 double 值的方法。Apply 方法将给定的 Function 应用于 double[] 的元素，返回包含结果的 double[]。在 Main 方法中，Apply 用于将三个不同函数应用于 double[]。



委托可以引用静态方法（例如前例中的 Square 或 Math.Sin）或实例方法（例如前例中的 m.Multiply）。引用实例方法的委托还引用特定的对象，并且当通过委托调用实例方法时，该对象在调用中成为 this。

委托也可以使用匿名函数创建，匿名函数是“内联方法”，即即时创建的。匿名函数可以看到周围方法的局部变量。因此上面的乘数示例可以更轻松地编写，而无需使用 Multiplier 类：

```
double[] doubles = Apply(a, (double x) => x * 2.0);
```

委托的一个有趣且有用的特性是它不知道也不关心其引用方法的类；唯一重要的是被引用方法具有与委托相同的参数和返回类型。

> BILL WAGNER  委托的此特性使它们成为提供组件之间接口的优秀工具，其耦合度尽可能低。

## 1.12 属性

类型、成员和 C# 程序中的其他实体支持控制其行为某些方面的修饰符。例如，方法的访问性使用 public、protected、internal 和 private 修饰符控制。C# 将此功能推广，使得用户定义的类型声明信息可以附加到程序实体并在运行时检索。程序通过定义和使用属性来指定此额外的声明信息。

以下示例声明了一个 HelpAttribute 属性，可以将其放置在程序实体上以提供指向其关联文档的链接。

```
using System;

public class HelpAttribute: Attribute
{
    string url;
    string topic;

    public HelpAttribute(string url) {
        this.url = url;
    }

    public string Url {
        get { return url; }
    }
}
```
```csharp
public string Topic {
    get { return topic; }
    set { topic = value; }
}
```

所有属性类都派生自 .NET Framework 提供的 System.Attribute 基类。可以通过在相关声明正前方的方括号内给出其名称以及任何参数来应用属性。如果属性的名称以 Attribute 结尾，则在引用属性时可以省略该部分名称。例如，HelpAttribute 属性可以如下使用。

```
```csharp
[Help("http://msdn.microsoft.com/.../MyClass.htm")]
public class Widget
{
    [Help("http://msdn.microsoft.com/.../MyClass.htm", Topic = "Display")]
    public void Display(string text) { }
}
```
```

此示例将 HelpAttribute 附加到 Widget 类，并将另一个 HelpAttribute 附加到该类中的 Display 方法。属性类的公共构造函数控制在将属性附加到程序实体时必须提供的信息。可以通过引用属性类的公共读写属性（例如之前对 Topic 属性的引用）来提供额外信息。

以下示例展示了如何使用反射在运行时检索给定程序实体的属性信息。

```
```csharp
using System;
using System.Reflection;
class Test
{
    static void ShowHelp(MemberInfo member) {
        HelpAttribute a = Attribute.GetCustomAttribute(member,
            typeof(HelpAttribute)) as HelpAttribute;
        if (a == null) {
            Console.WriteLine("No help for {0}", member);
        }
        else {
            Console.WriteLine("Help for {0}:", member);
            Console.WriteLine(" Url={0}, Topic={1}",
                a.Url, a.Topic);
        }
    }
    static void Main() {
        ShowHelp(typeof(Widget));
        ShowHelp(typeof(Widget).GetMethod("Display"));
    }
}
```
```

当通过反射请求特定属性时，将使用程序源中提供的信息调用属性类的构造函数，并返回 resulting 属性实例。如果通过属性提供了额外信息，则在返回属性实例之前将这些属性设置为给定值。

> **BILL WAGNER** 属性的全部潜力将在 C# 编译器的某个未来版本实现时得以实现，该版本使开发人员能够读取属性并在编译器创建 IL 之前使用它们修改代码模型。我希望能够使用属性来改变代码的行为，自 C# 首次发布以来我就想要这样做。

*本页特意留空*

# 2. 词法结构

### 2.1 程序

C# 程序由一个或多个源文件组成，正式称为编译单元 (§9.1)。源文件是有序的 Unicode 字符序列。源文件通常与文件系统中的文件一一对应，但这种对应关系不是必需的。为了最大限度地提高可移植性，建议文件系统中的文件使用 UTF-8 编码。

从概念上讲，程序的编译使用三个步骤：

- 1. 转换，将文件从特定的字符集和编码方案转换为 Unicode 字符序列。
- 2. 词法分析，将 Unicode 输入字符流翻译成标记流。
- 3. 语法分析，将标记流翻译成可执行代码。

### 2.2 语法

本规范使用两种语法来描述 C# 编程语言的语法。词法语法 (§2.2.2) 定义了 Unicode 字符如何组合形成行终止符、空白、注释、标记和预处理指令。语法语法 (§2.2.3) 定义了词法语法产生的标记如何组合形成 C# 程序。

### 2.2.1 语法记法

词法和语法语法使用语法产生式呈现。每个语法产生式定义一个非终结符以及该非终结符可能扩展为非终结符或终结符序列。 在语法产生式中，非终结符以斜体显示，终结符以等宽字体显示。

语法产生式的第一行是非终结符的名称，后跟冒号。每个后续缩进的行包含非终结符的可能扩展，表示为非终结符或终结符序列。例如，产生式

```
```
while-statement:
    while ( boolean-expression ) embedded-statement
```
```

定义 while-statement 由标记 while 组成，后跟标记“(”，后跟 boolean-expression，后跟标记“)”，后跟 embedded-statement。

当非终结符有多个可能扩展时，备选方案列在单独的行上。例如，产生式

```
```
statement-list:
    statement
    statement-list statement
```
```

定义 statement-list 要么由 statement 组成，要么由 statement-list 后跟 statement 组成。换句话说，该定义是递归的，并指定语句列表由一个或多个语句组成。

下标后缀“_opt”用于表示可选符号。产生式

```
```
block:
    { statement-list_opt }
```
```

是以下内容的简写

```
```
block:
    {   }
    { statement-list }
```
```

并定义 block 由“{”和“}”标记包围的可选 statement-list 组成。

备选方案通常列在单独的行上，尽管在备选方案很多的情况下，短语“one of”可能会先于单行给出的扩展列表。这只是逐行列出每个备选方案的简写。例如，产生式

```
```
real-type-suffix: one of
    F f D d M m
```
```

是以下内容的简写

```
```
real-type-suffix:
    F
    f
    D
    d
    M
    m
```
```

### 2.2.2 词法语法

C# 的词法语法在 §2.3、§2.4 和 §2.5 中呈现。词法语法的终结符是 Unicode 字符集的字符，词法语法指定字符如何组合形成标记 (§2.4)、空白 (§2.3.3)、注释 (§2.3.2) 和预处理指令 (§2.5)。

C# 程序中的每个源文件必须符合词法语法 (§2.3) 的 *input* 产生式。

### 2.2.3 语法规则

C# 的语法语法在后续章节和附录中呈现。语法语法的终结符是词法语法定义的标记，语法语法指定标记如何组合形成 C# 程序。

C# 程序中的每个源文件必须符合语法语法 (§9.1) 的 *compilation-unit* 产生式。

### 2.3 词法分析

*input* 产生式定义了 C# 源文件的词法结构。C# 程序中的每个源文件必须符合此词法语法产生式。

```
```
input:
    input-section_opt

input-section:
    input-section-part
    input-section input-section-part

input-section-part:
    input-elements_opt new-line
    pp-directive
```
```




```
input-elements:
    input-element
    input-elements input-element

input-element:
    whitespace
    comment
    token
```

五个基本元素构成 C# 源文件的词法结构：行终止符（§2.3.1）、空白（§2.3.3）、注释（§2.3.2）、标记（§2.4）和预处理指令（§2.5）。在这些基本元素中，只有标记在 C# 程序的句法语法（§2.2.3）中具有意义。

C# 源文件的词法处理包括将该文件归约为一个标记序列，该序列随后成为语法分析的输入。行终止符、空白和注释可用于分隔标记，预处理指令可使源文件的某些部分被跳过，但除此之外，这些词法元素对 C# 程序的语法结构没有影响。

当多个词法语法产生式匹配源文件中的某个字符序列时，词法处理总是形成尽可能长的词法元素。例如，字符序列 // 会被处理为单行注释的开头，因为该词法元素比单个 / 标记更长。

### 2.3.1 行终止符

行终止符将 C# 源文件的字符划分为行。

```
new-line:
    Carriage return character (U+000D)
    Line feed character (U+000A)
    Carriage return character (U+000D) followed by line feed character (U+000A)
    Next line character (U+0085)
    Line separator character (U+2028)
    Paragraph separator character (U+2029)
```

为了与添加文件结束标记的源代码编辑工具兼容，并使源文件能够被视为由正确终止的行组成的序列，对 C# 程序中的每个源文件按顺序应用以下转换：

- 如果源文件的最后一个字符是 Control-Z 字符（U+001A），则删除该字符。
- 如果源文件非空，且源文件的最后一个字符不是回车符（U+000D）、换行符（U+000A）、行分隔符（U+2028）或段落分隔符（U+2029），则在源文件末尾添加一个回车符（U+000D）。

### 2.3.2 注释

支持两种形式的注释：单行注释和分隔注释。单行注释以字符 // 开始，并延伸到源行的末尾。分隔注释以字符 /* 开始，并以字符 */ 结束。分隔注释可以跨越多行。

```
comment:
    single-line-comment
    delimited-comment

single-line-comment:
    // input-characters_opt

input-characters:
    input-character
    input-characters input-character

input-character:
    Any Unicode character except a new-line-character

new-line-character:
    Carriage return character (U+000D)
    Line feed character (U+000A)
    Next line character (U+0085)
    Line separator character (U+2028)
    Paragraph separator character (U+2029)

delimited-comment:
    /* delimited-comment-text_opt asterisks /

delimited-comment-text:
    delimited-comment-section
    delimited-comment-text delimited-comment-section

delimited-comment-section:
    /
    asterisks_opt not-slash-or-asterisk

asterisks:
    *
    asterisks *

not-slash-or-asterisk:
    Any Unicode character except / or *
```

注释不嵌套。字符序列 /* 和 */ 在 // 注释中没有特殊含义，字符序列 // 和 /* 在分隔注释中也没有特殊含义。

字符字面量和字符串字面量中的注释不会被处理。

示例

```
/* Hello, world program
    This program writes "hello, world" to the console
*/
class Hello
{
    static void Main() {
        System.Console.WriteLine("hello, world");
    }
}
```

包含一个分隔注释。

示例

```
// Hello, world program
// This program writes "hello, world" to the console
//
class Hello // any name will do for this class
{
    static void Main() { // this method must be named "Main"
        System.Console.WriteLine("hello, world");
    }
}
```

展示了若干单行注释。

### 2.3.3 空白

空白定义为 Unicode 类别为 Zs 的任何字符（包括空格字符），以及水平制表符、垂直制表符和换页符。

```
whitespace:
    Any character with Unicode class Zs
    Horizontal tab character (U+0009)
    Vertical tab character (U+000B)
    Form feed character (U+000C)
```

## 2.4 标记

标记有几种类型：标识符、关键字、字面量、运算符和标点符号。空白和注释不是标记，尽管它们充当标记的分隔符。

```
token:
    identifier
    keyword
    integer-literal
    real-literal
    character-literal
    string-literal
    operator-or-punctuator
```

### 2.4.1 Unicode 字符转义序列

Unicode 字符转义序列表示一个 Unicode 字符。Unicode 字符转义序列会在标识符（§2.4.2）、字符字面量（§2.4.4）和常规字符串字面量（§2.4.5）中处理。Unicode 字符转义不会在其他任何位置处理（例如，用于构成运算符、标点符号或关键字）。

```
unicode-escape-sequence:
    \u hex-digit hex-digit hex-digit hex-digit
    \U hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit
```

> **ERIC LIPPERT** 这种做法与 Java 不同，在 Java 中 Unicode 转义序列几乎可以出现在任何地方。

Unicode 转义序列表示由“\u”或“\U”字符后面的十六进制数字构成的单个 Unicode 字符。由于 C# 在字符值和字符串值中使用 Unicode 码点的 16 位编码，因此字符字面量中不允许使用 U+10000 到 U+10FFFF 范围内的 Unicode 字符，并且会在字符串字面量中使用 Unicode 代理项对来表示该字符。不支持码点高于 0x10FFFF 的 Unicode 字符。

不执行多重转换。例如，字符串字面量“`\u005C\u005C`”等价于“`\u005C`”，而不是“`\\`”。Unicode 值 `\u005C` 是字符“`\`”。

示例

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

展示了 \u0066 的若干用法，它是字母“f”的转义序列。该程序等价于

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

### 2.4.2 标识符

本节给出的标识符规则与 Unicode 标准附件 31 推荐的规则完全对应，但有以下例外：允许下划线作为初始字符（这是 C 编程语言中的传统做法），标识符中允许使用 Unicode 转义序列，并且允许“@”字符作为前缀，以便关键字可用作标识符。

```
identifier:
    available-identifier
    @ identifier-or-keyword

available-identifier:
    An identifier-or-keyword that is not a keyword

identifier-or-keyword:
    identifier-start-character identifier-part-characters opt

identifier-start-character:
    letter-character
    _ (the underscore character U+005F)

identifier-part-characters:
    identifier-part-character
    identifier-part-characters identifier-part-character

identifier-part-character:
    letter-character
    decimal-digit-character
    connecting-character
    combining-character
    formatting-character

letter-character:
    A Unicode character of classes Lu, Ll, Lt, Lm, Lo, or Nl
    A unicode-escape-sequence representing a character of classes Lu, Ll, Lt, Lm, Lo, or Nl

combining-character:
    A Unicode character of classes Mn or Mc
    A unicode-escape-sequence representing a character of classes Mn or Mc

decimal-digit-character:
    A Unicode character of the class Nd
    A unicode-escape-sequence representing a character of the class Nd

connecting-character:
    A Unicode character of the class Pc
    A unicode-escape-sequence representing a character of the class Pc

formatting-character:
    A Unicode character of the class Cf
    A unicode-escape-sequence representing a character of the class Cf
```

有关上述 Unicode 字符类的信息，请参见 The Unicode Standard, Version 3.0 第 4.5 节。

有效标识符的示例包括“identifier1”、“_identifier2”和“@if”。

符合规范的程序中的标识符必须采用由 Unicode 标准附件 15 定义的 Unicode 规范化形式 C 所规定的规范格式。遇到不处于规范化形式 C 的标识符时的行为由实现定义；但是，不要求产生诊断。




前缀“@”允许将关键字用作标识符，这在与其他编程语言交互时很有用。字符 @ 实际上并不是标识符的一部分，因此在其他语言中，该标识符可能被视为不带前缀的普通标识符。带有 @ 前缀的标识符称为逐字标识符。对于不是关键字的标识符，允许使用 @ 前缀，但从风格上强烈不建议这样做。

示例

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
class Class1
{
    static void M() {
        cl\u0061ss.st\u0061tic(true);
    }
}
```

定义了一个名为“class”的类，其中有一个名为“static”的静态方法，该方法接受一个名为“bool”的参数。注意，由于关键字中不允许使用 Unicode 转义，因此标记“cl\u0061ss”是一个标识符，并且与“@class”是同一个标识符。

如果两个标识符按顺序应用以下变换后相同，则认为它们是相同的：
- 如果使用了前缀“@”，则将其移除。
- 每个 Unicode 转义序列都被转换为对应的 Unicode 字符。
- 移除任何格式字符。

包含两个连续下划线字符（U+005F）的标识符保留给实现使用。例如，实现可能提供以两个下划线开头的扩展关键字。

## 2.4.3 关键字

关键字是类似标识符的字符序列，它是保留的，除非前面加上 @ 字符，否则不能用作标识符。

keyword: one of
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

在语法的某些位置，特定标识符具有特殊含义，但它们不是关键字。此类标识符有时称为“上下文关键字”。例如，在属性声明中，标识符“get”和“set”具有特殊含义（§10.7.2）。在这些位置，绝不允许使用 get 或 set 以外的标识符，因此这种用法不会与将这些词用作标识符发生冲突。在其他情况下，例如在隐式类型局部变量声明（§8.5.1）中使用标识符“var”时，上下文关键字可能与已声明的名称冲突。在这种情况下，已声明的名称优先于将该标识符用作上下文关键字。

> **ERIC LIPPERT** 自最初发布以来，C# 没有添加任何新的保留关键字。所有需要新关键字（yield、select 等）的新语言特性都使用“上下文关键字”，这些关键字不是保留的，只在上下文中具有特殊含义。这一决定有助于保持与现有程序的向后兼容性。

> **VLADIMIR RESHETNIKOV** 如果你需要这些上下文关键字的完整列表（包括支持的属性目标），如下所示：
> 
> `add alias ascending assembly by descending dynamic equals field from get global group into join let method module on orderby param partial property remove select set type typevar value var where yield`

## 2.4.4 字面量

字面量是值的源代码表示形式。

```
literal:
  boolean-literal
  integer-literal
  real-literal
  character-literal
  string-literal
  null-literal
```

### 2.4.4.1 布尔字面量

有两个布尔字面量值：true 和 false。

```
boolean-literal:
  true
  false
```

布尔字面量的类型是 bool。

### 2.4.4.2 整数字面量

整数字面量用于写入 int、uint、long 和 ulong 类型的值。整数字面量有两种可能的形式：十进制和十六进制。

```
integer-literal:
  decimal-integer-literal
  hexadecimal-integer-literal

decimal-integer-literal:
  decimal-digits integer-type-suffix_opt

decimal-digits:
  decimal-digit
  decimal-digit decimal-digit

decimal-digit: one of
  0 1 2 3 4 5 6 7 8 9

integer-type-suffix: one of
  U u L l UL Ul uL ul LU Lu lU lu
```

```
hexadecimal-integer-literal:
    0x hex-digits integer-type-suffix_opt
    0X hex-digits integer-type-suffix_opt
```

```
hex-digits:
    hex-digit
    hex-digits hex-digit
```

hex-digit: one of
0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f

> **ERIC LIPPERT** C# 不支持八进制字面量，原因有两个。首先，如今几乎没有人使用八进制字面量。其次，如果 C# 以标准的“前导零表示八进制”格式支持八进制，那么它可能会成为错误的潜在来源。考虑以下代码：
> 
> `FlightNumber = 0541;`
> 
> 显然，这个表达式意图作为十进制字面量，而不是八进制字面量。

整数字面量的类型确定如下：
- 如果字面量没有后缀，则其类型为这些类型中第一个能够表示其值的类型：int、uint、long、ulong。
- 如果字面量带有 U 或 u 后缀，则其类型为这些类型中第一个能够表示其值的类型：uint、ulong。
- 如果字面量带有 L 或 l 后缀，则其类型为这些类型中第一个能够表示其值的类型：long、ulong。
- 如果字面量带有 UL、Ul、uL、ul、LU、Lu、lU 或 lu 后缀，则其类型为 ulong。

如果整数字面量表示的值超出 ulong 类型的范围，则发生编译时错误。

从风格上讲，建议在书写 long 类型的字面量时使用“L”而不是“l”，因为很容易将字母“l”与数字“1”混淆。

为了允许最小的 int 和 long 值能够写成十进制整数字面量，存在以下两条规则：
- 当值为 2147483648（2^31）且没有整数类型后缀的十进制整数字面量作为紧接在一元减运算符标记（§7.7.2）之后的标记出现时，结果是类型为 int、值为 −2147483648（−2³¹）的常量。在所有其他情况下，这样的十进制整数字面量是 uint 类型。
- 当值为 9223372036854775808（2⁶³）且没有整数类型后缀或整数类型后缀为 L 或 l 的十进制整数字面量作为紧接在一元减运算符标记（§7.7.2）之后的标记出现时，结果是类型为 long、值为 −9223372036854775808（−2⁶³）的常量。在所有其他情况下，这样的十进制整数字面量是 ulong 类型。

> **JOSEPH ALBAHARI** 得益于隐式常量表达式转换（§6.1.8），整数字面量可以直接赋值给 uint、long 和 ulong 类型（以及 short、ushort、byte 和 sbyte）：
> 
> ```
> uint x = 3; long y = 3; ulong z = 3;
> ```
> 
> 因此，U 和 L 后缀很少有必要。它们仍然有用的一个例子是，强制对原本会采用 32 位算术的字面量进行 64 位计算：
> 
> ```
> long error = 1000000 * 1000000; // Compile-time error (32-bit overflow)
> long trillion = 1000000L * 1000000L; // Okay -- no overflow
> ```

### 2.4.4.3 实数字面量

实数字面量用于写入 float、double 和 decimal 类型的值。

real-literal:
  decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
  . decimal-digits exponent-part_opt real-type-suffix_opt
  decimal-digits exponent-part_opt real-type-suffix_opt
  decimal-digits real-type-suffix_opt

exponent-part:
  e sign_opt decimal-digits
  E sign_opt decimal-digits

sign: one of
  + -

real-type-suffix: one of
  F f D d M m

如果未指定 real-type-suffix，则实数字面量的类型为 double。否则，实数类型后缀按如下方式确定实数字面量的类型：
- 带有 F 或 f 后缀的实数字面量是 float 类型。例如，字面量 1f、1.5f、1e10f 和 123.456F 都是 float 类型。
- 带有 D 或 d 后缀的实数字面量是 double 类型。例如，字面量 1d、1.5d、1e10d 和 123.456D 都是 double 类型。
- 带有 M 或 m 后缀的实数字面量是 decimal 类型。例如，字面量 1m、1.5m、1e10m 和 123.456M 都是 decimal 类型。该字面量通过取精确值，并在必要时使用银行家舍入（§4.1.7）舍入到最接近的可表示值，从而转换为 decimal 值。除非值被舍入或值为零（在后一种情况下，符号和标度将为 0），否则字面量中明显可见的任何标度都会保留。因此，字面量 2.900m 将被解析为符号为 0、系数为 2900、标度为 3 的 decimal。

如果指定的字面量无法在指示的类型中表示，则发生编译时错误。

float 或 double 类型的实数字面量的值通过使用 IEEE“就近舍入”模式确定。

注意，在实数字面量中，小数点后始终需要十进制数字。例如，1.3F 是实数字面量，而 1.F 不是。

> **JOSEPH ALBAHARI** 在所有数值后缀中，m 和 f 是迄今为止最有用的。没有这些后缀，就无法在不进行强制转换的情况下指定小数形式的 float 或 decimal 字面量。例如，以下代码将无法编译，因为字面量 1.5 将被解析为 double 类型：
> 
> ```csharp
> float x = 1.5; // Error: no implicit conversion from double to float
> decimal y = 1.5; // Error: no implicit conversion from double to decimal
> ```
> 
> 有趣的是，以下代码确实可以编译，因为 C# 定义了从 int 到 decimal 的隐式转换：
> 
> ```csharp
> decimal z = 123; // Okay: parsed as int, and then implicitly converted
> // to decimal
> ```
> 
> 从技术上讲，d 后缀是多余的，因为小数点的存在起到了同样的作用：
> 
> ```csharp
> Console.WriteLine ((123.0).GetType() == typeof (double));// True
> ```

### 2.4.4.4 字符文字

字符文字表示单个字符，通常由引号中的字符组成，如 'a'。

```
character-literal:
  ' character '
```

```
character:
  single-character
  simple-escape-sequence
  hexadecimal-escape-sequence
  unicode-escape-sequence
```

```
single-character:
  Any character except ' (U+0027), \ (U+005C), and new-line-character
```

```
simple-escape-sequence: one of
  \' \" \\ \0 \a \b \f \n \r \t \v
```

```
hexadecimal-escape-sequence:
  \x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt
```

在字符中跟在反斜杠字符（\）后面的字符必须是以下字符之一：'、\、0、a、b、f、n、r、t、u、U、x、v。否则会发生编译时错误。

十六进制转义序列表示单个 Unicode 字符，其值由 "\x" 后的十六进制数字形成。

如果字符文字表示的值大于 U+FFFF，则会发生编译时错误。

字符文字中的 Unicode 字符转义序列（§2.4.1）必须在 U+0000 到 U+FFFF 范围内。

简单转义序列表示 Unicode 字符编码，如下表所述。

| 转义序列 | 字符名称 | Unicode 编码 |
|---|---|---|
| \' | 单引号 | 0x0027 |
| \" | 双引号 | 0x0022 |
| \\ | 反斜杠 | 0x005C |
| `\0` | 空字符 | `0x0000` |
| `\a` | 警报 | `0x0007` |
| `\b` | 退格 | `0x0008` |
| `\f` | 换页 | `0x000C` |
| `\n` | 换行 | `0x000A` |
| `\r` | 回车 | `0x000D` |
| `\t` | 水平制表符 | `0x0009` |
| `\v` | 垂直制表符 | `0x000B` |

*character-literal* 的类型是 `char`。

### 2.4.4.5 字符串文字

C# 支持两种形式的字符串文字：*regular string literals* 和 *verbatim string literals*。

常规字符串文字由双引号括起来的零个或多个字符组成，如 "hello"，并且可以包含简单转义序列（如 `\t` 表示制表符），以及十六进制和 Unicode 转义序列。

逐字字符串文字由 @ 字符、双引号字符、零个或多个字符以及闭合的双引号字符组成。简单示例是 @"hello"。在逐字字符串文字中，定界符之间的字符按字面解释，唯一例外是 *quote-escape-sequence*。特别是，简单转义序列以及十六进制和 Unicode 转义序列在逐字字符串文字中不会被处理。逐字字符串文字可以跨越多行。

> > **JON SKEET** 让我感到不安的逐字字符串文字的一个方面是换行会以其在文件中出现的形式呈现。当然这是自然的选择，但这意味着在 "\r\n" 和 "\n" 换行之间切换文件并不是纯粹的装饰性更改：它也可能影响行为。

## 2. 词法结构

```
string-literal:
  regular-string-literal
  verbatim-string-literal

regular-string-literal:
  " regular-string-literal-characters_opt "

regular-string-literal-characters:
  regular-string-literal-character
  regular-string-literal-characters regular-string-literal-character

regular-string-literal-character:
  single-regular-string-literal-character
  simple-escape-sequence
  hexadecimal-escape-sequence
  unicode-escape-sequence

single-regular-string-literal-character:
  Any character except " (U+0022), \ (U+005C), and new-line-character

verbatim-string-literal:
  @" verbatim-string-literal-characters_opt "

verbatim-string-literal-characters:
  verbatim-string-literal-character
  verbatim-string-literal-characters verbatim-string-literal-character

verbatim-string-literal-character:
  single-verbatim-string-literal-character
  quote-escape-sequence

single-verbatim-string-literal-character:
  Any character except "

quote-escape-sequence:
  ""
```

在 regular-string-literal-character 中跟在反斜杠字符（\）后面的字符必须是以下字符之一：'、"、\、0、a、b、f、n、r、t、u、U、x、v。否则会发生编译时错误。

### 示例

```
string a = "hello, world"; // hello, world
string b = @"hello, world"; // hello, world
string c = "hello \t world"; // hello world
string d = @"hello \t world"; // hello \t world
string e = "Joe said \"Hello\" to me"; // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me"; // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt"; // \\server\share\file.txt
string h = @"\\server\share\file.txt"; // \\server\share\file.txt

string i = "one\n\r\n two\r\nthree";
string j = @"one
two
three";
```

显示了各种字符串文字。最后一个字符串文字 j 是一个跨越多行的逐字字符串文字。引号之间的字符，包括换行符等空白，都被原样保留。

> **BRAD ABRAMS** 在 C# 语言设计的早期，我们尝试使用反引号（`）字符。个人而言，我真的很喜欢这个选择：反引号属于引号家族，是一个严重被低估的字符。事实上，它被低估到有些国际键盘甚至不包含它的键。我们很幸运地拥有 C# 早期良好的国际关注度，这使我们能够在语言设计的早期就修复这个潜在错误。

由于十六进制转义序列可以有可变数量的十六进制数字，字符串文字 "\x123" 包含一个十六进制值为 123 的单个字符。要创建包含十六进制值为 12 的字符后跟字符 3 的字符串，可以改写为 "\x00123" 或 "\x12" + "3"。

> **JON SKEET** 十六进制转义序列不仅罕见——而且危险。虽然像 "\x9Tabbed" 这样的字符串相当清晰，但 "\x9Badly tabbed" 实际上以 Unicode 字符 U+9BAD 开头却并不那么明显。

string-literal 的类型是 string。

每个字符串文字不一定会产生一个新的字符串实例。当同一个程序中出现两个或多个根据字符串相等运算符（§7.10.7）等价的字符串文字时，这些字符串文字引用同一个字符串实例。例如，由以下代码产生的输出

```
```csharp
class Test
{
    static void Main() {
        object a = "hello";
        object b = "hello";
        System.Console.WriteLine(a == b);
    }
}
```
```

为 True，因为这两个文字引用同一个字符串实例。

> **JOSEPH ALBAHARI** 这种优化称为 *interning*。interning 的好处之一是它减少了编译后程序集的大小，因为重复的字符串文字被提取出来。
> 
> 在前面的示例中，a 和 b 声明为 object 类型，这迫使后续比较使用 object 的引用类型相等语义。如果 a 和 b 声明为 string 类型，比较将绑定到 string 的 == 运算符，只要字符串内容相同，即使它们引用不同的底层对象，也会求值为 true。

### 2.4.4.6 null 文字

null-literal:
null

*null-literal* 可以隐式转换为引用类型或可空类型。

> **ERIC LIPPERT** null 文字表达式本身没有类型。

### 2.4.5 运算符和标点符号

有几种类型的运算符和标点符号。运算符用于在表达式中描述涉及一个或多个操作数的操作。例如，表达式 a + b 使用 + 运算符将两个操作数 a 和 b 相加。标点符号用于分组和分隔。

operator-or-punctuator: one of
{ } [ ] ( ) . , : ;
+ - * / % & ^ ! ~
= < > ? ?? :: ++ -- && ||
-> == != <= >= += -= *= /= %=
&= |= ^= << <<= =>

right-shift:
>|

right-shift-assignment:
>|=

right-shift 和 right-shift-assignment 产生式中的垂直条用于表示，与语法文法中的其他产生式不同，不允许在标记之间存在任何字符（甚至空白）。这些产生式被特殊处理以实现对类型参数列表（§10.1.3）的正确处理。

## 2.5 预处理指令

> BILL WAGNER 本节展示了 C 传统如何为现代开发着色如此之多。我很少，甚至从不使用任何预处理指令——但我只能想象如果 C# 没有包含强大的预处理指令集会引发怎样的批评风暴。

预处理指令提供有条件地跳过源文件部分、报告错误和警告条件以及划定源代码不同区域的能力。术语“预处理指令”仅为与 C 和 C++ 编程语言保持一致而使用。在 C# 中没有单独的预处理步骤；预处理指令作为词法分析阶段的一部分进行处理。

- pp-directive:
- pp-declaration
- pp-conditional
- pp-line
- pp-diagnostic
- pp-region
- pp-pragma



## 2. 词法结构

以下预处理指令可用：

-   `#define` 和 `#undef`，分别用于定义和取消定义条件编译符号（§2.5.3）。
-   `#if`、`#elif`、`#else` 和 `#endif`，用于有条件地跳过源代码的某些部分（§2.5.4）。
-   `#line`，用于控制为错误和警告输出的行号（§2.5.7）。
-   `#error` 和 `#warning`，分别用于发出错误和警告（§2.5.5）。
-   `#region` 和 `#endregion`，用于显式标记源代码的某些部分（§2.5.6）。
-   `#pragma`，用于向编译器指定可选的上下文信息（§2.5.8）。

预处理指令总是占据源代码的单独一行，并且总是以 # 字符和预处理指令名称开头。在 # 字符之前以及 # 字符与指令名称之间可以出现空白。

包含 #define、#undef、#if、#elif、#else、#endif 或 #line 指令的源代码行可以以单行注释结尾。包含预处理指令的源代码行不允许使用分隔注释（即 `/* */` 风格的注释）。

预处理指令不是标记，也不属于 C# 的语法文法。然而，预处理指令可用于包含或排除标记序列，并可以这种方式影响 C# 程序的含义。例如，编译时，程序

```csharp
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

会得到与以下程序完全相同的标记序列

```csharp
class C
{
    void F() {}
    void I() {}
}
```

因此，尽管这两个程序在词法上大不相同，但在语法上完全相同。

### 2.5.1 条件编译符号

由 #if、#elif、#else 和 #endif 指令提供的条件编译功能，通过预处理表达式（§2.5.2）和条件编译符号进行控制。

```
conditional-symbol:
    Any identifier or keyword except true or false
```

条件编译符号有两种可能的状态：*已定义* 或 *未定义*。在源文件的词法处理开始时，条件编译符号是未定义的，除非它已由外部机制（例如命令行编译器选项）显式定义。处理 #define 指令时，该指令中命名的条件编译符号会在该源文件中变为已定义。该符号保持已定义，直到处理针对同一符号的 #undef 指令，或直到到达源文件末尾。这意味着，一个源文件中的 #define 和 #undef 指令对同一程序中的其他源文件没有影响。

在预处理表达式中引用时，已定义的条件编译符号具有布尔值 *true*，未定义的条件编译符号具有布尔值 *false*。不要求条件编译符号在预处理表达式中被引用之前显式声明。相反，未声明的符号只是未定义，因此值为 *false*。

条件编译符号的命名空间与 C# 程序中的所有其他命名实体截然不同且相互独立。条件编译符号只能在 #define 和 #undef 指令以及预处理表达式中引用。

### 2.5.2 预处理表达式

预处理表达式可以出现在 #if 和 #elif 指令中。预处理表达式中允许使用运算符 !、==、!=、&& 和 ||，并且可以使用括号进行分组。

```
pp-expression:
    whitespace_opt pp-or-expression whitespace_opt

pp-or-expression:
    pp-and-expression
    pp-or-expression whitespace_opt || whitespace_opt pp-and-expression

pp-and-expression:
    pp-equality-expression
    pp-and-expression whitespace_opt && whitespace_opt pp-equality-expression

pp-equality-expression:
    pp-unary-expression
    pp-equality-expression whitespace_opt == whitespace_opt pp-unary-expression
    pp-equality-expression whitespace_opt != whitespace_opt pp-unary-expression

pp-unary-expression:
    pp-primary-expression
    ! whitespace_opt pp-unary-expression

pp-primary-expression:
    true
    false
    conditional-symbol
    ( whitespace_opt pp-expression whitespace_opt )
```

在预处理表达式中引用时，已定义的条件编译符号具有布尔值 `true`，未定义的条件编译符号具有布尔值 `false`。

预处理表达式的求值始终产生布尔值。预处理表达式的求值规则与常量表达式（§7.19）的求值规则相同，区别在于可引用的唯一用户定义实体是条件编译符号。

### 2.5.3 声明指令

声明指令用于定义或取消定义条件编译符号。

```
pp-declaration:
    whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
    whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line

pp-new-line:
    whitespace_opt single-line-comment_opt new-line
```

处理 #define 指令会使给定的条件编译符号变为已定义，从该指令之后的源代码行开始。同样，处理 #undef 指令会使给定的条件编译符号变为未定义，从该指令之后的源代码行开始。

源文件中的任何 #define 和 #undef 指令都必须出现在该源文件的第一个 *标记*（§2.4）之前；否则会发生编译时错误。直观地说，#define 和 #undef 指令必须位于源文件中任何“真实代码”之前。

下面的示例是有效的，因为 #define 指令位于源文件的第一个标记（namespace 关键字）之前。

```csharp
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

下面的示例会导致编译时错误，因为 #define 位于真实代码之后：

```csharp
#define A
namespace N
{
    #define B
    #if B
    class Class1 {}
    #endif
}
```

#define 可以定义已经定义的条件编译符号，而无需在该符号之前有任何中间的 #undef。下面的示例定义条件编译符号 A，然后再次定义它。

```csharp
#define A
#define A
```

#undef 可以“取消定义”一个未定义的条件编译符号。下面的示例定义条件编译符号 A，然后两次取消定义它；尽管第二个 #undef 没有效果，但它仍然有效。

```csharp
#define A
#undef A
#undef A
```

### 2.5.4 条件编译指令

条件编译指令用于有条件地包含或排除源文件的某些部分。

```
pp-conditional:
  pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif

pp-if-section:
  whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line
  conditional-section_opt

pp-elif-sections:
  pp-elif-section
  pp-elif-sections pp-elif-section

pp-elif-section:
  whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line
  conditional-section_opt

pp-else-section:
  whitespace_opt # whitespace_opt else pp-new-line conditional-section_opt

pp-endif:
  whitespace_opt # whitespace_opt endif pp-new-line

conditional-section:
  input-section
  skipped-section

skipped-section:
  skipped-section-part
  skipped-section skipped-section-part

skipped-section-part:
  skipped-characters_opt new-line
  pp-directive

skipped-characters:
  whitespace_opt not-number-sign input-characters_opt

not-number-sign:
  Any input-character except #
```



正如语法所示，条件编译指令必须写成由以下部分按顺序组成的集合：一个 #if 指令、零个或多个 #elif 指令、零个或一个 #else 指令，以及一个 #endif 指令。这些指令之间是源代码的条件节。每个节由紧邻其前的指令控制。条件节本身可以包含嵌套的条件编译指令，前提是这些指令构成完整的集合。

> CHRIS SELLS  我能看到 #if 和 #endif，但 #elif 呢？这是不是某个口齿不清的圣诞老人助手？还是对某种大型、灰色、皱巴巴动物的潮人缩写？我宁愿多花两个字符写成 #elseif，就为了我真能记住它……

一个 pp 条件会从所含的条件节中至多选择一个，用于正常的词法处理；

- #if 和 #elif 指令的 pp 表达式按顺序求值，直到其中一个结果为 true。如果某个表达式结果为 true，则选择对应指令的条件节。
- 如果所有 pp 表达式的结果都为 false，并且存在 #else 指令，则选择 #else 指令的条件节。
- 否则，不选择任何条件节。

被选中的条件节（如果有）会作为普通输入节处理：该节中包含的源代码必须遵循词法语法；会根据该节中的源代码生成标记；该节中的预处理指令具有规定的效果。

其余条件节（如果有）会作为跳过节处理：除预处理指令外，该节中的源代码不必遵循词法语法；不会根据该节中的源代码生成标记；该节中的预处理指令必须在词法上正确，但不会进行其他处理。在被作为跳过节处理的条件节内，任何嵌套的条件节（包含在嵌套的 #if...#endif 和 #region...#endregion 构造中）也会作为跳过节处理。

下面的示例说明了条件编译指令如何嵌套：

```
#define Debug      // Debugging on
#undef Trace      // Tracing off
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
}
```

除预处理指令外，跳过的源代码不进行词法分析。例如，尽管 #else 节中的注释未终止，下面的代码仍然有效：

```
#define Debug      // Debugging on
class PurchaseTransaction
{
    void Commit() {
        #if Debug
        CheckConsistency();
        #else
        // Do something else
        #endif
    }
}
```

但请注意，即使在源代码的跳过节中，预处理指令也必须在词法上正确。

> CHRIS SELLS  如果可以，请避免使用嵌套的预处理指令，原因很简单：默认情况下，地球上最流行的 C# 编辑器 Visual Studio 会把它们沿文本文件左边缘排列，使得跟踪嵌套关系变得非常困难。例如，

```
#define Debug      // Debugging on
#undef Trace       // Tracing off
class PurchaseTransaction {
void Commit() {
#if Debug
    CheckConsistency();
#if Trace
    WriteToLog(this.ToString());
#endif
#endif
    CommitHelper();
}
}
```

当预处理指令出现在多行输入元素内部时，不会被处理。例如，下面的程序

```
class Hello
{
    static void Main() {
        System.Console.WriteLine(@"hello,
#if Debug
        World
#else
        Nebraska
#endif
        ");
    }
}
```

会得到以下输出：

```
hello,
#if Debug
        World
#else
        Nebraska
#endif
```

在特殊情况下，实际处理的预处理指令集合可能取决于 pp 表达式的求值结果。例如

```
#if X
    /*
#else
    /* */ class Q { }
#endif
```

无论 X 是否定义，下面的示例总是产生相同的标记流（class Q { }）。如果定义了 X，由于多行注释，只有 #if 和 #endif 是被处理的指令。如果未定义 X，那么三个指令（#if、#else、#endif）都属于指令集合。

## 2.5.5 诊断指令

诊断指令用于显式生成错误和警告消息，这些消息的报告方式与其他编译时错误和警告相同。

```
pp-diagnostic:
    whitespace     # whitespace   error   pp-message
    whitespace_opt # whitespace   warning pp-message
```

```
pp-message:
    new-line
    whitespace input-characters_opt new-line
```

### 示例

```
#warning Code review needed before check-in
#if Debug && Retail
    #error A build can't be both debug and retail
#endif
class Test {...}
```

如果条件符号 Debug 和 Retail 都已定义，下面的示例总是产生一个警告（“Code review needed before check-in”），并产生一个编译时错误（“A build can't be both debug and retail”）。请注意，pp 消息可以包含任意文本；具体来说，它不必包含格式良好的标记，正如单词 can't 中的单引号所示。

## 2.5.6 区域指令

区域指令用于显式标记源代码区域。

```
pp-region:
    pp-start-region conditional-section_opt pp-end-region
```

```
pp-start-region:
    whitespace_opt # whitespace_opt region pp-message
```

```
pp-end-region:
    whitespace_opt # whitespace_opt endregion pp-message
```

区域不附带语义含义；区域旨在供程序员或自动化工具用来标记源代码的某一部分。#region 或 #endregion 指令中指定的消息同样没有语义含义；它仅用于标识该区域。匹配的 #region 和 #endregion 指令可以具有不同的 pp 消息。

对区域

```
#region
...
#endregion
```

的词法处理与对以下形式的条件编译指令的词法处理完全对应：

```
#if true
...
#endif
```

## 2.5.7 行指令

行指令可用于更改编译器在警告和错误等输出中报告的行号和源文件名。

行指令最常用于从其他文本输入生成 C# 源代码的元编程工具中。

```
pp-line:
    whitespace_opt # whitespace_opt line whitespace line-indicator pp-new-line
```

```
line-indicator:
    decimal-digits whitespace file-name
    decimal-digits
    default
    hidden
```

```
file-name:
    " file-name-characters "
```

```
file-name-characters:
    file-name-characters file-name-character
```

```
file-name-character:
    Any input-character except "
```

当不存在 #line 指令时，编译器在其输出中报告真实的行号和源文件名。当处理包含非 default 行指示符的 #line 指令时，编译器将该指令之后的下一行视为具有给定的行号（以及指定的文件名，如果指定了的话）。

> **JON SKEET**  如果你正在编写一个从其他源生成代码的工具，你可能会认为最简单的方法就是为输出的每一行都包含一个 #line 指令。然而，事情并没有那么简单：逐字字符串字面量中的 #line 指令最终会成为字符串的一部分，而不会被当作指令处理。因此，下面的代码几乎肯定无法按预期工作：

```
#line 5
Console.WriteLine(@"First line
#line 6
Second line");
```

#line default 指令会撤销所有先前 #line 指令的效果。编译器会为后续行报告真实的行信息，就好像没有处理过任何 #line 指令一样。

#line hidden 指令对错误消息中报告的文件和行号没有影响，但会影响源代码级调试。调试时，在 #line hidden 指令与后续 #line 指令（不是 #line hidden）之间的所有行都没有行号信息。在调试器中单步执行代码时，这些行会被完全跳过。

请注意，file-name 与常规字符串字面量不同，因为转义字符不会被处理；'\' 字符只是表示 file-name 中的普通反斜杠字符。

## 2.5.8 Pragma 指令

#pragma 预处理指令用于向编译器指定可选的上下文信息。#pragma 指令中提供的信息绝不会改变程序语义。

```
pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line
```

```
pragma-body:
    pragma-warning-body
```

C# 提供 #pragma 指令来控制编译器警告。该语言的未来版本可能会包含其他 #pragma 指令。为确保与其他 C# 编译器的互操作性，Microsoft C# 编译器不会对未知的 #pragma 指令发出编译错误；不过，这类指令确实会生成警告。

### 2.5.8.1 Pragma 警告

#pragma warning 指令用于在编译后续程序文本期间禁用或恢复全部或特定的一组警告消息。

```
pragma-warning-body:
    warning whitespace warning-action
    warning whitespace warning-action whitespace warning-list
```

```
warning-action:
    disable
    restore
```



```
warning-list:
    decimal-digits
    warning-list whitespace_opt , whitespace_opt decimal-digits
```

省略警告列表的 #pragma warning 指令会影响所有警告。包含警告列表的 #pragma warning 指令只影响该列表中指定的那些警告。

> JON SKEET 我不确定默认影响所有警告是不是个好主意。要求显式使用“all”作为另一种警告列表不会与其他任何警告冲突（因为单个警告必须是数字），而且会让含义清楚得多。话虽如此，我从未见过有人禁用所有警告——而且我希望永远不要这样做。

指令 #pragma warning disable 会禁用所有警告或给定的一组警告。

指令 #pragma warning restore 会将所有警告或给定的一组警告恢复到编译单元开始时生效的状态。请注意，如果某个特定警告是在外部被禁用的，则 #pragma warning restore（无论针对所有警告还是该特定警告）不会重新启用该警告。

以下示例演示如何使用 #pragma warning 临时禁用引用过时成员时报告的警告，其中使用 Microsoft C# 编译器的警告编号。

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

> JOSEPH ALBAHARI 当编译器检测到可能表明代码中存在错误的状况时，会生成警告。由于存在误报的可能，能够针对选定的代码行禁用某些警告对于维持良好的信噪比很重要——这样真正的错误才会被注意到。如果你想让编译器将警告视为错误，这一点也很关键——我在自己的项目中就是这么做的。

本页有意留白

# 3. 基本概念

### 3.1 应用程序启动

具有*入口点*的程序集称为*应用程序*。运行应用程序时，会创建一个新的*应用程序域*。同一台机器上可以同时存在同一个应用程序的多个不同实例化，每个实例化都有其自己的应用程序域。

*应用程序域*通过充当应用程序状态的容器来实现应用程序隔离。*应用程序域*充当应用程序及其使用的类库中定义的类型的容器和边界。加载到一个*应用程序域*中的类型与加载到另一个*应用程序域*中的相同类型是不同的，对象实例不会在*应用程序域*之间直接共享。例如，每个*应用程序域*都有这些类型的*静态变量*的自己的副本，并且类型的*静态构造函数*在每个*应用程序域*中最多运行一次。实现可以自由提供特定于实现的策略或机制来创建和销毁*应用程序域*。

当执行环境调用一个指定方法（称为应用程序的入口点）时，就会发生*应用程序启动*。此入口点方法始终命名为 `Main`，并且可以具有以下签名之一：

```
    static void Main() {...}
    static void Main(string[] args) {...}
    static int Main() {...}
    static int Main(string[] args) {...}
```

如所示，入口点可以选择性地返回一个 `int` 值。此返回值用于应用程序终止（§3.2）。

入口点可以选择性地具有一个形参。该参数可以具有任意名称，但参数的类型必须是 `string[]`。如果存在该形参，则执行环境会创建并传递一个 `string[]` 实参，其中包含启动应用程序时指定的命令行参数。该 `string[]` 实参永远不会是 `null`，但如果没有指定命令行参数，则其长度可以为零。

由于 C# 支持方法重载，类或结构体可以包含某个方法的多个定义，前提是每个定义具有不同的签名。然而，在单个程序中，任何类或结构体都不能包含多个名为 Main 且其定义有资格用作应用程序入口点的方法。但是，允许 Main 的其他重载版本，前提是它们具有多个参数，或者它们唯一的参数不是 string[] 类型。

一个应用程序可以由多个类或结构体组成。这些类或结构体中的多个可能包含一个名为 Main 且其定义有资格用作应用程序入口点的方法。在这种情况下，必须使用外部机制（例如命令行编译器选项）来选择其中一个 Main 方法作为入口点。

> ERIC LIPPERT “csc”命令行编译器为此提供了 /main: 开关。

在 C# 中，每个方法都必须定义为类或结构体的成员。通常，方法的声明可访问性（§3.5.1）由其声明中指定的访问修饰符（§10.3.5）决定，类似地，类型的声明可访问性由其声明中指定的访问修饰符决定。要使给定类型的给定方法可调用，该类型和该成员都必须可访问。然而，应用程序入口点是一个特殊情况。具体而言，无论其声明可访问性如何，也无论其封闭类型声明的声明可访问性如何，执行环境都可以访问应用程序的入口点。

应用程序入口点方法不能位于泛型类声明中。

在所有其他方面，入口点方法的行为与非入口点方法一样。

### 3.2 应用程序终止

*应用程序终止*将控制权返回给执行环境。

如果应用程序的*入口点*方法的返回类型是 *int*，则返回的值用作应用程序的*终止状态代码*。此代码的用途是允许向执行环境传达成功或失败。

如果入口点方法的返回类型是 *void*，则到达终止方法的右大括号（{}），或执行没有表达式的 *return* 语句，会导致终止状态代码为 0。

> **BILL WAGNER** 以下规则是 C# 与其他托管环境之间的一个重要区别。

在应用程序终止之前，会调用其所有尚未被垃圾回收的对象的析构函数，除非此类清理已被抑制（例如，通过调用库方法 GC.SuppressFinalize）。

### 3.3 声明

C# 程序中的声明定义程序的构成元素。C# 程序使用命名空间（§9）进行组织，命名空间可以包含类型声明和嵌套命名空间声明。类型声明（§9.6）用于定义类（§10）、结构体（§10.14）、接口（§13）、枚举（§14）和委托（§15）。类型声明中允许的成员种类取决于类型声明的形式。例如，类声明可以包含常量（§10.4）、字段（§10.5）、方法（§10.6）、属性（§10.7）、事件（§10.8）、索引器（§10.9）、运算符（§10.10）、实例构造函数（§10.11）、静态构造函数（§10.12）、析构函数（§10.13）和嵌套类型（§10.3.8）的声明。

声明在其所属的*声明空间*中定义一个名称。除重载成员（§3.6）外，在一个声明空间中存在两个或更多引入同名成员的声明是编译时错误。声明空间绝不可能包含同名的不同种类成员。例如，声明空间绝不能包含同名的字段和方法。

> **ERIC LIPPERT** “声明空间”经常与“作用域”混淆。虽然二者在概念上相关，但用途却大不相同。命名元素的作用域是程序文本中可以在不添加额外限定的情况下通过名称引用该元素的区域。相比之下，元素的声明空间是其中不能有两个元素同名的区域。（嗯，几乎如此——如果方法签名不同，则方法可以同名；如果类型的泛型参数数量不同，则类型可以同名。）

声明空间有几种不同类型。

-   在程序的所有源文件中，没有封闭*命名空间声明*的*命名空间成员声明*是称为*全局声明空间*的单个合并声明空间的成员。




## 3. 基本概念

- 在程序的所有源文件中，具有相同完全限定命名空间名的 *命名空间声明* 内的 *命名空间成员声明* 是单个组合声明空间的成员。
- 每个类、结构或接口声明都会创建一个新的声明空间。名称通过 *类成员声明*、*结构成员声明*、*接口成员声明* 或 *类型参数* 引入此声明空间。除了重载实例构造函数声明和静态构造函数声明外，类或结构不能包含与类或结构同名的成员声明。类、结构或接口允许声明重载方法和索引器。此外，类或结构允许声明重载实例构造函数和运算符。例如，类、结构或接口可以包含多个同名方法声明，前提是这些方法声明在签名（§3.6）上不同。请注意，基类不参与类的声明空间，基接口不参与接口的声明空间。因此，派生类或接口允许声明与继承成员同名的成员。这样的成员称为 *隐藏* 继承成员。
- 每个委托声明都会创建一个新的声明空间。名称通过形参（*固定参数* 和 *参数数组*）以及 *类型参数* 引入此声明空间。
- 每个枚举声明都会创建一个新的声明空间。名称通过 *枚举成员声明* 引入此声明空间。
- 每个方法声明、索引器声明、运算符声明、实例构造函数声明和匿名函数都会创建一个新的声明空间，称为 *局部变量声明空间*。名称通过形参（*固定参数* 和 *参数数组*）以及 *类型参数* 引入此声明空间。函数成员或匿名函数的主体（如果有）被视为嵌套在局部变量声明空间内。局部变量声明空间和嵌套的局部变量声明空间包含同名元素是错误的。因此，在嵌套声明空间内，不能声明与外层声明空间中的局部变量或常量同名的局部变量或常量。两个声明空间可以包含同名元素，只要一个声明空间不包含另一个声明空间。
- 每个 *块* 或 *switch 块*，以及每个 *for*、*foreach* 和 *using* 语句，都会为局部变量和局部常量创建一个局部变量声明空间。名称通过 *局部变量声明* 和 *局部常量声明* 引入此声明空间。请注意，作为函数成员或匿名函数主体出现或位于其中的块，嵌套在这些函数为其参数声明的局部变量声明空间内。因此，例如，方法具有同名局部变量和参数是错误的。
- 每个 *块* 或 *switch 块* 为标签创建一个单独的声明空间。名称通过 *带标签语句* 引入此声明空间，并通过 *goto 语句* 引用这些名称。块的 *标签声明空间* 包括任何嵌套块。因此，在嵌套块内，不能声明与外层块中的标签同名的标签。

名称声明的文本顺序通常不重要。特别是，文本顺序对于命名空间、常量、方法、属性、事件、索引器、运算符、实例构造函数、析构函数、静态构造函数和类型的声明与使用并不重要。声明顺序在以下方面很重要：

- 字段声明和局部变量声明的声明顺序决定了其初始化器（如果有）的执行顺序。
- 局部变量必须在使用前定义（§3.7）。
- 当省略 *常量表达式* 值时，枚举成员声明（§14.3）的声明顺序很重要。

命名空间的声明空间是“开放式”的，两个具有相同完全限定名的命名空间声明参与同一个声明空间。例如：

```csharp
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

上述两个命名空间声明参与同一个声明空间，在本例中声明了两个完全限定名为 Megacorp.Data.Customer 和 Megacorp.Data.Order 的类。由于这两个声明参与同一个声明空间，如果每个声明都包含同名类的声明，就会导致编译时错误。

> **比尔·瓦格纳** 将命名空间视为管理代码逻辑组织的工具。相比之下，程序集管理代码的物理组织。

如上所述，块的声明空间包括任何嵌套块。因此，在以下示例中，F 和 G 方法会导致编译时错误，因为名称 i 在外层块中声明，不能在内部块中重新声明。但是，H 和 I 方法是有效的，因为两个 i 是在分开的非嵌套块中声明的。

```csharp
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
            H();
        for (int i = 0; i < 10; i++)
            H();
    }
}
```

### 3.4 成员

命名空间和类型具有成员。实体的成员通常可通过使用限定名来访问，该限定名以对实体的引用开头，后跟一个“.”标记，再后跟成员名称。

类型的成员要么在类型声明中声明，要么从该类型的基类继承。当类型从基类继承时，基类的所有成员（实例构造函数、析构函数和静态构造函数除外）都成为派生类型的成员。基类成员的声明可访问性并不控制该成员是否被继承——继承扩展到任何不是实例构造函数、静态构造函数或析构函数的成员。但是，继承成员在派生类型中可能不可访问，这可能是由于其声明的可访问性（§3.5.1），也可能是由于它被类型自身的声明隐藏（§3.7.1.2）。

#### 3.4.1 命名空间成员

没有外层命名空间的命名空间和类型是全局命名空间的成员。这直接对应于在全局声明空间中声明的名称。

在命名空间内声明的命名空间和类型是该命名空间的成员。这直接对应于在该命名空间的声明空间中声明的名称。

命名空间没有访问限制。不能声明私有、受保护或内部命名空间，并且命名空间名称始终可公开访问。

#### 3.4.2 结构成员

结构的成员包括在结构中声明的成员，以及从结构的直接基类 System.ValueType 和间接基类 object 继承的成员。

简单类型的成员直接对应于该简单类型所别名化的结构类型的成员：

- sbyte 的成员是 System.SByte 结构的成员。
- byte 的成员是 System.Byte 结构的成员。
- short 的成员是 System.Int16 结构的成员。
- ushort 的成员是 System.UInt16 结构的成员。
- int 的成员是 System.Int32 结构的成员。
- uint 的成员是 System.UInt32 结构的成员。
- long 的成员是 System.Int64 结构的成员。





- ulong 的成员是 System.UInt64 结构的成员。
- char 的成员是 System.Char 结构的成员。
- float 的成员是 System.Single 结构的成员。
- double 的成员是 System.Double 结构的成员。
- decimal 的成员是 System.Decimal 结构的成员。
- bool 的成员是 System.Boolean 结构的成员。

### 3.4.3 枚举成员

枚举的成员包括在枚举中声明的常量，以及从枚举的直接基类 System.Enum 和间接基类 System.ValueType、object 继承的成员。

### 3.4.4 类成员

类的成员包括在类中声明的成员，以及从基类继承的成员（类 object 除外，因为它没有基类）。从基类继承的成员包括基类的常量、字段、方法、属性、事件、索引器、运算符和类型，但不包括基类的实例构造函数、析构函数和静态构造函数。无论基类成员具有什么可访问性，都会被继承。

类声明可以包含常量、字段、方法、属性、事件、索引器、运算符、实例构造函数、析构函数、静态构造函数和类型的声明。

object 和 string 的成员分别直接对应于它们所别名引用的类类型的成员：

- object 的成员是 System.Object 类的成员。
- string 的成员是 System.String 类的成员。

### 3.4.5 接口成员

接口的成员包括在接口中声明的成员，以及该接口的所有基接口中的成员。严格来说，类 object 中的成员并不是任何接口的成员（§13.2）。但是，可以通过成员查找在任何接口类型中使用类 object 中的成员（§7.4）。

### 3.4.6 数组成员

数组的成员是从 System.Array 类继承的成员。

### 3.4.7 委托成员

委托的成员是从 `System.Delegate` 类继承的成员。

> **VLADIMIR RESHETNIKOV** 在 Microsoft 的 C# 实现中，委托的成员还包括实例方法 `Invoke`、`BeginInvoke` 和 `EndInvoke`，以及从 `System.MulticastDelegate` 类继承的成员。

> **JON SKEET** Vladimir 提到的 `Invoke`、`BeginInvoke` 和 `EndInvoke` 方法无法在 `Delegate` 或 `MulticastDelegate` 类型中指定，因为它们取决于委托的参数和返回类型。这是参数化类型的一个示例：即使泛型从 C# 的第一个版本开始就存在，也未必能够很好地处理这种情况。

## 3.5 成员访问

成员声明允许控制成员访问。成员的可访问性由成员声明的可访问性（§3.5.1）与直接包含类型（如果存在）的可访问性共同确定。

当允许访问某个特定成员时，该成员被称为*可访问的*。相反，当不允许访问某个特定成员时，该成员被称为*不可访问的*。当发生访问的文本位置包含在成员的可访问性域（§3.5.2）中时，便允许访问该成员。

### 3.5.1 声明的可访问性

成员的*声明的可访问性*可以是以下几种之一：

- Public，这通过在成员声明中包含 public 修饰符来选择。public 的直观含义是“访问不受限制”。
- Protected，这通过在成员声明中包含 protected 修饰符来选择。protected 的直观含义是“访问仅限于包含类或从包含类派生的类型”。
- Internal，这通过在成员声明中包含 internal 修饰符来选择。internal 的直观含义是“访问仅限于此程序”。
- Protected internal（表示 protected 或 internal），这通过在成员声明中同时包含 protected 和 internal 修饰符来选择。protected internal 的直观含义是“访问仅限于此程序或从包含类派生的类型”。
- Private，这通过在成员声明中包含 private 修饰符来选择。private 的直观含义是“访问仅限于包含类型”。

> **JESSE LIBERTY** 虽然始终存在默认可访问性，但明确声明可访问性是一种良好的编程实践。这样编写的代码更易于阅读，也更易于维护。

> **JON SKEET** C# 对默认可访问性的选择非常合理。除了允许属性的 getter/setter 比整个属性声明具有更严格的限制这一情况外，默认可访问性始终是可用的最严格级别。过去我更倾向于将可访问性作为隐式值保留，但随着时间推移，我逐渐认同 Jesse 的观点。将任何内容明确写出，都表明你意识到存在一种选择，并且是有意选择了这个特定选项。如果将选择隐式保留，可能是因为你希望采用该选项，也可能是因为你一开始就忘记了存在需要作出的选择。

根据成员声明所在的上下文，只允许使用某些类型的声明可访问性。此外，当成员声明不包含任何访问修饰符时，声明所在的上下文决定默认的声明可访问性。

- 命名空间隐式具有 public 声明的可访问性。命名空间声明不允许使用访问修饰符。
- 在编译单元或命名空间中声明的类型可以具有 public 或 internal 声明的可访问性，默认具有 internal 声明的可访问性。
- 类成员可以具有五种声明的可访问性中的任意一种，默认具有 private 声明的可访问性。（请注意，声明为类成员的类型可以具有五种声明的可访问性中的任意一种，而声明为命名空间成员的类型只能具有 public 或 internal 声明的可访问性。）

> **VLADIMIR RESHETNIKOV** 如果密封类声明了 protected 或 protected internal 成员，则会发出警告。如果静态类声明了 protected 或 protected internal 成员，则会发生编译时错误（CS1057）。

- 结构成员可以具有 public、internal 或 private 声明的可访问性，默认具有 private 声明的可访问性，因为结构隐式为密封的。在结构中引入的结构成员（即不是该结构继承的成员）不能具有 protected 或 protected internal 声明的可访问性。（请注意，声明为结构成员的类型可以具有 public、internal 或 private 声明的可访问性，而声明为命名空间成员的类型只能具有 public 或 internal 声明的可访问性。）
- 接口成员隐式具有 public 声明的可访问性。接口成员声明不允许使用访问修饰符。
- 枚举成员隐式具有 public 声明的可访问性。枚举成员声明不允许使用访问修饰符。

> **VLADIMIR RESHETNIKOV** 这里的“枚举成员”是指“在枚举中声明的成员”。枚举还从其基类 System.Enum、System.ValueType 和 System.Object 继承成员，而这些成员可以是非公共的。

> **JOSEPH ALBAHARI** 这些规则背后的依据是：对于任何构造，其默认的声明可访问性都是使其有用所需的最低可访问性。降低可访问性是有益的，因为它能够促进封装。

> **JESSE LIBERTY** 话虽如此，明确声明可访问性仍是一种良好的编程实践，这会使代码更易于维护。

> **ERIC LIPPERT** “声明的”可访问性与实际的有效可访问性之间存在差异。例如，在声明为 internal 的类中声明为 public 的方法，在大多数实际情况下都是 internal 方法。

> 一个很好的理解方式是认识到，公共类成员只对那些能够访问该类的实体公开。

> **JON SKEET** Eric 的注释有一个值得注意的例外：在 internal（甚至 private）类中重写公共方法时，包括实现接口的情况。许多接口实现都位于 internal 类中，但其他程序集仍可能通过该接口访问这些类的实例。




### 3.5.2 可访问域

成员的*可访问域*由允许访问该成员的程序文本的（可能不相交的）部分组成。为了定义成员的可访问域，如果成员未在类型中声明，则称该成员为*顶层*成员；如果成员在另一类型中声明，则称该成员为*嵌套*成员。此外，程序的*程序文本*定义为该程序所有源文件中包含的全部程序文本，而类型的程序文本定义为该类型的*类型声明*中包含的全部程序文本（可能包括嵌套在该类型中的类型）。

预定义类型（如 `object`、`int` 或 `double`）的可访问域不受限制。

在程序 P 中声明的顶层未绑定类型 T（§4.4.3）的可访问域定义如下：

- 如果 T 的声明可访问性为 `public`，则 T 的可访问域是 P 的程序文本以及任何引用 P 的程序的程序文本。
- 如果 T 的声明可访问性为 `internal`，则 T 的可访问域是 P 的程序文本。

根据这些定义可知，顶层未绑定类型的可访问域始终至少是该类型所声明程序的程序文本。

构造类型 T<A₁, ..., Aₙ> 的可访问域是未绑定泛型类型 T 的可访问域与类型实参 A₁, ..., Aₙ 的可访问域的交集。

在程序 P 中的类型 T 内声明的嵌套成员 M 的可访问域定义如下（注意 M 本身可能是一个类型）：

- 如果 M 的声明可访问性为 `public`，则 M 的可访问域是 T 的可访问域。
- 如果 M 的声明可访问性为 `protected internal`，则令 D 为 P 的程序文本与任何在 P 外部声明的、从 T 派生的类型的程序文本的并集。M 的可访问域是 T 的可访问域与 D 的交集。
- 如果 M 的声明可访问性为 `protected`，则令 D 为 T 的程序文本与任何从 T 派生的类型的程序文本的并集。M 的可访问域是 T 的可访问域与 D 的交集。
- 如果 M 的声明可访问性为 `internal`，则 M 的可访问域是 T 的可访问域与 P 的程序文本的交集。
- 如果 M 的声明可访问性为 `private`，则 M 的可访问域是 T 的程序文本。

根据这些定义可知，嵌套成员的可访问域始终至少是该成员所声明类型的程序文本。此外，成员的可访问域绝不会比该成员所声明类型的可访问域的范围更广。

## 3.5 成员访问

直观地说，当访问类型或成员 **M** 时，将执行以下步骤以确保允许访问：

- 首先，如果 **M** 声明在某个类型中（而不是在编译单元或命名空间中），并且该类型不可访问，则发生编译时错误。
- 然后，如果 **M** 是 public，则允许访问。
- 否则，如果 **M** 是 protected internal，则当访问发生在声明 **M** 的程序内，或发生在从声明 **M** 的类派生的类内并且通过派生类类型进行时（§3.5.3），允许访问。
- 否则，如果 **M** 是 protected，则当访问发生在声明 **M** 的类内，或发生在从声明 **M** 的类派生的类内并且通过派生类类型进行时（§3.5.3），允许访问。
- 否则，如果 **M** 是 internal，则当访问发生在声明 **M** 的程序内时，允许访问。
- 否则，如果 **M** 是 private，则当访问发生在声明 **M** 的类型内时，允许访问。
- 否则，该类型或成员不可访问，并发生编译时错误。

在下面的示例中

```csharp
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

这些类和成员具有以下可访问域：

- A 和 A.X 的可访问域不受限制。
- A.Y、B.X、B.Y、B.C、B.C.X 和 B.C.Y 的可访问域是包含程序的程序文本。
- A.Z 的可访问域是 A 的程序文本。
- B.Z 和 B.D 的可访问域是 B 的程序文本，包括 B.C 和 B.D 的程序文本。
- B.C.Z 的可访问域是 B.C 的程序文本。
- B.D.X 和 B.D.Y 的可访问域是 B 的程序文本，包括 B.C 和 B.D 的程序文本。
- B.D.Z 的可访问域是 B.D 的程序文本。

如示例所示，成员的可访问域绝不会大于包含类型的可访问域。例如，尽管所有 X 成员都具有 public 声明可访问性，但除 A.X 外，所有成员的可访问域都受到包含类型的约束。

> **JOSEPH ALBAHARI** 在 internal 类型中声明 public 成员可能看起来毫无意义，因为该成员的可见性将被限制为 internal。然而，如果将 public 成员修饰符解释为“具有与包含类型相同的可见性”，那么这样做是有意义的。
>
> 判断是否应将 internal 类型的成员声明为 public 还是 internal 时，一个值得提出的好问题是：如果该类型后来提升为 public，我是否也希望此成员变为 public？如果答案是肯定的，就可以主张从一开始就将该成员声明为 public。

> **JESSE LIBERTY** 虽然上述每种情况都有合理的例子，但良好的编程实践强烈倾向于使用最简单、最明显的可访问性，以减少混淆并编写更易维护的代码。我编写过数百个商业上可行的应用程序，只使用了 public、private 和 protected。

如 §3.4 所述，基类的所有成员（实例构造函数、析构函数和静态构造函数除外）都由派生类型继承。这甚至包括基类的私有成员。但是，私有成员的可访问域仅包括声明该成员的类型所对应的程序文本。在下面的示例中

```csharp
class A
{
    int x;
    static void F(B b)
    {
        b.x = 1;    // Ok
    }
}

class B : A
{
    static void F(B b)
    {
        b.x = 1;    // Error: x not accessible
    }
}
```

B 类从 A 类继承私有成员 x。由于该成员是私有的，因此只能在 A 的类体中访问。所以对 b.x 的访问在 A::F 方法中成功，但在 B::F 方法中失败。

> BILL WAGNER 注意，这些不可访问的方法也消除了在 B::F() 上使用 new 修饰符的必要。

### 3.5.3 实例成员的受保护访问

当受保护实例成员在声明它的类的程序文本之外被访问时，以及当受保护内部实例成员在声明它的程序的程序文本之外被访问时，该访问必须发生在从声明该成员的类派生的类声明中。此外，该访问必须通过该派生类类型的实例或由它构造的类类型的实例进行。此限制防止一个派生类访问其他派生类的受保护成员，即使这些成员继承自同一个基类。




> **埃里克·克利珀特** 例如，假设有一个基类 `Animal` 和两个派生类 `Mammal` 与 `Reptile`，并且 `Animal` 有一个受保护的方法 `Feed()`。那么 `Mammal` 代码可以在 `Mammal` 或 `Mammal` 的任意子类（比如 `Tiger`）上调用 `Feed()`。
>
> `Mammal` 代码不能在类型为 `Reptile` 的表达式上调用 `Feed()`，因为 `Mammal` 和 `Reptile` 之间不存在继承关系。
>
> 此外，由于类型为 `Animal` 的表达式在运行时实际上可能是 `Reptile`，`Mammal` 代码也不能在类型为 `Animal` 的表达式上调用 `Feed()`。

设 B 是一个声明了受保护实例成员 M 的基类，D 是一个从 B 派生的类。在 D 的 *类体* 内，对 M 的访问可以采用以下形式之一：

- 形式为 M 的非限定 *类型名* 或 *主表达式*。
- 形式为 E.M 的 *主表达式*，前提是 E 的类型为 T 或从 T 派生的类，其中 T 是类类型 D，或由 D 构造的类类型。
- 形式为 `base.M` 的 *主表达式*。

除这些访问形式外，派生类还可以在 *构造函数初始化器*（§10.11.1）中访问基类的受保护实例构造函数。

> **弗拉基米尔·列舍特尼科夫** 简而言之，其他访问形式都是不允许的。例如，派生类不能在 new 运算符中调用其基类的受保护构造函数：
>
> ```csharp
> class Base
> {
>     protected Base() { }
> }
> 
> class Derived : Base
> {
>     static void Main()
>     {
>         new Base();        // Error CS0122: 'Base.Base()' is
>                            // inaccessible due to its
>                            // protection level
>     }
> }
> ```

在下面的示例中

```
public class A
{
    protected int x;

    static void F(A a, B b)
    {
        a.x = 1;    // Okay
        b.x = 1;    // Okay
    }
}

public class B : A
{
    static void F(A a, B b)
    {
        a.x = 1;    // Error: must access through instance of B
        b.x = 1;    // Okay
    }
}
```

在 A 内，可以通过 A 和 B 的实例访问 x，因为无论哪种情况，访问都通过 A 的实例或从 A 派生的类的实例进行。然而，在 B 内，不能通过 A 的实例访问 x，因为 A 不是从 B 派生的。

在下面的示例中

```
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

对 x 的三个赋值都是允许的，因为它们都通过由泛型类型构造的类类型的实例进行。

> **克里斯·塞尔斯** 为了最小化类或命名空间的表面积，我建议将内容保持为 private/internal，直到证明在更广的作用域中确有必要。在这里，重构是你的好帮手。

> **比尔·瓦格纳** 这些规则的存在是为了允许不同程序集中的组件独立演化。你不应将这些规则纳入常规设计模式。

### 3.5.4 可访问性约束

C# 语言中的若干构造要求某个类型*至少与*某个成员或另一个类型*一样可访问*。如果类型 *T* 的可访问域是成员或类型 *M* 的可访问域的超集，则称类型 *T* 至少与成员或类型 *M* 一样可访问。换句话说，如果在 *M* 可访问的所有上下文中 *T* 都可访问，则 *T* 至少与 *M* 一样可访问。

> **弗拉基米尔·列舍特尼科夫** 就本段而言，只考虑可访问性修饰符。例如，如果一个受保护成员声明在 public sealed 类中，那么该类不能有后代（因此，该成员的可访问域不包括任何后代）这一事实不予考虑。

存在以下可访问性约束：

- 类类型的直接基类必须至少与该类类型本身一样可访问。
- 接口类型的显式基接口必须至少与该接口类型本身一样可访问。
- 委托类型的返回类型和参数类型必须至少与该委托类型本身一样可访问。
- 常量的类型必须至少与该常量本身一样可访问。
- 字段的类型必须至少与该字段本身一样可访问。
- 方法的返回类型和参数类型必须至少与该方法本身一样可访问。
- 属性的类型必须至少与该属性本身一样可访问。
- 事件的类型必须至少与该事件本身一样可访问。
- 索引器的类型和参数类型必须至少与该索引器本身一样可访问。
- 运算符的返回类型和参数类型必须至少与该运算符本身一样可访问。
- 实例构造函数的参数类型必须至少与该实例构造函数本身一样可访问。

在下面的示例中

```
class A {...}
public class B: A {...}
```

B 类会导致编译时错误，因为 A 并不至少与 B 一样可访问。

同样，在下面的示例中

```
class A {...}
public class B
{
    A F() {...}
    internal A G() {...}
    public A H() {...}
}
```

B 中的 H 方法会导致编译时错误，因为返回类型 A 并不至少与该方法本身一样可访问。

## 3.6 签名与重载

方法、实例构造函数、索引器和运算符由其签名来表征：

- 方法的签名由方法名称、类型参数数目，以及每个形参的类型和种类（值、引用或输出）组成，按从左到右的顺序考虑。为此，方法中出现在形参类型中的任何类型参数不按其名称标识，而按其在该方法类型实参列表中的序号位置标识。方法的签名特别不包括返回类型、可为最右侧参数指定的 params 修饰符，或可选类型参数约束。

> **乔恩·斯基特**
>
> 按类型参数数目进行重载的用法很有趣——它也出现在类型层面（例如，考虑 .NET 类型 `System.Nullable` 和 `System.Nullable<T>`）。不考虑约束这一点偶尔会令人恼火。在某些情况下，能够编写以下代码会很方便
>
> ```
> void Process<T>(T reference) where T : class { ... }
> void Process<T>(T value) where T : struct { ... }
> ```
>
> 但这会给一个本来就已经很难推理的领域引入更多复杂性。众所周知，当重载和类型推断相遇时，开发人员的大脑会自发燃烧。

- 实例构造函数的签名由每个形参的类型和种类（值、引用或输出）组成，按从左到右的顺序考虑。实例构造函数的签名特别不包括可为最右侧参数指定的 `params` 修饰符。
- 索引器的签名由每个形参的类型组成，按从左到右的顺序考虑。索引器的签名特别不包括元素类型，也不包括可为最右侧参数指定的 `params` 修饰符。
- 运算符的签名由运算符名称和每个形参的类型组成，按从左到右的顺序考虑。运算符的签名特别不包括结果类型。

签名是类、结构和接口中成员**重载**的启用机制：

- 方法的重载允许类、结构或接口声明多个同名方法，前提是它们的签名在该类、结构或接口中唯一。
- 实例构造函数的重载允许类或结构声明多个实例构造函数，前提是它们的签名在该类或结构中唯一。
- 索引器的重载允许类、结构或接口声明多个索引器，前提是它们的签名在该类、结构或接口中唯一。



**弗拉基米尔·列舍特尼科夫** 索引器签名唯一性要求的一个例外：如果索引器是接口的显式实现，则其签名仅在该接口的显式实现的索引器内检查唯一性：

```csharp
class A : IIndexable
{
    int IIndexable.this[int x]
    {
        get { /* ... */ }
    }

    public int this[int x] // Okay
    {
        get { /* ... */ }
    }
}
```

-   运算符重载允许类或结构声明多个具有相同名称的运算符，前提是它们的签名在该类或结构内是唯一的。

尽管 `out` 和 `ref` 参数修饰符被视为签名的一部分，但同一类型中声明的成员不能仅因 `ref` 和 `out` 的不同而在签名上不同。如果在同一类型中声明两个成员，并且如果将两个方法中所有带 `out` 修饰符的参数都改为 `ref` 修饰符后它们的签名会相同，则发生编译时错误。对于签名匹配的其他目的（例如隐藏或重写），`ref` 和 `out` 被视为签名的一部分，并且彼此不匹配。（此限制是为了让 C# 程序能够轻松转换为在公共语言基础结构 [CLI] 上运行，而 CLI 不提供定义仅在 `ref` 和 `out` 上不同的方法的方式。）

就签名而言，类型 `object` 和 `dynamic` 被视为相同。因此，同一类型中声明的成员不能仅因 `object` 和 `dynamic` 的不同而在签名上不同。

下面的示例展示了一组重载方法声明及其签名。

```csharp
interface ITest
{
    void F();
    void F(int x);                  // F(int)
    void F(ref int x);              // F(ref int)
    void F(out int x);              // F(out int)      error
}
```

```cpp
void F(int x, int y);            // F(int, int)
int  F(string s);                // F(string)
int  F(int x);                   // F(int)        error
void F(string[] a);              // F(string[])
void F(params string[] a);       // F(string[])   error
}
```

请注意，任何 `ref` 和 `out` 参数修饰符（§10.6.1）都是签名的一部分。因此 `F(int)` 和 `F(ref int)` 是唯一签名。但是，`F(ref int)` 和 `F(out int)` 不能在同一接口内声明，因为它们的签名仅因 `ref` 和 `out` 的不同而不同。另外，请注意返回类型和 `params` 修饰符不是签名的一部分，因此不可能仅基于返回类型或包含/排除 `params` 修饰符来进行重载。因此，上面标识的方法 `F(int)` 和 `F(params string[])` 的声明会导致编译时错误。

## 3.7 作用域

名称的*作用域*是程序文本中无需限定名称即可引用该名称所声明实体的区域。作用域可以*嵌套*，内部作用域可以重新声明外部作用域中名称的含义（但是，这并不消除 §3.3 施加的限制，即在嵌套块中不能声明与封闭块中的局部变量同名的局部变量）。然后称外部作用域中的名称在内部作用域所覆盖的程序文本区域中是*隐藏的*，并且只有限定该名称才能访问外部名称。

-   由 *命名空间成员声明*（§9.5）声明且没有封闭 *命名空间声明* 的命名空间成员，其作用域是整个程序文本。
-   由完全限定名为 N 的 *命名空间声明* 中的 *命名空间成员声明* 声明的命名空间成员，其作用域是每个完全限定名为 N 或以 N 后跟句点开头的 *命名空间声明* 的 *命名空间体*。
-   由 *外部别名指令* 定义名称的作用域延伸至其直接包含的编译单元或命名空间体的 *using 指令*、*全局特性* 和 *命名空间成员声明*。一个 *外部别名指令* 不会向基础声明空间贡献任何新成员。换句话说，*外部别名指令* 不是传递的，而只影响它所在的编译单元或命名空间体。
-   由 *using 指令*（§9.4）定义或导入的名称的作用域延伸至该 using 指令所在的 *编译单元* 或 *命名空间体* 的 *命名空间成员声明*。一个 using 指令可以使零个或多个命名空间或类型名称在特定编译单元或命名空间体内可用，但不会向基础声明空间贡献任何新成员。换句话说，using 指令不是传递的，而只影响它所在的编译单元或命名空间体。
-   由类声明（§10.1）上的类型参数列表声明的类型参数的作用域是该类声明的类基、类型参数约束子句和类体。
-   由结构声明（§11.1）上的类型参数列表声明的类型参数的作用域是该结构声明的结构接口、类型参数约束子句和结构体主体。
-   由接口声明（§13.1）上的类型参数列表声明的类型参数的作用域是该接口声明的接口基、类型参数约束子句和接口体。
-   由委托声明（§15.1）上的类型参数列表声明的类型参数的作用域是该委托声明的返回类型、形参列表和类型参数约束子句。
-   由 *类成员声明*（§10.1.6）声明的成员，其作用域是声明所在的 *类体*。此外，类成员的作用域延伸到包含在该成员的 *可访问域*（§3.5.2）中的那些派生类的 *类体*。
-   由 *结构成员声明*（§11.2）声明的成员，其作用域是声明所在的 *结构体主体*。
-   由 *枚举成员声明*（§14.3）声明的成员，其作用域是声明所在的 *枚举体*。
-   在 *方法声明*（§10.6）中声明的参数，其作用域是该 *方法声明* 的 *方法体*。
-   在 *索引器声明*（§10.9）中声明的参数，其作用域是该 *索引器声明* 的 *访问器声明*。
-   在 *运算符声明*（§10.10）中声明的参数，其作用域是该 *运算符声明* 的块。
-   在 *构造函数声明*（§10.11）中声明的参数，其作用域是该 *构造函数声明* 的 *构造函数初始化器* 和块。
-   在 *lambda 表达式*（§7.15）中声明的参数，其作用域是该 *lambda 表达式* 的 *lambda 表达式体*。
-   在 *匿名方法表达式*（§7.15）中声明的参数，其作用域是该 *匿名方法表达式* 的块。
-   在 *带标签语句*（§8.4）中声明的标签，其作用域是声明所在的块。
-   在 *局部变量声明*（§8.5.1）中声明的局部变量，其作用域是声明所在的块。
-   在 switch 语句（§8.7.2）的 *switch 块* 中声明的局部变量，其作用域是 *switch 块*。
-   在 for 语句（§8.8.3）的 *for 初始化器* 中声明的局部变量，其作用域是 *for 初始化器*、*for 条件*、*for 迭代器* 以及该 for 语句的包含语句。
-   在 *局部常量声明*（§8.5.2）中声明的局部常量，其作用域是声明所在的块。在文本位置先于其 *常量声明符* 引用局部常量是编译时错误。
-   作为 foreach 语句、using 语句、lock 语句或查询表达式的一部分声明的变量，其作用域由给定构造的展开确定。

> **杰西·利伯蒂** 这个列表是一个经典、几乎标志性的例子，说明了可能做到的事与值得建议的事之间的区别。作用域，像方法名以及程序中几乎其他所有东西一样，应该尽可能自我揭示且无歧义——但不要过度！

在命名空间、类、结构或枚举成员的作用域内，可以在声明该成员的文本位置之前引用该成员。例如，在

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

中，F 在 i 声明之前引用 i 是有效的。

在局部变量的作用域内，在局部变量的局部变量声明符之前的文本位置引用该局部变量是编译时错误。例如：

```csharp
class A
{
    int i = 0;
```




```
void F()
{
    i = 1;                // Error: use precedes declaration
    int i;
    i = 2;
}
void G()
{
    int j = (j = 1);      // Valid
}
void H()
{
    int a = 1, b = ++a;   // Valid
}
```

在上面的 F 方法中，对 i 的第一次赋值特指不引用在外部作用域中声明的字段。相反，它引用的是局部变量，并且由于它在文本上先于变量的声明而导致编译时错误。在 G 方法中，在 j 的声明的初始化器中使用 j 是有效的，因为该使用并未先于 *local-variable-declarator*。在 H 方法中，后续的 *local-variable-declarator* 正确地引用了在同一 *local-variable-declaration* 中较早的 *local-variable-declarator* 所声明的局部变量。

局部变量的作用域规则旨在保证在块内在表达式上下文中使用的名称的含义始终相同。如果局部变量的作用域仅从其声明延伸到块的末尾，那么在上面的示例中，第一次赋值将赋值给实例变量，而第二次赋值将赋值给局部变量，如果稍后重新排列块的语句，可能会导致编译时错误。

块内名称的含义可能因名称使用上下文而异。在下面的示例中

```
using System;
class A { }
class Test
{
    static void Main()
    {
        string A = "hello, world";
        string s = A;

        Type t = typeof(A);

        Console.WriteLine(s);    // Writes "hello, world"
        Console.WriteLine(t);    // Writes "A"
    }
}
```

## 3. 基本概念

名称 A 在表达式上下文中用于引用局部变量 A，而在类型上下文中用于引用类 A。

## 3.7.1 名称隐藏

实体的作用域通常涵盖比实体声明空间更多的程序文本。特别是，实体的作用域可能包括引入包含同名实体的新声明空间的声明。此类声明会导致原始实体被隐藏。相反，当实体未被隐藏时，称其为可见。

名称隐藏发生在作用域通过嵌套重叠时，也发生在作用域通过继承重叠时。两种隐藏类型的特征在以下各节中描述。

> **JESSE LIBERTY** 我认为名称隐藏始终应被视为错误，因为它使得代码难以维护，而且总是可以避免的。

### 3.7.1.1 通过嵌套隐藏

通过嵌套的名称隐藏可能由于在命名空间内嵌套命名空间或类型而发生，也可能由于在类或结构中嵌套类型而发生，还可能由于参数和局部变量声明而发生。

在下面的示例中

```
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

在 F 方法内，实例变量 i 被局部变量 i 隐藏，但在 G 方法内，i 仍然引用实例变量。

当内部作用域中的名称隐藏外部作用域中的名称时，它会隐藏该名称的所有重载出现。在下面的示例中

```
class Outer
{
    static void F(int i) { }
    static void F(string s) { }
    class Inner
    {
        void G()
        {
            F(2);            // Invokes Outer.Inner.F
            F("Hello");      // Error
        }
        static void F(long l) { }
    }
}
```

调用 F(2) 引用在 Inner 中声明的 F，因为内部声明隐藏了所有外部的 F。对于同样的原因，调用 F("Hello") 会导致编译时错误。

> VLADIMIR RESHETNIKOV 如果嵌套作用域包含与外部作用域成员同名的成员，则外部作用域的成员并不总是被隐藏，原因如下规则：如果成员被调用，则所有不可调用的成员都从集合中移除（参见 §7.3）。

```
class A
{
    static void Foo() { }
    class B
    {
        const int Foo = 1;
        void Bar()
        {
            Foo(); // Okay
        }
    }
}
```

### 3.7.1.2 通过继承隐藏

通过继承的名称隐藏发生在类或结构重新声明从基类继承的名称时。此类型的名称隐藏采用以下形式之一：

- 在类或结构中引入的常量、字段、属性、事件或类型会隐藏基类中同名的所有成员。
- 在类或结构中引入的方法会隐藏基类中同名的所有非方法成员，以及基类中具有相同签名（方法名和参数个数、修饰符和类型）的方法。
- 在类或结构中引入的索引器会隐藏基类中具有相同签名（参数个数和类型）的所有索引器。

运算符声明的规则（§10.10）使得派生类无法声明与基类运算符具有相同签名的运算符。因此运算符永远不会相互隐藏。

与从外部作用域隐藏名称相反，从继承作用域隐藏可访问名称会导致发出警告。在下面的示例中

```
class Base
{
    public void F() { }
}
class Derived : Base
{
    public void F() { }        // Warning: hiding an inherited name
}
```

在 Derived 中声明 F 会导致发出警告。隐藏继承的名称特指不是错误，因为那样会妨碍基类的独立演进。例如，上面的情况可能是因为 Base 的较新版本引入了 F 方法，而该方法在类早期版本中不存在。如果上述情况是错误，则对单独版本化类库中的基类所做的任何更改都可能导致派生类变得无效。

通过使用 new 修饰符可以消除隐藏继承名称引起的警告：

```
class Base
{
    public void F() { }
}
class Derived : Base
{
    new public void F() { }
}
```

new 修饰符表示 Derived 中的 F 是“新的”，并且确实 intended 隐藏继承的成员。

新成员的声明仅在新成员的作用域内隐藏继承的成员。

```
class Base
{
    public static void F() { }
}
class Derived : Base
{
    new private static void F() { }        // Hides Base.F in Derived only
}
class MoreDerived : Derived
{
    static void G() { F(); }               // Invokes Base.F
}
```

在上面的示例中，Derived 中声明的 F 隐藏了从 Base 继承的 F，但由于 Derived 中的新 F 具有私有访问权限，其作用域不延伸到 MoreDerived。因此，MoreDerived.G 中的调用 F() 是有效的，并且将调用 Base.F。

> **CHRIS SELLS** 如果你发现自己使用 new 来隐藏基类上的实例方法，你几乎总是会失望，如果没有其他原因，调用者可以简单地强制转换为基类以获取到“隐藏”的方法。例如：
> 
> ```
> class Base { public void F() { } }
> class Derived : Base { new public void F() { } }
> Derived d = new Derived();
> ((Base)d).F();    // Base.F not so hidden as you would like
> ```
> 你会更开心如果在派生类中为该方法选择一个新名称。

## 3.8 命名空间和类型名称

C# 程序中的多个上下文需要指定 namespace-name 或 type-name。

+   namespace-name:
+     namespace-or-type-name
+   
+   type-name:
+     namespace-or-type-name
+   
+   namespace-or-type-name:
+     identifier type-argument-list_opt
+     namespace-or-type-name . identifier type-argument-list_opt
+     qualified-alias-member

namespace-name 是引用命名空间的 namespace-or-type-name。按照下面所述的解析，namespace-name 的 namespace-or-type-name 必须引用命名空间；否则，会发生编译时错误。namespace-name 中不能存在类型参数（§4.4.1）（只有类型可以具有类型参数）。

type-name 是引用类型的 namespace-or-type-name。按照下面所述的解析，type-name 的 namespace-or-type-name 必须引用类型；否则，会发生编译时错误。

如果 namespace-or-type-name 是 qualified-alias-member，则其含义如 §9.7 中所述。否则，namespace-or-type-name 有四种形式之一：

- I
- I<A₁, ..., Aₖ>
- N.I
- N.I<A₁, ..., Aₖ>

其中 I 是一个标识符，N 是一个 namespace-or-type-name，<A₁, ..., Aₖ> 是一个可选的类型参数列表。当未指定类型参数列表时，将 k 视为零。

namespace-or-type-name 的含义确定如下：

- 如果 namespace-or-type-name 的形式为 I 或形式为 I<A₁, ..., Aₖ>：
  - 如果 k 为零并且 namespace-or-type-name 出现在泛型方法声明（§10.6）内，并且该声明包含名称为 I 的类型参数（§10.1.3），则 namespace-or-type-name 引用该类型参数。
  - 否则，如果 namespace-or-type-name 出现在类型声明内，则对于每个实例类型 T（§10.3.1），从该类型声明的实例类型开始，继续到每个封闭类或结构声明（如果有）的实例类型：
    - 如果 k 为零并且 T 的声明包含名称为 I 的类型参数，则 namespace-or-type-name 引用该类型参数。
    - 否则，如果 namespace-or-type-name 出现在类型声明的主体中，并且 T 或其任何基类型包含具有名称 I 且 k 个类型参数的嵌套可访问类型，则 namespace-or-type-name 引用使用给定类型参数构造的该类型。如果存在多个此类类型，则在更派生的类型中声明的类型被选中。注意，非类型成员（常量、字段、方法、属性、索引器、运算符、实例构造函数、析构函数和静态构造函数）以及类型参数数量不同的类型成员在确定 namespace-or-type-name 的含义时会被忽略。



- 如果前面的步骤未成功，则对于每个命名空间 N，从出现该命名空间或类型名的命名空间开始，继续处理每个封闭命名空间（如果有），直到全局命名空间，按如下步骤进行求值，直到找到实体：
  - 如果 K 为零且 I 是 N 中某个命名空间的名称，则：
    - 如果出现该命名空间或类型名的位置由 N 的命名空间声明所封闭，并且该命名空间声明包含将名称 I 与某个命名空间或类型关联的 extern-alias-directive 或 using-alias-directive，则该命名空间或类型名有歧义，并发生编译时错误。
    - 否则，该命名空间或类型名引用 N 中名为 I 的命名空间。
  - 否则，如果 N 包含一个名称为 I 且具有 K 个类型参数的可访问类型，则：
    - 如果 K 为零且出现该命名空间或类型名的位置由 N 的命名空间声明所封闭，并且该命名空间声明包含将名称 I 与某个命名空间或类型关联的 extern-alias-directive 或 using-alias-directive，则该命名空间或类型名有歧义，并发生编译时错误。
    - 否则，该命名空间或类型名引用用给定类型实参构造的类型。
  - 否则，如果出现该命名空间或类型名的位置由 N 的命名空间声明所封闭：
    - 如果 K 为零且该命名空间声明包含将名称 I 与导入的命名空间或类型关联的 extern-alias-directive 或 using-alias-directive，则该命名空间或类型名引用该命名空间或类型。
    - 否则，如果该命名空间声明的 using-namespace-directives 所导入的命名空间中恰好包含一个名称为 I 且具有 K 个类型参数的类型，则该命名空间或类型名引用用给定类型实参构造的该类型。
    - 否则，如果该命名空间声明的 using-namespace-directives 所导入的命名空间中包含多个名称为 I 且具有 K 个类型参数的类型，则该命名空间或类型名有歧义，并发生错误。
- 否则，该命名空间或类型名未定义，并发生编译时错误。
- 否则，该命名空间或类型名具有 N.I 形式或 N.I<A₁, ..., Aₖ> 形式。首先将 N 解析为命名空间或类型名。如果 N 的解析不成功，则发生编译时错误。否则，N.I 或 N.I<A₁, ..., Aₖ> 按如下方式解析：
  - 如果 K 为零且 N 引用某个命名空间，并且 N 包含名称为 I 的嵌套命名空间，则该命名空间或类型名引用该嵌套命名空间。
  - 否则，如果 N 引用某个命名空间，并且 N 包含一个名称为 I 且具有 K 个类型参数的可访问类型，则该命名空间或类型名引用用给定类型实参构造的该类型。
  - 否则，如果 N 引用某个（可能是构造的）类或结构类型，并且 N 或其任何基类包含一个名称为 I 且具有 K 个类型参数的嵌套可访问类型，则该命名空间或类型名引用用给定类型实参构造的该类型。如果有多个这样的类型，则选择在更派生类型中声明的类型。注意，如果在解析 N 的基类规范时确定 N.I 的含义，则 N 的直接基类被视为 object（§10.1.4.1）。
  - 否则，N.I 是无效的命名空间或类型名，并发生编译时错误。

> **VLADIMIR RESHETNIKOV** 该算法与简单名称的相应算法不同（尽管相似）（见 §7.6.2）。这意味着在人为构造的情况下，同一标识符在类型名和简单名称的上下文中可能具有不同含义：

```csharp
class T
{
    public const int X = 1;
}
class C
{
    void Foo<T>(int x = T.X /* global::T */, T y = default(T) /* type parameter */) { }
}
```

仅当以下情况时，才允许命名空间或类型名引用静态类（§10.1.1.3）：

- 命名空间或类型名是 T.I 形式的命名空间或类型名中的 T，或者
- 命名空间或类型名是 typeof(T) 形式的 typeof 表达式（§7.5.11）中的 T。

### 3.8.1 完全限定名

每个命名空间和类型都有一个完全限定名，它在所有其他命名空间或类型中唯一标识该命名空间或类型。命名空间或类型 N 的完全限定名按如下方式确定：

- 如果 N 是全局命名空间的成员，则其完全限定名为 N。
- 否则，其完全限定名为 S::N，其中 S 是声明 N 的命名空间或类型的完全限定名。

换言之，N 的完全限定名是从全局命名空间开始、通向 N 的标识符的完整分层路径。由于命名空间或类型的每个成员都必须具有唯一名称，因此命名空间或类型的完全限定名始终是唯一的。

下面的示例展示了若干命名空间和类型声明及其关联的完全限定名。

```csharp
class A { }                // A
namespace X                // X
{
    class B                // X.B
    {
        class C { }        // X.B.C
    }
    namespace Y            // X.Y
    {
        class D { }        // X.Y.D
    }
}
namespace X.Y             // X.Y
{
    class E { }            // X.Y.E
}
```

> **JOSEPH ALBAHARI** 如果完全限定名与部分限定名或非限定名（例如嵌套的可访问类型）冲突，则后者胜出。在名称前加上 global:: 会强制完全限定名胜出（§9.7）。在人工编写的代码中发生这种冲突的可能性很小；然而，在机器编写的代码中，可能性更大。因此，设计工具和 IDE 中的一些代码生成器会在所有完全限定类型名之前生成 global:: 前缀，以消除任何冲突的可能性。

## 3.9 自动内存管理

C# 采用自动内存管理，使开发者无需手动分配和释放对象占用的内存。自动内存管理策略由垃圾回收器实现。对象的内存管理生命周期如下：

1. 创建对象时，为其分配内存，运行构造函数，并且该对象被视为存活。

2. 如果对象或其任何部分无法通过执行的任何可能延续（析构函数的运行除外）访问，则该对象被视为不再使用，并成为可销毁的。C# 编译器和垃圾回收器可以选择分析代码，以确定将来可能使用对对象的哪些引用。例如，如果作用域内的局部变量是对象唯一现存的引用，但在从过程中当前执行点开始的任何可能执行延续中都从未引用该局部变量，则垃圾回收器可以（但不必）将该对象视为不再使用。

    > **CHRISTIAN NAGEL** 从析构函数中，C# 编译器创建代码以重写基类的 `Finalize` 方法。重写 `Finalize` 方法也意味着对象实例化会有开销，并使对象存活更久，直到终结运行完成。使用 C++/CLI 时，从析构函数生成的代码实现 `IDisposable` 接口，这更适合确定性清理。
    >
    > **JON SKEET** 对象符合销毁条件的时间点比你预期的更早。特别是，对象析构函数可能在另一个线程仍在同一对象“中”执行实例方法时运行——只要该实例方法在当前执行点之后的任何可能代码路径中都不引用任何实例变量。
    >
    > 幸运的是，这种行为只会在具有析构函数的类型中引起明显问题，而自 SafeHandle 出现以来，这类类型在 .NET 代码中相对少见。

3. 一旦对象符合销毁条件，在某个未指定的稍后时间，将运行该对象的析构函数（§10.13）（如果有）。除非被显式调用覆盖，否则该对象的析构函数只运行一次。




> **克里斯蒂安·纳格尔**  “析构会在某个未指定的稍后时间被调用……”
> 
> 创建析构函数时，通常最好也实现 IDisposable 接口。借助 IDisposable 接口，当对象不再需要时，调用方有机会提前调用清理代码。

> **克里斯蒂安·纳格尔**  要多次调用析构函数，`GC.ReRegisterForFinalize` 会让对象保持存活，并允许析构函数再被调用一次。与其采用这种做法，不如改变应用程序架构，这可能更值得。

- 4. 对象的析构函数运行后，如果该对象或其任何部分无法被任何可能的后续执行（包括析构函数的运行）访问，则该对象被视为不可访问，并成为可回收对象。
- 5. 最后，在对象成为可回收对象之后的某个时间，垃圾回收器会释放与该对象关联的内存。

垃圾回收器维护有关对象使用情况的信息，并利用这些信息做出内存管理决策，例如在内存中的何处放置新创建的对象、何时重新定位对象，以及对象何时不再被使用或不可访问。

与假定存在垃圾回收器的其他语言一样，C# 的设计使垃圾回收器可以实现各种内存管理策略。例如，C# 不要求析构函数必须运行，也不要求对象一成为可回收对象就立即被回收，也不要求析构函数按任何特定顺序或在任何特定线程上运行。

垃圾回收器的行为在某种程度上可以通过类 `System.GC` 上的静态方法来控制。该类可用于请求发生一次回收、运行（或不运行）析构函数，等等。

> **埃里克·利珀特**  使用这些静态方法来控制垃圾回收器的行为几乎从来都不是好主意。在生产代码中，垃圾回收器很可能比你的程序更清楚什么时候适合执行回收。在运行时显式调整垃圾回收器的行为，通常应仅限于诸如为测试目的强制进行回收之类的用途。

## 3. 基本概念

由于垃圾回收器在决定何时回收对象和运行析构函数方面拥有很大自由度，符合规范的实现可能产生与以下代码所示不同的输出。该程序

```
    using System;

    class A
    {
        ~A()
        {
            Console.WriteLine("Destruct instance of A");
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
            Console.WriteLine("Destruct instance of B");
        }
    }

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

创建类 A 的一个实例和类 B 的一个实例。当变量 b 被赋值为 null 时，这些对象就成为可进行垃圾回收的对象，因为在此之后，任何用户编写的代码都不可能访问它们。输出可以是以下任一形式：

```
    Destruct instance of A
    Destruct instance of B
```

或

```
    Destruct instance of B
    Destruct instance of A
```

因为该语言对对象被垃圾回收的顺序没有任何约束。

在微妙的情况下，“可销毁”与“可回收”之间的区别可能很重要。例如：

```csharp
using System;

class A
{
    ~A() {
        Console.WriteLine("Destruct instance of A");
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
        Console.WriteLine("Destruct instance of B");
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

        // A and B now eligible for destruction
        GC.Collect();
        GC.WaitForPendingFinalizers();

        // B now eligible for collection, but A is not
        if (RefA != null)
            Console.WriteLine("RefA is not null");
    }
}
```

在上面的程序中，如果垃圾回收器选择先运行 A 的析构函数再运行 B 的析构函数，那么该程序的输出可能是

```text
Destruct instance of A
Destruct instance of B
A.F
RefA is not null
```

请注意，尽管 A 的实例当时未被使用，且 A 的析构函数已运行，A 的方法（在此例中为 F）仍然可能从另一个析构函数中被调用。另外请注意，运行析构函数可能导致对象再次可从主程序中使用。在此例中，运行 B 的析构函数导致先前未被使用的 A 实例可通过活动引用 Test.RefA 访问。调用 WaitForPendingFinalizers 之后，B 的实例可回收，但 A 的实例不可回收，因为有引用 Test.RefA。

为避免混淆和意外行为，通常最好让析构函数仅清理存储在其对象自身字段中的数据，而不对引用对象或静态字段执行任何操作。

> **埃里克·利珀特**  更好的做法是，让析构函数只清理包含表示非托管对象（例如操作系统句柄）的数据的字段。由于你不知道析构函数将在哪个线程上运行或何时运行，因此析构函数尽可能少产生副作用尤为重要。
> 
> 示例中对 `Console.WriteLine` 的调用显然违反了“只做清理、不执行其他操作”这一良好建议。此代码仅作为教学辅助。真实生产代码的析构函数绝不应尝试执行任何具有复杂副作用的操作，例如控制台输出。

使用析构函数的替代方案是让类实现 `System.IDisposable` 接口。这允许对象的客户端决定何时释放对象的资源，通常通过在 using 语句（§8.13）中将该对象作为资源访问来实现。

> **布拉德·艾布拉姆斯**  十有八九，使用 `GC.Collect()` 是个错误。它通常表明正在拼凑一个糟糕的设计。垃圾回收器就像保时捷一样，是精密调校的仪器。正如你不会开着新保时捷玩碰碰车一样，通常也应避免干扰垃圾回收器的算法。垃圾回收器旨在不引人注意地在正确时机介入，并回收最重要的未使用内存。用 `GC.Collect()` 调用去踢它可能会打乱平衡和调校。在采用此解决方案之前，花几分钟弄清为什么需要它。你是否已释放所有实例？你是否在可以释放的地方丢弃了引用？你是否在正确的位置使用了弱引用？

> > **克日什托夫·茨瓦利纳** 有些人将现代基于虚拟机的系统的性能问题归因于它们使用了垃圾回收。事实上，现代垃圾回收器效率很高，已经很少有软件会因垃圾回收器本身的性能而出现问题。最大的性能罪魁祸首是应用程序的过度工程化，遗憾的是，许多框架库也是如此。

> > **克里斯·塞尔斯** 在通常使用 .NET 构建的现代业务系统中，垃圾回收提供了令人惊叹的健壮性。直到现在，我们才开始在实时应用（例如游戏（如 Xbox 的 XNA）和 Windows Phone 7 平台）中使用托管代码，因此仔细考虑垃圾回收器的行为才变得重要。即使在这些情况下，高效设计也更多关乎在卡顿开始之前预分配资源，而不是直接乱动垃圾回收器。

> > **克里斯蒂安·纳格尔** 为再次强调克日什托夫提出的观点，关于垃圾回收器性能的讨论通常类似于多年前将 C 代码与汇编代码进行比较的讨论，或若干年后人们怀疑 C++ 性能不如 C 时的讨论。当然，汇编代码和 C 仍有其用武之地，但大多数应用程序对托管运行时感到满意。

> > **比尔·瓦格纳** 总的来说，这些注释指出，在析构函数的上下文中，你通常的假设中很少有仍然成立。成员变量可能已经运行过其析构函数。析构函数在不同线程上被调用，因此线程本地存储可能无效。析构函数由系统调用，因此你的应用程序不会看到析构函数通过异常报告的错误。你编写析构函数时需要多么防御性，这一点再怎么强调也不为过。幸运的是，很少需要它们。

### 3.10 执行顺序

C# 程序的执行过程会确保每个执行线程的副作用在关键执行点得以保留。*副作用*定义为对 volatile 字段的读取或写入、对非 volatile 变量的写入、对外部资源的写入以及引发异常。必须保留这些副作用顺序的关键执行点包括：对 volatile 字段的引用（§10.5.3）、lock 语句（§8.12）以及线程



## 3. 基本概念

创建和终止。执行环境可以自由更改 C# 程序的执行顺序，但须遵守以下约束：

- 执行线程内的数据依赖性得到保留。也就是说，每个变量的值是按所有语句在原始程序顺序中执行的方式计算的。
- 初始化排序规则得到保留（§10.5.4 和 §10.5.5）。
- 关于易失性读写（§10.5.3），副作用的顺序得到保留。此外，如果执行环境能够推断出表达式的值未被使用且不会产生所需的副作用（包括调用方法或访问易失性字段引起的任何副作用），则无需计算表达式的一部分。当程序执行被异步事件（如另一线程抛出的异常）中断时，不能保证可观察的副作用会以原始程序顺序可见。

# 4. 类型

C# 语言的类型分为两个主要类别：*值类型* 和 *引用类型*。值类型和引用类型都可能是 *泛型类型*，它们接受一个或多个 *类型参数*。类型参数可以指定值类型和引用类型。

```
type:
    value-type
    reference-type
    type-parameter
```

第三类类型，指针，仅在不安全代码中可用。有关此问题将在 §18.2 中进一步讨论。

值类型与引用类型的不同之处在于，值类型变量直接包含其数据，而引用类型变量存储对其数据的 *引用*，后者称为 *对象*。使用引用类型，两个变量可能引用同一个对象，因此对一个变量的操作可能会影响另一个变量引用的对象。使用值类型，每个变量都有自己的数据副本，因此一个变量上的操作不可能影响另一个变量。

C# 的类型系统是统一的，使得 *任何类型的值都可以被视为对象*。C# 中的每个类型都直接或间接派生自 `object` 类类型，而 `object` 是所有类型的最终基类。引用类型的值只需将值视为类型 `object` 即可被视为对象。值类型的值则通过执行装箱和拆箱操作（§4.3）被视为对象。

> **ERIC LIPPERT** 我们通常不会认为接口类型或与类型参数关联的类型本身具有“基类”。本文讨论的要点是，每个具体对象——无论在编译时如何处理它——在运行时都可以被视为 object 的实例。

### 4.1 值类型

值类型要么是结构体类型，要么是枚举类型。C# 提供了一组预定义的结构体类型，称为 *简单类型*。简单类型通过保留字来标识。

```
value-type:
    struct-type
    enum-type

struct-type:
    type-name
    simple-type
    nullable-type

simple-type:
    numeric-type
    bool

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

floating-point-type:
    float
    double

nullable-type:
    non-nullable-value-type ?

non-nullable-value-type:
    type

enum-type:
    type-name
```

与引用类型变量不同，值类型变量仅在值类型为可空类型时才能包含值 `null`。对于每个不可空值类型，都存在一个对应的可空值类型，表示相同的取值集合加上值 `null`。

向值类型变量赋值会创建所赋值的 *副本*。这与向引用类型变量赋值不同，后者复制引用但不复制引用所标识的对象。

### 4.1.1 System.ValueType 类型

所有值类型都隐式继承自类 `System.ValueType`，后者又继承自类 `object`。任何类型都不能派生自值类型，因此值类型被隐式密封（§10.1.2）。

请注意，`System.ValueType` 本身并不是 *值类型*。而是所有 *值类型* 自动派生的 *类类型*。

> **ERIC LIPPERT** 这个观点经常让新手感到困惑。我经常被问到，“但值类型如何可能派生自引用类型？” 我认为这种困惑源于对“派生自”含义的误解。派生并不意味着基类型的位布局在派生类型的位布局中某处存在。相反，它仅仅意味着存在某种机制，可以从派生类型访问基类型的成员。

### 4.1.2 默认构造函数

所有值类型都隐式声明一个名为 *默认构造函数* 的公共无参数实例构造函数。默认构造函数返回一个零初始化的实例，称为该值类型的 *默认值*：

- 对于所有 *简单类型*，默认值是由全零位模式产生的值：
  - 对于 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 和 `ulong`，默认值是 `0`。
  - 对于 `char`，默认值是 `'\x0000'`。
  - 对于 `float`，默认值是 `0.0f`。
  - 对于 `double`，默认值是 `0.0d`。
  - 对于 `decimal`，默认值是 `0.0m`。
  - 对于 `bool`，默认值是 `false`。
- 对于枚举类型 E，默认值是 0，转换为类型 E。
- 对于结构体类型，默认值是通过将所有值类型字段设置为其默认值并将所有引用类型字段设置为 null 而产生的值。

> VLADIMIR RESHETNIKOV 显然，此处的措辞“所有字段”仅指实例字段（不是静态字段）。如果存在，它还包括类似字段的实例事件。

- 对于可空类型，默认值是一个 HasValue 属性为 false 且 Value 属性未定义 的实例。默认值也称为可空类型的空值。

像其他任何实例构造函数一样，值类型的默认构造函数使用 new 运算符调用。出于效率原因，此要求并不意味着实现实际生成构造函数调用。在下面的示例中，变量 i 和 j 都被初始化为零。

```csharp
class A
{
    void F() {
        int i = 0;
        int j = new int();
    }
}
```

由于每个值类型都隐式具有公共无参数实例构造函数，因此结构体类型不能包含无参数构造函数的显式声明。然而，结构体类型允许声明带参数的实例构造函数（§11.3.8）。

> ERIC LIPPERT 获取类型的默认值另一种好方法是使用 default(type) 表达式。

> JON SKEET 这是一个 C# 语言和底层平台可能有不同想法的例子之一。如果你询问 .NET 平台关于值类型的构造函数，通常找不到无参数的构造函数。相反，.NET 有一条特定的指令用于初始化值类型的默认值。通常这些小的阻抗不匹配对开发人员没有影响，但了解它们是可能的——并且它们并不代表任何规范的缺陷——是很好的。

### 4.1.3 结构体类型

结构体类型是一种值类型，可以声明常量、字段、方法、属性、索引器、运算符、实例构造函数、静态构造函数和嵌套类型。结构体类型的声明在 §11.1 中描述。

### 4.1.4 简单类型

C# 提供了一组预定义的结构体类型，称为 *简单类型*。简单类型通过保留字标识，但这些保留字只是 System 命名空间中预定义结构体类型的别名，如下表所述。

| 保留字 | 别名类型 |
| --- | --- |
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

由于简单类型是结构体类型的别名，每个简单类型都有成员。例如，int 具有 System.Int32 声明的成员和从 System.Object 继承的成员，并且以下语句是允许的：

```csharp
int i = int.MaxValue;        // System.Int32.MaxValue constant
string s = i.ToString();     // System.Int32.ToString() instance method
string t = 123.ToString();   // System.Int32.ToString() instance method
```



简单类型与其他结构类型的区别在于，它们允许某些附加操作：

- 大多数简单类型允许通过编写*字面量*（§2.4.4）来创建值。例如，123 是 int 类型的字面量，'a' 是 char 类型的字面量。C# 通常不提供结构类型的字面量，其他结构类型的非默认值最终总是通过这些结构类型的实例构造函数创建。

> **ERIC LIPPERT**  “大多数简单类型”这一短语中的“大多数”指的是这样一个事实：某些简单类型（如 short）没有字面量形式。实际上，任何小到足以放入 short 的整数字面量在作为 short 使用时都会隐式转换为 short，因此从这个意义上说，所有简单类型都有字面量值。
>
> 简单类型有一小部分可能值没有字面量形式。例如，浮点类型的 NaN（非数字）值就没有字面量形式。

- 当表达式的操作数都是简单类型常量时，编译器可以在编译时计算该表达式。这样的表达式称为*常量表达式*（§7.19）。涉及其他结构类型所定义运算符的表达式不被视为常量表达式。

> **VLADIMIR RESHETNIKOV**  这不仅仅是“可能”：编译器总是会在编译时完全计算*常量表达式*。

- 通过 const 声明，可以声明简单类型的常量（§10.4）。不能有其它结构类型的常量，但静态只读字段提供了类似效果。

- 涉及简单类型的转换可以参与其他结构类型所定义的转换运算符的计算，但用户定义的转换运算符永远不能参与另一个用户定义运算符的计算（§6.4.3）。

> **JOSEPH ALBAHARI**  简单类型还提供了一种方式，使编译器能够利用 IL（并最终利用处理器）对整数值和浮点值计算的直接支持。这种方案允许对具有处理器支持的简单类型（通常是 float、double 和整型）进行算术运算时以本机速度运行。

## 4.1.5 整型

C# 支持九种整型：sbyte、byte、short、ushort、int、uint、long、ulong 和 char。整型具有以下大小和值范围：

- sbyte 类型表示有符号 8 位整数，值介于 −128 和 127 之间。
- byte 类型表示无符号 8 位整数，值介于 0 和 255 之间。
- short 类型表示有符号 16 位整数，值介于 −32768 和 32767 之间。
- ushort 类型表示无符号 16 位整数，值介于 0 和 65535 之间。
- int 类型表示有符号 32 位整数，值介于 −2147483648 和 2147483647 之间。
- uint 类型表示无符号 32 位整数，值介于 0 和 4294967295 之间。
- long 类型表示有符号 64 位整数，值介于 −9223372036854775808 和 9223372036854775807 之间。
- ulong 类型表示无符号 64 位整数，值介于 0 和 18446744073709551615 之间。
- char 类型表示无符号 16 位整数，值介于 0 和 65535 之间。char 类型的可能值集合对应于 Unicode 字符集。尽管 char 与 ushort 具有相同的表示形式，但并非所有允许对其中一种类型执行的操作都允许对另一种类型执行。

> **JESSE LIBERTY**  我必须承认，凭借现代 PC 的强大能力，以及程序员时间相对于内存成本的更高代价，我倾向于对几乎任何整型（非小数）值使用 int，对任何小数值使用 double。其余类型我几乎都忽略。

整型的一元和二元运算符始终以有符号 32 位精度、无符号 32 位精度、有符号 64 位精度或无符号 64 位精度运行：

- 对于一元 + 和 ~ 运算符，操作数转换为类型 T，其中 T 是 int、uint、long 和 ulong 中第一个能完全表示操作数所有可能值的类型。然后使用类型 T 的精度执行运算，结果的类型为 T。
- 对于一元 − 运算符，操作数转换为类型 T，其中 T 是 int 和 long 中第一个能完全表示操作数所有可能值的类型。然后使用类型 T 的精度执行运算，结果的类型为 T。一元 − 运算符不能应用于 ulong 类型的操作数。
- 对于二元 +、-、*、/、%、&、^、|、==、!=、>、<、>= 和 <= 运算符，操作数转换为类型 T，其中 T 是 int、uint、long 和 ulong 中第一个能完全表示两个操作数所有可能值的类型。然后使用类型 T 的精度执行运算，结果的类型为 T（关系运算符为 bool）。对于二元运算符，不允许一个操作数为 long 类型而另一个为 ulong 类型。
- 对于二元 << 和 >> 运算符，左操作数转换为类型 T，其中 T 是 int、uint、long 和 ulong 中第一个能完全表示操作数所有可能值的类型。然后使用类型 T 的精度执行运算，结果的类型为 T。

char 类型被归类为整型，但它与其他整型类型有两个不同之处：

- 不存在从其他类型到 char 类型的隐式转换。特别是，即使 sbyte、byte 和 ushort 类型的值范围可以完全用 char 类型表示，也不存在从 sbyte、byte 或 ushort 到 char 的隐式转换。
- char 类型的常量必须写为字符字面量，或写为整数字面量与到 char 类型的强制转换的组合。例如，(char)10 与 '\x000A' 相同。

checked 和 unchecked 运算符及语句用于控制整型算术运算和转换的溢出检查（§7.6.12）。在 checked 上下文中，溢出会产生编译时错误或导致抛出 System.OverflowException。在 unchecked 上下文中，溢出被忽略，任何不适合目标类型的高位都会被丢弃。

## 4.1.6 浮点类型

C# 支持两种浮点类型：float 和 double。float 和 double 类型分别使用 32 位单精度和 64 位双精度 IEEE 754 格式表示，提供以下值集合：

- 正零和负零。在大多数情况下，正零和负零作为简单值零的行为相同，但某些运算会区分二者（§7.8.2）。

> **VLADIMIR RESHETNIKOV**  请注意，值类型中 Equals 方法的默认实现有时会使用按位比较来提高性能。如果你的值类型的两个实例的字段分别包含正零和负零，它们比较起来可能不相等。你可以重写 Equals 方法以更改默认行为。

```csharp
using System;

struct S
{
    double X;

    static void Main()
    {
        var a = new S { X = 0.0 };
        var b = new S { X = -0.0 };
        Console.WriteLine(a.X.Equals(b.X)); // True
        Console.WriteLine(a.Equals(b)); // False
    }
}
```

> **PETER SESTOFT**  关于负零的一些困惑可能源于以下事实：当前 C# 实现以相同方式打印正零和负零，即 0.0，而且似乎没有任何格式参数组合会影响该显示。虽然这样做很可能是出于好意，但很不幸。要显示负零，你必须求助于像下面这样看起来奇怪的代码；它能工作是因为 1/(-0.0) = -Infinity < 0：

```csharp
public static string DoubleToString(double d) {
    if (d == 0.0 && 1/d < 0)
        return "-0.0";
    else
        return d.ToString();
}
```

- 正无穷和负无穷。无穷由诸如非零数除以零之类的运算产生。例如，1.0 / 0.0 产生正无穷，-1.0 / 0.0 产生负无穷。
- *非数字*值，通常缩写为 NaN。NaN 由无效的浮点运算产生，例如零除以零。

> **PETER SESTOFT**  存在大量不同的 NaN，每个都有不同的“载荷”。参见 §7.8.1 的注释。




- 形如 s × m × 2^e 的非零值有限集合；其中 s 为 1 或 −1，m 和 e 由具体的浮点类型决定：对于 float，0 < m < 2^24 且 −149 ≤ e ≤ 104；对于 double，0 < m < 2^53 且 −1075 ≤ e ≤ 970。非规格化浮点数被视为有效的非零值。

float 类型可表示约从 1.5 × 10^−45 到 3.4 × 10^38 的值，精度为 7 位数字。

double 类型可表示约从 5.0 × 10^−324 到 1.7 × 10^308 的值，精度为 15 或 16 位数字。

如果二元运算符的一个操作数是浮点类型，则另一个操作数必须是整型或浮点类型，并且该运算按如下方式求值：

- 如果一个操作数是整型，则该操作数转换为另一个操作数的浮点类型。
- 然后，如果任一操作数是 double 类型，则将另一个操作数转换为 double，使用至少 double 范围和精度执行运算，结果类型为 double（关系运算符则为 bool）。
- 否则，使用至少 float 范围和精度执行运算，结果类型为 float（关系运算符则为 bool）。

浮点运算符（包括赋值运算符）从不产生异常。相反，在异常情况下，浮点运算会产生零、无穷大或 NaN，如下所述：

- 如果浮点运算的结果对于目标格式而言太小，则运算结果变为正零或负零。
- 如果浮点运算的结果对于目标格式而言太大，则运算结果变为正无穷大或负无穷大。
- 如果浮点运算无效，则运算结果变为 NaN。
- 如果浮点运算的一个或两个操作数为 NaN，则运算结果变为 NaN。

浮点运算可以以高于该运算结果类型的精度执行。例如，某些硬件架构支持范围与精度都大于 double 类型的“扩展”或“long double”浮点类型，并隐式使用这种更高精度类型执行所有浮点运算。只有付出过高的性能代价，才能使此类硬件架构以较低精度执行浮点运算。C# 并不要求实现同时牺牲性能和精度，而是允许对所有浮点运算使用更高精度类型。除了提供更精确的结果外，这很少产生任何可测量的影响。然而，在形如 x * y / z 的表达式中，乘法产生的结果超出 double 范围，但随后的除法将临时结果带回 double 范围；该表达式以更高范围格式求值这一事实，可能导致产生有限结果而不是无穷大。

> JOSEPH ALBAHARI NaN 有时用于表示特殊值。在 Microsoft 的 Windows Presentation Foundation 中，double.NaN 表示值为“自动”的测量值。表示此类值的另一种方式是使用可空类型；还有一种方式是使用自定义结构，该结构包装数值类型并添加另一个字段。

## 4.1.7 decimal 类型

decimal 类型是适用于财务和货币计算的 128 位数据类型。decimal 类型可表示从 1.0 × 10⁻²⁸ 到约 7.9 × 10²⁸ 的值，具有 28 或 29 位有效数字。

decimal 类型的值有限集合的形式为 (−1)ˢ × c × 10ᵉ，其中符号 s 为 0 或 1，系数 c 满足 0 ≤ c < 2⁹⁶，标度 e 满足 0 ≤ e ≤ 28。decimal 类型不支持带符号零、无穷大或 NaN。decimal 表示为按 10 的幂缩放的 96 位整数。对于绝对值小于 1.0m 的 decimal，其值精确到小数点后第 28 位，但不会更精确。对于绝对值大于或等于 1.0m 的 decimal，其值精确到 28 或 29 位数字。与 float 和 double 数据类型不同，像 0.1 这样的十进制小数可以在 decimal 表示中精确表示。在 float 和 double 表示中，此类数字通常是无限小数，使这些表示更容易出现舍入误差。

> PETER SESTOFT IEEE 754-2008 标准描述了一种称为 decimal128 的十进制浮点类型。它类似于此处描述的 decimal 类型，但在相同的 128 位内具有强大得多的能力。它具有 34 位有效十进制数字，范围从 10⁻⁶¹⁴³ 到 10⁶¹⁴⁴，并支持 NaN。它由 IBM UK 的 Mike Cowlishaw 设计。由于它在所有方面扩展了当前的 decimal，因此 C# 在未来某个版本中改用 IEEE decimal128 似乎是可行的。

如果二元运算符的一个操作数是 decimal 类型，则另一个操作数必须是整型或 decimal 类型。如果存在整型操作数，则在执行运算前将其转换为 decimal。

> BILL WAGNER 不能混合使用 decimal 和浮点类型（float、double）。这条规则存在的原因是，在这些类型之间混合计算会丢失精度。混合 decimal 和浮点类型时，必须应用显式转换。

对 decimal 类型值进行运算的结果，相当于先计算精确结果（按每个运算符的定义保留标度），然后进行舍入以适合表示形式。结果会舍入到最接近的可表示值；当结果与两个可表示值同样接近时，则舍入到最低有效数字位为偶数的值（这称为“银行家舍入”）。零结果始终符号为 0、标度为 0。

> ERIC LIPPERT 这种方法有一个吸引人的特性：当两种可能值之间出现“平局”时，它通常比总是向下或向上舍入的方法引入的偏差更小。
> 
> 奇怪的是，尽管有这样一个绰号，但几乎没有证据表明这种舍入方法曾在银行业中广泛使用。

如果 decimal 算术运算产生的结果绝对值小于或等于 5 × 10^−28，则运算结果变为零。如果 decimal 算术运算产生的结果对于 decimal 格式而言太大，则抛出 System.OverflowException。

decimal 类型比浮点类型具有更高的精度，但范围更小。因此，从浮点类型转换为 decimal 可能产生溢出异常，而从 decimal 转换为浮点类型可能导致精度损失。由于这些原因，浮点类型与 decimal 之间不存在隐式转换；如果没有显式强制转换，就不可能在同一个表达式中混合使用浮点和 decimal 操作数。

> ERIC LIPPERT C# 不支持 Visual Basic 6 用户和其他基于 OLE 自动化的编程语言用户所熟悉的 Currency 数据类型。由于 decimal 比 Currency 具有更大的范围和更高的精度，因此用 Currency 能做的任何事情，用 decimal 也能同样做好。

## 4.1.8 bool 类型

bool 类型表示布尔逻辑量。bool 类型的可能值为 true 和 false。

bool 与其他类型之间不存在标准转换。特别地，bool 类型与整型截然不同且相互分离；bool 值不能代替整型值使用，反之亦然。

在 C 和 C++ 语言中，零值整型或浮点值，或空指针，可以转换为布尔值 false；非零整型或浮点值，或非空指针，可以转换为布尔值 true。在 C# 中，此类转换通过将整型或浮点值与零进行显式比较，或将对象引用与 null 进行显式比较来完成。

> **CHRIS SELLS** 非 bool 值无法转换为 bool，这最常在我进行 null 比较时带来麻烦。例如：
> 
> ```csharp
> object obj = null;
> if (obj) { ... } // Okay in C/C++, error in C#
> if (obj != null) { ... } // Okay in C/C++/C#
> ```

## 4.1.9 枚举类型

枚举类型是带命名常量的独特类型。每个枚举类型都有一个基础类型，必须为 byte、sbyte、short、ushort、int、uint、long 或 ulong。枚举类型的值集合与基础类型的值集合相同。枚举类型的值不限于命名常量的值。枚举类型通过枚举声明（§14.1）定义。

> **ERIC LIPPERT** 这是一个重要点：没有什么能阻止你将不在枚举类型中的值放入该类型的变量。不要依赖语言或运行时环境来验证枚举类型的实例是否在你预期的范围内。

> **VLADIMIR RESHETNIKOV** CLR 还支持将 char 作为枚举的基础类型。如果你在应用程序中碰巧引用了包含此类类型的程序集，C# 编译器将不会把该类型识别为枚举，并且不会允许你例如将其转换为整型或从整型转换。

## 4.1.10 可空类型

可空类型可以表示其基础类型的所有值，外加一个额外的 null 值。可空类型写作 T?，其中 T 是基础类型。此语法是 System.Nullable<T> 的简写，两种形式可以互换使用。



相反，不可为 null 的值类型是除 System.Nullable<T> 及其简写 T?（对于任何 T）之外的任何值类型，再加上被约束为不可为 null 的值类型的任何类型参数（即任何具有 struct 约束的类型参数）。System.Nullable<T> 类型指定了 T 的值类型约束（§10.1.5），这意味着可为 null 的类型的底层类型可以是任何不可为 null 的值类型。可为 null 的类型的底层类型不能是可为 null 的类型或引用类型。例如，int?? 和 string? 是无效类型。

可为 null 的类型 T? 的实例有两个公共只读属性：

- 一个类型为 bool 的 HasValue 属性
- 一个类型为 T 的 Value 属性

HasValue 为 true 的实例称为非 null。非 null 实例包含一个已知值，Value 返回该值。

HasValue 为 false 的实例称为 null。null 实例具有未定义的值。尝试读取 null 实例的 Value 会导致引发 System.InvalidOperationException。访问可为 null 实例的 Value 属性的过程称为解包。

除了默认构造函数之外，每个可为 null 的类型 T? 都有一个接受类型为 T 的单个参数的公共构造函数。给定类型为 T 的值 x，形式为

```
new T?(x)
```

的构造函数调用会创建 T? 的非 null 实例，其 Value 属性为 x。为给定值创建可为 null 类型的非 null 实例的过程称为包装。

存在从 null 字面量到 T? 的隐式转换（§6.1.5），以及从 T 到 T? 的隐式转换（§6.1.4）。

## 4.2 引用类型

引用类型是类类型、接口类型、数组类型或委托类型。

```
reference-type:
  class-type
  interface-type
  array-type
  delegate-type

class-type:
    type-name
    object
    dynamic
    string

interface-type:
    type-name

array-type:
    non-array-type rank-specifiers

non-array-type:
    type

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

引用类型值是对该类型实例的引用，后者称为对象。特殊值 null 与所有引用类型兼容，并指示实例不存在。

### 4.2.1 类类型

类类型定义一种数据结构，其中包含数据成员（常量和字段）、函数成员（方法、属性、事件、索引器、运算符、实例构造函数、析构函数和静态构造函数）以及嵌套类型。类类型支持继承，这是一种机制，派生类可通过该机制扩展和特化基类。类类型的实例使用对象创建表达式（§7.6.10.1）创建。

类类型在 §10 中描述。

某些预定义类类型在 C# 语言中具有特殊含义，如下表所述。

| 类类型 | 描述 |
|---|---|
| `System.Object` | 所有其他类型的最终基类。（参见 §4.2.2。） |
| `System.String` | C# 语言的字符串类型。（参见 §4.2.3。） |
| `System.ValueType` | 所有值类型的基类。（参见 §4.1.1。） |
| `System.Enum` | 所有枚举类型的基类。（参见 §14。） |
| `System.Array` | 所有数组类型的基类。（参见 §12。） |
| `System.Delegate` | 所有委托类型的基类。（参见 §15。） |
| `System.Exception` | 所有异常类型的基类。（参见 §16。） |

### 4.2.2 object 类型

object 类类型是所有其他类型的最终基类。C# 中的每个类型都直接或间接派生自 object 类类型。

关键字 object 只是预定义类 System.Object 的别名。

### 4.2.3 dynamic 类型

dynamic 类型与 object 一样，可以引用任何对象。当运算符应用于 dynamic 类型的表达式时，其解析会推迟到程序运行时。因此，如果该运算符无法合法地应用于所引用的对象，编译期间不会给出错误。相反，当运算符的解析在运行时失败时，将引发异常。

dynamic 类型在 §4.7 中进一步描述，动态绑定在 §7.2.2 中描述。

### 4.2.4 string 类型

string 类型是直接继承自 object 的密封类类型。string 类的实例表示 Unicode 字符串。

string 类型的值可以写为字符串字面量（§2.4.4.5）。

关键字 string 只是预定义类 System.String 的别名。

### 4.2.5 接口类型

接口定义一种契约。实现接口的类或结构必须遵守其契约。接口可以继承自多个基接口，类或结构可以实现多个接口。

接口类型在 §13 中描述。

### 4.2.6 数组类型

数组是一种数据结构，包含零个或多个通过计算索引访问的变量。数组中包含的变量（也称为数组的元素）都属于同一类型，此类型称为数组的元素类型。

数组类型在 §12 中描述。

### 4.2.7 委托类型

委托是一种数据结构，引用一个或多个方法。对于实例方法，它还引用其对应的对象实例。

C 或 C++ 中与委托最接近的等效项是函数指针，但函数指针只能引用静态函数，而委托可以引用静态方法和实例方法。在后一种情况下，委托不仅存储对方法入口点的引用，还存储对调用该方法的对象实例的引用。

委托类型在 §15 中描述。

> **克里斯·塞尔斯** 尽管 C++ 可以通过成员函数指针引用实例成员函数，但要正确处理它非常困难，以至于该特性还不如被视为非法！

## 4.3 装箱和拆箱

装箱和拆箱的概念是 C# 类型系统的核心。它允许任何*值类型*的值与 object 类型相互转换，从而在*值类型*和*引用类型*之间提供桥梁。装箱和拆箱实现了类型系统的统一视图，其中任何类型的值最终都可以被视为对象。

> **约瑟夫·阿尔巴哈里** 在 C# 2.0 之前，装箱和拆箱是编写通用集合（例如列表、堆栈或队列）的主要方式。自 C# 2.0 引入泛型以来，泛型在这些情况下提供了替代解决方案，从而带来更好的静态类型安全性和性能。装箱/拆箱必然需要少量性能开销，因为它意味着复制值、处理间接寻址以及在堆上分配内存。

> **杰西·利伯蒂** 我想更进一步地说，就所有实际目的而言，泛型的引入已将装箱和拆箱从核心关注点降为边缘关注点，只有在将值类型作为 out 或 ref 参数传递时才会受到关注。

> **克里斯蒂安·纳格尔** 如果遍历大型集合，装箱和拆箱通常较小的性能开销可能会变得巨大。泛型集合类有助于解决此问题。

### 4.3.1 装箱转换

装箱转换允许将*值类型*隐式转换为*引用类型*。存在以下装箱转换：

- 从任何*值类型*到类型 `object`。
- 从任何*值类型*到类型 `System.ValueType`。
- 从任何*不可为 null 的值类型*到该*值类型*实现的任何*接口类型*。
- 从任何*可为 null 的类型*到该*可为 null 的类型*的底层类型实现的任何*接口类型*。

> **弗拉基米尔·列什特尼科夫** *可为 null 的类型*不会从其底层类型实现接口；它只是可转换为这些接口。这种区别在某些上下文中很重要——例如，在检查泛型约束时。

- 从任何*枚举类型*到类型 `System.Enum`。
- 从任何具有底层*枚举类型*的*可为 null 的类型*到类型 `System.Enum`。




> **比尔·瓦格纳** 这里选择“转换”一词，说明了在这些情况下所看到的行为。你并不是将同一存储重新解释为不同的类型；你是在转换它。也就是说，你是在检查不同的存储，而不是通过两个不同的变量类型查看同一存储。

请注意，如果运行时最终从值类型转换为引用类型，则来自类型形参的隐式转换将作为装箱转换执行（§6.1.10）。

对非可空值类型的值进行装箱，包括分配一个对象实例，并将该非可空值类型的值复制到该实例中。

对可空类型的值进行装箱时，如果该值为null值（HasValue为false），则产生空引用；否则，产生解包并装箱其基础值的结果。

对非可空值类型的值进行装箱的实际过程，最好通过设想存在一个泛型装箱类来解释，该类的行为就好像声明如下：

```
sealed class Box<T>: System.ValueType
{
    T value;
    public Box(T t) {
        value = t;
    }
}
```

对类型T的值v进行装箱，现在包括执行表达式new Box<T>(v)，并将结果实例作为object类型的值返回。因此，语句

```
int i = 123;
object box = i;
```

在概念上对应于

```
int i = 123;
object box = new Box<int>(i);
```

上面这样的Box<T>装箱类实际上并不存在，已装箱值的动态类型实际上也不是类类型。相反，类型T的已装箱值具有动态类型T，并且使用is运算符进行的动态类型检查可以简单地引用类型T。例如，

```
int i = 123;
object box = i;
if (box is int) {
    Console.Write("Box contains an int");
}
```

将在控制台上输出字符串“Box contains an int”。

装箱转换意味着复制被装箱的值。这与将引用类型转换为object类型不同：在后一种情况下，值继续引用同一实例，只是被视为派生程度较低的类型object。例如，给定声明

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

以下语句

```
Point p = new Point(10, 10);
object box = p;
p.x = 20;
Console.Write(((Point)box).x);
```

将在控制台上输出值10，因为在将p赋值给box时发生的隐式装箱操作会导致p的值被复制。如果Point改为声明为类，则会输出值20，因为p和box将引用同一实例。

> **埃里克·利珀特** 这种可能性只是为什么将结构体设为不可变是一种好做法的原因之一。如果结构体无法变更，那么装箱会生成副本这一事实就无关紧要：两个副本将永远相同。

## 4.3.2 拆箱转换

拆箱转换允许将引用类型显式转换为值类型。存在以下拆箱转换：

- 从类型object到任何值类型。
- 从类型System.ValueType到任何值类型。
- 从任何接口类型到实现该接口类型的任何非可空值类型。
- 从任何接口类型到其基础类型实现该接口类型的任何可空类型。
- 从类型System.Enum到任何枚举类型。
- 从类型System.Enum到基础类型为枚举类型的任何可空类型。

> **比尔·瓦格纳** 与装箱一样，拆箱也涉及转换。如果对一个结构体进行装箱然后再拆箱，可能会产生三个不同的存储位置。你肯定没有三个变量在检查同一存储。

请注意，如果运行时最终从引用类型转换为值类型，则到类型形参的显式转换将作为拆箱转换执行（§6.2.6）。

到非可空值类型的拆箱操作包括：首先检查该对象实例是否为给定非可空值类型的已装箱值，然后从该实例中复制出值。

> **埃里克·利珀特** 尽管将未装箱的int转换为未装箱的double是合法的，但将已装箱的int转换为未装箱的double是不合法的——只能转换为未装箱的int。存在此约束是因为拆箱指令届时必须知道通常由编译器完成的所有类型转换规则。如果需要在运行时进行这类转换，请使用Convert类而不是拆箱强制转换。

拆箱到可空类型时，如果源操作数为null，则产生该可空类型的null值；否则，产生将该对象实例拆箱到该可空类型的基础类型后的包装结果。

参考上一节所述的假想装箱类，将对象box拆箱为值类型T的转换包括执行表达式((Box<T>) box).value。因此，语句

```
object box = 123;
int i = (int)box;
```

在概念上对应于

```
object box = new Box<int>(123);
int i = ((Box<int>)box).value;
```

要使到给定非可空值类型的拆箱转换在运行时成功，源操作数的值必须是对该非可空值类型的已装箱值的引用。如果源操作数为null，则引发System.NullReferenceException。如果源操作数是对不兼容对象的引用，则引发System.InvalidCastException。

> > **乔恩·斯基特** 有些拆箱转换并不由C#规范保证能够工作，但在CLI规范下是合法的。例如，前面给出的描述排除了从枚举值拆箱为其基础类型以及反向操作：
> >
> > ```csharp
> > object o = System.DayOfWeek.Sunday;
> > int i = (int) o;
> > ```
> >
> > 此转换在.NET中会成功，但在不同的C#实现上不保证成功。

要使到给定*可空类型*的拆箱转换在运行时成功，源操作数的值必须为null，或者是对该*可空类型*的基础*非可空值类型*的已装箱值的引用。如果源操作数是对不兼容对象的引用，则引发System.InvalidCastException。

> > **克里斯·塞尔斯** 装箱和拆箱的设计使你几乎不需要考虑它们，除非你试图减少内存使用（在这种情况下，性能分析是你的朋友！）。但是，如果你看到out或ref值在调用方位置似乎未正确设置，请怀疑是装箱问题。

## 4.4 构造类型

泛型类型声明本身表示一个*未绑定泛型类型*，它用作“蓝图”，通过应用*类型实参*来形成许多不同的类型。类型实参写紧跟在泛型类型名称之后的尖括号（<和>）内。包含至少一个类型实参的类型称为*构造类型*。构造类型可以在语言中类型名称可以出现的大多数地方使用。未绑定泛型类型只能在*typeof表达式*（§7.6.11）内使用。

构造类型也可以在表达式中用作简单名称（§7.6.2），或者在访问成员时使用（§7.6.4）。

当计算*命名空间或类型名称*时，只考虑具有正确数量类型形参的泛型类型。因此，只要类型具有不同数量的类型形参，就可以使用同一标识符来标识不同的类型。当在同一程序中混合泛型类和非泛型类时，这很有用：

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
        Queue q1;        // Nongeneric Widgets.Queue
        Queue<int> q2;   // Generic Widgets.Queue
    }
}
```

一个*类型名称*即使不直接指定类型形参，也可能标识一个构造类型。这种情况可能发生在类型嵌套在泛型类声明内，并且包含声明的实例类型被隐式用于名称查找时（§10.3.8.6）：

```
class Outer<T>
{
    public class Inner {...}
    public Inner i;        // Type of i is Outer<T>.Inner
}
```

在unsafe代码中，构造类型不能用作*非托管类型*（§18.2）。

### 4.4.1 类型实参

类型实参列表中的每个实参只是一个*类型*。

```
type-argument-list:
    < type-arguments >

type-arguments:
    type-argument
    type-arguments , type-argument

type-argument:
    type
```

在unsafe代码（§18）中，*类型实参*不能是指针类型。每个类型实参都必须满足对应类型形参上的任何约束（§10.1.5）。




### 4.4.2 开放类型和封闭类型

所有类型都可以分类为开放类型或封闭类型。开放类型是涉及类型参数的类型。更具体地说：

- 类型参数定义开放类型。
- 当且仅当数组类型的元素类型是开放类型时，该数组类型才是开放类型。
- 当且仅当构造类型的一个或多个类型实参是开放类型时，该构造类型才是开放类型。当且仅当构造嵌套类型的一个或多个类型实参，或其包含类型的类型实参是开放类型时，该构造嵌套类型才是开放类型。

封闭类型是非开放类型的类型。

在运行时，泛型类型声明中的所有代码都在某个封闭构造类型的上下文中执行，该封闭构造类型是通过向泛型声明应用类型实参而创建的。泛型类型中的每个类型参数都绑定到特定的运行时类型。所有语句和表达式的运行时处理始终使用封闭类型，而开放类型只在编译时处理期间出现。

每个封闭构造类型都有自己的一组静态变量，这些静态变量不会与其他任何封闭构造类型共享。由于开放类型在运行时不存在，因此不存在与开放类型关联的静态变量。如果两个封闭构造类型由同一个无界泛型类型构造而成，并且它们对应的类型实参是相同类型，则这两个封闭构造类型是同一类型。

### 4.4.3 已绑定类型和未绑定类型

术语“未绑定类型”指非泛型类型或未绑定泛型类型。术语“已绑定类型”指非泛型类型或构造类型。

> ERIC LIPPERT 是的，非泛型类型被视为同时属于已绑定类型和未绑定类型。

未绑定类型指由类型声明声明的实体。未绑定泛型类型本身不是一种类型，不能用作变量、参数或返回值的类型，也不能用作基类型。唯一可以引用未绑定泛型类型的构造是 typeof 表达式（§7.6.11）。

### 4.4.4 满足约束

每当引用构造类型或泛型方法时，都会根据泛型类型或方法上声明的类型参数约束（§10.1.5）检查所提供的类型实参。对于每个 where 子句，与命名类型参数对应的类型实参 A 将按照以下方式针对每个约束进行检查：

- 如果约束是类类型、接口类型或类型参数，则令 C 表示该约束，其中出现在约束中的任何类型参数都替换为所提供的类型实参。若要满足该约束，类型 A 必须能够通过以下转换之一转换为类型 C：
  - 标识转换（§6.1.1）。
  - 隐式引用转换（§6.1.6）。
  - 装箱转换（§6.1.7），前提是类型 A 是不可为 null 的值类型。
  - 从类型参数 A 到 C 的隐式引用转换、装箱转换或类型参数转换。
- 如果约束是引用类型约束（`class`），则类型 A 必须满足以下条件之一：
  - A 是接口类型、类类型、委托类型或数组类型。`System.ValueType` 和 `System.Enum` 都是满足此约束的引用类型。
  - A 是已知为引用类型的类型参数（§10.1.5）。
- 如果约束是值类型约束（`struct`），则类型 A 必须满足以下条件之一：
  - A 是结构类型或枚举类型，但不能是可为 null 的类型。`System.ValueType` 和 `System.Enum` 都是不能满足此约束的引用类型。
  - A 是具有值类型约束的类型参数（§10.1.5）。
- 如果约束是构造函数约束 `new()`，则类型 A 不能是抽象类型，并且必须具有公共无参数构造函数。以下任一条件成立时，即满足该约束：
  - A 是值类型，因为所有值类型都有公共默认构造函数（§4.1.2）。
  - A 是具有构造函数约束的类型参数（§10.1.5）。
  - A 是具有值类型约束的类型参数（§10.1.5）。
  - A 是非抽象类，并且包含一个显式声明的无参数公共构造函数。
  - A 不是抽象类型，并且具有默认构造函数（§10.11.4）。

如果给定的类型实参不满足类型参数的一个或多个约束，则会发生编译时错误。

由于类型参数不会被继承，因此约束也永远不会被继承。在下面的示例中，D 需要为其类型参数 T 指定约束，以便 T 满足基类 B<T> 所施加的约束。相比之下，类 E 无需指定约束，因为对于任何 T，List<T> 都实现了 IEnumerable。

```
class B<T> where T: IEnumerable {...}
class D<T>: B<T> where T: IEnumerable {...}
class E<T>: B<List<T>> {...}
```

## 4.5 类型参数

类型参数是一个标识符，用于指定该参数在运行时所绑定到的值类型或引用类型。

```
type-parameter:
    identifier
```

由于类型参数可以使用许多不同的实际类型实参进行实例化，因此类型参数具有不同于其他类型的操作和限制：

- 类型参数不能直接用于声明基类（§10.2.4）或接口（§13.1.3）。
- 类型参数的成员查找规则取决于应用于该类型参数的约束（如果有）。这些规则详见 §7.4。
- 类型参数可用的转换取决于应用于该类型参数的约束（如果有）。这些转换详见 §6.1.10 和 §6.2.6。
- 除非已知类型参数是引用类型（§6.1.10），否则字面量 null 不能转换为由类型参数指定的类型。但是，可以使用默认表达式（§7.6.13）代替。此外，除非类型参数具有值类型约束，否则可以使用 == 和 !=（§7.10.6）将类型参数指定的类型的值与 null 进行比较。
- 只有当类型参数受构造函数约束或值类型约束（§10.1.5）限制时，才能将 new 表达式（§7.6.10.1）与类型参数一起使用。
- 类型参数不能在特性中的任何位置使用。
- 不能在成员访问（§7.6.4）或类型名称（§3.8）中使用类型参数来标识静态成员或嵌套类型。
- 在不安全代码中，类型参数不能用作非托管类型（§18.2）。

作为一种类型，类型参数纯粹是编译时构造。在运行时，每个类型参数都会绑定到一个运行时类型，该类型是在向泛型类型声明提供类型实参时指定的。因此，使用类型参数声明的变量的类型在运行时将是一个封闭构造类型（§4.4.2）。涉及类型参数的所有语句和表达式在运行时执行时，都会使用作为该参数类型实参提供的实际类型。

## 4.6 表达式树类型

*表达式树*允许将匿名函数表示为数据结构，而不是可执行代码。*表达式树类型*是形如 `System.Linq.Expressions.Expression<D>` 的值，其中 D 是任意委托类型。在本规范的其余部分中，我们将使用简写形式 `Expression<D>` 来指代这些类型。

如果存在从匿名函数到委托类型 D 的转换，则也存在到表达式树类型 `Expression<D>` 的转换。将匿名函数转换为委托类型时，会生成一个引用该匿名函数可执行代码的委托；而将其转换为表达式树类型时，则会创建表示该匿名函数的表达式树。

表达式树是匿名函数的高效内存中数据表示，并使匿名函数的结构变得透明且明确。

与委托类型 D 一样，`Expression<D>` 也被称为具有参数类型和返回类型，这些类型与 D 的参数类型和返回类型相同。

以下示例同时将一个匿名函数表示为可执行代码和表达式树。由于存在到 `Func<int,int>` 的转换，因此也存在到 `Expression<Func<int,int>>` 的转换：

```csharp
Func<int,int> del = x => x + 1;           // Code
Expression<Func<int,int>> exp = x => x + 1;   // Data
```

执行这些赋值后，委托 `del` 引用一个返回 `x + 1` 的方法，而表达式树 `exp` 引用一个描述表达式 `x => x + 1` 的数据结构。

泛型类型 `Expression<D>` 的确切定义，以及将匿名函数转换为表达式树类型时构造表达式树的精确规则，均由实现定义。




有两点需要明确说明：

- 并非所有匿名函数都能表示为表达式树。例如，具有语句体的匿名函数以及包含赋值表达式的匿名函数无法表示。在这些情况下，转换仍然存在，但会在编译时失败。

- `Expression<D>` 提供了一个实例方法 `Compile`，用于生成类型为 `D` 的委托：

    ```csharp
    Func<int,int> del2 = exp.Compile();
    ```

    调用此委托会执行表达式树所表示的代码。因此，给定上述定义，del 和 del2 是等价的，以下两条语句将具有相同的效果：

    ```csharp
    int i1 = del(1);
    int i2 = del2(1);
    ```

    执行此代码后，i1 和 i2 的值都将为 2。

### 4.7 dynamic 类型

类型 dynamic 在 C# 中具有特殊含义。其目的是允许动态绑定，详见 §7.2.2。

除以下方面外，dynamic 类型被视为与 object 类型相同：

- 对 dynamic 类型表达式的操作可以进行动态绑定（§7.2.2）。

- 如果 dynamic 和 object 都是候选，类型推断（§7.5.2）将优先选择 dynamic 而非 object。

由于这种等价性，以下陈述成立：

- object 与 dynamic 之间存在隐式标识转换，并且在将 dynamic 替换为 object 后相同的构造类型之间也存在隐式标识转换。

- 往返于 object 的隐式和显式转换也适用于往返于 dynamic 的转换。

- 将 dynamic 替换为 object 后相同的方法签名被视为相同签名。

在运行时，类型 dynamic 与 object 无法区分。

类型为 dynamic 的表达式称为*动态表达式*。

> **ERIC LIPPERT** 类型 `dynamic` 是一个奇特的类型，但需要注意的是，从编译器的角度来看，它就是一个类型。与 `var` 不同，在大多数需要类型的情形中都可以使用它：返回类型、参数类型、类型实参等。

> **PETER SESTOFT** 实际上，`var` 是一个保留字，而不是编译时类型，而 `dynamic` 是编译时类型。`var` 关键字告诉编译器：“请根据此变量的初始化表达式推断该变量的编译时类型。” `dynamic` 类型本质上告诉编译器：“不必担心出现此变量的表达式的编译时类型检查；运行时系统将根据变量值的运行时类型执行正确的操作（或者在编译器本应报告类型错误的地方抛出异常）。” 类型 `dynamic` 不能用作扩展方法的接收者（this 类型）、类的基类型或泛型类型参数的类型约束，除此之外，它几乎可以像任何其他类型一样使用。

> **MAREK SAFAR** 使用 `dynamic` 和 `object` 类型时，方法签名被视为相同。这允许使用一个巧妙的技巧：用类型 `object` 声明的接口方法可以直接用类型 `dynamic` 的方法来实现。

> **CHRIS SELLS** 我开始对任何这样的语言感到好奇：下面这串字符既有效又有意义：
>
> 当然，这意味着 DoFoo 方法是一个类型方法（相对于实例方法），并且返回值的类型直到运行时才可知；但很难不把 DoFoo 同时读作 static 和 dynamic，并担心出现奇点。
>
> ```csharp
> class Foo {
>     public static dynamic DoFoo() {...}
> }
> ```

此页有意留白

# 5. 变量

变量表示存储位置。每个变量都有一个类型，该类型决定可存储在变量中的值。C# 是一种类型安全的语言，C# 编译器保证存储在变量中的值始终具有适当的类型。可以通过赋值或使用 ++ 和 -- 运算符来更改变量的值。

在获取变量的值之前，该变量必须被*明确赋值*（§5.3）。

如下文各节所述，变量要么是*初始已赋值*，要么是*初始未赋值*。初始已赋值的变量具有明确定义的初始值，并且始终被视为已明确赋值。初始未赋值的变量没有初始值。要使初始未赋值的变量在某个位置被视为已明确赋值，必须在通往该位置的所有可能执行路径中都对该变量进行赋值。

### 5.1 变量类别

C# 定义了七类变量：静态变量、实例变量、数组元素、值参数、引用参数、输出参数和局部变量。后续各节将分别描述这些类别。

在以下示例中

```csharp
class A
{
    public static int x;
    int y;

    void F(int[] v, int a, ref int b, out int c)
    {
        int i = 1;
        c = a + b++;
    }
}
```

x 是静态变量，y 是实例变量，v[0] 是数组元素，a 是值参数，b 是引用参数，c 是输出参数，i 是局部变量。

> **JESSE LIBERTY** 在我们的所有书中，第一个被描述的变量都使用 x 作为名称，这是不可避免的——但也很遗憾。变量名应当能够自我说明；除了也许在循环中用作计数器之外，绝不应使用单字母名称。我更希望看到这个示例（为了强调这一点）写成下面这样：
>
> ```csharp
> class ASimpleExampleClass
> {
>     public static int staticMember;
>     int memberVariable;
>     void ExampleFunction(
>         int[] arrayOfIntsParam,
>         int simpleParam,
>         ref int refParam,
>         out int outParam)
>     {
>         int tempVariable = 1;
>         outParam = simpleParam + refParam ++;
>     }
> }
> ```
>
> 虽然在这个简单示例中，这种命名方案可能显得繁琐，但正在发生的事情及其原因没有任何歧义——而且随后的解释几乎是多余的。

#### 5.1.1 静态变量

使用 static 修饰符声明的字段称为*静态变量*。静态变量在其包含类型的静态构造函数（§10.12）执行之前存在，并在关联的应用程序域停止存在时停止存在。

静态变量的初始值是该变量类型的默认值（§5.2）。

就明确赋值检查而言，静态变量被视为初始已赋值。

#### 5.1.2 实例变量

未使用 static 修饰符声明的字段称为*实例变量*。

##### 5.1.2.1 类中的实例变量

类的实例变量在该类的新实例创建时存在，并在没有对该实例的引用且该实例的析构函数（如果有）已执行后停止存在。

类的实例变量的初始值是该变量类型的默认值（§5.2）。

就明确赋值检查而言，类的实例变量被视为初始已赋值。

##### 5.1.2.2 结构体中的实例变量

结构体的实例变量与其所属的结构体变量具有完全相同的生存期。换句话说，当结构体类型的变量存在或停止存在时，该结构体的实例变量也同样存在或停止存在。

结构体的实例变量的初始赋值状态与包含它的结构体变量相同。换句话说，当结构体变量被视为初始已赋值时，其实例变量也是如此。当结构体变量被视为初始未赋值时，其实例变量同样未赋值。

> **BILL WAGNER** 结构体中引用类型的实例变量在包含它的结构体停止存在时，可能不符合垃圾回收条件。如果该对象可通过另一条路径访问，那么即使该结构体的实例变量已不存在，该对象仍然存活。数组元素也是如此。

#### 5.1.3 数组元素

数组的元素在创建数组实例时存在，并在没有对该数组实例的引用时停止存在。

数组每个元素的初始值都是该数组元素类型的默认值（§5.2）。

就明确赋值检查而言，数组元素被视为初始已赋值。

#### 5.1.4 值参数

未使用 ref 或 out 修饰符声明的参数是*值参数*。

值参数在调用该参数所属的函数成员（方法、实例构造函数、访问器或运算符）或匿名函数时存在，并使用调用中提供的实参值进行初始化。值参数通常在函数成员或匿名函数返回时停止存在。然而，如果值参数被匿名函数（§7.15）捕获，则其生存期至少延长到从该匿名函数创建的委托或表达式树符合垃圾回收条件为止。

就明确赋值检查而言，值参数被视为初始已赋值。



## 5. 变量

### 5.1.5 引用参数

使用 `ref` 修饰符声明的参数是*引用参数*。

引用参数不会创建新的存储位置。相反，引用参数表示与函数成员或匿名函数调用中作为实参给出的变量相同的存储位置。因此，引用参数的值始终与基础变量相同。

以下明确赋值规则适用于引用参数。注意 §5.1.6 中描述的输出参数规则有所不同。

- 变量在作为引用参数传递给函数成员或委托调用之前，必须已明确赋值（§5.3）。
- 在函数成员或匿名函数内，引用参数被视为初始已赋值。

在结构体类型的实例方法或实例访问器中，`this` 关键字的行为完全等同于该结构体类型的引用参数（§7.6.7）。

> **埃里克·利珀特** 更通俗地说，引用参数与输出参数的区别在于，引用参数表示“输入和输出”参数：它必须在方法开始时初始化，并且方法可以选择更改其内容。相比之下，输出参数用于输出；方法必须填充其内容，并且在完成填充之前不得查看其内容。

> **乔恩·斯基特** 甚至输出参数也不必仅用于输出。特别是，在方法为输出参数赋值之后，它随后可以从该参数读取。然而，由于该参数将与另一个变量共享存储位置，因此不能保证在方法中赋值后该值不会再次更改。这种处理方式防止输出参数被协变地使用。

> **埃里克·利珀特** 一些其他编程语言支持另一种参数传递方式：一种“仅输入”引用。也就是说，对变量的引用被传递给方法，但与 C# 引用参数不同，方法不能写入该引用——只能从中读取。这种方法对于高效传递大型值类型很有用；如果值很大，传递对变量的引用可能比传递值的副本具有更好的性能。C# 不支持这种引用传递。

### 5.1.6 输出参数

使用 `out` 修饰符声明的参数是*输出参数*。

输出参数不会创建新的存储位置。相反，输出参数表示与函数成员或委托调用中作为实参给出的变量相同的存储位置。因此，输出参数的值始终与基础变量相同。

以下明确赋值规则适用于输出参数。注意 §5.1.5 中描述的引用参数规则有所不同。

- 变量在作为输出参数传递给函数成员或委托调用之前，不需要已明确赋值。
- 在函数成员或委托调用正常完成后，作为输出参数传递的每个变量在该执行路径中视为已赋值。
- 在函数成员或匿名函数内，输出参数被视为初始未赋值。
- 函数成员或匿名函数的每个输出参数都必须在该函数成员或匿名函数正常返回之前明确赋值（§5.3）。

在结构体类型的实例构造函数中，`this` 关键字的行为完全等同于该结构体类型的输出参数（§7.6.7）。

> **克里斯蒂安·纳格尔** 与其使用输出参数从函数返回多个值，不如使用元组类型。此类型是 .NET 4 新增的。

### 5.1.7 局部变量

*局部变量*可以通过*局部变量声明*来声明，该声明可出现在*块*、*for 语句*、*switch 语句*或*using 语句*中；也可以通过*foreach 语句*声明；或者通过*try 语句*的*特定 catch 子句*声明。

局部变量的生存期是程序执行中保证为其保留存储的那一部分。该生存期至少从进入与其关联的*块*、*for 语句*、*switch 语句*、*using 语句*、*foreach 语句*或*特定 catch 子句*开始，直到该*块*、*for 语句*、*switch 语句*、*using 语句*、*foreach 语句*或*特定 catch 子句*以任何方式结束执行为止。（进入一个封闭的*块*或调用方法会暂停但不会结束当前*块*、*for 语句*、*switch 语句*、*using 语句*、*foreach 语句*或*特定 catch 子句*的执行。）如果局部变量被匿名函数（§7.15.5.1）捕获，则其生存期至少延长到从该匿名函数创建的委托或表达式树，以及任何其他引用该捕获变量的对象，符合垃圾回收条件为止。

> **比尔·瓦格纳** 最后这句话对匿名函数中捕获的局部变量的*可能成本*具有重要影响。这些变量的生存期可能长得多，这意味着这些局部变量引用的任何其他对象也将存活得久得多。

如果递归进入父*块*、*for 语句*、*switch 语句*、*using 语句*、*foreach 语句*或*特定 catch 子句*，则每次都会创建该局部变量的新实例，并且每次都会计算其*局部变量初始值设定项*（如果有）。

由*局部变量声明*引入的局部变量不会自动初始化，因此没有默认值。为了进行明确赋值检查，由*局部变量声明*引入的局部变量被视为初始未赋值。*局部变量声明*可以包含*局部变量初始值设定项*，在这种情况下，只有在初始化表达式（§5.3.3.4）之后，该变量才被视为明确赋值。

> **埃里克·利珀特** 要求局部变量必须明确赋值，而不是自动将它们赋值为默认值，这似乎会带来*性能优势*；毕竟，编译器不必生成向该位置冗余分配默认值的代码。实际上，这并不是该特性的动机。在实践中，CLR 确实会将局部变量初始化为其默认值，这通常发生得非常快。明确赋值检查的动机是防止一种常见的 bug 原因。C# 不会猜测你本意是让局部变量初始化并隐藏你的 bug；它要求在使用局部变量之前显式初始化它。

在由*局部变量声明*引入的局部变量的作用域内，在文本位置上引用该局部变量（该位置先于其*局部变量声明符*）是编译时错误。如果局部变量声明是隐式的（§8.5.1），则在其*局部变量声明符*内引用该变量也是错误。

由*foreach 语句*或*特定 catch 子句*引入的局部变量在其整个作用域内被视为明确赋值。

局部变量的实际生存期取决于实现。例如，编译器可能静态确定某个块中的局部变量仅在该块的一小部分中使用。使用这种分析，编译器可以生成代码，使该变量的存储具有比其包含块更短的生存期。

局部引用变量所引用的存储独立于该局部引用变量的生存期被回收（§3.9）。

> **克里斯·塞尔斯** C 要求变量在作用域顶部声明：
>
> ```c
> void F() {
>   int x = ...;
>   ...
>   Foo(x); // What was x again?
>   ...
> }
> ```
>
> 在 C# 中，通常认为将变量声明在远离其使用位置的地方是不好的做法。相反，更推荐以下形式：
>
> ```c
> void F() {
>   ...
>   int x = ...;
>   Foo(x); // Oh, right, I see x...
>   ...
> }
> ```
>
> 考虑这一原则（称为“引用局部性”）可使程序更具可读性和可维护性。

### 5.2 默认值

以下类别的变量会自动初始化为其默认值：

- 静态变量。
- 类实例的实例变量。
- 数组元素。

变量的默认值取决于变量的类型，并按如下方式确定：

- 对于值类型的变量，默认值与值类型的默认构造函数（§4.1.2）计算出的值相同。
- 对于引用类型的变量，默认值为 null。





通常，默认值初始化是由内存管理器或垃圾回收器在内存分配使用之前，将内存初始化为全零位来完成的。因此，使用全零位表示空引用很方便。

## 5.3 确定赋值

在函数成员的可执行代码中的某个位置，如果编译器能够通过特定的静态流分析（§5.3.3）证明某个变量已被自动初始化，或至少作为赋值目标出现过一次，则称该变量在此位置**已确定赋值**。非正式地说，确定赋值的规则如下：

- 初始已赋值变量（§5.3.1）始终被视为已确定赋值。
- 初始未赋值变量（§5.3.2）在某个位置被视为已确定赋值，当且仅当所有到达该位置的可能执行路径都至少包含以下情况之一：
  - 一条简单赋值（§7.17.1），其中该变量是左操作数。
  - 一个调用表达式（§7.6.5）或对象创建表达式（§7.6.10.1），其中将该变量作为输出参数传递。
  - 对于局部变量，包含变量初始化器的局部变量声明（§8.5.1）。

上述非正式规则所依据的形式化规范在 §5.3.1、§5.3.2 和 §5.3.3 中进行了描述。

结构类型变量的实例变量的确定赋值状态既会单独跟踪，也会整体跟踪。除了上述规则外，以下规则适用于结构类型变量及其实例变量：

- 如果某个实例变量所属的结构类型变量被视为已确定赋值，则该实例变量也被视为已确定赋值。
- 如果结构类型变量的每个实例变量都被视为已确定赋值，则该结构类型变量被视为已确定赋值。

在以下上下文中，必须满足确定赋值要求：

- 在获取变量值的每个位置，变量都必须已确定赋值。这确保不会出现未定义值。变量在表达式中的出现通常被视为获取该变量的值，但以下情况除外：
  - 变量是简单赋值的左操作数；
  - 变量作为输出参数传递；或者
  - 变量是*结构类型*变量，并且作为成员访问的左操作数出现。
- 在变量作为引用参数传递的每个位置，变量都必须已确定赋值。这确保被调用的函数成员可以将引用参数视为初始已赋值。
- 函数成员的所有输出参数，在函数成员返回的每个位置都必须已确定赋值（无论是通过 `return` 语句返回，还是执行到函数成员主体末尾而返回）。这确保函数成员不会在输出参数中返回未定义值，从而使编译器能够将一个以变量作为输出参数的函数成员调用视为等价于对该变量的赋值。
- 结构类型实例构造函数的*此*变量，在该实例构造函数返回的每个位置都必须已确定赋值。

### 5.3.1 初始已赋值变量

以下类别的变量被归类为初始已赋值：

- 静态变量。
- 类实例的实例变量。
- 初始已赋值结构变量的实例变量。
- 数组元素。
- 值参数。
- 引用参数。
- 在 `catch` 子句或 `foreach` 语句中声明的变量。

### 5.3.2 初始未赋值变量

以下类别的变量被归类为初始未赋值：

- 初始未赋值结构变量的实例变量。
- 输出参数，包括结构实例构造函数的*此*变量。
- 局部变量，但在 `catch` 子句或 `foreach` 语句中声明的变量除外。

### 5.3.3 确定确定赋值的精确规则

为了确定每个被使用的变量是否已确定赋值，编译器必须使用与本节所述过程等价的过程。

编译器会处理包含一个或多个初始未赋值变量的每个函数成员的主体。对于每个初始未赋值变量 v，编译器会在函数成员中的以下各个位置确定 v 的确定赋值状态：

- 每条语句的开头。
- 每条语句的终点（§8.1）。
- 每条将控制转移到另一条语句或某条语句终点的弧上。
- 每个表达式的开头。
- 每个表达式的末尾。

v 的确定赋值状态可以是：

- 已确定赋值。这表示在到达此位置的所有可能控制流中，v 都已被赋予值。
- 未确定赋值。对于布尔类型表达式末尾的变量状态，未被确定赋值的变量状态可能（但不一定）属于以下某个子状态：
  - 真表达式之后已确定赋值。此状态表示：如果布尔表达式的计算结果为 true，则 v 已确定赋值；但如果布尔表达式的计算结果为 false，则 v 不一定已赋值。
  - 假表达式之后已确定赋值。此状态表示：如果布尔表达式的计算结果为 false，则 v 已确定赋值；但如果布尔表达式的计算结果为 true，则 v 不一定已赋值。

以下规则决定变量 v 在每个位置的状态。

### 5.3.3.1 语句的一般规则

- 在函数成员主体的开头，v 未确定赋值。
- 在任何不可达语句的开头，v 已确定赋值。

> ERIC LIPPERT 这条规则可能会让你觉得不寻常。为什么在不可达语句中应该将每个变量都视为已确定赋值？这里讨论几个原因。
>
> 如果语句不可达，那么它就不会执行。如果它不会执行，那么它就不会读取未赋值的变量。因此，这不是问题；编译器要查找的是潜在问题，而这并不是潜在问题。
>
> 此外，不可达语句几乎肯定是错误的。一旦编译器识别出一个错误，很多相关错误很可能会聚集在其周围。与其报告大量相关问题，不如只报告一个问题并让用户修复它，通常会是更好的做法，而不是尝试报告所有可能违反规范的情况。

- 任何其他语句开头的 v 的确定赋值状态，通过检查所有目标为该语句开头的控制转移中 v 的确定赋值状态来确定。当且仅当 v 在所有此类控制转移中都已确定赋值时，v 才在该语句开头已确定赋值。可能的控制转移集合以与检查语句可达性（§8.1）相同的方式确定。
- `checked`、`unchecked`、`if`、`while`、`do`、`for`、`foreach`、`lock`、`using` 或 `switch` 语句的块终点处 v 的确定赋值状态，通过检查所有目标为该语句终点的控制转移中 v 的确定赋值状态来确定。如果 v 在所有此类控制转移中都已确定赋值，则 v 在该语句的终点处已确定赋值；否则，v 在该语句的终点处未确定赋值。可能的控制转移集合以与检查语句可达性（§8.1）相同的方式确定。

### 5.3.3.2 块语句、checked 语句和 unchecked 语句

在块中的语句列表的第一条语句处（或者，如果语句列表为空，则在块的终点处）发生控制转移时，v 的确定赋值状态与进入该块、`checked` 语句或 `unchecked` 语句之前 v 的确定赋值状态相同。

### 5.3.3.3 表达式语句

对于由表达式 expr 组成的表达式语句 stmt：

- expr 开头处 v 的确定赋值状态与 stmt 开头处相同。
- 如果 expr 末尾处 v 已确定赋值，则 stmt 终点处 v 已确定赋值；否则，stmt 终点处 v 未确定赋值。




### 5.3.3.4 声明语句

- 如果 stmt 是一个不带初始化器的声明语句，那么 v 在 stmt 结束点的明确赋值状态与在 stmt 开始处的明确赋值状态相同。
- 如果 stmt 是一个带初始化器的声明语句，那么 v 的明确赋值状态的确定方式如下：将 stmt 视为一个语句列表，其中每个带初始化器的声明对应一条赋值语句（按声明顺序）。

### 5.3.3.5 if 语句

对于形式如下的 if 语句 stmt：

```
if ( expr ) then-stmt else else-stmt
```

- v 在 expr 开始处的明确赋值状态与在 stmt 开始处的明确赋值状态相同。
- 如果 v 在 expr 结束点已明确赋值，那么在控制流转移到 then-stmt 时，以及在控制流转移到 else-stmt 时（如果没有 else 子句，则转移到 stmt 结束点）时，v 都已明确赋值。
- 如果 v 在 expr 结束点处于“真表达式之后已明确赋值”状态，那么在控制流转移到 then-stmt 时 v 已明确赋值，而在控制流转移到 else-stmt 时（如果没有 else 子句，则转移到 stmt 结束点）时 v 未明确赋值。
- 如果 v 在 expr 结束点处于“假表达式之后已明确赋值”状态，那么在控制流转移到 else-stmt 时 v 已明确赋值，而在控制流转移到 then-stmt 时 v 未明确赋值。当且仅当 v 在 then-stmt 结束点已明确赋值时，v 在 stmt 结束点才已明确赋值。
- 否则，在控制流转移到 then-stmt 或 else-stmt 时（如果没有 else 子句，则转移到 stmt 结束点）时，v 被视为未明确赋值。

### 5.3.3.6 switch 语句

在带有控制表达式 expr 的 switch 语句 stmt 中：

- v 在 expr 开始处的明确赋值状态与 v 在 stmt 开始处的状态相同。
- v 在控制流转移到可到达的 switch 块语句列表时的明确赋值状态与 v 在 expr 结束点处的明确赋值状态相同。

> **埃里克·利珀特** 遗憾的是，在少数情况下，可以对控制表达式的整个范围进行穷举 switch（即 bool、字节类型及其对应的可空类型）而不使用默认 switch 标签，但明确赋值检查不会考虑这种可能性：如果某个变量在每个 switch 节的结束点都已明确赋值，那么它在 switch 结束点也可能已明确赋值。例如：
>
> ```
> int x;
> bool b = B();
> switch(b) {
>   case true : x = 1; break;
>   case false: x = 2; break;
> }
> Console.WriteLine(x); // Error: x is not definitely assigned
> ```
>
> 在这些罕见情况下，你总可以在某个 switch 节上放一个不必要的默认 switch 标签，让明确赋值检查器满意。

### 5.3.3.7 while 语句

对于形式如下的 *while* 语句 *stmt*：

```
while ( expr ) while-body
```

- *v* 在 *expr* 开始处的明确赋值状态与在 *stmt* 开始处的明确赋值状态相同。
- 如果 *v* 在 *expr* 结束点已明确赋值，那么在控制流转移到 *while-body* 时以及在 *stmt* 结束点处，*v* 都已明确赋值。
- 如果 *v* 在 *expr* 结束点处于“真表达式之后已明确赋值”状态，那么在控制流转移到 *while-body* 时 *v* 已明确赋值，但在 *stmt* 结束点处 *v* 未明确赋值。
- 如果 *v* 在 *expr* 结束点处于“假表达式之后已明确赋值”状态，那么在控制流转移到 *stmt* 结束点时 *v* 已明确赋值，但在控制流转移到 *while-body* 时 *v* 未明确赋值。

### 5.3.3.8 do 语句

对于形式如下的 *do* 语句 *stmt*：

```
do do-body while ( expr ) ;
```

- *v* 在从 *stmt* 开始处到 *do-body* 的控制流转移中的明确赋值状态与在 *stmt* 开始处的明确赋值状态相同。
- v 在 expr 开始处的明确赋值状态与在 do-body 结束点处的明确赋值状态相同。
- 如果 v 在 expr 结束点已明确赋值，那么在控制流转移到 stmt 结束点时 v 已明确赋值。
- 如果 v 在 expr 结束点处于“假表达式之后已明确赋值”状态，那么在控制流转移到 stmt 结束点时 v 已明确赋值。

### 5.3.3.9 for 语句

对形式如下的 for 语句进行明确赋值检查：

```
for ( for-initializer ; for-condition ; for-iterator ) embedded-statement
```

检查方式如同该语句写成：

```
{
    for-initializer ;
    while ( for-condition ) {
        embedded-statement ;
        for-iterator ;
    }
}
```

如果 for 语句中省略了 for-condition，则明确赋值的求值过程如同在上述展开式中将 for-condition 替换为 true。

### 5.3.3.10 break、continue 和 goto 语句

由 break、continue 或 goto 语句引起的控制流转移中，v 的明确赋值状态与 v 在该语句开始处的明确赋值状态相同。

### 5.3.3.11 throw 语句

对于形式如下的语句 stmt：

```
throw expr ;
```

v 在 expr 开始处的明确赋值状态与 v 在 stmt 开始处的明确赋值状态相同。

### 5.3.3.12 return 语句

对于形式如下的语句 stmt：

```
return expr ;
```

- *v* 在 *expr* 开始处的明确赋值状态与 *v* 在 *stmt* 开始处的明确赋值状态相同。
- 如果 *v* 是输出参数，那么它必须在以下位置之一已明确赋值：
  - 在 *expr* 之后，或
  - 在包围该 return 语句的 try-finally 或 try-catch-finally 的 finally 块结束点。

对于形式如下的语句 *stmt*：

```
return ;
```

- 如果 *v* 是输出参数，那么它必须在以下位置之一已明确赋值：
  - 在 *stmt* 之前，或
  - 在包围该 return 语句的 try-finally 或 try-catch-finally 的 finally 块结束点。

### 5.3.3.13 try-catch 语句

> **比尔·瓦格纳** 从这里开始，你会看到任何非结构化语句（例如 throw、catch、goto、finally）都可能使编译器分析和你自己的理解变得复杂。在常规逻辑中使用这些语句时要小心。try/finally 语句是一个简化的特殊情况，但一般情况会大大降低程序的可读性。

对于形式如下的语句 *stmt*：

```
try try-block
catch(...) catch-block-1
...
catch(...) catch-block-n
```

- *v* 在 *try-block* 开始处的明确赋值状态与 *v* 在 *stmt* 开始处的明确赋值状态相同。
- *v* 在 *catch-block-i*（对于任意 *i*）开始处的明确赋值状态与 *v* 在 *stmt* 开始处的明确赋值状态相同。
- 当且仅当 *v* 在 *try-block* 结束点以及每个 *catch-block-i*（对于从 1 到 *n* 的每个 *i*）结束点都已明确赋值时，*v* 在 *stmt* 结束点才已明确赋值。

### 5.3.3.14 try-finally 语句

对于形式如下的 try 语句 stmt：

```
try try-block finally finally-block
```

- v 在 try-block 开始处的明确赋值状态与 v 在 stmt 开始处的明确赋值状态相同。
- v 在 finally-block 开始处的明确赋值状态与 v 在 stmt 开始处的明确赋值状态相同。
- 当且仅当以下至少一项为真时，v 在 stmt 结束点才已明确赋值：
  - v 在 try-block 结束点已明确赋值。
  - v 在 finally-block 结束点已明确赋值。

如果发生了控制流转移（例如 goto 语句），该转移始于 try-block 内并终止于 try-block 外，那么如果 v 在 finally-block 结束点已明确赋值，则在该控制流转移中 v 也被视为已明确赋值。（这不是“仅当”：如果 v 由于其他原因在该控制流转移中已明确赋值，那么它仍然被视为已明确赋值。）

### 5.3.3.15 try-catch-finally 语句

对形式如下的 try-catch-finally 语句进行明确赋值分析：

```
try try-block
catch(...) catch-block-1
...
catch(...) catch-block-n
finally finally-block
```

分析方式如同该语句是一个包围 try-catch 语句的 try-finally 语句：

```
try {
  try try-block
  catch(...) catch-block-1
  ...
  catch(...) catch-block-n
}
finally finally-block
```

下面的示例演示了 try 语句（§8.10）的不同块如何影响明确赋值。



class A
{
    static void F()
    {
        int i, j;
        try
        {
            goto LABEL;
            // Neither i nor j definitely assigned
            i = 1;
            // i definitely assigned
        }
        catch
        {
            // Neither i nor j definitely assigned
            i = 3;
            // i definitely assigned
        }
        finally
        {
            // Neither i nor j definitely assigned
            j = 5;
            // j definitely assigned
        }
        // i and j definitely assigned
        LABEL: ;
        // j definitely assigned
    }
}

## 5.3.3.16 foreach 语句

对于形式如下的 foreach 语句 stmt：

```
foreach ( type identifier in expr ) embedded-statement
```

- 在 expr 开始时 v 的明确赋值状态与在 stmt 开始时 v 的状态相同。
- 在控制流转移到 embedded-statement 或 stmt 的结束点时，v 的明确赋值状态与在 expr 结束时 v 的状态相同。

## 5.3.3.17 using 语句

对于形式如下的 using 语句 stmt：

```
using ( resource-acquisition ) embedded-statement
```

- 在 resource-acquisition 开始时 v 的明确赋值状态与在 stmt 开始时 v 的状态相同。
- 在控制流转移到 embedded-statement 时，v 的明确赋值状态与在 resource-acquisition 结束时 v 的状态相同。

## 5.3.3.18 lock 语句

对于形式如下的 lock 语句 stmt：

```
lock ( expr ) embedded-statement
```

- 在 expr 开始时 v 的明确赋值状态与在 stmt 开始时 v 的状态相同。
- 在控制流转移到 embedded-statement 时，v 的明确赋值状态与在 expr 结束时 v 的状态相同。

## 5.3.3.19 yield 语句

对于形式如下的 yield return 语句 stmt：

```
yield return expr ;
```

- 在 expr 开始时 v 的明确赋值状态与在 stmt 开始时 v 的状态相同。
- 在 stmt 结束时 v 的明确赋值状态与在 expr 结束时 v 的状态相同。

yield break 语句对明确赋值状态没有影响。

## 5.3.3.20 简单表达式的一般规则

以下规则适用于这些类型的表达式：字面量（§7.6.1）、简单名称（§7.6.2）、成员访问表达式（§7.6.4）、非索引基访问表达式（§7.6.8）、typeof 表达式（§7.6.11）和默认值表达式（§7.6.13）。

- 在此类表达式结束时 v 的明确赋值状态与该表达式开始时 v 的明确赋值状态相同。

## 5.3.3.21 带嵌入表达式的表达式的一般规则

以下规则适用于这些类型的表达式：括号表达式（§7.6.3）；元素访问表达式（§7.6.6）；带索引的基访问表达式（§7.6.8）；增量和减量表达式（§7.6.9、§7.7.5）；强制转换表达式（§7.6.6）；一元 +、-、~、* 表达式；二元 +、-、*、/、%、<<、>>、<、<=、>、>=、==、!=、is、as、&、|、^ 表达式（§7.8、§7.9、§7.10、§7.11）；复合赋值表达式（§7.17.2）；checked 和 unchecked 表达式（§7.6.12）；以及数组和委托创建表达式（§7.6.10）。

这些表达式中的每一个都有一个或多个子表达式，它们按固定顺序无条件求值。例如，二元 % 运算符先求值运算符的左侧，然后求值右侧。索引操作先求值被索引的表达式，然后按从左到右的顺序求值每个索引表达式。对于具有子表达式 expr<sub>1</sub>、expr<sub>2</sub>、...、expr<sub>n</sub> 并按该顺序求值的表达式 expr：

- 在 expr<sub>i</sub> 开始时 v 的明确赋值状态与在 expr 开始时的明确赋值状态相同。
- 在 expr<sub>i</sub>（i 大于 1）开始时 v 的明确赋值状态与在 expr<sub>i-1</sub> 结束时的明确赋值状态相同。
- 在 expr 结束时 v 的明确赋值状态与在 expr<sub>n</sub> 结束时的明确赋值状态相同。

## 5.3.3.22 调用表达式和对象创建表达式

对于形式如下的调用表达式 expr：

```
`primary-expression ( arg_1 , arg_2 , ... , arg_n )`
```

或形式如下的对象创建表达式：

```
`new type ( arg_1 , arg_2 , ... , arg_n )`
```

- 对于调用表达式，在 primary-expression 之前 v 的明确赋值状态与在 expr 之前 v 的状态相同。
- 对于调用表达式，在 arg<sub>i</sub> 之前 v 的明确赋值状态与在 primary-expression 之后 v 的状态相同。
- 对于对象创建表达式，在 arg<sub>i</sub> 之前 v 的明确赋值状态与在 expr 之前 v 的状态相同。
- 对于每个参数 arg<sub>i</sub>，在 arg<sub>i</sub> 之后 v 的明确赋值状态由常规表达式规则确定，忽略任何 ref 或 out 修饰符。
- 对于每个参数 arg<sub>i</sub>，对于任何大于 1 的 i，在 arg<sub>i</sub> 之前 v 的明确赋值状态与在 arg<sub>i-1</sub> 之后 v 的状态相同。
- 如果变量 v 作为 out 参数（即形式为“out v”的参数）在任何参数中传递，则在 expr 之后 v 的状态是明确赋值的。否则，在 expr 之后 v 的状态与在 arg<sub>n</sub> 之后 v 的状态相同。
- 对于数组初始值设定项（§7.6.10.4）、对象初始值设定项（§7.6.10.2）、集合初始值设定项（§7.6.10.3）和匿名对象初始值设定项（§7.6.10.6），明确赋值状态由这些构造所依据的展开形式确定。

## 5.3.3.23 简单赋值表达式

对于形式为 v = expr-rhs 的表达式 expr：

- 在 expr-rhs 之前 v 的明确赋值状态与在 expr 之前 v 的明确赋值状态相同。
- 如果 w 是与 v 相同的变量，则在 expr 之后 v 的明确赋值状态是明确赋值的。否则，在 expr 之后 v 的明确赋值状态与在 expr-rhs 之后 v 的明确赋值状态相同。

## 5.3.3.24 && 表达式

对于形式为 expr-first && expr-second 的表达式 expr：

- 在 expr-first 之前 v 的明确赋值状态与在 expr 之前 v 的明确赋值状态相同。
- 如果 expr-first 之后 v 的状态是明确赋值的或“在 true 表达式之后明确赋值”，则在 expr-second 之前 v 的明确赋值状态是明确赋值的。否则，它不是明确赋值的。
- 在 expr 之后 v 的明确赋值状态由以下规则确定：
  - 如果 expr-first 之后 v 的状态是明确赋值的，则 expr 之后 v 的状态是明确赋值的。
  - 否则，如果 expr-second 之后 v 的状态是明确赋值的，并且 expr-first 之后 v 的状态是“在 false 表达式之后明确赋值”，则 expr 之后 v 的状态是明确赋值的。
  - 否则，如果 expr-second 之后 v 的状态是明确赋值的或“在 true 表达式之后明确赋值”，则 expr 之后 v 的状态是“在 true 表达式之后明确赋值”。
  - 否则，如果 expr-first 之后 v 的状态是“在 false 表达式之后明确赋值”，并且 expr-second 之后 v 的状态是“在 false 表达式之后明确赋值”，则 expr 之后 v 的状态是“在 false 表达式之后明确赋值”。
  - 否则，expr 之后 v 的状态不是明确赋值的。

在示例中

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

变量 i 在 if 语句的一个嵌入语句中被视为明确赋值的，但在另一个中不是。在方法 F 的 if 语句中，变量 i 在第一个嵌入语句中是明确赋值的，因为表达式 (i = y) 的执行总是先于该嵌入语句的执行。相反，变量 i 在第二个嵌入语句中不是明确赋值的，因为 x >= 0 可能测试为 false，导致变量 i 未被赋值。

## 5.3.3.25 || 表达式

对于形式为 *expr-first* || *expr-second* 的表达式 *expr*：

- 在 *expr-first* 之前 *v* 的明确赋值状态与在 *expr* 之前 *v* 的明确赋值状态相同。
- 如果 *expr-first* 之后 *v* 的状态是明确赋值的或“在 false 表达式之后明确赋值”，则在 *expr-second* 之前 *v* 的明确赋值状态是明确赋值的。否则，它不是明确赋值的。
- 在 *expr* 之后 *v* 的明确赋值状态由以下规则确定：
  - 如果 *expr-first* 之后 *v* 的状态是明确赋值的，则 *expr* 之后 *v* 的状态是明确赋值的。
  - 否则，如果 *expr-second* 之后 *v* 的状态是明确赋值的，并且 *expr-first* 之后 *v* 的状态是“在 true 表达式之后明确赋值”，则 *expr* 之后 *v* 的状态是明确赋值的。
  - 否则，如果 *expr-second* 之后 *v* 的状态是明确赋值的或“在 false 表达式之后明确赋值”，则 *expr* 之后 *v* 的状态是“在 false 表达式之后明确赋值”。
  - 否则，如果 *expr-first* 之后 *v* 的状态是“在 true 表达式之后明确赋值”，并且 *expr-second* 之后 *v* 的状态是“在 true 表达式之后明确赋值”，则 *expr* 之后 *v* 的状态是“在 true 表达式之后明确赋值”。
  - 否则，*expr* 之后 *v* 的状态不是明确赋值的。

5. 变量




在示例中

```csharp
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

变量 *i* 在 `if` 语句的一个嵌入语句中被视为确定赋值，但在另一个嵌入语句中则不是。在方法 `G` 的 `if` 语句中，变量 *i* 在第二个嵌入语句中确定赋值，因为表达式 `(i = y)` 的执行总是先于该嵌入语句的执行。相反，变量 *i* 在第一个嵌入语句中不是确定赋值，因为 `x >= 0` 可能测试为 true，从而导致变量 `i` 未被赋值。

### 5.3.3.26 ! 表达式

对于形式为 `!` *expr-operand* 的表达式 *expr*：

- 在 *expr-operand* 之前，*v* 的确定赋值状态与在 *expr* 之前 *v* 的确定赋值状态相同。
- 在 *expr* 之后，*v* 的确定赋值状态由以下规则确定：
  - 如果在 *expr-operand* 之后 *v* 的状态为确定赋值，则在 *expr* 之后 *v* 的状态为确定赋值。
  - 如果在 *expr-operand* 之后 *v* 的状态不是确定赋值，则在 *expr* 之后 *v* 的状态不是确定赋值。
  - 如果在 *expr-operand* 之后 *v* 的状态为“假表达式后确定赋值”，则在 *expr* 之后 *v* 的状态为“真表达式后确定赋值”。
  - 如果在 *expr-operand* 之后 *v* 的状态为“真表达式后确定赋值”，则在 *expr* 之后 *v* 的状态为“假表达式后确定赋值”。

### 5.3.3.27 ?? 表达式

对于形式为 *expr-first* ?? *expr-second* 的表达式 *expr*：

- 在 *expr-first* 之前，*v* 的确定赋值状态与在 *expr* 之前 *v* 的确定赋值状态相同。
- 在 *expr-second* 之前，*v* 的确定赋值状态与在 *expr-first* 之后 *v* 的确定赋值状态相同。
- 在 *expr* 之后，*v* 的确定赋值状态由以下规则确定：
  - 如果 *expr-first* 是值为 null 的常量表达式（§7.19），则在 *expr* 之后 *v* 的状态与在 *expr-second* 之后 *v* 的状态相同。
- 否则，在 *expr* 之后 *v* 的状态与在 *expr-first* 之后 *v* 的确定赋值状态相同。

### 5.3.3.28 ?: 表达式

对于形式为 *expr-cond* ? *expr-true* : *expr-false* 的表达式 *expr*：

- 在 *expr-cond* 之前，*v* 的确定赋值状态与在 *expr* 之前 *v* 的状态相同。
- 在 *expr-true* 之前，*v* 的确定赋值状态为确定赋值，当且仅当在 *expr-cond* 之后 *v* 的状态为确定赋值或“真表达式后确定赋值”。
- 在 *expr-false* 之前，*v* 的确定赋值状态为确定赋值，当且仅当在 *expr-cond* 之后 *v* 的状态为确定赋值或“假表达式后确定赋值”。
- 在 *expr* 之后，*v* 的确定赋值状态由以下规则确定：
  - 如果 *expr-cond* 是值为 true 的常量表达式（§7.19），则在 *expr* 之后 *v* 的状态与在 *expr-true* 之后 *v* 的状态相同。
  - 否则，如果 *expr-cond* 是值为 false 的常量表达式（§7.19），则在 *expr* 之后 *v* 的状态与在 *expr-false* 之后 *v* 的状态相同。
  - 否则，如果在 *expr-true* 之后 *v* 的状态为确定赋值，并且在 *expr-false* 之后 *v* 的状态为确定赋值，则在 *expr* 之后 *v* 的状态为确定赋值。
  - 否则，在 *expr* 之后 *v* 的状态不是确定赋值。

### 5.3.3.29 匿名函数

对于带有主体 body（块或表达式）的 lambda 表达式或匿名方法表达式 expr：

- 在 body 之前，外部变量 v 的确定赋值状态与在 expr 之前 v 的状态相同。也就是说，外部变量的确定赋值状态继承自匿名函数的上下文。
- 在 expr 之后，外部变量 v 的确定赋值状态与在 expr 之前 v 的状态相同。

示例

```csharp
delegate bool Filter(int i);

void F()
{
    int max;
    // Error: max is not definitely assigned
    Filter f = (int n) => n < max;

    max = 5;
    DoWork(f);
}
```

会产生编译时错误，因为在声明匿名函数的位置，max 不是确定赋值。示例

```csharp
delegate void D();

void F() {
    int n;
    D d = () => { n = 1; };
    d();
    // Error: n is not definitely assigned
    Console.WriteLine(n);
}
```

也会产生编译时错误，因为匿名函数中对 n 的赋值不会影响匿名函数外部 n 的确定赋值状态。

## 5.4 变量引用

变量引用是分类为变量的表达式。变量引用表示一个存储位置，该位置既可以被访问以获取当前值，也可以被访问以存储新值。

variable-reference:
    expression

在 C 和 C++ 中，变量引用称为左值。

## 5.5 变量引用的原子性

以下数据类型的读取和写入是原子的：bool、char、byte、sbyte、short、ushort、uint、int、float 和引用类型。此外，基础类型位于前一列表中的枚举类型的读取和写入也是原子的。其他类型（包括 long、ulong、double 和 decimal，以及用户定义类型）的读取和写入不保证是原子的。除了为此目的设计的库函数外，不保证原子性的读取-修改-写入，例如在递增的情况下。

> **ERIC LIPPERT** 规范作者对读者做出某些假设——例如，关心原子性的读者已经知道它是什么。如果你不是这类读者，这里的问题在于：如果一个线程正在将 long 值 0x0123456776543210 写入当前保存零的变量，那么可能存在某个时刻，另一个线程可以从该变量读取到 0x0123456700000000。这个赋值不是“原子的”，因为它可能发生在两个不同的阶段：先是高 32 位，然后是低 32 位（或反之）。C# 语言向你保证，32 位数据类型绝不会发生这种情况，但对更大的类型不作任何保证。

> **JON SKEET** 人们常常混淆原子性与内存模型的其他复杂方面。特别是，仅仅因为赋值是原子的，并不意味着其他线程必然会立即看到它（或者实际上根本看不到），除非涉及诸如 volatile 变量、锁或显式内存屏障之类的同步技术。

本页有意留白

# 6. 转换

转换使表达式能够被视为具有特定类型。转换可以使给定类型的表达式被视为具有不同的类型，或者可以使没有类型的表达式获得类型。转换可以是隐式的或显式的，这决定了是否需要显式强制转换。例如，从 int 类型到 long 类型的转换是隐式的，因此 int 类型的表达式可以隐式地被视为 long 类型。相反的转换，从 long 类型到 int 类型，是显式的，因此需要显式强制转换。

```csharp
int a = 123;
long b = a;  // Implicit conversion from int to long
int c = (int) b; // Explicit conversion from long to int
```

某些转换由语言定义。程序也可以定义自己的转换（§6.4）。

> ERIC LIPPERT 当开发者需要知道给定转换是否可能在运行时失败时，将转换分为“显式”和“隐式”很方便。所有隐式转换都不会失败，但显式转换可能会失败。
>
> 本规范未深入考虑的另一种划分转换的方式是将其分为保留表示的转换和更改表示的转换。例如，从基类（Animal）到派生类（Giraffe）的显式转换，如果转换的表达式不是 Giraffe 的实例，则可能在运行时失败。如果它确实成功，至少我们知道该转换将产生完全相同的对象。然而，从 int 到 double 的隐式转换总是成功，但总是更改表示；会创建一个全新的 double 值，其表示与整数完全不同。
>
> 当我们讨论协变数组转换时，这种转换划分将变得重要。




## 6.1 隐式转换

以下转换被归类为隐式转换：

- 恒等转换。
- 隐式数值转换。
- 隐式枚举转换。
- 隐式可空转换。
- null 字面量转换。
- 隐式引用转换。
- 装箱转换。
- 隐式动态转换。
- 隐式常量表达式转换。
- 用户定义隐式转换。
- 匿名函数转换。
- 方法组转换。

隐式转换可出现在多种情形中，包括函数成员调用（§7.5.4）、强制转换表达式（§7.7.6）和赋值（§7.17）。

预定义隐式转换始终成功，且绝不会导致引发异常。设计良好的用户定义隐式转换也应具有这些特征。

就转换而言，类型 object 和 dynamic 被视为等效。但是，动态转换（§6.1.8 和 §6.2.6）仅适用于 dynamic 类型的表达式（§4.7）。

### 6.1.1 恒等转换

恒等转换从任意类型转换到同一类型。这种转换的存在，使得已经具有所需类型的实体可以被称为可转换为该类型。

由于 object 和 dynamic 被视为等效，因此 object 和 dynamic 之间存在恒等转换，并且在将所有出现的 dynamic 替换为 object 后相同的构造类型之间也存在恒等转换。

> **VLADIMIR RESHETNIKOV** 因此，恒等转换是对称的：如果类型 T 到类型 S 存在恒等转换，那么类型 S 到类型 T 也存在恒等转换。如果两个类型之间存在恒等转换，它们在运行时始终具有相同的表示形式。例如，List<object> 和 List<dynamic> 在运行时都表示为 List<object>。

> **BILL WAGNER** 这是 dynamic 类型的一个重要属性。它意味着 List<object> 和 List<dynamic> 等类型具有恒等转换。你可以将 object 类型的集合转换为 dynamic 类型的集合。此外，dynamic 与任何派生自 object 的类型之间不存在这种恒等关系。也就是说，List<string> 和 List<dynamic> 不具有恒等转换。

### 6.1.2 隐式数值转换

隐式数值转换包括：

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

从 int、uint、long 或 ulong 到 float，以及从 long 或 ulong 到 double 的转换可能造成精度损失，但绝不会造成数量级损失。其他隐式数值转换绝不会丢失任何信息。

不存在到 char 类型的隐式转换，因此其他整型类型的值不会自动转换为 char 类型。

### 6.1.3 隐式枚举转换

隐式枚举转换允许将*十进制整数字面量* `0` 转换为任何*枚举类型*，以及任何基础类型为*枚举类型*的*可空类型*。在后一种情况下，转换的求值方式是：先转换为基础*枚举类型*，再对结果进行包装（§4.1.10）。

> **ERIC LIPPERT** 这个问题对于表示一组标志的枚举尤其重要。为了符合 CLR 指南，打算用作标志的枚举类型最好用 `[Flags]` 特性标记，并将“None”值设置为零。但对于不满足这些条件的枚举，能够在不进行强制转换的情况下赋值为零是很好的。
>
> 关于枚举类型的正确使用，还有许多该做与不该做的事项。详情请参阅“Framework Design Guidelines”第 4.8 节。
>
> Microsoft 的 C# 实现允许任何常量零转换为任何枚举，而不仅仅是*字面量*常量零。这一轻微的规范违规因历史原因而存在。

> **JOSEPH ALBAHARI** 枚举类型的默认值为 `0`，因此赋予字面量 `0` 提供了一种将枚举变量重置为其默认值的一致方法。对于可组合的基于标志的枚举，`0` 表示“无标志”。

### 6.1.4 隐式可空转换

作用于不可空值类型的预定义隐式转换也可用于这些类型的可空形式。对于每个从不可空值类型 `S` 转换为不可空值类型 `T` 的预定义隐式恒等转换和数值转换，存在以下隐式可空转换：

- 从 `S?` 到 `T?` 的隐式转换。
- 从 `S` 到 `T?` 的隐式转换。

基于从 `S` 到 `T` 的基础转换的隐式可空转换，其求值过程如下：

- 如果可空转换是从 `S?` 到 `T?`：
    - 如果源值为 null（`HasValue` 属性为 `false`），则结果为 `T?` 类型的 null 值。
    - 否则，转换的求值方式为：先从 S? 解包为 S，再执行从 S 到 T 的基础转换，然后从 T 包装（§4.1.10）为 T?。
- 如果可空转换是从 S 到 T?，则转换的求值方式为：先执行从 S 到 T 的基础转换，然后从 T 包装为 T?。

### 6.1.5 null 字面量转换

存在从 null 字面量到任何可空类型的隐式转换。此转换生成给定可空类型的 null 值（§4.1.10）。

### 6.1.6 隐式引用转换

隐式引用转换包括：

- 从任何*引用类型*到 `object` 和 `dynamic`。
- 从任何*类类型* `S` 到任何*类类型* `T`，前提是 `S` 派生自 `T`。
- 从任何*接口类型* `S` 到任何*接口类型* `T`，前提是 `S` 实现 `T`。
- 从任何*接口类型* `S` 到任何*接口类型* `T`，前提是 `S` 派生自 `T`。
- 从元素类型为 S<sub>E</sub> 的*数组类型* `S` 到元素类型为 T<sub>E</sub> 的*数组类型* `T`，前提是以下所有条件均为真：
    - `S` 和 `T` 仅在元素类型上不同。换句话说，`S` 和 `T` 具有相同的维数。
    - S<sub>E</sub> 和 T<sub>E</sub> 都是*引用类型*。
    - 存在从 S<sub>E</sub> 到 T<sub>E</sub> 的隐式引用转换。

> **BILL WAGNER** S<sub>E</sub> 和 T<sub>E</sub> 都必须是*引用类型*，这意味着对数值类型的数组而言，数组转换是非法的。

> **VLADIMIR RESHETNIKOV** 实际上，Microsoft C# 编译器并不检查 S<sub>E</sub> 和 T<sub>E</sub> 是否为*引用类型*；它只检查从 S<sub>E</sub> 到 T<sub>E</sub> 的隐式转换是否被归类为隐式*引用*转换。这一区别相当微妙，但它允许类型参数数组之间的隐式转换。请注意，在以下示例中，类型参数 T 甚至并未在形式上*已知为引用类型*（§10.1.5），尽管它在运行时始终是引用类型：

```csharp
T[] Foo<T,S>(S[] x) where S : class, T
{
    return x;
}
```

> **ERIC LIPPERT** 协变数组转换是 CLI 和 C# 中一个颇具争议的新增功能。这种转换破坏了数组的类型安全。你可能以为可以将 `Turtle` 放入 `Animals` 数组中，但将 `Giraffes` 数组隐式转换为类型为 `Animals` 数组的表达式是合法的。当你尝试将 `Turtle` 添加到那个东西中时，运行时环境将不允许从 `Turtle` 到 `Giraffe` 的转换。因此，有时将 `Turtle` 放入 `Animals` 数组是*不*合法的，而且直到运行时你才会知道这一事实。编译器无法捕获这类错误。
>
> 在这种情况下，将转换描述为*保留表示*或*改变表示*，而不是隐式或显式，会很有用。CLI 对协变数组转换的规则要求，从源类型到目标类型的转换在运行时保留表示。例如，将包含 10 个整数的数组转换为包含 10 个 double 的数组，最终需要为每个 double 分配内存，因此无法廉价地“就地”完成。相比之下，将 `Giraffes` 数组转换为 `Animals` 数组会在运行时保留数组中每个元素的表示，从而保留数组本身的表示。
>
> 由于引用转换始终保留表示，C# 语言将显式和隐式协变数组转换限制为元素类型之间的转换是引用转换的情况。CLR 还允许其他保留表示的转换，例如 `int[]` 到 `uint[]`。

- 从任何*数组类型*到 `System.Array` 及其实现的接口。
- 从一维数组类型 `S[]` 到 `System.Collections.Generic.IList<T>` 及其基接口，前提是存在从 `S` 到 `T` 的隐式恒等转换或引用转换。
- 从任何*委托类型*到 `System.Delegate` 及其实现的接口。
- 从 null 字面量到任何*引用类型*。
- 从任何*引用类型*到*引用类型* `T`，前提是它具有到*引用类型* `T₀` 的隐式恒等转换或引用转换，并且 `T₀` 具有到 `T` 的恒等转换。

> **VLADIMIR RESHETNIKOV** 例如，存在从 `List<object>` 到 `ICollection<dynamic>` 的隐式引用转换。

- 从任何*引用类型*到接口或委托类型 `T`，前提是它具有到接口或委托类型 `T₀` 的隐式恒等转换或引用转换，并且 `T₀` 可变性可转换为 `T`（§13.1.3.2）。




> **VLADIMIR RESHETNIKOV** 例如，存在从 `List<string>` 到 `IEnumerable<object>` 的隐式引用转换。

- 已知为引用类型的类型参数所涉及的隐式转换。有关涉及类型参数的隐式转换的更多详细信息，请参阅 §6.1.10。

隐式引用转换是指在 *引用类型* 之间进行的转换，可以证明总是成功，因此在运行时不需要检查。

引用转换，无论是隐式还是显式，从不改变被转换对象的引用标识。换句话说，虽然引用转换可能会改变引用的类型，但它永远不会改变所引用对象的类型或值。

### 6.1.7 Boxing Conversions

装箱转换允许 *值类型* 被隐式转换为引用类型。从任何 *不可空值类型* 到 `object` 和 `dynamic`、到 `System.ValueType` 以及由该 *不可空值类型* 实现的任何 *接口类型* 都存在装箱转换。此外，*枚举类型* 可以转换为类型 `System.Enum`。

仅当从基础 *不可空值类型* 到该引用类型存在装箱转换时，从 *可空类型* 到引用类型才存在装箱转换。

如果值类型对接口类型 I₀ 有装箱转换且 I₀ 对 I 有恒等转换，则该值类型对接口类型 I 有装箱转换。

如果值类型对接口或委托类型 I₀ 有装箱转换且 I₀ 可方差转换为 I (§13.1.3.2)，则该值类型对接口类型 I 有装箱转换。

对 *不可空值类型* 的值进行装箱包括分配一个对象实例并将 *值类型* 值复制到该实例中。结构体可以装箱为类型 `System.ValueType`，因为它是所有结构体的基类 (§11.3.2)。

对 *可空类型* 的值进行装箱按如下方式进行：

- 如果源值为 null（`HasValue` 属性为 `false`），结果为目标类型的空引用。
- 否则，结果是对通过解包并装箱源值而产生的已装箱 T 的引用。

装箱转换在 §4.3.1 中进一步描述。

### 6.1.8 Implicit Dynamic Conversions

从类型为 dynamic 的表达式到任意类型 T 存在隐式动态转换。该转换是动态绑定的 (§7.2.2)，这意味着将在运行时从表达式的运行时类型到 T 查找隐式转换。如果未找到转换，则会抛出运行时异常。

> **VLADIMIR RESHETNIKOV** 这并不意味着存在从类型 dynamic 到任意类型 T 的隐式转换——这在某些重载解析场景中是一个重要的区别：
>
> 重载的 Foo(string x) 比 Foo(dynamic x) 更好，因为存在从 string 到 dynamic 的隐式转换，但不存在从 dynamic 到 string 的隐式转换。

```
class A
{
    static void Foo(string x) { }
    static void Foo(dynamic x) { }

    static void Main()
    {
        Foo(null);
    }
}
```

注意，此隐式转换似乎违反了 §6.1 开头提出的建议，即隐式转换绝不应导致异常。然而，并非转换本身，而是查找转换导致了异常。运行时异常的风险是使用动态绑定固有的。如果不希望转换的动态绑定，可以先将表达式转换为 object，然后再转换为所需类型。

以下示例说明了隐式动态转换：

```
object o = "object";
dynamic d = "dynamic";

string s1 = o; // Fails at compile time: no conversion exists
string s2 = d; // Compiles and succeeds at runtime
int i   = d; // Compiles but fails at runtime: no conversion exists
```

对 s2 和 i 的赋值都采用了隐式动态转换，其中操作的绑定被推迟到运行时。在运行时，会从 d 的运行时类型——string——到目标类型查找隐式转换。找到了到 string 的转换，但未找到到 int 的转换。

### 6.1.9 Implicit Constant Expression Conversions

隐式常量表达式转换允许以下转换：

- 类型为 `int` 的 *常量表达式* 可以转换为类型 `sbyte`、`byte`、`short`、`ushort`、`uint` 或 `ulong`，前提是 *常量表达式* 的值在目标类型的范围内。

> **JON SKEET** 这里 C# 的做法比 Java 更灵活：Java 仅允许隐式常量表达式转换作为赋值转换。例如，以下代码在 C# 中是合法的，但等效的 Java 代码将无法编译，因为整数表达式 10 不会被转换为 byte：

```
void MethodTakingByte(byte b) { ... }
...
// In another method
MethodTakingByte(10);
```

- 类型为 `long` 的 *常量表达式* 可以转换为类型 `ulong`，前提是 *常量表达式* 的值不为负。

### 6.1.10 Implicit Conversions Involving Type Parameters

对于给定的类型参数 T，存在以下隐式转换：

- 从 T 到其有效基类 C、从 T 到 C 的任何基类，以及从 T 到由 C 实现的任何接口。在运行时，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。
- 从 T 到 T 有效接口集中的接口类型 I，以及从 T 到 I 的任何基接口。在运行时，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。
- 从 T 到类型参数 U，前提是 T 依赖于 U (§10.1.5)。在运行时，如果 U 是值类型，则 T 和 U 必然是同一类型且不执行转换。否则，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。
- 从 null 字面量到 T，前提是已知 T 为引用类型。
- 从 T 到引用类型 I，如果它具有到引用类型 S₀ 的隐式转换且 S₀ 对 S 有恒等转换。在运行时，转换的执行方式与转换到 S₀ 相同。
- 从 T 到接口类型 I，如果它具有到接口或委托类型 I_g 的隐式转换且 I_g 可方差转换为 I (§13.1.3.2)。在运行时，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。

如果已知 T 为引用类型 (§10.1.5)，则上述转换全部归类为隐式引用转换 (§6.1.6)。如果 T *不是* 已知为引用类型，则上述转换归类为装箱转换 (§6.1.7)。

### 6.1.11 User-Defined Implicit Conversions

用户定义的隐式转换由可选的标准隐式转换、随后执行用户定义的隐式转换运算符、再随后是另一个可选的标准隐式转换组成。评估用户定义的隐式转换的确切规则在 §6.4.4 中描述。

### 6.1.12 Anonymous Function Conversions and Method Group Conversions

匿名函数和方法组本身没有类型，但可以隐式转换为委托类型或表达式树类型。匿名函数转换在 §6.5 中有更详细的描述，而方法组转换在 §6.6 中有描述。

## 6.2 Explicit Conversions

以下转换被归类为显式转换：

- 所有隐式转换。
- 显式数值转换。
- 显式枚举转换。
- 显式可空转换。
- 显式引用转换。
- 显式接口转换。
- 解箱转换。
- 显式动态转换。
- 用户定义的显式转换。

显式转换可以出现在强制转换表达式中 (§7.7.6)。

显式转换的集合包括所有隐式转换。这意味着允许冗余的强制转换表达式。



不属于隐式转换的显式转换，是指无法证明总是成功的转换、已知可能丢失信息的转换，以及跨类型领域的差异足够大而值得使用显式表示法的转换。

### 6.2.1 显式数值转换

显式数值转换是指从一种数值类型到另一种数值类型的转换，且尚不存在从前者到后者的隐式数值转换（§6.1.2）：

- 从 sbyte 到 byte、ushort、uint、ulong 或 char。
- 从 byte 到 sbyte 和 char。
- 从 short 到 sbyte、byte、ushort、uint、ulong 或 char。
- 从 ushort 到 sbyte、byte、short 或 char。
- 从 int 到 sbyte、byte、short、ushort、uint、ulong 或 char。
- 从 uint 到 sbyte、byte、short、ushort、int 或 char。
- 从 long 到 sbyte、byte、short、ushort、int、uint、ulong 或 char。
- 从 ulong 到 sbyte、byte、short、ushort、int、uint、long 或 char。
- 从 char 到 sbyte、byte 或 short。
- 从 float 到 sbyte、byte、short、ushort、int、uint、long、ulong、char 或 decimal。
- 从 double 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 decimal。
- 从 decimal 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 double。

由于显式转换包括所有隐式和显式数值转换，因此始终可以使用强制转换表达式（§7.7.6）从任何数值类型转换为任何其他数值类型。

显式数值转换可能丢失信息，也可能导致抛出异常。显式数值转换按如下方式处理：

- 对于从一种整型到另一种整型的转换，处理方式取决于执行该转换时所处的溢出检查上下文（§7.6.12）：
  - 在检查上下文中，如果源操作数的值在目标类型的范围内，则转换成功；但如果源操作数的值在目标类型的范围之外，则抛出 System.OverflowException。
  - 在非检查上下文中，转换总是成功，并按如下方式进行：
    - 如果源类型大于目标类型，则通过丢弃其“额外”的最高有效位来截断源值。然后将结果视为目标类型的值。
    - 如果源类型小于目标类型，则对源值进行符号扩展或零扩展，使其大小与目标类型相同。如果源类型有符号，则使用符号扩展；如果源类型无符号，则使用零扩展。然后将结果视为目标类型的值。
    - 如果源类型与目标类型大小相同，则将源值视为目标类型的值。
- 对于从 `decimal` 到整型的转换，源值向零舍入到最接近的整数值，该整数值成为转换的结果。如果结果整数值超出目标类型的范围，则抛出 `System.OverflowException`。
- 对于从 `float` 或 `double` 到整型的转换，处理方式取决于执行该转换时所处的溢出检查上下文（§7.6.12）：
  - 在检查上下文中，转换按如下方式进行：
    - 如果操作数的值为 NaN 或无穷大，则抛出 `System.OverflowException`。
    - 否则，源操作数向零舍入到最接近的整数值。如果该整数值在目标类型的范围内，则该值就是转换的结果。
    - 否则，抛出 `System.OverflowException`。
  - 在非检查上下文中，转换总是成功，并按如下方式进行：
    - 如果操作数的值为 NaN 或无穷大，则转换的结果是目标类型的一个未指定值。
    - 否则，源操作数向零舍入到最接近的整数值。如果该整数值在目标类型的范围内，则该值就是转换的结果。
    - 否则，转换的结果是目标类型的一个未指定值。
- 对于从 `double` 到 `float` 的转换，double 值会舍入到最接近的 float 值。如果 double 值太小而无法表示为 float，结果变为正零或负零。如果 double 值太大而无法表示为 float，结果变为正无穷大或负无穷大。如果 double 值是 NaN，结果也是 NaN。
- 对于从 float 或 double 到 decimal 的转换，源值会转换为 decimal 表示，并在需要时舍入到第 28 位小数之后最接近的数（§4.1.7）。如果源值太小而无法表示为 decimal，结果变为零。如果源值是 NaN、无穷大或太大而无法表示为 decimal，则抛出 System.OverflowException。
- 对于从 decimal 到 float 或 double 的转换，decimal 值会舍入到最接近的 double 或 float 值。虽然此转换可能丢失精度，但它从不引发异常。

> **约瑟夫·阿尔巴哈里** 实数到整型转换中的向零舍入行为很高效，但不总是最实用的方法。例如，在此方案下，(int) 3.9 的计算结果为 3，而不是 4。C# 不提供用于转换为最接近整数的内置机制；此能力留给外部库。在 Microsoft 的 .NET Framework 中，静态 Convert 类通过 ToInt32 等方法提供此功能。

### 6.2.2 显式枚举转换

显式枚举转换包括：

- 从 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal 到任何枚举类型。
- 从任何枚举类型到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal。
- 从任何枚举类型到任何其他枚举类型。

两个类型之间的显式枚举转换通过以下方式处理：将任何参与的枚举类型视为该枚举类型的基础类型，然后在结果类型之间执行隐式或显式数值转换。例如，给定基础类型为 int 的枚举类型 E，从 E 到 byte 的转换按从 int 到 byte 的显式数值转换（§6.2.1）处理，而从 byte 到 E 的转换按从 byte 到 int 的隐式数值转换（§6.1.2）处理。

### 6.2.3 显式可空转换

显式可空转换允许对非可空值类型进行操作的预定义显式转换也用于这些类型的可空形式。对于从非可空值类型 S 转换为非可空值类型 T 的每个预定义显式转换（§6.1.1、§6.1.2、§6.1.3、§6.2.1 和 §6.2.2），存在以下可空转换：

- 从 S? 到 T? 的显式转换。
- 从 S 到 T? 的显式转换。
- 从 S? 到 T 的显式转换。

对基于从 S 到 T 的基础转换的可空转换进行求值时，过程如下：

- 如果可空转换是从 S? 到 T?：
  - 如果源值为 null（HasValue 属性为 false），则结果为 T? 类型的 null 值。
  - 否则，该转换按以下方式求值：先从 S? 解包为 S，再执行从 S 到 T 的基础转换，然后从 T 包装为 T?。
- 如果可空转换是从 S 到 T?，则该转换按从 S 到 T 的基础转换后接从 T 到 T? 的包装来求值。
- 如果可空转换是从 S? 到 T，则该转换按从 S? 解包为 S 后接从 S 到 T 的基础转换来求值。

请注意，如果可空值的值为 null，尝试解包该值将引发异常。

### 6.2.4 显式引用转换

显式引用转换包括：

- 从 object 和 dynamic 到任何其他*引用类型*。
- 从任何*类类型* S 到任何*类类型* T，前提是 S 是 T 的基类。
- 从任何*类类型* S 到任何*接口类型* T，前提是 S 未密封且 S 未实现 T。
- 从任何*接口类型* S 到任何*类类型* T，前提是 T 未密封或 T 实现 S。
- 从任何*接口类型* S 到任何*接口类型* T，前提是 S 不派生自 T。
- 从元素类型为 Sₑ 的*数组类型* S 到元素类型为 Tₑ 的*数组类型* T，前提是以下所有条件均为真：
  - S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同的维数。
  - Sₑ 和 Tₑ 都是*引用类型*。
  - 存在从 Sₑ 到 Tₑ 的显式引用转换。



> **弗拉基米尔·列舍特尼科夫** Microsoft C# 编译器不检查 SE 和 TE 是否为*引用类型*；它只检查从 SE 到 TE 的显式转换是否被归类为显式*引用*转换。详细信息请参见 §6.1.6 中的相应注释。

- 从 System.Array 及其实现的接口到任何数组类型。
- 从一维数组类型 S[] 到 System.Collections.Generic.IList<T> 及其基接口，前提是存在从 S 到 T 的显式引用转换。
- 从 System.Collections.Generic.IList<S> 及其基接口到一维数组类型 T[]，前提是存在从 S 到 T 的显式恒等转换或引用转换。
- 从 System.Delegate 及其实现的接口到任何委托类型。
- 从引用类型到引用类型 T_r，前提是它存在到引用类型 T_o 的显式引用转换，并且 T_o 具有到 T_r 的恒等转换。
- 从引用类型到接口或委托类型 T，前提是它存在到接口或委托类型 T_o 的显式引用转换，并且 T_o 可变性可转换到 T，或者 T 可变性可转换到 T_o（§13.1.3.2）。
- 从 D<S1...Sn> 到 D<T1...Tn>，其中 D<X1...Xn> 是泛型委托类型，D<S1...Sn> 与 D<T1...Tn> 不兼容或不相同，并且对于 D 的每个类型参数 Xi，以下条件成立：
  - 如果 Xi 是不变的，则 Si 与 Ti 相同。
  - 如果 Xi 是协变的，则存在从 Si 到 Ti 的隐式或显式恒等转换或引用转换。
  - 如果 Xi 是逆变的，则 Si 和 Ti 要么相同，要么都是引用类型。

> **埃里克·利珀特** 最后一点的理由是，你可能有一个类型为 Action<S> 的变量，其中 S 是包含 Action<object> 实例的引用类型。你可以*隐式*将 Action<object> 转换为 Action<T>，其中 T 是任何引用类型，因此对于任何引用类型 S 和 T，你应该能够*显式*将 Action<S> 转换为 Action<T>。

- 涉及已知为引用类型的类型参数的显式转换。有关涉及类型参数的显式转换的更多详细信息，请参见 §6.2.7。

显式引用转换是那些需要在运行时检查以确保正确的引用类型之间的转换。

要使显式引用转换在运行时成功，源操作数的值必须为 null，或者源操作数所引用对象的实际类型必须是通过隐式引用转换（§6.1.6）或装箱转换（§6.1.7）可转换为目标类型的类型。如果显式引用转换失败，则抛出 System.InvalidCastException。

引用转换（无论是隐式还是显式）从不更改被转换对象的引用标识。换句话说，虽然引用转换可能更改引用的类型，但它从不更改被引用对象的类型或值。

### 6.2.5 拆箱转换

拆箱转换允许将引用类型显式转换为值类型。存在从类型 object、dynamic 和 System.ValueType 到任何非可空值类型的拆箱转换，以及从任何接口类型到实现该接口类型的任何非可空值类型的拆箱转换。此外，类型 System.Enum 可以拆箱为任何枚举类型。

如果存在从引用类型到可空类型的基础非可空值类型的拆箱转换，则存在从该引用类型到该可空类型的拆箱转换。

如果值类型 S 存在从接口类型 Iₐ 的拆箱转换，并且 Iₐ 具有到 I 的恒等转换，则值类型 S 存在从接口类型 I 的拆箱转换。

如果值类型 S 存在从接口或委托类型 Iₐ 的拆箱转换，并且 Iₐ 可变性可转换到 I，或者 I 可变性可转换到 Iₐ（§13.1.3.2），则值类型 S 存在从接口类型 I 的拆箱转换。

拆箱操作包括：首先检查对象实例是否为给定值类型的装箱值，然后从实例中复制该值。将 null 引用拆箱为可空类型会生成该可空类型的 null 值。结构体可以从类型 System.ValueType 拆箱，因为该类型是所有结构体的基类（§11.3.2）。

拆箱转换在 §4.3.2 中进一步描述。

### 6.2.6 显式动态转换

存在从类型 dynamic 的表达式到任何类型 T 的显式动态转换。该转换是动态绑定的（§7.2.2），这意味着将在运行时从表达式的运行时类型到 T 寻找显式转换。如果未找到转换，则抛出运行时异常。

如果不希望该转换进行动态绑定，可以先将表达式转换为 object，然后再转换为所需类型。

假设定义了以下类：

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

以下示例演示显式动态转换：

```
object o = "1";
dynamic d = "2";

var c1 = (C)o; // Compiles, but explicit reference conversion fails
var c2 = (C)d; // Compiles and user-defined conversion succeeds
```

在编译时，o 到 C 的最佳转换被确定为显式引用转换。这在运行时失败，因为 "1" 实际上并不是 C。然而，将 d 到 C 的转换作为显式动态转换会推迟到运行时，在运行时找到从 d 的运行时类型——string——到 C 的用户定义转换，并且该转换成功。

### 6.2.7 涉及类型参数的显式转换

对于给定的类型参数 T，存在以下显式转换：

- 从 T 的有效基类 C 到 T，以及从 C 的任何基类到 T。在运行时，如果 T 是值类型，则该转换作为拆箱转换执行。否则，该转换作为显式引用转换或恒等转换执行。
- 从任何接口类型到 T。在运行时，如果 T 是值类型，则该转换作为拆箱转换执行。否则，该转换作为显式引用转换或恒等转换执行。
- 从 T 到任何接口类型 I，前提是尚不存在从 T 到 I 的隐式转换。在运行时，如果 T 是值类型，则该转换作为装箱转换后跟显式引用转换执行。否则，该转换作为显式引用转换或恒等转换执行。
- 从类型参数 U 到 T，前提是 T 依赖于 U（§10.1.5）。在运行时，如果 U 是值类型，则 T 和 U 必然是同一类型，并且不执行转换。否则，如果 T 是值类型，则该转换作为拆箱转换执行。否则，该转换作为显式引用转换或恒等转换执行。

如果已知 T 是引用类型，则所有这些转换都被归类为显式引用转换（§6.2.4）。如果未知 T 是引用类型，则这些转换被归类为拆箱转换（§6.2.5）。

> **约瑟夫·阿尔巴哈里** 涉及类型参数的转换行为可以通过以下方法进一步说明：
>
> ```
> static T Cast<T>(object value) { return (T)value; }
> ```
>
> 此方法可以执行引用转换或拆箱，但从不执行数值转换或用户定义转换：
>
> ```
> string s = Cast<string>("s");
>     // Okay -- reference conversion
> int i = Cast<int>(3);
>     // Okay -- unboxing
> long l = Cast<long>(3);
>     // InvalidCastException: attempts
>     // an unboxing instead of an
>     // int->long numeric conversion
> ```
>
> 在方法 System.Linq.Enumerable.Cast 中会出现相同的情况，该方法在 Microsoft 的 LINQ 实现中是标准查询运算符。

上述规则不允许从不受约束的类型参数到非接口类型的直接显式转换，这可能令人惊讶。此规则的原因是为了防止混淆，并使此类转换的语义清晰。例如，考虑以下声明：

```
class X<T>
{
    public static long F(T t) {
        return (long)t;   // Error
    }
}
```

如果允许将 t 直接显式转换为 int，人们可能很容易期望 X<int>.F(7) 会返回 7L。然而，它不会，因为标准数值转换仅在绑定时间已知类型为数值类型时才被考虑。为了使语义清晰，上述示例必须改为写成：

```
class X<T>
{
    public static long F(T t) {
        return (long)(object)t;   // Okay, but works only when T is long
    }
}
```

此代码现在可以编译，但执行 X<int>.F(7) 会在运行时抛出异常，因为装箱的 int 不能直接转换为 long。




## 6.2.8 用户定义显式转换

用户定义显式转换由一个可选的标准显式转换、随后执行一个用户定义隐式或显式转换运算符，以及再一个可选的标准显式转换组成。求值用户定义显式转换的确切规则在§6.4.5中描述。

> **埃里克·利珀特** 那些“夹在”用户定义转换两端的转换是显式转换，因此它们自身也可能失败。因此，用户定义显式转换在运行时有三个潜在失败点，而不仅仅一个。
>
> 即便如此，至少这些夹在中间的转换本身从不是用户定义转换。例如，如果存在从X到Y的用户定义显式转换，以及从Y到Z的用户定义显式转换，那么尝试将X强制转换为Z不会成功。
>
> 话虽如此，在刻意构造的场景中，显式转换链可能变得相当长。例如，考虑一个结构Foo，它具有从Foo?到decimal的用户定义显式转换。对类型Foo的表达式到类型int?的强制转换将把Foo转换为Foo?，然后将Foo?转换为decimal，再将decimal转换为int，最后将int转换为int?。

## 6.3 标准转换

标准转换是那些可以作为用户定义转换的一部分发生的预定义转换。

### 6.3.1 标准隐式转换

以下隐式转换被归类为标准隐式转换：

- 标识转换（§6.1.1）。
- 隐式数值转换（§6.1.2）。
- 隐式可空转换（§6.1.4）。
- 隐式引用转换（§6.1.6）。
- 装箱转换（§6.1.7）。
- 隐式常量表达式转换（§6.1.8）。
- 涉及类型参数的隐式转换（§6.1.10）。

标准隐式转换明确排除用户定义隐式转换。

### 6.3.2 标准显式转换

标准显式转换包括所有标准隐式转换，再加上那些存在反向标准隐式转换的显式转换子集。换言之，如果存在从类型A到类型B的标准隐式转换，则存在从类型A到类型B以及从类型B到类型A的标准显式转换。

> **弗拉基米尔·列舍特尼科夫** 例如，从double到decimal以及从decimal到double的预定义显式数值转换不是标准显式转换。

## 6.4 用户定义转换

C#允许通过用户定义转换来扩充预定义隐式和显式转换。用户定义转换通过在类和结构类型中声明转换运算符（§10.10.3）引入。

> **比尔·瓦格纳** 通常，转换意味着多个类型在某种程度上可以互换。这一概念反过来意味着其中一个或多个类型可能并非必要。随着你编写更多转换方法，请考虑是否可能创建了服务于同一目的的多个类型。
>
> 当为引用类型编写转换时，务必保留这一属性：引用转换的结果始终引用与源相同的对象。

### 6.4.1 允许的用户定义转换

C#只允许声明某些用户定义转换。特别是，不可能重新定义已存在的隐式或显式转换。

对于给定的源类型S和目标类型T，如果S或T是可空类型，则令S₀和T₀指代它们的基础类型；否则，S₀和T₀分别等于S和T。只有当以下所有条件都为真时，类或结构才允许声明从源类型S到目标类型T的转换：

- S₀和T₀是不同的类型。
- S₀或T₀是运算符声明所在的类或结构类型。
- S₀和T₀都不是*接口类型*。
- 排除用户定义转换后，不存在从S到T或从T到S的转换。

适用于用户定义转换的限制将在§10.10.3中进一步讨论。

### 6.4.2 提升转换运算符

给定一个从非可空值类型S转换为非可空值类型T的用户定义转换运算符，存在一个从S?转换为T?的*提升转换运算符*。此提升转换运算符执行从S?到S的拆包，随后是从S到T的用户定义转换，随后是从T到T?的包装，例外是值为null的S?直接转换为值为null的T?。

提升转换运算符具有与其基础用户定义转换运算符相同的隐式或显式分类。“用户定义转换”一词适用于用户定义和提升转换运算符的使用。

### 6.4.3 用户定义转换的求值

用户定义转换将值从其类型（称为*源类型*）转换为另一种类型（称为*目标类型*）。用户定义转换的求值核心在于为特定的源类型和目标类型找到*最具体*的用户定义转换运算符。这一确定过程分为若干步骤：

- 查找将从中考虑用户定义转换运算符的类和结构集合。该集合由源类型及其基类以及目标类型及其基类组成（隐含假设只有类和结构可以声明用户定义运算符，且非类类型没有基类）。为执行此步骤，如果源类型或目标类型是*可空类型*，则改用其基础类型。
- 从该类型集合中，确定哪些用户定义转换运算符和提升转换运算符适用。要使转换运算符适用，必须能够执行从源类型到该运算符操作数类型的标准转换（§6.3），并且必须能够执行从该运算符结果类型到目标类型的标准转换。
- 从适用的用户定义运算符集合中，确定哪个运算符无歧义地最具体。一般而言，最具体的运算符是其操作数类型“最接近”源类型且其结果类型“最接近”目标类型的运算符。用户定义转换运算符优先于提升转换运算符。确定最具体用户定义转换运算符的确切规则在以下各节中定义。

一旦确定了最具体的用户定义转换运算符，用户定义转换的实际执行最多涉及三个步骤：

- 首先，如果需要，执行从源类型到用户定义或提升转换运算符操作数类型的标准转换。
- 接下来，调用用户定义或提升转换运算符来执行转换。
- 最后，如果需要，执行从用户定义或提升转换运算符结果类型到目标类型的标准转换。

用户定义转换的求值绝不会涉及一个以上的用户定义或提升转换运算符。换言之，从类型S到类型T的转换绝不会先执行从S到X的用户定义转换，然后再执行从X到T的用户定义转换。

用户定义隐式或显式转换求值的精确定义在以下各节中给出。这些定义使用以下术语：

- 如果存在从类型A到类型B的标准隐式转换（§6.3.1），且A和B都不是*接口类型*，则称A*被B涵盖*，并称B*涵盖*A。
- 类型集合中的*最具涵盖性的类型*是涵盖该集合中所有其他类型的那个类型。如果没有单一类型涵盖所有其他类型，则该集合没有*最具涵盖性的类型*。更直观地说，*最具涵盖性的类型*是集合中的“最大”类型——即其他每个类型都可以隐式转换到的那个类型。
- 类型集合中的*被涵盖最多的类型*是被该集合中所有其他类型涵盖的那个类型。如果没有单一类型被所有其他类型涵盖，则该集合没有*被涵盖最多的类型*。更直观地说，*被涵盖最多的类型*是集合中的“最小”类型——即可以隐式转换为其他每个类型的那个类型。

> **比尔·瓦格纳** 你编写的转换运算符越多，就越有可能在转换之间引入歧义。这些歧义会使你的类更难以使用。




## 6.4.4 用户定义隐式转换

从类型 S 到类型 T 的用户定义隐式转换按如下方式处理：

- 确定类型 S₀ 和 T₀。如果 S 和 T 是可空类型，则 S₀ 和 T₀ 是它们的基础类型；否则，S₀ 和 T₀ 分别等于 S 和 T。
- 查找将从中考虑用户定义转换运算符的类型集合 D。该集合由 S₀（如果 S₀ 是类或结构）、S₀ 的基类（如果 S₀ 是类）以及 T₀（如果 T₀ 是类或结构）组成。
- 查找适用的用户定义转换运算符和提升转换运算符的集合 U。该集合由 D 中的类或结构声明的、从包含 S 的类型转换为被 T 包含的类型的用户定义隐式转换运算符和提升隐式转换运算符组成。如果 U 为空，则该转换未定义，并发生编译时错误。
- 查找 U 中运算符的最具体源类型 Sₓ：
  - 如果 U 中有任何运算符从 S 转换，则 Sₓ 为 S。
  - 否则，Sₓ 是 U 中运算符的源类型合并集合中最被包含的类型。如果无法找到唯一的最被包含类型，则该转换有歧义，并发生编译时错误。
- 查找 U 中运算符的最具体目标类型 Tₓ：
  - 如果 U 中有任何运算符转换为 T，则 Tₓ 为 T。
  - 否则，Tₓ 是 U 中运算符的目标类型合并集合中最包含的类型。如果无法找到唯一的最包含类型，则该转换有歧义，并发生编译时错误。
- 查找最具体的转换运算符：
  - 如果 U 恰好包含一个从 Sₓ 转换为 Tₓ 的用户定义转换运算符，则这就是最具体的转换运算符。
  - 否则，如果 U 恰好包含一个从 Sₓ 转换为 Tₓ 的提升转换运算符，则这就是最具体的转换运算符。
  - 否则，该转换有歧义，并发生编译时错误。
- 最后，应用该转换：
  - 如果 S 不是 Sₓ，则执行从 S 到 Sₓ 的标准隐式转换。
  - 调用最具体的转换运算符将 Sₓ 转换为 Tₓ。
  - 如果 Tₓ 不是 T，则执行从 Tₓ 到 T 的标准隐式转换。

## 6.4.5 用户定义显式转换

从类型 S 到类型 T 的用户定义显式转换按如下方式处理：

- 确定类型 Sₐ 和 Tₐ。如果 S 或 T 是可空类型，则 Sₐ 和 Tₐ 是它们各自的基础类型；否则，Sₐ 和 Tₐ 分别等于 S 和 T。
- 查找将从中考虑用户定义转换运算符的类型集合 D。该集合由 Sₐ（如果 Sₐ 是类或结构）、Sₐ 的基类（如果 Sₐ 是类）、Tₐ（如果 Tₐ 是类或结构）以及 Tₐ 的基类（如果 Tₐ 是类）组成。
- 查找适用的用户定义转换运算符和提升转换运算符的集合 U。该集合由 D 中的类或结构声明的、从包含 S 或被 S 包含的类型转换为包含 T 或被 T 包含的类型的用户定义转换运算符和提升的隐式或显式转换运算符组成。如果 U 为空，则该转换未定义，并发生编译时错误。
- 查找 U 中运算符的最具体源类型 Sₓ：
  - 如果 U 中有任何运算符从 S 转换，则 Sₓ 为 S。
  - 否则，如果 U 中有任何运算符从包含 S 的类型转换，则 Sₓ 是这些运算符的源类型合并集合中最被包含的类型。如果找不到最被包含类型，则该转换有歧义，并发生编译时错误。
  - 否则，Sₓ 是 U 中运算符的源类型合并集合中最包含的类型。如果无法找到唯一的最包含类型，则该转换有歧义，并发生编译时错误。
- 查找 U 中运算符的最具体目标类型 Tₓ：
  - 如果 U 中有任何运算符转换为 T，则 Tₓ 为 T。
  - 否则，如果 U 中有任何运算符转换为被 T 包含的类型，则 Tₓ 是这些运算符的目标类型合并集合中最包含的类型。如果无法找到唯一的最包含类型，则该转换有歧义，并发生编译时错误。
  - 否则，Tₓ 是 U 中运算符的目标类型合并集合中最被包含的类型。如果找不到最被包含类型，则该转换有歧义，并发生编译时错误。
- 查找最具体的转换运算符：
  - 如果 U 恰好包含一个从 Sₓ 转换为 Tₓ 的用户定义转换运算符，则这就是最具体的转换运算符。
  - 否则，如果 U 恰好包含一个从 Sₓ 转换为 Tₓ 的提升转换运算符，则这就是最具体的转换运算符。
- 否则，该转换有歧义，并发生编译时错误。
- 最后，应用该转换：
  - 如果 S 不是 Sₓ，则执行从 S 到 Sₓ 的标准显式转换。
  - 调用最具体的用户定义转换运算符将 Sₓ 转换为 Tₓ。
  - 如果 Tₓ 不是 T，则执行从 Tₓ 到 T 的标准显式转换。

## 6.5 匿名函数转换

匿名方法表达式或 lambda 表达式归类为匿名函数（§7.15）。该表达式没有类型，但可以隐式转换为兼容的委托类型或表达式树类型。具体而言，委托类型 D 与匿名函数 F 兼容的条件是：

- 如果 F 包含匿名函数签名，则 D 和 F 具有相同数量的参数。
- 如果 F 不包含匿名函数签名，则 D 可以具有任意类型的零个或多个参数，只要 D 的任何参数都没有 out 参数修饰符。
- 如果 F 具有显式类型参数列表，则 D 中的每个参数与 F 中的对应参数具有相同的类型和修饰符。

> **VLADIMIR RESHETNIKOV** 此规则有一个例外：如果委托类型 D 具有带 params 修饰符的参数，则允许（并且要求）F 中的对应参数不具有任何修饰符。

- 如果 F 具有隐式类型参数列表，则 D 没有 ref 或 out 参数。
- 如果 D 具有 void 返回类型且 F 的主体是表达式，则当为 F 的每个参数赋予 D 中对应参数的类型时，F 的主体是有效表达式（相对于 §7），可作为语句表达式（§8.6）使用。
- 如果 D 具有 void 返回类型且 F 的主体是语句块，则当为 F 的每个参数赋予 D 中对应参数的类型时，F 的主体是有效语句块（相对于 §8.2），其中没有 return 语句指定表达式。
- 如果 D 具有非 void 返回类型且 F 的主体是表达式，则当为 F 的每个参数赋予 D 中对应参数的类型时，F 的主体是有效表达式（相对于 §7），且可隐式转换为 D 的返回类型。
- 如果 D 具有非 void 返回类型且 F 的主体是语句块，则当为 F 的每个参数赋予 D 中对应参数的类型时，F 的主体是有效语句块（相对于 §8.2），具有不可达的结束点，并且其中每个 return 语句指定的表达式都可隐式转换为 D 的返回类型。

如果委托类型 D 与匿名函数 F 兼容，则表达式树类型 Expression<D> 与匿名函数 F 兼容。

> VLADIMIR RESHETNIKOV 只有形式为 lambda 表达式的匿名函数才能隐式转换为表达式树类型（匿名方法表达式永远不能转换为这些类型）。但即使是 lambda 表达式的现有转换，也可能在编译时失败。

某些匿名函数不能转换为表达式树类型：即使转换存在，也会在编译时失败。如果匿名表达式包含以下一个或多个构造，则属于这种情况：

- 简单赋值运算符或复合赋值运算符。
- 动态绑定表达式。

> **VLADIMIR RESHETNIKOV** 当前实现不支持的其他构造包括嵌套的匿名方法表达式、带语句体的 lambda 表达式、带 ref 或 out 参数的 lambda 表达式、基访问、多维数组初始化器、命名参数和可选参数、隐式 ref 以及指针操作。
> 
> 如果需要在表达式树中将 dynamic 类型的表达式强制转换为另一种类型，可以要么使用 as 运算符，要么先将该表达式强制转换为 object。

以下示例使用泛型委托类型 Func<A,R>，它表示一个接受 A 类型参数并返回 R 类型值的函数：

```
delegate R Func<A,R>(A arg);
```

在以下赋值中

```
Func<int,int> f1 = x => x + 1;    // Okay
Func<int,double> f2 = x => x + 1;    // Okay
Func<double,int> f3 = x => x + 1;    // Error
```

每个匿名函数的参数类型和返回类型由该匿名函数所赋值到的变量的类型确定。




第一个赋值成功地将匿名函数转换为委托类型 Func<int, int>，因为当 x 被赋予 int 类型时，x + 1 是一个可隐式转换为 int 类型的有效表达式。

同样，第二个赋值成功地将匿名函数转换为委托类型 Func<int,double>，因为 x + 1 的结果（类型为 int）可隐式转换为 double 类型。

然而，第三个赋值会生成编译时错误，因为当 x 被赋予 double 类型时，x + 1 的结果（类型为 double）不能隐式转换为 int 类型。

匿名函数可能影响重载决策，并且可能参与类型推断。有关更多详细信息，请参见 §7.5。

### 6.5.1 匿名函数转换为委托类型的求值

将匿名函数转换为委托类型会生成一个委托实例，该实例引用匿名函数以及在求值时处于活动状态的（可能为空的）捕获外部变量集合。调用该委托时，将执行匿名函数的主体。主体中的代码使用该委托所引用的捕获外部变量集合来执行。

由匿名函数生成的委托的调用列表包含单个项。该委托的确切目标对象和目标方法未作规定。特别地，未规定该委托的目标对象是 null、外围函数成员的 this 值，还是某个其他对象。

将具有相同（可能为空的）捕获外部变量实例集合的语义相同匿名函数转换为相同委托类型时，允许（但不要求）返回同一个委托实例。这里的术语“语义相同”是指：在给定相同参数的情况下，匿名函数的执行在所有情况下都会产生相同的效果。此规则允许优化如下代码。

```csharp
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

由于这两个匿名函数委托具有相同（空）的捕获外部变量集合，并且由于这些匿名函数语义相同，因此允许编译器让这些委托引用同一个目标方法。实际上，允许编译器从两个匿名函数表达式中返回完全相同的委托实例。

> **JON SKEET**  当考虑合并和移除委托的前景时，这种潜在优化有些危险——这在涉及事件时尤其重要。考虑下面这段代码：
> 
> ```csharp
> button.Click += (sender, args) => Console.WriteLine("Clicked");
> button.Click += (sender, args) => Console.WriteLine("Clicked");
> ```
> 
> 假设采用简单的事件实现，结果会是什么？要么按钮的 Click 事件拥有与之前相同的事件处理程序，要么它会多出一个事件处理程序。要当心那些会显著改变行为的“优化”。

> **VLADIMIR RESHETNIKOV**  Microsoft C# 编译器不会在泛型方法内缓存委托实例。

### 6.5.2 匿名函数转换为表达式树类型的求值

将匿名函数转换为表达式树类型会生成表达式树（§4.6）。更准确地说，匿名函数转换的求值会导致构造一个表示匿名函数自身结构的对象结构。表达式树的精确结构以及创建它的确切过程均由实现定义。

> **VLADIMIR RESHETNIKOV**  与委托一样，表达式树也可以有一组捕获的外部变量。

### 6.5.3 实现示例

本节描述一种基于其他 C# 构造实现匿名函数转换的可能方式。这里描述的实现基于 Microsoft C# 编译器所使用的相同原则，但它绝不是强制性的实现，也不是唯一可能的实现。它只简要提及到表达式树的转换，因为其确切语义超出本规范的范围。

本节的其余部分给出若干包含具有不同特征的匿名函数的代码示例。对于每个示例，都提供了仅使用其他 C# 构造的相应代码转换。在这些示例中，假定标识符 D 表示以下委托类型：

```csharp
public delegate void D();
```

匿名函数的最简单形式是不捕获任何外部变量：

```csharp
class Test
{
    static void F() {
        D d = () => { Console.WriteLine("test"); };
    }
}
```

这可以转换为一个委托实例化，该委托引用一个编译器生成的静态方法，匿名函数的代码就放在该方法中：

```csharp
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

在下面的示例中，匿名函数引用了 this 的实例成员：

```csharp
class Test
{
    int x;
    void F() {
        D d = () => { Console.WriteLine(x); };
    }
}
```

这可以转换为一个编译器生成的实例方法，该方法包含匿名函数的代码：

```csharp
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

在这个示例中，匿名函数捕获一个局部变量：

```csharp
class Test
{
    void F() {
        int y = 123;
        D d = () => { Console.WriteLine(y); };
    }
}
```

现在，该局部变量的生存期必须至少延长到匿名函数委托的生存期。这可以通过将局部变量“提升”到编译器生成的类的字段中来实现。于是，局部变量的实例化（§7.15.5.2）对应于创建编译器生成的类的实例，而访问该局部变量则对应于访问编译器生成的类实例中的字段。此外，匿名函数会成为编译器生成的类的实例方法：

```csharp
class Test
{
    void F() {
        __locals1 __locals1 = new __locals1();
        __locals1.y = 123;
        D d = new D(__locals1.__Method1);
    }

    class __locals1
    {
        public int y;

        public void __Method1() {
            Console.WriteLine(y);
        }
    }
}
```

最后，下面的匿名函数捕获 this 以及两个具有不同生存期的局部变量：

```csharp
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

这里，会为每个捕获局部变量的语句块创建一个编译器生成的类，使得不同块中的局部变量可以具有独立的生存期。内部语句块的编译器生成类 __Local2 的实例包含局部变量 z 以及一个引用 __Local1 实例的字段。外部语句块的编译器生成类 __Local1 的实例包含局部变量 y 以及一个引用外围函数成员的 this 的字段。借助这些数据结构，可以通过 __Local2 的实例访问到所有捕获的外部变量，因此匿名函数的代码可以实现为该类的实例方法。

> **BILL WAGNER**  如果 F() 返回 D 的一个实例，那么这个函数捕获的所有变量的生存期都会被延长。

```csharp
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

    class __Locals1
    {
        public Test __this;
        public int y;
    }

    class __Locals2
    {
        public __Locals1 __locals1;
        public int z;
        public void __Method1() {
            Console.WriteLine(__locals1.__this.x + __locals1.y + z);
        }
    }
}
```

此处用于捕获局部变量的同一技术也可在将匿名函数转换为表达式树时使用：对编译器生成的对象的引用可以存储在表达式树中，而对局部变量的访问可以表示为对这些对象的字段访问。这种方法的优点是，它允许“提升”的局部变量在委托和表达式树之间共享。





> **ERIC LIPPERT** 这种实现技术的一个缺点（也是许多具有类似闭包语义的语言的许多实现共有的一个缺点）是，同一方法中两个不同的匿名函数分别闭包捕获两个不同的局部变量时，会导致这两个变量的生存期都被延长，以与生存期最长的委托相匹配。

假设你有两个局部变量 expensive 和 cheap，以及两个委托，每个委托分别捕获一个变量：

```
D longlived = () => cheap;
D shortlived = () => expensive;
```

expensive 的生存期至少与 longlived 所引用对象的生存期一样长，尽管 longlived 实际上并不使用 expensive。更复杂的实现会将闭包捕获的变量划分到单独的编译器生成类中，从而避免此问题。

## 6.6 方法组转换

存在从方法组（§7.1）到兼容委托类型的隐式转换（§6.1）。给定委托类型 D 和分类为方法组的表达式 E，如果 E 包含至少一个方法，该方法在其正常形式（§7.5.3.1）下适用于通过使用 D 的参数类型和修饰符构造的参数列表，则存在从 E 到 D 的隐式转换，如下所述。

下面描述从方法组 E 到委托类型 D 的转换在编译时的应用。请注意，从 E 到 D 的隐式转换的存在并不保证该转换在编译时的应用会无错误地成功。

> **VLADIMIR RESHETNIKOV** 尤其可能发生的情况是，重载决策会选择一个签名中包含委托类型的最佳函数成员，而作为相应参数提供的方法组到该委托类型的隐式转换将导致编译时错误。例如，这种情况可能发生，因为重载决策无法在该组中找到唯一最佳方法。即使找到了最佳方法，也可能违反其类型参数的约束，或者该方法可能与该委托类型不兼容，或者它可能是在静态上下文中引用的实例方法。

- 选择单个方法 M，对应于形式为 E(A) 的方法调用（§7.6.5.1），并作如下修改：
  - 参数列表 A 是表达式列表，每个表达式分类为变量，并具有 D 的形参列表中对应参数的类型和修饰符（ref 或 out）。
  - 考虑的候选方法仅包括那些在正常形式（§7.5.3.1）下适用的方法，而不是仅在展开形式下适用的方法。
- 如果 §7.6.5.1 的算法产生错误，则发生编译时错误。否则，该算法产生一个与 D 参数数量相同的唯一最佳方法 M，并认为转换存在。
- 所选方法 M 必须与委托类型 D 兼容（§15.2）；否则发生编译时错误。
- 如果所选方法 M 是实例方法，则与 E 关联的实例表达式确定委托的目标对象。
- 如果所选方法 M 是扩展方法（通过实例表达式上的成员访问来表示），则该实例表达式确定委托的目标对象。
- 转换结果是类型 D 的值——即一个新创建的委托，它引用所选方法和目标对象。

请注意，如果 §7.6.5.1 的算法未能找到实例方法，但成功将 E(A) 的调用作为扩展方法调用（§7.6.5.2）处理，则此过程可能导致创建指向扩展方法的委托。这样创建的委托既捕获扩展方法，也捕获其第一个参数。

> > **VLADIMIR RESHETNIKOV** 如果转换为委托类型的扩展方法的第一个参数是值类型，或者是未知为引用类型（§10.1.5）的类型参数，则发生编译时错误。
> >
> > 如果将 System.Nullable<T> 中声明的实例方法转换为委托类型，也会发生编译时错误。

以下示例演示方法组转换：

```
delegate string D1(object o);
delegate object D2(string s);
delegate object D3();
delegate string D4(object o, params object[] a);
```

```
delegate string D5(int i);
class Test
{
    static string F(object o) {...}
    static void G() {
        D1 d1 = F;    // Okay
        D2 d2 = F;    // Okay
        D3 d3 = F;    // Error: not applicable
        D4 d4 = F;    // Error: not applicable in normal form
        D5 d5 = F;    // Error: applicable but not compatible
    }
}
```

对 d1 的赋值将方法组 F 隐式转换为类型 D1 的值。

对 d2 的赋值展示了如何为具有派生程度较低（逆变）的参数类型和派生程度较高（协变）的返回类型的方法创建委托。

对 d3 的赋值说明如果方法不适用，则不存在转换。

对 d4 的赋值说明方法必须在其正常形式下适用。

对 d5 的赋值说明委托和方法的参数类型与返回类型只允许在引用类型上不同。

与所有其他隐式转换和显式转换一样，强制转换运算符可用于显式执行方法组转换。因此，示例

```
object obj = new EventHandler(myDialog.OkClick);
```

可以改为

```
object obj = (EventHandler)myDialog.OkClick;
```

方法组可能影响重载决策，并参与类型推断。有关更多详细信息，请参见 §7.5。

方法组转换的运行时求值过程如下：

- 如果编译时选择的方法是实例方法，或者它是作为实例方法访问的扩展方法，则委托的目标对象由与其关联的实例表达式确定：
  - 对实例表达式求值。如果此求值导致异常，则不执行后续步骤。
  - 如果实例表达式是引用类型，则实例表达式计算得到的值成为目标对象。如果所选方法是实例方法且目标对象为 null，则抛出 System.NullReferenceException，并且不执行后续步骤。
  - 如果实例表达式是值类型，则执行装箱操作（§4.3.1）将该值转换为对象，此对象成为目标对象。
- 否则，所选方法是静态方法调用的一部分，委托的目标对象为 null。
- 分配委托类型 D 的新实例。如果没有足够内存来分配新实例，则抛出 System.OutOfMemoryException，并且不执行后续步骤。

> > **JON SKEET** 规范在此处明确说明会创建新实例，这一事实阻止了一种潜在优化。如果匿名函数不捕获任何变量（包括 this），Microsoft C# 编译器能够缓存通过匿名函数创建的委托。对于通过任何选择静态方法的方法组转换创建的委托，同类缓存本来也是可行的——但规范禁止这样做。

- 新委托实例用对编译时确定的方法的引用和对上述计算出的目标对象的引用进行初始化。

# 7. 表达式

表达式是运算符和操作数的序列。本章定义表达式的语法、操作数和运算符的求值顺序，以及表达式的含义。

### 7.1 表达式分类

表达式分类为以下之一：

- 值。每个值都有一个关联类型。
- 变量。每个变量都有一个关联类型——即该变量的声明类型。

> > **VLADIMIR RESHETNIKOV** 在许多情况下，局部变量和 lambda 表达式参数的类型可由编译器推断，并且并不总是需要在声明中显式指定。

- 命名空间。具有此分类的表达式只能作为*成员访问*（§7.6.4）的左侧出现。在任何其他上下文中，分类为命名空间的表达式会导致编译时错误。
- 类型。具有此分类的表达式只能作为*成员访问*（§7.6.4）的左侧出现，或作为 as 运算符（§7.10.11）、is 运算符（§7.10.10）或 typeof 运算符（§7.6.11）的操作数出现。在任何其他上下文中，分类为类型的表达式会导致编译时错误。

> > **VLADIMIR RESHETNIKOV** 如果表达式分类为类型并作为*成员访问*的左侧出现，则它绝不表示数组或指针类型。如果该表达式表示类型参数，则它稍后总是会导致编译时错误。




- 方法组，即通过成员查找 (§7.4) 得到的一组重载方法。方法组可能具有关联的实例表达式和关联的类型参数列表。当实例方法被调用时，实例表达式求值的结果成为由 this 表示的实例 (§7.6.7)。方法组允许出现在调用表达式 (§7.6.5) 中、在委托创建表达式 (§7.6.10.5) 中，以及作为 is 运算符的左手侧，并且可以隐式转换为兼容的委托类型 (§6.6)。在任何其他上下文中，被归类为方法组的表达式会导致编译时错误。

> **ERIC LIPPERT** 方法组在 is 运算符的左手侧合法这一点有点具有误导性。is 评估的结果始终为 false，即使方法组可以转换为右手侧的类型。

> **VLADIMIR RESHETNIKOV** is 运算符左手侧的方法组不能在表达式树中使用。

- 空字面量。具有此分类的表达式可以隐式转换为引用类型或可空类型。

- 匿名函数。具有此分类的表达式可以隐式转换为兼容的委托类型或表达式树类型。

> **ERIC LIPPERT** 方法组、匿名函数和空字面量都是没有类型的表达式。这些不寻常的表达式只能在类型可以从上下文推断出来时使用。

- 属性访问。每个属性访问都有一个关联的类型——即属性的类型。此外，属性访问可能具有关联的实例表达式。当实例属性访问的访问器（get 或 set 块）被调用时，实例表达式求值的结果成为由 this 表示的实例 (§7.6.7)。

- 事件访问。每个事件访问都有一个关联的类型——即事件的类型。此外，事件访问可能具有关联的实例表达式。事件访问可以作为 += 和 -= 运算符 (§7.17.3) 的左手操作数出现。在任何其他上下文中，被归类为事件访问的表达式会导致编译时错误。

- 索引器访问。每个索引器访问都有一个关联的类型——即索引器的元素类型。此外，索引器访问具有关联的实例表达式和关联的参数列表。当索引器访问的访问器（get 或 set 块）被调用时，实例表达式求值的结果成为由 this 表示的实例 (§7.6.7)，并且参数列表求值的结果成为调用的参数列表。

- 无。这发生在表达式是对返回类型为 void 的方法调用时。被归类为无的表达式仅在语句表达式 (§8.6) 的上下文中有效。

表达式的最终结果永远不是命名空间、类型、方法组或事件访问。相反，如上所述，这些类别的表达式是仅在特定上下文中允许的中间构造。

属性访问或索引器访问总是通过调用 get 访问器或 set 访问器重新分类为值。特定访问器的确定取决于属性或索引器访问的上下文：如果访问是赋值的目标，则调用 set 访问器以分配新值 (§7.17.1)。否则，调用 get 访问器以获取当前值 (§7.1.1)。

### 7.1.1 表达式的值

大多数涉及表达式的构造最终要求表达式表示一个值。在这种情况下，如果实际表达式表示命名空间、类型、方法组或无，则会发生编译时错误。然而，如果表达式表示属性访问、索引器访问或变量，则会隐式替换属性、索引器或变量的值：

- 变量的值只是变量标识的存储位置当前存储的值。在获取变量的值之前，必须认为变量已被 definitely assigned (§5.3)；否则，会发生编译时错误。
- 属性访问表达式的值是通过调用属性的 get 访问器获得的。如果属性没有 get 访问器，则会发生编译时错误。否则，执行函数成员调用 (§7.5.4)，并且调用的结果成为属性访问表达式的值。
- 索引器访问表达式的值是通过调用索引器的 get 访问器获得的。如果索引器没有 get 访问器，则会发生编译时错误。否则，使用与索引器访问表达式关联的参数列表执行函数成员调用 (§7.5.4)，并且调用的结果成为索引器访问表达式的值。

> **Vladimir Reshetnikov** 如果属性或索引器具有 *get-accessor*，但访问器具有可访问性修饰符并且在当前上下文中不可访问，则会发生编译时错误。

## 7.2 静态绑定与动态绑定

根据构成表达式（参数、操作数、接收者）的类型或值确定操作的含义的过程通常称为 *binding*。例如，方法调用的含义是基于接收者和参数的类型确定的。运算符的含义是基于其操作数的类型确定的。

在 C# 中，操作的含义通常在编译时确定，基于其构成表达式的编译时类型。同样，如果表达式包含错误，错误会被编译器检测并报告。这种方法称为 *static binding*。

然而，如果表达式是 *dynamic expression*（即具有类型 `dynamic`），这表明其参与的任何绑定都应基于其运行时类型（即对象在运行时表示的 *actual type*），而不是其在编译时的类型。因此，此类操作的绑定被推迟到程序运行期间操作将被执行的时间。这称为 *dynamic binding*。

当操作被动态绑定时，编译器执行很少或不执行检查。相反，如果运行时绑定失败，则错误会作为异常在运行时报告。

以下 C# 操作受绑定影响：

- 成员访问：`e.M`
- 方法调用：`e.M(e, ..., e_n)`
- 委托调用：`e(e, ..., e_n)`
- 元素访问：`e[e, ..., e_n]`
- 对象创建：`new C(e, ..., e_n)`
- 重载的一元运算符：`+, -, !, ~, ++, --, true, false`
- 重载的二元运算符：`+, -, *, /, %, &, &&, |, ||, ?, ^, <<, >>, ==, !=, >, <, >=, <=`
- 赋值运算符：`=, +=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=`
- 隐式和显式转换

当不涉及动态表达式时，C# 默认使用静态绑定，这意味着构成表达式的编译时类型用于选择过程。然而，当上述操作中的一个构成表达式是动态表达式时，操作改为动态绑定。

### 7.2.1 绑定时间

静态绑定发生在编译时，而动态绑定发生在运行时。在以下各节中，术语 *binding time* 指绑定发生时的编译时或运行时。

以下示例说明了静态绑定和动态绑定以及绑定时间的概念：

```
object o = 5;
dynamic d = 5;

Console.WriteLine(5); // Static binding to Console.WriteLine(int)
Console.WriteLine(o); // Static binding to Console.WriteLine(object)
Console.WriteLine(d); // Dynamic binding to Console.WriteLine(int)
```

前两个调用是静态绑定的：`Console.WriteLine` 的重载是基于其参数的编译时类型选择的。因此绑定时间为 *compile time*。

第三个调用是动态绑定的：`Console.WriteLine` 的重载是基于其参数的运行时类型选择的。这是因为参数是动态表达式——其编译时类型为 `dynamic`。因此第三个调用的绑定时间为 *runtime*。

> **BILL WAGNER** 许多人将动态绑定与类型推断混淆。类型推断是静态绑定的。编译器在编译时确定类型。例如：
> 
> ```
> var i = 5;          // i is an int (Compiler performs type inference)
> Console.WriteLine(i); // Static binding to Console.WriteLine(int)
> ```
> 
> 编译器推断 `i` 为整数。对变量 `i` 的所有绑定都使用静态绑定。

### 7.2.2 动态绑定

动态绑定的目的是允许 C# 程序与 *dynamic objects* 交互——即不遵循 C# 类型系统正常规则的对象。动态对象可能是来自具有不同类型系统的其他编程语言的对象，也可能是以编程方式设置以对不同操作实现自己的绑定语义的对象。




> ERIC LIPPERT 这种对象的首要动机示例是（1）来自动态语言的对象，如 IronPython、IronRuby、JScript 等；（2）来自“expando”对象模型的对象，这些模型强调在运行时添加新属性，如 Internet Explorer 文档对象模型和其他基于标记的对象模型；以及（3）遗留的 COM 对象，如 Microsoft Office 对象模型。此处的意图是让专业的 C# 开发者更容易与这些系统互操作；我们的意图绝不是将 C# 变成像 JScript 那样的动态语言。

动态对象实现其自身语义的机制是实现定义的。动态对象实现一个给定的接口——同样是实现定义的——以向 C# 运行时发出信号，表明它们具有特殊语义。因此，只要对动态对象的操作是动态绑定的，其自身的绑定语义，而不是本文档中指定的 C# 语义，就会接管。

> ERIC LIPPERT Microsoft 对此功能的实现实际选择的机制与 IronPython 和其他 DLR 语言用于使其动态分析和分派高效的机制相同。动态操作会被编译成对 DLR 对象的方法的调用，这些方法随后使用 C# 表达式绑定器的特殊运行时版本来构建表示动态操作的表达式树。这些表达式树随后会被编译、缓存，并在下一次调用站点执行时重复使用。

虽然动态绑定的目的是允许与动态对象互操作，但 C# 允许对所有对象进行动态绑定，无论它们是否动态。这使得动态对象的集成更加顺畅，因为对其进行的运算结果可能本身不是动态对象，但仍是编译时程序员未知类型的对象。此外，动态绑定即使在涉及的对象都不是动态对象时，也有助于消除易出错的基于反射的代码。

> ERIC LIPPERT C# 已经支持一种动态方法分派形式：虚方法从技术上讲是一种动态分派形式，因为接收者的运行时类型用于精确确定要调用哪个方法。虽然我们不打算使 C# 成为动态语言（如我之前所述），但至少有一个编程问题中动态分派非常有用：“多重虚分派”问题。当你想根据许多参数的运行时类型（而不仅仅是接收者）来选择调用哪个方法时，就会产生此问题。（使用访问者模式实现“双重虚”分派并不困难，但对具有许多参数类型的方法实现运行时分派就会变得笨拙。）

以下各节针对语言中的每个构造，描述了动态绑定精确应用的时间、应用的编译时检查类型（如有）以及编译时结果和表达式分类。

## 7.2.3 构成表达式的类型

当操作是静态绑定时，构成表达式的类型（例如接收者、参数、索引或操作数）始终被视为该表达式的编译时类型。

当操作是动态绑定时，构成表达式的类型根据构成表达式的编译时类型以不同方式确定：

- 编译时类型为 dynamic 的构成表达式被认为具有该表达式在运行时求值时实际值的类型。

> **BILL WAGNER** 表达式的编译时类型为 dynamic 时使用实际运行时类型的规则会导致令人惊讶的行为，例如以下编译器错误：
> 
> ```
> public class Base
> {
>     public Base(dynamic parameter)
>     {
>     }
> }
> 
> public class Derived : Base
> {
>     public Derived(dynamic parameter) : base(parameter)
>     {
>     }
> }
> ```
> 
> 构造期间不允许动态分派，因此你必须强制对基构造函数调用进行静态分派。

- 编译时类型为类型参数的构成表达式被认为具有该类型参数在运行时绑定到的类型。

- 否则，构成表达式被认为具有其编译时类型。

## 7.3 运算符

表达式由 *操作数* 和 *运算符* 构成。表达式的运算符指示要对操作数应用哪些操作。运算符的示例包括 +、-、*、/ 和 new。操作数的示例包括字面量、字段、局部变量和表达式。

有三种类型的运算符：

- 一元运算符。一元运算符接受一个操作数，并使用前缀表示法（如 ~x）或后缀表示法（如 x++）。
- 二元运算符。二元运算符接受两个操作数，且全部使用中缀表示法（如 x + y）。
- 三元运算符。只有一个三元运算符 ?:；它接受三个操作数并使用中缀表示法（c ? x : y）。

表达式中运算符的求值顺序由运算符的 *优先级* 和 *结合性* 决定（§7.3.1）。

表达式中的操作数按从左到右的顺序求值。例如，在 F(i) + G(i++) * H(i) 中，方法 F 使用 i 的旧值调用，然后方法 G 使用 i 的旧值调用，最后方法 H 使用 i 的新值调用。这与运算符优先级无关且独立。

某些运算符可以被 *重载*。运算符重载允许为一个或两个操作数属于用户定义类或结构类型的操作指定用户定义的运算符实现（§7.3.2）。

### 7.3.1 运算符优先级和结合性

当表达式包含多个运算符时，运算符的 *优先级* 控制各个运算符求值的顺序。例如，表达式 x + y * z 被求值为 x + (y * z)，因为 * 运算符的优先级高于二元 + 运算符。运算符的优先级由其相关语法产生的定义确定。例如，一个 *加法表达式* 由 *乘法表达式* 序列组成，序列之间用 + 或 - 运算符分隔，从而使 + 和 - 运算符的优先级低于 *、/ 和 % 运算符。

下表按从高到低的优先级总结了所有运算符：

| 章节 | 类别 | 运算符 |
|---|---|---|
| 7.6 | 主 | `x.y` `f(x)` `a[x]` `x++` `x--` `new` `typeof` `default` `checked` `unchecked` `delegate` |
| 7.7 | 一元 | `+` `-` `!` `~` `++x` `--x` `(T)x` |
| 7.8 | 乘法 | `*` `/` `%` |
| 7.8 | 加法 | `+` `-` |
| 7.9 | 移位 | `<<` `>>` |
| 7.10 | 关系和类型测试 | `<` `>` `<=` `>=` `is` `as` |
| 7.10 | 相等 | `==` `!=` |
| 7.11 | 逻辑与 | `&` |
| 7.11 | 逻辑异或 | `^` |
| 7.11 | 逻辑或 | `|` |
| 7.11 | 条件与 | `&&` |
| 7.12 | 条件或 | `||` |
| 7.12 | 空合并 | `??` |
| 7.14 | 条件 | `?:` |
| 7.17, 7.15 | 赋值和 lambda 表达式 | `=` `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `&=` `^=` `|=` `=>` |

当一个操作数位于具有相同优先级的两个运算符之间时，运算符的结合性控制操作的执行顺序：

- 除赋值运算符外，所有二元运算符都是 *左结合* 的，这意味着操作从左到右执行。例如，`x + y + z` 被求值为 `(x + y) + z`。
- 赋值运算符和条件运算符（`?:`）是 *右结合* 的，这意味着操作从右到左执行。例如，`x = y = z` 被求值为 `x = (y = z)`。

优先级和结合性可以使用括号控制。例如，`x + y * z` 首先将 y 乘以 z，然后将结果加到 x 上，但 `(x + y) * z` 首先将 x 和 y 相加，然后将结果乘以 z。

> > **CHRIS SELLS**  我不太喜欢依赖运算符优先级来正确执行的程序。当执行顺序存在疑问时，请用括号将表达式括起来。括号不会影响编译输出（除非你修复了一个错误），但它们使代码对人类阅读者更容易理解。
> > **JESSE LIBERTY**  我认为再进一步 *始终* 用括号包裹表达式也没有害处。*你* 可能不会怀疑意图是什么，但维护你代码的程序员不应该查阅优先级才能理解代码。如果括号的数量本身变得令人困惑，请考虑使用临时中间变量将语句拆分为多个语句。
> > **ERIC LIPPERT**  优先级、结合性、括号和执行顺序之间的关系可能令人困惑。*操作数* 始终严格按从左到右的顺序求值。这些求值结果的组合方式受优先级、结合性和括号的影响。y 和 z 在 x 之前被求值的情况绝对 *不是* 如此。是的，乘法在加法之前计算，但 x 的求值发生在 *乘法之前*。

### 7.3.2 运算符重载

所有一元和二元运算符都有预定义实现，可在任何表达式中自动使用。除了预定义实现外，还可以通过在类和结构中包含运算符声明来引入用户定义实现（§10.10）。用户定义的运算符实现始终优先于预定义的运算符实现：只有在不存在适用的用户定义运算符实现时，才会考虑预定义的运算符实现，如 §7.3.3 和 §7.3.4 中所述。

*可重载的一元运算符* 是：

```
+   -   !   ~   ++   --   true   false
```



尽管 true 和 false 没有在表达式中显式使用（因此未包含在 §7.3.1 的优先级表中），但它们被视为运算符，因为它们会在若干表达式上下文中被调用：布尔表达式（§7.20）、涉及条件运算符的表达式（§7.14）以及条件逻辑运算符（§7.12）。

*可重载二元运算符* 包括：

+ - * / % & | ^ << >> == != > < >= <=

只有上面列出的运算符可以重载。特别地，不能重载成员访问、方法调用，或 =、&&、||、??、?:、=>、checked、unchecked、new、typeof、default、as 和 is 运算符。

当重载一个二元运算符时，对应的赋值运算符（如果有）也会被隐式重载。例如，运算符 * 的重载也是运算符 *= 的重载。§7.17.2 对此作了进一步描述。注意，赋值运算符本身（=）不能重载。赋值始终执行将值按位复制到变量中的简单操作。

强制转换操作（如 (T)x）通过提供用户定义转换（§6.4）来重载。

元素访问（如 a[x]）不被视为可重载运算符。相反，用户定义的索引通过索引器（§10.9）支持。

在表达式中，运算符使用运算符表示法引用；在声明中，运算符使用函数表示法引用。下表展示了一元和二元运算符的运算符表示法与函数表示法之间的关系。第一项中，*op* 表示任何可重载的一元前缀运算符。第二项中，*op* 表示一元后缀 ++ 和 -- 运算符。第三项中，*op* 表示任何可重载二元运算符。

| 运算符表示法 | 函数表示法 |
|---|---|
| `op x` | `operator op(x)` |
| `x op` | `operator op(x)` |
| `x op y` | `operator op(x, y)` |

用户定义的运算符声明始终要求至少有一个参数是包含该运算符声明的类或结构体类型。因此，用户定义的运算符不可能与预定义运算符具有相同的签名。

用户定义的运算符声明不能修改运算符的语法、优先级或结合性。例如，/ 运算符始终是二元运算符，始终具有 §7.3.1 中指定的优先级，并且始终是左结合的。

尽管用户定义的运算符可以执行任何它希望执行的计算，但强烈不鼓励产生不符合直觉预期结果的实现。例如，运算符 == 的实现应比较两个操作数是否相等，并返回适当的 bool 结果。

> > **比尔·瓦格纳**  除了遵循此规则外，还应将用户定义运算符的使用限制在操作对使用你代码的绝大多数开发人员都显而易见的时候。

> > **埃里克·利珀特**  可重载运算符本质上都是数学或逻辑运算符。如果你正在构建矩阵、向量等数学对象库，完全可以创建用户定义运算符。但请抵制创建“可爱”运算符的诱惑，例如“一个 Customer 加一个 Order 产生一个 Invoice”。

§7.6 至 §7.12 中对各个运算符的描述指定了运算符的预定义实现以及适用于每个运算符的任何附加规则。这些描述使用了 *一元运算符重载解析*、*二元运算符重载解析* 和 *数值提升* 这些术语，其定义见以下各节。

## 7.3.3 一元运算符重载解析

形式为 `op x` 或 `x op` 的操作（其中 *op* 是可重载一元运算符，x 是类型为 X 的表达式）按如下方式处理：

- 使用 §7.3.5 的规则确定 X 为操作 `operator op(x)` 提供的候选用户定义运算符集。
- 如果候选用户定义运算符集不为空，则它成为该操作的候选运算符集。否则，预定义一元运算符 `op` 实现（包括其提升形式）成为该操作的候选运算符集。给定运算符的预定义实现在该运算符的描述中指定（§7.6 和 §7.7）。
- 将 §7.5.3 的重载解析规则应用于候选运算符集，以针对参数列表 (x) 选择最佳运算符，该运算符成为重载解析过程的结果。如果重载解析未能选择单个最佳运算符，则发生绑定阶段错误。

## 7.3.4 二元运算符重载解析

形式为 x op y 的操作（其中 op 是可重载二元运算符，x 是类型为 X 的表达式，y 是类型为 Y 的表达式）按如下方式处理：

- 确定 X 和 Y 为操作 operator op(x, y) 提供的候选用户定义运算符集。该集合由 X 提供的候选运算符和 Y 提供的候选运算符的并集组成，二者分别使用 §7.3.5 的规则确定。如果 X 和 Y 是同一类型，或者 X 和 Y 派生自公共基类型，则共享的候选运算符在组合集中只出现一次。
- 如果候选用户定义运算符集不为空，则它成为该操作的候选运算符集。否则，预定义二元运算符 op 实现（包括其提升形式）成为该操作的候选运算符集。给定运算符的预定义实现在该运算符的描述中指定（§7.8 至 §7.12）。
- 将 §7.5.3 的重载解析规则应用于候选运算符集，以针对参数列表 (x, y) 选择最佳运算符，该运算符成为重载解析过程的结果。如果重载解析未能选择单个最佳运算符，则发生绑定阶段错误。

## 7.3.5 候选用户定义运算符

给定类型 T 和操作 operator op(A)（其中 op 是可重载运算符，A 是参数列表），T 为 operator op(A) 提供的候选用户定义运算符集按如下方式确定：

- 确定类型 T₀。如果 T 是可空类型，则 T₀ 是其基础类型；否则，T₀ 等于 T。
- 对于 T₀ 中的所有 operator op 声明以及此类运算符的所有提升形式，如果至少有一个运算符相对于参数列表 A 适用（§7.5.3.1），则候选运算符集由 T₀ 中所有此类适用运算符组成。
- 否则，如果 T₀ 是 object，则候选运算符集为空。
- 否则，T₀ 提供的候选运算符集是 T₀ 的直接基类提供的候选运算符集；如果 T₀ 是类型参数，则是 T₀ 的有效基类提供的候选运算符集。

## 7.3.6 数值提升

数值提升包括对预定义一元和二元数值运算符的操作数自动执行某些隐式转换。数值提升不是一种独立机制，而是对预定义运算符应用重载解析的效果。数值提升特别不影响用户定义运算符的求值，尽管用户定义运算符可以实现为表现出类似效果。

作为数值提升的一个例子，考虑二元 * 运算符的预定义实现：

```text
int operator *(int x, int y);
uint operator *(uint x, uint y);
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
float operator *(float x, float y);
double operator *(double x, double y);
decimal operator *(decimal x, decimal y);
```

当重载解析规则（§7.5.3）应用于这组运算符时，其效果是选择第一个存在从操作数类型隐式转换的运算符。例如，对于操作 b * s（其中 b 是 byte，s 是 short），重载解析选择 operator *(int, int) 作为最佳运算符。因此效果是 b 和 s 转换为 int，结果类型为 int。同样，对于操作 i * d（其中 i 是 int，d 是 double），重载解析选择 operator *(double, double) 作为最佳运算符。

### 7.3.6.1 一元数值提升

一元数值提升发生于预定义 +、- 和 ~ 一元运算符的操作数。一元数值提升仅包括将类型为 sbyte、byte、short、ushort 或 char 的操作数转换为类型 int。此外，对于一元 - 运算符，一元数值提升将类型为 uint 的操作数转换为类型 long。

### 7.3.6.2 二元数值提升

二元数值提升发生于预定义 +、-、*、/、%、&、|、^、==、!=、>、<、>= 和 <= 二元运算符的操作数。二元数值提升将两个操作数隐式转换为公共类型；对于非关系运算符，该公共类型也成为操作的结果类型。二元数值提升包括按此处出现的顺序应用以下规则：

- 如果任一操作数是 `decimal` 类型，则另一个操作数转换为 `decimal` 类型；如果另一个操作数是 `float` 或 `double` 类型，则发生绑定阶段错误。




-   否则，如果任一操作数是 double 类型，则另一个操作数会被转换为 double 类型。
-   否则，如果任一操作数是 float 类型，则另一个操作数会被转换为 float 类型。
-   否则，如果任一操作数是 ulong 类型，则另一个操作数会被转换为 ulong 类型，或者如果另一个操作数是 sbyte、short、int 或 long 类型，则会发生绑定时错误。
-   否则，如果任一操作数是 long 类型，则另一个操作数会被转换为 long 类型。
-   否则，如果任一操作数是 uint 类型且另一个操作数是 sbyte、short 或 int 类型，则两个操作数都将被转换为 long 类型。
-   否则，如果任一操作数是 uint 类型，则另一个操作数会被转换为 uint 类型。
-   否则，两个操作数都将被转换为 int 类型。

请注意，第一条规则禁止将 decimal 类型与 double 和 float 类型混合的任何操作。该规则源于 decimal 类型与 double 和 float 类型之间不存在隐式转换这一事实。

还请注意，不可能出现一个操作数是 ulong 类型而另一个操作数是有符号整数类型的情况。原因在于不存在一种整数类型能够同时表示 ulong 的完整范围以及有符号整数类型。

在上述两种情况下，都可以使用强制转换表达式显式地将一个操作数转换为与另一个操作数兼容的类型。

在示例中

```
decimal AddPercent(decimal x, double percent)
{
    return x * (1.0 + percent / 100.0);
}
```

会发生绑定时错误，因为 decimal 不能与 double 相乘。该错误可通过显式地将第二个操作数转换为 decimal 来解决，如下所示：

```
decimal AddPercent(decimal x, double percent)
{
    return x * (decimal)(1.0 + percent / 100.0);
}
```

> **JOSEPH ALBAHARI** 本节所述的预定义运算符始终会提升 8 位和 16 位整数类型——即 short、ushort、sbyte 和 byte。一个常见的陷阱是将这些类型上的计算结果赋回给 8 位或 16 位整数：

在这种情况下，变量 a 和 b 会被提升为 int，这要求代码能够编译时必须显式强制转换为 byte：

```
byte a = 1, b = 2;
byte c = a + b;    // Compile-time error
```

```
byte a = 1, b = 2;
byte c = (byte)(a + b);
```

## 7.3.7 提升的运算符

提升的运算符允许对非可空值类型操作的预定义和用户定义的运算符也用于这些类型的可空形式。提升的运算符由满足特定要求的预定义和用户定义运算符构造，如下列表所述：

-   对于一元运算符
  +   ++ - -- ! ~
  如果操作数类型和结果类型都是非可空值类型，则存在该运算符的提升形式。提升形式是通过在操作数类型和结果类型上添加单个 ? 修饰符构造的。如果操作数为 null，则提升的运算符会产生 null 值。否则，提升的运算符会解包操作数，应用底层运算符，并包装结果。
-   对于二元运算符
  +   - * / % & | ^ << >>
  如果操作数类型和结果类型都是非可空值类型，则存在该运算符的提升形式。提升形式是通过在每个操作数类型和结果类型上添加单个 ? 修饰符构造的。如果一个或两个操作数为 null，则提升的运算符会产生 null 值（bool? 类型的 & 和 | 运算符除外，如 §7.11.3 中所述）。否则，提升的运算符会解包操作数，应用底层运算符，并包装结果。
-   对于相等运算符
  == !=
  如果操作数类型都是非可空值类型且结果类型为 bool，则存在该运算符的提升形式。提升形式是通过在每个操作数类型上添加单个 ? 修饰符构造的。提升的运算符将两个 null 值视为相等，并将 null 值视为与任何非 null 值不相等。如果两个操作数都不是 null，则提升的运算符会解包操作数并应用底层运算符以产生 bool 结果。
-   对于关系运算符
  `< > <= >=`
  如果操作数类型都是非可空值类型且结果类型为 bool，则存在该运算符的提升形式。提升形式是通过在每个操作数类型上添加单个 ? 修饰符构造的。如果一个或两个操作数为 null，则提升的运算符会产生 false 值。否则，提升的运算符会解包操作数并应用底层运算符以产生 bool 结果。

> **BILL WAGNER** 任何可空类型的默认值既不大于也不小于包含值的可空类型。

## 7.4 成员查找

成员查找是确定名称在类型上下文中的含义的过程。成员查找可以在求值表达式中的简单名称 (§7.6.2) 或成员访问 (§7.6.4) 的过程中发生。如果简单名称或成员访问作为调用表达式 (§7.6.5.1) 的主表达式出现，则该成员被称为 *被调用的*。

如果成员是方法或事件，或者它是委托类型 (§15) 或 dynamic 类型 (§4.7) 的常量、字段或属性，则该成员被称为 *可调用的*。

成员查找不仅考虑成员的名称，还考虑成员具有的类型参数数量以及成员是否可访问。对于成员查找的目的，泛型方法和嵌套泛型类型具有在其各自声明中指示的类型参数数量，而所有其他成员的类型参数数量为零。

> **VLADIMIR RESHETNIKOV** 成员查找的结果永远不包含运算符、索引器、显式实现的接口成员、静态构造函数、实例构造函数、析构函数（终结器）或编译器生成的成员。尽管类型参数会贡献给其声明类型的声明空间，但它不是该类型的成员，因此不能成为成员查找的结果。

成员查找返回静态和实例成员，而不考虑访问形式。

在类型 T 中对具有 K 个类型参数的名称 N 进行成员查找的处理方式如下：

-   首先，确定一组可访问的名为 N 的成员：
  -   如果 T 是类型参数，则该集合是为 T 指定的每个作为主约束或次要约束 (§10.1.5) 的类型中可访问的名为 N 的成员集合的并集，以及 object 中可访问的名为 N 的成员集合。
  -   否则，该集合由 T 中所有可访问的 (§3.5) 名为 N 的成员组成，包括继承的成员和 object 中可访问的名为 N 的成员。如果 T 是构造类型，则成员集合是通过如 §10.3.2 所述替换类型参数获得的。包含 override 修饰符的成员被排除在集合之外。

-   接下来，如果 K 为零，则删除所有声明中包含类型参数的嵌套类型。如果 K 不为零，则删除所有类型参数数量不同的成员。请注意，当 K 为零时，具有类型参数的方法不会被删除，因为类型推断过程 (§7.5.2) 可能能够推断出类型参数。

-   接下来，如果成员是 *被调用的*，则从集合中删除所有非 *可调用的* 成员。

> VLADIMIR RESHETNIKOV 此规则允许你在类型 T 中存在同名非可调用实例成员时仍调用扩展方法。例如，即使集合具有类型为 int 的实例属性 Count，你也可以在该集合上调用扩展方法 Count()。

-   接下来，从集合中删除被其他成员隐藏的成员。对于集合中的每个成员 S.M，其中 S 是声明成员 M 的类型，应用以下规则：
  -   如果 M 是常量、字段、属性、事件或枚举成员，则从集合中删除在 S 的基类型中声明的所有成员。
  -   如果 M 是类型声明，则从集合中删除在 S 的基类型中声明的所有非类型，以及在 S 的基类型中声明的类型参数数量与 M 相同的类型声明。
  -   如果 M 是方法，则从集合中删除在 S 的基类型中声明的所有非方法成员。

> VLADIMIR RESHETNIKOV 在此步骤中从集合中删除的任何成员仍可能导致其他成员从集合中删除。因此，处理成员的顺序并不重要。



- 接下来，从集合中移除由类成员隐藏的接口成员。仅当 T 是类型参数，且 T 同时具有一个不是 object 的有效基类和一个非空的有效接口集（§10.1.5）时，此步骤才会生效。对于集合中的每个成员 S.M（其中 S 是声明成员 M 的类型），如果 S 是除 object 以外的类声明，则应用以下规则：
  - 如果 M 是常量、字段、属性、事件、枚举成员或类型声明，则从集合中移除在接口声明中声明的所有成员。
  - 如果 M 是方法，则从集合中移除在接口声明中声明的所有非方法成员，并且从集合中移除在接口声明中声明的所有与 M 具有相同签名的方法。

- 最后，在移除隐藏成员之后，确定查找的结果：
  - 如果该集合仅包含一个不是方法的成员，则该成员就是查找的结果。
  - 否则，如果该集合只包含方法，则这组方法就是查找的结果。
  - 否则，该查找是不明确的，并发生绑定期错误。

> VLADIMIR RESHETNIKOV  Microsoft C# 编译器在最后一种情况下更为宽松。如果集合同时包含方法和非方法，则会发出警告 CS0467，丢弃所有非方法，剩余的方法组成为查找的结果。此行为在某些 COM 互操作场景中很有用。

对于类型参数和接口以外的类型中的成员查找，以及在严格单继承的接口（继承链中的每个接口都恰好有零个或一个直接基接口）中的成员查找，查找规则的效果仅仅是派生成员隐藏具有相同名称或签名的基成员。此类单继承查找永远不会产生歧义。多继承接口中的成员查找可能引起的歧义在 §13.2.5 中描述。

## 7.4.1 基类型

为进行成员查找，类型 T 被视为具有以下基类型：

- 如果 T 是 object，则 T 没有基类型。
- 如果 T 是枚举类型，则 T 的基类型是类类型 System.Enum、System.ValueType 和 object。
- 如果 T 是 `struct-type`，则 T 的基类型是类类型 System.ValueType 和 object。
- 如果 T 是 `class-type`，则 T 的基类型是 T 的基类，包括类类型 object。
- 如果 T 是 `interface-type`，则 T 的基类型是 T 的基接口和类类型 object。

> ERIC LIPPERT 这一点确保：对接口类型的值调用 ToString() 以及 System.Object 的其他成员是合法的。在运行时，接口类型的任何值要么为 null，要么是继承自 System.Object 的某个对象，因此这是一个合理的选择。

- 如果 T 是 `array-type`，则 T 的基类型是类类型 System.Array 和 object。
- 如果 T 是 `delegate-type`，则 T 的基类型是类类型 System.Delegate 和 object。

## 7.5 函数成员

函数成员是包含可执行语句的成员。函数成员始终是类型的成员，不能是命名空间的成员。C# 定义了以下类别的函数成员：

- 方法
- 属性
- 事件
- 索引器
- 用户定义运算符
- 实例构造函数
- 静态构造函数
- 析构函数

除析构函数和静态构造函数（它们不能被显式调用）之外，函数成员中包含的语句通过函数成员调用来执行。编写函数成员调用的实际语法取决于特定的函数成员类别。

函数成员调用的参数列表（§7.5.1）为函数成员的参数提供实际值或变量引用。

泛型方法的调用可以采用类型推断来确定传递给方法的类型实参集。此过程在 §7.5.2 中描述。

方法、索引器、运算符和实例构造函数的调用采用重载决策来确定要调用候选函数成员集中的哪一个。此过程在 §7.5.3 中描述。

一旦在绑定期确定了某个特定函数成员（可能通过重载决策），调用该函数成员的实际运行时过程在 §7.5.4 中描述。

下表总结了涉及可显式调用的六类函数成员的构造中发生的处理。在下表中，e、x、y 和 value 表示归类为变量或值的表达式，T 表示归类为类型的表达式，F 是方法的简单名称，P 是属性的简单名称。

| 构造 | 示例 | 描述 |
|---|---|---|
| 方法调用 | F(x, y) | 应用重载决策来选择包含类或结构中的最佳方法 F。使用参数列表 (x, y) 调用该方法。如果方法不是静态的，则实例表达式为 this。 |
|  | T.F(x, y) | 应用重载决策来选择类或结构 T 中的最佳方法 F。如果方法不是静态的，则发生绑定期错误。使用参数列表 (x, y) 调用该方法。 |
|  | e.F(x, y) | 应用重载决策来选择由 e 的类型给定的类、结构或接口中的最佳方法 F。如果方法不是静态的，则发生绑定期错误。使用实例表达式 e 和参数列表 (x, y) 调用该方法。 |

| 构造 | 示例 | 描述 |
|---|---|---|
| 属性访问 | P | 调用包含类或结构中属性 P 的 get 访问器。如果 P 是只写的，则发生编译期错误。如果 P 不是静态的，则实例表达式为 this。 |
|  | P = value | 使用参数列表 (value) 调用包含类或结构中属性 P 的 set 访问器。如果 P 是只读的，则发生编译期错误。如果 P 不是静态的，则实例表达式为 this。 |
|  | T.P | 调用类或结构 T 中属性 P 的 get 访问器。如果 P 不是静态的，或者 P 是只写的，则发生编译期错误。 |
|  | T.P = value | 使用参数列表 (value) 调用类或结构 T 中属性 P 的 set 访问器。如果 P 不是静态的，或者 P 是只读的，则发生编译期错误。 |
|  | e.P | 使用实例表达式 e 调用由 e 的类型给定的类、结构或接口中属性 P 的 get 访问器。如果 P 是静态的，或者 P 是只写的，则发生绑定期错误。 |
|  | e.P = value | 使用实例表达式 e 和参数列表 (value) 调用由 e 的类型给定的类、结构或接口中属性 P 的 set 访问器。如果 P 是静态的，或者 P 是只读的，则发生绑定期错误。 |

## 7. 表达式

| 构造 | 示例 | 描述 |
|---|---|---|
| 事件访问 | `E += value` | 调用包含类或结构中事件 E 的 add 访问器。如果 E 不是静态的，则实例表达式为 this。 |
|  | `E -= value` | 调用包含类或结构中事件 E 的 remove 访问器。如果 E 不是静态的，则实例表达式为 this。 |
|  | `T.E += value` | 调用类或结构 T 中事件 E 的 add 访问器。如果 E 不是静态的，则发生绑定期错误。 |
|  | `T.E -= value` | 调用类或结构 T 中事件 E 的 remove 访问器。如果 E 不是静态的，则发生绑定期错误。 |
|  | `e.E += value` | 使用实例表达式 e 调用由 e 的类型给定的类、结构或接口中事件 E 的 add 访问器。如果 E 是静态的，则发生绑定期错误。 |
|  | `e.E -= value` | 使用实例表达式 e 调用由 e 的类型给定的类、结构或接口中事件 E 的 remove 访问器。如果 E 是静态的，则发生绑定期错误。 |
| 索引器访问 | `e[x, y]` | 应用重载决策来选择由 e 的类型给定的类、结构或接口中的最佳索引器。使用实例表达式 e 和参数列表 (x, y) 调用索引器的 get 访问器。如果索引器是只写的，则发生绑定期错误。 |
|  | `e[x, y] = value` | 应用重载决策来选择由 e 的类型给定的类、结构或接口中的最佳索引器。使用实例表达式 e 和参数列表 (x, y, value) 调用索引器的 set 访问器。如果索引器是只读的，则发生绑定期错误。 |

续



## 7. 表达式

| 构造 | 示例 | 描述 |
|---|---|---|
| 运算符调用 | `-x` | 重载解析应用于在由 `x` 的类型给出的类或结构体中选择最佳的一元运算符。所选运算符使用参数列表 (`x`) 被调用。 |
|  | `x + y` | 重载解析应用于在由 `x` 和 `y` 的类型给出的类或结构体中选择最佳的二元运算符。所选运算符使用参数列表 (`x`, `y`) 被调用。 |
| 实例构造函数调用 | `new T(x, y)` | 重载解析应用于在类或结构体 `T` 中选择最佳的实例构造函数。实例构造函数使用参数列表 (`x`, `y`) 被调用。 |

### 7.5.1 参数列表

每个函数成员和委托调用都包含一个参数列表，为函数成员的参数提供实际值或变量引用。函数成员调用的参数列表的指定语法取决于函数成员类别：

- 对于实例构造函数、方法、索引器和委托，参数指定为 *参数列表*，如下所述。对于索引器，在调用 set 访问器时，参数列表额外包含赋值运算符右操作数指定的表达式。

> **VLADIMIR RESHETNIKOV** 此额外参数不参与索引器的重载解析。

- 对于属性，在调用 get 访问器时参数列表为空，在调用 set 访问器时由赋值运算符右操作数指定的表达式组成。
- 对于事件，参数列表由 `+=` 或 `-=` 运算符右操作数指定的表达式组成。
- 对于用户定义运算符，参数列表由一元运算符的单个操作数或二元运算符的两个操作数组成。

属性 (§10.7)、事件 (§10.8) 和用户定义运算符 (§10.10) 的参数始终作为值参数 (§10.6.1.1) 传递。索引器 (§10.9) 的参数始终作为值参数 (§10.6.1.1) 或参数数组 (§10.6.1.4) 传递。对于这些类别的函数成员不支持引用和输出参数。

实例构造函数、方法、索引器或委托调用的参数指定为参数列表：

```
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

参数列表由一个或多个参数组成，以逗号分隔。每个参数由可选的参数名后跟参数值组成。带有参数名的参数称为命名参数，而不带参数名的参数为位置参数。在参数列表中，位置参数出现在命名参数之后是错误。

参数值可以采用以下形式之一：

- 一个表达式，表示参数作为值参数 (§10.6.1.1) 传递。
- 关键字 ref 后跟变量引用 (§5.4)，表示参数作为引用参数 (§10.6.1.2) 传递。变量必须在作为引用参数传递之前被明确赋值 (§5.3)。
- 关键字 out 后跟变量引用 (§5.4)，表示参数作为输出参数 (§10.6.1.3) 传递。变量在函数成员调用中作为输出参数传递后被视为已明确赋值 (§5.3)。

### 7.5.1.1 对应的参数

对于参数列表中的每个参数，被调用的函数成员或委托中必须有一个对应的参数。

以下使用的参数列表确定如下：

- 对于类中定义的虚方法和索引器，参数列表取自函数成员的最具体声明或重写，从接收者的静态类型开始，并在其基类中搜索。

> **ERIC LIPPERT** 这些规则处理不幸的（而且希望不太可能）情况，即你有一个虚方法——比如 void M(int x, int y)——和一个重写方法——比如 void M(int y, int x)。方法调用 M(y:1, x:2) 实际上调用 M(1, 2) 还是 M(2, 1)？参数名不是方法签名的一部分，因此在重载时可以更改。

- 对于接口方法和索引器，参数列表取自成员的最具体定义，从接口类型开始并在基接口中搜索。如果找不到唯一的参数列表，则构造一个具有不可访问名称且没有可选参数的参数列表，以便调用不能使用命名参数或省略可选参数。
- 对于部分方法，使用定义部分方法声明的参数列表。
- 对于所有其他函数成员和委托，只有一个参数列表，即所使用的参数列表。

参数或参数的位置定义为在参数列表或参数列表中在其之前出现的参数或参数的数量。

函数成员参数的对应参数确定如下：

- 实例构造函数、方法、索引器和委托的参数列表中的参数：
  - 在参数列表中同一位置出现固定参数的位置参数对应于该参数。
  - 在其正常形式中调用具有参数数组的函数成员的位置参数对应于参数数组，该参数数组必须在参数列表中处于同一位置。
  - 在其扩展形式中调用具有参数数组的函数成员的位置参数，在参数列表中同一位置没有固定参数时，对应于参数数组中的一个元素。
- 命名参数对应于参数列表中同名的参数。
- 对于索引器，在调用 set 访问器时，赋值运算符右操作数指定的表达式对应于 set 访问器声明的隐式值参数。
- 对于属性，在调用 get 访问器时没有参数。在调用 set 访问器时，赋值运算符右操作数指定的表达式对应于 set 访问器声明的隐式值参数。
- 对于用户定义的一元运算符（包括转换），单个操作数对应于运算符声明的单个参数。
- 对于用户定义的二元运算符，左操作数对应于第一个参数，右操作数对应于运算符声明的第二个参数。

### 7.5.1.2 参数列表的运行时求值

在函数成员调用 (§7.5.4) 的运行时处理期间，参数列表的表达式或变量引用按从左到右的顺序求值，如下所示：

- 对于值参数，参数表达式被求值并执行到对应参数类型的隐式转换 (§6.1)。 resulting 值成为函数成员调用中值参数的初始值。
- 对于引用或输出参数，变量引用被求值， resulting 存储位置成为函数成员调用中参数所表示的存储位置。如果作为引用或输出参数给出的变量引用是引用类型的数组元素，则会执行运行时检查以确保数组的元素类型与参数的类型相同。如果此检查失败，则会抛出 System.ArrayTypeMismatchException。

方法、索引器和实例构造函数可以将其最右边的参数声明为参数数组 (§10.6.1.4)。此类函数成员根据适用情况以其正常形式或扩展形式调用 (§7.5.3.1)：

- 当具有参数数组的函数成员以其正常形式调用时，为参数数组给出的参数必须是单个表达式，该表达式可隐式转换为 (§6.1) 参数数组类型。在这种情况下，参数数组完全像值参数一样起作用。
- 当具有参数数组的函数成员以其扩展形式调用时，调用必须为参数数组指定零个或多个位置参数，


其中每个实参都是可隐式转换（§6.1）为参数数组元素类型的表达式。在这种情况下，调用会创建参数数组类型的实例，其长度与实参数量相对应，用给定的实参值初始化该数组实例的元素，并将新创建的数组实例用作实际实参。

实参列表中的表达式总是按书写顺序求值。

因此，示例

```
class Test
{
    static void F(int x, int y = -1, int z = -2)
    {
        System.Console.WriteLine("x = {0}, y = {1}, z = {2}", x, y, z);
    }

    static void Main()
    {
        int i = 0;
        F(i++, i++, i++);
        F(z: i++, x: i++);
    }
}
```

生成输出

x = 0, y = 1, z = 2  
x = 4, y = -1, z = 3

数组协变规则（§12.5）允许数组类型 A[] 的值作为数组类型 B[] 实例的引用，前提是存在从 B 到 A 的隐式引用转换。由于这些规则，当引用类型的数组元素作为引用或输出参数传递时，需要运行时检查以确保数组的实际元素类型与参数的元素类型相同。在示例

```
class Test
{
    static void F(ref object x) {...}
    static void Main()
    {
        object[] a = new object[10];
        object[] b = new string[10];
        F(ref a[0]);    // Okay
        F(ref b[1]);    // ArrayTypeMismatchException
    }
}
```

中，第二次调用 F 会引发 System.ArrayTypeMismatchException，因为 b 的实际元素类型是 string 而不是 object。

当以展开形式调用带有参数数组的函数成员时，调用的处理方式完全如同在展开的参数周围插入了一个带数组初始化器（§7.6.10.4）的数组创建表达式。例如，给定声明

```
void F(int x, int y, params object[] args);
```

以下对该方法展开形式的调用

```
F(10, 20);
F(10, 20, 30, 40);
F(10, 20, 1, "hello", 3.0);
```

完全对应于

```
F(10, 20, new object[] { });
F(10, 20, new object[] { 30, 40 });
F(10, 20, new object[] { 1, "hello", 3.0 });
```

特别要注意，当为参数数组提供零个实参时，会创建一个空数组。

当从具有对应可选参数的函数成员中省略实参时，会隐式传递该函数成员声明的默认实参。由于这些默认实参始终是常量，对它们的求值不会影响其余实参的求值顺序。

### 7.5.2 类型推断

当调用泛型方法而未指定类型实参时，类型推断过程会尝试为该调用推断类型实参。类型推断的存在允许使用更方便的语法调用泛型方法，并使程序员能够避免指定冗余的类型信息。例如，给定方法声明

```
class Chooser
{
    static Random rand = new Random();
    public static T Choose<T>(T first, T second)
    {
        return (rand.Next(2) == 0) ? first : second;
    }
}
```

可以在不显式指定类型实参的情况下调用 Choose 方法：

```
int i = Chooser.Choose(5, 213);    // Calls Choose<int>
string s = Chooser.Choose("foo", "bar"); // Calls Choose<string>
```

通过类型推断，类型实参 int 和 string 由方法的实参确定。

> JON SKEET 有时，我会尝试针对一些行为不符合我预期的特定情况推演类型推断算法。我几乎总是后悔这么做，因为推演完之后我比之前更困惑了。这感觉有点像进入一座迷宫，希望能在中心找到宝藏（合适的类型实参），但通常会在途中遇到弥诺陶洛斯。我对那些不仅能在算法中游刃有余，还能在编译器中实现它的人深感敬佩。

> CHRIS SELLS 如果理解你的代码感觉像在迷宫中穿行，那说明你做错了什么。

类型推断作为方法调用（§7.6.5.1）绑定期处理的一部分发生，并且发生在该调用的重载决策步骤之前。当在方法调用中指定了特定方法组，并且未在该方法调用中指定类型实参时，会对该方法组中的每个泛型方法应用类型推断。如果类型推断成功，则使用推断出的类型实参来确定后续重载决策的实参类型。如果重载决策选择某个泛型方法作为要调用的方法，则推断出的类型实参将用作该调用的实际类型实参。如果对特定方法的类型推断失败，则该方法不参与重载决策。类型推断失败本身不会导致绑定期错误。但是，当重载决策随后找不到任何适用方法时，它通常会导致绑定期错误。

> ERIC LIPPERT 类型推断算法不保证产生适用的候选。（当然，重载决策会剔除不适用的候选。）类型推断算法旨在回答一个问题：仅给定实参和形参类型，对于每个类型参数，能够推断出的最佳类型实参是什么？如果最佳推断产生不适用的候选，那么我们不会回溯并试图猜测用户“真正”想表达什么，以便让推断选择不同的值。

> MAREK SAFAR 当类型推断成功但重载决策失败时，罪魁祸首可能是使用了约束的推断类型参数。类型推断算法忽略类型参数约束，将验证最佳候选的工作留给重载决策。

如果提供的实参数量与方法中的参数数量不同，则推断立即失败。否则，假定该泛型方法具有以下签名：

```
T₁ M<X₁...Xₙ>(T₁ X₁ ... Tₙ Xₙ)
```

对于形式为 M(E₁ ... Eₙ) 的方法调用，类型推断的任务是为每个类型参数 X₁ ... Xₙ 找到唯一的类型实参 S₁ ... Sₙ，使得调用 M<S₁ ... Sₙ>(E₁ ... Eₙ) 变得有效。

> VLADIMIR RESHETNIKOV 尽管这里没有明确说明，但签名可以具有 ref/out 参数。

在推断过程中，每个类型参数 Xᵢ 要么固定为特定类型 Sᵢ，要么未固定并关联一组边界。每个边界都是某个类型 T。最初，每个类型变量 Xᵢ 都是未固定的，并具有空边界集。

类型推断分阶段进行。每个阶段都会根据前一阶段的发现尝试为更多类型变量推断类型实参。第一阶段进行一些初始的边界推断，而第二阶段将类型变量固定为特定类型并推断进一步的边界。第二阶段可能需要重复多次。

注意：类型推断发生的情况不止调用泛型方法时。方法组转换的类型推断在 §7.5.2.13 中描述，而查找一组表达式的最佳公共类型在 §7.5.2.14 中描述。

> ERIC LIPPERT 语言设计团队偶尔会被问到：“你们为什么发明自己的类型推断算法，而不是使用 Hindley–Milner 风格的算法？”简短的回答是：(1) Hindley–Milner 风格的算法难以适应具有基于类的继承和协变类型的语言；(2) 回溯算法可能执行非常长的时间。
>
> 我们的类型推断算法旨在处理继承和类型变体。由于第二阶段的每次迭代要么将一个额外的类型参数“固定”为其推断类型，要么在无法做到时失败，因此显然类型推断过程会在相当短的时间内终止。



> PETER SESTOFT 虽然可能并非本意，前面的注释可能会让人产生一种印象，即对于 Hindley–Milner 风格的类型系统（即 ML let 多态）的类型推断算法必须使用回溯。特别是，Damas–Milner 算法（1978）不使用回溯。话虽如此，使用回溯对于 C# 类型推断来说是过度设计，因为在 C# 中所有类型参数都必须显式指定。相比之下，Damas–Milner 算法会发明足够多的类型参数以找到给定表达式的最一般（“主”）类型。该问题已知是关于指数时间的完备问题。

## 7.5.2.1 第一阶段

对于每个方法参数 E_i：

- 如果 E_i 是一个匿名函数，则从 E_i 到 T_i 进行显式参数类型推断（§7.5.2.7）。
- 否则，如果 E_i 具有类型 U 且 x_i 是值参数，则从 U 到 T_i 进行下界推断。
- 否则，如果 E_i 具有类型 U 且 x_i 是 ref 或 out 参数，则从 U 到 T_i 进行精确推断。
- 否则，对此参数不进行推断。

## 7.5.2.2 第二阶段

第二阶段按如下方式进行：

- 所有不依赖于（§7.5.2.5）任何 X_j 的未固定类型变量 X_i 均被固定（§7.5.2.10）。
- 如果不存在此类类型变量，则对所有满足以下两个条件的未固定类型变量 X_i 进行固定：
  - 存在至少一个依赖于 X_i 的类型变量 X_j。
  - X_i 具有非空的边界集合。
- 如果不存在此类类型变量且仍有未固定的类型变量，则类型推断失败。
- 否则，如果不存在进一步的未固定类型变量，则类型推断成功。
- 否则，对于所有参数类型为 T_i 的参数 E_i，其中输出类型（§7.5.2.4）包含未固定的类型变量 X_i 但输入类型（§7.5.2.3）不包含，则从 E_i 到 T_i 进行输出类型推断（§7.5.2.6）。然后重复第二阶段。

## 7.5.2.3 输入类型

如果 E 是方法组或隐式类型匿名函数且 T 是委托类型或表达式树类型，则 T 的所有参数类型都是 E *的输入类型* *类型为* T。

## 7.5.2.4 输出类型

如果 E 是方法组或匿名函数且 T 是委托类型或表达式树类型，则 T 的返回类型是 E *的输出类型* *类型为* T。

## 7.5.2.5 依赖关系

未固定类型变量 X_i 直接依赖于未固定类型变量 X_j，如果对于某个具有类型 T_i 的参数 E_i，X_j 出现在 E_i *的类型为* T_i 的 *输入类型* 中且 X_j 出现在 E_i *的类型为* T_i 的 *输出类型* 中。

X_i 依赖于 X_j，如果 X_i 直接依赖于 X_j，或者 X_i 直接依赖于 X_k 且 X_k 直接依赖于 X_j。因此“依赖于”是“直接依赖于”的传递但非自反闭包。

> > **VLADIMIR RESHETNIKOV** 类型参数可能直接或间接地依赖于自身。

## 7.5.2.6 输出类型推断

从表达式 E 到类型 T 进行 *输出类型推断* 如下：

- 如果 E 是一个具有推断返回类型 U（§7.5.2.12）的匿名函数且 T 是具有返回类型 T_b 的委托类型或表达式树类型，则进行从 U *到* T_b 的 *下界推断*（§7.5.2.9）。
- 否则，如果 E 是方法组且 T 是具有参数类型 T_1…T_k 和返回类型 T_b 的委托类型或表达式树类型，并且 E 与类型 T_1…T_k 的重载解析产生具有返回类型 U 的单个方法，则进行从 U *到* T_b 的 *下界推断*。

> > **VLADIMIR RESHETNIKOV** 此步骤仅在委托参数类型中出现的所有方法类型参数都已固定的情况下适用。重载解析不会尝试基于不完整类型信息选择最佳方法。

- 否则，如果 E 是具有类型 U 的表达式，则进行从 U *到* T 的 *下界推断*。
- 否则，不进行推断。

## 7.5.2.7 显式参数类型推断

从表达式 E 到类型 T 进行显式参数类型推断如下：

- 如果 E 是具有参数类型 U₁...Uₖ 的显式类型匿名函数且 T 是具有参数类型 V₁...Vᵣ 的委托类型或表达式树类型，则对每个 Uᵢ 从 Uᵢ 到对应的 Vᵢ 进行精确推断（§7.5.2.8）。

## 7.5.2.8 精确推断

从类型 U 到类型 V 的精确推断如下进行：

- 如果 V 是未固定的 X_i 之一，则 U 被添加到 X_i 的精确边界集合中。
- 否则，通过检查以下任何情况是否适用来确定集合 V₁...Vₖ 和 U₁...Uᵢ：
  - V 是数组类型 V₁[...] 且 U 是相同秩的数组类型 U₁[...]。
  - V 是类型 V? 且 U 是类型 U?。
  - V 是构造类型 C<V₁...Vₖ> 且 U 是构造类型 C<U₁...Uₖ>。
- 如果其中任何一种情况适用，则对每个 Uᵢ 到对应的 Vᵢ 进行精确推断。
- 否则，不进行推断。

## 7.5.2.9 下界推断

从类型 U 到类型 V 的下界推断如下进行：

- 如果 V 是未固定的 X_i 之一，则 U 被添加到 X_i 的下界集合中。
- 否则，通过检查以下任何情况是否适用来确定集合 U₁...Uₖ 和 V₁...Vₖ：
  - V 是数组类型 V₁[...] 且 U 是数组类型 U₁[...]（或有效基类型为 U₁[...] 的类型参数）且秩相同。
  - V 是 IEnumerable<V₁>、ICollection<V₁> 或 IList<V₁> 之一，且 U 是单维数组类型 U₁[]（或有效基类型为 U₁[] 的类型参数）。
> VLADIMIR RESHETNIKOV 当然，本条（以及下一段中对应的条目）提到了 System.Collections.Generic 命名空间中的接口。
  - V 是类型 V₁? 且 U 是类型 U₁?。
  - V 是构造的类、结构、接口或委托类型 C<V₁...Vₙ>，并且存在唯一的 C<U₁...Uₙ> 类型，使得 U（或如果 U 是类型参数，则其有效基类或其有效接口集合的任何成员）与 C<U₁...Uₙ> 相同、继承自（直接或间接）或实现（直接或间接）C<U₁...Uₙ>。

（“唯一性”限制意味着在接口 C<T>{ 类 U: C<X>, C<Y>{} 的情况下，从 U 推断到 C<T> 时不进行推断，因为 Uᵢ 可能是 X 或 Y。）

> **VLADIMIR RESHETNIKOV** 相同的推断规则适用于构造的枚举类型。尽管枚举类型在其声明中不能具有类型参数，但如果嵌套在泛型类或结构类型中，它们仍然可以是泛型的。

如果其中任何一种情况适用，则对每个 Uᵢ 到对应的 Vᵢ 进行推断如下：

- 如果 Uᵢ 不被已知为引用类型，则进行 *精确推断*。
- 否则，如果 U 是数组类型，则进行 *下界推断*。
- 否则，如果 V 是 C<V₁...Vₙ>，则推断取决于 C 的第 i 个类型参数：
  - 如果它是协变的，则进行 *下界推断*。
  - 如果它是逆变的，则进行 *上界推断*。
  - 如果它是不可变的，则进行 *精确推断*。
- 否则，不进行推断。

## 7.5.2.10 上界推断

从类型 U 到类型 V 的上界推断如下进行：

- 如果 V 是未固定的 X_i 之一，则 U 被添加到 X_i 的上界集合中。
- 否则，通过检查以下任何情况是否适用来确定集合 V₁...Vₙ 和 U₁...Uₙ：
  - U 是数组类型 Uᵢ[...] 且 V 是相同秩的数组类型 Vᵢ[...]。
  - U 是 IEnumerable<Uᵢ>、ICollection<Uᵢ> 或 IList<Uᵢ> 之一，且 V 是单维数组类型 Vᵢ[]。
  - U 是类型 Uᵢ? 且 V 是类型 Vᵢ?。



U 是构造的类、结构体、接口或委托类型 C<U1, ..., Un>，而 V 是类、结构体、接口或委托类型，其与唯一类型 C<V1, ..., Vn> 相同、继承自（直接或间接）或实现（直接或间接）该类型。

（“唯一性”限制意味着如果我们有接口 C<T>{} 类 V<Z>: C<X<Z>>, C<V<Z>>{}，则在从 C<U> 推断到 V<Q> 时不进行推断。不会从 U1 推断到 X<Q> 或 V<Q>。）

如果适用上述任一情况，则按如下方式从每个 Ui 推断到对应的 Vi：

- 如果不知道 Ui 是引用类型，则进行精确推断。
- 否则，如果 V 是数组类型，则进行上界推断。
- 否则，如果 U 是 C<U1, ..., Un>，则推断取决于 C 的第 i 个类型参数：
  - 如果它是协变的，则进行上界推断。
  - 如果它是逆变的，则进行下界推断。
  - 如果它是不可变的，则进行精确推断。
- 否则，不进行推断。

> **VLADIMIR RESHETNIKOV** 因此，对于在泛型方法参数类型中未出现的 方法类型参数，永远不会进行推断。例如，对于仅出现在约束中的参数，不会进行推断：
> 
> ```csharp
> using System.Collections.Generic;
> 
> class C
> {
>     static void Foo<T,U>(T x) where T : IEnumerable<U> { }
> 
>     static void Main()
>     {
>         Foo(new List<int>());
>         // Error CS0411: The type arguments for method
>         // 'C.Foo<T,U>(T)' cannot be inferred from the
>         // usage.
>     }
> }
> ```

## 7.5.2.11 Fixing

未固定的类型变量 Xi 及其一组边界的固定方式如下：

- 候选类型 Uj 的集合最初为 Xi 边界集合中的所有类型的集合。

> **ERIC LIPPERT**  此条件说明了 C# 的一个微妙设计点。面对给定一组类型时需要选择“最佳类型”的情况，我们总是从该集合中选择一种类型。也就是说，如果要求在 `{Cat, Dog, Goldfish}` 中选择最佳类型，我们将找不到最佳类型；我们永远不会说，“鉴于这三个选择，公共基类型 Animal 是我们能做到的最好”，因为 Animal 首先就不是选择之一。

- 然后我们依次检查 xᵢ 的每个边界：对于每个边界 U of xᵢ，所有不与 U 相同的类型 Uⱼ 都从候选集合中移除。对于每个下界 U of xᵢ，所有不存在从 U 到 Uⱼ 的隐式转换的类型 Uⱼ 都从候选集合中移除。对于每个上界 U of xᵢ，所有不存在从 Uⱼ 到 U 的隐式转换的类型 Uⱼ 都从候选集合中移除。
- 如果在剩余的候选类型 Uⱼ 中存在唯一的类型 V，可以隐式转换为所有其他候选类型，则将 xᵢ 固定为 V。
- 否则，类型推断失败。

> **ERIC LIPPERT**  在 C# 2.0 中，如果为同一类型参数计算出两个不同的边界，则泛型方法类型推断算法会失败。在 C# 3.0 中，我们有 Join 方法等情况，必须推断两个集合连接的“键”的类型。如果一个集合中的键是， say， `int`，而另一个集合中对应的键是 `int?`，则我们有两个不同的类型。然而，由于每个 int 都可以转换为 int?，我们可以允许这种歧义并通过选择两者中更通用的类型来解决它。C# 4.0 支持泛型协变，这进一步复杂化了情况；现在我们可能对类型参数具有上界、下界和精确边界。

## 7.5.2.12 Inferred Return Type

匿名函数 F 的 *推断返回类型* 在类型推断和重载解析期间使用。推断返回类型只能针对所有参数类型已知的匿名函数确定，这些参数类型要么是显式给出的，要么是通过匿名函数转换提供的，要么是在封闭泛型方法调用的类型推断期间推断出来的。推断返回类型按如下方式确定：

- 如果 F 的主体是 *表达式*，则 F 的推断返回类型为该表达式的类型。
- 如果 F 的主体是 *块* 并且块的 return 语句中表达式集合具有最佳公共类型 T (§7.5.2.14)，则 F 的推断返回类型为 T。

![](img/04b421b044b1254de966ab5335775a89_284_0.png)

> > **VLADIMIR RESHETNIKOV** 即使不可达代码中的 return 语句也被包含在集合中并参与推断返回类型的计算。这有一个令人惊讶的后果，即删除不可达代码可能会改变程序行为。

- 否则，无法为 F 推断返回类型。

作为涉及匿名函数的类型推断的示例，请考虑在 `System.Linq.Enumerable` 类中声明的 `Select` 扩展方法：

```
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource, TResult>(
            this IEnumerable<TSource> source,
            Func<TSource, TResult> selector)
        {
            foreach (TSource element in source)
                yield return selector(element);
        }
    }
}
```

假设已通过 using 子句导入 `System.Linq` 命名空间，并且给定一个 Name 属性类型为 string 的 Customer 类，则可以使用 Select 方法选择客户列表的名称：

```
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

Select 的扩展方法调用 (§7.6.5.2) 通过重写调用为静态方法调用来处理：

```
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

由于未显式指定类型参数，因此使用类型推断来推断类型参数。首先，将 customers 参数与 source 参数关联，推断 T 为 Customer。然后，使用上面描述的匿名函数类型推断过程，c 被赋予 Customer 类型，并且表达式 c.Name 与 selector 参数的返回类型关联，推断 S 为 string。因此，该调用等价于

```
Enumerable.Select<Customer,string>(customers, (Customer c) => c.Name)
```

并且结果的类型为 `IEnumerable<string>`。

以下示例演示了匿名函数类型推断如何允许类型信息在泛型方法调用的参数之间“流动”。给定方法

```
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2) {
    return f2(f1(value));
}
```

对调用的类型推断

```
double seconds = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalSeconds);
```

进行如下：首先，将参数 “1:15:30” 与 value 参数关联，推断 X 为 string。然后，将第一个匿名函数的参数 s 赋予推断出的 string 类型，并且表达式 TimeSpan.Parse(s) 与 f1 的返回类型关联，推断 Y 为 System.TimeSpan。最后，将第二个匿名函数的参数 t 赋予推断出的 System.TimeSpan 类型，并且表达式 t.TotalSeconds 与 f2 的返回类型关联，推断 Z 为 double。因此，该调用的结果类型为 double。

## 7.5.2.13 Type Inference for Conversion of Method Groups

与泛型方法调用类似，当包含泛型方法的 方法组 M 转换为给定的委托类型 D (§6.6) 时，也必须应用类型推断。给定方法

T_r M<X_1...X_n>(T_1 x_1 ... T_n x_n)

并且方法组 M 被赋给委托类型 D，类型推断的任务是找到类型参数 S_1...S_n，使得表达式

M<S_1...S_n>

与 D 兼容 (§15.1)。

与泛型方法调用的类型推断算法不同，在这种情况下只有参数类型——没有参数表达式。特别是，没有匿名函数，因此不需要多阶段推断。

相反，所有 X_i 都被视为未固定，并且从 D 的每个参数类型 U_i 到 M 的对应参数类型 T_i 进行下界推断。如果对于任何 X_i 未找到边界，则类型推断失败。否则，所有 X_i 都被固定为对应的 S_i，即类型推断的结果。




## 7.5.2.14 查找一组表达式的最佳公共类型

在某些情况下，需要为一组表达式推断一个公共类型。特别是，隐式类型化数组的元素类型和带块体的匿名函数的返回类型就是以这种方式找到的。

直观地说，给定一组表达式 E1 ... En，这种推断应等价于调用一个方法

```
T M<X>(X x1 ... X xn)
```

并以 E1 ... En 作为实参。

更准确地说，该推断从某个未固定类型变量 X 开始。然后从每个 Ei 到 X 进行输出类型推断。最后，X 被固定；如果成功，得到的类型 S 就是这些表达式最终的最佳公共类型。如果不存在这样的 S，则这些表达式没有最佳公共类型。

## 7.5.3 重载决策

重载决策是一种绑定期机制，用于在给定实参列表和一组候选函数成员的情况下，选择要调用的最佳函数成员。在 C# 中的以下不同上下文中，重载决策选择要调用的函数成员：

- 调用调用表达式中指定的方法（§7.6.5.1）。
- 调用对象创建表达式中指定的实例构造函数（§7.6.10.1）。
- 通过元素访问调用索引器访问器（§7.6.6）。
- 调用表达式中引用的预定义或用户定义运算符（§7.3.3 和 §7.3.4）。

> 弗拉基米尔·列舍特尼科夫 同样的规则也适用于特性规范中特性实例构造函数的选择、构造函数初始化器中实例构造函数的调用，以及通过基类访问调用索引器。

这些上下文各自以独特的方式定义候选函数成员集合和实参列表，具体描述见上文列出的各节。例如，方法调用的候选集合不包括标记为 override 的方法（§7.4）；如果派生类中的任何方法适用，则基类中的方法不是候选（§7.6.5.1）。

一旦确定了候选函数成员和实参列表，在所有情况下选择最佳函数成员的过程都相同：

- 给定适用候选函数成员的集合，定位该集合中的最佳函数成员。如果该集合只包含一个函数成员，则该函数成员就是最佳函数成员。否则，最佳函数成员是相对于给定实参列表比所有其他函数成员都更佳的那一个函数成员，前提是使用 §7.5.3.2 中的规则将每个函数成员与所有其他函数成员进行比较。如果并非恰好存在一个比所有其他函数成员都更佳的函数成员，则函数成员调用有歧义，并发生绑定期错误。

以下各节定义术语 *适用函数成员* 和 *更佳函数成员* 的确切含义。

> > **比尔·瓦格纳**   本节变得非常复杂。阅读时请记住，你创建的每个额外重载都可能造成重载决策中可能的歧义。你应将自己限制在真正能让用户更轻松的重载数量上。这种做法将为类的用户尽可能保持简单，并帮助他们确保获得正确的方法。

### 7.5.3.1 适用函数成员

> > **弗拉基米尔·列舍特尼科夫**   本节还规定委托的适用性（§7.6.5.3）。

当以下所有条件都成立时，称函数成员相对于实参列表 A 是一个 *适用函数成员*：

- A 中的每个实参都按 §7.5.1.1 所述对应于函数成员声明中的某个参数，并且任何没有对应实参的参数都是可选参数。
- 对于 A 中的每个实参，该实参的参数传递模式（即 *值*、*ref* 或 *out*）与对应参数的参数传递模式相同，并且
  - 对于 *值* 参数或参数数组，存在从该实参到对应参数类型的隐式转换（§6.1），或者
  - 对于 *ref* 或 *out* 参数，该实参的类型与对应参数的类型相同。毕竟，*ref* 或 *out* 参数是所传递实参的别名。

包含参数数组的函数成员，如果按上述规则适用，则称其以正常形式适用。如果包含参数数组的函数成员在其正常形式下不适用，则该函数成员可能改为以其展开形式适用：

- 展开形式的构造方式是：将函数成员声明中的参数数组替换为零个或多个该参数数组元素类型的值参数，使实参列表 A 中的实参数量与参数总数相匹配。如果 A 的实参数量少于函数成员声明中的固定参数数量，则无法构造该函数成员的展开形式，因此该形式不适用。
- 否则，如果对于 A 中的每个实参，该实参的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定值参数或由展开创建的值参数，存在从该实参的类型到对应参数类型的隐式转换（§6.1），或者
  - 对于 ref 或 out 参数，该实参的类型与对应参数的类型相同，则展开形式适用。

### 7.5.3.2 更佳函数成员

为了确定更佳函数成员，会构造一个精简的实参列表 A，其中仅包含实参表达式本身，并按其出现在原始实参列表中的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 没有对应实参的可选参数从参数列表中移除。
- 对参数重新排序，使其出现在与实参列表中对应实参相同的位置。

给定实参列表 A，其包含一组实参表达式 { E₁, E₂, ..., Eₙ }，以及两个适用函数成员 Mₐ 和 M_b，其参数类型分别为 { P₁, P₂, ..., Pₙ } 和 { Q₁, Q₂, ..., Qₙ }，如果满足以下条件，则定义 Mₐ 是比 M_b 更佳的函数成员：

- 对于每个实参，从 E_x 到 Q_x 的隐式转换都不比从 E_x 到 P_x 的隐式转换更佳，并且
- 对于至少一个实参，从 E_x 到 P_x 的转换比从 E_x 到 Q_x 的转换更佳。

执行此评估时，如果 M_x 或 M_y 以其展开形式适用，则 P_x 或 Q_x 指的是参数列表展开形式中的参数。

如果参数类型序列 {P_1, P_2, ..., P_v} 和 {Q_1, Q_2, ..., Q_v} 等效（即每个 P_i 到对应的 Q_i 都有恒等转换），则按顺序应用以下平局决胜规则来确定更佳函数成员：

- 如果 M_p 是非泛型方法，而 M_q 是泛型方法，则 M_p 比 M_q 更佳。
- 否则，如果 M_p 以其正常形式适用，而 M_q 具有 params 数组且仅以其展开形式适用，则 M_p 比 M_q 更佳。
- 否则，如果 M_p 声明的参数数量多于 M_q，则 M_p 比 M_q 更佳。当两个方法都具有 params 数组且仅在展开形式下适用时，就可能发生这种情况。
- 否则，如果 M_p 的所有参数都有对应实参，而 M_q 中至少有一个可选参数需要代入默认实参，则 M_p 比 M_q 更佳。
- 否则，如果 M_p 的参数类型比 M_q 更特定，则 M_p 比 M_q 更佳。令 {R_1, R_2, ..., R_v} 和 {S_1, S_2, ..., S_v} 表示 M_p 和 M_q 的未实例化且未展开的参数类型。如果对于每个参数，R_x 都不比 S_x 更不特定，并且对于至少一个参数，R_x 比 S_x 更特定，则 M_p 的参数类型比 M_q 的参数类型更特定：
  - 类型参数比非类型参数更不特定。
  - 递归地，如果一个构造类型至少有一个类型实参更特定，且没有任何类型实参比另一个构造类型中对应的类型实参更不特定，则该构造类型比另一个构造类型（具有相同数量的类型实参）更特定。
  - 如果一个数组类型的元素类型比另一个数组类型（具有相同维数）的元素类型更特定，则该数组类型比另一个数组类型更特定。
- 否则，如果一个成员是非提升运算符，而另一个是提升运算符，则非提升运算符更佳。
- 否则，两个函数成员都不更佳。




### 7.5.3.3 *表达式的更好转换*

给定一个从表达式 E 隐式转换为类型 T₁ 的隐式转换 C₁，以及一个从表达式 E 隐式转换为类型 T₂ 的隐式转换 C₂，如果满足以下至少一个条件，则 C₁ 是比 C₂ *更好的转换*：

- E 具有类型 S，并且从 S 到 T₁ 存在恒等转换，但从 S 到 T₂ 不存在。
- E 不是匿名函数，且 T₁ 是比 T₂ *更好的转换目标* (§7.5.3.5)。
- E 是匿名函数，T₁ 要么是委托类型 D₁ 要么是表达式树类型 `Expression<D₁>`，T₂ 要么是委托类型 D₂ 要么是表达式树类型 `Expression<D₂>`，且满足以下之一：
  - D₁ 是比 D₂ *更好的转换目标*。
  - D₁ 和 D₂ 具有相同的参数列表，且满足以下之一：
    - D₁ 具有返回类型 Y₁，且 D₂ 具有返回类型 Y₂，在该参数列表的上下文中，E 存在推断的返回类型 X (§7.5.2.12)，并且从 X 到 Y₁ 的转换比从 X 到 Y₂ 的转换更好。
    - D₁ 具有返回类型 Y，且 D₂ 为 void 返回。

### 7.5.3.4 *类型之间的更好转换*

给定一个从类型 S 转换为类型 T₁ 的转换 C₁，以及一个从类型 S 转换为类型 T₂ 的转换 C₂，如果满足以下至少一个条件，则 C₁ 是比 C₂ *更好的转换*：

- 从 S 到 T₁ 存在恒等转换，但从 S 到 T₂ 不存在。
- T₁ 是比 T₂ *更好的转换目标* (§7.5.3.5)。

### 7.5.3.5 *更好的转换目标*

给定两个不同的类型 T₁ 和 T₂，如果满足以下至少一个条件，则 T₁ 是比 T₂ *更好的转换目标*：

- 从 T₁ 到 T₂ 存在隐式转换，且从 T₂ 到 T₁ 不存在隐式转换。
- T₁ 是有符号整数类型且 T₂ 是无符号整数类型。具体来说：
  - T₁ 是 `sbyte` 且 T₂ 是 `byte`、`ushort`、`uint` 或 `ulong`。
  - T₁ 是 `short` 且 T₂ 是 `ushort`、`uint` 或 `ulong`。
  - T₁ 是 `int` 且 T₂ 是 `uint` 或 `ulong`。
  - T₁ 是 `long` 且 T₂ 是 `ulong`。

### 7.5.3.6 泛型类中的重载

虽然声明时的签名必须唯一，但类型参数的替换可能导致签名相同。在这种情况下，上述重载解析的平局打破规则将选择最具体的成员。

以下示例展示了根据此规则有效和无效的重载：

```csharp
interface I1<T> {...}
interface I2<T> {...}

class G1<U>
{
    int F1(U u);    // Overload resolution for G<int>.F1
    int F1(int i);  // will pick nongeneric
    void F2(I1<U> a);   // Valid overload
    void F2(I2<U> a);
}

class G2<U,V>
{
    void F3(U u, V v);    // Valid, but overload resolution for
    void F3(V v, U u);    // G2<int,int>.F3 will fail
    void F4(U u, I1<V> v);    // Valid, but overload resolution for
    void F4(I1<V> v, U u);    // G2<I1<int>,int>.F4 will fail
    void F5(U u1, I1<V> v2); // Valid overload
    void F5(V v1, U u2);
    void F6(ref U u);    // Valid overload
    void F6(out V v);
}
```

## 7.5.4 动态重载解析的编译时检查

对于大多数动态绑定操作，解析的候选集在编译时是未知的。然而，在某些情况下，候选集在编译时是已知的：

- 具有 dynamic 参数的静态方法调用。
- 接收方不是 dynamic 表达式的实例方法调用。
- 接收方不是 dynamic 表达式的索引器调用。
- 具有 dynamic 参数的构造函数调用。

在这些情况下，会对每个候选进行有限的编译时检查，以查看其中是否可能在运行时适用。该检查包括以下步骤：

- *部分类型推断：* 任何不直接或间接依赖于类型为 dynamic 的参数的类型参数都使用 §7.5.2 的规则进行推断。剩余的类型参数为 *未知*。
- *部分适用性检查：* 适用性根据 §7.5.3.1 进行检查，但忽略类型为 *未知* 的参数。

如果没有候选通过此测试，则会发生编译时错误。

## 7.5.5 函数成员调用

本节描述了在运行时调用特定函数成员时发生的过程。假定绑定时过程已经确定了要调用的特定成员，可能通过对一组候选函数成员应用重载解析来确定。

为了描述调用过程，函数成员分为两类：

- *静态函数成员。* 这些是静态方法、静态属性访问器和用户定义运算符。静态函数成员始终是非虚的。
- *实例函数成员。* 这些是实例方法、实例属性访问器和索引器访问器。实例函数成员要么是非虚的要么是虚的，并且始终在特定实例上调用。实例由实例表达式计算，并在函数成员内部作为 `this` 可访问 (§7.6.7)。

函数成员调用的运行时处理包括以下步骤，其中 `M` 是函数成员，如果 `M` 是实例成员，则 `E` 是实例表达式：

- 如果 `M` 是静态函数成员：
  - 参数列表按 §7.5.1 描述的方式进行求值。
  - 调用 `M`。

- 如果 `M` 是在 *值类型* 中声明的实例函数成员：
  - `E` 进行求值。如果此求值导致异常，则不再执行后续步骤。
  - 如果 `E` 未被分类为变量，则创建一个 `E` 类型的临时局部变量，并将 `E` 的值赋给该变量。`E` 然后被重新分类为对该临时局部变量的引用。临时变量在 `M` 内部作为 `this` 可访问，但在其他任何方式下不可访问。因此，只有当 E 是真正的变量时，调用方才有可能观察到 M 对 `this` 所做的更改。

> **ERIC LIPPERT** 这一点说明了可变性和按值复制语义的结合导致问题的又一种方式。例如，构造函数运行后，readonly 字段不再被分类为变量。因此，尝试调用一个会修改值类型 readonly 字段内容的方法会成功，但实际上修改的是一个副本！通过完全避免可变值类型来避免这些问题。

  - 参数列表按 §7.5.1 描述的方式进行求值。
  - 调用 `M`。 `E` 引用的变量变为 `this` 引用的变量。

- 如果 `M` 是在引用类型中声明的实例函数成员：
  - `E` 进行求值。如果此求值导致异常，则不再执行后续步骤。
  - 参数列表按 §7.5.1 描述的方式进行求值。
  - 如果 `E` 的类型是值类型，则执行装箱转换 (§4.3.1) 将 `E` 转换为类型 `object`，并且在后续步骤中 `E` 被视为 `object` 类型。在这种情况下，`M` 只能是 `System.Object` 的成员。
  - 检查 `E` 的值是否有效。如果 `E` 的值为 null，则抛出 `System.NullReferenceException` 并且不再执行后续步骤。
  - 确定要调用的函数成员实现：
    - 如果 `E` 的绑定时类型是接口，则要调用的函数成员是由 `E` 引用的实例的运行时类型提供的 `M` 的实现。该函数成员是通过应用接口映射规则 (§13.4.4) 来确定由 `E` 引用的实例的运行时类型提供的 `M` 的实现。
    - 否则，如果 `M` 是虚函数成员，则要调用的函数成员是由 `E` 引用的实例的运行时类型提供的 `M` 的实现。该函数成员是通过应用确定 `M` 的最派生实现 (§10.6.3) 的规则，相对于 `E` 引用的实例的运行时类型来确定的。
    - 否则，`M` 是非虚函数成员，且要调用的函数成员就是 `M` 本身。
- 调用上述步骤中确定的函数成员实现。 `E` 引用的对象变为 `this` 引用的对象。



## 7.5.5.1 对装箱实例的调用

在值类型中实现的函数成员可以在以下情形中通过该值类型的装箱实例调用：

- 当该函数成员是对从 object 类型继承的方法的重写，并且通过 object 类型的实例表达式调用时。
- 当该函数成员是接口函数成员的实现，并且通过接口类型的实例表达式调用时。
- 当该函数成员通过委托调用时。

在这些情形中，装箱实例被视为包含该值类型的一个变量，而在该函数成员调用内，this 引用的就是该变量。特别地，当在装箱实例上调用函数成员时，该函数成员有可能修改装箱实例中包含的值。

## 7.6 主表达式

主表达式包括最简单的表达式形式。

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
    checked-expression
    unchecked-expression
    default-value-expression
    anonymous-method-expression
```

主表达式分为数组创建表达式和非数组创建主表达式。以这种方式处理数组创建表达式，而不是将它与其他简单表达式形式并列，使语法能够禁止可能引起混淆的代码，例如

```
object o = new int[3][1];
```

否则它会被解释为

```
object o = (new int[3])[1];
```

## 7.6.1 字面量

由字面量（§2.4.4）构成的主表达式归类为值。

## 7.6.2 简单名称

简单名称由一个标识符组成，后面可选地跟一个类型实参列表：

```
simple-name:
    identifier type-argument-list_opt
```

简单名称要么是 I 形式，要么是 I<A1 ... Ak> 形式，其中 I 是单个标识符，<A1, ..., Ak> 是可选类型实参列表。未指定类型实参列表时，认为 k 为零。简单名称按如下方式求值并分类：

- 如果 k 为零，并且简单名称出现在某个块内，而且该块（或某个封闭块）的局部变量声明空间（§3.3）包含名为 I 的局部变量、参数或常量，那么该简单名称引用该局部变量、参数或常量，并归类为变量或值。
- 如果 k 为零，并且简单名称出现在泛型方法声明的体内，而且该声明包含名为 I 的类型参数，那么该简单名称引用该类型参数。

> VLADIMIR RESHETNIKOV 此规则也适用于简单名称出现在构造函数初始化器中并且与所在构造函数的参数名匹配的情形。

> VLADIMIR RESHETNIKOV 此条件稍后总会导致编译时错误。

- 否则，对于每个实例类型 T（§10.3.1），从直接封闭类型声明的实例类型开始，并继续到每个封闭类或结构声明的实例类型（如果有）：
  - 如果 K 为零，并且 T 的声明包含名为 I 的类型参数，那么该简单名称引用该类型参数。
- 否则，如果以 K 个类型实参在 T 中查找 I 的成员（§7.4）产生匹配：
  - 如果 T 是直接封闭类或结构类型的实例类型，并且该查找标识一个或多个方法，则结果是一个方法组，其关联的实例表达式为 this。如果指定了类型实参列表，则在调用泛型方法（§7.6.5.1）时使用它。
  - 否则，如果 T 是直接封闭类或结构类型的实例类型，如果该查找标识一个实例成员，并且如果该引用出现在实例构造函数、实例方法或实例访问器的块内，则结果与形式为 this.I 的成员访问（§7.6.4）相同。这仅在 K 为零时才会发生。
  - 否则，结果与形式为 T.I 或 T.I<A1, ..., An> 的成员访问（§7.6.4）相同。在这种情况下，简单名称引用实例成员会导致绑定期错误。
- 否则，对于每个命名空间 N，从简单名称所在的命名空间开始，继续到每个封闭命名空间（如果有），并以全局命名空间结束，按顺序计算以下步骤，直到定位到某个实体：
  - 如果 K 为零，并且 I 是 N 中某个命名空间的名称，则：
    - 如果简单名称出现的位置由针对 N 的命名空间声明封闭，并且该命名空间声明包含将名称 I 与某个命名空间或类型关联的 extern 别名指令或 using 别名指令，则该简单名称有歧义，并发生编译时错误。
  - 否则，该简单名称引用 N 中名为 I 的命名空间。

> VLADIMIR RESHETNIKOV 此条件稍后总会导致编译时错误。

- 否则，如果 N 包含一个可访问类型，其名称为 I 且具有 K 个类型参数，则：
  - 如果 K 为零，并且简单名称出现的位置由针对 N 的命名空间声明封闭，并且该命名空间声明包含将名称 I 与某个命名空间或类型关联的 extern 别名指令或 using 别名指令，则该简单名称有歧义，并发生编译时错误。
  - 否则，该命名空间或类型名引用用给定类型实参构造的类型。
- 否则，如果简单名称出现的位置由针对 N 的命名空间声明封闭：
  - 如果 K 为零，并且该命名空间声明包含将名称 I 与导入的命名空间或类型关联的 extern 别名指令或 using 别名指令，则该简单名称引用该命名空间或类型。
  - 否则，如果该命名空间声明的 using 命名空间指令所导入的命名空间中恰好包含一个名称为 I 且具有 K 个类型参数的类型，则该简单名称引用用给定类型实参构造的该类型。
  - 否则，如果该命名空间声明的 using 命名空间指令所导入的命名空间中包含多于一个名称为 I 且具有 K 个类型参数的类型，则该简单名称有歧义，并发生错误。

请注意，整个这一步与处理命名空间或类型名（§3.8）时的对应步骤完全平行。

- 否则，该简单名称未定义，并发生编译时错误。

## 7.6.2.1 块中的不变含义

对于给定标识符在表达式或声明符中作为简单名称的每次出现，在直接封闭该出现的局部变量声明空间（§3.3）内，同一标识符在表达式或声明符中作为简单名称的其他每次出现都必须引用同一实体。此规则确保，在给定块、switch 块、for 语句、foreach 语句、using 语句或匿名函数内，名称的含义始终相同。

> **ERIC LIPPERT** 此规则较为微妙的一个有利后果是，进行涉及移动局部变量声明的重构会变得更安全。任何会导致简单名称改变语义的此类重构都会被编译器捕获。

示例

```
class Test
{
    double x;

    void f(bool b) {
        x = 1.0;
        if (b) {
            int x;
            x = 1;
        }
    }
}
```

会导致编译时错误，因为 x 在外层块内引用了不同的实体（外层块的范围包括 if 语句中的嵌套块）。相比之下，示例

```
class Test
{
    double x;

    void f(bool b) {
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

是允许的，因为名称 x 从未在外层块中使用。

请注意，不变含义规则仅适用于简单名称。同一标识符作为简单名称具有一种含义，而作为成员访问（§7.6.4）的右操作数具有另一种含义，是完全合法的。例如：

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



上例说明了在实例构造函数中使用字段名作为参数名的一种常见模式。在示例中，简单名称 x 和 y 指的是参数，但这并不会阻止成员访问表达式 this.x 和 this.y 访问字段。

### 7.6.3 圆括号表达式

一个 *圆括号表达式* 由一个被圆括号括起来的 *表达式* 组成。

```text
    *parenthesized-expression*:
        ( *expression* )
```

一个 *圆括号表达式* 的求值是通过求值圆括号内的 *表达式* 来进行的。如果圆括号内的 *表达式* 表示一个命名空间或类型，则会发生编译时错误。否则，*圆括号表达式* 的结果是所包含 *表达式* 求值的结果。

### 7.6.4 成员访问

一个 *成员访问* 由一个 *主表达式*、一个 *预定义类型* 或一个 *限定别名成员* 组成，其后跟一个 “.” 标记，再跟一个标识符，可选地跟一个 *类型参数列表*。

```text
    *member-access*:
        *primary-expression*    . *identifier* *type-argument-list*_opt
        *predefined-type*    . *identifier* *type-argument-list*_opt
        *qualified-alias-member* . *identifier* *type-argument-list*_opt
```

```text
    *predefined-type*: one of
        bool    byte    char    decimal double  float   int     long
        object  sbyte   short   string  uint    ulong   ushort
```

*限定别名成员* 产生式在 §9.7 中定义。

一个 *成员访问* 要么是形式为 E.I，要么是形式为 E.I<A₁, ..., Aₖ>，其中 E 是一个 *主表达式*，I 是一个单一标识符，<A₁, ..., Aₖ> 是一个可选的 *类型参数列表*。当未指定 *类型参数列表* 时，将 K 视为零。

*主表达式* 类型为 dynamic 的 *成员访问* 是动态绑定的 (§7.2.2)。在这种情况下，编译器将成员访问分类为类型为 dynamic 的属性访问。下面用于确定 *成员访问* 含义的规则随后在运行时应用，使用运行时类型而不是 *主表达式* 的编译时类型。如果此运行时分类导致一个方法组，则该成员访问必须是 *调用表达式* 的 *主表达式*。

成员访问的求值和分类如下：

- 如果 K 为零，E 是一个命名空间，并且 E 包含一个名为 I 的嵌套命名空间，则结果为该命名空间。
- 否则，如果 E 是一个命名空间并且 E 包含一个可访问的类型，其名称为 I 且有 K 个类型参数，则结果为使用给定类型参数构造的该类型。
- 如果 E 是一个 *预定义类型* 或被分类为类型的 *主表达式*，如果 E 不是类型参数，并且在 E 中对 I 进行成员查找 (§7.4) 且有 K 个类型参数产生匹配，则 E.I 的求值和分类如下：
  - 如果 I 标识一个类型，则结果为使用给定类型参数构造的该类型。
  - 如果 I 标识一个或多个方法，则结果为没有关联实例表达式的方法组。如果指定了类型参数列表，则在调用泛型方法时使用它 (§7.6.5.1)。
  - 如果 I 标识一个静态属性，则结果为没有关联实例表达式的属性访问。
  - 如果 I 标识一个静态字段：
    - 如果该字段是只读的并且引用发生在声明该字段的类或结构体的静态构造函数之外，则结果是一个值——即 E 中静态字段 I 的值。
    - 否则，结果是一个变量——即 E 中的静态字段 I。
  - 如果 I 标识一个静态事件：
    - 如果引用发生在声明该事件的类或结构体内部，并且该事件是在没有事件访问器声明 (§10.8) 的情况下声明的，则 E.I 的处理方式与 I 为静态字段时完全相同。
    - 否则，结果为没有关联实例表达式的事件访问。
  - 如果 I 标识一个常量，则结果是一个值——即该常量的值。
  - 如果 I 标识一个枚举成员，则结果是一个值——即该枚举成员的值。
  - 否则，E.I 是一个无效的成员引用，并且会发生编译时错误。
- 如果 E 是一个属性访问、索引器访问、变量或值，其类型为 T，并且在 T 中对 I 进行成员查找 (§7.4) 且有 K 个类型参数产生匹配，则 E.I 的求值和分类如下：
  - 首先，如果 E 是属性或索引器访问，则获取属性或索引器访问的值 (§7.1.1) 并将 E 重新分类为值。
  - 如果 I 标识一个或多个方法，则结果为具有关联实例表达式 E 的方法组。如果指定了类型参数列表，则在调用泛型方法时使用它 (§7.6.5.1)。
  - 如果 I 标识一个实例属性，则结果为具有关联实例表达式 E 的属性访问。
  - 如果 T 是一个类类型并且 I 标识该类类型的实例字段：
    - 如果 E 的值为空，则抛出 System.NullReferenceException。
    - 否则，如果该字段是只读的并且引用发生在声明该字段的类的实例构造函数之外，则结果是一个值——即由 E 引用的对象中字段 I 的值。
    - 否则，结果是一个变量——即由 E 引用的对象中的字段 I。
  - 如果 T 是一个结构体类型并且 I 标识该结构体类型的实例字段：
    - 如果 E 是一个值，或者该字段是只读的并且引用发生在声明该字段的结构体的实例构造函数之外，则结果是一个值——即由 E 给出的结构体实例中字段 I 的值。
    - 否则，结果是一个变量——即由 E 给出的结构体实例中的字段 I。
  - 如果 I 标识一个实例事件：
    - 如果引用发生在声明该事件的类或结构体内部，并且该事件是在没有事件访问器声明 (§10.8) 的情况下声明的，并且引用未作为 += 或 -= 运算符的左侧出现，则 E.I 的处理方式与 I 为实例字段时完全相同。
    - 否则，结果为具有关联实例表达式 E 的事件访问。
- 否则，会尝试将 E.I 作为扩展方法调用 (§7.6.5.2) 处理。如果失败，E.I 是一个无效的成员引用，并且会发生绑定时错误。

> **PETER SESTOFT** 两个要点“如果字段是只读的……则结果是一个值”在字段具有结构体类型并且该结构体具有可变字段时会有略微令人惊讶的效果（这不是推荐的组合——请参阅对此点的其他注释）。考虑以下示例：
>
> ```
> struct S {
>     public int x;
>     public void SetX() { x = 2; }
> }
> class C {
>     public static void M() { s.SetX(); }
> }
> ```
>
> 预期情况下，在调用 `s.SetX()` 之后，结构体的字段 `s.x` 将具有值 2。现在如果我们在字段 `s` 的声明中添加 readonly 修饰符，那么调用 `s.SetX()` 突然就没有任何效果！也就是说，根据前面给出的规则，方法调用中的 `s` 现在是一个值，而不是一个变量；因此 `SetX()` 是在字段 `s` 的副本上执行，而不是在字段 `s` 本身之上。有点奇怪的是，如果 `s` 反而是一个在 using 语句 (§8.13) 中声明的结构体类型的局部变量，这也具有使 `s` 不可变的效果，那么 `s.SetX()` 仍会按预期更新 `s.x`。

### 7.6.4.1 *相同简单名称和类型名称*

在形式为 E.I 的成员访问中，如果 I 是一个单一标识符，并且 E 的含义作为 *简单名称* (§7.6.2) 是一个常量、字段、属性、局部变量或参数，其类型与 E 作为 *类型名称* (§3.8) 的含义相同，则 E 的两种可能含义均被允许。E.I 的两种可能含义永远不会产生歧义，因为在两种情况下 I 必须必然是类型 E 的成员。换句话说，该规则只是允许在原本会发生编译时错误的情况下访问 E 的静态成员和嵌套类型。例如：

```
struct Color
{
    public static readonly Color White = new Color(...);
    public static readonly Color Black = new Color(...);

    public Color Complement() {...}
}

class A
{
    public Color Color;        // Field Color of type Color

    void F() {
        Color = Color.Black;   // References Color.Black static member
    }
}
```



```
Color = Color.Complement(); // Invokes Complement() on Color field
}
static void G() {
    Color c = Color.White;    // References Color.White static member
}
```

在 A 类中，那些引用 Color 类型的 Color 标识符出现处带有下划线，而那些引用 Color 字段的出现处不带下划线。

## 7.6.4.2 语法歧义

简单名称（§7.6.2）和成员访问（§7.6.4）的生成式可能导致表达式语法中出现歧义。例如，语句

```
F(G<A,B>(7));
```

可以被解释为对 F 的调用，带有两个实参：G < A 和 B > (7)。或者，它也可以被解释为对 F 的调用，带有一个实参，即对泛型方法 G 的调用，带有两个类型实参和一个常规实参。

如果某个标记序列可以（在上下文中）被解析为以类型实参列表（§4.4.1）结尾的简单名称（§7.6.2）、成员访问（§7.6.4）或指针成员访问（§18.5.2），则检查紧跟在结束 > 标记之后的标记。如果它是以下之一

```
( ) ] } ; : , . ? == != | ^
```

则类型实参列表被保留为简单名称、成员访问或指针成员访问的一部分，并且该标记序列的任何其他可能解析都被丢弃。否则，类型实参列表不被视为简单名称、成员访问或指针成员访问的一部分，即使该标记序列没有其他可能的解析。注意，在解析命名空间或类型名（§3.8）中的类型实参列表时，这些规则不适用。语句

```
F(G<A,B>(7));
```

根据此规则，将被解释为对 F 的调用，带有一个实参，即对泛型方法 G 的调用，带有两个类型实参和一个常规实参。以下语句

```
F(G < A, B > 7);
F(G < A, B >> 7);
```

将各自被解释为对 F 的调用，带有两个实参。

语句

```
x = F < A > +y;
```

将被解释为包含小于运算符、大于运算符和一元加运算符，就好像该语句被写成 x = (F < A) > (+y)，而不是作为后跟二元加运算符的、带有*类型实参列表*的*简单名称*。在语句

```
x = y is C<T> + z;
```

中，标记 C<T> 被解释为带有*类型实参列表*的*命名空间或类型名*。

## 7.6.5 调用表达式

*调用表达式*用于调用方法。

```
invocation-expression:
    primary-expression   (   argument-list
                                      opt   )
```

如果以下条件至少满足一项，则*调用表达式*是动态绑定的（§7.2.2）：

- *主表达式*具有编译时类型 `dynamic`。
- 可选*实参列表*的至少一个实参具有编译时类型 `dynamic`，并且*主表达式*不具有委托类型。

> **弗拉基米尔·列舍特尼科夫** 此规则有一个例外：类型为 `dynamic` 的 `ref`/`out` 实参不会导致动态绑定。
> 
> 如果*调用表达式*是动态绑定的，并且其*主表达式*表示由*基访问*产生的方法组，则发生编译时错误（CS1971）。

在这种情况下，编译器将*调用表达式*归类为 dynamic 类型的值。然后，用于确定*调用表达式*含义的以下规则在运行时应用，使用运行时类型而不是那些具有编译时类型 dynamic 的*主表达式*和实参的编译时类型。如果*主表达式*不具有编译时类型 dynamic，则方法调用会经历 §7.5.4 中所述的有限编译时检查。

*调用表达式*的*主表达式*必须是方法组或*委托类型*的值。如果*主表达式*是方法组，则*调用表达式*是方法调用（§7.6.5.1）。如果*主表达式*是*委托类型*的值，则*调用表达式*是委托调用（§7.6.5.3）。如果*主表达式*既不是方法组也不是*委托类型*的值，则发生绑定期错误。

可选实参列表（§7.5.1）为方法的参数提供值或变量引用。

对调用表达式求值的结果分类如下：

- 如果调用表达式调用返回 void 的方法或委托，则结果为空（nothing）。被归类为 nothing 的表达式只允许在语句表达式（§8.6）的上下文中或作为 lambda 表达式（§7.15）的主体。否则，发生绑定期错误。
- 否则，结果是该方法或委托返回的类型的值。

### 7.6.5.1 方法调用

对于方法调用，调用表达式的主表达式必须是方法组。方法组标识要调用的一个方法，或从中选择要调用的特定方法的重载方法集。在后一种情况下，要调用的特定方法的确定基于实参列表中实参的类型提供的上下文。

形式为 M(A) 的方法调用的绑定期处理（其中 M 是方法组（可能包括类型实参列表），A 是可选实参列表）由以下步骤组成：

- 构造该方法调用的候选方法集。对于与方法组 M 关联的每个方法 F：
  - 如果 F 是非泛型方法，则 F 在以下情况下是候选方法：
    - M 没有类型实参列表，并且
    - F 相对于 A 是适用的（§7.5.3.1）。
  - 如果 F 是泛型方法且 M 没有类型实参列表，则 F 在以下情况下是候选方法：
    - 类型推断（§7.5.2）成功，推断出该调用的类型实参列表，并且
    - 一旦将推断出的类型实参替换对应的方法类型参数，F 的参数列表中的所有构造类型都满足其约束（§4.4.4），并且 F 的参数列表相对于 A 是适用的（§7.5.3.1）。

> 弗拉基米尔·列舍特尼科夫 注意，此步骤中仅检查出现在参数列表中的构造类型的约束。泛型方法本身的约束稍后在最终验证期间检查。

- 如果 F 是泛型方法且 M 包含类型实参列表，则 F 在以下情况下是候选方法：
  - F 的方法类型参数数量与类型实参列表中提供的数量相同，并且
  - 一旦将类型实参替换对应的方法类型参数，F 的参数列表中的所有构造类型都满足其约束（§4.4.4），并且 F 的参数列表相对于 A 是适用的（§7.5.3.1）。

- 候选方法集被缩减为只包含来自最多派生类型的方法：对于该集合中的每个方法 C.F（其中 C 是声明方法 F 的类型），从该集合中移除在 C 的基类型中声明的所有方法。此外，如果 C 是除 object 之外的类类型，则从该集合中移除在接口类型中声明的所有方法。（后一条规则仅在方法组是对类型参数进行成员查找的结果时生效，该类型参数具有除 object 之外的有效基类和有效接口集非空。）

> **弗拉基米尔·列舍特尼科夫** 此规则意味着会选择来自最多派生类型的适用方法，即使基类型中存在具有更好参数类型的方法，并且即使所选的来自最多派生类型的方法将无法通过最终验证。还要记住，在此步骤之前，在成员查找（§7.4）期间，所有重写方法都已被移除。

```csharp
class Base
{
    public virtual void Foo(int x) { }
}

class Derived : Base
{
    public override void Foo(int x) { }

    static void Foo(object x) { }
}

static void Main()
{
    var d = new Derived();
    d.Foo(1);
    // Error CS0176: Member 'Derived.Foo(object)'
    // cannot be accessed with an instance reference;
    // qualify it with a type name instead
}
```

- 如果得到的候选方法集为空，则放弃沿着以下步骤的进一步处理，并改为尝试将该调用作为扩展方法调用（§7.6.5.2）处理。如果此操作失败，则不存在适用的方法，并发生绑定期错误。




- 候选方法集合中的最佳方法使用 §7.5.3 的重载解析规则来确定。如果无法确定单一的最佳方法，则方法调用不明确，并发生绑定时错误。在执行重载解析时，泛型方法的参数是在用类型参数（提供或推断）替换相应的泛型方法类型参数之后再考虑的。

- 对选定的最佳方法进行最终验证：
  - 在方法组上下文中验证方法：如果最佳方法为静态方法，则方法组必须源自简单名称或通过类型进行的成员访问。如果最佳方法为实例方法，则方法组必须源自简单名称、通过变量或值进行的成员访问，或 base 访问。如果两者要求均不成立，则发生绑定时错误。

> **VLADIMIR RESHETNIKOV** 如果最佳方法为实例方法，且方法组源自简单名称，则该简单名称不得出现在静态上下文中（即在静态成员、嵌套类型、实例字段或类似字段的事件初始化器或构造函数初始化器中）；否则，发生绑定时错误。

  - 如果最佳方法为泛型方法，则会将类型参数（提供或推断）与泛型方法上声明的约束（§4.4.4）进行检查。如果任何类型参数不满足类型参数上的相应约束，则发生绑定时错误。

> **VLADIMIR RESHETNIKOV** 如果此检查成功，则它自动保证返回类型和方法的正文中所有构造类型的所有约束也都得到满足。

> **ERIC LIPPERT** 上述规则引发了大量争论：为什么编译器要进行类型推断、重载解析和排除不适用候选的所有工作，然后才说，“我选择了一个最终不可用的方法”？为什么不直接说不满足其约束的方法甚至不是候选？原因很微妙但很重要：C# 的一个基本设计原则是语言不会揣测用户。如果由参数和参数类型暗示的最佳选择无效，那么要么用户本意是使用最佳选择但犯了某种错误，要么用户本意是让编译器选择其他内容。最安全的做法是假设前者，而不是可能猜错。

一旦方法通过上述步骤在绑定时被选中并验证，实际的运行时调用将根据 §7.5.4 中描述的函数成员调用规则进行处理。

> BILL WAGNER  下一段至关重要：扩展方法不能替换类型作者定义的行为。

上述描述的解析规则的直观效果如下：要定位方法调用所调用的特定方法，从方法调用指示的类型开始，并沿继承链向上查找，直到找到至少一个适用、可访问、非重写的方法声明。然后对该类型中声明的适用、可访问、非重写方法集合执行类型推断和重载解析，并调用由此选定的方法。如果未找到方法，则尝试将其作为扩展方法调用来处理。

> ERIC LIPPERT  在此设计下，即使在基类中可能找到“更好”的方法，派生类中的任何适用方法都具有优先权。此设计的理由有两方面。

首先，派生类的实现者很可能比基类的实现者更了解此操作在其类上的期望语义；派生类的存在是因为它为基类添加了一些功能或特化。

其次，此设计避免了“脆弱基类”家族中的一个问题。假设你有依赖于对派生类中方法调用的代码。如果重载解析今天选择该方法，那么明天对基类的更改不应导致重载解析在重新编译时静默且突然开始选择基类方法。

当然，该方案也引入了相反的情况：如果您依赖重载解析来选择基类的方法，那么有人向更派生的类添加方法也可能在重新编译时静默地改变重载解析的选择。然而，这种“脆弱派生类”问题在实际生产代码中很少成为问题；大多数时候，您希望出于上述原因选择更派生的方法。

> JON SKEET  虽然我大部分同意 Eric 的推理，但此设计允许出现一种不幸的情况。如果派生类引入了基类方法的新的重载并重写了基类方法，那么显然该派生类知道基类方法——然而在选择方法时，该重写仍不会被考虑，直到算法到达基类。例如，考虑派生类中的以下方法，基类声明了明显的虚方法：

public void Foo(object x) { ... }
public override void Foo(int y) { ... }

对派生类型表达式调用 Foo(10) 将选择第一个方法——这与我向其展示此设计的每一位非微软开发者的预期相反。

```
public void Foo(object x) { ... }
public override void Foo(int y) { ... }
```

### 7.6.5.2 扩展方法调用

在 §7.5.5.1 的方法调用中，其形式之一为

```
expr . identifier ( )
expr . identifier ( args )
expr . identifier < typeargs > ( )
expr . identifier < typeargs > ( args )
```

如果对调用的正常处理未找到适用方法，则会尝试将该构造作为扩展方法调用来处理。如果 expr 或任何 args 的编译时类型为 dynamic，则扩展方法不适用。

> VLADIMIR RESHETNIKOV  最后一条规则不适用于类型为 dynamic 的 ref / out 参数。

目标是找到最佳类型名 C，以便可以进行相应的静态方法调用：

```
C . identifier ( expr )
C . identifier ( expr , args )
C . identifier < typeargs > ( expr )
C . identifier < typeargs > ( expr , args )
```

## 7. 表达式

扩展方法 C₁.Mⱼ 符合条件，如果：

- C₁ 是一个非泛型、非嵌套的类。
- Mⱼ 的名称为 *identifier*。
- Mⱼ 在作为上述所示的静态方法应用于参数时是可访问且适用的。
- 从 *expr* 到 Mⱼ 的第一个参数的类型存在隐式标识、引用或装箱转换。

> **ERIC LIPPERT**  此规则确保使扩展 `double` 的方法不会同时扩展 `int`。它还确保不会在匿名函数或方法组上定义扩展方法。

对 C 的搜索按如下方式进行：

- 从最近的封闭命名空间声明开始，继续每个封闭命名空间声明，并以包含的编译单元结束，依次尝试找到扩展方法的候选集：
  - 如果给定的命名空间或编译单元直接包含具有符合条件的扩展方法 Mⱼ 的非泛型类型声明 C₁，则这些扩展方法的集合为候选集。
  - 如果在给定的命名空间或编译单元中使用 using 命名空间指令导入的命名空间直接包含具有符合条件的扩展方法 Mⱼ 的非泛型类型声明 C₁，则这些扩展方法的集合为候选集。
- 如果在任何封闭命名空间声明或编译单元中均未找到候选，则发生编译时错误。
- 否则，对候选集应用重载解析，如 (§7.5.3) 中所述。如果未找到单一最佳方法，则发生编译时错误。
- C 是最佳方法作为扩展方法声明所在的类。

使用 C 作为目标，方法调用随后作为静态方法调用 (§7.5.4) 进行处理。

> **BILL WAGNER**  此处理有些复杂，它强化了不应在不同命名空间中创建重复扩展方法的建议。




> **PETER SESTOFT** 把扩展方法想成只是当没有合适的普通实例方法可用时才会被调用的一种有趣的非虚实例方法是很诱人的。不幸的是，在结构体类型 S 上的扩展方法 SetX(this S s) 与 S 上的实例方法并不完全相同，因为调用 s.SetX() 会被转换为调用 SetX(s)，该调用按值传递结构体 s，从而复制它。任何副作用都会发生在副本上，而不是原始结构体 s 上——这又是永远不要在结构体类型中拥有可变字段的另一个原因。

> **JON SKEET** 扩展方法的一个问题就在于意外导入超出预期或想要的内容是多么容易。我希望这个过程更明确，例如使用一种新的 using 指令类型：
> 
> `using static System.Linq.Enumerable;`
> 
> 这样类库就可以公开扩展方法，而不会给不想使用它们的用户增加 IntelliSense 混淆。此外，它还会为代码维护者提供一个提示，警告他们应预期在此编译单元中看到某些扩展方法被使用。

前述规则意味着实例方法优先于扩展方法，内部命名空间声明中可用的扩展方法优先于外部命名空间声明中可用的扩展方法，并且直接在命名空间中声明的扩展方法优先于通过 using namespace 指令导入到同一命名空间中的扩展方法。例如：

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
```

```
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

在示例中，B 的方法优先于第一个扩展方法，C 的方法优先于两个扩展方法。

```
public static class C
{
    public static void F(this int i) {
        Console.WriteLine("C.F({0})", i);
    }
    public static void G(this int i) {
        Console.WriteLine("C.G({0})", i);
    }
    public static void H(this int i) {
        Console.WriteLine("C.H({0})", i);
    }
}
```

```
namespace N1
{
    public static class D
    {
        public static void F(this int i) {
            Console.WriteLine("D.F({0})", i);
        }
        public static void G(this int i) {
            Console.WriteLine("D.G({0})", i);
        }
    }
}
```

```
namespace N2
{
    using N1;
    public static class E
    {
        public static void F(this int i) {
            Console.WriteLine("E.F({0})", i);
        }
    }
}
```

```
class Test
{
    static void Main(string[] args)
    {
        1.F();
        2.G();
        3.H();
    }
}
```

此示例的输出是

E.F(1)
D.G(2)
C.H(3)

D.G 优先于 C.G，E.F 优先于 D.F 和 C.F。

> **JOSEPH ALBAHARI** 实例方法比扩展方法优先级更高的一个原因是确保将扩展方法引入程序或框架时不会破坏现有代码。

> **ERIC LIPPERT** C# 查找扩展方法的方式导致了前面提到的“脆弱基类”问题的变体。如果你依赖调用处理来选择扩展方法，但有人在该类上引入了同名实例方法，那么在重新编译后扩展方法将不再被调用。
> 
> 这种行为其实不是问题——通常这正是你想要的。类上的方法比静态扩展方法拥有更多关于类内部结构的信息，因此应给予其优先权。
> 
> Microsoft C# 编译器不会发出警告，提示存在一个可作为所选实例方法替代的扩展方法。如果编译器发出此类警告，除了在周围放置 #pragma 指令来关闭警告外，就没有简单的方法来“修复”该警告。

> > JON SKEET 我认为在这种情况下发出警告实际上是最合适的处理方式，以便提醒开发人员，存在一个同名但含义不同的方法现在会在客户端代码没有任何更改（除重新编译外）的情况下被调用。在许多情况下——只要依赖扩展方法整个代码库都可以重新编译，因此不需要二进制兼容——该方法可以完全删除或重命名。在其他情况下，它可以转换为非扩展方法，从而允许与旧代码的二进制兼容。完全忽略成员查找结果的这种变化感觉是不对的。

### 7.6.5.3 委托调用

对于委托调用，*调用表达式* 的 *主表达式* 必须是一个 *委托类型* 的值。此外，将 *委托类型* 视为具有与 *委托类型* 相同参数列表的函数成员，*委托类型* 必须相对于 *调用表达式* 的 *参数列表* 可适用 (§7.5.3.1)。

形式为 D(A) 的委托调用的运行时处理，其中 D 是 *委托类型* 的 *主表达式*，A 是可选的 *参数列表*，包括以下步骤：

- 对 D 进行求值。如果此求值导致异常，则不再执行后续步骤。
- 检查 D 的值是否有效。如果 D 的值为 null，则抛出 System.NullReferenceException 并且不再执行后续步骤。
- 否则，D 是对委托实例的引用。对委托的调用列表中的每个可调用实体执行函数成员调用 (§7.5.4)。对于由实例和实例方法组成的可调用实体，调用的实例是可调用实体中包含的实例。

### 7.6.6 元素访问

*元素访问* 由 *主非数组创建表达式* 组成，后跟 “[” 标记，后跟 *参数列表*，后跟 “]” 标记。*参数列表* 由一个或多个 *参数* 组成，以逗号分隔。

```
element-access:
    primary-no-array-creation-expression   [   argument-list   ]
```

*元素访问* 的 *参数列表* 不允许包含 ref 或 out 参数。

如果满足以下任一条件，则 *元素访问* 是动态绑定的 (§7.2.2)：
- *主非数组创建表达式* 的编译时类型为 dynamic。
- *参数列表* 的至少一个表达式的编译时类型为 dynamic 且 *主非数组创建表达式* 没有数组类型。

在这种情况下，编译器将 *元素访问* 分类为类型为 dynamic 的值。然后在运行时应用下面确定 *元素访问* 含义的规则，使用运行时类型代替那些编译时类型为 dynamic 的 *主非数组创建表达式* 和 *参数列表* 表达式的编译时类型。如果 *主非数组创建表达式* 的编译时类型不是 dynamic，则 *元素访问* 会进行 §7.5.4 中描述的有限编译时检查。

如果 *元素访问* 的 *主非数组创建表达式* 是 *数组类型* 的值，则 *元素访问* 是数组访问 (§7.6.6.1)。否则，*主非数组创建表达式* 必须是一个类、结构体或接口类型的变量或值，该类型具有一个或多个索引器成员，在这种情况下 *元素访问* 是索引器访问 (§7.6.6.2)。

## 7.6.6.1 数组访问

对于数组访问，*元素访问* 的 *主非数组创建表达式* 必须是一个 *数组类型* 的值。此外，数组访问的 *参数列表* 不允许包含命名参数。*参数列表* 中表达式的数量必须与 *数组类型* 的秩相同，并且每个表达式必须为 int、uint、long 或 ulong 类型，或必须可隐式转换为其中一种或多种类型。

求值数组访问的结果是数组元素类型的变量——即由 *参数列表* 中表达式的值选择的数组元素。

> JON SKEET 这里结果是一个变量这一事实很重要：这意味着你可以在方法调用中使用数组元素作为 ref 或 out 参数。在数组协变的情况下，存储位置的实际类型会在方法被调用之前得到验证。

形式为 P[A] 的数组访问的运行时处理，其中 P 是 *数组类型* 的 *主非数组创建表达式*，A 是 *参数列表*，包括以下步骤：

- 对 P 进行求值。如果此求值导致异常，则不再执行后续步骤。
- 按从左到右的顺序求值 *参数列表* 的索引表达式。求值每个索引表达式后，执行到以下类型之一的隐式转换 (§6.1)：int、uint、long、ulong。第一个满足条件的类型为

存在隐式转换时，选择该隐式转换。例如，如果索引表达式的类型为 `short`，则执行到 `int` 的隐式转换，因为从 `short` 到 `int` 以及从 `short` 到 `long` 的隐式转换都是可能的。如果对索引表达式的求值或随后的隐式转换引发异常，则不再计算其他索引表达式，也不再执行后续步骤。

-   检查 `P` 的值是否有效。如果 `P` 的值为 null，则引发 `System.NullReferenceException`，并且不再执行后续步骤。
-   将参数列表中每个表达式的值与 `P` 所引用的数组实例的每个维度的实际边界进行对照检查。如果一个或多个值超出范围，则引发 `System.IndexOutOfRangeException`，并且不再执行后续步骤。
-   计算由索引表达式给出的数组元素的位置，该位置成为数组访问的结果。

### 7.6.6.2 索引器访问

对于索引器访问，元素访问的主非数组创建表达式必须是类、结构或接口类型的变量或值，并且该类型必须实现一个或多个适用于该元素访问的参数列表的索引器。

形如 `P[A]` 的索引器访问（其中 `P` 是类、结构或接口类型 `T` 的主非数组创建表达式，`A` 是参数列表）的绑定时间处理包括以下步骤：

-   构造由 `T` 提供的索引器集合。该集合由在 `T` 或 `T` 的基类型中声明的、不是重写声明且在当前上下文中可访问（§3.5）的所有索引器组成。
-   将该集合缩减为适用的且未被其他索引器隐藏的索引器。以下规则应用于集合中的每个索引器 `S.I`，其中 `S` 是声明索引器 `I` 的类型：
    -   如果 `I` 相对于 `A` 不适用（§7.5.3.1），则从集合中移除 `I`。
    -   如果 `I` 相对于 `A` 适用（§7.5.3.1），则从集合中移除在 `S` 的基类型中声明的所有索引器。
    -   如果 `I` 相对于 `A` 适用（§7.5.3.1）且 `S` 是除 `object` 之外的类类型，则从集合中移除在接口中声明的所有索引器。
-   如果得到的候选索引器集合为空，则不存在适用的索引器，并发生绑定时间错误。
-   使用 §7.5.3 的重载决策规则标识候选索引器集合中的最佳索引器。如果无法标识单个最佳索引器，则索引器访问存在二义性，并发生绑定时间错误。
-   按从左到右的顺序计算*参数列表*的索引表达式。处理索引器访问的结果是一个分类为索引器访问的表达式。该索引器访问表达式引用上述步骤中确定的索引器，并具有关联的 `P` 实例表达式和关联的 `A` 参数列表。

根据使用索引器访问的上下文，索引器访问会调用索引器的*获取访问器*或*设置访问器*。如果索引器访问是赋值的目标，则调用*设置访问器*来赋予新值（§7.17.1）。在所有其他情况下，调用*获取访问器*来获取当前值（§7.1.1）。

> **VLADIMIR RESHETNIKOV** 如果相应的访问器缺失或不可访问，则发生编译时错误。

### 7.6.7 this 访问

*this 访问*由保留字 *this* 组成。

```csharp
this-access:
    this
```

*this 访问*只允许在*实例构造函数*、*实例方法*或*实例访问器*的*块*中。它具有以下含义之一：

-   当在类的实例构造函数中的*主表达式*内使用 *this* 时，它被分类为值。该值的类型是该用法所在类的实例类型（§10.3.1），并且该值是对正在构造的对象的引用。
-   当在类的实例方法或实例访问器中的*主表达式*内使用 *this* 时，它被分类为值。该值的类型是该用法所在类的实例类型（§10.3.1），并且该值是对调用该方法或访问器时所针对的对象的引用。
-   当在结构的实例构造函数中的*主表达式*内使用 *this* 时，它被分类为变量。该变量的类型是该用法所在结构的实例类型（§10.3.1），并且该变量表示正在构造的结构。结构的实例构造函数的 *this* 变量的行为与结构类型的 *out* 参数完全相同——特别地，这意味着该变量必须在实例构造函数的每条执行路径上明确赋值。

## 7. 表达式

-   当在结构的实例方法或实例访问器中的*主表达式*内使用 *this* 时，它被分类为变量。该变量的类型是该用法所在结构的实例类型（§10.3.1）。
    -   如果该方法或访问器不是迭代器（§10.14），则该变量表示调用该方法或访问器时所针对的结构，并且其行为与结构类型的 `ref` 参数完全相同。
    -   如果该方法或访问器是迭代器，则该变量表示调用该方法或访问器时所针对的结构的一个副本，并且其行为与结构类型的 `value` 参数完全相同。

> **JON SKEET** 在值类型的方法中能够编写
>
> ```csharp
> this = new CustomStruct(...);
> ```
>
> 总让我觉得非常不对劲。考虑到结构体首先几乎总是应当不可变，我想知道这种写法在全球 C# 代码库中有多少合理的用途。

在除上述列出的上下文之外的上下文中，在*主表达式*中使用 this 是编译时错误。特别地，不能在静态方法、静态属性访问器或字段声明的*变量初始值设定项*中引用 this。

### 7.6.8 base 访问

*base 访问*由保留字 `base` 后跟一个“.”标记和一个标识符，或用方括号括起来的*参数列表*组成：

```text
base-access:
    base . identifier
    base [ argument-list ]
```

*base 访问*用于访问被当前类或结构中同名成员隐藏的基类成员。*base 访问*只允许在实例构造函数、实例方法或实例访问器的块中。当 `base.I` 出现在类或结构中时，`I` 必须表示该类或结构的基类的成员。同样，当 `base[E]` 出现在类中时，基类中必须存在适用的索引器。

在绑定时间，形如 `base.I` 和 `base[E]` 的*base 访问*表达式将完全按照它们被编写为 `((B)this).I` 和 `((B)this)[E]` 的方式求值，其中 `B` 是该构造所在类或结构的基类。因此，`base.I` 和 `base[E]` 对应于 `this.I` 和 `this[E]`，只不过这里的 this 被视为基类的实例。

> **VLADIMIR RESHETNIKOV** 如果后一种形式的*base 访问*是动态分派的（即，如果它具有类型为 *dynamic* 的参数），则发生编译时错误（CS1972）。

当*base 访问*引用虚拟函数成员（方法、属性或索引器）时，运行时确定调用哪个函数成员（§7.5.4）的方式会改变。所调用的函数成员通过查找该函数成员相对于 `B` 的最派生实现（§10.6.3）来确定（而不是像非 base 访问中通常那样相对于 this 的运行时类型来确定）。因此，在虚拟函数成员的*重写*中，可以使用*base 访问*来调用该函数成员的继承实现。如果*base 访问*引用的函数成员是抽象的，则发生绑定时间错误。

> **ERIC LIPPERT** 在 Microsoft C# 2.0 及更高版本的编译器中，对虚方法的 base 调用会生成为对编译时已知位于基类上的*特定*方法的非虚调用。如果你通过换入一个新版本的库（该库在“中间”新增了一个虚重写）来绕过编译器，而不重新编译进行 base 调用的代码，那么该代码将继续调用编译时标识的特定方法。简而言之，*base 调用不使用虚分派*。
>
> 转换为表达式树类型的 lambda 表达式包含 base 访问是不合法的。

### 7.6.9 后缀递增和递减运算符

```text
post-increment-expression:
    primary-expression ++

post-decrement-expression:
    primary-expression --
```

后缀递增或递减运算的操作数必须是分类为变量、属性访问或索引器访问的表达式。该运算的结果是与操作数类型相同的值。

如果*主表达式*的编译时类型为 *dynamic*，则该运算符进行动态绑定（§7.2.2），*后缀递增表达式*或*后缀递减表达式*的编译时类型为 *dynamic*，并且在运行时使用*主表达式*的运行时类型应用以下规则。



如果后缀递增或递减运算的操作数是属性或索引器访问，则该属性或索引器必须同时具有 get 和 set 访问器。如果不是这种情况，则发生绑定时间错误。

一元运算符重载解析（§7.3.3）用于选择特定的运算符实现。预定义的 ++ 和 -- 运算符适用于以下类型：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 以及任何枚举类型。预定义的 ++ 运算符返回将操作数加 1 所生成的值，预定义的 -- 运算符返回将操作数减 1 所生成的值。在受检查上下文中，如果该加法或减法的结果超出结果类型的范围，并且结果类型是整型或枚举类型，则抛出 System.OverflowException。

形式为 x++ 或 x-- 的后缀递增或递减运算的运行时处理包括以下步骤：

- 如果 x 被分类为变量：
  - 对 x 求值以产生该变量。
  - 保存 x 的值。
  - 以保存的 x 值作为参数调用所选运算符。
  - 运算符返回的值存储在由对 x 求值所给定的位置中。
  - 保存的 x 值成为该运算的结果。
- 如果 x 被分类为属性或索引器访问：
  - 对与 x 关联的实例表达式（如果 x 不是静态的）和参数列表（如果 x 是索引器访问）求值，并将结果用于后续的 get 和 set 访问器调用。
  - 调用 x 的 get 访问器并保存返回的值。
  - 以保存的 x 值作为参数调用所选运算符。
  - 以运算符返回的值作为值参数调用 x 的 set 访问器。
  - 保存的 x 值成为该运算的结果。

> **弗拉基米尔·列舍特尼科夫** 如果 get 访问器或 set 访问器缺失或不可访问，则发生编译时错误。

++ 和 -- 运算符还支持前缀表示法（§7.7.5）。通常，x++ 或 x-- 的结果是运算前 x 的值，而 ++x 或 --x 的结果是运算后 x 的值。无论哪种情况，运算后 x 本身都具有相同的值。

运算符 ++ 或运算符 -- 的实现可以使用后缀或前缀表示法调用。无法为这两种表示法分别提供不同的运算符实现。

## 7.6.10 new 运算符

new 运算符用于创建类型的新实例。

new 表达式有三种形式：

- 对象创建表达式用于创建类类型和值类型的新实例。
- 数组创建表达式用于创建数组类型的新实例。
- 委托创建表达式用于创建委托类型的新实例。

new 运算符意味着创建某个类型的实例，但不一定意味着动态分配内存。特别是，值类型的实例除了它们所在的变量之外不需要额外的内存，并且当使用 new 创建值类型的实例时不会发生动态分配。

### 7.6.10.1 对象创建表达式

对象创建表达式用于创建类类型或值类型的新实例。

```
object-creation-expression:
    new type ( argument-list_opt ) object-or-collection-initializer_opt
    new type object-or-collection-initializer

object-or-collection-initializer:
    object-initializer
    collection-initializer
```

对象创建表达式的类型必须是类类型、值类型或类型参数。该类型不能是抽象类类型。

仅当类型是类类型或结构类型时，才允许使用可选参数列表（§7.5.1）。

如果对象创建表达式包含对象初始值设定项或集合初始值设定项，则可以省略构造函数参数列表和括起它们的括号。省略构造函数参数列表和括起它们的括号等同于指定空参数列表。

处理包含对象初始值设定项或集合初始值设定项的对象创建表达式，包括首先处理实例构造函数，然后处理由对象初始值设定项（§7.6.10.2）或集合初始值设定项（§7.6.10.3）指定的成员初始化或元素初始化。

如果可选参数列表中的任何参数具有编译时类型 dynamic，则对象创建表达式是动态绑定的（§7.2.2），并且在运行时使用参数列表中具有编译时类型 dynamic 的那些参数的运行时类型来应用以下规则。但是，对象创建会经历有限的编译时检查，如 §7.5.4 所述。

形式为 new T(A) 的对象创建表达式的绑定时间处理（其中 T 是类类型或值类型，A 是可选参数列表）包括以下步骤：

- 如果 T 是值类型且 A 不存在：
  - 该对象创建表达式是默认构造函数调用。该对象创建表达式的结果是类型 T 的值——即 §4.1.1 中定义的 T 的默认值。
- 否则，如果 T 是类型参数且 A 不存在：
  - 如果没有为 T 指定值类型约束或构造函数约束（§10.1.5），则发生绑定时间错误。
  - 该对象创建表达式的结果是类型参数已绑定到的运行时类型的值——即调用该类型的默认构造函数的结果。该运行时类型可以是引用类型或值类型。
- 否则，如果 T 是类类型或结构类型：
  - 如果 T 是抽象类类型，则发生编译时错误。
  - 要调用的实例构造函数使用 §7.5.3 的重载解析规则确定。候选实例构造函数集合由 T 中声明的、相对于 A 适用的所有可访问实例构造函数组成（§7.5.3.1）。如果候选实例构造函数集合为空，或者无法标识单个最佳实例构造函数，则发生绑定时间错误。
  - 该对象创建表达式的结果是类型 T 的值——即调用上述步骤中确定的实例构造函数所生成的值。
- 否则，该对象创建表达式无效，并发生绑定时间错误。

即使对象创建表达式是动态绑定的，编译时类型仍然是 T。

形式为 new T(A) 的对象创建表达式的运行时处理（其中 T 是类类型或结构类型，A 是可选参数列表）包括以下步骤：

- 如果 *T* 是 *类类型*：
  - 分配类 *T* 的新实例。如果没有足够的内存可用于分配新实例，则抛出 `System.OutOfMemoryException`，并且不执行后续步骤。
  - 新实例的所有字段都被初始化为其默认值（§5.2）。
  - 根据函数成员调用规则（§7.5.4）调用实例构造函数。对新分配实例的引用会自动传递给实例构造函数，并且可以在该构造函数内部以 `this` 访问该实例。
- 如果 *T* 是 *结构类型*：
  - 通过分配临时局部变量来创建类型 *T* 的实例。由于 *结构类型* 的实例构造函数需要明确为所创建实例的每个字段赋值，因此不需要初始化临时变量。
  - 根据函数成员调用规则（§7.5.4）调用实例构造函数。对新分配实例的引用会自动传递给实例构造函数，并且可以在该构造函数内部以 `this` 访问该实例。

### 7.6.10.2 对象初始值设定项

*对象初始值设定项*指定对象的零个或多个字段或属性的值。

```
~~~
object-initializer:
    {  member-initializer-list_opt  }
    {  member-initializer-list  ,  }

member-initializer-list:
    member-initializer
    member-initializer-list  ,  member-initializer

member-initializer:
    identifier  =  initializer-value

initializer-value:
    expression
    object-or-collection-initializer
~~~
```

对象初始值设定项由一系列成员初始值设定项组成，这些成员初始值设定项由 { 和 } 标记包围并用逗号分隔。每个成员初始值设定项必须命名正在初始化的对象的一个可访问字段或属性，后跟等号以及表达式、对象初始值设定项或集合初始值设定项。对象初始值设定项包含……是错误的

对同一个字段或属性不能有多个成员初始化器。对象初始化器无法引用它正在初始化的新建对象。

指定等号后表达式的成员初始化器，按与对字段或属性的赋值（§7.17.1）相同的方式处理。

指定等号后对象初始化器的成员初始化器是一个嵌套对象初始化器——即对嵌入对象的初始化。不是为字段或属性分配新值，嵌套对象初始化器中的赋值被视为对字段或属性成员的赋值。嵌套对象初始化器不能应用于具有值类型的属性，或具有值类型的只读字段。

指定等号后集合初始化器的成员初始化器是对嵌入集合的初始化。不是为字段或属性分配新的集合，初始化器中给出的元素会被添加到字段或属性引用的集合中。字段或属性必须是满足 §7.6.10.3 中规定要求的集合类型。

下面的类表示具有两个坐标的点：

```
public class Point
{
    int x, y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

Point 的实例可以按如下方式创建并初始化：

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

其中 __a 是一个除此之外不可见且无法访问的临时变量。下面的类表示由两个点创建的矩形：

```
public class Rectangle
{
    Point p1, p2;
    public Point P1 { get { return p1; } set { p1 = value; } }
    public Point P2 { get { return p2; } set { p2 = value; } }
}
```

Rectangle 的实例可以按如下方式创建并初始化：

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

其中 __r、__p1 和 __p2 是除此之外不可见且无法访问的临时变量。

> JOSEPH ALBAHARI 使用隐藏的临时变量消除了在初始化期间抛出异常时得到部分初始化对象的可能性。相反，新构造的对象将被完全放弃：
> 
> ```
> Point p = null;
> int zero = 0;
> try { p = new Point { X = 3, Y = 4 / zero }; } // Throws DivideByZeroException
> catch { Console.WriteLine (p == null); } // True
> ```

> ERIC LIPPERT 使用隐藏的临时变量也使确定性赋值规则变得清晰。这里的第二行不等价于第一行：
> 
> ```
> Point p1 = new Point(); p1.Y = p1.X; // Legal
> Point p2 = new Point() { Y = p2.X }; // Not legal; p2 is not assigned yet
> ```
> 
> 如果 Rectangle 的构造函数分配了两个嵌入的 Point 实例：
> 
> ```
> public class Rectangle
> {
>     Point p1 = new Point();
>     Point p2 = new Point();
>     public Point P1 { get { return p1; } }
>     public Point P2 { get { return p2; } }
> }
> ```

以下构造可用于初始化嵌入的 Point 实例，而非分配新实例：

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

## 7.6.10.3 Collection Initializers

集合初始化器指定集合的元素。

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

集合初始化器由一系列元素初始化器组成，用 { 和 } 标记括起来并以逗号分隔。每个元素初始化器指定要添加到正在初始化的集合对象中的一个元素，并由用 { 和 } 标记括起来并以逗号分隔的表达式列表组成。单表达式元素初始化器可以不使用大括号书写，但此时不能是赋值表达式，以避免与成员初始化器的歧义。非赋值表达式产生式在 §7.18 中定义。

下面是一个包含集合初始化器的对象创建表达式的示例：

```
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

应用集合初始化器的集合对象必须是实现 System.Collections.IEnumerable 的类型，否则会发生编译时错误。对于每个指定的元素，按顺序，集合初始化器会在目标对象上调用 Add 方法，并将元素初始化器的表达式列表作为参数列表，使用正常的重载解析进行每次调用。因此，集合对象必须为每个元素初始化器包含一个适用的 Add 方法。

> ERIC LIPPERT 这里的规则有点奇怪：集合初始化器只有在对象实现 IEnumerable 且具有 Add 方法时才有效。请注意，在集合初始化器中我们从不调用 IEnumerable 的任何方法！那么为什么要要求它呢？C# 设计团队对现有对象进行了调查并得出了以下发现。首先，几乎所有具有 Add 方法的对象要么是集合，要么在实现某种算术运算。我们明确不希望此设计成为算术运算的语法糖——只是集合创建。其次，在那些是集合的对象中，没有一个通用的接口被它们全部实现的 Add 方法。第三，所有集合都实现了 IEnumerable，但没有任何算术对象实现它。出于所有这些原因，我们决定使用 IEnumerable 的存在加上 Add 方法作为判断集合初始化器是否有效的试金石。

下面的类表示具有姓名和电话号码列表的联系人：

```
public class Contact
{
    string name;
    List<string> phoneNumbers = new List<string>();
    public string Name { get { return name; } set { name = value; } }
    public List<string> PhoneNumbers { get { return phoneNumbers; } }
}
```

List<Contact> 可以按如下方式创建并初始化：

```
var contacts = new List<Contact> {
    new Contact {
        Name = "Chris Smith",
        PhoneNumbers = { "206-555-0101", "425-882-8080" }
    },
    new Contact {
        Name = "Bob Harris",
        PhoneNumbers = { "650-555-0199" }
    }
};
```

其效果与以下相同

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

其中 __clist、__c1 和 __c2 是除此之外不可见且无法访问的临时变量。

## 7.6.10.4 Array Creation Expressions

数组创建表达式用于创建数组类型的新的实例。

```
array-creation-expression:
new non-array-type [ expression-list ] rank-specifiers_opt array-initializer_opt
new array-type array-initializer
new rank-specifier array-initializer
```

第一种形式的数组创建表达式分配一个数组实例，其类型是从表达式列表中删除各个表达式后得到的类型。例如，数组创建表达式 new int[10, 20] 生成类型为 int[,] 的数组实例，而数组创建表达式 new int[10][,] 生成类型为 int[,] [,] 的数组。表达式列表中的每个表达式必须是 int、uint、long 或 ulong 类型，或可隐式转换为其中一种或多种类型。每个表达式的值决定了新分配数组实例中对应维度的长度。由于数组维度的长度必须为非负，因此在表达式列表中出现负值的常量表达式是编译时错误。

除在不安全上下文（§18.1）中外，数组的布局是未指定的。

如果第一种形式的数组创建表达式包含数组初始化器，表达式列表中的每个表达式必须是常量，并且表达式列表指定的秩和维度长度必须与数组初始化器的相匹配。

在第二种或第三种形式的数组创建表达式中，指定的数组类型或秩说明符的秩必须与数组初始化器的秩匹配。各个维度

长度是根据数组初始值设定项中各个对应嵌套层级的元素数量推断出来的。因此，表达式

```
`new int[,] {{0, 1}, {2, 3}, {4, 5}}`
```

完全对应于

```
`new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}`
```

第三种形式的数组创建表达式称为*隐式类型数组创建表达式*。它类似于第二种形式，不同之处在于数组的元素类型不是显式给出的，而是确定为数组初始值设定项中表达式集合的最常见类型（§7.5.2.14）。对于多维数组——即*秩说明符*包含至少一个逗号的数组——此集合包含嵌套*数组初始值设定项*中找到的所有*表达式*。

数组初始值设定项在 §12.6 中进一步描述。

对数组创建表达式求值的结果被归类为值——即对新分配的数组实例的引用。数组创建表达式的运行时处理包括以下步骤：

- *表达式列表*的维度长度表达式按从左到右的顺序求值。在对每个表达式求值之后，会执行到以下类型之一的隐式转换（§6.1）：int、uint、long、ulong。选择此列表中第一个存在隐式转换的类型。如果对某个表达式的求值或后续的隐式转换导致异常，则不再求值其他表达式，也不再执行后续步骤。
- 维度长度的计算值按如下方式验证。如果一个或多个值小于零，则引发 System.OverflowException，并且不再执行后续步骤。
- 分配具有给定维度长度的数组实例。如果没有足够的内存可用于分配新实例，则引发 System.OutOfMemoryException，并且不再执行后续步骤。
- 新数组实例的所有元素都初始化为其默认值（§5.2）。
- 如果数组创建表达式包含数组初始值设定项，则对数组初始值设定项中的每个表达式求值，并将其赋给对应的数组元素。求值和赋值按表达式在数组初始值设定项中写入的顺序执行——换句话说，元素按索引递增顺序初始化，其中最右侧维度最先递增。如果对给定表达式的求值或后续对相应数组元素的赋值导致异常，则不再初始化其他元素（因此其余元素将具有其默认值）。

数组创建表达式允许实例化其元素为数组类型的数组，但这种数组的元素必须手动初始化。例如，语句

```
int[][] a = new int[100][];
```

创建一个包含 100 个 int[] 类型元素的一维数组。每个元素的初始值为 null。同一个数组创建表达式不可能同时实例化子数组，而语句

```
int[][] a = new int[100][5];    // Error
```

会导致编译时错误。而子数组的实例化必须手动执行，如下所示：

```
int[][] a = new int[100][];
for (int i = 0; i < 100; i++) a[i] = new int[5];
```

> BILL WAGNER  下面的注释违反了 FxCop 规则，但确实解释了在哪些条件下应该违反该规则。

当数组的数组具有“矩形”形状——即所有子数组长度都相同时——使用多维数组更高效。在上面的示例中，实例化数组的数组会创建 101 个对象——一个外部数组和 100 个子数组。相比之下，

```
int[,] a = new int[100, 5];
```

只创建一个对象——即一个二维数组——并在单条语句中完成分配。

> PETER SESTOFT  语言规范包含关于效率的陈述是有些可疑的，因为效率是涉及实现而非语义的问题。确实，分配（并随后管理）一个 500 个整数的单块可能比 100 个 5 个整数的块更快，但作用于“慢”的数组的数组表示的矩阵乘法算法可能比作用于“高效”矩形数组表示的算法更快——这大概要归功于 JIT 编译器智能和现代 CPU 架构的结合。

以下为隐式类型数组创建表达式的示例：

```
var a = new[] { 1, 10, 100, 1000 };        // int[]
var b = new[] { 1, 1.5, 2, 2.5 };          // double[]
var c = new[,] { { "hello", null }, { "world", "!" } }; // string[,]
var d = new[] { 1, "one", 2, "two" };      // Error
```

最后一个表达式会导致编译时错误，因为 int 和 string 都不能隐式转换为对方，所以不存在最佳通用类型。在这种情况下必须使用显式类型数组创建表达式——例如，将类型指定为 object[]。或者，可以将其中一个元素强制转换为公共基类型，该类型随后将成为推断出的元素类型。

隐式类型数组创建表达式可以与匿名对象初始值设定项（§7.6.10.6）组合，以创建匿名类型的数据结构。例如：

```
var contacts = new[] {
    new {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0101", "425-888-8888" }
    },
    new {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

## 7.6.10.5 委托创建表达式

委托创建表达式用于创建委托类型的新实例。

```
delegate-creation-expression:
    new delegate-type ( expression )
```

委托创建表达式的参数必须是方法组、匿名函数，或者编译时类型为 dynamic 或委托类型的值。如果参数是方法组，则它标识方法；对于实例方法，还标识要为其创建委托的对象。如果参数是匿名函数，则它直接定义委托目标的参数和方法体。如果参数是值，则它标识要为其创建副本的委托实例。

如果表达式的编译时类型为 dynamic，则委托创建表达式进行动态绑定（§7.2.2），下面的规则在运行时使用该表达式的运行时类型来应用。否则，这些规则在编译时应用。

对于形式为 new D(E) 的委托创建表达式（其中 D 是委托类型，E 是表达式），其绑定时间处理包括以下步骤：

- 如果 E 是方法组，则委托创建表达式的处理方式与从 E 到 D 的方法组转换（§6.6）相同。
- 如果 E 是匿名函数，则委托创建表达式的处理方式与从 E 到 D 的匿名函数转换（§6.5）相同。
- 如果 E 是值，则 E 必须与 D 兼容（§15.1），结果是引用一个新创建的 D 类型委托，该委托引用与 E 相同的调用列表。如果 E 与 D 不兼容，则发生编译时错误。

对于形式为 new D(E) 的委托创建表达式（其中 D 是委托类型，E 是表达式），其运行时处理包括以下步骤：

- 如果 E 是方法组，则委托创建表达式按从 E 到 D 的方法组转换（§6.6）进行求值
- 如果 E 是匿名函数，则委托创建按从 E 到 D 的匿名函数转换（§6.5）进行求值。
- 如果 E 是委托类型的值：
  - 对 E 求值。如果此求值导致异常，则不再执行后续步骤。
  - 如果 E 的值为 null，则引发 System.NullReferenceException，并且不再执行后续步骤。
  - 分配委托类型 D 的新实例。如果没有足够的内存可用于分配新实例，则引发 System.OutOfMemoryException，并且不再执行后续步骤。
  - 新委托实例使用与 E 给定的委托实例相同的调用列表进行初始化。

委托的调用列表在委托实例化时确定，然后在委托的整个生存期内保持不变。换句话说，委托一旦创建，就不可能更改其目标可调用实体。当组合两个委托或从一个委托中移除另一个委托（§15.1）时，将产生一个新委托；现有委托的内容不会改变。

无法创建引用属性、索引器、用户定义运算符、实例构造函数、析构函数或静态构造函数的委托。

如上所述，当从方法组创建委托时，委托的形参列表和返回类型确定要选择哪个重载方法。在下面的示例中

```
delegate double DoubleFunc(double x);
class A
{
    DoubleFunc f = new DoubleFunc(Square);
    static float Square(float x) {
        return x * x;
    }
}
```


```
static double Square(double x) {
    return x * x;
}
```

A.f 字段用委托初始化，该委托引用第二个 Square 方法，因为该方法与 DoubleFunc 的形参列表和返回类型完全匹配。如果第二个 Square 方法不存在，则会发生编译时错误。

## 7.6.10.6 匿名对象创建表达式

匿名对象创建表达式用于创建匿名类型的对象。

```
anonymous-object-creation-expression:
    new anonymous-object-initializer

anonymous-object-initializer:
    { member-declarator-list opt }
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

> **VLADIMIR RESHETNIKOV** 仅当基访问的形式为 base.identifier 时，它才能是成员声明符；也就是说，此处不允许基索引器访问。

匿名对象初始值设定项声明匿名类型并返回该类型的实例。匿名类型是直接继承自 object 的无名类类型。匿名类型的成员是根据用于创建该类型实例的匿名对象初始值设定项推断出的一系列只读属性。具体而言，形式为

```
new { p₁ = e₁ , p₂ = e₂ , … pₙ = eₙ }
```

的匿名对象初始值设定项声明如下形式的匿名类型

```
class __Anonymous1
{
    private readonly T₁ f₁;
    private readonly T₂ f₂;
    ...
    private readonly Tₙ fₙ;
    public __Anonymous1(T₁ a₁, T₂ a₂, ..., Tₙ aₙ) {
        f₁ = a₁;
        f₂ = a₂;
        ...
        fₙ = aₙ;
    }
    public T₁ p₁ { get { return f₁; } }
    public T₂ p₂ { get { return f₂; } }
    ...
    public Tₙ pₙ { get { return fₙ; } }
    public override bool Equals(object o) { ... }
    public override int GetHashCode() { ... }
}
```

其中每个 T_i 是对应表达式 e_i 的类型。成员声明符中使用的表达式必须具有类型。因此，如果成员声明符中的表达式为 null 或匿名函数，则是编译时错误。表达式具有不安全类型也是编译时错误。

> **ERIC LIPPERT** Microsoft 实现为匿名类型生成的实际代码比这里讨论的要复杂一些，因为（后面会提到）希望结构等效的匿名类型在整个程序中由同一类型表示。由于字段类型可能是受保护的嵌套类型，因此很难确定究竟在哪里生成匿名类，以便它能在不同派生类型之间有效共享。为此，Microsoft 实现实际上生成一个泛型类，然后用适当的类型实参构造它。

匿名类型的名称由编译器自动生成，不能在程序文本中引用。

> **JON SKEET** 听起来虽然矛盾，但我确实很想看到命名匿名类型：这些类像匿名类型一样易于表达，并具有相同的不可变性、自然相等性以及属性的类型和名称安全性——但带有名称。尽管许多工具可以将匿名类型“展开”为等价的普通类，但此时类型表达的简洁性就丢失了。

在同一程序中，两个匿名对象初始值设定项如果按相同顺序指定具有相同名称和编译时类型的一系列属性，则将生成同一匿名类型的实例。

在示例

```
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```

中，最后一行的赋值是允许的，因为 p1 和 p2 属于同一匿名类型。

匿名类型上的 Equals 和 GetHashCode 方法重写从 object 继承的方法，并且根据属性的 Equals 和 GetHashCode 定义，因此同一匿名类型的两个实例相等当且仅当它们的所有属性都相等。

成员声明符可缩写为简单名称（§7.5.2）、成员访问（§7.5.4）或基访问（§7.6.8）。这称为投影初始值设定项，是声明并赋值给具有相同名称的属性的简写形式。具体而言，形式如下的成员声明符：

| 成员声明符形式 | 等价形式 |
| --- | --- |
| `identifier` | `identifier = identifier` |
| `expr . identifier` | `identifier = expr . identifier` |

分别完全等价。

因此，在投影初始值设定项中，标识符既选择值，也选择该值所赋到的字段或属性。直观地说，投影初始值设定项不仅投影值，还投影值的名称。

## 7.6.11 typeof 运算符

typeof 运算符用于获取类型的 System.Type 对象。

```
typeof-expression:
    typeof ( type )
    typeof ( unbound-type-name )
    typeof ( void )

unbound-type-name:
    identifier generic-dimension-specifier_opt
    identifier :: identifier generic-dimension-specifier_opt
    unbound-type-name . identifier generic-dimension-specifier_opt
```

```
generic-dimension-specifier:
    < commas_opt >

commas:
    ,
    commas ,
```

typeof 表达式的第一种形式由 typeof 关键字后跟括号中的类型组成。这种形式的表达式的结果是指示类型的 System.Type 对象。对于任何给定类型，只有一个 System.Type 对象。这意味着对于类型 T，typeof(T) == typeof(T) 始终为 true。该类型不能是 dynamic。

typeof 表达式的第二种形式由 typeof 关键字后跟括号中的未绑定类型名称组成。未绑定类型名称与类型名称（§3.8）非常相似，不同之处在于未绑定类型名称包含泛型维度说明符，而类型名称包含类型实参列表。当 typeof 表达式的操作数是一个同时满足未绑定类型名称和类型名称语法的标记序列时——即它既不包含泛型维度说明符也不包含类型实参列表——该标记序列被视为类型名称。未绑定类型名称的含义按如下方式确定：

- 通过将每个泛型维度说明符替换为具有相同逗号数量且每个类型实参均为关键字 object 的类型实参列表，将该标记序列转换为类型名称。
- 在忽略所有类型参数约束的情况下，计算得到的类型名称。
- 未绑定类型名称解析为与所得构造类型关联的未绑定泛型类型（§4.4.3）。

typeof 表达式的结果是所得未绑定泛型类型的 System.Type 对象。

typeof 表达式的第三种形式由 typeof 关键字后跟括号中的 void 关键字组成。这种形式的表达式的结果是表示没有类型的 System.Type 对象。typeof(void) 返回的类型对象不同于为任何类型返回的类型对象。这个特殊类型对象在允许对语言中的方法进行反射的类库中很有用，在这些类库中，这些方法希望有一种方式用 System.Type 实例表示任何方法（包括 void 方法）的返回类型。

typeof 运算符可用于类型参数。结果是绑定到该类型参数的运行时类型的 System.Type 对象。typeof 运算符还可用于构造类型或未绑定泛型类型（§4.4.3）。未绑定泛型类型的 System.Type 对象与实例类型的 System.Type 对象不同。实例类型在运行时始终是封闭构造类型，因此其 System.Type 对象取决于使用中的运行时类型实参，而未绑定泛型类型没有类型实参。

示例

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
            typeof(X<>),
            typeof(X<X<T>>),
            typeof(X<T>)
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
X`1[System.Int32]
X`1[X`1[System.Int32]]
X`1[T]
```

注意，int 和 System.Int32 是同一类型。

另请注意，typeof(X<>) 的结果不依赖于类型实参，而 typeof(X<T>) 的结果则依赖。




## 7.6.12 checked 和 unchecked 运算符

checked 和 unchecked 运算符用于控制整型算术运算和转换的溢出检查上下文。

```
checked-expression:
    checked ( expression )
```

```
unchecked-expression:
    unchecked ( expression )
```

checked 运算符在 checked 上下文中计算所包含的表达式，而 unchecked 运算符在 unchecked 上下文中计算所包含的表达式。checked-expression 或 unchecked-expression 与 parenthesized-expression（§7.6.3）完全对应，不同之处在于所包含的表达式是在给定的溢出检查上下文中计算的。

> 乔恩·斯基特：在大多数情况下，溢出表示错误——但根据我的经验，大多数开发者（包括我自己）通常默认在关闭检查功能的情况下构建。显然，这种做法会有性能损失，但通常比数据被悄悄破坏要好。将 /checked+ 设为调试版本的默认值、将 /checked- 设为发布版本的默认值可能是有意义的——不过，我通常对调试版本和发布版本之间的行为差异保持警惕。这有点类似于 Windows Forms 中跨线程异常的行为。
> 
> 在几乎总是适合采用未检查溢出行为的一种情况是 GetHashCode 实现中，此时生成值的大小并不真正重要；本质上，它只是一个任意的位模式。

溢出检查上下文也可以通过 checked 和 unchecked 语句（§8.11）控制。

以下操作受 checked 和 unchecked 运算符及语句所建立的溢出检查上下文影响：

- 预定义的 ++ 和 -- 一元运算符（§7.6.9 和 §7.7.5），当操作数为整型时。
- 预定义的 - 一元运算符（§7.7.2），当操作数为整型时。
- 预定义的 +、-、* 和 / 二元运算符（§7.8），当两个操作数均为整型时。
- 从一个整型到另一个整型的显式数值转换（§6.2.1），或从 float 或 double 到整型的显式数值转换。

当上述操作之一产生的结果太大而无法在目标类型中表示时，执行该操作的上下文控制最终行为：

- 在 checked 上下文中，如果该操作是常量表达式（§7.19），则发生编译时错误。否则，当该操作在运行时执行时，将抛出 System.OverflowException。
- 在 unchecked 上下文中，结果会被截断，丢弃任何不适合目标类型的高阶位。

对于未包含在任何 checked 或 unchecked 运算符或语句中的非常量表达式（在运行时计算的表达式），默认溢出检查上下文为 unchecked，除非外部因素（例如编译器开关和执行环境配置）要求进行 checked 求值。

对于常量表达式（可以在编译时完全求值的表达式），默认溢出检查上下文始终为 checked。除非常量表达式被显式置于 unchecked 上下文中，否则在表达式的编译时求值期间发生的溢出始终会导致编译时错误。

匿名函数的主体不受该匿名函数所在 checked 或 unchecked 上下文的影响。

在示例

```
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;

    static int F() {
        return checked(x * y);  // Throws OverflowException
    }

    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }

    static int H() {
        return x * y;             // Depends on default
    }
}
```

中，不会报告编译时错误，因为这两个表达式都无法在编译时求值。在运行时，F 方法抛出 System.OverflowException，G 方法返回 −727379968（超出范围结果的低 32 位）。H 方法的行为取决于编译的默认溢出检查上下文，但它要么与 F 相同，要么与 G 相同。

在示例

```
class Test
{
    const int x = 1000000;
    const int y = 1000000;

    static int F() {
        return checked(x * y);     // Compile error, overflow
    }
    static int G() {
        return unchecked(x * y);   // Returns -727379968
    }
    static int H() {
        return x * y;              // Compile error, overflow
    }
}
```

中，求值 F 和 H 中的常量表达式时发生的溢出会导致报告编译时错误，因为这些表达式是在 checked 上下文中求值的。求值 G 中的常量表达式时也会发生溢出，但由于求值发生在 unchecked 上下文中，因此不会报告溢出。

checked 和 unchecked 运算符仅对文本上包含在“(”和“)”标记内的那些操作影响溢出检查上下文。这些运算符对因求值所包含表达式而调用的函数成员没有影响。在示例

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

中，F 中 checked 的使用不影响 Multiply 中 x * y 的求值，因此 x * y 是在默认溢出检查上下文中求值的。

当以十六进制记法编写有符号整型的常量时，unchecked 运算符很方便。例如：

```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

上述两个十六进制常量均为 uint 类型。由于这些常量超出 int 范围，如果没有 unchecked 运算符，到 int 的强制转换将产生编译时错误。

checked 和 unchecked 运算符及语句允许程序员控制某些数值计算的某些方面。然而，某些数值运算符的行为取决于其操作数的数据类型。例如，两个 decimal 相乘即使在显式 unchecked 构造中，也始终会在溢出时引发异常。类似地，两个 float 相乘即使在显式 checked 构造中，也绝不会在溢出时引发异常。此外，其他运算符从不受检查模式影响，无论是默认模式还是显式模式。

## 7.6.13 默认值表达式

默认值表达式用于获取类型的默认值（§5.2）。通常，默认值表达式用于类型参数，因为可能不知道类型参数是值类型还是引用类型。（除非类型参数已知为引用类型，否则不存在从 null 字面量到类型参数的转换。）

```
default-value-expression:
    default ( type )
```

如果 default-value-expression 中的类型在运行时求值为引用类型，则结果为转换为该类型的 null。如果 default-value-expression 中的类型在运行时求值为值类型，则结果为该值类型的默认值（§4.1.2）。

如果类型是引用类型或已知为引用类型的类型参数（§10.1.5），则 default-value-expression 是常量表达式（§7.19）。此外，如果类型是以下值类型之一，则 default-value-expression 是常量表达式：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool 或任何枚举类型。

> **约瑟夫·阿尔巴哈里** 默认值表达式在泛型类型参数中特别有用。Microsoft 的 LINQ 实现广泛使用了此构造，例如在 FirstOrDefault、SingleOrDefault 和 DefaultIfEmpty 等运算符中。

## 7.6.14 匿名方法表达式

*匿名方法表达式*是定义匿名函数的两种方式之一。这些内容将在 §7.15 中进一步描述。

## 7.7 一元运算符

+、-、!、~、++、-- 和强制转换运算符称为一元运算符。

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
```

如果 *unary-expression* 的操作数具有编译时类型 *dynamic*，则对其进行动态绑定（§7.2.2）。在这种情况下，*unary-expression* 的编译时类型为 *dynamic*，并且下面描述的决定将在运行时使用操作数的运行时类型进行。

### 7.7.1 一元加运算符

对于形式为 +x 的操作，应用一元运算符重载决策（§7.3.3）来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。预定义的一元加运算符列出如下：

```
int operator +(int x);
uint operator +(uint x);
long operator +(long x);
ulong operator +(ulong x);
float operator +(float x);
double operator +(double x);
decimal operator +(decimal x);
```

对于这些运算符中的每一个，结果都只是操作数的值。

> 埃里克·利珀特：一元加运算符是世界上最没用的运算符。它被包含进来是为了完整性，这样你就可以编写 int x = -30; int y = +40;，如果你希望出于可读性目的强调该值为正数的话。





## 7.7.2 一元减运算符

对于形式为 -x 的运算，将应用一元运算符重载解析（§7.3.3）来选择特定的运算符实现。操作数将转换为所选运算符的参数类型，结果的类型则为该运算符的返回类型。预定义的求负运算符如下：

- 整数求负：

```
int operator -(int x);
long operator -(long x);
```

结果通过从零中减去 x 计算得出。如果 x 的值是操作数类型所能表示的最小值（int 为 −2³¹，long 为 −2⁶³），则 x 的数学负值无法在操作数类型中表示。如果该情况发生在 checked 上下文中，则会引发 System.OverflowException；如果发生在 unchecked 上下文中，则结果为操作数的值，并且不会报告溢出。

如果求负运算符的操作数为 uint 类型，则会将其转换为 long 类型，结果的类型也是 long。允许将 int 值 −2147483648（−2³¹）写作十进制整数字面量（§2.4.4.2）的规则是一种例外。

如果求负运算符的操作数为 ulong 类型，则会发生编译时错误。允许将 long 值 −9223372036854775808（−2⁶³）写作十进制整数字面量（§2.4.4.2）的规则是一种例外。

- 浮点数求负：

```
float operator -(float x);
double operator -(double x);
```

结果是 x 的值，但其符号取反。如果 x 为 NaN，则结果也为 NaN。

- decimal 求负：

```
decimal operator -(decimal x);
```

## 7.7.3 逻辑求反运算符

对于形式为 !x 的运算，将应用一元运算符重载解析（§7.3.3）来选择特定的运算符实现。操作数将转换为所选运算符的参数类型，结果的类型则为该运算符的返回类型。预定义的逻辑求反运算符只有一个：

```
bool operator !(bool x);
```

此运算符计算操作数的逻辑否定：如果操作数为 true，则结果为 false；如果操作数为 false，则结果为 true。

## 7.7.4 按位求补运算符

对于形式为 ~x 的运算，将应用一元运算符重载解析（§7.3.3）来选择特定的运算符实现。操作数将转换为所选运算符的参数类型，结果的类型则为该运算符的返回类型。预定义的按位求补运算符如下：

```
    int operator ~(int x);
    uint operator ~(uint x);
    long operator ~(long x);
    ulong operator ~(ulong x);
```

对于上述每个运算符，运算结果都是 x 的按位补码。

每个枚举类型 E 都隐式提供以下按位求补运算符：

```
    E operator ~(E x);
```

> > **比尔·瓦格纳** 此运算符通常会为枚举创建一个无效值。

对枚举类型 E 的表达式 x 求值 ~x 时，如果其基础类型为 U，则其结果与计算 (E)(~(U)x) 完全相同。

## 7.7.5 前缀递增和递减运算符

```
    pre-increment-expression:
        ++ unary-expression

    pre-decrement-expression:
        -- unary-expression
```

前缀递增或递减运算的操作数必须是归类为变量、属性访问或索引器访问的表达式。运算结果的类型与操作数的类型相同。

如果前缀递增或递减运算的操作数是属性访问或索引器访问，则该属性或索引器必须同时具有 get 访问器和 set 访问器。如果不满足此条件，则会发生绑定时错误。

将应用一元运算符重载解析（§7.3.3）来选择特定的运算符实现。以下类型具有预定义的 ++ 和 -- 运算符：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 以及任何枚举类型。预定义的 ++ 运算符返回将操作数加 1 后得到的值，预定义的 -- 运算符返回将操作数减 1 后得到的值。在 checked 上下文中，如果加法或减法的结果超出结果类型的范围，并且结果类型是整数类型或枚举类型，则会引发 System.OverflowException。

形式为 ++x 或 --x 的前缀递增或递减运算的运行时处理包括以下步骤：

- 如果 x 被归类为变量：
  - 对 x 求值以生成该变量。
  - 调用所选运算符，并将 x 的值作为其参数。
  - 将运算符返回的值存储到对 x 求值所确定的位置中。
  - 运算符返回的值成为运算结果。

- 如果 x 被归类为属性访问或索引器访问：
  - 对与 x 关联的实例表达式（如果 x 不是静态成员）和参数列表（如果 x 是索引器访问）求值，并在后续调用 get 和 set 访问器时使用所得结果。
  - 调用 x 的 get 访问器。
  - 调用所选运算符，并将 get 访问器返回的值作为其参数。
  - 调用 x 的 set 访问器，并将运算符返回的值作为其值参数。

> > **弗拉基米尔·佩舍特尼科夫** 如果缺少 *get 访问器* 或 *set 访问器*，或者访问器不可访问，则会发生编译时错误。

- 运算符返回的值成为运算结果。

++ 和 -- 运算符也支持后缀表示法（§7.6.9）。通常，x++ 或 x-- 的结果是运算前 x 的值，而 ++x 或 --x 的结果是运算后 x 的值。无论哪种情况，运算完成后 x 本身都具有相同的值。

![](img/04b421b044b1254de966ab5335775a89_346_0.png)

> **埃里克·利珀特** 请注意规范中的措辞“通常”。确实，几乎总是如此，但规范并未要求必须如此。运算后 x 的值可以是任意旧值；可能有其他线程正在修改 x，x 也可能是一个属性，每次调用其 getter 时都会返回随机值，等等。

请考虑以下代码：

```
index = 0; value = this.arr[index++];
```

我经常听到有人这样描述这段代码：“它获取索引零处的元素，然后将 index 递增到一；由于 ++ 位于索引之后，因此递增发生在数组查找之后。”如果你仔细阅读规范，就会发现这种说法完全错误。正确的事件顺序是：(1) 记住 index 的当前值；(2) 递增 index；(3) 使用记住的值执行数组查找。递增发生在查找之前，而不是之后。

```
index = 0; value = this.arr[index++];
```

可以使用后缀或前缀表示法调用 operator ++ 或 operator -- 的实现。不可能针对这两种表示法分别提供运算符实现。

## 7.7.6 强制转换表达式

强制转换表达式用于将一个表达式显式转换为指定类型。

```
cast-expression:
( type ) unary-expression
```

形式为 (T)E 的强制转换表达式中，T 是类型，E 是一元表达式，该表达式会将 E 的值显式转换（§6.2）为类型 T。如果不存在从 E 到 T 的显式转换，则会发生绑定时错误。否则，结果就是显式转换所产生的值。即使 E 表示一个变量，结果也始终归类为值。

> **埃里克·利珀特** 强制转换运算符有些与众不同，既因为其不寻常的语法，也因为其语义。强制转换运算符通常用于表示以下两种含义之一：（1）我断言运行时的值不会是强制转换类型；请采取一切必要措施，将其转换为所需类型的新值；或者（2）我断言运行时的值将是强制转换类型；如果我的断言错误，则通过引发异常来验证它。细心的读者会注意到，这两种含义是相互对立的。让一个运算符完成两件相反的事情确实是一种巧妙的设计，但其结果是，人们很容易混淆强制转换运算符实际执行的操作。




强制转换表达式的语法会导致某些句法歧义。例如，表达式 (x)-y 既可以解释为强制转换表达式（将 -y 强制转换为类型 x），也可以解释为加法表达式与括号表达式的组合（计算值 x - y）。

为了解决强制转换表达式的歧义，存在以下规则：仅当至少满足下列条件之一时，括在括号中的一个或多个标记（§2.3.3）才被视为强制转换表达式的开头：

- 该标记序列符合类型的正确语法，但不符合表达式的语法。
- 该标记序列符合类型的正确语法，并且紧跟在右括号之后的标记是标记“,”、标记“!”、标记“(”、标识符（§2.4.1）、字面量（§2.4.4）或除 as 和 is 之外的任何关键字（§2.4.3）。

上文的“正确的语法”一词仅表示该标记序列必须符合特定的语法产生式。它明确不考虑任何组成标识符的实际含义。例如，如果 x 和 y 是标识符，那么 x.y 符合类型的正确语法，即使 x.y 实际上并不表示一个类型。

根据消歧规则可知，如果 x 和 y 是标识符，则 (x)y、(x)(y) 和 (x)(-y) 是强制转换表达式，而 (x)-y 不是，即使 x 标识一个类型。然而，如果 x 是标识预定义类型（例如 int）的关键字，那么所有四种形式都是强制转换表达式（因为这样的关键字本身不可能是一个表达式）。

## 7.8 算术运算符

*, /, %, + 和 - 运算符称为算术运算符。

```
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

如果算术运算符的操作数具有编译时类型 dynamic，则该表达式是动态绑定的（§7.2.2）。在这种情况下，表达式的编译时类型为 dynamic，并且下文所述的重载解析将在运行时使用那些编译时类型为 dynamic 的操作数的运行时类型进行。

> **PETER SESTOFT** 当把 double 等简单类型的值赋给 dynamic 类型的变量时，通常必须在运行时对其进行装箱（作为对象存储在堆中）。因此，使用 dynamic 类型操作数的算术计算可能比使用简单编译时类型的计算更慢。例如，在 Microsoft .NET 4.0 上，这个循环比将 sum 声明为 double 类型时大约慢六倍：
>
> ```csharp
> dynamic sum = 0;
> for (int i=0; i<count; i++)
>     sum += (i + 1.0) * i;
> ```
>
> 实际上，与一些其他动态类型语言中的算术运算相比，这已经非常快了。

### 7.8.1 乘法运算符

对于形式为 x * y 的运算，会应用二元运算符重载解析（§7.3.4）来选择特定的运算符实现。操作数会转换为所选运算符的参数类型，而结果的类型是运算符的返回类型。

下面列出了预定义的乘法运算符。这些运算符都计算 x 和 y 的乘积。

- **整数乘法：**
  
  ```csharp
  int operator *(int x, int y);
  uint operator *(uint x, uint y);
  long operator *(long x, long y);
  ulong operator *(ulong x, ulong y);
  ```
  
  在受检查上下文中，如果乘积超出结果类型的范围，则引发 `System.OverflowException`。在未检查上下文中，不会报告溢出，并且结果类型范围之外的任何有效高位都将被丢弃。

- **浮点乘法：**
  
  ```csharp
  float operator *(float x, float y);
  double operator *(double x, double y);
  ```
  
  乘积根据 IEEE 754 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是正有限值；z 是 x * y 的结果。如果结果对目标类型而言太大，则 z 为无穷大。如果结果对目标类型而言太小，则 z 为零。

| | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | -z | +0 | -0 | +∞ | -∞ | NaN |
| -x | -z | +z | -0 | +0 | -∞ | +∞ | NaN |
| +0 | +0 | -0 | +0 | -0 | NaN | NaN | NaN |
| -0 | -0 | +0 | -0 | +0 | NaN | NaN | NaN |
| +∞ | +∞ | -∞ | NaN | NaN | +∞ | -∞ | NaN |
| -∞ | -∞ | +∞ | NaN | NaN | -∞ | +∞ | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- **十进制乘法：**

```
decimal operator *(decimal x, decimal y);
```

如果结果值太大而无法用 decimal 格式表示，则引发 System.OverflowException。如果结果值太小而无法用 decimal 格式表示，则结果为零。在任何舍入之前，结果的小数位数是两个操作数的小数位数之和。

十进制乘法等效于使用 System.Decimal 类型的乘法运算符。

> **PETER SESTOFT** 本章此处及其他地方若说“IEEE 754 浮点”，更精确的说法应是“IEEE754 二进制浮点”，因为该 IEEE 标准的 2008 版既描述二进制浮点，也描述十进制浮点，而这两者非常不同！
>
> 此外，以下规则由 IEEE 754 二进制浮点标准规定，并得到当前 Microsoft 和 Mono C# 实现的遵守：只要一个或多个操作数是 NaN，结果就是 NaN，并且结果的 NaN 载荷等于某个 NaN 操作数的载荷。64 位 double 的 NaN 载荷由其 51 个最低有效位组成（因此 double 可以表示 2^51——大约 2*10^15——个不同的 NaN）。32 位 float 的 NaN 载荷由其 22 个最低有效位组成（因此 float 可以表示 2^22——大约 4*10^6——个不同的 NaN）。

保留 NaN 载荷对于高效的科学计算很重要。要让这种方法真正可行，除了算术运算符之外，System.Math 中的数学函数也应当遵循 IEEE 二进制浮点标准。在当前的实现中，它们大多是这样做的。

.NET 库提供方法 System.Double.IsNan(d) 来测试 double 是否为 NaN。

对于 double 类型，它还提供方法 DoubleToInt64Bits 和 Int64BitsToDouble，可用于获取和设置 NaN 载荷位：

```
public static long GetNanPayload(double d) {
    return System.BitConverter.DoubleToInt64Bits(d) & 0x0007FFFFFFFFFFFF;
}

public static double MakeNanPayload(long nanbits) {
    nanbits &= 0x0007FFFFFFFFFFFF;
    nanbits |= System.BitConverter.DoubleToInt64Bits(Double.NaN);
    return System.BitConverter.Int64BitsToDouble(nanbits);
}
```

奇怪的是，.NET 库没有针对 float 类型的对应方法，但可以使用不安全指针转换来达到相同效果。详细情况参见 §18.4 的注释。

### 7.8.2 除法运算符

对于形式为 x / y 的运算，会应用二元运算符重载解析（§7.3.4）来选择特定的运算符实现。操作数会转换为所选运算符的参数类型，而结果的类型是运算符的返回类型。

下面列出了预定义的除法运算符。这些运算符都计算 x 和 y 的商。

- **整数除法：**

```
int operator /(int x, int y);
uint operator /(uint x, uint y);
long operator /(long x, long y);
ulong operator /(ulong x, ulong y);
```

如果右操作数的值为零，则引发 System.DivideByZeroException。

除法将结果向零舍入。因此，结果的绝对值是小于或等于两个操作数之商的绝对值的最大可能整数。当两个操作数符号相同时，结果为零或正数；当两个操作数符号相反时，结果为零或负数。





如果左操作数是最小的可表示 int 或 long 值，而右操作数是 −1，则会发生溢出。在 checked 上下文中，这会抛出 System.OverflowException（或其子类）。在 unchecked 上下文中，是抛出 System.OverflowException（或其子类）还是让溢出不被报告且结果值为左操作数的值，由实现定义。

- 浮点除法：

```
float operator /(float x, float y);
double operator /(double x, double y);
```

商根据 IEEE 754 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是正有限值；z 是 x / y 的结果。如果结果对于目标类型太大，则 z 是无穷大。如果结果对于目标类型太小，则 z 是零。

|  | +y | −y | +0 | −0 | +∞ | −∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | −z | +∞ | −∞ | +0 | −0 | NaN |
| −x | −z | +z | −∞ | +∞ | −0 | +0 | NaN |
| +0 | +0 | −0 | NaN | NaN | +0 | −0 | NaN |
| −0 | −0 | +0 | NaN | NaN | −0 | +0 | NaN |
| +∞ | +∞ | −∞ | +∞ | −∞ | NaN | NaN | NaN |
| −∞ | −∞ | +∞ | −∞ | +∞ | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制除法：

```
decimal operator /(decimal x, decimal y);
```

如果右操作数的值为零，则抛出 System.DivideByZeroException。如果结果值太大而无法用 decimal 格式表示，则抛出 System.OverflowException。如果结果值太小而无法用 decimal 格式表示，则结果为零。结果的小数位数是能够使结果等于与真实数学结果最接近的可表示 decimal 值所需的最小小数位数。

十进制除法等价于使用 System.Decimal 类型的除法运算符。

## 7.8.3 余数运算符

对于形式为 x % y 的操作，应用二元运算符重载决策（§7.3.4）来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型就是该运算符的返回类型。

预定义的余数运算符如下所示。这些运算符都计算 x 和 y 之间除法的余数。

- 整数余数：

```csharp
int operator %(int x, int y);
uint operator %(uint x, uint y);
long operator %(long x, long y);
ulong operator %(ulong x, ulong y);
```

x % y 的结果是由 x − (x / y) * y 生成的值。如果 y 为零，则抛出 System.DivideByZeroException。

> > **埃里克·利珀特**  思考以下代码：
> >
> > ```csharp
> > static bool IsOdd(int x) { return x%2 == 1; }
> > ```
> >
> > 正确吗？不正确！根据上面的句子，这等同于
> >
> > ```csharp
> > static bool IsOdd(int x) { return x-(x/2)*2 == 1; }
> > ```
> >
> > 如果 x 是 -1，则结果为假。正确的代码是
> >
> > ```csharp
> > static bool IsOdd(int x) { return x%2 != 0; }
> > ```

如果左操作数是最小的 int 或 long 值，且右操作数为 −1，则抛出 System.OverflowException。在 x / y 不会抛出异常的情况下，x % y 也绝不会抛出异常。

- 浮点余数：

```csharp
float operator %(float x, float y);
double operator %(double x, double y);
```

下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是正有限值；z 是 x % y 的结果，计算方式为 x − n * y，其中 n 是小于或等于 x / y 的最大可能整数。这种计算余数的方法与整数操作数使用的方法类似，但不同于 IEEE 754 定义（其中 n 是离 x / y 最近的整数）。

| | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | +z | NaN | NaN | x | x | NaN |
| -x | -z | -z | NaN | NaN | -x | -x | NaN |
| +0 | +0 | +0 | NaN | NaN | +0 | +0 | NaN |
| -0 | -0 | -0 | NaN | NaN | -0 | -0 | NaN |
| +∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| -∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制余数：

```
decimal operator %(decimal x, decimal y);
```

如果右操作数的值为零，则抛出 System.DivideByZeroException。结果的小数位数（在进行任何舍入之前）是两个操作数中较大的小数位数；如果结果非零，其符号与 x 相同。

十进制余数等价于使用 System.Decimal 类型的余数运算符。

> 克里斯·塞尔斯 “余数”运算符在其他计算机语言中也称为“模”（modulo），有时记作“mod”。如果你真的是个极客，你会发现在（大致）人类语句中你会用“modulo”而不是“除了……之外”，比如：“‘除了测试、调试和文档，我们准备发布了！’”

## 7.8.4 加法运算符

对于形式为 x + y 的操作，应用二元运算符重载决策（§7.3.4）来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型就是该运算符的返回类型。

预定义的加法运算符如下所示。对于数值类型和枚举类型，预定义的加法运算符计算两个操作数的和。当一个或两个操作数为 string 类型时，预定义的加法运算符将操作数的字符串表示进行连接。

- 整数加法：

```
int operator +(int x, int y);
uint operator +(uint x, uint y);
long operator +(long x, long y);
ulong operator +(ulong x, ulong y);
```

在 checked 上下文中，如果和超出结果类型的范围，则抛出 System.OverflowException。在 unchecked 上下文中，不报告溢出，超出结果类型范围的任何有效高阶位都将被丢弃。

- 浮点加法：

```
float operator +(float x, float y);
double operator +(double x, double y);
```

和根据 IEEE 754 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值；z 是 x + y 的结果。如果 x 和 y 具有相同的量级但符号相反，则 z 是正零。如果 x + y 太大而无法在目标类型中表示，则 z 是与 x + y 同号的无穷大。

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

如果结果值太大而无法用 decimal 格式表示，则抛出 System.OverflowException。结果的小数位数（在进行任何舍入之前）是两个操作数中较大的小数位数。

十进制加法等价于使用 System.Decimal 类型的加法运算符。

枚举加法。每个枚举类型隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：

```
E operator +(U x, U y);
E operator +(U x, E y);
```

在运行时，这些运算符的计算方式与 (E)((U)x + (U)y) 完全相同。

> 比尔·瓦格纳 再说一次，对枚举进行加法可能不会产生有效的枚举成员。所有算术运算符也是如此。

字符串连接：

```
string operator +(string x, string y);
string operator +(string x, object y);
string operator +(object x, string y);
```

这些二元 + 运算符的重载执行字符串连接。如果字符串连接的操作数为 null，则替换为空字符串。否则，任何非字符串参数都会通过调用从 object 类型继承的虚拟 ToString 方法转换为其字符串表示形式。如果 ToString 返回 null，则替换为空字符串。

```
using System;

class Test
{
    static void Main() {
        string s = null;
        Console.WriteLine("s = " + s + "<");    // Displays s = <
        int i = 1;
        Console.WriteLine("i = " + i);            // Displays i = 1
        float f = 1.2300E+15F;
        Console.WriteLine("f = " + f);            // Displays f = 1.23E+15
        decimal d = 2.900m;
        Console.WriteLine("d = " + d);            // Displays d = 2.900
    }
}
```

字符串连接运算符的结果是一个字符串，该字符串由左操作数的字符后跟右操作数的字符组成。字符串连接运算符从不返回 null 值。如果没有足够的内存来分配结果字符串，则可能抛出 System.OutOfMemoryException。




> **JON SKEET** 有点令人惊讶的是 .NET 的 System.String 类型在此情况下没有为 + 提供重载，直到你考虑到编译器可用的优化，因为它可以看到更多代码。像 a+b+c+d 这样的表达式不必产生三个中间字符串：一次调用 String.Concat(a, b, c, d) 可以使连接更高效地执行。

委托组合。每个委托类型都隐式提供以下预定义运算符，其中 D 为委托类型：

```
D operator +(D x, D y);
```

二元 + 运算符在两个操作数均为某个委托类型 D 时执行委托组合。（如果操作数具有不同的委托类型，则会发生绑定时错误。）如果第一个操作数为 null，则操作结果为第二个操作数的值（即使它也是 null）。否则，如果第二个操作数为 null，则操作结果为第一个操作数的值。否则，操作结果是一个新的委托实例，在调用时先调用第一个操作数，然后调用第二个操作数。有关委托组合的示例，请参阅 §7.8.5 和 §15.4。由于 System.Delegate 不是委托类型，因此未为其定义 operator +。

## 7.8.5 减法运算符

形式为 x - y 的操作会应用二元运算符重载解析（§7.3.4）来选择特定的运算符实现。操作数会被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。

下面列出了预定义的减法运算符。所有运算符都从 x 中减去 y。

- 整数减法：
  ```
  int operator -(int x, int y);
  uint operator -(uint x, uint y);
  long operator -(long x, long y);
  ulong operator -(ulong x, ulong y);
  ```

在有检查的上下文中，如果差值超出结果类型的范围，则会抛出 System.OverflowException。在无检查的上下文中，不会报告溢出，超出结果类型范围的任何有效高位都会被丢弃。

- 浮点减法：
  ```
  float operator -(float x, float y);
  double operator -(double x, double y);
  ```

差值是根据 IEEE 754 算术规则计算的。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。在表中，x 和 y 为非零有限值；z 为 x − y 的结果。如果 x 和 y 相等，则 z 为正零。如果 x − y 太大而无法在目标类型中表示，则 z 为与 x − y 相同符号的无穷大。

|   | y | +0 | −0 | +∞ | −∞ | NaN |
|---|---|---|---|---|---|---|
| x | z | x | x | −∞ | +∞ | NaN |
| +0 | −y | +0 | +0 | −∞ | +∞ | NaN |
| −0 | −y | −0 | +0 | −∞ | +∞ | NaN |
| +∞ | +∞ | +∞ | +∞ | NaN | +∞ | NaN |
| −∞ | −∞ | −∞ | −∞ | −∞ | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制减法：
  ```
  decimal operator −(decimal x, decimal y);
  ```

如果结果值太大而无法以十进制格式表示，则会抛出 System.OverflowException。结果的精度（在任何舍入之前）为两个操作数精度中的较大者。

十进制减法等价于使用类型 System.Decimal 的减法运算符。

- 枚举减法。每个枚举类型都隐式提供以下预定义运算符，其中 E 为枚举类型，U 为 E 的基础类型：
  ```
  U operator −(E x, E y);
  ```
该运算符的求值完全等同于 (U)((U)x − (U)y)。换句话说，该运算符计算 x 和 y 的序数值之间的差，结果的类型为枚举的基础类型。

```
E operator −(E x, U y);
```

该运算符的求值完全等同于 (E)((U)x − y)。换句话说，该运算符从枚举的基础类型值中减去一个值，得到枚举的值。

## 7. 表达式

- 委托移除。每个委托类型都隐式提供以下预定义运算符，其中 D 为委托类型：
  ```
  D operator -(D x, D y);
  ```

二元 - 运算符在两个操作数均为某个委托类型 D 时执行委托移除。如果操作数具有不同的委托类型，则会发生绑定时错误。如果第一个操作数为 null，则操作结果为 null。否则，如果第二个操作数为 null，则操作结果为第一个操作数的值。否则，两个操作数都表示包含一个或多个条目的调用列表（§15.1），结果是一个新的调用列表，由第一个操作数的列表组成，其中移除了第二个操作数的条目，前提是第二个操作数的列表是第一个列表的适当连续子列表。（为确定子列表相等性，对应条目按委托相等运算符（§7.10.8）的方式进行比较。）否则，结果为左操作数的值。操作过程中不会更改任一操作数的列表。如果第二个操作数的列表与第一个操作数列表中的多个连续条目子列表匹配，则移除最右边的匹配连续条目子列表。如果移除导致列表为空，则结果为 null。例如：

```
delegate void D(int x);

class C
{
    public static void M1(int i) { /* ... */ }
    public static void M2(int i) { /* ... */ }
}

class Test
{
    static void Main() {
        D cd1 = new D(C.M1);
        D cd2 = new D(C.M2);
        D cd3 = cd1 + cd2 + cd2 + cd1;  // M1 + M2 + M2 + M1
        cd3 -= cd1;                     // => M1 + M2 + M2

        cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
        cd3 -= cd1 + cd2;               // => M2 + M1

        cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
        cd3 -= cd2 + cd2;               // => M1 + M1

        cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
        cd3 -= cd2 + cd1;               // => M1 + M1

        cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
        cd3 -= cd1 + cd1;               // => M1 + M2 + M2 + M1
    }
}
```

## 7.9 移位运算符

`<<` 和 `>>` 运算符用于执行位移操作。

```
shift-expression:
    additive-expression
    shift-expression << additive-expression
    shift-expression >> additive-expression
```

如果 `shift-expression` 的某个操作数在编译时的类型为 `dynamic`，则该表达式是动态绑定的（§7.2.2）。在这种情况下，表达式的编译时类型为 `dynamic`，下面描述的解析将在运行时使用具有编译时类型 `dynamic` 的操作数的运行时类型进行。

对于形式为 `x << count` 或 `x >> count` 的操作，会应用二元运算符重载解析（§7.3.4）来选择特定的运算符实现。操作数会被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。

在声明重载的移位运算符时，第一个操作数的类型必须始终为包含运算符声明的类或结构体，第二个操作数的类型必须始终为 `int`。

下面列出了预定义的移位运算符。

- 左移：
  ```csharp
  int operator <<(int x, int count);
  uint operator <<(uint x, int count);
  long operator <<(long x, int count);
  ulong operator <<(ulong x, int count);
  ```
  `<<` 运算符将 `x` 左移下面描述计算出的位数。
  
  超出 `x` 结果类型范围的高位会被丢弃，剩余位左移，低位的空位设为零。
- 右移：
  ```csharp
  int operator >>(int x, int count);
  uint operator >>(uint x, int count);
  long operator >>(long x, int count);
  ulong operator >>(ulong x, int count);
  ```
  `>>` 运算符将 `x` 右移下面描述计算出的位数。



当 x 的类型为 int 或 long 时，x 的低位会被丢弃，其余位右移；如果 x 为非负，则高位空出的位被设为 0，如果 x 为负，则被设为 1。

当 x 的类型为 uint 或 ulong 时，x 的低位会被丢弃，其余位右移，高位空出的位被设为 0。

对于预定义运算符，要移位的位数按如下方式计算：

- 当 x 的类型为 int 或 uint 时，移位计数由 count 的低五位给出。换言之，移位计数由 `count & 0x1F` 计算。
- 当 x 的类型为 long 或 ulong 时，移位计数由 count 的低六位给出。换言之，移位计数由 `count & 0x3F` 计算。

如果结果移位计数为零，移位运算符直接返回 x 的值。

> **JON SKEET** 对移位计数进行掩码处理可能很高效，但会造成一些非常令人困惑的行为：
>
> ```csharp
> for (int i = 0; i < 40; i++)
> {
>     Console.WriteLine(int.MaxValue >> i);
> }
> ```
>
> 这段代码打印的值在每次迭代时减半——直到它们在达到 0 后循环回 `int.MaxValue`。

移位操作从不会导致溢出，并且在 checked 和 unchecked 上下文中产生相同的结果。

当 >> 运算符的左操作数为有符号整型时，该运算符执行算术右移，其中操作数的最高有效位（符号位）的值会传播到高位空出的位位置。当 >> 运算符的左操作数为无符号整型时，该运算符执行逻辑右移，其中高位空出的位位置始终设为零。要执行与根据操作数类型推断出的操作相反的操作，可以使用显式强制转换。例如，如果 x 是 int 类型变量，则运算 unchecked((int)((uint)x >> y)) 会对 x 执行逻辑右移。

## 7.10 关系运算符和类型测试运算符

==、!=、<、>、<=、>=、is 和 as 运算符称为关系运算符和类型测试运算符。

```
relational-expression:
    shift-expression
    relational-expression < shift-expression
    relational-expression > shift-expression
    relational-expression <= shift-expression
    relational-expression >= shift-expression
    relational-expression is type
    relational-expression as type
```

```
equality-expression:
    relational-expression
    equality-expression == relational-expression
    equality-expression != relational-expression
```

is 运算符在 §7.10.10 中描述，as 运算符在 §7.10.11 中描述。

==、!=、<、>、<= 和 >= 运算符是比较运算符。

如果比较运算符的某个操作数具有编译时类型 dynamic，则该表达式将进行动态绑定（§7.2.2）。在这种情况下，表达式的编译时类型为 dynamic，下面描述的解析将在运行时使用那些具有编译时类型 dynamic 的操作数的运行时类型来进行。

对于形式为 x op y 的运算，其中 op 是比较运算符，会应用重载解析（§7.3.4）来选择特定的运算符实现。操作数会转换为所选运算符的参数类型，而结果的类型是该运算符的返回类型。

预定义的比较运算符将在以下各节中描述。所有预定义的比较运算符都返回 bool 类型的结果，如下表所述。

| 运算 | 结果 |
|---|---|
| x == y | 如果 x 等于 y，则为 true；否则为 false |
| x != y | 如果 x 不等于 y，则为 true；否则为 false |
| x < y | 如果 x 小于 y，则为 true；否则为 false |
| x > y | 如果 x 大于 y，则为 true；否则为 false |
| x <= y | 如果 x 小于或等于 y，则为 true；否则为 false |
| x >= y | 如果 x 大于或等于 y，则为 true；否则为 false |

### 7.10.1 整数比较运算符

预定义的整数比较运算符如下所示：

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

这些运算符分别比较两个整数操作数的数值，并返回一个 bool 值，指示特定关系为 true 还是 false。

### 7.10.2 浮点比较运算符

预定义的浮点比较运算符如下所示：

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

这些运算符按照 IEEE 754 标准的规则比较操作数：

- 如果任一操作数为 NaN，则除 != 外的所有运算符的结果均为 false，而 != 的结果为 true。对于任意两个操作数，x != y 始终产生与 !(x == y) 相同的结果。但是，当一个或两个操作数为 NaN 时，<、<= 和 >= 运算符产生的结果并不等同于相反运算符的逻辑取反结果。例如，如果 x 和 y 中任一为 NaN，则 x < y 为 false，但 !(x >= y) 为 true。
- 当两个操作数都不是 NaN 时，这些运算符按照以下顺序比较两个浮点操作数的值

  ```
  -∞ < -max < ... < -min < -0.0 == +0.0 < +min < ... < +max < +∞
  ```

  其中 min 和 max 分别是给定浮点格式所能表示的最小和最大正有限值。这种顺序的显著影响如下：

  - 负零和正零被视为相等。
  - 负无穷被视为小于所有其他值，但等于另一个负无穷。
  - 正无穷被视为大于所有其他值，但等于另一个正无穷。

> PETER SESTOFT 同样成立的是，正零和负零根据 Object.Equals 是相等的，因此由 Object.GetHashCode 计算出的它们的哈希码也应相等。不幸的是，在当前所有实现中并非如此。

> JOSEPH ALBAHARI 两个 NaN 值虽然根据 == 运算符不相等，但根据 Equals 方法却相等：
>
> ```
> double x = double.NaN;
> Console.WriteLine(x == x);    // False
> Console.WriteLine(x != x);    // True
> Console.WriteLine(x.Equals(x)); // True
> ```
>
> 一般来说，类型的 Equals 方法遵循这样的原则：对象必须等于自身。如果没有这一假设，列表和字典就无法运作，因为将没有办法测试元素成员资格。然而，== 和 != 运算符不必遵循这一原则。

> PETER SESTOFT 即使具有不同负载的 NaN（参见 §7.8.1 的注释），根据 Object.Equals 也是相等的。

### 7.10.3 decimal 比较运算符

预定义的 decimal 比较运算符如下所示：

```csharp
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

这些运算符分别比较两个 decimal 操作数的数值，并返回一个 bool 值，指示特定关系为 true 还是 false。每个 decimal 比较都等价于使用 System.Decimal 类型对应的关系运算符或相等运算符。

### 7.10.4 布尔相等运算符

预定义的布尔相等运算符如下所示：

```csharp
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

== 的结果为 true 的条件是 x 和 y 均为 true，或 x 和 y 均为 false；否则结果为 false。

!= 的结果为 false 的条件是 x 和 y 均为 true，或 x 和 y 均为 false；否则结果为 true。当操作数为 bool 类型时，!= 运算符产生与 ^ 运算符相同的结果。

### 7.10.5 枚举比较运算符

每个枚举类型都隐式提供以下预定义比较运算符：

```csharp
bool operator ==(E x, E y);
bool operator !=(E x, E y);
bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

计算 x op y 的结果（其中 x 和 y 是基础类型为 U 的枚举类型 E 的表达式，op 是其中一个比较运算符）与计算 ((U)x) op ((U)y) 的结果完全相同。换言之，枚举类型比较运算符只是比较两个操作数的基础整数值。



## 7.10.6 引用类型相等运算符

预定义的引用类型相等运算符如下所示：

```csharp
bool operator ==(object x, object y);
bool operator !=(object x, object y);
```

这些运算符返回比较两个引用是否相等或不相等的比较结果。

由于预定义的引用类型相等运算符接受 object 类型的操作数，因此它们适用于所有未声明适用的 operator == 和 operator != 成员的类型。反过来，任何适用的用户定义相等运算符都会有效地隐藏预定义的引用类型相等运算符。

预定义的引用类型相等运算符要求满足以下条件之一：

- 两个操作数都是已知为*引用类型*的类型的值或字面量 null。此外，任一操作数的类型到另一操作数的类型存在显式引用转换（§6.2.4）。
- 一个操作数是类型 T 的值，其中 T 是*类型参数*，另一个操作数是字面量 null。此外，T 不具有值类型约束。

除非这些条件之一成立，否则会发生绑定时间错误。这些规则的显著含义如下：

- 使用预定义的引用类型相等运算符比较在绑定时间已知不同的两个引用，属于绑定时间错误。例如，如果操作数的绑定时间类型是两个类类型 A 和 B，并且 A 和 B 都不是从对方派生的，那么这两个操作数不可能引用同一对象。因此，该操作被视为绑定时间错误。
- 预定义的引用类型相等运算符不允许比较值类型操作数。因此，除非结构类型声明了自己的相等运算符，否则无法比较该结构类型的值。
- 预定义的引用类型相等运算符绝不会导致其操作数发生装箱操作。执行此类装箱操作毫无意义，因为对新分配的装箱实例的引用必然不同于所有其他引用。
- 如果将类型参数类型 T 的操作数与 null 进行比较，并且 T 的运行时类型是值类型，则比较结果为 false。

以下示例检查未约束类型参数类型的参数是否为 null。

```csharp
class C<T>
{
    void F(T x) {
        if (x == null) throw new ArgumentNullException();
        ...
    }
}
```

即使 T 可能表示值类型，也允许使用 x == null 构造；并且当 T 是值类型时，结果直接定义为 false。

> **比尔·瓦格纳** 如果使用 default(int?) 调用 C.F()，它将抛出异常。  
> 如果 HasValue 为 false，则可空类型被视为等于 null。

对于 x == y 或 x != y 形式的操作，如果存在任何适用的 operator == 或 operator !=，则运算符重载决议（§7.3.4）规则将选择该运算符，而不是预定义的引用类型相等运算符。然而，通过将一个或两个操作数显式转换为 object 类型，始终可以选择预定义的引用类型相等运算符。示例

```csharp
using System;
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

产生输出

```text
True
False
False
False
```

变量 s 和 t 引用两个不同的字符串实例，这两个实例包含相同的字符。第一个比较输出 True，因为当两个操作数都是 string 类型时，会选择预定义的字符串相等运算符（§7.10.7）。其余比较都输出 False，因为当一个或两个操作数是 object 类型时，会选择预定义的引用类型相等运算符。

请注意，上述技术对值类型没有意义。示例

```csharp
class Test
{
    static void Main()
    {
        int i = 123;
        int j = 123;
        System.Console.WriteLine((object)i == (object)j);
    }
}
```

输出 False，因为这些强制转换创建了对两个单独的装箱 int 值实例的引用。

## 7.10.7 字符串相等运算符

预定义的字符串相等运算符如下所示：

```csharp
bool operator ==(string x, string y);
bool operator !=(string x, string y);
```

当以下条件之一成立时，两个字符串值被视为相等：

- 两个值均为 null。
- 两个值都是对字符串实例的非 null 引用，且这些实例具有相同长度，并且每个字符位置上的字符都相同。

字符串相等运算符比较字符串值，而不是字符串引用。当两个单独的字符串实例包含完全相同的字符序列时，字符串的值相等，但引用不同。如 §7.10.6 所述，可以使用引用类型相等运算符来比较字符串引用而不是字符串值。

## 7.10.8 委托相等运算符

每个委托类型都隐式提供以下预定义比较运算符：

```csharp
bool operator ==(System.Delegate x, System.Delegate y);
bool operator !=(System.Delegate x, System.Delegate y);
```

在以下情况下，两个委托实例被视为相等：

- 如果任一委托实例为 null，则当且仅当两者都为 null 时它们相等。
- 如果委托具有不同的运行时类型，则它们永远不相等。
- 如果两个委托实例都有调用列表（§15.1），则当且仅当它们的调用列表长度相同，并且一个委托实例调用列表中的每个条目按顺序与另一个委托实例调用列表中对应条目相等（按下文定义）时，这两个实例相等。

以下规则决定调用列表条目的相等性：

- 如果两个调用列表条目都引用同一个静态方法，则这些条目相等。
- 如果两个调用列表条目都引用同一目标对象上的同一个非静态方法（由引用相等运算符定义），则这些条目相等。
- 由语义相同的匿名函数表达式（具有相同的一组捕获的外部变量实例，可能为空）求值产生的调用列表条目，允许（但不要求）相等。

## 7.10.9 相等运算符与 null

== 和 != 运算符允许一个操作数是可空类型的值，另一个操作数是 null 字面量，即使该操作不存在预定义或用户定义的运算符（非提升形式或提升形式）。

对于以下形式之一的操作

```text
x == null    null == x    x != null    null != x
```

其中 x 是可空类型的表达式，如果运算符重载决议（§7.2.4）未能找到适用的运算符，则改为根据 x 的 HasValue 属性计算结果。具体而言，前两种形式转换为 !x.HasValue，后两种形式转换为 x.HasValue。

## 7.10.10 is 运算符

is 运算符用于动态检查对象的运行时类型是否与给定类型兼容。操作 E is T 的结果（其中 E 是表达式，T 是类型）是一个布尔值，指示 E 是否可以通过引用转换、装箱转换或拆箱转换成功转换为类型 T。在已为所有类型参数替换类型实参后，按如下方式计算该操作：

- 如果 E 是匿名函数，则发生编译时错误。
- 如果 E 是方法组或 null 字面量，或者如果 E 的类型是引用类型或可空类型且 E 的值为 null，则结果为 false。
- 否则，按如下方式令 D 表示 E 的动态类型：
  - 如果 E 的类型是引用类型，则 D 是 E 所引用实例的运行时类型。
  - 如果 E 的类型是可空类型，则 D 是该可空类型的基础类型。
  - 如果 E 的类型是不可空值类型，则 D 是 E 的类型。
- 操作的结果取决于 D 和 T，如下所示：
  - 如果 T 是引用类型，则当 D 和 T 是同一类型，或 D 是引用类型且存在从 D 到 T 的隐式引用转换，或 D 是值类型且存在从 D 到 T 的装箱转换时，结果为 true。
  - 如果 T 是可空类型，则当 D 是 T 的基础类型时，结果为 true。
  - 如果 T 是不可空值类型，则当 D 和 T 是同一类型时，结果为 true。
  - 否则，结果为 false。

请注意，is 运算符不考虑用户定义转换。

## 7.10.11 as 运算符

as 运算符用于将值显式转换为给定的引用类型或可空类型。与强制转换表达式（§7.6）不同，as 运算符从不引发异常。相反，如果无法进行指示的转换，则结果值为 null。

在 E as T 形式的操作中，E 必须是表达式，T 必须是引用类型、已知为引用类型的类型参数或可空类型。此外，以下条件中至少有一个必须成立；否则，会发生编译时错误：

- 存在从 E 到 T 的标识转换（§6.1.1）、隐式可空转换（§6.1.4）、隐式引用转换（§6.1.6）、装箱转换（§6.1.7）、显式可空转换（§6.2.3）、显式引用转换（§6.2.4）或拆箱转换（§6.2.5）。
- E 或 T 的类型是开放类型。
- E 是 null 字面量。

如果 E 的编译时类型不是动态类型，则操作 E as T 产生与以下代码相同的结果

```csharp
E is T ? (T)(E) : (T)null
```




## 7. 表达式

除 E 只计算一次外。编译器可以将 E as T 优化为最多执行一次动态类型检查，而不是上述展开所隐含的两次动态类型检查。

如果 E 的编译时类型为 dynamic，则与强制转换运算符不同，as 运算符不会被动态绑定（§7.2.2）。因此，这种情况下的展开为

```
E is T ? (T)object(E) : (T)null
```

请注意，有些转换（如用户定义的转换）无法使用 as 运算符完成，此时应改用强制转换表达式。

在下面的示例中

```
class X
{
    public string F(object o) {
        return o as string;
        // Okay: string is a reference type
    }

    public T G<T>(object o) where T: Attribute {
        return o as T;
        // Okay: T has a class constraint
    }

    public U H<U>(object o) {
        return o as U;
        // Error: U is unconstrained
    }
}
```

G 的类型参数 T 已知是引用类型，因为它具有 class 约束。但是，H 的类型参数 U 并非已知；因此，在 H 中使用 as 运算符是不允许的。

> **CHRIS SELLS** 如果你正在使用 FxCop（而且你应该使用！）开箱即用，当你这样做时它并不喜欢：
>
> ```csharp
> if( x is Foo ) { ((Foo)x).DoFoo(); }
> ```
>
> 相反，它更倾向于你这样写：
>
> ```csharp
> Foo foo = x as Foo;
> if( foo != null ) { foo.DoFoo(); }
> ```
>
> 为什么？因为 is、as 和强制转换本质上都是相同的底层 .NET 操作，所以最好是只执行一次操作，检查结果是否为 null，然后对非 null 结果进行操作，而不是执行两次操作。

> **JOSEPH ALBAHARI** 尽管克里斯在技术上是对的，但这是一个微优化。引用转换的成本很低。

> **CHRIS SELLS** 尽管约瑟夫完全正确，但我更多是希望能摆脱 FxCop 的纠缠，而不是为了性能优化。

> **JOSEPH ALBAHARI** 有些人出于风格偏好，更喜欢使用 as 运算符而不是强制转换运算符。as 运算符的一个优点是，使用它可以清楚地表明该转换不是数值转换或用户定义的转换。然而，普遍偏爱将 as 运算符用于引用转换的问题在于，转换失败时计算结果为 null 并不总是可取的。为了说明这一点，请考虑以下代码的结果，如果 s 引用的对象不是字符串：
>
> ```csharp
> int length1 = ((string) s).Length;  // Throws InvalidCastException
> int length2 = (s as string).Length;  // Throws NullReferenceException
> ```
>
> 第一行会抛出包含有用信息的 InvalidCastException，而第二行会抛出（含义模糊的）NullReferenceException。（s 是 null 还是类型错误？）

> **JON SKEET** as 运算符几乎总是随后会进行空值测试——以至于它几乎值得拥有自己的语句类型：
>
> ```csharp
> // Would be equivalent to the code in Chris's annotation
> asif (Foo foo = x)
> {
>     foo.DoFoo();
> }
> ```
>
> 引入一种全新的语句类型可能有些过头——但当前这种模式的笨拙确实令人恼火。

## 7.11 逻辑运算符

&、^ 和 | 运算符称为逻辑运算符。

and-expression:
    equality-expression
    and-expression & equality-expression

```
exclusive-or-expression:
    and-expression
    exclusive-or-expression ^ and-expression

inclusive-or-expression:
    exclusive-or-expression
    inclusive-or-expression | exclusive-or-expression
```

如果逻辑运算符的某个操作数的编译时类型为 dynamic，则该表达式会被动态绑定（§7.2.2）。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时使用那些编译时类型为 dynamic 的操作数的运行时类型进行。

对于形式为 x op y 的操作，其中 op 是逻辑运算符之一，将应用重载决策（§7.3.4）来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型即为该运算符的返回类型。

预定义逻辑运算符将在以下各节中描述。

### 7.11.1 整数逻辑运算符

预定义的整数逻辑运算符如下所列：

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

& 运算符计算两个操作数的按位逻辑 AND，| 运算符计算两个操作数的按位逻辑 OR，^ 运算符计算两个操作数的按位逻辑异或。这些运算不会发生溢出。

### 7.11.2 枚举逻辑运算符

每个枚举类型 E 都隐式提供以下预定义逻辑运算符：

```
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```

计算 `x op y` 的结果，其中 x 和 y 是底层类型为 U 的枚举类型 E 的表达式，且 `op` 是逻辑运算符之一，与计算 `(E)((U)x op (U)y)` 的结果完全相同。换句话说，枚举类型逻辑运算符只是对两个操作数的底层类型执行逻辑运算。

### 7.11.3 布尔逻辑运算符

预定义的布尔逻辑运算符如下所列：

```csharp
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```

如果 x 和 y 都为 true，则 `x & y` 的结果为 true；否则结果为 false。

如果 x 或 y 中有一个为 true，则 `x | y` 的结果为 true；否则结果为 false。

如果 x 为 true 且 y 为 false，或者 x 为 false 且 y 为 true，则 `x ^ y` 的结果为 true；否则结果为 false。当操作数为 `bool` 类型时，`^` 运算符计算出的结果与 `!=` 运算符相同。

### 7.11.4 可空布尔逻辑运算符

可空布尔类型 `bool?` 可以表示三个值：true、false 和 null。它在概念上类似于 SQL 中用于布尔表达式的三值类型。为了确保 `&` 和 `|` 运算符为 `bool?` 操作数产生的结果与 SQL 的三值逻辑一致，提供了以下预定义运算符：

```csharp
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

下表列出了这些运算符对 true、false 和 null 所有值组合产生的结果。

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

## 7.12 条件逻辑运算符

&& 和 || 运算符称为条件逻辑运算符。它们也被称为“短路”逻辑运算符。

```
conditional-and-expression:
    inclusive-or-expression
    conditional-and-expression && inclusive-or-expression

conditional-or-expression:
    conditional-and-expression
    conditional-or-expression || conditional-and-expression
```

&& 和 || 运算符是 & 和 | 运算符的条件版本：

- 操作 `x && y` 对应于操作 `x & y`，不同之处在于仅当 x 不为 false 时才计算 y。
- 操作 `x || y` 对应于操作 `x | y`，不同之处在于仅当 x 不为 true 时才计算 y。

如果条件逻辑运算符的某个操作数的编译时类型为 dynamic，则该表达式会被动态绑定（§7.2.2）。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时使用那些编译时类型为 dynamic 的操作数的运行时类型进行。

形式为 x && y 或 x || y 的操作通过应用重载决策（§7.3.4）来处理，如同该操作写为 x & y 或 x | y 一样。然后，

- 如果重载决策无法找到唯一的最佳运算符，或者重载决策选择了预定义整数逻辑运算符之一，则会发生绑定期错误。
- 否则，如果所选运算符是预定义布尔逻辑运算符（§7.11.3）或可空布尔逻辑运算符（§7.11.4）之一，则按 §7.12.1 中描述的方式处理该操作。
- 否则，所选运算符是用户定义的运算符，则按 §7.12.2 中描述的方式处理该操作。

无法直接重载条件逻辑运算符。但是，由于条件逻辑运算符是根据常规逻辑运算符进行求值的，因此在某些限制下，常规逻辑运算符的重载也被视为条件逻辑运算符的重载。这种情况将在 §7.12.2 中进一步描述。




### 7.12.1 布尔条件逻辑运算符

当 `&&` 或 `||` 的操作数类型为 bool，或者操作数所属类型未定义适用的运算符 `&` 或运算符 `|`，但定义了到 bool 的隐式转换时，该操作按如下方式处理：

- 运算 `x && y` 按 `x ? y : false` 求值。换言之，先对 x 求值并转换为 bool 类型。然后，如果 x 为 `true`，则对 y 求值并转换为 bool 类型，该值成为运算结果。否则，运算结果为 `false`。
- 运算 `x || y` 按 `x ? true : y` 求值。换言之，先对 x 求值并转换为 bool 类型。然后，如果 x 为 `true`，运算结果为 `true`。否则，对 y 求值并转换为 bool 类型，该值成为运算结果。

### 7.12.2 用户定义的条件逻辑运算符

当 `&&` 或 `||` 的操作数所属类型声明了适用的用户定义运算符 `&` 或运算符 `|` 时，以下两项必须都为真，其中 T 是所选运算符声明所在的类型：

- 所选运算符的返回类型及其每个参数的类型都必须为 T。换言之，该运算符必须计算两个 T 类型操作数的逻辑 AND 或逻辑 OR，并且必须返回 T 类型的结果。
- T 必须包含运算符 `true` 和运算符 `false` 的声明。

如果这两项要求中的任一项不满足，则发生绑定时间错误。否则，通过将用户定义运算符 `true` 或运算符 `false` 与所选用户定义运算符组合，来对 `&&` 或 `||` 运算求值：

- 运算 `x && y` 按 `T.false(x) ? x : T.&(x, y)` 求值，其中 `T.false(x)` 是对 T 中声明的运算符 `false` 的调用，`T.&(x, y)` 是对所选运算符 `&` 的调用。换言之，先对 x 求值，并对结果调用运算符 false，以确定 x 是否肯定为 false。然后，如果 x 肯定为 false，则运算结果为先前为 x 计算的值。否则，对 y 求值，并对先前为 x 计算的值和 y 计算的值调用所选运算符 `&`，以生成运算结果。
- 运算 `x || y` 按 `T.true(x) ? x : T.|(x, y)` 求值，其中 `T.true(x)` 是对 T 中声明的运算符 `true` 的调用，`T.|(x, y)` 是对所选运算符 `|` 的调用。换言之，先对 x 求值，并对结果调用运算符 true，以确定 x 是否肯定为 true。然后，如果 x 肯定为 true，则运算结果为先前为 x 计算的值。否则，对 y 求值，并对先前为 x 计算的值和 y 计算的值调用所选运算符 `|`，以生成运算结果。

在这两种运算中，由 x 给出的表达式只求值一次，而由 y 给出的表达式要么不求值，要么恰好求值一次。

有关实现运算符 true 和运算符 false 的类型的示例，请参见 §11.4.2。

## 7.13 null 合并运算符

?? 运算符称为 null 合并运算符。

```
null-coalescing-expression:
    conditional-or-expression
    conditional-or-expression ?? null-coalescing-expression
```

形式为 a ?? b 的 null 合并表达式要求 a 为可空类型或引用类型。如果 a 为非 null，则 a ?? b 的结果为 a；否则结果为 b。仅当 a 为 null 时，该运算才会对 b 求值。

null 合并运算符是右结合的，这意味着运算从右到左分组。例如，形式为 a ?? b ?? c 的表达式按 a ?? (b ?? c) 求值。一般来说，形式为 E1 ?? E2 ... ?? En 的表达式返回第一个非 null 的操作数；如果所有操作数都为 null，则返回 null。

表达式 a ?? b 的类型取决于操作数上可用的隐式转换。按优先顺序，a ?? b 的类型为 Aν、A 或 B，其中 A 是 a 的类型（前提是 a 有类型），B 是 b 的类型（前提是 b 有类型），并且如果 A 是可空类型，则 Aν 是 A 的底层类型，否则 Aν 就是 A。具体而言，a ?? b 按如下方式处理：

- 如果 A 存在且不是可空类型或引用类型，则发生编译时错误。
- 如果 b 是动态表达式，则结果类型为 dynamic。在运行时，先对 a 求值。如果 a 不为 null，则将 a 转换为 dynamic 类型，该值成为结果。否则，对 b 求值，求值结果成为结果。
- 否则，如果 A 存在且为可空类型，并且存在从 b 到 Aν 的隐式转换，则结果类型为 Aν。在运行时，先对 a 求值。如果 a 不为 null，则将 a 解包为 Aν 类型，该值成为结果。否则，对 b 求值并转换为 Aν 类型，该值成为结果。
- 否则，如果 A 存在，并且存在从 b 到 A 的隐式转换，则结果类型为 A。在运行时，先对 a 求值。如果 a 不为 null，则 a 成为结果。否则，对 b 求值并转换为 A 类型，该值成为结果。
- 否则，如果 b 具有类型 B，并且存在从 a 到 B 的隐式转换，则结果类型为 B。在运行时，先对 a 求值。如果 a 不为 null，则将 a 解包为 Aν 类型（如果 A 存在且可为空）并转换为 B 类型，该值成为结果。否则，对 b 求值，该值成为结果。
- 否则，a 和 b 不兼容，并发生编译时错误。

> ERIC LIPPERT 这些转换规则使 null 合并运算符到表达式树的转换变得相当复杂。在某些情况下，编译器必须专门发出一个额外的表达式树 lambda 来处理转换逻辑。

> CHRIS SELLS ?? 运算符可用于为引用类型或可空值类型设置默认值。例如：
> 
> Foo f1 = ...;
> Foo f2 = f1 ?? new Foo(...);
> int? i1 = ...;
> int i2 = i1 ?? 452;

## 7.14 条件运算符

?: 运算符称为条件运算符，有时也称为三元运算符。

```
conditional-expression:
  null-coalescing-expression
  null-coalescing-expression ? expression : expression
```

形式为 b ? x : y 的条件表达式首先对条件 b 求值。然后，如果 b 为 true，则对 x 求值，该值成为运算结果。否则，对 y 求值，该值成为运算结果。条件表达式绝不会同时求值 x 和 y。

条件运算符是右结合的，这意味着运算从右到左分组。例如，形式为 a ? b : c ? d : e 的表达式按 a ? b : (c ? d : e) 求值。

> **JON SKEET** 我偶尔会发现自己使用多个条件运算符。乍看之下有些奇怪，但如果布局得当，可读性会很好。在某些方面，这是 C# 最接近 F# 等语言模式匹配的方式。
> 
> ```
> return firstCondition ? firstValue :
>     secondCondition ? secondValue :
>     thirdCondition ? thirdValue :
>     fallbackValue;
> ```

?: 运算符的第一个操作数必须是可隐式转换为 bool 的表达式，或者是实现了运算符 true 的类型的表达式。如果这两项要求都不满足，则发生编译时错误。

> **PETER SESTOFT** 特别是，由于不存在从可空类型 bool? 到 bool 的隐式转换，条件运算符的第一个操作数不能具有 bool? 类型。

?: 运算符的第二个和第三个操作数 x 和 y 控制条件表达式的类型。

- 如果 x 具有类型 X，y 具有类型 Y，则
  - 如果存在从 X 到 Y 的隐式转换（§6.1），但不存在从 Y 到 X 的隐式转换，则 Y 是条件表达式的类型。
  - 如果存在从 Y 到 X 的隐式转换（§6.1），但不存在从 X 到 Y 的隐式转换，则 X 是条件表达式的类型。
  - 否则，无法确定表达式类型，并发生编译时错误。
- 如果 x 和 y 中只有一个具有类型，并且 x 和 y 都能隐式转换为该类型，则该类型就是条件表达式的类型。
- 否则，无法确定表达式类型，并发生编译时错误。

> **ERIC LIPPERT** Microsoft C# 编译器实际上实现的算法略有不同：它检查的是从表达式到类型的转换，而不是从类型到类型的转换。在大多数情况下，这种差异无关紧要，而现在更改它会破坏现有代码。




> **彼得·塞斯托夫特**  尽管埃里克的批注中已经指出了这一点，但 Microsoft 的 C# 4.0 编译器与早期版本之间仍存在一处小的不兼容：该编译器无法推断下面右侧条件表达式的类型，并抱怨“在‘<null>’和‘<null>’之间不存在隐式转换”。
>
> C# 2.0 编译器会接受此表达式。C# 4.0 编译器的消息暗示编译器内部可能存在一种“null 类型”，或者至少编写该错误消息的人头脑中存在这种概念。鉴于这段极其刻意构造的代码，这种不兼容性不值得让人睡不着觉。
>
> ```csharp
> int? x = args.Length > 0 ? null : null;
> ```
>
> **弗拉基米尔·列舍特尼科夫**  早期版本的 C# 规范中存在“null 类型”的概念，但它在 C# 3.0 中被删除了，这导致在边缘情形中行为略有不同。目前，null 字面量是一个没有类型的表达式。

运行时对形如 `b ? x : y` 的条件表达式的处理包含以下步骤：

- 首先，对 `b` 求值，并确定 `b` 的 bool 值：
  - 如果存在从 `b` 的类型到 `bool` 的隐式转换，则执行该隐式转换以生成一个 bool 值。
  - 否则，调用由 `b` 的类型定义的 `true` 运算符以生成一个 bool 值。
- 如果上述步骤生成的 bool 值为 true，则对 `x` 求值并转换为条件表达式的类型，该值成为条件表达式的结果。
- 否则，对 `y` 求值并转换为条件表达式的类型，该值成为条件表达式的结果。

> **比尔·瓦格纳**  在我看来，空合并运算符和条件运算符都像浓烈的香料：少量使用时，它们是很棒的增强剂。克里斯指出了一些用法，其中空合并运算符比等价的 if-then-else 语句生成更清晰的代码。就像浓烈的香料一样，过度使用会令人痛苦，并毁掉原本可能非常令人愉悦的东西。

![](img/04b421b044b1254de966ab5335775a89_380_0.png)

## 7.15 匿名函数表达式

*匿名函数* 是表示“内联”方法定义的表达式。匿名函数本身没有值或类型，但可以转换为兼容的委托或表达式树类型。匿名函数转换的求值取决于转换的目标类型：如果它是委托类型，则该转换求值为一个委托值，该委托值引用匿名函数所定义的方法。如果它是表达式树类型，则该转换求值为一个表达式树，该表达式树以对象结构表示该方法的结构。

由于历史原因，匿名函数有两种语法形式，即 *lambda 表达式* 和 *匿名方法表达式*。在几乎所有用途中，*lambda 表达式* 都比 *匿名方法表达式* 更简洁、更具表现力；后者保留在语言中是为了确保向后兼容。

```text
lambda-expression:
    anonymous-function-signature  =>  anonymous-function-body

anonymous-method-expression:
    delegate  explicit-anonymous-function-signature_opt  block

anonymous-function-signature:
    explicit-anonymous-function-signature
    implicit-anonymous-function-signature

explicit-anonymous-function-signature:
    ( explicit-anonymous-function-parameter-list_opt )

explicit-anonymous-function-parameter-list:
    explicit-anonymous-function-parameter
    explicit-anonymous-function-parameter-list  ,  explicit-anonymous-function-parameter

explicit-anonymous-function-parameter:
    anonymous-function-parameter-modifier_opt  type  identifier

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
```

`=>` 运算符与赋值运算符（`=`）具有相同的优先级，并且是右结合的。

*lambda 表达式* 形式的匿名函数的参数可以显式或隐式类型化。在显式类型化的参数列表中，每个参数的类型都被明确说明。在隐式类型化的参数列表中，参数的类型根据匿名函数出现的上下文推断——具体而言，当匿名函数转换为兼容的委托类型或表达式树类型时，该类型提供参数类型（§6.5）。

> **比尔·瓦格纳**  一般而言，如果依赖隐式类型化，你的匿名函数将更具适应性。

对于具有单个隐式类型化参数的匿名函数，参数列表中可以省略括号。换句话说，形式为

```csharp
( param ) => expr
```

的匿名函数可以缩写为

```csharp
param => expr
```

*匿名方法表达式* 形式的匿名函数的参数列表是可选的。如果提供，参数必须显式类型化。如果不提供，则该匿名函数可转换为具有任意不包含 `out` 参数的参数列表的委托。

下面是一些匿名函数的示例：

```csharp
x => x + 1                          // Implicitly typed, expression body
x => { return x + 1; }              // Implicitly typed, statement body
(int x) => x + 1                    // Explicitly typed, expression body
(int x) => { return x + 1; }        // Explicitly typed, statement body
(x, y) => x * y                     // Multiple parameters
() => Console.WriteLine()           // No parameters
delegate (int x) { return x + 1; }  // Anonymous method expression
delegate { return 1 + 1; }          // Parameter list omitted
```

*lambda 表达式* 和 *匿名方法表达式* 的行为相同，但以下几点除外：

- *匿名方法表达式* 允许完全省略参数列表，从而可转换为具有任意值参数列表的委托类型。
- *lambda 表达式* 允许省略并推断参数类型，而 *匿名方法表达式* 要求显式声明参数类型。
- *lambda 表达式* 的主体可以是表达式或语句块，而 *匿名方法表达式* 的主体必须是语句块。
- 由于只有 *lambda 表达式* 可以具有表达式主体，因此没有任何 *匿名方法表达式* 能成功转换为表达式树类型（§4.6）。

> **比尔·瓦格纳**  这一点对于构建依赖表达式树的查询很重要，例如 Linq2SQL 和 Entity Framework 中的查询。

### 7.15.1 匿名函数签名

匿名函数可选的 *匿名函数签名* 定义该匿名函数的形式参数的名称，并可选地定义其类型。匿名函数参数的作用域是 *匿名函数体*（§3.7）。*匿名函数体* 与参数列表（如果提供）一起构成一个声明空间（§3.3）。因此，如果匿名函数的某个参数名称与某个局部变量、局部常量或参数名称匹配，且该局部变量、局部常量或参数的作用域包含该 *匿名方法表达式* 或 *lambda 表达式*，则构成编译时错误。

如果匿名函数具有 *显式匿名函数签名*，则兼容的委托类型和表达式树类型的集合仅限于那些具有相同参数类型和修饰符且顺序相同的类型。与方法组转换（§6.6）不同，不支持匿名函数参数类型的逆变。如果匿名函数没有 *匿名函数签名*，则兼容的委托类型和表达式树类型的集合仅限于那些没有 out 参数的类型。

注意，*匿名函数签名* 不能包含特性或参数数组。不过，*匿名函数签名* 仍可能与参数列表包含参数数组的委托类型兼容。

另请注意，即使兼容，转换为表达式树类型仍可能在编译时失败（§4.6）。




> **ERIC LIPPERT** 这是一个微妙的点。如果你有两个重载——比如，void M(Expression<Func<Giraffe>> f) 和 void M(Func<Animal> f)——并且调用 M(() => myGiraffes[++i])，那么表达式树重载会被选为更好的重载。在这种情况下，会发生编译时错误，因为递增运算符在表达式树内部是非法的。

## 7.15.2 匿名函数体

匿名函数的体（*表达式*或*块*）遵循以下规则：

- 如果匿名函数包含签名，则签名中指定的参数可在体中使用。如果匿名函数没有签名，则可以将其转换为带参数的委托类型或表达式类型（§6.5），但不能在体中访问这些参数。
- 除了最接近的外围匿名函数的签名中指定的 ref 或 out 参数（如果有）之外，体访问 ref 或 out 参数会导致编译时错误。
- 当 this 的类型是结构类型时，体访问 this 会导致编译时错误。无论访问是显式的（如 this.x 中）还是隐式的（如 x 中，其中 x 是结构的实例成员），都是如此。此规则只是禁止此类访问，不影响成员查找是否解析为结构的成员。
- 体可以访问匿名函数的外部变量（§7.15.5）。对外部变量的访问将引用在求值 lambda 表达式或匿名方法表达式时处于活动状态的变量实例（§7.15.6）。
- 如果体包含目标在体之外或包含的匿名函数体之内的 goto 语句、break 语句或 continue 语句，则会导致编译时错误。
- 体中的 return 语句从最近的外围匿名函数的调用返回控制权，而不是从外围函数成员返回。return 语句中指定的表达式必须可隐式转换为最近的 lambda 表达式或匿名方法表达式所转换到的委托类型或表达式树类型的返回类型（§6.5）。

明确未规定是否存在除通过求值和调用 lambda 表达式或匿名方法表达式之外执行匿名函数块的任何方式。特别是，编译器可以选择通过合成一个或多个命名方法或类型来实现匿名函数。任何此类合成元素的名称必须采用保留供编译器使用的形式。

## 7.15.3 重载决策

参数列表中的匿名函数参与类型推断和重载决策。确切规则请参阅 §7.4.2.3。

以下示例说明匿名函数对重载决策的影响。

```
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

ItemList<T> 类有两个 Sum 方法。每个方法都接受一个 selector 参数，该参数从列表项中提取用于求和的值。提取的值可以是 int 或 double，得到的和同样可以是 int 或 double。

例如，可以使用 Sum 方法从订单中的明细行列表计算总和。

```
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
    ...
}
```

在 orderDetails.Sum 的第一次调用中，两个 Sum 方法都适用，因为匿名函数 d => d.UnitCount 与 Func<Detail,int> 和 Func<Detail,double> 都兼容。然而，重载决策选择第一个 Sum 方法，因为到 Func<Detail,int> 的转换优于到 Func<Detail,double> 的转换。

在 orderDetails.Sum 的第二次调用中，只有第二个 Sum 方法适用，因为匿名函数 d => d.UnitPrice * d.UnitCount 生成 double 类型的值。因此，重载决策为该调用选择第二个 Sum 方法。

## 7.15.4 匿名函数与动态绑定

匿名函数不能作为动态绑定操作的接收者、参数或操作数。

## 7.15.5 外部变量

任何作用域包含该 lambda 表达式或匿名方法表达式的局部变量、值参数或参数数组，称为该匿名函数的外部变量。在类的实例函数成员中，this 值被视为值参数，并且是该函数成员内包含的任何匿名函数的外部变量。

> BILL WAGNER  这是 C# 中闭包实现方式的形式定义。这是一个很好的补充。

### 7.15.5.1 捕获的外部变量

当匿名函数引用某个外部变量时，称该外部变量已被该匿名函数捕获。通常，局部变量的生存期限于执行与其关联的块或语句（§5.1.7）。然而，捕获的外部变量的生存期至少延长到从该匿名函数创建的委托或表达式树有资格进行垃圾回收为止。

> BILL WAGNER  在下一个示例中，请注意 x 的生存期比你预期的更长，因为它被匿名方法结果捕获。如果 x 是昂贵的资源，则应通过限制匿名方法的生存期来避免这种行为。

在示例中

```
using System;
delegate int D();
class Test
{
    static D F() {
        int x = 0;
        D result = () => ++x;
        return result;
    }
}
```
```
static void Main() {
    D d = F();
    Console.WriteLine(d());
    Console.WriteLine(d());
    Console.WriteLine(d());
}
```

局部变量 x 被匿名函数捕获，并且 x 的生存期至少延长到从 F 返回的委托有资格进行垃圾回收为止（直到程序结束时才会发生）。由于匿名函数的每次调用都操作 x 的同一实例，因此该示例的输出为

- 1
- 2
- 3

当局部变量或值参数被匿名函数捕获时，该局部变量或参数不再被视为固定变量（§18.3），而是被视为可移动变量。因此，任何获取捕获的外部变量地址的不安全代码都必须先使用 fixed 语句固定该变量。

请注意，与未捕获的变量不同，捕获的局部变量可以同时暴露给多个执行线程。

### 7.15.5.2 局部变量的实例化

当执行进入变量的作用域时，局部变量被视为已实例化。例如，当调用以下方法时，局部变量 x 会被实例化和初始化三次——循环的每次迭代一次：

```
static void F() {
    for (int i = 0; i < 3; i++) {
        int x = i * 2 + 1;
        ...
    }
}
```

然而，将 x 的声明移到循环外部会导致 x 只实例化一次：

```
static void F() {
    int x;
    for (int i = 0; i < 3; i++) {
        x = i * 2 + 1;
        ...
    }
}
```

当未被捕获时，无法观察局部变量被实例化的确切频率：由于各实例化的生存期不相交，每个实例化可能只是使用相同的存储位置。然而，当匿名函数捕获局部变量时，实例化的效果会变得明显。

## 示例

```
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

产生以下输出：

1
3
5

然而，当 x 的声明移到循环外部时

```
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

输出为

5
5
5

如果 for 循环声明了迭代变量，则该变量本身被视为在循环外部声明。因此，如果将示例改为捕获迭代变量本身，



## 7. 表达式

```csharp
static D[] F() {
    D[] result = new D[3];
    for (int i = 0; i < 3; i++) {
        result[i] = () => { Console.WriteLine(i); };
    }
    return result;
}
```

只捕获迭代变量的一个实例，产生以下输出：

```text
3
3
3
```

> **埃里克·利珀特** 这种行为——即匿名函数捕获的是循环变量，而不是该变量的当前值——是我们收到的最常见的一类错误报告“我认为我在编译器中发现了一个 bug”的成因。对于本规范的未来版本，我们正在考虑将 foreach 循环变量的正式定义移到循环内部，这样循环内的匿名函数在每次循环时都会捕获一个新变量。从技术上讲，这将是一次破坏性变更，但它会让语言的行为符合大多数人所认为它应有的行为。很难想象在什么情况下你会*想要*将循环变量作为变量而不是作为值来捕获。

匿名函数委托可以共享某些捕获变量，同时拥有其他变量的独立实例。例如，如果 F 改为

```csharp
D[] result = new D[3];
int x = 0;
for (int i = 0; i < 3; i++) {
    int y = 0;
    result[i] = () => { Console.WriteLine("{0} {1}", ++x, ++y); };
}
return result;
}
```

这三个委托捕获同一个 x 实例，但捕获不同的 y 实例，输出为

```text
1 1
2 1
3 1
```

不同的匿名函数可以捕获外部变量的同一实例。在示例

```csharp
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

这两个匿名函数捕获局部变量 x 的同一实例，并且它们可以通过该变量“通信”。该示例的输出为

5
10

## 7.15.6 匿名函数表达式的求值

匿名函数 F 必须始终转换为委托类型 D 或表达式树类型 E，可以直接转换，也可以通过执行委托创建表达式 new D(F) 进行转换。此转换确定匿名函数的结果，如 §6.5 所述。

## 7.16 查询表达式

*查询表达式*提供了一种语言集成的查询语法，类似于 SQL 和 XQuery 等关系型和分层查询语言。

```
query-expression:
    from-clause query-body

from-clause:
    from type_opt identifier in expression

query-body:
    query-body-clauses_opt select-or-group-clause query-continuation_opt

query-body-clauses:
    query-body-clause
    query-body-clauses query-body-clause
```

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

ordering-direction:
    ascending
    descending

select-or-group-clause:
    select-clause
    group-clause

select-clause:
    select expression

```
group-clause:
    group expression by expression
```

```
query-continuation:
    into identifier query-body
```

查询表达式以 from 子句开头，并以 select 或 group 子句结尾。初始 from 子句后可以跟零个或多个 from、let、where、join 或 orderby 子句。每个 from 子句都是一个生成器，引入一个范围变量，该变量遍历序列的元素。每个 let 子句引入一个范围变量，表示通过前面的范围变量计算出的值。每个 where 子句都是一个筛选器，用于从结果中排除项。每个 join 子句将源序列的指定键与另一个序列的键进行比较，生成匹配对。每个 orderby 子句根据指定条件对项重新排序。最后的 select 或 group 子句根据范围变量指定结果的形状。最后，可以使用 into 子句将一个查询的结果作为后续查询中的生成器来“拼接”查询。

> **埃里克·利珀特** 为什么 C# 中的查询语法是“from…where…select”，而不是 SQL 开发者更熟悉的顺序：“select…from…where”？尽管 SQL 的顺序具有让 SQL 开发者熟悉、对英语使用者自然的优点，但它会给语言和 IDE 设计者带来许多 C# 顺序中不存在的问题。
> 
> 首先，由于作用域规则，IntelliSense 很难与 SQL 顺序一起使用。想象一下，你正在为“select 在前”的语法设计一个 IDE。用户刚刚输入了“select”：然后呢？你不知道用户要从哪个数据源进行投影，因此无法生成合理的实用选项列表。你也无法为“where”提供任何帮助。在 C# 体系中，“from”出现在“select”之前；因此，当用户输入“where”或“select”时，IDE 已经知道数据源的类型信息。
> 
> 其次，C# 的顺序是代码实际执行操作的顺序：首先确定集合，然后对集合运行筛选器，然后投影筛选器的结果。这种顺序有助于让人了解数据如何在系统中流动。

> **克里斯·塞尔斯** 现在我已经见过 SQL 中的“select-from”和 LINQ 中的“from-select”这两种顺序，LINQ 对我来说合理多了，而 SQL 不允许“from-select”风格让我感到沮丧。

## 7.16.1 查询表达式中的歧义

查询表达式包含许多“上下文关键字”——即在给定上下文中具有特殊含义的标识符。具体来说，这些关键字是 from、where、join、on、equals、into、let、orderby、ascending、descending、select、group 和 by。为了避免由于将这些标识符混合用作关键字或简单名称而在查询表达式中产生歧义，当这些标识符出现在查询表达式中的任何位置时，它们都被视为关键字。

为此，查询表达式是指以“from 标识符”开头，后跟除“;”、“=”或“,”之外的任何标记的任何表达式。

要在查询表达式内将这些词用作标识符，可以在它们前面加上“@”前缀（§2.4.2）。

## 7.16.2 查询表达式转换

C# 语言不规定查询表达式的执行语义。相反，查询表达式会被转换为对遵循查询表达式模式（§7.16.3）的方法的调用。具体来说，查询表达式会被转换为对名为 where、Select、SelectMany、Join、GroupJoin、OrderBy、OrderByDescending、ThenBy、ThenByDescending、GroupBy 和 Cast 的方法的调用。这些方法应具有特定的签名和结果类型，如 §7.16.3 所述。这些方法可以是被查询对象的实例方法，也可以是对象外部的扩展方法，它们实现查询的实际执行。

从查询表达式到方法调用的转换是一种语法映射，发生在执行任何类型绑定或重载解析之前。该转换保证语法正确，但不保证生成语义正确的 C# 代码。在查询表达式转换之后，生成的方法调用会作为常规方法调用处理，这反过来可能揭示错误——例如，如果方法不存在、参数类型错误，或者方法是泛型的且类型推断失败。

> **比尔·瓦格纳** 这一整节是理解查询表达式如何转换为方法调用（以及可能的扩展方法调用）的绝佳方式。

> **乔恩·斯基特** 查询表达式能够以对规范如此小的增补引入 C#，这一事实令我惊叹。虽然某些特性（例如泛型）几乎影响了语言的每个领域，但查询表达式惊人地自包含——尤其是考虑到它们所提供的表达力。



查询表达式通过反复应用以下转换来处理，直到不再可能进行任何归约为止。这些转换按应用顺序列出：每一节都假定前面各节中的转换已被穷尽执行；一旦某一节被穷尽，在同一个查询表达式的处理过程中就不会再回到该节。

查询表达式中不允许对范围变量赋值。但是，C# 实现可以不必始终强制执行此限制，因为对于此处给出的语法转换方案而言，有时这可能无法做到。

某些转换会注入带有由 * 表示的透明标识符的范围变量。透明标识符的特殊属性将在 §7.16.2.7 中进一步讨论。

> **克里斯·塞尔斯** 尽管我很喜欢 C# 3.0 查询语法，但有时很难把这些转换记在脑子里。如果你偶尔觉得需要用方法调用语法写出查询，也不必感到糟糕。另外，你自己实现的任何查询方法都不会有语言构造，因此有时你除了使用方法调用语法之外别无选择。
> 
> 此外，如果你的同行这样写查询，也完全没问题：
> 
> ```
> var duluthians = from c in Customers
>     where c.City == "Duluth" select c;
> ```
> 
> 而你这样写查询：
> 
> ```
> var duluthians = Customers.Where(c => c.City == "Duluth");
> ```
> 
> 第二种语法不需要在头脑中进行转换，并且适用于所有扩展方法，而不仅仅是那些已转换为关键字的方法。例如：
> 
> ```
> var tenDuluthites = Customers.Where(c => c.City == "Duluth").Take(10);
> ```
> 
> 对比：
> 
> ```
> var tenDuluthites = (from c in Customers where c.City ==
>     "Duluth" select c).Take(10);
> ```
> 
> 我是个简单的人，所以我更喜欢始终有效的语法风格，而不是如今那些时髦做法。

> **乔恩·斯基特** 虽然查询表达式不太可能支持 IEnumerable<T> 上的其他查询方法，但其定义的美妙之处之一在于其中立性：规范中没有任何内容规定这些类型应该是什么。这使得其他框架（例如 Reactive Extensions 和 Parallel Extensions）能够针对新类型编写查询方法，并且仍然利用查询表达式语法。

## 7.16.2.1 带延续的 select 和 GroupBy 子句

带延续的查询表达式

```
from ... into x ...
```

转换为

```
from x in ( from ... ) ...
```

以下各节中的转换假设查询没有 into 延续。

示例

```
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```

转换为

```
from g in
    from c in customers
    group c by c.Country
select new { Country = g.Key, CustCount = g.Count() }
```

其最终转换为

```
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

> **约瑟夫·阿尔巴哈里** 查询延续的目的是允许在 select 或 group 子句（否则它们会终止查询）之后继续添加子句。在查询延续之后，先前的范围变量以及通过 join 或 let 子句引入的任何变量都将超出作用域。相比之下，let 子句的作用类似于非破坏性 select：它使先前的范围变量和其他查询变量保持在作用域内。
> 
> 查询延续引入的标识符可以与前面的范围变量相同。

## 7.16.2.2 显式范围变量类型

显式指定范围变量类型的 from 子句

```
from T x in e
```

转换为

```
from x in ( e ) . Cast < T > ( )
```

显式指定范围变量类型的 join 子句

```
join T x in e on k1 equals k2
```

转换为

```
join x in ( e ) . Cast < T > ( ) on k1 equals k2
```

以下各节中的转换假设查询没有显式范围变量类型。

示例

```
from Customer c in customers
where c.City == "London"
select c
```

转换为

```
from c in customers.Cast<Customer>()
where c.City == "London"
select c
```

其最终转换为

```
customers.
Cast<Customer>().
Where(c => c.City == "London")
```

显式范围变量类型对于查询实现非泛型 IEnumerable 接口但不实现泛型 IEnumerable<T> 接口的集合很有用。在上面的示例中，如果 customers 的类型是 ArrayList，就属于这种情况。

## 7.16.2.3 退化查询表达式

形式如下的查询表达式

```
from x in e select x
```

转换为

```
( e ) . Select ( x => x )
```

示例

```
from c in customers
select c
```

转换为

```
customers.Select(c => c)
```

退化查询表达式是指简单地选择源中元素的查询表达式。转换的后续阶段会通过用其源替换其他转换步骤引入的退化查询来移除它们。然而，重要的是要确保查询表达式的结果永远不是源对象本身，因为那会向查询客户端暴露源的类型和标识。因此，这一步通过在源上显式调用 Select 来保护直接写在源代码中的退化查询。然后由 Select 和其他查询运算符的实现者确保这些方法永远不会返回源对象本身。

## 7.16.2.4 from、let、where、join 和 orderby 子句

> 约瑟夫·阿尔巴哈里 本节中看似笨拙的转换正是查询语法真正有用的原因：它们消除了手工写出笨拙查询的需要。如果没有这个问题，考虑到 lambda 表达式和扩展方法的能力，将查询表达式语法引入 C# 3.0 可能就没有多少理由了。
> 
> 更复杂转换中的共同主题是投影到临时匿名类型的过程，以便在 let、from 或 join 子句之后使先前的范围变量保持在作用域内。

带有第二个 from 子句后跟 select 子句的查询表达式

```
from x1 in e1
from x2 in e2
select v
```

转换为

```
( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => v )
```

带有第二个 from 子句后跟非 select 子句的查询表达式

```
from x1 in e1
from x2 in e2
...
```

转换为

```
from * in ( e₁ ) . SelectMany( x₁ => e₂ , ( x₁ , x₂ ) => new { x₁ , x₂ } )
```

### 带 let 子句的查询表达式

```
from x in e
let y = f
...
```

转换为

```
from * in ( e ) . Select ( x => new { x , y = f } )
...
```

### 带 where 子句的查询表达式

```
from x in e
where f
...
```

转换为

```
from x in ( e ) . Where ( x => f )
...
```

### 带有一个不带 into 的 join 子句且后跟 select 子句的查询表达式

```
from x₁ in e₁
join x₂ in e₂ on k₁ equals k₂
select v
```

转换为

```
( e₁ ) . Join( e₂ , x₁ => k₁ , x₂ => k₂ , ( x₁ , x₂ ) => v )
```

### 带有一个不带 into 的 join 子句且后跟非 select 子句的查询表达式

```
from x₁ in e₁
join x₂ in e₂ on k₁ equals k₂
...
```

转换为

```
from * in ( e₁ ) . Join( e₂ , x₁ => k₁ , x₂ => k₂ , ( x₁ , x₂ ) => new { x₁ , x₂ } )
...
```

带有一个带 into 的 join 子句且后跟 select 子句的查询表达式

```
from x₁ in e₁
join x₂ in e₂ on k₁ equals k₂ into g
select v
```

转换为

```
( e₁ ). GroupJoin( e₂ , x₁ => k₁ , x₂ => k₂ , ( x₁ , g ) => v )
```

带有一个带 into 的 join 子句且后跟非 select 子句的查询表达式

```
from x₁ in e₁
join x₂ in e₂ on k₁ equals k₂ into g
...
```

转换为

```
from * in ( e₁ ). GroupJoin( e₂ , x₁ => k₁ , x₂ => k₂ , ( x₁ , g ) => new { x₁ , g } )
```

带有 orderby 子句的查询表达式

```
from x in e
orderby k₁ , k₂ , ... , kₙ
...
```

转换为

```
from x in ( e ) .
OrderBy ( x => k₁ ) .
ThenBy ( x => k₂ ) .
...
ThenBy ( x => kₙ )
...
```

如果排序子句指定降序方向指示符，则改为生成对 OrderByDescending 或 ThenByDescending 的调用。

以下转换假设没有 let、where、join 或 orderby 子句，并且每个查询表达式中至多有一个初始 from 子句。

示例

```
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```

转换为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c.Name, o.OrderID, o.Total })
```


示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

被翻译成

```
from * in customers.
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

示例

```
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```

被翻译成

```
from * in Orders.
    Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000
select new { o.OrderID, Total = t }
```

其最终翻译为

```
Orders.
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) }).
Where(o => o.t >= 1000).
Select(x => new { x.o.OrderID, Total = x.t })
```

其中 x 是一个编译器生成的标识符，否则不可见且无法访问。

示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
select new { c.Name, o.OrderDate, o.Total }
```

被翻译成

```
customers.Join(orders, c => c.CustomerID, o => o.CustomerID,
    (c, o) => new { c.Name, o.OrderDate, o.Total })
```

## 示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID into co
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```

被翻译成

```
from * in customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
    (c, co) => new { c, co })
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```

其最终翻译为

```
customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID, (c, co) => new { c, co }).
Select(x => new { x, x.co.Count() }).
Where(y => y.n >= 10).
Select(y => new { y.x.c.Name, OrderCount = y.n })
```

其中 x 和 y 是编译器生成的标识符，否则不可见且无法访问。

## 示例

```
from o in orders
orderby o.Customer.Name, o.Total descending
select o
```

其最终翻译为

## 7.16.2.5 select 子句

形式为 的查询表达式

```
from x in e select v
```

被翻译成

```text
( e ) . Select( x => v )
```

除非 *v* 是标识符 *x*，此时翻译仅为

```text
( e )
```

例如，

```csharp
from c in customers.Where(c => c.City == "London")
select c
```

被简单翻译为

```csharp
customers.Where(c => c.City == "London")
```

## 7.16.2.6 *GroupBy* 子句

形式为 的查询表达式

```text
from x in e group v by k
```

被翻译成

```text
( e ) . GroupBy( x => k , x => v )
```

除非 *v* 是标识符 *x*，翻译为

```text
( e ) . GroupBy( x => k )
```

示例

```csharp
from c in customers
group c.Name by c.Country
```

被翻译成

```csharp
customers.
GroupBy(c => c.Country, c => c.Name)
```

## 7.16.2.7 *透明标识符*

某些翻译会注入用 * 表示的 *透明标识符* 范围变量。透明标识符不是正式的语言特性；它们仅作为查询表达式翻译过程中的中间步骤存在。

当查询翻译注入透明标识符时，后续的翻译步骤会将透明标识符传播到匿名函数和匿名对象初始化器中。在这些上下文中，透明标识符具有以下行为：

- 当透明标识符作为匿名函数的参数出现时，相关匿名类型的成员会在匿名函数体中自动进入作用域。
- 当带透明标识符的成员在作用域内时，该成员的成员也在作用域内。
- 当透明标识符作为匿名对象初始化器中的成员声明符出现时，它会引入一个带透明标识符的成员。

在上述描述的翻译步骤中，透明标识符总是与匿名类型一起引入，目的是将多个范围变量作为单个对象的成员捕获。C# 的实现可以使用不同于匿名类型的机制来对多个范围变量进行分组。以下翻译示例假定使用匿名类型，并展示透明标识符如何被消除。

示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```

被翻译成

```
from * in customers.
    SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.Total }
```

其进一步被翻译为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(* => o.Total).
Select(* => new { c.Name, o.Total })
```

当透明标识符被擦除时，其等价于

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

被翻译成

```
from * in customers.
Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o })
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```

其进一步被简化为

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
Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o }).
Join(details, x => x.o.OrderID, d => d.OrderID, (x, d) => new { x, d }).
Join(products, y => y.d.ProductID, p => p.ProductID, (y, p) => new { y, p }).
Select(z => new { z.y.x.c.Name, z.y.x.o.OrderDate, z.p.ProductName })
```

其中 x、y 和 z 是编译器生成的标识符，否则不可见且无法访问。

## 7.16.3 查询表达式模式

查询表达式模式建立了一种方法模式，类型可以实现该模式以支持查询表达式。由于查询表达式通过语法映射被翻译为方法调用，类型在实现查询表达式模式时具有相当大的灵活性。例如，模式的方法可以作为实例方法或扩展方法实现，因为两者具有相同的调用语法，并且方法可以请求委托或表达式树，因为匿名函数都可以转换为两者。

支持查询表达式模式的泛型类型 C<T> 的推荐形状如下所示。 使用泛型类型来说明参数类型和结果类型之间的正确关系，但也可以为非泛型类型实现该模式。

```
class C<T> : C
{
    public C<T> Where(Func<T,bool> predicate);
    public C<U> Select<U>(Func<T,U> selector);
}
```

## 7. 表达式

```
public C<V> SelectMany<U,V>(Func<T,U> selector,
    Func<T,U,V> resultSelector);

public C<V> Join<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
    Func<U,K> innerKeySelector, Func<T,U,V> resultSelector);

public C<V> GroupJoin<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
    Func<U,K> innerKeySelector, Func<T,C<U>,V> resultSelector);

public O<T> OrderBy<K>(Func<T,K> keySelector);

public O<T> OrderByDescending<K>(Func<T,K> keySelector);

public C<G<K,T>> GroupBy<K>(Func<T,K> keySelector);

public C<G<K,E>> GroupBy<K,E>(Func<T,K> keySelector,
    Func<T,E> elementSelector);
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

上述方法使用泛型委托类型 Func<T1, R> 和 Func<T1, T2, R>，但它们同样可以使用具有相同参数和结果类型关系的其他委托或表达式树类型。

请注意 C<T> 与 O<T> 之间的推荐关系，它确保 ThenBy 和 ThenByDescending 方法仅在 OrderBy 或 OrderByDescending 的结果上可用。还请注意 GroupBy 结果的推荐形状——序列的序列，其中每个内部序列都有一个额外的键属性。

> **BILL WAGNER**  ThenBy 通常比 OrderBy 性能更好，因为它只需要对具有多个值的内部序列进行排序。

System.Linq 命名空间为实现 System.Collections.Generic.IEnumerable<T> 接口的任何类型提供了查询运算符模式的实现。

> **BILL WAGNER**  对于实现 IQueryable<T> 的任何类型也存在实现。



> > **埃里克·利珀特** Join 的这个签名是方法类型推断算法中“先累积边界，再修正到最佳者”这一部分的主要动因之一。如果内层键的类型是 int，而外层键的类型是 int?，那么与其让类型推断因这种“矛盾”而失败，不如简单地选择这两种类型中更一般的那个。因为每个 int 都是 int?，所以类型推断算法会为 K 选择 int?。

## 7.17 赋值运算符

赋值运算符将新值赋给变量、属性、事件或索引器元素。

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

赋值运算符的左操作数必须是分类为变量、属性访问、索引器访问或事件访问的表达式。

= 运算符称为*简单赋值运算符*。它将右操作数的值赋给左操作数所给定的变量、属性或索引器元素。简单赋值运算符的左操作数不能是事件访问（§10.8.1 所述情况除外）。简单赋值运算符在 §7.17.1 中描述。

除 = 运算符之外的赋值运算符称为*复合赋值运算符*。这些运算符对两个操作数执行指定的运算，然后将结果值赋给左操作数所给定的变量、属性或索引器元素。复合赋值运算符在 §7.17.2 中描述。

以事件访问表达式为左操作数的 += 和 -= 运算符称为*事件赋值运算符*。其他赋值运算符不能以事件访问作为左操作数。事件赋值运算符在 §7.17.3 中描述。

赋值运算符是右结合的，意味着运算从右到左分组。例如，形式为 a = b = c 的表达式按 a = (b = c) 求值。

### 7.17.1 简单赋值

= 运算符称为简单赋值运算符。

如果简单赋值的左操作数形式为 E.P 或 E[E]，其中 E 的编译时类型为 dynamic，则该赋值是动态绑定的（§7.2.2）。在这种情况下，赋值表达式的编译时类型为 dynamic，下面描述的解析将在运行时基于 E 的运行时类型进行。

在简单赋值中，右操作数必须是可隐式转换为左操作数类型的表达式。该操作将右操作数的值赋给左操作数所给定的变量、属性或索引器元素。

简单赋值表达式的结果是赋给左操作数的值。该结果与左操作数具有相同类型，并且始终分类为值。

如果左操作数是属性或索引器访问，则该属性或索引器必须具有 set 访问器。如果不是，则发生绑定期错误。

形式为 x = y 的简单赋值的运行时处理包括以下步骤：

- 如果 x 分类为变量：
  - 对 x 求值以产生该变量。
  - 对 y 求值，并在需要时通过隐式转换（§6.1）转换为 x 的类型。
  - 如果 x 给定的变量是引用类型的数组元素，则执行运行时检查，以确保为 y 计算的值与 x 所属的数组实例兼容。如果 y 为 null，或者从 y 引用的实例的实际类型到包含 x 的数组实例的实际元素类型存在隐式引用转换（§6.1.6），则检查成功。否则，抛出 System.ArrayTypeMismatchException。
  - 由 y 的求值和转换产生的值存储到由 x 的求值给定的位置。
- 如果 x 分类为属性或索引器访问：
  - 与 x 关联的实例表达式（如果 x 不是静态的）和参数列表（如果 x 是索引器访问）被求值，结果用于后续的 set 访问器调用。
  - 对 y 求值，并在需要时通过隐式转换（§6.1）转换为 x 的类型。
  - 使用为 y 计算的值作为其 value 参数调用 x 的 set 访问器。

数组协变规则（§12.5）允许数组类型 A[] 的值成为数组类型 B[] 实例的引用，前提是存在从 B 到 A 的隐式引用转换。由于这些规则，对引用类型的数组元素进行赋值需要运行时检查，以确保所赋的值与数组实例兼容。在示例

```
string[] sa = new string[10];
object[] oa = sa;

oa[0] = null;          // Okay
oa[1] = "Hello";       // Okay
oa[2] = new ArrayList();   // ArrayTypeMismatchException
```

中，最后一个赋值导致抛出 System.ArrayTypeMismatchException，因为 ArrayList 的实例不能存储在 string[] 的元素中。

> > **比尔·瓦格纳** 这一点意味着数组赋值不会复制数组，而是向同一存储添加一个新引用。

当结构体类型中声明的属性或索引器是赋值目标时，与该属性或索引器访问关联的实例表达式必须分类为变量。如果实例表达式分类为值，则发生绑定期错误。根据 §7.6.4，同样的规则也适用于字段。

给定以下声明：

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

    public int Y
    {
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

在示例

```
Point p = new Point();
p.X = 100;
p.Y = 100;
Rectangle r = new Rectangle();
r.A = new Point(10, 10);
r.B = p;
```

中，对 p.X、p.Y、r.A 和 r.B 的赋值是允许的，因为 p 和 r 是变量。然而，在示例

```
Rectangle r = new Rectangle();
r.A.X = 10;
r.A.Y = 10;
r.B.X = 100;
r.B.Y = 100;
```

中，这些赋值全部无效，因为 r.A 和 r.B 不是变量。

> > **约瑟夫·阿尔巴哈里** C# 1.0 编译器的早期版本允许诸如 r.A.X = 10 的赋值——但它们会静默失败，因为 r.A 返回的是 Point 的副本（即值），而不是变量。人们发现这种行为令人困惑，因此检测到该情况并将其报告为错误。

> > **比尔·瓦格纳** 这一讨论凸显了结构体应当不可变的又一个原因。

### 7.17.2 复合赋值

如果复合赋值的左操作数形式为 E.P 或 E[E_i]，其中 E 的编译时类型为 dynamic，则该赋值是动态绑定的（§7.2.2）。在这种情况下，赋值表达式的编译时类型为 dynamic，下面描述的解析将在运行时基于 E 的运行时类型进行。

形式为 x op= y 的运算按如下方式处理：应用二元运算符重载解析（§7.3.4），如同该运算写成 x op y。然后，

- 如果所选运算符的返回类型可*隐式*转换为 x 的类型，则按 x = x op y 对该运算求值，但 x 只求值一次。
- 否则，如果所选运算符是预定义运算符，如果所选运算符的返回类型可*显式*转换为 x 的类型，并且如果 y 可*隐式*转换为 x 的类型，或者该运算符是移位运算符，则按 x = (T)(x op y) 对该运算求值，其中 T 是 x 的类型，但 x 只求值一次。
- 否则，该复合赋值无效，并发生绑定期错误。

> > **彼得·塞斯托夫特** 第二项中 y 可隐式转换为 x 的类型的条件意味着，C# 中的复合运算符比 C、C++ 和 Java 编程语言中的复合运算符限制更严格。在那些语言中，即使变量 x 具有整数类型，赋值 x+=0.9 也是合法的。当 x 非负时，该赋值没有效果；当 x 为负时，它会将 x 加 1。在 C# 中，该赋值被拒绝——在我看来这是明智的。

> > **弗拉基米尔·列舍特尼科夫** 这些规则的一个奇怪结果是，如果变量 x 具有类型 int?，则表达式 x <<= null 是合法的。当然，它在运行时将始终抛出异常。



术语“只求值一次”是指，在计算 x op y 时，x 的任何构成表达式的结果都会被临时保存，然后在执行对 x 的赋值时重用。例如，在赋值 A()[B()] += C() 中，A 是返回 int[] 的方法，B 和 C 是返回 int 的方法，这些方法只按 A、B、C 的顺序调用一次。

当复合赋值的左操作数是属性访问或索引器访问时，该属性或索引器必须同时具有 get 访问器和 set 访问器。如果不是这样，就会发生绑定时间错误。

上述第二条规则允许在某些上下文中将 x op= y 计算为 x = (T)(x op y)。该规则的存在使得当左操作数的类型为 sbyte、byte、short、ushort 或 char 时，预定义运算符可以用作复合运算符。即使两个参数都属于这些类型之一，预定义运算符也会生成 int 类型的结果，如 §7.3.6.2 所述。因此，如果没有强制转换，就不可能将结果赋给左操作数。

对于预定义运算符，该规则的直观效果很简单：如果 x op y 和 x = y 都允许，则允许 x op= y。在示例

```
byte b = 0;
char ch = '\0';
int i = 0;

b += 1;            // Okay
b += 1000;         // Error: b = 1000 not permitted
b += i;            // Error: b = i not permitted
b += (byte)i;      // Okay

ch += 1;           // Error: ch = 1 not permitted
ch += (char)1;     // Okay
```

中，每个错误的直观原因是对应的简单赋值也会是错误的。

这也意味着复合赋值运算支持提升运算。在示例

```
int? i = 0;
i += 1;            // Ok
```

中，使用了提升运算符 +(int?, int?)。

## 7.17.3 事件赋值

如果 += 或 -= 运算符的左操作数被归类为事件访问，则按如下方式计算表达式：

- 计算事件访问的实例表达式（如果有）。
- 计算 += 或 -= 运算符的右操作数，并在需要时通过隐式转换（§6.1）将其转换为左操作数的类型。
- 调用事件的事件访问器，其参数列表由求值后并在必要时转换后的右操作数组成。如果运算符是 +=，则调用 add 访问器；如果运算符是 -=，则调用 remove 访问器。

事件赋值表达式不产生值。因此，事件赋值表达式仅在语句表达式（§8.6）的上下文中有效。

## 7.18 表达式

表达式要么是非赋值表达式，要么是赋值。

```
expression:
    non-assignment-expression
    assignment

non-assignment-expression:
    conditional-expression
    lambda-expression
    query-expression
```

## 7.19 常量表达式

常量表达式是可以在编译时完全求值的表达式。

```
constant-expression:
    expression
```

常量表达式必须是 null 字面量，或者具有以下类型之一的值：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool、string 或任何枚举类型。常量表达式中只允许以下构造：

- 字面量（包括 null 字面量）。
- 对类和结构类型的 const 成员的引用。
- 对枚举类型成员的引用。
- 对 const 参数或局部变量的引用。
- 括号子表达式，其本身也是常量表达式。

- 强制转换表达式，前提是目标类型为上述列出的类型之一。
- checked 和 unchecked 表达式。
- 默认值表达式。
- 预定义的一元运算符 +、-、! 和 ~。
- 预定义的二元运算符 +、-、*、/、%、<<、>>、&、|、^、&&、||、==、!=、<、>、<= 和 >=，前提是每个操作数的类型均为上述列出的类型之一。
- ?: 条件运算符。

常量表达式中允许以下转换：

- 标识转换。
- 数值转换。
- 枚举转换。
- 常量表达式转换。
- 隐式和显式引用转换，前提是转换的源是求值为 null 值的常量表达式。

其他转换，包括装箱、拆箱以及非 null 值的隐式引用转换，在常量表达式中不允许。例如：

```
class C {
    const object i = 5;      // Error: boxing conversion not permitted
    const object str = "hello"; // Error: implicit reference conversion
}
```

在此示例中，i 的初始化是错误的，因为需要装箱转换。str 的初始化是错误的，因为需要从非 null 值进行隐式引用转换。

每当表达式满足上述要求时，该表达式都会在编译时求值。即使该表达式是包含非常量构造的更大表达式的子表达式，也是如此。

常量表达式的编译时求值使用与非恒定表达式运行时求值相同的规则，不同之处在于：运行时求值会抛出异常的地方，编译时求值会导致编译时错误发生。

除非常量表达式显式置于 unchecked 上下文中，否则在表达式的编译时求值期间，整型算术运算和转换中发生的溢出始终会导致编译时错误（§7.19）。

常量表达式出现在下面列出的上下文中。在这些上下文中，如果表达式无法在编译时完全求值，则会发生编译时错误。

- 常量声明（§10.4）。
- 枚举成员声明（§14.3）。
- switch 语句的 case 标签（§8.7.2）。
- goto case 语句（§8.9.3）。
- 包含初始化器的数组创建表达式（§7.6.10.4）中的维度长度。
- 特性（§17）。

隐式常量表达式转换（§6.1.8）允许将 int 类型的常量表达式转换为 sbyte、byte、short、ushort、uint 或 ulong，前提是该常量表达式的值位于目标类型的范围内。

## 7.20 布尔表达式

*布尔表达式*是直接产生 bool 类型结果，或者在某些上下文中通过应用 operator true 产生 bool 类型结果的表达式，具体如下所述。

```
boolean-expression:
    expression
```

*if 语句*（§8.7.1）、*while 语句*（§8.8.1）、*do 语句*（§8.8.2）或 *for 语句*（§8.8.3）的控制条件表达式是*布尔表达式*。?: 运算符（§7.14）的控制条件表达式遵循与*布尔表达式*相同的规则，但出于运算符优先级的考虑，它被归类为*条件或表达式*。

*布尔表达式*必须可隐式转换为 bool，或者其类型实现 operator true。如果两项要求均不满足，则会发生绑定时间错误。

当布尔表达式不能隐式转换为 bool，但确实实现 operator true 时，则在求值该表达式之后，会调用该类型提供的 operator true 实现来产生 bool 值。

§11.4.2 中的 DBBool 结构类型提供了一个实现 operator true 和 operator false 的类型的示例。

此页有意留空

# 8. 语句

C# 提供了多种语句。对于使用过 C 和 C++ 编程的开发人员来说，其中大多数语句都很熟悉。

- 语句：
  - 带标签语句
  - 声明语句
  - 嵌入语句

- 嵌入语句：
  - 块
  - 空语句
  - 表达式语句
  - 选择语句
  - 迭代语句
  - 跳转语句
  - try 语句
  - checked 语句
  - unchecked 语句
  - lock 语句
  - using 语句
  - yield 语句

*嵌入语句*非终结符用于出现在其他语句内的语句。使用*嵌入语句*而不是*语句*，排除了在这些上下文中使用声明语句和带标签语句。示例

```
void f(bool b) {
    if (b)
        int i = 44;
}
```

会导致编译时错误，因为 if 语句的 if 分支要求的是*嵌入语句*，而不是*语句*。如果允许这段代码，那么变量 i

将会被声明，但它永远无法被使用。然而，通过将 i 的声明放在一个块中，该示例是有效的。

## 8.1 端点和可达性

每个语句都有一个 *端点*。直观地说，语句的端点是紧跟在该语句之后的位置。复合语句（包含嵌入语句的语句）的执行规则指定了当控制流到达嵌入语句的端点时所采取的动作。例如，当控制流到达块中某个语句的端点时，控制流会转移到块中的下一个语句。

如果一个语句有可能通过执行到达，则称该语句为 *可达*。相反，如果一个语句不可能被执行，则称该语句为 *不可达*。

在下面的示例中

```csharp
void F() {
    Console.WriteLine("reachable");
    goto Label;
    Console.WriteLine("unreachable");
Label:
    Console.WriteLine("reachable");
}
```

第二次调用 Console.WriteLine 是不可达的，因为该语句不可能被执行。

如果编译器确定某个语句不可达，则会报告警告。特别地，语句不可达并不是错误。

为了确定某个特定语句或端点是否可达，编译器会根据为每个语句定义的可达性规则执行流分析。流分析会考虑控制语句行为的常量表达式 (§7.19) 的值，但不考虑非常量表达式的可能值。换句话说，就控制流分析而言，给定类型的非常量表达式被认为具有该类型的任何可能值。

在下面的示例中

```csharp
void F() {
    const int i = 1;
    if (i == 2) Console.WriteLine("unreachable");
}
```

if 语句的布尔表达式是一个常量表达式，因为 == 运算符的两个操作数都是常量。由于常量表达式在编译时求值，结果为 false，因此 Console.WriteLine 调用被视为不可达。然而，如果 i 被改为局部变量

```csharp
void F() {
    int i = 1;
    if (i == 2) Console.WriteLine("reachable");
}
```

Console.WriteLine 调用被视为可达，即使实际上它永远不会被执行。

> ERIC LIPPERT 人类知道永远为假的许多其他表达式，并不会被流分析器视为假。例如，如果我们将上面 if 语句的条件替换为 (i * 0 == 0)，那么根据规范，后果将被视为可达——即使你我都知道实际上它不可达。

函数成员的块始终被视为可达。通过依次评估块中每个语句的可达性规则，可以确定任何给定语句的可达性。

在下面的示例中

```csharp
void F(int x) {
    Console.WriteLine("start");
    if (x < 0) Console.WriteLine("negative");
}
```

第二个 Console.WriteLine 的可达性确定如下：

- 第一个 Console.WriteLine 表达式语句是可达的，因为 F 方法的块是可达的。
- 第一个 Console.WriteLine 表达式语句的端点是可达的，因为该语句是可达的。
- if 语句是可达的，因为第一个 Console.WriteLine 表达式语句的端点是可达的。
- 第二个 Console.WriteLine 表达式语句是可达的，因为 if 语句的布尔表达式不具有常量值 false。

有两种情况，语句的端点可达会导致编译时错误：

- 由于 switch 语句不允许 switch 部分“贯穿”到下一个 switch 部分，因此 switch 部分的语句列表的端点可达是编译时错误。如果出现此错误，通常表示缺少 break 语句。
- 对于计算值的函数成员的块的端点可达是编译时错误。如果出现此错误，通常表示缺少 return 语句。

> **BILL WAGNER** 可达代码的规则旨在偏向假设代码可达。例如，下面的示例不会对不可达代码生成任何警告：

对人类读者来说很明显，“weird”永远不会出现在你的控制台上。语言规则并不遵循同样的推理。

```csharp
public class Program
{
    public static int counter = 5;
    static void Main(string[] args)
    {
        if (counter == 6)
            Console.WriteLine("weird");
        else
            Console.WriteLine("normal");
    }
}
```

## 8.2 块

块允许在只允许单个语句的上下文中编写多个语句。

```
block:
    { statement-list_opt }
```

一个块由可选的语句列表 (§8.2.1) 组成，用大括号括起来。如果省略语句列表，则该块称为空块。

块可以包含声明语句 (§8.5)。在块中声明的局部变量或常量的作用域是该块。

在块内，在表达式上下文中使用的名称的含义必须始终相同 (§7.6.2.1)。

块的执行方式如下：

- 如果块为空，则控制流转移到块的端点。
- 如果块不为空，则控制流转移到语句列表。当且如果控制流到达语句列表的端点，则控制流转移到块的端点。

如果块本身可达，则块的语句列表可达。

如果块为空或语句列表的端点可达，则块的端点可达。

包含一个或多个 yield 语句 (§8.14) 的块称为迭代器块。迭代器块用于将函数成员实现为迭代器 (§10.14)。迭代器块有额外的限制：

- 在迭代器块中出现 return 语句是编译时错误（但允许 yield return 语句）。
- 迭代器块包含不安全上下文 (§18.1) 是编译时错误。迭代器块始终定义安全上下文，即使其声明嵌套在不安全上下文中。

### 8.2.1 语句列表

*语句列表* 由一个或多个按顺序编写的语句组成。语句列表出现在 *块* (§8.2) 和 *switch 块* (§8.7.2) 中。

```
statement-list:
    statement
    statement-list  statement
```

语句列表的执行是通过将控制流转移到第一个语句。当且如果控制流到达某个语句的端点，则控制流转移到下一个语句。当且如果控制流到达最后一个语句的端点，则控制流转移到语句列表的端点。

语句列表中的语句在以下任一条件为真时可达：

- 该语句是第一个语句且语句列表本身可达。
- 前一个语句的端点可达。
- 该语句是有标签的语句且标签被可达的 goto 语句引用。

> VLADIMIR RESHETNIKOV 当 goto 语句放置在包含 finally 块的 try 语句的 try 或 catch 块内，且有标签的语句位于 try 语句之外，且 finally 块的端点不可达时，不适用此规则。例如：

```csharp
class C
{
    static void Main()
    {
        int x;
        try
        {
            goto A; // Reachable statement
        }
        finally
        {
            throw new System.Exception();
        }
        A: x.ToString(); // Unreachable statement
    }
}
```

如果列表中最后一个语句的端点可达，则语句列表的端点可达。

## 8.3 空语句

空语句不执行任何操作。

```
empty-statement:
    ;
```

当在需要语句的上下文中没有操作要执行时，使用空语句。



> **乔恩·斯基特** 考虑到阅读代码时很容易漏掉空语句，我想知道对于这种相对少见的需求，是否更大的语法结构会更有用。例如，下面的代码是合法的，但很可能不是本意：
> 
> ```csharp
> while (text.IndexOf("xx") != -1);
> {
>     text = text.Replace("xx", "x");
> }
> ```
> 
> while 循环的空语句被伪装得相当好。如果你在确实想要空语句时必须写成“void;”之类的内容，编译器就可以把像前一个例子那样“意外为空”的语句标记为错误。

> **杰西·利伯蒂** 乔恩的例子说明了为什么空语句应当很少出现，并且应当明确标出（尽管不一定用注释）。他示例代码中的问题可以通过遵循最佳实践来纠正：空语句要么单独占一行，要么更好的是放在完整的花括号内：
> 
> ```csharp
> while (text.IndexOf("xx") != -1)
> {
>     ;
> }
> 
> {
>     text = text.Replace("xx", "x");
> }
> ```
> 
> 现在任何程序员都不会漏掉 while 循环有一个空语句。下一组花括号的用途并不比之前更（或更不）含糊，但空白有助于避免混淆。

空语句的执行只是将控制转移到该语句的结束点。因此，如果空语句可达，那么空语句的结束点就是可达的。

当编写循环体为空的 while 语句时，可以使用空语句：

```
bool ProcessMessage() {...}
void ProcessMessages() {
    while (ProcessMessage())
        ;
}
```

此外，空语句可用于在块的右花括号“}”之前声明标签：

```
    void F() {
        ...
        if (done) goto exit;
        ...
        exit: ;
    }
```

## 8.4 带标签语句

带标签语句允许在语句前加上标签。带标签语句允许出现在块中，但不允许作为嵌入语句。

*带标签语句：*
    *标识符* : *语句*

带标签语句声明一个由标识符给出名称的标签。标签的作用域是声明该标签的整个块，包括任何嵌套块。两个同名标签具有重叠作用域是编译时错误。

可以在标签作用域内从 goto 语句（§8.9.3）引用标签。这意味着 goto 语句可以在块内以及从块内向外转移控制，但绝不能转入块内。

标签有自己的声明空间，不会与其他标识符冲突。示例

```
    int F(int x) {
        if (x >= 0) goto x;
        x = -x;
    x: return x;
    }
```

是合法的，并将名称 x 同时用作参数和标签。

带标签语句的执行完全对应于执行该标签后面的语句。

除了正常控制流提供的可达性之外，如果标签被可达的 goto 语句引用，则该带标签语句也是可达的。（例外：如果 goto 语句位于包含 finally 块的 try 内，而带标签语句位于该 try 之外，并且 finally 块的结束点不可达，那么该带标签语句从该 goto 语句不可达。）

> **埃里克·利珀特** 例如，finally 块可能总是抛出异常，在这种情况下，就会有一个可达的 goto 指向一个可能不可达的标签。

> **彼得·塞斯托夫特** 另请参见 §8.9.3 中 goto 语句讨论里的注释。

## 8.5 声明语句

声明语句声明局部变量或常量。声明语句允许出现在块中，但不允许作为嵌入语句。

```
declaration-statement:
  local-variable-declaration ;
  local-constant-declaration ;
```

### 8.5.1 局部变量声明

local-variable-declaration 声明一个或多个局部变量。

```
local-variable-declaration:
  local-variable-type local-variable-declarators
```

```
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

local-variable-declaration 的 local-variable-type 要么直接指定该声明引入的变量的类型，要么用标识符 var 表示类型应根据初始化器推断。类型后跟一个 local-variable-declarators 列表，其中每个声明符引入一个新变量。local-variable-declarator 由一个命名该变量的标识符组成，后面可选地跟一个“=”标记和一个给出该变量初始值的 local-variable-initializer。

在局部变量声明的上下文中，标识符 var 充当上下文关键字（§2.4.3）。当 local-variable-type 指定为 var 且作用域中没有名为 var 的类型时，该声明是隐式类型局部变量声明，其类型从关联的初始化器表达式的类型推断。隐式类型局部变量声明受以下限制：

- local-variable-declaration 不能包含多个 local-variable-declarator。
- local-variable-declarator 必须包含 local-variable-initializer。
- local-variable-initializer 必须是表达式。
- 初始化器表达式必须具有编译时类型。
- 初始化器表达式不能引用所声明的变量本身。

> **埃里克·利珀特** 在此特性的早期设计中，允许多个声明符是合法的。
> 
> ```
> var a = 1, b = 2.5;
> ```
> 
> 当向 C# 开发者展示这段代码时，大约一半的人说它应当与
> 
> ```
> double a = 1, b = 2.5;
> ```
> 
> 具有相同的语义。
> 
> 另一半人说它应当与
> 
> ```
> int a = 1; double b = 2.5;
> ```
> 
> 具有相同的语义。
> 
> 双方都认为自己的解释是“显然正确”的。
> 
> 当面对一种允许两种互不兼容的“显然正确”解释的语法时，通常最好的做法是完全禁止这种语法，而不是滋生混淆。

> **克里斯·塞尔斯** 我认为仅仅为了复用类型名而在同一条语句中声明多个变量也应当是非法的。

> **埃里克·利珀特** 这一限制与显式类型局部变量声明形成对比，后者确实允许初始化器引用自身。
> 
> 例如，int j = M(out j); 很奇怪，但合法。如果这个表达式是 var j = M(out j)，那么重载决策在参数类型已知之前，无法确定 M 返回的类型，因而也无法确定 j 的类型。当然，参数类型正是我们试图确定的内容。
> 
> 与其尝试解决这个“先有鸡还是先有蛋”的问题，语言规范干脆将这种情况规定为非法。

以下是不正确的隐式类型局部变量声明的示例：

```
var x; // Error: no initializer to infer type from
var y = { 1, 2, 3 }; // Error: array initializer not permitted
var z = null; // Error: null does not have a type
var u = x => x + 1; // Error: anonymous functions do not have a type
var v = v++; // Error: initializer cannot refer to variable itself
```

局部变量的值在表达式中通过简单名称（§7.6.2）获取，局部变量的值通过赋值（§7.17）修改。局部变量在获取其值的每个位置都必须明确赋值（§5.3）。

> **克里斯·塞尔斯** 我非常喜欢隐式类型局部变量声明，当类型是匿名类型时（这种情况下你不得不使用它们），或者当变量类型作为初始化它的语句的一部分被显式表明时，但不是因为你懒得打字！
> 
> 例如：
> 
> ```
> var a = new { Name = "Bob", Age = 42 }; // Good
> var b = 1; // Good
> var v = new Person(); // Good
> var d = GetPerson(); // BAD!
> ```
> 
> 编译器完全乐意把 d 当作隐式类型变量，但可怜的人类读者！




> ERIC LIPPERT 我通常同意上面的注释，但想补充一点：var 效果很好，当代码编写者试图传达“此变量的存储类型无关紧要；重要的是变量的含义，而不是其实现细节”时。例如，我经常写类似“var attributes = ParseMethodAttributes();”的代码——在这里我的意思是，返回的是 AttributeSyntax[] 还是 List<AttributeSyntax> 并不重要。重要的是属性集合已经被解析了。

> BILL WAGNER 我坦率承认自己大量使用 var 的“罪行”。事实上，我的习惯是对除简单类型之外的几乎所有内容都使用隐式类型变量。我发现对变量具有语义上的理解比语法上的理解重要得多。在 Chris 的示例中，GetPerson() 在逻辑上会返回一个 Person，或一个 IPerson，或派生自 Person 或实现 IPerson 的东西。在所有这些情况下，我都可以接受那一点模糊性。我理解“代表类似人的东西的变量”这一概念，而无需知道其确切类型。

在局部变量声明中声明的局部变量的作用域是声明所在的块。在文本位置早于该局部变量的局部变量声明符处引用局部变量是错误。在局部变量的作用域内，以相同名称声明另一个局部变量或常量是编译时错误。

声明多个变量的局部变量声明等价于多个具有相同类型的单个变量声明。此外，局部变量声明中的变量初始化器恰好对应于在声明之后立即插入的赋值语句。

示例

```
void F() {
    int x = 1, y, z = x * 2;
}
```

恰好对应于

```
void F() {
    int x; x = 1;
    int y;
    int z; z = x * 2;
}
```

在隐式类型局部变量声明中，被声明的局部变量的类型被视为与用于初始化该变量的表达式的类型相同。例如：

```
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
```

上面的隐式类型局部变量声明与以下显式类型声明完全等价：

```
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
```

> **PETER SESTOFT** 虽然可以声明局部（编译时）常量，但在 C# 中却无法声明只读局部变量或只读方法参数，这与 Standard ML 和 Java 的 val、F# 的 let 以及 Java 的 final 不同。作为一名老派函数式程序员，我觉得这有点遗憾；我经常只是想为一个值命名，而不是声明一个可变变量。using 语句（§8.13）确实允许你声明一个不可变的局部变量，但这很繁琐且不符合惯用法（因此对大多数 C# 开发者来说令人困惑），而且它仅适用于局部变量，不适用于方法参数。

## 8.5.2 本地常量声明

一个 *本地常量声明* 声明一个或多个局部常量。

```
local-constant-declaration:
    const   type   constant-declarators

constant-declarators:
    constant-declarator
    constant-declarators   ,   constant-declarator

constant-declarator:
    identifier   =   constant-expression
```

*本地常量声明* 的类型指定了声明引入的常量的类型。类型后面跟着一个 *常量声明符* 列表，每个声明符引入

一个新的常量。常量声明符由一个命名常量的标识符组成，后跟 "=" 标记，再后跟一个给出常量值的常量表达式（§7.19）。

局部常量声明的类型和常量表达式必须遵循与常量成员声明（§10.4）相同的规则。

局部常量的值在表达式中通过使用简单名称（§7.6.2）获得。

局部常量的作用域是声明所在的块。在文本位置早于其常量声明符处引用局部常量是错误。在局部常量的作用域内，以相同名称声明另一个局部变量或常量是编译时错误。

声明多个常量的局部常量声明等价于多个具有相同类型的单个常量声明。

## 8.6 表达式语句

表达式语句计算给定的表达式。表达式计算得到的值（如果有）将被丢弃。

```
expression-statement:
    statement-expression ;

statement-expression:
    invocation-expression
    object-creation-expression
    assignment
    post-increment-expression
    post-decrement-expression
    pre-increment-expression
    pre-decrement-expression
```

并非所有表达式都允许作为语句。特别是，像 x + y 和 x == 1 这样仅计算值（将被丢弃）的表达式不允许作为语句。

执行表达式语句会计算包含的表达式，然后将控制权转移到表达式语句的终点。如果该表达式语句可达，则表达式语句的终点可达。

> **JON SKEET** 偶尔有人建议允许方法声明自己为永不结束；也就是说，它们永远不会正常返回。在这种方案下，它们终止的唯一方式就是通过异常。这样的一个明显例子是单元测试库中的 Assert.Fail。

如果这样的特性出现，调用此类方法的表达式语句的终点将不可达。偶尔，这种语法可以避免需要一个你知道永远不会执行的“虚拟” return 或 throw 语句。我怀疑额外的复杂性（在语言和实现方面）大于所带来的微小好处。

> **ERIC LIPPERT** 标准化 ECMAScript 语言的委员会过去曾提出一种“never”类型，其语义与 Jon 描述的相同。我同意在 C# 中拥有它会很好，但到目前为止，成本可能超过了相对较小的收益。

## 8.7 选择语句

选择语句根据某个表达式的值从若干可能语句中选择一个执行。

```
selection-statement:
  if-statement
  switch-statement
```

### 8.7.1 if 语句

if 语句根据布尔表达式的值选择一个语句执行。

```
if-statement:
  if ( boolean-expression ) embedded-statement
  if ( boolean-expression ) embedded-statement else embedded-statement
```

else 部分与语法允许的最近的先前 if 关联。因此形式为

```
if (x) if (y) F(); else G();
```

的 if 语句等价于

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

if 语句的执行如下：

- 计算 boolean-expression（§7.20）。
- 如果布尔表达式求值为 true，则控制权转移到第一个嵌入语句。当且仅当控制权到达该语句的终点时，控制权转移到 if 语句的终点。
- 如果布尔表达式求值为 false 且存在 else 部分，则控制权转移到第二个嵌入语句。当且仅当控制权到达该语句的终点时，控制权转移到 if 语句的终点。
- 如果布尔表达式求值为 false 且不存在 else 部分，则控制权转移到 if 语句的终点。

if 语句的第一个嵌入语句可达的条件是 if 语句可达且布尔表达式不具有常量值 false。

if 语句的第二个嵌入语句（如果存在）可达的条件是 if 语句可达且布尔表达式不具有常量值 true。

if 语句的终点可达的条件是其至少一个嵌入语句的终点可达。此外，没有 else 部分的 if 语句的终点可达的条件是 if 语句可达且布尔表达式不具有常量值 true。

### 8.7.2 switch 语句

switch 语句选择具有与 switch 表达式值对应的关联 switch 标签的语句列表执行。

```
switch-statement:
    switch ( expression ) switch-block

switch-block:
    { switch-sections_opt }
```

switch-sections:
    switch-section
    switch-sections switch-section

switch-section:
    switch-labels statement-list

switch-labels:
    switch-label
    switch-labels switch-label

switch-label:
    case constant-expression :
    default :

switch-statement 由关键字 switch 组成，后跟一个圆括号表达式（称为 switch 表达式），后跟一个 switch-block。switch-block 由零个或多个用大括号括起来的 switch-sections 组成。每个 switch-section 由一个或多个 switch-labels 后跟一个 statement-list (§8.2.1) 组成。

switch 语句的控制类型由 switch 表达式确定。

- 如果 switch 表达式的类型是 sbyte、byte、short、ushort、int、uint、long、ulong、bool、char、string 或 enum-type，或是这些类型之一对应的可空类型，则该类型即为 switch 语句的控制类型。
- 否则，必须存在且仅存在一个从 switch 表达式类型到以下可能控制类型之一的用户定义隐式转换 (§6.4)：sbyte、byte、short、ushort、int、uint、long、ulong、char、string，或这些类型之一对应的可空类型。
- 否则，如果不存在此类隐式转换，或存在多个此类隐式转换，则会发生编译时错误。

每个 case 标签的常量表达式必须表示一个可隐式转换为 switch 语句控制类型的数值。如果同一个 switch 语句中两个或多个 case 标签指定了相同的常量值，则会发生编译时错误。

switch 语句中最多只能有一个 default 标签。

switch 语句的执行方式如下：

- 计算 switch 表达式并将其转换为控制类型。
- 如果同一个 switch 语句中某个 case 标签指定的常量之一等于 switch 表达式的值，则控制转移到匹配的 case 标签之后的语句列表。

## 8. 语句

- 如果同一个 switch 语句中 case 标签指定的常量均不等于 switch 表达式的值，且存在 default 标签，则控制转移到 default 标签之后的语句列表。
- 如果同一个 switch 语句中 case 标签指定的常量均不等于 switch 表达式的值，且不存在 default 标签，则控制转移到 switch 语句的结束点。

如果 switch section 的语句列表的结束点可达，则会发生编译时错误。这被称为“no fall through”规则。示例

```
```csharp
switch (i) {
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
```

是有效的，因为没有任何 switch section 具有可达的结束点。与 C 和 C++ 不同，不允许 switch section 的执行“fall through”到下一个 switch section，而示例

```
```csharp
switch (i) {
    case 0:
        CaseZero();
    case 1:
        CaseZeroOrOne();
    default:
        CaseAny();
}
```
```

会导致编译时错误。当需要让一个 switch section 的执行后跟另一个 switch section 的执行时，必须使用显式的 goto case 或 goto default 语句：

```
```csharp
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
```

switch section 中允许使用多个标签。示例

```
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
```

是有效的。该示例不违反“no fall through”规则，因为标签 case 2: 和 default: 属于同一个 switch section。

“no fall through”规则防止了 C 和 C++ 中因意外省略 break 语句而出现的一类常见错误。此外，由于该规则，switch 语句的 switch sections 可以任意重新排列而不影响语句的行为。例如，上面的 switch 语句的各个 sections 可以反转而不影响语句的行为：

```
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
```

switch section 的语句列表通常以 break、goto case 或 goto default 语句结束，但任何使语句列表结束点不可达的构造都是允许的。例如，由布尔表达式 true 控制的 while 语句已知永远不会到达其结束点。同样，throw 或 return 语句总是将控制转移到别处，永远不会到达其结束点。因此以下示例是有效的：

```
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
```

> **JON SKEET** 我在想 C# 设计者是否明智地从头重新设计 switch/case。case 中引入的变量的作用域规则有些令人惊讶，而且 break 语句也感觉不对。我认为开发者把 case 视为块——那么为什么不强制执行呢？
> 
> 同样，允许使用逗号分隔的表达式列表来让多个 case 匹配同一个块，而不是重复整个 case 标签，可能更易读。

```
case 0:
{
    // Code for case 0 goes here, with no need for a break
}
```

switch 语句的控制类型可以是 string 类型。例如：

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

如同字符串相等运算符 (§7.10.7)，switch 语句区分大小写，并且只有当 switch 表达式字符串与某个 case 标签常量完全匹配时，才会执行相应的 switch section。

当 switch 语句的控制类型为 string 时，值 null 允许作为 case 标签常量。

switch-block 的 statement-lists 中可以包含声明语句 (§8.5)。在 switch block 中声明的局部变量或常量的作用域为 switch block。

> **BILL WAGNER** 这个想法表明每个 switch block 周围隐式存在大括号。

在 switch block 内，在表达式上下文中使用的名称的含义必须始终相同 (§7.6.2.1)。

给定的 switch section 的语句列表可达的条件是 switch 语句可达，并且满足以下至少一个条件：

- switch 表达式是非常量值。
- switch 表达式是常量值，且与该 switch section 中的某个 case 标签匹配。
- switch 表达式是常量值，且与任何 case 标签都不匹配，而该 switch section 包含 default 标签。
- 该 switch section 的某个 switch 标签被可达的 goto case 或 goto default 语句引用。

> VLADIMIR RESHETNIKOV  当 goto case 或 goto default 语句位于包含 finally 块的 try 语句的 try 或 catch 块内部，且 switch 标签位于 try 语句外部，并且 finally 块的结束点不可达时，不适用此规则。

switch 语句的结束点可达的条件是满足以下至少一个条件：

- switch 语句包含一个可达的 break 语句，该语句退出 switch 语句。

> VLADIMIR RESHETNIKOV  当 break 语句位于包含 finally 块的 try 语句的 try 或 catch 块内部，且 break 语句的目标位于 try 语句外部，并且 finally 块的结束点不可达时，不适用此规则。

- switch 语句可达，switch 表达式是非常量值，且不存在 default 标签。
- switch 语句可达，switch 表达式是常量值，且与任何 case 标签都不匹配，并且不存在 default 标签。




## 8.8 迭代语句

迭代语句会重复执行嵌入语句。

```
iteration-statement:
    while-statement
    do-statement
    for-statement
    foreach-statement
```

### 8.8.1 while 语句

`while` 语句根据条件执行嵌入语句零次或多次。

```
while-statement:
    while ( boolean-expression ) embedded-statement
```

`while` 语句的执行方式如下：

- 对*布尔表达式*（§7.20）求值。
- 如果布尔表达式的结果为 true，则将控制权转移给嵌入语句。当控制权到达嵌入语句的终点时（可能是由于执行了 `continue` 语句），控制权将转移到 `while` 语句的开头。
- 如果布尔表达式的结果为 false，则将控制权转移到 `while` 语句的终点。

在 `while` 语句的嵌入语句中，可以使用 `break` 语句（§8.9.1）将控制权转移到 `while` 语句的终点（从而结束嵌入语句的迭代），也可以使用 `continue` 语句（§8.9.2）将控制权转移到嵌入语句的终点（从而执行 `while` 语句的下一次迭代）。

如果 `while` 语句可到达且布尔表达式不具有常量值 `false`，则 `while` 语句的嵌入语句可到达。

在以下至少一种情况成立时，`while` 语句的终点可到达：

- `while` 语句包含一个可到达的、退出 `while` 语句的 `break` 语句。

> ■ **弗拉基米尔·列舍特尼科夫** 当 `break` 语句位于包含 `finally` 块的 `try` 语句的 `try` 或 `catch` 块中，且 `break` 语句的目标位于该 `try` 语句之外，同时 `finally` 块的终点不可到达时，不应用此规则。

- `while` 语句可到达，且布尔表达式不具有常量值 `true`。

### 8.8.2 do 语句

`do` 语句根据条件执行嵌入语句一次或多次。

```
do-statement:
    do  embedded-statement  while  (  boolean-expression  )  ;
```

`do` 语句的执行方式如下：

- 将控制权转移给嵌入语句。
- 当控制权到达嵌入语句的终点时（可能是由于执行了 `continue` 语句），对*布尔表达式*（§7.20）求值。如果布尔表达式的结果为 true，则将控制权转移到 `do` 语句的开头；否则，将控制权转移到 `do` 语句的终点。

在 `do` 语句的嵌入语句中，可以使用 `break` 语句（§8.9.1）将控制权转移到 `do` 语句的终点（从而结束嵌入语句的迭代），也可以使用 `continue` 语句（§8.9.2）将控制权转移到嵌入语句的终点。

如果 `do` 语句可到达，则 `do` 语句的嵌入语句可到达。

在以下至少一种情况成立时，`do` 语句的终点可到达：

- `do` 语句包含一个可到达的、退出 `do` 语句的 `break` 语句。

> ■ **弗拉基米尔·列舍特尼科夫** 当 `break` 语句位于包含 `finally` 块的 `try` 语句的 `try` 或 `catch` 块中，且 `break` 语句的目标位于该 `try` 语句之外，同时 `finally` 块的终点不可到达时，不应用此规则。

- 嵌入语句的终点可到达，且布尔表达式不具有常量值 `true`。

### 8.8.3 for 语句

`for` 语句先计算一系列初始化表达式，然后在条件为 true 时，重复执行嵌入语句并计算一系列迭代表达式。

```
for-statement:
    for ( for-initializer_opt ; for-condition_opt ; for-iterator_opt ) embedded-statement
for-initializer:
    local-variable-declaration
    statement-expression-list
for-condition:
    boolean-expression
for-iterator:
    statement-expression-list
statement-expression-list:
    statement-expression
    statement-expression-list , statement-expression
```

如果存在 for-initializer，则它由局部变量声明（§8.5.1）或由逗号分隔的语句表达式列表（§8.6）组成。for-initializer 声明的局部变量的作用域从该变量的局部变量声明符开始，延伸至嵌入语句的末尾。该作用域包括 for-condition 和 for-iterator。

如果存在 for-condition，则它必须是布尔表达式（§7.20）。

如果存在 for-iterator，则它由逗号分隔的语句表达式列表（§8.6）组成。

`for` 语句的执行方式如下：

- 如果存在 for-initializer，则按照变量初始化器或语句表达式的书写顺序执行它们。此步骤只执行一次。
- 如果存在 for-condition，则对其求值。
- 如果不存在 for-condition，或者求值结果为 true，则将控制权转移给嵌入语句。当控制权到达嵌入语句的终点时（可能是由于执行了 `continue` 语句），依次计算 for-iterator（如果存在）中的表达式，然后执行下一次迭代；下一次迭代从上述步骤中的 for-condition 求值开始。
- 如果存在 for-condition 且求值结果为 false，则将控制权转移到 `for` 语句的终点。

在 `for` 语句的嵌入语句中，可以使用 `break` 语句（§8.9.1）将控制权转移到 `for` 语句的终点（从而结束嵌入语句的迭代），也可以使用 `continue` 语句（§8.9.2）将控制权转移到嵌入语句的终点（从而执行 for-iterator，并执行 `for` 语句的下一次迭代，该迭代从 for-condition 开始）。

在以下任一情况成立时，`for` 语句的嵌入语句可到达：

- `for` 语句可到达，且不存在 for-condition。
- `for` 语句可到达，且存在 for-condition，并且该条件不具有常量值 `false`。

在以下至少一种情况成立时，`for` 语句的终点可到达：

- `for` 语句包含一个可到达的、退出 `for` 语句的 `break` 语句。

> **弗拉基米尔·列舍特尼科夫** 当 `break` 语句位于包含 `finally` 块的 `try` 语句的 `try` 或 `catch` 块中，且 `break` 语句的目标位于该 `try` 语句之外，同时 `finally` 块的终点不可到达时，不应用此规则。

- `for` 语句可到达，且存在 for-condition，并且该条件不具有常量值 `true`。

### 8.8.4 foreach 语句

`foreach` 语句枚举集合中的元素，并针对集合中的每个元素执行一次嵌入语句。

```
foreach-statement:
    foreach ( local-variable-type identifier in expression ) embedded-statement
```

`foreach` 语句的类型和标识符声明该语句的迭代变量。如果将 `var` 标识符指定为 local-variable-type，且作用域内不存在名为 `var` 的类型，则该迭代变量称为隐式类型迭代变量，其类型取为下文所述的 `foreach` 语句的元素类型。迭代变量对应于一个只读局部变量，其作用域延伸至嵌入语句。在 `foreach` 语句执行期间，迭代变量表示当前正在执行迭代的集合元素。如果嵌入语句试图修改迭代变量（通过赋值或 `++` 和 `--` 运算符），或将迭代变量作为 `ref` 或 `out` 参数传递，则会发生编译时错误。




> **CHRIS SELLS** 为了可读性，应优先使用 foreach 语句而不是 for 语句。

> **JON SKEET** 事实上只有一个迭代变量（它是只读的，却在每次迭代时神奇地改变其值）导致了捕获变量中最常见的问题之一。下面的代码看起来会打印“a”、“b”、“c”、“d”，但实际上会打印四次“d”。

```csharp
List<Action> actions = new List<Action>();
foreach (string value in new[] { "a", "b", "c", "d" })
{
    actions.Add(() => Console.WriteLine(value));
}
foreach (Action action in actions)
{
    action();
}
```

> 解决方案通常是在 foreach 语句的主体内部引入一个额外的变量，该变量获取迭代变量当前值的副本。这样每个委托将捕获不同的变量。在这种情况下，第一个循环将变为

```csharp
foreach (string value in new[] { "a", "b", "c", "d" })
{
    string copy = value;
    actions.Add(() => Console.WriteLine(copy));
}
```

> **PETER SESTOFT** foreach 语句本可以被定义为不同以避免 Jon Skeet 评论中讨论的变量捕获问题：只需将 try-while-finally 展开中稍后在本节所示的 while 循环内部移动声明 `v`。事实上，在原始 C# 语言规范中，声明出现在 while 循环内部，但在 C# 2.0 的标准化过程中，事实证明在 Microsoft 的实现中至少将 `v` 声明在循环外部更接近事实，因此标准据此进行了更改。

foreach 语句的编译时处理首先确定表达式的 *集合类型*、*枚举器类型* 和 *元素类型*。此确定按如下方式进行：

- 如果 *表达式* 的类型 X 是数组类型，则存在从 X 到 `System.Collections.IEnumerable` 接口的隐式引用转换（因为 `System.Array` 实现了该接口）。*集合类型* 是 `System.Collections.IEnumerable` 接口，*枚举器类型* 是 `System.Collections.IEnumerator` 接口，而 *元素类型* 是数组类型 X 的元素类型。
- 如果 *表达式* 的类型 X 是 *动态*，则存在从 *表达式* 到 `System.Collections.IEnumerable` 接口的隐式转换（§6.1.8）。*集合类型* 是 `System.Collections.IEnumerable` 接口，*枚举器类型* 是 `System.Collections.IEnumerator` 接口。如果 *局部变量类型* 给出 *var* 标识符，则 *元素类型* 为 *动态*；否则为 *object*。
- 否则，确定类型 X 是否具有适当的 GetEnumerator 方法：
  - 在类型 X 上使用标识符 GetEnumerator 且无类型参数执行成员查找。如果成员查找未产生匹配项，或产生歧义或不是方法组的匹配项，则按如下所述检查可枚举接口。建议如果成员查找产生除方法组或无匹配项之外的任何内容，则发出警告。

> > **ERIC LIPPERT** 这种基于“pattern”的方法被指定是为了在通用 `IEnumerable<T>` 可用之前的时代，集合作者能够为其枚举器对象提供更强的类型注释。
> >
> > 非通用 `IEnumerable` 的实现总是最终装箱整数集合的每个成员，因为 Current 属性的返回类型是 object。整数集合的提供者可以提供基于非接口的 GetEnumerator、MoveNext 和 Current 实现，使得 Current 返回未装箱的整数。
> >
> > 当然，在拥有通用 `IEnumerable<T>` 的世界里，所有这些努力都变得不必要了。大多数被迭代的集合将实现此接口。

- 使用 resulting 方法组和空参数列表执行重载解析。如果重载解析未产生适用方法、产生歧义，或产生单一最佳方法但该方法为静态或非公共，则按如下所述检查可枚举接口。建议如果重载解析产生除无歧义的公共实例方法或无适用方法之外的任何内容，则发出警告。
- 如果 GetEnumerator 方法的返回类型 E 不是类、结构或接口类型，则产生错误且不再进行后续步骤。

- 在 E 上使用标识符 Current 且无类型参数执行成员查找。如果成员查找未产生匹配项，结果为错误，或结果除允许读取的公共实例属性外为任何其他内容，则产生错误且不再进行后续步骤。
- 在 E 上使用标识符 MoveNext 且无类型参数执行成员查找。如果成员查找未产生匹配项，结果为错误，或结果除方法组外为任何其他内容，则产生错误且不再进行后续步骤。
- 对方法组使用空参数列表执行重载解析。如果重载解析未产生适用方法、产生歧义，或产生单一最佳方法但该方法为静态或非公共，或其返回类型不是 bool，则产生错误且不再进行后续步骤。
- *集合类型* 为 X，*枚举器类型* 为 E，*元素类型* 为 Current 属性的类型。
- 否则，检查可枚举接口：
  - 如果恰好存在一个类型 T，使得存在从 X 到接口 System.Collections.Generic.IEnumerable<T> 的隐式转换，则 *集合类型* 为此接口，*枚举器类型* 为接口 System.Collections.Generic.IEnumerator<T>，*元素类型* 为 T。
  - 否则，如果存在多个此类类型 T，则产生错误且不再进行后续步骤。
  - 否则，如果存在从 X 到 System.Collections.IEnumerable 接口的隐式转换，则 *集合类型* 为此接口，*枚举器类型* 为接口 System.Collections.IEnumerator，*元素类型* 为 object。
  - 否则，产生错误且不再进行后续步骤。

> > **PETER SESTOFT** 不幸的是，foreach 语句的编译时处理意味着它相当动态类型化。例如，对于任意非密封类 C 和接口 I，以下内容在类型上是正确的，并且不会产生任何编译器警告或错误：

```csharp
C[] xs = ...;
foreach (I x in xs)
...
```

> > 事实上，最近我就在移除一个看似无关的接口 I 从类 C 的接口列表时落入了这个陷阱。项目在构建阶段没有错误通过，但在运行时应用程序因 InvalidCastException 而崩溃，因为我忽略了几个 foreach 语句。实际上，这种行为是可以预期的，因为 C 的某个子类可能实现了接口 I。或许更令人惊讶的是，I 和 C 可以在前面的代码中互换而结果相同。

如果上述步骤成功，则会明确地产生 *集合类型* C、*枚举器类型* E 和 *元素类型* T。形式为的 foreach 语句

`foreach (V v in x) embedded-statement`

然后展开为：

```csharp
{
    E e = ((C)(x)).GetEnumerator();
    try {
        V v;
        while (e.MoveNext()) {
            v = (V)(T)e.Current;
            embedded-statement
        }
    }
    finally {
        ... // Dispose of e
    }
}
```

变量 e 不对表达式 x、嵌入语句或程序的任何其他源代码可见或可访问。变量 v 在嵌入语句中为只读。如果不存在从 T（*元素类型*）到 V（foreach 语句中的 *局部变量类型*）的显式转换（§6.2），则产生错误且不再进行后续步骤。如果 x 的值为 null，则在运行时抛出 System.NullReferenceException。

> > **MAREK SAFAR** foreach 语句是语言演进的经典示例。C# 1.0 没有通用的 IEnumerable<T>，必须从元素类型到局部变量使用显式转换。C# 2.0 引入了具有泛型元素类型的 foreach 语句的泛型版本。C# 3.0 通过引入 *隐式类型迭代变量* 将此结构带回了本应开始的地方，这使显式转换变为隐式，并避免了执行期间的任何 InvalidCastException。



An implementation is permitted to implement a given foreach statement differently—for example, for performance reasons—as long as the behavior is consistent with the above expansion.

The body of the finally block is constructed according to the following steps:

- If there is an implicit conversion from E to the System.IDisposable interface, then
  - If E is a non-nullable value type, then the finally clause is expanded to the semantic equivalent of

    ```csharp
    finally {
        ((System.IDisposable)e).Dispose();
    }
    ```

  - Otherwise, the finally clause is expanded to the semantic equivalent of

    ```csharp
    finally {
        if (e != null) ((System.IDisposable)e).Dispose();
    }
    ```

    except that if E is a value type, or a type parameter instantiated to a value type, then the cast of e to System.IDisposable will not cause boxing to occur.

- Otherwise, if E is a sealed type, then the finally clause is expanded to an empty block:

  ```csharp
  finally {
  }
  ```

- Otherwise, the finally clause is expanded to

  ```csharp
  finally {
      System.IDisposable d = e as System.IDisposable;
      if (d != null) d.Dispose();
  }
  ```

The local variable d is not visible to or accessible to any user code. In particular, it does not conflict with any other variable whose scope includes the finally block.

> **JON SKEET** The fact that the foreach statement disposes of its iterator makes the iterator blocks in C# 2.0 vastly more useful than they otherwise would be: It is entirely reasonable to acquire a resource to iterate over, and then dispose of that resource when either the iterator has been exhausted or the caller breaks out of the loop for some reason.

The order in which foreach traverses the elements of an array is as follows: For single-dimensional arrays, elements are traversed in increasing index order, starting with index 0 and ending with index Length - 1. For multi-dimensional arrays, elements are traversed such that the indices of the rightmost dimension are increased first, then the next left dimension, and so on to the left.

The following example prints out each value in a two-dimensional array, in element order:

```csharp
using System;
class Test
{
    static void Main()
    {
        double[,] values = {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };
        foreach (double elementValue in values)
        {
            Console.Write("{0} ", elementValue);
        }
        Console.WriteLine();
    }
}
```

The output produced is as follows:

```
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

In the example

```csharp
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
```

The type of n is inferred to be int, the element type of numbers.

## 8.9 Jump Statements

Jump statements unconditionally transfer control.

- jump-statement:
  - break-statement
  - continue-statement
  - goto-statement
  - return-statement
  - throw-statement

The location to which a jump statement transfers control is called the *target* of the jump statement.

When a jump statement occurs within a block, and the target of that jump statement is outside that block, the jump statement is said to *exit* the block. While a jump statement may transfer control out of a block, it can never transfer control into a block.

Execution of jump statements is complicated by the presence of intervening *try* statements. In the absence of such *try* statements, a jump statement unconditionally transfers control from the jump statement to its target. In the presence of such intervening *try* statements, execution is more complex. If the jump statement exits one or more *try* blocks with associated *finally* blocks, control is initially transferred to the *finally* block of the innermost *try* statement. When and if control reaches the end point of a *finally* block, control is transferred to the *finally* block of the next enclosing *try* statement. This process is repeated until the *finally* blocks of all intervening *try* statements have been executed.

In the example

```csharp
using System;
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
            Console.WriteLine("After break");
        }
    }
}
```

The *finally* blocks associated with two *try* statements are executed before control is transferred to the target of the jump statement.

The output produced is as follows:

```
Before break
Innermost finally block
Outermost finally block
After break
```

### 8.9.1 The break Statement

The break statement exits the nearest enclosing switch, while, do, for, or foreach statement.

```csharp
break-statement:
    break ;
```

The target of a break statement is the end point of the nearest enclosing switch, while, do, for, or foreach statement. If a break statement is not enclosed by a switch, while, do, for, or foreach statement, a compile-time error occurs.

When multiple switch, while, do, for, or foreach statements are nested within each other, a break statement applies only to the innermost statement. To transfer control across multiple nesting levels, a goto statement (§8.9.3) must be used.

A break statement cannot exit a finally block (§8.10). When a break statement occurs within a finally block, the target of the break statement must be within the same finally block; otherwise, a compile-time error occurs.

A break statement is executed as follows:

- If the break statement exits one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all intervening try statements have been executed.
- Control is transferred to the target of the break statement.

Because a break statement unconditionally transfers control elsewhere, the end point of a break statement is never reachable.

> **JESSE LIBERTY** Whenever you see unconditional transfer or (especially) exit from within the flow of a method, treat it as a volatile explosive (that is, run screaming from the room).
>
> While a case can be made for break, continue, and goto statements, it is rare that you can't rewrite or refactor them out of existence. The resulting code is very likely to be easier to read, understand, and maintain.

### 8.9.2 The continue Statement

The continue statement starts a new iteration of the nearest enclosing while, do, for, or foreach statement.

```csharp
continue-statement:
    continue ;
```

The target of a continue statement is the end point of the embedded statement of the nearest enclosing while, do, for, or foreach statement. If a continue statement is not enclosed by a while, do, for, or foreach statement, a compile-time error occurs.

When multiple while, do, for, or foreach statements are nested within each other, a continue statement applies only to the innermost statement. To transfer control across multiple nesting levels, a goto statement (§8.9.3) must be used.

A continue statement cannot exit a finally block (§8.10). When a continue statement occurs within a finally block, the target of the continue statement must be within the same finally block; otherwise, a compile-time error occurs.

A continue statement is executed as follows:

- If the continue statement exits one or more try blocks with associated finally blocks, control is initially transferred to the finally block of the innermost try statement. When and if control reaches the end point of a finally block, control is transferred to the finally block of the next enclosing try statement. This process is repeated until the finally blocks of all intervening try statements have been executed.
- Control is transferred to the target of the continue statement.

Because a continue statement unconditionally transfers control elsewhere, the end point of a continue statement is never reachable.

> **PETER SESTOFT** Some languages—notably the Java programming language—have generalized versions of the break and continue statements, where a target label specifies which of multiple enclosing loops should be exited or resumed. The same effect can be obtained in C# using the goto statement. Moreover, although the generalized break and continue statements are disciplined versions of goto, they are almost as difficult to understand as goto statements and, in my opinion, detrimental to readability even in short programs. See examples 78 and 79 in my book *Java Precisely*, second edition.



## 8.9.3 goto 语句

goto 语句将控制转移到由标签标记的语句。

```
goto-statement:
    goto identifier ;
    goto case constant-expression ;
    goto default ;
```

goto identifier 语句的目标是带有给定标签的带标签语句。如果当前函数成员中不存在具有给定名称的标签，或者 goto 语句不在该标签的作用域内，则发生编译时错误。此规则允许使用 goto 语句将控制转移到嵌套作用域之外，但不允许转入嵌套作用域。在示例

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
            int row, col;
            for (row = 0; row <= 1; ++row)
                for (col = 0; col <= 2; ++col)
                    if (str == table[row,col])
                        goto done;
            Console.WriteLine("{0} not found", str);
            continue;
        done:
            Console.WriteLine("Found {0} at [{1}][{2}]", str, row, col);
    }
}
```

中使用 goto 语句将控制转移到嵌套作用域之外。

goto case 语句的目标是直接封闭的 switch 语句（§8.7.2）中的语句列表，该 switch 语句包含具有给定常量值的 case 标签。如果 goto case 语句未被 switch 语句包围，如果常量表达式不能隐式转换（§6.1）为最近封闭 switch 语句的控制类型，或者如果最近封闭的 switch 语句不包含具有给定常量值的 case 标签，则发生编译时错误。

goto default 语句的目标是直接封闭的 switch 语句（§8.7.2）中的语句列表，该 switch 语句包含 default 标签。如果 goto default 语句未被 switch 语句包围，或者如果最近封闭的 switch 语句不包含 default 标签，则发生编译时错误。

goto 语句不能退出 finally 块（§8.10）。当 goto 语句出现在 finally 块内时，goto 语句的目标必须位于同一 finally 块内；否则发生编译时错误。

> BILL WAGNER 这些规则使 goto 在 C# 中不那么纯粹邪恶，但我还没见过它的良好用途。

goto 语句的执行方式如下：

- 如果 goto 语句退出一个或多个带有相关联 finally 块的 try 块，控制最初转移到最内层 try 语句的 finally 块。当控制到达 finally 块的结束点（如果到达），控制转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有中间 try 语句的 finally 块都已执行。
- 控制转移到 goto 语句的目标。

因为 goto 语句无条件将控制转移到别处，goto 语句的结束点永远不可到达。

> CHRIS SELLS 请不要使用标签或 goto 语句。我从未读过任何代码是去掉它们后不会更可读的。

> CHRISTIAN NAGEL 尽管 goto 语句在 switch 语句中作为显式贯穿选项是有意义的，但不应在其他场景中使用它们。

> PETER SESTOFT Don Knuth 1974 年的论文“Structured Programming with go to Statements”深入阐明了 goto 语句的替代方案，并指出了 goto 语句的合理用途。最终，Knuth 确实得出结论：“我们确实应该废除 go to……至少作为训练人们更仔细地表述其抽象概念的一项实验。”仅该论文的致谢名单就呈现了编程语言先驱的“名人录”。

> 在 C# 中包含 goto 的最好理由可能是你可能想生成使用 goto 的代码——例如，解析器、词法分析器、自动机、状态图、虚拟机及类似程序。

## 8.9.4 return 语句

return 语句将控制返回给出现该 return 语句的函数成员的调用方。

```
return-statement:
    return expression_opt ;
```

不带表达式的 return 语句只能用于不计算值的函数成员中——即返回类型为 void 的方法、属性或索引器的 set 访问器、事件的 add 和 remove 访问器、实例构造函数、静态构造函数或析构函数。

带表达式的 return 语句只能用于计算值的函数成员中——即返回类型非 void 的方法、属性或索引器的 get 访问器，或用户定义运算符。必须存在从表达式类型到包含该 return 语句的函数成员返回类型的隐式转换（§6.1）。

> > **VLADIMIR RESHETNIKOV** 如果 return 语句位于匿名函数内，则改为应用 §6.5 中的规则。

return 语句出现在 finally 块（§8.10）中是编译时错误。

return 语句执行如下：

- 如果 return 语句指定表达式，则计算该表达式，并通过隐式转换将结果值转换为包含该 return 语句的函数成员的返回类型。转换结果成为返回给调用方的值。
- 如果 return 语句被一个或多个带有相关联 finally 块的 try 块包围，控制最初转移到最内层 try 语句的 finally 块。当控制到达 finally 块的结束点（如果到达），控制转移到下一个封闭 try 语句的 finally 块。重复此过程，直到所有封闭 try 语句的 finally 块都已执行。
- 控制返回给包含该 return 语句的函数成员的调用方。

因为 return 语句无条件将控制转移到别处，return 语句的结束点永远不可到达。

## 8.9.5 throw 语句

throw 语句引发异常。

```
throw-statement:
    throw expression_opt ;
```

带表达式的 throw 语句引发通过计算该表达式产生的值。该表达式必须表示 System.Exception 类类型的值、从 System.Exception 派生的类类型的值，或有效基类为 System.Exception（或其子类）的类型参数类型的值。如果表达式求值产生 null，则改为引发 System.NullReferenceException。

> **PETER SESTOFT** 因此，在 C# 中引发的异常永远不会为 null，因此，§8.10 中描述的（基于其类）对异常的 try-catch 匹配是有意义的。事实上，.NET/CLI 中间语言中名为 throw 的指令在这方面表现得就像 C# 的 throw 语句。因此，即使异常是由用另一种 .NET/CLI 语言编写的代码引发的，当由 try-catch 语句处理时，它也将是非 null 的。

不带表达式的 throw 语句只能在 catch 块中使用，在这种情况下，该语句会重新引发该 catch 块当前正在处理的异常。

> **VLADIMIR RESHETNIKOV** 不带表达式的 throw 语句不允许出现在 finally 块或嵌套在最近封闭的 catch 块内的匿名函数中：

```csharp
delegate void F();
class Program
{
    static void Main()
    {
        try
        {
        }
        catch
        {
            F f = () => { throw; }; // Error CS8156
            try
            {
            }
            finally
            {
                throw;          // Error CS0724
            }
        }
    }
}
```

因为 throw 语句无条件将控制转移到别处，throw 语句的结束点永远不可到达。

当引发异常时，控制转移到可处理该异常的封闭 try 语句中的第一个 catch 子句。从异常引发点发生到将控制转移到合适的异常处理程序所发生的过程称为*异常传播*。异常传播包括重复计算以下步骤，直到找到匹配该异常的 catch 子句。在此描述中，*引发点*最初是引发异常的位置。

- 在当前函数成员中，检查每个包围引发点的 try 语句。对于每个语句 S，从最内层 try 语句开始到最外层 try 语句结束，计算以下步骤：
  - 如果 S 的 try 块包围引发点，并且 S 有一个或多个 catch 子句，则按出现顺序检查 catch 子句，以找到适合该异常的处理程序。第一个指定异常类型或异常类型的基类型的 catch 子句被视为匹配。一般 catch 子句（§8.10）被视为匹配任何异常类型。如果找到匹配的 catch 子句，则通过将控制转移到该 catch 子句的块来完成异常传播。
  - 否则，如果 S 的 try 块或 catch 块包围引发点，并且 S 有 finally 块，则控制转移到 finally 块。如果 finally 块引发另一个异常，则终止当前异常的处理。否则，当控制到达 finally 块的结束点时，继续处理当前异常。
- 如果在当前函数成员调用中未找到异常处理程序，则终止该函数成员调用。然后对调用该函数成员的调用方重复上述步骤，其引发点对应于调用该函数成员的语句。
- 如果异常处理终止当前线程中的所有函数成员调用，表明该线程没有该异常的处理程序，则线程本身终止。这种终止的影响由实现定义。

> > **BILL WAGNER** 此过程意味着你应该在所有线程的最顶层方法中执行一些基本清理。否则，在异常导致线程终止时，应用程序的行为将是未定义的。



## 8.10 try 语句

try 语句提供了一种机制，用于捕获在块执行期间发生的异常。此外，try 语句还提供了指定一个代码块的能力，当控制离开 try 语句时，该代码块总是会执行。

```
try-statement:
    try block catch-clauses
    try block finally-clause
    try block catch-clauses finally-clause

catch-clauses:
    specific-catch-clauses general-catch-clause_opt
    specific-catch-clauses_opt general-catch-clause

specific-catch-clauses:
    specific-catch-clause
    specific-catch-clauses specific-catch-clause

specific-catch-clause:
    catch ( class-type identifier_opt ) block

general-catch-clause:
    catch block

finally-clause:
    finally block
```

try 语句有三种可能的形式：

- 一个 try 块后跟一个或多个 catch 块。
- 一个 try 块后跟一个 finally 块。
- 一个 try 块后跟一个或多个 catch 块，再后跟一个 finally 块。

当 catch 子句指定 class-type 时，该类型必须是 System.Exception、从 System.Exception 派生的类型，或有效基类为 System.Exception（或其子类）的类型参数类型。

当 catch 子句同时指定 class-type 和标识符时，会声明一个具有给定名称和类型的异常变量。该异常变量对应于一个局部变量，其作用域覆盖 catch 块。在执行 catch 块期间，异常变量表示当前正在处理的异常。为了进行明确赋值检查，异常变量在其整个作用域内被视为已明确赋值。

除非 catch 子句包含异常变量名，否则无法在 catch 块中访问异常对象。

既不指定异常类型也不指定异常变量名的 catch 子句称为通用 catch 子句。一个 try 语句只能有一个通用 catch 子句，如果存在，它必须是最后一个 catch 子句。

某些编程语言可能支持无法表示为从 System.Exception 派生的对象的异常，尽管此类异常永远无法由 C# 代码生成。通用 catch 子句可用于捕获此类异常。因此，通用 catch 子句在语义上不同于指定 System.Exception 类型的 catch 子句，因为前者还可以捕获来自其他语言的异常。

> **埃里克·利珀特**
>
> 在当前 Microsoft 的 C# 和 CLR 实现中，默认情况下，抛出的不派生自 Exception 的对象会被转换为 RuntimeWrappedException 对象。因此，catch (Exception e) 会捕获所有异常。
>
> 如果要禁用此行为并使用 C# 1.0 语义（即其他语言抛出的非 Exception 对象不会以这种方式被捕获），请使用以下程序集特性：
>
> ```
> [assembly:System.Runtime.CompilerServices.RuntimeCompatibility(WrapNonExceptionThrows = false)]
> ```

为了定位异常的处理程序，catch 子句按词法顺序检查。如果 catch 子句指定的类型与同一 try 块的较早 catch 子句中指定的类型相同或派生自该类型，则会发生编译时错误。如果没有此限制，就可能编写出不可达的 catch 子句。

在 catch 块内，可以使用不带表达式的 throw 语句（§8.9.5）重新引发该 catch 块捕获的异常。对异常变量的赋值不会改变重新引发的异常。

在示例

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
            throw;                  // Rethrow
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

中，方法 F 捕获一个异常，向控制台写入一些诊断信息，修改异常变量，并重新引发该异常。重新引发的异常是原始异常，因此产生的输出为

```
Exception in F: G
Exception in Main: G
```

如果第一个 catch 块抛出 e 而不是重新引发当前异常，则产生的输出将如下所示：

```
Exception in F: G
Exception in Main: F
```

对于 break、continue 或 goto 语句将控制转移出 finally 块，属于编译时错误。当 break、continue 或 goto 语句出现在 finally 块中时，该语句的目标必须位于同一个 finally 块内；否则，会发生编译时错误。

`return` 语句出现在 `finally` 块中属于编译时错误。

`try` 语句的执行方式如下：

- 控制转移到 `try` 块。
- 当控制到达 `try` 块的结束点（如果到达）时：
  - 如果 `try` 语句有 `finally` 块，则执行 `finally` 块。
  - 控制转移到 `try` 语句的结束点。
- 如果在执行 `try` 块期间有异常传播到 `try` 语句：
  - 按出现顺序检查 `catch` 子句（如果有），以定位适合该异常的处理程序。第一个指定异常类型或该异常类型的基类型的 `catch` 子句被视为匹配。通用 `catch` 子句被视为匹配任何异常类型。如果找到匹配的 `catch` 子句：
    - 如果匹配的 `catch` 子句声明了异常变量，则将异常对象赋给该异常变量。
    - 控制转移到匹配的 `catch` 块。
- 当控制到达 `catch` 块的结束点（如果到达）时：
  - 如果 `try` 语句有 `finally` 块，则执行 `finally` 块。
  - 控制转移到 `try` 语句的结束点。
- 如果在执行 `catch` 块期间有异常传播到 `try` 语句：
  - 如果 `try` 语句有 `finally` 块，则执行 `finally` 块。
  - 异常传播到下一个封闭的 `try` 语句。
- 如果 `try` 语句没有 `catch` 子句，或者没有 `catch` 子句匹配该异常：
  - 如果 `try` 语句有 `finally` 块，则执行 `finally` 块。
  - 异常传播到下一个封闭的 `try` 语句。

> **埃里克·利珀特**
>
> 如果调用堆栈包含由其他语言（如 Visual Basic）编写的 try-catch 块保护的代码，则运行环境可能会执行“异常筛选器”，以查看给定的 catch 块是否适合所引发的异常。因此，用户代码可能会在异常引发之后、关联的 finally 块执行之前执行。如果你的异常处理代码依赖于在任何其他用户代码运行之前由 finally 块使全局状态保持一致，那么你应采取适当措施，确保你的代码在运行环境执行堆栈中可能存在的用户定义异常筛选器之前捕获异常。

当控制离开 try 语句时，finally 块的语句总是会执行。无论控制转移是正常执行的结果、执行 break、continue、goto 或 return 语句的结果，还是将异常从 try 语句传播出去的结果，都是如此。

如果在执行 finally 块期间引发异常，并且未在同一 finally 块内捕获，则该异常会传播到下一个封闭的 try 语句。如果当时正在传播另一个异常，则该异常会丢失。传播异常的过程在 throw 语句（§8.9.5）的描述中进一步讨论。

> **比尔·瓦格纳**
>
> 此行为使得以防御性方式编写 finally 子句非常重要，以避免引发第二个异常。

> **乔恩·斯基特**
>
> 当然，如果我们不必以防御性方式编写 finally 子句，那就太好了。.NET Framework 中已经通过“内部异常”的概念体现了由一个错误导致另一个错误的思想。即便如此，两个异常可能相关，但并不知道其中一个导致另一个，这种想法目前还没有常见的表示方式。同样，还有一个普遍棘手的问题：一个方法可能引发哪些异常。Java 试图用“受检异常”来解决这个问题——在我看来，大多不成功。
>
> 有时感觉我们（作为一个行业）在成功场景上已经相当擅长，但在错误处理方面还有很长的路要走。




**try** 语句的 **try** 块在 **try** 语句可达时可达。

**try** 语句的 **catch** 块在 **try** 语句可达时可达。

**try** 语句的 **finally** 块在 **try** 语句可达时可达。

**try** 语句的结束点在以下两个条件都为真时可达：

- **try** 块的结束点可达，或至少一个 **catch** 块的结束点可达。
- 如果存在 **finally** 块，则 **finally** 块的结束点可达。

## 8.11 checked 和 unchecked 语句

**checked** 和 **unchecked** 语句用于控制整数类型算术运算和转换的 *overflow* 检查上下文。

```
checked-statement:
    checked block

unchecked-statement:
    unchecked block
```

**checked** 语句导致 *block* 中的所有表达式都在 **checked** 上下文中求值。**unchecked** 语句导致 *block* 中的所有表达式都在 **unchecked** 上下文中求值。

**checked** 和 **unchecked** 语句与 **checked** 和 **unchecked** 运算符 (§7.6.12) 完全等价，只是它们操作的是块而不是表达式。

## 8.12 lock 语句

**lock** 语句为给定对象获取互斥锁，执行一条语句，然后释放锁。

```
lock-statement:
    lock ( expression ) embedded-statement
```

**lock** 语句的表达式必须表示已知为 *reference-type* 的类型的值。**lock** 语句的表达式永远不会执行隐式装箱转换 (§6.1.7)，因此表达式表示值类型的值是编译时错误。

形式为的 lock 语句

```
lock (x) ...
```

其中 x 是 reference-type 的表达式，精确等价于

```
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, __lockWasTaken);
    ...
}
finally {
    if (__lockWasTaken) System.Threading.Monitor.Exit(x);
}
```

只是 x 只被求值一次。

> **BILL WAGNER** lock() 语句提供了额外的编译器检查，以防止尝试锁定值类型。

在持有互斥锁期间，同一执行线程中执行的代码也可以获取和释放锁。然而，在其他线程中执行的代码在锁被释放之前会被阻止获取锁。

为了同步对静态数据的访问而锁定 System.Type 对象是不推荐的。其他代码可能锁定在同一类型上，这可能导致死锁。更好的方法是，通过锁定私有静态对象来同步对静态数据的访问。例如：

```
class Cache
{
    private static readonly object synchronizationObject = new object();
    public static void Add(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }

    public static void Remove(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }
}
```

> **JOSEPH ALBAHARI** 在编写供公众使用的库时，一个好的策略是使静态函数从一开始就是线程安全的（通常通过在函数内部实现锁定，如本例所示）。对于使用者来说，在调用静态方法或属性周围加锁要困难得多（甚至不可能），因为他们不知道函数是从哪些其他位置调用的。

## 8.13 using 语句

using 语句获取一个或多个资源，执行一条语句，然后释放该资源。

> **ERIC LIPPERT** 规范在此明确指出，using 语句的要点是确保 *resource* 的获取和及时释放。通常，这将包括来自操作系统的某些非托管资源，例如文件句柄。尽快停止使用资源是礼貌的；当你使用完它时，其他程序可能想要读取该文件。我不建议使用 using 语句来强制执行程序不变量。例如，有时人们会看到这样的代码：
>
> ```csharp
> using(new TemporarilyStopReportingErrors()) AttemptSomething();
> ```
>
> 这里 TemporarilyStopReportingErrors 是一个类型，其构造函数作为副作用关闭错误报告，而其释放方法将其重新打开。我认为这种（不幸地广泛存在）的做法是对 using 语句的滥用；程序副作用不是资源，在构造函数和释放器中引起全局副作用似乎是个坏主意。我会改用 try-finally 结构编写此代码。

```
using-statement:
    using ( resource-acquisition ) embedded-statement

resource-acquisition:
    local-variable-declaration
    expression
```

*resource* 是一个实现 System.IDisposable 的类或结构体，其中包含一个名为 Dispose 的单个无参数方法。使用资源的代码可以调用 Dispose 来表示资源不再需要。如果未调用 Dispose，则由于垃圾回收，最终会自动释放。

> **JOSEPH ALBAHARI** 调用 Dispose 以任何方式都不影响垃圾回收：对象在（且仅在）没有其他对象引用它时才有资格进行自动垃圾回收。同样，垃圾回收也不影响释放：除非你编写了一个显式进行此调用的终结器（析构函数），否则垃圾收集器不会调用 Dispose。
>
> Dispose 方法中最常执行的两个活动是释放非托管资源以及对其他被引用或“拥有”的对象调用 Dispose。也可以在终结器内部释放非托管资源，尽管这种操作意味着要等待不确定的时间让垃圾收集器触发。这就是为什么存在 IDisposable。

如果 *resource-acquisition* 的形式是 *local-variable-declaration*，则 *local-variable-declaration* 的类型必须是 dynamic 或可以隐式转换为 `System.IDisposable` 的类型。如果 *resource-acquisition* 的形式是 *expression*，则该表达式必须可以隐式转换为 `System.IDisposable`。

在 *resource-acquisition* 中声明的局部变量是只读的，并且必须包含初始值设定项。如果嵌入语句尝试修改这些局部变量（通过赋值或 ++ 和 -- 运算符）、获取它们的地址或将它们作为 ref 或 out 参数传递，则会发生编译时错误。

using 语句被翻译为三个部分：获取、使用和释放。资源的使用被隐式包含在包含 finally 子句的 try 语句中。此 finally 子句释放资源。如果获取到 null 资源，则不会调用 Dispose，也不会抛出异常。如果资源的类型为 dynamic，则在获取期间通过隐式动态转换 (§6.1.8) 动态转换为 IDisposable，以确保在进行使用和释放之前转换成功。

形式为的 using 语句

```
using (ResourceType resource = expression) statement
```

对应于三种可能的展开之一。当 ResourceType 是非可空值类型时，展开为

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

否则，当 ResourceType 是可空值类型或除 dynamic 之外的引用类型时，展开为

```
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        if (resource != null) ((IDisposable)resource).Dispose();
    }
}
```

否则，当 ResourceType 为 dynamic 时，展开为

```
{
    ResourceType resource = expression;
    IDisposable d = (IDisposable)resource;
    try {
        statement;
    }
    finally {
        if (d != null) d.Dispose();
    }
}
```

在任何展开中，资源变量在嵌入语句中都是只读的，而 d 变量在嵌入语句中不可访问且对嵌入语句不可见。

> **PETER SESTOFT** 感谢上述规则，using 语句也可以（被）用于以这种风格声明只读局部变量：
>
> ```csharp
> using (MyClass v = ...)
> using (MyStruct s = ...) {
>     ...
> }
> ```
>
> 事实上，这是在 C# 中声明不可变局部变量的唯一方法，但它很丑陋且奇怪。而且，它仅适用于实现 IDisposable 接口的类型 MyClass 和 MyStruct，而不适用于 int 和 string 等。例如，从语言设计的角度来看，也许令人困惑的是，与 struct 类型的只读字段 (§10.5.2 和 §7.6.4) 不同，struct 类型 MyStruct 的不可变资源变量 s 被视为变量，而不是值。因此，方法调用 s.SetX() 作用于存储在 s 中的结构体，而不是它的副本。总的来说，这种行为表明在 C# 中声明不可变局部变量和参数的机制是存在的，但遗憾的是并不以可用的形式存在。



实现可以以不同的方式实现给定的 using 语句——例如出于性能原因——只要行为与上述展开一致。

A using statement of the form

```
using (expression) statement
```

具有相同的三种可能的展开形式，但在这种情况下 ResourceType 隐式为表达式的编译时类型，并且资源变量在嵌入语句中不可访问，也对嵌入语句不可见。

> **JON SKEET** 我通常坚持在所有内容周围使用大括号——这种偏好通常也扩展到 using 语句。然而，如果你获取多种类型的多个资源（需要多个 using 语句），你可以用一组大括号将它们嵌套：
> 
> ```
> using (TextWriter output = File.CreateText("log.txt"))
> using (TextReader input = File.OpenText("log.txt")) {
>     // Copy contents from one to the other
> }
> ```
> 
> 这可以显著减少所需的缩进层级，使代码更易读。

当资源获取采用局部变量声明的形式时，可以获取给定类型的多个资源。A using statement of the form

```
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) statement
```

的 using 语句与一系列嵌套的 using 语句完全等价：

```
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```

下面的示例创建一个名为 log.txt 的文件并向文件中写入两行文本。然后示例打开同一个文件进行读取并将包含的行复制到控制台。

```csharp
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

由于 TextWriter 和 TextReader 类实现了 IDisposable 接口，示例可以使用 using 语句确保在写入或读取操作后底层文件被正确关闭。

> **CHRIS SELLS** 你几乎总是应该将 using 块包裹在你获取的任何实现 IDisposable 的资源周围（除非你在方法调用之间保留该对象）。尽管 .NET 垃圾回收器在释放内存资源方面做得非常出色，但所有其他资源都由你管理。同样，编译器在为你生成正确的释放代码方面做得非常出色，但只有当你将资源分配包裹在 using 块中时才会如此。

## 8.14 yield 语句

> **BILL WAGNER** yield return 和 yield break 语句似乎是 C# 语言中最被低估的两个语句。当你编写处理数据序列的算法时，它们非常有用。生成序列、过滤序列、组合序列以及其他算法都是使用这些语句构建的。事实上，大多数 LINQ to Objects 都是使用 yield 语句构建的。
> 
> 如果你还不熟悉这些技术，你应该花时间将这种技术作为日常开发实践的一部分。

> **CHRIS SELLS** 我同意 Bill 的观点。我直到看到有人写出这样的代码才意识到 `yield return` 有多么有用：

```
IEnumerable<int> GetSomeNumbers() {
    yield return 1;
    yield return 2;
    yield return 3;
}
```

如果你能理解这一点以及编译器为实现这一点所做的工作，你会发现自己使用这个功能会更多。

yield 语句用于迭代器块（§8.2）中，将值传递给迭代器的枚举器对象（§10.14.4）或可枚举对象（§10.14.5），或表示迭代结束。

```
yield-statement:
    yield return expression ;
    yield break ;
```

请注意 yield 不是保留字；它只有在使用 return 或 break 关键字之前时才具有特殊含义。在其他上下文中，yield 可以用作标识符。

yield 语句可以出现的位置有若干限制，如以下列表所述：

- 在方法体、运算符体或访问器体之外出现 yield 语句（任一形式）是编译时错误。
- 在匿名函数内部出现 yield 语句（任一形式）是编译时错误。
- 在 try 语句的 finally 子句中出现 yield 语句（任一形式）是编译时错误。
- 在包含任何 catch 子句的 try 语句中的任何位置出现 yield return 语句是编译时错误。

下面的示例显示了一些有效和无效的 yield 语句用法。

```
delegate IEnumerable<int> D();

IEnumerator<int> GetEnumerator() {
    try {
        yield return 1;  // Okay
        yield break;     // Okay
    }
}
finally {
    yield return 2;  // Error: yield in finally
    yield break;     // Error: yield in finally
}
try {
    yield return 3;  // Error: yield return in try...catch
    yield break;     // Okay
}
catch {
    yield return 4;  // Error: yield return in try...catch
    yield break;     // Okay
}

D d = delegate {
    yield return 5;  // Error: yield in an anonymous function
};
int MyMethod() {
    yield return 1;  // Error: wrong return type for an
                     // iterator block
}
```

yield return 语句中表达式的类型必须存在到迭代器的 yield 类型（§10.14.3）的隐式转换（§6.1）。

yield return 语句按如下方式执行：

- 语句中给出的表达式被求值，隐式转换为 yield 类型，并赋给枚举器对象的 Current 属性。
- 迭代器块的执行被挂起。如果 yield return 语句位于一个或多个 try 块内，则相关的 finally 块此时不会执行。
- 枚举器对象的 MoveNext 方法向其调用者返回 true，表示枚举器对象成功推进到下一项。

对枚举器对象的 MoveNext 方法的下一次调用将从上次挂起的位置恢复迭代器块的执行。

yield break 语句按如下方式执行：

- 如果 yield break 语句被一个或多个带有相关 finally 块的 try 块所包含，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制将转移到下一个外层 try 语句的 finally 块。此过程重复，直到所有外层 try 语句的 finally 块都已执行。
- 控制返回到迭代器块的调用者。这要么是枚举器对象的 MoveNext 方法，要么是 Dispose 方法。

由于 yield break 语句无条件地将控制转移到别处，yield break 语句的终点永远无法到达。

> **CHRIS SELLS** 我有时会忘记 yield return 与 return 不同，即 yield return 之后的代码可以被执行。例如，这里第一个 return 之后的代码永远不会被执行：
> 
> ```
> int F() {
>     return 1;
>     return 2; // Can never be executed
> }
> ```
> 
> 相比之下，这里第一个 yield return 之后的代码可以被执行：
> 
> ```
> IEnumerable<int> F() {
>     yield return 1;
>     yield return 2; // Can be executed
> }
> ```
> 
> 这经常在我使用 if 语句时会咬到我：
> 
> ```
> IEnumerable<int> F() {
>     if(...) { yield return 1; } // I mean this to be the only
>     // thing returned
>     yield return 2;           // Oops!
> }
> ```
> 
> 在这些情况下，记住 yield return 不像 return 那样是“最终的”是有帮助的。

> **CHRISTIAN NAGEL** 自 C# 1.0 以来，使用迭代器（foreach 语句）变得很容易。自 C# 2.0 以来，创建迭代器变得很容易（yield 语句）。



# 9. 命名空间

C# 程序使用命名空间进行组织。命名空间既用作程序的“内部”组织系统，也用作“外部”组织系统——一种呈现向其他程序公开的程序元素的方式。

使用指令（§9.4）用于方便命名空间的使用。

> BILL WAGNER 阅读本文时请记住，命名空间是一种逻辑组织：多个命名空间可以，并且经常出现在一个程序集中，而单个命名空间可能在许多不同的程序集中声明。

### 9.1 编译单元

编译单元定义源文件的整体结构。编译单元由零个或多个使用指令组成，其后跟零个或多个全局属性，再后跟零个或多个命名空间成员声明。

```
compilation-unit:
    extern-alias-directives_opt using-directives_opt global-attributes_opt
    namespace-member-declarations_opt
```

C# 程序由一个或多个编译单元组成，每个编译单元包含在单独的源文件中。当 C# 程序被编译时，所有编译单元都会一起处理。因此编译单元可以相互依赖，甚至可能形成循环依赖。

> CHRIS SELLS 仅此一项功能就使 C# 比 C 或 C++ 更容易使用大约十倍。

编译单元的使用指令会影响该编译单元的全局属性和命名空间成员声明，但不会影响其他编译单元。

> **JON SKEET** 大多数时候我认为我喜欢这个功能——但偶尔，当我想快速编写一个程序来测试几行代码时，我宁愿不必导入一堆命名空间。了解在“项目级”使用指令（如程序集引用）在另一种现实中会产生什么影响会很有趣。

> **ERIC LIPPERT** Jon 的观点很有道理：如果程序非常短，编写任何 C# 程序所需的“仪式”是不成比例的。虽然 C# 本身并非旨在成为“脚本”语言，但有一点很不错，那就是一行程序在例如 JScript 中确实只有一行。

编译单元的 *全局属性*（§17）允许为目标程序集和模块指定属性。程序集和模块充当类型的物理容器。程序集可能由几个物理上分离的模块组成。

程序的每个编译单元的 *命名空间成员声明* 为称为全局命名空间的单个声明空间贡献成员。例如：

```
File A.cs:
    class A {}

File B.cs:
    class B {}
```

这两个编译单元贡献给单个全局命名空间——在这种情况下，声明了两个完全限定名为 A 和 B 的类。由于这两个编译单元贡献给同一个声明空间，如果每个编译单元都包含同名成员的声明，就会成为错误。

### 9.2 命名空间声明

*命名空间声明* 由关键字 namespace 组成，其后跟命名空间名称和主体，可选择后跟分号。

```
namespace-declaration:
    namespace qualified-identifier namespace-body ;opt

qualified-identifier:
    identifier
    qualified-identifier . identifier

namespace-body:
    { extern-alias-directives_opt using-directives_opt namespace-member-declarations_opt }
```

命名空间声明可以作为编译单元中的顶级声明出现，也可以作为另一个命名空间声明内的成员声明出现。当命名空间声明作为编译单元中的顶级声明出现时，该命名空间成为全局命名空间的成员。当命名空间声明在另一个命名空间声明内出现时，内部命名空间成为外部命名空间的成员。在任何情况下，命名空间的名称在其包含的命名空间内必须是唯一的。

命名空间隐式为 public，命名空间的声明不能包含任何访问修饰符。

在命名空间主体内，可选的使用指令导入其他命名空间和类型的名称，使它们可以通过限定名称直接引用。可选的命名空间成员声明为命名空间的声明空间贡献成员。请注意，所有使用指令必须出现在任何成员声明之前。

命名空间声明的 qualified-identifier 可以是单个标识符，也可以是由“.” 标记分隔的标识符序列。后一种形式允许程序在不词法嵌套多个命名空间声明的情况下定义嵌套命名空间。例如，

```
namespace N1.N2
{
    class A { }
    class B { }
}
```

在语义上等价于

```
namespace N1
{
    namespace N2
    {
        class A { }
        class B { }
    }
}
```

命名空间是开放式的，并且具有相同完全限定命名空间名称的两个命名空间声明贡献给同一个声明空间（§3.3）。在示例中

```
namespace N1.N2
{
    class A { }
}

namespace N1.N2
{
    class B { }
}
```

这两个命名空间声明贡献给同一个声明空间——在这种情况下声明了两个完全限定名为 N1.N2.A 和 N1.N2.B 的类。由于这两个声明贡献给同一个声明空间，如果每个声明都包含同名成员的声明，就会成为错误。

### 9.3 外部别名

*外部别名指令* 引入一个标识符，该标识符用作命名空间的别名。被别名化的命名空间的规范位于程序源代码之外，并且也适用于被别名化命名空间的嵌套命名空间。

```
extern-alias-directives:
    extern-alias-directive
    extern-alias-directives  extern-alias-directive

extern-alias-directive:
    extern  alias  identifier  ;
```

*外部别名指令* 的作用域扩展到其直接包含的编译单元或命名空间主体中的 *使用指令*、*全局属性* 和 *命名空间成员声明*。

在包含 *外部别名指令* 的编译单元或命名空间主体内，由 *外部别名指令* 引入的标识符可用于引用被别名化的命名空间。标识符为 global 词是编译时错误。

*外部别名指令* 在特定编译单元或命名空间主体内使别名可用，但它不会向底层声明空间贡献任何新成员。换句话说，*外部别名指令* 不是传递的，而是仅影响它出现的编译单元或命名空间主体。

以下程序声明并使用两个 extern 别名 X 和 Y，每个别名代表一个不同的命名空间层次结构的根：

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

程序声明了 extern 别名 X 和 Y 的存在，但别名的实际定义位于程序之外。现在同名 N.B 类可以作为 X.N.B 和 Y.N.B 引用，或使用命名空间别名限定符作为 X::N.B 和 Y::N.B 引用。如果程序声明了一个没有外部定义提供的 extern 别名，则会发生错误。

### 9.4 使用指令

***使用指令*** 方便使用在其他命名空间中定义的命名空间和类型。使用指令会影响 *命名空间或类型名称*（§3.8）和 *简单名称*（§7.6.2）的名称解析过程，但与声明不同，使用指令不会向使用它们的编译单元或命名空间的底层声明空间贡献新成员。

```
using-directives:
    using-directive
    using-directives   using-directive
```

```
using-directive:
    using-alias-directive
    using-namespace-directive
```

*使用别名指令*（§9.4.1）为命名空间或类型引入别名。

*使用命名空间指令*（§9.4.2）导入命名空间的类型成员。

*使用指令* 的作用域扩展到其直接包含的编译单元或命名空间主体中的 *命名空间成员声明*。*使用指令* 的作用域特别不包括其同级 *使用指令*。因此同级 *使用指令* 互不影响，它们书写的顺序无关紧要。




## 9.4.1 using 别名指令

*using-alias-directive* 引入一个标识符，该标识符在直接包含它的编译单元或命名空间主体中，作为命名空间或类型的别名。

```
using-alias-directive:
    using identifier = namespace-or-type-name ;
```

在包含 *using-alias-directive* 的编译单元或命名空间主体的成员声明中，可以使用 *using-alias-directive* 引入的标识符来引用给定的命名空间或类型。例如：

```
namespace N1.N2
{
    class A { }
}

namespace N3
{
    using A = N1.N2.A;
    class B : A { }
}
```

在此示例中，在 N3 命名空间的成员声明中，A 是 N1.N2.A 的别名，因此 N3.B 类派生自 N1.N2.A 类。通过为 N1.N2 创建别名 R，然后引用 R.A，也可以获得相同的效果：

```
namespace N3
{
    using R = N1.N2;
    class B : R.A { }
}
```

*using-alias-directive* 的 *identifier* 在直接包含该 *using-alias-directive* 的编译单元或命名空间的声明空间中必须是唯一的。例如：

```
namespace N3
{
    class A { }
}

namespace N3
{
    using A = N1.N2.A;      // 错误：A 已存在
}
```

在此示例中，N3 已经包含成员 A，因此 *using-alias-directive* 使用该标识符会导致编译时错误。同样，在同一个编译单元或命名空间主体中，两个或多个 *using-alias-directive* 使用相同名称声明别名，也会导致编译时错误。

*using-alias-directive* 使别名在特定的编译单元或命名空间主体中可用，但不会向底层声明空间贡献任何新成员。换句话说，*using-alias-directive* 不是传递性的，而只影响其所在的编译单元或命名空间主体。在以下示例中：

```
namespace N3
{
    using R = N1.N2;
}
namespace N3
{
    class B : R.A {}        // 错误：R 未知
}
```

引入 R 的 *using-alias-directive* 的作用域仅扩展到其所在命名空间主体中的成员声明，因此在第二个命名空间声明中，R 未知。但是，将 *using-alias-directive* 放置在包含它的编译单元中，可以使该别名在两个命名空间声明中都可用：

```
using R = N1.N2;
namespace N3
{
    class B: R.A {}
}
namespace N3
{
    class C: R.A {}
}
```

与普通成员一样，*using-alias-directive* 引入的名称会被嵌套作用域中名称相同的成员隐藏。在以下示例中：

```
using R = N1.N2;
namespace N3
{
    class R {}
    class B: R.A {}        // 错误：R 没有成员 A
}
```

B 的声明中对 R.A 的引用会导致编译时错误，因为 R 指的是 N3.R，而不是 N1.N2。

*using-alias-directive* 的书写顺序没有意义，并且 *using-alias-directive* 所引用的 *namespace-or-type-name* 的解析不受该 using-alias-directive 本身或直接包含它的编译单元或命名空间主体中的其他 using 指令影响。换句话说，using-alias-directive 的 namespace-or-type-name 会在直接包含它的编译单元或命名空间主体仿佛没有任何 using 指令的情况下进行解析。不过，using-alias-directive 可能会受到直接包含它的编译单元或命名空间主体中的 extern-alias-directive 影响。在以下示例中：

```
namespace N1.N2 { }
namespace N3
{
    extern alias E;

    using R1 = E.N;      // 正确
    using R2 = N1;       // 正确
    using R3 = N1.N2;    // 正确
    using R4 = R2.N2;    // 错误：R2 未知
}
```

最后一个 using-alias-directive 会导致编译时错误，因为它不受第一个 using-alias-directive 的影响。第一个 using-alias-directive 不会产生错误，因为 extern 别名 E 的作用域包含该 using-alias-directive。

using-alias-directive 可以为任何命名空间或类型创建别名，包括其所在的命名空间，以及嵌套在该命名空间中的任何命名空间或类型。

通过别名访问命名空间或类型，与通过其声明名称访问该命名空间或类型的结果完全相同。例如，给定以下代码：

```
namespace N1.N2
{
    class A { }
}
namespace N3
{
    using R1 = N1;
    using R2 = N1.N2;
    class B
    {
        N1.N2.A a;      // 引用 N1.N2.A
        R1.N2.A b;      // 引用 N1.N2.A
        R2.A c;         // 引用 N1.N2.A
    }
}
```

名称 N1.N2.A、R1.N2.A 和 R2.A 是等价的，并且都引用完全限定名称为 N1.N2.A 的类。

using 别名可以命名封闭构造类型，但不能在不提供类型实参的情况下命名未绑定的泛型类型声明。例如：

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
    using W = N1.A;      // 错误：无法命名未绑定的泛型类型
    using X = N1.A.B;    // 错误：无法命名未绑定的泛型类型
    using Y = N1.A<int>; // 正确：可以命名封闭构造类型
    using Z<T> = N1.A<T>; // 错误：using 别名不能包含类型参数
}
```

## 9.4.2 using 命名空间指令

using-namespace-directive 将命名空间中包含的类型导入直接包含它的编译单元或命名空间主体，从而可以在不进行限定的情况下使用每个类型的标识符。

```
using-namespace-directive:
    using namespace-name ;
```

在包含 using-namespace-directive 的编译单元或命名空间主体的成员声明中，可以直接引用给定命名空间中包含的类型。例如：

```
namespace N1.N2
{
    class A { }
}
namespace N3
{
    using N1.N2;
    class B : A { }
}
```

在此示例中，在 N3 命名空间的成员声明中，N1.N2 的类型成员可以直接使用，因此 N3.B 类派生自 N1.N2.A 类。

using-namespace-directive 会导入给定命名空间中包含的类型，但明确不会导入嵌套命名空间。在以下示例中：

```
namespace N1.N2
{
    class A { }
}
namespace N3
{
    using N1;
    class B : N2.A { }      // 错误：N2 未知
}
```

using-namespace-directive 会导入 N1 中包含的类型，但不会导入嵌套在 N1 中的命名空间。因此，B 的声明中对 N2.A 的引用会导致编译时错误，因为作用域中没有名为 N2 的成员。

与 using-alias-directive 不同，using-namespace-directive 可以导入标识符已在直接包含它的编译单元或命名空间主体中定义的类型。实际上，using-namespace-directive 导入的名称会被直接包含它的编译单元或命名空间主体中名称相同的成员隐藏。例如：

```
namespace N1.N2
{
    class A { }
    class B { }
}
namespace N3
{
    using N1.N2;
    class A { }
}
```

在这里，在 N3 命名空间的成员声明中，A 指的是 N3.A，而不是 N1.N2.A。

当同一编译单元或命名空间主体中的 using-namespace-directive 导入的多个命名空间包含同名类型时，对该名称的引用会被视为具有歧义。在以下示例中：

```
namespace N1
{
    class A { }
}
namespace N2
{
    class A { }
}
```

```
namespace N3
{
    using N1;
    using N2;
    class B : A {        // 错误：A 存在歧义
}
```

N1 和 N2 都包含成员 A，并且由于 N3 同时导入了这两个命名空间，因此在 N3 中引用 A 会导致编译时错误。在这种情况下，可以通过限定对 A 的引用，或引入一个选择特定 A 的 using-alias-directive 来解决冲突。例如：

```
namespace N3
{
    using N1;
    using N2;
    using A = N1.A;
    class B : A { }        // A 表示 N1.A
}
```

与 using-alias-directive 一样，using-namespace-directive 不会向编译单元或命名空间的底层声明空间贡献任何新成员，而只影响其所在的编译单元或命名空间主体。

using-namespace-directive 所引用的 namespace-name 的解析方式，与 using-alias-directive 所引用的 namespace-or-type-name 的解析方式相同。因此，同一编译单元或命名空间主体中的 using-namespace-directive 不会相互影响，并且可以按任意顺序书写。

## 9.5 命名空间成员

namespace-member-declaration 要么是 namespace-declaration（命名空间声明）（§9.2），要么是 type-declaration（类型声明）（§9.6）。

```
namespace-member-declarations:
    namespace-member-declaration
    namespace-member-declarations namespace-member-declaration

namespace-member-declaration:
    namespace-declaration
    type-declaration
```




编译单元或命名空间主体可以包含*命名空间成员声明*，此类声明会向包含它的编译单元或命名空间主体的基础声明空间贡献新成员。

## 9.6 类型声明

*类型声明*是*类声明*（§10.1）、*结构声明*（§11.1）、*接口声明*（§13.1）、*枚举声明*（§14.1）或*委托声明*（§15.1）。

```
type-declaration:
    class-declaration
    struct-declaration
    interface-declaration
    enum-declaration
    delegate-declaration
```

*类型声明*可以作为编译单元中的顶级声明出现，也可以作为命名空间、类或结构中的成员声明出现。

当类型 T 的类型声明作为编译单元中的顶级声明出现时，新声明类型的完全限定名就是 T。当类型 T 的类型声明出现在命名空间、类或结构中时，新声明类型的完全限定名为 N.T，其中 N 是包含该声明的命名空间、类或结构的完全限定名。

在类或结构内声明的类型称为嵌套类型（§10.3.8）。

类型声明允许的访问修饰符和默认访问权限取决于声明所在的上下文（§3.5.1）：

- 在编译单元或命名空间中声明的类型可以具有 public 或 internal 访问权限。默认是 internal 访问权限。
- 在类中声明的类型可以具有 public、protected internal、protected、internal 或 private 访问权限。默认是 private 访问权限。
- 在结构中声明的类型可以具有 public、internal 或 private 访问权限。默认是 private 访问权限。

## 9.7 命名空间别名限定符

*命名空间别名限定符* `::` 可以确保类型名称查找不受新类型和新成员引入的影响。命名空间别名限定符始终出现在两个标识符之间，这两个标识符称为左侧标识符和右侧标识符。与常规的 . 限定符不同，:: 限定符的左侧标识符仅作为 extern 别名或 using 别名进行查找。

*限定别名成员*定义如下：

```
qualified-alias-member:
    identifier :: identifier type-argument-list_opt
```

*限定别名成员*可以用作*命名空间或类型名*（§3.8），也可以用作*成员访问*（§7.6.4）中的左操作数。

*限定别名成员*具有以下两种形式之一：

- *N* :: *I*<*A*₁, ..., *A*ₖ>，其中 *N* 和 *I* 表示标识符，<*A*₁, ..., *A*ₖ> 是类型实参列表。（K 始终至少为 1。）
- *N* :: *I*，其中 *N* 和 *I* 表示标识符。（在这种情况下，K 视为 0。）

使用这种表示法，*限定别名成员*的含义按如下方式确定：

- 如果 *N* 是标识符 `global`，则在全局命名空间中搜索 *I*：
  - 如果全局命名空间包含名为 *I* 的命名空间且 *K* 为 0，则*限定别名成员*引用该命名空间。
  - 否则，如果全局命名空间包含名为 *I* 的非泛型类型且 *K* 为 0，则*限定别名成员*引用该类型。
  - 否则，如果全局命名空间包含名为 *I* 且具有 *K* 个类型参数的类型，则*限定别名成员*引用用给定类型实参构造的该类型。
  - 否则，*限定别名成员*未定义，并发生编译时错误。
- 否则，从紧包含*限定别名成员*的命名空间声明（§9.2）（如果有）开始，继续处理每个外围命名空间声明（如果有），直到包含*限定别名成员*的编译单元结束，按以下步骤求值，直到定位到某个实体：
  - 如果该命名空间声明或编译单元包含将 *N* 与类型关联的 *using 别名指令*，则*限定别名成员*未定义，并发生编译时错误。
  - 否则，如果该命名空间声明或编译单元包含将 *N* 与命名空间关联的 *extern 别名指令*或 *using 别名指令*，则：
    - 如果与 *N* 关联的命名空间包含名为 *I* 的命名空间且 *K* 为 0，则*限定别名成员*引用该命名空间。
    - 否则，如果与 N 关联的命名空间包含名为 I 的非泛型类型且 K 为 0，则*限定别名成员*引用该类型。
    - 否则，如果与 N 关联的命名空间包含名为 I 且具有 K 个类型参数的类型，则*限定别名成员*引用用给定类型实参构造的该类型。
    - 否则，*限定别名成员*未定义，并发生编译时错误。
  - 否则，*限定别名成员*未定义，并发生编译时错误。

注意，将命名空间别名限定符与引用类型的别名一起使用会导致编译时错误。另请注意，如果标识符 N 为 global，则查找会在全局命名空间中执行，即使存在将 global 与类型或命名空间关联的 using 别名。

### 9.7.1 别名的唯一性

每个编译单元和命名空间主体都拥有用于 extern 别名和 using 别名的单独声明空间。因此，虽然 extern 别名或 using 别名的名称在紧包含它的编译单元或命名空间主体中所声明的 extern 别名和 using 别名集合内必须唯一，但只要别名仅与 :: 限定符一起使用，就允许该别名与某个类型或命名空间同名。

在以下示例中

```
namespace N
{
    public class A { }
    public class B { }
}
namespace N
{
    using A = System.IO;
    class X
    {
        A.Stream s1;          // Error: A is ambiguous
        A::Stream s2;         // Okay
    }
}
```

名称 A 在第二个命名空间主体中有两种可能的含义，因为类 A 和 using 别名 A 都处于作用域中。因此，在限定名 A.Stream 中使用 A 会产生歧义，并导致编译时错误。但是，将 A 与 :: 限定符一起使用不会出错，因为 A 仅作为命名空间别名进行查找。

# 10. 类

类是一种数据结构，可以包含数据成员（常量和字段）、函数成员（方法、属性、事件、索引器、运算符、实例构造函数、析构函数和静态构造函数）以及嵌套类型。类类型支持继承，这是一种使派生类可以扩展并特化基类的机制。

### 10.1 类声明

类声明是声明新类的类型声明（§9.6）。

```
class-declaration:
    attributes_opt class-modifiers_opt partial class identifier type-parameter-list_opt
        class-base_opt type-parameter-constraints-clauses_opt class-body ;opt
```

类声明由可选的一组特性（§17）、可选的一组类修饰符（§10.1.1）、可选的 partial 修饰符、关键字 class 和命名该类的标识符、可选的类型参数列表（§10.1.3）、可选的类基规范（§10.1.4）、可选的一组类型参数约束子句（§10.1.5）、类主体（§10.1.6）组成，后面可选跟一个分号。

类声明除非同时提供类型参数列表，否则不能提供类型参数约束子句。

提供类型参数列表的类声明是泛型类声明。此外，嵌套在泛型类声明或泛型结构声明中的任何类本身也是泛型类声明，因为创建构造类型时必须提供包含类型的类型参数。

### 10.1.1 类修饰符

类声明可以选择性地包含一系列类修饰符：

```
class-modifiers:
    class-modifier
    class-modifiers class-modifier
```

*类修饰符：*
- new
- public
- protected
- internal
- private
- abstract
- sealed
- static

同一个修饰符在类声明中出现多次是编译时错误。

new 修饰符允许用于嵌套类。它指定该类隐藏同名的继承成员，如 §10.3.4 所述。new 修饰符出现在不是嵌套类声明的类声明上是编译时错误。

public、protected、internal 和 private 修饰符控制类的可访问性。根据类声明出现的上下文，其中某些修饰符可能不被允许（§3.5.1）。

abstract、sealed 和 static 修饰符将在以下各节中讨论。

## 10.1.1.1 抽象类

abstract 修饰符用于指示类是不完整的，并且意图仅用作基类。抽象类与非抽象类在以下方面不同：

- 抽象类不能直接实例化，并且对抽象类使用 `new` 运算符是编译时错误。虽然可以具有编译时类型为抽象的变量和值，但这些变量和值必然要么为 null，要么包含对派生自该抽象类型的非抽象类实例的引用。
- 抽象类允许（但不要求）包含抽象成员。
- 抽象类不能是密封的。

当非抽象类派生自抽象类时，该非抽象类必须包含所有继承的抽象成员的实际实现，从而重写这些抽象成员。在示例中

```
abstract class A
{
    public abstract void F();
}

abstract class B: A
{
    public void G() {}
}
class C: B
{
    public override void F() {
        // Actual implementation of F
    }
}
```

抽象类 A 引入抽象方法 F。类 B 引入额外的方法 G，但由于它未提供 F 的实现，B 也必须声明为抽象。类 C 重写 F 并提供实际实现。由于 C 中没有抽象成员，C 允许（但不要求）为非抽象。

## 10.1.1.2 密封类

sealed 修饰符用于阻止从类派生。如果将密封类指定为另一个类的基类，则发生编译时错误。

密封类也不能同时是抽象类。

sealed 修饰符主要用于防止意外派生，但它也支持某些运行时优化。特别是，由于已知密封类永远不会有任何派生类，因此可以将对密封类实例的虚函数成员调用转换为非虚调用。

> JON SKEET  默认让类非密封（但方法非虚）的选择一直是一个激烈争议的问题。我同意“为继承而设计，否则禁止继承”这一格言，但两种观点都有论据。奇怪的一点是默认值有多么强大：尽管我通常在想的时候会选择密封类，但完全忽略这个选择实在太容易了。它显然不影响可以表达什么，但我确信它会影响实际生成的代码。

> JESSE LIBERTY  我愿意冒与 Jon 意见不同的风险。
> 
> 即使提前几个月，你能准确预见需要什么，这显然是不成立的。因此，良好的编程实践会要求让你的设计逐渐浮现，在明确需要之前只构建很少或什么都不构建，并避免关闭你认为永远不需要的途径。
> 
> 密封就像是布下的雷区，用来声明：“你永远不需要到这里来。”我认为你不可能知道这一点，也不应该自以为可以尝试。

## 10.1.1.3 静态类

static 修饰符用于将所声明的类标记为静态类。静态类不能被实例化，不能用作类型，并且只能包含静态成员。只有静态类才能包含扩展方法的声明（§10.6.9）。

静态类声明受以下限制：

- 静态类不得包含 sealed 或 abstract 修饰符。但请注意，由于静态类不能被实例化或派生，它的行为就好像既是密封的又是抽象的。
- 静态类不得包含类基规范（§10.1.4），也不能显式指定基类或所实现接口的列表。静态类隐式继承自 object 类型。
- 静态类只能包含静态成员（§10.3.7）。请注意，常量和嵌套类型被归类为静态成员。
- 静态类不能具有声明可访问性为 protected 或 protected internal 的成员。

违反上述任何限制都是编译时错误。

静态类没有实例构造函数。不能在静态类中声明实例构造函数，并且不会为静态类提供默认实例构造函数（§10.11.4）。

静态类的成员不会自动成为静态成员，成员声明必须显式包含 static 修饰符（常量和嵌套类型除外）。当某个类嵌套在静态外部类中时，除非该嵌套类显式包含 static 修饰符，否则它不是静态类。

> MAREK SAFAR 在 C# 1.0 中，必须使用带有私有构造函数的密封类来模拟静态类。这不再需要了，因为静态类提供了更优雅的方式来表达这一意图，并且还带来了许多编译器检查的好处，可检查在静态上下文中不允许的操作。

### 10.1.1.3.1 引用静态类类型

命名空间或类型名（§3.8）在以下情况下允许引用静态类：

- 该命名空间或类型名是形式为 T.I 的命名空间或类型名中的 T，或者
- 该命名空间或类型名是形式为 typeof(T) 的 typeof 表达式（§7.5.11）中的 T。

主表达式（§7.5）在以下情况下允许引用静态类：

- 该主表达式是形式为 E.I 的成员访问（§7.5.4）中的 E。

在任何其他上下文中，引用静态类都是编译时错误。例如，将静态类用作基类、成员的组成类型（§10.3.8）、泛型类型实参或类型参数约束都是错误。同样，静态类不能用于数组类型、指针类型、new 表达式、cast 表达式、is 表达式、as 表达式、sizeof 表达式或默认值表达式。

## 10.1.2 partial 修饰符

partial 修饰符用于指示此类声明是分部类型声明。封闭命名空间或类型声明中具有相同名称的多个分部类型声明按照 §10.2 中指定的规则合并成一个类型声明。

如果类的声明分布在不同的程序文本段中，并且这些段在不同上下文中生成或维护，那么这种做法可能很有用。例如，类声明的一部分可以由机器生成，而另一部分由手工编写。将二者在文本上分开可以防止一方的更新与另一方的更新发生冲突。

> CHRIS SELLS 我喜欢 partial 类能够将机器生成的部分与人工生成的部分分开的能力。不幸的是，你可以通过将一个类拆分到两个以上文件来滥用 partial 类。作为代码阅读者，我发现这种做法极难理解，并且我强烈不建议这样做。

## 10.1.3 类型参数

类型参数是一个简单标识符，表示用于创建构造类型时所提供的类型实参的占位符。类型参数是稍后将提供的类型的形式占位符。相比之下，类型实参（§4.4.1）是在创建构造类型时替换类型参数的实际类型。

```
type-parameter-list:
  < type-parameters >

type-parameters:
  attributes_opt type-parameter
  type-parameters , attributes_opt type-parameter

type-parameter:
  identifier
```



每个类声明中的类型参数都在该类的声明空间（§3.3）中定义一个名称。因此，它不能与另一个类型参数或在该类中声明的成员具有相同的名称。类型参数也不能与类型本身具有相同的名称。

## 10.1.4 类基规范

类声明可以包含一个 *类基* 规范，它定义了该类的直接基类以及该类直接实现的接口（§13）。

```text
class-base:
    :   class-type
    :   interface-type-list
    :   class-type  ,  interface-type-list

interface-type-list:
    interface-type
    interface-type-list  ,  interface-type
```

在类声明中指定的基类可以是构造的类类型（§4.4）。基类本身不能是类型参数，尽管它可以涉及作用域中的类型参数。

```csharp
class Extend<V> : V { }    // Error: type parameter used as base class
```

> **BILL WAGNER** 我希望能移除这个限制。这将是一种创建混入的绝佳方式。我意识到这是一个非常困难的问题，因为 V 可能包含任意的方法和属性。根据在封闭泛型类型中为 V 使用的任何具体类型，Extend<V> 可能无法编译。

### 10.1.4.1 基类

当 *类类型* 包含在 *类基* 中时，它指定了正在声明的类的直接基类。如果类声明没有 *类基*，或 *类基* 仅列出接口类型，则假定直接基类为 `object`。类从其直接基类继承成员，如 §10.3.3 中所述。

在示例中

```csharp
class A { }
class B : A { }
```

class `A` 被称为 `B` 的直接基类，而 `B` 被称为派生自 `A`。由于 `A` 没有显式指定直接基类，其直接基类隐式为 `object`。

对于构造的类类型，如果在泛型类声明中指定了基类，则构造类型的基类是通过为基类声明中的每个 *类型参数* 替换构造类型的相应 *类型实参* 而得到的。给定泛型类声明

```csharp
class B<U, V> { ... }
class G<T> : B<string, T> { ... }
```

构造类型 `G<int>` 的基类将为 `B<string, int>`。

类类型的直接基类的可访问性必须至少与类类型本身一样（§3.5.2）。例如，公共类派生自私有或内部类是编译时错误。

类类型的直接基类不得是以下任何类型：`System.Array`、`System.Delegate`、`System.MulticastDelegate`、`System.Enum` 或 `System.ValueType`。此外，泛型类声明不能将 `System.Attribute` 用作直接或间接基类。

在确定类 `B` 的直接基类规范 `A` 的含义时，`B` 的直接基类暂时假定为 `object`。直观上，这确保了类规范的含义不能递归地依赖于自身。示例

```csharp
class A<T>
{
    public class B { }
}

class C : A<C.B> { }
```

是错误的，因为在基类规范 `A<C.B>` 中，`C` 的直接基类被视为 `object`；因此，根据 §3.8 的规则，`C` 不被视为具有成员 `B`。

类类型的基类是直接基类及其基类。换句话说，基类集合是直接基类关系的传递闭包。参考上面的示例，`B` 的基类是 `A` 和 `object`。在示例中

```csharp
class A { ... }
class B<T> : A { ... }
class C<T> : B<IComparable<T>> { ... }
class D<T> : C<T> { ... }
```

`D<int>` 的基类是 `C<int>`、`B<IComparable<int>>`、`A` 和 `object`。

除 `object` 类外，每个类类型都有且仅有一个直接基类。`object` 类没有直接基类，并且是所有其他类的最终基类。

当类 `B` 派生自类 `A` 时，`A` 依赖于 `B` 是编译时错误。类 *直接依赖于* 其直接基类（如果有），并且 *直接依赖于* 其立即嵌套所在的类（如果有）。根据此定义，类所依赖的完整类集合是 *直接依赖于* 关系的自反和传递闭包。

> **VLADIMIR RESHETNIKOV** 就此规则而言，类型实参（如果有）将被忽略。例如，虽然 `A<T>` 和 `A<A<T>>` 是不同的类型，但以下声明仍然无效：
>
> ```csharp
> class A<T> : A<A<T>> { }
> ```
>
> 相反，将类出现在指定为其基类的构造类型的类型实参中是完全有效的：
>
> ```csharp
> class A<T> { }
> class B : A<B[]> { } // Okay
> ```

示例

```csharp
class A : A { }
```

是错误的，因为该类依赖于自身。同样，示例

```csharp
class A : B { }
class B : C { }
class C : A { }
```

是错误的，因为这些类循环依赖于自身。最后，示例

```csharp
class A : B.C { }

class B : A
{
    public class C { }
}
```

会导致编译时错误，因为 `A` 依赖于 `B.C`（其直接基类），`B.C` 依赖于 `B`（其立即封闭类），而 `B` 循环依赖于 `A`。

请注意，类不依赖于嵌套在其内部的类。在示例中

```csharp
class A
{
    class B : A { }
}
```

`B` 依赖于 `A`，因为 `A` 既是其直接基类也是其立即封闭类，但 `A` 不依赖于 `B`，因为 `B` 既不是 `A` 的基类也不是 `A` 的封闭类。因此，该示例是有效的。

不可能从密封类派生。在示例中

```csharp
sealed class A { }

class B : A { }          // Error: cannot derive from a sealed class
```

类 `B` 是错误的，因为它试图从密封类 `A` 派生。

### 10.1.4.2 接口实现

*类基* 规范可以包含接口类型的列表，在这种情况下，类被认为直接实现了给定的接口类型。接口实现在 §13.4 中进一步讨论。

## 10.1.5 类型参数约束

泛型类型和方法的声明可以通过包含 *类型参数约束子句* 可选地指定类型参数约束。

```text
type-parameter-constraints:
    type-parameter-constraints-clause
    type-parameter-constraints-clauses  type-parameter-constraints-clause

type-parameter-constraints-clause:
    where  type-parameter  :  type-parameter-constraints

type-parameter-constraints:
    primary-constraint
    secondary-constraints
    constructor-constraint
    primary-constraint  ,  secondary-constraints
    primary-constraint  ,  constructor-constraint
    secondary-constraints  ,  constructor-constraint
    primary-constraint  ,  secondary-constraints  ,  constructor-constraint

primary-constraint:
    class-type
    class
    struct

secondary-constraints:
    interface-type
    type-parameter
    secondary-constraints  ,  interface-type
    secondary-constraints  ,  type-parameter

constructor-constraint:
    new    (    )
```

每个类型参数约束子句由标记 `where` 组成，后跟类型参数的名称，后跟冒号和该类型参数的约束列表。每个类型参数最多只能有一个 `where` 子句，并且 `where` 子句可以按任何顺序列出。与属性访问器中的 `get` 和 `set` 标记一样，`where` 标记不是关键字。

在 `where` 子句中给出的约束列表可以包含以下组件，按此顺序：单个主约束、一个或多个次要约束以及构造函数约束 `new()`。

主约束可以是类类型或引用类型约束 `class` 或值类型约束 `struct`。次要约束可以是类型参数或接口类型。

引用类型约束指定用于类型参数的类型实参必须是引用类型。所有类类型、接口类型、委托类型、数组类型以及已知为引用类型的类型参数（定义如下）都满足此约束。

值类型约束指定用于类型参数的类型实参必须是不可空的值类型。所有不可空的结构类型、枚举类型以及具有值类型约束的类型参数都满足此约束。尽管被归类为值类型，可空类型（§4.1.10）不满足值类型约束。具有值类型约束的类型参数也不能具有构造函数约束。

> **BILL WAGNER** 在某个时候，我发现这组约束非常有限。我想用泛型进行元编程，能够指定任意一组成员作为约束——比如其他构造函数签名或运算符。现在 C# 3.0 拥有 lambda 表达式并且更自然地支持将方法用作参数，这种感觉消失了。通过将委托签名指定为类型参数或作为方法的参数，C# 程序员几乎可以实现任何事情。

指针类型永远不允许作为类型实参，并且不被认为满足引用类型或值类型约束。

如果约束是类类型、接口类型或类型参数，则该类型指定了每个用于该类型参数的类型实参必须支持的最小“基类型”。每当使用构造类型或泛型方法时，类型实参都会在编译时与类型参数的约束进行检查。提供的类型实参必须满足 §4.4.4 中描述的条件。

类类型约束必须满足以下规则：

- 类型必须是类类型。
- 类型不得被密封。



- 该类型不得为以下类型之一：System.Array、System.Delegate、System.Enum 或 System.ValueType。

> **乔恩·斯基特**
>
> 我不知道有什么理由禁止 System.Enum 或 System.Delegate 在这里作为类型——尽管如果能写成“where T : enum”而不是“where T : struct, Enum”肯定更友好，后者将是最常见的用法。虽然 C# 是相对于 CLI 单独指定的，但你可能会怀疑这是 CLI 限制——但事实并非如此。实际上，ECMA-335 明确列出了这一项和其他 C# 中禁止的约束。也许这一限制将在语言未来版本中移除；有很多情况它会很有用。

- 该类型不得为 object。因为所有类型都派生自 object，这样的约束如果允许则没有效果。
- 对于给定的类型参数，至多一个约束可以是类类型。

指定为接口类型约束的类型必须满足以下规则：

- 该类型必须是接口类型。
- 在给定的 where 子句中，类型不得被多次指定。

无论哪种情况，约束都可以涉及关联类型或方法声明的任何类型参数，作为构造类型的一部分，并且可以涉及正在声明的类型。

指定为类型参数约束的任何类或接口类型都必须至少与泛型类型或方法声明的可访问性（§3.5.4）相同。

指定为类型参数约束的类型必须满足以下规则：

- 该类型必须是类型参数。
- 在给定的 where 子句中，类型不得被多次指定。

此外，类型参数的依赖关系图中不得存在循环，其中依赖关系定义如下：

- 如果类型参数 T 用作类型参数 S 的约束，则 S 依赖于 T。
- 如果类型参数 S 依赖于类型参数 T，并且 T 依赖于类型参数 U，则 S 依赖于 U。

给定此关系，类型参数依赖自身（直接或间接）是编译时错误。

## 10. 类

任何约束在依赖类型参数之间必须一致。如果类型参数 S 依赖于类型参数 T，则

- T 不得具有值类型约束。否则，T 实际上是密封的，因此 S 将被强制与 T 为同一类型，从而不再需要两个类型参数。
- 如果 S 具有值类型约束，则 T 不得具有*类类型*约束。
- 如果 S 具有*类类型*约束 A，且 T 具有*类类型*约束 B，则必须存在从 A 到 B 的标识转换或隐式引用转换，或者存在从 B 到 A 的隐式引用转换。
- 如果 S 还依赖于类型参数 U，且 U 具有*类类型*约束 A，T 具有*类类型*约束 B，则必须存在从 A 到 B 的标识转换或隐式引用转换，或者存在从 B 到 A 的隐式引用转换。

S 具有值类型约束且 T 具有引用类型约束是有效的。实际上，这会将 T 限制为 System.Object、System.ValueType、System.Enum 以及任何接口类型。

如果类型参数的 where 子句包含构造函数约束（其形式为 new()），则可以使用 new 运算符创建该类型的实例（§7.6.10.1）。用于具有构造函数约束的类型参数的任何类型实参都必须具有公共无参数构造函数（对于任何值类型，此构造函数隐式存在），或者是具有值类型约束或构造函数约束的类型参数（详情见 §10.1.5）。

以下是约束的示例：

```csharp
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

class Printer<T> where T : IPrintable {...}
class SortedList<T> where T : IComparable<T> {...}

class Dictionary<K, V>
    where K : IComparable<K>
    where V : IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

以下示例是错误的，因为它会导致类型参数的依赖关系图中出现循环：

```csharp
class Circular<S, T>
    where S : T
    where T : S    // Error: circularity in dependency graph
{
    ...
}
```

以下示例说明了其他无效情况：

```csharp
class Sealed<S, T>
    where S : T
    where T : struct    // Error: T is sealed
{
    ...
}

class A {...}
class B {...}

class Incompat<S, T>
    where S : A, T
    where T : B    // Error: incompatible class-type constraints
{
    ...
}

class StructWithClass<S, T, U>
    where S : struct, T
    where T : U
    where U : A    // Error: A incompatible with struct
{
    ...
}
```

类型参数 T 的有效基类定义如下：

- 如果 T 没有主约束或类型参数约束，则其有效基类为 object。
- 如果 T 具有值类型约束，则其有效基类为 System.ValueType。
- 如果 T 具有类类型约束 C 但没有类型参数约束，则其有效基类为 C。
- 如果 T 没有*类类型*约束但具有一个或多个*类型参数*约束，则其有效基类是其*类型参数*约束的有效基类集合中最包含的类型（§6.4.2）。一致性规则确保存在这样的最包含类型。
- 如果 T 同时具有*类类型*约束和一个或多个*类型参数*约束，则其有效基类是由 T 的*类类型*约束及其*类型参数*约束的有效基类组成的集合中最包含的类型（§6.4.2）。一致性规则确保存在这样的最包含类型。
- 如果 T 具有引用类型约束但没有*类类型*约束，则其有效基类为 object。

就这些规则而言，如果 T 具有一个为*值类型*的约束 V，则改用 V 的最具体基类型，该基类型为*类类型*。这种情况永远不会发生在显式给定的约束中，但当泛型方法的约束由重写方法声明或接口方法的显式实现隐式继承时，可能会发生。

这些规则确保有效基类始终是*类类型*。

> **埃里克·利珀特**
>
> 例如，假设你有
>
> ```csharp
> class B<T> { public virtual void M<U>() where U : T {} }
> class D : B<DateTime> { public override void M<V>() }
> ```
>
> 那么 V 的有效基类是类类型 System.ValueType，而不是结构类型 DateTime。类似地，如果不是 DateTime，而是 DateTime[]，那么有效基类将是类类型 System.Array，而不是数组类型 DateTime[]。

类型参数 T 的*有效接口集*定义如下：

- 如果 T 没有*次要约束*，则其有效接口集为空。
- 如果 T 具有*接口类型*约束但没有*类型参数*约束，则其有效接口集是其*接口类型*约束的集合。
- 如果 T 没有*接口类型*约束但具有*类型参数*约束，则其有效接口集是其*类型参数*约束的有效接口集的并集。
- 如果 T 同时具有*接口类型*约束和*类型参数*约束，则其有效接口集是其*接口类型*约束集合与其*类型参数*约束的有效接口集的并集。

如果类型参数具有引用类型约束，或者其有效基类不是 object 或 System.ValueType，则该类型参数已知为引用类型。

受约束的类型参数类型的值可用于访问约束所隐含的实例成员。在示例

```csharp
interface IPrintable
{
    void Print();
}

class Printer<T> where T : IPrintable
{
    void PrintOne(T x) {
        x.Print();
    }
}
```

中，可以直接在 x 上调用 IPrintable 的方法，因为 T 被约束为始终实现 IPrintable。

### 10.1.6 类体

类的类体定义该类的成员。

```
class-body:
    { class-member-declarations_opt }
```

### 10.2 分部类型

类型声明可以拆分到多个分部类型声明中。该类型声明按照本节中的规则由其各个部分构造而成，随后在程序的编译时和运行时处理的其余过程中被视为单个声明。

类声明、结构声明或接口声明如果包含 partial 修饰符，则表示分部类型声明。注意，partial 不是关键字，只有在类型声明中紧挨在关键字 class、struct 或 interface 之一之前出现，或者在方法声明中紧挨在类型 void 之前出现时，才充当修饰符。在其他上下文中，它可以用作普通标识符。

分部类型声明的每个部分都必须包含 partial 修饰符。它必须具有相同的名称，并与其他部分声明在相同的命名空间或类型声明中。partial 修饰符表示类型声明的其他部分可能存在于其他地方，但并不要求存在这样的其他部分；具有单个声明的类型包含 partial 修饰符是有效的。




分部类型的所有部分必须一起编译，以便这些部分可以在编译时合并为单个类型声明。分部类型明确不允许扩展已经编译好的类型。

通过使用 partial 修饰符，可以在多个部分中声明嵌套类型。通常，包含类型也使用 partial 声明，而嵌套类型的每个部分都在包含类型的不同部分中声明。

不允许在委托或枚举声明上使用 partial 修饰符。

> **BILL WAGNER** 显然，添加此特性是为了支持代码生成器，但它还有许多其他用途。我曾将嵌套类放在单独的编译单元中，并按照其他逻辑边界拆分类。然而，在一般情况下，仅仅为了让多个开发人员处理同一个类而拆分类是不建议的。

> **BRAD ABRAMS** 可视化软件设计工具采用的传统模型是提供某种用户界面，开发人员使用该界面表达其意图；然后工具根据该意图生成源代码。这种方法经过时间检验且广泛适用。例如，数据设计时、ASP.NET 设计时和 WinForms 设计时都使用这种基本模型。然而，这种模型确实带来一些挑战——即开发人员经常需要调整、修改或扩展工具生成的代码。直接编辑生成的代码是一种流行的解决方案，但它有一个主要缺点：使可视化设计工具无法使用。从生成的代码派生子类是另一种方法，但通常会因类型问题而变得复杂。分部类型和方法允许类由设计工具部分生成，并部分自定义以更好地适应给定场景。

## 10.2.1 特性

分部类型的特性通过以未指定的顺序组合每个部分的特性来确定。如果将某个特性放在多个部分上，则等效于在该类型上多次指定该特性。例如，以下两个部分

```
[Attr1, Attr2("hello")]
partial class A {}

[Attr3, Attr2("goodbye")]
partial class A {}
```

等效于以下声明：

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

类型参数上的特性可以按类似方式组合。

## 10.2.2 修饰符

当分部类型声明包含可访问性规范（public、protected、internal 和 private 修饰符）时，它必须与所有其他包含可访问性规范的部分一致。如果分部类型的任何部分都不包含可访问性规范，则给该类型赋予适当的默认可访问性（§3.5.1）。

如果嵌套类型的一个或多个分部声明包含 new 修饰符，则当该嵌套类型隐藏继承成员时不报告警告（§3.7.1.2）。

如果类的一个或多个分部声明包含 abstract 修饰符，则该类被视为抽象类（§10.1.1.1）。否则，该类被视为非抽象类。

如果类的一个或多个分部声明包含 sealed 修饰符，则该类被视为密封类（§10.1.1.2）。否则，该类被视为非密封类。

注意，类不能同时是抽象类和密封类。

当在分部类型声明上使用 unsafe 修饰符时，只有该特定部分被视为不安全上下文（§18.1）。

## 10.2.3 类型参数和约束

如果泛型类型在多个部分中声明，则每个部分都必须声明类型参数。每个部分必须具有相同数量的类型参数，并且每个类型参数的名称必须按顺序相同。

当分部泛型类型声明包含约束（where 子句）时，这些约束必须与所有其他包含约束的部分一致。具体而言，每个包含约束的部分都必须为同一组类型参数提供约束，并且对于每个类型参数，主要约束、次要约束和构造函数约束的集合必须等效。如果两个约束集合包含相同的成员，则它们是等效的。如果分部泛型类型的任何部分都未指定类型参数约束，则这些类型参数被视为不受约束。

示例

```
    partial class Dictionary<K,V>
        where K: IComparable<K>
        where V: IKeyProvider<K>, IPersistable
    {
        ...
    }

    partial class Dictionary<K,V>
        where V: IPersistable, IKeyProvider<K>
        where K: IComparable<K>
    {
        ...
    }

    partial class Dictionary<K,V>
    {
        ...
    }
```

是正确的，因为那些包含约束的部分（前两个部分）实际上分别为同一组类型参数指定了相同的主要约束、次要约束和构造函数约束集合。

> > **BILL WAGNER** 在可能的情况下，我倾向于在所有副本上指定类型参数和约束。这种技巧可以提高可读性。

## 10.2.4 基类

当分部类声明包含基类规范时，它必须与所有其他包含基类规范的部分一致。如果分部类的任何部分都不包含基类规范，则基类变为 System.Object（§10.1.4.1）。

## 10.2.5 基接口

在多个部分中声明的类型的基接口集合是每个部分上指定的基接口的并集。特定基接口在每个部分上只能命名一次，但允许多个部分命名相同的基接口。任何给定基接口的成员必须只有一个实现。

在示例中

```
    partial class C: IA, IB {...}
    partial class C: IC {...}
    partial class C: IA, IB {...}
```

类 C 的基接口集合为 IA、IB 和 IC。

通常，每个部分提供在该部分上声明的接口的实现；然而，这并不是一项要求。一个部分可以为在另一部分上声明的接口提供实现：

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

## 10.2.6 成员

除分部方法（§10.2.7）外，在多个部分中声明的类型的成员集合就是每个部分中声明的成员集合的并集。类型声明的所有部分的主体共享同一声明空间（§3.3），并且每个成员的作用域（§3.7）延伸到所有部分的主体。任何成员的可访问域始终包括封闭类型的所有部分；在一个部分中声明的私有成员可以从另一个部分自由访问。在类型的多个部分中声明同一成员是编译时错误，除非该成员是带有 partial 修饰符的类型。

> > **BILL WAGNER** 从逻辑上讲，你可以将以下示例视为一个很长的源文件，只不过你不知道类内容组合的顺序。

```
    partial class A
    {
        int x;                    // Error: cannot declare x more than once

        partial class Inner      // Okay: Inner is a partial type
        {
            int y;
        }
    }

    partial class A
    {
        int x;                    // Error: cannot declare x more than once

        partial class Inner      // Okay: Inner is a partial type
        {
            int z;
        }
    }
```

类型内成员的顺序对 C# 代码而言很少重要，但在与其他语言和环境交互时可能很重要。在这些情况下，在多个部分中声明的类型内成员的顺序是未定义的。

> **JON SKEET** 在 C# 中，顺序重要的一个领域是静态和实例变量初始化器：保证它们按照在类中出现的“文本顺序”（§10.5.5）执行。这不算重大损失，因为依赖这种顺序通常是个坏主意：仅仅重新排列声明就会出错的类，从一开始就过于脆弱。

> 期望在同一部分内声明的成员按明显顺序处理并非不合理，尽管规范并未明确保证这一点。

## 10.2.7 分部方法

分部方法可以在类型声明的一个部分中定义，并在另一个部分中实现。实现是可选的；如果没有任何部分实现该分部方法，则从各部分组合得到的类型声明中移除该分部方法声明及其所有调用。

> **VLADIMIR RESHETNIKOV** 分部方法只能在分部类或分部结构中声明。不能在非分部类型或接口中声明。

分部方法不能定义访问修饰符，但隐式是私有的。其返回类型必须为 void，并且其参数不能具有 out 修饰符。标识符 partial 只有在方法声明中紧邻 void 类型之前出现时，才被识别为特殊关键字；否则，它可以作为普通标识符使用。分部方法不能显式实现接口方法。

分部方法声明有两种：如果方法声明的主体是分号，则该声明称为定义分部方法声明。如果主体以块的形式给出，则该声明称为实现分部方法声明。在类型声明的各个部分中，对于给定签名，只能有一个定义分部方法声明，并且对于给定签名，只能有一个实现分部方法声明。如果给出了实现分部方法声明，则必须存在相应的定义分部方法声明，并且这些声明必须按以下规定匹配：

- 这些声明必须具有相同的修饰符（尽管不一定按相同顺序）、方法名、类型参数数量和参数数量。
- 声明中的对应参数必须具有相同的修饰符（尽管不一定按相同顺序）和相同的类型（类型参数名称的差异除外）。




-   声明中对应的类型参数必须具有相同的约束条件（忽略类型参数名称的差异）。

实现的部分方法声明可以与对应的定义部分方法声明出现在同一部分中。

只有定义的部分方法参与重载解析。因此，无论是否提供了实现声明，调用表达式都可能解析为对部分方法的调用。因为部分方法始终返回 void，这样的调用表达式始终是表达式语句。此外，因为部分方法隐式为 private，这样的语句始终出现在声明该部分方法类型的部分之一中。

如果部分类型声明的任何部分都不包含给定部分方法的实现声明，则调用它的任何表达式语句都将简单地从组合的类型声明中移除。因此，调用表达式（包括任何构成表达式）在运行时没有任何效果。部分方法本身也被移除，不会成为组合类型声明的成员。

如果存在给定部分方法的实现声明，则部分方法的调用将被保留。部分方法会产生一个与实现部分方法声明类似的方法声明，但有以下例外：

-   不包含 partial 修饰符。
-   生成的方法声明中的特性是定义部分方法声明和实现部分方法声明的特性的组合，顺序不确定。重复项不会被移除。
-   生成的方法声明参数上的特性是定义部分方法声明和实现部分方法声明中对应参数的特性的组合，顺序不确定。重复项不会被移除。

如果为部分方法 M 提供了定义声明但未提供实现声明，则适用以下限制：

-   创建指向该方法的委托是编译时错误（§7.6.10.5）。
-   在转换为表达式树类型的匿名函数内部引用 M 是编译时错误（§6.5.2）。
-   作为 M 调用的一部分出现的表达式不影响明确赋值状态（§5.3），这可能导致编译时错误。
-   M 不能作为应用程序的入口点（§3.1）。

部分方法对于允许类型声明的一个部分自定义另一部分的行为非常有用——例如，由工具生成的部分。请考虑以下部分类声明：

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

如果在没有其他部分的情况下编译此类，则定义的部分方法声明及其调用将被移除，并且生成的组合类声明将等同于以下内容：

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

然而，假设提供了另一部分，其中提供了部分方法的实现声明：

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

那么生成的组合类声明将等同于以下内容：

```csharp
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

**CHRIS SELLS**

在引入部分方法之前，模式是使用类似以下的虚方法：

```csharp
class Base {
    public void Foo() { HelpWithFoo(); ... }
        // Dynamically bound
    protected virtual void HelpWithFoo() {}
        // Do nothing in the base
}
class Derived : Base {
    protected override void HelpWithFoo() { ... }
}
```

这种方法要求机器生成的代码使用效率较低的动态绑定虚方法，以便“调用”到部分类的另一部分，即使实现在编译时可用。有了部分方法，模式变得更高效：

```csharp
partial class MyClass {          // Machine generated
    public void Foo() { HelpWithFoo(); ... }
        // Statically bound
    partial void HelpWithFoo();
        // Declare the partial method
}
partial class MyClass {          // Human generated
    partial void HelpWithFoo() { ... }
        // Implement the partial method
}
```

> **ERIC LIPPERT** Chris 的观点很有道理。我还要补充一点，需要考虑的成本不仅仅是执行虚调用所需的额外几纳秒。假设你有一个机器生成的类，其中可能有数百个可扩展点，而机器生成的代码希望调用用户生成侧定义的辅助方法。如果用户生成侧的作者只想实现其中一个，所有调用站点的代码和所有方法的元数据仍然会被生成。部分方法真正实现了“按需付费”：你只对实际使用的可扩展点承担额外的代码大小。

### 10.2.8 名称绑定

虽然可扩展类型的每个部分必须在同一命名空间内声明，但这些部分通常在不同的命名空间声明中编写。因此，每个部分可能存在不同的 using 指令（§9.4）。在解释一个部分内的简单名称（§7.5.2）时，仅考虑封闭该部分的命名空间声明（s）的 using 指令。这可能导致同一标识符在不同部分中具有不同的含义：

```csharp
namespace N
{
    using List = System.Collections.ArrayList;
    partial class A
    {
        List x;    // x has type System.Collections.ArrayList
    }
}

namespace N
{
    using List = Widgets.LinkedList;
    partial class A
    {
        List y;    // y has type Widgets.LinkedList
    }
}
```

## 10.3 类成员

类的成员由其 *类成员声明* 引入的成员以及从直接基类继承的成员组成。

```
class-member-declarations:
    class-member-declaration
    class-member-declarations class-member-declaration

class-member-declaration:
    constant-declaration
    field-declaration
    method-declaration
    property-declaration
    event-declaration
    indexer-declaration
    operator-declaration
    constructor-declaration
    destructor-declaration
    static-constructor-declaration
    type-declaration
```

类类型的成员分为以下几类：

-   常量，表示与类关联的常量值（§10.4）。
-   字段，即类的变量（§10.5）。
-   方法，实现类可以执行的计算和操作（§10.6）。
-   属性，定义命名特征以及与读取和写入这些特征相关联的操作（§10.7）。
-   事件，定义类可以生成的通知（§10.8）。
-   索引器，允许以与数组相同的方式（语法上）对类的实例进行索引（§10.9）。
-   运算符，定义可应用于类实例的表达式运算符（§10.10）。
-   实例构造函数，实现初始化类实例所需的操作（§10.11）。
-   析构函数，实现在类实例被永久丢弃之前执行的操作（§10.13）。
-   静态构造函数，实现初始化类本身所需的操作（§10.12）。
-   类型，表示局部于类的类型（§10.3.8）。

可以包含可执行代码的成员统称为类类型的 *函数成员*。类类型的函数成员是该类类型的方法、属性、事件、索引器、运算符、实例构造函数、析构函数和静态构造函数。



类声明会创建一个新的声明空间 (§3.3)，并且由类声明直接包含的类成员声明会在此声明空间中引入新的成员。以下规则适用于类成员声明：

- 实例构造函数、析构函数和静态构造函数必须与直接外围的类具有相同的名称。所有其他成员的名称必须与直接外围的类的名称不同。
- 常量、字段、属性、事件或类型的名称必须与同一类中声明的所有其他成员的名称不同。
- 方法的名称必须与同一类中声明的所有其他非方法名称不同。此外，方法的签名 (§3.6) 必须与同一类中声明的所有其他方法的签名不同，并且同一类中声明的两个方法不能仅因 ref 和 out 而签名不同。
- 实例构造函数的签名必须与同一类中声明的所有其他实例构造函数的签名不同，并且同一类中声明的两个构造函数不能仅因 ref 和 out 而签名不同。
- 索引器的签名必须与同一类中声明的所有其他索引器的签名不同。
- 运算符的签名必须与同一类中声明的所有其他运算符的签名不同。

类类型的继承成员 (§10.3.3) 不是类声明空间的一部分。因此派生类允许声明与继承成员具有相同名称或签名的成员（实际上隐藏了继承的成员）。

## 10.3.1 实例类型

每个类声明都有一个关联的绑定类型 (§4.4.3)，称为实例类型。对于泛型类声明，实例类型是通过从类型声明创建构造类型 (§4.4) 形成的，其中提供的每个类型参数都是相应的类型参数。由于实例类型使用类型参数，它只能在类型参数处于作用域内时使用——即在类声明内部。实例类型是类声明内部编写的代码中 this 的类型。对于非泛型类，实例类型就是声明的类。以下是几个类声明及其实例类型的示例：

```
class A<T>
{
    class B {}        // Instance type: A<T>.B
    class C<U> {}     // Instance type: A<T>.C<U>
}
class D {}            // Instance type: D
```

## 10.3.2 构造类型的成员

构造类型的非继承成员是通过为成员声明中的每个 *类型参数* 替换构造类型的相应 *类型实参* 而获得的。替换过程基于类型声明的语义含义，而不仅仅是文本替换。

例如，给定泛型类声明

```
~~~
class Gen<T,U>
{
    public T[,] a;

    public void G(int i, T t, Gen<U,T> gt) {...}

    public U Prop { get {...} set {...} }

    public int H(double d) {...}
}
~~~
```

构造类型 Gen<int[,],IComparable<string>> 具有以下成员：

```
~~~
public int[,][] a;

public void G(int i, int[,] t, Gen<IComparable<string>,int[,]> gt) {...}

public IComparable<string> Prop { get {...} set {...} }

public int H(double d) {...}
~~~
```

泛型类声明 *Gen* 中成员 *a* 的类型是“*T* 的二维数组”，因此上面构造类型中成员 *a* 的类型是“int 的一维数组的二维数组”，即 int[,][]。

在实例函数成员内部，*this* 的类型是包含声明的实例类型 (§10.3.1)。

> **JON SKEET**  通过替换处理泛型会导致明显的棘手情况。以下代码会做什么？

```
~~~
public class Puzzle<T> {
    public void Method(int i) {}
    public void Method(T t) {}
}
...
new Puzzle<int>().Method(10);
~~~
```

> “替换”导致两个方法具有完全相同的签名——那么 Method(10) 表达式调用的是哪一个？我承认如果不查阅或尝试，我就不知道答案。我强烈建议在可能的情况下避免此类歧义。在我的经验中，它最有可能发生在索引器对上，索引器可以按位置（一个 int）或键（一个类型参数）查找项目。

> **ERIC LIPPERT** 在 C# 2.0 泛型的早期设计中，语言设计者考虑过甚至禁止 *声明* 一个类，该类可能被构造从而产生像 Jon 描述的那样的签名歧义。不幸的是，该限制随后使某些明显可取的模式变得非法：

```
class C<T> { public C(T t) { ... } public C(Stream serializedState) { ... } }
```

仅仅因为某人日后可能会创建 C<Stream>，就禁止声明 C<T> 是否合法？这似乎太过分了。

即便如此，创建在构造时可能具有歧义签名的类型然后实际进行此类构造是一种极差的编程实践。这样做在某些人为构造的情况下可能会在 CLR 中暴露实现定义的行为。

泛型类的所有成员都可以使用任何外围类的类型参数，无论是直接使用还是作为构造类型的一部分。当特定闭合构造类型 (§4.4.2) 在运行时使用时，每个类型参数的使用都会被替换为提供给构造类型的实际类型实参。例如：

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
```

```
class Application
{
    static void Main() {
        C<int> x1 = new C<int>(1);
        Console.WriteLine(x1.f1);          // Prints 1

        C<double> x2 = new C<double>(3.1415);
        Console.WriteLine(x2.f1);          // Prints 3.1415
    }
}
```

## 10.3.3 继承

类继承其直接基类类型的成员。继承意味着类隐式包含其直接基类类型的所有成员，除了基类的实例构造函数、析构函数和静态构造函数。这里列出了继承的一些重要方面：

- 继承是传递的。如果 C 派生自 B，且 B 派生自 A，则 C 继承 B 中声明的成员以及 A 中声明的成员。
- 派生类扩展其直接基类。派生类可以向继承的成员添加新成员，但不能删除继承成员的定义。
- 实例构造函数、析构函数和静态构造函数不会被继承，但所有其他成员都会被继承，无论其声明的可访问性 (§3.5) 如何。然而，根据其声明的可访问性，继承的成员在派生类中可能无法访问。

> **JON SKEET** 偶尔，开发人员会询问为什么实例构造函数不被继承。我的观点是只有特定类知道创建有效实例所需的信息。例如，如果实例构造函数被继承，所有类都必须具有无参数构造函数（因为 object 有）。在不指定文件名或句柄的情况下创建新的 FileStream 会意味着什么？

- 派生类可以通过声明具有相同名称或签名的新成员来隐藏 (§3.7.1.2) 继承的成员。然而请注意，隐藏继承成员并不会删除该成员——它只是使该成员无法直接通过派生类访问。
- 类的实例包含该类及其基类中声明的所有实例字段的集合，并且从派生类类型到其任何基类类型存在隐式转换 (§6.1.6)。因此，对某个派生类实例的引用可以被视为对其中任何一个基类实例的引用。
- 类可以声明虚方法、属性和索引器，并且派生类可以重写这些函数成员的实现。这使得类能够表现出多态行为，其中函数成员调用执行的操作取决于调用该函数成员的实例的运行时类型。

构造类类型的继承成员是直接基类类型 (§10.1.4.1) 的成员，该基类类型是通过将构造类型的类型实参替换为基类规范中相应类型参数的每次出现而找到的。这些成员反过来又通过为成员声明中的每个类型参数替换基类规范的相应类型实参而转换。

```csharp
class B<U>
{
    public U F(long index) {...}
}

class D<T>: B<T[]>
{
    public T G(string s) {...}
}
```



在上面的示例中，构造类型 D<int> 具有一个非继承成员 public int G(string s)，它是通过用类型实参 int 替换类型参数 T 得到的。D<int> 还具有一个来自类声明 B 的继承成员。该继承成员的确定方式是：首先通过在基类规范 B<T[]> 中将 T 替换为 int，确定 D<int> 的基类类型 B<int[]>。然后，作为 B 的类型实参，将 int[] 替换 public U F(long index) 中的 U，从而得到继承成员 public int[] F(long index)。

## 10.3.4 new 修饰符

类成员声明允许声明与继承成员具有相同名称或签名的成员。发生这种情况时，称派生类成员隐藏了基类成员。隐藏继承成员不被视为错误，但确实会导致编译器发出警告。若要抑制该警告，派生类成员的声明可以包含 new 修饰符，以指示该派生成员意图隐藏基成员。本主题在 §3.7.1.2 中进一步讨论。

如果声明中包含 new 修饰符，但并未隐藏继承成员，则会发出相应警告。通过移除 new 修饰符可抑制该警告。

## 10.3.5 访问修饰符

类成员声明可以具有五种可能的声明可访问性之一（§3.5.1）：public、protected internal、protected、internal 或 private。除 protected internal 组合外，指定多个访问修饰符是编译时错误。当类成员声明不包含任何访问修饰符时，假定为 private。

## 10.3.6 组成类型

成员声明中使用的类型称为该成员的组成类型。可能的组成类型包括：常量、字段、属性、事件或索引器的类型；方法或运算符的返回类型；以及方法、索引器、运算符或实例构造函数的参数类型。成员的组成类型必须至少与该成员本身一样可访问（§3.5.4）。

## 10.3.7 静态成员和实例成员

类成员要么是静态成员，要么是实例成员。一般来说，将静态成员视为属于类类型、实例成员视为属于对象（类类型的实例）是有用的。

当字段、方法、属性、事件、运算符或构造函数声明包含 static 修饰符时，它声明静态成员。此外，常量或类型声明隐式声明静态成员。静态成员具有以下特征：

- 当在形式为 E.M 的成员访问（§7.6.4）中引用静态成员 M 时，E 必须表示包含 M 的类型。E 表示实例是编译时错误。
- 静态字段标识一个存储位置，由给定封闭类类型的所有实例共享。无论创建给定封闭类类型的多少个实例，静态字段始终只有一个副本。
- 静态函数成员（方法、属性、事件、运算符或构造函数）不对特定实例进行操作，在此类函数成员中引用 this 是编译时错误。

当字段、方法、属性、事件、索引器、构造函数或析构函数声明不包含 static 修饰符时，它声明实例成员。（实例成员有时称为非静态成员。）实例成员具有以下特征：

- 当在形式为 E.M 的成员访问（§7.6.4）中引用实例成员 M 时，E 必须表示包含 M 的类型的实例。E 表示类型是绑定期错误。
- 类的每个实例都包含该类所有实例字段的一组单独副本。
- 实例函数成员（方法、属性、索引器、实例构造函数或析构函数）对类的给定实例进行操作，并且可以通过 this（§7.6.7）访问该实例。

以下示例说明访问静态成员和实例成员的规则：

```
class Test
{
    int x;
    static int y;

    void F() {
        x = 1;        // Okay: same as this.x = 1
        y = 1;        // Okay: same as Test.y = 1
    }

    static void G() {
        x = 1;        // Error: cannot access this.x
        y = 1;        // Okay: same as Test.y = 1
    }
}
```

```
    static void Main() {
        Test t = new Test();       // Okay
        t.x = 1;                   // Error: cannot access static
        t.y = 1;                   //        member through instance
        Test.x = 1;                // Error: cannot access instance member
                                   //        through type
        Test.y = 1;                // Okay
    }
```

F 方法表明，在实例函数成员中，可以使用*简单名称*（§7.6.2）访问实例成员和静态成员。G 方法表明，在静态函数成员中，通过*简单名称*访问实例成员是编译时错误。Main 方法表明，在*成员访问*（§7.6.4）中，实例成员必须通过实例访问，静态成员必须通过类型访问。

## 10.3.8 嵌套类型

在类或结构体声明中声明的类型称为*嵌套类型*。在编译单元或命名空间中声明的类型称为*非嵌套类型*。

> > **乔恩·斯基特** 我听到“顶级类型”这个说法比“非嵌套类型”更常用——而且我毫不怀疑我自己也传播过这个非标准术语。考虑到绝大多数类型都是非嵌套的，感觉描述性术语应该是正面的，而不只是表示没有嵌套。不管怎样，这就是我的借口，其他人也欢迎借用。

在示例

```
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

中，类 B 是嵌套类型，因为它声明在类 A 中；类 A 是非嵌套类型，因为它声明在编译单元中。

> > **布拉德·艾布拉姆斯** 我并不太喜欢可重用库中的公开可访问嵌套类型。嵌套类型的可发现性并不好。更重要的是，我们已经有一种分组机制——命名空间——应该用它来表示相关类型。

### 10.3.8.1 完全限定名

嵌套类型的完全限定名（§3.8.1）为 S.N，其中 S 是声明类型 N 的类型的完全限定名。

### 10.3.8.2 声明可访问性

非嵌套类型可以具有 public 或 internal 声明可访问性，默认具有 internal 声明可访问性。嵌套类型也可以具有这些形式的声明可访问性，另外还可以具有一种或多种其他形式的声明可访问性，具体取决于包含类型是类还是结构体：

- 在类中声明的嵌套类型可以具有五种声明可访问性中的任意一种（public、protected internal、protected、internal 或 private），并且与其他类成员一样，默认具有 private 声明可访问性。
- 在结构体中声明的嵌套类型可以具有三种声明可访问性中的任意一种（public、internal 或 private），并且与其他结构体成员一样，默认具有 private 声明可访问性。

示例

```
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
```
```

```
~~~csharp
        public void AddToBack(object o) {...}
        public object RemoveFromFront() {...}
        public object RemoveFromBack() {...}
        public int Count { get {...} }
        }
~~~
```

声明了一个私有嵌套类 Node。

### 10.3.8.3 *隐藏*

嵌套类型可以隐藏（§7.3.1）基成员。嵌套类型声明上允许使用 *new* 修饰符，以便可以显式表达隐藏。示例

```
~~~csharp
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
~~~
```

展示了一个嵌套类 M，它隐藏了 Base 中定义的方法 M。

### 10.3.8.4 *this* 访问

嵌套类型与其包含类型在 *this 访问*（§7.6.7）方面没有特殊关系。具体而言，嵌套类型中的 *this* 不能用于引用包含类型的实例成员。在嵌套类型需要访问其包含类型的实例成员的情况下，可以通过提供来提供访问


将包含类型的实例的 `this` 作为嵌套类型的构造函数参数传递。下面的示例

```csharp
using System;
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
```

展示了这种技术。C 的实例创建 Nested 的实例，并将自身的 `this` 传递给 Nested 的构造函数，以便后续访问 C 的实例成员。

> **JON SKEET** 规范中的这一节乍看之下可能有些奇怪：为什么要费心规定你不能做什么？为什么有人会期望从嵌套类型的实例访问包含类型的实例？嗯，在 Java 中，内部类正是这样工作的。要实现类似 C# 的嵌套类型行为，你需要将嵌套类型声明为 static——这与 C# 中的静态类完全不同！

### 10.3.8.5 对包含类型的私有成员和受保护成员的访问

嵌套类型可以访问其包含类型可访问的所有成员，包括包含类型中声明为私有和受保护可访问性的成员。下面的示例

```csharp
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
```

展示了一个类 C，其中包含嵌套类 Nested。在 Nested 内部，方法 G 调用 C 中定义的静态方法 F，而 F 具有私有声明可访问性。

> > **JON SKEET** 同样，这种行为与 Java 中的行为不同：在 Java 中，外部类型可以访问嵌套类型的私有成员，但反过来不行。我认为 C# 的做法更合理。它还允许一些不错的模式，例如创建一个带有私有构造函数的抽象类：所有派生类都必须嵌套在该抽象类中。奇怪的是，我发现这种行为的主要用例是模拟 Java 枚举。

嵌套类型还可以访问其包含类型的基类型中定义的受保护成员。在下面的示例中

```csharp
using System;

class Base
{
    protected void F() {
        Console.WriteLine("Base.F");
    }
}

class Derived: Base
{
    public class Nested
    {
        public void G() {
            Derived d = new Derived();
            d.F();          // Okay
        }
    }
}
class Test
{
    static void Main() {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```

嵌套类 Derived.Nested 通过 Derived 的实例调用 Derived 的基类 Base 中定义的受保护方法 F。

### 10.3.8.6 泛型类中的嵌套类型

泛型类声明可以包含嵌套类型声明。封闭类的类型参数可以在嵌套类型中使用。嵌套类型声明可以包含仅适用于该嵌套类型的附加类型参数。

泛型类声明中包含的每个类型声明都隐式地是泛型类型声明。编写对泛型类型中嵌套的类型的引用时，必须指定包含它的构造类型，包括其类型实参。但是，在外部类内部，嵌套类型可以不加限定地使用；构造嵌套类型时，可以隐式使用外部类的实例类型。下面的示例展示了引用由 Inner 创建的构造类型的三种不同且正确的方式；前两种是等效的：

```csharp
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }

    static void F(T t) {
        Outer<T>.Inner<string>.F(t, "abc");   // These two statements
        Inner<string>.F(t, "abc");            // have the same effect

        Outer<int>.Inner<string>.F(3, "abc"); // This type is different

        Outer.Inner<string>.F(t, "abc");      // Error: Outer needs type arg
    }
}
```

尽管这是一种糟糕的编程风格，但嵌套类型中的类型参数可以隐藏外部类型中声明的成员或类型参数：

```csharp
class Outer<T>
{
    class Inner<T>    // Valid: hides Outer's T
    {
        public T t;   // Refers to Inner's T
    }
}
```

## 10.3.9 保留成员名称

为了便于底层 C# 运行时实现，对于每个为属性、事件或索引器的源成员声明，实现必须根据成员声明的种类、名称和类型保留两个方法签名。如果程序声明了签名与这些保留签名之一匹配的成员，则属于编译时错误，即使底层运行时实现并未使用这些保留。

保留名称不会引入声明；因此它们不参与成员查找。但是，声明所关联的保留方法签名确实参与继承（§10.3.3），并且可以用 `new` 修饰符隐藏（§10.3.4）。

保留这些名称有三个目的：

- 它允许底层实现使用普通标识符作为方法名，以 get 或 set 访问 C# 语言功能。
- 它允许其他语言互操作，使用普通标识符作为方法名，以 get 或 set 访问 C# 语言功能。
- 它通过使保留成员名称的具体细节在所有 C# 实现中保持一致，帮助确保一个符合规范的编译器接受的源能被另一个编译器接受。

析构函数（§10.13）的声明也会导致保留一个签名（§10.3.9.4）。

### 10.3.9.1 为属性保留的成员名称

对于类型为 T 的属性 P（§10.7），保留以下签名：

```
T get_P();
void set_P(T value);
```

即使属性是只读或只写的，这两个签名也都会保留。

> > **BILL WAGNER** 尽管你可以编写名为 `get_<something>` 和 `set_<something>` 的方法，但如果 `<something>` 不是属性名，则不推荐使用这种技术。避免这样做将最大限度地减少将来更新代码的需要。

在下面的示例中

```csharp
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

类 A 定义了只读属性 P，因此保留了 get_P 和 set_P 方法的签名。类 B 派生自 A，并隐藏了这两个保留签名。该示例产生以下输出：

```
123
123
456
```

### 10.3.9.2 为事件保留的成员名称

对于委托类型为 T 的事件 E（§10.8），保留以下签名：

```
void add_E(T handler);
void remove_E(T handler);
```

### 10.3.9.3 为索引器保留的成员名称

对于类型为 T、参数列表为 L 的索引器（§10.9），保留以下签名：

```
T get_Item(L);
void set_Item(L, T value);
```

即使索引器是只读或只写的，这两个签名也都会保留。此外，成员名称 Item 也会保留。

### 10.3.9.4 为析构函数保留的成员名称

对于包含析构函数（§10.13）的类，保留以下签名：

```
void Finalize();
```

## 10.4 常量

常量是一种类成员，表示一个常量值——一个可以在编译时计算的值。常量声明引入一个或多个给定类型的常量。

```
constant-declaration:
    attributes_opt constant-modifiers_opt const type constant-declarators ;
```

```
constant-modifiers:
    constant-modifier
    constant-modifiers constant-modifier
```

- new
- public
- protected
- internal
- private

```
constant-declarators:
    constant-declarator
    constant-declarators , constant-declarator
```




```
constant-declarator:
    identifier = constant-expression
```

*常量声明*可以包含一组特性（§17）、一个 new 修饰符（§10.3.4），以及四个访问修饰符（§10.3.5）的有效组合。特性和修饰符应用于该*常量声明*所声明的所有成员。尽管常量被视为静态成员，但*常量声明*既不要求也不允许 static 修饰符。同一修饰符在常量声明中出现多次是错误的。

*常量声明*的*类型*指定该声明所引入的成员的类型。类型后跟一个*常量声明符*列表，每个*常量声明符*引入一个新成员。*常量声明符*由一个命名该成员的*标识符*组成，其后跟一个“=”标记，再跟一个给出该成员值的*常量表达式*（§7.19）。

常量声明中指定的*类型*必须是 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool、string、一个*枚举类型*或一个*引用类型*。每个*常量表达式*必须产生目标类型的值，或产生可通过隐式转换（§6.1）转换为目标类型的值。

> **乔恩·斯基特**  在面向公共语言基础结构时，这里包含 decimal 很有意思。其他所有类型在 CLI 中都有字面量表示，而 decimal 没有。Microsoft C# 编译器通过创建静态只读字段声明来实现适当行为，尽管用 `DecimalConstantAttribute` 修饰。DateTime 存在一个 Microsoft 特性，但 C# 不允许 DateTime 常量。

常量的*类型*的可访问性必须至少与常量本身相同（§3.5.4）。

在表达式中，常量的值通过*简单名称*（§7.6.2）或*成员访问*（§7.6.4）获取。

常量本身可以参与*常量表达式*。因此，常量可用于任何需要*常量表达式*的构造。此类构造的示例包括 case 标签、goto case 语句、枚举成员声明、特性以及其他常量声明。

如 §7.19 所述，*常量表达式*是可在编译时完全求值的表达式。由于创建 string 以外的*引用类型*的非 null 值的唯一方式是应用 new 运算符，并且由于*常量表达式*中不允许使用 new 运算符，因此 string 以外的*引用类型*常量的唯一可能值是 null。

当需要为常量值提供符号名称，但该值的类型不允许在常量声明中使用，或者该值无法通过常量表达式在编译时计算时，可以改用 readonly 字段（§10.5.2）。

声明多个常量的一个常量声明，等价于多个具有相同特性、修饰符和类型的单个常量声明。例如，

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

> 克里斯·塞尔斯  从可读性角度看，我发现同一行上的多个声明——无论是常量还是非常量、静态还是实例、字段还是局部变量——都难以解读。我倾向于每行只放一个声明，最好同时考虑引用的局部性。

只要依赖关系不具有循环性质，常量就允许依赖同一程序中的其他常量。编译器会自动安排以适当的顺序计算常量声明。在下面的示例中

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

编译器首先计算 A.Y，然后计算 B.Z，最后计算 A.X，并按该顺序生成值 10、11 和 12。常量声明可以依赖其他程序中的常量，但此类依赖只能在一个方向上存在。参考上面的示例，如果 A 和 B 声明在不同程序中，则 A.X 可以依赖 B.Z，但 B.Z 就不能同时依赖 A.Y。

## 10.5 字段

*字段*是表示与对象或类关联的变量的成员。*字段声明*引入一个或多个给定类型的字段。

```
field-declaration:
    attributes_opt  field-modifiers_opt  type  variable-declarators  ;
```

```
field-modifiers:
    field-modifier
    field-modifiers  field-modifier
```

```
field-modifier:
    new
    public
    protected
    internal
    private
    static
    readonly
    volatile
```

```
variable-declarators:
    variable-declarator
    variable-declarators  ,  variable-declarator
```

```
variable-declarator:
    identifier
    identifier  =  variable-initializer
```

```
variable-initializer:
    expression
    array-initializer
```

*字段声明*可以包含一组特性（§17）、一个 new 修饰符（§10.3.4）、四个访问修饰符（§10.3.5）的有效组合，以及一个 static 修饰符（§10.5.1）。此外，*字段声明*可以包含 readonly 修饰符（§10.5.2）或 volatile 修饰符（§10.5.3），但不能同时包含两者。特性和修饰符应用于该*字段声明*所声明的所有成员。同一修饰符在字段声明中出现多次是错误的。

*字段声明*的*类型*指定该声明所引入的成员的类型。类型后跟一个*变量声明符*列表，每个*变量声明符*引入一个新成员。*变量声明符*由一个命名该成员的*标识符*组成，其后可选跟一个“=”标记和一个*变量初始值设定项*（§10.5.5），该初始值设定项给出该成员的初始值。

字段的*类型*的可访问性必须至少与字段本身相同（§3.5.4）。

在表达式中，字段的值通过*简单名称*（§7.6.2）或*成员访问*（§7.6.4）获取。非只读字段的值通过*赋值*（§7.17）修改。非只读字段的值可以使用后缀递增和递减运算符（§7.6.9）以及前缀递增和递减运算符（§7.7.5）来获取和修改。

声明多个字段的一个字段声明，等价于多个具有相同特性、修饰符和类型的单个字段声明。例如，

```
```csharp
class A
{
    public static int X = 1, Y, Z = 100;
}
```
```

等价于

```
```csharp
class A
{
    public static int X = 1;
    public static int Y;
    public static int Z = 100;
}
```
```

### 10.5.1 静态字段和实例字段

当字段声明包含 static 修饰符时，该声明引入的字段是*静态字段*。当不存在 static 修饰符时，该声明引入的字段是*实例字段*。静态字段和实例字段是 C# 支持的几种变量（§5）中的两种，有时分别称为*静态变量*和*实例变量*。

静态字段不属于特定实例；相反，它在封闭类型（§4.4.2）的所有实例之间共享。无论创建多少个封闭类类型的实例，关联的应用程序域中都始终只有静态字段的一个副本。

例如：

```
```csharp
class C<V>
{
    static int count = 0;

    public C() {
        count++;
    }
}
```
```

```
public static int Count {
    get { return count; }
}
}
```

```
class Application
{
    static void Main() {
        C<int> x1 = new C<int>();
        Console.WriteLine(C<int>.Count);    // Prints 1
        C<double> x2 = new C<double>();
        Console.WriteLine(C<int>.Count);    // Prints 1
        C<int> x3 = new C<int>();
        Console.WriteLine(C<int>.Count);    // Prints 2
    }
}
```

实例字段属于某个实例。具体来说，类的每个实例都包含该类所有实例字段的独立集合。

当在形式为 E.M 的*成员访问*（§7.6.4）中引用字段时，如果 M 是静态字段，则 E 必须表示包含 M 的类型；如果 M 是实例字段，则 E 必须表示包含 M 的类型的实例。

静态成员和实例成员之间的差异将在 §10.3.7 中进一步讨论。

### 10.5.2 只读字段

当*字段声明*包含 readonly 修饰符时，该声明引入的字段是只读字段。对 readonly 字段的直接赋值只能作为该声明的一部分，或出现在同一类的实例构造函数或静态构造函数中。（在这些上下文中，可以对 readonly 字段多次赋值。）具体来说，只有在以下上下文中才允许对 readonly 字段进行直接赋值：

- 在引入该字段的*变量声明符*中（通过在声明中包含*变量初始值设定项*）。
- 对于实例字段，在包含该字段声明的类的实例构造函数中；对于静态字段，在包含该字段声明的类的静态构造函数中。这些也是唯一可以有效地将 *readonly* 字段作为 *out* 或 *ref* 参数传递的上下文。

在任何其他上下文中尝试给 readonly 字段赋值，或将其作为 out 或 ref 参数传递，都是编译时错误。




> > **VLADIMIR RESHETNIKOV** 只有该对象的实例只读字段可以在实例构造函数中被赋值，而不能赋值同一类型的其他对象的字段：

~~~csharp
class A
{
    readonly int x;

    A(A a)
    {
        this.x = 1;    // Okay
        a.x = 1;       // Error CS0191: A read-only field
                       // cannot be assigned to
    }
}
~~~

> > 此外，即使该函数位于构造函数中，只读字段也不能在匿名函数中被赋值（或作为 ref 或 out 参数传递）。

### 10.5.2.1 使用静态只读字段作为常量

静态只读字段在需要为常量值提供符号名称时很有用，但当该值的类型不允许在 const 声明中使用，或该值无法在编译时计算时。示例中

~~~csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte red, green, blue;

    public Color(byte r, byte g, byte b) {
        red = r;
        green = g;
        blue = b;
    }
}
~~~

Black、White、Red、Green 和 Blue 成员无法声明为 const 成员，因为它们的值无法在编译时计算。将它们声明为 static readonly 而不是 const 效果基本相同。

### 10.5.2.2 常量和静态只读字段的版本控制

常量和只读字段具有不同的二进制版本语义。当表达式引用常量时，常量的值在编译时获取，但当表达式引用只读字段时，字段的值要到运行时才获取。考虑一个由两个独立程序组成的应用程序：

~~~csharp
using System;

namespace Program1
{
    public class Utils
    {
        public static readonly int X = 1;
    }
}

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

`Program1` 和 `Program2` 命名空间表示两个分别编译的程序。因为 `Program1.Utils.X` 被声明为 `static readonly` 字段，`Console.WriteLine` 语句输出的值在编译时未知，而是在运行时获取。因此，如果 `X` 的值被更改并且 `Program1` 被重新编译，`Console.WriteLine` 语句将输出新值，即使 `Program2` 未被重新编译。然而，如果 `X` 是一个常量，`X` 的值将在 `Program2` 编译时获取，并且在 `Program2` 重新编译之前不受 `Program1` 更改的影响。

> > **BILL WAGNER** 这一讨论证明了为什么 `readonly` 通常应优先于 `const`。

> > **JON SKEET** 我基本同意 Bill 的观点，即 `readonly` 通常应优先使用，但在某些情况下 `const` 也有好处。由常量构成的表达式可以在编译时求值，而不是每次访问时重新计算。对于计算字符串常量的情况，这种做法还可以避免每次求值表达式时创建新的字符串。某些数字确实 *是* 自然常数：例如一秒中的毫秒数，或 `int` 的最小值。当值绝对不可能改变时，使用 `const` 是合理的。当有任何疑问时，`readonly` 更安全。

## 10.5.3 易失字段

当字段声明包含 volatile 修饰符时，由该声明引入的字段为易失字段。

对于非易失字段，重排序指令的优化技术可能导致在没有同步（如 lock 语句（§8.12）提供的同步）访问字段的多线程程序中出现意外且不可预测的结果。这些优化可以由编译器、运行时系统或硬件执行。对于易失字段，此类重排序优化受到限制：

- 对易失字段的读取称为易失读取。易失读取具有“获取语义”；也就是说，它保证在指令序列中在其之后发生的任何内存引用之前发生。
- 对易失字段的写入称为易失写入。易失写入具有“释放语义”；也就是说，它保证在指令序列中写入指令之前的任何内存引用之后发生。

这些限制确保所有线程都会按执行顺序观察到任何其他线程执行的易失写入。符合规范的实现不需要提供从所有执行线程看到的易失写入的单一总顺序。易失字段的类型必须是以下之一：

- 引用类型。
- 类型 byte、sbyte、short、ushort、int、uint、char、float、bool、System.IntPtr 或 System.UIntPtr。
- 枚举类型，其枚举基础类型为 byte、sbyte、short、ushort、int 或 uint。

示例

~~~csharp
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

        // Wait for Thread2 to signal that it has a
        // result by setting finished to true
        for (;;) {
            if (finished) {
                Console.WriteLine("result = {0}", result);
                return;
            }
        }
    }
}
~~~

生成以下输出：

```
result = 143
```

在此示例中，`Main` 方法启动一个新线程运行 `Thread2` 方法。该方法将值存储到名为 `result` 的非易失字段中，然后将 `true` 存储到易失字段 `finished` 中。主线程等待 `finished` 字段被设置为 `true`，然后读取 `result` 字段。由于 `finished` 已声明为易失，主线程必须从 `result` 字段读取值 `143`。如果 `finished` 字段未声明为易失，则允许对 `result` 的存储在主线程中在对 `finished` 的存储之后才可见，从而主线程可能从 `result` 字段读取值 `0`。将 `finished` 声明为易失字段可防止此类不一致。

> > **JOSEPH ALBAHARI** 始终在 lock 语句（§8.12）内访问的字段无需使用 volatile 关键字声明。因此，运行时必须确保 `Monitor.Enter` 和 `Monitor.Exit` 之间使用的字段的任何排序优化不会超出这些语句的范围。

> > **JON SKEET** 无锁并发代码很难写对。易失性的精确保证很难推理，使得在阅读代码时很难明显看出代码是否真正正确。我倾向于将低级无锁代码的细节留给专家，而更喜欢基于专家编写的高级库构建。当然，规范详细说明行为对这些专家仍然很重要。

## 10.5.4 字段初始化

字段的初始值，无论是静态字段还是实例字段，都是字段类型默认值（§5.2）。在默认初始化发生之前无法观察字段的值；因此字段永远不会“未初始化”。示例

~~~csharp
using System;
class Test
{
    static bool b;
    int i;
    static void Main() {
        Test t = new Test();
        Console.WriteLine("b = {0}, i = {1}", b, t.i);
    }
}
~~~

生成输出
b = false, i = 0

因为 b 和 i 都自动初始化为默认值。

## 10.5.5 变量初始化器

字段声明可以包含变量初始化器。对于静态字段，变量初始化器对应于在类初始化期间执行的赋值语句。对于实例字段，变量初始化器对应于在创建类的实例时执行的赋值语句。

示例

~~~csharp
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
~~~

生成输出
x = 1.4142135623731, i = 100, s = Hello

因为在静态字段初始化器执行时对 x 进行赋值，而在实例字段初始化器执行时对 i 和 s 进行赋值。



§10.5.4 中描述的默认值初始化适用于所有字段，包括具有变量初始值设定项的字段。因此，当一个类被初始化时，该类中的所有静态字段首先被初始化为默认值，然后静态字段初始值设定项按文本顺序执行。同样地，当一个类的实例被创建时，该实例中的所有实例字段首先被初始化为默认值，然后实例字段初始值设定项按文本顺序执行。

具有变量初始值设定项的静态字段可能在其默认值状态下被观察到，但这在风格上是强烈不鼓励的。示例

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

表现出这种行为。尽管 a 和 b 的定义是循环的，但程序是有效的。其输出结果为

a = 1, b = 2

因为静态字段 a 和 b 在其初始值设定项执行之前被初始化为 0（int 的默认值）。当 a 的初始值设定项运行时，b 的值为零，因此 a 被初始化为 1。当 b 的初始值设定项运行时，a 的值已经是 1，因此 b 被初始化为 2。

> BILL WAGNER  这种情况下更容易理解，当静态变量在多个源单元中的部分类中声明时。此外，由于你不知道源单元的包含顺序，因此无法知道哪个变量会先被初始化。

### 10.5.5.1 静态字段初始化

类的静态字段变量初始值设定项对应于按其在类声明中出现的文本顺序执行的赋值序列。如果类中存在静态构造函数（§10.12），则静态字段初始值设定项的执行发生在执行该静态构造函数之前。否则，静态字段初始值设定项在该类的静态字段首次使用之前在实现相关的时间执行。示例

```csharp
using System;

class Test
{
    static void Main() {
        Console.WriteLine("{0} {1}", B.Y, A.X);
    }

    public static int F(string s) {
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

```text
Init A
Init B
1 1
```

或此输出：

```text
Init B
Init A
1 1
```

这种变化是可能的，因为 X 的初始值设定项和 Y 的初始值设定项的执行顺序可能不同；它们仅受约束必须在对这些字段的引用之前发生。然而，在示例中

```csharp
using System;

class Test
{
    static void Main() {
        Console.WriteLine("{0} {1}", B.Y, A.X);
    }

    public static int F(string s) {
        Console.WriteLine(s);
        return 1;
    }
}
class A
{
    static A() {}
    public static int X = Test.F("Init A");
}
class B
{
    static B() {}
    public static int Y = Test.F("Init B");
}
```

输出必须是

```text
Init B
Init A
1 1
```

因为关于静态构造函数执行时机的规则（定义在 §10.12 中）规定 B 的静态构造函数（因此 B 的静态字段初始值设定项）必须在 A 的静态构造函数和字段初始值设定项之前运行。

### 10.5.5.2 实例字段初始化

类的实例字段变量初始值设定项对应于在进入该类的任何一个实例构造函数（§10.11.1）时立即执行的赋值序列。变量初始值设定项按其在类声明中出现的文本顺序执行。类实例创建和初始化过程在 §10.11 中进一步描述。

实例字段的变量初始值设定项不能引用正在创建的实例。因此，在变量初始值设定项中引用 this 会导致编译时错误，因为变量初始值设定项通过简单名称引用任何实例成员是编译时错误。

在示例中

```
class A
{
    int x = 1;
    int y = x + 1; // Error: reference to instance member of this
}
```

y 的变量初始值设定项导致编译时错误，因为它引用了正在创建的实例的成员。

## 10.6 方法

一个 *方法* 是实现可由对象或类执行计算或操作的成员。方法使用 *方法声明* 声明：

~~~
method-declaration:
    method-header  method-body

method-header:
    attributes_opt  method-modifiers_opt  partial_opt  return-type  member-name
        type-parameter-list_opt  (  formal-parameter-list_opt  )
        type-parameter-constraints-clauses_opt

method-modifiers:
    method-modifier
    method-modifiers  method-modifier

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

return-type:
    type
    void

member-name:
    identifier
    interface-type  .  identifier

method-body:
    block
    ;
~~~

一个 *方法声明* 可能包括一组 *特性*（§17）以及四个 *访问修饰符*（§10.3.5）和 *new*（§10.3.4）、*static*（§10.6.2）、*virtual*（§10.6.3）、*override*（§10.6.4）、*sealed*（§10.6.5）、*abstract*（§10.6.6）和 *extern*（§10.6.7）修饰符的有效组合。

如果满足以下所有条件，则声明具有修饰符的有效组合：

- 声明包含访问修饰符的有效组合（§10.3.5）。
- 声明不包含重复的相同修饰符。
- 声明最多包含以下修饰符之一：*static*、*virtual* 和 *override*。
- 声明最多包含以下修饰符之一：*new* 和 *override*。
- 如果声明包含 *abstract* 修饰符，则声明不包含以下任何修饰符：*static*、*virtual*、*sealed* 或 *extern*。
- 如果声明包含 *private* 修饰符，则声明不包含以下任何修饰符：*virtual*、*override* 或 *abstract*。
- 如果声明包含 *sealed* 修饰符，则声明也包含 *override* 修饰符。
- 如果声明包含 *partial* 修饰符，则它不包含以下任何修饰符：*new*、*public*、*protected*、*internal*、*private*、*virtual*、*sealed*、*override*、*abstract* 或 *extern*。

方法声明的 *返回类型* 指定方法计算并返回的值的类型。如果方法不返回值，则 *返回类型* 为 *void*。如果声明包含 *partial* 修饰符，则返回类型必须是 *void*。

*成员名称* 指定方法名称。除非方法是显式接口成员实现（§13.4.1），否则 *成员名称* 只是 *标识符*。对于显式接口成员实现，*成员名称* 由 *接口类型* 后跟一个 "." 和一个 *标识符* 组成。

可选的 *类型参数列表* 指定方法类型参数（§10.1.3）。如果指定了 *类型参数列表*，则该方法为 *泛型方法*。如果方法具有 *extern* 修饰符，则不能指定 *类型参数列表*。

可选的 *形式参数列表* 指定方法参数（§10.6.1）。

可选的 *类型参数约束子句* 指定单个类型参数的约束（§10.1.5），并且只有在同时提供了 *类型参数列表* 且方法没有 *override* 修饰符时才可指定。

方法的 *返回类型* 以及 *形式参数列表* 中引用的每种类型必须至少与方法本身一样可访问（§3.5.4）。

对于抽象方法和 extern 方法，*方法体* 仅由一个分号组成。对于 *partial* 方法，*方法体* 可以由分号或 *块* 组成。对于所有其他方法，*方法体* 由 *块* 组成，该块指定在调用方法时执行的语句。

方法的名称、类型参数列表和形式参数列表定义了该方法的签名（§3.6）。具体来说，方法的签名由其名称、类型参数的数量以及其形式参数的数量、修饰符和类型组成。为此目的，方法中出现在形式参数类型中的任何类型参数不是按其名称标识，而是按其在方法类型参数列表中的序数位置标识。返回类型不是方法签名的一部分，类型参数或形式参数的名称也不是。

方法名称必须与同一类中声明的所有其他非方法名称不同。此外，方法的签名必须与同一类中声明的所有其他方法的签名不同，并且同一类中声明的两个方法不能仅因 `ref` 和 `out` 而签名不同。

方法的 *类型参数* 在整个 *方法声明* 中都在作用域内，并且可以用于形成在 *返回类型*、*方法体* 和 *类型参数约束子句* 中处于作用域的类型，但在 *特性* 中不在作用域内。

所有形式参数和类型参数必须具有不同的名称。

### 10.6.1 方法参数

方法参数（如果有）由方法的 *形式参数列表* 声明。

```text
formal-parameter-list:
    fixed-parameters
    fixed-parameters   ,   parameter-array
    parameter-array

fixed-parameters:
    fixed-parameter
    fixed-parameters   ,   fixed-parameter

fixed-parameter:
    attributes_opt   parameter-modifier_opt   type   identifier   default-argument_opt

default-argument:
    =   expression
```

```
parameter-modifier:
    ref
    out
    this
```

```
parameter-array:
    attributes_opt params array-type identifier
```

形参列表由一个或多个以逗号分隔的参数组成，其中只有最后一个可以是参数数组。

固定参数由一组可选的特性（§17）、可选的 ref、out 或 this 修饰符、一个类型、一个标识符以及可选的默认实参组成。每个固定参数声明一个具有给定类型和给定名称的参数。this 修饰符将该方法指定为扩展方法，并且只允许在静态方法的第一个参数上使用。扩展方法在 §10.6.9 中进一步描述。

带默认实参的固定参数称为可选参数，而不带默认实参的固定参数是必需参数。在形参列表中，必需参数不得出现在可选参数之后。

> CHRISTIAN NAGEL 在版本控制方面必须注意可选参数。编译器会采用默认实参，并将其添加到调用方程序集中的调用方。如果默认实参随着代码的新版本更改为新值，而调用方代码未重新编译，则调用方仍包含旧值。

ref 或 out 参数不能有默认实参。默认实参中的表达式必须是以下之一：

- 常量表达式。
- 形如 new S() 的表达式，其中 S 是值类型。
- 形如 default(S) 的表达式，其中 S 是值类型。

该表达式必须能够通过标识转换或可空转换隐式转换为该参数的类型。

如果可选参数出现在实现分部方法声明（§10.2.7）、显式接口成员实现（§13.4.1）或单参数索引器声明（§10.9）中，编译器应发出警告，因为这些成员永远无法以允许省略实参的方式被调用。

*参数数组*由一组可选的*特性*（§17）、params 修饰符、一个*数组类型*和一个标识符组成。参数数组声明一个具有给定数组类型和给定名称的单个参数。参数数组的*数组类型*必须是一维数组类型（§12.1）。在方法调用中，参数数组允许指定一个具有给定数组类型的实参，或者指定零个或多个具有数组元素类型的实参。参数数组在 §10.6.1.4 中进一步描述。

*参数数组*可以出现在可选参数之后，但不能有默认值——省略*参数数组*的实参反而会导致创建一个空数组。

以下示例演示了不同类型的参数：

```csharp
public void M(
    ref int      i,
    decimal      d,
    bool         b = false,
    bool?        n = false,
    string       s = "Hello",
    object       o = null,
    T            t = default(T),
    params int[] a
) { }
```

在 M 的*形参列表*中，i 是必需的 ref 参数；d 是必需的值参数；b、s、o 和 t 是可选的值参数；a 是参数数组。

方法声明为参数、类型参数和局部变量创建单独的声明空间。名称由方法的类型参数列表和形参列表以及方法*块*中的局部变量声明引入此声明空间。方法声明空间的两个成员具有相同名称是错误的。方法声明空间与嵌套声明空间的局部变量声明空间包含相同名称的元素是错误的。

方法调用（§7.6.5.1）会创建该方法形参和局部变量的、特定于该调用的副本，并且调用的实参列表会向新创建的形参赋值或分配变量引用。在方法的*块*内，可以通过*简单名称*表达式（§7.6.2）中的标识符来引用形参。

形参有四类：

- 值参数，声明时不带任何修饰符。
- 引用参数，使用 ref 修饰符声明。
- 输出参数，使用 out 修饰符声明。
- 参数数组，使用 params 修饰符声明。

如 §3.6 所述，ref 和 out 修饰符是方法签名的一部分，但 params 修饰符不是。

### 10.6.1.1 值参数

不带修饰符声明的参数是值参数。值参数对应于一个局部变量，该局部变量从方法调用中提供的相应实参获取其初始值。

当形参是值参数时，方法调用中的相应实参必须是可隐式转换（§6.1）为形参类型的表达式。

允许方法向值参数赋予新值。此类赋值只影响该值参数所表示的本地存储位置；它们对方法调用中给定的实际实参没有影响。

### 10.6.1.2 引用参数

使用 ref 修饰符声明的参数是引用参数。与值参数不同，引用参数不会创建新的存储位置。相反，引用参数表示与方法调用中作为实参给出的变量相同的存储位置。

当形参是引用参数时，方法调用中的相应实参必须由关键字 ref 后跟与形参类型相同的变量引用（§5.3.3）组成。变量在作为引用参数传递之前必须明确赋值。

在方法内，引用参数始终被视为已明确赋值。

声明为迭代器（§10.14）的方法不能有引用参数。

示例

```csharp
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

产生以下输出：

i = 2, j = 1

对于 Main 中对 Swap 的调用，x 表示 i，y 表示 j。因此该调用具有交换 i 和 j 的值的效果。

在接受引用参数的方法中，多个名称可能表示同一存储位置。在示例

```csharp
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

G 中对 F 的调用为 a 和 b 都传递对 s 的引用。因此，对于该调用，名称 s、a 和 b 都引用同一存储位置，并且这三个赋值都修改实例字段 s。

### 10.6.1.3 输出参数

使用 out 修饰符声明的参数是输出参数。与引用参数类似，输出参数不会创建新的存储位置。相反，输出参数表示与方法调用中作为实参给出的变量相同的存储位置。

当形参是输出参数时，方法调用中的相应实参必须由关键字 out 后跟与形参类型相同的变量引用（§5.3.3）组成。变量在作为输出参数传递之前不必明确赋值，但在将变量作为输出参数传递的调用之后，该变量被视为已明确赋值。

在方法内，与局部变量一样，输出参数最初被视为未赋值，并且在其值被使用之前必须明确赋值。

方法的每个输出参数都必须在方法返回之前明确赋值。




声明为分部方法（§10.2.7）或迭代器（§10.14）的方法不能有输出参数。

输出参数通常用于产生多个返回值的方法。

> BILL WAGNER 当然，你可以创建一个结构或类来返回多个值，这样就不需要输出参数了。此外，新的 Tuple<> 泛型类可用于返回多个值。

> JON SKEET Bill 观点的一个例子可以是 .NET Framework 中的 int.TryParse。它实际上返回两个值：解析后的整数，以及一个指示操作是否成功的布尔标志。C# 中的可空值类型已经恰好提供了这种组合，因此当前的方法签名：
>
> bool TryParse(string s, out int result)
>
> 本可以改为：
>
> int? TryParse(string s)
>
> 对于类似的调用（例如 decimal.TryParse 等），情况也是如此。

例如：

```csharp
using System;
class Test { static void SplitPath(string path, out string dir, out string name) { int i = path.Length; while (i > 0) { char ch = path[i - 1]; if (ch == '/' || ch == ':') break; i--; } dir = path.Substring(0, i); name = path.Substring(i); } static void Main() { string dir, name; SplitPath("c:\\Windows\\System\\hello.txt", out dir, out name); Console.WriteLine(dir); Console.WriteLine(name); } }
```

该示例产生以下输出：

```
c:\Windows\System\
hello.txt
```

注意，`dir` 和 `name` 变量在传递给 `SplitPath` 之前可以未赋值，并且在调用之后它们被视为明确赋值。

### 10.6.1.4 参数数组

使用 `params` 修饰符声明的参数是参数数组。如果形参列表包含参数数组，则它必须是列表中的最后一个参数，并且必须是一维数组类型。例如，类型 `string[]` 和 `string[][]` 可以用作参数数组的类型，但类型 `string[,]` 不能。不能将 `params` 修饰符与 `ref` 和 `out` 修饰符组合使用。

参数数组允许在方法调用中以两种方式之一指定实参：

- 为参数数组提供的实参可以是单个表达式，该表达式可隐式转换（§6.1）为参数数组类型。在这种情况下，参数数组的行为完全类似于值参数。
- 或者，调用可以为参数数组指定零个或多个实参，其中每个实参都是可隐式转换（§6.1）为参数数组元素类型的表达式。在这种情况下，调用会创建一个长度与实参数量相对应的参数数组类型实例，使用给定的实参值初始化该数组实例的元素，并将新创建的数组实例用作实际实参。

除了允许调用中使用可变数量的实参外，参数数组完全等价于同一类型的值参数（§10.6.1.1）。

示例

```csharp
using System;

class Test
{
    static void F(params int[] args) {
        Console.Write("Array contains {0} elements:", args.Length);
        foreach (int i in args)
            Console.Write(" {0}", i);
        Console.WriteLine();
    }
}
```

```csharp
static void Main() {
    int[] arr = {1, 2, 3};
    F(arr);
    F(10, 20, 30, 40);
    F();
}
```

产生以下输出：

```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

对 F 的第一次调用只是将数组作为值参数传递。对 F 的第二次调用会自动创建一个包含给定元素值的四元素 int[]，并将该数组实例作为值参数传递。同样，对 F 的第三次调用会创建一个零元素 int[]，并将该实例作为值参数传递。第二次和第三次调用完全等价于编写

```
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

在执行重载决策时，带参数数组的方法可能以其正常形式或其展开形式（§7.5.3.1）适用。仅当方法的正常形式不适用，并且同一类型中尚未声明与展开形式具有相同签名的方法时，方法的展开形式才可用。

示例

```csharp
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

产生以下输出：

```
F();
F(object[]);
F(object,object);
F(object[]);
F(object[]);
```

> **BILL WAGNER** 你创建的可能是合适方法的方法越多，给用户带来的麻烦就越多。更多的编译器歧义也会给客户端开发人员带来更多歧义。

在示例中，带参数数组的方法的两种可能的展开形式已经作为常规方法包含在类中。因此，在执行重载决策时不考虑这些展开形式，第一次和第三次方法调用会选择常规方法。当类声明带参数数组的方法时，还包含一些展开形式作为常规方法并不罕见。这样做可以避免在调用带参数数组的方法的展开形式时发生的数组实例分配。

当参数数组的类型为 object[] 时，在方法的正常形式与单个 object 参数的展开形式之间会产生潜在歧义。产生歧义的原因是 object[] 本身可隐式转换为类型 object。然而，这种歧义不会造成问题，因为如果需要，可以通过插入强制转换来解决。

示例

```csharp
using System;
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
        object[] a = {1, "Hello", 123.456};
        object o = a;
        F(a);
        F((object)a);
        F(o);
        F((object[])o);
    }
}
```

产生以下输出：

```
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
```

在对 F 的第一次和最后一次调用中，F 的正常形式适用，因为存在从实参类型到参数类型的隐式转换（两者都是 object[] 类型）。因此，重载决策会选择 F 的正常形式，并且实参作为常规值参数传递。在第二次和第三次调用中，F 的正常形式不适用，因为不存在从实参类型到参数类型的隐式转换（类型 object 不能隐式转换为类型 object[]）。但是，F 的展开形式适用，因此它被重载决策选中。结果，调用会创建一个单元素 object[]，并且该数组的单个元素会用给定的实参值（该值本身是对 object[] 的引用）初始化。

## 10.6.2 静态方法和实例方法

当方法声明包含 static 修饰符时，该方法称为静态方法。当不存在 static 修饰符时，该方法称为实例方法。

静态方法不针对特定实例进行操作，在静态方法中引用 this 是编译时错误。

实例方法针对类的给定实例进行操作，并且该实例可作为 this（§7.6.7）访问。

当在形式为 *E.M* 的*成员访问*（§7.6.4）中引用方法时，如果 *M* 是静态方法，则 *E* 必须表示包含 *M* 的类型；如果 *M* 是实例方法，则 *E* 必须表示包含 *M* 的类型的实例。

静态成员和实例成员之间的差异将在 §10.3.7 中进一步讨论。





## 10.6.3 虚方法

当实例方法声明包含 `virtual` 修饰符时，该方法称为虚方法。当不存在 `virtual` 修饰符时，该方法称为非虚方法。

> **BILL WAGNER** 即使在非泛型类中，也可以创建泛型虚方法。这样做时，任何重写也必须是泛型的。不能重写某个特定的实例化版本。

> **JON SKEET** 私有方法不能是虚方法，尽管存在一种边界情况，在这种情况下允许私有方法为虚方法是有意义的：从其自身容器类派生的嵌套类可以重写它（使用另一个私有方法）。规范禁止这种可能性虽然略显不够优雅，但这意味着那些意外声明为私有且为虚方法的方法可以被视为错误——而这种情况要常见得多。

非虚方法的实现是不变的：无论该方法是在声明它的类的实例上调用，还是在派生类的实例上调用，其实现都相同。相比之下，虚方法的实现可以被派生类取代。取代继承的虚方法的实现的过程称为重写该方法（§10.6.4）。

在虚方法调用中，调用所针对的实例的运行时类型决定实际要调用的方法实现。在非虚方法调用中，实例的编译时类型起决定作用。更精确地说，当在编译时类型为 C、运行时类型为 R 的实例上使用参数列表 A 调用名为 N 的方法时（其中 R 要么是 C，要么是从 C 派生的类），该调用按以下方式处理：

- 首先，对 C、N 和 A 应用重载解析，从 C 声明或继承的方法集合中选择一个特定的方法 M。相关内容请参见 §7.6.5.1。
- 然后，如果 M 是非虚方法，则调用 M。
- 否则，M 是虚方法，并调用相对于 R 的 M 的最派生实现。

对于类声明或继承的每个虚方法，相对于该类都存在一个该方法的最派生实现。相对于类 R 的虚方法 M 的最派生实现按以下方式确定：

- 如果 R 包含 M 的引入虚声明，则该声明就是 M 的最派生实现。
- 否则，如果 R 包含 M 的重写，则该重写就是 M 的最派生实现。
- 否则，相对于 R 的 M 的最派生实现，与相对于 R 的直接基类的 M 的最派生实现相同。

以下示例说明了虚方法和非虚方法之间的差异：

```
using System;
class A
{
    public void F() { Console.WriteLine("A.F"); }
    public virtual void G() { Console.WriteLine("A.G"); }
}
class B : A
{
    new public void F() { Console.WriteLine("B.F"); }
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

在此示例中，A 引入了一个非虚方法 F 和一个虚方法 G。类 B 引入了一个新的非虚方法 F，从而隐藏继承的 F，同时还重写了继承的方法 G。该示例产生以下输出：

A.F
B.F
B.G
B.G

请注意，语句 `a.G()` 调用的是 B.G，而不是 A.G。出现这种结果是因为决定实际要调用的方法实现的是实例的运行时类型（即 B），而不是实例的编译时类型（即 A）。

由于允许方法隐藏继承的方法，因此一个类可能包含多个具有相同签名的虚方法。这不会造成歧义问题，因为除了最派生的方法之外，其他方法都会被隐藏。在以下示例中：

```
using System;
class A
{
    public virtual void F() { Console.WriteLine("A.F"); }
}
class B : A
{
    public override void F() { Console.WriteLine("B.F"); }
}
class C : B
{
    new public virtual void F() { Console.WriteLine("C.F"); }
}
class D : C
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

C 类和 D 类包含两个具有相同签名的虚方法：一个由 A 引入，另一个由 C 引入。C 引入的方法隐藏了从 A 继承的方法。因此，D 中的重写声明重写的是 C 引入的方法，而 D 不可能重写 A 引入的方法。该示例产生以下输出：

```
B.F
B.F
D.F
D.F
```

请注意，可以通过一个派生程度较低且该方法未被隐藏的类型来访问 D 的实例，从而调用被隐藏的虚方法。

## 10.6.4 重写方法

当实例方法声明包含 `override` 修饰符时，该方法称为重写方法。重写方法会重写具有相同签名的继承虚方法。虚方法声明会引入一个新方法，而重写方法声明则通过提供该方法的新实现，来专门化一个现有的继承虚方法。

被重写声明重写的方法称为被重写的基方法。对于类 C 中声明的重写方法 M，被重写的基方法通过检查 C 的每个基类类型来确定：从 C 的直接基类类型开始，依次检查后续的每个直接基类类型，直到在某个基类类型中找到至少一个可访问的方法，该方法在替换类型参数后与 M 具有相同的签名。为了定位被重写的基方法，如果方法是公共的、受保护的、受保护的内部方法，或者是内部方法且与 C 在同一程序中声明，则该方法被视为可访问。

除非重写声明满足以下所有条件，否则会发生编译时错误：

- 可以按照上述方式找到被重写的基方法。
- 恰好存在一个这样的被重写基方法。仅当基类类型是构造类型，并且类型参数的替换使两个方法具有相同签名时，此限制才会生效。
- 被重写的基方法是虚方法、抽象方法或重写方法。换句话说，被重写的基方法不能是静态方法或非虚方法。
- 被重写的基方法不是密封方法。
- 重写方法与被重写的基方法具有相同的返回类型。
- 重写声明与被重写的基方法具有相同的声明可访问性。换句话说，重写声明不能更改虚方法的可访问性。但是，如果被重写的基方法是受保护的内部方法，并且它声明在不同于包含重写方法的程序集的另一个程序集中，则重写方法的声明可访问性必须是受保护的。
- 重写声明不指定类型参数约束子句。相反，约束从被重写的基方法继承。请注意，被重写方法中的类型参数约束可能会在继承的约束中被类型实参替换。这可能导致一些在显式指定时不合法的约束，例如值类型或密封类型。

以下示例演示了泛型类中重写规则的工作方式：

```
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}
class D: C<string>
{
    public override string F() {...}        // Okay
    public override C<string> G() {...}    // Okay
    public override void H(C<T> x) {...}   // Error: should be C<string>
}
class E<T,U>: C<U>
{
    public override U F() {...}            // Okay
    public override C<U> G() {...}         // Okay
    public override void H(C<T> x) {...}   // Error: should be C<U>
}
```

重写声明可以使用 *基访问*（§7.6.8）访问被重写的基方法。在以下示例中：

```
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
    public override void PrintFields() {
        base.PrintFields();
        Console.WriteLine("y = {0}", y);
    }
}
```

B 中的 `base.PrintFields()` 调用调用的是 A 中声明的 `PrintFields` 方法。*基访问*会禁用虚调用机制，并将基方法简单地视为非虚方法。如果 B 中的调用写成 `((A)this).PrintFields()`，它


会递归调用 B 中声明的 PrintFields 方法，而不是 A 中声明的那个，因为 PrintFields 是虚方法，且 ((A)this) 的运行时类型是 B。

只有包含 override 修饰符，一个方法才能重写另一个方法。在所有其他情况下，与继承方法具有相同签名的方法只是隐藏该继承方法。在下面的示例中

```csharp
class A
{
    public virtual void F() { }
}

class B: A
{
    public virtual void F() { }        // Warning: hiding inherited F()
}
```

B 中的 F 方法不包含 override 修饰符，因此不会重写 A 中的 F 方法。相反，B 中的 F 方法隐藏了 A 中的方法，并且由于该声明不包含 new 修饰符，因此会报告警告。

在下面的示例中

```csharp
class A
{
    public virtual void F() { }
}

class B: A
{
    new private void F() { }        // Hides A.F within body of B
}

class C: B
{
    public override void F() { }    // Okay: overrides A.F
}
```

B 中的 F 方法隐藏了从 A 继承的虚 F 方法。由于 B 中新的 F 具有 private 访问权限，其作用域仅包括 B 的类体，而不扩展到 C。因此，允许 C 中 F 的声明重写从 A 继承的 F。

### 10.6.5 密封方法

当实例方法声明包含 sealed 修饰符时，该方法称为*密封方法*。如果实例方法声明包含 sealed 修饰符，则它还必须包含 override 修饰符。使用 sealed 修饰符可以阻止派生类进一步重写该方法。

在下面的示例中

```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }

    public virtual void G() {
        Console.WriteLine("A.G");
    }
}

class B: A
{
    sealed override public void F() {
        Console.WriteLine("B.F");
    }

    override public void G() {
        Console.WriteLine("B.G");
    }
}

class C: B
{
    override public void G() {
        Console.WriteLine("C.G");
    }
}
```

类 B 提供了两个重写方法：一个带有 sealed 修饰符的 F 方法，以及一个不带 sealed 修饰符的 G 方法。类 B 对 sealed 修饰符的使用阻止了类 C 进一步重写 F。

> **克里斯·塞尔斯**   当我想要从某个类派生时，如果该类是密封的，或者某个方法是密封的，这会让我发疯，因为这些限制限定了我使用该类的方式。
>
> 当我想要构建一个基类时，我希望它尽可能受到限制，以便我可以测试我想要支持的可能的派生场景。我不想被困在支持某些客户做过的、而我从未打算支持的疯狂事情中。
>
> 与软件设计中的所有事情一样，使用 sealed 修饰符涉及一种平衡。除非必须使用，否则我倾向于避免使用 sealed 关键字。如果客户变得疯狂，好吧，这正是让事情保持有趣的原因。

### 10.6.6 抽象方法

当实例方法声明包含 abstract 修饰符时，该方法称为*抽象方法*。虽然抽象方法隐式地也是虚方法，但它不能带有 virtual 修饰符。

抽象方法声明引入一个新的虚方法，但不提供该方法的实现。相反，非抽象派生类必须通过重写该方法来提供自己的实现。由于抽象方法不提供实际实现，抽象方法的*方法体*仅由一个分号组成。

抽象方法声明只允许在抽象类中（§10.1.1.1）。

在下面的示例中

```csharp
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

Shape 类定义了可自行绘制的几何形状对象的抽象概念。Paint 方法是抽象的，因为没有有意义的默认实现。Ellipse 和 Box 类是具体的 Shape 实现。由于这些类是非抽象的，因此它们必须重写 Paint 方法并提供实际实现。

*基类访问*（§7.6.8）引用抽象方法会造成编译时错误。在下面的示例中

```csharp
abstract class A
{
    public abstract void F();
}

class B: A
{
    public override void F() {
        base.F();               // Error: base.F is abstract
    }
}
```

对 base.F() 的调用会报告编译时错误，因为它引用了抽象方法。

允许抽象方法声明重写虚方法。这允许抽象类强制在派生类中重新实现该方法，并使该方法的原始实现不可用。在下面的示例中

```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }
}

abstract class B: A
{
    public abstract override void F();
}

class C: B
{
    public override void F() {
        Console.WriteLine("C.F");
    }
}
```

类 A 声明一个虚方法，类 B 用抽象方法重写此方法，类 C 重写该抽象方法以提供自己的实现。

> **马雷克·萨法尔** 抽象方法没有可见性限制，只是它们不能是 private。当有人意外地在公共抽象类中声明 internal 抽象方法时，这种访问选择可能会引起麻烦；这样的类即使声明为 public，也不能在类所在程序集之外使用。

### 10.6.7 外部方法

当方法声明包含 extern 修饰符时，该方法称为*外部方法*。外部方法在外部实现，通常使用 C# 以外的语言。由于外部方法声明不提供实际实现，外部方法的方法体仅由一个分号组成。外部方法不能是泛型的。

extern 修饰符通常与 DllImport 特性（§17.5.1）一起使用，从而允许外部方法由动态链接库（DLL）实现。执行环境可能支持其他机制来提供外部方法的实现。

当外部方法包含 DllImport 特性时，方法声明还必须包含 static 修饰符。下面的示例演示了 extern 修饰符和 DllImport 特性的使用：

```csharp
using System.Text;
using System.Security.Permissions;
using System.Runtime.InteropServices;

class Path
{
    [DllImport("kernel32", SetLastError=true)]
    static extern bool CreateDirectory(string name, SecurityAttribute sa);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool RemoveDirectory(string name);

    [DllImport("kernel32", SetLastError=true)]
    static extern int GetCurrentDirectory(int bufSize, StringBuilder buf);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool SetCurrentDirectory(string name);
}
```

### 10.6.8 分部方法

当方法声明包含 partial 修饰符时，该方法称为分部方法。分部方法只能声明为分部类型（§10.2）的成员，并受到许多限制。分部方法在 §10.2.7 中进一步描述。

### 10.6.9 扩展方法

当方法的第一个参数包含 this 修饰符时，该方法称为扩展方法。扩展方法只能在非泛型、非嵌套的静态类中声明。扩展方法的第一个参数除 this 外不能有任何其他修饰符，并且参数类型不能是指针类型。

> **彼得·塞斯托夫特**  参数类型也不能是 dynamic（尽管那实际上只意味着 object）。但它可以是 T，其中 T 是扩展方法的类型参数，如下所示：
>
> ```csharp
> public static void Foo<T>(this T x) { ... }
> ```
>
> 这可能很有用，特别是当 T 具有类型约束，并且还有更多参数的类型涉及 T 时。

下面的示例是一个声明了两个扩展方法的静态类：

```csharp
using System;
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

扩展方法是一种常规静态方法。此外，当其所在的静态类在作用域内时，可以使用实例方法调用语法（§7.6.5.2）调用扩展方法，并将接收者表达式作为第一个参数。

下面的程序使用上面声明的扩展方法：

```csharp
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

Slice 方法可在 string[] 上使用，ToInt32 方法可在 string 上使用，因为它们已声明为扩展方法。该程序的含义与下面使用普通静态方法调用的程序相同：

```csharp
static class Program
{
    static void Main() {
```




```csharp
string[] strings = { "1", "22", "333", "4444" };
foreach (string s in Extensions.Slice(strings, 1, 2)) {
    Console.WriteLine(Extensions.ToInt32(s));
}
}
}
```

> > **PETER SESTOFT** Slice 扩展方法 是泛型的：它适用于 T 的任意数组，无论类型参数 T 为何。你还可以定义涉及类型约束的泛型扩展方法（下面方法 IsSorted）以及在泛型类型的特定类型实例上工作的扩展方法（方法 ConcatWith）。后者也表明，扩展方法当然可以有默认参数（§10.1.6）：
> >
> > ```csharp
> > public static bool IsSorted<T>(this IEnumerable<T> xs)
> >     where T : IComparable<T>
> > { ... }
> >
> > public static string ConcatWith(this IEnumerable<string> xs, string glue = ", ")
> > { ... }
> > ```

> > **CHRIS SELLS** 一方面，扩展方法是一种在保持语法仿佛设计者已考虑到你每一个心愿的同时，添加类型设计者遗漏的方法的好方法。另一方面，这些方法很容易被滥用。我曾在某个实验系统中看到过针对 object 的扩展方法，这在我们小组中变成了一个持续的笑话，看我们是否能以更令人困惑的设计超越它。

> > **PETER SESTOFT** 这里有一个最广泛适用的扩展方法的例子。任何尝试对任意对象调用非静态方法 toString，小写 t，并传入任意数量的任意类型参数，都将调用此方法代替：
> >
> > ```csharp
> > public static string toString(this object x, params object[] args) {
> >     return "Make that ToString(), mate!";
> > }
> > ```
> >
> > 扩展方法是非虚的并且不重写任何内容；因此，不能通过声明扩展方法来替换现有类型 YourType 的 ToString 方法，大写 T。下面的声明是合法的但没有任何效果。对 o.ToString() 的调用将选取 Object.ToString() 或某个重写或隐藏它的 方法，而不是这个方法：
> >
> > ```csharp
> > public static string ToString(this YourType x) { ... }
> > ```

## 10. 类

### 10.6.10 方法体

方法声明的 *方法体* 由 *块* 或分号组成。

抽象方法和外部方法声明不提供方法实现，因此它们的方法体仅由分号组成。对于任何其他方法，方法体是一个块（§8.2），其中包含调用该方法时要执行的语句。

当方法的返回类型为 void 时，该方法体中的 return 语句（§8.9.4）不允许指定表达式。如果 void 方法的方法体正常完成执行，即控制流离开方法体末尾，该方法 simply 返回给其调用方。

当方法的返回类型不是 void 时，该方法体中的每个 return 语句必须指定一个可隐式转换为返回类型的表达式。值返回方法的方法体终点必须是不可达的。换句话说，在值返回方法中，不允许控制流离开方法体末尾。

在示例中

```
    class A
    {
        public int F() { }        // Error: return value required

        public int G() {
            return 1;
        }

        public int H(bool b) {
            if (b) {
                return 1;
            }
            else {
                return 0;
            }
        }
    }
```

值返回的 F 方法会导致编译时错误，因为控制流可以离开方法体末尾。G 和 H 方法是正确的，因为所有可能的执行路径都以指定返回值的 return 语句结束。

### 10.6.11 方法重载

方法重载解析规则在 §7.5.2 中描述。

## 10.7 属性

属性是提供对对象或类的特征访问的成员。属性的示例包括字符串的长度、字体的大小、窗口的标题、客户的名称等等。属性是字段的自然扩展——两者都是具有关联类型的命名成员，并且访问字段和属性的语法相同。然而，与字段不同，属性不表示存储位置。相反，属性具有访问器，指定在读取或写入其值时要执行的语句。因此，属性提供了一种将操作与对象属性的读取和写入关联起来的机制；此外，它们允许此类属性被计算得出。

属性使用 property-declarations 声明：

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

member-name:
    identifier
    interface-type . identifier
```

property-declaration 可以包含一组属性（§17）、四个访问修饰符（§10.3.5）的有效组合，以及 new（§10.3.4）、static（§10.6.2）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符。

属性声明受与方法声明（§10.6）相同的规则约束，关于修饰符的有效组合。

属性声明的 *类型* 指定声明引入的属性的类型，而 *成员名* 指定属性的名称。除非属性是显式接口成员实现，否则 *成员名* 只是 *标识符*。对于显式接口成员实现（§13.4.1），*成员名* 由 *接口类型* 后跟 “.” 和 *标识符* 组成。

属性的 *类型* 必须至少与属性本身一样可访问（§3.5.4）。

*访问器声明* 必须用 “{” 和 “}” 标记括起来，声明属性的访问器（§10.7.2）。访问器指定与读取和写入属性相关联的可执行语句。

尽管访问属性的语法与访问字段相同，但属性不被归类为变量。因此，不可能将属性作为 `ref` 或 `out` 参数传递。

当属性声明包含 extern 修饰符时，该属性被称为 *外部属性*。因为外部属性声明不提供实际实现，所以其每个 *访问器声明* 都由分号组成。

### 10.7.1 静态和实例属性

当属性声明包含 static 修饰符时，该属性被称为 *静态属性*。当没有 static 修饰符时，该属性被称为 *实例属性*。

静态属性不与特定实例关联，并且在静态属性的访问器中引用 `this` 是编译时错误。

实例属性与类的给定实例关联，并且该实例可以在该属性的访问器中作为 `this`（§7.6.7）访问。

当属性在形式为 *E.M* 的 *成员访问*（§7.6.4）中被引用时，如果 *M* 是静态属性，则 *E* 必须表示包含 *M* 的类型；如果 *M* 是实例属性，则 *E* 必须表示包含 *M* 的类型的实例。

静态成员和实例成员之间的差异在 §10.3.7 中进一步讨论。

### 10.7.2 访问器

属性的访问器声明指定与读取和写入该属性相关联的可执行语句。

```
accessor-declarations:
  get-accessor-declaration  set-accessor-declaration_opt
  set-accessor-declaration  get-accessor-declaration_opt
```

```
get-accessor-declaration:
    attributes_opt  accessor-modifier_opt  get  accessor-body
```

```
set-accessor-declaration:
    attributes_opt  accessor-modifier_opt  set  accessor-body
```

```
accessor-modifier:
  protected
  internal
  private
  protected  internal
  internal  protected
```

```
accessor-body:
  block
  ;
```

访问器声明由 get-accessor-declaration、set-accessor-declaration 或两者组成。每个访问器声明由标记 get 或 set 后跟可选的访问器修饰符和访问器体组成。

访问器修饰符的使用受以下限制约束：

- 访问器修饰符不得在接口或显式接口成员实现中使用。
- 对于没有 override 修饰符的属性或索引器，只有当属性或索引器同时具有 get 和 set 访问器时，才允许使用访问器修饰符，并且仅允许在其中一个访问器上使用。
- 对于包含 override 修饰符的属性或索引器，访问器必须与被重写的访问器的访问器修饰符，如果有，匹配。



## 10. 类

- *访问器修饰符*必须声明一种可访问性，该可访问性严格比属性或索引器本身声明的可访问性更受限制。具体而言：
  - 如果属性或索引器声明的可访问性为 `public`，则*访问器修饰符*可以是 `protected internal`、`internal`、`protected` 或 `private`。
  - 如果属性或索引器声明的可访问性为 `protected internal`，则*访问器修饰符*可以是 `internal`、`protected` 或 `private`。
  - 如果属性或索引器声明的可访问性为 `internal` 或 `protected`，则*访问器修饰符*必须是 `private`。
  - 如果属性或索引器声明的可访问性为 `private`，则不能使用任何*访问器修饰符*。

对于抽象属性和 extern 属性，所指定的每个访问器的*访问器体*只是一个分号。非抽象、非 extern 属性可以是**_自动实现的属性_**，在这种情况下，必须同时提供 get 和 set 访问器，二者都以分号作为主体（§10.7.3）。对于任何其他非抽象、非 extern 属性的访问器，*访问器体*是一个块，其中指定调用相应访问器时要执行的语句。

get 访问器对应于一个无参数方法，其返回值为属性类型。除非作为赋值目标，否则在表达式中引用属性时，会调用该属性的 get 访问器来计算属性的值（§7.1.1）。get 访问器的主体必须符合 §10.6.10 中描述的返回值方法规则。特别是，get 访问器主体中的所有 return 语句都必须指定一个可隐式转换为属性类型的表达式。此外，get 访问器的终点必须不可到达。

set 访问器对应于一个方法，该方法具有一个属性类型的值参数和 `void` 返回类型。set 访问器的隐式参数始终命名为 `value`。当属性作为赋值目标（§7.17）或作为 `++` 或 `--` 的操作数（§7.6.9、§7.7.5）被引用时，会调用 set 访问器，并传入一个参数（其值为赋值右侧的值或 `++` 或 `--` 运算符的操作数），该参数提供新值（§7.17.1）。set 访问器的主体必须符合 §10.6.10 中描述的 void 方法规则。特别是，不允许 set 访问器主体中的 return 语句指定表达式。由于 set 访问器隐式具有名为 `value` 的参数，因此 set 访问器中的局部变量或常量声明使用该名称属于编译时错误。

根据 get 和 set 访问器的存在与否，属性分类如下：

- 同时包含 get 访问器和 set 访问器的属性称为*读写*属性。
- 只有 get 访问器的属性称为*只读*属性。只读属性作为赋值目标属于编译时错误。
- 只有 set 访问器的属性称为*只写*属性。除非作为赋值目标，否则在表达式中引用只写属性属于编译时错误。

在以下示例中

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
        // Painting code goes here
    }
}
```

Button 控件声明了一个公共的 Caption 属性。Caption 属性的 get 访问器返回存储在私有 caption 字段中的字符串。set 访问器检查新值是否与当前值不同，如果不同，则存储新值并重新绘制控件。属性通常遵循上面所示的模式：get 访问器只返回存储在私有字段中的值，而 set 访问器修改该私有字段，然后执行完全更新对象状态所需的任何附加操作。

鉴于上面的 Button 类，以下是使用 Caption 属性的示例：

```
Button okButton = new Button();
okButton.Caption = "OK";    // Invokes set accessor
string s = okButton.Caption;    // Invokes get accessor
```

这里，通过向属性赋值来调用 set 访问器，并通过在表达式中引用属性来调用 get 访问器。

## 10. 类

属性的 get 和 set 访问器不是不同的成员，并且不可能分别声明属性的访问器。因此，读写属性的两个访问器不可能具有不同的可访问性。示例

```csharp
class A
{
    private string name;

    public string Name {        // Error: duplicate member name
        get { return name; }
    }

    public string Name {        // Error: duplicate member name
        set { name = value; }
    }
}
```

并不声明单个读写属性。相反，它声明了两个同名属性，一个只读，一个只写。由于同一个类中声明的两个成员不能具有相同名称，因此该示例会导致编译时错误。

当派生类声明与继承属性同名的属性时，派生属性在读取和写入两方面都会隐藏继承属性。在示例

```csharp
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

中，B 中的 P 属性在读取和写入两方面都隐藏了 A 中的 P 属性。因此，在以下语句中

```csharp
B b = new B();
b.P = 1;             // Error: B.P is read-only
((A)b).P = 1;        // Okay: reference to A.P
```

对 b.P 的赋值会导致报告编译时错误，因为 B 中的只读 P 属性隐藏了 A 中的只写 P 属性。但是请注意，可以使用强制转换来访问被隐藏的 P 属性。

与公共字段不同，属性在对象的内部状态与其公共接口之间提供了分离。考虑以下示例：

```csharp
class Label
{
    private int x, y;
    private string caption;
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

这里，Label 类使用两个 int 字段 x 和 y 来存储其位置。该位置通过 X 和 Y 属性以及 Point 类型的 Location 属性公开。如果在 Label 的未来版本中，将位置内部存储为 Point 变得更方便，则可以在不影响类公共接口的情况下进行更改：

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

如果 x 和 y 改为公共只读字段，则不可能对 Label 类进行这样的更改。

通过属性公开状态不一定比直接公开字段效率更低。特别是，当属性是非虚拟的并且仅包含少量代码时，执行环境可以用访问器的实际代码替换对访问器的调用。此过程称为内联，它使属性访问与字段访问一样高效，同时保留了属性更高的灵活性。

由于调用 get 访问器在概念上等同于读取字段的值，因此 get 访问器具有可观察的副作用被认为是不良编程风格。在示例

```csharp
class Counter
{
    private int next;
    public int Next {
        get { return next++; }
    }
}
```

中，Next 属性的值取决于此前访问该属性的次数。因此，访问该属性会产生可观察的副作用，该属性应改为实现为方法。

get 访问器的“无副作用”约定并不意味着 get 访问器应始终编写为仅返回存储在字段中的值。实际上，get 访问器通常通过访问多个字段或调用方法来计算属性的值。但是，设计良好的 get 访问器不会执行任何导致对象状态发生可观察更改的操作。

属性可用于将资源的初始化延迟到首次引用该资源时。例如：

```csharp
using System.IO;

public class Console
{
    private static TextReader reader;
    private static TextWriter writer;
    private static TextWriter error;
```



```csharp
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
```

Console 类包含三个属性——In、Out 和 Error，分别表示标准输入、输出和错误设备。通过将这些成员公开为属性，Console 类可以延迟它们的初始化，直到实际使用时为止。例如，在首次引用 Out 属性时，如

`Console.Out.WriteLine("hello, world");`

底层用于输出设备的 TextWriter 将被创建。但如果应用程序未引用 In 和 Error 属性，则不会为这些设备创建对象。

## 10.7.3 自动实现的属性

> **JON SKEET**  C# 3.0 规范的早期草案将这些属性称为“automatic properties”。这个名称存在的时间刚好足够让人记住，现在在社区中的使用频率远高于完整名称。

当属性被指定为自动实现属性时，会自动为该属性提供一个隐藏的备份字段，并且访问器被实现为从该备份字段读取和写入。

示例

```csharp
public class Point {
    public int X { get; set; } // Automatically implemented
    public int Y { get; set; } // Automatically implemented
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

由于备份字段无法访问，即使在包含的类型内部，也只能通过属性访问器读取和写入它。

这意味着自动实现的只读或只写属性没有意义，因此不允许使用。可以为每个访问器设置不同的访问级别。因此，可以通过以下方式模拟具有私有备份字段的只读属性的效果：

```csharp
public class ReadOnlyPoint {
    public int X { get; private set; }
    public int Y { get; private set; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```

> **BILL WAGNER** 虽然属性是只读的，但其底层的备份存储不是。ReadOnlyPoint 内部的代码不必遵守不可变性的规则。

> **JON SKEET** 虽然这种行为对其他类型模拟了只读属性的效果，但它与属性（或确实是备份字段）真正只读并不相同。我希望能够指定只读属性，也许采用以下形式：

```csharp
public int X { get; readonly set; }
```

这段代码将产生一个只读字段；setter 的使用仅在构造函数内允许，在那里它将被编译为对备份字段的直接写入。

不幸的是，目前创建真正不可变类型的代码比创建可变类型更冗长。

> **PETER SESTOFT**  自动实现的属性非常好，因为属性可以在对象初始值设定项（§7.6.10.2）中使用。对象初始值设定项对于坐标对和三元组、复数以及类似的项目——即结构体值——特别有用。然而，通常我们更希望结构体具有不可变字段，因为它们在赋值和参数传递期间会被复制。出于这个原因，我完全支持 Jon 对具有自动实现访问器的只读字段的简洁表示法的愿望，前提是 set 访问器可以在构造函数中以及*在对象初始值设定项*中使用。

此限制还意味着，具有自动实现属性的结构体类型的确定性赋值只能使用结构体的标准构造函数来实现，因为对属性本身的赋值要求结构体已被确定性赋值。这意味着用户定义的构造函数必须调用默认构造函数。

## 10.7.4 可访问性

如果访问器具有*访问器修饰符*，则访问器的可访问性域（§3.5.2）使用*访问器修饰符*声明的可访问性确定。如果访问器没有*访问器修饰符*，则访问器的可访问性域从属性或索引器的声明可访问性确定。

*访问器修饰符*的存在永远不会影响成员查找（§7.3）或重载解析（§7.5.3）。属性或索引器上的修饰符始终决定绑定到哪个属性或索引器，而与访问的上下文无关。

一旦选择了特定的属性或索引器，就会使用特定访问器的可访问性域来确定该使用是否有效：

- 如果使用的是值（§7.1.1），则 get 访问器必须存在并且可访问。
- 如果使用的是简单赋值的目标（§7.17.1），则 set 访问器必须存在并且可访问。
- 如果使用的是复合赋值的目标（§7.17.2）或 ++ 或 -- 运算符的目标（§7.5.9、§7.6.5），则 get 访问器和 set 访问器都必须存在并且可访问。

在下面的示例中，即使在仅调用 set 访问器的上下文中，属性 B.Text 也会隐藏属性 A.Text。相比之下，属性 B.Count 对类 M 不可访问，因此改用可访问的属性 A.Count。

```csharp
class A
{
    public string Text {
        get { return "hello"; }
        set { }
    }

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
        b.Count = 12;        // Calls A.Count set accessor
        int i = b.Count;     // Calls A.Count get accessor
        b.Text = "howdy";    // Error: B.Text set accessor is not accessible
        string s = b.Text;   // Calls B.Text get accessor
    }
}
```

用于实现接口的访问器可能没有*访问器修饰符*。如果仅使用一个访问器来实现接口，则另一个访问器可以用*访问器修饰符*声明：

```csharp
public interface I
{
    string Prop { get; }
}

public class C: I
{
    public string Prop {
        get { return "April"; } // Must not have a modifier here
        internal set {...}      // Okay, because I.Prop has no set accessor
    }
}
```

## 10.7.5 虚拟、密封、重写和抽象访问器

虚拟属性声明指定该属性的访问器是虚拟的。virtual 修饰符适用于读写属性的两个访问器——不可能只让读写属性的一个访问器为虚拟。

抽象属性声明指定该属性的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写属性为访问器提供自己的实现。由于抽象属性声明的访问器不提供实际实现，其访问器体仅由一个分号组成。

包含 abstract 和 override 修饰符的属性声明指定该属性是抽象的并且重写了基属性。此类属性的访问器也是抽象的。

抽象属性声明仅允许在抽象类（§10.1.1.1）中使用。继承的虚拟属性的访问器可以通过包含指定 override 指令的属性声明在派生类中被重写。这称为重写属性声明。相反，它只是专门化现有虚拟属性的访问器实现。

重写属性声明必须指定与继承属性完全相同的可访问性修饰符、类型和名称。如果继承的属性只有一个访问器（即继承的属性是只读或只写），则重写属性必须仅包含该访问器。如果继承的属性包含两个访问器（即继承的属性是读写），则重写属性可以包含单个访问器或两个访问器。

重写属性声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该属性。密封属性的访问器也是密封的。

除了声明和调用语法上的差异外，虚拟、密封、重写和抽象访问器的行为与虚拟、密封、重写和抽象方法完全相同。具体来说，§10.6.3、§10.6.4、§10.6.5 和 §10.6.6 中描述的规则就好像访问器是相应形式的方法一样适用：

- get 访问器对应于一个无参数的方法，其返回值为属性类型，并且与包含属性具有相同的修饰符。
- set 访问器对应于一个具有单个属性类型的值参数、void 返回类型，并且与包含属性具有相同修饰符的方法。



在下面的示例中

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

X 是虚拟只读属性，Y 是虚拟读写属性，Z 是抽象读写属性。由于 Z 是抽象的，包含它的类 A 也必须声明为抽象类。

下面展示了一个从 A 派生的类：

```
class B: A
{
    int z;

    public override int X {
        get { return base.X + 1; }
    }

    public override int Y {
        set { base.Y = value < 0 ? 0: value; }
    }

    public override int Z {
        get { return z; }
        set { z = value; }
    }
}
```

此处，X、Y 和 Z 的声明是重写属性声明。每个属性声明都与其对应继承属性的可访问性修饰符、类型和名称完全匹配。X 的 get 访问器和 Y 的 set 访问器使用 base 关键字访问继承的访问器。Z 的声明重写了两个抽象访问器——因此 B 中不存在未实现的抽象函数成员，B 可以是非抽象类。

当属性声明为重写时，任何被重写的访问器都必须可由重写代码访问。此外，属性或索引器本身以及访问器的声明可访问性，必须与被重写成员和访问器的可访问性匹配。例如：

```csharp
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
        protected set {...}        // Must specify protected here
        get {...}                  // Must not have a modifier here
    }
}
```

## 10.8 事件

*事件*是一种成员，它使对象或类能够提供通知。客户端可以通过提供*事件处理程序*来为事件附加可执行代码。

事件使用*事件声明*来声明：

```text
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
```

```
event-accessor-declarations:
    add-accessor-declaration  remove-accessor-declaration
    remove-accessor-declaration  add-accessor-declaration

add-accessor-declaration:
    attributes_opt  add  block

remove-accessor-declaration:
    attributes_opt  remove  block
```

事件声明可以包含一组特性（§17）、四个访问修饰符（§10.3.5）的有效组合，以及 new（§10.3.4）、static（§10.6.2）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符。

就修饰符的有效组合而言，事件声明遵循与方法声明（§10.6）相同的规则。

事件声明的类型必须是委托类型（§4.2），并且该委托类型的可访问性必须至少不低于事件本身（§3.5.4）。

事件声明可以包含事件访问器声明。但是，如果未包含，则对于非 extern、非 abstract 事件，编译器会自动提供这些访问器声明（§10.8.1）；对于 extern 事件，访问器由外部提供。

省略事件访问器声明的事件声明会定义一个或多个事件——每个变量声明符对应一个事件。特性和修饰符应用于此类事件声明所声明的所有成员。

事件声明同时包含 abstract 修饰符和用大括号分隔的事件访问器声明，会导致编译时错误。

当事件声明包含 extern 修饰符时，该事件称为外部事件。由于外部事件声明不提供实际实现，因此它同时包含 extern 修饰符和事件访问器声明是错误的。

事件可以用作 += 和 -= 运算符（§7.17.3）的左操作数。这两个运算符分别用于将事件处理程序附加到事件或从事件中移除事件处理程序，而事件的访问修饰符控制允许此类操作的上下文。

由于 += 和 -= 是声明事件的类型之外允许对事件执行的唯一操作，因此外部代码可以为事件添加和移除处理程序，但不能以任何其他方式获取或修改底层的事件处理程序列表。

在 x += y 或 x -= y 形式的运算中，当 x 是事件且引用发生在包含 x 声明的类型之外时，该运算的结果类型为 void（而不是具有 x 的类型以及赋值后的 x 值）。此规则禁止外部代码间接检查事件的底层委托。

下面的示例展示如何将事件处理程序附加到 Button 类的实例：

```
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
}
public class LoginDialog: Form
{
    Button OkButton;
    Button CancelButton;
    public LoginDialog() {
        OkButton = new Button(...);
        OkButton.Click += new EventHandler(OkButtonClick);
        CancelButton = new Button(...);
        CancelButton.Click += new EventHandler(CancelButtonClick);
    }
    void OkButtonClick(object sender, EventArgs e) {
        // Handle OkButton.Click event
    }
    void CancelButtonClick(object sender, EventArgs e) {
        // Handle CancelButton.Click event
    }
}
```

此处，LoginDialog 实例构造函数创建两个 Button 实例，并将事件处理程序附加到 Click 事件。

> **CHRISTIAN NAGEL** 内存泄漏常常源于事件使用不当。如果客户端对象附加到事件但未从中分离，并且对客户端对象的引用不再使用，那么由于发布者仍持有引用，客户端对象仍无法被垃圾回收器回收。可以通过以下方式避免：(1) 当不再使用客户端对象时分离事件；(2) 使用持有委托的 WeakReference 类自定义实现 add 和 remove 访问器；或 (3) 使用 WPF 结合 IWeakEventListener 接口所采用的弱事件模式。

> **JON SKEET** 我倾向于将（并解释）事件视为类似于属性：它们是一对方法（add 和 remove），编译器知道如何使用简写形式（+= 和 -=）来调用它们。事件比属性限制更多，因为其类型必须是委托类型，并且必须始终同时存在 add 和 remove 方法；不存在像只读属性那样的“仅 add”事件。除了这些点之外，相似性很强——然而属性通常被很好地理解，而事件却造成大量混淆。我推测，类似字段的事件是这一问题的根源。

### 10.8.1 类似字段的事件

在包含事件声明的类或结构的程序文本中，某些事件可以像字段一样使用。要以这种方式使用，事件不能是 abstract 或 extern，并且不能显式包含事件访问器声明。此类事件可以在任何允许字段的上下文中使用。该字段包含一个委托（§15），该委托引用已添加到事件的事件处理程序列表。如果尚未添加任何事件处理程序，则该字段包含 null。

> **JON SKEET** 如果自动实现属性从一开始就存在于 C# 中，我认为将类似字段的事件称为“自动实现事件”会更合理，语法如下：
> 
> public event EventHandler Click { add; remove; }
> 
> 这可能会减少人们对事件究竟是什么的困惑。

在下面的示例中

```
public delegate void EventHandler(object sender, EventArgs e);
public class Button: Control
{
    public event EventHandler Click;
    protected void OnClick(EventArgs e) {
        if (Click != null) Click(this, e);
    }
    public void Reset() {
        Click = null;
    }
}
```




Click 在 Button 类中用作一个字段。如示例所示，该字段可以被检查、修改，并在委托调用表达式中使用。Button 类中的 OnClick 方法“引发” Click 事件。引发事件的概念与调用事件所表示的委托完全等价——因此没有用于引发事件的特殊语言构造。请注意，委托调用之前会进行检查以确保委托不为空。

在 Button 类的声明之外，Click 成员只能在 += 和 -= 运算符的左侧使用，如

```
    b.Click += new EventHandler(...);
```

它将委托附加到 Click 事件的调用列表中，并且

```
    b.Click -= new EventHandler(...);
```

它将委托从 Click 事件的调用列表中移除。

编译类字段的事件时，编译器会自动创建存储以保存委托，并为事件创建访问器以向委托字段添加或移除事件处理程序。添加和移除操作是线程安全的，并且可以在持有包含对象的锁（§8.12）——对于实例事件，或类型对象（§7.6.10.6）——对于静态事件的情况下执行（但不是必须的）。

因此，形式为

```
    class X
    {
        public event D Ev;
    }
```

的实例事件声明

将被编译为等效于

```
    class X
    {
        private D __Ev;  // Field to hold the delegate
        public event D Ev {
            add {
                /* Add the delegate in a thread-safe way */
            }
            remove {
                /* Remove the delegate in a thread-safe way */
            }
        }
    }
```

在类 X 内部，对 Ev 在 += 和 -= 运算符左侧的引用会导致 add 和 remove 访问器被调用。Ev 的所有其他引用都被编译为引用隐藏字段 __Ev。名称 "__Ev" 是任意的；隐藏字段可以有任何名称或根本没有名称。

## 10.8.2 事件访问器

事件声明通常省略事件访问器声明，如上面的 Button 示例所示。省略这样做的一种情况涉及每个事件一个字段的存储成本不可接受的情况。在这种情况下，类可以包含事件访问器声明并使用私有机制来存储事件处理程序列表。

事件的事件访问器声明指定与添加和移除事件处理程序相关联的可执行语句。

访问器声明由一个 add 访问器声明和一个 remove 访问器声明组成。每个访问器声明由标记 add 或 remove 后跟一个块组成。与 add 访问器声明关联的块指定在添加事件处理程序时要执行的语句，而与 remove 访问器声明关联的块指定在移除事件处理程序时要执行的语句。

每个 add 访问器声明和 remove 访问器声明对应于一个具有事件类型单个 value 参数和 void 返回类型的方法。事件访问器的隐式参数名为 value。当事件在事件赋值中使用时，会使用适当的事件访问器。具体来说，如果赋值运算符是 +=，则使用 add 访问器；如果赋值运算符是 -=，则使用 remove 访问器。在任何情况下，赋值运算符的右操作数都用作事件访问器的参数。add 访问器声明或 remove 访问器声明的块必须符合 §10.6.10 中描述的 void 方法规则。特别是，此类块中的 return 语句不允许指定表达式。

由于事件访问器隐式具有名为 value 的参数，因此在事件访问器中声明的局部变量或常量具有该名称是编译时错误。

在示例

```
class Control : Component
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

中，Control 类实现了事件的内部存储机制。AddEventHandler 方法将委托值与键关联，GetEventHandler 方法返回当前与键关联的委托，而 RemoveEventHandler 方法将委托作为指定事件的事件处理程序移除。推测底层存储机制设计为将 null 委托值与键关联没有成本，因此未处理的事件不消耗存储。

## 10.8.3 静态事件和实例事件

当事件声明包含 static 修饰符时，该事件称为静态事件。当没有 static 修饰符时，该事件称为实例事件。

静态事件与特定实例无关，在静态事件的访问器中引用 this 是编译时错误。

实例事件与类的给定实例关联，并且该实例可以在该事件的访问器中作为 this (§7.6.7) 访问。

当事件在形式为 E.M 的成员访问（§7.6.4）中被引用时，如果 M 是静态事件，则 E 必须表示包含 M 的类型；如果 M 是实例事件，则 E 必须表示包含 M 的类型的实例。

静态成员和实例成员之间的差异在 §10.3.7 中进一步讨论。

## 10.8.4 虚拟、密封、重写和抽象访问器

虚拟事件声明指定该事件的访问器是虚拟的。virtual 修饰符适用于事件的两个访问器。

抽象事件声明指定事件的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写事件为访问器提供自己的实现。由于抽象事件声明不提供实际实现，因此它不能提供用大括号分隔的事件访问器声明。

包含 abstract 和 override 修饰符的事件声明指定该事件是抽象的并且重写了基事件。此类事件的访问器也是抽象的。

抽象事件声明仅允许在抽象类中（§10.1.1.1）。

继承的虚拟事件的访问器可以通过包含指定 override 修饰符的事件声明在派生类中被重写。这称为重写事件声明。重写事件声明不会声明新事件。相反，它只是专门化现有虚拟事件的访问器的实现。

重写事件声明必须指定与被重写事件完全相同的可访问性修饰符、类型和名称。

重写事件声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该事件。密封事件的访问器也是密封的。

重写事件声明包含 new 修饰符是编译时错误。

除了声明和调用语法上的差异外，virtual、sealed、override 和 abstract 访问器与 virtual、sealed、override 和 abstract 方法完全相同。具体来说，§10.6.3、§10.6.4、§10.6.5 和 §10.6.6 中描述的规则就好像访问器是相应形式的方法一样适用。每个访问器对应于一个具有事件类型单个 value 参数、void 返回类型以及与包含事件相同的修饰符的方法。

## 10.9 索引器

索引器是使对象能够像数组一样被索引的成员。索引器使用索引器声明进行声明：


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

索引器声明可以包含一组特性（§17）、四个访问修饰符的有效组合（§10.3.5），以及 new（§10.3.4）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符。

索引器声明在修饰符的有效组合方面遵循与方法声明（§10.6）相同的规则，唯一例外是索引器声明中不允许使用 static 修饰符。

修饰符 virtual、override 和 abstract 互斥，但有一种情况例外。abstract 和 override 修饰符可以一起使用，以便抽象索引器可以重写虚拟索引器。

索引器声明的类型指定该声明所引入索引器的元素类型。除非索引器是显式接口成员实现，否则类型后面跟关键字 this。对于显式接口成员实现，类型后面跟一个接口类型、一个“.”以及关键字 this。与其他成员不同，索引器没有用户定义的名称。

形参列表指定索引器的参数。索引器的形参列表与方法（§10.6.1）的形参列表对应，但必须至少指定一个参数，并且不允许使用 ref 和 out 参数修饰符。

索引器的*类型*以及*形参列表*中引用的每个类型，其可访问性必须至少与索引器本身相同（§3.5.4）。

*访问器声明*（§10.7.2）必须括在“{”和“}”标记中，它们声明索引器的访问器。访问器指定与读取和写入索引器元素相关联的可执行语句。

尽管访问索引器元素的语法与访问数组元素的语法相同，但索引器元素不被归类为变量。因此，不能将索引器元素作为 `ref` 或 `out` 实参传递。

索引器的形参列表定义索引器的签名（§3.6）。具体而言，索引器的签名由其形参的数量和类型组成。元素类型和形参名称不属于索引器签名的一部分。

索引器的签名必须不同于同一类中声明的所有其他索引器的签名。

索引器和属性在概念上非常相似，但有以下不同之处：

- 属性由其名称标识，而索引器由其签名标识。
- 属性通过*简单名*（§7.6.2）或*成员访问*（§7.6.4）访问，而索引器元素通过*元素访问*（§7.6.6.2）访问。
- 属性可以是 `static` 成员，而索引器始终是实例成员。
- 属性的 get 访问器对应于无参数的方法，而索引器的 get 访问器对应于与索引器具有相同形参列表的方法。
- 属性的 set 访问器对应于带有一个名为 `value` 的参数的方法，而索引器的 set 访问器对应于与索引器具有相同形参列表的方法，再加上一个名为 `value` 的附加参数。
- 索引器访问器声明与索引器参数同名的局部变量属于编译时错误。
- 在重写属性声明中，使用语法 `base.P` 访问继承的属性，其中 `P` 是属性名。在重写索引器声明中，使用语法 `base[E]` 访问继承的索引器，其中 `E` 是以逗号分隔的表达式列表。

除这些差异外，§10.7.2 和 §10.7.3 中定义的所有规则既适用于属性访问器，也适用于索引器访问器。

> > **JON SKEET** 我觉得很奇怪：事件可以是 static（但几乎从不如此），而索引器却不可以。例如，Encoding.GetEncoding(string) 若作为静态索引器存在，也许是有意义的。实际上，我期望静态索引器主要充当其声明类型的工厂成员。在大多数地方，方法完全足以作为替代方案，但禁止静态索引器有点奇怪。

当索引器声明包含 extern 修饰符时，该索引器称为外部索引器。由于外部索引器声明不提供实际实现，其每个访问器声明都由一个分号组成。

下面的示例声明一个 BitArray 类，该类实现一个用于访问位数组中各个位的索引器。

```csharp
using System;
class BitArray
{
    int[] bits;
    int length;

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
            return (bits[index >> 5] & (1 << (index & 31))) != 0;
        }
        set {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            if (value) {
                bits[index >> 5] |= 1 << (index & 31);
            }
            else {
                bits[index >> 5] &= ~(1 << (index & 31));
            }
        }
    }
}
```

BitArray 类的实例消耗的内存远少于相应的 bool[]（因为前者的每个值只占一位，而不是后者的一个字节），但它允许与 bool[] 相同的操作。

下面的 CountPrimes 类使用 BitArray 和经典的“筛法”算法计算 1 与给定最大值之间的素数个数：

```csharp
class CountPrimes
{
    static int Count(int max) {
        BitArray flags = new BitArray(max + 1);
        int count = 1;
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
        Console.WriteLine("Found {0} primes between 1 and {1}", count, max);
    }
}
```

请注意，访问 BitArray 元素的语法与访问 bool[] 的语法完全相同。

下面的示例展示一个 26 × 10 的网格类，它有一个带两个参数的索引器。第一个参数必须是 A–Z 范围内的大写或小写字母，第二个参数必须是 0–9 范围内的整数。

```csharp
using System;

class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;

    int[,] cells = new int[NumRows, NumCols];

    public int this[char c, int col] {
        get {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            return cells[c - 'A', col];
        }
        set {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            cells[c - 'A', col] = value;
        }
    }
}
```

## 10.9.1 索引器重载

索引器重载解析规则在 §7.5.2 中描述。

## 10.10 运算符

*运算符*是一种成员，它定义可应用于类实例的表达式运算符的含义。运算符使用*运算符声明*来声明：

*operator-declaration:*
    *attributes*ₒₚₜ *operator-modifiers* *operator-declarator* *operator-body*

*operator-modifiers:*
    *operator-modifier*
    *operator-modifiers* *operator-modifier*

*operator-modifier:*
    public
    static
    extern

*operator-declarator:*
    *unary-operator-declarator*
    *binary-operator-declarator*
    *conversion-operator-declarator*




```
unary-operator-declarator:
    type operator overloadable-unary-operator ( type identifier )
```

```
overloadable-unary-operator: one of
    +  -  !  ~  ++  --  true  false
```

```
binary-operator-declarator:
    type operator overloadable-binary-operator ( type identifier , type identifier )
```

- overloadable-binary-operator:
  - +
  - -
  - *
  - /
  - %
  - &
  - |
  - ^
  - <<
  - >>
  - ==
  - !=
  - >
  - <
  - >=
  - <=

```
conversion-operator-declarator:
    implicit operator type ( type identifier )
    explicit operator type ( type identifier )
```

```
operator-body:
    block
    ;
```

可重载运算符分为三类：一元运算符（§10.10.1）、二元运算符（§10.10.2）和转换运算符（§10.10.3）。

当运算符声明包含 `extern` 修饰符时，该运算符称为外部运算符。由于外部运算符不提供实际实现，其运算符主体由分号组成。对于所有其他运算符，运算符主体由一个块组成，该块指定调用运算符时要执行的语句。运算符的块必须符合 §10.6.10 中所述的有返回值方法的规则。

以下规则适用于所有运算符声明：

- 运算符声明必须同时包含 `public` 和 `static` 修饰符。
- 运算符的参数必须是值参数。运算符声明指定 `ref` 或 `out` 参数会导致编译时错误。
- 运算符的签名（§10.10.1、§10.10.2、§10.10.3）必须不同于同一类中声明的所有其他运算符的签名。
- 运算符声明中引用的所有类型的可访问性都必须至少与运算符本身相同（§3.5.4）。
- 同一修饰符在运算符声明中出现多次是错误的。

每个运算符类别都会施加额外限制，如下文各节所述。

与其他成员一样，基类中声明的运算符由派生类继承。由于运算符声明始终要求声明该运算符的类或结构参与该运算符的签名，因此派生类中声明的运算符不可能隐藏基类中声明的运算符。因此，在运算符声明中，`new` 修饰符永远不是必需的，也因此永远不允许使用。

有关一元运算符和二元运算符的更多信息，请参阅 §7.3。

有关转换运算符的更多信息，请参阅 §6.4。

## 10.10.1 一元运算符

以下规则适用于一元运算符声明，其中 `T` 表示包含该运算符声明的类或结构的实例类型：

- 一元 `+`、`-`、`!` 或 `~` 运算符必须采用一个类型为 `T` 或 `T?` 的参数，并且可以返回任何类型。
- 一元 `++` 或 `--` 运算符必须采用一个类型为 `T` 或 `T?` 的参数，并且必须返回该相同类型或从中派生的类型。
- 一元 `true` 或 `false` 运算符必须采用一个类型为 `T` 或 `T?` 的参数，并且必须返回类型 `bool`。

一元运算符的签名由运算符标记（`+`、`-`、`!`、`~`、`++`、`--`、`true` 或 `false`）和单个形参的类型组成。返回类型不是一元运算符签名的一部分，形参的名称也不是。

true 和 false 一元运算符要求成对声明。如果某个类声明了其中一个运算符而未同时声明另一个，则会发生编译时错误。true 和 false 运算符在 §7.12.2 和 §7.20 中进一步描述。

以下示例展示整数向量类的 operator ++ 的实现及后续用法：

```csharp
public class IntVector
{
    public IntVector(int length) {...}
    public int Length {...}                  // Read-only property
    public int this[int index] {...}         // Read-write indexer
    public static IntVector operator ++(IntVector iv) {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
            temp[i] = iv[i] + 1;
        return temp;
    }
}
class Test
{
    static void Main() {
        IntVector iv1 = new IntVector(4);    // Vector of 4 x 0
        IntVector iv2;

        iv2 = iv1++;                          // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;                          // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

请注意，该运算符方法返回将操作数加 1 后产生的值，就像后缀递增和递减运算符（§7.6.9）以及前缀递增和递减运算符（§7.7.5）一样。与 C++ 中不同，此方法无需直接修改其操作数的值。事实上，修改操作数的值会违反后缀递增运算符的标准语义。

## 10.10.2 二元运算符

以下规则适用于二元运算符声明，其中 `T` 表示包含该运算符声明的类或结构的实例类型：

- 二元非移位运算符必须采用两个参数，其中至少一个参数的类型必须为 `T` 或 `T?`，并且可以返回任何类型。
- 二元 `<<` 或 `>>` 运算符必须采用两个参数，第一个参数的类型必须为 `T` 或 `T?`，第二个参数的类型必须为 `int` 或 `int?`，并且可以返回任何类型。

二元运算符的签名由运算符标记（`+`、`-`、`*`、`/`、`%`、`&`、`|`、`^`、`<<`、`>>`、`==`、`!=`、`>`、`<`、`>=`、`<=`）和两个形参的类型组成。返回类型和形参的名称不是二元运算符签名的一部分。

某些二元运算符要求成对声明。对于一对运算符中任一运算符的每个声明，都必须存在该对中另一运算符的匹配声明。当两个运算符声明具有相同的返回类型且每个参数的类型相同时，这两个声明匹配。以下运算符要求成对声明：

- 运算符 `==` 和运算符 `!=`
- 运算符 `>` 和运算符 `<`
- 运算符 `>=` 和运算符 `<=`

> **埃里克·利珀特** 人们很容易想在 Clothing 类上定义一个比较运算符，该类可表示 Socks、Shoes、Shirt、Tie 和 Hat，然后定义用户定义的比较，使得 Socks < Shoes、Shirt < Tie，而其他所有项都相等。这样做的希望在于，对这些项的数组进行排序会产生合理的顺序——Socks 总是排在 Shoes 之前，Shirt 排在 Tie 之前，但其他所有项可以按任意顺序排列。然而，这种比较在逻辑上并不一致：如果 Hat 等于 Socks，Hat 等于 Shoes，且 Socks 小于 Shoes，那么从逻辑上讲，Hat 必须小于 Hat，这是荒谬的。大多数排序算法都假设比较运算符定义全序；当给定一个不健全的比较运算符时，一些算法会崩溃、永远运行或给出荒谬的结果。如果要实现偏序排序，明智的做法是通过重载比较运算符以外的某种机制来实现。

## 10.10.3 转换运算符

转换运算符声明引入用户定义转换（§6.4），该转换扩充预定义的隐式转换和显式转换。

包含 `implicit` 关键字的转换运算符声明引入用户定义的隐式转换。隐式转换可出现在多种情形中，包括函数成员调用、强制转换表达式和赋值。§6.1 对此做了进一步描述。

> **比尔·瓦格纳** 隐式转换应始终成功且绝不丢失信息，因为它们会在客户端程序员不知情的情况下被自动调用。出于同样的原因，隐式转换绝不应涉及开销高昂的操作。

> **乔恩·斯基特** 正如 §6.1.2 所述，某些从整型到 `float` 或 `double` 的隐式转换可能会丢失信息。不过，这一可能性不应成为你自己定义的用户定义隐式转换丢失信息的借口。

包含 `explicit` 关键字的转换运算符声明引入用户定义的显式转换。显式转换可出现在强制转换表达式中，§6.2 对此做了进一步描述。

> **比尔·瓦格纳** 与隐式转换不同，显式转换可能失败，也可能丢失信息，因为用户必须显式请求该转换。

转换运算符从源类型转换为目标类型，源类型由转换运算符的参数类型指示，目标类型由转换运算符的返回类型指示。

对于给定的源类型 S 和目标类型 T，如果 S 或 T 是可空类型，则让 S₀ 和 T₀ 指代它们的基础类型；否则，S₀ 和 T₀ 分别等于 S 和 T。仅当以下所有条件都成立时，才允许类或结构声明从源类型 S 到目标类型 T 的转换：

- S₀ 和 T₀ 是不同的类型。
- S₀ 或 T₀ 是声明该运算符的类或结构类型。
- S₀ 和 T₀ 都不是*接口类型*。
- 除用户定义转换外，不存在从 S 到 T 或从 T 到 S 的转换。

就这些规则而言，与 S 或 T 关联的任何类型参数都被视为与其他类型没有继承关系的唯一类型，并且忽略这些类型参数上的任何约束。

在以下示例中：

```csharp
class C<T> { ... }
class D<T> : C<T>
{
    public static implicit operator C<int>(D<T> value) {...}  // Okay
    public static implicit operator C<string>(D<T> value) {...} // Okay
    public static implicit operator C<T>(D<T> value) {...}  // Error
}
```



前两个运算符声明是允许的，因为就 §10.9.3 的目的而言，T 分别与 int 和 string 没有关系；在两种情况下，它们都被视为唯一的类型。然而，第三个运算符是错误，因为 C<T> 是 D<T> 的基类。

根据第二条规则可知，转换运算符必须将运算符声明所在的类或结构体类型转换为或从该类型转换。例如，类或结构体类型 C 可以定义从 C 到 int 的转换以及从 int 到 C 的转换，但不能从 int 到 bool。

不可能直接重新定义预定义转换。因此转换运算符不允许从 object 转换或转换到 object，因为 object 与所有其他类型之间已存在隐式和显式转换。同样，转换的源类型或目标类型也不能是对方的基类型，因为那样转换已经存在。

然而，可以在泛型类型上声明运算符，对于特定的类型参数，指定已作为预定义转换存在的转换。在示例中

```csharp
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```

当将类型 object 指定为 T 的类型参数时，第二个运算符声明的转换已存在（从任何类型到类型 object 存在隐式转换，因此也存在显式转换）。

在两种类型之间存在预定义转换的情况下，两种类型之间的任何用户定义转换都会被忽略。具体而言：

- 如果从类型 S 到类型 T 存在预定义隐式转换（§6.1），则从 S 到 T 的所有用户定义转换（隐式或显式）将被忽略。
- 如果从类型 S 到类型 T 存在预定义显式转换（§6.2），则从 S 到 T 的任何用户定义显式转换将被忽略。此外：
  - 如果 T 是接口类型，则从 S 到 T 的用户定义隐式转换将被忽略。
  - 否则，从 S 到 T 的用户定义隐式转换仍会被考虑。

对于除 object 之外的所有类型，上面 Convertible<T> 类型声明的运算符不会与预定义转换冲突。例如：

```csharp
void f(int i, Convertible<int> n) {
    i = n;                 // Error
    i = (int)n;            // User-defined explicit conversion
    n = i;                 // User-defined implicit conversion
    n = (Convertible<int>)i;  // User-defined implicit conversion
}
```

然而，对于类型 object，预定义转换在除一种情况外的所有情况下都会隐藏用户定义转换：

```csharp
void F(object o, ConvertibleObject n) {
    o = n;                     // Predefined boxing conversion
    o = (object)n;             // Predefined boxing conversion
    n = o;                     // User-defined implicit conversion
    n = (ConvertibleObject)o;  // Predefined unboxing conversion
}
```

不允许用户定义转换从接口类型转换或转换到接口类型。特别是，此限制确保在转换到接口类型时不会发生用户定义的转换，并且只有在被转换的对象实际实现了指定的接口类型时，转换到接口类型才会成功。

转换运算符的签名由源类型和目标类型组成。（请注意，这是返回类型参与签名的唯一形式的成员。）转换运算符的隐式或显式分类不是运算符签名的一部分。因此类或结构体不能同时声明具有相同源类型和目标类型的隐式和显式转换运算符。

通常，用户定义的隐式转换应设计为永不抛出异常且永不丢失信息。如果用户定义的转换可能引发异常（例如，因为源参数超出范围）或导致信息丢失（例如丢弃高位），则该转换应定义为显式转换。

在示例中

```csharp
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

从 Digit 到 byte 的转换是隐式的，因为它永不抛出异常也不丢失信息，但从 byte 到 Digit 的转换是显式的，因为 Digit 只能表示 byte 可能值的一个子集。

## 10.11 实例构造函数

实例构造函数是实现初始化类实例所需操作的成员。实例构造函数使用构造函数声明：

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

构造函数声明可能会包含一组特性（§17）、四个访问修饰符（§10.3.5）的有效组合，以及 extern（§10.6.7）修饰符。构造函数声明不允许包含重复的修饰符。

构造函数声明符的标识符必须命名声明实例构造函数的类。如果指定了其他名称，将发生编译时错误。

实例构造函数的可选形式参数列表须遵守与方法（§10.6）的形式参数列表相同的规则。形式参数列表定义实例构造函数的签名（§3.6），并控制重载解析（§7.5.2）在调用中选择特定实例构造函数的过程。

实例构造函数的形式参数列表中引用的每种类型必须至少与构造函数本身一样可访问（§3.5.4）。

可选的构造函数初始化器指定在执行此实例构造函数的构造函数体中给出的语句之前调用的另一个实例构造函数。这在 §10.11.1 中进一步描述。

当构造函数声明包含 extern 修饰符时，该构造函数称为外部构造函数。由于外部构造函数声明不提供实际实现，其构造函数体由分号组成。对于所有其他构造函数，构造函数体由一个块组成，该块指定初始化类的新实例的语句。这与返回类型为 void 的实例方法（§10.6.10）的块完全对应。

实例构造函数不会被继承。因此，类没有除在类中实际声明的实例构造函数之外的其他实例构造函数。如果类不包含实例构造函数声明，则会自动提供默认实例构造函数（§10.11.4）。

实例构造函数由对象创建表达式（§7.6.10.1）以及通过构造函数初始化器调用。

### 10.11.1 构造函数初始化器

所有实例构造函数（类 object 的构造函数除外）都在构造函数体之前隐式包含对另一个实例构造函数的调用。要隐式调用的构造函数由构造函数初始化器确定：

- 形式为 base(argument-list_opt) 的实例构造函数初始化器会导致从直接基类调用一个实例构造函数。该构造函数使用 argument-list 和 §7.5.3 的重载解析规则进行选择。候选实例构造函数的集合由直接基类中包含的所有可访问实例构造函数组成，如果直接基类中未声明实例构造函数，则为默认构造函数（§10.11.4）。如果该集合为空，或无法识别出唯一的最佳实例构造函数，则会发生编译时错误。
- 形式为 this(argument-list_opt) 的实例构造函数初始化器会导致从类本身调用一个实例构造函数。构造函数使用 argument-list 和 §7.5.3 的重载解析规则进行选择。候选实例

构造函数由该类本身声明的所有可访问实例构造函数组成。如果此集合为空，或者无法识别出唯一的最佳实例构造函数，则会发生编译时错误。如果实例构造函数声明包含调用自身构造函数的构造函数初始化器，则会发生编译时错误。

> **VLADIMIR RESHETNIKOV**  *constructor-initializer* 中的参数只有在参数具有 `ref` 或 `out` 修饰符时才可以是类型 `dynamic`；否则会发生编译时错误（CS1975）。因此 *constructor-initializer* 从不进行动态分派。

如果实例构造函数没有构造函数初始化器，则会隐式提供形式为 `base()` 的构造函数初始化器。因此形式为

```
~~~
C(...) {...}
~~~
```

完全等价于

```
~~~
C(...): base() {...}
~~~
```

实例构造函数声明的 *formal-parameter-list* 提供的参数的作用域包括该声明的构造函数初始化器。因此构造函数初始化器允许访问构造函数的参数。例如：

```
~~~csharp
class A
{
    public A(int x, int y) {}
}

class B: A
{
    public B(int x, int y): base(x + y, x - y) {}
}
~~~
```

实例构造函数初始化器无法访问正在创建的实例。因此，在构造函数初始化器的参数表达式中引用 `this` 是编译时错误，因为参数表达式通过 *simple-name* 引用任何实例成员也是编译时错误。

## 10.11.2 实例变量初始化器

当实例构造函数没有构造函数初始化器，或其具有形式为 `base(...)` 的构造函数初始化器时，该构造函数会隐式执行其类中声明的实例字段的 *variable-initializers* 指定的初始化。这对应于一系列赋值，在进入构造函数时立即执行，并在隐式调用直接基类构造函数之前执行。变量初始化器按其在类声明中出现的文本顺序执行。

### 10.11.3 构造函数执行

变量初始化器被转换为赋值语句，并且这些赋值语句在调用基类实例构造函数之前执行。此顺序确保在任何可以访问该实例的语句执行之前，所有实例字段都已由其变量初始化器初始化。

给定示例

```csharp
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

当使用 new B() 创建 B 的实例时，产生以下输出：

```text
x = 1, y = 0
```

x 的值为 1，因为变量初始化器在调用基类实例构造函数之前执行。然而，y 的值为 0（int 的默认值），因为对 y 的赋值要等到基类构造函数返回后才执行。

将实例变量初始化器和构造函数初始化器视为在 *constructor-body* 之前自动插入的语句是有用的。示例

```csharp
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

包含多个变量初始化器；它还包含两种形式的构造函数初始化器（base 和 this）。该示例对应于下面所示的代码，其中每个注释都表示一个自动插入的语句（用于自动插入的构造函数调用的语法无效，但仅用于说明机制）。

```csharp
using System.Collections;

class A
{
    int x, y, count;

    public A() {
        x = 1;                 // Variable initializer
        y = -1;                // Variable initializer
        object();              // Invoke object() constructor
        count = 0;
    }

    public A(int n) {
        x = 1;                 // Variable initializer
        y = -1;                // Variable initializer
        object();              // Invoke object() constructor
        count = n;
    }
}

class B: A
{
    double sqrt2;
    ArrayList items;
    int max;

    public B(): this(100) {
        B(100);                // Invoke B(int) constructor
        items.Add("default");
    }

    public B(int n) : base(n - 1) {
        sqrt2 = Math.Sqrt(2.0);    // Variable initializer
        items = new ArrayList(100); // Variable initializer
        A(n - 1);                   // Invoke A(int) constructor
        max = n;
    }
}
```

## 10.11.4 默认构造函数

如果类不包含实例构造函数声明，则会自动提供默认实例构造函数。该默认构造函数仅调用直接基类的无参数构造函数。如果直接基类没有可访问的无参数实例构造函数，则会发生编译时错误。如果类是抽象的，则默认构造函数的声明可访问性为 protected。否则，默认构造函数的声明可访问性为 public。因此默认构造函数始终具有以下形式

```csharp
protected C(): base() { }
```

或

```csharp
public C(): base() { }
```

其中 C 是类的名称。

在示例中

```csharp
class Message
{
    object sender;
    string text;
}
```

提供了默认构造函数，因为类不包含实例构造函数声明。因此该示例精确等价于

```csharp
class Message
{
    object sender;
    string text;

    public Message(): base() { }
}
```

## 10.11.5 私有构造函数

当类 T 仅声明私有实例构造函数时，T 的程序文本之外的类无法从 T 派生，也无法直接创建 T 的实例。因此，如果一个类仅包含静态成员且不打算被实例化，添加一个空的私有实例构造函数将防止实例化。例如：

```csharp
public class Trig
{
    private Trig() { }    // Prevent instantiation
    public const double PI = 3.14159265358979323846;
    public static double Sin(double x) {...}
    public static double Cos(double x) {...}
    public static double Tan(double x) {...}
}
```

Trig 类对相关方法和常量进行分组，但不打算被实例化。因此它声明了一个空的私有实例构造函数。必须声明至少一个实例构造函数以抑制默认构造函数的自动生成。

> BILL WAGNER 如果一个类不打算被实例化，最好将其设为静态类。然而，如果你正在实现单例模式，私有构造函数可确保只有你的工厂方法可以创建单例对象。

> JOSEPH ALBAHARI 如果目标只是防止实例化，更简单的方法是声明该类为静态。

私有构造函数还有一个更微妙的目的，这依赖于私有构造函数仍可从同一类的静态成员中调用的事实。有时将静态方法作为实例化类的唯一公共手段会带来某些优势。例如，对于不可变对象，可以使用这种方法实现透明的对象缓存系统。

## 10.11.6 可选实例构造函数参数

this(...) 形式的构造函数初始化器通常与重载结合使用以实现可选实例构造函数参数。在示例中

```csharp
class Text
{
    public Text(): this(0, 0, null) {}
    public Text(int x, int y): this(x, y, null) {}
    public Text(int x, int y, string s) {
        // Actual constructor implementation
    }
}
```

前两个实例构造函数仅为缺失的参数提供默认值。两者都使用 `this(...)` 构造函数初始值设定项来调用第三个实例构造函数，而第三个实例构造函数实际完成初始化新实例的工作。其效果相当于可选构造函数参数：

```csharp
Text t1 = new Text();              // Same as Text(0, 0, null)
Text t2 = new Text(5, 10);         // Same as Text(5, 10, null)
Text t3 = new Text(5, 20, "Hello");
```

## 10.12 静态构造函数

*静态构造函数*是一种成员，它实现初始化封闭类类型所需的操作。静态构造函数使用*静态构造函数声明*来声明：

```text
static-constructor-declaration:
    attributes_opt   static-constructor-modifiers identifier (   ) static-constructor-body

static-constructor-modifiers:
    extern_opt static
    static extern_opt

static-constructor-body:
    block
    ;
```

一个*静态构造函数声明*可以包含一组特性（§17）和一个 *extern* 修饰符（§10.6.7）。

*静态构造函数声明*的*标识符*必须命名声明该静态构造函数的类。如果指定了任何其他名称，则发生编译时错误。

当静态构造函数声明包含 *extern* 修饰符时，该静态构造函数称为*外部静态构造函数*。由于外部静态构造函数声明不提供实际实现，其*static-constructor-body*由一个分号组成。对于所有其他静态构造函数声明，*static-constructor-body*由一个*块*组成，该块指定为初始化类而要执行的语句。这完全对应于返回类型为 void 的静态方法的*method-body*（§10.6.10）。

静态构造函数不会被继承，也不能直接调用。

封闭类类型的静态构造函数在给定应用程序域中最多执行一次。静态构造函数的执行由应用程序域中发生的下列事件中的第一个触发：

- 创建该类类型的实例。
- 引用该类类型的任何静态成员。

> **JON SKEET** 空静态构造函数的存在极有可能影响代码的行为，因为它可以改变静态字段初始值设定项的执行时机。如果你选择利用这种行为，我强烈建议你至少在静态构造函数中包含一条注释，解释你为何以及如何依赖它的存在，以避免它在日后被过于热心的维护者删除。

如果类包含作为执行起点的 Main 方法（§3.1），则该类的静态构造函数在调用 Main 方法之前执行。

要初始化新的封闭类类型，首先为该特定封闭类型创建一组新的静态字段（§10.5.1）。每个静态字段都初始化为其默认值（§5.2）。接下来，对这些静态字段执行静态字段初始值设定项（§10.4.5.1）。最后，执行静态构造函数。

### 示例

```csharp
using System;

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

必须产生以下输出

Init A
A.F
Init B
B.F

因为 A 的静态构造函数的执行由对 A.F 的调用触发，而 B 的静态构造函数的执行由对 B.F 的调用触发。

可以构造循环依赖，使带有变量初始值设定项的静态字段被观察到处于其默认值状态。

### 示例

```csharp
using System;

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
    static B() { }
    static void Main()
    {
        Console.WriteLine("X = {0}, Y = {1}", A.X, B.Y);
    }
}
```

产生以下输出：

X = 1, Y = 2

为了执行 Main 方法，系统首先在类 B 的静态构造函数之前运行 B.Y 的初始值设定项。Y 的初始值设定项导致 A 的静态构造函数运行，因为引用了 A.X 的值。A 的静态构造函数接着继续计算 X 的值，并在这样做时获取 Y 的默认值，即零。A.X 因此初始化为 1。然后，运行 A 的静态字段初始值设定项和静态构造函数的过程完成，返回到 Y 的初始值的计算，其结果变为 2。

由于对于每个封闭构造类类型，静态构造函数恰好执行一次，因此它是对类型参数实施运行时检查的方便位置，而这些检查无法通过约束（§10.1.5）在编译时检查。例如，以下类型使用静态构造函数来强制类型参数为枚举：

```csharp
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

## 10.13 析构函数

析构函数是一种成员，它实现析构类实例所需的操作。析构函数使用析构函数声明来声明：

```
destructor-declaration:
    attributes_opt extern_opt ~ identifier ( ) destructor-body

destructor-body:
    block
;
```

一个析构函数声明可以包含一组特性（§17）。

析构函数声明的标识符必须命名声明该析构函数的类。如果指定了任何其他名称，则发生编译时错误。

当析构函数声明包含 extern 修饰符时，该析构函数称为外部析构函数。由于外部析构函数声明不提供实际实现，其析构函数体由一个分号组成。对于所有其他析构函数，析构函数体由一个块组成，该块指定为析构类实例而要执行的语句。析构函数体完全对应于返回类型为 void 的实例方法的方法体（§10.6.10）。

析构函数不会被继承。因此，除了可能在该类中声明的那个析构函数之外，类没有其他析构函数。

由于析构函数要求没有参数，因此它不能被重载，所以一个类最多只能有一个析构函数。

析构函数会自动调用，不能显式调用。当任何代码都不再可能使用某个实例时，该实例就有资格被析构。实例的析构函数的执行可以在该实例有资格被析构之后的任何时间发生。当析构一个实例时，该实例继承链中的析构函数会按从派生程度最高到派生程度最低的顺序调用。析构函数可以在任何线程上执行。关于控制析构函数何时以及如何执行的规则的进一步讨论，请参见 §3.9。

> ERIC LIPPERT 显然，在析构函数中运行的代码所运行的环境，可能与程序中其他任何位置的代码所运行的环境非常不同。做任何复杂、危险、有副作用或耗时的事情都是非常糟糕的主意。特别是，以下代码会产生写入控制台的复杂副作用，仅用于教学目的，并不是你在实际析构函数中应该做什么的示例。

### 示例

```csharp
using System;

class A
{
    ~A()
    {
        Console.WriteLine("A's destructor");
    }
}

class B : A
{
    ~B()
    {
        Console.WriteLine("B's destructor");
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


产生以下输出

```
B's destructor
A's destructor
```

因为继承链中的析构函数按顺序调用，从最派生到最不派生。

> 埃里克·利珀特 传统上，“析构函数”一词指的是确定性的清理方法，而“终结器”指的是由垃圾回收器调用的非确定性清理方法。在 C# 中，“析构函数”这个名称有点不幸，属于用词不当；理想情况下，这些方法应称为“终结器”，而 IDisposable 的 Dispose 方法应称为“析构函数”。

析构函数通过重写 System.Object 上的虚方法 Finalize 来实现。不允许 C# 程序重写此方法，或直接调用它（或它的重写）。例如，以下程序

```
class A
{
    protected override void Finalize() { }    // Error
    public void F()
    {
        this.Finalize();    // Error
    }
}
```

包含两个错误。

编译器表现得就好像此方法及其重写根本不存在一样。因此，以下程序

```
class A
{
    void Finalize() { }    // Permitted
}
```

是有效的，并且所示方法隐藏了 System.Object 的 Finalize 方法。

关于从析构函数中抛出异常时的行为讨论，请参见 §16.3。

## 10.14 迭代器

使用迭代器块（§8.2）实现的函数成员（§7.5）称为*迭代器*。

只要相应函数成员的返回类型是枚举器接口（§10.14.1）之一或可枚举接口（§10.14.2）之一，迭代器块就可以用作函数成员的主体。它可以作为*方法体*、*运算符体*或*访问器体*出现，而事件、实例构造函数、静态构造函数和析构函数不能实现为迭代器。

当使用迭代器块实现函数成员时，如果该函数成员的形式参数列表指定任何 *ref* 或 *out* 参数，则会产生编译时错误。

### 10.14.1 枚举器接口

*枚举器接口*是非泛型接口 `System.Collections.IEnumerator` 以及泛型接口 `System.Collections.Generic.IEnumerator<T>` 的所有实例化。为简洁起见，本章将这些接口分别称为 `IEnumerator` 和 `IEnumerator<T>`。

> **乔恩·斯基特** 我希望“可枚举”和“枚举器”这两个术语原本是“可迭代”和“迭代器”，包括 `IEnumerable<T>` 和 `IIterator<T>` 接口。诚然，双 I 的部分很难看，但它会在迭代器和枚举之间保留更多词法空间。对枚举进行枚举，啰嗦得离奇。

### 10.14.2 可枚举接口

*可枚举接口*是非泛型接口 `System.Collections.IEnumerable` 以及泛型接口 `System.Collections.Generic.IEnumerable<T>` 的所有实例化。为简洁起见，本章将这些接口分别称为 `IEnumerable` 和 `IEnumerable<T>`。

### 10.14.3 产出类型

迭代器产生一个值序列，所有值的类型相同。此类型称为迭代器的*产出类型*。

- 返回 `IEnumerator` 或 `IEnumerable` 的迭代器的产出类型是 `object`。
- 返回 `IEnumerator<T>` 或 `IEnumerable<T>` 的迭代器的产出类型是 `T`。

### 10.14.4 枚举器对象

当使用迭代器块实现返回枚举器接口类型的函数成员时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建并返回一个*枚举器对象*。此对象封装迭代器块中指定的代码，迭代器块中代码的执行在调用枚举器对象的 MoveNext 方法时发生。枚举器对象具有以下特征：

- 它实现 IEnumerator 和 IEnumerator<T>，其中 T 是迭代器的产出类型。
- 它实现 System.IDisposable。
- 它使用传递给函数成员的实参值（如果有）和实例值的副本进行初始化。
- 它具有四种可能状态——*之前*、*运行中*、*挂起*和*之后*——并且最初处于*之前*状态。

> > **乔恩·斯基特** 迭代器块中的代码*没有任何*部分会运行，直到第一次调用 MoveNext()，这一点很烦人。这意味着如果你需要检查任何参数值，就确实应该使用两个方法：一个执行适当验证并调用第二个方法的普通方法，而第二个方法则用迭代器块实现。理想情况下，应该提供某种构造来指示迭代器块中应在构造状态机之前立即执行的部分。

枚举器对象通常是编译器生成的枚举器类的实例，该类封装迭代器块中的代码并实现枚举器接口，但也可以采用其他实现方式。如果枚举器类由编译器生成，则该类将直接或间接嵌套在包含该函数成员的类中；它将具有私有可访问性；并且它将具有保留供编译器使用的名称（§2.4.2）。

枚举器对象可以实现比上面指定的更多接口。

以下各节描述由枚举器对象提供的 IEnumerable 和 IEnumerable<T> 接口实现中 MoveNext、Current 和 Dispose 成员的确切行为。

请注意，枚举器对象不支持 IEnumerator.Reset 方法。调用此方法会导致抛出 System.NotSupportedException。

### 10.14.4.1 MoveNext 方法

枚举器对象的 MoveNext 方法封装迭代器块的代码。调用 MoveNext 方法会执行迭代器块中的代码，并适当地设置枚举器对象的 Current 属性。MoveNext 执行的确切操作取决于调用 MoveNext 时枚举器对象的状态：

- 如果枚举器对象的状态是*之前*，则调用 MoveNext 会：
  - 将状态更改为*运行中*。
  - 将迭代器块的参数（包括 this）初始化为初始化枚举器对象时保存的实参值和实例值。
  - 从头开始执行迭代器块，直到执行被中断（如下所述）。
- 如果枚举器对象的状态是*运行中*，则调用 MoveNext 的结果未指定。
- 如果枚举器对象的状态是*挂起*，则调用 MoveNext 会：
  - 将状态更改为*运行中*。
  - 将所有局部变量和参数（包括 this）的值恢复为上次挂起迭代器块执行时保存的值。请注意，自上次调用 MoveNext 以来，这些变量所引用的任何对象的内容可能已更改。
  - 在导致执行挂起的 yield return 语句之后立即恢复迭代器块的执行，并继续执行，直到执行被中断（如下所述）。
- 如果枚举器对象的状态是*之后*，则调用 MoveNext 返回 false。

当 MoveNext 执行迭代器块时，执行可以通过四种方式中断：通过 yield return 语句、通过 yield break 语句、通过遇到迭代器块的末尾，以及通过抛出异常并将其传播出迭代器块。

- 当遇到 yield return 语句（§8.14）时：
  - 计算该语句中给出的表达式，将其隐式转换为产出类型，并赋给枚举器对象的 Current 属性。
  - 迭代器主体的执行被挂起。保存所有局部变量和参数（包括 this）的值，并保存此 yield return 语句的位置。
  - 如果 yield return 语句位于一个或多个 try 块中，则此时不执行关联的 finally 块。
  - 枚举器对象的状态更改为*挂起*。
  - MoveNext 方法向调用方返回 true，指示迭代成功前进到下一个值。

- 当遇到 yield break 语句（§8.14）时：
  - 如果 yield break 语句位于一个或多个 try 块中，则执行关联的 finally 块。
  - 枚举器对象的状态更改为*之后*。
  - MoveNext 方法向调用方返回 false，指示迭代完成。

- 当遇到迭代器主体的末尾时：
  - 枚举器对象的状态更改为*之后*。
  - MoveNext 方法向调用方返回 false，指示迭代完成。

- 当抛出异常并将其传播出迭代器块时：
  - 异常传播会执行迭代器主体中适当的 finally 块。
  - 枚举器对象的状态更改为*之后*。
  - 异常传播继续到 MoveNext 方法的调用方。

### 10.14.4.2 Current 属性

枚举器对象的 Current 属性受迭代器块中的 yield return 语句影响。

当枚举器对象处于挂起状态时，Current 的值是上一次调用 MoveNext 所设置的值。当枚举器对象处于之前、运行中或之后状态时，访问 Current 的结果未指定。

对于产出类型不是 object 的迭代器，通过枚举器对象的 IEnumerable 实现访问 Current 的结果，对应于通过枚举器对象的 IEnumerator<T> 实现访问 Current 并将结果强制转换为 object。




### 10.14.4.3 Dispose 方法

`Dispose` 方法用于通过将枚举器对象置于 *之后* 状态来清理迭代。

- 如果枚举器对象的状态为 *之前*，则调用 `Dispose` 会将状态更改为 *之后*。
- 如果枚举器对象的状态为 *运行中*，则调用 `Dispose` 的结果未指定。
- 如果枚举器对象的状态为 *挂起*，则调用 `Dispose`：
  - 将状态更改为 *运行中*。
  - 执行任何 `finally` 块，就像最后执行的 `yield return` 语句是 `yield break` 语句一样。如果这导致异常被抛出并传播到迭代器主体之外，则枚举器对象的状态被设置为 *之后*，并且该异常被传播到 `Dispose` 方法的调用方。
  - 将状态更改为 *之后*。
- 如果枚举器对象的状态为 *之后*，则调用 `Dispose` 没有任何效果。

## 10.14.5 可枚举对象

当使用迭代器块实现返回可枚举接口类型的函数成员时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建并返回一个 *可枚举对象*。可枚举对象的 `GetEnumerator` 方法返回一个枚举器对象，该对象封装迭代器块中指定的代码；迭代器块中代码的执行发生在调用枚举器对象的 `MoveNext` 方法时。可枚举对象具有以下特征：

- 它实现 `IEnumerable` 和 `IEnumerable<T>`，其中 `T` 是迭代器的 yield 类型。
- 它使用传递给该函数成员的参数值（如果有）和实例值的副本进行初始化。

可枚举对象通常是编译器生成的可枚举类的实例，该类封装迭代器块中的代码并实现可枚举接口，但也可以采用其他实现方式。如果可枚举类由编译器生成，则该类将直接或间接嵌套在包含该函数成员的类中，具有私有可访问性，并具有为编译器使用保留的名称（§2.4.2）。

可枚举对象可能实现比上面指定的更多的接口。特别地，可枚举对象还可以实现 IEnumerator 和 IEnumerator<T>，使其既能充当可枚举对象又能充当枚举器。在这种实现类型中，首次调用可枚举对象的 GetEnumerator 方法时，返回可枚举对象本身。之后对可枚举对象的 GetEnumerator 的任何调用都会返回该可枚举对象的副本。因此，每个返回的枚举器都有自己的状态，一个枚举器中的更改不会影响另一个。

### 10.14.5.1 GetEnumerator 方法

可枚举对象提供 IEnumerable 和 IEnumerable<T> 接口的 GetEnumerator 方法的实现。这两个 GetEnumerator 方法共享一个公共实现，该实现获取并返回一个可用的枚举器对象。枚举器对象使用初始化可枚举对象时保存的参数值和实例值进行初始化，但除此之外，枚举器对象的功能如 §10.14.4 所述。

## 10.14.6 实现示例

本节描述基于标准 C# 构造的迭代器的一种可能实现。这里描述的实现基于 Microsoft C# 编译器所使用的相同原则，但它绝不是强制实现，也不是唯一可能的实现。

> BILL WAGNER 当你查看此示例时，请注意，编译器只是创建了你在创建自己的嵌套枚举器类时会生成的所有代码。迭代器方法使你免于大量重复工作，并提高了代码的可读性。

下面的 Stack<T> 类使用迭代器实现其 GetEnumerator 方法。该迭代器按从栈顶到栈底的顺序枚举栈中的元素。

```
using System;
using System.Collections;
using System.Collections.Generic;

class Stack<T> : IEnumerable<T>
{
    T[] items;
    int count;

public void Push(T item)
{
    if (items == null)
    {
        items = new T[4];
    }
    else if (items.Length == count)
    {
        T[] newItems = new T[count * 2];
        Array.Copy(items, 0, newItems, 0, count);
        items = newItems;
    }
    items[count++] = item;
}
public T Pop()
{
    T result = items[--count];
    items[count] = default(T);
    return result;
}
public IEnumerator<T> GetEnumerator()
{
    for (int i = count - 1; i >= 0; --i) yield return items[i];
}
```

GetEnumerator 方法可以转换为编译器生成的枚举器类的实例化，该类封装迭代器块中的代码，如下例所示：

```
class Stack<T>: IEnumerable<T>
{
    ...
    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }
    class __Enumerator1: IEnumerator<T>, IEnumerator
    {
        int __state;
        T __current;
        Stack<T> __this;
        int i;
        public __Enumerator1(Stack<T> __this) {
            this.__this = __this;
        }
        public T Current {
            get { return __current; }
        }
    }

object IEnumerator.Current {
    get { return __current; }
}

public bool MoveNext() {
    switch (__state) {
        case 1: goto __state1;
        case 2: goto __state2;
    }
    i = __this.count - 1;
__loop:
    if (i < 0) goto __state2;
    __current = __this.items[i];
    __state = 1;
    return true;
__state1:
    --i;
    goto __loop;
__state2:
    __state = 2;
    return false;
}

public void Dispose() {
    __state = 2;
}

void IEnumerator.Reset() {
    throw new NotSupportedException();
}
}
```

在前面的转换中，迭代器块中的代码被转换为状态机，并放入枚举器类的 MoveNext 方法中。此外，局部变量 i 被转换为枚举器对象中的字段，以便它可以在多次调用 MoveNext 之间继续存在。

以下示例打印整数 1 到 10 的简单乘法表。示例中的 FromTo 方法返回一个可枚举对象，并使用迭代器实现。

```
using System;
using System.Collections.Generic;

class Test
{
    static IEnumerable<int> FromTo(int from, int to)
    {
        while (from <= to) yield return from++;
    }
}
```

```csharp
static void Main()
{
    IEnumerable<int> e = FromTo(1, 10);
    foreach (int x in e)
    {
        foreach (int y in e)
        {
            Console.Write("{0,3}", x * y);
        }
        Console.WriteLine();
    }
}
```

FromTo 方法可以转换为编译器生成的可枚举类的实例化，该类封装迭代器块中的代码，如下例所示：

```csharp
using System;
using System.Threading;
using System.Collections;
using System.Collections.Generic;

class Test
{
    ...

    static IEnumerable<int> FromTo(int from, int to) {
        return new __Enumerable1(from, to);
    }

    class __Enumerable1:
        IEnumerable<int>, IEnumerable,
        IEnumerator<int>, IEnumerator
    {
        int __state;
        int __current;
        int __from;
        int from;
        int to;
        int i;

        public __Enumerable1(int __from, int to) {
            this.__from = __from;
            this.to = to;
        }

        public IEnumerator<int> GetEnumerator() {
            __Enumerable1 result = this;
            if (Interlocked.CompareExchange(ref __state, 1, 0) != 0) {
                result = new __Enumerable1(__from, to);
                result.__state = 1;
            }
            result.from = result.__from;
            return result;
        }
    }
}
```

```
IEnumerator IEnumerable.GetEnumerator() {
    return (IEnumerator)GetEnumerator();
}

public int Current {
    get { return __current; }
}

object IEnumerator.Current {
    get { return __current; }
}

public bool MoveNext() {
    switch (__state) {
    case 1:
        if (from > to) goto case 2;
        __current = from++;
        __state = 1;
        return true;
    case 2:
        __state = 2;
        return false;
    default:
        throw new InvalidOperationException();
    }
}

public void Dispose() {
    __state = 2;
}

void IEnumerator.Reset() {
    throw new NotSupportedException();
}
}
```

该可枚举类同时实现可枚举接口和枚举器接口，使其既能充当可枚举对象又能充当枚举器。首次调用 GetEnumerator 方法时，返回可枚举对象本身。之后对可枚举对象的 GetEnumerator 的任何调用都会返回该可枚举对象的副本。因此，每个返回的枚举器都有自己的状态，一个枚举器中的更改不会影响另一个。Interlocked.CompareExchange 方法用于确保线程安全的操作。

from 和 to 参数被转换为可枚举类中的字段。由于 from 在迭代器块中被修改，因此引入了一个额外的 __from 字段，以保存每个枚举器中赋给 from 的初始值。

如果在 __state 为 0 时调用 MoveNext 方法，则它会抛出 InvalidOperationException。这可以防止在未首先调用 GetEnumerator 的情况下将可枚举对象用作枚举器对象。





The following example shows a simple tree class. The Tree<T> class implements its GetEnumerator method using an iterator. The iterator enumerates the elements of the tree in infix order.

```csharp
using System;
using System.Collections.Generic;

class Tree<T> : IEnumerable<T>
{
    T value;
    Tree<T> left;
    Tree<T> right;

    public Tree(T value, Tree<T> left, Tree<T> right)
    {
        this.value = value;
        this.left = left;
        this.right = right;
    }

    public IEnumerator<T> GetEnumerator() {
        if (left != null) foreach (T x in left) yield x;
        yield value;
        if (right != null) foreach (T x in right) yield x;
    }
}

class Program
{
    static Tree<T> MakeTree<T>(T[] items, int left, int right)
    {
        if (left > right) return null;
        int i = (left + right) / 2;
        return new Tree<T>(items[i],
            MakeTree(items, left, i - 1),
            MakeTree(items, i + 1, right));
    }
    static Tree<T> MakeTree<T>(params T[] items)
    {
        return MakeTree(items, 0, items.Length - 1);
    }

    // The output of the program is:
    // 1 2 3 4 5 6 7 8 9
    // Mon Tue Wed Thu Fri Sat Sun

    static void Main()
    {
        Tree<int> ints = MakeTree(1, 2, 3, 4, 5, 6, 7, 8, 9);
        foreach (int i in ints) Console.Write("{0} ", i);
        Console.WriteLine();
        Tree<string> strings = MakeTree(
            "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun");
        foreach (string s in strings) Console.Write("{0}, ", s);
        Console.WriteLine();
    }
}
```

The GetEnumerator method can be translated into an instantiation of a compiler-generated enumerator class that encapsulates the code in the iterator block, as shown in the following example:

```csharp
class Tree<T> : IEnumerable<T>
{
    ...
    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }
    class __Enumerator1 : IEnumerator<T>, IEnumerator
    {
        Tree<T> __this;
        IEnumerator<T> __left, __right;
        int __state;
        T __current;
        public __Enumerator1(Tree<T> __this) {
            this.__this = __this;
        }
        public T Current {
            get { return __current; }
        }
        object IEnumerator.Current {
            get { return __current; }
        }
        public bool MoveNext() {
            try {
                switch (__state) {
                    case 0:
                        __state = -1;
                        if (__this.left == null)
                            goto __yield_value;
                        __left = __this.left.GetEnumerator();
                        goto case 1;
                    case 1:
                        __state = -2;
                        if (!__left.MoveNext())
                            goto __left_dispose;
                        __current = __left.Current;
                        __state = 1;
                        return true;
__left_dispose:
    __state = -1;
    __left.Dispose();

__yield_value:
    __current = __this.value;
    __state = 2;
    return true;

case 2:
    __state = -1;
    if (__this.right == null) goto __end;
    __right = __this.right.GetEnumerator();
    goto case 3;

case 3:
    __state = -3;
    if (!__right.MoveNext()) goto __right_dispose;
    __current = __right.Current;
    __state = 3;
    return true;

__right_dispose:
    __state = -1;
    __right.Dispose();

__end:
    __state = 4;
    break;
}
}
finally {
    if (__state < 0) Dispose();
}
return false;
}
public void Dispose() {
try {
    switch (__state) {
    case 1:
    case -2:
        __left.Dispose();
        break;

    case 3:
    case -3:
        __right.Dispose();
        break;
    }
}
finally {
    __state = 4;
}
}
void IEnumerator.Reset() {
    throw new NotSupportedException();
}
}
```

The compiler generated temporaries used in the foreach statements are lifted into the __left and __right fields of the enumerator object. The __state field of the enumerator object is carefully updated so that the Dispose() method will be called correctly if an exception is thrown. Note that it is not possible to write the translated code with simple foreach statements.

# 11. 结构体

结构体与类相似，因为它们表示可以包含数据成员和函数成员的数据结构。然而，与类不同，结构体是值类型并且不需要堆分配。结构体类型变量直接包含结构体的数据，而类类型变量包含对数据的引用，后者称为对象。

> ERIC LIPPERT The statement that “structs do not require heap allocation” is not the statement “all instances of all structs are always allocated on the stack.” First, the second statement is not true: The memory for a DateTime field of a Customer class will be allocated on the heap along with the rest of the memory of the Customer class. Second, whether a local variable of value type is allocated by changing the stack register in the CPU is an implementation detail of a particular version of the framework. The specification is pointing out the opportunity for an optimization here, not stating that a particular allocation pattern is required.

结构体对于具有值语义的小型数据结构特别有用。复数、坐标系中的点或字典中的键–值对都是结构体的良好示例。这些数据结构的关键在于它们具有少量数据成员，不需要使用继承或引用标识，并且可以方便地使用值语义实现，其中赋值复制值而不是引用。

如 §4.1.4 中所述，C# 提供的简单类型，如 int、double 和 bool，实际上都是结构体类型。就像这些预定义类型是结构体一样，也可以使用结构体和运算符重载在 C# 语言中实现新的“原始”类型。本章末尾 (§11.4) 给出了此类类型的两个示例。

> BILL WAGNER All simple types are immutable. Any structs you create should also be immutable.

> > **JON SKEET** While I have always appreciated the *ability* to create user-defined value types, I've almost never found myself needing to do so. When it's appropriate, though it can be extremely useful. For example, I'm currently involved in porting a date/time API from Java, and we have three different value types all wrapping just a long. In the Java code, these are often represented as plain long values for efficiency—but using different types with different operations (and operators) available has made the C# code *vastly* more readable.

### 11.1 结构体声明

A struct-declaration is a type-declaration (§9.6) that declares a new struct:

```
struct-declaration:
    attributes_opt  struct-modifiers_opt  partial_opt  struct  identifier  type-parameter-list_opt
    struct-interfaces_opt  type-parameter-constraints-clauses_opt  struct-body  ;_opt
```

A struct-declaration consists of an optional set of attributes (§17), followed by an optional set of struct-modifiers (§11.1.1), followed by an optional partial modifier, followed by the keyword struct and an identifier that names the struct, followed by an optional type-parameter-list specification (§10.1.3), followed by an optional struct-interfaces specification (§11.1.2), followed by an optional type-parameters-constraints-clauses specification (§10.1.5), followed by a struct-body (§11.1.4), optionally followed by a semicolon.

#### 11.1.1 结构体修饰符

A struct-declaration may optionally include a sequence of struct modifiers:

```
struct-modifiers:
    struct-modifier
    struct-modifiers  struct-modifier

struct-modifier:
    new
    public
    protected
    internal
    private
```

It is a compile-time error for the same modifier to appear multiple times in a struct declaration.

The modifiers of a struct declaration have the same meaning as those of a class declaration (§10.1).




### 11.1.2 partial 修饰符

partial 修饰符表示此结构声明是一个部分类型声明。同一封闭命名空间或类型声明内具有相同名称的多个 partial struct 声明会合并形成一个 struct 声明，遵循 §10.2 中指定的规则。

### 11.1.3 结构接口

一个结构声明可以包含 struct-interfaces 规范，在这种情况下，该结构被认为直接实现了给定的接口类型。

```
struct-interfaces:
    : interface-type-list
```

接口实现在 §13.4 中进一步讨论。

### 11.1.4 结构体主体

结构的 struct-body 定义了结构体的成员。

```
struct-body:
    { struct-member-declarations_opt }
```

## 11.2 结构成员

结构的成员由其 struct-member-declarations 引入的成员以及从类型 System.ValueType 继承的成员组成。

```
struct-member-declarations:
    struct-member-declaration
    struct-member-declarations struct-member-declaration

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

除 §11.3 中所述的差异外，§10.3 至 §10.14 中提供的类成员描述同样适用于结构成员。

## 11.3 类与结构的区别

结构与类在多个重要方面存在差异：

- 结构是值类型（§11.3.1）。
- 所有结构类型都隐式继承自类 System.ValueType（§11.3.2）。
- 向结构类型变量赋值会创建所赋值的副本（§11.3.3）。
- 结构的默认值是通过将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 所产生的值（§11.3.4）。
- 装箱和拆箱操作用于在结构类型与 object 之间转换（§11.3.5）。
- this 的含义对结构不同（§7.6.7）。
- 结构的实例字段声明不允许包含变量初始值设定项（§11.3.7）。
- 结构不允许声明无参数实例构造函数（§11.3.8）。
- 结构不允许声明析构函数（§11.3.9）。

> JESSE LIBERTY 请注意，这些差异在语义上是重要的，这与 C++ 中结构和类之间的微不足道差异不同。

### 11.3.1 值语义

结构是值类型（§4.1），据说具有值语义。相比之下，类是引用类型（§4.2），据说具有引用语义。

> BILL WAGNER 下面关于结构类型变量直接包含结构数据的陈述是那些正确但具有误导性的规范陈述之一。结构可能包含引用类型的成员。结构的数据是对类类型的引用。例如：
> 
> 赋值复制对 message 的引用，而不是字符本身。

```
struct Message
{
    int code;
    string message;
    // message contains a reference to a string
    // object, not the characters in the message
}
```

结构类型变量直接包含结构的数据，而类类型变量包含对数据的引用，后者称为对象。当结构 B 包含类型为 A 的实例字段且 A 是结构类型时，A 依赖于 B 属于编译时错误。如果 X 包含类型为 Y 的实例字段，则结构 X 直接依赖于结构 Y。给定此定义，结构所依赖的结构的完整集合是直接依赖关系的传递闭包。例如，

```
struct Node
{
    int data;
    Node next; // Error: Node directly depends on itself
}
```

这是一个错误，因为 Node 包含其自身类型的实例字段。另一个例子

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

这是一个错误，因为类型 A、B 和 C 彼此相互依赖。

对于类，两个变量可能引用同一个对象，因此对一个变量的操作可能影响另一个变量引用的对象。对于结构，每个变量都有自己的数据副本（ref 和 out 参数变量的情况除外），因此一个变量上的操作不可能影响其他变量。此外，由于结构不是引用类型，因此结构类型的值不可能为 null。

给定声明

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

```
Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);
```

输出值为 10。a 赋给 b 会创建值的副本，因此 b 不受对 a.x 的赋值影响。如果 Point 改为声明为类，则输出将为 100，因为 a 和 b 将引用同一个对象。

### 11.3.2 继承

所有结构类型都隐式继承自类 System.ValueType，而后者又继承自类 object。结构声明可以指定已实现的接口列表，但结构声明不能指定基类。

结构类型永远不是抽象的，并且始终隐式密封。因此，abstract 和 sealed 修饰符不允许出现在结构声明中。

由于结构不支持继承，结构成员声明的访问性不能为 protected 或 protected internal。

结构中的函数成员不能是 abstract 或 virtual，并且 override 修饰符仅允许重写从 System.ValueType 继承的方法。

### 11.3.3 赋值

向结构类型变量赋值会创建所赋值的副本。这与向类类型变量赋值不同，后者复制引用但不复制引用所标识的对象。

类似于赋值，当结构作为值参数传递或作为函数成员的结果返回时，会创建结构的副本。结构可以使用 ref 或 out 参数按引用传递给函数成员。

> **ERIC LIPPERT** 另一种看待此问题的方式是 ref 和 out 参数为变量创建别名。与其认为“我将使用 ref 参数按引用传递此结构”，我更喜欢认为“我将使用 ref 参数使此参数成为包含此结构的变量的别名”。

当结构的属性或索引器是赋值的目标时，与属性或索引器访问关联的实例表达式必须被分类为变量。如果实例表达式被分类为值，则会发生编译时错误。这在 §7.17.1 中有更详细的描述。

### 11.3.4 默认值

如 §5.2 中所述，几种类型的变量在创建时会自动初始化为其默认值。对于类类型和其他引用类型的变量，此
默认值是 null。然而，由于结构是不能为 null 的值类型，结构的默认值是通过将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 所产生的值。

参考上面声明的 Point 结构，示例

```
```csharp
Point[] a = new Point[100];
```
```

将数组中的每个 Point 初始化为将 x 和 y 字段设置为零所产生的值。

结构的默认值对应于结构默认构造函数返回的值（§4.1.2）。与类不同，结构不允许声明无参数实例构造函数。相反，每个结构都隐式具有无参数实例构造函数，它始终返回将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 所产生的值。

结构应设计为将默认初始化状态视为有效状态。在示例中

```
```csharp
using System;
struct KeyValuePair
{
    string key;
    string value;
    public KeyValuePair(string key, string value) {
        if (key == null || value == null)
            throw new ArgumentException();
        this.key = key;
        this.value = value;
    }
}
```
```

用户定义的实例构造函数仅在显式调用时才防止 null 值。在 KeyValuePair 变量受默认值初始化的情况中，key 和 value 字段将为 null，结构必须准备好处理此状态。

### 11.3.5 装箱和拆箱

> **BILL WAGNER** 自 C# 2.0 引入以来，您经常可以通过使用泛型来避免装箱和拆箱。

类类型的值可以通过在编译时将引用视为另一种类型，简单地转换为 object 类型或由该类实现的接口类型。



同样，object 类型的值或接口类型的值可以转换回类类型，而无需更改引用（当然，在这种情况下需要进行运行时类型检查）。

由于结构体不是引用类型，因此对于结构体类型，这些操作的实现方式不同。当结构体类型的值转换为 object 类型或转换为该结构体实现的接口类型时，会发生装箱操作。同样，当 object 类型的值或接口类型的值转换回结构体类型时，会发生拆箱操作。与对类类型执行相同操作的关键区别在于，装箱和拆箱会将结构体值复制到装箱实例中或从装箱实例中复制出来。因此，在装箱或拆箱操作之后，对拆箱后的结构体所做的更改不会反映到装箱后的结构体中。

> **ERIC LIPPERT** 这又是值类型应当不可变的另一个原因：如果不可能发生更改，那么对拆箱后的结构体所做的更改不会反映到装箱后的结构体中这一事实就变得无关紧要。与其处理这些意外且令人困惑的语义，不如完全避免它们。

当结构体类型重写从 System.Object 继承的虚方法（例如 Equals、GetHashCode 或 ToString）时，通过该结构体类型的实例调用该虚方法不会导致装箱。即使将该结构体用作类型参数，并且通过类型参数类型的实例进行调用，也是如此。例如：

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

该程序的输出为

1
2
3

尽管 ToString 具有副作用是不良风格，但该示例表明，三次调用 x.ToString() 都没有发生装箱。

类似地，在访问受约束类型参数上的成员时，绝不会隐式发生装箱。例如，假设接口 ICounter 包含可用于修改值的方法 Increment。如果 ICounter 用作约束，则调用 Increment 方法的实现时，传入的是对调用 Increment 的变量的引用——绝不是装箱副本。

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
        x.Increment();
        // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();
        // Modify boxed copy of x
        Console.WriteLine(x);
    }
    static void Main() {
        Test<Counter>();
    }
}
```

第一次调用 Increment 会修改变量 x 中的值。这与第二次调用 Increment 不等价，后者修改 x 的装箱副本中的值。因此该程序的输出为

0
1
1

有关装箱和拆箱的更多详细信息，请参见 §4.3。

## 11.3.6 this 的含义

在类的实例构造函数或实例函数成员中，this 被归类为值。因此，虽然 this 可用于引用调用该函数成员的实例，但在类的函数成员中不能对 this 赋值。

在结构体的实例构造函数中，this 对应于结构体类型的 out 参数；在结构体的实例函数成员中，this 对应于结构体类型的 ref 参数。在两种情况下，this 都被归类为变量，并且可以通过对 this 赋值或将 this 作为 ref 或 out 参数传递，来修改调用该函数成员的整个结构体。

> VLADIMIR RESHETNIKOV 结构体内的匿名函数和查询表达式不能访问 this 或 this 的实例成员。

## 11.3.7 字段初始值设定项

如 §11.3.4 所述，结构体的默认值由将所有值类型字段设置为其默认值、将所有引用类型字段设置为 null 后得到的值组成。因此，结构体不允许实例字段声明包含变量初始值设定项。此限制仅适用于实例字段。结构体的静态字段允许包含变量初始值设定项。

示例

```
struct Point
{
    public int x = 1; // Error: initializer not permitted
    public int y = 1; // Error: initializer not permitted
}
```

有错误，因为实例字段声明包含变量初始值设定项。

> JOSEPH ALBAHARI 以下模式提供了一种变通方法，为 X 提供默认值 1：

```
struct Point
{
    bool initialized;  // Default value false
    int x;
    public int X {
        get {
            if (!initialized) { x = 1; initialized = true; }
            return x;
        }
    }
}
```

> ERIC LIPPERT 约瑟夫技术的更简洁版本是将标志隐藏在一个可空类型中，并使用空合并运算符：

```
struct Point
{
    private int? x; // Default value is null
    public int X { get { return x ?? 1; } }
}
```

因为可空 int 实际上是实现为包含一个 int 和一个 bool 的结构体，所以这本质上是同一种技术，只是更简洁一些。

## 11.3.8 构造函数

与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，它始终返回将所有值类型字段设置为其默认值、将所有引用类型字段设置为 null 后得到的值（§4.1.2）。结构体可以声明带参数的实例构造函数。例如：

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

都创建一个 x 和 y 初始化为零的 Point。

结构体实例构造函数不允许包含形式为 `base(...)` 的构造函数初始值设定项。

如果结构体实例构造函数未指定构造函数初始值设定项，则 `this` 变量对应于结构体类型的 `out` 参数；与 `out` 参数类似，在构造函数返回的每个位置，都必须明确赋值（§5.3）。如果结构体实例构造函数指定了构造函数初始值设定项，则 `this` 变量对应于结构体类型的 `ref` 参数；与 `ref` 参数类似，在进入构造函数体时，它被视为已明确赋值。考虑下面的实例构造函数实现：

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
        X = x;   // Error: this is not yet definitely assigned
        Y = y;   // Error: this is not yet definitely assigned
    }
}
```

在正在构造的结构体的所有字段都已明确赋值之前，不能调用任何实例成员函数（包括属性 X 和 Y 的 set 访问器）。但请注意，如果 Point 是类而不是结构体，则允许这种实例构造函数实现。

> **ERIC LIPPERT**  规范未提到，使其可行的方法是直接强制调用默认构造函数，以确保字段已初始化：

> ```csharp
> public Point(int x, int y) : this() { // Struct is guaranteed to be initialized
> ```

## 11.3.9 析构函数

结构体不允许声明析构函数。

## 11.3.10 静态构造函数

结构体的静态构造函数遵循与类的大多数相同规则。结构体类型的静态构造函数的执行由应用程序域内发生的下列事件中的第一个触发：

- 引用结构体类型的静态成员。
- 调用结构体类型的显式声明的构造函数。

创建结构体类型的默认值（§11.3.4）不会触发静态构造函数。（这方面的一个例子是数组中元素的初始值。）

## 11.4 结构体示例

下面展示了两个重要示例，说明如何使用结构体类型创建可以类似语言内置类型使用、但具有修改后语义的类型。

> **BILL WAGNER** 既然语言和框架中已经添加了可空类型，这些示例就不那么有说服力了。即便如此，我发现当创建非常大的数据值集合时，我仍然会创建用于保存类型实例的结构体类型。

## 11.4.1 数据库整数类型

下面的 DBInt 结构体实现了一个整数类型，它可以表示 int 类型的完整值集，外加一个表示未知值的附加状态。具有这些特征的类型常用于数据库中。

```
using System;

public struct DBInt
{
    // The Null member represents an unknown DBInt value.
    public static readonly DBInt Null = new DBInt();

    // When the defined field is true, this DBInt represents a
    // known value that is stored in the value field. When
    // the defined field is false, this DBInt represents an
    // unknown value, and the value field is 0.
```



```csharp
int value;
bool defined;
// Private instance constructor.
// Creates a DBInt with a known value.
DBInt(int value) {
    this.value = value;
    this.defined = true;
}

// The IsNull property is true if this
// DBInt represents an unknown value.
public bool IsNull { get { return !defined; } }
// The Value property is the known value of this DBInt,
// or 0 if this DBInt represents an unknown value.
public int Value { get { return value; } }
// Implicit conversion from int to DBInt.
public static implicit operator DBInt(int x) {
    return new DBInt(x);
}

// Explicit conversion from DBInt to int. Throws an
// exception if the given DBInt represents an unknown value.
public static explicit operator int(DBInt x) {
    if (!x.defined) throw new InvalidOperationException();
    return x.value;
}

public static DBInt operator +(DBInt x) {
    return x;
}

public static DBInt operator -(DBInt x) {
    return x.defined ? -x.value : Null;
}

public static DBInt operator +(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value + y.value: Null;
}

public static DBInt operator -(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value - y.value: Null;
}

public static DBInt operator *(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value * y.value: Null;
}

public static DBInt operator /(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value / y.value: Null;
}

public static DBInt operator %(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value % y.value: Null;
}

public static DBBool operator ==(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value == y.value: DBBool.Null;
}

public static DBBool operator !=(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value != y.value: DBBool.Null;
}

public static DBBool operator >(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value > y.value: DBBool.Null;
}

public static DBBool operator <(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value < y.value: DBBool.Null;
}

public static DBBool operator >=(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value >= y.value: DBBool.Null;
}

public static DBBool operator <=(DBInt x, DBInt y) {
    return x.defined &&
        y.defined? x.value <= y.value: DBBool.Null;
}

public override bool Equals(object obj) {
    if (!(obj is DBInt)) return false;
    DBInt x = (DBInt)obj;
    return value == x.value && defined == x.defined;
}

public override int GetHashCode() {
    return value;
}

public override string ToString() {
    return defined? value.ToString():"DBInt.Null";
}
}
```

> **CHRISTIAN NAGEL** 在命名空间 System.Data.SqlTypes 中，.NET 包含映射结构，例如 SqlBoolean 和 SqlInt32，它们与这里的示例 DBInt 和 DBBool 有些相似。这些类型自 .NET 1.0 起就可用，并被创建以允许空值，就像原生数据库类型所能做的那样。鉴于可空类型自 .NET 2.0 起就可用，可以避免创建自定义类型，而改用 int? 和 bool?。

## 11.4.2 数据库布尔类型

下面的 DBBool 结构体实现了一个三值逻辑类型。此类型的可能值是 DBBool.True、DBBool.False 和 DBBool.Null，其中 Null 成员表示未知值。这种三值逻辑类型在数据库中很常见。

```csharp
using System;
public struct DBBool
{
    // The three possible DBBool values.
    public static readonly DBBool Null = new DBBool(0);
    public static readonly DBBool False = new DBBool(-1);
    public static readonly DBBool True = new DBBool(1);
    // Private field that stores -1, 0, 1 for False, Null, True.
    sbyte value;
    // Private instance constructor.
    // The value parameter must be -1, 0, or 1.
    DBBool(int value) {
        this.value = (sbyte)value;
    }
    // Properties to examine the value of a DBBool. Return true
    // if this DBBool has the given value, false otherwise.
    public bool IsNull { get { return value == 0; } }
    public bool IsFalse { get { return value < 0; } }
    public bool IsTrue { get { return value > 0; } }
    // Implicit conversion from bool to DBBool. Maps true to
    // DBBool.True and false to DBBool.False.
    public static implicit operator DBBool(bool x) {
        return x ? True : False;
    }
    // Explicit conversion from DBBool to bool.
    // Throws an exception if the given DBBool
    // is Null; otherwise, returns true or false.
    public static explicit operator bool(DBBool x) {
        if (x.value == 0) throw new InvalidOperationException();
        return x.value > 0;
    }
    // Equality operator. Returns Null if either operand is Null;
    // otherwise, returns True or False.
    public static DBBool operator ==(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value == y.value? True: False;
    }
    // Inequality operator. Returns Null if either operand is Null;
    // otherwise, returns True or False.
    public static DBBool operator !=(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value != y.value? True: False;
    }
    // Logical negation operator. Returns True if the operand is
    // False, Null if the operand is Null,
    // or False if the operand is True.
    public static DBBool operator !(DBBool x) {
        return new DBBool(-x.value);
    }
    // Logical AND operator. Returns False if either operand is False;
    // otherwise, Null if either operand is Null; otherwise, True.
    public static DBBool operator &(DBBool x, DBBool y) {
        return new DBBool(x.value < y.value? x.value: y.value);
    }
    // Logical OR operator. Returns True if either operand is True;
    // otherwise, Null if either operand is Null; otherwise, False.
    public static DBBool operator |(DBBool x, DBBool y) {
        return new DBBool(x.value > y.value? x.value: y.value);
    }
    // Definitely true operator. Returns true if the
    // operand is True, false otherwise.
    public static bool operator true(DBBool x) {
        return x.value > 0;
    }
    // Definitely false operator. Returns true if the
    // operand is False, false otherwise.
    public static bool operator false(DBBool x) {
        return x.value < 0;
    }
    public override bool Equals(object obj) {
        if (!(obj is DBBool)) return false;
        return value == ((DBBool)obj).value;
    }
    public override int GetHashCode() {
        return value;
    }
    public override string ToString() {
        if (value > 0) return "DBBool.True";
        if (value < 0) return "DBBool.False";
        return "DBBool.Null";
    }
}
```

> **CHRIS SELLS** 当 .NET 首次推出时，用户定义的值类型是该系统区别于 Java 的重要差异点。实际上，我发现这些类型大多是在分析显示垃圾回收器在没有值得的目标上过度工作后才作为优化手段使用的。

> **ERIC LIPPERT** 某些值类型的局部变量可以廉价地分配在栈上这一事实，并不自动使其比引用类型“性能更高”。堆分配比栈分配稍贵，但仍然相当便宜。真正的成本节约通常来自于释放：堆上分配的对象越少，垃圾回收器需要识别和压缩的潜在垃圾就越少。即使如此，分配和释放的任何成本节约往往会被按值复制值类型的需求所抵消。处理器针对复制大小近似于引用大小的事物进行了优化。值类型的大小可能很奇怪并且会被大量复制，这在某些情况下会增加总成本。

> 我的建议是根据按值复制还是按引用复制更有意义来做出值与引用的选择，然后使用分析器进行性能测试。只有在你有良好的、经验性的、可重复的数据表明这样做会带来可衡量且重要的差异时，才将引用类型更改为值类型（或反之）。



## 12. 数组

数组是一种数据结构，它包含若干通过计算得到的索引来访问的变量。数组中包含的变量也称为数组的元素，它们都具有相同的类型，这种类型称为数组的元素类型。

数组具有一个秩，它确定与每个数组元素关联的索引数目。数组的秩也称为数组的维度。秩为 1 的数组称为*一维数组*。秩大于 1 的数组称为*多维数组*。特定大小的多维数组通常称为二维数组、三维数组等。

数组的每个维度都有一个关联的长度，它是一个大于或等于零的整数。维度长度不是数组类型的一部分，而是在运行时创建数组类型的实例时确立。维度的长度确定该维度的有效索引范围：对于长度为 *N* 的维度，索引范围可以从 0 到 *N* - 1（含）。数组中元素的总数是数组中每个维度长度的乘积。如果数组的一个或多个维度的长度为零，则称该数组为空。

数组的元素类型可以是任何类型，包括数组类型。

### 12.1 数组类型

数组类型写作一个*非数组类型*，后跟一个或多个*秩说明符*：

```
    array-type:
        non-array-type rank-specifiers

    non-array-type:
        type

    rank-specifiers:
        rank-specifier
        rank-specifiers rank-specifier
```

```text
rank-specifier:
    [   dim-separators_opt   ]

dim-separators:
    ,
    dim-separators ,
```

非数组类型是任何本身不是数组类型的类型。

数组类型的秩由该数组类型中最左边的秩说明符给出。秩说明符指示该数组是一个秩为 1 加上该秩说明符中“,”标记数的数组。

数组类型的元素类型是删除最左边秩说明符后得到的类型：

- 形式为 T[R] 的数组类型是秩为 R、非数组元素类型为 T 的数组。
- 形式为 T[R][R]...[R] 的数组类型是秩为 R、元素类型为 T[R]...[R] 的数组。

实际上，秩说明符是在最终的非数组元素类型之前从左到右读取的。类型 int[][,][,] 是一个一维数组，其元素是 int 的二维数组的三维数组。

> **ERIC LIPPERT** 数组的数组的秩说明符以“反向”读取这一事实常常令人困惑。实际上，这种方案有一个很好的性质：索引操作与声明以相同顺序进行；你会按 `arr[a][b,c,d][e,f]` 那样索引那个复杂数组。

在运行时，数组类型的值可以是 null，也可以是对该数组类型实例的引用。

### 12.1.1 System.Array 类型

System.Array 类型是所有数组类型的抽象基类型。存在从任何数组类型到 System.Array 的隐式引用转换（§6.1.6），以及从 System.Array 到任何数组类型的显式引用转换（§6.2.4）。注意，System.Array 本身不是数组类型。相反，它是所有数组类型都派生自的类类型。

在运行时，System.Array 类型的值可以是 null，也可以是对任何数组类型实例的引用。

### 12.1.2 数组与泛型 IList 接口

一维数组 T[] 实现接口 System.Collections.Generic.IList<T>（简称 IList<T>）及其基接口。因此，存在从 T[] 到 IList<T> 及其基接口的隐式转换。此外，如果存在从 S 到 T 的隐式引用转换，那么 S[] 实现 IList<T>，并且存在从 S[] 到 IList<T> 及其基接口的隐式引用转换（§6.1.6）。如果存在从 S 到 T 的显式引用转换，那么存在从 S[] 到 IList<T> 及其基接口的显式引用转换（§6.2.4）。例如：

```csharp
using System.Collections.Generic;

class Test
{
    static void Main() {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;

        IList<string> lst1 = sa;        // Okay
        IList<string> lst2 = oa1;       // Error: cast needed
        IList<object> lst3 = sa;        // Okay
        IList<object> lst4 = oa1;       // Okay

        IList<string> lst5 = (IList<string>)oa1;  // Exception
        IList<string> lst6 = (IList<string>)oa2;  // Okay
    }
}
```

赋值 lst2 = oa1 会产生编译时错误，因为从 object[] 到 IList<string> 的转换是显式转换，而不是隐式转换。强制转换 (IList<string>) oa1 将在运行时引发异常，因为 oa1 引用的是 object[] 而不是 string[]。然而，强制转换 (IList<string>)oa2 不会引发异常，因为 oa2 引用的是 string[]。

每当存在从 S[] 到 IList<T> 的隐式或显式引用转换时，也存在从 IList<T> 及其基接口到 S[] 的显式引用转换（§6.2.4）。

当数组类型 S[] 实现 IList<T> 时，所实现接口的某些成员可能会引发异常。该接口实现的确切行为超出了本规范的范围。

> **ERIC LIPPERT** 考虑一个反事实世界是很有趣的：CLR 在版本 1 中就有泛型类型。在那个反事实世界中，可能会有泛型数组类型 Array<>、Array2<> 等。在那个世界中，复杂数组类型的声明变得更加清晰：Array2<int,int> 是一个一维数组，其中每个元素都是整数的二维数组。

> **BILL WAGNER** 数组 T[] 通过为某些方法抛出异常来实现 IList<T>，这是现实世界中令人烦恼的问题之一，对此没有好的解决方案。IList<T> 具有添加或移除元素的方法。然而，数组具有固定大小，无法支持其中一些方法。即便如此，你还是想使用 IList<T> 接口中存在的对元素的随机访问。

## 12.2 数组创建

数组实例由数组创建表达式（§7.6.10.4）创建，或由包含数组初始值设定项（§12.6）的字段或局部变量声明创建。

创建数组实例时，会确立秩和每个维度的长度，然后它们在实例的整个生存期内保持不变。换句话说，不可能更改现有数组实例的秩，也不可能调整其维度的大小。

数组实例始终属于数组类型。System.Array 类型是抽象类型，不能实例化。

由数组创建表达式创建的数组的元素始终初始化为其默认值（§5.2）。

## 12.3 数组元素访问

数组元素使用形式为 A[I₁, I₂, …, Iₙ] 的元素访问表达式（§7.6.6.1）进行访问，其中 A 是数组类型的表达式，每个 Iₓ 是类型为 int、uint、long 或 ulong 的表达式，或者可以隐式转换为这些类型中的一种或多种。数组元素访问的结果是一个变量——即由索引选定的数组元素。

可以使用 foreach 语句（§8.8.4）枚举数组的元素。

## 12.4 数组成员

每个数组类型都继承 System.Array 类型声明的成员。

## 12.5 数组协变

对于任意两个引用类型 A 和 B，如果存在从 A 到 B 的隐式引用转换（§6.1.6）或显式引用转换（§6.2.4），那么也存在从数组类型 A[R] 到数组类型 B[R] 的相同引用转换，其中 R 是任意给定的秩说明符（但对两个数组类型相同）。这种关系称为数组协变。特别地，数组协变意味着数组类型 A[R] 的值实际上可以是对数组类型 B[R] 实例的引用，前提是存在从 B 到 A 的隐式引用转换。

由于数组协变，对引用类型数组元素的赋值包括运行时检查，以确保要赋给数组元素的值实际上是允许的类型（§7.17.1）。例如：

```csharp
class Test
{
    static void Fill(object[] array, int index, int count, object value) {
        for (int i = index; i < index + count; i++)
            array[i] = value;
    }

    static void Main() {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```

Fill 方法中对 array[i] 的赋值隐式包含运行时检查，以确保 value 引用的对象要么为 null，要么是与 array 的实际元素类型兼容的实例。在 Main 中，前两次 Fill 调用成功，但第三次调用在执行对 array[i] 的第一次赋值时导致引发 System.ArrayTypeMismatchException。发生该异常是因为装箱的 int 不能存储在 string 数组中。

> **ERIC LIPPERT** 这是我提名的 C#“最差特性”。它允许赋值在运行时失败，而源代码中没有任何表明这种失败可能发生的指示。它给极其常见的代码施加性能成本，以使罕见场景快速执行；安全地访问非密封引用类型的数组比协变数组转换常见得多。我更喜欢已添加到 IEnumerable<T> 的类型安全协变。




> CHRIS SELLS 我发现自己很少使用数组——即使是单维数组，更不用说多维或锯齿数组了——因此那些奇怪的边界情况通常无关紧要。鉴于 List<T>、Dictionary<K, V> 和 IEnumerable<T> 的可用性，如果完全没有数组我也会很开心。

> PETER SESTOFT Eric 抱怨的运行时检查的必要性源于数组类型在元素类型上是协变的（当 Student 是 Person 的子类型时，Student[] 是 Person[] 的子类型）。这种数组协变的设计缺陷与 Java 编程语言共用，在 Java 中情况甚至更糟：因为 Java 通过类型擦除实现泛型，运行时不存在表示泛型类型参数的类型对象，因此如果数组是作为 new T[...] 为某个类型参数 T 创建的，或作为 new Stack<Person>[...] 创建的，则无法执行检查。因此 Java 必须禁止创建元素类型为类型参数或作为泛型类型的类型实例构造的类型 的数组。在 C# 中，类型参数和构造类型在运行时得到忠实表示，因此这些限制对数组创建并不存在。

> 在 Scala 语言中，该语言诞生时就带有泛型类型，数组类型在元素类型上是不变的，因此不需要运行时检查（但在 Scala 编译为 Java 字节码时很可能会仍然执行）。

> BILL WAGNER Eric 的评论在很大程度上解释了为什么 C# 4.0 为泛型添加的安全协变和逆变如此重要。用同一次更改同时提高速度和正确性通常是很少见的。

数组协变特指不扩展到值类型的数组。例如，不存在允许将 int[] 视为 object[] 的转换。

## 12.6 数组初始化器

数组初始化器可在字段声明 (§10.5)、局部变量声明 (§8.5.1) 和数组创建表达式 (§7.6.10.4) 中指定：

```
array-initializer:
{ variable-initializer-list_opt }
{ variable-initializer-list , }
```

```
variable-initializer-list:
    variable-initializer
    variable-initializer-list  ,  variable-initializer

variable-initializer:
    expression
    array-initializer
```

数组初始化器由一系列变量初始化器组成，用“{”和“}”标记括起来，并用“,”标记分隔。每个变量初始化器是一个表达式，或者在多维数组的情况下，是一个嵌套的数组初始化器。

在数组初始化器被使用的上下文决定了正在初始化的数组的类型。在数组创建表达式中，数组类型紧跟在初始化器之前，或从数组初始化器中的表达式推断得出。在字段或变量声明中，数组类型是正在声明的字段或变量的类型。当数组初始化器在字段或变量声明中使用时，例如

```
int[] a = {0, 2, 4, 6, 8};
```

它只是等效数组创建表达式的简写：

```
int[] a = new int[] {0, 2, 4, 6, 8};
```

对于单维数组，数组初始化器必须由与数组元素类型赋值兼容的表达式序列组成。表达式按递增顺序初始化数组元素，从索引 0 处的元素开始。数组初始化器中表达式的数量决定了正在创建的数组实例的长度。例如，上面的数组初始化器创建一个长度为 5 的 int[] 实例，然后用以下值初始化该实例：

```
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

对于多维数组，数组初始化器必须具有与数组中维度一样多的嵌套层级。最外层的嵌套层级对应于最左边的维度，最内层的嵌套层级对应于最右边的维度。数组每个维度的长度由数组初始化器中相应嵌套层级处的元素数量决定。对于每个嵌套的数组初始化器，其元素数量必须与同一层级的其他数组初始化器相同。示例

```
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```

创建一个二维数组，最左边维度的长度为 5，最右边维度的长度为 2：

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

如果除最右边之外的一个维度被指定为长度 0，则假定后续维度也具有长度 0。示例

```
int[,] c = {};
```

创建一个二维数组，最左边和最右边维度的长度均为 0：

```
int[,] c = new int[0, 0];
```

当数组创建表达式同时包含显式维度长度和数组初始化器时，长度必须是常量表达式，并且每个嵌套层级处的元素数量必须与相应的维度长度匹配。以下是一些示例：

```
int i = 3;
int[] x = new int[3] {0, 1, 2};    // Okay
int[] y = new int[i] {0, 1, 2};    // Error: i not a constant
int[] z = new int[3] {0, 1, 2, 3}; // Error: length/initializer mismatch
```

这里，y 的初始化器导致编译时错误，因为维度长度表达式不是常量，而 z 的初始化器导致编译时错误，因为长度和初始化器中的元素数量不一致。

## 13. 接口

接口定义了一个契约。实现接口的类或结构必须遵守其契约。接口可以继承多个基接口，类或结构可以实现多个接口。

> **BILL WAGNER** 接口在范围小且数量少时效果最佳。较大的接口会给实现者带来更多工作。接口数量越多，产生歧义和冲突的机会就越多。

> **ERIC LIPPERT** 接口是契约这一说法无疑既有用又经常被提及。值得指出的是，接口实际上是表示契约的一种相当薄弱的方式。接口告诉你的全部是哪些方法可用、它们的名字是什么、它们接受哪些类型、返回哪些类型。契约中完全没有表示操作的语义：遵守此契约的对象必须积极处置，Drive() 如果在 StartEngine() 之后未调用则抛出异常，第一个参数必须为 null 且第二个参数必须非零，等等。所有这些内容都写在文档中，而不是分析工具可以挖掘的地方。随 CLR 4.0 版本发布的新的代码契约系统使你既能比单独使用接口更详细地指定契约，又能在编译时对这些契约进行有趣的分析。

接口可以包含方法、属性、事件和索引器。接口本身不为其定义成员提供实现。接口仅指定实现接口的类或结构必须提供的成员。

### 13.1 接口声明

interface-declaration 是声明新的接口类型的 type-declaration (§9.6)。

```
interface-declaration:
    attributes_opt interface-modifiers_opt partial_opt interface
    identifier variant-type-parameter-list_opt interface-base_opt
    type-parameter-constraints-clauses_opt interface-body ;_opt
```

interface-declaration 由一组可选的属性 (§17) 组成，其后是可选的一组接口修饰符 (§13.1.1)，其后是可选的 partial 修饰符，其后是关键字 interface 和一个命名接口的标识符，其后是可选的 variant-type-parameter-list 规范 (§13.1.3)，其后是可选的 interface-base 规范 (§13.1.4)，其后是可选的 type-parameter-constraints-clauses 规范 (§10.1.5)，其后是 interface-body (§13.1.5)，可选地后跟一个分号。

### 13.1.1 接口修饰符

interface-declaration 可选择性地包含一系列接口修饰符：

```
interface-modifiers:
    interface-modifier
    interface-modifier interface-modifier
```

```
interface-modifier:
    new
    public
    protected
    internal
    private
```

在接口声明中，相同的修饰符出现多次是编译时错误。

new 修饰符仅允许在类中定义的接口上使用。它指定接口隐藏了同名继承的成员，如 §10.3.4 中所述。

public、protected、internal 和 private 修饰符控制接口的可访问性。根据接口声明出现的上下文，其中只有某些修饰符可能被允许 (§3.5.1)。

### 13.1.2 partial 修饰符

partial 修饰符表示此 interface-declaration 是一个部分类型声明。封闭命名空间或类型声明中具有相同名称的多个 partial 接口声明组合形成一个接口声明，遵循 §10.2 中指定的规则。



### 13.1.3 变体类型参数列表

变体类型参数列表只能出现在接口和委托类型上。与普通类型参数列表的区别在于每个类型参数上可选的变体注解。

```
variant-type-parameter-list:
    < variant-type-parameters >

variant-type-parameters:
    attributes_opt variance-annotation_opt type-parameter
    variant-type-parameters , attributes_opt variance-annotation_opt type-parameter

variance-annotation:
    in
    out
```

如果变体注解为 out，则称该类型参数为协变。如果变体注解为 in，则称该类型参数为逆变。如果没有变体注解，则称该类型参数为不变。

> ERIC LIPPERT 协变是这样一种性质：从类型实参到泛型类型的映射保持赋值兼容性。例如，可以将 string 赋给 object 类型的变量。从 T 到 IEnumerable<T> 的映射保持赋值兼容性；可以将 IEnumerable<string> 赋给 IEnumerable<object> 类型的变量。因此，“该类型参数是协变的”这一命名是一种简写；实际上协变的是类型实参与构造类型之间的关系。准确地说，我们应当说：“从——任意引用类型 T 到 IEnumerable<T> 的映射在 T 上是协变的”，但相比简单地说“T 是协变的”并理解较长的陈述才是其含义，这种说法相当拗口。

在示例中

```
interface <out X, in Y, Z>
{
    X M(Y y);
    Z P { get; set; }
}
```

X 是协变的，Y 是逆变的，Z 是不变的。

## 13. 接口

### 13.1.3.1 *变体安全性*

类型的类型参数列表中出现变体注解会限制类型可在类型声明中出现的位置。

如果下列任一条件成立，则类型 T 是*输出不安全*的：

- T 是逆变类型参数。
- T 是元素类型为输出不安全的数组类型。
- T 是由泛型类型 S<X₁, ..., Xₖ> 构造的接口或委托类型 S<A₁, ..., Aₖ>，其中对于至少一个 Aᵢ，下列条件之一成立：
  - Xᵢ 是协变或不变的，并且 Aᵢ 是输出不安全的。
  - Xᵢ 是逆变或不变的，并且 Aᵢ 是输入安全的。

如果下列任一条件成立，则类型 T 是*输入不安全*的：

- T 是协变类型参数。
- T 是元素类型为输入不安全的数组类型。
- T 是由泛型类型 S<X₁, ..., Xₖ> 构造的接口或委托类型 S<A₁, ..., Aₖ>，其中对于至少一个 Aᵢ，下列条件之一成立：
  - Xᵢ 是协变或不变的，并且 Aᵢ 是输入不安全的。
  - Xᵢ 是逆变或不变的，并且 Aᵢ 是输出不安全的。

直观地说，输出不安全类型禁止出现在输出位置，输入不安全类型禁止出现在输入位置。

如果类型不是输出不安全的，则它是*输出安全*的；如果类型不是输入不安全的，则它是*输入安全*的。

### 13.1.3.2 *变体转换*

变体注解的目的是允许更宽松（但仍类型安全）地转换为接口和委托类型。为此，隐式转换（§6.1）和显式转换（§6.2）的定义使用了变体可转换性的概念，其定义如下：

如果 T 是接口或委托类型，且以变体类型参数 T<X₁, ..., Xₙ> 声明，并且对于每个变体类型参数 Xᵢ，下列条件之一成立，则类型 T<A₁, ..., Aₙ> 可变体转换为类型 T<B₁, ..., Bₙ>：

- Xᵢ 是协变的，并且存在从 Aᵢ 到 Bᵢ 的隐式引用转换或标识转换。
- Xᵢ 是逆变的，并且存在从 Bᵢ 到 Aᵢ 的隐式引用转换或标识转换。
- Xᵢ 是不变的，并且存在从 Aᵢ 到 Bᵢ 的标识转换。

> **JON SKEET** 我怀疑许多开发者永远不需要声明自己的变体接口或委托。事实上，我猜想很多时候我们甚至不会注意到自己正在*使用*变体——它只是意味着，我们凭直觉期望能正常工作的代码现在可以正常工作了，尽管这些代码在 C# 3.0 中会编译失败。

### 13.1.4 基接口

接口可以从零个或多个接口类型继承，这些接口类型称为该接口的*显式基接口*。当接口有一个或多个显式基接口时，在该接口的声明中，接口标识符后跟一个冒号和一个以逗号分隔的基接口类型列表。

```
interface-base:
    : interface-type-list
```

对于构造接口类型，其显式基接口是这样形成的：取泛型类型声明上的显式基接口声明，并对基接口声明中的每个*类型参数*替换为构造类型的相应*类型实参*。

接口的显式基接口的可访问性必须至少与接口本身相同（§3.5.4）。例如，在*公共*接口的*接口基*中指定*私有*或*内部*接口是编译时错误。

接口直接或间接继承自身是编译时错误。

> **VLADIMIR RESHETNIKOV** 就本规则而言，类型实参（如果有）会被忽略。例如，尽管 `I<T>` 和 `I<I<T>>` 是不同类型，以下声明仍然无效：
> 
> ```csharp
> interface I<T> : I<I<T>> { }
> ```
> 
> 反过来，接口出现在其基接口的类型实参中是完全有效的：
> 
> ```csharp
> interface IA<T> { }
> interface IB : IA<I[]> { }  // Okay
> ```

接口的*基接口*是显式基接口及其基接口。换句话说，基接口集合是显式基接口、它们的显式基接口等等的完整传递闭包。接口继承其基接口的所有成员。在示例中

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

interface IComboBox : ITextBox, IListBox { }
```

IComboBox 的基接口是 IControl、ITextBox 和 IListBox。

换句话说，上面的 IComboBox 接口继承了成员 SetText 和 SetItems 以及 Paint。

接口的每个基接口都必须是输出安全的（§13.1.3.1）。实现接口的类或结构体也隐式实现该接口的所有基接口。

> **ERIC LIPPERT**  “继承”对于接口来说是一个不幸的用词选择。人们通常认为从基类继承意味着共享实现，而接口显然不这样做。我更愿意把接口看作契约，它可以指定还必须履行的其他契约，而不是看作“继承”其他契约的契约。

> **JESSE LIBERTY**  已经形成了一种命名约定：在所有接口前加上字母“I”（IControl、IWriteable、IClaudius）。这样做并没有令人信服的理由，但它作为“匈牙利”表示法的最后残余已经持续了至少十年。最终，去掉“I”会让代码更具可读性。

### 13.1.5 接口体

接口的接口体定义接口的成员。

```
interface-body:
{ interface-member-declarations_opt }
```

### 13.2 接口成员

接口的成员是从基接口继承的成员以及接口本身声明的成员。

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

接口声明可以声明零个或多个成员。接口的成员必须是方法、属性、事件或索引器。接口不能包含常量、字段、运算符、实例构造函数、析构函数或类型，接口也不能包含任何类型的静态成员。

所有接口成员都隐式具有公共访问权限。接口成员声明包含任何修饰符都是编译时错误。特别地，接口成员不能使用 abstract、public、protected、internal、private、virtual、override 或 static 修饰符声明。

> **JON SKEET** 偶尔如果能创建带有内部成员的内部接口，并且这些成员可以由内部方法隐式实现，那会很好。目前，内部接口迫使实现类型要么公开公共方法，要么使用显式接口实现；在某些情况下，这两种选择都不特别令人愉快。

示例

```
public delegate void StringListEvent(IStringList sender);

public interface IStringList
{
    void Add(string s);
    int Count { get; }
    event StringListEvent Changed;
    string this[int index] { get; set; }
}
```

声明了一个接口，其中包含每种可能成员类型各一个：一个方法、一个属性、一个事件和一个索引器。




一个 *接口声明* 创建一个新的声明空间 (§3.3)，并且由该 *接口声明* 直接包含的 *接口成员声明* 在此声明空间中引入新的成员。以下规则适用于 *接口成员声明*：

- 方法的名称必须与同一接口中声明的所有属性和事件的名称不同。此外，方法的签名 (§3.6) 必须与同一接口中声明的所有其他方法的签名不同，并且同一接口中声明的两个方法不能仅因 *ref* 和 *out* 而签名不同。
- 属性或事件的名称必须与同一接口中声明的所有其他成员的名称不同。
- 索引器的签名必须与同一接口中声明的所有其他索引器的签名不同。

接口的继承成员明确不属于该接口的声明空间。因此，接口允许声明一个与继承成员具有相同名称或签名的成员。当这种情况发生时，派生的接口成员被称为 *隐藏* 基接口成员。隐藏继承成员不被视为错误，但会导致编译器发出警告。为了抑制警告，派生接口成员的声明必须包含 new 修饰符，以指示派生成员旨在隐藏基成员。此主题在 §3.7.1.2 中进一步讨论。

如果在未隐藏继承成员的声明中包含 new 修饰符，则会发出相应警告。通过移除 new 修饰符可以抑制此警告。

请注意，class object 中的成员严格来说不是任何接口的成员 (§13.2)。然而，class object 中的成员可通过任何接口类型的成员查找 (§7.4) 获得。

## 13.2.1 接口方法

接口方法使用 *接口方法声明* 声明：

```
interface-method-declaration:
    attributes_opt new_opt return-type identifier type-parameter-list
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;
```

接口方法声明的 *属性*、*返回类型*、*标识符* 和 *形式参数列表* 与类 (§10.6) 中的方法声明具有相同的含义。接口方法声明不允许指定方法体，因此声明始终以分号结束。

> VLADIMIR RESHETNIKOV 与类或结构体方法声明不同，接口方法声明的标识符可以与包含它的接口声明的名称相同。接口属性声明和接口事件声明也是如此。

接口方法的每个形式参数类型必须是 input-safe (§13.1.3.1)，并且返回类型必须是 void 或 output-safe。此外，方法中任何类型参数上的每个类类型约束、接口类型约束和类型参数约束都必须是 input-safe。

这些规则确保接口的任何协变或逆变使用仍然是类型安全的。例如，

```
interface I<out T> { void M<U>() where U : T; }
```

是非法的，因为 T 作为 U 的类型参数约束的使用不是 input-safe。

如果没有此限制，就可能以以下方式违反类型安全：

```
class B {}
class D : B {}
class E : B {}
class C : I<D> { public void M<U>() {...} }
...
I<B> b = new C();
b.M<E>();
```

这实际上是对 C.M<E> 的调用。该调用要求 E 派生自 D，然而，这样就会在这里违反类型安全。

## 13.2.2 接口属性

接口属性使用 接口属性声明 声明：

```
interface-property-declaration:
    attributes_opt new_opt type identifier { interface-accessors }

interface-accessors:
    attributes_opt get ;
    attributes_opt set ;
    attributes_opt get ; attributes_opt set ;
    attributes_opt set ; attributes_opt get ;
```

接口属性声明的 属性、类型 和 标识符 与类 (§10.7) 中的属性声明具有相同的含义。

接口属性声明的访问器对应于类属性声明 (§10.7.2) 的访问器，只是访问器体必须始终为分号。因此，访问器仅指示属性是读写、只读还是只写。

如果存在 get 访问器，则接口属性的类型必须是 output-safe；如果存在 set 访问器，则必须是 input-safe。

## 13.2.3 接口事件

接口事件使用 *接口事件声明* 声明：

```
interface-event-declaration:
    attributes_opt new_opt event type identifier ;
```

接口事件声明的 *属性*、*类型* 和 *标识符* 与类 (§10.8) 中的事件声明具有相同的含义。

接口事件的类型必须是 input-safe。

## 13.2.4 接口索引器

接口索引器使用 *接口索引器声明* 声明：

```
interface-indexer-declaration:
    attributes_opt new_opt type this [ formal-parameter-list ] { interface-accessors }
```

接口索引器声明的 *属性*、*类型* 和 *形式参数列表* 与类 (§10.9) 中的索引器声明具有相同的含义。

接口索引器声明的访问器对应于类索引器声明 (§10.9) 的访问器，只是访问器体必须始终为分号。因此，访问器仅指示索引器是读写、只读还是只写。

接口索引器的所有形式参数类型必须是 input-safe。此外，任何 out 或 ref 形式参数类型也必须是 output-safe。请注意，即使是 out 参数也要求是 input-safe，这是由于底层执行平台的限制。

如果存在 get 访问器，则接口索引器的类型必须是 output-safe；如果存在 set 访问器，则必须是 input-safe。

## 13.2.5 接口成员访问

接口成员通过成员访问 (§7.6.4) 和索引器访问 (§7.6.6.2) 表达式访问，形式为 I.M 和 I[A]，其中 I 是接口类型；M 是该接口类型的方法、属性或事件；A 是索引器参数列表。

对于严格单继承的接口（继承链中的每个接口恰好有零个或一个直接基接口），成员查找 (§7.4)、方法调用 (§7.6.5.1) 和索引器访问 (§7.6.6.2) 规则的效果与类和结构体完全相同：更派生的成员会隐藏具有相同名称或签名的更低派生成员。然而，对于多继承接口，当两个或多个不相关的基接口声明具有相同名称或签名的成员时，可能会出现歧义。本节展示了此类情况的几个示例。在所有情况下，都可以使用显式转换来解决歧义。

在示例

```
interface IList
{
    int Count { get; set; }
}
interface ICounter
{
    void Count(int i);
}
interface IListCounter : IList, ICounter { }
class C
{
    void Test(IListCounter x)
    {
        x.Count(1);          // Error
        x.Count = 1;         // Error
        ((IList)x).Count = 1; // Okay: invokes IList.Count_set
        ((ICounter)x).Count(1); // Okay: invokes ICounter.Count
    }
}
```

前两个语句导致编译时错误，因为在 IListCounter 中 Count 的成员查找 (§7.4) 是不明确的。如示例所示，通过将 x 转换为适当的基接口类型可以解决歧义。此类转换没有运行时成本——它们仅在编译时将实例视为更低派生类型。

在示例

```
interface IInteger
{
    void Add(int i);
}
interface IDouble
{
    void Add(double d);
}
interface INumber : IInteger, IDouble { }
```

```
class C
{
    void Test(INumber n)
    {
        n.Add(1);                // Invokes IInteger.Add
        n.Add(1.0);              // Only IDouble.Add is applicable
        ((IInteger)n).Add(1);    // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);     // Only IDouble.Add is a candidate
    }
}
```

调用 n.Add(1) 通过应用 §7.5.3 的重载解析规则选择 IInteger.Add。类似地，调用 n.Add(1.0) 选择 IDouble.Add。当插入显式转换时，只有一个候选方法，因此没有歧义。

在示例

```
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
        d.F(1);                  // Invokes ILeft.F
        ((IBase)d).F(1);         // Invokes IBase.F
        ((ILeft)d).F(1);         // Invokes ILeft.F
        ((IRight)d).F(1);        // Invokes IBase.F
    }
}
```

IBase.F 成员被 ILeft.F 成员隐藏。因此，调用 d.F(1) 选择 ILeft.F，即使 IBase.F 在通过 IRight 的访问路径中似乎未被隐藏。

多继承接口中隐藏的直观规则很简单：如果一个成员在任何访问路径中被隐藏，则它在所有访问路径中都被隐藏。因为从 IDerived 到 ILeft 再到 IBase 的访问路径隐藏了 IBase.F，所以该成员在从 IDerived 到 IRight 再到 IBase 的访问路径中也被隐藏。




## 13.3 完全限定的接口成员名称

接口成员有时会被其完全限定名称引用。接口成员的完全限定名称由声明该成员的接口的名称组成，其后跟一个点，再跟成员的名称。成员的完全限定名称引用了声明该成员的接口。例如，给定以下声明

```
interface IControl
{
    void Paint();
}
interface ITextBox : IControl
{
    void SetText(string text);
}
```

Paint 的完全限定名称是 IControl.Paint，而 SetText 的完全限定名称是 ITextBox.SetText。

在上面的示例中，不可能将 Paint 称为 ITextBox.Paint。

当接口属于命名空间的一部分时，接口成员的完全限定名称包含命名空间名称。例如：

```
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

在这里，Clone 方法的完全限定名称是 System.ICloneable.Clone。

## 13.4 接口实现

接口可以由类和结构体实现。为了表示类或结构体直接实现接口，接口标识符包含在该类或结构体的基类列表中。例如：

```
interface ICloneable
{
    object Clone();
}
```

```
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

> > **JON SKEET** 这让我困扰的是接口实现通常是完全隐式的。没有任何迹象表明 CompareTo 和 Clone 方法与它们所提供实现的接口有关。当重写从基类继承的虚方法时，override 修饰符使这种行为变得明显：任何重构类并想要重命名方法的人都会被告知它与别处的方法相关联。对于接口则没有这样的指示。
> >
> > 不幸的是，接口实现的設計与在声明中添加修饰符并不完全一致。声明方法的代码甚至不一定知道它可能被用来实现接口：
> >
> >     interface IFoo { void Foo(); }
> >     class Base
> >     {
> >         public void Foo();
> >     }
> >     // IFoo.Foo is implemented by Base.Foo
> >     class Derived : Base, IFoo { }
> >
> > 这可能是处理接口最务实的方法，但从纯粹性（或控制狂）的角度来看，它感觉有点不对。

直接实现接口的类或结构体也隐式地直接实现了该接口的所有基接口。这即使类或结构体没有在基类列表中显式列出所有基接口也是如此。例如：

```
    interface IControl
    {
        void Paint();
    }

    interface ITextBox : IControl
    {
        void SetText(string text);
    }
```

```
class TextBox : ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

在这里，类 TextBox 同时实现了 IControl 和 ITextBox。

当类 C 直接实现接口时，从 C 派生的所有类也隐式地实现了该接口。在类声明中指定的基接口可以是构造的接口类型（§4.4）。基接口本身不能是类型参数，尽管它可以涉及作用域中的类型参数。以下代码说明了类如何实现和扩展构造类型：

```
class C<U, V> { }
interface II<T> { }
class D : C<string, int>, II<string> { }
class E<T> : C<int, T>, II<T> { }
```

泛型类声明的基接口必须满足 §13.4.2 中描述的唯一性规则。

### 13.4.1 显式接口成员实现

为了实现接口的目的，类或结构体可以声明显式接口成员实现。显式接口成员实现是对引用完全限定接口成员名称的方法、属性、事件或索引器声明。例如：

```
interface IList<T>
{
    T[] GetElements();
}
interface IDictionary<K,V>
{
    V this[K key];
    void Add(K key, V value);
}
class List<T> : IList<T>, IDictionary<int,T>
{
    T[] IList<T>.GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

这里 `IDictionary<int,T>.this` 和 `IDictionary<int,T>.Add` 是显式接口成员实现。

在某些情况下，接口成员的名称可能不适合实现类，在这种情况下，接口成员可以使用显式接口成员实现来实现。例如，实现文件抽象的类很可能会实现一个 `Close` 成员函数，其效果是释放文件资源，并使用显式接口成员实现来实现 `IDisposable` 接口的 `Dispose` 方法：

```csharp
interface IDisposable
{
    void Dispose();
}

class MyFile : IDisposable
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

不可能通过其完全限定名称在方法调用、属性访问或索引器访问中访问显式接口成员实现。显式接口成员实现只能通过接口实例访问，在这种情况下仅通过其成员名称引用。

显式接口成员实现包含访问修饰符是编译时错误，并且包含修饰符 `abstract`、`virtual`、`override` 或 `static` 也是编译时错误。

显式接口成员实现与其他成员具有不同的可访问性特征。因为显式接口成员实现永远无法通过其完全限定名称在方法调用或属性访问中访问，所以在某种意义上它们是私有的。然而，因为它们可以通过接口实例访问，所以在某种意义上它们也是公共的。

> > **VLADIMIR RESHETNIKOV**  为了可访问性约束检查的目的（参见 §3.5.4），显式接口实现被视为私有。

显式接口成员实现主要有两个目的：

- 因为显式接口成员实现无法通过类或结构体实例访问，所以它们允许接口实现被排除在类或结构体的公共接口之外。当类或结构体实现对该类或结构体的使用者而言不感兴趣的内部接口时，这尤其有用。
- 显式接口成员实现允许对具有相同签名的接口成员进行消歧。没有显式接口成员实现，类或结构体就不可能对具有相同签名和返回类型的接口成员具有不同的实现，也就不可能对具有相同签名但返回类型不同的接口成员有任何实现。

> > **JON SKEET** 这个第二种情况的某种规范示例是 `IEnumerable<T>`，它扩展了 `IEnumerable` 的契约。这意味着实现必须提供两个方法：
> >
> > ```
> > IEnumerator GetEnumerator()
> > IEnumerator<T> GetEnumerator()
> > ```
> >
> > 这通常通过显式实现非泛型的 `IEnumerable.GetEnumerator()` 来调用泛型版本——这之所以可行，是因为 `IEnumerator<T>` 和 `IEnumerator` 具有相同类型的关系。

要使显式接口成员实现有效，类或结构体必须在其基类列表中命名一个接口，该接口包含一个成员，其完全限定名称、类型和参数类型与显式接口成员实现完全匹配。因此，在以下类中

```
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...} // Invalid
}
```

IComparable.CompareTo 的声明导致编译时错误，因为 IComparable 没有列在 Shape 的基类列表中，也不是 ICloneable 的基接口。同样，在以下声明中

```
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
}
```



```
class Ellipse: Shape
{
    object ICloneable.Clone() {...}    // Invalid
}
```

Ellipse 中 ICloneable.Clone 的声明会导致编译时错误，因为 ICloneable 未显式列在 Ellipse 的基类列表中。

接口成员的完全限定名必须引用声明该成员的接口。因此，在以下声明中：

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

Paint 的显式接口成员实现必须写成 IControl.Paint。

## 13.4.2 所实现接口的唯一性

泛型类型声明所实现的接口对于所有可能的构造类型必须保持唯一。如果没有此规则，对于某些构造类型将无法确定应调用哪个正确方法。例如，假设允许将泛型类声明写成如下形式：

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

如果允许这样做，在以下情况中将无法确定执行哪段代码：

```csharp
I<int> x = new X<int,int>();
x.F();
```

为确定泛型类型声明的接口列表是否有效，需执行以下步骤：

- 令 L 为泛型类、结构或接口声明 C 中直接指定的接口列表。
- 将 L 中已有接口的任何基接口添加到 L。
- 从 L 中移除任何重复项。
- 如果由 C 创建的任何可能构造类型在将类型实参替换到 L 后，会导致 L 中的两个接口相同，则 C 的声明无效。在确定所有可能的构造类型时不考虑约束声明。

在上述类声明 X 中，接口列表 L 由 I<U> 和 I<V> 组成。该声明无效，因为任何将 U 和 V 设为同一类型的构造类型都会使这两个接口成为相同类型。

在不同继承层次指定的接口可以统一：

```csharp
interface I<T>
{
    void F();
}
class Base<U>: I<U>
{
    void I<U>.F() {...}
}
class Derived<U,V>: Base<U>, I<V>    // Okay
{
    void I<V>.F() {...}
}
```

即使 Derived<U,V> 同时实现 I<U> 和 I<V>，此代码仍然有效。以下代码：

```csharp
I<int> x = new Derived<int,int>();
x.F();
```

调用 Derived 中的方法，因为 Derived<int,int> 有效地重新实现了 I<int>（§13.4.6）。

> **ERIC LIPPERT** 尽管创建这样的类是不合法的：两个接口在构造后可能变得相同，但在 C# 4.0 中，由于泛型协变和逆变，可以以各种更微妙的方式创建有歧义的类。例如，设想一个实现 IEnumerable<object> 的基类和一个实现 IEnumerable<string> 的派生类。在 C# 3.0 中这些是不兼容类型，但情况已不再如此。因为 IEnumerable<string> 现在可转换为 IEnumerable<object>，所以在派生类上调用 IEnumerable<object> 的方法时，究竟会调用哪个实现并不完全清楚。这类奇异场景往往会暴露运行时的实现定义行为，应尽可能避免。

## 13.4.3 泛型方法的实现

当泛型方法隐式实现接口方法时，两个声明中为每个方法类型参数给定的约束必须等价（在将任何接口类型参数替换为相应类型实参之后），其中方法类型参数按从左到右的序号位置标识。

然而，当泛型方法显式实现接口方法时，实现方法上不允许有约束。约束改为从接口方法继承：

```
interface IX<A, B, C>
{
    void F<T>(T t) where T : A;
    void G<T>(T t) where T : B;
    void H<T>(T t) where T : C;
}

class C : IX<object, C, string>
{
    public void F<T>(T t) {...}          // Okay
    public void G<T>(T t) where T : C {...}   // Okay
    public void H<T>(T t) where T : string {...} // Error
}
```

方法 C.F<T> 隐式实现 IX<object,C,string>.F<T>。在此情况下，C.F<T> 不需要（也不允许）指定约束 T: object，因为 object 是所有类型参数的隐式约束。方法 C.G<T> 隐式实现 IX<object,C,string>.G<T>，因为在将接口类型参数替换为对应类型实参后，其约束与接口中的约束匹配。方法 C.H<T> 的约束是错误的，因为密封类型（此处为 string）不能用作约束。省略该约束也会出错，因为隐式接口方法实现的约束必须匹配。因此，无法隐式实现 IX<object,C,string>.H<T>。此接口方法只能使用显式接口成员实现来实现：

```
class C: IX<object,C,string>
{
    ...
    public void H<U>(U u) where U: class {...}
    void IX<object,C,string>.H<T>(T t) {
        string s = t;    // Okay
        H<T>(t);
    }
}
```

在此示例中，显式接口成员实现调用一个约束严格更弱的公共方法。注意，从 t 到 s 的赋值有效，因为 T 继承了 T: string 的约束，尽管该约束无法在源代码中表达。

## 13.4.4 接口映射

类或结构必须为类或结构的基类列表中列出的接口的所有成员提供实现。在实现类或结构中定位接口成员实现的过程称为接口映射。

对于类或结构 C 的接口映射，会为 C 的基类列表中指定的每个接口的每个成员定位一个实现。特定接口成员 I.M（其中 I 是声明成员 M 的接口）的实现，通过检查每个类或结构 S 来确定，从 C 开始，并对 C 的每个后续基类重复此过程，直到找到匹配项：

- 如果 S 包含与 I 和 M 匹配的显式接口成员实现的声明，则该成员是 I.M 的实现。
- 否则，如果 S 包含与 M 匹配的非静态公共成员的声明，则该成员是 I.M 的实现。如果匹配的成员不止一个，则未指定哪个成员是 I.M 的实现。这种情况仅在 S 是构造类型时发生，此时泛型类型中声明的两个成员具有不同签名，但类型实参使它们的签名相同。

如果无法为 C 的基类列表中指定的所有接口的所有成员定位实现，则发生编译时错误。注意，接口的成员包括从基接口继承的成员。

就接口映射而言，当以下情况成立时，类成员 A 与接口成员 B 匹配：

- A 和 B 是方法，并且 A 和 B 的名称、类型和形参列表完全相同。
- A 和 B 是属性，A 和 B 的名称和类型完全相同，并且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外访问器）。
- A 和 B 是事件，并且 A 和 B 的名称和类型完全相同。
- A 和 B 是索引器，A 和 B 的类型和形参列表完全相同，并且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外访问器）。

接口映射算法的显著推论如下：

- 在确定实现接口成员的类或结构成员时，显式接口成员实现优先于同一类或结构中的其他成员。
- 非公共成员和静态成员均不参与接口映射。

在以下示例中：

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

C 的 ICloneable.Clone 成员成为 ICloneable 中 Clone 的实现，因为显式接口成员实现优先于其他成员。

如果类或结构实现两个或更多接口，而这些接口包含具有相同名称、类型和参数类型的成员，则可以将这些接口成员中的每一个映射到单个类或结构成员。例如：

```
interface IControl
{
    void Paint();
}
```




```csharp
interface IForm
{
    void Paint();
}
class Page : IControl, IForm
{
    public void Paint() {...}
}
```

这里，IControl 和 IForm 的 Paint 方法都映射到 Page 中的 Paint 方法。当然，也可以为这两个方法分别提供单独的显式接口成员实现。

如果一个类或结构体实现了一个包含隐藏成员的接口，那么某些成员必须通过显式接口成员实现来实现。例如：

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

此接口的实现将至少需要一个显式接口成员实现，并采用以下形式之一：

```csharp
class C : IDerived
{
    int IBase.P { get {...} }
    int IDerived.P() {...}
}
class C : IDerived
{
    public int P { get {...} }
    int IDerived.P() {...}
}
class C : IDerived
{
    int IBase.P { get {...} }
    public int P() {...}
}
```

当一个类实现多个具有相同基接口的接口时，基接口只能有一个实现。在下面的示例中

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
    void IListBox.SetItems(string[] items) {...}
}
```

不可能为基类列表中命名的 IControl、由 ITextBox 继承的 IControl 以及由 IListBox 继承的 IControl 分别提供实现。事实上，这些接口没有单独身份的概念。相反，ITextBox 和 IListBox 的实现共享同一个 IControl 实现，而 ComboBox 只是被视为实现了三个接口：IControl、ITextBox 和 IListBox。

基类的成员参与接口映射。在下面的示例中

```csharp
interface Interface1
{
    void F();
}

class Class1
{
    public void F() { }
    public void G() { }
}

class Class2 : Class1, Interface1
{
    new public void G() { }
}
```

Class1 中的方法 F 用于 Class2 对 Interface1 的实现。

## 13.4.5 接口实现继承

> **比尔·瓦格纳** 埃里克早先关于“继承”是一个不幸用词的评论，在本节中更加正确。接口方法的行为不同于基类中声明的虚方法或非虚方法。当层次结构中的多个类声明对接口的实现时，要准确理解哪个方法是最佳选择可能需要一些时间。在阅读本节时，你会看到许多不同的规则，用于在某个方法于接口中定义时选择最佳方法。

如果不显式地*重新实现*接口，派生类无论如何都不能更改它从基类继承的接口映射。例如，在下面的声明中

```csharp
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
    new public void Paint() {...}
}
```

TextBox 中的 Paint 方法隐藏了 Control 中的 Paint 方法，但它不会更改 Control.Paint 到 IControl.Paint 的映射，并且通过类实例和接口实例对 Paint 的调用将具有以下效果：

```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();            // Invokes Control.Paint();
t.Paint();            // Invokes TextBox.Paint();
ic.Paint();           // Invokes Control.Paint();
it.Paint();           // Invokes Control.Paint();
```

然而，当接口方法映射到类中的虚方法时，派生类可以重写该虚方法并更改接口的实现。例如，将上面的声明改写为

```csharp
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

现在将观察到以下效果：

```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();          // Invokes Control.Paint();
t.Paint();          // Invokes TextBox.Paint();
ic.Paint();         // Invokes Control.Paint();
it.Paint();         // Invokes TextBox.Paint();
```

由于显式接口成员实现不能声明为虚方法，因此无法重写显式接口成员实现。但是，显式接口成员实现调用另一个方法是完全合法的，并且该另一个方法可以声明为虚方法，以便派生类重写它。例如：

```csharp
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

这里，从 Control 派生的类可以通过重写 PaintControl 方法来定制 IControl.Paint 的实现。

## 13.4.6 接口重新实现

继承接口实现的类可以通过将接口包含在基类列表中来重新实现该接口。

接口的重新实现遵循与接口初始实现完全相同的接口映射规则。因此，继承的接口映射对为接口重新实现所建立的接口映射没有任何影响。

例如，在下面的声明中

```csharp
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

Control 将 IControl.Paint 映射到 Control.IControl.Paint 这一事实不会影响 MyControl 中的重新实现，后者将 IControl.Paint 映射到 MyControl.Paint。

继承的公共成员声明和继承的显式接口成员声明参与重新实现的接口的接口映射过程。例如：

```csharp
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
```

```csharp
class Derived: Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

这里，Derived 中 IMethods 的实现将接口方法映射到 Derived.F、Base.IMethods.G、Derived.IMethods.H 和 Base.I。

当一个类实现一个接口时，它隐式地也实现该接口的所有基接口。同样，接口的重新实现也隐式地是该接口所有基接口的重新实现。例如：

```csharp
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

这里，IDerived 的重新实现也重新实现了 IBase，将 IBase.F 映射到 D.F。

> **乔恩·斯基特** 虽然这类做法在某些场合确实有用，但通常应避免，因为它是巨大混乱的根源。通常，对同一对象使用相同方法名和相同参数列表的每次调用都应导致调用同一个方法。偏离这种理想情况的方式有很多，所有这些方式都应极其谨慎地使用，并且仅在绝对必要时使用。

## 13.4.7 抽象类和接口

与非抽象类一样，抽象类必须为类的基类列表中列出的接口的所有成员提供实现。但是，允许抽象类将接口方法映射到抽象方法。例如：

```csharp
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

这里，IMethods 的实现将 F 和 G 映射到抽象方法，这些抽象方法必须在从 C 派生的非抽象类中重写。

请注意，显式接口成员实现不能是抽象的，但显式接口成员实现当然可以调用抽象方法。例如：

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

这里，从 C 派生的非抽象类将被要求重写 FF 和 GG，从而提供 IMethods 的实际实现。




此页面有意留空

## 14. 枚举

枚举类型是一种独特的值类型（§4.1），它声明了一组命名常量。

> JON SKEET（乔恩·斯基特） 值得注意的是，这些“命名常量”实际上只是数字。它们无法表达行为，这与C#中几乎其他所有内容都不同。这是Java比C#更具表现力的极少数领域之一。在Java中，枚举功能强大得多：例如，枚举可以声明方法，然后为特定值重写这些方法。虽然在C#中可以模拟Java枚举的部分功能，但在未来版本中提供语言（和框架）支持将是非常受欢迎的。

以下示例

```
enum Color
{
    Red,
    Green,
    Blue
}
```

声明了一个名为 Color 的枚举类型，其成员为 Red、Green 和 Blue。

### 14.1 枚举声明

枚举声明用于声明新的枚举类型。枚举声明以关键字 enum 开头，并定义枚举的名称、可访问性、基础类型和成员。

```
enum-declaration:
    attributes_opt enum-modifiers_opt enum identifier enum-base_opt enum-body ;_opt

enum-base:
    : integral-type

enum-body:
    { enum-member-declarations_opt }
    { enum-member-declarations , }
```

每个枚举类型都有一个对应的整型类型，称为该枚举类型的基础类型。此基础类型必须能够表示枚举中定义的所有枚举值。枚举声明可以显式声明 byte、sbyte、short、ushort、int、uint、long 或 ulong 作为基础类型。注意，char 不能用作基础类型。未显式声明基础类型的枚举声明默认具有 int 基础类型。

> JON SKEET（乔恩·斯基特） 这是该语言中为数不多的、不能用类型全称等效形式替换其“简写”形式的地方之一。例如，不能按如下方式声明 Color 枚举：
> 
>     enum Color: System.Int64 { ... }

以下示例

```
enum Color : long
{
    Red,
    Green,
    Blue
}
```

声明了一个基础类型为 long 的枚举。开发人员可能会选择使用 long 作为基础类型，如示例所示，以便能够使用 long 范围内但不在 int 范围内的值，或为将来保留此选项。

### 14.2 枚举修饰符

枚举声明可以可选地包含一系列枚举修饰符：

```
enum-modifiers:
    enum-modifier
    enum-modifiers enum-modifier

enum-modifier:
    new
    public
    protected
    internal
    private
```

在枚举声明中，同一修饰符多次出现是编译时错误。

枚举声明的修饰符与类声明（§10.1.1）的修饰符含义相同。但请注意，abstract 和 sealed 修饰符不允许出现在枚举声明中。枚举不能是抽象的，也不允许派生。

### 14.3 枚举成员

枚举类型声明的主体定义了零个或多个枚举成员，这些成员是枚举类型的命名常量。任意两个枚举成员不能具有相同的名称。

```
enum-member-declarations:
    enum-member-declaration
    enum-member-declarations , enum-member-declaration

enum-member-declaration:
    attributes_opt identifier
    attributes_opt identifier = constant-expression
```

> > **VLADIMIR RESHETNIKOV（弗拉基米尔·雷舍特尼科夫）** 在微软的C#实现中，枚举成员不能命名为 value__，因为该名称保留用于枚举的内部表示。

每个枚举成员都有一个关联的常量值。该值的类型是所属枚举的基础类型。每个枚举成员的常量值必须在该枚举基础类型的范围内。以下示例

```
enum Color : uint
{
    Red = -1,
    Green = -2,
    Blue = -3
}
```

会导致编译时错误，因为常量值 -1、-2 和 -3 不在基础整型类型 uint 的范围内。

多个枚举成员可以共享相同的关联值。以下示例

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

枚举成员的关联值通过隐式或显式方式赋值。如果枚举成员的声明具有常量表达式初始值设定项，则该常量表达式的值（隐式转换为枚举的基础类型）即为枚举成员的关联值。如果枚举成员的声明没有初始值设定项，则其关联值按如下方式隐式设置：

- 如果该枚举成员是枚举类型中声明的第一个枚举成员，则其关联值为 0。
- 否则，该枚举成员的关联值通过将文本上位于其前面的枚举成员的关联值加 1 来获得。此增加后的值必须位于基础类型可以表示的值范围内；否则，将发生编译时错误。

> JON SKEET（乔恩·斯基特） 对于 [Flags] 枚举，使用默认值几乎总是错误的选择，因为其值通常应为 1、2、4、8 等——通常还有一个“None”值对应 0。语言本可以帮助开发人员避免意外使用不恰当的值，但很难判断在不增加超出合理范围的复杂度的前提下，这一目标能在多大程度上实现。

> BILL WAGNER（比尔·瓦格纳） 我更希望看到以下示例使用扩展方法实现。“Color.Red.StringFromColor()” 对我而言比 “StringFromColor(Color.Red)” 读起来更好。
> 
> 该技术也开始回应乔恩关于无法表达行为的评论。

以下示例

```
using System;
enum Color
{
    Red,
    Green = 10,
    Blue
}
```

```
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
                return String.Format("Red = {0}", (int)c);
            case Color.Green:
                return String.Format("Green = {0}", (int)c);
            case Color.Blue:
                return String.Format("Blue = {0}", (int)c);
            default:
                return "Invalid color";
        }
    }
}
```

打印出枚举成员名称及其关联值。输出为

```
Red = 0
Green = 10
Blue = 11
```

原因如下：

- 枚举成员 Red 被自动分配值为零（因为它没有初始值设定项，并且是第一个枚举成员）。
- 枚举成员 Green 被显式赋予值 10。
- 枚举成员 Blue 被自动分配比其文本前一个成员大 1 的值。

枚举成员的关联值不能直接或间接使用该枚举成员自身的值。除了这种循环限制之外，枚举成员初始值设定项可以自由引用其他枚举成员的初始值设定项，无论它们的文本位置如何。在枚举成员初始值设定项内，其他枚举成员的值始终被视为其基础类型的值，因此在引用其他枚举成员时无需进行强制转换。

以下示例

```
enum Circular
{
    A = B,
    B
}
```

会导致编译时错误，因为 A 和 B 的声明是循环的。A 显式依赖于 B，而 B 隐式依赖于 A。

枚举成员的命名和作用域方式与类中的字段完全类似。枚举成员的作用域是其所在枚举类型的主体。在该作用域内，可以通过简单名称引用枚举成员。在所有其他代码中，枚举成员的名称必须以其枚举类型的名称进行限定。枚举成员没有声明的可访问性——如果枚举成员所在的枚举类型是可访问的，则该枚举成员是可访问的。

### 14.4 System.Enum 类型

System.Enum 类型是所有枚举类型的抽象基类（这与枚举类型的基础类型不同），从 System.Enum 继承的成员可在任何枚举类型中使用。存在从任何枚举类型到 System.Enum 的装箱转换（§4.3.1），以及从 System.Enum 到任何枚举类型的取消装箱转换（§4.3.2）。

请注意，System.Enum 本身不是枚举类型。相反，它是一个类类型，所有枚举类型都从中派生。System.Enum 类型继承自 System.ValueType 类型（§4.1.1），而 System.ValueType 又继承自 object 类型。在运行时，System.Enum 类型的值可以为 null，也可以是对任何枚举类型的装箱值的引用。

### 14.5 枚举值和运算

每个枚举类型都定义了一个独特的类型；在枚举类型和整型类型之间，或在两个枚举类型之间进行转换时，需要显式枚举转换（§6.2.2）。枚举类型可以取值的集合不仅限于其枚举成员。特别是，枚举基础类型的任何值都可以强制转换为该枚举类型，并且是该枚举类型的一个独特有效值。

枚举成员具有其所在枚举类型的类型（但在其他枚举成员初始值设定项中除外；请参阅 §14.3）。在枚举类型 E 中声明的关联值为 v 的枚举成员，其值为 (E)v。




以下运算符可用于枚举类型的值：==、!=、<、>、<=、>=（§7.10.5）、二元 +（§7.8.4）、二元 -（§7.8.5）、^、&、|（§7.11.2）、~（§7.7.4），以及 ++ 和 --（§7.6.9 和 §7.7.5）。

> JON SKEET 其中一些运算符仅对使用 [Flags] 装饰的枚举才真正有意义，但语言在任何方面都不强制执行这一限制。

每个枚举类型都自动派生自类 System.Enum（它本身又派生自 System.ValueType 和 object）。因此该类的继承方法与属性可用于枚举类型的值。

本页特意留空

## 15. 委托

委托实现了其他语言（如 C++、Pascal 和 Modula）使用函数指针来处理的场景。然而，与 C++ 函数指针不同，委托是完全面向对象的。此外，与 C++ 成员函数指针不同，委托同时封装了一个对象实例和方法。

> **BILL WAGNER** 在阅读语言规范中这一小章节时，我感到一种奇怪的惊讶。委托自 C# 1.0 发布以来就是 C# 的一部分。当时，大多数 C# 社区（包括我）将委托视为围绕事件的一点额外仪式。十年后，我无法想象没有委托的 C# 语言。它们是我们大多数人每天在 LINQ 查询、函数组合、闭包等中使用的东西。委托以及将代码视为数据的概念是现代 .NET 生态系统中如此重要的一部分，以至于我无法想象在不允许我将函数（和操作）作为数据表达的语言中编程。

委托声明定义了一个派生自类 System.Delegate 的类。委托实例封装了一个调用列表，即一个或多个方法列表，每个方法称为可调用实体。对于实例方法，可调用实体由一个实例及其上的方法组成。对于静态方法，可调用实体仅由一个方法组成。使用适当的一组参数调用委托实例会导致委托的每个可调用实体都使用给定的一组参数被调用。

委托实例的一个有趣且有用的属性是它不知道也不关心其封装的方法的类；唯一重要的是这些方法与委托的类型兼容（§15.1）。这使得委托非常适合“匿名”调用。

> ERIC LIPPERT 委托通常在开发者第一次遇到时相当令人困惑。我喜欢把委托类型看作类似于只有一个方法在其上的接口；委托类型的实例是一个实现此方法的对象。

### 15.1 委托声明

委托声明是类型声明（§9.6），它声明一个新的委托类型。

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

委托修饰符:
- new
- public
- protected
- internal
- private

在委托声明中，相同的修饰符出现多次是编译时错误。

new 修饰符仅允许在另一个类型内声明的委托上使用，在这种情况下它指定该委托隐藏了同名的继承成员，如 §10.3.4 所述。

public、protected、internal 和 private 修饰符控制委托类型的可访问性。根据委托声明出现的上下文，其中一些修饰符可能不被允许（§3.5.1）。

委托的类型名称是 identifier。

可选的 formal-parameter-list 指定委托的参数，return-type 指示委托的返回类型。

可选的 variant-type-parameter-list（§13.1.3）指定委托本身的类型参数。

委托类型的返回类型必须是 void 或 output-safe（§13.1.3.1）。

委托类型的所有形式参数类型必须是 input-safe。此外，任何 out 或 ref 参数类型必须是 output-safe。请注意，即使是 out 参数也要求是 input-safe，这是由于底层执行平台的限制。

> ERIC LIPPERT 这里提到的限制是 out 参数实际上在幕后被实现为 ref 参数：你可以同时读取和写入参数。编译器强制执行的规则是 out 参数必须在被读取前先写入，但这是 C# 语言的规则，而不是运行时的规则。如果 out 参数真正是“只写”的并且此限制由运行时强制执行，那么从理论上讲它们可以被设为协变的。下次你设计新的类型系统时请记住这一点。

C# 中的委托类型是名称等价的，而不是结构等价的。具体来说，具有相同参数列表和返回类型的两个不同委托类型被视为不同的委托类型。然而，两个不同但结构等价的委托类型的实例可能比较相等（§7.9.8）。

例如：

```csharp
delegate int D1(int i, double d);

class A
{
    public static int M1(int a, double b) {...}
}

class B
{
    delegate int D2(int c, double d);
    public static int M1(int f, double g) {...}
    public static void M2(int k, double l) {...}
    public static int M3(int g) {...}
    public static void M4(int g) {...}
}
```

委托类型 D1 和 D2 都与方法 A.M1 和 B.M1 兼容，因为它们具有相同的返回类型和参数列表；然而，这些委托类型是两种不同的类型，因此不可互换。委托类型 D1 和 D2 与方法 B.M2、B.M3 和 B.M4 不兼容，因为它们具有不同的返回类型或参数列表。

> **ERIC LIPPERT** 当你设计新的类型系统时，你不知道它将来会如何使用。可以想象未来涉及不同类别的委托的场景（例如“委托给具有可观察副作用的方法”或“委托给可以并发调用的方法”）。那么禁止这些类别之间的赋值是有意义的。实际上，正如事实证明的那样，委托的结构化类型非常有用；`Predicate<int>` 和 `Func<int, bool>` 之间实际上没有需要在运行时强制执行的语义差异。如果我们要重新来过，委托类型会比今天更结构兼容。

像其他泛型类型声明一样，必须给出类型参数才能创建构造的委托类型。构造的委托类型的参数类型和返回类型是通过为委托声明中的每个类型参数替换构造的委托类型的相应类型参数而创建的。由此产生的返回类型和参数类型用于确定哪些方法与构造的委托类型兼容。例如：

```
delegate bool Predicate<T>(T value);
class X
{
    static bool F(int i) {...}
    static bool G(string s) {...}
}
```

委托类型 Predicate<int> 与方法 X.F 兼容，委托类型 Predicate<string> 与方法 X.G 兼容。

声明委托类型的唯一方式是通过 delegate-declaration。委托类型是派生自 System.Delegate 的类类型。委托类型是隐式密封的，因此不允许从委托类型派生任何类型。也不允许从 System.Delegate 派生非委托类类型。请注意，System.Delegate 本身不是委托类型；它是所有委托类型派生的类类型。

C# 为委托实例化和调用提供了特殊语法。除了实例化之外，可以应用于类或类实例的任何操作也可以分别应用于委托类或实例。特别是，可以通过通常的成员访问语法访问 System.Delegate 类型的成员。



委托实例所封装的方法集合称为调用列表。当委托实例由单个方法创建（§15.2）时，它封装该方法，其调用列表只包含一个条目。然而，当两个非空委托实例组合时，它们的调用列表会连接起来——按左操作数在前、右操作数在后的顺序——形成一个新的调用列表，其中包含两个或更多条目。

> **乔恩·斯基特** 这种单播/多播的双重性在某些方面极其别扭——而在另一些方面又极其有用。例如，谈论单播委托的“目标”是合理的，而多播委托的调用列表中的每个条目可能具有各自独立的目标。这很少造成实际问题，但会让人难以既简单又准确地描述委托。

委托使用二元 + 运算符（§7.8.4）和 += 运算符（§7.17.2）进行组合。可以使用二元 - 运算符（§7.8.5）和 -= 运算符（§7.17.2）从委托组合中移除某个委托。还可以对委托进行相等性比较（§7.10.8）。

以下示例展示若干委托的实例化及其对应的调用列表：

```
delegate void D(int x);

class C
{
    public static void M1(int i) {...}
    public static void M2(int i) {...}
}

class Test
{
    static void Main()
    {
        D cd1 = new D(C.M1);     // M1
        D cd2 = new D(C.M2);     // M2
        D cd3 = cd1 + cd2;       // M1 + M2
        D cd4 = cd3 + cd1;       // M1 + M2 + M1
        D cd5 = cd4 + cd3;       // M1 + M2 + M1 + M1 + M2
    }
}
```

当 cd1 和 cd2 实例化时，它们各自封装一个方法。当 cd3 实例化时，它的调用列表按该顺序包含 M1 和 M2 两个方法。cd4 的调用列表按该顺序包含 M1、M2 和 M1。最后，cd5 的调用列表按该顺序包含 M1、M2、M1、M1 和 M2。有关组合（以及移除）委托的更多示例，请参见 §15.4。

### 15.2 委托兼容性

如果以下所有条件均为真，则方法或委托 M 与委托类型 D 兼容：

- D 和 M 具有相同数量的参数，并且 D 中的每个参数与 M 中的对应参数具有相同的 ref 或 out 修饰符。
- 对于每个值参数（不带 ref 或 out 修饰符的参数），存在从 D 中的参数类型到 M 中对应参数类型的恒等转换（§6.1.1）或隐式引用转换（§6.1.6）。
- 对于每个 ref 或 out 参数，D 中的参数类型与 M 中的参数类型相同。
- 存在从 M 的返回类型到 D 的返回类型的恒等转换或隐式引用转换。

### 15.3 委托实例化

委托实例通过委托创建表达式（§7.6.10.5）或到委托类型的转换来创建。新创建的委托实例随后引用以下之一：

- 委托创建表达式中引用的静态方法，或
- 委托创建表达式中引用的目标对象（不能为 null）和实例方法，或
- 另一个委托。

例如：

```
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public void M2(int i) {...}
}
class Test
{
    static void Main()
    {
        D cd1 = new D(C.M1);      // Static method
        C t = new C();
        D cd2 = new D(t.M2);      // Instance method
        D cd3 = new D(cd2);       // Another delegate
    }
}
```

一旦实例化，委托实例始终引用相同的目标对象和方法。请记住，当两个委托组合，或从一个委托中移除另一个委托时，会产生一个具有自己的调用列表的新委托；被组合或移除的委托的调用列表保持不变。

### 15.4 委托调用

C# 提供了用于调用委托的特殊语法。当调用一个调用列表只包含一个条目的非空委托实例时，它会使用传给它的相同参数调用那一个方法，并返回与被引用方法相同的值。（有关委托调用的详细信息，请参见 §7.6.5.3。）如果在此类委托的调用过程中发生异常，并且该异常未在被调用的方法中捕获，则异常捕获子句的搜索会在调用该委托的方法中继续，就像该方法直接调用了该委托所引用的方法一样。

调用其调用列表包含多个条目的委托实例时，会按顺序同步调用调用列表中的每个方法。如此调用的每个方法都会收到与传给该委托实例的同一组参数。如果此类委托调用包含引用参数（§10.6.1.2），则每次方法调用都会使用对同一变量的引用；调用列表中的一个方法对该变量所做的更改，对调用列表中更靠后的方法可见。如果委托调用包含输出参数或返回值，则它们的最终值将来自对列表中最后一个委托的调用。

如果在此类委托调用的处理过程中发生异常，并且该异常未在被调用的方法中捕获，则异常捕获子句的搜索会在调用该委托的方法中继续，而调用列表中更靠后的任何方法都不会被调用。

> **比尔·瓦格纳** 正是这种行为导致在一般情况下，你应当努力创建在任何情况下都不抛出异常的、用于实现委托的方法。它会引入你很可能无法安全恢复的错误。当你知道委托只会在单播场景中使用时，这一考虑就不那么重要了。

> **克里斯蒂安·纳格尔** 有一种方法可以处理由委托引用的处理程序方法抛出的异常。与其直接调用委托实例，不如使用委托的 GetInvocationList 方法分别调用调用列表中的每个委托。这种调用可以用 try-catch 块加以保护。在发生异常的情况下，处理失败的处理程序方法的一种方式是将其从调用列表中移除。

尝试调用值为 null 的委托实例会导致类型为 System.NullReferenceException 的异常。

> **乔恩·斯基特** 在某些方面，这一结果完全合理；而在另一些方面，它与 null 引用作为空调用列表的常规表示这一地位不一致。或许可以通过让每个委托类型都有一个 *静态* Invoke 方法来避免这种困惑——甚至可以是扩展方法——该方法可以执行适当的 null 性检查。这种解决方案会比 C# 编译器自动对每个调用表达式执行 null 检查更优雅。诚然，当委托类型具有非 void 返回类型或使用 out 参数时，事情会变得更加复杂。
>
> 无论最佳解决方案本应是什么，无可否认的是，在每次想要调用委托的地方都必须检查 null 性，这非常令人头疼。

> **埃里克·利珀特** “线程安全”委托的一种常见模式是执行类似以下操作：
>
> ```
> var temp = this.mydelegate;
> if (temp != null) temp();
> ```
>
> 而不是更显而易见的解决方案：
>
> ```
> if (this.mydelegate != null) this.mydelegate();
> ```
>
> 前者更安全，因为如果 mydelegate 可以在另一个线程上更改，那么它可能在测试与调用之间被更改为 null。此外，这种方法只消除了一种竞态。假设我们使用前一种代码。临时变量缓存了 mydelegate 的当前值。在另一个线程上，mydelegate 被设置为 null，而 mydelegate 之前的内容要成功执行所需的全局状态被销毁。但即将被调用的正是之前的内容！如果你的委托（特别是与事件关联的委托）容易受到此问题影响，则必须实现某种其他机制，以确保如果发生这种竞态，不会发生糟糕的事情。可能最好的做法是编写代码，确保即使调用了“过时”的委托，也不会发生糟糕的事情。

以下示例展示如何实例化、组合、移除和调用委托：

```
using System;
delegate void D(int x);
```



```
class C
{
    public static void M1(int i)
    {
        Console.WriteLine("C.M1: " + i);
    }

    public static void M2(int i)
    {
        Console.WriteLine("C.M2: " + i);
    }

    public void M3(int i)
    {
        Console.WriteLine("C.M3: " + i);
    }
}

class Test
{
    static void Main()
    {
        D cd1 = new D(C.M1);
        cd1(-1);                // Call M1

        D cd2 = new D(C.M2);
        cd2(-2);                // Call M2

        D cd3 = cd1 + cd2;
        cd3(10);                // Call M1 then M2

        cd3 += cd1;
        cd3(20);                // Call M1, M2, then M1

        C c = new C();
        D cd4 = new D(c.M3);
        cd3 += cd4;
        cd3(30);                // Call M1, M2, M1, then M3

        cd3 -= cd1;             // Remove last M1
        cd3(40);                // Call M1, M2, then M3

        cd3 -= cd4;
        cd3(50);                // Call M1 then M2

        cd3 -= cd2;
        cd3(60);                // Call M1

        cd3 -= cd2;             // Impossible removal is benign
        cd3(60);                // Call M1

        cd3 -= cd1;             // Invocation list is empty so cd3 is null
        // cd3(70);            // System.NullReferenceException thrown

        cd3 -= cd1;             // Impossible removal is benign
    }
}
```

## 15. 委托

如语句 cd3 += cd1; 所示，委托可以在调用列表中出现多次。在这种情况下，它会按出现次数每次调用一次。在这样的调用列表中，当该委托被移除时，实际被移除的是调用列表中最后一次出现的位置。

在最后一条语句 cd3 -= cd1; 执行之前，委托 cd3 引用一个空的调用列表。尝试从空列表中移除委托（或从非空列表中移除不存在的委托）不是错误。

产生的输出是

```
C.M1: -1
C.M2: -2
C.M1: 10
C.M2: 10
C.M1: 20
C.M2: 20
C.M1: 20
C.M2: 20
C.M1: 30
C.M2: 30
C.M1: 30
C.M2: 30
C.M1: 40
C.M2: 40
C.M3: 40
C.M1: 50
C.M2: 50
C.M3: 50
C.M1: 60
C.M2: 60
C.M1: 60
```

## 16. 异常

C# 中的异常提供了一种结构化、统一且类型安全的方式来处理系统级和应用级错误条件。C# 中的异常机制与 C++ 的非常相似，只是有一些重要的区别。

> **ERIC LIPPERT** 关于系统级和应用级异常的指导曾经是所有应用异常都应派生自 `ApplicationException`。这被证明是一个坏主意，我们不再推荐这种做法：异常来自应用程序还是框架类库几乎总是无关紧要的。

- 在 C# 中，所有异常都必须由派生自 `System.Exception` 的类类型的实例表示。在 C++ 中，任何类型的任何值都可用于表示异常。

> **ERIC LIPPERT** 在 CLR 的第一个版本中，可以抛出非异常并使用空 catch 子句在 C# 中捕获它。这使得需要捕获非异常异常的 C# 程序中的异常处理代码变得有些令人困惑。在较新版本的 CLR 中，被抛出的非异常对象会自动包装在可以正常捕获的异常对象中。

- 在 C# 中，`finally` 块 (§8.10) 可用于编写在正常执行和异常情况下都会执行的终止代码。在 C++ 中不复制代码就编写此类代码很困难。

> **ERIC LIPPERT** 人们偶尔会听到“finally 块总是执行”的神话。当然不是。finally 块在以下情况不会执行：（1）try 受保护区域进入无限循环，（2）程序在 finally 块运行之前终止，例如通过“快速失败”条件或管理员终止进程，或（3）有人拔掉电源线。确实，有时你并不希望 finally 块运行。如果异常表明程序状态混乱到运行 finally 块会使情况更糟，那么有时正确的做法就是简单地快速失败并在造成更多损害之前终止进程。

- 在 C# 中，诸如溢出、除零和空引用之类的系统级异常具有明确定义的异常类，并且与应用级错误条件处于同一水平。

> **BILL WAGNER** 这一点强调了一个重要的优势——即 C# 异常与 C++ 异常有很大共同之处。这种共同性使 C# 社区能够利用 C++ 社区（尤其是 Dave Abrahams 和 Herb Sutter）所做的工作来定义一套使代码在面对异常时更健壮的做法。

> **CHRIS SELLS** 拥有单一统一的错误通信和处理方式的价值是 .NET 提供的一项重要优势，但有时会被遗忘。当我看到 .NET 设计以其他方式传达错误时，我会假设它是错误的，直到有人证明我错了。我只能想到一次这样的情况——而且那是我自己设计的，所以我几乎不是一个公正的评判者。

> **PETER SESTOFT** Chris 规则的一个大例外（抱歉）是数值代码，其中 NaN 用于报告和传播错误，并将错误信息编码在 NaN 有效载荷位中（参见 §7.8.1 中的注释）。抛出异常可能比传播 NaN 慢三到四个数量级。当然，如果程序即使只抛出一个异常也必须以错误报告终止，速度就无关紧要了。然而，在某些情况下，数值“错误”可能只是表示输入的缺失，因此在计算过程中可能会发生数百万甚至数十亿个“错误”；在这种情况下，成本很重要。

### 16.1 异常的原因

异常可以通过两种不同的方式抛出。

- throw 语句 (§8.9.5) 会立即且无条件地抛出异常。控制永远不会到达 throw 之后的下一条语句。
- 在处理 C# 语句和表达式期间出现的某些异常条件会在操作无法正常完成时在某些情况下导致异常。例如，整数除法操作 (§7.8.2) 如果分母为零则会抛出 System.DivideByZeroException。参见 §16.4 以了解以这种方式可能发生的各种异常列表。

> **CHRISTIAN NAGEL** 在抛出异常时，不应抛出类型为 Exception 的异常，而应抛出派生自 Exception 类的类型异常。

### 16.2 System.Exception 类

System.Exception 类是所有异常的基础类型。该类有几个所有异常共有的显著属性：

- Message 是类型为 string 的只读属性，包含异常原因的人类可读描述。
- InnerException 是类型为 Exception 的只读属性。如果其值非空，则引用导致当前异常的异常——即当前异常是在处理 InnerException 的 catch 块中引发的。否则，其值为 null，表示此异常不是由另一个异常引起的。以这种方式链接在一起的异常对象的数量可以是任意的。

这些属性的值可以在对 System.Exception 的实例构造函数的调用中指定。

> **ERIC LIPPERT** 从这个描述来看，似乎异常是不可变对象，但事实并非如此。每次抛出特定异常对象实例时，该异常捕获的调用栈都会被重置。例如，如果你创建一个异常实例然后从多个线程抛出它，异常的调用栈将被观察到在处理它的所有线程上发生变化，这很可能会令人困惑。每次需要时都创建一个新的异常。



## 16.3 异常如何处理

异常由 try 语句处理（§8.10）。

当异常发生时，系统会搜索能够处理该异常的最近 catch 子句，具体由异常的运行时类型确定。首先，在当前方法中搜索词法上封闭的 try 语句，并按顺序考虑该 try 语句关联的 catch 子句。如果失败，则在调用当前方法的方法中搜索词法上封闭的 try 语句，该 try 语句包含对当前方法的调用点。此搜索会持续进行，直到找到一个能够处理当前异常的 catch 子句：该子句命名一个异常类，该类与所抛出异常的运行时类型相同，或是其基类。不指定异常类的 catch 子句可以处理任何异常。

一旦找到匹配的 catch 子句，系统就准备将控制转移到该 catch 子句的第一条语句。在执行 catch 子句开始之前，系统首先按顺序执行与那些比捕获该异常的 try 语句嵌套更深的 try 语句相关联的任何 finally 子句。

如果未找到匹配的 `catch` 子句，则会发生以下两种情况之一：

- 如果对匹配 catch 子句的搜索到达静态构造函数（§10.12）或静态字段初始化器，则在触发调用静态构造函数的位置抛出 `System.TypeInitializationException`。`System.TypeInitializationException` 的内部异常包含最初抛出的异常。
- 如果对匹配 catch 子句的搜索到达最初启动该线程的代码，则终止该线程的执行。这种终止的影响由实现定义。

> **埃里克·利珀特** 在早期版本的 CLR 中，实现定义的行为是：如果未处理异常发生在主线程上，则使应用程序终止。如果它出现在工作线程上，则策略是终止该工作线程但保持主线程继续运行。事实证明这是一个糟糕的策略，因为工作线程上存在缺陷代码的应用程序会逐渐失去所有工作线程，最终留下一个仍在运行却什么都不做的应用程序，令用户困惑。新策略更激进：*任何*线程上的未处理异常都会使应用程序终止。灾难性地失败通常比当作什么都没发生继续运行更好；如果你足够响亮地失败多次，最终会有人发现问题并修复它。

析构函数执行期间发生的异常值得特别提及。如果析构函数执行期间发生异常且该异常未被捕获，则终止该析构函数的执行，并调用基类的析构函数（如果有）。如果没有基类（如 object 类型的情况），或者没有基类析构函数，则丢弃该异常。

> **克里斯蒂安·内格尔** C# 编译器会从析构函数创建终结器。在终结器内部，会添加一个 try-finally 块，并在 finally 块中调用基类的终结器。

## 16.4 常见异常类

以下异常由某些 C# 操作抛出。

| 异常 | 描述 |
|---|---|
| System.ArithmeticException | 算术运算期间发生的异常的基类，例如 System.DivideByZeroException 和 System.OverflowException。 |
| System.ArrayTypeMismatchException | 当向数组存储元素失败，因为所存储元素的实际类型与数组的实际类型不兼容时抛出。 |
| System.DivideByZeroException | 当尝试将整数值除以零时抛出。 |
| System.IndexOutOfRangeException | 当通过小于零或超出数组边界的索引来索引数组时抛出。 |
| System.InvalidCastException | 当在运行时从基类型或接口到派生类型的显式转换失败时抛出。 |
| System.NullReferenceException | 当以需要所引用对象的方式使用空引用时抛出。 |
| System.OutOfMemoryException | 当尝试分配内存（通过 new）失败时抛出。 |
| System.OverflowException | 当在 checked 上下文中算术运算溢出时抛出。 |
| System.StackOverflowException | 当执行堆栈因过多挂起的方法调用而耗尽时抛出；通常表明递归非常深或无界。 |
| System.TypeInitializationException | 当静态构造函数抛出异常，且不存在可捕获它的 catch 子句时抛出。 |

> **乔恩·斯基特** 该表列出的不是最常见的异常，而是执行环境中由 C# 操作自然产生的异常。你自己应极少（如果曾经有过）显式抛出这些异常。相比之下，更常见的异常（如 System.ArgumentException 及其子类）未在此列出——它们由更高层的代码抛出，无论是系统库还是应用程序代码。

> **埃里克·利珀特** 我把异常分为*致命、愚蠢、恼人、外源*四类。
>
> *致命*异常既不应抛出也不应捕获；它们包括内存不足、线程中止等。问题不是你造成的，你也无法修复；异常只是通知你世界即将终结的机制。
>
> *愚蠢*异常是可避免的，因此只会由有缺陷的程序抛出；它们包括空引用解引用、无效参数等。绝不要捕获它们；捕获愚蠢异常是在掩盖某人的缺陷。相反，应修复该缺陷。
>
> *恼人*异常是你必须处理的异常，因为 API 被设计为通过异常传达事实。例如，框架的早期版本缺少“这个字符串是合法的 GUID 吗？”方法；要回答这个问题，你可能会尝试调用 GUID 构造函数并捕获恼人异常，以查看它成功还是失败。尽量不要编写会抛出恼人异常的代码。
>
> *外源*异常是你必须捕获的异常，因为它们表明现实世界中出现了意外事实：CD 已从驱动器中取出、网络路由器已拔掉，等等。

## 17. 特性

C# 语言的许多部分使程序员能够指定关于程序中定义实体的声明性信息。例如，类中某个方法的可访问性通过用 *方法修饰符* public、protected、internal 和 private 修饰该方法来指定。

C# 使程序员能够发明新的声明性信息种类，称为*特性*。然后，程序员可以将特性附加到各种程序实体上，并在运行时环境中检索特性信息。例如，框架可能定义一个 HelpAttribute 特性，可将其放置在某些程序元素（如类和方法）上，以提供从这些程序元素到其文档的映射。

> **杰西·利伯蒂** 在 Silverlight 和 WPF 中随处可见特性的常见且强大的用法：特性用于指示与某个类关联的可用视图状态。
>
> 同样，测试库使用特性区分测试方法与支持方法。Web 服务使用特性指定哪些方法向客户端公开。

特性通过声明特性类来定义（§17.1），特性类可以具有位置参数和命名参数（§17.1.2）。特性使用特性规范附加到 C# 程序中的实体上（§17.2），并可在运行时作为特性实例检索（§17.3）。

> **埃里克·利珀特** 尽量仅使用特性来描述*类型本身*，而不要表示该类型*语义*的细节。例如，假设你有一个类 Book，它有一个属性 Author。这是该类语义的一部分：该类表示书籍，而书籍有作者。如果你在 Book 类上放置 AuthorAttribute，它表示的不是*书*的作者，而是*类*的作者。Television 类可能有一个属性 Obsolete，用于指示某个特定型号是否已停产。如果你在该类上放置 ObsoleteAttribute，这意味着*该类本身*已过时，而不是它表示一个过时的产品。





## 17.1 特性类

直接或间接从抽象类 System.Attribute 派生的类都是特性类。特性类的声明定义了一种可放置在声明上的新特性。按照约定，特性类以 Attribute 为后缀命名。使用特性时既可以包含也可以省略该后缀。

### 17.1.1 特性用法

AttributeUsage 特性（§17.4.1）用于描述特性类可以如何被使用。

AttributeUsage 具有一个位置参数（§17.1.2），使特性类能够指定可在哪些种类的声明上使用它。下面的示例

```csharp
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute
{
    ...
}
```

定义了一个名为 SimpleAttribute 的特性类，它只能放置在类声明和接口声明上。下面的示例

```csharp
[Simple] class Class1 {...}
[Simple] interface Interface1 {...}
```

展示了 Simple 特性的若干用法。虽然该特性定义时使用的名称是 SimpleAttribute，但在使用该特性时可以省略 Attribute 后缀，从而得到短名称 Simple。因此，上面的示例在语义上等价于以下代码：

```csharp
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

AttributeUsage 具有一个名为 AllowMultiple 的命名参数（§17.1.2），它指示该特性是否可以为给定实体指定多次。如果某个特性类的 AllowMultiple 为 true，那么该特性类就是可多次使用的特性类，可以在一个实体上指定多次。如果某个特性类的 AllowMultiple 为 false 或未指定，那么该特性类就是只能使用一次的特性类，在一个实体上最多只能指定一次。

下面的示例

```csharp
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

定义了一个名为 AuthorAttribute 的可多次使用的特性类。下面的示例

```csharp
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1
{
    ...
}
```

展示了一个类声明，其中两次使用了 Author 特性。

> **CHRIS SELLS** 对于正在阅读这个示例却不知道 Brian Kernighan 或 Dennis Ritchie 是谁的读者：真该感到羞愧！他们是真正的软件传奇人物。

> **JON SKEET** 虽然我同意 Chris 的看法，但我当然希望所涉及的这两位备受尊敬的先生都不会写出一个名为 Class1 的类。

AttributeUsage 还有另一个名为 Inherited 的命名参数，它指示当该特性在基类上指定时，是否也由从该基类派生的类继承。如果某个特性类的 Inherited 为 true，那么该特性会被继承。如果某个特性类的 Inherited 为 false，那么该特性不会被继承。如果未指定，其默认值为 true。

如果一个特性类 X 没有附加 AttributeUsage 特性，如下所示：

```csharp
using System;
class X: Attribute {...}
```

则等价于以下内容：

```csharp
using System;
[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute {...}
```

### 17.1.2 位置参数和命名参数

> BILL WAGNER 在大多数情况下，使用命名参数会得到更清晰、更易于理解的程序。位置参数只应用于只有一个属性的特性，并且该属性通过特性名称即可明确表示，例如 AuthorAttribute。

特性类可以具有位置参数和命名参数。特性类的每个公共实例构造函数都为该特性类定义有效的位置参数序列。特性类的每个非静态公共可读写字段和属性都为该特性类定义命名参数。

下面的示例

```csharp
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute: Attribute
{
    public HelpAttribute(string url) { // Positional parameter
        ...
    }

    public string Topic {
        get {...}
        set {...}
    }

    public string Url {
        get {...}
    }
}
```

定义了一个名为 HelpAttribute 的特性类，它有一个位置参数 url 和一个命名参数 Topic。虽然属性 Url 是非静态且公共的，但它并不定义命名参数，因为它不是可读写的。

该特性类可以按如下方式使用：

```csharp
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
    ...
}

[Help("http://www.mycompany.com/.../Misc.htm", Topic = "Class2")]
class Class2
{
    ...
}
```

### 17.1.3 特性参数类型

特性类的位置参数和命名参数的类型限于*特性参数类型*：

- 以下类型之一：`bool, byte, char, double, float, int, long, sbyte, short, string, uint, ulong, ushort`。
- `object` 类型。
- `System.Type` 类型。
- 枚举类型，前提是该类型具有公共可访问性，并且其嵌套所在的类型（如果有）也具有公共可访问性（§17.2）。
- 上述类型的一维数组。

> **JON SKEET** 请注意，`decimal` 不能用作参数类型，尽管可以声明 `decimal` 常量。这是 CLI 规则渗入 C# 的一个例子。

> **MAREK SAFAR** 虽然支持数组，但对于引用类型的特性，不允许数组协变。同样，在期望 `object` 类型的位置不能使用 C# 4.0 的 `dynamic` 类型。

不具有这些类型之一的构造函数参数或公共字段，不能在特性指定中用作位置参数或命名参数。

## 17.2 特性指定

特性指定是将先前定义的特性应用到声明上。特性是为某个声明指定的一条附加声明性信息。特性可以在全局范围指定（用于指定包含程序集或模块上的特性），也可以为类型声明（§9.6）、类成员声明（§10.1.5）、接口成员声明（§13.2）、结构成员声明（§11.2）、枚举成员声明（§14.3）、访问器声明（§10.7.2）、事件访问器声明（§10.8.1）和形参列表（§10.6.1）指定。

特性在特性节中指定。特性节由一对中括号组成，中括号内是一个或多个特性的逗号分隔列表。特性在这样的列表中指定的顺序，以及附加到同一程序实体的各节的排列顺序，并不重要。例如，特性指定 [A][B]、[B][A]、[A, B] 和 [B, A] 都是等价的。

```
global-attributes:
    global-attribute-sections

global-attribute-sections:
    global-attribute-section
    global-attribute-section global-attribute-section

global-attribute-section:
    [ global-attribute-target-specifier attribute-list ]
    [ global-attribute-target-specifier attribute-list , ]

global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    assembly
    module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-section attribute-section

attribute-section:
    [ attribute-target-specifier_opt attribute-list ]
    [ attribute-target-specifier_opt attribute-list , ]

attribute-target-specifier:
    attribute-target :

attribute-target:
    field
    event
    method
    param
    property
    return
    type

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


特性由一个特性名和一个可选的位置实参和命名实参列表组成。位置实参（如果有）位于命名实参之前。位置实参由一个特性实参表达式组成；命名实参由一个名称、后跟一个等号、再后跟一个特性实参表达式组成，它们共同受与简单赋值相同的规则约束。命名实参的顺序无关紧要。

特性名标识一个特性类。如果特性名的形式为类型名，则此名称必须引用一个特性类。否则，将发生编译时错误。示例

```
class Class1 {}
[Class1] class Class2 {}    // Error
```

会导致编译时错误，因为它试图在 Class1 不是特性类时将 Class1 用作特性类。

某些上下文允许在一个以上的目标上指定特性。程序可以通过包含特性目标说明符来显式指定目标。当特性置于全局级别时，需要全局特性目标说明符。在所有其他位置，会应用合理的默认值，但在某些有歧义的情况下，可以使用特性目标说明符来确认或重写默认值（或在无歧义的情况下仅确认默认值）。因此，通常除全局级别外，可以省略特性目标说明符。可能产生歧义的上下文按如下方式解决：

- 在全局范围指定的特性可以应用于目标程序集或目标模块。此上下文不存在默认值，因此在此上下文中始终需要特性目标说明符。存在 assembly 特性目标说明符表示该特性应用于目标程序集；存在 module 特性目标说明符表示该特性应用于目标模块。
- 在委托声明上指定的特性可以应用于所声明的委托或其返回值。在缺少特性目标说明符时，该特性应用于委托。存在 type 特性目标说明符表示该特性应用于委托；存在 return 特性目标说明符表示该特性应用于返回值。
- 在方法声明上指定的特性可以应用于所声明的方法或其返回值。在缺少特性目标说明符时，该特性应用于方法。存在 method 特性目标说明符表示该特性应用于方法；存在 return 特性目标说明符表示该特性应用于返回值。

- 在运算符声明上指定的特性可以应用于所声明的运算符或其返回值。在缺少 *特性目标说明符* 时，该特性应用于运算符。存在 method *特性目标说明符* 表示该特性应用于运算符；存在 return *特性目标说明符* 表示该特性应用于返回值。
- 在省略事件访问器的事件声明上指定的特性可以应用于所声明的事件、关联字段（如果事件不是抽象的）或关联的 add 和 remove 方法。在缺少 *特性目标说明符* 时，该特性应用于事件。存在 event *特性目标说明符* 表示该特性应用于事件；存在 field *特性目标说明符* 表示该特性应用于字段；存在 method *特性目标说明符* 表示该特性应用于方法。
- 在属性或索引器声明的 get 访问器声明上指定的特性可以应用于关联方法或其返回值。在缺少 *特性目标说明符* 时，该特性应用于方法。存在 method *特性目标说明符* 表示该特性应用于方法；存在 return *特性目标说明符* 表示该特性应用于返回值。
- 在属性或索引器声明的 set 访问器上指定的特性可以应用于关联方法或其唯一的隐式参数。在缺少 *特性目标说明符* 时，该特性应用于方法。存在 method *特性目标说明符* 表示该特性应用于方法；存在 param *特性目标说明符* 表示该特性应用于参数；存在 return *特性目标说明符* 表示该特性应用于返回值。
- 在事件声明的 add 或 remove 访问器声明上指定的特性可以应用于关联方法或其唯一参数。在缺少 *特性目标说明符* 时，该特性应用于方法。存在 method *特性目标说明符* 表示该特性应用于方法；存在 param *特性目标说明符* 表示该特性应用于参数；存在 return *特性目标说明符* 表示该特性应用于返回值。

在其他上下文中，允许包含 *特性目标说明符*，但并非必需。例如，类声明可以包含或省略说明符 type：

```csharp
[Type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
```

指定无效的特性目标说明符是错误的。例如，说明符 param 不能用于类声明：

```csharp
[param: Author("Brian Kernighan")]    // Error
class Class1 {}
```

按照约定，特性类的名称带有 Attribute 后缀。形式为类型名的特性名可以包含或省略此后缀。如果同时找到带此后缀和不带此后缀的特性类，则存在歧义，并导致编译时错误。如果特性名的拼写使其最右侧标识符为逐字标识符（§2.4.2），则只匹配不带后缀的特性，从而可以解决此类歧义。示例

```csharp
using System;
[AttributeUsage(AttributeTargets.All)]
public class X: Attribute
{}
[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}
[X]                     // Error: ambiguity
class Class1 {}
[XAttribute]            // Refers to XAttribute
class Class2 {}
[@X]                    // Refers to X
class Class3 {}
[@XAttribute]           // Refers to XAttribute
class Class4 {}
```

展示了两个名为 X 和 XAttribute 的特性类。特性 [X] 有歧义，因为它可以引用 X 或 XAttribute。使用逐字标识符可以在这种罕见情况下指定确切意图。特性 [XAttribute] 没有歧义（不过，如果存在名为 XAttributeAttribute 的特性类，就会有歧义！）。如果移除类 X 的声明，则两个特性都引用名为 XAttribute 的特性类，如下所示：

```csharp
using System;
[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}
[X]                     // Refers to XAttribute
class Class1 {}
[XAttribute]            // Refers to XAttribute
class Class2 {}
[@X]                    // Error: no attribute named "X"
class Class3 {}
```

在同一实体上多次使用单次使用特性类会导致编译时错误。示例

```csharp
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute: Attribute
{
    string value;

    public HelpStringAttribute(string value) {
        this.value = value;
    }

    public string Value {
        get {...}
    }
}
[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]
public class Class1 {}
```

会导致编译时错误，因为它试图在 Class1 的声明上多次使用 HelpString，而 HelpString 是单次使用特性类。

如果以下所有语句均为真，则表达式 E 是特性实参表达式：

- E 的类型是特性参数类型（§17.1.3）。
- 在编译时，E 的值可以解析为以下之一：
  - 常量值。
  - 一个 System.Type 对象。
  - 一个特性实参表达式的一维数组。

例如：

```csharp
using System;
[AttributeUsage(AttributeTargets.Class)]
public class TestAttribute: Attribute
{
    public int P1 {
        get {...}
        set {...}
    }

    public Type P2 {
        get {...}
        set {...}
    }
}
```



```csharp
public object P3 {
    get {...}
    set {...}
}

[Test(P1 = 1234, P3 = new int[] {1, 3, 5}, P2 = typeof(float))]
class MyClass { }
```

一个 *typeof 表达式* (§7.6.11) 用作属性参数表达式时可以引用非泛型类型、封闭构造类型或未绑定泛型类型，但不能引用开放类型。这是为了确保该表达式可以在编译时解析。

```csharp
class A: Attribute
{
    public A(Type t) {...}
}

class G<T>
{
    [A(typeof(T))] T t;               // Error: open type in attribute
}

class X
{
    [A(typeof(List<int>))] int x;      // Okay: closed constructed type
    [A(typeof(List<>))] int y;         // Okay: unbound generic type
}
```

## 17.3 属性实例

一个 *属性实例* 是在运行时表示属性的实例。属性由属性类、位置参数和命名参数定义。属性实例是属性类的实例，其使用位置参数和命名参数进行初始化。

检索属性实例涉及编译时和运行时的处理，如以下各节所述。

### 17.3.1 属性的编译

一个 *属性* 的编译，其属性类为 *T*、*位置参数列表 P* 和 *命名参数列表 N*，包括以下步骤：

- 遵循编译 *对象创建表达式* new *T(P)* 形式的编译时处理步骤。这些步骤要么导致编译时错误，要么确定可在运行时调用的 *T* 上的实例构造函数 *C*。
- 如果 *C* 没有公共可访问性，则会发生编译时错误。
- 对于 N 中的每个 *命名参数* Arg：
  - 将 Name 设为该 *命名参数* Arg 的 *标识符*。
  - Name 必须标识 T 上的非静态可读写的公共字段或属性。如果 T 没有这样的字段或属性，则会发生编译时错误。
- 为属性的运行时实例化保留以下信息：属性类 T、T 上的实例构造函数 C、*位置参数列表* P 以及 *命名参数列表* N。

> **MAREK SAFAR**  在这种情况下，公共可访问性限制有点令人困惑。例如，类属性在词法上在类外部声明，但它们仍然可以使用同一类中声明的私有常量。

### 17.3.2 属性实例的运行时检索

*属性* 的编译会产生属性类 T、T 上的实例构造函数 C、*位置参数列表* P 和 *命名参数列表* N。给定这些信息，可以使用以下步骤在运行时检索属性实例：

- 遵循执行形式为 `new T(P)` 的 *对象创建表达式* 的运行时处理步骤，使用编译时确定的实例构造函数 C。这些步骤要么导致异常，要么生成 T 的实例 O。
- 按顺序对 N 中的每个 *命名参数* Arg：
  - 将 Name 设为该 *命名参数* Arg 的 *标识符*。如果 Name 未标识 T 上的非静态公共可读写字段或属性，则抛出异常。
  - 将 Value 设为 Arg 的 *属性参数表达式* 的求值结果。
  - 如果 Name 标识 O 上的字段，则将该字段设为 Value。
  - 否则，Name 标识 O 上的属性。将该属性设为 Value。
- 结果是 O，即使用 *位置参数列表* P 和 *命名参数列表* N 初始化的属性类 T 的实例。

## 17.4 保留属性

少量属性以某种方式影响语言。这些属性包括：

- `System.AttributeUsageAttribute` (§17.4.1)，用于描述属性类可以使用的方式。

## 17. 属性

- `System.Diagnostics.ConditionalAttribute` (§17.4.2)，用于定义条件方法。
- `System.ObsoleteAttribute` (§17.4.3)，用于将成员标记为已过时。

### 17.4.1 AttributeUsage 属性

AttributeUsage 属性用于描述属性类可以使用的方式。

用 AttributeUsage 属性装饰的类必须直接或间接派生自 System.Attribute。否则会发生编译时错误。

```csharp
namespace System
{
    [AttributeUsage(AttributeTargets.Class)]
    public class AttributeUsageAttribute : Attribute
    {
        public AttributeUsageAttribute(AttributeTargets validOn) {
            ...
        }

        public virtual bool AllowMultiple { get {...} set {...} }
        public virtual bool Inherited { get {...} set {...} }
        public virtual AttributeTargets ValidOn { get {...} }
    }
    public enum AttributeTargets
    {
        Assembly     = 0x0001,
        Module       = 0x0002,
        Class        = 0x0004,
        Struct       = 0x0008,
        Enum         = 0x0010,
        Constructor  = 0x0020,
        Method       = 0x0040,
        Property     = 0x0080,
        Field        = 0x0100,
        Event        = 0x0200,
        Interface    = 0x0400,
        Parameter    = 0x0800,
        Delegate     = 0x1000,
        ReturnValue  = 0x2000,

        All = Assembly | Module | Class | Struct | Enum |
              Constructor | Method | Property | Field | Event |
              Interface | Parameter | Delegate | ReturnValue
    }
}
```

### 17.4.2 Conditional 属性

Conditional 属性使条件方法和条件属性类的定义成为可能。

```csharp
namespace System.Diagnostics
{
    [AttributeUsage(AttributeTargets.Method | AttributeTargets.Class,
        AllowMultiple = true)]
    public class ConditionalAttribute : Attribute
    {
        public ConditionalAttribute(string conditionString) {...}
        public string ConditionString { get {...} }
    }
}
```

### 17.4.2.1 条件方法

用 Conditional 属性装饰的方法是条件方法。Conditional 属性通过测试条件编译符号来指示条件。对条件方法的调用是否包含或省略取决于调用点是否定义了该符号。如果定义了该符号，则包含调用；否则，省略调用（包括对接收者和调用参数的求值）。

条件方法受以下限制：

- 条件方法必须是类声明或结构声明中的方法。如果在接口声明中的方法上指定 Conditional 属性，则会发生编译时错误。
- 条件方法必须具有 void 返回类型。
- 条件方法不得使用 override 修饰符进行标记。然而，条件方法可以使用 virtual 修饰符进行标记。此类方法的重写隐式为条件，且不得显式标记为 Conditional 属性。
- 条件方法不得是接口方法的实现。否则会发生编译时错误。

此外，如果在委托创建表达式中使用条件方法，则会发生编译时错误。示例

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

声明 Class1.M 为条件方法。Class2 的 Test 方法调用此方法。由于条件编译符号 DEBUG 已定义，如果调用 Class2.Test，则会调用 M。如果未定义符号 DEBUG，则 Class2.Test 不会调用 Class1.M。

请注意，对条件方法的调用的包含或排除由调用点的条件编译符号控制。在示例中

# File class1.cs:

```csharp
using System.Diagnostics;
class Class1
{
    [Conditional("DEBUG")]
    public static void F() {
        Console.WriteLine("Executed Class1.F");
    }
}
```

# File class2.cs:

```csharp
#define DEBUG
class Class2
{
    public static void G() {
        Class1.F();        // F is called
    }
}
```

# File class3.cs:

```csharp
#undef DEBUG
class Class3
{
    public static void H() {
        Class1.F();        // F is not called
    }
}
```




类 Class2 和 Class3 各自包含对条件方法 Class1.F 的调用，该方法依据是否定义 DEBUG 来决定条件。由于该符号在 Class2 的上下文中已定义，但在 Class3 的上下文中未定义，因此 Class2 中对 F 的调用会被包含，而 Class3 中对 F 的调用会被省略。

在继承链中使用条件方法可能会令人困惑。通过 base 以 base.M 的形式对条件方法进行的调用，遵循常规的条件方法调用规则。在下面的示例中：

# 文件 class1.cs：

```
using System;
using System.Diagnostics;

class Class1
{
    [Conditional("DEBUG")]
    public virtual void M() {
        Console.WriteLine("Class1.M executed");
    }
}
```

# 文件 class2.cs：

```
using System;
class Class2: Class1
{
    public override void M() {
        Console.WriteLine("Class2.M executed");
        base.M();            // base.M is not called!
    }
}
```

# 文件 class3.cs：

```
#define DEBUG
using System;
class Class3
{
    public static void Test() {
        Class2 c = new Class2();
        c.M();               // M is called
    }
}
```

Class2 包含对在其基类中定义的 M 的调用。该调用被省略，因为基方法是条件方法，其条件取决于符号 DEBUG 是否定义，而该符号未定义。因此，该方法只会向控制台写入 "Class2.M executed"。审慎使用 pp-声明可以消除此类问题。

## 17.4.2.2 条件特性类

带有一个或多个 Conditional 特性的特性类（§17.1）即为条件特性类。因此，条件特性类与其 Conditional 特性中声明的条件编译符号相关联。例如：

```
using System;
using System.Diagnostics;
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

将 TestAttribute 声明为与条件编译符号 ALPHA 和 BETA 相关联的条件特性类。

如果在指定位置处定义了一个或多个与其关联的条件编译符号，则包含条件特性的特性规范（§17.2）；否则，省略该特性规范。

需要注意的是，条件特性类的特性规范是包含还是排除，取决于指定位置处的条件编译符号。在下面的示例中：

# 文件 test.cs：

```
using System;
using System.Diagnostics;
[Conditional("DEBUG")]
public class TestAttribute : Attribute {}
```

# 文件 class1.cs：

```
#define DEBUG
[Test]    // TestAttribute is specified
class Class1 {}
```

# 文件 class2.cs：

```
#undef DEBUG
[Test]    // TestAttribute is not specified
class Class2 {}
```

类 Class1 和 Class2 各自带有 Test 特性，该特性依据是否定义 DEBUG 来决定条件。由于该符号在 Class1 的上下文中已定义，而在 Class2 的上下文中未定义，因此 Class1 上 Test 特性的规范被包含，而 Class2 上 Test 特性的规范被省略。

> **ERIC LIPPERT** 条件特性显然与条件编译符号有着紧密的联系——但重要的是要记住，它们是截然不同的。一个常见的错误是写出类似这样的代码：

```
#if DEBUG
int counter;
#endif
[Conditional("DEBUG")] void DoIt(int x) { ... }
...
DoIt(this.counter);
```

如果未定义 DEBUG 符号，字段 counter 的定义将完全从程序中移除。编译器如何知道要移除对 DoIt 的调用？因为 DoIt(int) 是条件方法，且未定义 DEBUG。但编译器如何知道调用的是 DoIt(int) 而不是其他重载？因为 counter 被声明为 int——哦，等等，那个字段定义已被移除。没有这样的字段，因此在非调试版本中编译将失败。

## 17.4.3 Obsolete 特性

Obsolete 特性用于标记不应再使用的类型和类型成员。

```
namespace System
{
    [AttributeUsage(
        AttributeTargets.Class |
        AttributeTargets.Struct |
        AttributeTargets.Enum |
        AttributeTargets.Interface |
        AttributeTargets.Delegate |
        AttributeTargets.Method |
        AttributeTargets.Constructor |
        AttributeTargets.Property |
        AttributeTargets.Field |
        AttributeTargets.Event,
        Inherited = false)
    ]
    public class ObsoleteAttribute : Attribute
    {
        public ObsoleteAttribute() {...}
        public ObsoleteAttribute(string message) {...}
        public ObsoleteAttribute(string message, bool error) {...}
        public string Message { get {...} }
        public bool IsError { get {...} }
    }
}
```

如果程序使用了带有 Obsolete 特性的类型或成员，编译器将发出警告或错误。具体来说，如果未提供 error 参数，或提供了 error 参数但值为 false，编译器将发出警告。如果指定了 error 参数且其值为 true，编译器将发出错误。

在下面的示例中：

```csharp
[Obsolete("This class is obsolete; use class B instead")]
class A
{
    public void F() { }
}
class B
{
    public void F() { }
}
class Test
{
    static void Main()
    {
        A a = new A();      // Warning
        a.F();
    }
}
```

类 A 带有 Obsolete 特性。在 Main 中对 A 的每次使用都会产生一条警告，其中包含指定的消息："This class is obsolete; use class B instead."

> **JON SKEET** 这个例子有一个重要的教训：当您将某些内容标记为过时时，一定要给出实现类似效果的新首选方式的指导。理想情况下，还应说明为什么“旧”代码会被声明为过时（或许可以在文档中说明，而不只是在特性消息中说明）。当长期正常工作的代码突然开始毫无合理解释地发出警告时，这非常令人恼火。

> **MAREK SAFAR** 编译器不会自动将虚方法的重写标记为过时。因此，当虚方法被标记为 Obsolete 时，所有重写它的方法也必须手动使用 Obsolete 特性进行修饰。

## 17.5 用于互操作的特性

*注意：本节仅适用于 C# 的 Microsoft .NET 实现。*

## 17.5.1 与 COM 和 Win32 组件的互操作

.NET 运行时提供了大量特性，使 C# 程序能够与使用 COM 和 Win32 DLL 编写的组件进行互操作。例如，DllImport 特性可用于 static extern 方法，以指示该方法的实现位于 Win32 DLL 中。这些特性位于 System.Runtime.InteropServices 命名空间中，有关这些特性的详细文档可在 .NET 运行时文档中找到。

## 17.5.2 与其他 .NET 语言的互操作

## 17.5.2.1 IndexerName 特性

在 .NET 中，索引器是使用索引属性实现的，并且在 .NET 元数据中具有名称。如果索引器没有 IndexerName 特性，则默认使用名称 Item。IndexerName 特性使开发人员能够覆盖此默认值并指定不同的名称。

```csharp
namespace System.Runtime.CompilerServices.CSharp
{
    [AttributeUsage(AttributeTargets.Property)]
    public class IndexerNameAttribute : Attribute
    {
        public IndexerNameAttribute(string indexerName) {...}
        public string Value { get {...} }
    }
}
```

此页有意留空

## 18. 不安全代码

如前几章所定义的，C# 核心语言与 C 和 C++ 的显著区别在于它省略了指针这一数据类型。相反，C# 提供了引用以及创建由垃圾回收器管理的对象的能力。这种设计，加上其他特性，使 C# 成为比 C 或 C++ 安全得多的语言。在 C# 核心语言中，根本不可能存在未初始化的变量、“悬空”指针或对数组进行越界索引的表达式。因此，那些经常困扰 C 和 C++ 程序的整类 bug 都被消除了。

虽然 C 或 C++ 中几乎每一种指针类型构造在 C# 中都有对应的引用类型，但在某些情况下，访问指针类型仍然是必要的。例如，与底层操作系统交互、访问内存映射设备或实现时间关键型算法，如果无法访问指针，可能就无法实现或不切实际。为了满足这一需求，C# 提供了编写*不安全代码*的能力。

> **CHRIS SELLS** 自从我从事 .NET 编程以来（从 1.0 RTM 之前就开始了），我从来没有发现需要编写不安全代码的情况。一次也没有。

在不安全代码中，可以声明和操作指针，执行指针与整型之间的转换，获取变量的地址，等等。从某种意义上说，编写不安全代码就像在 C# 程序中编写 C 代码。

事实上，从开发者和用户的角度来看，不安全代码是一个“安全”的特性。不安全代码必须使用 unsafe 修饰符明确标记，这样开发者就不可能在无意中使用不安全特性，而且执行引擎会努力确保不安全代码无法在不受信任的环境中执行。





## 18.1 不安全上下文

C# 的不安全功能仅在不安全上下文中可用。不安全上下文是通过在类型或成员的声明中包含 unsafe 修饰符或使用 unsafe-statement 来引入的：

- 类、结构体、接口或委托的声明可以包含 unsafe 修饰符，在这种情况下，该类型声明的整个文本范围（包括类、结构体或接口的主体）被视为不安全上下文。
- 字段、方法、属性、事件、索引器、运算符、实例构造函数、析构函数或静态构造函数的声明可以包含 unsafe 修饰符，在这种情况下，该成员声明的整个文本范围被视为不安全上下文。
- unsafe-statement 使在块内使用不安全上下文成为可能。与之关联的块的整个文本范围被视为不安全上下文。

相关的语法扩展如下所示。为简洁起见，省略号 (...) 用于表示在前几章中出现的产生式。

```
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
```

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

destructor-declaration:
  attributes_opt extern_opt unsafe_opt ~ identifier ( ) destructor-body
  attributes_opt unsafe_opt extern_opt ~ identifier ( ) destructor-body

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

在下面的示例中

```
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
```

在 struct 声明中指定的 unsafe 修饰符会导致 struct 声明的整个文本范围成为不安全上下文。因此，可以将 Left 和 Right 字段声明为指针类型。上面的示例也可以写成如下形式：

```
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

这里，字段声明中的 unsafe 修饰符使得这些声明被视为不安全上下文。

除建立不安全上下文从而允许使用指针类型外，unsafe 修饰符对类型或成员没有影响。在下面的示例中

```
public class A
{
    public unsafe virtual void F() {
        char* p;
        ...
    }
}

public class B : A
{
    public override void F() {
        base.F();
        ...
    }
}
```

A 中 F 方法上的 unsafe 修饰符只是使 F 的文本范围成为可使用语言不安全功能的不安全上下文。在 B 中对 F 的重写中，无需重新指定 unsafe 修饰符——除非当然 B 中的 F 方法本身需要访问不安全功能。

当指针类型是方法签名的一部分时，情况略有不同：

```
public unsafe class A
{
    public virtual void F(char* p) {...}
}

public class B : A
{
    public unsafe override void F(char* p) {...}
}
```

这里，由于 F 的签名包含指针类型，它只能在不安全上下文中编写。然而，不安全上下文可以通过使整个类变为 unsafe（如 A 中所示）或在方法声明中包含 unsafe 修饰符（如 B 中所示）来引入。

## 18.2 指针类型

在不安全上下文中，*type* (§4) 除了可以是 *value-type* 或 *reference-type* 外，还可以是 *pointer-type*。然而，*pointer-type* 也可在不安全上下文之外在 typeof 表达式 (§7.6.10.6) 中使用，因为这种使用不是不安全的。

```text
type:
    ...
    pointer-type
```

*pointer-type* 以 *unmanaged-type* 或关键字 `void` 开头，后跟 `*` 标记书写：

```text
pointer-type:
    unmanaged-type  *
    void            *

unmanaged-type:
    type
```

指针类型中 `*` 之前指定的类型称为该指针类型的 *referent type*。它表示指针类型的值所指向的变量的类型。

与引用（引用类型的值）不同，指针不由垃圾回收器跟踪——垃圾回收器对指针及其指向的数据一无所知。因此，指针不允许指向引用或包含引用的结构体，并且指针的 referent type 必须是 *unmanaged-type*。

*unmanaged-type* 是任何不是 *reference-type* 或构造类型的类型，并且在任何嵌套层级都不包含 *reference-type* 或构造类型的字段。换句话说，*unmanaged-type* 是以下之一：

- `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, or `bool`.
- 任意 *enum-type*。
- 任意 *pointer-type*。
- 任意用户定义的 *struct-type*，它不是构造类型且仅包含 *unmanaged-types* 的字段。

混合使用指针和引用的直观规则是，引用的引用对象（对象）允许包含指针，但指针的引用对象不允许包含引用。

下表给出了一些指针类型的示例：

| 示例 | 描述 |
|---|---|
| byte* | 指向 byte 的指针 |
| char* | 指向 char 的指针 |
| int** | 指向 int 的指针的指针 |
| int*[] | 指向 int 的指针的单维数组 |
| void* | 指向未知类型的指针 |

对于给定的实现，所有指针类型必须具有相同的大小和表示形式。

与 C 和 C++ 不同，当在同一声明中声明多个指针时，在 C# 中 * 仅与底层类型一起书写，而不是作为每个指针名称的前缀标点。例如：

```
int* p1, p2; // NOT as int *p1, *p2;
```

类型为 T* 的指针的值表示类型为 T 的变量的地址。指针间接运算符 * (§18.5.1) 可用于访问该变量。例如，给定类型为 int* 的变量 P，表达式 *P 表示在 P 包含的地址处找到的 int 变量。

与对象引用类似，指针可以为 null。对空指针应用间接运算符会导致实现定义的行为。值为 null 的指针由全零位表示。

void* 类型表示指向未知类型的指针。由于 referent type 未知，不能对 void* 类型的指针应用间接运算符，也不能对这种指针执行任何算术运算。然而，void* 类型的指针可以强制转换为任何其他指针类型（反之亦然）。

指针类型是类型的一个独立类别。与引用类型和值类型不同，指针类型不继承自 object，并且指针类型与 object 之间不存在转换。特别是，不支持指针的装箱和拆箱 (§4.3)。然而，不同指针类型之间以及指针类型与整型之间允许进行转换。这在 §18.4 中描述。

*pointer-type* 不能用作类型参数 (§4.4)，并且类型推断 (§7.5.2) 在会推断出类型参数为指针类型的泛型方法调用上会失败。

*pointer-type* 可用作易失字段 (§10.5.3) 的类型。

尽管指针可以作为 ref 或 out 参数传递，但这样做可能导致未定义行为，因为指针可能被设置为指向一个在被调用方法返回时已不再存在的局部变量，或指向一个不再固定的固定对象。例如：

```csharp
using System;
class Test
{
    static int value = 20;
    unsafe static void F(out int* p1, ref int* p2)
    {
        int i = 10;
        p1 = &i;
        fixed (int* pj = &value)
        {
            // ...
            p2 = pj;
        }
    }

    static void Main()
    {
        int i = 10;
        unsafe
        {
            int* px1;
            int* px2 = &i;
            F(out px1, ref px2);
            Console.WriteLine("*px1 = {0}, *px2 = {1}", *px1, *px2);
            // Undefined behavior
        }
    }
}
```




方法可以返回某种类型的值，而该类型可以是指针。例如，当给定一个指向连续 int 序列的指针、该序列的元素数量以及另一个 int 值时，如果发生匹配，下面的方法会返回该值在该序列中的地址；否则，它返回 null：

```
unsafe static int* Find(int* p1, int size, int value) {
    for (int i = 0; i < size; ++i) {
        if (*p1 == value)
            return p1;
        ++p1;
    }
    return null;
}
```

在不安全上下文中，有多种构造可用于操作指针：

- * 运算符可用于执行指针间接寻址（§18.5.1）。
- -> 运算符可用于通过指针访问结构体的成员（§18.5.2）。
- [] 运算符可用于为指针建立索引（§18.5.3）。
- & 运算符可用于获取变量的地址（§18.5.4）。
- ++ 和 -- 运算符可用于递增和递减指针（§18.5.5）。
- + 和 - 运算符可用于执行指针算术运算（§18.5.6）。
- ==、!=、<、>、<= 和 >= 运算符可用于比较指针（§18.5.7）。
- stackalloc 运算符可用于从调用栈分配内存（§18.7）。
- fixed 语句可用于临时固定变量，以便获取其地址（§18.6）。

## 18.3 固定变量和可移动变量

地址运算符（§18.5.4）和 fixed 语句（§18.6）将变量分为两类：固定变量和可移动变量。

固定变量驻留在不受垃圾回收器操作影响的存储位置中。（固定变量的示例包括局部变量、值参数以及通过解引用指针创建的变量。）相反，可移动变量驻留在可能被垃圾回收器重定位或处置的存储位置中。（可移动变量的示例包括对象中的字段和数组的元素。）

& 运算符（§18.5.4）允许不受限制地获取固定变量的地址。然而，由于可移动变量可能被垃圾回收器重定位或处置，因此只能通过使用 fixed 语句（§18.6）获取可移动变量的地址，并且该地址仅在该 fixed 语句的持续时间内有效。

确切地说，固定变量是以下各项之一：

- 由引用局部变量或值参数的简单名称（§7.6.2）产生的变量，除非该变量被匿名函数捕获。
- 由形式为 V.I 的成员访问（§7.6.4）产生的变量，其中 V 是结构类型的固定变量。
- 由形式为 *P 的指针间接寻址表达式（§18.5.1）、形式为 P->I 的指针成员访问（§18.5.2）或形式为 P[E] 的指针元素访问（§18.5.3）产生的变量。

所有其他变量都归类为可移动变量。

请注意，静态字段归类为可移动变量。另请注意，ref 或 out 参数归类为可移动变量，即使为该参数提供的实参是固定变量也是如此。最后请注意，通过解引用指针产生的变量始终归类为固定变量。

## 18.4 指针转换

在不安全上下文中，可用的隐式转换（§6.1）集合被扩展为包括以下隐式指针转换：

- 从任何指针类型到 void* 类型。
- 从 null 字面量到任何指针类型。

此外，在不安全上下文中，可用的显式转换（§6.2）集合被扩展为包括以下显式指针转换：

- 从任何指针类型到任何其他指针类型。
- 从 sbyte、byte、short、ushort、int、uint、long 或 ulong 到任何指针类型。
- 从任何指针类型到 sbyte、byte、short、ushort、int、uint、long 或 ulong。

最后，在不安全上下文中，标准隐式转换（§6.3.1）集合包括以下指针转换：

- 从任何*指针类型*到 void* 类型。

两个指针类型之间的转换绝不会更改实际指针值。换句话说，从一种指针类型到另一种指针类型的转换不会影响该指针给出的基础地址。

当一种指针类型转换为另一种指针类型时，如果结果指针未针对所指向的类型正确对齐，则解引用该结果时的行为是未定义的。一般而言，“正确对齐”的概念具有传递性：如果指向类型 A 的指针对指向类型 B 的指针正确对齐，而后者又对指向类型 C 的指针正确对齐，那么指向类型 A 的指针对指向类型 C 的指针正确对齐。

考虑以下情况：通过指向另一种类型的指针访问具有一种类型的变量：

```
char c = 'A';
char* pc = &c;
void* pv = pc;
int* pi = (int*)pv;
int i = *pi;      // Undefined
*pi = 123456;     // Undefined
```

当指针类型转换为指向 byte 的指针时，结果指向该变量的最低地址字节。对结果连续递增，直到该变量的大小，会得到指向该变量其余字节的指针。例如，以下方法将 double 中的八个字节分别显示为十六进制值：

```
using System;
class Test
{
    unsafe static void Main()
    {
        double d = 123.456e23;
        unsafe
        {
            byte* pb = (byte*)&d;
            for (int i = 0; i < sizeof(double); ++i)
                Console.Write("{0:X2} ", *pb++);
            Console.WriteLine();
        }
    }
}
```

当然，产生的输出取决于字节序。

**彼得·塞斯托夫特** 不安全代码的一种用途是：通过不安全地对指针进行类型转换，重新解释表示基元数据、结构体或引用的位模式来执行转换。在大多数情况下，结果将是不可移植的或无意义的。然而，这种重新解释可用于以可移植的方式获取和设置 IEEE 浮点数的 NaN 有效载荷位（参见 §7.8.1 中的注释）：

```
    unsafe static int GetNaNPayload(float f) {
        float* p = &f;
        return *((int*)p) & 0x003FFFFF;
    }

    unsafe static float MakeNaNPayload(int nanbits) {
        float nan = Single.NaN;
        float* p = &nan;
        *((int*)p) |= (nanbits & 0x003FFFFF);
        return nan;
    }
```

不安全代码不必如此晦涩，但它很可能是错误的，因为标准的健全性检查被关闭了。

指针与整数之间的映射是实现定义的。然而，在具有线性地址空间的 32 位和 64 位 CPU 架构上，指针与整型之间的转换通常分别完全类似于 `uint` 或 `ulong` 值与这些整型之间的转换。

### 18.4.1 指针数组

在不安全上下文中，可以构造指针数组。指针数组只允许使用适用于其他数组类型的部分转换：

- 从任何*数组类型*到 `System.Array` 及其实现的接口的隐式引用转换（§6.1.6）也适用于指针数组。但是，任何通过 `System.Array` 或其实现的接口访问数组元素的尝试都会在运行时导致异常，因为指针类型不能转换为 `object`。
- 从一维数组类型 `S[]` 到 `System.Collections.Generic.IList<T>` 及其基接口的隐式和显式引用转换（§6.1.6、§6.2.4）绝不适用于指针数组，因为指针类型不能用作类型实参，并且不存在从指针类型到非指针类型的转换。
- 从 `System.Array` 及其实现的接口到任何*数组类型*的显式引用转换（§6.2.4）适用于指针数组。
- 从 System.Collections.Generic.IList<S> 及其基接口到一维数组类型 T[] 的显式引用转换（§6.2.4）绝不适用于指针数组，因为指针类型不能用作类型实参，并且不存在从指针类型到非指针类型的转换。

这些限制意味着，§8.8.4 中描述的针对数组的 foreach 语句展开不能应用于指针数组。相反，形式为

foreach (V v in x) embedded-statement

的 foreach 语句，其中 x 的类型是形式为 T[, ...] 的数组类型，n 是维数减 1，并且 T 或 V 是指针类型，将使用嵌套 for 循环按如下方式展开：

```
{
    T[, ...] a = x;
    V v;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
        for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
            ...
            for (int in = a.GetLowerBound(n); in <= a.GetUpperBound(n); in++) {
                v = (V)a.GetValue(i0,i1,...,in);
                embedded-statement
            }
}
```

变量 a、i0、i1、... in 对 x、embedded-statement 或程序的任何其他源代码不可见也不可访问。变量 v 在嵌入语句中是只读的。如果不存在从 T（元素类型）到 V 的显式转换，则会产生错误，并且不再执行进一步步骤。如果 x 的值为 null，则会在运行时引发 System.NullReferenceException。

## 18.5 表达式中的指针

在不安全上下文中，表达式可以产生指针类型的结果。在不安全上下文之外，表达式为指针类型是编译时错误。确切地说，在不安全上下文之外，如果任何简单名称（§7.6.2）、成员访问（§7.6.4）、调用表达式（§7.6.5）或元素访问（§7.6.6）为指针类型，则会发生编译时错误。

在不安全上下文中，primary-no-array-creation-expression（§7.6）和 unary-expression（§7.7）产生式允许以下附加构造：
primary-no-array-creation-expression:
...
pointer-member-access
pointer-element-access
sizeof-expression

一元表达式：
...
指针间接寻址表达式
取地址表达式

这些构造在以下各节中描述。不安全运算符的优先级和结合性由语法隐含。

## 18.5.1 指针间接寻址

指针间接寻址表达式由一个星号 (*) 后跟一个一元表达式组成。

```
pointer-indirection-expression:
  * unary-expression
```

一元 * 运算符表示指针间接寻址，用于获取指针所指向的变量。计算 *P 的结果，其中 P 是指针类型 T* 的表达式，是类型为 T 的变量。将一元 * 运算符应用于类型为 void* 的表达式或非指针类型的表达式是编译时错误。

对空指针应用一元 * 运算符的效果是实现定义的。特别是，不能保证此操作会抛出 System.NullReferenceException。

如果指针被赋予了无效值，则一元 * 运算符的行为是未定义的。通过一元 * 运算符解引用指针的无效值包括为指向的类型不当对齐的地址（参见 §18.4 中的示例），以及变量生命周期结束后的地址。

就确定性赋值分析而言，通过计算形如 *P 的表达式产生的变量被视为已初始赋值 (§5.3.1)。

## 18.5.2 指针成员访问

指针成员访问由一个主表达式、后跟一个 "->" 标记、后跟一个标识符组成。

```
pointer-member-access:
  primary-expression -> identifier type-argument-list_opt
```

在形如 P->I 的指针成员访问中，P 必须是除 void* 外的指针类型的表达式，且 I 必须表示 P 所指向类型的可访问成员。

> VLADIMIR RESHETNIKOV 你不能将指针成员访问应用于指向指针的类型（如 int**），因为指针没有成员。

形如 P->I 的指针成员访问的求值方式与 (*P).I 完全相同。有关指针间接运算符 (*) 的描述，请参见 §18.5.1。有关成员访问运算符 (.) 的描述，请参见 §7.6.4。

在示例

```csharp
using System;
struct Point
{
    public int x;
    public int y;
    public override string ToString()
    {
        return "(" + x + "," + y + ")";
    }
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

中，-> 运算符用于通过指针访问结构体的字段并调用其方法。因为操作 P->I 与 (*P).I 精确等价，Main 方法同样可以写成如下形式：

```csharp
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

## 18.5.3 指针元素访问

一个 *指针元素访问* 由一个 *主非数组创建表达式* 后跟一个用 “\[” 和 “\]” 括起来的表达式组成。

```
pointer-element-access:
    primary-no-array-creation-expression  [  expression  ]
```

在形如 P[E] 的指针元素访问中，P 必须是除 void* 外的指针类型的表达式，且 E 必须是可隐式转换为 int、uint、long 或 ulong 的表达式。

形如 P[E] 的指针元素访问的求值方式与 *(P + E) 完全相同。有关指针间接运算符 (*) 的描述，请参见 §18.5.1。有关指针加法运算符 (+) 的描述，请参见 §18.5.6。

在示例

```
class Test
{
    static void Main()
    {
        unsafe
        {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
        }
    }
}
```

中，指针元素访问用于在 for 循环中初始化字符缓冲区。因为操作 P[E] 与 *(P + E) 精确等价，该示例同样可以写成如下形式：

```
class Test
{
    static void Main()
    {
        unsafe
        {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) *(p + i) = (char)i;
        }
    }
}
```

指针元素访问运算符不检查越界错误，访问越界元素时的行为是未定义的。这与 C 和 C++ 中使用的方法相同。

## 18.5.4 取地址运算符

取地址表达式由一个与号 (&) 后跟一个一元表达式组成。

```
addressof-expression:
    & unary-expression
```

给定一个类型为 T 且被归类为固定变量 (§18.3) 的表达式 E，构造 &E 计算由 E 给出的变量的地址。结果的类型为 T* 且被归类为值。如果 E 未被归类为变量，如果 E 被归类为只读局部变量，或如果 E 表示可移动变量，则会发生编译时错误。在最后一种情况下，可以使用 fixed 语句 (§18.6) 在获取其地址之前暂时“固定”该变量。如 §7.6.4 所述，在定义只读字段的结构或类的实例构造函数或静态构造函数之外，该字段被视为值，而不是变量。因此，其地址无法获取。同样，常量的地址也无法获取。

& 运算符不要求其参数已确定赋值，但在 & 操作之后，运算符所应用的变量在该操作发生的执行路径中被视为已确定赋值。确保在此情况下变量确实得到正确初始化是程序员的责任。

在示例

```
using System;
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

中使用 &i 操作初始化 p 之后，i 被视为已确定赋值。对 *p 的赋值实际上初始化了 i，但包含此初始化是程序员的责任，如果删除该赋值也不会发生编译时错误。

& 运算符的确定性赋值规则的存在是为了避免局部变量的冗余初始化。例如，许多外部 API 接受一个由 API 填充的结构体的指针。对此类 API 的调用通常传递局部

struct 变量的地址，而没有该规则，则需要对 struct 变量进行冗余初始化。

## 18.5.5 指针递增和递减

在不安全上下文中，++ 和 -- 运算符 (§7.6.9 和 §7.7.5) 可以应用于除 void* 外的所有类型的指针变量。因此，对于每个指针类型 T*，以下运算符被隐式定义：

```
T* operator ++(T* x);
T* operator --(T* x);
```

这些运算符分别产生与 x + 1 和 x - 1 相同的结果 (§18.5.6)。换句话说，对于类型为 T* 的指针变量，++ 运算符将变量中包含的地址加上 sizeof(T)，而 -- 运算符将变量中包含的地址减去 sizeof(T)。

如果指针递增或递减操作溢出了指针类型的域，结果是实现定义的，但不会产生异常。

## 18.5.6 指针算术

在不安全上下文中，+ 和 - 运算符 (§7.8.4 和 §7.8.5) 可以应用于除 void* 外的所有指针类型的值。因此，对于每个指针类型 T*，以下运算符被隐式定义：

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

给定一个指针类型 T* 的表达式 P 和类型为 int、uint、long 或 ulong 的表达式 N，表达式 P + N 和 N + P 计算的类型为 T* 的指针值是通过将 N * sizeof(T) 加到 P 给出的地址得到的。同样，表达式 P - N 计算的类型为 T* 的指针值是通过从 P 给出的地址减去 N * sizeof(T) 得到的。



给定指针类型 T* 的两个表达式 P 和 Q，表达式 P - Q 计算 P 和 Q 给出的地址之差，然后将该差值除以 sizeof(T)。结果的类型始终为 long。实际上，P - Q 的计算方式为 ((long)(P) - (long)(Q)) / sizeof(T)。

例如，

```csharp
using System;
class Test
{
    static void Main()
    {
        unsafe
        {
            int* values = stackalloc int[20];
            int* p = &values[1];
            int* q = &values[15];
            Console.WriteLine("p - q = {0}", p - q);
            Console.WriteLine("q - p = {0}", q - p);
        }
    }
}
```

生成以下输出：

p - q = -14
q - p = 14

如果指针算术运算溢出指针类型的域，结果以实现定义的方式截断，但不会产生异常。

## 18.5.7 指针比较

在不安全上下文中，==、!=、<、>、<= 和 >= 运算符（§7.10）可应用于所有指针类型的值。指针比较运算符为：

```csharp
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

由于存在从任何指针类型到 void* 类型的隐式转换，可以使用这些运算符比较任何指针类型的操作数。比较运算符将两个操作数给出的地址当作无符号整数进行比较。

## 18.5.8 sizeof 运算符

sizeof 运算符返回给定类型的变量所占用的字节数。指定为 sizeof 操作数的类型必须是非托管类型（§18.2）。

```
sizeof-expression:
    sizeof ( unmanaged-type )
```

sizeof 运算符的结果是 int 类型的值。对于某些预定义类型，sizeof 运算符会生成如下表所示的常量值。

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

对于所有其他类型，sizeof 运算符的结果由实现定义，并且归类为值，而不是常量。

成员打包到结构体中的顺序未指定。

出于对齐目的，结构体的开头、结构体内部和结构体末尾可能存在未命名的填充。用作填充的位的内容是不确定的。

当应用于具有结构体类型的操作数时，结果是该类型变量中的总字节数，包括任何填充。

## 18.6 fixed 语句

在不安全上下文中，*嵌入语句*（§8）产生式允许一种附加构造，即 fixed 语句，它用于“固定”可移动变量，使其地址在该语句执行期间保持不变。

```
embedded-statement:
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

每个 fixed-pointer-declarator 声明一个具有给定 pointer-type 的局部变量，并用相应 fixed-pointer-initializer 计算出的地址初始化该局部变量。在 fixed 语句中声明的局部变量，可在该变量声明右侧出现的任何 fixed-pointer-initializer 中访问，也可在 fixed 语句的嵌入语句中访问。由 fixed 语句声明的局部变量被视为只读。如果嵌入语句尝试修改此局部变量（通过赋值或 ++ 和 -- 运算符）或将其作为 ref 或 out 参数传递，则会发生编译时错误。

fixed-pointer-initializer 可以是以下之一：

- 标记“&”后跟对非托管类型 T 的可移动变量（§18.3）的 *变量引用*（§5.3.3），前提是类型 T* 可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算给定变量的地址，并保证该变量在 fixed 语句执行期间保持固定地址。
- 具有非托管类型 T 元素的 *数组类型* 表达式，前提是类型 T* 可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算数组中第一个元素的地址，并保证整个数组在 fixed 语句执行期间保持固定地址。如果数组表达式为 null 或数组包含零个元素，则 fixed 语句的行为由实现定义。
- 类型为 string 的表达式，前提是类型 char* 可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算字符串中第一个字符的地址，并保证整个字符串在 fixed 语句执行期间保持固定地址。如果字符串表达式为 null，则 fixed 语句的行为由实现定义。
- 引用可移动变量的固定大小缓冲区成员的 simple-name 或 member-access，前提是该固定大小缓冲区成员的类型可隐式转换为 fixed 语句中给出的指针类型。在这种情况下，初始化器计算指向固定大小缓冲区（§18.7.2）第一个元素的指针，并保证该固定大小缓冲区在 fixed 语句执行期间保持固定地址。

> **埃里克·利珀特** 这一点展示了一种可能令人困惑的概念混用：关键字 fixed 既用于表示“位置固定”，也用于表示“大小固定”。更令人困惑的是，一个大小固定的数组成员必须位置固定才能使用。请尽量记住，大小固定的块并不会自动固定在原位。

对于 fixed-pointer-initializer 计算出的每个地址，fixed 语句确保该地址所引用的变量在 fixed 语句执行期间不会被垃圾回收器重定位或释放。例如，如果 fixed-pointer-initializer 计算出的地址引用了对象的字段或数组实例的元素，则 fixed 语句保证包含该字段或元素的对象实例在语句生存期内不会被重定位或释放。

程序员有责任确保由 fixed 语句创建的指针不会在这些语句执行结束后继续存在。例如，当由 fixed 语句创建的指针传递给外部 API 时，程序员有责任确保这些 API 不保留这些指针的任何记录。

> **埃里克·利珀特** 如果你不幸需要让一块托管内存保持在固定位置的时间超过 fixed 语句的持续期间，那么可以通过 GCHandle 类型做到这一点。话虽如此，最好一开始就避免陷入这种情况。

固定对象可能导致堆碎片化（因为它们无法移动）。因此，只有在绝对必要时才应固定对象，并且只应在尽可能短的时间内固定。

下面的示例

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

演示了 fixed 语句的几种用法。第一条语句固定并获取静态字段的地址，第二条语句固定并获取实例字段的地址，第三条语句固定并获取数组元素的地址。在每种情况下，使用常规 & 运算符都会出错，因为这些变量都被归类为可移动变量。

上面示例中的第四个 fixed 语句产生与第三个类似的结果。

下面这个 fixed 语句示例使用 string：

```csharp
class Test
{
    static string name = "xx";
    unsafe static void F(char* p)
    {
        for (int i = 0; p[i] != '\0'; ++i)
        {
            Console.WriteLine(p[i]);
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




在不安全上下文中，一维数组的数组元素按索引递增的顺序存储，从索引 0 开始，到索引 Length - 1 结束。对于多维数组，数组元素的存储方式是：最右侧维度的索引首先递增，然后是左侧的下一维度，依此类推，直到最左侧维度。在获取数组实例 a 的指针 p 的固定语句中，从 p 到 p + a.Length - 1 的指针值表示数组中各元素的地址。同样，从 p[0] 到 p[a.Length - 1] 的变量表示实际的数组元素。根据数组的存储方式，我们可以将任意维度的数组视为线性数组。

例如：

```csharp
using System;
class Test
{
    static void Main()
    {
        int[, ,] a = new int[2, 3, 4];
        unsafe
        {
            fixed (int* p = a)
            {
                for (int i = 0; i < a.Length; ++i)    // Treat as linear
                    p[i] = i;
            }
        }
        for (int i = 0; i < 2; ++i)
            for (int j = 0; j < 3; ++j)
            {
                for (int k = 0; k < 4; ++k)
                    Console.Write($"[{i},{j},{k}] = {a[i, j, k]}");
                Console.WriteLine();
            }
    }
}
```

生成以下输出：

[0,0,0] = 0 [0,0,1] = 1 [0,0,2] = 2 [0,0,3] = 3
[0,1,0] = 4 [0,1,1] = 5 [0,1,2] = 6 [0,1,3] = 7
[0,2,0] = 8 [0,2,1] = 9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23

## 18. 不安全代码

在以下示例中：

```csharp
class Test
{
    unsafe static void Fill(int* p, int count, int value)
    {
        for (; count != 0; count--) *p++ = value;
    }

    static void Main()
    {
        int[] a = new int[100];
        unsafe
        {
            fixed (int* p = a) Fill(p, 100, -1);
        }
    }
}
```

使用 fixed 语句固定数组，以便将其地址传递给接收指针的方法。

在以下示例中：

```csharp
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
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    Font f;

    unsafe static void Main()
    {
        Test test = new Test();
        test.f.size = 10;
        fixed (char* p = test.f.name)
        {
            PutString("Times New Roman", p, 32);
        }
    }
}
```

使用 fixed 语句固定结构的固定大小缓冲区，以便其地址可以作为指针使用。

通过固定字符串实例生成的 char* 值始终指向以 null 结尾的字符串。在获取字符串实例 s 的指针 p 的固定语句中，从 p 到 p + s.Length - 1 的指针值表示字符串中各字符的地址，而指针值 p + s.Length 始终指向 null 字符（值为“\0”的字符）。

通过固定指针修改托管类型的对象可能导致未定义行为。例如，由于字符串是不可变的，因此程序员有责任确保不修改固定字符串指针所引用的字符。

字符串自动以 null 结尾的特性在调用要求使用“C 风格”字符串的外部 API 时尤其方便。但是请注意，字符串实例允许包含 null 字符。如果存在此类 null 字符，将字符串作为以 null 结尾的 char* 处理时，字符串看起来会被截断。

## 18.7 固定大小缓冲区

固定大小缓冲区用于将“C 风格”的内联数组声明为结构的成员，主要用于与非托管 API 进行交互。

### 18.7.1 固定大小缓冲区声明

固定大小缓冲区是一种成员，它表示用于存储给定类型的固定长度变量缓冲区的空间。固定大小缓冲区声明会引入一个或多个具有给定元素类型的固定大小缓冲区。固定大小缓冲区只能在结构声明中使用，并且只能出现在不安全上下文（§18.1）中。

```
struct-member-declaration:
    ...
    fixed-size-buffer-declaration

fixed-size-buffer-declaration:
    attributes_opt   fixed   buffer-element-type
        fixed-size-buffer-declarators   ;

fixed-size-buffer-modifiers:
    fixed-size-buffer-modifier
    fixed-size-buffer-modifier   fixed-size-buffer-modifiers
```

```
fixed-size-buffer-modifier:
  new
  public
  protected
  internal
  private
  unsafe
```

```
buffer-element-type:
  type
```

```
fixed-size-buffer-declarators:
  fixed-size-buffer-declarator
  fixed-size-buffer-declarator , fixed-size-buffer-declarators
```

```
fixed-size-buffer-declarator:
  identifier [ constant-expression ]
```

固定大小缓冲区声明可以包含一组特性（§17）、一个 new 修饰符（§10.2.2）、四种访问修饰符的有效组合（§10.2.3）以及一个 unsafe 修饰符（§18.1）。这些特性和修饰符适用于固定大小缓冲区声明所声明的所有成员。在固定大小缓冲区声明中，同一修饰符不能出现多次。

固定大小缓冲区声明不能包含 static 修饰符。

固定大小缓冲区声明中的缓冲区元素类型指定该声明引入的缓冲区的元素类型。缓冲区元素类型必须是以下预定义类型之一：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 bool。

缓冲区元素类型后跟一个固定大小缓冲区声明符列表，其中每个声明符都会引入一个新成员。固定大小缓冲区声明符由一个用于命名成员的标识符组成，后跟用“[”和“]”标记括起来的常量表达式。该常量表达式表示此固定大小缓冲区声明符所引入成员中的元素数量。常量表达式的类型必须可隐式转换为 int 类型，并且其值必须是非零正整数。

固定大小缓冲区的元素保证在内存中按顺序布局。

声明多个固定大小缓冲区的固定大小缓冲区声明，等效于多个具有相同特性和元素类型的单个固定大小缓冲区声明。例如：

```
unsafe struct A
{
    public fixed int x[5], y[10], z[100];
}
```

等效于：

```
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```

### 18.7.2 表达式中的固定大小缓冲区

固定大小缓冲区成员的成员查找（§7.3）与字段的成员查找完全相同。

可以使用简单名称（§7.5.2）或成员访问（§7.5.4）在表达式中引用固定大小缓冲区。

当固定大小缓冲区成员作为简单名称引用时，其效果等同于 this.I 形式的成员访问，其中 I 是固定大小缓冲区成员。

在 E.I 形式的成员访问中，如果 E 属于结构类型，并且在该结构类型中对 I 执行成员查找时识别出一个固定大小成员，则 E.I 的求值和分类如下：

- 如果表达式 E.I 不在不安全上下文中，则会发生编译时错误。
- 如果 E 被分类为值，则会发生编译时错误。
- 否则，如果 E 是可移动变量（§18.3），并且表达式 E.I 不是固定指针初始化器（§18.6），则会发生编译时错误。
- 否则，E 引用一个固定变量，表达式的结果是 E 中固定大小缓冲区成员 I 的第一个元素的指针。结果类型为 S*，其中 S 是 I 的元素类型，并且结果被分类为值。

可以使用指针操作从固定大小缓冲区的第一个元素访问其后续元素。与数组访问不同，访问固定大小缓冲区的元素属于不安全操作，并且不会执行范围检查。

以下示例声明并使用了一个包含固定大小缓冲区成员的结构：

```
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}
```





```
class Test
{
    unsafe static void PutString(string s, char* buffer, int bufsize)
    {
        int len = s.Length;
        if (len > bufsize) len = bufsize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufsize; i++) buffer[i] = (char)0;
    }
    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

## 18.7.3 明确赋值检查

固定大小缓冲区不受明确赋值检查（§5.3）约束，并且就结构类型变量的明确赋值检查而言，固定大小缓冲区成员会被忽略。

当固定大小缓冲区成员的最外层包含结构变量是静态变量、类实例的实例变量或数组元素时，固定大小缓冲区的元素会自动初始化为其默认值（§5.2）。在所有其他情况下，固定大小缓冲区的初始内容未定义。

## 18.8 堆栈分配

在非安全上下文中，局部变量声明（§8.5.1）可以包含堆栈分配初始值设定项，该初始值设定项从调用堆栈分配内存。

> ERIC LIPPERT 这有点过于具体；并不要求特定 CPU 允许在其调用堆栈上分配任意内存。例如，CLR 可以在一种 CPU 架构上实现，该架构保留两个堆栈——一个用于存储局部变量，一个用于跟踪返回地址。（此类架构可防止曾困扰 x86 架构的堆栈重写攻击。）实际上，我们这里应该简单地说，每次方法调用都关联一个不可移动的本地内存存储，而 stackalloc 从该存储中分配内存。在典型实现中，该存储将是调用堆栈，但这是实现细节。

local-variable-initializer:
... 
    stackalloc-initializer

stackalloc-initializer:
    stackalloc unmanaged-type [ expression ]

非托管类型指示将存储在新分配位置中的项的类型，表达式指示这些项的数量。两者共同指定所需的分配大小。由于堆栈分配的大小不能为负，因此将项数指定为计算结果为负值的常量表达式是编译时错误。

形式为 stackalloc T[E] 的堆栈分配初始值设定项要求 T 是非托管类型（§18.2），E 是 int 类型的表达式。该构造从调用堆栈分配 E * sizeof(T) 字节，并返回指向新分配块的 T* 类型指针。如果 E 为负值，则行为未定义。如果 E 为零，则不进行分配，返回的指针由实现定义。如果没有足够内存可用于分配给定大小的块，则引发 System.StackOverflowException。

新分配内存的内容未定义。

catch 或 finally 块（§8.10）中不允许使用堆栈分配初始值设定项。

无法显式释放使用 stackalloc 分配的内存。在函数成员执行期间创建的所有堆栈分配内存块都会在该函数成员返回时自动丢弃。这对应于 alloca 函数，这是 C 和 C++ 实现中常见的扩展。

在下面的示例中

```
using System;
class Test
{
    static string IntToString(int value)
    {
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
            if (value < 0) *--p = '-';
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

在 IntToString 方法中，使用 stackalloc 初始值设定项在堆栈上分配一个包含 16 个字符的缓冲区。该方法返回时，缓冲区会自动丢弃。

## 18.9 动态内存分配

除 stackalloc 运算符外，C# 不提供用于管理非垃圾回收内存的预定义构造。此类服务通常由支持类库提供，或直接从底层操作系统导入。例如，下面的 Memory 类说明了如何从 C# 访问底层操作系统的堆函数：

```
using System;
using System.Runtime.InteropServices;

public unsafe class Memory
{
    // Handle for the process heap. This handle is used
    // in all calls to the
    // HeapXXX APIs in the methods below.

    static int ph = GetProcessHeap();

    // Private instance constructor to prevent instantiation.
    private Memory() { }

    // Allocates a memory block of the given size.
    // The allocated memory is
    // automatically initialized to zero.
    public static void* Alloc(int size)
    {
        void* result = HeapAlloc(ph, HEAP_ZERO_MEMORY, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }

    // Copies count bytes from src to dst. The source and destination
    // blocks are permitted to overlap.
    public static void Copy(void* src, void* dst, int count)
    {
        byte* ps = (byte*)src;
        byte* pd = (byte*)dst;
        if (ps > pd)
        {
            for (; count != 0; count--) *pd++ = *ps++;
        }
        else if (ps < pd)
        {
            for (ps += count, pd += count; count != 0; count--) *--pd = *--ps;
        }
    }

    // Frees a memory block.
    public static void Free(void* block)
    {
        if (!HeapFree(ph, 0, block)) throw new InvalidOperationException();
    }

    // Reallocates a memory block. If the reallocation
    // request is for a larger size, the additional region of
    // memory is automatically initialized to zero.
    public static void* ReAlloc(void* block, int size)
    {
        void* result = HeapReAlloc(ph, HEAP_ZERO_MEMORY, block, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }

    // Returns the size of a memory block.
    public static int SizeOf(void* block)
    {
        int result = HeapSize(ph, 0, block);
        if (result == -1) throw new InvalidOperationException();
        return result;
    }

    // Heap API flags
    const int HEAP_ZERO_MEMORY = 0x00000008;

    // Heap API functions
    [DllImport("kernel32")]
    static extern GetProcessHeap();

    [DllImport("kernel32")]
    static extern void* HeapAlloc(int hHeap, int flags, int size);

    [DllImport("kernel32")]
    static extern bool HeapFree(int hHeap, int flags, void* block);

    [DllImport("kernel32")]
    static extern void* HeapReAlloc(int hHeap, int flags,
        void* block, int size);
    [DllImport("kernel32")]
    static extern int HeapSize(int hHeap, int flags, void* block);
}
```

下面给出了一个使用 Memory 类的示例：

```
class Test
{
    static void Main()
    {
        unsafe
        {
            byte* buffer = (byte*)Memory.Alloc(256);
            try
            {
                for (int i = 0; i < 256; i++) buffer[i] = (byte)i;
                byte[] array = new byte[256];
                fixed (byte* p = array) Memory.Copy(buffer, p, 256);
            }
            finally
            {
                Memory.Free(buffer);
            }
            for (int i = 0; i < 256; i++) Console.WriteLine(array[i]);
        }
    }
}
```

此示例通过 Memory.Alloc 分配 256 字节内存，并使用从 0 到 255 递增的值初始化该内存块。然后它分配一个包含 256 个元素的字节数组，并使用 Memory.Copy 将内存块的内容复制到该字节数组中。最后，使用 Memory.Free 释放该内存块，并将字节数组的内容输出到控制台。

## A. 文档注释

C# 为程序员提供了一种机制，使他们可以使用包含 XML 文本的特殊注释语法来记录代码。在源代码文件中，具有某种形式的注释可用于指示工具从这些注释及其前面的源代码元素生成 XML。使用此类语法的注释称为文档注释。它们必须紧邻用户定义类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。XML 生成工具称为文档生成器。（此生成器可以是 C# 编译器本身，但不必是。）文档生成器生成的输出称为文档文件。文档文件用作文档查看器的输入——文档查看器是一种旨在以某种可视方式显示类型信息及其关联文档的工具。

本规范建议了一组可在文档注释中使用的标记。并不要求使用这些标记，如果需要，也可以使用其他标记，只要遵循格式良好的 XML 规则即可。

### A.1 引言

具有特殊形式的注释可用于指示工具从这些注释及其前面的源代码元素生成 XML。此类注释是以三个斜杠（///）开头的单行注释，或以一个斜杠和两个星号（/**）开头的分隔注释。它们必须紧邻其所注释的用户定义类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。特性节（§17.2）被视为声明的一部分，因此文档注释必须位于应用于类型或成员的特性之前。

语法：

```
single-line-doc-comment:
    /// input-characters_opt

delimited-doc-comment:
    /** delimited-comment-text_opt */
```


在单行文档注释中，如果与当前单行文档注释相邻的每个单行文档注释中，`///` 字符后有一个空白字符，则该空白字符不包含在 XML 输出中。

在分隔文档注释中，如果第二行第一个非空白字符是星号，并且相同的“可选空白字符加星号字符”模式在分隔文档注释内每一行的开头重复出现，则该重复模式的字符不包含在 XML 输出中。该模式可以在星号字符前后都包含空白字符。

## 示例：

```
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
///
public class Point
{
    /// <summary>method <c>draw</c> renders the point.</summary>
    void draw() {...}
}
```

文档注释内的文本必须根据 XML 规则（http://www.w3.org/TR/REC-xml）格式良好。如果 XML 格式不良，则会生成警告，并且文档文件将包含一条注释，说明遇到了错误。

尽管开发者可以自由创建自己的标签集，但 §A.2 中定义了一组建议标签。部分建议标签具有特殊含义：

- `<param>` 标签用于描述参数。如果使用此类标签，文档生成器必须验证指定的参数存在，并且所有参数都在文档注释中描述。如果此类验证失败，文档生成器将发出警告。
- `cref` 特性可以附加到任何标签，以提供对代码元素的引用。文档生成器必须验证该代码元素存在。如果验证失败，文档生成器将发出警告。在查找 `cref` 特性中描述的名称时，文档生成器必须根据源代码中出现的 `using` 语句遵守命名空间可见性。对于泛型代码元素，不能使用常规泛型语法（即 “List<T>”），因为它会产生无效的 XML。可以使用花括号代替尖括号（即 “List{T}”），也可以使用 XML 转义语法（即 “List&lt;T&gt;”）。
- `<summary>` 标签旨在由文档查看器用来显示关于类型或成员的附加信息。
- `<include>` 标签包含来自外部 XML 文件的信息。

请注意，文档文件不提供关于类型和成员的完整信息（例如，它不包含任何类型信息）。要获取关于类型或成员的此类信息，必须将文档文件与对实际类型或成员的反射结合使用。

## A.2 建议标签

文档生成器必须接受并处理任何根据 XML 规则有效的标签。以下标签在用户文档中提供常用功能。（当然，其他标签也是可能的。）

| 标签 | 节 | 用途 |
|---|---|---|
| `<c>` | A.2.1 | 将文本设置为类似代码的字体 |
| `<code>` | A.2.2 | 设置一行或多行源代码或程序输出 |
| `<example>` | A.2.3 | 指示示例 |
| `<exception>` | A.2.4 | 标识方法可抛出的异常 |
| `<include>` | A.2.5 | 包含来自外部文件的 XML |
| `<list>` | A.2.6 | 创建列表或表格 |
| `<para>` | A.2.7 | 允许向文本添加结构 |
| `<param>` | A.2.8 | 描述方法或构造函数的参数 |
| `<paramref>` | A.2.9 | 标识某个词是参数名 |
| `<permission>` | A.2.10 | 记录成员的安全可访问性 |
| `<remark>` | A.2.11 | 描述关于类型的附加信息 |
| `<returns>` | A.2.12 | 描述方法的返回值 |
| `<see>` | A.2.13 | 指定链接 |
| `<seealso>` | A.2.14 | 生成“另请参见”条目 |
| `<summary>` | A.2.15 | 描述类型或类型的成员 |
| `<value>` | A.2.16 | 描述属性 |

| 标签 | 节 | 用途 |
|---|---|---|
| `<typeparam>` | A.2.17 | 描述泛型类型参数 |
| `<typeparamref>` | A.2.18 | 标识某个词是类型参数名 |

### A.2.1 `<c>`

此标签提供一种机制，用于指示描述中的文本片段应使用特殊字体（例如用于代码块的字体）设置。对于实际代码行，请使用 `<code>`（§A.2.2）。

### 语法：

```
`<c>text</c>`
```

### 示例：

```
// <summary>Class <c>Point</c> models a point in a two-dimensional
// plane.</summary>
public class Point
{
    // ...
}
```

### A.2.2 `<code>`

此标签用于以某种特殊字体设置一行或多行源代码或程序输出。对于叙述中的小型代码片段，请使用 `<c>`（§A.2.1）。

### 语法：

```
`<code>source code or program output</code>`
```

### 示例：

```
// <summary>This method changes the point's location by
// the given x- and y-offsets.
// <example>For example:
// <code>
// Point p = new Point(3,5);
// p.Translate(-1,3);
// </code>
// results in <c>p</c>'s having the value (2,8).
// </example>
// </summary>

public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### A.2.3 `<example>`

此标签允许注释中的示例代码指定方法或其他库成员可以如何使用。通常，这也会涉及使用 `<code>` 标签（§A.2.2）。

### 语法：

```
<example>description</example>
```

### 示例：

有关示例，请参见 `<code>`（§A.2.2）。

### A.2.4 `<exception>`

此标签提供一种记录方法可抛出异常的方法。

### 语法：

```
<exception cref="member">description</exception>
```

其中

```
cref="member"
```

成员的名称。文档生成器检查给定成员是否存在，并将 `member` 转换为文档文件中的规范元素名称。

description
异常抛出情况的描述。

### 示例：

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
        // _
    }
}
```

### A.2.5 `<include>`

此标签允许包含来自源代码文件外部 XML 文档的信息。外部文件必须是格式良好的 XML 文档，并且对该文档应用 XPath 表达式，以指定要包含该文档中的哪些 XML。然后，`<include>` 标签会被来自外部文档的选定 XML 替换。

### 语法：

```
<include file="filename" path="xpath" />
```

其中

```
file="filename"
```

外部 XML 文件的文件名。该文件名相对于包含 `include` 标签的文件进行解释。

```
path="xpath"
```

一个 XPath 表达式，用于选择外部 XML 文件中的部分 XML。

### 示例：

如果源代码包含如下声明：

```
// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class Intlist { ... }
```

并且外部文件 “docs.xml” 具有以下内容：

```
<?xml version="1.0" ?>
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

那么输出的文档将与源代码包含以下内容时相同：

```
/// <summary>
/// Contains a list of integers.
/// </summary>
public class Intlist { ... }
```

### A.2.6 `<list>`

此标签用于创建项列表或表格。它可以包含一个 `<listheader>` 块，用于定义表格或定义列表的标题行。（定义表格时，只需提供标题中 `term` 的条目。）

列表中的每一项都用 `<item>` 块指定。创建定义列表时，必须同时指定 `term` 和 *description*。然而，对于表格、项目符号列表或编号列表，只需指定 *description*。

### 语法：

```xml
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

其中

- term
  要定义的术语，其定义在 *description* 中。
- description
  项目符号列表或编号列表中的项，或者 *term* 的定义。

### 示例：

```java
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
}
```



## A.2.7 <para>

此标签用于其他标签内部，例如 <summary>（§A.2.11）或 <returns>（§A.2.12），并允许向文本中添加结构。

语法：

```
<para>content</para>
```

其中

content

段落的文本。

示例：

```
/// <summary>This is the entry point of the Point class testing program.
/// <para>This program tests each method and operator, and
/// is intended to be run after any nontrivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // ...
}
```

## A.2.8 <param>

此标签用于描述方法、构造函数或索引器的参数。

语法：

```
<param name="name">description</param>
```

## A.2.9 <paramref>

此标签用于指示某个词是参数。可以处理文档文件，以某种独特方式格式化此参数。

语法：

```
<paramref name="name"/>
```

其中

name

参数的名称。

示例：

```
/// <summary>This constructor initializes the new point to
/// <paramref name="xor"></paramref>,<paramref name="yor"></paramref>.</summary>
/// <param name="xor">the new point's x-coordinate.</param>
/// <param name="yor">the new point's y-coordinate.</param>
public Point(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

## A.2.10 <permission>

此标签允许记录成员的安全可访问性。

语法：

```
<permission cref="member">description</permission>
```

其中

cref="member"

成员的名称。文档生成器会检查给定的代码元素是否存在，并将 member 转换为文档文件中的规范元素名称。

description

对成员访问权限的描述。

示例：

```
/// <permission cref="System.Security.PermissionSet">Everyone can
/// access this method.</permission>
public static void Test() {
    // ...
}
```

## A.2.11 <remark>

此标签用于指定有关类型的额外信息。（使用 <summary>（§A.2.15）描述类型本身以及类型的成员。）

语法：

```
<remark>description</remark>
```

其中

*描述*

备注的文本。

示例：

```
/// <summary>Class <c>Point</c> models a point in a
/// two-dimensional plane.</summary>
/// <remark>Uses polar coordinates</remark>
public class Point
{
    // ...
}
```

## A.2.12 <returns>

此标签用于描述方法的返回值。

语法：

```
<returns>description</returns>
```

其中

*描述*

返回值的描述。

示例：

```
/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y),
///  without any leading, trailing, or embedded whitespace.</returns>
public override string ToString() {
    return "(" + X + "," + Y + ")";
}
```

## A.2.13 <see>

此标签允许在文本中指定链接。使用 <seealso>（§A.2.14）指示要出现在“另请参阅”部分中的文本。

语法：

```
<see cref="member"/>
```

其中

```
cref="member"
```

成员的名称。文档生成器会检查给定的代码元素是否存在，并将 member 更改为生成的文档文件中的元素名称。

示例：

```
/// <summary>This method changes the point's location to
/// the given coordinates.</summary>
/// <see cref="Translate"/>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// </summary>
/// <see cref="Move"/>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

## A.2.14 <seealso>

此标签允许为“另请参阅”部分生成一个条目。使用 <see>（§A.2.13）指定文本中的链接。

语法：

```
<seealso cref="member"/>
```

其中

```
cref="member"
```

成员的名称。文档生成器会检查给定的代码元素是否存在，并将 member 更改为生成的文档文件中的元素名称。

示例：

```
// <summary>This method determines whether two points have the same
// location.</summary>
// <seealso cref="operator==" />
// <seealso cref="operator!=" />
public override bool Equals(object o) {
    // ...
}
```

## A.2.15 <summary>

此标签可用于描述类型或类型的成员。使用 <remark>（§A.2.11）描述类型本身。

语法：

```
<summary>description</summary>
```

其中

description

类型或成员的摘要。

示例：

```
// <summary>This constructor initializes the new point to (0,0).</summary>
public Point() : this(0,0) {
}
```

## A.2.16 <value>

此标签允许描述属性。

语法：

```
<value>property description</value>
```

其中

property description

属性的描述。

示例：

```
// <value>Property <c>X</c> represents the point's x-coordinate.</value>
public int X
{
    get { return x; }
    set { x = value; }
}
```

## A.2.17 <typeparam>

此标签用于描述类、结构、接口、委托或方法的泛型类型参数。

语法：

```
<typeparam name="name">description</typeparam>
```

其中

name

类型参数的名称。

description

类型参数的描述。

示例：

```
/// <summary>A generic list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
public class MyList<T> {
  ...
}
```

## A.2.18 <typeparamref>

此标签用于指示某个词是类型参数。可以处理文档文件，以某种独特方式格式化此类型参数。

语法：

```
<typeparamref name="name"/>
```

其中

name

类型参数的名称。

示例：

```
/// <summary>This method fetches data and returns a
///   list of <typeparamref name="T" />.</summary>
/// <param name="string">query to execute</param>
public List<T> FetchData<T>(string query) {
  ...
}
```

## A.3 处理文档文件

文档生成器会为源代码中带有文档注释标记的每个元素生成一个 ID 字符串。此 ID 字符串唯一标识一个源元素。文档查看器可以使用 ID 字符串来标识文档所适用的对应元数据或反射项。

文档文件不是源代码的层次化表示；相反，它是一个扁平列表，每个元素都有一个生成的 ID 字符串。

### A.3.1 ID 字符串格式

文档生成器在生成 ID 字符串时遵循以下规则：

- 字符串中不放置空白字符。
- 字符串的第一部分通过一个后跟冒号的单个字符来标识所记录的成员种类。下表列出了已定义的成员种类。

| 字符 | 说明 |
|---|---|
| E | 事件 |
| F | 字段 |
| M | 方法（包括构造函数、析构函数和运算符） |
| N | 命名空间 |
| P | 属性（包括索引器） |
| T | 类型（例如类、委托、枚举、接口和结构） |
| ! | 错误字符串；字符串的其余部分提供有关该错误的信息。例如，文档生成器会为无法解析的链接生成错误信息。 |

- 字符串的第二部分是元素的完全限定名，从命名空间的根开始。元素名称、其封闭类型和命名空间用句点分隔。如果项本身的名称包含句点，则这些句点会被替换为 #（U+0023）字符。（假定没有元素的名称包含此字符。）

对于带参数的方法和属性，后面是参数列表，并括在圆括号中。对于没有参数的成员，省略圆括号。参数之间用逗号分隔。每个参数的编码与 CLI 签名相同，如下所示：

参数由其文档名称表示，该名称基于其完全限定名，并按如下方式修改：

- 表示泛型类型的参数会追加一个 &#96; 字符，后跟类型参数的数量。
- 具有 out 或 ref 修饰符的参数在其类型名后有一个 @。按值传递或通过 params 传递的参数没有特殊表示法。
- 数组参数表示为 [ lowerbound : size , ... , lowerbound : size ]，其中逗号的数量为秩减 1，每个维度的下界和大小（如果已知）用十进制表示。如果未指定下界或大小，则省略它。如果省略某个特定维度的下界和大小，则“:”也一并省略。交错数组每层用一个“[]”表示。
- 具有非 void 指针类型的参数使用类型名后的 * 表示。void 指针使用类型名 System.Void 表示。
- 引用在类型上定义的泛型类型参数的参数使用 &#96; 字符后跟该类型参数的从零开始的索引进行编码。
- 使用在方法中定义的泛型类型参数的参数使用双反引号 &#96;&#96;，而不是类型所用的 &#96;。
- 引用构造泛型类型的参数使用泛型类型编码，后跟“{”，再后跟以逗号分隔的类型参数列表，再后跟“}”。

### A.3.2 ID 字符串示例

以下每个示例展示一段 C# 代码片段，以及从每个能够带有文档注释的源元素生成的 ID 字符串：

类型使用其完全限定名表示，并补充泛型信息：

```
enum Color { Red, Blue, Green }
namespace Acme
{
    interface IProcess {...}
    struct ValueType {...}
```




```
class Widget: IProcess
{
    public class NestedClass {...}
    public interface IMenuItem {...}
    public delegate void Del(int i);
    public enum Direction { North, South, East, West }
}
class MyList<T>
{
    class Helper<U,V> {...}
}
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

- 字段由其完全限定名表示：

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

## 构造函数。

```
namespace Acme
{
    class Widget: IProcess
    {
        static Widget() {...}
        public Widget() {...}
        public Widget(string s) {...}
    }
}
```

"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor(System.String)"

## 析构函数。

```
namespace Acme
{
    class Widget: IProcess
    {
        ~Widget() {...}
    }
}
```

"M:Acme.Widget.Finalize"

## 方法。

```
namespace Acme
{
    struct ValueType
    {
        public void M(int i) {...}
    }
    class Widget: IProcess
    {
        public class NestedClass
        {
            public void M(int i) {...}
        }
    }
```

## A. 文档注释

```
```
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
    public void Test(T t) { }
}
class UseList
{
    public void Process(MyList<int> list) { }
    public MyList<T> GetValues<T>(T inputValue) { return null; }
}
"M:Acme.ValueType.M(System.Int32)"
"M:Acme.Widget.NestedClass.M(System.Int32)"
"M:Acme.Widget.M0"
"M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
"M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
"M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:,0:][])"
"M:Acme.Widget.M4(System.Char*,Color**)"
"M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:][])"
"M:Acme.Widget.M6(System.Int32,System.Object[])"
"M:Acme.MyList`1.Test(`0)"
"M:Acme.UseList.Process(Acme.MyList{System.Int32})"
"M:Acme.UseList.GetValues``1(`0)"

- 属性和索引器。

```
```
namespace Acme
{
    class Widget: IProcess
    {
        public int Width { get {...} set {...} }
        public int this[int i] { get {...} set {...} }
        public int this[string s, int i] { get {...} set {...} }
    }
}
```

"P:Acme.Widget.Width"
"P:Acme.Widget.Item(System.Int32)"
"P:Acme.Widget.Item(System.String,System.Int32)"

- 事件。

```
```
namespace Acme
{
    class Widget: IProcess
    {
```
```
public event Del AnEvent;
}
}
"E:Acme.Widget.AnEvent"

- 一元运算符。

```
namespace Acme
{
    class Widget: IProcess
    {
        public static Widget operator+(Widget x) {...}
    }
}
```

"M:Acme.Widget.op_UnaryPlus(Acme.Widget)"

所使用的完整一元运算符函数名称集如下：op_UnaryPlus、op_UnaryNegation、op_LogicalNot、op_OnesComplement、op_Increment、op_Decrement、op_True 和 op_False。

- 二元运算符。

```
namespace Acme
{
    class Widget: IProcess
    {
        public static Widget operator+(Widget x1, Widget x2) {...}
    }
}
```

"M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"

所使用的完整二元运算符函数名称集如下：op_Addition、op_Subtraction、op_Multiply、op_Division、op_Modulus、op_BitwiseAnd、op_BitwiseOr、op_ExclusiveOr、op_LeftShift、op_RightShift、op_Equality、op_Inequality、op_LessThan、op_LessThanOrEqual、op_GreaterThan 和 op_GreaterThanOrEqual。

- 转换运算符在其后带有“~”，后跟返回类型。

```
namespace Acme
{
    class Widget: IProcess
    {
        public static explicit operator int(Widget x) {...}
        public static implicit operator long(Widget x) {...}
    }
}
```

"M:Acme.Widget.op_Explicit(Acme.Widget)->System.Int32"
"M:Acme.Widget.op_Implicit(Acme.Widget)->System.Int64"

## A.4 示例

### A.4.1 C# 源代码

以下示例展示了 Point 类的源代码：

```
```csharp
namespace Graphics
{
    /// <summary>Class <c>Point</c> models a point in a two-dimensional plane.
    /// </summary>
    public class Point
    {
        /// <summary>Instance variable <c>x</c> represents the point's
        /// x-coordinate.</summary>
        private int x;

        /// <summary>Instance variable <c>y</c> represents the point's
        /// y-coordinate.</summary>
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

        /// <summary>This constructor initializes the new point to
        /// (0,0).</summary>
        public Point() : this(0, 0) { }

        /// <summary>This constructor initializes the new point to
        /// (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
        /// <param><c>xor</c> is the new point's x-coordinate.</param>
        /// <param><c>yor</c> is the new point's y-coordinate.</param>
        public Point(int xor, int yor)
        {
            X = xor;
            Y = yor;
        }

        /// <summary>This method changes the point's location to
        /// the given coordinates.</summary>
        /// <param><c>xor</c> is the new x-coordinate.</param>
        /// <param><c>yor</c> is the new y-coordinate.</param>
        /// <see cref="Translate"/>
        public void Move(int xor, int yor)
        {
            X = xor;
            Y = yor;
        }
    }
}
```
```

```
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// <example>For example:
///
/// <code>
/// Point p = new Point(3,5);
/// p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// </example>
/// </summary>
/// <param><c>xor</c> is the relative x-offset.</param>
/// <param><c>yor</c> is the relative y-offset.</param>
/// <see cref="Move"/>
public void Translate(int xor, int yor)
{
    X += xor;
    Y += yor;
}
/// <summary>This method determines whether two points have the same
/// location.</summary>
/// <param><c>o</c> is the object to be compared to the current object.</param>
/// <returns>True if the points have the same location and they have
/// the exact same type; otherwise, false.</returns>
/// <seealso cref="operator=="/>
/// <seealso cref="operator!="/>
public override bool Equals(object o)
{
    if (o == null)
    {
        return false;
    }
    if (this == o)
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
/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y),
/// without any leading, trailing, or embedded whitespace.</returns>
public override string ToString()
{
    return "(" + X + "," + Y + ")";
}
/// <summary>This method determines whether two points have the same
/// location.</summary>
/// <param><c>p1</c> is the first point to be compared.</param>
```



## A. 文档注释

```csharp
/// <param name="p2"><c>p2</c> is the second point to be compared.</param>
/// <returns>True if the points have the same location and they have
/// the exact same type; otherwise, false.</returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator!="/>
public static bool operator ==(Point p1, Point p2)
{
    if ((object)p1 == null || (object)p2 == null)
    {
        return false;
    }
    if (p1.GetType() == p2.GetType())
    {
        return (p1.X == p2.X) && (p1.Y == p2.Y);
    }
    return false;
}
/// <summary>This operator determines whether two points have the same
/// location.</summary>
/// <param name="p1"><c>p1</c> is the first point to be compared.</param>
/// <param name="p2"><c>p2</c> is the second point to be compared.</param>
/// <returns>True if the points do not have the same location and the
/// exact same type; otherwise, false.</returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator=="/>
public static bool operator !=(Point p1, Point p2)
{
    return !(p1 == p2);
}
/// <summary>This is the entry point of the Point class testing
/// program.</summary>
/// <para>This program tests each method and operator, and
/// is intended to be run after any nontrivial maintenance has
/// been performed on the Point class.</para>
public static void Main()
{
    // Class test code goes here
}
```

### A.4.2 生成的 XML

以下是某个文档生成器在给定上面所示的 Point 类源代码时生成的输出：

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
<members>
  <member name="T:Graphics.Point">
    <summary>
      Class <c>Point</c> models a point in a two-dimensional
      plane.
    </summary>
  </member>
  <member name="F:Graphics.Point.x">
    <summary>
      Instance variable <c>x</c> represents the point's
      x-coordinate.
    </summary>
  </member>
  <member name="F:Graphics.Point.y">
    <summary>
      Instance variable <c>y</c> represents the point's
      y-coordinate.
    </summary>
  </member>
  <member name="M:Graphics.Point.#ctor">
    <summary>
      This constructor initializes the new point to
      (0,0).
    </summary>
  </member>
  <member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
    <summary>
      This constructor initializes the new point to
      (<paramref name="x"/>, <paramref name="y"/>).
    </summary>
    <param>
      <c>x</c> is the new point's x-coordinate.
    </param>
    <param>
      <c>y</c> is the new point's y-coordinate.
    </param>
  </member>
  <member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
    <summary>
      This method changes the point's location to
      the given coordinates.
    </summary>
    <param>
      <c>x</c> is the new x-coordinate.
    </param>
    <param>
      <c>y</c> is the new y-coordinate.
    </param>
    <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
  </member>
<member name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
<summary>
This method changes the point's location by
the given x- and y-offsets.
<example>
For example:
<code>
Point p = new Point(3,5);
p.Translate(-1,3);
</code>
results in <c>p</c>'s having the value (2,8).
</example>
</summary>
<param name="x">
<c>x</c> is the relative x-offset.
</param>
<param name="y">
<c>y</c> is the relative y-offset.
</param>
<see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
</member>
<member name="M:Graphics.Point.Equals(System.Object)">
<summary>
This method determines whether two points have the same
location.
</summary>
<param name="obj">
<c>obj</c> is the object to be compared to the current
object.
</param>
<returns>
True if the points have the same location and they have
the exact same type; otherwise, false.
</returns>
<seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
</seealso>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.ToString">
<summary>Report a point's location as a string.</summary>
<returns>
A string representing a point's location, in the form
(x,y)
without any leading, trailing, or embedded whitespace.
</returns>
</member>
<member name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
<summary>
This operator determines whether two points have the
same
location.
</summary>
</summary>
<param>
  <c>p1</c> is the first point to be compared.
</param>
<param>
  <c>p2</c> is the second point to be compared.
</param>
<returns>
  True if the points have the same location and they have
  the exact same type; otherwise, false.
</returns>
<seealso cref="M:Graphics.Point.Equals(System.Object)"/>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
  <summary>
    This operator determines whether two points have the
    same
    location.
  </summary>
  <param>
    <c>p1</c> is the first point to be compared.
  </param>
  <param>
    <c>p2</c> is the second point to be compared.
  </param>
  <returns>
    True if the points do not have the same location and the
    exact same type; otherwise, false.
  </returns>
  <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
  <seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.Main">
  <summary>
    This is the entry point of the Point class testing
    program.
    <para>
      This program tests each method and operator, and
      is intended to be run after any nontrivial maintenance has
      been performed on the Point class.
    </para>
  </summary>
</member>
<member name="P:Graphics.Point.X">
  <value>
    Property <c>X</c> represents the point's
    x-coordinate.
  </value>
</member>
<member name="P:Graphics.Point.Y">
    <value>
Property <c>Y</c> represents the point's
y-coordinate.
    </value>
</member>
</members>
</doc>
```

## B. 语法

本附录包含主文档中出现的词法语法和句法语法摘要，以及针对不安全代码的语法扩展。语法产生式在此处按其在主文档中出现的相同顺序列出。

### B.1 词法语法

```
input:
    input-section_opt
input-section:
    input-section-part
    input-section input-section-part
input-section-part:
    input-elements_opt new-line
    pp-directive
input-elements:
    input-element
    input-elements input-element
input-element:
    whitespace
    comment
    token
```

### B.1.1 行终止符

new-line:
- 回车字符（U+000D）
- 换行字符（U+000A）
- 回车字符（U+000D）后跟换行字符（U+000A）
- 下一行字符（U+0085）
- 行分隔符字符（U+2028）
- 段落分隔符字符（U+2029）

### B.1.2 注释

```
comment:
  single-line-comment
  delimited-comment

single-line-comment:
  // input-characters_opt

input-characters:
  input-character
  input-characters input-character

input-character:
  Any Unicode character except a new-line-character

new-line-character:
  Carriage return character (U+000D)
  Line feed character (U+000A)
  Next line character (U+0085)
  Line separator character (U+2028)
  Paragraph separator character (U+2029)

delimited-comment:
  /* delimited-comment-text_opt asterisks /

delimited-comment-text:
  delimited-comment-section
  delimited-comment-text delimited-comment-section

delimited-comment-section:
  /
  asterisks_opt not-slash-or-asterisk

asterisks:
  *
  asterisks *

not-slash-or-asterisk:
  Any Unicode character except / or *
```

### B.1.3 空白

```
whitespace:
    Any character with Unicode class Zs
    Horizontal tab character (U+0009)
    Vertical tab character (U+000B)
    Form feed character (U+000C)
```

### B.1.4 标记

```
token:
    identifier
    keyword
    integer-literal
    real-literal
    character-literal
    string-literal
    operator-or-punctuator
```

### B.1.5 Unicode 字符转义序列

```
unicode-escape-sequence:
    \u hex-digit hex-digit hex-digit hex-digit
    \U hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit
```

### B.1.6 标识符

```
identifier:
    available-identifier
    @ identifier-or-keyword
```

```
available-identifier:
    An identifier-or-keyword that is not a keyword
```

```
identifier-or-keyword:
    identifier-start-character identifier-part-characters_opt
```

```
identifier-start-character:
    letter-character
    _ (the underscore character U+005F)
```

```
identifier-part-characters:
    identifier-part-character
    identifier-part-characters identifier-part-character
```


identifier-part-character:
  letter-character
  decimal-digit-character
  connecting-character
  combining-character
  formatting-character

letter-character:
  属于 Lu、Ll、Lt、Lm、Lo 或 Nl 类的 Unicode 字符
  表示 Lu、Ll、Lt、Lm、Lo 或 Nl 类字符的 Unicode 转义序列

combining-character:
  属于 Mn 或 Mc 类的 Unicode 字符
  表示 Mn 或 Mc 类字符的 Unicode 转义序列

decimal-digit-character:
  属于 Nd 类的 Unicode 字符
  表示 Nd 类字符的 Unicode 转义序列

connecting-character:
  属于 Pc 类的 Unicode 字符
  表示 Pc 类字符的 Unicode 转义序列

formatting-character:
  属于 Cf 类的 Unicode 字符
  表示 Cf 类字符的 Unicode 转义序列

## B.1.7 关键字

keyword: 以下之一

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

## B.1.8 字面量

```
literal:
    boolean-literal
    integer-literal
    real-literal
    character-literal
    string-literal
    null-literal

boolean-literal:
    true
    false

integer-literal:
    decimal-integer-literal
    hexadecimal-integer-literal

decimal-integer-literal:
    decimal-digits integer-type-suffix_opt

decimal-digits:
    decimal-digit
    decimal-digits decimal-digit

decimal-digit: one of
    0 1 2 3 4 5 6 7 8 9

integer-type-suffix: one of
    U u L l UL Ul uL ul LU Lu lU lu

hexadecimal-integer-literal:
    0x hex-digits integer-type-suffix_opt
    0X hex-digits integer-type-suffix_opt

hex-digits:
    hex-digit
    hex-digits hex-digit

hex-digit: one of
    0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f
```

```
~~~
real-literal:
    decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
    . decimal-digits exponent-part_opt real-type-suffix_opt
    decimal-digits exponent-part real-type-suffix_opt
    decimal-digits real-type-suffix

exponent-part:
    e sign_opt decimal-digits
    E sign_opt decimal-digits

sign: one of
    + -

real-type-suffix: one of
    F f D d M m

character-literal:
    ' character '

character:
    single-character
    simple-escape-sequence
    hexadecimal-escape-sequence
    unicode-escape-sequence

single-character:
    Any character except ' (U+0027), \ (U+005C), and new-line-character

simple-escape-sequence: one of
    \' \" \\ \0 \a \b \f \n \r \t \v

hexadecimal-escape-sequence:
    \x hex-digit hex-digit_opt hex-digit_opt hex-digit_opt

string-literal:
    regular-string-literal
    verbatim-string-literal

regular-string-literal:
    " regular-string-literal-characters_opt "

regular-string-literal-characters:
    regular-string-literal-character
    regular-string-literal-characters regular-string-literal-character
~~~
```

regular-string-literal-character:
  single-regular-string-literal-character
  simple-escape-sequence
  hexadecimal-escape-sequence
  unicode-escape-sequence

single-regular-string-literal-character:
  除 " (U+0022)、\ (U+005C) 和换行字符之外的任意字符

verbatim-string-literal:
  @" verbatim-string-literal-characters_opt "

verbatim-string-literal-characters:
  verbatim-string-literal-character
  verbatim-string-literal-characters verbatim-string-literal-character

verbatim-string-literal-character:
  single-verbatim-string-literal-character
  quote-escape-sequence

single-verbatim-string-literal-character:
  除 " 之外的任意字符

quote-escape-sequence:
  ""

null-literal:
  null

## B.1.9 运算符和标点符号

operator-or-punctuator: 以下之一
{ } [ ] ( ) . , : ;
+ - * / % & | ^ ~
= < > ? ?? :: ++ -- && ||
-> == != <= >= += -= *= /= %=
&= |= ^= << <<= =>

right-shift:
  >|>

right-shift-assignment:
  >|>=

## B.1.10 预处理指令

```text
pp-directive:
    pp-declaration
    pp-conditional
    pp-line
    pp-diagnostic
    pp-region
    pp-pragma

conditional-symbol:
    Any identifier-or-keyword except true or false

pp-expression:
    whitespace_opt pp-or-expression whitespace_opt

pp-or-expression:
    pp-and-expression
    pp-or-expression whitespace_opt || whitespace_opt pp-and-expression

pp-and-expression:
    pp-equality-expression
    pp-and-expression whitespace_opt && whitespace_opt pp-equality-expression

pp-equality-expression:
    pp-unary-expression
    pp-equality-expression whitespace_opt == whitespace_opt pp-unary-expression
    pp-equality-expression whitespace_opt != whitespace_opt pp-unary-expression

pp-unary-expression:
    pp-primary-expression
    ! whitespace_opt pp-unary-expression

pp-primary-expression:
    true
    false
    conditional-symbol
    ( whitespace_opt pp-expression whitespace_opt )

pp-declaration:
    whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
    whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line
```

```
pp-new-line:
    whitespace_opt single-line-comment_opt new-line

pp-conditional:
    pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif

pp-if-section:
    whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line
    conditional-section_opt

pp-elif-sections:
    pp-elif-section
    pp-elif-sections pp-elif-section

pp-elif-section:
    whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line
    conditional-section_opt

pp-else-section:
    whitespace_opt # whitespace_opt else pp-new-line conditional-section_opt

pp-endif:
    whitespace_opt # whitespace_opt endif pp-new-line

conditional-section:
    input-section
    skipped-section

skipped-section:
    skipped-section-part
    skipped-section skipped-section-part

skipped-section-part:
    skipped-characters_opt new-line
    pp-directive

skipped-characters:
    whitespace_opt not-number-sign input-characters_opt

not-number-sign:
    Any input-character except #
```

```
pp-diagnostic:
    whitespace_opt # whitespace_opt error pp-message
    whitespace_opt # whitespace_opt warning pp-message

pp-message:
    new-line
    whitespace input-characters_opt new-line

pp-region:
    pp-start-region conditional-section_opt pp-end-region

pp-start-region:
    whitespace_opt # whitespace_opt region pp-message

pp-end-region:
    whitespace_opt # whitespace_opt endregion pp-message

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

pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line

pragma-body:
    pragma-warning-body

pragma-warning-body:
    warning whitespace warning-action
    warning whitespace warning-action whitespace warning-list
```

```
~~~
warning-action:
    disable
    restore
~~~
```

```
~~~
warning-list:
    decimal-digits
    warning-list whitespace_opt , whitespace_opt decimal-digits
~~~
```

## B.2 句法语法

### B.2.1 基本概念

```
~~~
namespace-name:
    namespace-or-type-name
~~~
```

```
~~~
type-name:
    namespace-or-type-name
~~~
```

```
~~~
namespace-or-type-name:
    identifier type-argument-list_opt
    namespace-or-type-name . identifier type-argument-list_opt
    qualified-alias-member
~~~
```

### B.2.2 类型

```
~~~
type:
    value-type
    reference-type
    type-parameter
~~~
```

```
~~~
value-type:
    struct-type
    enum-type
~~~
```

```
~~~
struct-type:
    type-name
    simple-type
    nullable-type
~~~
```

```
~~~
simple-type:
    numeric-type
    bool
~~~
```



## B. 语法

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

floating-point-type:
    float
    double

nullable-type:
    non-nullable-value-type  ?

non-nullable-value-type:
    type

enum-type:
    type-name

reference-type:
    class-type
    interface-type
    array-type
    delegate-type

class-type:
    type-name
    object
    dynamic
    string

interface-type:
    type-name
```

```
array-type:
    non-array-type rank-specifiers

non-array-type:
    type

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

type-argument-list:
    < type-arguments >

type-arguments:
    type-argument
    type-arguments , type-argument

type-argument:
    type

type-parameter:
    identifier
```

### B.2.3 变量

```
variable-reference:
    expression
```

### B.2.4 表达式

```
argument-list:
    argument
    argument-list , argument
```

```
argument:
    argument-name_opt  argument-value

argument-name:
    identifier :

argument-value:
    expression
    ref variable-reference
    out variable-reference

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
    checked-expression
    unchecked-expression
    default-value-expression
    anonymous-method-expression

simple-name:
    identifier type-argument-list_opt

parenthesized-expression:
    ( expression )
```

```
member-access:
    primary-expression  .  identifier type-argument-list
    predefined-type  .  identifier type-argument-list_opt
    qualified-alias-member  .  identifier type-argument-list_opt

predefined-type: one of
    bool      byte      char      decimal      double      float      int      long
    object    sbyte     short     string       uint       ulong      ushort

invocation-expression:
    primary-expression  (  argument-list_opt  )

element-access:
    primary-no-array-creation-expression  [  argument-list  ]

this-access:
    this

base-access:
    base  .  identifier
    base  [  argument-list  ]

post-increment-expression:
    primary-expression  ++

post-decrement-expression:
    primary-expression  --

object-creation-expression:
    new  type  (  argument-list_opt  )  object-or-collection-initializer_opt
    new  type  object-or-collection-initializer

object-or-collection-initializer:
    object-initializer
    collection-initializer

object-initializer:
    {  member-initializer-list_opt  }
    {  member-initializer-list  ,  }

member-initializer-list:
    member-initializer
    member-initializer-list  ,  member-initializer
```

```
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

expression-list:
    expression
    expression-list , expression

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
```

```
member-declarator:
    simple-name
    member-access
    base-access
    identifier = expression

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
```

```
pre-increment-expression:
    ++ unary-expression

pre-decrement-expression:
    -- unary-expression

cast-expression:
    ( type ) unary-expression

multiplicative-expression:
    unary-expression
    multiplicative-expression * unary-expression
    multiplicative-expression / unary-expression
    multiplicative-expression % unary-expression

additive-expression:
    multiplicative-expression
    additive-expression + multiplicative-expression
    additive-expression - multiplicative-expression

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
```

```
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
    anonymous-function-signature => anonymous-function-body

anonymous-method-expression:
    delegate explicit-anonymous-function-signature_opt block

anonymous-function-signature:
    explicit-anonymous-function-signature
    implicit-anonymous-function-signature

explicit-anonymous-function-signature:
    ( explicit-anonymous-function-parameter-list_opt )

explicit-anonymous-function-parameter-list:
    explicit-anonymous-function-parameter
    explicit-anonymous-function-parameter-list , explicit-anonymous-function-parameter

explicit-anonymous-function-parameter:
    anonymous-function-parameter-modifier_opt type identifier
```

```
anonymous-function-parameter-modifier:
    ref
    out

implicit-anonymous-function-signature:
    ( implicit-anonymous-function-parameter-list )_opt
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
```


```text
join-into-clause:
    join type_opt identifier in expression on expression equals expression
    into identifier

orderby-clause:
    orderby orderings

orderings:
    ordering
    orderings , ordering

ordering:
    expression ordering-direction_opt

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

assignment:
    unary-expression assignment-operator expression

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

expression:
    non-assignment-expression
    assignment

non-assignment-expression:
    conditional-expression
    lambda-expression
    query-expression

constant-expression:
    expression

boolean-expression:
    expression
```

### B.2.5 语句

```text
statement:
    labeled-statement
    declaration-statement
    embedded-statement

embedded-statement:
    block
    empty-statement
    expression-statement
    selection-statement
    iteration-statement
    jump-statement
    try-statement
    checked-statement
    unchecked-statement
    lock-statement
    using-statement
    yield-statement

block:
    {   statement-list_opt   }

statement-list:
    statement
    statement-list   statement

empty-statement:
    ;

labeled-statement:
    identifier : statement

declaration-statement:
    local-variable-declaration ;
    local-constant-declaration ;

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

local-constant-declaration:
    const type constant-declarators

constant-declarators:
    constant-declarator
    constant-declarators , constant-declarator

constant-declarator:
    identifier = constant-expression

expression-statement:
    statement-expression ;

statement-expression:
    invocation-expression
    object-creation-expression
    assignment
    post-increment-expression
    post-decrement-expression
    pre-increment-expression
    pre-decrement-expression

selection-statement:
    if-statement
    switch-statement

if-statement:
    if ( boolean-expression ) embedded-statement
    if ( boolean-expression ) embedded-statement else embedded-statement

switch-statement:
    switch ( expression ) switch-block

switch-block:
    { switch-sections_opt }

switch-sections:
    switch-section
    switch-sections switch-section

switch-section:
    switch-labels statement-list

switch-labels:
    switch-label
    switch-labels switch-label

switch-label:
    case constant-expression :
    default :

iteration-statement:
    while-statement
    do-statement
    for-statement
    foreach-statement

while-statement:
    while ( boolean-expression ) embedded-statement

do-statement:
    do embedded-statement while ( boolean-expression ) ;

for-statement:
    for ( for-initializer_opt ; for-condition_opt ; for-iterator_opt ) embedded-statement

for-initializer:
    local-variable-declaration
    statement-expression-list

for-condition:
    boolean-expression

for-iterator:
    statement-expression-list

statement-expression-list:
    statement-expression
    statement-expression-list , statement-expression

foreach-statement:
    foreach ( local-variable-type identifier in expression ) embedded-statement

jump-statement:
    break-statement
    continue-statement
    goto-statement
    return-statement
    throw-statement

break-statement:
    break ;

continue-statement:
    continue ;

goto-statement:
    goto identifier ;
    goto case constant-expression ;
    goto default ;

return-statement:
    return expression_opt ;

throw-statement:
    throw expression_opt ;

try-statement:
    try block catch-clauses
    try block finally-clause
    try block catch-clauses finally-clause

catch-clauses:
    specific-catch-clauses general-catch-clause_opt
    specific-catch-clauses_opt general-catch-clause

specific-catch-clauses:
    specific-catch-clause
    specific-catch-clauses specific-catch-clause

specific-catch-clause:
    catch ( class-type identifier_opt ) block

general-catch-clause:
    catch block

finally-clause:
    finally block

checked-statement:
    checked block

unchecked-statement:
    unchecked block

lock-statement:
    lock ( expression ) embedded-statement

using-statement:
    using ( resource-acquisition ) embedded-statement

resource-acquisition:
    local-variable-declaration
    expression

yield-statement:
    yield return expression ;
    yield break ;
```

### B.2.6 命名空间

```text
compilation-unit:
    extern-alias-directives_opt using-directives_opt global-attributes_opt
        namespace-member-declarations_opt

namespace-declaration:
    namespace qualified-identifier namespace-body ;_opt

qualified-identifier:
    identifier
    qualified-identifier . identifier

namespace-body:
    { extern-alias-directives_opt using-directives_opt namespace-member-declarations_opt }

extern-alias-directives:
    extern-alias-directive
    extern-alias-directives extern-alias-directive

extern-alias-directive:
    extern alias identifier ;

using-directives:
    using-directive
    using-directives using-directive

using-directive:
    using-alias-directive
    using-namespace-directive

using-alias-directive:
    using identifier = namespace-or-type-name ;

using-namespace-directive:
    using namespace-name ;

namespace-member-declarations:
    namespace-member-declaration
    namespace-member-declarations namespace-member-declaration

namespace-member-declaration:
    namespace-declaration
    type-declaration

type-declaration:
    class-declaration
    struct-declaration
    interface-declaration
    enum-declaration
    delegate-declaration

qualified-alias-member:
    identifier :: identifier type-argument-list_opt
```

### B.2.7 类

```text
class-declaration:
    attributes_opt class-modifiers_opt partial_opt class identifier type-parameter-list_opt
        class-base_opt type-parameter-constraints-clauses_opt class-body ;_opt

class-modifiers:
    class-modifier
    class-modifiers class-modifier

class-modifier:
    new
    public
    protected
    internal
    private
    abstract
    sealed
    static

type-parameter-list:
    < type-parameters >

type-parameters:
    attributes_opt type-parameter
    type-parameters , attributes_opt type-parameter

type-parameter:
    identifier

class-base:
    : class-type
    : interface-type-list
    : class-type , interface-type-list

interface-type-list:
    interface-type
    interface-type-list , interface-type

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


class-body:
    { class-member-declarations_opt }

class-member-declarations:
    class-member-declaration
    class-member-declarations class-member-declaration

class-member-declaration:
    constant-declaration
    field-declaration
    method-declaration
    property-declaration
    event-declaration
    indexer-declaration
    operator-declaration
    constructor-declaration
    destructor-declaration
    static-constructor-declaration
    type-declaration

constant-declaration:
    attributes_opt constant-modifiers_opt const type constant-declarators ;

constant-modifiers:
    constant-modifier
    constant-modifiers constant-modifier

constant-modifier:
    new
    public
    protected
    internal
    private

constant-declarators:
    constant-declarator
    constant-declarators , constant-declarator

constant-declarator:
    identifier = constant-expression

field-declaration:
    attributes_opt field-modifiers_opt type variable-declarators ;

field-modifiers:
    field-modifier
    field-modifiers field-modifier

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

return-type:
  type
  void

member-name:
  identifier
  interface-type . identifier

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
  ref
  out
  this

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

member-name:
  identifier
  interface-type . identifier

accessor-declarations:
  get-accessor-declaration set-accessor-declaration_opt
  set-accessor-declaration get-accessor-declaration_opt

get-accessor-declaration:
  attributes_opt accessor-modifier_opt get accessor-body

set-accessor-declaration:
  attributes_opt accessor-modifier_opt set accessor-body

accessor-modifier:
    protected
    internal
    private
    protected  internal
    internal  protected

accessor-body:
    block
    ;

event-declaration:
    attributes_opt event-modifiers_opt event type variable-declarators ;
    attributes_opt event-modifiers_opt event type member-name
        { event-accessor-declarations }

event-modifiers:
    event-modifier
    event-modifiers  event-modifier

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
    add-accessor-declaration  remove-accessor-declaration
    remove-accessor-declaration  add-accessor-declaration

add-accessor-declaration:
    attributes_opt add block

remove-accessor-declaration:
    attributes_opt remove block

indexer-declaration:
    attributes_opt  indexer-modifiers_opt  indexer-declarator  {  accessor-declarations  }

indexer-modifiers:
    indexer-modifier
    indexer-modifiers  indexer-modifier

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
    type  this  [  formal-parameter-list  ]
    type  interface-type  .  this  [  formal-parameter-list  ]

operator-declaration:
    attributes_opt  operator-modifiers  operator-declarator  operator-body

operator-modifiers:
    operator-modifier
    operator-modifiers  operator-modifier

operator-modifier:
    public
    static
    extern

operator-declarator:
    unary-operator-declarator
    binary-operator-declarator
    conversion-operator-declarator

unary-operator-declarator:
    type  operator  overloadable-unary-operator  (  type  identifier  )

overloadable-unary-operator:  以下之一
    +    -    !    ~    ++    --    true    false

binary-operator-declarator:
    type operator overloadable-binary-operator ( type identifier , type identifier )

overloadable-binary-operator:
    +
    -
    *
    /
    %
    &
    |
    ^
    <<
    >>
    ==
    !=
    >
    <
    >=
    <=

conversion-operator-declarator:
    implicit operator type ( type identifier )
    explicit operator type ( type identifier )

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

destructor-declaration:
    attributes_opt extern_opt ~ identifier ( ) destructor-body

destructor-body:
    block
    ;

## B.2.8 结构体

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

## B.2.9 数组

array-type:
  non-array-type rank-specifiers

non-array-type:
  type

rank-specifiers:
  rank-specifier
  rank-specifiers rank-specifier

rank-specifier:
  [ dim-separators_opt ]

dim-separators:
  ,
  dim-separators ,

array-initializer:
  { variable-initializer-list_opt }
  { variable-initializer-list , }

variable-initializer-list:
  variable-initializer
  variable-initializer-list , variable-initializer

variable-initializer:
  expression
  array-initializer

## B.2.10 接口

interface-declaration:
  attributes_opt interface-modifiers_opt partial_opt interface
    identifier variant-type-parameter-list_opt interface-base_opt
      type-parameter-constraints-clauses_opt interface-body ;_opt

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
  attributes_opt new_opt return-type identifier type-parameter-list
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

## B.2.11 枚举

```
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
```

## B.2.12 委托

## B.2.13 属性

```
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

delegate-declaration:
  attributes_opt delegate-modifiers_opt delegate return-type
  identifier variant-type-parameter-list
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

global-attributes:
  global-attribute-sections

global-attribute-sections:
  global-attribute-section
  global-attribute-sections global-attribute-section

global-attribute-section:
  [ global-attribute-target-specifier attribute-list ]
  [ global-attribute-target-specifier attribute-list , ]
```

## B. 语法

```
global-attribute-target-specifier:
    global-attribute-target :

global-attribute-target:
    assembly
    module

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
    field
    event
    method
    param
    property
    return
    type

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
```

```
positional-argument-list:
    positional-argument
    positional-argument-list  ,  positional-argument
```

```
positional-argument:
    argument-name<sub>opt</sub>  attribute-argument-expression
```

```
named-argument-list:
    named-argument
    named-argument-list  ,  named-argument
```

```
named-argument:
    identifier  =  attribute-argument-expression
```

```
attribute-argument-expression:
    expression
```

## B.3 不安全代码的语法扩展

```
class-modifier:
    ...
    unsafe
```

```
struct-modifier:
    ...
    unsafe
```

```
interface-modifier:
    ...
    unsafe
```

```
delegate-modifier:
    ...
    unsafe
```

```
field-modifier:
    ...
    unsafe
```

```
method-modifier:
    ...
    unsafe
```

```
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

destructor-declaration:
  attributes_opt extern_opt unsafe_opt ~ identifier ( ) destructor-body
  attributes_opt unsafe_opt extern_opt ~ identifier ( ) destructor-body

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
  fixed-statement

unsafe-statement:
  unsafe block

type:
  ...
  pointer-type
```

```
pointer-type:
    unmanaged-type *
    void *

unmanaged-type:
    type

primary-no-array-creation-expression:
    ...
    pointer-member-access
    pointer-element-access
    sizeof-expression

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

sizeof-expression:
    sizeof ( unmanaged-type )

fixed-statement:
    fixed ( pointer-type fixed-pointer-declarators ) embedded-statement

fixed-pointer-declarators:
    fixed-pointer-declarator
    fixed-pointer-declarators , fixed-pointer-declarator

fixed-pointer-declarator:
    identifier = fixed-pointer-initializer
```

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

local-variable-initializer:
  ...
  stackalloc-initializer

stackalloc-initializer:
  stackalloc unmanaged-type [ expression ]

## C. 参考文献

IEEE. IEEE 二进制浮点算术标准。ANSI/IEEE 标准 754-1985。可从 http://www.ieee.org 获取。

ISO/IEC. C++。ANSI/ISO/IEC 14882:1998。

Unicode Consortium. Unicode 标准，版本 3.0。Addison-Wesley, Reading, Massachusetts, 2000, ISBN 0-201-616335-5。

本页特意留空

## 索引

A
\a 转义序列,81
抽象访问器, 46, 557-558
抽象类
  与接口, 661
  概述, 468-469
抽象事件, 566
抽象索引器, 567
抽象方法, 35, 539-540
访问和可访问性
  数组元素, 628
  包含类型, 502-503
  事件, 253
  索引器, 253, 300-301
  成员, 23-24, 107, 496
  可访问性域, 110-113
  约束, 116-117
  声明的可访问性, 107-109
  接口, 642-644
  指针, 721-722
  在主表达式中, 283-288
  protected, 113-116
  嵌套类型, 499-503
  指针元素, 723
  主表达式元素, 298-301
  属性, 252, 555-556
访问器
  抽象, 46, 557-558
  属性, 695
  事件, 564-565
  属性, 43, 46, 547-853
Acquire 语义, 514
using 语句中的获取, 445-446
add 访问器
  属性, 695
  事件, 49, 564
Add 方法
  IEnumerable, 311
  List, 42
AddEventHandler 方法, 565
加法运算符
  描述, 15
  用法, 337-340
取地址运算符, 724-725
地址
  固定变量, 728-733
  用于指针, 714, 724-725
枚举器对象的 after 状态, 593-596
Alert 转义序列,81
别名
  用于命名空间和类型, 456-461
  限定符, 464-466
  唯一性, 466
对齐枚举, 58-59
Alloc 方法, 738
分配，栈, 736-738
AllowMultiple 参数,688

+   - 歧义
+     - 语法, 287–288
+     - 在查询表达式中, 376
+   - 与号 (&)
+     - 用于地址, 716
+     - 在赋值运算符中, 389
+     - 确定性赋值规则, 188–189
+     - 用于逻辑运算符, 355–359
+     - 用于指针, 724–725
+     - 在预处理表达式中, 87
+   - AND 运算符, 15
+   - 用于类型参数的角度括号 (<>), 160
+   - 匿名函数
+     - 主体, 367
+     - 转换, 219–221
+       - 评估为委托类型, 165–166, 221–222
+       - 评估为表达式树类型, 222
+     - 实现示例, 222–226
+     - 隐式, 204
+     - 确定性赋值规则, 192
+     - 委托创建, 61
+     - 动态绑定, 369
+     - 评估, 373
+     - 表达式, 165–166, 326, 364–366
+     - 外部变量, 369–373
+     - 重载, 368
+     - 签名, 365–366
+   - 匿名对象, 317–319
+   - AppendFormat 方法, 31
+   - 可适用函数成员, 271–272
+   - 应用程序域, 99
+   - ApplicationException 类, 681
+   - 应用程序, 4
+     - 启动, 99–100
+     - 终止, 100–101
+   - Apply 方法, 60
+   - 参数, 28。另请参阅 Parameters
+     - 命令行, 99
+     - 用于函数成员, 254–259
+       - 类型, 161–162
+       - 类型推断, 259–270
+   - 算术运算符, 331–332
+     - 加法, 337–340
+     - 除法, 334–335
+   - 乘法, 332–333
+   - 指针, 725–726
+   - 余数, 336–337
+   - 移位, 344
+   - 减法, 340–342
+   - ArithmeticException 类, 335, 685
+   - 数组和数组类型, 625
+     - 访问, 299–300, 628
+     - 内容, 13
+     - 转换, 200
+     - 协变, 200, 629–630
+     - 创建, 628
+     - 描述, 8, 155
+     - 元素, 53, 171, 628
+     - 与 foreach, 429
+     - IList 接口, 627–628
+     - 初始化器, 55, 630–632
+     - 成员, 106, 628
+     - new 运算符, 53, 55, 312–315
+     - 概述, 53–55
+     - 参数, 31, 528–531
+     - 和指针, 719–720, 730–731
+     - 秩说明符, 625–626
+     - 语法语法, 804–805
+   - ArrayTypeMismatchException 类
+     - 描述, 685
+     - 类型不匹配, 390–391, 629
+   - as 运算符, 353–355
+   - 程序集, 4–5
+   - 赋值
+     - 在类与结构中, 612
+     - 确定。另请参阅 Definite assignment
+     - 固定大小缓冲区, 736
+   - 赋值运算符, 16
+     - 复合, 393–394
+     - 事件, 394–395
+     - 概述, 389–390
+     - 简单, 390–393
+   - 运算符结合性, 238–240
+   - 星号 (*)
+     - 赋值运算符, 389
+     - 注释, 69–70, 741–742
+     - 乘法, 332–333
+     - 指针, 713–716, 721
+     - 透明标识符, 385



## B
- 标识符中的 @ 符号字符，72-74
- 变量引用的原子性，193
- 属性类，62,688
- 属性，687
  - 类，688–691，704–705
  - 编译，698–699
  - 编译单元，454
  - 实例，698–699
  - 用于互操作，707
  - 概述，61–63
  - 参数，690–691
  - 部分类型，482–483
  - 保留，699–700
    - AttributeUsage，700
    - Conditional，701–705
    - Obsolete，705–706
  - 部分，692
  - 规范，692–698
  - 语法结构，807–809
- AttributeUsage 属性，688–690,700
- 自动内存管理，132–137
- 自动实现的属性，548，553–555
- \b 转义序列，81
- 反斜杠字符 (\)
  - 用于字符，80–81
  - 转义序列，80–81
  - 用于字符串，82
- Backspace 转义序列，81
- 反引号字符 (`)，83
- 银行家舍入，150
- 基访问，302–303
- 基类，22，25–26
  - 部分类型，484
  - 规范，472–475
  - 类型参数约束，476
- 基接口
  - 继承自，637–638
  - 部分类型，484–485
- 基础类型，249–250
- 枚举器对象的 before 状态，593–596
- 更好的转换，274–275
- 更好的函数成员，272–273
- 二元运算符，238
  - 声明，574–575
  - 在 ID 字符串格式中，759
  - 提升，246
  - 数字提升，244–245
  - 重载解析，243
  - 可重载，241
- 二进制点类型，9
- Bind 方法，56
- 绑定
  - 构成表达式，237
  - 动态，166，234–237
  - 名称，490
  - 静态，234–235
  - 时间，235
- BitArray 类，569–570
- 按位补码运算符，328
- 块
  - 在声明中，102–104
  - 确定性赋值规则，179
  - 退出，430
  - 在语法记法中，66
  - 不变含义，281–283
  - 在方法中，544
  - 可达性，401
  - 在语句中，402–404
  - 用于不安全代码，710
- 主体
  - 类，481
  - 接口，638
  - 方法，32–33,544
  - 结构，609
- Boneheaded 异常，686
- bool 类型，8–9，150–151
- 布尔值
  - 表达式，397
  - 字面量，76
  - 运算符
    - 条件逻辑，359
    - 相等，348
    - 逻辑，357
  - 在结构示例中，622–623
- Boss 类，47
- 绑定类型，162
- Box 类，539
- 装箱实例上的调用，278
- 装箱，12，155-156
  - 在类与结构中，613-616
  - 转换，156-158，201
- break 语句
  - 确定性赋值规则，182
  - 示例，19
  - 用于 for 语句，423
  - 概述，431
  - 用于 switch，416-417
  - 用于 while，420
  - yield break，449-452,594-595
- 脆弱基类综合征，35,292
- 脆弱派生类综合征，292,297
- 固定大小的缓冲区
  - 声明，733-735
  - 确定性赋值，736
  - 在表达式中，735-736
- 错误。参见 Unsafe code
- Button 类，549,561
- byte 类型，10

## C
- <<> 标签，744
- Cache 类，444
- 可调用实体，671
- 候选用户定义运算符，243
- 捕获的外层变量，369-370
- 插入符号 (^)
  - 在赋值运算符中，389
  - 用于逻辑运算符，355-357
- 回车字符
  - 转义序列，81
  - 作为行终止符，68-69
- case 标签，415-419
- 强制转换表达式，330-331
- cast 运算符与 as 运算符，355
- catch 块
  - 确定性赋值规则，183-185
  - 用于异常，684-685
  - throw 语句，436-437
  - try 语句，438-443
- char 类型，146
- 字符字面量，80-81
- 字符，9
- checked 语句
  - 确定性赋值规则，179
  - 示例，20
  - 概述，443
  - 在主表达式中，322-325
- Chooser 类，259-260
- 类
  - 可访问性，23
  - 属性，688-691,704-705
  - 基类，25-26,472-475
  - 主体，481
  - 常量，506-508
  - 构造函数，42-43
  - 实例，579-586
  - 静态，586-589
  - 声明，467
  - 基规范，472-475
  - 主体，481
  - 修饰符，467-471
  - 部分类型，471
  - 类型参数约束，475-481
  - 类型参数，471-472
  - 定义，467
  - 析构函数，50,589-591
  - 事件，47-49
  - 访问器，564-565
  - 声明，559-562
  - 类似字段，562-564
  - 实例和静态，565
  - 字段，26-27
  - 声明，509-510
  - 初始化，515-516
  - 只读，511-513
  - 静态和实例，510-511
  - 变量初始化器，516-519
  - volatile，514-515
  - 函数成员，40-50
  - 索引器，46-47,566-571
  - 实例变量，170-171
  - 接口实现，57
  - 迭代器。参见 Iterators
  - 成员，22–23，106，490–492
    - 访问修饰符，496
    - 构成类型，496
    - 构造类型，493–494
    - 继承，494–496
    - 实例类型，492
    - 嵌套类型，498–504
    - new 修饰符，496
    - 保留名称，504–506
    - 静态和实例，496–498
  - 方法，28–40
    - 抽象，539–540
    - 主体，544
    - 声明，520–522
    - 扩展，541–543
    - 外部，539–540
    - 参数，522–531
    - 部分，541
    - 密封，537–538
    - 静态和实例，531
    - 虚拟，532–534
  - 运算符，49–50
    - 二元，574–575
    - 转换，575–578
    - 声明，571–573
    - 一元，573–574
  - 概述，21–22
  - 部分类型。参见 Partial types
  - 在程序结构中，4–5
  - 属性，43–46
    - 可访问性，555–556
    - 访问器，547–553
    - 自动实现，553–555
    - 声明，545–546
    - 静态和实例，546
  - 与结构对比，610–619
  - 语法结构，794–803
  - 类型参数，24–25
  - 类型，6–13，153–154
- 表达式分类，231–234
- 单击事件，562–563
- 封闭类型，162
- CLS（通用语言规范），9
- <code> 标签，744
- 集合
  - 用于 foreach，425
  - 初始化器，310–312
- 冒号 (:)
  - 别名限定符，464–465
  - 语法产生式，66
  - 接口标识符，637
  - 三元运算符，191，361–362
  - 类型参数约束，476
- Color 类，27，512
- Color 枚举，58，664–666
- Color 结构，286
- COM，与之互操作，707
- 组合委托，340，675
- 命令行参数，99
- 逗号 (,)
  - 数组，54
  - 属性，692
  - 集合初始化器，310
  - ID 字符串格式，755
  - 接口标识符，637
  - 方法参数列表，522
  - 对象初始化器，307
- 注释，741
  - 文档文件处理，754–759
  - 示例，760–766
  - 词法语法，69–70，768
  - 概述，741–743
  - 标签，743–753
  - 用于 XML，741–742，762–765
- Commit 方法，92
- 通用语言规范（CLS），9
- 类型推断的通用类型，270
- CompareExchange 方法，600
- 比较运算符，49
  - 布尔值，348
  - 十进制数，348
  - 委托，351–352
  - 枚举，348
  - 浮点数，346–347
  - 整数，346
  - 概述，344–345
  - 指针，726
  - 引用类型，349–351
  - 字符串，351
- 委托与方法兼容性，676
- 编译
  - 属性，698–699
  - 绑定，235
  - 动态重载解析检查，275–276
  - 即时编译，5
- 编译指令，90–93
- 编译符号，87
- 编译单元产生式，67
- 编译单元，65，453–454
- 实例的编译时类型，35,532
- 补码运算符，328
- 组件化编程，1–2
- 复合赋值
  - 运算符，389
  - 过程，393–394
- 字符串连接，339
- 条件属性，701–705
- 条件类，704–705
- 条件编译指令，90–93
- 条件编译符号，87
- 条件逻辑运算符，15，358–360
- 条件方法，701–703
- 条件运算符，15，361–363
- Console 类，31，552–553
- Constant 类，35–36
- 常量，41
  - 声明，411–412，506–508
  - 枚举。参见 Enumerations and enum types
  - 表达式，203，395–397
  - 静态字段，512–513
  - 版本控制，512–513
- 构成表达式，237
- 构成类型，496
- 约束
  - 可访问性，116–117
  - 构造类型，162–164
  - 部分类型，483–484
  - 类型参数，475–481
- 构造类型，160–161
  - 绑定与未绑定，162
  - 约束，162–164
  - 成员，493–494
  - 开放与封闭，162
  - 类型参数，161
- 构造函数，41
  - 用于类，42–43
  - 类与结构对比，617–618
  - 默认，141–142，584
  - 在 ID 字符串格式中，757
  - 实例。参见 Instance constructors
  - 调用，254
  - 静态，42，586–589
- Contact 类，311
- 上下文
  - 用于属性，694–696
  - 不安全，710–713
- 上下文关键字，75
- continue 语句
  - 确定性赋值规则，182
  - 用于 do，421
  - 示例，19
  - 用于 for 语句，423
  - 概述，432
  - 用于 while，420
- 契约，接口作为，633
- 反变类型参数，635
- Control 类，564–565
- Control-Z 字符，68
- 转换，195
  - 匿名函数，165–166，219–226，365–366
  - 装箱，156–158，201
  - 常量表达式，203
  - 动态，202,210
  - 枚举，198,207
  - 显式，204–213
  - 表达式，330–331
  - 函数成员，274–275
  - 恒等，196–197
  - 隐式，195–204
  - 标准，213
  - 用户定义，217–219
  - 方法组，226–229
  - null 字面量，199
  - 可空，198–199，207–208，360–361
  - 数字，197，205–207
  - as 运算符，353–355




- 运算符，575–578,759
- 指针的，717–720
- 引用，199–201, 208–210
- 标准，213–214
- 类型参数，203–204, 211–212
- 拆箱，158–160, 210
- 用户定义。参见用户定义转换
  - 变体，636
- Convert 类，207
- Copy 方法，739
- Counter 类，552
- Counter 结构，614
- CountPrimes 类，570
- 协变
  - 数组，200, 629–630
  - 类型参数，635
- cref 特性，742
- 关键执行点，137
- .cs 扩展名，3
- 花括号 ({})
  - 数组，55
  - 集合初始值设定项，310
  - 语法表示法，66
  - 对象初始值设定项，307
- Currency 类型，150
- Current 属性，595
- Customer 类，488–489
## D
- 数据库结构示例
  - 布尔类型，622–623
  - 整数类型，619–621
- DBBool 结构，622–623
- DBInt 结构，619–621
- 十进制数和类型，9–10
  - 加法，338–339
  - 比较运算符，348
  - 除法，335
  - 乘法，333
  - 求反，327
  - 余数运算符，337
  - 减法，341
  - 使用，149–150
- decimal128 类型，149
- 声明指令，88–89
- 声明空间，101
- 声明语句，407–412
- 声明
  - 类，467
    - 基类规范，472–475
    - 主体，481
    - 修饰符，467–471
    - 分部类型，471
    - 类型参数约束，475–481
    - 类型参数，471–472
  - 常量，411–412, 506–508
  - 明确赋值规则，180
  - 委托，672–675
  - 枚举，59, 663–664
  - 事件，559–562
  - 字段，509–510
  - 固定大小缓冲区，733–735
  - 索引器，566–571
  - 实例构造函数，579–580
  - 接口，633–638
  - 方法，520–522
  - 命名空间，103, 454–456
  - 运算符，571–573
  - 顺序，6, 103
  - 概述，101–104
  - 参数，522–525
  - 指针，714
  - 属性，545–546
  - 属性访问器，547
  - 静态构造函数，586–589
  - 结构成员，609
  - 结构，608–609
  - 类型，10, 464
  - 变量，175, 407–411
- 声明可访问性
  - 嵌套类型，499–500
  - 概述，107–109
- 递减运算符
  - 指针，725
  - 后缀，303–305
  - 前缀，328–330
- default 表达式，142
- 默认值
  - 构造函数，141–142, 584
  - switch 语句标签，415-416
  - 值，141, 175-176
    - 类与结构，612-613
    - 表达式，325
  - 保留的成员名，506
  - 成员，23
- #define 指令，87, 89
- 定义分部方法声明，486
- 明确赋值，33, 169, 176-177
  - 固定大小缓冲区，736
  - 初始赋值的变量，177
  - 初始未赋值的变量，177
  - 规则，178-192
- 退化查询表达式，379-380
- Delegate 类，671
- 委托和委托类型，671-672
  - 组合，340, 675
  - 兼容，676
  - 内容，13
  - 转换，165-166, 221-222
  - 声明，672-675
  - 描述，8, 11, 155
  - 相等性，351-352
  - 实例化，676-677
  - 调用，298, 677-680
  - 的成员，107
  - 的 new 运算符，315-317
  - 概述，60-61
  - 移除，342
  - 句法语法，807
- 分隔注释，69-70, 741-742
- 依赖
  - 对基类，473-474
  - 在结构中，611
  - 类型推断，263
- 取决于关系，473-474, 611
- 派生类，22, 25-26
- 析构函数
  - 对于类，50, 589-591
  - 对于类与结构，619
  - 的异常，685
  - 垃圾回收，132-137
  - 在 ID 字符串格式中，757
- 诊断指令，93-94
- Digit 结构，578
- 维度，数组，11, 54, 625, 631-632
- 直接基类，472-473
- 指令
  - 预处理，参见预处理指令
  - using，参见 using 指令
- 直接取决于关系，473-474, 611
- using 语句中的释放，446
- Dispose 方法，591
  - 对于枚举器对象，596, 604-605
  - 对于资源，445-446
- Divide 方法，30
- DivideByZeroException 类，333-334, 683, 685
- 除法运算符，334-335
- DllImport 特性，541
- DLL（动态链接库），541
- do 语句
  - 明确赋值规则，181-182
  - 示例，18
  - 概述，421
- 文档注释，741
  - 的文档文件，741, 754
    - ID 字符串示例，755-759
    - ID 字符串格式，754-756
  - 示例，760-766
  - 概述，741-743
  - 的标签，743-753
  - 的 XML 文件，741-742, 762-765
- 文档生成器，741
- 文档查看器，741
- 域
  - 可访问性，110-113
  - 应用程序，99
- 双引号 (")
  - 字符，80
  - 字符串，80
- double 类型，9-10, 146-149
- DoubleToInt64Bits 方法，334
- 动态绑定
  - 匿名函数，369
  - 概述，234-237
- 动态链接库 (DLL)，541
- 动态内存分配，738-740
- 动态重载决策，275-276
- dynamic 类型，154
  - 转换，202, 210
  - 标识转换，197
  - 概述，166-167
## E
- ECMA-334 标准，1
- EdiBox 类，56-57
- 有效基类，480
- 有效接口集，480
- 元素
  - 数组，53, 171, 628
  - foreach，425-427
  - 指针，723
  - 主表达式，298-301
- #elif 指令，87-88, 91
- Ellipse 类，539
- #else 指令，87, 90-93
- 嵌入语句和表达式
  - 一般规则，186-187
  - 在语法表示法中，66
- 空语句，404-406
- 被包含类型，216
- 包含类型，216
- 文件尾标记，68
- 结束点，400-402
- #endif 指令，91
- #endregion 指令，94
- Entity 类，33-34
- Entry 类，5
- 入口点，99
- 可枚举接口，592
- 迭代器的可枚举对象，596-597
- 枚举和枚举类型
  - 的加法，339
  - 比较运算符，348
  - 转换
    - 显式，207
    - 隐式，198
  - 声明，663-664
  - 描述，8, 11, 663-668
  - 逻辑运算符，356-357
  - 成员，106, 665-668
  - 修饰符，664-665
  - 概述，58-59
  - 的减法，341
  - 句法语法，806-807
  - 的类型，151
  - 值和运算，668-669
- 枚举器接口，592
- 迭代器的枚举器对象，593-596
- foreach 的枚举器类型，425-426
- 等号 (=)
  - 赋值运算符，389
  - 比较，345
  - 运算符 ==，49-50
  - 指针，726
  - 预处理表达式，87
- 相等运算符，15
  - 布尔值，348
  - 委托，351-352
  - 提升的，246-247
  - 和 null，352
  - 引用类型，349-351
  - 字符串，351
- Equals 方法
  - 对匿名类型，319
  - DBBool，623
  - DBInt，621
  - List，42
    - 使用 NaN 值，347
  - Point，761
- #error 指令，94
- Error 属性，553
- ID 字符串格式中的错误字符串，754
- 转义序列
  - 字符，81
  - 词法语法，769
  - 字符串，81
  - Unicode 字符，71-72
- Evaluate 方法，37
- 用户定义转换的求值，215-216
- 事件处理程序，48, 559, 562
- 事件，4
  - 对事件的访问，253
  - 访问器，564-565
  - 赋值运算符，394-395
  - 声明，559-562
  - 示例，42
  - 类似字段，562-564
  - 在 ID 字符串格式中，754, 758-759
  - 实例和静态，565
  - 接口，642
  - 保留的成员名，506
  - 概述，47-49
- 精确参数类型推断，264
- <example> 标签，745
- Exception 类，436, 438, 682-684
- 异常传播，437
- <exception> 标签，745
- 异常变量，438
- 异常
  - 原因，683
  - 的类，685-686
  - 对于委托，677
  - 处理，1, 684-685
  - 概述，681-682
  - 引发，436-437
  - 的 try 语句，438-443
- 感叹号 (!)
  - 比较，345
  - 明确赋值规则，190
  - 逻辑求反，327
  - 运算符 !=，49
  - 指针，726
  - 预处理表达式，87
- 执行
  - 实例构造函数，582-584
  - 顺序，137-138
- 退出块，430
- 外生异常，686
- 展开形式的函数成员，272
- 显式基接口，637
- 显式转换，204-205
  - dynamic，210
  - 枚举，207
  - 可空类型，207-208
  - 数值，205-207
  - 引用，208-210
  - 标准，214
  - 类型参数，211-212
  - 拆箱，210
  - 用户定义，213, 218-219
- 显式接口成员实现，57, 647-650
- explicit 关键字，576-578
- 显式参数类型推断，264
- Expression 类，35-37
- 表达式语句，17, 179, 412-413
- 表达式，231
  - 匿名函数。参见匿名函数
  - 绑定，234-237
  - 布尔，397
  - 强制转换，330-331
  - 分类，231-234
  - 常量，203, 395-397
  - 构成项，237
  - 明确赋值规则，186-191
  - dynamic，166
  - 固定大小缓冲区，735-736
  - 函数成员
    - 参数列表，254-259
    - 类别，250-254
    - 调用，276-278
    - 重载决策，270-275
    - 类型推断，259-270
  - 成员查找，247-250
  - 运算符，238
    - 算术。参见算术运算符
    - 赋值，389-395
    - 逻辑，355-357
    - 数值提升，244-246
    - 重载，240-243
    - 优先级和结合性，238-240
    - 关系，345
    - 移位，343-344
    - 一元，326-331
  - 概述，13-16
  - 中的指针，720-727
  - 预处理，87-88
  - 主表达式。参见主表达式




- 查询，373–375
  - 中的歧义，376
  - 模式，387–389
  - 中的翻译，376–387
  - 语法文法，779–788
  - 树类型，165–166, 222
  - 值，233
- 可扩展标记语言 (XML)，741–742, 762–765
- 扩展方法
  - 示例，541–543
  - 调用，293–297
- Extensions 类，542
- extern 别名，456–457
- 外部构造函数，580, 586
- 外部析构函数，589
- 外部事件，560
- 外部索引器，569
- 外部方法，539–540
- 外部运算符，572
- 外部属性，546

## F

- `\f` 转义序列，81
- false 值，76
- 致命异常，686
- 类似字段的事件，562–564
- 字段，4
  - 声明，509–510
  - 示例，41
  - 在 ID 字符串格式中，754, 756–757
  - 初始化，515, 516, 616–617
  - 实例，26–27, 510–511
  - 概述，26–27
  - 只读，27–28, 511–513
  - 静态，510–511
  - 变量初始值设定项，516–519
  - 易失，514–515
- Fill 方法，629
- 筛选器，442
- Finalize 方法，591
- 终结器，50
- finally 块
  - 明确赋值规则，184–185
  - 用于异常，684
  - 执行，682
  - 与 goto 一起使用，434
  - 与 try 一起使用，438–443
- 固定大小缓冲区
  - 声明，733–735
  - 明确赋值，736
  - 在表达式中，735–736
  - fixed 语句，716, 728–733
- 固定变量，716–717
- 修正类型推断，266–267
- float 类型，9–10, 146–149
- 浮点数
  - 加法，338
  - 比较运算符，346–347
  - 除法，334–335
  - 乘法，332
  - NaN 有效负载，333–334
  - 求反，327
  - 余数运算符，336
  - 减法，340–341
  - 类型，9–10, 146–149
- for 语句
  - 明确赋值规则，182
  - 示例，19
  - 概述，422–423
- foreach 语句
  - 明确赋值规则，185
  - 示例，19
  - 概述，423–429
- 换页转义序列，81
- 前向声明，6
- 碎片化，堆，729
- Free 方法，739
- from 子句，375, 379–387
- FromTo 方法，599–600
- 完全限定名
  - 描述，1, 31
  - 接口成员，645
  - 嵌套类型，499
- 函数成员
  - 参数列表，254–259
  - 在类中，40–50
  - 动态重载决策检查，275–276
  - 重载决策，270–275
  - 概述，250–254
  - 类型推断，259–270
- 函数指针，671
- 函数表示法，241
- 函数，匿名。请参阅匿名函数

## G

- 垃圾回收，1
  - 在应用程序终止时，101
  - 用于析构函数，50
  - 在内存管理中，132–137, 176
  - 与指针，713
  - 用于变量，716
- GC 类，133, 136
- 泛型类和类型，25, 139
  - 匿名对象，318
  - 装箱，156, 613
  - 约束，162, 475–477, 483
  - 声明，467, 473
  - 委托，220
  - 实例类型，492
  - 接口，650–651
  - 成员查找，247
  - 方法，521, 532, 652–653
  - 嵌套，247, 503
  - 重载，275
  - 重写，536
  - 查询表达式模式，387
  - 签名，28
  - 静态字段，26
  - 类型推断，259–261, 267
  - 未绑定，160
- 泛型接口，627–628
- get 访问器
  - 用于特性，695
  - 定义，45
  - 描述，557
  - 使用，547–553
- GetEnumerator 方法
  - 用于 foreach，425
  - 用于迭代器，596–603
- GetEventHandler 方法，565
- GetHashCode 方法
  - 在匿名类型上，319
  - 比较，347
  - DBBool，623
  - DBInt，621
- GetHourlyRate 方法，38
- GetInvocationList 方法，677
- GetNextSerialNo 方法，34
- GetProcessHeap 方法，739
- 全局声明空间，101
- 全局命名空间，105
- goto 语句
  - 明确赋值规则，182
  - 示例，19
  - 用于 switch，416–417, 419
  - 使用，433–434
- switch 语句的主导类型，415, 418
- 文法，65
  - 歧义，287–288
  - 词法。请参阅词法文法
  - 表示法，65–67
  - 语法。请参阅语法文法
  - 用于不安全代码，809–812
- 大于号 (>)
  - 赋值运算符，389
  - 比较，345
  - 指针，716, 721–722, 726
  - 移位运算符，343–344
- Grid 类，570–571
- group 子句，375, 378, 385

## H

- 处理程序，事件，48, 559, 562
- HasValue 属性，152
- 堆，7
  - 访问其函数，738–740
  - 碎片化，729
- HeapAlloc 方法，739
- HeapFree 方法，739
- HeapReAlloc 方法，740
- HeapSize 方法，740
- Hello, World 程序，3
- Hello 类，93
- HelpAttribute 类，61–62, 690
- HelpStringAttribute 类，697
- 十六进制转义序列
  - 用于字符，80
  - 用于字符串，83
- 隐藏
  - 继承成员，102, 125–127, 495
  - 在多继承接口中，644
  - 在嵌套中，124–127, 500
  - 属性，550
  - 在作用域中，120
- Hindley-Milner 风格算法，261
- 水平制表符转义序列，81

## I

- IBase 接口，644, 655, 660
- ICloneable 接口，645–646, 649, 654
- IComboBox 接口，56, 638
- IComparable 接口，646
- IControl 接口，56–57, 638
  - 实现，646
  - 继承，657–659
  - 映射，654–656
  - 成员实现，650
  - 成员名称，645
  - 重新实现，659–660
- ICounter 接口，643
- ICounter 结构，615
- ID 字符串格式
  - 用于文档文件，754–756
  - 示例，755–759
- IDataBound 接口，56–57
- 相同的简单名称和类型名称，286–287
- 标识符
  - 接口，634
  - 词法文法，769–770
  - 规则，72–74
- 标识转换，196–197
- IDerived 接口，655
- IDictionary 接口，648
- IDisposable 接口，136, 428, 445–447, 591, 648
- IDouble 接口，644
- IEnumerable 接口，311, 427–428, 596–597
- IEnumerator 接口，592
- #if 指令，87–88, 90–93
- if 语句
  - 明确赋值规则，180
  - 示例，18
  - 使用，413–414
- IForm 接口，655
- IInteger 接口，643–644
- IL（中间语言）指令，5
- IList 接口，627–628, 643, 647
- IListBox 接口，56, 638, 656
- IListCounter 接口，643
- IMethods 接口，659–661
- 实现分部方法声明，486
- 隐式转换，195–196
  - 匿名函数和方法组，204
  - 装箱，201
  - 常量表达式，203
  - 动态，202
  - 枚举，198
  - 标识，196
  - null 字面量，199
  - 可空，198–199
  - 数值，197
  - 用于隐式转换的运算符，575–578
  - 标准，213
  - 类型参数，203–204
  - 用户定义，204, 217
  - implicit 关键字，575–578
- 隐式类型化数组创建表达式，313
- 隐式类型化迭代变量，423, 427
- 隐式类型化局部变量声明，408–409
- 导入类型，461–463
- 内联方法，61
- In 属性，553
- 不可访问成员，107
- <include> 标记，742, 745–746
- 递增运算符
  - 用于指针，725
  - 后缀，303–305
  - 前缀，328–330
- IndexerNameAttribute，707
- 索引器
  - 访问，253, 300–301
  - 声明，566–571
  - 示例，42
  - 在 ID 字符串格式中，758
  - 接口，642
  - 为其保留的成员名称，506
  - 概述，46–47
  - 中的签名，119
- IndexOf 方法，39–40
- IndexOutOfRangeException 类，300, 685
- 索引，数组，53
- 间接寻址，指针，716, 721
- 推断，类型，259–270
- 无穷大值，147–148
- 继承，22
  - 从基接口，637–638
  - 在类中，25–26, 105, 494–496
  - 在类与结构中的对比，612
  - 通过继承隐藏，102, 125–127, 495
  - 接口，640, 657–659
  - 参数，689
  - 属性，550
- 初始值设定项
  - 数组，55, 630–632
  - 字段，515–516, 616–617
  - 在 for 语句中，422
  - 实例构造函数，580–581
  - 堆栈分配，736–738
  - 变量，516–519, 581
- 初始已赋值变量，169, 177
- 初始未赋值变量，169, 177
- 内联过程，552
- InnerException 属性，683
- 输入产生式，67
- 输入安全类型，636
- 类型推断中的输入类型，263
- 输入不安全类型，636
- 实例构造函数
  - 声明，579–580
  - 默认，584
  - 描述，42
  - 执行，582–584
  - 初始值设定项，580–581
  - 调用，254
  - 可选参数，585–586
  - 私有，584–585
- 实例事件，565
- 实例字段
  - 类，510–511
  - 示例，26–27
  - 初始化，515–516, 519
  - 只读，511–513
- 实例成员
  - 类，496–498
  - 描述，22
  - 受保护访问，113–116
- 实例方法，28, 33–34, 531
- 实例属性，546
- 实例类型，492
- 实例变量，170–171, 510–511
- 实例，21–22
  - 特性，698–699
  - 类型，153
- 实例化
  - 委托，676–677
  - 局部变量，370–373
  - int 类型，9–10
- Int64BitsToDouble 方法，334
- 整数
  - 加法，338
  - 比较运算符，346
  - 除法，334
  - 字面量，76–78
  - 逻辑运算符，356
  - 乘法，332
  - 求反，327
  - 余数，336
  - 在结构示例中，619–621
  - 减法，340
- 整型，9–10, 145–146
- interface 关键字，634
- 接口集，480




- 接口, 4, 633
  - 基, 637–638
  - 主体, 638
  - 声明, 633–638
  - 可枚举, 592
  - 枚举器, 592
  - 泛型, 650–651
  - 实现, 645–647
    - 抽象类, 661
    - 基类, 475
    - 显式成员, 647–650
    - 泛型方法, 652–653
    - 继承, 657–659
    - 映射, 653–656
    - 重新实现, 659–660
    - 唯一性, 650–652
  - 继承自, 637–638
  - 成员, 106, 639–640
    - 访问, 642–644
    - 事件, 642
    - 完全限定名, 645
    - 索引器, 642
    - 方法, 640–641
    - 属性, 641–642
  - 修饰符, 634
  - 概述, 56–57
  - 部分类型, 484–485
  - 结构体, 609
  - 语法, 805–806
  - 类型, 8, 11–13, 155
  - 变体类型参数列表, 635–637
- 中间语言 (IL) 指令, 5
- 内部可访问性, 23, 107
- 驻留, 84
- 互操作属性, 707
- IntToString 方法, 737–738
- IntVector 类, 574
- InvalidCastException 类, 159, 210, 355, 685
- InvalidOperationException 类, 152, 600
- 块中的不变含义, 281–283
- 不变类型参数, 635
- 可调用成员, 247–248
- 调用
  - 委托, 298, 677–680
  - 函数成员, 276–278
  - 实例构造函数, 254
  - 方法, 251
  - 运算符, 254
- 调用表达式, 187, 288–298
- 调用列表, 675, 677
- 被调用成员, 247–248
- IronPython, 236
- is 运算符, 352–353
- isFalse 属性, 622
- IsNaN 方法, 334
- isNull 属性
  - DBBool, 622
  - DBInt, 620
- ISO/IEC 23270 标准, 1
- IStringList 接口, 639
- isTrue 属性, 622
- 迭代语句, 420
  - do, 421
  - for, 422–423
  - foreach, 423–429
  - while, 420–421
- foreach 中的迭代变量, 423–424
- 迭代器, 592
  - 块, 403
  - 可枚举接口, 592
  - 用于...的可枚举对象, 596–597
  - 枚举器接口, 592
  - 用于...的枚举器对象, 593–596
  - 实现示例, 597–603
  - yield 类型, 592
- ITest 接口, 119–120
- ITextBox 接口, 56, 638, 645–647, 650, 656

## J

- 不规则数组, 54
- JIT (即时) 编译器, 5
- join 子句, 380–384
- 跳转语句
  - break, 431
  - continue, 432
  - goto, 433–434
  - 概述, 429–431
  - return, 435
  - throw, 436–437
- 即时 (JIT) 编译器, 5

## K

- KeyValuePair 结构体, 613
- 关键字
  - 词法语法, 770
  - 列表, 74–75

## L

- Label 类, 551–552
- 标签声明空间, 102–103
- 标签语句
  - 用于 goto, 433–434
  - 概述, 406–407
  - 用于 switch, 181, 415–419
- 左结合运算符, 239
- 左移运算符, 343–344
- 数组长度, 53, 625, 631–632
- 小于号 (<)
  - 赋值运算符, 389
  - 比较, 345
  - 指针, 726
  - 移位运算符, 343–344
- let 子句, 380–384
- 词法语法, 67, 767
  - 注释, 69–70, 768
  - 标识符, 769–770
  - 关键字, 770
  - 行终止符, 68–69, 767
  - 字面量, 771–773
  - 运算符和标点符号, 773
  - 预处理指令, 774–777
  - 标记, 769
  - Unicode 字符转义序列, 769
  - 空白字符, 70–71, 769
- 词法结构, 65
  - 语法, 65–67
    - 词法。参见 词法语法
    - 语法。参见 语法
  - 词法分析, 67–71
  - 预处理指令, 85–87
    - 条件编译, 87, 90–93
    - 声明, 88–89
    - 诊断, 93–94
    - 行, 95–96
    - pragma, 96–97
  - 预处理表达式, 87–88
  - 区域, 94
  - 程序, 65
  - 标记, 71
    - 标识符, 72–74
    - 关键字, 74–75
    - 字面量, 76–84
    - 运算符, 84–85
    - Unicode 字符转义序列, 71–72
- 库, 4, 541
- 提升转换, 215
- 提升运算符, 246–247
- #line 指令, 94
- #line default 指令, 96
- 行指令, 95–96
- 换行符字符, 69
- #line hidden 指令, 96
- 行分隔符字符, 69
- 行终止符, 68–69, 767
- List 类, 40–50
- <list> 标签, 746–747
- ListChanged 方法, 48
- 语句列表, 403–404
- 字面量
  - 布尔, 76
  - 字符, 80–81
  - 在常量表达式中, 395
  - 转换, 199
  - 定义, 76
  - 整数, 76–78
  - 词法语法, 771–773
  - null, 84
  - 在主表达式中, 279
  - 实数, 78–79
  - 简单值, 144
  - 字符串, 81–84
- 局部常量声明, 17, 411–412
- 局部变量声明空间, 103
- 局部变量
  - 声明, 17, 407–411
  - 实例化, 370–373
  - 在方法中, 32–33
  - 作用域, 124–125
  - 使用, 173–175
- lock 语句
  - 确定性赋值规则, 186
  - 示例, 21
  - 概述, 443–445
- 逻辑运算符
  - AND, 15
  - 对于布尔值, 357
  - 条件, 358–360
  - 对于枚举, 356–357
  - 对于整数, 356
  - 否定, 327–328
  - OR, 15
  - 概述, 356–357
  - 移位, 344
  - XOR, 15
- LoginDialog 类, 561
- long 类型, 9–10
- 成员查找, 247–250
- 下界类型推断, 264–265
- 左值, 193

## M

- Main 方法
  - 用于启动, 99–100
  - 用于静态构造函数, 587–588
- 映射
  - 接口, 653–656
  - 指针和整数, 719
- Math 类, 334
- 成员, 4, 22–23, 105
  - 访问, 23, 107, 496
  - 可访问性域, 110–113
  - 约束, 116–117
  - 声明的可访问性, 107–109
  - 接口, 642–644
  - 指针, 721–722
  - 在主表达式中, 283–288
  - protected, 113–116
  - 可访问性, 23–24
  - 数组, 106, 628
  - 类, 106, 490–492
    - 访问修饰符, 496
    - 构成类型, 496
    - 构造类型, 493–494
    - 继承, 494–496
    - 实例类型, 492
    - 嵌套类型, 498–504
    - new 修饰符, 496
    - 保留名称, 504–506
    - 静态和实例, 496–498
  - 委托, 107
  - 枚举, 106, 665–668
  - 函数，参见 函数成员
  - 继承, 102, 105, 125–127, 494–496
  - 接口, 106, 639–640
    - 访问, 642–644
    - 事件, 642
    - 显式实现, 57, 647–650
    - 完全限定名, 645
    - 索引器, 642
    - 方法, 640–641
    - 属性, 641–642
  - 查找, 247–250
  - 命名空间, 105, 463–464
  - 部分类型, 485
  - 指针, 721–722
  - 结构体, 105–106, 609
- 内存
  - 自动管理, 132–137, 176
  - 动态分配, 738–740
- Memory 类, 738–740
- 事件导致的内存泄漏, 561
- Message 属性, 683
- 元数据, 5
- 方法组转换
  - 隐式, 204
  - 概述, 226–229
  - 类型推断, 269
- 方法, 4, 28
  - 抽象, 35, 539–540
  - 正文, 32–33, 544
  - 条件, 701–703
  - 声明, 520–522
  - 扩展, 541–543
  - 外部, 539–540
  - 在 ID 字符串格式中, 754, 757–758
  - 实例, 28, 33–34, 531
  - 接口, 640–641
  - 调用, 251, 288–298
  - 在 List 中, 42
  - 重载, 38–40
  - 重写, 35, 535–537
  - 参数, 29–32
    - 数组, 528–531
    - 声明, 522–525
    - 输出, 526–527
    - 引用, 525–526
    - 值, 525
  - 部分, 486–490, 541
  - 密封, 537–538
  - 静态, 28, 33–34, 531
  - 虚拟, 35–38, 532–534
- 减号 (-) 运算符, 327
- 减号 (-)
  - 赋值运算符, 389
  - 自减运算符, 303–305, 328–330
  - 指针, 716, 721–722, 725
  - 减法, 340–342
- 修饰符
  - 类, 467–471
  - 枚举, 664–665
  - 接口, 634
  - 部分类型, 483
  - 结构体, 609
- 取模运算符, 336–337
- 最派生方法实现, 532–533
- 最包容类型, 216
- 最具体运算符, 215
- Move 方法, 760–761
- 可移动变量
  - 描述, 716–717
  - 固定地址, 728–733
- MoveNext 方法, 426
  - 枚举器对象, 451, 593–595
  - Stack, 599
  - Tree, 603–604
- 多维数组, 11, 54, 625, 631–632
- 多用途属性类, 688
- 多重继承, 56–57, 644
- 多条语句, 402–403
- 乘法运算符, 15, 332–333
- 乘法运算符, 15
- Multiplier 类, 60–61
- Multiply 方法, 60
- 互斥锁, 443–445

## N

- \n 转义序列, 81
- 命名常量。参见 枚举和枚举类型
- 命名参数, 690–691
- 名称
  - 匿名类型, 318–319
  - 绑定, 490
  - 完全限定, 131
    - 接口成员, 645
    - 嵌套类型, 499
  - 隐藏, 124–127
  - 方法, 521
  - 保留, 504–506
  - 简单
    - 在主表达式中, 279–283
    - 和类型名称, 286–287
  - 变量, 170
- namespace 关键字, 454
- 命名空间, 3–4, 453
  - 别名, 456–461, 464–466
  - 编译单元, 453–454
  - 声明, 103, 454–456
  - 中的 using 指令, 457–463
  - 中的完全限定名, 131
  - 在 ID 字符串格式中, 754
  - 成员, 105, 463–464
  - 概述, 127–130
  - 目的, 104
  - 语法, 793–794
  - 类型声明, 464
- NaN (非数字) 值
  - 原因, 147, 149
  - 异常, 682
  - 在浮点比较中, 347
  - 有效负载结果, 333–334
- 否定
  - 逻辑, 327–328
  - 数值, 327
- 嵌套数组初始化器, 631–632
- 嵌套块, 104
- 嵌套类, 468
- 嵌套成员, 110–111



嵌套作用域，120
嵌套类型，498-499
可访问性，499-503
描述，464
完全限定名称，499
在泛型类中，503
被包含的成员访问，502-503
部分，482
对 this 的访问，500-501
嵌套
别名，460
使用 break，431
注释，70
通过隐藏，124-125，500
对象初始化器，308
换行转义序列，81
new 修饰符
类成员，496
类，468
委托，672
接口成员，640
接口，634
new 运算符
匿名对象，317-319
数组，53，55，312-315
集合初始化器，310-312
构造函数，43
委托，315-317
隐藏方法，126
对象初始化器，307-310
对象，305
结构，52
禁止贯穿规则，416-417
无副作用约定，552
非嵌套类型，498
不可空值类型，152
非虚方法，35
非终结符，65-66
正规形式函数成员，272
规范化形式 C，73
Not-a-Number (NaN) 值
原因，147，149
异常，682
在浮点比较中，347
负载结果，333-334
记法，语法，65-67

NotSupportedException 类，593
空合并运算符，360-361
事件的空字段，48
空字面量，84，152，199
空指针，714
字符串空终止，733
空值
用于数组元素，54
在类与结构中，613
转义序列，81
垃圾收集器，134
可空布尔逻辑运算符，357
可空类型，11-12
内容，13
转换
显式，207-208
隐式，198-199
运算符，353-355
描述，8
与相等运算符，352
概述，151-152
NullReferenceException 类
数组访问，300
使用 as 运算符，355
委托创建，316
委托调用，678
描述，685
foreach 语句，427
throw 语句，436
拆箱转换，159
数值转换
显式，205-207
隐式，197
数值提升，244-246
## O
object 类，141，154
对象变量，12-13
对象
创建表达式
确定性赋值规则，187
new 运算符，305-307
释放，22
描述，139
初始化器，307-310
作为实例类型，153

- Obsolete 属性，705–706
- 八进制字面量，77
- OnChanged 方法，42，48
- 一维数组，54
- 开放类型，162
- 操作数，13，238
- Operation 类，35–36
- 运算符记法，241
- 运算符，13，42，49，84–85
  - 算术。参见 Arithmetic operators
  - 赋值运算符，16，389
    - 复合，393–394
    - 事件，394–395
    - 简单，390–393
  - 二元。参见 Binary operators
  - 条件，361–363
  - 转换，575–578，759
  - 声明，571–573
  - 枚举，668–669
  - 在 ID 字符串格式中，759
  - 调用，254
  - 词法语法，773
  - 提升，246–247
  - 逻辑，355–357
  - 空合并，360–361
  - 数值提升，244–246
  - operator !=，49
  - operator ==，49–50
  - 重载，240–243
  - 概述，238
  - 优先级和结合性，238–240
  - 关系。参见 Relational operators
  - 移位，343–344
  - 类型测试，352–353
  - 一元。参见 Unary operators
- 可选参数，522，585–586
- 语法记法中的可选符号，66
- OR 运算符，15
- 顺序
  - 声明，103
  - 执行，137–138
- orderby 子句，375，380–384
- Out 属性，553
- 外部变量，369–373

- OutOfMemoryException 类，313，316，339，685
- 输出参数，30，173，526–527
- 输出安全类型，636
- 类型推断中的输出类型，263
- 输出不安全类型，636
- 溢出检查上下文，322–325，443
- OverflowException 类
  - 加法，338
  - 数组，313
  - checked 运算符，323–324
  - decimal 类型，150
  - 描述，686
  - 除法，335
  - 自增和自减运算符，329
  - 乘法，332–333
  - 余数运算符，336
- 重载解析
  - 匿名函数，368
  - 函数成员，270–275
- 重载运算符，13
  - 目的，238
  - 移位，343
- 重载
  - 索引器，47
  - 方法，38–40
  - 运算符，240–243
  - 签名，38，117–120
- 被重写的基础方法，535
- Override 事件，566
- Override 索引器，567
- Override 方法，535–537
- 重写
  - 事件声明，566
  - 方法，35
  - 属性访问器，46，557
  - 属性声明，557–558

## P
- 指针填充，727
- Paint 方法，56，539
- Pair 类，24
- 成对声明，575
- <para> 标签，748
- 段落分隔符字符，69

<param> 标签，742,748
参数列表，变体类型，635-637
参数
  匿名函数，365
  数组，528-531
  属性，690-691
  入口点，99
  函数成员调用，255-256
  索引器，46-47，567-568
  实例构造函数，581，585-586
  方法，29-32
    声明，522-525
    类型，524-531
  可选，585-586
  输出，173，526-527
  在重载中，117-118
  引用，172，525-526
  类型。参见 Type parameters
  值，171,525
<paramref> 标签,749
params 修饰符，31-32，528-531
括号 ()
  匿名函数,365
  在语法记法中,66
  在 ID 字符串格式中,755
  用于运算符优先级,240
带括号的表达式,283
部分方法,541
partial 修饰符,471
  接口,634
  结构,609
  类型,481-482
部分类型,471
  属性,482-483
  基类,484
  基接口,484
  成员,485
  方法,486-490
  修饰符,483
  名称绑定,490
  概述,481-482
  类型参数和约束,483-484
模式，查询表达式,387-389
百分号 (%)
  赋值运算符,389
  余数运算符,336-337

句点 (.)
  基访问,302
  成员,105
<permission> 标签,749
允许的用户定义转换,214-215
阶段，类型推断,262
加号 (+) 运算符,326
加号 (+)
  加法,337-340
  赋值运算符,389
  自增运算符,303-305,328-330
  指针,725
Point 类
  基类,25
  坐标,308
  声明,22
  实例化对象,51
  属性,554
  源代码,760-762
Point 结构,611-612
  赋值运算符,391-392
  默认值,613
  字段初始化器,616-618
  实例化对象,51-52
Point3D 类,25
指针
  算术,725-726
  数组,719-720
  转换,717-720
  元素访问,723
  在表达式中,720-727
  用于固定变量,728-733
  函数,671
  间接寻址,716,721
  成员访问,721-722
  运算符
    取地址,724-725
    比较,726
    自增和自减,725
    sizeof,727
  类型,713-716
  不安全,7,709
  变量,716-717
多态性,22,26
Pop 方法,4-5
位置参数,690-691

后缀自增和自减运算符，303-305

#pragma 指令，96

#pragma warning 指令，96-97

运算符优先级，13，238-240

前缀自增和自减运算符，328-330

预处理指令
条件编译，87，90-93
声明，88-89
诊断，93-94
词法语法，774-777
行，95-96
概述，85-87
pragma，96-97
预处理表达式，87-88
区域，94

预处理表达式，87-88

主表达式
匿名方法，326
checked 和 unchecked 运算符，322-325
默认值，325
元素访问，298-301
形式，278-279
调用，288-298
其中的字面量，279
成员访问，283-288
new 运算符
匿名对象，317-319
数组，312-315
集合初始化器，310-312
委托，315-317
对象初始化器，307-310
对象，305-307
带括号，283
后缀自增和自减运算符，303-305
其中的简单名称，279-283
其中的 this 访问，301-302
typeof 运算符，319-322

主运算符，14
PrintColor 方法，58
私有可访问性，23-24,107
私有构造函数，584-585
产生式，语法，65
Program 类，47，602-603，614-615
程序结构，4-6
程序，4，65
投影初始化器，319
提升，数值，244-246
传播，异常，437
属性，4
访问，252
可访问性，555-556
自动实现，553-555
声明，545-546
示例，42
在 ID 字符串格式中，754,758
索引器，568
接口，641-642
保留的成员名称，504-505
概述，43-46
静态和实例，546
属性访问器，46
声明，547
概述，547-553
类型，553
受保护可访问性，23-24
声明，107
实例成员，113-116
内部，23-24，107
公共可访问性，23-24,107
标点符号
词法语法，773
列表，84-85
PurchaseTransaction 类，92
Push 方法，4

## Q
限定符，别名，464-466
查询表达式
其中的歧义，376
概述，373-375
模式，387-389
其中的转换，376-387
问号 (?)
空合并运算符，360-361
三元运算符，191，361-362
字符的引号 ('"')，80-81



## R
- \r 转义序列，81
- 范围变量，375，379
- 数组的秩，54，625-626
- 可达性
  - 块，401
  - do 语句，421
  - for 语句，424
  - 带标签语句，406-407
  - 概述，400-402
  - return 语句，435
  - 语句列表，403
  - throw 语句，437
  - while 语句，420-421
- 只读字段，27-28，511-513
- 只读属性，45，549-550，554
- 读写属性，45，549-550
- readonly 修饰符，27，511
- ReadOnlyPoint 类，554
- 读取，易失性，514
- 实数字面量，78-79
- ReAlloc 方法，739
- 建议的注释标签，743-753
- Rectangle 类，308-309
- Rectangle 结构，392
- ref 修饰符，30
- 引用转换
  - 显式，208-210
  - 隐式，199-201
- 引用参数，29-30，172，525-526
- 引用类型，6-8，152-153
  - 数组，53，155
  - 类，153-154
  - 约束，476
  - 委托，155
  - 动态，154
  - 相等运算符，349-351
  - 接口，155
  - 对象，154
  - 字符串，154
- 引用，139
  - 按引用传递参数，29-30
  - 变量，192-193
- 引用静态类类型，470-471
- 引用目标类型，指针，713
- 区域指令，94
- 常规字符串字面量，81-82
- 接口重新实现，659-660
- 关系运算符
  - 布尔值，348
  - 十进制数，348
  - 委托，351-352
  - 描述，15
  - 枚举，348
  - 整数，346
  - 提升的，247
  - 概述，344-345
  - 引用类型，349-351
  - 字符串，351
- 释放语义，514
- 余数运算符，336-337
- <remarks> 标签，750
- 移除访问器
  - 特性，695
  - 事件，49，564
- RemoveEventHandler 方法，565
- 移除委托，342
- 必需参数，522
- 保留特性，699-700
  - AttributeUsage，700
  - Conditional，701-705
  - Obsolete，705-706
- 类成员的保留名称，504-506
- Reset 方法，604
- 解析
  - 函数成员，270-275
  - 运算符重载，38，243
- 资源，using 语句，445-449
- return 语句
  - 明确赋值规则，182-183
  - 示例，19
  - 方法，33
  - 概述，435
  - 带 yield，449-452
- 返回类型
  - 入口点，100
  - 推断的，267-269
  - 方法，28，521-522
- <returns> 标签，750
- 右结合运算符，239
- 右移运算符，343-344

## S
- 舍入，150
- 明确赋值规则，178-192
- 枚举器对象的运行状态，593-596
- 运行时过程
  - 参数列表求值，257-259
  - 数组创建，313
  - 特性实例检索，699
  - 绑定，235
  - 委托创建，316
  - 函数成员调用，276-277
  - 递增和递减运算符，304
  - 对象创建，306-307
  - 前缀递增和递减操作，329
  - 拆箱转换，160
- 运行时类型，35，532
- RuntimeWrappedException 类，439
- sbyte 类型，9
- 作用域
  - 别名，459-460
  - 特性，694
  - 与声明空间，101
  - 局部变量，410
  - 用于名称隐藏，124-127
  - 概述，120-124
- 密封访问器，557
- 密封类，469，474-475
- 密封事件，566
- 密封索引器，567
- 密封方法，537-538
- sealed 修饰符，469，537-538
- 特性的节，692
- <see> 标签，751
- <seealso> 标签，751-752
- select 子句，375，378，384-385
- 选择语句，413
  - if，413-414
  - switch，414-419
- 分号 (;)
  - 访问器，548
  - 接口标识符，642
  - 方法体，544
  - 命名空间声明，454
- 查询表达式中的序列，375
- set 访问器
  - 用于特性，695
  - 定义，45
  - 描述，557
  - 使用，547-550
- SetItems 方法，56
- SetNextSerialNo 方法，34
- SetText 方法，56
- Shape 类，539
- 移位运算符
  - 描述，15
  - 概述，343-344
- 短路逻辑运算符，358
- short 类型，9-10，144
- ShowHelp 方法，62
- 副作用
  - 与访问器，552
  - 与执行顺序，137-138
- 签名
  - 匿名函数，365-366
  - 索引器，568
  - 方法，28，521
  - 运算符
    - 二元，575
    - 转换，578
    - 一元，573
  - 在重载中，38，117-120
- 有符号整数，8-9
- 简单赋值
  - 明确赋值规则，188
  - 运算符，389
  - 概述，390-393
- 简单表达式赋值规则，186
- 简单名称
  - 在主表达式中，279-283
  - 与类型名称，286-287
- 简单类型，8，140-144
- 一维数组
  - 定义，625
  - 示例，54
  - 初始值设定项，631
- 单行注释，69-70，741-742
- 字符的单引号 (')，80-81
- 单次使用特性类，688
- SizeOf 方法，739
- sizeof 运算符，727
- 斜杠 (/)
  - 赋值运算符，389
  - 注释，69-70，741-742
  - 除法，334-335
- Slice 方法，542-543
- 源文件
  - 编译，6
  - 描述，65
  - Point 类，760-762
- 转换中的源类型，215
- SplitPath 方法，527
- SqlBoolean 结构，621
- SqlInt32 结构，621
- 方括号 ([])
  - 数组，11，54
  - 特性，692
  - 索引器，46
  - 指针，716，723
- Square 方法，60
- Squares 类，33
- 堆栈
  - 分配，736-738
  - 堆栈上的值，7
- Stack 类，4-5，597-598
- stackalloc 运算符，716，736-738
- StackOverflowException 类，686，737
- 标准转换，213-214
- 应用程序启动，99-100
- 语句列表，403-404
- 语句，399-400
  - 块，402-404
  - checked 和 unchecked，443
  - 声明，407-412
  - 明确赋值规则，179
  - 空，404-406
  - 结束点和可达性，400-402
  - 表达式，17，179，412-413
  - 在语法表示法中，66
  - 迭代，420
    - do，421
    - for，422-423
    - foreach，423-429
    - while，420-421
  - 跳转，429-431
    - break，431
    - continue，432
    - goto，433-434
    - return，435
    - throw，436-437
  - 带标签的，406-407
  - lock，443-445
  - 概述，16-21
  - 选择，413
    - if，413-414
    - switch，414-419
  - 语法文法，788-793
  - try，438-443
  - using，445-449
  - yield，449-452
- 状态，明确赋值，178
- 静态绑定，234-235
- 静态类，470-471
- 静态构造函数，42
  - 在类与结构中，619
  - 概述，586-589
- 静态事件，565
- 静态字段，26，510-511
  - 用于常量，512-513
  - 初始化，515-519
  - 只读，511-513
- 静态成员，22，496-498
- 静态方法，28
  - 垃圾回收，133
  - 与实例，33-34，531
- static 修饰符，470-471
- 静态属性，546
- 静态变量，170，510-511
- 状态代码，终止，100
- String 类，39-40，154
- string 类型，9，154
- StringFromColor 方法，667
- StringListEvent 方法，639
- 字符串
  - 串联，339
  - 相等运算符，351
  - 字面量，81-84
  - null 终止，733
  - switch 控制类型，418
- 结构
  - 赋值，612
  - 装箱和拆箱，613-616
  - 与类，610-619
  - 构造函数，617-618
  - 声明，608-609
  - 默认值，612-613
  - 析构函数，619
  - 示例
    - 数据库布尔类型，622-623
    - 数据库整数类型，619-621
  - 中的字段初始值设定项，616-617
  - 继承，612
  - 实例变量，171
  - 接口实现（由结构），57
  - 成员，105-106，609
  - 概述，50-53，607
  - 语法文法，803-804
  - 中的 this 访问，616
  - 类型，6，8，10-11，143
  - 值语义，610-612
- 减法运算符，340-342
- 数字后缀，76-79
- <summary> 标签，742，752
- SuppressFinalize 方法，101
- 挂起状态，593-596
- Swap 方法，29
- switch 语句
  - 明确赋值规则，180
  - 示例，18
  - 概述，414-419
  - 可达性，402
- 语法文法，67
  - 数组，804-805
  - 特性，807-809
  - 基本概念，777
  - 类，794-803
  - 委托，807
  - 枚举，806-807
  - 表达式，779-788
  - 接口，805-806
  - 命名空间，793-794
  - 语句，788-793
  - 结构，803-804
  - 类型，777-779
  - 变量，779
- 系统级异常，682
- System 命名空间，143

## T
- \t 转义序列，81
- 制表符转义序列，81
- 注释标签，743-753
- 转换中的目标类型，215
- 目标
  - goto，433-434
  - 跳转，430
- 终结符，65-66
- 应用程序终止，100-101
- 行终止符，68-69，767
- 三元运算符，238，361-363
- TextReader 类，449
- TextWriter 类，449
- this 访问
  - 类与结构，616
  - 索引器，46
  - 实例构造函数，585-586
  - 嵌套类型，500-501
  - 概述，301-302
  - 属性，546
  - 静态方法，33
- 线程安全委托，677
- 三维数组，54
- 抛出点，437
- throw 语句
  - 明确赋值规则，182
  - 示例，20
  - 用于异常，683
  - 概述，436-437
- 波浪号 (~)
  - 按位求补，328
  - 转换，759
- 时间，绑定，235
- ToInt32 方法，542
- 标记，71
  - 标识符，72-74
  - 关键字，74-75



## T

- 词法语法，769
- 字面量，76-84
- 运算符，84-85
- Unicode 字符转义序列，71-72
- ToString 方法，339
  - 与装箱，614-615
- DBBool，623
- DBInt，621
- Point，761-762
- Translate 方法，761
- 查询表达式中的转换，376-387
- 查询表达式中的透明标识符，377，385-387
- Tree 类，602-603
- 树类型，表达式，165-166
- Trig 类，585
- 真值，76
- try 语句
  - 明确赋值规则，183-185
  - 示例，20
  - 用于异常，684-685
  - 与 goto 一起使用，434
  - 概述，438-443
- TryParse 方法，527
- 二维数组
  - 分配，54
  - 初始化表达式，631
- 类型转换，59
- 类型推断，259-270
- 类型名称，127-130
  - 完全限定，131
  - 相同，286-287
- 类型参数，139
  - 类声明，24-25，471-472
  - 约束，475-481
  - 转换，211-212
  - 隐式转换，203-204
  - 概述，164-165
  - 分部类型，483-484
- 类型安全设计，1
- 类型测试运算符
  - as，353-355
  - 描述，15
  - is，352-353
- TypeInitializationException 类，684，686
- typeof 运算符
  - 与指针一起使用，713
  - 主要表达式，319-322
- `<typeparamref>` 标记，753
- `<typeparamref>` 标记，753
- 类型
  - 别名，456-461
  - 特性参数，691
  - 装箱和拆箱，156-158
  - 构造类型，160-164，493-494
  - 声明，10，464
  - 动态类型，166-167
  - 在 ID 字符串格式中，754-756
  - 导入，461-463
  - 实例，492
  - 嵌套，464，498-504
  - 可为 null。参见可空类型
  - 概述，6-13，139
  - 分部。参见分部类型
  - 指针。参见指针
  - 引用。参见引用类型
  - 句法语法，777-779
  - 基础类型，58-59，151
  - 值。参见值类型

## U

- uint 类型，10
- ulong 类型，10
- 一元运算符，326
  - 强制转换表达式，330-331
  - 描述，1，4，238
  - 在 ID 字符串格式中，759
  - 提升的，246
  - 减号，327
  - 数值提升，244
  - 重载决策，242-243
  - 可重载，240-241
  - 概述，573-574
  - 加号，326
  - 前缀递增和递减，328-330
- 未赋值变量，177
- 未绑定类型，160，162
- 拆箱转换
  - 描述，210
  - 概述，158–160
- 拆箱操作
  - 在类与结构中，613–616
  - 示例，12
- unchecked 语句
  - 明确赋值规则，179
  - 示例，20
  - 概述，443
  - 在主要表达式中，322–325
- #undef 指令，87–89
- 未定义的条件编译符号，87
- 基础类型
  - 枚举，58–59，664
  - 可空类型，151
- 用于标识符的下划线字符（_），72–74
- Unicode 字符
  - 转义序列，71–72
  - 词法语法，67，769
  - 用于字符串，9
- Unicode 规范化形式 C，73
- 统一类型系统，1
- 唯一性
  - 别名，466
  - 接口实现，650–652
- 非托管类型，713
- 不可达语句，400
- 不安全代码，709
  - 上下文，710–713
  - 动态内存分配，738–740
  - 固定大小缓冲区，733–736
  - fixed 语句，728–733
  - 语法扩展，809–812
  - 指针
    - 数组，719–720
    - 转换，717–720
    - 在表达式中，720–727
  - 支持，7
  - 类型，713–716
  - 堆栈分配，736–738
  - unsafe 修饰符，710–713
- 无符号整数，8–10
- 解包非可空值类型，152
- 上限类型推断，265–266
- 用户定义转换，214
  - 计算，215–216
  - 显式，213，218–219
  - 隐式，204，217
  - 提升运算符，215
  - 概述，575–578
  - 允许的，214–215
- 用户定义运算符
  - 候选，243
  - 条件逻辑，359–360
- ushort 类型，10
- using 指令
  - 用于别名，458–461
  - 明确赋值规则，185–186
  - 示例，21
  - 用于导入类型，461–463
  - 概述，445–449，457
  - 用途，3

## V

- \v 转义序列，81
- Value 方法，620
- 值参数，29，171，525
- Value 属性，152
- `<value>` 标记，752
- 值类型
  - bool，150–151
  - 约束，476
  - 内容，13
  - decimal，149–150
  - 默认构造函数，141–142
  - 描述，8
  - 枚举，151
  - 浮点，146–149
  - 整数，145–146
  - 可空，151–152
  - 概述，140–141
  - 简单，143–144
  - 存储，7
  - struct，143
- 值
  - 数组类型，626
  - 类与结构，610-612
  - 默认，141
  - 类与结构，612-613
  - 初始化，175-176
  - 枚举，668-669
  - 表达式，233
  - 字段，510-511
  - 局部常量，412
  - 变量，169，175-176，408-409
- ValueType 类，141，612
- VariableReference 类，35-36
- 变量，169
  - 匿名函数，369-373
  - 数组元素，171
  - 声明，175，407-411
  - 默认值，175-176
  - 明确赋值。参见明确赋值
  - 固定地址，728-733
  - 固定和可移动，716-717
  - 初始化表达式，516-519，581
  - 实例，170-171，510-511
  - 局部，173-175
  - 在方法中，32-33
  - 名称，170
  - 输出参数，173
  - 概述，12-13
  - 查询表达式，375，379
  - 引用参数，172
  - 引用，192-193
  - 作用域，124-125，410
  - 静态，170，510-511
  - 句法语法，779
  - 值参数，171
- 变体类型参数列表，635-637
- 逐字标识符，74
- 逐字字符串字面量，81-83
- 版本控制
  - 常量的，512-513
  - 描述，1
- 竖线（|）
  - 赋值运算符，389
  - 明确赋值规则，189-190
  - 逻辑运算符，355-359
  - 预处理表达式，87
- 垂直制表符转义序列，81
- 烦人异常，686
- 查看器，文档，741
- 虚拟访问器，46，557-559
- 虚拟事件，566
- 虚拟索引器，567
- 虚拟方法
  - 描述，236
  - 概述，35-38
  - 使用，532-534
- 作用域中的可见性，120，124
- void 类型和值
  - 入口点方法，100
  - 事件，564
  - 指针，714
  - 返回，28，33
  - 与 typeof 一起使用，320
- 易失字段，514-515

## W

- WaitForPendingFinalizers 方法，136
- #warning 指令，94
- 警告，预处理指令，96-97
- where 子句
  - 查询表达式，380-384
  - 类型参数约束，163，476
- while 语句
  - 明确赋值规则，181
  - 示例，18
  - 概述，420-421
- 空白
  - 在注释中，742
  - 定义，70-71
  - 在 ID 字符串格式中，754
  - 词法语法，769
- Win32 组件互操作性，707
- workCompleted 方法，47
- Worker 类，47-48
- 包装非可空值类型，152
- Write 方法，31
- 只写属性，45，549–550，554
- WriteLine 方法，3，31，136
- 写入，易失，514

## X

- \x 转义序列，80
- XAttribute 类，696–697
- XML（可扩展标记语言），741–742，762–765
- XOR 运算符，15

## Y

- yield 语句
  - 明确赋值规则，186
  - 示例，20
  - 概述，449–452
  - yield break，594–595
  - yield return，594–595
- yield 类型迭代器，592

## Z

- 零值，146–148

