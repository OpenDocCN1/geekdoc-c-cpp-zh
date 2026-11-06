

**表 1 C++ 中的变量定义**

| 变量名 | 注释 |
|---|---|
| `int cans = 6;` | 定义一个整型变量，并将其初始化为 6。 |
| `int total = cans + bottles;` | 初始值不必是常量。（当然，cans 和 bottles 必须已经预先定义。） |
| ⛔ `int bottles = "10";` | **错误：**不能使用字符串初始化数字。 |
| `int bottles;` | 定义一个未初始化的整型变量。这可能导致错误——参见第 37 页的常见错误 2.2。 |
| `int cans, bottles;` | 在一条语句中定义两个整型变量。在本书中，我们将分别使用单独的语句定义每个变量。 |
| ⚠️ `bottles = 1;` | **注意：**缺少类型。此语句不是定义，而是将新值赋给现有变量——参见第 34 页的第 2.1.4 节。 |

## 2.1.2 数字类型

> 对于不能包含小数部分的数字，请使用 `int` 类型。

在 C++ 中，有几种不同的数字类型。可以使用称为 `int` 的*整数*类型表示没有小数部分的整数。例如，一箱罐装饮料中的罐数必须是整数——不可能有半罐饮料。

**表 2 C++ 中的数字字面量**

| 数字 | 类型 | 注释 |
|---|---|---|
| 6 | int | 整数没有小数部分。 |
| -6 | int | 整数可以是负数。 |
| 0 | int | 零是整数。 |
| 0.5 | double | 带有小数部分的数字类型为 double。 |
| 1.0 | double | 带有小数部分 .0 的整数类型为 double。 |
| 1E6 | double | 使用指数表示法表示的数字：1 × 10^6 或 1000000。使用指数表示法的数字始终为 double 类型。 |
| 2.96E-2 | double | 负指数：2.96 × 10^-2 = 2.96 / 100 = 0.0296 |
| ⛔ 100,000 | | **错误：**不要使用逗号作为数字分隔符。 |
| ⛔ 3 1/2 | | **错误：**不要使用分数；请使用十进制表示法：3.5。 |

![](img/5e58fb4c840712efd6ed6fa82bb97f57_60_0.png)

当需要小数部分时（例如数字 0.355），我们使用浮点数。C++ 中最常用的浮点数类型称为 double。（如果想了解原因，请阅读第 38 页的专题 2.1。）下面是浮点变量的定义：

```
double can_volume = 0.355;
```

当 6 或 0.355 这样的值出现在 C++ 程序中时，它被称为数字字面量。表 2 展示了如何在 C++ 中书写整数和浮点数字面量。

## 2.1.3 变量名

定义变量时，应选择一个能够说明其用途的名称。例如，使用 `can_volume` 这样的描述性名称，比使用 `cv` 这样的简短名称更好。

在 C++ 中，变量名有几条简单规则：

1. 变量名必须以字母或下划线（_）字符开头，其余字符必须是字母、数字或下划线。
2. 不能使用 `$` 或 `%` 等其他符号。名称中也不允许有空格。可以使用下划线代替空格，例如 `can_volume`。
3. 变量名**区分大小写**，也就是说，`Can_volume` 和 `can_volume` 是不同的名称。因此，变量名最好只使用小写字母。
4. 不能使用 `double` 或 `return` 等保留字作为名称；这些单词专门保留用于表示 C++ 中的特殊含义。（参见附录 B。）

表 3 展示了 C++ 中合法和非法变量名的示例。

| 变量名 | 注释 |
|---|---|
| `can_volume1` | 变量名由字母、数字和下划线字符组成。 |
| `x` | 在数学中，通常使用 x 或 y 这样的简短变量名。在 C++ 中这样做是合法的，但并不常见，因为这可能使程序更难理解（参见第 38 页的编程提示 2.1）。 |
| ⚠️ `Can_volume` | **注意：**变量名区分大小写。此变量名与 `can_volume` 不同。 |
| 🚫 `6pack` | **错误：**变量名不能以数字开头。 |
| 🚫 `can volume` | **错误：**变量名不能包含空格。 |
| 🚫 `double` | **错误：**不能使用保留字作为变量名。 |
| 🚫 `ltr/fl.oz` | **错误：**不能使用 `/` 或 `.` 等符号。 |

## 2.1.4 赋值语句

> 赋值语句将一个新值存储到变量中，替换之前存储的值。

可以使用**赋值语句**将新值放入变量中。下面是一个示例：

```
cans_per_pack = 8;
```

赋值语句的左侧由一个变量组成。右侧是一个具有值的表达式。该值会存储到变量中，并覆盖变量之前的内容。

变量定义和赋值语句之间有一个重要区别：

```
int cans_per_pack = 6;  // Variable definition
...
cans_per_pack = 8;      // Assignment statement
```

第一条语句是 cans_per_pack 的*定义*。它指示创建一个 `int` 类型的新变量，将其命名为 cans_per_pack，并使用 6 对其进行初始化。第二条语句是*赋值语句*：它指示将现有变量 cans_per_pack 的内容替换为另一个值。

`=` 符号并不表示左侧等于右侧。右侧的表达式会被求值，其值随后放入左侧的变量中。

> 赋值运算符 `=` 不表示数学上的相等关系。

不要将此*赋值操作*与代数中用于表示*相等*的 `=` 混淆。赋值运算符是一条执行某项操作的指令，即将一个值放入变量中。数学上的相等关系则表示两个值相等这一事实。

例如，在 C++ 中，下面的写法完全合法：

```
total_volume = total_volume + 2;
```

它表示读取变量 total_volume 中存储的值，将其加上 2，然后将结果放回 total_volume 中。（参见图 1。）执行该语句的最终效果是将 total_volume 增加 2。例如，如果执行该语句之前 total_volume 为 2.13，那么执行之后它将被设置为 4.13。当然，在数学中，写出 x = x + 2 是没有意义的。没有任何值会等于它自身加 2。

### 语法 2.2 赋值

![](img/5e58fb4c840712efd6ed6fa82bb97f57_61_0.png)

可以使用 `//` 语法编写单行注释。如果注释跨越多行，请将其放在 `/*` 和 `*/` 分隔符之间。编译器会忽略这些分隔符以及其中的所有内容。

下面是一个典型示例：在程序开头使用一段较长的注释来说明程序的用途：

```
/*
   This program computes the volume (in liters) of a six-pack of soda cans
   and the total volume of a six-pack and a two-liter bottle.
*/
```

现在我们已经准备好完成程序。下面的程序展示了变量、常量和赋值语句的用法。该程序显示一组六罐装饮料的容量，以及这组六罐装饮料和一瓶两升饮料的总容量。我们使用常量表示罐子和瓶子的容量。total_volume 变量使用罐子的容量进行初始化。然后使用赋值语句加上瓶子的容量。

### ch02/volume1.cpp

```
#include <iostream>

using namespace std;

/*
   This program computes the volume (in liters) of a six-pack of soda
   cans and the total volume of a six-pack and a two-liter bottle.
*/
int main()
{
   int cans_per_pack = 6;
   const double CAN_VOLUME = 0.355; // Liters in a 12-ounce can
   double total_volume = cans_per_pack * CAN_VOLUME;

   cout << "A six-pack of 12-ounce cans contains "
        << total_volume << " liters." << endl;

   const double BOTTLE_VOLUME = 2; // Two-liter bottle

   total_volume = total_volume + BOTTLE_VOLUME;

   cout << "A six-pack and a two-liter bottle contain "
        << total_volume << " liters." << endl;

   return 0;
}
```

### 程序运行结果

```
A six-pack of 12-ounce cans contains 2.13 liters.
A six-pack and a two-liter bottle contain 4.13 liters.
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_63_0.png)

1. 定义一个适合存储箱中瓶子数量的变量。
2. 下面的变量定义有什么问题？

```
int ounces_per_liter = 28.35;
```

