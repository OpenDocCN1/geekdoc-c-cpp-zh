
```cpp
int main()                                      //Line 4
{                                               //Line 5
    string name;                                //Line 6
    int age = 0;                                //Line 7
    int weight = 0;                             //Line 8
    double height = 0.0;                        //Line 9

    cout << "Line 10: Enter name, age, weight, and " //Line 10
         << "height: ";                        //Line 11
    cin >> name >> age >> weight >> height;     //Line 12
    cout << endl;

    cout << "Line 13: Name: " << name << endl;  //Line 13
    cout << "Line 14: Age: " << age << endl;    //Line 14
    cout << "Line 15: Weight: " << weight << endl; //Line 15
    cout << "Line 16: Height: " << height << endl; //Line 16

    return 0;                                   //Line 17
}                                               //Line 18
```

**示例运行：** 在这些示例运行中，用户输入以阴影显示。

### 示例运行 1

```
Line 10: Enter name, age, weight, and height: Sam 35 q56 6.2

Line 13: Name: Sam
Line 14: Age: 35
Line 15: Weight: 0
Line 16: Height: 0
```

第6、7、8和9行的语句声明变量 name、age、weight 和 height，并初始化变量 age、weight 和 height。第10行的语句提示用户输入一个人的姓名、年龄、体重和身高；第11行的语句将这些值分别输入变量 name、age、weight 和 height。

在此示例运行中，第三个输入是 q56，cin 语句试图将其输入变量 weight。然而，输入 q56 以字符 'q' 开头，而 weight 是 int 类型的变量，因此 cin 进入失败状态。注意，变量 weight 和 height 的打印值保持不变，如第15和16行语句的输出所示。

### 示例运行 2

```
Line 10: Enter name, age, weight, and height: Sam 35.0 156 6.2

Line 13: Name: Sam
Line 14: Age: 35
Line 15: Weight: 0
Line 16: Height: 0
```

在此示例运行中，将 Sam 输入 name、将 35 输入 age 后，第11行的 cin 语句在读取到小数点时停止。接下来，cin 语句试图将小数点输入 weight，而 weight 是 int 变量。因此，输入流进入失败状态，**weight** 和 **height** 的值保持不变，如第15和16行语句的输出所示。

## clear 函数

当输入流进入失败状态时，系统会忽略使用该流的所有后续 I/O。你可以使用流函数 `clear` 将输入流恢复到工作状态。

使用函数 `clear` 的语法是：

```
istreamVar.clear();
```

这里，`istreamVar` 是输入流变量，例如 `cin`。

使用函数 `clear` 将输入流恢复到工作状态后，你仍然需要清除输入流中剩余的垃圾数据。这可以通过使用函数 `ignore` 来完成。示例 3-9 说明了这种情况。

### 示例 3-9

```cpp
//Input failure and the clear function
#include <iostream>                                      //Line 1
#include <string>                                        //Line 2

using namespace std;                                     //Line 3

int main()                                               //Line 4
{
    string name;                                         //Line 5
    int age = 0;                                         //Line 6
    int weight = 0;                                       //Line 7
    double height = 0.0;                                  //Line 8

    cout << "Line 10: Enter name, age, weight, and "
         << "height: ";                                  //Line 10
    cin >> name >> age >> weight >> height;               //Line 11
    cout << endl;                                         //Line 12

    cout << "Line 13: Name: " << name << endl;           //Line 13
    cout << "Line 14: Age: " << age << endl;             //Line 14
    cout << "Line 15: Weight: " << weight << endl;       //Line 15
    cout << "Line 16: Height: " << height << endl;       //Line 16

    cin.clear();                         //Restore input stream; Line 17

    cin.ignore(200,'\n');                    //Clear the buffer; Line 18

    cout << "\nLine 19: Enter name, age, weight, "
         << "and height: ";                              //Line 19
    cin >> name >> age >> weight >> height;          //Line 20
    cout << endl;                                      //Line 21

    cout << "Line 22: Name: " << name << endl;        //Line 22
    cout << "Line 23: Age: " << age << endl;          //Line 23
    cout << "Line 24: Weight: " << weight << endl;    //Line 24
    cout << "Line 25: Height: " << height << endl;    //Line 25

    return 0;                                          //Line 26
}                                                   //Line 27
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Line 10: Enter name, age, weight, and height: Sam 35 q56 6.2

Line 13: Name: Sam
Line 14: Age: 35
Line 15: Weight: 0
Line 16: Height: 0

Line 19: Enter name, age, weight, and height: Sam 35 156 6.2

Line 22: Name: Sam
Line 23: Age: 35
Line 24: Weight: 156
Line 25: Height: 6.2
```

第6、7、8和9行的语句声明变量 name、age、weight 和 height，并初始化变量 age、weight 和 height。第10行的语句提示用户输入一个人的姓名、年龄、体重和身高；第11行的语句将这些值分别输入变量 name、age、weight 和 height。

如示例 3-8 中那样，当 cin 语句试图将 q56 输入 weight 时，它进入失败状态。第17行的语句通过使用函数 clear 恢复输入流，第18行的语句忽略剩余的输入。第19行的语句再次提示用户输入一个人的姓名、年龄、体重和身高；第20行的语句将这些值分别存储到 name、age、weight 和 height 中。接下来，第22至25行的语句输出 name、age、weight 和 height 的值。

## 输出与格式化输出

除了编写高效的程序外，生成所需的输出是程序员最重要的任务之一。第2章简要介绍了在标准输出设备上生成输出所涉及的过程。更准确地说，你学习了如何使用插入运算符 `<<` 和操纵符 `endl` 在标准输出设备上显示结果。

然而，输出远不止显示结果。有时，浮点数必须以特定方式输出。例如，工资单必须打印到两位小数，而科学实验的结果可能要求将浮点数输出到六位、七位，甚至十位小数。此外，你可能希望将数字按特定列对齐，或用空白以外的字符填充字符串与数字之间的空白。例如，在编制目录时，章节标题和页码之间的空白可能需要用点或短划线填充。在本节中，你将学习各种输出函数和操纵符，它们允许你以所需的方式格式化输出。

回想一下，`cout` 与插入运算符 `<<` 一起使用时的语法是：

```
cout << expression or manipulator << expression or manipulator...;
```

其中，`expression` 会被求值，其值被打印，而 `manipulator` 用于格式化输出。到目前为止你使用过的最简单的操纵符是 `endl`，它用于将插入点移动到下一行的开头。

其他值得关注的输出操纵符包括 `setprecision`、`fixed`、`showpoint` 和 `setw`。接下来几节将介绍这些操纵符。

### setprecision 操纵符

使用 `setprecision` 操纵符来控制浮点数的输出。通常，浮点数的默认输出是科学记数法。某些集成开发环境（IDE）可能对浮点数的默认输出使用最多六位小数。然而，当打印员工工资单时，期望的输出是最多两位小数。要将浮点输出打印到两位小数，可使用 `setprecision` 操纵符将精度设置为 2。

`setprecision` 操纵符的一般语法是：

```
setprecision(n)
```

其中 n 是小数位数。

将 `setprecision` 操纵符与 `cout` 和插入运算符一起使用。例如，语句：

```
cout << setprecision(2);
```

将十进制数的输出格式化为两位小数，直到后续语句更改精度。注意，小数位数（即精度值）作为参数传递给 `setprecision`。

要使用 `setprecision` 操纵符，程序必须包含头文件 `iomanip`。因此，需要以下 include 语句：

```
#include <iomanip>
```
