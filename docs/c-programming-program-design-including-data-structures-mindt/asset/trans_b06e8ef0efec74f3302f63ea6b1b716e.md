
- 5. 要以定点小数格式输出浮点数并保留小数点和尾随零，设置操纵符 `fixed` 和 `showpoint`。此外，要将浮点数输出到两位小数，将精度设置为两位小数。
- 6. 将第 1 组的课程平均分初始化为 `0.0`。
- 7. 将第 2 组的课程平均分初始化为 `0.0`。
- 8. 将课程数量初始化为 `0`。
- 9. 打印标题。
- 10. 获取第 1 组的课程 ID `courseId1`。
- 11. 获取第 2 组的课程 ID `courseId2`。
- 12. 对于第 1 组和第 2 组中的每门课程，
  - a. `if (courseId1 != courseId2)`
    ```cpp
    {
        cout << "Data error: Course IDs do not match.\n";
        return 1;
    }
    ```
  - b. `else`
    ```cpp
    {
    ```
    - i. 计算第 1 组的课程平均分（调用函数 `calculateAverage` 并传入适当参数）。
    - ii. 计算第 2 组的课程平均分（调用函数 `calculateAverage` 并传入适当参数）。
    - iii. 打印第 1 组的结果（调用函数 `printResult` 并传入适当参数）。
    - iv. 打印第 2 组的结果（调用函数 `printResult` 并传入适当参数）。
    - v. 更新第 1 组的平均分。
    - vi. 更新第 2 组的平均分。
    - vii. 增加课程数量。
    ```cpp
    }
    ```
  - c. 获取第 1 组的课程 ID `courseId1`。
  - d. 获取第 2 组的课程 ID `courseId2`。
- 13. a. 如果第 1 组为 `not_end_of_file` 且第 2 组为 `end_of_file`，打印“第 2 组的数据在第 1 组之前用完”
  - b. `else` 如果第 1 组为 `end_of_file` 且第 2 组为 `not_end_of_file`，打印“第 1 组的数据在第 2 组之前用完”
  - c. `else` 打印第 1 组和第 2 组的平均分。
- 14. 关闭输入和输出文件。

## 完整程序清单

```cpp
/*******************************************************
// Author: D.S. Malik
//
// Program: Comparison of Class Averages
// This program computes and compares the class averages of
// two groups of students.
********************************************************/
#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>
using namespace std;

        //function prototypes
void calculateAverage(ifstream& inp, double& courseAvg);
void printResult(ofstream& outp, string courseId,
                 int groupNo, double avg);

int main()
{
        //Step 1
    string courseId1;          //course ID for group 1
    string courseId2;          //course ID for group 2
    int numberOfCourses;
    double avg1;               //average for a course in group 1
    double avg2;               //average for a course in group 2
    double avgGroup1;          //average group 1
    double avgGroup2;          //average group 2
    ifstream group1;           //input stream variable for group 1
    ifstream group2;           //input stream variable for group 2
    ofstream outfile;           //output stream variable

    group1.open("group1.txt");                         //Step 2
    group2.open("group2.txt");                         //Step 2

    if (!group1 || !group2)                              //Step 3
    {
        cout << "Unable to open files." << endl;
        cout << "Program terminates." << endl;
        return 1;
    }

    outfile.open("student.out");                       //Step 4
    outfile << fixed << showpoint;                      //Step 5
    outfile << setprecision(2);                         //Step 5

    avgGroup1 = 0.0;                                     //Step 6
    avgGroup2 = 0.0;                                     //Step 7
    numberOfCourses = 0;                                      //Step 8

    outfile << "Course No   Group No    "
           << "Course Average" << endl;                       //Step 9

    group1 >> courseId1;                                      //Step 10
    group2 >> courseId2;                                      //Step 11
    while (group1 && group2)                                  //Step 12
    {
        if (courseId1 != courseId2)                            //Step 12a
        {
            cout << "Data error: Course IDs "
                 << "do not match." << endl;
            cout << "Program terminates." << endl;
            return 1;
        }
        else                                                  //Step 12b
        {
            calculateAverage(group1, avg1);                   //Step 12b.i
            calculateAverage(group2, avg2);                   //Step 12b.ii
            printResult(outfile, courseId1,
                        1, avg1);                             //Step 12b.iii
            printResult(outfile, courseId2,
                        2, avg2);                             //Step 12b.iv
            avgGroup1 += avg1;                    //Step 12b.v
            avgGroup2 += avg2;                    //Step 12b.vi
            outfile << endl;
            numberOfCourses++;                                //Step 12b.vii
        }
        
        group1 >> courseId1;                                  //Step 12c
        group2 >> courseId2;                                  //Step 12d
    } // end while

    if (group1 && !group2)                                    //Step 13a
        cout << "Ran out of data for group 2 "
             << "before group 1." << endl;
    else if (!group1 && group2)                              //Step 13b
        cout << "Ran out of data for group 1 "
             << "before group 2." << endl;
    else                                                   //Step 13c
    {
        outfile << "Avg for group 1: "
                << avgGroup1 / numberOfCourses
                << endl;
        outfile << "Avg for group 2: "
                << avgGroup2 / numberOfCourses
                << endl;
    }

    group1.close();                         //Step 14
    group2.close();                         //Step 14
    outfile.close();                         //Step 14

    return 0;
}

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
    } //end while

    courseAvg = totalScore / numberOfStudents;
} //end calculateAverage

void printResult(ofstream& outp, string courseId, int groupNo,
                double avg)
{
    if (groupNo == 1)
        outp << "  " << courseId << "  ";
    else
        outp << "             ";

    outp << setw(8) << groupNo << setw(17) << avg << endl;
} //end printResult
```

## 示例运行：

| 课程编号 | 组号 | 课程平均分 |
|---|---:|---:|
| CSC | 1 | 83.71 |
|  | 2 | 80.82 |
| ENG | 1 | 82.00 |
|  | 2 | 78.20 |
| HIS | 1 | 77.69 |
|  | 2 | 84.15 |
| MTH | 1 | 83.57 |
|  | 2 | 84.29 |
| PHY | 1 | 83.22 |
|  | 2 | 82.60 |

```text
Avg for group 1: 82.04
Avg for group 2: 82.01
```

## 输入数据组 1

```text
CSC 80 100 70 80 72 90 89 100 83 70 90 73 85 90 -999
ENG 80 90 80 94 90 74 78 63 83 80 90 -999
HIS 90 70 80 70 90 50 89 83 90 68 90 60 80 -999
MTH 74 80 75 89 90 73 90 82 74 90 84 100 90 79 -999
PHY 100 83 93 80 63 78 88 89 75 -999
```

## 输入数据组 2

```text
CSC 90 75 90 75 80 89 100 60 80 70 80 -999
ENG 80 80 70 68 70 78 80 90 90 76 -999
HIS 100 80 80 70 90 76 88 90 90 75 90 85 80 -999
MTH 80 85 85 92 90 90 74 89 83 65 72 90 84 100 -999
PHY 90 93 73 85 68 75 67 100 87 88 -999
```

## 条形图

在商业世界中，公司高管通常喜欢以某种可视化形式查看结果，例如条形图。许多当前可用的软件包可以分析多种形式的数据，然后以可视化形式显示结果，例如条形图或饼图。该程序的第二部分旨在以条形图形式显示先前得到的结果，如下所示：

```text
Course        Course Average
  ID      0    10    20    30    40    50    60    70    80    90   100
          |....|....|....|....|....|....|....|....|....|....|
  CSC     ******************************************
          ########################################
  ENG     ******************************************
          ########################################
    .
    .
    .
  Group 1 -- ****
  Group 2 -- ####

  Avg for group 1: 82.04
  Avg for group 2: 82.01
```

条形图中的每个符号（* 或 #）代表两分。如果课程平均分小于 2，则不打印任何符号。

由于输出采用条形图形式，我们需要修改函数 `printResult`。

## 打印条形

函数 printResult 打印课程 ID 以及表示某门课程平均分的条形图。输出存储在文件中。因此，必须向该函数传递四个参数：与输出文件关联的 ofstream 变量、组
