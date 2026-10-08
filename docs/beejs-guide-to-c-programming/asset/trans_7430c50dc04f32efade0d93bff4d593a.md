

# 第 30 章

# 变长数组 (VLAs)

C 语言提供了一种声明其大小在运行时确定的数组的方法。这让你拥有了类似于使用 `malloc()` 那样的动态运行时调整的优势，但不需要担心之后要 `free()` 释放内存。

现在，许多人并不喜欢 VLAs。例如，它们在 Linux 内核中被禁止使用了。我们稍后会深入探讨背后的原理。

这是该语言的一个可选特性。如果不存在 VLAs，宏 `__STC_NO_VLA__` 会设置为 1（它们在 C99 中是强制性的，但在 C11 中变为可选的了）。

```c
#if __STC_NO_VLA__ == 1
  #error Sorry, need VLAs for this program!
#endif
```

但由于 GCC 和 Clang 都没有懒得定义这个宏，你可能从中获益有限。让我们先看一个例子，然后我们再寻找细节中的“魔鬼”。

## 30.1 基础知识

普通数组使用常量大小声明，如下：

```c
int v[10];
```

使用 VLA，我们可以使用运行时确定的尺寸来设置数组，如下：

```c
int n = 10;
int v[n];
```

现在，这看起来是一样的，在很多方面也确实如此，但它给了你灵活性来计算所需的大小，然后获取一个完全相同大小的数组。

让我们让用户输入数组的大小，然后在每个数组元素中存储“索引乘以 10”的值：

```c
#include <stdio.h>

int main(void)
{
  int n;

  printf("Enter a number: "); fflush(stdout);
  scanf("%d", &n);

  int v[n];

  for (int i = 0; i < n; i++)
    v[i] = i * 10;

  for (int i = 0; i < n; i++)
    printf("%d] = %d\n", i, v[i]);
}
```

（在第 7 行，我使用了 `fflush()`）这强制了该行输出，尽管我在末尾没有换行符。）

第 10 行是 VLA 所在——一旦执行过了这一行，数组的大小就被设置为运行时 `n` 的任何值。该数组无法被更改。

你也可以在括号中放入表达式：
`int v[x * 100];`

- 你不能在文件作用域声明 VLA，也不能在块作用域内创建静态 VLA。
- 你不能使用初始化列表来初始化数组。

此外，为数组大小输入负值会导致未定义行为——至少在这种情况下如此。

## 30.2 sizeof 和 VLAs

我们习惯于使用 `sizeof` 获取任何特定对象（包括数组）的字节大小。VLAs 也不例外。主要区别在于 VLA 上的 `sizeof` 是在运行时计算的，而在非变长变量上它是在编译时计算的。*但用法是一样的。*

你甚至可以使用常用的技巧计算 VLA 中的元素个数：`size_t num_elems = sizeof(v) / sizeof(v[0]);`

从上面的行可以得出一个微妙且正确的暗示：指针算术的工作方式就像你对普通数组的预期一样。所以尽情使用它吧：

```c
#include <stdio.h>

int main(void)
{
    int n = 5;
    int v[n];

    int *p = v;

    *(p+2) = 12;
    printf("%d\n", v[2]); // 12
}
```

*这是因为 VLAs 通常在栈上分配，而且 VLAs 的核心思想是它们会在函数结束时自动释放内存。*

像普通数组一样，你可以使用括号配合 `sizeof()` 来声明一个变量：

```c
int x = 12;
printf("%zu\n", sizeof(x)); // 在我的系统中输出 48
```

## 30.3 多维 VLAs

你可以创建一个或多个维度设置为变量的 VLA：

```c
int w = 10;
int h = 20;
int x[h][w];
int y[5][w];
int z[10][w];
```

同样，你可以像处理普通数组一样处理这些。

## 30.4 向函数传递一维 VLAs

向函数传递一维 VLA 与传递普通数组没有区别：

```c
#include <stdio.h>

int sum(int count, int v[])
{
  int total = 0;

  for (int i = 0; i < count; i++)
    total += v[i];

  return total;
}

int main(void)
{
  int a = 5;
  int x[5]; // 标准数组
  int y[a];  // VLA

  for (int i = 0; i < a; i++)
    x[i] = i + 1;

  printf("%d\n", sum(5, x));
  printf("%d\n", sum(a, y));
}
```

还有一点，你可以通过在参数列表中传递维度来告诉 C 语言数组是一个特定的 VLA 大：

VLA 原型：
```c
void do_something(int count, int v[count]); // 有名称
void do_something(int count, int v[]); // 无名称
```

同样，只有在原型中有效——在函数内部，你必须显式指定大小。现在进入多维情况！乐趣开始了。

## 30.5 向函数传递多维 VLAs

与你上面处理一维 VLA 的一样，但这次我们传递两个维度并使用它们。在下面的示例中，我们构建了一个宽度和高度可乘法表，并将其传递给函数打印。

```c
#include <stdio.h>

void print_matrix(int h, int w, int m[h][w]) {
    for (int row = 0; row < h; row++) {
        for (int col = 0; col < w; col++) {
            printf("%d ", m[row][col]);
        }
        printf("\n");
    }
}

int main(void)
{
    int rows = 4;
    int cols = 7;

    int matrix[rows][cols];

    for (int row = 0; row < rows; row++) {
        for (int col = 0; col < cols; col++) {
            matrix[row][col] = row * col;
        }
    }

    print_matrix(rows, cols, matrix);
}
```

### 30.5.1 部分多维 VLAs

你可以让某些维度固定，而某些维度为变量。假设我们有一个长度固定为 5 个元素的记录，但我们不知道有多少记录。

## 30.6 与普通数组的兼容性

由于 VLAs 在内存中与普通数组一样，只要维度匹配，相互传递它们是完全允许的。例如，如果我们有一个专门想要 3×5 数组的函数，我们仍然可以它传递一个 VLA。

```c
int foo(int m[5][3]) {
    ...
}

int w = 3, h = 5;
int matrix[h][w];

foo(matrix); // OK!

int foo(int h, int w, int m[h][w]) {
    ...
}

int matrix[3][5];

foo(3, 5, matrix); // OK!
```

同样，如果你有一个 VLA 函数，你可以向它传递一个普通数组：但注意：如果维度不匹配，可能会出现某些未定义行为。

## 30.7 typedef VLAs

你可以对 VLA 进行 `typedef`，但行为可能不像你预期的那样。基本上，`typedef` 会根据执行 `typedef` 瞬间存在的值创建一个新类型。所以，它与其说是对 VLA 的 `typedef`，不如说是执行当时的维度的固定大小数组。

```c
#include <stdio.h>

int main(void)
{
    int w = 10;

    typedef int[w];

    // goat 是一个包含 10 个整数的数组
    goat x;

    // 用平方初始化
    for (int i = 0; i < w; i++)
        x[i] = i*i;

    // 打印它们
    for (int i = 0; i < w; i++)
        printf("%d\n", x[i]);

    // 现在让我们改变 w...
    w = 20;

    // 但 goat 仍然是一个 10 个整数的数组，因为那是
    // 执行 typedef 时 w 的值。
}
```

所以它的行为就像固定大小的数组。但仍然不能对其使用初始化列表。

## 30.8 跳跳转陷阱

在 VLA 附近使用 `goto` 时，你必须小心，因为很多操作是不合法的。当你使用 `longjmp()` 时，有一种情况你会因为 VLA 导致内存泄漏。但这两个问题我们将在各自的章节中介绍。

## 30.9 通用问题

VLAs 在 Linux 内核中被禁止有几个原因：

- 许多使用它们的地方应该是固定大小的。
- VLAs 背后的代码运行速度较慢（大多数人会注意到的程度，但在操作系统中会有影响）。
- 并不是所有的 C 编译器的支持程度相同。
- 栈空间是有限的，而 VLAs 位于栈上。如果某些代码无意中（或恶意地）向分配 VLA 的内核函数传递一个大值，可能会发生 _坏事™_。

