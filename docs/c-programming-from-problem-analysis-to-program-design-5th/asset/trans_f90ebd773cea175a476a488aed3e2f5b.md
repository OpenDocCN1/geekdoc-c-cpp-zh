

```cpp
cout << first << " " << last << " today's temperature is: ";
    << temperature << endl;

return 0;
}
```

- 25. 变量在程序中使用之前必须采取什么操作？

- 26. 预处理指令以下列哪个符号开头：
  - a. `*`
  - b. `#`
  - c. `$`
  - d. `!`
  - e. 以上都不是。

- 27. 如果可能，写出等价的复合语句。
  - a. `x = 2 * x`
  - b. `x = x + y - 2;`
  - c. `sum = sum + num;`
  - d. `z = z * x + 2 * z;`
  - e. `y = y / (x + 5);`

- 28. 将下列复合语句写成等价的简单语句。
  - a. `x += 5 - z;`
  - b. `y *= 2 * x + 5 - z;`
  - c. `w += 2 * z + 4;`
  - d. `x -= z + y - t;`
  - e. `sum += num;`

- 29. 假设 a、b 和 c 是 int 变量，且 a = 5，b = 6。每条语句执行后，每个变量被赋予什么值？如果某个变量在特定语句处未定义，请报告 UND（未定义）。

| 语句 | a | b | c |
|---|---:|---:|---:|
| `a = (b++) + 3;` | — | — | — |
| `c = 2 * a + (++b);` | — | — | — |
| `b = 2 * (++c) - (a++);` | — | — | — |

- 30. 假设 a、b 和 sum 是 int 变量，c 是 double 变量。每条语句执行后，每个变量被赋予什么值？假设 a = 3，b = 5，c = 14.1。

| 语句 | a | b | c | sum |
|---|---:|---:|---:|---:|
| `sum = a + b + c;` | — | — | — | — |
| `c /= a;` | — | — | — | — |
| `a += c - a;` | — | — | — | — |
| `a *= 2 * b + c;` | — | — | — | — |

- 31. 下面的程序输出什么？假设输入是：

`20 15`

```cpp
#include <iostream>

using namespace std;

const int NUM = 10;
const double X = 20.5;

int main()
{
    int a, b;
    double z;
```

- 4. 重复练习 3，但将 num1、num2、num3 和 average 声明为 double 类型。将 75.35 存入 num1，-35.56 存入 num2，15.76 存入 num3。

- 5. 考虑以下 C++ 程序，其中的语句顺序不正确。重新排列这些语句，使其提示用户输入矩形的长度和宽度，并输出矩形的面积和周长。

```cpp
#include <iostream>
{
    int main()

    cout << "Enter the length: ";
    cin >> length;
    cout << endl;

    int length;

    area = length * width;

    return 0;

    int width;

    cin >> width;
    cout << "Enter the width: ";
    cout << endl;

    cout << "Area = " << area << endl;
    cout << "Perimeter = " << perimeter << endl;

    int area;
    using namespace std;
    int perimeter;
}
```

- 6. 考虑以下程序段：

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

  - a. 编写包含头文件 `iostream` 和 `string` 的 C++ 语句。
  - b. 编写一条 C++ 语句，使你可以不用前缀 `std::` 就能使用 `cin`、`cout` 和 `endl`。
  - c. 编写声明以下变量的 C++ 语句：`string` 类型的 name 和 `double` 类型的 studyHours。
  - d. 编写 C++ 语句，提示用户输入一个字符串存入 `name`，并输入一个 `double` 值存入 `studyHours`。
  - e. 编写一条 C++ 语句，输出 `name` 和 `studyHours` 的值并附上适当的文本。例如，如果 `name` 的值是 "Donald"，`studyHours` 的值是 4.5，则输出为：

Hello, Donald! On Saturday, you need to study 4.5 hours for the exam.

  - f. 编译并运行你的程序。

- 7. 编写一个程序，提示用户输入一个小数，并输出该数四舍五入到最接近的整数后的结果。

- 8. 考虑以下程序段：

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

  - a. 编写包含头文件 `iostream` 和 `string` 的 C++ 语句。
  - b. 编写一条 C++ 语句，使你可以不用前缀 `std::` 就能使用 `cin`、`cout` 和 `endl`。
  - c. 编写 C++ 语句，声明并初始化以下命名常量：`int` 类型的 SECRET 初始化为 11，`double` 类型的 RATE 初始化为 12.50。
  - d. 编写声明以下变量的 C++ 语句：`int` 类型的 `num1`、`num2` 和 `newNum`；`string` 类型的 `name`；以及 `double` 类型的 `hoursWorked` 和 `wages`。
  - e. 编写 C++ 语句，提示用户输入两个整数，并将第一个数存储在 `num1` 中，第二个数存储在 `num2` 中。
  - f. 编写一条（或几条）C++ 语句，输出 num1 和 num2 的值，并指明哪个是 num1，哪个是 num2。例如，如果 num1 是 8，num2 是 5，则输出为：

The value of num1 = 8 and the value of num2 = 5.

  - g. 编写一条 C++ 语句，将 num1 的值乘以 2，再加上 num2 的值，然后将结果存储在 newNum 中。然后，编写一条 C++ 语句输出 newNum 的值。
  - h. 编写一条 C++ 语句，将命名常量 SECRET 的值加到 newNum 上来更新 newNum 的值。然后，编写一条 C++ 语句，附上适当的信息输出 newNum 的值。
  - i. 编写 C++ 语句，提示用户输入一个人的姓氏，然后将该姓氏存储到变量 name 中。
  - j. 编写 C++ 语句，提示用户输入一个介于 0 和 70 之间的小数，然后将输入的数存储到 hoursWorked 中。
  - k. 编写一条 C++ 语句，将命名常量 RATE 的值与 hoursWorked 的值相乘，然后将结果存储到变量 wages 中。
  - l. 编写 C++ 语句，产生以下输出：

```cpp
Name:          //output the value of the variable name
Pay Rate: $    //output the value of the variable rate
Hours Worked:  //output the value of the variable hoursWorked

Salary: $      //output the value of the variable wages
```

例如，如果 name 的值是 "Rainbow"，hoursWorked 是 45.50，则输出为：

```cpp
Name: Rainbow
Pay Rate: $12.50
Hours Worked: 45.50
Salary: $568.75
```

  - m. 编写一个 C++ 程序，测试你在 a 到 l 部分编写的每一条 C++ 语句。将这些语句放在前面 C++ 程序段的适当位置。使用以下输入数据（两次）测试运行你的程序：
    - a. num1 = 13, num2 = 28; name = "Jacobson"; hoursWorked = 48.30。
    - b. num1 = 32, num2 = 15; name = "Crawford"; hoursWorked = 58.45。

- 9. 编写一个程序，提示用户输入五个测试分数，然后输出平均测试分数。（假设测试分数是小数。）

- 10. 编写一个程序，提示用户输入五个小数。程序应将这五个小数相加，将总和转换为最接近的整数，并输出结果。

- 11. 编写一个程序，执行以下操作：
  - a. 提示用户输入五个小数。
  - b. 输出这五个小数。
  - c. 将每个小数转换为最接近的整数。
  - d. 将五个整数相加。
  - e. 输出这五个整数的总和与平均值。

- 12. 编写一个程序，提示输入汽车油箱的容量（以加仑为单位）以及汽车每加仑汽油可行驶的英里数。程序输出汽车在不加油的情况下可行驶的英里数。

- 13. 编写一个 C++ 程序，提示用户输入事件经过的时间（以秒为单位）。程序然后以小时、分钟和秒输出经过的时间。（例如，如果经过的时间是 9630 秒，则输出为 2:40:30。）

- 14. 编写一个 C++ 程序，提示用户以小时、分钟和秒输入事件经过的时间。程序然后以秒输出经过的时间。

- 15. 为了盈利，当地一家商店按一定百分比加价销售商品。编写一个 C++ 程序，读取商品的原始价格、加价百分比和销售税率。程序然后输出商品的原始价格、加价百分比、商店的售价、销售税率、销售税和商品的最终价格。（商品的最终价格是售价加上销售税。）

- 16. 编写一个程序，提示用户输入以厘米表示的长度。程序应将长度转换为英寸（四舍五入到最接近的英寸），并依次以码、英尺和英寸输出长度。例如，假设输入的厘米数是 312。按最接近的英寸计算，312 厘米等于 123 英寸。因此 123 英寸应输出为：

3 yard(s), 1 feet (foot), and 3 inch(es).

- 17. 编写一个程序来实现并测试你在第 1 章练习 15 中设计的算法。（你可以假设 π = 3.141593。在你的程序中，声明一个命名常量 PI 来存储这个值。）

- 18. 一个牛奶盒可以容纳 3.78 升牛奶。每天早晨，一个奶牛场将盒装牛奶运往当地一家杂货店。生产一升牛奶的成本是 0.38 美元，每盒牛奶的利润是 0.27 美元。编写一个程序，执行以下操作：

