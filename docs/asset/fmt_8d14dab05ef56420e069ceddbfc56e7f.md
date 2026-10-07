
To auto-close the console when debugging stops, enable `Tools>Options>Debugging>Automatically close the console when debugging stops`.

Press any key to close this window . . .

### 2.3 - 递归

“递归”（recursion）一术在编程中非常典型，在 C# 语言中也是如此。当问题变得过于复杂时，算法需要拆分成更小的部分以找到解决方案。递归是一种编程技术，其中当前程序方法或过程反复调用自身来解决该问题。因此，为了更容易，递归是执行一个函数的过程，意味着在函数主体块内部调用自身。某些需要遍历特定代码块的问题可以通过递归进行简化和解决。最好的案例应该是著名的数学问题——阶乘（factorial）的计算。一个数的阶乘表示从1到该特定数的所有数的乘积。零的阶乘值位于第一个或等号的一侧。以下是第一个或等号左侧的几种阶乘表示示例。数学符号‘!’不应与 C# 的非运算符‘!’混淆，后者返回当前布尔值的相反值。在 C# 中，‘!’ 总是将布尔值从 true 翻转为 false 或反之。记住，下面的示例不是有效的 C# 代码，而是数学阶乘表示法的示例。

```
0! = 1

1! = 1

2! = 1*2 = 2

3! = 1*2*3 = 6

4! = 1*2*3*4 = 24

5! = 1*2*3*4*5 = 120
```

```cs
static void Main(string[] args)
{
    Console.WriteLine(fact(5));
    Console.WriteLine(factLoop(5));
}
public static int fact(int n)
{
    if (n <= 1) // base case
        return 1;
    else
        return n * fact(n - 1);
}
public static int factLoop(int n)
{
    if (n <= 1) // base case
        return 1;
    int factorialValue = 1;
    int i = 1;
    while(i<= n)
    {
        factorialValue *= i; // factorialValue = factorialValue * i;
        i++;
    }
    return factorialValue;
}
```

```cs
// Example 1: if statement
int exampleOneYear = 1988;
if (exampleOneYear < 1900)
{
    Console.WriteLine("19th Century");
}
// Example 2: if-else statement
int exampleTwoYear = 1988;
if (exampleTwoYear < 2000)
{
    Console.WriteLine("Unknown Century");
}
else
{
    Console.WriteLine("21st Century");
}
// Example 3: if-else if statement
int exampleThreeYear = 2010;
if (exampleThreeYear < 1900)
{
    Console.WriteLine("Unknown Century");
}
else if (exampleThreeYear < 2000)
{
    Console.WriteLine("20th Century");
}
else
{
    Console.WriteLine("21st Century");
}
```

在第一个示例中，1988年的条件将不会满足，程序将不会进入 `if` 代码块——控制台不会打印任何内容。

在第二个示例中，即1998年，变量 `year` 在此情况下小于2000，因此程序将进入 `if` 代码块，并在控制台上打印“Unknown Century”（未知世纪）。

在第三个示例中，2010年，第一个条件将不会满足，因为2010并不小于1900。程序接着进入 `else-if` 条件，由于年份也不小于2000，程序将进入最后的 `else` 分支，在控制台行打印“21st Century”（21世纪）。

现在让我们来看下面的 `switch` 语句示例：

```cs
// switch statement
int month = 5;
switch (month) {
    case 1:
        Console.WriteLine("January");
        break;
    case 2:
        Console.WriteLine("February");
        break;
    case 3:
        Console.WriteLine("March");
        break;
    case 4:
        Console.WriteLine("April");
        break;
    case 5:
        Console.WriteLine("May");
        break;
    case 6:
        Console.WriteLine("June");
        break;
    case 7:
        Console.WriteLine("July");
        break;
    case 8:
        Console.WriteLine("August");
        break;
    case 9:
        Console.WriteLine("September");
        break;
    case 10:
        Console.WriteLine("October");
        break;
    case 11:
        Console.WriteLine("November");
        break;
    case 12:
        Console.WriteLine("December");
        break;
    default:
        Console.WriteLine("None of the months");
        break;
}
```

在这里，程序将月份数字初始化为值 `5`。此值表示一年的第五个月，即五月。`switch` 语句是如何工作的？它在开头有一个 `switch` 条件。根据该条件，程序将进入下面定义的某个 `case` 之一。每个 `case` 都类似于 `if` 语句。如果从 `switch` 条件传递的值与某个 `case` 匹配，程序将进入该特定 `case` 的代码块。在输入没有匹配 `case` 的情况下，程序将进入 `default` 代码块。也可以不定义 `default` 情况，但最好这样做，因为这样程序可以确保在输入没有对应 `case` 时不会发生错误。

在这个示例中，月份值为五，因此程序将进入 `case 5` 代码块，并在控制台上打印“May”。

让我们用下面这一个程序来总结本章，该程序将演示循环、递归和分支处理的基本操作：

```cs
class Program
{
    static void Main(string[] args)
    {
        ForLoop();
        WhileLoop();
        IfElseStatements();
        FibonacciRecursion(0, 1, 1, 10);
    }
    private static void ForLoop()
    {
        for (int index = 0; index < 10; index++)
        {
            Console.WriteLine(index);
        }
    }
    private static void WhileLoop()
    {
        int index = 0;
        while (index < 10)
        {
            Console.WriteLine($"{index++}");
        }
    }
    private static void IfElseStatements()
    {
        for (int index = 0; index < 10; index++)
        {
            if (index % 2 == 0)
            {
                Console.WriteLine($"{index} is even");
            }
            else
            {
                Console.WriteLine($"{index} is odd");
            }
        }
    }
    private static void FibonacciRecursion(int a, int b, int counter, int number)
    {
        Console.WriteLine(a);
        if (counter < number) FibonacciRecursion(b, a+b, counter+1, number);
    }
}
```

在这个示例中，我们展示了类 `Program`，它包含五个方法（注意：文中说是五个，但代码显示了四个方法：Main, ForLoop, WhileLoop, IfElseStatements 和 FibonacciRecursion - 等等，那是五个：Main, ForLoop, WhileLoop, IfElseStatements, FibonacciRecursion）。

无限延伸的斐波那契数列。该方法初始调用时带有以下四个参数：$0$ 代表要打印的当前元素，$1$ 代表下一个要打印的元素，$1$ 代表一次打印的步长，$$10$ 代表斐波那契数组的长度。在开始，程序打印斐波那契数组的当前元素，该元素作为第一个参数传递。

之后，程序有一个条件，检查从第三个参数传递的步长是否小于目标输出数组的长度。如果满足该条件，方法将再次调用自己，但使用不同的参数。在下一次调用中，第一个参数变为上一次调用的第二个参数，因为在上一次调用中，第二个参数是下一个要打印的元素。第二个参数代表下一个打印的元素，通过上一次调用中的当前元素和下一个元素相加计算。第三个参数是增加了一个步长，第四个参数在每次调用中保持不变。这样，通过方法自调用的递归原理构建了斐波那契数列。递归调用的流与执行的方法的方法相同，其结果返回给它的父方法——即执行子方法的方法。在这种情况下，“父方法”指的是调用了另一个方法，而“子方法”指的是被父方法调的方法。“父方法”也称为“调用方法”，“子方法”也称为“被调用方法”。这种流传播到主父方法调用。该序列的输出将逐行显示 $0, 1, 1, 2, 3, 5, 8, 13, 21$ 和 $34$。该程序的完整输出如下：

```
Microsoft Visual Studio Debug Console
0
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
```

```
Microsoft Visual Studio Debug Console
0 is even
1 is odd
2 is even
3 is odd
4 is even
5 is odd
6 is even
7 is odd
8 is even
9 is odd
10 is even
11 is odd
12 is even
13 is odd
14 is even
15 is odd
16 is even
17 is odd
18 is even
19 is odd
20 is even
21 is odd
22 is even
23 is odd
24
:\Users\LENVO\Desktop\EBOOK\C#EBOOK\Outline Problem Examples\2 - BranchesAndLoops\bin\Debug\netcoreapp3.1\BranchesAndLoops.exe (process 260) exited with code 0.
To NOT to AUTOMATICALLY close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
Press any key to close this window.
```

# 第3章：方法与属性

在 C# 编程语言中，以及其他面向对象的编程语言中，都有称为“方法”的术语。方法是程序内部被调用时执行的代码块。它也可以被定义为一组执行有意义逻辑的语句。方法也被称为函数，用于执行某些操作。使用方法最大的优势是代码的可重用性。特定的逻辑可以定义在一个地方，也可以在程序的不同地方被多次调用。方法通过其名称定义，后面跟着括号——()。方法的关键元素是访问修饰符、方法的返回类型、方法名、参数列表和方法体。访问修饰符代表了从另一个类的角度来看方法的可见性。根据返回类型，方法分为两类：void 方法和显式类型方法。void 方法没有返回值，它们被指定执行某些不需要结果的工作。而显式类型方法是具有返回值的方法。方法的返回类型可以是多种。例如，方法的返回类型可以是 `int`、`string`、`bool` 等。方法名代表方法的唯一标识符，并且在 C# 中是区分大小写的。这意味着它能识别大写和小写字母的区别。例如，`EBook()` 方法名与 `EBOOK()` 方法名不同。参数列表用于在方法之间传递和接收数据。参数是方法内部可选的元素。参数可以是任何类型，并且可以传递多个参数。将参数传递给方法有几种方法。在值传递方法中，方法内部对此参数的所有更改对传递进的值没有影响。这是因为变量的引用没有传递给函数，它只是值的副本。在引用传递方法中，对参数的任何更改都会对传递的变量产生影响。这是因为参数内存位置的引用被复制到形式参数中。方法的**体代码块**包含了执行某些逻辑所需的指令序列。方法还可以被**重载**。重载意味着可以定义多个相同但参数不同的方法。例如，如果 `EBook()` 方法名与 `EBOOK()` 方法名不同，编译器不会报告错误。（*注：此处原文后续存在大量重复段落，译文已根据核心逻辑进行整合处理*）

- **字段**是类中声明的变量，用于持有对象的数据。
- **属性**提供了一种读写私有字段值的机制。
- **访问器**（如 `get` 和 `set`）用于定义属性的行为。

```csharp
using System;

namespace MethodsAndProperties
{
    class Program
    {
        static void Main(string[] args)
        {
            Car car = new Car("Renault Clio");
            Console.WriteLine(car.Model);
            car.Model = "Megane";
            Console.WriteLine(car.Model);
        }
    }
    class Car
    {
        private string _model;
        public Car(string modelName)
        {
            _model = modelName;
        }
        public string Model
        {
            get
            {
                return _model;
            }
            set
            {
                _model = "Renault " + value;
            }
        }
    }
}
```
