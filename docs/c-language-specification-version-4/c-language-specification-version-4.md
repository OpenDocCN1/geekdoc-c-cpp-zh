# C# 语言规范 第 4 版





## 1. 引言

C#（读作“See Sharp”）是一种简单、现代、面向对象且类型安全的编程语言。C# 植根于 C 语言家族，C、C++ 和 Java 程序员会立即熟悉它。C# 由 ECMA International 标准化为 *ECMA-334* 标准，并由 ISO/IEC 标准化为 *ISO/IEC 23270* 标准。Microsoft 针对 .NET Framework 的 C# 编译器是这两个标准的一致性实现。

C# 是一种面向对象的语言，但 C# 进一步支持*面向组件*的编程。当代软件设计越来越依赖于以自包含且自描述的功能包形式出现的软件组件。此类组件的关键在于它们呈现一个带有属性、方法和事件的编程模型；它们具有提供关于组件的声明性信息的特性；并且它们包含自己的文档。C# 提供语言构造来直接支持这些概念，使 C# 成为创建和使用软件组件的一种非常自然的语言。

若干 C# 特性有助于构建健壮且持久的应用程序：*垃圾回收*自动回收未使用对象占用的内存；*异常处理*提供了一种结构化且可扩展的进行错误检测和恢复的方法；而语言的*类型安全*设计使得无法读取未初始化的变量、无法索引超出数组边界的数组，也无法执行未检查的类型转换。

C# 具有*统一的类型系统*。所有 C# 类型（包括 `int` 和 `double` 等基元类型）都继承自单一的根 *object* 类型。因此，所有类型共享一组公共操作，任何类型的值都可以以一致的方式存储、传输和操作。此外，C# 同时支持用户定义的引用类型和值类型，允许动态分配对象以及轻量级结构的内联存储。

为确保 C# 程序和库能够以兼容的方式随时间演进，C# 的设计非常强调*版本控制*。许多编程语言很少关注此问题，因此当引入依赖库的较新版本时，用这些语言编写的程序会比必要更频繁地中断。C# 设计中直接受到版本控制考虑影响的方面包括单独的 *virtual* 和 *override* 修饰符、方法重载解析规则，以及对显式接口成员声明的支持。

本章其余部分描述 C# 语言的基本特性。尽管后续章节以注重细节、有时是数学化的方式描述规则和例外情况，但本章力求清晰简洁，牺牲完整性。其目的是向读者提供该语言的介绍，以便于编写早期程序和阅读后续章节。

### 1.1 Hello world

“Hello, World”程序传统上用于介绍一种编程语言。以下是 C# 中的该程序：

```csharp
using System;
class Hello
{
    static void Main() {
        Console.WriteLine("Hello, world");
    }
}
```

C# 源文件通常具有文件扩展名 .cs。假设“Hello, World”程序存储在文件 hello.cs 中，则可以使用命令行通过 Microsoft C# 编译器编译该程序

```
csc hello.cs
```

这将生成名为 hello.exe 的可执行程序集。该应用程序运行时产生的输出为

```
Hello, world
```

“Hello, World”程序以引用 System 命名空间的 using 指令开始。命名空间提供了一种分层方式来组织 C# 程序和库。命名空间包含类型和其他命名空间——例如，System 命名空间包含许多类型（如程序中引用的 Console 类）以及许多其他命名空间（如 IO 和 Collections）。引用给定命名空间的 using 指令使得可以非限定地使用作为该命名空间成员的类型。由于 using 指令，程序可以使用 Console.WriteLine 作为 System.Console.WriteLine 的简写。

Hello 类由“Hello, World”程序声明，具有单个成员，即名为 Main 的方法。Main 方法使用 static 修饰符声明。虽然实例方法可以使用关键字 this 引用特定的封闭对象实例，但静态方法在操作时不引用特定对象。按照惯例，名为 Main 的静态方法用作程序的入口点。

程序的输出由 System 命名空间中 Console 类的 writeLine 方法产生。该类由 .NET Framework 类库提供，默认情况下，Microsoft C# 编译器会自动引用这些类库。注意，C# 本身没有单独的运行时库。相反，.NET Framework 是 C# 的运行时库。

### 1.2 程序结构

C# 中的关键组织概念是程序、命名空间、类型、成员和程序集。C# 程序由一个或多个源文件组成。程序声明类型，类型包含成员，并且可以组织到命名空间中。类和接口是类型的示例。字段、方法、属性和事件是成员的示例。当 C# 程序被编译时，它们被物理打包到程序集中。程序集通常具有文件扩展名 .exe 或 .dll，具体取决于它们实现的是应用程序还是库。

该示例

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
```

在名为 Acme.Collections 的命名空间中声明一个名为 Stack 的类。此类的完全限定名称为 Acme.Collections.Stack。该类包含若干成员：名为 top 的字段、两个名为 Push 和 Pop 的方法，以及名为 Entry 的嵌套类。Entry 类进一步包含三个成员：名为 next 的字段、名为 data 的字段和一个构造函数。假设示例的源代码存储在文件 acme.cs 中，则命令行

```
csc /t:library acme.cs
```

将该示例编译为库（没有 Main 入口点的代码），并生成名为 acme.dll 的程序集。

程序集包含以*中间语言*（IL）指令形式表示的可执行代码，以及以***元数据***形式表示的符号信息。在执行之前，程序集中的 IL 代码由 .NET 公共语言运行时的实时（JIT）编译器自动转换为特定于处理器的代码。

由于程序集是包含代码和*元数据*的自描述功能单元，因此在 C# 中不需要 #include 指令和头文件。特定程序集中包含的公共类型和成员只需在编译程序时引用该程序集，即可在 C# 程序中使用。例如，此程序使用来自 acme.dll 程序集的 Acme.Collections.Stack 类：

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

如果程序存储在文件 test.cs 中，则编译 test.cs 时，可以使用编译器的 /r 选项引用 acme.dll 程序集：

```
csc /r:acme.dll test.cs
```

这会创建名为 test.exe 的可执行程序集，运行时产生输出：

```
100
10
1
```

C# 允许将程序的源文本存储在多个源文件中。编译多文件 C# 程序时，所有源文件会一起处理，并且源文件可以自由地相互引用——从概念上讲，就好像所有源文件在处理之前被连接成一个大文件一样。在 C# 中永远不需要前向声明，因为除极少数例外情况外，声明顺序无关紧要。C# 不限制一个源文件只能声明一个公共类型，也不要求源文件的名称与源文件中声明的类型匹配。




### 1.3 类型和变量

C# 中有两种类型：*值类型*和*引用类型*。值类型的变量直接包含其数据，而引用类型的变量存储对其数据的引用，后者称为对象。对于引用类型，两个变量可以引用同一个对象，因此对一个变量的操作可能影响另一个变量所引用的对象。对于值类型，每个变量都有自己的数据副本，对一个变量的操作不可能影响另一个变量（`ref` 和 `out` 参数变量除外）。

C# 的值类型进一步分为*简单类型*、*枚举类型*、*结构类型*和*可空类型*，C# 的引用类型进一步分为*类类型*、*接口类型*、*数组类型*和*委托类型*。

下表概述了 C# 的类型系统。

| 类别 | 子类别 | 说明 |
|---|---|---|
| 值类型 | 简单类型 | 有符号整型：`sbyte`、`short`、`int`、`long` |
| 值类型 | 简单类型 | 无符号整型：`byte`、`ushort`、`uint`、`ulong` |
| 值类型 | 简单类型 | Unicode 字符：`char` |
| 值类型 | 简单类型 | IEEE 浮点：`float`、`double` |
| 值类型 | 简单类型 | 高精度十进制：`decimal` |
| 值类型 | 简单类型 | 布尔：`bool` |
| 值类型 | 枚举类型 | 形式为 `enum E {...}` 的用户定义类型 |
| 值类型 | 结构类型 | 形式为 `struct S {...}` 的用户定义类型 |
| 值类型 | 可空类型 | 带有 `null` 值的所有其他值类型的扩展 |
| 引用类型 | 类类型 | 所有其他类型的最终基类：`object` |
| 引用类型 | 类类型 | Unicode 字符串：`string` |
| 引用类型 | 类类型 | 形式为 `class C {...}` 的用户定义类型 |
| 引用类型 | 接口类型 | 形式为 `interface I {...}` 的用户定义类型 |
| 引用类型 | 数组类型 | 一维和多维，例如 `int[]` 和 `int[,]` |
| 引用类型 | 委托类型 | 用户定义类型，例如形式为 `delegate int D(...)` |

八种整型支持 8 位、16 位、32 位和 64 位的有符号或无符号形式的值。

两种浮点类型 `float` 和 `double` 分别使用 32 位单精度和 64 位双精度 IEEE 754 格式表示。

`decimal` 类型是 128 位数据类型，适用于财务和货币计算。

C# 的 `bool` 类型用于表示布尔值——即 `true` 或 `false` 的值。

C# 中的字符和字符串处理使用 Unicode 编码。`char` 类型表示一个 UTF-16 代码单元，`string` 类型表示 UTF-16 代码单元序列。

下表总结了 C# 的数值类型。

| 类别 | 位数 | 类型 | 范围/精度 |
|---|---:|---|---|
| 有符号整型 | 8 | `sbyte` | -128...127 |
|  | 16 | `short` | -32,768...32,767 |
|  | 32 | `int` | -2,147,483,648...2,147,483,647 |
|  | 64 | `long` | -9,223,372,036,854,775,808...9,223,372,036,854,775,807 |
| 无符号整型 | 8 | `byte` | 0...255 |
|  | 16 | `ushort` | 0...65,535 |
|  | 32 | `uint` | 0...4,294,967,295 |
|  | 64 | `ulong` | 0...18,446,744,073,709,551,615 |
| 浮点 | 32 | `float` | 1.5 × 10^-45 到 3.4 × 10^38，7 位精度 |
|  | 64 | `double` | 5.0 × 10^-324 到 1.7 × 10^308，15 位精度 |
| 十进制 | 128 | `decimal` | 1.0 × 10^-28 到 7.9 × 10^28，28 位精度 |

C# 程序使用*类型声明*创建新类型。类型声明指定新类型的名称和成员。C# 的五种类别类型可由用户定义：类类型、结构类型、接口类型、枚举类型和委托类型。

类类型定义包含数据成员（字段）和函数成员（方法、属性等）的数据结构。类类型支持单继承和多态，这些机制使派生类能够扩展和特化基类。

结构类型与类类型相似，因为它表示包含数据成员和函数成员的结构。但是，与类不同，结构是值类型，不需要堆分配。结构类型不支持用户指定的继承，所有结构类型都隐式继承自 `object` 类型。

接口类型将契约定义为公共函数成员的命名集合。实现接口的类或结构必须提供该接口函数成员的实现。接口可以继承自多个基接口，类或结构可以实现多个接口。

委托类型表示对具有特定参数列表和返回类型的方法的引用。委托使得可以将方法视为可分配给变量并作为参数传递的实体。委托类似于某些其他语言中的函数指针概念，但与函数指针不同，委托是面向对象且类型安全的。

类、结构、接口和委托类型都支持泛型，因此可以用其他类型对它们进行参数化。

枚举类型是包含命名常量的不同种类类型。每个枚举类型都有一个基础类型，该类型必须是八种整型之一。枚举类型的值集与基础类型的值集相同。

C# 支持任意类型的一维和多维数组。与上面列出的类型不同，数组类型不必在使用前声明。相反，数组类型通过在类型名后跟方括号来构造。例如，`int[]` 是 `int` 的一维数组，`int[,]` 是 `int` 的二维数组，`int[][]` 是 `int` 的一维数组的一维数组。

可空类型也不必在使用前声明。对于每个不可空值类型 `T`，都有一个对应的可空类型 `T?`，它可以额外保存一个值 `null`。例如，`int?` 是可以保存任何 32 位整数或值 `null` 的类型。

C# 的类型系统是统一的，因此任何类型的值都可以被视为对象。C# 中的每个类型都直接或间接派生自 object 类类型，而 object 是所有类型的最终基类。引用类型的值只需将这些值视为 object 类型，即可当作对象处理。值类型的值通过执行*装箱*和*拆箱*操作来当作对象处理。在以下示例中，int 值转换为 object，然后再转换回 int。

```csharp
using System;
class Test
{
    static void Main() {
        int i = 123;
        object o = i;      // boxing
        int j = (int)o;    // unboxing
    }
}
```

当值类型的值转换为 object 类型时，会分配一个对象实例（也称为“箱”）来保存该值，并将该值复制到该箱中。相反，当对象引用强制转换为值类型时，会检查所引用的对象是否为正确值类型的箱，如果检查成功，则将该箱中的值复制出来。

C# 的统一类型系统实际上意味着值类型可以“按需”成为对象。由于这种统一性，使用 object 类型的通用库既可以用于引用类型，也可以用于值类型。

C# 中有几种*变量*，包括字段、数组元素、局部变量和参数。变量表示存储位置，每个变量都有一个类型，该类型决定可以存储在变量中的值，如下表所示。

| 变量类型 | 可能内容 |
|---|---|
| 非可空值类型 | 该确切类型的值 |
| 可空值类型 | null 值或该确切类型的值 |
| object | null 引用、对任意引用类型的对象的引用，或对任意值类型的装箱值的引用 |
| 类类型 | null 引用、对该类类型的实例的引用，或对派生自该类类型的类的实例的引用 |
| 接口类型 | null 引用、对实现该接口类型的类类型的实例的引用，或对实现该接口类型的值类型的装箱值的引用 |
| 数组类型 | null 引用、对该数组类型的实例的引用，或对兼容数组类型的实例的引用 |
| 委托类型 | null 引用或对该委托类型的实例的引用 |

### 1.4 表达式

*表达式*由*操作数*和*运算符*构造而成。表达式的运算符指示要对操作数应用哪些操作。运算符的示例包括 +、-、\*、/ 和 new。操作数的示例包括字面量、字段、局部变量和表达式。




当表达式包含多个运算符时，运算符的优先级控制各个运算符被求值的顺序。例如，表达式 x + y * z 被求值为 x + (y * z)，因为 * 运算符的优先级高于 + 运算符。

大多数运算符可以重载。运算符重载允许为一个或两个操作数属于用户定义类或结构类型的操作指定用户定义的运算符实现。

下表总结了 C# 的运算符，按优先级从高到低列出运算符类别。同一类别中的运算符具有相同的优先级。

| 类别 | 表达式 | 描述 |
|---|---|---|
| 主 | x.m | 成员访问 |
| 主 | x(...) | 方法和委托调用 |
| 主 | x[...] | 数组和索引器访问 |
| 主 | x++ | 后缀递增 |
| 主 | x-- | 后缀递减 |
| 主 | new T(...) | 对象和委托创建 |
| 主 | new T(...) {...} | 带初始化器的对象创建 |
| 主 | new {...} | 匿名对象初始化器 |
| 主 | new T[...] | 数组创建 |
| 主 | typeof(T) | 获取 T 的 System.Type 对象 |
| 主 | checked(x) | 在 checked 上下文中求值表达式 |
| 主 | unchecked(x) | 在 unchecked 上下文中求值表达式 |
| 主 | default(T) | 获取类型 T 的默认值 |
| 主 | delegate {...} | 匿名函数（匿名方法） |
| 一元 | +x | 恒等 |
| 一元 | -x | 取反 |
| 一元 | !x | 逻辑取反 |
| 一元 | ~x | 按位取反 |
| 一元 | ++x | 前缀递增 |
| 一元 | --x | 前缀递减 |
| 一元 | (T)x | 显式将 x 转换为类型 T |
| 乘法 | x * y | 乘法 |
| 乘法 | x / y | 除法 |
| 乘法 | x % y | 余数 |
| 加法 | x + y | 加法、字符串连接、委托组合 |
| 加法 | x - y | 减法、委托移除 |

| 类别 | 运算符 | 描述 |
|---|---|---|
| 移位 | `x << y` | 左移 |
| | `x >> y` | 右移 |
| 关系和类型测试 | `x < y` | 小于 |
| | `x > y` | 大于 |
| | `x <= y` | 小于或等于 |
| | `x >= y` | 大于或等于 |
| | `x is T` | 如果 x 是 T 则返回 true，否则返回 false |
| | `x as T` | 如果 x 不是 T 则返回 x 强制为 T 类型，否则返回 null |
| 相等 | `x == y` | 相等 |
| | `x != y` | 不相等 |
| 逻辑与 | `x & y` | 整数按位与、布尔逻辑与 |
| 逻辑异或 | `x ^ y` | 整数按位异或、布尔逻辑异或 |
| 逻辑或 | `x | y` | 整数按位或、布尔逻辑或 |
| 条件与 | `x && y` | 仅当 x 为 true 时才求值 y |
| 条件或 | `x || y` | 仅当 x 为 false 时才求值 y |
| 空合并 | `x ?? y` | 如果 x 为 null 则求值为 y，否则求值为 x |
| 条件 | `x ? y : z` | 如果 x 为 true 则求值 y，如果 x 为 false 则求值 z |
| 赋值或匿名函数 | `x = y` | 赋值 |
| | `x op= y` | 复合赋值；支持的运算符为 `*= /= %= += -= <<= >>= &= ^= |=` |
| | `(T x) => y` | 匿名函数（lambda 表达式） |

### 1.5 语句

程序的行为使用 *语句* 表达。C# 支持多种不同类型的语句，其中一些是基于嵌入语句定义的。

*块* 允许在只允许单个语句的上下文中编写多个语句。块由写在定界符 `{` 和 `}` 之间的语句列表组成。

*声明语句* 用于声明局部变量和常量。

*表达式语句* 用于求值表达式。可用作语句的表达式包括方法调用、使用 new 运算符的对象分配、使用 `=` 和复合赋值运算符的赋值，以及使用 `++` 和 `--` 运算符的递增和递减操作。

*选择语句* 用于根据某个表达式的值从多个可能的语句中选择一个执行。此组包括 `if` 和 `switch` 语句。

*迭代语句* 用于重复执行嵌入语句。此组包括 `while`、`do`、`for` 和 `foreach` 语句。

*跳转语句* 用于转移控制。此组包括 `break`、`continue`、`goto`、`throw`、`return` 和 `yield` 语句。

try...catch 语句用于捕获在块执行期间发生的异常，而 try...finally 语句用于指定无论是否发生异常都会始终执行的终结代码。

checked 和 unchecked 语句用于控制整数类型算术运算和转换的溢出检查上下文。

lock 语句用于获取给定对象的互斥锁，执行语句，然后释放锁。

using 语句用于获取资源，执行语句，然后释放该资源。

下表列出了 C# 的语句，并为每一种提供示例。

| 语句 | 示例 |
|---|---|
| 局部变量声明 | static void Main() { 
  int a;
  int b = 2, c = 3;
  a = 1;
  Console.WriteLine(a + b + c);
} |
| 局部常量声明 | static void Main() { 
  const float pi = 3.1415927f;
  const int r = 25;
  Console.WriteLine(pi * r * r);
} |
| 表达式语句 | static void Main() { 
  int i;
  i = 123; // Expression statement
  Console.WriteLine(i); // Expression statement
  i++; // Expression statement
  Console.WriteLine(i); // Expression statement
} |
| if 语句 | static void Main(string[] args) { 
  if (args.Length == 0) {
    Console.WriteLine("No arguments");
  } else {
    Console.WriteLine("One or more arguments");
  }
} |

| 语句 | 代码 |
|---|---|
| switch 语句 | ```csharp
static void Main(string[] args) {
    int n = args.Length;
    switch (n) {
        case 0:
            Console.WriteLine("No arguments");
            break;
        case 1:
            Console.WriteLine("One argument");
            break;
        default:
            Console.WriteLine("{0} arguments", n);
            break;
    }
}
``` |
| while 语句 | ```csharp
static void Main(string[] args) {
    int i = 0;
    while (i < args.Length) {
        Console.WriteLine(args[i]);
        i++;
    }
}
``` |
| do 语句 | ```csharp
static void Main() {
    string s;
    do {
        s = Console.ReadLine();
        if (s != null) Console.WriteLine(s);
    } while (s != null);
}
``` |
| for 语句 | ```csharp
static void Main(string[] args) {
    for (int i = 0; i < args.Length; i++) {
        Console.WriteLine(args[i]);
    }
}
``` |
| foreach 语句 | ```csharp
static void Main(string[] args) {
    foreach (string s in args) {
        Console.WriteLine(s);
    }
}
``` |
| break 语句 | ```csharp
static void Main() {
    while (true) {
        string s = Console.ReadLine();
        if (s == null) break;
        Console.WriteLine(s);
    }
}
``` |
| continue 语句 | ```csharp
static void Main(string[] args) {
    for (int i = 0; i < args.Length; i++) {
        if (args[i].StartsWith("/")) continue;
        Console.WriteLine(args[i]);
    }
}
``` |

| 语句 | 代码 |
|---|---|
| goto 语句 | static void Main(string[] args) { int i = 0; goto check; loop: Console.WriteLine(args[i++]); check: if (i < args.Length) goto loop; } |
| return 语句 | static int Add(int a, int b) { return a + b; } static void Main() { Console.WriteLine(Add(1, 2)); return; } |
| yield 语句 | static IEnumerable<int> Range(int from, int to) { for (int i = from; i < to; i++) { yield return i; } yield break; } static void Main() { foreach (int x in Range(-10,10)) { Console.WriteLine(x); } } |
| throw 和 try 语句 | static double Divide(double x, double y) { if (y == 0) throw new DivideByZeroException(); return x / y; } static void Main(string[] args) { try { if (args.Length != 2) { throw new Exception("Two numbers required"); } double x = double.Parse(args[0]); double y = double.Parse(args[1]); Console.WriteLine(Divide(x, y)); } catch (Exception e) { Console.WriteLine(e.Message); } finally { Console.WriteLine("Good bye!"); } } |
| checked 和 unchecked 语句 | static void Main() { int i = int.MaxValue; checked { Console.WriteLine(i + 1); // Exception } unchecked { Console.WriteLine(i + 1); // Overflow } } |



| 语句 | 示例 |
|---|---|
| `lock` 语句 | <pre><code>class Account<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;decimal balance;<br>&nbsp;&nbsp;&nbsp;&nbsp;public void withdraw(decimal amount) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lock (this) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (amount > balance) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;throw new Exception("Insufficient funds");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;balance -= amount;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>}</code></pre> |
| `using` 语句 | <pre><code>static void Main() {<br>&nbsp;&nbsp;&nbsp;&nbsp;using (TextWriter w = File.CreateText("test.txt")) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line one");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line two");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line three");<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>}</code></pre> |

### 1.6 类和对象

类是 C# 中最基本的类型。类是一种数据结构，将状态（字段）和操作（方法和其他函数成员）组合在一个单元中。类为动态创建的类实例（也称为对象）提供定义。类支持继承和多态，这些机制使派生类能够扩展和特化基类。

使用类声明创建新类。类声明以标头开始，该标头指定类的特性和修饰符、类名、基类（如果给定）以及类实现的接口。标头后面是类主体，主体由写在分隔符 `{` 和 `}` 之间的成员声明列表组成。

下面是一个名为 Point 的简单类的声明：

```csharp
public class Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

类的实例使用 `new` 运算符创建，该运算符为新实例分配内存、调用构造函数初始化实例，并返回对实例的引用。以下语句创建两个 `Point` 对象，并将对这些对象的引用存储在两个变量中：

```csharp
Point p1 = new Point(0, 0);
Point p2 = new Point(10, 20);
```

对象占用的内存在对象不再使用时自动回收。在 C# 中，显式释放对象既不必要也不可能。

### 1.6.1 成员

类的成员要么是静态成员，要么是实例成员。静态成员属于类，实例成员属于对象（类的实例）。

下表概述了类可以包含的成员种类。

| 成员 | 说明 |
|---|---|
| 常量 | 与类关联的常量值 |
| 字段 | 类的变量 |
| 方法 | 类可执行的计算和操作 |
| 属性 | 与读写类的命名属性相关的操作 |
| 索引器 | 与像数组一样索引类实例相关的操作 |
| 事件 | 类可以生成的通知 |
| 运算符 | 类支持的转换和表达式运算符 |
| 构造函数 | 初始化类实例或类本身所需的操作 |
| 析构函数 | 在永久丢弃类实例之前执行的操作 |
| 类型 | 类声明的嵌套类型 |

### 1.6.2 可访问性

类的每个成员都有关联的可访问性，它控制能够访问该成员的程序文本区域。可访问性有五种可能的形式。下表对此进行了总结。

| 可访问性 | 含义 |
|---|---|
| public | 访问不受限制 |
| protected | 访问限于此类或从此类派生的类 |
| internal | 访问限于此程序 |
| protected internal | 访问限于此程序或从此类派生的类 |
| private | 访问限于此类 |

### 1.6.3 类型参数

类定义可以通过在类名后面加上包含类型参数名称列表的尖括号来指定一组类型参数。然后可以在类声明的主体中使用类型参数来定义类的成员。在下面的示例中，`Pair` 的类型参数是 `TFirst` 和 `TSecond`：

```csharp
public class Pair<TFirst,TSecond>
{
    public TFirst First;
    public TSecond Second;
}
```

声明为接受类型参数的类类型称为泛型类类型。结构、接口和委托类型也可以是泛型。

使用泛型类时，必须为每个类型参数提供类型实参：

```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First; // TFirst is int
string s = pair.Second; // TSecond is string
```

提供了类型实参的泛型类型（如上面的 `Pair<int,string>`）称为构造类型。

### 1.6.4 基类

类声明可以通过在类名和类型参数后面加上冒号和基类名称来指定基类。省略基类规范等同于从 `object` 类型派生。在下面的示例中，`Point3D` 的基类是 `Point`，而 `Point` 的基类是 `object`：

```csharp
public class Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
public class Point3D: Point
{
    public int z;
    public Point3D(int x, int y, int z): base(x, y) {
        this.z = z;
    }
}
```

类继承其基类的成员。继承意味着类隐式包含其基类的所有成员，但基类的实例构造函数、静态构造函数和析构函数除外。派生类可以向其继承的成员添加新成员，但不能移除继承成员的定义。在前面的示例中，`Point3D` 从 `Point` 继承了 `x` 和 `y` 字段，每个 `Point3D` 实例都包含三个字段：`x`、`y` 和 `z`。

存在从类类型到其任何基类类型的隐式转换。因此，类类型的变量可以引用该类的实例或任何派生类的实例。例如，对于前面的类声明，`Point` 类型的变量可以引用 `Point` 或 `Point3D`：

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

### 1.6.5 字段

字段是与类或类实例关联的变量。

使用 `static` 修饰符声明的字段定义静态字段。静态字段标识一个存储位置。无论创建多少个类实例，静态字段始终只有一个副本。

未使用 `static` 修饰符声明的字段定义实例字段。类的每个实例都包含该类所有实例字段的单独副本。

在下面的示例中，`Color` 类的每个实例都有 `r`、`g` 和 `b` 实例字段的单独副本，但 `Black`、`White`、`Red`、`Green` 和 `Blue` 静态字段只有一个副本：

```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);
    private byte r, g, b;

    public Color(byte r, byte g, byte b) {
        this.r = r;
        this.g = g;
        this.b = b;
    }
}
```

如前面的示例所示，可以使用 `readonly` 修饰符声明只读字段。对 `readonly` 字段的赋值只能作为字段声明的一部分，或在同一类的构造函数中进行。

### 1.6.6 方法

方法是实现对象或类可以执行的计算或操作的成员。静态方法通过类访问。实例方法通过类的实例访问。

方法有一个（可能为空的）参数列表，表示传递给该方法的值或变量引用，以及一个返回类型，指定该方法计算并返回的值的类型。如果方法不返回值，则其返回类型为 `void`。

与类型一样，方法也可以有一组类型参数，调用方法时必须为其指定类型实参。与类型不同，类型实参通常可以从方法调用的实参推断出来，无需显式给出。

方法的签名在声明该方法的类中必须是唯一的。方法的签名由方法名称、类型参数数量以及参数的数量、修饰符和类型组成。方法的签名不包括返回类型。

#### 1.6.6.1 参数

参数用于向方法传递值或变量引用。方法的参数从调用方法时指定的实参中获取实际值。参数有四种：值参数、引用参数、输出参数和参数数组。

值参数用于输入参数传递。值参数对应于一个局部变量，其初始值来自为该参数传递的实参。对值参数的修改不影响为该参数传递的实参。

值参数可以是可选的，通过指定默认值，以便可以省略相应的实参。

引用参数同时用于输入和输出参数传递。为引用参数传递的实参必须是变量，在方法执行期间，引用参数表示与实参变量相同的存储位置。引用参数使用 `ref` 修饰符声明。下面的示例展示了 `ref` 参数的使用。

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
        Console.WriteLine("{0} {1}", i, j);      // Outputs "2 1"
    }
}
```



*输出参数*（output parameter）用于输出参数传递。输出参数与引用参数类似，不同之处在于调用方提供的参数的初始值并不重要。输出参数使用*out*修饰符声明。下面的示例演示了*out*参数的使用。

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
        Console.WriteLine("{0} {1}", res, rem);  // Outputs "3 1"
    }
}
```

*参数数组*（parameter array）允许向方法传递可变数量的参数。参数数组使用*params*修饰符声明。方法中只有最后一个参数可以是参数数组，且参数数组的类型必须是一维数组类型。*System.Console*类的*Write*和*WriteLine*方法是参数数组使用的典型示例。它们的声明如下。

```
public class Console
{
    public static void Write(string fmt, params object[] args) {...}
    public static void WriteLine(string fmt, params object[] args) {...}
    ...
}
```

在使用参数数组的方法中，参数数组的行为与普通数组类型参数完全一致。但是，在调用带有参数数组的方法时，既可以传递一个参数数组类型的参数，也可以传递任意数量的参数数组元素类型的参数。在后一种情况下，系统会自动创建并初始化一个数组实例，用给定的参数填充它。例如：

```
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```

等价于以下写法：

```
string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
```

#### 1.6.6.2 方法体和局部变量

方法体指定调用方法时要执行的语句。

方法体可以声明特定于该次方法调用的变量。这些变量称为*局部变量*（local variable）。局部变量声明指定一个类型名称、一个变量名称，以及可能的一个初始值。下面的示例声明了一个初始值为零的局部变量i，以及一个没有初始值的局部变量j。

```
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

C#要求在获取局部变量的值之前，必须先对其明确赋值。例如，如果前面示例中i的声明没有包含初始值，编译器将会在后续使用i的地方报告错误，因为在程序的这些位置上i没有被明确赋值。

方法可以使用return语句将控制权返回给调用方。在返回void的方法中，return语句不能指定表达式。在返回非void的方法中，return语句必须包含一个计算返回值的表达式。

#### 1.6.6.3 静态方法和实例方法

使用static修饰符声明的方法是静态方法。静态方法不针对特定实例进行操作，并且只能直接访问静态成员。

不使用static修饰符声明的方法是实例方法。实例方法针对特定实例进行操作，并且可以访问静态成员和实例成员。调用实例方法的那个实例可以通过this显式访问。在静态方法中引用this是错误的。

下面的Entity类既有静态成员也有实例成员。

```
class Entity
{
    static int nextSerialNo;
    int serialNo;
    public Entity() {
        serialNo = nextSerialNo++;
    }
    public int GetSerialNo() {
        return serialNo;
    }
    public static int GetNextSerialNo() {
        return nextSerialNo;
    }
    public static void SetNextSerialNo(int value) {
        nextSerialNo = value;
    }
}
```

每个Entity实例包含一个序列号（可能还包含其他此处未显示的信息）。Entity构造函数（类似于实例方法）使用下一个可用的序列号来初始化新实例。由于构造函数是实例成员，它可以同时访问serialNo实例字段和nextSerialNo静态字段。

GetNextSerialNo和SetNextSerialNo静态方法可以访问nextSerialNo静态字段，但如果它们直接访问serialNo实例字段则是错误的。

下面的示例演示了Entity类的使用。

```
using System;
class Test
{
    static void Main() {
        Entity.SetNextSerialNo(1000);
        Entity e1 = new Entity();
        Entity e2 = new Entity();
        Console.WriteLine(e1.GetSerialNo());        // Outputs "1000"
        Console.WriteLine(e2.GetSerialNo());        // Outputs "1001"
        Console.WriteLine(Entity.GetNextSerialNo());  // Outputs "1002"
    }
}
```

请注意，SetNextSerialNo和GetNextSerialNo静态方法是针对类调用的，而GetSerialNo实例方法是针对类的实例调用的。

#### 1.6.6.4 虚方法、重写方法和抽象方法

当实例方法声明包含virtual修饰符时，该方法称为*虚方法*（virtual method）。当没有virtual修饰符时，该方法称为*非虚方法*（non-virtual method）。

当调用虚方法时，进行调用的实例的运行时类型决定了实际要调用的方法实现。而在非虚方法调用中，实例的编译时类型是决定因素。

虚方法可以在派生类中被重写。当实例方法声明包含override修饰符时，该方法将重写一个具有相同签名的继承虚方法。虚方法声明引入一个新方法，而重写方法声明通过提供一个新的实现来特化现有的继承虚方法。

抽象方法是没有实现的虚方法。抽象方法使用abstract修饰符声明，并且只允许在同样声明为抽象的类中。每个非抽象派生类都必须重写抽象方法。

下面的示例声明了一个抽象类Expression，它表示表达式树节点，以及三个派生类Constant、VariableReference和Operation，它们分别实现常量、变量引用和算术运算的表达式树节点。（这与§4.6节中引入的表达式树类型类似，但不要混淆。）

```
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

以上四个类可用于对算术表达式进行建模。例如，使用这些类的实例，表达式x + 3可以表示如下：

```
Expression e = new Operation(
    new VariableReference("x"),
    '+',
    new Constant(3));
```

调用Expression实例的Evaluate方法来计算给定的表达式并产生一个double值。该方法接受一个Hashtable作为参数，其中包含变量名（作为条目的键）和值（作为条目的值）。Evaluate方法是一个虚抽象方法，这意味着非抽象派生类必须重写它以提供实际实现。

Constant的Evaluate实现只是返回存储的常量。VariableReference的Evaluate实现在哈希表中查找变量名并返回结果值。Operation的Evaluate实现首先计算左操作数和右操作数（通过递归调用它们的Evaluate方法），然后执行给定的算术运算。

下面的程序使用Expression类针对不同的x和y值计算表达式x * (y + 2)。

```
using System;
using System.Collections;
class Test
{
    static void Main() {
```




```csharp
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
            Console.WriteLine(e.Evaluate(vars));      // Outputs "21"
            vars["x"] = 1.5;
            vars["y"] = 9;
            Console.WriteLine(e.Evaluate(vars));      // Outputs "16.5"
        }
    }
```

#### 1.6.6.5 方法重载

方法*重载*允许同一个类中的多个方法具有相同的名称，只要它们的签名唯一即可。在编译对重载方法的调用时，编译器使用*重载决策*来确定要调用的特定方法。重载决策会找到与参数最匹配的一个方法，如果没有找到唯一的最佳匹配，则会报告错误。下面的示例展示了重载决策的实际效果。`Main`方法中每个调用的注释显示了实际调用的方法。

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
            F();                 // Invokes F()
            F(1);                // Invokes F(int)
            F(1.0);              // Invokes F(double)
            F("abc");            // Invokes F(object)
            F((double)1);        // Invokes F(double)
            F((object)1);        // Invokes F(object)
            F<int>(1);           // Invokes F<T>(T)
            F(1, 1);             // Invokes F(double, double)
        }
    }
```

如示例所示，可以通过将参数显式转换为确切的参数类型和/或显式提供类型参数，始终选择特定的方法。

### 1.6.7 其他函数成员

包含可执行代码的成员统称为类的*函数成员*。前面的部分描述了方法，它们是函数成员的主要类型。本节介绍C#支持的其他类型的函数成员：构造函数、属性、索引器、事件、运算符和析构函数。

下表展示了一个名为`List<T>`的泛型类，它实现了一个可增长的对象列表。该类包含了最常见的几种函数成员的示例。

| 代码 | 种类 |
|------|------|
| `public class List<T> {` | |
| `  const int defaultCapacity = 4;` | 常量 |
| `  T[] items;`<br>`  int count;` | 字段 |
| `  public List(int capacity = defaultCapacity) {`<br>`    items = new T[capacity];`<br>`  }` | 构造函数 |
| `  public int Count {`<br>`    get { return count; }`<br>`  }`<br>`  public int Capacity {`<br>`    get {`<br>`      return items.Length;`<br>`    }`<br>`    set {`<br>`      if (value < count) value = count;`<br>`      if (value != items.Length) {`<br>`        T[] newItems = new T[value];`<br>`        Array.Copy(items, 0, newItems, 0, count);`<br>`        items = newItems;`<br>`      }`<br>`    }`<br>`  }` | 属性 |
| `  public T this[int index] {`<br>`    get { return items[index]; }`<br>`    set { items[index] = value; OnChanged(); }`<br>`  }` | 索引器 |
| `  public void Add(T item) {`<br>`    if (count == Capacity) Capacity = count * 2;`<br>`    items[count] = item;`<br>`    count++;`<br>`    OnChanged();`<br>`  }`<br>`  protected virtual void OnChanged() {`<br>`    if (Changed != null) Changed(this, EventArgs.Empty);`<br>`  }`<br>`  public override bool Equals(object other) {`<br>`    return Equals(this, other as List<T>);`<br>`  }`<br>`  static bool Equals(List<T> a, List<T> b) {`<br>`    if (a == null) return b == null;`<br>`    if (b == null \|\| a.count != b.count) return false;`<br>`    for (int i = 0; i < a.count; i++)`<br>`      if (!object.Equals(a.items[i], b.items[i])) {`<br>`        return false;`<br>`      }`<br>`    return true;`<br>`  }` | 方法 |
| `  public event EventHandler Changed;` | 事件 |
| `  public static bool operator ==(List<T> a, List<T> b) {`<br>`    return Equals(a, b);`<br>`  }`<br>`  public static bool operator !=(List<T> a, List<T> b) {`<br>`    return !Equals(a, b);`<br>`  }` | 运算符 |
| `}` |  |

#### 1.6.7.1 构造函数

C#支持实例构造函数和静态构造函数。实例构造函数是一个成员，它实现了初始化类实例所需的操作。静态构造函数是一个成员，它在类首次加载时实现初始化类本身所需的操作。

构造函数的声明方式类似于方法，但没有返回类型，并且名称与包含它的类相同。如果构造函数声明包含`static`修饰符，则它声明的是静态构造函数。否则，它声明的是实例构造函数。

实例构造函数可以重载。例如，`List<T>`类声明了两个实例构造函数，一个没有参数，另一个接受一个`int`参数。实例构造函数使用`new`运算符调用。以下语句使用`List<T>`类的每个构造函数分配了两个`List<string>`实例。

```
List<string> list1 = new List<string>();
List<string> list2 = new List<string>(10);
```

与其他成员不同，实例构造函数不会被继承，并且除了类中实际声明的构造函数外，一个类没有其他实例构造函数。如果没有为类提供实例构造函数，则会自动提供一个无参数的空构造函数。

#### 1.6.7.2 属性

属性是字段的自然扩展。两者都是具有关联类型的命名成员，访问字段和属性的语法是相同的。然而，与字段不同，属性不表示存储位置。相反，属性具有访问器，这些访问器指定在读取或写入其值时要执行的语句。

属性的声明方式类似于字段，不同之处在于声明以`{`和`}`分隔符之间编写的`get`访问器和/或`set`访问器结尾，而不是以分号结尾。同时具有`get`访问器和`set`访问器的属性是读写属性，只有`get`访问器的属性是只读属性，只有`set`访问器的属性是只写属性。

`get`访问器对应于一个无参数且返回值为属性类型的方法。除了作为赋值的目标之外，当属性在表达式中被引用时，会调用该属性的`get`访问器来计算属性的值。

`set`访问器对应于一个具有名为`value`的单个参数且没有返回类型的方法。当属性作为赋值的目标或作为`++`或`--`的操作数被引用时，会使用提供新值的参数调用`set`访问器。

`List<T>`类声明了两个属性`Count`和`Capacity`，它们分别是只读和读写的。以下是使用这些属性的示例。

```
List<string> names = new List<string>();
names.Capacity = 100;      // Invokes set accessor
int i = names.Count;       // Invokes get accessor
int j = names.Capacity;    // Invokes get accessor
```

与字段和方法类似，C#支持实例属性和静态属性。静态属性使用`static`修饰符声明，而实例属性不使用它声明。

属性的访问器可以是虚的。当属性声明包含`virtual`、`abstract`或`override`修饰符时，该修饰符应用于属性的访问器。

#### 1.6.7.3 索引器

索引器是一个成员，它使对象能够像数组一样被索引。索引器的声明方式类似于属性，不同之处在于成员名称是`this`，后跟写在`[`和`]`分隔符之间的参数列表。这些参数在索引器的访问器中可用。与属性类似，索引器可以是读写的、只读的和只写的，并且索引器的访问器可以是虚的。

`List<T>`类声明了一个接受`int`参数的读写索引器。该索引器使得可以使用`int`值对`List<T>`实例进行索引。例如

```
List<string> names = new List<string>();
names.Add("Liz");
names.Add("Martha");
names.Add("Beth");
for (int i = 0; i < names.Count; i++) {
    string s = names[i];
    names[i] = s.ToUpper();
}
```

索引器可以重载，这意味着一个类可以声明多个索引器，只要它们的参数数量或类型不同即可。





#### 1.6.7.4 事件

事件是一种成员，它使类或对象能够提供通知。事件的声明方式与字段类似，只是声明中包括 event 关键字，并且类型必须是委托类型。

在声明了事件成员的类中，该事件的行为与委托类型的字段完全相同（前提是事件不是抽象的，并且未声明访问器）。该字段存储对委托的引用，该委托表示已添加到事件的事件处理程序。如果没有任何事件处理程序，则该字段为 null。

List<T> 类声明了一个名为 Changed 的事件成员，它表示列表中添加了新项。Changed 事件由 OnChanged 虚方法引发，该方法首先检查事件是否为 null（表示没有处理程序）。引发事件的概念与调用事件所表示的委托完全等价，因此，不存在用于引发事件的特殊语言构造。

客户端通过事件处理程序对事件作出反应。事件处理程序使用 += 运算符进行附加，使用 -= 运算符进行移除。以下示例向 List<string> 的 Changed 事件附加了一个事件处理程序。

```
using System;
class Test
{
    static int changeCount;
    static void ListChanged(object sender, EventArgs e) {
        changeCount++;
    }
    static void Main() {
        List<string> names = new List<string>();
        names.Changed += new EventHandler(ListChanged);
        names.Add("Liz");
        names.Add("Martha");
        names.Add("Beth");
        Console.WriteLine(changeCount);      // Outputs "3"
    }
}
```

对于需要控制事件底层存储的高级场景，事件声明可以显式提供 add 和 remove 访问器，这些访问器在某种程度上类似于属性的 set 访问器。

#### 1.6.7.5 运算符

运算符是一种成员，它定义了将特定表达式运算符应用于类实例时的含义。可以定义三种运算符：一元运算符、二元运算符和转换运算符。所有运算符都必须声明为 public 和 static。

List<T> 类声明了两个运算符：operator == 和 operator !=，从而为将这些运算符应用于 List 实例的表达式赋予了新的含义。具体而言，这些运算符将两个 List<T> 实例的相等性定义为使用它们各自的 Equals 方法比较所包含的每个对象。以下示例使用 == 运算符来比较两个 List<int> 实例。

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
        Console.WriteLine(a == b);    // Outputs "True"
        b.Add(3);
        Console.WriteLine(a == b);    // Outputs "False"
    }
}
```

第一个 Console.WriteLine 输出 True，因为这两个列表包含相同数量的对象，且这些对象的值和顺序都相同。如果 List<T> 没有定义 operator ==，那么第一个 Console.WriteLine 将输出 False，因为 a 和 b 引用的是不同的 List<int> 实例。

#### 1.6.7.6 析构函数

析构函数是一种成员，用于实现销毁类实例所需执行的操作。析构函数不能有参数，不能有可访问性修饰符，也不能被显式调用。实例的析构函数在垃圾回收过程中自动调用。

垃圾回收器在决定何时回收对象和运行析构函数方面有相当大的自由度。具体而言，析构函数调用的时机是不确定的，析构函数可能在任意线程上执行。由于这些及其它原因，类只应在没有其它可行解决方案时才实现析构函数。

using 语句提供了一种更好的对象销毁方法。

### 1.7 结构体

与类一样，结构体是包含数据成员和函数成员的数据结构，但与类不同，结构体是值类型，不需要堆分配。结构体类型的变量直接存储该结构体的数据，而类类型的变量存储对动态分配对象的引用。结构体类型不支持用户指定的继承，所有结构体类型都隐式继承自 object 类型。

结构体对于具有值语义的小型数据结构特别有用。复数、坐标系中的点、字典中的键值对都是结构体的绝佳示例。对于小型数据结构，使用结构体而非类可以显著影响应用程序执行的内存分配次数。例如，以下程序创建并初始化一个包含 100 个点的数组。如果将 Point 实现为类，则会实例化 101 个独立对象——一个用于数组，其余 100 个分别用于 100 个元素。

```
class Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

```
class Test
{
    static void Main() {
        Point[] points = new Point[100];
        for (int i = 0; i < 100; i++) points[i] = new Point(i, i);
    }
}
```

另一种做法是将 Point 设为结构体。

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

现在，只实例化了一个对象——用于数组的那个对象——Point 实例则内联存储在数组中。

结构体构造函数使用 new 运算符调用，但这并不意味着在分配内存。结构体构造函数不会动态分配对象并返回对它的引用，而是直接返回结构体值本身（通常在栈上的临时位置），然后根据需要复制该值。

对于类，两个变量有可能引用同一个对象，因此对一个变量执行的操作可能会影响另一个变量所引用的对象。而对于结构体，每个变量都有自己的数据副本，因此对一个变量执行的操作不可能影响另一个变量。例如，以下代码片段产生的输出取决于 Point 是类还是结构体。

```
Point a = new Point(10, 10);
Point b = a;
a.x = 20;
Console.WriteLine(b.x);
```

如果 Point 是类，输出为 20，因为 a 和 b 引用同一个对象。如果 Point 是结构体，输出为 10，因为将 a 赋给 b 会创建该值的一个副本，而 a.x 的后续赋值不会影响这个副本。

前面的例子突显了结构体的两个局限性。首先，复制整个结构体通常比复制对象引用效率更低，因此对于结构体而言，赋值和值参数传递可能比引用类型开销更大。其次，除了 ref 和 out 参数之外，无法创建对结构体的引用，这使得结构体在许多情况下无法使用。

### 1.8 数组

数组是一种数据结构，包含若干可通过计算索引访问的变量。数组中包含的变量（也称为数组的元素）都具有相同的类型，该类型称为数组的元素类型。

```csharp
using System;
class Test
{
    static void Main() {
        int[] a = new int[10];
        for (int i = 0; i < a.Length; i++) {
            a[i] = i * i;
        }
        for (int i = 0; i < a.Length; i++) {
            Console.WriteLine("a[{0}] = {1}", i, a[i]);
        }
    }
}
```

此示例创建并操作一个*一维数组*。C# 还支持*多维数组*。数组类型的维数（也称为数组类型的*秩*）等于数组类型的方括号之间逗号数量加一。以下示例分别分配一个一维数组、一个二维数组和一个三维数组。

```csharp
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
```

a1 数组包含 10 个元素，a2 数组包含 50（10 × 5）个元素，a3 数组包含 100（10 × 5 × 2）个元素。

数组的元素类型可以是任何类型，包括数组类型。元素类型为数组类型的数组有时称为*交错数组*，因为元素数组的长度不必都相同。以下示例分配一个元素为 `int` 数组的数组：

```csharp
int[][] a = new int[3][];
a[0] = new int[10];
a[1] = new int[5];
a[2] = new int[20];
```

第一行创建了一个包含三个元素的数组，每个元素的类型都是 `int[]`，且每个元素的初始值都为 `null`。随后几行使用对不同长度的各个数组实例的引用来初始化这三个元素。

new 运算符允许使用*数组初始值设定项*来指定数组元素的初始值，数组初始值设定项是写在分隔符 `{` 和 `}` 之间的表达式列表。以下示例分配并初始化一个包含三个元素的 `int[]`。

```csharp
int[] a = new int[] {1, 2, 3};
```

请注意，数组的长度是根据 `{` 和 `}` 之间表达式的数量推断出来的。局部变量和字段声明可以进一步缩短，从而无需重述数组类型。

```csharp
int[] a = {1, 2, 3};
```

以上两个示例都等同于以下代码：

```csharp
int[] t = new int[3];
t[0] = 1;
t[1] = 2;
t[2] = 3;
int[] a = t;
```

### 1.9 接口

*接口*定义了一个可由类和结构体实现的契约。接口可以包含方法、属性、事件和索引器。接口不提供其成员的实现，它


定义——它仅仅指定实现接口的类或结构体必须提供的成员。

接口可使用多重继承。以下示例中，接口 IComboBox 同时继承自 ITextBox 和 IListBox。

```csharp
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
interface IComboBox: ITextBox, IListBox {}
```

类和结构体可以实现多个接口。以下示例中，类 EditBox 同时实现 IControl 和 IDataBound。

```csharp
interface IDataBound
{
    void Bind(Binder b);
}
public class EditBox: IControl, IDataBound
{
    public void Paint() {...}
    public void Bind(Binder b) {...}
}
```

当类或结构体实现特定接口时，该类或结构体的实例可以隐式转换为该接口类型。例如

```csharp
EditBox editBox = new EditBox();
IControl control = editBox;
IDataBound dataBound = editBox;
```

在实例在静态上不确定是否实现特定接口的情况下，可以使用动态类型转换。例如，以下语句使用动态类型转换来获取对象的 IControl 和 IDataBound 接口实现。由于对象的实际类型是 EditBox，转换成功。

```csharp
object obj = new EditBox();
IControl control = (IControl)obj;
IDataBound dataBound = (IDataBound)obj;
```

在之前的 EditBox 类中，来自 IControl 接口的 Paint 方法和来自 IDataBound 接口的 Bind 方法使用公共成员实现。C# 还支持显式接口成员实现，通过它类或结构体可以避免将成员设为 public。显式接口成员实现使用完全限定的接口成员名称编写。例如，EditBox 类可以使用显式接口成员实现如下实现 IControl.Paint 和 IDataBound.Bind 方法。

```csharp
public class EditBox: IControl, IDataBound
{
    void IControl.Paint() {...}
    void IDataBound.Bind(Binder b) {...}
}
```

显式接口成员只能通过接口类型访问。例如，之前 EditBox 类提供的 IControl.Paint 实现只能在先将 EditBox 引用转换为 IControl 接口类型后才能调用。

```csharp
EditBox editBox = new EditBox();    // Error, no such method
editBox.Paint();
IControl control = editBox;         // Ok
control.Paint();
```

### 1.10 枚举

枚举类型是一种具有一组命名常量的独立值类型。以下示例声明并使用名为 Color 的枚举类型，具有三个常量值 Red、Green 和 Blue。

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

每个枚举类型都有一个对应的整型，称为枚举类型的底层类型。未显式声明底层类型的枚举类型的底层类型为 int。枚举类型的存储格式和可能值的范围由其底层类型决定。枚举类型可以取的值的集合不受其枚举成员的限制。特别是，枚举的底层类型的任何值都可以强制转换为枚举类型，并且是该枚举类型的有效且不同的值。

以下示例声明了一个名为 Alignment 的枚举类型，其底层类型为 sbyte。

```csharp
enum Alignment: sbyte
{
    Left = -1,
    Center = 0,
    Right = 1
}
```

如前例所示，枚举成员声明可以包含指定成员值的常量表达式。每个枚举成员的常量值必须在枚举的底层类型范围内。当枚举成员声明未显式指定值时，该成员被赋值为零（如果它是枚举类型中的第一个成员）或文本上前一个枚举成员的值加一。

枚举值可以通过类型转换转换为整型值，反之亦然。例如

```csharp
int i = (int)Color.Blue;    // int i = 2;
Color c = (Color)2;         // Color c = Color.Blue;
```

任何枚举类型的默认值都是整型值零转换为枚举类型。在变量自动初始化为默认值的情况下，这是赋予枚举类型变量的值。为了使枚举类型的默认值易于获取，字面量 0 可隐式转换为任何枚举类型。因此，以下写法是允许的。

```csharp
Color c = 0;
```

### 1.11 委托

委托类型表示具有特定参数列表和返回类型的方法引用。委托使方法能够作为可分配给变量并作为参数传递的实体来处理。委托类似于某些其他语言中函数指针的概念，但与函数指针不同，委托是面向对象且类型安全的。

以下示例声明并使用名为 Function 的委托类型。

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

Function 委托类型的实例可以引用任何接受 double 参数并返回 double 值的方法。Apply 方法将给定的 Function 应用于 double[] 的元素，返回包含结果的 double[]。在 Main 方法中，Apply 用于将三个不同的函数应用于 double[]。

委托可以引用静态方法（如前例中的 Square 或 Math.Sin）或实例方法（如前例中的 m.Multiply）。引用实例方法的委托还引用特定对象，并且当通过委托调用实例方法时，该对象在调用中成为 this。

委托也可以使用匿名函数创建，匿名函数是“内联方法”，即即时创建。匿名函数可以看到周围方法的局部变量。因此，上面的乘数示例可以更轻松地编写，而无需使用 Multiplier 类：

```csharp
double[] doubles = Apply(a, (double x) => x * 2.0);
```

委托的一个有趣且有用的特性是它不知道也不关心其引用的方法的类；唯一重要的是被引用方法具有与委托相同的参数和返回类型。

## 1.12 属性

C# 程序中的类型、成员和其他实体支持控制其行为某些方面的修饰符。例如，方法的访问性使用 public、protected、internal 和 private 修饰符控制。C# 将此功能概括为用户定义的声明性信息类型可以附加到程序实体并在运行时检索。程序通过定义和使用属性来指定此额外的声明性信息。

以下示例声明了一个 HelpAttribute 属性，可将其放置在程序实体上以提供指向其关联文档的链接。

```csharp
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
    public string Topic {
        get { return topic; }
        set { topic = value; }
    }
}
```

所有属性类都派生自 .NET Framework 提供的 System.Attribute 基类。

属性可以通过在相关声明前紧跟的方括号内给出其名称以及任何参数来应用。如果属性的名称以 Attribute 结尾，则在引用属性时可以省略该部分名称。例如，HelpAttribute 可如下使用。

```csharp
[Help("http://msdn.microsoft.com/.../MyClass.htm")]
public class Widget
{
    [Help("http://msdn.microsoft.com/.../MyClass.htm", Topic = "Display")]
    public void Display(string text) {}
}
```



此示例将 HelpAttribute 附加到 Widget 类，并将另一个 HelpAttribute 附加到该类中的 Display 方法。属性类的公共构造函数控制在将属性附加到程序实体时必须提供的信息。可以通过引用属性类的公共读写属性来提供附加信息（如之前对 Topic 属性的引用）。

以下示例展示了如何使用反射在运行时检索给定程序实体的属性信息。

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
            Console.WriteLine("  Url={0}, Topic={1}", a.Url, a.Topic);
        }
    }

    static void Main() {
        ShowHelp(typeof(Widget));
        ShowHelp(typeof(Widget).GetMethod("Display"));
    }
}
```

当通过反射请求特定属性时，将使用程序源中提供的信息调用属性类的构造函数，并返回由此产生的属性实例。如果通过属性提供了附加信息，则在返回属性实例之前，这些属性将被设置为给定值。

## 2. 词法结构

### 2.1 程序

C# 程序由一个或多个源文件组成，正式称为编译单元（§9.1）。源文件是有序的 Unicode 字符序列。源文件通常与文件系统中的文件一一对应，但这种对应关系不是必需的。为了最大限度地提高可移植性，建议将文件系统中的文件使用 UTF-8 编码。

概念上讲，程序的编译使用三个步骤：

- 1. 转换，将文件从特定的字符集和编码方案转换为 Unicode 字符序列。
- 2. 词法分析，将 Unicode 输入字符流转换为标记流。
- 3. 语法分析，将标记流转换为可执行代码。

### 2.2 语法

本规范使用两种语法来描述 C# 编程语言的语法。词法语法（§2.2.2）定义了 Unicode 字符如何组合形成行终止符、空白、注释、标记和预处理指令。语法语法（§2.2.3）定义了词法语法产生的标记如何组合形成 C# 程序。

### 2.2.1 语法记法

词法和语法语法使用语法产生式呈现。每个语法产生式定义一个非终结符以及该非终结符可能扩展为非终结符或终结符序列。 在语法产生式中，非终结符以斜体显示，而终结符以等宽字体显示。

语法产生式的第一行是非终结符的名称，后跟冒号。每个后续缩进的行包含非终结符的可能扩展，表示为非终结符或终结符的序列。例如，产生式：

```
while-statement:
    while ( boolean-expression ) embedded-statement
```

定义 while-statement 由标记 while 组成，后跟标记“（”，后跟 boolean-expression，后跟标记“）”，后跟 embedded-statement。

当非终结符有多个可能的扩展时，备选方案会列在单独的行上。例如，产生式：

是简写形式：

```
~~~
    block:
        {   }
        {   statement-list   }
~~~
```

并定义 *block* 由可选的 *statement-list* 组成，被“{”和“}”标记包围。

备选方案通常列在单独的行上，尽管在备选方案很多的情况下，短语“one of”可能会先于在一行上给出的扩展列表。这只是逐行列出每个备选方案的简写形式。例如，产生式：

```
~~~
    real-type-suffix:  one of
        F   f   D   d   M   m
~~~
```

是简写形式：

```
~~~
    real-type-suffix:
        F
        f
        D
        d
        M
        m
~~~
```

### 2.2.2 词法语法

C# 的词法语法在 §2.3、§2.4 和 §2.5 中呈现。词法语法的终结符是 Unicode 字符集的字符，词法语法指定字符如何组合形成标记（§2.4）、空白（§2.3.3）、注释（§2.3.2）和预处理指令（§2.5）。

C# 程序中的每个源文件必须符合词法语法（§2.3）的 *input* 产生式。

### 2.2.3 语法语法

C# 的语法语法在随后本章的章节和附录中呈现。语法语法的终结符是由词法语法定义的标记，语法语法指定标记如何组合形成 C# 程序。

C# 程序中的每个源文件必须符合语法语法（§9.1）的 *compilation-unit* 产生式。

### 2.3 词法分析

*input* 产生式定义了 C# 源文件的词法结构。C# 程序中的每个源文件必须符合此词法语法产生式。

```
~~~
    input:
        input-section_opt

    input-section:
        input-section-part
        input-section  input-section-part

    input-section-part:
        input-elements_opt  new-line
        pp-directive
~~~
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

五个基本元素构成了 C# 源文件的词法结构：行终止符（§2.3.1）、空白（§2.3.3）、注释（§2.3.2）、标记（§2.4）和预处理指令（§2.5）。在这些基本元素中，只有标记在 C# 程序的语法语法（§2.2.3）中才有意义。

C# 源文件的词法处理包括将文件简化为标记序列，该序列成为语法分析的输入。行终止符、空白和注释可以用于分隔标记，预处理指令可以导致源文件的某些部分被跳过，但除此之外，这些词法元素对 C# 程序的语法结构没有影响。

当多个词法语法产生式匹配源文件中的字符序列时，词法处理总是形成最长的可能词法元素。例如，字符序列 // 被处理为单行注释的开始，因为该词法元素比单个 / 标记更长。

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

为了与添加文件结束标记的源代码编辑工具兼容，并使源文件能够作为一系列正确终止的行来查看，以下转换按顺序应用于 C# 程序中的每个源文件：

- 如果源文件的最后一个字符是 Control-Z 字符（U+001A），则删除该字符。
- 如果源文件非空且源文件的最后一个字符不是回车（U+000D）、换行（U+000A）、行分隔符（U+2028）或段落分隔符（U+2029），则在源文件末尾添加一个回车字符（U+000D）。

### 2.3.2 注释

支持两种形式的注释：单行注释和定界注释。单行注释以字符 // 开始并延伸到源行末尾。定界注释以字符 /* 开始并以字符 */ 结束。定界注释可以跨越多行。

```
comment:
  single-line-comment
  delimited-comment

single-line-comment:
  // input-characters_opt
```

输入字符：
    输入字符
    输入字符  输入字符

输入字符：
    除换行字符外的任何 Unicode 字符

换行字符：
    回车字符 (U+000D)
    换行符 (U+000A)
    下一行字符 (U+0085)
    行分隔符字符 (U+2028)
    段落分隔符字符 (U+2029)

分隔注释：
    /* 分隔注释文本_opt 星号 /

分隔注释文本：
    分隔注释段
    分隔注释文本 分隔注释段

分隔注释段：
    /
    星号_opt 非斜杠或星号

星号：
    *
    星号 *

非斜杠或星号：
    除 / 或 * 外的任何 Unicode 字符

注释不嵌套。字符序列 /* 和 */ 在 // 注释中没有特殊含义，字符序列 // 和 /* 在分隔注释中没有特殊含义。

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
class Hello // any name will do for this class
{
    static void Main() { // this method must be named "Main"
        System.Console.WriteLine("hello, world");
    }
}
```

展示了多个单行注释。

### 2.3.3 空白

空白定义为 Unicode 类别为 Zs 的任何字符（包括空格字符），以及水平制表符、垂直制表符和换页符。

-   空白：
-   - Unicode 类别为 Zs 的任何字符
-   - 水平制表符 (U+0009)
-   - 垂直制表符 (U+000B)
-   - 换页符 (U+000C)

## 2.4 标记

标记有几种：标识符、关键字、字面量、运算符和标点符号。空白和注释不是标记，但它们充当标记的分隔符。

-   标记：
-   - 标识符
-   - 关键字
-   - 整数字面量
-   - 实数字面量
-   - 字符字面量
-   - 字符串字面量
-   - 运算符或标点符号

### 2.4.1 Unicode 字符转义序列

Unicode 字符转义序列表示一个 Unicode 字符。Unicode 字符转义序列在标识符（§2.4.2）、字符字面量（§2.4.4.4）和常规字符串字面量（§2.4.4.5）中被处理。Unicode 字符转义不在任何其他位置处理（例如，用于形成运算符、标点符号或关键字）。

-   Unicode 转义序列：
-   - \u 十六进制数字 十六进制数字 十六进制数字 十六进制数字
-   - \U 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字

Unicode 转义序列表示由 "\u" 或 "\U" 字符后面的十六进制数字形成的单个 Unicode 字符。由于 C# 在字符和字符串值中使用 Unicode 码点的 16 位编码，因此字符字面量中不允许使用 U+10000 到 U+10FFFF 范围内的 Unicode 字符，并且在字符串字面量中使用 Unicode 代理项对来表示。不支持码点高于 0x10FFFF 的 Unicode 字符。

不执行多次转换。例如，字符串字面量 "\u005Cu005C" 等效于 "\u005C" 而不是 "\\"。Unicode 值 \u005C 是字符 "\"。

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

展示了 \u0066 的几种用法，它是字母 "f" 的转义序列。该程序等效于

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

本节给出的标识符规则与 Unicode 标准附录 31 推荐的规则完全一致，不同之处在于允许下划线作为起始字符（这是 C 编程语言的传统），标识符中允许使用 Unicode 转义序列，并且允许 “@” 字符作为前缀，以便关键字可以用作标识符。

-   - *标识符：*
-     - *可用标识符*
-     - **@** *标识符或关键字*
-   - *可用标识符：*
-     - 一个不是 *关键字* 的 *标识符或关键字*
-   - *标识符或关键字：*
-     - *标识符起始字符* *标识符部分字符*_opt
-   - *标识符起始字符：*
-     - *字母字符*
-     - `_`（下划线字符 U+005F）
-   - *标识符部分字符：*
-     - *标识符部分字符*
-     - *标识符部分字符* *标识符部分字符*
-   - *标识符部分字符：*
-     - *字母字符*
-     - *十进制数字字符*
-     - *连接字符*
-     - *组合字符*
-     - *格式化字符*
-   - *字母字符：*
-     - Unicode 类别为 Lu、Ll、Lt、Lm、Lo 或 Nl 的字符
-     - 表示类别为 Lu、Ll、Lt、Lm、Lo 或 Nl 的字符的 *Unicode 转义序列*
-   - *组合字符：*
-     - Unicode 类别为 Mn 或 Mc 的字符
-     - 表示类别为 Mn 或 Mc 的字符的 *Unicode 转义序列*
-   - *十进制数字字符：*
-     - Unicode 类别为 Nd 的字符
-     - 表示类别为 Nd 的字符的 *Unicode 转义序列*
-   - *连接字符：*
-     - Unicode 类别为 Pc 的字符
-     - 表示类别为 Pc 的字符的 *Unicode 转义序列*
-   - *格式化字符：*
-     - Unicode 类别为 Cf 的字符
-     - 表示类别为 Cf 的字符的 *Unicode 转义序列*

关键字：以下之一
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

在语法的某些地方，特定标识符具有特殊含义，但不是关键字。此类标识符有时称为“上下文关键字”。例如，在属性声明中，“get”和“set”标识符具有特殊含义（§10.7.2）。在这些位置，除 get 或 set 之外的标识符永远不允许出现，因此这种用法不会与这些词作为标识符的用法冲突。在其他情况下，例如在隐式类型局部变量声明（§8.5.1）中的标识符“var”，上下文关键字可能与声明的名称冲突。在这种情况下，声明的名称优先于将该标识符用作上下文关键字。

## 2.4.4 字面量

字面量是值的源代码表示。

-   字面量：
-   布尔字面量
-   整数字面量
-   实数字面量
-   字符字面量
-   字符串字面量
-   null 字面量

### 2.4.4.1 布尔字面量

布尔字面量有两个值：true 和 false。

-   布尔字面量：
-   true
-   false

布尔字面量的类型是 bool。

### 2.4.4.2 整数字面量

整数字面量用于写入 int、uint、long 和 ulong 类型的值。整数字面量有两种可能的形式：十进制和十六进制。

-   整数字面量：
-   十进制整数字面量
-   十六进制整数字面量

十进制整数字面量：
    十进制数字 整数类型后缀_opt

十进制数字：
    十进制数字
    十进制数字 十进制数字

十进制数字：以下之一
    0 1 2 3 4 5 6 7 8 9

整数类型后缀：以下之一
    U u L l UL uL Ul ul LU Lu lU lu

十六进制整数字面量：
    0x 十六进制数字 整数类型后缀_opt
    0X 十六进制数字 整数类型后缀_opt

十六进制数字：
    十六进制数字
    十六进制数字 十六进制数字

十六进制数字：以下之一
    0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f

整数字面量的类型确定如下：

-   - 如果字面量没有后缀，则其类型为能够表示其值的这些类型中的第一个：int、uint、long、ulong。
-   - 如果字面量带有 U 或 u 后缀，则其类型为能够表示其值的这些类型中的第一个：uint、ulong。
-   - 如果字面量带有 L 或 l 后缀，则其类型为能够表示其值的这些类型中的第一个：long、ulong。
-   - 如果字面量带有 UL、uL、Ul、ul、LU、Lu、lU 或 lu 后缀，则其类型为 ulong。

如果整数字面量表示的值超出 ulong 类型的范围，则发生编译时错误。

作为一种风格，建议在编写 long 类型的字面量时使用 "L" 而不是 "l"，因为字母 "l" 很容易与数字 "1" 混淆。

为了允许将尽可能最小的 int 和 long 值写成十进制整数字面量，存在以下两条规则：

-   - 当值为 2147483648 (2^31) 且没有整数类型后缀的十进制整数字面量作为一元减号运算符标记（§7.7.2）后面紧跟的标记出现时，结果是类型为 int 且值为 −2147483648 (−2^31) 的常量。在所有其他情况下，此类十进制整数字面量的类型为 uint。
-   - 当值为 9223372036854775808 (2^63) 且没有整数类型后缀或整数类型后缀为 L 或 l 的十进制整数字面量作为一元减号运算符标记（§7.7.2）后面紧跟的标记出现时，结果是类型为 long 且值为 −9223372036854775808 (−2^63) 的常量。在所有其他情况下，此类十进制整数字面量的类型为 ulong。

### 2.4.4.3 实数字面量

实数字面量用于写入 float、double 和 decimal 类型的值。



real-literal:
  decimal-digits . decimal-digits exponent-part_opt real-type-suffix_opt
  . decimal-digits exponent-part_opt real-type-suffix_opt
  decimal-digits exponent-part real-type-suffix_opt
  decimal-digits real-type-suffix

exponent-part:
  e sign_opt decimal-digits
  E sign_opt decimal-digits

sign: one of
  +  -

real-type-suffix: one of
  F f D d M m

如果未指定 real-type-suffix，则实数字面量的类型为 double。否则，实数类型后缀决定实数字面量的类型，如下所示：

- 以 F 或 f 为后缀的实数字面量的类型为 float。例如，字面量 1f、1.5f、1e10f 和 123.456F 均为 float 类型。
- 以 D 或 d 为后缀的实数字面量的类型为 double。例如，字面量 1d、1.5d、1e10d 和 123.456D 均为 double 类型。
- 以 M 或 m 为后缀的实数字面量的类型为 decimal。例如，字面量 1m、1.5m、1e10m 和 123.456M 均为 decimal 类型。此字面量通过采用精确值转换为 decimal 值，如有必要，使用银行家舍入法（§4.1.7）舍入到最接近的可表示值。除非值被舍入或值为零（在后一种情况下，符号和小数位数为 0），否则字面量中呈现的任何小数位数都将保留。因此，字面量 2.900m 将被解析为符号为 0、系数为 2900、小数位数为 3 的 decimal。

如果指定的字面量无法用所指示的类型表示，则发生编译时错误。

float 或 double 类型的实数字面量的值通过使用 IEEE“就近舍入”模式确定。

注意，在实数字面量中，小数点后始终需要十进制数字。例如，1.3F 是实数字面量，但 1.F 不是。

## 2.4.4.4 字符字面量

字符字面量表示单个字符，通常由引号中的字符组成，如 'a'。

```
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
```

在 character 中，反斜杠字符（\）后面的字符必须是以下字符之一：`'`、`"`、`\`、`0`、`a`、`b`、`f`、`n`、`r`、`t`、`u`、`U`、`x`、`v`。否则，发生编译时错误。

十六进制转义序列表示单个 Unicode 字符，其值由 `\x` 后面的十六进制数构成。

如果字符字面量表示的值大于 U+FFFF，则发生编译时错误。

字符字面量中的 Unicode 字符转义序列（§2.4.1）必须在 U+0000 到 U+FFFF 的范围内。

简单转义序列表示 Unicode 字符编码，如下表所述。

| 转义序列 | 字符名称 | Unicode 编码 |
|---|---|---|
| \' | 单引号 | 0x0027 |
| \" | 双引号 | 0x0022 |
| \\ | 反斜杠 | 0x005C |
| \0 | 空字符 | 0x0000 |
| \a | 警报 | 0x0007 |
| \b | 退格 | 0x0008 |
| \f | 换页 | 0x000C |
| \n | 换行 | 0x000A |
| \r | 回车 | 0x000D |
| \t | 水平制表符 | 0x0009 |
| \v | 垂直制表符 | 0x000B |

字符字面量的类型为 char。

## 2.4.4.5 字符串字面量

C# 支持两种形式的字符串字面量：常规字符串字面量和逐字字符串字面量。

常规字符串字面量由双引号括起来的零个或多个字符组成，如 "hello"，并且可以包括简单转义序列（例如表示制表符的 \t）以及十六进制和 Unicode 转义序列。

逐字字符串字面量由 @ 字符后跟双引号字符、零个或多个字符以及结尾双引号字符组成。一个简单的示例是 @"hello"。在逐字字符串字面量中，分隔符之间的字符按原样解释，唯一例外是引号转义序列。特别是，简单转义序列以及十六进制和 Unicode 转义序列不会在逐字字符串字面量中处理。逐字字符串字面量可以跨越多行。

```
string-literal:
    regular-string-literal
    verbatim-string-literal

regular-string-literal:
    " regular-string-literal-characters_opt "
```

regular-string-literal-characters:
    regular-string-literal-character
    regular-string-literal-characters   regular-string-literal-character

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
    verbatim-string-literal-characters   verbatim-string-literal-character

verbatim-string-literal-character:
    single-verbatim-string-literal-character
    quote-escape-sequence

single-verbatim-string-literal-character:
    Any character except "

quote-escape-sequence:
    ""

在 regular-string-literal-character 中，反斜杠字符（\）后面的字符必须是以下字符之一：`'`、`"`、`\`、`0`、`a`、`b`、`f`、`n`、`r`、`t`、`u`、`U`、`x`、`v`。否则，发生编译时错误。

示例

```csharp
string a = "hello, world";                   // hello, world
string b = @"hello, world";                  // hello, world
string c = "hello \t world";                 // hello    world
string d = @"hello \t world";                // hello \t world
string e = "Joe said \"Hello\" to me";       // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me";      // Joe said "Hello" to me
string g = "\\\\server\\share\\file.txt";    // \\server\share\file.txt
string h = @"\\server\share\file.txt";       // \\server\share\file.txt
string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```

展示了各种字符串字面量。最后一个字符串字面量 j 是跨越多行的逐字字符串字面量。引号之间的字符，包括换行字符等空白，均按原样保留。

由于十六进制转义序列可以具有可变数量的十六进制数字，字符串字面量 "\x123" 包含一个十六进制值为 123 的单个字符。要创建包含十六进制值为 12 的字符后跟字符 3 的字符串，可以改为编写 "\x00123" 或 "\x12" + "3"。

字符串字面量的类型为 string。

## 2.4.4.6 null 字面量

```
null-literal:
    null
```

null 字面量可以隐式转换为引用类型或可空类型。

## 2.4.5 运算符和标点符号

有多种运算符和标点符号。运算符用于表达式中，描述涉及一个或多个操作数的运算。例如，表达式 a + b 使用 + 运算符将两个操作数 a 和 b 相加。标点符号用于分组和分隔。

operator-or-punctuator: one of
{ } [ ] ( ) . , : ;
+ - * / % & | ^ ! ~
= < > ? ?? :: ++ --
-> == != <= >= += -= *=
&= |= ^= <<= >>= =>

```
right-shift:
    >|>
```

```
right-shift-assignment:
    >|=
```

right-shift 和 right-shift-assignment 产生式中的竖线用于指示：与句法语法中的其他产生式不同，标记之间不允许出现任何字符（甚至空白）。这些产生式被特殊处理，以便能够正确处理 type-parameter-lists（§10.1.3）。

## 2.5 预处理指令

预处理指令提供了有条件地跳过源文件部分、报告错误和警告条件以及描绘源代码不同区域的能力。“预处理指令”这一术语仅用于与 C 和 C++ 编程语言保持一致。在 C# 中，没有单独的预处理步骤；预处理指令作为词法分析阶段的一部分进行处理。

pp-directive:
- pp-declaration
- pp-conditional
- pp-line
- pp-diagnostic
- pp-region
- pp-pragma



以下预处理指令可用：

-   `#define` 和 `#undef`，分别用于定义和取消定义条件编译符号 (§2.5.3)。
-   `#if`、`#elif`、`#else` 和 `#endif`，用于有条件地跳过源代码的某些部分 (§2.5.4)。
-   `#line`，用于控制错误和警告所发出的行号 (§2.5.7)。
-   `#error` 和 `#warning`，分别用于发出错误和警告 (§2.5.5)。
-   `#region` 和 `#endregion`，用于显式标记源代码的各部分 (§2.5.6)。
-   `#pragma`，用于向编译器指定可选的上下文信息 (§2.5.8)。

预处理指令始终占用源代码的单独一行，并且始终以 # 字符和预处理指令名称开头。在 # 字符之前以及 # 字符与指令名称之间可以出现空白。

包含 #define、#undef、#if、#elif、#else、#endif 或 #line 指令的源行可以以单行注释结束。分隔注释（/* */ 风格的注释）在包含预处理指令的源行上是不允许的。

预处理指令不是标记，也不是 C# 语法文法的一部分。然而，预处理指令可用于包含或排除标记序列，从而以这种方式影响 C# 程序的含义。例如，编译时，程序：

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

结果产生的标记序列与以下程序完全相同：

```csharp
class C
{
    void F() {}
    void I() {}
}
```

因此，虽然在词法上这两个程序差异很大，但在语法上它们是相同的。

## 2.5.1 条件编译符号

#if、#elif、#else 和 #endif 指令提供的条件编译功能通过预处理表达式 (§2.5.2) 和条件编译符号控制。

```
conditional-symbol:
    Any identifier-or-keyword except true or false
```

条件编译符号有两种可能的状态：**已定义** 或 **未定义**。在源文件的词法处理开始时，条件编译符号为未定义，除非它已被外部机制（例如命令行编译器选项）显式定义。当处理 #define 指令时，该指令中命名的条件编译符号在该源文件中变为已定义。该符号保持已定义状态，直到处理了针对同一符号的 #undef 指令，或直到到达源文件末尾为止。其含义之一是，一个源文件中的 #define 和 #undef 指令对同一程序中的其他源文件没有影响。

在预处理表达式中引用时，已定义的条件编译符号具有布尔值 true，而未定义的条件编译符号具有布尔值 false。条件编译符号在预处理表达式中被引用之前无需显式声明。相反，未声明的符号只是未定义，因此其值为 false。

条件编译符号的命名空间与 C# 程序中的所有其他命名实体是独立且分开的。条件编译符号只能在 #define 和 #undef 指令以及预处理表达式中引用。

## 2.5.2 预处理表达式

预处理表达式可以出现在 #if 和 #elif 指令中。运算符 !、==、!=、&& 和 || 在预处理表达式中允许使用，并且可以使用括号进行分组。

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

在预处理表达式中引用时，已定义的条件编译符号具有布尔值 true，而未定义的条件编译符号具有布尔值 false。

预处理表达式的求值始终产生布尔值。预处理表达式的求值规则与常量表达式 (§7.19) 的规则相同，只是唯一可以引用的用户定义实体是条件编译符号。

## 2.5.3 声明指令

声明指令用于定义或取消定义条件编译符号。

```
pp-declaration:
  whitespace_opt # whitespace_opt define whitespace conditional-symbol pp-new-line
  whitespace_opt # whitespace_opt undef whitespace conditional-symbol pp-new-line

pp-new-line:
  whitespace_opt single-line-comment_opt new-line
```

处理 #define 指令会导致给定的条件编译符号从指令之后的源行开始变为已定义。同样，处理 #undef 指令会导致给定的条件编译符号从指令之后的源行开始变为未定义。

源文件中的任何 #define 和 #undef 指令必须出现在源文件中的第一个标记 (§2.4) 之前；否则会发生编译时错误。直观地说，#define 和 #undef 指令必须位于源文件中的任何“实际代码”之前。

示例：

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

是有效的，因为 #define 指令位于源文件中的第一个标记（namespace 关键字）之前。

以下示例会导致编译时错误，因为 #define 出现在实际代码之后：

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

## 2.5.4 条件编译指令

条件编译指令用于有条件地包含或排除源文件的部分内容。

```
pp-conditional:
  pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif

pp-if-section:
    whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line conditional-section_opt
pp-elif-sections:
    pp-elif-section
    pp-elif-sections pp-elif-section
pp-elif-section:
    whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line conditional-section_opt
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

如语法所示，条件编译指令必须作为集合编写，按顺序包括 #if 指令、零个或多个 #elif 指令、零个或一个 #else 指令以及一个 #endif 指令。指令之间是源代码的条件部分。每个部分由紧邻其前面的指令控制。条件部分本身可以包含嵌套的条件编译指令，前提是这些指令构成完整的集合。

pp-conditional 最多选择其中一个包含的条件部分进行正常的词法处理：

-   #if 和 #elif 指令的 pp-expression 按顺序求值，直到有一个产生 true。如果某个表达式产生 true，则选择对应指令的条件部分。
-   如果所有 pp-expression 都产生 false，并且存在 #else 指令，则选择 #else 指令的条件部分。
-   否则，不选择任何条件部分。

如果有被选中的条件部分，则将其作为正常的 input-section 处理：该部分包含的源代码必须遵循词法语法；从该部分中的源代码生成标记；并且该部分中的预处理指令具有规定的效果。

剩余的条件部分（如果有）则作为 skipped-section 处理：除预处理指令外，该部分中的源代码无需遵循词法语法；不会从该部分中的源代码生成标记；并且该部分中的预处理指令必须在词法上正确但不是

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

入口点，无论其声明的可访问性如何，也无论其外层类型声明的可访问性如何。

应用程序入口点方法不得位于泛型类声明中。

在所有其他方面，入口点方法的行为与非入口点方法相同。

## 3.2 应用程序终止

应用程序终止会将控制权返回给执行环境。

如果应用程序入口点方法的返回类型为 int，则返回的值用作应用程序的终止状态代码。此代码的用途是允许将成功或失败传达给执行环境。

如果入口点方法的返回类型为 void，则到达终止该方法的右花括号 {}，或执行不带表达式的 return 语句，都会导致终止状态代码为 0。

在应用程序终止之前，会调用其所有尚未被垃圾回收的对象的析构函数，除非此类清理已被抑制（例如，通过调用库方法 GC.SuppressFinalize）。

## 3.3 声明

C# 程序中的声明定义程序的构成元素。C# 程序使用命名空间（§9）组织，命名空间可以包含类型声明和嵌套命名空间声明。类型声明（§9.6）用于定义类（§10）、结构（§10.14）、接口（§13）、枚举（§14）和委托（§15）。类型声明中允许的成员种类取决于类型声明的形式。例如，类声明可以包含常量（§10.4）、字段（§10.5）、方法（§10.6）、属性（§10.7）、事件（§10.8）、索引器（§10.9）、运算符（§10.10）、实例构造函数（§10.11）、静态构造函数（§10.12）、析构函数（§10.13）和嵌套类型（§10.3.8）的声明。

声明会在该声明所属的声明空间中定义一个名称。除重载成员（§3.6）外，在一个声明空间中存在两个或更多引入同名成员的声明属于编译时错误。声明空间绝不可能包含具有相同名称的不同种类成员。例如，声明空间绝不能包含具有相同名称的字段和方法。

声明空间有几种不同类型，如下所述。

-   在程序的所有源文件中，没有外层命名空间声明的命名空间成员声明是一个名为全局声明空间的单一组合声明空间的成员。
-   在程序的所有源文件中，具有相同完全限定命名空间名的命名空间声明内的命名空间成员声明是一个单一组合声明空间的成员。
-   每个类、结构或接口声明都会创建一个新的声明空间。名称通过类成员声明、结构成员声明、接口成员声明或类型参数引入此声明空间。除重载实例构造函数声明和静态构造函数声明外，类或结构不能包含与类或结构同名的成员声明。类、结构或接口允许声明重载方法和索引器。此外，类或结构允许声明重载实例构造函数和运算符。例如，类、结构或接口可以包含多个同名方法声明，前提是这些方法声明在签名（§3.6）上不同。请注意，基类不会构成类的声明空间的一部分，基接口不会构成接口的声明空间的一部分。因此，派生类或接口可以声明与继承成员同名的成员。这种成员称为隐藏继承成员。
-   每个委托声明都会创建一个新的声明空间。名称通过形参（*固定参数* 和 *参数数组*）以及 *类型参数* 引入此声明空间。
-   每个枚举声明都会创建一个新的声明空间。名称通过 *枚举成员声明* 引入此声明空间。
-   每个方法声明、索引器声明、运算符声明、实例构造函数声明和匿名函数都会创建一个新的声明空间，称为 *局部变量声明空间*。名称通过形参（*固定参数* 和 *参数数组*）以及 *类型参数* 引入此声明空间。函数成员或匿名函数的主体（如果有）被视为嵌套在该局部变量声明空间内。局部变量声明空间和嵌套的局部变量声明空间包含同名元素是错误的。因此，在嵌套声明空间内，不能声明与外围声明空间中的局部变量或常量同名的局部变量或常量。两个声明空间可以包含同名元素，只要这两个声明空间互不包含。
-   每个 *块* 或 *switch 块*，以及 *for*、*foreach* 和 *using* 语句，都会为局部变量和局部常量创建局部变量声明空间。名称通过 *局部变量声明* 和 *局部常量声明* 引入此声明空间。注意，作为函数成员或匿名函数主体出现或位于其内的块，会嵌套在这些函数为其参数声明的局部变量声明空间内。因此，例如，方法具有同名的局部变量和参数是错误的。
-   每个 *块* 或 *switch 块* 都会为标签创建单独的声明空间。名称通过 *带标签语句* 引入此声明空间，并通过 *goto 语句* 引用这些名称。块的 *标签声明空间* 包括任何嵌套块。因此，在嵌套块内，不能声明与外围块中的标签同名的标签。

名称声明的文本顺序通常无关紧要。尤其对于命名空间、常量、方法、属性、事件、索引器、运算符、实例构造函数、析构函数、静态构造函数和类型的声明与使用，文本顺序并不重要。声明顺序在以下方面很重要：

-   字段声明和局部变量声明的声明顺序决定其初始化器（如果有）的执行顺序。
-   局部变量必须先定义后使用（§3.7）。
-   当省略 *常量表达式* 值时，枚举成员声明（§14.3）的声明顺序很重要。

命名空间的声明空间是“开放式的”，具有相同完全限定名的两个命名空间声明会构成同一个声明空间。例如

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

上面的两个命名空间声明构成同一个声明空间，在本例中声明了两个类，其完全限定名分别为 Megacorp.Data.Customer 和 Megacorp.Data.Order。由于这两个声明构成同一个声明空间，如果每个声明都包含一个同名类的声明，就会导致编译时错误。

如上所述，块的声明空间包括任何嵌套块。因此，在下面的示例中，F 和 G 方法会导致编译时错误，因为名称 i 在外层块中声明，不能在内部块中重新声明。但是，H 和 I 方法是有效的，因为两个 i 是在互不嵌套的单独块中声明的。

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

## 3.4 成员

命名空间和类型具有成员。通常可以通过限定名访问实体的成员，该限定名以对实体的引用开头，后跟一个“.”标记，再跟成员名。

类型的成员要么在类型声明中声明，要么从该类型的基类继承。当类型从基类继承时，基类的所有成员（实例构造函数、析构函数和静态构造函数除外）都会成为派生类型的成员。基类成员的声明可访问性并不控制该成员是否被继承——继承适用于任何不是实例构造函数、静态构造函数或析构函数的成员。但是，继承的成员在派生类型中可能不可访问，原因可能是其声明可访问性（§3.5.1），也可能是它被该类型自身中的声明隐藏（§3.7.1.2）。

### 3.4.1 命名空间成员

没有外层命名空间的命名空间和类型是全局命名空间的成员。这直接对应于全局声明空间中声明的名称。



在命名空间中声明的命名空间和类型是该命名空间的成员。这直接对应于该命名空间的声明空间中声明的名称。

命名空间没有访问限制。不能声明私有、受保护或内部命名空间，并且命名空间名称始终可公开访问。

### 3.4.2 结构体成员

结构体的成员是在该结构体中声明的成员，以及从该结构体的直接基类 `System.ValueType` 和间接基类 `object` 继承的成员。

简单类型的成员直接对应于该简单类型所别名的结构体类型的成员：

- `sbyte` 的成员是 `System.SByte` 结构体的成员。
- `byte` 的成员是 `System.Byte` 结构体的成员。
- `short` 的成员是 `System.Int16` 结构体的成员。
- `ushort` 的成员是 `System.UInt16` 结构体的成员。
- `int` 的成员是 `System.Int32` 结构体的成员。
- `uint` 的成员是 `System.UInt32` 结构体的成员。
- `long` 的成员是 `System.Int64` 结构体的成员。
- `ulong` 的成员是 `System.UInt64` 结构体的成员。
- `char` 的成员是 `System.Char` 结构体的成员。
- `float` 的成员是 `System.Single` 结构体的成员。
- `double` 的成员是 `System.Double` 结构体的成员。
- `decimal` 的成员是 `System.Decimal` 结构体的成员。
- `bool` 的成员是 `System.Boolean` 结构体的成员。

### 3.4.3 枚举成员

枚举的成员是在该枚举中声明的常量，以及从该枚举的直接基类 `System.Enum` 和间接基类 `System.ValueType` 和 `object` 继承的成员。

### 3.4.4 类成员

类的成员是在该类中声明的成员，以及从基类继承的成员（类 `object` 除外，它没有基类）。从基类继承的成员包括基类的常量、字段、方法、属性、事件、索引器、运算符和类型，但不包括基类的实例构造函数、析构函数和静态构造函数。基类成员被继承时不考虑其可访问性。

类声明可以包含常量、字段、方法、属性、事件、索引器、运算符、实例构造函数、析构函数、静态构造函数和类型的声明。

`object` 和 `string` 的成员直接对应于它们所别名的类类型的成员：

- `object` 的成员是 `System.Object` 类的成员。
- `string` 的成员是 `System.String` 类的成员。

### 3.4.5 接口成员

接口的成员是在该接口以及该接口的所有基接口中声明的成员。严格来说，类 object 中的成员不是任何接口的成员（§13.2）。但是，类 object 中的成员可通过任何接口类型中的成员查找来使用（§7.4）。

### 3.4.6 数组成员

数组的成员是从类 System.Array 继承的成员。

### 3.4.7 委托成员

委托的成员是从类 System.Delegate 继承的成员。

## 3.5 成员访问

成员声明允许控制成员访问。成员的可访问性由该成员的声明可访问性（§3.5.1）与直接包含类型（如果有）的可访问性共同确定。

当允许访问特定成员时，称该成员可访问。相反，当不允许访问特定成员时，称该成员不可访问。当进行访问的文本位置包含于该成员的可访问性域（§3.5.2）中时，才允许访问该成员。

### 3.5.1 声明可访问性

成员的声明可访问性可以是以下之一：

- 公共（Public），通过在成员声明中包含 `public` 修饰符选择。`public` 的直观含义是“访问不受限制”。
- 受保护（Protected），通过在成员声明中包含 `protected` 修饰符选择。`protected` 的直观含义是“访问限于包含类或派生自包含类的类型”。
- 内部（Internal），通过在成员声明中包含 `internal` 修饰符选择。`internal` 的直观含义是“访问限于此程序”。
- 受保护的内部（Protected internal，即 protected 或 internal），通过在成员声明中同时包含 `protected` 和 `internal` 修饰符选择。`protected internal` 的直观含义是“访问限于此程序或派生自包含类的类型”。
- 私有（Private），通过在成员声明中包含 `private` 修饰符选择。`private` 的直观含义是“访问限于包含类型”。

根据成员声明发生的上下文，只允许某些类型的声明可访问性。此外，当成员声明不包含任何访问修饰符时，声明发生的上下文决定默认声明可访问性。

- 命名空间隐式具有 `public` 声明可访问性。命名空间声明上不允许使用访问修饰符。
- 在编译单元或命名空间中声明的类型可以具有 `public` 或 `internal` 声明可访问性，并默认为 `internal` 声明可访问性。
- 类成员可以具有五种声明可访问性中的任意一种，并默认为 `private` 声明可访问性。（注意，声明为类成员的类型可以具有五种声明可访问性中的任意一种，而声明为命名空间成员的类型只能具有 `public` 或 `internal` 声明可访问性。）
- 结构体成员可以具有 `public`、`internal` 或 `private` 声明可访问性，并默认为 `private` 声明可访问性，因为结构体是隐式密封的。在结构体中引入的（即不由该结构体继承的）结构体成员不能具有 `protected` 或 `protected internal` 声明可访问性。（注意，声明为结构体成员的类型可以具有 `public`、`internal` 或 `private` 声明可访问性，而声明为命名空间成员的类型只能具有 `public` 或 `internal` 声明可访问性。）
- 接口成员隐式具有 `public` 声明可访问性。接口成员声明上不允许使用访问修饰符。
- 枚举成员隐式具有 `public` 声明可访问性。枚举成员声明上不允许使用访问修饰符。

### 3.5.2 可访问性域

成员的*可访问性域*由允许访问该成员的（可能不相交的）程序文本部分构成。为了定义成员的可访问性域，如果成员未在某个类型中声明，则称该成员为*顶级*；如果成员在另一个类型中声明，则称该成员为*嵌套*。此外，程序的*程序文本*定义为该程序所有源文件中包含的全部程序文本，而某个类型的程序文本定义为该类型的*类型声明*中包含的全部程序文本（可能包括嵌套在该类型中的类型）。

预定义类型（如 `object`、`int` 或 `double`）的可访问性域不受限制。

在程序 `P` 中声明的顶级未绑定类型 `T`（§4.4.3）的可访问性域定义如下：

- 如果 `T` 的声明可访问性是 `public`，则 `T` 的可访问性域是 `P` 的程序文本以及任何引用 `P` 的程序的程序文本。
- 如果 `T` 的声明可访问性是 `internal`，则 `T` 的可访问性域是 `P` 的程序文本。

由这些定义可知，顶级未绑定类型的可访问性域始终至少是声明该类型的程序的程序文本。

构造类型 `T<A1, ..., AN>` 的可访问性域是未绑定泛型类型 `T` 的可访问性域与类型参数 `A1, ..., AN` 的可访问性域的交集。

在程序 `P` 中的类型 `T` 内声明的嵌套成员 `M` 的可访问性域定义如下（注意 `M` 本身可能是一个类型）：

- 如果 `M` 的声明可访问性是 `public`，则 `M` 的可访问性域是 `T` 的可访问性域。
- 如果 `M` 的声明可访问性是 `protected internal`，令 `D` 为 `P` 的程序文本与任何在 `P` 之外声明的、派生自 `T` 的类型的程序文本的并集。`M` 的可访问性域是 `T` 的可访问性域与 `D` 的交集。
- 如果 `M` 的声明可访问性是 `protected`，令 `D` 为 `T` 的程序文本与任何派生自 `T` 的类型的程序文本的并集。`M` 的可访问性域是 `T` 的可访问性域与 `D` 的交集。
- 如果 `M` 的声明可访问性是 `internal`，则 `M` 的可访问性域是 `T` 的可访问性域与 `P` 的程序文本的交集。
- 如果 `M` 的声明可访问性是 `private`，则 `M` 的可访问性域是 `T` 的程序文本。

由这些定义可知，嵌套成员的可访问性域始终至少是声明该成员的类型的程序文本。此外，还可得出，成员的可访问性域绝不会比声明该成员的类型的可访问性域更宽泛。



## C# 语言规范

直观地说，当访问类型或成员 M 时，会评估以下步骤以确保允许访问：

- 首先，如果 M 在类型内声明（而不是编译单元或命名空间），如果该类型不可访问，则会发生编译时错误。
- 然后，如果 M 是 public，则允许访问。
- 否则，如果 M 是 protected internal，则如果访问发生在 M 声明所在的程序内，或发生在从 M 声明所在的类派生的类内并且通过派生类类型进行访问（§3.5.3），则允许访问。
- 否则，如果 M 是 protected，则如果访问发生在 M 声明所在的类内，或发生在从 M 声明所在的类派生的类内并且通过派生类类型进行访问（§3.5.3），则允许访问。
- 否则，如果 M 是 internal，则如果访问发生在 M 声明所在的程序内，则允许访问。
- 否则，如果 M 是 private，则如果访问发生在 M 声明所在的类内，则允许访问。
- 否则，类型或成员不可访问，并且会发生编译时错误。

在示例中

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

类和成员具有以下可访问性域：

- A 和 A.X 的可访问性域是无限的。
- A.Y、B、B.X、B.Y、B.C、B.C.X 和 B.C.Y 的可访问性域是包含程序的程序文本。
- A.Z 的可访问性域是 A 的程序文本。
- B.Z 和 B.D 的可访问性域是 B 的程序文本，包括 B.C 和 B.D 的程序文本。

```csharp
static void F(A a, B b) {
    a.x = 1;    // Ok
    b.x = 1;    // Ok
}
```

```csharp
public class B: A
{
    static void F(A a, B b) {
        a.x = 1;    // Error, must access through instance of B
        b.x = 1;    // Ok
    }
}
```

在 A 内部，可以通过 A 和 B 的实例访问 x，因为在任何一种情况下，访问都是通过 A 的实例或从 A 派生的类进行的。然而，在 B 内部，不可能通过 A 的实例访问 x，因为 A 并未派生自 B。

在示例中

```csharp
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

对 x 的三次赋值都被允许，因为它们都通过从泛型类型构造的类类型的实例进行。

### 3.5.4 可访问性约束

C# 语言中的多个构造要求类型至少与成员或其他类型一样可访问。如果类型 T 的可访问性域是成员或类型 M 的可访问性域的超集，则称类型 T 至少与成员或类型 M 一样可访问。换句话说，如果 T 在 M 可访问的所有上下文中都可访问，则 T 至少与 M 一样可访问。

存在以下可访问性约束：

- 类类型的直接基类必须至少与类类型本身一样可访问。
- 接口类型的显式基接口必须至少与接口类型本身一样可访问。
- 委托类型的返回类型和参数类型必须至少与委托类型本身一样可访问。
- 常量的类型必须至少与常量本身一样可访问。
- 字段的类型必须至少与字段本身一样可访问。
- 方法的返回类型和参数类型必须至少与方法本身一样可访问。
- 属性的类型必须至少与属性本身一样可访问。
- 事件的类型必须至少与事件本身一样可访问。
- 索引器的类型和参数类型必须至少与索引器本身一样可访问。
- 运算符的返回类型和参数类型必须至少与运算符本身一样可访问。
- 实例构造函数的参数类型必须至少与实例构造函数本身一样可访问。

在示例中

```csharp
class A {...}
public class B: A {...}
```

B 类会导致编译时错误，因为 A 并非至少与 B 一样可访问。

同样，在示例中

```csharp
class A {...}
public class B
{
    A F() {...}
    internal A G() {...}
    public A H() {...}
}
```

B 中的 H 方法会导致编译时错误，因为返回类型 A 并非至少与方法一样可访问。

### 3.6 签名和重载

方法、实例构造函数、索引器和运算符由其签名表征：

- 方法的签名由方法名、类型参数的数量以及每个形式参数的类型和种类（值、引用或输出）组成，按从左到右的顺序考虑。为此目的，方法中出现在形式参数类型中的任何类型参数不是按其名称标识，而是按其在方法类型参数列表中的序数位置标识。方法的签名特别不包括返回类型、可能指定给最右参数的 params 修饰符，也不支持可选的类型参数约束。
- 实例构造函数的签名由每个形式参数的类型和种类（值、引用或输出）组成，按从左到右的顺序考虑。实例构造函数的签名特别不包括可能指定给最右参数的 params 修饰符。
- 索引器的签名由每个形式参数的类型组成，按从左到右的顺序考虑。索引器的签名特别不包括元素类型，也不包括可能指定给最右参数的 params 修饰符。
- 运算符的签名由运算符的名称和每个形式参数的类型组成，按从左到右的顺序考虑。运算符的签名特别不包括结果类型。

签名是类、结构和接口中成员重载的启用机制：

- 方法重载允许类、结构或接口声明多个同名方法，前提是其签名在该类、结构或接口内是唯一的。
- 实例构造函数重载允许类或结构声明多个实例构造函数，前提是其签名在该类或结构内是唯一的。
- 索引器重载允许类、结构或接口声明多个索引器，前提是其签名在该类、结构或接口内是唯一的。
- 运算符重载允许类或结构声明多个同名运算符，前提是其签名在该类或结构内是唯一的。

尽管 `out` 和 `ref` 参数修饰符被视为签名的一部分，但在单个类型中声明的成员不能仅因 `ref` 和 `out` 而在签名上有所不同。如果在同一类型中声明了两个成员，其签名在将两个方法中所有带有 `out` 修饰符的参数都更改为 `ref` 修饰符后相同，则会发生编译时错误。对于签名匹配的其他目的（例如隐藏或重写），`ref` 和 `out` 被视为签名的一部分且互不匹配。（此限制是为了允许 C# 程序易于翻译以在通用语言基础设施（CLI）上运行，后者不提供定义仅在 `ref` 和 `out` 上不同的方法的办法。）

就签名而言，类型 `object` 和 `dynamic` 被视为相同。因此，在单个类型中声明的成员不能仅因 `object` 和 `dynamic` 而在签名上有所不同。

以下示例显示了一组重载的方法声明及其签名。

```csharp
interface ITest
{
    void F();                  // F()
    void F(int x);             // F(int)
    void F(ref int x);         // F(ref int)
    void F(out int x);         // F(out int)     error
    void F(int x, int y);      // F(int, int)
    int F(string s);           // F(string)
    int F(int x);              // F(int)         error
    void F(string[] a);        // F(string[])
    void F(params string[] a); // F(string[])    error
}
```

请注意，任何 `ref` 和 `out` 参数修饰符（§10.6.1）都是签名的一部分。因此，`F(int)` 和 `F(ref int)` 是唯一的签名。然而，`F(ref int)` 和 `F(out int)` 不能在同一接口中声明，因为它们的签名仅因 `ref` 和 `out` 而不同。此外，请注意，返回类型和 `params` 修饰符不是签名的一部分，因此无法仅基于返回类型或 `params` 修饰符的包含或排除来进行重载。因此，上面标识的方法 `F(int)` 和 `F(params string[])` 的声明会导致编译时错误。

### 3.7 作用域

名称的 **作用域** 是程序文本中可以引用该名称声明的实体而无需限定该名称的区域。作用域可以 **嵌套**，并且内部作用域可能会重新声明外部作用域中名称的含义（但这并不会消除 §3.3 规定的限制，即在嵌套块内无法声明与封闭块中的局部变量同名的局部变量）。然后，外部作用域的名称在内部作用域覆盖的程序文本区域中被视为 **隐藏**，并且只能通过限定名称来访问外部名称。

- 由 *命名空间成员声明*（§9.5）声明且没有封闭 *命名空间声明* 的命名空间成员的作用域是整个程序文本。
- 由 *命名空间成员声明* 在 *命名空间声明* 内声明的命名空间成员的作用域，如果其完全限定名称为 `N`，则为每个完全限定名称为 `N` 或以 `N` 开后跟一个句点的 *命名空间声明* 的 *命名空间体*。



- 由外部别名指令定义的名字的作用域，涵盖其直接包含的编译单元或命名空间体中的 using 指令、全局特性和命名空间成员声明。外部别名指令不会向基础声明空间贡献任何新成员。换言之，外部别名指令不是传递性的，而只影响其所在的编译单元或命名空间体。
- 由 using 指令（§9.4）定义或导入的名字的作用域，涵盖该 using 指令所在的编译单元或命名空间体的命名空间成员声明。using 指令可以使零个或多个命名空间或类型名称在特定编译单元或命名空间体内可用，但不会向基础声明空间贡献任何新成员。换言之，using 指令不是传递性的，而只影响其所在的编译单元或命名空间体。
- 由类声明（§10.1）上的类型参数列表声明的类型参数的作用域，是该类声明的类基、类型参数约束子句和类体。
- 由结构体声明（§11.1）上的类型参数列表声明的类型参数的作用域，是该结构体声明的结构体接口、类型参数约束子句和结构体体。
- 由接口声明（§13.1）上的类型参数列表声明的类型参数的作用域，是该接口声明的接口基、类型参数约束子句和接口体。
- 由委托声明（§15.1）上的类型参数列表声明的类型参数的作用域，是该委托声明的返回类型、形参列表和类型参数约束子句。
- 由类成员声明（§10.1.6）声明的成员的作用域，是声明所在的类体。此外，类成员的作用域延伸到那些包含在该成员可访问域（§3.5.2）中的派生类的类体。
- 由结构体成员声明（§11.2）声明的成员的作用域，是声明所在的结构体体。
- 由枚举成员声明（§14.3）声明的成员的作用域，是声明所在的枚举体。
- 在方法声明（§10.6）中声明的参数的作用域，是该方法声明的方法体。
- 在索引器声明（§10.9）中声明的参数的作用域，是该索引器声明的访问器声明。
- 在运算符声明（§10.10）中声明的参数的作用域，是该运算符声明的块。
- 在构造函数声明（§10.11）中声明的参数的作用域，是该构造函数声明的构造函数初始化器和块。
- 在 lambda 表达式（§）中声明的参数的作用域，是该 lambda 表达式的 lambda 表达式体。
- 在匿名方法表达式（§）中声明的参数的作用域，是该匿名方法表达式的块。
- 在带标签语句（§8.4）中声明的标签的作用域，是声明所在的块。
- 在局部变量声明（§8.5.1）中声明的局部变量的作用域，是声明所在的块。
- 在 switch 语句（§8.7.2）的 switch 块中声明的局部变量的作用域，是 switch 块。
- 在 *for* 语句（§8.8.3）的 *for 初始化器* 中声明的局部变量，其作用域是该 *for 初始化器*、*for 条件*、*for 迭代器* 以及该 *for* 语句所包含的语句。
- 在 *局部常量声明*（§8.5.2）中声明的局部常量的作用域，是声明所在的块。在文本位置上引用位于其 *常量声明符* 之前的局部常量，属于编译时错误。
- 作为 *foreach 语句*、*using 语句*、*lock 语句* 或 *查询表达式* 的一部分声明的变量，其作用域由给定构造的展开决定。

在命名空间、类、结构体或枚举成员的作用域内，可以在成员声明之前的文本位置引用该成员。例如

```
class A
{
    void F() {
        i = 1;
    }

    int i = 0;
}
```

在这里，F 在 i 声明之前引用 i 是有效的。

在局部变量的作用域内，在文本位置上引用位于该局部变量的 *局部变量声明符* 之前的局部变量，属于编译时错误。例如

```
class A
{
    int i = 0;
    void F() {
        i = 1;             // Error, use precedes declaration
        int i;
        i = 2;
    }

    void G() {
        int j = (j = 1);   // Valid
    }

    void H() {
        int a = 1, b = ++a; // Valid
    }
}
```

在上面的 F 方法中，对 i 的第一次赋值明确不引用外层作用域中声明的字段。相反，它引用的是局部变量，并导致编译时错误，因为它在文本上位于该变量声明之前。在 G 方法中，在 j 声明的初始化器中引用 j 是有效的，因为该引用没有位于 *局部变量声明符* 之前。在 H 方法中，后续的 *局部变量声明符* 正确地引用同一 *局部变量声明* 中较早的 *局部变量声明符* 所声明的局部变量。

局部变量的作用域规则旨在保证：在表达式上下文中使用的名称，在一个块内的含义始终相同。如果局部变量的作用域仅从其声明处延伸到块的末尾，那么在上面的示例中，第一次赋值将赋给实例变量，第二次赋值将赋给局部变量；如果该块中的语句后来被重新排列，这可能会导致编译时错误。

块内名称的含义可能因使用该名称的上下文而异。在示例中

```csharp
using System;

class A {}
class Test
{
    static void Main() {
        string A = "hello, world";
        string s = A;                       // expression context
        Type t = typeof(A);                 // type context
        Console.WriteLine(s);               // writes "hello, world"
        Console.WriteLine(t);               // writes "A"
    }
}
```

名称 A 在表达式上下文中用于引用局部变量 A，在类型上下文中用于引用类 A。

## 3.7.1 名称隐藏

实体的作用域通常涵盖比该实体的声明空间更多的程序文本。特别地，实体的作用域可能包括引入包含同名实体的新声明空间的声明。此类声明会导致原始实体被隐藏。反之，当实体未被隐藏时，称该实体是可见的。

当作用域通过嵌套而重叠，以及当作用域通过继承而重叠时，就会发生名称隐藏。以下各节描述这两种隐藏类型的特征。

### 3.7.1.1 通过嵌套隐藏

通过嵌套发生的名称隐藏可能由以下原因产生：在命名空间中嵌套命名空间或类型，在类或结构体中嵌套类型，以及参数和局部变量声明。

在示例中

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

在 F 方法内，实例变量 i 被局部变量 i 隐藏，但在 G 方法内，i 仍引用实例变量。

当内层作用域中的名称隐藏外层作用域中的名称时，它会隐藏该名称的所有重载出现。

在示例中

```csharp
class Outer
{
    static void F(int i) {}
    static void F(string s) {}
    class Inner
    {
        void G() {
            F(1);          // Invokes Outer.Inner.F
            F("Hello");    // Error
        }
    }
}
```



```
      static void F(long l) {}
    }
```

调用 F(1) 会调用 Inner 中声明的 F，因为所有外部的 F 出现都被内部声明隐藏了。出于同样的原因，调用 F("Hello") 会导致编译时错误。

## 3.7.1.2 Hiding through inheritance

Name hiding through inheritance occurs when classes or structs redeclare names that were inherited from base classes. This type of name hiding takes one of the following forms:

通过继承隐藏名称发生在类或结构体重新声明从基类继承的名称时。这种名称隐藏有以下几种形式：

- A constant, field, property, event, or type introduced in a class or struct hides all base class members with the same name.
在类或结构体中引入的常量、字段、属性、事件或类型会隐藏所有同名基类成员。

- A method introduced in a class or struct hides all non-method base class members with the same name, and all base class methods with the same signature (method name and parameter count, modifiers, and types).
在类或结构体中引入的方法会隐藏所有同名非方法基类成员，以及所有具有相同签名（方法名和参数个数、修饰符和类型）的基类方法。

- An indexer introduced in a class or struct hides all base class indexers with the same signature (parameter count and types).
在类或结构体中引入的索引器会隐藏所有具有相同签名（参数个数和类型）的基类索引器。

The rules governing operator declarations (§10.10) make it impossible for a derived class to declare an operator with the same signature as an operator in a base class. Thus, operators never hide one another.
运算符声明的规则（§10.10）使得派生类无法声明与基类运算符具有相同签名的运算符。因此，运算符永远不会相互隐藏。

Contrary to hiding a name from an outer scope, hiding an accessible name from an inherited scope causes a warning to be reported. In the example

与从外部作用域隐藏名称相反，从继承作用域隐藏可访问名称会导致发出警告。在示例中

```csharp
class Base
{
    public void F() {}
}
class Derived: Base
{
    public void F() {}      // warning, hiding an inherited name
}
```

the declaration of F in Derived causes a warning to be reported. Hiding an inherited name is specifically not an error, since that would preclude separate evolution of base classes. For example, the above situation might have come about because a later version of Base introduced an F method that wasn't present in an earlier version of the class. Had the above situation been an error, then any change made to a base class in a separately versioned class library could potentially cause derived classes to become invalid.
在 Derived 中声明 F 会导致发出警告。隐藏继承的名称特意不是错误，因为那样会阻止基类的独立演进。例如，上述情况可能是因为 Base 的较新版本引入了 F 方法，而该方法在类的早期版本中不存在。如果上述情况是错误，那么在单独版本化的类库中对基类所做的任何更改都可能导致派生类变得无效。

The warning caused by hiding an inherited name can be eliminated through use of the new modifier:

通过使用 new 修饰符可以消除隐藏继承名称引起的警告：

```csharp
class Base
{
    public void F() {}
}
class Derived: Base
{
    new public void F() {}
}
```

The new modifier indicates that the F in Derived is “new”, and that it is indeed intended to hide the inherited member.
new 修饰符表示 Derived 中的 F 是“新的”，并且确实 intended to hide the inherited member。

A declaration of a new member hides an inherited member only within the scope of the new member.

新成员的声明仅在其自身作用域内隐藏继承的成员。

```csharp
class Base
{
    public static void F() {}
}
class Derived: Base
{
    new private static void F() {}    // Hides Base.F in Derived only
}
class MoreDerived: Derived
{
    static void G() { F(); }          // Invokes Base.F
}
```

In the example above, the declaration of F in Derived hides the F that was inherited from Base, but since the new F in Derived has private access, its scope does not extend to MoreDerived. Thus, the call F() in MoreDerived.G is valid and will invoke Base.F.
在上面的示例中，Derived 中 F 的声明隐藏了从 Base 继承的 F，但由于 Derived 中的新 F 具有私有访问权限，其作用域不会扩展到 MoreDerived。因此，MoreDerived.G 中对 F() 的调用是有效的，并且会调用 Base.F。

## 3.8 Namespace and type names

Several contexts in a C# program require a namespace-name or a type-name to be specified.

C# 程序中的多个上下文要求指定 namespace-name 或 type-name。

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

A namespace-name is a namespace-or-type-name that refers to a namespace. Following resolution as described below, the namespace-or-type-name of a namespace-name must refer to a namespace, or otherwise a compile-time error occurs. No type arguments (§4.4.1) can be present in a namespace-name (only types can have type arguments).
namespace-name 是一个引用命名空间的 namespace-or-type-name。按照下面描述的解析，namespace-name 的 namespace-or-type-name 必须引用一个命名空间，否则会发生编译时错误。namespace-name 中不能存在类型参数（§4.4.1）（只有类型可以具有类型参数）。

A type-name is a namespace-or-type-name that refers to a type. Following resolution as described below, the namespace-or-type-name of a type-name must refer to a type, or otherwise a compile-time error occurs.
type-name 是一个引用类型的 namespace-or-type-name。按照下面描述的解析，type-name 的 namespace-or-type-name 必须引用一个类型，否则会发生编译时错误。

If the namespace-or-type-name is a qualified-alias-member, its meaning is as described in §9.7. Otherwise, a namespace-or-type-name has one of four forms:
如果 namespace-or-type-name 是 qualified-alias-member，则其含义如 §9.7 中所述。否则，namespace-or-type-name 有以下四种形式之一：

- I
- I<A₁, ..., Aₙ>
- N.I
- N.I<A₁, ..., Aₙ>

where I is a single identifier, N is a namespace-or-type-name and <A₁, ..., Aₙ> is an optional type-argument-list. When no type-argument-list is specified, consider K to be zero.
其中 I 是一个标识符，N 是一个 namespace-or-type-name，而 <A₁, ..., Aₙ> 是一个可选的类型参数列表。当未指定类型参数列表时，将 K 视为零。

The meaning of a namespace-or-type-name is determined as follows:
namespace-or-type-name 的含义确定如下：

- If the namespace-or-type-name is of the form I or of the form I<A₁, ..., Aₙ>:
如果 namespace-or-type-name 的形式为 I 或 I<A₁, ..., Aₙ>：

  - If K is zero and the namespace-or-type-name appears within a generic method declaration (§10.6) and if that declaration includes a type parameter (§10.1.3) with name I, then the namespace-or-type-name refers to that type parameter.
  如果 K 为零且 namespace-or-type-name 出现在泛型方法声明（§10.6）中，并且该声明包含名称为 I 的类型参数（§10.1.3），则 namespace-or-type-name 引用该类型参数。

  - Otherwise, if the namespace-or-type-name appears within a type declaration, then for each instance type T (§10.3.1), starting with the instance type of that type declaration and continuing with the instance type of each enclosing class or struct declaration (if any):
  否则，如果 namespace-or-type-name 出现在类型声明中，则对于每个实例类型 T（§10.3.1），从该类型声明的实例类型开始，继续到每个封闭的类或结构体声明（如果有）的实例类型：

    - If K is zero and the declaration of T includes a type parameter with name I, then the *namespace-or-type-name* refers to that type parameter.
    如果 K 为零且 T 的声明包含名称为 I 的类型参数，则 *命名空间或类型名* 引用该类型参数。

    - Otherwise, if the *namespace-or-type-name* appears within the body of the type declaration, and T or any of its base types contain a nested accessible type having name I and K type parameters, then the *namespace-or-type-name* refers to that type constructed with the given type arguments. If there is more than one such type, the type declared within the more derived type is selected. Note that non-type members (constants, fields, methods, properties, indexers, operators, instance constructors, destructors, and static constructors) and type members with a different number of type parameters are ignored when determining the meaning of the *namespace-or-type-name*.
    否则，如果 *命名空间或类型名* 出现在类型声明的主体中，并且 T 或其任何基类型包含名称为 I 且具有 K 个类型参数的嵌套可访问类型，则 *命名空间或类型名* 引用使用给定类型参数构造的该类型。如果存在多个此类类型，则选择在更派生的类型中声明的类型。请注意，非类型成员（常量、字段、方法、属性、索引器、运算符、实例构造函数、析构函数和静态构造函数）以及类型参数数量不同的类型成员在确定 *命名空间或类型名* 的含义时会被忽略。

    - If the previous steps were unsuccessful then, for each namespace N, starting with the namespace in which the *namespace-or-type-name* occurs, continuing with each enclosing namespace (if any), and ending with the global namespace, the following steps are evaluated until an entity is located:
    如果前面的步骤不成功，则对于每个命名空间 N，从 *命名空间或类型名* 出现的命名空间开始，继续到每个封闭的命名空间（如果有），并以全局命名空间结束，以下步骤将被评估直到找到一个实体：

      - If K is zero and I is the name of a namespace in N, then:
      如果 K 为零且 I 是 N 中的命名空间的名称，则：

        - If the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with a namespace or type, then the *namespace-or-type-name* is ambiguous and a compile-time error occurs.
        如果 *命名空间或类型名* 出现的位置被 N 的命名空间声明所包含，并且命名空间声明包含一个将名称 I 与命名空间或类型关联的 *extern 别名指令* 或 *using 别名指令*，则 *命名空间或类型名* 是模棱两可的，并且会发生编译时错误。

        - Otherwise, the *namespace-or-type-name* refers to the namespace named I in N.
        否则，*命名空间或类型名* 引用 N 中名为 I 的命名空间。

      - Otherwise, if N contains an accessible type having name I and K type parameters, then:
      否则，如果 N 包含名称为 I 且具有 K 个类型参数的可访问类型，则：

        - If K is zero and the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with a namespace or type, then the *namespace-or-type-name* is ambiguous and a compile-time error occurs.
        如果 K 为零且 *命名空间或类型名* 出现的位置被 N 的命名空间声明所包含，并且命名空间声明包含一个将名称 I 与命名空间或类型关联的 *extern 别名指令* 或 *using 别名指令*，则 *命名空间或类型名* 是模棱两可的，并且会发生编译时错误。

        - Otherwise, the *namespace-or-type-name* refers to the type constructed with the given type arguments.
        否则，*命名空间或类型名* 引用使用给定类型参数构造的类型。

      - Otherwise, if the location where the *namespace-or-type-name* occurs is enclosed by a namespace declaration for N:
      否则，如果 *命名空间或类型名* 出现的位置被 N 的命名空间声明所包含：

        - If K is zero and the namespace declaration contains an *extern-alias-directive* or *using-alias-directive* that associates the name I with an imported namespace or type, then the *namespace-or-type-name* refers to that namespace or type.
        如果 K 为零且命名空间声明包含一个将名称 I 与导入的命名空间或类型关联的 *extern 别名指令* 或 *using 别名指令*，则 *命名空间或类型名* 引用该命名空间或类型。

        - Otherwise, if the namespaces imported by the *using-namespace-directives* of the namespace declaration contain exactly one type having name I and K type parameters, then the *namespace-or-type-name* refers to that type constructed with the given type arguments.
        否则，如果命名空间声明的 *using 命名空间指令* 导入的命名空间恰好包含一个名称为 I 且具有 K 个类型参数的类型，则 *命名空间或类型名* 引用使用给定类型参数构造的该类型。

        - Otherwise, if the namespaces imported by the *using-namespace-directives* of the namespace declaration contain more than one type having name I and K type parameters, then the *namespace-or-type-name* is ambiguous and an error occurs.
        否则，如果命名空间声明的 *using 命名空间指令* 导入的命名空间包含多个名称为 I 且具有 K 个类型参数的类型，则 *命名空间或类型名* 是模棱两可的，并且会发生错误。

        - Otherwise, the *namespace-or-type-name* is undefined and a compile-time error occurs.
        否则，*命名空间或类型名* 未定义，并且会发生编译时错误。

      - Otherwise, the *namespace-or-type-name* is of the form N.I or of the form N.I<A₁, ..., Aₖ>. N is first resolved as a *namespace-or-type-name*. If the resolution of N is not successful, a compile-time error occurs. Otherwise, N.I or N.I<A₁, ..., Aₖ> is resolved as follows:
      否则，*命名空间或类型名* 的形式为 N.I 或 N.I<A₁, ..., Aₖ>。首先将 N 解析为 *命名空间或类型名*。如果 N 的解析不成功，则会发生编译时错误。否则，按如下方式解析 N.I 或 N.I<A₁, ..., Aₖ>：

        - If K is zero and N refers to a namespace and N contains a nested namespace with name I, then the *namespace-or-type-name* refers to that nested namespace.
        如果 K 为零且 N 引用一个命名空间并且 N 包含名称为 I 的嵌套命名空间，则 *命名空间或类型名* 引用该嵌套命名空间。



-   否则，如果 N 指代一个命名空间，并且 N 包含一个具有名称 I 和 K 个类型参数的可访问类型，则该命名空间或类型名指代使用给定类型实参构造的那个类型。
-   否则，如果 N 指代一个（可能已构造的）类或结构类型，并且 N 或其任何基类包含一个具有名称 I 和 K 个类型参数的嵌套可访问类型，则该命名空间或类型名指代使用给定类型实参构造的那个类型。如果有多个这样的类型，则选择在更派生类型中声明的类型。注意，如果 N.I 的含义是在解析 N 的基类规范的过程中确定的，则 N 的直接基类被视为 object（§10.1.4.1）。
-   否则，N.I 是无效的命名空间或类型名，并发生编译时错误。

仅当满足以下条件之一时，才允许命名空间或类型名引用静态类（§10.1.1.3）：
-   该命名空间或类型名是形如 T.I 的命名空间或类型名中的 T，或者
-   该命名空间或类型名是形如 typeof(T) 的 typeof 表达式（§7.5.11）中的 T。

## 3.8.1 完全限定名

每个命名空间和类型都有一个完全限定名，它在所有其他命名空间和类型中唯一标识该命名空间或类型。命名空间或类型 N 的完全限定名按如下方式确定：
-   如果 N 是全局命名空间的成员，则其完全限定名为 N。
-   否则，其完全限定名为 S.N，其中 S 是声明 N 的命名空间或类型的完全限定名。

换言之，N 的完全限定名是从全局命名空间开始、通向 N 的完整标识符分层路径。由于命名空间或类型的每个成员都必须具有唯一名称，因此命名空间或类型的完全限定名始终唯一。

下面的示例展示了若干命名空间和类型声明及其关联的完全限定名。

```
class A {}          // A
namespace X         // X
{
    class B         // X.B
    {
        class C {}  // X.B.C
    }
    namespace Y     // X.Y
    {
        class D {}  // X.Y.D
    }
}
namespace X.Y       // X.Y
{
    class E {}      // X.Y.E
}
```

## 3.9 自动内存管理

C# 采用自动内存管理，使开发者无需手动分配和释放对象占用的内存。自动内存管理策略由垃圾回收器实现。对象的内存管理生命周期如下：
1.  创建对象时，为其分配内存，运行构造函数，并且该对象被视为存活。
2.  如果对象或其任何部分不能被执行的任何可能后续（除运行析构函数之外）访问，则该对象被视为不再使用，并变为可被销毁。C# 编译器和垃圾回收器可以选择分析代码，以确定将来可能使用对对象的哪些引用。例如，如果作用域中的局部变量是对象的唯一现有引用，但在从过程中当前执行点开始的任何可能后续执行中都不会引用该局部变量，则垃圾回收器可以（但不要求）将该对象视为不再使用。
3.  一旦对象可被销毁，在某个未指定的稍后时间，将运行该对象的析构函数（§10.13）（如果有）。除非被显式调用覆盖，否则该对象的析构函数仅运行一次。
4.  一旦对象的析构函数运行完毕，如果该对象或其任何部分不能被执行的任何可能后续（包括运行析构函数）访问，则该对象被视为不可访问，并变为可被回收。
5.  最后，在对象变为可被回收之后的某个时间，垃圾回收器释放与该对象关联的内存。

垃圾回收器维护有关对象使用情况的信息，并使用此信息做出内存管理决策，例如在内存中的何处放置新创建的对象、何时重定位对象，以及对象何时不再使用或不可访问。

与其他假定存在垃圾回收器的语言一样，C# 的设计使垃圾回收器可以实现广泛的内存管理策略。例如，C# 不要求对象一可被销毁就运行析构函数或一可被回收就回收对象，也不要求按任何特定顺序或在任何特定线程上运行析构函数。

垃圾回收器的行为可以在一定程度上通过类 System.GC 上的静态方法进行控制。此类可用于请求执行回收、运行（或不运行）析构函数等。

由于允许垃圾回收器在决定何时回收对象和运行析构函数方面具有很大自由度，符合规范的实现可能产生与以下代码所示不同的输出。程序

```
using System;
class A
{
    ~A() {
        Console.WriteLine("Destruct instance of A");
    }
}
class B
{
    object Ref;
    public B(object o) {
        Ref = o;
    }
    ~B() {
        Console.WriteLine("Destruct instance of B");
    }
}
```

```csharp
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

创建类 A 的实例和类 B 的实例。当变量 b 被赋值为 null 时，这些对象变为可被垃圾回收，因为在此之后，任何用户编写的代码都不可能访问它们。输出可能是

```
Destruct instance of A
Destruct instance of B
```

或

```
Destruct instance of B
Destruct instance of A
```

因为该语言对对象被垃圾回收的顺序不施加任何约束。

在微妙的情况下，“可被销毁”和“可被回收”之间的区别可能很重要。例如，

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

在上述程序中，如果垃圾回收器选择在 B 的析构函数之前运行 A 的析构函数，则此程序的输出可能是：

```
Destruct instance of A
Destruct instance of B
A.F
RefA is not null
```

注意，尽管 A 的实例未被使用且 A 的析构函数已运行，但仍可能从另一个析构函数调用 A 的方法（在此例中为 F）。另外，请注意，运行析构函数可能导致对象再次可从主程序使用。在此例中，运行 B 的析构函数导致先前未使用的 A 的实例可从活动引用 Test.RefA 访问。在调用 waitForPendingFinalizers 之后，B 的实例可被回收，但 A 的实例不可被回收，因为有引用 Test.RefA。

为避免混淆和意外行为，通常好的做法是让析构函数仅对存储在其对象自身字段中的数据执行清理，而不要对引用的对象或静态字段执行任何操作。

使用析构函数的另一种替代方法是让类实现 System.IDisposable 接口。这允许对象的客户端决定何时释放对象的资源，通常通过在 using 语句（§8.13）中将该对象作为资源访问来实现。

## 3.10 执行顺序

C# 程序的执行方式使得每个执行线程的副作用在关键执行点得以保留。副作用定义为对易失字段的读取或写入、对非易失变量的写入、对外部资源的写入以及异常的引发。必须保留这些副作用顺序的关键执行点包括：对易失字段的引用（§10.5.3）、lock 语句（§8.12）以及线程的创建和终止。执行环境可以自由更改 C# 程序的执行顺序，但须遵守以下约束：
-   数据依赖在一个执行线程内得以保留。也就是说，每个变量的值按如下方式计算：如同线程中的所有语句都按原始程序顺序执行。
-   初始化顺序规则得以保留（§10.5.4 和 §10.5.5）。
-   相对于易失读取和写入（§10.5.3），副作用的顺序得以保留。此外，如果执行环境能够推断出表达式的值未被使用且未产生任何所需副作用（包括由调用方法或访问易失字段引起的任何副作用），则无需计算表达式的某一部分。当程序执行被异步事件（例如另一个线程引发的异常）中断时，不保证可观察的副作用按原始程序顺序可见。




## 4. 类型

C# 语言的类型分为两个主要类别：*值类型* 和 *引用类型*。值类型和引用类型都可能是 *泛型类型*，它们接受一个或多个 *类型参数*。类型参数可以指定值类型和引用类型。

- 类型:
  - 值类型
  - 引用类型
  - 类型参数

第三类类型，指针，仅在不安全代码中可用。将在 §18.2 中进一步讨论。

值类型与引用类型的区别在于，值类型变量直接包含其数据，而引用类型变量存储对其数据的 *引用*，后者称为 *对象*。对于引用类型，两个变量可能引用同一个对象，因此对一个变量的操作可能会影响另一个变量所引用的对象。对于值类型，每个变量都有自己数据的副本，不可能通过对一个变量的操作影响另一个变量。

C# 的类型系统是统一的，使得 *任何类型的值都可以被视为对象*。C# 中的每个类型直接或间接派生自 *object* 类类型，而 *object* 是所有类型的最终基类。引用类型的值只需将值视为 *object* 类型即可被视为对象。值类型的值则通过执行装箱和拆箱操作（§4.3）被视为对象。

### 4.1 值类型

值类型要么是结构体类型，要么是枚举类型。C# 提供了一组预定义的结构体类型，称为 *简单类型*。简单类型通过保留字来标识。

- 值类型:
  - 结构体类型
  - 枚举类型

- 结构体类型:
  - 类型名
  - 简单类型
  - 可空类型

- 简单类型:
  - 数值类型
  - bool

- 数值类型:
  - 整数类型
  - 浮点类型
  - decimal

```
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

与引用类型变量不同，值类型变量只有在值类型为可空类型时才能包含 null 值。对于每个不可空值类型，都存在一个对应的可空值类型，表示相同的取值集合加上 null 值。

向值类型变量赋值会创建所赋值的副本。这与向引用类型变量赋值不同，后者复制引用但不复制引用所标识的对象。

#### 4.1.1 System.ValueType 类型

所有值类型都隐式继承自类 System.ValueType，而后者又继承自类 object。任何类型都不能派生自值类型，因此值类型是隐式密封的（§10.1.1.2）。

请注意，System.ValueType 本身并不是值类型。相反，它是一个类类型，所有值类型都自动从它派生。

#### 4.1.2 默认构造函数

所有值类型都隐式声明一个名为默认构造函数的公共无参数实例构造函数。默认构造函数返回一个零初始化的实例，被称为该值类型的默认值：

- 对于所有简单类型，默认值是由全零位模式产生的值：
  - 对于 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 和 `ulong`，默认值是 0。
  - 对于 `char`，默认值是 '\x0000'。
  - 对于 `float`，默认值是 0.0f。
  - 对于 `double`，默认值是 0.0d。
  - 对于 `decimal`，默认值是 0.0m。
  - 对于 `bool`，默认值是 false。
- 对于枚举类型 E，默认值是 0，转换为类型 E。
- 对于 *结构体类型*，默认值是通过将所有值类型字段设置为其默认值以及所有引用类型字段设置为 `null` 而产生的值。
- 对于 *可空类型*，默认值是一个 `HasValue` 属性为 false 且 `Value` 属性未定义 的实例。默认值也称为可空类型的 *null 值*。

与任何其他实例构造函数一样，值类型的默认构造函数使用 `new` 运算符调用。出于效率原因，此要求并不意味着实现实际生成构造函数调用。下面示例中，变量 `i` 和 `j` 都被初始化为零。

```
class A
{
    void F() {
        int i = 0;
        int j = new int();
    }
}
```

由于每个值类型都隐式具有公共无参数实例构造函数，因此结构体类型不能包含无参数构造函数的显式声明。然而，结构体类型允许声明带参数的实例构造函数（§11.3.8）。

#### 4.1.3 结构体类型

结构体类型是一种值类型，可以声明常量、字段、方法、属性、索引器、运算符、实例构造函数、静态构造函数和嵌套类型。结构体类型的声明在 §11.1 中描述。

#### 4.1.4 简单类型

C# 提供了一组预定义的结构体类型，称为 *简单类型*。简单类型通过保留字标识，但这些保留字只是 System 命名空间中预定义结构体类型的别名，如下表所述。

| 保留字 | 别名类型 |
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

由于简单类型别名一个结构体类型，每个简单类型都有成员。例如，`int` 具有在 `System.Int32` 中声明的成员以及从 `System.Object` 继承的成员，并且以下语句是允许的：

```
int i = int.MaxValue;    // System.Int32.MaxValue constant
string s = i.ToString();    // System.Int32.ToString() instance method
string t = 123.ToString();    // System.Int32.ToString() instance method
```

简单类型与其它结构体类型不同之处在于它们允许某些额外操作：

- 大多数简单类型允许通过编写文字来创建值（§2.4.4）。例如，123 是类型 `int` 的文字，'a' 是类型 `char` 的文字。C# 对结构体类型一般不提供文字，非默认值通常总是通过这些结构体类型的实例构造函数创建。
- 当表达式的操作数都是简单类型常量时，编译器可以对表达式进行编译时求值。这种表达式称为 *常量表达式*（§7.19）。涉及其它结构体类型定义的运算符的表达式不被视为常量表达式。
- 通过 `const` 声明可以声明简单类型的常量（§10.4）。不能有其它结构体类型的常量，但 `static readonly` 字段提供了类似的效果。
- 涉及简单类型的转换可以参与由其它结构体类型定义的转换运算符的求值，但用户定义的转换运算符永远不能参与另一个用户定义运算符的求值（§6.4.3）。

#### 4.1.5 整数类型

C# 支持九种整数类型：`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong` 和 `char`。整数类型具有以下大小和取值范围：

- `sbyte` 类型表示有符号 8 位整数，取值范围在 −128 到 127 之间。
- `byte` 类型表示无符号 8 位整数，取值范围在 0 到 255 之间。
- `short` 类型表示有符号 16 位整数，取值范围在 −32768 到 32767 之间。
- `ushort` 类型表示无符号 16 位整数，取值范围在 0 到 65535 之间。
- `int` 类型表示有符号 32 位整数，取值范围在 −2147483648 到 2147483647 之间。
- `uint` 类型表示无符号 32 位整数，取值范围在 0 到 4294967295 之间。
- `long` 类型表示有符号 64 位整数，取值范围在 −9223372036854775808 到 9223372036854775807 之间。
- `ulong` 类型表示无符号 64 位整数，取值范围在 0 到 18446744073709551615 之间。
- `char` 类型表示无符号 16 位整数，取值范围在 0 到 65535 之间。`char` 类型的可能取值集合对应于 Unicode 字符集。虽然 `char` 与 `ushort` 具有相同的表示，但并非对一种类型允许的所有操作都对另一种类型允许。

整数类型的 unary 和 binary 运算符始终以有符号 32 位精度、无符号 32 位精度、有符号 64 位精度或无符号 64 位精度操作：

- 对于 unary `+` 和 `-` 运算符，操作数被转换为类型 T，其中 T 是 `int`、`uint`、`long` 和 `ulong` 中第一个能够完全表示操作数所有可能值的类型。然后使用类型 T 的精度执行操作，结果的类型为 T。
- 对于 unary `-` 运算符，操作数被转换为类型 T，其中 T 是 `int` 和 `long` 中第一个能够完全表示操作数所有可能值的类型。然后使用类型 T 的精度执行操作，结果的类型为 T。unary `-` 运算符不能应用于类型为 `ulong` 的操作数。
- 对于 binary `+`、`-`、`*`、 `/`、`%`、`&`、`^`、`|`、`==`、`!=`、`>`、`<`、`>=` 和 `<=` 运算符，操作数被转换为类型 T，其中 T 是 `int`、`uint`、`long` 和 `ulong` 中第一个能够完全表示两者所有可能值的类型

操作数。随后使用类型 T 的精度执行运算，结果类型为 T（关系运算符则为 bool）。对于二元运算符，不允许一个操作数为 long 类型而另一个为 ulong 类型。

- 对于二元 << 和 >> 运算符，左操作数转换为类型 T，其中 T 是 int、uint、long 和 ulong 中第一个能够完全表示该操作数所有可能值的类型。随后使用类型 T 的精度执行运算，结果类型为 T。

char 类型归类为整型，但它在两个方面与其他整型不同：

- 不存在从其他类型到 char 类型的隐式转换。特别地，尽管 sbyte、byte 和 ushort 类型的值范围完全可以用 char 类型表示，也不存在从 sbyte、byte 或 ushort 到 char 的隐式转换。
- char 类型的常量必须写成字符字面量，或写成与到 char 类型的强制转换组合的整数字面量。例如，(char)10 与 '\x000A' 相同。

checked 和 unchecked 运算符与语句用于控制整型算术运算和转换的溢出检查（§7.6.12）。在 checked 上下文中，溢出会产生编译时错误，或导致引发 System.OverflowException。在 unchecked 上下文中，溢出被忽略，任何不适合目标类型的高位都会被丢弃。

## 4.1.6 浮点类型

C# 支持两种浮点类型：float 和 double。float 和 double 类型分别使用 32 位单精度和 64 位双精度 IEEE 754 格式表示，它们提供以下值集合：

- 正零和负零。在大多数情况下，正零和负零的行为与简单值零完全相同，但某些运算会区分二者（§7.8.2）。
- 正无穷大和负无穷大。无穷大由诸如非零数除以零之类的运算产生。例如，1.0 / 0.0 产生正无穷大，而 −1.0 / 0.0 产生负无穷大。
- 非数字值，通常缩写为 NaN。NaN 由无效的浮点运算产生，例如零除以零。
- 形式为 s × m × 2^e 的有限非零值集合，其中 s 为 1 或 −1，m 和 e 由具体浮点类型决定：对于 float，0 < m < 2^24 且 −149 ≤ e ≤ 104；对于 double，0 < m < 2^53 且 −1075 ≤ e ≤ 970。非规范化浮点数被视为有效的非零值。

float 类型可以表示大约从 1.5 × 10^−45 到 3.4 × 10^38 的值，精度为 7 位数字。

double 类型可以表示大约从 5.0 × 10^−324 到 1.7 × 10^308 的值，精度为 15-16 位数字。

如果二元运算符的一个操作数为浮点类型，则另一个操作数必须为整型或浮点类型，并且按如下方式对该运算求值：

- 如果其中一个操作数为整型，则将该操作数转换为另一个操作数的浮点类型。
- 然后，如果任一操作数为 double 类型，则将另一个操作数转换为 double，运算至少使用 double 的范围和精度执行，结果类型为 double（关系运算符则为 bool）。
- 否则，运算至少使用 float 的范围和精度执行，结果类型为 float（关系运算符则为 bool）。

浮点运算符（包括赋值运算符）从不产生异常。相反，在异常情形下，浮点运算会产生零、无穷大或 NaN，如下所述：

- 如果浮点运算的结果对于目标格式而言太小，则运算结果变为正零或负零。
- 如果浮点运算的结果对于目标格式而言太大，则运算结果变为正无穷大或负无穷大。
- 如果浮点运算无效，则运算结果变为 NaN。
- 如果浮点运算的一个或两个操作数为 NaN，则运算结果变为 NaN。

浮点运算的执行精度可能高于该运算的结果类型。例如，某些硬件架构支持范围与精度均高于 double 类型的“扩展”或“long double”浮点类型，并隐式使用这种更高精度的类型执行所有浮点运算。只有付出过高的性能代价，才能让此类硬件架构以较低精度执行浮点运算；与其要求实现同时牺牲性能和精度，C# 允许所有浮点运算使用更高精度的类型。除了提供更精确的结果外，这很少产生任何可测量的影响。然而，在 x * y / z 形式的表达式中，乘法产生的结果超出 double 范围，但随后的除法又将临时结果带回 double 范围；此时表达式以更高范围格式求值这一事实，可能导致产生有限结果而不是无穷大。

## 4.1.7 decimal 类型

decimal 类型是一种 128 位数据类型，适用于财务和货币计算。decimal 类型可以表示从 1.0 × 10⁻²⁸ 到大约 7.9 × 10²⁸ 的值，具有 28-29 位有效数字。

decimal 类型的有限值集合的形式为 (−1)ˢ × c × 10ᵉ，其中符号 s 为 0 或 1，系数 c 满足 0 ≤ c < 2²⁶，小数位数 e 满足 0 ≤ e ≤ 28。decimal 类型不支持带符号零、无穷大或 NaN。decimal 表示为一个按十的幂缩放的 96 位整数。对于绝对值小于 1.0m 的 decimal，其值精确到第 28 位小数，但不会更精确。对于绝对值大于或等于 1.0m 的 decimal，其值精确到 28 或 29 位数字。与 float 和 double 数据类型不同，像 0.1 这样的十进制小数可以在 decimal 表示中精确表示。在 float 和 double 表示中，此类数字通常是无限小数，使这些表示更容易产生舍入误差。

如果二元运算符的一个操作数为 decimal 类型，则另一个操作数必须为整型或 decimal 类型。如果存在整型操作数，则在执行运算前将其转换为 decimal。

对 decimal 类型的值执行运算的结果，相当于先计算精确结果（保留为每个运算符定义的小数位数），然后进行舍入以适应表示形式所得到的结果。结果舍入到最接近的可表示值；当结果与两个可表示值距离相等时，舍入到最低有效数字位为偶数的值（这称为“银行家舍入法”）。零结果的符号始终为 0，小数位数始终为 0。

如果 decimal 算术运算产生的值的绝对值小于或等于 5 × 10⁻²⁹，则运算结果变为零。如果 decimal 算术运算产生的结果对于 decimal 格式而言太大，则引发 System.OverflowException。

decimal 类型比浮点类型精度更高，但范围更小。因此，从浮点类型到 decimal 的转换可能产生溢出异常，而从 decimal 到浮点类型的转换可能导致精度损失。由于这些原因，浮点类型与 decimal 之间不存在隐式转换；如果没有显式强制转换，就不可能在同一个表达式中混用浮点操作数和 decimal 操作数。



### 4.1.8 bool 类型

bool 类型表示布尔逻辑量。bool 类型的可能值为 true 和 false。

bool 与其他类型之间不存在标准转换。特别地，bool 类型与整型截然不同且相互独立，bool 值不能代替整型值使用，反之亦然。

在 C 和 C++ 语言中，零整型或浮点值、或空指针可以转换为布尔值 false，非零整型或浮点值、或非空指针可以转换为布尔值 true。在 C# 中，此类转换通过将整型或浮点值与零进行显式比较，或将对象引用与 null 进行显式比较来完成。

### 4.1.9 枚举类型

枚举类型是一种包含命名常量的独特类型。每个枚举类型都有一个基础类型，该类型必须是 byte、sbyte、short、ushort、int、uint、long 或 ulong。枚举类型的值集与基础类型的值集相同。枚举类型的值不限于命名常量的值。枚举类型通过枚举声明（§14.1）定义。

### 4.1.10 可空类型

可空类型可以表示其基础类型的所有值，外加一个额外的 null 值。可空类型写作 T?，其中 T 是基础类型。此语法是 System.Nullable<T> 的简写形式，两种形式可以互换使用。

相反，非可空值类型是除 System.Nullable<T> 及其简写 T?（对于任意 T）之外的任何值类型，再加上被约束为非可空值类型的任何类型参数（即带有 struct 约束的任何类型参数）。System.Nullable<T> 类型为 T 指定值类型约束（§10.1.5），这意味着可空类型的基础类型可以是任何非可空值类型。可空类型的基础类型不能是可空类型或引用类型。例如，int?? 和 string? 是无效类型。

可空类型 T? 的实例有两个公共只读属性：

- 一个 bool 类型的 HasValue 属性
- 一个 T 类型的 Value 属性

HasValue 为 true 的实例称为非空实例。非空实例包含一个已知值，Value 返回该值。

HasValue 为 false 的实例称为 null 实例。null 实例具有未定义的值。尝试读取 null 实例的 Value 会导致抛出 System.InvalidOperationException。访问可空类型的 Value 属性的过程称为解包（unwrapping）。

除了默认构造函数外，每个可空类型 T? 都有一个公共构造函数，该构造函数接受一个 T 类型的参数。给定一个 T 类型的值 x，形式如下的构造函数调用

```
new T?(x)
```

创建 T? 的一个非空实例，其 Value 属性为 x。为给定值创建可空类型的非空实例的过程称为包装（wrapping）。存在从 null 字面量到 T?（§6.1.5）以及从 T 到 T?（§6.1.4）的隐式转换。

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
    non-array-type  rank-specifiers

non-array-type:
    type

rank-specifiers:
    rank-specifier
    rank-specifiers  rank-specifier

rank-specifier:
    [  dim-separators_opt  ]

dim-separators:
    ,
    dim-separators  ,

delegate-type:
    type-name
```

引用类型值是对该类型实例的引用，后者称为对象。特殊值 null 与所有引用类型兼容，表示不存在实例。

### 4.2.1 类类型

类类型定义一种数据结构，其中包含数据成员（常量和字段）、函数成员（方法、属性、事件、索引器、运算符、实例构造函数、析构函数和静态构造函数）以及嵌套类型。类类型支持继承，这是一种使派生类可以扩展和特化基类的机制。类类型的实例使用对象创建表达式（§7.6.10.1）创建。

类类型在 §10 中描述。

某些预定义类类型在 C# 语言中具有特殊含义，如下表所述。

| 类类型 | 说明 |
|---|---|
| System.Object | 所有其他类型的最终基类。参见 §4.2.2。 |
| System.String | C# 语言的字符串类型。参见 §4.2.4。 |
| System.ValueType | 所有值类型的基类。参见 §4.1.1。 |
| System.Enum | 所有枚举类型的基类。参见 §14。 |
| System.Array | 所有数组类型的基类。参见 §12。 |
| System.Delegate | 所有委托类型的基类。参见 §15。 |
| System.Exception | 所有异常类型的基类。参见 §16。 |

### 4.2.2 object 类型

object 类类型是所有其他类型的最终基类。C# 中的每个类型都直接或间接派生自 object 类类型。

关键字 object 只是预定义类 System.Object 的别名。

### 4.2.3 dynamic 类型

dynamic 类型与 object 一样，可以引用任何对象。当运算符应用于 dynamic 类型的表达式时，其解析会推迟到程序运行时进行。因此，如果该运算符不能合法地应用于所引用的对象，编译期间不会报错。相反，当运算符的解析在运行时失败时，将引发异常。

dynamic 类型在 §4.7 中进一步描述，动态绑定在 §7.2.2 中描述。

### 4.2.4 string 类型

string 类型是一个密封类类型，直接继承自 object。string 类的实例表示 Unicode 字符串。

string 类型的值可以写成字符串字面量（§2.4.4.5）。

关键字 string 只是预定义类 System.String 的别名。

### 4.2.5 接口类型

接口定义一种契约。实现接口的类或结构必须遵守其契约。接口可以继承多个基接口，类或结构可以实现多个接口。

接口类型在 §13 中描述。

### 4.2.6 数组类型

数组是一种数据结构，包含零个或多个通过计算索引访问的变量。数组中包含的变量也称为数组元素，它们都具有相同的类型，该类型称为数组的元素类型。

数组类型在 §12 中描述。

### 4.2.7 委托类型

委托是一种数据结构，引用一个或多个方法。对于实例方法，它还引用其对应的对象实例。

在 C 或 C++ 中，与委托最接近的等效项是函数指针，但函数指针只能引用静态函数，而委托可以引用静态方法和实例方法。在后一种情况下，委托不仅存储对方法入口点的引用，还存储对调用该方法时所针对的对象实例的引用。

委托类型在 §15 中描述。

## 4.3 装箱和拆箱

装箱和拆箱的概念是 C# 类型系统的核心。它通过允许值类型的任何值转换为 object 类型以及从 object 类型转换回来，在值类型和引用类型之间提供了一座桥梁。装箱和拆箱使类型系统能够以统一的视图呈现，其中任何类型的值最终都可以当作对象处理。

### 4.3.1 装箱转换

装箱转换允许将值类型隐式转换为引用类型。存在以下装箱转换：

- 从任何值类型到 object 类型。
- 从任何值类型到 System.ValueType 类型。
- 从任何非可空值类型到该值类型实现的任何接口类型。
- 从任何可空类型到该可空类型的基础类型实现的任何接口类型。
- 从任何枚举类型到 System.Enum 类型。
- 从任何基础类型为枚举类型的可空类型到 System.Enum 类型。

注意，如果类型参数的隐式转换在运行时最终是从值类型转换为引用类型，则该转换将作为装箱转换执行（§6.1.10）。

对非可空值类型的值进行装箱包括分配一个对象实例并将该非可空值类型的值复制到该实例中。

对可空类型的值进行装箱时，如果该值为 null 值（HasValue 为 false），则产生 null 引用；否则产生对其基础值进行解包并装箱后的结果。

最好通过设想存在一个泛型装箱类来解释对非可空值类型的值进行装箱的实际过程，该类的行为如同声明如下：

```csharp
sealed class Box<T>: System.ValueType
{
    T value;
    public Box(T t) {
        value = t;
    }
}
```

现在，对类型 T 的值 v 进行装箱包括执行表达式 new Box<T>(v)，并将得到的实例作为 object 类型的值返回。因此，语句

```csharp
int i = 123;
object box = i;
```

在概念上对应于

```csharp
int i = 123;
object box = new Box<int>(i);
```

上面这样的装箱类 Box<T> 实际上并不存在，装箱值的动态类型实际上也不是类类型。相反，类型 T 的装箱值具有动态类型 T，并且使用 is 运算符进行动态类型检查可以简单地引用类型 T。例如，

```
int i = 123;
object box = i;
if (box is int) {
    Console.Write("Box contains an int");
}
```

将在控制台上输出字符串“Box contains an int”。

装箱转换意味着复制被装箱的值。这与将引用类型转换为 object 类型不同：在后一种转换中，值仍然引用同一实例，只是被视为派生程度较低的类型 object。例如，给定以下声明

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

将在控制台上输出值 10，因为将 p 赋给 box 时发生的隐式装箱操作会复制 p 的值。如果 Point 改为声明为类，则将输出值 20，因为 p 和 box 将引用同一实例。

### 4.3.2 拆箱转换

拆箱转换允许将引用类型显式转换为值类型。存在以下拆箱转换：

-   从类型 object 到任何值类型。
-   从类型 System.ValueType 到任何值类型。
-   从任何接口类型到任何实现该接口类型的非可空值类型。
-   从任何接口类型到基础类型实现该接口类型的任何可空类型。
-   从类型 System.Enum 到任何枚举类型。
-   从类型 System.Enum 到基础类型为枚举类型的任何可空类型。

请注意，到类型参数的显式转换如果在运行时最终从引用类型转换为值类型，则将作为拆箱转换执行（§6.2.6）。

到非可空值类型的拆箱操作包括：首先检查该对象实例是否为给定非可空值类型的装箱值，然后从该实例中复制出该值。

如果源操作数为 null，则到可空类型的拆箱将生成该可空类型的 null 值；否则，将生成将该对象实例拆箱为该可空类型的基础类型后的包装结果。

参考上一节中描述的假想装箱类，将 object 类型的 box 拆箱为值类型 T 的转换包括执行表达式 ((Box<T>)box).value。因此，以下语句

```
object box = 123;
int i = (int)box;
```

在概念上对应于

```
object box = new Box<int>(123);
int i = ((Box<int>)box).value;
```

要使到给定非可空值类型的拆箱转换在运行时成功，源操作数的值必须是指向该非可空值类型的装箱值的引用。如果源操作数为 null，则引发 System.NullReferenceException。如果源操作数是指向不兼容对象的引用，则引发 System.InvalidCastException。

要使到给定可空类型的拆箱转换在运行时成功，源操作数的值必须为 null，或者为指向该可空类型的基础非可空值类型的装箱值的引用。如果源操作数是指向不兼容对象的引用，则引发 System.InvalidCastException。

## 4.4 构造类型

泛型类型声明本身表示一个非绑定泛型类型，它被用作“蓝图”，通过应用类型实参来形成许多不同的类型。类型实参写在紧跟在泛型类型名称后面的尖括号（< 和 >）内。包含至少一个类型实参的类型称为构造类型。在语言中类型名称可以出现的大多数位置，都可以使用构造类型。非绑定泛型类型只能在 typeof 表达式（§7.6.11）中使用。

构造类型也可以在表达式中作为简单名称使用（§7.6.2），或者在访问成员时使用（§7.6.4）。

当计算命名空间或类型名时，只考虑具有正确类型参数数量的泛型类型。因此，只要类型具有不同的类型参数数量，就可以使用同一标识符来标识不同的类型。当在同一程序中混合使用泛型类和非泛型类时，这很有用：

```
namespace widgets
{
    class Queue {...}
    class Queue<TElement> {...}
}
namespace MyApplication
{
    using widgets;
    class X
    {
        Queue q1;        // Non-generic Widgets.Queue
        Queue<int> q2;   // Generic Widgets.Queue
    }
}
```

类型名即使不直接指定类型参数，也可能标识构造类型。当类型嵌套在泛型类声明中，并且隐式使用包含声明的实例类型进行名称查找时，就可能发生这种情况（§10.3.8.6）：

```
class Outer<T>
{
    public class Inner {...}
    public Inner i;        // Type of i is Outer<T>.Inner
}
```

在不安全代码中，构造类型不能用作非托管类型（§18.2）。

### 4.4.1 类型实参

类型实参列表中的每个实参只是一个类型。

```
type-argument-list:
    < type-arguments >
type-arguments:
    type-argument
    type-arguments , type-argument
type-argument:
    type
```

在不安全代码（§18）中，类型实参不能是指针类型。每个类型实参必须满足对应类型参数上的任何约束（§10.1.5）。

### 4.4.2 开放类型和封闭类型

所有类型都可以分类为开放类型或封闭类型。开放类型是涉及类型参数的类型。更具体地说：

-   类型参数定义开放类型。
-   数组类型是开放类型，当且仅当其元素类型是开放类型。
-   构造类型是开放类型，当且仅当其一个或多个类型实参是开放类型。构造嵌套类型是开放类型，当且仅当其一个或多个类型实参或其包含类型的一个或多个类型实参是开放类型。

封闭类型不是开放类型。

在运行时，泛型类型声明中的所有代码都在封闭构造类型的上下文中执行，该封闭构造类型是通过将类型实参应用于泛型声明而创建的。泛型类型中的每个类型参数都绑定到特定的运行时类型。所有语句和表达式的运行时处理总是在封闭类型中进行，而开放类型只在编译时处理期间出现。

每个封闭构造类型都有自己的一组静态变量，这些变量不与任何其他封闭构造类型共享。由于开放类型在运行时不存在，因此没有与开放类型关联的静态变量。如果两个封闭构造类型由同一非绑定泛型类型构造，并且它们对应的类型实参是同一类型，则这两个封闭构造类型是同一类型。

### 4.4.3 绑定类型和非绑定类型

术语非绑定类型指非泛型类型或非绑定泛型类型。术语绑定类型指非泛型类型或构造类型。

非绑定类型指由类型声明所声明的实体。非绑定泛型类型本身不是类型，不能用作变量、参数或返回值的类型，也不能用作基类型。可以引用非绑定泛型类型的唯一构造是 typeof 表达式（§7.6.11）。

### 4.4.4 满足约束

每当引用构造类型或泛型方法时，都会根据泛型类型或方法上声明的类型参数约束来检查提供的类型实参（§10.1.5）。对于每个 where 子句，与命名类型参数对应的类型实参 A 都会按如下方式对照每个约束进行检查：

-   如果约束是类类型、接口类型或类型参数，则令 C 表示用提供的类型实参替换约束中出现的任何类型参数后的该约束。为满足约束，必须满足：类型 A 可通过以下方式之一转换为类型 C：

- 标识转换（§6.1.1）
- 隐式引用转换（§6.1.6）
- 装箱转换（§6.1.7），前提是类型 A 为非可空值类型。
- 从类型参数 A 到 C 的隐式引用转换、装箱转换或类型参数转换。

- 如果约束是引用类型约束（`class`），则类型 A 必须满足以下条件之一：
  - A 是接口类型、类类型、委托类型或数组类型。注意，`System.ValueType` 和 `System.Enum` 是满足此约束的引用类型。
  - A 是已知为引用类型的类型参数（§10.1.5）。
- 如果约束是值类型约束（`struct`），则类型 A 必须满足以下条件之一：
  - A 是结构类型或枚举类型，但不是可空类型。注意，`System.ValueType` 和 `System.Enum` 是不满足此约束的引用类型。
  - A 是具有值类型约束的类型参数（§10.1.5）。
- 如果约束是构造函数约束 `new()`，则类型 A 不能是 `abstract`，并且必须具有公共无参数构造函数。如果以下条件之一成立，则满足此要求：
  - A 是值类型，因为所有值类型都具有公共默认构造函数（§4.1.2）。
  - A 是具有构造函数约束的类型参数（§10.1.5）。
  - A 是具有值类型约束的类型参数（§10.1.5）。
  - A 是不是 `abstract` 的类，并且包含显式声明的无参数 `public` 构造函数。
  - A 不是 `abstract`，并且具有默认构造函数（§10.11.4）。

如果给定的类型实参不满足类型参数的一个或多个约束，则发生编译时错误。

由于类型参数不会被继承，约束也永远不会被继承。在下面的示例中，D 需要为其类型参数 T 指定约束，以便 T 满足基类 B<T> 施加的约束。相反，类 E 无需指定约束，因为对于任何 T，List<T> 都实现 IEnumerable。

```csharp
class B<T> where T: IEnumerable {...}
class D<T>: B<T> where T: IEnumerable {...}
class E<T>: B<List<T>> {...}
```

## 4.5 类型参数

类型参数是一个标识符，它指定参数在运行时绑定到的值类型或引用类型。

```
type-parameter:
    identifier
```

由于类型参数可以用许多不同的实际类型实参来实例化，因此类型参数的操作和限制与其他类型略有不同。这些包括：

- 类型参数不能直接用于声明基类（§10.2.4）或接口（§13.1.3）。
- 类型参数的成员查找规则取决于应用于该类型参数的约束（如果有）。§7.4 对此进行了详细说明。
- 类型参数可用的转换取决于应用于该类型参数的约束（如果有）。§6.1.10 和 §6.2.6 对此进行了详细说明。
- 字面量 null 不能转换为由类型参数给定的类型，除非该类型参数已知为引用类型（§6.1.10）。但是，可以改用默认表达式（§7.6.13）。此外，由类型参数给定类型的值可以使用 == 和 != 与 null 进行比较（§7.10.6），除非该类型参数具有值类型约束。
- 仅当类型参数受构造函数约束或值类型约束（§10.1.5）约束时，new 表达式（§7.6.10.1）才能与该类型参数一起使用。
- 类型参数不能在特性中的任何位置使用。
- 类型参数不能在成员访问（§7.6.4）或类型名（§3.8）中用于标识静态成员或嵌套类型。
- 在不安全代码中，类型参数不能用作非托管类型（§18.2）。

作为一种类型，类型参数纯粹是编译时构造。在运行时，每个类型参数都绑定到一个运行时类型，该类型是通过向泛型类型声明提供类型实参而指定的。因此，用类型参数声明的变量在运行时的类型将是封闭构造类型（§4.4.2）。涉及类型参数的所有语句和表达式的运行时执行都使用作为该参数的类型实参提供的实际类型。

## 4.6 表达式树类型

表达式树允许将匿名函数表示为数据结构而不是可执行代码。表达式树是形式为 System.Linq.Expressions.Expression<D> 的表达式树类型的值，其中 D 是任意委托类型。在本规范的其余部分中，我们将使用简写 Expression<D> 来指代这些类型。

如果存在从匿名函数到委托类型 D 的转换，则也存在到表达式树类型 Expression<D> 的转换。将匿名函数转换为委托类型会生成一个委托，该委托引用匿名函数的可执行代码；而转换为表达式树类型则创建该匿名函数的表达式树表示。

表达式树是匿名函数的高效内存数据表示，并使匿名函数的结构透明且明确。

就像委托类型 D 一样，Expression<D> 也被认为具有参数类型和返回类型，这些类型与 D 的相同。

下面的示例将匿名函数同时表示为可执行代码和表达式树。由于存在到 Func<int, int> 的转换，因此也存在到 Expression<Func<int, int>> 的转换：

```csharp
Func<int,int> del = x => x + 1;      // Code
Expression<Func<int,int>> exp = x => x + 1;  // Data
```

执行这些赋值后，委托 del 引用一个返回 x + 1 的方法，而表达式树 exp 引用一个描述表达式 x => x + 1 的数据结构。

泛型类型 Expression<D> 的精确定义，以及将匿名函数转换为表达式树类型时构造表达式树的精确规则，均不在本规范的范围内，而是在其他地方描述。

有两点需要明确说明：

## C# 语言规范

- 并非所有匿名函数都能表示为表达式树。例如，具有语句体的匿名函数以及包含赋值表达式的匿名函数不能表示。在这些情况下，转换仍然存在，但会在编译时失败。
- Expression<D> 提供一个实例方法 Compile，该方法生成类型为 D 的委托：

```csharp
Func<int,int> del2 = exp.Compile();
```

调用此委托会导致执行表达式树所表示的代码。因此，给定上述定义，del 和 del2 是等效的，并且以下两个语句将具有相同的效果：

```
int i1 = del(1);
```

```
int i2 = del2(1);
```

执行此代码后，i1 和 i2 都将具有值 2。

## 4.7 dynamic 类型

dynamic 类型在 C# 中具有特殊含义。其目的是允许动态绑定，§7.2.2 对此进行了详细描述。

除以下方面外，dynamic 被视为与 object 完全相同：

- 对 dynamic 类型表达式的操作可以动态绑定（§7.2.2）。
- 如果 dynamic 和 object 都是候选，类型推断（§7.5.2）将优先选择 dynamic 而不是 object。

由于这种等价性，以下结论成立：

- 在 object 与 dynamic 之间，以及在将 dynamic 替换为 object 后相同的构造类型之间，存在隐式标识转换
- 与 object 之间的隐式和显式转换也适用于与 dynamic 之间的转换。
- 将 dynamic 替换为 object 后相同的方法签名被视为相同签名

在运行时，dynamic 类型与 object 无法区分。

dynamic 类型的表达式称为动态表达式。

## 5. 变量

变量表示存储位置。每个变量都有一个类型，该类型决定可以存储在变量中的值。C# 是一种类型安全的语言，C# 编译器保证存储在变量中的值始终具有适当的类型。变量的值可以通过赋值或使用 ++ 和 -- 运算符来更改。

在获取变量的值之前，必须明确赋值（§5.3）该变量。

如下文各节所述，变量要么是初始已赋值，要么是初始未赋值。初始已赋值的变量具有明确定义的初始值，并且始终被视为明确赋值。初始未赋值的变量没有初始值。要使初始未赋值的变量在某一位置被视为明确赋值，在通向该位置的每一条可能的执行路径上都必须对该变量进行赋值。

### 5.1 变量类别

C# 定义了七类变量：静态变量、实例变量、数组元素、值参数、引用参数、输出参数和局部变量。后续各节将描述这些类别中的每一类。

在下面的示例中

```csharp
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

x 是静态变量，y 是实例变量，v[0] 是数组元素，a 是值参数，b 是引用参数，c 是输出参数，i 是局部变量。

### 5.1.1 静态变量

使用 static 修饰符声明的字段称为静态变量。静态变量在其包含类型的静态构造函数（§10.12）执行之前就存在，并在关联的应用程序域不再存在时不再存在。

静态变量的初始值是该变量类型的默认值（§5.2）。

出于明确赋值检查的目的，静态变量被视为初始已赋值。

### 5.1.2 实例变量

未使用 static 修饰符声明的字段称为实例变量。

### 5.1.2.1 类中的实例变量

类的实例变量在该类的新实例创建时存在，并在没有对该实例的引用且该实例的析构函数（如果有）已执行时不再存在。

类的实例变量的初始值是该变量类型的默认值（§5.2）。




为了进行确定赋值检查，类的实例变量被视为初始已赋值。

### 5.1.2.2 结构中的实例变量

结构的实例变量与其所属的结构变量具有完全相同的生存期。换句话说，当结构类型的变量开始存在或停止存在时，该结构的实例变量也随之开始存在或停止存在。

结构实例变量的初始赋值状态与包含它的结构变量的初始赋值状态相同。换句话说，当结构变量被视为初始已赋值时，其实例变量也被视为初始已赋值；当结构变量被视为初始未赋值时，其实例变量也同样未赋值。

### 5.1.3 数组元素

数组元素在数组实例创建时开始存在，在该数组实例不再有任何引用时停止存在。

数组每个元素的初始值是该数组元素类型的默认值（§5.2）。

为了进行确定赋值检查，数组元素被视为初始已赋值。

### 5.1.4 值参数

声明时没有 ref 或 out 修饰符的参数是值参数。

值参数在调用其所属的函数成员（方法、实例构造函数、访问器或运算符）或匿名函数时开始存在，并使用调用中给定的参数值进行初始化。值参数通常在函数成员或匿名函数返回时停止存在。但是，如果值参数被匿名函数捕获（§7.15），其生存期至少会延长到从该匿名函数创建的委托或表达式树可被垃圾回收时为止。

为了进行确定赋值检查，值参数被视为初始已赋值。

### 5.1.5 引用参数

使用 ref 修饰符声明的参数是引用参数。

引用参数不会创建新的存储位置。相反，引用参数表示与函数成员或匿名函数调用中作为参数给定的变量相同的存储位置。因此，引用参数的值始终与底层变量相同。

以下确定赋值规则适用于引用参数。请注意 §5.1.6 中描述的输出参数的不同规则。

- 变量必须已确定赋值（§5.3），然后才能作为引用参数传递给函数成员或委托调用。
- 在函数成员或匿名函数内，引用参数被视为初始已赋值。

在结构类型的实例方法或实例访问器中，this 关键字的行为与结构类型的引用参数完全相同（§7.6.7）。

### 5.1.6 输出参数

使用 out 修饰符声明的参数是输出参数。

输出参数不会创建新的存储位置。相反，输出参数表示与函数成员或委托调用中作为参数给定的变量相同的存储位置。因此，输出参数的值始终与底层变量相同。

以下确定赋值规则适用于输出参数。请注意 §5.1.5 中描述的引用参数的不同规则。

- 变量不必先确定赋值，即可作为输出参数传递给函数成员或委托调用。
- 在函数成员或委托调用正常完成后，在该执行路径中，每个作为输出参数传递的变量都被视为已赋值。
- 在函数成员或匿名函数内，输出参数被视为初始未赋值。
- 函数成员或匿名函数的每个输出参数都必须在该函数成员或匿名函数正常返回之前已确定赋值（§5.3）。

在结构类型的实例构造函数中，this 关键字的行为与结构类型的输出参数完全相同（§7.6.7）。

### 5.1.7 局部变量

局部变量由局部变量声明声明，该声明可以出现在块、for 语句、switch 语句或 using 语句中；也可以由 foreach 语句或 try 语句的特定 catch 子句声明。

局部变量的生存期是程序执行期间保证为其保留存储的那一部分。该生存期至少从进入与其关联的块、for 语句、switch 语句、using 语句、foreach 语句或特定 catch 子句开始，直到该块、for 语句、switch 语句、using 语句、foreach 语句或特定 catch 子句以任何方式结束执行为止。（进入嵌套块或调用方法会挂起当前块、for 语句、switch 语句、using 语句、foreach 语句或特定 catch 子句的执行，但不会结束它。）如果局部变量被匿名函数捕获（§7.15.5.1），其生存期至少会延长到从该匿名函数创建的委托或表达式树，以及任何其他开始引用被捕获变量的对象，都可以被垃圾回收时为止。

如果父块、for 语句、switch 语句、using 语句、foreach 语句或特定 catch 子句被递归进入，则每次都会创建该局部变量的一个新实例，并且每次都会计算其局部变量初始化器（如果有的话）。

由局部变量声明引入的局部变量不会自动初始化，因此没有默认值。为了进行确定赋值检查，由局部变量声明引入的局部变量被视为初始未赋值。局部变量声明可以包含局部变量初始化器，在这种情况下，该变量仅在初始化表达式（§5.3.3.4）之后才被视为已确定赋值。

在由局部变量声明引入的局部变量的作用域内，在位于其局部变量声明符之前的文本位置引用该局部变量属于编译时错误。如果局部变量声明是隐式的（§8.5.1），在其局部变量声明符内引用该变量也属于错误。

由 foreach 语句或特定 catch 子句引入的局部变量在其整个作用域内都被视为已确定赋值。

局部变量的实际生存期取决于实现。例如，编译器可能会静态地确定块中的局部变量仅在该块的一小部分中被使用。利用这种分析，编译器可以生成代码，使该变量的存储的生存期比其所在块的生存期更短。

局部引用变量所引用的存储，其回收独立于该局部引用变量的生存期（§3.9）。

## 5.2 默认值

以下类别的变量会自动初始化为其默认值：

- 静态变量。
- 类实例的实例变量。
- 数组元素。

变量的默认值取决于变量的类型，并按如下方式确定：

- 对于值类型的变量，默认值与该值类型的默认构造函数（§4.1.2）计算出的值相同。
- 对于引用类型的变量，默认值为 null。

默认值的初始化通常由内存管理器或垃圾回收器在内存分配用于使用之前将其初始化为全零位来完成。因此，使用全零位来表示空引用是很方便的。

## 5.3 确定赋值

在函数成员的可执行代码中的给定位置，如果编译器可以通过特定的静态流分析（§5.3.3）证明变量已被自动初始化或已是至少一次赋值的对象，则称该变量已确定赋值。非正式地说，确定赋值的规则如下：

- 初始已赋值的变量（§5.3.1）始终被视为已确定赋值。
- 初始未赋值的变量（§5.3.2）在给定位置被视为已确定赋值，如果到达该位置的所有可能执行路径都包含以下至少一项：
  - 变量是左操作数的简单赋值（§7.17.1）。
  - 将变量作为输出参数传递的调用表达式（§7.6.5）或对象创建表达式（§7.6.10.1）。
  - 对于局部变量，包含变量初始化器的局部变量声明（§8.5.1）。

上述非正式规则所依据的形式规范在 §5.3.1、§5.3.2 和 §5.3.3 中描述。

结构类型变量的实例变量的确定赋值状态会被单独跟踪，也会被整体跟踪。除了上述规则外，以下规则适用于结构类型变量及其实例变量：

- 如果实例变量所属的结构类型变量被视为已确定赋值，则该实例变量被视为已确定赋值。
- 如果结构类型变量的每个实例变量都被视为已确定赋值，则该结构类型变量被视为已确定赋值。

在以下上下文中，确定赋值是一项要求：

- 变量在获取其值的每个位置都必须已确定赋值。这可以确保永远不会出现未定义的值。变量在表达式中的出现被视为获取该变量的值，但以下情况除外：
  - 变量是简单赋值的左操作数；
  - 变量作为输出参数传递；或
  - 变量是结构类型变量，并且作为成员访问的左操作数出现。



-   变量在作为引用参数传递的每个位置都必须已明确赋值。这确保被调用的函数成员可以将该引用参数视为最初已赋值。
-   函数成员的所有输出参数在该函数成员返回的每个位置（通过 `return` 语句返回，或通过执行到达函数成员主体末尾而返回）都必须已明确赋值。这确保函数成员不会在输出参数中返回未定义的值，从而使编译器能够将以变量作为输出参数的函数成员调用视为对该变量的赋值。
-   `struct-type` 实例构造函数的 `this` 变量在该实例构造函数返回的每个位置都必须已明确赋值。

## 5.3.1 初始已赋值的变量

以下类别的变量被归类为初始已赋值：

-   静态变量。
-   类实例的实例变量。
-   初始已赋值的结构变量的实例变量。
-   数组元素。
-   值参数。
-   引用参数。
-   在 `catch` 子句或 `foreach` 语句中声明的变量。

## 5.3.2 初始未赋值的变量

以下类别的变量被归类为初始未赋值：

-   初始未赋值的结构变量的实例变量。
-   输出参数，包括结构实例构造函数的 `this` 变量。
-   局部变量，但在 `catch` 子句或 `foreach` 语句中声明的变量除外。

## 5.3.3 确定明确赋值的精确规则

为了确定每个使用的变量都已明确赋值，编译器必须使用与本节所述过程等效的过程。

编译器处理每个具有一个或多个初始未赋值变量的函数成员的主体。对于每个初始未赋值变量 v，编译器在函数成员中的以下每个位置确定 v 的明确赋值状态：

-   每条语句的开始处
-   每条语句的结束点（§8.1）
-   每条将控制转移到另一语句或语句结束点的弧上
-   每个表达式的开始处
-   每个表达式的结束处

v 的明确赋值状态可以是：

-   已明确赋值。这表示在到达此位置的所有可能控制流上，v 都已被赋值。
-   未明确赋值。对于 `bool` 类型表达式结束时变量的状态，未明确赋值的变量状态可能（但不一定）属于以下子状态之一：
    -   true 表达式后已明确赋值。此状态表示如果布尔表达式求值为 true，则 v 已明确赋值；但如果布尔表达式求值为 false，则不一定已赋值。
    -   false 表达式后已明确赋值。此状态表示如果布尔表达式求值为 false，则 v 已明确赋值；但如果布尔表达式求值为 true，则不一定已赋值。

以下规则规定如何确定变量 v 在每个位置的状态。

### 5.3.3.1 语句的一般规则

-   v 在函数成员主体的开始处未明确赋值。
-   v 在任何不可达语句的开始处已明确赋值。
-   v 在任何其他语句开始处的明确赋值状态，通过检查所有以该语句开始处为目标控制流转移上的 v 的明确赋值状态来确定。当且仅当 v 在所有此类控制流转移上均已明确赋值时，v 在该语句开始处才已明确赋值。可能的控制流转移集合的确定方式与检查语句可达性（§8.1）相同。
-   v 在块、checked、unchecked、if、while、do、for、foreach、lock、using 或 switch 语句结束点的明确赋值状态，通过检查所有以该语句结束点为目标控制流转移上的 v 的明确赋值状态来确定。如果 v 在所有此类控制流转移上均已明确赋值，则 v 在该语句结束点已明确赋值。否则，v 在该语句结束点未明确赋值。可能的控制流转移集合的确定方式与检查语句可达性（§8.1）相同。

### 5.3.3.2 块语句、checked 语句和 unchecked 语句

在控制转移到块中语句列表的第一条语句（如果语句列表为空，则转移到块的结束点）时，v 的明确赋值状态与块、checked 或 unchecked 语句之前的 v 的明确赋值状态相同。

### 5.3.3.3 表达式语句

对于由表达式 expr 组成的表达式语句 stmt：

-   v 在 expr 开始处的明确赋值状态与在 stmt 开始处的明确赋值状态相同。
-   如果 v 在 expr 结束处已明确赋值，则它在 stmt 结束点已明确赋值；否则，它在 stmt 结束点未明确赋值。

### 5.3.3.4 声明语句

-   如果 stmt 是不带初始值设定项的声明语句，则 v 在 stmt 结束点的明确赋值状态与在 stmt 开始处的明确赋值状态相同。
-   如果 stmt 是带初始值设定项的声明语句，则 v 的明确赋值状态按如下方式确定：如同 stmt 是一个语句列表，其中每个带初始值设定项的声明对应一个赋值语句（按声明顺序）。

### 5.3.3.5 if 语句

对于形式如下的 if 语句 stmt：

```
if ( expr ) then-stmt else else-stmt
```

-   v 在 expr 开始处的明确赋值状态与在 stmt 开始处的明确赋值状态相同。
-   如果 *v* 在 *expr* 结束处已明确赋值，则它在控制流转移到 *then-stmt* 时已明确赋值，并且在无 else 子句时控制流转移到 *else-stmt* 或 *stmt* 结束点时也已明确赋值。
-   如果 *v* 在 *expr* 结束处具有“true 表达式后已明确赋值”状态，则它在控制流转移到 *then-stmt* 时已明确赋值，而在无 else 子句时控制流转移到 *else-stmt* 或 *stmt* 结束点时未明确赋值。
-   如果 *v* 在 *expr* 结束处具有“false 表达式后已明确赋值”状态，则它在控制流转移到 *else-stmt* 时已明确赋值，而在控制流转移到 *then-stmt* 时未明确赋值。当且仅当它在 *then-stmt* 结束点已明确赋值时，它才在 *stmt* 结束点已明确赋值。
-   否则，*v* 被视为在控制流转移到 *then-stmt* 或 *else-stmt* 时未明确赋值，或者在无 else 子句时在控制流转移到 *stmt* 结束点时未明确赋值。

### 5.3.3.6 switch 语句

在带有控制表达式 *expr* 的 *switch* 语句 *stmt* 中：

-   *v* 在 *expr* 开始处的明确赋值状态与 *v* 在 *stmt* 开始处的状态相同。
-   *v* 在控制流转移到可到达的 switch 块语句列表时的明确赋值状态，与 *v* 在 *expr* 结束处的明确赋值状态相同。

### 5.3.3.7 while 语句

对于形式如下的 *while* 语句 *stmt*：

```
while ( expr ) while-body
```

-   *v* 在 *expr* 开始处的明确赋值状态与在 *stmt* 开始处的明确赋值状态相同。
-   如果 *v* 在 *expr* 结束处已明确赋值，则它在控制流转移到 *while-body* 时以及在 *stmt* 结束点都已明确赋值。
-   如果 *v* 在 *expr* 结束处具有“true 表达式后已明确赋值”状态，则它在控制流转移到 *while-body* 时已明确赋值，但在 *stmt* 结束点未明确赋值。
-   如果 *v* 在 *expr* 结束处具有“false 表达式后已明确赋值”状态，则它在控制流转移到 *stmt* 结束点时已明确赋值，但在控制流转移到 *while-body* 时未明确赋值。

### 5.3.3.8 do 语句

对于形式如下的 *do* 语句 *stmt*：

```
do do-body while ( expr ) ;
```

-   *v* 在控制流从 *stmt* 开始处转移到 *do-body* 时的明确赋值状态，与在 *stmt* 开始处的明确赋值状态相同。
-   *v* 在 *expr* 开始处的明确赋值状态与在 *do-body* 结束点的明确赋值状态相同。
-   如果 *v* 在 *expr* 结束处已明确赋值，则它在控制流转移到 *stmt* 结束点时已明确赋值。
-   如果 *v* 在 *expr* 结束处具有“false 表达式后已明确赋值”状态，则它在控制流转移到 *stmt* 结束点时已明确赋值。




## 5.3.3.9 for 语句

对于以下形式的 for 语句：

```
for ( for-initializer ; for-condition ; for-iterator ) embedded-statement
```

其确定赋值检查按如下方式执行，就好像该语句写成：

```
{
  for-initializer ;
  while ( for-condition ) {
    embedded-statement ;
    for-iterator ;
  }
}
```

如果 for 语句中省略了 for-condition，则确定赋值的计算按如下方式进行，就好像在上述展开中将 for-condition 替换为 true。

## 5.3.3.10 break、continue 和 goto 语句

由 break、continue 或 goto 语句引起的控制流转移上，v 的确定赋值状态与该语句开头处 v 的确定赋值状态相同。

## 5.3.3.11 throw 语句

对于以下形式的语句 stmt

```
throw expr ;
```

expr 开头处 v 的确定赋值状态与 stmt 开头处 v 的确定赋值状态相同。

## 5.3.3.12 return 语句

对于以下形式的语句 stmt

```
return expr ;
```

- expr 开头处 v 的确定赋值状态与 stmt 开头处 v 的确定赋值状态相同。
- 如果 v 是输出参数，则必须在以下任一位置确定赋值：
  - expr 之后
  - 或在包含该 return 语句的 try-finally 或 try-catch-finally 的 finally 块末尾。

对于以下形式的语句 stmt：

```
return ;
```

- 如果 v 是输出参数，则必须在以下任一位置确定赋值：
  - stmt 之前
  - 或在包含该 return 语句的 try-finally 或 try-catch-finally 的 finally 块末尾。

## 5.3.3.13 try-catch 语句

对于以下形式的语句 stmt：

```
try try-block
catch(...) catch-block-1
...
catch(...) catch-block-n
```

- try-block 开头处 v 的确定赋值状态与 stmt 开头处 v 的确定赋值状态相同。
- catch-block-i（对于任意 i）开头处 v 的确定赋值状态与 stmt 开头处 v 的确定赋值状态相同。
- 当且仅当 v 在 try-block 的结束点以及每个 catch-block-i（对于从 1 到 n 的每个 i）的结束点均确定赋值时，v 在 stmt 的结束点才确定赋值。

## 5.3.3.14 try-finally 语句

对于以下形式的 try 语句 stmt：

```
try try-block finally finally-block
```

- try-block 开头处 v 的确定赋值状态与 stmt 开头处 v 的确定赋值状态相同。
- finally-block 开头处 v 的确定赋值状态与 stmt 开头处 v 的确定赋值状态相同。
- 当且仅当以下至少一项为真时，v 在 stmt 的结束点才确定赋值：
  - v 在 try-block 的结束点确定赋值
  - v 在 finally-block 的结束点确定赋值

如果发生一个控制流转移（例如 goto 语句），该转移始于 try-block 内并止于 try-block 外，那么如果 v 在 finally-block 的结束点确定赋值，则在该控制流转移上 v 也被视为确定赋值。（这并不是一个“仅当”——如果 v 在该控制流转移上由于其他原因而确定赋值，则仍被视为确定赋值。）

## 5.3.3.15 try-catch-finally 语句

对于以下形式的 try-catch-finally 语句：

```
try try-block
catch(...) catch-block-1
...
catch(...) catch-block-n
finally finally-block
```

其确定赋值分析按如下方式执行，就好像该语句是一个包含 try-catch 语句的 try-finally 语句：

```
try {
  try try-block
  catch(...) catch-block-1
  ...
  catch(...) catch-block-n
}
finally finally-block
```

以下示例演示 try 语句（§8.10）的不同块如何影响确定赋值。

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
```

## 5.3.3.16 foreach 语句

对于以下形式的 foreach 语句 stmt：

```
foreach ( type identifier in expr ) embedded-statement
```

- expr 开头处 v 的确定赋值状态与 stmt 开头处 v 的状态相同。
- 在转移到 embedded-statement 或 stmt 结束点的控制流转移上，v 的确定赋值状态与 expr 末尾处 v 的状态相同。

## 5.3.3.17 using 语句

对于以下形式的 using 语句 stmt：

```
using ( resource-acquisition ) embedded-statement
```

- resource-acquisition 开头处 v 的确定赋值状态与 stmt 开头处 v 的状态相同。
- 在转移到 embedded-statement 的控制流转移上，v 的确定赋值状态与 resource-acquisition 结束点处 v 的状态相同。

## 5.3.3.18 lock 语句

对于以下形式的 lock 语句 stmt：

```
lock ( expr ) embedded-statement
```

- expr 开头处 v 的确定赋值状态与 stmt 开头处 v 的状态相同。
- 在转移到 embedded-statement 的控制流转移上，v 的确定赋值状态与 expr 结束点处 v 的状态相同。

## 5.3.3.19 yield 语句

对于以下形式的 yield return 语句 *stmt*：

```
    yield return expr ;
```

- *v* 在 *expr* 开头处的确定赋值状态与 *v* 在 *stmt* 开头处的状态相同。
- *v* 在 *stmt* 结束处的确定赋值状态与 *v* 在 *expr* 结束处的状态相同。

yield break 语句对确定赋值状态没有影响。

## 5.3.3.20 简单表达式的一般规则

以下规则适用于这些类型的表达式：字面量（§7.6.1）、简单名称（§7.6.2）、成员访问表达式（§7.6.4）、非索引基访问表达式（§7.6.8）、typeof 表达式（§7.6.11）和默认值表达式（§7.6.13）。

- 在此类表达式的结束处，*v* 的确定赋值状态与 *v* 在该表达式开头处的确定赋值状态相同。

## 5.3.3.21 带嵌入表达式的表达式的一般规则

以下规则适用于这些类型的表达式：带括号表达式（§7.6.3）、元素访问表达式（§7.6.6）、带索引的基访问表达式（§7.6.8）、递增和递减表达式（§7.6.9、§7.7.5）、强制转换表达式（§7.7.6）、一元 +、-、~、* 表达式，二元 +、-、*、/、%、<<、>>、<、>、<=、>=、==、!=、is、as、&、|、^ 表达式（§7.8、§7.9、§7.10、§7.11）、复合赋值表达式（§7.17.2）、checked 和 unchecked 表达式（§7.6.12），以及数组和委托创建表达式（§7.6.10）。

这些表达式中的每一个都有一个或多个按固定顺序无条件求值的子表达式。例如，二元 % 运算符先求运算符左侧的值，再求右侧的值。索引操作先求被索引表达式的值，然后按从左到右的顺序求每个索引表达式的值。对于表达式 *expr*，其子表达式 *expr₁*、*expr₂*、...、*exprₙ* 按该顺序求值：

- *v* 在 *exprᵢ* 开头处的确定赋值状态与在 *expr* 开头处的确定赋值状态相同。
- *v* 在 *exprᵢ* 开头处（*i* 大于 1）的确定赋值状态与在 *exprᵢ₋₁* 结束处的确定赋值状态相同。
- *v* 在 *expr* 结束处的确定赋值状态与在 *exprₙ* 结束处的确定赋值状态相同。

## 5.3.3.22 调用表达式和对象创建表达式

对于以下形式的调用表达式 *expr*：

```
    primary-expression ( arg₁ , arg₂ , ... , argₙ )
```

或以下形式的对象创建表达式：

```
    new type ( arg₁ , arg₂ , ... , argₙ )
```

- 对于调用表达式，*v* 在 *primary-expression* 之前的确定赋值状态与 *v* 在 *expr* 之前的状态相同。
- 对于调用表达式，*v* 在 *argᵢ* 之前的确定赋值状态与 *v* 在 *primary-expression* 之后的状态相同。




## C# 语言规范

- 对于对象创建表达式，v 在 arg_i 之前的明确赋值状态与 v 在 expr 之前的状态相同。
- 对于每个参数 arg_i，v 在 arg_i 之后的明确赋值状态由普通表达式规则确定，忽略任何 ref 或 out 修饰符。
- 对于每个参数 arg_i，对于大于一的任意 i，v 在 arg_i 之前的明确赋值状态与 v 在 arg_{i-1} 之后的状态相同。
- 如果变量 v 作为 out 参数（即形式为 "out v" 的参数）在任何参数中传递，则 v 在 expr 之后的状态是明确赋值的。否则，v 在 expr 之后的状态与 v 在 arg_n 之后的状态相同。
- 对于数组初始化器 (§7.6.10.4)、对象初始化器 (§7.6.10.2)、集合初始化器 (§7.6.10.3) 和匿名对象初始化器 (§7.6.10.6)，明确赋值状态由这些结构所定义的展开式确定。

### 5.3.3.23 简单赋值表达式

对于形式为 w = expr-rhs 的表达式 expr：

- v 在 expr-rhs 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- 如果 w 与 v 是同一变量，则 v 在 expr 之后的明确赋值状态是明确赋值的。否则，v 在 expr 之后的明确赋值状态与 v 在 expr-rhs 之后的明确赋值状态相同。

### 5.3.3.24 && 表达式

对于形式为 expr-first && expr-second 的表达式 expr：

- v 在 expr-first 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- 如果 v 在 expr-first 之后的状态是明确赋值或 "在真表达式后已明确赋值"，则 v 在 expr-second 之前的明确赋值状态是明确赋值的。否则，不是明确赋值的。
- v 在 expr 之后的明确赋值状态由以下规则确定：
  - 如果 v 在 expr-first 之后的状态是明确赋值的，则 v 在 expr 之后的状态是明确赋值的。
  - 否则，如果 v 在 expr-second 之后的状态是明确赋值的，且 v 在 expr-first 之后的状态是 "在假表达式后已明确赋值"，则 v 在 expr 之后的状态是明确赋值的。
  - 否则，如果 v 在 expr-second 之后的状态是明确赋值或 "在真表达式后已明确赋值"，则 v 在 expr 之后的状态是 "在真表达式后已明确赋值"。
  - 否则，如果 v 在 expr-first 之后的状态是 "在假表达式后已明确赋值"，且 v 在 expr-second 之后的状态是 "在假表达式后已明确赋值"，则 v 在 expr 之后的状态是 "在假表达式后已明确赋值"。
  - 否则，v 在 expr 之后的状态不是明确赋值的。

示例中

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

变量 i 在 if 语句的一个嵌入语句中被视为已明确赋值，而在另一个中则不是。在方法 F 中的 if 语句中，变量 i 在第一个嵌入语句中是明确赋值的，因为表达式 (i = y) 的执行总是先于该嵌入语句的执行。相比之下，变量 i 在第二个嵌入语句中不是明确赋值的，因为 x >= 0 可能测试为假，导致变量 i 未被赋值。

### 5.3.3.25 || 表达式

对于形式为 expr-first || expr-second 的表达式 expr：

- v 在 expr-first 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- 如果 v 在 expr-first 之后的状态是明确赋值或 “在假表达式后已明确赋值”，则 v 在 expr-second 之前的明确赋值状态是明确赋值的。否则，不是明确赋值的。
- v 在 expr 之后的明确赋值状态由以下规则确定：
  - 如果 v 在 expr-first 之后的状态是明确赋值的，则 v 在 expr 之后的状态是明确赋值的。
  - 否则，如果 v 在 expr-second 之后的状态是明确赋值的，且 v 在 expr-first 之后的状态是 “在真表达式后已明确赋值”，则 v 在 expr 之后的状态是明确赋值的。
  - 否则，如果 v 在 expr-second 之后的状态是明确赋值或 “在假表达式后已明确赋值”，则 v 在 expr 之后的状态是 “在假表达式后已明确赋值”。
  - 否则，如果 v 在 expr-first 之后的状态是 “在真表达式后已明确赋值”，且 v 在 expr-second 之后的状态是 “在真表达式后已明确赋值”，则 v 在 expr 之后的状态是 “在真表达式后已明确赋值”。
  - 否则，v 在 expr 之后的状态不是明确赋值的。

示例中

```
class A
{
    static void G(int x, int y) {
        int i;
        if (x >= 0 || (i = y) >= 0) {
            // i not definitely assigned
        }
        else {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```

变量 i 在 if 语句的一个嵌入语句中被视为已明确赋值，而在另一个中则不是。在方法 G 中的 if 语句中，变量 i 在第二个嵌入语句中是明确赋值的，因为表达式 (i = y) 的执行总是先于该嵌入语句的执行。相比之下，变量 i 在第一个嵌入语句中不是明确赋值的，因为 x >= 0 可能测试为真，导致变量 i 未被赋值。

### 5.3.3.26 ! 表达式

对于形式为 ! expr-operand 的表达式 expr：

- v 在 expr-operand 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- v 在 expr 之后的明确赋值状态由以下规则确定：
  - 如果 v 在 expr-operand 之后的状态是明确赋值的，则 v 在 expr 之后的状态是明确赋值的。
  - 如果 v 在 expr-operand 之后的状态不是明确赋值的，则 v 在 expr 之后的状态不是明确赋值的。
  - 如果 v 在 expr-operand 之后的状态是 "在假表达式后已明确赋值"，则 v 在 expr 之后的状态是 "在真表达式后已明确赋值"。
  - 如果 v 在 expr-operand 之后的状态是 "在真表达式后已明确赋值"，则 v 在 expr 之后的状态是 "在假表达式后已明确赋值"。

### 5.3.3.27 ?? 表达式

对于形式为 expr-first ?? expr-second 的表达式 expr：

- v 在 expr-first 之前的明确赋值状态与 v 在 expr 之前的明确赋值状态相同。
- v 在 expr-second 之前的明确赋值状态与 v 在 expr-first 之后的状态相同。
- v 在 expr 之后的明确赋值状态由以下规则确定：
  - 如果 expr-first 是值为 null 的常量表达式 (§7.19)，则 v 在 expr 之后的状态与 v 在 expr-second 之后的状态相同。
- 否则，v 在 expr 之后的状态与 v 在 expr-first 之后的明确赋值状态相同。

### 5.3.3.28 ?: 表达式

对于形式为 expr-cond ? expr-true : expr-false 的表达式 expr：

- v 在 expr-cond 之前的明确赋值状态与 v 在 expr 之前的状态相同。
- v 在 expr-true 之前的明确赋值状态当且仅当 v 在 expr-cond 之后的状态是明确赋值或 "在真表达式后已明确赋值" 时才是明确赋值的。
- v 在 expr-false 之前的明确赋值状态当且仅当 v 在 expr-cond 之后的状态是明确赋值或 "在假表达式后已明确赋值" 时才是明确赋值的。
- v 在 expr 之后的明确赋值状态由以下规则确定：
  - 如果 expr-cond 是值为 true 的常量表达式 (§7.19)，则 v 在 expr 之后的状态与 v 在 expr-true 之后的状态相同。



- 否则，如果 expr-cond 是常量表达式 (§7.19) 且值为 false，则 v 在 expr 之后的状态与 v 在 expr-false 之后的状态相同。
- 否则，如果 v 在 expr-true 之后的状态是已明确赋值且 v 在 expr-false 之后的状态是已明确赋值，则 v 在 expr 之后的状态是已明确赋值。
- 否则，v 在 expr 之后的状态未明确赋值。

## 5.3.3.29 匿名函数

对于具有主体（块或表达式）body 的 lambda 表达式或匿名方法表达式 expr：

- 匿名函数主体 body 执行前外部变量 v 的明确赋值状态与 v 在 expr 之前的状态相同。也就是说，外部变量的明确赋值状态从匿名函数的上下文继承而来。
- 外部变量 v 在 expr 之后 的明确赋值状态与 v 在 expr 之前的状态相同。

示例

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

生成编译时错误，因为在声明匿名函数的位置 max 未明确赋值。

示例

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

也会生成编译时错误，因为匿名函数中对 n 的赋值对匿名函数外部 n 的明确赋值状态没有影响。

## 5.4 变量引用

变量引用是被归类为变量的表达式。变量引用表示一个存储位置，可以访问以获取当前值并存储新值。

variable-reference:
    expression

在 C 和 C++ 中，变量引用被称为左值（lvalue）。

## 5.5 变量引用的原子性

以下数据类型的读取和写入是原子的：bool、char、byte、sbyte、short、ushort、uint、int、float 以及引用类型。此外，具有前述列表中底层类型的枚举类型的读取和写入也是原子的。其他类型的读取和写入，包括 long、ulong、double 和 decimal 以及用户定义的类型，并不保证是原子的。除专门为此目的设计的库函数外，读-改-写操作（如自增或自减）不保证是原子的。

## 6. 转换

转换使表达式可被视为特定类型。转换可能导致给定类型的表达式被视为具有不同类型，或者可能导致无类型的表达式获得类型。转换可以是隐式的或显式的，这决定是否需要显式强制转换。例如，从类型 int 到类型 long 的转换是隐式的，因此 int 类型的表达式可以隐式地被视为 long 类型。相反的转换，从 long 类型到 int 类型是显式的，因此需要显式强制转换。

```
int a = 123;
long b = a;    // implicit conversion from int to long
int c = (int) b; // explicit conversion from long to int
```

一些转换由语言定义。程序也可以定义自己的转换 (§6.4)。

## 6.1 隐式转换

以下转换被归类为隐式转换：

- 身份转换
- 隐式数值转换
- 隐式枚举转换。
- 隐式可空转换
- 空字面量转换
- 隐式引用转换
- 装箱转换
- 隐式动态转换
- 隐式常量表达式转换
- 用户定义的隐式转换
- 匿名函数转换
- 方法组转换

隐式转换可以在多种情况下发生，包括函数成员调用 (§7.5.4)、强制转换表达式 (§7.7.6) 和赋值 (§7.17)。

预定义的隐式转换总是成功且永远不会引发异常。设计良好的用户定义的隐式转换也应具有这些特性。

就转换而言，类型 object 和 dynamic 被视为等价。

然而，动态转换 (§6.1.8 和 §6.2.6) 仅适用于类型为 dynamic (§4.7) 的表达式。

## 6.1.1 身份转换

身份转换将任意类型转换为同一类型。此转换存在是为了使已经具有所需类型的实体可以被认为可转换为该类型。

由于 object 和 dynamic 被视为等价，因此 object 和 dynamic 之间存在身份转换，并且在将 dynamic 的所有出现替换为 object 后相同的构造类型之间也存在身份转换。

## 6.1.2 隐式数值转换

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

不存在到 char 类型的隐式转换，因此其他整型的值不会自动转换为 char 类型。

## 6.1.3 隐式枚举转换

隐式枚举转换允许十进制整数字面量 0 转换为任何枚举类型以及底层类型为枚举类型的任何可空类型。在后一种情况下，转换通过转换为底层枚举类型并包装结果 (§4.1.10) 来求值。

## 6.1.4 隐式可空转换

作用于不可空值类型的预定义隐式转换也可以与这些类型的可空形式一起使用。对于每个从不可空值类型 S 转换为不可空值类型 T 的预定义隐式身份和数值转换，存在以下隐式可空转换：

- 从 S? 到 T? 的隐式转换。
- 从 S 到 T? 的隐式转换。

基于从 S 到 T 的底层转换的隐式可空转换的求值如下进行：

- 如果可空转换是从 S? 到 T?：
  - 如果源值为 null（HasValue 属性为 false），结果为类型 T? 的 null 值。
  - 否则，转换被求值为空从 S? 解包到 S，然后进行从 S 到 T 的底层转换，然后从 T 包装 (§4.1.10) 到 T?。
- 如果可空转换是从 S 到 T?，则转换被求值为空从 S 到 T 的底层转换然后从 T 包装到 T?。

## 6.1.5 空字面量转换

从 null 字面量到任何可空类型存在隐式转换。此转换产生给定可空类型的 null 值 (§4.1.10)。

## 6.1.6 隐式引用转换

隐式引用转换如下：

- 从任何引用类型到 object 和 dynamic。
- 从任何类类型 S 到任何类类型 T，前提是 S 派生自 T。
- 从任何类类型 S 到任何接口类型 T，前提是 S 实现 T。
- 从任何接口类型 S 到任何接口类型 T，前提是 S 派生自 T。
- 从元素类型为 S_E 的数组类型 S 到元素类型为 T_E 的数组类型 T，前提是以下全部为真：
  - S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同数量的维度。
  - S_E 和 T_E 都是引用类型。
  - 从 S_E 到 T_E 存在隐式引用转换。
- 从任何数组类型到 System.Array 及其实现的接口。
- 从单维数组类型 S[] 到 System.Collections.Generic.IList<T> 及其基接口，前提是存在从 S 到 T 的隐式身份或引用转换。
- 从任何委托类型到 System.Delegate 及其实现的接口。
- 从 null 字面量到任何引用类型。
- 从任何引用类型到引用类型 T，如果它具有到引用类型 T0 的隐式身份或引用转换且 T0 具有到 T 的身份转换。
- 从任何引用类型到接口或委托类型 T，如果它具有到接口或委托类型 T0 的隐式身份或引用转换且 T0 可方差转换为 (§13.1.3.2) T。
- 涉及已知为引用类型的类型参数的隐式转换。有关涉及类型参数的隐式转换的更多详细信息，请参阅 §6.1.10。

隐式引用转换是可在编译时证明总是成功的引用类型之间的转换，因此在运行时不需要检查。

引用转换，无论是隐式还是显式，从不改变被转换对象的引用标识。换句话说，虽然引用转换可能会改变引用的类型，但它永远不会改变所引用对象的类型或值。

## 6.1.7 装箱转换

装箱转换允许值类型隐式转换为引用类型。任何不可空值类型到 object 和 dynamic、到 System.ValueType 以及到该不可空值类型实现的任何接口类型都存在装箱转换。此外，枚举类型可以转换为 System.Enum 类型。

当且仅当底层不可空值类型到该引用类型存在装箱转换时，从可空类型到引用类型才存在装箱转换。

如果值类型具有到接口类型 I0 的装箱转换且 I0 具有到 I 的身份转换，则该值类型具有到接口类型 I 的装箱转换。



值类型对接口类型 I 具有装箱转换，如果它对接口或委托类型 I0 具有装箱转换，并且 I0 可方差转换为 I（§13.1.3.2）。

装箱不可空值类型的值包括分配一个对象实例并将值类型的值复制到该实例中。结构体可以装箱为类型 System.ValueType，因为它是所有结构体的基类（§11.3.2）。

装箱可空类型的值按如下方式进行：

- 如果源值为 null（HasValue 属性为 false），结果为目标类型的空引用。
- 否则，结果是对通过解包并装箱源值而产生的装箱 T 的引用。

装箱转换在 §4.3.1 中进一步描述。

### 6.1.8 隐式动态转换

从类型为 dynamic 的表达式到任意类型 T 存在隐式动态转换。该转换是动态绑定的（§7.2.2），这意味着在运行时会从表达式的运行时类型到 T 寻找隐式转换。如果找不到转换，则会抛出运行时异常。

请注意，此隐式转换似乎违反了 §6.1 开头中“隐式转换绝不应导致异常”的建议。然而，并非转换本身，而是查找转换导致了异常。运行时异常的风险是使用动态绑定的固有特性。如果不希望转换进行动态绑定，则可以将表达式先转换为 object，然后再转换为所需类型。

以下示例说明了隐式动态转换：

```
object o = "object";
dynamic d = "dynamic";
string s1 = o; // Fails at compile-time - no conversion exists
string s2 = d; // Compiles and succeeds at run-time
int i = d; // Compiles but fails at run-time - no conversion exists
```

对 s2 和 i 的赋值都采用了隐式动态转换，其中操作的绑定被推迟到运行时。在运行时，会从 d 的运行时类型 – string – 到目标类型寻找隐式转换。可以找到到 string 的转换，但找不到到 int 的转换。

### 6.1.9 隐式常量表达式转换

隐式常量表达式转换允许以下转换：

- 类型为 int 的常量表达式（§7.19）可以转换为类型 sbyte、byte、short、ushort、uint 或 ulong，前提是常量表达式的值在目标类型的范围内。
- 类型为 long 的常量表达式可以转换为类型 ulong，前提是常量表达式的值不为负。

### 6.1.10 涉及类型参数的隐式转换

对于给定的类型参数 T，存在以下隐式转换：

- 从 T 到其有效基类 C，从 T 到 C 的任何基类，以及从 T 到 C 实现的任何接口。在运行时，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。
- 从 T 到 T 有效接口集中的接口类型 I，以及从 T 到 I 的任何基接口。在运行时，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。
- 从 T 到类型参数 U，前提是 T 依赖于 U（§10.1.5）。在运行时，如果 U 是值类型，则 T 和 U 必然是同一类型且不执行转换。否则，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。
- 从 null 字面量到 T，前提是已知 T 为引用类型。
- 从 T 到引用类型 S，如果它具有到引用类型 S0 的隐式转换且 S0 具有到 S 的恒等转换。在运行时，转换的执行方式与转换到 S0 相同。
- 从 T 到接口类型 I，如果它具有到接口或委托类型 I0 的隐式转换且 I0 可方差转换为 I（§13.1.3.2）。在运行时，如果 T 是值类型，则转换作为装箱转换执行。否则，转换作为隐式引用转换或恒等转换执行。

如果已知 T 为引用类型（§10.1.5），则上述转换全部归类为隐式引用转换（§6.1.6）。如果 T 未知为引用类型，则上述转换归类为装箱转换（§6.1.7）。

### 6.1.11 用户定义的隐式转换

用户定义的隐式转换由可选的标准隐式转换组成，其后执行用户定义的隐式转换运算符，其后是另一个可选的标准隐式转换。评估用户定义的隐式转换的确切规则在 §6.4.4 中描述。

### 6.1.12 匿名函数转换和方法组转换

匿名函数和方法组本身没有类型，但可以隐式转换为委托类型或表达式树类型。匿名函数转换在 §6.5 中有更详细的描述，方法组转换在 §6.6 中。

## 6.2 显式转换

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

显式转换可以出现在强制转换表达式中（§7.7.6）。

显式转换的集合包括所有隐式转换。这意味着允许冗余的强制转换表达式。

不是隐式转换的显式转换是那些无法证明总是成功、已知可能丢失信息以及跨越类型域足够不同以值得显式表示的转换。

### 6.2.1 显式数值转换

显式数值转换是从一种数值类型到另一种数值类型的转换，其中不存在隐式数值转换（§6.1.2）：

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

由于显式转换包括所有隐式和显式数值转换，因此始终可以使用强制转换表达式（§7.7.6）将任何数值类型转换为任何其他数值类型。

显式数值转换可能丢失信息或可能导致抛出异常。显式数值转换的处理如下：

- 对于从一种整型到另一种整型的转换，处理取决于转换发生的溢出检查上下文（§7.6.12）：
  - 在有检查的上下文中，如果源操作数的值在目标类型的范围内，则转换成功；但如果源操作数的值超出目标类型的范围，则抛出 System.OverflowException。
  - 在无检查的上下文中，转换总是成功，并按如下方式进行：
    - 如果源类型大于目标类型，则通过丢弃其“额外”的最高有效位来截断源值。然后将结果视为目标类型的值。
    - 如果源类型小于目标类型，则源值将被符号扩展或零扩展，使其与目标类型大小相同。如果源类型为有符号，则使用符号扩展；如果源类型为无符号，则使用零扩展。然后将结果视为目标类型的值。
    - 如果源类型与目标类型大小相同，则源值被视为目标类型的值。
- 对于从 decimal 到整型的转换，源值向零舍入到最接近的整数值，并且该整数值成为转换的结果。如果得到的整数值超出目标类型的范围，则抛出 System.OverflowException。
- 对于从 float 或 double 到整型的转换，处理取决于转换发生的溢出检查上下文（§7.6.12）中转换发生的情况：


- 在 checked 上下文中，转换按如下方式执行：
  - 如果操作数的值为 NaN 或无穷大，则引发 `System.OverflowException`。
  - 否则，将源操作数向零舍入到最接近的整数值。如果该整数值位于目标类型的范围内，则该值就是转换的结果。
  - 否则，引发 `System.OverflowException`。
- 在 unchecked 上下文中，转换始终成功，并按如下方式执行。
  - 如果操作数的值为 NaN 或无穷大，则转换结果是目标类型的未指定值。
  - 否则，将源操作数向零舍入到最接近的整数值。如果该整数值位于目标类型的范围内，则该值就是转换的结果。
  - 否则，转换结果是目标类型的未指定值。

- 对于从 `double` 到 `float` 的转换，将 `double` 值舍入到最接近的 `float` 值。如果该 `double` 值太小而无法表示为 `float`，则结果变为正零或负零。如果该 `double` 值太大而无法表示为 `float`，则结果变为正无穷大或负无穷大。如果该 `double` 值为 NaN，则结果也是 NaN。
- 对于从 `float` 或 `double` 到 `decimal` 的转换，将源值转换为 `decimal` 表示形式，并在需要时舍入到小数点后第 28 位之后最接近的数字（§4.1.7）。如果源值太小而无法表示为 `decimal`，则结果变为零。如果源值为 NaN、无穷大或太大而无法表示为 `decimal`，则引发 `System.OverflowException`。
- 对于从 `decimal` 到 `float` 或 `double` 的转换，将 `decimal` 值舍入到最接近的 `double` 或 `float` 值。虽然此转换可能会丢失精度，但它绝不会引发异常。

## 6.2.2 显式枚举转换

显式枚举转换包括：

- 从 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double` 或 `decimal` 到任何 `enum-type`。
- 从任何 `enum-type` 到 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double` 或 `decimal`。
- 从任何 `enum-type` 到任何其他 `enum-type`。

两个类型之间的显式枚举转换的处理方式是：将任何涉及的 `enum-type` 视为该 `enum-type` 的基础类型，然后在所得类型之间执行隐式或显式数值转换。例如，给定基础类型为 `int` 的 `enum-type` E，从 E 到 `byte` 的转换按从 `int` 到 `byte` 的显式数值转换（§6.2.1）处理，而从 `byte` 到 E 的转换按从 `byte` 到 `int` 的隐式数值转换（§6.1.2）处理。

## 6.2.3 显式可空转换

显式可空转换允许对非可空值类型执行的预定义显式转换也可用于这些类型的可空形式。对于从非可空值类型 S 转换为非可空值类型 T 的每个预定义显式转换（§6.1.1、§6.1.2、§6.1.3、§6.2.1 和 §6.2.2），存在以下可空转换：

- 从 S? 到 T? 的显式转换。
- 从 S 到 T? 的显式转换。

从 S? 到 T 的显式转换。

基于从 S 到 T 的基础转换来评估可空转换的过程如下：

- 如果可空转换是从 S? 到 T?：
  - 如果源值为 null（HasValue 属性为 false），则结果为 T? 类型的 null 值。
  - 否则，该转换按以下方式评估：从 S? 解包到 S，然后执行从 S 到 T 的基础转换，然后从 T 包装到 T?。
- 如果可空转换是从 S 到 T?，则该转换按从 S 到 T 的基础转换后跟从 T 包装到 T? 来评估。
- 如果可空转换是从 S? 到 T，则该转换按从 S? 解包到 S 后跟从 S 到 T 的基础转换来评估。

注意，如果可空值为 null，则尝试对该值进行解包将引发异常。

## 6.2.4 显式引用转换

显式引用转换包括：

- 从 object 和 dynamic 到任何其他引用类型。
- 从任何类类型 S 到任何类类型 T，前提是 S 是 T 的基类。
- 从任何类类型 S 到任何接口类型 T，前提是 S 未密封，并且 S 不实现 T。
- 从任何接口类型 S 到任何类类型 T，前提是 T 未密封，或者 T 实现 S。
- 从任何接口类型 S 到任何接口类型 T，前提是 S 不是从 T 派生。
- 从元素类型为 S_E 的数组类型 S 到元素类型为 T_E 的数组类型 T，前提是以下所有条件均为 true：
  - S 和 T 仅在元素类型上不同。换言之，S 和 T 具有相同的维数。
  - S_E 和 T_E 都是引用类型。
  - 存在从 S_E 到 T_E 的显式引用转换。
- 从 System.Array 及其实现的接口到任何数组类型。
- 从一维数组类型 S[] 到 System.Collections.Generic.IList<T> 及其基接口，前提是存在从 S 到 T 的显式引用转换。
- 从 System.Collections.Generic.IList<S> 及其基接口到一维数组类型 T[]，前提是存在从 S 到 T 的显式标识转换或引用转换。
- 从 System.Delegate 及其实现的接口到任何委托类型。
- 从引用类型到引用类型 T，前提是它具有到引用类型 T0 的显式引用转换，并且 T0 具有到 T 的标识转换。
- 从引用类型到接口或委托类型 T，前提是它具有到接口或委托类型 T0 的显式引用转换，并且 T0 可变性可转换为 T，或者 T 可变性可转换为 T0（§13.1.3.2）。
- 从 D<S1...Sn> 到 D<T1...Tn>，其中 D<X1...Xn> 是泛型委托类型，D<S1...Sn> 与 D<T1...Tn> 不兼容或不相同，并且对于 D 的每个类型参数 X_i，以下条件成立：
  - 如果 X_i 是不变的，则 S_i 与 T_i 相同。
  - 如果 X_i 是协变的，则存在从 S_i 到 T_i 的隐式或显式标识转换或引用转换。
  - 如果 X_i 是逆变的，则 S_i 和 T_i 要么相同，要么都是引用类型。
- 涉及已知为引用类型的类型参数的显式转换。有关涉及类型参数的显式转换的更多详细信息，请参见 §6.2.6。

显式引用转换是那些需要在运行时检查以确保正确的引用类型之间的转换。

为使显式引用转换在运行时成功，源操作数的值必须为 null，或者源操作数所引用的对象的实际类型必须是通过隐式引用转换（§6.1.6）或装箱转换（§6.1.7）可转换为目标类型的类型。如果显式引用转换失败，则引发 System.InvalidCastException。

引用转换（无论隐式还是显式）绝不会更改被转换对象的引用标识。换言之，引用转换可能会更改引用的类型，但绝不会更改被引用对象的类型或值。

## 6.2.5 拆箱转换

拆箱转换允许将引用类型显式转换为值类型。存在从类型 object、dynamic 和 System.ValueType 到任何非可空值类型的拆箱转换，以及从任何接口类型到实现该接口类型的任何非可空值类型的拆箱转换。此外，类型 System.Enum 可拆箱为任何枚举类型。

如果存在从引用类型到可空类型的基础非可空值类型的拆箱转换，则存在从该引用类型到该可空类型的拆箱转换。

如果值类型 S 具有从接口类型 I0 的拆箱转换，并且 I0 具有到 I 的标识转换，则 S 具有从接口类型 I 的拆箱转换。

如果值类型 S 具有从接口类型或委托类型 I0 的拆箱转换，并且 I0 可变性可转换为 I，或者 I 可变性可转换为 I0（§13.1.3.2），则 S 具有从接口类型 I 的拆箱转换。

拆箱操作包括：首先检查对象实例是否为给定值类型的装箱值，然后从实例中复制出该值。将 null 引用拆箱为可空类型会生成该可空类型的 null 值。结构可以从类型 System.ValueType 拆箱，因为它是所有结构的基类（§11.3.2）。

拆箱转换在 §4.3.2 中进一步描述。

## 6.2.6 显式动态转换

存在从 dynamic 类型的表达式到任何类型 T 的显式动态转换。该转换是动态绑定的（§7.2.2），这意味着将在运行时从该表达式的运行时类型到 T 查找显式转换。如果找不到转换，则引发运行时异常。

如果不希望对该转换进行动态绑定，可以先将表达式转换为 object，然后再转换为所需类型。

假设定义了以下类：

```
class C
{
    int i;
    public C(int i) { this.i = i; }
}
```




```csharp
public static explicit operator C(string s)
{
    return new C(int.Parse(s));
}
```

以下示例说明了显式动态转换：

```csharp
object o = "1";
dynamic d = "2";
var c1 = (C)o; // Compiles, but explicit reference conversion fails
var c2 = (C)d; // Compiles and user defined conversion succeeds
```

o 到 C 的最佳转换在编译时被确定为显式引用转换。这在运行时会失败，因为“1”实际上并不是一个 C。而 d 到 C 的转换则作为显式动态转换被推迟到运行时，在运行时会找到从 d 的运行时类型——string——到 C 的用户定义转换，并且转换成功。

### 6.2.7 Explicit conversions involving type parameters

对于给定的类型参数 T，存在以下显式转换：

- 从 T 的有效基类 C 到 T，以及从 C 的任意基类到 T。在运行时，如果 T 是值类型，则转换作为拆箱转换执行。否则，转换作为显式引用转换或恒等转换执行。
- 从任意接口类型到 T。在运行时，如果 T 是值类型，则转换作为拆箱转换执行。否则，转换作为显式引用转换或恒等转换执行。
- 从 T 到任意接口类型 I，前提是 T 到 I 不已存在隐式转换。在运行时，如果 T 是值类型，则转换作为装箱转换后跟显式引用转换执行。否则，转换作为显式引用转换或恒等转换执行。
- 从类型参数 U 到 T，前提是 T 依赖于 U (§10.1.5)。在运行时，如果 U 是值类型，则 T 和 U 必然是同一类型且不执行转换。否则，如果 T 是值类型，则转换作为拆箱转换执行。否则，转换作为显式引用转换或恒等转换执行。

如果已知 T 是引用类型，则上述转换全部归类为显式引用转换 (§6.2.4)。如果 T 未知是否引用类型，则上述转换归类为拆箱转换 (§6.2.5)。

上述规则不允许从无约束的类型参数到非接口类型的直接显式转换，这可能令人惊讶。该规则的原因是为了防止混淆并使此类转换的语义清晰。例如，考虑以下声明：

```csharp
class X<T>
{
    public static long F(T t) {
        return (long)t;            // Error
    }
}
```

如果允许 t 到 int 的直接显式转换，人们很容易期望 X<int>.F(7) 会返回 7L。然而事实并非如此，因为标准数值转换仅在绑定时已知类型为数值时才会被考虑。为了使语义清晰，上述示例必须改写为：

```csharp
class X<T>
{
    public static long F(T t) {
        return (long)(object)t;  // Ok, but will only work when T is long
    }
}
```

此代码现在可以编译，但执行 X<int>.F(7) 时仍会在运行时抛出异常，因为装箱的 int 不能直接转换为 long。

### 6.2.8 User-defined explicit conversions

用户定义的显式转换由可选的标准显式转换组成，其后执行用户定义的隐式或显式转换运算符，再后跟另一个可选的标准显式转换。评估用户定义显式转换的确切规则在 §6.4.5 中描述。

## 6.3 Standard conversions

标准转换是指可在用户定义转换的一部分中发生的预定义转换。

### 6.3.1 Standard implicit conversions

以下隐式转换被归类为标准隐式转换：

- Identity conversions (§6.1.1)
- Implicit numeric conversions (§6.1.2)
- Implicit nullable conversions (§6.1.4)
- Implicit reference conversions (§6.1.6)
- Boxing conversions (§6.1.7)
- Implicit constant expression conversions (§6.1.8)
- Implicit conversions involving type parameters (§6.1.10)

标准隐式转换明确排除用户定义的隐式转换。

### 6.3.2 Standard explicit conversions

标准显式转换包括所有标准隐式转换，外加存在相反标准隐式转换的显式转换的子集。换句话说，如果从类型 A 到类型 B 存在标准隐式转换，则从类型 A 到类型 B 以及从类型 B 到类型 A 都存在标准显式转换。

## 6.4 User-defined conversions

C# 允许通过用户定义转换来扩展预定义的隐式和显式转换。用户定义转换通过在类和结构类型中声明转换运算符 (§10.10.3) 来引入。

### 6.4.1 Permitted user-defined conversions

C# 仅允许声明某些用户定义转换。特别是，不可能重新定义已存在的隐式或显式转换。

对于给定的源类型 S 和目标类型 T，如果 S 或 T 是可空类型，则令 S₀ 和 T₀ 指代其底层类型，否则 S₀ 和 T₀ 分别等于 S 和 T。类或结构仅在满足以下所有条件时才允许声明从源类型 S 到目标类型 T 的转换：

- S₀ 和 T₀ 是不同的类型。
- S₀ 或 T₀ 是运算符声明所在的类或结构类型。
- S₀ 和 T₀ 都不是 *interface-type*。
- 排除用户定义转换后，从 S 到 T 或从 T 到 S 不存在转换。

适用于用户定义转换的限制在 §10.10.3 中进一步讨论。

### 6.4.2 Lifted conversion operators

给定一个将非可空值类型 S 转换为非可空值类型 T 的用户定义转换运算符，则存在一个 **lifted conversion operator** 将 S? 转换为 T?。此提升的转换运算符执行从 S? 到 S 的解包，然后执行从 S 到 T 的用户定义转换，然后执行从 T 到 T? 的包装，除了 null 值的 S? 直接转换为 null 值的 T?。

提升的转换运算符具有与其底层用户定义转换运算符相同的隐式或显式分类。术语“用户定义转换”适用于用户定义和提升的转换运算符的使用。

### 6.4.3 Evaluation of user-defined conversions

用户定义转换将值从其类型，即 *source type*，转换为另一个类型，即 *target type*。用户定义转换的评估集中于为特定源类型和目标类型找到 *most specific* 的用户定义转换运算符。此确定分为几个步骤：

- 确定将考虑用户定义转换运算符的类和结构集合。该集合由源类型及其基类以及目标类型及其基类组成（隐含假设只有类和结构可以声明用户定义运算符，且非类类型没有基类）。为此步骤的目的，如果源类型或目标类型是 *nullable-type*，则改用其底层类型。
- 从该类型集合中，确定哪些用户定义和提升的转换运算符适用。对于转换运算符要适用，必须能够从源类型到运算符的操作数类型执行标准转换 (§6.3)，并且必须能够从运算符的结果类型到目标类型执行标准转换。
- 从适用的用户定义运算符集合中，确定哪个运算符无歧义地是最具体的。总体而言，最具体的运算符是其操作数类型“最接近”源类型且其结果类型“最接近”目标类型的运算符。用户定义转换运算符优先于提升的转换运算符。确定最具体的用户定义转换运算符的确切规则在以下各节中定义。

一旦确定了最具体的用户定义转换运算符，用户定义转换的实际执行涉及最多三个步骤：

- 首先，如有需要，从源类型到用户定义或提升的转换运算符的操作数类型执行标准转换。
- 其次，调用用户定义或提升的转换运算符执行转换。
- 最后，如有需要，从用户定义或提升的转换运算符的结果类型到目标类型执行标准转换。

用户定义转换的评估永远不会涉及多于一个用户定义或提升的转换运算符。换句话说，从类型 S 到类型 T 的转换永远不会先执行从 S 到 X 的用户定义转换，然后再执行从 X 到 T 的用户定义转换。

用户定义隐式或显式转换评估的确切定义在以下各节中给出。定义使用了以下术语：

- 如果存在从类型 A 到类型 B 的标准隐式转换（§6.3.1），且 A 和 B 都不是*接口类型*，则称 A *被 B 包容*，且称 B *包容* A。
- 一组类型中的*最具包容性的类型*是能包容该组中所有其他类型的那个类型。如果没有任何一个类型能包容所有其他类型，则该组没有最具包容性的类型。更直观地说，最具包容性的类型就是该组中“最大”的类型——其他每个类型都能隐式转换到的那个类型。
- 一组类型中的*最被包容的类型*是被该组中所有其他类型所包容的那个类型。如果没有任何一个类型被所有其他类型包容，则该组没有最被包容的类型。更直观地说，最被包容的类型就是该组中“最小”的类型——可以隐式转换为每个其他类型的那个类型。

### 6.4.4 用户定义的隐式转换

从类型 S 到类型 T 的用户定义隐式转换按以下步骤处理：

- 确定类型 S₀ 和 T₀。如果 S 或 T 是可空类型，则 S₀ 和 T₀ 是它们的基础类型；否则 S₀ 和 T₀ 分别等于 S 和 T。
- 查找将考虑用户定义转换运算符的类型集合 D。该集合由 S₀（如果 S₀ 是类或结构）、S₀ 的基类（如果 S₀ 是类）以及 T₀（如果 T₀ 是类或结构）组成。
- 查找适用的用户定义转换运算符和提升的转换运算符的集合 U。该集合由 D 中的类或结构声明的、可以执行从包容 S 的类型到被 T 包容的类型转换的用户定义和提升的隐式转换运算符组成。如果 U 为空，则转换未定义，并发生编译时错误。
- 查找 U 中运算符的最具体的源类型 Sₓ：
  - 如果 U 中有任何运算符从 S 转换，则 Sₓ 为 S。
  - 否则，Sₓ 是 U 中运算符的源类型组合集合中最被包容的类型。如果无法找到唯一一个最被包容的类型，则转换存在歧义，并发生编译时错误。
- 查找 U 中运算符的最具体的目标类型 Tₓ：
  - 如果 U 中有任何运算符转换为 T，则 Tₓ 为 T。
  - 否则，Tₓ 是 U 中运算符的目标类型组合集合中最具包容性的类型。如果无法找到唯一一个最具包容性的类型，则转换存在歧义，并发生编译时错误。
- 查找最具体的转换运算符：
  - 如果 U 中正好包含一个将 Sₓ 转换为 Tₓ 的用户定义转换运算符，则它就是最具体的转换运算符。
  - 否则，如果 U 中正好包含一个将 Sₓ 转换为 Tₓ 的提升的转换运算符，则它就是最具体的转换运算符。
  - 否则，转换存在歧义，并发生编译时错误。
- 最后，应用该转换：
  - 如果 S 不是 Sₓ，则执行从 S 到 Sₓ 的标准隐式转换。
  - 调用最具体的转换运算符将 Sₓ 转换为 Tₓ。
  - 如果 Tₓ 不是 T，则执行从 Tₓ 到 T 的标准隐式转换。

### 6.4.5 用户定义的显式转换

从类型 S 到类型 T 的用户定义显式转换按以下步骤处理：

- 确定类型 S₀ 和 T₀。如果 S 或 T 是可空类型，则 S₀ 和 T₀ 是它们的基础类型；否则 S₀ 和 T₀ 分别等于 S 和 T。
- 查找将考虑用户定义转换运算符的类型集合 D。该集合由 S₀（如果 S₀ 是类或结构）、S₀ 的基类（如果 S₀ 是类）、T₀（如果 T₀ 是类或结构）以及 T₀ 的基类（如果 T₀ 是类）组成。
- 查找适用的用户定义转换运算符和提升的转换运算符的集合 U。该集合由 D 中的类或结构声明的、可以执行从包容 S 或被 S 包容的类型到被 T 包容或包容 T 的类型转换的用户定义和提升的隐式或显式转换运算符组成。如果 U 为空，则转换未定义，并发生编译时错误。
- 查找 U 中运算符的最具体的源类型 Sₓ：
  - 如果 U 中有任何运算符从 S 转换，则 Sₓ 为 S。
  - 否则，如果 U 中有任何运算符从包容 S 的类型转换，则 Sₓ 是这些运算符的源类型组合集合中最被包容的类型。如果无法找到最被包容的类型，则转换存在歧义，并发生编译时错误。
  - 否则，Sₓ 是 U 中运算符的源类型组合集合中最具包容性的类型。如果无法找到唯一一个最具包容性的类型，则转换存在歧义，并发生编译时错误。
- 查找 U 中运算符的最具体的目标类型 Tₓ：
  - 如果 U 中有任何运算符转换为 T，则 Tₓ 为 T。
  - 否则，如果 U 中有任何运算符转换为被 T 包容的类型，则 Tₓ 是这些运算符的目标类型组合集合中最具包容性的类型。如果无法找到唯一一个最具包容性的类型，则转换存在歧义，并发生编译时错误。
  - 否则，Tₓ 是 U 中运算符的目标类型组合集合中最被包容的类型。如果无法找到最被包容的类型，则转换存在歧义，并发生编译时错误。
- 查找最具体的转换运算符：
  - 如果 U 中正好包含一个将 Sₓ 转换为 Tₓ 的用户定义转换运算符，则它就是最具体的转换运算符。
  - 否则，如果 U 中正好包含一个将 Sₓ 转换为 Tₓ 的提升的转换运算符，则它就是最具体的转换运算符。
  - 否则，转换存在歧义，并发生编译时错误。
- 最后，应用该转换：
  - 如果 S 不是 Sₓ，则执行从 S 到 Sₓ 的标准显式转换。
  - 调用最具体的用户定义转换运算符将 Sₓ 转换为 Tₓ。
  - 如果 Tₓ 不是 T，则执行从 Tₓ 到 T 的标准显式转换。

## 6.5 匿名函数转换

匿名方法表达式或 lambda 表达式被归类为匿名函数（§7.15）。该表达式没有类型，但可以隐式转换为兼容的委托类型或表达式树类型。具体来说，如果满足以下条件，委托类型 D 与匿名函数 F 兼容：

- 如果 F 包含匿名函数签名，则 D 和 F 具有相同数量的参数。
- 如果 F 不包含匿名函数签名，则 D 可以具有零个或多个任意类型的参数，只要 D 的任何参数都不带 out 参数修饰符。
- 如果 F 具有显式类型的参数列表，则 D 中的每个参数与 F 中对应参数具有相同的类型和修饰符。
- 如果 F 具有隐式类型的参数列表，则 D 不能有 ref 或 out 参数。
- 如果 D 具有 void 返回类型且 F 的主体是表达式，则当 F 的每个参数都被赋予 D 中对应参数的类型时，F 的主体是有效表达式（根据 §7），并且允许作为语句表达式（§8.6）使用。
- 如果 D 具有 void 返回类型且 F 的主体是语句块，则当 F 的每个参数都被赋予 D 中对应参数的类型时，F 的主体是有效语句块（根据 §8.2），其中没有 return 语句指定表达式。
- 如果 D 具有非 void 返回类型且 F 的主体是表达式，则当 F 的每个参数都被赋予 D 中对应参数的类型时，F 的主体是有效表达式（根据 §7），并且可隐式转换为 D 的返回类型。
- 如果 D 具有非 void 返回类型且 F 的主体是语句块，则当 F 的每个参数都被赋予 D 中对应参数的类型时，F 的主体是有效语句块（根据 §8.2），其结束点不可到达，并且每个 return 语句都指定一个可隐式转换为 D 的返回类型的表达式。

如果委托类型 D 与 F 兼容，则表达式树类型 Expression<D> 与匿名函数 F 兼容。

某些匿名函数无法转换为表达式树类型：即使转换存在，也会在编译时失败。如果匿名表达式包含以下一种或多种构造，则属于这种情况：

- 简单赋值运算符或复合赋值运算符
- 动态绑定表达式

下面的示例使用泛型委托类型 Func<A,R>，它表示一个接受类型为 A 的参数并返回类型为 R 的值的函数：

```
delegate R Func<A,R>(A arg);
```

在以下赋值中

```
Func<int,int> f1 = x => x + 1;    // ok
Func<int,double> f2 = x => x + 1;    // ok
Func<double,int> f3 = x => x + 1;    // Error
```

每个匿名函数的参数类型和返回类型由该匿名函数所赋给的变量的类型决定。

第一个赋值成功地将匿名函数转换为委托类型 Func<int,int>，因为当 x 被赋予类型 int 时，x + 1 是有效的表达式，并且可以隐式转换为类型 int。



同样，第二个赋值成功地将匿名函数转换为委托类型 Func<int,double>，因为 x + 1 的结果（类型为 int）可隐式转换为类型 double。

然而，第三个赋值是编译时错误，因为当 x 被赋予类型 double 时，x + 1 的结果（类型为 double）不能隐式转换为类型 int。

匿名函数可能影响重载决策，并参与类型推断。有关更多详细信息，请参见 §7.5。

## 6.5.1 匿名函数到委托类型转换的求值

将匿名函数转换为委托类型会生成一个委托实例，该实例引用匿名函数以及在求值时处于活动状态的（可能为空的）捕获外部变量集合。调用委托时，将执行匿名函数的主体。主体中的代码使用该委托所引用的捕获外部变量集合来执行。

由匿名函数生成的委托的调用列表包含单个条目。委托的确切目标对象和目标方法未指定。特别地，未指定委托的目标对象是 null、外围函数成员的 this 值，还是某个其他对象。

对于具有相同（可能为空的）捕获外部变量实例集合且语义相同的匿名函数，允许（但不要求）其到相同委托类型的转换返回同一个委托实例。此处术语“语义相同”用于表示：在给定相同参数的所有情况下，匿名函数的执行将产生相同的效果。此规则允许优化如下代码。

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

由于这两个匿名函数委托具有相同（空）的捕获外部变量集合，并且由于这些匿名函数语义相同，因此允许编译器让这些委托引用同一个目标方法。实际上，允许编译器从两个匿名函数表达式返回完全相同的委托实例。

## 6.5.2 匿名函数到表达式树类型转换的求值

将匿名函数转换为表达式树类型会生成表达式树（§4.6）。更准确地说，匿名函数转换的求值会导致构造一个表示匿名函数本身结构的对象结构。表达式树的精确结构以及创建它的确切过程由实现定义。

## 6.5.3 实现示例

本节描述一种基于其他 C# 构造的匿名函数转换的可能实现。这里描述的实现基于 Microsoft C# 编译器所使用的相同原则，但它绝不是强制实现，也不是唯一可能的实现。它仅简要提及到表达式树的转换，因为其确切语义超出本规范的范围。

本节其余部分给出几个包含具有不同特征的匿名函数的代码示例。对于每个示例，提供了仅使用其他 C# 构造的相应转换代码。在这些示例中，假定标识符 D 表示以下委托类型：

```
public delegate void D();
```

匿名函数的最简单形式是不捕获任何外部变量的形式：

```csharp
class Test
{
    static void F() {
        D d = () => { Console.WriteLine("test"); };
    }
}
```

这可以转换为一个委托实例化，该实例化引用一个编译器生成的静态方法，匿名函数的代码放置在该方法中：

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

在以下示例中，匿名函数引用 this 的实例成员：

```csharp
class Test
{
    int x;
    void F() {
        D d = () => { Console.WriteLine(x); };
    }
}
```

这可以转换为一个包含匿名函数代码的编译器生成的实例方法：

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

在此示例中，匿名函数捕获局部变量：

```csharp
class Test
{
    void F() {
        int y = 123;
        D d = () => { Console.WriteLine(y); };
    }
}
```

现在必须将局部变量的生存期至少延长到匿名函数委托的生存期。这可以通过将局部变量“提升”到编译器生成的类的字段中来实现。随后，局部变量的实例化（§7.15.5.2）对应于创建编译器生成的类的实例，而访问局部变量对应于访问编译器生成的类实例中的字段。此外，匿名函数成为编译器生成的类的实例方法：

```
class Test
{
    void F() {
        __Locals1 __locals1 = new __Locals1();
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

最后，以下匿名函数捕获 this 以及两个具有不同生存期的局部变量：

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

这里，为捕获局部变量的每个语句块创建一个编译器生成的类，使得不同块中的局部变量可以具有独立的生存期。__Locals2 是内部语句块的编译器生成类，其实例包含局部变量 z 和一个引用 __Locals1 实例的字段。__Locals1 是外部语句块的编译器生成类，其实例包含局部变量 y 和一个引用外围函数成员的 this 的字段。借助这些数据结构，可以通过 __Locals2 的实例访问所有捕获的外部变量，因此匿名函数的代码可以实现为该类的实例方法。

```
class Test
{
    void F() {
        __Locals1 __locals1 = new __Locals1();
        __locals1.__this = this;
        __locals1.y = 123;
        for (int i = 0; i < 10; i++) {
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
}
```

```
class __Locals2
{
    public __Locals1 __locals1;
    public int z;
    public void __Method1() {
        Console.WriteLine(__locals1.__this.x + __locals1.y + z);
    }
}
```

这里用于捕获局部变量的相同技术也可用于将匿名函数转换为表达式树：对编译器生成的对象的引用可以存储在表达式树中，而对局部变量的访问可以表示为对这些对象的字段访问。此方法的优点是允许“提升”的局部变量在委托和表达式树之间共享。

## 6.6 方法组转换

存在从方法组（§7.1）到兼容委托类型的隐式转换（§6.1）。给定委托类型 D 和被归类为方法组的表达式 E，如果 E 包含至少一个方法，该方法在其正常形式（§7.5.3.1）下适用于通过使用 D 的参数类型和修饰符构造的参数列表，则存在从 E 到 D 的隐式转换，如下所述。

以下描述从方法组 E 到委托类型 D 的转换的编译时应用。注意，从 E 到 D 的隐式转换的存在并不保证该转换的编译时应用会在没有错误的情况下成功。

- 选择单个方法 M，对应于形式为 E(A) 的方法调用（§7.6.5.1），并进行以下修改：
  - 参数列表 A 是表达式列表，每个表达式被归类为变量，并具有 D 的形参列表中对应参数的类型和修饰符（ref 或 out）。
  - 考虑的方法仅为那些在其正常形式（§7.5.3.1）下适用的方法，而不是仅在展开形式下适用的方法。
- 如果 §7.6.5.1 的算法产生错误，则发生编译时错误。否则，该算法产生一个具有与 D 相同参数数量的单个最佳方法 M，并认为转换存在。
- 所选方法 M 必须与委托类型 D 兼容（§15.2），否则发生编译时错误。
- 如果所选方法 M 是实例方法，则与 E 关联的实例表达式确定委托的目标对象。
- 如果所选方法 M 是通过实例表达式上的成员访问表示的扩展方法，则该实例表达式确定委托的目标对象。
- 转换的结果是类型 D 的值，即一个新创建的委托，它引用所选方法和目标对象。

注意，如果 §7.6.5.1 的算法未能找到实例方法，但成功地将 E(A) 的调用作为扩展方法调用（§7.6.5.2）处理，则此过程可能导致创建指向扩展方法的委托。这样创建的委托会捕获该扩展方法及其第一个参数。

以下示例演示方法组转换：

```
delegate string D1(object o);
delegate object D2(string s);
```



```csharp
delegate object D3();
delegate string D4(object o, params object[] a);
delegate string D5(int i);
class Test
{
    static string F(object o) {...}
    static void G() {
        D1 d1 = F;    // Ok
        D2 d2 = F;    // Ok
        D3 d3 = F;    // Error - not applicable
        D4 d4 = F;    // Error - not applicable in normal form
        D5 d5 = F;    // Error - applicable but not compatible
    }
}
```

对 d1 的赋值会隐式地将方法组 F 转换为类型为 D1 的值。

对 d2 的赋值展示了如何创建一个指向具有更少派生（逆变）参数类型和更派生（协变）返回类型的方法的委托。

对 d3 的赋值展示了如果方法不适用则不存在转换的情况。

对 d4 的赋值展示了方法必须在其常规形式下适用。

对 d5 的赋值展示了委托和方法参数类型与返回类型仅允许在引用类型时不同。

与所有其他隐式和显式转换一样，转换运算符可用于显式执行方法组转换。因此，示例

```csharp
object obj = new EventHandler(myDialog.OkClick);
```

可以改写为

```csharp
object obj = (EventHandler)myDialog.OkClick;
```

方法组可能会影响重载解析，并参与类型推断。请参阅 §7.5 了解更多详细信息。

方法组转换的运行时求值按以下步骤进行：

- 如果在编译时选择的方法是实例方法，或是作为实例方法访问的扩展方法，则委托的目标对象由与 E 关联的实例表达式确定：
  - 实例表达式会被求值。如果此求值导致异常，则不再执行后续步骤。
  - 如果实例表达式为引用类型，则实例表达式计算得到的值成为目标对象。如果所选方法为实例方法且目标对象为 null，则会抛出 System.NullReferenceException 且不再执行后续步骤。
  - 如果实例表达式为值类型，则会执行装箱操作（§4.3.1）将值转换为对象，且该对象成为目标对象。
- 否则，所选方法为静态方法调用的一部分，委托的目标对象为 null。
- 分配委托类型 D 的新实例。如果没有足够的内存分配新实例，则会抛出 System.OutOfMemoryException 且不再执行后续步骤。
- 新的委托实例使用在编译时确定的方法的引用以及上面计算得到的目标对象的引用进行初始化。

## 7. 表达式

表达式是一系列运算符和操作数。本章定义了表达式的语法、操作数和运算符的求值顺序以及表达式的含义。

### 7.1 表达式分类

表达式被归类为以下之一：

- 值。每个值都有一个关联的类型。
- 变量。每个变量都有一个关联的类型，即变量的声明类型。
- 命名空间。此分类的表达式只能作为成员访问（§7.6.4）的左侧出现。在任何其他上下文中，被归类为命名空间的表达式会导致编译时错误。
- 类型。此分类的表达式只能作为成员访问（§7.6.4）的左侧出现，或作为 as 运算符（§7.10.11）、is 运算符（§7.10.10）或 typeof 运算符（§7.6.11）的操作数。在任何其他上下文中，被归类为类型的表达式会导致编译时错误。
- 方法组，即成员查找（§7.4）得到的一组重载方法。方法组可能具有关联的实例表达式和关联的类型参数列表。当实例方法被调用时，求值实例表达式的结果成为由 this 表示的实例（§7.6.7）。方法组允许出现在调用表达式（§7.6.5）、委托创建表达式（§7.6.10.5）以及 is 运算符的左侧，并可隐式转换为兼容的委托类型（§6.6）。在任何其他上下文中，被归类为方法组的表达式会导致编译时错误。
- null 字面量。此分类的表达式可以隐式转换为引用类型或可空类型。
- 匿名函数。此分类的表达式可以隐式转换为兼容的委托类型或表达式树类型。
- 属性访问。每个属性访问都有一个关联的类型，即属性的类型。此外，属性访问可能具有关联的实例表达式。当实例属性访问的访问器（get 或 set 块）被调用时，求值实例表达式的结果成为由 this 表示的实例（§7.6.7）。
- 事件访问。每个事件访问都有一个关联的类型，即事件的类型。此外，事件访问可能具有关联的实例表达式。事件访问可作为 += 和 -= 运算符（§7.17.3）的左侧操作数出现。在任何其他上下文中，被归类为事件访问的表达式会导致编译时错误。
- 索引器访问。每个索引器访问都有一个关联的类型，即索引器的元素类型。此外，索引器访问具有关联的实例表达式和关联的参数列表。当索引器访问的访问器（get 或 set 块）被调用时，求值实例表达式的结果成为由 this 表示的实例（§7.6.7），而求值参数列表的结果成为调用的参数列表。
- 无值。这发生在表达式是对返回类型为 void 的方法调用时。被归类为无值的表达式仅在语句表达式（§8.6）的上下文中有效。

表达式的最终结果永远不是命名空间、类型、方法组或事件访问。相反，如上所述，这些类别的表达式是仅允许在特定上下文中出现的中间构造。

属性访问或索引器访问始终通过调用 get 访问器或 set 访问器重新分类为值。具体的访问器由属性或索引器访问的上下文决定：如果访问是赋值的目标，则调用 set 访问器以分配新值（§7.17.1）。否则，调用 get 访问器以获取当前值（§7.1.1）。

#### 7.1.1 表达式的值

涉及表达式的大多数构造最终要求表达式表示一个值。在这种情况下，如果实际表达式表示命名空间、类型、方法组或无值，则会发生编译时错误。然而，如果表达式表示属性访问、索引器访问或变量，则会隐式替换属性、索引器或变量的值：

- 变量的值就是变量所标识的存储位置中当前存储的值。在获取变量的值之前，变量必须被认为已明确赋值（§5.3），否则会发生编译时错误。
- 属性访问表达式的值通过调用属性的 get 访问器获得。如果属性没有 get 访问器，则会发生编译时错误。否则，执行函数成员调用（§7.5.4），调用的结果成为属性访问表达式的值。
- 索引器访问表达式的值通过调用索引器的 get 访问器获得。如果索引器没有 get 访问器，则会发生编译时错误。否则，使用与索引器访问表达式关联的参数列表执行函数成员调用（§7.5.4），调用的结果成为索引器访问表达式的值。

### 7.2 静态与动态绑定

确定操作含义（基于构成表达式的类型或值（参数、操作数、接收者））的过程通常称为绑定。例如，方法调用的含义基于接收者和参数的类型确定。运算符的含义基于其操作数的类型确定。

在 C# 中，操作的含义通常在编译时确定，基于其构成表达式的编译时类型。同样，如果表达式包含错误，错误会被编译器检测并报告。这种方法称为静态绑定。

然而，如果表达式是动态表达式（即类型为 dynamic），则表示其参与的任何绑定都应基于其运行时类型（即运行时表示的对象的实际类型），而不是编译时的类型。因此，此类操作的绑定被推迟到程序运行期间操作执行时才进行。这称为动态绑定。

当操作被动态绑定时，编译器几乎不进行检查。相反，如果运行时绑定失败，错误会作为异常在运行时报告。

以下 C# 操作受绑定影响：

- 成员访问：e.M
- 方法调用：e.M(e1,...,en)
- 委托调用：e(e1,...,en)
- 元素访问：e[e1,...,en]
- 对象创建：new C(e1,...,en)



- 重载的一元运算符：+, -, !, ~, ++, --, true, false
- 重载的二元运算符：+, -, *, /, %, &, &&, |, ||, ??, ^, <<, >>, ==, !=, >, <, >=, <=
- 赋值运算符：+=, -=, *=, /=, %=, &=, |=, ^=, <<=, >>=
- 隐式和显式转换

当不涉及动态表达式时，C# 默认采用静态绑定，这意味着在选择过程中使用构成表达式的编译时类型。但是，当上面列出的操作中的某个构成表达式是动态表达式时，该操作将改为动态绑定。

## 7.2.1 绑定时间

静态绑定在编译时进行，而动态绑定在运行时进行。在以下各节中，术语“绑定时间”指编译时或运行时，具体取决于绑定发生的时间。

以下示例说明了静态绑定和动态绑定以及绑定时间的概念：

```
object o = 5;
dynamic d = 5;
Console.WriteLine(5); // static binding to Console.WriteLine(int)
Console.WriteLine(o); // static binding to Console.WriteLine(object)
Console.WriteLine(d); // dynamic binding to Console.WriteLine(int)
```

前两个调用是静态绑定的：Console.WriteLine 的重载是根据其参数的编译时类型选择的。因此，绑定时间是编译时。

第三个调用是动态绑定的：Console.WriteLine 的重载是根据其参数的运行时类型选择的。这是因为该参数是动态表达式——其编译时类型为 dynamic。因此，第三个调用的绑定时间是运行时。

## 7.2.2 动态绑定

动态绑定的目的是允许 C# 程序与动态对象交互，即不遵循 C# 类型系统常规规则的对象。动态对象可能是来自具有不同类型系统的其他编程语言的对象，也可能是通过编程方式设置以便为不同操作实现其自身绑定语义的对象。

动态对象实现其自身语义的机制由实现定义。动态对象实现某个给定接口——同样由实现定义——以向 C# 运行时发出信号，表明它们具有特殊语义。因此，每当对动态对象的操作进行动态绑定时，将采用它们自己的绑定语义，而不是本文档中规定的 C# 绑定语义。

尽管动态绑定的目的是允许与动态对象进行互操作，但 C# 允许对所有对象进行动态绑定，无论它们是否为动态对象。这可以实现动态对象更顺畅的集成，因为对动态对象进行操作的结果本身可能不是动态对象，但其类型在编译时对程序员而言仍然未知。此外，即使所涉及的对象都不是动态对象，动态绑定也有助于消除容易出错的基于反射的代码。

以下各节描述语言中每种构造究竟在何时应用动态绑定、应用何种编译时检查（如果有），以及编译时结果和表达式分类是什么。

## 7.2.3 构成表达式的类型

当操作是静态绑定时，构成表达式（例如接收方、实参、索引或操作数）的类型始终被视为该表达式的编译时类型。

当操作是动态绑定时，构成表达式的类型根据该构成表达式的编译时类型以不同方式确定：

- 编译时类型为 dynamic 的构成表达式被视为具有该表达式在运行时求值所得实际值的类型
- 编译时类型为类型参数的构成表达式被视为具有该类型参数在运行时绑定到的类型
- 否则，该构成表达式被视为具有其编译时类型。

## 7.3 运算符

表达式由操作数和运算符构成。表达式的运算符指示要对操作数应用哪些操作。运算符的示例包括 +、-、*、/ 和 new。操作数的示例包括字面量、字段、局部变量和表达式。

运算符分为三种：

- 一元运算符。一元运算符接受一个操作数，并使用前缀表示法（如 ~x）或后缀表示法（如 x++）。
- 二元运算符。二元运算符接受两个操作数，并且全部使用中缀表示法（如 x + y）。
- 三元运算符。仅存在一个三元运算符 ?:；它接受三个操作数并使用中缀表示法（c? x : y）。

表达式中运算符的求值顺序由运算符的优先级和结合性确定（§7.3.1）。

表达式中的操作数从左到右求值。例如，在 F(i) + G(i++) * H(i) 中，方法 F 使用 i 的旧值被调用，然后方法 G 使用 i 的旧值被调用，最后方法 H 使用 i 的新值被调用。这与运算符优先级是分开的，且不相关。

某些运算符可以重载。运算符重载允许为一个或两个操作数属于用户定义的类或结构体类型的操作指定用户定义的运算符实现（§7.3.2）。

## 7.3.1 运算符优先级和结合性

当表达式包含多个运算符时，运算符的优先级控制各个运算符的求值顺序。例如，表达式 x + y * z 按 x + (y * z) 求值，因为 * 运算符的优先级高于二元 + 运算符。运算符的优先级由其关联的语法产生式的定义确立。例如，加法表达式由一系列由 + 或 - 运算符分隔的乘法表达式组成，因此 + 和 - 运算符的优先级低于 *、/ 和 % 运算符。

下表按优先级从高到低汇总所有运算符：

| 节 | 类别 | 运算符 |
|---|---|---|
| 7.6 | 主要 | x.y f(x) a[x] x++ x-- new typeof default checked unchecked delegate |
| 7.7 | 一元 | + - ! ~ ++x --x (T)x |
| 7.8 | 乘法 | * / % |
| 7.8 | 加法 | + - |
| 7.9 | 移位 | << >> |
| 7.10 | 关系和类型测试 | < > <= >= is as |
| 7.10 | 相等 | == != |
| 7.11 | 逻辑 AND | & |
| 7.11 | 逻辑 XOR | ^ |
| 7.11 | 逻辑 OR | | |
| 7.12 | 条件 AND | && |
| 7.12 | 条件 OR | || |
| 7.13 | null 合并 | ?? |
| 7.14 | 条件 | ?: |
| 7.17, 7.15 | 赋值和 lambda 表达式 | = *= /= %= += -= <<= >>= &= ^= |= => |

当一个操作数出现在两个优先级相同的运算符之间时，运算符的结合性控制操作的执行顺序：

- 除赋值运算符外，所有二元运算符都是左结合的，这意味着操作从左到右执行。例如，x + y + z 按 (x + y) + z 求值。
- 赋值运算符和条件运算符（?:）是右结合的，这意味着操作从右到左执行。例如，x = y = z 按 x = (y = z) 求值。

可以使用括号控制优先级和结合性。例如，x + y * z 先将 y 乘以 z，然后将结果加到 x，而 (x + y) * z 先将 x 和 y 相加，然后将结果乘以 z。

## 7.3.2 运算符重载

所有一元和二元运算符都有预定义实现，这些实现可在任何表达式中自动使用。除预定义实现外，还可以通过在类和结构体中包含运算符声明来引入用户定义的实现（§10.10）。用户定义的运算符实现始终优先于预定义运算符实现：仅当不存在适用的用户定义运算符实现时，才会考虑预定义运算符实现，如 §7.3.3 和 §7.3.4 所述。

可重载的一元运算符包括：
- !
- ~
- ++
- --
- true
- false

尽管 true 和 false 未在表达式中显式使用（因此未包含在 §7.3.1 的优先级表中），但它们被视为运算符，因为它们会在若干表达式中被调用。



-   X 为操作 operator op(x) 提供的候选用户定义运算符集合是根据 §7.3.5 的规则确定的。

-   如果候选用户定义运算符集合非空，则它成为该操作的候选运算符集合。否则，预定义的一元运算符 op 实现（包括其提升形式）成为该操作的候选运算符集合。给定运算符的预定义实现在运算符的描述中指定（§7.6 和 §7.7）。

-   §7.5.3 的重载解析规则应用于候选运算符集合，以相对于参数列表 (x) 选择最佳运算符，并且该运算符成为重载解析过程的结果。如果重载解析无法选择单一的最佳运算符，则会发生绑定时错误。

## 7.3.4 二元运算符重载解析

形式为 x op y 的操作，其中 op 是可重载的二元运算符，x 是类型为 X 的表达式，y 是类型为 Y 的表达式，按如下方式处理：

-   确定 X 和 Y 为操作 operator op(x, y) 提供的候选用户定义运算符集合。该集合由 X 提供的候选运算符与 Y 提供的候选运算符的并集组成，各自均使用 §7.3.5 的规则确定。如果 X 和 Y 是同一类型，或者 X 和 Y 派生自共同的基类型，则共享的候选运算符在合并集合中只出现一次。

-   如果候选用户定义运算符集合非空，则它成为该操作的候选运算符集合。否则，预定义的二元运算符 op 实现（包括其提升形式）成为该操作的候选运算符集合。给定运算符的预定义实现在运算符的描述中指定（§7.8 至 §7.12）。

-   §7.5.3 的重载解析规则应用于候选运算符集合，以相对于参数列表 (x, y) 选择最佳运算符，并且该运算符成为重载解析过程的结果。如果重载解析无法选择单一的最佳运算符，则会发生绑定时错误。

## 7.3.5 候选用户定义运算符

给定类型 T 和操作 operator op(A)，其中 op 是可重载运算符，A 是参数列表，T 为运算符 op(A) 提供的候选用户定义运算符集合按如下方式确定：

-   确定类型 T0。如果 T 是可空类型，则 T0 为其基础类型，否则 T0 等于 T。

-   对于 T0 中所有 operator op 声明以及此类运算符的所有提升形式，如果至少有一个运算符相对于参数列表 A 是适用的（§7.5.3.1），则候选运算符集合由 T0 中所有此类适用运算符组成。

-   否则，如果 T0 是 object，则候选运算符集合为空。

-   否则，T0 提供的候选运算符集合是 T0 的直接基类提供的候选运算符集合，或者如果 T0 是类型参数，则是 T0 的有效基类提供的候选运算符集合。

## 7.3.6 数值提升

数值提升包括对预定义的一元和二元数值运算符的操作数自动执行某些隐式转换。数值提升不是一种独立的机制，而是在对预定义运算符应用重载解析时的效果。数值提升具体不影响用户定义运算符的求值，尽管用户定义运算符可以实现以表现出类似的效果。

作为数值提升的示例，请考虑二元 `*` 运算符的预定义实现：

```csharp
int operator *(int x, int y);
uint operator *(uint x, uint y);
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
float operator *(float x, float y);
double operator *(double x, double y);
decimal operator *(decimal x, decimal y);
```

当将重载解析规则（§7.5.3）应用于此运算符集合时，其效果是选择操作数类型存在隐式转换的第一个运算符。例如，对于操作 `b * s`，其中 b 为 byte，s 为 short，重载解析选择 `operator *(int, int)` 作为最佳运算符。因此，其效果是 b 和 s 被转换为 int，且结果的类型为 int。同样，对于操作 `i * d`，其中 i 为 int，d 为 double，重载解析选择 `operator *(double, double)` 作为最佳运算符。

### 7.3.6.1 一元数值提升

一元数值提升发生在预定义 `+`、`-` 和 `~` 一元运算符的操作数上。一元数值提升仅包括将类型为 sbyte、byte、short、ushort 或 char 的操作数转换为 int 类型。此外，对于一元 `-` 运算符，一元数值提升将类型为 uint 的操作数转换为 long。

### 7.3.6.2 二元数值提升

二元数值提升发生在预定义 `+`、`-`、`*`、 `/`、`%`、`&`、`|`、`^`、`<<`、`>>`、`==`、`!=`、`>`、`<`、`>=` 和 `<=` 二元运算符的操作数上。二元数值提升隐式地将两个操作数转换为共同类型，对于非关系运算符而言，该类型也成为操作的结果类型。二元数值提升包括按此处出现的顺序应用以下规则：

-   如果任一操作数为 decimal 类型，则另一操作数转换为 decimal 类型，或者如果另一操作数为 float 或 double 类型，则发生绑定时错误。

-   否则，如果任一操作数为 double 类型，则另一操作数转换为 double 类型。

-   否则，如果任一操作数为 float 类型，则另一操作数转换为 float 类型。

-   否则，如果任一操作数为 ulong 类型，则另一操作数转换为 ulong 类型，或者如果另一操作数为 sbyte、short、int 或 long 类型，则发生绑定时错误。

-   否则，如果任一操作数为 long 类型，则另一操作数转换为 long 类型。

-   否则，如果任一操作数为 uint 类型且另一操作数为 sbyte、short 或 int 类型，则两个操作数均转换为 long 类型。

-   否则，如果任一操作数为 uint 类型，则另一操作数转换为 uint 类型。

-   否则，两个操作数均转换为 int 类型。

请注意，第一条规则禁止将 decimal 类型与 double 和 float 类型混合的任何操作。该规则源于 decimal 类型与 double 和 float 类型之间不存在隐式转换的事实。

还请注意，不可能出现一个操作数为 ulong 类型而另一个操作数为有符号整数类型的情况。原因在于不存在能够同时表示 ulong 的完整范围以及有符号整数类型的整数类型。

在上述两种情况下，都可以使用强制转换表达式显式地将一个操作数转换为与另一个操作数兼容的类型。

在示例

```csharp
decimal AddPercent(decimal x, double percent) {
    return x * (1.0 + percent / 100.0);
}
```

会发生绑定时错误，因为 decimal 不能与 double 相乘。该错误通过显式地将第二个操作数转换为 decimal 来解决，如下所示：

```csharp
decimal AddPercent(decimal x, double percent) {
    return x * (decimal)(1.0 + percent / 100);
}
```

## 7.3.7 提升的运算符

*提升的运算符* 允许对非可空值类型操作的预定义和用户定义运算符也与这些类型的可空形式一起使用。提升的运算符由满足某些要求的预定义和用户定义运算符构造，如下所述：

-   对于一元运算符

  `+  ++  -  --  !  ~`

  如果操作数和结果类型均为非可空值类型，则存在该运算符的提升形式。提升形式是通过在操作数和结果类型上添加单个 `?` 修饰符构造的。提升运算符如果操作数为 null 则产生 null 值。否则，提升运算符解包操作数，应用基础运算符，并包装结果。

-   对于二元运算符

  `+  -  *  /  %  &  |  ^  <<  >>`

  如果操作数和结果类型均为非可空值类型，则存在该运算符的提升形式。提升形式是通过在每个操作数和结果类型上添加单个 `?` 修饰符构造的。提升运算符如果一个或两个操作数为 null 则产生 null 值（`bool?` 类型的 `&` 和 `|` 运算符除外，如 §7.11.3 中所述）。否则，提升运算符解包操作数，应用基础运算符，并包装结果。

-   对于相等运算符

  `==  !=`

  如果操作数类型均为非可空值类型且结果类型为 `bool`，则存在该运算符的提升形式。提升形式是通过在每个操作数类型上添加单个 `?` 修饰符构造的。提升运算符将两个 null 值视为相等，并将 null 值视为与任何非 null 值不相等。如果两个操作数均非 null，则提升运算符解包操作数并应用基础运算符以产生 `bool` 结果。

-   对于关系运算符

  `<  >  <=  >=`

  如果操作数类型均为非可空值类型且结果类型为 `bool`，则存在该运算符的提升形式。提升形式是通过在每个操作数类型上添加单个 `?` 修饰符构造的。提升运算符如果一个或两个操作数为 null 则产生值 `false`。否则，提升运算符解包操作数并应用基础运算符以产生 `bool` 结果。

## 7.4 成员查找

成员查找是在类型上下文中确定名称含义的过程。成员查找可以在求值表达式中的 *简单名称*（§7.6.2）或 *成员访问*（§7.6.4）的一部分中发生。如果 *简单名称* 或 *成员访问* 作为 *调用表达式*（§7.6.5.1）的 *简单表达式* 出现，则该成员被称为 *被调用*。



如果一个成员是方法或事件，或者它是委托类型 (§15) 或类型 dynamic (§4.7) 的常量、字段或属性，则该成员被称为可调用的。

成员查找不仅考虑成员的名称，还考虑成员具有的类型参数数量以及成员是否可访问。就成员查找而言，泛型方法和嵌套泛型类型具有在其各自声明中指示的类型参数数量，而所有其他成员的类型参数数量为零。

在类型 T 中对名称为 N 且具有 K 个类型参数的成员查找按如下方式处理：

- 首先，确定一组名为 N 的可访问成员：
  - 如果 T 是类型参数，则该集合是为 T 指定的主约束或次约束 (§10.1.5) 中每个类型里名为 N 的可访问成员集合的并集，以及 object 中名为 N 的可访问成员集合。
  - 否则，该集合由 T 中所有可访问的 (§3.5) 成员名 N 组成，包括继承的成员和 object 中可访问的成员名 N。如果 T 是构造类型，则成员集合通过 §10.3.2 中描述的类型参数替换获得。包含 override 修饰符的成员被排除在集合之外。
- 接下来，如果 K 为零，则删除所有声明中包含类型参数的嵌套类型。如果 K 不为零，则删除所有类型参数数量不同的成员。注意，当 K 为零时，具有类型参数的方法不会被删除，因为类型推断过程 (§7.5.2) 可能能够推断出类型参数。
- 接下来，如果成员被调用，则从集合中删除所有不可调用的成员。
- 接下来，从集合中删除被其他成员隐藏的成员。对于集合中的每个成员 S.M，其中 S 是声明成员 M 的类型，应用以下规则：
  - 如果 M 是常量、字段、属性、事件或枚举成员，则从集合中删除在 S 的基类型中声明的所有成员。
  - 如果 M 是类型声明，则从集合中删除在 S 的基类型中声明的所有非类型，以及在 S 的基类型中声明的与 M 具有相同数量类型参数的所有类型声明。
  - 如果 M 是方法，则从集合中删除在 S 的基类型中声明的所有非方法成员。
- 接下来，从集合中删除被类成员隐藏的接口成员。此步骤只有在 T 是类型参数并且 T 具有除 object 以外的有效基类且具有非空的有效接口集 (§10.1.5) 时才有效。对于集合中的每个成员 S.M，其中 S 是声明成员 M 的类型，如果 S 是 object 以外的类声明，则应用以下规则：
  - 如果 M 是常量、字段、属性、事件、枚举成员或类型声明，则从集合中删除在接口声明中声明的所有成员。
  - 如果 M 是方法，则从集合中删除在接口声明中声明的所有非方法成员，以及在接口声明中声明的与 M 具有相同签名的所有方法。
- 最后，在删除隐藏成员后，确定查找结果：
  - 如果集合由单个非方法成员组成，则该成员是查找结果。
  - 否则，如果集合仅包含方法，则该方法组是查找结果。
  - 否则，查找不明确，并发生绑定时错误。

对于类型参数和接口之外的类型中的成员查找，以及对于严格单继承的接口中的成员查找（继承链中的每个接口恰好有零个或一个直接基接口），查找规则的效果仅仅是派生成员隐藏具有相同名称或签名的基成员。此类单继承查找永远不会不明确。可能由多继承接口中的成员查找引起的歧义在 §13.2.5 中描述。

## 7.4.1 基类型

就成员查找而言，类型 T 被认为具有以下基类型：

- 如果 T 是 object，则 T 没有基类型。
- 如果 T 是枚举类型，则 T 的基类型是类类型 System.Enum、System.ValueType 和 object。
- 如果 T 是结构体类型，则 T 的基类型是类类型 System.ValueType 和 object。
- 如果 T 是类类型，则 T 的基类型是 T 的基类，包括类类型 object。
- 如果 T 是接口类型，则 T 的基类型是 T 的基接口和类类型 object。
- 如果 T 是数组类型，则 T 的基类型是类类型 System.Array 和 object。
- 如果 T 是委托类型，则 T 的基类型是类类型 System.Delegate 和 object。

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

除析构函数和静态构造函数（不能显式调用）外，函数成员中包含的语句通过函数成员调用执行。编写函数成员调用的实际语法取决于特定的函数成员类别。

函数成员调用的参数列表 (§7.5.1) 为函数成员的参数提供实际值或变量引用。

泛型方法的调用可能采用类型推断来确定要传递给方法的类型参数集合。此过程在 §7.5.2 中描述。

方法、索引器、运算符和实例构造函数的调用采用重载解析来确定要调用的候选函数成员集合中的哪一个。此过程在 §7.5.3 中描述。

一旦在绑定时（可能通过重载解析）识别出特定的函数成员，则调用函数成员的实际运行时过程在 §7.5.4 中描述。

| Construct | Example | Description |
|---|---|---|
|  | `T.E += value` | 类或结构体 T 中事件 E 的 add 访问器被调用。如果 E 不是静态的，则发生绑定时错误。 |
|  | `T.E -= value` | 类或结构体 T 中事件 E 的 remove 访问器被调用。如果 E 不是静态的，则发生绑定时错误。 |
|  | `e.E += value` | 用实例表达式 e 调用由 e 的类型给出的类、结构体或接口中事件 E 的 add 访问器。如果 E 是静态的，则发生绑定时错误。 |
|  | `e.E -= value` | 用实例表达式 e 调用由 e 的类型给出的类、结构体或接口中事件 E 的 remove 访问器。如果 E 是静态的，则发生绑定时错误。 |
| 索引器访问 | `e[x, y]` | 对由 e 的类型给出的类、结构体或接口应用重载解析以选择最佳索引器。用实例表达式 e 和参数列表 (x, y) 调用索引器的 **get** 访问器。如果索引器是写-only，则发生绑定时错误。 |
| 索引器访问 | `e[x, y] = value` | 对由 e 的类型给出的类、结构体或接口应用重载解析以选择最佳索引器。用实例表达式 e 和参数列表 (x, y, value) 调用索引器的 **set** 访问器。如果索引器是只读的，则发生绑定时错误。 |
| 运算符调用 | `-x` | 对由 x 的类型给出的类或结构体应用重载解析以选择最佳一元运算符。用参数列表 (x) 调用所选运算符。 |
| 运算符调用 | `x + y` | 对由 x 和 y 的类型给出的类或结构体应用重载解析以选择最佳二元运算符。用参数列表 (x, y) 调用所选运算符。 |
| 实例构造函数调用 | `new T(x, y)` | 对类或结构体 T 应用重载解析以选择最佳实例构造函数。用参数列表 (x, y) 调用实例构造函数。 |

### 7.5.1 参数列表

每个函数成员和委托调用都包含一个参数列表，该列表为函数成员的参数提供实际值或变量引用。指定函数成员调用的参数列表的语法取决于函数成员类别：

- 对于实例构造函数、方法、索引器和委托，参数指定为 *argument-list*，如下所述。对于索引器，在调用 **set** 访问器时，参数列表 additionally 包括指定为赋值运算符右操作数的表达式。
- 对于属性，调用 **get** 访问器时参数列表为空，而调用 **set** 访问器时参数列表由指定为赋值运算符右操作数的表达式组成。
- 对于事件，参数列表由指定为 **+=** 或 **-=** 运算符右操作数的表达式组成。



-   对于用户定义的操作符，参数列表由一元操作符的单个操作数或二元操作符的两个操作数组成。

属性（§10.7）、事件（§10.8）和用户定义的操作符（§10.10）的参数总是作为值参数（§10.6.1.1）传递。索引器（§10.9）的参数总是作为值参数（§10.6.1.1）或参数数组（§10.6.1.4）传递。对于这些类别的函数成员，不支持引用参数和输出参数。

实例构造函数、方法、索引器或委托调用的参数被指定为一个*argument-list*：

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

*argument-list*由一个或多个*arguments*组成，以逗号分隔。每个*argument*由一个可选的*argument-name*后跟一个*argument-value*组成。带有*argument-name*的*argument*称为*命名参数*，而没有*argument-name*的*argument*则是*位置参数*。在*argument-list*中，位置参数出现在命名参数之后是错误的。

*argument-value*可以采用以下形式之一：

-   一个*expression*，表示该参数作为值参数（§10.6.1.1）传递。
-   关键字*ref*后跟一个*variable-reference*（§5.4），表示该参数作为引用参数（§10.6.1.2）传递。变量在被作为引用参数传递之前必须被明确赋值（§5.3）。
-   关键字*out*后跟一个*variable-reference*（§5.4），表示该参数作为输出参数（§10.6.1.3）传递。在变量作为输出参数传递的函数成员调用之后，该变量被视为已明确赋值（§5.3）。

## 7.5.1.1 对应的参数

对于参数列表中的每个参数，在被调用的函数成员或委托中必须有一个对应的参数。

下面使用的参数列表按如下方式确定：

-   对于类中定义的虚拟方法和索引器，参数列表取自函数成员的最特定声明或重写，从接收者的静态类型开始，并搜索其基类。
-   对于接口方法和索引器，参数列表取自成员的最特定定义，从接口类型开始，并搜索基接口。如果找不到唯一的参数列表，则构造一个具有不可访问名称且没有可选参数的参数列表，以便调用不能使用命名参数或省略可选参数。
-   对于分部方法，使用定义性分部方法声明的参数列表。
-   对于所有其他函数成员和委托，只有一个参数列表，即所使用的那个。

参数或参数的位置定义为参数列表或参数列表中它前面的参数或参数的个数。

函数成员参数的对应参数按如下方式确定：

-   实例构造函数、方法、索引器和委托的*argument-list*中的参数：
    -   位置参数，其中固定参数在参数列表中同一位置出现，对应于该参数。
    -   以其正常形式调用的具有参数数组的函数成员的位置参数对应于参数数组，该参数数组必须出现在参数列表中的同一位置。
    -   以其展开形式调用的具有参数数组的函数成员的位置参数，在参数列表中同一位置没有固定参数时，对应于参数数组中的一个元素。
    -   命名参数对应于参数列表中同名的参数。
    -   对于索引器，当调用`set`访问器时，指定为赋值运算符右操作数的表达式对应于`set`访问器声明的隐式`value`参数。
-   对于属性，当调用`get`访问器时没有参数。当调用`set`访问器时，指定为赋值运算符右操作数的表达式对应于`set`访问器声明的隐式`value`参数。
-   对于用户定义的一元操作符（包括转换），单个操作数对应于操作符声明的单个参数。
-   对于用户定义的二元操作符，左操作数对应于第一个参数，右操作数对应于操作符声明的第二个参数。

## 7.5.1.2 参数列表的运行时求值

在函数成员调用（§7.5.4）的运行时处理期间，参数列表的表达式或变量引用按顺序从左到右求值，如下所示：

-   对于值参数，对参数表达式进行求值，并执行到相应参数类型的隐式转换（§6.1）。结果值成为函数成员调用中值参数的初始值。
-   对于引用或输出参数，对变量引用进行求值，所得的存储位置成为函数成员调用中参数所表示的存储位置。如果作为引用或输出参数给出的变量引用是*引用类型*的数组元素，则执行运行时检查以确保数组的元素类型与参数的类型相同。如果此检查失败，则抛出`System.ArrayTypeMismatchException`。

方法、索引器和实例构造函数可以将其最右边的参数声明为参数数组（§10.6.1.4）。此类函数成员以其正常形式或展开形式调用，具体取决于哪个适用（§7.5.3.1）：

-   当具有参数数组的函数成员以其正常形式调用时，为参数数组给定的参数必须是单个表达式，该表达式可隐式转换（§6.1）为参数数组类型。在这种情况下，参数数组的作用完全类似于值参数。
-   当具有参数数组的函数成员以其展开形式调用时，调用必须为参数数组指定零个或多个位置参数，其中每个参数都是可隐式转换（§6.1）为参数数组元素类型的表达式。在这种情况下，调用会创建参数数组类型的一个实例，其长度与参数个数对应，用给定的参数值初始化数组实例的元素，并将新创建的数组实例用作实际参数。

参数列表的表达式总是按书写顺序求值。因此，示例

```csharp
class Test
{
    static void F(int x, int y = -1, int z = -2) {
        System.Console.WriteLine("x = {0}, y = {1}, z = {2}", x, y, z);
    }
    static void Main() {
        int i = 0;
        F(i++, i++, i++);
        F(z: i++, x: i++);
    }
}
```

产生输出

x = 0, y = 1, z = 2
x = 4, y = -1, z = 3

数组协变规则（§12.5）允许数组类型A[]的值成为数组类型B[]实例的引用，前提是存在从B到A的隐式引用转换。由于这些规则，当引用类型的数组元素作为引用或输出参数传递时，需要进行运行时检查，以确保数组的实际元素类型与参数的类型相同。在示例中

```csharp
class Test
{
    static void F(ref object x) {...}
    static void Main() {
        object[] a = new object[10];
        object[] b = new string[10];
        F(ref a[0]);    // OK
        F(ref b[1]);    // ArrayTypeMismatchException
    }
}
```

第二次调用F会导致抛出System.ArrayTypeMismatchException，因为b的实际元素类型是string而不是object。

当具有参数数组的函数成员以其展开形式调用时，调用的处理方式与在展开的参数周围插入带有数组初始化器的数组创建表达式（§7.6.10.4）完全一样。例如，给定声明

```csharp
void F(int x, int y, params object[] args);
```

以下对该方法展开形式的调用
F(10, 20);
F(10, 20, 30, 40);
F(10, 20, 1, "hello", 3.0);

完全对应于
F(10, 20, new object[] {});
F(10, 20, new object[] {30, 40});
F(10, 20, new object[] {1, "hello", 3.0});

特别要注意，当为参数数组给定零个参数时，会创建一个空数组。




当从具有相应可选参数的函数成员中省略实参时，会隐式传递该函数成员声明中的默认实参。由于这些默认实参始终是常量，对它们的求值不会影响其余实参的求值顺序。

## 7.5.2 类型推断

当调用泛型方法但未指定类型实参时，类型推断过程会尝试为该调用推断类型实参。类型推断的存在允许使用更方便的语法来调用泛型方法，并使程序员能够避免指定冗余的类型信息。例如，给定以下方法声明：

```
class Chooser
{
    static Random rand = new Random();
    public static T Choose<T>(T first, T second) {
        return (rand.Next(2) == 0)? first: second;
    }
}
```

可以在不显式指定类型实参的情况下调用 Choose 方法：

```
int i = Chooser.Choose(5, 213);     // Calls Choose<int>
string s = Chooser.Choose("foo", "bar");   // Calls Choose<string>
```

通过类型推断，类型实参 int 和 string 由该方法的实参确定。

类型推断作为方法调用的绑定期处理的一部分发生（§7.6.5.1），并且在该调用的重载决策步骤之前进行。当在方法调用中指定了特定方法组，且未在方法调用中指定类型实参时，会对该方法组中的每个泛型方法应用类型推断。如果类型推断成功，则使用推断出的类型实参来确定后续重载决策的实参类型。如果重载决策选择某个泛型方法作为要调用的方法，则使用推断出的类型实参作为该调用的实际类型实参。如果对特定方法的类型推断失败，则该方法不参与重载决策。类型推断失败本身不会导致绑定期错误。然而，当重载决策随后未能找到任何适用的方法时，它通常会导致绑定期错误。

如果提供的实参数量与方法中的参数数量不同，则推断立即失败。否则，假设该泛型方法具有以下签名：T_r M<X1...Xn>(T1 X1 ... Tn X_n)

对于形式为 M(E1 ... Em) 的方法调用，类型推断的任务是为每个类型参数 X1...Xn 找到唯一的类型实参 S1...Sn，使得调用 M<S1...Sn>(E1...Em) 变得有效。

在推断过程中，每个类型参数 Xi 要么固定为特定类型 Si，要么未固定并具有一组关联的边界。每个边界都是某种类型 T。最初，每个类型变量 Xi 都是未固定的，并且边界集为空。

类型推断分阶段进行。每个阶段将基于上一阶段的发现，尝试为更多类型变量推断类型实参。第一阶段进行一些初始的边界推断，而第二阶段将类型变量固定为特定类型并推断更多边界。第二阶段可能需要重复多次。

注意：类型推断不仅发生在调用泛型方法时。方法组转换的类型推断在 §7.5.2.13 中描述，查找一组表达式的最佳公共类型在 §7.5.2.14 中描述。

### 7.5.2.1 第一阶段

对于每个方法实参 E_i：

- 如果 Eᵢ 是匿名函数，则从 Eᵢ 到 Tᵢ 进行显式参数类型推断（§7.5.2.7）。
- 否则，如果 Eᵢ 具有类型 U 且 xᵢ 是值参数，则从 U 到 Tᵢ 进行下限推断。
- 否则，如果 Eᵢ 具有类型 U 且 xᵢ 是 ref 或 out 参数，则从 U 到 Tᵢ 进行精确推断。
- 否则，不对此实参进行任何推断。

### 7.5.2.2 第二阶段

第二阶段按如下方式进行：

- 所有不依赖于（§7.5.2.5）任何 Xⱼ 的未固定类型变量 Xᵢ 都被固定（§7.5.2.10）。
- 如果不存在此类类型变量，则固定所有满足以下全部条件的未固定类型变量 Xᵢ：
  - 至少存在一个依赖于 Xᵢ 的类型变量 Xⱼ
  - Xᵢ 具有非空边界集
- 如果不存在此类类型变量且仍有未固定类型变量，则类型推断失败。
- 否则，如果不存在更多未固定类型变量，则类型推断成功。
- 否则，对于所有具有对应参数类型 Tᵢ 的实参 Eᵢ，若输出类型（§7.5.2.4）包含未固定类型变量 Xᵢ 而输入类型（§7.5.2.3）不包含，则从 Eᵢ 到 Tᵢ 进行输出类型推断（§7.5.2.6）。然后重复第二阶段。

### 7.5.2.3 输入类型

如果 E 是方法组或隐式类型匿名函数，且 T 是委托类型或表达式树类型，则 T 的所有参数类型都是 E（具有类型 T）的输入类型。

### 7.5.2.4 输出类型

如果 E 是方法组或匿名函数，且 T 是委托类型或表达式树类型，则 T 的返回类型是 E（具有类型 T）的输出类型。

### 7.5.2.5 依赖关系

如果对于某个具有类型 Tₖ 的实参 Eₖ，Xⱼ 出现在 Eₖ（具有类型 Tₖ）的输入类型中，而 Xᵢ 出现在 Eₖ（具有类型 Tₖ）的输出类型中，则未固定类型变量 Xᵢ 直接依赖于未固定类型变量 Xⱼ。

如果 Xⱼ 直接依赖于 Xᵢ，或者 Xᵢ 直接依赖于 Xₖ 且 Xₖ 依赖于 Xⱼ，则 Xⱼ 依赖于 Xᵢ。因此，“依赖于”是“直接依赖于”的传递但非自反闭包。

### 7.5.2.6 输出类型推断

输出类型推断按以下方式从表达式 E 到类型 T 进行：

- 如果 E 是推断返回类型为 U 的匿名函数（§7.5.2.12），且 T 是返回类型为 T_b 的委托类型或表达式树类型，则从 U 到 T_b 进行下限推断（§7.5.2.9）。
- 否则，如果 E 是方法组，且 T 是具有参数类型 T₁..T_k 和返回类型 T_b 的委托类型或表达式树类型，并且使用类型 T₁..T_k 对 E 进行重载决策得到单个返回类型为 U 的方法，则从 U 到 T_b 进行下限推断。
- 否则，如果 E 是具有类型 U 的表达式，则从 U 到 T 进行下限推断。
- 否则，不进行任何推断。

### 7.5.2.7 显式参数类型推断

显式参数类型推断按以下方式从表达式 E 到类型 T 进行：

- 如果 E 是具有参数类型 U₁...Uₖ 的显式类型匿名函数，且 T 是具有参数类型 V₁...Vₖ 的委托类型或表达式树类型，则对于每个 Uᵢ，都*从* Uᵢ *到*对应的 Vᵢ 进行*精确推断*（§7.5.2.8）。

### 7.5.2.8 精确推断

*从类型 U 到类型 V 的精确推断*按如下方式进行：

- 如果 V 是某个*未固定*的 Xᵢ，则将 U 添加到 Xᵢ 的精确边界集中。
- 否则，通过检查以下任一情况是否适用来确定集合 V₁...Vₖ 和 U₁...Uₖ：
  - V 是数组类型 V₁[...] 且 U 是相同秩的数组类型 U₁[...]
  - V 是类型 V₁? 且 U 是类型 U₁?
  - V 是构造类型 C<V₁...Vₖ> 且 U 是构造类型 C<U₁...Uₖ>
- 如果任一情况适用，则从每个 Uᵢ 到对应的 Vᵢ 进行*精确推断*。
- 否则，不进行任何推断。

### 7.5.2.9 下限推断

*从类型 U 到类型 V 的下限推断*按如下方式进行：

- 如果 V 是某个*未固定*的 Xᵢ，则将 U 添加到 Xᵢ 的下限集中。
- 否则，通过检查以下任一情况是否适用来确定集合 U₁...Uₖ 和 V₁...Vₖ：
  - V 是数组类型 V₁[...] 且 U 是相同秩的数组类型 U₁[...]（或有效基类型为 U₁[...] 的类型参数）
  - V 是 IEnumerable<V₁>、ICollection<V₁> 或 IList<V₁> 之一，且 U 是一维数组类型 U₁[]（或有效基类型为 U₁[] 的类型参数）
  - V 是类型 V₁? 且 U 是类型 U₁?
  - V 是构造类、结构、接口或委托类型 C<V₁...Vₖ>，且存在唯一类型 C<U₁...Uₖ>，使得 U（或者，如果 U 是类型参数，则为其有效基类或有效接口集中的任何成员）与 C<U₁...Uₖ> 相同、继承自（直接或间接）或实现（直接或间接）C<U₁...Uₖ>。
- （“唯一性”限制意味着，在接口 C<T>{}、类 U: C<X>, C<Y>{} 的情况下，当从 U 推断到 C<T> 时不进行任何推断，因为 U₁ 可能是 X 或 Y。）
- 如果任一情况适用，则按如下方式从每个 Uᵢ 到对应的 Vᵢ 进行推断：
  - 如果 Uᵢ 未知为引用类型，则进行*精确推断*
  - 否则，如果 U 是数组类型，则进行*下限推断*
  - 否则，如果 V 是 C<V₁...Vₖ>，则推断取决于 C 的第 i 个类型参数：
    - 如果它是协变的，则进行*下限推断*。
    - 如果它是逆变的，则进行*上限推断*。
    - 如果它是不变的，则进行*精确推断*。
- 否则，不进行任何推断。



## 7.5.2.10 上界推断

从类型 U 到类型 V 的上界推断按如下方式进行：

- 如果 V 是某个未固定的 X_i 之一，则将 U 添加到 X_i 的上界集合中。
- 否则，通过检查以下任一情况是否适用来确定集合 V₁...V_k 和 U₁...U_k：
  - U 是数组类型 U₁[...]，且 V 是相同秩的数组类型 V₁[...]
  - U 是 IEnumerable<U₀>、ICollection<U₀> 或 IList<U₀> 之一，且 V 是一维数组类型 V_e[]
  - U 是类型 U₁?，且 V 是类型 V₁?
  - U 是构造的类、结构、接口或委托类型 C<U₁...U_k>，且 V 是类、结构、接口或委托类型，该类型与某个唯一类型 C<V₁...V_k> 相同、从它继承（直接或间接）或实现它（直接或间接）
    （“唯一性”限制意味着，如果我们有接口 C<T>{} class V<Z>: C<X<Z>>, C<Y<Z>>{}，那么从 C<U₁> 推断到 V<Q> 时不会进行推断。不会从 U₁ 推断到 X<Q> 或 Y<Q>。）

如果这些情况中的任一情况适用，则按如下方式从每个 U_i 推断到对应的 V_i：

- 如果 U_i 未知为引用类型，则进行精确推断
- 否则，如果 V 是数组类型，则进行上界推断
- 否则，如果 U 是 C<U₁...U_k>，则推断取决于 C 的第 i 个类型参数：
  - 如果它是协变的，则进行上界推断。
  - 如果它是逆变的，则进行下界推断。
  - 如果它是不变的，则进行精确推断。
- 否则，不进行任何推断。

## 7.5.2.11 固定

具有界限集合的未固定类型变量 X_i 按如下方式固定：

- 候选类型集合 U_j 初始为 X_i 的界限集合中的所有类型组成的集合。
- 然后依次检查 X_i 的每个界限：对于 X_i 的每个界限 U，从候选集合中移除所有与 U 不相同的类型 U_j。对于 X_i 的每个下界 U，从候选集合中移除所有不存在从 U 到 U_j 的隐式转换的类型 U_j。对于 X_i 的每个上界 U，从候选集合中移除所有不存在从 U_j 到 U 的隐式转换的类型 U_j。
- 如果在剩余的候选类型 U_j 中存在唯一类型 V，使得存在从 V 到所有其他候选类型的隐式转换，则将 X_i 固定为 V。
- 否则，类型推断失败。

## 7.5.2.12 推断的返回类型

匿名函数 F 的推断返回类型在类型推断和重载决策期间使用。只能为所有参数类型均已知的匿名函数确定推断返回类型，这些参数类型要么是显式给出的，要么是通过匿名函数转换提供的，要么是在对封闭泛型方法调用进行类型推断期间推断出的。推断返回类型按如下方式确定：

- 如果 F 的主体是表达式，则 F 的推断返回类型是该表达式的类型。
- 如果 F 的主体是块，并且该块的 return 语句中的表达式集合具有最佳公共类型 T（§7.5.2.14），则 F 的推断返回类型是 T。
- 否则，无法为 F 推断返回类型。

作为涉及匿名函数的类型推断示例，请考虑在 System.Linq.Enumerable 类中声明的 Select 扩展方法：

```
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource,TResult>(
            this IEnumerable<TSource> source,
            Func<TSource,TResult> selector)
        {
            foreach (TSource element in source) yield return selector(element);
        }
    }
}
```

假设已通过 using 子句导入 System.Linq 命名空间，并给定一个具有 string 类型 Name 属性的 Customer 类，则可以使用 Select 方法选择客户列表中的姓名：

```
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

Select 的扩展方法调用（§7.6.5.2）通过将调用重写为静态方法调用来处理：

```
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

由于未显式指定类型实参，因此使用类型推断来推断类型实参。首先，customers 实参与 source 形参关联，推断 T 为 Customer。然后，使用上述匿名函数类型推断过程，为 c 赋予类型 Customer，并将表达式 c.Name 与 selector 形参的返回类型关联，推断 S 为 string。因此，该调用等效于

```
Enumerable.Select<Customer,string>(customers, (Customer c) => c.Name)
```

且结果的类型为 IEnumerable<string>。

以下示例演示匿名函数类型推断如何使类型信息在泛型方法调用中的实参之间“流动”。给定方法：

```
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2) {
    return f2(f1(value));
}
```

对以下调用的类型推断：

```
double seconds = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalSeconds);
```

按如下方式进行：首先，实参 "1:15:30" 与 value 形参关联，推断 X 为 string。然后，第一个匿名函数的形参 s 被赋予推断出的类型 string，并将表达式 TimeSpan.Parse(s) 与 f1 的返回类型关联，推断 Y 为 System.TimeSpan。最后，第二个匿名函数的形参 t 被赋予推断出的类型 System.TimeSpan，并将表达式 t.TotalSeconds 与 f2 的返回类型关联，推断 Z 为 double。因此，该调用的结果为 double 类型。

## 7.5.2.13 方法组转换的类型推断

与泛型方法的调用类似，当包含泛型方法的方法组 M 转换为给定委托类型 D（§6.6）时，也必须应用类型推断。给定方法

```
T_r M<X1...Xn>(T1 X1 ... Tm Xn)
```

并且将方法组 M 赋给委托类型 D 时，类型推断的任务是找到类型实参 S1...Sn，使得表达式：
M<S1...Sn>
与 D 兼容（§15.1）。

与泛型方法调用的类型推断算法不同，在这种情况下只有实参类型，没有实参表达式。特别地，没有匿名函数，因此不需要多阶段推断。

相反，所有 Xi 被视为未固定，并从 D 的每个实参类型 Uj 到 M 的对应形参类型 Tj 进行下界推断。如果对于任何 Xi 都未找到界限，则类型推断失败。否则，所有 Xi 被固定为对应的 Si，这些 Si 就是类型推断的结果。

## 7.5.2.14 寻找一组表达式的最佳公共类型

在某些情况下，需要为一组表达式推断公共类型。特别地，隐式类型数组的元素类型以及具有块主体的匿名函数的返回类型就是通过这种方式找到的。

直观地说，给定一组表达式 E1...Em，这种推断应等效于调用方法
T_r M<X>(X x1 ... X xm)
并以 Ei 作为实参。

更准确地说，推断从一个未固定类型变量 X 开始。然后从每个 Ei 到 X 进行输出类型推断。最后，固定 X，如果成功，则所得类型 S 就是这些表达式的最佳公共类型。如果不存在这样的 S，则这些表达式没有最佳公共类型。

## 7.5.3 重载决策

重载决策是一种绑定时的机制，用于在给定实参列表和一组候选函数成员的情况下选择要调用的最佳函数成员。在 C# 中，重载决策在以下不同上下文中选择要调用的函数成员：

- 调用调用表达式中命名的方法（§7.6.5.1）。
- 调用对象创建表达式中命名的实例构造函数（§7.6.10.1）。
- 通过元素访问调用索引器访问器（§7.6.6）。
- 调用表达式中引用的预定义或用户定义运算符（§7.3.3 和 §7.3.4）。



下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其出现在参数列表中与对应参数相同的[content]
下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其出现在参数列表中与对应参数相同的[content]
下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其出现在参数列表中与对应参数相同的[content]
下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其出现在参数列表中与对应参数相同的[content]
下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其出现在参数列表中与对应参数相同的[content]
下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其出现在参数列表中与对应参数相同的[content]
下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其出现在参数列表中与对应参数相同的[content]
下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其出现在参数列表中与对应参数相同的[content]
下面的各节定义了术语 *适用的函数成员* 和 *更好的函数成员* 的确切含义。

## 7.5.3.1 适用的函数成员

函数成员在相对于参数列表 A 时，如果满足以下所有条件，则称其为 *适用的函数成员*：

- A 中的每个参数都对应于函数成员声明中所述的 §7.5.1.1 中的一个参数，并且任何没有对应参数的参数都是可选参数。
- 对于 A 中的每个参数，参数的参数传递模式（即 value、ref 或 out）与对应参数的参数传递模式相同，并且
  - 对于值参数或参数数组，从参数到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。毕竟，ref 或 out 参数是传递的参数的别名。

对于包含参数数组的函数成员，如果该函数成员根据上述规则适用，则称其在其 *常规形式* 下适用。如果包含参数数组的函数成员在其常规形式下不适用，则该函数成员可能在其 *展开形式* 下适用：

- 展开形式是通过用参数数组的元素类型的零个或多个值参数替换函数成员声明中的参数数组构造的，使得参数列表 A 中的参数数量与参数总数匹配。如果 A 的参数少于函数成员声明中固定参数的数量，则无法构造该函数成员的展开形式，因此不适用。
- 否则，如果对于 A 中的每个参数，参数的参数传递模式与对应参数的参数传递模式相同，并且
  - 对于固定的值参数或由展开创建的值参数，从参数类型到对应参数类型的隐式转换 (§6.1) 存在，或者
  - 对于 ref 或 out 参数，参数的类型与对应参数的类型相同。

## 7.5.3.2 更好的函数成员

为了确定更好的函数成员，构造一个精简的参数列表 A，仅包含参数表达式本身，按其在原始参数列表中出现的顺序排列。

每个候选函数成员的参数列表按以下方式构造：

- 如果函数成员仅在展开形式下适用，则使用展开形式。
- 从参数列表中删除没有对应参数的可选参数
- 参数被重新排序，使其与参数列表中对应参数的位置一致。

给定参数列表 A 及其参数表达式集合 { E1, E2, ..., En } 以及两个适用的函数成员 Mp 和 Mq，其参数类型分别为 { P1, P2, ..., Pn } 和 { Q1, Q2, ..., Qn }，如果满足以下条件，则 Mp 被定义为比 Mq 更好的函数成员

- 对于每个参数，从 Ex 到 Qx 的隐式转换不优于从 Ex 到 Px 的隐式转换，并且
- 对于至少一个参数，从 Ex 到 Px 的转换优于从 Ex 到 Qx 的转换。

## 7.5.3.4 从类型转换的更好性

给定一个从类型 S 转换为类型 T₁ 的转换 C₁，以及一个从类型 S 转换为类型 T₂ 的转换 C₂，如果满足以下至少一个条件，则 C₁ 是比 C₂ 更好的转换：

- 从 S 到 T₁ 存在恒等转换，但从 S 到 T₂ 不存在
- T₁ 比 T₂ 是更好的转换目标 (§7.5.3.5)

## 7.5.3.5 更好的转换目标

给定两个不同的类型 T₁ 和 T₂，如果满足以下至少一个条件，则 T₁ 是比 T₂ 更好的转换目标：

- 从 T₁ 到 T₂ 存在隐式转换，而从 T₂ 到 T₁ 不存在隐式转换
- T₁ 是有符号整数类型而 T₂ 是无符号整数类型。具体而言：
  - T₁ 是 sbyte 而 T₂ 是 byte、ushort、uint 或 ulong
  - T₁ 是 short 而 T₂ 是 ushort、uint 或 ulong
  - T₁ 是 int 而 T₂ 是 uint 或 ulong
  - T₁ 是 long 而 T₂ 是 ulong

## 7.5.3.6 泛型类中的重载

虽然声明时的签名必须唯一，但类型参数的替换可能导致签名相同。在这种情况下，重载解析的上述平局打破规则将选择最具体的成员。

以下示例展示了根据此规则有效和无效的重载：

```
interface I1<T> { ... }
interface I2<T> { ... }
class G1<U>
{
    int F1(U u);            // overload resolution for G<int>.F1
    int F1(int i);          // will pick non-generic
    void F2(I1<U> a);       // valid overload
    void F2(I2<U> a);
}
class G2<U,V>
{
    void F3(U u, V v);      // valid, but overload resolution for
    void F3(V v, U u);      // G2<int,int>.F3 will fail
    void F4(U u, I1<V> v);  // Valid, but overload resolution for
    void F4(I1<V> v, V u);  // G2<I1<int>,int>.F4 will fail
    void F5(U u1, I1<V> v2); // valid overload
    void F5(V v1, U u2);
    void F6(ref U u);       // valid overload
    void F6(out V v);
}
```

## 7.5.4 动态重载解析的编译时检查

对于大多数动态绑定操作，解析的候选集在编译时是未知的。然而在某些情况下，候选集在编译时是已知的：

- 具有动态参数的静态方法调用
- 接收方不是动态表达式的实例方法调用
- 接收方不是动态表达式的索引器调用
- 具有动态参数的构造函数调用

在这些情况下，对每个候选执行有限的编译时检查，以查看它们在运行时是否可能适用。该检查包括以下步骤：

- 部分类型推断：任何不直接或间接依赖于类型为 dynamic 的参数的类型参数都使用 §7.5.2 的规则推断。剩余的类型参数未知。
- 部分适用性检查：根据 §7.5.3.1 检查适用性，但忽略类型未知的参数。

如果没有候选通过此测试，则会发生编译时错误。

## 7.5.5 函数成员调用

本节描述了在运行时调用特定函数成员时发生的过程。假设绑定时过程已经确定了要调用的特定成员，可能通过对一组候选函数成员应用重载解析。

为了描述调用过程，函数成员分为两类：

- 静态函数成员。这些是实例构造函数、静态方法、静态属性访问器和用户定义运算符。静态函数成员始终是非虚拟的。
- 实例函数成员。这些是实例方法、实例属性访问器和索引器访问器。实例函数成员是不可虚拟或虚拟的，并且始终在特定实例上调用。实例由实例表达式计算，并在函数成员内作为 this (§7.6.7) 可访问。

函数成员调用的运行时处理包括以下步骤，其中 M 是函数成员，如果 M 是实例成员，则 E 是实例表达式：

- 如果 M 是静态函数成员：
  - 按 §7.5.1 所述评估参数列表。
  - 调用 M。
- 如果 M 是在值类型中声明的实例函数成员：
  - 评估 E。如果此评估导致异常，则不执行后续步骤。
  - 如果 E 未被分类为变量，则创建 E 类型的一个临时局部变量，并将 E 的值赋给该变量。然后 E 被重新分类为对该临时局部变量的引用。临时变量在 M 内作为 this 可访问，但在其他任何地方不可访问。因此，只有当 E 是真正的变量时，调用者才能观察到 M 对 this 所做的更改。
  - 按 §7.5.1 所述评估参数列表。
  - 调用 M。E 引用的变量变为 this 引用的变量。
- 如果 M 是在引用类型中声明的实例函数成员：
  - 评估 E。如果此评估导致异常，则不执行后续步骤。
  - 按 §7.5.1 所述评估参数列表。
  - 如果 E 的类型是值类型，则执行装箱转换 (§4.3.1) 将 E 转换为类型 object，并在以下步骤中将 E 视为 object 类型。在这种情况下，M 只能是 System.Object 的成员。



- 将检查 E 的值是否有效。如果 E 的值为 null，则抛出 System.NullReferenceException，并且不再执行后续步骤。
- 确定要调用的函数成员实现：
  - 如果 E 的绑定期类型是接口，则要调用的函数成员是 E 所引用实例的运行时类型提供的 M 的实现。该函数成员通过应用接口映射规则（§13.4.4）来确定 E 所引用实例的运行时类型所提供的 M 的实现。
  - 否则，如果 M 是虚函数成员，则要调用的函数成员是 E 所引用实例的运行时类型提供的 M 的实现。该函数成员通过应用相对于 E 所引用实例的运行时类型来确定 M 的最派生实现的规则（§10.6.3）来确定。
  - 否则，M 是非虚函数成员，要调用的函数成员就是 M 本身。
- 然后调用上一步确定的函数成员实现。E 所引用的对象成为 this 所引用的对象。

## 7.5.5.1 对装箱实例的调用

在值类型中实现的函数成员，在下列情况下可以通过该值类型的装箱实例进行调用：

- 当该函数成员是继承自 object 类型的方法的重写，并且通过 object 类型的实例表达式进行调用时。
- 当该函数成员是接口函数成员的实现，并且通过接口类型的实例表达式进行调用时。
- 当该函数成员通过委托进行调用时。

在这些情况下，装箱实例被视为包含一个该值类型的变量，并且此变量成为函数成员调用中 this 所引用的变量。特别是，这意味着当在装箱实例上调用函数成员时，函数成员有可能修改装箱实例中所包含的值。

## 7.6 主表达式

主表达式包括最简单的表达式形式。

```
primary-expression:
  primary-no-array-creation-expression
  array-creation-expression
```

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
checked-expression
unchecked-expression
default-value-expression
anonymous-method-expression
```

主表达式分为数组创建表达式和不含数组创建表达式的主表达式。以这种方式处理数组创建表达式，而不是将其与其他简单表达式形式列在一起，使语法能够禁止可能引起混淆的代码，例如

```
object o = new int[3][1];
```

否则它会被解释为：

```
object o = (new int[3])[1];
```

### 7.6.1 字面量

由字面量（§2.4.4）组成的主表达式被分类为值。

### 7.6.2 简单名称

简单名称由一个标识符组成，其后可选地跟一个类型实参列表：

```
simple-name:
  identifier type-argument-list_opt
```

简单名称的形式为 I 或 I<A1, ..., Ak>，其中 I 是单个标识符，<A1, ..., Ak> 是可选的类型实参列表。如果未指定类型实参列表，则 K 视为零。简单名称按如下方式计算和分类：

- 如果 K 为零，且该简单名称出现在块内，并且该块（或某个封闭块）的局部变量声明空间（§3.3）包含名为 I 的局部变量、参数或常量，则该简单名称引用该局部变量、参数或常量，并被分类为变量和值。
- 如果 K 为零，且该简单名称出现在泛型方法声明的主体中，并且该声明包含名为 I 的类型参数，则该简单名称引用该类型参数。
- 否则，对于每个实例类型 T（§10.3.1），从直接包含该简单名称的类型声明的实例类型开始，并继续依次查看每个封闭类或结构声明的实例类型（如果有的话）：
  - 如果 K 为零，且 T 的声明包含名为 I 的类型参数，则该简单名称引用该类型参数。
  - 否则，如果在 T 中对 I 执行带 K 个类型实参的成员查找（§7.4）产生匹配，则：
    - 如果 T 是直接封闭类或结构类型的实例类型，并且该查找标识出一个或多个方法，则结果是一个方法组，其关联的实例表达式为 this。如果指定了类型实参列表，则它用于调用泛型方法（§7.6.5.1）。
    - 否则，如果 T 是直接封闭类或结构类型的实例类型，如果该查找标识出一个实例成员，并且该引用出现在实例构造函数、实例方法或实例访问器的块内，则结果与形式为 this.I 的成员访问（§7.6.4）相同。这种情况只可能发生在 K 为零时。
    - 否则，结果与形式为 T.I 或 T.I<A1, ..., Ak> 的成员访问（§7.6.4）相同。在这种情况下，简单名称引用实例成员属于绑定期错误。
  - 否则，对于每个命名空间 N，从简单名称出现的命名空间开始，继续依次查看每个封闭命名空间（如果有的话），最后到全局命名空间，执行以下步骤，直到找到实体为止：
    - 如果 K 为零，且 I 是 N 中某个命名空间的名称，则：
      - 如果简单名称出现的位置被 N 的命名空间声明所包围，并且该命名空间声明包含将名称 I 与某个命名空间或类型关联的外部别名指令或 using 别名指令，则该简单名称具有歧义，并发生编译时错误。
      - 否则，该简单名称引用 N 中名为 I 的命名空间。
    - 否则，如果 N 包含名为 I 且具有 K 个类型参数的可访问类型，则：
      - 如果 K 为零，且简单名称出现的位置被 N 的命名空间声明所包围，并且该命名空间声明包含将名称 I 与某个命名空间或类型关联的外部别名指令或 using 别名指令，则该简单名称具有歧义，并发生编译时错误。
      - 否则，该命名空间或类型名称引用使用给定类型实参构造的类型。
    - 否则，如果简单名称出现的位置被 N 的命名空间声明所包围：
      - 如果 K 为零，且该命名空间声明包含将名称 I 与导入的命名空间或类型关联的外部别名指令或 using 别名指令，则该简单名称引用该命名空间或类型。
      - 否则，如果该命名空间声明的 using 命名空间指令所导入的命名空间中，恰好只有一个名为 I 且具有 K 个类型参数的类型，则该简单名称引用使用给定类型实参构造的类型。
      - 否则，如果该命名空间声明的 using 命名空间指令所导入的命名空间中，包含多个名为 I 且具有 K 个类型参数的类型，则该简单名称具有歧义，并发生错误。

  请注意，这整个步骤与处理命名空间或类型名称（§3.8）时的相应步骤完全对应。
- 否则，该简单名称未定义，并发生编译时错误。




在给定的块、switch 块、for、foreach 或 using 语句或者匿名函数中，名称的含义始终相同。

示例

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

会导致编译时错误，因为 x 在外层块（其范围包括 if 语句中的嵌套块）中引用了不同的实体。相反，示例

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

是允许的，因为名称 x 从未在外层块中使用。

注意，不变含义规则仅适用于简单名称。同一标识符作为简单名称具有一种含义，而作为成员访问（§7.6.4）的右操作数具有另一种含义，这完全有效。例如：

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

上面的示例说明了在实例构造函数中将字段名称用作参数名称的常见模式。在该示例中，简单名称 x 和 y 引用参数，但这并不妨碍成员访问表达式 this.x 和 this.y 访问字段。

## 7.6.3 括号表达式

括号表达式由括在括号中的表达式组成。

```
parenthesized-expression:
    ( expression )
```

括号表达式的求值方式是求值括号内的表达式。如果括号内的表达式表示命名空间或类型，则发生编译时错误。否则，括号表达式的结果就是所包含表达式的求值结果。

## 7.6.4 成员访问

成员访问由主表达式、预定义类型或限定别名成员组成，后跟一个 `.` 标记，再后跟一个标识符，可选地后跟一个类型实参列表。

```
member-access:
  primary-expression . identifier type-argument-list_opt
  predefined-type . identifier type-argument-list_opt
  qualified-alias-member . identifier
```

```
predefined-type: one of
  bool byte char decimal double float int long
  object sbyte short string uint ulong ushort
```

限定别名成员产生式在 §9.7 中定义。

成员访问的形式为 E.I 或 E.I<A1, ..., Ak>，其中 E 是主表达式，I 是单个标识符，<A1, ..., Ak> 是可选的类型实参列表。未指定类型实参列表时，将 k 视为零。

主表达式类型为 dynamic 的成员访问采用动态绑定（§7.2.2）。在这种情况下，编译器将该成员访问分类为 dynamic 类型的属性访问。随后在运行时应用下面用于确定成员访问含义的规则，使用主表达式的运行时类型而不是编译时类型。如果该运行时分类导致方法组，则该成员访问必须是调用表达式的主表达式。

成员访问的求值和分类如下：

- 如果 k 为零，且 E 是命名空间，并且 E 包含名为 I 的嵌套命名空间，则结果就是该命名空间。
- 否则，如果 E 是命名空间，并且 E 包含具有名称 I 和 k 个类型形参的可访问类型，则结果是用给定类型实参构造的该类型。
- 如果 E 是预定义类型或分类为类型的主表达式，如果 E 不是类型形参，并且对 E 中具有 k 个类型形参的 I 进行成员查找（§7.4）产生匹配，则 E.I 的求值和分类如下：
  - 如果 I 标识一个类型，则结果是用给定类型实参构造的该类型。
  - 如果 I 标识一个或多个方法，则结果是没有关联实例表达式的方法组。如果指定了类型实参列表，则它用于调用泛型方法（§7.6.5.1）。
  - 如果 I 标识静态属性，则结果是没有关联实例表达式的属性访问。
  - 如果 I 标识静态字段：
    - 如果该字段是 readonly，并且引用发生在声明该字段的类或结构的静态构造函数之外，则结果是一个值，即 E 中静态字段 I 的值。
    - 否则，结果是一个变量，即 E 中的静态字段 I。
  - 如果 I 标识静态事件：
    - 如果引用发生在声明该事件的类或结构内，并且该事件声明时没有事件访问器声明（§10.8），则 E . I 的处理方式完全如同 I 是静态字段一样。
    - 否则，结果是没有关联实例表达式的事件访问。
  - 如果 I 标识常量，则结果是一个值，即该常量的值。
  - 如果 I 标识枚举成员，则结果是一个值，即该枚举成员的值。
  - 否则，E . I 是无效的成员引用，并发生编译时错误。
- 如果 E 是属性访问、索引器访问、变量或值，其类型为 T，并且对 T 中具有 k 个类型实参的 I 进行成员查找（§7.4）产生匹配，则 E . I 的求值和分类如下：
  - 首先，如果 E 是属性或索引器访问，则获取该属性或索引器访问的值（§7.1.1），并将 E 重新分类为值。
  - 如果 I 标识一个或多个方法，则结果是具有关联实例表达式 E 的方法组。如果指定了类型实参列表，则它用于调用泛型方法（§7.6.5.1）。
  - 如果 I 标识实例属性，则结果是具有关联实例表达式 E 的属性访问。
  - 如果 T 是类类型，并且 I 标识该类类型的实例字段：
    - 如果 E 的值为 null，则引发 System.NullReferenceException。
    - 否则，如果该字段是 readonly，并且引用发生在声明该字段的类的实例构造函数之外，则结果是一个值，即 E 所引用对象中字段 I 的值。
    - 否则，结果是一个变量，即 E 所引用对象中的字段 I。
  - 如果 T 是结构类型，并且 I 标识该结构类型的实例字段：
    - 如果 E 是值，或者该字段是 readonly，并且引用发生在声明该字段的结构的实例构造函数之外，则结果是一个值，即 E 给出的结构实例中字段 I 的值。
    - 否则，结果是一个变量，即 E 给出的结构实例中的字段 I。
  - 如果 I 标识实例事件：
    - 如果引用发生在声明该事件的类或结构内，并且该事件声明时没有事件访问器声明（§10.8），则 E . I 的处理方式完全如同 I 是实例字段一样。
    - 否则，结果是具有关联实例表达式 E 的事件访问。
- 否则，尝试将 E . I 作为扩展方法调用（§7.6.5.2）处理。如果失败，则 E . I 是无效的成员引用，并发生绑定期错误。

### 7.6.4.1 相同的简单名称和类型名称

在形式为 E . I 的成员访问中，如果 E 是单个标识符，并且 E 作为简单名称（§7.6.2）的含义是具有与 E 作为类型名称（§3.8）的含义相同类型的常量、字段、属性、局部变量或参数，则允许 E 的两种可能含义。E . I 的两种可能含义永远不会产生歧义，因为在这两种情况下，I 都必然是类型 E 的成员。换句话说，该规则只是允许访问 E 的静态成员和嵌套类型，而在其他情况下本会发生编译时错误。例如：

```
struct Color
{
    public static readonly Color White = new Color(...);
    public static readonly Color Black = new Color(...);
    public Color Complement() {...}
}
class A
{
    public Color Color;            // Field Color of type Color
    void F() {
        Color = Color.Black;       // References Color.Black static member
        Color = Color.Complement(); // Invokes Complement() on Color field
    }
    static void G() {
        Color c = Color.White;     // References Color.White static member
    }
}
```

在 A 类中，引用 Color 类型的那些 Color 标识符出现位置带下划线，而引用 Color 字段的那些出现位置不带下划线。

### 7.6.4.2 语法歧义

简单名称（§7.6.2）和成员访问（§7.6.4）的产生式可能导致表达式语法出现歧义。例如，语句：

```
F(G<A,B>(7));
```

可以被解释为对 F 的调用，带有两个实参，G < A 和 B > (7)。或者，它可以被解释为对 F 的调用，带有一个实参，该实参是对泛型方法 G 的调用，G 具有两个类型实参和一个普通实参。

如果某个标记序列可以（在上下文中）被解析为以类型实参列表（§4.4.1）结尾的简单名称（§7.6.2）、成员访问（§7.6.4）或指针成员访问（§18.5.2），则检查紧跟右尖括号 > 标记之后的标记。如果它是以下之一：

```
( ) ] : ; , . ? == != | ^
```

则保留该类型实参列表作为简单名称、成员访问或指针成员访问的一部分，并丢弃该标记序列的任何其他可能解析。否则，不将该类型实参列表视为简单名称、成员访问或指针成员访问的一部分，即使该标记序列没有其他可能解析。注意，在解析命名空间或类型名（§3.8）中的类型实参列表时，不应用这些规则。语句

```
F(G<A,B>(7));
```

根据该规则，将被解释为对 F 的调用，带有一个实参，该实参是对泛型方法 G 的调用，G 具有两个类型实参和一个普通实参。语句

```
F(G < A, B > 7);
F(G < A, B >> 7);
```

每个都将被解释为对 F 的调用，带有两个实参。语句

```
x = F < A > +y;
```

将被解释为小于运算符、大于运算符和一元加运算符，就好像该语句写成 x = (F < A >) (+y)，而不是带有类型实参列表的简单名称后跟二元加运算符。在语句

x = y is C<T> + z;

标记 C<T> 被解释为带有类型实参列表的命名空间或类型名。

## 7.6.5 调用表达式

调用表达式用于调用方法。

```
invocation-expression:
    primary-expression ( argument-list_opt )
```

如果至少满足以下条件之一，则调用表达式是动态绑定的（§7.2.2）：

- 主表达式的编译时类型为 dynamic。
- 可选实参列表中至少有一个实参的编译时类型为 dynamic，并且主表达式不具有委托类型。

在这种情况下，编译器将调用表达式归类为 dynamic 类型的值。然后，在运行时应用以下用于确定调用表达式含义的规则，并对那些编译时类型为 dynamic 的主表达式和实参使用运行时类型而不是编译时类型。如果主表达式不具有编译时类型 dynamic，则方法调用会经历 §7.5.4 所述的有限编译时检查。

调用表达式的主表达式必须是方法组或委托类型的值。如果主表达式是方法组，则调用表达式是方法调用（§7.6.5.1）。如果主表达式是委托类型的值，则调用表达式是委托调用（§7.6.5.3）。如果主表达式既不是方法组也不是委托类型的值，则发生绑定期错误。

可选实参列表（§7.5.1）为方法的参数提供值或变量引用。

调用表达式的求值结果分类如下：

- 如果调用表达式调用返回 void 的方法或委托，则结果为 nothing。分类为 nothing 的表达式仅允许在语句表达式（§8.6）的上下文中，或作为 lambda 表达式（§7.15）的主体。否则发生绑定期错误。
- 否则，结果是该方法或委托返回的类型的值。

### 7.6.5.1 方法调用

对于方法调用，调用表达式的主表达式必须是方法组。方法组标识要调用的单个方法，或从中选择要调用的特定方法的重载方法集合。在后一种情况下，确定要调用的特定方法基于实参列表中实参的类型所提供的上下文。

对形式为 M(A) 的方法调用的绑定期处理，其中 M 是方法组（可能包含类型实参列表），A 是可选实参列表，包括以下步骤：

- 构造该方法调用的候选方法集。对于与方法组 M 关联的每个方法 F：
  - 如果 F 是非泛型方法，则当以下条件成立时，F 是候选方法：
    - M 没有类型实参列表，并且
    - F 相对于 A 是适用的（§7.5.3.1）。
  - 如果 F 是泛型方法且 M 没有类型实参列表，则当以下条件成立时，F 是候选方法：
    - 类型推断（§7.5.2）成功，推断出该调用的类型实参列表，并且
    - 一旦将推断出的类型实参替换为相应的方法类型参数，F 的参数列表中的所有构造类型都满足其约束（§4.4.4），并且 F 的参数列表相对于 A 是适用的（§7.5.3.1）。
  - 如果 F 是泛型方法且 M 包含类型实参列表，则当以下条件成立时，F 是候选方法：
    - F 的方法类型参数数量与类型实参列表中提供的数量相同，并且
    - 一旦将类型实参替换为相应的方法类型参数，F 的参数列表中的所有构造类型都满足其约束（§4.4.4），并且 F 的参数列表相对于 A 是适用的（§7.5.3.1）。
- 候选方法集被缩减为仅包含来自最派生类型的方法：对于该集合中的每个方法 C . F（其中 C 是声明方法 F 的类型），从集合中移除在 C 的基类型中声明的所有方法。此外，如果 C 是除 object 之外的类类型，则从集合中移除在接口类型中声明的所有方法。（后一条规则仅当方法组是对某个类型参数进行成员查找的结果时才有效，该类型参数具有除 object 之外的有效基类和非空有效接口集。）
- 如果得到的候选方法集为空，则放弃按以下步骤继续处理，并改为尝试将该调用作为扩展方法调用处理（§7.6.5.2）。如果这也失败，则不存在适用的方法，并发生绑定期错误。
- 使用 §7.5.3 的重载决策规则标识候选方法集中的最佳方法。如果无法标识单个最佳方法，则该方法调用有歧义，并发生绑定期错误。执行重载决策时，在将类型实参（提供的或推断的）替换为相应的方法类型参数之后，才考虑泛型方法的参数。
- 对所选最佳方法执行最终验证：
  - 在方法组的上下文中验证该方法：如果最佳方法是静态方法，则方法组必须来自简单名称或通过类型进行的成员访问。如果最佳方法是实例方法，则方法组必须来自简单名称、通过变量或值进行的成员访问，或 base 访问。如果这两个要求都不成立，则发生绑定期错误。
  - 如果最佳方法是泛型方法，则根据泛型方法上声明的约束（§4.4.4）检查类型实参（提供的或推断的）。如果任何类型实参不满足类型参数上的相应约束，则发生绑定期错误。

一旦在绑定期通过上述步骤选择并验证了方法，实际运行时调用将按照 §7.5.4 中描述的函数成员调用规则处理。

上述解析规则的直观效果如下：要定位方法调用所调用的特定方法，从方法调用所指示的类型开始，沿继承链向上查找，直到找到至少一个适用的、可访问的、非 override 的方法声明。然后对该类型中声明的适用的、可访问的、非 override 的方法集合执行类型推断和重载决策，并调用由此选择的方法。如果未找到方法，则改为尝试将该调用作为扩展方法调用处理。

### 7.6.5.2 扩展方法调用

在具有下列形式之一的方法调用（§7.6.5.1）中

```
expr . identifier ( )
expr . identifier ( args )
expr . identifier < typeargs > ( )
expr . identifier < typeargs > ( args )
```

如果调用的常规处理未找到适用方法，则尝试将该构造作为扩展方法调用处理。如果 expr 或任何 args 具有编译时类型 dynamic，则扩展方法不适用。

目标是找到最佳类型名 C，以便可以执行相应的静态方法调用：

C . identifier ( expr )
C . identifier ( expr , args )
C . identifier < typeargs > ( expr )
C . identifier < typeargs > ( expr , args )

如果满足以下条件，则扩展方法 C_i . M_j 是合格的：

- C_i 是非泛型、非嵌套类
- M_j 的名称是 identifier
- 当如上所示作为静态方法应用于实参时，M_j 是可访问且适用的
- 存在从 expr 到 M_j 第一个参数类型的隐式标识转换、引用转换或装箱转换。

对 C 的搜索过程如下：

- 从最接近的封闭命名空间声明开始，继续处理每个封闭命名空间声明，直到包含编译单元，依次尝试查找候选扩展方法集：
  - 如果给定命名空间或编译单元直接包含带有合格扩展方法 M_j 的非泛型类型声明 C_i，则这些扩展方法的集合就是候选集。
  - 如果给定命名空间或编译单元中通过 using namespace 指令导入的命名空间直接包含带有合格扩展方法 M_j 的非泛型类型声明 C_i，则这些扩展方法的集合就是候选集。
- 如果在任何封闭命名空间声明或编译单元中都未找到候选集，则发生编译时错误。
- 否则，按（§7.5.3）所述对候选集应用重载决策。如果未找到单个最佳方法，则发生编译时错误。
- C 是将最佳方法声明为扩展方法的类型。

然后以 C 为目标，将该方法调用作为静态方法调用处理（§7.5.4）。

前面的规则意味着：实例方法优先于扩展方法；内部命名空间声明中可用的扩展方法优先于外部命名空间声明中可用的扩展方法；直接在命名空间中声明的扩展方法优先于通过 using namespace 指令导入到同一命名空间中的扩展方法。例如：

```
public static class E
{
    public static void F(this object obj, int i) { }
    public static void F(this object obj, string s) { }
}
class A { }
```




```
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
        a.F(1);      // E.F(object, int)
        a.F("hello"); // E.F(object, string)
        b.F(1);      // B.F(int)
        b.F("hello"); // E.F(object, string)
        c.F(1);      // C.F(object)
        c.F("hello"); // C.F(object)
    }
}
```

在示例中，B 的方法优先于第一个扩展方法，C 的方法优先于两个扩展方法。

```
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

```
E.F(1)
D.G(2)
C.H(3)
```

D.G 优先于 C.G，E.F 优先于 D.F 和 C.F 两者。

## 7.6.5.3 委托调用

对于委托调用，调用表达式的主表达式必须是委托类型的值。此外，将委托类型视为具有与委托类型相同的参数列表的函数成员，委托类型必须相对于调用表达式的参数列表适用 (§7.5.3.1)。

形式为 D(A) 的委托调用的运行时处理，其中 D 是委托类型的主表达式，A 是可选的参数列表，包括以下步骤：

- D 被求值。如果此求值导致异常，则不执行后续步骤。
- 检查 D 的值是否有效。如果 D 的值为 null，则抛出 System.NullReferenceException 且不执行后续步骤。
- 否则，D 是对委托实例的引用。在委托的调用列表中的每个可调用实体上执行函数成员调用 (§7.5.4)。对于由实例和实例方法组成的可调用实体，调用的实例是可调用实体中包含的实例。

## 7.6.6 元素访问

元素访问由 primary-no-array-creation-expression、后跟 “[” 标记、后跟 argument-list、后跟 “]” 标记组成。argument-list 由一个或多个由逗号分隔的参数组成。

```
element-access:
    primary-no-array-creation-expression [ argument-list ]
```

元素访问的参数列表不允许包含 ref 或 out 参数。

如果满足以下条件之一，则元素访问是动态绑定的 (§7.2.2)：

- primary-no-array-creation-expression 的编译时类型为 dynamic。
- argument-list 的至少一个表达式的编译时类型为 dynamic 且 primary-no-array-creation-expression 没有数组类型。

形式为 P[A] 的数组访问的运行时处理，其中 P 是数组类型的 primary-no-array-creation-expression，A 是参数列表，包括以下步骤：

- P 被求值。如果此求值导致异常，则不执行后续步骤。
- 参数列表的索引表达式按从左到右的顺序求值。求值每个索引表达式后，执行到以下类型之一的隐式转换 (§6.1)：int、uint、long、ulong。选择列表中存在隐式转换的第一个类型。例如，如果索引表达式的类型为 short，则执行到 int 的隐式转换，因为 short 到 int 和 short 到 long 都存在隐式转换。如果索引表达式的求值或随后的隐式转换导致异常，则不求值任何进一步的索引表达式且不执行后续步骤。
- 检查 P 的值是否有效。如果 P 的值为 null，则抛出 System.NullReferenceException 且不执行后续步骤。
- 检查参数列表中每个表达式的值是否在 P 引用的数组实例的每个维度的实际边界内。如果一个或多个值超出范围，则抛出 System.IndexOutOfRangeException 且不执行后续步骤。
- 计算由索引表达式(s)给出的数组元素的位置，此位置成为数组访问的结果。

### 7.6.6.2 索引器访问

对于索引器访问，元素访问的 primary-no-array-creation-expression 必须是类、结构或接口类型变量或值，并且该类型必须实现一个或多个相对于元素访问的参数列表适用的索引器。

形式为 P[A] 的索引器访问的绑定时处理，其中 P 是类、结构或接口类型 T 的 primary-no-array-creation-expression，A 是参数列表，包括以下步骤：

- 构造 T 提供的索引器集合。该集合由在 T 或 T 的基类型中声明且不是重写声明并且在当前上下文中可访问 (§3.5) 的所有索引器组成。
- 将集合缩小为适用且未被其他索引器隐藏的索引器。对集合中每个索引器 S.I 应用以下规则，其中 S 是声明索引器 I 的类型：
  - 如果 I 相对于 A 不适用 (§7.5.3.1)，则从集合中移除 I。
  - 如果 I 相对于 A 适用 (§7.5.3.1)，则从集合中移除在 S 的基类型中声明的所有索引器。
  - 如果 I 相对于 A 适用 (§7.5.3.1) 且 S 是 object 以外的类类型，则从集合中移除在接口中声明的所有索引器。
- 如果候选索引器集合为空，则不存在适用的索引器，并发生绑定时错误。
- 使用 §7.5.3 的重载解析规则识别候选索引器集合的最佳索引器。如果无法识别单个最佳索引器，则索引器访问不明确，并发生绑定时错误。
- 参数列表的索引表达式按从左到右的顺序求值。处理索引器访问的结果被归类为索引器访问表达式。索引器访问表达式引用上面步骤中确定的索引器，并具有关联的实例表达式 P 和关联的参数列表 A。

根据其使用的上下文，索引器访问会导致调用索引器的 get 访问器或 set 访问器。如果索引器访问是赋值的目标，则调用 set 访问器以分配新值 (§7.17.1)。在所有其他情况下，调用 get 访问器以获取当前值 (§7.1.1)。

## 7.6.7 this 访问

this-access 由保留字 this 组成。

```
this-access:
    this
```

this-access 仅允许在实例构造函数、实例方法或实例访问器的块中。它具有以下含义之一：

- 当 this 在类实例构造函数的 primary-expression 中使用时，它被归类为值。该值类型是使用该用法发生的类的实例类型 (§10.3.1)，并且该值是对正在构造的对象的引用。
- 当 this 在类实例方法或实例访问器的 primary-expression 中使用时，它被归类为值。该值类型是使用该用法发生的类的实例类型 (§10.3.1)，并且该值是对调用该方法或访问器的对象的引用。
- 当 this 在结构实例构造函数的 primary-expression 中使用时，它被归类为变量。该变量类型是使用该用法发生的结构的实例类型 (§10.3.1)，并且该变量表示正在构造的结构。结构实例构造函数的 this 变量的行为与结构类型的 out 参数完全相同——特别是，这意味着该变量必须在实例构造函数的每个执行路径中都被明确赋值。
- 当 this 在结构实例方法或实例访问器的 primary-expression 中使用时，它被归类为变量。该变量类型是使用该用法发生的结构的实例类型 (§10.3.1)，并且该变量表示使用该用法的结构。
  - 如果该方法或访问器不是迭代器 (§10.14)，则 this 变量表示调用该方法或访问器的结构，并行为与结构类型的 ref 参数完全相同。
  - 如果该方法或访问器是迭代器，则 this 变量表示调用该方法或访问器的结构的副本，并行为与值参数完全相同。

在上述列出的上下文之外在 primary-expression 中使用 this 是编译时错误。特别是，不能在静态方法、静态属性访问器或字段声明的变量初始化器中引用 this。

## 7.6.8 base 访问

base-access 由保留字 base 后跟 “.” 标记和标识符或用方括号括起的参数列表组成：

```
base-access:
    base . identifier
    base [ argument-list ]
```

base-access 用于访问被当前类或结构中同名成员隐藏的基类成员。base-access 仅允许在实例构造函数、实例方法或实例访问器的块中。当 base.I 出现在类或结构中时，I 必须表示该类或结构基类的成员。同样，当 base[E] 出现在类中时，基类中必须存在适用的索引器。

在绑定时，形式为 base.I 和 base[E] 的 base-access 表达式的求值方式就好像它们被写成 ((B)this).I 和 ((B)this)[E]，其中 B 是包含该

构造发生。因此，base.I 和 base[E] 对应于 this.I 和 this[E]，只是 this 被视为基类的实例。

当 base-access 引用一个虚函数成员（方法、属性或索引器）时，在运行时确定要调用哪个函数成员（§7.5.4）的过程会发生变化。被调用的函数成员是通过查找相对于 B（而不是相对于 this 的运行时类型，如非 base 访问的通常情况）的函数成员的最派生实现（§10.6.3）来确定的。因此，在虚函数成员的重写中，可以使用 base-access 来调用该函数成员的继承实现。如果 base-access 引用的函数成员是抽象的，则会发生绑定时错误。

## 7.6.9 后缀递增和递减运算符

```
post-increment-expression:
    primary-expression ++
post-decrement-expression:
    primary-expression --
```

后缀递增或递减操作的运算对象必须是被归类为变量、属性访问或索引器访问的表达式。操作的结果是与运算对象相同类型的值。

如果 primary-expression 的编译时类型为 dynamic，则运算符是动态绑定的（§7.2.2），post-increment-expression 或 post-decrement-expression 的编译时类型为 dynamic，并且以下规则使用 primary-expression 的运行时类型在运行时应用。

如果后缀递增或递减操作的运算对象是属性或索引器访问，则该属性或索引器必须同时具有 get 和 set 访问器。如果不是这样，则会发生绑定时错误。

应用一元运算符重载解析（§7.3.3）来选择特定的运算符实现。预定义的 ++ 和 -- 运算符存在于以下类型：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 以及任何枚举类型。预定义的 ++ 运算符返回将 1 加到运算对象后得到的值，而预定义的 -- 运算符返回从运算对象减去 1 后得到的值。在检查上下文中，如果此加法或减法的结果超出结果类型的范围并且结果类型是整型或枚举类型，则会抛出 System.OverflowException。

形式为 x++ 或 x-- 的后缀递增或递减操作的运行时处理包括以下步骤：

- 如果 x 被归类为变量：
  - x 被求值以生成变量。
  - x 的值被保存。
  - 所选运算符以 x 的保存值作为其参数被调用。
  - 运算符返回的值存储在 x 的求值给出的位置中。
  - x 的保存值成为操作的结果。
- 如果 x 被归类为属性或索引器访问：
  - 与 x 关联的实例表达式（如果 x 不是 static）以及参数列表（如果 x 是索引器访问）被求值，其结果用于后续的 get 和 set 访问器调用。
  - x 的 get 访问器被调用并保存返回的值。
  - 所选运算符以 x 的保存值作为其参数被调用。
  - x 的 set 访问器以运算符返回的值作为其值参数被调用。
- x 的保存值成为操作的结果。

++ 和 -- 运算符也支持前缀表示法（§7.7.5）。通常，x++ 或 x-- 的结果是操作前 x 的值，而 ++x 或 --x 的结果是操作后 x 的值。在任何情况下，操作后 x 本身的值都相同。

operator ++ 或 operator -- 实现可以使用后缀或前缀表示法调用。不可能为这两种表示法拥有单独的运算符实现。

## 7.6.10 new 运算符

new 运算符用于创建类型的新的实例。

new 表达式有三种形式：

- 对象创建表达式用于创建类类型和值类型的新的实例。
- 数组创建表达式用于创建数组类型的新的实例。
- 委托创建表达式用于创建委托类型的新的实例。

new 运算符意味着创建类型的实例，但不一定意味着动态分配内存。特别是，值类型的实例不需要超出其所在变量之外的额外内存，并且在使用 new 创建值类型的实例时不会发生动态分配。

### 7.6.10.1 对象创建表达式

object-creation-expression 用于创建类类型或值类型的新实例。

```
object-creation-expression:
    new type ( argument-list_opt ) object-or-collection-initializer_opt
    new type object-or-collection-initializer

object-or-collection-initializer:
    object-initializer
    collection-initializer
```

object-creation-expression 的类型必须是类类型、值类型或类型参数。类型不能是抽象类类型。

可选的 argument-list（§7.5.1）仅在类型为类类型或结构类型时才允许。

对象创建表达式可以省略构造函数参数列表和包围的圆括号，前提是它包含对象初始值设定项或集合初始值设定项。省略构造函数参数列表和包围的圆括号等同于指定空参数列表。

包含对象初始值设定项或集合初始值设定项的对象创建表达式的处理包括首先处理实例构造函数，然后处理对象初始值设定项（§7.6.10.2）或集合初始值设定项（§7.6.10.3）指定的成员或元素初始化。

如果可选 argument-list 中的任何参数的编译时类型为 dynamic，则 object-creation-expression 是动态绑定的（§7.2.2），并且以下规则使用 argument-list 中编译时类型为 dynamic 的那些参数的运行时类型在运行时应用。然而，对象创建会进行如 §7.5.4 中所述的有限编译时检查。

形式为 new T(A) 的 object-creation-expression 的绑定时处理，其中 T 是类类型或值类型，A 是可选参数列表，包括以下步骤：

- 如果 T 是值类型且 A 不存在：
  - object-creation-expression 是默认构造函数调用。object-creation-expression 的结果是类型 T 的值，即 §4.1.1 中定义的 T 的默认值。
- 否则，如果 T 是类型参数且 A 不存在：
  - 如果未为 T 指定值类型约束或构造函数约束（§10.1.5），则会发生绑定时错误。
  - object-creation-expression 的结果是类型参数已被绑定的运行时类型的值，即调用该类型的默认构造函数的結果。运行时类型可能是引用类型或值类型。
- 否则，如果 T 是类类型或结构类型：
  - 如果 T 是抽象类类型，则会发生编译时错误。
  - 要调用的实例构造函数是使用 §7.5.3 的重载解析规则确定的。候选实例构造函数的集合由 T 中声明的所有可访问实例构造函数组成，这些构造函数相对于 A 是适用的（§7.5.3.1）。如果候选实例构造函数的集合为空，或者无法识别出唯一的最佳实例构造函数，则会发生绑定时错误。
  - object-creation-expression 的结果是类型 T 的值，即通过调用上述步骤中确定的实例构造函数产生的值。
- 否则，object-creation-expression 无效，并且会发生绑定时错误。

即使 object-creation-expression 是动态绑定的，其编译时类型仍然是 T。

形式为 new T(A) 的 object-creation-expression 的运行时处理，其中 T 是类类型或结构类型，A 是可选参数列表，包括以下步骤：

- 如果 T 是类类型：
  - 分配类 T 的新实例。如果没有足够的内存来分配新实例，则会抛出 System.OutOfMemoryException 并且不再执行后续步骤。
  - 新实例的所有字段都初始化为其默认值（§5.2）。
  - 实例构造函数根据函数成员调用的规则（§7.5.4）被调用。对新分配实例的引用会自动传递给实例构造函数，并且可以在该构造函数内部将实例作为 this 访问。
- 如果 T 是结构类型：
  - 通过分配临时局部变量来创建类型 T 的实例。由于结构类型的实例构造函数必须为正在创建的实例的每个字段明确赋值，因此不需要对临时变量进行初始化。
  - 实例构造函数根据函数成员调用的规则（§7.5.4）被调用。对新分配实例的引用会自动传递给实例构造函数，并且可以在该构造函数内部将实例作为 this 访问。

### 7.6.10.2 对象初始值设定项

对象初始值设定项指定对象的零个或多个字段或属性的值。

```
object-initializer:
    { member-initializer-list_opt }
    { member-initializer-list , }
```



## C# 语言规范

```
member-initializer-list:
    member-initializer
    member-initializer-list , member-initializer
member-initializer
    identifier = initializer-value
initializer-value:
    expression
    object-or-collection-initializer
```

对象初始值设定项由一系列成员初始值设定项组成，这些成员初始值设定项由 { 和 } 标记括起来并用逗号分隔。每个成员初始值设定项必须指定正在初始化的对象的一个可访问字段或属性，后跟等号以及一个表达式、对象初始值设定项或集合初始值设定项。若对象初始值设定项为同一字段或属性包含多个成员初始值设定项，则会导致错误。对象初始值设定项无法引用它正在初始化的新创建对象。

在等号后指定表达式的成员初始值设定项，其处理方式与对该字段或属性的赋值（§7.17.1）相同。

在等号后指定对象初始值设定项的成员初始值设定项是嵌套对象初始值设定项，即对嵌入对象的初始化。嵌套对象初始值设定项中的赋值不会向该字段或属性赋予新值，而是被视为对该字段或属性成员的赋值。嵌套对象初始值设定项不能应用于具有值类型的属性，也不能应用于具有值类型的只读字段。

在等号后指定集合初始值设定项的成员初始值设定项是对嵌入集合的初始化。该初始值设定项不会向该字段或属性赋予新集合，而是将初始值设定项中给定的元素添加到该字段或属性引用的集合中。该字段或属性必须是满足 §7.6.10.3 中指定要求的集合类型。

以下类表示一个具有两个坐标的点：

```
public class Point
{
    int x, y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

可按如下方式创建并初始化 Point 的实例：

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

其中 __a 是一个在其他情况下不可见且不可访问的临时变量。以下类表示一个矩形：

```
public class Rectangle
{
    Point p1, p2;
    public Point P1 { get { return p1; } set { p1 = value; } }
    public Point P2 { get { return p2; } set { p2 = value; } }
}
```

可按如下方式创建并初始化 Rectangle 的实例：

```csharp
Rectangle r = new Rectangle {
    P1 = new Point { X = 0, Y = 1 },
    P2 = new Point { X = 2, Y = 3 }
};
```

其效果与以下代码相同：

```csharp
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

其中 __r、__p1 和 __p2 是在其他情况下不可见且不可访问的临时变量。

如果 Rectangle 的构造函数分配两个嵌入的 Point 实例

```csharp
public class Rectangle
{
    Point p1 = new Point();
    Point p2 = new Point();
    public Point P1 { get { return p1; } }
    public Point P2 { get { return p2; } }
}
```

则可以使用以下构造来初始化这些嵌入的 Point 实例，而不是赋予新实例：

```csharp
Rectangle r = new Rectangle {
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```

其效果与以下代码相同：

```csharp
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

## 7.6.10.3 集合初始值设定项

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
```

```
expression-list:
  expression
  expression-list , expression
```

集合初始值设定项由一系列元素初始值设定项组成，这些元素初始值设定项由 { 和 } 标记括起来并用逗号分隔。每个元素初始值设定项指定要添加到正在初始化的集合对象中的一个元素，并由一个表达式列表组成，该表达式列表由 { 和 } 标记括起来并用逗号分隔。单表达式元素初始值设定项可以不带花括号书写，但此时不能是赋值表达式，以避免与成员初始值设定项产生歧义。非赋值表达式产生式在 §7.18 中定义。

以下是一个包含集合初始值设定项的对象创建表达式示例：

```
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

应用集合初始值设定项的集合对象必须是实现 System.Collections.IEnumerable 的类型，否则会发生编译时错误。对于按顺序指定的每个元素，集合初始值设定项使用元素初始值设定项的表达式列表作为参数列表，对目标对象调用 Add 方法，并对每次调用应用常规重载决策。因此，集合对象必须为每个元素初始值设定项包含一个适用的 Add 方法。

以下类表示一个包含姓名和电话号码列表的联系人：

```
public class Contact
{
    string name;
    List<string> phoneNumbers = new List<string>();
    public string Name { get { return name; } set { name = value; } }
    public List<string> PhoneNumbers { get { return phoneNumbers; } }
}
```

可按如下方式创建并初始化 List<Contact>：

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

其效果与以下代码相同：

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

其中 __clist、__c1 和 __c2 是在其他情况下不可见且不可访问的临时变量。

## 7.6.10.4 数组创建表达式

数组创建表达式用于创建数组类型的新实例。

```
array-creation-expression:
    new non-array-type [ expression-list ] rank-specifiers_opt array-initializer_opt
    new array-type array-initializer
    new rank-specifier array-initializer
```

第一种形式的数组创建表达式分配一个数组实例，其类型由从表达式列表中删除各个表达式后得到。例如，数组创建表达式 new int[10, 20] 生成一个类型为 int[,] 的数组实例，而数组创建表达式 new int[10] 生成一个类型为 int[][] 的数组。表达式列表中的每个表达式必须具有类型 int、uint、long 或 ulong，或者可隐式转换为这些类型中的一个或多个。每个表达式的值确定新分配的数组实例中对应维度的长度。由于数组维度的长度必须为非负，因此表达式列表中包含值为负的常量表达式会导致编译时错误。

除在不安全上下文（§18.1）中之外，数组的布局未作规定。

如果第一种形式的数组创建表达式包含数组初始值设定项，则表达式列表中的每个表达式必须是常量，并且表达式列表指定的秩和维度长度必须与数组初始值设定项的秩和维度长度匹配。

在第二种或第三种形式的数组创建表达式中，指定的数组类型或秩说明符的秩必须与数组初始值设定项的秩匹配。各个维度长度从数组初始值设定项中每个对应嵌套级别的元素数量推断。因此，表达式

```
new int[,] {{0, 1}, {2, 3}, {4, 5}}
```

完全对应于

```
new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}
```

第三种形式的数组创建表达式称为隐式类型化数组创建表达式。它与第二种形式类似，不同之处在于数组的元素类型未显式给出，而是确定为数组初始值设定项中表达式集合的最佳通用类型（§7.5.2.14）。对于多维数组，即秩说明符包含至少一个逗号的数组，该集合包含嵌套数组初始值设定项中找到的所有表达式。

数组初始值设定项在 §12.6 中进一步描述。

计算数组创建表达式的结果被归类为值，即对新分配的数组实例的引用。数组创建表达式的运行时处理包括以下步骤：

- 按从左到右的顺序计算表达式列表中的维度长度表达式。在计算每个表达式之后，执行到以下类型之一的隐式转换（§6.1）：int、uint、long、ulong。选择此列表中存在隐式转换的第一种类型。如果表达式计算或随后的隐式转换导致异常，则不再计算其他表达式，也不执行后续步骤。
- 按如下方式验证维度长度的计算值。如果一个或多个值小于零，则引发 System.OverflowException，并且不执行后续步骤。
- 分配具有给定维度长度的数组实例。如果没有足够内存可用于分配新实例，则引发 System.OutOfMemoryException，并且不执行后续步骤。
- 新数组实例的所有元素都初始化为其默认值（§5.2）。
- 如果数组创建表达式包含数组初始值设定项，则计算数组初始值设定项中的每个表达式，并将其赋给对应的数组元素。求值和赋值按表达式在数组初始值设定项中写入的顺序执行——换句话说，元素按


按递增索引顺序，最右边的维度先递增。如果对给定表达式的求值或随后对相应数组元素的赋值导致异常，则不再初始化后续元素（因此剩余元素将具有其默认值）。

数组创建表达式允许实例化一个元素类型为数组类型的数组，但此类数组的元素必须手动初始化。例如，语句

```
int[][] a = new int[100][];
```

创建一个具有 100 个类型为 int[] 元素的单维数组。每个元素的初始值为 null。同一数组创建表达式不可能同时实例化子数组，并且语句

```
int[][] a = new int[100][5];    // Error
```

会导致编译时错误。子数组的实例化必须改为手动执行，如下所示

```
int[][] a = new int[100][];
for (int i = 0; i < 100; i++) a[i] = new int[5];
```

当数组的数组具有“矩形”形状时，即当子数组都具有相同的长度时，使用多维数组更高效。在上面的示例中，数组的数组的实例化创建了 101 个对象——一个外部数组和 100 个子数组。相比之下，

```
int[,] a = new int[100, 5];
```

只创建单个对象，即二维数组，并在单个语句中完成分配。

以下是对隐式类型数组创建表达式的示例：

```
var a = new[] { 1, 10, 100, 1000 };          // int[]
var b = new[] { 1, 1.5, 2, 2.5 };             // double[]
var c = new[,] { { "hello", null }, { "world", "!" } };  // string[,]
var d = new[] { 1, "one", 2, "two" };         // Error
```

最后一个表达式导致编译时错误，因为 int 和 string 彼此都不能隐式转换，因此没有最佳公共类型。在这种情况下必须使用显式类型数组创建表达式，例如指定类型为 object[]。或者，可以将其中一个元素强制转换为公共基类型，这将成为推断的元素类型。

隐式类型数组创建表达式可以与匿名对象初始值设定项 (§7.6.10.6) 结合使用以创建匿名类型的数据结构。例如：

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

### 7.6.10.5 委托创建表达式

delegate-creation-expression 用于创建 delegate-type 的新实例。

```
delegate-creation-expression:
    new delegate-type ( expression )
```

委托创建表达式的参数必须是方法组、匿名函数或编译时类型为 dynamic 或 delegate-type 的值。如果参数是方法组，则它标识该方法，并且对于实例方法，标识创建委托的对象。如果参数是匿名函数，则它直接定义委托目标的参数和方法体。如果参数是值，则它标识要创建副本的委托实例。

如果表达式的编译时类型为 dynamic，则 delegate-creation-expression 动态绑定 (§7.2.2)，并且以下规则在运行时使用表达式的运行时类型应用。否则规则在编译时应用。

形式为 new D(E) 的 delegate-creation-expression 的绑定时处理，其中 D 是 delegate-type，E 是表达式，由以下步骤组成：

- 如果 E 是方法组，则委托创建表达式的处理方式与从 E 到 D 的方法组转换 (§6.6) 相同。
- 如果 E 是匿名函数，则委托创建表达式的处理方式与从 E 到 D 的匿名函数转换 (§6.5) 相同。
- 如果 E 是值，则 E 必须与 D 兼容 (§15.1)，结果是对类型为 D 的新创建委托的引用，该委托引用与 E 相同的调用列表。如果 E 与 D 不兼容，则会发生编译时错误。

形式为 new D(E) 的 delegate-creation-expression 的运行时处理，其中 D 是 delegate-type，E 是表达式，由以下步骤组成：

- 如果 E 是方法组，则委托创建表达式被评估为从 E 到 D 的方法组转换 (§6.6)。
- 如果 E 是匿名函数，则委托创建被评估为从 E 到 D 的匿名函数转换 (§6.5)。
- 如果 E 是 delegate-type 的值：
  - 对 E 进行求值。如果此求值导致异常，则不执行后续步骤。
  - 如果 E 的值为 null，则抛出 System.NullReferenceException 并且不执行后续步骤。
  - 分配委托类型 D 的新实例。如果没有足够的内存来分配新实例，则抛出 System.OutOfMemoryException 并且不执行后续步骤。
  - 使用委托实例 E 给出的调用列表初始化新的委托实例。

委托的调用列表在委托实例化时确定，然后在委托整个生命周期内保持不变。换句话说，一旦委托被创建，就不可能更改其目标可调用实体。当两个委托组合或一个从另一个中移除时 (§15.1)，会产生新的委托；没有任何现有委托的内容被更改。

不可能创建引用属性、索引器、用户定义运算符、实例构造函数、析构函数或静态构造函数的委托。

如上所述，当从方法组创建委托时，委托的形式参数列表和返回类型决定选择哪个重载方法。在示例中

```
delegate double DoubleFunc(double x);
class A
{
    DoubleFunc f = new DoubleFunc(Square);
    static float Square(float x) {
        return x * x;
    }
}

static double Square(double x) {
    return x * x;
}
}
```

A. f 字段被初始化为引用第二个 Square 方法的委托，因为该方法与 DoubleFunc 的形式参数列表和返回类型完全匹配。如果没有第二个 Square 方法，则会发生编译时错误。

### 7.6.10.6 匿名对象创建表达式

anonymous-object-creation-expression 用于创建匿名类型对象。

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

匿名对象初始值设定项声明匿名类型并返回该类型的实例。匿名类型是直接继承自 object 的无名类类型。匿名类型的成员是从用于创建类型实例的匿名对象初始值设定项推断的一系列只读属性。具体来说，形式为

```
new { p1 = e1 , p2 = e2 , ... pn = en }
```

的匿名对象初始值设定项声明形式为

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

    public override bool Equals(object o) { ... }
    public override int GetHashCode() { ... }
}
```

的匿名类型，其中每个 T_i 是对应表达式 e_i 的类型。member-declarator 中使用的表达式必须具有类型。因此，member-declarator 中的表达式为 null 或匿名函数是编译时错误。表达式具有不安全类型也是编译时错误。

匿名类型的名称由编译器自动生成，不能在程序文本中引用。

在同一程序中，指定相同名称和编译时类型且顺序相同的属性序列的两个匿名对象初始值设定项将产生同一匿名类型的实例。

在示例中

```
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```

最后一行的赋值是允许的，因为 p1 和 p2 是同一匿名类型。

匿名类型上的 Equals 和 GetHashCode 方法重写了从 object 继承的方法，并以属性的 Equals 和 GetHashCode 为定义，因此同一匿名类型的两个实例相等当且仅当它们的所有属性都相等。

成员声明符可以缩写为简单名称 (§7.5.2)、成员访问 (§7.5.4) 或基访问 (§7.6.8)。这称为投影初始值设定项，是对具有相同名称的属性的声明和赋值的简写。具体来说，形式为

```
identifier                    expr . identifier
```

的成员声明符分别精确等同于以下内容：

```
identifier = identifier       identifier = expr . identifier
```

因此，在投影初始值设定项中，标识符同时选择值和要将值分配到的字段或属性。直观地说，投影初始值设定项不仅投影值，还投影值的名称。

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

generic-dimension-specifier:
    < commas_opt >

commas:
    ,
    commas ,
```

typeof-expression 的第一种形式由 typeof 关键字后跟带括号的类型组成。此类表达式的结果是所指示类型的 System.Type 对象。只有一种


任何给定类型的 System.Type 对象。这意味着对于类型 T，typeof(T) == typeof(T) 始终为 true。该类型不能是动态类型。

typeof 表达式的第二种形式由 typeof 关键字后跟带括号的未绑定类型名称组成。未绑定类型名称与类型名称（§3.8）非常相似，不同之处在于未绑定类型名称包含泛型维度说明符，而类型名称包含类型实参列表。当 typeof 表达式的操作数是同时满足未绑定类型名称和类型名称语法的标记序列时，即当它既不包含泛型维度说明符也不包含类型实参列表时，该标记序列被视为类型名称。未绑定类型名称的含义按如下方式确定：

- 将标记序列转换为类型名称：把每个泛型维度说明符替换为一个类型实参列表，该列表具有相同数量的逗号，并以关键字 object 作为每个类型实参。
- 对得到的类型名称求值，同时忽略所有类型参数约束。
- 未绑定类型名称解析为与所得构造类型（§4.4.3）关联的未绑定泛型类型。

typeof 表达式的结果是所得未绑定泛型类型的 System.Type 对象。

typeof 表达式的第三种形式由 typeof 关键字后跟带括号的 void 关键字组成。这种形式的表达式的结果是表示不存在类型的 System.Type 对象。typeof(void) 返回的类型对象与为任何类型返回的类型对象不同。这个特殊类型对象在允许对语言中的方法进行反射的类库中很有用；在这些类库中，那些方法希望有一种方式用 System.Type 的实例来表示任何方法的返回类型，包括 void 方法。

typeof 运算符可用于类型参数。结果是绑定到该类型参数的运行时类型的 System.Type 对象。typeof 运算符也可用于构造类型或未绑定泛型类型（§4.4.3）。未绑定泛型类型的 System.Type 对象与实例类型的 System.Type 对象不同。实例类型在运行时始终是封闭构造类型，因此其 System.Type 对象取决于所使用的运行时类型实参，而未绑定泛型类型没有类型实参。

示例

```csharp
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
            typeof(X<X<T>>),
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

注意，int 和 System.Int32 是同一类型。

另请注意，typeof(X<>) 的结果不依赖于类型实参，而 typeof(X<T>) 的结果则依赖。

### 7.6.12 checked 和 unchecked 运算符

checked 和 unchecked 运算符用于控制整型算术运算和转换的溢出检查上下文。

```
checked-expression:
    checked ( expression )
unchecked-expression:
    unchecked ( expression )
```

checked 运算符在 checked 上下文中计算所包含的表达式，而 unchecked 运算符在 unchecked 上下文中计算所包含的表达式。checked 表达式或 unchecked 表达式与带括号的表达式（§7.6.3）完全对应，不同之处在于所包含的表达式在给定的溢出检查上下文中求值。

溢出检查上下文也可通过 checked 和 unchecked 语句（§8.11）控制。

以下操作受 checked 和 unchecked 运算符及语句建立的溢出检查上下文影响：

- 预定义的 ++ 和 -- 一元运算符（§7.6.9 和 §7.7.5），当操作数为整型时。
- 预定义的 - 一元运算符（§7.7.2），当操作数为整型时。
- 预定义的 +、-、* 和 / 二元运算符（§7.8），当两个操作数均为整型时。
- 从一个整型到另一个整型，或从 float 或 double 到整型的显式数值转换（§6.2.1）。

当上述操作之一产生的结果太大，无法在目标类型中表示时，执行该操作的上下文控制最终行为：

- 在 checked 上下文中，如果该操作是常量表达式（§7.19），则发生编译时错误。否则，当该操作在运行时执行时，将抛出 System.OverflowException。
- 在 unchecked 上下文中，结果通过丢弃任何不适合目标类型的高序位来截断。

C# 语言规范

对于未包含在任何 checked 或 unchecked 运算符或语句中的非常量表达式（在运行时求值的表达式），默认溢出检查上下文为 unchecked，除非外部因素（如编译器开关和执行环境配置）要求进行 checked 求值。

对于常量表达式（可在编译时完全求值的表达式），默认溢出检查上下文始终为 checked。除非常量表达式被显式置于 unchecked 上下文中，否则在表达式的编译时求值期间发生的溢出始终会导致编译时错误。

匿名函数的主体不受该匿名函数所在 checked 或 unchecked 上下文的影响。

在示例

```csharp
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

不会报告编译时错误，因为这两个表达式都不能在编译时求值。在运行时，F 方法抛出 System.OverflowException，G 方法返回 -727379968（越界结果的低 32 位）。H 方法的行为取决于编译的默认溢出检查上下文，但它要么与 F 相同，要么与 G 相同。

在示例

```csharp
class Test
{
    const int x = 1000000;
    const int y = 1000000;
    static int F() {
        return checked(x * y);    // Compile error, overflow
    }
    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }
    static int H() {
        return x * y;             // Compile error, overflow
    }
}
```

在 F 和 H 中求值常量表达式时发生的溢出会导致报告编译时错误，因为这些表达式在 checked 上下文中求值。在 G 中求值常量表达式时也会发生溢出，但由于求值在 unchecked 上下文中进行，因此不会报告该溢出。

checked 和 unchecked 运算符仅影响在文本上包含在“(”和“)”标记内的那些操作的溢出检查上下文。这些运算符对因求值所包含表达式而调用的函数成员没有影响。在示例

```csharp
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

F 中使用 checked 不会影响 Multiply 中 x * y 的求值，因此 x * y 在默认溢出检查上下文中求值。

当以十六进制记法编写有符号整型常量时，unchecked 运算符很方便。例如：

```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

上面的两个十六进制常量都是 uint 类型。因为这些常量超出 int 范围，如果没有 unchecked 运算符，到 int 的强制转换将产生编译时错误。

checked 和 unchecked 运算符及语句允许程序员控制某些数值计算的某些方面。然而，某些数值运算符的行为取决于其操作数的数据类型。例如，两个 decimal 相乘即使在显式 unchecked 构造中，也始终会在溢出时产生异常。类似地，两个 float 相乘即使在显式 checked 构造中，也绝不会在溢出时产生异常。此外，其他运算符绝不会受检查模式（无论默认还是显式）的影响。

### 7.6.13 默认值表达式

默认值表达式用于获取类型的默认值（§5.2）。通常，默认值表达式用于类型参数，因为可能不知道类型参数是值类型还是引用类型。（除非已知类型参数是引用类型，否则不存在从 null 字面量到类型参数的转换。）

```
default-value-expression:
    default ( type )
```

如果默认值表达式中的类型在运行时求值为引用类型，则结果为转换为该类型的 null。如果默认值表达式中的类型在运行时求值为值类型，则结果为该值类型的默认值（§4.1.2）。

如果类型是引用类型或已知为引用类型的类型参数（§10.1.5），则默认值表达式是常量表达式（§7.19）。此外，如果类型是以下值类型之一：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool 或任何枚举类型，则默认值表达式也是常量表达式。

### 7.6.14 匿名方法表达式

匿名方法表达式是定义匿名函数的两种方式之一。这些将在 §7.15 中进一步描述。



## 7.7 一元运算符

+, -, !, ~, ++, -- 和强制转换运算符称为一元运算符。

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

如果一元表达式的操作数具有编译时类型 dynamic，则它是动态绑定的（§7.2.2）。在这种情况下，一元表达式的编译时类型为 dynamic，并且下面描述的决策将在运行时使用操作数的运行时类型进行。

### 7.7.1 一元加运算符

对于 +x 形式的运算，应用一元运算符重载决策（§7.3.3）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。预定义的一元加运算符为：

```
int operator +(int x);
uint operator +(uint x);
long operator +(long x);
ulong operator +(ulong x);
float operator +(float x);
double operator +(double x);
decimal operator +(decimal x);
```

对于这些运算符中的每一个，结果就是操作数的值。

### 7.7.2 一元减运算符

对于 -x 形式的运算，应用一元运算符重载决策（§7.3.3）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。预定义的求负运算符为：

- 整数求负：
- 浮点数求负：

```
int operator -(int x);
long operator -(long x);
```

结果通过从零中减去 x 来计算。如果 x 的值为操作数类型可表示的最小值（int 为 -2^31，long 为 -2^63），则 x 的数学求负值在操作数类型中不可表示。如果这种情况发生在受检查上下文中，则抛出 System.OverflowException；如果发生在未检查上下文中，则结果为操作数的值，并且不报告溢出。

```
float operator -(float x);
double operator -(double x);
```

结果是 x 的值反转符号后的值。如果 x 为 NaN，则结果也为 NaN。

- 十进制求负：
  `decimal operator -(decimal x);`

结果通过从零中减去 x 来计算。十进制求负等效于使用 System.Decimal 类型的一元减运算符。

### 7.7.3 逻辑求反运算符

对于 !x 形式的运算，应用一元运算符重载决策（§7.3.3）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。只存在一个预定义逻辑求反运算符：

```
bool operator !(bool x);
```

此运算符计算操作数的逻辑求反：如果操作数为 true，则结果为 false。如果操作数为 false，则结果为 true。

### 7.7.4 按位求补运算符

对于 ~x 形式的运算，应用一元运算符重载决策（§7.3.3）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。预定义的按位求补运算符为：

```
int operator ~(int x);
uint operator ~(uint x);
long operator ~(long x);
ulong operator ~(ulong x);
```

对于这些运算符中的每一个，运算结果都是 x 的按位求补。

每个枚举类型 E 都隐式提供以下按位求补运算符：

```
E operator ~(E x);
```

计算 ~x（其中 x 是枚举类型 E 的表达式，E 的基础类型为 U）的结果与计算 (E)(~(U)x) 完全相同。

### 7.7.5 前缀递增和递减运算符

```
pre-increment-expression:
  ++ unary-expression
pre-decrement-expression:
  -- unary-expression
```

前缀递增或递减运算的操作数必须是分类为变量、属性访问或索引器访问的表达式。运算的结果是与操作数类型相同的值。

如果前缀递增或递减运算的操作数是属性或索引器访问，则该属性或索引器必须同时具有 get 和 set 访问器。如果不是这种情况，则发生绑定时间错误。

应用一元运算符重载决策（§7.3.3）来选择特定的运算符实现。预定义的 ++ 和 -- 运算符适用于以下类型：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal 以及任何枚举类型。预定义的 ++ 运算符返回向操作数加 1 所产生的值，预定义的 -- 运算符返回从操作数减 1 所产生的值。在受检查上下文中，如果此加法或减法的结果超出结果类型的范围，并且结果类型为整型或枚举类型，则抛出 System.OverflowException。

对 ++x 或 --x 形式的前缀递增或递减运算的运行时处理包括以下步骤：

- 如果 x 被分类为变量：
  - 计算 x 以产生该变量。
  - 使用 x 的值作为参数调用所选运算符。
  - 将运算符返回的值存储在计算 x 所得的位置中。
  - 运算符返回的值成为运算的结果。
- 如果 x 被分类为属性或索引器访问：
  - 计算与 x 关联的实例表达式（如果 x 不是静态的）和参数列表（如果 x 是索引器访问），并将结果用于后续的 get 和 set 访问器调用。
  - 调用 x 的 get 访问器。
  - 使用 get 访问器返回的值作为参数调用所选运算符。
  - 使用运算符返回的值作为其 value 参数调用 x 的 set 访问器。
  - 运算符返回的值成为运算的结果。

++ 和 -- 运算符也支持后缀表示法（§7.6.9）。通常，x++ 或 x-- 的结果是运算前 x 的值，而 ++x 或 --x 的结果是运算后 x 的值。无论哪种情况，运算后 x 本身都具有相同的值。

operator ++ 或 operator -- 实现可以使用后缀或前缀表示法调用。无法为这两种表示法分别提供不同的运算符实现。

### 7.7.6 强制转换表达式

强制转换表达式用于将表达式显式转换为给定类型。

```
cast-expression:
    ( type ) unary-expression
```

形式为 (T)E 的强制转换表达式（其中 T 是类型，E 是一元表达式）执行将 E 的值显式转换（§6.2）为类型 T。如果不存在从 E 到 T 的显式转换，则发生绑定时间错误。否则，结果是由显式转换产生的值。即使 E 表示变量，结果也始终分类为值。

强制转换表达式的语法会导致某些句法歧义。例如，表达式 (x)-y 既可以解释为强制转换表达式（将 -y 强制转换为类型 x），也可以解释为加法表达式与带括号表达式的组合（计算值 x - y）。

为了解决强制转换表达式的歧义，存在以下规则：仅当以下至少一项为真时，括在括号中的一个或多个标记（§2.3.3）序列才被视为强制转换表达式的开头：

- 该标记序列是类型的正确语法，但不是表达式的正确语法。
- 该标记序列是类型的正确语法，并且紧跟在右括号之后的标记是标记“~”、标记“!”、标记“*”、标识符（§2.4.1）、字面量（§2.4.4）或除 as 和 is 之外的任何关键字（§2.4.3）。

上面的术语“正确语法”仅表示标记序列必须符合特定的语法产生式。它特别不考虑任何构成标识符的实际含义。例如，如果 x 和 y 是标识符，则 x.y 是类型的正确语法，即使 x.y 实际上并不表示类型。



根据消歧规则可知，如果 x 和 y 是标识符，则 (x)y、(x)(y) 和 (x)(−y) 都是强制转换表达式，但 (x)−y 不是，即使 x 标识一个类型。然而，如果 x 是标识预定义类型的关键字（如 int），则四种形式都是强制转换表达式（因为此类关键字本身不可能是一个表达式）。

## 7.8 算术运算符

*, /, %, +, 和 − 运算符称为算术运算符。

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

如果算术运算符的操作数具有编译时类型 dynamic，则表达式是动态绑定的 (§7.2.2)。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时使用具有编译时类型 dynamic 的那些操作数的运行时类型进行。

### 7.8.1 乘法运算符

对于形式为 x * y 的操作，将应用二元运算符重载解析 (§7.3.4) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。

预定义的乘法运算符列于下文。所有运算符都计算 x 和 y 的乘积。

- 整数乘法：
  ```
  int operator *(int x, int y);
  uint operator *(uint x, uint y);
  long operator *(long x, long y);
  ulong operator *(ulong x, ulong y);
  ```
- 浮点乘法：
  ```
  float operator *(float x, float y);
  double operator *(double x, double y);
  ```

在检查上下文中，如果乘积超出结果类型的范围，则会抛出 System.OverflowException。在未检查上下文中，不会报告溢出，并且结果类型范围之外的任何有意义的高位都被丢弃。

乘积是根据 IEEE 754 算术规则计算的。下表列出了所有非零有限值、零、无穷大和 NaN 的可能组合的结果。在表中，x 和 y 为正有限值。z 是 x * y 的结果。如果结果对于目标类型来说太大，则 z 为无穷大。如果结果对于目标类型来说太小，则 z 为零。

|  | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | -z | +0 | -0 | +∞ | -∞ | NaN |
| -x | -z | +z | -0 | +0 | -∞ | +∞ | NaN |
| +0 | +0 | -0 | +0 | -0 | NaN | NaN | NaN |
| -0 | -0 | +0 | -0 | +0 | NaN | NaN | NaN |
| +∞ | +∞ | -∞ | NaN | NaN | +∞ | -∞ | NaN |
| -∞ | -∞ | +∞ | NaN | NaN | -∞ | +∞ | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制乘法：
  `decimal operator *(decimal x, decimal y);`

  如果结果值太大而无法以十进制格式表示，则会抛出 System.OverflowException。如果结果值太小而无法以十进制格式表示，则结果为零。结果的精度，在任何舍入之前，是两个操作数精度的总和。

  十进制乘法等价于使用类型 System.Decimal 的乘法运算符。

### 7.8.2 除法运算符

对于形式为 x / y 的操作，将应用二元运算符重载解析 (§7.3.4) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。

预定义的除法运算符列于下文。所有运算符都计算 x 和 y 的商。

- 整数除法：
  `int operator /(int x, int y);`
  `uint operator /(uint x, uint y);`
  `long operator /(long x, long y);`
  `ulong operator /(ulong x, ulong y);`

  如果右操作数的值为零，则会抛出 System.DivideByZeroException。

  除法将结果向零舍入。因此，结果的绝对值是小于或等于两个操作数商的绝对值的最大可能整数。当两个操作数的符号相同时，结果为零或正数；当两个操作数的符号相反时，结果为零或负数。

  如果左操作数是最小的可表示 int 或 long 值且右操作数为 -1，则会发生溢出。在检查上下文中，这会导致抛出 System.ArithmeticException（或其子类）。在未检查上下文中，是否抛出 System.ArithmeticException（或其子类）或溢出未报告且结果值为左操作数的值是实现定义的。

- 浮点除法：
  `float operator /(float x, float y);`
  `double operator /(double x, double y);`

  商是根据 IEEE 754 算术规则计算的。下表列出了所有非零有限值、零、无穷大和 NaN 的可能组合的结果。在表中，x 和 y 为正有限值。z 是 x / y 的结果。如果结果对于目标类型来说太大，则 z 为无穷大。如果结果对于目标类型来说太小，则 z 为零。

|  | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +x | +z | -z | +∞ | -∞ | +0 | -0 | NaN |
| -x | -z | +z | -∞ | +∞ | -0 | +0 | NaN |
| +0 | +0 | -0 | NaN | NaN | +0 | -0 | NaN |
| -0 | -0 | +0 | NaN | NaN | -0 | +0 | NaN |
| +∞ | +∞ | -∞ | +∞ | -∞ | NaN | NaN | NaN |
| -∞ | -∞ | +∞ | -∞ | +∞ | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制除法：
  `decimal operator /(decimal x, decimal y);`

如果右操作数的值为零，则会抛出 System.DivideByZeroException。如果结果值太大而无法以十进制格式表示，则会抛出 System.OverflowException。如果结果值太小而无法以十进制格式表示，则结果为零。结果的精度是能够保持等于最接近真实数学结果的可表示十进制值的最小精度。

十进制除法等价于使用类型 System.Decimal 的除法运算符。

### 7.8.3 余数运算符

对于形式为 x % y 的操作，将应用二元运算符重载解析 (§7.3.4) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。

预定义的余数运算符列于下文。所有运算符都计算 x 和 y 相除的余数。

- 整数取余：
  `int operator %(int x, int y);`
  `uint operator %(uint x, uint y);`
  `long operator %(long x, long y);`
  `ulong operator %(ulong x, ulong y);`

x % y 的结果是 x - (x / y) * y 产生的值。如果 y 为零，则会抛出 System.DivideByZeroException。

如果左操作数是最小的 int 或 long 值且右操作数为 -1，则会抛出 System.OverflowException。在任何情况下，x % y 都不会在 x / y 不会抛出异常的情况下抛出异常。

- 浮点取余：
  `float operator %(float x, float y);`
  `double operator %(double x, double y);`

下表列出了所有非零有限值、零、无穷大和 NaN 的可能组合的结果。在表中，x 和 y 为正有限值。z 是 x % y 的结果，计算方式为 x - n * y，其中 n 是小于或等于 x / y 的最大可能整数。这种计算余数的方法类似于对整数操作数使用的方法，但与 IEEE 754 定义不同（其中 n 是最接近 x / y 的整数）。



| | +y | -y | +0 | -0 | +∞ | -∞ | NaN |
|---|---|---|---|---|---|---|---|
| +X | +Z | +Z | NaN | NaN | X | X | NaN |
| -X | -Z | -Z | NaN | NaN | -X | -X | NaN |
| +0 | +0 | +0 | NaN | NaN | +0 | +0 | NaN |
| -0 | -0 | -0 | NaN | NaN | -0 | -0 | NaN |
| +∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| -∞ | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- 十进制余数：

    ```
    decimal operator %(decimal x, decimal y);
    ```

    如果右操作数的值为零，则引发 System.DivideByZeroException。在进行任何舍入之前，结果的小数位数是两个操作数中小数位数较大者；如果结果非零，则其符号与 x 的符号相同。

    decimal 余数等效于使用 System.Decimal 类型的余数运算符。

### 7.8.4 加法运算符

对于形如 x + y 的运算，应用二元运算符重载决策（§7.3.4）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型是该运算符的返回类型。

下面列出预定义的加法运算符。对于数值类型和枚举类型，预定义的加法运算符计算两个操作数之和。当一个或两个操作数为 string 类型时，预定义的加法运算符将操作数的字符串表示形式串联起来。

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

    和根据 IEEE 754 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值，z 是 x + y 的结果。如果 x 和 y 具有相同量值但符号相反，则 z 为正零。如果 x + y 太大而无法在目标类型中表示，则 z 是与 x + y 符号相同的无穷大。

    | | y | +0 | -0 | +∞ | -∞ | NaN |
    |---|---|---|---|---|---|---|
    | x | z | x | x | +∞ | -∞ | NaN |
    | +0 | y | +0 | +0 | +∞ | -∞ | NaN |
    | -0 | y | +0 | -0 | +∞ | -∞ | NaN |
    | +∞ | +∞ | +∞ | +∞ | +∞ | NaN | NaN |
    | -∞ | -∞ | -∞ | -∞ | NaN | -∞ | NaN |
    | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- decimal 加法：

    ```csharp
    decimal operator +(decimal x, decimal y);
    ```

    如果结果值太大而无法用 decimal 格式表示，则引发 System.OverflowException。在进行任何舍入之前，结果的小数位数是两个操作数中小数位数较大者。

    decimal 加法等效于使用 System.Decimal 类型的加法运算符。

- 枚举加法。每个枚举类型都隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：

    ```csharp
    E operator +(E x, U y);
    E operator +(U x, E y);
    ```

    在运行时，这些运算符完全按照 (E)((U)x + (U)y) 求值。

- 字符串串联：

    ```csharp
    string operator +(string x, string y);
    string operator +(string x, object y);
    string operator +(object x, string y);
    ```

    二元 + 运算符的这些重载执行字符串串联。如果字符串串联的操作数为 null，则替换为空字符串。否则，任何非字符串参数都通过调用从 object 类型继承的虚拟 ToString 方法转换为字符串表示形式。如果 ToString 返回 null，则替换为空字符串。

    ```
    using System;
    class Test
    {
        static void Main() {
            string s = null;
            Console.WriteLine("s = >" + s + "<");    // displays s = ><
            int i = 1;
            Console.WriteLine("i = " + i);           // displays i = 1
            float f = 1.2300E+15F;
            Console.WriteLine("f = " + f);           // displays f = 1.23E+15
            decimal d = 2.900m;
            Console.WriteLine("d = " + d);           // displays d = 2.900
        }
    }
    ```

    字符串串联运算符的结果是一个字符串，它由左操作数的字符后跟右操作数的字符组成。字符串串联运算符从不返回 null 值。如果没有足够内存来分配结果字符串，则可能引发 System.OutOfMemoryException。

- 委托组合。每个委托类型都隐式提供以下预定义运算符，其中 D 是委托类型：

    ```
    D operator +(D x, D y);
    ```

    当两个操作数都是某个委托类型 D 时，二元 + 运算符执行委托组合。（如果操作数具有不同的委托类型，则发生绑定期错误。）如果第一个操作数为 null，则运算结果是第二个操作数的值（即使该值也为 null）。否则，如果第二个操作数为 null，则运算结果是第一个操作数的值。否则，运算结果是一个新的委托实例，调用该实例时，先调用第一个操作数，再调用第二个操作数。有关委托组合的示例，请参见 §7.8.5 和 §15.4。由于 System.Delegate 不是委托类型，因此未为其定义运算符 +。

### 7.8.5 减法运算符

对于形如 x - y 的运算，应用二元运算符重载决策（§7.3.4）来选择特定的运算符实现。操作数转换为所选运算符的参数类型，结果的类型是该运算符的返回类型。

下面列出预定义的减法运算符。这些运算符都从 x 中减去 y。

- 整数减法：

    ```
    int operator -(int x, int y);
    uint operator -(uint x, uint y);
    long operator -(long x, long y);
    ulong operator -(ulong x, ulong y);
    ```

    在 checked 上下文中，如果差超出结果类型的范围，则引发 System.OverflowException。在 unchecked 上下文中，不报告溢出，并且丢弃结果类型范围之外的任何有效高阶位。

- 浮点减法：

    ```
    float operator -(float x, float y);
    double operator -(double x, double y);
    ```

    差根据 IEEE 754 算术规则计算。下表列出了非零有限值、零、无穷大和 NaN 的所有可能组合的结果。表中，x 和 y 是非零有限值，z 是 x - y 的结果。如果 x 和 y 相等，则 z 为正零。如果 x - y 太大而无法在目标类型中表示，则 z 是与 x - y 符号相同的无穷大。

    | | y | +0 | -0 | +∞ | -∞ | NaN |
    |---|---|---|---|---|---|---|
    | x | z | x | x | -∞ | +∞ | NaN |
    | +0 | -y | +0 | +0 | -∞ | +∞ | NaN |
    | -0 | -y | -0 | +0 | -∞ | +∞ | NaN |
    | +∞ | +∞ | +∞ | +∞ | NaN | +∞ | NaN |
    | -∞ | -∞ | -∞ | -∞ | -∞ | NaN | NaN |
    | NaN | NaN | NaN | NaN | NaN | NaN | NaN |

- decimal 减法：

    ```
    decimal operator -(decimal x, decimal y);
    ```

    如果结果值太大而无法用 decimal 格式表示，则引发 System.OverflowException。在进行任何舍入之前，结果的小数位数是两个操作数中小数位数较大者。

    decimal 减法等效于使用 System.Decimal 类型的减法运算符。

- 枚举减法。每个枚举类型都隐式提供以下预定义运算符，其中 E 是枚举类型，U 是 E 的基础类型：

    `U operator -(E x, E y);`

    此运算符完全按照 (U)((U)x - (U)y) 求值。换言之，该运算符计算 x 和 y 的序数值之差，结果的类型是枚举的基础类型。

    `E operator -(E x, U y);`

    此运算符完全按照 (E)((U)x - y) 求值。换言之，该运算符从枚举的基础类型中减去一个值，从而产生枚举值。

- 委托移除。每个委托类型都隐式提供以下预定义运算符，其中 D 是委托类型：

    `D operator -(D x, D y);`

    当两个操作数都是某个委托类型 D 时，二元 - 运算符执行委托移除。如果操作数具有不同的委托类型，则发生绑定期错误。如果第一个操作数为 null，则运算结果为 null。否则，如果第二个操作数为 null，则运算结果是第一个操作数的值。否则，两个操作数都表示具有一个或多个条目的调用列表（§15.1），并且如果第二个操作数的列表是第一个操作数列表的适当连续子列表，则结果是一个新的调用列表，它由从第一个操作数的列表中移除第二个操作数的条目后组成。（为了确定子列表相等性，相应条目按照委托相等运算符（§7.10.8）的方式进行比较。）否则，结果是左操作数的值。在此过程中，两个操作数的列表都不会更改。如果第二个操作数的列表与第一个操作数列表中的多个连续条目子列表匹配，则移除最右侧匹配的连续条目子列表。如果移除导致空列表，则结果为 null。例如：

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
            D cd3 = cd1 + cd2 + cd2 + cd1;    // M1 + M2 + M2 + M1
            cd3 -= cd1;                       // => M1 + M2 + M2

            cd3 = cd1 + cd2 + cd2 + cd1;      // M1 + M2 + M2 + M1
            cd3 -= cd1 + cd2;                 // => M2 + M1

            cd3 = cd1 + cd2 + cd2 + cd1;      // M1 + M2 + M2 + M1
            cd3 -= cd2 + cd2;                 // => M1 + M1

            cd3 = cd1 + cd2 + cd2 + cd1;      // M1 + M2 + M2 + M1
            cd3 -= cd2 + cd1;                 // => M1 + M2

            cd3 = cd1 + cd2 + cd2 + cd1;      // M1 + M2 + M2 + M1
            cd3 -= cd1 + cd1;                 // => M1 + M2 + M2 + M1
        }
    }
    ```

## 7.9 移位运算符

<< 和 >> 运算符用于执行移位操作。




## C# 语言规范

```
shift-expression:
    additive-expression
    shift-expression << additive-expression
    shift-expression right-shift additive-expression
```

如果 shift-expression 的操作数具有编译时类型 dynamic，则该表达式是动态绑定的 (§7.2.2)。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时使用具有编译时类型 dynamic 的那些操作数的运行时类型进行。

对于形式为 x << count 或 x >> count 的操作，将应用二进制运算符重载解析 (§7.3.4) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，并且结果的类型为运算符的返回类型。

在声明重载的移位运算符时，第一个操作数的类型必须始终是包含运算符声明的类或结构体，并且第二个操作数的类型必须始终为 int。

预定义的移位运算符列在下面。

- 左移：
```
int operator <<(int x, int count);
uint operator <<(uint x, int count);
long operator <<(long x, int count);
ulong operator <<(ulong x, int count);
```

<< 运算符将 x 左移下面描述计算出的位数。

超出 x 结果类型的范围的高位被丢弃，其余位左移，低位的空位设为零。

- 右移：
```
int operator >>(int x, int count);
uint operator >>(uint x, int count);
long operator >>(long x, int count);
ulong operator >>(ulong x, int count);
```

>> 运算符将 x 右移下面描述计算出的位数。

当 x 的类型为 int 或 long 时，x 的低位被丢弃，其余位右移，如果 x 为非负数则高位的空位设为零，如果 x 为负数则设为一。

当 x 的类型为 uint 或 ulong 时，x 的低位被丢弃，其余位右移，高位的空位设为零。

对于预定义运算符，移位位数按如下方式计算：

- 当 x 的类型为 int 或 uint 时，移位计数由 count 的低五位给出。换句话说，移位计数由 count & 0x1F 计算得出。
- 当 x 的类型为 long 或 ulong 时，移位计数由 count 的低六位给出。换句话说，移位计数由 count & 0x3F 计算得出。

如果得到的移位计数为零，移位运算符 simply 返回 x 的值。

移位操作永远不会导致溢出，并且在 checked 和 unchecked 上下文中产生相同的结果。

当 >> 运算符的左操作数为有符号整数类型时，运算符执行算术右移，其中操作数的最高有效位（符号位）的值会传播到高位的空位。当 >> 运算符的左操作数为无符号整数类型时，运算符执行逻辑右移，其中高位的空位始终设为零。为了执行与操作数类型推断相反的操作，可以使用显式转换。例如，如果 x 是类型为 int 的变量，则操作 unchecked((int)((uint)x >> y)) 对 x 执行逻辑右移。

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

equality-expression:
    relational-expression
    equality-expression == relational-expression
    equality-expression != relational-expression
```

is 运算符在 §7.10.10 中描述，as 运算符在 §7.10.11 中描述。

==、!=、<、>、<= 和 >= 运算符是比较运算符。

如果比较运算符的操作数具有编译时类型 dynamic，则该表达式是动态绑定的 (§7.2.2)。在这种情况下，表达式的编译时类型为 dynamic，并且下面描述的解析将在运行时使用具有编译时类型 dynamic 的那些操作数的运行时类型进行。

对于形式为 x op y 的操作，其中 op 是比较运算符，将应用重载解析 (§7.3.4) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，并且结果的类型为运算符的返回类型。

预定义的比较运算符在以下各节中描述。所有预定义的比较运算符都返回类型为 bool 的结果，如下表所述。

| 操作 | 结果 |
|---|---|
| x == y | 如果 x 等于 y 则为 true，否则为 false |
| x != y | 如果 x 不等于 y 则为 true，否则为 false |
| x < y | 如果 x 小于 y 则为 true，否则为 false |
| x > y | 如果 x 大于 y 则为 true，否则为 false |
| x <= y | 如果 x 小于或等于 y 则为 true，否则为 false |
| x >= y | 如果 x 大于或等于 y 则为 true，否则为 false |

### 7.10.1 整数比较运算符

预定义的整数比较运算符为：

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

这些运算符中的每一个都比较两个整数操作数的数值，并返回一个 bool 值，表示特定关系是否为真或假。

### 7.10.2 浮点比较运算符

预定义的浮点比较运算符为：

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

运算符根据 IEEE 754 标准规则比较操作数：

- 如果任一操作数为 NaN，则除 != 之外的所有运算符的结果均为 false，而 != 的结果为 true。对于任意两个操作数，x != y 始终产生与 !(x == y) 相同的结果。然而，当一个或两个操作数为 NaN 时，<、>、<= 和 >= 运算符不会产生与相反运算符的逻辑否定相同的结果。例如，如果 x 和 y 中任一为 NaN，则 x < y 为 false，但 !(x >= y) 为 true。
- 当两个操作数都不是 NaN 时，运算符根据以下顺序比较两个浮点操作数的值
-∞ < -max < … < -min < -0.0 == +0.0 < +min < … < +max < +∞
其中 min 和 max 是可在给定浮点格式中表示的最小和最大正有限值。此顺序的显著影响是：
- 负零和正零被视为相等。
- 负无穷被认为小于所有其他值，但等于另一个负无穷。



- 正无穷被认为大于所有其他值，但等于另一个正无穷。

## 7.10.3 十进制比较运算符

预定义的十进制比较运算符如下：

```
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

每个运算符都会比较两个 decimal 操作数的数值，并返回一个 bool 值，指示特定关系为 true 还是 false。每个十进制比较都等同于使用 System.Decimal 类型的相应关系运算符或相等运算符。

## 7.10.4 布尔相等运算符

预定义的布尔相等运算符如下：

```
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

如果 x 和 y 都为 true 或都为 false，则 == 的结果为 true；否则结果为 false。如果 x 和 y 都为 true 或都为 false，则 != 的结果为 false；否则结果为 true。当操作数为 bool 类型时，!= 运算符产生的结果与 ^ 运算符相同。

## 7.10.5 枚举比较运算符

每个枚举类型都隐式提供以下预定义比较运算符：

```
bool operator ==(E x, E y);
bool operator !=(E x, E y);
bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

计算 x op y 的结果（其中 x 和 y 是基础类型为 U 的枚举类型 E 的表达式，op 是比较运算符之一）与计算 ((U)x) op ((U)y) 的结果完全相同。换句话说，枚举类型比较运算符只是比较两个操作数的基础整数值。

## 7.10.6 引用类型相等运算符

预定义的引用类型相等运算符如下：

bool operator ==(object x, object y);
bool operator !=(object x, object y);

这些运算符返回比较两个引用相等或不相等的结果。

由于预定义的引用类型相等运算符接受 object 类型的操作数，它们适用于所有未声明适用的 operator == 和 operator != 成员的类型。相反，任何适用的用户自定义相等运算符都会有效地隐藏预定义的引用类型相等运算符。

预定义的引用类型相等运算符要求满足以下条件之一：

- 两个操作数都是已知为*引用类型*的类型的值或 null 字面量。此外，从任一操作数的类型到另一个操作数的类型存在显式引用转换（§6.2.4）。
- 一个操作数是类型 T 的值，其中 T 是*类型参数*，另一个操作数是 null 字面量。此外，T 没有值类型约束。

除非满足这些条件之一，否则会发生绑定期错误。这些规则的重要含义如下：

- 使用预定义的引用类型相等运算符比较在绑定期已知不同的两个引用是一个绑定期错误。例如，如果操作数的绑定期类型是两个类类型 A 和 B，并且 A 和 B 都不从另一个派生，那么两个操作数不可能引用同一个对象。因此，该操作被视为绑定期错误。
- 预定义的引用类型相等运算符不允许比较值类型操作数。因此，除非结构类型声明了自己的相等运算符，否则无法比较该结构类型的值。
- 预定义的引用类型相等运算符不会对其操作数执行装箱操作。执行此类装箱操作毫无意义，因为对新分配的装箱实例的引用必然与所有其他引用不同。
- 如果类型参数类型 T 的操作数与 null 比较，并且 T 的运行时类型是值类型，则比较结果为 false。

下面的示例检查无约束类型参数类型的参数是否为 null。

```csharp
class C<T>
{
    void F(T x) {
        if (x == null) throw new ArgumentNullException();
        ...
    }
}
```

x == null 构造是允许的，即使 T 可能表示值类型，并且当 T 是值类型时，结果被简单定义为 false。

对于形式为 x == y 或 x != y 的操作，如果存在任何适用的 operator == 或 operator !=，运算符重载决策（§7.3.4）规则将选择该运算符，而不是预定义的引用类型相等运算符。但是，始终可以通过将其中一个或两个操作数显式强制转换为 object 类型来选择预定义的引用类型相等运算符。例如：

```csharp
using System;
class Test
{
    static void Main() {
        string s = "Test";
        string t = string.Copy(s);
        Console.WriteLine(s == t);
        Console.WriteLine((object)s == t);
        Console.WriteLine(s == (object)t);
        Console.WriteLine((object)s == (object)t);
    }
}
```

产生以下输出：

True
False
False
False

变量 s 和 t 引用两个包含相同字符的不同字符串实例。第一个比较输出 True，因为当两个操作数都是 string 类型时，会选择预定义的字符串相等运算符（§7.10.7）。其余比较均输出 False，因为当一个或两个操作数是 object 类型时，会选择预定义的引用类型相等运算符。

请注意，上述技术对值类型没有意义。例如：

```csharp
class Test
{
    static void Main() {
        int i = 123;
        int j = 123;
        System.Console.WriteLine((object)i == (object)j);
    }
}
```

输出 False，因为强制转换创建了对两个独立的装箱 int 值实例的引用。

## 7.10.7 字符串相等运算符

预定义的字符串相等运算符如下：

```
bool operator ==(string x, string y);
bool operator !=(string x, string y);
```

当以下条件之一为真时，两个字符串值被视为相等：

- 两个值都为 null。
- 两个值都是对字符串实例的非 null 引用，这些字符串实例具有相同的长度，并且在每个字符位置具有相同的字符。

字符串相等运算符比较字符串值而不是字符串引用。当两个不同的字符串实例包含完全相同的字符序列时，字符串的值相等，但引用不同。如 §7.10.6 所述，可以使用引用类型相等运算符来比较字符串引用而不是字符串值。

## 7.10.8 委托相等运算符

每个委托类型隐式提供以下预定义比较运算符：

```
bool operator ==(System.Delegate x, System.Delegate y);
bool operator !=(System.Delegate x, System.Delegate y);
```

两个委托实例按如下方式被视为相等：

- 如果任一委托实例为 null，则当且仅当两者都为 null 时，它们相等。
- 如果委托具有不同的运行时类型，则它们永远不相等。
- 如果两个委托实例都有调用列表（§15.1），则当且仅当它们的调用列表长度相同，并且一个调用列表中的每个条目（按顺序）与另一个调用列表中对应的条目相等（定义如下）时，这些实例相等。

以下规则管理调用列表条目的相等性：

- 如果两个调用列表条目都引用同一个静态方法，则这些条目相等。
- 如果两个调用列表条目都引用同一目标对象上的同一个非静态方法（由引用相等运算符定义），则这些条目相等。
- 由语义相同的*匿名函数表达式*求值生成的调用列表条目，如果具有相同的（可能为空的）捕获外部变量实例集合，则允许（但不要求）相等。

## 7.10.9 相等运算符与 null

`==` 和 `!=` 运算符允许一个操作数是可空类型的值，另一个操作数是 `null` 字面量，即使该操作没有预定义或用户定义的运算符（未提升或提升形式）存在。

对于以下形式之一的操作：

```
x == null    null == x    x != null    null != x
```

其中 x 是可空类型的表达式，如果运算符重载决策（§7.2.4）无法找到适用的运算符，则改为根据 x 的 `HasValue` 属性计算结果。具体来说，前两种形式转换为 `!x.HasValue`，后两种形式转换为 `x.HasValue`。

## 7.10.10 *is* 运算符

`is` 运算符用于动态检查对象的运行时类型是否与给定类型兼容。操作 E *is* T 的结果（其中 E 是表达式，T 是类型）是一个布尔值，指示 E 是否可以通过引用转换、装箱转换或取消装箱转换成功转换为类型 T。在为所有类型参数替换类型实参后，按如下方式计算该操作：

- 如果 E 是匿名函数，则发生编译时错误。
- 如果 E 是方法组或 `null` 字面量，或者 E 的类型是引用类型或可空类型且 E 的值为 `null`，则结果为 false。
- 否则，设 D 表示 E 的动态类型，如下所示：
  - 如果 E 的类型是引用类型，则 D 是 E 引用的实例的运行时类型。
  - 如果 E 的类型是可空类型，则 D 是那个可空类型的基础类型。
  - 如果 E 的类型是不可空值类型，则 D 是 E 的类型。
- 操作的结果取决于 D 和 T，如下所示：
  - 如果 T 是引用类型，则当 D 和 T 是相同类型、D 是引用类型且存在从 D 到 T 的隐式引用转换，或者 D 是值类型且存在从 D 到 T 的装箱转换时，结果为 true。
  - 如果 T 是可空类型，则当 D 是 T 的基础类型时，结果为 true。
  - 如果 T 是不可空值类型，则当 D 和 T 是相同类型时，结果为 true。
  - 否则，结果为 false。

请注意，`is` 运算符不考虑用户定义的转换。

## 7.10.11 *as* 运算符

`as` 运算符用于将值显式转换为给定的引用类型或可空类型。与强制转换表达式（§7.7.6）不同，`as` 运算符永远不会引发异常。相反，如果指示的转换不可能，则结果值为 `null`。




在形如 `E as T` 的操作中，`E` 必须是表达式，`T` 必须是引用类型、已知为引用类型的类型参数或可空类型。此外，以下条件中至少有一个必须为真，否则将发生编译时错误：

-   存在从 `E` 到 `T` 的恒等转换（§6.1.1）、隐式可空转换（§6.1.4）、隐式引用转换（§6.1.6）、装箱转换（§6.1.7）、显式可空转换（§6.2.3）、显式引用转换（§6.2.4）或拆箱转换（§6.2.5）。
-   `E` 或 `T` 的类型是开放类型。
-   `E` 是 `null` 字面量。

如果 `E` 的编译时类型不是 `dynamic`，则操作 `E as T` 产生与以下相同的结果：

```
E is T ? (T)(E) : (T)null
```

区别在于 `E` 只计算一次。可以预期编译器会将 `E as T` 优化为最多执行一次动态类型检查，而不是上述展开所隐含的两次动态类型检查。

如果 `E` 的编译时类型是 `dynamic`，与强制转换运算符不同，`as` 运算符不会动态绑定（§7.2.2）。因此这种情况下的展开是：

```
E is T ? (T)(object)(E) : (T)null
```

注意，某些转换（例如用户定义的转换）不能使用 `as` 运算符进行，而应改用强制转换表达式。

在示例中

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

`G` 的类型参数 `T` 已知为引用类型，因为它具有类约束。然而，`H` 的类型参数 `U` 不是引用类型；因此，在 `H` 中使用 `as` 运算符是不允许的。

## 7.11 逻辑运算符

`&`、`^` 和 `|` 运算符称为逻辑运算符。

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

如果逻辑运算符的一个操作数具有编译时类型 `dynamic`，则该表达式会动态绑定（§7.2.2）。在这种情况下，表达式的编译时类型为 `dynamic`，下面描述的解析将在运行时使用具有编译时类型 `dynamic` 的那些操作数的运行时类型进行。

对于形如 `x op y` 的操作，其中 `op` 是逻辑运算符之一，将应用重载决策（§7.3.4）来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型是运算符的返回类型。

预定义逻辑运算符将在以下各节中描述。

### 7.11.1 整数逻辑运算符

预定义的整数逻辑运算符有：

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

`&` 运算符计算两个操作数的按位逻辑与（AND），`|` 运算符计算两个操作数的按位逻辑或（OR），`^` 运算符计算两个操作数的按位逻辑异或（XOR）。这些运算不可能产生溢出。

### 7.11.2 枚举逻辑运算符

每个枚举类型 `E` 都隐式提供以下预定义逻辑运算符：

```
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```

计算 `x op y` 的结果（其中 `x` 和 `y` 是基础类型为 `U` 的枚举类型 `E` 的表达式，`op` 是逻辑运算符之一）与计算 `(E)((U)x op (U)y)` 完全相同。换句话说，枚举类型逻辑运算符只是对两个操作数的基础类型执行逻辑运算。

### 7.11.3 布尔逻辑运算符

预定义的布尔逻辑运算符有：

```
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```

如果 `x` 和 `y` 都为 `true`，则 `x & y` 的结果为 `true`；否则结果为 `false`。如果 `x` 或 `y` 中有一个为 `true`，则 `x | y` 的结果为 `true`；否则结果为 `false`。如果 `x` 为 `true` 且 `y` 为 `false`，或者 `x` 为 `false` 且 `y` 为 `true`，则 `x ^ y` 的结果为 `true`；否则结果为 `false`。当操作数为 `bool` 类型时，`^` 运算符的计算结果与 `!=` 运算符相同。

### 7.11.4 可空布尔逻辑运算符

可空布尔类型 `bool?` 可以表示三个值：`true`、`false` 和 `null`，在概念上类似于 SQL 中用于布尔表达式的三值类型。为了确保 `&` 和 `|` 运算符针对 `bool?` 操作数产生的结果与 SQL 的三值逻辑一致，提供了以下预定义运算符：

```
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

下表列出了这些运算符对于 `true`、`false` 和 `null` 的所有值组合所产生的结果。

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

`&&` 和 `||` 运算符称为条件逻辑运算符。它们也被称为“短路”逻辑运算符。

```
conditional-and-expression:
    inclusive-or-expression
    conditional-and-expression && inclusive-or-expression

conditional-or-expression:
    conditional-and-expression
    conditional-or-expression || conditional-and-expression
```

`&&` 和 `||` 运算符是 `&` 和 `|` 运算符的条件版本：

-   操作 `x && y` 对应于操作 `x & y`，不同之处在于仅当 `x` 不为 `false` 时才计算 `y`。
-   操作 `x || y` 对应于操作 `x | y`，不同之处在于仅当 `x` 不为 `true` 时才计算 `y`。

如果条件逻辑运算符的一个操作数具有编译时类型 `dynamic`，则该表达式会动态绑定（§7.2.2）。在这种情况下，表达式的编译时类型为 `dynamic`，下面描述的解析将在运行时使用具有编译时类型 `dynamic` 的那些操作数的运行时类型进行。

形如 `x && y` 或 `x || y` 的操作通过应用重载决策（§7.3.4）来处理，就如同该操作被写为 `x & y` 或 `x | y`。然后：

-   如果重载决策未能找到唯一的最佳运算符，或者重载决策选择了预定义整数逻辑运算符之一，则会发生绑定期错误。
-   否则，如果所选运算符是预定义布尔逻辑运算符（§7.11.3）或可空布尔逻辑运算符（§7.11.4）之一，则按 §7.12.1 中所述处理该操作。
-   否则，所选运算符是用户定义的运算符，并按 §7.12.2 中所述处理该操作。

无法直接重载条件逻辑运算符。然而，由于条件逻辑运算符是根据常规逻辑运算符来计算的，因此常规逻辑运算符的重载在特定限制下也被视为条件逻辑运算符的重载。这将在 §7.12.2 中进一步说明。

### 7.12.1 布尔条件逻辑运算符

当 `&&` 或 `||` 的操作数为 `bool` 类型，或者操作数的类型未定义适用的 `&` 运算符或 `|` 运算符，但定义了到 `bool` 的隐式转换时，按如下方式处理该操作：

-   操作 `x && y` 被计算为 `x ? y : false`。换句话说，首先计算 `x` 并将其转换为 `bool` 类型。然后，如果 `x` 为 `true`，则计算 `y` 并将其转换为 `bool` 类型，该值即为操作的结果。否则，操作的结果为 `false`。
-   操作 `x || y` 被计算为 `x ? true : y`。换句话说，首先计算 `x` 并将其转换为 `bool` 类型。然后，如果 `x` 为 `true`，则操作的结果为 `true`。否则，计算 `y` 并将其转换为 `bool` 类型，该值即为操作的结果。

### 7.12.2 用户定义的条件逻辑运算符

当 `&&` 或 `||` 的操作数类型声明了适用的用户定义运算符 `&` 或运算符 `|` 时，以下两项都必须为真，其中 `T` 是所选运算符声明所在的类型：

-   所选运算符的返回类型和每个参数的类型都必须是 `T`。换句话说，该运算符必须计算类型 `T` 的两个操作数的逻辑与或逻辑或，并且必须返回类型 `T` 的结果。
-   `T` 必须包含 `operator true` 和 `operator false` 的声明。

如果这两项要求中任一项未得到满足，则会发生绑定期错误。否则，`&&` 或 `||` 操作通过将用户定义的 `operator true` 或 `operator false` 与所选用户定义运算符结合来求值：

-   操作 `x && y` 被计算为 `T.false(x) ? x : T.&(x, y)`，其中 `T.false(x)` 是对 `T` 中声明的 `operator false` 的调用，`T.&(x, y)` 是对选定的运算符 `&` 的调用。换句话说，首先计算 `x`，并对结果调用 `operator false` 以确定 `x` 是否肯定为 `false`。然后，如果 `x` 肯定为 `false`，则操作的结果是先前为 `x` 计算的值。否则，计算 `y`，并对先前为 `x` 计算的值和为 `y` 计算的值调用选定的运算符 `&`，以产生操作的结果。
-   操作 `x || y` 被计算为 `T.true(x) ? x : T.|(x, y)`，其中 `T.true(x)` 是对 `T` 中声明的 `operator true` 的调用，`T.|(x, y)` 是对选定的运算符 `|` 的调用。换句话说，首先计算 `x`，并对结果调用 `operator true` 以确定 `x` 是否肯定为 `true`。然后，如果 `x` 肯定为 `true`，则操作的结果是先前为 `x` 计算的值。否则，计算 `y`，并对先前为 `x` 计算的值和为 `y` 计算的值调用选定的运算符 `|`，以产生操作的结果。

在这两个操作中的任何一个中，表达式 `x` 只计算一次，而表达式 `y` 要么不计算，要么恰好计算一次。

有关实现 `operator true` 和 `operator false` 的类型示例，请参阅 §11.4.2。

## 7.13 空合并运算符

`??` 运算符称为空合并运算符。



```
null-coalescing-expression:
    conditional-or-expression
    conditional-or-expression   ??   null-coalescing-expression
```

空合并表达式的形式为 a ?? b 要求 a 为可空类型或引用类型。如果 a 为非空，则 a ?? b 的结果为 a；否则结果为 b。该操作仅在 a 为 null 时才求值 b。

空合并运算符是右结合的，这意味着操作是从右到左分组的。例如，形式为 a ?? b ?? c 的表达式被求值为 a ?? (b ?? c)。一般来说，形式为 E₁ ?? E₂ ?? ... ?? E_N 的表达式返回第一个非空的操作数，如果所有操作数都为 null，则返回 null。

表达式 a ?? b 的类型取决于操作数上可用的隐式转换。按优先顺序，a ?? b 的类型为 A₀、A 或 B，其中 A 为 a 的类型（前提是 a 有类型），B 为 b 的类型（前提是 b 有类型），A₀ 为 A 的底层类型，如果 A 是可空类型，否则为 A。具体来说，a ?? b 按如下方式处理：

- 如果 A 存在且不是可空类型或引用类型，则发生编译时错误。
- 如果 b 是 dynamic 表达式，则结果类型为 dynamic。运行时，首先求值 a。如果 a 不为 null，则 a 转换为 dynamic，这成为结果。否则，求值 b，这成为结果。
- 否则，如果 A 存在且为可空类型，并且存在从 b 到 A₀ 的隐式转换，则结果类型为 A₀。运行时，首先求值 a。如果 a 为非空，则 a 解包为类型 A₀，这成为结果。否则，求值 b 并转换为类型 A₀，这成为结果。
- 否则，如果 A 存在并且存在从 b 到 A 的隐式转换，则结果类型为 A。运行时，首先求值 a。如果 a 为非空，则 a 成为结果。否则，求值 b 并转换为类型 A，这成为结果。
- 否则，如果 b 有类型 B 并且存在从 a 到 B 的隐式转换，则结果类型为 B。运行时，首先求值 a。如果 a 为非空，则 a 解包为类型 A₀（如果 A 存在且为可空）并转换为类型 B，这成为结果。否则，求值 b 并成为结果。
- 否则，a 和 b 不兼容，发生编译时错误。

## 7.14 条件运算符

?: 运算符称为条件运算符。有时也称为三元运算符。

```
conditional-expression:
    null-coalescing-expression
    null-coalescing-expression   ?   expression   :   expression
```

形式为 b ? x : y 的条件表达式首先求值条件 b。然后，如果 b 为 true，则求值 x 并成为操作的结果。否则，求值 y 并成为操作的结果。条件表达式永远不会同时求值 x 和 y。

条件运算符是右结合的，这意味着操作是从右到左分组的。例如，形式为 a ? b : c ? d : e 的表达式被求值为 a ? b : (c ? d : e)。

?: 运算符的第一个操作数必须是可隐式转换为 bool 的表达式，或实现 operator true 的类型的表达式。如果不满足这两个要求中的任何一个，则发生编译时错误。

?: 运算符的第二个和第三个操作数 x 和 y 控制条件表达式的类型。

- 如果 x 的类型为 X 且 y 的类型为 Y 则
  - 如果存在从 X 到 Y 的隐式转换 (§6.1)，但不存在从 Y 到 X 的隐式转换，则 Y 为条件表达式的类型。
- 如果存在从 Y 到 X 的隐式转换 (§6.1)，但不存在从 X 到 Y 的隐式转换，则 X 为条件表达式的类型。
- 否则，无法确定表达式类型，发生编译时错误。
- 如果只有 x 和 y 中的一个有类型，并且 x 和 y 都可隐式转换为该类型，则该类型为条件表达式的类型。
- 否则，无法确定表达式类型，发生编译时错误。

形式为 b ? x : y 的条件表达式的运行时处理包括以下步骤：

- 首先，求值 b，并确定其 bool 值：
  - 如果存在从 b 的类型到 bool 的隐式转换，则执行此隐式转换以生成 bool 值。
  - 否则，调用 b 的类型定义的 operator true 以生成 bool 值。
- 如果上一步产生的 bool 值为 true，则求值 x 并转换为条件表达式的类型，这成为条件表达式的结果。
- 否则，求值 y 并转换为条件表达式的类型，这成为条件表达式的结果。

## 7.15 匿名函数表达式

匿名函数是一个表示“内联”方法定义的表达式。匿名函数本身没有值或类型，但可转换为兼容的委托或表达式树类型。匿名函数转换的求值取决于转换的目标类型：如果目标类型为委托类型，则转换求值为引用匿名函数定义的方法的委托值。如果目标类型为表达式树类型，则转换求值为表示方法结构为对象结构的表达式树。

出于历史原因，匿名函数有两种语法形式，即 lambda 表达式和匿名方法表达式。对于几乎所有目的而言，lambda 表达式比匿名方法表达式更简洁、更具表达力，而匿名方法表达式保留在语言中以保持向后兼容。

```
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
anonymous-function-parameter-modifier:
    ref
    out
```

```
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

=> 运算符的优先级与赋值 (=) 相同并且是右结合的。

lambda 表达式形式的匿名函数的参数可以显式或隐式键入。在显式类型参数列表中，每个参数的类型被显式声明。在隐式类型参数列表中，参数的类型从匿名函数出现的上下文中推断——具体来说，当匿名函数转换为兼容的委托类型或表达式树类型时，该类型提供参数类型 (§6.5)。

在具有单个隐式类型参数的匿名函数中，参数列表的括号可以省略。换句话说，形式为

```
( param ) => expr
```

的匿名函数可以缩写为

```
param => expr
```

匿名方法表达式形式的匿名函数的参数列表是可选的。如果给出，参数必须显式键入。如果没有给出，匿名函数可转换为不包含 out 参数的任意参数列表的委托。

下面是一些匿名函数的示例：

```
x => x + 1                     // Implicitly typed, expression body
x => { return x + 1; }          // Implicitly typed, statement body
(int x) => x + 1                // Explicitly typed, expression body
(int x) => { return x + 1; }    // Explicitly typed, statement body
(x, y) => x * y                 // Multiple parameters
() => Console.WriteLine()       // No parameters
delegate (int x) { return x + 1; } // Anonymous method expression
delegate { return 1 + 1; }      // Parameter list omitted
```

lambda 表达式和匿名方法表达式的行为相同，除了以下几点：

- 匿名方法表达式允许完全省略参数列表，从而可转换为任意值参数列表的委托类型。
- lambda 表达式允许省略参数类型并推断，而匿名方法表达式要求参数类型必须显式声明。



- lambda 表达式的体可以是表达式或语句块，而匿名方法表达式的体必须是语句块。
- 由于只有 lambda 表达式可以具有表达式体，因此没有任何匿名方法表达式可以成功转换为表达式树类型（§4.6）。

## 7.15.1 匿名函数签名

匿名函数的可选匿名函数签名定义匿名函数的形参的名称以及可选的类型。匿名函数参数的作用域是匿名函数体。（§3.7）与参数列表（如果给定）一起，匿名方法体构成声明空间（§3.3）。因此，如果匿名函数的参数名称与某个局部变量、局部常量或参数的名称匹配，而该局部变量、局部常量或参数的作用域包括匿名方法表达式或 lambda 表达式，则这是编译时错误。

如果匿名函数具有显式匿名函数签名，则兼容的委托类型和表达式树类型的集合被限制为那些具有相同参数类型和修饰符且顺序相同的类型。与方法组转换（§6.6）不同，不支持匿名函数参数类型的逆变。如果匿名函数没有匿名函数签名，则兼容的委托类型和表达式树类型的集合被限制为那些没有 out 参数的类型。

注意，匿名函数签名不能包含特性或参数数组。不过，匿名函数签名可以与参数列表包含参数数组的委托类型兼容。

还要注意，即使兼容，转换为表达式树类型仍可能在编译时失败（§4.6）。

## 7.15.2 匿名函数体

匿名函数的体（表达式或块）受以下规则约束：

- 如果匿名函数包含签名，则签名中指定的参数在体中可用。如果匿名函数没有签名，则可以转换为具有参数的委托类型或表达式类型（§6.5），但在体中无法访问这些参数。
- 除最接近的封闭匿名函数（如果有）的签名中指定的 ref 或 out 参数外，体访问 ref 或 out 参数是编译时错误。
- 当 this 的类型为结构类型时，体访问 this 是编译时错误。无论访问是显式的（如 this.x）还是隐式的（如 x，其中 x 是结构的实例成员），都是如此。此规则只是禁止此类访问，不影响成员查找是否产生结构的成员。
- 体可以访问匿名函数的外部变量（§7.15.5）。访问外部变量将引用在求值 lambda 表达式或匿名方法表达式时处于活动状态的变量实例（§7.15.6）。
- 体包含目标在体之外或包含的匿名函数体之内的 goto 语句、break 语句或 continue 语句，是编译时错误。
- 体中的 return 语句从最接近的封闭匿名函数的调用返回控制，而不是从封闭函数成员返回。return 语句中指定的表达式必须可以隐式转换为最接近的封闭 lambda 表达式或匿名方法表达式所转换到的委托类型或表达式树类型的返回类型（§6.5）。

明确未指定：除了通过求值并调用 lambda 表达式或匿名方法表达式之外，是否存在任何方式执行匿名函数的块。特别是，

### 7.15.5.1 捕获的外部变量

当匿名函数引用外部变量时，称该外部变量已被匿名函数捕获。通常，局部变量的生存期仅限于执行与其关联的块或语句（§5.1.7）。然而，被捕获的外部变量的生存期至少延长到从匿名函数创建的委托或表达式树有资格进行垃圾回收为止。

在示例中

```
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
```

局部变量 x 被匿名函数捕获，x 的生存期至少延长到从 F 返回的委托有资格进行垃圾回收为止（这直到程序结束时才会发生）。由于匿名函数的每次调用都操作同一个 x 实例，示例的输出为：

1
2
3

当局部变量或值参数被匿名函数捕获时，该局部变量或参数不再被视为固定变量（§18.3），而被视为可移动变量。因此，任何获取被捕获外部变量地址的不安全代码都必须先使用 fixed 语句固定该变量。

注意，与未捕获的变量不同，被捕获的局部变量可以同时暴露给多个执行线程。

### 7.15.5.2 局部变量的实例化

当执行进入变量的作用域时，局部变量被视为已实例化。例如，调用以下方法时，局部变量 x 被实例化和初始化三次——循环的每次迭代一次。

```
```csharp
static void F() {
    for (int i = 0; i < 3; i++) {
        int x = i * 2 + 1;
        ...
    }
}
```
```

然而，将 x 的声明移到循环外部会导致 x 只实例化一次：

```
static void F() {
    int x;
    for (int j = 0; j < 3; j++) {
        x = i * 2 + 1;
    }   ...
}
```

当未被捕获时，无法确切观察局部变量被实例化的频率——因为各实例化的生存期不相交，每个实例化可以简单地使用相同的存储位置。然而，当匿名函数捕获局部变量时，实例化的效果会变得明显。

示例

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

产生输出：

1
3
5

然而，当 x 的声明移到循环外部时：

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

输出为：

5
5
5

如果 for 循环声明迭代变量，则该变量本身被视为在循环外部声明。因此，如果将示例改为捕获迭代变量本身：

```
```csharp
static D[] F() {
    D[] result = new D[3];
    for (int i = 0; i < 3; i++) {
        result[i] = () => { Console.WriteLine(i); };
    }
    return result;
}
```
```

则只捕获迭代变量的一个实例，这产生输出：

3
3
3

匿名函数委托可以共享某些捕获变量，而其他捕获变量具有单独的实例。例如，如果将 F 改为

```
```csharp
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
```

三个委托捕获同一个 x 实例，但捕获不同的 y 实例，输出为：

1 1
2 1
3 1

不同的匿名函数可以捕获同一外部变量实例。在示例中：

```
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
```

两个匿名函数捕获局部变量 x 的同一实例，因此它们可以通过该变量“通信”。示例输出为：

5
10

## 7.15.6 匿名函数表达式的求值

匿名函数 F 必须始终转换为委托类型 D 或表达式树类型 E，可以直接转换，也可以通过执行委托创建表达式 new D(F) 进行转换。此转换确定匿名函数的结果，如 §6.5 所述。



## 7.16 查询表达式

*查询表达式*为查询提供了一种语言集成语法，类似于 SQL 和 XQuery 等关系型和层次型查询语言。

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

```
group-clause:
    group expression by expression
query-continuation:
    into identifier query-body
```

查询表达式以 from 子句开始，以 select 或 group 子句结束。初始 from 子句之后可以跟零个或多个 from、let、where、join 或 orderby 子句。每个 from 子句都是一个生成器，引入一个范围变量，该范围变量在序列的元素上迭代。每个 let 子句引入一个范围变量，表示通过前面的范围变量计算得到的值。每个 where 子句都是一个筛选器，从结果中排除项。每个 join 子句将源序列的指定键与另一个序列的键进行比较，生成匹配对。每个 orderby 子句根据指定条件对项重新排序。最后的 select 或 group 子句根据范围变量指定结果的形状。最后，into 子句可用于“拼接”查询，方法是将一个查询的结果视为后续查询中的生成器。

### 7.16.1 查询表达式中的歧义

查询表达式包含若干“上下文关键字”，即，在给定上下文中具有特殊含义的标识符。具体而言，这些标识符是 from、where、join、on、equals、into、let、orderby、ascending、descending、select、group 和 by。为了避免因将这些标识符混合用作关键字或简单名称而导致查询表达式中的歧义，当这些标识符出现在查询表达式中的任何位置时，它们都被视为关键字。

为此，查询表达式是指以“from identifier”开头、后跟除“;”、“=”或“,”之外的任意标记的任何表达式。

为了在查询表达式内将这些词用作标识符，可以在它们前面加上“@”（§2.4.2）。

### 7.16.2 查询表达式转换

C# 语言不规定查询表达式的执行语义。相反，查询表达式会被转换为对遵循查询表达式模式（§7.16.3）的方法的调用。具体而言，查询表达式会被转换为对名为 where、Select、SelectMany、Join、GroupJoin、OrderBy、OrderByDescending、ThenBy、ThenByDescending、GroupBy 和 Cast 的方法的调用。这些方法应具有特定的签名和结果类型，如 §7.16.3 所述。这些方法可以是被查询对象的实例方法，也可以是该对象外部的扩展方法，它们实现查询的实际执行。

从查询表达式到方法调用的转换是一种语法映射，发生在执行任何类型绑定或重载决策之前。该转换保证语法正确，但不保证生成语义正确的 C# 代码。在查询表达式转换之后，生成的方法调用会作为常规方法调用进行处理，这反过来可能会发现错误，例如方法不存在、参数类型错误，或者方法是泛型方法而类型推断失败。

查询表达式通过反复应用以下转换来处理，直到无法再进行任何归约。这些转换按应用顺序列出：每一节都假定前面各节中的转换已被完全执行；一旦执行完毕，在处理同一查询表达式时，后面不会再回到该节。

查询表达式中不允许对范围变量赋值。但是，允许 C# 实现不总是强制实施此限制，因为对于此处给出的语法转换方案，有时可能无法做到这一点。

某些转换会注入带有由 * 表示的透明标识符的范围变量。透明标识符的特殊属性将在 §7.16.2.7 中进一步讨论。

### 7.16.2.1 带延续的 Select 和 groupby 子句

带延续的查询表达式

```
from ... into x ...
```

被转换为

```
from x in ( from ... ) ...
```

以下各节中的转换假定查询没有 into 延续。

示例

```
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```

被转换为

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

### 7.16.2.2 显式范围变量类型

显式指定范围变量类型的 from 子句

```
from T x in e
```

被转换为

```
from x in ( e ) . Cast < T > ( )
```

显式指定范围变量类型的 join 子句

```
join T x in e on k1 equals k2
```

被转换为

```
join x in ( e ) . Cast < T > ( ) on k1 equals k2
```

以下各节中的转换假定查询没有显式范围变量类型。

示例

```
from Customer c in customers
where c.City == "London"
select c
```

被转换为

```
from c in customers.Cast<Customer>()
where c.City == "London"
select c
```

其最终转换为

```
customers.
Cast<Customer>().
where(c => c.City == "London")
```

显式范围变量类型对于查询实现非泛型 IEnumerable 接口但不实现泛型 IEnumerable<T> 接口的集合很有用。在上面的示例中，如果 customers 的类型为 ArrayList，就会出现这种情况。

### 7.16.2.3 退化查询表达式

形式为

```
from x in e select x
```

的查询表达式

被转换为

```
( e ) . Select ( x => x )
```

示例

```
from c in customers
select c
```

被转换为

```
customers.Select(c => c)
```

退化查询表达式是指简单地选择源元素的一种查询表达式。转换的后续阶段会移除由其他转换步骤引入的退化查询，方法是将其替换为它们的源。然而，重要的是确保查询表达式的结果永远不会是源对象本身，因为这会向查询客户端泄露源的类型和标识。因此，此步骤通过在源上显式调用 Select 来保护直接在源代码中编写的退化查询。然后，Select 和其他查询运算符的实现者需要确保这些方法永远不会返回源对象本身。

### 7.16.2.4 From、let、where、join 和 orderby 子句

带第二个 from 子句且后跟 select 子句的查询表达式

```
from x1 in e1
from x2 in e2
select v
```

被转换为

```
( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => v )
```

**带 where 子句的查询表达式**

```
from x in e
where f
...
```

被转换为

```
from x in ( e ) . Where ( x => f )
...
```

**带不带 into 的 join 子句且后跟 select 子句的查询表达式**

```
from x1 in e1
join x2 in e2 on k1 equals k2
select v
```

被转换为

```
( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => v )
```

**带不带 into 的 join 子句且后跟 select 子句以外内容的查询表达式**

```
from x1 in e1
join x2 in e2 on k1 equals k2
...
```

被转换为

```
from * in ( e1 ) . Join(
    e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => new { x1 , x2 })
...
```

**带 into 的 join 子句且后跟 select 子句的查询表达式**

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
select v
```

被转换为

```
( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => v )
```

**带 into 的 join 子句且后跟 select 子句以外内容的查询表达式**

```
from x1 in e1
join x2 in e2 on k1 equals k2 into g
```

被转换为

```
from * in ( e1 ) . GroupJoin(
    e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => new { x1 , g })
...
```

**带 orderby 子句的查询表达式**

```
from x in e
orderby k1 , k2 , ... , kn
...
```

被转换为

## C# 语言规范

```
from x in ( e ) .
OrderBy ( x => k1 ) .
ThenBy ( x => k2 ) .
...
ThenBy ( x => kn )
...
```

如果排序子句指定降序方向指示符，则改为生成对 OrderByDescending 或 ThenByDescending 的调用。

以下转换假设不存在 let、where、join 或 orderby 子句，并且每个查询表达式中至多有一个初始 from 子句。

示例

```
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```

转换为

```
customers.
SelectMany(c => c.Orders,
(c,o) => new { c.Name, o.OrderID, o.Total }
)
```

示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

转换为

```
from * in customers.
SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```

其最终转换为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.OrderID, x.o.Total })
```

其中 x 是编译器生成的标识符，除此之外不可见且不可访问。

示例

```
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```

转换为

```
from * in orders.
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000
select new { o.OrderID, Total = t }
```

其最终转换为

```
orders.
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) }).
Where(x => x.t >= 1000).
Select(x => new { x.o.OrderID, Total = x.t })
```

其中 x 是编译器生成的标识符，除此之外不可见且不可访问。

示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
select new { c.Name, o.OrderDate, o.Total }
```

转换为

```
customers.Join(orders, c => c.CustomerID, o => o.CustomerID,
(c, o) => new { c.Name, o.OrderDate, o.Total })
```

示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID into co
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```

转换为

```
from * in customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
(c, co) => new { c, co })
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```

其最终转换为

```
customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
(c, co) => new { c, co }).
Select(x => new { x, n = x.co.Count() }).
Where(y => y.n >= 10).
Select(y => new { y.x.c.Name, OrderCount = y.n })
```

其中 x 和 y 是编译器生成的标识符，除此之外不可见且不可访问。

示例

```
from o in orders
orderby o.Customer.Name, o.Total descending
select o
```

最终转换为

```
orders.
OrderBy(o => o.Customer.Name).
ThenByDescending(o => o.Total)
```

## 7.16.2.5 Select 子句

形式为

```
from x in e select v
```

的查询表达式转换为

```
( e ) . Select ( x => v )
```

除非 v 是标识符 x，此时转换就是

```
( e )
```

例如

```
from c in customers.Where(c => c.City == "London")
select c
```

直接转换为

```
customers.Where(c => c.City == "London")
```

## 7.16.2.6 Groupby 子句

形式为

```
from x in e group v by k
```

的查询表达式转换为

```
( e ) . GroupBy ( x => k , x => v )
```

除非 v 是标识符 x，此时转换为

```
( e ) . GroupBy ( x => k )
```

示例

```
from c in customers
group c.Name by c.Country
```

转换为

```
customers.
GroupBy(c => c.Country, c => c.Name)
```

## 7.16.2.7 透明标识符

某些转换会注入带有由 * 表示的透明标识符的范围变量。透明标识符不是正式的语言功能；它们仅作为查询表达式转换过程中的中间步骤存在。

当查询转换注入透明标识符时，后续转换步骤会将透明标识符传播到匿名函数和匿名对象初始值设定项中。在这些上下文中，透明标识符具有以下行为：

- 当透明标识符作为匿名函数中的参数出现时，关联匿名类型的成员会自动位于该匿名函数体内的作用域中。
- 当带有透明标识符的成员位于作用域中时，该成员的成员也位于作用域中。
- 当透明标识符作为匿名对象初始值设定项中的成员声明符出现时，它会引入一个带有透明标识符的成员。

在上述转换步骤中，透明标识符始终与匿名类型一起引入，目的是将多个范围变量捕获为单个对象的成员。C# 实现可以使用不同于匿名类型的机制来将多个范围变量组合在一起。

示例

```
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```

转换为

```
from * in customers.
    SelectMany(c => c.Orders, (c,o) => new { c, o })
    orderby o.Total descending
    select new { c.Name, o.Total }
```

其进一步转换为

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(* => o.Total).
Select(* => new { c.Name, o.Total })
```

其中，当透明标识符被擦除后，等效于

```
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.Total })
```

其中 x 是编译器生成的标识符，除此之外不可见且不可访问。

示例

```
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```

转换为

```
from * in customers.
    Join(orders, c => c.CustomerID, o => o.CustomerID,
        (c, o) => new { c, o })
    join d in details on o.OrderID equals d.OrderID
    join p in products on d.ProductID equals p.ProductID
    select new { c.Name, o.OrderDate, p.ProductName }
```

其进一步简化为

```
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o }).
Join(details, * => o.OrderID, d => d.OrderID, (*, d) => new { *, d }).
Join(products, * => d.ProductID, p => p.ProductID, (*, p) => new { *, p }).
Select(* => new { c.Name, o.OrderDate, p.ProductName })
```

其最终转换为

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

其中 x、y 和 z 是编译器生成的标识符，除此之外不可见且不可访问。

## 7.16.3 查询表达式模式

查询表达式模式建立了一种方法模式，类型可以实现该模式以支持查询表达式。由于查询表达式通过语法映射被转换为方法调用，因此类型在如何实现查询表达式模式方面具有相当大的灵活性。例如，该模式的方法可以实现为实例方法或扩展方法，因为两者具有相同的调用语法；并且这些方法可以要求委托或表达式树，因为匿名函数可转换为两者。

下面展示了支持查询表达式模式的泛型类型 C<T> 的建议形式。使用泛型类型是为了说明参数类型和结果类型之间的正确关系，但也完全可以为非泛型类型实现该模式。

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
    public C<V> SelectMany<U,V>(Func<T,C<U>> selector,
        Func<T,U,V> resultsSelector);
    public C<U> Join<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,U,V> resultSelector);
    public C<V> GroupJoin<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,C<U>,V> resultSelector);
    public O<T> OrderBy<K>(Func<T,K> keySelector);
    public O<T> OrderByDescending<K>(Func<T,K> keySelector);
    public C<K,T> GroupBy<K>(Func<T,K> keySelector);
    public C<G<K,E>> GroupBy<K,E>(Func<T,K> keySelector,
        Func<T,K,E> elementSelector);
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

上述方法使用泛型委托类型 Func<T1, R> 和 Func<T1, T2, R>，但它们同样可以使用在参数类型和结果类型中具有相同关系的其他委托或表达式树类型。

请注意 C<T> 和 O<T> 之间的建议关系，该关系确保 ThenBy 和 ThenByDescending 方法仅可用于 OrderBy 或 OrderByDescending 的结果。另请注意 GroupBy 结果的建议形式——一个序列的序列，其中每个内部序列都有一个额外的 Key 属性。

System.Linq 命名空间为任何实现 System.Collections.Generic.IEnumerable<T> 接口的类型提供查询运算符模式的实现。

## 7.17 赋值运算符

赋值运算符将新值赋给变量、属性、事件或索引器元素。

```
assignment:
    unary-expression assignment-operator expression
```





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
  >>= 

赋值的左操作数必须是归类为变量、属性访问、索引器访问或事件访问的表达式。

= 运算符称为简单赋值运算符。它将右操作数的值赋给左操作数所给定的变量、属性或索引器元素。简单赋值运算符的左操作数不能是事件访问（§10.8.1 所述情况除外）。简单赋值运算符在 §7.17.1 中描述。

除 = 运算符以外的赋值运算符称为复合赋值运算符。这些运算符对两个操作数执行指定的运算，然后将结果值赋给左操作数所给定的变量、属性或索引器元素。复合赋值运算符在 §7.17.2 中描述。

左操作数为事件访问表达式的 += 和 -= 运算符称为事件赋值运算符。其他任何赋值运算符都不能以事件访问作为左操作数。事件赋值运算符在 §7.17.3 中描述。

赋值运算符是右结合的，这意味着运算从右向左分组。例如，形式为 a = b = c 的表达式按 a = (b = c) 求值。

## 7.17.1 简单赋值

= 运算符称为简单赋值运算符。

如果简单赋值的左操作数形式为 E.P 或 E[E_i]，其中 E 的编译时类型为 dynamic，则该赋值采用动态绑定（§7.2.2）。在这种情况下，赋值表达式的编译时类型为 dynamic，下面描述的解析将在运行时基于 E 的运行时类型进行。

在简单赋值中，右操作数必须是可隐式转换为左操作数类型的表达式。该运算将右操作数的值赋给左操作数所给定的变量、属性或索引器元素。

形式为 x = y 的简单赋值的运行时处理包括以下步骤：

- 如果 x 归类为变量：
  - 对 x 求值以生成该变量。
  - 对 y 求值，并在需要时通过隐式转换（§6.1）转换为 x 的类型。
- 如果 x 给出的变量是引用类型的数组元素，则执行运行时检查，以确保为 y 计算出的值与包含 x 的数组实例兼容。如果 y 为 null，或者从 y 所引用实例的实际类型到包含 x 的数组实例的实际元素类型存在隐式引用转换（§6.1.6），则检查成功。否则，抛出 System.ArrayTypeMismatchException。
- 对 y 求值并转换后得到的值存储到对 x 求值所给出的位置中。
- 如果 x 归类为属性访问或索引器访问：
  - 对与 x 关联的实例表达式（如果 x 不是 static）和实参列表（如果 x 是索引器访问）求值，结果用于后续的 set 访问器调用。
  - 对 y 求值，并在需要时通过隐式转换（§6.1）转换为 x 的类型。
  - 调用 x 的 set 访问器，以计算出的 y 值作为其 value 实参。

数组协变规则（§12.5）允许数组类型 A[] 的值作为数组类型 B[] 实例的引用，前提是存在从 B 到 A 的隐式引用转换。由于这些规则，对引用类型的数组元素赋值需要运行时检查，以确保所赋的值与数组实例兼容。在以下示例中

```
string[] sa = new string[10];
object[] oa = sa;

oa[0] = null;    // Ok
oa[1] = "Hello"; // Ok
oa[2] = new ArrayList(); // ArrayTypeMismatchException
```

最后一个赋值会导致抛出 System.ArrayTypeMismatchException，因为 ArrayList 的实例不能存储在 string[] 的元素中。

当结构类型中声明的属性或索引器是赋值目标时，与该属性或索引器访问关联的实例表达式必须归类为变量。如果实例表达式归类为值，则发生绑定期错误。由于 §7.6.4，同样的规则也适用于字段。

给定以下声明：

```
struct Point
{
    int x, y;
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
}
struct Rectangle
{
    Point a, b;
}
```

```
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
```

在以下示例中

```
Point p = new Point();
p.X = 100;
p.Y = 100;
Rectangle r = new Rectangle();
r.A = new Point(10, 10);
r.B = p;
```

对 p.X、p.Y、r.A 和 r.B 的赋值是允许的，因为 p 和 r 是变量。然而，在以下示例中

```
Rectangle r = new Rectangle();
r.A.X = 10;
r.A.Y = 10;
r.B.X = 100;
r.B.Y = 100;
```

这些赋值全都无效，因为 r.A 和 r.B 不是变量。

## 7.17.2 复合赋值

如果复合赋值的左操作数形式为 E.P 或 E[E_i]，其中 E 的编译时类型为 dynamic，则该赋值采用动态绑定（§7.2.2）。在这种情况下，赋值表达式的编译时类型为 dynamic，下面描述的解析将在运行时基于 E 的运行时类型进行。

形式为 x op= y 的运算按如下方式处理：先像该运算写成 x op y 一样应用二元运算符重载决策（§7.3.4）。然后，

- 如果所选运算符的返回类型可隐式转换为 x 的类型，则按 x = x op y 对该运算求值，但 x 只求值一次。
- 否则，如果所选运算符是预定义运算符，如果所选运算符的返回类型可显式转换为 x 的类型，并且 y 可隐式转换为 x 的类型或该运算符是移位运算符，则按 x = (T) (x op y) 对该运算求值，其中 T 是 x 的类型，但 x 只求值一次。
- 否则，复合赋值无效，并发生绑定期错误。

术语“只求值一次”意味着：在对 x op y 求值时，x 的任意组成表达式的结果都会被临时保存，然后在执行对 x 的赋值时重用。例如，在赋值 A()[B()] += C() 中，A 是返回 int[] 的方法，B 和 C 是返回 int 的方法，这些方法只按 A、B、C 的顺序调用一次。

当复合赋值的左操作数是属性访问或索引器访问时，该属性或索引器必须同时具有 get 访问器和 set 访问器。如果不是这样，则发生绑定期错误。

上面的第二条规则允许在某些上下文中将 x op= y 求值为 x = (T) (x op y)。该规则的存在是为了：当左操作数的类型为 sbyte、byte、short、ushort 或 char 时，可以将预定义运算符用作复合运算符。即使两个参数都是这些类型之一，预定义运算符也会产生 int 类型的结果，如 §7.3.6.2 所述。因此，如果不进行强制转换，就无法将结果赋给左操作数。

对于预定义运算符，该规则的直观效果很简单：如果 x op y 和 x = y 都允许，则允许 x op= y。在以下示例中

```
byte b = 0;
char ch = '\0';
int i = 0;

b += 1;      // Ok
b += 1000;   // Error, b = 1000 not permitted
b += i;      // Error, b = i not permitted
b += (byte)i; // Ok

ch += 1;     // Error, ch = 1 not permitted
ch += (char)1; // Ok
```

每个错误的直观原因在于，对应的简单赋值也会出错。

这也意味着复合赋值运算支持提升运算。在以下示例中

```
int? i = 0;
i += 1;      // Ok
```

使用的是提升运算符 +(int?, int?)。

## 7.17.3 事件赋值

如果 += 或 -= 运算符的左操作数归类为事件访问，则按如下方式对该表达式求值：

- 对事件访问的实例表达式（如果有）求值。
- 对 += 或 -= 运算符的右操作数求值，并在需要时通过隐式转换（§6.1）将其转换为左操作数的类型。
- 调用该事件的某个事件访问器，其参数列表由求值并（如有必要）转换后的右操作数组成。如果运算符是 +=，则调用 add 访问器；如果运算符是 -=，则调用 remove 访问器。

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

常量表达式是可在编译时完全求值的表达式。




## 常量表达式:
    expression

常量表达式必须是 null 字面量或具有以下类型之一的值：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool、string，或任何枚举类型。仅允许在常量表达式中使用以下构造：

- 字面量（包括 null 字面量）。
- 对类和结构体类型的 const 成员的引用。
- 对枚举类型成员的引用。
- 对 const 参数或局部变量的引用
- 括号化的子表达式，其本身也是常量表达式。
- 强制转换表达式，前提是目标类型是上面列出的类型之一。
- checked 和 unchecked 表达式
- 默认值表达式
- 预定义的 +、-、! 和 ~ 一元运算符。
- 预定义的 +、-、*、/、% 、<<、>>、&、|、^、&&、||、==、!=、<、>、<= 和 >= 二元运算符，前提是每个操作数都是上面列出的类型之一。
- ?: 条件运算符。

以下转换允许在常量表达式中使用：

- 恒等转换
- 数值转换
- 枚举转换
- 常量表达式转换
- 隐式和显式引用转换，前提是转换的源是一个求值为 null 值 的常量表达式。

其他转换包括装箱、拆箱以及非 null 值的隐式引用转换，不允许在常量表达式中使用。例如：

```
class C {
    const object i = 5; // error: boxing conversion not permitted
    const object str = "hello"; // error: implicit reference conversion
}
```

i 的初始化是一个错误，因为需要装箱转换。str 的初始化是一个错误，因为需要从非 null 值进行隐式引用转换。

每当表达式满足上面列出的要求时，表达式将在编译时求值。即使该表达式是包含非常量构造的较大表达式的子表达式，也成立。

常量表达式的编译时求值使用与非常量表达式的运行时求值相同的规则，只是运行时求值会抛出异常的地方，编译时求值会导致编译时错误发生。

除非常量表达式明确放置在 unchecked 上下文中，否则在表达式的编译时求值期间，整数类型算术运算和转换中发生的溢出始终会导致编译时错误（§7.19）。

常量表达式出现在下面列出的上下文中。在这些上下文中，如果表达式不能在编译时完全求值，则会发生编译时错误。

- 常量声明（§10.4）。
- 枚举成员声明（§14.3）。
- switch 语句的 case 标签（§8.7.2）。
- goto case 语句（§8.9.3）。
- 包含初始值设定项的数组创建表达式中的维度长度（§7.6.10.4）。
- 属性（§17）。

隐式常量表达式转换（§6.1.8）允许将类型为 int 的常量表达式转换为 sbyte、byte、short、ushort、uint 或 ulong，前提是常量表达式的值在目标类型的范围内。

## 7.20 布尔表达式

布尔表达式是一个表达式，其结果类型为 bool；要么直接，要么通过在以下指定的某些上下文中应用 operator true。

```
boolean-expression:
    expression
```

if 语句（§8.7.1）、while 语句（§8.8.1）、do 语句（§8.8.2）或 for 语句（§8.8.3）的控制条件表达式是布尔表达式。?: 运算符（§7.14）的控制条件表达式遵循与布尔表达式相同的规则，但由于运算符优先级的缘故，被归类为条件或表达式。

布尔表达式必须能够隐式转换为 bool，或为实现了 operator true 的类型。如果两个要求均不满足，则会发生绑定时错误。

当布尔表达式不能隐式转换为 bool 但实现了 operator true 时，则在求值表达式后，将调用该类型提供的 operator true 实现以生成 bool 值。

§11.4.2 中的 DBBool 结构体类型提供了实现 operator true 和 operator false 的类型的示例。

## 8. 语句

C# 提供了多种语句。大多数语句对曾使用 C 和 C++ 编程的开发人员来说都很熟悉。

- *语句:*
  *标记语句*
  *声明语句*
  *嵌入语句*

- *嵌入语句:*
  *块*
  *空语句*
  *表达式语句*
  *选择语句*
  *迭代语句*
  *跳转语句*
  *try 语句*
  *checked 语句*
  *unchecked 语句*
  *lock 语句*
  *using 语句*
  *yield 语句*

*嵌入语句* 非终结符用于出现在其他语句内的语句。 使用 *嵌入语句* 而不是 *语句* 排除了在这些上下文中使用声明语句和标记语句。 示例

```
void F(bool b) {
    if (b)
        int i = 44;
}
```

结果会产生编译时错误，因为一个 *if* 语句需要一个 *嵌入语句* 而不是一个 *语句* 作为其 *if* 分支。如果允许此代码，则变量 *i* 将被声明，但永远无法使用。 然而请注意，通过将 *i* 的声明放在块中，示例是有效的。

### 8.1 终点和可达性

每个语句都有一个 *终点*。直观地说，语句的终点是紧跟在该语句之后的位置。复合语句（包含嵌入语句的语句）的执行规则指定了当控制到达嵌入语句的终点时采取的操作。例如，当控制到达块中语句的终点时，控制会转移到块中的下一条语句。

如果语句可能通过执行到达，则该语句被称为 *可达*。相反，如果语句永远不会被执行，则该语句被称为 *不可达*。

在示例中

```csharp
void F() {
    Console.WriteLine("reachable");
    goto Label1;
    Console.WriteLine("unreachable");
    Label1:
    Console.WriteLine("reachable");
}
```

第二个 Console.WriteLine 调用是不可达的，因为没有可能执行该语句。

如果编译器确定语句不可达，则会报告警告。特别地，语句不可达不是错误。

为了确定特定语句或终点是否可达，编译器根据为每个语句定义的<|message|> 可达性规则执行流分析。流分析会考虑控制语句行为的常量表达式（§7.19）的值，但不考虑非常量表达式的可能值。换句话说，对于控制流分析的目的，非常量表达式被认为具有该类型的任何可能值。

在示例中

```csharp
void F() {
    const int i = 1;
    if (i == 2) Console.WriteLine("unreachable");
}
```

if 语句的布尔表达式是常量表达式，因为 == 运算符的两个操作数都是常量。由于常量表达式在编译时求值，产生值 false，因此 Console.WriteLine 调用被认为不可达。然而，如果将 i 改为局部变量

```csharp
void F() {
    int i = 1;
    if (i == 2) Console.WriteLine("reachable");
}
```

Console.WriteLine 调用被认为可达，即使实际上它永远不会被执行。

函数成员的块始终被认为可达。通过依次评估块中每个语句的可达性规则，可以确定任何给定语句的可达性。

在示例中

```csharp
void F(int x) {
    Console.WriteLine("start");
    if (x < 0) Console.WriteLine("negative");
}
```

第二个 Console.WriteLine 的可达性确定如下：

- 第一个 Console.WriteLine 表达式语句是可达的，因为 F 方法的块是可达的。
- 第一个 Console.WriteLine 表达式语句的终点是可达的，因为该语句是可达的。
- if 语句是可达的，因为第一个 Console.WriteLine 表达式语句的终点是可达的。
- 第二个 Console.WriteLine 表达式语句是可达的，因为 if 语句的布尔表达式不具有常量值 false。

存在两种情况，如果语句的终点可达，则为编译时错误：

- 由于 switch 语句不允许一个 switch 节“贯穿”到下一个 switch 节，因此 switch 节的语句列表的结束点可达是编译时错误。如果出现此错误，通常表明缺少 break 语句。
- 计算值的函数成员的块的结束点可达是编译时错误。如果出现此错误，通常表明缺少 return 语句。

## 8.2 块

块允许在只允许单个语句的上下文中编写多个语句。

```
block:
{ statement-list_opt }
```

块由可选的语句列表（§8.2.1）组成，并括在大括号中。如果省略语句列表，则称该块为空。

块可以包含声明语句（§8.5）。在块中声明的局部变量或常量的作用域是该块。

在块内，表达式上下文中使用的名称的含义必须始终相同（§7.6.2.1）。

块的执行方式如下：

- 如果块为空，控制转移到块的结束点。
- 如果块不为空，控制转移到语句列表。当控制到达（且如果到达）语句列表的结束点时，控制转移到块的结束点。

如果块本身可达，则块的语句列表可达。

如果块为空，或者语句列表的结束点可达，则块的结束点可达。

包含一个或多个 yield 语句（§8.14）的块称为迭代器块。迭代器块用于将函数成员实现为迭代器（§10.14）。迭代器块还适用一些附加限制：

- return 语句出现在迭代器块中是编译时错误（但允许 yield return 语句）。
- 迭代器块包含不安全上下文（§18.1）是编译时错误。迭代器块始终定义安全上下文，即使其声明嵌套在不安全上下文中也是如此。

### 8.2.1 语句列表

语句列表由一个或多个按顺序编写的语句组成。语句列表出现在块（§8.2）和 switch 块（§8.7.2）中。

```
statement-list:
    statement
    statement-list statement
```

语句列表的执行方式是将控制转移到第一个语句。当控制到达（且如果到达）某个语句的结束点时，控制转移到下一个语句。当控制到达（且如果到达）最后一个语句的结束点时，控制转移到语句列表的结束点。

语句列表中的语句在以下至少一项为真时可达：

- 该语句是第一个语句，且语句列表本身可达。
- 前一个语句的结束点可达。
- 该语句是带标签语句，且该标签被一个可达的 goto 语句引用。

如果列表中最后一个语句的结束点可达，则语句列表的结束点可达。

## 8.3 空语句

空语句不执行任何操作。

```
empty-statement:
;
```

当在需要语句的上下文中没有要执行的操作时，使用空语句。

空语句的执行只是将控制转移到该语句的结束点。因此，如果空语句可达，则空语句的结束点可达。

在编写具有 null 主体的 while 语句时，可以使用空语句：

```
bool ProcessMessage() {...}
void ProcessMessages() {
    while (ProcessMessage())
    ;
}
```

此外，空语句可用于在块的右大括号“}”之前声明标签：

```
void F() {
    ...
    if (done) goto exit;
    ...
}
exit: ;
```

## 8.4 带标签语句

带标签语句允许在语句前面加上标签。带标签语句允许出现在块中，但不允许作为嵌入语句。

```
labeled-statement:
    identifier : statement
```

带标签语句声明一个名称由标识符给出的标签。标签的作用域是声明该标签的整个块，包括任何嵌套块。两个同名标签的作用域重叠是编译时错误。

在标签的作用域内，可以从 goto 语句（§8.9.3）引用标签。这意味着 goto 语句可以在块内以及从块内向外转移控制，但绝不能转入块内。

标签有自己的声明空间，不会干扰其他标识符。示例

```
int F(int x) {
    if (x >= 0) goto x;
    x = -x;
    x: return x;
}
```

是有效的，并将名称 x 同时用作参数和标签。

带标签语句的执行与标签后语句的执行完全对应。

除了正常控制流提供的可达性之外，如果标签被一个可达的 goto 语句引用，则该带标签语句也可达。（例外：如果 goto 语句位于包含 finally 块的 try 内，而带标签语句位于该 try 之外，并且 finally 块的结束点不可达，则该带标签语句从该 goto 语句不可达。）

## 8.5 声明语句

声明语句声明局部变量或常量。声明语句允许出现在块中，但不允许作为嵌入语句。

```
declaration-statement:
    local-variable-declaration ;
    local-constant-declaration ;
```

### 8.5.1 局部变量声明

局部变量声明声明一个或多个局部变量。

```
local-variable-declaration:
    local-variable-type  local-variable-declarators

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

局部变量声明的 local-variable-type 要么直接指定该声明引入的变量的类型，要么用标识符 var 表示应根据初始值设定项推断类型。类型后跟一个局部变量声明符列表，其中每个声明符引入一个新变量。局部变量声明符由一个命名该变量的标识符组成，后面可选地跟一个“=”标记以及一个给出该变量初始值的局部变量初始值设定项。

在局部变量声明的上下文中，标识符 var 充当上下文关键字（§2.4.3）。当 local-variable-type 指定为 var 且作用域中没有名为 var 的类型时，该声明是隐式类型局部变量声明，其类型从关联的初始值设定项表达式的类型推断。隐式类型局部变量声明受以下限制：

- 局部变量声明不能包含多个局部变量声明符。
- 局部变量声明符必须包含局部变量初始值设定项。
- 局部变量初始值设定项必须是表达式。
- 初始值设定项表达式必须具有编译时类型。
- 初始值设定项表达式不能引用所声明的变量本身

以下是错误的隐式类型局部变量声明示例：

```
var x;          // Error, no initializer to infer type from
var y = {1, 2, 3};  // Error, array initializer not permitted
var z = null;   // Error, null does not have a type
var u = x => x + 1; // Error, anonymous functions do not have a type
var v = v++;    // Error, initializer cannot refer to variable itself
```

局部变量的值在表达式中使用简单名称（§7.6.2）获取，局部变量的值使用赋值（§7.17）修改。在每个获取其值的位置，局部变量必须明确赋值（§5.3）。

在局部变量声明中声明的局部变量的作用域是出现该声明的块。在文本位置上引用位于该局部变量的局部变量声明符之前的局部变量是错误的。在局部变量的作用域内，声明另一个同名局部变量或常量是编译时错误。

声明多个变量的局部变量声明等效于多个具有相同类型的单变量声明。此外，局部变量声明中的变量初始值设定项完全对应于紧接在该声明之后插入的赋值语句。

示例

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

在隐式类型局部变量声明中，所声明的局部变量的类型被视为与用于初始化该变量的表达式的类型相同。例如：

```
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
```

上面的隐式类型局部变量声明完全等效于以下显式类型声明：

```
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
```

### 8.5.2 局部常量声明

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

局部常量声明的类型指定该声明引入的常量的类型。类型后跟一个常量声明符列表，其中每个声明符引入一个新常量。常量声明符由一个命名该常量的标识符组成，后面跟一个“=”标记，再后面跟一个给出该常量值的常量表达式（§7.19）。



局部常量声明的类型和常量表达式必须遵循与常量成员声明（§10.4）相同的规则。局部常量的值通过在表达式中使用简单名称（§7.6.2）来获取。局部常量的作用域是其中发生声明的块。在文本位置上引用位于其常量声明符之前的局部常量是错误的。在局部常量的作用域内，声明另一个具有相同名称的局部变量或常量是编译时错误。声明多个常量的局部常量声明等效于多个具有相同类型的单个常量的声明。

## 8.6 表达式语句

表达式语句计算给定表达式。表达式计算出的值（如果有）将被丢弃。

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

并非所有表达式都允许作为语句。特别是，像 x + y 和 x == 1 这样仅计算一个值（该值将被丢弃）的表达式不允许作为语句。

表达式语句的执行会计算所含表达式，然后将控制转移到该表达式语句的结束点。如果该表达式语句可到达，则该表达式语句的结束点可到达。

## 8.7 选择语句

选择语句根据某个表达式的值，选择若干可能语句中的一个来执行。

```
selection-statement:
    if-statement
    switch-statement
```

### 8.7.1 if 语句

if 语句根据布尔表达式的值选择一个语句来执行。

```
if-statement:
    if ( boolean-expression ) embedded-statement
    if ( boolean-expression ) embedded-statement else embedded-statement
```

else 部分与语法允许的词法上最近的前面 if 相关联。因此，形式为 if (x) if (y) F(); else G(); 的 if 语句等效于

C# 语言规范

```csharp
if (x) {
    if (y) {
        F();
    }
    else {
        G();
    }
}
```

if 语句按如下方式执行：

- 计算布尔表达式（§7.20）。
- 如果布尔表达式产生 true，则控制转移到第一个内嵌语句。当控制到达该语句的结束点时，控制转移到 if 语句的结束点。
- 如果布尔表达式产生 false 且存在 else 部分，则控制转移到第二个内嵌语句。当控制到达该语句的结束点时，控制转移到 if 语句的结束点。
- 如果布尔表达式产生 false 且不存在 else 部分，则控制转移到 if 语句的结束点。

如果 if 语句可到达且布尔表达式不具有常量值 false，则 if 语句的第一个内嵌语句可到达。

如果 if 语句可到达且布尔表达式不具有常量值 true，则 if 语句的第二个内嵌语句（如果存在）可到达。

如果 if 语句的至少一个内嵌语句的结束点可到达，则该 if 语句的结束点可到达。此外，如果 if 语句可到达且布尔表达式不具有常量值 true，则不带 else 部分的 if 语句的结束点可到达。

### 8.7.2 switch 语句

switch 语句选择具有与 switch 表达式的值对应的关联 switch 标签的语句列表来执行。

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
switch-labels:
    switch-label
    switch-labels switch-label
switch-label:
    case constant-expression :
    default :
```

switch 语句由关键字 switch、后跟带括号的表达式（称为 switch 表达式），再后跟 switch 块组成。switch 块由零个或多个 switch 节组成，并括在大括号中。每个 switch 节由一个或多个 switch 标签后跟语句列表（§8.2.1）组成。

switch 语句的主导类型由 switch 表达式确定。

- 如果 switch 表达式的类型是 sbyte、byte、short、ushort、int、uint、long、ulong、bool、char、string 或枚举类型，或者它是对应于这些类型之一的可空类型，那么该类型就是 switch 语句的主导类型。
- 否则，必须存在恰好一个从 switch 表达式的类型到以下可能主导类型之一的用户定义隐式转换（§6.4）：sbyte、byte、short、ushort、int、uint、long、ulong、char、string，或对应于这些类型之一的可空类型。
- 否则，如果不存在此类隐式转换，或者存在多个此类隐式转换，则发生编译时错误。

每个 case 标签的常量表达式必须表示一个可隐式转换（§6.1）为 switch 语句主导类型的值。如果同一个 switch 语句中的两个或多个 case 标签指定相同的常量值，则发生编译时错误。

一个 switch 语句中最多只能有一个 default 标签。

switch 语句按如下方式执行：

- 计算 switch 表达式并将其转换为主导类型。
- 如果同一个 switch 语句中某个 case 标签指定的常量之一等于 switch 表达式的值，则控制转移到匹配的 case 标签后面的语句列表。
- 如果同一个 switch 语句中 case 标签指定的常量均不等于 switch 表达式的值，且存在 default 标签，则控制转移到 default 标签后面的语句列表。
- 如果同一个 switch 语句中 case 标签指定的常量均不等于 switch 表达式的值，且不存在 default 标签，则控制转移到 switch 语句的结束点。

如果 switch 节的语句列表的结束点可到达，则发生编译时错误。这称为“无贯穿”规则。示例

```
switch (i) {
    case 0:
        caseZero();
        break;
    case 1:
        caseOne();
        break;
    default:
        caseOthers();
        break;
}
```

是有效的，因为没有 switch 节的结束点可到达。与 C 和 C++ 不同，不允许 switch 节的执行“贯穿”到下一个 switch 节，而示例

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

会导致编译时错误。当执行一个 switch 节之后要执行另一个 switch 节时，必须使用显式的 goto case 或 goto default 语句：

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

一个 switch 节中允许多个标签。示例

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

是有效的。该示例不违反“无贯穿”规则，因为标签 case 2: 和 default: 是同一个 switch 节的一部分。

“无贯穿”规则可防止 C 和 C++ 中因意外省略 break 语句而发生的一类常见缺陷。此外，由于此规则，switch 语句的各个 switch 节可以任意重新排列，而不会影响该语句的行为。例如，上述 switch 语句的各节可以反转，而不会影响该语句的行为：

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

switch 节的语句列表通常以 break、goto case 或 goto default 语句结尾，但任何使语句列表的结束点不可到达的构造都是允许的。例如，由布尔表达式 true 控制的 while 语句已知永远不会到达其结束点。同样，throw 或 return 语句总是将控制转移到其他地方，并且永远不会到达其结束点。因此，以下示例是有效的：

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

与字符串相等运算符（§7.10.7）类似，switch 语句区分大小写，并且仅当 switch 表达式字符串与某个 case 标签常量完全匹配时，才会执行给定的 switch 节。

当 switch 语句的控制类型为 string 时，允许将 null 值作为 case 标签常量。

switch 块的语句列表可以包含声明语句（§8.5）。在 switch 块中声明的局部变量或常量的作用域是该 switch 块。

在 switch 块内，在表达式上下文中使用的名称的含义必须始终相同（§7.6.2.1）。

如果 switch 语句可到达，并且下列条件中至少有一项为真，则给定 switch 节的语句列表可到达：

- switch 表达式是非常量值。
- switch 表达式是与该 switch 节中的某个 case 标签匹配的常量值。
- switch 表达式是不匹配任何 case 标签的常量值，并且该 switch 节包含 default 标签。
- 该 switch 节的某个 switch 标签被可到达的 goto case 或 goto default 语句引用。

如果下列条件中至少有一项为真，则 switch 语句的结束点可到达：

- switch 语句包含一个可到达的 break 语句，该语句退出 switch 语句。
- switch 语句可到达，switch 表达式是非常量值，并且不存在 default 标签。
- switch 语句可到达，switch 表达式是不匹配任何 case 标签的常量值，并且不存在 default 标签。

## 8.8 迭代语句

迭代语句重复执行嵌入语句。

```
iteration-statement:
while-statement
do-statement
for-statement
foreach-statement
```

### 8.8.1 while 语句

while 语句有条件地执行嵌入语句零次或多次。

```
while-statement:
while ( boolean-expression ) embedded-statement
```

while 语句按如下方式执行：

- 计算布尔表达式（§7.20）。
- 如果布尔表达式的结果为 true，则控制转移到嵌入语句。当控制到达嵌入语句的结束点（可能来自执行 continue 语句）时，控制转移到 while 语句的开头。
- 如果布尔表达式的结果为 false，则控制转移到 while 语句的结束点。

在 while 语句的嵌入语句中，可以使用 break 语句（§8.9.1）将控制转移到 while 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点（从而执行 while 语句的下一次迭代）。

如果 while 语句可到达，并且布尔表达式不具有常量值 false，则 while 语句的嵌入语句可到达。

如果下列条件中至少有一项为真，则 while 语句的结束点可到达：

- while 语句包含一个可到达的 break 语句，该语句退出 while 语句。
- while 语句可到达，并且布尔表达式不具有常量值 true。

### 8.8.2 do 语句

do 语句有条件地执行嵌入语句一次或多次。

```
do-statement:
do embedded-statement while ( boolean-expression ) ;
```

do 语句按如下方式执行：

- 控制转移到嵌入语句。
- 当控制到达嵌入语句的结束点（可能来自执行 continue 语句）时，计算布尔表达式（§7.20）。如果布尔表达式的结果为 true，则控制转移到 do 语句的开头。否则，控制转移到 do 语句的结束点。

在 do 语句的嵌入语句中，可以使用 break 语句（§8.9.1）将控制转移到 do 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点。

如果 do 语句可到达，则 do 语句的嵌入语句可到达。

如果下列条件中至少有一项为真，则 do 语句的结束点可到达：

- do 语句包含一个可到达的 break 语句，该语句退出 do 语句。
- 嵌入语句的结束点可到达，并且布尔表达式不具有常量值 true。

### 8.8.3 for 语句

for 语句计算一系列初始化表达式，然后，在条件为 true 时，重复执行嵌入语句并计算一系列迭代表达式。

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

for 初始值设定项（如果存在）由局部变量声明（§8.5.1）或以逗号分隔的语句表达式列表（§8.6）组成。由 for 初始值设定项声明的局部变量的作用域从该变量的局部变量声明符开始，一直延伸到嵌入语句的结尾。该作用域包括 for 条件和 for 迭代器。

for 条件（如果存在）必须是布尔表达式（§7.20）。

for 迭代器（如果存在）由以逗号分隔的语句表达式列表（§8.6）组成。

for 语句按如下方式执行：

- 如果存在 for 初始值设定项，则按书写顺序执行变量初始值设定项或语句表达式。此步骤仅执行一次。
- 如果存在 for 条件，则计算该条件。
- 如果不存在 for 条件，或者计算结果为 true，则控制转移到嵌入语句。当控制到达嵌入语句的结束点（可能来自执行 continue 语句）时，按顺序计算 for 迭代器的表达式（如果有），然后执行下一次迭代，并从上述步骤中对 for 条件的计算开始。
- 如果存在 for 条件且计算结果为 false，则控制转移到 for 语句的结束点。

在 for 语句的嵌入语句中，可以使用 break 语句（§8.9.1）将控制转移到 for 语句的结束点（从而结束嵌入语句的迭代），也可以使用 continue 语句（§8.9.2）将控制转移到嵌入语句的结束点（从而执行 for 迭代器，并从 for 条件开始执行 for 语句的下一次迭代）。

如果下列条件之一为真，则 for 语句的嵌入语句可到达：

- for 语句可到达，并且不存在 for 条件。
- for 语句可到达，并且存在 for 条件，且该条件不具有常量值 false。

如果下列条件中至少有一项为真，则 for 语句的结束点可到达：

- for 语句包含一个可到达的 break 语句，该语句退出 for 语句。
- for 语句可到达，并且存在 for 条件，且该条件不具有常量值 true。

### 8.8.4 foreach 语句

foreach 语句枚举集合的元素，并为集合的每个元素执行嵌入语句。

```
foreach-statement:
    foreach ( local-variable-type identifier in expression ) embedded-statement
```

foreach 语句的类型和标识符声明该语句的迭代变量。如果给定 var 标识符作为局部变量类型，并且作用域中不存在名为 var 的类型，则称该迭代变量为隐式类型迭代变量，其类型按如下指定取为 foreach 语句的元素类型。该迭代变量对应于一个只读局部变量，其作用域覆盖嵌入语句。在执行 foreach 语句期间，迭代变量表示当前正在执行迭代的集合元素。如果嵌入语句试图修改迭代变量（通过赋值或 ++ 和 -- 运算符）或将迭代变量作为 ref 或 out 参数传递，则会发生编译时错误。

foreach 语句的编译时处理首先确定表达式的集合类型、枚举器类型和元素类型。该确定过程如下：

- 如果表达式的类型 X 是数组类型，则存在从 X 到 System.Collections.IEnumerable 接口的隐式引用转换（因为 System.Array 实现此接口）。集合类型为 System.Collections.IEnumerable 接口，枚举器类型为 System.Collections.IEnumerator 接口，元素类型为数组类型 X 的元素类型。
- 如果表达式的类型 X 是 dynamic，则存在从表达式到 System.Collections.IEnumerable 接口的隐式转换（§6.1.8）。集合类型为 System.Collections.IEnumerable 接口，枚举器类型为 System.Collections.IEnumerator 接口。如果给定 var 标识符作为局部变量类型，则元素类型为 dynamic；否则为 object。
- 否则，确定类型 X 是否具有适当的 GetEnumerator 方法：
  - 在类型 X 上使用标识符 GetEnumerator 且不带类型实参执行成员查找。如果成员查找未产生匹配、产生二义性，或产生的匹配不是方法组，则按下文所述检查可枚举接口。建议在成员查找产生的结果除方法组或无匹配之外的任何内容时发出警告。
  - 使用得到的方法组和空实参列表执行重载决策。如果重载决策未产生适用方法、产生二义性，或产生单个最佳方法但该方法为静态方法或不是公共方法，则按下文所述检查可枚举接口。建议在重载决策产生的结果除明确的公共实例方法或无适用方法之外的任何内容时发出警告。
  - 如果 GetEnumerator 方法的返回类型 E 不是类、结构或接口类型，则产生错误，并且不执行后续步骤。
  - 在 E 上使用标识符 Current 且不带类型实参执行成员查找。如果成员查找未产生匹配、结果为错误，或结果除允许读取的公共实例属性之外的任何内容，则产生错误，并且不执行后续步骤。



- 如果 E 是一个不可为空的值类型，则 finally 子句展开为语义等价于：

```csharp
finally {
    ((System.IDisposable)e).Dispose();
}
```

- 否则 finally 子句展开为语义等价于：

```csharp
finally {
    if (e != null) ((System.IDisposable)e).Dispose();
}
```

除非 E 是值类型，或实例化为值类型的类型参数，则 e 转换为 System.IDisposable 不会引起装箱。

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

本地变量 d 对任何用户代码不可见或不可访问。特别是，它不会与作用域包含 finally 块的任何其他变量冲突。

foreach 遍历数组元素的顺序如下：对于单维数组，元素按递增索引顺序遍历，从索引 0 开始，到索引 Length - 1 结束。对于多维数组，元素遍历的方式是先增加最右维的索引，然后是下一个左维，依此类推向左。

以下示例按元素顺序打印出二维数组中的每个值：

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
    }
}
```

输出如下：

```
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

在示例中

```csharp
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
```

n 的类型被推断为 int，即 numbers 的元素类型。

## 8.9 跳转语句

跳转语句无条件地转移控制。

- jump-statement:
  - break-statement
  - continue-statement
  - goto-statement
  - return-statement
  - throw-statement

该跳转语句转移控制到的位置称为跳转语句的 *target*。

当跳转语句出现在一个块内，且该跳转语句的目标位于该块之外时，称该跳转语句 *exit* 该块。虽然跳转语句可以从块中转移控制，但它永远不能将控制转移到块中。

跳转语句的执行因存在 intervening *try* 语句而变得复杂。在没有此类 *try* 语句的情况下，跳转语句无条件地将控制从跳转语句转移到其目标。在存在此类 intervening *try* 语句的情况下，执行更为复杂。如果跳转语句退出一个或多个带有相关联 *finally* 块的 *try* 块，则控制最初转移到最内层 *try* 语句的 *finally* 块。当且仅当控制到达 *finally* 块的终点时，控制将转移到下一个封闭 *try* 语句的 *finally* 块。此过程重复进行，直到所有 intervening *try* 语句的 *finally* 块都已执行。

在示例中

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

与两个 *try* 语句相关联的 *finally* 块在控制转移到跳转语句的目标之前执行。

输出如下：

```
Before break
Innermost finally block
Outermost finally block
After break
```

### 8.9.1 break 语句

break 语句退出最近的封闭 *switch*、*while*、*do*、*for* 或 *foreach* 语句。

- break-statement:
  - break ;

break 语句的目标是最近的封闭 switch、while、do、for 或 foreach 语句的终点。如果 break 语句未被 switch、while、do、for 或 foreach 语句包围，则会发生编译时错误。

当多个 switch、while、do、for 或 foreach 语句相互嵌套时，break 语句仅适用于最内层的语句。要跨越多个嵌套层级转移控制，必须使用 goto 语句 (§8.9.3)。

break 语句不能退出 finally 块 (§8.10)。当 break 语句出现在 finally 块内时，break 语句的目标必须在同一 finally 块内；否则会发生编译时错误。

break 语句的执行如下：

- 如果 break 语句退出一个或多个带有相关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制将转移到下一个封闭 try 语句的 finally 块。此过程重复进行，直到所有 intervening try 语句的 finally 块都已执行。
- 控制转移到 break 语句的目标。

由于 break 语句无条件地将控制转移到其他位置，因此 break 语句的终点永远不可达。

### 8.9.2 continue 语句

continue 语句开始最近的封闭 while、do、for 或 foreach 语句的新迭代。

```
continue-statement:
    continue ;
```

continue 语句的目标是最近的封闭 while、do、for 或 foreach 语句的嵌入语句的终点。如果 continue 语句未被 while、do、for 或 foreach 语句包围，则会发生编译时错误。

当多个 while、do、for 或 foreach 语句相互嵌套时，continue 语句仅适用于最内层的语句。要跨越多个嵌套层级转移控制，必须使用 goto 语句 (§8.9.3)。

continue 语句不能退出 finally 块 (§8.10)。当 continue 语句出现在 finally 块内时，continue 语句的目标必须在同一 finally 块内；否则会发生编译时错误。

continue 语句的执行如下：

- 如果 continue 语句退出一个或多个带有相关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制将转移到下一个封闭 try 语句的 finally 块。此过程重复进行，直到所有 intervening try 语句的 finally 块都已执行。
- 控制转移到 continue 语句的目标。

由于 continue 语句无条件地将控制转移到其他位置，因此 continue 语句的终点永远不可达。

### 8.9.3 goto 语句

goto 语句将控制转移到由标签标记的语句。

```
goto-statement:
    goto identifier ;
    goto case constant-expression ;
    goto default ;
```

goto identifier 语句的目标是具有给定标签的带标签语句。如果在当前函数成员中不存在具有给定名称的标签，或者 goto 语句不在标签的作用域内，则会发生编译时错误。此规则允许使用 goto 语句将控制转移出嵌套作用域，但不允许转移进入嵌套作用域。在示例中

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

使用 goto 语句将控制转移出嵌套作用域。

goto case 语句的目标是立即封闭的 switch 语句 (§8.7.2) 中的语句列表，其中包含具有给定常量值的 case 标签。如果 goto case 语句未被 switch 语句包围，如果 constant-expression 不能隐式转换为最近封闭 switch 语句的控制类型 (§6.1)，或者最近封闭的 switch 语句不包含具有给定常量值的 case 标签，则会发生编译时错误。

goto default 语句的目标是立即封闭的 switch 语句 (§8.7.2) 中的语句列表，其中包含 default 标签。如果 goto default 语句未被 switch 语句包围，或者最近封闭的 switch 语句不包含 default 标签，则会发生编译时错误。

goto 语句不能退出 finally 块 (§8.10)。当 goto 语句出现在 finally 块内时，goto 语句的目标必须在同一 finally 块内，否则会发生编译时错误。

goto 语句的执行如下：

- 如果 goto 语句退出一个或多个带有相关联 finally 块的 try 块，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制将转移到下一个封闭 try 语句的 finally 块。此过程重复进行，直到所有 intervening try 语句的 finally 块都已执行。
- 控制转移到 goto 语句的目标。



因为 `goto` 语句无条件地将控制转移到别处，所以 `goto` 语句的终点永远无法到达。

### 8.9.4 return 语句

`return` 语句将控制返回给包含该 `return` 语句的函数成员的调用者。

```
return-statement:
    return expression_opt ;
```

没有表达式的 `return` 语句只能用在不计算值的函数成员中，即返回类型为 `void` 的方法、属性或索引器的 `set` 访问器、事件的 `add` 和 `remove` 访问器、实例构造函数、静态构造函数或析构函数。

带有表达式的 `return` 语句只能用在计算值的函数成员中，即返回类型为非 `void` 的方法、属性或索引器的 `get` 访问器，或用户定义的运算符。必须存在从表达式类型到包含该函数成员的返回类型的隐式转换 (§6.1)。

在 `finally` 块 (§8.10) 中出现 `return` 语句是编译时错误。

`return` 语句的执行如下：

- 如果 `return` 语句指定了表达式，则会计算该表达式，并通过隐式转换将其结果值转换为包含该函数成员的返回类型。转换的结果成为返回给调用者的值。
- 如果 `return` 语句被一个或多个带有关联 `finally` 块的 `try` 块所包围，则控制最初转移到最内层 `try` 语句的 `finally` 块。当且仅当控制到达 `finally` 块的终点时，控制会转移到下一个外层 `try` 语句的 `finally` 块。此过程重复进行，直到所有外层 `try` 语句的 `finally` 块都已执行完毕。
- 控制返回给包含该函数成员的调用者。

因为 `return` 语句无条件地将控制转移到别处，所以 `return` 语句的终点永远无法到达。

### 8.9.5 throw 语句

`throw` 语句抛出异常。

```
throw-statement:
    throw expression_opt ;
```

带有表达式的 `throw` 语句抛出计算表达式得到的值。表达式必须表示类类型 `System.Exception` 的值、派生自 `System.Exception` 的类类型的值，或其有效基类为 `System.Exception`（或其子类）的类型参数类型的值。如果表达式的计算结果为 `null`，则改为抛出 `System.NullReferenceException`。

没有表达式的 `throw` 语句只能在 `catch` 块中使用，在这种情况下该语句会重新抛出当前由该 `catch` 块处理的异常。

因为 `throw` 语句无条件地将控制转移到别处，所以 `throw` 语句的终点永远无法到达。

当抛出异常时，控制会转移到能够处理该异常的外层 `try` 语句中的第一个 `catch` 子句。从抛出异常的点到将控制转移到合适的异常处理程序的点所发生的过程称为 *异常传播*。异常的传播包括重复评估以下步骤，直到找到匹配该异常的 *catch* 子句。在此描述中，*throw point* 最初是抛出异常的位置。

- 在当前函数成员中，检查每个包围 throw point 的 *try* 语句。对于每个语句 S，从最内层的 *try* 语句开始，到最外层的 *try* 语句结束，评估以下步骤：
  - 如果 S 的 *try* 块包围了 throw point 且 S 具有一个或多个 *catch* 子句，则按出现顺序检查 *catch* 子句以定位适合处理异常的处理程序。第一个指定异常类型或异常类型的基类型的 *catch* 子句被视为匹配。一般 *catch* 子句 (§8.10) 被视为与任何异常类型匹配。如果找到匹配的 *catch* 子句，则通过将控制转移到该 *catch* 子句的块来完成异常传播。
  - 否则，如果 S 的 *try* 块或 *catch* 块包围了 throw point 且 S 具有 *finally* 块，则控制转移到 *finally* 块。如果 *finally* 块抛出另一个异常，则当前异常的处理终止。否则，当控制到达 *finally* 块的终点时，当前异常的处理继续。
- 如果在当前函数成员调用中未找到异常处理程序，则函数成员调用终止。然后对函数成员的调用者重复上述步骤，throw point 对应于调用该函数成员的语句。
- 如果异常处理终止了当前线程中的所有函数成员调用，表示该线程没有处理该异常的处理程序，则线程本身被终止。此类终止的影响是实现定义的。

## 8.10 try 语句

*try* 语句提供了一种在块执行期间捕获异常的机制。此外，*try* 语句提供了指定在控制离开 *try* 语句时始终执行的代码块的能力。

```
try-statement:
    try block catch-clauses
    try block finally-clause
    try block catch-clauses finally-clause

catch-clauses:
    specific-catch-clauses general-catch-clauseopt
    specific-catch-clausesopt general-catch-clause

specific-catch-clauses:
    specific-catch-clause
    specific-catch-clauses specific-catch-clause

specific-catch-clause:
    catch ( class-type identifieropt ) block

general-catch-clause:
    catch block

finally-clause:
    finally block
```

*try* 语句有三种可能的形式：

C# 语言规范

- 后跟一个或多个 catch 块的 try 块。
- 后跟 finally 块的 try 块。
- 后跟一个或多个 catch 块再跟 finally 块的 try 块。

当 catch 子句指定 class-type 时，该类型必须是 System.Exception、派生自 System.Exception 的类型，或其有效基类为 System.Exception（或其子类）的类型参数类型。

当 catch 子句同时指定 class-type 和标识符时，会声明一个具有给定名称和类型的异常变量。异常变量对应于作用域扩展到 catch 块上的局部变量。在 catch 块执行期间，异常变量表示当前正在处理的异常。对于确定性赋值检查而言，异常变量在其整个作用域内被视为已明确赋值。

除非 catch 子句包含异常变量名，否则在 catch 块中无法访问异常对象。

不指定异常类型也不指定异常变量名的 catch 子句称为一般 catch 子句。try 语句只能有一个一般 catch 子句，如果存在，则必须是最后一个 catch 子句。

某些编程语言可能支持不能表示为派生自 System.Exception 的对象的异常，尽管此类异常永远不会由 C# 代码生成。一般 catch 子句可用于捕获此类异常。因此，一般 catch 子句在语义上不同于指定类型 System.Exception 的子句，因为前者还可能捕获来自其他语言的异常。

为了定位异常的处理程序，catch 子句按词法顺序检查。如果 catch 子句指定的类型与同一 try 的 earlier catch 子句中指定的类型相同或派生自该类型，则会发生编译时错误。如果没有此限制，就有可能编写不可达的 catch 子句。

在 catch 块内，可以使用没有表达式的 throw 语句 (§8.9.5) 重新抛出由该 catch 块捕获的异常。对异常变量的赋值不会改变被重新抛出的异常。

示例中

```
using System;
class Test
{
    static void F() {
        try { G(); }
        catch (Exception e) {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw; // re-throw
        }
    }
    static void G() {
        throw new Exception("G");
    }
}
```



```
static void Main() {
    try {
        F();
    }
    catch (Exception e) {
        Console.WriteLine("Exception in Main: " + e.Message);
    }
}
```

方法 F 捕获一个异常，将一些诊断信息写入控制台，修改异常变量，并重新抛出异常。被重新抛出的异常是原始异常，因此产生的输出为：

```
Exception in F: G
Exception in Main: G
```

如果第一个 catch 块抛出 e 而不是重新抛出当前异常，则产生的输出如下：

```
Exception in F: G
Exception in Main: F
```

如果 break、continue 或 goto 语句将控制权转移出 finally 块，则为编译时错误。当 break、continue 或 goto 语句出现在 finally 块中时，该语句的目标必须在同一个 finally 块内，否则会发生编译时错误。

在 finally 块中出现 return 语句是编译时错误。

try 语句的执行方式如下：

- 控制权转移到 try 块。
- 当且仅当控制权到达 try 块的终点时：
  - 如果 try 语句有 finally 块，则执行 finally 块。
  - 控制权转移到 try 语句的终点。
- 如果在 try 块执行期间有异常传播到 try 语句：
  - 按出现顺序检查 catch 子句（如果有），以定位适合处理异常的处理程序。第一个指定异常类型或异常类型的基类型的 catch 子句被视为匹配。一般 catch 子句被视为与任何异常类型匹配。如果找到匹配的 catch 子句：
    - 如果匹配的 catch 子句声明了异常变量，则将异常对象赋给异常变量。
    - 控制权转移到匹配的 catch 块。
    - 当且仅当控制权到达 catch 块的终点时：
      - 如果 try 语句有 finally 块，则执行 finally 块。
      - 控制权转移到 try 语句的终点。
    - 如果在 catch 块执行期间有异常传播到 try 语句：
      - 如果 try 语句有 finally 块，则执行 finally 块。
      - 该异常传播到下一个封闭的 try 语句。
  - 如果 try 语句没有 catch 子句或没有 catch 子句匹配该异常：
- 如果 try 语句有 finally 块，则执行 finally 块。
- 该异常传播到下一个封闭的 try 语句。

当控制权离开 try 语句时，finally 块的语句总是会被执行。这无论控制转移是由于正常执行、执行 break、continue、goto 或 return 语句的结果，还是由于将异常从 try 语句传播出来的结果，都为真。

如果在 finally 块执行期间抛出异常，并且未在同一 finally 块内捕获，则该异常传播到下一个封闭的 try 语句。如果另一个异常正在传播过程中，则该异常会丢失。异常传播的过程在 throw 语句 (§8.9.5) 的描述中进一步讨论。

如果 try 语句可达，则 try 语句的 try 块可达。

如果 try 语句可达，则 try 语句的 catch 块可达。

如果 try 语句可达，则 try 语句的 finally 块可达。

如果以下两点均为真，则 try 语句的终点可达：

- try 块的终点可达，或至少一个 catch 块的终点可达。
- 如果存在 finally 块，则 finally 块的终点可达。

## 8.11 checked 和 unchecked 语句

checked 和 unchecked 语句用于控制整数类型算术运算和转换的溢出检查上下文。

```
checked-statement:
    checked block

unchecked-statement:
    unchecked block
```

checked 语句导致块中的所有表达式都在已检查上下文中求值，而 unchecked 语句导致块中的所有表达式都在未检查上下文中求值。

checked 和 unchecked 语句与 checked 和 unchecked 运算符 (§7.6.12) 精确等价，只是它们操作的是块而不是表达式。

## 8.12 lock 语句

lock 语句为给定对象获取互斥锁，执行一个语句，然后释放该锁。

```
lock-statement:
    lock ( expression ) embedded-statement
```

lock 语句的表达式必须表示已知为引用类型的类型的值。lock 语句的表达式永远不会执行隐式装箱转换 (§6.1.7)，因此表达式表示值类型的值是编译时错误。

形式为的 lock 语句

```
lock ( x ) ...
```

其中 x 是引用类型的表达式，精确等价于

如果资源的类型为 dynamic，则在获取期间通过隐式动态转换 (§6.1.8) 动态转换为 IDisposable，以确保转换在使用和释放之前成功。

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

在任一展开中，资源变量在嵌入语句中为只读，且 d 变量在嵌入语句中不可访问且对嵌入语句不可见。

实现可以以不同方式实现给定的 using 语句，例如出于性能原因，只要行为与上述展开一致即可。

形式为的 using 语句

```
using (expression) statement
```

具有相同的三种可能展开，但在这种情况下 ResourceType 隐式为表达式的编译时类型，且资源变量在嵌入语句中不可访问且对嵌入语句不可见。

当资源获取采用局部变量声明的形式时，可以获取给定类型的多个资源。形式为的 using 语句

```
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) statement
```

精确等价于一组嵌套的 using 语句：

```
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```

下面的示例创建一个名为 `log.txt` 的文件并向其中写入两行文本。然后示例打开同一个文件进行读取并将包含的行文本复制到控制台。

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

由于 `TextWriter` 和 `TextReader` 类实现了 `IDisposable` 接口，示例可以使用 `using` 语句确保在写入或读取操作后底层文件被正确关闭。

## 8.14 yield 语句

`yield` 语句用于迭代器块 (§8.2) 中，将值传递给迭代器的枚举器对象 (§10.14.4) 或可枚举对象 (§10.14.5)，或用于发出迭代结束的信号。

```
yield-statement:
    yield return expression ;
    yield break ;
```

`yield` 不是保留字；只有在 `return` 或 `break` 关键字之前立即使用时才有特殊含义。在其他上下文中，`yield` 可用作标识符。

`yield` 语句可以出现的位置有若干限制，如下所述。

- `yield` 语句（任一形式）出现在 *方法体*、*运算符体* 或 *访问器体* 之外是编译时错误
- `yield` 语句（任一形式）出现在匿名函数内部是编译时错误。
- `yield` 语句（任一形式）出现在 *try* 语句的 *finally* 子句中是编译时错误。
- `yield return` 语句出现在包含任何 *catch* 子句的 *try* 语句中的任何位置是编译时错误。

以下示例展示了 `yield` 语句的一些有效和无效用法。

```csharp
delegate IEnumerable<int> D();
```

```IEnumerator<int> GetEnumerator() {
    try {
        yield return 1;     // Ok
        yield break;        // Ok
    }
    finally {
        yield return 2;     // Error, yield in finally
        yield break;        // Error, yield in finally
    }

    try {
        yield return 3;     // Error, yield return in try...catch
        yield break;        // Ok
    }
    catch {
        yield return 4;     // Error, yield return in try...catch
        yield break;        // Ok
    }

    D d = delegate {
        yield return 5;     // Error, yield in an anonymous function
    };
}

int MyMethod() {
    yield return 1;         // Error, wrong return type for an iterator block
}
```

隐式转换 (§6.1) 必须存在于 yield return 语句中表达式的类型与迭代器的 yield 类型 (§10.14.3) 之间。

## yield return 语句的执行方式如下：

- 语句中给出的表达式会被求值，隐式转换为 yield 类型，并赋给枚举器对象的 Current 属性。
- 迭代器块的执行被挂起。如果 yield return 语句位于一个或多个 try 块内，则相关的 finally 块此时不会执行。
- 枚举器对象的 MoveNext 方法向其调用者返回 true，表示枚举器对象已成功推进到下一项。

枚举器对象的 MoveNext 方法的下一次调用将从上次挂起的位置恢复迭代器块的执行。

## yield break 语句的执行方式如下：

- 如果 yield break 语句被一个或多个带有相关 finally 块的 try 块包围，则控制最初转移到最内层 try 语句的 finally 块。当且仅当控制到达 finally 块的终点时，控制会转移到下一个外层 try 语句的 finally 块。此过程重复进行，直到所有外层 try 语句的 finally 块都已执行。
- 控制返回到迭代器块的调用者。这可以是枚举器对象的 MoveNext 方法或 Dispose 方法。

由于 yield break 语句无条件地将控制转移到别处，因此 yield break 语句的终点永远不可达。

## 9. 命名空间

C# 程序使用命名空间进行组织。命名空间既用作程序的“内部”组织系统，也用作“外部”组织系统——一种呈现程序中暴露给其他程序的元素的方式。

使用指令 (§9.4) 用于促进命名空间的使用。

### 9.1 编译单元

compilation-unit 定义了源文件整体结构。编译单元由零个或多个 using-directives 组成，其后跟零个或多个 global-attributes，再后跟零个或多个 namespace-member-declarations。

```
compilation-unit:
    extern-alias-directivesopt  using-directivesopt  global-attributesopt
    namespace-member-declarationsopt
```

C# 程序由一个或多个编译单元组成，每个编译单元包含在单独的源文件中。当 C# 程序被编译时，所有编译单元会一起处理。因此，编译单元可以相互依赖，甚至可能形成循环依赖。

编译单元的 using-directives 影响该编译单元的 global-attributes 和 namespace-member-declarations，但对其他编译单元没有影响。

编译单元的 global-attributes (§17) 允许为目标程序集和模块指定属性。程序集和模块充当类型的物理容器。程序集可能由多个物理上分离的模块组成。

程序中每个编译单元的 namespace-member-declarations 都向一个名为全局命名空间的单一声明空间贡献成员。例如：

```
File A.cs:
    class A {}

File B.cs:
    class B {}
```

这两个编译单元贡献给单一的全局命名空间，在此例中声明了两个类，其完全限定名为 A 和 B。由于这两个编译单元贡献给同一个声明空间，如果每个编译单元都包含同名成员的声明，则会出错。

### 9.2 命名空间声明

namespace-declaration 由关键字 namespace 组成，其后跟命名空间名称和主体，可选地后跟分号。

```
namespace-declaration:
    namespace  qualified-identifier  namespace-body  ;opt

qualified-identifier:
    identifier
    qualified-identifier . identifier
```

```
namespace-body:
    { extern-alias-directives_opt using-directives_opt namespace-member-declarations_opt }
```

namespace-declaration 可以作为编译单元中的顶层声明出现，也可以作为另一个 namespace-declaration 内的成员声明出现。当 namespace-declaration 作为编译单元中的顶层声明出现时，该命名空间成为全局命名空间的成员。当 namespace-declaration 出现在另一个 namespace-declaration 内时，内部命名空间成为外部命名空间的成员。在任何情况下，命名空间的名称在其包含的命名空间内必须是唯一的。

命名空间隐式为 public，命名空间的声明不能包含任何访问修饰符。

在 namespace-body 内，可选的 using-directives 导入其他命名空间和类型的名称，使其可以通过非限定名称直接引用，而不是通过限定名称。可选的 namespace-member-declarations 向命名空间的声明空间贡献成员。请注意，所有 using-directives 必须出现在任何成员声明之前。

namespace-declaration 的 qualified-identifier 可以是单个标识符，也可以是由“.” 标记分隔的标识符序列。后一种形式允许程序在不词法嵌套多个命名空间声明的情况下定义嵌套命名空间。例如，

```
namespace N1.N2
{
    class A {}
    class B {}
}
```

在语义上等价于

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

命名空间是开放式的，并且具有相同完全限定名的两个命名空间声明贡献给同一个声明空间 (§3.3)。在示例中

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

上述两个命名空间声明贡献给同一个声明空间，在此例中声明了两个类，其完全限定名为 N1.N2.A 和 N1.N2.B。由于这两个声明贡献给同一个声明空间，如果每个声明都包含同名成员的声明，则会出错。

### 9.3 外部别名

extern-alias-directive 引入一个标识符，该标识符用作命名空间的别名。被别名化的命名空间的规范位于程序源代码之外，并且也适用于被别名化命名空间的嵌套命名空间。

```
extern-alias-directives:
    extern-alias-directive
    extern-alias-directives extern-alias-directive

extern-alias-directive:
    extern alias identifier ;
```

extern-alias-directive 的作用域扩展到其直接包含的编译单元或命名空间主体中的 using-directives、global-attributes 和 namespace-member-declarations。

在包含 extern-alias-directive 的编译单元或命名空间主体内，由 extern-alias-directive 引入的标识符可用于引用被别名化的命名空间。标识符为单词 global 是编译时错误。

extern-alias-directive 使别名在特定编译单元或命名空间主体内可用，但它不会向底层声明空间贡献任何新成员。换句话说，extern-alias-directive 不是传递的，而是仅影响它出现的编译单元或命名空间主体。

以下程序声明并使用两个 extern 别名 X 和 Y，它们各自代表一个不同的命名空间层次结构的根：

```
extern alias X;
extern alias Y;
class Test
{
    X::N::A a;
    X::N::B b1;
    Y::N::B b2;
    Y::N::C c;
}
```

该程序声明了 extern 别名 X 和 Y 的存在，但别名的实际定义位于程序之外。同名 N::B 类现在可以作为 X::N::B 和 Y::N::B 引用，或使用命名空间别名限定符引用 X::N::B 和 Y::N::B。如果程序声明了一个没有外部定义的 extern 别名，则会发生错误。

### 9.4 using 指令

using 指令促进了在其他命名空间中定义的命名空间和类型的使用。using 指令影响 namespace-or-type-names (§3.8) 和 simple-names (§7.6.2) 的名称解析过程，但与声明不同，using 指令不会向其使用的编译单元或命名空间的底层声明空间贡献新成员。

```
using-directives:
    using-directive
    using-directives using-directive

using-directive:
    using-alias-directive
    using-namespace-directive
```

using-alias-directive (§9.4.1) 为命名空间或类型引入别名。

using-namespace-directive (§9.4.2) 导入命名空间的类型成员。

using-directive 的作用域扩展到其直接包含的编译单元或命名空间主体中的 namespace-member-declarations。using-directive 的作用域 specifically 不包括其同级 using-directives。因此，同级 using-directives 互不影响，它们书写的顺序无关紧要。



## 9.4.1 使用别名指令

using 别名指令引入一个标识符，该标识符用作紧邻的编译单元或命名空间体内命名空间或类型的别名。

```
using-alias-directive:
    using identifier = namespace-or-type-name ;
```

在包含 using 别名指令的编译单元或命名空间体的成员声明中，using 别名指令引入的标识符可用于引用给定的命名空间或类型。例如：

```
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

在上面的示例中，在 N3 命名空间的成员声明中，A 是 N1.N2.A 的别名，因此类 N3.B 派生自类 N1.N2.A。通过为 N1.N2 创建别名 R，然后引用 R.A，也可以获得相同的效果：

```
namespace N3
{
    using R = N1.N2;
    class B: R.A {}
}
```

using 别名指令的标识符在直接包含该 using 别名指令的编译单元或命名空间的声明空间中必须唯一。例如：

```
namespace N3
{
    class A {}
}
namespace N3
{
    using A = N1.N2.A;    // Error, A already exists
}
```

在上面的示例中，N3 已经包含成员 A，因此 using 别名指令使用该标识符会导致编译时错误。同样，同一编译单元或命名空间体中的两个或多个 using 别名指令用同一名称声明别名也会导致编译时错误。

using 别名指令使别名在特定编译单元或命名空间体内可用，但它不会向基础声明空间贡献任何新成员。换句话说，using 别名指令不具有传递性，而只影响其所在的编译单元或命名空间体。在示例

```
namespace N3
{
    using R = N1.N2;
}
namespace N3
{
    class B: R.A {}    // Error, R unknown
}
```

```
namespace N1.N2
{
    class A {}
}
namespace N3
{
    using N1;
    class B: N2.A {}      // Error, N2 unknown
}
```

中，using 命名空间指令导入 N1 中包含的类型，但不导入 N1 中嵌套的命名空间。因此，在 B 的声明中对 N2.A 的引用会导致编译时错误，因为作用域中没有名为 N2 的成员。

与 using 别名指令不同，using 命名空间指令可以导入其标识符已在包含它的编译单元或命名空间体中定义的类型。实际上，由 using 命名空间指令导入的名称会被包含它的编译单元或命名空间体中同名的成员隐藏。例如：

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

这里，在 N3 命名空间的成员声明中，A 指的是 N3.A，而不是 N1.N2.A。

当同一编译单元或命名空间体中由 using 命名空间指令导入的多个命名空间包含同名类型时，对该名称的引用被视为不明确。在示例

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
    class B: A {}          // Error, A is ambiguous
}
```

中，N1 和 N2 都包含成员 A，并且由于 N3 同时导入两者，在 N3 中引用 A 会导致编译时错误。在这种情况下，可以通过限定对 A 的引用，或通过引入选择特定 A 的 using 别名指令来解决冲突。例如：

```
namespace N3
{
    using N1;
```
- 结构中声明的类型可以具有 public、internal 或 private 访问权限。默认访问权限为 private。

## 9.7 命名空间别名限定符

命名空间别名限定符 :: 可以保证类型名称查找不受新类型和成员引入的影响。命名空间别名限定符始终出现在两个标识符之间，这两个标识符称为左标识符和右标识符。与常规的 . 限定符不同，:: 限定符的左标识符仅作为 extern 或 using 别名进行查找。

限定别名成员的定义如下：

```
qualified-alias-member:
    identifier :: identifier type-argument-list_opt
```

限定别名成员可以用作命名空间或类型名称（§3.8），也可以用作成员访问（§7.6.4）中的左操作数。

限定别名成员具有以下两种形式之一：

- N :: I<A1, ..., Ak>，其中 N 和 I 表示标识符，<A1, ..., Ak> 是类型参数列表。（K 始终至少为 1。）
- N :: I，其中 N 和 I 表示标识符。（在这种情况下，K 视为零。）

使用此表示法，限定别名成员的含义按如下方式确定：

- 如果 N 是标识符 global，则在全局命名空间中搜索 I：
  - 如果全局命名空间包含名为 I 的命名空间且 K 为零，则限定别名成员引用该命名空间。
  - 否则，如果全局命名空间包含名为 I 的非泛型类型且 K 为零，则限定别名成员引用该类型。
  - 否则，如果全局命名空间包含名为 I 且具有 K 个类型参数的类型，则限定别名成员引用用给定类型参数构造的该类型。
  - 否则，限定别名成员未定义，并发生编译时错误。
- 否则，从直接包含该限定别名成员的命名空间声明（如果有）开始，继续处理每个外层命名空间声明（如果有），直到包含该限定别名成员的编译单元，按以下步骤求值，直到定位到实体：
  - 如果命名空间声明或编译单元包含将 N 与类型关联的 using 别名指令，则限定别名成员未定义，并发生编译时错误。
  - 否则，如果命名空间声明或编译单元包含将 N 与命名空间关联的 extern 别名指令或 using 别名指令，则：
    - 如果与 N 关联的命名空间包含名为 I 的命名空间且 K 为零，则限定别名成员引用该命名空间。
    - 否则，如果与 N 关联的命名空间包含名为 I 的非泛型类型且 K 为零，则限定别名成员引用该类型。
    - 否则，如果与 N 关联的命名空间包含名为 I 且具有 K 个类型参数的类型，则限定别名成员引用用给定类型参数构造的该类型。
    - 否则，限定别名成员未定义，并发生编译时错误。
- 否则，限定别名成员未定义，并发生编译时错误。

请注意，将命名空间别名限定符与引用类型的别名一起使用会导致编译时错误。
另请注意，如果标识符 N 是 global，则即使在存在将 global 与类型或命名空间关联的 using 别名的情况下，也会在全局命名空间中执行查找。

### 9.7.1 别名的唯一性

每个编译单元和命名空间体都有单独的声明空间用于 extern 别名和 using 别名。
因此，虽然 extern 别名或 using 别名的名称在直接包含它的编译单元或命名空间体中声明的 extern 别名和 using 别名集合内必须唯一，但只要别名仅与 :: 限定符一起使用，就允许别名与类型或命名空间同名。

在示例

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

中，名称 A 在第二个命名空间体中有两种可能的含义，因为类 A 和 using 别名 A 都在作用域中。因此，在限定名 A.Stream 中使用 A 是不明确的，并会导致编译时错误。但是，将 A 与 :: 限定符一起使用不会出错，因为 A 仅作为命名空间别名进行查找。




## 10. 类

类是一种数据结构，它可以包含数据成员（常量和字段）、函数成员（方法、属性、事件、索引器、运算符、实例构造函数、析构函数和静态构造函数）以及嵌套类型。类类型支持继承，这是一种机制，通过该机制，派生类可以扩展并特化基类。

### 10.1 类声明

类声明是一种类型声明（§9.6），它声明一个新类。

```
class-declaration:
    attributes_opt class-modifiers_opt partial_opt class identifier type-parameter-list_opt
    class-base_opt type-parameter-constraints-clauses_opt class-body ;_opt
```

类声明由一个可选特性集（§17）、一个可选类修饰符集（§10.1.1）、一个可选 partial 修饰符、关键字 class 和命名该类的标识符、一个可选类型参数列表（§10.1.3）、一个可选类基规范（§10.1.4）、一个可选类型参数约束子句集（§10.1.5）、一个类体（§10.1.6）组成，其后可选跟一个分号。

类声明不能提供类型参数约束子句，除非它还提供类型参数列表。

提供类型参数列表的类声明是泛型类声明。此外，嵌套在泛型类声明或泛型结构声明内的任何类本身也是泛型类声明，因为必须提供包含类型的类型参数才能创建构造类型。

### 10.1.1 类修饰符

类声明可以可选地包含一系列类修饰符：

```
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
```

同一修饰符在类声明中多次出现是编译时错误。

new 修饰符允许用于嵌套类。它指定该类隐藏同名的继承成员，如 §10.3.4 所述。对于不是嵌套类声明的类声明，出现 new 修饰符是编译时错误。

public、protected、internal 和 private 修饰符控制类的可访问性。根据类声明发生的上下文，其中某些修饰符可能不被允许（§3.5.1）。

### 10.1.1.1 抽象类

abstract 修饰符用于指示类是不完整的，并且旨在仅用作基类。抽象类与非抽象类在以下方面不同：

- 抽象类不能直接实例化，并且对抽象类使用 new 运算符是编译时错误。虽然可以拥有编译时类型为抽象类的变量和值，但此类变量和值必然要么为 null，要么包含对从抽象类型派生的非抽象类实例的引用。
- 抽象类允许（但不要求）包含抽象成员。
- 抽象类不能是密封的。

当非抽象类从抽象类派生时，该非抽象类必须包含所有继承的抽象成员的实际实现，从而重写这些抽象成员。在示例中

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
    public override void F() { // actual implementation of F
    }
}
```

抽象类 A 引入一个抽象方法 F。类 B 引入一个附加方法 G，但由于它不提供 F 的实现，B 也必须声明为抽象。类 C 重写 F 并提供实际实现。由于 C 中没有抽象成员，C 允许（但不要求）为非抽象。

### 10.1.1.2 密封类

sealed 修饰符用于防止从类派生。如果将密封类指定为另一个类的基类，则发生编译时错误。

密封类也不能是抽象类。

sealed 修饰符主要用于防止意外的派生，但它也支持某些运行时优化。特别是，由于已知密封类永远没有任何派生类，因此可以将对密封类实例的虚函数成员调用转换为非虚调用。

### 10.1.1.3 静态类

static 修饰符用于将所声明的类标记为静态类。静态类不能实例化，不能用作类型，并且只能包含静态成员。只有静态类可以包含扩展方法声明（§10.6.9）。

静态类声明受以下限制：

- 静态类不能包含 sealed 或 abstract 修饰符。但请注意，由于静态类不能实例化也不能派生，它的行为就像既是密封的又是抽象的。
- 静态类不能包含类基规范（§10.1.4），并且不能显式指定基类或所实现接口的列表。静态类隐式继承自类型 object。
- 静态类只能包含静态成员（§10.3.7）。请注意，常量和嵌套类型被归类为静态成员。
- 静态类不能具有声明可访问性为 protected 或 protected internal 的成员。

违反上述任何限制都是编译时错误。

静态类没有实例构造函数。不能在静态类中声明实例构造函数，并且不为静态类提供默认实例构造函数（§10.11.4）。

静态类的成员不自动是静态的，成员声明必须显式包含 static 修饰符（常量和嵌套类型除外）。当类嵌套在静态外部类中时，嵌套类不是静态类，除非它显式包含 static 修饰符。

### 10.1.1.3.1 引用静态类类型

如果满足以下条件，则允许命名空间或类型名（§3.8）引用静态类：

- 该命名空间或类型名是形式为 T.I 的命名空间或类型名中的 T，或者
- 该命名空间或类型名是形式为 typeof(T) 的 typeof 表达式（§7.5.11）中的 T。

如果满足以下条件，则允许初等表达式（§7.5）引用静态类：

- 该初等表达式是形式为 E.I 的成员访问（§7.5.4）中的 E。

在任何其他上下文中，引用静态类都是编译时错误。例如，将静态类用作基类、成员的组成类型（§10.3.8）、泛型类型实参或类型参数约束是错误的。同样，静态类不能用于数组类型、指针类型、new 表达式、强制转换表达式、is 表达式、as 表达式、sizeof 表达式或默认值表达式。

### 10.1.2 partial 修饰符

partial 修饰符用于指示此类声明是部分类型声明。在封闭命名空间或类型声明内，具有相同名称的多个部分类型声明按照 §10.2 中指定的规则组合成一个类型声明。

将类的声明分散在程序文本的各个独立段中可能很有用，如果这些段是在不同上下文中生成或维护的。例如，类声明的一部分可能由机器生成，而另一部分由人工编写。两者的文本分离可防止一方的更新与另一方的更新发生冲突。

### 10.1.3 类型参数

类型参数是一个简单标识符，它表示用于创建构造类型时所提供的类型实参的占位符。类型参数是稍后将提供的类型的正式占位符。相比之下，类型实参（§4.4.1）是在创建构造类型时替换类型参数的实际类型。

```
type-parameter-list:
    < type-parameters >
type-parameters:
    attributes_opt type-parameter
    type-parameters , attributes_opt type-parameter
type-parameter:
    identifier
```



每个类声明中的类型参数都在该类的声明空间（§3.3）中定义一个名称。因此，它不能与另一个类型参数或在该类中声明的成员具有相同的名称。类型参数不能与类型本身具有相同的名称。

## 10.1.4 类基规范

类声明可以包含类基规范，该规范定义了类的直接基类以及类直接实现的接口（§13）。

```
class-base:
    : class-type
    : interface-type-list
    : class-type , interface-type-list

interface-type-list:
    interface-type
    interface-type-list , interface-type
```

类声明中指定的基类可以是构造的类类型（§4.4）。基类本身不能是类型参数，尽管它可以涉及作用域中的类型参数。

```
class Extend<V>: V {}    // Error, type parameter used as base class
```

### 10.1.4.1 基类

当 class-base 中包含 class-type 时，它指定了正在声明的类的直接基类。如果类声明没有 class-base，或者 class-base 仅列出接口类型，则假定直接基类为 object。类从其直接基类继承成员，如 §10.3.3 中所述。

示例中

```
class A {}
class B: A {}
```

class A 被称为 B 的直接基类，而 B 被称为派生自 A。由于 A 没有显式指定直接基类，其直接基类隐式为 object。

对于构造的类类型，如果在泛型类声明中指定了基类，则构造类型的基类是通过为基类声明中的每个类型参数替换构造类型的相应类型参数来获得的。给定泛型类声明

```
class B<U,V> {...}
class G<T>: B<string,T[]> {...}
```

构造类型 G<int> 的基类将为 B<string,int[]>。

类类型的直接基类必须至少与类类型本身一样可访问（§5.5.2）。例如，公共类派生自私有或内部类是编译时错误。

类类型的直接基类不得是以下任何类型：System.Array、System.Delegate、System.MulticastDelegate、System.Enum 或 System.ValueType。此外，泛型类声明不能将 System.Attribute 用作直接或间接基类。

在确定类 B 的直接基类规范 A 的含义时，B 的直接基类暂时假定为 object。直观上，这确保了基类规范的含义不能递归地依赖于自身。示例：

```
class A<T> {
    public class B{}
}
```

```
class C : A<C.B> {}
```

这是错误的，因为在基类规范 A<C.B> 中，C 的直接基类被认为是 object，因此（根据 §3.8 的规则）C 不被认为具有成员 B。

类类型的基类是直接基类及其基类。换句话说，基类集合是直接基类关系的传递闭包。参考上面的示例，B 的基类是 A 和 object。在示例中

```
class A {...}
class B<T>: A {...}
class C<T>: B<IComparable<T>> {...}
class D<T>: C<T[]> {...}
```

D<int> 的基类是 C<int[]>、B<IComparable<int[]>>、A 和 object。

除了类 object 之外，每个类类型都有且仅有一个直接基类。object 类没有直接基类，是所有其他类的最终基类。

当类 B 派生自类 A 时，A 依赖于 B 是编译时错误。类直接依赖于直接基类（如果有）并直接依赖于其立即嵌套在其中的类（如果有）。根据此定义，类所依赖的完整类集合是直接依赖关系的自反和传递闭包。

示例

```
class A: A {}
```

这是错误的，因为该类依赖于自身。同样，示例

```
class A: B {}
class B: C {}
class C: A {}
```

是错误的，因为类循环依赖于自身。最后，示例

```
class A: B.C {}
class B: A
{
    public class C {}
}
```

导致编译时错误，因为 A 依赖于 B.C（其直接基类），B.C 依赖于 B（其立即封闭类），而 B 循环依赖于 A。

请注意，类不依赖于嵌套在其内部的类。在示例中

```
class A
{
    class B: A {}
}
```

B 依赖于 A（因为 A 既是其直接基类也是其立即封闭类），但 A 不依赖于 B（因为 B 既不是 A 的基类也不是封闭类）。因此，该示例是有效的。

不能从密封类派生。在示例中

```
sealed class A {}
class B: A {}      // Error, cannot derive from a sealed class
```

class B 是错误的，因为它试图从密封类 A 派生。

### 10.1.4.2 接口实现

类基规范可以包含接口类型列表，在这种情况下，类被认为直接实现了给定的接口类型。接口实现在 §13.4 中进一步讨论。

## 10.1.5 类型参数约束

泛型类型和方法声明可以通过包含 type-parameter-constraints-clauses 可选地指定类型参数约束。

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

每个 type-parameter-constraints-clause 由标记 where 组成，后跟类型参数的名称，后跟冒号和该类型参数的约束列表。每个类型参数最多只能有一个 where 子句，并且 where 子句可以按任何顺序列出。与属性访问器中的 get 和 set 标记类似，where 标记不是关键字。

where 子句中给出的约束列表可以包含以下任何组件，按此顺序：单个主约束、一个或多个次要约束，以及构造函数约束 new()。

主约束可以是类类型或引用类型约束 class 或值类型约束 struct。次要约束可以是 type-parameter 或 interface-type。

引用类型约束指定用于类型参数的类型参数必须是引用类型。所有类类型、接口类型、委托类型、数组类型以及已知为引用类型（如下定义）的类型参数都满足此约束。

值类型约束指定用于类型参数的类型参数必须是不可空值类型。所有不可空 struct 类型、枚举类型以及具有值类型约束的类型参数都满足此约束。请注意，尽管被归类为值类型，可空类型（§4.1.10）不满足值类型约束。具有值类型约束的类型参数也不能具有构造函数约束。

指针类型永远不允许作为类型参数，也不被认为满足引用类型或值类型约束。

如果约束是类类型、接口类型或类型参数，则该类型指定每个用于该类型参数的类型参数必须支持的最小基类型。每当使用构造类型或泛型方法时，类型参数在编译时都会根据类型参数的约束进行检查。提供的类型参数必须满足第 4.4.4 节中描述的条件。

类类型约束必须满足以下规则：

- 类型必须是类类型。
- 类型不能是密封的。
- 类型不得是以下类型之一：System.Array、System.Delegate、System.Enum 或 System.ValueType。
- 类型不得是 object。因为所有类型都派生自 object，如果允许此类约束则不会产生任何效果。
- 对于给定的类型参数，最多只能有一个约束是类类型。

指定为接口类型约束的类型必须满足以下规则：

- 类型必须是接口类型。
- 在给定的 where 子句中，类型不得被指定多次。

在任何一种情况下，约束都可以作为构造类型的一部分涉及关联类型或方法声明的任何类型参数，并且可以涉及正在声明的类型。

作为类型参数约束指定的任何类或接口类型必须至少与正在声明的泛型类型或方法一样可访问（§3.5.4）。

指定为类型参数约束的类型必须满足以下规则：

- 类型必须是类型参数。
- 在给定的 where 子句中，类型不得被指定多次。

此外，类型参数的依赖关系图中不得存在循环，其中依赖关系是由以下定义的传递关系：

- 如果类型参数 T 被用作类型参数 S 的约束，则 S 依赖于 T。
- 如果类型参数 S 依赖于类型参数 T 且 T 依赖于类型参数 U，则 S 依赖于 U。

根据此关系，类型参数依赖于自身（直接或间接）是编译时错误。

任何约束在依赖的类型参数之间必须一致。如果类型参数 S 依赖于类型参数 T，则：

- T 不能具有值类型约束。否则，T effectively sealed，因此 S 将被强制为与 T 相同的类型，从而消除了对两个类型参数的需求。
- 如果 S 具有值类型约束，则 T 不能具有类类型约束。



## C# 语言规范

- 如果 S 具有类类型约束 A 且 T 具有类类型约束 B，则必须存在从 A 到 B 的同一性转换或隐式引用转换，或者存在从 B 到 A 的隐式引用转换。
- 如果 S 还依赖于类型参数 U，且 U 具有类类型约束 A，而 T 具有类类型约束 B，则必须存在从 A 到 B 的同一性转换或隐式引用转换，或者存在从 B 到 A 的隐式引用转换。

S 具有值类型约束而 T 具有引用类型约束是有效的。实际上，这将 T 限制为类型 System.Object、System.ValueType、System.Enum 以及任何接口类型。

如果类型参数的 where 子句包含构造函数约束（其形式为 `new()`），则可以使用 new 运算符创建该类型的实例（§7.6.10.1）。用于具有构造函数约束的类型参数的任何类型实参都必须具有公共无参数构造函数（对于任何值类型，此构造函数隐式存在），或者是具有值类型约束或构造函数约束的类型参数（有关详细信息，请参见 §10.1.5）。

以下是约束的示例：

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
class Printer<T> where T : IPrintable { ... }
class SortedList<T> where T : IComparable<T> { ... }
class Dictionary<K,V>
    where K : IComparable<K>
    where V : IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

以下示例是错误的，因为它导致类型参数的依赖图中出现循环：

```
class Circular<S,T>
    where S : T
    where T : S    // Error, circularity in dependency graph
{
    ...
}
```

以下示例说明了其他无效情况：

```
class Sealed<S,T>
    where S : T
    where T : struct    // Error, T is sealed
{
    ...
}
class A { ... }
class B { ... }
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

类型参数 T 的有效基类定义如下：

- 如果 T 没有主要约束或类型参数约束，则其有效基类为 object。
- 如果 T 具有值类型约束，则其有效基类为 System.ValueType。
- 如果 T 具有类类型约束 C 但没有类型参数约束，则其有效基类为 C。
- 如果 T 没有类类型约束但具有一个或多个类型参数约束，则其有效基类是其类型参数约束的有效基类集合中最包容的类型（§6.4.2）。一致性规则确保存在这样的最包容类型。
- 如果 T 同时具有类类型约束和一个或多个类型参数约束，则其有效基类是以下集合中最包容的类型（§6.4.2）：T 的类类型约束以及其类型参数约束的有效基类。一致性规则确保存在这样的最包容类型。
- 如果 T 具有引用类型约束但没有类类型约束，则其有效基类为 object。

为了这些规则的目的，如果 T 具有一个值类型约束 V，则改用 V 的最特定基类中为类类型的那个。这绝不会在显式给定的约束中发生，但当泛型方法的约束由重写方法声明或接口方法的显式实现隐式继承时可能发生。

这些规则确保有效基类始终是类类型。

类型参数 T 的有效接口集定义如下：

- 如果 T 没有次要约束，则其有效接口集为空。
- 如果 T 具有接口类型约束但没有类型参数约束，则其有效接口集为其接口类型约束集。
- 如果 T 没有接口类型约束但具有类型参数约束，则其有效接口集为其类型参数约束的有效接口集的并集。
- 如果 T 同时具有接口类型约束和类型参数约束，则其有效接口集为其接口类型约束集与其类型参数约束的有效接口集的并集。

如果类型参数具有引用类型约束，或者其有效基类不是 object 或 System.ValueType，则已知该类型参数为引用类型。

受约束的类型参数类型的值可用于访问约束所隐含的实例成员。在示例

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

中，可以直接在 x 上调用 IPrintable 的方法，因为 T 被约束为始终实现 IPrintable。

## 10.1.6 类体

类的类体定义该类的成员。

```
class-body:
    { class-member-declarations_opt }
```

## 10.2 分部类型

类型声明可以拆分到多个分部类型声明中。类型声明按照本节中的规则由其各部分构造而成，随后在程序的编译时和运行时处理的其余部分中将其视为单个声明。

如果类声明、结构声明或接口声明包含 partial 修饰符，则它表示分部类型声明。partial 不是关键字，仅当它在类型声明中紧接在 class、struct 或 interface 关键字之一之前，或在方法声明中紧接在类型 void 之前出现时，才作为修饰符起作用。在其他上下文中，它可以用作普通标识符。

分部类型声明的每个部分都必须包含 partial 修饰符。它必须具有相同的名称，并且与其他部分声明在同一命名空间或类型声明中。partial 修饰符指示类型声明的其他部分可能存在于其他地方，但不要求存在此类其他部分；具有单个声明的类型包含 partial 修饰符是有效的。

分部类型的所有部分必须一起编译，以便这些部分可以在编译时合并为单个类型声明。分部类型特别不允许扩展已编译的类型。

嵌套类型可以使用 partial 修饰符在多个部分中声明。通常，包含类型也使用 partial 声明，并且嵌套类型的每个部分在包含类型的不同部分中声明。

不允许在委托声明或枚举声明上使用 partial 修饰符。

### 10.2.1 特性

分部类型的特性通过以未指定的顺序合并每个部分的特性来确定。如果特性放置在多个部分上，则等效于在该类型上多次指定该特性。例如，以下两个部分：

```
[Attr1, Attr2("hello")]
partial class A {}
[Attr3, Attr2("goodbye")]
partial class A {}
```

等效于如下声明：

```
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

### 10.2.4 基类

当分部类声明包含基类指定时，它必须与包含基类指定的所有其他部分一致。如果分部类的任何部分都不包含基类指定，则基类变为 System.Object（§10.1.4.1）。

### 10.2.5 基接口

在多个部分中声明的类型的基接口集是在每个部分上指定的基接口的并集。特定基接口在每个部分上只能命名一次，但允许多个部分命名相同的基接口。任何给定基接口的成员必须只有一个实现。

在示例

```
partial class C: IA, IB {...}
partial class C: IC {...}
partial class C: IA, IB {...}
```

中，类 C 的基接口集为 IA、IB 和 IC。

通常，每个部分提供在该部分上声明的接口的实现；然而，这不是要求。一个部分可以为在不同部分上声明的接口提供实现：

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

### 10.2.6 成员

除分部方法（§10.2.7）外，在多个部分中声明的类型的成员集只是每个部分中声明的成员集的并集。类型声明的所有部分的体共享同一声明空间（§3.3），并且每个成员（§3.7）的作用域延伸到所有部分的体。任何成员的可访问域始终包括封闭类型的所有部分；在一个部分中声明的私有成员可以从另一个部分自由访问。在类型的多个部分中声明同一成员是编译时错误，除非该成员是具有 partial 修饰符的类型。

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




类型中成员的顺序对 C# 代码来说很少有意义，但在与其他语言和环境交互时可能很重要。在这些情况下，在多个部分中声明的类型中成员的顺序是未定义的。

## 10.2.7 分部方法

分部方法可以在类型声明的一个部分中定义，并在另一个部分中实现。实现是可选的；如果没有部分实现该分部方法，则分部方法声明及其所有调用都会从由各部分组合而成的类型声明中移除。

分部方法不能定义访问修饰符，但隐式是私有的。它们的返回类型必须为 void，并且它们的参数不能具有 out 修饰符。仅当标识符 partial 紧挨在 void 类型之前出现时，才会在方法声明中将其识别为特殊关键字；否则它可以作为普通标识符使用。分部方法不能显式实现接口方法。

分部方法声明有两种：如果方法声明的主体是分号，则该声明称为定义分部方法声明。如果主体以块的形式给出，则该声明称为实现分部方法声明。在类型声明的各个部分中，对于给定签名，只能有一个定义分部方法声明，并且对于给定签名，只能有一个实现分部方法声明。如果给出了实现分部方法声明，则必须存在相应的定义分部方法声明，并且这些声明必须按以下规定匹配：

- 这些声明必须具有相同的修饰符（尽管不一定按相同顺序）、方法名、类型参数数量和参数数量。
- 声明中的对应参数必须具有相同的修饰符（尽管不一定按相同顺序）和相同的类型（类型参数名称的差异除外）。
- 声明中的对应类型参数必须具有相同的约束（类型参数名称的差异除外）。

实现分部方法声明可以与相应的定义分部方法声明出现在同一部分中。

只有定义分部方法参与重载决策。因此，无论是否给出了实现声明，调用表达式都可能解析为对该分部方法的调用。由于分部方法总是返回 void，因此此类调用表达式将始终是表达式语句。此外，由于分部方法是隐式私有的，因此此类语句将始终出现在声明该分部方法的类型声明的某个部分内。

如果分部类型声明的任何部分都不包含针对给定分部方法的实现声明，则调用它的任何表达式语句都会简单地从组合类型声明中移除。因此，该调用表达式（包括任何组成表达式）在运行时没有效果。该分部方法本身也会被移除，并且不会成为组合类型声明的成员。

如果针对给定分部方法存在实现声明，则保留对该分部方法的调用。该分部方法会产生一个类似于实现分部方法声明的方法声明，但以下情况除外：

- 不包含 partial 修饰符
- 生成的方法声明中的特性是定义分部方法声明和实现分部方法声明的特性的组合，顺序未指定。不会移除重复项。
- 生成的方法声明的参数上的特性是定义分部方法声明和实现分部方法声明的对应参数的组合特性，顺序未指定。不会移除重复项。

如果为分部方法 M 给出了定义声明但没有给出实现声明，则以下限制适用：

- 创建指向方法的委托（§7.6.10.5）是编译时错误。
- 在转换为表达式树类型的匿名函数（§6.5.2）中引用 M 是编译时错误。
- 作为 M 调用的一部分出现的表达式不会影响确定赋值状态（§5.3），这可能导致编译时错误。
- M 不能作为应用程序的入口点（§3.1）。

分部方法有助于允许类型声明的一个部分自定义另一个部分的行为，例如，由工具生成的部分。考虑以下分部类声明：

```
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

如果编译该类时没有任何其他部分，则定义分部方法声明及其调用将被移除，并且生成的组合类声明将等效于以下内容：

```
class Customer
{
    string name;
    public string Name {
        get { return name; }
        set { name = value; }
    }
}
```

但是，假设给出了另一个部分，它提供了这些分部方法的实现声明：

```
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

那么生成的组合类声明将等效于以下内容：

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

## 10.2.8 名称绑定

尽管可扩展类型的每个部分都必须在同一命名空间中声明，但这些部分通常写在不同的命名空间声明中。因此，每个部分可能存在不同的 using 指令（§9.4）。在解释某个部分内的简单名称（§7.5.2）时，只考虑包含该部分的命名空间声明的 using 指令。这可能导致同一标识符在不同部分中具有不同含义：

```
namespace N
{
    using List = System.Collections.ArrayList;
    partial class A
    {
        List x;        // x has type System.Collections.ArrayList
    }
}
namespace N
{
    using List = Widgets.LinkedList;
    partial class A
    {
        List y;        // y has type Widgets.LinkedList
    }
}
```

## 10.3 类成员

类的成员由它的类成员声明引入的成员以及从直接基类继承的成员组成。

```
class-member-declarations:
    class-member-declaration
    class-member-declarations  class-member-declaration
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
destructor-declaration
static-constructor-declaration
type-declaration
```

类类型的成员分为以下类别：

- 常量，表示与类关联的常量值（§10.4）。
- 字段，即类的变量（§10.5）。
- 方法，实现类可以执行的计算和操作（§10.6）。
- 属性，定义命名特征以及与读取和写入这些特征相关联的操作（§10.7）。
- 事件，定义类可以生成的通知（§10.8）。
- 索引器，允许以与数组相同的方式（在语法上）为类的实例编制索引（§10.9）。
- 运算符，定义可应用于类实例的表达式运算符（§10.10）。
- 实例构造函数，实现初始化类实例所需的操作（§10.11）
- 析构函数，实现永久丢弃类实例之前要执行的操作（§10.13）。
- 静态构造函数，实现初始化类本身所需的操作（§10.12）。
- 类型，表示类的局部类型（§10.3.8）。

可以包含可执行代码的成员统称为类类型的函数成员。类类型的函数成员是该类类型的方法、属性、事件、索引器、运算符、实例构造函数、析构函数和静态构造函数。

类声明会创建一个新的声明空间（§3.3），并且由类声明直接包含的类成员声明会将新成员引入此声明空间。以下规则适用于类成员声明：

- 实例构造函数、析构函数和静态构造函数必须与直接包含它们的类具有相同的名称。所有其他成员的名称必须不同于直接包含它们的类的名称。
- 常量、字段、属性、事件或类型的名称必须不同于同一类中声明的所有其他成员的名称。
- 方法的名称必须不同于同一类中声明的所有其他非方法的名称。此外，方法的签名（§3.6）必须不同于同一类中声明的所有其他方法的签名，并且同一类中声明的两个方法不能具有仅 ref 和 out 不同的签名。




- 实例构造函数的签名必须与同一类中声明的所有其他实例构造函数的签名不同，并且同一类中声明的两个构造函数不能仅因 ref 和 out 而签名不同。
- 索引器的签名必须与同一类中声明的所有其他索引器的签名不同。
- 运算符的签名必须与同一类中声明的所有其他运算符的签名不同。

类类型的继承成员（§10.3.3）不是类声明空间的一部分。因此，派生类允许声明与继承成员具有相同名称或签名的成员（这实际上隐藏了继承的成员）。

## 10.3.1 实例类型

每个类声明都有一个关联的边界类型（§4.4.3），即实例类型。对于泛型类声明，实例类型是通过从类型声明创建构造类型（§4.4）形成的，其中每个提供的类型实参对应于相应的类型参数。由于实例类型使用了类型参数，它只能在类型参数处于作用域内时使用；也就是说，在类声明内部。实例类型是类声明内部编写的代码中 this 的类型。对于非泛型类，实例类型就是声明的类。以下显示了几个类声明及其实例类型：

```
class A<T> // instance type: A<T>
{
    class B {} // instance type: A<T>.B
    class C<U> {} // instance type: A<T>.C<U>
}
class D {} // instance type: D
```

## 10.3.2 构造类型的成员

构造类型的非继承成员是通过为成员声明中的每个类型参数替换构造类型的相应类型实参获得的。替换过程基于类型声明的语义含义，而不仅仅是文本替换。

例如，给定泛型类声明

```
class Gen<T,U>
{
    public T[,] a;
    public void G(int i, T t, Gen<U,T> gt) {...}
    public U Prop { get {...} set {...} }
    public int H(double d) {...}
}
```

构造类型 Gen<int[], IComparable<string>> 具有以下成员：

```
public int[,][] a;
public void G(int i, int[] t, Gen<IComparable<string>, int[]> gt) {...}
public IComparable<string> Prop { get {...} set {...} }
public int H(double d) {...}
```

泛型类声明 Gen 中成员 a 的类型是“T 的二维数组”，因此上面构造类型中成员 a 的类型是“int 的一维数组的二维数组”，即 int[,][]。

在实例函数成员内部，this 的类型是包含声明的实例类型（§10.3.1）。

泛型类的所有成员都可以使用任何封闭类的类型参数，无论是直接使用还是作为构造类型的一部分。当在运行时使用某个特定的封闭构造类型（§4.4.2）时，每个类型参数的使用都会被替换为提供给构造类型的实际类型实参。例如：

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
        C<int> x1 = new C<int>(1);        // Prints 1
        Console.WriteLine(x1.f1);
        C<double> x2 = new C<double>(3.1415);    // Prints 3.1415
        Console.WriteLine(x2.f1);
    }
}
```

## 10.3.3 继承

类继承其直接基类类型的成员。继承意味着类隐式包含其直接基类类型的所有成员，除了基类的实例构造函数、析构函数和静态构造函数。继承的一些重要方面是：

- 继承是传递的。如果 C 派生自 B，且 B 派生自 A，则 C 继承 B 中声明的成员以及 A 中声明的成员。
- 派生类扩展其直接基类。派生类可以向继承的成员添加新成员，但不能移除继承成员的定义。
- 实例构造函数、析构函数和静态构造函数不会被继承，但所有其他成员都会被继承，无论其声明的可访问性如何（§3.5）。然而，根据其声明的可访问性，继承的成员在派生类中可能无法访问。
- 派生类可以通过声明具有相同名称或签名的新成员来隐藏（§3.7.1.2）继承的成员。但是请注意，隐藏继承的成员并不会删除该成员——它只是使该成员无法直接通过派生类访问。
- 类的一个实例包含该类及其基类中声明的所有实例字段的集合，并且存在从派生类类型到其任何基类类型的隐式转换（§6.1.6）。因此，对某个派生类实例的引用可以被视为对其实任何基类实例的引用。
- 类可以声明虚方法、属性和索引器，并且派生类可以重写这些函数成员的实现。这使得类能够表现出多态行为，其中函数成员调用执行的操作取决于调用该函数成员的实例的运行时类型。

构造类类型的继承成员是直接基类类型的成员（§10.1.4.1），该基类类型是通过将构造类型的类型实参替换为基类规范中相应类型参数的每次出现而找到的。这些成员随后通过为成员声明中的每个类型参数替换基类规范的相应类型实参进行转换。

```
class B<U>
{
    public U F(long index) {...}
}
class D<T>: B<T[]>
{
    public T G(string s) {...}
}
```

在上面的示例中，构造类型 D<int> 具有非继承成员 public int G(string s)，该成员是通过将类型实参 int 替换为类型参数 T 获得的。D<int> 还有一个来自类声明 B 的继承成员。该继承成员是通过首先通过在基类规范 B<T[]> 中将 int 替换为 T 来确定 D<int> 的基类类型 B<int[]> 而确定的。然后，作为 B 的类型实参，int[] 被替换为 public U F(long index) 中的 U，从而得到继承成员 public int[] F(long index)。

## 10.3.4 new 修饰符

类成员声明允许声明与继承成员具有相同名称或签名的成员。当这种情况发生时，派生类成员被认为隐藏了基类成员。隐藏继承的成员不被视为错误，但会导致编译器发出警告。为了抑制警告，派生类成员的声明可以包含 new 修饰符，以指示派生成员旨在隐藏基成员。该主题在 §3.7.1.2 中进一步讨论。

如果在不隐藏继承成员的声明中包含 new 修饰符，则会发出相应的警告。通过移除 new 修饰符可以抑制此警告。

## 10.3.5 访问修饰符

类成员声明可以具有五种可能声明的可访问性（§3.5.1）中的任意一种：public、protected internal、protected、internal 或 private。除了 protected internal 组合外，指定多个访问修饰符是编译时错误。当类成员声明不包含任何访问修饰符时，默认为 private。

## 10.3.6 构成类型

在成员声明中使用的类型称为该成员的构成类型。可能的构成类型包括常量、字段、属性、事件或索引器的类型，方法或运算符的返回类型，以及方法、索引器、运算符或索引构造函数的参数类型。成员的构成类型必须至少与该成员本身一样可访问（§3.5.4）。

## 10.3.7 静态成员和实例成员

类的成员要么是静态成员，要么是实例成员。一般来说，将静态成员视为属于类类型，而将实例成员视为属于对象（类类型的实例）是有用的。

当字段、方法、属性、事件、运算符或构造函数声明包含 static 修饰符时，它声明一个静态成员。此外，常量或类型声明隐式声明一个静态成员。静态成员具有以下特征：

- 当静态成员 M 在形式为 E.M 的成员访问（§7.6.4）中被引用时，E 必须表示包含 M 的类型。E 表示实例是编译时错误。
- 静态字段标识一个存储位置，该位置由给定封闭类类型的所有实例共享。不管创建了多少个给定封闭类类型的实例，静态字段永远只有一个副本。



- 静态函数成员（方法、属性、事件、运算符或构造函数）不作用于特定实例，在这样的函数成员中引用 this 是编译时错误。

当字段、方法、属性、事件、索引器、构造函数或析构函数声明不包含 static 修饰符时，它声明的是实例成员。（实例成员有时称为非静态成员。）实例成员具有以下特征：

- 当在形式为 E.M 的成员访问（§7.6.4）中引用实例成员 M 时，E 必须表示包含 M 的类型的实例。E 表示类型是绑定期错误。
- 类的每个实例都包含该类所有实例字段的一组独立副本。
- 实例函数成员（方法、属性、索引器、实例构造函数或析构函数）作用于类的给定实例，并且可以通过 this（§7.6.7）访问该实例。

以下示例说明了访问静态成员和实例成员的规则：

```
class Test
{
    int x;
    static int y;
    void F() {
        x = 1;      // Ok, same as this.x = 1
        y = 1;      // Ok, same as Test.y = 1
    }
    static void G() {
        x = 1;      // Error, cannot access this.x
        y = 1;      // Ok, same as Test.y = 1
    }
    static void Main() {
        Test t = new Test();
        t.x = 1;    // Ok
        t.y = 1;    // Error, cannot access static member through instance
        Test.x = 1; // Error, cannot access instance member through type
        Test.y = 1; // Ok
    }
}
```

F 方法表明，在实例函数成员中，可以使用简单名（§7.6.2）访问实例成员和静态成员。G 方法表明，在静态函数成员中，通过简单名访问实例成员是编译时错误。Main 方法表明，在成员访问（§7.6.4）中，实例成员必须通过实例访问，静态成员必须通过类型访问。

## 10.3.8 嵌套类型

在类或结构声明中声明的类型称为嵌套类型。在编译单元或命名空间中声明的类型称为非嵌套类型。

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

### 10.3.8.1 完全限定名

嵌套类型的完全限定名（§3.8.1）是 S.N，其中 S 是声明类型 N 的类型的完全限定名。

### 10.3.8.2 声明可访问性

非嵌套类型可以具有 public 或 internal 声明可访问性，并且默认具有 internal 声明可访问性。嵌套类型也可以具有这些形式的声明可访问性，并且还可以具有一种或多种其他形式的声明可访问性，具体取决于包含类型是类还是结构：

- 在类中声明的嵌套类型可以具有五种声明可访问性中的任意一种（public、protected internal、protected、internal 或 private），并且与其他类成员一样，默认具有 private 声明可访问性。
- 在结构中声明的嵌套类型可以具有三种声明可访问性中的任意一种（public、internal 或 private），并且与其他结构成员一样，默认具有 private 声明可访问性。

示例

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

声明了一个私有嵌套类 Node。

### 10.3.8.3 隐藏

嵌套类型可以隐藏（§3.7.1）基成员。嵌套类型声明上允许使用 new 修饰符，以便可以显式表达隐藏。示例

```csharp
using System;
class Base
{
    public static void M() {
        Console.WriteLine("Base.M");
    }
}
```

```
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

展示了类 C，它包含嵌套类 Nested。在 Nested 内，方法 G 调用在 C 中定义的静态方法 F，并且 F 具有 private 声明可访问性。

嵌套类型还可以访问在其包含类型的基类型中定义的受保护成员。在以下示例中

```
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
            d.F();    // ok
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

嵌套类 Derived.Nested 通过 Derived 的实例进行调用，访问在 Derived 的基类 Base 中定义的受保护方法 F。

### 10.3.8.6 泛型类中的嵌套类型

泛型类声明可以包含嵌套类型声明。外层类的类型参数可以在嵌套类型内使用。嵌套类型声明可以包含仅适用于该嵌套类型的其他类型参数。

泛型类声明中包含的每个类型声明都隐式是泛型类型声明。当编写对嵌套在泛型类型中的类型的引用时，必须命名包含它的构造类型，包括其类型实参。但是，在外层类内部，可以不加限定地使用嵌套类型；构造嵌套类型时，可以隐式使用外层类的实例类型。以下示例展示了三种引用由 Inner 创建的构造类型的不同正确方式；前两种是等效的：

```
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }
    static void F(T t) {
        Outer<T>.Inner<string>.F(t, "abc");    // These two statements have
        Inner<string>.F(t, "abc");    // the same effect
        Outer<int>.Inner<string>.F(3, "abc");    // This type is different
        Outer.Inner<string>.F(t, "abc");    // Error, Outer needs type arg
    }
}
```

尽管这是不良编程风格，但嵌套类型中的类型参数可以隐藏在外层类型中声明的成员或类型参数：

```
class Outer<T>
{
    class Inner<T>    // valid, hides Outer's T
    {
        public T t;    // Refers to Inner's T
    }
}
```

## 10.3.9 保留成员名

为了便于底层 C# 运行时实现，对于每个作为属性、事件或索引器的源成员声明，实现必须根据成员声明的种类、名称和类型保留两个方法签名。如果程序声明了签名与这些保留签名之一匹配的成员，则会产生编译时错误，即使底层运行时实现不使用这些保留签名。

保留名称不引入声明，因此不参与成员查找。但是，声明关联的保留方法签名确实参与继承（§10.3.3），并且可以用 new 修饰符（§10.3.4）隐藏。

保留这些名称有三个目的：

- 允许底层实现使用普通标识符作为方法名，以对 C# 语言特性进行 get 或 set 访问。
- 允许其他语言使用普通标识符作为方法名进行互操作，以对 C# 语言特性进行 get 或 set 访问。
- 通过使保留成员名的具体细节在所有 C# 实现中保持一致，帮助确保一个符合规范的编译器接受的源代码也能被另一个编译器接受。

析构函数（§10.13）的声明也会导致保留一个签名（§10.3.9.4）。

### 10.3.9.1 为属性保留的成员名

对于类型 T 的属性 P（§10.7），保留以下签名：

```
T get_P();
void set_P(T value);
```



即使属性是只读或只写的，两个签名也都会保留。

在下面的示例中：

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

类 A 定义只读属性 P，因此保留了 get_P 和 set_P 方法的签名。类 B 从 A 派生，并隐藏了这两个保留的签名。该示例产生以下输出：

```
123
123
456
```

### 10.3.9.2 为事件保留的成员名称

对于委托类型 T 的事件 E（§10.8），保留以下签名：

```csharp
void add_E(T handler);
void remove_E(T handler);
```

### 10.3.9.3 为索引器保留的成员名称

对于类型为 T、参数列表为 L 的索引器（§10.9），保留以下签名：

```csharp
T get_Item(L);
void set_Item(L, T value);
```

即使索引器是只读或只写的，两个签名也都会保留。

此外，成员名 Item 也会保留。

### 10.3.9.4 为析构函数保留的成员名称

对于包含析构函数（§10.13）的类，保留以下签名：

```csharp
void Finalize();
```

## 10.4 常量

*常量*是表示常量值的类成员：该值可在编译时计算。*常量声明*引入一个或多个给定类型的常量。

```text
constant-declaration:
    attributes_opt constant-modifiers_opt const type constant-declarators ;
constant-modifiers:
    constant-modifier
    constant-modifier constant-modifier
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
```

常量声明可以包含一组特性（§17）、一个 new 修饰符（§10.3.4），以及四个访问修饰符（§10.3.5）的有效组合。特性和修饰符应用于该常量声明所声明的所有成员。即使常量被视为静态成员，常量声明既不要求也不允许 static 修饰符。同一修饰符在常量声明中出现多次是错误的。

常量声明的类型指定该声明所引入成员的类型。类型后跟常量声明符列表，其中每个常量声明符引入一个新成员。常量声明符由一个命名该成员的标识符、一个“=”标记以及一个给出该成员值的常量表达式（§7.19）组成。

常量声明中指定的类型必须是 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool、string、枚举类型或引用类型。每个常量表达式必须产生目标类型的值，或产生可通过隐式转换（§6.1）转换为目标类型的值。

常量的类型必须至少与常量本身具有相同的可访问性（§3.5.4）。

在表达式中，可使用简单名称（§7.6.2）或成员访问（§7.6.4）获取常量的值。

常量本身可以参与常量表达式。因此，常量可用于任何需要常量表达式的构造。此类构造的示例包括 case 标签、goto case 语句、枚举成员声明、特性以及其他常量声明。

如 §7.19 所述，常量表达式是可在编译时完全求值的表达式。由于创建除 string 以外的引用类型的非 null 值的唯一方式是应用 new 运算符，并且常量表达式中不允许使用 new 运算符，因此除 string 以外的引用类型常量唯一可能的值是 null。

当需要为常量值使用符号名称，但该值的类型不允许用于常量声明，或者该值无法由常量表达式在编译时计算时，可以改用 readonly 字段（§10.5.2）。

声明多个常量的常量声明等效于多个具有相同特性、修饰符和类型的单常量声明。例如

```csharp
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```

等效于

```csharp
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

只要依赖关系不是循环的，就允许常量依赖同一程序中的其他常量。编译器会自动安排以适当的顺序对常量声明求值。在示例中

```csharp
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

编译器首先对 A.Y 求值，然后对 B.Z 求值，最后对 A.X 求值，产生值 10、11 和 12。常量声明可以依赖其他程序中的常量，但这种依赖只能沿一个方向进行。参考上面的示例，如果 A 和 B 声明在不同程序中，则 A.X 可以依赖 B.Z，但此时 B.Z 不能同时依赖 A.Y。

## 10.5 字段

*字段*是表示与对象或类关联的变量的成员。*字段声明*引入一个或多个给定类型的字段。

```text
field-declaration:
    attributes_opt   field-modifiers_opt   type   variable-declarators   ;

field-modifiers:
    field-modifier
    field-modifiers  field-modifier

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
```

```text
    variable-declarator:
        identifier
        identifier = variable-initializer

    variable-initializer:
        expression
        array-initializer
```

字段声明可以包含一组特性（§17）、一个 new 修饰符（§10.3.4）、四个访问修饰符（§10.3.5）的有效组合，以及一个 static 修饰符（§10.5.1）。此外，字段声明可以包含 readonly 修饰符（§10.5.2）或 volatile 修饰符（§10.5.3），但不能同时包含二者。特性和修饰符应用于该字段声明所声明的所有成员。同一修饰符在字段声明中出现多次是错误的。

字段声明的类型指定该声明所引入成员的类型。类型后跟变量声明符列表，其中每个变量声明符引入一个新成员。变量声明符由一个命名该成员的标识符组成，后面可选地跟一个“=”标记和一个给出该成员初始值的变量初始值设定项（§10.5.5）。

字段的类型必须至少与字段本身具有相同的可访问性（§3.5.4）。

在表达式中，可使用简单名称（§7.6.2）或成员访问（§7.6.4）获取字段的值。使用赋值（§7.17）修改非 readonly 字段的值。使用后缀递增和递减运算符（§7.6.9）以及前缀递增和递减运算符（§7.7.5）既可以获取也可以修改非 readonly 字段的值。

声明多个字段的字段声明等效于多个具有相同特性、修饰符和类型的单字段声明。例如

```
    class A
    {
        public static int X = 1, Y, Z = 100;
    }
```

等效于

```
    class A
    {
        public static int X = 1;
        public static int Y;
        public static int Z = 100;
    }
```

### 10.5.1 静态字段和实例字段

当字段声明包含 static 修饰符时，该声明引入的字段是静态字段。当不存在 static 修饰符时，该声明引入的字段是实例字段。静态字段和实例字段是 C# 支持的若干种变量（§5）中的两种，有时分别称为静态变量和实例变量。

静态字段不属于特定实例；相反，它在封闭类型（§4.4.2）的所有实例之间共享。无论创建多少个封闭类类型的实例，对于关联的应用程序域，静态字段始终只有一个副本。

例如：

```
    class C<V>
    {
        static int count = 0;
    }
```




```
    public C() {
        count++;
    }
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
            Console.WriteLine(C<int>.Count);      // Prints 1
            C<double> x2 = new C<double>();
            Console.WriteLine(C<int>.Count);      // Prints 1
            C<int> x3 = new C<int>();
            Console.WriteLine(C<int>.Count);      // Prints 2
        }
    }
```

实例字段属于实例。具体而言，类的每个实例都包含该类的所有实例字段的一组独立副本。

当在形式为 E.M 的成员访问（§7.6.4）中引用字段时，如果 M 是静态字段，则 E 必须表示包含 M 的类型；如果 M 是实例字段，则 E 必须表示包含 M 的类型的实例。

静态成员与实例成员之间的差异将在 §10.3.7 中进一步讨论。

## 10.5.2 只读字段

当*字段声明*包含 readonly 修饰符时，该声明引入的字段为*只读字段*。对只读字段的直接赋值只能作为该声明的一部分，或在同一个类中的实例构造函数或静态构造函数中发生。（在这些上下文中，可以对一个只读字段多次赋值。）具体而言，仅在以下上下文中允许对*只读字段*进行直接赋值：

- 在引入该字段的*变量声明符*中（通过在声明中包含*变量初始值设定项*）。
- 对于实例字段，在包含该字段声明的类的实例构造函数中；对于静态字段，在包含该字段声明的类的静态构造函数中。这些也是将*只读字段*作为 *out* 或 *ref* 参数传递唯一有效的上下文。

在任何其他上下文中尝试对*只读字段*赋值或将其作为 *out* 或 *ref* 参数传递，都是编译时错误。

### 10.5.2.1 使用静态只读字段表示常量

当需要为某个常量值提供符号名称，但该值的类型不允许在 const 声明中使用，或者该值无法在编译时计算时，静态只读字段很有用。在示例

```
    public class Color
    {
        public static readonly Color Black = new Color(0, 0, 0);
        public static readonly Color White = new Color(255, 255, 255);
        public static readonly Color Red = new Color(255, 0, 0);
        public static readonly Color Green = new Color(0, 255, 0);
        public static readonly Color Blue = new Color(0, 0, 255);

        private byte red, green, blue;
    }
```

```
public Color(byte r, byte g, byte b) {
    red = r;
    green = g;
    blue = b;
}
```

Black、White、Red、Green 和 Blue 成员不能声明为 const 成员，因为它们的值无法在编译时计算。然而，改为将它们声明为静态只读字段具有大致相同的效果。

### 10.5.2.2 常量与静态只读字段的版本管理

常量和只读字段具有不同的二进制版本管理语义。当表达式引用常量时，常量的值在编译时获取；但当表达式引用只读字段时，字段的值要到运行时才获取。考虑一个由两个独立程序组成的应用程序：

```
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
```

Program1 和 Program2 命名空间表示两个分别编译的程序。因为 Program1.Utils.X 声明为静态只读字段，所以 Console.WriteLine 语句输出的值在编译时未知，而是在运行时获取。因此，如果 X 的值发生更改并重新编译 Program1，则即使不重新编译 Program2，Console.WriteLine 语句也会输出新值。然而，如果 X 是常量，则 X 的值会在编译 Program2 时获取，并且在重新编译 Program2 之前不受 Program1 更改的影响。

## 10.5.3 易失字段

当字段声明包含 volatile 修饰符时，该声明引入的字段为易失字段。

对于非易失字段，重排指令的优化技术可能会在未经同步（例如 lock 语句（§8.12）所提供的同步）而访问字段的多线程程序中导致意外且不可预测的结果。这些优化可由编译器、运行时系统或硬件执行。对于易失字段，此类重排优化受到限制：

- 对易失字段的读取称为易失读取。易失读取具有“获取语义”；也就是说，它保证发生在指令序列中位于其后的任何内存引用之前。
- 对易失字段的写入称为易失写入。易失写入具有“释放语义”；也就是说，它保证发生在指令序列中位于写入指令之前的任何内存引用之后。

这些限制确保所有线程都将按照其他线程执行易失写入的顺序观察到这些写入。符合规范的实现不要求提供从所有执行线程看到的易失写入的单一全序。易失字段的类型必须是下列类型之一：

- *引用类型*。
- 类型 `byte`、`sbyte`、`short`、`ushort`、`int`、`uint`、`char`、`float`、`bool`、`System.IntPtr` 或 `System.UIntPtr`。
- 具有 `byte`、`sbyte`、`short`、`ushort`、`int` 或 `uint` 枚举基类型的*枚举类型*。

示例

```csharp
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
        // Wait for Thread2 to signal that it has a result by setting
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

```text
result = 143
```

在此示例中，方法 `Main` 启动一个新线程来运行方法 `Thread2`。此方法将值存储到名为 `result` 的非易失字段中，然后将 `true` 存储到易失字段 `finished` 中。主线程等待字段 `finished` 被设置为 `true`，然后读取字段 `result`。由于 `finished` 已声明为 `volatile`，主线程必须从字段 `result` 读取值 143。如果字段 `finished` 未声明为 `volatile`，则允许对 `result` 的存储在对 `finished` 的存储*之后*才对主线程可见，因此主线程可能会从字段 `result` 读取值 0。将 `finished` 声明为 `volatile` 字段可防止任何此类不一致。

## 10.5.4 字段初始化

字段的初始值，无论是静态字段还是实例字段，都是该字段类型的默认值（§5.2）。在发生此默认初始化之前，不可能观察到字段的值，因此字段永远不会“未初始化”。示例

```csharp
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
```

产生输出

```
b = False, i = 0
```

因为 b 和 i 都自动初始化为默认值。

## 10.5.5 变量初始值设定项

字段声明可以包含*变量初始值设定项*。对于静态字段，变量初始值设定项对应于在类初始化期间执行的赋值语句。对于实例字段，变量初始值设定项对应于在创建类的实例时执行的赋值语句。

示例

```csharp
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

```
x = 1.4142135623731, i = 100, s = Hello
```

因为对 x 的赋值在静态字段初始值设定项执行时发生，而对 i 和 s 的赋值在实例字段初始值设定项执行时发生。

§10.5.4 中描述的默认值初始化会对所有字段发生，包括具有变量初始值设定项的字段。因此，当初始化一个类时，该类中的所有静态字段首先初始化为其默认值，然后按文本顺序执行静态字段初始值设定项。同样，当创建类的实例时，该实例中的所有实例字段首先初始化为其默认值，然后按文本顺序执行实例字段初始值设定项。

有可能观察到具有变量初始值设定项的静态字段处于其默认值状态。然而，从风格上强烈不建议这样做。示例

```csharp
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




表现出这种行为。尽管 a 和 b 的定义是循环的，该程序仍然有效。它产生以下输出

```
a = 1, b = 2
```

因为静态字段 a 和 b 在执行它们的初始化器之前被初始化为 0（int 的默认值）。当 a 的初始化器运行时，b 的值为零，因此 a 被初始化为 1。当 b 的初始化器运行时，a 的值已经是 1，因此 b 被初始化为 2。

## 10.5.5.1 静态字段初始化

类的静态字段变量初始化器对应于一系列赋值，这些赋值按照它们在类声明中出现的文本顺序执行。如果类中存在静态构造函数（§10.12），则静态字段初始化器的执行紧接在执行该静态构造函数之前发生。否则，静态字段初始化器将在首次使用该类的静态字段之前、由实现决定的时间执行。下面的示例

```
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

可能产生以下任一输出：

```
Init A
Init B
1 1
```

或者以下输出：

```
Init B
Init A
1 1
```

因为 X 的初始化器和 Y 的初始化器的执行可以以任意顺序发生；它们只被约束为必须在这两个字段被引用之前发生。然而，在下面的示例中：

```
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

输出必须是：

```
Init B
Init A
1 1
```

因为关于静态构造函数何时执行的规则（如 §10.12 所定义）规定，B 的静态构造函数（因而 B 的静态字段初始化器）必须在 A 的静态构造函数和字段初始化器之前运行。

## 10.5.5.2 实例字段初始化

类的实例字段变量初始化器对应于一系列赋值，这些赋值在进入该类的任意一个实例构造函数（§10.11.1）时立即执行。变量初始化器按照它们在类声明中出现的文本顺序执行。类实例创建和初始化过程在 §10.11 中进一步描述。

实例字段的变量初始化器不能引用正在创建的实例。因此，变量初始化器在变量初始化器中引用 this 是编译时错误，同样，变量初始化器通过简单名称引用任何实例成员也是编译时错误。在下面的示例中

```
class A
{
    int x = 1;
    int y = x + 1;  // Error, reference to instance member of this
}
```

y 的变量初始化器会导致编译时错误，因为它引用了正在创建的实例的成员。

## 10.6 方法

方法是实现对象或类可执行的计算或操作的成员。方法使用 method-declaration 声明：

```
method-declaration:
    method-header method-body

method-header:
    attributesopt method-modifiersopt partialopt return-type member-name type-parameter-listopt
    ( formal-parameter-listopt ) type-parameter-constraints-clausesopt

method-modifiers:
    method-modifier
    method-modifiers method-modifier
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

return-type:
  type
  void

member-name:
  identifier
  interface-type . identifier

method-body:
  block
  ;

一个 method-declaration 可以包含一组属性（§17）以及四种访问修饰符（§10.3.5）和 new（§10.3.4）、static（§10.6.2）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符的有效组合。

如果以下所有条件都成立，则声明具有有效的修饰符组合：

- 声明包含访问修饰符（§10.3.5）的有效组合。
- 声明不包含同一修饰符多次。
- 声明至多包含以下修饰符之一：static、virtual 和 override。
- 声明至多包含以下修饰符之一：new 和 override。
- 如果声明包含 abstract 修饰符，则声明不包含以下任何修饰符：static、virtual、sealed 或 extern。
- 如果声明包含 private 修饰符，则声明不包含以下任何修饰符：virtual、override 或 abstract。
- 如果声明包含 sealed 修饰符，则声明还包含 override 修饰符。
- 如果声明包含 partial 修饰符，则它不包含以下任何修饰符：new、public、protected、internal、private、virtual、sealed、override、abstract 或 extern。

方法声明的 return-type 指定该方法计算并返回的值的类型。如果方法不返回值，则 return-type 为 void。如果声明包含 partial 修饰符，则返回类型必须为 void。

member-name 指定方法的名称。除非方法是显式接口成员实现（§13.4.1），否则 member-name 只是一个标识符。对于显式接口成员实现，member-name 由一个 interface-type 后跟一个“.”和一个标识符组成。

可选的 type-parameter-list 指定方法的类型参数（§10.1.3）。如果指定了 type-parameter-list，则该方法为泛型方法。如果方法具有 extern 修饰符，则不能指定 type-parameter-list。

可选的 formal-parameter-list 指定方法的参数（§10.6.1）。

可选的 type-parameter-constraints-clauses 指定对各个类型参数的约束（§10.1.5），并且仅当同时提供了 type-parameter-list 且该方法不具有 override 修饰符时才能指定。

方法的 return-type 以及 formal-parameter-list 中引用的每个类型必须至少与该方法本身一样可访问（§3.5.4）。

对于 abstract 和 extern 方法，method-body 仅由一个分号组成。对于 partial 方法，method-body 可以由一个分号或一个块组成。对于所有其他方法，method-body 由一个块组成，该块指定调用方法时要执行的语句。

方法的名称、类型参数列表和形参列表定义该方法的签名（§3.6）。具体而言，方法的签名由其名称、类型参数的数量以及形参的数量、修饰符和类型组成。为此，方法中出现在形参类型中的任何类型参数不是通过其名称来标识，而是通过其在方法的类型实参列表中的序号位置来标识。返回类型不是方法签名的一部分，类型参数或形参的名称也不是。

方法的名称必须不同于同一类中声明的所有其他非方法成员的名称。此外，方法的签名必须不同于同一类中声明的所有其他方法的签名，并且同一类中声明的两个方法不能具有仅因 ref 和 out 而不同的签名。

方法的类型参数在整个 method-declaration 中都在作用域内，并且可以在该作用域内用于在 return-type、method-body 和 type-parameter-constraints-clauses 中构成类型，但不能在属性中构成类型。

所有形参和类型参数必须具有不同的名称。

## 10.6.1 方法参数

方法的参数（如果有）由该方法的 formal-parameter-list 声明。

```
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
```



形参列表由一个或多个以逗号分隔的参数组成，其中只有最后一个参数可以是参数数组。

固定参数由可选的特性集（§17）、可选的 ref、out 或 this 修饰符、一个类型、一个标识符和一个可选的默认实参组成。每个固定参数声明一个具有给定类型和给定名称的参数。this 修饰符将方法指定为扩展方法，并且只允许在静态方法的第一个参数上使用。扩展方法在 §10.6.9 中进一步描述。

带默认实参的固定参数称为可选参数，而不带默认实参的固定参数是必需参数。必需参数不能出现在形参列表中的可选参数之后。

ref 或 out 参数不能有默认实参。默认实参中的表达式必须是下列之一：

- 常量表达式
- 形式为 new S() 的表达式，其中 S 是值类型
- 形式为 default(S) 的表达式，其中 S 是值类型

该表达式必须能通过恒等转换或可空转换隐式转换为该参数的类型。

如果可选参数出现在实现分部方法声明（§10.2.7）、显式接口成员实现（§13.4.1）或单参数索引器声明（§10.9）中，编译器应给出警告，因为这些成员永远无法以允许省略实参的方式调用。

参数数组由可选的特性集（§17）、params 修饰符、数组类型和标识符组成。参数数组声明一个具有给定数组类型和给定名称的单个参数。参数数组的数组类型必须是一维数组类型（§12.1）。在方法调用中，参数数组允许指定一个给定数组类型的单个实参，或者允许指定零个或多个数组元素类型的实参。参数数组在 §10.6.1.4 中进一步描述。

参数数组可以出现在可选参数之后，但不能有默认值——省略参数数组的实参反而会导致创建空数组。

下面的示例说明不同类型的参数：

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

在 M 的形参列表中，i 是必需的 ref 参数，d 是必需的值参数，b、s、o 和 t 是可选值参数，a 是参数数组。

方法声明为参数、类型参数和局部变量创建单独的声明空间。名称由方法的类型参数列表和形参列表以及方法块中的局部变量声明引入此声明空间。方法声明空间的两个成员同名是错误的。若方法声明空间与嵌套声明空间的局部变量声明空间包含同名元素，则是错误。

方法调用（§7.6.5.1）会创建该方法形参和局部变量的副本，该副本特定于该调用；调用的实参列表会将值或变量引用赋给新创建的形参。

在方法块内，可以通过形参的标识符在简单名称表达式（§7.6.2）中引用形参。

形参有四类：

- 值参数，声明时不带任何修饰符。
- 引用参数，使用 ref 修饰符声明。
- 输出参数，使用 out 修饰符声明。
- 参数数组，使用 params 修饰符声明。

如 §3.6 所述，ref 和 out 修饰符是方法签名的一部分，但 params 修饰符不是。

### 10.6.1.1 值参数

不带修饰符声明的参数是值参数。值参数对应于一个局部变量，该局部变量从方法调用中提供的对应实参获取初始值。

当形参是值参数时，方法调用中的对应实参必须是可隐式转换（§6.1）为形参类型的表达式。

允许方法向值参数赋予新值。此类赋值只影响该值参数所表示的本地存储位置——对方法调用中给定的实际实参没有影响。

### 10.6.1.2 引用参数

使用 ref 修饰符声明的参数是引用参数。与值参数不同，引用参数不会创建新的存储位置。相反，引用参数表示与方法调用中作为实参给出的变量相同的存储位置。

当形参是引用参数时，方法调用中的对应实参必须由关键字 ref 后跟与形参类型相同的变量引用（§5.3.3）组成。变量在作为引用参数传递之前必须明确赋值。

在方法内，引用参数始终被视为已明确赋值。

声明为迭代器（§10.14）的方法不能有引用参数。

示例

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

生成输出

i = 2, j = 1

对于 Main 中对 Swap 的调用，x 表示 i，y 表示 j。因此，该调用具有交换 i 和 j 的值的效果。

在采用引用参数的方法中，多个名称可能表示同一个存储位置。在示例

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

G 中对 F 的调用为 a 和 b 二者传递对 s 的引用。因此，对于该调用，名称 s、a 和 b 都引用同一个存储位置，并且这三个赋值都修改实例字段 s。

### 10.6.1.3 输出参数

使用 out 修饰符声明的参数是输出参数。与引用参数类似，输出参数不会创建新的存储位置。相反，输出参数表示与方法调用中作为实参给出的变量相同的存储位置。

当形参是输出参数时，方法调用中的对应实参必须由关键字 out 后跟与形参类型相同的变量引用（§5.3.3）组成。变量在作为输出参数传递之前不必明确赋值，但在将变量作为输出参数传递的调用之后，该变量被视为已明确赋值。

在方法内，与局部变量一样，输出参数最初被视为未赋值，并且在其值被使用之前必须明确赋值。

方法的每个输出参数都必须在该方法返回之前明确赋值。

声明为分部方法（§10.2.7）或迭代器（§10.14）的方法不能有输出参数。

输出参数通常用于产生多个返回值的方法。例如：

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
}
```



```
static void Main() {
    string dir, name;
    SplitPath("c:\\windows\\System\\hello.txt", out dir, out name);
    Console.WriteLine(dir);
    Console.WriteLine(name);
}
}
```

示例产生的输出为：

```
c:\windows\System\
hello.txt
```

请注意，dir 和 name 变量在传递给 SplitPath 之前可以未赋值，并且在调用之后被认为是已明确赋值。

## 10.6.1.4 参数数组

使用 params 修饰符声明的参数是参数数组。如果形式参数列表包含参数数组，则它必须是列表中的最后一个参数，并且必须是单维数组类型。例如，类型 string[] 和 string[][] 可用作参数数组的类型，但类型 string[,] 不可以。params 修饰符不能与 ref 和 out 修饰符组合使用。

参数数组允许在方法调用中以两种方式指定参数：

-   为参数数组提供的参数可以是一个表达式，该表达式可隐式转换为 (§6.1) 参数数组类型。在这种情况下，参数数组完全像值参数一样工作。
-   或者，调用可以为参数数组指定零个或多个参数，其中每个参数都是可隐式转换为 (§6.1) 参数数组元素类型的表达式。在这种情况下，调用会创建一个长度与参数数量相对应的参数数组类型实例，用给定的参数值初始化数组实例的元素，并将新创建的数组实例用作实际参数。

除允许在调用中具有可变数量的参数外，参数数组与相同类型的值参数 (§10.6.1.1) 完全等价。

示例

```
using System;
class Test
{
    static void F(params int[] args) {
        Console.Write("Array contains {0} elements:", args.Length);
        foreach (int i in args)
            Console.Write(" {0}", i);
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

产生的输出为

```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

F 的第一次调用只是将数组 arr 作为值参数传递。F 的第二次调用自动创建一个包含给定元素值的四元素 int[]，并将该数组实例作为值参数传递。同样，F 的第三次调用创建一个零元素 int[] 并将该实例作为值参数传递。第二次和第三次调用与编写以下内容完全等价：

```
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

在执行重载解析时，具有参数数组的方法可能在其常规形式或其扩展形式 (§7.5.3.1) 下适用。方法的扩展形式只有在该方法的常规形式不适用并且同一类型中尚未声明具有与扩展形式相同签名的 方法时才可用。

示例

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

产生的输出为

```
F()
F(object[])
F(object,object)
F(object[])
F(object[])
```

在示例中，参数数组方法可能的两种扩展形式已作为常规方法包含在类中。因此，在执行重载解析时不会考虑这些扩展形式，因此第一次和第三次方法调用选择常规方法。当类声明具有参数数组的方法时，同时包含一些扩展形式作为常规方法并不罕见。通过这样做，可以避免在调用具有参数数组的方法的扩展形式时发生的数组实例分配。

当参数数组的类型为 object[] 时，方法常规形式与单个 object 参数的扩展形式之间会出现潜在的歧义。产生歧义的原因是 object[] 本身可隐式转换为 object 类型。然而，这种歧义不会造成问题，因为如果需要，可以通过插入强制转换来解决。

示例

```
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

产生的输出为

```
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
```

在 F 的第一次和最后一次调用中，F 的常规形式适用，因为从参数类型到参数类型的隐式转换存在（两者均为 object[] 类型）。因此，重载解析选择 F 的常规形式，并且参数作为常规值参数传递。在第二次和第三次调用中，F 的常规形式不适用，因为从参数类型到参数类型不存在隐式转换（object 类型不能隐式转换为 object[] 类型）。然而，F 的扩展形式适用，因此被重载解析选中。结果，调用创建了一个一元素 object[]，并且数组的单个元素用给定的参数值初始化（该值本身是对 object[] 的引用）。

## 10.6.2 静态方法和实例方法

当方法声明包含 static 修饰符时，该方法称为静态方法。当没有 static 修饰符时，该方法称为实例方法。

静态方法不操作特定实例，在静态方法中引用 this 会导致编译时错误。

实例方法操作类的给定实例，并且该实例可以作为 this (§7.6.7) 访问。

当方法在形式为 E.M 的成员访问 (§7.6.4) 中被引用时，如果 M 是静态方法，则 E 必须表示包含 M 的类型；如果 M 是实例方法，则 E 必须表示包含 M 的类型的实例。

静态成员和实例成员之间的差异在 §10.3.7 中进一步讨论。

## 10.6.3 虚方法

当实例方法声明包含 virtual 修饰符时，该方法称为虚方法。当没有 virtual 修饰符时，该方法称为非虚方法。

非虚方法的实现是不变的：无论方法是在声明它的类的实例上调用还是在派生类的实例上调用，实现都相同。相比之下，虚方法的实现可以被派生类取代。取代继承的虚方法实现的进程称为重写该方法 (§10.6.4)。

在虚方法调用中，进行该调用的实例的运行时类型决定要调用的实际方法实现。在非虚方法调用中，实例的编译时类型是决定因素。具体来说，当在编译时类型为 C 且运行时类型为 R（其中 R 为 C 或派生自 C 的类）的实例上使用参数列表 A 调用名为 N 的方法时，调用按如下方式处理：

-   首先，对 C、N 和 A 应用重载解析，以从声明于 C 中并继承自 C 的方法集合中选择特定方法 M。这在 §7.6.5.1 中描述。
-   然后，如果 M 是非虚方法，则调用 M。
-   否则，M 是虚方法，并且相对于 R 调用 M 的最派生实现。

对于声明于类中或继承自类的每个虚方法，相对于该类都存在该方法的最派生实现。相对于类 R 的虚方法 M 的最派生实现按如下方式确定：

-   如果 R 包含 M 的引入虚声明，则这是 M 的最派生实现。
-   否则，如果 R 包含 M 的重写，则这是 M 的最派生实现。
-   否则，相对于 R 的 M 的最派生实现与相对于 R 的直接基类的 M 的最派生实现相同。

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

在示例中，A 引入了非虚方法 F 和虚方法 G。类 B 引入了一个新的非虚方法 F，从而隐藏了继承的 F，并重写了继承的方法 G。示例产生的输出为：

```
A.F
B.F
B.G
B.G
```

请注意，语句 a.G() 调用的是 B.G，而不是 A.G。这是由于实例的运行时类型（即 B），而不是实例的编译时类型（即 A），决定了要调用的实际方法实现。



因为允许方法隐藏继承的方法，所以一个类可能包含多个具有相同签名的虚方法。这不会产生歧义问题，因为除最派生的方法之外的所有方法都被隐藏。示例中

```csharp
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

C 类和 D 类包含两个具有相同签名的虚方法：一个是由 A 引入的，另一个是由 C 引入的。C 引入的方法隐藏了从 A 继承的方法。因此，D 中的 override 声明重写了 C 引入的方法，并且 D 不可能重写 A 引入的方法。示例的输出为：

B.F
B.F
D.F
D.F

请注意，可以通过使用方法未被隐藏的较少派生类型来访问 D 的实例，从而调用隐藏的虚方法。

## 10.6.4 重写方法

当实例方法声明包含 override 修饰符时，该方法称为重写方法。重写方法重写具有相同签名的继承虚方法。虚方法声明引入一个新方法，而重写方法声明通过提供该方法的新实现来特化已有的继承虚方法。

被重写声明重写的方法称为被重写的基方法。对于在类 C 中声明的重写方法 M，被重写的基方法是通过检查 C 的每个基类类型来确定的，从 C 的直接基类类型开始，继续检查每个后续的直接基类类型，直到在某个基类类型中至少找到一个可访问的方法，该方法在类型参数替换后与 M 具有相同的签名。为了定位被重写的基方法，如果方法是 public、protected、protected internal，或者是 internal 且在与 C 相同的程序中声明，则认为该方法是可访问的。

除非以下所有条件都为重写声明为真，否则会发生编译时错误：

- 可以按照上述描述定位到被重写的基方法。
- 恰好存在一个这样的被重写的基方法。此限制仅在基类类型为构造类型且类型参数的替换使两个方法的签名相同的情况下才生效。
- 被重写的基方法是一个 virtual、abstract 或 override 方法。换句话说，被重写的基方法不能是 static 或非虚的。
- 被重写的基方法不是 sealed 方法。
- 重写方法和被重写的基方法具有相同的返回类型。
- 重写声明和被重写的基方法具有相同的声明可访问性。换句话说，重写声明不能更改虚方法的可访问性。但是，如果被重写的基方法是 protected internal 并且它声明在与包含重写方法的程序集不同的程序集中，则重写方法的声明可访问性必须是 protected。
- 重写声明不指定类型参数约束子句。相反，约束是从被重写的基方法继承的。请注意，被重写方法中的约束的类型参数可能在继承的约束中被类型参数替换。这可能导致在显式指定时不合法的约束，例如值类型或密封类型。

以下示例演示了重写规则如何适用于泛型类：

```csharp
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}
class D : C<string>
{
    public override string F() {...}          // Ok
    public override C<string> G() {...}       // Ok
    public override void H(C<T> x) {...}      // Error, should be C<string>
}
class E<T,U> : C<U>
{
    public override U F() {...}               // Ok
    public override C<U> G() {...}            // Ok
    public override void H(C<T> x) {...}      // Error, should be C<U>
}
```

重写声明可以使用 base-access (§7.6.8) 访问被重写的基方法。示例中

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
    public override void PrintFields() {
        base.PrintFields();
        Console.WriteLine("y = {0}", y);
    }
}
```

B 中的 base.PrintFields() 调用会调用在 A 中声明的 PrintFields 方法。base-access 禁用虚调用机制，并简单地将基方法视为非虚方法。如果 B 中的调用被写成 ((A)this).PrintFields()，它将递归调用在 B 中声明的 PrintFields 方法，而不是在 A 中声明的方法，因为 PrintFields 是虚方法，且 ((A)this) 的运行时类型是 B。

只有包含 override 修饰符，方法才能重写另一个方法。在所有其他情况下，与继承方法具有相同签名的方法只是隐藏继承的方法。示例中

```csharp
class A
{
    public virtual void F() {}
}
class B: A
{
    public virtual void F() {}    // warning, hiding inherited F()
}
```

B 中的 F 方法不包含 override 修饰符，因此不重写 A 中的 F 方法。相反，B 中的 F 方法隐藏了 A 中的方法，并且会报告警告，因为声明中不包含 new 修饰符。

示例中

```csharp
class A
{
    public virtual void F() {}
}
class B: A
{
    new private void F() {}    // Hides A.F within body of B
}
class C: B
{
    public override void F() {}    // Ok, overrides A.F
}
```

B 中的 F 方法隐藏了从 A 继承的虚 F 方法。由于 B 中的 new F 具有 private 访问权限，其作用域仅包括 B 的类体，并不扩展到 C。因此，C 中 F 的声明被允许重写从 A 继承的 F。

## 10.6.5 密封方法

当实例方法声明包含 sealed 修饰符时，该方法称为密封方法。如果实例方法声明包含 sealed 修饰符，它还必须包含 override 修饰符。使用 sealed 修饰符可防止派生类进一步重写该方法。

示例

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

B 类提供了两个重写方法：一个带有 sealed 修饰符的 F 方法和一个不带该修饰符的 G 方法。B 对 sealed 修饰符的使用阻止了 C 进一步重写 F。

## 10.6.6 抽象方法

当实例方法声明包含 abstract 修饰符时，该方法称为抽象方法。虽然抽象方法隐式也是虚方法，但它不能具有 virtual 修饰符。

抽象方法声明引入一个新虚方法，但不提供该方法实现。相反，非抽象派生类必须通过重写该方法来提供自己的实现。由于抽象方法不提供实际实现，抽象方法的方法体仅由一个分号组成。

抽象方法声明仅允许在抽象类中 (§10.1.1.1)。

示例中

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



`Shape` 类定义了可自行绘制的几何形状对象的抽象概念。`Paint` 方法是抽象的，因为没有有意义的默认实现。`Ellipse` 和 `Box` 类是 `Shape` 的具体实现。因为这些类是非抽象的，所以它们必须重写 `Paint` 方法并提供实际的实现。

*基访问* (§7.6.8) 引用抽象方法是一个编译时错误。在示例中

```csharp
abstract class A
{
    public abstract void F();
}

class B: A
{
    public override void F() {
        base.F();        // Error, base.F is abstract
    }
}
```

对 `base.F()` 的调用会报告编译时错误，因为它引用了抽象方法。

抽象方法声明允许重写虚方法。这允许抽象类强制在派生类中重新实现该方法，并使该方法的原始实现不可用。在示例中

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

类 A 声明了一个虚方法，类 B 用抽象方法重写此方法，而类 C 重写抽象方法以提供自己的实现。

## 10.6.7 外部方法

当方法声明包含 `extern` 修饰符时，该方法被称为 *外部方法*。外部方法在外部实现，通常使用 C# 以外的语言。因为外部方法声明不提供实际实现，所以外部方法的 *方法体* 仅由一个分号组成。外部方法不能是泛型的。

`extern` 修饰符通常与 `DllImport` 属性 (§17.5.1) 一起使用，允许外部方法由 DLL（动态链接库）实现。执行环境可能支持其他机制来提供外部方法的实现。

当外部方法包含 `DllImport` 属性时，方法声明还必须包含 `static` 修饰符。此示例演示了 `extern` 修饰符和 `DllImport` 属性的使用：

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
    static extern int GetCurrentDirectory(int bufsize, StringBuilder buf);
    [DllImport("kernel32", SetLastError=true)]
    static extern bool SetCurrentDirectory(string name);
}
```

## 10.6.8 部分方法

当方法声明包含 partial 修饰符时，该方法被称为部分方法。部分方法只能声明为部分类型 (§10.2) 的成员，并且受一系列限制。部分方法在 §10.2.7 中进一步描述。

## 10.6.9 扩展方法

当方法的第一个参数包含 this 修饰符时，该方法被称为扩展方法。扩展方法只能在非泛型、非嵌套的静态类中声明。扩展方法的第一个参数不能有 this 以外的修饰符，并且参数类型不能是指针类型。

下列是一个声明了两个扩展方法的静态类的示例：

```csharp
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

扩展方法是一个常规的静态方法。此外，当其封闭的静态类在作用域内时，扩展方法可以使用实例方法调用语法 (§7.6.5.2) 进行调用，将接收者表达式用作第一个参数。

以下程序使用了上面声明的扩展方法：

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

Slice 方法在 string[] 上可用，ToInt32 方法在 string 上可用，因为它们已被声明为扩展方法。该程序的含义与以下使用普通静态方法调用的情况相同：

```csharp
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

## 10.6.10 方法体

方法声明的 *方法体* 由 *块* 或分号组成。

抽象方法和外部方法声明不提供方法实现，因此它们的方法体仅由分号组成。对于任何其他方法，方法体是一个块 (§8.2)，其中包含在调用该方法时要执行的语句。

当方法的返回类型为 void 时，该方法体中的 return 语句 (§8.9.4) 不允许指定表达式。如果 void 方法的方法体正常完成（即控制流离开方法体的末尾），该方法仅返回给其调用者。

当方法的返回类型不是 void 时，该方法体中的每个 return 语句必须指定一个可隐式转换为返回类型的表达式。值返回方法的方法体的终点必须是不可达的。换句话说，在值返回方法中，不允许控制流离开方法体的末尾。

在示例中

```csharp
class A
{
    public int F() {}       // Error, return value required
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

值返回的 F 方法导致编译时错误，因为控制可以流出方法体的末尾。G 和 H 方法是正确的，因为所有可能的执行路径都以指定返回值的 return 语句结束。

## 10.6.11 方法重载

方法重载解析规则在 §7.5.2 中描述。

## 10.7 属性

*属性* 是提供对对象或类特征访问的成员。属性的示例包括字符串的长度、字体的大小、窗口的标题、客户的名称等等。属性是字段的自然扩展——两者都是具有关联类型的命名成员，并且语法为

访问字段和属性是相同的。然而，与字段不同，属性不表示存储位置。相反，属性具有访问器，指定在读取或写入其值时要执行的语句。因此，属性提供了一种将操作与对象属性的读取和写入关联起来的机制；此外，它们允许计算此类属性。

属性使用 property-declarations 声明：

```
property-declaration:
    attributesopt property-modifiersopt type member-name { accessor-declarations }
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

property-declaration 可能会包含一组属性 (§17) 以及四个访问修饰符 (§10.3.5)、new (§10.3.4)、static (§10.6.2)、virtual (§10.6.3)、override (§10.6.4)、sealed (§10.6.5)、abstract (§10.6.6) 和 extern (§10.6.7) 修饰符的有效组合。

关于修饰符的有效组合，属性声明受与方法声明 (§10.6) 相同的规则约束。

属性声明的类型指定了声明引入的属性的类型，而 member-name 指定了属性的名称。除非属性是显式接口成员实现，否则 member-name 只是标识符。对于显式接口成员实现 (§13.4.1)，member-name 由 interface-type 后跟 '.' 和标识符组成。

属性的类型必须至少与属性本身一样可访问 (§3.5.4)。必须用 '{' 和 '}' 标记括起来的 accessor-declarations 声明属性的访问器 (§10.7.2)。访问器指定与读取和写入属性相关联的可执行语句。尽管访问属性的语法与访问字段的语法相同，但属性不被归类为变量。因此，不可能将属性作为 ref 或 out 参数传递。当属性声明包含 extern 修饰符时，该属性被称为外部属性。因为外部属性声明不提供实际实现，所以其每个 accessor-declarations 都由分号组成。



## 10.7.1 静态属性和实例属性

当属性声明包含 static 修饰符时，该属性称为静态属性。当不存在 static 修饰符时，该属性称为实例属性。

静态属性不与特定实例关联，在静态属性的访问器中引用 this 会导致编译时错误。

实例属性与类的给定实例关联，并且在该属性的访问器中可以通过 this（§7.6.7）访问该实例。

当在形式为 E.M 的成员访问（§7.6.4）中引用属性时，如果 M 是静态属性，则 E 必须表示包含 M 的类型；如果 M 是实例属性，则 E 必须表示包含 M 的类型的实例。

静态成员和实例成员之间的差异将在 §10.3.7 中进一步讨论。

## 10.7.2 访问器

属性的访问器声明指定与读取和写入该属性相关联的可执行语句。

```
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
```

访问器声明由 get 访问器声明、set 访问器声明或两者组成。每个访问器声明由标记 get 或 set 后跟可选的访问器修饰符和访问器体组成。

访问器修饰符的使用受以下限制约束：

- 访问器修饰符不得用于接口或显式接口成员实现中。
- 对于没有 override 修饰符的属性或索引器，仅当该属性或索引器同时具有 get 和 set 访问器时才允许使用访问器修饰符，并且只能用于其中一个访问器。
- 对于包含 override 修饰符的属性或索引器，访问器必须与被重写访问器的访问器修饰符（如果有）匹配。
- 访问器修饰符声明的可访问性必须严格比属性或索引器本身声明的可访问性限制更严格。具体而言：
  - 如果属性或索引器声明的可访问性为 public，则访问器修饰符可以为 protected internal、internal、protected 或 private。
  - 如果属性或索引器声明的可访问性为 `protected internal`，则 *访问器修饰符* 可以为 `internal`、`protected` 或 `private`。
  - 如果属性或索引器声明的可访问性为 `internal` 或 `protected`，则 *访问器修饰符* 必须为 `private`。
  - 如果属性或索引器声明的可访问性为 `private`，则不得使用 *访问器修饰符*。

对于抽象属性和 extern 属性，所指定的每个访问器的 *访问器体* 只是一个分号。非抽象、非 extern 属性可以是 *自动实现的属性*，在这种情况下必须同时提供 get 和 set 访问器，且两者的体均为分号（§10.7.3）。对于任何其他非抽象、非 extern 属性的访问器，*访问器体* 是一个 *块*，它指定在调用相应访问器时要执行的语句。

get 访问器对应于一个无参数方法，其返回值为属性类型。除非作为赋值目标，否则当在表达式中引用属性时，会调用该属性的 get 访问器来计算属性值（§7.1.1）。get 访问器的主体必须符合 §10.6.10 中所述的值返回方法规则。特别是，get 访问器主体中的所有 return 语句都必须指定一个可隐式转换为属性类型的表达式。此外，get 访问器的端点必须不可到达。

set 访问器对应于一个方法，该方法具有一个属性类型的值参数和 void 返回类型。set 访问器的隐式参数始终名为 value。当属性作为赋值目标（§7.17）或作为 ++ 或 -- 的操作数（§7.6.9、§7.7.5）被引用时，会使用一个提供新值的参数（其值为赋值右侧的值或 ++ 或 -- 运算符的操作数）调用 set 访问器（§7.17.1）。set 访问器的主体必须符合 §10.6.10 中所述的 void 方法规则。特别是，set 访问器主体中的 return 语句不得指定表达式。由于 set 访问器隐式具有名为 value 的参数，因此 set 访问器中的局部变量或常量声明使用该名称会导致编译时错误。

根据是否存在 get 和 set 访问器，属性分类如下：

- 同时包含 get 访问器和 set 访问器的属性称为 *读写* 属性。
- 只有 get 访问器的属性称为 *只读* 属性。只读属性作为赋值目标会导致编译时错误。
- 只有 set 访问器的属性称为 *只写* 属性。除非作为赋值目标，否则在表达式中引用只写属性会导致编译时错误。

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
    public override void Paint(Graphics g, Rectangle r) { // Painting code goes here
    }
}
```

Button 控件声明了一个 public 的 Caption 属性。Caption 属性的 get 访问器返回存储在私有 caption 字段中的字符串。set 访问器检查新值是否不同于当前值，如果不同，则存储新值并重新绘制控件。属性通常遵循上面所示的模式：get 访问器仅返回存储在私有字段中的值，set 访问器修改该私有字段，然后执行完全更新对象状态所需的任何附加操作。

给定上面的 Button 类，以下是对 Caption 属性的使用示例：

```
Button okButton = new Button(); // Invokes set accessor
okButton.Caption = "OK"; // Invokes set accessor
string s = okButton.Caption; // Invokes get accessor
```

这里，通过向属性赋值来调用 set 访问器，通过在表达式中引用属性来调用 get 访问器。

属性的 get 和 set 访问器不是不同的成员，并且不可能单独声明属性的访问器。因此，读写属性的两个访问器不可能具有不同的可访问性。示例

```
class A
{
    private string name;
    public string Name {
        get { return name; } // Error, duplicate member name
    }
    public string Name {
        set { name = value; } // Error, duplicate member name
    }
}
```

并未声明单个读写属性。相反，它声明了两个同名属性，一个只读，一个只写。由于在同一类中声明的两个成员不能同名，因此该示例会导致编译时错误。

当派生类声明与继承属性同名的属性时，派生属性在读取和写入两方面都会隐藏继承属性。在示例

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

中，B 中的 P 属性在读取和写入两方面隐藏了 A 中的 P 属性。因此，在以下语句中

```
B b = new B(); // Error, B.P is read-only
((A)b).P = 1; // Ok, reference to A.P
```



对 b.P 的赋值会导致报告编译时错误，因为 B 中的只读属性 P 隐藏了 A 中的只写属性 P。但请注意，可以使用强制转换来访问被隐藏的 P 属性。

与公共字段不同，属性在对象的内部状态与其公共接口之间提供了分离。考虑以下示例：

```
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

这里，Label 类使用两个 int 字段 x 和 y 来存储其位置。该位置同时以 X 和 Y 属性以及 Point 类型的 Location 属性公开。如果未来版本的 Label 在内部以 Point 存储位置更为方便，则可以在不影响该类的公共接口的情况下进行更改：

```
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

如果 x 和 y 是公共只读字段，那么对 Label 类进行这样的更改将是不可能的。

通过属性公开状态未必比直接公开字段效率低。特别是，当属性是非虚拟的且仅包含少量代码时，执行环境可能会将对访问器的调用替换为访问器的实际代码。此过程称为内联，它使属性访问与字段访问一样高效，同时保留了属性更高的灵活性。

由于调用 get 访问器在概念上等同于读取字段的值，因此让 get 访问器具有可观察的副作用被认为是不良编程风格。例如：

```
~~~csharp
class Counter
{
    private int next;
    public int Next {
        get { return next++; }
    }
}
~~~
```

Next 属性的值取决于该属性先前被访问的次数。因此，访问该属性会产生可观察的副作用，并且该属性应改为作为方法实现。

get 访问器的“无副作用”约定并不意味着 get 访问器总是应该简单地返回存储在字段中的值。实际上，get 访问器通常通过访问多个字段或调用方法来计算属性的值。然而，设计良好的 get 访问器不会执行任何导致对象状态发生可观察变化的操作。

属性可用于将资源的初始化延迟到首次引用它的那一刻。例如：

```
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
}
~~~
```

Console 类包含三个属性 In、Out 和 Error，分别表示标准输入、输出和错误设备。通过将这些成员公开为属性，Console 类可以将它们的初始化延迟到实际使用时。例如，在首次引用 Out 属性时，如下所示：

```
Console.Out.WriteLine("hello, world");
```

就会为输出设备创建底层 TextWriter。但如果应用程序不引用 In 和 Error 属性，则不会为这些设备创建任何对象。

## 10.7.3 自动实现的属性

当属性被指定为自动实现的属性时，会自动为该属性提供一个隐藏的后备字段，并且访问器被实现为从该后备字段读取和写入。

以下示例：

```
public class Point {
    public int X { get; set; } // automatically implemented
    public int Y { get; set; } // automatically implemented
}
```

等效于以下声明：

```
public class Point {
    private int x;
    private int y;
    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

由于后备字段不可访问，因此即使在其包含类型内，也只能通过属性访问器对其进行读写。这意味着自动实现的只读或只写属性没有意义，因此是不允许的。然而，可以分别设置每个访问器的访问级别。因此，可以通过以下方式模拟具有私有后备字段的只读属性的效果：

```
public class ReadOnlyPoint {
    public int X { get; private set; }
    public int Y { get; private set; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```

此限制还意味着，带有自动实现属性的结构类型的明确赋值只能通过该结构的标准构造函数来实现，因为对属性本身的赋值要求结构已明确赋值。这意味着用户定义的构造函数必须调用默认构造函数。

## 10.7.4 可访问性

如果访问器具有访问器修饰符，则该访问器的可访问性域（§3.5.2）由访问器修饰符的声明可访问性决定。如果访问器不具有访问器修饰符，则该访问器的可访问性域由属性或索引器的声明可访问性决定。

访问器修饰符的存在绝不会影响成员查找（§7.3）或重载决策（§7.5.3）。属性或索引器上的修饰符始终决定绑定到哪个属性或索引器，而无论访问的上下文如何。

一旦选择了特定的属性或索引器，就会使用所涉及的特定访问器的可访问性域来确定该用法是否有效：
- 如果用作值（§7.1.1），则 get 访问器必须存在且可访问。
- 如果用作简单赋值（§7.17.1）的目标，则 set 访问器必须存在且可访问。
- 如果用作复合赋值（§7.17.2）的目标，或用作 ++ 或 -- 运算符（§7.5.9、§7.6.5）的目标，则 get 访问器和 set 访问器都必须存在且可访问。

在下面的示例中，属性 A.Text 被属性 B.Text 隐藏，即使在仅调用 set 访问器的上下文中也是如此。相比之下，属性 B.Count 对类 M 不可访问，因此使用可访问的属性 A.Count。

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
class B : A
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
        b.Text = "howdy";    // Error, B.Text set accessor not accessible
        string s = b.Text;   // Calls B.Text get accessor
    }
}
```

用于实现接口的访问器可能没有访问器修饰符。如果仅使用一个访问器来实现接口，则另一个访问器可以声明有访问器修饰符：

```csharp
public interface I
{
    string Prop { get; }
}
public class C : I
{
    public string Prop {
        get { return "April"; }    // Must not have a modifier here
        internal set {...}         // Ok, because I.Prop has no set accessor
    }
}
```




## 10.7.5 虚拟、密封、重写和抽象访问器

虚拟属性声明指定该属性的访问器为虚拟。virtual 修饰符适用于读写属性的两个访问器——不可能让读写属性的仅一个访问器为虚拟。

抽象属性声明指定该属性的访问器为虚拟，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写该属性为访问器提供自己的实现。因为抽象属性声明的访问器不提供实际实现，其访问器体仅由一个分号组成。

包含 abstract 和 override 修饰符的属性声明指定该属性为抽象并重写基属性。此类属性的访问器也是抽象的。

抽象属性声明仅允许在抽象类中（§10.1.1.1）。继承的虚拟属性的访问器可以通过包含指定 override 指令的属性声明在派生类中被重写。这被称为 *重写属性声明*。重写属性声明不会声明新的属性。相反，它只是专门化现有虚拟属性的访问器的实现。

重写属性声明必须指定与继承属性完全相同的可访问性修饰符、类型和名称。如果继承的属性只有一个访问器（即继承的属性为只读或只写），则重写属性必须仅包含该访问器。如果继承的属性包含两个访问器（即继承的属性为读写），则重写属性可以包含单个访问器或两个访问器。

重写属性声明可以包含 sealed 修饰符。使用此修饰符可防止派生类进一步重写该属性。密封属性的访问器也是密封的。

除声明和调用语法上的差异外，虚拟、密封、重写和抽象访问器的行为与虚拟、密封、重写和抽象方法完全相同。具体而言，§10.6.3、§10.6.4、§10.6.5 和 §10.6.6 中描述的规则就好像访问器是相应形式的方法一样适用：

- get 访问器对应于一个无参数的方法，其返回值为属性类型，并且与包含该属性的修饰符相同。
- set 访问器对应于一个方法，该方法具有单个属性类型的值参数、void 返回类型，并且与包含该属性的修饰符相同。

在示例

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

X 是一个虚拟只读属性，Y 是一个虚拟读写属性，Z 是一个抽象读写属性。因为 Z 是抽象的，所以包含类 A 也必须声明为抽象。

派生自 A 的类如下所示：

```
class B: A
{
    int z;
    public override int X {
        get { return base.X + 1; }
    }
    public override int Y {
        set { base.Y = value < 0? 0: value; }
    }
    public override int Z {
        get { return z; }
        set { z = value; }
    }
}
```

这里，X、Y 和 Z 的声明是重写属性声明。每个属性声明都与相应继承属性的可访问性修饰符、类型和名称完全匹配。X 的 get 访问器和 Y 的 set 访问器使用 base 关键字访问继承的访问器。Z 的声明重写了两个抽象访问器——因此，B 中没有未决的抽象函数成员，B 允许为非抽象类。

当属性声明为 override 时，任何被重写的访问器必须对重写代码可访问。此外，属性或索引器本身以及访问器的声明可访问性必须与被重写成员和访问器的可访问性匹配。例如：

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

## 10.8 事件

事件是一个成员，使对象或类能够提供通知。客户端可以通过提供事件处理程序为事件附加可执行代码。

事件使用 event-declaration 声明：

```
event-declaration:
    attributes_opt event-modifiers_opt event type variable-declarators ;
    attributes_opt event-modifiers_opt event type member-name { event-accessor-declarations }
```

```
event-modifiers:
    event-modifier
    event-modifiers event-modifier
```

```
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
  add-accessor-declaration remove-accessor-declaration
  remove-accessor-declaration add-accessor-declaration

add-accessor-declaration:
  attributes_opt add block

remove-accessor-declaration:
  attributes_opt remove block
```

event-declaration 可能会包含一组属性（§17）和四个访问修饰符（§10.3.5）、new（§10.3.4）、static（§10.6.2）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符的有效组合。

关于修饰符的有效组合，事件声明受与方法声明（§10.6）相同的规则约束。

事件声明的类型必须是委托类型（§4.2），并且该委托类型必须至少与事件本身一样可访问（§3.5.4）。

事件声明可以包含 event-accessor-declarations。但是，如果没有，对于非 extern、非抽象事件，编译器会自动提供它们（§10.8.1）；对于 extern 事件，访问器由外部提供。

省略 event-accessor-declarations 的事件声明定义一个或多个事件——每个 variable-declarator 一个。此类 event-declaration 声明的成员的所有属性和修饰符都适用。

event-declaration 同时包含 abstract 修饰符和用大括号分隔的 event-accessor-declarations 是编译时错误。

当事件声明包含 extern 修饰符时，该事件称为外部事件。因为外部事件声明不提供实际实现，所以它同时包含 extern 修饰符和 event-accessor-declarations 是错误的。

事件可以用作 += 和 -= 运算符（§7.17.3）的左操作数。这些运算符分别用于将事件处理程序附加到事件或从事件中移除事件处理程序，并且事件的访问修饰符控制允许此类操作发生的上下文。

由于 += 和 -= 是在声明事件的类型之外允许对事件执行的唯一操作，外部代码可以为事件添加和移除处理程序，但不能以任何其他方式获取或修改底层事件处理程序列表。

在形式为 x += y 或 x -= y 的操作中，当 x 是事件并且引用发生在包含 x 声明的类型之外时，操作的结果类型为 void（与具有 x 的类型且值为赋值后 x 的值相反）。此规则禁止外部代码间接检查事件的底层委托。

以下示例展示了如何将事件处理程序附加到 Button 类的实例：

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

这里，LoginDialog 实例构造函数创建了两个 Button 实例并将事件处理程序附加到 Click 事件。

### 10.8.1 类似字段的事件

在包含事件声明的类或结构程序文本内，某些事件可以像字段一样使用。要以这种方式使用，事件必须不是抽象或 extern，并且不得显式包含 event-accessor-declarations。此类事件可以在允许字段的任何上下文中使用。该字段包含一个委托（§15），它引用已添加到事件的事件处理程序列表。如果没有添加事件处理程序，则该字段包含 null。

在示例

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

Click 在 Button 类内用作字段。如示例所示，该字段可以被检查、修改并在委托调用表达式中使用。Button 类中的 OnClick 方法“引发” Click 事件。引发事件的概念与调用事件表示的委托完全等价——因此，没有用于引发事件的特殊语言结构。请注意，委托调用之前有一个检查，以确保委托不为 null。



在 Button 类的声明之外，Click 成员只能用于 += 和 -= 运算符的左侧，例如

```
b.Click += new EventHandler(...);
```

它会把一个委托追加到 Click 事件的调用列表中；而

```
b.Click -= new EventHandler(...);
```

它会从 Click 事件的调用列表中移除一个委托。

编译字段式事件时，编译器会自动创建用于保存委托的存储，并为该事件创建访问器，以便向委托字段添加或移除事件处理程序。为了保证线程安全，添加或移除操作会在持有锁（§8.12）的情况下执行：对于实例事件，该锁位于包含该事件的对象上；对于静态事件，该锁位于类型对象（§7.6.10.6）上。

因此，如下形式的实例事件声明：

```
class X
{
    public event D Ev;
}
```

可编译为与以下代码等效的形式：

```
class X
{
    private D __Ev; // field to hold the delegate
    public event D Ev {
        add {
            lock(this) { __Ev = __Ev + value; }
        }
        remove {
            lock(this) { __Ev = __Ev - value; }
        }
    }
}
```

在类 X 内部，对 Ev 的引用会被编译为改为引用隐藏字段 __Ev。名称“__Ev”是任意的；该隐藏字段可以具有任何名称，也可以完全没有名称。

类似地，如下形式的静态事件声明：

```
class X
{
    public static event D Ev;
}
```

可编译为与以下代码等效的形式：

```
class X
{
    private static D __Ev; // field to hold the delegate
    public static event D Ev {
        add {
            lock(typeof(X)) { __Ev = __Ev + value; }
        }
        remove {
            lock(typeof(X)) { __Ev = __Ev - value; }
        }
    }
}
```

Control 类为事件实现了一种内部存储机制。AddEventHandler 方法将委托值与键关联起来，GetEventHandler 方法返回当前与某个键关联的委托，RemoveEventHandler 方法移除作为指定事件的事件处理程序的委托。据推测，底层存储机制的设计使得将空委托值与键关联不会产生开销，因此未处理的事件不占用存储空间。

## 10.8.3 静态事件和实例事件

当事件声明包含 static 修饰符时，该事件称为静态事件。当不存在 static 修饰符时，该事件称为实例事件。

静态事件不与特定实例关联，并且在静态事件的访问器中引用 this 会导致编译时错误。

实例事件与类的给定实例关联，并且在该事件的访问器中可以通过 this（§7.6.7）访问该实例。

当在 E.M 形式的成员访问（§7.6.4）中引用事件时，如果 M 是静态事件，则 E 必须表示包含 M 的类型；如果 M 是实例事件，则 E 必须表示包含 M 的类型的实例。

静态成员与实例成员之间的差异将在 §10.3.7 中进一步讨论。

## 10.8.4 虚拟、密封、重写和抽象访问器

虚拟事件声明指定该事件的访问器是虚拟的。virtual 修饰符同时适用于事件的两个访问器。

抽象事件声明指定该事件的访问器是虚拟的，但不提供访问器的实际实现。相反，非抽象派生类必须通过重写该事件来为访问器提供自己的实现。由于抽象事件声明不提供实际实现，因此它不能提供用大括号分隔的事件访问器声明。

同时包含 abstract 和 override 修饰符的事件声明指定该事件是抽象的，并且重写一个基事件。此类事件的访问器也是抽象的。

抽象事件声明只允许在抽象类（§10.1.1.1）中。

通过包含指定 override 修饰符的事件声明，可以在派生类中重写继承的虚拟事件的访问器。这称为重写事件声明。重写事件声明不会声明新事件。相反，它只是特化现有虚拟事件的访问器实现。

重写事件声明必须指定与被重写事件完全相同的可访问性修饰符、类型和名称。

重写事件声明可以包含 sealed 修饰符。使用此修饰符可阻止派生类进一步重写该事件。密封事件的访问器也是密封的。

重写事件声明包含 new 修饰符会导致编译时错误。

除声明和调用语法不同外，虚拟、密封、重写和抽象访问器的行为与虚拟、密封、重写和抽象方法完全相同。具体而言，§10.6.3、§10.6.4、§10.6.5 和 §10.6.6 中描述的规则适用，就如同访问器是相应形式的方法一样。每个访问器对应于一个方法，该方法具有一个事件类型的值参数、void 返回类型，以及与包含该事件的事件相同的修饰符。

## 10.9 索引器

索引器是一种成员，它使对象能够像数组一样被索引。索引器使用 indexer-declarations 声明：

## C# 语言规范

```
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
```

indexer-declaration 可以包含一组特性（§17）以及四个访问修饰符（§10.3.5）、new（§10.3.4）、virtual（§10.6.3）、override（§10.6.4）、sealed（§10.6.5）、abstract（§10.6.6）和 extern（§10.6.7）修饰符的有效组合。

在修饰符的有效组合方面，索引器声明遵循与方法声明（§10.6）相同的规则，唯一的例外是索引器声明中不允许使用 static 修饰符。

virtual、override 和 abstract 修饰符互斥，只有一种情况例外。abstract 和 override 修饰符可以一起使用，以便抽象索引器可以重写虚拟索引器。

索引器声明的类型指定该声明所引入索引器的元素类型。除非该索引器是显式接口成员实现，否则该类型后跟关键字 this。对于显式接口成员实现，该类型后跟 interface-type、一个“.”以及关键字 this。与其他成员不同，索引器没有用户定义的名称。

formal-parameter-list 指定索引器的参数。索引器的形参列表对应于方法的形参列表（§10.6.1），不同之处在于必须至少指定一个参数，并且不允许使用 ref 和 out 参数修饰符。

索引器的类型以及 formal-parameter-list 中引用的每个类型，其可访问性必须至少与索引器本身相同（§3.5.4）。

accessor-declarations（§10.7.2）必须括在“{”和“}”标记中，它们声明索引器的访问器。访问器指定与读取和写入索引器元素相关联的可执行语句。

尽管访问索引器元素的语法与访问数组元素的语法相同，但索引器元素不会被归类为变量。因此，不能将索引器元素作为 ref 或 out 参数传递。

索引器和属性在概念上非常相似，但有以下不同之处：

- 属性由其名称标识，而索引器由其签名标识。
- 属性通过 *简单名称*（§7.6.2）或 *成员访问*（§7.6.4）访问，而索引器元素通过 *元素访问*（§7.6.2）访问。
- 属性可以是 `static` 成员，而索引器始终是实例成员。
- 属性的 `get` 访问器对应于没有参数的方法，而索引器的 `get` 访问器对应于与索引器具有相同形参列表的方法。
- 属性的 `set` 访问器对应于一个具有名为 `value` 的单个参数的方法，而索引器的 `set` 访问器对应于一个具有与索引器相同形参列表并额外具有名为 `value` 的参数的方法。
- 如果索引器访问器声明了与索引器参数同名的局部变量，则会导致编译时错误。
- 在重写属性声明中，继承的属性使用语法 `base.P` 访问，其中 P 是属性名。在重写索引器声明中，继承的索引器使用语法 `base[E]` 访问，其中 E 是逗号分隔的表达式列表。

除这些差异外，§10.7.2 和 §10.7.3 中定义的所有规则同样适用于索引器访问器和属性访问器。

当索引器声明包含 extern 修饰符时，该索引器称为外部索引器。由于外部索引器声明不提供实际实现，因此其每个访问器声明都由一个分号组成。

下面的示例声明了一个 BitArray 类，该类实现了一个索引器，用于访问位数组中的各个位。

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
}
```


```
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

BitArray 类的实例比相应的 bool [] 消耗的内存少得多（因为前者的每个值仅占一位，而后者的每个值占一个字节），但它允许与 bool [] 相同的操作。

下面的 CountPrimes 类使用 BitArray 和经典的“筛法”算法来计算 1 到给定最大值之间的素数个数：

```
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

请注意，访问 BitArray 元素的语法与访问 bool [] 的语法完全相同。

下面的示例展示了一个 26 × 10 的网格类，其索引器带有两个参数。第一个参数必须是 A–Z 范围内的大写或小写字母，第二个参数必须是 0–9 范围内的整数。

```
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
```

### 10.9.1 索引器重载

索引器重载解析规则在 §7.5.2 中描述。

## 10.10 运算符

运算符是一种成员，它定义了可应用于类实例的表达式运算符的含义。运算符使用运算符声明（operator-declarations）来声明：

```
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
    type operator overloadable-unary-operator ( type identifier )
overloadable-unary-operator: one of
    +  -  !  ~  ++  --  true  false
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
  right-shift
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
```

可重载运算符分为三类：一元运算符（§10.10.1）、二元运算符（§10.10.2）和转换运算符（§10.10.3）。

当运算符声明包含 extern 修饰符时，该运算符称为外部运算符。由于外部运算符不提供实际实现，其运算符体（operator-body）由一个分号组成。对于所有其他运算符，运算符体由一个块组成，该块指定调用运算符时要执行的语句。运算符的块必须符合 §10.6.10 中描述的返回值方法的规则。

以下规则适用于所有运算符声明：

- 运算符声明必须同时包含 public 和 static 修饰符。
- 运算符的参数必须是值参数。运算符声明指定 ref 或 out 参数会导致编译时错误。
- 运算符的签名（§10.10.1、§10.10.2、§10.10.3）必须与同一类中声明的所有其他运算符的签名不同。
- 运算符声明中引用的所有类型的可访问性必须至少与运算符本身相同（§3.5.4）。
- 同一修饰符在运算符声明中多次出现是错误的。

每个运算符类别还有额外的限制，如以下各节所述。

与其他成员一样，基类中声明的运算符会被派生类继承。由于运算符声明始终要求声明运算符的类或结构体参与运算符的签名，因此派生类中声明的运算符不可能隐藏基类中声明的运算符。因此，在运算符声明中永远不需要 new 修饰符，因此也永远不允许使用。

有关一元运算符和二元运算符的更多信息，请参见 §7.3。

有关转换运算符的更多信息，请参见 §6.4。

### 10.10.1 一元运算符

以下规则适用于一元运算符声明，其中 T 表示包含运算符声明的类或结构体的实例类型：

- 一元 +、-、! 或 ~ 运算符必须接受类型为 T 或 T? 的单个参数，并且可以返回任何类型。
- 一元 ++ 或 -- 运算符必须接受类型为 T 或 T? 的单个参数，并且必须返回相同类型或由其派生的类型。
- 一元 true 或 false 运算符必须接受类型为 T 或 T? 的单个参数，并且必须返回 bool 类型。

一元运算符的签名由运算符标记（+、-、!、~、++、--、true 或 false）和单个形参的类型组成。返回类型不属于一元运算符签名的组成部分，形参的名称也不属于。

true 和 false 一元运算符需要成对声明。如果某个类只声明了其中一个运算符而未同时声明另一个，则会发生编译时错误。true 和 false 运算符将在 §7.12.2 和 §7.20 中进一步描述。

下面的示例演示了整数向量类中 operator ++ 的实现及其后续用法：

```
public class IntVector
{
    public IntVector(int length) {...}
    public int Length {...}    // read-only property
    public int this[int index] {...}    // read-write indexer
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
        IntVector iv1 = new IntVector(4);    // vector of 4 x 0
        IntVector iv2;
        iv2 = iv1++;    // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;    // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

请注意，该运算符方法返回将操作数加 1 后产生的值，就像后缀递增和递减运算符（§7.6.9）以及前缀递增和递减运算符（§7.7.5）一样。与 C++ 不同，此方法不必直接修改其操作数的值。事实上，修改操作数值会违反后缀递增运算符的标准语义。

### 10.10.2 二元运算符

以下规则适用于二元运算符声明，其中 T 表示包含运算符声明的类或结构体的实例类型：

- 二元非移位运算符必须接受两个参数，其中至少一个参数的类型必须为 T 或 T?，并且可以返回任何类型。





- 二元 << 或 >> 运算符必须接受两个参数，其中第一个参数必须具有类型 T 或 T?，第二个参数必须具有类型 int 或 int?，并且可以返回任何类型。

二元运算符的签名由运算符标记（+, -, *, /, %, &, |, ^, <<, >>, ==, !=, >, <, >= 或 <=）和两个形参的类型组成。返回类型和形参的名称不属于二元运算符的签名。

某些二元运算符要求成对声明。对于一对运算符中任一运算符的每个声明，都必须有该对中另一运算符的匹配声明。当两个运算符声明具有相同的返回类型且每个参数的类型相同时，它们匹配。以下运算符要求成对声明：

- operator == 和 operator !=
- operator > 和 operator <
- operator >= 和 operator <=

## 10.10.3 转换运算符

转换运算符声明引入用户定义转换（§6.4），该转换扩充预定义的隐式和显式转换。

包含 implicit 关键字的转换运算符声明引入用户定义的隐式转换。隐式转换可出现在各种情形中，包括函数成员调用、强制转换表达式和赋值。§6.1 对此作了进一步描述。

包含 explicit 关键字的转换运算符声明引入用户定义的显式转换。显式转换可出现在强制转换表达式中，§6.2 对此作了进一步描述。

转换运算符从源类型转换为目标类型，源类型由转换运算符的参数类型指示，目标类型由转换运算符的返回类型指示。

对于给定的源类型 S 和目标类型 T，如果 S 或 T 是可空类型，则让 S0 和 T0 指代它们的基础类型；否则 S0 和 T0 分别等于 S 和 T。仅当以下所有条件都为真时，才允许类或结构声明从源类型 S 到目标类型 T 的转换：

- S0 和 T0 是不同的类型。
- S0 或 T0 是运算符声明所在的类或结构类型。
- S0 和 T0 都不是接口类型。
- 排除用户定义转换后，不存在从 S 到 T 或从 T 到 S 的转换。

就这些规则而言，与 S 或 T 关联的任何类型参数均被视为与其他类型没有继承关系的唯一类型，并且忽略对这些类型参数的任何约束。

在下面的示例中：

```
class C<T> {...}
class D<T> : C<T>
{
    public static implicit operator int(D<T> value) {...}   // Ok
    public static implicit operator string(D<T> value) {...} // Ok
    public static implicit operator T(D<T> value) {...}     // Error
}
```

前两个运算符声明是允许的，因为就 §10.9.3 而言，T 分别与 int 和 string 被视为没有关系的唯一类型。但是，第三个运算符是错误的，因为 C<T> 是 D<T> 的基类。

由第二条规则可知，转换运算符必须转换为声明该运算符的类或结构类型，或从该类型转换。例如，类或结构类型 C 可以定义从 C 到 int 以及从 int 到 C 的转换，但不能定义从 int 到 bool 的转换。

不能直接重新定义预定义转换。因此，不允许转换运算符从 object 转换或转换为 object，因为 object 与所有其他类型之间已经存在隐式和显式转换。同样，转换的源类型和目标类型都不能是对方的基类型，因为那样一来转换就已经存在。

但是，可以在泛型类型上声明这样的运算符：对于特定类型实参，它们指定已经作为预定义转换存在的转换。在下面的示例中：

```csharp
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```

当将类型 object 指定为 T 的类型实参时，第二个运算符声明了一个已经存在的转换（存在从任何类型到类型 object 的隐式转换，因而也存在显式转换）。

当两种类型之间存在预定义转换时，这些类型之间的任何用户定义转换都会被忽略。具体而言：

- 如果存在从类型 S 到类型 T 的预定义隐式转换（§6.1），则从 S 到 T 的所有用户定义转换（隐式或显式）都会被忽略。
- 如果存在从类型 S 到类型 T 的预定义显式转换（§6.2），则从 S 到 T 的任何用户定义显式转换都会被忽略。此外：
  - 如果 T 是接口类型，则从 S 到 T 的用户定义隐式转换会被忽略。
  - 否则，从 S 到 T 的用户定义隐式转换仍会被考虑。

对于除 object 之外的所有类型，上面 Convertible<T> 类型声明的运算符不会与预定义转换冲突。例如：

```csharp
void F(int i, Convertible<int> n) {
    i = n;                     // Error
    i = (int)n;                // User-defined explicit conversion
    n = i;                     // User-defined implicit conversion
    n = (Convertible<int>)i;   // User-defined implicit conversion
}
```

但是，对于类型 object，预定义转换在除一种情况外的所有情况下都会隐藏用户定义转换：

```csharp
void F(object o, Convertible<object> n) {
    o = n;                     // Pre-defined boxing conversion
    o = (object)n;             // Pre-defined boxing conversion
    n = o;                     // User-defined implicit conversion
    n = (Convertible<object>)o; // Pre-defined unboxing conversion
}
```

不允许用户定义转换从接口类型转换或转换为接口类型。特别地，此限制确保在转换为接口类型时不会发生用户定义的变换，并且仅当被转换的对象实际实现指定的接口类型时，到接口类型的转换才会成功。

转换运算符的签名由源类型和目标类型组成。（请注意，这是返回类型参与签名的唯一成员形式。）转换运算符的隐式或显式分类不属于该运算符的签名。因此，类或结构不能同时声明具有相同源类型和目标类型的隐式转换运算符和显式转换运算符。

通常，用户定义的隐式转换应设计为从不引发异常，也从不丢失信息。如果用户定义转换可能引发异常（例如，因为源实参超出范围）或丢失信息（例如丢弃高位），则该转换应定义为显式转换。

在下面的示例中：

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

从 Digit 到 byte 的转换是隐式的，因为它从不引发异常或丢失信息；但从 byte 到 Digit 的转换是显式的，因为 Digit 只能表示 byte 可能值的一个子集。

## 10.11 实例构造函数

实例构造函数是实现初始化类实例所需操作的成员。实例构造函数通过构造函数声明来声明：

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
```


```csharp
constructor-body:
    block
    ;
```

构造函数声明可以包含一组特性（§17）、四种访问修饰符（§10.3.5）的有效组合，以及 extern（§10.6.7）修饰符。构造函数声明不允许多次包含相同的修饰符。

构造函数声明符的标识符必须命名声明该实例构造函数的类。如果指定了其他名称，则会发生编译时错误。

实例构造函数的可选形式参数列表须遵守与方法（§10.6）的形式参数列表相同的规则。形式参数列表定义了实例构造函数的签名（§3.6），并控制重载解析（§7.5.2）在调用中选择特定实例构造函数的过程。

实例构造函数形式参数列表中引用的每种类型必须至少与构造函数本身一样可访问（§3.5.4）。

可选的构造函数初始化器指定在执行此实例构造函数的构造函数体中给出的语句之前要调用的另一个实例构造函数。详情请参见§10.11.1。

当构造函数声明包含 extern 修饰符时，该构造函数被称为外部构造函数。由于外部构造函数声明不提供实际实现，其构造函数体由一个分号组成。对于所有其他构造函数，构造函数体由一个块组成，该块指定初始化类的新实例的语句。这与返回类型为 void 的实例方法（§10.6.10）的块完全对应。

实例构造函数不会被继承。因此，类没有除在类中实际声明的实例构造函数之外的其他实例构造函数。如果类不包含实例构造函数声明，则会自动提供默认实例构造函数（§10.11.4）。

实例构造函数由对象创建表达式（§7.6.10.1）和通过构造函数初始化器调用。

### 10.11.1 构造函数初始化器

除 object 类之外的所有实例构造函数都在构造函数体之前隐式包含对另一个实例构造函数的调用。要隐式调用的构造函数由构造函数初始化器确定：

- 形式为 `base(argument-list_opt)` 的实例构造函数初始化器会导致直接基类的实例构造函数被调用。该构造函数使用 `argument-list` 和 §7.5.3 的重载解析规则进行选择。候选实例构造函数的集合由直接基类中包含的所有可访问实例构造函数组成，或者如果直接基类中未声明实例构造函数，则为默认构造函数（§10.11.4）。如果该集合为空，或者无法识别出唯一的最佳实例构造函数，则会发生编译时错误。
- 形式为 `this(argument-list_opt)` 的实例构造函数初始化器会导致类本身的实例构造函数被调用。该构造函数使用 `argument-list` 和 §7.5.3 的重载解析规则进行选择。候选实例构造函数的集合由类本身声明的所有可访问实例构造函数组成。如果该集合为空，或者无法识别出唯一的最佳实例构造函数，则会发生编译时错误。如果实例构造函数声明包含调用自身构造函数的构造函数初始化器，则会发生编译时错误。

如果实例构造函数没有构造函数初始化器，则会隐式提供形式为 `base()` 的构造函数初始化器。因此，形式为

```csharp
C(...) {...}
```

与

```csharp
C(...): base() {...}
```

完全等价

实例构造函数声明的形式参数列表给出的参数的作用域包括该声明的构造函数初始化器。因此，构造函数初始化器可以访问构造函数的参数。例如：

```csharp
class A
{
    public A(int x, int y) {}
}
class B: A
{
    public B(int x, int y): base(x + y, x - y) {}
}
```

实例构造函数初始化器无法访问正在创建的实例。因此，在构造函数初始化器的参数表达式中引用 `this` 是编译时错误，参数表达式通过简单名称引用任何实例成员也是编译时错误。

### 10.11.2 实例变量初始化器

当实例构造函数没有构造函数初始化器，或其构造函数初始化器形式为 `base(...)` 时，该构造函数会隐式执行其类中声明的实例字段的变量初始化器指定的初始化。这对应于一系列赋值，在进入构造函数后立即执行，并在隐式调用直接基类构造函数之前执行。变量初始化器按其在类声明中出现的文本顺序执行。

### 10.11.3 构造函数执行

变量初始化器被转换为赋值语句，并且这些赋值语句在调用基类实例构造函数之前执行。此顺序确保在执行任何可以访问该实例的语句之前，所有实例字段都已由其变量初始化器初始化。

给出示例

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

当使用 `new B()` 创建 B 的实例时，会产生以下输出：

```csharp
x = 1, y = 0
```

x 的值为 1，因为变量初始化器在调用基类实例构造函数之前执行。然而，y 的值为 0（int 的默认值），因为对 y 的赋值要等到基类构造函数返回后才执行。

将实例变量初始化器和构造函数初始化器视为在构造函数体之前自动插入的语句是有用的。示例

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

包含多个变量初始化器；它还包含两种形式的构造函数初始化器（base 和 this）。该示例对应于下面显示的代码，其中每个注释都指示一个自动插入的语句（用于自动插入的构造函数调用的语法无效，但仅用于说明机制）

```csharp
using System.Collections;

class A
{
    int x, y, count;
    public A() {
        x = 1;                // variable initializer
        y = -1;               // variable initializer
        object();             // Invoke object() constructor
        count = 0;
    }
    public A(int n) {
        x = 1;                // variable initializer
        y = -1;               // variable initializer
        object();             // Invoke object() constructor
        count = n;
    }
}

class B: A
{
    double sqrt2;
    ArrayList items;
    int max;
    public B(): this(100) {
        B(100);               // Invoke B(int) constructor
        items.Add("default");
    }
    public B(int n): base(n - 1) {
        sqrt2 = Math.Sqrt(2.0);    // variable initializer
        items = new ArrayList(100); // variable initializer
        A(n - 1);                 // Invoke A(int) constructor
        max = n;
    }
}
```

### 10.11.4 默认构造函数

如果类不包含实例构造函数声明，则会自动提供默认实例构造函数。该默认构造函数仅调用直接基类的无参数构造函数。如果直接基类没有可访问的无参数实例构造函数，则会发生编译时错误。如果类是抽象的，则默认构造函数的声明可访问性为 protected。否则，默认构造函数的声明可访问性为 public。因此，默认构造函数始终具有以下形式

```csharp
protected C(): base() {}
```

或

```csharp
public C(): base() {}
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

由于类不包含实例构造函数声明，因此提供了默认构造函数。因此，该示例与以下内容完全等价

```csharp
class Message
{
    object sender;
    string text;
    public Message(): base() {}
}
```

### 10.11.5 私有构造函数

当类 T 仅声明私有实例构造函数时，T 的程序文本之外的类无法从 T 派生，也无法直接创建 T 的实例。因此，如果类仅包含静态成员且不打算实例化，则添加一个空的私有实例构造函数将阻止实例化。例如：

```csharp
public class Trig
{
    private Trig() {}    // Prevent instantiation
    public const double PI = 3.14159265358979323846;
}
```



```java
public static double sin(double x) {...}
public static double cos(double x) {...}
public static double tan(double x) {...}
}
```

Trig 类将相关方法和常量分组，但并不打算被实例化。因此它声明了一个单一的空私有实例构造函数。必须声明至少一个实例构造函数以抑制默认构造函数的自动生成。

## 10.11.6 可选实例构造函数参数

`this(...)` 形式的构造函数初始化器通常与重载结合使用以实现可选实例构造函数参数。在示例中

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

前两个实例构造函数仅为缺失的参数提供默认值。两者都使用 `this(...)` 构造函数初始化器来调用第三个实例构造函数，后者实际执行初始化新实例的工作。其效果等同于可选的构造函数参数：

```csharp
Text t1 = new Text();                 // Same as Text(0, 0, null)
Text t2 = new Text(5, 10);            // Same as Text(5, 10, null)
Text t3 = new Text(5, 20, "Hello");
```

## 10.12 静态构造函数

一个 *静态构造函数* 是实现初始化封闭类类型所需操作的成员。静态构造函数使用 *静态构造函数声明* 声明：

```
static-constructor-declaration:
    attributes_opt  static-constructor-modifiers  identifier  (  )  static-constructor-body

static-constructor-modifiers:
    extern_opt  static
    static  extern_opt

static-constructor-body:
    block
    ;
```

一个 *静态构造函数声明* 可能会包含一组 *属性*（§17）和一个 `extern` 修饰符（§10.6.7）。

*静态构造函数声明* 的 *标识符* 必须命名声明静态构造函数的类。如果指定了其他名称，则会发生编译时错误。

当静态构造函数声明包含 `extern` 修饰符时，该静态构造函数被称为 *外部静态构造函数*。由于外部静态构造函数声明不提供实际实现，其 *静态构造函数体* 由分号组成。对于所有其他静态构造函数声明，*静态构造函数体* 由一个 *块* 组成，该块指定为初始化类而执行的语句。这正好对应于返回类型为 `void` 的静态方法的 *方法体*（§10.6.10）。

静态构造函数不被继承，也不能直接调用。

C# 语言规范

封闭类类型的静态构造函数在一个应用程序域中最多执行一次。静态构造函数的执行由应用程序域内首先发生的以下事件触发：

- 创建了该类类型的实例。
- 引用了该类类型的任何静态成员。

如果一个类包含执行开始的 Main 方法（§3.1），则该类的静态构造函数在调用 Main 方法之前执行。

要初始化一个新的封闭类类型，首先为该特定封闭类型创建一个新的静态字段（§10.5.1）集合。每个静态字段都初始化为其默认值（§5.2）。接下来，为这些静态字段执行静态字段初始值设定项（§10.4.5.1）。最后，执行静态构造函数。

示例

```csharp
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

因为对 A.F 的调用触发了 A 的静态构造函数的执行，而对 B.F 的调用触发了 B 的静态构造函数的执行。

可以构造循环依赖，使得具有变量初始值设定项的静态字段在其默认值状态下被观察到。

示例

```csharp
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
    static B() {}
    static void Main() {
        Console.WriteLine("X = {0}, Y = {1}", A.X, B.Y);
    }
}
```

产生输出

X = 1, Y = 2

为执行 Main 方法，系统首先在类 B 的静态构造函数之前运行 B.Y 的初始值设定项。Y 的初始值设定项导致 A 的静态构造函数运行，因为引用了 A.X 的值。A 的静态构造函数随后继续计算 X 的值，在此过程中获取 Y 的默认值，即零。因此 A.X 被初始化为 1。运行 A 的静态字段初始值设定项和静态构造函数的过程随后完成，返回到计算 Y 的初始值的计算，其结果变为 2。

因为静态构造函数对于每个封闭构造类类型只执行一次，所以它是一个方便的位置，用于强制执行在编译时无法通过约束（§10.1.5）检查的类型参数的运行时检查。例如，以下类型使用静态构造函数来强制类型参数为枚举：

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

## 10.13 析构函数

析构函数是实现销毁类实例所需操作的成员。析构函数使用 destructor-declaration 声明：

```
destructor-declaration:
    attributes_opt extern_opt ~ identifier ( ) destructor-body
destructor-body:
    block
    ;
```

destructor-declaration 可能会包含一组属性（§17）。

destructor-declaration 的标识符必须命名声明析构函数的类。如果指定了其他名称，则会发生编译时错误。

当析构函数声明包含 extern 修饰符时，该析构函数被称为外部析构函数。由于外部析构函数声明不提供实际实现，其 destructor-body 由分号组成。对于所有其他析构函数，destructor-body 由一个块组成，该块指定为销毁类实例而执行的语句。destructor-body 正好对应于返回类型为 void 的实例方法的方法体（§10.6.10）。

析构函数不被继承。因此，一个类没有除其自身可能声明的析构函数之外的析构函数。

由于析构函数要求没有参数，因此它不能被重载，所以一个类最多只能有一个析构函数。

析构函数会自动调用，不能显式调用。当不再可能有任何代码使用该实例时，实例变得有资格被销毁。实例的析构函数的执行可能在实例变得有资格被销毁之后任何时间发生。当实例被销毁时，该实例继承链中的析构函数按从最派生到最不派生的顺序调用。析构函数可能在任何线程上执行。有关何时以及如何执行析构函数的规则的进一步讨论，请参阅 §3.9。

示例的输出

```csharp
using System;
class A
{
    ~A() {
        Console.WriteLine("A's destructor");
    }
}
class B: A
{
    ~B() {
        Console.WriteLine("B's destructor");
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

是

```
B's destructor
A's destructor
```

因为继承链中的析构函数按从最派生到最不派生的顺序调用。

析构函数通过覆盖 System.Object 上的虚方法 Finalize 来实现。C# 程序不允许覆盖此方法或直接调用它（或其重写）。例如，程序

```csharp
class A
{
    override protected void Finalize() {} // error
    public void F() {
        this.Finalize();
    } // error
}
```

```csharp
class A
{
    void Finalize() {}                // permitted
}
```

是有效的，并且所示方法隐藏了 System.Object 的 Finalize 方法。

有关析构函数中抛出异常时的行为的讨论，请参阅 §16.3。

## 10.14 迭代器

使用迭代器块 (§8.2) 实现的函数成员 (§7.5) 称为 *iterator*。

迭代器块可以用作函数成员的主体，只要相应函数成员的返回类型是枚举器接口 (§10.14.1) 之一或可枚举接口 (§10.14.2) 之一。它可以作为 *method-body*、*operator-body* 或 *accessor-body* 出现，而事件、实例构造函数、静态构造函数和析构函数不能实现为迭代器。

当函数成员使用迭代器块实现时，如果函数成员的形式参数列表指定了任何 ref 或 out 参数，则为编译时错误。

### 10.14.1 枚举器接口

*enumerator interfaces* 是非泛型接口 `System.Collections.IEnumerator` 以及泛型接口 `System.Collections.Generic.IEnumerator<T>` 的所有实例化。为简洁起见，本章中这些接口分别简称为 `IEnumerator` 和 `IEnumerator<T>`。

### 10.14.2 可枚举接口

*enumerable interfaces* 是非泛型接口 `System.Collections.IEnumerable` 以及泛型接口 `System.Collections.Generic.IEnumerable<T>` 的所有实例化。为简洁起见，本章中这些接口分别简称为 `IEnumerable` 和 `IEnumerable<T>`。

### 10.14.3 产出类型

迭代器产生一系列值，所有值类型相同。该类型称为迭代器的 *yield type*。

- 返回 `IEnumerator` 或 `IEnumerable` 的迭代器的产出类型为 `object`。
- 返回 `IEnumerator<T>` 或 `IEnumerable<T>` 的迭代器的产出类型为 `T`。

### 10.14.4 枚举器对象

当返回枚举器接口类型的函数成员使用迭代器块实现时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建一个 *enumerator object* 并返回。该对象封装了迭代器块中指定的代码，并且迭代器块中的代码执行发生在枚举器对象的 `MoveNext` 方法被调用时。

枚举器对象具有以下特征：

- 它实现了 `IEnumerator` 和 `IEnumerator<T>`，其中 `T` 是迭代器的产出类型。
- 它实现了 `System.IDisposable`。
- 它使用传递给函数成员的参数值（如果有）和实例值的副本进行初始化。
- 它有四个可能的状态，*before*、*running*、*suspended* 和 *after*，并且初始状态为 *before*。

枚举器对象通常是编译器生成的枚举器类的实例，该类封装了迭代器块中的代码并实现了枚举器接口，但也可能有其他实现方法。如果枚举器类由编译器生成，则该类将直接或间接嵌套在
包含函数成员的类中，它将具有私有访问权限，并且其名称保留供编译器使用 (§2.4.2)。

枚举器对象可能实现比上述指定的更多接口。

以下各节描述了枚举器对象提供的 IEnumerable 和 IEnumerable<T> 接口实现中 MoveNext、Current 和 Dispose 成员的确切行为。

请注意，枚举器对象不支持 IEnumerator.Reset 方法。调用此方法会导致抛出 System.NotSupportedException。

### 10.14.4.1 MoveNext 方法

枚举器对象的 MoveNext 方法封装了迭代器块的代码。调用 MoveNext 方法会执行迭代器块中的代码并相应地设置枚举器对象的 Current 属性。MoveNext 执行的确切操作取决于调用 MoveNext 时枚举器对象的状态：

- 如果枚举器对象的状态为 before，调用 MoveNext：
  - 将状态更改为 running。
  - 将迭代器块的参数（包括 this）初始化为枚举器对象初始化时保存的参数值和实例值。
  - 从开头执行迭代器块，直到执行被中断（如下面所述）。
- 如果枚举器对象的状态为 running，调用 MoveNext 的结果是不确定的。
- 如果枚举器对象的状态为 suspended，调用 MoveNext：
  - 将状态更改为 running。
  - 将所有局部变量和参数（包括 this）的值恢复为上次暂停迭代器块执行时保存的值。请注意，这些变量引用的任何对象的内容可能自上次调用 MoveNext 以来已发生变化。
  - 从导致执行暂停的 yield return 语句之后立即恢复迭代器块的执行，并继续执行直到执行被中断（如下面所述）。
- 如果枚举器对象的状态为 after，调用 MoveNext 返回 false。

当 MoveNext 执行迭代器块时，执行可能以四种方式被中断：通过 yield return 语句，通过 yield break 语句，通过遇到迭代器块的末尾，以及通过异常被抛出并从迭代器块中传播。

- 当遇到 yield return 语句 (§8.14) 时：
  - 语句中给出的表达式被求值，隐式转换为产出类型，并赋给枚举器对象的 Current 属性。
  - 迭代器体的执行被挂起。所有局部变量和参数（包括 this）的值被保存，yield return 语句的位置也被保存。如果 yield return 语句位于一个或多个 try 块内，则相关的 finally 块此时不会执行。
  - 枚举器对象的状态更改为 suspended。
  - MoveNext 方法向其调用者返回 true，表示迭代成功推进到下一个值。
- 当遇到 yield break 语句 (§8.14) 时：
  - 如果 `yield break` 语句位于一个或多个 `try` 块内，则相关的 `finally` 块将被执行。
  - 枚举器对象的状态更改为 *after*。
  - `MoveNext` 方法向其调用者返回 `false`，表示迭代已完成。
- 当遇到迭代器体的末尾时：
  - 枚举器对象的状态更改为 *after*。
  - `MoveNext` 方法向其调用者返回 `false`，表示迭代已完成。
- 当异常被抛出并从迭代器块中传播时：
  - 异常传播将已执行迭代器体中的适当 `finally` 块。
  - 枚举器对象的状态更改为 *after*。
  - 异常传播继续到 `MoveNext` 方法的调用者。

### 10.14.4.2 Current 属性

枚举器对象的 `Current` 属性受迭代器块中 `yield return` 语句的影响。

当枚举器对象处于 *suspended* 状态时，`Current` 的值是上一次调用 `MoveNext` 时设置的值。当枚举器对象处于 *before*、*running* 或 *after* 状态时，访问 `Current` 的结果是不确定的。

对于产出类型不是 `object` 的迭代器，通过枚举器对象的 `IEnumerable` 实现访问 `Current` 的结果对应于通过枚举器对象的 `IEnumerator<T>` 实现访问 `Current` 并将结果强制转换为 `object`。

### 10.14.4.3 Dispose 方法

`Dispose` 方法用于通过将枚举器对象带到 *after* 状态来清理迭代。

- 如果枚举器对象的状态为 *before*，调用 `Dispose` 将状态更改为 *after*。
- 如果枚举器对象的状态为 *running*，调用 `Dispose` 的结果是不确定的。
- 如果枚举器对象的状态为 *suspended*，调用 `Dispose`：
  - 将状态更改为 *running*。
  - 执行任何 finally 块，就好像最后执行的 `yield return` 语句是 `yield break` 语句一样。如果这导致异常被抛出并从迭代器体中传播，则枚举器对象的状态设置为 *after*，并且异常传播到 `Dispose` 方法的调用者。
  - 将状态更改为 *after*。
- 如果枚举器对象的状态为 *after*，调用 `Dispose` 没有影响。

### 10.14.5 可枚举对象

当返回可枚举接口类型的函数成员使用迭代器块实现时，调用该函数成员不会立即执行迭代器块中的代码。相反，会创建一个 *enumerable object* 并返回。可枚举对象的 `GetEnumerator` 方法返回一个封装了迭代器块中指定代码的枚举器对象，并且迭代器块中的代码执行发生在枚举器对象的 `MoveNext` 方法被调用时。可枚举对象具有以下特征：

-   它实现了 `IEnumerable` 和 `IEnumerable<T>`，其中 `T` 是迭代器的 yield 类型。
-   它使用参数值（如果有）的副本以及传递给函数成员的实例值进行初始化。

可枚举对象通常是编译器生成的可枚举类的实例，该类封装了迭代器块中的代码并实现了可枚举接口，但也存在其他实现方法。如果可枚举类由编译器生成，则该类将直接或间接嵌套在包含函数成员的类中，它将具有私有访问权限，并且其名称将保留供编译器使用（§2.4.2）。

可枚举对象可能实现比上述指定的更多接口。特别是，可枚举对象还可能实现 `IEnumerator` 和 `IEnumerator<T>`，使其既可作为可枚举对象又可作为枚举器。在这种类型的实现中，可枚举对象的 `GetEnumerator` 方法首次被调用时，返回可枚举对象本身。随后对可枚举对象的 `GetEnumerator` 的调用（如有）将返回可枚举对象的副本。因此，每个返回的枚举器都有自己的状态，一个枚举器的更改不会影响另一个。

### 10.14.5.1 GetEnumerator 方法

可枚举对象提供了 `IEnumerable` 和 `IEnumerable<T>` 接口的 `GetEnumerator` 方法的实现。两个 `GetEnumerator` 方法共享一个公共实现，该实现获取并返回一个可用的枚举器对象。枚举器对象使用在可枚举对象初始化时保存的参数值和实例值进行初始化，但除此之外，枚举器对象按 §10.14.4 中所述运行。

### 10.14.6 实现示例

本节描述了使用标准 C# 结构实现迭代器的一种可能方法。此处描述的实现基于 Microsoft C# 编译器使用的相同原理，但它绝不是强制性的实现，也不是唯一可能的实现。

以下 `Stack<T>` 类使用迭代器实现其 `GetEnumerator` 方法。迭代器按从栈顶到底的顺序枚举栈中的元素。

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

class Stack<T>: IEnumerable<T>
{
    T[] items;
    int count;

    public void Push(T item) {
        if (items == null) {
            items = new T[4];
        }
        else if (items.Length == count) {
            T[] newItems = new T[count * 2];
            Array.Copy(items, 0, newItems, 0, count);
            items = newItems;
        }
        items[count++] = item;
    }

    public T Pop() {
        T result = items[--count];
        items[count] = default(T);
        return result;
    }

    public IEnumerator<T> GetEnumerator() {
        for (int i = count - 1; i >= 0; --i) yield return items[i];
    }
}
```

GetEnumerator 方法可以被翻译为编译器生成的枚举器类的实例化，该类封装了迭代器块中的代码，如下所示。

```csharp
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
}
```

在前面的转换中，迭代器块中的代码被转换为状态机并放置在枚举器类的 MoveNext 方法中。此外，局部变量 i 被转换为枚举器对象中的字段，以便它可以在 MoveNext 的多次调用之间继续存在。

以下示例打印 1 到 10 的整数的简单乘法表。示例中的 FromTo 方法返回一个可枚举对象，并使用迭代器实现。

```csharp
using System;
using System.Collections.Generic;
class Test
{
    static IEnumerable<int> FromTo(int from, int to) {
        while (from <= to) yield return from++;
    }

    static void Main() {
        IEnumerable<int> e = FromTo(1, 10);
        foreach (int x in e) {
            foreach (int y in e) {
                Console.Write("{0,3} ", x * y);
            }
            Console.WriteLine();
        }
    }
}
```

FromTo 方法可以被翻译为编译器生成的可枚举类的实例化，该类封装了迭代器块中的代码，如下所示。

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
}
```

可枚举类同时实现了可枚举接口和枚举器接口，使其既可作为可枚举对象又可作为枚举器。首次调用 GetEnumerator 方法时，返回可枚举对象本身。随后对可枚举对象的 GetEnumerator 的调用（如有）将返回可枚举对象的副本。因此，每个返回的枚举器都有自己的状态，一个枚举器的更改不会影响另一个。Interlocked.CompareExchange 方法用于确保线程安全操作。

from 和 to 参数被转换为可枚举类中的字段。由于 from 在迭代器块中被修改，因此引入了额外的 __from 字段来保存为每个枚举器提供的 from 的初始值。

如果在 __state 为 0 时调用 MoveNext 方法，则会抛出 InvalidOperationException。这可防止在未先调用 GetEnumerator 的情况下将可枚举对象用作枚举器对象。

以下示例展示了一个简单的树类。Tree<T> 类使用迭代器实现其 GetEnumerator 方法。迭代器以中缀顺序枚举树中的元素。

```csharp
using System;
using System.Collections.Generic;
class Tree<T>: IEnumerable<T>
{
    T value;
    Tree<T> left;
    Tree<T> right;
    public Tree(T value, Tree<T> left, Tree<T> right) {
        this.value = value;
        this.left = left;
        this.right = right;
    }
```



```csharp
public IEnumerator<T> GetEnumerator() {
    if (left != null) foreach (T x in left) yield x;
    yield value;
    if (right != null) foreach (T x in right) yield x;
}
}
class Program
{
    static Tree<T> MakeTree<T>(T[] items, int left, int right) {
        if (left > right) return null;
        int i = (left + right) / 2;
        return new Tree<T>(items[i]);
        MakeTree(items, left, i - 1);
        MakeTree(items, i + 1, right);
    }

    static Tree<T> MakeTree<T>(params T[] items) {
        return MakeTree(items, 0, items.Length - 1);
    }

    // The output of the program is:
    // 1 2 3 4 5 6 7 8 9
    // Mon Tue Wed Thu Fri Sat Sun
    static void Main() {
        Tree<int> ints = MakeTree(1, 2, 3, 4, 5, 6, 7, 8, 9);
        foreach (int i in ints) Console.Write("{0} ", i);
        Console.WriteLine();
        Tree<string> strings = MakeTree(
            "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun");
        foreach (string s in strings) Console.Write("{0} ", s);
        Console.WriteLine();
    }
}
```

GetEnumerator 方法可以被翻译成一个编译器生成的枚举器类的实例化，该类封装了迭代器块中的代码，如下所示。

```csharp
class Tree<T>: IEnumerable<T>
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
    }
}
```

```csharp
public bool MoveNext() {
    try {
        switch (__state) {
            case 0:
                __state = -1;
                if (__this.left == null) goto __yield_value;
                __left = __this.left.GetEnumerator();
                goto case 1;
            case 1:
                __state = -2;
                if (!__left.MoveNext()) goto __left_dispose;
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
            case 2:
                __left.Dispose();
                break;
            case 3:
            case -3:
                __right.Dispose();
                break;
        }
    }
}
```

```csharp
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

在 foreach 语句中使用的编译器生成的临时变量被提升到枚举器对象的 __left 和 __right 字段中。枚举器对象的 __state 字段会被仔细更新，以确保在抛出异常时能正确调用正确的 Dispose() 方法。注意，不可能用简单的 foreach 语句编写翻译后的代码。

## 11. 结构体

结构体与类相似，因为它们表示可包含数据成员和函数成员的数据结构。然而，与类不同，结构体是值类型且不需要堆分配。结构体类型变量直接包含结构体的数据，而类类型变量包含对数据的引用，后者称为对象。

结构体对于具有值语义的小型数据结构特别有用。复数、坐标系中的点或字典中的键值对都是结构体的良好示例。这些数据结构的关键在于它们数据成员较少，不需要使用继承或引用标识，并且可以方便地使用值语义实现，其中赋值复制值而不是引用。

如 §4.1.4所述，C# 提供的简单类型，如 int、double 和 bool，实际上都是结构体类型。就像这些预定义类型是结构体一样，也可以使用结构体和运算符重载在 C# 语言中实现新的“原始”类型。本章末尾 (§11.4) 给出了此类类型的两个示例。

### 11.1 结构体声明

struct-declaration 是 type-declaration (§9.6)，它声明一个新的结构体：

```
struct-declaration:
    attributesopt struct-modifiersopt partialopt struct identifier type-parameter-listopt
    struct-interfacesopt type-parameter-constraints-clausesopt struct-body ;opt
```

struct-declaration 由一组可选的属性 (§17) 组成，其后是可选的一组 struct-modifiers (§11.1.1)，其后是可选的 partial 修饰符，其后是关键字 struct 和标识结构体名称的标识符，其后是可选的 type-parameter-list 规范 (§10.1.3)，其后是可选的 struct-interfaces 规范 (§11.1.2 )，其后是可选的 type-parameters-constraints-clauses 规范 (§10.1.5)，其后是 struct-body (§11.1.4)，可选地后跟一个分号。

#### 11.1.1 结构体修饰符

struct-declaration 可选择性地包含一系列结构体修饰符：

```
struct-modifiers:
    struct-modifier
    struct-modifier struct-modifier

struct-modifier:
    new
    public
    protected
    internal
    private
```

在结构体声明中，同一个修饰符出现多次是编译时错误。

结构体声明的修饰符与类声明 (§10.1) 的修饰符含义相同。

#### 11.1.2 Partial 修饰符

partial 修饰符表示此 struct-declaration 是一个部分类型声明。封闭命名空间或类型声明中具有相同名称的多个部分结构体声明会合并形成一个结构体声明，遵循 §10.2 中指定的规则。

#### 11.1.3 结构体接口

结构体声明可以包含 struct-interfaces 规范，在这种情况下，结构体被认为直接实现了给定的接口类型。

```
struct-interfaces:
    : interface-type-list
```

接口实现在 §13.4 中进一步讨论。

#### 11.1.4 结构体体

结构体的 struct-body 定义了结构体的成员。

```
struct-body:
    { struct-member-declarationsopt }
```

### 11.2 结构体成员

结构体的成员由其 struct-member-declarations 引入的成员以及从类型 System.ValueType 继承的成员组成。

```
struct-member-declarations:
    struct-member-declaration
    struct-member-declarations struct-member-declaration
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

除 §11.3 中所述的差异外，§10.3 至 §10.14 中提供的类成员描述同样适用于结构体成员。

### 11.3 类与结构体的差异

结构体与类在几个重要方面有所不同：

- 结构体是值类型 (§11.3.1)。
- 所有结构体类型都隐式继承自类 System.ValueType (§11.3.2)。
- 将值赋给结构体类型变量会创建被赋值的副本 (§11.3.3)。
- 结构体的默认值是通过将所有值类型字段设置为其默认值并将所有引用类型字段设置为 null 而产生的 (§11.3.4)。
- 装箱和拆箱操作用于在结构体类型和 object 之间转换 (§11.3.5)。



-   这对于结构体 (§7.6.7) 的含义不同。
-   结构体的实例字段声明不允许包含变量初始值设定项 (§11.3.7)。
-   结构体不允许声明无参数的实例构造函数 (§11.3.8)。
-   结构体不允许声明析构函数 (§11.3.9)。

## 11.3.1 值语义

结构体是值类型 (§4.1)，据说具有值语义。另一方面，类是引用类型 (§4.2)，据说具有引用语义。

一个结构体类型变量直接包含结构体的數據，而一个类类型变量包含对数据的引用，后者称为对象。当结构体 B 包含类型为 A 的实例字段且 A 是结构体类型时，A 依赖于 B 会导致编译时错误。如果结构体 X 包含类型为 Y 的实例字段，则结构体 X 直接依赖于结构体 Y。基于此定义，结构体所依赖的结构体完整集合是直接依赖关系的传递闭包。例如

```
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```

是错误，因为 Node 包含其自身类型的实例字段。另一个例子

```
struct A { B b; }
struct B { C c; }
struct C { A a; }
```

是错误，因为类型 A、B 和 C 彼此相互依赖。

对于类，两个变量可以引用同一个对象，因此对一个变量的操作可能会影响另一个变量引用的对象。对于结构体，变量各自拥有数据的副本（ref 和 out 参数变量的情况除外），因此一个变量上的操作不可能影响另一个变量。此外，由于结构体不是引用类型，结构体类型的值不可能为 null。

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

输出值为 10。将 a 赋给 b 会创建值的副本，因此 b 不受对 a.x 的赋值影响。如果 Point 改为声明为类，则输出将为 100，因为 a 和 b 将引用同一个对象。

## 11.3.2 继承

所有结构体类型都隐式继承自类 System.ValueType，而后者又继承自类 object。结构体声明可以指定已实现的接口列表，但结构体声明不能指定基类。

结构体类型永远不是抽象的，并且始终隐式密封。因此，abstract 和 sealed 修饰符不允许出现在结构体声明中。

由于结构体不支持继承，结构体成员声明的访问性不能是 protected 或 protected internal。

结构体中的函数成员不能是 abstract 或 virtual，并且 override 修饰符仅允许用于重写从 System.ValueType 继承的方法。

## 11.3.3 赋值

将值赋给结构体类型变量会创建被赋值的副本。这与将值赋给类类型变量不同，后者复制引用但不复制引用所标识的对象。

类似于赋值，当结构体作为值参数传递或作为函数成员的结果返回时，会创建结构体的副本。结构体可以通过 ref 或 out 参数按引用传递给函数成员。

当结构体的属性或索引器的目标是赋值时，与属性或索引器访问关联的实例表达式必须被分类为变量。如果实例表达式被分类为值，则会发生编译时错误。这在 §7.17.1 中有更详细的描述。

## 11.3.4 默认值

如 §5.2 中所述，几种类型的变量在创建时会自动初始化为其默认值。对于类类型和其他引用类型的变量，此默认值是 null。然而，由于结构体是不能为 null 的值类型，结构体的默认值是通过将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 而产生的值。

参考上面声明的 Point 结构体，示例

```
Point[] a = new Point[100];
```

将数组中的每个 Point 初始化为将 x 和 y 字段设置为零而产生的值。

结构体的默认值对应于结构体默认构造函数返回的值 (§4.1.2)。与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，该构造函数始终返回将所有值类型字段设置为其默认值以及所有引用类型字段设置为 null 而产生的值。

结构体应设计为将默认初始化状态视为有效状态。在示例中

```
using System;
struct KeyValuePair
{
    string key;
    string value;
    public KeyValuePair(string key, string value) {
        if (key == null || value == null) throw new ArgumentException();
        this.key = key;
        this.value = value;
    }
}
```

用户定义的实例构造函数仅在显式调用时才防止 null 值。在 KeyValuePair 变量受默认值初始化的情况中，key 和 value 字段将为 null，并且结构体必须准备好处理此状态。

## 11.3.5 装箱和拆箱

类类型的值可以通过在编译时将引用视为另一种类型，简单地转换为 object 类型或由该类实现的接口类型。同样，object 类型的值或接口类型的值可以转换回类类型，而不会更改引用（但当然在这种情况下需要运行时类型检查）。

由于结构体不是引用类型，这些操作对于结构体类型实现方式不同。当结构体类型的值转换为 object 类型或由结构体实现的接口类型时，会发生装箱操作。同样，当 object 类型的值或接口类型的值转换回结构体类型时，会发生拆箱操作。与类类型上的相同操作相比，关键区别在于装箱和拆箱会将结构体值复制到装箱实例中或从装箱实例中复制出来。因此，在装箱或拆箱操作之后，对未装箱结构体的更改不会反映在装箱结构体中。

当结构体类型重写从 System.Object 继承的虚方法（如 Equals、GetHashCode 或 ToString）时，通过结构体类型实例调用虚方法不会导致装箱发生。即使结构体用作类型参数并且调用通过类型参数类型实例发生时也是如此。例如：

```csharp
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

尽管 ToString 具有副作用是不好的风格，但该示例证明了对 x.ToString() 的三次调用均未发生装箱。

同样，在受约束的类型参数上访问成员时，装箱永远不会隐式发生。例如，假设接口 ICounter 包含一个可用于修改值的方法 Increment。如果 ICounter 用作约束，则 Increment 方法的实现会使用对调用 Increment 的变量的引用调用，从不使用装箱的副本。



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
        x.Increment();            // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();  // Modify boxed copy of x
        Console.WriteLine(x);
    }
    static void Main() {
        Test<Counter>();
    }
}
```

第一次调用 Increment 修改变量 x 中的值。这与第二次调用 Increment 不等价，后者修改的是 x 的装箱副本中的值。因此，程序的输出为：

0
1
1

有关装箱和拆箱的进一步细节，请参阅 §4.3。

## 11.3.6 this 的含义

在类的实例构造函数或实例函数成员中，this 被归类为值。因此，虽然可以使用 this 来引用调用该函数成员的实例，但在类的函数成员中无法为 this 赋值。

在结构体的实例构造函数中，this 对应于结构体类型的 out 参数，而在结构体的实例函数成员中，this 对应于结构体类型的 ref 参数。在这两种情况下，this 被归类为变量，并且可以通过为 this 赋值或将 this 作为 ref 或 out 参数传递来修改调用该函数成员的整个结构体。

## 11.3.7 字段初始化器

如 §11.3.4 所描述，结构体的默认值由将所有值类型字段设置为其默认值且所有引用类型字段设置为 null 得到的结果组成。因此，结构体不允许实例字段声明包含变量初始化器。此限制仅适用于实例字段。结构体的静态字段允许包含变量初始化器。

示例

```
struct Point
{
    public int x = 1;  // Error, initializer not permitted
    public int y = 1;  // Error, initializer not permitted
}
```

由于实例字段声明包含变量初始化器，因此出错。

## 11.3.8 构造函数

与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，该构造函数始终返回将所有值类型字段设置为其默认值且所有引用类型字段设置为 null 得到的值（§4.1.2）。结构体可以声明具有参数的实例构造函数。例如

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

根据上述声明，以下语句

```
    Point p1 = new Point();
    Point p2 = new Point(0, 0);
```

都创建了一个 x 和 y 初始化为零的 Point。

结构体实例构造函数不允许包含形式为 base(...) 的构造函数初始化器。

如果结构体实例构造函数未指定构造函数初始化器，则 this 变量对应于结构体类型的 out 参数，并且与 out 参数类似，this 必须在构造函数返回的每个位置都已明确赋值（§5.3）。如果结构体实例构造函数指定了构造函数初始化器，则 this 变量对应于结构体类型的 ref 参数，并且与 ref 参数类似，this 在进入构造函数体时被视为已明确赋值。请考虑下面的实例构造函数实现：

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
        X = x;      // error, this is not yet definitely assigned
        Y = y;      // error, this is not yet definitely assigned
    }
}
```

在被构造的结构体的所有字段都已明确赋值之前，不能调用任何实例成员函数（包括属性 X 和 Y 的 set 访问器）。请注意，然而，如果 Point 是类而不是结构体，则实例构造函数实现将被允许。

## 11.3.9 析构函数

结构体不允许声明析构函数。

## 11.3.10 静态构造函数

结构体的静态构造函数遵循与类的大多数相同规则。结构体类型的静态构造函数的执行由应用程序域内首先发生的以下事件触发：

- 引用了结构体类型的静态成员。
- 调用了结构体类型的显式声明的构造函数。

结构体类型的默认值（§11.3.4）的创建不会触发静态构造函数。（一个例子是数组中元素的初始值。）

## 11.4 结构体示例

以下展示了使用结构体类型创建可与语言内置类型类似使用但具有修改后语义的类型两个重要示例。

## 11.4.1 数据库整数类型

下面的 DBInt 结构体实现了一种整数类型，该类型可以表示 int 类型的完整值集合，外加一个表示未知值的额外状态。具有这些特征的类型在数据库中常用。

```
using System;
public struct DBInt
{
    // The Null member represents an unknown DBInt value.
    public static readonly DBInt Null = new DBInt();
    // when the defined field is true, this DBInt represents a known value
    // which is stored in the value field. When the defined field is false,
    // this DBInt represents an unknown value, and the value field is 0.
    int value;
    bool defined;
    // Private instance constructor. Creates a DBInt with a known value.
    DBInt(int value) {
        this.value = value;
        this.defined = true;
    }
    // The IsNull property is true if this DBInt represents an unknown value.
    public bool IsNull { get { return !defined; } }
    // The Value property is the known value of this DBInt, or 0 if this
    // DBInt represents an unknown value.
    public int Value { get { return value; } }
    // Implicit conversion from int to DBInt.
    public static implicit operator DBInt(int x) {
        return new DBInt(x);
    }
    // Explicit conversion from DBInt to int. Throws an exception if the
    // given DBInt represents an unknown value.
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
    return x.defined && y.defined? x.value == y.value: DBBool.Null;
}
public static DBBool operator !=(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value != y.value: DBBool.Null;
}
public static DBBool operator >(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value > y.value: DBBool.Null;
}
public static DBBool operator <(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value < y.value: DBBool.Null;
}
public static DBBool operator >=(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value >= y.value: DBBool.Null;
}
public static DBBool operator <=(DBInt x, DBInt y) {
    return x.defined && y.defined? x.value <= y.value: DBBool.Null;
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
    return defined? value.ToString(): "DBInt.Null";
}
}
```



## 11.4.2 数据库布尔类型

下面的 DBBool 结构体实现了一种三值逻辑类型。该类型的可能值为 DBBool.True、DBBool.False 和 DBBool.Null，其中 Null 成员表示未知值。这种三值逻辑类型常用于数据库。

```
using System;
public struct DBBool
{
    // The three possible DBBool values.
    public static readonly DBBool Null = new DBBool(0);
    public static readonly DBBool False = new DBBool(-1);
    public static readonly DBBool True = new DBBool(1);

    // Private field that stores -1, 0, 1 for False, Null, True.
    sbyte value;

    // Private instance constructor. The value parameter must be -1, 0, or 1.
    DBBool(int value) {
        this.value = (sbyte)value;
    }

    // Properties to examine the value of a DBBool. Return true if this
    // DBBool has the given value, false otherwise.
    public bool IsNull { get { return value == 0; } }
    public bool IsFalse { get { return value < 0; } }
    public bool IsTrue { get { return value > 0; } }

    // Implicit conversion from bool to DBBool. Maps true to DBBool.True and
    // false to DBBool.False.
    public static implicit operator DBBool(bool x) {
        return x? True: False;
    }

    // Explicit conversion from DBBool to bool. Throws an exception if the
    // given DBBool is Null, otherwise returns true or false.
    public static explicit operator bool(DBBool x) {
        if (x.value == 0) throw new InvalidOperationException();
        return x.value > 0;
    }

    // Equality operator. Returns Null if either operand is Null, otherwise
    // returns True or False.
    public static DBBool operator ==(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value == y.value? True: False;
    }

    // Inequality operator. Returns Null if either operand is Null, otherwise
    // returns True or False.
    public static DBBool operator !=(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value != y.value? True: False;
    }

    // Logical negation operator. Returns True if the operand is False, Null
    // if the operand is Null, or False if the operand is True.
    public static DBBool operator !(DBBool x) {
        return new DBBool(-x.value);
    }

    // Logical AND operator. Returns False if either operand is False,
    // otherwise Null if either operand is Null, otherwise True.
    public static DBBool operator &(DBBool x, DBBool y) {
        return new DBBool(x.value < y.value? x.value: y.value);
    }
    // Logical OR operator. Returns True if either operand is True, otherwise
    // Null if either operand is Null, otherwise False.
    public static DBBool operator |(DBBool x, DBBool y) {
        return new DBBool(x.value > y.value? x.value: y.value);
    }
    // Definitely true operator. Returns true if the operand is True, false
    // otherwise.
    public static bool operator true(DBBool x) {
        return x.value > 0;
    }
    // Definitely false operator. Returns true if the operand is False, false
    // otherwise.
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

## 12. 数组

数组是一种数据结构，它包含若干变量，这些变量通过计算得到的索引进行访问。数组中包含的变量也称为数组的元素，它们都具有相同的类型，该类型称为数组的元素类型。

数组具有秩，它决定与每个数组元素关联的索引数量。数组的秩也称为数组的维数。秩为 1 的数组称为一维数组。秩大于 1 的数组称为多维数组。特定大小的多维数组通常称为二维数组、三维数组等。

数组的每个维度都有一个关联的长度，它是一个大于或等于零的整数。维度长度不是数组类型的一部分，而是在运行时创建数组类型实例时确定的。维度长度决定该维度的有效索引范围：对于长度为 N 的维度，索引范围为 0 到 N – 1（含）。数组中的元素总数是数组中每个维度长度的乘积。如果数组的一个或多个维度的长度为零，则称该数组为空。

数组的元素类型可以是任何类型，包括数组类型。

### 12.1 数组类型

数组类型写成一个非数组类型后跟一个或多个秩说明符：

```
array-type:
    non-array-type  rank-specifiers

non-array-type:
    type

rank-specifiers:
    rank-specifier
    rank-specifiers  rank-specifier

rank-specifier:
    [ dim-separators_opt ]

dim-separators:
    ,
    dim-separators ,
```

非数组类型是任何自身不是数组类型的类型。

数组类型的秩由数组类型中最左侧的秩说明符给出：秩说明符表示该数组的秩为 1 加上该秩说明符中 `,` 标记的数量。

数组类型的元素类型是删除最左侧秩说明符后得到的类型：

- 形式为 T[R] 的数组类型是秩为 R、非数组元素类型为 T 的数组。
- 形式为 T[R][R1]…[Rn] 的数组类型是秩为 R、元素类型为 T[R1]…[Rn] 的数组。

实际上，秩说明符从最终的非数组元素类型之前从左到右读取。类型 int[,][,][,] 是一个一维数组，该数组的元素类型是三维数组，该三维数组的元素类型是二维数组，而该二维数组的元素类型是 int。

在运行时，数组类型的值可以是 null，也可以是对该数组类型实例的引用。

### 12.1.1 System.Array 类型

System.Array 类型是所有数组类型的抽象基类型。存在从任何数组类型到 System.Array 的隐式引用转换（§6.1.6），以及从 System.Array 到任何数组类型的显式引用转换（§6.2.4）。注意，System.Array 本身不是数组类型。相反，它是所有数组类型派生自的类类型。

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

        IList<string> lst1 = sa;            // Ok
        IList<string> lst2 = oa1;           // Error, cast needed
        IList<object> lst3 = sa;            // Ok
        IList<object> lst4 = oa1;           // Ok

        IList<string> lst5 = (IList<string>)oa1; // Exception
        IList<string> lst6 = (IList<string>)oa2; // Ok
    }
}
```

赋值 lst2 = oa1 会生成编译时错误，因为从 object[] 到 IList<string> 的转换是显式转换，而不是隐式转换。强制转换 (IList<string>)oa1 会在运行时引发异常，因为 oa1 引用的是 object[] 而不是 string[]。然而，强制转换 (IList<string>)oa2 不会引发异常，因为 oa2 引用的是 string[]。

每当存在从 S[] 到 IList<T> 的隐式或显式引用转换时，也存在从 IList<T> 及其基接口到 S[] 的显式引用转换（§6.2.4）。

当数组类型 S[] 实现 IList<T> 时，所实现接口的某些成员可能会引发异常。接口实现的确切行为超出了本规范的范围。

### 12.2 数组创建

数组实例由数组创建表达式（§7.6.10.4）创建，或者由包含数组初始值设定项（§12.6）的字段或局部变量声明创建。

创建数组实例时，会确定秩和每个维度的长度，然后在该实例的整个生存期内保持不变。换句话说，无法更改现有数组实例的秩，也无法调整其维度大小。




## 12.3 数组元素访问
数组元素使用 *元素访问* 表达式 (§7.6.6.1) 进行访问，形式为 A[I₁, I₂, …, Iₙ]，其中 A 是数组类型的表达式，每个 Iₓ 都是 int、uint、long、ulong 类型的表达式，或可以隐式转换为其中一种或多种类型。数组元素访问的结果是一个变量，即由索引选出的数组元素。

数组元素可以使用 foreach 语句 (§8.8.4) 进行枚举。

## 12.4 数组成员
每个数组类型都继承了 System.Array 类型声明的成员。

## 12.5 数组协变
对于任意两个引用类型 A 和 B，如果存在从 A 到 B 的隐式引用转换 (§6.1.6) 或显式引用转换 (§6.2.4)，那么从数组类型 A[R] 到数组类型 B[R] 也存在相同的引用转换，其中 R 是任意给定的秩说明符（但对两个数组类型相同）。这种关系称为数组协变。数组协变特别意味着，数组类型 A[R] 的值实际上可能是一个数组类型 B[R] 实例的引用，前提是从 B 到 A 存在隐式引用转换。

由于数组协变，对引用类型数组元素的赋值包含运行时检查，以确保赋给数组元素的值实际上是允许的类型 (§7.17.1)。例如：

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

Fill 方法中对 array[i] 的赋值隐式包含运行时检查，以确保 value 引用的对象要么为 null，要么是与 array 的实际元素类型兼容的实例。在 Main 中，Fill 的前两次调用成功，但第三次调用在执行对 array[i] 的第一次赋值时抛出 System.ArrayTypeMismatchException。异常发生的原因是装箱的 int 不能存储在字符串数组中。

数组协变特别不扩展到值类型的数组。例如，不存在允许将 int[] 当作 object[] 处理的转换。

## 12.6 数组初始化器
数组初始化器可在字段声明 (§10.5)、局部变量声明 (§8.5.1) 和数组创建表达式 (§7.6.10.4) 中指定：

```
array-initializer:
    { variable-initializer-list_opt }
    { variable-initializer-list , }

variable-initializer-list:
    variable-initializer
    variable-initializer-list , variable-initializer
```

```
variable-initializer:
  expression
  array-initializer
```

数组初始化器由一系列变量初始化器组成，用 “{” 和 “}” 标记括起来，并用 “,” 标记分隔。每个变量初始化器是一个表达式，或者在多维数组的情况下，是一个嵌套的数组初始化器。

数组初始化器使用的上下文决定了正在初始化的数组的类型。在数组创建表达式中，数组类型紧跟在初始化器之前，或从数组初始化器中的表达式推断得出。在字段或变量声明中，数组类型是正在声明的字段或变量的类型。当数组初始化器在字段或变量声明中使用时，例如：

```
int[] a = {0, 2, 4, 6, 8};
```

它只是等价数组创建表达式的简写：

```
int[] a = new int[] {0, 2, 4, 6, 8};
```

对于单维数组，数组初始化器必须由与数组元素类型赋值兼容的表达式序列组成。表达式按递增顺序初始化数组元素，从索引零的元素开始。数组初始化器中表达式的数量决定了正在创建的数组实例的长度。例如，上面的数组初始化器创建一个长度为 5 的 int[] 实例，然后用以下值初始化该实例：

```
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

对于多维数组，数组初始化器必须具有与数组中维度一样多的嵌套层级。最外层的嵌套层级对应于最左边的维度，最内层的嵌套层级对应于最右边的维度。数组每个维度的长度由数组初始化器中相应嵌套层级处的元素数量决定。对于每个嵌套的数组初始化器，其元素数量必须与同一层级的其他数组初始化器相同。示例：

```
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```

创建一个二维数组，最左边维度的长度为五，最右边维度的长度为二：

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

如果除最右边之外的一个维度被指定为长度零，则假定后续维度也具有长度零。示例：

```
int[,] c = {};
```

创建一个二维数组，最左边和最右边维度的长度均为零：

```
int[,] c = new int[0, 0];
```

当数组创建表达式同时包含显式维度长度和数组初始化器时，长度必须是常量表达式，并且每个嵌套层级处的元素数量必须与相应的维度长度匹配。以下是一些示例：

```
int i = 3;
int[] x = new int[i] {0, 1, 2};    // OK
int[] y = new int[i] {0, 1, 2};    // Error, i not a constant
int[] z = new int[3] {0, 1, 2, 3}; // Error, length/initializer mismatch
```

这里，y 的初始化器导致编译时错误，因为维度长度表达式不是常量，而 z 的初始化器导致编译时错误，因为长度与初始化器中的元素数量不匹配。

## C# 语言规范

## 13. 接口
接口定义了一个契约。实现接口的类或结构体必须遵守其契约。接口可以继承多个基接口，类或结构体可以实现多个接口。

接口可以包含方法、属性、事件和索引器。接口本身不对它定义成员提供实现。接口仅指定实现该接口的类或结构体必须提供的成员。

## 13.1 接口声明
interface-declaration 是一个类型声明 (§9.6)，声明一个新的接口类型。

```
interface-declaration:
    attributes_opt interface-modifiers_opt partial_opt interface
    identifier variant-type-parameter-list_opt interface-base_opt
    type-parameter-constraints-clauses_opt interface-body ;opt
```

interface-declaration 由一组可选的属性 (§17) 组成，其后是可选的一组接口修饰符 (§13.1.1)，其后是可选的 partial 修饰符，其后是关键字 interface 和一个命名接口的标识符，其后是可选的 variant-type-parameter-list 规范 (§13.1.3)，其后是可选的 interface-base 规范 (§13.1.4)，其后是可选的 type-parameter-constraints-clauses 规范 (§10.1.5)，其后是接口体 (§13.1.5)，可选地后跟一个分号。

### 13.1.1 接口修饰符
interface-declaration 可选择性地包含一系列接口修饰符：

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

在接口声明中，同一个修饰符出现多次是编译时错误。

new 修饰符仅允许在类中定义的接口上。它指定接口隐藏了同名继承的成员，如 §10.3.4 中所述。

public、protected、internal 和 private 修饰符控制接口的可访问性。根据接口声明出现的上下文，其中只有某些修饰符可能被允许 (§3.5.1)。

### 13.1.2 Partial 修饰符
partial 修饰符表示此 interface-declaration 是一个部分类型声明。封闭命名空间或类型声明中具有相同名称的多个部分接口声明组合形成一个接口声明，遵循 §10.2 中指定的规则。



## 13.1.3 变体类型参数列表

变体类型参数列表只能出现在接口和委托类型上。与普通类型参数列表的区别在于，每个类型参数上都有一个可选的变体注释。

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

如果变体注释为 out，则称该类型参数是协变的。如果变体注释为 in，则称该类型参数是逆变的。如果没有变体注释，则称该类型参数是不变的。

在示例中

```
interface C<out X, in Y, Z>
{
    X M(Y y);
    Z P { get; set; }
}
```

X 是协变的，Y 是逆变的，Z 是不变的。

### 13.1.3.1 变体安全性

类型参数列表中变体注释的出现会限制类型在类型声明中可出现的位置。

如果以下条件之一成立，则类型 T 是输出不安全的：

- T 是逆变类型参数
- T 是元素类型为输出不安全的数组类型
- T 是从泛型类型 S<X1, ... Xk> 构造的接口或委托类型 S<A1 ... Ak>，其中对于至少一个 Ai，以下条件之一成立：
  - Xi 是协变或不变的，并且 Ai 是输出不安全的。
  - Xi 是逆变或不变的，并且 Ai 是输入安全的。

如果以下条件之一成立，则类型 T 是输入不安全的：

- T 是协变类型参数
- T 是元素类型为输入不安全的数组类型
- T 是从泛型类型 S<X1, ... Xk> 构造的接口或委托类型 S<A1 ... Ak>，其中对于至少一个 Ai，以下条件之一成立：
  - Xi 是协变或不变的，并且 Ai 是输入不安全的。
  - Xi 是逆变或不变的，并且 Ai 是输出不安全的。

直观地说，输出不安全类型禁止出现在输出位置，输入不安全类型禁止出现在输入位置。

如果类型不是输出不安全的，则该类型是*输出安全*的；如果类型不是输入不安全的，则该类型是*输入安全*的。

### 13.1.3.2 变体转换

变体注释的目的是提供更宽松（但仍类型安全）的到接口和委托类型的转换。为此，隐式转换（§6.1）和显式转换（§6.2）的定义使用了变体可转换性的概念，其定义如下：

如果 T 是使用变体类型参数 T<X₁, ..., Xₙ> 声明的接口或委托类型，并且对于每个变体类型参数 Xᵢ，以下条件之一成立，则类型 T<A₁, ..., Aₙ> 可变体转换为类型 T<B₁, ..., Bₙ>：

- Xᵢ 是协变的，并且存在从 Aᵢ 到 Bᵢ 的隐式引用转换或恒等转换
- Xᵢ 是逆变的，并且存在从 Bᵢ 到 Aᵢ 的隐式引用转换或恒等转换
- Xᵢ 是不变的，并且存在从 Aᵢ 到 Bᵢ 的恒等转换

## 13.1.4 基接口

接口可以从零个或多个接口类型继承，这些接口类型称为该接口的*显式基接口*。当接口具有一个或多个显式基接口时，在该接口的声明中，接口标识符后跟一个冒号和一个以逗号分隔的基接口类型列表。

```
interface-base:
    : interface-type-list
```

对于构造接口类型，其显式基接口的构成方式是：取泛型类型声明上的显式基接口声明，并将基接口声明中的每个*类型参数*替换为构造类型的相应*类型实参*。

接口的显式基接口必须至少具有与该接口本身相同的可访问性（§3.5.4）。例如，在*公共*接口的*接口基*中指定*私有*或*内部*接口是编译时错误。

接口直接或间接从自身继承是编译时错误。

接口的*基接口*是显式基接口及其基接口。换言之，基接口集合是显式基接口、它们的显式基接口等的完整传递闭包。接口继承其基接口的所有成员。在示例中

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
interface IComboBox: ITextBox, IListBox {}
```

IComboBox 的基接口是 IControl、ITextBox 和 IListBox。

换言之，上面的 IComboBox 接口继承成员 SetText 和 SetItems 以及 Paint。

接口的每个基接口都必须是输出安全的（§13.1.3.1）。实现接口的类或结构也隐式实现该接口的所有基接口。

## 13.1.5 接口体

接口的接口体定义该接口的成员。

```
interface-body:
    { interface-member-declarations_opt }
```

## 13.2 接口成员

接口的成员包括从基接口继承的成员以及接口自身声明的成员。

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

接口声明可以声明零个或多个成员。接口的成员必须是方法、属性、事件或索引器。接口不能包含常量、字段、运算符、实例构造函数、析构函数或类型，接口也不能包含任何种类的静态成员。

所有接口成员都隐式具有公共访问权限。接口成员声明包含任何修饰符都是编译时错误。具体而言，接口成员不能用 abstract、public、protected、internal、private、virtual、override 或 static 修饰符声明。

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

声明一个接口，其中包含每种可能成员类型各一个：一个方法、一个属性、一个事件和一个索引器。

接口声明会创建新的声明空间（§3.3），并且由该接口声明直接包含的接口成员声明会将新成员引入此声明空间。以下规则适用于接口成员声明：

- 方法的名称必须不同于同一接口中声明的所有属性和事件的名称。此外，方法的签名（§3.6）必须不同于同一接口中声明的所有其他方法的签名，并且同一接口中声明的两个方法不能具有仅因 ref 和 out 而不同的签名。
- 属性或事件的名称必须不同于同一接口中声明的所有其他成员的名称。
- 索引器的签名必须不同于同一接口中声明的所有其他索引器的签名。

接口的继承成员明确不属于该接口的声明空间。因此，允许接口声明与继承成员具有相同名称或签名的成员。发生这种情况时，称派生接口成员*隐藏*基接口成员。隐藏继承成员不被视为错误，但确实会导致编译器发出警告。若要抑制该警告，派生接口成员的声明必须包含 `new` 修饰符，以指示派生成员意图隐藏基成员。本主题在 §3.7.1.2 中进一步讨论。

如果 `new` 修饰符包含在不隐藏继承成员的声明中，则会发出相应警告。通过移除 `new` 修饰符可抑制此警告。

请注意，严格来说，`object` 类中的成员不是任何接口的成员（§13.2）。但是，`object` 类中的成员可通过任何接口类型中的成员查找来使用（§7.4）。

### 13.2.1 接口方法

接口方法使用*接口方法声明*进行声明：

```csharp
interface-method-declaration:
    attributes_opt  new_opt  return-type  identifier  type-parameter-list
        (  formal-parameter-list_opt  )  type-parameter-constraints-clauses_opt  ;
```

接口方法声明的*特性*、*返回类型*、*标识符*和*形参列表*与类中方法声明（§10.6）的对应项具有相同含义。不允许接口方法声明指定方法体，因此该声明始终以分号结尾。

接口方法的每个形参类型必须是输入安全的（§13.1.3.1），并且返回类型必须是 `void` 或输出安全的。此外，该方法任何类型参数上的每个类类型约束、接口类型约束和类型参数约束都必须是输入安全的。

这些规则确保接口的任何协变或逆变用法保持类型安全。例如，

```csharp
interface I<out T> { void M<U>() where U : T; }
```

是非法的，因为将 `T` 用作对 `U` 的类型参数约束不是输入安全的。

如果没有此限制，就可能通过以下方式违反类型安全：

```csharp
class B {}
class D : B {}
class E : B {}
class C : I<D> { public void M<U>() {...} }

I<B> b = new C();
b.M<E>();
```

这实际上是对 `C.M<E>` 的调用。但该调用要求 `E` 派生自 `D`，因此这里会违反类型安全。

### 13.2.2 接口属性

接口属性使用*接口属性声明*进行声明：

```csharp
interface-property-declaration:
    attributes_opt  new_opt  type  identifier  {  interface-accessors  }

interface-accessors:
    attributes_opt  get  ;
    attributes_opt  set  ;
    attributes_opt  get  ;  attributes_opt  set  ;
    attributes_opt  set  ;  attributes_opt  get  ;
```


接口属性声明的特性、类型和标识符与类中的属性声明（§10.7）具有相同的含义。

接口属性声明的访问器与类属性声明（§10.7.2）的访问器相对应，不同之处在于接口访问器的主体必须始终是一个分号。因此，访问器仅指示该属性是可读写、只读还是只写。

如果存在 get 访问器，接口属性的类型必须是输出安全的；如果存在 set 访问器，则必须是输入安全的。

### 13.2.3 接口事件

接口事件使用 interface-event-declaration 声明：

```
interface-event-declaration:
    attributes_opt new_opt event type identifier ;
```

接口事件声明的特性、类型和标识符的含义与类中的事件声明（§10.8）相同。

接口事件的类型必须是输入安全的。

### 13.2.4 接口索引器

接口索引器使用 interface-indexer-declaration 声明：

```
interface-indexer-declaration:
    attributes_opt new_opt type this [ formal-parameter-list ] { interface-accessors }
```

接口索引器声明的特性、类型和形参列表的含义与类中的索引器声明（§10.9）相同。

接口索引器声明的访问器与类索引器声明（§10.9）的访问器相对应，不同之处在于访问器主体必须始终是一个分号。因此，访问器仅指示该索引器是可读写、只读还是只写。

### 13.2.5 接口成员访问

接口成员通过形式为 I.M 和 I[A] 的成员访问（§7.6.4）和索引器访问（§7.6.6.2）表达式进行访问，其中 I 是接口类型，M 是该接口类型的方法、属性或事件，A 是索引器参数列表。

对于严格单一继承的接口（继承链中的每个接口恰好有零个或一个直接基接口），成员查找（§7.4）、方法调用（§7.6.5.1）和索引器访问（§7.6.6.2）规则的效果与类和结构体完全相同：派生程度更高的成员会隐藏派生程度更低且具有相同名称或签名的成员。然而，对于多重继承的接口，当两个或更多不相关的基接口声明了具有相同名称或签名的成员时，可能会产生歧义。本节展示了此类情况的几个示例。在所有情况下，都可以使用显式转换来解决歧义。

例如

```
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
    void Test(IListCounter x) {    // Error
        x.Count(1);                 // Error
        x.Count = 1;                // Ok, invokes IList.Count.set
        ((ICounter)x).Count(1);     // Ok, invokes ICounter.Count
    }
}
```

前两个语句会导致编译时错误，因为在 IListCounter 中对 Count 的成员查找（§7.4）存在歧义。如示例所示，可以通过将 x 转换为适当的基接口类型来解决歧义。此类转换没有运行时开销——它们只是在编译时将实例视为派生程度较低的类型。

例如

```
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
        n.Add(1);       // Invokes IInteger.Add
        n.Add(1.0);     // Only IDouble.Add is applicable
        ((IInteger)n).Add(1);   // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);    // Only IDouble.Add is a candidate
    }
}
```

调用 n.Add(1) 通过应用 §7.5.3 的重载解析规则选择 IInteger.Add。类似地，调用 n.Add(1.0) 选择 IDouble.Add。当插入显式转换后，只有一个候选方法，因此不会产生歧义。

例如

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
```

```csharp
class A
{
    void Test(IDerived d) {
        d.F(1);        // Invokes ILeft.F
        ((IBase)d).F(1);   // Invokes IBase.F
        ((ILeft)d).F(1);   // Invokes ILeft.F
        ((IRight)d).F(1);  // Invokes IBase.F
    }
}
```

成员 IBase.F 被成员 ILeft.F 隐藏。因此，调用 d.F(1) 选择 ILeft.F，尽管 IBase.F 在经由 IRight 的访问路径中似乎并未被隐藏。

多重继承接口中隐藏的直观规则很简单：如果一个成员在任意访问路径中被隐藏，那么它在所有访问路径中都被隐藏。因为从 IDerived 经 ILeft 到 IBase 的访问路径隐藏了 IBase.F，所以该成员在从 IDerived 经 IRight 到 IBase 的访问路径中也被隐藏。

## 13.3 完全限定的接口成员名称

接口成员有时通过其完全限定名称来引用。接口成员的完全限定名称由声明该成员的接口名称、一个点以及该成员的名称组成。成员的完全限定名称引用声明该成员的接口。例如，给定以下声明：

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

Paint 的完全限定名称是 IControl.Paint，SetText 的完全限定名称是 ITextBox.SetText。

在上面的示例中，不能将 Paint 引用为 ITextBox.Paint。

当接口是命名空间的一部分时，接口成员的完全限定名称包含命名空间名称。例如

```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

这里，Clone 方法的完全限定名称是 System.ICloneable.Clone。

## 13.4 接口实现

类和结构体可以实现接口。为了表示某个类或结构体直接实现某个接口，需要将该接口的标识符包含在类或结构体的基类列表中。例如：

```csharp
interface ICloneable
{
    object Clone();
}
```

```csharp
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

直接实现某个接口的类或结构体，也会隐式地直接实现该接口的所有基接口。即使类或结构体没有在基类列表中显式列出所有基接口，这一点也成立。例如：

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

这里，类 TextBox 实现了 IControl 和 ITextBox。

当类 C 直接实现某个接口时，从 C 派生的所有类也隐式地实现该接口。类声明中指定的基接口可以是构造的接口类型（§4.4）。基接口本身不能是类型参数，但可以涉及范围内的类型参数。下面的代码演示了类如何实现和扩展构造类型：

```csharp
class C<U,V> {}
interface I1<V> {}
class D: C<string,int>, I1<string> {}
class E<T>: C<int,T>, I1<T> {}
```

泛型类声明的基接口必须满足 §13.4.2 中描述的唯一性规则。

### 13.4.1 显式接口成员实现

为了实现接口，类或结构体可以声明显式接口成员实现。显式接口成员实现是引用完全限定的接口成员名称的方法、属性、事件或索引器声明。例如：

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
```




```
class List<T>: IList<T>, IDictionary<int,T>
{
    T[] IList<T>.GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

这里 IDictionary<int,T>.this 和 IDictionary<int,T>.Add 是显式接口成员实现。

在某些情况下，接口成员的名称可能不适合实现该接口的类，在这种情况下，可以使用显式接口成员实现来实现该接口成员。例如，实现文件抽象的类很可能会实现一个 Close 成员函数，其作用是释放文件资源，并使用显式接口成员实现来实现 IDisposable 接口的 Dispose 方法：

```
interface IDisposable
{
    void Dispose();
}
class MyFile: IDisposable
{
    void IDisposable.Dispose() {
        Close();
    }
    public void Close() {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

不可能通过其完全限定名在方法调用、属性访问或索引器访问中访问显式接口成员实现。显式接口成员实现只能通过接口实例访问，在这种情况下仅通过其成员名引用。

显式接口成员实现包含访问修饰符是编译时错误，包含 abstract、virtual、override 或 static 修饰符也是编译时错误。

显式接口成员实现与其他成员具有不同的可访问性特征。因为显式接口成员实现永远无法通过其完全限定名在方法调用或属性访问中访问，所以在某种意义上它们是私有的。然而，由于它们可以通过接口实例访问，所以在某种意义上它们也是公共的。

显式接口成员实现主要有两个用途：

- 因为显式接口成员实现无法通过类或结构实例访问，所以它们允许将接口实现从类或结构的公共接口中排除。这在类或结构实现对该类或结构的消费者而言不感兴趣的内部接口时特别有用。
- 显式接口成员实现允许对具有相同签名的接口成员进行消歧。没有显式接口成员实现，类或结构就不可能对具有相同签名和返回类型的接口成员具有不同的实现，也就不可能对具有相同签名但返回类型不同的接口成员有任何实现。

要使显式接口成员实现有效，类或结构必须在其基类列表中命名一个接口，该接口包含一个成员，其完全限定名、类型和参数类型与显式接口成员实现完全匹配。因此，在下面的类中

```
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...}  // invalid
}
```

IComparable.CompareTo 的声明导致编译时错误，因为 IComparable 未列在 Shape 的基类列表中，也不是 ICloneable 的基接口。同样，在以下声明中

```
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
}
class Ellipse: Shape
{
    object ICloneable.Clone() {...}  // invalid
}
```

Ellipse 中 ICloneable.Clone 的声明导致编译时错误，因为 ICloneable 未明确列在 Ellipse 的基类列表中。

接口成员的完全限定名必须引用声明该成员的接口。因此，在以下声明中

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

## 13.4.2 已实现接口的唯一性

泛型类型声明所实现的接口对于所有可能的构造类型必须保持唯一。没有此规则，就不可能为某些构造类型确定要调用的正确方法。例如，假设允许泛型类声明写成如下形式：

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

如果允许这样做，则在以下情况下将无法确定要执行哪段代码：

```
I<int> x = new X<int,int>();
x.F();
```

为了确定泛型类型声明的接口列表是否有效，执行以下步骤：

- 设 L 为在泛型类、结构或接口声明 C 中直接指定的接口列表。
- 将 L 中已存在接口的任何基接口添加到 L。
- 从 L 中删除任何重复项。
- 如果从 C 创建的任何可能构造类型在将类型参数代入 L 之后会导致 L 中的两个接口相同，则 C 的声明无效。确定所有可能的构造类型时不考虑约束声明。

在上面的类声明 X 中，接口列表 L 由 I<U> 和 I<V> 组成。该声明无效，因为 U 和 V 为相同类型的任何构造类型都会导致这两个接口成为相同的类型。

可以在不同的继承级别指定接口并统一：

```
interface I<T>
{
    void F();
}
class Base<U>: I<U>
{
    void I<U>.F() {}
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

调用 Derived 中的方法，因为 Derived<int,int> 有效地重新实现了 I<int> (§13.4.6)。

## 13.4.3 泛型方法的实现

当泛型方法隐式实现接口方法时，每个方法类型参数给出的约束在两个声明中必须等价（在用适当的类型参数替换任何接口类型参数之后），其中方法类型参数按从左到右的序数位置标识。

然而，当泛型方法显式实现接口方法时，实现方法上不允许有约束。相反，约束是从接口方法继承的

```
interface I<A,B,C>
{
    void F<T>(T t) where T: A;
    void G<T>(T t) where T: B;
    void H<T>(T t) where T: C;
}
class C: I<object,C,string>
{
    public void F<T>(T t) {...}            // Ok
    public void G<T>(T t) where T: C {...} // Ok
    public void H<T>(T t) where T: string {...} // Error
}
```

方法 C.F<T> 隐式实现 I<object,C,string>.F<T>。在这种情况下，C.F<T> 不需要（也不允许）指定约束 T: object，因为 object 是所有类型参数的隐式约束。方法 C.G<T> 隐式实现 I<object,C,string>.G<T>，因为在用相应的类型参数替换接口类型参数后，约束与接口中的约束匹配。方法 C.H<T> 的约束是错误，因为密封类型（本例中为 string）不能用作约束。省略约束也将是错误，因为隐式接口方法实现的约束必须匹配。因此，不可能隐式实现 I<object,C,string>.H<T>。此接口方法只能使用显式接口成员实现来实现：

```
class C : I<object,C,string>
{
    ...
    public void H<U>(U u) where U: class {...}
    void I<object,C,string>.H<T>(T t) {
        string s = t; // Ok
        H<T>(t);
    }
}
```

在此示例中，显式接口成员实现调用了一个具有严格更弱约束的公共方法。请注意，从 t 到 s 的赋值是有效的，因为 T 继承了 T: string 的约束，即使该约束在源代码中无法表达。

## 13.4.4 接口映射

类或结构必须为列在其基类列表中的接口的所有成员提供实现。在实现类或结构中查找接口成员实现的过程称为接口映射。

对于类或结构 C 的接口映射，会为 C 的基类列表中指定的每个接口的每个成员定位一个实现。特定接口成员 I.M 的实现，其中 I 是声明成员 M 的接口，是通过检查每个类或结构 S 确定的，从 C 开始并对 C 的每个后续基类重复，直到找到匹配项：

- 如果 S 包含与 I 和 M 匹配的显式接口成员实现声明，则该成员是 I.M 的实现。
- 否则，如果 S 包含与 M 匹配的非静态公共成员声明，则该成员是 I.M 的实现。如果有多个成员匹配，则未指定哪个成员是 I.M 的实现。这种情况只能发生在 S 是构造类型时，其中两个成员在泛型类型中声明的签名不同，但类型参数使它们的签名相同。

如果无法为 C 的基类列表中指定的所有接口的所有成员定位实现，则会发生编译时错误。请注意，接口的成员包括从基接口继承的那些成员。

出于接口映射的目的，类成员 A 与接口成员 B 匹配的条件是：

- A 和 B 都是方法，并且 A 和 B 的名称、类型和形式参数列表相同。
- A 和 B 都是属性，并且 A 和 B 的名称和类型相同，且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。
- A 和 B 都是事件，并且 A 和 B 的名称和类型相同。



## C# 语言规范

- A 和 B 是索引器，A 和 B 的类型和形式参数列表相同，并且 A 具有与 B 相同的访问器（如果 A 不是显式接口成员实现，则允许 A 具有额外的访问器）。

接口映射算法的显著含义如下：

- 显式接口成员实现在确定实现接口成员的类或结构成员时优先于同一类或结构中的其他成员。
- 非公共成员和静态成员均不参与接口映射。

在示例中

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

C 的 ICloneable.Clone 成员成为 ICloneable 中 Clone 的实现，因为显式接口成员实现优先于其他成员。

如果一个类或结构实现两个或多个包含名称、类型和参数类型相同成员的接口，则可以将这些接口成员映射到单个类或结构成员上。例如

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

在这里，IControl 和 IForm 的 Paint 方法都映射到 Page 中的 Paint 方法。当然也可以为这两种方法提供单独的显式接口成员实现。

如果一个类或结构实现包含隐藏成员的接口，则某些成员必须通过显式接口成员实现来实现。例如

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

实现此接口至少需要一个显式接口成员实现，并可采用以下形式之一

```csharp
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
    public int P() {...}
}
```

当一个类实现多个具有相同基接口的接口时，基接口只能有一个实现。在示例中

```csharp
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

不可能为基类列表中命名的 IControl、由 ITextBox 继承的 IControl 以及由 IListBox 继承的 IControl 分别提供实现。事实上，这些接口没有单独身份的概念。相反，ITextBox 和 IListBox 的实现共享同一个 IControl 实现，ComboBox 只是被认为实现了三个接口，IControl、ITextBox 和 IListBox。

基类的成员参与接口映射。在示例中

```csharp
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

Class1 中的方法 F 用于 Class2 对 Interface1 的实现。

## 13.4.5 接口实现继承

一个类继承其基类提供的所有接口实现。

如果不显式重新实现接口，派生类无法以任何方式更改从基类继承的接口映射。例如，在以下声明中

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

TextBox 中的 Paint 方法隐藏了 Control 中的 Paint 方法，但它不会更改 Control.Paint 到 IControl.Paint 的映射，并且通过类实例和接口实例对 Paint 的调用将产生以下效果

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

然而，当接口方法映射到类中的虚方法时，派生类可以重写该虚方法并更改接口的实现。例如，将上述声明重写为

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
c.Paint();      // invokes Control.Paint();
t.Paint();      // invokes TextBox.Paint();
ic.Paint();     // invokes Control.Paint();
it.Paint();     // invokes TextBox.Paint();
```

由于显式接口成员实现不能声明为虚，因此无法重写显式接口成员实现。然而，显式接口成员实现调用另一个方法是完全有效的，并且该其他方法可以声明为虚以允许派生类重写它。例如

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

在这里，从 Control 派生的类可以通过重写 PaintControl 方法来专门化 IControl.Paint 的实现。

## 13.4.6 接口重新实现

继承接口实现的类允许通过将其包含在基类列表中来重新实现该接口。

接口的重新实现遵循与接口的初始实现完全相同的接口映射规则。因此，继承的接口映射对为接口重新实现建立的接口映射没有任何影响。例如，在以下声明中

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

Control 将 IControl.Paint 映射到 Control.IControl.Paint 这一事实不会影响 MyControl 中的重新实现，后者将 IControl.Paint 映射到 MyControl.Paint。

继承的公共成员声明和继承的显式接口成员声明参与重新实现接口的接口映射过程。例如

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

class Derived: Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

在这里，Derived 中 IMethods 的实现将接口方法映射到 Derived.F、Base.IMethods.G、Derived.IMethods.H 和 Base.I。

当一个类实现一个接口时，它隐式地也实现了该接口的所有基接口。同样，接口的重新实现也隐式地是对该接口所有基接口的重新实现。例如

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

在这里，IDerived 的重新实现也重新实现了 IBase，将 IBase.F 映射到 D.F。

## 13.4.7 抽象类和接口

与非抽象类一样，抽象类必须提供其基类列表中列出的接口的所有成员的实现。然而，抽象类允许将接口方法映射到抽象方法。例如

```csharp
interface IMethods
{
    void F();
    void G();
}
```



```
abstract class C: IMethods
{
    public abstract void F();
    public abstract void G();
}
```

这里，IMethods 的实现将 F 和 G 映射到抽象方法，这些方法必须在从 C 派生的非抽象类中重写。

注意，显式接口成员实现不能是抽象的，但显式接口成员实现当然可以调用抽象方法。例如

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

这里，从 C 派生的非抽象类将被要求重写 FF 和 GG，从而提供 IMethods 的实际实现。

## 14. 枚举

枚举类型是一种独特的值类型（§4.1），它声明一组命名常量。

示例

```
enum Color
{
    Red,
    Green,
    Blue
}
```

声明一个名为 Color 的枚举类型，其成员为 Red、Green 和 Blue。

### 14.1 枚举声明

枚举声明声明一个新的枚举类型。枚举声明以关键字 enum 开头，并定义枚举的名称、可访问性、基础类型和成员。

```
enum-declaration:
    attributes_opt enum-modifiers_opt enum identifier enum-base_opt enum-body ;_opt

enum-base:
    : integral-type

enum-body:
    { enum-member-declarations_opt }
    { enum-member-declarations , }
```

每个枚举类型都有一个对应的整型类型，称为该枚举类型的基础类型。此基础类型必须能够表示枚举中定义的所有枚举器值。枚举声明可以显式声明 byte、sbyte、short、ushort、int、uint、long 或 ulong 的基础类型。注意，char 不能用作基础类型。未显式声明基础类型的枚举声明，其基础类型为 int。

示例

```
enum Color: long
{
    Red,
    Green,
    Blue
}
```

声明一个基础类型为 long 的枚举。开发者可能选择使用 long 作为基础类型，如示例所示，以便能够使用位于 long 范围内但不在 int 范围内的值，或为将来保留此选项。

### 14.2 枚举修饰符

枚举声明可以选择包含一系列枚举修饰符：

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

同一修饰符在枚举声明中出现多次是编译时错误。

枚举声明的修饰符与类声明的修饰符含义相同（§10.1.1）。但请注意，枚举声明中不允许使用 abstract 和 sealed 修饰符。枚举不能是抽象的，也不允许派生。

### 14.3 枚举成员

枚举类型声明的体定义零个或多个枚举成员，这些成员是枚举类型的命名常量。任意两个枚举成员不能具有相同名称。

```
enum-member-declarations:
  enum-member-declaration
  enum-member-declarations , enum-member-declaration

enum-member-declaration:
  attributes_opt identifier
  attributes_opt identifier = constant-expression
```

每个枚举成员都有一个关联的常量值。此值的类型为包含它的枚举的基础类型。每个枚举成员的常量值必须位于该枚举的基础类型范围内。示例

```
enum Color: uint
{
  Red = -1,
  Green = -2,
  Blue = -3
}
```

会导致编译时错误，因为常量值 -1、-2 和 -3 不在基础整型类型 uint 的范围内。

多个枚举成员可以共享同一个关联值。示例

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

枚举成员的关联值可以隐式或显式分配。如果枚举成员的声明具有常量表达式初始值设定项，则该常量表达式的值（隐式转换为枚举的基础类型）就是该枚举成员的关联值。如果枚举成员的声明没有初始值设定项，则其关联值按如下方式隐式设置：

- 如果该枚举成员是枚举类型中声明的第一个枚举成员，则其关联值为零。
- 否则，该枚举成员的关联值通过将文本上位于其前面的枚举成员的关联值加一获得。增加后的值必须在基础类型可表示的取值范围内，否则会发生编译时错误。

示例

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
        Console.WriteLine(StringFromColor(Color.Red));
        Console.WriteLine(StringFromColor(Color.Green));
        Console.WriteLine(StringFromColor(Color.Blue));
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

- 枚举成员 Red 被自动赋值为零（因为它没有初始值设定项，并且是第一个枚举成员）；
- 枚举成员 Green 被显式赋予值 10；
- 并且枚举成员 Blue 被自动赋值为比文本上位于其前面的成员大 1 的值。

枚举成员的关联值不得直接或间接使用其自身关联枚举成员的值。除这一循环性限制外，枚举成员初始值设定项可以自由引用其他枚举成员初始值设定项，而不论其文本位置如何。在枚举成员初始值设定项内，其他枚举成员的值始终被视为具有其基础类型，因此在引用其他枚举成员时不需要强制转换。

示例

```
enum Circular
{
    A = B,
    B
}
```

会导致编译时错误，因为 A 和 B 的声明是循环的。A 显式依赖于 B，而 B 隐式依赖于 A。

枚举成员的命名和范围方式与类中的字段完全类似。枚举成员的作用域是其包含枚举类型的体。在该作用域内，可以通过简单名称引用枚举成员。从所有其他代码中，枚举成员的名称必须用其枚举类型的名称限定。枚举成员没有任何声明的可访问性——如果包含它的枚举类型可访问，则该枚举成员可访问。

### 14.4 System.Enum 类型

System.Enum 类型是所有枚举类型的抽象基类（它与枚举类型的基础类型不同且相异），并且从 System.Enum 继承的成员在任何枚举类型中都可用。存在从任何枚举类型到 System.Enum 的装箱转换（§4.3.1），以及从 System.Enum 到任何枚举类型的拆箱转换（§4.3.2）。

注意，System.Enum 本身不是枚举类型。相反，它是一个类类型，所有枚举类型都从它派生。System.Enum 类型继承自 System.ValueType 类型（§4.1.1），而后者又继承自 object 类型。在运行时，System.Enum 类型的值可以为 null，也可以是对任何枚举类型的装箱值的引用。

### 14.5 枚举值和操作

每个枚举类型定义一个不同的类型；在枚举类型与整型类型之间，或在两个枚举类型之间进行转换，需要显式枚举转换（§6.2.2）。枚举类型可采用的值的集合不受其枚举成员限制。特别地，枚举的基础类型的任何值都可以强制转换为该枚举类型，并且是该枚举类型的一个不同的有效值。

枚举成员具有其包含枚举类型的类型（其他枚举成员初始值设定项内除外：参见 §14.3）。在枚举类型 E 中声明的、关联值为 v 的枚举成员，其值为 (E)v。

以下运算符可用于枚举类型的值：==、!=、<、>、<=、>=（§7.10.5）、二元 +（§7.8.4）、二元 -（§7.8.5）、^、&、|（§7.11.2）、~（§7.7.4）、++ 和 --（§7.6.9 和 §7.7.5）。

每个枚举类型都自动派生自 System.Enum 类（后者又派生自 System.ValueType 和 object）。因此，该类的继承方法和属性可用于枚举类型的值。



## 15. 委托

委托实现了其他语言（如 C++、Pascal 和 Modula）使用函数指针来处理的场景。然而，与 C++ 函数指针不同，委托是完全面向对象的，并且与 C++ 成员函数指针不同，委托同时封装了一个对象实例和方法。

委托声明定义了一个派生自类 System.Delegate 的类。委托实例封装了一个调用列表，它是一个包含一个或多个方法列表，每个方法被称为可调用实体。对于实例方法，可调用实体由一个实例及其上的方法组成。对于静态方法，可调用实体仅由一个方法组成。使用适当的一组参数调用委托实例会导致委托的每个可调用实体都使用给定的参数集被调用。

委托实例的一个有趣且有用的特性是它并不关心也不在乎其封装的方法的类；唯一重要的是这些方法与委托的类型兼容（§15.1）。这使得委托非常适合“匿名”调用。

### 15.1 委托声明

委托声明是一个类型声明（§9.6），它声明一个新的委托类型。

```
delegate-declaration:
    attributes_opt delegate-modifiers_opt delegate return-type
    identifier variant-type-parameter-list_opt
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;

delegate-modifiers:
    delegate-modifier
    delegate-modifier delegate-modifier

delegate-modifier:
    new
    public
    protected
    internal
    private
```

在委托声明中，相同的修饰符出现多次是编译时错误。

new 修饰符仅允许用于在另一个类型内声明的委托，在这种情况下它指定该委托隐藏了同名继承的成员，如 §10.3.4 所述。

public、protected、internal 和 private 修饰符控制委托类型的可访问性。根据委托声明出现的上下文，其中一些修饰符可能不被允许（§3.5.1）。

委托的类型名是 identifier。

可选的 formal-parameter-list 指定委托的参数，return-type 表示委托的返回类型。

可选的 variant-type-parameter-list（§13.1.3）指定委托本身的类型参数。

委托类型的返回类型必须是 void，或 output-safe（§13.1.3.1）。

委托类型的所有形式参数类型必须是 input-safe。此外，任何 out 或 ref 参数类型也必须是 output-safe。注意，即使是 out 参数也要求是 input-safe，这是由于底层执行平台的限制。

C# 中的委托类型按名称等价，而不是结构等价。具体来说，具有相同参数列表和返回类型的两个不同委托类型被视为不同的委托类型。然而，两个不同但结构等价的委托类型的实例可能比较相等（§7.9.8）。

例如：

```
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

与其他泛型类型声明类似，必须给出类型参数才能创建构造的委托类型。通过为委托声明中的每个类型参数替换构造的委托类型的相应类型参数，来创建构造的委托类型的参数类型和返回类型。所得的返回类型和参数类型用于确定哪些方法与构造的委托类型兼容。例如：

```
delegate bool Predicate<T>(T value);
class X
{
    static bool F(int i) {...}
    static bool G(string s) {...}
}
```

委托类型 Predicate<int> 与方法 X.F 兼容，委托类型 Predicate<string> 与方法 X.G 兼容。

声明委托类型的唯一方式是通过委托声明。委托类型是从 System.Delegate 派生的类类型。委托类型是隐式密封的，因此不允许从委托类型派生任何类型。也不允许从 System.Delegate 派生非委托类类型。注意 System.Delegate 本身不是委托类型；它是一个类类型，所有委托类型都从它派生。

C# 为委托实例化和调用提供了特殊语法。除了实例化之外，可以应用于类或类实例的任何操作也可以分别应用于委托类或实例。特别是，可以通过通常的成员访问语法访问 System.Delegate 类型的成员。

委托实例封装的方法集称为调用列表。当委托实例由单个方法创建（§15.2）时，它封装该方法，其调用列表仅包含一个条目。然而，当两个非空委托实例组合时，它们的调用列表会按左操作数然后右操作数的顺序连接，以形成新的调用列表，其中包含两个或多个条目。

委托使用二元 +（§7.8.4）和 += 运算符（§7.17.2）组合。委托可以使用二元 -（§7.8.5）和 -= 运算符（§7.17.2）从委托组合中移除。委托可以进行相等比较（§7.10.8）。

以下示例展示了多个委托的实例化及其对应的调用列表：

```
delegate void D(int x);
class C
{
    public static void M1(int i) {...}
    public static void M2(int i) {...}
}
class Test
{
    static void Main() {
        D cd1 = new D(C.M1);      // M1
        D cd2 = new D(C.M2);      // M2
        D cd3 = cd1 + cd2;        // M1 + M2
        D cd4 = cd3 + cd1;        // M1 + M2 + M1
        D cd5 = cd4 + cd3;        // M1 + M2 + M1 + M1 + M2
    }
}
```

当 cd1 和 cd2 被实例化时，它们各自封装一个方法。当 cd3 被实例化时，它具有包含两个方法 M1 和 M2 的调用列表，按此顺序。cd4 的调用列表包含 M1、M2 和 M1，按此顺序。最后，cd5 的调用列表包含 M1、M2、M1、M1 和 M2，按此顺序。有关组合（以及移除）委托的更多示例，请参阅 §15.4。

### 15.2 委托兼容性

方法或委托 M 与委托类型 D *兼容* 当且仅当以下所有条件都为真时：

- D 和 M 具有相同数量的参数，并且 D 中的每个参数与 M 中对应参数具有相同的 `ref` 或 `out` 修饰符。
- 对于每个值参数（没有 `ref` 或 `out` 修饰符的参数），从 D 中的参数类型到 M 中对应参数类型存在恒等转换（§6.1.1）或隐式引用转换（§6.1.6）。
- 对于每个 `ref` 或 `out` 参数，D 中的参数类型与 M 中的参数类型相同。
- 从 M 的返回类型到 D 的返回类型存在恒等或隐式引用转换。

### 15.3 委托实例化

委托的实例由 *委托创建表达式*（§7.6.10.5）或转换为委托类型创建。新建的委托实例随后引用以下之一：

- *委托创建表达式* 中引用的静态方法，或
- *委托创建表达式* 中引用的目标对象（不能为 `null`）和实例方法，或


- 另一个委托。

例如：

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

一旦实例化，委托实例始终引用相同的目标对象和方法。请记住，当两个委托组合，或者一个委托从另一个委托中移除时，会产生一个新的委托，它拥有自己的调用列表；被组合或移除的委托的调用列表保持不变。

## 15.4 委托调用

C# 提供了用于调用委托的特殊语法。当调用一个非 null 且其调用列表仅包含一个条目的委托实例时，它将使用所给的相同参数调用那个方法，并返回与被引用方法相同的值。（关于委托调用的详细信息，请参见 §7.6.5.3。）如果在调用此类委托期间发生异常，且该异常未在被调用的方法中被捕获，则将继续在调用该委托的方法中搜索异常捕获子句，就好像该方法直接调用了该委托所引用的方法一样。

调用列表包含多个条目的委托实例的调用，会按顺序同步调用调用列表中的每个方法。所调用的每个方法都会收到与委托实例相同的参数集。如果此类委托调用包含引用参数（§10.6.1.2），则每次方法调用都将引用同一个变量；调用列表中某个方法对该变量所做的更改，对于调用列表后续的方法将是可见的。如果委托调用包含输出参数或返回值，则其最终值将来自列表中最后一个委托的调用。

如果在处理此类委托调用期间发生异常，且该异常未在被调用的方法中被捕获，则将继续在调用该委托的方法中搜索异常捕获子句，并且调用列表中任何更靠后的方法都将不会被调用。

尝试调用值为 null 的委托实例将导致类型为 System.NullReferenceException 的异常。以下示例演示了如何实例化、组合、移除和调用委托：

```csharp
using System;
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
        D cd4 = new D(C.M3);
        cd3 += cd4;
        cd3(30);    // call M1, M2, M1, then M3
        cd3 -= cd1;    // remove last M1
        cd3(40);    // call M1, M2, then M3
        cd3 -= cd4;
        cd3(50);    // call M1 then M2
        cd3 -= cd2;
        cd3(60);    // call M1
        cd3 -= cd2;    // impossible removal is benign
        cd3(60);    // call M1
        cd3 -= cd1;    // invocation list is empty so cd3 is null
        //  cd3(70);  // System.NullReferenceException thrown
        cd3 -= cd1;    // impossible removal is benign
    }
}
```

如语句 `cd3 += cd1;` 所示，一个委托可以在调用列表中出现多次。在这种情况下，它只是每次出现时被调用一次。在这样一个调用列表中，当该委托被移除时，调用列表中最后一次出现的位置才是实际被移除的。

在最后一条语句 `cd3 -= cd1;` 执行之前，委托 cd3 引用一个空的调用列表。尝试从空列表中移除委托（或从非空列表中移除不存在的委托）并不是错误。

产生的输出为：

## 16. 异常

C# 中的异常提供了一种结构化、统一且类型安全的方式来处理系统级和应用程序级的错误条件。C# 中的异常机制与 C++ 非常相似，但有几个重要的区别：

- 在 C# 中，所有异常都必须由派生自 System.Exception 的类类型的实例来表示。在 C++ 中，任何类型的任何值都可以用来表示异常。
- 在 C# 中，可以使用 finally 块（§8.10）来编写终止代码，这些代码在正常执行和异常情况下都会执行。在 C++ 中，如果不重复代码，很难编写这样的代码。
- 在 C# 中，诸如溢出、除零和空引用之类的系统级异常具有定义良好的异常类，并且与应用程序级错误条件处于同等地位。

### 16.1 异常的原因

异常可以通过两种不同的方式抛出：

- throw 语句（§8.9.5）立即且无条件地抛出异常。控制永远不会到达紧跟在 throw 之后的语句。
- 在处理 C# 语句和表达式过程中出现的某些异常情况，在操作无法正常完成时，会在特定情况下导致异常。例如，如果分母为零，整数除法运算（§7.8.2）会抛出 System.DivideByZeroException。有关可能以这种方式发生的各种异常的列表，请参见 §16.4。

### 16.2 System.Exception 类

System.Exception 类是所有异常的基类型。此类具有几个所有异常共享的值得注意的属性：

- Message 是类型为 string 的只读属性，包含异常原因的人类可读描述。
- InnerException 是类型为 Exception 的只读属性。如果其值非 null，则它引用导致当前异常的异常——也就是说，当前异常是在处理 InnerException 的 catch 块中引发的。否则，其值为 null，表示此异常不是由另一个异常引起的。以这种方式链接在一起的异常对象的数量可以是任意的。

这些属性的值可以在对 System.Exception 的实例构造函数的调用中指定。

### 16.3 异常的处理方式

异常由 try 语句（§8.10）处理。

当发生异常时，系统会搜索能够处理该异常的最近 catch 子句，具体由异常的运行时类型决定。首先，在当前方法中搜索词法上封闭的 try 语句，并按顺序考虑该 try 语句关联的 catch 子句。如果失败，则在调用当前方法的方法中搜索词法上封闭且包含对当前方法调用点的 try 语句。此搜索一直持续到找到能够处理当前异常的 catch 子句，即通过命名与所抛出异常的运行时类型相同或为其基类的异常类。未命名异常类的 catch 子句可以处理任何异常。

一旦找到匹配的 catch 子句，系统就准备将控制转移到该 catch 子句的第一条语句。在 catch 子句开始执行之前，系统首先按顺序执行与比捕获异常的那个 try 语句嵌套更深的 try 语句关联的所有 finally 子句。

如果没有找到匹配的 catch 子句，则会发生以下两种情况之一：

- 如果对匹配 catch 子句的搜索到达静态构造函数（§10.12）或静态字段初始化器，则在触发静态构造函数调用的位置抛出 System.TypeInitializationException。System.TypeInitializationException 的内部异常包含最初抛出的异常。
- 如果对匹配 catch 子句的搜索到达最初启动线程的代码，则线程的执行将被终止。这种终止的影响由实现定义。

在析构函数执行期间发生的异常值得特别提及。如果在析构函数执行期间发生异常，并且该异常未被捕获，那么该析构函数的执行将终止，并调用基类（如果有）的析构函数。如果没有基类（如 object 类型的情况）或没有基类析构函数，则该异常将被丢弃。

### 16.4 常见异常类

以下异常由某些 C# 操作抛出。

| 异常 | 描述 |
|---|---|
| System.ArithmeticException | 算术运算期间发生的异常的基类，例如 System.DivideByZeroException 和 System.OverflowException。 |
| System.ArrayTypeMismatchException | 当向数组存储元素失败，因为存储元素的实际类型与数组的实际类型不兼容时抛出。 |
| System.DivideByZeroException | 当尝试将整数值除以零时抛出。 |
| System.IndexOutOfRangeException | 当尝试使用小于零或超出数组边界的索引对数组进行索引时抛出。 |
| System.InvalidCastException | 当从基类型或接口到派生类型的显式转换在运行时失败时抛出。 |
| System.NullReferenceException | 当使用 null 引用导致需要引用对象时抛出。 |
| System.OutOfMemoryException | 当尝试（通过 new）分配内存失败时抛出。 |
| System.OverflowException | 当 checked 上下文中的算术运算溢出时抛出。 |
| System.StackOverflowException | 当执行堆栈因挂起的方法调用过多而耗尽时抛出；通常表示非常深或无界的递归。 |
| System.TypeInitializationException | 当静态构造函数抛出异常且不存在捕获该异常的 catch 子句时抛出。 |




## 17. 属性

C# 语言的大部分功能使程序员能够为程序中定义的实体指定声明性信息。例如，类中方法的访问性是通过为其添加方法修饰符 public、protected、internal 和 private 来指定的。

C# 使程序员能够发明新的声明性信息类型，称为属性。程序员随后可以将属性附加到各种程序实体，并在运行时环境中检索属性信息。例如，一个框架可能会定义一个 HelpAttribute 属性，该属性可以放置在某些程序元素（如类和方法）上，以提供这些程序元素与其文档之间的映射。

属性是通过属性类的声明来定义的 (§17.1)，属性类可以具有位置参数和命名参数 (§17.1.2)。属性是使用属性规范 (§17.2) 附加到 C# 程序中的实体，并在运行时作为属性实例检索 (§17.3)。

### 17.1 属性类

派生自抽象类 System.Attribute 的类，无论是直接还是间接，都称为属性类。属性类的声明定义了一种可以放置在声明上的新属性类型。按惯例，属性类以 Attribute 为后缀命名。使用属性时可以包含或省略此后缀。

### 17.1.1 属性用法

AttributeUsage 属性 (§17.4.1) 用于描述属性类如何被使用。

AttributeUsage 具有一个位置参数 (§17.1.2)，使属性类能够指定其可使用的声明类型。示例

```
using System;
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute
{
    ...
}
```

定义了一个名为 SimpleAttribute 的属性类，只能放置在类声明和接口声明上。示例

```
[Simple] class Class1 {...}
[Simple] interface Interface1 {...}
```

显示了 Simple 属性的几种用法。尽管此属性定义时名称为 SimpleAttribute，但在该属性使用时可以省略 Attribute 后缀，从而得到简短名称 Simple。因此，上面的示例在语义上等同于以下内容：

```
[SimpleAttribute] class Class1 {...}
[SimpleAttribute] interface Interface1 {...}
```

AttributeUsage 具有一个名为 AllowMultiple 的命名参数 (§17.1.2)，指示该属性是否可以对给定实体指定多次。如果属性类的 AllowMultiple 为 true，则该属性类为多用属性类，可以在实体上指定多次。如果属性类的 AllowMultiple 为 false 或未指定，则该属性类为单用属性类，最多只能在实体上指定一次。

示例

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

定义了一个名为 AuthorAttribute 的多用属性类。示例

```csharp
[Author("Brian Kernighan"), Author("Dennis Ritchie")]
class Class1
{
    ...
}
```

显示了一个类声明，其中使用了两次 Author 属性。

AttributeUsage 还有另一个名为 Inherited 的命名参数，指示当属性指定在基类上时，是否也会被派生自该基类的类继承。如果属性类的 Inherited 为 true，则该属性会被继承。如果属性类的 Inherited 为 false 则该属性不会被继承。如果未指定，其默认值是 true。

未附加 AttributeUsage 属性的属性类 X，如

```csharp
using System;
class X: Attribute {...}
```

所示，等同于以下内容：

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

属性类可以具有位置参数和命名参数。属性类的每个公共实例构造函数都为该属性类定义了一个有效的位置参数序列。属性类的每个非静态公共读写字段和属性都为该属性类定义一个命名参数。

示例

```csharp
using System;
[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute : Attribute
{
    public HelpAttribute(string url) {  // Positional parameter
        ...
    }

    public string Topic {
        get {...}
        set {...}
    }  // Named parameter

    public string Url {
        get {...}
    }
}
```

定义了一个名为 HelpAttribute 的属性类，它有一个位置参数 url 和一个命名参数 Topic。尽管 Url 属性是非静态的且为公共，但它不定义命名参数，因为它不是可读写的。

该属性类可能按如下方式使用：

```
[Help("http://www.mycompany.com/.../class1.htm")]
class Class1
{
    ...
}

[Help("http://www.mycompany.com/.../misc.htm", Topic = "Class2")]
class Class2
{
    ...
}
```

### 17.1.3 属性参数类型

属性类的位置参数和命名参数的类型仅限于属性参数类型，具体如下：

- 以下类型之一：bool、byte、char、double、float、int、long、sbyte、short、string、uint、ulong、ushort。
- 类型 object。
- 类型 System.Type。
- 枚举类型，前提是它具有公共可访问性，并且其中嵌套的类型（如有）也具有公共可访问性 (§17.2)。
- 上述类型的单维数组。

构造函数参数或公共字段如果不具有这些类型之一，则不能在属性规范中用作位置参数或命名参数。

### 17.2 属性规范

属性规范是将先前定义的属性应用于声明。属性是为声明指定的额外声明性信息的一部分。属性可以在全局作用域指定（以指定包含程序集或模块的属性），也可以用于类型声明 (§9.6)、类成员声明 (§10.1.5)、接口成员声明 (§13.2)、结构成员声明 (§11.2)、枚举成员声明 (§14.3)、访问器声明 (§10.7.2)、事件访问器声明 (§10.8.1) 和形式参数列表 (§10.6.1)。

属性在属性节中指定。属性节由一对方括号组成，方括号包围一个或多个属性的逗号分隔列表。在此类列表中指定属性的顺序，以及附加到同一程序实体的节的排列顺序，均无关紧要。例如，属性规范 [A] [B]、[B] [A]、[A, B] 和 [B, A] 是等价的。

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

一个特性由一个特性名以及可选的位置参数和命名参数列表组成。位置参数（如果有）位于命名参数之前。位置参数由一个特性实参表达式组成；命名参数由一个名称、后跟等号、再后跟一个特性实参表达式组成，它们共同受与简单赋值相同的规则约束。命名参数的顺序不重要。

特性名标识一个特性类。如果特性名的形式是类型名，那么该名称必须引用一个特性类。否则，将发生编译时错误。示例

```
class Class1 {}
[Class1] class Class2 {}  // Error
```

会导致编译时错误，因为它试图在 Class1 不是特性类时将 Class1 用作特性类。

某些上下文允许在多个目标上指定一个特性。程序可以通过包含特性目标说明符来显式指定目标。当特性置于全局级别时，需要全局特性目标说明符。在所有其他位置，会应用合理的默认值，但在某些有歧义的情况下，可以使用特性目标说明符来确认或重写默认值（或者仅在无歧义的情况下确认默认值）。因此，通常除全局级别外，可以省略特性目标说明符。潜在有歧义的上下文按如下方式解决：

- 在全局范围指定的特性可以应用于目标程序集或目标模块。此上下文不存在默认值，因此在此上下文中始终需要特性目标说明符。存在 assembly 特性目标说明符表示该特性应用于目标程序集；存在 module 特性目标说明符表示该特性应用于目标模块。

- 在委托声明上指定的特性可以应用于正在声明的委托或其返回值。缺少特性目标说明符时，该特性应用于委托。存在 type 特性目标说明符表示该特性应用于委托；存在 return 特性目标说明符表示该特性应用于返回值。

- 在方法声明上指定的特性可以应用于正在声明的方法或其返回值。缺少特性目标说明符时，该特性应用于方法。存在 method 特性目标说明符表示该特性应用于方法；存在 return 特性目标说明符表示该特性应用于返回值。

- 在运算符声明上指定的特性可以应用于正在声明的运算符或其返回值。缺少特性目标说明符时，该特性应用于运算符。存在 method 特性目标说明符表示该特性应用于运算符；存在 return 特性目标说明符表示该特性应用于返回值。

- 在省略事件访问器的事件声明上指定的特性可以应用于正在声明的事件、关联字段（如果事件不是抽象事件）或关联的 add 和 remove 方法。缺少特性目标说明符时，该特性应用于事件。存在 event 特性目标说明符表示该特性应用于事件；存在 field 特性目标说明符表示该特性应用于字段；存在 method 特性目标说明符表示该特性应用于方法。

- 在属性或索引器声明的 get 访问器声明上指定的特性可以应用于关联方法或其返回值。缺少特性目标说明符时，该特性应用于方法。存在 method 特性目标说明符表示该特性应用于方法；存在 return 特性目标说明符表示该特性应用于返回值。

- 在属性或索引器声明的 set 访问器声明上指定的特性可以应用于关联方法或其唯一的隐式参数。缺少特性目标说明符时，该特性应用于方法。存在 method 特性目标说明符表示该特性应用于方法；存在 param 特性目标说明符表示该特性应用于参数；存在 return 特性目标说明符表示该特性应用于返回值。

- 在事件声明的 add 或 remove 访问器声明上指定的特性可以应用于关联方法或其唯一参数。缺少特性目标说明符时，该特性应用于方法。存在 method 特性目标说明符表示该特性应用于方法；存在 param 特性目标说明符表示该特性应用于参数；存在 return 特性目标说明符表示该特性应用于返回值。

在其他上下文中，允许包含特性目标说明符，但不是必需的。例如，类声明可以包含或省略说明符 type：

```
[type: Author("Brian Kernighan")]
class Class1 {}
[Author("Dennis Ritchie")]
class Class2 {}
```

指定无效的特性目标说明符是错误的。例如，说明符 param 不能用于类声明：

```
[param: Author("Brian Kernighan")]    // Error
class Class1 {}
```

按照约定，特性类的命名带有后缀 Attribute。形式为类型名的特性名可以包含或省略此后缀。如果同时找到带此后缀和不带此后缀的特性类，则存在歧义，并导致编译时错误。如果特性名的拼写使其最右侧标识符是逐字标识符（§2.4.2），则只匹配不带后缀的特性，从而能够解决此类歧义。示例

```
using System;
[AttributeUsage(AttributeTargets.All)]
public class X: Attribute
{}
[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}
[x]    // Error: ambiguity
class Class1 {}
[XAttribute]    // Refers to XAttribute
class Class2 {}
[@x]    // Refers to X
class Class3 {}
[@XAttribute]    // Refers to XAttribute
class Class4 {}
```

展示了两个名为 X 和 XAttribute 的特性类。特性 [X] 有歧义，因为它可以引用 X 或 XAttribute。使用逐字标识符允许在此类罕见情况下指定确切的意图。特性 [XAttribute] 没有歧义（不过如果存在名为 XAttributeAttribute 的特性类，就会有歧义！）。如果移除类 X 的声明，那么两个特性都会引用名为 XAttribute 的特性类，如下所示：

```
using System;
[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}
[x]    // Refers to XAttribute
class Class1 {}
[XAttribute]    // Refers to XAttribute
class Class2 {}
[@x]    // Error: no attribute named "x"
class Class3 {}
```

在同一实体上多次使用单次使用特性类会导致编译时错误。示例

```
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

会导致编译时错误，因为它试图在 Class1 的声明上多次使用 HelpString，而 HelpString 是一个单次使用特性类。

如果以下所有语句均为真，则表达式 E 是特性实参表达式：

- E 的类型是特性参数类型（§17.1.3）。




- 在编译时，E 的值可以解析为以下其中之一：
  - 一个常量值。
  - 一个 System.Type 对象。
  - 一个一维的 *属性参数表达式* 数组。

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

    public object P3 {
        get {...}
        set {...}
    }
}

[Test(P1 = 1234, P3 = new int[] {1, 3, 5}, P2 = typeof(float))]
class MyClass {}
```

一个作为属性参数表达式使用的 *typeof 表达式* (§7.6.11) 可以引用非泛型类型、封闭构造类型或未绑定泛型类型，但不能引用开放类型。这是为了确保表达式可以在编译时解析。

```csharp
class A: Attribute
{
    public A(Type t) {...}
}

class G<T>
{
    [A(typeof(T))] T t;             // Error, open type in attribute
}

class X
{
    [A(typeof(List<int>))] int x;   // Ok, closed constructed type
    [A(typeof(List<>))] int y;      // Ok, unbound generic type
}
```

## 17.3 属性实例

一个 *属性实例* 是在运行时表示一个属性的实例。一个属性是用属性类、位置参数和命名参数定义的。一个属性实例是属性类的一个实例，它使用位置参数和命名参数进行初始化。

检索属性实例涉及编译时和运行时的处理，如以下各节所述。

### 17.3.1 属性的编译

一个具有属性类 T、*位置参数列表* P 和 *命名参数列表* N 的 *属性* 的编译包括以下步骤：

- 遵循编译对象创建表达式 new T(P) 形式的编译时处理步骤。这些步骤要么导致编译时错误，要么确定可在运行时调用的 T 上的实例构造函数 C。
- 如果 C 没有公共可访问性，则会发生编译时错误。
- 对于 N 中的每个命名参数 Arg：
  - 将 Name 设置为命名参数 Arg 的标识符。
  - Name 必须标识 T 上的一个非静态可读写的公共字段或属性。如果 T 没有这样的字段或属性，则会发生编译时错误。
- 为属性的运行时实例化保留以下信息：属性类 T、T 上的实例构造函数 C、*位置参数列表* P 和 *命名参数列表* N。

### 17.3.2 属性实例的运行时检索

属性的编译会产生属性类 T、T 上的实例构造函数 C、*位置参数列表* P 和 *命名参数列表* N。给定这些信息，可以使用以下步骤在运行时检索属性实例：

- 遵循执行对象创建表达式 new T(P) 形式的运行时处理步骤，使用编译时确定的实例构造函数 C。这些步骤要么导致异常，要么产生 T 的实例 O。
- 按顺序对 N 中的每个命名参数 Arg：
  - 将 Name 设置为命名参数 Arg 的标识符。如果 Name 不能标识 O 上的一个非静态公共可读写字段或属性，则会抛出异常。
  - 将 Value 设置为 Arg 的属性参数表达式的求值结果。
  - 如果 Name 标识 O 上的一个字段，则将该字段设置为 Value。
  - 否则，Name 标识 O 上的一个属性。将该属性设置为 Value。
- 结果是 O，即使用 *位置参数列表* P 和 *命名参数列表* N 初始化的属性类 T 的一个实例。

## 17.4 保留属性

少量属性以某种方式影响语言。这些属性包括：

- System.AttributeUsageAttribute (§17.4.1)，用于描述属性类可以使用的方式。
- System.Diagnostics.ConditionalAttribute (§17.4.2)，用于定义条件方法。
- System.ObsoleteAttribute (§17.4.3)，用于将成员标记为已过时。

### 17.4.1 AttributeUsage 属性

AttributeUsage 属性用于描述属性类可以使用的方式。

用 AttributeUsage 属性装饰的类必须直接或间接派生自 System.Attribute。否则会发生编译时错误。

```csharp
namespace System
{
    [AttributeUsage(AttributeTargets.Class)]
    public class AttributeUsageAttribute: Attribute
    {
        public AttributeUsageAttribute(AttributeTargets validOn) {...}
        public virtual bool AllowMultiple { get {...} set {...} }
        public virtual bool Inherited { get {...} set {...} }
        public virtual AttributeTargets ValidOn { get {...} }
    }

    public enum AttributeTargets
    {
        Assembly = 0x0001,
        Module = 0x0002,
        Class = 0x0004,
        Struct = 0x0008,
        Enum = 0x0010,
        Constructor = 0x0020,
        Method = 0x0040,
        Property = 0x0080,
        Field = 0x0100,
        Event = 0x0200,
        Interface = 0x0400,
        Parameter = 0x0800,
        Delegate = 0x1000,
        ReturnValue = 0x2000,

        All = Assembly | Module | Class | Struct | Enum | Constructor |
            Method | Property | Field | Event | Interface | Parameter |
            Delegate | ReturnValue
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
    public class ConditionalAttribute: Attribute
    {
        public ConditionalAttribute(string conditionString) {...}
        public string ConditionString { get {...} }
    }
}
```

#### 17.4.2.1 条件方法

用 Conditional 属性装饰的方法是条件方法。Conditional 属性通过测试条件编译符号来指示一个条件。对条件方法的调用是否包含取决于调用点是否定义了该符号。如果定义了该符号，则包含调用；否则，省略调用（包括接收者和调用参数的求值）。

条件方法受以下限制：

- 条件方法必须是类声明或结构声明中的方法。如果在接口声明中的方法上指定了 Conditional 属性，则会发生编译时错误。
- 条件方法必须具有 void 返回类型。
- 条件方法不得标记为 override 修饰符。然而，条件方法可以标记为 virtual 修饰符。此类方法的重写隐式为条件，且不得显式标记为 Conditional 属性。
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

声明 Class1.M 为条件方法。Class2 的 Test 方法调用此方法。由于条件编译符号 DEBUG 已定义，如果调用 Class2.Test，它将调用 M。如果未定义符号 DEBUG，则 Class2.Test 不会调用 Class1.M。

请注意，对条件方法的调用的包含或排除由调用点的条件编译符号控制。在示例中

```csharp
File class1.cs:
    using System.Diagnostics;
    class Class1
    {
        [Conditional("DEBUG")]
        public static void F() {
            Console.WriteLine("Executed Class1.F");
        }
    }

File class2.cs:
    #define DEBUG
    class Class2
    {
        public static void G() {
            Class1.F();    // F is called
        }
    }

File class3.cs:
    #undef DEBUG
```



```
class Class3
{
    public static void H() {
        Class1.F();        // F is not called
    }
}
```

类 Class2 和 Class3 各自包含对条件方法 Class1.F 的调用，该方法根据 DEBUG 是否定义而为条件。由于该符号在 Class2 的上下文中定义，而在 Class3 中未定义，因此 Class2 中的对 F 的调用被包含，而 Class3 中的对 F 的调用被省略。

在继承链中使用条件方法可能会令人困惑。通过 base 以 base.M 的形式对条件方法进行的调用受正常条件方法调用规则的约束。示例中

文件 class1.cs:

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

文件 class2.cs:

```
using System;
class Class2: Class1
{
    public override void M() {
        Console.WriteLine("Class2.M executed");
        base.M();                // base.M is not called!
    }
}
```

文件 class3.cs:

```
#define DEBUG
using System;
class Class3
{
    public static void Test() {
        Class2 c = new Class2();
        c.M();                   // M is called
    }
}
```

Class2 包含对其基类中定义的 M 的调用。由于基方法根据符号 DEBUG 的存在而为条件，且该符号未定义，因此此调用被省略。因此，该方法仅向控制台写入“Class2.M executed”。谨慎使用预处理指令可以消除此类问题。

## 17.4.2.2 条件属性类

用一个或多个 Conditional 属性装饰的属性类（§17.1）是条件属性类。

因此，条件属性类与在其 Conditional 属性中声明的条件编译符号相关联。以下示例：

```
using System;
using System.Diagnostics;
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

将 TestAttribute 声明为与条件编译符号 ALPHA 和 BETA 相关联的条件属性类。

条件属性的属性规范（§17.2）如果在其关联的条件编译符号中的一个或多个在规范点被定义则包含，否则属性规范被省略。

需要注意的是，条件属性类的属性规范的包含或排除由规范点处的条件编译符号控制。示例中

```
File test.cs:
    using System;
    using System.Diagnostics;
    [Conditional("DEBUG")]
    public class TestAttribute : Attribute {}

File class1.cs:
    #define DEBUG
    [Test]        // TestAttribute is specified
    class Class1 {}

File class2.cs:
    #undef DEBUG
    [Test]        // TestAttribute is not specified
    class Class2 {}
```

类 Class1 和 Class2 各自用属性 Test 装饰，该属性根据 DEBUG 是否定义而为条件。由于该符号在 Class1 的上下文中定义而在 Class2 中未定义，因此 Class1 上的 Test 属性的规范被包含，而 Class2 上的 Test 属性的规范被省略。

## 17.4.3 Obsolete 属性

Obsolete 属性用于标记不应再使用的类型和类型的成员。

```csharp
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
    public class ObsoleteAttribute: Attribute
    {
        public ObsoleteAttribute() {...}
        public ObsoleteAttribute(string message) {...}
        public ObsoleteAttribute(string message, bool error) {...}
        public string Message { get {...} }
        public bool IsError { get {...} }
    }
}
```

如果程序使用用 Obsolete 属性装饰的类型或成员，编译器会发出警告或错误。具体而言，如果未提供 error 参数，或提供了 error 参数且其值为 false，则编译器发出警告。如果指定了 error 参数且其值为 true，则编译器发出错误。

示例中

```csharp
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
        A a = new A();      // warning
        a.F();
    }
}
```

类 A 用 Obsolete 属性装饰。Main 中对 A 的每次使用都会产生警告，其中包含指定的消息，“This class is obsolete; use class B instead.”

## 17.5 用于互操作的特性

*注意：本节仅适用于 Microsoft .NET 对 C# 的实现。*

## 17.5.1 与 COM 和 Win32 组件的互操作

.NET 运行库提供了大量属性，使 C# 程序能够与使用 COM 和 Win32 DLL 编写的组件互操作。例如，DllImport 属性可用于

static extern 方法以指示该方法的实现位于 Win32 DLL 中。这些属性位于 System.Runtime.InteropServices 命名空间中，这些属性的详细文档可在 .NET 运行时文档中找到。

## 17.5.2 与其他 .NET 语言的互操作

## 17.5.2.1 IndexerName 属性

在 .NET 中，索引器使用索引属性实现，并在 .NET 元数据中具有名称。如果索引器没有 IndexerName 属性，则默认使用名称 Item。IndexerName 属性使开发人员能够覆盖此默认值并指定不同的名称。

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

## 18. 不安全代码

如前几章所述的核心 C# 语言，与 C 和 C++ 相比，其显著区别在于省略了指针作为数据类型。相反，C# 提供了引用以及创建由垃圾回收器管理的对象的能力。这种设计结合其他特性，使 C# 比 C 和 C++ 更安全得多。在核心 C# 语言中，根本不可能出现未初始化的变量、“dangling” 指针或索引超出数组边界的表达式。 routinely 困扰 C 和 C++ 程序的整类错误因此被消除。

尽管 C 或 C++ 中几乎每种指针类型构造在 C# 中都有引用类型对应物，但仍存在需要访问指针类型的情况。例如，在没有指针访问的情况下，可能无法或不切实际地与底层操作系统接口、访问内存映射设备或实现时间关键算法。为解决此需求，C# 提供了编写不安全代码的能力。

在不安全代码中，可以声明和操作指针、执行指针与整数类型之间的转换、获取变量的地址，等等。从某种意义上说，在 C# 程序中编写不安全代码就像在 C# 程序中编写 C 代码一样。

从开发人员和用户的角度来看，不安全代码实际上是一种“安全”特性。不安全代码必须用 unsafe 修饰符明确标记，因此开发人员不可能意外使用不安全特性，并且执行引擎会确保不安全代码无法在不受信任的环境中执行。

## 18.1 不安全上下文

C# 的不安全特性仅在不安全上下文中可用。不安全上下文是通过在类型或成员的声明中包含 unsafe 修饰符，或使用 unsafe-statement 来引入的：

- 类、结构、接口或委托的声明可以包含 unsafe 修饰符，在这种情况下，该类型声明的整个文本范围（包括类、结构或接口的主体）被视为不安全上下文。
- 字段、方法、属性、事件、索引器、运算符、实例构造函数、析构函数或静态构造函数的声明可以包含 unsafe 修饰符，在这种情况下，该成员声明的整个文本范围被视为不安全上下文。
- unsafe-statement 使能够在块内使用不安全上下文。与之关联的块的整个文本范围被视为不安全上下文。

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
```

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
destructor-declaration:
    attributes_opt unsafe_opt ~ identifier ( ) destructor-body
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

在以下示例中：

```
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
```

结构声明中指定的 `unsafe` 修饰符会使该结构声明的整个文本范围成为不安全上下文。因此，可以将 `Left` 和 `Right` 字段声明为指针类型。上面的示例也可以写成：

```
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

在这里，字段声明中的 `unsafe` 修饰符使这些声明被视为不安全上下文。

除了建立不安全上下文，从而允许使用指针类型之外，`unsafe` 修饰符不会对类型或成员产生任何影响。在以下示例中：

```
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
        ...
    }
}
```

`A` 中 `F` 方法上的 `unsafe` 修饰符仅会使 `F` 的整个文本范围成为不安全上下文，在该上下文中可以使用语言的不安全功能。在 `B` 对 `F` 的重写中，无需重新指定 `unsafe` 修饰符——当然，除非 `B` 中的 `F` 方法本身需要访问不安全功能。

当指针类型成为方法签名的一部分时，情况略有不同：

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

这里，由于 `F` 的签名包含指针类型，因此只能在不安全上下文中编写它。不过，可以通过以下任一方式引入不安全上下文：使整个类成为不安全类（如 `A` 中所示），或者在方法声明中包含 `unsafe` 修饰符（如 `B` 中所示）。

## 18.2 指针类型

在不安全上下文中，类型（§4）除了可以是值类型或引用类型之外，还可以是指针类型。不过，在不安全上下文之外，指针类型也可以用于 typeof 表达式（§7.6.10.6），因为这种用法并不不安全。

-   type:
-       ...
-       pointer-type

指针类型由非托管类型或关键字 `void` 后跟一个 `*` 标记构成：

```
pointer-type:
    unmanaged-type *
    void *

unmanaged-type:
    type
```

指针类型中 `*` 前指定的类型称为该指针类型的指向类型。它表示指针类型值所指向的变量的类型。

与引用（引用类型的值）不同，指针不会被垃圾回收器跟踪——垃圾回收器不了解指针，也不了解指针所指向的数据。因此，不允许指针指向引用或包含引用的结构，并且指针的指向类型必须是非托管类型。

非托管类型是任何不是引用类型或构造类型，且在任意嵌套层级都不包含引用类型或构造类型字段的类型。换句话说，非托管类型包括以下类型：

-   - `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double`、`decimal` 或 `bool`。
-   - 任意枚举类型。
-   - 任意指针类型。
-   - 任意不是构造类型且仅包含非托管类型字段的用户定义结构类型。

指针和引用混合使用时的直观规则是：引用的指向对象允许包含指针，但指针的指向对象不允许包含引用。

下表给出了一些指针类型的示例：

| 示例 | 描述 |
|---|---|
| byte* | 指向 byte 的指针 |
| char* | 指向 char 的指针 |
| int** | 指向 int 指针的指针 |
| int*[] | 指向 int 的指针所组成的一维数组 |
| void* | 指向未知类型的指针 |

对于给定的实现，所有指针类型都必须具有相同的大小和表示形式。与 C 和 C++ 不同，当在同一声明中声明多个指针时，C# 只将 `*` 与基础类型一起书写，而不会将其作为每个指针名称前的前缀标点。例如 `int* pi, pj; // NOT as int *pi, *pj;`。类型为 `T*` 的指针值表示类型为 `T` 的变量的地址。可以使用指针间接寻址运算符 `*`（§18.5.1）访问此变量。例如，给定一个类型为 `int*` 的变量 `P`，表达式 `*P` 表示位于 `P` 中所包含地址处的 `int` 变量。与对象引用一样，指针可以为 null。对 null 指针应用间接寻址运算符会产生由实现定义的行为。值为 null 的指针以全零位表示。

`void*` 类型表示指向未知类型的指针。由于指向类型未知，不能对 `void*` 类型的指针应用间接寻址运算符，也不能对这种指针执行任何算术运算。不过，`void*` 类型的指针可以转换为任何其他指针类型，反之亦然。

指针类型是独立的一类类型。与引用类型和值类型不同，指针类型不继承自 `object`，并且指针类型与 `object` 之间不存在转换。特别是，指针不支持装箱和拆箱（§4.3）。不过，不同指针类型之间，以及指针类型与整型之间允许进行转换。相关内容请参见 §18.4。

指针类型不能用作类型实参（§4.4），并且对于本应推断出指针类型类型实参的泛型方法调用，类型推断（§7.5.2）会失败。

指针类型可以用作易失性字段（§10.5.3）的类型。

尽管指针可以作为 `ref` 或 `out` 参数传递，但这样做可能导致未定义行为，因为指针可能会被设置为指向某个局部变量，而被调用方法返回时该局部变量已经不存在；或者指针以前指向的固定对象不再处于固定状态。例如：

```
using System;
class Test
{
    static int value = 20;
    unsafe static void F(out int* pi1, ref int* pi2) {
        int i = 10;
        pi1 = &i;
        fixed (int* pj = &value) {
            // ...
            pi2 = pj;
        }
    }

    static void Main() {
        int i = 10;
        unsafe {
            int* px1;
            int* px2 = &i;
            F(out px1, ref px2);
            Console.WriteLine("{0}, *px2 = {1}",
                *px1, *px2);  // undefined behavior
        }
    }
}
```

方法可以返回某种类型的值，而该类型可以是指针类型。例如，给定一个指向连续 `int` 序列的指针、该序列的元素数量以及另一个 `int` 值，以下方法会在匹配成功时返回该序列中该值的地址，否则返回 null：

```
unsafe static int* Find(int* pi, int size, int value) {
    for (int i = 0; i < size; ++i) {
        if (*pi == value)
            return pi;
        ++pi;
    }
    return null;
}
```

在不安全上下文中，可以使用以下若干构造来操作指针：

-   - `*` 运算符可用于执行指针间接寻址（§18.5.1）。
-   - `->` 运算符可用于通过指针访问结构成员（§18.5.2）。
-   - `[]` 运算符可用于对指针进行索引（§18.5.3）。
-   - `&` 运算符可用于获取变量的地址（§18.5.4）。
-   - `++` 和 `--` 运算符可用于递增和递减指针（§18.5.5）。
-   - `+` 和 `-` 运算符可用于执行指针算术运算（§18.5.6）。
-   - `==`、`!=`、`<`、`>`、`<=` 和 `>=` 运算符可用于比较指针（§18.5.7）。
-   - `stackalloc` 运算符可用于从调用堆栈分配内存（§18.7）。
-   - `fixed` 语句可用于临时固定变量，以便获取其地址（§18.6）。

## 18.3 固定变量和可移动变量

取地址运算符（§18.5.4）和 `fixed` 语句（§18.6）将变量分为两类：固定变量和可移动变量。

固定变量位于不受垃圾回收器操作影响的存储位置中。（固定变量的示例包括局部变量、值参数以及通过对指针进行解引用而创建的变量。）另一方面，可移动变量位于可能被垃圾回收器重新定位或释放的存储位置中。（可移动变量的示例包括对象中的字段和数组中的元素。）

`&` 运算符允许不受限制地获取固定变量的地址。不过，由于可移动变量可能被垃圾回收器重新定位或释放，因此只能使用 `fixed` 语句（§18.6）获取可移动变量的地址，并且该地址仅在此 `fixed` 语句的持续期间有效。

严格来说，固定变量包括以下几种：

-   - 由简单名称（§7.6.2）产生且引用局部变量或值参数的变量，除非该变量被匿名函数捕获。
-   - 由形式为 `V.I` 的成员访问（§7.6.4）产生的变量，其中 `V` 是结构类型的固定变量。
-   - 由形式为 `*P` 的指针间接寻址表达式（§18.5.1）、形式为 `P->I` 的指针成员访问（§18.5.2）或形式为 `P[E]` 的指针元素访问（§18.5.3）产生的变量。

所有其他变量都归类为可移动变量。

请注意，静态字段被归类为可移动变量。还请注意，即使为 `ref` 或 `out` 参数提供的实参是固定变量，`ref` 或 `out` 参数也会被归类为可移动变量。最后请注意，通过对指针进行解引用而产生的变量始终被归类为固定变量。

## 18.4 指针转换

在不安全上下文中，可用的隐式转换集合（§6.1）扩展为包括以下隐式指针转换：

-   - 从任意指针类型转换为 `void*` 类型。
-   - 从 null 字面量转换为任意指针类型。

此外，在不安全上下文中，可用的显式转换集合（§6.2）扩展为包括以下显式指针转换：

-   - 从任意指针类型转换为任意其他指针类型。
-   - 从 `sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 或 `ulong` 转换为任意指针类型。




- 从任意指针类型到 sbyte、byte、short、ushort、int、uint、long 或 ulong。

最后，在 unsafe 上下文中，标准隐式转换 (§6.3.1) 的集合包括以下指针转换：

- 从任意指针类型到 void* 类型。

转换两个指针类型永远不会改变实际的指针值。换句话说，从一种指针类型到另一种指针类型的转换对指针给出的底层地址没有任何影响。

当一种指针类型转换为另一种时，如果 resulting pointer 对指向的类型不对齐，则如果对其进行解引用，行为是未定义的。通常，“correctly aligned”的概念是传递的：如果指向类型 A 的指针对指向类型 B 的指针正确对齐，而后者又对指向类型 C 的指针正确对齐，则指向类型 A 的指针对指向类型 C 的指针正确对齐。

考虑以下情况，其中具有一种类型的变量通过指向不同类型的指针进行访问：

```
char c = 'A';
char* pc = &c;
void* pv = pc;
int* pi = (int*)pv;
int i = *pi;    // undefined
*pi = 123456;    // undefined
```

当指针类型转换为指向 byte 的指针时，结果指向变量的最低地址字节。对结果的连续递增，直到变量的大小，会产生指向该变量剩余字节的指针。例如，以下方法以十六进制值显示 double 中的每个字节：

```
using System;
class Test
{
    unsafe static void Main() {
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

当然，产生的输出取决于字节序。

指针与整数之间的映射是实现定义的。然而，在具有线性地址空间的 32 位和 64 位 CPU 架构上，指针与整数类型之间的转换通常表现得与 uint 或 ulong 值分别与这些整数类型之间的转换完全相同。

### 18.4.1 指针数组

在 unsafe 上下文中，可以构造指针数组。仅允许对指针数组应用适用于其他数组类型的某些转换：

- 从任意数组类型到 System.Array 及其实现的接口的隐式引用转换 (§6.1.6) 也适用于指针数组。然而，通过 System.Array 或其实现的接口访问数组元素的任何尝试都将在运行时导致异常，因为指针类型不能转换为 object。

- 从单维数组类型 S[] 到 System.Collections.Generic.IList<T> 及其基接口的隐式和显式引用转换 (§6.1.6, §6.2.4) 从不适用于指针数组，因为指针类型不能用作类型参数，并且指针类型到非指针类型的转换不存在。

- 从 System.Array 及其实现的接口到任意数组类型的显式引用转换 (§6.2.4) 适用于指针数组。

- 从 System.Collections.Generic.IList<S> 及其基接口到单维数组类型 T[] 的显式引用转换 (§6.2.4) 从不适用于指针数组，因为指针类型不能用作类型参数，并且指针类型到非指针类型的转换不存在。

这些限制意味着 §8.8.4 中描述的对数组的 foreach 语句的展开不能应用于指针数组。相反，形式为

```
foreach (V v in x) embedded-statement
```

其中 x 的类型是形式为 T[, ...] 的数组类型，n 是维度数减 1，且 T 或 V 是指针类型，则使用嵌套 for 循环按如下方式展开：

```
{
    T[, ...] a = x;
    V v;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
    for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
    for (int i_n = a.GetLowerBound(n); i_n <= a.GetUpperBound(n); i_n++) {
        v = (V)a.GetValue(i0,i1,...,i_n);
        embedded-statement
    }
}
```

变量 a、i0、i1、... i_n 对 x、嵌入语句或程序的任何其他源代码不可见或不可访问。变量 v 在嵌入语句中是只读的。如果不存在从 T（元素类型）到 V 的显式转换 (§18.4)，则会产生错误且不进行任何进一步步骤。如果 x 的值为 null，则在运行时抛出 System.NullReferenceException。

## 18.5 表达式中的指针

在 unsafe 上下文中，表达式可能产生指针类型的结果，但在 unsafe 上下文之外，表达式为指针类型是编译时错误。精确地说，在 unsafe 上下文之外，如果任何简单名称 (§7.6.2)、成员访问 (§7.6.4)、调用表达式 (§7.6.5) 或元素访问 (§7.6.6) 为指针类型，则会发生编译时错误。

在 unsafe 上下文中，primary-no-array-creation-expression (§7.6) 和 unary-expression (§7.7) 产生式允许以下附加构造：

```
primary-no-array-creation-expression:
...
pointer-member-access
pointer-element-access
sizeof-expression

unary-expression:
...
pointer-indirection-expression
addressof-expression
```

这些构造在以下各节中描述。unsafe 运算符的优先级和结合性由语法暗示。

### 18.5.1 指针间接

pointer-indirection-expression 由一个星号 (*) 后跟一个 unary-expression 组成。

```
pointer-indirection-expression:
  * unary-expression
```

一元 * 运算符表示指针间接引用，用于获取指针指向的变量。计算 *P 的结果，其中 P 是指针类型 T* 的表达式，是类型为 T 的变量。对类型为 void* 的表达式或不是指针类型的表达式应用一元 * 运算符是编译时错误。

对空指针应用一元 * 运算符的效果是实现定义的。特别是，不能保证此操作会抛出 System.NullReferenceException。

如果为指针分配了无效值，则一元 * 运算符的行为是未定义的。通过一元 * 运算符解引用指针的无效值包括为指向的类型不当对齐的地址（参见 §18.4 中的示例），以及变量生命周期结束后的地址。

对于确定性赋值分析，通过计算形式为 *P 的表达式产生的变量被视为已初始赋值 (§5.3.1)。

### 18.5.2 指针成员访问

pointer-member-access 由一个 primary-expression，后跟 "->" 标记，后跟一个标识符组成。

```
pointer-member-access:
  primary-expression -> identifier
```

在形式为 P->I 的指针成员访问中，P 必须是除 void* 之外的指针类型的表达式，且 I 必须表示 P 指向的类型的一个可访问成员。

形式为 P->I 的指针成员访问的计算方式与 (*P).I 完全相同。有关指针间接运算符 (*) 的描述，请参阅 §18.5.1。有关成员访问运算符 (.) 的描述，请参阅 §7.6.4。

在示例中

```
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

-> 运算符用于通过指针访问结构体的字段并调用方法。因为操作 P->I 与 (*P).I 精确等价，Main 方法同样可以写成：

```
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

### 18.5.3 指针元素访问

pointer-element-access 由一个 primary-no-array-creation-expression 后跟用 “[” 和 “]” 括起来的表达式组成。

```
pointer-element-access:
    primary-no-array-creation-expression [ expression ]
```

在形式为 P[E] 的指针元素访问中，P 必须是除 void* 之外的指针类型的表达式，且 E 必须是可隐式转换为 int、uint、long 或 ulong 的表达式。

形式为 P[E] 的指针元素访问的计算方式与 *(P + E) 完全相同。有关指针间接运算符 (*) 的描述，请参阅 §18.5.1。有关指针加法运算符 (+) 的描述，请参阅 §18.5.6。

在示例中

```
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

指针元素访问用于在 for 循环中初始化字符缓冲区。因为操作 P[E] 与 *(P + E) 精确等价，示例同样可以写成：

```
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

指针元素访问运算符不检查越界错误，访问越界元素时的行为是未定义的。这与 C 和 C++ 相同。

### 18.5.4 取地址运算符

addressof-expression 由一个与号 (&) 后跟一个 unary-expression 组成。

```
addressof-expression:
    & unary-expression
```

给定一个类型为 T 且被归类为固定变量 (§18.3) 的表达式 E，构造 &E 计算由 E 给出的变量的地址。结果的类型为 T*，被归类为值。A

如果 E 未被归类为变量、E 被归类为只读局部变量，或者 E 表示可移动变量，则发生编译时错误。在最后一种情况下，可以使用 fixed 语句（§18.6）在获取变量的地址之前临时“固定”该变量。如 §7.6.4 所述，在定义了 readonly 字段的结构或类的实例构造函数或静态构造函数之外，该字段被视为值，而不是变量。因此，不能获取它的地址。同样，也不能获取常量的地址。

& 运算符不要求其参数已明确赋值，但在 & 运算之后，在该运算发生的执行路径中，应用该运算符的变量被视为已明确赋值。程序员有责任确保在这种情况下确实对该变量进行了正确的初始化。

在示例中

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

在用于初始化 p 的 &i 运算之后，i 被视为已明确赋值。对 *p 的赋值实际上初始化了 i，但包含此初始化是程序员的责任，如果移除该赋值，则不会发生编译时错误。

& 运算符的明确赋值规则的存在是为了避免局部变量的冗余初始化。例如，许多外部 API 接受一个指向结构的指针，该结构由 API 填充。对此类 API 的调用通常传递局部结构变量的地址，如果没有该规则，则需要对结构变量进行冗余初始化。

## 18.5.5 指针递增和递减

在不安全上下文中，++ 和 -- 运算符（§7.6.9 和 §7.7.5）可应用于除 void* 之外的所有类型的指针变量。因此，对于每个指针类型 T*，以下运算符被隐式定义：

```csharp
T* operator ++(T* x);
T* operator --(T* x);
```

这些运算符分别产生与 x + 1 和 x - 1 相同的结果（§18.5.6）。换言之，对于类型 T* 的指针变量，++ 运算符将 sizeof(T) 加到该变量包含的地址上，而 -- 运算符从该变量包含的地址中减去 sizeof(T)。

如果指针递增或递减运算溢出指针类型的域，则结果由实现定义，但不会产生异常。

## 18.5.6 指针算术

在不安全上下文中，+ 和 - 运算符（§7.8.4 和 §7.8.5）可应用于除 void* 之外的所有指针类型的值。因此，对于每个指针类型 T*，以下运算符被隐式定义：

```csharp
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

给定指针类型 T* 的表达式 P 和类型为 int、uint、long 或 ulong 的表达式 N，表达式 P + N 和 N + P 计算将 N * sizeof(T) 加到 P 给出的地址上所得的 T* 类型的指针值。同样，表达式 P - N 计算从 P 给出的地址中减去 N * sizeof(T) 所得的 T* 类型的指针值。

给定指针类型 T* 的两个表达式 P 和 Q，表达式 P - Q 计算 P 和 Q 给出的地址之间的差，然后将该差除以 sizeof(T)。结果类型始终为 long。实际上，P - Q 按 ((long)(P) - (long)(Q)) / sizeof(T) 计算。

例如：

```
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

它产生以下输出：

```
p - q = -14
q - p = 14
```

如果指针算术运算溢出指针类型的域，则结果以实现定义的方式截断，但不会产生异常。

## 18.5.7 指针比较

在不安全上下文中，==、!=、<、>、<= 和 >= 运算符（§7.10）可应用于所有指针类型的值。指针比较运算符为：

```
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

由于存在从任何指针类型到 void* 类型的隐式转换，因此可以使用这些运算符比较任何指针类型的操作数。比较运算符将两个操作数给出的地址当作无符号整数进行比较。

## 18.5.8 sizeof 运算符

sizeof 运算符返回给定类型的变量所占用的字节数。指定为 sizeof 操作数的类型必须是非托管类型（§18.2）。

```
sizeof-expression:
    sizeof ( unmanaged-type )
```

sizeof 运算符的结果是 int 类型的值。对于某些预定义类型，sizeof 运算符产生如下表所示的常量值。

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

对于所有其他类型，sizeof 运算符的结果由实现定义，并被归类为值，而不是常量。

成员打包到结构中的顺序未指定。

出于对齐目的，结构的开头、结构内部和结构末尾可能存在未命名的填充。用作填充的位的内容是不确定的。

当应用于具有结构类型的操作数时，结果是该类型变量中的总字节数，包括任何填充。

## 18.6 fixed 语句

在不安全上下文中，embedded-statement（§8）产生式允许附加构造，即 fixed 语句，用于“固定”可移动变量，使其地址在语句的持续时间内保持不变。

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

每个 fixed-pointer-declarator 声明给定 pointer-type 的局部变量，并用相应的 fixed-pointer-initializer 计算出的地址初始化该局部变量。在 fixed 语句中声明的局部变量，在该变量声明右侧出现的任何 fixed-pointer-initializer 中以及在 fixed 语句的 embedded-statement 中均可访问。由 fixed 语句声明的局部变量被视为只读。如果 embedded 语句试图修改此局部变量（通过赋值或 ++ 和 -- 运算符）或将其作为 ref 或 out 参数传递，则发生编译时错误。

fixed-pointer-initializer 可以是以下之一：

- 标记“&”后跟对非托管类型 T 的可移动变量（§18.3）的 variable-reference（§5.3.3），前提是类型 T* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算给定变量的地址，并保证该变量在 fixed 语句的持续时间内保持在固定地址。
- 数组类型的表达式，其元素为非托管类型 T，前提是类型 T* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算数组中第一个元素的地址，并保证整个数组在 fixed 语句的持续时间内保持在固定地址。如果数组表达式为 null 或数组元素为零，则 fixed 语句的行为由实现定义。
- 类型为 string 的表达式，前提是类型 char* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算字符串中第一个字符的地址，并保证整个字符串在 fixed 语句的持续时间内保持在固定地址。如果字符串表达式为 null，则 fixed 语句的行为由实现定义。
- 引用固定大小缓冲区成员的 simple-name 或 member-access 是可移动变量，前提是该固定大小缓冲区成员的类型可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算指向固定大小缓冲区（§18.7.2）第一个元素的指针，并保证该固定大小缓冲区在 fixed 语句的持续时间内保持在固定地址。

对于 fixed-pointer-initializer 计算的每个地址，fixed 语句确保该地址引用的变量在 fixed 语句的持续时间内不会被垃圾回收器重定位或释放。例如，如果 fixed-pointer-initializer 计算的地址引用对象的字段或数组实例的元素，则 fixed 语句保证包含该字段或元素的对象的实例在语句的生存期内不会被重定位或释放。

程序员有责任确保由 fixed 语句创建的指针不会在这些语句执行之后继续存在。例如，当由 fixed 语句创建的指针传递给外部 API 时，程序员有责任确保这些 API 不保留对这些指针的任何记忆。

固定对象可能导致堆碎片化（因为它们无法移动）。因此，仅应在绝对必要时固定对象，并且只应固定尽可能最短的时间。

示例

```
class Test
{
    static int x;
    int y;
```



```csharp
unsafe static void F(int* p) {
    *p = 1;
}
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
```

该示例演示了 fixed 语句的几种用法。第一个语句固定并获取静态字段的地址，第二个语句固定并获取实例字段的地址，第三个语句固定并获取数组元素的地址。在每种情况下，使用常规的 & 运算符都会出错，因为这些变量都被归类为可移动变量。

第四个 fixed 语句与第三个产生类似的结果。

fixed 语句的此示例使用字符串：

```csharp
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

在不安全上下文中，单维数组的元素按递增索引顺序存储，从索引 0 开始，到索引 Length – 1 结束。对于多维数组，数组元素存储方式为先增加最右维的索引，然后是下一个左维，依此类推向左。在获取指向数组实例 a 的指针 p 的 fixed 语句中，从 p 到 p + a.Length – 1 的指针值表示数组中元素的地址。同样，变量 p[0] 到 p[a.Length – 1] 表示实际的数组元素。鉴于数组的存储方式，我们可以将任意维度的数组视为线性。

例如：

```csharp
using System;
class Test
{
    static void Main() {
        int[,,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i) // treat as linear
                    p[i] = i;
            }
        }

        for (int i = 0; i < 2; ++i) {
            for (int j = 0; j < 3; ++j) {
                for (int k = 0; k < 4; ++k)
                    Console.Write("{0},{1},{2} = {3,2} ", i, j, k, a[i,j,k]);
                Console.WriteLine();
            }
        }
    }
}
```

其输出为：

```text
[0,0,0] = 0 [0,0,1] = 1 [0,0,2] = 2 [0,0,3] = 3
[0,1,0] = 4 [0,1,1] = 5 [0,1,2] = 6 [0,1,3] = 7
[0,2,0] = 8 [0,2,1] = 9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23
```

在示例中

```csharp
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

使用 fixed 语句固定数组，以便将其地址传递给接受指针的方法。

在示例中：

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

    Font f;
    unsafe static void Main()
    {
        Test test = new Test();
        test.f.size = 10;
        fixed (char* p = test.f.name) {
            PutString("Times New Roman", p, 32);
        }
    }
}
```

使用 fixed 语句固定结构体的固定大小缓冲区，以便其地址可作为指针使用。

通过固定字符串实例产生的 char* 值始终指向以 null 结尾的字符串。在获取指向字符串实例 s 的指针 p 的 fixed 语句中，从 p 到 p + s.Length - 1 的指针值表示字符串中字符的地址，而指针值 p + s.Length 始终指向 null 字符（值为 '\0' 的字符）。

通过固定指针修改托管类型的对象可能导致未定义行为。例如，由于字符串是不可变的，程序员有责任确保不修改由指向固定字符串的指针引用的字符。

字符串的自动 null 终止在调用期望“C 风格”字符串的外部 API 时特别方便。然而请注意，字符串实例允许包含 null 字符。如果存在此类 null 字符，则在将其视为以 null 结尾的 char* 处理时，字符串将显示为被截断。

## 18.7 固定大小缓冲区

固定大小缓冲区用于将“C 风格”的内联数组声明为结构体的成员，主要用于与非托管 API 接口。

### 18.7.1 固定大小缓冲区声明

固定大小缓冲区是表示给定类型变量的固定长度缓冲区存储的成员。固定大小缓冲区声明引入一个或多个给定元素类型的固定大小缓冲区。固定大小缓冲区仅允许在结构体声明中使用，并且只能出现在不安全上下文中（§18.1）。

```text
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

固定大小缓冲区声明可以包含一组属性（§17）、new 修饰符（§10.2.2）、四个访问修饰符（§10.2.3）的有效组合以及 unsafe 修饰符（§18.1）。属性和修饰符适用于固定大小缓冲区声明所声明的所有成员。同一修饰符在固定大小缓冲区声明中出现多次是错误。

固定大小缓冲区声明不允许包含 static 修饰符。

固定大小缓冲区声明的缓冲区元素类型指定声明所引入的缓冲区（s）的元素类型。缓冲区元素类型必须是预定义类型 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 bool 之一。

缓冲区元素类型后面跟着固定大小缓冲区声明符的列表，每个声明符引入一个新成员。固定大小缓冲区声明符由标识成员的名称的标识符组成，后跟用 [ 和 ] 标记括起来的常量表达式。该常量表达式表示该固定大小缓冲区声明符所引入的成员中的元素数。常量表达式的类型必须可隐式转换为 int 类型，且值必须是大于零的正整数。

固定大小缓冲区的元素保证在内存中按顺序布局。

声明多个固定大小缓冲区的固定大小缓冲区声明等效于使用相同属性和元素类型的单个固定大小缓冲区声明的多次声明。例如

```csharp
unsafe struct A
{
    public fixed int x[5], y[10], z[100];
}
```

等效于

```csharp
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```

### 18.7.2 表达式中的固定大小缓冲区

固定大小缓冲区成员的成员查找（§7.3）与字段的成员查找完全相同。

固定大小缓冲区可以通过简单名称（§7.5.2）或成员访问（§7.5.4）在表达式中引用。

当固定大小缓冲区成员作为简单名称引用时，其效果与形式为 this.I 的成员访问相同，其中 I 是固定大小缓冲区成员。

在形式为 E.I 的成员访问中，如果 E 是结构体类型，并且在该结构体类型中对 I 的成员查找识别出一个固定大小缓冲区成员，则 E.I 的求值和分类如下：

- 如果表达式 E.I 不在不安全上下文中出现，则会发生编译时错误。
- 如果 E 被分类为值，则会发生编译时错误。
- 否则，如果 E 是可移动变量（§18.3）并且表达式 E.I 不是固定指针初始化器（§18.6），则会发生编译时错误。
- 否则，E 引用一个固定变量，表达式的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针。结果的类型为 S*，其中 S 是 I 的元素类型，并被分类为值。

固定大小缓冲区的后续元素可以使用从第一个元素开始的指针操作进行访问。

与数组访问不同，固定大小缓冲区元素的访问是不安全操作且不进行范围检查。

以下示例声明并使用具有固定大小缓冲区成员的结构体。



```
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

## 18.7.3 确定性赋值检查

固定大小缓冲区不受确定性赋值检查 (§5.3) 的约束，并且在对结构体类型变量进行确定性赋值检查时，固定大小缓冲区成员会被忽略。

当固定大小缓冲区成员的最外层包含的结构体变量是静态变量、类实例的实例变量或数组元素时，固定大小缓冲区的元素会自动初始化为其默认值 (§5.2)。在所有其他情况下，固定大小缓冲区的初始内容是未定义的。

## 18.8 栈分配

在不安全上下文中，局部变量声明 (§8.5.1) 可以包含栈分配初始化器，该初始化器从调用栈分配内存。

```
local-variable-initializer:
    ...
    stackalloc-initializer

stackalloc-initializer:
    stackalloc unmanaged-type [ expression ]
```

unmanaged-type 表示将存储在新分配位置中的项目的类型，而 expression 表示这些项目的数量。两者合在一起指定了所需的分配大小。由于栈分配的大小不能为负，因此将项目数量指定为求值为负值的常量表达式是编译时错误。

形式为 stackalloc T[E] 的栈分配初始化器要求 T 为非托管类型 (§18.2)，E 为类型为 int 的表达式。该构造从调用栈分配 E * sizeof(T) 字节，并返回指向新分配块的指针，其类型为 T*。如果 E 为负值，则行为未定义。如果 E 为零，则不进行分配，且返回的指针由实现定义。如果没有足够的内存来分配给定大小的块，则会抛出 System.StackOverflowException。

新分配内存的内容是未定义的。

栈分配初始化器不允许在 catch 或 finally 块 (§8.10) 中使用。

分配的内存会在方法返回时自动丢弃。这对应于 alloca 函数，这是在 C 和 C++ 实现中常见的扩展。

在示例中

```csharp
using System;
class Test
{
    static string IntToString(int value) {
        int n = value >= 0? value: -value;
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

栈分配初始化器在 IntToString 方法中用于在栈上分配一个 16 个字符的缓冲区。缓冲区会在方法返回时自动丢弃。

## 18.9 动态内存分配

除 stackalloc 运算符外，C# 未提供用于管理非垃圾回收内存的预定义结构。此类服务通常由支持的类库提供，或直接从底层操作系统导入。例如，下面的 Memory 类说明了如何从 C# 访问底层操作系统的堆函数：

```csharp
using System;
using System.Runtime.InteropServices;
public unsafe class Memory
{
    // Handle for the process heap. This handle is used in all calls to the
    // HeapXXX APIs in the methods below.
    static int ph = GetProcessHeap();
    // Private instance constructor to prevent instantiation.
    private Memory() {}
    // Allocates a memory block of the given size. The allocated memory is
    // automatically initialized to zero.
    public static void* Alloc(int size) {
        void* result = HeapAlloc(ph, HEAP_ZERO_MEMORY, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }
    // Copies count bytes from src to dst. The source and destination
    // blocks are permitted to overlap.
    public static void Copy(void* src, void* dst, int count) {
        byte* ps = (byte*)src;
        byte* pd = (byte*)dst;
        if (ps > pd) {
            for (; count != 0; count--) *pd++ = *ps++;
        }
        else if (ps < pd) {
            for (ps += count, pd += count; count != 0; count--) *--pd = *--ps;
        }
    }
    // Frees a memory block.
    public static void Free(void* block) {
        if (!HeapFree(ph, 0, block)) throw new InvalidOperationException();
    }
    // Re-allocates a memory block. If the reallocation request is for a
    // larger size, the additional region of memory is automatically
    // initialized to zero.
    public static void* ReAlloc(void* block, int size) {
        void* result = HeapReAlloc(ph, HEAP_ZERO_MEMORY, block, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }
    // Returns the size of a memory block.
    public static int SizeOf(void* block) {
        int result = HeapSize(ph, 0, block);
        if (result == -1) throw new InvalidOperationException();
        return result;
    }
    // Heap flags
    const int HEAP_ZERO_MEMORY = 0x00000008;
    // Heap API functions
    [DllImport("kernel32")]
    static extern int GetProcessHeap();
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

使用 Memory 类的示例如下所示：

```
class Test
{
    static void Main() {
        unsafe {
            byte* buffer = (byte*)Memory.Alloc(256);
            try {
                for (int i = 0; i < 256; i++) buffer[i] = (byte)i;
                byte[] array = new byte[256];
                fixed (byte* p = array) Memory.Copy(buffer, p, 256);
            }
            finally {
                Memory.Free(buffer);
            }
        }
        for (int i = 0; i < 256; i++) Console.WriteLine(array[i]);
    }
}
```

该示例通过 Memory.Alloc 分配 256 字节的内存，并使用从 0 到 255 递增的值初始化内存块。然后它分配一个包含 256 个元素的字节数组，并使用 Memory.Copy 将内存块的内容复制到字节数组中。最后，使用 Memory.Free 释放内存块，并将字节数组的内容输出到控制台。

## A. 文档注释

C# 为程序员提供了一种机制，使用包含 XML 文本的特殊注释语法来记录代码。在源代码文件中，具有特定形式的注释可用于指示工具从这些注释和它们前面的源代码元素生成 XML。使用此类语法的注释称为文档注释。它们必须立即位于用户定义的类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。XML 生成工具称为文档生成器。（该生成器可以是，但不必是 C# 编译器本身。）文档生成器产生的输出称为文档文件。文档文件用作文档查看器的输入，文档查看器是一种旨在以某种方式可视化显示类型信息及其相关文档的工具。

本规范建议了一组可在文档注释中使用的标签，但使用这些标签不是必需的，如果需要，也可以使用其他标签，只要遵循良好的 XML 规则即可。

### A.1 引言

具有特殊形式的注释可用于指示工具从这些注释和它们前面的源代码元素生成 XML。此类注释是单行注释，以三个斜杠 (///) 开头，或定界注释，以斜杠和两个星号 (/**) 开头。它们必须立即位于它们注释的用户定义的类型（如类、委托或接口）或成员（如字段、事件、属性或方法）之前。属性部分 (§17.2) 被视为声明的一部分，因此文档注释必须位于应用于类型或成员的属性之前。

语法：

```
single-line-doc-comment:
    /// input-characters_opt

delimited-doc-comment:
    /** delimited-comment-text_opt */
```

在单行文档注释中，如果在当前单行文档注释相邻的每个单行文档注释的 /// 字符后都有一个空白字符，则该空白字符不会包含在 XML 输出中。

在定界文档注释中，如果第二行的第一个非空白字符是星号，并且在定界文档注释内的每一行开头都重复相同的可选空白字符和星号字符的模式，则重复模式的字符不会包含在 XML 输出中。该模式可能在星号字符之前以及之后包含空白字符。

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



文档注释中的文本必须根据 XML 规则（http://www.w3.org/TR/REC-xml）格式良好。如果 XML 格式不良，则会生成警告，并且文档文件中将包含一条注释，说明遇到了错误。

尽管开发者可以自由创建自己的标记集，但 §A.2 中定义了一组推荐的标记。其中一些推荐的标记具有特殊含义：

- `<param>` 标记用于描述参数。如果使用了此类标记，文档生成器必须验证指定的参数存在，并且所有参数都在文档注释中进行了描述。如果此类验证失败，文档生成器将发出警告。
- `cref` 属性可以附加到任何标记上，以提供对代码元素的引用。文档生成器必须验证此代码元素存在。如果验证失败，文档生成器将发出警告。在查找 `cref` 属性中描述的名称时，文档生成器必须根据源代码中出现的 `using` 语句遵循命名空间可见性。对于泛型代码元素，不能使用常规泛型语法（即“`List<T>`”），因为它会产生无效的 XML。可以使用花括号代替方括号（即“`List{T}`”），或者可以使用 XML 转义语法（即“`List&lt;T&gt;`”）。
- `<summary>` 标记旨在由文档查看器使用，以显示关于类型或成员的附加信息。
- `<include>` 标记包含来自外部 XML 文件的信息。

请仔细注意，文档文件不提供关于类型和成员的完整信息（例如，它不包含任何类型信息）。要获取关于类型或成员的此类信息，必须将文档文件与对实际类型或成员的反射结合使用。

## A.2 推荐的标记

文档生成器必须接受并处理任何根据 XML 规则有效的标记。以下标记提供了用户文档中常用的功能。（当然，其他标记也是可能的。）

| 标记 | 章节 | 用途 |
|---|---|---|
| <c> | A.2.1 | 以类似代码的字体设置文本 |
| <code> | A.2.2 | 设置一行或多行源代码或程序输出 |
| <example> | A.2.3 | 指示一个示例 |
| <exception> | A.2.4 | 标识方法可引发的异常 |
| <include> | A.2.5 | 包含来自外部文件的 XML |
| <list> | A.2.6 | 创建列表或表格 |
| <para> | A.2.7 | 允许向文本添加结构 |
| <param> | A.2.8 | 描述方法或构造函数的参数 |
| <paramref> | A.2.9 | 标识某个词是参数名 |
| <permission> | A.2.10 | 记录成员的安全可访问性 |
| <remark> | A.2.11 | 描述关于类型的附加信息 |
| <returns> | A.2.12 | 描述方法的返回值 |
| <see> | A.2.13 | 指定链接 |
| <seealso> | A.2.14 | 生成“另请参阅”条目 |
| <summary> | A.2.15 | 描述类型或类型的成员 |
| <value> | A.2.16 | 描述属性 |
| <typeparam> |  | 描述泛型类型参数 |
| <typeparamref> |  | 标识某个词是类型参数名 |

### A.2.1 <c>

此标记提供了一种机制，用于指示描述中的文本片段应使用特殊字体（例如用于代码块的字体）设置。对于实际代码行，请使用 <code>（§A.2.2）。

**语法：**

```
<c>text</c>
```

**示例：**

```
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
public class Point
{
    // ...
}
```

### A.2.2 <code>

此标记用于以某种特殊字体设置一行或多行源代码或程序输出。对于叙述中的小代码片段，请使用 <c>（§A.2.1）。

**语法：**

```
<code>source code or program output</code>
```

**示例：**

```
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// <example>For example:
/// <code>
/// Point p = new Point(3,5);
/// p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// </example>
/// </summary>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### A.2.3 <example>

此标记允许在注释中提供示例代码，以指定方法或其他库成员可以如何使用。通常，这还会涉及使用 <code> 标记（§A.2.2）。

**语法：**

```
<example>description</example>
```

**示例：**

有关示例，请参见 <code>（§A.2.2）。

### A.2.4 <exception>

此标记提供了一种记录方法可引发的异常的方式。

**语法：**

```
<exception cref="member">description</exception>
```

**其中**

**cref="member"**

成员的名称。文档生成器会检查给定成员是否存在，并将 member 转换为文档文件中的规范元素名称。

**description**

对引发异常的情况的描述。

**示例：**

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
        // ...
    }
}
```

### A.2.5 <include>

此标记允许包含来自源代码文件外部 XML 文档的信息。外部文件必须是格式良好的 XML 文档，并且会向该文档应用 XPath 表达式，以指定要从该文档中包含哪些 XML。然后，<include> 标记会被来自外部文档的选定 XML 替换。

**语法：**

```
<include file="filename" path="xpath" />
```

**其中**

**file="filename"**

外部 XML 文件的文件名。该文件名相对于包含 include 标记的文件进行解释。

**path="xpath"**

一个 XPath 表达式，用于选择外部 XML 文件中的某些 XML。

**示例：**

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

那么输出的文档将与源代码包含以下内容时相同：

```
/// <summary>
/// Contains a list of integers.
/// </summary>
public class IntList { ... }
```

### A.2.6 <list>

此标记用于创建项目列表或表格。它可以包含一个 <listheader> 块，用于定义表格或定义列表的标题行。（定义表格时，只需提供标题中 term 的条目。）

列表中的每一项都用 <item> 块指定。创建定义列表时，必须同时指定 term 和 description。但是，对于表格、项目符号列表或编号列表，只需指定 description。

**语法：**

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
  ...item
  <term>term</term>
  <description>description</description>
  </item>
</list>
```

**其中**

**term**

要定义的术语，其定义位于 description 中。

**description**

项目符号列表或编号列表中的一项，或者术语的定义。

**示例：**

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
}
```

### A.2.7 <para>

此标记用于其他标记内部，例如 <summary>（§A.2.11）或 <returns>（§A.2.12），并允许向文本添加结构。

**语法：**

```
<para>content</para>
```

**其中**

**content**

段落的文本。

**示例：**

```
/// <summary>This is the entry point of the Point class testing program.
/// <para>This program tests each method and operator, and
/// is intended to be run after any non-trivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // ...
}
```

## A.2.8 <param>

此标记用于描述方法、构造函数或索引器的参数。

语法：

```
<param name="name">description</param>
```

示例：

```
/// <summary>This method changes the point's location to
/// the given coordinates.</summary>
/// <param name="xor">the new x-coordinate.</param>
/// <param name="yor">the new y-coordinate.</param>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

## A.2.9 <paramref>

此标记用于指明某个词是一个参数。文档文件可以被处理，以某种不同的方式格式化该参数。

语法：

```
<paramref name="name"/>
```

示例：

```
/// <summary>This constructor initializes the new Point to
/// <paramref name="xor"/>,<paramref name="yor"/>.</summary>
/// <param name="xor">the new Point's x-coordinate.</param>
/// <param name="yor">the new Point's y-coordinate.</param>
public Point(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

## A.2.10 <permission>

此标记允许记录成员的访问安全性。

```
<permission cref="member">description</permission>
```

其中

`cref="member"`

成员的名称。文档生成器会检查给定的代码元素是否存在，并将 *成员* 转换为文档文件中的规范元素名称。

*描述*

对成员访问权限的描述。

**示例：**

```
/// <permission cref="System.Security.PermissionSet">Everyone can
/// access this method.</permission>
public static void Test() {
    // ...
}
```

### A.2.11 <remark>

此标记用于指定有关类型的额外信息。（使用 <summary>（§A.2.15）来描述类型本身及其成员。）

**语法：**

```
<remark>description</remark>
```

其中

*描述*

备注的文本。

**示例：**

```
/// <summary>Class <c>Point</c> models a point in a
/// two-dimensional plane.</summary>
/// <remark>Uses polar coordinates</remark>
public class Point
{
    // ...
}
```

### A.2.12 <returns>

此标记用于描述方法的返回值。

**语法：**

```
<returns>description</returns>
```

其中

*描述*

对返回值的描述。

**示例：**

```
/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y),
/// without any leading, trailing, or embedded whitespace.</returns>
public override string ToString() {
    return "(" + X + "," + Y + ")";
}
```

## A.2.13 <see>

此标记允许在文本中指定链接。使用 <seealso>（§A.2.14）指示要出现在“另请参阅”部分中的文本。

### 语法：

```
<see cref="member"/>
```

其中
cref="member"
成员的名称。文档生成器会检查给定的代码元素是否存在，并将成员更改为生成的文档文件中的元素名称。

### 示例：

```
/// <summary>This method changes the point's location to
/// the given coordinates.</summary>
/// <see cref="Translate"/>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.</summary>
/// <see cref="Move"/>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

## A.2.14 <seealso>

此标记允许为“另请参阅”部分生成条目。使用 <see>（§A.2.13）从文本中指定链接。

### 语法：

```
<seealso cref="member"/>
```

其中
cref="member"
成员的名称。文档生成器会检查给定的代码元素是否存在，并将成员更改为生成的文档文件中的元素名称。

### 示例：

```
/// <summary>This method determines whether two Points have the same
/// location.</summary>
/// <seealso cref="operator=="/>
/// <seealso cref="operator!="/>
public override bool Equals(object o) {
    // ...
}
```

## A.2.15 <summary>

此标记可用于描述类型或类型的成员。使用 <remark>（§A.2.11）来描述类型本身。

### 语法：

```
<summary>description</summary>
```

其中

描述

类型或成员的摘要。

### 示例：

```
/// <summary>This constructor initializes the new Point to (0,0).</summary>
public Point() : this(0,0) {
```

## A.2.16 <value>

此标记允许描述属性。

### 语法：

```
<value>property description</value>
```

其中

属性描述

对属性的描述。

### 示例：

```
/// <value>Property <c>X</c> represents the point's x-coordinate.</value>
public int X
{
    get { return x; }
    set { x = value; }
}
```

## A.2.17 <typeparam>

此标记用于描述类、结构、接口、委托或方法的泛型类型参数。

### 语法：

```
<typeparam name="name">description</typeparam>
```

其中

*名称*

类型参数的名称。

## A.2.18 <typeparamref>

此标记用于指明某个词是一个类型参数。文档文件可以被处理，以某种不同的方式格式化该类型参数。

### 示例：

```
// <summary>This method fetches data and returns a list of <typeparamref name="T" />...</summary>
// <param name="string">query to execute</param>
public List<T> FetchData<T>(string query) {
  ...
}
```

## A.3 处理文档文件

文档生成器为源代码中带有文档注释标记的每个元素生成一个 ID 字符串。该 ID 字符串唯一标识一个源代码元素。文档查看器可以使用 ID 字符串来识别文档所对应的元数据/反射项。

文档文件不是源代码的层次结构表示，而是一个扁平列表，其中每个元素都有一个生成的 ID 字符串。

### A.3.1 ID 字符串格式

文档生成器在生成 ID 字符串时遵循以下规则：

- 字符串中不包含空格。
- 字符串的第一部分通过一个字符后跟冒号来标识所记录成员的类型。定义了以下成员类型：

| 字符 | 描述 |
|---|---|
| E | 事件 |
| F | 字段 |
| M | 方法（包括构造函数、析构函数和运算符） |
| N | 命名空间 |
| P | 属性（包括索引器） |
| T | 类型（如类、委托、枚举、接口和结构） |
| ! | 错误字符串；字符串的其余部分提供有关错误的信息。例如，文档生成器会为无法解析的链接生成错误信息。 |

- 字符串的第二部分是元素的完全限定名称，从命名空间的根开始。元素名称、其包含类型和命名空间之间用句点分隔。如果元素名称本身包含句点，则这些句点将替换为 #（U+0023）字符。（假设没有元素的名称中包含此字符。）

- 对于带参数的方法和属性，参数列表跟在后面，并用括号括起来。对于不带参数的方法和属性，括号省略。参数之间用逗号分隔。每个参数的编码与 CLI 签名相同，如下所示：

- 参数由其文档名称表示，该名称基于其完全限定名称，并按如下方式修改：

表示泛型类型的参数会附加一个“`”字符，后跟类型参数的数目。

带有 out 或 ref 修饰符的参数在其类型名称后有一个 @。按值传递或通过 params 传递的参数没有特殊记号。

数组参数表示为 [ lowerbound : size , ... , lowerbound : size ]，其中逗号的数量为秩减一，每个维度的下界和大小（如果已知）以十进制表示。如果未指定下界或大小，则省略。如果某个维度的下界和大小都省略，则“:”也省略。交错数组按每层级一个“[]”表示。

非 void 类型的指针参数使用类型名称后跟 * 表示。void 指针使用类型名称 System.Void 表示。

引用类型上定义的泛型类型参数的参数使用“`”字符后跟该类型参数的从零开始的索引进行编码。

使用方法中定义的泛型类型参数的参数使用双反引号“``”，而不是类型所使用的“`”。

引用构造泛型类型的参数使用泛型类型后跟“{”，再跟逗号分隔的类型参数列表，最后跟“}”进行编码。

### A.3.2 ID 字符串示例

以下每个示例都展示了一段 C# 代码，以及每个能够具有文档注释的源代码元素生成的 ID 字符串：

- 类型使用其完全限定名称表示，并附加上泛型信息：

```csharp
enum Color { Red, Blue, Green }
namespace Acme
{
    interface IProcess {...}
    struct ValueType {...}
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
        private Widget[] array2;
        private unsafe int *pCount;
        private unsafe float **ppValues;
    }
}
```

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
```

- 构造函数。

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

```
"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor(System.String)"
```

- 析构函数。

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

- 方法。

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
        public static void M0() {...}
        public void M1(char c, out float f, ref ValueType v) {...}
        public void M2(short[] x1, int[,] x2, long[][,] x3) {...}
        public void M3(long[][] x3, Widget[][,] x4) {...}
        public unsafe void M4(char *pc, Color **pf) {...}
        public unsafe void M5(void *pv, double *[,] pd) {...}
        public void M6(int i, params object[] args) {...}
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
}
```

```
"M:Acme.ValueType.M(System.Int32)"
"M:Acme.Widget.NestedClass.M(System.Int32)"
"M:Acme.Widget.M0()"
"M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
"M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
"M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:,0:])"
"M:Acme.Widget.M4(System.Char*,Color**)"
"M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:])"
"M:Acme.Widget.M6(System.Int32,System.Object[])"
"M:Acme.MyList`1.Test(`0)"
"M:Acme.UseList.Process(Acme.MyList<System.Int32>)"
"M:Acme.UseList.GetValues`1(`0)"
```

- 属性和索引器。

```
namespace Acme
{
    class Widget: IProcess
    {
        public int width { get {...} set {...} }
        public int this[int i] { get {...} set {...} }
        public int this[string s, int i] { get {...} set {...} }
    }
}
```

```
"P:Acme.Widget.Width"
"P:Acme.Widget.Item(System.Int32)"
"P:Acme.Widget.Item(System.String,System.Int32)"
```

- 事件。

```
namespace Acme
{
    class Widget: IProcess
    {
        public event Del AnEvent;
    }
}
```

```
"E:Acme.Widget.AnEvent"
```

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

```
"M:Acme.Widget.op_UnaryPlus(Acme.Widget)"
```

所使用的一元运算符函数名的完整集合如下：op_UnaryPlus、op_UnaryNegation、op_LogicalNot、op_OnesComplement、op_Increment、op_Decrement、op_True 和 op_False。

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

```
"M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"
```

所使用的二元运算符函数名的完整集合如下：op_Addition、op_Subtraction、op_Multiply、op_Division、op_Modulus、op_BitwiseAnd、op_BitwiseOr、op_ExclusiveOr、op_LeftShift、op_RightShift、op_Equality、op_Inequality、op_LessThan、op_LessThanOrEqual、op_GreaterThan 和 op_GreaterThanOrEqual。

- 转换运算符带有一个尾随的 "~"，后跟返回类型。

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
"M:Acme.Widget.op_Explicit(Acme.Widget)~System.Int32"
"M:Acme.Widget.op_Implicit(Acme.Widget)~System.Int64"

## A.4 示例

### A.4.1 C# 源代码

以下示例展示了 Point 类的源代码：

```
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
        
        /// <summary>This constructor initializes the new Point to
        /// (0,0).</summary>
        public Point() : this(0,0) {}
        
        /// <summary>This constructor initializes the new Point to
        /// <paramref name="x"/><paramref name="y"/></summary>
        /// <param><c>x</c> is the new Point's x-coordinate.</param>
        /// <param><c>y</c> is the new Point's y-coordinate.</param>
        public Point(int x, int y) {
            X = x;
            Y = y;
        }
        
        /// <summary>This method changes the point's location to
        /// the given coordinates.</summary>
        /// <param><c>x</c> is the new x-coordinate.</param>
        /// <param><c>y</c> is the new y-coordinate.</param>
        /// <see cref="Translate"/>
        public void Move(int x, int y) {
            X = x;
            Y = y;
        }
        /// <summary>This method changes the point's location by
        /// the given x- and y-offsets.
        /// <example>For example:
        /// <code>
        Point p = new Point(3,5);
        p.Translate(-1,3);
        </code>
        /// results in <c>p</c>'s having the value (2,8).
        /// </example>
        /// </summary>
        /// <param><c>x</c> is the relative x-offset.</param>
        /// <param><c>y</c> is the relative y-offset.</param>
        /// <see cref="Move"/>
        public void Translate(int x, int y) {
            X += x;
            Y += y;
        }
        /// <summary>This method determines whether two Points have the same
        /// location.</summary>
        /// <param><c>o</c> is the object to be compared to the current object.</param>
        /// <returns>True if the Points have the same location and they have
        /// the exact same type; otherwise, false.</returns>
        /// <seealso cref="operator==" />
        /// <seealso cref="operator!="/>
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
        /// <returns>A string representing a point's location, in the form (x,y),
        /// without any leading, trailing, or embedded whitespace.</returns>
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
        /// <seealso cref="operator=="/>
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
        /// <seealso cref="operator=="/>
        public static bool operator!=(Point p1, Point p2) {
            return !(p1 == p2);
        }

        /// <summary>This is the entry point of the Point class testing
        /// program.</summary>
        /// <para>This program tests each method and operator, and
        /// is intended to be run after any non-trivial maintenance has
        /// been performed on the Point class.</para></summary>
        public static void Main() {
            // class test code goes here
        }
    }
}
```

### A.4.2 生成的 XML

以下是某个文档生成器在获得上面所示的 Point 类的源代码后生成的输出：

```
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
    <members>
        <member name="T:Graphics.Point">
            <summary>Class <c>Point</c> models a point in a two-dimensional
            plane.</summary>
        </member>
        <member name="F:Graphics.Point.X">
            <summary>Instance variable <c>x</c> represents the point's
            x-coordinate.</summary>
        </member>
```


<member name="F:Graphics.Point.y">
<summary>实例变量 <c>y</c> 表示点的 y 坐标。</summary>
</member>
<member name="M:Graphics.Point.#ctor">
<summary>此构造函数将新的 Point 初始化为 (0,0)。</summary>
</member>
<member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
<summary>此构造函数将新的 Point 初始化为（<paramref name="xor"/>,<paramref name="yor"/>）。</summary>
<param><c>xor</c> 是新 Point 的 x 坐标。</param>
<param><c>yor</c> 是新 Point 的 y 坐标。</param>
</member>
<member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
<summary>此方法将点的位置更改为给定坐标。</summary>
<param><c>xor</c> 是新的 x 坐标。</param>
<param><c>yor</c> 是新的 y 坐标。</param>
<see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
</member>
<member name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
<summary>此方法通过给定的 x 和 y 偏移量更改点的位置。
<example>例如：
<code>
Point p = new Point(3,5);
p.Translate(-1,3);
</code>
结果使 <c>p</c> 的值变为 (2,8)。
</example>
</summary>
<param><c>xor</c> 是相对 x 偏移量。</param>
<param><c>yor</c> 是相对 y 偏移量。</param>
<see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
</member>
<member name="M:Graphics.Point.Equals(System.Object)">
<summary>此方法确定两个 Points 是否具有相同的位置。</summary>
<param><c>o</c> 是要与当前对象进行比较的对象。</param>
<returns>如果 Points 具有相同的位置并且它们具有完全相同的类型，则为 True；否则为 false。</returns>
<seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.ToString">
<summary>以字符串形式报告点的位置。</summary>
<returns>表示点位置的字符串，形式为 (x,y)，不含任何前导、尾随或嵌入的空白。</returns>
</member>

<member name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
<summary>此运算符确定两个 Points 是否具有相同的位置。</summary>
<param><c>p1</c> 是要比较的第一个 Point。</param>
<param><c>p2</c> 是要比较的第二个 Point。</param>
<returns>如果 Points 具有相同的位置并且它们具有完全相同的类型，则为 True；否则为 false。</returns>
<seealso cref="M:Graphics.Point.Equals(System.Object)"/>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>

<member name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
<summary>此运算符确定两个 Points 是否具有相同的位置。</summary>
<param><c>p1</c> 是要比较的第一个 Point。</param>
<param><c>p2</c> 是要比较的第二个 Point。</param>
<returns>如果 Points 不具有相同的位置并且类型完全相同，则为 True；否则为 false。</returns>
<seealso cref="M:Graphics.Point.Equals(System.Object)"/>
<seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
</member>

<member name="M:Graphics.Point.Main">
<summary>这是 Point 类测试程序的入口点。
<para>此程序测试每个方法和运算符，旨在在对 Point 类进行任何非平凡维护后运行。</para></summary>
</member>

<member name="P:Graphics.Point.X">
<value>属性 <c>X</c> 表示点的 x 坐标。</value>
</member>

<member name="P:Graphics.Point.Y">
<value>属性 <c>Y</c> 表示点的 y 坐标。</value>
</member>

</members>
</doc>

## B. Grammar

本附录包含主文档中出现的词法和语法文法的摘要，以及不安全代码的文法扩展。文法产生式在此出现的顺序与它们在主文档中出现的顺序相同。

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

```
new-line:
    Carriage return character (U+000D)
    Line feed character (U+000A)
    Carriage return character (U+000D) followed by line feed character (U+000A)
    Next line character (U+0085)
    Line separator character (U+2028)
    Paragraph separator character (U+2029)
```

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
```

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

### B.1.3 空白

whitespace:
Any character with Unicode class Zs
Horizontal tab character (U+0009)
Vertical tab character (U+000B)
Form feed character (U+000C)

### B.1.4 标记

token:
identifier
keyword
integer-literal
real-literal
character-literal
string-literal
operator-or-punctuator

### B.1.5 Unicode 字符转义序列

unicode-escape-sequence:
\u hex-digit hex-digit hex-digit hex-digit
\U hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit hex-digit

### B.1.6 标识符

identifier:
available-identifier
@ identifier-or-keyword

available-identifier:
An identifier-or-keyword that is not a keyword

```
identifier-or-keyword:
    identifier-start-character identifier-part-characters_opt

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

### B.1.7 关键字

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

### B.1.8 字面量

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
  U u L l UL ul U l uL u l LU Lu lU l u

hexadecimal-integer-literal:
  0x hex-digits integer-type-suffix_opt
  0X hex-digits integer-type-suffix_opt

hex-digits:
  hex-digit
  hex-digits hex-digit

hex-digit: one of
  0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f

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
```


character-literal:
' character '

character:
single-character
simple-escape-sequence
hexadecimal-escape-sequence
unicode-escape-sequence

single-character:
除 ' (U+0027)、\ (U+005C) 和换行字符之外的任何字符

simple-escape-sequence: 以下之一
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

regular-string-literal-character:
single-regular-string-literal-character
simple-escape-sequence
hexadecimal-escape-sequence
unicode-escape-sequence

single-regular-string-literal-character:
除 " (U+0022)、\ (U+005C) 和换行字符之外的任何字符

verbatim-string-literal:
@" verbatim-string-literal-characters_opt "

verbatim-string-literal-characters:
verbatim-string-literal-character
verbatim-string-literal-characters verbatim-string-literal-character

verbatim-string-literal-character:
single-verbatim-string-literal-character
quote-escape-sequence

single-verbatim-string-literal-character:
除 " 之外的任何字符

quote-escape-sequence:
""

null-literal:
null

## B.1.9 运算符和标点符号

operator-or-punctuator: 以下之一
{ } [ ] ( ) . , : ;
+ - * / % & | ^ ! ~
= < > ? ?? :: ++ -- && ||
-> == != <= >= += -= *= /= %=
&= |= ^= << <<= =>

right-shift:
>>

right-shift-assignment:
>>=

## B.1.10 预处理指令

pp-directive:
pp-declaration
pp-conditional
pp-line
pp-diagnostic
pp-region
pp-pragma

conditional-symbol:
除 true 或 false 之外的任何标识符或关键字

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

## C# 语言规范

```
pp-new-line:
    whitespace_opt single-line-comment_opt new-line

pp-conditional:
    pp-if-section pp-elif-sections_opt pp-else-section_opt pp-endif

pp-if-section:
    whitespace_opt # whitespace_opt if whitespace pp-expression pp-new-line conditional-section_opt

pp-elif-sections:
    pp-elif-section
    pp-elif-sections pp-elif-section

pp-elif-section:
    whitespace_opt # whitespace_opt elif whitespace pp-expression pp-new-line conditional-section_opt

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
```

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
pp-pragma:
    whitespace_opt # whitespace_opt pragma whitespace pragma-body pp-new-line
pragma-body:
    pragma-warning-body
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

## B.2 语法文法

### B.2.1 基本概念

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

### B.2.2 类型

```
type:
    value-type
    reference-type
    type-parameter
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

variable-reference:
    expression

### B.2.4 表达式

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
member-access:
primary-expression . identifier type-argument-list_opt
predefined-type . identifier type-argument-list_opt
qualified-alias-member . identifier
predefined-type: 以下之一
bool byte char decimal double float int long
object sbyte short string uint ulong ushort
invocation-expression:
primary-expression ( argument-list_opt )
element-access:
primary-no-array-creation-expression [ argument-list ]
this-access:
this
base-access:
base . identifier
base [ argument-list ]
post-increment-expression:
primary-expression ++
post-decrement-expression:
primary-expression --
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
member-declarator:
    simple-name
    member-access
    identifier = expression


typeof表达式:
    typeof ( 类型 )
    typeof ( 未绑定类型名 )
    typeof ( void )

未绑定类型名:
    标识符 通用维度说明符_opt
    标识符 :: 标识符 通用维度说明符_opt
    未绑定类型名 . 标识符 通用维度说明符_opt

通用维度说明符:
    < 逗号_opt >

逗号:
    ,
    逗号 ,

checked表达式:
    checked ( 表达式 )

unchecked表达式:
    unchecked ( 表达式 )

默认值表达式:
    default ( 类型 )

一元表达式:
    主表达式
    + 一元表达式
    - 一元表达式
    ! 一元表达式
    ~ 一元表达式
    前缀递增表达式
    前缀递减表达式
    强制转换表达式

前缀递增表达式:
    ++ 一元表达式

前缀递减表达式:
    -- 一元表达式

强制转换表达式:
    ( 类型 ) 一元表达式

乘法表达式:
    一元表达式
    乘法表达式 * 一元表达式
    乘法表达式 / 一元表达式
    乘法表达式 % 一元表达式

加法表达式:
    乘法表达式
    加法表达式 + 乘法表达式
    加法表达式 - 乘法表达式

移位表达式:
    加法表达式
    移位表达式 << 加法表达式
    移位表达式 右移 加法表达式

关系表达式:
    移位表达式
    关系表达式 < 移位表达式
    关系表达式 > 移位表达式
    关系表达式 <= 移位表达式
    关系表达式 >= 移位表达式
    关系表达式 is 类型
    关系表达式 as 类型

相等表达式:
    关系表达式
    相等表达式 == 关系表达式
    相等表达式 != 关系表达式

与表达式:
    相等表达式
    与表达式 & 相等表达式

异或表达式:
    与表达式
    异或表达式 ^ 与表达式

包含或表达式:
    异或表达式
    包含或表达式 | 异或表达式

条件与表达式:
    包含或表达式
    条件与表达式 && 包含或表达式

条件或表达式:
    条件与表达式
    条件或表达式 || 条件与表达式

空合并表达式:
    条件或表达式
    条件或表达式 ?? 空合并表达式

条件表达式:
    空合并表达式
    空合并表达式 ? 表达式 : 表达式

lambda表达式:
    匿名函数签名 => 匿名函数体

匿名方法表达式:
    delegate 显式匿名函数签名_opt 块

匿名函数签名:
    显式匿名函数签名
    隐式匿名函数签名

显式匿名函数签名:
    ( 显式匿名函数参数列表_opt )

显式匿名函数参数列表:
    显式匿名函数参数
    显式匿名函数参数列表 , 显式匿名函数参数

显式匿名函数参数:
    匿名函数参数修饰符_opt 类型 标识符

匿名函数参数修饰符:
    ref
    out

隐式匿名函数签名:
    ( 隐式匿名函数参数列表_opt )

隐式匿名函数参数:
    隐式匿名函数参数

隐式匿名函数参数列表:
    隐式匿名函数参数
    隐式匿名函数参数列表 , 隐式匿名函数参数

隐式匿名函数参数:
    标识符

匿名函数体:
    表达式
    块

查询表达式:
    from子句 查询主体

from子句:
    from 类型_opt 标识符 in 表达式

查询主体:
    查询主体子句_opt 选择或分组子句 查询延续_opt

查询主体子句:
    查询主体子句
    查询主体子句 查询主体子句

查询主体子句:
    from子句
    let子句
    where子句
    join子句
    join-into子句
    orderby子句

let子句:
    let 标识符 = 表达式

where子句:
    where 布尔表达式

join子句:
    join 类型_opt 标识符 in 表达式 on 表达式 equals 表达式

join-into子句:
    join 类型_opt 标识符 in 表达式 on 表达式 equals 表达式 into 标识符
orderby子句:
    orderby 排序
排序:
    排序项
    排序 , 排序项
排序项:
    表达式 排序方向_opt
排序方向:
    升序
    降序
选择或分组子句:
    select子句
    group子句
select子句:
    select 表达式
group子句:
    group 表达式 by 表达式
查询延续:
    into 标识符 查询主体
赋值:
    一元表达式 赋值运算符 表达式
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

## B.2.5 语句
布尔表达式:
    表达式

语句:
    标签语句
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

标签语句:
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
    调用表达式
    对象创建表达式
    赋值
    后缀递增表达式
    后缀递减表达式
    前缀递增表达式
    前缀递减表达式
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

## C# 语言规范
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
    for ( for初始化_opt ; for条件_opt ; for迭代_opt ) 嵌入语句

for初始化:
    局部变量声明
    语句表达式列表

for条件:
    布尔表达式

for迭代:
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

## B.2.6 命名空间

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

## B.2.7 类

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
class-body:
    { class-member-declarations_opt }
class-member-declarations:
    class-member-declaration
    class-member-declarations class-member-declaration

## C# 语言规范

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
    attributes_opt method-modifiers_opt partial_opt return-type member-name type-parameter-list_opt
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
    type operator overloadable-unary-operator ( type identifier )

overloadable-unary-operator: one of
    +  -  !  ~  ++  --  true  false

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

### B.2.8 结构体

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

### B.2.9 数组

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

### B.2.10 接口

```
interface-declaration:
  attributes_opt interface-modifiers_opt partial_opt interface
  identifier variant-type-parameter-list_opt interface-base_opt
  type-parameter-constraints-clauses_opt interface-body ;_opt

interface-modifiers:
  interface-modifier
  interface-modifiers interface-modifier
```

```csharp
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
```

### B.2.12 委托

```csharp
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
```

### B.2.13 属性

```csharp
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
```

```
global-attribute-target:
    assembly
    module

attributes:
    attribute-sections

attribute-sections:
    attribute-section
    attribute-sections   attribute-section

attribute-section:
    [   attribute-target-specifier_opt   attribute-list  ]
    [   attribute-target-specifier_opt   attribute-list  ,  ]

attribute-target-specifier:
    attribute-target  :

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
    attribute-list  ,  attribute

attribute:
    attribute-name  attribute-arguments_opt

attribute-name:
    type-name

attribute-arguments:
    ( positional-argument-list_opt )
    ( positional-argument-list  ,  named-argument-list )
    ( named-argument-list )

positional-argument-list:
    positional-argument
    positional-argument-list  ,  positional-argument

positional-argument:
    argument-name_opt  attribute-argument-expression

named-argument-list:
    named-argument
    named-argument-list  ,  named-argument

named-argument:
    identifier  =  attribute-argument-expression

attribute-argument-expression:
    expression
```

### B.3 不安全代码的语法扩展

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
```

```
    event-modifier:
        ...
        unsafe
```

```
    indexer-modifier:
        ...
        unsafe
```

```
    operator-modifier:
        ...
        unsafe
```

```
    constructor-modifier:
        ...
        unsafe
```

```
    destructor-declaration:
        attributes_opt extern_opt unsafe_opt ~ identifier ( ) destructor-body
        attributes_opt unsafe_opt extern_opt ~ identifier ( ) destructor-body
```

```
    static-constructor-modifiers:
        extern_opt unsafe_opt static
        unsafe_opt extern_opt static
        extern_opt static unsafe_opt
        unsafe_opt static extern_opt
        static extern_opt unsafe_opt
        static unsafe_opt extern_opt
```

```
embedded-statement:
    ...
    unsafe-statement
    fixed-statement

unsafe-statement:
    unsafe block

type:
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
    sizeof-expression

unary-expression:
    ...
    pointer-indirection-expression
    addressof-expression

pointer-indirection-expression:
    * unary-expression

pointer-member-access:
    primary-expression -> identifier

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

fixed-pointer-initializer:
    & variable-reference
    expression
```

```
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
    fixed-size-buffer-declarator fixed-size-buffer-declarators
fixed-size-buffer-declarator:
    identifier [ constant-expression ]
local-variable-initializer:
    ...
    stackalloc-initializer
stackalloc-initializer:
    stackalloc unmanaged-type [ expression ]
```

## C. 参考文献

Unicode Consortium. *Unicode 标准，版本 3.0.* Addison-Wesley, Reading, Massachusetts, 2000, ISBN 0-201-616335-5.

IEEE. *IEEE 二进制浮点算术标准.* ANSI/IEEE 标准 754-1985。可从 http://www.ieee.org 获取。

ISO/IEC. *C++.* ANSI/ISO/IEC 14882:1998.
