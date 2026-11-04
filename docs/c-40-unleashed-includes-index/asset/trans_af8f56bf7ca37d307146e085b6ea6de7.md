
编写这段代码还有很多其他方式，但我只是为了说明代码中使用的 if 语句所引入的新作用域这一点。两个分支都会引入一个新作用域，其中声明了一个变量 y。它们不会冲突，因为它们是彼此并行声明的：两个 y 变量是不同的。

然而，在同一代码块的外层作用域中隐藏变量是非法的：

```csharp
public static void PrintAbs(int x)
{
    int y = x;

    if (x >= 0)
    {
        Print(y);
    }
    else if (x < 0)
    {
        // Error: A local variable named 'y' cannot be declared in this
        //          scope because it would give a different meaning to 'y',
        //          which is already used in a 'parent or current' scope to
        //          denote something else.
        int y = -x; // error: hiding y in outer scope
        Print(y);
    }
}
```

这不仅减少了潜在的混淆，还消除了用某种关键字来区分两个变量的需要。想一想，如果你有一堆嵌套作用域，每个作用域都隐藏外层作用域中的变量，而你想引用这样一个声明在“向上三层作用域”中的隐藏变量，会发生什么。

同样，在子作用域中使用过某个变量名之后，也不允许在外层作用域中重用该变量名：

```csharp
private static void PrintInt(int x)
{
    if (x >= 0)
    {
        int y = x;
        Print(y);
        return;
    }

    // Error: A local variable named 'y' cannot be declared in this scope
    //          because it would give a different meaning to 'y', which is
    //          already used in a 'child' scope to denote something else.
    int y = -x;
    Print(y);
}
```

而且显而易见，正如你现在可能已经猜到的那样，在同一作用域中声明同名但类型不同的变量是无效的。在一些其他无类型语言中，这是可能的，但往往是造成混淆的主要根源。

```csharp
int x = 5;

// Error: A local variable named 'x' is already defined in this scope.
string x = "Five";
```

## 赋值

除了声明局部变量之外，还需要在使用它们之前对其进行初始化。C# 非常严格，不允许使用未初始化的变量，因为这是其他语言中非常常见的错误来源。正因如此，下面的代码片段无法编译：

```csharp
int x;

// Error: Use of unassigned local variable 'x'.
Console.WriteLine(x);
```

为了确保变量在使用前被正确赋值，C# 有几条基于静态程序流分析的明确赋值规则。我不会详细讨论这些规则，但有时会顺带提到其中一些规则。

赋值是指根据类型，用某个值或引用来替换与变量关联的存储单元内容的行为。要使其正常工作，类型必须匹配。赋值运算符是 =，其中左侧（lhs）是变量名，右侧（rhs）是要求值的表达式：

```csharp
int x;
x = 42;
```

这里，42 只是一个由整数字面量组成的常量表达式，它被赋给名为 x 的变量。类型正好匹配，所以编译器很满意。如果你违反类型规则，就会产生错误：

```csharp
int x;

// Error: Cannot implicitly convert type 'string' to 'int'.
x = "Oops";
```

隐式转换与显式转换之间的区别将在第 13 章“运算符重载与转换”中讨论。在前面的示例中，没有理由不将变量的声明和初始化作为同一条语句的一部分：

```csharp
int x = 42;
```

同样，可以在同一行中为多个变量赋值：

```csharp
int x = 0, y = 1, z = 2;
```

到目前为止，我们讨论的是简单赋值。在学习二元运算符之后，我们将看看复合赋值。下面是一个你可以预测其行为的示例：

```csharp
int x = 0;
x += 1;
```

## 常量

变量顾名思义是可变的。它们可以被多次写入，从而导致存储单元的内容被替换。另一方面，常量在其初始化之后就不能再更改，而初始化必须在声明常量的位置进行。要声明局部常量，请使用 const 关键字：

```csharp
const int x = 42;
```

```csharp
// Error: The left-hand side of an assignment must be a variable, property or indexer.
x = 43;
```

常量在可初始化为什么值方面受到限制：该值必须能够在编译时计算出来。在实践中，这意味着允许整数类型和实数类型、字符类型、字符串类型和布尔类型，以及在使用 null 字面量时的引用类型。

看看这里幕后发生了什么很有教育意义。由于该值是在编译时计算的，因此（用 IL 的话说）没有必要将其存储在某个局部变量中。它可以作为常量直接内联到所有使用它的地方。

考虑下面的代码片段：

```csharp
int x = 42;
const int y = 42;

Console.WriteLine(x);
Console.WriteLine(y);
```

执行典型的编译和反汇编步骤，查看包含该代码的方法所生成的 IL 代码。图 4.21 显示了结果。

请注意用于声明局部变量的 IL 指令：

```text
.locals init ([0] int32 x)
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_243_0.png)

图 4.21 幕后的变量与常量。

这表明执行该代码需要一个局部变量，其类型为 int32（对应于 C# 的 int 和 BCL 的 System.Int32 的 CLR 内置类型）。常量 y 没有这样的条目。这已经揭示了局部常量所应受到的不同的处理方式。

> **注意**
> 
> 取决于你是在调试模式还是发布模式下构建，局部变量 x 在 ILDASM 的视角下会保留其名称。原因是 ILDASM 会在被反汇编的程序集旁边查找 PDB 符号文件，以获取更多信息，例如局部变量的名称。对 CLR 而言，变量名称无关紧要，因此它们会在编译时被去掉。如果没有 PDB 文件——这是发布模式下的默认行为——你会看到局部变量名为 V_0，这是反汇编器出于美化目的而生成的名字。

在 IL 代码内部，你可以看到常量 42 使用 ldc.i4.s 指令加载，该指令表示“加载 4 字节有符号常量整数”，并使用 stloc.0 存储到局部变量槽，stloc.0 表示“存储到局部槽 0”。第一个矩形标出了这一点。在接下来的几行中，该变量再次被加载，以传入 Console.WriteLine 的方法调用。

对于常量 y，没有保留局部变量槽，源代码中每次出现的 y 都被替换为常量值。第二个矩形说明了这一点。如果我们在该作用域内多次使用 y，那么每次使用都会看到一条针对其常量值 42 的 ldc.i4.s 指令。另一方面，在该作用域内多次使用 x 时，每次使用都会导致使用 ldloc.0 从局部变量槽中读取。

除了常量之外，还有只读字段，我们将在第 11 章中探讨并将其与常量进行比较。

## 隐式类型局部变量声明

**C# 3.0**

在前面的章节中，你已经看到了一种用于声明和初始化局部变量的语法：指定类型，为变量命名（lhs），并为其赋予某个表达式（rhs）。

```csharp
string name = "Bart";
```

正如你将看到的，表达式总是有类型的。这意味着我们向编译器指定了一些冗余信息。在左侧，我们显式声明了一个类型，而编译器可以从右侧推断出该信息。在这个例子中，字面量“Bart”的类型是 System.String。那么，为什么我们需要在左侧显式指定该类型呢？

### var 关键字

在 C# 语言 2.0 版之前，答案就是这样：事情就是这样；接受它吧。但从 3.0 版开始，局部变量声明可以省略左侧的类型，使其成为隐式类型：

```csharp
var name = "Bart";
```

这里，var 关键字指示编译器根据赋值符号右侧的表达式推断变量的类型。

不要以任何方式将其与 dynamic 或 System.Object 混淆。该变量在编译时仍然是静态类型的：编译器完全知道我们的意思。事实上，生成的 IL 代码与原始代码片段的 IL 代码逐条指令等价。为了证明这一点，请使用 Visual Studio 并查看 IntelliSense 和工具提示，如图 4.22 所示。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_244_0.png)

**图 4.22** 隐式类型的局部变量是静态类型的。

如果 var 代表 System.Object，我们就不会看到字符串对象有任何有意义的 IntelliSense（除了 Equals、GetHashCode 和 ToString 这三项）。如果它代表 dynamic，我们根本看不到 IntelliSense，因为操作会在运行时分派。总之，var 是静态类型的。
