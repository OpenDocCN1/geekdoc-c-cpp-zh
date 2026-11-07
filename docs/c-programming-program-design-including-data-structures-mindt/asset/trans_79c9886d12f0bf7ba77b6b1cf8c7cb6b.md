
示例 3-14 中的程序说明了在程序中使用 `setfill` 的效果。

### 示例 3-14

```cpp
//This program illustrates how the function setfill works.

#include <iostream>                                      //Line 1
#include <string>                                        //Line 2
#include <iomanip>                                       //Line 3

using namespace std;                                     //Line 4

int main()                                               //Line 5
{
    string name = "Jessica";                            //Line 7
    double gpa = 3.75;                                   //Line 8
    int scholarship = 7850;                              //Line 9

    cout << "123456789012345678901234567890" << endl;   //Line 10
    cout << fixed << showpoint << setprecision(2);      //Line 11

    cout << setw(10) << name << setw(7) << gpa
         << setw(8) << scholarship << endl;              //Line 12

    cout << setfill('*');                                //Line 13
    cout << setw(10) << name << setw(7) << gpa
         << setw(8) << scholarship << endl;              //Line 14

    cout << setw(10) << name << setfill('#')
         << setw(7) << gpa
         << setw(8) << scholarship << endl;              //Line 15

    cout << setw(10) << setfill('@') << name
         << setw(7) << setfill('#') << gpa
         << setw(8) << setfill('^') << scholarship
         << endl;                                        //Line 16

    cout << setfill(' ');                                //Line 17
    cout << setw(10) << name << setw(7) << gpa
         << setw(8) << scholarship << endl;              //Line 18

    return 0;                                            //Line 19
}                                                       //Line 20
```

### 运行示例：

```text
123456789012345678901234567890
    Jessica   3.75    7850
***Jessica***3.75****7850
***Jessica###3.75####7850
@@@Jessica##3.75^^^7850
    Jessica   3.75    7850
```

第 7、8、9 行的语句声明并初始化变量 `name`、`gpa` 和 `scholarship`，分别赋值为 `"Jessica"`、`3.75` 和 `7850`。第 10 行语句的输出——输出的第一行——显示了后续语句输出变量值时的列位置。第 11 行语句将十进制数的输出设置为带小数点的定点小数格式，并保留两位小数。第 12 行语句在十列中输出 `name` 的值，在七列中输出 `gpa` 的值，在八列中输出 `scholarship` 的值。在该语句中，填充字符为空白字符，如输出的第二行所示。

第 13 行语句将填充字符设置为 `*`。第 14 行语句在十列中输出 `name` 的值，在七列中输出 `gpa` 的值，在八列中输出 `scholarship` 的值。因为 `"Jessica"` 是长度为 7 的字符串，而分配了十列来输出其值，所以前三列未使用，因此由填充字符 `*` 填充。类似地，`gpa` 和 `scholarship` 的值未使用的列由 `*` 填充。

第 15 行语句的输出——输出的第四行——与第 14 行语句的输出类似，不同之处在于 `gpa` 和 `scholarship` 的填充字符是 `#`。在第 16 行语句的输出（输出的第五行）中，`name` 的填充字符是 `@`，`gpa` 的填充字符是 `#`，`scholarship` 的填充字符是 `^`。操纵器 `setfill` 设置这些填充字符。

第 17 行语句将填充字符设置为空白。第 18 行语句使用空白填充字符输出 `name`、`gpa` 和 `scholarship` 的值，如输出的第六行所示。

## left 和 right 操纵器

回想一下，如果 `setw` 操纵器中指定的列数超过下一个表达式所需的列数，默认输出是右对齐的。有时，你可能希望输出左对齐。要使输出左对齐，应使用操纵器 `left`。

设置操纵器 `left` 的语法为：

```cpp
ostreamVar << left;
```

其中 `ostreamVar` 是输出流变量。例如，以下语句将标准输出设备上的输出设置为左对齐：

```cpp
cout << left;
```

可以使用流函数 `unsetf` 禁用操纵器 `left`。禁用操纵器 `left` 的语法为：

```cpp
ostreamVar.unsetf(ios::left);
```

其中 `ostreamVar` 是输出流变量。禁用操纵器 `left` 会将输出恢复为默认输出格式的设置。例如，以下语句在标准输出设备上禁用操纵器 `left`：

```cpp
cout.unsetf(ios::left);
```

设置操纵器 `right` 的语法为：

```cpp
ostreamVar << right;
```

其中 `ostreamVar` 是输出流变量。例如，以下语句将标准输出设备上的输出设置为右对齐：

```cpp
cout << right;
```

> **注意**
>
> 在某些编译器上，语句 `cout << left;` 和 `cout << right;` 可能无法工作。在这种情况下，可以使用 `cout.setf(ios::left);` 代替 `cout << left;`，并使用 `cout.setf(ios::right);` 代替 `cout << right;`。

示例 3-15 中的程序说明了操纵器 `left` 和 `right` 的效果。

### 示例 3-15

```cpp
//Example: left justification

#include <iostream>                                      //Line 1
#include <string>                                        //Line 2
#include <iomanip>                                       //Line 3

using namespace std;                                     //Line 4

int main()                                               //Line 5
{                                                        //Line 6
    string name = "Jessica";                            //Line 7
    double gpa = 3.75;                                   //Line 8
    int scholarship = 7850;                              //Line 9

    cout << "123456789012345678901234567890" << endl;   //Line 10
    cout << fixed << showpoint << setprecision(2);      //Line 11

    cout << left;                                        //Line 12

    cout << setw(10) << name << setw(7) << gpa
         << setw(8) << scholarship << endl;             //Line 13

    cout << setfill('*');                                //Line 14
    cout << setw(10) << name << setw(7) << gpa
         << setw(8) << scholarship << endl;             //Line 15

    cout << setw(10) << name << setfill('#')
         << setw(7) << gpa
         << setw(8) << scholarship << endl;              //Line 16

    cout << setw(10) << setfill('@') << name
         << setw(7) << setfill('#') << gpa
         << setw(8) << setfill('^') << scholarship
         << endl;                                      //Line 17

    cout << right;                                     //Line 18
    cout << setfill(' ');                              //Line 19
    cout << setw(10) << name << setw(7) << gpa
         << setw(8) << scholarship << endl;            //Line 20

    return 0;                                          //Line 21
}                                                      //Line 22
```

### 运行示例：

```text
123456789012345678901234567890
Jessica   3.75   7850
Jessica***3.75***7850****
Jessica###3.75###7850####
Jessica@@@3.75@@@7850^^^
   Jessica   3.75   7850
```

该程序的输出与示例 3-14 的输出相同。这里唯一的区别是，对于第 13 行到第 17 行的语句，输出为左对齐。建议你逐步走查该程序。

> **注意**
>
> 本章讨论若干流函数和流操纵器。要在程序中使用 `get`、`ignore`、`fill` 和 `clear` 等流函数，程序必须包含头文件 `iostream`。
>
> 操纵器有两种类型：带参数的和不带参数的。带参数的操纵器称为**参数化流操纵器**。例如，`setprecision`、`setw` 和 `setfill` 等操纵器是参数化的。另一方面，`endl`、`fixed`、`scientific`、`showpoint` 和 `left` 等操纵器没有参数。
>
> 要在程序中使用参数化流操纵器，必须包含头文件 `iomanip`。不带参数的操纵器是 `iostream` 头文件的一部分，因此不需要包含头文件 `iomanip`。

## 输入/输出与 `string` 类型

可以使用输入流变量（如 `cin`）和提取运算符 `>>` 将字符串读入 `string` 数据类型的变量。例如，如果输入是字符串 `"Shelly"`，以下代码会将该输入存储到 `string` 变量 `name` 中：

```cpp
string name;   //variable declaration
cin >> name;   //input statement
```

回想一下，提取运算符会跳过所有前导空白字符，并且读取会在空白字符处停止。因此，你不能使用
