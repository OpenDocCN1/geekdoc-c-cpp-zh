

![](img/a9b60755682bc3cf43c528c679efbca7_66_0.png)

在与（AND）电路（串联）中，当 s 和 p 两个开关都闭合，即都为 True 时，表示电流通过的 T 信号将到达末端节点。在或（OR）电路（并联）中，只有当 s 和 p 都处于断开状态，即 False 时，电流 T 才无法到达末端节点，如上图所示，这一切与之前看到的 AND 和 OR 真值表一致。在非（NOT）电路中，当我们打开开关 (1) 时，我们切断了上方的连接 (2)，灯熄灭，反之亦然。

电子学中这三个逻辑门的符号为：

![](img/a9b60755682bc3cf43c528c679efbca7_66_1.png)

## 练习

- 1) 使用亚里士多德的矛盾律，编写一个程序，在 if 中比较句子 `!!(1>0)`（其为真）与一个由单个值 0 或 1（真或假）表示的变量 k，k 通过从键盘读取一个数字并对其除以 2 取余运算得到，当结果为 1 时打印“T”，结果为 0 时打印“F”。（使用 `gets(a); n = atol(a); k = n%2;`，不要忘记事先声明变量。）
- 2) 编写一个程序，从键盘读取一个四位非零数字的数字 n，并计算其除以 9 的余数（`n = k%9;` 是“弃九法”的计算）。然后程序必须测试这个计算出的数字。如果它小于 3 或大于 6，则打印该数字并附上消息“我讨厌中间。”否则，打印该数字并附上：“美德居于中间（亚里士多德）。”

## 第九章

### 库函数 - 头文件

ANSI 标准库的头文件（或称库文件）如下：

| assert.h | setjmp.h |
| ctype.h | signal.h |
| errno.h | stdarg.h |
| float.h | stddef.h |
| limits.h | stdio.h |
| locale.h | string.h |
| math.h | time.h |

这些库中较小的是 signal.h——只有两个函数 `raise()` 和 `signal()`；setjmp.h——包含用于非局部跳转的函数 `longjmp()` 和 `setjmp()`；以及 assert.h——只有函数 `assert()`，用于测试断言，即验证表达式的有效性。

每个开发 C++ 编译器的公司都添加了一定数量的头文件，但它们的名称在不同品牌之间并不相同。差异更大的地方在于屏幕操作函数。例如，Turbo C++ 中的图形文件是 `graphics.h`，而 Microsoft C++ 中是 `graph.h`。不同编译器的视频函数之间很少有一致性，但在这个领域，这种现象并非 C 语言独有。在不涉及视频操作的情况下，多家公司达成了普遍共识，这主要归功于 ANSI 的标准化努力。

### 数学函数

如前所述，数学函数大多存储在名为 `math.h` 的头文件中。`stdlib.h` 头文件包含一些数学函数，例如非初等函数 `abs()` 和 `rand()`，用于求绝对值和随机数，以及函数 `div()`，它提供除法的商和余数。

ANSI C 定义的 `math.h` 文件包含以下函数：`acos(), asin(), atan(), atan2(), ceil(), cos(), cosh(), exp(), fabs(), floor(), fmod(), frexp(), ldexp(), log(), log10(), modf(), pow(), sin(), sinh(), sqrt(), tan()` 和 `tanh()`。

函数 `acos()`、`asin()` 和 `atan()` 分别提供反余弦、反正弦和反正切。函数 `atan2()` 使用两个参数 x 和 y（两条直角边）来计算反正切；`cosh()` 是双曲余弦，而 `exp()` 和 `log()` 是以 e 为底的指数和对数函数（自然底数 e = 2.718...，常用对数是 `log10()`）；`fabs()` 给出绝对值（非负值），`modf()` 提供两个值相除的余数，`floor()` 和 `ceil()` 分别提供参数中包含的最小和最大整数（在许多其他语言中 `floor()` 是 `int()`），`pow()` 用两个参数计算幂，`frexp()` 提供一个从 .5 到 1 的尾数，而 `ldexp()` 返回 `x*2^k` 的结果，参数为 x 和 k。

使用 `stdio.h` 和 `math.h`，你可以体验以下示例：

```
main() {float x,y,w,t; x=4.81; y=cos(2*log(x+1));

w=floor(y); t=pow(4,w); printf("\n%f %f %f",y,w,t);}
```

### 字母数字函数

字母数字函数（或称字符串函数）大多包含在头文件 `ctype.h` 和 `string.h` 中。

在 ANSI 标准中，`ctype.h` 文件的函数有：`isalnum(), isalpha(), iscntrl(), isdigit(), isgraph(), islower(), isprint(), ispunct(), isspace(), isupper(), isxdigit(), tolower()` 和 `toupper()`。后者（`toupper()`）将字符转换为大写（‘upper’），而 `tolower()` 转换为小写（‘lower’）。其他函数检查字符是否属于特定类型。因此 `isalnum()` 检查字符是否为字母数字，`isalpha()` 检查是否为字母表中的字母，`iscntrl()` 检查是否为控制字符，以此类推。

标准的 `string.h` 头文件包含以下函数：`memchr(), memcmp(), memcpy(), memmove(), memset(), strcat(), strchr(), strcmp(), strcoll(), strcpy(), strerror(), strlen(), strncat(), strncmp(), strncpy(), strpbrk(), strrchr(), strspn(),`

`strstr(), strtok()` 和 `strxfrm()`。让我们看一些例子。表达式 `memchr(const *s, int c, size_t m);` 中，函数在 `*s` 变量指向的内容的前 m 个字符中搜索字符 c。语句 `char *strcat(char *s, const char *p);` 将字符串 p 连接到字符串 s 的末尾。`strcmp()` 函数比较两个字母数字参数，`strcpy()` 将第一个参数的字符串复制到第二个参数中，`strncpy()` 对前 n 个字符做同样的事情，`strlen()` 提供字符串的长度。`strcoll()` 和 `strxfrm()` 函数比较不同语言的字符串。它们不在 Turbo C 或 Microsoft C 中。

下面的示例程序说明了某些字母数字函数的用法。

### 示例程序 #9A

```
/* Programa "Alphanum.cpp" */
#include <stdio.h>
#include <string.h>
#define TOTAL 80
void Invert(char s[])
{ int i, k=strlen(s);
printf("\n");
for(i=k-1; i>=0; --i) putchar(s[i]);
}
void Space(char s[])
{ int i,k=strlen(s);
printf("\n");
for(i=0;i<k;i++){putchar(s[i]); putchar(' ');}
}
main()
{ char s[TOTAL]; char m[TOTAL];
char p[]="Bed"; char q[]="time";
printf("\n Type a name:\n"); gets(s);
Invert(s); printf("\n");
Space(s); printf("\n");
printf("\n% s",p); printf("\n% s",q);
strcpy(m,p); strcat(m,q); printf("\n% s\n",m);
}
```

练习修改：第一个可能的改动是将“Bed”和“time”这两个词换成不同长度的词，例如“Page”和“ant”。第二个改动稍显艰巨：创建 `Combine()` 函数，同时执行 `Invert()` 和 `Space()` 的功能。第三个改动：将“Type a name:”改为“Type two words:”，并创建第四个函数，名为 `Merge()`，它执行程序中当前最后两行指令的操作，这两行以 `printf()` 和 `strcpy()` 开头。当然，一旦你创建了该函数，这些行应该被删除，并用对该函数的调用代替。

使用头文件 `stdio.h`、`string.h` 和 `ctype.h`，读者要创建上述建议的 `Merge()` 函数，可以基于下面的小程序，该程序将表达式“Aca pulco”赋给向量 m，并将融合后的单词“Acapulco”输出到向量 p。

```
main() { char p[80],m[]="Aca pulco"; int i,k,s=strlen(m);
    printf("\n");for(i=0;i<=s;i++)if(isspace(m[i])) k=i; strncpy(p,m,k);
    for(i=0;i<=s;i++) {p[i+k]=m[i+k+1];} printf("\n %s",p);}
```

### 其他字母数字函数

除了重要的实用函数，如 `abort(), atexit(), bsearch(), calloc(), exit(), free(), malloc(), qsort(), realloc(), system()`，以及一些数学函数（`abs(), div(), labs(), ldiv(), rand()` 和 `srand()`）之外，`stdlib.h` 头文件还包含几个将字符串转换为其他类型对象的函数。最知名的编译器包括以下函数：`atof(), atoi(), atol(), strtod(), strtol()` 和 `strtoul()`。`atof()` 函数将以字符串（ASCII）形式输入的数字转换为 float 数据类型。`atoi()` 函数将其转换为整数类型，而 `atol()` 转换为 long 类型整数。`strtod(), strtol()` 和 `strtoul()` 函数分别将字母数字字符串转换为 long 和 unsigned long 类型的值，但在最后两个函数中，它们有三个参数，第三个参数指明数字的进制。

使用 `stdio.h`、`stdlib.h` 和 `time.h`，你可以运行以下示例，该示例生成两个随机数，首先将键盘输入的数字作为种子（`srand()`），然后通过 `time()` 函数获取系统值作为种子。

```
main() { float k,r1,r2;char s[80];puts("Type number:");gets(s);
    k=atol(s);srand(k); r1=rand(); srand(time(NULL)); r2=rand();
    printf("\n%6f%6f",r1,r2);}
```

