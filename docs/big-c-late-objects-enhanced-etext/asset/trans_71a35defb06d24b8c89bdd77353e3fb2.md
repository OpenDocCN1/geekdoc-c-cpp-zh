

现在把伪代码转换成真正的代码。最后三种情况很简单，因为辅助函数已经为它们开发好了：

```
if (part >= 20)
{
    name = name + " " + tens_name(part);
    part = part % 10;
}
else if (part >= 10)
{
    name = name + " " + teen_name(part);
    part = 0;
}

if (part > 0)
{
    name = name + " " + digit_name(part);
}
```

最后，让我们处理 100 到 999 之间的数字。因为 part < 1000，part / 100 是一个一位数，我们通过调用 digit_name 来获取它的名称。然后我们添加 "hundred" 后缀：

```
if (part >= 100)
{
    name = digit_name(part / 100) + " hundred";
    part = part % 100;
}
```

现在你已经看到了 int_name 函数所有重要的构建模块。下面是完整的程序：

## sec07/intname.cpp

```
#include <iostream>
#include <string>

using namespace std;

/**
 *Turns a digit into its English name.
 *@param digit an integer between 1 and 9
 *@return the name of digit ("one" ... "nine")
 */
string digit_name(int digit)
{
    if (digit == 1) return "one";
    if (digit == 2) return "two";
    if (digit == 3) return "three";
    if (digit == 4) return "four";
    if (digit == 5) return "five";
    if (digit == 6) return "six";
    if (digit == 7) return "seven";
    if (digit == 8) return "eight";
    if (digit == 9) return "nine";
    return "";
}

/**
 *Turns a number between 10 and 19 into its English name.
 * @param number an integer between 10 and 19
 * @return the name of the given number ("ten" ... "nineteen")
 */
string teen_name(int number)
{
    if (number == 10) return "ten";
    if (number == 11) return "eleven";
    if (number == 12) return "twelve";
    if (number == 13) return "thirteen";
    if (number == 14) return "fourteen";
    if (number == 15) return "fifteen";
    if (number == 16) return "sixteen";
    if (number == 17) return "seventeen";
    if (number == 18) return "eighteen";
    if (number == 19) return "nineteen";
    return "";
}

/**
 * Gives the name of the tens part of a number between 20 and 99.
 * @param number an integer between 20 and 99
 * @return the name of the tens part of the number ("twenty" ... "ninety")
 */
string tens_name(int number)
{
    if (number >= 90) return "ninety";
    if (number >= 80) return "eighty";
    if (number >= 70) return "seventy";
    if (number >= 60) return "sixty";
    if (number >= 50) return "fifty";
    if (number >= 40) return "forty";
    if (number >= 30) return "thirty";
    if (number >= 20) return "twenty";
    return "";
}

/**
 * Turns a number into its English name.
 * @param number a positive integer < 1,000
 * @return the name of the number (e.g. "two hundred seventy four")
 */
string int_name(int number)
{
    int part = number; // The part that still needs to be converted
    string name; // The return value

    if (part >= 100)
    {
        name = digit_name(part / 100) + " hundred";
        part = part % 100;
    }

    if (part >= 20)
    {
        name = name + " " + tens_name(part);
        part = part % 10;
    }
    else if (part >= 10)
    {
        name = name + " " + teen_name(part);
        part = 0;
    }

    if (part > 0)
    {
        name = name + " " + digit_name(part);
    }

    return name;
}

int main()
{
    cout << "Please enter a positive integer: ";
    int input;
    cin >> input;
    cout << int_name(input) << endl;
    return 0;
}
```

## 程序运行

```
Please enter a positive integer: 729
seven hundred twenty nine
```

![](img/d61019b035dd82beb581604273c0ee6b_258_0.png)

## 编程技巧 5.3
### 保持函数简短

编写函数是有一定代价的。你需要设计、编码并测试这个函数。函数需要编写文档。你需要花费一些精力让函数可复用，而不是与特定上下文绑定。为了避免这种代价，人们总是想在一个地方塞进越来越多的代码，而不是费心将代码拆分成独立的函数。我们经常看到经验不足的程序员写出长达数百行的函数。

根据经验法则，如果一个函数太长，其代码在开发环境中一屏显示不下，那么就应该把它拆开。

![](img/d61019b035dd82beb581604273c0ee6b_258_1.png)

## 编程技巧 5.4
### 跟踪函数

当你设计一组复杂的函数时，在把程序交给计算机之前，最好先进行一次手动走查。

拿一张索引卡或其他纸片，写下你想要研究的函数调用。写下函数名以及参数变量的名称和值，就像这样：

![](img/d61019b035dd82beb581604273c0ee6b_258_2.png)

```
*/
string digit_name(int digit)
{
    return "mumble";
}

/**
 Gives the name of the tens part of a number between 20 and 99.
 @param number an integer between 20 and 99
 Return the tens name of the number ("twenty" ... "ninety")
 */
string tens_name(int number)
{
    return "mumblety";
}
```

如果你将这些桩函数与 `int_name` 函数组合，并用参数 274 进行测试，你会得到“mumble hundred mumblety mumble”这样的结果，这表明 `int_name` 函数的基本逻辑工作正常。

![](img/d61019b035dd82beb581604273c0ee6b_260_0.png)

*桩（stub）是不完整的函数，可用于测试。*

© lilliphotography/iStockphoto.

![](img/d61019b035dd82beb581604273c0ee6b_260_1.png)

## 实例演练 5.3
### 计算课程成绩

学习如何使用逐步求精来解决将一组字母等级转换为课程平均成绩的问题。请参阅你的电子教材，或访问 wiley.com/go/bcl03。

![](img/d61019b035dd82beb581604273c0ee6b_260_2.png)

© paul kline/iStockphoto.

## 5.8 变量作用域与全局变量

变量的作用域（scope）是程序中该变量可见的部分。

在程序中，同一个变量名可以被定义多次。当使用某个变量名时，你需要知道它属于哪一个定义。在本节中，我们讨论处理同名多重定义的规则。

在函数内定义的变量，从其定义点开始到其所在块的末尾都是可见的。这个区域称为变量的作用域。

考虑下面例子中的 volume 变量：

```
double cube_volume(double side_length)
{
    double volume = side_length * side_length * side_length;
    return volume;
}
```

```
int main()
{
    double volume = cube_volume(2);
    cout << volume << endl;

    return 0;
}
```

每个 volume 变量都定义在各自独立的函数中，它们的作用域互不重叠。

在同一个作用域中定义两个同名变量是不合法的。例如，下面的代码是不合法的：

```
int main()
{
    double volume = cube_volume(2);
    double volume = cube_volume(10);
    // ERROR: cannot define another volume variable in this scope
}
```

然而，你可以在嵌套块中定义另一个同名变量。这里，我们定义了两个名为 amount 的变量。

```
double withdraw(double balance, double amount)
{
    if (...) {
        double amount = 10; // Another variable named amount
    }
    ...
}
```

![](img/d61019b035dd82beb581604273c0ee6b_261_0.png)

© jehamp/iStockphoto (Railway and Main); © StevenCarrieJohnson/iStockphoto (Main and N. Putnam); © jsmith/iStockphoto (Main and South St.)

就像不同城市里都可以有一条名为 “Main Street” 的街道一样，C++ 程序也可以有多个同名变量。

嵌套块中的变量会遮蔽外层块中的同名变量。

局部变量定义在函数内部。全局变量定义在函数外部。

参数变量 amount 的作用域是整个函数，但嵌套块内部除外。在嵌套块内部，amount 指的是在该块中定义的变量。我们说内部变量遮蔽了外部块中定义的变量。在编写函数时，你应该避免这种可能引起混淆的情况，只需重命名其中一个变量即可。

在函数内部定义的变量称为局部变量。C++ 还支持全局变量：定义在函数外部的变量。全局变量对其之后定义的所有函数可见。例如，<iostream> 头文件定义了全局变量 cin 和 cout。

下面是一个全局变量的例子：

```
int balance = 10000; // A global variable

void withdraw(double amount)
{
    if (balance >= amount)
    {
        balance = balance - amount;
    }
}

int main()
{
    withdraw(1000);
    cout << balance << endl;
    return 0;
}
```

变量 balance 的作用域覆盖 withdraw 和 main 两个函数。

一般来说，全局变量并不是一个好主意。当多个函数更新全局变量时，结果可能难以预测。尤其是在由多个程序员开发的大型程序中，每个函数的效果清晰且易于理解非常重要。你应该在程序中避免使用全局变量。

在程序中避免使用全局变量。

![](img/d61019b035dd82beb581604273c0ee6b_262_0.png)

## 编程技巧 5.6
### 避免使用全局变量

有少数情况需要使用全局变量（例如 cin 和 cout），但这种情况相当罕见。使用全局变量的程序难以维护和扩展，因为你无法再把每个函数看作一个仅接收参数并返回结果的“黑盒”。当函数修改全局变量时，理解函数调用的效果就变得更加困难。随着程序规模变大，这种困难会迅速增加。不要使用全局变量，而应使用函数参数在程序的不同部分之间传递信息。

## 5.9 引用参数

如果你想编写一个改变实参值的函数，就必须使用引用参数才能允许这种改变。我们首先解释为什么需要一种不同的参数类型，然后展示引用参数的语法。

