
++ 递增运算符和 -- 递减运算符将给定数字改变一，并返回得到的新值。它们最常用于统计循环中的迭代次数。递增运算符将值增加一，递减运算符将值减少一。

递增和递减运算符可以放在操作数之前或之后，以产生不同效果。如果放在操作数之前（前缀），其值会立即改变；如果放在操作数之后（后缀），则先记录其值，稍后再改变。

![](img/db19f3858a1e321646bf2590afd29547_76_0.png)

与运算符一起构成表达式的数字称为“操作数”——在表达式 2 + 3 中，数字 2 和 3 就是操作数。

- 1. 使用预处理指令开始一个新程序，以包含标准输入/输出库函数

```c
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_76_1.png)

arithmetic.c

- 2. 添加一个 main 函数，声明并初始化几个整型变量

```c
int main()
{
    int a = 4, b = 8, c = 1, d = 1;
}
```

- 3. 接下来，在 main 函数块中，输出对变量值执行算术运算的结果

```c
printf("Addition: %d \n", a + b);
printf("Subtraction: %d \n", b - a);
printf("Multiplication: %d \n", a * b);
printf("Division: %d \n", b / a);
printf("Modulus: %d \n", a % b);
```

- 4. 现在，在 main 函数块中，输出后缀和前缀递增运算的结果

```
printf("Postfix increment: %d\n", c++);
printf("Postfix now: %d\n", c);
printf("Prefix increment: %d\n", ++d);
printf("Prefix now: %d\n", d);
```

- 5. 在 main 函数块末尾，按照函数声明的要求返回整数值零

```
return 0;
```

- 6. 保存程序文件，然后编译并执行程序，查看算术运算的结果

```
Addition: 12
Subtraction: 4
Multiplication: 32
Division: 2
Modulus: 4
Postfix increment: 1
Postfix now: 2
Prefix increment: 2
Prefix now: 2
```

注意，只有使用前缀递增运算符时，变量值才会立即增加——使用后缀运算符时，它会在下一次被引用时递增。

## 赋值

C 程序中用于赋值的运算符列在下表中。除简单的 = 赋值运算符外，其他运算符都是较长表达式的简写形式，因此为清晰起见，给出了各自的等价形式。

![](img/db19f3858a1e321646bf2590afd29547_78_0.png)

| 运算符： | 示例： | 等价形式： |
|---|---|---|
| = | a = b | a = b |
| += | a += b | a = (a + b) |
| -= | a -= b | a = (a - b) |
| *= | a *= b | a = (a * b) |
| /= | a /= b | a = (a / b) |
| %= | a %= b | a = (a % b) |

重要的是要把 = 运算符理解为“赋值”而不是“等于”，以避免与 == 相等运算符混淆。

在上面的示例中，名为 a 的变量被赋值为名为 b 的变量中包含的值——因此该值成为存储在 a 变量中的新值。

+= 运算符适用于将一个值加到 a 变量中存储的现有值上。在表格示例中，+= 运算符先将变量 a 中存储的值与变量 b 中存储的值相加，然后将结果赋值为存储在 a 变量中的新值。

表中的所有其他运算符都以相同方式工作：先对两个值执行算术运算，然后将结果赋给第一个变量，使其成为该变量存储的新值。

使用 %= 运算符时，第一个操作数 a 除以第二个操作数 b，然后将该运算的余数赋给 a 变量。

![](img/db19f3858a1e321646bf2590afd29547_79_0.png)

== 相等运算符比较操作数的值。此处对此进行了描述。

- 1. 使用预处理指令开始一个新程序，以包含标准输入/输出库函数

```
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_79_1.png)

assign.c

- 2. 添加一个 main 函数，声明两个整型变量

```
int main()
{
    int a, b;
}
```

- 3. 接下来，在 main 函数块中，输出对变量执行赋值运算的结果

```
printf(" Assigned: \n" );
printf(" Variable a = %d \n", a = 8 );
printf(" Variable b = %d \n", b = 4 );
printf(" Added & assigned: \n" );
printf(" Variable a+=b (8+=4) a= %d \n", a += b );
printf(" Subtracted & assigned: \n" );
printf(" Variable a-=b (12-=4) a= %d \n", a -= b );
printf(" Multiplied & assigned: \n" );
printf(" Variable a*=b (8*=4) a= %d \n", a *= b );
printf(" Divided & assigned: \n" );
printf(" Variable a/=b (32/=4) a= %d \n", a /= b );
printf(" Modulated & assigned: \n" );
printf(" Variable a%%=b (8%%=4) a= %d \n", a %= b );
```

- 4. 在 main 函数块末尾，按照函数声明的要求返回整数值零
return 0;

- 5. 保存程序文件，然后编译并执行程序，查看赋值运算的结果

![](img/db19f3858a1e321646bf2590afd29547_80_0.png)

> 注意，必须使用 %% 才能通过 printf() 函数显示 % 字符。

## 比较值

C 编程中常用于比较两个数值的运算符列在下表中：

![](img/db19f3858a1e321646bf2590afd29547_81_0.png)

| 运算符： | 比较测试： |
| --- | --- |
| == | 相等 |
| != | 不相等 |
| > | 大于 |
| < | 小于 |
| >= | 大于或等于 |
| <= | 小于或等于 |

== 相等运算符比较两个操作数，如果两者的值相等，则返回 1（真），否则返回 0（假）。如果两者是相同的数字，则它们相等；如果两者是字符，则按数值比较它们的 ASCII 码值。

相反，!= 不相等运算符在两个操作数不相等时返回 1（真），使用与 == 相等运算符相同的规则；否则返回 0（假）。

相等和不相等运算符可用于测试两个变量的状态，以便在程序中执行条件分支。

大于运算符（>）比较两个操作数，如果第一个的值大于第二个，则返回 1（真）；如果相等或更小，则返回 0（假）。大于运算符（>）经常用于测试循环中倒计时的值。

小于运算符（<）进行相同的比较，但如果第一个操作数的值小于第二个，则返回 1（真），否则返回 0（假）。

在大于运算符（>）或小于运算符（<）后加上 = 运算符，使其在两个操作数的值完全相等时也返回 1（真）。

![](img/db19f3858a1e321646bf2590afd29547_82_0.png)

有关 ASCII 码值的更多信息，可在参考部分的此处找到。

- 1. 使用预处理指令开始一个新程序，以包含标准输入/输出库函数

```c
#include <stdio.h>
```

![](img/db19f3858a1e321646bf2590afd29547_82_1.png)

- 2. 添加一个 main 函数，声明并初始化三个整型变量和两个字符变量

```c
int main()
{
int zero = 0, nil = 0, one = 1;
char upr = 'A', lwr = 'a';
}
```

- 3. 接下来，在 main 函数块中，输出对变量执行比较运算的结果

```c
printf("Equality (0==0): %d\n", zero == nil );
printf("Equality (0==1): %d\n", zero == one );
printf("Equality (A==a): %d\n", upr == lwr );
printf("Inequality (A!=a): %d\n", upr != lwr );
printf("Greater than (1>0): %d\n", one > nil );
printf("Less than (1<0): %d\n", one < nil );
printf("Greater or equal (0>=0): %d\n", zero >= nil );
```

```
printf("Less or equal (1<=0): %d \n", one <= nil );
```

在 main 函数块末尾，按照函数声明的要求返回整数值零
return 0 ;

保存程序文件，然后编译并执行程序，查看比较运算的结果

![](img/db19f3858a1e321646bf2590afd29547_83_0.png)

![](img/db19f3858a1e321646bf2590afd29547_83_1.png)

在数值上，1 表示真结果，0 表示假结果。

![](img/db19f3858a1e321646bf2590afd29547_83_2.png)

大写 'A' 的 ASCII 码值是 65，小写 'a' 的 ASCII 码值是 97——因此此处对它们的比较返回 0（假）。

