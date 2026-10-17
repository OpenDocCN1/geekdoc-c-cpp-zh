
## 2. 统计该课程的人数。

## 3. 将总分除以人数以找到课程平均分。

## 4. 输出。

处理每门课程的数据是类似的，涉及一个两步骤的过程：

1. 累加该课程的分数。
2. 统计该课程的人数。
3. 将总分除以人数以找到课程平均分。
4. 输出。

### 406 | 第7章：用户自定义函数

前面的讨论翻译为以下算法：

1. 声明并初始化变量。
2. 获取下一个课程分数，`score`。
3. 如果分数不是 `-999`，打印错误信息并退出。
4. 计算两组的平均分。
5. 输出如下形式。
6. 对每门课程重复第2到第5步。
7. 输出最终结果。

前面的讨论建议程序需要变量：

```cpp
string courseID1; // 第一组课程ID
string courseID2; // 第二组课程ID
int numberOfCourses;
double avg1; // 第一组平均分
double avg2; // 第二组平均分
double avggroup1; // 第一组平均分
double avggroup2; // 第二组平均分
istream group1; // 第一组输入流
istream group2; // 第二组输入流
```

```cpp
ostream;
```

接下来，我们讨论 `calculateAverage` 和 `printResult` 函数。然后，我们将函数组合。

该函数计算课程的平均分。由于输出存储在文件中，我们必须向此函数传递四个参数：与输出文件相关的 `ofstream` 变量、分组编号、课程 ID 以及该组的课程平均分。`ofstream` 变量必须引用传递。由于函数只使用其他变量的值，其余三个参数应该是值参数。此外，从输出可以明显看出我们只在分组编号之前打印课程 ID。

1. 在伪代码中，算法是：

   如果 (`groupNo` == 1)

     打印课程 ID

   else

     打印一个空白

打印分组编号和课程平均分

（函数定义）

```cpp
void calculateAverage(istream& stream, double& courseAvg) {
  // ... 代码 ...
  stream >> score;
  while (score != -999) {
    totalScore = totalScore + score;
    numberOfStudents++;
    stream >> score;
  }
  courseAvg = totalScore / numberOfStudents;
}
```

```cpp
void printResult(ofstream& out, int groupNo, string courseID, double avg) {
  // ... 代码 ...
}
```

函数 `printResult` 的定义：

```cpp
void printResult(ofstream& outp, string courseID, int groupNo,
    double avg) {
    if (groupNo == 1)
        outp << " " << courseID << " ";
    else
        outp << " " << "# ";

    outp << setw(8) << groupNo << setw(17) << avg << endl;
} //printResult
```

现在我们已经定义并设计了 `calculateAverage` 和 `printResult` 函数，我们可以描述 `main` 函数的算法。然而，在概述算法之前，请注意以下几：在输入文件中，数据可能是按课程 ID 排序的，但一个文件包含的课程可能另一个少。在处理完两个文件并发现其中一个文件还有未处理的数据之前，我们不会发现这个错误。在打印最终答案（即第1 组和第 2 组的平均值）之前，请确保检查此错误。

## MAIN

算法：

函数 `main`

- 1. 声明变量（局部声明）。
- 2. 打开输入文件。
- 3. 如果无法打开文件，则打印消息并终止程序。
- 4. 打开输出文件。
- 5. 为了输出固定小数格式且带有小数点和末尾零的浮点数，设置操纵符 `fixed` 和 `showpoint`。此外，为了输出两位小数浮点数，将精度设置为两位。
- 6. 将第 1 组的课程平均值初始化为 0.0。
- 7. 将第 2 组的课程平均值初始化为 0.0。
- 8. 将课程数量初始化为 0。
- 9. 打印表头。
- 10. 获取第 1 组的课程 ID，`courseId1`。
- 11. 获取第 2 组的课程 ID，`courseId2`。
- 12. 对于第 1 组和第 2 组中的每门课程
    - a. 如果 (`courseId1` != `courseId2`)
        `cout << "Data error: Course IDs do not match.\n";`
        `return 1;`
    - b. 或者
        i. 计算第 1 组的课程平均值（调用函数 `calculateAverage` 并传递相应的参数）。
        ii. 计算第 2 组的课程平均值（调用函数 `calculateAverage` 并传递相应的参数）。
        iii. 打印第 1 组的结果（调用函数 `printResult` 并传递相应的参数）。
        iv. 打印第 2 组的结果（调用函数 `printResult` 并传递相应的参数）。
        v. 更新第 1 组的平均值。
        vi. 更新第 2 组的平均值。
        vii. 课程数量加 1。
    - c. 获取第 1 组的课程 ID，`courseId1`。
    - d. 获取第 2 组的课程 ID，`courseId2`。
- 13. a. 如果第 1 组未结束文件且第 2 组已结束文件
      打印 "Ran out of data for group 2 before group 1"
    - b. 或者如果第 1 组已结束文件且第 2 组未结束文件
      打印 "Ran out of data for group 1 before group 2"
    - c. 否则打印第 1 组和第 2 组的平均值。
- 14. 关闭输入和输出文件。

```
完整程序列表
/************************************************************************************/
// 作者: D.S. Malik
//
// 程序: 班级平均分比较
// 此程序计算并比较
// 两个学生的班级平均分。
/************************************************************************************/

#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>
using namespace std;
```

# 414 | 第 7 章：用户定义函数 II

```cpp
void printResult(ofstream& outp, string courseID,
    int groupNo, double avg)
{
    int noOfSymbols;
    int count;

    if (groupNo == 1)
        outp << setw(4) << courseID << " ";
    else
        outp << " ";
    noOfSymbols = static_cast<int>(avg) / 2;

    if (groupNo == 1)
        for (count = 1; count <= noOfSymbols; count++)
            outp << '*';
    else
        for (count = 1; count <= noOfSymbols; count++)
            outp << '#';
    outp << endl;
} //endprintResult
```

我们还包含了一个函数 `printHeading` 用于打印输出的前两行。

该函数的定义为：

```cpp
void printHeading(ofstream& outp)
{
    outp << "Course" << "\tCourse Average" << endl;
    outp << " \tID" << "\t 0 10 20 30 40 50 60 70%" << endl;
    outp << "" << "\t80 100%" << endl;
    outp << "" << "\t...|...|...|...|...|...|...|...|...|...|" << endl;
}
```

### printHeading

替换前面程序中的函数 `printResult`，包含函数 `printHeading`，包含输出 1 组 **** 和 2 组 ---- 的语句，并重新运行程序。你的程序应该生成一个与之前显示的条形图类似的条形图。（完整的程序列表可在随附书籍的网站上找到。）

## 快速回顾

- 1. 没有数据类型的函数称为 `void` 函数。
- 2. `void` 函数中可以使用不带任何值的 `return` 语句。如果在 `void` 函数中使用 `return` 语句，它通常用于提前退出函数。
- 3. `void` 函数的函数头以 `void` 单词开头。
- 4. 在 C++ 中，`void` 是一个关键字。
- 5. 函数可以有参数，也可以没有参数。
- 6. 对 `void` 函数的调用是一个独立的语句。
- 7. 要调用 `void` 函数，你需要在独立语句中使用函数名连同实际参数使用。
- 8. 形式参数有两种类型：值参数和引用参数。
- 9. 值参数接收其对应的实际参数的副本。
- 10. 引用参数接收其对应的实际参数的地址（内存位置）。
- 11. 值参数的实际参数是一个表达式、变量或一个常量值。
- 12. 常量值不能传递给引用参数。
- 13. 引用参数的实际参数必须是一个变量。
- 14. 当你在形式参数的数据类型后加上 `&` 时，该形式参数就变成了引用参数。
- 15. 流变量应该通过引用传递给函数。
- 16. 如果形式参数需要改变实际参数的值，在函数头中，必须将此形式参数声明为引用参数。
- 17. 标识符的作用域是指程序中可以访问它的部分。
- 18. 在函数（或块）内声明的变量是局部变量。
- 19. 在每个函数定义（和块）之外声明的变量是全局变量。
- 20. 函数的作用域与在任何块之外声明的标识符的作用域相同。
- 21. 参见本章中的规则（标识符的作用域章节）。
- 22. C++ 不允许函数定义的嵌套。
- 23. 自动变量是在进入函数（或块）时分配内存，在退出（函数或或块）时释放内存的变量。
- 24. 静态变量是内存在整个程序执行期间保持分配状态的变量。
- 25. 根据 C++ 规定，全局变量是静态变量。
- 26. 在 C++ 中，函数可以被重载。
- 27. 如果两个函数具有不同的形式参数列表，则称这两个函数不同：
    - 形式参数的数量不同
    - 如果形式参数的数量相同，则按照列出的顺序，形式参数的数据类型在至少一个位置上不同。
- 28. 函数的签名由函数名和它的参数列表组成。如果两个函数的名称不同或参数列表不同，则它们具有不同的签名。
- 29. 如果一个函数被重载，那么在调用该函数时，签名——即函数的形式参数列表——决定了执行哪一个函数。
- 30. C++ 允许函数具有默认参数。
- 31. 如果你没有指定默认参数的值，则对该参数使用默认值。
- 32. 所有的默认参数都必须位于函数的右侧。
- 33. 假设一个函数有多个默认参数。在函数调用中，如果未指定默认参数的值，你必须省略它。
- 34. 默认值可以是常量、全局变量或函数调用。
- 35. 调用函数有权指定任何默认参数以外的其他值。
- 36. 你不能将常量值作为引用参数的默认值。

# 练习题

- 1. 判断下列陈述的对错。
    - a. 改变引用参数值的值的函数也会改变实际参数的值。
    - b. 变量名不能传递给值参数。
    - c. 如果 C++ 函数不使用参数，空参数列表周围的括号仍然是需要的。
    - d. 在 C++ 中，形式参数和实际参数的名字必须相同。
    - e. 每当引用参数的值改变时，实际参数就会改变。
    - f. 在 C++ 中，函数定义是可以嵌套的；也就是说，一个函数的定义可以包含在另一个函数的体内。
    - g. 在程序中使用全局变量比使用局部变量是更好的编程风格，因为可以避免额外的变量。
    - h. 在程序中，全局常量和全局变量一样危险。
    - i. 静态变量的内存在函数调用之间保持分配状态。

- 2. 在编程代码中识别以下内容：
    - a. 函数原型、函数头、函数体和函数定义
    - b. 函数调用语句、形式参数和实际参数
    - c. 值参数和引用参数
    - d. 局部变量和全局变量

```cpp
#include <iostream> //Line 1
using namespace std; //Line 2
int one; //Line 3
void hello(int&, double, char); //Line 4
int main() //Line 5
{
    int x; //Line 6
    double y; //Line 7
    char z; //Line 8
    hello(x, y, z); //Line 10
    hello(x, 3.5, 'S'); //Line 11
}
void hello(int first, double second, char ch) //Line 13
{
    int num; //Line 14
    double y; //Line 15
    int u; //Line 16
```

- 3. a. 解释实际参数和形式参数的区别。
    b. 解释值参数和引用参数的区别。
    c. 解释局部变量和全局变量的区别。

- 4. 下列程序的输出是什么？
