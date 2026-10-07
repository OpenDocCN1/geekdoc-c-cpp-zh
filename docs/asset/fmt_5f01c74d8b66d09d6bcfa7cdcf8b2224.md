
尽管如此，鼓励实现提供一致的结果，无论求值是在翻译期间还是执行期间进行的。

## 6 语句

除另有指示外，语句顺序执行。
语句：
- 带有标签的语句
- `[属性限定符序列_{可选}]` 表达式语句
- `[属性限定符序列_{可选}]` 复合语句
- `[属性限定符序列_{可选}]` 选择语句
- `[属性限定符序列_{可选}]` 迭代语句
- `[属性限定符序列_{可选}]` 跳转语句
- 声明语句
- `[属性限定符序列_{可选}]` try 块
可选的属性限定符序列用于语句。

## 6.1 带有标签的语句

带有标签的语句可以标记。
带有标签的语句：
- `属性限定符序列_{可选}` 语句 : 语句
- `属性限定符序列_{可选}` 表达式 : 语句
- `属性限定符序列_{可选}` 默认 : 语句
属性限定符序列用于语句。带有标签的语句用于 `goto`。带有标签的语句的标识符出现在其所在处。带有标签的 `if` 语句声明了标识符。默认标签仅出现在 `switch` 语句中。

## 6.2 表达式语句

表达式语句通过执行
表达式语句：
表达式
表达式语句的类型（5）。表达式语句的后续是空 语句。[注意：大多数表达式是赋值或函数调用。带有表达式的语句是空 语句。表达式的 `if` 语句用于 `for` 和 `while` 迭代语句（6.5）。——注意]

### 6.3 复合语句或块

如果复合语句的子语句是单个语句而非复合语句。
复合语句：
`{` 语句序列`_{可选}` `}`
语句序列：
语句

复合语句定义作用域（3.3）。复合语句的后续是空 语句。

## 6.4 选择语句

- 选择语句选择若干种控制流。
选择语句：
    - `if (条件)` 语句
    - `if (条件)` 语句 `else` 语句
    - `switch (条件)` 语句
条件：
    - 表达式
    - `属性限定符序列_{可选}` 声明 = 初始化器列表
    - `属性限定符序列_{可选}` 语句序列

如果字面量类型的表达式用在需要整数常量表达式的上下，则该类型必须有一个到整数或未转义枚举的非显式转换，且该转换函数是 `constexpr`。如果类型限定符出现在类型限定符序列中，标识符的类型是从初始化器推导出的（见 7.1.6.4）。

条件中的声明引入的名称（通过类型限定符序列或条件的限定符引入）其作用域从声明点一直持续受条件控制的语句的结束。如果名称在受条件控制的最外块中被重新声明，则重新声明名称的声明是错误的。[示例：

```
if (int x = f()) {
  int x;
  // 初始化器，声明 x
} else {
  int x;
  // 初始化器，声明 x
}
```
示例

- 条件的规则同时适用于选择语句以及 `for`、`while` 语句（6.5）。限定符不应指定函数或数组。

- 非 `switch` 语句中初始化声明的条件的值是所声明变量在文中转换为 `bool` 的值（见 4 节）。如果该值是错误的，则程序是错误的。`switch` 语句中初始化声明的条件的值是所声明变量的值（如果它具有整数或枚举类型），或者该变量被隐式转换为整数或枚举类型。表达式作为条件的值是表达式的值，对于 `switch` 语句以外的语句转换为 `bool` 的值；如果该条件是错误的，

# ISO/IEC 14882:2011(E)

程序格式不正确。当用法无歧义时，条件的值将简单地称为“条件”。

如果一个条件在语法上可以被解析为表达式或块作用域名的声明，则它被解释为声明。

在条件的声明说明符序列（`decl-specifier-seq`）中，每个声明说明符都应当是类型指定说明符（`type-specifier`）或 `constexpr`。

## 6.4.1 if 语句 [smt.if]:

如果条件（6.4）为真，则执行第一个子语句。如果存在 `else` 语句且条件为假，则执行第二个子语句。在它的第二种形式（即包含 `else` 的形式）中，如果第一个语句也是一个 `if` 语句，则内部语句应当包含一个 `else` 部分。85

## 6.4.2 switch 语句 [smt.switch]:

`switch` 语句根据条件的值将控制转移到多个语句中的一个。
条件应当为整数类型、枚举类型，或存在单一非显式到整数的转换的类类型（12.3）。如果条件是类类型，则通过调用该转换函数对条件进行转换，转换结果在本节的剩余部分将替代原始条件。执行隐式类型提升。`switch` 语句内的任何语句应当被标记一个或多个 `case` 标签，如下：

`case-expression` :

其中，常量表达式应当是 `switch` 条件提升后类型的转换常量表达式（5.19）。同一个 `switch` 中的，任意两个 `case` 常数在转换为 `switch` 条件的提升类型后值不应相同。

`switch` 语句中最多有一个形式为

`default` :

的标签。

`switch` 语句可以嵌套；`case` 或 `default` 标签与最小的闭合 `switch` 关联。

当执行 `switch` 语句时，它会被求值，并与每个 `case` 常数进行比较。如果其中一个 `case` 常数等于条件的值，则控制将传递到匹配标签之后的语句。如果没有 `case` 常数匹配条件，且存在 `default` 标签，则控制将传递到由 `default` 标签标记的语句。如果既没有 `case` 也没有 `default`，则 `switch` 语句中的任何语句都不会执行。

`case` 和 `default` 标签本身不改变控制流，控制流将不受阻地跨越此类标签继续。要退出 `switch`，使用 `break`, 6.6.1。[注：通常，作为 `switch` 主体的子语句是复合语句，`case` 和 `default` 标签出现在包含其中的顶层语句上

> 85) 换句话说，`else` 与最近的未使用的 `if` 关联。

## § 6.4.2

132 ISO/IEC 2011 – 版权所有

该（复合）子语句，但这不是强制的。声明可以出现在任何 `switch` 语句的子语句中。—— 脚注结束

## 6.5 迭代语句指定

[stmt.iter]

+ 1 迭代语句循环。
`iteration-statement`:
`while (condition)` `statement`
`do` `statement` `while (expression);`
`for (for-item-statement condition_opt; expression_opt)` `statement`
`for (for-range-declaration : for-range-initializer)` `statement`
`for-item-statement`:
`expression-statement`
`simple-declaration`
`for-range-declaration`:
`attribute-specifier-seq_opt` `decl-specifier-seq` `declarator`
`for-item-initializer`:
`expression`
`broadcast-list`

关于范围声明（`range-declaration`）中可选的属性说明符序列（`attribute-specifier-seq`），请参阅 8.3。[注：`for` 语句以分号结束。—— 脚注结束]

+ 2 迭代语句中的子语句隐式定义了一个块作用域（3.3），在每次循环时都会进入和退出该作用域。

如果迭代语句中的子语句是单个语句而非复合语句，则它被重写为包含该语句的复合语句。例如：

```
while (x >= 0)
int i;
```

可以重写为
```
while (x >= 0) {
  int i;
}
```

3 `while` 语句结束后，该变量不再在作用域内。4 注：迭代语句中的条件参见 6.4。]

### 6.5.1 while 语句

[stmt.while]

`while` 子语句重复执行，直到条件（6.4）为假。在 `while` 语句执行前进行测试。

2 如果 `while` 语句的条件是声明，则该变量的作用域从声明点延伸到 `while` 语句结束。例如：
```
struct A {
  int val;
  A(int i) : val(i) {}
  operator bool() { return val != 0; }
};
int i = 0;
while (A i)
```
在 `while` 循环中，会调用构造函数和析构函数，一次用于条件，一次用于迭代。—— 结束

### 6.5.2 do 语句

+ 1 `do` 语句重复执行，直到表达式为假。`do` 语句的测试在执行之后。

### 6.5.3 for 语句

+ 1 `for` 语句 `for (for-init-statement condition_opt; expression_opt) statement` 等同于

```
{
  for-init-statement
  while (condition) {
    statement
  }
}
```
其中 `for-init-statement` 中声明的名字与条件处于相同的作用域；表达式指定在每次迭代后进行递增；2 条件和表达式均可以省略。缺失条件将隐含的 `while` 等同于 `while(true)`。

3 如果 `for-init-statement` 是声明，则声明的作用域延伸到 `for` 语句结束。例如：
```
int i = 42;
a[10];
for (int i = 0; i < 10; i++)
a[i] = i;
```

## 6.5.4 基于范围的 for 语句 [stmt.ranged]

1 对于形式为

`for (range-declaration : expression) statement`
令 `range-init` 等同于带圆括号的表达式 (`expression`)

并且对于形式为

`for (range-declaration : braced-init-list) statement`

在每种情况下，基于范围的 `for` 语句等同于

```
auto && _range = range-init;
for ( auto _begin = begin-expr,
     _end = end-expr;
     __begin = end;
     ++_begin ) {
  range-declaration = _begin;
 statement
}
```

其中 `_range`、`__begin` 和 `__end` 是仅用于说明的变量，`_RangeT` 是表达式的类型，`begin-expr` 和 `end-expr` 确定：

   * 如果 `RangeT` 是数组类型，`begin-expr` 和 `end-expr` 分别为 `_range` 和 `_range + _bound`，其中 `_bound` 是未知大小或不完整类型的数组，程序格式不正确；
   * 如果 `RangeT` 是类类型，未限定的 `begin` 和 `end` 在 `RangeT` 的作用域中按类成员查找（3.4.5）进行，且其中一个（或两者）至少找到声明，`begin-expr` 和 `end-expr` 分别为 `_range.begin()` 和 `_range.end()`；
   * 其他，`begin-expr` 和 `end-expr` 分别为 `begin(_range)` 和 `end(_range)`，其中 `begin` 和 `end` 通过参数依赖查找（3.4.2）进行。对于此名称查找，`std` 是一个关联命名空间。

86 此使用的顶层逗号运算符可以重新解释为范围声明中初始化声明符之间的分隔符。

# ISO/IEC 14882:2011(E)

示例：

```cpp
int array[5] = { 1, 2, 3, 4, 5 };
for (int& x : array)
    x *= 2;
```
结束示例

+ 2 在 `for-range-declaration` 的 `decl-specifier-seq` 中，每个 `decl-specifier` 均应为 `type-specifier` 或 `constexpr`。

## 6.6 跳转语句 [stmt.jump]

+ 1 跳转语句无条件地转移控制流。
`jump-statement`:
    `break;`
    `continue;`
    `return expression_stmt;`
    `return braced-init-list;`
    `goto identifier;`

+ 2 当离开作用域时（无论如何实现），在该作用域内构造的具有自动存储生存期（3.7.3）的对象将按照其构造的反逆顺序进行析毁。[注：对于临时对象，见 12.2.—结束注] 离开作用域、离开一个块或跳过一个已初始化的具有自动存储生存期的变量，将触发在转移点处于作用域内但在目标点不在作用域内的对象的析毁。（6.7 关于进入块）。[注：然而，程序可以通过调用 `std::exit()` 或 `std::abort()` (18.5) 终止，而无需析毁具有自动存储生存期的对象.—结束注]

### 6.6.1 break 语句 [stmt.break]

+ 1 `break` 语句只能出现在迭代语句或 `switch` 语句中，并导致控制传递到最小包含它的迭代语句或 `switch` 语句；控制传递到已终止的语句（如果有）。

### 6.6.2 continue 语句 [stmt.cont]

+ 1 `continue` 语句只能出现在迭代语句中，并导致控制传递到最小包含它的迭代语句的循环延续点，即循环的末尾。更具体地说，在以下每个语句中

```cpp
while (foo) {
    // ...
    continue;
}
for (... ; ;) {
    // ...
    continue;
}
while (foo) {
    // ...
    continue;
}
```

一个不包含在嵌套迭代语句中的 `continue` 等同于 `goto`。

### 6.6.3 return 语句 [stmt.return]

+ 1 函数通过 `return` 语句返回到其调用者。

+ 2 既没有表达式也没有大括号初始化列表的 `return` 语句只能用于不返回值的函数、返回类型为 `void` 的函数、构造函数（12.1）或析构函数（12.4）。

带有非 `void` 类型表达式的 `return` 语句只能用于返回值的函数；该表达式的值被返回给函数的调用者。该表达式的值被隐式转换为其所出现的函数的返回类型。`return` 语句可能涉及临时对象的构造以及拷贝或移动（12.2）。[注：为了在重载解析中进行选择时，与 `return` 语句相关的拷贝或移动操作可以被视为右值（12.8).—结束注] 带有大括号初始化列表的 `return` 语句通过指定的初始化列表，通过拷贝初始化（8.5.4）对从函数返回的对象的对象的引用进行初始化。[示例：]

```cpp
std::string f(const char* p, int x) {
    return {p,x};
}
```
—结束示例

从函数末尾流出等于无值的返回；这在返回值的函数会导致未定义行为。

+ 3 带有 `void` 类型表达式的 `return` 语句只能用于返回类型为 `void` 的函数；该表达式在函数返回其调用者之前求值。

### 6.6.4 goto 语句 [stmt.goto]

+ 1 `goto` 语句无条件地将控制转移到标识符标记的语句。该标识符应为位于当前函数的标签（6.1）。

### 6.7 声明语句 [stmt.dcl]

+ 1 声明语句向块中引入一个或多个标识符；其形式为
`declaration-statement;`
`block-declaration`

如果引入的标识符之前在外部块中声明过，则该外部块在当前块的剩余部分被隐藏，之后它将恢复其功能。

+ 2 具有自动存储生存期（3.7.3）的变量在每次执行声明语句时都会初始化。在块中声明的对象离开块时析毁（6.6）。

+ 3 可以进入块，但不能以跳过初始化声明的方式进入。程序从一个自动存储生存期变量不在作用域内的点跳转到一个格式错误的点，除非该变量具有类类型、具有默认构造函数和简单析构函数的类型、这些类型之一的 cv 修饰版本，或上述任何类型，且在没有初始化器的情况下声明的（8.5）。[示例：]

```cpp
void f() {
    // 格式错误：跳转进入 a 的作用域
    goto ly;
    X = 1;
    // ...
ly:
    goto ly;
    // OK，跳转意味着离开了 a 的析构调用
    // 随后是构造调用
}
```
