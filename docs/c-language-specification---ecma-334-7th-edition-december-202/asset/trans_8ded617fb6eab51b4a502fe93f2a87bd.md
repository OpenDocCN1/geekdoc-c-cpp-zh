
使用标识符 _ 的声明表达式是一个丢弃（§9.2.9.1），并且不会为变量引入名称。使用除 _ 之外的标识符的声明表达式会将该名称引入最近的外层局部变量声明空间（§7.3）。

*示例：*

```csharp
string M(out int i, string s, out bool b) { ... }

var s1 = M(out int i1, "One", out var b1);
Console.WriteLine($"{i1}, {b1}, {s1}");
// Error: i2 referenced within declaring argument list
var s2 = M(out var i2, M(out i2, "Two", out bool b2), out b2);
var s3 = M(out int _, "Three", out var _);
```

s1 的声明同时展示了显式类型和隐式类型的声明表达式。b1 的推断类型为 bool，因为那是 M 中对应 out 参数的类型。随后的 WriteLine 能够访问 i1 和 b1，因为它们已被引入到外层作用域。

s2 的声明展示了在嵌套调用 M 中尝试使用 i2，这是不允许的，因为引用发生在 i2 被声明的参数列表内。另一方面，对最终参数中 b2 的引用是允许的，因为它发生在 b2 被声明的嵌套参数列表结束之后。

s3 的声明展示了既有隐式类型又有显式类型的丢弃声明表达式。因为丢弃不会声明命名变量，所以标识符 _ 的多次出现是允许的。

```csharp
(int i1, int _, (var i2, var _), _) = (1, 2, (3, 4), 5);
```

此示例展示了在解构赋值中对变量和丢弃同时使用隐式类型和显式类型的声明表达式。当找不到 _ 的声明时，simple_name _ 等同于 var _。

```csharp
void M1(out int i) { ... }

void M2(string _)
{
    M1(out _);      // Error: `_` is a string
    M1(out var _);
}
```

此示例展示了使用 var _ 来提供隐式类型的丢弃，当 _ 不可用时，因为它指定了外层作用域中的变量。

*结束示例*

## 12.18 条件运算符

?: 运算符称为条件运算符。有时也称为三元运算符。

```
conditional_expression
    : null_coalescing_expression
    | null_coalescing_expression '?' expression ':' expression
    | null_coalescing_expression '?' 'ref' variable_reference ':'
      'ref' variable_reference
    ;
```

如果存在 ref，则在条件运算符中不允许使用 throw 表达式（§12.16）。

形式为 b ? x : y 的条件表达式首先计算条件 b。然后，如果 b 为 true，则计算 x 并成为操作的结果。否则，计算 y 并成为操作的结果。条件表达式永远不会同时计算 x 和 y。

条件运算符是右结合的，这意味着操作是从右到左分组的。

示例：形式为 a ? b : c ? d : e 的表达式被求值为 a ? b : (c ? d : e)。结束示例

?: 运算符的第一个操作数应为可隐式转换为 bool 的表达式，或实现 operator true 的类型的表达式。如果不满足其中任何一个要求，将发生编译时错误。

如果存在 ref：
- 两个 variable_references 类型之间必须存在恒等转换，并且结果的类型可以是任一类型。如果任一类型为 dynamic，则类型推断优先选择 dynamic（§8.7）。如果任一类型为元组类型（§8.3.11），则当两个元组中相同序数位置的元素名称匹配时，类型推断会包含元素名称。
- 结果是一个变量引用，如果两个 variable_references 都是可写的，则它是可写的。

> *注意：* 当存在 ref 时，conditional_expression 返回一个变量引用，该引用可使用 = ref 运算符分配给引用变量，或作为引用/输入/输出参数传递。结束注意

如果不存在 ref，则 ?: 运算符的第二个和第三个操作数 x 和 y 控制条件表达式的类型：
- 如果 x 的类型为 X 且 y 的类型为 Y，则
  - 如果 X 和 Y 之间存在恒等转换，则结果为一组表达式的最佳公共类型（§12.6.3.15）。如果任一类型为 dynamic，则类型推断优先选择 dynamic（§8.7）。如果任一类型为元组类型（§8.3.11），则当两个元组中相同序数位置的元素名称匹配时，类型推断会包含元素名称。
  - 否则，如果存在从 X 到 Y 的隐式转换（§10.2），但不存在从 Y 到 X 的隐式转换，则 Y 为条件表达式的类型。
  - 否则，如果存在从 X 到 Y 的隐式枚举转换（§10.2.4），则 Y 为条件表达式的类型。
  - 否则，如果存在从 Y 到 X 的隐式枚举转换（§10.2.4），则 X 为条件表达式的类型。
  - 否则，如果存在从 Y 到 X 的隐式转换（§10.2），但不存在从 X 到 Y 的隐式转换，则 X 为条件表达式的类型。
  - 否则，无法确定表达式类型，将发生编译时错误。
- 如果只有 x 和 y 中的一个具有类型，并且 x 和 y 都可隐式转换为该类型，则该类型为条件表达式的类型。
- 否则，无法确定表达式类型，将发生编译时错误。

形式为 b ? ref x : ref y 的 ref 条件表达式的运行时处理包括以下步骤：
- 首先，`b` 被计算，并且 `b` 的 `bool` 值被确定：
  - 如果存在从 `b` 的类型到 `bool` 的隐式转换，则执行此隐式转换以生成 `bool` 值。
  - 否则，调用 `b` 的类型定义的 `true` 运算符以生成 `bool` 值。
- 如果上一步产生的 `bool` 值为 `true`，则计算 `x`，并且 resulting 变量引用成为条件表达式的结果。
- 否则，计算 `y`，并且 resulting 变量引用成为条件表达式的结果。

形式为 `b ? x : y` 的条件表达式的运行时处理包括以下步骤：
- 首先，`b` 被计算，并且 `b` 的 `bool` 值被确定：
  - 如果存在从 `b` 的类型到 `bool` 的隐式转换，则执行此隐式转换以生成 `bool` 值。
  - 否则，调用 `b` 的类型定义的 `true` 运算符以生成 `bool` 值。
- 如果上一步产生的 `bool` 值为 `true`，则计算 `x` 并将其转换为条件表达式的类型，这成为条件表达式的结果。
- 否则，计算 `y` 并将其转换为条件表达式的类型，这成为条件表达式的结果。

## 12.19 匿名函数表达式

### 12.19.1 通用

*匿名函数* 是表示“内联”方法定义的表达式。匿名函数本身没有值或类型，但可转换为兼容的委托或表达式树类型。匿名函数转换的求值取决于转换的目标类型：如果目标类型是委托类型，则转换求值为引用匿名函数定义的方法的委托值。如果目标类型是表达式树类型，则转换求值为表示方法结构为对象结构的表达式树。

> *注意：* 出于历史原因，匿名函数有两种语法风格，即 *lambda 表达式* 和 *匿名方法表达式*。对于几乎所有目的，*lambda 表达式* 比 *匿名方法表达式* 更简洁、更具表达力，而后者为向后兼容而保留在语言中。*结束注意*

```
lambda_expression
    : 'async'? anonymous_function_signature '=>' anonymous_function_body
    ;

anonymous_method_expression
    : 'async'? 'delegate' explicit_anonymous_function_signature? block
    ;

anonymous_function_signature
    : explicit_anonymous_function_signature
    | implicit_anonymous_function_signature
    ;
```
