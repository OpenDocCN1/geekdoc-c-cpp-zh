
also generates a compile-time error since the assignment to n in the anonymous function has no effect on the definite assignment state of n outside the anonymous function. end example]

## 10.5 变量引用

变量引用是一个被归类为变量的表达式。变量引用表示一个存储位置，可以同时访问以获取当前值并存储新值。

```
variable-reference:
    expression
```

> [注意：在 C 和 C++ 中，变量引用被称为左值。end note]

## 10.6 变量引用的原子性

以下数据类型的读取和写入应是原子的：bool、char、byte、sbyte、short、ushort、uint、int、float 以及引用类型。此外，具有前述列表中底层类型的枚举类型的读取和写入也应是原子的。其他类型的读取和写入，包括 long、ulong、double 和 decimal 以及用户定义的类型，无需是原子的。除为此目的设计的库函数外，读-改-写操作的原子性不予保证，例如增量或减量的情况。

## 11. 转换

## 11.1 通用

转换会导致表达式被转换为特定类型，或被视为特定类型；在前一种情况下，转换可能涉及表示形式的更改。转换可以是隐式的或显式的，这决定了是否需要显式转换。[示例：例如，从类型 int 到类型 long 的转换是隐式的，因此 int 类型的表达式可以隐式地被视为 long 类型。相反的转换，从 long 类型到 int 类型是显式的，因此需要显式转换。

```
int a = 123;
long b = a;    // implicit conversion from int to long
int c = (int) b; // explicit conversion from long to int
```

end example] 一些转换由语言定义。程序也可以定义自己的转换 (§11.5)。

语言中的一些转换是从表达式到类型定义的，其他的是从类型到类型定义的。从类型进行的转换适用于所有具有该类型的表达式。[示例：

```
enum Color { Red, Blue, Green }
color c0 = 0; // The expression 0 converts implicitly to enum types
color c1 = (Color)1; // other int expressions need explicit conversion
string x = null; // Conversion from null expression (no type) to String
Func<int, int> square = x => x * x; // Conversion from lambda expression to delegate type
```

end example]

## 11.2 隐式转换

## 11.2.1 通用

以下转换被归类为隐式转换：

- 标识转换
- 隐式数值转换
- 隐式枚举转换
- 隐式引用转换
- 装箱转换
- 隐式动态转换
- 隐式类型参数转换
- 隐式常量表达式转换
- 用户定义的隐式转换
- 匿名函数转换
- 方法组转换
- 空字面量转换
- 隐式可空转换
- 提升的用户定义隐式转换

隐式转换可以在多种情况下发生，包括函数成员调用 (§12.6.6)、转换表达式 (§12.8.7) 和赋值 (§12.18)。

预定义的隐式转换总是成功，并且永远不会引发异常。[注意：设计良好的用户定义的隐式转换也应表现出这些特性。end note]

对于转换而言，类型 object 和 dynamic 被视为等价。

然而，动态转换 (§11.2.9 和 §11.3.7) 仅适用于类型为 dynamic 的表达式 (§9.2.4)。

### 11.2.2 标识转换

标识转换将任意类型转换为同一类型。此转换存在的一个原因是，可以说类型 T 或类型为 T 的表达式可转换为其自身。

由于 object 和 dynamic 被视为等价，因此 object 与 dynamic 之间存在标识转换，并且在将 dynamic 的所有出现替换为 object 后相同的构造类型之间也存在标识转换。

在大多数情况下，标识转换在运行时没有效果。然而，由于浮点运算可能以高于其类型规定的精度执行 (§9.3.7)，对其结果的赋值可能导致精度损失，而显式转换保证将精度降低到类型规定的精度。

### 11.2.3 隐式数值转换

隐式数值转换如下：

- 从 sbyte 到 short、int、long、float、double 或 decimal。
- 从 byte 到 short、ushort、int、uint、long、ulong、float、double 或 decimal。
- 从 short 到 int、long、float、double 或 decimal。
- 从 ushort 到 int、uint、long、ulong、float、double 或 decimal。
- 从 int 到 long、float、double 或 decimal。
- 从 uint 到 long、ulong、float、double 或 decimal。
- 从 long 到 float、double 或 decimal。
- 从 ulong 到 float、double 或 decimal。
- 从 char 到 ushort、int、uint、long、ulong、float、double 或 decimal。
- 从 float 到 double。

从 int、uint、long 或 ulong 到 float 的转换以及从 long 或 ulong 到 double 的转换可能会导致精度损失，但永远不会导致量级损失。其他隐式数值转换永远不会丢失任何信息。

没有预定义的到 char 类型的隐式转换，因此其他整型的值不会自动转换为 char 类型。

### 11.2.4 隐式枚举转换

隐式枚举转换允许十进制整数字面量 0（或 0L 等）转换为任何枚举类型以及底层类型为枚举类型的任何可空值类型。在后一种情况下，转换通过转换为底层枚举类型并包装结果来求值 (§9.3.11)。

### 11.2.5 隐式可空转换

隐式可空转换是源自隐式预定义转换的可空转换 (§11.6.1)。

### 11.2.6 空字面量转换

从空字面量到任何引用类型或可空值类型存在隐式转换。如果目标类型是引用类型，则此转换产生空引用，或给定可空值类型的空值 (§9.3.11)。

### 11.2.7 隐式引用转换

隐式引用转换如下：

- 从任何引用类型到 object 和 dynamic。
- 从任何类类型 S 到任何类类型 T，前提是 S 派生自 T。
- 从任何类类型 S 到任何接口类型 T，前提是 S 实现 T。
- 从任何接口类型 S 到任何接口类型 T，前提是 S 派生自 T。
- 从元素类型为 S_E 的任何数组类型 S 到元素类型为 T_E 的数组类型 T，前提是以下所有条件都为真：
  - S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同数量的维度。
  - 从 S_E 到 T_E 存在隐式引用转换。
- 从单维数组类型 S[] 到 System.Collections.Generic.IList<T>、System.Collections.Generic.IReadOnlyList<T> 及其基接口，前提是从 S 到 T 存在隐式标识或引用转换。
- 从任何数组类型到 System.Array 及其实现的接口。
- 从任何委托类型到 System.Delegate 及其实现的接口。
- 从空字面量 (§7.4.5.7) 到任何引用类型。
- 从任何引用类型到引用类型 T，如果它具有到引用类型 T0 的隐式标识或引用转换，并且 T0 具有到 T 的标识转换。
- 从任何引用类型到接口或委托类型 T，如果它具有到接口或委托类型 T0 的隐式标识或引用转换，并且 T0 可方差转换为 (§18.2.3.3) T。
- 涉及已知为引用类型的类型参数的隐式转换。有关涉及类型参数的隐式转换的更多详细信息，请参阅 §11.2.11。

隐式引用转换是可在编译时证明总是成功的引用类型之间的转换，因此在运行时不需要检查。

引用转换，无论是隐式还是显式，从不改变被转换对象的引用标识。[注意：换句话说，虽然引用转换可以更改引用的类型，但它永远不会更改所引用对象的类型或值。end note]

### 11.2.8 装箱转换

装箱转换允许值类型隐式转换为引用类型。以下装箱转换存在：

- 从任何值类型到类型 object。
- 从任何值类型到类型 System.ValueType。
- 从任何枚举类型到类型 System.Enum。
- 从任何非可空值类型到该非可空值类型实现的任何接口类型。
- 从任何非可空值类型到接口类型 I，前提是从该非可空值类型到另一个接口类型 I0 存在装箱转换，并且 I0 具有到 I 的标识转换。
- 从任何非可空值类型到接口类型 I，前提是从该非可空值类型到另一个接口类型 I0 存在装箱转换，并且 I0 可方差转换为 (§18.2.3.3) I。
- 从任何可空值类型到任何引用类型，前提是从该可空值类型的底层类型到该引用类型存在装箱转换。
- 从已知不是引用类型的类型参数到任何类型，前提是转换由 §11.2.11 允许。

对非可空值类型的值进行装箱包括分配一个对象实例并将值复制到该实例中。

对可空值类型的值进行装箱，如果它是空值（HasValue 为 false），则产生空引用，否则产生解包并装箱底层值的结果。

[注意：装箱过程可以想象为每个值类型都存在一个装箱类。例如，考虑一个实现接口 I 的结构体 S，其装箱类名为 S_Boxing。]
