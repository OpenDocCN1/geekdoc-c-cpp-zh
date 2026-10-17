
函数 `distance` 可能具有改变浮点环境的副作用。尽管如此，浮点环境是线程本地的，因此函数外部状态的变化与该变化是有顺序的，直到函数返回时观测值恢复。然而，这种副作用对于调用者并非如此。总体而言，该函数是无状态的、无力的且等幂的，特别是具有可重复属性。因为该函数可以在浮点环境没有属性的上下文中被调用，其中 `distance` 不是独立的，也不是无序的。尽管如此，在合理的情况下添加无序属性可以引入优化机会。

```c
double g(double y, double const x[static 2]) {
// 我们断言 distance 不会看到浮点环境的不同状态。
extern double distance(double const x[static 2]) [[unsequenced]];
y[0] = distance(x);
// return distance(x); // 替换为 y[0] 是有效的
}
```

# ISO/IEC 9899:2024(en)

## 6.8 语句和块 (Statements and blocks)

### 6.8.1 通用

#### 语法

```
statement:
  labeled-statement labeled-statement
unlabeled-statement:
  expression-statement
  attribute-specifier-sequence_opt primary-block
  attribute-specifier-sequence_opt jump-statement
primary-block:
  compound-statement
  selection-statement
  iteration-statement
secondary-block:
  statement
```

#### 语义

语句指定了要执行的操作。除另说明外，语句按顺序执行。可选的属性指定序列涉及相应的语句。

块可以是主块、次级块或与函数定义关联的块；允许将一组声明和语句分组为一个语法单元。每当块 B 在语法产生式作为包含块 A 的定义时，B 的标识符和字面量的范围不会扩展到 A 之外的部分。具有自动存储期的标识符，以及块作用域声明中的任何大小和类型运算符将被求值，没有初始化器的声明的表示变为不确定；按照执行顺序每次进行声明，就像它是语句一样，并且按照出现的顺序进行每个声明。

全表达式是指不属于另一个表达式、不属于声明符或抽象声明符的表达式。还有一个隐式表达式，其中可变修改类型的非常量表达式被求值；在该全表达式内部，不同大小表达式的求值彼此是无序的。在一个全表达式求值与下一个全表达式求值之间存在序列点。

> 注意 以下每一项都是全表达式：
>
> - 可变修改类型的声明符
>
> - 不属于复合字面量的部分的初始化器
>
> - 表达式语句中的表达式
>
> - 选择语句（if 或 switch）的控制表达式
>
> - while 或 do 语句的控制表达式
>
> - for 语句的每个（可选的）表达式
>
> - 返回语句中的（可选的）表达式

虽然常量表达式符合全表达式的定义，但其求值不依赖于也不产生任何副作用，因为全表达式的顺序影响对常量表达式无效。

前向引用：表达式和空语句 (`6.8.4`)，选择语句 (`6.8.5`)，迭代语句 (`6.8.6`)，返回语句 (`6.8.7`)。

## 6.8.2 标签语句 (Labeled statements)

#### 语法

```
label:
attribute-specifier-sequence_opt identifier :
attribute-specifier-sequence_opt case constant-expression :
attribute-specifier-sequence_opt default :
labeled-statement:
label statement
```

#### 约束

`case` 或 `default` 标签应出现在 `switch` 语句中。关于此类标签的进一步约束请见 `switch` 语句部分的讨论。

标签名称在函数内应是唯一的。

#### 语义

复合语句中的任何语句或声明之前都可以跟一个前缀，该前缀将一个标识符声明为标签。可选的属性指定符序列属于该标签。标签本身不改变控制流，控制流会继续通过。

前向引用：`goto` 语句 (`6.8.7.2`)，`switch` 语句 (`6.8.5.3`)。

## 6.8.3 复合语句 (Compound statement)

#### 语法

```
compound-statement:
{ block-item-list_opt }
block-item:
block-item
block-item-list block-item
block-item:
declaration
unlabeled-statement
label
```

#### 语义

作为函数体的复合语句连同参数类型列表以及可选的属性指定符序列，构成了与其出现的函数定义相关的块。否则，它是一个不同于任何其他块的块。标签的翻译方式就像其后面紧跟一个空语句。

## 6.8.4 表达式语句和空语句 (Expression and null statements)

#### 语法

```
expression-statement:
expression_opt ;
attribute-specifier-sequence expression;
```

#### 语义

属性指定符序列属于该表达式。表达式语句中的表达式为了其副作用被作为 `void` 表达式进行求值¹¹¹⁸²)

空语句（仅由一个分号组成）不执行任何操作。

¹¹¹⁸²)例如赋值和具有副作用的函数调用。

示例 1 如果函数调用仅为了其副作用被求值为表达式语句，可以通过通过类型转换将表达式转换为 `void` 表达式，来显式地丢弃其值：

```c
int p(int);
/* ... */
(void)p(0);
```

示例 2 在程序片段中

```c
char *s;
/* ... */
while (+s++) != '\0'
;
```

使用空语句为迭代语句提供了一个空循环体。

前向引用：迭代语句 (`6.8.6`)。

## 6.8.5 选择语句 (Selection statements)

#### 6.8.5.1 通用

#### 语法

```
if ( expression ) secondary-block
if ( expression ) secondary-block else secondary-block
switch ( expression ) secondary-block
```

`selection-statement:`

#### 语义

选择语句根据控制表达式的值，从一组辅助块中选择一个。

#### 6.8.5.2 if 语句

### 约束

`if` 语句的控制表达式应具有标量类型。

### 语义

在两种形式中，如果表达式不等于 `0`，则执行第一个语句。在 `else` 形式中，如果表达式等于 `0`，则执行第二个语句。如果通过标签到达第一个语句，则不执行第二个语句。

`else` 与语法允许的、词最近的一个 `if` 关联。

#### 6.8.5.3 switch 语句

### 约束

`switch` 语句的控制表达式应具有整数类型。

如果 `switch` 语句在一个可变修改类型的标识符的作用范围内关联有 `case` 或 `default` 标签，则整个 `switch` 语句应处于该标识符的作用范围内¹¹¹⁸³

每个 `case` 标签的表达式应为整数常量，且关联同一个 `switch` 语句的两个 `case` 表达式在转换后的值不能相同。一个 `switch` 语句最多关联一个 `default` 标签。（任何嵌套的 `switch` 语句都可以有一个 `default` 标签或与外层 `switch` 语句中 `case` 表达式值相同的常量表达式。）

> ¹¹¹⁸³即声明位于 `switch` 语句，或者位于包含该声明的块中 `switch` 的最后一个 `case` 或 `default` 标签之后。

#### 语义

`switch` 语句根据控制表达式的值，跳转到、进入或跳过 `switch` 主体，取决于 `default` 标签的存在以及 `switch` 主体上或内部任何 `case` 标签的值。`case` 或 `default` 标签仅在最近的封装 `switch` 语句内部可访问。

在控制表达式上执行整数程序。每个 `case` 标签中的常量表达式转换为控制表达式的提升类型。转换后的值与提升后的控制表达式匹配，控制跳转到匹配的 `case` 标签之后的语句或声明。否则，如果有 `default` 标签，控制跳转到 `default` 标签之后的语句或声明。如果没有匹配的 `case` 常量表达式且没有 `default` 标签，则不执行 `switch` 主体的体的任何部分。

#### 实现限制

如 `5.3.5.52` 所述，实现可能会限制 `switch` 语句中 `case` 值 的数量。

示例 在人工程序片段中

```c
switch (expr)
{
    int i = 4;
    f(i);
    case 0:
        i = 17;
        /* falls into default code *//
        default:
            printf("%d\n", i);
}
```

标识符具有自动存储 `duration`（在块内）但从未初始的对象，因此如果控制表达式非零值，对 `printf` 函数的调用将访问具有不确定表示的对象。同样，对函数 `f` 的调用无法到达。

## 6.8.6 迭代语句 (Iteration statements)

#### 6.8.6.1 通用

### 语法

```
iteration-statement:
while ( expression ) secondary-block
    do-while ( expression ) ;
    for ( declaration expression_opt ; expression_opt ; expression_opt ) secondary-block
```

### 约束

迭代语句的控制表达式应具有标量类型。

### 语义

迭代语句重复执行一个循环体，直到控制表达式为 `0`。无论是从迭代语句进入循环体还是通过跳转进入¹¹¹⁸⁴

如果控制表达式不是常量表达式¹¹¹⁸⁵且未执行以下操作，实现可以假设迭代语句终止

> ¹¹¹⁸⁴跳过的代码不执行。特别是，`for` 或 `while` 语句的表达式-`f` (`6.8.4`) 不执行。
>
> ¹¹¹⁸⁵省略的控制表达式被非零常量替换。

- 输出操作

- 访问 `volatile` 对象

- 同步或原子操作

#### 6.8.6.2 while 语句

控制表达式的求值发生在每次循环体执行之前。

#### 6.8.6.3 do 语句

控制表达式的求值发生在每次循环体执行之后。

#### 6.8.6.4 for 语句

```
for (clause-1; expression-2; expression-3) statement
```

行为如下：`expression-2` 是在每次循环体执行之前的控制表达式。`expression-3` 在每次循环体执行后作为 `void` 表达式求值。如果 `clause-1` 是声明，其声明的标识符的作用域是声明剩余部分以及整个循环；包括其他表达式；它在第一次求值控制表达式之前顺序执行。如果 `clause-1` 是表达式，它在第一次求值控制表达式之前作为 `void` 表达式求值¹¹¹⁷

`clause-1` 和 `expression-3` 可以省略。省略的 `expression-2` 被非零常量替换。

## 6.8.7 跳转语句 (Jump statements)

#### 6.8.7.1 通用

#### 语法

```
jump-statement:

goto identifier;
continue;
break;
return expression_opt;
```

#### 语义

跳转语句导致无条件跳转到其他。

#### 6.8.7.2 goto 语句

#### 约束

`goto` 语句中的标识符应命名位于封装函数某处的标签。`goto` 语句不应从可变修改类型标识符的作用域外跳转到该标识符的作用域内。

#### 语义

`goto` 语句会导致无条件跳转到包围函数中以命名标签为前缀的语句。

示例 1 有时，跳转到一组复杂语句的中间是方便的。下面的大纲基于以下三个假设展示了解决问题的一种种可能方法：

- 1. 通用初始化代码仅访问对当前函数可见的对象。
- 2. 通用初始化代码过于大，不宜重复。
- 3. 确定下一次操作位于循环头部。（例如，允许通过 `continue` 语句到达此处。）

```c
/* ... */
goto first_time;
for (;;) {
    // determine next operation
    /* ... */
    if (need to reinitialize) {
        // reinitialize-only code
        /* ... */
    }
    first_time:
        // general initialization code
        /* ... */
        continue;
    }
    // handle other operations
    /* ... */
}
```

示例 2 包含任何可变修改类型对象声明的 `goto` 语句是不符合规范的。但它是有效的。

```c
goto lab3; // 无效：进入 VLA 作用域。
{
    double a[n];
    a[j] = 4.4;
3:
    a[j] = 3.3;
    goto lab4; // 有效：在 VLA 作用域内。
    a[j] = 5.5;
lab4:
    a[j] = 6.6;
}
goto lab4; // 无效：进入 VLA 作用域。
```

## 6.8.7.3 continue语句

### 约束

`continue` 语句应出现在循环体内部或作为循环体。

#### 语义

`continue` 语句会导致跳转到最内包围迭代语句的循环继续点，即循环体的末尾。更具体地说，在以下每个语句中：

```c
while (/* ... */) {
    /* ... */
    continue;
    /* ... */
    contin:
}
d {
    /* ... */
    continue;
    /* ... */
    contin:
    while (/* ... */);
}
```

# ISO/IEC 9899:2024(en)

除非所示的 `continue` 语句位于包围的迭代语句中（在这种情况下它在该语句内解释），否则它等同于 `goto continue^{189}`

## 6.8.7.4 break语句

### 约束

`break` 语句应出现在 `switch` 体或循环体内部或作为其体。

#### 语义

`break` 语句终止最内包围 `switch` 或迭代语句的执行。

## 6.8.7.5 return语句

### 约束

带有表达式的 `return` 语句不出现在返回类型为 `void` 的函数中。不带表达式的 `return` 语句应出现在返回类型为 `void` 的函数中。

#### 语义

`return` 语句终止当前函数的执行并将控制权返回给其调用者。函数可以有任意数量的 `return` 语句。

如果执行了带有表达式的 `return` 语句，表达式的值作为函数表达式的值返回给调用者。如果表达式的类型与它所在函数的返回类型不同，则值的转换就像赋值给一个具有函数返回类型的对象一样^{190}

示例在：

```c
struct s { double i; } f(void) {
union {
    struct {
        int f1;
        struct s f2;
    } u1;
    struct {
        struct s f3;
        int f4;
    } u2;
} g;

struct s f(void) {
    return g.u1.f2;
}
/* ... */
g.u2.f3 = f();
};
```

这里没有未定义行为，尽管如果直接赋值（不使用函数调用来获取值），会有未定义行为。

>^{189}在第二个示例中跟随 `continue` 标签之后是一个空语句。第一个和第三个示例中的空语句是由标签（`6.8.7.3`）隐含的。
>
>^{190}`return` 语句不是赋值。`6.5.17.2` 的重叠限制不适用于函数返回情况。浮点值的表示范围或精度可能比类型暗示的更宽；可以使用强制转换移除这种额外的范围和精度。

# ISO/IEC 9829:2024(en)

### 6.9 外部定义

#### 6.9.1 一般

#### 语法

```
translation-unit:
    external-declaration
    translation-unit external-declaration
```

```
external-declaration:
    function-definition
    declaration
```

#### 约束

存储类说明符 `register` 不应出现在外部声明的声明说明符中。存储类说明符 `auto` 仅在类型推导时出现在外部声明的声明说明符中。

对于翻译单元中每个具有内部链接的标识符，外部定义不超过一个。此外，如果在表达式中使用具有内部链接的标识符，则该标识符应仅有一个外部定义，除非它是：

- `sizeof` 运算符的操作数，其结果为常量；
- `alignof` 运算符的操作数，其结果为常量；
- 通用选择的控制表达式；
- 通用选择的表达式；

#### 语义

存储类说明符 `register` 不应出现在外部声明的声明说明符中。存储类说明符 `auto` 仅在类型推导时出现在外部声明的声明说明符中。

对于翻译单元中每个具有内部链接的标识符，外部定义不超过一个。此外，如果在表达式中使用具有内部链接的标识符，则该标识符应仅有一个外部定义，除非它是：
