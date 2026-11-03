
## 2. 初始化器

这里 cmat 已被声明为具有 parts matrix 和 tag 的结构类型变量。因此，其初始化器的一般形式为

```c
{ initializer-for-matrix, char-constant }
```

由于 matrix 是 COMPLEX 类型的数组，其初始化器的形式为

```c
{ initializer-for-row-0,
  initializer-for-row-1
}
```

等等。最后，每个 COMPLEX 结构的初始化器形式为

```c
{ initializer-for-real-part, initializer-for-imag-part }
```

等等，cmat 的完整初始化器由一系列逐步细化得出。注意 cmat.matrix 的第一行的第一个元素并未显式初始化。在外部声明的情况下，默认情况下它将为 {0.0, 0.0}。

如果为联合指定了初始化器，它必须对应于声明的第一个部分。联合和结构都不能在自动声明中初始化。

### 2.6 函数定义

函数定义看起来有点像被初始化的数据声明——因此在本节中讨论它。事实上，参数和函数体构成了与函数名关联的值，因此它们确实起着类似于初始化器的作用，只是函数名代表常量（不可更改）值，而不是变量。函数指针类型的变量可能会改变其归属，但函数不会！

函数定义的语法是

```c
function-definition ::= { extern | static }opt
type-specifier opt declarator ( argument-list opt )
argument-declaration-list opt
compound-statement
```

复合语句最简单的形式是被大括号括起来的语句序列（命令式命令）。下面是一个完整的函数定义：

```c
double length(x, y)
double x, y;
{
    return sqrt(x * x + y * y);
}
```

名称 x 和 y 是函数 length 的形式参数，它们表现得像特殊变量，每次调用函数时都会初始化为不同的值。因此，在参数规范中不允许有显式初始化器。length(0.0, p[2]) 的出现等价于 sqrt(0.0 * 0.0 + p[2] * p[2])。

像 (*fpa())[] 这样的复杂函数声明符可以通过类型定义来避免，如 [1.7] 中所述，因此其解释将推迟到第 4 章。

在详细检查复合语句之前，区分指针参数和其他参数是有启发性的。一个函数改变调用该函数的环境中某个变量 x 的值的唯一方法是将 x 的位置 &x 传递给它，其中相应的形式参数是指针类型。此外，聚合类型（struct、union 或 array）不能直接作为参数传递，但指向它们的指针可以。下一页所示的函数旨在用 value x 等于数组 table 的元素的第一个下标位置替换 index：

```c
float table[6] = {0, 0, 1, 2, 3, 7}, x = 2;
int index;
main() {
    lookup(&table[0], x, &index);
}
```

```c
lookup(t, val, i)
float *t;
float val;
int *i;
{
    int k;
    for (k = 0; k < 6; ++k)
        if (*(t + k) == val)
        {
            *i = k;
            return;
        }
    *i = -1;
}
```

其中一些内容在完全理解指针表达式和 variable-name-exprs 之前不会很清楚；请特别参见 [3.1] 和 [3.3]。重要的是要认识到，在 &index 之后，对应于形式指针参数 i 的实际参数被给出；然后，像 *i = k; 这样的赋值实际上意味着对 index 的赋值，因为前缀指针操作 * 使表达式 *i 成为内存中可更改对象的有效 name-expr。

上面的程序可以重写，将 &table[0] 改为 table，将 float *t 改为 float t[]，将 *(t + k) 改为 t[k]，而不会改变含义。这是因为未下标的数组名被视为指向第 0 个元素的指针的值，因为形式数组参数被解释为指向数组元素类型的指针，并且因为 t[k]  anyway 被实现为表达式 *(t + k)（参见 [3.4]）。

现在是时候描述一些语句了。函数定义的基本单位是复合语句，其语法如下所示：

```c
compound-statement =
{ { local-declaration | type-definition }
  { statement } }
```

这些局部声明和类型定义的详细讨论——它们在很大程度上与外部声明相同——在第 4 章中。对于现在，我们将集中于 C 语言的语句，或命令式命令。

```c
statement =
| expr ;     % assignments and function calls
| compound-statement % for grouping
| selection-statement
| repetition-statement
| interruption-statement
| labeled-statement % null statement
;
```

尽管表达式（即 exprs）的详细讨论必须等待第 3 章，但我们将介绍简单的赋值表达式（大多数语言中的语句）和函数调用（其他地方的 procedure 或 subroutine 调用），因为它们是大多数 C 程序的活跃主力。一些已经遇到的表达式语句是：

```c
k = 0;
/* same as k = k + 1; */
lookup(table, x, &index);
```

无法做出选择的程序确实很弱，因此 C 有两种选择语句：

```c
selection-statement =
| if ( logical-expr ) statement
| if ( logical-expr ) statement else statement
| switch ( expr ) switch-statement-group

switch-statement-group =
| { { local-declaration | type-definition } }
| case-prefixed-statement

case-prefixed-statement =
| case constant-expr : statement
| default : statement
```

if 语句要求在 logical-expr 为“真”（非零）时精确执行第一个子语句；否则，它要求在 else 之后执行第二个子语句。当省略 else 短语时，就好像显式指定了 else /* null */; 一样。例如，

```c
if (k < 2)
    p = f(k);
else
    p = g(2 - k);
```

将根据 k 相对于 2 的大小执行两个赋值中的恰好一个。关系运算符提供 1 表示“真”，0 表示“假”，将在第 3 章中更详细地讨论。常见形式是

```c
if (p)
...
else if (q)
...
else if (r)
...
else
/* none of the above */
...
```

并且推荐这种缩进风格。

经常 enough，逻辑表达式 p、q、r 等具有 k == 1、k == 2、k == 5 等形式，其中 == 是 C 中的相等比较运算符。switch 语句可处理此类情况，例如

```c
switch(k - 2)
{
case 3: j = k*k; break;
case 5: case 2: ++k; do_something(k); break;
default: error("bad k");
}
```

由于 case 前缀只允许常量表达式，switch 语句可以非常高效地实现。break 语句对于在每个可选择部分之后终止 switch 语句是必要的；否则，控制会以最不令人满意的方式从一个 case 流向下一个 case。case 标签可能出现在复合语句中嵌入。只有嵌入的 switch 语句限制了这种有问题的功能。

C 的重复语句由以下给出

```c
repetition-statement =
| while ( logical-expr ) statement
| do statement while ( logical-expr );
| for ( expr_opt ; logical-expr ; expr_opt ) statement
```

while 语句重复执行其子语句，直到 logical-expr 不再为“真”，如果 logical-expr 为“假”，则永远不会开始执行子语句。如果 logical-expr 最初为“假”，它可能是一个重数为 0 的重复。

do 语句类似，只是测试是在每次执行子语句之后进行，并且重复可能在此时终止。因此它至少执行一次其子语句。

for 语句是以下内容的简写

```c
expr1;
while ( logical-expr )
{ statement ; expr2 }
```

因此第一个表达式通常是初始化；第二个是逻辑预测试；第三个是某种形式的后增量。示例是

```c
while (c[i] == ' ' && i < SIZE)
    ++i;
do
{
    swap (c, i, j);
    ++i;
    --j;
}
while (i < j);
/* array c now reversed */
for (i = 0; i < SIZE; ++i)
{
    a[i] = b[i];
    c[i] = -1.0;
}
/* array b copied to a and c set to -1.0 */
```

如果 for 语句中的 logical-expr 缺失，则假定为常量“真”值（1）。
