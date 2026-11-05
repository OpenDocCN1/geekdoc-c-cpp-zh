
在同一程序中，两个匿名对象初始化器如果指定了属性名称相同、编译时类型相同且顺序相同的属性序列，则会生成相同匿名类型的实例。

在示例中

```
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```

最后一条赋值语句是允许的，因为 p1 和 p2 是同一匿名类型。

匿名类型上的 Equals 和 GetHashCode 方法重写了从 object 继承的方法，并根据属性的 Equals 和 GetHashCode 定义，因此同一匿名类型的两个实例相等当且仅当它们的所有属性都相等。

成员声明符可以缩写为简单名称 (§7.5.2)、成员访问 (§7.5.4) 或基访问 (§7.6.8)。这称为投影初始化器，是对具有相同名称的属性的声明和赋值的简写。具体而言，形式为

```
identifier

expr . identifier
```

的成员声明符分别精确等价于以下内容：

```
identifier = identifier
identifier = expr . identifier
```

因此，在投影初始化器中，标识符同时选择值以及要将值赋给的字段或属性。直观上，投影初始化器不仅投影值，还投影值的名称。

## 7.6.11 typeof 运算符

typeof 运算符用于获取类型的 System.Type 对象。

```
typeof-expression:
    typeof ( type )
    typeof ( unbound-type-name )
    typeof ( void )
```

```
unbound-type-name:
    identifier generic-dimension-specifier_opt
    identifier :: identifier generic-dimension-specifier_opt
    unbound-type-name . identifier generic-dimension-specifier_opt
```

```
generic-dimension-specifier:
    < commas_opt >

commas:
    ,
    commas ,
```

typeof-expression 的第一种形式由 typeof 关键字后跟带括号的类型组成。此类表达式的结果是所指示类型的 System.Type 对象。任何给定类型只有一个 System.Type 对象。这意味着对于类型 T，typeof(T) == typeof(T) 始终为 true。该类型不能为 dynamic。

typeof-expression 的第二种形式由 typeof 关键字后跟带括号的 unbound-type-name 组成。unbound-type-name 与 type-name (§3.8) 非常相似，只是 unbound-type-name 包含 generic-dimension-specifiers，而 type-name 包含 type-argument-lists。当 typeof-expression 的操作数是同时满足 unbound-type-name 和 type-name 文法的标记序列时——即当它既不包含 generic-dimension-specifier 也不包含 type-argument-list 时——该标记序列被视为 type-name。unbound-type-name 的含义确定如下：

- 将标记序列转换为 type-name，用具有相同数量逗号且每个类型参数均为关键字 object 的 type-argument-list 替换每个 generic-dimension-specifier。
- 在忽略所有类型参数约束的情况下计算 resulting type-name。
- unbound-type-name 解析为与 resulting constructed type (§4.4.3) 关联的未绑定泛型类型。

typeof-expression 的结果是 resulting 未绑定泛型类型的 System.Type 对象。

typeof-expression 的第三种形式由 typeof 关键字后跟带括号的 void 关键字组成。此类表达式的结果是表示类型缺失的 System.Type 对象。typeof(void) 返回的类型对象与任何类型的返回类型对象不同。此特殊类型对象在允许对语言中的方法进行反射的类库中很有用，其中这些方法希望以 System.Type 的实例来表示任何方法的返回类型，包括 void 方法。

typeof 运算符可用于类型参数。结果是绑定到类型参数的运行时类型的 System.Type 对象。typeof 运算符也可用于构造类型或未绑定泛型类型 (§4.4.3)。未绑定泛型类型的 System.Type 对象与实例类型的 System.Type 对象不同。

实例类型在运行时始终是封闭的构造类型，因此其 System.Type 对象取决于正在使用的运行时类型参数，而未绑定泛型类型没有类型参数。

## 示例

```
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

System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X`1[System.Int32]
X`1[X`1[System.Int32]]
X`1[T]

请注意 int 和 System.Int32 是同一类型。

还请注意 typeof(X<>) 的结果不依赖于类型参数，但 typeof(X<T>) 的结果会依赖。

## 7.6.12 checked 和 unchecked 运算符

checked 和 unchecked 运算符用于控制整数类型算术运算和转换的 *溢出检查上下文*。

```
checked-expression:
    checked   (  expression  )

unchecked-expression:
    unchecked   (  expression  )
```

checked 运算符在 checked 上下文中计算包含的表达式，而 unchecked 运算符在 unchecked 上下文中计算包含的表达式。*checked 表达式* 或 *unchecked 表达式* 精确对应于 *带括号的表达式* (§7.6.3)，只是包含的表达式在给定的溢出检查上下文中进行求值。

> > **JON SKEET**  在大多数情况下，溢出表示错误——但在我经验中，大多数开发人员（包括我自己）通常默认情况下不开启检查功能。显然，这种方法有性能损失，但这通常比静默损坏的数据更可取。也许让 `/checked+` 成为 debug 构建的默认值而 `/checked-` 成为 release 构建的默认值是有意义的——尽管我通常对 debug 和 release 之间的行为变化持谨慎态度。这有点像 Windows Forms 中跨线程异常的行为。
> >
> > GetHashCode 实现中 unchecked 溢出行为几乎总是合适的一种情况，在那里生成的值的大小并不重要；本质上，它只是一个任意的位模式。

溢出检查上下文也可以通过 checked 和 unchecked 语句 (§8.11) 控制。

以下操作受 checked 和 unchecked 运算符和语句建立的溢出检查上下文影响：

- 预定义的 `++` 和 `--` 一元运算符 (§7.6.9 和 §7.7.5)，当操作数为整数类型时。
- 预定义的 `-` 一元运算符 (§7.7.2)，当操作数为整数类型时。
- 预定义的 `+`、`-`、`*` 和 `/` 二元运算符 (§7.8)，当两个操作数均为整数类型时。
- 从一种整数类型到另一种整数类型的显式数值转换 (§6.2.1)，或从 float 或 double 到整数类型的转换。

当上述任一操作产生无法在目标类型中表示的结果时，执行操作的上下文控制 resulting 行为：

- 在 checked 上下文中，如果操作是常量表达式 (§7.19)，则会发生编译时错误。否则，当操作在运行时执行时，会抛出 System.OverflowException。
- 在 unchecked 上下文中，结果通过丢弃不适合目标类型的任何高位位来截断。

对于未被任何 checked 或 unchecked 运算符或语句包围的非常量表达式（在运行时求值的表达式），默认溢出检查上下文为 unchecked，除非外部因素（如编译器开关和执行环境配置）要求 checked 求值。

对于常量表达式（可在编译时完全求值的表达式），默认溢出检查上下文始终为 checked。除非常量表达式明确置于 unchecked 上下文中，否则在表达式编译时求值期间发生的溢出始终会导致编译时错误。

匿名函数的函数体不受匿名函数出现的 checked 或 unchecked 上下文的影响。

在示例中

```
    class Test
    {
        static readonly int x = 1000000;
        static readonly int y = 1000000;

        static int F() {
            return checked(x * y);      // Throws OverflowException
        }

        static int G() {
            return unchecked(x * y);    // Returns -727379968
        }

        static int H() {
            return x * y;               // Depends on default
        }
    }
```

未报告编译时错误，因为这两个表达式都无法在编译时求值。在运行时，F 方法抛出 System.OverflowException 且 G
