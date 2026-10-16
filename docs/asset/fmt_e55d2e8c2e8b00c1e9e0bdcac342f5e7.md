
```csharp
// This isn’t a real formula; it is made up for the purposes of this guide...
double a = 5.1;
double b = -6.5;
double c = 87;
double d = -56;
double e = 5.487;

double result = (((a + b) * (c - 4)) + d) * e;
```

顺便说一下，我想回顾一下我之前提到过的一点，为什么等号不被用来表示一件事等于另一件事。至少不是直接这样。`=` 符号是赋值运算符，它的作用是

实际上意思是它右边的内容会被计算，然后结果被放到左边的一个变量中。

让我们看看它是如何工作的：

```csharp
int a = 7;
```

```csharp
a = a + 2; // the variable called a will have a value of 9 once this line

// has been run.
```

数学家看到这个会觉得很奇怪。说到底，一个变量不可能等于它自己加 2。举个例子，从两边同时减去 `a`，就得到 `0 = 2`。从你的角度来看，这没有意义。

从编程的角度来看，这完全有意义。我们所说的是，取 `a` 中的值（7），加上 2，得到 9，然后把这个新值赋回给 `a`。我们只是取了 `a` 变量并给它加了 2。

### 复合赋值运算符

我们刚才谈到的，取一个值，对它做一些操作，然后再把它放回原来的变量，这在 `C#` 中非常常见，以至于专门为此设置了一整套运算符。这些被称为复合运算符——它们可以在同时进行数学运算和赋值操作。

让我们看看它们是如何工作的：

```csharp
int a = 7;
```

```csharp
a += 2; // This is the equivalent of a = a + 2;
```

对于减法运算符、除法、乘法和取模运算也有类似的运算符：

还有减法、乘法、除法和取模的等价运算符：

```csharp
int b = 8;
```

```csharp
b -= 4; // This is the equivalent of b = b − 4; at this stage, b would be

// 4.
```

`b *= 5;` // This is the equivalent of `b = b * 5;` at this stage, `b` would be 20.

`b /= 4;` // This is the equivalent of `b = b / 4;` at this stage `b` would be 5.

`b %= 2;` // This is the equivalent of `b = b % 2;` at this stage, `b` would be 1.

明白了吗？我们将在后面的章节中讨论更多数学方程和计算。

### 快速入门

- 加法的工作方式像 `int a = 4 + 5;`

- 减法的工作方式像 `int b = 6 − 3;`

- 乘法使用 `*` 作为符号，使用方式如下 − `int c = 5 * 5;`

- 除法使用 `/` 作为符号，使用方式如下 − `int d = 8 / 4;`

- 取模运算使用 `%` 作为符号，用于确定除法运算后的余数，像这样 − `int e = 22 % 7;` （`int e` 的值将为 1）。

- 在 `C#` 中进行数学运算时，可以使用任何标准数字类型 − `double`、`int`、`float`、`short` 等。

- 可以将多个运算组合成一个表达式，也可以在使用语句时使用之前创建的变量 − `int f = 3 * b − 4;`

- 运算顺序非常重要，它与你在学校学到的一样。乘法和除法优先于加法和减法，从左到右进行。括号优先于任何操作，因此使用它们来使计算按你想要的顺序进行，例如，

```csharp
double m = (y2 - y1)/ (x2 - x1)
```

- 复合赋值运算符是 `+=`、`-=`、`/=` 和 `%=`。它们执行运算并将值赋给左边的变量。例如，`a += 3;` 等价于 `a = a +3;` 并且只是给 `a` 中已有的值加上 3。

#### 下一步是什么？

我们在这里讨论了基本的数学运算，但还有更多内容需要学习。我们接下来会稍微偏离一下，看看如何使用命令行进行用户输入，这样在我们回到数学课之前，你就能知道它是如何工作的。

### 用户输入

这只是一个简短的部分；我们将快速查看几段代码，这些代码对于创建具有一定价值的程序是必需的。首先，我们将查看控制台窗口，了解如何使用它来获取用户输入，然后我们将了解如何将其转换为正确的数据类型。最后，我们将把所有学到的内容结合起来，编写一个程序，告诉我们圆柱体的体积和表面积。

#### 从控制台获取用户输入

我们可以使用以下语句从用户那里获取一些输入：

```csharp
string whatTheUserTyped = Console.ReadLine();
```

这使用了一个方法（我们将在后面的章节中讨论），它会读取用户提供的文本行。用户的文本被放到左边名为 `whatTheUserTyped` 的变量中。记住，任何变量都可以放在那里，这个变量没有什么特别之处。

#### 转换

大多数时候，仅从用户那里获取输入并将其放入字符串变量中是不够的，无法为我们的需求提供正确的数据类型。如果例如我们想要一个数字怎么办？当它被放入字符串中时，除非我们先将其转换为正确的数据类型，否则无法对其进行任何数学计算。不要误解我；有时字符串就是正确的类型，所以你并不总是需要更改它。

转换到另一种类型需要一种方法来将一种数据类型转换为另一种类型。我现在不会详细介绍；那是后面的内容。简而言之，如果我们想将字符串转换为整数，我们需要这样做：

```csharp
int aNumber = Convert.ToInt32(whatTheUserTyped);
```

每种可能的数据类型都有一个对应的类似方法。例如，`ToBoolean` 转换为 `bool` 类型；`ToInt16` 转换为 `short` 类型，`ToDouble` 用于 `double` 等等。其中有一个棘手的——`float` 类型。对于它，你必须使用 `ToSingle`，因为 `float` 是一个单精度值。你将在程序中看到它的运行情况。

#### 一个完整的程序

很好，我们已经有了一些更多的部分，现在我们可以创建一个真正做一些事情的程序。我们要做的是一个程序，让用户输入两个值——圆柱体半径和圆柱体高度。然后使用一些数学运算，所有公式都已为你提供，以计算圆柱体的体积和表面积。然后结果会打印给用户。

现在，对你来说最好的学习方式就是直接上手，看看你能想出什么。说真的，真正学习的最好方式是通过挣扎并尝试把所有部分拼凑起来。这不会发生，至少在指南的这个阶段不会发生。此外，这是一个教程，旨在让你按自己的节奏进行，而不是学校课程。

当然，你现在可以利用学到的知识构建你的程序，然后与我要告诉你的内容进行比较。你需要明白的一件事是——如果你的程序和我的不完全匹配也没关系——只要输出正确，代码正确就行。

无论如何，这是代码：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace CylinderCalculator
{
class Program
{
```

```csharp
static void Main(string[] args)
{
// Print a greeting message.
Console.WriteLine("Welcome to Cylinder Calculator !");

// Read cylinder's radius supplied by the user
Console.Write("Enter the cylinder's radius: ");
string radiusAsAString = Console.ReadLine();
double radius = Convert.ToDouble(radiusAsAString);

// Read cylinder's height supplied by the user
Console.Write("Enter the cylinder's height: ");
string heightAsAString = Console.ReadLine();
double height = Convert.ToDouble(heightAsAString);

double pi = 3.1415926536; // We’ll look at a different way to do PI later on

// These are the standard formulas for cylinder volume and surface area.
double volume = pi * radius * radius * height;
double surfaceArea = 2 * pi * radius * (radius + height);

// Now the results can be output
Console.WriteLine("The cylinder's volume is: " + volume + " cubic units.");
Console.WriteLine("The cylinder's surface area is: " + surfaceArea + " square units.");
```

```csharp
// Before you close, wait for a response from the user...
Console.ReadKey();
}
}
}
```

让我们分解一下。

第一部分应该对你非常熟悉，就是包含 `using` 语句的部分。

我们为用户提供了一个欢迎消息。

```csharp
// Print a greeting message.
Console.WriteLine("Welcome to Cylinder Calculator!");
```

与本指南开头 `Hello World!` 示例几乎相同。

接下来，我们要求用户输入圆柱体的高度和半径，然后使用本节开头讨论的内容将值转换为正确类型：

```csharp
// Read cylinder's radius supplied by the user
Console.Write("Enter the cylinder's radius: ");
string radiusAsAString = Console.ReadLine();
double radius = Convert.ToDouble(radiusAsAString);
```

```csharp
// Read cylinder's height supplied by the user
Console.Write("Enter the cylinder's height: ");
string heightAsAString = Console.ReadLine();
double height = Convert.ToDouble(heightAsAString);
```

The first line is nothing more than simple input and, after that, we read the user’s text in and stored it inside a string object. The next bit turned it into the right data type, in our case, the `double` type and then we did the same with the height of the cylinder.

Next, the value of PI was defined. Then we use some of the math operations we looked at in the last section to calculate what the cylinder surface area and volume are.

```csharp
double pi = 3.1415926536; // We’ll look at a different way to do PI later on.
```

```csharp
// These are the standard formulas for cylinder volume and surface area.
double volume = pi * radius * radius * height;
double surfaceArea = 2 * pi * radius * (radius + height);
```

Last, the result is output to the user:

```csharp
// Now the results can be output
Console.WriteLine("The cylinder's volume is: " + volume + " cubic units.");
Console.WriteLine("The cylinder's surface area is: " + surfaceArea + " square units.");
```

```csharp
// Before you close, wait for a response from the user...
Console.ReadKey();
```

That is our very first useful program written in `C#`.

### What’s Next?

Now we’ve learned enough to create a useful program, we can kick things up a notch and take things further. Next, we’re going back to math but in much more detail this time. Once we’ve done that, we can get stuck into logic, into getting our computer to make some choices about what it does.

### Math Part 2

Now, this is quite an involved section so don’t panic if you don’t understand it all first time around – go over it as many times as you need to.

As I explained earlier, computers absolutely love math, which is great, because that is pretty much all they can do. We will be moving on to more exciting stuff soon, I promise but this is a very important subject to learn.

One thing I do need to warn you is that the sections here are separate, not really related to one another at all. This is good because, if you need help on one specific thing, you can just jump straight to that section.

What are we going to discuss?

We’ll start off doing some division using integers, covering a very interesting problem that arises from it. Then we’ll move on to data conversion in a process called typecasting before we cover the subject of division by zero. After that, some of the special `C#` numbers, such is `NaN`, infinity, pi, and `e`, and then we’ll cover over and underflow. To finish, we’ll look at incrementing and decrementing, a very special `C#` feature.

Even if you think you know the subject, please don’t be tempted to skip a section; it never hurts to have a refresher and especially do not skip the final section – you really will regret it!

Above all, although there is so much to learn here, do try and have fun. Programming doesn’t have to be strait-laced, nose-to-the-grindstone theory.

Let’s get started.

#### Integer Division
