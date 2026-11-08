
```c
double val = -1.0;
printf("\n The Arc Tangent of %f is %f ",val, atan(val));
getch();
}
```

前面示例的输出如下：

```
The Arc Tangent of -1.000000 is -0.785398
```

### atanh()

atanh() 函数族返回传给它们的实参的反双曲正切值。实参的值必须在 -1 到 1 的范围内；否则，编译器将抛出错误。如果实参的值等于 1 或 -1，则编译器会抛出范围错误。atanh() 函数族的签名如下：

```c
float atanhf(float param);
double atanh(double param);
long double atanhl(long double param);
```

atanh()、atanhf() 和 atanhl() 函数由 C99 编译器引入。atanhf() 函数用于 float 数据类型；而 atanhl() 函数用于 long double 数据类型。让我们以清单 8.6 中提到的 atanh() 函数为例：

清单 8.6：atanh() 函数的用法。

```c
#include<stdio.h>
#include<math.h>

int main()
{
    double val = -0.5;
    printf("\n The Arc Hyperbolic Tangent of %f is %f ",val, atanh(val));
    getch();
}
```

前面示例的输出如下：

```
The Arc Hyperbolic Tangent of -0.500000 is -0.549306
```

### tan()

tan() 函数族返回传给它们的实参的正切值。实参的值必须以弧度为单位。tan() 函数族的签名如下：

```c
float tanf(float param);
double tan(double param);
long double tanl(long double param);
```

tanf() 和 tanl() 函数由 C99 编译器引入。tanf() 函数用于 float 数据类型；而 tanl() 函数用于 long double 数据类型。让我们以清单 8.7 中提到的 tan() 函数为例：

清单 8.7：tan() 函数的用法。

```c
#include<stdio.h>
#include<math.h>

int main()
{
    double val = -0.5;
    printf("\n The Tangent of %f is %f ",val, tan(val));
    getch();
}
```

前面示例的输出如下：

```
The Tangent of -0.500000 is -0.549306
```

### tanh()

tanh() 函数族返回传给它们的实参的双曲正切值。tanh() 函数族的签名如下：

```c
float tanhf(float param);
double tanh(double param);
long double tanhl(long double param);
```

tanh() 和 tanhf() 函数由 C99 编译器引入。tanhf() 函数用于 float 数据类型，tanhl() 函数用于 long double 数据类型。让我们以清单 8.8 中提到的 tanh() 函数为例：

清单 8.8：tanh() 函数的用法。

```c
#include<stdio.h>
#include<math.h>

int main()
{
    double val = -0.5;
    printf("\n the hyperbolic Tangent of %f is %f ",val, tanh(val));
    getch();
}
```

前面示例的输出如下：

```
The hyperbolic Tangent of -0.500000 is -0.462117
```

### cbrt()

cbrt() 函数族返回传给它们的实参的立方根。cbrt() 函数族的签名如下：

```c
float cbrtf(float param);
double cbrt(double param);
long double cbrtl(long double param);
```

cbrt()、cbrtf() 和 cbrtl() 函数由 C99 编译器引入。让我们以清单 8.9 中提到的 cbrt() 函数为例：

清单 8.9：cbrt() 函数的用法。

```c
#include<stdio.h>
#include<math.h>
int main()
{
    double val = 27;
    printf("\n The cube root of %f is %f ",val, cbrt(val));
    getch();
}
```

前面示例的输出如下：

```
The cube root of 27.000000 is 3.000000
```

## 第8章

### sqrt()

sqrt() 函数族返回传给它们的实参的平方根。任何作为实参传入的负值都可能导致错误。sqrt() 函数族的签名如下：

```c
float sqrtf(float num);
double sqrt(double num);
long double sqrtl(long double num);
```

sqrtf() 和 sqrtl() 函数由 C99 编译器引入。让我们以清单 8.10 中提到的 sqrt() 函数为例：

**清单 8.10：** sqrt() 函数的用法。

```c
#include<stdio.h>
#include<math.h>

int main()
{
    double val = 121;
    printf("The Square root of %f is %f", val, sqrt(val));
    getch();
}
```

前面示例的输出如下：

```
The Square root of 121.000000 is 11.000000
```

### pow()

pow() 函数族返回底数的指数次幂的值，即 base^exp。如果底值为零或 exp 值小于或等于零，编译器将抛出错误。如果底值为负且 exp 值为正，也可能发生错误。

pow() 函数族的签名如下：

```c
float powf(float base, float exp);
double pow(double base, double exp);
long double powl(long double base, long double exp);
```

powf() 和 powl() 函数由 C99 编译器引入。让我们以清单 8.11 中提到的 pow() 函数为例：

**清单 8.11：** pow() 函数的用法。

```c
#include<stdio.h>
#include<math.h>

int main()
{
    double base = 17;
    double exp = 6;
    printf("\n %f raise to the power of %f becomes %f",base,exp,pow(base, exp));
    getch();
}
```

前面示例的输出如下：

```
17.000000 raise to the power of 6.000000 becomes 24137569.000000
```

### exp()

exp() 函数族返回 e 的实参次幂的对数值，其中 e 始终舍入为 2.718282。exp() 函数族的签名如下：

让我们详细讨论一些时间函数。

### asctime()

asctime() 函数返回指向字符串的指针。该函数的原型定义在 `<time.h>` 头文件中。asctime() 函数的签名如下：

```c
char *asctime(const struct tm *ptr);
```

上述函数包含存储在结构体 ptr 中的信息，该结构体作为实参传递给它。由 ptr 指向的结构体可从 gmtime() 函数或 localtime() 函数获得。asctime() 函数使用的缓冲区是一个静态分配的数组，每次调用该函数时都会被覆盖。

asctime() 函数返回的输出格式如下：

```
day month date hours:minutes:seconds year\n\0
```

让我们以清单 8.16 中提到的 asctime() 函数为例：

清单 8.16：asctime() 函数的用法。

```c
#include<stdio.h>
#include<time.h>
int main()
{
    struct tm *ptr;
    time_t t1;
    t1 = time(NULL);
    ptr = localtime(&t1);
    printf("\n The current time is %s ",asctime(ptr));
    getch();
}
```

前面示例的输出如下：

```
The current time is Mon Mar 26 16:02:32 2012
```

### ctime()

ctime() 函数接受一个指向日历类型变量的指针作为实参。日历时间通过调用 time() 函数获得。ctime() 函数使用的缓冲区是一个静态分配的缓冲区，每次调用时都会被覆盖。ctime() 函数的签名如下：

```c
char *ctime(const time_t *time);
```

ctime() 函数返回指向字符串的指针，格式如下：

```
day month date hours:minutes:seconds year\n\0
```

让我们以清单 8.17 中提到的 ctime() 函数为例：

清单 8.17：ctime() 函数的用法。

```c
#include<stdio.h>
#include<time.h>

int main()
{
    time_t t1;
    t1 = time(NULL);
    printf("\n The current time is %s ",ctime(&t1));
    getch();
}
```

前面示例的输出如下：

```
The current time is Mon Mar 26 16:16:19 2012
```

### difftime()

difftime() 函数的签名如下：

```c
double difftime(time_t time2, time_t time1);
```

difftime() 函数返回 time1 和 time2 之间以秒为单位的差值。让我们以清单 8.18 中提到的 difftime() 函数为例：

清单 8.18：difftime() 函数的用法。

```c
#include<stdio.h>
#include<time.h>

int main()
{
    time_t t1,t2;
    long int count = 0;
    t1 = time(NULL);
    while( count <= 100000000) {
        count++;
    }
    t2 = time(NULL);
    printf("\n The difference in time is %f ",difftime(t2,t1));
    return 0;
}
```

前面示例的输出如下：

```
The difference in time is 2.000000
```

### gmtime()

gmtime() 函数返回指向结构体形式的时间的指针。时间以协调世界时（UTC）表示，即格林尼治子午线时间。gmtime() 函数的签名如下：

```c
struct tm *gmtime(const time_t *time);
```

时间指针通过 time() 函数获得。如果系统不支持 UTC，则该函数返回 NULL。让我们以清单 8.19 中提到的 gmtime() 函数为例：

清单 8.19：gmtime() 函数的用法。

```c
#include<stdio.h>
#include<time.h>

int main()
{
    struct tm *gmt;
    time_t t1;

    t1 = time(NULL);
    gmt = gmtime(&t1);

    printf("\n The UTC time is %s ",asctime(gmt));
    getch();
}
```

前面示例的输出如下：
