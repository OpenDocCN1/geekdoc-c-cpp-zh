

那是我们为让 C# 编译器满意所做的许多工作。

首先，我们必须把这个静态方法包装在一个类中，因为方法不能脱离类单独存在，而且我们必须经历这些繁琐的步骤来在方法中声明类型，并在类型没有完全吻合时修复它们。我保证，随着你使用 C#，对类型的关注会变得自然而然。到了某个阶段，你会在不思考的情况下就理清所有类型。但第一次经历这些繁琐步骤教会了我们关于 C# 和类型的一般性观点。

## Chapter 4 Static Typing & Built-in Types

我们刚刚了解到 C# 对类型很挑剔。它希望在开始前就知道一切的类型，变量、方法的参数、返回值。并非所有语言都这样工作。例如，如果你把这个方法转换成 JavaScript，它非常相似。

```
C#
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    float temperatureCelsius = (temperatureFahrenheit - 32) / 1.8f;
    return temperatureCelsius;
}
```

```
JavaScript
function FahrenheitToCelsius(temperatureFahrenheit)
{
    temperatureCelsius = (temperatureFahrenheit - 32) / 1.8;
    return temperatureCelsius;
}
```

几乎只有细微差别。但如果你标记出这些差异，你会发现它们大多与类型有关。像 JavaScript 这样不需要声明类型的语言被称为动态类型语言。而像 C# 这样必须声明类型的语言被称为静态类型语言。你也可以简称为静态和动态。哪一个更好，静态类型还是动态类型？这是编程界的争论，我将谨慎避开这个争论，因为我认为这取决于你想做什么。动态和静态语言在各自的方式上都有用。然而，我们已经

数字。我们已经提到过常规的 int，但 C# 还有许多对同一概念的变体。

| Type | Size and range |
|---|---|
| sbyte | 8 bits (from -128 to 127) |
| short | 16 bits (from -32,768 to 32,767) |
| int | 32 bits (from -2,147,483,648 to 2,147,483,647) |
| long | 64 bits (from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807) |

long 就像范围更大的 int，而 short 的范围更小，但占用内存更少。最后，sbyte，即有符号字节，是最小的，只有 8 位长。然后还有所有这些类型的无符号版本，只能包含正数：byte、ushort 表示无符号 short、uint 和 ulong。

| Type | Size and range |
|---|---|
| byte | 8 bits (from 0 to 255) |
| ushort | 16 bits (from 0 to 65,535) |
| uint | 32 bits (from 0 to 4,294,967,295) |
| ulong | 64 bits (from 0 to 18,446,744,073,709,551,615) |

为了更全面，还有两种原生的整数类型，称为 nint 表示原生 int 和 nuint 表示原生无符号 int，它们的尺寸取决于你运行的平台。它们仅在非常特殊的情况下才有用，比如编程。

| Type | Size |
|---|---|
| nint | It depends on the platform. |
| nuint | It depends on the platform. |

选择如此之多，你可能会感到不知所措，但事情是这样的，不必太担心选择正确的类型。通常当你选择变量的类型时，内存不是大问题，所以在大多数情况下，如果数字不是太大，你就使用 int，如果你有理由认为数字可能会超过 20 亿左右，那么你就选择 long。其他类型留给特殊情况，比如当你需要表示本质上是 8 位的东西时使用 byte。然后还有十进制类型，我们的选择更少。有我们已经提到的两种浮点类型 float 和 double，还有 decimal 是一种定点类型，这意味着本质上它是那些你不想近似而应为精确数字的数字的最佳选择。经典的例子是金钱。如果你做金钱计算，最后得到 99.99999 等奇怪的近似值，等等，分，这很可能是因为你应该对金钱使用 decimal 而不是 float 或 double。

| Type | Size and range |
|---|---|
| float | 32 bits, floating point (~6-9 digits) |
| double | 64 bits, floating point (~15-17 digits) |
| decimal | 128 bits, fixed point (from ±1.0 x 10⁻²⁸ to ±7.9228 x 10²⁸) |

最后，还有其他基本类型：字符串，即字符序列；字符，即单个 Unicode 字符；

和布尔值，即布尔值，只能为 true 或 false。
到此为止，我们已经对 C# 中的所有基本类型做了表面上的介绍。

![](img/0155736aec718cf18821e9f10a5d308d_471_0.png)

没有了。然而，C# 中还有更多类型，只是它们不是基本类型。事实上，C# 中有无限多种类型，因为你可以创建自己的类型，而这正是编程的全部内容。但我承诺过在这本书中我们不会过多谈论编程，所以只要知道就语言类型而言，当谈到这个世界时，你刚刚看到了整个列表。

```
```csharp
string[] interestingAnimals;
```
```

所以，这个变量是一个字符串数组。这是 C# 中声明字符串数组的语法，与许多其他语言中的数组类似。你也可以有任何其他类型的数组。让我们为这个数组赋值，像这样。大括号表示数组，在这种情况下，其中的值必须是字符串并用逗号分隔。

```
```csharp
string[] interestingAnimals = { "Aardvark", "Binturong", "Pangolin" };
```
```

不要忘记末尾的分号。稍后，我们可以用这种语法引用此数组中的元素，即单个字符串，方括号和索引。遵循编程传统，数组的索引从 0 开始，所以这是第一个元素，这是第二个，这是第三个。

```
```csharp
string[] interestingAnimals = { "Aardvark", "Binturong", "Pangolin" };
string anInterestingAnimal = interestingAnimals[0];
```
```

这就是你需要了解数组的全部内容。我们终于可以回到大本营，回到“Hello World！”，看看我们已经理解了多少。

## Chapter 6 Back to the Base Camp

终于，我们回到了我们开始的地方，基本的 Hello World 程序。所以我们又回来了。我移除了我们复制到这里的另一个方法，现在它又只是基本的 Hello World。

```
```csharp
using System;

namespace MyFirstProgram
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World");
        }
    }
}
```
```

让我们看看我们现在理解了这个程序的多少。这不是对你知识的测试。我们还没有完全解释一些东西，所以你可能需要做一些猜测或依赖你从其他编程语言获得的知识，但仍然，如果你愿意，这将是一个有趣的练习。你知道 Console.WriteLine 吗。WriteLine 是一个静态方法。定义在名为 Console 的这个类上的静态方法。实际上，如果我们用鼠标指针悬停在 WriteLine 上，Visual Studio 会向我们显示有关此方法的信息，甚至是

程序，.NET 会将这些参数打包成一个字符串数组并将其传递给 main 方法，而 main 方法可以决定对这些字符串做些什么。在我们的例子中，程序忽略了这些参数，我们也没有向此程序传递任何参数，所以这个数组将有 0 个元素，但它在需要时就在这里。回顾一下，现在我们理解了 Hello World 的大部分内容，这些行，直到你考虑到我们为达到这一点学了多少 C#，可能看起来并不多。我们学习了静态方法，如何将它们包含在类中，我们大量谈论了类型，C# 是一种类型安全语言的整体思想，如何修复一些类型相关的错误，我们浏览了 C# 中的类型，我们顺便提到了类型推断，我们涉及了数组，最后我们提到了 main 方法及其工作原理。我们没有深入探讨这些主题中的任何一个，但我们至少必须对它们有一个大致的了解，并且走得足够远以理解它是如何工作的，甚至还不完全。

```
1  using System;
2
3  namespace MyFirstProgram
4  {
```

我们没有谈论这里的几行，因为这些行把我们带到了一个稍微不同的世界，即比这个简单东西更复杂的真实程序的世界，它们通常由不止一个类和一个方法组成。而这就是下一章的主题。

