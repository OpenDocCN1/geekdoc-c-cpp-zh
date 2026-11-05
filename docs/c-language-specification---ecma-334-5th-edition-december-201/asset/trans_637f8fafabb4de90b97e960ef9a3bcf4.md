
## 11.3.2 显式数值转换

显式数值转换是从一种数值类型到另一种数值类型，而隐式数值转换 (§11.2.3) 并不已存在的转换：

- 从 sbyte 到 byte、ushort、uint、ulong 或 char。
- 从 byte 到 sbyte 或 char。
- 从 short 到 sbyte、byte、ushort、uint、ulong 或 char。
- 从 ushort 到 sbyte、byte、short 或 char。
- 从 int 到 sbyte、byte、short、ushort、uint、ulong 或 char。
- 从 uint 到 sbyte、byte、short、ushort、int 或 char。
- 从 long 到 sbyte、byte、short、ushort、int、uint、ulong 或 char。
- 从 ulong 到 sbyte、byte、short、ushort、int、uint、long 或 char。
- 从 char 到 sbyte、byte 或 short。
- 从 float 到 sbyte、byte、short、ushort、int、uint、long、ulong、char 或 decimal。
- 从 double 到 sbyte、byte、short、ushort、int、uint、long、ulong、char 或 decimal。
- 从 decimal 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 double。

因为显式转换包括所有隐式和显式数值转换，所以始终可以使用强制转换表达式 (§12.8.7) 将任何数值类型转换为任何其他数值类型。

显式数值转换可能会丢失信息或可能导致抛出异常。显式数值转换的处理如下：

- 对于从一种整型到另一种整型的转换，处理取决于转换发生的溢出检查上下文 (§12.7.14)：
  - 在有检查的上下文中，如果源操作数的值在目标类型的范围内，则转换成功；但如果源操作数的值超出目标类型的范围，则抛出 System.OverflowException。
  - 在无检查的上下文中，转换总是成功，并按如下方式进行。
    - 如果源类型大于目标类型，则通过丢弃其“额外”的最显著位来截断源值。然后将结果视为目标类型的值。
    - 如果源类型小于目标类型，则源值会被符号扩展或零扩展，使其与目标类型大小相同。如果源类型是有符号的，则使用符号扩展；如果源类型是无符号的，则使用零扩展。然后将结果视为目标类型的值。
    - 如果源类型与目标类型大小相同，则源值被视为目标类型的值。
- 对于从 decimal 到整型的转换，源值会向零舍入到最近的整数值，并且该整数值成为转换的结果。如果所得整数值超出目标类型的范围，则抛出 System.OverflowException。
- 对于从 float 或 double 到整型的转换，处理取决于转换发生的溢出检查上下文 (§12.7.14)：
  - 在有检查的上下文中，转换按如下方式进行：
    - 如果操作数的值为 NaN 或无穷大，则抛出 System.OverflowException。
    - 否则，源操作数会向零舍入到最近的整数值。如果该整数值在目标类型的范围内，则该值是转换的结果。
  - 否则，抛出 System.OverflowException。
  - 在无检查的上下文中，转换总是成功，并按如下方式进行。
    - 如果操作数的值为 NaN 或无穷大，则转换的结果是目标类型的未指定值。
    - 否则，源操作数会向零舍入到最近的整数值。如果该整数值在目标类型的范围内，则该值是转换的结果。
    - 否则，转换的结果是目标类型的未指定值。
- 对于从 double 到 float 的转换，double 值会舍入到最近的 float 值。如果 double 值太小而无法表示为 float，则结果变为与该值符号相同的零。如果 double 值的大小太大而无法表示为 float，则结果变为与该值符号相同的无穷大。如果 double 值为 NaN，则结果也是 NaN。
- 对于从 float 或 double 到 decimal 的转换，源值会转换为 decimal 表示，并在需要时舍入到最接近的数字 (§9.3.8)。
  - 如果源值太小而无法表示为 decimal，则结果变为零，如果 decimal 支持有符号零值，则保留原始值的符号。
  - 如果源值的大小太大而无法表示为 decimal，或该值为无穷大，则结果为保留原始值符号的无穷大，如果 decimal 表示支持无穷大；否则抛出 System.OverflowException。
  - 如果源值为 NaN，则如果 decimal 表示支持 NaN，则结果为 NaN；否则抛出 System.OverflowException。
- 对于从 decimal 到 float 或 double 的转换，decimal 值会舍入到最近的 double 或 float 值。如果源值的大小太大而无法在目标类型中表示，或该值为无穷大，则结果为保留原始值符号的无穷大。如果源值为 NaN，则结果为 NaN。虽然此转换可能会丢失精度，但永远不会导致抛出异常。

[Note: decimal 类型不需要支持无穷大或 NaN 值，但可以支持；其范围可能小于 float 和 double 的范围，但并非 guaranteed。对于没有无穷大或 NaN 值且范围小于 float 的 decimal 表示，从 decimal 到 float 或 double 的转换结果永远不会是无穷大或 NaN。end note]

## 11.3.3 显式枚举转换

显式枚举转换是：

- 从 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal 到任何枚举类型。
- 从任何枚举类型到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal。
- 从任何枚举类型到任何其他枚举类型。

两个类型之间的显式枚举转换通过将参与的任何枚举类型视为该枚举类型的底层类型，然后在所得类型之间执行隐式或显式数值转换来处理。[Example: 给定底层类型为 int 的枚举类型 E，从 E 到 byte 的转换被处理为从 int 到 byte 的显式数值转换 (§11.3.2)，而从 byte 到 E 的转换被处理为从 byte 到 int 的隐式数值转换 (§11.2.3)。end example]

## 11.3.4 显式可空转换

显式可空转换是那些源自显式和隐式预定义转换的可空转换 (§11.6.1)。

## 11.3.5 显式引用转换

显式引用转换是：

- 从 object 和 dynamic 到任何其他引用类型。
- 从任何类类型 S 到任何类类型 T，前提是 S 是 T 的基类。
- 从任何类类型 S 到任何接口类型 T，前提是 S 未被密封并且 S 未实现 T。
- 从任何接口类型 S 到任何类类型 T，前提是 T 未被密封或 T 实现了 S。
- 从任何接口类型 S 到任何接口类型 T，前提是 S 未派生自 T。
- 从元素类型为 Se 的数组类型 S 到元素类型为 Te 的数组类型 T，前提是以下所有条件都为真：
  - S 和 T 仅在元素类型上不同。换句话说，S 和 T 具有相同的维度数。
  - 从 Se 到 Te 存在显式引用转换。
- 从 System.Array 及其实现的接口到任何数组类型。
- 从单维数组类型 S[] 到 System.Collections.Generic.IList<T>、System.Collections.Generic.IReadOnlyList<T> 及其基接口，前提是存在从 S 到 T 的恒等转换或显式引用转换。
- 从 System.Collections.Generic.IList<S>、System.Collections.Generic.IReadOnlyList<S> 及其基接口到单维数组类型 T[]，前提是存在从 S 到 T 的恒等转换或显式引用转换。
- 从 System.Delegate 及其实现的接口到任何委托类型。
- 从引用类型 S 到引用类型 T，如果它从 S 到引用类型 T0 存在显式引用转换，并且从 T0 到 T 存在显式引用转换，并且存在从 T0 到 T 的恒等转换。
- 从引用类型 S 到接口或委托类型 T，如果存在从 S 到接口或委托类型 T0 的显式引用转换，并且 T0 可以方差转换为 T 或 T 可以方差转换为 T0 (§18.2.3)。
- 从 D<S1...Sn> 到 D<T1...Tn>，其中 D<X1...Xn> 是泛型委托类型，D<S1...Sn> 与 D<T1...Tn> 不兼容或不相同，并且对于 D 的每个类型参数 Xi 均满足以下条件：
  - 如果 Xi 是不变的，则 Si 与 Ti 相同。
  - 如果 Xi 是协变的，则存在从 Si 到 Ti 的恒等转换、隐式引用转换或显式引用转换。
  - 如果 Xi 是逆变的，则 Si 和 Ti 相同或均为引用类型。
- 涉及已知为引用类型的类型参数的显式转换。有关涉及类型参数的显式转换的更多详细信息，请参阅 §11.3.8。

显式引用转换是那些在运行时需要检查以确保其正确性的引用类型之间的转换。

要使显式引用转换在运行时成功，源操作数的值应为 null，或者源操作数引用的对象的类型应为可通过隐式引用转换 (§11.2.7) 转换为目标类型的类型。如果显式引用转换失败，则抛出 System.InvalidCastException。

引用转换，无论是隐式还是显式，从不改变正在转换的对象的引用同一性。[Note: 换句话说，虽然引用转换可以改变引用的类型，但它永远不会改变所引用对象的类型或值。end note]
