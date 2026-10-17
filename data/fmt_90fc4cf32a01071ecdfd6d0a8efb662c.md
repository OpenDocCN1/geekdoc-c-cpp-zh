
## 编程项目

编程项目比练习程序需要更多的问题解决，通常可以通过多种方法解决。访问 `myprogramminglab.com` 在线完成许多项目并获得即时反馈。

- 1. 使用动态数组完成第 7 个编程项目。在该问题中，使用动态数组存储每个大整数的数字![](img/ca450b03f7ea64419b139be8fdd92a4a_570_0.png)。允许任意数量的数字，而不是将位数限制为20位。
- 2. 完成第3 个编程项目。在该问题中，返回一个删除了所有重复字母的新动态数组，而不是修改部分填充的数组。当数据不再需要时，忘记释放这些返回动态数组的内存。
- 3. 编写一个函数合并两个动态整数数组的内容。你的函数应该包含数组引用指针和两个数组大小的参数。你的函数应返回一个包含两个元素拷贝的新数组指针。使用驱动程序测试你的函数。
- 4. C 字符串存储为字符数组并用特殊字符 `'\0'` 指定字符串结束。普通字符数组能够在结尾没有特殊字符的情况下工作。编写函数 `cString`，它接受字符数组的 `const` 指针和一个数组大小整数。检查特殊字符 `'\0'` 是否存在。如果存在，返回 `true`；否则返回 `false`。编写一个驱动程序，通过传递 C 字符串、普通字符数组和动态数组来测试你的函数。
- 5. 你运行四个计算机实验室。每个实验室包含下表所示编号的计算机站：

| 实验室编号 | 计算机站 |
| :--- | :--- |
| 1 | 1-5 |
| 2 | 1-6 |
| 3 | 1-4 |
| 4 | 1-3 |

每个用户有一个唯一的五位 ID 号。每当用户登录时，用户的 ID、实验室编号和计算机站编号传输到你的系统。例如，如果 49193 登录到实验室 3 的 2 号站，你的系统接收输入数据 `(49193, 2)`。同样，当用户注销站点时，你的系统接收实验室编号和计算机站编号。

编写一个计算机程序，按实验室跟踪哪个用户登录了哪个计算机。例如，如果用户 49193 登录到实验室 3 的 2 号站，而 99577 登录到实验室 4 的 1 号站，那么你的系统可能会显示如下：

实验室编号 计算机站
1: 1: empty 2: empty 4: empty 5: empty
2: 1: empty 2: empty 4: empty 5: empty 6: empty
3: 1: empty 2: 49193 3: empty 4: empty
4: 1: 99577 2: empty 3: empty

## 第 9 章 / 指针与动态数组

创建一个菜单，允许管理员通过手动输入登录或注销数据来模拟信息的传输。每有人登录或注销时，显示内容都应该更新。此外，编写一个搜索选项，让管理员输入用户 ID，系统将输出该用户登录的实验室和工作站编号；如果用户 ID 未登录到任何计算机系统，则输出“None”。

你应该使用一个长度为 4 的固定数组来表示实验室。数组的每个条目指向一个动态数组，该数组存储每个相应计算机工作站的用户登录信息。

结构如图所示。这种结构有时被称为“锯齿数组”（ragged array），因为列的长度是不相等的。

实验室数组 工作站的动态数组

| | | | | | | |
|---|---|---|---|---|---|
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |

- 动态数组的一个问题是数组是使用 `new` 运算符创建的，大小无法更改。例如，你可能像使用 `vector` 那样向数组中添加或删除条目。本项目要求你创建函数，使用动态数组来模拟 `vector` 的行为。

首先，编写一个程序创建一个包含五个字符串的动态数组。在动态数组中存入五个任意名称。接下来，完成以下函数：

```cpp
string addEntry(string *dynamicArray, int &size, string newEntry);
```

该函数应该创建一个比 `dynamicArray` 更大的动态数组元素，将 `dynamicArray` 中的所有元素复制到新数组中，在新数组末尾添加新条目，递增 `size`，删除 `dynamicArray`，并返回新的动态数组。

```cpp
string deleteEntry(string *dynamicArray, int &size, string entryToDelete);
```

该函数应该在 `dynamicArray` 中搜索 `entryToDelete`。如果未找到，则忽略该请求并返回未修改的 `dynamicArray`。如果找到，则创建一个比 `dynamicArray` 小一个元素的动态数组。将除 `entryToDelete` 之外的所有元素复制到新数组，删除 `dynamicArray`，递减 `size`，并返回新的动态数组。

通过向数组中添加和删除名称来测试你的函数，同时输出数组的内容。你必须将 `addEntry` 或 `deleteEntry` 返回的数组赋值回主函数中的动态数组。

- 7. 如果 C++ 没有内置的二维数组机制怎么办？是否可以通过在一个一维数组周围编写封装函数来模拟它们？基本思想如下所示。考虑以下二维数组：

```cpp
int matrix[2][3];
```

它可以被视化为一个表格：

| matrix[0][0] | matrix[0][1] | matrix[0][2] |
| matrix[1][0] | matrix[1][1] | matrix[1][2] |

二维数组可以映射并存储在一个维数组中，其中每行存储在连续的内存位置上（你的编译器实际上执行了类似的操作将二维数组映射到内存）。

```cpp
int matrix1D[6];
```

| matrix1D[0] | matrix1D[1] | matrix1D[2] | matrix1D[3] | matrix1D[4] | matrix1D[5] |

在这里，映射关系如下：

```
matrix[0][0] 将存储在 matrix1D[0]
matrix[0][1] 将存储在 matrix1D[1]
matrix[0][2] 将存储在 matrix1D[2]
matrix[1][0] 将存储在 matrix1D[3]
matrix[1][1] 将存储在 matrix1D[4]
matrix[1][2] 将存储在 matrix1D[5]
```

基于此想法，完成以下函数的定义：

```cpp
int* create2DArray(int rows, int columns);
```

这创建了一个一维动态数组来模拟二维数组，并返回该一维动态数组的指针。

`rows` 是二维数组中所需的行数。
`columns` 是二维数组中所需的列数。
返回值：指向一维动态数组的指针，其大小足够容纳 `rows x columns` 的二维数组。

注意，`int ptr = create2DArray(2,3);` 将创建一个类似于 `int ptr[2][3];` 创建的数组。

```cpp
void set(int *arr, int rows, int columns,
        int desired_row, int desired_column, int val);
```

这会将 `val` 存储在模拟的二维数组中 `desired_row`, `desired_column` 的位置。如果所需的索引无效，函数应打印错误信息并退出。

`arr` 是用于模拟二维数组的一维数组。
`rows` 是二维数组的总行数。
`columns` 是二维数组的总列数。
`desired_row` 是调用者想要访问的行索引（从0开始）。
`desired_column` 是调用者想要访问的列索引（从0开始）。
`val` 是存储在 `desired_row` 和 `desired_column` 处的值。

```cpp
int get(int *arr, int rows, int columns,
        int desired_row, int desired_column);
```

这返回模拟的二维数组中 `desired_row`, `desired_column` 位置的值。

## 编程项目

## 10.1 结构体

与其关联的数据项：账户余额、账户利率以及期限（即距离到期为止的月数）。前两项可以表示为 `double` 类型的值，而月数可以表示为 `int` 类型的值。显示 10.1 展示了用于此类账户的 `CDAccount` 结构体的定义。该定义嵌入在一个完整的程序中，该程序演示了这种结构体类型。从示例对话中可以看出，这家银行专门经营短期定期存款（CD），因此期限始终为 12 个月或更短。让我们来看看这个示例是如何定义和使用的。

结构体的定义如下：

```cpp
struct CDAccount
{
    double balance;
    double interestRate;
    int term; // 直到到期的月数
};
```

`struct` 关键字声明这是一个结构体类型定义。标识符 `CDAccount` 是该结构体类型的名称。结构体标签可以是任何合法的标识符（不是关键字）。虽然 C++ 语言并不要求这种约定，但结构体标签通常使用大小写字母混合写法，并以大写字母开头。在大花括号 `{}` 内部声明的标识符被称为成员名称。如示例所示，结构体类型定义以大括号和分号结束。

结构体定义通常放置在任何函数之外（方式与全局常量声明放置在所有函数定义之外相同）。该结构体类型对于结构体定义之后的所有代码都是可用的。

一旦给出了结构体类型，就可以像使用 `int`、`char` 等预定义类型一样使用该类型。例如，以下代码将声明两个名为 `myAccount` 和 `yourAccount` 的变量，它们的类型均为 `CDAccount`：

```cpp
CDAccount myAccount, yourAccount;
```

结构体变量可以像任何其他变量一样存储值。结构体值是一组被称为成员值的较小值的集合。对于结构体定义中声明的每个成员名称，都有对应的一个成员值。例如，`CDAccount` 类型的值是三个成员值的集合：两个 `double` 类型的值和一个 `int` 类型的值。构成结构体值的成员值存储在成员变量中，我们将在接下来讨论这些。

每个结构体类型都指定了一个成员名称列表。在显示 10.1 中，`CDAccount` 结构体有三个成员名称 `balance`、`interestRate` 和 `term`。

![](img/ca450b03f7ea64419b139be8fdd92a4a_579_0.png)

## 第 10 章 / 定义类

### 显示 10.1 结构体定义（2 部分中的第 1 部分）

```cpp
// 演示 CDAccount 结构体类型的程序。
#include <iostream>
using namespace std;
// 银行定期存款结构体：
struct CDAccount
{
    double balance;
    double interestRate;
    int term; // 直到到期的月数
};
void getData(CDAccount &theAccount)
// 后置条件：theAccount.balance 和 theAccount.interestRate
// 已获得用户从键盘输入的值。
int main()
{
    CDAccount account;
    getData(account);
    double rateFraction, interest;
    rateFraction = account.interestRate / 100.0;
    interest = account.balance * rateFraction * (account.term / 12.0);
    account.balance = account.balance + interest;
    cout(ios::fixed);
    cout(ios::showpoint);
    cout.precision(2);
    cout << "When your CD matures in "
         << account.term << " months.\n";
    cout << "it will have a balance of $$";
         << account.balance << endl;
    return 0;
}
// 使用 iostream：
void getData(CDAccount &theAccount)
{
    cout << "Enter account balance: $$";
    cin >> theAccount.balance;
    cout << "Enter account interest rate: $$";
    cin >> theAccount.interestRate;
    cout << "Enter the number of months until maturity\n"
    << " (must be 12 or fewer months): $$";
    cin >> theAccount.term;
}
```

### 显示 10.1 结构体定义（2 部分中的第 2 部分）

示例对话

```
Enter account balance: $100.00
Enter account interest rate: 10.0
Enter the number of months until maturity
(must be 12 or fewer months): 6
When your CD matures in 6 months,
it will have a balance of $105.00
```

和 `term`。这些成员名称中的每一个都可以用于提取出一个作为较大结构体变量部分的较小变量。这些较小的变量被称为成员变量。成员变量是通过给出结构体变量的名称，后跟一个点（即句号），然后是成员名称来指定的。例如，如果 `account` 是类型 `CDAccount` 的结构体变量（如在显示 10.1 中声明），那么结构体变量 `account` 具有以下三个变量：

- `account.balance`
- `account.interestRate`
- `account.term`

前两个成员变量是 `double` 类型，最后一个是 `int` 类型。这些成员变量可以像其他任何类型的变量一样使用。例如，可以通过以下赋值语句给上述成员变量赋值：

```cpp
account.balance = 1000.0;
account.interestRate = 5.5;
account.term = 12;
```

### 显示 10.2 成员值

```cpp
struct CDAccount
{
    double balance;
    double interestRate;
    int term; // 直到到期的月数
};
int main()
{
    CDAccount account;
    account.balance = 1000.0;
```
