
$-b - \sqrt{b^2 - 4c}$ 必须能被 2 整除。下面的函数将 b 和 c 的值作为参数，并返回 u 和 v 的值，同时指出该多项式是否可因式分解。

```cpp
void factorization(int b, int c, int& u1, int& v1, bool& isFactorable)
{
    double discriminant;
    int temp;

    isFactorable = true;

    discriminant = b * b - 4 * c;

    if (discriminant < 0)
        isFactorable = false;
    else
    {
        temp = static_cast<int>(sqrt(discriminant));

        if (temp * temp != discriminant)
            isFactorable = false;
        else
        {
            if (((-b + temp) % 2 != 0) || ((-b - temp) % 2 != 0))
                isFactorable = false;
            else
            {
                u1 = (-b + temp) / 2;
                v1 = (-b - temp) / 2;
            }
        }
    }
}
```

下面的程序展示了如何在程序中使用函数 factorization。

```cpp
//Program: Second degree polynomial factorization

#include <iostream>
#include <cmath>

using namespace std;

void factorization(int b, int c, int& u1, int& v1, bool& isFactorable);

int main()
{
    int coeffOfX;
    int constantTerm;
    int u;
    int v;
    bool isPolynomialFactorable;

    cout << "Enter the coefficient of x: ";
    cin >> coeffOfX;
    cout << endl;

    cout << "Enter the constant term: ";
    cin >> constantTerm;
    cout << endl;

    factorization(coeffOfX, constantTerm, u, v,
                  isPolynomialFactorable);

    if (isPolynomialFactorable)
    {
        cout << "x^2";

        if (coeffOfX > 0)
            cout << " + " << coeffOfX << "x";
        else if (coeffOfX < 0)
            cout << " - " << abs(coeffOfX) << "x";

        if (constantTerm > 0)
            cout << " + " << constantTerm;
        else if (constantTerm < 0)
            cout << " - " << abs(constantTerm);

        cout << " = (x";

        if (u > 0)
            cout << " - " << u << ")(x";
        else if (u < 0)
            cout << " + " << abs(u) << ")(x";

        if (v > 0)
            cout << " - " << v << ")" << endl;
        else if (v < 0)
            cout << " + " << abs(v) << ")" << endl;
    }
    else
        cout << "The polynomial is not factorable." << endl;

    return 0;
}
```

```cpp
//Place the definition of the function factorization here.
```

**示例运行：** 在这些示例运行中，用户输入以阴影显示。

**示例运行 1：**

输入 x 的系数：`5`
输入常数项：`6`
x^2 + 5x + 6 = (x + 3)(x + 2)

**示例运行 2：**

输入 x 的系数：`0`
输入常数项：`-25`
x^2 - 25 = (x - 5)(x + 5)

**示例运行 3：**

```text
Enter the coefficient of x: 8
Enter the constant term: 16
x^2 + 8x + 16 = (x + 4)(x + 4)
```

**示例运行 4：**

```text
Enter the coefficient of x: -13
Enter the constant term: 20
The polynomial is not factorable.
```

### 示例 6-17（菜单驱动程序）

下面是一个菜单驱动程序的示例。程序执行时，会向用户提供一个可供选择的选项列表。该程序进一步说明了值参数和引用参数如何工作。它将长度从英尺和英寸转换为米和厘米，反之亦然。该程序包含三个函数：showChoices、feetAndInchesToMetersAndCent 和 metersAndCentToFeetAndInches。函数 showChoices 告知用户如何使用该程序。用户可以根据自己的意愿多次运行该程序。

```cpp
//Menu driven program.

#include <iostream>

using namespace std;

const double CONVERSION = 2.54;
const int INCHES_IN_FOOT = 12;
const int CENTIMETERS_IN_METER = 100;

void showChoices();

void feetAndInchesToMetersAndCent(int f, int in,
                                  int& mt, int& ct);
void metersAndCentToFeetAndInches(int mt, int ct,
                                  int& f, int& in);

int main()
{
    int feet, inches;
    int meters, centimeters;
    int choice;

    do
    {
        showChoices();
        cin >> choice;
        cout << endl;

        switch (choice)
        {
        case 1:
            cout << "Enter feet and inches: ";
            cin >> feet >> inches;
            cout << endl;
            feetAndInchesToMetersAndCent(feet, inches,
                                         meters, centimeters);

            cout << feet << " feet(foot), "
                 << inches << " inch(es) = "
                 << meters << " meter(s), "
                 << centimeters << " centimeter(s)." << endl;
            break;

        case 2:
            cout << "Enter meters and centimeters: ";
            cin >> meters >> centimeters;
            cout << endl;
            metersAndCentToFeetAndInches(meters, centimeters,
                                         feet, inches);

            cout << meters << " meter(s), "
                 << centimeters << " centimeter(s) = "
                 << feet << " feet(foot), "
                 << inches << " inch(es)."
                 << endl;
            break;

        case 99:
            break;

        default:
            cout << "Invalid input." << endl;
        }
    } while (choice != 99);

    return 0;
}

void showChoices()
{
    cout << "Enter--" << endl;
    cout << "1: To convert from feet and inches to meters "
         << "and centimeters." << endl;
    cout << "2: To convert from meters and centimeters to feet "
         << "and inches." << endl;
    cout << "99: To quit the program." << endl;
}

void feetAndInchesToMetersAndCent(int f, int in,
                                  int& mt, int& ct)
{
    int inches;

    inches = f * INCHES_IN_FOOT + in;
    ct = static_cast<int>(inches * CONVERSION);
    mt = ct / CENTIMETERS_IN_METER;
    ct = ct % CENTIMETERS_IN_METER;
}

void metersAndCentToFeetAndInches(int mt, int ct,
                                  int& f, int& in)
{
    int centimeters;

    centimeters = mt * CENTIMETERS_IN_METER + ct;
    in = static_cast<int>(centimeters / CONVERSION);
    f = in / INCHES_IN_FOOT;
    in = in % INCHES_IN_FOOT;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Enter--
1: To convert from feet and inches to meters and centimeters.
2: To convert from meters and centimeters to feet and inches.
99: To quit the program.
2

Enter meters and centimeters: 6 28

6 meter(s), 28 centimeter(s) = 20 feet(foot), 7 inch(es).
Enter--
1: To convert from feet and inches to meters and centimeters.
2: To convert from meters and centimeters to feet and inches.
99: To quit the program.
1

Enter feet and inches: 18 7

18 feet(foot), 7 inch(es) = 5 meter(s), 66 centimeter(s).
Enter--
1: To convert from feet and inches to meters and centimeters.
2: To convert from meters and centimeters to feet and inches.
99: To quit the program.
99
```

函数 main 中的 do...while 循环在用户未输入 99 时会继续执行，这允许用户按自己的意愿多次运行程序。前面的输出不言自明。

## 静态变量和自动变量

到目前为止讨论的变量遵循两条简单规则：

- 1. 只要程序执行，全局变量的内存就保持分配状态。
- 2. 在块内声明的变量的内存会在进入块时分配，并在退出块时释放。例如，函数的形参和局部变量的内存会在调用函数时分配，并在函数退出时释放。

在进入块时分配内存、在退出块时释放内存的变量称为**自动变量**。只要程序执行就保持内存分配的变量称为**静态变量**。全局变量是静态变量；默认情况下，在块内声明的变量是自动变量。可以使用保留字 `static` 在块内声明静态变量。声明静态变量的语法是：

```cpp
static dataType identifier;
```

语句：

```cpp
static int x;
```

将 x 声明为 int 类型的静态变量。

在块内声明的静态变量是该块的局部变量，其作用域与该块中任何其他局部标识符的作用域相同。

大多数编译器会将 `static` 变量初始化为其默认值。例如，`static int` 变量会被初始化为 0。不过，最好自行初始化 `static` 变量，尤其是当初始值不是默认值时。在这种情况下，`static` 变量会在声明时初始化。语句：

```cpp
static int x = 0;
```

将 x 声明为 int 类型的静态变量，并在第一次调用函数时将 x 初始化为 0。

### 示例 6-18

下面的程序展示了静态变量和自动变量的行为。

```cpp
//Program: Static and automatic variables
#include <iostream>

using namespace std;

void test();
```
