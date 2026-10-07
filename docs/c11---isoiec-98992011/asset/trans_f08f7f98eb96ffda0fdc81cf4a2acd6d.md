

## 6.7.10 静态断言 (Static assertions)

语法

```
static_assert_declaration:
    _Static_assert ( constant-expression , string-literal ) ;
```

约束

+ 2 常量表达式应当不等于 0。

语义

+ 3 常量表达式应当是一个整数常量表达式。如果常量表达式的值不等于 0，则该声明没有作用。否则，则违反了约束，且实现应产生一条诊断信息，其中包含字符串字面量的文本，但对于基本源字符集中的字符，不要求显示在消息中。

前向引用：诊断 (7.2)。

## ISO/IEC 9899:2011 (E)

## 6.8 语句与块 (Statements and blocks)

语法

+ 1 语句：
- 标记语句 (labeled-statement)
- 复合语句 (compound-statement)
- 表达式语句 (expression-statement)
- 选择语句 (selection-statement)
- 迭代语句 (iteration-statement)
- 跳转语句 (jump-statement)

语义

+ 2 语句指定了要执行的操作。除另有规定外，语句顺序执行。

+ 3 块允许将一组声明和语句分组为一个语法单元。具有自动存储生存期的对象的初始化器，以及具有块作用域的标识符的变长数组，在每次按照执行顺序到达声明时，都会进行求值，并将值存储在对象中（包括在没有初始化器的对象中存储一个不确定的值），就像它是一个语句一样，并且按照声明出现的顺序在每个声明内部进行处理。

+ 4 完整表达式是指不是其他表达式或声明符部分的表达式。以下每一项都是完整表达式：不属于复合字面量部分的初始化器；表达式语句中的表达式；选择语句（if 或 switch）的控制表达式；while 或 do 语句的控制表达式；for 语句中的每个（可选）表达式；return 语句中的（可选）表达式。在完整表达式的求值与下一个待求值的表达式的求值之间存在一个序列点。

前向引用：表达式与空语句 (6.8.3)，选择语句 (6.8.4)，迭代语句 (6.8.5)，return 语句 (6.8.6)。

## 6.8.1 标记语句 (Labeled statements)

语法

+ 1 标记语句：
- 标识符 : 语句
- case 常量表达式 : 语句
- default : 语句

约束

+ 2 case 或 default 标记只能出现在 switch 语句中。对此的进一步约束在 switch 语句下讨论。

+ 3 标记名称在函数内应当唯一的。

## 语义

+ 4 任何语句之前都可以有一个前缀，用于将一个标识符声明为标记名称。标记本身不改变控制流，控制流将越过标记继续执行。

前向引用：goto (6.8.6.1)，switch 语句 (6.8.4.2)。

## 6.8.2 复合语句 (Compound statement)

## 语法

+ 1 复合语句：
 { block-item-list-opt }

block-item-list:
 block-item
 block-item-list block-item

block-item:
 declaration
 statement

## 语义

+ 2 复合语句是一个块。

## 6.8.3 表达式语句与空语句 (Expression and null statements)

## 语法

+ 1 表达式语句：
 expression_opt ;

## 语义

+ 2 表达式语句中的表达式被求值为 void 表达式，以产生其副作用。(153)

+ 3 空语句（仅由一个分号组成）不执行任何操作。

+ 4 示例 1 如果函数仅为了其副作用而作为表达式语句调用，可以通过强制类型转换将表达式转换为 void 表达式，从而显式地丢弃其返回值。

```
int p(int);
/* ... */
(void)p(0);
```

> 153 如下赋值和函数调用可以产生副作用。

+ 5 示例 2 在程序片段中

```
char *s;
/* ... */
while (*s++ != '\0')
    ;
```

使用空语句来为迭代语句提供一个空循环。

+ 6 示例 3 空语句也可以用于在复合语句的结束括号 } 之前携带一个标记。

```
while (loop1) {
    /* */
    while (loop2) {
        /* */
        if (want_out)
            goto end_loop1;
        /* ... */
    }
    /* ... */
end_loop1;
}
```

前向引用：迭代语句 (6.8.5)。

## 6.8.4 选择语句 (Selection statements)

## 语法

+ 1 选择语句：
    if ( expression ) statement
    if ( expression ) statement else statement
    switch ( expression ) statement

## 语义

+ 2 选择语句根据控制表达式的值，在一组语句中进行选择。

+ 3 选择语句是一个块，其作用域是其包含块作用域的严格子集。每个关联的语句也是一个块，其作用域是选择语句作用域的严格子集。

## 6.8.4.1 if语句

## 约束

+ 1 if 语句的控制表达式应当具有标量类型。

## 语义

+ 2 在两种形式中，如果表达式与 0 比较，则执行第一个语句。在 else 形式中，如果表达式比较不等于 0，则执行第二个语句。

## 6.8.4.2 switch语句

## 约束

+ 1 switch 语句的控制表达式应当具有整数类型。

+ 2 for 语句的声明部分应当仅声明存储类为 auto 或 register 的标识符。（注：此处原文逻辑可能有误，按原文翻译）
+ 3 switch 语句的控制表达式应当具有整数类型。

## 语义

+ 4 switch 语句根据控制表达式的值跳转到 switch 之后的语句。如果 case 匹配，跳转到关联的语句。否则，如果存在 default 标记，则跳转语句。

## 6.8.5 迭代语句 (Iteration statements)

## 语法

+ 1 迭代语句：
    while ( expression ) statement
    do statement while ( expression ) ;
    for ( expression_opt ; expression_opt ; expression_opt ) statement
    for ( declaration expression_opt ; expression_opt ) statement

## 约束

+ 1 迭代语句的控制表达式应当具有标量类型。

+ 2 for 语句的声明部分应当仅声明存储类为 auto 或 register 的标识符。

## 语义

+ 1 迭代语句导致一个称为循环体的语句被重复执行，直到控制表达式与 0 比较为止。无论循环体是从迭代语句进入还是通过跳转进入，重复都会发生。

+ 2 迭代语句是一个块，其作用域是其包含块作用域的子集。循环体也是一个块，其作用域是迭代语句作用域的子集。

