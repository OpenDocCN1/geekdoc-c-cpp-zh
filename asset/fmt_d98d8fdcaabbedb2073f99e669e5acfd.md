
输出：`AIDNI SI YM YRTNUOC`

假设最大单词长度为 10 个字符，单词由换行符/空格分隔。

## 程序

```c
/* Read a file and print each word in reverse order */
#include <stdio.h>
int main()
{
    FILE *fp;
    char str[ 11 ], ch;
    int i=0;
```

```c
fp = fopen ("INPUT.TXT", "r");

if ( fp == NULL )
{
    puts ("Unable to open file\n");
    exit (1 );
}

while ( (ch = getc ( fp )) != EOF )
{
    if ( ch == '\n' || ch == ' ')
    {
        str[i] = '\0';
        // 此处编写反转逻辑
        printf("%s", str);
        i = 0;
    }
    else
    {
        str[i++] = ch;
    }
}

fclose ( fp );
return 0;
}
```

- (s) 编写一个 C 程序读取大文件 `NOTES.TXT` 并以分页页的形式打印，在 50 行处分页，并在每页屏幕上显示暂停信息以便用户换纸。程序：

```c
/* Reading a file and printing on cut sheets */
## include <stdio.h>

int main()
{
  FILE *fp;
  /* 每行字符和每页行数 */
  int charcount = 0, linecount = 0;
  char ch;

  fp = fopen("NOTES.TXT", "r"); /* 读取模式 */

  if (fp == NULL) {
    puts("Unable to open file\n");
    exit (1);
  }

  /* 读取到文件结束 */
  while ((ch = getc (fp)) != EOF) {
    if (ch == '\t') {
      charcount += 3; /* 制表符加3个字符 */
    }

    charcount++;

    if (ch == '\n' || charcount >= 80) {
      linecount++; /* 80个字符后行数加1 */
      charcount = 0; /* 重置字符计数器 */
    }

    if (linecount == 49) { /* 每49行打印 */
      puts("Insert another page, press any key...");
      linecount = 0; /* 重置行计数器 */
    }
    fputc (ch, stdout); /* 发送到打印机 */
  }
  fclose ( fp );
  return 0;
}
```

# 第二十章 输入/输出的更多问题

## [A] 回答：

(a) 你将如何使用以下程序

- 将一个文件的内容复制到另一个文件中。
- 创建新文件并添加某些文本。
- 显示现有文件的内容。

```c
#include <stdio.h>
int main()
{
    char ch, str[10 ];
    while (( ch = getc ( stdin )) != EOF)
        putc ( ch, stdout);
    return 0;
}
```

答案：

```c
#include <stdio.h>
int main()
{
    char ch, str[10 ], tar[10 ];
    /* fp1: 源文件指针 */
    /* ft: 目标文件指针 */
    FILE *fp1, *ft;

    /* 将一个文件的内容复制到另一个 */
    while ((ch = getc (fp1)) != EOF)
        putc ( ch, ft );

    /* 创建新文件并添加某些文本 */
    while ((ch = getc (stdin)) != EOF)
        putc ( ch, ft );

    /* 显示现有文件的内容 */
    while ((ch = getc (fp1)) != EOF)
        putc ( ch, stdout );

    return 0;
}
```

(b) 判断对错：

1. 如果我们定义没有参数的 `main()`，可以在命令行传递参数。

答案：False

2. 使用标准文件指针不需要使用 `fopen()` 打开文件。

答案：True

3. `argv` 数组的第一个元素始终是可执行文件的名称。

答案：False

(c) 指出以下程序的错误（如果有）：

```c
#include <stdio.h>
int main (int ac, char (*) av[])
{
    printf("%d\n", ac);
    printf("%s\n", av[0]);
    return 0;
}
```

`av` 的声明应该是 `char *av[]`。

## [B] 尝试以下：

- 使用命令行参数编写程序，在文件中搜索一个单词并替换为指定的单词。程序的用法所示。

`C> change <old word> <new word> <filename>`

## 程序：

```c
#include <stdio.h>
#include <string.h>

FILE *fs, *ft;
int newstr (char *, char *, char);
int main (int argc, char *argv[])
{
    char *str[80];
    char *arg1, *arg2, *fname;
    int newstr (char *s, char *t, char *n);
    int c = 0;

    /* 检查传递了正确数量的参数 */
    if (argc != 4) {
        puts("Improper number of arguments\n");
        exit (1);
    }

    fs = fopen ( argv[ 3 ], "r+");
    ft = fopen ("temp.c", "w");

    if ( fs == NULL ) {
        puts ("Unable to open the file\n");
        exit (2);
    }

    if ( strlen ( argv[ 1 ] ) > strlen ( argv[ 2 ] )) {
        printf ("Number of characters in strings mismatch\n");
        exit (3);
    }

    arg1 = argv[ 1 ];
    arg2 = argv[ 2 ];
    fname = argv[ 3 ];

    while ( gets ( str, 79, fs ) != NULL ) {
        c = newstr ( str, arg1, arg2);
    }

    fclose ( fs );
    fclose ( ft );
    printf("%d replacements done\n", c );
    remove ( fname );
    rename ("temp.c", fname );

    return 0;
}
```

```c
int newstr ( char *pt, char *t, char *n ) {
    static int count = 0;
    char *p, *temp, *news, *p1 ;
}
```

```c
/* 在我们的数组中查找输入的字符串 */
p1 = pt;
do
{
    p = strstr ( p1, t);

    if ( p == NULL)
        break;

    /* 复制剩余字符串 */
    news = p + strlen ( t );
    strcpy ( temp, news);

    /* 替换旧字符串 */
    strcpy ( p, n);

    /* 最后追加剩余部分 */
    strcat ( p, temp );
    count++;

    p1 = p1 + strlen (t);
} while ( 1 );

fputs (pt, ft);
return count;
```

(b) 编写一个可以在命令行提示符作为计算实用工具使用的程序。程序的用法如下所示。

`C> calc <switch> <n> <m>`

其中，`n` 和 `m` 是两个整数操作数。`switch` 可以是任何算术运算符或比较运算符之一。如果提供了算术运算符，输出应为操作的结果。如果提供了比较运算符，则输出应为 True 或 False。

## 程序：

```c
/* 对两个整数执行给定的算术操作 */
#include <stdio.h>
#include <string.h>

int main ( int argc
{
    case 0:
        result = first + second;
        printf("%d\n", result);
        break;
    case 1:
        result = first - second;
        printf("%d\n", result);
        break;
    case 2:
        result = first * second;
        printf("%d\n", result);
        break;
    case 3:
        result = first / second;
        printf("%d\n", result);
        break;
    case 4:
        result = first % second;
        printf("%d\n", result);
        break;
    case 5:
        result = first && second;
        result == 0 ? printf("False\n") : printf("True\n");
        break;
    case 6:
        result = first || second;
        result == 0 ? printf("False\n") : printf("True\n");
        break;
}
return 0;
}
```

# 第二十二章 位操作

[A] 回答以下问题：

- (a) 颜色信息存储在一个名为 `color` 的 `char` 变量位中。第 0 到 6 位分别代表彩虹的 7 种颜色，例如：位 0 代表紫色，1 代表靛色，以此此类推。编写一个程序，要求用户输入一个数字，并根据该数字报告彩虹中的哪些颜色。

程序：

```c
/* 确定颜色 */
#include <stdio.h>

int main()
{
    int color;

    printf ("\nEnter任意数字: ");
    scanf("%d",&color);

    printf ("\代表的颜色有:\n");

    if (( ( color & 1) == 1) /* 位 0 */
        printf ("Violet\n");
    if (( (color & 2) == 2) /* 位 1 */
        printf("Indigo");
    if (( (color & 4) == 4) /* 位 2 */
        printf("Blue");
    if (( (color & 8) == 8) /* 位 3 */
        printf("Green");
    if (( (color & 16) == 16) /* 位 4 */
        printf("Yellow");
    if (( (color & 32) == 32) /* 位 5 */
        printf("Orange");
    if (( (color & 64) == 64) /* 位 6 */
        printf("Red");

    return 0;
}
```

(b) 一家计划在市场上推出新报纸的公司正在进行调查。调查中考虑的各种参数有：经济状况（上层、中层和下层阶级）、读者偏好的语言（英语、印地语、区域语言）以及报纸类型（日报、杂志、小报）。编写一个程序，通过键盘读取 10 名受访者的数据，并将信息存储在整数数组中。存储在整数中的位信息如下所示：

| 位数 | 信息 |
|---|---|
| 0 | 上层类 |
| 1 | 中层类 |
| 2 | 下层 |
| 3 | 英语 |
| 4 | 印地语 |
| 5 | 区域语言 |
| 6 | 日报 |
| 7 | 杂志 |
| 8 | 小报 |

最后，给出每天阅读英语报的人数、阅读小报的上层阶级人数以及区域语言读者的统计数据。

程序：

```c
/* 实现调查 */
#include <stdio.h>

int main()
{
    int status, lang, cat;
    int data[10];
    int i;
    int rl = 0, ut = 0, eng = 0;

    /* 将数组初始化为 0 */
    for (i = 0; i < 10; i++)
        data[i] = 0;

    for (i = 0; i < 10; i++) {
        printf("\nEnter经济状况: 上层/中层/下层阶级: (0/1/2): ");
        scanf("%d", &status);

        /* 检查状态 */
        switch (status) {
            case 0:
                data[i] = data[i];
                break;
            case 1:
                data[i] = data[i];
                break;
            case 2:
                data[i] = data[i];
                break;
        }
        printf("\nEnter偏好的语言: 英语/印地语/区域: (0/1/2): ");
        scanf("%d", &lang);

        printf("\nEnter报纸类型: 日报/杂志/小报: (0/1/2): ");
        scanf("%d", &cat);

        /* 此处省略位操作逻辑 */
    }
    // 统计数据逻辑将此处
    return 0;
}
```

(c) 在校际比赛中进行板球、篮球、网球、台球和象棋。赢得 5 场以上比赛的学院将获得冠军。如果通过键盘输入上述数字，请编写一个程序找出该学院是否获得了冠军，以及赢得的次数。

程序：

```c
#include <stdio.h>

int main()
{
    int game, cnt, count = 0;

    printf("\nEnter任意数字: ");
    scanf("%d",&game);

    /* 计数比赛 */
    for ( cnt = 1 ; cnt <= 256 ; cnt *= 2)
    {
        if (( game & cnt) == cnt)
            count++;
    }
    printf("赢得的比赛次数为:%d\n", count);

    if (count >= 5)
    {
        printf("学院获得了冠军\n");
    }
    return 0;
}
```

# 第二十二章：位操作

`printf("学院赢得的比赛有:\n");`

```c
if ((game & 1) == 1) /* 位 0 */
    printf("板球");
if ((game & 2) == 2) /* 位 1 */
    printf("篮球");
if ((game & 4) == 4) /* 位 2 */
    printf("足球");
if ((game & 8) == 8) /* 位 3 */
    printf("曲球");
if ((game & 16) == 16) /* 位 4 */
    printf("网球");
if ((game & 32) == 32) /* 位 5 */
    printf("台球");
if ((game & 64) == 64) /* 位 6 */
    printf("卡龙");
if ((game & 128) == 128) /* 位 7 */
    printf("象棋");

return 0;
```

(d) 动物可能是犬科动物（狗、狼、狐等）或猫科动物（猫、猞猁、豹等）、鲸类动物（鲸、一角鲸等）或袋类动物（考拉、袋鼠等）。特定动物是犬科、猫科、鲸类或袋类动物的信息分别存储在名为 `type` 的整数变量的第 0、1、2 和 3 位。变量 `type` 的第 4 位存储关于动物是肉食动物还是草食动物的信息。

对于以下动物，完成程序以确定该动物是草食动物还是肉食动物。
