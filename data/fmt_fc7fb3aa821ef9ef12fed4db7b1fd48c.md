
    `noOfBlanks` = 30;

    for (`counter` = 1; `counter` <= `noOfLines`; `counter`++) {

        `printStars`(`noOfBlanks`, `counter`);

        `noOfBlanks`--;

    }

    return 0;

}

void `printStars`(int `blanks`, int `starsInLine`) {

    int `count`;

    for (`count` = 1; `count` <= `blanks`; `count`++) {

        // 打印空格的逻辑 

    }

    for (`count` = 1; `count` <= `starsInLine`; `count`++) {

        `cout` << "*";

        if (`count` < `starsInLine`) {

            `cout` << " ";

        }

    }

    `cout` << `endl`;

}

```
*(注：由于原文代码块中 `printStars` 的实现不完整，翻译时保持代码逻辑结构)*
```cpp
//程序：打印星号三角形
#include <iostream>
using namespace std;
void `printStars`(int `blanks`, int `starsInLine`);
int `main`() {
    int `noOfLines`; // 用于存储行数的变量
    int `counter`; // for 循环控制变量
    int `noOfBlanks`; // 用于存储空格数的变量
    `cout` << "Enter the number of star lines (1 to 20) ";
    `cout` << "to be printed: ";
    `cin` >> `noOfLines`;
    while (`noOfLines` < 0 || `noOfLines` > 20) {
        `cout` << "Enter the number of star lines ";
        `cout` << "(1 to 20) to be printed: ";
        `cin` >> `noOfLines`;
    }
    `cout` << `endl`;
    `noOfBlanks` = 30;
    for (`counter` = 1; `counter` <= `noOfLines`; `counter`++) {
        `printStars`(`noOfBlanks`, `counter`);
        `noOfBlanks`--;
    }
    return 0;
}
void `printStars`(int `blanks`, int `starsInLine`) {
    int `count`;
    for (`count` = 1; `count` <= `blanks`; `count`++) {
        // 打印空格的逻辑
    }
    for (`count` = 1; `count` <= `starsInLine`; `count`++) {
        `cout` << "*";
        if (`count` < `starsInLine`) {
            `cout` << " ";
        }
    }
    `cout` << `endl`;
}
```
*(注：原文提供的文本中 `printStars` 定义部分似乎截断，此处根据语意完成翻译并保持格式)*

*(更正：根据原文提供的文本，最后的 `printStars` 代码块存在缺失，以下为基于原文内容的对应翻译)*
```cpp
void `printStars`(int `blanks`, int `starsInLine`) {
    int `count`;
    for (`count` = 1; `count` <= `blanks`; `count`++) {
        // 打印空格
    }
    for (`count` = 1; `count` <= `starsInLine`; `count`++) {
        // 打印星号
    }
    `cout` << `endl`;
}
```
示例输出：
Enter the number of star lines (1 to 20) to be printed: 5
                                 *
                              * *
                            * * *
                          * * * *
                        * * * * *
*(注：原文文本结尾部分混乱，此处为核心逻辑说明)*

## 示例 6-13
## 计算成绩

以下程序接收一个课程得分（0 到 100 之间的值）并确定学生的课程成绩。该程序有三个函数：`main`、`getScore` 和 `printGrade`，如下：

- 1. `main`
   a. 获取课程得分。
   b. 打印课程成绩。
- 2. `getScore`
   a. 提示用户输入。
   b. 获取输入。
   c. 打印课程得分。
- 3. `printGrade`
   a. 计算课程成绩。
   b. 打印课程成绩。

完整程序如下：
```cpp
//This程序读取课程得分并打印
//相关的课程成绩。
#include <iostream>
using namespace std;
void `getScore`(int& `score`);
void `printGrade`(int `score`);
int `main`() {
    int `courseScore`;
    `cout` << "Line 8: Based on the course score, \n"
         << "this program computes the \n"
         << "course grade." << `endl`;
    `getScore`(`courseScore`);
    `printGrade`(`courseScore`);
    return 0;
}
```
```cpp
void `getScore`(int& `score`) //Line 13
{
    `cout` << "Line 15: Enter course score: "; //Line 14
    `cin` >> `score`; //Line 15
    `cout` << `endl` << "Line 17: The course score is " //Line 16
    << `score` << `endl`; //Line 17
} //Line 18
```
```cpp
void `printGrade`(int `cScore`) //Line 19
{
    `cout` << "Line 21: The course grade is: " //Line 20
    if (`cScore` >= 90) //Line 22
        `cout` << "A." << `endl`; //Line 23
    else if (`cScore` >= 80) //Line 24
        `cout` << "B." << `endl`; //Line 25
    else if (`cScore` >= 70) //Line 26
        `cout` << "C." << `endl`; //Line 27
    else if (`cScore` >= 60) //Line 28
        `cout` << "D." << `endl`; //Line 29
    else //Line 30
        `cout` << "F." << `endl`; //Line 31
} //Line 32
```
示例运行：在此示例运行中，用户输入被阴影显示。
Line 8: Based on the course score,
this program computes the course grade.
Line 15: Enter course score: 85
Line 17: The course score is 85
Line 21: The course grade is: B.

该程序的工作原理如下。程序从 Line 8 开始执行，打印输出输出的第一行（参见示例运行）。Line 9 中的语句调用了函数 `getScore`，并传入了实际参数 `courseScore`（在 `main` 中声明的变量）。由于函数 `getScore` 的形式参数 `score` 是引用参数，地址（即变量 `courseScore` 的内存位置）传递给了 `score`。因此，`score` 和 `courseScore` 指向同一个内存位置，即 `courseScore`（见图 6-5）。

![](img/d998292a174f7bfd8a26bfbada3d454e_437_0.png)
图 6-5 变量 `courseScore` 和参数 `score`

对 `score` 的任何更改都会立即改变 `courseScore` 的值。控制转移到 Line 15 执行的函数 `getScore`，打印输出的第一行。该语句提示用户输入课程得分。Line 16 中的语句读取并存储用户输入的值（示例运行中为 85）到 `score`，这实际上是 `courseScore`（因为 `score` 是引用参数）。因此，在此时，两个变量 `score` 和 `courseScore` 的值均为 85（见图 6-6）。

![](img/d998292a174f7bfd8a26bfbada3d454e_438_0.png)
图 6-6 在 Line 16 语句执行后，变量 `courseScore` 和参数 `score`

接下，Line 17 中的语句输出 `score` 的值，如示例运行的第三行所示。Line 17 执行后，控制返回到函数 `main`（见图 6-7）。

![](img/d998292a174f7bfd8a26bfbada3d454e_438_1.png)
图 6-7 在 Line 17 语句执行后，变量 `courseScore`，控制返回 `main`

Line 10 中的语句接着执行。它是对函数 `printGrade` 的调用，传入了实际参数 `courseScore`。由于函数 `printGrade` 的形式参数 `cScore` 是值参数，参数 `cScore` 接收了相应实际参数 `courseScore` 的值。因此，`cScore` 的值为 85。在将 `courseScore` 的值复制到 `cScore` 后，`cScore` 和 `courseScore` 之间不再存在通信（见图 6-8）。

![](img/d998292a174f7bfd8a26bfbada3d454e_438_2.png)
图 6-8 变量 `courseScore` 和参数 `cScore`

程序执行 Line 21 中的语句，如示例运行的最后一行所示。
- **示例 6-13**
  - 计算成绩
以下程序接收一个课程得分（0 到 100 之间的值）并确定学生的课程成绩。该程序有三个函数：`main`、`getScore` 和 `printGrade`，如下：
- 1. `main`
   a. 获取课程得分。
   b. 打印课程成绩。
- 2. `getScore`
   a. 提示用户输入。
   b. 获取输入。
   c. 打印课程得分。
- 3. `printGrade`
   a. 计算课程成绩。
   b. 打印课程成绩。
完整程序如下：
```cpp
//This程序读取课程得分并打印
//相关的课程成绩。
#include <iostream>
using namespace std;
void `getScore`(int& `score`);
void `printGrade`(int `score`);
int `main`() {
    int `courseScore`;
    `cout` << "Line 8: Based on the course score, \n"
         << "this program computes the \n"
         << "course grade." << `endl`;
    `getScore`(`courseScore`);
    `printGrade`(`courseScore`);
    return 0;
}
```
```cpp
void `getScore`(int& `score`) //Line 13
{
    `cout` << "Line 15: Enter course score: "; //Line 14
    `cin` >> `score`; //Line 15
    `cout` << `endl` << "Line 17: The course score is " //Line 16
    << `score` << `endl`; //Line 17
} //Line 18
```
```cpp
void `printGrade`(int `cScore`) //Line 19
{
    `cout` << "Line 21: The course grade is: " //Line 20
    if (`cScore` >= 90) //Line 22
        `cout` << "A." << `endl`; //Line 23
    else if (`cScore` >= 80) //Line 24
        `cout` << "B." << `endl`; //Line 25
    else if (`cScore` >= 70) //Line 26
        `cout` << "C." << `endl`; //Line 27
    else if (`cScore` >= 60) //Line 28
        `cout` << "D." << `endl`; //Line 29
    else //Line 30
        `cout` << "F." << `endl`; //Line 31
} //Line 32
```
