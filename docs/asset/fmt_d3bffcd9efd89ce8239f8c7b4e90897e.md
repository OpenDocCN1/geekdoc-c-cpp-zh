
赋值语句 `slope = 3.7;` 将值 `3.7` 分配给 `slope`。下一个赋值语句 `slope = 6.28;` 将 `3.7` 的值覆盖为 `6.28`。像赋值语句中通常一样，程序首先计算等号右侧表达式的值，并将此值存储在等号左侧的变量中。例如，在赋值语句 `totalWeight = factor * weight;` 中，算术表达式 `factor * weight` 被求值以产生结果。

在编写赋值语句时，你需要注意两个重要的考虑因素。由于等号右侧的表达式会被求值，因此如果结果要有意义，表达式中使用的所有变量必须具有有效值。例如，赋值语句 `totalWeight = factor * weight;` 只有当程序员小心给 `factor` 然后给 `weight` 分配了有效数字时，才会在 `totalWeight` 中存储一个有效数字。因此，以下语句序列

```
factor = 1.06;
weight = 155.0;
totalWeight = factor * weight;
```

图 3.1 展示了存储在变量 `factor`、`weight` 和 `totalWeight` 中的值。

| factor | weight | totalWeight |
| --- | --- | --- |
| 1.06 | 155.0 | 164.30 |

图 3.1 存储在变量中的值

第二个考虑因素是，表达式的值存储在等号左侧的变量中，该位置只能列出一个变量。例如，赋值语句

`amount + 1892 = 1000 + 10 * 5;`

是无效的。右侧表达式求值为整数 `1050`，它只能存储在变量中。由于 `amount + 1892` 不是合法的变量名，编译器不知道将计算出的值存储在哪里。

# 第 3 章
## 赋值操作

程序 3.1 展示了如何使用赋值语句计算圆柱体的体积。如图 3.2 所示，圆柱体的体积由公式 `volume = πrh` 决定，其中 `$r$` 是圆柱体的半径，`$h$` 是高度，而 `π` 是常量 `3.1416`（精确到四位小数）。

### 106 赋值 格式化、交互式输入

### 程序 3.1

```cpp
// 此程序计算圆柱的体积，
// 给定半径和高度
#include <iostream>
using namespace std;
```

```cpp
int main()
{
    double radius, height, volume;
    radius = 2.5;
    height = 16.0;
    volume = 3.1416 * radius * radius * height;
    cout << "The volume of the cylinder is " << volume << endl;
    return 0;
}
```

当编译并执行程序 3.1 时，输出如下：

The volume of the cylinder is 314.16

查看计算机在执行程序 3.1 时使用的控制流。程序从 `main()` 函数体的第一条语句开始，并按顺序逐条执行，直到遇到 `main()` 的右大括号。

这种顺序控制流适用于所有程序。计算机一次只处理一条语句，在执行该语句时并不知道下一条语句是什么。这种顺序控制流解释了表达式中使用的所有操作数如何在表达式求值之前被赋值。当计算机执行程序 3.1 中的这条语句时：

`volume = 3.1416 * radius * radius * height;`

它使用的是在赋值语句执行时存储在变量 `radius` 和 `height` 中的任何值。如果在在赋值语句中使用这些变量之前没有为它们专门赋值值，计算机将使用在引用它们时内存中所占据的任何值。大多数 C++ 编译器会自动将所有变量初始化为零。计算机不会“向前看”你之后是否会在程序的后面给这些变量赋值。

在 C++ 中，赋值语句中使用的等号 `=` 是一个运算符，这与大多数其他高级语言处理该符号的方式不同。在 C++ 中（与 C 一样），`=` 符号被称为赋值运算符，而使用该运算符的表达式（如 `interest = principal * rate`）被称为赋值表达式。由于赋值运算符的优先级低于任何算术运算符，因此等号右侧任何表达式的值在赋值之前都会先求值。

> ²由于 C++ 没有幂运算符，半径的平方是通过项 `radius * radius` 来获取的。第 3.3 节引入了 C++ 的幂函数 `pow()`，它允许你将一个数提高某个幂。

## 第 3 章 赋值操作 107

与所有表达式一样，赋值表达式有一个值，该值是赋赋值运算符左侧变量的值。例如，`a = 5` 给变量 `a` 赋值为 `5`，并导致该表达式的值为 `5`。表达式的值始终可以通过如下语句进行验证：

```cpp
cout << "Value of the expression " << (a = 5);
```

这条语句显示表达式的值，而不是变量的内容。虽然变量的内容和表达式具有相同的值，但值得的是，你处理的是两个不同的实体。

从编程的角度来看，对变量进行数值的实际赋值在赋值表达式中是重要的；赋值的最终值其实影响并不大。然而，赋值表达式具有值这一事实具有某些必须被考虑的影响，当你在学习 C++ 关系运算符时必须考虑这些影响，关系运算符将在下一节中解释（第 4.1 节）。

任何以分号终止的表达式都变成一个 C++ 语句。常见的例子是赋值表达式，它仅仅是一个以分号终止的赋值表达式。例如，在赋值语句 `a = 33;` 中用分号终止赋值表达式 `a = 33`，可以在程序中单独占一行使用。

由于等于在 C++ 中是一个运算符，在同一个表达式或等等语句中可以进行多次赋值。例如，在表达式 `a = b = c = 25` 中，所有的赋值操作具有相同的优先级。由于赋值运算符具有从右到左的结合性，最终评估按此顺序进行：

```cpp
c = 25
b = c
a = b
```

这一系列表达式的效果是将数字 `25` 赋值给每个变量，可以表示为：

```cpp
a = (b = (c = 25 ))
```

在原始表达式后附加分号得到此多赋值语句：

```cpp
a = b = c = 25;
```

这条语句将值 `25` 赋值给三个变量，等于：

```cpp
c = 25;
b = 25;
a = 25;
```

### 强制类型转换 (Coercion)

处理赋值语句时，请记住表达式两边的数据类型匹配，因为数据类型转换发生在赋值运算符上。换句话说，赋值运算符右侧表达式的值被转换为赋值运算符左侧变量的数据类型。如果赋值运算符左侧赋值的值被强制转换为其被赋值的数据类型，则这种转换被称为强制类型转换（coercion）。强制类型转换的一个示例发生在将整数值赋值给实数变量时；此赋值导致整数转换为实数值。同样，将实数值赋值给整数变量会强制将实数转换为整数，这始终会导致通过截断丢失数字的小数部分。例如，如果 `temp` 是一个整数变量，赋值 `temp = 25.89` 将值 `25` 转换并存储在整数变量中。

类型转换的一个更完整的示例（包括混合模式和赋值表达式）是表达式表达式的求值：

```cpp
a = b * d
```

其中 `a` 和 `b` 是整数变量，`d` 是单精度变量。当求值混合表达式 `b * d` 时，为了计算目的，`d` 的值被转换为双精度数。由于赋值运算符的左侧是一个整数变量，`(b * d)` 的双精度值被截断为整数值并存储在 `sum` 中。

## 赋值、格式化和交互式输入

### 信息点

| 左值 (lvalues) 和 右值 (rvalues) | |

左值和右值在编程技术中经常被使用。这些术语是与语言无关的，并用于指定以下内容：左值可以被赋值值，但右值不能。

在 C 和 C++ 中，左值可以出现在赋值运算符的左侧和右侧，但右值只能出现在赋值运算符的右侧。你遇到的变量可以是左值也可以是右值，但数字只能是右值。然而，并不是所有变量既是左值也是右值。例如，在第 7 章引入的数组类型既不能是左值也不是右值，但数组元素可以既都是。

### 赋值变体

虽然赋值表达式中符号的左侧只允许一个变量，但左侧的变量也可以用于右侧。例如，赋值表达式 `sum = sum + 10` 是有效的。显然，作为一个代数方程，`sum` 永远等于它自己加10。但在 C++ 中，`sum = sum + 10` 不是方程——它分两个阶段执行：首先，计算 `sum + 10` 的值；其次，将计算出的值存储在 `sum` 中。

## 第 3 章 操作

### 程序 3.2

```cpp
#include <iostream>
using namespace std;
int main()
{
    int sum;
    sum = 25;
    cout << "The number stored in sum is " << sum << endl;
    sum = sum + 10;
    cout << "The number now stored in sum is " << sum << endl;
    return 0;
}
```

在程序 3.2 中，赋值语句 `sum = 25` 告诉计算机将数字25存储在 `sum` 中，如图 3.3 所示。

| sum |
| 25 |

图 3.3 整数 25 存储在 sum

第一个 `cout` 显示存储在 `sum` 中的值以及消息 The stored in sum is 25。第二个赋值语句 `sum = sum + 10;` 导致程序获取存储在 `sum` 中的25 并加上 10，得到 35。然后将数字 35 存储在等号左侧的变量中，即该变量。原本在 `sum` 中的 25 仅仅被新值 35 覆盖（见图 3.4）。

| 旧值被覆盖 | 新值 (35) 被存储 |
| 25 | 35 |

图 3.4 `sum = sum + 10;` 导致新值被存储在 `sum` 中

## 赋值、格式化与交互输入

赋值表达式如 `sum = sum + 25`，在赋值运算符的两侧都使用了相同的变量，可以使用简写赋值运算符来编写：

```
+= ==  / %=
```

例如，表达式 `sum = sum + 10` 可以写为 `sum += 10`。同样，表达式 `price *= rate` 等价于表达式 `price * rate`。在使用这些新的赋值运算符时，赋值运算符左侧的变量被应用于右侧的完整表达式。例如，表达式 `price *= rate + 1` 等价于表达式 `price = price * (rate + 1)`，而不是 `price *= rate + 1`。

### 累加

赋值表达式如 `sum += 10` 或其等价的 `sum = sum + 10` 在编程中非常常见。在逐个输入数据时，需要这些表达式来累加小计。例如，如果你想像计算器一样加上数字 96、70、85 和 60，可以使用以下语句：

| 语句 | sum 中的值 |
|---|---|
| sum = 0; | 0 |
| sum = sum + 96; | 96 |
| sum = sum + 70; | 166 |
| sum = sum + 85; | 251 |
| sum = sum + 60; | 311 |

第一语句将 `sum` 初始化为 0，这消除了存储在 `sum` 中的任何可能导致结果无效的数字（“垃圾值”）。随着每个数字的加入，`sum` 中存储的值相应增加。完成最后一个语句后，`sum` 包含了所有相加数字的总和。程序 3.3 通过显示每次加后 `sum` 的内容说明了这些语句的效果。

# 程序 3.3

```cpp
#include <iostream>
using namespace std;
int main()
{
    int sum = 0;
    cout << "The value of sum is initially set to " << sum << endl;
    sum = sum + 96;
    cout << "sum is now " << sum << endl;
    sum = sum + 70;
    cout << "sum is now " << sum << endl;
    sum = sum + 85;
    cout << "sum is now " << sum << endl;
    sum = sum + 60;
    cout << "The final sum is " << sum << endl;
    return 0;
}
```

程序 3.3 显示此输出：

The value of sum is initially set to 0
sum is now 96
sum is now 166
sum is now 251
The final sum is adding to 311

虽然程序 3.3 不是一个实用的程序（因为手动相加数字更简单），但它说明了这种形式的重复语句的小计效果：

`variable = variable + newValue;`

这种语句被称为累加语句。当你更熟悉第 5 章介绍的循环语句时，你会发现许多累加语句的用法。

### 计数

计数语句是一种与累加语句类似的赋值语句，其形式如下：

`variable = variable + fixedNumber;`

计数语句的示例如下：

```
i = i + 1;
n = n + 1;
count = count + 1;
j = j + 2;
m = m + 2;
kk = k + 3;
```

在这些示例中，等号的两侧使用了相同的变量。执行第一条语句后，变量 `i`、`n` 和 `count` 增加了1。在接下来的两个示例中，变量增加了2，在最后一个示例中，变量 `kk` 增加了3。

对于变量仅增加或减少1 的情况，C++ 提供了两个单元运算符：递增和递减运算符。使用递增运算符 `++`，表达式 `variable + 1` 可以被表达式 `variable +=` 替换。以下是递增运算符的示例：

| 表达式 | 替代方案 |
|---|---|
| i = i + 1 | i++ ++i |
| n = n + 1 | n++ ++n |
| count = count + 1 | count++ ++count |

程序 3.4 展示了递增运算符的使用。

> ^作为历史说明，C++ 名称中的 `++` 受到递增运算符符号的启发。它用来表示 C++ 是 C 语言的下一个增量。

# 第 3 章 赋值操作

# 程序 3.4

```cpp
#include <iostream>
using namespace std;
int main() {
  int count;
  count = 0;
  cout << "The initial value of count is " << count << endl;
  count++;
  cout << " count is now " << count << endl;
  count++;
  cout << " count is now " << count << endl;
  count++;
  cout << " count is now " << count << endl;
  return 0;
}
```

程序 3.4 显示此输出：

The initial value of count is 0
count is now 1
count is now 2
count is now 3
count is now 4

当 `++` 运算符出现在变量之前时，它被称为前置递增运算符；当它出现在变量之后时，它被称为后置递增运算符。当被递增的变量用于赋值表达式时，前置和后置递增运算符之间的区别非常重要。例如，表达式 `k = ++n` 等价于表达式 `k = n * (n + 1)`，而不是 `k = n++`。（*注：此处原文逻辑似乎有误，已按原意翻译*）。

（注：由于提供的文本存在大量重复段落，上述翻译已根据要求合并并保留核心逻辑内容。）

- 11. (Debug) 确定并纠正以下程序中的错误。

- a.
```cpp
#include <iostream>
using namespace std;
int main() {
    int width = 15;
    int area = length * width;
    cout << "The area is " << area;
}
```

- b.
```cpp
#include <iostream>
using namespace std;
int main() {
    int length, width, area;
    length = 20;
    width = 15;
    area = length * width;
    cout << "The area is " << area;
    return 0;
}
```

- c.
```cpp
#include <iostream>
int main() {
    int length = 20, width = 15, area;
    area = length * width;
    cout << "The area is " << area;
    return 0;
}
```

- 12. (Debug) 错误地将程序 3.3 中的语句重新排序如下：

```cpp
#include <iostream>
using namespace std;
int main() {
    int sum;
    sum = 0;
    sum = sum + 96;
    sum = sum + 70;
    sum = sum * 85;
    sum = sum * 60;
    cout << "The value of sum is initially set to " << sum << endl;
```
