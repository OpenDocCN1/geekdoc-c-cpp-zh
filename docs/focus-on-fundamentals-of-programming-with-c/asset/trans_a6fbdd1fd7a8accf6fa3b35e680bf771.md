
在 main() 中，原始命令行上的值现在可以像任何其他变量一样被访问和使用。我们稍后将看到，还可以从命令行向 main() 传递文件名，并打开和访问文件的内容。下面的程序只是将其命令行参数回显到终端窗口：

```
// echo1.c

#include <stdio.h>

int main(int argc, char *argv[]) {
    int i;
    for(i = 0; i < argc; i++) {
        printf("%s ", argv[i]);
    }
    printf("\n");
    return 0;
}
```

由于 argv 是指向指针数组的指针，我们可以不使用数组索引来重写上面的程序：

```
// echo2.c

#include <stdio.h>

int main(int argc, char *argv[]) {
    while(--argc > 0) {
        printf("%s ", *++argv);
    }
    printf("\n");
}
```

由于 argv 是指向参数字符串数组开头的指针，将其加 1（即 ++argv）会使其指向 argv[1] 而不是 argv[0]。每次后续迭代都会将其移动到下一个参数。*argv 此时即为该参数的指针。当 argc 变为 0 时，表示不再有剩余参数。

```
// caps.c

#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

int main(int argc, char *argv[]) {
    int c;
    FILE *fp;

    if (!(fp = fopen(argv[1], "r"))) {
        puts("Could not open file. ");
        exit(1);
    }

    while((c = getc(fp)) != EOF) {
        if(islower(c)) {
            putchar(toupper(c));
        } else {
            putchar(c);
        }
    }

    return 0;
}
```

我们的最后一个示例展示了如何使用标志来修改命令。标志通常由连字符引导，并在命令行中作为第二个参数出现。下面的程序将输出其命令行参数，如果存在标志 -c，则参数将以大写字母输出；否则，参数将按其在命令行中出现的形式输出。请注意，包含标志的参数不会被输出。

```
// flag.c

#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
    int i = 1, flag = 0;

    if (!strcmp(argv[1], "-c")) {
        flag = 1;
        i = 2;
    }
    for ( ; i < argc; ++i) {
        if (flag) {
            strupr(argv[i]);
            printf("%s ", argv[i]);
        }
    }
    printf("\n");
    return 0;
}
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_352_0.png)

## 可变长度参数列表 - 高级

可以创建接收不特定数量参数的函数！事实上，printf() 接收可变数量的参数。至少，printf() 必须将字符串作为其第一个参数，但可以接收任意数量的其他参数。printf() 的实际函数原型为：

```
int printf(char *fmt, ...);
```

声明 ...（省略号）表示这些参数的数量和类型可能会变化。函数可以接收任意类型的可变数量的参数。此声明只能出现在参数列表的末尾。

声明带有可变数量参数的函数可以为我们提供极大的灵活性。考虑一个名为 average() 的函数，它可以计算可变数量参数的平均值。它可能会以如下方式调用：

```
avg = average(a, b, c);
avg = average(a, b, c, d);
```

在 C 中处理可变数量参数的秘诀在于参数传递给函数的方式。让我们来看看 C 函数进入时栈的内容。当调用函数时，参数后跟返回地址会被放置在栈上：

```
foo(arg1, arg2);

high addresses
+-----------+
|   arg2    |
+-----------+
|   arg1    |
+-----------+
| return address |
sp-> +-----------+
     |           |
     | stack     |
     | grows     |
     | downward  |
     |           |
     +-----------+
low addresses
```

在 C 中，函数的参数按其在函数调用中出现的相反顺序放置在栈上。结果是，第一个参数始终位于栈指针 sp 的固定偏移处。该偏移是存储返回地址所需的字节数。因此，无论向 C 函数传递多少个参数，第一个参数始终很容易访问。

因此，当进入 C 函数时，第一个参数出现在返回地址上方的栈上，即它具有下一个更高的地址。其他参数具有依次更高的地址。因此，如果你能访问栈上的第一个参数，并且知道所有其他参数的大小，那么你就可以逐个检索参数！

有一个标准 C 头文件 <stdarg.h>，它包含一组宏以及一种新定义的数据类型，使处理可变数量参数的任务变得简单直接。该头文件的实现因机器而异，但它提供的接口是统一的。stdarg.h 包含的第一件事是一种新数据类型的定义：

```
va_list
```

它用于声明一个变量，该变量将依次引用每个参数：

```
va_list ap;
```

我们将 ap 声明为 va_list 类型的参数指针。ap 将由其他宏用于处理可变长度参数列表，即 ap 将依次指向每个参数。

va_start 是一个宏，它初始化参数指针 ap，使其指向传递给函数的栈上的第一个未命名参数。在使用 ap 访问任何未命名参数之前，必须先调用一次 va_start。va_start 的原型为：

```
void va_start(va_list ap, lastarg);
```

第一个参数 ap 是参数指针。第二个参数 lastarg 是传递给被调用函数的最后一个固定函数参数的名称。这是参数列表中省略号 (...) 之前的最右侧参数。请注意，函数必须至少有一个命名参数。va_arg 是一个宏，它将参数指针 ap 推进到栈上的下一个参数。第一次使用 va_arg 时，它返回列表中的第一个参数。每次后续使用 va_arg 时，它返回列表中的下一个参数。它通过先解引用 ap，然后递增 ap 以指向下一个项目来实现这一点。

va_arg 的原型为：

```
type va_arg(va_list ap, type);
```

第一个参数 ap 是参数指针。第二个参数 type 表示参数列表中预期值的类型，例如 int、double 等。请注意，不能使用 char、unsigned char 或 float。va_arg 使用 type 既执行解引用以确定返回什么类型，又确定采取多大的步长来定位栈上的下一个参数。该宏返回参数类型的值。

va_end 是一个宏，它执行必要的清理操作，以帮助被调用函数执行正常返回。它必须在 va_arg 读取所有参数之后且在函数返回之前调用。如果不这样做，可能会导致程序出现奇怪的未定义行为。va_end 的原型如下：

```
void va_end(va_list ap);
```

参数 ap 是参数指针。

下面的程序返回一系列数字的平均值。average() 函数的第一个参数始终是要平均的值的数量：

```
// arg1.c

#include <stdio.h>
#include <stdarg.h>

int main(void);
double average(int num, ...);

int main(void) {
    double a = 2.0, b = 4.0, c = 6.0, d = 8.0;

    printf("%5.1f\n", average(2, a, b));
    printf("%5.1f\n", average(3, a, b, c));
    printf("%5.1f\n", average(4, a, b, c, d));
    return 0;
}

double average(int num, ...) {
    int i;

    double total = 0.0;

    va_list ap;

    va_start(ap, num);
    for(i = 1; i <= num; i++) {
        total += va_arg(ap, double);
    }
    va_end(ap);

    return total / num;
}
