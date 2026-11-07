
```cpp
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
        feetAndInchesToMetersAndCent (feet, inches,
                                      meters, centimeters);

        cout << feet << " feet (foot), "
             << inches << " inch(es) = "
             << meters << " meter(s), "
             << centimeters << " centimeter(s)." << endl;
        break;

    case 2:
        cout << "Enter meters and centimeters: ";
        cin >> meters >> centimeters;
        cout << endl;
        metersAndCentToFeetAndInches (meters, centimeters,
                                      feet, inches);
        cout << meters << " meter(s), "
             << centimeters << " centimeter(s) = "
             << feet << " feet (foot), "
             << inches << " inch(es)."
             << endl;
        break;

    case 99:
        break;

    default:
        cout << "Invalid input." << endl;
    }
}
while (choice != 99);

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

```
Enter--
1: To convert from feet and inches to meters and centimeters.
2: To convert from meters and centimeters to feet and inches.
99: To quit the program.
2

Enter meters and centimeters: 4 25

4 meter(s), 25 centimeter(s) = 13 feet (foot), 11 inch(es).
Enter--
1: To convert from feet and inches to meters and centimeters.
2: To convert from meters and centimeters to feet and inches.
99: To quit the program.
1

Enter feet and inches: 15 8

15 feet (foot), 8 inch(es) = 4 meter(s), 77 centimeter(s).
Enter--
1: To convert from feet and inches to meters and centimeters.
2: To convert from meters and centimeters to feet and inches.
99: To quit the program.
99
```

函数 main 中的 do...while 循环只要用户没有输入 99 就会继续执行，这允许用户按自己的意愿运行程序。前面的输出不言自明。

## 静态变量和自动变量

到目前为止讨论的变量遵循两条简单规则：

1. 全局变量的内存在程序执行期间始终保持分配。
2. 在块内声明的变量，其内存在进入块时分配，在退出块时释放。例如，函数的形式参数和局部变量的内存在调用函数时分配，在函数退出时释放。

在进入块时分配内存、在退出块时释放内存的变量称为**自动变量**。在程序执行期间始终保持内存分配的变量称为**静态变量**。全局变量是静态变量，默认情况下，在块内声明的变量是自动变量。可以使用保留字 `static` 在块内声明静态变量。声明静态变量的语法是：

```
static dataType identifier;
```

语句：

```
static int x;
```

将 x 声明为 `int` 类型的静态变量。

在块内声明的静态变量是该块的局部变量，其作用域与该块中任何其他局部标识符相同。

大多数编译器会将静态变量初始化为其默认值。例如，**static int** 变量被初始化为 0。然而，最好自己初始化静态变量，尤其是当初始值不是默认值时。在这种情况下，静态变量在声明时初始化。语句：

```
static int x = 0;
```

将 x 声明为 `int` 类型的静态变量，并将 x 初始化为 0。

### 示例 7-9

下面的程序展示了静态变量和自动变量的行为。

```cpp
//Program: Static and automatic variables
#include <iostream>

using namespace std;

void test();

int main()
{
    int count;

    for (count = 1; count <= 5; count++)
        test();

    return 0;
}

void test()
{
    static int x = 0;
    int y = 10;

    x = x + 2;
    y = y + 1;

    cout << "Inside test x = " << x << " and y = "
         << y << endl;
}
```

### 示例运行：

```
Inside test x = 2 and y = 11
Inside test x = 4 and y = 11
Inside test x = 6 and y = 11
Inside test x = 8 and y = 11
Inside test x = 10 and y = 11
```

在函数 test 中，x 是初始化为 0 的静态变量，y 是初始化为 10 的自动变量。函数 main 调用函数 test 五次。每次调用函数 test 时，变量 y 的内存都会被分配，并在函数退出时释放。因此，每次调用函数 test 时，它都会为 y 打印相同的值。然而，由于 x 是静态变量，x 的内存在程序执行期间始终保持分配。变量 x 只初始化一次为 0。后续对函数 test 的调用使用 x 的当前值。

由于静态变量的内存在函数调用之间始终保持分配，因此静态变量允许你在一次函数调用到另一次函数调用之间使用变量的值。尽管如果你想在一次函数调用到另一次函数调用之间使用某些值，可以使用全局变量，但静态变量的局部作用域可以防止其他函数操纵其值。

## 调试：使用驱动程序和桩函数

在本章和上一章中，你学习了如何编写函数，将问题划分为子问题，解决每个子问题，然后组合这些函数以形成完整程序，从而得到问题的解决方案。一个程序可能包含多个函数。在复杂程序中，通常编写完一个函数后，会单独测试和调试它。你可以编写一个单独的程序来测试该函数。测试函数的程序称为驱动程序。例如，示例 7-8 中的程序包含将长度从英尺和英寸转换为米和厘米以及反向转换的函数。在编写完整程序之前，你可以编写单独的驱动程序，以确保每个函数都能正常工作。

有时，一个函数计算出的结果需要在另一个函数中使用。在这种情况下，依赖于另一个函数的函数无法单独测试。例如，考虑下面这个确定注满游泳池所需时间的程序。

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

const double GALLONS_IN_A_CUBIC_FOOT = 7.48;

double poolCapacity(double len, double wid, double dep);
void poolFillTime(double len, double wid, double dep,
                  double fRate, int& fTime);
void print(int fTime);

int main()
{
    double length, width, depth;
    double fillRate;
    int fillTime;

    cout << fixed << showpoint << setprecision(2);

    cout << "Enter the length, width, and the depth of the "
         << "pool (in feet):";
    cin >> length >> width >> depth;
    cout << endl;

    cout << "Enter the rate of the water (in gallons per minute): ";
    cin >> fillRate;
    cout << endl;

    poolFillTime(length, width, depth, fillRate, fillTime);
    print(fillTime);

    return 0;
}

double poolCapacity(double len, double wid, double dep)
{
    double volume;
    double poolWaterCapacity;

    volume = len * wid * dep;
    poolWaterCapacity = volume * GALLONS_IN_A_CUBIC_FOOT;

    return poolWaterCapacity;
}
```
