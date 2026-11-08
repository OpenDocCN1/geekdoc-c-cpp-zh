

```cpp
using namespace std;

int main()
{
    int x = 19;                              //Line 1
    int a = 345;                             //Line 2
    double y = 76.384;                       //Line 3

    cout << fixed << showpoint;              //Line 4

    cout << "12345678901234567890" << endl;  //Line 5

    cout << setw(5) << x << endl;            //Line 6
    cout << setw(5) << a << setw(5) << "Hi"
         << setw(5) << x << endl;            //Line 7

    cout << setprecision(2);                 //Line 8
    cout << setw(6) << a << setw(6) << y
         << setw(6) << x << endl;            //Line 9
    cout << setw(6) << x << setw(6) << a
         << setw(6) << y << endl;            //Line 10

    cout << setw(5) << a << x << endl;       //Line 11
    cout << setw(2) << a << setw(4) << x << endl; //Line 12

    return 0;
}
```

### 示例运行：

```text
12345678901234567890
       19
      345   Hi    19

     345  76.38     19
       19     345  76.38

34519
345  19
```

第 1、2、3 行中的语句声明变量 x、a 和 y，并分别将这些变量初始化为 19、345 和 76.384。第 4 行中的语句将浮点数的输出设置为带小数点和尾随零的定点十进制格式。第 5 行语句的输出显示了打印这些特定值时的列位置；它是输出的第一行。

第 6 行中的语句在五列中输出 x 的值。因为 x 只有两位数，所以输出其值只需要两列。因此，在输出的第二行中，前三列留空。第 7 行中的语句在前五列中输出 a 的值，在接下来的五列中输出字符串 "Hi"，然后在随后的五列中输出 x 的值。因为字符串 "Hi" 只包含两个字符，而设置了五列来输出这两个字符，所以前三列留空。操纵符 `setfill` 将标准输出设备上的填充字符设置为 `'#'`。

要使用操纵符 `setfill`，程序必须包含头文件 `iomanip`。

示例 3-13 中的程序说明了在程序中使用 `setfill` 的效果。

### 示例 3-13

```cpp
//Example: setfill

#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    int x = 15;                                      //Line 1
    int y = 7634;                                    //Line 2

    cout << "12345678901234567890" << endl;         //Line 3
    cout << setw(5) << x << setw(7) << y
         << setw(8) << "Warm" << endl;              //Line 4

    cout << setfill('*');                            //Line 5
    cout << setw(5) << x << setw(7) << y
         << setw(8) << "Warm" << endl;              //Line 6

    cout << setw(5) << x << setw(7) << setfill('#')
         << y << setw(8) << "Warm" << endl;         //Line 7

    cout << setw(5) << setfill('@') << x
         << setw(7) << setfill('#') << y
         << setw(8) << setfill('^') << "Warm"
         << endl;                                    //Line 8
    cout << setfill(' ');                            //Line 9
    cout << setw(5) << x << setw(7) << y
         << setw(8) << "Warm" << endl;              //Line 10

    return 0;
}
```

### 示例运行：

```text
12345678901234567890
     15  7634     Warm
***15***7634****Warm
@@@15###7634^^^^Warm
     15  7634     Warm
```

第 1 行和第 2 行中的语句声明变量 x 和 y，并分别将它们初始化为 15 和 7634。第 3 行语句的输出——即输出的第一行——显示了后续语句输出变量值时的列位置。第 4 行中的语句在五列中输出 x 的值，在七列中输出 y 的值，在八列中输出字符串 "Warm"。在这条语句中，填充字符是空白字符，如输出的第二行所示。

第 5 行中的语句将填充字符设置为 *。第 6 行中的语句在五列中输出 x 的值，在七列中输出 y 的值，在八列中输出字符串 "Warm"。因为 x 是两位数，而分配了五列来输出其值，所以前三列未被 x 使用，因此由填充字符 * 填充。为了打印 y 的值，分配了七列；然而 y 是四位数，所以填充字符填充前三列。类似地，为了打印字符串 "Warm" 的值，分配了八列；字符串 "Warm" 只有四个字符，所以填充字符填充前四列。参见输出的第三行。

第 7 行语句的输出——即输出的第四行——与第 6 行语句的输出类似，不同之处在于 x 和字符串 "Warm" 的填充字符是 #。在第 8 行语句的输出（输出的第五行）中，x 的填充字符是 @，y 的填充字符是 #，字符串 "Warm" 的填充字符是 ^。操纵符 setfill 设置这些填充字符。

第 9 行中的语句将填充字符设置为空白。第 10 行中的语句使用空白填充字符输出 x、y 和字符串 "Warm" 的值，如输出的第六行所示。

## left 和 right 操纵符

回想一下，如果 setw 操纵符中指定的列数超过下一个表达式所需的列数，默认输出是右对齐的。有时，你可能希望输出左对齐。要使输出左对齐，可以使用 left 操纵符。

设置 left 操纵符的语法是：

```cpp
ostreamVar << left;
```

其中 ostreamVar 是输出流变量。例如，以下语句将标准输出设备上的输出设置为左对齐：

```cpp
cout << left;
```

可以使用流函数 unsetf 禁用 left 操纵符。禁用 left 操纵符的语法是：

```cpp
ostreamVar.unsetf(ios::left);
```

其中 ostreamVar 是输出流变量。禁用 left 操纵符会使输出恢复为默认输出格式的设置。例如，以下语句在标准输出设备上禁用 left 操纵符：

```cpp
cout.unsetf(ios::left);
```

设置 right 操纵符的语法是：

```cpp
ostreamVar << right;
```

其中 ostreamVar 是输出流变量。例如，以下语句将标准输出设备上的输出设置为右对齐：

```cpp
cout << right;
```

> **注意**
>
> 在某些编译器上，语句 `cin>> left;` 和 `cin>> right;` 可能不起作用。在这种情况下，可以使用 `cin.setf(ios::left);` 代替 `cin>> left;`，并使用 `cin.setf(ios::right);` 代替 `cin>> right;`

示例 3-14 中的程序说明了 left 和 right 操纵符的效果。

### 示例 3-14

```cpp
//Example: left justification

#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    int x = 15;                           //Line 1
    int y = 7634;                         //Line 2

    cout << left;                         //Line 3

    cout << "12345678901234567890" << endl;   //Line 4
    cout << setw(5) << x << setw(7) << y      //Line 5
         << setw(8) << "Warm" << endl;

    cout << setfill('*');                 //Line 6

    cout << setw(5) << x << setw(7) << y      //Line 7
         << setw(8) << "Warm" << endl;

    cout << setw(5) << x << setw(7) << setfill('*') //Line 8
         << y << setw(8) << "Warm" << endl;

    cout << setw(5) << setfill('@') << x
         << setw(7) << setfill('#') << y
         << setw(8) << setfill('^') << "Warm"
         << endl;                                      //Line 9

    cout << right;                                    //Line 10
    cout << setfill(' ');                             //Line 11

    cout << setw(5) << x << setw(7) << y
         << setw(8) << "Warm" << endl;               //Line 12

    return 0;
}
```

### 示例运行：

```text
12345678901234567890
15    7634   Warm
15***7634***Warm***
15***7634###Warm###
15@@@7634###Warm^^^
    15   7634    Warm
```

该程序的输出与示例 3-13 的输出相同。这里唯一的区别是，对于第 4 行到第 9 行的语句，输出是左对齐的。鼓励你对这个程序进行逐步分析。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_196_0.png)

本章讨论了几个流函数和流操纵符。要在程序中使用 `get`、`ignore`、`fill` 和 `clear` 等流函数，程序必须包含头文件 `iostream`。

操纵符有两种类型：带参数的和不带参数的。带参数的操纵符称为**带参数的流操纵符**。例如，`setprecision`、`setw` 和 `setfill` 等操纵符是带参数的。另一方面，`endl`、`fixed`、`scientific`、`showpoint` 和 `left` 等操纵符不带参数。

要在程序中使用带参数的流操纵符，必须包含头文件 `iomanip`。不带参数的操纵符是 `iostream` 头文件的一部分，因此不需要包含头文件 `iomanip`。

## 输入/输出与 `string` 类型

可以使用输入流变量（如 `cin`）和提取运算符 `>>`，将字符串读入 `string` 数据类型的变量。例如，如果输入是字符串 "Shelly"，以下代码会将此输入存储到字符串变量 name 中：

```cpp
string name;    //variable declaration
cin >> name;    //input statement
```

