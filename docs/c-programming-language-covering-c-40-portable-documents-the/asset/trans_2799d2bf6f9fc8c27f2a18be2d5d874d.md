
非隐式转换的显式转换是指无法证明总是会成功的转换、已知可能丢失信息的转换，以及跨越类型域足够不同以至于需要显式表示法的转换。

## 6.2.1 显式数值转换

显式数值转换是从一种数值类型到另一种数值类型的转换，对于这些转换，隐式数值转换 (§6.1.2) 并不存在：

- 从 sbyte 到 byte、ushort、uint、ulong 或 char。
- 从 byte 到 sbyte 和 char。
- 从 short 到 sbyte、byte、ushort、uint、ulong 或 char。
- 从 ushort 到 sbyte、byte、short 或 char。
- 从 int 到 sbyte、byte、short、ushort、uint、ulong 或 char。
- 从 uint 到 sbyte、byte、short、ushort、int 或 char。
- 从 long 到 sbyte、byte、short、ushort、int、uint、ulong 或 char。
- 从 ulong 到 sbyte、byte、short、ushort、int、uint、long 或 char。
- 从 char 到 sbyte、byte 或 short。
- 从 float 到 sbyte、byte、short、ushort、int、uint、long、ulong、char 或 decimal。
- 从 double 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 decimal。
- 从 decimal 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 double。

由于显式转换包括所有隐式和显式数值转换，因此始终可以使用强制转换表达式 (§7.7.6) 将任何数值类型转换为任何其他数值类型。

显式数值转换可能丢失信息或可能引发异常。显式数值转换的处理如下：

- 对于从一种整型到另一种整型的转换，处理取决于转换发生的溢出检查上下文 (§7.6.12)：
  - 在已检查上下文中，如果源操作数的值在目标类型的范围内，则转换成功，但如果源操作数的值超出目标类型的范围，则会抛出 System.OverflowException。
  - 在未检查上下文中，转换总是成功，并按如下方式进行：
    - 如果源类型大于目标类型，则源值通过丢弃其“extra”最显著位来截断。然后将结果视为目标类型的值。
    - 如果源类型小于目标类型，则源值会被符号扩展或零扩展，使其与目标类型大小相同。如果源类型是有符号的，则使用符号扩展；如果源类型是无符号的，则使用零扩展。然后将结果视为目标类型的值。
    - 如果源类型与目标类型大小相同，则源值被视为目标类型的值。
- 对于从 decimal 到整型的转换，源值向零舍入到最接近的整数值，此整数值成为转换的结果。如果所得整数值超出目标类型的范围，则会抛出 System.OverflowException。
- 对于从 float 或 double 到整型的转换，处理取决于转换发生的溢出检查上下文 (§7.6.12)：
  - 在已检查上下文中，转换按如下方式进行：
    - 如果操作数的值为 NaN 或无穷大，则会抛出 System.OverflowException。
    - 否则，源操作数向零舍入到最接近的整数值。如果此整数值在目标类型的范围内，则此值是转换的结果。
    - 否则，会抛出 System.OverflowException。
  - 在未检查上下文中，转换总是成功，并按如下方式进行：
    - 如果操作数的值为 NaN 或无穷大，则转换的结果是目标类型的未指定值。
    - 否则，源操作数向零舍入到最接近的整数值。如果此整数值在目标类型的范围内，则此值是转换的结果。
    - 否则，转换的结果是目标类型的未指定值。
- 对于从 double 到 float 的转换，double 值被舍入为最接近的 float 值。如果 double 值太小而无法表示为 float，则结果变为正零或负零。如果 double 值太大而无法表示为 float，则结果变为正无穷大或负无穷大。如果 double 值为 NaN，则结果也是 NaN。
- 对于从 float 或 double 到 decimal 的转换，源值被转换为十进制表示，并在需要时舍入到第 28 位小数之后的最接近数字 (§4.1.7)。如果源值太小而无法表示为 decimal，则结果变为零。如果源值为 NaN、无穷大或太大而无法表示为 decimal，则会抛出 System.OverflowException。
- 对于从 decimal 到 float 或 double 的转换，decimal 值被舍入为最接近的 double 或 float 值。虽然此转换可能会丢失精度，但它永远不会导致异常被抛出。

> **JOSEPH ALBAHARI** 实数到整数转换中的向零舍入行为是高效的，但并不总是更有用的方法。例如，在此方案下，(int) 3.9 的计算结果为 3，而不是 4。C# 没有内置的转换为最接近整数的机制；此功能留给外部库。在 Microsoft 的 .NET Framework 中，静态 Convert 类通过诸如 ToInt32 之类的方法提供此功能。

## 6.2.2 显式枚举转换

显式枚举转换是：

- 从 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal 到任何 enum-type。
- 从任何 enum-type 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal。
- 从任何 enum-type 到任何其他 enum-type。

两个类型之间的显式枚举转换是通过将参与的任何 enum-type 视为该 enum-type 的基础类型，然后在所得类型之间执行隐式或显式数值转换来处理的。例如，给定基础类型为 int 的 enum-type E，从 E 到 byte 的转换被处理为从 int 到 byte 的显式数值转换 (§6.2.1)，而从 byte 到 E 的转换被处理为从 byte 到 int 的隐式数值转换 (§6.1.2)。

## 6.2.3 显式可空转换

显式可空转换允许在非可空值类型上操作的预定义显式转换也与这些类型的可空形式一起使用。对于将非可空值类型 S 转换为非可空值类型 T 的每个预定义显式转换 (§6.1.1、§6.1.2、§6.1.3、§6.2.1 和 §6.2.2)，存在以下可空转换：

- 从 S? 到 T? 的显式转换。
- 从 S 到 T? 的显式转换。
- 从 S? 到 T 的显式转换。

基于从 S 到 T 的底层转换的可空转换的求值如下进行：

- 如果可空转换是从 S? 到 T?：如果源值为 null（HasValue 属性为 false），则结果是类型 T? 的 null 值。否则，转换被求值为空包从 S? 到 S，然后是 S 到 T 的底层转换，然后是从 T 到 T? 的包装。
- 如果可空转换是从 S 到 T?，则转换被求值 S 到 T 的底层转换，然后是从 T 到 T? 的包装。
- 如果可空转换是从 S? 到 T，则转换被求值为空包从 S? 到 S，然后是 S 到 T 的底层转换。

请注意，尝试解包可空值如果该值为 null 将会抛出异常。

## 6.2.4 显式引用转换

显式引用转换是：

- 从 object 和 dynamic 到任何其他引用类型。
- 从任何类类型 S 到任何类类型 T，前提是 S 是 T 的基类。
- 从任何类类型 S 到任何接口类型 T，前提是 S 未被密封并且 S 未实现 T。
- 从任何接口类型 S 到任何类类型 T，前提是 T 未被密封或 T 实现了 S。
- 从任何接口类型 S 到任何接口类型 T，前提是 S 未派生自 T。
- 从元素类型为 S₁ 的数组类型 S 到元素类型为 T₁ 的数组类型 T，前提是以下所有条件为真：
  - S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同的维度数。
  - S₁ 和 T₁ 都是引用类型。
  - 从 S₁ 到 T₁ 存在显式引用转换。
