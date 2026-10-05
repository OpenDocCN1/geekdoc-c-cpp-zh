

# 示例 2 在程序片段中

```
char *s;
/* ... ... */
while (*s++ != '\0')
  ;
```

空语句（a null statement）用于为迭代语句提供一个空的循环体。

# 示例 3 空语句也可以用于在复合语句的结束大括号 `}` 之前携带一个标签（label）。

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

### 实现限制

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

