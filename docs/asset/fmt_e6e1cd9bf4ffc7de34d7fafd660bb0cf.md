
列表 17.10 中的 `main()` 看起来很熟悉。它与列表 17.9 中的 `main()` 几乎相同，仅第 14 行不同。该函数没有使用 `rename()`，而是使用了 `copy()`。由于 C 没有复制函数，第 24 行到 60 行创建了一个复制函数。第 31 行和 32 行以二进制读取模式打开源文件 `fold`。第 36 行到 40 行以二进制写入模式打开目标文件 `fnew`。注意，如果打开目标文件出错，第 38 行会关闭源文件。第 46 行到 54 行的 `while` 循环执行文件的实际复制。第 48 行从源文件 `fold` 获取一个字符。第 50 行检查是否读取到了文件结束标记。如果已到达文件末尾，则执行 `break` 语句退出 `while` 循环。如果未到达文件末尾，则将字符写入目标文件 `fnew`。第 56 行和 57 行在返回 `main()` 之前关闭了两个文件。

# 使用临时文件

## 输入

列表 17.11 `tempfilemaker.c`-- 使用 `tmpnam()` 创建临时文件名

```
1: // tempfilemaker.c-- 临时文件名的演示。
2:
3: #include <stdio.h>
4:
5: int main(void )
6: {
7:     char buffer[10], *c;
8:
9:     // 在定义的缓冲区中获取一个临时名称。
10:
11:     tmpnam(buffer);
12:
13:     /* 获取另一个名称，这次是在函数的
14:        内部缓冲区中。 */
15:
16:     c = tmpnam(NULL);
17:
18:     // 显示这些名称。
19:
20:     printf("Temporary name 1: %s", buffer);
21:     printf("\nTemporary name 2: %s\n", c);
22:
23:     return 0;
24:
25: }
```

## 输出

Temporary name 1: us.

Temporary name 2: us.

> 你在系统中创建的临时名称可能与这些不同。

## 分析

此程序仅生成并打印临时名称；它并没有实际创建任何文件。第 11 行将临时名称存储在字符数组 `buffer` 中。第 16 行将字符指针赋值给 `tmpnam()` 返回的名称的变量 `c`。你的程序必须使用生成的名称来打开临时文件，并在程序执行终止之前将其删除。下面的代码片段说明了这一点：

# 452 课程 17 使用磁盘文件

```
char tempename[80];
*tmpfile;
tmpnam(tempename);
tmpfile = fopen(tempename, "w"); /* 使用适当的模式 */
close(tmpfile);
remove(tempename);
```

| 应当 (DO) | 不要 (DON'T) |
|---|---|
| 记得删除你创建的临时文件。它们不会被自动删除。 | 不要删除你可能还需要需要的文件。 |

### 总结

在本节中，你学习了 C 程序使用磁盘文件。C 将磁盘文件视为流（字符序列），就像你在第 14 节学习的预定义流一样。与磁盘文件关联流在使用之前必须打开，在使用后必须关闭。磁盘文件流可以以文本模式或二进制模式打开。

打开磁盘文件后，你可以从文件中读取数据到程序中，从程序向文件中写入数据，或者两者兼之。有三种类型的文件 I/O：格式化、字符和直接。每种类型的 I/O 都最适用于特定类型的数据存储和检索任务。

每个磁盘文件都有一个关联的位置指示器。该指示器指定文件中的位置（以从文件开始的字节数计算），随后的读取和写入操作将发生在此。对于某些类型的文件访问，位置指示器会自动更新，你不需要担心它。对于随机文件访问，C 标准提供了用于操纵位置指示器的函数。

最后，C 提供了一些基础的文件管理函数，允许你删除和重命名磁盘文件。在本节中，你自己编写了一个用于复制磁盘文件的函数。

### 问答

- 在使用 `remove()`、`rename()`、`fopen()` 和其他文件函数时，可以使用带路径的文件名吗？

- 你可以使用带有路径和驱动器的完整文件名，也可以只使用文件名。如果你只使用文件名，函数将在当前目录中查找。记住，在使用反斜杠 (`\`) 时，需要使用转义序列。还要记住 UNIX 使用正斜杠 (`/`) 作为目录分隔符。

# 我可以读取文件末尾之后吗？

可以。你也可以读取文件开头之前。这种读取的结果可能是灾难性的。读取文件就像处理数组一样。你正在查看内存中的偏移量。如果你使用 `fseek()`，你应该检查并确保没有超出文件末尾。

# 如果我不关闭文件会发生什么？

良好的编程习惯是关闭你打开的任何文件。默认情况下，文件在程序退出时应该关闭；但你不应该依赖这一点。如果文件没有关闭，你可能无法再次访问它，因为操作系统会认为该文件正在使用中。

# 我可以同时打开多少个文件？

这个问题无法用一个数字来回答。打开文件数量的限制取决于你操作系统的变量。更多信息请参阅你的操作系统手册。

# 我可以使用随机访问函数顺序读取文件吗？

在顺序读取文件时，不需要使用像 `fseek()` 这样的函数。因为文件指针被留在最后占据的位置，对于顺序读取来说，它始终位于你想要的位置。你可以使用 `fseek()` 顺序读取文件；但你从中没有任何获处。

### 工作坊

工作坊提供了测试题，帮助你巩固对所涵盖材料的理解，并提供了练习让你获得使用所学知识的。

### 测验

- 1. 文本模式流和二进制模式流之间的区别是什么？
- 2. 程序读取磁盘文件必须做什么？
- 3. 打开文件时，你必须提供什么信息？
- 4. 三种文件 I/O 类型是什么？
- 5. 如何检测文件结束？
- 6. `EOF` 的值是多少？
- 7. `strlen()` 的返回类型是什么？
- 8. 如何删除文件？
- 9. 文件的位置指示器是什么？
- 10. 如何重命名磁盘文件？

### 练习

- 1. 编写一个确定字符串长度的程序。
- 2. 编写一个打开文件并统计字符数的程序。
- 3. 找到以下代码中的错误：

```
FILE *fp;
int c;

if ( fp = fopen(,"r") == NULL )
    return -1;

while (( c = fgetc(fp)) != EOF )
    fprintf(stdout, "%c", c);

close(fp);
```

- 4. 编写一个显示字符串长度的程序。
- 5. 编写一个用指定模式打开文件的程序。
- 6. 编写一个将小写字母转换为大写字母并保持其他字符不变的程序。
- 7. 编写一个打开文件、按 128 字节块读取它、并以十六进制和 ASCII 格式显示内容的程序。
- 8. 编写一个打开临时文件并在程序终止时将其删除的程序。（提示：使用 `atexit()`。）

# 课程 18

操纵字符串

C 存储在字符串中的文本数据是许多程序的重要部分。到目前为止，你已经学习了 C 如何存储字符串以及你如何输入和输出字符串。C 还提供了许多其他用于字符串操作的函数。在本节中，你将学习：

- 如何确定字符串的长度
- 如何复制和合并字符串
- 比较字符串的函数
- 如何搜索字符串
- 如何转换字符串
- 如何测试字符

## 输出

输入一行文本，按空行以退出。

我是钢铁侠！

```
该行有 14 个字符。
输入一行文本，按空行以退出。
```

## 分析

此程序的作用仅演示了 `strlen()` 的用法。第 13 行和第 14 行显示了一条消息并获取了一个名为 `buf` 的字符串。第 16 行使用 `strlen()` 将 `buf` 的长度赋值给变量 `length`。第 18 行通过检查长度是否为 0 来判断该字符串是否为空。如果字符串不为空，第 19 行打印字符串的大小。

# 复制字符串

C 库有两个用于复制字符串的函数。由于 C 处理字符串的方式，你不能像其他计算机语言那样简单地将一个字符串赋值给另一个。你必须将源字符串从它的位置复制到目标字符串的内存位置。字符串复制函数是 `strcpy()` 和 `strncpy()`。这些函数需要 `string.h` 头文件。

## strcpy() 函数

库函数 `strcpy()` 将整个字符串复制到另一个内存位置。它的原型如下：

```c
char *strcpy(char *destination, const char *source);
```

函数 `strcpy()` 将 `source` 指向的字符串（包括终止空字符 `\0`）复制到 `destination` 指向的位置。返回值是指向新字符串 `destination` 的指针。

在使用 `strcpy()` 时，你必须先为目标字符串分配存储空间。该函数无法得知 `destination` 指向的是已分配的空间。如果没有分配空间，该函数将从 `destination` 开始覆盖 `strlen(source)` 字节的内存。这可能会导致不可预测的问题。列表 18.2 示例了 `strcpy()` 的用法。

# 第 18 节 操纵字符串

注意

当程序使用 `malloc()` 分配内存时（如列表 18.2 所示），良好的编程习惯要求在程序结束使用该内存时使用 `free()` 函数释放内存。你将在第 21 节“处理内存”中学习到 `free()`。

## 输入

列表 18.2 `stringcopy.c`：在使用 `strcpy()` 之前，你必须为目标字符串分配存储空间

```c
1: // stringcopy.c--演示 strcpy()。
2: #include <stdlib.h>
3: #include <stdio.h>
4: #include <string.h>
5: 
6: char source[] = "The source string."
7: 
8: int main( void )
9: {
10: char dest1[80];
11: char *dest2, *dest3;
12: 
13: printf("\source: %s", source );
14: 
15: // 复制到 dest1 是可以，因为 dest1 指向
16: // 80 字节已分配的空间。
17: 
18: strcpy(dest1, source);
19: printf("\ndest1: %s", dest1);
20: 
21: // 复制 dest2 必须分配空间。
22: 
23: dest2 = (char *)malloc(strlen(source) +1);
24: strcpy(dest2, source);
25: printf("\ndest2: %s\n", dest2);
26: 
27: // 在不分配目标空间的情况下复制是不允许的。
28: // 以下可能导致严重问题。
29: 
30: // strcpy(dest3, source);
31: return(0);
32: }
```

## 输出

source: The source string.

dest1: The source string.

dest2: The source string.

## 分析

此程序演示了将字符串复制到字符数组（如第 10 行声明的 `dest1`）以及到字符指针（如第 11 行与 `dest3` 一起声明的 `dest2`）。第 13 行打印原始源字符串。随后在第 18 行使用 `strcpy()` 将该字符串复制到 `dest1`。第 24 行将 `source` 复制到 `dest2`。打印 `dest1` 和 `dest2` 以显示函数执行成功。注意第 23 行使用 `malloc()` 函数为 `dest2` 分配了适当的空间。如果你将字符串复制到一个尚未分配内存的字符指针，你将得到不可预测的结果。

# strncpy() 函数

`strncpy` 函数与 `strcpy()` 类似，不同在于 `strncpy` 允许你指定复制多少个字符。它的原型是：

```c
char *strncpy(char *destination, const char *source, size_t n);
```

参数 `destination` 和 `source` 是指向目标字符串和源字符串的指针。函数将 `source` 的前 `n` 个字符复制到 `destination`。如果 `source` 短于 `n`，则会在 `source` 末尾添加空字符，使得共复制 `n` 个字符到 `destination`。如果 `source` 长于 `n`，则不添加终止的 `\0`。函数的返回值为 `destination`。列表 18.3 演示了 `strncpy()` 的用法。

## 输入

列表 18.3 `strcpy2.c`：`strncpy()` 函数

```c
/* strcpy2.c-使用 strncpy() 函数。 */
2: #include <stdio.h>
3: #include <string.h>
5: char dest[] = "";
7: char source[] = "abcdefghijklmnopqrstuvwxyz";
9: int main(void )
10:
11:   size_t n;
12:
13:   while (1)
14:   {
15:       puts("Enter the number of characters to copy (1-26)");
16:       scanf("%d", &n);
17:       if (n > 0 && n < 27)
18:           break;
19:   }
20:   printf("\nBefore strncpy = %s", dest);
21:   strncpy(dest, source, n);
22:   printf("\nAfter strncpy = %s\n", dest);
23: return(0);
```

## 输出

Enter the number of characters to copy (1-26)

Before strncpy = 

After strncpy = abcdefghijklmnopqrstuvwxyz

## 分析

`strncpy` 函数演示了将字符串复制到字符数组 `dest`。第 20 行打印 `dest` 在复制前的值。第 13 行的 `while` 循环允许用户输入有效的数字。第 16 行使用 `scanf` 获取 `n`。第 17 行检查 `n` 是否在 1 到 26 之间。第 24 行使用 `strncpy()` 将 `source` 的前 `n` 个字符复制到 `dest`。第 22 行打印复制后的 `dest`。注意，如果 `n` 等于字符串长度，`strncpy` 不会添加终止 `\0`。

string。你必须为 `str` 分配足够的空间来存储生成的字符串。该函数返回指向 `str` 的指针。列表 18.5 使用 `strcat()` 生成与列表 18.4 相同的输出。

### 输入

列表 18.5 `stringcat2.c`：使用 `strcat()` 函数拼接字符串

```c
1: // stringcat2.c--The strcat() function.
2:
3: #include <stdio.h>
4: #include <string.h>
5:
6: char str2[] = "abcdefghijklmnopqrstuvwxyz";
7:
8: int main(void )
9: {
10:    char str[27];
11:    int n;
12:
13:    for (n=1; n< 27; n++)
14:    {
15:        strcpy(str, "");
16:        strcat(str, str2, n);
17:        puts(str);
18:    }
19:
20:    return 0;
21: }
```

### 输出

a

ab

abc

abcd

abcde

ababcdef

ababcdefg

ababcdefgh

ababcdefghi

ababcdefghij

ababcdefghijk

ababcdefghijkl

ababcdefghijklij

ababcdefghijklm

ababcdefghijklklmn

ababcdefghijklmno

ababcdefghijklmnop

ababcdefghijklklmnopq

ababcdefghijklmmnopqr

abcdefghijklmnopqr

ababcdefghijklmnopqrt

ababcdefghijklmnopstu

ababcdefghijklmnopqrstuv

ababcdefghijklmnopqrstuvw

ababcdefghijklmnopqrstuvwx

ababcdefghijklmnopqrstxy

ababcdefghijklmnopqrstuvwxyz

## 课程 18 字符串操作

### 分析

你可能会好奇第 15 行 `strcpy(str1, "");` 的用途。这一行复制了一个包含单个空字符的空字符串。结果是 `str1` 中的该字符——`str1[0]` 被设置为 0（空字符）。语句 `str1[0] = 0;` 或 `str1[0] = '\0';` 也可以实现的功能。

### 比较字符串

对字符串进行比较是为了判断它们是否相等。如果不相等，则其中一个字符串比另一个“大于”或“小于”。“大于”和“小于”的判定是根据字符的 ASCII 码进行的。对于字母，这等同于字母顺序，但有一个奇怪的例外：所有大写字母都“小于”由 97–122 表示的小写字母 a–z。因此，通过这些 C 函数评估时，“ZEBRA”会被认为小于“apple”。

ANSI C 库包含了两种类型的字符串比较函数：比较两个字符串以及比较两个字符串中特定数量的字符。

### 比较两个完整字符串
