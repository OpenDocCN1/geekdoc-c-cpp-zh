
```
}
    X<int>.PrintTypes();
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

注意 int 和 System.Int32 是同一类型。typeof(X<>) 的结果不依赖于类型参数，但 typeof(X<T>) 的结果会依赖。

*结束示例*

## 12.8.18 sizeof 运算符

sizeof 运算符返回给定类型变量所占用的 8 位字节数。作为 sizeof 操作数的类型应为 unmanaged_type (§8.8)。

```
sizeof_expression
    : 'sizeof' '(' unmanaged_type ')'
    ;
```

对于某些预定义类型，sizeof 运算符会产生如下表所示的常量 int 值：

| 表达式 | 结果 |
|---|---|
| sizeof(sbyte) | 1 |
| sizeof(byte) | 1 |
| sizeof(short) | 2 |
| sizeof(ushort) | 2 |
| sizeof(int) | 4 |
| sizeof(uint) | 4 |
| sizeof(long) | 8 |
| sizeof(ulong) | 8 |
| sizeof(char) | 2 |
| sizeof(float) | 4 |
| sizeof(double) | 8 |
| sizeof(bool) | 1 |
| sizeof(decimal) | 16 |

对于枚举类型 T，表达式 sizeof(T) 的结果是一个常量值，等于其基础类型的大小，如上所述。对于所有其他操作数类型，sizeof 运算符在 §23.6.9 中指定。

```
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;

    static int F() => checked(x * y);    // Throws OverflowException
    static int G() => unchecked(x * y);  // Returns -727379968
    static int H() => x * y;             // Depends on default
}
```

没有报告编译时错误，因为这两个表达式都无法在编译时求值。在运行时，F 方法抛出 System.OverflowException，而 G 方法返回 –727379968（超出范围结果的低 32 位）。H 方法的行为取决于编译的默认溢出检查上下文，但它要么与 F 相同，要么与 G 相同。

*结束示例*

示例：在以下代码中

```
class Test
{
    const int x = 1000000;
    const int y = 1000000;

    static int F() => checked(x * y);    // Compile-time error, overflow
    static int G() => unchecked(x * y);  // Returns -727379968
    static int H() => x * y;             // Compile-time error, overflow
}
```

在 F 和 H 中求值常量表达式时发生的溢出会导致报告编译时错误，因为这些表达式在 checked 上下文中求值。在 G 中求值常量表达式时也会发生溢出，但由于求值是在 unchecked 上下文中进行，因此不会报告溢出。

*结束示例*

checked 和 unchecked 运算符仅影响在 “(” 和 “)” 标记内文本包含的那些操作的溢出检查上下文。这些运算符对因求值包含的表达式而被调用的函数成员没有任何影响。

示例：在以下代码中

```
class Test
{
    static int Multiply(int x, int y) => x * y;

    static int F() => checked(Multiply(1000000, 1000000));
}
```

在 F 中使用 checked 不会影响 Multiply 中 x * y 的求值，因此 x * y 在默认溢出检查上下文中求值。

*结束示例*

当以十六进制表示法编写有符号整数类型的常量时，unchecked 运算符很方便。

示例：

```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

上述两个十六进制常量都是 `uint` 类型。因为这些常量超出了 `int` 范围，所以如果没有 `unchecked` 运算符，转换到 `int` 将会产生编译时错误。

*结束示例*

*注意：* `checked` 和 `unchecked` 运算符和语句允许程序员控制某些数值计算的方面。然而，某些数值运算符的行为取决于其操作数的数据类型。例如，即使在明确的 unchecked 构造中相乘两个 decimal 也始终会在溢出时导致异常。同样，即使在明确的 checked 构造中相乘两个 float 也永远不会在溢出时导致异常。此外，其他运算符不受检查模式的影响，无论是默认还是显式。*结束注释*

## 12.8.20 默认值表达式

默认值表达式用于获取类型的默认值 (§9.3)。

```
default_value_expression
    : explicitly_typed_default
    | default_literal
    ;

explicitly_typed_default
    : 'default' '(' 'type' ')'
    ;

default_literal
    : 'default'
    ;
```

*default_literal* 表示默认值 (§9.3)。它没有类型，但可以通过默认值转换 (§10.2.16) 转换为任何类型。

*default_value_expression* 的结果是 *explicitly_typed_default* 中显式类型的默认值 (§9.3)，或 *default_value_expression* 的转换的目标类型。

- *default_value_expression* 是常量表达式 (§12.23) 如果类型是以下之一：
  - 引用类型
  - 已知为引用类型的类型参数 (§8.2)；
  - 以下值类型之一：`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float`、`double`、`decimal`、`bool`；或
  - 任何枚举类型。

## 12.8.21 栈分配

栈分配表达式从执行栈分配一块内存。*执行栈* 是存储局部变量的内存区域。执行栈不是托管堆的一部分。用于局部变量存储的内存会在当前函数返回时自动回收。

栈分配表达式的安全上下文规则在 §16.4.12.7 中描述。

```
stackalloc_expression
  : 'stackalloc' unmanaged_type '[' expression ']'
  | 'stackalloc' unmanaged_type? '[' constant_expression? ']' stackalloc_initializer
  ;

stackalloc_initializer
  : '{' stackalloc_initializer_element_list '}'
  ;

stackalloc_initializer_element_list
  : stackalloc_element_initializer (',' stackalloc_element_initializer)* ','?
  ;

stackalloc_element_initializer
  : expression
  ;
```

- 1. 局部变量声明 (§13.6.2) 的初始化表达式 E；和
- 2. 简单赋值 (§12.21.2) 的右操作数表达式 E，其本身作为表达式语句 (§13.7) 出现

在这两种上下文中，stackalloc_expression 仅允许作为以下形式出现：

- - E 的全部；或
- - 条件表达式 (§12.18) 的第二个和/或第三个操作数，其本身是 E 的全部。

unmanaged_type (§8.8) 表示将存储在新分配位置中的项的类型，而表达式表示这些项的数量。两者合在一起指定所需的分配大小。表达式的类型必须能隐式转换为 int 类型。

由于栈分配的大小不能为负，因此将项的数量指定为求值为负值的 constant_expression 是编译时错误。

在运行时，如果要分配的项数为负值，则行为未定义。如果为零，则不进行分配，并且返回的值是实现定义的。如果没有足够的内存来分配项，则会抛出 System.StackOverflowException。

当存在 stackalloc_initializer 时：

- - 如果省略 unmanaged_type，则根据 stackalloc_element_initializers 集合的最佳公共类型规则 (§12.6.3.15) 推断。
- - 如果省略 constant_expression，则推断为 stackalloc_element_initializers 的数量。
- - 如果存在 constant_expression，则它必须等于 stackalloc_element_initializers 的数量。

- - 结果的 Length 属性返回已分配的项数。
- - 结果的索引器 (§15.9) 返回对已分配块中某项的 variable_reference (§9.5)，并且会进行范围检查。

注意：当在不安全代码中出现时，stackalloc_expression 的结果可能为不同类型，参见 (§23.9)。结束注释

在 catch 或 finally 块 (§13.11) 中不允许使用栈分配初始化器。

注意：没有办法显式释放使用 stackalloc 分配的内存。结束注释

在函数成员执行期间创建的所有栈分配内存块在该函数成员返回时自动丢弃。

除了 stackalloc 运算符之外，C# 没有提供管理非垃圾回收内存的预定义结构。此类服务通常由支持的类库提供或直接从底层操作系统导入。

示例：

// Memory uninitialized
Span<int> span1 = stackalloc int[3];
// Memory initialized
Span<int> span2 = stackalloc int[3] { -10, -15, -30 };
// Type int is inferred
Span<int> span3 = stackalloc[] { 11, 12, 13 };
// Error; result is int*, not allowed in a safe context
var span4 = stackalloc[] { 11, 12, 13 };
// Error: no conversion from Span<int> to Span<long>
Span<long> span5 = stackalloc[] { 11, 12, 13 };
// Converts 11 and 13, and returns Span<long>
Span<long> span6 = stackalloc[] { 11, 121, 13 };
// Converts all and returns Span<long>
Span<long> span7 = stackalloc long[] { 11, 12, 13 };
// Implicit conversion of Span<T>
ReadOnlySpan<int> span8 = stackalloc int[] { 10, 22, 30 };
// Implicit conversion of Span<T>
Widget<double> span9 = stackalloc double[] { 1.2, 5.6 };

public class Widget<T>
{
    public static implicit operator Widget<T>(Span<double> sp) { return null; }
}
```

在 span8 的情况下，stackalloc 生成一个 Span<int>，它通过隐式运算符转换为 ReadOnlySpan<int>。同样，对于 span9，生成的 Span<double> 使用转换转换为用户定义的类型 Widget<double>，如所示。结束示例

## 12.8.22 Nameof 表达式

nameof_expression 用于以常量字符串形式获取程序实体的名称。

```
nameof_expression
  : 'nameof' '(' named_entity ')'
  ;

named_entity
```
