
对于第 21–40 题，判断每个是整数字面量、实数字面量、字符字面量还是字符串字面量。如果都不是，请说明原因。

+   21. `1234`
+   22. `1,234`
+   23. `1.234`
+   24. `-1.`
+   25. `123e4`
+   26. `123-4`
+   27. `0.123E-4`
+   28. `+1235`
+   29. `12+34`
+   30. `$12.34`
+   31. `'12+34'`
+   32. `'one'`
+   33. `one`
+   34. `"Ohm's law"`
+   35. `"1234"`
+   36. `01234`
+   37. `0x1234`
+   38. `E4`
+   39. `'#1'`
+   40. `'\32'`

41. 编写一个类型为 `int` 的变量 `count` 的声明。
42. 编写变量 `time` 类型为 `unsigned`、`temperature` 类型为 `float`、`scale` 类型为 `char` 的声明。
43. 重复第 41 题，但将 `count` 初始化为零。
44. 重复第 42 题，但将 `time` 初始化为 `9999`、`temperature` 初始化为零、`scale` 初始化为空格。
45. 编写常量声明，将 `CELSIUS_FREEZE` 与整数 `0` 关联，将 `CELSIUS_BOIL` 与整数 `100` 关联。
46. 编写常量声明，将 `EARTH` 与 `1.5E10` 关联，将 `MARS` 与 `1.2E12` 关联。

## 练习

对于练习 1–20，判断每个是否为有效的 C++ 标识符。如果不是，请给出原因。

+   1. `x Axis`
+   2. `x-Axis`
+   3. `x_Axis`
+   4. `xAxis`
+   5. `carbon14`
+   6. `3M`
+   7. `PDQ123`
+   8. `angle`
+   9. `angel`
+   10. `anlge`
+   11. `PS.175`
+   12. `x`
+   13. `4`
+   14. `n/4`
+   15. `$M`
+   16. `zzzzzz`
+   17. `z_z_z_z_z_z`
+   18. `A+`
+   19. `R2-D2`
+   20. `R2_D2`

对于练习 21–40，将每个分类为整数字面量、实数字面量或两者都不是。如果两者都不是，请给出原因。

+   21. `5,280`
+   22. `5280`
+   23. `"5280"`
+   24. `528.0`
+   25. `5280e0`
+   26. `-5280`
+   27. `--5280`
+   28. `+5280`
+   29. `52+80`
+   30. `$52.80`
+   31. `52E80`
+   32. `E5280`
+   33. `eighty`
+   34. `0.528E0`
+   35. `.00005280`
+   36. `5.2e-80`
+   37. `+52E+80`
+   38. `-(-1)`
+   39. `-0`
+   40. `-1/2`

对于练习 41–52，判断每个是否为有效的字符串字面量。如果不是，请给出原因。

+   41. `"X"`
+   42. `"123"`
+   43. `INCH"`
+   44. `"square feet"`
+   45. `"Print \"MPH\""`
+   46. `"isn't"`
+   47. `"constant"`
+   48. `"$1.98"`
+   49. `"DON\'T"`
+   50. `"12 + 34"`
+   51. `"\'twas"`
+   52. `"\"A\"\"B\"\"C\""`

对于练习 53–56，编写常量声明，将每个名称与指定的常量关联。

+   53. `40.0` 与名称 `REGULAR_HOURS` 和 `1.5` 与名称 `OVERTIME_FACTOR`
+   54. 普朗克常数 `6.6256 × 10^-34` 与名称 `PLANCK`
+   55. `FAHRENHEIT_FREEZE` 与整数 `32` 和 `FAHRENHEIT_BOIL` 与整数 `212`
+   56. `0` 与 `ZERO`、`*` 与 `ASTERISK`、以及一个撇号与 `APOSTROPHE`

对于练习 57–60，编写每个变量的声明。

+   57. `length` 和 `momentOfInertia` 类型为 `double`
+   58. `population` 和 `year` 类型为 `unsigned`
+   59. `mileage` 类型为 `double`、`cost` 和 `distance` 类型为 `unsigned`
+   60. `alpha` 和 `beta` 类型为 `long`、`code` 类型为 `char`、`root` 类型为 `double`

对于练习 61–62，编写声明以声明每个变量具有指定的类型和初始值。

+   61. `numberOfDeposits` 和 `numberOfChecks` 为类型 `int`，各自初始值为 `0`；`totalDeposits` 和 `totalChecks` 为类型 `double`，各自初始值为 `0.0`；`serviceCharge` 为类型 `double` 初始值为 `0.25`
+   62. `symbol_1` 和 `symbol_2` 为类型 `char` 且初始值分别为一个空白字符和一个分号；`debug` 为类型 `char` 初始值为 `T`。

63. 编写常量声明，将当前年份与名称 `YEAR` 关联，将 `99999.99` 与 `MAXIMUM_SALARY` 关联，并编写变量声明，声明 `number` 和 `prime` 为类型 `int`，`scale` 为类型 `char`。

## 编程问题

+   1. 编写一个程序，将以英尺为单位的测量值转换为等价的 (a) 码、(b) 英寸、(c) 厘米和 (d) 米数（`1 ft = 12 in`，`1 yd = 3 ft`，`1 in = 2.54 cm`，`1 m = 100 cm`）。
+   2. 编写一个程序，将以盎司为单位的重量转换为等价的 (a) 磅、(b) 吨、(c) 克和 (d) 千克数（`1 lb = 16 oz`，`1 ton = 2000 lb`，`1 oz = 28.349523 g`，`1 kg = 1000 g`）。
+   3. 对于三个串联电阻，总电阻是各电阻之和，根据欧姆定律，电路中的电流由 `amps = voltage / total_resistance` 给出。编写一个程序，输入电压和三个电阻，然后计算并显示电流。
+   4. 如问题 3 所进行，但对于并联电阻，总电阻使用公式计算

$$total\_resistance = \frac{1}{\frac{1}{resistor1} + \frac{1}{resistor2} + \frac{1}{resistor3}}$$

> “算术就是能在不脱鞋的情况下数到二十。”

> 

> — 米老鼠

> “有时一点不准确可以节省大量的解释。”

> 

> — 萨基（H. H. MUNROE）

在前一章中，我们研究了如何使用 C++ 类型语句将问题的对象表示为 *软件对象*（也称为 *程序实体*）。本章重点介绍 C++ 中提供的可用于解决问题的操作，以及它们如何用于形成各种表达式。

## 4.1 入门示例：爱因斯坦方程

### 4.1.1 问题

假设你的物理课程教授布置了一套大量问题集，要求在下次课前完成，其中许多问题需要使用爱因斯坦方程计算给定质量的物质释放的能量。由于时间压力，如果所有计算都手工完成，可能会出现错误。最好有一个程序可以用来核对答案。

### 4.1.2 面向对象的设计

#### 4.1.2.1 行为

程序应在屏幕上显示物质数量（即其质量）的提示。然后它将从键盘读取此值。程序随后应使用爱因斯坦方程计算该物质数量可产生的能量，并将此值连同描述性标签一起显示到屏幕上。

#### 4.1.2.2 对象

从我们的行为描述中，我们可以识别出以下对象：

| 问题对象 | 类型 | Kind | 名称 |
|---|---|---|---|
| screen | output device | variable | `cout` |
| prompt | text string | constant | none |
| quantity of matter | `double` | variable | `mass` |
| keyboard | input device | variable | `cin` |
| quantity of energy | `double` | variable | `energy` |
| descriptive label | string | constant | none |

#### 4.1.2.3 操作

同样，从我们的行为描述中，我们有以下操作：

+   i. 输出一个字符串（提示、描述性标签）。
+   ii. 从键盘读取一个非负数值（`mass`）。
- iii. 从质量计算能量。
- iv. 在屏幕上输出一个数值（能量）和一个字符串（描述性标签）。

C++ 提供了针对这些操作中的每一个的操作，除了第三个操作之外。对于这一点，我们必须使用爱因斯坦熟悉的方程

`e = m × c²`

其中 `m` 是质量，`c` 是光速常数，`e` 是产生的能量。因此执行此操作需要以下操作：

- 指数运算（`c²`）
- 实数乘法（`m × c²`）
- 实数存储（`e = m × c²`）

此细化在我们的对象列表中添加了两个额外的对象：

| 问题对象 | 类型 | 种类 | C++ 标识符 |
|---|---|---|---|
| 软件对象 |  |  |  |
| screen | output device | variable | `cout` |
| prompt | text string | constant | none |
| quantity of matter | `double` | variable | `mass` |
| keyboard | input device | variable | `cin` |
| quantity of energy | `double` | variable | `energy` |
| descriptive label | string | constant | none |
| speed of light | `double` | constant | `SPEED_OF_LIGHT` |
| 2 | `int` | constant | none |

#### 4.1.2.4 算法

接下来，我们将这些对象和操作组织成一个算法：

- 1. 定义常数 `SPEED_OF_LIGHT`。
- 2. 向 `cout` 显示质量的提示。
- 3. 从 `cin` 读取一个非负实数到 `mass` 中。
- 4. 计算 `energy = mass × SPEED_OF_LIGHT²`。
- 5. 向 `cout` 输出描述性标签和 `energy`。

#### 4.1.2.5 编码、执行和测试

Example 4.1 中的程序实现了前述算法。其中两个示例运行使用了输出可以轻松检查的测试数据，第三个使用了“真实”数据。

#### Example 4.1 质量-能量转换

```
/* This program computes energy from a given mass using Einstein's mass-to-energy conversion equation.

Input: the mass (in kilograms) being converted to energy
Output: the amount of energy (in kilojoules) corresponding to mass
--------------------------------------------------------------------------*/

#include <iostream>      // cin, cout, <<, >>
#include <cmath>         // pow()
using namespace std;

int main()
{
    const double SPEED_OF_LIGHT = 2.997925e8; // meters/sec

    double mass;
    cout << "To find the amount of energy obtained from a given mass,\n" 
         "enter a mass (in kilograms): ";
    cin >> mass;            // get mass

                        // compute energy
    double energy = mass * pow(SPEED_OF_LIGHT, 2);

                        // display energy
    cout << mass << " kilograms of matter will release\n"
         << energy << " kilojoules of energy.\n";
}
```

### SAMPLE RUNS:

```
To find the amount of energy obtained from a given mass,
enter a mass (in kilograms): 1
1 kilograms of matter will release
8.98755e+16 kilojoules of energy.

To find the amount of energy obtained from a given mass,
enter a mass (in kilograms): .5
0.5 kilograms of matter will release
4.49378e+16 kilojoules of energy.

To find the amount of energy obtained from a given mass,
enter a mass (in kilograms): 155.5
155.5 kilograms of matter will release
1.39756e+19 kilojoules of energy.
```

任何小数部分都被丢弃，结果整数即为结果；不会进行四舍五入。在其他涉及除法的表达式中，操作数中至少有一个是实数，因此执行实数除法，产生实数结果 `2.25`。初学者程序员常见的困难是记住如果 `m` 和 `n` 是整数且 `|m| < |n|`，则 `m/n` 的值为 `0`；例如，`1/2`、`1/3`、`9/10`、`−99/100` 均产生值 `0`。

在整数除法的情况下，C++ 提供了两个运算符（`/`）给出整数商，另一个运算符（`%`）给出整数除法的余数。² 以下有一些示例：

```
6 / 4 → 1      6 % 4 → 2
83 / 10 → 8     83 % 10 → 3
148 / 10 → 14   148 % 10 → 8
```

对于实数值，`/` 执行实数除法并产生精度取决于机器的实数商。`%` 运算符不能用于实数值。

### 4.2.1.1 运算符优先级

表达式中运算符应用的顺序由称为运算符优先级（或 precedence）的特性决定。对于算术运算符，`*`、`/` 和 `%` 的优先级高于 `+` 和 `−`。

优先级较高的运算符在优先级较低的运算符之前应用。例如，在表达式 `3 + 4 * 5` 中，乘法在加法之前执行，因为 `*` 的优先级高于 `+`，因此该表达式的值为 `23`。附录 C 给出了所有 C++ 运算符的优先级级别。

### 4.2.1.2 运算符结合性

运算符 `+`、`−`、`*`、`/` 和 `%` 都被称为左结合，这意味着在具有两个相同优先级运算符的表达式中，左侧运算符先应用。因此，

```
9 - 4 - 3
```

被求值如下

```
(9 - 4) - 3 → 5 - 3 → 2
```

在后面的章节中，我们将看到一些 C++ 运算符是右结合的。

结合性也用于包含不同相同优先级运算符的更复杂表达式。例如，考虑

```
9 * 10 - 8 % 3 * 4 + 5
```

现在执行除法，得出

```
1 + 9
```

加法产生最终结果

```
10
```

即使不需要括号，也应在包含多个操作的表达式中自由使用它们，以使求值意图的顺序清晰，并将复杂表达式写成更简单的表达式的组合。但请确保括号平衡——每个左括号在表达式后面都有一个匹配的右括号——否则会导致编译错误。

### 4.2.1.4 一元运算符

当 `+` 和 `−` 用作 **一元运算符**（即应用于单个操作数）时，如 `−x + 5` 和 `−2 * x`，它们具有高于相应二元操作的优先级。因此，如果 `x` 的值为 `−1`，则这些表达式的值将分别为 `6` 和 `2`。

### 4.2.1.5 总结

以下规则总结了算术表达式的求值。

### OPERATOR PRIORITIES

Higher: unary `+`, unary `-`

`*`, `/`, `%`

Lower: binary `+`, binary `-`

- 1. 优先级较高的操作在优先级较低的操作之前执行。
- 2. 具有相同优先级的运算符如果为左结合则从左到右应用，如果为右结合则从右到左应用。
- 3. 如果表达式包含带括号的子表达式，则先求值它们，使用规则 1 和 2 指定的顺序。对于嵌套括号，最内层的子表达式先求值。

### 4.2.1.6 位运算符

C++ 还提供了可用于操作整数存储的二进制表示中各个位的运算：`~`（取反）、`&`（按位与）、`|`（按位或）、`^`（按位异或）、`<<`（左移位）和 `>>`（右移位）。它们有时用于必须检查内存或直接与计算机硬件交互的低级图形或操作系统程序中。有关这些操作的更多信息可在前言中描述的文本网站上找到。

### 4.2.2 类型强制转换
