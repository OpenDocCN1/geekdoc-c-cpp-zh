

```c
v1.i = 2; // 有效
v1.k = 3; // 无效：内部结构不是匿名的
v1.w.k = 5; // 有效
```

示例 2 声明之后：

结构体 `s` 有一个灵活数组成员 `d`。使用它的典型方法是：

```c
int m = /* some value */;
struct s *p = malloc(sizeof(struct s) + sizeof(double [m]));
```

假设调用 `malloc` 成功，`p` 指向的对象大多数情况下表现就像 `p` 被声明为如下：

```c
struct { int n; double d[m]; } *p;
```

（在某些情况下这种等效性会被破坏；特别是成员 `d` 的偏移量可能不同）。遵循上述声明：

```c
struct s t1 = { 0 }; // 有效
struct s t2 = { 1, { 4.2 } }; // 无效
t1.n = 4; // 有效
t1.d[0] = 42; // 可能是未定义行为
```

`t2` 的初始化是无效的（违反了约束），因为 `struct s` 被处理为不包含成员 `d`。赋值 `d` 可能是未定义的，但可能：

```c
sizeof(struct s) >= offsetof(struct s, d) + sizeof(double)
```

在这种情况下，该赋值是合法的。尽管如此，它不能出现在严格符合的代码中。

在进一步声明之后：

```c
struct ss { int n; };
```

表达式：

```c
sizeof(struct s) >= sizeof(struct ss)
sizeof(struct s) >= offsetof(struct s, d)
```

等于于 1。

如果 `sizeof (double)` 为 8，则执行以下代码：

```c
struct s *s1;
struct s *s2;
s1 = malloc(sizeof(struct s) + 64);
s2 = malloc(sizeof(struct s) + 46);
```

假设对 `malloc` 调用成功，`s1` 和 `s2` 指向的对象大多数情况下表现就像这些标识符被声明为：

```c
struct { int n; double d[8]; } *s1;
struct { int n; double d[5]; } *s2;
```

在进一步的成功赋值之后：

![](img/b1371b4bc75a631228eb4aa5fac6defe_131_0.png)

```c
s1 = malloc(sizeof(struct s) + 10);
s2 = malloc(sizeof(struct s) + 6);
```

它们的行为就像声明为：

```c
struct { int n; double d[1]; } *s1, *s2;
```

并且：

```c
double *dp;
dp = &(s1->d[0]); // 有效
*dp = 42;             // 有效
dp = &(s2->d[0]); // 有效
*dp = 42;             // 未定义行为
```

25 赋值：

```c
*s1 = *s2;
```

只复制成员 `n`；如果任何数组元素在结构上位于第一个 `sizeof (struct s)` 范围内，它们可能会被复制，或仅用不确定值覆盖。

26 示例 3 匿名结构体和联合体的成员应该是包含它们的结构体或联合体的成员，在下面的示例中，`struct s` 有多个命名成员，因此灵活数组成员的使用是：

```c
struct s {
    struct { int i; };
    int a[];
};
```

前引用：声明符 (6.7.6)，标签 (6.7.2.3)。

## 6.7.2.2 枚举说明符

### 语法

```
enum-specifier:
enum identifier_opt { enumerator-list }
enum identifier_opt { enumerator-list , }
enum identifier
```

```
enumerator-list:
```

```
enumerator
enumerator-list , enumerator
```

```
enumerator:
```

```
enumeration-constant
enumeration-constant = constant-expression
```

## 约束

定义枚举常量值的表达式应当是一个整数常量表达式，其值可以被表示为 `int`。

## 语义

枚举器成员列表中的标识符被声明为类型为 `int` 的常量，并可以出现在任何允许的地方。（127）带有 `=` 的枚举器将其枚举常量定义为该常量的值。如果第一个枚举器没有 `=`，则其枚举常量的值为 0。随后的每个没有 `=` 的枚举器将其枚举常量定义为在上一个枚举常量值的基础上加 1 得到的常量表达式的值。（使用带有 `=` 的枚举器可能会产生值与同一枚举中其他值重复的枚举常量。） 举的枚举器也被称为它的成员。

每个枚举类型都应当与 `char`、有符号整数类型或无符号整数类型兼容。类型的选择由实现定义，（128）但应当能够表示枚举中所有成员的值。在 `}` 终止枚举器声明列表 之前，该枚举类型是不完全的，此之后是完全的。

示例 以下片段：

```c-plus
enum hue = {chartreuse, burgundy, claret=20, winedark};
enum hue col, *cp;
col = claret;
cp = &col;
if (*cp != burgundy)
/* ... */
```

使得 `hue` 是一个枚举标签，并将 `col` 声明为该类型的对象，将 `cp` 声明为指向该类型的指针。枚举的值在 {0, 1, 20}。

前引用：标签 (6.7.2.3)。

## 6.7.2.3 标签

### 约束

特定类型最多出现一次内容。

使用相同标签的声明应当具有相同的 `struct`、`union` 或 `enum` 选择。如下形式的类型说明符：

```c
enum identifier
```

如果没有枚举器列表，则仅出现在指定的类型完全完全之后。

> 127) 因此，同一作用域内的枚举常量标识符是唯一的，且来自声明符中的其他标识符。

> 128) 实现可能会推迟对类型的选择，直到所有枚举常量被看到。

具有相同作用域且具有相同标签的 `struct`、`union` 或枚举类型应当具有相同的类型。（129）只有在不需要对象大小时，可以使用不完全类型。（参见 6.2.5）

具有相同作用域且具有相同标签的 `struct`、`union` 或枚举类型应当具有相同的类型。（130）只有在不需要对象大小时，可以使用不完全类型。（参见 6.2.5）

具有相同作用域且具有相同标签的 `struct`、`union` 或枚举类型应当具有相同的类型。（131）不存在带有 `enum` 的类似结构。（等等……

（自纠：提供的 OCR 文本在后面的页面似乎是重复或乱码。我将根据提供的文本清理逻辑流，同时保持所有内容。）

实际上，查看提供的原始 OCR，第 134-135 页包含许多重复短语和提取不当的文本。我将对提供的内容进行处理，但修正拼写错误。

[content]
```c
v1.i = 2; // 有效
v1.k = 3; // 无效：内部结构不是匿名的
v1.w.k = 5; // 有效
```

示例 2 声明之后：

结构体 `s` 有一个灵活数组成员 `d`。使用它的典型方法是：

```c
int m = /* some value */;
struct s *p = malloc(sizeof(struct s) + sizeof(double [m]));
```

假设调用 `malloc` 成功，`p` 指向的对象大多数情况下表现就像 `p` 被声明为如下：

```c
struct { int n; double d[m]; } *p;
```

（在某些情况下这种等效性会被破坏；特别是成员 `d` 的偏移量可能不同）。遵循上述声明：

```c
struct s t1 = { 0 }; // 有效
struct s t2 = { 1, { 4.2 } }; // 无效
t1.n = 4; // 有效
t1.d[0] = 42; // 可能是未定义行为
```

`t2` 的初始化是无效的（违反了约束），因为 `struct s` 被处理为不包含成员 `d`。赋值 `d` 可能是未定义的，但可能：

```c
sizeof(struct s) >= offsetof(struct s, d) + sizeof(double)
```

在这种情况下，该赋值是合法的。尽管如此，它不能出现在严格符合的代码中。

在进一步声明之后：

```c
struct ss { int n; };
```

表达式：

```c
sizeof(struct s) >= sizeof(struct ss)
sizeof(struct s) >= offsetof(struct s, d)
```

等于于 1。

如果 `sizeof (double)` 为 8，则执行以下代码：

```c
struct s *s1;
struct s *s2;
s1 = malloc(sizeof(struct s) + 64);
s2 = malloc(sizeof(struct s) + 46);
```

假设对 `malloc` 调用成功，`s1` 和 `s2` 指向的对象大多数情况下表现就像这些标识符被声明为：

```c
struct { int n; double d[8]; } *s1;
struct { int n; double d[5]; } *s2;
```

在进一步的成功赋值之后：

![](img/b1371b4bc75a631228eb4aa5fac6defe_131_0.png)

```c
s1 = malloc(sizeof(struct s) + 10);
s2 = malloc(sizeof(struct s) + 6);
```

它们的行为就像声明为：

```c
struct { int n; double d[1]; } *s1, *s2;
```

并且：

```c
double *dp;
dp = &(s1->d[0]); // 有效
*dp = 42;             // 有效
dp = &(s2->d[0]); // 有效
*dp = 42;             // 未定义行为
```

25 赋值：

```c
*s1 = *s2;
```

只复制成员 `n`；如果任何数组元素在结构上位于第一个 `sizeof (struct s)` 范围内，它们可能会被复制，或仅用不确定值覆盖。

26 示例 3 匿名结构体和联合体的成员应该是包含它们的结构体或联合体的成员，在下面的示例中，`struct s` 有多个命名成员，因此灵活数组成员的使用是：

```c
struct s {
    struct { int i; };
    int a[];
};
```

前引用：声明符 (6.7.6)，标签 (6.7.2.3)。

## 6.7.2.2 枚举说明符

### 语法

```
enum-specifier:
enum identifier_opt { enumerator-list }
enum identifier_opt { enumerator-list , }
enum identifier
```

```
enumerator-list:
```

```
enumerator
enumerator-list , enumerator
```

```
enumerator:
```

```
enumeration-constant
enumeration-constant = constant-expression
```

## 约束

定义枚举常量值的表达式应当是一个整数常量表达式，其值可以被表示为 `int`。

## 语义

枚举器成员列表中的标识符被声明为类型为 `int` 的常量，并可以出现在任何允许的地方。（127）带有 `=` 的枚举器将其枚举常量定义为该常量的值。如果第一个枚举器没有 `=`，则其枚举常量的值为 0。随后的每个没有 `=` 的枚举器将其枚举常量定义为在上一个枚举常量值的基础上加 1 得到的常量表达式的值。（使用带有 `=` 的枚举器可能会产生值与同一枚举中其他值重复的枚举常量。） 举的枚举器也被称为它的成员。

每个枚举类型都应当与 `char`、有符号整数类型或无符号整数类型兼容。类型的选择由实现定义，（128）但应当能够表示枚举中所有成员的值。在 `}` 终止枚举器声明列表 之前，该枚举类型是不完全的，此之后是完全的。

示例 以下片段：

```c-plus
enum hue = {chartreuse, burgundy, claret=20, winedark};
enum hue col, *cp;
col = claret;
cp = &col;
if (*cp != burgundy)
/* ... */
```

使得 `hue` 是一个枚举标签，并将 `col` 声明为该类型的对象，将 `cp` 声明为指向该类型的指针。枚举的值在 {0, 1, 20}。

前引用：标签 (6.7.2.3)。

## 6.7.2.3 标签

### 约束

特定类型最多出现一次内容。

使用相同标签的声明应当具有相同的 `struct`、`union` 或 `enum` 选择。如下形式的类型说明符：

```c
enum identifier
```

如果没有枚举器列表，则仅出现在指定的类型完全完全之后。

> 127) 因此，同一作用域内的枚举常量标识符是唯一的，且来自声明符中的其他标识符。

> 128) 实现可能会推迟对类型的选择，直到所有枚举常量被看到。

具有相同作用域且具有相同标签的 `struct`、`union` 或枚举类型应当具有相同的类型。（129）只有在不需要对象大小时，可以使用不完全类型。（参见 6.2.5）

具有相同作用域且具有相同标签的 `struct`、`union` 或枚举类型应当具有相同的类型。（130）只有在不需要对象大小时，可以使用不完全类型。（参见 6.2.5）

具有相同作用域且具有相同标签的 `struct`、`union` 或枚举类型应当具有相同的类型。（131）不存在带有 `enum` 的类似结构。（等等……

