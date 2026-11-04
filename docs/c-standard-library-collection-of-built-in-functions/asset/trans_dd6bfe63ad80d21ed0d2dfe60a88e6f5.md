

| 修饰符 | 描述 |
|---|---|
| h | 参数被解释为 short int 或 unsigned short int（仅适用于整数说明符：i、d、o、u、x 和 X）。 |
| l | 对于整数说明符（i、d、o、u、x 和 X），参数被解释为 long int 或 unsigned long int；对于说明符 c 和 s，参数被解释为宽字符或宽字符串。 |
| L | 参数被解释为 long double（仅适用于浮点说明符：e、E、f、g 和 G）。 |

- **arg** -- 表示可变参数列表的对象。这应由 <stdarg> 中定义的 va_start 宏初始化。

## 返回值

如果成功，则返回写入的总字符数，否则返回负数。

## 示例

以下示例演示了 vprintf() 函数的用法。

```c
#include <stdio.h>
#include <stdarg.h>

void WriteFrmtd(char *format, ...)
{
    va_list args;

    va_start(args, format);
    vprintf(format, args);
    va_end(args);
}

int main ()
{
    WriteFrmtd("%d variable argument\n", 1);
    WriteFrmtd("%d variable %s\n", 2, "arguments");

    return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```
1 variable argument
2 variable arguments
```

## int vsprintf(char *str, const char *format, va_list arg)

### 描述

C 库函数 int vsprintf(char *str, const char *format, va_list arg) 使用传递给它的参数列表将格式化输出发送到字符串。

### 声明

以下是 vsprintf() 函数的声明。

```c
int vsprintf(char *str, const char *format, va_list arg)
```

### 参数

- str -- 这是 char 元素数组，结果字符串将存储在其中。
- format -- 这是 C 字符串，包含要写入 str 的文本。它可以选择包含内嵌格式标签，这些标签会被后续附加参数中指定的值替换，并按要求格式化。格式标签原型：%[flags][width][.precision][length]specifier，如下所述：

| 说明符 | 输出 |
|---|---|
| c | 字符 |
| d 或 i | 有符号十进制整数 |
| e | 使用 e 字符的科学计数法（尾数/指数） |
| E | 使用 E 字符的科学计数法（尾数/指数） |
| f | 十进制浮点数 |
| g | 使用 %e 或 %f 中较短者 |
| G | 使用 %E 或 %f 中较短者 |
| o | 有符号八进制 |
| s | 字符串 |
| u | 无符号十进制整数 |
| x | 无符号十六进制整数 |
| X | 无符号十六进制整数（大写字母） |
| p | 指针地址 |
| n | 不打印任何内容 |
| % | 字符 |

| 标志 | 描述 |
|---|---|
| - | 在给定字段宽度内左对齐；默认右对齐（参见 width 子说明符）。 |
| + | 强制在结果前加上正号或负号（+ 或 -），即使对于正数也是如此。默认情况下，只有负数前会加上负号。 |
| (空格) | 如果不会写入任何符号，则在值前插入一个空格。 |
| # | 与 o、x 或 X 说明符一起使用时，对于不等于零的值，值前会分别加上 0、0x 或 0X。与 e、E 和 f 一起使用时，它强制写入的输出包含小数点，即使后面没有数字。默认情况下，如果后面没有数字，则不写入小数点。与 g 或 G 一起使用时，结果与 e 或 E 相同，但不会删除末尾的零。 |
| 0 | 在指定填充时（参见 width 子说明符），用零（0）而不是空格左填充数字。 |
| width | 描述 |

### 返回值

如果成功，则返回写入的总字符数，否则返回负数。

### 示例

以下示例演示了 vsprintf() 函数的用法。

```c
#include <stdio.h>
#include <stdarg.h>

char buffer[80];
int vspfunc(char *format, ...)
{
   va_list aptr;
   int ret;

   va_start(aptr, format);
   ret = vsprintf(buffer, format, aptr);
   va_end(aptr);

   return(ret);
}

int main()
{
   int i = 5;
   float f = 27.0;
   char str[50] = "tutorialspoint.com";

   vspfunc("%d %f %s", i, f, str);
   printf("%s\n", buffer);

   return(0);
}
```

让我们编译并运行上述程序，这将产生以下结果：

## int fscanf(FILE *stream, const char *format, ...)

### 描述

C 库函数 int fscanf(FILE *stream, const char *format, ...) 从流中读取格式化输入。

### 声明

以下是 fscanf() 函数的声明。

```c
int fscanf(FILE *stream, const char *format, ...)
```

### 参数

- **stream** -- 这是指向 FILE 对象的指针，该对象标识流。
- **format** -- 这是 C 字符串，包含以下一项或多项：空白字符、非空白字符和格式说明符。格式说明符将如下所示：[= %[*][width][modifiers]type=]，其说明如下：

| 参数 | 描述 |
|---|---|
| * | 这是一个可选的起始星号，表示要从流中读取数据但忽略它，即不将其存储到对应参数中。 |
| width | 指定当前读取操作中要读取的最大字符数。 |
| modifiers | 为对应附加参数所指向的数据指定与 int（对于 d、i 和 n）、unsigned int（对于 o、u 和 x）或 float（对于 e、f 和 g）不同的大小：h：short int（对于 d、i 和 n），或 unsigned short int（对于 o、u 和 x）；l：long int（对于 d、i 和 n），或 unsigned long int（对于 o、u 和 x），或 double（对于 e、f 和 g）；L：long double（对于 e、f 和 g） |
| type | 指定要读取的数据类型以及期望如何读取的字符。参见下表。 |

### fscanf 类型说明符：

| 类型 | 限定输入 | 参数类型 |
|---|---|---|
| c | 单个字符：读取下一个字符。如果指定了不同于 1 的宽度，函数将读取 width 个字符并将它们存储在作为参数传递的数组的连续位置中。末尾不会追加空字符。 | char * |
| d | 十进制整数：可选地以 + 或 - 符号开头的数字 | int * |
| e、E、f、g、G | 浮点数：包含小数点的十进制数，可选地以 + 或 - 符号开头，并可选地后跟 e 或 E 字符和十进制数。有效条目的两个示例是 -732.103 和 7.12e4 | float * |
| o | 八进制整数： | int * |
| s | 字符串。这将读取后续字符，直到找到空白字符（空白字符被视为空格、换行和制表符）。 | char * |
| u | 无符号十进制整数。 | unsigned int * |
| x、X | 十六进制整数 | int * |

- **附加参数** -- 根据格式字符串，函数可能期望一系列附加参数，每个参数包含一个值，用于替换格式参数中指定的每个 % 标签（如果有）。这些参数的数量应与期望值的 % 标签数量相同。

### 返回值

该函数返回成功匹配并赋值的输入项数，该数量可能少于提供的数量，或者在早期匹配失败时甚至为零。

### 示例

以下示例演示了 fscanf() 函数的用法。

```c
#include <stdio.h>
#include <stdlib.h>

int main()
{
   char str1[10], str2[10], str3[10];
   int year;
   FILE * fp;

   fp = fopen ("file.txt", "w+");
   fputs("We are in 2012", fp);

   rewind(fp);
   fscanf(fp, "%s %s %s %d", str1, str2, str3, &year);

   printf("Read String1 |%s|\n", str1 );
   printf("Read String2 |%s|\n", str2 );
   printf("Read String3 |%s|\n", str3 );
   printf("Read Integer |%d|\n", year );

   fclose(fp);

   return(0);
}
```

让我们编译并运行上述程序，它将产生以下结果：

```text
Read String1 |We|
Read String2 |are|
Read String3 |in|
Read Integer |2012|
```

## int scanf(const char *format, ...)

### 描述

C 库函数 **int scanf(const char *format, ...)** 从 stdin 读取格式化输入。

