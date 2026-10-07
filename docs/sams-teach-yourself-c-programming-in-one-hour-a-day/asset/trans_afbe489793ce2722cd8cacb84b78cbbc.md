

# 第 17  使用磁盘文件

输入 ▼

代码列表 17.5 fileposition.c-- 使用 ftell() 和 rewind()

```c
// fileposition.c--演示了 ftell() 和 rewind()。
#include <stdlib.h>
#include <stdio.h>

#define BUFLEN 6

char msg[] = "abcdefghijklmnopqrstuvwxyz";
int main( void )
{
    FILE *fp;
    char buf[BUFLEN];

    if (fp = fopen("fileposition.txt", "w") == NULL) {
        fprintf(stderr, "Error opening file.");
        exit(1);
    }

    if (fputs(msg, fp) == EOF) {
        fprintf(stderr, "Error opening file.");
        exit(1);
    }

    fclose(fp);
// 现在以读取模式打开文件。
    if (fp = fopen("fileposition.txt", "r") == NULL) {
        fprintf(stderr, "Error opening file.");
        exit(1);
    }
    printf("%nImmediately after opening, position = %ld", ftell(fp));

// 读取 5 个字符。
    fgets(buf, BUFLEN, fp);
    printf("%nafter reading in %s, position = %ld", buf, ftell(fp));

// 读取接 5 个字符。
    fgets(buf, BUFLEN, fp);
    printf("\n\nNext 5 characters are %s, and position now = %ld", buf, ftell(fp));
}
```

# 理解顺序访问与随机文件访问

```c
48:   // 回置流。
49:
50:   rewind(fp);
51:
52:   printf("\nAfter rewinding, the position is back at %ld",
53:   ftell(fp));
54:
55:   // 读取 5 个字符。
56:
57:   fgets(buf, BUFLEN, fp);
58:   printf("\nreading starts at the beginning again: %s\n", buf);
59:   fclose(fp);
60:   return(0);
61: }
```

# 输出 ▼

刚打开后，位置 = 0
读取 abcde 后，位置 = 5

接 5 个字符是 fghij，现在位置为 = 10

回置后，位置回到 0
并且再次从头开始读取：abcde

# 分析 ▼

此程序将字符串 `msg` 写入名为 `position.txt` 的文件中。该消息由字母表的 26 个字母顺序组成。第 14 到 18 行以写入模式打开 `position.txt` 并测试以确保文件成功打开。第 20 到 24 行使用 `fprintf()` 将 `msg` 写入文件，并检查写入是否成功。第 26 行使用 `fclose()` 关闭文件，完成了创建文件供程序其余部分使用的过程。

第 30 到 34 行再次打开文件，但这次是用于读取的。第 35 行打印 `ftell()` 的返回值。注意，此位置位于文件开头。第 39 行执行 `fgets()` 来读取五个字符。第 40 行打印这五个字符和新的文件位置。注意 `ftell()` 返回了正确的偏移量。第 50 行调用 `rewind()` 将指针放回文件开头，然后在第 52 行再次打印文件位置。这应该向你确认 `rewind()` 重置了位置。第 57 行的额外读取进一步证实了程序确实回到了文件开头。第 59 行在程序结束前关闭了文件。

# fseek() 函数

通过 `fseek()` 库可以对流的位置指示器进行更精确的控制。通过使用 `fseek()`，你可以将位置指示器设置为文件的任何位置。该函数在 `stdio.h` 中的原型为：

```c
int fseek(FILE *fp, long offset, int origin);
```

参数 `fp` 是与文件关联的 FILE 指针。`offset` 是位置指示器按字节移动的字节距离。参数 `origin` 指定了移动的相对起点。`origin` 有三个值，在 `io.h` 中定义了符号常量，如表 17.2 所示。

| 表 17.2 fseek() 的可能值 | | |
| :--- | :--- | :--- |
| 常量 | 数值 | 描述 |
| SEEK_SET | 0 | 移动到开头 |
| SEEK_CUR | 1 | 从当前位置移动 |
| SEEK_END | 2 | 从文件末尾移动 |

如果指示器移动成功，函数 `fseek()` 返回 0；如果发生错误，返回非零。

输入 ▼

代码列表 17.6 fileposition.c-- 使用 fseek() 的随机访问

```c
1: // fileposition.c-- 使用 seekseek 的随机访问
2: #include <stdlib.h>
3: #include <stdio.h>
4:
5: #define MAX 50
6:
7: int main( void )
8: {
9:     FILE *fp;
10:    char buf[BUFLEN];
11:
12:    if (fp = fopen("fileposition.txt", "r") == NULL) {
13:        fprintf(stderr, "Error opening file.");
14:        exit(1);
15:    }
16:
17:    // 初始化数组
18:    for (count = 0; count < MAX; count++) {
19:        // ... (省略部分)
20:    }
21:
22:    // 移动到文件开头
23:    fseek(fp, 0, SEEK_SET);
24:
25:    // 向后移动 10 字节
26:    fseek(fp, 10, SEEK_CUR);
27:
28:    // 移动到文件末尾
29:    fseek(fp, -10, SEEK_END);
30:
31: }
```

