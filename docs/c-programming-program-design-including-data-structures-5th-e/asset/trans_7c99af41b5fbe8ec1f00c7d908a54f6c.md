
- 15. 以下 C++ 程序的输出是什么？

```cpp
#include <iostream>
#include <cmath>

using namespace std;

int main()
{
    int counter;

    for (counter = 1; counter <= 100; counter++)
        if (pow(floor(sqrt(counter + 0.0)), 2) == counter)
            cout << counter << " ";

    cout << endl;

    return 0;
}
```

- 16. 以下程序的输出是什么？

```cpp
#include <iostream>

using namespace std;

int mystery(int x, int y, int z);

int main()
{
    cout << mystery(7, 8, 3) << endl;
    cout << mystery(10, 5, 30) << endl;
    cout << mystery(9, 12, 11) << endl;
    cout << mystery(5, 5, 8) << endl;
    cout << mystery(10, 10, 10) << endl;

    return 0;
}

int mystery(int x, int y, int z)
{
    if (x <= y && x <= z)
        return (y + z - x);
    else if (y <= z && y <= x)
        return (z + x - y);
    else
        return (x + y - z);
}
```

- 17. 编写一个函数的定义，该函数以三个数为输入，并返回前两个数之和乘以第三个数。（假设这三个数均为 double 类型。）

- 18. 写出以下程序的输出：

```cpp
#include <iostream>

using namespace std;

int mystery(int);

int main()
{
    int n;

    for (n = 1; n <= 5; n++)
        cout << mystery(n) << endl;

    return 0;
}

int mystery(int k)
{
    int x, y;

    y = k;

    for (x = 1; x <= (k - 1); x++)
        y = y * (k - x);

    return y;
}
```

## 编程练习

- 1. 编写一个程序，使用示例 6-5（回文数）中给出的函数 `isNumPalindrome`。用以下数字测试你的程序：10、34、22、333、678、67876、44444 和 123454321。

- 2. 编写一个带返回值的函数 `isVowel`，如果给定字符是元音则返回 `true`，否则返回 `false`。

- 3. 编写一个程序，提示用户输入一个字符序列，并输出其中元音的数量。（使用编程练习 2 中编写的函数 `isVowel`。）

- 4. 编写一个程序，定义命名常量 `PI`（`const double PI = 3.1419;`），用于存储 π 的值。该程序应使用 `PI` 和表 6-1 中列出的函数完成以下任务。
  - a. 输出 √π 的值。
  - b. 提示用户输入 `double` 变量 `r` 的值，该变量存储球的半径。然后程序输出以下内容：
    - i. 4πr² 的值，即球的表面积。
    - ii. (4/3)πr³ 的值，即球的体积。

- 5. 以下程序旨在求矩形的面积、圆的面积或圆柱的体积。然而，(a) 语句顺序不正确；(b) 函数调用不正确；(c) `while` 循环中的逻辑表达式不正确；(d) 函数定义不正确。重写该程序，使其正确运行。你的程序必须正确缩进。（注意，该程序是菜单驱动的，允许用户按自己的意愿反复运行程序。）

```cpp
#include <iostream>

using namespace std;

const double PI = 3.1419;

double rectangle(double l, double w);

#include <iomanip>

int main()
{
    double radius;
    double height;

    cout << fixed << showpoint << setprecision(2) << endl;
    cout << "This program can calculate the area of a rectangle, "
         << "the area of a circle, or volume of a cylinder." << endl;
    cout << "To run the program enter: " << endl;
    cout << "1: To find the area of rectangle." << endl;
    cout << "2: To find the area of a circle." << endl;
    cout << "3: To find the volume of a cylinder." << endl;
    cout << "-1: To terminate the program." << endl;
    cin >> choice;
    cout << endl;

    int choice;

    while (choice != -1)
    {
        {
        case 1:
            cout << "Enter the radius of the base and the "
                 << "height of the cylinder: ";
            cin >> radius >> height;
            cout << endl;

            cout << "Area = " << circle(length, height) << endl;
            break;

        case 3:
            double length, width;
            cout << "Enter the radius of the circle: ";
            cin >> radius;
            cout << endl;
cout << "Area = " << rectangle(radius)
     << endl;
break;

case 2:
    cout << "Enter the length and the width "
         << "of the rectangle: ";
    cin >> length >> width;
    cout << endl;

    cout << "Volume = " << cylinder(radius, height)
         << endl;
    break;
default:
    cout << "Invalid choice!" << endl;
}
switch (choice)
}

double circle(double r)
double cylinder(double bR, double h);

cout << "To run the program enter: " << endl;
cout << "2: To find the area of a circle." << endl;
cout << "1: To find the area of rectangle." << endl;
cout << "3: To find the volume of a cylinder." << endl;
cout << "-1: To terminate the program." << endl;
cin >> choice;
cout << endl;

return 0;
}

double rectangle(double l, double w)
{
    return l * r;
}

double circle(double r)
{
    return PI * r * w;
}

double cylinder(double bR, double h)
{
    return PI * bR * bR * l;
}
```

- 6. 编写一个函数 reverseDigit，它接受一个整数作为参数，并返回其数字反转后的数。例如，reverseDigit(12345) 的值为 54321；reverseDigit(5600) 的值为 65；reverseDigit(7008) 的值为 8007；reverseDigit(-532) 的值为 -235。

- 7. 修改掷骰子程序示例 6-4，使其允许用户输入想要掷出的数字之和。还允许用户按需要多次调用 `rolldice` 函数。

- 8. 以下公式给出笛卡尔平面中两点 $(x_1, y_1)$ 和 $(x_2, y_2)$ 之间的距离：

  $$\sqrt{(x_2-x_1)^2+(y_2-y_1)^2}$$

  给定圆心和圆上一点，可以使用该公式求出圆的半径。编写一个程序，提示用户输入圆心和圆上一点。然后程序应输出圆的半径、直径、周长和面积。程序至少必须包含以下函数：

  - a. `distance`：该函数以表示平面中两个点的四个数为参数，并返回它们之间的距离。
  - b. `radius`：该函数以表示圆心和圆上一点的四个数为参数，调用函数 `distance` 求圆的半径，并返回圆的半径。
  - c. `circumference`：该函数以一个表示圆半径的数为参数，并返回圆的周长。（如果 $r$ 是半径，则周长为 $2\pi r$。）
  - d. `area`：该函数以一个表示圆半径的数为参数，并返回圆的面积。（如果 $r$ 是半径，则面积为 $\pi r^2$。）

  假设 $\pi = 3.1416$。

- 9. 重写第 4 章编程练习 15（手机公司）中的程序，使其使用以下函数计算账单金额。（在本编程练习中，不要输出使用服务的分钟数。）
  - a. `regularBill`：该函数计算并返回常规服务的账单金额。
  - b. `premiumBill`：该函数计算并返回优质服务的账单金额。

- 10. 编写一个程序，输入五个数，并输出这些数的均值（平均数）和标准差。如果这些数是 $x_1$、$x_2$、$x_3$、$x_4$ 和 $x_5$，则均值为 $x = (x_1 + x_2 + x_3 + x_4 + x_5)/5$，标准差为：

  $$s = \sqrt{\frac{(x_1-x)^2+(x_2-x)^2+(x_3-x)^2+(x_4-x)^2+(x_5-x)^2}{5}}$$

  你的程序至少必须包含以下函数：一个计算并返回均值的函数，以及一个计算标准差的函数。

- 11. 当你借钱买房、买车或用于其他目的时，通常通过定期还款来偿还。假设贷款金额为 \(L\)，\(r\) 是年利率，\(m\) 是一年中的还款次数，贷款期限为 \(t\) 年。假设 \(i=(r/m)\)，且 \(r\) 为小数形式。则定期还款额为：

  $$R=\frac{Li}{1-(1+i)^{-mt}}.$$

  你也可以计算进行某些还款后的未偿还贷款余额。例如，进行 \(k\) 次还款后的未偿还余额为：

  $$L'=R\left[\frac{1-(1+i)^{-(mt-k)}}{i}\right],$$

  其中 \(R\) 是定期还款额。（注意，如果按月还款，则 \(m=12\)。）

  编写一个程序，提示用户输入 \(L\)、\(r\)、\(m\)、\(t\) 和 \(k\) 的值。然后程序输出相应的值。你的程序至少必须包含两个函数，并带有适当的参数，用于计算定期还款额和某些还款后的未偿还余额。使程序采用菜单驱动，并使用循环，以便用户可针对不同值重复运行程序。

- 12. 在报税季，每周五，J&J 会计师事务所为自行准备纳税申报表的人提供协助。其收费如下：
  - a. 如果某人为低收入（≤ $25,000）且咨询时间小于或等于 30 分钟，则不收费；否则，超过 30 分钟的部分按正常小时费率的 40% 收取服务费。
  - b. 对于其他人，如果咨询时间小于或等于 20 分钟，则不收取服务费；否则，超过 20 分钟的部分按正常小时费率的 70% 收取服务费。

  （例如，假设某人为低收入，花费 1 小时 15 分钟，小时费率为 $70.00。则账单金额为 70.00 × 0.40 × (45 / 60) = $21.00。）

  编写一个程序，提示用户输入小时费率、总咨询时间以及该人是否为低收入。程序应输出账单金额。你的程序必须包含一个函数，该函数以小时费率、总咨询时间和表示该人是否为低收入的值为输入。该函数应返回账单金额。你的程序可以提示用户以分钟为单位输入咨询时间。

