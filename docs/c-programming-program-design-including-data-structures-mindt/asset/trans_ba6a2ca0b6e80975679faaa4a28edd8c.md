

```cpp
void funcValueParam(int num);                     //Line 3

int main()                                        //Line 4
{                                                 //Line 5
    int number = 6;                               //Line 6

    cout << "Line 7: Before calling the function "
         << "funcValueParam, number = " << number
         << endl;                                  //Line 7

    funcValueParam(number);                        //Line 8

    cout << "Line 9: After calling the function "
         << "funcValueParam, number = " << number
         << endl;                                  //Line 9

    return 0;                                      //Line 10
}                                                  //Line 11

void funcValueParam(int num)                       //Line 12
{                                                  //Line 13
    cout << "Line 14: In the function funcValueParam, "
         << "before changing, num = " << num
         << endl;                                  //Line 14

    num = 15;                                      //Line 15

    cout << "Line 16: In the function funcValueParam, "
         << "after changing, num = " << num
         << endl;                                  //Line 16
}                                                  //Line 17
```

## 示例运行：

```text
Line 7: Before calling the function funcValueParam, number = 6
Line 14: In the function funcValueParam, before changing, num = 6
Line 16: In the function funcValueParam, after changing, num = 15
Line 9: After calling the function funcValueParam, number = 6
```

本程序的工作过程如下。执行从函数 main 开始。第 6 行的语句声明并初始化 int 变量 number。第 7 行的语句在调用函数 funcValueParam 之前输出 number 的值；第 8 行的语句调用函数 funcValueParam。随后，变量 number 的值被传递给形式参数 num。控制权现在转移到函数 funcValueParam。

第 14 行的语句在改变 num 的值之前输出 num 的值。第 15 行的语句将 num 的值改为 15；第 16 行的语句输出 num 的值。执行完该语句后，函数 funcValueParam 退出，控制权回到函数 main。

```cpp
void getScore(int& score)                                      //Line 13
{                                                              //Line 14
    cout << "Line 15: Enter course score: ";                  //Line 15
    cin >> score;                                              //Line 16
    cout << endl << "Line 17: The course score is "           //Line 17
         << score << endl;                                     //Line 17
}                                                              //Line 18

void printGrade(int cScore)                                   //Line 19
{                                                              //Line 20
    cout << "Line 21: The course grade is: ";                //Line 21

    if (cScore >= 90)                                         //Line 22
        cout << "A." << endl;                                //Line 23
    else if (cScore >= 80)                                    //Line 24
        cout << "B." << endl;                                //Line 25
    else if (cScore >= 70)                                    //Line 26
        cout << "C." << endl;                                //Line 27
    else if (cScore >= 60)                                    //Line 28
        cout << "D." << endl;                                //Line 29
    else                                                       //Line 30
        cout << "F." << endl;                                //Line 31
}                                                              //Line 32
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```text
Line 8: Based on the course score,
          this program computes the course grade.
Line 15: Enter course score: 85

Line 17: The course score is 85
Line 21: The course grade is: B.
```

本程序的工作过程如下。程序从第 8 行开始执行，该行打印输出的第一行（见示例运行）。第 9 行的语句调用函数 getScore，实际参数为 courseScore（在 main 中声明的变量）。由于函数 getScore 的形式参数 score 是引用参数，courseScore 的地址（即变量 courseScore 的内存位置）被传递给 score。因此，score 和 courseScore 现在都指向同一内存位置，即 courseScore（见图 6-5）。

![](img/b217c421655b51e7494cf3b89bb5432d_437_0.png)

图 6-5 变量 courseScore 与参数 score

然后程序执行第 21 行的语句，该语句输出第四行。第 22 行至第 31 行的 `if...else` 语句确定并输出课程成绩。由于第 7 行的输出语句不包含换行符或操纵符 `endl`，`if...else` 语句的输出构成输出的第四行的一部分。执行完 `if...else` 语句后，控制权回到函数 `main`。由于函数 `main` 中接下来要执行的语句是函数 `main` 的最后一条语句，程序终止。

在此程序中，函数 `main` 首先调用函数 `getScore` 从用户处获取课程分数。然后函数 `main` 调用函数 `printGrade`，根据该课程分数计算并打印成绩。课程分数由函数 `getScore` 获取；随后，该课程分数由函数 `printGrade` 使用。由于 `getScore` 函数获取的值稍后会在程序中使用，函数 `getScore` 必须将该值传递到函数外部。由于 `getScore` 被编写为 void 函数，保存该值的形式参数必须是引用参数。

## 值与引用参数及内存分配

调用函数时，其形式参数以及函数体中声明的变量（称为**局部变量**）的内存会在函数数据区中分配。回想一下，对于值参数，实际参数的值被复制到其对应形式参数的内存单元中。对于引用参数，实际参数的地址被传递给形式参数。也就是说，形式参数的内容是一个地址。在数据操作期间，形式参数中存储的地址指示计算机操作该地址处内存单元中的数据。因此，对于引用参数，实际参数和形式参数都指向同一内存位置。因此，在程序执行期间，形式参数所做的更改会永久改变实际参数的值。

> **注意**
> 流变量（例如 `ifstream` 和 `ofstream`）应通过引用传递给函数。打开输入/输出文件后，或读取和/或输出数据后，输入和/或输出流的状态随后可以传递到函数外部。

由于参数传递是任何编程语言的基础，示例 6-14 和 6-15 进一步说明这一概念。每个示例涵盖不同的场景。

## 示例 6-14

以下程序展示引用参数和值参数如何工作。

```cpp
//Example 6-14: Reference and value parameters

#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

void funOne(int a, int& b, char v);                      //Line 3
void funTwo(int& x, int y, char& w);                     //Line 4

int main()                                               //Line 5
{
    int num1, num2;                                       //Line 7
    char ch;                                              //Line 8

    num1 = 10;                                            //Line 9
    num2 = 15;                                            //Line 10
    ch = 'A';                                             //Line 11

    cout << "Line 12: Inside main: num1 = " << num1
         << ", num2 = " << num2 << ", and ch = "
         << ch << endl;                                   //Line 12

    funOne(num1, num2, ch);                               //Line 13

    cout << "Line 14: After funOne: num1 = " << num1
         << ", num2 = " << num2 << ", and ch = "
         << ch << endl;                                   //Line 14

    funTwo(num2, 25, ch);                                 //Line 15

    cout << "Line 16: After funTwo: num1 = " << num1
         << ", num2 = " << num2 << ", and ch = "
         << ch << endl;                                   //Line 16

    return 0;                                             //Line 17
}                                                        //Line 18

void funOne(int a, int& b, char v)                       //Line 19
{
    int one;                                              //Line 21

    one = a;                                              //Line 22
    a++;                                                  //Line 23
    b = b * 2;                                            //Line 24
    v = 'B';                                              //Line 25
```

