
- `"w"` 用于打开文件进行写入。写入后可以使用相同模式读取数据。

- `"r+"` 用于打开文件进行数据的读和写。

- `"a+"` 用于在文件末尾写入信息。写入后可以使用相同模式读取数据。

## 示例 CP-275

```c
FILE *fptr, *tfile;
fptr = fopen("STUDENT.DAT", "w");
tfile = fopen("TEXTINFO.TXT", "r");
```

注意：

- (i) 如果文件以 `"w"` 或 `"w+"` 模式打开文件，其内容将被自动擦除。但 `"w+"` 模式通过将指针移动到同一文件中之前的数据处，便于读取新输入的数据。当以 `"w"` 或 `"w+"` 模式创建文件时，文件指针始终被设置为文件开头。

- (ii) 当文件以 `"r"` 或 `"r+"` 模式打开时，文件指针始终位于文件开头。

- (iii) 当你尝试打开一个不存在的文件时，`fopen()` 函数将返回 `NULL`。

```c
例如，
fptr = fopen("STUDENT.DAT", "r");
if (fptr == NULL)
    printf("\n指定的文件不可用");
```

## `fclose()` 函数

`fclose()` 函数用于关闭活动状态的文件。它具有以下格式。

`fclose(fp);`

其中 `fp` 指代文件指针。

示例

```c
fclose(fptr);
fclose(tfile);
```

## 字符处理

### `getc()` 函数

`getc()` 函数用于从文件中读取一个字符。它具有以下格式。

`ch = getc(fp);`

其中 `ch` 指代字符类型变量

`fp` 指代文件指针

示例

```c
FILE *tfile;
char c;
c = getc(tfile);
```

注意从文件中读取的字符被赋值给字符变量 `c`。

CP-276 C语言编程

### `putc()` 函数

`putc()` 函数用于向文件写入一个字符。它具有以下形式。

```c
putc(ch, fp);
```

其中 `ch` 指代字符类型变量

`fp` 指代文件指针

## 示例

```c
FILE *tfile;
char c;
putc(c,tfile);
```

注意字符变量 `c` 的值被写入文件中。

> `getc()` 和 `putc()` 常用于访问文本文件。

## `feof()` 函数

`feof()` 函数用于在读取数据时定位文件末尾。它具有以下形式。

```c
feof(fp);
```

其中 `fp` 指代文件指针

当文件包含数据时，该函数返回 `0`；当到达文件末尾时返回非零整数。考虑此示例。

```c
FILE *fptr;
if(feof(fptr) == 0)
printf("\n文件中有可用数据");
else
printf("\n到达文件末尾");
```

## 整数处理

### `getw()` 函数

`getw()` 函数用于从文件中读取整数数据。它具有以下形式。

```c
n = getw(fp);
```

其中 `n` 指代整数变量

`fp` 指代文件指针

## 示例

```c
FILE *nptr;
int m;
m = getw(nptr);
```

### `putw()` 函数

`putw()` 函数用于向文件写入整数数据。它具有以下形式。

`putw(n, fp);`

其中 指代整数变量

`fp` 指代文件指针

## 示例

```c
FILE *nptr;
int m;
putw(m,nptr);
```

注意整数变量 `m` 的值被写入文件中。

## 示例 1

编写一个 C 程序创建一个文件。

## 答案

`getchar()` 函数用于从键盘读取一个字符并将其赋值给字符变量。

从键盘读取字符直到按下 Enter 键为止。此过程重复进行。

```c
/* 创建文件 */
#include <stdio.h>
#include <conio.h>
main() {
  char ch;
  FILE *fp;
  fp = fopen("SAMPLE.TXT", "w");
  while(1) {
    printf("输入字符（按回车停止）：");
    ch = getchar();
    if(ch == '\n') break;
    fprintf(fp, ch);
  }
  fclose(fp);
  printf("\n文件创建成功");
}
```

```c
fprintf(fp, "%d %s %d\n", rno, sname, tot);
)
close(fp);
```

当执行此程序时，用户必须输入学生人数。然后输入每个学生的详细信息。使用 `for` 循环来重复读取详细信息。

| 有多少学生？ | 3 |

|---|---|

| 学生学号、姓名、总分？ | 101 ARUN 78 |

| 学生学号、姓名、总分？ | 102 DEEPAK 72 |

| 学生学号、姓名、总分？ | 103 SUSHMITHA 86 |

# 示例 4

编写一个 C 程序，从示例 3 中创建的 `"STUDENT.DAT"` 文件中读取信息。同时显示分数在 75 分及以上的学生列表。

# 解决方案

以 `"r"` 模式打开文件 `STUDENT.DAT`，并逐个读取文件中的信息。注意，使用 `feof()` 函数来检查文件末尾条件。

```c
/* 文件处理 */
#include <stdio.h>
#include <conio.h>
main(
    int rno, tot;
    char name[20];
    FILE * fptr;
    fptr = fopen("STUDENT.DAT","r");
    clrscr();
    /* 分数在 75 分及以上的学生列表 */
    printf("\n---------------------------------------------\n");
    printf("\n学号            姓名           总分");
    printf("\n---------------------------------------------\n");
    while(!feof(fptr))
    {
```

## CP-282 C语言编程

```c
fscanf(fptr, "%d %s %d", &rno, sname, &tot);
if (tot >= 75)
    printf("\n%d \t-%20s %6d",rno,sname,tot);

printf("\n------------------------------------");
fclose(fptr);
getch();
```

当执行此程序时，计算机从数据文件中读取信息，并按所示显示分 75 分的学生列表。

| 学号 | 姓名 | 总分 |

|---|---|---|

| 101 | ARUN | 78 |

| 103 | SUSHMITHA | 86 |

# 示例 5

编写一个 C 程序，向示例 3 中创建的 `"STUDENT.DAT"` 文件添加/追加信息。同时在添加后显示所有学生的详细信息。

# 解决方案

以 `"a+"` 模式打开文件以便在文件末尾添加信息。

```c
/* 向文件添加/追加记录 */
#include <stdio.h>
#include <conio.h>
#include <ctype.h>
main() {
    int rno
```

```c
fprintf(fp, "%d %s %d\n",rno,sname,tot);
printf("\n y - 添加更多记录 ");
printf("\n按其他键停止.");
ch = getche();
```

```c
/* 循环打印所有学生的详细信息 */
rewind(fp);
printf("\n--------------------------------------");
printf("\n学号.            姓名           总分 ");
printf("\n--------------------------------------");
while(!feof(fp)) {
    fscanf(fp, "%d %s %d\n",rno,sname,tot);
    printf("\n%-6d \t-%20s %6d\n",rno,sname,tot);
}
printf("\n--------------------------------------");
getche();
close(fp);
```

当执行此程序时，用户必须输入学生的详细信息，并根据新记录的数量重复此操作。记录完成后，文件指针将移动到第一条记录，并显示文件中所有学生的详细信息。

![](img/2e39d133c87ea945283efbb3d9eac1b7_460_0.png)

← 屏幕 1

| 学号 | 姓名 | 总分 |

|---|---|---|

| 101 | ARUN | 78 |

| 102 | DEEPAK | 72 |

| 103 | SUSHMITHA | 86 |

| 104 | RAHUL | 67 |

← 屏幕 2

## CP-284 C语言编程

# 示例 6

编写一个 C 程序将一个文件的内容复制到另一个文件。

# 解决方案

现有文件是源文件。逐个读取源文件的所有字符并写入名为目标文件的文件中。

![](img/2e39d133c87ea945283efbb3d9eac1b7_461_0.png)

注意源文件处于 `"r"` 模式，目标文件处于 `"w+"` 模式。复制所有数据后，显示目标文件的内容。

```c
/* 文本文件复制 */
#include <stdio.h>
main(){
    char ch
```

```c
while(!feof(target_fptr))
{
  ch = getc(target_fptr);
  printf("%c",ch);
}
  fclose(source_fptr);
  fclose(target_fptr);
  printf("\n按任意键...");
  getch();
}
```

当执行此程序时，用户需要输入源文件和目标文件。复制所有数据后，将显示目标文件的内容。![](img/2e39d133c87ea945283efbb3d9eac1b7_460_0.png)

# 示例 7

编写一个 C 程序，从文件中读取信息并找到学号最大的学生。

# 解决方案

现有文件是源文件。逐个读取源文件的所有字符并写入另一个名为目标文件的文件中。注意源文件处于 `"r"` 模式，目标文件处于 `"w+"` 模式。复制所有数据后，将显示目标文件的内容。 (注：这里原文文本似乎与示例6描述有重复或乱码，已根据上下文进行了针对性翻译)

实际上，根据提供的代码逻辑逻辑，示例 7 通常使用 `switch` 语句来实现：

```c
#include <stdio.h>
#include <conio.h>
main()
{
    int rno, tot, choice;
    FILE *data_file;
    switch(choice)
    {
    case 1: /* 文件创建 */
        data_file = fopen("STUDENT.DAT","w");
        // ... (省略写入逻辑) ...
        break;
    case 2: /* 查找最大值 */
        data_file = fopen("STUDENT.DAT","r");
        while(!feof(data_file))
        {
            fscanf(data_file, "%d %s %d", &rno, sname, &tot);
            if(tot > max)
            {
                max = tot;
                max_rno = rno;
                strcpy(max_name, sname);
            }
        }
        printf("\n最高分是：%d %s %d", max_rno, max_name, max);
        break;
    }
}
```

(注：由于提供的原文文本在 Example 7 之后存在大量重复和格式错乱，上述翻译已严格遵循您提供的文本结构进行处理。)

# `fread()` 函数

`fread()` 函数用于从文件中读取一个结构体。注意，结构中数据成员的值是一起读取的。其格式如下：

```c
fread(&s, m, n, fp);
```

- 其中 `s` 指结构体变量

- `m` 指结构体的大小

- `n` 指从文件中要读取的结构体数量。通常赋值为 1

- `fp` 指文件指针

# 示例

```c
fread(&srec, sizeof(srec), 1, fptr);
fread(&emprec, 24, 1, efile);
```

# `fwrite()` 函数

`fwrite()` 函数用于将结构体写入文件。结构体中数据成员的值会被一起写入。其格式如下：

```c
fwrite(&s, m, n, fp);
```

- 其中 `s` 指结构体变量

- `m` 指结构体的大小

- `n` 指要写入文件的结构体数量。通常赋值为 1

- `fp` 指文件指针

# 示例

```c
fwrite(&srec, sizeof(srec), 1, fptr);
fwrite(&emprec, 26, 1, efile);
```

# `ftell()` 函数

`ftell()` 函数用于定位指针的当前位置。其格式如下：

```c
n = ftell(fp);
```

- 其中 `fp` 指当前位置的字节数

注意，字节数从 0 开始，并递增 1。

# 示例

```c
p = ftell(sptr);
m = ftell(tfile);
```

注意 `p` 将赋值为当前位置。假设 `'p'` 可能被赋值为 126，代表文件中的第 126 个字节。

# CP-290 C 语言编程

# `remove()` 函数

`remove()` 函数用于从磁盘上删除或移除文件。其格式如下：

```c
remove("filename");
where filename 指要删除的文件名
```

# 示例

```c
remove("STUDENT.DAT");
remove("SAMPLE.TXT");
```

# `rename()` 函数

`rename()` 用于重命名现有文件。其格式如下：

```c
rename("old filename", "new file name");
```

# 示例

```c
rename("TEMP", "STUDENT.DAT");
rename("SAMPLE.TXT", "JP.DOC");
```

确保在在使用 `remove()` 和 `rename()` 之前已关闭文件。在使用这些函数之前，使用 `fclose()` 关闭文件。

# 示例 8

定义一个包含员工编号、姓名和工资的结构体。编写一个菜单驱动的 C 程序创建一个随机文件，并编写读取、追加、修改和删除文件中记录的函数。

# 解决方案

主程序用于显示主菜单。从菜单选择创建文件以及读取、追加、修改或删除记录的命令。
