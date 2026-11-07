
26. 判断以下是否为有效的 `switch` 语句。如果不是，请解释原因。假设 `n` 和 `digit` 是 `int` 变量。(11)

a.

```cpp
switch (n <= 2)
{
    case 0:
        cout << "Draw." << endl;
        break;
    case 1:
        cout << "Win." << endl;
        break;
    case 2:
        cout << "Lose." << endl;
        break;
}
```

b.

```cpp
switch (digit / 4)
{
    case 0:
    case 1:
        cout << "low." << endl;
        break;
    case 1:
    case 2:
        cout << "middle." << endl;
        break;
    case 3:
        cout << "high." << endl;
}
```

c.

```cpp
switch (n % 6)
{
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        cout << n;
        break;
    case 0:
        cout << endl;
        break;
}
```

d.

```cpp
switch (n % 10)
    case 2:
    {
    case 4:
    case 6:
    case 8:
        cout << "Even";
        break;
    case 1:
    case 3:
    case 5:
    case 7:
        cout << "Odd";
        break;
    }
```

27. 假设 alpha 是 int 变量。考虑以下 C++ 代码。(3, 11)

```cpp
cin >> alpha;
switch (alpha % 9)
{
case 0: case 3:
    alpha = alpha / 3;
    break;
case 1: case 5: case 7:
    alpha = alpha / 2;
    break;
case 2: case 4:
    ++alpha;
    break;
case 6:
    alpha = (alpha / 9) * (alpha / 9);
    break;
case 8:
    alpha = (alpha % 9) * (alpha % 9);
    break;
default:
    alpha--;
}
cout << alpha << endl;
```

- a. 如果输入为 16，输出是什么？

- b. 如果输入为 8，输出是什么？

- c. 如果输入为 1，输出是什么？

- d. 如果输入为 25，输出是什么？

28. 假设 `beta` 是 `int` 变量。考虑以下 C++ 代码。(11)

```cpp
cin >> beta;
switch (beta % 10)
{
case 0: case 1:
    beta = beta - 2;
    break;
case 2: case 8:
    beta = beta + beta;
    break;
case 3: case 5:
    beta--;
    break;
case 6: case 7:
    beta = static_cast<int>(pow(beta, 3.0));
    break;
case 4: case 9:
    beta = static_cast<int>(sqrt(beta * 1.0));
    break;
default:
    beta = -5;
}
cout << beta << endl;
```

- a. 如果输入为 4，输出是什么？

- b. 如果输入为 23，输出是什么？

- c. 如果输入为 1，输出是什么？

- d. 如果输入为 89，输出是什么？

29. 假设 `num` 是 `int` 变量。考虑以下 C++ 代码。(3, 11)

```cpp
cin >> num;
if (num >= 0)
    switch (num % 3)
    {
    case 0:
        num--;
        break;
    case 1:
        ++num;
        break;
    case 2:
        num = static_cast<int>(pow(num, 3.0));
        break;
    }
else
{
    num = -num;
    num = static_cast<int>(sqrt(num * 1.0));
}
cout << num << endl;
```

- a. 如果输入为 7，输出是什么？

- b. 如果输入为 23，输出是什么？

- c. 如果输入为 20，输出是什么？

- d. 如果输入为 -9，输出是什么？

30. 在以下代码中，不添加新语句，改正任何会阻止程序编译或运行的错误。(3, 11)

```cpp
#include <iostream>

using namespace;

int main
{
    int num1, num2;
    bool found = false;

    cout << "Enter two integers: ";
    cin >> num1 >> num2;
    cout << endl;

    found = (num1 > num2);

    if (found
        switch (num1 % num2);
        {
        case 0:
            num2 = num1 / 2;
            break;
        case 1:
            num1 = num2 / 2;
            break;
        default:
            num1 = num1 / num2;
            num2 = num1 * num2;
        };
    else
    {
        num1 = num1 - num2;
        num2 = (num1 + num2) / 10;
    }

    cout << num1 << " " << num2 << endl;

    return;
}
```

改正代码后，回答以下问题。（如有需要，可插入提示行来告知用户输入。）

- a. 如果输入为 `16 5`，输出是什么？

- b. 如果输入为 `13 27`，输出是什么？

31. 以下程序包含错误。改正这些错误，使程序能够运行并输出 `w = 25`。(3, 11)

```cpp
#include <iostream>

using namespace std;

const int SECRET = 5

main ()
{
        int x, y, w, z;
        z == 13;

        if (z < 15);
                x = 12; y = 8, w = x + y + SECRET;
        else
                x = 12; y = 8, w = x + y + SECRET;

        cout << "w = " << w << endl;
}
```

32. 在以下程序中编写缺失的语句，使其提示用户输入两个数。如果其中一个数为 0 或负数，程序输出两个数都必须为正数。如果两个数相等，则输出这两个数之和；如果第一个数小于或等于 2 且两个数不相等，则输出第二个数的第一个数次幂；否则输出这两个数的乘积。(3)

```cpp
#include <iostream>
//Include additional header files, if necessary

using namespace std;

int main()
{
        double firstNum, secondNum;

        cout << "Enter two nonzero numbers: ";
        cin >> firstNum >> secondNum;
        cout << endl;

        //Missing statements

        return 0;
}
```

33. 假设 `classStanding` 是 char 变量，`gpa` 和 `dues` 是 double 变量。编写一个 `switch` 表达式，按如下方式分配会费：如果 `classStanding` 为 `'f'`，会费为 $150.00；如果 `classStanding` 为 `'s'`，（如果 gpa 至少为 3.75，会费为 $75.00；否则会费为 $120.00）；如果 `classStanding` 为 `'j'`，（如果 gpa 至少为 3.75，会费为 $50.00；否则会费为 $100.00）；如果 `classStanding` 为 `'n'`，（如果 gpa 至少为 3.75，会费为 $25.00；否则会费为 $75.00）。（注意，代码 `'f'` 代表一年级学生，代码 `'s'` 代表二年级学生，代码 `'j'` 代表三年级学生，代码 `'n'` 代表四年级学生。）(3)

34. 假设 `billingAmount` 是 double 变量，表示你需要向百货商店支付的金额。如果你全额支付，你可获得 $10.00 或 `billingAmount` 的 1%（以较小者为准），作为下一期账单的抵扣额；如果你支付至少 `billingAmount` 的 50%，罚金为余额的 5%；如果你支付至少 `billingAmount` 的 20% 且少于 `billingAmount` 的 50%，罚金为余额的 10%；否则罚金为余额的 20%。设计一个算法，提示用户输入账单金额和期望支付金额。然后该算法计算并输出抵扣额或剩余余额。如果未全额支付，算法还应输出罚金金额。(3)

## 编程练习

- 1. 编写一个程序，提示用户输入一个数。然后程序应输出该数，并输出一条消息说明该数是正数、负数还是零。

- 2. 编写一个程序，提示用户输入三个数。然后程序应按升序输出这些数。

- 3. 编写一个程序，提示用户输入一个 0 到 35 之间的整数。如果该数小于或等于 9，程序应输出该数；否则，对于 10 应输出 A，11 应输出 B，12 应输出 C，……，35 应输出 Z。（提示：对于大于等于 10 的数，使用强制类型转换运算符 `static_cast<char>()`。）

- 4. 以下程序中的语句顺序不正确。重新排列这些语句，使其提示用户输入形状类型（矩形、圆形或圆柱体）以及该形状的相应尺寸。然后程序输出以下关于该形状的信息：对于矩形，输出面积和周长；对于圆形，输出面积和周长；对于圆柱体，输出体积和表面积。重新排列语句后，程序应正确缩进。

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
         << PI * pow(radius, 2.0)* height << endl;
    double length;
}
return 0;
```
