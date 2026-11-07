
该语句将 `board` 声明为一个包含四个指针的数组，其中每个指针都是 `int` 类型。由于 `board[0]`、`board[1]`、`board[2]` 和 `board[3]` 都是指针，现在可以使用这些指针来创建 `board` 的各行。假设 `board` 的每一行有六列。那么，下面的 `for` 循环会创建 `board` 的各行。

```cpp
for (int row = 0; row < 4; row++)
    board[row] = new int[6];
```

注意，表达式 `new int[6]` 创建一个包含六个 `int` 类型分量的数组，并返回该数组的基地址。然后，赋值语句将返回的地址存入 `board[row]`。由此可知，在执行前面的 `for` 循环之后，`board` 就是一个四行六列的二维数组。

在前面的 `for` 循环中，如果将数字 6 替换为数字 10，那么该循环将创建一个四行十列的二维数组。换句话说，`board` 的列数可以在执行期间指定。然而，按照 `board` 的声明方式，行数是固定的。因此，实际上 `board` 并不是真正的动态二维数组。

接下来，考虑下面的语句：

```cpp
int **board;
```

该语句将 `board` 声明为一个指向指针的指针。换句话说，`board` 和 `*board` 都是指针。现在，`board` 可以存储一个指针的地址，或一个 `int` 类型指针数组的地址；而 `*board` 可以存储一个 `int` 内存空间的地址，或一个 `int` 值数组的地址。

假设希望 `board` 是一个 10 行 15 列的数组。为此，首先创建一个包含 10 个 `int` 类型指针的数组，并将该数组的地址赋给 `board`。下面的语句完成这一操作：

```cpp
board = new int* [10]; //create an array of 10 int pointers
```

由于 `board` 的元素是 `int` 指针，因此其中每个元素都可以指向一个 `int` 值数组。

接下来，我们创建 `board` 的各列。下面的 `for` 循环完成这一操作：

```cpp
for (int row = 0; row < 10; row++)
    board[row] = new int[15];
```

要访问 `board` 的分量，可以使用第 8 章中讨论的数组下标表示法。

注意，`board` 的行数和列数都可以在程序执行期间指定。下面的程序进一步说明如何创建二维数组。

```cpp
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

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Line 4: Enter the number of rows and columns: 3 4
Enter 4 number(s) for row number 0: 1 2 3 4
Enter 4 number(s) for row number 1: 5 6 7 8
Enter 4 number(s) for row number 2: 9 10 11 12
Line 11: Board:
    1    2    3    4
    5    6    7    8
    9   10   11   12
```

前面的程序包含 `fill` 和 `print` 函数。`fill` 函数提示用户输入 `int` 类型二维数组的元素。`print` 函数输出 `int` 类型二维数组的元素。

前面输出的大部分内容应该都很清楚。让我们看看 `main` 函数中的语句。第 1 行的语句将 `board` 声明为一个指向 `int` 类型指针的指针。第 2 行和第 3 行的语句声明 `int` 变量 `rows` 和 `columns`。第 4 行的语句提示用户输入行数和列数。第 5 行的语句将行数存入变量 `rows`，将列数存入变量 `columns`。第 7 行的语句创建 `board` 的各行，第 8 行和第 9 行的 `for` 循环创建 `board` 的各列。第 10 行的语句使用 `fill` 函数填充数组 `board`，第 12 行的语句使用 `print` 函数输出 `board` 的元素。

## 浅拷贝与深拷贝以及指针

在前面的小节中，我们讨论了指针算术，并说明如果不小心，一个指针可能会访问另一个（完全无关的）指针的数据。这种情况可能导致意想不到或错误的结果。这里，我们讨论指针的另一个特殊之处。为便于讨论，我们将使用图示来展示指针及其相关的内存。

考虑下面的语句：

```cpp
int *first;
int *second;

first = new int[10];
```

前两条语句声明 `first` 和 `second` 两个 `int` 类型指针变量。第三条语句创建一个包含 10 个分量的数组，并将该数组的基地址存入 `first`（见图 12-8）。（注意，`first` 连同箭头表示 `first` 指向已分配的内存。）

![](img/d0be7fc6d804b63484835c6c8bc67a07_890_0.png)

**图 12-8** 指针 `first` 及其指向的数组

假设 `first` 所指向的数组中存储了一些有意义的数据。具体来说，假设该数组如图 12-9 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_890_1.png)

**图 12-9** 指针 `first` 及其数组

接下来，考虑下面的语句：

```cpp
second = first;    //Line A
```

该语句将 `first` 所持有的内存地址复制到 `second`。执行该语句后，`first` 和 `second` 都指向同一个数组，如图 12-10 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_890_2.png)

**图 12-10** 执行语句 `second = first;` 之后的 `first` 和 `second`

接下来执行下面的语句：

```cpp
delete [] second;
```

执行该语句后，`second` 所指向的数组被删除。此操作的结果如图 12-11 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_890_3.png)

**图 12-11** 执行语句 `delete [] second;` 之后的 `first` 和 `second`

由于 `first` 和 `second` 指向同一个数组，在执行语句：

```cpp
delete [] second;
```

之后，`first` 变为无效，也就是说，`first`（以及 `second`）现在是悬空指针。因此，如果程序之后试图访问 `first` 所指向的内存，程序要么会访问错误的内存，要么会因错误而终止。这种情况是浅拷贝的一个例子。更正式地说，在**浅拷贝**中，两个或多个同类型的指针指向同一块内存；也就是说，它们指向同一份数据。

另一方面，假设我们没有使用前面的语句 `second = first;`（位于第 A 行），而是使用下面的语句：

```cpp
second = new int[10];

for (int j = 0; j < 10; j++)
    second[j] = first[j];
```

第一条语句创建一个包含 10 个 `int` 类型分量的数组，并将该数组的基地址存入 `second`。第二条语句将 `first` 所指向的数组复制到 `second` 所指向的数组（见图 12-12）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_891_0.png)

**图 12-12** *first 和 second 都指向各自的数据*

现在 `first` 和 `second` 都指向各自的数据。如果 `second` 删除其内存，不会影响 `first`。这种情况是深拷贝的一个例子。更正式地说，在**深拷贝**中，两个或多个同类型的指针指向各自的数据副本。

从前面的讨论可知，必须知道何时使用浅拷贝、何时使用深拷贝。

## 类与指针：一些特殊之处

在前一节中，我们讨论了当指针变量是类类型时，如何使用箭头表示法通过指针访问类成员。由于类可以拥有指针成员变量，本节讨论此类类的一些特殊之处。为便于讨论，我们将使用下面的类：

```cpp
class ptrMemberVarType
{
public:
    .
    .
    .
private:
    int x;
    int lenP;
    int *p;
};
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_891_1.png)

另外，考虑下面的语句（见图 12-13）：

```cpp
ptrMemberVarType objectOne;
ptrMemberVarType objectTwo;
```

![](img/d0be7fc6d804b63484835c6c8bc67a07_892_0.png)

**图 12-13** 对象 *objectOne* 和 *objectTwo*

### 析构函数

对象 *objectOne* 有一个指针成员变量 `p`。假设在程序执行期间，指针 `p` 创建了一个动态数组。当 `objectOne` 离开作用域时，`objectOne` 的所有成员变量都会被销毁。然而，`p` 创建了一个动态数组，而动态内存必须使用运算符 `delete` 释放。因此，如果指针 `p` 不使用 `delete` 运算符释放该动态数组，那么该动态数组的内存空间将仍然被标记为已分配，即使无法访问它。我们如何确保当 `p` 被销毁时，由 `p` 创建的动态内存也被销毁？假设 `objectOne` 如图 12-14 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_892_1.png)

**图 12-14** 对象 *objectOne* 及其数据

