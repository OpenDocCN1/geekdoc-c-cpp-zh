
```cpp
case 5:
case 7:
    cout << "Odd";
    break;
}
```

27. 假设 score 是一个 int 变量。考虑以下 C++ 代码：(3, 11)

```cpp
int score;
cin >> score;
switch (score % 7)
{
case 0:
    score = score / 2 - 1;
    break;
case 1: case 3:
    score = 3 * score + 1;
    break;
case 2:
    ++score;
    break;
case 4:
    break;
case 5: case 6:
    score = score % 3;
    break;
default:
    score = score / 2;
}
cout << score << endl;
```

- a. 如果输入是 12，输出是什么？
- b. 如果输入是 4，输出是什么？
- c. 如果输入是 3，输出是什么？
- d. 如果输入是 25，输出是什么？

28. 假设 beta 是一个 int 变量。考虑以下 C++ 代码：(11)

```cpp
cin >> beta;
switch (beta % 8)
{
case 0:
case 1:
    beta = beta + beta;
    break;
case 2:
    beta--;
    break;
case 3:
case 7:
    beta = static_cast<int>(sqrt(beta * 1.0));
    beta = beta / 3;
    break;
case 4:
    beta = beta * beta;
case 5:
case 6:
    beta = 11 - beta;
    break;
default:
    beta = -5;
}

cout << beta << endl;
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_301_0.png)

- a. 如果输入是 3，输出是什么？
- b. 如果输入是 12，输出是什么？
- c. 如果输入是 15，输出是什么？
- d. 如果输入是 28，输出是什么？

**29.** 假设 num 是一个 `int` 变量。考虑以下 C++ 代码：(3, 11)

```cpp
cin >> num;
if (num >= 0)
{
    switch (num)
    {
    case 0:
        num = static_cast<int>(pow(num, 3.0));
        break;
    case 2:
        num = ++num;
        break;
    case 4:
        num = num - 4;
        break;
    case 5:
        num = num * 4;
    case 6:
        num = num / 6;
        break;
    case 10:
        num--;
        break;
    default:
        num = -20;
    }
}
else
    num = num + 10;

cout << num << endl;
```

- a. 如果输入是 5，输出是什么？
- b. 如果输入是 26，输出是什么？
- c. 如果输入是 2，输出是什么？
- d. 如果输入是 −5，输出是什么？

30. 在以下代码中，改正任何会导致程序无法编译或运行的错误：(3, 11)

```cpp
include <iostream>

main ()
{
    int num1, num2;
    bool found;

    cout << "Enter two integers: ;
    cin >> num1 >> num2;
    cout << endl;

    if (num1 >= num2) && num2 > 0
        switch (num % num2)
        {
        case 1
            found = (num / num2) >= 6;
            break;
        case 2: case 3
            num1 = num2 / 2;
            break;
        default:
            num2 = num1 * num2;
        }
    else
    {
        found = (2 * num2 < num1);
        if found
            cin >> num2
            num1 = num2 - num1;
            temp = (num1 + num2) / 10;
        if num2
        {
            num1 = num2;
            num2 = temp;
        }

        cout << num1 << " " << num2 << endl;
    }
```

改正代码后，回答以下问题。（如有需要，插入提示行以告知用户输入。）

- a. 如果输入是 10 8，输出是什么？
- b. 如果输入是 4 9，输出是什么？

31. 以下程序包含错误。改正这些错误，使程序能够运行并输出 w = 21。(3, 11)

```cpp
#include <iostream>

using namespace std;
```

34. 假设 billingAmount 是一个 double 变量，表示你需要向百货商店支付的金额。如果你全额付款，你将获得 $10.00 或 billingAmount 的 1%（以较小者为准）作为下次账单的抵扣；如果你支付至少 billingAmount 的 50%，罚金为余额的 5%；如果你支付至少 billingAmount 的 20% 且少于 billingAmount 的 50%，罚金为余额的 10%；否则，罚金为余额的 20%。设计一个算法，提示用户输入账单金额和期望付款额。然后该算法计算并输出抵扣额或剩余余额。如果未全额付款，算法还应输出罚金金额。(3)

## 编程练习

- 1. 编写一个程序，提示用户输入一个数。然后程序应输出该数，并输出一条消息说明该数是正数、负数还是零。

- 2. 编写一个程序，提示用户输入三个数。然后程序应按升序输出这些数。

- 3. 编写一个程序，提示用户输入一个 0 到 35 之间的整数。如果该数小于或等于 9，程序应输出该数；否则，对于 10 输出 A，对于 11 输出 B，对于 12 输出 C……对于 35 输出 Z。（提示：对于 >= 10 的数，使用强制类型转换运算符 static_cast<char>()。）

- 4. 以下程序中的语句顺序不正确。重新排列这些语句，使程序提示用户输入形状类型（rectangle、circle 或 cylinder）以及该形状的相应尺寸。然后程序输出以下形状信息：对于 rectangle，输出面积和周长；对于 circle，输出面积和周长；对于 cylinder，输出体积和表面积。重新排列语句后，程序应正确缩进。

```cpp
using namespace std;

#include <iostream>

int main()
{
    string shape;
    double height;

    #include <string>

    cout << "Enter the shape type: (rectangle, circle, cylinder) ";
    cin >> shape;
    cout << endl;
if (shape == "rectangle")
{
    cout << "Area of the circle = "
         << PI * pow(radius, 2.0) << endl;

    cout << "Circumference of the circle: "
         << 2 * PI * radius << endl;

    cout << "Enter the height of the cylinder: ";
    cin >> height;
    cout << endl;

    cout << "Enter the width of the rectangle: ";
    cin >> width;
    cout << endl;

    cout << "Perimeter of the rectangle = "
         << 2 * (length + width) << endl;
    double width;
}
cout << "Surface area of the cylinder: "
     << 2 * PI * radius * height + 2 * PI * pow(radius, 2.0)
     << endl;
}
else if (shape == "circle")
{
    cout << "Enter the radius of the circle: ";
    cin >> radius;
    cout << endl;

    cout << "Volume of the cylinder = "
         << PI * pow(radius, 2.0) * height << endl;
    double length;
}
return 0;
else if (shape == "cylinder")
{
    double radius;

    cout << "Enter the length of the rectangle: ";
    cin >> length;
    cout << endl;

    #include <iomanip>

    cout << "Enter the radius of the base of the cylinder: ";
    cin >> radius;
    cout << endl;
}
const double PI = 3.1416;
cout << "Area of the rectangle = "
     << length * width << endl;
else
     cout << "The program does not handle " << shape << endl;
     cout << fixed << showpoint << setprecision(2);
#include <cmath>
}
```

- 5. 在直角三角形中，一条边长度的平方等于另外两条边长度的平方和。编写一个程序，提示用户输入三角形的三条边长度，然后输出一条消息说明该三角形是否为直角三角形。

- 6. 一盒饼干可装 24 块饼干，一个容器可装 75 盒饼干。编写一个程序，提示用户输入饼干总数、每盒饼干数以及每个容器中的饼干盒数。然后程序输出运输这些饼干所需的盒数和容器数。注意，每盒必须包含指定数量的饼干，每个容器必须包含指定数量的盒子。如果最后一盒饼干包含的饼干数少于指定数量，可以丢弃它并输出剩余饼干数。类似地，如果最后一个容器包含的盒子数少于指定数量，可以丢弃它并输出剩余盒子数。

- 7. 二次方程 $ax^2 + bx + c = 0$，$a \ne 0$ 的根由以下公式给出：

$$\frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$

在该公式中，项 $b^2 - 4ac$ 称为**判别式**。如果 $b^2 - 4ac = 0$，则方程有一个（重）根。如果 $b^2 - 4ac > 0$，方程有两个实根。如果 $b^2 - 4ac < 0$，方程有两个复根。编写一个程序，提示用户输入 $a$ 的值（$x^2$ 的系数）、$b$ 的值（$x$ 的系数）和 $c$ 的值（常数项），并输出方程的根类型。此外，如果 $b^2 - 4ac \ge 0$，程序应输出二次方程的根。*（提示：使用头文件 cmath 中的函数 pow 计算平方根。第3章解释了函数 pow 的用法。）*

