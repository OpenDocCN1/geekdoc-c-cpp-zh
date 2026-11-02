
接受一个整数信号编号作为参数。图 14.5 总结了头文件 `<signal.h>` 中定义的*标准信号*。

| 信号 | 说明 |
|---|---|
| SIGABRT | 程序异常终止（例如调用函数 abort）。 |
| SIGFPE | 错误的算术运算，例如除零或导致溢出的运算。 |
| SIGILL | 检测到非法指令。 |
| SIGINT | 收到交互式注意信号（`<Ctrl> c` 或 `<command> c`）。 |
| SIGSEGV | 试图访问未分配给程序的内存。 |
| SIGTERM | 发送给程序的终止请求。 |

图 14.5 | `signal.h` 标准信号。

图 14.6 使用函数 `signal` 捕获 `SIGINT`。第 12 行使用 `SIGINT` 和指向函数 `signalHandler` 的指针调用 `signal`（请记住，函数名就是指向该函数的指针）。当发生 `SIGINT` 类型的信号时，控制权传递给函数 `signalHandler`，该函数打印一条消息，并让用户选择是否继续正常执行程序。如果用户希望继续执行，则通过再次调用 `signal` 重新初始化信号处理函数，控制权返回到程序中检测到该信号的位置。

在此程序中，函数 `raise`（第 21 行）用于模拟 `SIGINT`。选择一个 1 到 50 之间的随机数。如果该数字为 25，则调用 `raise` 生成该信号。通常，`SIGINT` 是在程序外部发起的。例如，在 Linux/UNIX 或 Windows 系统上执行程序时键入 `<Ctrl> c` 会生成一个 `SIGINT`，从而终止程序执行。信号处理可用于捕获 `SIGINT` 并防止程序被终止。

```c
1  // Fig. 14.6: fig14_06.c
2  // Using signal handling
3  #include <stdio.h>
4  #include <signal.h>
5  #include <stdlib.h>
6  #include <time.h>
7
8  void signalHandler(int signalValue); // prototype
9
10 int main(void)
11 {
12    signal(SIGINT, signalHandler); // register signal handler
13    srand(time(NULL));
14
15    // output numbers 1 to 100
16    for (int i = 1; i <= 100; ++i) {
17       int x = 1 + rand() % 50; // generate random number to raise SIGINT
```

图 14.6 | 使用信号处理。（第 1 部分，共 3 部分。）

```
94 95 96
Interrupt signal (2) received.
Do you wish to continue (1 = yes or 2 = no)? 2
```

**图 14.6** | 使用信号处理。（第 3 部分，共 3 部分。）

## 14.9 动态内存分配：函数 `calloc` 和 `realloc`

第 12 章介绍了使用函数 `malloc` 动态分配内存的概念。正如第 12 章所述，对于快速排序、搜索和数据访问，数组优于链表。然而，数组通常是静态数据结构。通用工具库（`stdlib.h`）还提供了另外两个用于动态内存分配的函数——`calloc` 和 `realloc`。这些函数可用于创建和修改动态数组。函数 `calloc` 动态地为数组分配内存。`calloc` 的原型为

```c
void *calloc(size_t nmemb, size_t size);
```

它的两个参数分别表示*元素个数*（`nmemb`）和*每个元素的大小*（`size`）。函数 `calloc` 还会将数组元素初始化为零。该函数返回指向已分配内存的指针；如果内存*未*分配，则返回 `NULL` 指针。`malloc` 与 `calloc` 的主要区别在于：`calloc` 会清除其分配的内存，而 `malloc` *不会*。

函数 `realloc` *改变*先前调用 `malloc`、`calloc` 或 `realloc` 所分配对象的大小。只要分配的内存量*大于*先前分配的量，原对象的内容就*不会被修改*。否则，内容在新对象大小范围内保持不变。`realloc` 的原型为

```c
void *realloc(void *ptr, size_t size);
```

这两个参数分别是指向原对象的指针（`ptr`）和对象的*新大小*（`size`）。如果 `ptr` 为 `NULL`，则 `realloc` 的工作方式与 `malloc` 完全相同。如果 `ptr` 不为 `NULL` 且 `size` 大于零，`realloc` 会尝试为该对象*分配一个新的内存块*。如果新空间*无法*分配，则 `ptr` 所指向的对象保持不变。函数 `realloc` 返回指向重新分配的内存的指针，或返回 `NULL` 指针以表示内存未被重新分配。

> **错误预防提示 14.1**
>
> *避免在调用 `malloc`、`calloc` 和 `realloc` 时进行零大小分配。*

## 14.10 使用 `goto` 进行无条件分支

我们已强调使用结构化编程技术来构建易于调试、维护和修改的可靠软件的重要性。在某些情况下，性能比严格遵循结构化编程技术更重要。在这些情况下，可能会使用一些非结构化编程技术。例如，我们可以在循环继续条件变为假之前使用 break 终止迭代语句的执行。如果在循环终止之前任务已完成，这可以节省不必要的循环迭代。

非结构化编程的另一个例子是 goto 语句——无条件分支。goto 语句的结果是控制流转移到 goto 语句中指定标签之后的第一个语句。标签是一个后跟冒号的标识符。标签必须与引用它的 goto 语句出现在同一函数中。标签在不同函数之间不必唯一。图 14.7 使用 goto 语句循环十次，并每次打印计数器值。将 count 初始化为 1 后，第 11 行测试 count 以确定它是否大于 10（跳过标签 start:，因为标签不执行任何操作）。如果是，则控制权从 goto 转移到标签 end: 之后的第一个语句（位于第 20 行）。否则，第 15–16 行打印并递增 count，控制权从 goto（第 18 行）转移到标签 start: 之后的第一个语句（位于第 9 行）。

```c
// Fig. 14.7: fig14_07.c
// Using the goto statement
#include <stdio.h>

int main(void)
{
    int count = 1; // initialize count

start: // label

    if (count > 10) {
        goto end;
    }

    printf("%d ", count);
    ++count;

    goto start; // goto start on line 9

end: // label
    putchar('\n');
}
```

![](img/d0d3b7423c2d9e5650be79209ea1885d_576_0.png)

**图 14.7** | 使用 goto 语句。

在第 3 章中，我们指出编写任何程序只需要三种控制结构——顺序、选择和迭代。遵循结构化编程规则时，可能会在函数内创建深层嵌套的控制结构，而从中高效退出可能很困难。一些程序员在这种情况下使用 goto 语句，以便快速退出深层嵌套结构。这样就不必为了退出控制结构而测试多个条件。还有一些额外情况实际上建议使用 goto——例如参见 CERT 建议 MEM12-C，“在使用和释放资源时，因错误离开函数可考虑使用 Goto 链。”

**性能提示 14.1**
使用 goto 语句可以高效地退出深层嵌套的控制结构。

**软件工程观察 14.3**
goto 语句是非结构化的，可能导致程序更难以调试、维护和修改。

## 小结

### 第 14.2 节 重定向 I/O
- 在许多计算机系统上，可以重定向程序的输入（p. 564）和输出。
- 使用重定向输入符号（<；p. 564）或管道（|；p. 565）从命令行重定向输入。
- 使用重定向输出符号（>；p. 565）或追加输出符号（>>；p. 565）从命令行重定向输出。重定向输出符号只是将程序输出存储到文件中，而追加输出符号将输出追加到文件末尾。

### 第 14.3 节 可变长度参数列表
- 可变参数头文件 <stdarg.h>（p. 565）中的宏和定义提供了构建具有可变长度参数列表（p. 565）的函数所需的能力。
- 函数原型中的省略号（...）（p. 565）表示可变数量的参数。
- 类型 va_list（p. 567）适合保存宏 va_start、va_arg 和 va_end 所需的信息。要访问可变长度参数列表中的参数，必须声明一个 va_list 类型的对象。
- 在访问可变长度参数列表的参数之前，调用宏 va_start（p. 567）。该宏初始化用 va_list 声明的对象，以供 va_arg 和 va_end 宏使用。
- 宏 va_arg（p. 567）展开为可变长度参数列表中下一个参数的值和类型的表达式。每次调用 va_arg 都会修改用 va_list 声明的对象，使该对象指向列表中的下一个参数。
- 宏 va_end（p. 567）使函数能够正常返回，该函数的可变长度参数列表曾由 va_start 宏引用。

### 第 14.4 节 使用命令行参数
- 在许多系统上，可以通过在 main 的参数列表中包含参数 int argc（p. 567）和 char *argv[]（p. 567），从命令行向 main 传递参数。参数 argc 接收命令行参数的数量。参数 argv 是一个字符串数组，其中存储实际的命令行参数。

### 第 14.5 节 编译多源文件程序

