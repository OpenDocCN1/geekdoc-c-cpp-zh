
要输出尾随零，可以使用操纵符 showpoint。以下语句将带小数点和尾随零的十进制数输出到标准输出设备：

```cpp
cout << showpoint;
```

当然，以下语句将浮点数以带小数点和尾随零的定点十进制格式输出到标准输出设备：

```cpp
cout << fixed << showpoint;
```

示例 3-11 中的程序说明了如何使用操纵符 setprecision、fixed 和 showpoint。

### 示例 3-11

```cpp
//Example: setprecision, fixed, showpoint
#include <iostream>                              //Line 1
#include <iomanip>                               //Line 2

using namespace std;                             //Line 3

const double PI = 3.14159265;                    //Line 4

int main()                                         //Line 5
{
    double radius = 12.67;                        //Line 7
    double height = 12.00;                        //Line 8

    cout << fixed << showpoint;                   //Line 9

    cout << setprecision(2)
         << "Line 10: setprecision(2)" << endl;  //Line 10
    cout << "Line 11: radius = " << radius << endl; //Line 11
    cout << "Line 12: height = " << height << endl; //Line 12
    cout << "Line 13: volume = "
         << PI * radius * radius * height << endl; //Line 13
    cout << "Line 14: PI = " << PI << endl;       //Line 14

    cout << setprecision(3)
         << "Line 15: setprecision(3)" << endl;  //Line 15
    cout << "Line 16: radius = " << radius << endl; //Line 16
    cout << "Line 17: height = " << height << endl; //Line 17
    cout << "Line 18: volume = "
         << PI * radius * radius * height << endl; //Line 18
    cout << "Line 19: PI = " << PI << endl;       //Line 19

    cout << setprecision(4)
         << "Line 20: setprecision(4)" << endl;  //Line 20
    cout << "Line 21: radius = " << radius << endl; //Line 21
    cout << "Line 22: height = " << height << endl; //Line 22
    cout << "Line 23: volume = "
         << PI * radius * radius * height << endl;   //Line 23
    cout << "Line 24: PI = " << PI << endl << endl;   //Line 24

    cout << "Line 25: "
         << setprecision(3) << radius << ", "
         << setprecision(2) << height << ", "
         << setprecision(5) << PI << endl;             //Line 25

    return 0;                                           //Line 26
}                                                   //Line 27
```

### 示例运行：

```text
Line 10: setprecision(2)
Line 11: radius = 12.67
Line 12: height = 12.00
Line 13: volume = 6051.80
Line 14: PI = 3.14

Line 15: setprecision(3)
Line 16: radius = 12.670
Line 17: height = 12.000
Line 18: volume = 6051.797
Line 19: PI = 3.142

Line 20: setprecision(4)
Line 21: radius = 12.6700
Line 22: height = 12.0000
Line 23: volume = 6051.7969
Line 24: PI = 3.1416

Line 25: 12.670, 12.00, 3.14159
```

在此程序中，第 2 行的语句包含头文件 iomanip，第 4 行的语句声明命名常量 PI 并将其值设置为八位小数。第 7 行和第 8 行的语句声明并初始化变量 radius 和 height，以存储圆柱底面的半径和圆柱的高度。第 9 行的语句将浮点数设置为以带小数点和尾随零的定点十进制格式输出。

第 11、12、13 和 14 行的语句将 radius、height、volume 和 PI 的值输出到两位小数。

第 16、17、18 和 19 行的语句将 radius、height、volume 和 PI 的值输出到三位小数。

第 21、22、23 和 24 行的语句将 radius、height、volume 和 PI 的值输出到四位小数。

第 25 行的语句将 radius 的值输出到三位小数，将 height 的值输出到两位小数，将 PI 的值输出到五位小数。

请注意 radius 的值在第 11、16 和 21 行中是如何打印的。第 16 行打印的 radius 值包含一个尾随 0。这是因为 radius 的存储值只有两位小数；第三位小数处会打印一个 0。类似地，height 的值在第 12、17 和 22 行中打印。

另外，请注意第 13、18 和 23 行的语句如何计算 volume 并将其分别输出到两位、三位和四位小数。

注意，第 24 行打印的 PI 值经过了舍入。

第 25 行的语句首先将浮点数的输出设置为三位小数，然后将 radius 的值输出到三位小数。在打印 radius 的值之后，第 25 行的语句将浮点数的输出设置为两位小数，然后将 height 的值输出到两位小数。接着，它将浮点数的输出设置为五位小数，然后将 PI 的值输出到五位小数。

如果省略第 9 行的语句并重新编译和运行程序，你将看到十进制数的默认输出。更具体地说，计算 volume 的表达式值可能会以科学计数法打印。

## setw

操纵符 setw 用于按指定的列数输出表达式的值。表达式的值可以是字符串或数字。表达式 `setw(n)` 在 n 列中输出下一个表达式的值。输出为右对齐。因此，例如，如果将列数指定为 8，而输出只需要四列，则前四列留空。此外，如果指定的列数小于输出所需的列数，输出会自动扩展到所需的列数；输出不会被截断。例如，如果 x 是 `int` 变量，以下语句在标准输出设备上以五列输出 x 的值：

```cpp
cout << setw(5) << x << endl;
```

要使用操纵符 setw，程序必须包含头文件 iomanip。因此，需要以下 `include` 语句：

```cpp
#include <iomanip>
```

与 setprecision 不同（它控制所有浮点数的输出，直到被重置），setw 只控制下一个表达式的输出。

### 示例 3-12

```cpp
//Example: setw

#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    int x = 19;                        //Line 1
    int a = 345;                       //Line 2
    double y = 76.384;                 //Line 3

    cout << fixed << showpoint;        //Line 4

    cout << "12345678901234567890" << endl; //Line 5

    cout << setw(5) << x << endl;      //Line 6
    cout << setw(5) << a << setw(5) << "Hi"
         << setw(5) << x << endl << endl; //Line 7

    cout << setprecision(2);           //Line 8
    cout << setw(6) << a << setw(6) << y
         << setw(6) << x << endl;      //Line 9
    cout << setw(6) << x << setw(6) << a
         << setw(6) << y << endl << endl; //Line 10

    cout << setw(5) << a << x << endl; //Line 11
    cout << setw(2) << a << setw(4) << x << endl; //Line 12

    return 0;
}
```

### 示例运行：

```text
12345678901234567890
   19
  345   Hi   19

   345 76.38    19
    19   345 76.38

  34519
345  19
```

第 1、2 和 3 行的语句声明变量 x、a 和 y，并分别将这些变量初始化为 19、345 和 76.384。第 4 行的语句将浮点数设置为以带小数点和尾随零的定点十进制格式输出。第 5 行的语句输出显示了打印特定值时的列位置；它是输出的第一行。

第 6 行的语句以五列输出 x 的值。因为 x 只有两位数字，所以只需要两列来输出其值。因此，在输出的第二行中，前三列留空。第 7 行的语句在前五列输出 a 的值，在接下来的五列输出字符串 "Hi"，然后在随后的五列输出 x 的值。因为字符串 "Hi" 只包含两个字符，而设置了五列来输出这两个字符，所以前三列留空。参见
