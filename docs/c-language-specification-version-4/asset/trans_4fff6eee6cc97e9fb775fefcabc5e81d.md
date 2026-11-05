
任何给定类型的 System.Type 对象。这意味着对于类型 T，typeof(T) == typeof(T) 始终为 true。该类型不能是动态类型。

typeof 表达式的第二种形式由 typeof 关键字后跟带括号的未绑定类型名称组成。未绑定类型名称与类型名称（§3.8）非常相似，不同之处在于未绑定类型名称包含泛型维度说明符，而类型名称包含类型实参列表。当 typeof 表达式的操作数是同时满足未绑定类型名称和类型名称语法的标记序列时，即当它既不包含泛型维度说明符也不包含类型实参列表时，该标记序列被视为类型名称。未绑定类型名称的含义按如下方式确定：

- 将标记序列转换为类型名称：把每个泛型维度说明符替换为一个类型实参列表，该列表具有相同数量的逗号，并以关键字 object 作为每个类型实参。
- 对得到的类型名称求值，同时忽略所有类型参数约束。
- 未绑定类型名称解析为与所得构造类型（§4.4.3）关联的未绑定泛型类型。

typeof 表达式的结果是所得未绑定泛型类型的 System.Type 对象。

typeof 表达式的第三种形式由 typeof 关键字后跟带括号的 void 关键字组成。这种形式的表达式的结果是表示不存在类型的 System.Type 对象。typeof(void) 返回的类型对象与为任何类型返回的类型对象不同。这个特殊类型对象在允许对语言中的方法进行反射的类库中很有用；在这些类库中，那些方法希望有一种方式用 System.Type 的实例来表示任何方法的返回类型，包括 void 方法。

typeof 运算符可用于类型参数。结果是绑定到该类型参数的运行时类型的 System.Type 对象。typeof 运算符也可用于构造类型或未绑定泛型类型（§4.4.3）。未绑定泛型类型的 System.Type 对象与实例类型的 System.Type 对象不同。实例类型在运行时始终是封闭构造类型，因此其 System.Type 对象取决于所使用的运行时类型实参，而未绑定泛型类型没有类型实参。

示例

```csharp
using System;
class X<T>
{
    public static void PrintTypes() {
        Type[] t = {
            typeof(int),
            typeof(System.Int32),
            typeof(string),
            typeof(double[]),
            typeof(void),
            typeof(T),
            typeof(X<T>),
            typeof(X<X<T>>),
            typeof(X<>)
        };
        for (int i = 0; i < t.Length; i++) {
            Console.WriteLine(t[i]);
        }
    }
}
class Test
{
    static void Main() {
        X<int>.PrintTypes();
    }
}
```

生成以下输出：

```
System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X`1[System.Int32]
X`1[X`1[System.Int32]]
X`1[T]
```

注意，int 和 System.Int32 是同一类型。

另请注意，typeof(X<>) 的结果不依赖于类型实参，而 typeof(X<T>) 的结果则依赖。

### 7.6.12 checked 和 unchecked 运算符

checked 和 unchecked 运算符用于控制整型算术运算和转换的溢出检查上下文。

```
checked-expression:
    checked ( expression )
unchecked-expression:
    unchecked ( expression )
```

checked 运算符在 checked 上下文中计算所包含的表达式，而 unchecked 运算符在 unchecked 上下文中计算所包含的表达式。checked 表达式或 unchecked 表达式与带括号的表达式（§7.6.3）完全对应，不同之处在于所包含的表达式在给定的溢出检查上下文中求值。

溢出检查上下文也可通过 checked 和 unchecked 语句（§8.11）控制。

以下操作受 checked 和 unchecked 运算符及语句建立的溢出检查上下文影响：

- 预定义的 ++ 和 -- 一元运算符（§7.6.9 和 §7.7.5），当操作数为整型时。
- 预定义的 - 一元运算符（§7.7.2），当操作数为整型时。
- 预定义的 +、-、* 和 / 二元运算符（§7.8），当两个操作数均为整型时。
- 从一个整型到另一个整型，或从 float 或 double 到整型的显式数值转换（§6.2.1）。

当上述操作之一产生的结果太大，无法在目标类型中表示时，执行该操作的上下文控制最终行为：

- 在 checked 上下文中，如果该操作是常量表达式（§7.19），则发生编译时错误。否则，当该操作在运行时执行时，将抛出 System.OverflowException。
- 在 unchecked 上下文中，结果通过丢弃任何不适合目标类型的高序位来截断。

C# 语言规范

对于未包含在任何 checked 或 unchecked 运算符或语句中的非常量表达式（在运行时求值的表达式），默认溢出检查上下文为 unchecked，除非外部因素（如编译器开关和执行环境配置）要求进行 checked 求值。

对于常量表达式（可在编译时完全求值的表达式），默认溢出检查上下文始终为 checked。除非常量表达式被显式置于 unchecked 上下文中，否则在表达式的编译时求值期间发生的溢出始终会导致编译时错误。

匿名函数的主体不受该匿名函数所在 checked 或 unchecked 上下文的影响。

在示例

```csharp
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;
    static int F() {
        return checked(x * y);    // Throws OverflowException
    }
    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }
    static int H() {
        return x * y;             // Depends on default
    }
}
```

不会报告编译时错误，因为这两个表达式都不能在编译时求值。在运行时，F 方法抛出 System.OverflowException，G 方法返回 -727379968（越界结果的低 32 位）。H 方法的行为取决于编译的默认溢出检查上下文，但它要么与 F 相同，要么与 G 相同。

在示例

```csharp
class Test
{
    const int x = 1000000;
    const int y = 1000000;
    static int F() {
        return checked(x * y);    // Compile error, overflow
    }
    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }
    static int H() {
        return x * y;             // Compile error, overflow
    }
}
```

在 F 和 H 中求值常量表达式时发生的溢出会导致报告编译时错误，因为这些表达式在 checked 上下文中求值。在 G 中求值常量表达式时也会发生溢出，但由于求值在 unchecked 上下文中进行，因此不会报告该溢出。

checked 和 unchecked 运算符仅影响在文本上包含在“(”和“)”标记内的那些操作的溢出检查上下文。这些运算符对因求值所包含表达式而调用的函数成员没有影响。在示例

```csharp
class Test
{
    static int Multiply(int x, int y) {
        return x * y;
    }
    static int F() {
        return checked(Multiply(1000000, 1000000));
    }
}
```

F 中使用 checked 不会影响 Multiply 中 x * y 的求值，因此 x * y 在默认溢出检查上下文中求值。

当以十六进制记法编写有符号整型常量时，unchecked 运算符很方便。例如：

```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

上面的两个十六进制常量都是 uint 类型。因为这些常量超出 int 范围，如果没有 unchecked 运算符，到 int 的强制转换将产生编译时错误。

checked 和 unchecked 运算符及语句允许程序员控制某些数值计算的某些方面。然而，某些数值运算符的行为取决于其操作数的数据类型。例如，两个 decimal 相乘即使在显式 unchecked 构造中，也始终会在溢出时产生异常。类似地，两个 float 相乘即使在显式 checked 构造中，也绝不会在溢出时产生异常。此外，其他运算符绝不会受检查模式（无论默认还是显式）的影响。

### 7.6.13 默认值表达式

默认值表达式用于获取类型的默认值（§5.2）。通常，默认值表达式用于类型参数，因为可能不知道类型参数是值类型还是引用类型。（除非已知类型参数是引用类型，否则不存在从 null 字面量到类型参数的转换。）

```
default-value-expression:
    default ( type )
```

如果默认值表达式中的类型在运行时求值为引用类型，则结果为转换为该类型的 null。如果默认值表达式中的类型在运行时求值为值类型，则结果为该值类型的默认值（§4.1.2）。

如果类型是引用类型或已知为引用类型的类型参数（§10.1.5），则默认值表达式是常量表达式（§7.19）。此外，如果类型是以下值类型之一：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool 或任何枚举类型，则默认值表达式也是常量表达式。

### 7.6.14 匿名方法表达式

匿名方法表达式是定义匿名函数的两种方式之一。这些将在 §7.15 中进一步描述。
