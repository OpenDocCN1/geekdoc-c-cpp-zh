
显然，输入值 x 与报告值 1 之间存在不匹配，而二者完全无关。如何检测这种情况？一种方法是在调用 `scanf()` 之前为变量赋予已知值。如果变量有一个已知值，然后在 `scanf()` 失败的过程中将其设置为 1，那将是 `scanf()` 实现中的一个严重缺陷，而这极不可能发生。

试图对“未定义行为”进行推理本质上是在浪费时间，因为绝对*任何事情*都可能发生。不过，如果你想要某种直观理解，这里概述一下可能正在发生的情况。由于变量 `i`（在之前的调用中）尚未初始化，因此从编译器的角度来看，它的“生命周期”尚未开始。该变量与另一个变量共享一个寄存器，而那个变量的生命周期在该变量初始化之前就结束了。另一个变量在某些条件下恰好获得了值 1，并且由于该变量未初始化，它只是获得寄存器中残留的任何内容。因此，*绝不能读取未初始化的变量*：编译器可以假定变量在初始化之前永远不会被读取，并且它可以并且确实基于这些假设进行优化。

请注意，未定义行为不仅没有意义，而且一旦编译器可能确定它不可避免，它就可能发生。按照清单 2.21 中代码的写法，一旦 `scanf()` 函数以不完整的结果结束，你就有了“未定义行为”。

在本节开头的示例中，“绝对做任何事情”恰好是“在某些特定情况下，偶尔将变量 i 的值设置为 1”。这不是编译器缺陷，因为根据定义，一旦你有了“未定义行为”，就不存在编译器缺陷这回事。此时，对编译器生成什么代码没有任何要求。

当你想从命令行读取字符串和数字时，还有一些其他有趣的场景，其中一些在此处描述：

[https://stackoverflow.com/questions/20867382/c-programming-scanf-not-working-correctly](https://stackoverflow.com/questions/20867382/c-programming-scanf-not-working-correctly)

## 从命令行读取多个字符串

清单 2.22 显示了 `FirstLastName.c` 的内容，它说明了如何提示用户输入一个人的名字和姓氏。

### 清单 2.22：FirstLastName.c

```c
#include <stdio.h>
#include <string.h>

char first[100];
char last[100];
char full[200];

int main()
{
    printf("Enter first name: ");
    fgets(first, sizeof(first), stdin);

    // see comment below about this snippet:
    // first[strlen(first)-1] = '\0';
    printf("Enter last name: ");
    fgets(last, sizeof(last), stdin);

    strcpy(full, first);
    strcat(full, " ");
    strcat(full, last);

    printf("The name is %s\n", full);

    return (0);
}
```

清单 2.22 声明了字符变量 first、last 和 fullName，长度分别为 100、100 和 200。接下来，main() 函数使用 2 个不同的 printf() 语句提示用户输入名字和姓氏，并使用内置的 gets() C 函数捕获这些输入值。

代码的下一部分使用内置的 strcpy() C 函数将 first 复制到变量 full。接下来，内置的 strcat() 函数追加一个空格（" "），然后将 last 追加到变量 full。下面是启动清单 2.22 中代码的示例调用：

```
Enter first name: john
Enter last name: smith
The name is john
smith
```

请注意，全名显示在单独的行上，这是因为用户输入名字后必须按 <RETURN>，而 <RETURN> 字符被包含在变量 full 中。我们可以通过取消注释以下代码片段来简单地移除 <RETURN> 字符：

```
first[strlen(first)-1] = '\0';
```

然而，如果变量 first 是空字符串，启用前面的代码片段可能会产生未定义行为，如果该程序接收空文件作为输入，就可能发生这种情况。清单 2.22 中代码的这一方面说明了在代码中无意引入缺陷是多么容易。解决方案很简单：*在通过前面的代码片段截断变量 first 中的字符串之前，测试 strlen(first) 的值以确保它不是 0。*

重新编译修改后的代码并在命令行重新启动，以下是一个示例调用：

```
Enter first name: john
Enter last name: smith
The name is john smith
```

还有一点需要记住：如果变量 first 是空字符串，移除 <RETURN> 字符的前述代码片段会导致未定义行为。因此，你需要修改清单 2.22 中的代码，在截断字符串之前测试 strlen(first) 的值以确保它不是 0。

## 用于数值计算的用户输入

清单 2.23 显示了 SimpleAdder.c 的内容，它说明了如何提示用户输入，然后使用 fgets() 和 sscanf() 函数获取输入，所有这些都发生在 while 循环内。

### 清单 2.23：SimpleAdder.c

```c
#include <stdio.h>

char line[100]; // line of data from the input
int result;  // the result of the calculations
char operator; // operator the user specified
int value;    // value specified after the operator

int main()
{
    result = 0; // initialize the final result

    while (1) {
        printf("Result: %d\n", result);
        printf("Enter operator and number: ");

        fgets(line, sizeof(line), stdin);
        sscanf(line, "%c %d", &operator, &value);

        if (operator == '+') { // why does "=" also work?
            result += value;
        }
        else if (operator == '-') {
            result -= value;
        }

        else {
            printf("Exiting loop: unknown operator: %c\n",
                   operator);
            break;
        }
    }

    return 0;
}
```

清单 2.23 首先将变量 result 初始化为 0。程序的主体是一个 while 循环，重复执行直到遇到 break 语句。while 循环的主体包含一个代码块，提示用户输入运算符和数字，如下所示：

```
printf("Enter operator and number: ");
```

函数以及使用 scanf()
函数进行格式化输入。

## 第3章

### 循环和数组

本章包含演示如何在 C 中使用简单循环、嵌套循环和数组的代码示例。这些代码示例执行与字符串相关的任务，以及使用数字数组和字符串数组的各种任务。此外，许多代码示例包含 `if/else` 条件逻辑，这些逻辑在[第2章](#)中介绍过（如果你还没有阅读该章，请先阅读）。

本章第一部分讨论基本循环、一维和多维数组，以及如何在数组中执行线性搜索。本章第二部分计算数字数组中的最大值和最小值，如何向数组中插入元素，以及如何从数组中删除元素。

本章第三部分包含 `while` 循环、`do-while` 循环，以及涉及 while 循环的字符串相关示例。本节的代码示例还包含条件逻辑，这些逻辑在[第2章](#)中介绍过。最后一节包含确定正整数因子的代码示例，以及如何检查一个数是否为质数。

## 使用 for 循环

清单 3.1 显示了 ForLoop.c 的内容，向你展示如何在 C 中使用 for 循环。

### 清单 3.1：ForLoop.c

```c
#include <stdio.h>

int main()
{
   int max=5;
   for(int i=0; i<max; i++)
   {
      printf("i : %d\n", i);
   }

   return 0;
}
```

清单 3.1 很直接：一个 `main()` 函数初始化整型变量 max（其值为 5），然后是一个 for 循环，打印 0 到 max 之间的整数。

启动清单 3.1 中的 C 程序后的输出如下：

```
i : 0
i : 1
i : 2
i : 3
i : 4
```

## 在 for 循环中使用 break 和 continue
