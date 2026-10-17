
```cpp
#include <iostream>
#include <iomanip>

using namespace std;
const int N = 20;
// 函数原型
void initialize(int& zeroCount, int& oddCount, int& evenCount);
void getNumber(int& num);
void classifyNumber(int num, int& zeroCount, int& oddCount, int& evenCount);
void printResults(int zeroCount, int oddCount, int& evenCount);
```

```cpp
int main ()
{
    // 变量声明
    int counter; //循环控制变量
    int number; // 存储新数字的变量
    int zeros; // 存储零数量的变量
    int odds; // 存储奇整数数量的变量
    int evens; // 存储偶整数数量的变量

    initialize(zeros, odds, evens); // 步骤 1

    cout << "Please enter " << N << " integers."; // 步骤 2
    cout << "The numbers you entered are: " << endl;

    for (counter = 1; counter <= N; counter++) // 步骤 3
    {
        getNumber(number); // 步骤 3a
        cout << number << " "; // 步骤 3b
        classifyNumber(number, zeros, odds, evens); // 步骤 3c
    }

    cout << endl;

    printResults(zeros, odds, evens); // 步骤 4

    return 0;
}
```

```cpp
case 1:
case -1:
    oddCount++;
} //end switch
//end classifyNumber
```

```cpp
void printResults(int zeroCount, int oddCount, int evens)
{
    cout << "There are " << evenCount << " " 
    << "which includes " << zeroCount << " zeros"
    << endl;
    cout << "The number of odd numbers is: " << oddCount
    << endl;
} //end printResults
```

### 示例运行

在此示例运行中，用户输入被阴影显示。

请输入 20 个整数。

你输入的数字是：

18 0 7 5 17 0 0 24 88 36 0 9 31 26 62 0 1 92 55 0

18 0 7 5 17 0 0 24 88 36 0 9 31 26 62 0 1 92 55 0

有 13 个偶数，包括 6 个 0

奇数的个数是： 7

> 在之前的程序中，由于假设数据是从标准输入设备（键盘）输入的，并且函数 `getNumber` 只返回一个值，你也可以将函数 `getNumber` 写成一个返回值的函数。如果写成返回值的函数，`getNumber` 的定义如下：

```cpp
int getNumber() {
    int num;
    cin >> num;
    return num;
}
```

在这种情况下，`main` 函数中的语句（函数调用）：

`getNumber(number);`

应该替换为语句：

`number = getNumber();`

当然，你还需要更改函数原型。

## 编程示例：数据比较

这个编程示例说明了以下内容：

- 如何在同一个程序中从多个文件中读取数据。
- 如何将输出发送到文件。
- 如何生成条形图。
- 在函数和参数传递的帮助，如何在不同的（但相似）的数据集上使用相同的程序段。
- 如何使用结构化设计来解决问题，以及如何进行参数传递。

该程序分为两个部分。首先，你学习如何从多个文件中读取数据。其次，你学习如何生成条形图。

当地大学的两组学生在夏季学期参加了某些课程。这些课程是首次提供的，并由不同的教师教授。学期末，两组学生都针对相同的课程参加相同的测试，他们的分数记录在单独的文件中。每个文件的数据格式如下：

```
courseNo score1, score2, ... scoreN -999
courseNo score1, score2, ... scoreM -999
```

让我们写一个程序来计算每组每门课程的平均分。输出格式如下：

| 课程编号 | 组编号 | 课程平均分 |
| --- | --- | --- |
| CSC | 1 | 83.71 |
| | 2 | 80.82 |
| ENG | 1 | 82.00 |
| | 2 | 78.20 |

组 1 的平均分：82.04

组 2 的平均分：82.01

输入：由于两组的数据记录在单独的文件中，因此输入数据出现在两个独立的文件中。

输出：如上所示。

## 第 6 章：用户自定义函数

从两个文件中读取输入数据是直接的。假设数据存储在 `group1.txt`（第 1 组）和 `group2.txt`（第 2 组）中。处理完一组数据后，我们可以处理另一组相同课程的数据，直到数据用完。处理每门课程是非常简单的，分为两步：

### 问题与算法设计

- a. 累加课程的分数。
- b. 统计课程人数。
- c. 将总分除以人数得到平均分。
- 2. 输出结果。

我们正在比较每组对应课程的平均分，每个文件的数据按课程 ID 排序。为了确保只比较对应课程的平均分，我们比较每组的课程 ID。如果相应的课程 ID 不同，我们就输出错误信息。

这些讨论建议我们写一个 `calculateAverage` 函数来查找平均分。我们还应该写另一个 `printResult` 函数来按格式输出数据。通过传递适当参数，我们可以使用相同的 `calculateAverage` 和 `printResult` 函数处理两组的每门课程数据。（在程序的第二部分，我们修改了 `printResult` 函数。）

上述讨论转化为以下算法：

- 1. 初始化变量。
- 2. 获取第 1 组和第 2 组的课程 ID。
- 3. 如果课程 ID 不同，打印错误信息并退出程序。
- 4. 计算第 1 组和第 2 组的平均分。
- 5. 按上述格式打印结果。
- 6. 对每门课程重复步骤 2 到 5。
- 7. 输出最终结果。

上述讨论建议 `main` 函数需要以下变量：

变量（函数）`main`

```cpp
string courseID1;               // 第 1 组的 ID
string courseID2;               // 第 2 组的 ID
int numberOfCourses;
double avg1;                    // 第 1 组课程的平均分
double avg2;                    // 第 2 组课程的平均分
double avgGroup1;                // 组1
double avgGroup2;                // 组2
ifstream streamGroup1;           // 第 1 组的输入流
ifstream streamGroup2;           // 第 2 组的输入流
ofstream outfile;
```

编程示例：数据比较 | 427

接下来，我们讨论 `calculateAverage` 和 `printResult` 函数。然后我们将 `main` 函数整合在一起。

`calculateAverage` 计算课程的平均分。由于输入存储在文件中，且文件在 `main` 函数中打开，我们必须将与文件的 `ifstream` 变量传递给该函数。此外，在计算平均分后，该函数必须将平均分传递给 `main` 函数。因此，该函数有两个参数，且都必须是引用参数。为了找到平均分，我们必须首先找到总和人数。因此，我们需要找到人数。上述代码转化为以下算法：

- 1. 初始化变量。
- 2. 获取（下一个）分数。
- 3. 当分数不是 `-999` 时：
   a. 通过加分数更新 `totalScore`。
   b. `numberOfStudents` 加。
   c. 获取分数。
- 4. `courseAvg = totalScore / numberOfStudents`。

我们现在准备编写 `calculateAverage` 的定义了。

```cpp
void calculateAverage(ifstream& inp, double& courseAvg)
{
    double totalScore = 0.0;
    int numberOfStudents = 0;
    int score;
    inp >> score;
    while (score != -999)
    {
        totalScore = totalScore + score;
        numberOfStudents++;
        inp >> score;
    }
    courseAvg = totalScore / numberOfStudents;
} //end calculate Average
```

428 | 第 6 章：用户自定义函数

`printResults` 函数输出课程 ID、组编号和课程平均分。输出存储在文件中。我们必须向此函数传递四个参数：与输出文件相关的 `ofstream` 变量、组编号、课程 ID 以及课程平均分。`ofstream` 变量必须通过引用传递。由于函数只使用其他变量的值，其余三个参数必须是值参数。此外，从输出可以看出，我们只在组编号之前打印课程 ID。

在伪代码中，算法是：

```
if (group number == 1)
    print course ID
else
    print a blank
```

打印组编号和课程平均分

`print` 函数的定义如下：

```cpp
void printResult(ostream& outp, string courseID, int groupNo,
double avg)
{
    if (groupNo == 1)
        outp << " " << courseID << " << ";
    else
        outp << " " << ";

    outp << setw(8) << groupNo << setw(17) << avg << endl;
}
```

现在我们已经设计并定义了 `calculateAverage` 和 `printResult` 函数，可以描述 `main` 函数的算法。在概述算法之前，我们注意到：可能在两个文件中中的数据都是根据课程 ID 排序的，但一个文件可能包含一个或多个另一个文件中没有的课程。在处理两个文件并发现一个文件有未处理的数据之前，我们不会涵盖此错误。在打印最终答案（即第 1 组和第 2 组的平均分）之前，确保检查此错误。

- 1. 声明变量（局部声明）。
- 2. 打开输入文件。
- 3. 如果无法打开文件，打印消息并终止程序。
- 4. 打开输出文件。
- 5. 要以固定小数格式输出浮点数，并保留小数点和末尾零，请设置 `fixed` 和 `showpoint`。此外，为了将浮点操纵符输出为两位小数，请将精度设置为两位。
- 6. 将组 1 的课程平均分初始化为 0.0。
- 7. 将组 2 的课程平均分初始化为 0.0。
- 8. 将课程数量初始化为 0。
- 9. 打印标题。
- 10. 获取组 1 的课程 ID `courseId1`。
- 11. 获取组 2 的课程 ID `courseId2`。
- 12. 对于组 1 和组 2 中的每门课程

```cpp
a. if (courseId1 != courseId2)
{
  cout << "Data error: Course IDs do not match.\n";
  return 1;
}
```

- b. else

{
  i. 计算组 1 的课程平均分（调用函数 `calculateAverage` 并传递适当参数）。
  ii. 计算组 2 的课程平均分（调用函数 `calculateAverage` 并传递适当参数）。
  iii. 打印组 1 的结果（调用函数 `printResult` 并传递适当参数）。
  iv. 打印组 2 的结果（调用函数 `printResult` 并传递适当参数）。
  v. 更新组 1 的平均分。
  vi. 更新组 2 的平均分。
  vii. 课程数量加 。
}

- c. 获取组 1 的课程 ID `courseId1`。
- d. 获取组 2 的课程 ID `courseId2`。
- 13. a. 如果 `not_end_file_on` 在组 1 为真，打印 "Ran out of data for group 2 before group 1"
  b. else 如果 `not_end_file_on` 在组 1 为真且 `not_end_file_on` 在组 2 为真，打印 "Ran out of data for group 1 before group 2"
  c. else 打印组 1 和组 2 的平均分。
- 14. 关闭输入和输出文件。

# 完整程序列表

```cpp
// ***************************************************************************************************
// Author: D.S. Malik
//
// Program: 级平均分比较
// 此程序计算并比较
// 两组学生的班级平均分。
// ***************************************************************************************************
```

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
```

```cpp
//函数原型
void calculateAverage(istream& inp, double& courseAvg);
void printResult(ostream& out, string courseId,
    int groupNo, double avg);
```

```cpp
int main()
{
    //Step 1
    string courseId1; // 组 1 的课程 ID
    string courseId2; // 组 2 的课程 ID
    int numberOfCourses;
    double avg1; // 组 1 某门课程的平均分
    double avg2; // 组 2 某门课程的平均分
    double avgGroup1; // 组 1 平均分
    double avgGroup2; // 组 2 平均分
    istream group1; // 组 1 的输入流变量
    istream group2; // 组 2 的输入流变量
    ostream outfile; // 输出流变量
```

```cpp
group1.open("group1.txt"); //Step 2
group2.open("group2.txt"); //Step 2
```

```cpp
if (!group1 || !group2) //Step 3
{
    cout << "Unable to open files." << endl;
    cout << "Program terminates." << endl;
    return 1;
}
```

```cpp
outfile.open("student.out"); //Step 4
outfile << fixed << showpoint; //Step 5
outfile << setprecision(2); //Step 5
```

```cpp
avgGroup1 = 0.0; //Step 6
avgGroup2 = 0.0; //Step 7
```

# 编程示例：数据比较 | 431
