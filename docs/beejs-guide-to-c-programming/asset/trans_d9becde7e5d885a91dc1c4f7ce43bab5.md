

## 第 32 章 类型第 V 部分：复合字面量与泛型选择

float f;
char c;

```c
char *s = _Generic(i,
int: "that variable is an int",
float: "that variable is a float",
default: "that variable is some type"
);
printf("%s\n", s);
```

查看从第 9 行开始的 _Generic_ 表达式。
当编译器看到它时，它会查看第一个参数的类型（在本例中，是变量 `i` 的类型）。它遍历所有分支以寻找该类型。然后用参数替换整个 `_Generic` 表达式。

在这种情况下，`i` 是一个 `int`，所以它匹配了该分支。字符串被替换了表达式。因此，当编译器看到这一行变为：

```c
char *s = "that variable is an int"
```

如果编译器在 `_Generic` 中找不到匹配项，它会寻找可选的 `default` 情况并使用它。
如果找不到匹配项且没有 `default`，你将得到编译错误。第一个表达式必须匹配其中一种类型或 `default`。

由于反复编写 `_Generic` 非常不方便，它通常用于构建宏的体。
让我们定义一个宏 `TYPESTR(x)`，它接受一个参数并返回一个包含该参数类型的字符串。

例如，`TYPESTR(1)` 将返回字符串 "int"。

我们开始吧：

```c
#include <stdio.h>

#define TYPESTR(x) _Generic((x), \
int: "int", \
long: "long", \
float: "float", \
double: "double", \
default: "something else")

int main(void) 
{
    int i;
    long l;
    float f;
    double d;
    char c;

    printf("i is type %s\n", TYPESTR(i));
    printf("l is type %s\n", TYPESTR(l));
    printf("f is type %s\n", TYPESTR(f));
    printf("d is type %s\n", TYPESTR(d));
    printf("c is type %s\n", TYPESTR(c));
}
```

输出如下：

```
i is type int
l is type long
f is type float
d is type double
c is type something else
```

这并不意外，因为正如我们所说，`main()` 函数中的那些代码在编译时被替换为了以下内容：

```c
printf("i %s\n", "int");
printf("l %s\n", "long");
printf("f %s\n", "float");
printf("d %s\n", "double");
printf("c %s\n", "something else");
```

这正是我们看到的输出。

再再来一个。我包含了一些宏，以便当你运行：：

```c
int i = 10;
char *s = "Foo";
PRINT_VAL(i);
PRINT_VAL(s);
```

你会得到输出：

```
i = 10
s = Foo!
```

我们需要利用一些宏的魔法来实现这一点。

```c
#include <stdio.h>
#include <string.h>

// 返回类型对应格式化符的宏
#define FMTSPEC(x) _Generic((x), \
int: "%d", \
long: "%ld", \
float: "%f", \
double: "%f", \
char: "%s", \
// TODO: 添加更多类型)

// 以 "变量名 = 值" 形式打印变量的宏
#define PRINT_VAL(x) do { \
    char fmt[512]; \
    snprintf(fmt, sizeof(fmt), "%x = %s\n", FMTSPEC(x)); \
    printf(fmt, (x)); \
} while(0)

int main(void)
{
    int i = 10;
    float f = 3.14159;
    char *s = "Hello, world!";

    PRINT_VAL(i);
    PRINT_VAL(f);
    PRINT_VAL(s);
}
```

输出为：
```
i = 10
f = 3.141590
s = Hello, world!
```

我们可以把它们全部挤在一个大宏里，但为了防止视觉疲劳，我把它分成了两个。

## 第 33 章

## 数组第二部分

在本章中，我们将介绍关于数组的一些额外杂项内容。

- 数组参数中的类型限定符
- 数组参数中的 `static` 关键字
- 部分多维数组的初始化器

它们并不非常常见，但由于它们是新版规范的一部分，我们会窥探一下。

### 33.1 参数列表中数组的类型限定符

如果你还记得早些时候的内容，这两者在函数参数列表中的功能是等价的：

```c
int func(int p) {......}
int func(int p[]) {......}
```

你可能还记得可以这样为指针变量添加限定符：

```c
int const p;
int volatile p;
int const volatile p;
// 等等
```

但当我们使用数组表示法时该怎么做？（等等，这里的 OCR 文本似乎有点乱码，让我们根据上下文进行重构）：
但当我们在参数列表中使用数组表示法时该怎么做？结果是它放在括号里。以下行是等价的：

```c
int func(int volatile p) {......}
int func(int const p[]) {......}
int func(int const volatile p[]) {......}
```

如果你有一个多维数组，需要在第一组括号中使用类型限定符。

### 33.2 参数列表中的 static

同样，你可以在数组参数列表中使用 `static` 关键字。我从未在实际中见过。它总是紧跟在之后：

```c
int func(int static p[]) {......}
```

任何其他都是未定义行为。

```c
int func(int static p[]) {}

int main(void)
{
    int a[] = {11, 22};
    int b[] = {11, 22, 33, 44};
    int c[] = {11, 22};
}
```

注意：编译器并没有禁止你传递较小的数组。编译器可能不会警告，也不会在运行时检测到。通过在那里放置 `static`，你说：“我不会传递更小的数组。”而编译器说：“好的，”并信任你会正确处理。

### 33.3 等价初始化器

在初始化器方面，C 相当灵活。我们已经见过一些缺失值被替换为 0 的情况。例如，我们可以用这种方式将 5 元素的数组初始化为 1, 2, 0, 0, 0：

```c
int a[5] = {1, 2};
```

或者用这种方式将整个数组置零：

```c
int a[5] = {0};
```

但在初始化多维数组时情况变得有趣。让我们创建一个 3 行 2 列的数组：

```c
int a[3][2];
```

写一些代码来初始化它并打印结果：

```c
#include <stdio.h>

int main(void)
{
    int a[3][2] = {
        {1, 2},
        {3, 4},
        {5, 6}
    };
}
```

当我们运行它，得到了预期的结果：

```
1 2
3 4
5 6
```

留下一些初始化元素，看看它们是如何被设置为零的：

```c
int a[3][2] = {
    {1, 2},
    {3}, // 留下了 4
    {5, 6}
};
```

产生：

```
1 2
3 0
5 6
```

现在留下整个中间的元素：

```c
int a[3][2] = {
    {1, 2},
    // {3, 4}, // 直接删掉这个
    {5, 6}
};
```

现在我们得到了这个，这可能不是你预期的：

```
1 2
5 6
0 0
```

但如果你停止思考它，我们提供了足够的初始化器，所以它们被用于前两行。剩余元素被初始化为 0。

到目前为止良好。通常情况下，如果我们漏掉了初始化器的部分，编译器会将相应的元素设置为 0。但让我们疯狂一下。

```c
int a[3][2] = { 1, 2, 3, 4, 5, 6 };
```

这是一个二维数组，但它只有一个一维初始化器！结果证明这是合法的（尽管如果开启了相应的警告，GCC 会警告你）。基本上，它做的是从左到右填充第 0 行、然后是第 1 行、第 2 行的元素。所以当我们打印时，它是按顺序打印的：

```
1 2
3 4
5 6
```

如果我们漏掉了一些：

```c
int a[3][2] = { 1, 2, 3 };
```

它们会填零：

```
1 2
3 0
0 0
```

所以如果你想用 `{}` 填充整个数组，尽管去做：

```c
int a[3][2] = {0};
```

但我的建议是如果你有一个二维数组，使用二维初始化器。这会让代码更具可读性。（除了用 `{}` 初始化整个数组，那时无论数组维度如何，使用 `{}` 都是惯例。）

## 第 34 章

## 使用 setjmp, longjmp 进行长跳转

我们已经见过了 `goto`，它在函数作用范围内跳转。`longjmp()` 允许你跳回执行早早点，回到调用它的函数。有很多限制和注意事项，但它可以作为一个从调用栈深处退出回到早早状态的有用函数。根据我的经验，这是一个很少使用的功能。

### 34.1 使用 setjmp 和 longjmp

我们在这里要做的“舞蹈”基本上是用 `setjmp()` 在执行中放置一个标记。稍后，我们会调用 `longjmp()`，它跳回到我们用 `setjmp()` 设置标记的执行早早点。如果你调用了子函数，它可以做到。

这里有一个快速演示，我们调用了深几层的函数然后退出。我们将使用一个文件变量 `env` 来保存 `setjmp()` 时的状态，以便在调用 `longjmp()` 时恢复它们。这就是我们记录“位置”的变量。

变量 `env` 是 `jmp_buf`，这是一个在 `<setjmp.h>` 中声明的不透明类型。

```c
#include <stdio.h>
#include <setjmp.h>
jmp_buf env;
void depth2(void)
{
    printf("Entering depth 2\n");
    longjmp(env, 3490); // 退出
    printf("Leaving depth 2\n"); // 这不会发生
}
void depth1(void)
{
    printf("Entering depth 1\n");
    depth2();
    printf("Leaving depth 1\n"); // 这不会发生
}
```

