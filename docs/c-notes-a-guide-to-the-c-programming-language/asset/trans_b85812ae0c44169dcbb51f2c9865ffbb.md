
有时中断语句的正常顺序很方便，可以使用以下之一：

```
interruption-statement =
| break ;
| continue ;
| return expr ;
| goto identifier ;
|
```

break 语句导致最小的外层重复或 switch 语句终止。

continue 语句导致最小的外层重复语句的可重复子语句终止。执行将从 for 的增量部分或 do 或 while 的测试部分恢复。

return 语句终止包含函数的执行。如果指定了 expr，则它在转换为函数声明的类型后成为函数的返回值；如果没有表达式，则函数返回的值是垃圾。在每个函数体的末尾，都有一个隐式的无表达式 return。

goto 语句指定执行应从标识符标记的语句处恢复。最后，带标签的语句的语法为

```
labeled-statement =
    identifier : statement
```

并作为 goto 语句的目标。在同一个函数中，只能出现给定标签的此类定义之一。由于带标签的语句是语句的合法形式，因此可以按顺序出现任意数量的标签。实际上，break 很少需要，continue 从不需要，而 goto 的需要比那还要少。由此可知，如果避免使用 goto，则永远不需要使用标签。同样，将 return 语句的数量最小化也是良好的风格；为了可读性，在函数末尾恰好有一个是最好的。

## 2.7 初始化器语法

所有数据初始化器采用以下形式

```
initializer ::= =opt { expr | initializer-list ,opt } |
```

并且所有函数初始化器都是以下形式的复合语句

```
compound-statement ::= { [ { local-declaration | type-definition } ]opt { statement }opt }
```

```
statement =
| expr ;                 % assignments and function calls
| compound-statement     % for grouping
| selection-statement
| repetition-statement
| interruption-statement
| labeled-statement
| ;                      % null statement
|
```

```
selection-statement =
| if ( logical-expr ) statement
  ( else statement )opt
| switch ( expr ) switch-statement-group
|
```

```
switch-statement-group =
{ [ { local-declaration | type-definition } ]opt
  { case-prefixed-statement } }
```

```
case-prefixed-statement =
{ case constant-expr | default : } statement
```

```
repetition-statement =
| while ( logical-expr ) statement
| do statement while ( logical-expr ) ;
| for ( expr opt ; logical-expr opt ; expr opt ) statement
|
```

```
interruption-statement =
| break ;
| continue ;
| return expr opt ;
| goto identifier ;
|
```

```
labeled-statement =
identifier : statement
```

## 3：表达式

> 我们将要除的结果，如你所见，
> 除以九百九十和九十二：
> 然后减去十七，答案必须
> 完全且完美地正确。
>
> —— 刘易斯·卡罗尔，《寻觅史纳克》

### 3.0 引言

C 的表达式实际上执行程序的工作（变量状态的改变）。特别是，简单赋值用新计算的值替换某个变量的当前值，其语法为

```
variable-name-expr = expr
```

variable-name-expr 的复杂程度从整数变量的简单标识符到像这样的复杂名称表达式不等

pcm -> matrix[1][k].imag

它标识由指针变量 pcm 指向的结构的 matrix 部分中第 1 行第 k 列的 complex 成员的 imag 部分。本章的其余部分将解释此类表达式。

表达式本身是一个更广泛的类，允许将许多不同的运算符与 variable-name-expr 和常量结合起来，从而提供语言的计算能力。这些表达式的复杂程度从简单的整数常量到诸如
(mlk +2) >>3) | (p -> f * (*pfun)(2,j))
之类的东西，后者难以用简单的语言描述。

在我们踏上穿越运算符空间的漫长旅程之前，有几个具有普遍兴趣的话题至少应简要讨论一下。首先是运算符的优先级和结合性。

每当出现序列
operand1 binop1 operand2 binop2 operand3
时（例如 a + b * c），表达式的解释就会存在潜在的歧义 [例如 (a + b) * c 或 a + (b * c)]。C 中的每个运算符都有相对于其他运算符的优先级级别，如果两个运算符的级别不同，则该级别可明确确定结合性。由于乘法运算符 * 的级别高于加法运算符 +，因此表达式 a + b * c 的含义为 a + (b * c)。程序员可以使用括号来覆盖这些规则 [例如通过写成 (a + b) * c]。

在同一优先级级别内，大多数二元运算符将“从左到右”结合。例如，
a + b - c + d 的含义为 ((a + b) - c) + d

然而，赋值运算符则恰恰相反：
x = a[2] = j = 0 的含义为 x = (a[2] = (j = 0))

所有一元运算符都在同一级别，并且高于所有二元运算符。它们从右到左结合，正如人们所期望的那样，因为它们大多处于前缀位置。例如，
-*pi
表示 pi 所指向的整数的负值。在大多数情况下，语言不规定子表达式的求值顺序，因此 a * b + c * d 可能是先计算 (a * b)，然后计算 (c * d)，或反之亦然。这对于像
(t = f(a)) + g(t)
这样的表达式具有明确的意义，其值不保证可重复计算。程序员在使用计算中的赋值表达式时应谨慎。语言还允许实现重新排列具有相同可交换运算符的表达式：

```
a + b + c is (a + c) + b or (a + b) + c. etc.
```

算术类型（整数和浮点）从 char 到 double 形成一个自然的层次结构，称为扩展层次结构：

```
char → short → int → unsigned → long → float → double
```

它决定了当两个操作数具有不同的算术类型时，许多运算符返回的值的类型。例如，在

```
(i + '0') - x  /* i is int, x float */
```

char 值 '0' 被扩展为整数，然后可以与 i 相加；然后该整数结果被扩展为浮点数，以便可以减去浮点数 x，从而产生最终的浮点结果。语言还具有强制转换运算符，可显式请求此类扩展，因此上面等价于

```
(float)(i + (int)'0') - x
```

二元算术运算符的正常规则要求将较窄的操作数扩展到较宽的操作数。语言保留了通过扩展操作数超过必要的程度来执行算术运算的权利，只是为了满足此规则。因此，char 和 short 操作数经常被扩展为 int，而 float 算术通常在 double 中执行。这种区别通常对程序员来说并不明显。

当 variable-name-expr 的类型比赋给它的表达式的类型更宽时，会发生正常的扩展；当它更窄时，转换取决于机器且容易丢失信息，因此应谨慎使用窄化赋值。

C 程序可能包含语法如下的 conditional-expr

```
conditional-expr =
logical-expr ? expr : expr
```

它们用于在 if else 中避免重复大部分表达式，当只有一部分取决于某些条件时。例如，

x = (y < 3.0) ? -1.0 : 1.0 ;

将 -1.0 的值赋给 x，如果 y 小于 3.0；否则，将 1.0 的值赋给。语言规则规定只评估其中一个而不是两个 expr。结果始终是两个 expr 类型中较宽的类型，因此上面的整数 1 在赋给 x 之前会被扩展为 1.0。

```
assignment-expr = |
| variable-name-expr binop = expr
| ++ | -- | scalar-variable-expr ++ | -- |
% scalar means arithmetic or pointer

binop = + | - | * | / | % | & | | | ^ | << | >> |
```

类似 x += y 的赋值用 x + y 的值替换 x，但 x 不会被计算两次。要将 x、i、j 加倍，只需写成
x, i, j *= 2

类似 ++x、--x 的赋值分别等价于 (x += 1)、(x -= 1)。所有 assignment-expr 都返回一个值，该值是赋值发生前或后的变量值。在 assignment-expr 的三种形式中，只有后缀增量运算符 (++、--) 在赋值前返回值。

```
k = 0; /* k is 0 */
n = k++; /* n is 0, k is 1 */
m = (k * 2); /* m and k are 2 */
k = --n; /* k and n are 1 */
k += (n++) - n /* ouch! no promises */
```

应该记住，语言不指定赋值的两个操作数的求值顺序，因此

i = 2; a[i] = x + (i == 3) /* a[i] is a2 or a3 ? */

不是确定的。
