
**示例运行：** 在此示例运行中，用户输入以底纹显示。

```text
Line 1: Based on the course score,
        this program computes the course grade.
Line 4: Enter course score: 85

Line 6: Course score is 85
Line 7: Your grade for the course is B.
```

该程序的工作方式如下。程序从第 1 行开始执行，打印输出的第一行（见示例运行）。第 2 行中的语句调用函数 getScore，实参为 courseScore（在 main 中声明的变量）。因为函数 getScore 的形参 score 是引用参数，所以地址（即变量 courseScore 的内存位置）会传递给 score。因此，score 和 courseScore 都指向同一内存位置，即 courseScore（见图 6-5）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_417_0.png)

**图 6-5** 变量 courseScore 和形参 score

对 score 所做的任何更改都会立即改变 courseScore 的值。

随后控制权转移到函数 getScore，第 4 行中的语句执行，打印输出的第二行。该语句提示用户输入课程成绩。第 5 行中的语句读取用户输入的值（示例运行中为 85），并将其存储在变量 score 中，而该变量实际上就是 courseScore（因为 score 是引用参数）。因此，此时变量 score 和 courseScore 的值均为 85（见图 6-6）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_417_1.png)

**图 6-6** 第 5 行语句执行后变量 courseScore 和形参 score

接下来，第 6 行中的语句输出 score 的值，如示例运行的第三行所示。第 6 行执行后，控制权返回到函数 main（见图 6-7）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_418_0.png)

**图 6-7** 第 6 行语句执行且控制权返回 main 后的变量 courseScore

接下来执行第 3 行中的语句。这是对函数 printGrade 的函数调用，实参为 courseScore。因为函数 printGrade 的形参 cScore 是值参数，所以形参 cScore 接收对应实参 courseScore 的值。因此，cScore 的值为 85。将 courseScore 的值复制到 cScore 后，cScore 和 courseScore 之间不再存在联系（见图 6-8）。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_418_1.png)

**图 6-8** 变量 courseScore 和形参 cScore

然后程序执行第 7 行中的语句，输出第四行。第 8 行中的 if...else 语句确定并输出课程等级。因为第 7 行中的输出语句不包含换行符或操纵符 endl，所以 if...else 语句的输出是输出第四行的一部分。if...else 语句执行后，控制权返回到函数 main。因为函数 main 中接下来要执行的语句是函数 main 的最后一条语句，所以程序终止。

在此程序中，函数 main 首先调用函数 getScore 从用户处获取课程成绩。然后函数 main 调用函数 printGrade，根据该课程成绩计算并打印等级。课程成绩由函数 getScore 获取；之后，该课程成绩由函数 printGrade 使用。因为 getScore 函数获取的值在程序后面会用到，所以函数 getScore 必须将该值传递到函数外部。因为 getScore 被编写为 void 函数，所以保存该值的形参必须是引用参数。

## 值参数、引用参数与内存分配

调用函数时，为其形参以及函数体中声明的变量（称为局部变量）分配的内存位于函数数据区中。回想一下，对于值参数，实参的值会被复制到其对应形参的内存单元中。对于引用参数，实参的地址会传递给形参。也就是说，形参的内容是一个地址。在数据操作期间，形参的内容指示计算机操作由其内容所指示的内存单元中的数据。因此，对于引用参数，实参和形参都指向同一内存位置。因此，在程序执行期间，形参所做的更改会永久改变实参的值。

> 流变量（例如 `ifstream` 和 `ofstream`）应按引用传递给函数。打开输入/输出文件或读取和/或输出数据后，输入和/或输出流的状态随后可以传递到函数外部。

由于参数传递是任何编程语言的基础，示例 6-13 和 6-14 进一步说明了这一概念。每个示例涵盖不同的场景。

### 示例 6-13

以下程序展示了引用参数和值参数的工作方式。

```cpp
//Example 6-13: Reference and value parameters

#include <iostream>

using namespace std;

void funOne(int a, int& b, char v);
void funTwo(int& x, int y, char& w);

int main()
{
    int num1, num2;
    char ch;

    num1 = 10;                              //Line 1
    num2 = 15;                              //Line 2
    ch = 'A';                               //Line 3

    cout << "Line 4: Inside main: num1 = " << num1
         << ", num2 = " << num2 << ", ch = "
         << ch << endl;                     //Line 4

    funOne(num1, num2, ch);                 //Line 5
    cout << "Line 6: After funOne: num1 = " << num1
         << ", num2 = " << num2 << ", and ch = "
         << ch << endl;                     //Line 6

    funTwo(num2, 25, ch);                   //Line 7
    cout << "Line 8: After funTwo: num1 = " << num1
         << ", num2 = " << num2 << ", and ch = "
         << ch << endl;                     //Line 8

    return 0;
}

void funOne(int a, int& b, char v)
{
    int one;

    one = a;                                //Line 9
    a++;                                    //Line 10
    b = b * 2;                              //Line 11
    v = 'B';                                //Line 12

    cout << "Line 13: Inside funOne: a = " << a
         << ", b = " << b << ", v = " << v
         << ", and one = " << one << endl;  //Line 13
}

void funTwo(int& x, int y, char& w)
{
    x++;                                    //Line 14
    y = y * 2;                              //Line 15
    w = 'G';                                //Line 16

    cout << "Line 17: Inside funTwo: x = " << x
         << ", y = " << y << ", and w = " << w
         << endl;                           //Line 17
}
```

**示例运行：**

```text
Line 4: Inside main: num1 = 10, num2 = 15, and ch = A
Line 13: Inside funOne: a = 11, b = 30, v = B, and one = 10
Line 6: After funOne: num1 = 10, num2 = 30, and ch = A
Line 17: Inside funTwo: x = 31, y = 50, and w = G
Line 8: After funTwo: num1 = 10, num2 = 50, and ch = G
```

让我们逐步分析这个程序。变量的值显示在每条语句执行之前和/或之后。

就在第 1 行中的语句执行之前，仅为函数 main 的变量分配了内存；该内存未初始化。第 3 行中的语句执行后，变量如图 6-9 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_421_0.png)

**图 6-9** 第 3 行中的语句执行后各变量的值

第 4 行中的语句产生以下输出：

```text
Line 4: Inside main: num1 = 10, num2 = 15, and ch = A
```

第 5 行中的语句是对函数 funOne 的函数调用。现在函数 funOne 有三个形参和一个局部变量。为函数 funOne 的形参和局部变量分配内存。因为形参 b 是引用参数，所以它接收对应实参的地址（内存位置），即 num2。另外两个形参是值参数，因此它们复制对应实参的值。就在第 9 行中的语句执行之前，变量如图 6-10 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_421_1.png)

**图 6-10** 第 9 行中的语句执行前各变量的值
