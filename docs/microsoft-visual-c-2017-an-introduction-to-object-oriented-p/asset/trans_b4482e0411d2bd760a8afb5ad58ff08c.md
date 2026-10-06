
false。在第二个语句中，`annualIncome` 变量必须大于 100000，该表达式才为真。

在第 4 章学习了如何在 C# 程序中进行决策后，布尔变量将变得更有用。

当你调用 `write()` 或 `WriteLine()` 显示 `bool` 变量的值时，显示的值会被大写为 True 或 False。然而，程序内部的值是小写的：true 或 false。

## 两个真理一假

### 使用 bool 数据类型

- 1. 如果 `rate` 为 7.5 且 `min` 为 7，那么 `rate >= min` 的值为 false。
- 2. 如果 `rate` 为 7.5 且 `min` 为 7，那么 `rate < min` 的值为 false。
- 3. 如果 `rate` 为 7.5 且 `min` 为 7，那么 `rate == min` 的值为 false。

```
min=true;
```
错误的语句是 #1。如果 `rate` 为 7.5 且 `min` 为 7，那么 `rate == true` 的值为 false。如果 `rate` 为 7.5 且 `min` 为 7，那么 `rate == min` 的值为 false。

## 你来操作

操作布尔变量
接下来你将编写一个程序来演示布尔变量是如何工作的。

- 1. 在编辑器中打开一个新文件，并将其命名为 DemoVariables.cs。
- 2. 输入以下代码。在 `Main()` 方法中，你声明了一个整数值，然后给布尔变量分配了不同的值。注意，当你声明 `value` 和 `isSixMore` 时，你分配了类型。当你稍后在程序中为这些变量重新赋值时，不需要使用类型名称重新声明。相反，你为已声明的变量分配新值。

## 理解数值类型转换

```
using static System.Console;
class DemoVariables3
{
    static void Main()
    {
        int comparisonValue = 4;
        bool isSixMore = 6 > comparisonValue;
        WriteLine("comparisonValue is {0}, isSixMore is {1}", comparisonValue, isSixMore);
        comparisonValue = 35;
        isSixMore = 6 > comparisonValue;
        WriteLine("comparisonValue is {0}, isSixMore is {1}", comparisonValue, isSixMore);
    }
}
```

- 3. 保存、编译并运行程序。输出结果如图 2-12所示。

| 输出 |
| :--- |
| comparisonValue is 4, isSixMore is True |
| comparisonValue is 35, isSixMore is False |

**图 2-12** DemoVariables3 程序的输出

- 4. 在初始化语句和后面的赋值语句中，将名为 `comparisonValue` 的变量更改为你选择的任何值。尝试预测输出，然后运行程序以确认你的预测。至少在一个位置处将 `comparisonValue` 改为 6 以预测结果并再次运行程序。

当你对相同类型的变量或常量进行算术运算时，运算结果将保留其类型。例如，当除两个 `int` 时，结果是 `int`；当相减两个 `double` 时，结果是 `double`。然而，你需要在不同类型之间执行数学运算。例如，在下面的代码中，你可以将一个 `int` 乘以一个 `double`：

```
int hoursWorked = 36;
double payRate = 12.35;
double grossPay = hoursWorked * payRate;
```

## 第 2 章 使用数据

当你对不同类型的操作数进行算术运算时，C# 会为结果选择一个**统一类型**（unifying type），并**隐式地**（自动）将不符合的操作数转换为统一类型，即具有**更高优先级**的类型。这种转换被称为**隐式转换**或**隐式转换**——即当值赋值给优先级更高的类型时发生的自动转换。

隐式数值转换包括：

- sbyte 转换为 short, int, long, float, double 或 decimal
- byte 转换为 short, ushort, int, uint, long, float, double 或 decimal
- short 转换为 int, long, float, double 或 decimal
- ushort 转换为 int, uint, ulong, float, double 或 decimal
- int 转换为 long, float, double 或 decimal
- uint 转换为 long, ulong, float, double 或 decimal
- long 转换为 float, double 或 decimal
- ulong 转换为 float, double 或 decimal
- char 转换为 ushort, int, uint, ulong, float, double 或 decimal
- float 转换为 double

隐式转换也发生在简单赋值和计算中。例如，如果 *money* 被声明为 *double*，那么以下语句隐式地将整数 15 转换为 *double*：

```
money = 15;
```

> 从 int、uint 或 long 转换为 float，以及从 long 转换为 double 可能会导致精度损失，但永远不会导致数量损失。

> int 类型的常量表达式（例如 25）可以转换为 sbyte, short, ushort, int 或 long。例如，sbyte age = 19; 这将 int 分配给 sbyte 是合法的。然而，你必须确保赋值的值在目标类型的允许范围内，否则程序将无法编译。例如，sbyte age = 200; 是不合法的，因为 sbyte 的最大值为 127。

例如，当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。

当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。

当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。

当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。

当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。

当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。

当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。

当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。

当你将一个 **int** 乘以一个 **double** 时，结果是 **double**。
