
函数 `funcExp` 有七个参数。参数 `w`、`x`、`y` 和 `z` 是默认参数。如果在调用函数 `funcExp` 时没有为 `w`、`x`、`y` 和 `z` 指定值，则使用它们的默认值。

假设有如下语句：

```cpp
int a, b;
char ch;
double d;
```

以下函数调用是合法的：

- 1. `funcExp(a, b, d);`
- 2. `funcExp(a, 15, 34.6, 'B', 87, ch);`
- 3. `funcExp(b, a, 14.56, 'D');`

在语句 1 中，使用了 `w`、`x`、`y` 和 `z` 的默认值。在语句 2 中，`w` 的默认值被替换为 `'B'`，`x` 的默认值被替换为 `87`，`y` 的默认值被替换为 `ch` 的值，并且使用 `z` 的默认值。在语句 3 中，`w` 的默认值被替换为 `'D'`，并且使用 `x`、`y` 和 `z` 的默认值。

以下函数调用是非法的：

- 1. `funcExp(a, 15, 34.6, 46.7);`
- 2. `funcExp(b, 25, 48.76, 'D', 4567, 78.34);`

在语句 1 中，因为省略了 `w` 的值，所以所有其他默认值也必须省略。在语句 2 中，因为省略了 `y` 的值，所以 `z` 的值也应省略。

以下带默认参数的函数原型是非法的：

- 1. `void funcOne(int x, double z = 23.45, char ch, int u = 45);`
- 2. `int funcTwo(int length = 1, int width, int height = 1);`
- 3. `void funcThree(int x, int& y = 16, double z = 34);`

在语句 1 中，因为第二个参数 `z` 是默认参数，所以 `z` 之后的所有其他参数也必须是默认参数。在语句 2 中，因为第一个参数是默认参数，所以所有参数都必须是默认参数。在语句 3 中，不能将常量值赋给 `y`，因为 `y` 是引用参数。

示例 6-19 进一步说明了带默认参数的函数。

## 示例 6-19

```cpp
#include <iostream>  //Line 1
#include <iomanip>   //Line 2

using namespace std;  //Line 3

int volume(int l = 1, int w = 1, int h = 1);        //Line 4
void funcOne(int& x, double y = 12.34, char z = 'B'); //Line 5
```

```cpp
int main()
{
    int a = 23;                                      //Line 7
    double b = 48.78;                                //Line 8
    char ch = 'M';                                   //Line 9
                                                     //Line 10
    cout << fixed << showpoint << setprecision(2);   //Line 11

    cout << "Line 12: a = " << a << ", b = "
         << b << ", ch = " << ch << endl;           //Line 12
    cout << "Line 13: Volume = " << volume()
         << endl;                                    //Line 13
    cout << "Line 14: Volume = " << volume(5, 4)
         << endl;                                    //Line 14
    cout << "Line 15: Volume = " << volume(34)
         << endl;                                    //Line 15
    cout << "Line 16: Volume = "
         << volume(6, 4, 5) << endl;                 //Line 16
    funcOne(a);                                      //Line 17
    funcOne(a, 42.68);                               //Line 18
    funcOne(a, 34.65, 'Q');                          //Line 19
    cout << "Line 20: a = " << a << ", b = "
         << b << ", ch = " << ch << endl;           //Line 20

    return 0;                                        //Line 21
}                                                    //Line 22
```

```cpp
int volume(int l, int w, int h)                      //Line 23
{                                                    //Line 24
    return l * w * h;                                //Line 25
}                                                    //Line 26
```

```cpp
void funcOne(int& x, double y, char z)               //Line 27
{                                                    //Line 28
    x = 2 * x;                                       //Line 29
    cout << "Line 30: x = " << x << ", y = "
         << y << ", z = " << z << endl;             //Line 30
}                                                    //Line 31
```

示例运行：

```text
Line 12: a = 23, b = 48.78, ch = M
Line 13: Volume = 1
Line 14: Volume = 20
Line 15: Volume = 34
Line 16: Volume = 120
Line 30: x = 46, y = 12.34, z = B
Line 30: x = 92, y = 42.68, z = B
Line 30: x = 184, y = 34.65, z = Q
Line 20: a = 184, b = 48.78, ch = M
```

**注意**  在本书的程序中，并且按照推荐做法，函数 `main` 的定义放在任何用户定义函数的定义之前。因此，必须在函数原型中指定参数的默认值，并且只能在函数原型中指定，而不能在函数定义中指定，因为这必须发生在函数名第一次出现时。

## 编程示例：数字分类

在本示例中，我们使用函数重写一个程序，该程序从给定的整数列表中确定奇数和偶数的数量。该程序最初是在第 5 章编写的。

主算法保持不变：

- 1. 将变量 `zeros`、`odds` 和 `evens` 初始化为 0。
- 2. 读取一个数字。
- 3. 如果该数字是偶数，则递增偶数计数；如果该数字同时也是零，则递增零计数；否则，递增奇数计数。
- 4. 对列表中的每个数字重复步骤 2 和 3。

程序的主要部分是：初始化变量、读取并分类数字，然后输出结果。为了简化函数 `main` 并进一步说明参数传递，该程序包含：

- 一个函数 `initialize`，用于初始化变量，例如 `zeros`、`odds` 和 `evens`。
- 一个函数 `getNumber`，用于获取数字。
- 一个函数 `classifyNumber`，用于判断数字是奇数还是偶数（以及是否同时为零）。该函数还会递增相应的计数。
- 一个函数 `printResults`，用于打印结果。

现在让我们描述这些函数中的每一个。

### initialize

函数 `initialize` 将变量初始化为其初始值。我们需要初始化的变量是 `zeros`、`odds` 和 `evens`。和之前一样，它们的初始值都是 0。显然，该函数有三个参数。因为初始化这些变量的形参的值必须从函数外部传入，所以这些形参必须是引用参数。本质上，该函数是：

```cpp
void initialize(int& zeroCount, int& oddCount, int& evenCount)
{
    zeroCount = 0;
    oddCount = 0;
    evenCount = 0;
}
```

该函数不修改变量的值，而只是打印它们。形参是值参数。该函数的定义是：

```cpp
void printResults(int zeroCount, int oddCount, int evenCount)
{
    cout << "There are " << evenCount << " evens, "
         << "which includes " << zeroCount << " zeros"
         << endl;

    cout << "The number of odd numbers is: " << oddCount
         << endl;
} //end printResults
```

### 主算法

现在我们给出主算法，并展示函数 main 如何调用这些函数。

- 1. 调用函数 `initialize` 初始化变量。
- 2. 提示用户输入 20 个数字。
- 3. 对列表中的每个数字：
  - a. 调用函数 `getNumber` 读取一个数字。
  - b. 输出该数字。
  - c. 调用函数 `classifyNumber` 对该数字进行分类并递增相应的计数。
- 4. 调用函数 `printResults` 打印最终结果。

### 完整程序清单

```cpp
///////////////////////////////
// Author: D.S. Malik
//
// Program: Classify Numbers
// This program reads 20 numbers and outputs the number of
// zeroes, odd, and even numbers.
///////////////////////////////

#include <iostream>
#include <iomanip>

using namespace std;

const int N = 20;

    //Function prototypes
void initialize(int& zeroCount, int& oddCount, int& evenCount);
void getNumber(int& num);
void classifyNumber(int num, int& zeroCount, int& oddCount,
                   int& evenCount);
void printResults(int zeroCount, int oddCount, int evenCount);
```
