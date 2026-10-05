

# 条件结构与循环

------要执行的语句------
break;
}
程序 2.4 解释了 switch case（分支语句）的概念。

```c
#include<stdio.h>
#include<conio.h>
int main() {
    int mark;
    printf("please enter the mark(100/80/50/34)");
    scanf("%d",&mark);
    switch(mark) {
        case 100:
            printf("V.Good!!Keep it up");
            break;
        case 80:
            printf("Good!!");
            break;
        case 50:
            printf("Should perform well!!");
            break;
        case 34:
            printf("Poor performance!!");
            break;
        default:
            printf("Enter a number from 100,80,50,34");
            break;
    }
    getch();
    return 0;
}
```

程序 2.4 Switch Case
示例输入输出在输出 2.4 中显示

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_32_0.png)

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_32_1.png)

# 22 C语言简明教程

```
C:\Dev-Cpp\switch_case_prog.exe
please enter the nmark<100/80/50/34>
58
Enter a number from 100.80.50.34_
```

输出 2.4 代码 2.4 的输出。

关于 switch case 的注意点：

- 1. case 标签应该是一个 int 或 char 类型的变量。（在之前的示例中，mark 是 case 标签，它的类型是 int 类型！）
- 2. Case 值可以是整数、字符值或整数表达式！

示例，
```c
switch (mark)
{ 
    case 100-80+60: // 绝对有效；
        //要执行的语句
        break;
    case 'Y':// 有效。
        //要执行的语句
        break;
}
```

- 3. 在每个 case 的末尾必须有一个 'break' 语句。否则，当前 case 之后的 case 将自动执行，直到遇到 break 为止。
- 4. default 可以放在开头或结尾，并不是强制要有 default 语句。

# 2.2. 循环结构

当用户需要重复执行某些语句多次时，循环结构非常有优势。

例如，如果用户需要打印 100 次他的名字，连续写 100 次 print 语句显然会消耗用户大量的时间。在这种情况下，循环的优点是令人赞叹的。

与其不断编写 100 次相同的 print，不如利用循环结构，因为它们：

- 1. 消耗更少。
- 2. 缩短程序长度。
- 3. 提高了可读性。

后续章节将解释循环结构的使用。

# 2.2.1. for 循环。

语法：
for (初始化部分; 条件部分; 递增/递减部分)

---要执行的语句---
}

例如，
for(i=0;i<5;i++) -> 此循环将 i 初始化为 0，检查条件 i 是否小于 5，i++ 是递增运算符，类似于 i=i+1；（关于该运算符的更多细节见第 4 章）。

程序 2.5 解释了打印 100 次某语句，

```c
#include<stdio.h>
#include<conio.h>
void main() {
    int i;
    for(i=0;i<100;i++)
    printf("Hello, Welcome to C programming");
    getch();
}
```

# 程序 2.5 for 循环

输出 2.5 显示了部分执行过程：

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_34_0.png)

# 输出 2.5 程序 2.5 的输出。

注意：for 循环并不包含上述所有的三个部分。（即）人们可以如下跳过初始化部分，

```c
i=0;
for(i<5;i++)
```

# 24 C语言简明教程

同样，人们可以通过在循环终止之前包含递增/递减语句来省略递增/递减部分。

程序 2.6 和输出 2.6 解释了使用 * 打印一个模式。

```c
//for_loop.c
#include<stdio.h>
#include<conio.h>
main() {
    int i,j;
    for (i=0;i<7;i++) {
        for (j=0;j<=1;j++) {
            printf("*");
        }
    }
    getch();
}
```

# 程序 2.6 使用循环打印 * 模式。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_35_0.png)

输出 2.6 程序 2.6 的 * 打印。

程序 2.7 解释了打印从 0 到 19 的偶数，
输出 2.7 显示了示例。

```c
#include<stdio.h>
#include<conio.h>
void main() {
    int i,j;
    for(i=0;i<20;i++) {
        if(i%2==0)
            printf("even:%d\t",i);
        else
            printf("odd:%d\t",i);
    }
    getch();
}
```

# 程序 2.7 'for' 循环示例。

# 条件结构与循环

```
C:\Documents and Settings\Desktop\prog_for_loop.exe
even:0 odd:1
even:2 odd:3
even:4 odd:5
even:6 odd:7
even:10 odd:11
even:12 odd:13
even:14 odd:15
even:16 odd:17
```

输出 2.7 程序 2.7 的示例输出。

# 2.2.2. while 循环

语法：
初始化；
while(condition)
{
---要执行的语句---
递增/递减语句;
}

什么时候偏 while 循环？
当程序员不知道迭代次数时，while 循环比 for 循环更好。程序 2.8 显示了这一点。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int number, value;
    number=100;
    while(number>0)
    {
        printf("Please enter the number to be subtracted:");
        scanf("%d",&value);
        printf("Remaining:%d\n",number);
        number=number-value;
    }
    getch();
}
```

# 26

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_37_0.png)

输出 2.8 while 循环的示例输出。

# 2.2.1. do-while 循环

语法：
do
{
---要执行的语句---
} while(condition);

while 和 do-while 循环的区别是什么？
区别是 do-while 至少执行一次循环体。程序 2.9 显示了这一点。

```c
#include<stdio.h>
#include<conio.h>
main()
{
    int i;
    i=100;
    do{
        printf("enter the value of i:");
        scanf("%d",&i);
        printf("i=%d\n", i);
        i=i-10;
    }while(i>0);
    getch();
}
```

# 程序 2.9 do-while 循环

# 条件结构与循环

运行上述代码时，可以看到如输出 2.9 所示。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_38_0.png)

# 输出 2.9 程序 2.9 的输出。

注意：如果上述程序使用 while 循环编写，将会发生以下情况。

```c
// while_loop.c
#include<stdio.h>
#include<conio.h>
main() {
    int i;
    printf("enter the value of i: %d"
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa17d_38_1.png)

# 程序 2.10 While 示例

# 2.2.3. break 和 continue 语句。

如果读者还记得，break 之前用过。是的，在 2.4 中，break 语句被用于终止 switch case。

该语句是自解释的。它被用于中断某些操作。如果在循环中使用，它会中断循环并跳出。如果在 switch case 中使用，它会中断切换过程。

| Break | Continue |
|---|---|
| 用于终止其内部过程。 | 用于跳过当前步骤（迭代）并继续下一个步骤（迭代）。 |

后续程序 2.11 解释了这个概念。

```c
//break_continue.c
#include <stdio.h>
#include <conio.h>
main() {
    float i;
    do {
        printf("enter the value of GPA value:\n");
        scanf("%f", &i);
        if (i<0)
            printf("Terminating...\n");
            break;
        else if (i>10) // GPA 永远不会超过 10!
            printf("Sorry, GPA never crosses 10!!\n");
            continue;
        else
            printf("Your GPA is %f\n", i);
    } while (1);
    getch();
}
```

# 程序 2.11 break and continue 示例。

输出在下方的输出 2.11 中。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_39_0.png)

# 输出 2.11 程序 2.11 的输出

