

## ISO/IEC 14882:2020(E)

8 在条件表达式的 decl-specifier-seq 中，每个 decl-specifier 必须为 type-specifier 或 constexpr。

## 8.2 Labeled statement [stmt.label]

1 一个语句可以带标签。

```
labeled-statement:
  attribute-specifier-seq_opt identifier : statement
  attribute-specifier-seq_opt case constant-expression : statement
  attribute-specifier-seq_opt default : statement
```

可选的 attribute-specifier-seq 属于该标签。identifier 标签声明了该标识符。identifier 标签的唯一用途是作为 goto 的目标。标签的作用域为其出现的函数。标签在函数内不得被重新声明。标签可以在其声明之前在 goto 语句中使用。标签拥有自己的命名空间，并且不会干扰其他标识符。

> [Note 1: 一个标签可以与同一作用域中的其他声明或封闭作用域中的模板参数同名。非限定名称查找 (6.5.2) 忽略标签。 — end note]

2 case 标签和 default 标签只能出现在 switch 语句中。

## 8.3 Expression statement [stmt.expr]

1 表达式语句的形式为

```
expression-statement:
  expression_opt ;
```

表达式为 discarded-value 表达式 (7.2.3)。在执行下一个语句之前，表达式语句的所有副作用都会完成。表达式缺失的表达式语句称为空语句。

> [Note 1: 大多数语句都是表达式语句——通常是赋值或函数调用。空语句用于在复合语句的 } 之前携带标签，并为迭代语句（如 while 语句 (8.6.2)）提供空体。 — end note]

## 8.4 Compound statement or block [stmt.block]

1 复合语句（也称为块）将一系列语句组合成单个语句。

```
compound-statement:
  { statement-seq_opt }
statement-seq:
  statement
  statement-seq statement
```

复合语句定义了一个块作用域 (6.4)。

> [Note 1: 声明是一个语句 (8.8)。 — end note]

## 8.5 Selection statements [stmt.select]

### 8.5.1 General [stmt.select.general]

1 选择语句选择其中一个控制流。

```
selection-statement:
  if constexpr_opt ( init-statement_opt condition ) statement
  if constexpr_opt ( init-statement_opt condition ) statement else statement
  switch ( init-statement_opt condition ) statement
```

参见 9.3.4 了解条件中的可选 attribute-specifier-seq。

> [Note 1: init-statement 以分号结束。 — end note]

2 选择语句中的子语句（else 形式的 if 语句中的每个子语句）隐式定义了一个块作用域 (6.4)。如果选择语句中的子语句是单个语句且不是复合语句，则相当于将其重写为包含原始子语句的复合语句。

> [Example 1:
>
> ```
> if (x)
>     int i;
> ```
>
> 可以等价地重写为
>
> ```
> if (x) {
>     int i;
> }
> ```
>
> 因此在 if 语句之后，i 不再在作用域内。 — end example]

### 8.5.2 The if statement [stmt.if]

1 如果条件 (8.5) 的结果为 true，则执行第一个子语句。如果选择语句存在 else 部分且条件结果为 false，则执行第二个子语句。如果第一个子语句是通过标签到达的，则条件不被求值且第二个子语句不被执行。在第二种形式的 if 语句（包含 else 的形式）中，如果第一个子语句也是 if 语句，则该内部 if 语句必须包含 else 部分。88

2 如果 if 语句为 if constexpr 形式，则条件的取值必须为类型为 bool 的上下文转换常量表达式 (7.7)；这种形式称为 constexpr if 语句。如果转换后条件的值为 false，则第一个子语句为 discarded 语句，否则如果存在则第二个子语句为 discarded 语句。在封闭模板实体 (13.1) 的实例化期间，如果条件在其实例化后不是值相关的，则 discarded 子语句（如果有）不被实例化。[Note 1: discarded 语句中的 odr-use (6.3) 不要求实体必须被定义。 — end note]

出现在此类 if 语句中的 case 或 default 标签必须与同一 if 语句内的 switch 语句 (8.5.3) 相关联。在 constexpr if 语句的子语句中声明的标签 (8.2) 只能由同一子语句中的语句 (8.7.6) 引用。

[Example 1:

```
template<typename T, typename ... Rest> void g(T&& p, Rest&& ...rs) {
    // ... handle p

    if constexpr (sizeof...(rs) > 0)
        g(rs...);        // never instantiated with an empty argument list
}
```

```
extern int x;        // no definition of x required
```

```
int f() {
    if constexpr (true)
        return 0;
    else if (x)
        return x;
    else
        return -x;
}
```

— end example]

3 形式为

```
if constexpr_opt ( init-statement condition ) statement
```

的 if 语句等价于

```
{
    init-statement
    if constexpr_opt ( condition ) statement
}
```

并且形式为

```
if constexpr_opt ( init-statement condition ) statement else statement
```

的 if 语句等价于

```
{
    init-statement
    if constexpr_opt ( condition ) statement else statement
}
```

在 do 语句中，子语句会重复执行，直到表达式的值变为 `false`。测试在每次执行语句后进行。

### 8.6.4 The for statement

for 语句

```
for ( init-statement condition_opt ; expression_opt ) statement
```

等价于

```
{
    init-statement
    while ( condition ) {
        statement
        expression ;
    }
}
```

除非 *init-statement* 中声明的名称与 *condition* 中声明的名称处于同一声明区域，并且除非 *statement*（未被另一个迭代语句包围）中的 `continue` 会在重新求值 *condition* 之前执行 *expression*。

> [Note 1: 因此第一个语句为循环指定初始化；*condition* (8.5) 指定在每次迭代之前求序的测试，使得当条件变为 `false` 时退出循环；*expression* 通常指定在每次迭代之后求序的递增。 — end note]

*condition* 和 *expression* 可以省略一个或两个。缺失的 *condition* 使隐含的 `while` 子句等价于 `while(true)`。

如果 *init-statement* 是一个声明，则所声明的名称的作用域延伸到 for 语句的末尾。

[Example 1:

```
int i = 42;
int a[10];

for (int i = 0; i < 10; i++)
    a[i] = i;

int j = i;        // j = 42
```

— end example]

### 8.6.5 The range-based for statement

基于范围的 for 语句

```
for ( init-statement_opt for-range-declaration : for-range-initializer ) statement
```

等价于

```
{
    init-statement_opt
    auto &&range = for-range-initializer ;
    auto begin = begin-expr ;
    auto end = end-expr ;
    for ( ; begin != end ; ++begin ) {
        for-range-declaration = *begin ;
        statement
    }
}
```

其中

- (1.1) — 如果 *for-range-initializer* 是一个 *expression*，则视为被括号包围（以便逗号运算符不会被重新解释为分隔两个 *init-declarators*）；
- (1.2) — *range*、*begin* 和 *end* 仅为阐述而定义的变量；并且
- (1.3) — *begin-expr* 和 *end-expr* 如下确定：

### 8.7.4 The return statement

函数通过 `return` 语句返回给其调用者。

`return` 语句的 *expr-or-braced-init-list* 称为其操作数。没有操作数的 `return` 语句只能用于返回类型为 `cv void` 的函数、构造函数 (11.4.5) 或析构函数 (11.4.7)。操作数为 void 类型的 `return` 语句只能用于返回类型为 `cv void` 的函数。具有其他操作数的 `return` 语句只能用于返回类型不是 `cv void` 的函数；`return` 语句通过拷贝初始化 (9.4) 从操作数初始化（显式或隐式）函数调用的结果 glvalue 或 prvalue 对象。

> [Note 1: `return` 语句可能涉及构造函数调用以执行操作数的拷贝或移动，如果它不是 prvalue 或其类型与函数的返回类型不同。`return` 语句相关联的拷贝操作可以被省略或转换为移动操作，如果返回的是自动存储期变量 (11.10.6)。 — end note]

[Example 1:

```
std::pair<std::string,int> f(const char* p, int x) {
  return {p,x};
}
```

— end example]

结果对象的析构函数可能会被调用 (11.4.7, 14.3)。

[Example 2:

```
class A {
  ~A() {}
};
A f() { return A(); }   // error: destructor of A is private (even though it is never invoked)
```

— end example]

从构造函数、析构函数或返回类型为 `cv void` 的非协程函数末尾流出等价于没有操作数的 `return`。否则，从 `main` (6.9.3.1) 或协程 (9.5.4) 以外的函数末尾流出会导致未定义行为。

调用结果的拷贝初始化在 `return` 语句操作数所建立的完整表达式末尾的临时对象销毁之前求序，而后者又在包含 `return` 语句的块的局部变量销毁 (8.7) 之前求序。

### 8.7.5 The co_return statement

```
coroutine-return-statement:
    co_return expr-or-braced-init-list_opt ;
```

协程通过 `co_return` 语句或在挂起时 (7.6.2.4) 返回给其调用者或恢复者 (9.5.4)。协程不得包含 `return` 语句 (8.7.4)。

> [Note 1: 对于此判定，`return` 语句是否被 discarded 语句 (8.5.2) 包围无关紧要。 — end note]

`co_return` 语句的 *expr-or-braced-init-list* 称为其操作数。设 `p` 为命名协程 promise 对象的左值 (9.5.4)。`co_return` 语句等价于：

```
{ S; goto final-suspend; }
```

其中 *final-suspend* 为 9.5.4 中定义的阐述用标签，`S` 定义如下：

- 1. 如果操作数是 *braced-init-list* 或非 void 类型的表达式，则 `S` 为 `p.return_value(expr-or-braced-init-list)`。表达式 `S` 必须为类型为 void 的 prvalue。
- 2. 否则，`S` 为 *compound-statement* `{ expression_opt ; p.return_void(); }`。表达式 `p.return_void()` 必须为类型为 void 的 prvalue。

如果 `p.return_void()` 是一个有效的表达式，则协程末尾流出等价于没有操作数的 `co_return`；否则协程末尾流出会导致未定义行为。

### 8.7.6 The goto statement

`goto` 语句无条件地将控制转移到标识符所标记的语句。标识符必须为位于当前函数中的标签 (8.2)。

