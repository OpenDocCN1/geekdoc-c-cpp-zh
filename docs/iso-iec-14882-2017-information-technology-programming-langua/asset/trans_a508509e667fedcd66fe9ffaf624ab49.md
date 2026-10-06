

# ISO/IEC 14882:2017(E)

```cpp
alignas(a) int n;               // error: 二义转换
struct B { int n : a; };     // error: 二义转换
// end example
```

# ISO/IEC 14882:2017(E)

# 9 语句

+ 1 除另有外，语句按顺序执行。
  statement:
    label-statement
  attribute-specifier-seq_qopt expression-statement
  attribute-specifier-seq_qopt compound-statement
  attribute-specifier-seq_qopt selection-statement
  attribute-specifier-seq_qopt iteration-statement
  attribute-specifier-seq_qopt jump-statement
  declaration-statement
  attribute-specifier-seq_qopt try-block
  init-statement:
    expression-statement
    simple-declaration
  condition:
    expression
    attribute-specifier-seq_qopt decl-specifier-seq brace-or-equal-initializer

+ 2 条件的规则仅适用于选择语句以及 for 和 while 语句（9.5）。声明不应指定函数或数组。decl-specifier-seq 不应定义类或枚举。如果 `auto` 类型说明符出现在 decl-specifier-seq 中，则被声明的标识符的类型将按照第 10.1.7.4 节所述从初始化器推导出。

+ 3 由条件引入的名称（无论是通过 decl-specifier-seq 引入还是通过条件的声明）其作用域从声明点开始，直到该条件所控制的语句结束。如果在受条件控制的语句的最外层块中重新声明了该名称，则重新声明该名称的声明为格式非法（ill-formed）。[示例:

```cpp
if (int x = {}) {
 // 格式非法，x 的声明
}
```

+ 4 在 switch 语句以外的声明中初始化的条件值，是被声明变量在文中转换为 bool 的值（第 7 节）。如果该转换格式非法，则程序为格式非法。在 switch 语句中初始化的条件值，如果被声明变量具有整数或枚举类型，则为该变量的值；否则，为该值隐式转换为整数或枚举类型。作为表达式的条件值，对于 switch 以外的语句，是表达式在文中转换为 bool 的值；如果该转换格式非法，则程序为格式非法。在用法无二义的情况下，条件的值被称为“条件”。

+ 5 如果一个条件在语法上可以被解析为表达式或块作用域名称的声明，则它被解释为声明。

+ 6 在条件的 decl-specifier-seq 中，每个 decl-specifier 应当是类型说明符或 `constexpr`。

# ISO/IEC 14882:2017(E)

# 9.1 标记语句

+ 1 语句可以被标记。

```cpp
labeled-statement:
  attribute-specification-seq<sub>opt⟩ identifier : statement
  attribute-specification-seq<sub>opt⟩ case constant-expression : statement
  attribute-specification-seq<sub>opt⟩ default : statement
```

可选的 attribute-specification 应仅出现在同一语句中。标记声明了标识符。标识符的唯一用途是 goto 的目标。标记的作用域是其所在的函数。标记不应在函数内部被引用。标记可以在其声明之前的 goto 语句中使用。标记有自己的空间，且与其他标识符不冲突。注意：标记的名称可能与同一作用域内的另一个声明或外层作用域的模板参数相同：(6.4.1) 忽略标记。——注结束

+ 2 case 和 default 标记应当出现在 switch 语句中。

# 9.2 表达式语句

+ 1 表达式语句的形式为

```cpp
expression-statement:
  expression<sub>opt⟩
```

该表达式是一个丢弃值表达式（第 8 节）。表达式语句的所有副作用在执行下一条语句之前均完成。缺少表达式的表达式语句是调用语句。注意：大多数语句都是表达式语句——通常是赋值或函数调用。语句可以用于在复合语句结束前携带标记，并为迭代语句（如 while 语句 (9.5.1)）提供空体。——注结束

# 9.3 复合语句或块

+ 1 使得在提供复合语句（也等效地称为“块”）的地方可以使用单个语句。

```cpp
compound-statement:
  statement-seq<sub>opt⟩
  statement-seq
```

复合语句定义了一个块语句（6.3）。注意：声明是一个语句（9.7）。——注结束

# 9.4 选择语句

+ 1 选择语句从多个控制流中选择一种，

```cpp
selection-statement:
  if const-expression (init-statement<sub>opt⟩ , condition) statement
  if const-expression (init-statement<sub>opt⟩ , condition) statement else statement
  switch (init-statement<sub>opt⟩ , condition) statement
```

参见第 11.3 节关于 goto 中的可选 attribute-specification。注意：带有分号的 init-statement。——注结束。在第 9 节中，substatement（子语句）指的是语法表示中出现的包含语句或语句。

