
你使用 `setprecision` 操纵符配合 `cout` 和插入运算符。例如，以下语句：

```cpp
cout << setprecision(2);
```

会将十进制数的输出格式化为两位小数，直到后续类似的语句改变精度。注意，小数位数（即精度值）作为参数传递给 `setprecision`。

要使用操纵符 `setprecision`，程序必须包含头文件 `iomanip`。因此，需要以下包含语句：

```cpp
#include <iomanip>
```

## `fixed` 操纵符

要进一步控制浮点数的输出，可以使用其他操纵符。要以定点十进制格式输出浮点数，可使用操纵符 `fixed`。以下语句将标准输出设备上浮点数的输出设置为定点十进制格式：

```cpp
cout << fixed;
```

执行上述语句后，所有浮点数都将以定点十进制格式显示，直到禁用操纵符 `fixed`。可以使用流成员函数 `unsetf` 禁用操纵符 `fixed`。例如，要在标准输出设备上禁用操纵符 `fixed`，可使用以下语句：

```cpp
cout.unsetf(ios::fixed);
```

禁用操纵符 `fixed` 后，浮点数的输出将恢复为默认设置。操纵符 `scientific` 用于以科学计数法格式输出浮点数。

> **注意**
>
> 在某些编译器上，语句 `cin >> fixed;` 和 `cin >> scientific;` 可能无法正常工作。在这种情况下，可以使用 `cin.setf(ios::fixed);` 代替 `cin >> fixed;`，并使用 `cin.setf(ios::scientific);` 代替 `cin >> scientific;`。

以下示例展示了在不使用操纵符 `setprecision` 时，操纵符 `scientific` 和 `fixed` 如何工作。

### 示例 3-10

```cpp
//Example: scientific and fixed

#include <iostream>

using namespace std;

int main()
{
    double hours = 35.45;
    double rate = 15.00;
    double tolerance = 0.01000;

    cout << "hours = " << hours << ", rate = " << rate
         << ", pay = " << hours * rate
         << ", tolerance = " << tolerance << endl << endl;

    cout << scientific;
    cout << "Scientific notation: " << endl;
    cout << "hours = " << hours << ", rate = " << rate
         << ", pay = " << hours * rate
         << ", tolerance = " << tolerance << endl << endl;

    cout << fixed;
    cout << "Fixed decimal notation: " << endl;
    cout << "hours = " << hours << ", rate = " << rate
         << ", pay = " << hours * rate
         << ", tolerance = " << tolerance << endl << endl;

    return 0;
}
```

### 示例运行结果

```text
hours = 35.45, rate = 15, pay = 531.75, tolerance = 0.01

Scientific notation:
hours = 3.545000e+001, rate = 1.500000e+001, pay = 5.317500e+002, tolerance = 1.000000e-002

Fixed decimal notation:
hours = 35.450000, rate = 15.000000, pay = 531.750000, tolerance = 0.010000
```

示例运行结果表明，当未设置 scientific 或 fixed 操纵符而打印 rate 和 tolerance 的值时，不会显示末尾零；对于 rate，小数点也不会显示。设置操纵符后，这些值将打印为六位小数。下一节将介绍操纵符 showpoint，用于强制系统显示小数点和末尾零。然后给出一个示例，展示如何使用操纵符 setprecision、fixed 和 showpoint 获得所需输出。

## `showpoint` 操纵符

假设一个十进制数的小数部分为零。在这种情况下，当你指示计算机以定点十进制格式输出该十进制数时，输出可能不会显示小数点和末尾零。要强制输出显示小数点和末尾零，可使用操纵符 `showpoint`。以下语句将标准输出设备上十进制数的输出设置为带小数点和末尾零：

```cpp
cout << showpoint;
```

当然，以下语句将标准输出设备上浮点数的输出设置为带小数点和末尾零的定点十进制格式：

```cpp
cout << fixed << showpoint;
```

示例 3-11 中的程序说明了如何使用操纵符 `setprecision`、`fixed` 和 `showpoint`。

### 示例 3-11

```cpp
//Example: setprecision, fixed, showpoint

#include <iostream>                                      //Line 1
#include <iomanip>                                       //Line 2

using namespace std;                                     //Line 3

const double PI = 3.14159265;                            //Line 4

int main()                                               //Line 5
{                                                        //Line 6
    double radius = 12.67;                               //Line 7
    double height = 12.00;                               //Line 8

    cout << fixed << showpoint;                          //Line 9

    cout << setprecision(2)
         << "Line 10: setprecision(2) " << endl;        //Line 10
    cout << "Line 11: radius = " << radius << endl;     //Line 11
    cout << "Line 12: height = " << height << endl;     //Line 12
    cout << "Line 13: volume = "
         << PI * radius * radius * height << endl;       //Line 13
    cout << "Line 14: PI = " << PI << endl;             //Line 14

    cout << setprecision(3)
         << "Line 15: setprecision(3) " << endl;        //Line 15
    cout << "Line 16: radius = " << radius << endl;     //Line 16
    cout << "Line 17: height = " << height << endl;     //Line 17
    cout << "Line 18: volume = "
         << PI * radius * radius * height << endl;       //Line 18
    cout << "Line 19: PI = " << PI << endl;             //Line 19

    cout << setprecision(4)
         << "Line 20: setprecision(4) " << endl;        //Line 20
    cout << "Line 21: radius = " << radius << endl;     //Line 21
    cout << "Line 22: height = " << height << endl;     //Line 22
    cout << "Line 23: volume = "
         << PI * radius * radius * height << endl;       //Line 23
    cout << "Line 24: PI = " << PI << endl << endl;     //Line 24

    cout << "Line 25: "
         << setprecision(3) << radius << ", "
         << setprecision(2) << height << ", "
         << setprecision(5) << PI << endl;              //Line 25

    return 0;                                            //Line 26
}                                                        //Line 27
```

### 示例运行结果

```text
Line 10: setprecision(2)
Line 11: radius = 12.67
Line 12: height = 12.00
Line 13: volume = 6051.80
Line 14: PI = 3.14

Line 15: setprecision(3)
Line 16: radius = 12.670
Line 17: height = 12.00
Line 18: volume = 6051.797
Line 19: PI = 3.142

Line 20: setprecision(4)
Line 21: radius = 12.6700
Line 22: height = 12.0000
Line 23: volume = 6051.7969
Line 24: PI = 3.1416

Line 25: 12.670, 12.00, 3.14159
```

在该程序中，第 2 行的语句包含头文件 `iomanip`，第 4 行的语句声明命名常量 `PI` 并将其值设置为八位小数。第 7 行和第 8 行的语句声明并初始化变量 `radius` 和 `height`，用于存储圆柱体底面的半径和圆柱体的高度。第 10 行的语句将浮点数的输出设置为带小数点和末尾零的定点十进制格式。

第 11、12、13 和 14 行的语句将 `radius`、`height`、体积和 `PI` 的值输出为两位小数。

第 16、17、18 和 19 行的语句将 `radius`、`height`、体积和 `PI` 的值输出为三位小数。

第 21、22、23 和 24 行的语句将 `radius`、`height`、体积和 `PI` 的值输出为四位小数。

第 25 行的语句将 `radius` 的值输出为三位小数，将 `height` 的值输出为两位小数，将 `PI` 的值输出为五位小数。

