

# 第 17 节 使用磁盘文件

## 输出

输入要显示的文本文件名称：
hello.c
#include <stdio.h>
int main( void )
{
  printf("Hello, world.");
  return(0);
}

## 分析

该程序中的 while 循环（第 25 行到 29 行）是用于[执行]顺序处理的更复杂程序中典型的 while 循环。只要没有到达文件末尾，while 语句中的代码（第 27 行和第 28 行）就会重复执行。当调用 eof() 并返回非零值时，循环结束，文件关闭，程序结束。

## 文件管理函数

文件管理术语是指对现有文件进行处理——而不是从它们读取或向它们写入——包括删除、重命名和复制文件。C 标准库包含了用于删除和重命名文件的函数，你也可以编写自己的文件复制程序。

## 删除文件

要删除一个文件，请使用库函数 remove()。它的原型定义在 stdio.h 中，如下：

```
int remove( const char *filename);
```

变量 *filename* 是指向要删除的文件名称的指针。（参见本节较早之前的“使用文件名”部分）。指定的文件不能处于打开状态。如果文件存在，则会被删除，remove() 返回 0。如果文件不存在、文件是只读的、你没有足够的访问权限，或者发生了其他错误，remove() 返回 -1。

列表 17.8 展示了 remove() 的用法。要小心：如果你 remove() 删除了一个文件，它将永远消失。

## 输入

列表 17.8 filedelete.c：使用 remove() 函数删除磁盘文件

```
1: // filedelete.c--演示 remove() 函数的使用。
2:
3:#include <stdio.h>
4:
5: int main(void )
6: {
7:     char filename[80];
8:
9:     printf("Enter the filename to delete: ");
10:    gets(filename);
11: "
```

| 要做 | 不要做 |
|---|---|
| 使用 rewind() 或 fseek(fp, SEEK_SET, 0 ) 将文件位置重置为文件开头。 | 不要读取文件末尾之后或文件之前的内容。通过检查你的位置来避免这一点。 |
| 在处理二进制文件时使用 feof() 检查文件末尾。 | 不要对二进制文件使用 EOF。 |

```
12: if ( remove(filename) == 0)
13:     printf("The file %s has been deleted.\n", filename);
14: else
15:     fprintf(stderr, "Error deleting the file %s.\n", filename);
16:     return(0);
17: }
```

## 输出

输入要删除的文件名：*.bak
删除文件 *.bak 错误。
输入要删除的文件名：list1414.bak
文件 list1414.bak 已删除。

## 分析

该程序在第 9 行提示用户要删除的文件名。第 12 行调用 remove() 删除输入的文件。如果返回值为 0，则文件被删除，并显示说明此事实的消息。如果返回值不为 0，则发生了错误，文件未被删除。

> 验证用户是否真的想要删除一个文件始终是一个好主意。

## 重命名文件

rename() 函数更改现有磁盘文件的名称。该函数原型在 stdio.h 中如下：

```
int rename(const char *oldname, const char *newname);
```

oldname 和 newname 指向的文件名遵循本节之前给出的规则。唯一的限制是名称必须指向同一个磁盘驱动；函数 rename() 成功时返回 0，发生错误时返回 -1。错误可能由以下条件（包括限于）引起：

- * 文件 oldname 不存在。
- 已经存在一个名为 newname 的文件。
- 你尝试重命名到另一个磁盘。

列表 17.9 展示了 rename() 的用法。

## 输入

列表 17.9 filenamer.c：使用 rename() 更改磁盘文件的名称

```
1: /* 使用 rename() 更改文件名。 */
2:
3: #include <stdio.h>
4:
5: int main(void)
6: {
7:     char oldname[80], newname[80];
8:
9:     printf("Enter current filename: %s");
10:    gets(oldname);
11:    printf("Enter new name for file: %s");
12:    gets(newname);
13:
14:    if ( rename(oldname, newname) == 0 )
15:        printf("%s has been renamed %s.\n", oldname, newname);
16:    else
17:        fprintf(stderr, "An error has occurred renaming %s.\n", oldname);
18:    return(0);
19: }
```

## 输出

输入当前文件名：**My first file**
输入文件新名称：**SuperNewFile.txt**
My first file 已重命名为 SuperNewFile.txt。

## 分析

列表 17.9 显示了 C 语言有多强大。仅用 18 行代码，该程序就替换了系统调用，并且是一个友好的函数。第 9 行提示要重命名的文件名。第 11 行提示新文件名。rename() 调用被封装在第 14 行的 if 语句中，确保文件的重命名执行。如果是，第 15 行打印确认消息；否则，第 17 行打印错误消息。

## 复制文件

经常需要制作文件的副本——一个具有不同名称（或相同名称但在不同驱动器或目录中）的文件。在 Windows 中，你通过复制文件并粘贴到新目录来实现。在 C 中如何复制文件？没有库函数，所以你需要自己写。

这听起来可能有点复杂，但由于 C 使用了输入输出流，它非常简单。步骤如下：

- 以二进制模式打开源文件。（使用二进制模式确保函数可以复制所有类型的文件，而不只是文本文件。）
- 以二进制模式打开目标文件。
- 从源文件中读取一个字符。记住，当打开文件时，指针位于文件开头，因此不需要设置位置。
- 如果 eof() 表示已到达文件末尾，你已完成，可以关闭两个文件。
- 如果未到达文件末尾，将字符写入目标文件，并返回步骤 3。

列表 17.10 包含一个函数 copy_file()，它接收源文件目标文件名并按上述步骤执行复制操作。如果打开文件出错，函数不会尝试复制操作并向调用程序返回 -1。复制操作完成后，程序关闭两个文件并返回 0。

## 输入

列表 17.10 copier.c：复制文件的函数

```
1: // copier.c--复制文件。
2:
3: #include <stdio.h>
4:
5: int file_copy(char *oldname, char *newname)
6: {
7:     FILE *fold, *fnew;
8:     int c;
9:
10:     /* 以二进制模式打开源文件。 */
11:     if ( fold = fopen(oldname, "rb") == NULL )
12:         return -1;
13:
14:     /* 以二进制模式打开目标文件。 */
15:
16:     if ( fnew = fopen(newname, "wb") == NULL )
17:     {
18:         fclose(fold );
19:         return -1;
20:     }
21:     /* 从源每次读取一个字节；如果未到达文件
22:     末尾，将字节写入目标文件。 */
23:
24:     while (1)
25:     {
26:         c = fgetc( fold );
27:
28:         if ( eof(fold ))
29:             fputc(c, fnew);
30:         else
31:             break;
32:     }
33:     fclose( fnew );
34:     fclose( fold );
35:
36:     return 0;
37: }
```

## 输出

输入源文件：list1710.c
输入目标文件：tmpfile.c
复制操作成功

## 分析

copy_file() 函数工作非常完美，让你从一个小文本文件复制到一个巨大的程序文件。然而，它也有局限性。如果目标文件已存在，函数会在不询问的情况下将其删除。对你很好的编程练习是修改 copy_file() 以检查目标文件是否存在，然后询问用户是否覆盖旧文件。

列表 17.10 中的 main() 看起来很熟悉。它与列表 17.9 中的 main() 几乎相同，仅第 14 行不同。该函数没有使用 rename()，而是使用了 copy()。由于 C 没有复制函数，第 24 行到 60 行创建了一个复制函数。第 31 行和 32 行以二进制读取模式打开源文件 fold。第 36 行到 40 行以二进制写入模式打开目标文件 fnew。注意，如果打开目标文件出错，第 38 行会关闭源文件。第 46 行到 54 行的 while 循环执行文件的实际复制。第 48 行从源文件 fold 获取一个字符。第 50 行检查是否读取到了文件结束标记。如果已到达文件末尾，则执行 break 语句退出 while 循环。如果未到达文件末尾，则将字符写入目标文件 fnew。第 56 行和 57 行在返回 main() 之前关闭了两个文件。

