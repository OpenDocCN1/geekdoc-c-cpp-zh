

# 常见 C 函数

| 函数 | 头文件 | 函数原型 |
| --- | --- | --- |
| fseek* | stdio.h | int fseek(FILE *, long, int); |
| fsetpos* | stdio.h | int fsetpos(FILE *, const fpos_t *); |
| ftell* | stdio.h | long ftell(FILE *); |
| fwrite* | stdio.h | size_t fwrite(const void *, size_t, size_t, FILE *); |
| getc* | stdio.h | int getc(FILE *); |
| getch* | stdio.h | int getch(void); |
| getchar* | stdio.h | int getchar(void); |
| getche* | stdio.h | int getche(void); |
| getenv* | stdlib.h | char *getenv(const char *); |
| gets* | stdio.h | char *gets(char *); |
| gmtime* | time.h | struct tm *gmtime(const time_t *); |
| isalnum* | ctype.h | int isalnum(int); |
| isalpha* | ctype.h | int isalpha(int); |
| isascii* | ctype.h | int isascii(int); |
| iscntrl* | ctype.h | int iscntrl(int); |
| isdigit* | ctype.h | int isdigit(int); |
| isgraph* | ctype.h | int isgraph(int); |
| islower* | ctype.h | int islower(int); |
| isprint* | ctype.h | int isprint(int); |
| ispunct* | ctype.h | int ispunct(int); |
| isspace* | ctype.h | int isspace(int); |
| isupper* | ctype.h | int isupper(int); |
| isxdigit* | ctype.h | int isxdigit(int); |
| labs | stdlib.h | long int labs(long int); |
| ldexp | math.h | double ldexp(double, int); |
| ldiv | stdlib.h | long int ldiv(long int, long int); |
| localtime* | time.h | struct tm *localtime(const time_t *); |
| log* | math.h | double log(double); |
| log10* | math.h | double log10(double); |
| malloc* | stdlib.h | void *malloc(size_t); |
| mblen | stdlib.h | int mblen(const char *, size_t); |
| mbstowcs* | stdlib.h | size_t mbstowcs(wchar_t *, const char *, size_t); |
| mbtowc* | stdio.h | int mbtowc(wchar_t *, const char *, size_t); |

# 附录 C

| 函数 | 头文件 | 函数原型 |
| --- | --- | --- |
| memchr | string.h | void *memchr(const void *, int, size_t); |
| memcmp | string.h | int memcmp(const void *, const void *, size_t); |
| memcpy | string.h | void *memcpy(void *, const void *, size_t); |
| memmove | string.h | void *memmove(void *, const void *, size_t); |
| memset | string.h | void *memset(void *, int, size_t); |
| mktime* | time.h | time_t mktime(struct tm *); |
| modf | math.h | double modf(double, double *); |
| perror* | stdio.h | void perror(const char *); |
| pow* | math.h | double pow(double, double); |
| printf* | stdio.h | int printf(const char *, ...); |
| putc* | stdio.h | int putc(int, FILE *); |
| putchar* | stdio.h | int putchar(int); |
| puts* | stdio.h | int puts(const char *); |
| qsort* | stdlib.h | void qsort(void*, size_t, size_t, int (*)(const void *, const void *)); |
| rand | stdlib.h | int rand(void); |
| realloc* | stdlib.h | void *realloc(void *, size_t); |
| remove* | stdio.h | int remove(const char *); |
| rename* | stdio.h | int rename(const char *, const char *); |
| rewind* | stdio.h | void rewind(FILE *); |
| scanf* | stdio.h | int scanf(const char *, ...); |
| setbuf | stdio.h | void setbuf(FILE *, char *); |
| setvbuf* | stdio.h | int setvbuf(FILE *, char *, int, size_t); |
| sin* | math.h | double sin(double); |
| sinh* | math.h | double sinh(double); |
| sleep* | time.h | unsigned int sleep(unsigned int); |
| sprintf* | stdio.h | int sprintf(char *, const char *, ...); |
| sqrt* | math.h | double sqrt(double); |
| srand | stdlib.h | void srand(unsigned int); |
| strcat* | string.h | char *strcat(char *, const char *); |
| strchr* | string.h | char *strchr(const char *, int); |
| strcmp* | string.h | int strcmp(const char *, const char *); |

# 常见 C 函数

| 函数 | 头文件 | 函数原型 |
| --- | --- | --- |
| strcmp | string.h | int strcmp(const char *, const char *); |
| strcpy | string.h | char *strcpy(char *, const char *); |
| strncpy | string.h | char *strncpy(char *, const char *, size_t); |
| strdup | string.h | char *strdup(const char *); |
| strerror | string.h | char *strerror(int); |
| strftime | time.h | size_t strftime(char *, size_t, const char *, const struct tm *); |
| strlen | string.h | size_t strlen(const char *); |
| strlwr | string.h | char *strlwr(char *); |
| strncat | string.h | char *strncat(char *, const char *, size_t); |
| strncmp | string.h | int strncmp(const char *, const char *, size_t); |
| strncpy | string.h | char *strncpy(char *, const char *, size_t); |
| strnset | string.h | char *strnset(char *, int, size_t); |
| strpbrk | string.h | char *strpbrk(const char *, const char *); |
| strchr | string.h | char *strchr(const char *, int); |
| strspn | string.h | size_t strspn(const char *, const char *); |
| strstr | string.h | char *strstr(const char *, const char *); |
| strtod | stdlib.h | double strtod(const char *, char **); |
| strtok | string.h | char *strtok(char *, const char *); |
| strtol | stdlib.h | long strtol(const char *, char **, int); |
| strtoul | stdlib.h | unsigned long strtoul(const char *, char **, int); |
| strupr | string.h | char *strupr(char *); |
| system | stdlib.h | int system(const char *); |
| tan | math.h | double tan(double); |
| tanh | math.h | double tanh(double); |
| time | time.h | time_t time(time_t *); |
| tmpfile | stdio.h | FILE *tmpfile(void); |
| tmpnam | stdio.h | char *tmpnam(char *); |
| tolower | ctype.h | int tolower(int); |
| toupper | ctype.h | int toupper(int); |

# 附录 C

| 函数 | 头文件 | 函数原型 |
| --- | --- | --- |
| ungetc* | stdio.h | int ungetc(int, FILE *); |
| va_arg* | stdarg.h | type va_arg(va_list, type); |
| va_end* | stdarg.h | void va_end(va_list); |
| va_start* | stdarg.h | void va_start(va_list, lastarg); |
| vprintf | stdio.h | int vprintf(const char *, va_list); |
| vsprintf | stdio.h | int vsprintf(char *, const char *, va_list); |
| wcstombs | stdlib.h | size_t wcstombs(char *, const wchar_t *, size_t); |
| wctomb | stdlib.h | int wctomb(char *, wchar_t); |

# 附录 D

# 答案

## 第 1 课的答案

### 测验

- 1. C 强大、流行且可移植。
- 2. 编译器将源代码翻译成计算机可以理解的机器语言指令。
- 3. 编辑、编译、链接和测试。
- 4. 这个问题的答案取决于你的编译器。请查阅编译器的手册。
- 5. 这个问题的答案取决于你的编译器。请查阅编译器的手册。
- 6. C 源文件的适当扩展名为 .C 或 .c。
  注意：C++ 使用扩展名 .CPP。你可以用 .CPP 扩展名编写和编译 C 程序，但使用 .c 扩展名更为合适。
- 7. FILENAME.TXT 可以编译。但是，使用 .c 扩展名更为合适。
- 8. 你应该修改源代码以纠正问题。你应该重新编译和重新链接。重新链接后，你应该再次运行程序以查看你的修正是否修复了程序。
- 9. 机器语言由计算机可以理解的数字或二进制指令组成。因为计算机无法理解 C 源代码，所以编译器将源代码翻译为机器代码，也称为目标代码。
- 10. 链接器将程序的目标代码与函数库的目标代码合并并创建可执行文件。

# 练习

- 1. 当你查看目标文件时，你会看到许多不寻常的字符和其他乱码。混杂在乱码中，你还会看到源文件的一部分。

- 2. 这个程序计算圆的面积。它提示用户输入半径然后显示面积。

- 3. 这个程序生成一个由字符 x 组成的 10x10 块。类似的程序在第 6 课“基本程序控制”中介绍。

- 4. 这个程序会生成编译错误。你应该会收到类似以下的消息：

```
Error: chlex4.c: Declaration terminated incorrectly
```

这个错误是由第 3 行末尾的分号引起的。如果删除分号，这个程序应该可以正确编译和链接。

- 5. 这个程序可以正常编译，但会出现链接错误。你应该会收到类似以下的消息：
Error: Undefined symbol _do_it in module...

这个错误发生是因为链接器找不到名为 do_it 的函数。要修复这个程序，将 do_it 改为 printf。

- 6. 与打印由字符 x 填充的 10x10 块不同，程序打印的是一个 10x10 的笑脸块。

## 第 2 课的答案

### 测验

- 1. 一个块。

- 2. main() 函数。

- 3. 你使用程序注释来对程序的结构和操作进行说明。/* 和 */ 之间的任何文本都是程序注释，会被编译器忽略。此外，你还可以使用单行注释。同一行中 // 之后的所有文本都被视为注释。

- 4. 函数是执行特定任务并被赋予名称的独立程序代码段。通过使用函数名，程序可以执行函数中的代码。

- 5. 用户定义的函数由程序员创建。库函数随 C 编译器提供。

