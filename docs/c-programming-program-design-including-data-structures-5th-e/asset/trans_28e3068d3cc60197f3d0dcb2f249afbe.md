

```
cout << "Line 7: In the function funcValueParam, "
     << "after changing, num = " << num
     << endl;                                      //Line 7
}
```

## 示例运行

```
Line 2: Before calling the function funcValueParam, number = 6
Line 5: In the function funcValueParam, before changing, num = 6
Line 7: In the function funcValueParam, after changing, num = 15
Line 4: After calling the function funcValueParam, number = 6
```

该程序的运行过程如下。程序从函数 main 开始执行。第 1 行中的语句声明并初始化 int 变量 number。第 2 行中的语句在调用函数 funcValueParam 之前输出 number 的值；第 3 行中的语句调用函数 funcValueParam。然后，变量 number 的值传递给形参 num。控制权现在转移到函数 funcValueParam。

第 5 行中的语句在更改 num 的值之前输出 num 的值。第 6 行中的语句将 num 的值更改为 15；第 7 行中的语句输出 num 的值。该语句执行后，函数 funcValueParam 退出，控制权返回函数 main。

第 4 行中的语句在调用函数 funcValueParam 之后输出 number 的值。示例运行表明，即使其对应形参 num 的值在函数 funcValueParam 内被更改，number 的值（第 2 行和第 4 行）仍保持不变。

输出显示了语句执行的顺序。

复制数据后，值参数与实参没有联系，因此值参数不能将任何结果传回调用函数。函数执行时，对形参所做的任何更改都不会以任何方式影响实参。实参并不知道形参发生了什么。因此，值参数不能将信息传出函数。值参数仅在实参和形参之间提供单向联系。因此，仅使用值参数的函数存在局限性。

## 引用变量作为参数

示例 7-4 中的程序说明了值参数如何工作。另一方面，假设形参是引用参数。因为引用参数接收实参的地址（内存位置），所以引用参数可以从函数中传出一个或多个值，并且可以更改实参的值。

引用参数在三种情况下很有用：

- 当需要更改实参的值时
- 当希望从函数返回多个值时
- 当传递地址相对于复制大量数据可以节省内存空间和时间时

本书通篇演示了前两种情况。第 9 章和第 11 章在介绍数组和类时讨论第三种情况。

回想一下，当你在函数形参列表中的 `dataType` 后加上 `&` 时，该 `dataType` 后面的变量就变成引用参数。

> **注意**
> 
> 可以使用关键字 `const` 将引用（形）参声明为常量。第 10 章和第 11 章将讨论常量引用参数。在此之前，你使用的引用参数将如本章所定义的那样是非常量引用参数。根据引用参数的定义可知，常量值或表达式不能传递给非常量引用参数。如果形参是非常量引用参数，那么在函数调用期间，其对应的实参必须是变量。

### 示例 7-5：计算成绩

下面的程序接收一个课程分数（0 到 100 之间的值），并确定学生的课程等级。该程序有三个函数：`main`、`getScore` 和 `printGrade`，如下所示：

- 1. `main`
  - a. 获取课程分数。
  - b. 打印课程等级。
- 2. `getScore`
  - a. 提示用户输入。
  - b. 获取输入。
  - c. 打印课程分数。
- 3. `printGrade`
  - a. 计算课程等级。
  - b. 打印课程等级。

完整程序如下：

```
//This program reads a course score and prints the
//associated course grade.
#include <iostream>
using namespace std;

void getScore(int& score);
void printGrade(int score);

int main()
{
    int courseScore;

    cout << "Line 1: Based on the course score, \n"
         << "       this program computes the "
         << "course grade." << endl;                 //Line 1

    getScore(courseScore);                            //Line 2

    printGrade(courseScore);                          //Line 3

    return 0;
}

void getScore(int& score)
{
    cout << "Line 4: Enter course score: ";           //Line 4
    cin >> score;                                     //Line 5
    cout << endl << "Line 6: Course score is "
         << score << endl;                            //Line 6
}

void printGrade(int cScore)
{
    cout << "Line 7: Your grade for the course is "; //Line 7

    if (cScore >= 90)                                 //Line 8
        cout << "A." << endl;
    else if (cScore >= 80)
        cout << "B." << endl;
    else if(cScore >= 70)
        cout << "C." << endl;
    else if (cScore >= 60)
        cout << "D." << endl;
    else
        cout << "F." << endl;
}
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```
Line 1: Based on the course score,
        this program computes the course grade.
Line 4: Enter course score: 85

Line 6: Course score is 85
Line 7: Your grade for the course is B.
```

该程序的运行过程如下。程序从第 1 行开始执行，该行打印输出的第一行（参见示例运行）。第 2 行中的语句用实参 courseScore（在 main 中声明的变量）调用函数 getScore。因为函数 `getScore` 的形参 `score` 是引用参数，所以地址（即变量 `courseScore` 的内存位置）传递给 `score`。因此，`score` 和 `courseScore` 都指向同一个内存位置，即 `courseScore`（见图 7-1）。

![](img/f97f778697507bb6fdd80c5991210cba_412_0.png)

**图 7-1** 变量 `courseScore` 和参数 `score`

对 `score` 所做的任何更改都会立即改变 `courseScore` 的值。

然后控制权转移到函数 `getScore`，第 4 行中的语句执行，打印输出的第二行。该语句提示用户输入课程分数。第 5 行中的语句读取用户输入的值（示例运行中为 85），并将其存储到 `score` 中，而 `score` 实际上就是 `courseScore`（因为 `score` 是引用参数）。因此，此时变量 `score` 和 `courseScore` 的值都是 85（见图 7-2）。

![](img/f97f778697507bb6fdd80c5991210cba_412_1.png)

**图 7-2** 第 5 行中的语句执行后变量 `courseScore` 和参数 `score`

接下来，第 6 行中的语句输出 `score` 的值，如示例运行第三行所示。第 6 行执行后，控制权返回函数 `main`（见图 7-3）。

![](img/f97f778697507bb6fdd80c5991210cba_412_2.png)

**图 7-3** 第 6 行中的语句执行且控制权返回 `main` 后的变量 `courseScore`

接下来执行第 3 行中的语句。它是一次对函数 `printGrade` 的调用，实参为 `courseScore`。因为函数 `printGrade` 的形参 `cScore` 是值参数，所以参数 `cScore` 接收对应实参 `courseScore` 的值。因此，`cScore` 的值为 85。将 `courseScore` 的值复制到 `cScore` 后，`cScore` 和 `courseScore` 之间就不存在任何联系（见图 7-4）。

![](img/f97f778697507bb6fdd80c5991210cba_413_0.png)

**图 7-4** 变量 `courseScore` 和参数 `cScore`

然后程序执行第 7 行中的语句，输出第四行。第 8 行中的 `if...else` 语句确定并输出课程等级。因为第 7 行中的输出语句不包含换行符或操纵符 `endl`，所以 `if...else` 语句的输出是输出第四行的一部分。`if...else` 语句执行后，控制权返回函数 `main`。因为函数 `main` 中下一条要执行的语句是函数 `main` 的最后一条语句，所以程序终止。

在该程序中，函数 `main` 首先调用函数 `getScore` 从用户处获取课程分数。然后，函数 `main` 调用函数 `printGrade`，根据该课程分数计算并打印等级。课程分数由函数 `getScore` 获取；之后，该课程分数由函数 `printGrade` 使用。因为 `getScore` 函数获取的值会在程序后面使用，所以函数 `getScore` 必须将该值传出。因此，保存该值的形参必须是引用参数。

## 值参数、引用参数与内存分配

调用函数时，为其形参以及函数体中声明的变量（称为**局部变量**）分配的内存位于函数数据区中。回想一下，对于值参数，实参的值会被复制到其对应形参的内存单元中。对于引用参数，实参的地址会传递给形参。也就是说，形参的内容是一个地址。在数据操作期间，形参的内容指示计算机操作其内容所指示的内存单元中的数据。因此，对于引用参数，实参和形参都指向同一个内存位置。因此，在程序执行期间，形参所做的更改会永久改变实参的值。

