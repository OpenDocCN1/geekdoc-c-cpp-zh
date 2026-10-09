
## 第七章 循环

**while** 结构与 **if** 结构类似，但有一个主要区别：在 **if** 结构中，如果表达式为真，代码块只运行一次。而在 **while** 结构中，代码块会反复运行，直到表达式变为假。

将 **main()** 函数重写为以下形式：

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int i = 0;
    while (i < 12) {
        printf("%d. Aaron is Cool\n", i);
        i++;
    }
    return 0;
}
```

构建并运行程序。

条件（`i < 12`）在代码块每次执行之前都会进行检查。第一次当它评估为假时，执行将跳转到代码块之后的代码。

请注意，代码块的第二行增加了 `i` 的值。这很重要。如果没有增加 `i`，那么按照当前写法，这个循环将永远持续下去，因为表达式将始终为真。下面是这个 while 循环的流程图：

![](img/5f9368899ebf8d92fc145f8def1e89f8_60_0.png)

### for 循环

**while** 循环是一种通用的循环结构，但 C 程序员经常使用相同的基本模式：`一些初始化 while (一些检查) { 一些代码 一些最后一步 }`

因此，C 语言提供了一种快捷方式：**for** 循环。在 **for** 循环中，上述模式变为：

```c
for (一些初始化; 一些检查; 一些最后一步) {
    一些代码;
}
```

将程序修改为使用 **for** 循环：

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    for (int i = 0; i < 12; i++) {
        printf("%d. Aaron is Cool\n", i);
    }
    return 0;
}
```

**图 7.2 for 循环**

![](img/5f9368899ebf8d92fc145f8def1e89f8_61_0.png)

注意，在这个简单的循环示例中，你使用循环来规定某事发生的次数。然而，更常见的情况是，循环被用来*遍历*一组项目，例如一个姓名列表。例如，我可以修改此程序，使其结合朋友姓名列表使用循环。每次循环时，不同的朋友都会变得“酷”。从第 15 章开始，我们将看到更多关于集合和循环的内容。

### break

有时需要从循环内部停止循环的执行。例如，假设你想遍历正整数以寻找数字 *x*，其中 *x + 90 = x²*。你的计划是遍历 0 到 11 的整数，并在找到解决方案时跳出循环。修改代码：

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int i;
    for (i = 0; i < 12; i++) {
        printf("Checking i = %d\n", i);
        if (i + 90 == i * i) {
            break;
        }
    }
    printf("The answer is %d.\n", i);
    return 0;
}
```

构建并运行程序。你应该看到：

```text
Checking i = 0
Checking i = 1
Checking i = 2
Checking i = 3
Checking i = 4
Checking i = 5
Checking i = 6
Checking i = 7
Checking i = 8
Checking i = 9
Checking i = 10
The answer is 10.
```

请注意，当调用 **break** 时，执行直接跳过代码块的剩余部分。

**图 7.3 跳出循环**

![](img/5f9368899ebf8d92fc145f8def1e89f8_62_0.png)

### continue

有时你会发现自己处于代码块的中间，需要说：“忘记这次代码块执行的其余部分，开始下一次代码块执行。” 这是通过 **continue** 命令完成的。例如，如果你相当确定 3 的倍数不满足方程怎么办？你如何避免浪费宝贵的时间去检查它们？

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int i;
    for (i = 0; i < 12; i++) {
        if (i % 3 == 0) {
            continue;
        }
        printf("Checking i = %d\n", i);
        if (i + 90 == i * i) {
            break;
        }
    }
    printf("The answer is %d.\n", i);
    return 0;
}
```

构建并运行它：

```text
Checking i = 1
Checking i = 2
Checking i = 4
Checking i = 5
Checking i = 7
Checking i = 8
Checking i = 10
The answer is 10.
```

![](img/5f9368899ebf8d92fc145f8def1e89f8_63_0.png)

### do-while 循环

没有酷孩子使用 **do-while** 循环，但为了完整性，这里介绍它。**do-while** 循环在执行为代码块之前不检查表达式。因此，它确保代码块至少执行一次。如果你重写最初的练习以使用 **do-while** 循环，它看起来像这样：

```c
int main(int argc, const char * argv[]) 
{
    int i = 0;
    do {
        printf("%d. Aaron is Cool\n", i);
        i++;
    } while (i < 13);
    return 0;
}
```

注意末尾的分号。这是因为与其他循环不同，**do-while** 循环实际上是一个长的语句：

```text
do { something } while ( something else stays true );
```

下面是这个 do-while 循环的流程图：

![](img/5f9368899ebf8d92fc145f8def1e89f8_64_0.png)

### 挑战

编写一个程序，从 99 倒数到 0，步长为 3，打印每个数字。但是，如果该数字能被 5 整除，还应该打印单词“Found one!”。因此，输出应该看起来像这样：

```text
99
96
93
90
Found one!
87
...
0
Found one!
```

## 地址和指针

你的电脑核心是一个处理器（中央处理器或 CPU）和一片巨大的开关草地（随机访问内存或 RAM），这些开关可以被处理器打开或关闭。我们说一个开关保存一个*比特*的信息。你经常会看到 1 用来表示“开”，0 用来表示“关。”

八个这样的开关构成一个*字节*的信息。处理器可以获取这些开关的状态，对比特位进行操作，并将结果存储在另一组开关中。例如，处理器可能从某处获取一个字节，从另一处获取另一个字节，将它们相加，并将结果存储在遥远的某个地方的一个字节中。

![](img/5f9368899ebf8d92fc145f8def1e89f8_65_0.png)

内存是经过编号的，我们通常谈论特定数据字节的*地址*。当人们谈论 32 位 CPU 或 64 位 CPU 时，他们通常指的是地址的大小。64 位 CPU 可以处理的内存远比 32 位 CPU 多。

### 获取地址

在 Xcode 中创建一个新的项目：一个名为 **Addresses** 的 C 命令行工具。

变量的地址是存储该变量值的内存位置。要获取变量的地址，你需要使用 `&` 运算符：

```c
#include <stdio.h>

int main(int argc, const char * argv[])
{
    int i = 17;
    printf("i stores its value at %p\n", &i);
    return 0;
}
```

注意 `%p` 标记。这是你可以用内存地址替换的标记。构建并运行程序。你将看到类似以下内容：

```text
i stores its value at 0xbffff738
```

虽然你的电脑可能会将 `i` 放在完全不同的地址。内存地址几乎总是以十六进制格式打印。

在计算机中，一切都存储在内存中，因此一切都具有地址。例如，一个函数从某个特定地址开始。要获取该地址，你只需使用函数名：

```c
int main(int argc, const char * argv[])
{
    int i = 17;
    printf("i stores its value at %p\n", &i);
    printf("this function starts at %p\n", main);
    return 0;
}
```

构建并运行程序。

### 在指针中存储地址

如果你想在一个变量中存储一个地址怎么办？你可以把它塞进一个大小合适的无符号整数中，但如果你在指定该变量类型时更具体，编译器可以帮助你捕捉错误。例如，如果你想要一个名为 `ptr` 的变量，它保存可以找到浮点数的地址，你会这样声明它：

```c
float *ptr;
```

我们说 `ptr` 是一个指向浮点数的*指针*变量。它不存储浮点数的值；它指向可能存储浮点数的地址。

声明一个名为 `addressOfI` 的新变量，它是指向 `int` 的指针。将 `i` 的地址赋值给它。

```c
int main(int argc, const char * argv[])
{
    int i = 17;
    int *addressOfI = &i;
    printf("i stores its value at %p\n", addressOfI);
    printf("this function starts at %p\n", main);
    return 0;
}
```

构建并运行程序。你应该看不到其行为有任何变化。

我们现在使用整数只是为了简单起见。但如果你想知道指针的意义何在，我理解你。传递分配给此变量的整数值与传递其地址一样容易。然而，很快，你的数据将比单个整数大得多，复杂得多。这就是为什么我们传递地址。并不总是可以传递你要操作的数据的副本，但你总是可以传递该数据起始位置的*地址*。一旦你有了它的地址，访问数据就很容易了。

