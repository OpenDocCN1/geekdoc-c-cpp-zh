

```c
#include <stdio.h>

void main (void) {
    FILE *fp;
    int value;

    fp = fopen("/home/pi/input.txt", "rb");
    if (fp != NULL) {
        fseek(fp, 10, SEEK_CUR);
        while (1) {
            value = getc(fp);
            if (value == EOF) break;
            else printf("%c", value);
        }
        fclose(fp);
    }
}
```

`fseek(fp, 10, SEEK_CUR)` 将文件指针向当前位置向前移动10个字节，此程序将打印文件中所有的前十个字符。fseek 的第一个参数是文件指针，第二个是指针移动的偏移量。这可以是正数也可以负数：`fseek(fp, -5, SEEK_CUR)` 将指针从当前位置向后移动5个字节。

fseek 的第三个参数允许你选择相对于文件开头（SEEK_SET）或文件末尾（SEEK_END）的位置，而不是相对于当前位置（SEEK_CUR）。因此，`fseek(fp, 12, SEEK_SET)` 将指针置于文件开头12个字节处，而 `fseek(fp, -17, SEEK_END)` 将其置于文件末尾后17个字节处。

## 检查库

该库提供了许多用于读写文件数据的函数，我们刚刚查看了其中一些。如果你需要访问文件，请查看库的其他函数，例如 `fread`、`write`、`fputs`、`sscanf`、`gets`，看看它们是否比我们在这里使用的基本 `fputc` 和 `getc` 更合适。

## 第11章

## 关于类型和变量的更多

全局变量、类型定义、枚举和结构

在本章中，我们将介绍关于变量和类型使用的一些高级主题，包括局部变量和全局变量之间的区别、定义新类型以及枚举和数据结构的使用。

当我们在书中示例中使用变量时，总是将它们放在函数定义内部。因此，这些是局部变量；也就是说，变量仅限于这些函数，并且在函数外部没有意义。

## 全局变量

C 还允许使用全局变量，即定义在所有函数之外的变量。它们具有全局作用域，这意味着可以在程序内的任何函数中进行读取和写入。让我们来看一个示例：

```c
#include <stdio.h>

int result;

void add(int a, int b)
{
    result = a + b;
}

void main(void)
{
    add(3, 4);
    printf("The result is %d\n", result);
}
```

在这个示例中，变量 `result` 是全局的。因此，可以在 `add` 函数和 `main` 函数中对其进行读取或写入。如你所见，我们在 `add` 中对其写入一个值并在 `main` 中将其读取，因此我们不需要从 `add` 返回值。

在某些方面，这看起来比到处传递值要简单，不是吗？那么为什么不一直这样做呢？答案是内存。函数中的局部变量在函数运行时分配空间，并在函数结束时释放内存。但全局变量在程序启动时分配空间，该空间直到程序结束才会被释放，如果你分配了足够的全局变量，可能会耗尽系统内存。

有一种更好的方法可以让每个函数都能访问大量数据，我们稍后会介绍……

## 不同的名称

虽然在同一个程序中给局部变量和全局变量起相同的名称是完全有效的，但不是吗？如果你有一个同名的全局变量和局部变量，局部变量将在声明它的函数中使用，而全局变量将在任何可以使用的地方被使用，这可能会导致意料之外的行为。

## 类型定义

在第2章中，我们查看了C语言变量类型的范围：`char`、`int`、`float` 等。C 还允许你通过所谓的 `typedef` 来定义自己的类型。`typedef` 是一种格式为 `typedef <现有类型> <新名称>` 的行，通常放在程序的开头。例如：

```c
typedef unsigned char BYTE;
```

这定义了一个名为 `BYTE` 的新类型，它是 `unsigned char` 的另一个名称（注意，按照习惯，用户定义的类型通常使用大写字母命名。这并不是强制的，但在阅读代码时有助于将它们与变量区分开）。

当我们定义一个新类型时，它实际上是为现有类型创建一个别名。这看起来似乎没什么意义，但它可以从两个方面提供帮助。首先，如果你让类型名称针对你的程序数据，它可以让你的代码行为变得更加直观。其次，通过定义特定类型，你可以让编译器在函数参数或变量使用错误的类型时向你发出警告。

在某些特定情况下，`typedef` 特别有用：这些是枚举类型数据结构。

## 枚举类型

通常，某些变量只能取少数几个值中的一个。C提供了一种名为 `enum` 的类型用于此，它定义了一个具有固定一组命名值的整数。

这里有一个示例：

```c
#include <stdio.h>

typedef enum {
    false,
    true
} BOOLEAN;

void main (void) {
    BOOLEAN b_var = false;

    if (b_var == true) {
        printf("TRUE\n");
    } else {
        printf("FALSE\n");
    }
}
```

如你所示，使用了命名值而不是数字。这可以使代码变得更容易。

### 编号枚举

使用 `typedef` 的另一个有用方法是用于定义结构

### 结构

使用 `typedef` 的另一个有用方法是用于定义数据结构。这是一个组合在一起的变量集合，允许你传递整个结构而不是单个变量。这里有一个示例：

```c
#include <stdio.h>

typedef struct {
    int inval1;
    int inval2;
    int outval;
} MY_DATA;

void add (MY_DATA *d)
{
    d->outval = d->inval1 + d->inval2;
}

void main (void)
{
    MY_DATA data;

    data.inval1 = 5;
    data.inval2 = 7;
    add(&data);

    printf("The sum of %d and %d is %d\n", data.inval1, data.inval2, data.outval);
}
```

结构可以包含其他类型（基本类型、枚举甚至是结构），只需确保在包含它们的结构 `typedef` 之前出现这些类型的 `typedef` 即可。

## C 语言与 GUI 编程简介

```
File Edit Tabs Help
pi@raspberrypi: 5 ./myprog
The sum of 5 and 7 is 12
pi@raspberrypi: 6
```

* 除非用户想要添加，否则所有的 MYDATA 实例都是唯一的

