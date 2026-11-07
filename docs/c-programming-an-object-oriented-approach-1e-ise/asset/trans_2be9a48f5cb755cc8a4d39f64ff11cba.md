

![](img/d68f6199646ca63591a6d8419e0ed4ba_202_0.png)

**图 5.13** *do-while* 循环分析

## 5.5 关于循环的更多内容

在本节中，我们首先比较三种循环结构：*while* 循环、*for* 循环和 *do-while* 循环。然后我们会了解如何组合它们来创建嵌套循环，这有助于解决问题。

### 5.5.1 三种循环的比较

前面几节讨论的三种循环语句有一些共同特征，也有一些不同特征。表 5.3 展示了 *n* 次迭代的比较总结。

- *while* 循环和 *for* 循环是前测试循环。*do-while* 循环是后测试循环。
- *while* 循环和 *do-while* 循环主要设计为事件控制循环；*for* 循环主要设计为计数器控制循环。
- *while* 循环和 *for* 循环可以迭代零次；*do-while* 循环至少迭代一次。
- 如果我们希望循环进行 *n* 次迭代，那么 *while* 循环和 *for* 循环中需要 *n + 1* 次测试，而 *do-while* 循环中只需要 *n* 次测试。

### 5.5.2 嵌套循环

我们可以有**嵌套循环**，即一个循环位于另一个循环内部。内层循环不必与外层循环类型相同。

**表 5.3** *while*、*for* 和 *do-while* 循环的比较

| 特性 | while 循环 | for 循环 | do-while 循环 |
|---|---|---|---|
| 测试类型 | 前测试 | 前测试 | 后测试 |
| 主要设计 | 事件控制 | 计数器控制 | 事件控制 |
| 最少迭代次数 | 0 | 0 | 1 |
| 测试次数 | *n + 1* | *n + 1* | *n* |

**例 5.18**

我们可以使用嵌套的 *for* 循环来水平和垂直打印一组星号；也就是说，打印一个星号矩形。外层循环控制行；内层循环控制列。对于外层循环的每次迭代，内层循环会针对每一列重复一次。要打印一个四行、每行八个星号（列）的矩形，外层循环使用 4 次迭代；内层循环使用 32（4 × 8）次迭代。程序 5.14 展示了代码和两个示例运行。

**程序 5.14** *一个 for 语句位于另一个 for 语句内部*

```cpp
/********************************************************
 * Use a for loop inside another loop to print a pattern of      *
 * asterisks horizontally and vertically                         *
 ********************************************************/
#include <iostream>
using namespace std;

int main ( )
{
    // Declaration
    int rows;    // Number of rows
    int cols;    // Number of columns
    // Inputs
    cout << "Enter the number of rows: ";
    cin >> rows;
    cout << "Enter the number of columns: ";
    cin >> cols;
    // Output
    for (int count1 = 1; count1 <= rows; count1++)
    {
        for (int count2 = 1; count2 <= cols; count2++)
        {
            cout << "*";
        }
        cout << endl;
    }
    return 0;
}
```

```text
Run:
Enter the number of rows: 3
Enter the number of columns: 8
********
********
********
```

```text
Run:
Enter the number of rows: 2
Enter the number of columns: 6
******
******
```

**例 5.19**

让我们看另一个例子。这一次，外层循环计数器的值控制内层循环计数器的起始值（程序 5.15）。

**程序 5.15** 打印数字图案

```cpp
/*******************************************************
 * Use a for loop inside another loop to print a pattern of
 * digits horizontally and vertically
 *******************************************************/
#include <iostream>
using namespace std;

int main()
{
    // Declaration
    int rows;    // Number of rows
    int cols;    // Number of columns
    // Inputs
    cout << "Enter the number of rows: ";
    cin >> rows;
    cout << "Enter the number of columns: ";
    cin >> cols;
    // Nested loops
    for (int i = 1; i <= rows; i++)
    {
        for (int j = i; j <= i + cols - 1; j++)
        {
            cout << j << " ";
        } // End inner loop
        cout << endl;
    }
    return 0;
}
```

```text
Run:
Enter the number of rows: 3
Enter the number of columns: 6
1 2 3 4 5 6
2 3 4 5 6 7
3 4 5 6 7 8
```

```text
Run:
Enter the number of rows: 2
Enter the number of columns: 8
1 2 3 4 5 6 7 8
2 3 4 5 6 7 8 9
```

**例 5.20**

程序 5.16 展示了如何创建大小为 2 到 10 的乘法表。大小由用户输入。注意第 *i* 行和第 *j* 列的值实际上是 (*i* * *j*) 的值。

**程序 5.16** 创建乘法表

```cpp
/****************************************************************
 * Use a for loop inside another loop to print a multiplication
 * table of size 2 to 10.
 ****************************************************************/
#include <iostream>
#include <iomanip>
using namespace std;

int main ()
{
    // Declaration of size
    int size;
    // Input and validation
    do
    {
        cout << "Enter table size (2 to 10): ";
        cin >> size;
    } while (size < 2 || size > 10);
    // Printing the table (nested loops)
    for (int i = 1; i <= size; i++)
    {
        for (int j = 1; j <= size; j++)
        {
            cout << setw (4) << i * j;
        }
        cout << endl;
    }
    return 0;
}
```

```text
Run:
Enter table size (2 to 10): 4
   1   2   3   4
   2   4   6   8
   3   6   9  12
   4   8  12  16
```

```text
Run:
Enter table size (2 to 10): 11
Enter table size (2 to 10): 9
1 2 3 4 5 6 7 8 9
2 4 6 8 10 12 14 16 18
3 6 9 12 15 18 21 24 27
4 8 12 16 20 24 28 32 36
5 10 15 20 25 30 35 40 45
6 12 18 24 30 36 42 48 54
7 14 21 28 35 42 49 56 63
8 16 24 32 40 48 56 64 72
9 18 27 36 45 54 63 72 81
```

## 5.6 其他相关语句

除了三种重复语句之外，C++ 还定义了另一组通常与重复语句一起使用的语句：*return*、*break*、*continue* 和 *goto*。图 5.14 展示了这些语句的分类。

### 5.6.1 *return* 语句

**return 语句**立即终止当前函数，并将控制权返回给函数调用者。在循环中使用 *return 语句*会导致循环终止，同时也会终止循环正在其中迭代的函数（例如 *main*）。

**例 5.21**

在数学中，我们可以将正整数分为三类：1、*素数*和*合数*。素数只能被它自身和 1 整除。合数不是素数。素数在计算机科学和安全中起着非常重要的作用。要判断一个数是否为素数，我们可以使用以下步骤（尽管还有更高效但更复杂的方法）。

- a. 如果该数是 1，我们知道该数不是素数。
- b. 如果该数能被任何小于它自身的数整除，那么它不是素数；它是合数。

注意，我们不必测试从 2 到该数本身的所有数；一旦找到任何能整除该数的、大于等于 2 的整数，我们就可以宣布该数不是素数并终止循环。程序 5.17 展示了一种解决方案。

注意，我们在第 23 行插入了一个 *return 语句*，在第 32 行插入了一个 *return 语句*，并在第 37 行插入了一个 *return 语句*。这三个语句都可以终止程序。

![](img/d68f6199646ca63591a6d8419e0ed4ba_206_0.png)

**图 5.14** 与重复相关的语句

**程序 5.17** 判断一个数是否为素数

```cpp
/*******************************************************
 * Use a return statement to find if a number is a prime or not. *
 * The program returns from the main function as soon as it finds *
 * that a number is 1 or composite.                              *
 *******************************************************/
#include <iostream>
using namespace std;

int main ()
{
    // Declaration
    int num;
    // Input validation loop
    do
    {
        cout << "Enter a positive integer: ";
        cin >> num;
    } while (num <= 0);
    // Testing if the input is 1
    if (num == 1)
    {
        cout << "1 is not a composite nor a prime.";
        return 0;
    }
    // Testing for composite
    for (int i = 2; i < num ; i++)
    {
        if (num % i == 0)
        {
            cout << num << " is composite." << endl;
            cout << "The first divisor is " << i << endl;
            return 0;
        }
    }
    // Output Result
    cout << num << " is a prime." << endl;
    return 0;
}
```

```text
Run:
Enter a positive integer: 1
1 is not a composite nor a prime.
```

```text
Run:
Enter a positive integer: 12
12 is composite.
The first divisor is 2
```

