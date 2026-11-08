
接下来，考虑以下语句：

```cpp
int numberOfLines = 15;
int numberOfBlanks = 30;

for (counter = 1; counter <= numberOfLines; counter++)
{
    printStars(numberOfBlanks, counter);
    numberOfBlanks--;
}
```

for 循环调用函数 printStars。该 for 循环的每次迭代都会使用变量 numberOfBlanks 和 counter 指定要在一行中打印的空格数以及随后的星号数。每次调用函数 printStars 时，收到的空格数都比上一次调用少一个，星号数多一个。例如，主程序中 for 循环的第一次迭代指定 30 个空格和 1 个星号（它们作为参数 numberOfBlanks 和 counter 传递给函数 printStars）。然后，for 循环通过执行语句 numberOfBlanks--; 将空格数减 1。在 for 循环末尾，星号数会为下一次迭代增加 1。这是通过执行 for 语句中的更新语句 counter++ 来完成的，该语句将变量 counter 的值增加 1。换句话说，第二次调用函数 printStars 时，接收 29 个空格和 2 个星号作为参数。因此，前面的语句将打印一个由 15 行组成的星号三角形。

```cpp
//Program: Print a triangle of stars

#include <iostream>

using namespace std;

void printStars(int blanks, int starsInLine);

int main()
{
    int noOfLines;    //variable to store the number of lines
    int counter;      //for loop control variable
    int noOfBlanks;   //variable to store the number of blanks

    cout << "Enter the number of star lines (1 to 20) "
         << "to be printed: ";                         //Line 1

    cin >> noOfLines;                                   //Line 2

    while (noOfLines < 0 || noOfLines > 20)             //Line 3
    {
        cout << "Number of star lines should be "
             << "between 1 and 20" << endl;             //Line 4
        cout << "Enter the number of star lines "
             << "(1 to 20) to be printed: ";            //Line 5
        cin >> noOfLines;                                //Line 6
    }

    cout << endl << endl;                         //Line 7
    noOfBlanks = 30;                              //Line 8

    for (counter = 1; counter <= noOfLines; counter++) //Line 9
    {
        printStars(noOfBlanks, counter);          //Line 10
        noOfBlanks--;                              //Line 11
    }

    return 0;                                     //Line 12
}

void printStars(int blanks, int starsInLine)
{
    int count;

    for (count = 1; count <= blanks; count++)  //Line 13
        cout << ' ';                           //Line 14
    for (count = 1; count <= starsInLine; count++) //Line 15
        cout << "*";                           //Line 16
    cout << endl;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

输入要打印的星线行数（1 到 20）：**15**

```
              *
             * *
            * * *
           * * * *
          * * * * *
         * * * * * *
        * * * * * * *
       * * * * * * * *
      * * * * * * * * *
     * * * * * * * * * *
    * * * * * * * * * * *
   * * * * * * * * * * * *
  * * * * * * * * * * * * *
 * * * * * * * * * * * * * *
* * * * * * * * * * * * * * *
```

在函数 main 中，首先要求用户指定要打印多少行星号（第 1 行）。（在此程序中，用户被限制为最多 20 行，因为最多 20 行的三角形网格可以很好地适应屏幕。）由于程序限制为最多 20 行，因此第 3 行到第 6 行的 while 循环确保：当行数在 1 到 20 之间时，程序只打印星号三角形网格。

## 值参数

上一节定义了两种参数——值参数和引用参数。示例 6–10 展示了一个使用带参数函数的程序。在考虑更多带参数的 void 函数示例之前，我们先对值参数和引用参数作如下观察。调用函数时，实际参数的值会被复制到相应的形式参数中。如果形式参数是值参数，那么在复制实际参数的值之后，形式参数和实际参数之间就没有联系；也就是说，形式参数拥有自己的一份数据副本。因此，在程序执行期间，形式参数操作的是存储在其自身内存空间中的数据。示例 6–11 中的程序进一步说明了值参数如何工作。

### 示例 6-11

下面的程序展示了简单数据类型的形式参数如何工作。

```cpp
//Example 6-11
//Program illustrating how a value parameter works.

#include <iostream>

using namespace std;

void funcValueParam(int num);

int main()
{
    int number = 6;                                      //Line 1

    cout << "Line 2: Before calling the function "
         << "funcValueParam, number = " << number
         << endl;                                        //Line 2

    funcValueParam(number);                              //Line 3

    cout << "Line 4: After calling the function "
         << "funcValueParam, number = " << number
         << endl;                                        //Line 4

    return 0;
}

void funcValueParam(int num)
{
    cout << "Line 5: In the function funcValueParam, "
         << "before changing, num = " << num
         << endl;                                        //Line 5

    num = 15;                                             //Line 6
```

引用参数在三种情况下很有用：

- 当需要更改实际参数的值时
- 当希望从函数返回多个值时（回想一下，return 语句只能返回一个值）
- 当传递地址相对于复制大量数据可以节省内存空间和时间时

本书通篇都说明了前两种情况。第 8 章和第 10 章在介绍数组和类时讨论第三种情况。

回想一下，当你在函数的形式参数列表中在 dataType 后附加 & 时，该 dataType 后面的变量就会成为引用参数。

> 你可以使用关键字 `const` 将引用（形式）参数声明为常量。第 9 章和第 10 章将讨论常量引用参数。在此之前，你将使用的引用参数都是本章所定义的非恒定引用参数。从引用参数的定义可知，常量值或表达式不能传递给非恒定引用参数。如果形式参数是非恒定引用参数，那么在函数调用期间，其对应的实际参数必须是变量。

### 示例 6-12：计算成绩

下面的程序接收课程分数（0 到 100 之间的值），并确定学生的课程成绩。该程序有三个函数：`main`、`getScore` 和 `printGrade`，如下所示：

1. `main`
   - 获取课程分数。
   - 打印课程成绩。
2. `getScore`
   - 提示用户输入。
   - 获取输入。
   - 打印课程分数。
3. `printGrade`
   - 计算课程成绩。
   - 打印课程成绩。

完整程序如下：

```cpp
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
         << "    this program computes the "
         << "course grade." << endl;        //Line 1

    getScore(courseScore);                   //Line 2

    printGrade(courseScore);                 //Line 3

    return 0;
}

void getScore(int& score)
{
    cout << "Line 4: Enter course score: ";  //Line 4
    cin >> score;                            //Line 5
    cout << "Line 6: Course score is "
         << score << endl;                   //Line 6
}

void printGrade(int cScore)
{
    cout << "Line 7: Your grade for the course is "; //Line 7

    if (cScore >= 90)
        cout << "A." << endl;               //Line 8
    else if (cScore >= 80)
        cout << "B." << endl;
    else if (cScore >= 70)
        cout << "C." << endl;
    else if (cScore >= 60)
        cout << "D." << endl;
    else
        cout << "F." << endl;
}
```
