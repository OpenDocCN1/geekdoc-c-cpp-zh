
图 1-4 显示了如何在代码中使用注释。程序涵盖了 10 行，但只有 7 行是可执行的 C# 程序，包括包含大括号的行以及行注释。当程序运行时，唯一起作用的是显示 Message 的阴影行。

```
/* 此程序用于演示使用注释 */
ClassWithOneLine
{
    static void Main()
    {
        // 下一行写入
        System.Console.WriteLine("Message");
    } // Main 结束
} // ClassWithOneLine 结束
```

图 1-4 使用注释

# 使用 命名空间

程序可以包含任意数量的语句。例如，图 1-5 中的程序产生了图 1-6 所示的三行输出。（为了获得输出，你需要了解如何编译和执行程序，你将在本书的后续部分学习。）分号分隔了每个程序语句。

```csharp
class ThreeLinesOutput
{
    static void Main()
    {
        System.Console.WriteLine("Line one");
        System.Console.WriteLine("Line two");
        System.Console.WriteLine("Line three");
    }
}
```

图 1-5 一个产生三行输出的程序![](7516c1fecf7bbbe7afb10cf209b17ae3_45_0.png)

图 1-6 ThreeLines 程序的输出

# 第 1 章 使用 C# 的第一个程序

图 1-6 显示了 ThreeLines 的输出。按任意键继续的提示并不是程序的一部分；它是 Visual Studio 添加的，但如果你从命令行运行程序，它就不会出现。

图 1-5 中的程序显示大量的重复代码——`System.Console.WriteLine` 出现了三次。当你需要重用同一命名空间中的类时，可以通过输入指示类类的 using 子句或 using 指令来缩短语句。如果你在类定义之前输入 `using System;`，编译器在遇到 Console 类时就会使用 System 命名空间。图 1-7 程序的输出与图 1-5 相同，在图 1-5 中 System 在每个 WriteLine() 语句中重复出现。

```csharp
using System;
class ThreeLinesOutput
{
    static void Main()
    {
        Console.WriteLine("Line one");
        Console.WriteLine("Line two");
        Console.WriteLine("Line three");
    }
}
```

图 1-7 使用 using; 子句产生三行输出的程序

尽管在 C# 的旧版本中这不是选项，但你可以通过在程序顶部插入 `using static System.Console;` 来进一步减少输入。因此，图 1-8 中的程序在其输出语句中只使用了 `WriteLine()` 方法，并且程序运行正常（你已经在 Main() 方法头中看到了 static 一词。记住，static 表示在不创建对象的情况下使用方法。你将在第 7 章学习更多关于 static 关键字的使用）。图 1-8 所示的更简单风格将用于本书剩余部分的程序。

```csharp
using static System.Console;
class ThreeLinesOutput
{
    static void Main()
    {
        WriteLine("Line one");
        WriteLine("Line two");
        WriteLine("Line three");
    }
}
```

图 1-8 使用 using static System.Console; 子句产生三行输出的程序

两个事实一个谎言

通过添加注释和使用 System 命名空间改进程序

1. 行注释以双斜杠 (//) 开头，并在当前行结束。
2. 块注释可以跨越任意行。
3. 当你需要反复使用同一命名空间中的类时，使用 using 子句或 using 指令的命名空间来缩短语句。

```
到当前行的结束。
错误的语句是 #1. // 行注释以双斜杠 (//) 开头
```

# 你来做

现在你已经理解了 C# 程序编写的基本框架，准备好在文本编辑器中输入你的第一个 C# 程序了。程序员之间有一个传统：你用任何语言编写的第一个程序输出的都是 Hello, world!。要创建一个 C# 程序，你可以使用任何简单的文本编辑器，如记事本，或者 Microsoft Visual Studio 包含的编辑器。使用 C# 编辑器编写程序有优势，但在入门时使用纯文本编辑器更简单。

## 在编辑器中输入程序

1. 启动任何文本编辑器（如记事本），并在必要时打开新文档。
2. 输入使用 语句和类的头：
   `using static System.Console;`
   `class Hello`
3. 在接下来的两行中，输入类的左大括号和右大括号：有些程序员会在输入左大括号后立即输入右大括号，以确保他们总是成对输入。
4. 在类大括号之间，插入 Main 方法的左大括号和右大括号：
5. 在接下来的两行中，输入方法的左大括号和右大括号：
6. 在方法大括号之间，插入 WriteLine 语句：
7. 在类大括号之间，插入方法的大括号：

```csharp
using static System.Console;
class Hello
{
    static void Main()
    {
        WriteLine("Hello, world!");
    }
}
```

图 1-9 Hello![](7516c1fecf7bbbe7afb10cf209b17ae3_48_0.png)

# 编译和执行 C# 程序

在你编写并保存程序之后，在查看输出之前必须执行另外两个步骤：

- 你必须将程序（**源代码**）编译为**中间语言 (IL)**
- C# **即时 (JIT)** 编译器必须将中间代码翻译成可执行代码。

