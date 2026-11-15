

- `double log(double x);` 计算 ln x，即 x 以 e 为底的自然对数；如果 x <= 0 则发生错误
- `double log10(double x);` 计算 log10 x，即 x 以 10 为底的常用对数；如果 x <= 0 则发生错误
- `double pow(double x, double y);` 计算 x 的 y 次幂，即 x^y；如果 x = 0 且 y <= 0，或者 x < 0 且 y 不是整数，则发生错误
- `double sin(double x);` 计算 x 的正弦值，其中 x 为弧度
- `double sinh(double x);` 计算 x 的双曲正弦值，等于 (e^x - e^-x)/2
- `double sqrt(double x);` 计算 x 的平方根，其中 x >= 0
- `double tan(double x);` 计算 x 的正切值，其中 x 为弧度
- `double tanh(double x);` 计算 x 的双曲正切值，等于 sinh x / cosh x

头文件 `<cstdlib>` 定义了未包含在其他任何头文件中的类型、宏和函数。类型 `div_t` 和 `ldiv_t` 是用于存储商和余数的结构。宏如下：

- NULL
- 二进制零的整数值
- EXIT_FAILURE
- EXIT_SUCCESS
- 分别用于向主机返回不成功或成功终止状态的积分表达式
- RAND_MAX
- 返回 RAND 函数最大值的积分表达式
- MB_CUR_MAX
- 值为多字节字符最大字节数的正整数表达式

工程应用中最可能使用的函数如下，附带函数原型声明和简要描述：

- `void abort(void);` 导致程序异常终止
- `int abs(int k);`
- `long int labs(long int k);` 计算整数 k 的绝对值
- `int atexit(void (*func)(void));` 注册由 func 指向的函数，在正常程序终止时无参数调用
- `double atof(const char *s);`
- `int atoi(const char *s);`
- `long int atol(const char *s);`
- `double strtod(const char *s, char **endptr);`
- `long int strtol(const char *s, char **endptr, int base);`
- `unsigned long int strtoul(const char *s, char **endptr, int base);`
  将 s 指向的字符串的初始部分转换为数值表示
- `void* bsearch(const void *key, const void *base, size_t n, int (*compar)(const void *, const void *));`
  在 n 个对象的数组中搜索 key 指向的值
- `void* calloc(size_t n, size_t size);`
  为 n 个对象（每个大小为 size）的数组分配空间
- `div_t div(int numerator, int denom);`
- `ldiv_t ldiv(long int numer, long int denom);`
  计算 numer 除以 denom 的商和余数
- `void exit(int status);`
  导致正常程序终止
- `void free(void *ptr);`
  释放 ptr 指向的空间
- `void* malloc(size_t size);`
  为大小为 size 的对象分配空间
- `void* qsort(void *base, size_t nmemb, size_t size, int (*compar)(const void *, const void *));`
  将 n 个对象排序为升序
- `int rand(void);`
  返回 0 到 RAND_MAX 范围内的伪随机整数
- `void* realloc(void *ptr, size_t size);`
  更改 ptr 指向的对象的大小
- `void srand(unsigned int seed);`
  使用种子初始化来自 RAND 函数的新值序列

## <cstring>

头文件 <cstring> 定义了类型 size_t（无符号整数）和宏 NULL（值为二进制零）。此外，该头文件还定义了一系列用于处理字符串的函数。

- `void* memchr(const void *s, int c, size_t n);`
  返回 s 指向的对象的前 n 个字符中 c 首次出现的位置的指针
- `int memcmp(const void *s1, const void *s2, size_t n);`
  返回大于、等于或小于零的整数，具体取决于 s1 指向的字符串分别是大于、等于还是小于 s2 指向的字符串
- `void* memcpy(void *s, const void *t, size_t n);` 将 t 指向的对象中的 n 个字符复制到 s 指向的对象中
- `void* memmove(void *s, const void *t, size_t n);` 使用临时区域，将 t 指向的对象中的 n 个字符复制到 s 指向的对象中
- `void* memset(void *s, int c, size_t n);` 将 c 的值复制到 s 指向的对象的前 n 个字符中
- `char* strcat(char *s, const char *t);` 将 t 指向的字符串连接到 s 指向的字符串末尾；返回指向 s 指向的字符串的指针
- `char* strchr(const char *s, int c);` 返回 s 指向的字符串中字符 c 首次出现的位置的指针
- `int strcmp(const char *s, const char *t);` 对字符串 s 和字符串 t 进行逐元素比较；根据 s 指向的字符串分别是大于、等于还是小于 t 指向的字符串，返回大于、等于或小于零的整数
- `int strcoll(const char *s, const char *t);` 根据 s 指向的字符串分别是大于、等于还是小于 t 指向的字符串，返回大于、等于或小于零的整数
- `char* strcpy(char *s, const char *t);` 将 t 指向的字符串复制到 s 指向的字符串；返回指向 s 指向的字符串的指针
- `size_t strcspn(const char *s, const char *t);` 返回 s 指向的字符串的初始段长度，该初始段完全由不在 t 指向的字符串中的字符组成
- `size_t strlen(const char *s);` 返回 s 指向的字符串的长度
- `char* strncat(char *s, const char *t, size_t n);` 最多将字符串 t 的 n 个字符连接到字符串 s；返回指向 s 指向的字符串的指针
- `int strncmp(const char *s, const char *t, size_t n);` 最多对字符串 s 和字符串 t 的 n 个字符进行逐元素比较；根据 s 指向的字符串分别是大于、等于还是小于 t 指向的字符串，返回大于、等于或小于零的整数
- `char* strncpy(char *s, const char *t, size_t n);` 最多从 t 指向的字符串复制 n 个字符到 s 指向的字符串；如果 t 的字符少于 s，则 s 用空字符填充；返回指向 s 的指针
- `char* strpbrk(const char *s, const char *t);` 返回 s 指向的字符串中 t 指向的字符串的任意字符首次出现的位置的指针
- `char* strrchr(const char *s, int c);` 返回 s 指向的字符串中字符 c 最后一次出现的位置的指针
- `size_t strspn(const char *s, const char *t);` 返回 s 指向的字符串的初始段长度，该初始段完全由 t 指向的字符串中的字符组成
- `char* strstr(const char *s, const char *t);` 返回 t 指向的字符串在 s 指向的字符串中起始位置的指针

## <ctime>

头文件 <ctime> 定义了两个宏、四种类型和若干函数，用于表示和操作日历时间和本地时间。类型 clock_t 和 time_t 是能够表示时间的算术类型，结构 tm 包含拆分为秒（tm_sec）、分钟（tm_min）、小时（tm_hour）、日期（tm_mday）、自一月以来的月份（tm_mon）、自 1900 年以来的年份（tm_year）、自周日以来的天数（tm_wday）、自 1 月 1 日以来的天数（tm_yday）以及夏令时标志（tm_isdst）的日历时间；结构中值的顺序取决于系统。相关宏如下：

- CLOCKS_PER_SEC
  clock 函数返回值的每秒数
- NULL
  表示二进制零的整数

随后是函数原型及其相关计算的简要描述：

- `char* asctime(const struct tm *timeptr);`
  返回指向包含转换后时间的字符串的指针
- `clock_t clock(void);`
  返回当前处理器时间
- `char* ctime(const time_t *time);`
  返回指向包含转换后时间的字符串的指针
- `double difftime(time_t time1, time_t time0);`
  计算两个日历时间之间的差值
- `struct tm *gmtime(const time_t *timer);`
  返回指向以协调世界时表示的时间的指针
- `struct tm *localtime(const time_t *timer);`
  返回指向从日历时间转换而来的时间的指针
- `time_t mktime(struct tm *timeptr);`
  将分解的时间转换为日历时间值
- `time_t time(time_t *timer);`
  返回当前日历时间
- `size_t strftime(char *s, size_t maxsize, const char *format, const struct tm *timeptr);`
  将时间转换为格式化的多字节字符序列

