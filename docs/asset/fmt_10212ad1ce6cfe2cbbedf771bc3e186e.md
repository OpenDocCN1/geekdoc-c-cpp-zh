
# 第四部分

附录 I: ASCII 符号完整列表
附录 II: C 关键字和运算符完整列表
附录 III: C 库所有函数的按头文件列表

本页留白。

# 附录 I
## ASCII 符号完整列表

### ASCII 表

数值列 – 十进制对应关系 - 字符

| 0 | NUL | 14 | SO | 28 | FS |
|---|---|---|---|---|---|
| 1 | SOH | 15 | SI | 29 | GS |
| 2 | STX | 16 | DLE | 30 | RS |
| 3 | ETX | 17 | DC1 | 31 | US |
| 4 | EOT | 18 | DC2 | 32 | SP |
| 5 | ENQ | 19 | DC3 | 33 | ! |
| 6 | ACK | 20 | DC4 | 34 | " |
| 7 | BEL | 21 | NAK | 35 | # |
| 8 | BS | 22 | SYN | 36 | $ |
| 9 | HT | 23 | ETB | 37 | % |
| 10 | LF | 24 | CAN | 38 | & |
| 11 | VT | 25 | EM | 39 | ' |
| 12 | FF | 26 | SUB | 40 | ( |
| 13 | CR | 27 | ESC | 41 | ) |

| 42 | * | 71 | G | 100 | d |
|---|---|---|---|---|---|
| 43 | + | 72 | H | 101 | e |
| 44 | , | 73 | I | 102 | f |
| 45 | - | 74 | J | 103 | g |
| 46 | . | 75 | K | 104 | h |
| 47 | / | 76 | L | 105 | i |
| 48 | 0 | 77 | M | 106 | j |
| 49 | 1 | 78 | N | 107 | k |
| 50 | 2 | 79 | O | 108 | l |
| 51 | 3 | 80 | P | 109 | m |
| 52 | 4 | 81 | Q | 110 | n |
| 53 | 5 | 82 | R | 111 | o |
| 54 | 6 | 83 | S | 112 | p |
| 55 | 7 | 84 | T | 113 | q |
| 56 | 8 | 85 | U | 114 | r |
| 57 | 9 | 86 | V | 115 | s |
| 58 | : | 87 | W | 116 | t |
| 59 | ; | 88 | X | 117 | u |
| 60 | < | 89 | Y | 118 | v |
| 61 | = | 90 | Z | 119 | w |
| 62 | > | 91 | [ | 120 | x |
| 63 | ? | 92 | \ | 121 | y |
| 64 | @ | 93 | ] | 122 | z |
| 65 | A | 94 | ^ | 123 | { |
| 66 | B | 95 | _ | 124 | \| |
| 67 | C | 96 | ` | 125 | } |
| 68 | D | 97 | a | 126 | ~ |
| 69 | E | 98 | b | 127 | DEL |
| 70 | F | 99 | c | | |

# 附录 II
## C 语言关键字和运算符完整列表

### 运算符与关键字

| 运算符 | 含义 |
|---|---|
| `+` | 加法或一元加 |
| `-` | 减法或一元负 |
| `*` | 乘法 |
| `/` | 除法 |
| `%` | 取模运算符（取余数） |
| `<` | 小于 |
| `<=` | 小于等于 |
| `>` | 大于 |
| `>=` | 大于等于 |
| `==` | 等于 |
| `!=` | 不等于 |
| `&&` | 逻辑与 (AND) |
| `\|\|` | 逻辑或 (OR) |
| `!` | 逻辑非 (NOT) |
| `+=` | 加等于赋值 |
| `-=` | 减等于赋值 |
| `*=` | 乘等于赋值 |
| `/=` | 除等于赋值 |
| `%=` | 取模等于赋值 |
| `++` | 增一 |
| `--` | 减一 |
| `?:` | 三元运算符 |
| `&` | 位与 |
| `\|` | 位或 |
| `^` | 位异或 |
| `<<` | 左移 |
| `>>` | 右移 |
| `sizeof` | 字节大小 |

### 运算符优先级

| 顺序 | 类别 | 运算符 | 操作 | 结合性 |
|---|---|---|---|---|
| 1 | 最高优先级 | `()` `[]` `->` `.` | 函数调用、数组下标、结构成员访问 | 从左到右 |
| 2 | 一元 | `!` `~` `+` `-` `++` `--` `&` `*` `sizeof` | 逻辑非、位按 1 补码、一元加、一元负、前置/后增、前置/后减、地址、间接、操作数的大小（以字节为单位） | 从右到左 |
| 3 | 成员访问 | `.` `->` | 结构/联合成员访问、指针成员访问 | 从左到右 |
| 4 | 乘法 | `*` `/` `%` | 乘、除、取模 | 从左到右 |
| 5 | 加法 | `+` `-` | 二元加、二元减 | 从左到右 |
| 6 | 移位 | `<<` `>>` | 左移、右移 | 从左到右 |
| 7 | 关系 | `<` `<=` `>` `>=` | 小于、小于等于、大于、大于等于 | 从左到右 |
| 8 | 相等 | `==` `!=` | 等于、不等于 | 从左到右 |
| 9 | 位与 | `&` | 位与 | 从左到右 |
| 10 | 位异或 | `^` | 位异或 | 从左到右 |
| 11 | 位或 | `\|` | 位或 | 从左到右 |
| 12 | 逻辑与 | `&&` | 逻辑与 | 从左到右 |
| 13 | 逻辑或 | `\|\|` | 逻辑或 | 从左到右 |
| 14 | 条件 | `?:` | 三元条件运算符 | 从右到左 |
| 15 | 赋值 | `=` `*=` `/=` `%=` `+=` `-=` `&=` `^=` `\|=` `<<=` `>>=` | 赋值、乘法赋值、除法赋值、取模赋值、加法赋值、减法赋值、位与赋值、位异或赋值、位或赋值、左移赋值、右移赋值 | 从右到左 |

### 关键字

`auto` `break` `case` `const` `continue` `default`
`do` `double` `else` `extern` `float` `for`
`goto` `if` `int` `long` `register` `short`
`signed` `sizeof` `static` `struct` `switch` `typedef`
`unsigned` `void` `volatile` `while` `union`

***

![](img/42571661744bb1de16ed6abc45190753_226_0.png)

# 附录 III
## C 标准库中所有函数的按头文件分类列表

### C 标准库函数

| 序号 | 头文件 | 函数 | 声明 | 描述 |
|---|---|---|---|---|
| 1. | `assert.h` | `assert` | `void assert(int expression);` | `assert` 宏允许将诊断信息写入标准错误文件。如果表达式求值为 0（假），则该表达式、源代码文件名， |
| 2. | `ctype.h` | `isalnum` | `int isalnum(int c);` | 测试字符是否为字母数字。 |
| | | `isalpha` | `int isalpha(int c);` | 测试字符是否为字母。 |
| | | `isdigit` | `int isdigit(int c);` | 测试字符是否为数字。 |
| | | `isxdigit` | `int isxdigit(int c);` | 测试字符是否为十六进制数字。 |
| | | `isprint` | `int isprint(int c);` | 测试字符是否为可打印字符。 |
| | | `isspace` | `int isspace(int c);` | 测试字符是否为空白字符。 |
| | | `islower` | `int islower(int c);` | 测试字符是否为小写字母。 |
| | | `isupper` | `int isupper(int c);` | 测试字符是否为大写字母。 |
| | | `iscntrl` | `int iscntrl(int c);` | 测试字符是否为控制字符。 |
| | | `isgraph` | `int isgraph(int c);` | 测试字符是否为可打印字符（非空格）。 |
| | | `toupper` | `int toupper(int c);` | 将小写字母转换为大写。 |
| | | `tolower` | `int tolower(int c);` | 将大写字母转换为小写。 |
| | | `isxdigit` | `int isxdigit(int c);` | 测试字符是否为十六进制数字。 |
| 3. | `errno.h` | `abort` | `void abort(void);` | 异常终止程序。 |
| | | `exit` | `void exit(int);` | 正常终止程序。 |
| | | `errno` | `int errno;` | 获取全局错误编号。 |
| 4. | `math.h` | `acos` | `double acos(double x);` | 返回 x 的反余弦。 |
| | | `asin` | `double asin(double x);` | 返回 x 的反正弦。 |
| | | `atan` | `double atan(double x);` | 返回 x 的反正切。 |
| | | `atan2` | `double atan2(double y, double x);` | 返回 y/x 的反正切。 |
| | | `cos` | `double cos(double x);` | 返回弧度 x 的余弦。 |
| | | `cosh` | `double cosh(double x);` | 返回 x 的双曲余弦。 |
| | | `sin` | `double sin(double x);` | 返回弧度 x 的正弦。 |
| | | `sinh` | `double sinh(double x);` | 返回 x 的双曲正弦。 |
| | | `sqrt` | `double sqrt(double x);` | 返回 x 的平方根。 |
| | | `exp` | `double exp(double x);` | 返回 e 的 x 次方。 |
| | | `pow` | `double pow(double x, double y);` | 返回 x 的 y 次方。 |
| | | `log` | `double log(double x);` | 返回 x 的自然对数（以 e 为底）。 |
| | | `log10` | `double log10(double x);` | 返回 x 的常用对数（以 10 为底）。 |
| | | `floor` | `double floor(double x);` | 返回小于等于 x 的最大整数。 |
| | | `ceil` | `double ceil(double x);` | 返回大于等于 x 的最小整数。 |
| | | `fmod` | `double fmod(double x, double y);` | 返回 x 除以 y 的余数。 |
| | | `frexp` | `double frexp(double x, int *exponent);` | 将浮点数 x 分解为尾数和指数。 |
| | | `ldexp` | `double ldexp(double x, int exponent);` | 返回 x 乘以 2 的指数次方。 |
| | | `modf` | `double modf(double x, double *integer);` | 将浮点数 x 分解为整数和分数部分。返回的值是小数部分，并设置整数部分。 |
| | | `tan` | `double tan(double x);` | 返回弧度 x 的正切。 |
| | | `tanh` | `double tanh(double x);` | 返回 x 的双曲正切。 |
| 5. | `setjmp.h` | `setjmp` | `int setjmp(jmp_buf environment);` | 将环境保存到变量 `environment` 中。如果返回非零值，则表示源代码中的该点是通过 `longjmp` 到达的。否则返回零，表示环境已保存。 |
| | | `longjmp` | `void longjmp(jmp_buf environment, int value);` | 从 `setjmp` 调用处恢复环境，该调用处的环境变量 `environment` 已保存。 |
| 6. | `signal.h` | 宏: `SIG_DFL` `SIG_ERR` `SIG_IGN` `SIGABRT` `SIGFPE` `SIGILL` `SIGINT` `SIGSEGV` `SIGTERM` | | 默认处理程序。表示信号错误。忽略信号。异常终止（由 `abort` 函数生成）。浮点数错误（由除以零、无效操作等引起的错误）。非法操作（指令）。交互式注意信号（如 ctrl-C）。对存储的无效访问（段错误、内存违规）。终止请求。 |
| | | `signal` | `void (*signal(int sig, void (*func)(int)))(int);` | 控制信号如何被处理，`sig` 代表与 `SIG` 宏兼容的信号值。`func` 是信号发生时要调用的函数。 |
| | | `raise` | `int raise(int sig);` | 产生信号 `sig`。`sig` 参数与 `SIG` 宏兼容。 |
| 7. | `stdarg.h` | `va_start` | `void va_start(va_list ap, last_arg);` | 为配合 `va_arg` 和 `va_end` 宏进行初始化。`last_arg` 是传递给函数的最后一个已知固定参数。 |
| | | `va_arg` | `type va_arg(va_list ap, type);` | 展开为函数参数列表中具有指定类型的下一个参数。 |
| | | `va_end` | `void va_end(va_list ap);` | 允许使用 `va_start` 宏的变长参数函数返回。 |
| 8. | `stddef.h` | `offsetof` | `offsetof(type, member)` | 产生一个 `size_t` 类型的常量整数，表示结构体成员从结构体开始的字节偏移。 |
| 9. | `stdio.h` | 宏 | | |
| | | `_IOFBF` `_IOLBF` `_IONBF` | | 用于 `setvbuf` 函数。 |
| | | `BUFSIZ` | | `BUFSIZ` 是一个整数，表示 `setbuf` 函数使用的缓冲区大小。 |
| | | `EOF` | | `EOF` 是一个负整数，表示已到达文件末尾。 |
| | | `FOPEN_MAX` | | `FOPEN_MAX` 是整数，表示系统可以保证同时打开的文件最大数量。 |
| | | `FILENAME_MAX` | | `FILENAME_MAX` 是整数，表示适合持有最长文件名的字符数组长度。 |
| | | `L_tmpnam` | | `L_tmpnam` 是整数，表示适合持有由 `tmpnam` 函数创建的最长临时文件名的字符数组长度。 |
| | | `SEEK_CUR` `SEEK_END` `SEEK_SET` | | 用于 `fseek` 函数。 |
| | | `TMP_MAX` | | `TMP_MAX` 是函数 `tmpnam` 可以生成的唯一文件名最大数量。 |
| | | `stderr` `stdin` `stdout` | | `stderr`、`stdin` 和 `stdout` 是指向 `FILE` 类型的指针，分别对应标准错误、标准输入、标准输出流。 |
| | | `clearerr` | `void clearerr(FILE *stream);` | 清除给定流的文件末尾指示和错误指示。 |
| | | `fclose` | `int fclose(FILE *stream);` | 关闭流。所有缓冲区都会被刷新。 |
| | | `feof` | `int feof(FILE *stream);` | 测试给定流的文件末尾指示。 |
| | | `ferror` | `int ferror(FILE *stream);` | 测试给定流的错误指示。 |
| | | `fflush` | `int fflush(FILE *stream);` | 刷新流的输出缓冲区。 |
| | | `fgetpos` | `int fgetpos(FILE *stream, fpos_t *pos);` | 获取当前文件位置并将其写入 `pos`。 |
| | | `fopen` | `FILE *fopen(const char *filename, const char *mode);` | 打开 `filename` 指向的文件。 |
| | | `fread` | `size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);` | 从给定流读取数据到 `ptr` 指向的数组。 |
| | | `freopen` | `FILE *freopen(const char *filename, const char *mode, FILE *stream);` | 将新文件名与给定流关联。 |
| | | `fseek` | `int fseek(FILE *stream, long offset, int whence);` | 设置流的文件位置为给定的偏移量。 |
| | | `fsetpos` | `int fsetpos(FILE *stream, const fpos_t *pos);` | 设置流的文件位置为 `pos`。 |
| | | `ftell` | `long ftell(FILE *stream);` | 获取流当前的位置。 |
| | | `fwrite` | `size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);` | 将 `ptr` 指向的数据写入流。 |
| | | `remove` | `int remove(const char *filename);` | 删除指定的文件。 |
| | | `rename` | `int rename(const char *oldfilename, const char *newfilename);` | 将旧文件名重命名为新文件名。 |
| | | `rewind` | `void rewind(FILE *stream);` | 将流的位置回到开头。 |
| | | `setbuf` | `void setbuf(FILE *stream, char *buffer);` | 设置流如何缓冲。 |
| | | `setvbuf` | `int setvbuf(FILE *stream, char *buffer, int mode, size_t size);` | 设置流的缓冲模式。 |
| | | `tmpfile` | `FILE *tmpfile(void);` | 创建临时文件并在程序终止时关闭。 |
| | | `tmpnam` | `char *tmpnam(char *str);` | 生成有效的临时文件名。 |
| | | `fprintf` | `int fprintf(FILE *stream, const char *format, ...);` | 向流输出格式化数据。 |
| | | `fscanf` | `int fscanf(FILE *stream, const char *format, ...);` | 从流读取格式化数据。 |
| | | `printf` | `int printf(const char *format, ...);` | 向标准输出输出格式化数据。 |
| | | `scanf` | `int scanf(const char *format, ...);` | 从标准输入读取格式化数据。 |
| | | `sprintf` | `int sprintf(char *str, const char *format, ...);` | 向字符串 `str` 输出格式化数据。 |
| | | `sscanf` | `int sscanf(const char *str, const char *format, ...);` | 从字符串 `str` 读取格式化数据。 |
| | | `vprintf` | `int vprintf(const char *format, va_list arg);` | 使用参数列表向标准输出输出数据。 |
| | | `vfprintf` | `int vfprintf(FILE *stream, const char *format, va_list arg);` | 使用参数列表向流输出数据。 |
| | | `vsprintf` | `int vsprintf(char *str, const char *format, va_list arg);` | 使用参数列表向字符串输出数据。 |
| | | `getc` | `int getc(FILE *stream);` | 获取流的字符。 |
| | | `fgets` | `char *fgets(char *str, int n, FILE *stream);` | 从指定流读取一行并存入字符串 `str`。 |
| | | `fputc` | `int fputc(int char, FILE *stream);` | 将字符写入指定流并移动位置指示器。 |
| | | `fputs` | `int fputs(const char *str, FILE *stream);` | 向指定流写入字符串，但不包括空字符。 |
| | | `getchar` | `int getchar(void);` | 从标准输入获取字符。 |
| | | `gets` | `char *gets(char *str);` | 从标准输入读取一行并存入字符串 `str`。 |
| | | `putc` | `int putc(int char, FILE *stream);` | 将字符写入指定流并移动位置指示器。 |
| | | `putchar` | `int putchar(int char);` | 将字符写入标准输出。 |
| | | `puts` | `int puts(const char *str);` | 向标准输出写入字符串，但不包括空字符。 |
| | | `ungetc` | `int ungetc(int char, FILE *stream);` | 将字符推入指定流，以便下次读取。 |
| | | `perror` | `void perror(const char *str);` | 向标准错误输出打印描述性错误信息。 |
| 10. | `stdlib.h` | `abort` | `void abort(void);` | 导致程序异常终止。 |
| | | `abs` | `int abs(int x);` | 返回 x 的绝对值。 |
| | | `atexit` | `int atexit(void (*func)(void));` | 在程序正常终止时调用指定的函数。 |
| | | `atof` | `double atof(const char *str);` | 将参数 `str` 指向的字符串转换为浮点数（double 类型）。 |
| | | `atoi` | `int atoi(const char *str);` | 将参数 `str` 指向的字符串转换为整数（int 类型）。 |
| | | `atol` | `long int atol(const char *str);` | 将参数 `str` 指向的字符串转换为长整数（long int）。 |
| | | `bsearch` | `void *bsearch(const void *key, const void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *));` | 执行二分查找。 |
| | | `calloc` | `void *calloc(size_t nitems, size_t size);` | 分配请求的内存并返回其指针。 |
| | | `div` | `div_t div(int numer, int denom);` | 将 `numer`（分子）除以 `denom`（除数）。 |
| | | `free` | `void free(void *ptr);` | 释放之前通过 `calloc`、`malloc` 或 `realloc` 分配的内存。 |
| | | `exit` | `void exit(int status);` | 使程序正常终止。 |
| | | `getenv` | `char *getenv(const char *name);` | 查找 `name` 指向的环境字符串并返回关联的值。 |
| | | `labs` | `long int labs(long int x);` | 返回 `x` 的绝对值。 |
| | | `ldiv` | `ldiv_t ldiv(long numer, long int denom);` | 将 `numer`（分子）除以 `denom`（除数）。 |
| | | `malloc` | `void *malloc(size_t size);` | 分配请求的内存并返回其指针。 |
| | | `mblen` | `int mblen(const char *str, size_t n);` | 返回参数 `str` 指向的多字节字符的长度。 |
| | | `mbstowcs` | `size_t mbstowcs(wchar_t *pwcs, const char *str, size_t n);` | 将参数 `str` 指向的多字节字符字符串转换为 `pwcs` 指向的数组。 |
| | | `mbtowc` | `int mbtowc(wchar_t *pwc, const char *str, size_t n);` | 检查参数 `str` 指向的多字节字符。 |
| | | `qsort` | `void qsort(void *base, size_t nitems, size_t size, int (*compar)(const void *, const void *));` | 排序数组。 |
| | | `rand` | `int rand(void);` | 返回 0 到 `RAND_MAX` 之间的伪随机数。 |
| | | `realloc` | `void *realloc(void *ptr, size_t size);` | 尝试调整之前通过 `malloc` 或 `calloc` 分配的 `ptr` 指向的内存块的大小。 |
| | | `srand` | `void srand(unsigned int seed);` | 此函数为 `rand` 函数使用的随机数生成器设置种子。 |
| | | `strtod` | `double strtod(const char *str, char **endptr);` | 将参数 `str` 指向的字符串转换为浮点数。 |
| | | `strtol` | `long strtol(const char *str, char **endptr, int base);` | 将参数 `str` 指向的字符串转换为长整数（long int）。 |
| | | `strtoul` | `unsigned long strtoul(const char *str, char **endptr, int base);` | 将参数 `str` 指向的字符串转换为无符号长整数（unsigned long int）。 |
| | | `system` | `int system(const char *string);` | 将 `string` 指定命令传递给主机环境由命令处理器执行。 |
| | | `wcstombs` | `size_t wcstombs(char *str, const wchar_t *pwcs, size_t n);` | 将数组 `pwcs` 中存储的编码转换为多字节字符并存储在字符串 `str` 中。 |
| | | `wctomb` | `int wctomb(char *str, wchar_t wchar);` | 检查由参数 `wchar` 给定的宽字符对应的多字节字符编码。 |
| 11. | `string.h` | `memchr` | `void *memchr(const void *str, int c, size_t n);` | 在参数 `str` 指向字符串的前 `n` 个字节中查找字符 `c`（无符号字符）的首次出现。 |
| | | `memcmp` | `int memcmp(const void *str1, const void *str2, size_t n);` | 比较 `str1` 和 `str2` 的前 `n` 个字节。遇到空字符后不停止（始终检查 `n` 个字符）。 |
| | | `memcpy` | `void *memcpy(void *str1, const void *str2, size_t n);` | 从 `str2` 拷贝 `n` 个字符到 `str1`。如果 `str1` 和 `str2` 重叠，则行为未定义。 |
| | | `memmove` | `void *memmove(void *str1, const void *str2, size_t n);` | 从 `str2` 拷贝 `n` 个字符到 `str1`。处理重叠内存。 |
| | | `memset` | `void *memset(void *str, int c, size_t n);` | 将字符 `c`（无符号字符）拷贝到 `str` 的前 `n` 个字符。 |
| | | `strcat` | `char *strcat(char *str1, const char *str2);` | 将 `str2` 指向的字符串附加到 `str1` 指向字符串的末尾。 |
| | | `strncat` | `char *strncat(char *str1, const char *str2, size_t n);` | 在 `str1` 的末尾最多附加 `n` 个字符。 |
| | | `strchr` | `char *strchr(const char *str, int c);` | 在 `str` 指向的字符串中查找字符 `c`（无符号字符）的首次出现。 |
| | | `strcmp` | `int strcmp(const char *str1, const char *str2);` | 比较 `str1` 指向的字符串和 `str2` 指向的字符串。 |
| | | `strncmp` | `int strncmp(const char *str1, const char *str2, size_t n);` | 比较 `str1` 和 `str2` 最多 `n` 个字节。遇到空字符停止。 |
| | | `strcpy` | `char *strcpy(char *str1, const char *str2);` | 将 `str2` 指向的字符串拷贝到 `str1`。 |
| | | `strncpy` | `char *strncpy(char *str1, const char *str2, size_t n);` | 将 `str2` 指向的字符串最多 `n` 个字符拷贝到 `str1`。 |
| | | `strcspn` | `size_t strcspn(const char *str1, const char *str2);` | 找到 `str1` 中不包含 `str2` 中任何字符的第一个序列的长度。 |
| | | `strlen` | `size_t strlen(const char *str);` | 计算不包含终止空字符的字符串长度。 |
| | | `strpbrk` | `char *strpbrk(const char *str1, const char *str2);` | 找到 `str1` 中匹配 `str2` 中任何字符的第一个字符。 |
| | | `strrchr` | `char *strrchr(const char *str, int c);` | 在 `str` 指向的字符串中查找字符 `c`（无符号字符）的最后出现。空字符被视为字符串的一部分。 |
| | | `strspn` | `size_t strspn(const char *str1, const char *str2);` | 找到 `str1` 中包含 `str2` 中任何字符的第一个序列的长度。 |
| | | `strstr` | `char *strstr(const char *str1, const char *str2);` | 在 `str1` 中找到整个字符串 `str2`（不包括空字符）的首次出现。 |
| | | `strtok` | `char *strtok(char *str1, const char *str2);` | 将字符串拆分为一系列标记。 |
| | | `strxfrm` | `size_t strxfrm(char *str1, const char *str2, size_t n);` | 转换字符串 `str2` 并将结果放入 `str1`。 |
| | | `strerror` | `char *strerror(int err);` | 在内部数组中查找错误号 `err` 并返回错误消息字符串指针。 |
| 12. | `time.h` | `asctime` | `char *asctime(const struct tm *timeptr);` | 返回表示结构体日期和时间的字符串指针。 |
| | | `clock` | `clock_t clock(void);` | 返回自实现定义时代（通常是程序开始）以来的处理器时钟时间。 |
| | | `ctime` | `char *ctime(const time_t *timer);` | 返回根据参数 `timer` 表示的本地时间字符串。 |
| | | `difftime` | `double difftime(time_t time1, time_t time2);` | 计算 `time1` 和 `time2` 之间的秒差（`time1-time2`）。返回秒数。 |
| | | `gmtime` | `struct tm *gmtime(const time_t *timer);` | 将 `timer` 的值分解为结构 `tm` 并以协调时（UTC，也称为格林尼治标准时间 GMT）表示。 |
| | | `localtime` | `struct tm *localtime(const time_t *timer);` | 将 `timer` 的值分解为结构并在本地区域表示。 |
| | | `mktime` | `time_t mktime(struct tm *timeptr);` | 将 `timeptr` 指向的结构根据本地区域转换为 `time_t` 值。 |
| | | `strftime` | `size_t strftime(char *str, size_t maxsize, const char *format, struct tm *timeptr);` | 根据 `format` 中定义的格式规则对结构 `timeptr` 表示的时间进行格式化并存入 `str`。存入 `str` 的字符不超过 `maxsize`（包括终止空字符）。 |
| | | `time` | `time_t time(time_t *timer);` | 计算当前日历时间并编码为 `time_t` 格式。 |

# 关于本书

多年来，我们对 C 语言一直处于爱恨交织的感情。我们热爱编写 C 程序的便利性。我们热爱当今 C 编译器构建的开发环境。但我们厌恨那种犯错的容易。我们厌恨 C 编程通常对细节的极致关注。最重要的是，我们厌恨许多程序员设计其他语言的方式。事实是：C 是终极编程语言（也没有其他语言如此）。然而，这是一门每位软件开发者都应该熟悉的语言。无论好坏，它已成为计算机世界的*通用语言*（lingua franca）。本书试图让这门通用语言更贴近我们这些计算机专业人士。

前一本书《C语言编程》曾作为某门课程的主教材。具有高级语言的编程经验会有帮助，但对于精通计算机的读者来说并非必须。由于本书内容自成体系，既可以用于参考也可以用于学习，因此对于学习数据结构、编译器设计、操作系统、计算机图形或其他使用 C 作为编程语言的课程的学生来说，它是极佳的伙伴。由于书中包含了大量的程序、练习题和实践，对于自学 C 语言的读者也会有用。

# 本书涵盖的主题

- 算法流程图
- C 历史
- 标记符、关键字
- 变量、静态、类
- 数据类型
- 运算符、结合、关联
- 隐式类型、版本推断
- 显式转换
- 控制语句
- 标准复合运算符、循环
- 预处理器指令、宏
- 字符串、输入输出说明符
- 函数调用类型、递归
- 数组、多维数组
- 指针、地址、指针表达式
- 算术指针与函数
- 动态内存分配
- 结构体、联合体
- 文件管理
- 输入输出
- 命令行

# 关于作者

Sakshi Kadam 博士是一位工程毕业生。他从服务工程师开始职业生涯，加入 MCA（计算机应用硕士）和 IT 行业担任研究员。他通过嵌入式系统高级文凭（PGDES）专注于嵌入式系统。随后他进入学术界追求研究兴趣。他在计算机应用领域完成了博士研究。他发明了一种名为 C（概念建模语言）的新型计算机语言，专为教育设计。在学术界，他也紧密参与业界，参加针对行业专业人士的国家研讨会和工作坊，并作为大学教师教授从嵌入式系统到超级计算机的各种主题。他在全印度范围内承担咨询和教学任务。他是领先计算机杂志和出版物的定期投稿作者。目前，他在 Sinhgad 计算机应用学院（SITCA）担任院长。

Gaur (Ranhavi) Maden 女士目前担任马哈拉哈特拉邦普纳 MIT-WAI 学院 MCA（科学）和 MCA（商业）课程的讲师。她曾担任 2009-10 学年 MCA（商业）课程的负责人，并任职于普纳辛比奥斯国际大学辛比奥斯信息技术中心 MCA-IT 课程的教师。

作为研究生，她加入了纳西克的 K Waught College，担任 B.Sc.（计算机）全职讲师。自2008年以来，她一直担任 MCA（科学）、MCA（商业）、MCA（信息技术）和 M.Sc.（计算机科学）等研究生课程的全职讲师。

她的兴趣领域包括移动与无线通信、数据通信与网络操作、下一代网络、客户端/服务器计算以及互联网编程。她已获得普纳大学的认证。

![](img/42571661744bb1de16ed6abc45190753_243_0.png)

www.himpub.com

ISBN: 978-93-5693-715-4 ESM 0354
