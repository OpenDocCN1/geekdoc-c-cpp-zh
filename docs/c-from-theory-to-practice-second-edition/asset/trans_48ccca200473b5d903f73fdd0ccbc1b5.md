
`char *strcat(char *str1, const char *str2):` 将 str2 所指向的字符串追加到 str1 所指向的字符串末尾并添加空字符。它返回指向连接后字符串的 str1。

`char *strchr(const char *str, int val):` 在 str 所指向的字符串中搜索字符 val。如果找到则返回指向其首次出现位置的指针，否则返回 NULL。

`int strcmp(const char *str1, const char *str2):` 比较 str1 和 str2 所指向的字符串，并根据第一个字符串是否按字典序小于、等于或大于第二个字符串返回负值、零或正值。

`int strcoll(const char *str1, const char *str2):` 根据当前区域设置规则比较 str1 和 str2 所指向的字符串并返回比较结果。

`char *strcpy(char *dest, const char *src):` 将 src 所指向的字符串复制到 dest 所指向的数组中。它返回 dest 指针。

`size_t strcspn(const char *str, const char *set):` 它返回 str 所指向的字符串中不包含 set 所指向字符串中任何字符的最长部分的长度。

`char *strerror(int err):` 它返回指向包含对应于 err 的错误消息的字符串的指针。

`size_t strlen(const char *str):` 它返回 str 所指向的字符串的长度，不包括空字符。

`char *strncat(char *str1, const char *str2, size_t count):` 将 str2 所指向的字符串中的 count 个字符追加到 str1 所指向的字符串末尾并添加空字符。它返回指向连接后字符串的 str1。

`int strncmp(const char *str1, const char *str2, size_t count):` 比较 str1 和 str2 所指向的字符串的 count 个字符并返回比较结果。

`char *strncpy(char* dest, const char *src, size_t count):` 将 src 所指向的字符串的 count 个字符复制到 dest 所指向的字符串中。它返回 dest 指针。

`char *strpbrk(const char *str, const char *set):` 它返回 str 所指向的字符串中第一个包含在 set 所指向的字符串中的字符的指针。如果未找到匹配项则返回 NULL。

`char *strrchr(const char *str, int val):` 它返回 str 所指向的字符串中 val 的最后一次出现的指针。如果不包含则返回 NULL。

`size_t strspn(const char *str, const char *set):` 它返回 str 所指向的字符串中完全由 set 所指向的字符串的字符组成的最长部分的长度。

`char *strstr(const char *str1, const char *str2):` 检查 str2 所指向的字符串是否包含在 str1 所指向的字符串中。如果包含，则返回其在 str1 中首次出现的指针，否则返回 NULL。

`char *strtok(char *str, const char *set)`: 在 str 所指向的字符串中搜索由不在 set 所指向的字符串中的字符组成的段。如果找到，则返回指向该段第一个字符的指针，否则返回 NULL。

`size_t strxfrm(char *dest, const char *src, size_t count)`: 使用当前区域设置将 src 所指向的字符串的 count 个字符转换并将结果存储到 dest 所指向的数组中。它返回转换后字符串的长度。

## <time.h>

`char *asctime(const struct tm *ptr)`: 将 ptr 所指向的 tm 类型结构中存储的日期和时间信息转换为形如 "Sun Nov 13 11:13:58 2016" 的字符串。它返回指向构造的字符串的指针。

`clock_t clock(void)`: 它返回自程序执行开始以来的经过时间，以处理器时钟滴答为单位。要将其转换为秒，请将该值除以常量 CLOCKS_PER_SEC。

`char *ctime(const time_t *ptr)`: 将 ptr 所指向的 time_t 类型结构中存储的日历时间转换为形如 "Sun Nov 13 11:13:58 2016" 的字符串，并根据本地时区设置进行调整。它返回指向构造的字符串的指针。

`double difftime(time_t t1, time_t t0)`: 它返回以秒为单位的时间差 t1-t0。

`struct tm *gmtime(const time_t *ptr)`: 将 ptr 所指向的日历时间转换为通用时间并返回指向保存结果的 tm 类型结构的指针。

`struct tm *localtime(const time_t *ptr)`: 将 ptr 所指向的日历时间转换为本地时间并返回指向保存结果的 tm 类型结构的指针。

`time_t mktime(struct tm *ptr)`: 将 ptr 所指向的本地时间转换为日历时间并返回保存结果的 time_t。

`size_t strftime(char *str, size_t size, const char *fmt, const struct tm *ptr)`: 根据 fmt 所指向的格式字符串格式化 ptr 所指向的时间信息并将 size 个字符存储到 str 所指向的数组中。它返回存储的字符数。

`time_t time(time_t *ptr)`: 返回当前日历时间。

## 附录 4：十六进制系统

本附录提供了十六进制系统的简要描述。十六进制系统的基数为 16。数字 0-9 与十进制系统相同。数字 10-15 用字母 A 到 F 表示。十六进制系统与二进制和十进制系统的对应关系在表 A.4.1 中显示。

如图所示，每个十六进制数字（0 到 F）用四个二进制数字表示。例如，十六进制数 F4A 在二进制中写为 1111 0100 1010。

要找到由 n 个数字组成的十六进制数的十进制值（例如，dₙ₋₁ … d₂ d₁ d₀），我们应用以下公式：

Decimal = Σᵢ₌₀ⁿ⁻¹ (dᵢ × 16ⁱ).

例如，F4A 的十进制值为 (A × 16⁰) + (4 × 16¹) + (F × 16²) = 10 + 64 + 3840 = 3914。

表 A.4.1
十六进制、二进制和十进制系统

| 十六进制 | 二进制 | 十进制 |
|---|---|---|
| 0 | 0000 | 0 |
| 1 | 0001 | 1 |
| 2 | 0010 | 2 |
| 3 | 0011 | 3 |
| 4 | 0100 | 4 |
| 5 | 0101 | 5 |
| 6 | 0110 | 6 |
| 7 | 0111 | 7 |
| 8 | 1000 | 8 |
| 9 | 1001 | 9 |
| A | 1010 | 10 |
| B | 1011 | 11 |
| C | 1100 | 12 |
| D | 1101 | 13 |
| E | 1110 | 14 |
| F | 1111 | 15 |

## 索引

页码后跟 f 和 t 分别表示图和表。

, (comma) 运算符，56–57
在 for 语句中，106
?:（条件）运算符，88–89
运算符，62
优先级，64

A

抽象接口，Java，626，627，628
abstract 修饰符，Java，617，619–620
可访问性
C++ 中的类数据，581
一维数组，元素，152–154
accessibility_type，590
访问修饰符（A_M），Java，612，616–620，617t
private，617
protected，617
public，616–617
add () 函数，606
add_list_end() 函数，487
add_node() 函数，491
地址运算符 &，35，189
& 地址运算符，35，189
add_sort() 函数，389–390
add_stack() 函数，477–478，487
ALERTING 消息结构，联合，442f
ISDN 网络，443–445
算法
二分查找，383–386
冒泡排序，395–398
插入排序，392–394，393f
线性查找，381–383
快速排序，398–400
选择排序，386–392
美国国家标准学会（ANSI），1
美国信息交换标准代码（ASCII）代码，12，15，239，253，258，284
字符集，242，665，666t
在文件中，507
大小写字母及其值，242

ANSI C（Standard C），1
ANSI/ISO C 标准，1
a.out，8，577
argc（argument count）参数，364，365，612
args[] 参数，612
参数
数组，330
转换，330
定义，307
在 main () 中，364
一维数组作为，330–336
指针，308
结构作为，424–426
二维数组作为，358–364
使用 const，332
变长列表，367
与参数对比，307
算术，指针，199–201
算术转换，15–18
显式转换，17–18
隐式转换，16–17
算术运算符，46–47
算术溢出，46
ARP 数据包结构，MAC，355–357，356f
ARP_Relay，355
ARP_Request，355
指针数组，216–218
到函数，231–235
数组，151–184；另见 Structures；Unions；Variable(s)
访问，152
地址，204，206，303
作为参数，330
常见错误，153
const 限定符，155
复制，153
定义，151
从中删除键，500–501
五个整数（示例），153–154
长度，151，154
内存大小，152
多维，171
