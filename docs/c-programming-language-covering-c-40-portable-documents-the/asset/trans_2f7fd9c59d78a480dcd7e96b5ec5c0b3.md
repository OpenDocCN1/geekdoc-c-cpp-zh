

> **埃里克·利珀特** 我基本同意上面的注释，但还想补充一点：当代码编写者试图表达“这个变量的存储类型并不重要；重要的是变量的含义，而不是它的实现细节”时，使用 `var` 很合适。例如，我经常会编写如下代码：`var attributes = ParseMethodAttributes();`——我在这里表达的是，返回的结果究竟是 `AttributeSyntax[]` 还是 `List<AttributeSyntax>` 并不重要。重要的是，属性集合已经完成了解析。

> **比尔·瓦格纳** 我坦率承认，自己大量使用 `var`。事实上，除了简单类型以外，我几乎在所有情况下都会使用隐式类型变量。我认为，对变量具有语义上的理解，比具有语法上的理解重要得多。在 Chris 的示例中，`GetPerson()` 从逻辑上讲会返回 `Person`、`IPerson`，或者某个派生自 `Person` 或实现了 `IPerson` 的类型。在所有这些情况下，我都能接受这种程度的模糊性。即使不知道变量的确切类型，我也能理解“一个表示某种类似人员的对象的变量”这一概念。

在局部变量声明中声明的局部变量，其作用域是包含该声明的代码块。若在文本位置上先于该局部变量的局部变量声明符引用该局部变量，则会发生错误。在局部变量的作用域内，声明另一个具有相同名称的局部变量或常量属于编译时错误。

声明多个变量的局部变量声明，等价于使用相同类型声明多个单独变量。此外，局部变量声明中的变量初始化器，与紧接在声明之后插入的一条赋值语句完全对应。

### 示例

```
void f() {
    int x = 1, y, z = x * 2;
}
```

与以下代码完全对应：

```
void f() {
    int x; x = 1;
    int y;
    int z; z = x * 2;
}
```

在隐式类型的局部变量声明中，被声明的局部变量的类型被视为与用于初始化该变量的表达式类型相同。例如：

```
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
```

上述隐式类型局部变量声明与以下显式类型声明完全等价：

```
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
```

> **彼得·塞斯托夫特** 虽然可以声明局部的（编译时）常量，但在 C# 中不能声明只读的局部变量或只读的方法参数；而 Standard ML 和 Scala 有 `val`，F# 有 `let`，Java 有 `final`。作为一名老派的函数式程序员，我对此感到有些遗憾；很多时候，我只是想给一个值命名，而不是声明一个可变变量。`using` 语句（§8.13）确实允许我声明不可变的局部变量，但这种方式既繁琐又不符合惯用写法（因此会让大多数 C# 开发人员感到困惑），而且它只能用于局部变量，不能用于方法参数。

## 8.5.2 局部常量声明

局部常量声明用于声明一个或多个局部常量。

```
local-constant-declaration:
    const type constant-declarators

constant-declarators:
    constant-declarator
    constant-declarators , constant-declarator

constant-declarator:
    identifier = constant-expression
```

局部常量声明的类型指定了该声明所引入常量的类型。类型后面跟着一个常量声明符列表，其中每个常量声明符都会引入一个新常量。常量声明符由以下部分组成：用于命名常量的标识符、一个 `"="` 标记，以及用于给出常量值的常量表达式（§7.19）。

局部常量声明的类型和常量表达式必须遵循常量成员声明（§10.4）的相同规则。

局部常量的值可以在表达式中通过简单名称（§7.6.2）获取。

局部常量的作用域是包含该声明的代码块。若在文本位置上先于该常量声明符引用局部常量，则会发生错误。在局部常量的作用域内，声明另一个具有相同名称的局部变量或常量属于编译时错误。

声明多个常量的局部常量声明，等价于使用相同类型声明多个单独的常量。

## 8.6 表达式语句

表达式语句计算给定的表达式。表达式计算出的值（如果有）将被丢弃。

```
expression-statement:
    statement-expression ;
```

- statement-expression:
- invocation-expression
- object-creation-expression
- assignment
- post-increment-expression
- post-decrement-expression
- pre-increment-expression
- pre-decrement-expression

并非所有表达式都允许作为语句。尤其是，诸如 x + y 和 x == 1 这类仅计算一个值（该值随后会被丢弃）的表达式，不允许作为语句。

表达式语句的执行过程如下：计算其中包含的表达式，然后将控制权转移到表达式语句的终点。如果表达式语句可达，则其终点也是可达的。

> **乔恩·斯基特** 偶尔会有人建议，应该允许方法声明自己永不结束，也就是说，它们永远不会正常返回。按照这种方案，它们唯一可能终止的方式就是通过异常。单元测试库中的 `Assert.Fail` 就是这类方法的一个明显例子。

如果这种特性真的出现，那么调用这类方法的表达式语法的终点将不可达。只是偶尔地，这种语法可以避免编写一个你明知永远不会执行的“占位”返回语句或 `throw` 语句。我猜想，从语言和实现两方面来看，由此增加的复杂性，都超过了它所带来的那一点微小收益。

> **埃里克·利珀特** 过去，负责标准化 ECMAScript 语言的委员会曾提出过一种“never”类型，其语义正如 Jon 所描述的那样。我同意在 C# 中拥有这种类型会很好，但在目前看来，其成本可能超过相对有限的收益。

## 8.7 选择语句

选择语句根据某个表达式的值，从多个可能的语句中选择一个执行。

```
selection-statement:
  if-statement
  switch-statement
```

### 8.7.1 if 语句

if 语句根据布尔表达式的值选择一个语句执行。

```
if-statement:
    if ( boolean-expression ) embedded-statement
    if ( boolean-expression ) embedded-statement else embedded-statement
```

`else` 部分与语法所允许的、在文本上最近的前一个 `if` 相关联。因此，以下形式的 if 语句：

```
if (x) if (y) F(); else G();
```

等价于：

```
if (x) {
    if (y) {
        F();
    }
    else {
        G();
    }
}
```

if 语句的执行过程如下：

- 计算布尔表达式（§7.20）。
- 如果布尔表达式的结果为 `true`，则将控制权转移到第一个嵌入语句。当且如果控制权到达该语句的终点时，控制权将转移到 if 语句的终点。
- 如果布尔表达式的结果为 `false`，并且存在 `else` 部分，则将控制权转移到第二个嵌入语句。当且如果控制权到达该语句的终点时，控制权将转移到 if 语句的终点。
- 如果布尔表达式的结果为 `false`，且不存在 `else` 部分，则将控制权转移到 if 语句的终点。

如果 if 语句可达，并且布尔表达式不具有常量值 `false`，则 if 语句的第一个嵌入语句可达。

如果存在第二个嵌入语句，则当 if 语句可达且布尔表达式不具有常量值 `true` 时，该嵌入语句可达。

如果其至少一个嵌入语句的终点可达，则 if 语句的终点可达。此外，对于不带 `else` 部分的 if 语句，如果该 if 语句可达且布尔表达式不具有常量值 `true`，则其终点也可达。

### 8.7.2 switch 语句

switch 语句选择一个带有关联 switch 标签的语句列表来执行，该 switch 标签与 switch 表达式的值相对应。

```
switch-statement:
    switch ( expression ) switch-block

switch-block:
    { switch-sections_opt }
```

