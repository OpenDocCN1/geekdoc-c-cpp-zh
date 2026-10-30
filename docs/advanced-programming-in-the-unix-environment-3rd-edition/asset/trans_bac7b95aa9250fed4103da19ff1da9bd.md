

文本文件和二进制文件。 由于 UNIX 内核并不区分这些类型的文件，指定类型中的字符 b 没有任何效果。

使用 fdopen 时，type 参数的含义略有不同。 描述符已经打开，因此写入时不会截断文件。 （例如，如果描述符是由 open 函数创建的，并且文件已存在，则 O_TRUNC 标志将控制文件是否被截断。 fdopen 函数不能简单地截断它打开以进行写入的任何文件。）此外，标准 I/O 追加模式不能创建文件（因为如果描述符引用它，则文件必须存在）。

当文件以追加类型打开时，每次写入都将在当时的文件末尾进行。 如果多个进程以标准 I/O 追加模式打开同一文件，每个进程的数据都将正确写入文件。

Berkeley 在 4.4BSD 之前版本的 fopen 以及 Kernighan 和 Ritchie [1988] 第 177 页所示的简单版本无法正确处理追加模式。 这些版本在打开流时会执行 lseek 到文件末尾。 为了在涉及多个进程时正确支持追加模式，必须使用 O_APPEND 标志打开文件，我们在第 3.3 节中讨论过它。 在每次写入之前执行 lseek 也行不通，正如我们在第 3.11 节中所讨论的那样。

当文件以读写方式打开（类型中的加号）时，适用两个限制。

+   - 输出不能在没有 intervening fflush、fseek、fsetpos 或 rewind 的情况下直接跟随输入。
+   - 输入不能在没有 intervening fseek、fsetpos 或 rewind 的情况下直接跟随输出，或在遇到文件末尾的输入操作。

我们可以将图 5.2 中的打开流的六种方式总结在图 5.3 中。

| Restriction | r | w | a | r+ | w+ | a+ |
|---|---|---|---|---|---|---|
| file must already exist | • |  |  | • |  |  |
| previous contents of file discarded |  | • |  |  | • |  |
| stream can be read | • |  |  | • | • | • |
| stream can be written |  | • | • | • | • | • |
| stream can be written only at end |  |  | • |  |  | • |

Figure 5.3 Six ways to open a standard I/O stream

请注意，如果通过指定类型为 w 或 a 来创建新文件，我们无法指定文件的访问权限位，就像我们在第 3 章中使用 open 函数和 creat 函数时所能做的那样。 POSIX.1 要求实现以以下权限位集创建文件：

S_IRUSR | S_IWUSR | S_IRGRP | S_IWGRP | S_IROTH | S_IWOTH

然而，正如我们在第 4.8 节中所回忆的那样，我们可以通过调整 umask 值来限制这些权限。

默认情况下，打开的流是完全缓冲的，除非它引用终端设备，在这种情况下它是行缓冲的。 在打开流后，但在对流执行任何其他操作之前，我们可以使用上一节中的 setbuf 或 setvbuf 函数根据需要更改缓冲。

通过调用 fclose 关闭打开的流。

```
#include <stdio.h>
int fclose(FILE *fp);

Returns: 0 if OK, EOF on error
```

在文件关闭之前，先刷新任何缓冲的输出数据。 任何可能缓冲的输入数据将被丢弃。 如果标准 I/O 库曾为流自动分配缓冲区，则该缓冲区将被释放。

当进程正常终止时，无论是通过直接调用 exit 函数还是从 main 函数返回，所有具有未写入缓冲数据的标准 I/O 流都会被刷新，并且所有打开的标准 I/O 流都会被关闭。

## 5.6 Reading and Writing a Stream

打开流后，我们可以选择三种非格式化 I/O：

+   1. 逐字符 I/O。 我们可以一次读写一个字符，标准 I/O 函数会处理所有缓冲，如果流是缓冲的。
+   2. 逐行 I/O。 如果我们想一次读写一行，我们使用 fgets 和 fputs。 每行以换行符终止，并且在调用 fgets 时我们必须指定可以处理的最高行长度。 我们在第 5.7 节中描述这两个函数。
+   3. 直接 I/O。 这种类型的 I/O 由 fread 和 fwrite 函数支持。 对于每次 I/O 操作，我们读取或写入一些对象，其中每个对象的大小是指定的。 这两个函数通常用于二进制文件，其中每次操作读取或写入一个结构。 我们在第 5.9 节中描述这两个函数。

> ISO C 标准中的直接 I/O 术语有许多名称：二进制 I/O、一次一个对象 I/O、记录导向 I/O 或结构导向 I/O。 不要将此功能与 FreeBSD 和 Linux 支持的 O_DIRECT 打开标志混淆——它们无关。

（我们将在第 5.11 节中描述格式化的 I/O 函数，例如 printf 和 scanf。）

### Input Functions

三个函数允许我们一次读取一个字符。

```
#include <stdio.h>
int getc(FILE *fp);
int fgetc(FILE *fp);
int getchar(void);

All three return: next character if OK, EOF on end of file or error
```

函数 getchar 定义为等价于 getc(stdin)。 getc 和 fgetc 之间的区别在于 getc 可以实现为宏，而 fgetc 不能实现为宏。 这意味着三件事。

+   1. getc 的参数不应是具有副作用的表达式，因为它可能被评估多次。
+   2. 由于 fgetc 保证是一个函数，我们可以获取其地址。 这使我们能够将 fgetc 的地址作为参数传递给另一个函数。
+   3. 调用 fgetc 可能比调用 getc 慢，因为通常调用函数需要更多时间。

这三个函数返回下一个字符作为 unsigned char 转换为 int。 指定 unsigned 的原因是如果设置了最高位，返回值就不会为负。 要求整数返回值的原因是所有可能的字符值都可以返回，以及指示发生错误或遇到文件末尾的指示。 <stdio.h> 中的常量 EOF 要求为负值。 其值通常为 −1。 这种表示还意味着我们不能将这三个函数的返回值存储在字符变量中，然后将该值与常量 EOF 进行比较。

请注意，这些函数在发生错误或到达文件末尾时返回相同的值。 为了区分两者，我们必须调用 ferror 或 feof。

```
#include <stdio.h>
int ferror(FILE *fp);
int feof(FILE *fp);

Both return: nonzero (true) if condition is true, 0 (false) otherwise

void clearerr(FILE *fp);
```

在大多数实现中，FILE 对象为每个流维护两个标志：

+   - 一个错误标志
+   - 一个文件结束标志

两个标志都可以通过调用 clearerr 来清除。
读取流后，我们可以通过调用 ungetc 来推回字符。

```
#include <stdio.h>
int ungetc(int c, FILE *fp);

Returns: c if OK, EOF on error
```

被推回的字符将以其被推回的相反顺序由流上的后续读取返回。 但是请注意，虽然 ISO C 允许实现支持任意数量的推回，但实现只需要提供一个字符的推回。 我们不应指望超过一个字符。

我们推回的字符不必与读取的字符相同。 我们无法推回 EOF。 然而，当我们到达文件末尾时，我们可以推回一个字符。 下一次读取将返回该字符，其后的读取将返回 EOF。 这是有效的，因为对 ungetc 的成功调用会清除流的文件结束指示。

推回通常用于我们读取输入流并将其分解为某种形式的单词或标记时。 有时我们需要查看下一个字符以确定如何处理当前字符。 然后很容易将我们查看的字符推回，以便下一次调用 getc 返回它。 如果标准 I/O 库不提供此推回功能，我们就必须将字符存储在自己的变量中，并附带一个标志，告诉我们在下一次需要字符时使用此字符而不是调用 getc。

> 当我们使用 ungetc 推回字符时，它们不会写回底层文件或设备。 相反，它们保存在标准 I/O 库为流的缓冲区核心中。

### Output Functions

有可用的输出函数对应于我们已经描述的每个输入函数。

```
#include <stdio.h>

int putc(int c, FILE *fp);
int fputc(int c, FILE *fp);
int putchar(int c);

All three return: c if OK, EOF on error
```

与输入函数一样，putchar(c) 等价于 putc(c, stdout)，并且 putc 可以实现为宏，而 fputc 不能实现为宏。

## 5.7 Line-at-a-Time I/O

逐行输入由两个函数提供，fgets 和 gets。

```
#include <stdio.h>

char *fgets(char *restrict buf, int n, FILE *restrict fp);
char *gets(char *buf);

Both return: buf if OK, NULL on end of file or error
```

