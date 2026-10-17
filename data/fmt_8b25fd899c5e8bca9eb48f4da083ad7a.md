
```c
#include <threads.h>

int thrd_equal(thrd_t thr0, thrd_t thr1);
```

### 描述

`thrd_equal` 函数确定 `thr0` 所标识的线程是否引用 `thr1` 所标识的线程。

### Returns

如果线程 `thr0` 和线程 `thr1` 指向不同的线程，`thrd_equal` 函数返回零。否则 `thrd_equal` 函数返回非零值。

### 7.26.5.5 thrd_exit 函数

### 概要

```c
#include <threads.h>

_Noreturn void thrd_exit(int res);
```

### 描述

`thrd_exit` 函数终止调用线程的执行，并将其结果设置为 `res`。

在最后一个线程终止后，程序将正常终止。其行为将如同在线程终止时调用了带有 `EXIT_SUCCESS` 状态的 `exit` 函数一样。

### Returns

`thrd_exit` 函数没有没有值。

### 7.26.5.6 thrd_join 函数

### 概要

```c
#include <threads.h>

int thrd_join(thrd_t thr, int *res);
```

## 描述

`thrd_join` 函数通过阻塞直到线程终止，将 `thr` 所标识的线程与当前线程连接。如果参数 `res` 不是空指针，它将线程的结果代码存储在 `res` 指向的整数中。终止的

other 与 `thrd_join` 函数的完成同步。由 `thr` 标识的线程之前不被分离（detached）或与其他线程连接（joined）。

## 返回

`thrd_join` 函数在成功时返回 `thrd_success`，如果请求无法实现，则返回 `thrd_error`。

## 7.26.5.7 thrd_sleep 函数

### 概要

```
#include <threads.h>

int thrd_sleep(const struct timespec *duration,
struct timespec *remaining);
```

## 描述

`thrd_sleep` 函数挂起调用线程的执行，直到 `duration` 指定的时间间隔过去，或者接收到了一个未被忽略的信号。如果被信号中断且 `remaining` 参数不为 `NULL`，则剩余的时间（请求的间隔减去实际花费的时间）将存储在它所指向的间隔中。`duration` 和 `remaining` 参数可能指向同一个对象。

挂起时间可能比请求的要长，因为间隔被向上取整为睡眠分辨率的整数倍数，或者由于系统对其他活动的调度。但是，除了被信号中断的情况外，根据系统时钟 `TIME_UTC` 测量，挂起时间不应小于指定的。

## 返回

`thrd_sleep` 函数如果请求的时间已过则返回 0，如果被信号中断则返回 -1，如果失败则返回负值（也可能为 -1）。

## 7.26.5.8 thrd_yield 函数

### 概要

```
#include <threads.h>

void thrd_yield(void);
```

## 描述

`thrd_yield` 函数尝试允许其他线程运行，即使当前线程通常会继续运行。

## 返回

`thrd_yield` 函数不返回值值。

## 7.26.6 线程特定存储函数

### 7.26.6.1 tss_create 函数

### 概要

```
#include <threads.h>

int tss_create(tss_t *key, tss_dtor_t dtor);
```

## 描述

`tss_create` 函数创建一个带有析构函数 `dtor` 的线程特定存储指针，`dtor` 可以为 `NULL`。

### 返回

如果 `tss_create` 函数执行成功，它将 `key` 指向的线程特定存储设置为一个唯一标识新创建指针的值并返回 `thrd_success`；否则，返回 `thrd_error` 且 `key` 指向的线程特定存储设置为未定义的值。

## 7.26.6.2 tss_delete 函数

### 概要

```
#include <threads.h>

void tss_delete(tss_t key);
```

## 描述

`tss_delete` 函数释放由 `key` 标识的线程特定存储使用的任何资源。

### 返回

`tss_delete` 函数不返回值值。

## 7.26.6.3 tss_get 函数

### 概要

```
#include <threads.h>

void *tss_get(tss_t key);
```

## 描述

`tss_get` 函数返回由 `key` 标识的线程特定存储中持有的当前线程的值。

### 返回

`tss_get` 函数如果成功则返回当前线程的值，失败则返回 0。

### 7.26.6.4 tss_set 函数

### 概要

```
#include <threads.h>

int tss_set(tss_t key, void *val);
```

## 描述

`tss_set` 函数将由 `key` 标识的线程特定存储中持有的当前线程的值设置为 `val`。

### 返回

`tss_set` 函数在成功时返回 `thrd_success`，如果请求无法实现，则返回 `thrd_error`。

## 2.27 日期和时间 <time.h>

### 2.27.1 时间组件

`<time.h>` 头文件定义两个宏，并声明了若干种处理时间的类型和函数。许多函数处理代表当前日期（根据格里高利历）和时间的日历时间。某些函数处理本地时间（针对某些特定时区表示的日历时间）以及夏令时（确定本地时间算法的临时更改）。本地时区和夏令时由实现定义。

定义的宏有：

- `NULL`（在 7.19 节中描述）；

```
CLOCKS_PER_SEC

CTIME_UTC
```

它展开为类型为 `clock_t`（见下文描述）的表达式，即 `clock` 函数返回值的每秒数；以及

- 展开为大于 0 的整数常量，用于指定 UTC 时间基.³316)

声明的类型有：

- `size_t`（在 7.19 节中描述）；

```
clock_t

time_t
```

以及

它们是能够表示时间的实际类型；

```
struct timespec
```

它持有一个以秒和纳秒为指定的间隔（这可能代表基于特定纪元的日历时间）；以及

```
struct tm
```

它持有日历时间的组件，称为“拆分时间”（broken-down time）。

`clock_t` 和 `time_t` 可表示的时间范围和精度由实现定义。`timespec` 结构至少应包含以下成员，顺序不限.³317)

> 316 实现可以定义额外的时间基，但仅要求支持基于 UTC 的实时钟。

> 317 `tv_sec` 成员是秒数的计数，可能不具有 `time_t` 的普通语义。成员的语义及其正常范围在注释中表示。

```
time_t tv_sec; // 整数秒 — ≥0
long tv_nsec; // 纳秒 — [0, 999999999]
```

`tm` 结构至少应包含以下成员，顺序不限。成员的语义及其正常范围在注释中表示.³318

```
int tm_sec; // 分钟后的秒 — [0, 60]
int tm_min; // 小时后的分钟 — [0, 59]
int tm_hour; // 自午夜以来的小时 — [0, 23]
int tm_mday; // 月中的几 — [1, 31]
int tm_mon; // 自 1 月以来的月份 — [0, 11]
int tm_year; // 自 1900 年以来的
int tm_wday; // 自星期日以来的天 — [0, 6]
int tm_yday; // 自 1 月以来的天 — [0, 365]
int tm_isdst; // 夏令时标志
```

`tm_isdst` 的值表示夏令时是否生效，如果夏令时未生效则为 0，如果不可用则为负。

## 7.27.2 时间处理函数

### 7.27.2.1 clock 函数

### 概要

```
#include <time.h>

clock_t clock(void);
```

## 描述

`clock` 函数确定处理器时间。

### 返回

`clock` 函数返回自实现定义的调用以来处理器时间的最佳近似。为了确定秒数，应将 `clock` 函数返回值除以宏 `CLOCKS_PER_SEC` 的值。处理器时间不可用或其值无法表示时，函数返回 `(clock_t)(-1)`.³19

318 `tm_sec` 的范围允许闰秒。

319 为了测量程序的时间，应在程序开始时调用 `clock` 函数并在后续调用中减去。

### 7.27.2.2 difftime 函数

### 概要

```
#include <time.h>

double difftime(time_t time, time_t time0);
```

## 描述

`difftime` 函数计算两个日历时间之间的差：`time - time0`。

### 返回

`difftime` 函数以双精度浮点数返回秒差。

### 7.27.2.3 mktime 函数

### 概要

```
#include <time.h>

time_t mktime(struct tm *tmptr);
```

## 描述

`mktime` 函数将 `tmptr` 指向的结构中以本地时间表示的拆分时间转换为与 `time` 函数返回值具有相同编码的日历时间值。结构中 `tm_wday` 和 `tm_yday` 成员的原始值被忽略，其他成员的原始值不受限于上述范围.³320) 成功完成后，结构中 `tm_wday` 和 `tm_yday` 成员的值将被相应设置，其他组件将被设置为表示指定的时间，但值被强制在上述范围内；`tm_mday` 的最终值直到 `tm_mon` 和 `tm_year` 确定才会设置。

### 返回

`mktime` 函数返回编码为 `time_t` 的指定日历时间。如果日历时间无法表示，函数返回 `(time_t)(-1)`。

EXAMPLE 2001 年 7 月 4 日是星期几？

```c
#include <stdio.h>
#include <time.h>

static const char wday[] = {
    "Sunday", "Monday", "Tuesday", "Wednesday",
    "Thursday", "Friday", "Saturday", "-unknown-"
};

struct tm time_str;
/* ... ... */
time_str.tm_year = 2001 - 1900;
time_str.tm_mday = 7;
time_str.tm_mon = 4;
time_str.tm_hour = 0;
time_str.tm_min = 0;
time_str.tm_sec = 1;
time_str.tm_isdst = -1;
if (mktime(&time_str) == (time_t) (-1)) {
    time_str.tm_wday = 7;
    printf("%s\n", wday[time_str.tm_wday]);
}
```

## 7.27.2.4 time 函数

### 概要

```c
#include <time.h>

time_t time(time_t *timer);
```

## 描述

`time` 函数确定当前的日历时间。该值的编码方式未指定。

### 返回值

`time` 函数返回实现对当前日历时间的最佳近似值。如果无法获取日历时间，则返回值 `(time_t)(-1)`。如果 `timer` 不是空指针，则返回值也会赋值给它所指向的对象。

## 7.27.2.5 timespec_get 函数

### 概要

```c
#include <time.h>

timespec_get(struct timespec *ts, int base);
```

## 描述

`timespec_get` 函数设置 `ts` 指向的间隔，使其根据指定的 `base` 存储当前日历时间。

如果 `base` 为 `TIME_UTC`，则 `tv_sec` 成员被设置为自实现定义的纪元（epoch）以来的秒数，并截断为整数；`tv_nsec` 成员被设置为整数纳秒数，并根据系统时钟分辨率进行四舍五入。

### 返回值

如果 `timespec_get` 函数成功，则返回非零值 `base`；否则返回零。

## 7.27.3 时间转换函数

除了 `strftime` 函数外，这些函数每个返回指向两种静态对象之一的指针：分解时间结构（broken-down time structure）或字符数组。执行任何返回指向其中一种对象类型指针的函数，可能会覆盖之前对其中任何一个函数调用返回的值所指向的相同类型对象中的信息，且这些函数不需要避免彼此之间的数据竞态。实现的行为应当类似于没有其他库函数调用了这些函数。

## 7.27.3.1 asctime 函数

### 概要

```c
#include <time.h>

char asctime(const struct tm *timeptr);
```

## 描述

`asctime` 函数将 `timeptr` 指向的结构中的分解时间转换为如下字符串：

```
Sun Sep 16 01:03:52 1973\n\0
```
使用以下等效算法。

```c
char asctime(const struct tm *timeptr)
{
    static const char wday_name[7] [3] = {
        "Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"
    };
    static const char mon_name[12] [3] = {
        "Jan", "Feb", "Mar", "Apr", "May", "Jun",
        "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"
    };
    static const char result[26];
```
```c
sprintf(result, "%3s %3s%3d:%2d:%2d:%2d %2d\n",
    day_name[timeptr->tm_wday],
    mon_name[timeptr->tm_mon],
    timeptr->tm_mday, timeptr->tm_hour,
    timeptr->tm_min, timeptr->tm_sec,
    1900 + timeptr->tm_year);
return result;
```
如果分解时间的任何成员包含超出其范围的值，则 `asctime` 函数的行为是未定义的。同样，如果计算出的年份超过四位数或小于 1000，其行为也是未定义的。

### 返回值

`asctime` 函数返回指向字符串的指针。

## 7.27.3.2 ctime 函数

### 概要

```c
#include <time.h>

char *ctime(const time_t *timer);
```

## 描述

`ctime` 函数将 `timer` 指向的日历时间转换为字符串形式的本地时间。它等同于 `asctime(localtime(timer))`。

### 返回值

`ctime` 函数返回以分解时间作为参数的 `asctime` 的返回值。向前引用：`localtime` 函数 (7.27.3.4)。

## 7.27.3.3 gmtime 函数

### 概要

```c
#include <time.h>

struct tm *gmtime(const time_t *timer);
```

## 描述

`gmtime` 函数将 `timer` 指向的日历时间转换为以 UTC 表示的分解时间。

### 返回值

`gmtime` 函数返回指向分解时间的指针，如果指定的时间无法转换为 UTC，则返回空指针。

## 7.27.3.4 localtime 函数

### 概要

```c
#include <time.h>

struct tm *localtime(const time_t *timer);
```

## 描述

`localtime` 函数将 `timer` 指向的日历时间转换为以本地时间表示的分解时间。

### 返回值

`localtime` 函数返回指向分解时间的指针，如果指定的时间无法转换为本地时间，则返回空指针。

## 7.27.3.5 strftime 函数

### 概要

```c
#include <time.h>

size_t strftime(char *restrict s, size_t maxsize, const char *restrict format, const struct tm *restrict timeptr);
```
