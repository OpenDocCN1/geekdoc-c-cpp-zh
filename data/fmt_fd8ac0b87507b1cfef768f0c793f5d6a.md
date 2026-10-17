
`printf("Parent : terminated normally\n");`

}

}

(f) `waitpid()` 如何防止僵尸进程的产生？

答案：
`waitpid()` 函数会让父进程等待子进程完成。结果是子进程不会变成僵尸。

(g) Linux 如何知道我们是否注册了信号？

答案：
操作系统维护一个结构，按进程跟踪已注册/阻塞的信号。

(h) 当我们注册一个处理器时会发生什么？

答案：
每当注册新信号时，操作系统获取该信号的地址并标记为已注册。

(i) 编写一个程序验证 SIGSTOP 和 SIGKILL 信号是否不可捕。

**程序：**
```c
/* 验证 SIGSTOP 和 SIGKILL 信号是不可捕的 */

#include <signal.h>

void intHandler (int sign)

{

    printf("SIGINT recd inside handler\n");

}

void killHandler (int sign)

{

    printf("SIGKILL is not catchable\n");

}

void stopHandler (int sign)

{

    printf("SIGSTOP is not catchable\n");

}

int main()

{

    signal ( SIGINT,intHandler );

    signal ( SIGSTOP,stopHandler );

    signal ( SIGKILL,killHandler );

    while ( 1 ) {

        printf("Program Running\r");

    }

    return 0;

}
```

(j) 编写一个处理 SIGINT 和 SIGTERM 信号的程序。在 SIGINT 信号的处理器内部编写一个无限循环来打印消息“Processing Signal...”。运行程序并多次使用 Ctrl + C。再次运行程序并按一次 Ctrl + C。然后使用 kill 命令。你的观察结果是什么？

程序：
```c
/* 处理 SIGINT 和 SIGTERM 信号 */
# include <signal.h>

void intHandler ( int signum ) {

    while ( 1 ) {

        printf ("Processing Signal...\n");

    }

}

void termHandler ( int signum ) {

    printf ("SIGTERM recd inside sighhandler\n");

}

void contHandler ( int signum ) {

    printf ("SIGCONT recd inside sighhandler\n");

}

int main() {

    signal ( SIGINT, ( void* ) intHandler );

    signal ( SIGCONT, ( void* ) contHandler );

    signal ( SIGTERM, ( void* ) termHandler );

    while ( 1 ) {

        printf ("Program Running\n");

    }

}
```

(k) 编写一个程序，在执行 SIGINT 信号期间阻塞 SIGTERM 信号。

程序如下：
```c
/* To block SIGTERM signal during execution of SIGINT signal */
#include <signal.h>
#include <unistd.h>
#include <sys/types.h>
#include <stdio.h>
#include <string.h>

void intHandler (int signum)
{
    sigset_t block;
    char buffer[10];
    sigprocemptyset(&block);
    sigaddset(&block, SIGTERM);
    sigprocmask(SIG_BLOCK, &block, NULL);
    while (strcmp(buffer, "\n") != 0)
    {
        printf("Enter a string: ");
        gets(buffer);
        puts(buffer);
    }
    sigprocmask(SIG_UNBLOCK, &block, NULL);
}

void termHandler (int signum)
{
    printf("SIGTERM recd inside sighandler\n");
}

int main()
{
    signal (SIGINT, intHandler);
    signal (SIGTERM, termHandler);
    while ( 1 ) {
        printf("Program Running\n");
        return 0;
    }
}
```

## 第二四章

## 周期测试

## 周期测试 I

### [A] 填空：[ 5 分，每题 1 分 ]

- (1) 表达式 `i++` 与 `++i` 相同。
- (2) 实数 / `float` / `double` 类型的值无法使用 `switch-case` 进行检查。
- (3) C 程序中的每条指令都必须以 `;` 结尾。
- (4) `int` 数据类型的大小为 4 字节。
- (5) 编写在 `do-while` 循环中的语句即使条件为假，也会至少执行一次。

### [B] 判断对错：[ 5 分，每题 1 分 ]

- (1) 语句 `for ( ; ; )` 是一个有效语句。对。
- (2) `if - else if - else` 语句中的 `else` 子句会在所有 `ifs` 处执行。对。
- (3) `^` 运算符在 C 中用于执行幂运算。错。
- (4) C 允许 `=` 运算符的左侧仅有一个变量。对。
- (5) 条件运算符不能嵌套。错。

### [C] 下列程序的输出结果是什么：[ 5 分，每题 1 分 ]

- (a) 5 5 6
- (b) 65 A
- (c) 2 1
- (d) 21 525
- (e) 0 1

### [D] 指出有效程序中的错误（如有）：

## 第 24 章：周期测试

[ 5 分，每题 1 分 ]

- (a) 使用 `==` 代替 `:` 
- (b) `'then'`：未声明的标识符
- (c) 语法错误：在 `''` 之前缺少 `';'`：
- (d) 无错误。
- (e) 错误：变量 `'c'` 在未初始化的情况下使用。

### [E] 尝试完成以下：[ 20 分，每题 5 分 ]

```c
#include <stdio.h>
int main ()
{
    int i, j, prod1, prod2, term, s;
###s = 0;
    for (i = 1; i <= 3; i++)
    {
        prod1 = 1;
        for (j = 1; j<=i; j++)
            prod1 = prod1 * j;
        prod2 = prod1 * j;
        term = prod1 * prod2;
        s = s + term;
    }
    printf("sum of series=%f\n", s);
    return 0;
}
```

(2) 编写一个程序，根据用户要求一直输入数字，最后显示输入的正数、负数和零的数量。
```c
#include <stdio.h>
int main()
{
    int neg
```

(3) 编写一个程序找到通过键盘输入的一组数字的范围。范围是列表中最小和最大数字之间的差。

(4) 如果通过键盘输入三个整数，编写一个程序来判断它们是否构成勾股数元。
```c
#include<stdio.h>
int main()
{
    int i, j, k;
    printf("Enter three integers: \n");
    scanf("%d%d%d", &i, &j, &k);
    if ((i*i+j*j==k*k) || (j*j+k*k==i*i) || (k*k+i*i==j*j)) {
        printf("Numbers form pythagorian triplet \n");
    } else {
        printf("Numbers do not form pythagorian triplet \n");
    }
    return 0;
}
```

## 第 24 章：周期测试

## 周期测试 II

### [A] 填空：[ 5 分，每题 1 分 ]

- (1) `system ( )` 函数用于清屏。
- (2) 指针是变量，它们保存其他变量的地址。
- (3) `&` 被称为“地址”运算符。
- (4) 用于给复杂的公式提供方便名称的预处理器指令称为宏展开。
- (5) 对于引用传递，我们应该向被调用函数传递变量的地址。

### [B] 判断对错：[ 5 分，每题 1 分 ]

- (1) 函数可以返回多个值。错。
- (2) 每次调用函数都会创建一个新的变量。对。
- (3) 指针的大小是 4 字节。对。
- (4) 结构可以变成递归。错。
- (5) 编译顺序是链接。对。

### [C] 回答以下问题：[ 10 分，每题 2 分 ]

- (1) 为什么结构存储在栈上？
- (2) 如何决定按值还是引用传递？
- (3) 结构的大小取决于架构。
- (4) 为什么结构中存在空隙？为了内存对齐访问。
- (5) 结构的大小受成员顺序的影响吗证明。
- (6) 为什么递归会导致栈溢出？如果递归太深，栈内存会被耗尽。
- (7) 函数可以返回结构吗？可以，但按值返回的效率较低。
- (8) 如何向函数传递结构？按值传递（拷贝整个结构）或通过指针（传递地址）。

### [D] 尝试完成以下：[ 20 分，每题 5 分 ]

```c
#include <stdio.h>
int main ()
{
    int i, j, prod1, prod2, term, s;
    s = 0;
    for (i = 1; i <= 3; i++)
    {
        prod1 = 1;
        for (j = 1; j<=i; j++)
            prod1 = prod1 * j;
        prod2 = prod1 * j;
        term = prod1 * prod2;
        s = s + term;
    }
    printf("sum of series=%f\n", s);
    return 0;
}
```

(2) 编写一个程序，根据用户要求一直输入数字，最后显示输入的正数、负数和零的数量。
```c
#include <stdio.h>
int main()
{
    int neg
```

(3) 编写一个程序找到通过键盘输入的一组数字的范围。范围是列表中最小和最大数字之间的差。

(4) 如果通过键盘输入三个整数，编写一个程序来判断它们是否构成勾股数元。
```c
#include<stdio.h>
int main()
{
    int i, j, k;
    printf("Enter three integers: \n");
    scanf("%d%d%d", &i, &j, &k);
    if ((i*i+j*j==k*k) || (j*j+k*k==i*i) || (k*k+i*i==j*j)) {
        printf("Numbers form pythagorian triplet \n");
    } else {
        printf("Numbers do not form pythagorian triplet \n");
    }
    return 0;
}
```

## 定期测试 III

### [A] 填空题：[ 5 分，每题 1 分 ]

- (1) 提到数组名会产生数组的基地址。
- (2) C 语言允许我们超出数组的下界和上界。
- (3) 数组的大小是数组中单个元素大小之和。
- (4) 数组元素始终从零开始计数。
- (5) 结构体（structure）通常是一组不同元素的集合。

### [B] 判断对错：[ 5 分，每题 1 分 ]

- (1) 如果数组很大，它的元素可能会被存储在非连续的位置上。错误。
- (2) 所有字符串都以 `'0'` 结尾。正确。
- (3) 使用 `#pragma pack` 可以控制内存中结构体元素的布局。正确。
- (4) 二维数组的元素在内存中按以行和列的形式存储。错误。
- (5) 三维数组是多个一维数组的集合。错误。

### [C] 回答以下问题：[ 10 分，每题 2 分 ]

- (1) 如果超过了数组的边界会发生什么？
在读取数组时如果超过了边界，将出错。然而，如果在写入数组时超过了边界，边界之外已经存在的某些重要信息将被覆盖。有时这甚至可能导致程序挂起。如果超过了数组边界，编译器不会报告“Subscript out of range（下标越界）”的错误。边界检查始终是程序员的责任。

- (2) 在什么情况下你倾向于使用结构体而不是数组来存储相似元素？请举例说明。
当需要从函数返回一组相似元素时，倾向于使用结构体而不是数组，因为尝试返回数组时，只会返回它的基地址。

例如，如果我们要素返回一个包含实部和虚部（均为 `float` 类型）的复数，那么将它们放入一个结构体中比放入数组中更方便。

- (3) 字符串指针数组的局限性是什么？如何克服？
如果我们需要通过键盘读取字符串并接收到该数组中，字符串指针数组将非常不利。可以通过首先使用 `malloc()` 为字符串分配空间，然后将字符串的地址存储在指针数组中来解决这个问题。

- (4) 在二维数组 `a[4][4]` 中，为什么表达式 `a*a` 给给出基地址？
`a` 应该给出基地址，是因为 `a` 作为数组名，充当指向数组第 0 个元素的指针。二维数组是多个一维数组的集合。因此，当我们使用 `*a` 时，我们指的是第 0 个一维数组。而引用一个一维数组会产生其基地址，因此引用 `*a` 同样给出了基地址。

- (5) 如何使用 `scanf()` 和 `gets()` 接收多单词字符串作为输入？
```c
char str[30];
scanf("%[^\n]s", str);
gets(str);
```

### [D] 尝试完成以下题目：[ 20 分，每题 5 分 ]

- (1) 编写一个函数，该函数接收参数：一维数组、其大小和一个整数，并返回该整数在数组中出现的次数。
```c
#include <stdio.h>
int countnum ( int *a, int sz, int n);
int main() {
    int arr[100], size, num, i, count;
    printf("Enter the size of array:\n");
    scanf("%d", &size);
    printf("Enter the elements of an array:\n");
    for (i = 0; i < size; i++) {
        scanf("%d", &arr[i]);
    }
    printf("Enter the number you want to count:\n");
    scanf("%d", &num);
    count = countnum (arr, size, num);
    printf("count = %d", count);
    return 0;
}
int countnum (int *a, int sz, int n) {
    int j, cnt = 0;
    for (j = 0; j < sz; j++) {
        if (*a == n)
            cnt++;
        a++;
    }
    return cnt;
}
```

- (2) 创建一个包含 10 个城市名称的指针数组。编写一个程序按字母倒序对这些城市，并打印这个倒序列表。
```cpp
#include<iostream>
#include <string.h>
using namespace std;
int main() {
    char *cities[] = {
        "Nagpur",
        "Kanpur",
        "Delhi",
        "Sikandarabad",
        "Akola",
        "Ghatanji",
        "Jabalpur",
        "Ziri",
        "Shegaon",
        "Bombay"
    };
    char *t;
    int i, j;
    for (i = 0; i < 9; i++) {
        for (j = i + 1; j < 10; j++) {
            if (strcmp(cities[i], cities[j]) < 0) {
                t = cities[i];
                cities[i] = cities[j];
                cities[j] = t;
            }
        }
    }
```
