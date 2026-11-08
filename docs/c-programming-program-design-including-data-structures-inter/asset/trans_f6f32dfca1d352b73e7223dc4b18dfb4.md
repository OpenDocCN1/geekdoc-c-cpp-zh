
最终使该表达式的求值为 `false`。我们通过在 `while` 循环体中更新或重新初始化 LCV 来做到这一点。因此，通常 `while` 循环会写成以下形式：

```cpp
//initialize the loop control variable(s)

while (expression)  //expression tests the LCV
{
   .
   .
   .
   //update the loop control variable(s)
   .
   .
   .
}
```

例如，在示例 5-1 中，第 1 行的语句将 LCV `i` 初始化为 0。第 2 行的表达式 `i <= 20` 检查 `i` 是否小于等于 20，第 4 行的语句更新 `i` 的值。

### 示例 5-2

考虑以下 C++ 程序段：

```cpp
i = 20;                  //Line 1
while (i < 20)           //Line 2
{
    cout << i << " ";    //Line 3
    i = i + 5;           //Line 4
}
cout << endl;            //Line 5
```

很容易忽略本示例与示例 5-1 之间的区别。在本示例中，第 1 行将 `i` 设为 20。由于 `i` 为 20，`while` 语句（第 2 行）中的表达式 `i < 20` 求值为 `false`。由于一开始循环进入条件 `i < 20` 就是 `false`，所以 `while` 循环体永远不会执行。因此不会输出任何值，`i` 的值仍为 20。

接下来几节介绍 `while` 循环的各种形式。

## 情况 1：计数器控制的 `while` 循环

假设你确切知道某些语句需要执行多少次。例如，假设你确切知道需要读取多少个数据项（或条目）。在这种情况下，`while` 循环采用**计数器控制的 `while` 循环**形式。假设一组语句需要执行 *N* 次。你可以设置一个计数器（在 `while` 语句之前初始化为 0），用于跟踪已读取多少个项。在执行 `while` 语句的循环体之前，会将计数器与 N 进行比较。如果 counter < N，则执行 `while` 语句的循环体。循环体会继续执行，直到 counter >= N。因此，在 `while` 语句的循环体内部，计数器在读取一个新项后递增。在这种情况下，`while` 循环可能如下所示：

```cpp
counter = 0;          //initialize the loop control variable

while (counter < N) //test the loop control variable
{
    .
    .
    .
    counter++;        //update the loop control variable
    .
    .
    .
}
```

如果 *N* 表示文件中的数据项数，则可以通过几种方式确定 *N* 的值。程序可以提示你指定文件中的项数；输入语句可以读取该值；或者你可以将文件中的第一项指定为文件中的项数，这样就不必记住输入值（项）的数量。如果由程序员以外的人输入数据，这会很有用。考虑示例 5-3。

### 示例 5-3

当地一所中学的学生自愿出售新鲜烘焙的饼干，以筹集资金为计算机实验室增加计算机数量。每位学生报告了他/她售出的盒数。我们将编写一个程序，输出售出的饼干总盒数、销售饼干产生的总收入，以及每位学生平均售出的盒数。所提供的数据采用以下形式：

`studentName numOfBoxesSold`

考虑以下程序：

```cpp
//Program: Counter-Controlled Loop
//This program computes and outputs the total number of boxes of
//cookies sold, the total revenue, and the average number of
//boxes sold by each volunteer.

#include <iostream>                           //Line 1
#include <string>                             //Line 2
#include <iomanip>                            //Line 3

using namespace std;                          //Line 4

int main()                                    //Line 5
{
    string name;                                      //Line 6
    int numOfVolunteers;                              //Line 7
    int numOfBoxesSold;                               //Line 8
    int totalNumOfBoxesSold;                          //Line 9
    int counter;                                      //Line 10
    double costOfOneBox;                              //Line 12

    cout << fixed << showpoint << setprecision(2);    //Line 13

    cout << "Line 14: Enter the number of "
         << "volunteers: ";                          //Line 14
    cin >> numOfVolunteers;                           //Line 15
    cout << endl;                                     //Line 16

    totalNumOfBoxesSold = 0;                          //Line 17
    counter = 0;                                      //Line 18

    while (counter < numOfVolunteers)                 //Line 19
    {
        cout << "Line 21: Enter the volunteer's name"
             << " and the number of boxes sold: ";    //Line 21
        cin >> name >> numOfBoxesSold;                //Line 22
        cout << endl;                                 //Line 23
        totalNumOfBoxesSold = totalNumOfBoxesSold
                            + numOfBoxesSold;         //Line 24
        counter++;                                    //Line 25
    }                                                //Line 26

    cout << "Line 27: The total number of boxes sold: "
         << totalNumOfBoxesSold << endl;              //Line 27

    cout << "Line 28: Enter the cost of one box: ";   //Line 28
    cin >> costOfOneBox;                              //Line 29
    cout << endl;                                     //Line 30

    cout << "Line 31: The total money made by selling "
         << "cookies: $"
         << totalNumOfBoxesSold * costOfOneBox << endl; //Line 31

    if (counter != 0)                                //Line 32
        cout << "Line 33: The average number of "
             << "boxes sold by each volunteer: "
             << totalNumOfBoxesSold / counter << endl; //Line 33
    else                                               //Line 34
        cout << "Line 35: No input," << endl;         //Line 35

    return 0;                                         //Line 36
}                                                    //Line 37
```

### 示例运行：

在此示例运行中，用户输入以底纹显示。

```text
Line 14: Enter the number of volunteers: 5
Line 21: Enter the volunteer’s name and the number of boxes sold: Sara 120
Line 21: Enter the volunteer’s name and the number of boxes sold: Lisa 128
Line 21: Enter the volunteer’s name and the number of boxes sold: Cindy 359
Line 21: Enter the volunteer’s name and the number of boxes sold: Nicole 267
Line 21: Enter the volunteer’s name and the number of boxes sold: Blair 165
Line 27: The total number of boxes sold: 1039
Line 28: Enter the cost of one box: 3.50
Line 31: The total money made by selling cookies: $3636.50
Line 33: The average number of boxes sold by each volunteer: 207
```

该程序的工作方式如下。第 7 行至第 12 行的语句声明程序中使用的变量。第 14 行的语句提示用户输入学生志愿者人数。第 15 行的语句将此数字输入变量 numOfVolunteers。第 17 行和第 18 行的语句初始化变量 totalNumOfBoxesSold 和 counter。（变量 counter 是循环控制变量。）

第 19 行的 while 语句检查 counter 的值，以确定已读取多少名学生的数据。如果 counter 小于 numOfVolunteers，则 while 循环继续下一次迭代。第 21 行的语句提示用户输入学生姓名和学生售出的盒数。第 22 行的语句将学生姓名输入变量 name，并将学生售出的盒数输入变量 numOfBoxesSold。第 24 行的语句通过将 numOfBoxesSold 的值加到先前的值上来更新 totalNumOfBoxesSold 的值，第 25 行的语句将 counter 的值递增 1。第 27 行的语句输出售出的总盒数，第 28 行的语句提示用户输入一盒饼干的成本，第 29 行的语句将成本输入变量 costOfOneBox。第 31 行的语句输出销售饼干所得总金额，第 32 行至第 35 行的语句输出每位志愿者平均售出的盒数。

注意，在此程序中，第 17 行将 totalNumOfBoxesSold 初始化为 0。在第 22 行中，读取一名学生售出的盒数后，程序会将其加到当前盒数之前所有已售盒数的总和中。读取到的第一个 numOfBoxesSold 会加到零上（因为 totalNumOfBoxesSold 被初始化为 0），从而得到第一个数字的正确总和。要计算平均值，请将 totalNumOfBoxesSold 除以 counter。如果 counter 为 0，那么除以零将终止程序，并会收到错误消息。因此，在将 totalNumOfBoxesSold 除以 counter 之前，必须检查 counter 是否为 0。

注意，在此程序中，第 18 行的语句将 LCV counter 初始化为 0。第 19 行的表达式 counter < numOfVolunteers 判断 counter 是否小于 numOfVolunteers。第 25 行的语句更新 counter 的值。
