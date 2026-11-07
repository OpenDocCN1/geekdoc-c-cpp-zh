
函数 `func2` 有三个参数，类型分别为 `int`、`int` 和 `double`，假设分别为 a、b 和 c。编写 `func2` 的定义，使其作用如下：

- a. 提示用户输入两个整数，并分别将这两个数存入 a 和 b。
- b. 如果两个数都非零：
    - i. 如果 `a >= b`，则赋给 c 的值为 a 的 b 次方，即 aᵇ。
    - ii. 如果 `a < b`，则赋给 c 的值为 b 的 a 次方，即 bᵃ。
- c. 如果 a 非零且 b 为零，则赋给 c 的值为 a 的绝对值的平方根。
- d. 如果 b 非零且 a 为零，则赋给 c 的值为 b 的绝对值的平方根。
- e. 否则，赋给 c 的值为 0。

a、b 和 c 的值会传回调用环境。

完成 `func2` 的定义并编写其函数原型后，测试运行你的程序

- 3. 以下程序中的语句顺序不正确。重新排列这些语句，使程序输出员工每天在工作上花费的总时间。程序要求用户输入员工姓名、到达时间（到达小时、到达分钟、AM 或 PM）和离开时间（离开小时、离开分钟、AM 或 PM）。程序还允许用户按自己的意愿反复运行程序。重新排列语句后，程序必须正确缩进。

```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string employeeName;
    int arrivalHr;

    int departureHr;
    int departureMin;
    bool departureAM;

    char response;
    char discard;
    char isAM;

    cout << "This program calculates the total time spent by an "
         << "employee on the job." << endl;
    cout << "To run the program, enter (y/Y): ";
    cin >> response;
    cout << endl;
}

void timeOnJob(int arvHr, int arvMin, bool arvIsAM,
              int depHr, int depMin, bool depIsAM)
{
    int arvTimeInMin;
    int depTimeInMin;
    int timeOnJobInMin;

    else if (arvIsAM == true && depIsAM == false)
    {
        arvTimeInMin = arvHr * 60 + arvMin;
        depTimeInMin = depHr * 60 + depMin;

        timeOnJobInMin = (720 - arvTimeInMin) + depTimeInMin;
        cout << "Time spent on job: "
             << timeOnJobInMin / 60 << " hour(s) and "
             << timeOnJobInMin % 60 << " minutes." << endl;
    }

    else if (arvTimeInMin <= depTimeInMin)
    {
        timeOnJobInMin = depTimeInMin - arvTimeInMin;
        cout << "Time spent on job: "
             << timeOnJobInMin / 60 << " hour(s) and "
             << timeOnJobInMin % 60 << " minutes." << endl;
    }
    else
        cout << "Invalid input." << endl;
    if ((arvIsAM == true && depIsAM == true)
        || (arvIsAM == false && depIsAM == false))
    {
        cout << "Invalid input." << endl;
    }
}

void timeOnJob(int arvHr, int arvMin, bool arvIsAM,
              int depHr, int depMin, bool depIsAM);
```

- 4. 示例 7-5 中的函数 `printGrade` 被编写为 `void` 函数，用于计算并输出课程成绩。课程分数作为参数传递给函数 `printGrade`。将函数 `printGrade` 重写为有返回值的函数，使其计算并返回课程成绩。（课程成绩必须在 `main` 函数中输出。）同时，将函数名改为 `calculateGrade`。

- 5. 在本练习中，你要修改本章的 Classify Numbers 编程示例。按照当前写法，程序从标准输入设备（键盘）输入数据，并将结果输出到标准输出设备（屏幕）。该程序只能处理 20 个数字。重写程序以满足以下要求：

    - a. 程序的数据从长度未指定的文件输入；也就是说，程序事先不知道文件中有多少个数字。
    - b. 将程序的输出保存到文件中。
    - c. 修改函数 `getNumber`，使其从输入文件（在 main 函数中打开）读取一个数字，将该数字输出到输出文件（在 main 函数中打开），并将读取到的数字发送给 main 函数。每行只打印 10 个数字。
    - d. 让程序求出这些数字的和与平均值。
    - e. 修改函数 `printResult`，使其将最终结果输出到输出文件（在 main 函数中打开）。除了输出相应的计数外，`printResult` 的这个新定义还应输出这些数字的和与平均值。

- 6. 为了研究目的并更好地帮助学生，你当地大学的招生办公室想了解女学生和男学生在某些课程中的表现如何。你收到一个文件，其中包含某些课程女学生和男学生的 GPA。由于保密，女学生使用字母代码 f，男学生使用字母代码 m。每个文件条目由一个字母代码后跟一个 GPA 组成。每行有一个条目。文件中的条目数未知。编写一个程序，计算并输出女学生和男学生的平均 GPA。将结果格式化为两位小数。你的程序应使用以下函数：

    - a. 函数 `openFiles`：此函数打开输入文件和输出文件，并将浮点数的输出设置为固定小数格式、保留两位小数，并带小数点和尾随零。
    - b. 函数 `initialize`：此函数初始化诸如 `countFemale`、`countMale`、`sumFemaleGPA` 和 `sumMaleGPA` 等变量。
    - c. 函数 `sumGrades`：此函数计算女学生和男学生 GPA 的总和。
    - d. 函数 `averageGrade`：此函数计算女学生和男学生的平均 GPA。
    - e. 函数 `printResults`：此函数输出相关结果。
    - f. 不能有全局变量。使用适当的参数在函数中传入和传出信息。

- 7. 编写一个程序，给定形式为 month-day-year 的日期，打印该日期是当年的第几天。例如，如果输入是 1-1-2006，则日号为 1；如果输入是 12-25-2006，则日号为 359。程序应检查闰年。如果年份能被 4 整除但不能被 100 整除，则为闰年。例如，1992 和 2008 能被 4 整除，但不能被 100 整除。能被 100 整除的年份如果能同时被 400 整除，则为闰年。例如，1600 和 2000 能被 400 整除。然而，1800 不是闰年，因为 1800 不能被 400 整除。

![](img/f97f778697507bb6fdd80c5991210cba_470_0.png)

- 8. 编写一个程序，读取一个字符串，并输出其中每个小写元音出现的次数。你的程序必须包含一个函数，其参数之一为 string 变量，并返回其中每个小写元音出现的次数。还要编写一个程序来测试你的函数。（注意，如果 str 是 string 类型变量，那么 `str.at(i)` 返回第 i 个位置上的字符。第一个字符的位置是 0。此外，`str.length()` 返回 str 的长度，即 str 中的字符数。）

- 9. 按如下要求重做编程练习 8。编写一个程序，读取一个字符串，并输出其中每个小写元音出现的次数。你的程序必须包含一个函数，其参数之一为 `char` 变量，并且如果该字符是元音，则增加该元音的计数。

- 10. 编写一个函数，接受一个整数作为参数（作为 `long` 值），并返回奇数数字、偶数数字和零数字的个数。还要编写一个程序来测试你的函数。

- 11. 成为健身中心会员的费用如下：(a) 老年人折扣为 30%，(b) 如果购买并支付 12 个月或以上的会员费，则折扣为 15%，(c) 如果购买并支付超过五次私人训练课程，则每节课的折扣为 20%。编写一个菜单驱动程序来确定新会员的费用。你的程序必须包含一个显示健身中心及其收费一般信息的函数；一个获取确定会员费用所需全部信息的函数；以及一个确定会员费用的函数。使用适当的参数在函数中传入和传出信息。（不要使用任何全局变量。）

- 12. 编写一个程序，输出连续两年的通胀率以及通胀是在上升还是下降。要求用户输入某物品的当前价格及其一年前和两年前的价格。要计算某年的通胀率，用一年前该物品的价格减去该年该物品的价格，然后将结果除以一年前的价格。你的程序必须至少包含以下函数：获取输入的函数、计算结果的函数和输出结果的函数。使用适当的参数在函数中传入和传出信息。不要使用任何全局变量。

- 13. 编写一个程序，将时间从 24 小时制转换为 12 小时制，反之亦然。你的程序必须采用菜单驱动方式，让用户选择在两种表示法之间转换时间。此外，你的程序必须至少包含以下函数：将时间从 24 小时制转换为 12 小时制的函数、将时间从 12 小时制转换为 24 小时制的函数、显示选项的函数、获取输入的函数以及显示结果的函数。（对于 12 小时制时间表示，程序必须显示 AM 或 PM。）

- 14. （盒子问题）给你一块面积为例如 70 平方英寸的平整纸板，通过从每个角剪去一个正方形来制作一个无盖盒子，并且
