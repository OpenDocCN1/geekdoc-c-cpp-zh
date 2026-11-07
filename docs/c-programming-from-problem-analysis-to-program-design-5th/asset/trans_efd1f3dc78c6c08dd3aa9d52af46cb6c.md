

```cpp
printResults(zeros, odds, evens); //Step 4

return 0;
}

void initialize(int& zeroCount, int& oddCount, int& evenCount)
{
    zeroCount = 0;
    oddCount = 0;
    evenCount = 0;
}

void getNumber(int& num)
{
    cin >> num;
}

void classifyNumber(int num, int& zeroCount, int& oddCount,
                    int& evenCount)
{
    switch (num % 2)
    {
    case 0:
        evenCount++;
        if (num == 0)
            zeroCount++;
        break;
    case 1:
    case -1:
        oddCount++;
    } //end switch
} //end classifyNumber

void printResults(int zeroCount, int oddCount, int evenCount)
{
    cout << "There are " << evenCount << " evens, "
         << "which includes " << zeroCount << " zeros"
         << endl;

    cout << "The number of odd numbers is: " << oddCount
         << endl;
} //end printResults
```

**示例运行：** 在此示例运行中，用户输入带有底纹。

```text
Please enter 20 integers.
The numbers you entered are:
0 0 12 23 45 7 -2 -8 -3 -9 4 0 1 0 -7 23 -24 0 0 12
0 0 12 23 45 7 -2 -8 -3 -9 4 0 1 0 -7 23 -24 0 0 12
There are 12 evens, which includes 6 zeros
The number of odd numbers is: 8
```

**注意：** 在前一个程序中，由于假定数据是从标准输入设备（键盘）输入的，并且函数 `getNumber` 只返回一个值，因此你也可以将函数 `getNumber` 编写为返回值的函数。如果写成返回值的函数，则函数 `getNumber` 的定义如下：

```cpp
int getNumber()
{
    int num;

    cin >> num;

    return num;
}
```

在这种情况下，语句（函数调用）：

`getNumber(number);`

在函数 `main` 中应被以下语句替换：

`number = getNumber();`

当然，你还需要更改函数原型。

## 编程示例：数据比较

本编程示例说明：

- 如何在同一程序中从多个文件读取数据。
- 如何将输出发送到文件。
- 如何生成条形图。
- 如何借助函数和参数传递，在（相似的）不同数据集上使用同一程序段。
- 如何使用结构化设计解决问题以及如何进行参数传递。

本程序分为两部分。首先，你学习如何从多个文件读取数据。其次，你学习如何生成条形图。

当地一所大学的两组学生在夏季学期注册了某些特殊课程。这些课程都是第一次开设，由不同的教师授课。学期结束时，两个组参加了相同课程的相同测试，他们的成绩记录在单独的文件中。每个文件中的数据格式如下：

```text
courseNo  score1, score2, ..., scoreN --999
courseNo  score1, score2, ..., scoreM --999
.
.
.
```

让我们编写一个程序，找出每组中每门课程的平均课程分数。输出格式如下：

| 课程编号 | 组号 | 课程平均分 |
|---|---:|---:|
| CSC | 1 | 83.71 |
| CSC | 2 | 80.82 |
| ENG | 1 | 82.00 |
| ENG | 2 | 78.20 |

```text
Avg for group 1: 82.04
Avg for group 2: 82.01
```

**输入** 由于两组的数据记录在单独的文件中，输入数据出现在两个单独的文件中。

**输出** 如上所示。

## 问题分析与算法设计

从两个文件读取输入数据很简单。假设第 1 组的数据存储在文件 `group1.txt` 中，第 2 组的数据存储在文件 `group2.txt` 中。处理完一个组的数据后，我们可以处理第二个组同一课程的数据，并继续直到数据用完。每门课程的数据处理过程类似，是一个两步过程：

- 1. **求和**该课程的成绩。
  - 2. **统计**该课程的学生人数。
  - 3. **将总分除以**学生人数得到课程平均分。
- 2. 输出结果。

我们只比较每组中对应课程的平均值，每个文件中的数据按课程 ID 排序。为了确保只比较相应课程的平均值，我们比较每组的课程 ID。如果相应的课程 ID 不相同，则输出错误消息并终止程序。

这一讨论表明，我们应该编写一个函数 `calculateAverage` 来求课程平均分。我们还应该编写另一个函数 `printResult`，以给定形式输出数据。通过传递适当的参数，我们可以使用相同的函数 `calculateAverage` 和 `printResult` 来处理两组中每门课程的数据。（在程序的第二部分中，我们会修改函数 `printResult`。）

```cpp
void printResult(ofstream& outp, string courseID, int groupNo,
                 double avg)
{
    if (groupNo == 1)
        outp << "  " << courseID << "  ";
    else
        outp << "       ";

    outp << setw(8) << groupNo << setw(17) << avg << endl;
} //end printResult
```

现在我们已经设计并定义了函数 calculateAverage 和 printResult，接下来可以描述函数 main 的算法。然而，在概述算法之前，我们注意以下几点：两个输入文件中的数据很可能都按课程 ID 排序，但一个文件可能比另一个文件少一些课程。我们直到处理完两个文件并发现一个文件有未处理的数据时才会发现此错误。在打印最终答案（即第 1 组和第 2 组的平均值）之前，一定要检查这个错误。

### 主算法

- 1. 声明变量（局部声明）。
- 2. 打开输入文件。
- 3. 如果无法打开文件，则打印一条消息并终止程序。
- 4. 打开输出文件。
- 5. 要以带小数点和尾随零的定点十进制格式输出浮点数，请设置操纵符 `fixed` 和 `showpoint`。另外，要将浮点数输出到两位小数，请将精度设置为两位小数。
- 6. 将第 1 组的课程平均分初始化为 0.0。
- 7. 将第 2 组的课程平均分初始化为 0.0。
- 8. 将课程数初始化为 0。
- 9. 打印标题。
- 10. 获取第 1 组的课程 ID `courseId1`。
- 11. 获取第 2 组的课程 ID `courseId2`。
- 12. 对于第 1 组和第 2 组中的每门课程，
  - a. 如果 `(courseId1 != courseId2)`
    ```cpp
    {
        cout << "Data error: Course IDs do not match.\n";
        return 1;
    }
    ```

```cpp
//Function prototypes
void calculateAverage(ifstream& inp, double& courseAvg);
void printResult(ofstream& outp, string courseId,
                 int groupNo, double avg);

int main()
{
    //Step 1
    string courseId1;       //course ID for group 1
    string courseId2;       //course ID for group 2
    int numberOfCourses;
    double avg1;            //average for a course in group 1
    double avg2;            //average for a course in group 2
    double avgGroup1;       //average group 1
    double avgGroup2;       //average group 2
    ifstream group1;        //input stream variable for group 1
    ifstream group2;        //input stream variable for group 2
    ofstream outfile;       //output stream variable

    group1.open("group1.txt");                    //Step 2
    group2.open("group2.txt");                    //Step 2

    if (!group1 || !group2)                       //Step 3
    {
        cout << "Unable to open files." << endl;
        cout << "Program terminates." << endl;
        return 1;
    }

    outfile.open("student.out");                 //Step 4
    outfile << fixed << showpoint;                 //Step 5
    outfile << setprecision(2);                    //Step 5

    avgGroup1 = 0.0;                               //Step 6
    avgGroup2 = 0.0;                               //Step 7

    numberOfCourses = 0;                           //Step 8

    outfile << "Course No.    Group No.    "
            << "Course Average" << endl;           //Step 9

    group1 >> courseId1;                           //Step 10
    group2 >> courseId2;                           //Step 11
    while (group1 && group2)                       //Step 12
    {
        if (courseId1 != courseId2)                //Step 12a
        {
            cout << "Data error: Course IDs "
                 << "do not match." << endl;
```

