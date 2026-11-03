
```
`<assert.h>`
```

## 诊断函数

assert() 函数包含在 `assert.h` 头文件中，可用于向程序添加诊断信息：

```
void assert( int expression );
```

如果在执行 `assert( expression )` 时 `expression` 为零，该函数将在 `stderr` 上打印一条消息，例如：

```
Assertion failed: expression, file filename, line n
```

assert() 函数随后尝试终止程序。

```
`<stdarg.h>`
```

## 参数函数

`stdarg.h` 头文件包含可用于在事先不知道其数量和类型的情况下遍历函数参数列表的函数。由于这些函数的性质，它们必须在函数体内作为“宏”实现。

参数列表被分配给一个名为 `va_list` 的特殊数据类型。以下表格中列出的函数操作名为 “args” 的 `va_list` 类型变量：

| 函数 | 描述 |
|---|---|
| `va_start( va_list args, lastarg )` | 必须调用一次以在最后一个已知参数 `lastarg` 在列表中的位置初始化名为 `args` 的 `va_list`。 |
| `va_arg( va_list args, data-type )` | 在 `va_list args` 由 `va_start()` 初始化后，对 `va_arg()` 的每次后续调用都将以指定的 `data-type` 返回 `args` 列表中下一个参数的值。 |
| `va_end( va_list args )` | 必须在处理完 `va_list args` 中的参数后、在退出函数之前调用一次。 |

## 日期和时间函数

`time.h` 头文件包含用于操作日期和时间的函数。其中一些函数处理“日历时间”，它基于格里高利历。以自纪元（1970 年 1 月 1 日 00:00:00 GMT）以来的秒数表示。

`time.h` 中包含的其他函数处理“本地时间”，它是考虑时区的日历时间的转换。

数据类型 `time_t` 用于描述日历时间和本地时间。

一个名为 `tm` 的结构体包含日历时间的组成部分，列于下表：

| 组件 | 描述 |
|---|---|
| `int tm_sec` | 秒数，分钟后，0-61 |
| `int tm_min` | 分钟数，小时后，0-59 |
| `int tm_hour` | 自午夜以来的小时数，0-23 |
| `int tm_mday` | 月中的日期，1-31 |
| `int tm_mon` | 自一月以来的月份，0-11 |
| `int tm_year` | 自 1900 年以来的年数 |
| `int tm_wday` | 自星期日以来的天数，0-6 |
| `int tm_yday` | 自 1 月 1 日以来的天数，0-365 |
| `int tm_isdst` | 夏令时标志 |

`tm_isdst` 组件如果启用夏令时为正数；如果未启用则为零；如果信息不可用则为负数。

`time.h` 头文件中包含的函数列于第 182 页的表格中。

`time.h` 头文件包含以下可用于操作日期和时间的函数：

| 函数 | 描述 |
|---|---|
| `clock_t clock( void )` | 返回程序启动以来使用的处理器时间，如果不可用则返回 -1 |
| `time_t time( time_t *tp )` | 返回当前日历时间，如果不可用则返回 -1 |
| `double difftime( time_t time2, time_t time1 )` | 返回 time2 减去 time1，以秒表示 |
| `time_t mktime( struct tm *tp )` | 将结构 `*tp` 中的本地时间转换为日历时间 |
| `char *asctime( const struct tm *tp )` | 将 struct `*tp` 中的时间转换为标准字符串 |
| `char *ctime( const time_t *tp )` | 将日历时间转换为本地时间 |
| `struct tm *gmtime( const time_t *tp )` | 将日历时间转换为协调世界时（UTC 或 GMT） |
| `struct tm *localtime( const time_t *tp )` | 将日历时间 `*tp` 转换为本地时间 |
| `size_t strftime( char *s, size_t smax, const char *fmt, const struct tm *tp )` | 将时间 `*tp` 格式化为所选格式 `*fmt` |

`strftime()` 函数根据指定的格式说明符格式化 `tm` 结构体的选定组件。所有可能的格式说明符列于对面页的表格中。

| 说明符 | 描述 |
|---|---|
| `%a` | 星期几的缩写名称 |
| `%A` | 星期几的全称 |
| `%b` | 月份的缩写名称 |
| `%B` | 月份的全称 |
| `%c` | 本地日期和时间表示 |
| `%d` | 月中的日期，01-31 |
| `%H` | 小时（24 小时制），00-23 |
| `%I` | 小时（12 小时制），01-12 |
| `%j` | 一年中的天数，001-366 |
| `%m` | 一年中的月份，01-12 |
| `%M` | 分钟，00-59 |
| `%p` | AM 或 PM 的本地等效表示 |
| `%S` | 秒，00-61（考虑闰秒） |
| `%U` | 一年中的周数（以星期日为一周的第一天），00-53 |
| `%w` | 星期几编号，0-6（星期日为 0） |
| `%W` | 一年中的周数（以星期一为一周的第一天），00-53 |
| `%x` | 本地日期表示 |
| `%X` | 本地时间表示 |
| `%y` | 不带世纪的年份，00-99 |
| `%Y` | 带世纪的年份 |
| `%Z` | 时区名称，如有 |

## 跳转函数

`setjmp.h` 头文件用于控制低级调用，并提供一种避免正常调用和返回序列的方法。

```
int setjmp( jmp_buf env )
Low-level function used in conditional tests to save the environment in the env variable, then return zero

void longjmp( jmp_buf env, int value )
Restores an environment that has been saved in the env variable by setjmp(), as if setjmp() had returned the value
```

## 信号函数

`signal.h` 头文件包含用于处理程序执行期间可能出现的异常情况的函数：

```
void ( *signal( int sig, void ( *handler )( int ) ) )( int )
The signal() function specifies how subsequent signals will be handled. The handler can be SIG_DFL, an implementation-defined default; or SIG_IGN, to ignore the signal. Valid sig signals include:
```

- `SIGABRT`: 中止终止
- `SIGFPE`: 算术错误
- `SIGILL`: 非法指令
- `SIGINT`: 外部中断
- `SIGSEGV`: 访问超出内存限制
- `SIGTERM`: 发送给程序的终止请求

该函数返回该特定信号的处理程序的先前值，如果发生错误则返回 `SIG_ERR`。当下一次出现 `sig` 信号时，信号会恢复为其默认行为，然后调用信号处理程序。如果处理程序返回，执行将从信号发生的位置恢复。

```
int raise( int sig )
Attempts to send the sig signal to the program and returns a non-zero value if the attempt is unsuccessful
```

## 限制常量

下表列出了与最大和最小数值限制相关的常量。它们的值根据实现而变化。如果在括号中给出值，则表示该常量的最小大小——但实际上可能强制执行更大的值。程序不应假设任何实现相关的常量具有特定值。

| 常量 | 值 |
|---|---|
| CHAR_BIT | char 中的位数（8） |
| CHAR_MAX | char 的最大值（UCHAR_MAX 或 SCHAR_MAX） |
| CHAR_MIN | char 的最小值（零或 SCHAR_MIN） |
| INT_MAX | int 的最大值（+32,767） |
| INT_MIN | int 的最小值（-32,767） |
| LONG_MAX | long 的最大值（+2,147,483,647） |
| LONG_MIN | long 的最小值（-2,147,483,647） |
| SCHAR_MAX | signed char 的最大值（+127） |
| SCHAR_MIN | signed char 的最小值（-127） |
| SHRT_MAX | short 的最大值（+32,767） |
| SHRT_MIN | short 的最小值（-32,767） |
| UCHAR_MAX | unsigned char 的最大值（+255） |
| UINT_MAX | unsigned int 的最大值（+65,535） |
| ULONG_MAX | unsigned long 的最大值（+4,294,967,295） |
| USHRT_MAX | unsigned short 的最大值（+65,535） |

## 浮点常量

下表列出了与浮点运算相关的常量。它们的值根据实现而变化。如果在括号中给出值，则表示该常量的最小大小。

| 常量 | 值 |
|---|---|
| `FLT_RADIX` | 浮点指数表示的基数（2） |
| `FLT_ROUNDS` | 四舍五入到最接近的数字 |
| `FLT_DIG` | 精确位数（5） |
| `FLT_EPSILON` | 最小的数 x，使得 1.0 + x != 1.0（1E-5） |
| `FLT_MANT_DIG` | `FLT_RADIX` 尾数位数 |
| `FLT_MAX` | 最大浮点数（1E+37） |
| `FLT_MAX_EXP` | 最大数 n，使得 `FLT_RADIX^(n-1)` 为有效数 |
| `FLT_MIN` | 最小浮点数（1E-37） |
| `FLT_MIN_EXP` | 最小数 n，使得 `FLT_RADIX^(n-1)` 为有效数 |
| `DBL_DIG` | 双精度位数（10） |
| `DBL_EPSILON` | 最小的数 x，使得 1.0 + x != 1.0（1E-9） |
| `DBL_MANT_DIG` | `FLT_RADIX` 尾数位数 |
| `DBL_MAX` | 最大双精度浮点数（1E+37） |
| `DBL_MAX_EXP` | 最大数 n，使得 `FLT_RADIX^(n-1)` 为有效数 |
| `DBL_MIN` | 最小双精度浮点数（1E-37） |
| `DBL_MIN_EXP` | 最小数 n，使得 `FLT_RADIX^(n-1)` 为有效数 |

