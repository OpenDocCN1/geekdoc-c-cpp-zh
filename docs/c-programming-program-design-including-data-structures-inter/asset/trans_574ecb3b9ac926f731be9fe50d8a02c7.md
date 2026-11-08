

## 输入失败

程序执行过程中可能出很多问题。语法正确的程序也可能产生错误结果。例如，假设兼职员工的工资按以下公式计算：

```cpp
wages = payRate * hoursWorked;
```

如果你不小心把 * 误输入为 +，那么即使包含 + 的语句在语法上是正确的，计算出的工资也会是错误的。

那么尝试读取无效数据会怎样呢？例如，如果你试图把字母输入到 int 变量中，会发生什么？如果输入数据与相应变量不匹配，程序就会遇到问题。例如，试图把字母读入 int 或 double 变量会导致输入失败。考虑以下语句：

```cpp
int a, b, c;
double x;
```

如果输入是：

```
W 54
```

那么语句：

```cpp
cin >> a >> b;
```

会导致输入失败，因为你试图把字符 'W' 输入到 int 变量 a 中。如果输入是：

```
35 67.93 48
```

那么输入语句：

```cpp
cin >> a >> x >> b;
```

会把 35 存入 a，把 67.93 存入 x，把 48 存入 b。

现在用前面的输入（包含三个值的输入）考虑下面的读取语句：

```cpp
cin >> a >> b >> c;
```

该语句把 35 存入 a，把 67 存入 b。读取在小数点处停止。因为下一个变量 c 的数据类型是 int，计算机会试图把 . 读入 c，这是一个错误。随后输入流进入一种称为失败状态的状态。

当输入流进入失败状态时，实际会发生什么？一旦输入流进入失败状态，使用该流的所有后续 I/O 语句都会被忽略。不幸的是，程序会带着变量中存储的任何值悄悄继续执行，并产生错误结果。示例 3-8 中的程序演示了输入失败。该程序在你的系统上可能产生不同结果。

### 示例 3-8

```cpp
//Input Failure program
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string name;                                      //Line 1
    int age = 0;                                      //Line 2
    int weight = 0;                                   //Line 3
    double height = 0.0;                              //Line 4

    cout << "Line 5: Enter name, age, weight, and "
         << "height: ";                              //Line 5
    cin >> name >> age >> weight >> height;           //Line 6
    cout << endl;                                     //Line 7

    cout << "Line 8: Name: " << name << endl;         //Line 8
    cout << "Line 9: Age: " << age << endl;           //Line 9
    cout << "Line 10: Weight: " << weight << endl;   //Line 10
    cout << "Line 11: Height: " << height << endl;   //Line 11

    return 0;                                         //Line 12
}
```

**示例运行：** 在这些示例运行中，用户输入以加粗表示。

### 示例运行 1

```
Line 5: Enter name, age, weight, and height: **Sam 35 q56 6.2**
```

```
Line 8: Name: Sam
Line 9: Age: 35
Line 10: Weight: 0
Line 11: Height: 0
```

第 1、2、3、4 行中的语句声明变量 name、age、weight 和 height，并且还初始化变量 age、weight 和 height。第 5 行中的语句提示用户输入一个人的姓名、年龄、体重和身高；第 6 行中的语句将这些值分别输入变量 name、age、weight 和 height。

在此示例运行中，第三个输入是 q56，cin 语句试图将其输入变量 weight。然而，输入 q56 以字符 'q' 开头，而 weight 是 int 类型变量，因此 cin 认为该输入无效。注意，如第 10 行和第 11 行语句的输出所示，变量 weight 和 height 的打印值保持不变。

### 示例运行 2

```
Line 5: Enter name, age, weight, and height: Sam 35.0 156 6.2

Line 8: Name: Sam
Line 9: Age: 35
Line 10: Weight: 0
Line 11: Height: 0
```

在此示例运行中，在把 Sam 输入 name、把 35 输入 age 之后，第 6 行 cin 语句的读取在小数点处停止。接着 cin 语句试图把小数点输入 weight，而 weight 是 int 变量。因此输入流进入失败状态，weight 和 height 的值保持不变，如第 10 行和第 11 行语句的输出所示。

## `clear` 函数

当输入流进入失败状态时，系统会忽略使用该流的所有后续 I/O。你可以使用流函数 clear 将输入流恢复到工作状态。

使用函数 clear 的语法是：

```cpp
istreamVar.clear();
```

这里，istreamVar 是输入流变量，例如 cin。

使用函数 clear 将输入流恢复到工作状态后，你仍然需要清除输入流中剩余的垃圾数据。这可以通过使用函数 ignore 来完成。示例 3-9 说明了这种情况。

### 示例 3-9

```cpp
// Input failure and the clear function
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string name;                         //Line 1
    int age = 0;                         //Line 2
    int weight = 0;                      //Line 3
    double height = 0.0;                 //Line 4

    cout << "Line 5: Enter name, age, weight, and "
         << "height: ";                  //Line 5

    cin >> name >> age >> weight >> height;        //Line 6
    cout << endl;                                   //Line 7

    cout << "Line 8: Name: " << name << endl;      //Line 8
    cout << "Line 9: Age: " << age << endl;        //Line 9
    cout << "Line 10: Weight: " << weight << endl;  //Line 10
    cout << "Line 11: Height: " << height << endl;  //Line 11

    cin.clear();                  //Restore input stream; Line 12

    cin.ignore(200,'\n');        //Clear the buffer; Line 13

    cout << "\nLine 14: Enter name, age, weight, "      //Line 14
         << "and height: ";
    cin >> name >> age >> weight >> height;          //Line 15
    cout << endl;                                    //Line 16

    cout << "Line 17: Name: " << name << endl;       //Line 17
    cout << "Line 18: Age: " << age << endl;         //Line 18
    cout << "Line 19: Weight: " << weight << endl;   //Line 19
    cout << "Line 20: Height: " << height << endl;   //Line 20

    return 0;                                        //Line 21
}
```

**示例运行：** 在此示例运行中，用户输入以加粗表示。

```
Line 5: Enter name, age, weight, and height: Sam 35 q56 6.2

Line 8: Name: Sam
Line 9: Age: 35
Line 10: Weight: 0
Line 11: Height: 0

Line 14: Enter name, age, weight, and height: Sam 35 156 6.2

Line 17: Name: Sam
Line 18: Age: 35
Line 19: Weight: 156
Line 20: Height: 6.2
```

第 1、2、3、4 行中的语句声明变量 name、age、weight 和 height，并且还初始化变量 age、weight 和 height。第 5 行中的语句提示用户输入一个人的姓名、年龄、体重和身高；第 6 行中的语句将这些值分别输入变量 name、age、weight 和 height。

如示例 3-8 中那样，当 cin 语句试图把 q56 输入 weight 时，它进入失败状态。第 12 行中的语句使用函数 clear 恢复输入流，第 13 行中的语句忽略剩余输入。第 14 行中的语句再次提示用户输入一个人的姓名、年龄、体重和身高；第 15 行中的语句将这些值分别存入 name、age、weight 和 height。接着，第 17 行到第 20 行中的语句输出 name、age、weight 和 height 的值。

你将 `setprecision` 操纵符与 `cout` 和插入运算符一起使用。例如，语句：

```cpp
cout << setprecision(2);
```

将十进制数的输出格式化为两位小数，直到后续类似语句改变精度。注意，小数位数（即精度值）作为参数传递给 `setprecision`。

要使用操纵符 `setprecision`，程序必须包含头文件 `iomanip`。因此，需要以下 include 语句：

```cpp
#include <iomanip>
```

### fixed 操纵符

要进一步控制浮点数的输出，你可以使用其他操纵符。要以固定小数格式输出浮点数，你可以使用操纵符 `fixed`。以下语句将标准输出设备上浮点数的输出设置为固定小数格式：

```cpp
cout << fixed;
```

执行前面的语句后，所有浮点数都会以固定小数格式显示，直到操纵符 `fixed` 被禁用。你可以使用流成员函数 `unsetf` 禁用操纵符 `fixed`。例如，要禁用标准输出设备上的操纵符 `fixed`，你使用以下语句：

```cpp
cout.unsetf(ios::fixed);
```

操纵符 `fixed` 被禁用后，浮点数的输出恢复为默认设置。操纵符 `scientific` 用于以科学格式输出浮点数。

> **注意**
>
> 在某些编译器上，语句 `cin>>fixed;` 和 `cin>>scientific;` 可能不起作用。在这种情况下，你可以用 `cin.setf(ios::fixed);` 代替 `cin>>fixed;`，并用 `cin.setf(ios::scientific);` 代替 `cin>>scientific;`。

### 示例 3-10

```cpp
//Example: scientific and fixed

#include <iostream>

using namespace std;
```

