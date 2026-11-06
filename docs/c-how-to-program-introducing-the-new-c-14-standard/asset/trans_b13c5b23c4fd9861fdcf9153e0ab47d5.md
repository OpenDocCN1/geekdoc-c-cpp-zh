

## 5.4 使用`for`语句的示例

下面的示例展示了在`for`语句中改变控制变量的技巧。在每种情况下，我们*只*编写相应的`for`语句头。注意对于*递减*控制变量的循环，关系运算符发生了变化。

- 1. 使控制变量从`1`变到`100`，每次增量为`1`。

```cpp
for (unsigned int i{}; i <= 100; i++)
```

- 2. 使控制变量从`100`递减到`1`，每次减量为`1`。

```cpp
for (unsigned int i{100}; i >= 1; i--)
```

- 3. 使控制变量从`7`变到`77`，每次增量为`7`。

```cpp
for (unsigned int i{7}; i <= 77; i += 7)
```

- 4. 使控制变量从`20`递减到`2`，每次*减量*为`2`。

```cpp
for (unsigned int i(20); i >= 2; i -= 2)
```

- 5. 使控制变量依次取值`2`、`5`、`8`、`11`、`14`、`17`、`20`。

```cpp
for (unsigned int i(2); i <= 20; i += 3)
```

- 6. 使控制变量依次取值`99`、`88`、`77`、`66`、`55`、`44`、`33`、`22`、`11`、`0`。这里我们使用`int`而不是`unsigned int`，因为条件直到`i`的值为`-11`时才变为假，因此控制变量必须能够表示正值和负值。

```cpp
for (int i(99); i >= 0; i -= 11)
```

在向下计数的循环的循环继续条件中使用错误的关系运算符（例如，在向下计数到1的循环中使用`i <= 1`而不是`i >= 1`）通常是逻辑错误。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_573_0.png)

## 常见编程错误

### 5.5

如果循环的控制变量每次递增或递减超过1，不要在循环继续条件中使用相等运算符（`!=`或`==`）。例如，考虑`for`语句头`for (unsigned int counter{1}; counter != 10; counter += 2)`。循环继续条件测试`counter != 10`永远不会变为假（导致无限循环），因为`counter`在每次迭代后递增2（并且永远不会变为10）。

## 5.5 应用：对偶数求和

我们现在来考虑两个示例应用，它们演示了`for`的简单用法。**图5.5**中的应用使用`for`语句对从2到20的偶数求和，并将结果存储在一个名为`total`的`unsigned int`变量中。循环的每次迭代（第10-12行）都将控制变量`number`的值加到变量`total`上。

```cpp
// Fig. 5.5: Sum.cpp
// Summing integers with the for statement.
#include <iostream>
using namespace std;

int main() {
    unsigned int total{};

    // total even integers from 2 through 20
    for (unsigned int number{2}; number <= 20; number += 2) {
        total += number;
    }

    cout << "Sum is " << total << endl;
}
```

```text
Sum is 110
```

**图5.5** 使用`for`语句对整数求和。

*初始化*和*增量*表达式可以是逗号分隔的列表，使您能够使用多个初始化表达式或多个增量表达式。例如，虽然不鼓励这样做，但您可以使用逗号将`for`语句的循环体（第11行）合并到`for`语句头的增量部分中，如下所示：

```cpp
total += number, number += 2
```

表达式`total += number`和`number += 2`之间的逗号是**逗号运算符**，它保证表达式列表从左到右求值。逗号运算符在所有C++运算符中优先级最低。逗号分隔的表达式列表的值和类型是*最右边*表达式的值和类型。逗号运算符通常用于需要*多个初始化表达式*和/或*多个增量表达式*的`for`语句中。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_575_0.png)

## 良好编程实践

### 5.1

*在`for`语句的初始化和增量部分中，只放置涉及控制变量的表达式。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_576_0.png)

## 良好编程实践

### 5.2

*为了可读性，如果可能，将控制语句头的长度限制为一行。*

## 5.6 应用：复利计算

让我们使用`for`语句来计算复利。考虑以下问题：

- *某人将1000美元存入一个年利率为5%的储蓄账户。假设所有利息都留在存款中，计算并打印10年内每年年底账户中的金额。使用以下公式来确定这些金额：*

$$a = p(1+r)^n$$

其中

- $p$ 是原始投资金额（即本金）
- $r$ 是年利率（例如，5%使用0.05）
- $n$ 是年数
- $a$ 是第$n$年年底的存款金额。

这个问题的解决方案（*图5.6*）涉及一个循环，该循环在资金存入的10年中的每一年执行指定的计算。对于这个解决方案，我们使用`double`值进行货币计算，然后讨论使用浮点类型表示货币金额的问题。在下一节中，我们将开发一个新的`DollarAmount`类，它使用非常大的整数来精确表示货币金额。您将看到，该类仅使用整数运算来执行货币计算。

```cpp
// Fig. 5.6: Interest.cpp
// Compound-interest calculations with for.
#include <iostream>
#include <iomanip>
#include <cmath> // for pow function
using namespace std;

int main() {
    // set floating-point number format
    cout << fixed << setprecision(2);

    double principal{1000.00}; // initial amount before interest
    double rate{0.05}; // interest rate

    cout << "Initial principal: " << principal << endl;
    cout << "    Interest rate:  " << rate << endl;

    // display headers
    cout << "Year" << setw(20) << "Amount on deposit" << endl;

    // calculate amount on deposit for each of ten years
    for (unsigned int year{1}; year <= 10; year++) {
        // calculate amount on deposit at the end of the specified year
        double amount = principal * pow(1.0 + rate, year);

        // display the year and the amount
        cout << setw(4) << year << setw(20) << amount << endl;
    }
}
```

```text
Initial principal: 1000.00
    Interest rate:  0.05

Year   Amount on deposit
   1             1050.00
   2             1102.50
   3             1157.63
   4             1215.51
   5             1276.28
   6             1340.10
   7             1407.10
   8             1477.46
   9             1551.33
  10             1628.89
```

**图5.6** 使用`for`进行复利计算。

`main`中的第12-13行声明了`double`变量`principal`和`rate`，并将`principal`初始化为`1000.00`，将`rate`初始化为`0.05`。C++将像`1000.00`和`0.05`这样的浮点字面量视为`double`类型。类似地，C++将像`7`和`-22`这样的整数字面量视为`int`类型。第15-16行显示初始本金和利率。

## 使用字段宽度和对齐方式格式化

`for`循环之前的第10行输出语句与`for`循环中的第27行输出语句相结合，按照*参数化*流操纵符`setprecision`和**`setw`**以及*非参数化*流操纵符`fixed`所指定的格式，打印变量`year`和`amount`的值。流操纵符`setw(4)`指定下一个输出的值应出现在4个字符的**字段宽度**中——即`cout <<`打印该值时*至少*占用四个字符位置。如果要输出的值的宽度*小于*四个字符位置，则该值默认在字段中**右对齐**。如果要输出的值的宽度*大于*四个字符位置，则字段宽度会向右扩展额外的字符位置以容纳整个值。若要指示值应**左对齐**输出，只需输出非参数化流操纵符`left`（位于头文件`<iostream>`中）。通过输出非参数化流操纵符`right`可以恢复右对齐。

