

```cpp
cout << height << " " << weight << endl;

discount = (2 * height + weight) % 10.0
price = 49.99;

billingAmount = price * (1 - discount) - DECIMAL ;
DECIMAL = 7.55;

cout << price << blanks << "$" << billingAmount << endl;

bonus = hoursWorked * PAY_RATE / 50;

cout << "Bonus = " << bonus << endl;

}
return 0;
```

- **23.** 以下程序存在语法错误。请改正它们。在后续每一行中，假设前面所有错误都已改正。(12)

```cpp
const char * STAR = '*'
const int PRIME = 71;

int main
{
    int count, sum;
    double x;

    count = 1;
    sum = count + PRIME;
    x = 25.67
    newNum = count + ONE + 2;
    sum + count + sum;
    (x + sum)++;
    x = x + sum * COUNT;
    sum += 3 - ;
    cout << " count = " << count << ", sum = " << sum
         << ", PRIME = " << Prime << endl;
}
```

- **24.** 以下程序存在语法错误和/或语句顺序不正确。请改正它们。在后续每一行中，假设前面所有错误都已改正。(12)

```cpp
using namespace std;

#include <iostream>

int main()
{
    int num1, num2;
    string str1;

    cout << "Enter a string without any blanks in it ";
    cin >> string;
    cout << endl;

    cout << "Enter two integers: ";
    cin << num1, num2;
    cout << endl;

    return 0;

    cout << str1 << " "
         << "num1 * num2 = " << num1 * num2 << endl
}
```

- **25.** 在程序中使用变量之前，必须采取哪些操作？(7)

- **26.** 预处理指令以以下哪个符号开头？(12)

  - a. `*`
  - b. `#`
  - c. `$`
  - d. `!`
  - e. 以上都不是。

- **27.** 如果可能，编写等价的复合语句。(14)

  - a. `x = x + 5;`
  - b. `x = 2 * x * y;`
  - c. `totalPay = totalPay + currentPay;`
  - d. `z = z * x + 2 * z;`
  - e. `y = y / (x + 5);`

- **28.** 将以下复合语句改写为等价的简单语句。(14)

  - a. `x += 5 - z;`
  - b. `y *= 2 * x + 5 - z;`
  - c. `w += 2 * z + 4;`
  - d. `x -= z + y - t;`
  - e. `sum += num;`

- **29.** 假设 a、b 和 c 是 `int` 变量，且 a = 7、b = 2。每条语句执行时，各变量被赋了什么值？如果某个变量在某条语句处未定义，请报告 UND（未定义）。(6, 9)

| 语句 | a | b | c |
|---|---|---|---|
| `a = ++b + 5;` | ___ | ___ | ___ |
| `c = a + b-- + 1;` | ___ | ___ | ___ |
| `b = (a++) - (--c);` | ___ | ___ | ___ |

![](img/b217c421655b51e7494cf3b89bb5432d_160_0.png)

- **30.** 假设 a、b 和 sum 是 int 变量，c 是 double 变量。每条语句执行后，各变量被赋了什么值？假设 a = 6、b = 3、c = 2.2。(14)

| 语句 | a | b | c | sum |
| --- | --- | --- | --- | --- |
| `sum = static_cast<int>(a + b + c);` | — | — | — | — |
| `b += c * a;` | — | — | — | — |
| `c -= a;` | — | — | — | — |
| `a *= 2 * b - c;` | — | — | — | — |

- **31.** 以下程序会输出什么？假设输入为：

35 10.5 27 B

```cpp
#include <iostream>

using namespace std;

const int NUM = 10;
const double X = 20.5;

int main()
{
    int firstNum, secondNum;
    double z;
    char grade;

    firstNum = 62;

    cout << "firstNum = " << firstNum << endl;

    cout << "Enter three numbers: ";
    cin >> firstNum >> z >> secondNum;
    cout << endl;

    cout << "The numbers you entered are "
         << firstNum << ", " << z << ", and "
         << secondNum << endl;

    z = z - X + 2 * firstNum - secondNum;
    cout << "z = " << z << endl;

    cout << "Enter grade: ";
    cin >> grade;
    cout << endl;

    cout << "The letter that follows your grade is: "
         << static_cast<char>(static_cast<int>(grade) + 1)
         << endl;

    return 0;
}
```

```cpp
int main()
{
    string employeeID;
    string department;
    int num;
    double salary;

    cout << "Enter employee ID: ";
    cin >> employeeID;
    cout << endl;

    cout << "Enter department: ";
    cin >> department;
    cout << endl;

    cout << "Enter a positive integer less than 80: ";
    cin >> num;
    cout << endl;

    salary = num * X;
    cout << "ID: " << employeeID << endl;
    cout << "Star: " << STAR << endl;
    cout << "Wages: $" << salary << endl;
    cout << "X = " << X << endl;
    cout << "X+Y = " << X + Y << endl;

    return 0;
}
```

- **34.** 以下程序需要什么类型的输入，以及需要按什么顺序提供输入？(8, 10, 11)

```cpp
#include <iostream>

using namespace std;

int main()
{
    int invoiceNumber;
    double salesTaxRate;
    double productPrice;
    string productName;

    cin >> productName;
    cin >> salesTaxRate >> productPrice;
    cin >> invoiceNumber;

    return 0;
}
```

## 编程练习

- **1.** 编写一个程序，产生以下输出：

```text
*****************************
* Programming Assignment 1    *
* Computer Programming I      *
*         Author: ???         *
* Due Date: Thursday, Jan. 24 *
*****************************
```

在你的程序中，用你自己的姓名替换 ???。如有必要，调整星号的位置和数量以生成一个矩形。

- **2.** 编写一个程序，产生以下输出：

```text
ccccccccc        ++                 ++
cc               ++                 ++
cc          ++++++++++++++++    ++++++++++++++++
cc          ++++++++++++++++    ++++++++++++++++
cc               ++                 ++
cc               ++                 ++
ccccccccc        ++                 ++
```

- **3.** 考虑以下程序段：

```cpp
//include statement(s)
//using namespace statement

int main()
{
    //variable declaration

    //executable statements

    //return statement
}
```

  - a. 编写一条包含头文件 iostream 的 C++ 语句。
  - b. 编写一条 C++ 语句，使你无需使用前缀 std:: 即可使用 cin、cout 和 endl。
  - c. 编写 C++ 语句，声明以下变量：类型为 int 的 num1、num2、num3 和 average。
  - d. 编写 C++ 语句，将 125 存入 num1，将 28 存入 num2，将 -25 存入 num3。
  - e. 编写一条 C++ 语句，将 num1、num2 和 num3 的平均值存入 average。
  - f. 编写 C++ 语句，输出 num1、num2、num3 和 average 的值。
  - g. 编译并运行你的程序。

- **4.** 重复编程练习 3，但将 num1、num2 和 num3 以及 average 声明为 double 类型。将 75.35 存入 num1，将 -35.56 存入 num2，将 15.76 存入 num3。

- **5.** 考虑以下 C++ 程序，其中语句的顺序不正确。重新排列这些语句，使其提示用户输入圆的半径，并输出该圆的面积和周长。

```cpp
#include <iostream>
{
    int main()

    cout << "Enter the radius: ";
    cin >> radius;
    cout << endl;

    double radius;
    double area;

    using namespace std;

    return 0;

    cout << "Area = " << area << endl;

    area = PI * radius * radius;

    circumference = 2 * PI * radius;

    cout << "Circumference = " << circumference << endl;

    const double PI = 3.14;

    double circumference;
}
```

- **6.** 考虑以下程序段：

```cpp
//include statement(s)
//using namespace statement

int main()
{
    //variable declaration

    //executable statements

    //return statement
}
```

  - a. 编写 C++ 语句，包含头文件 `iostream` 和 `string`。
  - b. 编写一条 C++ 语句，使你无需使用前缀 `std::` 即可使用 `cin`、`cout` 和 `endl`。
  - c. 编写 C++ 语句，声明以下变量：类型为 `string` 的 `name` 和类型为 `double` 的 `studyHours`。
  - d. 编写 C++ 语句，提示并将一个字符串输入到 `name`，将一个 `double` 值输入到 `studyHours`。
  - e. 编写一条 C++ 语句，用合适的文本输出 `name` 和 `studyHours` 的值。例如，如果 name 的值为 "Donald"、studyHours 的值为 4.5，则输出为：

    你好，Donald！星期六你需要为考试学习 4.5 小时。

  - f. 编译并运行你的程序。

- **7.** 编写一个程序，提示用户输入一个十进制数，并输出四舍五入到最接近整数的结果。

- **8.** 考虑以下程序段：

```cpp
//include statement(s)
//using namespace statement
int main()
{
    //variable declaration
    //executable statements
    //return statement
}
```

  - a. 编写 C++ 语句，包含头文件 `iostream` 和 `string`。
  - b. 编写一条 C++ 语句，使你无需使用前缀 `std::` 即可使用 `cin`、`cout` 和 `endl`。
  - c. 编写 C++ 语句，声明并初始化以下具名常量：类型为 `int`、初始化为 11 的 `SECRET`，以及类型为 `double`、初始化为 12.50 的 `RATE`。
  - d. 编写 C++ 语句，声明以下变量：类型为 `int` 的 `num1`、`num2` 和 `newNum`；类型为 `string` 的 `name`；以及类型为 `double` 的 `hoursWorked` 和 `wages`。
  - e. 编写 C++ 语句，提示用户输入两个整数，并将第一个数存入 `num1`，第二个数存入 `num2`。
  - f. 编写 C++ 语句，输出 `num1` 和 `num2` 的值，并指明哪个是 `num1`、哪个是 `num2`。例如，如果 `num1` 为 8、`num2` 为 5，则输出为：

    num1 的值为 8，num2 的值为 5。

  - g. 编写一条 C++ 语句，将 `num1` 的值乘以 2，再加上 `num2` 的值，然后将结果存入 `newNum`。然后，编写一条输出 `newNum` 值的 C++ 语句。
  - h. 编写一条 C++ 语句，通过将具名常量 `SECRET` 的值加到 `newNum` 上来更新 `newNum` 的值。然后，编写一条带合适消息输出 `newNum` 值的 C++ 语句。
  - i. 编写 C++ 语句，提示用户输入一个人的姓氏，然后将该姓氏存入变量 `name`。

