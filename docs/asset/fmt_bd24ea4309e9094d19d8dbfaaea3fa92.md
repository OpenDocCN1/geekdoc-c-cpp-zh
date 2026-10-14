
我们将如何指定我们想要访问特定数据文件？ 理论上，每次想要从中读取或写入时都可以提及文件的名称是可能的。 但这种方法会有一些缺点。 相反，通常的做法（也是 C 的 `stdio` 库采用的方法）是你在打开文件时只提及一次文件名。 此后，您使用一些小标记，在本例中，文件指针来跟踪（对您和库而言）您所讨论的是哪个文件。 每当您想要从正在处理的文件之一读取或写入时，您都会通过使用其文件指针来标识该文件（即您在打开文件时获得的文件指针）。 正如我们将看到的，您将文件指针存储在变量中，就像您存储处理的任何其他数据一样，因此只要您使用不同的变量来存储文件指针，就有可能打开多个文件。

您声明一个变量来存储文件指针，如下所示：

```
FILE *fp;
```

类型 `FILE` 由 `<stdio.h>` 为您预定义。 它是一个数据结构，标准 I/O 库需要它来为您跟踪文件。 出于历史原因，您声明一个变量，该变量是指向此 `FILE` 类型的指针。 变量的名称可以（像任何变量一样）是您选择的任何名称； 使用字母 `fp` 作为变量名是传统的（因为我们谈论的是文件指针）。 如果您同时从两个文件读取，您可能会使用两个文件指针：

```
FILE *fp1, *fp2;
```

如果您从一个文件读取并写入另一个文件，您可能会声明一个输入文件指针和一个输出文件指针：

```
FILE *ifp, *ofp;
```

像任何指针变量一样，文件指针在初始化为指向某物之前是没有用的。 （实际上，任何类型的变量在初始化之前都不是很有用。）要实际打开文件并接收您将存储在文件指针变量中的“标记”，请调用 `fopen`。 `fopen` 接受一个文件名（作为字符串）和一个模式值，表示您是否打算读取或写入此文件。 （模式变量也是一个字符串。）要打开 `input.dat` 进行读取，您可能会调用

```
ifp = fopen("input.dat", "r");
```

模式字符串 `"r"` 表示读取。 模式 `"w"` 表示写入，因此我们可以像这样打开 `output.dat` 进行输出：

```
ofp = fopen("output.dat", "w");
```

模式字符串的其他值使用频率较低。 第三个主要模式是 `"a"` 用于追加。 （如果您使用 `"w"` 写入已存在的文件，其旧内容将被丢弃。）您还可以在模式字符串中添加 `"+"` 字符以表示您想要同时读取和写入，或添加 `"b"` 字符以表示您想要执行“二进制”（而不是文本）I/O。

打开文件时需要注意的一件事是，这是一个可能失败的操作。 请求的文件可能不存在，或者它可能受到读取或写入保护。 （这些可能性应该很明显，但很容易忘记它们。）`fopen` 如果无法打开请求的文件，则返回空指针，并且在继续使用 `fopen` 的返回值作为文件指针之前检查这种情况非常重要。 每次调用 `fopen` 通常都会跟随一个测试，如下所示：

```
ifp = fopen("input.dat", "r");
if(ifp == NULL)
{
printf("can't open file\n");
exit or return
}
```

如果 `fopen` 返回空指针，并且您将其存储在文件指针变量中并继续尝试使用它进行 I/O，您的程序通常会崩溃。 通常将对 `fopen` 的调用和赋值与测试合并：

```
if((ifp = fopen("input.dat", "r")) == NULL)
{
printf("can't open file\n");
exit or return
```

如果你不习惯这些“紧凑”测试，你不必编写它们，但你会在其他人的代码中看到它们，所以你应该能够阅读它们。

### 自测问题

- 1. `FILE` 类型在头文件 ________ 中预定义。

- 2. 我们可以在 `fopen` 函数的模式字符串中添加一个“+”字符，以表示我们想要同时读写。(对/错)

### 13.3 关闭文件

虽然你可以打开多个文件，但同时打开的文件数量是有限制的。如果你的程序将连续打开许多文件，你需要在每个文件用完后关闭它；否则标准 I/O 库可能会耗尽用于跟踪打开文件的资源。关闭文件只需以文件指针为参数调用 `fclose`：

```
fclose(fp);
```

调用 `fclose` 可以确保（如果文件是以输出模式打开的）任何最后的缓冲输出最终被写入文件，并且操作系统（和 C 库）用于该文件的资源被释放。如果你忘记关闭文件，它会在程序退出时自动关闭。

### 自测问题

- 3. 关闭文件只需以 __________ 为参数调用 `fclose`。

- 4. 如果你忘记关闭文件，它会在程序退出时自动关闭。(对/错)

### 13.4 文件输入/输出操作

目前我们使用过的每个 I/O 库函数都有一个配套函数，它接受一个额外的文件指针参数，告诉它从哪里读取或写入。`printf` 的配套函数是 `fprintf`，文件指针参数位于最前面。要向我们在上一节中打开的 `output.dat` 文件打印一个字符串，我们可以调用

```
fprintf(ofp, "Hello, world!\n");
```

`getchar` 的配套函数是 `getc`，文件指针是它唯一的参数。要从我们在上一节中打开的 `input.dat` 文件中读取一个字符，我们可以调用

```
int c;
c = getc(ifp);
```

`putchar` 的配套函数是 `putc`，文件指针参数放在最后。要向 `output.dat` 写入一个字符，我们可以调用

```
putc(c, ofp);
```

我们自己的 `getline` 函数调用 `getchar`，因此总是读取标准输入。我们可以编写一个配套的 `fgetline` 函数，它从任意文件指针读取：

```
#include <stdio.h>
```

/* 从 `fp` 读取一行，*/

/* 将其复制到 `line` 数组（但不超过 `max` 字符）。*/

/* 不在 `line` 数组中放置终止的 `\n`。*/

/* 返回行长度，空行返回 0，文件结束返回 `EOF`。*/

```
int fgetline(FILE *fp, char line[], int max)
{
int nch = 0;
int c;
max = max - 1; /* leave room for '\0' */

while((c = getc(fp)) != EOF)
{
if(c == '\n')
break;
```

```
if(nch < max)
{
line[nch] = c;
nch = nch + 1;
}
if(c == EOF && nch == 0) return EOF;

line[nch] = '\0';
return nch;
}
```

现在我们可以通过以下调用从 `ifp` 读取一行：

```
char line[MAXLINE];

...

fgetline(ifp, line, MAXLINE);
```

#### 程序 13.1：向文件写入数据

```
#include <stdio.h>
main()
{
FILE *fp;
char stuff[25];
int index;
fp = fopen("TENLINES.TXT","w"); /* open for writing */
strcpy(stuff,"This is an example line.");
for (index = 1; index <= 10; index++)
fprintf(fp,"%s Line number %d\n", stuff, index);
```

```
fclose(fp); /* close the file before ending program */
}
```

#### 13.4.1 预定义流

除了通过调用 `fopen` 显式打开的文件指针外，还有三个预定义流。`stdin` 是标准输入对应的常量文件指针，`stdout` 是标准输出对应的常量文件指针。这两个可以在任何需要文件指针的地方使用；例如，`getchar()` 等同于 `getc(stdin)`，`putchar(c)` 等同于 `putc(c, stdout)`。第三个预定义流是 `stderr`。与 `stdout` 一样，`stderr` 默认通常连接到屏幕。区别在于，当标准输出被重定向时，`stderr` 不会被重定向。例如，在 Unix 或 MS-DOS 下，当你执行

```
program > filename
```

任何打印到 `stdout` 的内容都会被重定向到文件 `filename`，但任何打印到 `stderr` 的内容仍然会输出到屏幕。`stderr` 背后的意图是它是“标准错误输出”；打印到其中的错误消息不会消失在输出文件中。例如，当文件无法打开时，更实际的打印错误消息的方式是

```
if((ifp = fopen(filename, "r")) == NULL)
{
    fprintf(stderr, "can't open file %s\n", filename);
    exit or return
}
```

其中 `filename` 是一个字符串变量，指示要打开的文件名。错误消息不仅打印到 `stderr`，而且更信息丰富，因为它提到了无法打开的文件名。

#### 程序 13.2：读取数据文件 input.dat

假设你有一个由数字的行和列组成的数据文件：

```
1 2 34

5 6 78

9 10 112
```

假设你想把这些数字读入一个数组。（实际上，该数组将是一个数组的数组，或“多维”数组；）我们可以通过组合几个部分来编写代码：我们刚才展示的 `fgetline` 函数，以及将每一行拆分成单词的 `getwords` 函数。假设数据文件名为 `input.dat`，代码将如下所示：

```
#define MAXLINE 100
#define MAXROWS 10
#define MAXCOLS 10
```

```
int array[MAXROWS][MAXCOLS]; char *filename = "input.dat"; FILE *ifp;
char line[MAXLINE];
char *words[MAXCOLS];
int nrows = 0;
int n; int i;
```

```
ifp = fopen(filename, "r");
if(ifp == NULL)
{
fprintf(stderr,"can't open %s\n", filename); exit(EXIT_FAILURE);
}
```

```c
while(fgetline(ifp, line, MAXLINE) != EOF) {

if(nrows >= MAXROWS)

{
    fprintf(stderr, "too many rows\n");
    exit(EXIT_FAILURE);
}

n = getwords(line, words, MAXCOLS);

for(i = 0;i < n;i++)
    array[nrows][i] = atoi(words[i]);

nrows++;
}
```

循环每执行一次，就使用 `fgetsline` 从文件中读取一行。每一行使用 `getwords` 拆分成“单词”；每个“单词”实际上是一个数字。然而，这些数字仍表示为字符串，因此在存储到数组之前，每个数字通过调用 `atoi` 转换为 `int`。代码检查两种不同的错误条件（无法打开输入文件，以及输入文件行数过多），如果发生其中一种情况，它会打印错误消息并退出。`exit` 函数是一个标准库函数，用于终止程序。它在 `<stdlib.h>` 中声明，接受一个参数，即程序的退出状态。`EXIT_FAILURE` 是一个代码，也由 `<stdlib.h>` 定义，表示程序失败。成功用 `EXIT_SUCCESS` 或简单的 `0` 表示。（这些值也可以从 `main()` 返回；以特定状态值调用 `exit` 本质上等同于从 `main()` 返回相同的状态值。）

### 自测问题

- 5. `putchar` 的配套函数是 `put`，并且文件指针参数位于最前面。(对/错)

- 6. 除了通过调用 `fopen` 显式打开的文件指针外，还有 __________ 个预定义流。

- 7. `getchar()` 与 `getc(stdin)` 相同。(对/错)

### 13.5 I/O 操作中的错误处理

标准 I/O 函数为每个打开的流维护两个指示器，以显示流的文件结束和错误状态。这些可以通过以下函数查询和设置：

```
#include <stdio.h>
void clearerr(FILE *stream);
int feof(FILE *stream);
int ferror(FILE *stream);
void perror(const char *s);
```

`clearerr` 清除流的错误和 EOF 指示器。

如果流的 EOF 指示器被设置，`feof` 返回非零值，否则返回零。如果流的错误指示器被设置，`ferror` 返回非零值，否则返回零。

`perror` 在程序的标准输出上打印一行错误消息，前缀为 `s` 指向的字符串，并附加一个冒号和一个空格。错误消息由 `errno` 的值决定，旨在对导致错误的条件给出一些解释。例如，下面的程序产生所示的错误消息：

```
#include <stdio.h>
```

```
#include <stdlib.h>
main(){
fclose(stdout);
if(fgetc(stdout) >= 0){
fprintf(stderr, "What - no error!\n");
exit(EXIT_FAILURE);
}
perror("fgetc");
exit(EXIT_SUCCESS); }
/* Result */
fgetc: Bad file number
```

### Self Assessment Questions

8._______ 清除流的错误和 EOF 指示符。

9._______ 如果流的错误指示符已设置则返回非零，否则返回零。

### 13.6 文件的随机访问

所有文件 I/O 例程的工作方式都相同；除非用户采取明确步骤更改文件位置指示器，否则文件将按顺序读取和写入。读取后跟写入后跟读取（如果文件以允许这种方式打开）将导致第二次读取从刚刚写入的数据末尾立即开始。（请记住，stdio 要求用户在读-写-读循环的每个元素之间插入缓冲区刷新操作。）

为控制此行为，随机访问函数允许控制文件中的隐含读写位置。文件位置指示器可以在无需读取或写入的情况下移动，并指示下一次对文件操作的字节。

存在三种类型的函数允许检查或更改文件位置指示器。它们的声明和描述如下。 
```
#include <stdio.h>
/* return file position indicator */
long ftell(FILE *stream);
int fgetpos(FILE *stream, fpos_t *pos);
/* set file position indicator to zero */
void rewind(FILE *stream);
/* set file position indicator */
int fseek(FILE *stream, long offset, int ptrname);
int fsetpos(FILE *stream, const fpos_t *pos);
```

**`ftell`** 如果 `stream` 引用的是二进制文件，则返回文件位置指示器的当前值（以字符为单位）。对于文本文件，返回一个‘magic’数字，该数字只能在后续对 **`fseek`** 的调用中用于重新定位到当前文件位置指示器。失败时返回 `-1L` 并设置 **`errno`**。

**`rewind`** 将 `stream` 指示的文件的当前文件位置指示器设置为文件开头。通过调用 `rewind` 重置文件错误指示符。不返回任何值。

**`fseek`** 允许将 `stream` 的文件位置指示器设置为任意值（对于二进制文件），或对于文本文件，仅设置为从 `ftell` 获得的位置，如下所示：

一般情况下，文件位置指示器被设置为距由 `ptrname` 值确定的文件中的某一点 `offset` 字节（字符）。

`Offset` 可以为负。`ptrname` 的值可以是 `SEEK_SET`，将文件位置指示器相对于文件开头设置，`SEEK_CUR`，将文件位置指示器相对于其当前值设置，以及 `SEEK_END`，将文件位置指示器相对于文件末尾设置。后者不一定保证在二进制流上正常工作。

对于文本文件，`offset` 必须为零或从同一流先前对 `ftell` 的调用返回的值，且 `ptrname` 的值必须为 `SEEK_SET`。

`fseek` 清除给定流的末尾文件指示符并擦除任何 `ungetc` 的记忆。它适用于输入和输出。

成功时返回零，禁止请求时返回非零。

请注意，对于 `ftell` 和 `fseek`，必须能够将文件位置指示器的值编码为 `long`。对于非常长的文件，这可能无法工作，因此标准引入了 `fgetpos` 和 `fsetpos`，它们以消除该问题的方式指定。

`fgetpos` 将 `stream` 的当前文件位置指示器存储在 `pos` 指向的对象中。存储的值是‘magic’，仅用于使用 `fsetpos` 返回到同一流的指定位置。

`fsetpos` 按上文所述工作，同时清除流的末尾文件指示符并忘记任何 `ungetc` 操作的影响。

对于这两个函数，成功时返回零；失败时返回非零并设置 `errno`。

### Self Assessment Questions

10._________ 函数如果 `stream` 引用的是二进制文件，则返回文件位置指示器的当前值（以字符为单位）。

11.`fseek` 允许将 `stream` 的文件位置指示器设置为任意值。 （True/False）

12._________ 将 `stream` 的当前文件位置指示器存储在 `pos` 指向的对象中。

### 13.7 命令行参数

我们多次提到，如果程序每次运行都做完全相同的事情，那么它很少有用。向程序提供一些可变输入的另一种方式是通过命令行参数调用它。它是在调用程序时提供给程序的参数。

（我们应该承认命令行用户界面有点老式，目前有点不受欢迎。如果你使用过 Unix 或 MSDOS，你知道什么是命令行，但如果你使用的是 Macintosh 或 Microsoft Windows 或其他图形用户界面，可能从未见过命令行。事实上，如果你在 Mac 或 Windows 上学习 C，给程序提供命令行可能很棘手。
