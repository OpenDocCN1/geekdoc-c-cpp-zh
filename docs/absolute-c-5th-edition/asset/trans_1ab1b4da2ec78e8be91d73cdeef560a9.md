

# 范围规则 133

> 提示：（续上）

在分支中定义函数并放置函数调用。同样，如果循环体很大，最好是将复合语句转换为一个函数定义，并将循环体变为一个函数调用。

# 在 for 循环中声明的变量

变量可以在 `for` 语句的头部中声明，这样该变量在 `for` 语句开始时就同时被声明和初始化。例如，

```cpp
for (int n = 1; n < 10; n++)
sum = sum + n;
```

ANSI/ISO C++ 标准要求声称符合该标准的 C++ 编译器将 `for` 初始化器中的任何声明处理为等同于在循环体中执行的声明。早期的 C++ 编译器并没有这样做。你应该确定你的编译器如何处理在 `for` 初始化器中声明的变量。如果移植性对你的应用程序至关重要，则你不应该编写依赖于此行为的代码。最终，所有广泛使用的 C++ 编译器都可能遵守这一点，但目前的编译器可能遵守，也可能不遵守。

# 自测练习

25. 我们敦促你不要使用这种风格进行编程，我们提供了一个使用嵌套块的练习，帮助你理解范围规则。请说明这段代码段在一个原本完整、正确的程序中会产生什么输出。

```cpp
{
  int x = 1;
  cout << x << endl;
  cout << x << endl;
  int x = 2;
  cout << x << endl;
  {
    cout << x << endl;
    int x = 3;
    cout << x << endl;
  }
  cout << x << endl;
}
cout << x << endl;
}
```

# 本章总结

- C++ 中有两种函数：返回值的函数和 `void` 函数。

- 函数的定义应该使其能够像黑盒一样被使用。使用该函数的程序员不需要了解关于函数代码实现的任何细节。程序员只需要知道函数的声明以及描述返回值的随附注释。这一规则有时被称为过程抽象原则。

- 编写函数声明注释的一种好方法是使用前置条件（precondition）和后置条件（postcondition）。前置条件说明了调用函数时假设为真的条件。后置条件描述了函数调用的影响；即后置条件告诉，在前置条件成立的情况下，执行函数后将会变成什么情况。

- 在函数定义中声明的变量被称为函数的局部变量。

- 形式参数是一种占位符，在调用函数时用实形参数填充。关于此“填充”过程的细节将在第 4 章中介绍。

# 自测练习答案

- 1. 4.0 4.0 8.0
8.0 8.0 1.21
3 3 0
3.0 3.5 3.5
6.0 6.0 5.0
5.0 4.5 4.5
3 3.0 3

- 2. a. sqrt (x + y)
b. pow(x, y + 7)
c. sqrt (area+time)/nobody
d. sqrt ((b ± sqrt(b*b - 4*a*c))/(2*a))
e. abs (x - y) or labs (x - y) or fabs (x - y)

```cpp
3. #include <iostream>
#include <cmath>
using namespace std;
int main()
{
    int i;
for (i = 1; i <= 10; i++)
cout << "The square root of " << i
cout << " is " << sqrt(i) << endl;
return 0;
}
```

- 4. 参数被传递给操作系统。对于你的 C++ 程序而言，你可以使用任何值作为参数。然而，通过转换，对于由错误引起的 `exit` 调用使用 1，而在其他情况下使用 0。

- 5. (5 + (rand() % 6))

- 6. #include <iostream>
#include <cstdlib>
using namespace std;

int main() {

cout << "Enter a nonnegative integer to use as the \n"
<< "_seed for the random number generator: \n"
unsigned int seed;
cin >> seed;
srand(seed);

cout << "Here are ten random probabilities:\n"
int i;
for (i = 0; i < 10; i++)
cout << (RAND_MAX - rand())/static_cast<double>(RAND_MAX) << endl;

return 0;
}

```

- 8. 函数声明为：

```cpp
int sum(int n1, int n2, int n3);
// 返回 n1, n2 和 n3 的和；
```

定义为：

```cpp
int sum(int n1, int n2, int n3) {

return (n1 + n2 + n3);
}
```

- 9. 函数声明为：

```cpp
char positiveTest(double number);
// 如果 number 为正，返回 'P'。
// 如果 number 为负或零，返回 'N'。
```

函数定义为：

```cpp
char positiveTest(double number) {
    if (number > 0)
        return 'P';
    else
        return 'N';
}
```

- 10. 不能，函数定义不能出现在另一个函数定义的体内部。

- 11. 预定义函数和用户定义函数的调用方式是相同的。

- 12. bool inOrder(int n1, int n2, int n3)
    return (n1 <= n2) && (n2 <= n3);

- 13. bool even(int n)
    return (n % 2) == 0;

- 14. bool isDigit(char ch)
    return ('0' <= ch) && (ch <= '9');

- 15. Hello
Goodbye
One more time:
Hello
End of program.

- 16. 如果你在显示 3.7 中为 `iceCreamDivision` 的函数定义中省略了 `return` 语句，程序将编译并运行。然而，如果你输入的客户数量为零，程序将因为除以零而产生运行时错误。

- 17. #include <iostream>
    using namespace std;
    void productOut(int n1, int n2, int n3);

```cpp
int main() {
    int num1, num2, num3;
    cout << "Enter three integers: ";
    cin >> num1 >> num2 >> num3;
    productOut(num1, num2, num3);
    return 0;
}
```

# 自测练习答案 137

```cpp
void productOut(int n1, int n2, int n3) {
  cout << "The product of the three numbers "
       << n1 << ", " << n2 << ", and"
       << n3 << " is " << (n1*n2*n3) << endl;
}
```

18. 这些答案取决于系统。

```cpp
19. double sqrt(double n);
// 前置条件：n >= 0。
// 返回 n 的平方根。
```

如果你喜欢，可以按如下重写第二行注释，但之前的版本是返回值的函数的常用形式：

// 后置条件：返回 n 的平方根

20. 如果你输入的客户数量为零，程序将编译并运行。然而，如果你输入的客户数量为零，程序将因为除以零产生运行时错误。

21. 过程抽象原则认为函数的定义应该使其能够像黑盒一样被使用。使用该函数的程序员不需要了解关于函数代码实现的任何细节。

22. 定义函数和用户定义函数的调用方式是相同的。

23. 当我们说函数应该被视为黑盒时，意味着程序员不需要查看函数的体。

24. 在下文中，我们将这些变量重命名为 x1, x2 和 x3。

```cpp
int x1 = 1; // 输出
cout << x1 << endl; // 第1行
{
  cout << x1 << endl; // 第1行
int x2 = 2;
```

# 138 第3章 函数基础

```cpp
cout << x2 << endl; // 第2行
{
  cout << x2 << endl; // 第2行
int x3 = 3;
cout << x3 << endl; // 第3行
}
```

# 我的编程项目

访问 www.myprogramming.com 选择练习并获取即时反馈。

- 1. 1升等于0.264179加仑。编写一个程序读取用户消耗的升数和行驶里程，然后输出汽车每加仑数。你的程序应该允许用户重复此计算。定义一个函数来计算每加仑数。你的程序应该使用全局定义的常量来表示加仑。
- 2. 写一个程序来衡量过去一年的胀率。程序询问物品（如热狗或克拉钻石）一年前和今天的价格。它将通胀率估计为价格除以年前的价格。你的程序应该允许用户重复此计算。定义一个函数来计算通胀率。通胀率应该是double类型，以百分比形式给出，例如5.3表示5.3%。
- 3. 增强你之前的程序，输出物品在计算时间后一年和两预计价格。一年的成本增加估计为通胀率乘以年初的价格。定义第二个函数来确定指定年份后的物品预计成本，将物品当前价格和通胀率作为参数。
- 4. 两个质量分别为 $m1$ 和 $m2$ 的物体在距离 $d$ 之间的引力由以下公式给出，

```
$F = \frac{Gm_1m_2}{d^2}
```

其中 $G$ 是通用引力常数：
$G=6.673\times 10^{-8} \text{cm}^3/(g\cdot\text{sec}^2)$

编写一个函数，接收两个物体质量和它们之间距离的参数，并返回它们之间的引力。

