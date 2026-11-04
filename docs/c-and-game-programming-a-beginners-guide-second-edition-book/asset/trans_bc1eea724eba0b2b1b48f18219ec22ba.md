
> **注意**
>
> 我们也可以将那个用户定义函数替换为预定义函数 `Math.Sqrt()`。

## 将函数编写为黑盒

*黑盒理论* 只是一个概念，它强调这样一种观点：大多数（即使不是全部）函数都应被视为独立或自包含的子程序。它还认为，只想调用某个函数的程序员无需研究或了解用于构造该函数的代码。因此，访问一个函数所需的唯一信息就是正确传入的变量，以及知道该函数将返回什么。这类似于会开车，但不知道如何修理发动机。这在 C# 中实际上是常态，因为所有预定义函数对大多数程序员来说都是黑盒，而增强它们的想法实际上会迫使我们打开它们，并按照某种新标准重新设计它们（不幸的是，这在游戏编程中通常是必要的）。当然，如果你编写自己的用户定义函数，你肯定知道每个函数是如何工作的。

创建黑盒风格的函数要求或限制我们使用封装控制。当然，这意味着你必须避免使用全局变量，并且必须为每个原型添加注释，以提醒任何其他程序员注意变量设置及其结果。此外，你应该记住，在后面的章节中，我们将从单独的文件中读取和写入用户定义函数，因此确实需要详细注释来解释这些不同的函数调用各自做什么。

> **将黑盒方法应用于示例 2.40**
>
> 假设你并没有真正理解上一个示例的第二部分，但你还是使用了平方根函数。虽然这让我内心中的数学家有点沮丧，但这不会影响程序执行该数据的方式，事实上，这恰好说明了我的观点。不过，如果那段代码引起了你的兴趣，那么下面是对其数学原理的简要概述（见示例 2.41）。

### 示例 2.41. 平方根函数详解。

```
static float SquareRoot (float n){    // Newton's Method (Basic Calculus)
float test1, test2;                    // Xₙ₊₁ = Xₙ - f(Xₙ)/f'(Xₙ)  n = 1, 2, 3,
... 
test1 = n-(float).01 -                 // X₀ = Guess-Estimate
    ((n-(float).01)*(n-(float).01) - n)/(n*(n-(float).01));
test2 = test1 - ((test1*test1)-n)/((n)*test1);

while (test1 != test2){                // X₁ = X₀ - (X₀² - Number)/(Number*X₀)
    test1 = test2;                     // X₁ = X₀ - (X₀² - Number)/(Number*X₀)
    test2 = test1 -                    // X₂ = X₁ - (X₁² - Number)/(Number*X₁)
        (test1*test1 - n) /            // X4 = X₃ - (X₃² - Number)/(Number*X₃)
        ((n)*test1);                   // X₆ = X₅ - (X₅² - Number)/(Number*X₅)
}
return (test2);                        // until Xₙ = Xₙ₊₁
}
```

同样，我们也可以使用预定义函数 Math.Sqrt() 重建上一个程序（见示例 2.42）。

### 示例 2.42. 用户定义函数与预定义函数对比。

```
using System;

namespace Chapter2 {
    class Class1 {
        static void Main() {
            string input;
            float number = 0, root = 0;

            Console.WriteLine("This program will find the "
                + "square root of any number\n"
                + "To continue just enter a number when prompted\n"
                + "Your results will appear after you press enter\n"
                + "To quit just enter the number \"1\"^n"
                + "Enter your first value now: ");
            input = Console.ReadLine();
            number = float.Parse(input);
```

```csharp
class Class1 {
    static void Main() {
        string input = "Y", Horse;
        int iNumber1 = 0, iNumber2 = 0, iNumber3 = 0;

        Console.WriteLine("Let's have a horse race.\n"
            + "To play select one of the horses below");

        while (char.ToUpper(char.Parse(input)) != 'N') {
            Console.WriteLine("(1) for Whitefire\n"
                + "(2) for The Train and, \n"
                + "(3) for Noisy Glue\n");
            Horse = Console.ReadLine();

            TheRace(ref iNumber1);
            TheRace(ref iNumber2);
            TheRace(ref iNumber3);

            TieBreaker(iNumber1, ref iNumber2);
            TieBreaker(iNumber2, ref iNumber3);
            TieBreaker(iNumber1, ref iNumber3);

            Console.Write("And the winner is ");
            if (iNumber1 > iNumber2 && iNumber1 > iNumber3)
                Console.WriteLine("Noisy Glue"); // 3
            else if (iNumber2 > iNumber1 && iNumber2 > iNumber3)
                Console.WriteLine("The Train"); // 2
            else
                Console.WriteLine("Whitefire"); // 1

            Console.WriteLine("Would you like to play again (Y/N)?");
            input = Console.ReadLine();
        }
    }

    static void TheRace(ref int Num) {
        Random rnd = new Random();

        Num = (int)Math.Round(rnd.NextDouble() * 1000);
    }

    static void TieBreaker(int Num1, ref int Num2) {
        if (Num1 == Num2) {
TheRace(ref Num2);
TieBreaker(Num1, ref Num2);
} 
} 
}
```

## 关键字 out

关键字 out 是一种特殊的异常标记，它通知编译器：所检查的变量在被作为引用变量传递之前不需要赋值。这通常适用于这样的情况：在适当的函数执行之前，这些变量本来不会有有意义的值。由于 out 值也是引用值，此关键字消除了对第二个引用（ref）的需要（见示例 2.44）。

### 示例 2.44. 关键字 out。

```
using System;

namespace Chapter7 {
    class Class1 {
        static void Main() {
            string input = "Y", Horse;
            int iNumber1, iNumber2, iNumber3;

            Console.WriteLine("Let's have a horse race.\n"
                + "To play select one of the horses below");

            while (char.ToUpper(char.Parse(input)) != 'N') {
                Console.WriteLine("(1) for Whitefire\n"
                    + "(2) for The Train and, \n"
                    + "(3) for Noisy Glue\n");
                Horse = Console.ReadLine();

                TheRace (out iNumber1);
                TheRace (out iNumber2);
                TheRace (out iNumber3);

                TieBreaker (iNumber1, ref iNumber2);
                TieBreaker (iNumber2, ref iNumber3);
                TieBreaker (iNumber1, ref iNumber3);
Console.Write ("And the winner is");

if (iNumber1 > iNumber2 && iNumber1 > iNumber3)
    Console.WriteLine("Noisy Glue"); // 3
else if (iNumber2 > iNumber1 && iNumber2 > iNumber3)
    Console.WriteLine("The Train"); // 2
else
    Console.WriteLine("Whitefire"); // 1

Console.WriteLine("Would you like to play again (Y/N)?");
input = Console.ReadLine(); }

static void TheRace(out int Num) {
Random rnd = new Random();
Num = (int)Math.Round(rnd.NextDouble() * 1000);
}

static void TieBreaker(int Num1, ref int Num2) {
if (Num1 == Num2) {
    TheRace(out Num2);
    TieBreaker(Num1, ref Num2);
}
}
}
```

## 多态简介

多态（也称为重载）发生在任何引用具有密切匹配但不完全相同的定义时。这些辅助函数或替代函数虽然在技术上并非必需，但通常倾向于保持在第一个函数用途的范围内。如果将一个重载函数修改到足以促成一个全新定义的程度，那么重载就没有必要了。虽然重载函数确实共享相同的引用名称，但它们的定义必须在排列上至少有一个传递数据类型不同。使用这些不同的访问点会引导编译器找到正确的（重载）函数。由于存在多个可能的引用点，错误调用该函数的可能性也会增加，从而产生运行时错误。示例 2.45 和 2.46 给出了可以产生相同结果的替代函数，但只有一个实际上执行正确。

