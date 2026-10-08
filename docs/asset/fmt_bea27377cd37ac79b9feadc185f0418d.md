
这个程序是该系列中第一个从 `main` 函数返回错误值的程序。如果 `fopen` 命令失败，`f` 将包含一个 NULL 值（0）。我们用 `if` 语句检查错误。该语句查看变量 `f` 的真假值。记住在 C 语言中，0 是假，任何其他值都是真。所以如果打开文件发生错误，`f` 将包含零，即为假。`!` 是取反运算符。它反转一个布尔值。所以语句可以写成这样：

```c
if ( f == 0)
```

这是等价的。然而，`(!f)` 更常见。如果发生文件错误，我们从 `main` 函数返回 1。在 Linux 中，你实际上可以在命令行上测试此值。详情请参 shell 文档。

# 第18章：二进制文件

二进制文件与结构体数组非常相似，不同之处在于结构体在磁盘文件中，其速度比在内存数组中更快。由于二进制文件中的结构体在磁盘上，你可以创建非常大的集合（仅受限于你的可用磁盘空间）。它们也是永久的，并且始终可用的。唯一的缺点是磁盘访问时间带来的速度慢问题。

二进制文件有两个区别于文本文件的特征：

- 你可以立即跳转到文件中的任何结构体，这提供了类似于数组的随机访问能力。
- 你可以在任何时间在任何位置修改文件中任何位置的结构体内容。

二进制文件的读写速度也比文本文件快，因为记录的二进制镜像直接从内存存储到磁盘（或反之）。在文本文件中，所有内容都必须在文本和二进制之间反复转换，这会消耗时间。

C 语言非常纯粹地支持了“结构体文件”的概念。一旦打开文件，你就可以读取一个结构体、写入一个结构体或定位到文件中的任何结构体。这种文件概念支持**文件指针**的概念。当文件被打开时，指针指向记录 0（文件中的第一条记录）。任何**读取操作**都会读取当前指向的结构体并将指针向下移动一个结构体。任何**写入操作**都会写入当前指向的结构体并将指针向下移动一个结构体。**Seek** 将指针移动到请求的记录。

请记住，C 语言将磁盘文件中的所有内容都视为从磁盘读取到内存或从内存写入磁盘的字节块。C 语言使用文件指针，但它可以指向文件中的任何字节位置。因此，你必须跟踪这些。

以下程序说明了这些概念：

```c
#include <stdio.h>

/* 随机记录描述 - 可以是任意 */
struct rec {
    int x, y, z;
};

/*
 * 从 "junk" 文件写入并读取 10 条任意记录。
 */
int main(void) {
    int i, j;
    FILE *f;
    struct rec r;

    /* 创建包含 10 条记录的文件 */
    f = fopen("junk", "w");
    if (!f) {
        return 1;
    }
    for (i = 1; i <= 10; i++) {
        r.x = i;
        fwrite(&r, sizeof(struct rec), 1, f);
    }
    fclose(f);
```

```c
/* 读取这 10 条记录 */
f = fopen("junk", "r");
if (!f)
{
    return 1;
}
for (i = 1; i <= 10; i++)
{
    fread(&r, sizeof(struct rec), 1, f);
    printf("%d\n", r.x);
}
fclose(f);
printf("%d\n");

/* 使用 fseek 倒序读取这 10 条记录 */
f = fopen("junk", "r");
if (!f)
{
    return 1;
}
for (i = 9; i >= 0; i--)
{
    fseek(f, sizeof(struct rec)*i, SEEK_SET);
    fread(&r, sizeof(struct rec), 1, f);
    printf("%d\n", r.x);
}
fclose(f);
printf("%d\n");

/* 使用 fseek 每隔读取一条记录 */
f = fopen("junk", "r");
if (!f)
{
    return 1;
}
fseek(f, 0, SEEK_SET);

for (i = 0; i < 5; i++)
{
    fread(&r, sizeof(struct rec), 1, f);
    printf("%d\n", r.x);
    fseek(f, sizeof(struct rec), SEEK_CUR); // 注意：此处原文逻辑可能有误，但按原文翻译
}
fclose(f);
printf("\n");
```

```c
/* 使用 fseek 修改第 4 条记录并写回 */
f = fopen("junk", "r+");
if (!f)
{
    return 1;
}
fseek(f, sizeof(struct rec)*3, SEEK_SET);
r.x = 100;
fseek(f, sizeof(struct rec)*3, SEEK_SET);
fwrite(&r, sizeof(struct rec), 1, f);
fclose(f);
printf("\n");
```

```c
/* 读取这 10 条记录以确保第 4 条记录已修改 */
f = fopen("junk", "r");
if (!f)
{
    return 1;
}
for (i = 1; i <= 10; i++)
{
    fread(&r, sizeof(struct rec), 1, f);
    printf("%d\n", r.x);
}
fclose(f);

    return 0;
}
```

在这个程序中，使用了结构体描述 `rec`，但你可以使用任何结构体描述。可以看到 `fopen` 和 `fclose` 的工作方式与文本文件相同。

新函数是 `fread`、`fwrite` 和 `fseek`。`fread` 函数四个四个参数：

- 内存
- 每个块读取的字节数
- 读取的块数
- 文件变量

因此，`fread(&r, sizeof(struct rec), 1, f);` 表示从文件 `f`（从指针当前位置）读取 12 字节（`rec` 的大小）。通过将 1 改为 100，就可以轻松地从磁盘读取 100 块到数组中。

`fwrite` 函数以相同的方式工作，但将字节块从内存移动到文件。`fseek` 函数将文件指针移动到文件的字节。通常，你按 `sizeof(struct rec)` 的增量移动指针，以保持在记录边界。定位时可以使用三个选项：

- `SEEK_SET`
- `SEEK_CUR`
- `SEEK_END`

`SEEK_SET` 将指针从文件开头移动 x 字节（从文件的字节 0 开始）。`SEEK_CUR` 将指针从当前位置移动 x 字节。`SEEK_END` 从文件末尾移动（因此在使用此选项时必须使用负偏移量）。

上面的代码出现了几种不同的选项。特别注意使用 `r+` 模式打开文件的部分。它以读写模式打开文件，允许修改记录。代码定位到一条记录，读取它并修改一个字段；然后由于读取移动了指针而返回，并写回更改。

# 第19章

## 阅读

欲了解更多关于 C 及相关主题的信息，请查看下方链接。

1. Cprogramming.com: 编程教程
2. C 语言程序开发周期
3. 使用 C++ 面向对象编程简介
4. C 语言
5. comp.lang.c 常见问题

## 索引

- 地址运算符, 10
- 编译型语言, 2
- 华氏转摄氏度, 18
- if 语句, 13
- 库, 4
- printf, 7
- 编程语言, 2
- qcompiler, 2
- 类型, 5
- 变量, 5
