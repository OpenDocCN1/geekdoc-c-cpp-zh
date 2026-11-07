

## 程序 6.27 求定期投资的未来值

```cpp
void input (double& invest, double& rate, double& term)
{
    invest = getInput ("Enter the value of periodic investment: ");
    rate = getInput ("Enter the interest rate per year: ");
    term = getInput ("Enter the term (number of years): ");
}

/*
 * The process function calls findMultiplier to calculate the
 * multiplier. It then multiplies the return value by the value
 * invested to find the future value.
 */
void process (double invest, double rate, double term,
              double& multiplier, double& futureValue)
{
    multiplier = findMultiplier (rate, term);
    futureValue = multiplier * invest;
}

/*
 * The output function calls printData to print three given values.
 * It then calls printResult to print the calculated values.
 */
void output (double invest, double rate, double term,
             double multiplier, double futureValue)
{
    printData (invest, rate, term);
    printResult (multiplier, futureValue);
}

/*
 * The getInput function gets the input from the user. Its
 * only parameter is an object of type string that contains
 * a different message in each call to force the user to input
 * the appropriate data. It then validates the data and sends it back
 * to the calling expression in the input function.
 */
double getInput(string message )
{
    double input;
    do
    {
        cout << message;
        cin >> input;
    } while (input < 0.0);
    return input;
83 }
84 /**********************************************************
85  * This findMultiplier in this case needs to add all multipliers      *
86  * calculated for each year together, each with a different exponent. *
87  * The function then returns the result to the process function.      *
88  **********************************************************/
89 double findMultiplier (double rate, double term)
90 {
91     double multiplier = 0;
92     double factor = 1 + rate/100;
93     for (int i = term; i > 0; i--)
94     {
95         multiplier += pow (factor , i);
96     }
97     return multiplier;
98 }
99 /**********************************************************
100 * The printData function prints the three data items input by      *
101 * the user with appropriate explanations.                           *
102 **********************************************************/
103 void printData (double invest, double rate, double term)
104 {
105     cout << endl << "Information about period investment" << endl;
106     cout << "Periodic Investment: " << fixed << setprecision (2)
107                                      << invest << endl;
108     cout << "Interest rate: " << rate << fixed << setprecision (2);
109     cout << " percent per year" << endl;
110     cout << "Term: " << term << " years" << endl << endl;
111 }
112 /**********************************************************
113 * The printResult function prints the two results of the program.   *
114 * It prints the multiplier and the futureValue of the investment.    *
115 **********************************************************/
116 void printResult (double multiplier, double futureValue)
117 {
118     cout << "Result of investment" << endl;
119     cout << "The investment is multiplied by: " << fixed << setprecision (8);
120     cout << multiplier << endl;
121     cout << "Future value: " << fixed << setprecision(2);
122     cout << futureValue << endl;
123 }
```

```text
Run:
Enter the value of periodic investment: 12000
Enter the interest rate per year: 5
Enter the term (number of years): 30

Information about period investment
Periodic investment: 12000.00
Interest rate: 5.00 percent per year
Term: 30.00 years

Result of investment
Investment is multiplied by: 69.76078988
Future value: 837129.48
```

注意，程序 6.26 和程序 6.27 中的总投资为 360,000 美元，但第二个程序的未来值更小。这是自然的，因为当我们定期投资时，资金并非在整个期限内全额投入。

## 关键术语

- 自动局部变量
- 默认参数
- 函数
- 函数体
- 函数调用
- 函数声明
- 函数定义
- 函数头
- 函数重载
- 函数原型
- 函数作用域
- 函数遮蔽
- 函数签名
- 全局作用域
- 生命周期
- 局部作用域
- 嵌套块
- 参数列表
- 按指针传递
- 按引用传递
- 按值传递
- 作用域
- 静态局部变量
- void 函数

## 小结

函数是一个实体，由函数头和一组旨在完成某项任务的语句组成。随着程序变得越来越复杂，我们将任务划分为更小的任务，每个小任务负责工作的一部分。将任务划分为若干小任务有四个好处：更易于编写、更易于调试、可复用，并且可以保存以供将来使用。

与函数相关的有三个实体：函数定义、函数声明和函数调用。

在库函数中，定义已在 C++ 库中创建；我们只需在程序中包含相应的头文件，然后调用该函数。在用户定义函数中，我们需要声明、定义并调用该函数。

程序中的函数可能需要交换数据。我们将这种活动称为*数据传递*和*数据返回*。二者均可通过三种方法之一完成：按值、按引用或按指针。

在函数声明中，我们可以有一个或多个带预定义值的默认参数。

函数重载为同名函数提供了多个定义，但这些定义具有不同的*签名*，即参数数量不同、参数类型不同，或两者均不同。函数的返回类型不属于其签名的一部分。

作用域和生命周期是影响函数设计与使用的两个概念。作用域定义了命名实体在源代码中可见的位置。程序中的实体具有生命周期：它诞生，也会消亡。

## 习题

- **PR-1.** 找出下列每个函数声明对应的签名：

```cpp
int firstFunction (int x, float y, int z);
void secondFunction (int x, boolean y);
void thirdFunction (double x, double y);
void fourthFunction ();
```

- **PR-2.** 已知以下两个函数的声明，判断它们是否为彼此的重载版本。

```cpp
int fun (int x, int y);
void fun (int a, int b);
```

- **PR-3.** 已知以下两个函数的声明，判断它们是否为彼此的重载版本。

```cpp
int fun (int x, int y);
void fun (float a, float b);
```

- **PR-4.** 已知以下两个函数的声明，判断它们是否为彼此的重载版本。

```cpp
int fun (int x, int y, int z);
float fun (int a, int b);
```

- **PR-5.** 已知以下两个函数的声明，判断它们是否为彼此的重载版本。

```cpp
int functionOne (int x, int y);
int functionTwo (int a, int b);
```

- **PR-6.** 已知以下两个函数的声明，判断它们是否为彼此的重载版本。

```cpp
int fun ();
float fun ();
```

- **PR-7.** 找出下列有效的函数声明：

```cpp
a. float one (int a, int b);
b. boolean two (int a, int b);
c. float (int a, int b);
d. void three (void);
e. int ();
```

- **PR-15.** 调用以下函数时将返回什么？

```cpp
double test ()
{
    return 9;
}
```

- **PR-16.** 以下程序将打印什么？

```cpp
#include <iostream>
using namespace std;

int main ()
{
    int x;
    cout << x;
    return 0;
}
```

- **PR-17.** 以下程序将打印什么？

```cpp
#include <iostream>
using namespace std;

int x;

int main ()
{
    cout << x;
    return 0;
}
```

- **PR-18.** 以下程序将打印什么？

```cpp
#include <iostream>
using namespace std;

int x;

int main ()
{
    int x;
    cout << x;
}
```

- **PR-19.** 以下程序将打印什么？

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main ()
```

