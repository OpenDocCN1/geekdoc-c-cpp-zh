
```c
#include <stdio.h>
#include <stdlib>

// 我们要排序的结构体类型
struct animal {
    char *name;
    int leg_count;
};

// 这是由 qsort 调用的比较函数，帮助确定
// 具体按什么进行排序。我们将用它按 leg_count 排序
// 动物结构体数组。
int comp(const void *elem1, const void *elem2)
{
    // 我们知道正在排序动物，所以让两个参数
    // 都成为指向 struct animal 的指针
    const struct animal *animal1 = elem1;
    const struct animal *animal2 = elem2;

    // 根据我们想要排序的标准返回 <0 或 >0。

    // 我们按 leg_count 升序排序，所以返回
    // leg_count 的差异
    if (animal1->leg_count > animal2->leg_count)
        return 1;

    if (animal1->leg_count < animal2->leg_count)
        return -1;

    return 0;
}

int main(void)
{
    // 我们构建一个包含 4 个不同特征动物的数组。
    // 这个数组按 leg_count 排序是有序的，
    // 我们将在几秒后对其排序。
    struct animal a[4] = {
        {.name="Dog", .leg_count=4},
        {.name="Monkey", .leg_count=2},
        {.name="Antelope", .leg_count=4},
        {.name="Snake", .leg_count=0}
    };

    // 调用 qsort 排序数组。qsort 需要明确告知
    // 根据什么排序这些数据，我们将在 comp()
    // 函数内部完成这一点。

    // 此调用表示：qsort 数组 a，它有 4 个元素，
    // 每个元素的大小为 sizeof(struct animal) 字节，
    // 这是一个比较任意两个元素的函数。
    qsort(a, 4, sizeof(struct animal), comp);

    // 打印所有内容
    for (int i = 0; i < 4; i++) {
        printf("%d: %s\n", a[i].leg_count, a[i].name);
    }
}
```

只要你给 `sort()` 提供一个可以比较排序数组中任意两个项的函数，它就可以排序任何内容。而且它这样做时不需要在任何地方硬编码项目的类型。`qsort()` 仅仅根据你传递的 `comp()` 函数的结果来重新排列字节块。

# 12. 手动分配

在许多语言中，内存是由系统处理的，但在 C 中，你必须自己管理。这意味着在你需要时分配内存，并在完成后释放它。

堆是一个可以在运行时使用的巨大内存池。为了从堆上获取内存，我们使用 `malloc()`。`malloc` 的意思是“memory allocation”（内存分配）。它返回一个指向分配块起始字节的指针。

```c
void *malloc(size_t size);
```

`size` 参数是你想要分配的字节数。它返回一个 `void*`，这是一个可以转换为任何其他指针类型的通用指针。如果 `malloc()` 分配内存失败，将返回 `NULL`。

检查 `malloc()` 是否返回 `NULL` 总是重要的。

```c
int *ptr = malloc(sizeof(int));
if (ptr == NULL) {
    // 处理错误
    return 1;
}
```

当你完成分配内存的使用后，必须调用 `free()` 将其返回系统。不这样做会导致内存泄漏。

```c
free(ptr);
```

在调用 `free(ptr)` 后，该指针会变成“悬空指针”，因为它仍然指向不再属于你的内存。在释放后将其设置为 `NULL` 是一个良好的习惯。

```c
free(ptr);
ptr = NULL;
```

## 12.3 为数组分配空间

我们已经见过如何为单个对象分配空间；那么数组中的多个对象该怎么办呢？

在 C 语言中，数组是连续内存区域中紧挨着排列的一系列相同类型的对象。

我们可以分配一段连续的内存——我们已经见过如何做到的了。如果我们需要 3490 字节的内存，可以直接请求：

```c
char *p = malloc(3490); // 搞定
```

而且——确实——这就是一个包含 3490 个字符的数组（一个字符串！），因为每个 `char` 占用 1 字节。换句话说，`sizeof(char)` 是 1。

注意：新分配的内存不会进行初始化——它充满了垃圾数据。如果你需要，可以使用 `memset()` 清除它，或者使用下方的 `calloc()`。

但我们只需要将对象的大小乘以所需的元素个数，并使用指针或数组表示法来访问它们即可。示例！

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    // 为 10 个 int 分配空间
    int *p = malloc(sizeof(int) * 10);

    // 分配值 0-45：
    for (int i = 0; i < 10; i++)
        p[i] = i * 5;

    // 打印所有值 0, 5, 10, 15, ..., 45
    for (int i = 0; i < 10; i++)
        printf("%d\n\n", p[i]);

    // 释放空间
    free(p);
}
```

关键在于 `malloc()` 这一行。如果我们知道每个 `int` 需要 `sizeof(int)` 字节来存储，并且我们需要 10 个，就可以可以通过方式分配相应字节数：

```c
sizeof(int) * 10
```

这个技巧适用于所有类型。只需将其传递给 `sizeof` 并乘以数组的大小即可。

## 12.4 替代方案：calloc()

这是另一种与 `calloc()` 功能相相似的分配方式，但有两个主要区别：

- 它不是单次分配，而是传递单个元素的大小和要分配的元素个数。它就像是专为分配数组设计的。

- 它会将内存清零。

你仍然使用 `free()` 来释放通过 `calloc()` 获取的内存。

这里是 `calloc()` 和 `malloc()` 的对比：

```c
// 使用 calloc() 为 10 个 int 分配空间并初始化为0：
int *p = calloc(10, sizeof(int));

// 使用 malloc() 为 10 个 int 分配空间并初始化为0：
int *q = malloc(10 * sizeof(int));
memset(q, 0, 10 * sizeof(int)); // 设置为0
```

同样，两者的结果大小相同，只是 `malloc()` 不会自动清零内存。

## 12.5 使用 realloc() 修改分配的大小

如果你已经分配了 10 个 `int`，但后来需要 20 个，该怎么办？

一种方案是一些新空间，然后用 `memcpy` 将内存覆盖……但事实证明，有时你不需要移动任何。有一个函数足够聪明，可以在所有情况下做正确的事：`realloc()`。

它接收一个指向之前分配的内存（通过 `malloc()` 或 `calloc()`）的指针，以及目标内存区域的新大小。

它会扩大或缩小该内存，并返回指向它的新指针。有时它可能会返回相同的指针（如果数据不需要复制到其他地方），也可能返回不同的指针（如果数据必须复制）。

在使用 `realloc()` 时，务必指定要分配的**字节数**而不仅仅是元素个数！

```c
num_floats = 2;
```

```c
np = realloc(p, num_floats); // 错误：需要字节数，元素个数！
```

```c
np = realloc(p, num_floats * sizeof(float)); // 更好！
```

让我们分配一个包含 20 个 `float` 的数组，并将其修改为包含 40 个元素的数组。

我们将 `realloc()` 的返回值赋值给另一个指针，以确保它是 `NULL`。如果不是 `NULL`，我们就可以将其重新赋值给原始指针。（如果我们直接将返回值赋值给原始指针，一旦函数返回 `NULL`，我们就会丢失指针且无从找回）。

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    // 为 20 个 float 分配空间
    float *p = malloc(sizeof(float) * 20); // sizeof *p 是 sizeof(float)

    // 分配浮点值 0.0-1.0：
    for (int i = 0; i < 20; i++)
        np[i] = i / 20.0;

    // 等等！让我们实际上把它变成一个 40 个元素的数组
    float *new_p = realloc(p, p * 40);

    // 检查是否成功重新分配
    if (new_p == NULL) {
        printf("Error reallocing\n");
        return 1;
    }

    // 如果成功了，我们可以重新赋值 p
    p = new_p;

    // 分配 20-40 范围内的元素
    for (int i = 20; i < 40; i++)
        p[i] = (i - 20) / 20.0;

    // 打印所有 0-40 的值
    for (int i = 0; i < 40; i++)
        printf("%f\n", p[i]);

    // 释放空间
    free(p);
}
```

注意我们获取 `realloc()` 的返回值并重新赋值给传入的同一个指针。这非常常见。如果代码看起来奇怪，记得 `sizeof *p` 等于 `sizeof(float)`。

### 12.5.1 读取任意长度的行

我想通过这个完整的示例演示两点：

1. 当需要更多数据时使用 `realloc()` 扩展缓冲区。

2. 完成读取后使用 `realloc()` 将缓冲区缩小到完美大小。

我们看到一个不断调用 `getc()` 到缓冲区，直到看到换行符。一旦发现换行符，将其缩小到合适的大小并返回。

```c
#include <stdio.h>
#include <stdlib.h>

char *readline(FILE *fp)
{
    int offset = 0; // 缓冲区中的索引
    int bufsize = 4; // 初始大小（2的幂）
    char *buf; // 已读取的字符
    int c;

    buf = malloc(bufsize); // 分配缓冲区
    if (buf == NULL) // 错误检查
        return NULL;

    // 主循环--读取直到换行符或 EOF
    while ((c = getc(fp)) != '\n' && c != EOF) {
        // 检查缓冲区空间，考虑 NUL 终止符字节
        if (offset == bufsize - 1) { // -1 用于 终止符
            bufsize *= 2; // 空间翻倍

            char *new_buf = realloc(buf, bufsize);

            if (new_buf == NULL) { // 错误，释放并退出
                free(buf);
                return NULL;
            }

            buf = new_buf; // 成功的 realloc
        }
        buf[offset++] = c; // 将字节添加到缓冲区
    }

    // 遇到换行符或 EOF...
    // 如果在 EOF 处读取字节，释放缓冲区并返回 NULL 表示到达 EOF
    if (c == EOF && offset == 0) {
        free(buf);
        return NULL;
    }

    // 缩小以适应
    if (offset < bufsize - 1) { // 如果空间不足
        char *new_buf = realloc(buf, offset + 1); // +1 用于 终止符

        // 如果成功，将 buf 指向 new_buf；
        // 否则保持原样
        if (new_buf != NULL)
            buf = new_buf;
    }

    // 添加 NUL 终止符
    buf[offset] = '\0';

    return buf;
}

int main(void)
{
    FILE *fp = fopen("foo.txt", "r");
    char *line;

    while ((line = readline(fp)) != NULL) {
        printf("%s\n", line);
        free(line);
    }
    fclose(fp);
}
```

在这样移动内存时，通常（尽管不是强制）每次倍增空间以减少 `realloc` 的次数。

最后你可能会注意到 `readline()` 返回的是指向 `malloc()` 缓冲区的指针。因此，由调用者在完成后显式地 `free()` 该内存。

### 12.5.2 与 NULL 的 realloc

简单如反！这些行是等价的：

```c
char *p = malloc(3490);
char *p = realloc(NULL, 3490);
```

如果你有某种分配循环且不想对第一次 `malloc()` 进行特殊处理，这非常方便。

```c
int *p = NULL;
int length = 0;

while (!done) {
    // 再分配 10 个 int：
    length += 10;
    p = realloc(p, sizeof *p * length);

    // 做一些神奇的事情
    //
}
```

在示例中，由于 `p` 初始为 `NULL`，所以不需要初始的 `malloc()`。

## 12.6 对齐分配

你可能用不到这个。

现在不想在这里说得太深，但有一种叫做“内存对齐”的东西，它与内存地址（指针值）是某个数字的倍数有关。

例如，系统可能要求 16 位的值起始于 2 的倍数内存地址。或者要求 64 位的值起始于 2, 4, 8 等数字的倍数内存地址。这取决于 CPU。

某些系统需要这种对齐来实现快速内存访问，甚至为了所有的内存访问。现在，如果你使用 `malloc()` `、`calloc()` ` 或 `realloc()`，它们将给你一块对于任何值（甚至是结构体）都良好对齐的内存。这在所有情况下都有效。

但有时你可能知道某些数据可以在较小的边界上对齐，或者由于某种原因必须在更大的边界上对齐。我想这在嵌入式系统编程中更常见。

在这种情况下，你可以通过 `aligned_alloc( )` 指定对齐方式。

## 第 12 章. 手动内存分配

对齐是一个大于 0 的整数幂，例如 2, 4, 8, 16 等，你需要在提供你感兴趣的字节数之前，将其传递给 `aligned_alloc()` 函数。

另一个限制是，你分配的字节数必须是对齐值的倍数。但这可能会发生。请参阅 C 缺陷报告（Defect Report） 460。

让我们来做一个例子，在 64 字节边界上分配：

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
```

```c
int main() {
    // 分配 256 字节并对齐到 64 字节边界
    char *p = aligned_alloc(64, 256); // 256 == 64 * 4

    // 在其中拷贝一个字符串并打印
    strncpy(p, "Hello, world!");
    printf("%s\n", p);

    // 释放空间
    free(p);
}
```

我想在这里提一下关于 `realloc()` 和 `aligned_alloc()` 的说明。`realloc()` 没有任何对齐保证，因此如果你需要获取某些对齐分配的空间，你必须通过 `malloc(ptr)` 这种困难的方法来处理。

这里有一个非标准的 `aligned_realloc()` 函数，如果你需要的话：
