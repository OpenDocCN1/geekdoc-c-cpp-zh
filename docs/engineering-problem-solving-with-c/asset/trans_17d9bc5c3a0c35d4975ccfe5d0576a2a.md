
double atof(const char *s);
int atoi(const char *s);
long int atol(const char *s);
double strtod(const char *s, char **endptr);
long int strtol(const char *s, char **endptr, int base);
unsigned long int strtoul(const char *s, char **endptr, int base);
将由 s 指向的字符串的初始部分转换为数值表示。

void* bsearch(const void *key, const void *base, size_t n, size_t size, int(*compar)(const void *, const void *));
在 n 个对象的数组中搜索 key 指向的值。

void* calloc(size_t n, size_t size);
为 n 个对象分配空间，每个对象的大小为 size。

div_t div(int numer, int denom);
ldiv_t ldiv(long int numer, long int denom);
计算 numer 除以 denom 的商和余数。

void exit(int status);
导致正常程序终止。

void free(void *ptr);
释放 ptr 指向的空间。

void* malloc(size_t size);
为大小为 size 的对象分配空间。

void qsort(void *base, size_t nmemb, size_t size, int(*compar)(const void *, const void *));
将 n 个对象排序为升序。

int rand(void);
返回 0 到 RAND_MAX 范围内的伪随机整数。

void* realloc(void *ptr, size_t size);
更改 ptr 指向的对象的大小。

void srand(unsigned int seed);
使用种子初始化来自 RAND 函数的新值序列。

## <cstring>

头文件 <cstring> 定义了类型 size_t（无符号整数）和宏 NULL（值为二进制零）。此外，该头文件还定义了一系列用于处理字符串的函数。

void* memchr(const void *s, int c, size_t n);
返回 s 指向的对象的前 n 个字符中 c 首次出现的位置的指针。

int memcmp(const void *s1, const void *s2, size_t n);
根据 s 指向的字符串与 t 指向的字符串的比较结果（大于、等于或小于），返回相应的大于、等于或小于零的整数。

void* memcpy(void *s, const void *t, size_t n);
将 t 指向的对象中的 n 个字符复制到 s 指向的对象中。

void* memmove(void *s, const void *t, size_t n);
使用临时区域，将 t 指向的对象中的 n 个字符复制到 s 指向的对象中。

void* memset(void *s, int c, size_t n);
将 c 的值复制到 s 指向的对象的前 n 个字符中。

char* strcat(char *s, const char *t);
将 t 指向的字符串连接到 s 指向的字符串的末尾；返回指向 s 指向的字符串的指针。

char* strchr(const char *s, int c);
返回 s 指向的字符串中字符 c 首次出现的位置的指针。

int strcmp(const char *s, const char *t);
按元素逐个比较字符串 s 和字符串 t；根据 s 指向的字符串与 t 指向的字符串分别是大于、等于还是小于，返回大于、等于或小于零的整数。

int strcoll(const char *s, const char *t);
根据 s 指向的字符串与 t 指向的字符串分别是大于、等于还是小于，返回大于、等于或小于零的整数。

char* strcpy(char *s, const char *t);
将 t 指向的字符串复制到 s 指向的字符串；返回指向 s 指向的字符串的指针。

size_t strcspn(const char *s, const char *t);
返回 s 指向的字符串中完全不包含 t 指向的字符串中的字符的初始片段的长度。

size_t strlen(const char *s);
返回 s 指向的字符串的长度。

char* strncat(char *s, const char *t, size_t n);
最多将字符串 t 的 n 个字符连接到字符串 s；返回指向 s 指向的字符串的指针。

int strncmp(const char *s, const char *t, size_t n);
按元素逐个比较字符串 s 和字符串 t 的最多 n 个字符；根据 s 指向的字符串与 t 指向的字符串分别是大于、等于还是小于，返回大于、等于或小于零的整数。

char* strncpy(char *s, const char *t, size_t n);
从 t 指向的字符串复制最多 n 个字符到 s 指向的字符串；如果 t 的字符数少于 n，则 s 将用空字符填充；返回指向 s 的指针。

char* strpbrk(const char *s, const char *t);
返回 s 指向的字符串中 t 指向的字符串的任意字符首次出现的位置的指针。

char* strrchr(const char *s, int c);
返回 s 指向的字符串中字符 c 最后一次出现的位置的指针。

size_t strspn(const char *s, const char *t);
返回 s 指向的字符串中完全包含在 t 指向的字符串中的字符的初始片段的长度。

char* strstr(const char *s, const char *t);
返回 t 指向的字符串在 s 指向的字符串中首次出现的位置的指针。

## <ctime>

头文件 <ctime> 定义了两个宏、四种类型和若干函数，用于表示和操作日历时间和本地时间。类型 clock_t 和 time_t 是能够表示时间的算术类型，结构 tm 包含拆分为秒（tm_sec）、分钟（tm_min）、小时（tm_hour）、月中的天数（tm_mday）、自一月以来的月份（tm_mon）、自 1900 年以来的年份（tm_year）、自周日以来的天数（tm_wday）、自 1 月 1 日以来的天数（tm_yday）以及夏令时标志（tm_isdst）的日历时间；结构中值的顺序取决于系统。相关宏如下：

CLOCKS_PER_SEC
clock 函数返回的值每秒的数量。

NULL
表示二进制零的整数。

随后列出函数原型及其相关计算的简要描述：

char* asctime(const struct tm *timeptr);
返回指向包含转换后时间的字符串的指针。

clock_t clock(void);
返回当前处理器时间。

char* ctime(const time_t *timer);
返回指向包含转换后时间的字符串的指针。

double difftime(time_t time1, time_t time0);
计算两个日历时间之间的差值。

struct tm *gmtime(const time_t *timer);
返回指向以协调世界时表示的时间的指针。

struct tm *localtime(const time_t *timer);
返回指向从日历时间转换而来的时间的指针。

time_t mktime(struct tm *timeptr);
将拆分后的时间转换为日历时间值。

time_t time(time_t *timer);
返回当前日历时间。

size_t strftime(char *s, size_t maxsize, const char *format, const struct tm *timeptr);
将时间转换为格式化的多字节字符序列。

## <iostream>

头文件 <iostream> 包含许多用于标准输入和输出的函数。我们现在以最通用的形式列出其中几个：

### istream 函数：

- `istream& operator >>`
  输入（提取）操作

- `int gcount();`
  返回上一次输入操作提取的字符数。

- `int get(char ch);`
  从输入流中提取一个字符。

- `getline(char_string var, int max, [char delimiter]);`
  读取 max-1 个字符，或直到找到分隔符。\n 是默认分隔符。

- `ignore();`
  从输入流中提取并丢弃一个字符。

- `char peek();`
  返回输入流中下一个字符的值。
  将字符保留在输入流中（不提取）。

- `putback(ch);`
  将最后一个字符放回输入流。

### ostream 函数：

- `ostream& operator<<`
  输出（插入）运算符

- `flush();`
  刷新输出缓冲区。

- `put(ch char);`
  将字符放入输出流。

## 附录 B ASCII 字符代码

下表包含 128 个 ASCII 字符及其等效整数值和二进制值。与整数 1 到 31 对应的字符对计算机系统具有特殊意义。例如，字符 BEL 由整数 7 表示，并导致键盘上的蜂鸣器响起。

字符从低到高的顺序是排序序列，并具有几个有趣的特征。请注意，数字小于大写字母，且大写字母小于小写字母。还要注意，特殊字符并未归组在一起。有些在数字之前，有些在数字之后，有些在大写字母和小写字母之间。

| 字符 | 整数等效值 | 二进制等效值 |
| :--- | :--- | :--- |
| NUL (二进制零) | 0 | 00000000 |
| SOH (报头开始) | 1 | 00000001 |
| STX (文本开始) | 2 | 00000010 |
| ETX (文本结束) | 3 | 00000011 |
| EOT (传输结束) | 4 | 00000100 |
| ENQ (查询) | 5 | 00000101 |
| ACK (确认) | 6 | 00000110 |
| BEL (铃声) | 7 | 00000111 |
| BS (退格) | 8 | 00001000 |
| HT (水平制表) | 9 | 00001001 |
| LF (换行或新行) | 10 | 00001010 |
| VT (垂直制表) | 11 | 00001011 |
| FF (换页) | 12 | 00001100 |
| CR (回车) | 13 | 00001101 |
| SO (移出) | 14 | 00001110 |
| SI (移入) | 15 | 00001111 |
| DLE (数据链路转义) | 16 | 00010000 |
| DC1 (设备控制 1) | 17 | 00010001 |
| DC2 (设备控制 2) | 18 | 00010010 |
| DC3 (设备控制 3) | 19 | 00010011 |
| DC4 (设备控制 4-停止) | 20 | 00010100 |
| NAK (否定确认) | 21 | 00010101 |
| SYN (同步) | 22 | 00010110 |
| ETB (文本块结束) | 23 | 00010111 |
| CAN (取消) | 24 | 00011000 |
| EM (介质结束) | 25 | 00011001 |
| SUB (替换) | 26 | 00011010 |
| | | (继续) |
