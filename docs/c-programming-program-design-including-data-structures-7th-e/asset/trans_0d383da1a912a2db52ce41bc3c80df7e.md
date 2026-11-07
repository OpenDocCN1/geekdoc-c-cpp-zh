
```cpp
int main()
{
    int num = 4;

    cout << "Line 1: The value returned by funcRet1: "
         << funcRet1() << endl;                         // Line 1
    cout << "Line 2: The value returned by funcRet2: "
         << funcRet2(num) << endl;                      // Line 2

    return 0;
}

int funcRet1()
{
    int x = 45;

    return 23, x;   //only the value of x is returned
}

int funcRet2(int z)
{
    int a = 2;
    int b = 3;

    return 2 * a + b, z + b; //only the value of z + b is returned
}
```

```text
Sample Run:

Line 1: The value returned by funcRet1: 45
Line 2: The value returned by funcRet2: 7
```

尽管一个 `return` 语句可以包含多个表达式，但程序中的 return 语句应只包含一个表达式。在 `return` 语句中包含多个表达式可能导致冗余、浪费代码以及语法混乱。

## 更多返回值函数的示例

### 例 6-3

在本例中，我们编写函数 `courseGrade` 的定义。该函数接受一个 `int` 值作为参数，指定某门课程的分数，并返回该课程的成绩等级，其类型为 `char`。（我们假设考试分数是 0 到 100（含）之间的值。）

```cpp
char courseGrade(int score)
{
    switch (score / 10)
    {
        case 0:
        case 1:
        case 2:
        case 3:
        case 4:
        case 5:
            return 'F';
        case 6:
            return 'D';
        case 7:
            return 'C';
        case 8:
            return 'B';
        case 9:
        case 10:
            return 'A';
    }
}
```

你也可以编写函数 courseGrade 的等效定义，使用 if...else 结构来确定课程成绩。

### 例 6-4（掷一对骰子）

在本例中，我们编写一个函数，掷一对骰子，直到掷出的数字之和为某个特定数。我们还想知道为了得到目标总和需要掷多少次骰子。

每个骰子上的最小数字是 1，最大数字是 6。因此，掷出的数字之和最小为 2，最大为 12。假设我们有如下声明：

```cpp
int die1;
int die2;
int sum;
int rollCount = 0;
```

我们使用第 5 章讨论过的随机数生成器来随机生成一个 1 到 6 之间的数。然后，下面的语句随机生成一个 1 到 6 之间的数，并将该数存入 die1，它成为 die1 掷出的数。

```cpp
die1 = rand() % 6 + 1;
```

同样，下面的语句随机生成一个 1 到 6 之间的数，并将该数存入 die2，它成为 die2 掷出的数。

```c
die2 = rand() % 6 + 1;
```

两个骰子掷出的数字之和为：

```c
sum = die1 + die2;
```

接下来，我们判断 sum 是否包含骰子掷出的目标总和。（假设 int 变量 num 包含要掷出的目标总和。）如果 sum 不等于 num，则我们再次掷骰子。这可以通过下面的 do...while 循环完成。

```c
do
{
    die1 = rand() % 6 + 1;
    die2 = rand() % 6 + 1;
    sum = die1 + die2;
    rollCount++;
}
while (sum != num);
```

现在我们可以编写函数 rollDice，它接受要掷出的数字的目标总和作为参数，并返回为了掷出目标总和而掷骰子的次数。

```c
int rollDice(int num)
{
    int die1;
    int die2;
    int sum;
    int rollCount = 0;

    srand(time(0));

    do
    {
        die1 = rand() % 6 + 1;
        die2 = rand() % 6 + 1;
        sum = die1 + die2;
        rollCount++;
    }
    while (sum != num);

    return rollCount;
}
```

下面的程序展示了如何在程序中使用函数 `rollDice`：

```cpp
//Program: Roll dice

#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int rollDice(int num);

int main()
{
    cout << "The number of times the dice are rolled to "
         << "get the sum 10 = " << rollDice(10) << endl;
    cout << "The number of times the dice are rolled to "
         << "get the sum 6 = " << rollDice(6) << endl;

    return 0;
}

int rollDice(int num)
{
    int die1;
    int die2;
    int sum;
    int rollCount = 0;

    srand(time(0));

    do
    {
        die1 = rand() % 6 + 1;
        die2 = rand() % 6 + 1;
        sum = die1 + die2;
        rollCount++;
    }
    while (sum != num);

    return rollCount;
}
```

### 示例运行：

掷骰子得到总和 10 的次数 = 11  
掷骰子得到总和 6 的次数 = 7

我们把它留作练习，让你修改这个程序，使用户能够输入要掷出的数字的目标总和。（参见本章末尾的编程练习 7。）

### 例 6-5（斐波那契数）

在第 5 章的第一个编程示例中，我们设计并实现了一个算法来求斐波那契数列中的某个数。在本例中，我们通过编写一个函数来计算并返回斐波那契数列中所需的数，从而修改主程序。由于我们已经设计并讨论过如何确定斐波那契数列中的特定数，接下来，我们给出实现该算法的函数定义。

给定第一个数、第二个数以及所需斐波那契数的位置，下面的函数返回该斐波那契数：

```cpp
int nthFibonacciNum(int first, int second, int nthFibNum)
{
    int current;
    int counter;

    if (nthFibNum == 1)
        current = first;
    else if (nthFibNum == 2)
        current = second;
    else
    {
        counter = 3;

        while (counter <= nthFibNum)
        {
            current = second + first;
            first = second;
            second = current;
            counter++;
        } //end while
    } //end else

    return current;
}
```

下面展示了如何在程序中使用这个函数。

```cpp
//Program: Fibonacci number
#include <iostream>
using namespace std;

int nthFibonacciNum(int first, int second, int position);

int main()
{
    int firstFibonacciNum;
    int secondFibonacciNum;
    int nthFibonacci;

    cout << "Enter the first two Fibonacci "
         << "numbers: ";
    cin >> firstFibonacciNum >> secondFibonacciNum;
    cout << endl;

    cout << "The first two Fibonacci numbers are "
         << firstFibonacciNum << " and "
         << secondFibonacciNum
         << endl;

    cout << "Enter the position of the desired "
         << "Fibonacci number: ";
    cin >> nthFibonacci;
    cout << endl;

    cout << "The Fibonacci number at position "
         << nthFibonacci << " is "
         << nthFibonacciNum(firstFibonacciNum, secondFibonacciNum,
                            nthFibonacci)
         << endl;

    return 0;
}

int nthFibonacciNum(int first, int second, int nthFibNum)
{
    int current;
    int counter;

    if (nthFibNum == 1)
        current = first;
    else if (nthFibNum == 2)
        current = second;
    else
    {
        counter = 3;

        while (counter <= nthFibNum)
        {
            current = second + first;
            first = second;
            second = current;
            counter++;
        } //end while
    }//end else

    return current;
}
```

### 示例运行：

在这些示例运行中，用户输入以阴影显示。

### 示例运行 1：

输入前两个斐波那契数：`12 16`

前两个斐波那契数是 12 和 16

输入所需斐波那契数的位置：`10`

位置 10 处的斐波那契数是 796

### 示例运行 2：

输入前两个斐波那契数：`1 1`

前两个斐波那契数是 1 和 1

输入所需斐波那契数的位置：`15`

位置 15 处的斐波那契数是 610

下面是一个返回布尔值的函数示例。

### 例 6-6（回文）

在本例中，设计一个函数 `isPalindrome`，如果字符串是回文则返回 **真**，否则返回 **假**。如果一个字符串正着读和倒着读都一样，那么它就是回文。例如，字符串 "madamimadam"、"5"、"434" 和 "78956987" 都是回文。

假设 `str` 是一个字符串。要判断 `str` 是否为回文，首先比较 `str` 的第一个字符和最后一个字符。如果它们不相同，则 `str` 不是回文，因此函数应返回 **假**。如果 `str` 的第一个字符和最后一个字符相同，则我们比较第二个字符与倒数第二个字符，依此类推。

注意，如果 `length = str.length()` 是 `str` 中的字符数，那么我们需要比较 `str[0]` 与 `str[length - 1]`、`str[1]` 与 `str[length - 2]`，一般地比较 `str[i]` 与 `str[length - 1 - i]`，其中 `0 <= i <= length / 2`。

下面的算法实现了这一讨论：

- 1. `int length = str.length();`
- 2. `for (int i = 0; i < length / 2; i++)`
  - `if (str[i] != str[length - 1 - i])`
    - `return false;`
  - `return true;`

下面的函数实现了该算法：

```cpp
bool isPalindrome(string str)
{
    int length = str.length();                 //Step 1
```
