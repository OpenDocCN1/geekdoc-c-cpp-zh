
> *注意：* 对 `is` 运算符的右操作数的查找必须首先作为类型进行测试，然后作为可能跨多个标记的表达式。在操作数为表达式的情况下，模式表达式的优先级必须至少与 `shift_expression` 一样高。结束注释

The `is` 运算符在 §12.12.12 中描述，`as` 运算符在 §12.12.13 中描述。

`==`、`!=`、`<`、`>`、`<=` 和 `>=` 运算符是比较运算符。

如果 `default_literal` (§8.20) 用作 `<`、`>`、`<=` 或 `>=` 运算符的操作数，则会发生编译时错误。如果 `default_literal` 用作 `==` 或 `!=` 运算符的两个操作数，则会发生编译时错误。如果 `default_literal` 用作 `is` 或 `as` 运算符的左操作数，则会发生编译时错误。

如果比较运算符的操作数具有编译时类型 `dynamic`，则该表达式是动态绑定的 (§12.3.3)。在这种情况下，表达式的编译时类型为 `dynamic`，下面描述的解析将在运行时使用具有编译时类型 `dynamic` 的那些操作数的运行时类型进行。

对于形式为 `x «op» y` 的操作，其中 «op» 是比较运算符，将应用重载解析 (§12.4.5) 来选择特定的运算符实现。操作数将被转换为所选运算符的参数类型，结果的类型为运算符的返回类型。如果 `equality_expression` 的两个操作数都是 `null` 字面量，则不执行重载解析，并且表达式根据运算符是 `==` 还是 `!=` 求值为 `true` 或 `false` 的常量值。

预定义的比较运算符在以下小节中描述。所有预定义的比较运算符都返回 `bool` 类型的结果，如下表所述。

| 操作 | 结果 |
| --- | --- |
| x == y | 若 x 等于 y 则为 true，否则为 false |
| x != y | 若 x 不等于 y 则为 true，否则为 false |
| x < y | 若 x 小于 y 则为 true，否则为 false |
| x > y | 若 x 大于 y 则为 true，否则为 false |
| x <= y | 若 x 小于或等于 y 则为 true，否则为 false |
| x >= y | 若 x 大于或等于 y 则为 true，否则为 false |

### 12.12.2 整数比较运算符

预定义的整数比较运算符为：

```csharp
bool operator ==(int x, int y);
bool operator ==(uint x, uint y);
bool operator ==(long x, long y);
bool operator ==(ulong x, ulong y);

bool operator !=(int x, int y);
bool operator !=(uint x, uint y);
bool operator !=(long x, long y);
bool operator !=(ulong x, ulong y);

bool operator <(int x, int y);
bool operator <(uint x, uint y);
bool operator <(long x, long y);
bool operator <(ulong x, ulong y);
bool operator >(int x, int y);
bool operator >(uint x, uint y);
bool operator >(long x, long y);
bool operator >(ulong x, ulong y);
bool operator <=(int x, int y);
bool operator <=(uint x, uint y);
bool operator <=(long x, long y);
bool operator <=(ulong x, ulong y);
bool operator >=(int x, int y);
bool operator >=(uint x, uint y);
bool operator >=(long x, long y);
bool operator >=(ulong x, ulong y);
```

这些运算符中的每一个都比较两个整数操作数的数值，并返回一个 `bool` 值，指示特定关系是否为真或假。

上述未提升的预定义整数比较运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.12.3 浮点比较运算符

预定义的浮点比较运算符为：

```csharp
bool operator ==(float x, float y);
bool operator ==(double x, double y);
bool operator !=(float x, float y);
bool operator !=(double x, double y);
bool operator <(float x, float y);
bool operator <(double x, double y);
bool operator >(float x, float y);
bool operator >(double x, double y);
bool operator <=(float x, float y);
bool operator <=(double x, double y);
bool operator >=(float x, float y);
bool operator >=(double x, double y);
```

运算符根据 IEC 60559 标准规则比较操作数：

如果任一操作数为 NaN，则除 `!=` 外所有运算符的结果均为 false，而 `!=` 的结果为 true。对于任意两个操作数，`x != y` 始终产生与 `!(x == y)` 相同的结果。然而，当一个或两个操作数为 NaN 时，`<`、`>`、`<=` 和 `>=` 运算符不会产生与相反运算符的逻辑否定相同的结果。

示例：如果 `x` 和 `y` 中任一为 NaN，则 `x < y` 为 false，但 `!(x >= y)` 为 true。结束示例

当两个操作数都不是 NaN 时，运算符根据以下顺序比较两个浮点操作数的值

```
-∞ < -max < ... < -min < -0.0 == +0.0 < +min < ... < +max < +∞
```

其中 `min` 和 `max` 是在给定浮点格式中可以表示的最小和最大正有限值。此顺序的显著影响包括：

- 负零和正零被视为相等。
- 负无穷被视为小于所有其他值，但等于另一个负无穷。
- 正无穷被视为大于所有其他值，但等于另一个正无穷。

上述未提升的预定义浮点比较运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.12.4 十进制比较运算符

预定义的十进制比较运算符为：

```csharp
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

这些运算符中的每一个都比较两个十进制操作数的数值，并返回一个 `bool` 值，指示特定关系是否为 `true` 或 `false`。每个十进制比较等价于使用类型为 `System.Decimal` 的相应关系或相等运算符。

上述未提升的预定义十进制比较运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.12.5 布尔相等运算符

预定义的布尔相等运算符为：

```csharp
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

`==` 的结果为 `true`，如果 `x` 和 `y` 均为 `true`，或 `x` 和 `y` 均为 `false`。否则，结果为 `false`。

`!=` 的结果为 `false`，如果 `x` 和 `y` 均为 `true`，或 `x` 和 `y` 均为 `false`。否则，结果为 `true`。当操作数为 `bool` 类型时，`!=` 运算符产生与 `^` 运算符相同的结果。

上述未提升的预定义布尔相等运算符的提升形式 (§12.4.8) 也是预定义的。

### 12.12.6 枚举比较运算符

每个枚举类型隐式提供以下预定义比较运算符：

```csharp
bool operator ==(E x, E y);
bool operator !=(E x, E y);

bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

计算 `x «op» y` 的结果，其中 `x` 和 `y` 是具有基础类型 `U` 的枚举类型 `E` 的表达式，且 «op» 是比较运算符之一，其结果与计算完全相同

结束注释

示例：以下示例检查无约束类型参数类型的参数是否为 null。

```csharp
class C<T>
{
    void F(T x)
    {
        if (x == null)
        {
            throw new ArgumentNullException();
        }
        ...
    }
}
```

`x == null` 构造是允许的，即使 `T` 可能表示非可空值类型，并且当 `T` 为非可空值类型时，结果简单地定义为 false。

结束示例

对于形式为 `x == y` 或 `x != y` 的操作，如果存在任何适用的 `operator ==` 或 `operator !=`，则运算符重载解析 (§12.4.5) 规则将选择该运算符而不是预定义的引用类型相等运算符。

> 注意：通过显式地将两个操作数都强制转换为类型 `object`，始终可以选定预定义的引用类型相等运算符。结束注释

示例：示例

```csharp
class Test
{
    static void Main()
    {
        string s = "Test";
        string t = string.Copy(s);
        Console.WriteLine(s == t);
        Console.WriteLine((object)s == t);
        Console.WriteLine(s == (object)t);
        Console.WriteLine((object)s == (object)t);
    }
}
```

生成输出

```
True
False
False
False
```

`s` 和 `t` 变量引用包含相同字符的两个不同的字符串实例。第一个比较输出 `True`，因为当两个操作数均为 `string` 类型时，选择了预定义的字符串相等运算符 (§12.12.8)。其余比较均输出 `False`，因为当任一操作数的绑定时类型为 `object` 时，`string` 类型中的 `operator ==` 重载不适用。

请注意，上述技术对于值类型没有意义。示例
