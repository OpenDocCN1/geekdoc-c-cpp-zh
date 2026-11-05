
对于常量表达式 (§11.20)（可在编译时完全求值的表达式），默认的溢出检查上下文始终为已检查。除非常量表达式被显式置于未检查上下文中，否则在表达式编译时求值期间发生的溢出始终会导致编译时错误。

匿名函数的函数体不受匿名函数所在已检查或未检查上下文的影响。

示例：在以下代码中

```csharp
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;

    static int F() => checked(x * y);    // Throws OverflowException
    static int G() => unchecked(x * y);  // Returns -727379968
    static int H() => x * y;             // Depends on default
}
```

未报告编译时错误，因为这两个表达式都无法在编译时求值。在运行时，F 方法会抛出 System.OverflowException，而 G 方法返回 -727379968（超出范围结果的低 32 位）。H 方法的行为取决于编译的默认溢出检查上下文，但它要么与 F 相同，要么与 G 相同。

示例结束

示例：在以下代码中

```csharp
class Test
{
    const int x = 1000000;
    const int y = 1000000;

    static int F() => checked(x * y);    // Compile-time error, overflow
    static int G() => unchecked(x * y);  // Returns -727379968
    static int H() => x * y;             // Compile-time error, overflow
}
```

在 F 和 H 中求值常量表达式时发生的溢出会导致报告编译时错误，因为这些表达式是在已检查上下文中求值的。在 G 中求值常量表达式时也会发生溢出，但由于求值是在未检查上下文中进行的，因此不会报告溢出。

示例结束

checked 和 unchecked 运算符仅影响在“(”和“)”标记内文本包含的那些操作的溢出检查上下文。运算符对因求值包含的表达式而被调用的函数成员没有影响。

示例：在以下代码中

```csharp
class Test
{
    static int Multiply(int x, int y) => x * y;
    static int F() => checked(Multiply(1000000, 1000000));
}
```

在 F 中使用 checked 不会影响 Multiply 中 x * y 的求值，因此 x * y 是在默认溢出检查上下文中求值的。

示例结束

在十六进制表示法中编写有符号整型常数时，未检查运算符很方便。

示例：

```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

上述两个十六进制常量均为 uint 类型。因为这些常量超出了 int 范围，所以如果没有 unchecked 运算符，强制转换为 int 将会产生编译时错误。

示例结束

注：checked 和 unchecked 运算符和语句允许程序员控制某些数值计算的某些方面。然而，某些数值运算符的行为取决于其操作数的数据类型。例如，即使在显式的未检查结构中相乘两个 decimal 也始终会在溢出时导致异常。类似地，即使在显式的已检查结构中相乘两个 float 也永远不会在溢出时导致异常。此外，其他运算符不受检查模式的影响，无论是默认还是显式。 注释结束

## 11.7.19 默认值表达式

默认值表达式用于获取类型的默认值 (§9.3)。通常默认值表达式用于类型参数，因为可能不知道类型参数是值类型还是引用类型。（除非已知类型参数是引用类型 (§8.2)，否则不存在从 null 字面量 (§6.4.5.7) 到类型参数的转换。）

```
default_value_expression
    : 'default' '(' type ')'
    ;
```

如果 default_value_expression 中的类型在运行时求值为引用类型，则结果为转换为该类型的 null。如果 default_value_expression 中的类型在运行时求值为值类型，则结果为该值类型的默认值 (§8.3.3)。

如果 type 是引用类型或已知为引用类型的类型参数 (§8.2)，则 default_value_expression 是常量表达式 (§11.20)。此外，如果 type 是以下值类型之一，则 default_value_expression 也是常量表达式：sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double、decimal、bool 或任何枚举类型。

## 11.7.20 Nameof 表达式

nameof_expression 用于以常量字符串的形式获取程序实体的名称。

```
nameof_expression
    : 'nameof' '(' named_entity ')'
    ;
```

```
named_entity
  : named_entity_target ('.' identifier type_argument_list?)*
  ;

named_entity_target
  : simple_name
  | 'this'
  | 'base'
  | predefined_type
  | qualified_alias_member
  ;
```

因为 nameof 不是关键字，所以 nameof_expression 在语法上始终与简单名称 nameof 的调用不明确。出于兼容性原因，如果对名称 nameof 的名称查找 (§11.7.4) 成功，则该表达式被视为 invocation_expression —— 无论该调用是否有效。否则它就是一个 nameof_expression。

在编译时，根据 §11.7.4 和 §11.7.6 中描述的规则，对 named_entity 执行简单名称和成员访问查找。然而，当 §11.7.4 和 §11.7.6 中描述的查找因在静态上下文中找到实例成员而导致错误时，nameof_expression 不会产生此类错误。

对于指定方法组的 named_entity 具有 type_argument_list 来说是编译时错误。对于 named_entity_target 具有类型 dynamic 来说是编译时错误。

nameof_expression 是类型为 string 的常量表达式，在运行时没有效果。具体而言，其 named_entity 不会被求值，并且在确定性赋值分析 (§9.4.4.22) 方面被忽略。其值是 named_entity 中在可选的最终 type_argument_list 之前的最后一个标识符，按以下方式转换：

- 前缀 "@"，如果使用，则被移除。
- 每个 unicode_escape_sequence 转换为其对应的 Unicode 字符。
- 任何 formatting_characters 都被移除。

这些是 §6.4.3 中在测试标识符相等性时应用的相同转换。

示例：以下说明了各种 nameof 表达式的结果，假设泛型类型 List<> 在 System.Collections.Generic 命名空间内声明：

```csharp
using System.Collections.Generic;

using TestAlias = System.String;

class Program
{
    static void Main()
    {
        var point = (x: 3, y: 4);

        string n1 = nameof(System);                 // "System"
        string n2 = nameof(System.Collections.Generic); // "Generic"
        string n3 = nameof(point);                  // "point"
        string n4 = nameof(point.x);                // "x"
        string n5 = nameof(Program);                // "Program"
        string n6 = nameof(System.Int32);           // "Int32"
    }
}
string n7 = nameof(TestAlias); // "TestAlias"
string n8 = nameof(List<int>); // "List"
string n9 = nameof(Program.InstanceMethod); // "InstanceMethod"
string n10 = nameof(Program.GenericMethod); // "GenericMethod"
string n11 = nameof(Program.NestedClass); // "NestedClass"

// Invalid
// string x1 = nameof(List<>); // Empty type argument list
// string x2 = nameof(List<T>); // T is not in scope
// string x3 = nameof(GenericMethod<>); // Empty type argument list
// string x4 = nameof(GenericMethod<T>); // T is not in scope
// string x5 = nameof(int); // Keywords not permitted
// string x6 = nameof(GenericMethod<Program>); // Type arguments not permitted // for method group
}
void InstanceMethod() { }
void GenericMethod<T>() {
    string n1 = nameof(List<T>); // "List"
    string n2 = nameof(T); // "T"
}
class NestedClass { }
}
```

此示例中可能令人惊讶的部分是 nameof(System.Collections.Generic) 解析为仅 "Generic" 而不是完整命名空间，以及 nameof(TestAlias) 解析为 "TestAlias" 而不是 "String"。 示例结束

## 11.7.21 匿名方法表达式

anonymous_method_expression 是定义匿名函数的两种方式之一。这些内容在 §11.16 中进一步描述。

## 11.8 一元运算符

### 11.8.1 通用

+、-、!、~、++、--、cast 和 await 运算符称为一元运算符。

```
unary_expression
: primary_expression
| '+' unary_expression
| '-' unary_expression
| '!' unary_expression
| '~' unary_expression
| pre_increment_expression
| pre_decrement_expression
| cast_expression
| await_expression
| pointer_indirection_expression    // unsafe code support
```
