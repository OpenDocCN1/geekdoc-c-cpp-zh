
## main 的返回类型

main 函数的 int 返回值指示程序是否正确执行。在早期版本的 C 中，我们会显式地在 main 末尾放置

`return 0; // 0 indicates successful program termination`

C 标准指出，如果省略上述语句——正如本书通篇所做的那样——main 会隐式返回 0。你可以从 main 显式返回非零值，以指示程序执行期间发生了问题。有关如何报告程序失败的信息，请参阅你所使用操作系统的文档。

## 5.3.2 maximum 函数

让我们考虑一个自定义的 maximum 函数，它返回三个整数中的最大值（图 5.2）。接下来，它们被传递给 maximum（第 17 行），由它确定最大的整数。该值由 maximum 中的 return 语句（第 32 行）返回给 main。随后，第 17 行的 printf 语句打印 maximum 返回的值。

```c
// fig05_02.c
// Finding the maximum of three integers.
#include <stdio.h>

int maximum(int x, int y, int z); // function prototype

int main(void) {
   int number1 = 0; // first integer entered by the user
   int number2 = 0; // second integer entered by the user
   int number3 = 0; // third integer entered by the user

   printf("%s", "Enter three integers: ");
   scanf("%d%d%d", &number1, &number2, &number3);

   // number1, number2 and number3 are arguments
   // to the maximum function call
   printf("Maximum is: %d\n", maximum(number1, number2, number3));
}

// Function maximum definition
int maximum(int x, int y, int z) {
   int max = x; // assume x is largest

   if (y > max) { // if y is larger than max,
      max = y; // assign y to max
   }

   if (z > max) { // if z is larger than max,
      max = z; // assign z to max
   }

   return max; // max is largest value
}
```

**图 5.2** | 求三个整数中的最大值。（第 1 部分，共 2 部分。）

```text
Enter three integers: 22 85 17
Maximum is: 85
```

```text
Enter three integers: 47 32 14
Maximum is: 47
```

```text
Enter three integers: 35 8 79
Maximum is: 79
```

**图 5.2** | 求三个整数中的最大值。（第 2 部分，共 2 部分。）

该函数最初假定其第一个实参（存储在参数 `x` 中）是最大值，并将其赋给 `max`（第 22 行）。接下来，第 24—26 行的 `if` 语句判断 `y` 是否大于 `max`，如果是，则将 `y` 赋给 `max`。然后，第 28—30 行的 `if` 语句判断 `z` 是否大于 `max`，如果是，则将 `z` 赋给 `max`。最后，第 32 行将 `max` 返回给调用者。

### 自测

- 1. *(单选题)* 下面这行代码是 ______。

```c
int square(int y);
```

a) 函数定义。
b) 函数语句。
c) 函数原型。
d) 以上都不是。

答案：c。

- 2. *(单选题)* 考虑图 5.2 中的 maximum 函数。以下哪个说法是*错误的*？

a) 该代码确定三个整数值中的最大值。
b) 语句 `return max;` 将结果送回调用函数。
c) 第 21 行代码——`int maximum(int x, int y, int z)`——通常称为函数头。
d) 如果 `int max = x;`（第 22 行）被意外替换为 `int max = y;`，该函数仍会返回相同结果。

答案：d) 是*错误的*。此时该函数将错误地返回仅参数 `y` 和 `z` 所含值中的较大者。

## 5.6 函数原型：深入探讨

C 的一个重要特性是函数原型，它借鉴自 C++。编译器使用函数原型来验证函数调用。标准之前的 C 不执行这种检查，因此可能以不正确的方式调用函数，而编译器检测不到这些错误。这类调用可能导致致命的执行时错误，或导致隐蔽、难以检测问题的非致命错误。函数原型纠正了这一缺陷。

你应为所有函数包含函数原型，以利用 C 的类型检查能力。使用 #include 预处理指令从标准库头文件、第三方库头文件以及你或团队成员开发的函数头文件中获取函数原型。

图 5.2 中 maximum 的函数原型（第 5 行）为

```
int maximum(int x, int y, int z); // function prototype
```

它表明 maximum 接受三个 int 类型的实参并返回一个 int 结果。注意，函数原型（省略分号）与 maximum 定义的第一行相同。我们在函数原型中包含参数名，以便文档说明。编译器会忽略这些名称，因此以下原型也有效：

```
int maximum(int, int, int);
```

### 编译错误

与函数原型不匹配的函数调用是编译错误。如果函数原型与函数定义不一致，也会出错。例如，在图 5.2 中，如果函数原型写成

```
void maximum(int x, int y, int z);
```

编译器将生成错误，因为函数原型的 void 返回类型与函数头中的 int 返回类型不同。

### 实参强制转换与“通常算术转换规则”

函数原型的另一个重要特性是实参强制转换，即隐式地将实参转换为适当类型。例如，即使 <math.h> 中的函数原型指定了 double 形参，用整数实参调用数学库函数 sqrt 仍然可行。以下语句会正确计算 sqrt(4) 并打印 2.000：

```
printf("%.3f\n", sqrt(4));
```

函数原型使编译器在将 int 值 4 传递给 sqrt 之前，把它的一个副本转换为 double 值 4.0。一般来说，与函数原型的形参类型不完全对应的实参值会在调用函数之前转换为适当类型。如果不遵循 C 的通常算术转换规则，这类转换可能导致错误结果。这些规则规定了如何在不丢失数据的情况下将值转换为其他类型。

在我们的 sqrt 示例中，int 可以自动转换为 double 而不改变其值——double 能表示的取值范围比 int 宽得多。然而，将 double 转换为 int 会截断 double 的小数部分，从而改变原值。将大整数类型转换为小整数类型（例如 long 转换为 short）也可能改变值。

### 混合类型表达式

通常算术转换规则由编译器处理。它们适用于混合类型表达式——即包含多种数据类型值的表达式。在此类表达式中，编译器会为需要转换的值创建临时副本，然后将这些副本转换为表达式中的“最高”类型——这称为提升。对于至少包含一个浮点值的混合类型表达式：

- 如果一个值是 long double，则其他值转换为 long double。
- 如果一个值是 double，则其他值转换为 double。
- 如果一个值是 float，则其他值转换为 float。

如果混合类型表达式仅包含整数类型，则通常算术转换会指定一组整数提升规则。

C 标准文档第 6.3.1 节详细规定了算术操作数和通常算术转换规则的完整细节。下表列出了浮点类型和整数类型，以及每种类型的 `printf` 和 `scanf` 转换规范。在大多数情况下，下表中位置较低的整数类型会转换为较高类型：

| 数据类型 | `printf` 转换规范 | `scanf` 转换规范 |
|---|---|---|
| *浮点类型* |  |  |
| long double | `%Lf` | `%Lf` |
| double | `%f` | `%lf` |
| float | `%f` | `%f` |
| *整数类型* |  |  |
| unsigned long long int | `%llu` | `%llu` |
| long long int | `%lld` | `%lld` |
| unsigned long int | `%lu` | `%lu` |
| long int | `%ld` | `%ld` |
| unsigned int | `%u` | `%u` |
| int | `%d` | `%d` |
| unsigned short | `%hu` | `%hu` |
| short | `%hd` | `%hd` |
| char | `%c` | `%c` |

值只能通过显式地将值赋给较低类型的变量，或使用强制类型转换运算符，才能转换为较低类型。实参会转换为函数原型中指定的形参类型，就像这些实参被赋给这些类型的变量一样。因此，如果我们向图 5.1 中的 square 函数传递一个 double，该 double 会被转换为 `int`（较低类型），而 square 通常会返回错误的值。例如，`square(4.5)` 返回 16，而不是 20.25。

在提升层次中从较高数据类型转换为较低类型可能会改变数据值。许多编译器在这种情况下会发出警告。
