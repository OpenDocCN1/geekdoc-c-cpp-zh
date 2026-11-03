
## 输出格式化函数

```c
int fprintf( FILE *stream, const char *format, ... )
```

fprintf() 函数在格式说明符的控制下将输出转换并写入指定的文件流。它返回写入的字符数，如果发生错误则返回负值。

```c
int printf( const char *format, ... )
```

printf() 函数将输出写入并转换到 stdout。它等价于 fprintf( stdout, format, ... )。

```c
int sprintf( char *s, const char *format, ... )
```

sprintf() 函数与 printf() 相同，只是输出写入指定的字符串并以 \0 空字符终止。

```c
vprintf( const char *format, va_list arg )
vfprintf( FILE *stream, const char *format, va_list arg )
vsprintf( char *s, const char *format, va_list arg )
```

这三个函数等价于相应的 printf() 函数，只是其可变参数列表被 va_list 类型的参数取代。有关更多详细信息，请参阅第 180 页的 stdarg.h 头文件函数。

## 输入格式化函数

```c
int fscanf( FILE *stream, const char *format, ... )
```

fscanf() 函数在格式说明符的控制下从指定流读取，并将转换后的值赋给后续参数。它返回转换的输入项数，如果到达文件末尾或发生错误则返回 EOF 常量。

```c
int scanf( const char *format, ... )
```

scanf() 函数从 stdin 读取并转换输入。它等价于 fscanf( stdin, format, ... )。

```c
int sscanf( char *s, const char *format, ... )
```

sscanf() 函数与 scanf() 相同，只是输入从指定的字符串读取。

## 输出格式说明符

在 C 语言中，% 前缀表示格式说明符。下面列出了所有 printf() 格式说明符，以及第 168 页的 scanf() 说明符。

| Character | printf() converts to |
|---|---|
| d, i | int 数据类型，有符号十进制 |
| o | int 数据类型，无前导零的无符号八进制 |
| x, X | int 数据类型，无符号十六进制。0x 使用小写，例如 0xff，0X 使用大写，例如 0XFF |
| u | int 数据类型，无符号十进制 |
| c | int 单个字符，转换后为 char 数据类型 |
| s | char 指向字符串的指针，以 \0 空字符结束 |
| f | double 数据类型，形式为 xxx.yyyyy，小数点后数字位数由精度设置。默认精度为 6 位 |
| e, E | double 数据类型，形式为 xx.yyyyyye±zz 或 xx.yyyyyyE±zz，小数点后数字位数由精度设置。默认精度为 6 位 |
| g, G | double 数据类型，按 %e 或 %E 转换或 %f 转换输出，以较短者为准 |
| p | 指针的内存地址 |
| n | 不是转换，而是将 printf() 函数调用迄今为止写入的字符数存储在 int 指针参数中 |
| % | 不是转换；打印一个 % |

## 字符输入输出函数

**int fgetc( FILE *stream )**

返回指定流的下一个字符作为 char，如果到达文件末尾或发生错误则返回 EOF 常量。

**char *fgets( char *s , int n , FILE *stream )**

从指定流读取下一个 n-1 个字符到 s，然后在数组末尾添加 \0 空字符。此函数返回 s，如果到达文件末尾或发生错误则返回 NULL。

**int fputc( int c , FILE *stream )**

将字符 c 写入指定流并返回写入的字符，如果发生错误则返回 EOF。

**int fputs( const char *s , FILE *stream )**

将字符串 s 写入指定流并返回非负值，如果发生错误则返回 EOF。

**int getc( FILE *stream )**

getc() 函数是 fgetc() 的宏等价物。

**int getchar( void )**

getchar() 函数等价于 getc( stdin )。

**char *gets( char *s )**

读取下一行输入到数组中，用 \0 空字符替换其最后的换行符。它返回 s，如果到达文件末尾或发生错误则返回 NULL。

**int putc( int c , FILE *stream )**

putc() 函数是 fputc() 的宏等价物。

**int putchar( int c )**

putchar() 函数等价于 putc( c , stdout )。

**int puts( const char *s )**

将字符串 s 和换行符写入 stdout。它返回非负值，如果发生错误则返回 EOF。

**int ungetc( int c , FILE *stream )**

将字符 c 推回指定流，在下一次读取时返回。每个流保证只有一个推回字符，且不能推回 EOF。此函数返回推回的字符，如果发生错误则返回 EOF。

## 直接流输入输出函数

stdio.h 头文件中的 fread() 和 fwrite() 函数最适合读取和写入整个文本文件：

```c
size_t fread( void *ptr , size_t size , size_t nobj , FILE *stream )
```

fread() 函数从指定流读取最多 nobj 个大小为 size 的对象到 ptr 指向的数组中。此函数返回已读取的对象数，可能少于函数调用中请求的数量。

可以使用 feof() 和 ferror() 函数在 fread() 执行过程中测试其状态——请参阅对面页列出的错误函数。

```c
size_t fwrite(const void *ptr, size_t size, size_t nobj, FILE *stream)
```

fwrite() 函数将 ptr 指向的数组中的 nobj 个大小为 size 的对象写入指定流。它返回已写入的对象数。如果发生错误，返回的值将小于函数调用中 nobj 请求的数量。

## 错误函数

C 库中的许多标准函数在发生错误或到达文件末尾时设置状态指示器。这些指示器可以使用下表中列出的错误函数进行测试。此外，在 errno.h 头文件中定义的整数表达式 errno 可能包含错误代码，提供有关最近错误的更多信息。

| Function | Description |
|---|---|
| `void clearerr( FILE *stream )` | clearerr() 函数清除指定流的文件结束和错误指示器。 |
| `int feof( FILE *stream )` | feof() 函数如果指定流的文件结束指示器已设置则返回非零值。 |
| `int ferror( FILE *stream )` | ferror() 函数如果指定流的错误指示器已设置则返回非零值。 |
| `void perror( const char *s )` | perror() 函数打印与 errno 表达式中包含的整数值相关联的实现定义错误消息。另请参阅 string.h 头文件中的 strerror() 函数。 |

文件流是通过逐个移动其包含的字符来处理的。下表中列出的函数可用于操作文件流中的位置：

| Function | Description |
|---|---|
| `int fseek(FILE *stream , long offset , int original )` | fseek() 函数设置指定流中的文件位置。后续的读取或写入从新位置开始。新位置通过指定位置相对于其原始位置的偏移量来确定。可选地，此函数的第三个参数可以指定为 SEEK_SET（开头）、SEEK_CUR（当前位置）或 SEEK_END（文件末尾）。对于文本流，偏移量必须为零或由 ftell() 函数返回的值，且原始位置指定为 SEEK_SET。fseek() 函数如果发生错误则返回非零值。 |
| `long ftell(FILE *stream )` | ftell() 函数返回指定流的当前文件位置，如果发生错误则返回 -1。 |
| `int fgetpos(FILE *stream , fpos_t *ptr )` | fgetpos() 函数将指定流的当前文件位置记录在指定的 ptr 指针中，作为特殊的 fpos_t 类型。此函数如果发生错误则返回非零值。 |
| `int fsetpos(FILE *stream , const fpos_t *ptr )` | fsetpos() 函数将指定流中的文件指针定位到 ptr 指针中由 fgetpos() 记录的位置。此函数如果发生错误则返回非零值。 |

