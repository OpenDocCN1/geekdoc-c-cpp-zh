

可以用来给程序中 Example 6.2 中的 tempFahrenheit 等 double 类型变量赋值的语句：

```
double tempFahrenheit = celsiusToFahrenheit(tempCelsius);
```

类似地，驱动程序中 Example 6.3 中的输出语句

```
cout << "100C => " << celsiusToFahrenheit(100) << "C\n"
<< "0C => " << celsiusToFahrenheit(0) << "C\n"
<< "10C => " << celsiusToFahrenheit(10) << "C\n";
```

对 celsiusToFahrenheit() 有三次调用，并且是一个合法的语句，因为 << 运算符可以用来输出 double 值。

## 6.3.4 局部变量

函数 celsiusToFahrenheit() 是一个非常简单的函数；其函数体只包含一个语句，并且只使用一个变量——参数 tempCelsius——和两个常量。然而，许多函数更为复杂，具有更多的语句并使用多个变量和/或常量来计算其返回值。

例如，假设我们希望构造一个函数来计算风寒指数。美国国家气象局使用的风寒指数公式为

wind chill = 35.74 + 0.6215 × t − 35.75 × v^0.16 + 0.4275 × t × v^0.16

其中包含五个不同的常量和两个变量：t，表示华氏温度，和 v，表示英里每小时的风速。相应地，Example 6.4 中的函数 windChill() 有两个参数：tempFahr，表示公式中的 t，和 windSpeed，表示 v。它使用前述公式来计算风寒指数，但为了效率，将其分解为两个步骤，以便 v^0.16 只计算一次：

- 计算 multiplier = −35.75 × 0.4275 × t
- 计算 wind chill = 35.74 + 0.6215 × t + multiplier × v^0.16

变量 multiplier 用于存储第一步计算的结果。Example 6.4 还展示了一个简单的驱动程序来测试 windChill()。

## Example 6.4 计算风寒指数

```
/* This is a driver program to test the windChill() function.
------------------------------------------------------------*/
```

```
#include <iostream>      // cin, cout, <<, >>
using namespace std;
```

如果尝试在函数外部使用它们，就会产生错误。其结果之一是函数外部的标识符可能与函数内部的参数或局部变量或常量同名。

## 6.3.5 函数中的控制结构

到目前为止，顺序一直是我们函数示例中唯一使用的控制结构。然而，选择和重复结构也可以使用。Example 6.5 中的程序通过将第 5.5 节中使用 for 循环计算阶乘的代码封装到一个函数中来说明这一点。

## Example 6.5 计算阶乘

```
/* This is a driver program to test the factorial() function.
--------------------------------------------------------------------------*/

#include <iostream>    // cin, cout, <<, >>
using namespace std;

unsigned factorial(unsigned n);    // prototype

int main()
{
    unsigned number;    // integer whose factorial is computed

    cout << "Enter a nonnegative integer: ";
    cin >> number;
    cout << number << "! = " << factorial(number) << endl;
}

/* factorial computes the factorial of a nonnegative integer

   Receive: n, a nonnegative integer
   Return:  n!
--------------------------------------------------------------------------*/

unsigned factorial(unsigned n)    // definition
{
    unsigned nfact = 1;
    for (unsigned i = 1; i <= n; i++)
        nfact *= i;

    return nfact;
}
```

## SAMPLE RUNS:

```
Enter a nonnegative integer: 0
0! = 1
```

```
Enter a nonnegative integer: 4
4! = 24

Enter a nonnegative integer: 10
10! = 3628800
```

## 6.3.6 不返回任何值的函数

假设一个问题涉及货币计算，我们需要以 $dd.cc 的形式显示金额。我们可以直接使用包含多个格式操纵符的输出语句：

```
int main()
{
    // ...
    cout << fixed << showpoint
         << right << setprecision(2)
         << '$' << dollarAmount;
}
```

但把此类细节放在 main 函数中会使程序变得杂乱无章，尤其是在多个不同位置都需要时。最好使用更简单的语句，例如

```
int main()
{
    // ...
    printAsMoney(dollarAmount);
}
```

其中 printAsMoney() 将像一个接收 dollarAmount 值参数并以所需格式输出它但不返回值的函数一样工作。

在某些编程语言中，我们可以用称为过程或子程序的子程序来完成此操作，它们与函数不同。然而，在 C++ 中，唯一的子程序是函数。这意味着我们必须编写一个名为 printAsMoney() 的函数。代替通常的“Receive–Return”规范，我们可能会使用

**Receive:** 一个实数值 dollars

**Output:** 以货币值适当格式输出 dollars 的值

从该规范中，我们可以看到 printAsMoney() 将有一个名为 dollars 的 double（或 float）参数，但对于一个不返回值的函数，我们用什么作为返回类型呢？

对于这些不向调用者返回任何值的特殊函数，C++ 提供了关键字 void 来表示没有类型。因此我们只需将其用作 printAsMoney() 的返回类型：

```
void printAsMoney(double dollars);
```

因此，C++ 中的 void 函数就是其他编程语言中过程和子程序的对应物。

由于 void 函数不返回值，因此不能像到目前为止我们考虑过的函数那样在表达式中使用。例如，如果我们写

```
cout << "Amount due: "
    << printAsMoney(dollarAmount)    // ERROR!
    << endl;
```

就会产生错误，因为 printAsMoney(dollarAmount) 不返回值。相反，void 函数是用形如

```
function_Name(argument_list);
```

的语句调用的。因此，代替前面的输出语句，我们可以写

```
cout << "Amount due: ";
printAsMoney(dollarAmount);
cout << endl;
```

Example 6.6 给出了 printAsMoney() 的完整定义。它还展示了一个输入购买金额和已付款金额的程序，并使用 printAsMoney() 显示退还给客户的金额。

## Example 6.6 货币交易

```
/* Program to compute the amount to be returned for a purchase.

Input: purchase, payment
Output: amount returned to customer (via printAsMoney())
-------------------------------------------------- --------------------*/

#include <iostream>  // cin, cout, <<, >>, ...
#include <iomanip>  // setprecision, ...
using namespace std;

void printAsMoney(double dollars);  // prototype

int main()
```

```
{
    double purchase,              // amount of purchase
            payment;                // amount paid

    cout << "Enter amount of purchase: ";
    cin >> purchase;
    cout << "Enter amount paid (>= purchase): ";
    cin >> payment;
    if (payment >= purchase)
    {
        cout << "Amount to return is: ";
        printAsMoney(payment - purchase);
        cout << endl;
    }
    else
        cout << "Inadequate payment!";
    cout << endl;
}
```

```
/* printAsMoney displays an amount in monetary format.

    Receive: dollars, the double value to be displayed
    Output: dollars in monetary format
    ----------------------------------------------- */

void printAsMoney(double dollars)
{
    cout << fixed << showpoint
         << setprecision(2)
         << '$' << dollars;
}
```

## SAMPLE RUNS:

```
Enter amount of purchase: 4.01
Enter amount paid (>= purchase): 5.00
Amount to return is: $0.99

Enter amount of purchase: 9.00
Enter amount paid (>= purchase): 20.00
Amount to return is: $11.00
```

注意，将货币格式细节隐藏在 void 函数 printAsMoney() 中使 main 函数更易于阅读。正如本章介绍中所指出的，这种通过隐藏某些细节而使事物简化起来的观点被称为抽象或信息隐藏。我们的 printAsMoney() 函数“隐藏”了如何完成显示货币值操作的细节（至少就 main 函数的读者而言）。

