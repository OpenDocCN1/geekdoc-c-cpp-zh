
该语句声明 `board` 为一个包含四个指针的数组，其中每个指针都是 `int` 类型。因为 `board[0]`、`board[1]`、`board[2]` 和 `board[3]` 都是指针，所以现在可以使用这些指针来创建 `board` 的各行。假设 `board` 的每一行有六列。那么，下面的 `for` 循环创建 `board` 的各行。

```cpp
for (int row = 0; row < 4; row++)
    board[row] = new int[6];
```

注意，表达式 `new int[6]` 创建一个包含六个 `int` 类型元素的数组，并返回该数组的基地址。然后赋值语句将返回的地址存入 `board[row]`。因此，在前面的 `for` 循环执行之后，`board` 是一个四行六列的二维数组。

在前面的 `for` 循环中，如果将数字 6 替换为数字 10，则该循环将创建一个四行十列的二维数组。换句话说，`board` 的列数可以在执行期间指定。然而，按照 `board` 的声明方式，行数是固定的。因此实际上，`board` 并不是真正的动态二维数组。

接下来，考虑以下语句：

```cpp
int **board;
```

该语句声明 `board` 为一个指向指针的指针。换句话说，`board` 和 `*board` 都是指针。现在 `board` 可以存储一个指针或一个 `int` 类型指针数组的地址，而 `*board` 可以存储一个 `int` 内存空间或一个 `int` 值数组的地址。

假设你希望 `board` 是一个 10 行 15 列的数组。为此，首先创建一个包含 10 个 `int` 类型指针的数组，并将该数组的地址赋给 `board`。下面的语句完成此操作：

```cpp
board = new int* [10];  // create an array of 10 int pointers
```

因为 `board` 的元素是 `int` 指针，它们中的每一个都可以指向一个 `int` 值数组。

接下来，我们创建 `board` 的列。下面的 `for` 循环完成此操作：

```cpp
for (int row = 0; row < 10; row++)
    board[row] = new int[15];
```

要访问 `board` 的元素，可以使用第 8 章讨论的数组下标表示法。

注意，`board` 的行数和列数可以在程序执行期间指定。下面的程序进一步说明如何创建二维数组。

![](img/b217c421655b51e7494cf3b89bb5432d_892_0.png)

### 示例 12-7

```cpp
#include <iostream>                                      //Line 1
#include <iomanip>                                       //Line 2

using namespace std;                                     //Line 3

void fill(int **p, int rowsSize, int columnSize);       //Line 4
void print(int **p, int rowsSize, int columnSize);       //Line 5

int main()                                               //Line 6
{
    int **board;                                         //Line 8

    int rows;                                            //Line 9
    int columns;                                         //Line 10

    cout << "Line 11: Enter the number of rows "
         << "and columns: ";                            //Line 11
    cin >> rows >> columns;                              //Line 12
    cout << endl;                                        //Line 13

            //Create the rows of board
    board = new int* [rows];                              //Line 14

            //Create the columns of board
    for (int row = 0; row < rows; row++)                 //Line 15
        board[row] = new int[columns];                   //Line 16

            //Insert elements into board
    fill(board, rows, columns);                          //Line 17

    cout << "Line 18: Board:" << endl;                   //Line 18

            //Output the elements of board
    print(board, rows, columns);                         //Line 19

    return 0;                                             //Line 20
}                                                        //Line 21

void fill(int **p, int rowsSize, int columnSize)
{
    for (int row = 0; row < rowsSize; row++)
    {
        cout << "Enter " << columnSize << " number(s)"
             << " for row number " << row << ": ";
        for (int col = 0; col < columnSize; col++)
            cin >> p[row][col];
        cout << endl;
    }
}

void print(int **p, int rowSize, int columnSize)
{
    for (int row = 0; row < rowSize; row++)
    {
        for (int col = 0; col < columnSize; col++)
            cout << setw(5) << p[row][col];
        cout << endl;
    }
}
```

**样例运行：** 在本次样例运行中，用户输入以底纹显示。

```text
Line 11: Enter the number of rows and columns: 3 4

Enter 4 number(s) for row number 0: 1 2 3 4

Enter 4 number(s) for row number 1: 5 6 7 8

Enter 4 number(s) for row number 2: 9 10 11 12

Line 18: Board:
    1    2    3    4
    5    6    7    8
    9   10   11   12
```

前面的程序包含函数 `fill` 和 `print`。函数 `fill` 提示用户输入一个 `int` 类型二维数组的元素。函数 `print` 输出一个 `int` 类型二维数组的元素。

前面的输出大部分应该很清楚。让我们看看函数 `main` 中的语句。第 8 行的语句声明 `board` 为一个 `int` 类型指针的指针。第 9 行和第 10 行的语句声明 `int` 变量 `rows` 和 `columns`。第 11 行的语句提示用户输入行数和列数。第 12 行的语句将行数存入变量 `rows`，将列数存入变量 `columns`。第 14 行的语句创建 `board` 的行，第 15 行和第 16 行的 `for` 循环创建 `board` 的列。第 17 行的语句使用函数 `fill` 填充数组 `board`，第 19 行的语句使用函数 `print` 输出 `board` 的元素。

## 浅拷贝与深拷贝及指针

在前面的小节中，我们讨论了指针算术，并解释说，如果不小心，一个指针可能会访问另一个（完全无关的）指针的数据。这种情况可能导致未预料或错误的结果。这里，我们讨论指针的另一个特殊之处。为便于讨论，我们将用示意图展示指针及其相关内存。

考虑以下语句：

```cpp
int *first;
int *second;

first = new int[10];
```

前两条语句声明 `first` 和 `second` 两个 `int` 类型指针变量。第三条语句创建一个包含 10 个元素的数组，并将该数组的基地址存入 `first`（见图 12-8）。（注意，`first` 连同箭头表示 `first` 指向已分配的内存。）

![](img/b217c421655b51e7494cf3b89bb5432d_895_0.png)

**图 12-8** 指针 `first` 及其指向的数组

假设 `first` 指向的数组中存储了一些有意义的数据。具体来说，假设该数组如图 12-9 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_895_1.png)

**图 12-9** 指针 `first` 及其数组

接下来，考虑以下语句：

```cpp
second = first;        //Line A
```

该语句将 `first` 持有的内存地址复制到 `second`。该语句执行后，`first` 和 `second` 都指向同一个数组，如图 12-10 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_895_2.png)

**图 12-10** 执行语句 `second = first;` 后的 `first` 和 `second`

接下来执行以下语句：

```cpp
delete [] second;
```

该语句执行后，`second` 指向的数组被删除。此操作导致图 12-11 所示的结果。

![](img/b217c421655b51e7494cf3b89bb5432d_895_3.png)

**图 12-11** 执行语句 `delete [] second;` 后的 `first` 和 `second`

因为 **first** 和 **second** 指向同一个数组，在语句

```cpp
delete [] second;
```

执行后，**first** 变为无效；也就是说，**first**（以及 **second**）现在是悬空指针。因此，如果程序之后试图访问 **first** 指向的内存，程序要么访问错误的内存，要么以错误终止。这种情况是浅拷贝的一个例子。更正式地说，在**浅拷贝**中，两个或多个同类型指针指向同一内存；也就是说，它们指向相同的数据。

另一方面，假设不是前面的语句 **second = first;**（在行 A 中），而是有以下语句：

```cpp
second = new int[10];

for (int j = 0; j < 10; j++)
    second[j] = first[j];
```

第一条语句创建一个包含 10 个 **int** 类型元素的数组，并将该数组的基地址存入 **second**。第二条语句将 **first** 指向的数组复制到 **second** 指向的数组中（见图 12-12）。

![](img/b217c421655b51e7494cf3b89bb5432d_896_0.png)

**图 12-12** *first* 和 *second* 都指向各自的数据

**first** 和 **second** 现在都指向各自的数据。如果 **second** 删除其内存，对 **first** 没有影响。这种情况是深拷贝的一个例子。更正式地说，在**深拷贝**中，两个或多个同类型指针各自指向自己的数据副本。

从上述讨论可知，必须知道何时使用浅拷贝、何时使用深拷贝。

## 类与指针：一些特殊之处

在前面的小节中，我们讨论了如果指针变量是类类型，如何使用箭头表示法通过指针访问类成员。因为类可以有指针成员变量，本节讨论此类类的一些特殊之处。为便于讨论，我们将使用以下类：

```cpp
class ptrMemberVarType
{
```
