
## while 循环（重复）结构

在上一节中，你已经看到有时需要重复执行一组语句若干次。C++ 有三种重复结构（或称循环结构），允许你重复执行一组语句，直到满足某些条件。本节讨论第一种循环结构，称为 while 循环。

while 语句的一般形式为：

```cpp
while (expression)
    statement
```

在 C++ 中，while 是保留字。当然，语句可以是简单语句或复合语句。表达式充当决策者，通常是逻辑表达式。该语句称为循环体。注意，表达式两侧的圆括号是语法的一部分。图 5-1 展示了 while 循环的执行流程。

![](img/b217c421655b51e7494cf3b89bb5432d_318_0.png)

图 5-1 while 循环

表达式为循环提供入口条件。如果它最初求值为 true，则语句执行。然后重新求值循环条件——即该表达式。如果它再次求值为 true，则语句再次执行。语句（循环体）会继续执行，直到表达式不再为 true。无限持续执行的循环称为无限循环。为了避免无限循环，请确保循环体包含某些语句，保证入口条件——即 while 语句中的表达式——最终会变为 false。

现在我们已经知道如何使用 while 循环重复语句，接下来重写程序，以确定一周内平均消耗的卡路里数。

```cpp
#include <iostream>

using namespace std;

int main()
{
    int calBurnedInADay;
    int calBurnedInAWeek;
    int day;

    day = 1;
    calBurnedInAWeek = 0;

    while (day <= 7)
    {
        cout << "Enter calories burned day " << day << ": ";
        cin >> calBurnedInADay;
        cout << endl;

        calBurnedInAWeek = calBurnedInAWeek + calBurnedInADay;
        day = day + 1;
    }

    cout << "Average number of calories burned each day: "
         << calBurnedInAWeek / 7 << endl;

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Enter calories burned day 1: 375
Enter calories burned day 2: 425
Enter calories burned day 3: 270
Enter calories burned day 4: 190
Enter calories burned day 5: 350
Enter calories burned day 6: 200
Enter calories burned day 7: 365
Average number of calories burned each day: 310
```

在考虑更多 *while* 循环示例之前，在下一个示例中，我们说明 *while* 语句中表达式的几点注意事项。

### 例 5-1

考虑以下 C++ 程序段：

```cpp
int i = 0;              //Line 1

while (i <= 20)         //Line 2
{                       //Line 3
    cout << i << " ";   //Line 4
    i = i + 5;          //Line 5
}                       //Line 6

cout << endl;           //Line 7
```

在这个程序段中，第 1 行的语句将 `i` 声明为 `int` 变量，并将其初始化为 0。第 2 行到第 6 行的语句构成 `while` 循环。`while` 语句中的 `expression`，即 `i <= 20`，位于第 2 行；`while` 循环的循环体是第 3 行到第 6 行。只要 `expression` `i <= 20` 求值为 `true`，`while` 循环的循环体就会继续执行。下表展示了 `while` 循环的迭代过程。

| 迭代 | `i` 的值 | 第 2 行中的表达式 | 第 4 行和第 5 行中的语句 |
|---|---|---|---|
| 1 | `i = 0` | `i <= 20` 为真 | 输出：0<br>`i = i + 5 = 0 + 5 = 5` |
| 2 | `i = 5` | `i <= 20` 为真 | 输出：5<br>`i = i + 5 = 5 + 5 = 10` |
| 3 | `i = 10` | `i <= 20` 为真 | 输出：10<br>`i = i + 5 = 10 + 5 = 15` |
| 4 | `i = 15` | `i <= 20` 为真 | 输出：15<br>`i = i + 5 = 15 + 5 = 20` |
| 5 | `i = 20` | `i <= 20` 为真 | 输出：20<br>`i = i + 5 = 20 + 5 = 25` |
| 6 | `i = 25` | `i <= 20` 为假 | 循环终止 |

前面的 `while` 循环产生以下输出：

```text
0 5 10 15 20
```

表达式中的变量 `i`（在第 2 行）称为**循环控制变量**。此外，我们还要注意以下几点：

- a. 在第六次迭代中，`i` 变为 25，但没有被打印，因为入口条件为 `false`。

- b. 如果从循环体中省略语句：

  ```cpp
  i = i + 5;
  ```

  则会出现无限循环，不断打印一行行的零。

- c. 必须在执行循环之前初始化循环控制变量 `i`。如果省略语句：

  ```cpp
  i = 0;
  ```

  （在第 1 行），则循环可能根本不执行。（回顾一下，C++ 中的变量不会自动初始化。）

- d. 如果循环体中的两条语句，即第 4 行和第 5 行，互换位置，可能会极大地改变结果。例如，考虑以下语句：

  ```cpp
  i = 0;

  while (i <= 20)
  {
      i = i + 5;
      cout << i << " ";
  }

  cout << endl;
  ```

  这里，输出为：

  ```text
  5 10 15 20 25
  ```

- e. 如果在 `while` 循环末尾（逻辑表达式之后）放置分号，那么 `while` 循环的动作语句为空或空语句。例如，以下 `while` 循环的动作语句为空。

  ```cpp
  int i = 0;

  while (i <= 20);
  {
      i = i + 5;
      cout << i << " ";
  }

  cout << endl;
  ```

  大括号内的语句不构成 `while` 循环的循环体。

## 设计 `while` 循环

如例 5-1 所示，仅当 `while` 语句中的**表达式**求值为 `true` 时，`while` 的循环体才会执行。通常，该表达式检查一个称为**循环控制变量（LCV）**的变量是否满足某些条件。例如，在例 5-1 中，`while` 语句中的表达式检查 `i <= 20` 是否成立。在遇到 `while` 循环之前，必须正确初始化 LCV，并且它最终应使表达式求值为 `false`。我们通过在 `while` 循环的循环体中更新 LCV 或为其赋新值来实现这一点。因此，通常 `while` 循环按以下形式编写：

```cpp
//initialize the loop control variable(s)

while (expression)  //expression tests the LCV
{
    .
    .
    .
    // update the LCV
    .
    .
    .
}
```

例如，在例 5-1 中，第 1 行的语句将 LCV `i` 初始化为 0。第 2 行中的表达式 `i <= 20` 检查 `i` 是否小于或等于 20。第 5 行的语句更新 `i` 的值，最终使 `i` 大于 20，并使表达式 `i <= 20` 求值为 `false`。

`while` 语句中的表达式可能包含多个用于控制循环的变量。在这种情况下，循环具有多个 LCV，并且所有 LCV 都必须正确初始化并更新。

### 例 5-2

考虑以下 C++ 程序段：

```cpp
i = 20;                 //Line 1
while (i < 20)          //Line 2
{                       //Line 3
    cout << i << " ";   //Line 4
    i = i + 5;          //Line 5
}                       //Line 6
cout << endl;           //Line 7
```

很容易忽略此示例与例 5-1 之间的差异。在此示例中，第 1 行将 `i` 初始化为 20，这使得 `while` 语句（第 2 行）中的表达式 `i < 20` 求值为 `false`。由于最初循环入口条件 `i < 20` 为 `false`，因此 `while` 循环的循环体永远不会执行。因此，不会输出任何值，并且 `i` 的值仍为 20。此示例说明了 LCV 初始化值的重要性。

```cpp
#include <iostream>                                      //Line 1
#include <string>                                         //Line 2
#include <iomanip>                                        //Line 3

using namespace std;                                      //Line 4

int main()                                               //Line 5
{                                                         //Line 6
    string name;                                          //Line 7
    int numOfVolunteers;                                  //Line 8
    int numOfBoxesSold;                                   //Line 9
    int totalNumOfBoxesSold;                              //Line 10
    int counter;                                          //Line 11
    double costOfOneBox;                                  //Line 12

    cout << fixed << showpoint << setprecision(2);         //Line 13

    cout << "Line 14: Enter the number of "
         << "volunteers: ";                              //Line 14
    cin >> numOfVolunteers;                               //Line 15
    cout << endl;                                         //Line 16

    totalNumOfBoxesSold = 0;                              //Line 17
    counter = 0;                                          //Line 18

    while (counter < numOfVolunteers)                     //Line 19
    {                                                     //Line 20
        cout << "Line 21: Enter the volunteer's name"
             << " and the number of boxes sold: ";       //Line 21
        cin >> name >> numOfBoxesSold;                    //Line 22
        cout << endl;                                     //Line 23
        totalNumOfBoxesSold = totalNumOfBoxesSold
                            + numOfBoxesSold;             //Line 24
        counter++;                                        //Line 25
    }                                                     //Line 26

    cout << "Line 27: The total number of boxes sold: "
         << totalNumOfBoxesSold << endl;                  //Line 27

    cout << "Line 28: Enter the cost of one box: ";      //Line 28
    cin >> costOfOneBox;                                  //Line 29
    cout << endl;                                         //Line 30

    cout << "Line 31: The total money made by selling "
         << "cookies: $"
         << totalNumOfBoxesSold * costOfOneBox << endl;   //Line 31

    if (counter != 0)                                     //Line 32
        cout << "Line 33: The average number of "
             << "boxes sold by each volunteer: "
             << totalNumOfBoxesSold / counter << endl;    //Line 33
```

