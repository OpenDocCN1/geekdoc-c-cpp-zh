

- iii. 从质量计算能量。
- iv. 在屏幕上输出一个数值（能量）和一个字符串（描述性标签）。

C++ 提供了针对这些操作中的每一个的操作，除了第三个操作之外。对于这一点，我们必须使用爱因斯坦熟悉的方程

e = m × c²

其中 m 是质量，c 是光速常数，e 是产生的能量。因此执行此操作需要以下操作：

- 指数运算（c²）
- 实数乘法（m × c²）
- 实数存储（e = m × c²）

此细化在我们的对象列表中添加了两个额外的对象：

| 问题对象 | 类型 | 种类 | C++ 标识符 |
|---|---|---|---|
| 软件对象 |  |  |  |
| screen | output device | variable | cout |
| prompt | text string | constant | none |
| quantity of matter | double | variable | mass |
| keyboard | input device | variable | cin |
| quantity of energy | double | variable | energy |
| descriptive label | string | constant | none |
| speed of light | double | constant | SPEED_OF_LIGHT |
| 2 | int | constant | none |

### 4.1.2.4 算法

接下来，我们将这些对象和操作组织成一个算法：

- 1. 定义常数 SPEED_OF_LIGHT。
- 2. 向 cout 显示质量的提示。
- 3. 从 cin 读取一个非负实数到 mass 中。
- 4. 计算 energy = mass × SPEED_OF_LIGHT²。
- 5. 向 cout 输出描述性标签和 energy。

### 4.1.2.5 编码、执行和测试

Example 4.1 中的程序实现了前述算法。其中两个示例运行使用了输出可以轻松检查的测试数据，第三个使用了“真实”数据。

### Example 4.1 质量-能量转换

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

任何小数部分都被丢弃，结果整数即为结果；不会进行四舍五入。在其他涉及除法的表达式中，操作数中至少有一个是实数，因此执行实数除法，产生实数结果 2.25。初学者程序员常见的困难是记住如果 m 和 n 是整数且 |m| < |n|，则 m/n 的值为 0；例如，1/2、1/3、9/10、−99/100 均产生值 0。

在整数除法的情况下，C++ 提供了两个运算符（/）给出整数商，另一个运算符（%）给出整数除法的余数。² 以下有一些示例：

```
6 / 4 → 1      6 % 4 → 2
83 / 10 → 8     83 % 10 → 3
148 / 10 → 14   148 % 10 → 8
```

对于实数值，/ 执行实数除法并产生精度取决于机器的实数商。% 运算符不能用于实数值。

### 4.2.1.1 运算符优先级

表达式中运算符应用的顺序由称为运算符优先级（或 precedence）的特性决定。对于算术运算符，*、/ 和 % 的优先级高于 + 和 −。

优先级较高的运算符在优先级较低的运算符之前应用。例如，在表达式 3 + 4 * 5 中，乘法在加法之前执行，因为 * 的优先级高于 +，因此该表达式的值为 23。附录 C 给出了所有 C++ 运算符的优先级级别。

### 4.2.1.2 运算符结合性

运算符 +、−、*、/ 和 % 都被称为左结合，这意味着在具有两个相同优先级运算符的表达式中，左侧运算符先应用。因此，

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

当 + 和 − 用作 **一元运算符**（即应用于单个操作数）时，如 −x + 5 和 −2 * x，它们具有高于相应二元操作的优先级。因此，如果 x 的值为 −1，则这些表达式的值将分别为 6 和 2。

### 4.2.1.5 总结

以下规则总结了算术表达式的求值。

### OPERATOR PRIORITIES

Higher: unary +, unary -

*, /, %

Lower: binary +, binary -

- 1. 优先级较高的操作在优先级较低的操作之前执行。
- 2. 具有相同优先级的运算符如果为左结合则从左到右应用，如果为右结合则从右到左应用。
- 3. 如果表达式包含带括号的子表达式，则先求值它们，使用规则 1 和 2 指定的顺序。对于嵌套括号，最内层的子表达式先求值。

### 4.2.1.6 位运算符

C++ 还提供了可用于操作整数存储的二进制表示中各个位的运算：~（取反）、&（按位与）、|（按位或）、^（按位异或）、<<（左移位）和 >>（右移位）。它们有时用于必须检查内存或直接与计算机硬件交互的低级图形或操作系统程序中。有关这些操作的更多信息可在前言中描述的文本网站上找到。

### 4.2.2 类型强制转换

如前所述，在涉及整数和实数操作数的混合类型表达式 6.0 / 4 中，C++ 执行实数除法并产生实数值 1.5。这是因为编译器自动将整数值 4 转换为实数值 4.0，然后执行实数除法运算 6.0 / 4.0。编译器进行的这种自动类型转换称为类型强制转换。它也发生在涉及字符和整数或实数的混合类型表达式中；字符值会自动替换为其数字代码（参见第 3.3 节）。例如，如果字符采用 ASCII 表示，则表达式 'a' + 3 的值为 100，因为 'a' 被 97 替换，即其数字代码。

一般来说，这些类型转换在任何混合类型表达式中自动发生，其中“窄”值——存储在较少位数中的值——被转换为占用更多位数的“宽”值。这种在表达式中将较窄值自动扩展到较宽值的大小的过程称为较窄值的提升。它允许字符、整数和实数值在 C++ 表达式中自由混合。两个值如果满足以下条件之一则称为兼容：(i) 它们具有相同的类型，(ii) 一个可以提升为另一个的类型，或 (iii) 两者都可以提升为同一类型。例如，int 和 double 是兼容的，因为 int 可以提升为 double。

### 4.2.2.1 显式类型转换

除了自动类型转换外，显式转换也是可能的。例如，如果 intVal 是整数值，则表达式 double(intVal) 或 (double)intVal 中的任一个都会产生等价于 intVal 的 double 值。类似地，如果 doubleVal 的类型为 double，则 int(doubleVal) 或 (int)doubleVal 中的任一个将截断 doubleVal 的小数部分并产生其整数部分。

一般来说，形式为

```
type(expression)
```

或

```
(type)expression
```

其中 type 是有效的 C++ 类型，可以用于将 expression 的类型转换为 type（如果可能）。第一种形式有时称为函数表示法，最后一种形式称为（C 风格）强制转换表示法。

### 4.3 赋值表达式

赋值表达式使用赋值运算符（=）为变量赋值。

### ASSIGNMENT EXPRESSION

**Form:**

```
variable = expression
```
