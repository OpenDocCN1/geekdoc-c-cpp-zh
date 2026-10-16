
```
class DerivedClass: BaseClass
{
    public DerivedClass(BaseClass base)
    {
        // 从 Base 实例初始化对象
    }
    // 等等
```

### 装箱和拆箱强制转换

前面的讨论集中在基类和派生类之间的强制转换，其中双方都是引用类型。类似的原理也适用于值类型的强制转换，尽管这种情况下不可能简单地复制引用——必须发生一些数据复制。

当然，不可能从结构或原始值类型进行派生。基类和派生结构之间的强制转换，总是意味着在原始类型或结构与 `System.Object` 之间进行强制转换。（理论上，在结构和 `System.ValueType` 之间进行强制转换是可能的，虽然很难看出你为什么会想要这样做。）

从任何结构（或原始类型）到 `object` 的强制转换总是可以作为隐式强制转换使用——因为它是从派生类型到基类型的强制转换——并且这正是我们熟悉的装箱过程。例如，使用 `Currency` 结构：

```
var balance = new Currency(40,0);
object baseCopy = balance;
```

当执行这个隐式强制转换时，`balance` 的内容会被复制到堆上一个已装箱的对象中，`baseCopy` 对象引用会设置为指向该对象。在幕后实际发生的事情是这样：当你最初定义 `Currency` 结构时，.NET 框架隐式地提供了另一个（隐藏的）类，一个装箱的 `Currency` 类，它包含与 `Currency` 结构相同的字段，但它是存储在堆上的引用类型。每当你定义值类型（无论是结构还是枚举）时都会发生这种情况，并且对应于 `int`、`double`、`uint` 等所有原始值类型的类似装箱引用类型也存在。在源代码中无法也不必直接以编程方式访问这些装箱类中的任何一个，但每当值类型被强制转换为 `object` 时，它们就是在幕后工作的对象。当你隐式地将 `Currency` 强制转换为 `object` 时，会实例化一个装箱的 `Currency` 实例，并用 `Currency` 结构中的所有数据对其初始化。在前面的代码中，`baseCopy` 引用的正是这个装箱的 `Currency` 实例。通过这种方式，从派生类型到基类型的强制转换在语法上就可以对值类型和引用类型以相同的方式工作。

反向的强制转换称为拆箱。与基引用类型和派生引用类型之间的强制转换一样，它是显式强制转换，因为如果被转换的对象类型不正确，就会抛出异常：

```
object derivedObject = new Currency(40,0);
```

```csharp
object baseObject = new object();
Currency derivedCopy1 = (Currency)derivedObject;    // OK
Currency derivedCopy2 = (Currency)baseObject;       // Exception thrown
```

这段代码的工作方式与前面为引用类型展示的代码类似。将 `derivedObject` 强制转换为 `Currency` 之所以可行，是因为 `derivedObject` 实际上引用的是一个已装箱的 `Currency` 实例——该转换通过将字段从已装箱的 `Currency` 对象复制到一个新的 `Currency` 结构体中来执行。第二次转换失败，因为 `baseObject` 并不引用已装箱的 `Currency` 对象。

在使用装箱和取消装箱时，务必理解这两个过程实际上都会将数据复制到新的已装箱或已取消装箱的对象中。因此，例如对已装箱对象进行操作，并不会影响原始值类型的内容。

### 多重转换

在定义转换时，你需要注意一点：如果 C# 编译器遇到没有直接转换可执行所需转换的情况，它会尝试寻找组合转换的方式来完成转换。例如，对于 `Currency` 结构体，假设编译器遇到这样几行代码：

```csharp
var balance = new Currency(10,50);
long amount = (long)balance;
double amountD = balance;
```

你首先初始化了一个 `Currency` 实例，然后尝试将其转换为 `long`。问题在于你并没有定义执行该转换的强制转换。然而，这段代码仍然可以成功编译。其过程如下：编译器意识到你已经定义了一个从 `Currency` 到 `float` 的隐式转换，并且编译器已经知道如何将 `float` 显式转换为 `long`。因此，它会将该行代码编译成 IL 代码，先把 `balance` 转换为 `float`，再把结果转换为 `long`。代码的最后一行也是如此，将 `balance` 转换为 `double`。不过，由于从 `Currency` 到 `float` 的转换以及从 `float` 到 `double` 的预定义转换都是隐式的，你可以在代码中将此转换写成隐式转换。如果你愿意，也可以显式指定转换路径：

```csharp
var balance = new Currency(10,50);
long amount = (long)(float)balance;
double amountD = (double)(float)balance;
```

然而，在大多数情况下，这会被视为不必要地使代码复杂化。相比之下，以下代码会产生编译错误：

```csharp
var balance = new Currency(10,50);
long amount = balance;
```

原因是编译器能够找到的最佳转换匹配仍然是先转换为 `float`，然后再转换为 `long`。不过，从 `float` 到 `long` 的转换必须显式指定。

这些规则本身并不会给你带来太多麻烦。毕竟，这些规则相当直观，其设计目的是防止在开发者不知情的情况下发生任何数据丢失。然而，问题在于，如果你在定义转换时不够小心，编译器有可能选择一条导致意外结果的路径。例如，假设编写 `Currency` 结构体的团队中有其他人想到，能够将包含金额总美分数（以美分为单位，而不是以美元为单位，因为这样做的目的是不丢失美元的分数部分）的 `uint` 转换为 `Currency` 将会很有用。于是，可能会编写这样的转换来实现这个目的：

```csharp
// 不要这样做！
public static implicit operator Currency (uint value) =>
    new Currency(value/100u, (ushort)(value%100));
```

注意这段代码中第一个 100 后面的 `u`，这是为了确保 `value/100u` 被解释为 `uint`。如果你写成 `value/100`，编译器会将其解释为 `int`，而不是 `uint`。

代码中明确标注了注释 `不要这样做！`，原因如下：下面的代码片段仅仅是将一个包含 350 的 `uint` 转换为 `Currency`，然后再转换回来；但你认为执行完这段代码后，`bal2` 会包含什么值呢？

```csharp
uint bal = 350;
Currency balance = bal;
uint bal2 = (uint)balance;
```

答案不是 350，而是 3！而且这一切都符合逻辑。你将 350 隐式转换为 `Currency`，得到结果 `balance.Dollars = 3, balance.Cents = 50`。然后编译器像往常一样，找出最佳路径进行回转。`balance` 最终被隐式转换为 `float`（值 3.5），再被显式转换为值为 3 的 `uint`。

当然，还存在其他将一种数据类型转换再转回导致数据丢失的情况。例如，将一个包含 5.8 的 `float` 转换为 `int`，再转回 `float`，会丢失小数部分，得到结果 5。但丢失一个数字的小数部分与将一个整数除以 100 多，在原则上是略有不同的。`Currency` 突然变成了一个相当危险的类，会对整数做一些奇怪的事情！

问题在于，你的转换在解释整数时存在冲突。`Currency` 与 `float` 之间的转换将整数 1 解释为对应 1 美元，但最新的 `uint` 到 `Currency` 的转换却将该值解释为 1 美分。这是一个设计极差的例子。如果你希望自己的类易于使用，就应该确保所有转换的行为相互兼容，即它们直觉上给出相同的结果。在这种情况下，解决方案显然就是重写 `uint` 到 `Currency` 的转换，使其将整数 1 解释为 1 美元：

```csharp
public static implicit operator Currency (uint value) =>
    new Currency(value, 0);
```

顺便提一下，你可能会想这个新转换是否真的有必要。答案是它可能很有用。如果没有这个转换，编译器执行 `uint` 到 `Currency` 转换的唯一方式就是通过 `float`。在这种情况下，直接转换效率要高得多，因此添加这个额外的转换可以带来性能上的好处，不过你需要确保它与通过 `float` 转换得到的结果一致，而你现在已经做到了。在其他情况下，你可能还会发现为不同的预定义数据类型单独定义转换，可以使更多的转换成为隐式转换而不是显式转换，虽然这里的情况并非如此。

一个检验你的转换是否兼容的好方法是，询问一次转换是否会给出相同的结果（除了像 `float` 到 `int` 转换中可能出现的精度损失），而不管它走的是哪条路径。`Currency` 类为此提供了一个很好的例子。考虑以下代码：

```csharp
var balance = new Currency(50, 35);
ulong bal = (ulong) balance;
```

目前，编译器只有一种方法可以完成此转换：先将 `Currency` 隐式转换为 `float`，然后将其显式转换为 `ulong`。`float` 到 `ulong` 的转换需要显式转换，但这没关系，因为你已经在这里指定了显式转换。

然而，假设你随后又添加了一个转换，即从 `Currency` 隐式转换为 `uint`。实际上，你需要通过修改 `Currency` 结构体，添加上下文所展示的双向转换（代码文件 `CastingSample/Currency.cs`）：

```csharp
public static implicit operator Currency (uint value) =>
    new Currency(value, 0);

public static implicit operator uint (Currency value) =>
    value.Dollars;
```

现在编译器有了另一条从 `Currency` 转换为 `ulong` 的可能路径：先从 `Currency` 隐式转换为 `uint`，然后隐式转换为 `ulong`。它会选择这两条路径中的哪一条呢？C# 对于编译器在存在多种可能性时选择最佳路径有一些精确的规则。（本书不涉及这些规则，但如果你对细节感兴趣，可以参阅 MSDN 文档。）最好的答案是，你应该设计你的转换，使所有路径都给出相同的结果（除了可能的精度损失），这样编译器选择哪一条路径并不重要。（在本例中，编译器会选择 `Currency` → `uint` → `ulong` 路径，而不是 `Currency` → `float` → `ulong`。）

为了测试将 `Currency` 转换为 `uint`，请将以下测试代码添加到 `Main` 方法中（代码文件 `CastingSample/Program.cs`）：

```csharp
static void Main()
{
    try
    {
        var balance = new Currency(50,35);

        WriteLine(balance);
        WriteLine($"balance is {balance}");

        uint balance3 = (uint) balance;

        WriteLine($"Converting to uint gives {balance3}");
    }
    catch (Exception ex)
    {
        WriteLine($"Exception occurred: {ex.Message}");
    }
}
```

运行示例现在会得到以下结果：

```
50
balance is $50.35
Converting to uint gives 50
```

输出显示转换到 `uint` 已成功，不过正如预期的那样，在进行此转换时你已丢失了 `Currency` 的分部分。将负浮点数转换为 `Currency` 也产生了预期的溢出异常，因为 `float` 到 `Currency` 的转换本身现在定义了一个已检查的上下文。

然而，输出也展示了你在处理转换时需要意识到的最后一个潜在问题。输出的第一行并没有正确显示余额，显示的是 50 而不是 50.35。

发生了什么？问题在于当你将转换与方法重载结合使用时，你会得到另一个不可预测性的来源。

使用格式字符串的 `WriteLine` 语句会隐式调用 `Currency.ToString` 方法，确保 `Currency` 以字符串形式显示。

然而，第一个 `WriteLine` 方法只是将原始 `Currency` 结构体传递给 `WriteLine`。现在，`WriteLine` 有许多重载，但其中没有一个接受 `Currency` 结构体。因此，编译器开始寻找它可以将 `Currency` 转换为什么类型以使其匹配 `WriteLine` 的某个重载。碰巧的是，`WriteLine` 的其中一个重载是为快速高效地显示 `uint` 而设计的，并且它接受 `uint` 作为参数——你现在提供了一个将 `Currency` 隐式转换为 `uint` 的转换。

事实上，`WriteLine` 还有另一个重载接受 `double` 作为参数并显示该 `double` 的值。如果你仔细查看之前运行示例的输出，其中不存在转换到 `uint`，你会看到第一行输出将 `Currency` 显示为 `double`，使用了这个重载。在那个示例中，没有从 `Currency` 到 `uint` 的直接转换，所以编译器选择 `Currency` 到 `float` 再到 `double` 作为其匹配可用转换到可用 `WriteLine` 重载的首选方式。然而，现在在 `SimpleCurrency2` 中存在直接转换到 `uint`，编译器选择了这条路径。

由此得出的结论是，如果你有一个具有多个重载的方法调用，并且你尝试传递一个数据类型与任何重载都不完全匹配的参数，那么你就迫使编译器不仅决定使用什么转换来执行数据转换，还要决定选择哪个重载，以及因此选择哪种数据转换。编译器总是按逻辑并根据严格规则工作，但结果可能不是你所期望的。如果有任何疑问，你最好明确指定要使用的转换。

### Summary

本章介绍了 C# 提供的标准运算符，描述了对象相等性的机制，并检查了编译器如何将标准数据类型从一种转换为另一种。它还演示了如何使用运算符重载在你的数据类型上实现自定义运算符支持。最后，你研究了一种特殊的运算符重载类型，即转换运算符，它使你能够指定如何将你的类型的实例转换为其他数据类型。

下一章将解释委托、lambda 表达式和事件。

### 9 Delegates, Lambdas, and Events

#### What’s In This Chapter?

- Delegates
- Lambda expressions
- Closures
- Events
- Weak Events

#### Wrox.com Code Downloads for This Chapter

本章在 `www.wrox.com/go/professionalcsharp6` 的 Download Code 标签下可以找到 wrox.com 代码下载。本章的代码分为以下主要示例：

- Simple Delegates
- Bubble Sorter
- Lambda Expressions
- Events Sample
- Weak Events

#### Referencing Methods

委托是 .NET 中指向方法的地址的变体。将其与 C++ 相比，在 C++ 中，函数指针只不过是指向内存位置的指针，而且不是类型安全的。你不知道指针到底指向什么，诸如参数和返回类型等项目是未知的。这与 .NET 完全不同；委托是类型安全的类，定义了返回类型和参数类型。委托类不仅包含对方法的引用，还可以保存对多个方法的引用。

Lambda 表达式与委托直接相关。当参数是委托类型时，你可以使用 lambda 表达式来实现从委托引用的方法。

本章解释了委托和 lambda 表达式的基础知识，并展示了如何使用 lambda 表达式实现由委托调用的方法。它还演示了 .NET 如何使用委托作为实现事件的手段。

#### Delegates

委托适用于你想要将方法传递给其他方法的情况。要了解这意味着什么，请考虑这行代码：

```
int i = int.Parse("99");
```

你已经习惯于将数据作为参数传递给方法，就像这个例子一样，以至于你不会有意识地思考它，所以将方法而不是数据传递的想法可能听起来有点奇怪。然而，有时你有一个执行某些操作的方法，而不是对数据进行操作，该方法可能需要执行某些涉及调用另一个方法的操作。更复杂的是，你在编译时并不知道这个第二方法是什么。该信息只有在运行时才可用，因此需要作为参数传递给第一个方法。这听起来可能令人困惑，但通过几个例子应该会变得更清晰：

- **Threads and tasks**—在 C# 中，可以让计算机在并行于当前正在执行的操作的同时启动一个新的执行序列。这种序列被称为 *thread*，你使用 `System.Threading.Thread` 基类之一实例上的 `Start` 方法来启动它。如果你告诉计算机启动一个新的执行序列，你必须告诉它从哪里开始该序列；也就是说，你必须提供一个方法在其中可以开始执行的细节。换句话说，`Thread` 类的构造函数接受一个参数，该参数定义了线程将调用的方法。
