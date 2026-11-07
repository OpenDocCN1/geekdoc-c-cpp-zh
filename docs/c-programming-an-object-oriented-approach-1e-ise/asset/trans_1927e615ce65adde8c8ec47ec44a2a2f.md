

### 程序 3.13 计算复杂表达式（续）

| 计算步骤 | 表达式 | 注释 |
| --- | --- | --- |
| result | result = 5 - 15 % 4 | 原始表达式 |
|  | result = 5 - 3 | 第一次计算后 |
|  | result = 2 | 第二次计算后 |
| 副作用 | 2 | 返回值 |

### 例 3.14

现在假设我们需要有意改变一个简单表达式的优先级。例如，我们需要将字面量 6 加到变量 x 的值上，然后将结果乘以 7。这里乘法优先于加法，但我们需要先做加法。解决方案是使用括号。如前所述，一对括号会创建一个处于最高优先级的基本表达式。程序 3.14 展示了如何编写并计算该表达式。

### 程序 3.14 带括号的简单表达式

```cpp
/*********************************************************
 * Evaluating simple expression including parentheses
 **********************************************************/
#include <iostream>
using namespace std;

int main ( )
{
    // Declaration
    int x = 5;
    // Outputting value of expression
    cout << "Value of (x + 6) * 7: " << (x + 6) * 7 ;
    return 0;
}
```

运行：
Value of (x + 6) * 7: 77

| 计算步骤 | 表达式 | 注释 |
| --- | --- | --- |
|  | (x + 6) * 7 | 原始表达式 |
|  | 11 * 7 | 第一次计算后 |
|  | 77 | 第二次计算后 |

### 例 3.15

作为另一个示例，假设 x 和 y 的原始值分别为 8 和 10。程序 3.15 展示了在计算以下表达式后，我们如何求得 y 的值：

### 程序 3.15 带副作用的表达式

```cpp
/* **************************************
   * Evaluating a simple expression with side effect
   ************************************** */
#include <iostream>
using namespace std;

int main( )
{
    // Declaration and initialization
    int x = 8;
    int y = 10;
    // Assignment
    y *= x + 5;
    // Outputting value of variable y
    cout << "Value of y: " << y;
    return 0;
}
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_97_0.png)

**y *= x + 5.** 注意，当我们将复合赋值展开为简单赋值时，复合赋值运算符右侧的表达式被视为一个基本表达式。换句话说，复合赋值实际上是 **y *= (x + 5)**，它展开为 **y = y * (x + 5)**。

### 3.3.2 结合性

在前面的示例中，我们使用的复杂表达式仅包含一个某类表达式实例（乘法、加法或赋值）。如果一个复杂表达式在同一优先级上包含多个表达式（例如两个乘法表达式），会发生什么？在这种情况下，我们需要使用简单表达式的结合性。运算符的结合性要么是从左到右，要么是从右到左（见表 3.1）。当需要计算包含多个同类表达式实例的特定表达式时，我们需要根据它们的结合性来计算这些表达式。

### 例 3.16

我们来求一个包含两个乘法运算符和两个加法运算符的表达式值：**5 − 30 / 4 * 8 + 10**。程序 3.16 展示了 C++ 如何计算该表达式。

### 程序 3.17 具有相同优先级的表达式（续）

```cpp
// Declaration and initialization
int x = 10;
int y = 20;
// Assignment
y += x *= 40;
// Printing values of x and y
cout << "Value of x: " << x << endl;
cout << "Value of y: " << y;
return 0;
}
```

```text
Run:
Value of x: 400
Value of y: 420
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_99_0.png)

## 3.4 溢出和下溢

在编写更多程序之前，我们讨论一个所有程序员都需要理解的问题：*溢出*和*下溢*。在现实生活中，可以在纸上写出一个非常大的数。然而，每种计算机系统中为数据类型分配的内存是有限的。如果我们试图存储一个大于某类型最大值或小于其最小值的数，会发生什么？结果就是**溢出或下溢**。C++ 在编译期间不会产生错误消息，尽管可能会给出警告。实际发生的情况是结果并非我们所期望的。整数和浮点值的溢出与下溢行为不同（其他类型会提升为整数或浮点数，如前所述）。

### 3.4.1 整数中的溢出和下溢

众所周知，整数数据类型可以是有符号的或无符号的。无符号整数和有符号整数的溢出与下溢错误不同。我们分别讨论每种情况。

### 无符号整数中的溢出和下溢

无符号整数的范围从零到正最大值。我们想看看当试图使用大于最大值的值或小于零的值时会发生什么。第一种情况是溢出；第二种情况是下溢。两者如图 3.8 所示。无论哪种情况，值都会被回绕

![](img/d68f6199646ca63591a6d8419e0ed4ba_101_0.png)

**图 3.9** 有符号整数中的溢出和下溢

### 有符号整数中的溢出和下溢

有符号整数的范围从负的最小值到正的最大值。我们想看看当试图使用大于最大值的值或小于最小值的值时会发生什么。第一种情况是溢出；第二种情况是下溢。两者如图 3.9 所示。换句话说，值会被回绕到有效范围内。大于正最大值的正值会变成负值；小于负最小值的负值会变成正值。

程序 3.19 展示了 **signed int** 类型中溢出和下溢的效果。我们将变量（num1）初始化为最大值，然后尝试给它加 1。我们将另一个变量（num2）初始化为最小值，然后尝试从中减 1。输出结果表明发生了回绕。由于最大值和最小值取决于系统，我们在第 11 行和第 12 行使用库函数来设置这些值。

### 程序 3.19 测试有符号整数中的溢出和下溢

```cpp
/*******************************************************
 * A program to test overflow and underflow in signed integers       *
 *******************************************************/
#include <iostream>
#include <limits>
using namespace std;

int main( )
{
    // Find the maximum and minimum of an integer
    int num1 = numeric_limits<int>::max();
    int num2 = numeric_limits<int>::min();
    // Print the maximum and minimum values
    cout << "Value of maximum signed int: " << num1 << endl;
    cout << "Value of minimum signed int: " << num2 << endl;
    // Cause num1 and num2 to overflow
    num1 += 1;
    num2 -= 1;
    // Print the overflowed values
    cout << "The value of num1 + 1 after overflow: " << num1 << endl;
    cout << "The value of num2 - 1 after underflow: " << num2 << endl;
22    return 0;
23  }
```

```text
Run:
The value of maximum signed int: 2147483647
The value of minimum signed int: −2147483648
The value of num1 + 1 after overflow: −2147483648
The value of num2 − 1 after underflow: 2147483647
```

![](img/d68f6199646ca63591a6d8419e0ed4ba_102_0.png)

### 3.4.2 浮点值中的溢出和下溢

浮点值中也会出现溢出和下溢；不过这里有两个不同之处。第一，所有浮点值都是有符号的。第二，发生溢出和下溢时不会回绕；相反，我们会发生*下沉*。溢出会导致下沉到 +无穷大；下溢会导致下沉到 −无穷大。图 3.10 展示了这一概念。

注意，我们有两个最大值和两个最小值。最小值定义了最接近零的小数。正最大值和负最大值在分别增大或减小时，可能会产生正无穷大或负无穷大。程序 3.20 将 num1 和 num2 初始化为正最大值和负最大值，然后将每个数乘以 1000.00，使这些值溢出为 +inf 和 −inf。由于正最大值和负最大值取决于系统，我们在第 11 行和第 12 行使用库函数来初始化它们。

### 程序 3.20 双精度浮点数中的溢出和下溢

```cpp
 1  /**************************************************************
 2  * A program to test overflow and underflow in doubles          *
 3  ***************************************************************/
 4  #include <iostream>
 5  #include <limits>
 6  using namespace std;
 7
 8  int main()
 9  {
10      // Find the positive and negative maximum double
11      double num1 = +numeric_limits<double>::max();
12      double num2 = −numeric_limits<double>::max();
```

