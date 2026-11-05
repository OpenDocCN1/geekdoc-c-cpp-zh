
-   否则，如果 expr_cond 是常量表达式 (§11.20) 且值为 false，则 expr 之后 v 的状态与 expr_false 之后 v 的状态相同。
-   否则，如果 expr_true 之后 v 的状态是已明确赋值且 expr_false 之后 v 的状态是已明确赋值，则 expr 之后 v 的状态是已明确赋值。
-   否则，expr 之后 v 的状态不是已明确赋值。

### 9.4.4.31 匿名函数

对于具有主体（块或表达式）body 的 lambda_expression 或 anonymous_method_expression expr：

-   参数的明确赋值状态与命名方法 (§9.2.6, §9.2.7) 的参数相同。
-   匿名函数主体执行前外部变量 v 的明确赋值状态与 expr 之前 v 的状态相同。也就是说，外部变量的明确赋值状态从匿名函数的上下文继承而来。
-   expr 之后外部变量 v 的明确赋值状态与 expr 之前 v 的状态相同。

示例：示例

```
delegate bool Filter(int i);
void F()
{
    int max;
    // Error, max is not definitely assigned
    Filter f = (int n) => n < max;
    max = 5;
    DoWork(f);
}
```

生成编译时错误，因为在匿名函数声明处 max 未明确赋值。

end example

示例：示例

```
delegate void D();
void F()
{
    int n;
    D d = () => { n = 1; };
    d();
    // Error, n is not definitely assigned
    Console.WriteLine(n);
}
```

也生成编译时错误，因为匿名函数中对 n 的赋值对匿名函数外部 n 的明确赋值状态没有影响。

end example

### 9.5 变量引用

variable_reference 是被归类为变量的表达式。variable_reference 表示一个存储位置，可以同时访问以获取当前值并存储新值。

```
variable_reference
    : expression
    ;
```

注意：在 C 和 C++ 中，variable_reference 被称为左值。 end note

### 9.6 变量引用的原子性

以下数据类型的读写应为原子操作：bool、char、byte、sbyte、short、ushort、uint、int、float 以及引用类型。此外，具有前述列表中底层类型的枚举类型的读写也应为原子操作。其他类型的读写，包括 long、ulong、double 和 decimal，以及用户定义的类型，不必是原子的。除了为此目的而设计的库函数外，不保证原子读写修改，例如在递增或递减的情况下。

## 10. 转换

### 10.1 通用

**转换** 会导致表达式被转换为特定类型，或被视为特定类型；在前一种情况下，转换可能涉及表示形式的更改。转换可以是 **隐式** 或 **显式**，这决定是否需要显式强制转换。

示例：例如，从类型 `int` 到类型 `long` 的转换是隐式的，因此 `int` 类型的表达式可以隐式地视为 `long` 类型。相反的转换，从类型 `long` 到类型 `int`，是显式的，因此需要显式强制转换。

```
int a = 123;
long b = a;    // implicit conversion from int to long
int c = (int) b; // explicit conversion from long to int
```

end example

一些转换由语言定义。程序也可以定义自己的转换 (§10.5)。

语言中的一些转换是从表达式到类型定义，其他的是从类型到类型。类型转换适用于所有具有该类型的表达式。

示例：

```
enum Color { Red, Blue, Green }
Color c0 = 0;    // The expression 0 converts implicitly to enum types
Color c1 = (Color)1; // other int expressions need explicit conversion
String x = null;   // Conversion from null expression (no type) to String
Func<int, int> square = x => x * x; // Conversion from lambda expression to delegate type
```

end example

### 10.2 隐式转换

### 10.2.1 通用

以下转换被归类为隐式转换：

-   标识转换
-   隐式数值转换
-   隐式枚举转换
-   隐式插值字符串转换
-   隐式引用转换
-   装箱转换
-   隐式动态转换
-   隐式类型参数转换
-   隐式常量表达式转换
-   用户定义的隐式转换
-   匿名函数转换
-   方法组转换
-   空字面量转换
-   隐式可空转换
-   提升的用户定义隐式转换

隐式转换可以在多种情况下发生，包括函数成员调用 (§11.6.6)、强制转换表达式 (§11.8.7) 和赋值 (§11.18)。

预定义的隐式转换总是成功且永远不会引发异常。

> 注意：设计良好的用户定义隐式转换也应表现出这些特性。 end note

就转换而言，类型 object 和 dynamic 被视为等价。

然而，动态转换 (§10.2.10 和 §10.3.7) 仅适用于类型为 dynamic (§8.2.4) 的表达式。

### 10.2.2 标识转换

标识转换将任何类型转换为同一类型。存在此转换的一个原因是，可以说类型 T 或类型 T 的表达式可转换为其自身。

由于 object 和 dynamic 被视为等价，因此 object 与 dynamic 之间存在标识转换，以及在将 dynamic 的所有出现替换为 object 后相同的构造类型之间存在标识转换。

在大多数情况下，标识转换在运行时没有效果。然而，由于浮点运算可能以其类型规定的更高精度执行 (§8.3.7)，其结果的赋值可能导致精度损失，而显式强制转换保证将精度降低到类型规定的精度 (§11.8.7)。

### 10.2.3 隐式数值转换

隐式数值转换为：

-   从 sbyte 到 short、int、long、float、double 或 decimal。
-   从 byte 到 short、ushort、int、uint、long、ulong、float、double 或 decimal。
-   从 short 到 int、long、float、double 或 decimal。
-   从 ushort 到 int、uint、long、ulong、float、double 或 decimal。
-   从 int 到 long、float、double 或 decimal。
-   从 uint 到 long、ulong、float、double 或 decimal。
-   从 long 到 float、double 或 decimal。
-   从 ulong 到 float、double 或 decimal。
-   从 char 到 ushort、int、uint、long、ulong、float、double 或 decimal。
-   从 float 到 double。

从 int、uint、long 或 ulong 到 float 以及从 long 或 ulong 到 double 的转换可能导致精度损失，但永远不会导致幅度损失。其他隐式数值转换永远不会丢失任何信息。

没有预定义的隐式转换到 char 类型，因此其他整数类型的值不会自动转换为 char 类型。

### 10.2.4 隐式枚举转换

隐式枚举转换允许 *constant_expression* (§11.20) 具有任意整数类型且值为零，转换为任意 *enum_type* 以及底层类型为 *enum_type* 的任意 *nullable_value_type*。在后一种情况下，转换通过转换为底层 *enum_type* 并包装结果 (§8.3.11) 来求值。

### 10.2.5 隐式插值字符串转换

隐式插值字符串转换允许 *interpolated_string_expression* (§11.7.3) 转换为 `System.IFormattable` 或 `System.FormattableString`（实现了 `System.IFormattable`）。当应用此转换时，不会从插值字符串组成字符串值。相反，会创建 `System.FormattableString` 的实例，如 §11.7.3 进一步所述。

### 10.2.6 隐式可空转换

隐式可空转换是源自隐式预定义转换的那些可空转换 (§10.6.1)。

### 10.2.7 空字面量转换

存在从 null 字面量到任何引用类型或可空值类型的隐式转换。此转换如果目标类型是引用类型则产生 null 引用，或产生给定可空值类型的 null 值 (§8.3.11)。

### 10.2.8 隐式引用转换

隐式引用转换为：

-   从任何 *reference_type* 到 object 和 dynamic。
-   从任何 *class_type* S 到任何 *class_type* T，前提是 S 从 T 派生。
-   从任何 *class_type* S 到任何 *interface_type* T，前提是 S 实现 T。
-   从任何 *interface_type* S 到任何 *interface_type* T，前提是 S 从 T 派生。
-   从元素类型为 S_I 的 *array_type* S 到元素类型为 T_I 的 *array_type* T，前提是以下所有条件为真：
  -   S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同数量的维度。
  -   从 S_I 到 T_I 存在隐式引用转换。
