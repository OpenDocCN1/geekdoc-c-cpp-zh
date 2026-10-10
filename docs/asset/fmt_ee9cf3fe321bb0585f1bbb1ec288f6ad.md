
# C 和 C++ 实现了空终止字符串

`C` 和 `C++` 实现了空终止字符串。字符串是一个空终止字符数组（空值为 ASCII 0，表示为 `'\0'`）。因此，`C` 风格的空终止字符串是一个以空字符作为其最后一个最后一个元素的字符数组。这里有一个示例：

```c
"hello world"
```

`C` 编译器会自动在该字符串字面量的末尾添加一个空字符。包含在双引号内的字符序列被 `C` 编译器解释为常量字符字符串。常量字符串不能更改。

```c
char* str = "hello world";
str = 'z'; // 错误 - 尝试将 'h' 改为 'z'
```

声明一个存储空终止字符串的字符数组时，必须将其声明为比它可以包含的最大字符串长一个字符。即额外的字符 `'\0'`。

以下字符串声明都是等价的：

```c
char* str = "hello world";
char str[12] = "hello world";
char str[] = "hello world";
```

## 文件格式化输入

`fscanf` 函数从文本文件中读取数据并将数据放入变量中。文件中的数据元素必须用空格分隔。如果发生错误或尝试读取文件末尾，`fscanf` 将返回 `EOF`。这是一个示例：

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    char name[1024];
    float length;
    int mass;

    fp = fopen("animals.txt", "r");
    while (fcanf(fp, "%s %f %d", name, &length, &mass) != EOF)
        printf("%s animal, %d lbs, %.1f meters\n", name, mass, length);

    fclose(fp);
}
```

## 写入文件

我们使用 `fopen("filename", "w")` 打开一个文件进行写入。如果文件已存在，它将被截断为长度 0。

文件读取函数 `getc`、`fgets` 和 `fscanf` 有对应的文件写入函数：`fputc`、`fputs` 和 `fprintf`。我们如下所示使用这些函数：

```c
#include <stdio.h>

int main(void)
{
    FILE *fp;
    int x = 32;

    fp = fopen("output.txt", "w");
    fputs('B', fp);
    fputc('\n', fp);
    fprintf(fp, "x = %d\n", x);
    fputs("Hello, world!\n", fp);

    fclose(fp);
}
```

注意，由于 `stdout` 是指向 `FILE` 的指针，我们可以执行 `f = stdout`。

## 二进制文件

二进制文件的工作原理与文本文件非常相似，但 I/O 子系统不会对数据进行像文本文件那样的转换。对于二进制文件，我们得到原始字节流，它不会被 I/O 子系统转换。

要以二进制模式打开文件，我们在文件模式中添加 `'b'`（`'rb'` 或 `'wb'`）。最常用的函数是 `fread()` 和 `fwrite()`。这些函数从文件流读取或向其写入指定数量的字节。

## C 语言：内存分配

`C` 语言使用 `malloc()` 函数来分配内存。`malloc()` 将分配的字节数作为其唯一参数，并返回指向新分配连续内存块的 `void` 指针。`void` 类型指针可以转换为任何其他类型。如果无法分配内存，`malloc()` 返回 `NULL`。`malloc` 不初始化新分配的内存。

在我们完成内存的使用后，使用 `free()` 释放内存。这是一个示例：

```c
#include <stdlib>
// 从 void* 到 int* 的隐式类型转换
int *p = malloc(sizeof(int));
*p = 12;

printf("%d\n", *p);
free(p);
```

`calloc()` 与 `malloc()` 类似。它接收单个元素的大小和分配的元素个数。`calloc()` 将分配的内存初始化为 ASCII 空 字节（`"\0"`）。

```c
#include <stdlib>
int *p = calloc(sizeof(int), 10);
...
free(p);
```

`realloc()` 函数可用于缩小或扩大已分配的内存。`realloc` 接收指向已分配内存的指针和新内存分配的大小。它会扩大或缩小内存，并返回指向它的 `void` 指针。

```c
float *p = malloc(40);   // 分配 40 字节
...
float *new_p = realloc(p, 80);
```

## C 语言：存储类限定符

存储类限定符告诉编译器如何存储变量。`C` 语言有四种存储类限定符：

- `extern`
- `static`
- `register`
- `auto`

带有存储类限定符的变量声明方式如下：

```c
storage_class_specifier type variable_name;
```

### extern

`C` 和 `C++` 允许将大型程序拆分为多个文件，并对这些文件进行单独编译，然后链接在一起。由于由于，必须有一种方法告诉一个文件在其他文件中声明的变量。

变量声明声明了变量的名字和类型。变量定义会为变量分配存储。在大多数情况下，变量声明和定义是结合在一起的（例如 `int x = 5`）。但当我们在变量声明之前加上 `extern` 限定符时，我们告知编译器该变量是在另一个文件中声明的。

`extern` 的一个显著用法是在一个一个文件中声明所有的全局变量，并在其他文件中使用 `extern` 声明来访问这些变量。

示例：

文件 1

文件 2

```c
int x, y;           extern int x, y;
```

`extern` 限定符告诉编译器紧随其后的变量名已经在其他文件中声明过。换句话说，`extern` 让编译器知道这些全局变量的类型和名称，而无需再次为它们创建存储。当链接器链接两个目标文件时，所有对外部变量的引用都会被解析。

`extern` 关键字具有这种通用形式：

```c
extern type variable_name;
```

### 静态变量

与全局变量不同，静态变量在声明它的函数或文件外部是不可知的。此外，在函数内部声明的静态变量在函数调用之间保持其值。

#### 函数内部的静态变量

函数内部的静态局部变量在函数调用之间保留其值。

这是一个示例：

```c
int series(void)
{
    static int series_num;
    series_num = series_num+23;
    return series_num;
}
```

静态局部变量在函数调用之间保留其值。

#### 静态全局变量

将 `static` 限定符应用于变量，告知编译器该变量仅在声明它的文件中可见。
