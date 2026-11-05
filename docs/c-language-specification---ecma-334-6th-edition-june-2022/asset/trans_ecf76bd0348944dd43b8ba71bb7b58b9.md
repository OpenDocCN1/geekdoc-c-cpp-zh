
最后 一行的赋值是允许的，因为 p1 和 p2 是同一匿名类型。

*结束示例*

匿名类型上的 Equals 和 GetHashCode 方法重写了从 object 继承的方法，并以属性的 Equals 和 GetHashCode 定义，因此同一匿名类型的两个实例相等当且仅当它们的所有属性都相等。

成员声明符可以缩写为简单名称 (§11.7.4)、成员访问 (§11.7.6)、空条件投影初始化器 (§11.7.7) 或基访问 (§11.7.13)。这称为投影初始化器，是对同名属性的声明和赋值的简写。具体而言，形式为的成员声明符

```
«identifier», «expr» . «identifier» and «expr» ? . «identifier»
```

分别精确等价于以下内容：

```
«identifier» = «identifier», «identifier» = «expr» . «identifier» and «identifier» = «expr» ? . «identifier»
```

因此，在投影初始化器中，标识符同时选择值以及要将值赋给的字段或属性。直观地说，投影初始化器不仅投影值，还投影值的名称。

## 11.7.16 typeof 运算符

typeof 运算符用于获取类型的 System.Type 对象。

```
typeof_expression
: 'typeof' '(' type ')'
| 'typeof' '(' unbound_type_name ')'
| 'typeof' '(' 'void' ')'
;

unbound_type_name
: identifier generic_dimension_specifier?
| identifier '::' identifier generic_dimension_specifier?
| unbound_type_name '.' identifier generic_dimension_specifier?
;

generic_dimension_specifier
: '<' comma* '>'
;

comma
: ','
;
```

typeof_expression 的第一种形式由 typeof 关键字后跟带括号的类型组成。这种形式表达式的结果是所指示类型的 System.Type 对象。任何给定类型只有一个 System.Type 对象。这意味着对于类型 T，typeof(T) == typeof(T) 始终为 true。类型不能是 dynamic。

typeof_expression 的第二种形式由 typeof 关键字后跟带括号的 unbound_type_name 组成。

注：unbound_type_name 与 type_name (§7.8) 非常相似，只是 unbound_type_name 包含 generic_dimension_specifiers 而 type_name 包含 type_argument_lists。 *结束注释*

当 typeof_expression 的操作数是同时满足 unbound_type_name 和 type_name 文法的标记序列时，即当它既不包含 generic_dimension_specifier 也不包含 type_argument_list 时，该标记序列被视为 type_name。unbound_type_name 的含义确定如下：

- 将标记序列转换为 type_name，用具有相同逗号数且每个 type_argument 均为 keyword object 的 type_argument_list 替换每个 generic_dimension_specifier。
- 在忽略所有类型参数约束的情况下计算得到的 type_name。
- unbound_type_name 解析为与得到的构造类型关联的未绑定泛型类型 (§8.4)。

typeof_expression 的结果是所得未绑定泛型类型的 System.Type 对象。

typeof_expression 的第三种形式由 typeof 关键字后跟带括号的 void 关键字组成。这种形式表达式的结果是表示类型缺失的 System.Type 对象。typeof(void) 返回的类型对象与任何类型的类型对象都不同。

注：此特殊类型对象在允许对语言中的方法进行反射的类库中很有用，其中这些方法希望有一种方式用 System.Type 的实例表示任何方法的返回类型，包括 void 方法。 *结束注释*

typeof 运算符可用于类型参数。结果是绑定到类型参数的运行时类型的 System.Type 对象。typeof 运算符也可用于构造类型或未绑定泛型类型 (§8.4.4)。未绑定泛型类型的 System.Type 对象与实例类型的 System.Type 对象 (§14.3.2) 不同。实例类型在运行时始终是封闭的构造类型，因此其 System.Type 对象取决于正在使用的运行时类型参数。而未绑定泛型类型没有类型参数，无论运行时类型参数如何都产生相同的 System.Type 对象。

示例：示例

```
using System;
class X<T>
{
    public static void PrintTypes()
    {
        Type[] t =
        {
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
        for (int i = 0; i < t.Length; i++)
        {
            Console.WriteLine(t[i]);
        }
    }
}
class Test
{
    static void Main()
    {
        X<int>.PrintTypes();
    }
}
```

产生以下输出：

System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X'1[System.Int32]
X'1[X'1[System.Int32]]
X'1[T]

请注意 int 和 System.Int32 是同一类型。typeof(X<>) 的结果不依赖于类型参数，但 typeof(X<T>) 的结果会依赖。

*结束示例*

## 11.7.17 sizeof 运算符

sizeof 运算符返回给定类型变量所占用的 8 位字节数。作为 sizeof 操作数的类型应为 unmanaged_type (§8.8)。

```
sizeof_expression
    : 'sizeof' '(' unmanaged_type ')'
    ;
```

对于某些预定义类型，sizeof 运算符产生如下表所示的常量 int 值：

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

对于枚举类型 T，表达式 sizeof(T) 的结果是等于其基础类型的大小的常量值，如上所示。对于所有其他操作数类型，sizeof 运算符在 §22.6.9 中指定。

## 11.7.18 checked 和 unchecked 运算符

checked 和 unchecked 运算符用于控制整数类型算术运算和转换的溢出检查上下文。

```
checked_expression
  : 'checked' '(' expression ')'
  ;

unchecked_expression
  : 'unchecked' '(' expression ')'
  ;
```

checked 运算符在 checked 上下文中计算包含的表达式，而 unchecked 运算符在 unchecked 上下文中计算包含的表达式。checked_expression 或 unchecked_expression 与带括号的表达式 (§11.7.5) 完全对应，只是包含的表达式在给定的溢出检查上下文中进行求值。

溢出检查上下文也可以通过 checked 和 unchecked 语句 (§12.12) 进行控制。

以下操作受 checked 和 unchecked 运算符和语句建立的溢出检查上下文影响：

- 预定义的 ++ 和 -- 运算符 (§11.7.14 和 §11.8.6)，当操作数为整数或枚举类型时。
- 预定义的 - 一元运算符 (§11.8.3)，当操作数为整数类型时。
- 预定义的 +, -, *, 和 / 二元运算符 (§11.9)，当两个操作数均为整数或枚举类型时。
- 从一个整数或枚举类型到另一个整数或枚举类型的显式数值转换 (§10.3.2)，或从 float 或 double 到整数或枚举类型的转换。

当上述操作之一产生无法在目标类型中表示的结果时，执行操作的上下文控制所得行为：

- 在 checked 上下文中，如果操作是常量表达式 (§11.20)，则会发生编译时错误。否则，当操作在运行时执行时，会抛出 System.OverflowException。
- 在 unchecked 上下文中，结果通过丢弃不适合目标类型的任何高位来截断。

对于未被任何 checked 或 unchecked 运算符或语句包围的非常量表达式 (§11.20)（在运行时求值的表达式），默认溢出检查上下文为 unchecked，除非外部因素（如编译器开关和执行环境配置）要求进行 checked 求值。

