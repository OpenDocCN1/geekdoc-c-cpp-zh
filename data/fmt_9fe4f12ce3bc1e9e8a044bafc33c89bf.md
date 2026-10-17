
以全括号格式进行。

注意，通常情况下，全括号和最少括号形式的初始化不容易引起混淆。

示例 7 一完成数组类型的初始化形式涉及类型定义名。给定声明：

```c
typedef int a[]; // OK - 在块作用域内声明
```

声明：

```c
A a = { 1, 2 }, b = { 3, 4, 5 };
```

由于不完全类型的规则，它等同于：

```c
int a[] = { 1, 2 }, b[] = { 3, 4, 5 };
```

示例 8 声明：

```c
char s[] = "abc", t[3] = "abc";
```

定义了“普通”字符数组对象 `s` 和 `t`，其元素用字符字符串字面量初始化。该声明等同于：

```c
char s[] = { 'a', 'b', 'c', '\0' };
t[] = { 'a', 'b', 'c' };
```

数组的内容是可修改的。另一方面，声明：

```c
char *p = "abc";
```

`p` 的类型为“指向字符的指针”，并初始化为指向一个长度为 4 个元素的“字符数组”类型的对象。

示例 9 结构体初始化：

```c
struct {
    int x;
    int y;
} s = { 1, 2 };
```

示例 10 联合体初始化：

```c
union {
    int i;
    float f;
} u = { .i = 1 };
```

示例 11 数组初始化：

```c
int arr[3] = { 1, 2, 3 };
```

示例 12 嵌套数组初始化：

```c
int arr[2][2] = { {1, 2}, {3, 4} };
```

示例 13 静态断言：

```c
static_assert(1 == 1, "error");
```

## 6.8 语句

### 语法

```c
statement:
- labeled-statement
- compound-statement
- expression-statement
- selection-statement
- iteration-statement
- jump-statement
```

### 语义

语句指定执行的操作。

#### 6.8.1 L语句

### 语法

```c
labeled-statement:
- identifier : statement
- case constant-expression : statement
- default : statement
```

### 约束

`case` 或 `default` 标签仅出现在 `switch` 语句中。此类标签的进一步约束在 `switch` 语句部分讨论。标签名在函数范围内应该是唯一的。

### 语义

标签本身不改变控制流，控制流不受阻地继续。

**引用：** `goto` (6.8.6.1)，`switch` 语句 (6.8.4.2)。

#### 6.8.2 复合语句

### 语法

```c
compound-statement:
  { block-item-list opt }

  block-item-list:
    block-item
    block-item-list block-item

  block-item:
    declaration
    statement
```

### 语义

复合语句是一个块。

#### 6.8.3 表达式语句和空语句

### 语法

```c
expression-statement:
  expression_opt ;
```

### 语义

表达式语句中的表达式作为 void 表达式进行求值。¹153

空语句（仅由分号组成）不执行任何操作。

示例 1 如果函数调用仅为了副作用作为表达式语句求值，可以通过强制转换将表达式转换为 void 表达式来显式丢弃其值：

```c
int p(int);
/* ... * */
(void)p(0);
```

> 153) 这些赋值以及具有副作用的函数调用。

## 示例 2 在程序片段中

```
char *s;
/* ... ... */
while (*s++ != '\0')
  ;
```

空语句（a null statement）用于为迭代语句提供一个空的循环体。

## 示例 3 空语句也可以用于在复合语句的结束大括号 `}` 之前携带一个标签（label）。

```
while (loop1) {
  /* ... ... */
  while (loop2) {
    /* ... ... */
    if (want_out)
      goto end_loop1;
  }
  /* ... ... */
}
end_loop1;
;
```

前向：迭代语句（6.8.5）。

## 6.8.4 选择语句

### 语法

```
selection-statement:
if ( expression ) statement
if ( expression ) statement else statement
switch ( expression ) statement
```

### 语义

选择语句根据控制表达式的值，从一组语句中选择一个。

选择语句是一个块（block），其作用域是其包含块作用域的严格子集。每个子语句也是一个块，其作用域是选择语句作用域的严格子集。

### 6.8.4.1 if 语句

### 约束

if 语句的控制表达式应具有标量类型（scalar type）。

### 语义

在两种形式中，如果表达式的值不等于 0，则执行第一个子语句。在 `else` 形式中，如果表达式等于 0，则执行第二个子语句。如果通过标签到达第一条语句，则不执行第二条语句。

3 `else` 与语法允许的最近的先一个 `if` 关联。

### 6.8.4.2 switch 语句

### 约束

1 switch 语句的控制表达式应具有整数类型。

2 如果 switch 语句在具有可变修饰类型（variably modified type）的标识符作用域内有一个关联的 `case` 或 `default` 标签，则整个 switch 语句应位于该标识符的作用域内.¹¹¹154)

3 每个 `case` 标签的表达式是相同的整数常量表达式，且同一个 switch 语句中没有两个 `case` 常量表达式在转换后具有相同的值。一个 switch 语句中最多有一个 `default` 标签。（任何包含的 switch 语句可以有一个 `default` 标签或值与外层 switch 语句中的 `case` 常量表达式重复的常量表达式。）

### 语义

4 switch 语句根据控制表达式的值、`default` 标签的存在以及 switch 体或内部任何 `case` 标签的值，导致控制跳转到、进入或跳过 switch 体语句。`case` 或 `default` 标签仅在最近的包含它的 switch 语句内可访问。

5 整数运算在控制表达式上进行。每个 `case` 标签中的常量表达式被转换为控制表达式的提升类型（promoted type）。如果转换后的值与提升后的控制表达式匹配，控制跳转到匹配的 `case` 标签之后的语句。否则，如果存在 `default` 标签，控制跳转到该标签的语句。如果没有匹配的转换表达式且没有 `default` 标签，则不执行 switch 体的任何部分。

## 实现限制

6 如 5.2.4.1 节所述，实现可能会限制 switch 语句中 `case` 值的数量。

> ¹¹¹154) 也就是说，声明要么在 switch 语句之前，要么在包含该声明的块中对应的最后一个 `case` 或 `default` 标签之后。

```
switch (expr)
{
    int i = 4;
    f(i);
    case 0:
        i = 17;
        /* 穿透 default 代码 */
    default:
        printf("%d\n", i);
}
```

对象标识符 `i` 以原子存储存在，因此控制表达式具有非零值，对 `printf` 函数的调用将访问一个不确定的值。同样，对函数 `f` 的调用无法到达。

## 6.8.5 迭代语句

### 语法

+   iteration-statement:

while ( expression ) statement

do statement while ( expression )

for ( [ declaration ] expression ; [ expression ] ) statement

### 约束

+   迭代语句的控制表达式应具有标量类型。

+   for 语句的声明部分应具有 `auto` 类型。

### 语义

+   如果控制表达式的值等于 0，迭代语句会导致重复执行循环体。`do-while` 语句的作用域是其包含块作用域的严格子集。

+   `for` 语句的声明作用域是迭代语句的作用域的严格子集。

+   `for` 语句的控制表达式在每次执行循环体之前执行。`expression-3` 在每次执行循环体后执行。¹¹¹155}

> ¹¹¹155 被跳转的语句不执行。特别是对于 `for` 语句的 `clause-1`。

> ¹¹¹156 省略的控制表达式被替换为非零常量表达式。

### 6.8.5.1 while 语句

控制表达式在每次执行循环体之前执行。

### 6.8.5.2 do 语句

控制表达式在每次执行循环体后执行。

### 6.8.5.3 for 语句

`for ( [ declaration ] expression ; [ expression ] ) statement` 行为如下：`expression-2` 在每次执行循环体之前执行。`expression-3` 在每次执行循环体后执行（作为空表达式）。如果 `clause-1` 是声明，其声明的标识符的作用域是整个循环。如果 `clause-1` 是表达式，它在第一次执行控制表达式之前执行。¹¹¹157}

> ¹¹¹157 这种设计是为了在无法证明终止的情况下允许编译器移除空循环。

## 6.8.6 跳跃语句

### 语法

```
jump-statement:
goto identifier ;
continue ;
break;
return expression_{opt};
```

> ¹¹¹158 省略的 `expression-2` 被替换为非零常量。

### 语义

2 跳转语句导致无条件跳转到另一个地方。

### 6.8.6.1 goto 语句

### 约束

1 `goto` 语句中的标识符应命名包含函数内的某个标签。`goto` 语句从从可变修饰类型标识符的作用域外部跳转到其内部内部。

### 语义

2 `goto` 语句导致无条件跳转到所在函数内以该标签标记的语句。

# 示例 2 `goto` 语句不允许跳转过具有可变类型对象的声明。在作用域内的 `goto` 跳跃是允许的。

```c
goto lab3;
// 无效：进入 VLA（变长数组）的作用域。
{
    double a[n];
    a[j] = 4.4;
l3:
    a[j] = 3.3;
    goto lab4;    // 有效：在 VLA 作用域内。
    a[j] = 5.5;
lab4:
    a[j] = 6.6;
}
goto lab4; // 无效：进入 VLA 作用域。
```

## 6.8.6.2 continue 语句

### 约束

continue 语句只能出现在循环体内或作为循环体。

### 语义

continue 语句会导致跳转到最小包含它的迭代语句的循环继续部分；即跳转到循环体的结束。更精确地说，在每个语句中：

```c
while (/* ... */) do { for (/* ... ... */) {
    /* ... */          /* ... */
    continue;         continue;
    /* ... */          /* ... */
contin;           contin;           contin;
} while (/* ... */);
}}
```

除非 continue 语句显示在一个嵌套的迭代语句中（在这种情况下它在该语句内解释），否则它等同于 `goto contin;`¹⁵⁹

## 6.8.6.3 break 语句

### 约束

### 语义

break 语句只能出现在 switch 体或循环体内，或作为其体。

break 语句终止最小包含它的 switch 或迭代语句的执行。

> ¹⁵⁹) `contin:` 标签之后是一个空语句。

## 6.8.6.4 return 语句

### 约束

带有表达式的 return语句应出现在返回类型为 `void` 的函数中。不带表达式的 return语句只能出现在返回类型为 `void` 的函数中。

### 语义

return 语句终止当前函数的执行并将控制返回给调用者。函数可以有任意数量的 return语句。

如果执行了带有表达式的 return语句，表达式的值将作为函数调用表达式的值返回给调用者。如果表达式的类型与它所在函数的返回类型不同，则该值将像赋值一样转换为具有该函数返回类型的对象¹160)

示例 输入：

```c
struct s { double i; } f(void);
union {
  struct {
    int f1;
    struct s f2;
  }
  struct {
    struct s f3;
    int f4;
  } u2;
} g;
struct s f(void)
{
  return g.u.f2;
}
/* ... */
g.u2.f3 = f();
```

这里不存在未定义行为，尽管如果直接进行赋值（不使用函数调用来获取值）将会产生未定义行为。

> 160) return 语句不是赋值。子句 6.5.16.1 的重叠限制不适用于函数返回的情况。浮点值的表示可能比类型暗示的具有更宽范围或精度；可以使用类型转换来消除这种额外的范围和精度。

## 6.9 外部定义

### 语法

```c
translation-unit:
  external-declaration
  translation-unit external-declaration

external-declaration:
  function-definition
  declaration
```

### 约束

在外部声明的标识符中不应出现存储类限定符 `auto` 和 `register`。

在一个翻译单元中，每个用内部链接（internal linkage）声明的标识符最多只能有一个外部定义。此外，如果一个用内部链接声明的标识符在表达式中使用（除了作为 `sizeof` 或 `_Alignof` 符的操作数，且其结果为整数常量），则在该翻译单元中该标识符必须恰好有一个外部定义。

### 语义

如 5.1.1.1 节所示，预处理后的程序文本单元是翻译单元，它由一系列外部声明组成。这些声明被称为“外部的”，是因为它们出现在任何函数之外（因此具有文件作用域）。如 6.7 所示，如果声明还导致为标识符命名的对象或函数预留存储空间，则为定义。

外部定义是一个也是函数（内联定义除外）或对象的定义的外部声明。如果一个用外部链接声明的标识符在表达式中使用（除了作为 `sizeof` 或 `_Alignof` 符的操作数，且其结果为整数常量），则在整个程序中该标识符恰好有一个外部定义；否则，最多有一个。^{161)

> 161) 因此，如果一个用外部链接声明的标识符没有在表达式中使用，则不需要外部定义。

## 6.9.1 函数定义

### 语法

```c
function-definition:
de declaration-specifiers declarator declaration-list_opt compound-statement
de declaration-list:
de declaration
de declaration-list declaration
```

### 约束

在函数定义中声明的标识符（即函数名）应具有函数定义中声明符部分指定的函数类型¹162)

函数的返回类型应为 `void` 或除数组类型外的完整对象类型。

存储类限定符（如果有）应为 `extern` 或 `static`。

如果声明符包含参数列表，则每个参数的类型都应声明，但 `void` 类型的特殊情况除外。如果声明符包含标识符列表¹³参数的类型应在随后的声明列表中声明。在任何情况下，参数的类型均根据 7.6.3 进行调整；结果类型应为完整对象类型。

### 语义

7 函数定义中的声明符指定了函数的名称及其参数的标识符。如果声明符包含参数列表，该列表还指定了所有参数的类型；声明符同时也作为对同一翻译单元后续调用的函数原型。如果声明符包含标识符列表，参数的类型在随后的声明列表中声明。

8 如果接受变数量参数的函数没有以省略号表示结尾的参数列表，则行为是未定义的。

9 每个参数都具有自动存储期；其标识符是一个左值¹¹⁴ 参数的存储布局是不指定的。

10 进入函数时，将计算每个可变参数的大小表达式，并将每个参数表达式的值按赋值的方式转换为参数的类型。（数组表达式和函数设计符作为参数在调用前已转换为指针。）

11 在所有参数赋值后，执行构成函数定义体的复合语句。

12 如果到达了终止函数的 `}`，且调用者使用了函数调用的值，则行为是未定义的。

13 示例 1 在以下代码中：

```c
extern int max(int a, int b)
{
    return a > b ? a : b;
}
```

`extern` 是存储类限定符，`int` 是类型限定符；`max(int a, int b)` 是函数声明符；

  { return a > b ? a : b; }

是函数体。类似的类似的定义使用了标识符列表形式进行参数声明。
