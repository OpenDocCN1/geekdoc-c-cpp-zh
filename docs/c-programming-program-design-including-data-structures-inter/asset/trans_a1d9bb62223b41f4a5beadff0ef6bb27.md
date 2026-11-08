
## 案例 2：哨兵控制的 `while` 循环

你并不总是知道需要读取多少条数据（或条目），但你可能知道最后一条条目是一个特殊值，称为 **哨兵**。在这种情况下，你在 while 语句之前读取第一个项。如果该项不等于哨兵，则执行 while 语句的主体。只要程序尚未读取到哨兵，while 循环就会继续执行。这样的 while 循环称为 **哨兵控制的 while 循环**。在这种情况下，while 循环可能如下所示：

```cpp
cin >> variable;             //initialize the loop control variable

while (variable != sentinel) //test the loop control variable
{
    .
    .
    .
    cin >> variable;         //update the loop control variable
    .
    .
}
```

### 示例 5-4

示例 5-3 中的程序计算并输出售出的饼干盒总数、总收入以及每名学生售出的平均盒数。然而，该程序假设程序员知道志愿者的确切人数。现在假设程序员不知道志愿者的确切人数。再一次假设数据采用以下格式：学生姓名后跟一个空格，然后是学生售出的盒数。由于我们不知道确切人数，我们假设 -1 将标记数据的结束。因此，考虑以下程序：

```cpp
//Program: Sentinel-Controlled Loop
//This program computes and outputs the total number of boxes of
//cookies sold, the total revenue, and the average number of
//boxes sold by each volunteer.

#include <iostream>                                      //Line 1
#include <string>                                        //Line 2
#include <iomanip>                                       //Line 3

using namespace std;                                     //Line 4

const string SENTINEL = "-1";                           //Line 5

int main()                                               //Line 6
{
    string name;                                         //Line 8
    int numOfVolunteers;                                  //Line 9
    int numOfBoxesSold;                  //Line 10
    int totalNumOfBoxesSold;             //Line 11
    double costOfOneBox;                 //Line 12

    cout << fixed << showpoint << setprecision(2);   //Line 13

    cout << "Line 14: Enter volunteers data ending "  //Line 14
         << "with -1: " << endl;

    totalNumOfBoxesSold = 0;             //Line 15
    numOfVolunteers = 0;                 //Line 16

    cin >> name;                         //Line 17

    while (name != SENTINEL)             //Line 18
    {                                    //Line 19
        cin >> numOfBoxesSold;           //Line 20
        totalNumOfBoxesSold = totalNumOfBoxesSold
                             + numOfBoxesSold; //Line 21
        numOfVolunteers++;               //Line 22
        cin >> name;                     //Line 23
    }                                    //Line 24

    cout << endl;                        //Line 25

    cout << "Line 26: The total number of boxes sold: "
         << totalNumOfBoxesSold << endl; //Line 26

    cout << "Line 27: Enter the cost of one box: "; //Line 27
    cin >> costOfOneBox;                 //Line 28
    cout << endl;                        //Line 29

    cout << "Line 30: The total money made by selling "
         << "cookies: $"
         << totalNumOfBoxesSold * costOfOneBox << endl; //Line 30

    if (numOfVolunteers != 0)            //Line 31
        cout << "Line 32: The average number of "
             << "boxes sold by each volunteer: "
             << totalNumOfBoxesSold / numOfVolunteers
             << endl;                    //Line 32
    else
        cout << "Line 34: No input." << endl; //Line 34

    return 0;                            //Line 35
}                                        //Line 36
```

**示例运行：** 在此示例运行中，用户输入以底纹显示。

```text
Line 14: Enter volunteers data ending with -1:
Sara 120
Lisa 128
Cindy 359
Nicole 267
Blair 165
Abby 290
Amy 190
Megan 450
Elizabeth 280
Meredith 290
Leslie 430
Chelsea 378
-1

Line 26: The total number of boxes sold: 3347
Line 27: Enter the cost of one box: 3.50

Line 30: The total money made by selling cookies: $11714.50
Line 32: The average number of boxes sold by each volunteer: 278
```

该程序的工作方式如下。第 8 行到第 12 行的语句声明程序中使用的变量。第 14 行的语句提示用户输入以 -1 结束的数据。第 15 行和第 16 行的语句初始化变量 totalNumOfBoxesSold 和 numOfVolunteers。第 17 行的语句读取第一个姓名并将其存储在 name 中。第 18 行的 while 语句检查 name 是否不等于 SENTINEL。（变量 name 是循环控制变量。）如果 name 不等于 SENTINEL，则执行 while 循环的主体。第 20 行的语句读取学生售出的盒数并将其存储在变量 numOfBoxesSold 中，第 21 行的语句通过将 numOfBoxesSold 加到 totalNumOfBoxesSold 上来更新 totalNumOfBoxesSold 的值。第 22 行的语句将 numOfVolunteers 的值递增 1，第 23 行的语句读取下一个姓名并将其存储到 name 中。第 20 行到第 23 行的语句重复执行，直到程序读取到 SENTINEL。第 26 行的语句输出变量 totalNumOfBoxesSold 中学生售出的盒总数，第 28 行的语句将成本输入变量 costOfOneBox 中。第 30 行的语句输出通过销售饼干获得的总收入，第 31 行到第 34 行的语句输出每名志愿者售出的平均盒数。

请注意，第 17 行的语句初始化 LCV name。第 18 行中的表达式 name != SENTINEL 检查 name 的值是否不等于 SENTINEL。第 23 行的语句重新初始化 LCV name。

接下来，考虑哨兵控制的 while 循环的另一个示例。在此示例中，提示用户输入要处理的值。如果用户想要停止程序，可以输入哨兵。

### 示例 5-5：电话号码数字

以下程序读取字母代码 A 到 Z，并打印对应的电话数字。该程序使用哨兵控制的 while 循环。要停止程序，系统会提示用户输入哨兵，即 #。这也是一个嵌套控制结构的示例，其中 if...else、switch 和 while 循环相互嵌套。

```cpp
//**********************************************************
// Program: Telephone Digits
// This is an example of a sentinel-controlled loop. This
// program converts uppercase letters to their corresponding
// telephone digits.
//**********************************************************

#include <iostream>

using namespace std;

int main()
{
    char letter;                                      //Line 1

    cout << "Program to convert uppercase "
         << "letters to their corresponding "
         << "telephone digits." << endl;              //Line 2

    cout << "To stop the program enter #."
         << endl;                                     //Line 3

    cout << "Enter a letter: ";                       //Line 4
    cin >> letter;                                    //Line 5
    cout << endl;                                     //Line 6

    while (letter != '#')                             //Line 7
    {
        cout << "The letter you entered is: "
             << letter << endl;                       //Line 8
        cout << "The corresponding telephone "
             << "digit is: ";                         //Line 9

        if (letter >= 'A' && letter <= 'Z')           //Line 10
            switch (letter)                           //Line 11
            {
                case 'A':
                case 'B':
                case 'C':
                    cout << 2 << endl;                //Line 12
                    break;                            //Line 13
```
