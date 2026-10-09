
![](img/0c86cf81300257fe2415e40f8fb03508_125_0.png)

这里是之前的示例 4.25 - `value_of_inputs.cpp` 的改进版本，它使用 `good()` 成员函数来在计算机期望接收整数时阻止任何文本值通过：

## 示例 4.27 - `validate_two_numbers.cpp`

```cpp
#include <iostream>    // 程序将使用屏幕和键盘

using namespace std;      // 将使用标准标识符 cin, cout, endl

int main()
{
    int errorCode = 0;      // 表示完全没有遇到任何错误

    int firstInt, secondInt, sum;

    // 请求用户输入第一个整数
    cout << "Enter 1st integer...";
    cin >> firstInt;

    // 检查第一个整数是否接受
    if (cin.good())
    {
        // 请求用户输入第二个整数
        cout << "Enter 2nd integer...";
        cin >> secondInt;

        // 检查第二个整数是否接受
        if (cin.good())
        {
            // 两个输入均已 - 继续处理数据。

            // 将两个整数相加并存储结果
            sum = firstInt + secondInt;

            // 在屏幕上显示结果
            cout << "The sum of the integers is " << sum << endl;
        }
        else
        {
            cout << "Sorry. The second input was not a number." << endl;
            errorCode = 2;      // 表示第二个数字出了问题
            // 完成第二个输入的检查
        }
    }
    else
    {
        cout << "Sorry. The first input was not a number." << endl;
        errorCode = 1;      // 表示第一个数字出了问题
        // 完成第一个输入的检查
    }

    return errorCode;      // 让 Linux 知道数据是否有效
}
```

程序是如何运行的？在输入第一个值后，通过调用 `cin.good()` 函数对该值进行检查。这决定了第一个值是否是一个接受的数字。

如果第一个值是有效的，程序将提示用户输入第二个值。它调用 `cin.good()` 来检查这个第二个值是否为有效数字。

如果发现第二个值也是一个有效数字，那么两个输入都已输入 —— 继续处理数据。

将两个整数相加并存储结果

`sum = firstInt + secondInt;`

在屏幕上显示结果

`cout << "The sum of the integers is " << sum << endl;`

然而，如果发现任何一个值无效，则会设置 `errorCode` 的值。

# 供你尝试的问题和练习

| 1. | 编写一个程序，让你输入一个整数。使用 `setw()` 将数字的宽度更改为 1、5 和 10 个字符，并显示三次数字。 |
| 2. | 编写一个程序，要求你输入一个句子。显示三次句子，每次使用不同的颜色。 |
| 3. | 编写一个程序，要求你输入一个整数。让程序在执行结束前等待该数字对应的秒数。 |
| 4. | 编写一个程序，要求你每次输入一个数字。让它显示这三个数字的总和。 |

## 第 5 章：

### 使用运算符处理数据

## 使用 ++ 增运算符和 -- 减运算符改变变量的值

我们之前已经见过如何使用 `=` 赋值运算符将变量的值设置为存储一个字面量。

还有其他设置数值型变量值的方法，包括针对整数和浮点数的方法。与其给变量设置一个特定值，你还可以根据变量当前的值来更改它的值。你可以将表达式的结果赋值给变量，如下所示：

```
livesLeft = livesLeft + 1;
```

上述语句的意思是：

> "将 `livesLeft` 变量的值设置为 `livesLeft` 当前的值，并在此基础上加 1。"

注意 `livesLeft + 1` 是一个简单的表达式，它结合了命名值 `livesLeft`、`+` 运算符和字面量 `1`。

## 使用 ++ 增运算符向值上加 1

C++ 还有另一种给变量值加 1 的简单方法，称为增运算符：`++`

而不是编写：

```
livesLeft = livesLeft + 1;
```

...你可以使用增运算符让 `livesLeft` 变量的值加 1：

```
livesLeft++;
```

## 使用 -- 减运算符从值上减去 1

C++ 还有一个运算符可以从变量的值中减去 1，称为减运算符：`--`

而不是编写：

```
livesLeft = livesLeft - 1;
```

...你可以使用减运算符让 `livesLeft` 变量的值减少 1：

```
livesLeft--;
```

## 使用 ++ 增运算符和 -- 减运算符的不同方法

`++` 增运算符和 `--` 减运算符都可以以不同的方式工作，这取决于你将它们放置在相对于操作的变量名的什么位置。你可以选择将运算符放在变量名的之前或之后。

## 作为独立语句的自增

记住 `++` 运算符会将变量的值加 1。在这里，它被用作一个简单的语句来增加名为 `people` 的变量的值：

```
int people = 5;
people++;
cout << people << endl;
```

第一行代码创建了一个名为 `people` 值为 5 的整数变量。然后它增加了了 `people` 的值，将其从 5 变为 6。最后，最后一行代码显示变量的值，显示为 6。

## 前置增，作为另一个语句的一部分

在下面的示例中，增运算符被嵌入到用于显示变量值的语句中，从而减少了一行代码：

```
int people = 5;
cout << ++people << endl;
```

第一行代码创建了名为 `people` 的变量，与第一个示例一样。下一行代码将在屏幕上显示变量的值，但在使用该变量之前，`++` 运算符会将其值加 1。然后它继续使用更改后的值，在屏幕上显示 6。

当你将 `++` 运算符放在变量名之前时，它被称为**前置增运算符**。变量的值在使用之前会先加 1。

## 后置增，作为另一个语句的一部分

```
int people = 5;
cout << people++ << endl;
```

这段代码的作用是创建一个值为 5 的整数变量。它会显示变量，在屏幕上显示值 5。一旦变量被使用，它就会增加该值，将其从 5 变为 6。

当你将 `++` 运算符放在变量名之后时，它被称为**后置增运算符**。变量的值只有在使用后才会加 1。

## 前置减和后置减作为另一个语句的一部分

与 `++` 增运算符一样，你可以将 `--` 减运算符放在所操作的变量名的之前或之后。这些被称为前置减和后置减操作。

## += "加量" 和 -= "减量" 运算符

`++` 增运算符给变量的值加 1，而 `--` 运算符减去 1。

你如何加或减去 1 以外的不同数字呢？

你可以编写这样的语句：

```
playerScore = playerScore + 100;
```

这告诉计算机为变量 `playerScore` 设置一个新值，使其等于 `playerScore` 的旧值并额外加 100。

或者，你可以使用 `+=` 加量运算符在变量当前值上加上特定的数，或使用 `-=` 减量运算符减去特定的数：

```
playerScore += 100;
time -= 30;
```

## 使用 * 运算符相乘

值可以使用 `*` 运算符相乘。

例如，这些语句中的每一个定义了一个变量等于相乘的结果：

```
bonus = timeLeft * 10;
areaOfRectangle = width * height;
areaOfCircle = pi * radius * radius;
```

使用 `*`（星号）而不是人们通常在纸上使用的 x 交叉是为了避免与字母 "x" 混淆。

你可以相乘相同类型的值，例如将整数相乘：

```
int hoursInOneWeek = 7 * 24;
```

你也可以相乘不同类型的值，例如将一个 `float` 值乘以一个 `int` 值：

```
float dailyPay = 8.25 * 6;
```

在示例中，浮点值 8.25 乘以整数值 6。由于被相乘的值之一是一个使用小数点的值，编译器将假设结果也需要小数点，因此结果也将是一个浮点值而不是整数。出于此原因，变量 `dailyPay` 使用 `float` 数据类型声明。

```cpp
// 使用它们进行计算并显示结果

cout << "There are ";

cout << DAYS * HOURS;

cout << " hours in a week." << endl;

cout << "There are ";

cout << HOURS * MINUTES;

cout << " minutes in a day." << endl;

return 0;
```

在上述代码中，常量 `DAYS` 的值为 7，常量 `HOURS` 的值为 24。

语句：

```cpp
cout << DAYS * HOURS;
```

...显示了 7 乘以 24 的结果，即 168 小时。

同样，常量 `MINUTES` 的值为 60，因此语句：

```cpp
cout << HOURS * MINUTES;
```

...显示了 24 乘以 60 的结果，即 1440 分钟。

![](img/0c86cf81300257fe2415e40f8fb03508_136_0.png)

## 使用 / 运算符进行数字除法

你可以使用 `/` 除法运算符将一个数值除以另一个数值。

## 示例 5.3 - `divide.cpp`

```cpp
#include <iostream> // 程序将使用屏幕和键盘

using namespace std; // 将使用标准标识 cin, cout, endl

int main()
{
    cout << "What is the top part of the fraction?" << endl;
    int top;
    cin >> top;
    // -----

    cout << "What is the bottom part of the fraction?" << endl;
    int bottom;
    cin >> bottom;
    // -----

    cout << "As a decimal value, your fraction is: " << endl;
    float asDecimalValue = top / bottom;

    cout << asDecimalValue;
    cout << endl << endl;

    return 0;
}
```

运行此程序可能会产生一些意料之外的结果。10 / 5 得到答案 2，这是正确的，但你可能会发现 1 / 2 得到的答案是 0 而不是 0.5。这是因为计算机忽略了小数点后的数字，因为它认为自己正在处理纯整数。

# 强制转换 - 将值转换为不同的数据类型

解决问题的方法是告诉计算机在执行除法之前，将分子和分母值都视为 `float`。这种不同数据类型之间的转换被称为“强制转换”（cast）。

```cpp
float asDecimalValue = (float) top / (float) bottom;
```

在上述语句中，`(float)` 强制计算机将分子和分母变量视为 `float` 而不是 `int` 值，因此计算机不会丢弃小数值。

强制转换将在本章稍后详细介绍，你会发现从一种数据类型转换为另一种数据类型时，使用 `static_cast` 关键字是最佳实践。

# 示例计算 - UNIX生日快乐

这是一个利用了本章涵盖的许多要点的示例。它检查树莓派上的时间，以确定自“UNIX 时间”（定义为 1970 年 1 月 1 日）以来已经过去了多少秒。

## 示例 5.4 - `calc_age.cpp`

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本
#include <ctime> // 程序使用 time() 函数作为随机种子

using namespace std; // 将使用标准标识符 cout 和 endl

int main() {
    const float DAYS_IN_YR = 365.25;
    const int HRS_IN_DAY = 24;
    const int MIN_IN_HR = 60;
    const int SECS_IN_MIN = 60;

    // 计算 1 年有多少秒...
    const float SECS_IN_YEAR = SECS_IN_MIN * MIN_IN_HR * HRS_IN_DAY * DAYS_IN_YR;

    // 找出 UNIX 的年龄（以秒为单位给出）
    int ageOfInSeconds = time(0 );

    // 将此除以一年的秒数，
    //这将是以年为单位的 UNIX 年，而不是秒...
    cout << "Unix is " << ageOfInSeconds / SECS_IN_YEAR <<
    cout << " years old." << endl;

    return 0;
}
```

程序将显示此结果：

> Unix is 57 years old。（注：OCR 文字在此处输出乱码，但逻辑是一致的）

# 浮点除法的结果

当你尝试用一个整数除以一个实数（例如浮点值 0.5）时会发生什么？

示例 5.7 - `int_by_float.cpp`

```cpp
#include <iostream>    // 程序将在屏幕上显示一些文本
using namespace std; // 将使用标准标识符 cout 和 endl
int main()
{
    int distance = 10;
    float half = 0.5;

    cout << "How many times does " << half;
    cout << " go into " << distance;
    cout << " ? ";

    cout << distance / half;
    cout << endl << endl;

    float third = 0.333333;

    cout << "How many times does " << third;
    cout << " go into " << distance;
    cout << " ? ";

    cout << distance / third;
    cout << endl << endl;

    return 0;
}
```

这一次，结果显示为：

![](img/0c86cf81300257fe2415e40f8fb03508_141_0.png)

计算机在屏幕上的两个结果中都没有显示任何小数位。如果你用手持计算器尝试第二个示例，你实际上可能会看到结果 30.00003（或非常相似的结果，取决于你计算器的精度）。

最后，这个程序说明了一个实数除以另一个实数时发生的情况：

## 示例 5.8 - `float_by_float.cpp`

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本
using namespace std; // 将使用标准标识符 cout 和 endl

int main()
{
    float myNumber = 2.5;
    float half = 0.5;

    cout << "How many times does " << half;
    cout << "go into " << myNumber;
    cout << " ?";

    cout << myNumber / half;
    cout << endl << endl;

    float threeQuarters = 0.75;

    cout << "How many times does " << threeQuarters;
    cout << "go into " << myNumber;
    cout << " ?";

    cout << endl << endl;

    return 0;
}
```

屏幕上显示的结果如下：

| 0.5 可以除入 2.5 几次？ | 5 |
| 0.75 可以除入 2.5 几次？ | 3.33333 |

因为 2.5 / 0.5 得到的答案是一个精确的数字，所以小数点后不会显示任何不必要的 0。只有在确实需要时才会显示小数位，例如上面截图中的第二次除法，其结果是循环的 3.33333。

## 使用模运算符寻找余数

例如，我们知道 16 / 3 的结果是 5，因为 3 除入 16 中恰好有 5 次，留下了 1 的余数。

为了找到余数，我们可以使用 `%` 取模运算符。

```
16 % 3 意味着“找到16 除以 3 的余数”。

结果是 1，因为 16 除以 3 等于 5，余数为 1。
```

![](img/0c86cf81300257fe2415e40f8fb03508_143_0.png)

以下是运行时的情况：

| 盒子里有多少块巧克力？ | 16 |
