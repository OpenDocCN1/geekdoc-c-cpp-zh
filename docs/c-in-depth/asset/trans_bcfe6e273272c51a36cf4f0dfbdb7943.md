
这里 arg1、arg2……是形式参数。macro_name 被替换为 macro_expansion，形式参数被替换为宏调用中提供的对应实际参数。因此，对于不同的实际参数，macro_expansion 会不同。例如，假设我们定义以下两个宏：

```
#define SUM(x, y) ( (x) + (y) )
#define PROD(x, y) ( (x) * (y) )
```

现在假设程序中包含以下两条语句：

```
s = SUM(5, 6);
p = PROD(m, n);
```

经过预处理器处理后，这些语句将展开为：

```
s = ( (5) + (6) );
p = ( (m) * (n) );
```

由于这只是文本替换，因此参数可以是任何数据类型。例如，我们也可以使用宏 SUM 来求 long 或 float 类型的和。

以下语句：

```
s = SUM( 2.3, 4.8 );
```

将展开为：

```
s = ( (2.3) + (4.8) );
```

```
/*P12.2 Program to understand macros with arguments*/
#include<stdio.h>
#define SUM(x,y) ((x)+(y))
#define PROD(x,y) ((x)*(y))
main()
{
int l,m,i,j,a=5,b=3;
float p,q;
l=SUM(a,b);
m=PROD(a,b);
i=SUM(4,6);
j=PROD(4,6);
p=SUM(2.2,3.4);
q=PROD(2.2,3.4);
printf("l=%d,m=%d,i=%d,j=%d,p=%f,q=%f\n",l,m,i,j,p,q);
}
```

输出：

l = 8, m = 15, i = 10, j = 24, p = 5.6, q = 7.5

让我们再看一些带参数宏的示例：

```
#define SQUARE(x) (x)*(x)
#define MAX( x, y ) ( (x) > (y) ? (x) : (y) )
#define MIN( x, y ) ( (x) < (y) ? (x) : (y) )
#define ISLOWER(c) ( c >= 97 && c <= 122 )
#define ISUPPER(c) ( c >= 65 && c <= 90 )
```

```
#define TOUPPER(c) ( (c) + 'A' - 'a' )
#define ISLEAP(y) ( (y%400 == 0) || ( y%100!=0 && y%4 == 0) )
#define BLANK_LINES(n) { int i; for ( i = 0; i < n; i++ ) printf("\n"); }
#define CIRCLE_AREA(rad) ( 3.14 * (rad) * (rad) )
```

注意 macro_name 与左括号之间不应有空格，否则宏展开会被认为从左括号开始。例如，如果我们这样编写宏：

```
#define SQUARE(x) ( (x)*(x) )
```

现在任何像 SQUARE(5) 这样的调用都会展开为：

```
(x)*(x))(5)
```

这里 SQUARE 被视为无参数宏，而文本 (x)*(x)) 被视为宏展开。因此 SQUARE 被宏展开替换，而 (5) 原样写出。

## 12.3 宏中的嵌套

一个宏名也可用于定义另一个宏名，即宏展开中也可包含另一个宏的名称。例如：

```
#define PI 3.14
#define PISQUARE PI*PI
```

现在如果我们有一个表达式：

```
k = PISQUARE;
```

预处理器第一次会将其展开为：

```
k = PI * PI;
```

现在预处理器会再次重新扫描这个展开后的表达式，如果发现任何宏就替换它们。这个重新扫描过程会持续到表达式中不再有宏为止。因此最终展开后的表达式为：

```
k = 3.14 * 3.14;
```

下面是宏嵌套的另一个示例：

```
#define ISLOWER(c) (c >= 97 && c <= 122)
#define TOUPPER(c) ISLOWER(c) ? (c + 'A' - 'a') : c
```

这里宏 TOUPPER 在其展开中使用了宏 ISLOWER。仅当字符为小写时才会改为大写，否则保持不变。

以下程序说明嵌套宏的用法：

```
/*P12.3 Program to understand nesting in macros*/
#include<stdio.h>
#define ISLOWER(c) (c>=97&&c<=122)
#define ISUPPER(c) (c>=65&&c<=90)
#define ISALPHA(c) ( ISLOWER(c) || ISUPPER(c))
#define ISNUM(c) (c>=48&&c<=57)
#define ISALPHANUM(c) ( ISALPHA(c) || ISNUM(c))
main()
{
```
```c
char ch;
printf("Enter a character \n");
scanf("%c", &ch);
if (ISALPHANUM(ch))
printf("%c is an alphanumeric character\n",ch);
else
printf("%c is not an alphanumeric character\n",ch);
```
```

如果宏名出现在其自身的展开中，则它不会被展开。因此不要尝试编写这样的递归宏：

```c
#define FACTORIAL(k) k * FACTORIAL(k-1) /*Incorrect*/
```

## 12.4 宏的问题

你一定想知道为什么宏展开中使用了这么多括号。由于预处理器只是用实际参数替换形式参数，在某些情况下我们可能得不到期望的结果。让我们看看使用宏时会出现什么样的问题，以及如何避免它们。

在以下程序中，我们定义了一个宏 PROD，其宏展开中没有任何括号：

```c
/*PL2.4*/
#include<stdio.h>
#define PROD(x,y) x*y
main()
{
printf("%d\t",PROD(2,4));
printf("%d\n",PROD(3+4,5+1));
}
```

输出：
8 24

这里第一个 printf() 给出正确结果 8，但第二个 printf() 打印 24，而我们期望结果是 7 和 6 的乘积，即 42。让我们看看预处理器如何展开这些宏。

PROD(3+4, 5+1 ) 被展开为 3+4*5+1

乘法运算符的优先级高于加法运算符，因此计算过程为 3+20*1 =24，所以得到了错误结果。这个问题可以通过将形式参数括在括号中来解决。因此现在我们这样重写程序：

```c
/*PL2.5*/
#include<stdio.h>
#define PROD(x,y) (x)*(y)
main()
{
printf("%d\t",PROD(2,4));
printf("%d\t",PROD(3+4,5+1));
printf("%d\n",60/PROD(2,3));
}
```

输出：

8 42 90

现在前两个 printf() 给出了期望结果。在第三个 printf 中，我们试图用 60 除以 2 和 3 的乘积，期望结果是 10，但得到 90，所以我们的宏仍然有问题。让我们再次看看预处理器是如何进行展开的。

PROD(2, 4) 被展开为 (2)*(4)
PROD(3+4, 5+1) 被展开为 (3+4)*(5+1)
60/PROD(2, 3) 被展开为 60 / (2)*(3)

这里我们可以看到，在最后一种情况下，首先 60 除以 2，然后结果乘以 3，因为 / 和 * 运算符从左到右结合。所以结果不是期望的结果。为了解决这类问题，我们应该将整个宏展开括在括号中。因此定义宏的正确方式是：

```
#define PROD(x, y) ( (x)*(y) )
```

现在 60/PROD(2, 3) 将展开为 60 / ( (2)*(3) )，因此 60 除以 2 和 3 的乘积，我们就能得到期望结果。

因此，如果你的宏接受参数并希望它正常工作，最好在整个宏展开以及每个参数周围都加上括号。

现在考虑这个程序，我们会发现另一类问题。

```
/*P12.6*/
#include<stdio.h>
#define SQUARE(x) ((x)*(x))
main()
{
int k=5,s;
s=SQUARE(k++);
printf("s = %d, k = %d\n",s,k);
}
```

输出：

s = 25, k = 7

这里语句
s = SQUARE(k++); 被展开为 s = ( (k++) * (k++) );

这里 k 的值被递增了两次，而我们本意是将 k 的平方赋给变量 s，然后只将 k 的值递增一次。此外，像 (k++)*(k++) 这样的表达式在 C 中的结果未定义。因此在这种情况下，最好使用函数而不是宏。

```
s=square(k++);
printf("s = %d, k = %d\n",s,k);
}
```

输出：

s = 25, k = 6

现在我们将看到另一类问题。考虑这个程序，其中我们编写了一个宏来交换任意数据类型的两个变量的值。

```
/*P12.8*/
#include<stdio.h>
#define SWAP(dtype,x,y) { dtype t; t = x, x = y, y = t; }
main()
{
    int a=2,b=5;
    SWAP(int,a,b)
    printf("a=%d,b=%d\n",a,b);
}
```

输出：
a = 5, b=2

这个程序没有问题。它按我们的预期工作，并交换了 a 和 b 的值。宏按以下方式展开：

SWAP(int, a, b) 被展开为 { int t; t = a, a = b, b = t; }

宏展开后，main() 函数将如下所示：

```
main()
{
    int a=2,b=5;
    { int t; t=a, a=b, b=t; }
    printf("a = %d, b = %d\n",a,b);
}
```

这里 t 是局部于其定义所在代码块的变量。

现在考虑下一个程序，它与上面的程序类似，只是要交换的变量名是 s 和 t。

```
/*P12.9*/
#include<stdio.h>
#define SWAP(dtype,x,y) { dtype t; t=x, x=y, y=t; }
main()
{
    int s=2, t=5;
    SWAP(int,s,t)
    printf("s = %d, t = %d\n",s,t);
}
```

输出：

s = 2, t = 5

s 和 t 变量的值没有被交换。宏展开后，main 函数将如下所示：
