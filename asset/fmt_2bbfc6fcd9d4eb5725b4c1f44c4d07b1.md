
程序 10.18 的示例结果如下：

```
Enter the number of disks: 3
Move Disk 1 from Post A to C
Move Disk 2 from Post A to B
Move Disk 1 from Post C to B
Move Disk 3 from Post A to C
Move Disk 1 from Post B to A
Move Disk 2 from Post B to C
Move Disk 1 from Post A to C
```

在程序文件的顶部，例如对于常见的数学计算，我们使用 `#include <cmath>` 指令来包含 `cmath` 文件，该文件包含了 `cmath` 库中数学函数的函数原型。附录 A 提供了 C++ 中一些常用内置函数的列表。

例如，为了编写涉及浮点数计算等的数学程序，我们无疑需要访问数学库。这些函数和相关的宏定义在 `<cmath>` 头文件中。在表 10.2 中，`x` 和 `y` 的类型为 `double`，`n` 是 `int`，且所有函数都返回 `double`。三角函数的角度用弧度而不是角度表示。

### 表 10.2：C++ 中的示例数学函数。

| 数学函数 | 描述 |
| :--- | :--- |
| `sin(x)` | `x` 的正弦 |
| `cos(x)` | `x` 的余弦 |
| `tan(x)` | `x` 的正切 |
| `exp(x)` | 指数函数 $e^x$ |
| `log(x)` | 以 $e$ 为底的自然对数，$x>0$ |
| `log10(x)` | 以 10 为底的对数 $\log10(x)$，$x>0$ |
| `pow(x,y)` | $x^y$，如果 $x=0$ 或 $y\le0$，或者当 $x<0$ 且 $y$ 不是整数，则发生域错误 |
| `sqrt(x)` | $x$ 的平方根，$x \ge0$ |
| `ceil(x)` | 不小于 `x` 的最小整数，以 `double` 类型表示 |
| `floor(x)` | 不大于 `x` 的最大整数，以 `double` 类型表示 |
| `fabs(x)` | 绝对值 $|x|$ |

程序 10.20 展示了在 C++ 中使用数学内置函数的示例。

```cpp
// Program 10.20
// Built-in functions example
#include <iostream>
#include <cmath>
using namespace std;
int main()
{
    double x = 1.0, y = 2.0, z = -3.45;
    cout << "Math-sin example : " << sin(22.0/42.0) << endl;
    cout << "Math-cos example : " << cos(0.0) << endl;
    cout << "Math-tan example : " << tan(22.0/28) << endl;
    cout << "Math-exp example : " << exp(x) << endl;
    cout << "Math-log(base e) example : " << log(2.71822) << endl;
    cout << "Math-log(base 10) example : " << log10(100.0) << endl;
    cout << "Math-power example : " << pow(4,y) << endl;
    cout << "Math-square root example : " << sqrt(y) << endl;
    cout << " Math-ceil example : " << ceil(z) << endl;
    cout << " Math-floor example : " << floor(z) << endl;
    cout << " Math-absolute value example : " << fabs(z) << endl;
    return 0;
}
```

程序 10.20 的结果如下：

```
Math-sin example : 0.500183
Math-cos example : 1
Math-tangent example : 1.00063
Math-exp example : 2.71828
Math-log(base) example : 0.999974
Math-log(base 10) example : 2
Math-power example : 16
math-square root example : 1.41421
Math-ceil example : -3
Math-floor example : -4
Math-absolute value example : 3.45
```

## 10.11 复习题

1. 什么是函数？用户定义函数与 `main()` 函数有什么区别？
2. 用户定义函数与内置函数有什么区别？请讨论。
3. 描述与函数相关的术语：函数名、函数签名、返回类型、函数原型、实参、形参和函数参数。
4. 描述 C++ 中函数的通用格式以演示用户定义函数。
5. 编写一个 C++ 程序来演示用户定义函数。
6. 编写一个可执行程序来演示从 `main()` 传递参数。
7. 解释函数中的以下关键字：(a) `return` (b) `void` (c) `static` (d) `inline`。
8. 变量的作用域是什么？
9. 什么是递归？编写一个程序进行演示。
10. 编写一个 C++ 程序查找递归。
11. 编写一个 C++ 程序生成斐波那契数列。
12. 编写一个 C++ 程序进行演示。
13. 列出 C++ 中至少五个可用函数。
14. 编写一个程序进行演示。

在一个文件中。随后，在程序中声明并使用该结构类型的变量。例如：

```cpp
struct item Biscuit;
```

我们也可以像下面所示定义一个 `struct item` 类型的变量：

```cpp
struct item
{
    char item_name[10];
    float price;
    char manufacturer[40];
    int item_no;
} Biscuit;
```

同样，要定义多个 `struct item` 类型的变量，我们可以使用以下语句中的任意一个。

```cpp
struct item Biscuit, Candy;
```

或者，

```cpp
struct item
{
    char item_name[10];
    float price;
    char manufacturer[40];
    int item_no;
} Biscuit, Candy;
```

## 11.3 结构的初始化

为结构体对象成员赋值的第一种方法是在对象定义中定义它们的值。假设我们想初始化一个项目，其中包含你最喜爱的饼干之一“SweetBest”的数据，价格标签为 7.50 元，项目编号为 9341，由“青岛饼干有限公司”制造。我们可以按照如下方式初始化结构：

```cpp
struct item Biscuit =
{
    "SweetBest",
    7.5,
    "Qingdao Biscuits Ltd",
    9341
};
```

初始化值出现在初始化列表中，其方式与数组元素相同。然而，数组中初始值的顺序需要与该结构体在定义中成员的顺序一致。`Biscuit` 结构中的每个成员都有一个对应的初始值，如注释所示。初始化结构变量的语法与标准变量的语法不同。由于 `item_name` 和 `manufacturer` 成员是数组或字符串，简单使用赋值是不起作用的。结构元素通过点符号（dot notation）访问。单个元素（如 `item_no`）的初始化如下：

```cpp
Biscuit.price = 7.5;
Biscuit.item_no = 9341;
```

人们可以通过像之前那样初始化单个元素来初始化结构，也可以简单地在花括号内列出元素的值，每个值在单行内用逗号分隔，如下所示。

```cpp
struct item Biscuit = {"SweetBest",7.5,"Qingdao Biscuits Ltd",9341};
```

与数组的初始化类似，结构的部分初始化可以如下所示：

```cpp
struct item Biscuit = {"SweetBest",7.5,"Qingdao Biscuits Ltd"};
```

在前面的案例中，`item_no` 元素被初始化为 0.0。在下一节中，我们将学习更多点符号以及如何访问成员结构。

## 11.4 访问结构成员

在 11.3 节中，我们学习了结构的定义及其成员的初始化。要访问结构的单个成员，我们使用点（`.`）作为成员选择运算符。该运算符有时被称为成员访问运算符。要引用一个成员，我们编写变量名结构，后面跟一个点，然后是成员名。成员访问运算符编码为结构变量名和我们想要访问的结构成员之间的一个点。例如，要将 `item_no` 改为 1818，我们可以像下面所示：

```cpp
Biscuit.item_no = 1818;
```

这会将 `item_no` 的值设置为 1818。此外，我们可以像使用任何其他变量完全相同的方式使用结构成员。例如，要将成员编号增加 4，我们可以写：

```cpp
Biscuit.item_no += 4;
```

程序 11.1 显示了一个总结之前描述的示例。在以下程序中，声明了两个类型 `item` 的结构 `Biscuit` 和 `Candy`。对于结构 `Biscuit`，我们通过初始化来提供值。然而，对于结构 `Candy`，我们从键盘读取值。最后，信息显示在屏幕上。

```cpp
// 程序 11.1
// 理解结构
#include <iostream>
using namespace std;
int main()
{
    struct item
    {
        char item_name[10];
        float price;
        char manufacturer[40];
        int item_no;
    };
    // Biscuit 结构的初始化
    struct item Biscuit = {
        "SweetBest",
        7.5,
        "Qingdao Biscuits Ltd",
        9341
    };
    struct item Candy;
    // 读取 Candy 的成员值
    cout << "Enter the item_name for Candy " << endl;
    cin >> Candy.item_name;
    cout << "Enter the price of candy " << endl;
    cin >> Candy.price;
    cout << "Enter the Manufacturer name " << endl;
    cin >> Candy.manufacturer;
    cout << "Enter the item number " << endl;
    cin >> Candy.item_no;
    // 将 Biscuit 信息显示到屏幕
    cout << endl << "Biscuit Information " << endl;
    cout << "Biscuit Name: " << Biscuit.item_name << endl;
    cout << "Biscuit Price: " << Biscuit.price << endl;
    cout << "Biscuit Manufacturer: " << Biscuit.manufacturer << endl;
    cout << "Biscuit Item Number: " << Biscuit.item_no << endl;
    return 0;
}
```

## 11.5 使用 typedef

正如第3章所述，C++ 允许使用 `typedef` 关键字重命名数据类型。例如：

```cpp
typedef int Uint;
```

## 11.6 嵌套结构

在程序 11.1 中，结构只有四个成员。让我们考虑另一种结构，它反过来包含另一个结构作为其成员之一。下面的示例描述了一个嵌套结构的示例。

```cpp
struct item {
    char item_name[10];
    float price;
    char manufacturer[40];
    int item_no;
    date expiry_date;
};
```

`expiry_date` 的定义要求预先定义 `item_date` 结构，否则会产生编译器错误。因此，我们可以如下所示定义 `item_date` 结构：

```cpp
typedef struct
{
    int day;
    int month;
    int year;
}item_date;
```

## 11.7 包含数组的结构 — 211

```cpp
<< Biscuit.expiry_date.day << "/"
<< Biscuit.expiry_date.month << "/"
<< Biscuit.expiry_date.year << endl;
return 0;
```

程序 11.2 的结果所示：

| 饼干名称：SweetBest |
| --- |
| 饼干价格：7.5 |
| 饼干厂家：青岛饼有限公司 |
| 饼干编号：9341 |
| 饼干过期日期：11/8/2019 |

此示例演示了 `typedef` 关键字与结构体的应用。最初，使用成员运算符或点符号对类型为 `item` 的 `Biscuit` 结构体的前几个成员进行逐个初始化。由于第一个成员 `item_name` 和第三个成员 `manufacturer` 是字符数组，因此我们使用了 `strcpy()` 函数来将字符串赋值给它们。第四个成员 `expiry` 是 `item_date` 类型的嵌套结构。由于 `expiry_date` 结构位于 `Biscuit` 结构内部，我们应该像下面的语句一样使用点符号。

```cpp
Biscuit.expiry_date.day = 11;
Biscuit.expiry_date.month = 8;
Biscuit.expiry_date.year = 2019;
```

## 11.7 包含数组的结构

程序 11.2 中定义的 `item` 结构，其成员 `item_name` 和 `manufacturer` 都是字符数组。因此，结构体中包含包含数组的元素也是完全可能的，但在初始化它们时需要格外小心。让我们考虑一个同时包含字符数组和整数数组的额外结构示例。

```cpp
struct Science_Scores
{
    char student_name[20];
    int student_number;
    char subject_name[4][15];
    int student_score[4];
};
```

```cpp
struct Science_Scores FirstYearStudent;
```

在之前的结构 `FirstYearStudent` 中，有四个成员，其中三个是数组。数组 `student_name` 和 `student_score` 是一维数组，而数组 `subject_name` 是二维数组。考虑一个学生“东超”的成绩单示例，她的学号为 911212：

### 表 11.1：学生成绩单示例

| 学生姓名 | 东超 | |
| --- | --- | --- |
| 学号 | 911212 | |
| 科目名称 | 得分 | |
| 科目 1 | 物理 | 86 |
| 科目 2 | 化学 | 97 |
| 科目 3 | 数学 | 81 |
| 科目 4 | 生物 | 91 |

表 11.1 所示的成绩单四个科目，它们都是字符数组。因此，我们定义了字符串数组 `char subject_name[4][15]`。由于四个科目，我们需要一个整数数组来显示每个科目的成绩。程序 11.3 演示了表 11.1 中提到的成绩单示例，并展示了结构体如何处理不同类型的数组。

```cpp
// 程序 11.3
// 包含数组的结构示例
#include <iostream>
#include <cstring>
using namespace std;
int main()
{
  struct Science_Scores
  {
    char student_name[20];
    int student_number;
    char subject_name[4][15];
    int student_score[4];
  };
}
```

## 11.7 包含数组的结构 — 213

```cpp
struct Science_Scores FirstYearStudent;
strcpy(FirstYearStudent.student_name, "Dong Chao");
FirstYearStudent.student_number = 911212;
```

```cpp
strcpy(FirstYearStudent.subject_name[0], "Physics");
strcpy(FirstYearStudent.subject_name[1], "Chemistry");
```
