
## 7.6.12 checked 和 unchecked 运算符

checked 和 unchecked 运算符用于控制整型算术运算和转换的溢出检查上下文。

```
checked-expression:
    checked ( expression )
```

```
unchecked-expression:
    unchecked ( expression )
```

checked 运算符在 checked 上下文中计算所包含的表达式，而 unchecked 运算符在 unchecked 上下文中计算所包含的表达式。checked-expression 或 unchecked-expression 与 parenthesized-expression（§7.6.3）完全对应，不同之处在于所包含的表达式是在给定的溢出检查上下文中计算的。

> 乔恩·斯基特：在大多数情况下，溢出表示错误——但根据我的经验，大多数开发者（包括我自己）通常默认在关闭检查功能的情况下构建。显然，这种做法会有性能损失，但通常比数据被悄悄破坏要好。将 /checked+ 设为调试版本的默认值、将 /checked- 设为发布版本的默认值可能是有意义的——不过，我通常对调试版本和发布版本之间的行为差异保持警惕。这有点类似于 Windows Forms 中跨线程异常的行为。
> 
> 在几乎总是适合采用未检查溢出行为的一种情况是 GetHashCode 实现中，此时生成值的大小并不真正重要；本质上，它只是一个任意的位模式。

溢出检查上下文也可以通过 checked 和 unchecked 语句（§8.11）控制。

以下操作受 checked 和 unchecked 运算符及语句所建立的溢出检查上下文影响：

- 预定义的 ++ 和 -- 一元运算符（§7.6.9 和 §7.7.5），当操作数为整型时。
- 预定义的 - 一元运算符（§7.7.2），当操作数为整型时。
- 预定义的 +、-、* 和 / 二元运算符（§7.8），当两个操作数均为整型时。
- 从一个整型到另一个整型的显式数值转换（§6.2.1），或从 float 或 double 到整型的显式数值转换。

当上述操作之一产生的结果太大而无法在目标类型中表示时，执行该操作的上下文控制最终行为：

- 在 checked 上下文中，如果该操作是常量表达式（§7.19），则发生编译时错误。否则，当该操作在运行时执行时，将抛出 System.OverflowException。
- 在 unchecked 上下文中，结果会被截断，丢弃任何不适合目标类型的高阶位。

对于未包含在任何 checked 或 unchecked 运算符或语句中的非常量表达式（在运行时计算的表达式），默认溢出检查上下文为 unchecked，除非外部因素（例如编译器开关和执行环境配置）要求进行 checked 求值。

对于常量表达式（可以在编译时完全求值的表达式），默认溢出检查上下文始终为 checked。除非常量表达式被显式置于 unchecked 上下文中，否则在表达式的编译时求值期间发生的溢出始终会导致编译时错误。

匿名函数的主体不受该匿名函数所在 checked 或 unchecked 上下文的影响。

在示例

```
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;

    static int F() {
        return checked(x * y);  // Throws OverflowException
    }

    static int G() {
        return unchecked(x * y);  // Returns -727379968
    }

    static int H() {
        return x * y;             // Depends on default
    }
}
```

中，不会报告编译时错误，因为这两个表达式都无法在编译时求值。在运行时，F 方法抛出 System.OverflowException，G 方法返回 −727379968（超出范围结果的低 32 位）。H 方法的行为取决于编译的默认溢出检查上下文，但它要么与 F 相同，要么与 G 相同。

在示例

```
class Test
{
    const int x = 1000000;
    const int y = 1000000;

    static int F() {
        return checked(x * y);     // Compile error, overflow
    }
    static int G() {
        return unchecked(x * y);   // Returns -727379968
    }
    static int H() {
        return x * y;              // Compile error, overflow
    }
}
```

中，求值 F 和 H 中的常量表达式时发生的溢出会导致报告编译时错误，因为这些表达式是在 checked 上下文中求值的。求值 G 中的常量表达式时也会发生溢出，但由于求值发生在 unchecked 上下文中，因此不会报告溢出。

checked 和 unchecked 运算符仅对文本上包含在“(”和“)”标记内的那些操作影响溢出检查上下文。这些运算符对因求值所包含表达式而调用的函数成员没有影响。在示例

```
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

中，F 中 checked 的使用不影响 Multiply 中 x * y 的求值，因此 x * y 是在默认溢出检查上下文中求值的。

当以十六进制记法编写有符号整型的常量时，unchecked 运算符很方便。例如：

```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

上述两个十六进制常量均为 uint 类型。由于这些常量超出 int 范围，如果没有 unchecked 运算符，到 int 的强制转换将产生编译时错误。

checked 和 unchecked 运算符及语句允许程序员控制某些数值计算的某些方面。然而，某些数值运算符的行为取决于其操作数的数据类型。例如，两个 decimal 相乘即使在显式 unchecked 构造中，也始终会在溢出时引发异常。类似地，两个 float 相乘即使在显式 checked 构造中，也绝不会在溢出时引发异常。此外，其他运算符从不受检查模式影响，无论是默认模式还是显式模式。

## 7.6.13 默认值表达式

默认值表达式用于获取类型的默认值（§5.2）。通常，默认值表达式用于类型参数，因为可能不知道类型参数是值类型还是引用类型。（除非类型参数已知为引用类型，否则不存在从 null 字面量到类型参数的转换。）

```
default-value-expression:
    default ( type )
```

如果 default-value-expression 中的类型在运行时求值为引用类型，则结果为转换为该类型的 null。如果 default-value-expression 中的类型在运行时求值为值类型，则结果为该值类型的默认值（§4.1.2）。

如果类型是引用类型或已知为引用类型的类型参数（§10.1.5），则 default-value-expression 是常量表达式（§7.19）。此外，如果类型是以下值类型之一，则 default-value-expression 是常量表达式：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool 或任何枚举类型。

> **约瑟夫·阿尔巴哈里** 默认值表达式在泛型类型参数中特别有用。Microsoft 的 LINQ 实现广泛使用了此构造，例如在 FirstOrDefault、SingleOrDefault 和 DefaultIfEmpty 等运算符中。

## 7.6.14 匿名方法表达式

*匿名方法表达式*是定义匿名函数的两种方式之一。这些内容将在 §7.15 中进一步描述。

## 7.7 一元运算符

+、-、!、~、++、-- 和强制转换运算符称为一元运算符。

```
unary-expression:
    primary-expression
    + unary-expression
    - unary-expression
    ! unary-expression
    ~ unary-expression
    pre-increment-expression
    pre-decrement-expression
    cast-expression
```

如果 *unary-expression* 的操作数具有编译时类型 *dynamic*，则对其进行动态绑定（§7.2.2）。在这种情况下，*unary-expression* 的编译时类型为 *dynamic*，并且下面描述的决定将在运行时使用操作数的运行时类型进行。

### 7.7.1 一元加运算符

对于形式为 +x 的操作，应用一元运算符重载决策（§7.3.3）来选择特定的运算符实现。操作数被转换为所选运算符的参数类型，结果的类型为该运算符的返回类型。预定义的一元加运算符列出如下：

```
int operator +(int x);
uint operator +(uint x);
long operator +(long x);
ulong operator +(ulong x);
float operator +(float x);
double operator +(double x);
decimal operator +(decimal x);
```

对于这些运算符中的每一个，结果都只是操作数的值。

> 埃里克·利珀特：一元加运算符是世界上最没用的运算符。它被包含进来是为了完整性，这样你就可以编写 int x = -30; int y = +40;，如果你希望出于可读性目的强调该值为正数的话。

