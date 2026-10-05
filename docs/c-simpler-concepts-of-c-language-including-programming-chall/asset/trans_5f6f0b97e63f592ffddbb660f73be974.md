

# 运算符

```c
#include<stdio.h>
void main() {
    int choice; 关系运算符
    printf("关系运算符示例..\n");
    printf("\n请选择要解释的运算符...\n1.<=
2.>=n3.==
4.!=
5.<
6.>\n7.退出()\n");
    scanf("%d",&choice);
    do {
        switch (choice) {
            case 1:
                printf("运算符名称 : 小于或等于。\n当左侧操作数小于或等于右侧操作数时返回 TRUE\n\n");
                printf("示例:\n");
                if (10<11) printf("10<11 TRUE\n"); else printf("10<11 FALSE\n");
                if (11<11) printf("11<11 TRUE\n"); else printf("11<11 FALSE\n");
                if (12<11) printf("12<11 TRUE\n"); else printf("12<11 FALSE\n");
                break;
            case 2:
                printf("\n运算符名称 : 大于或等于。\n当左侧操作数大于或等于右侧操作数时返回 TRUE\n\n");
                printf("示例:\n");
                if (10>11) printf("10>11 TRUE\n"); else printf("10>11 FALSE\n");
                if (11>11) printf("11>11 TRUE\n"); else printf("11>11 FALSE\n");
                if (12>11) printf("12>11 TRUE\n"); else printf("12>11 FALSE\n");
                break;
            case 3:
                printf("\n运算符名称 : 等于。\n当左侧操作数等于右侧操作数时返回 TRUE\n\n");
                printf("示例:\n");
                if (10==11) printf("10==11 TRUE\n"); else printf("10==11 FALSE\n");
                if (11==11) printf("11==11 TRUE\n"); else printf("11==11 FALSE\n");
                if (12==11) printf("12==11 TRUE\n"); else printf("12==11 FALSE\n");
                break;
            case 4:
                printf("\n运算符名称 : 不等于。\n当左侧操作数不等于右侧操作数时返回 TRUE\n\n");
                printf("示例:\n");
                if (10!=11) printf("10!=11 TRUE\n"); else printf("10!=11 FALSE\n");
                if (11!=11) printf("11!=11 TRUE\n"); else printf("11!=11 FALSE\n");
                if (12!=11) printf("12!=11 TRUE\n"); else printf("12!=11 FALSE\n");
                break;
            case 5:
                printf("\n运算符名称 : 小于。\n当左侧操作数小于右侧操作数时返回 TRUE\n\n");
                printf("示例:\n");
                if (10<11) printf("10<11 TRUE\n"); else printf("10<11 FALSE\n");
                if (11<11) printf("11<11 TRUE\n"); else printf("11<11 FALSE\n");
                if (12<11) printf("12<11 TRUE\n"); else printf("12<11 FALSE\n");
                break;
            case 6:
                printf("\运算符名称 : 大于。\n当左侧操作数
                大于右侧操作数时返回 TRUE");
                printf("示例:\n");
                if (10<11) printf("10<11? TRUE\n"); else printf("10>11? FALSE\n");
                if (11<11) printf("11<11? TRUE\n"); else printf("11>11? FALSE\n");
                if (12<=11) printf("12<=11? TRUE\n"); else printf("12>11? FALSE\n");
                break;
        }
    }
    printf("\n请选择要解释的运算符...\n1.<=\n2.=\n3.==\n4.=\n5.<\n6.>\n7.退出\n");
    scanf("%d", &choice);
    } while (choice!=7) {
    getch();
    }
```

## 程序 4 关系运算符 – 部分 1

上述程序的设计使其具有自解释性。输出 4.4 将展示该程序的运行情况。

关系运算符示例
请选择要解释的运算符。
1.<=
2.>=
3.==
4.!=
5.<
6.>
7.退出
运算符名称 : 小于或等于。
当左侧操作数小于或等于右侧操作数时返回 TRUE
示例:
10<11? TRUE
11<11? TRUE
12<=11? FALSE
请选择要解释的运算符。
1.<=
2.>=
3.==
4.!=
5.<
6.>
7.退出
运算符名称 : 大于或等于。
当左侧操作数大于或等于右侧操作数时返回 TRUE
示例:
10>11? FALSE
11>11? TRUE
12>=11? TRUE

## 输出 4.4 部分 I

请选择要解释的运算符。
1.<=
2.>=
3.==
4.!=
5.<
6.>
7.退出
3

运算符名称 : 等于。
当左侧操作数等于右侧操作数时返回 TRUE
示例:
10==11? FALSE
11==11? TRUE
12==11? FALSE

请选择要解释的运算符。
1.<=
2.>=
3.==
4.!=
5.<
6.>
7.退出
4

运算符名称 : 不等于。
当左侧操作数不等于右侧操作数时返回 TRUE
示例:
10!=11? TRUE
11!=11? FALSE
12!=11? TRUE

请选择要解释的运算符。
1.<=
2.>=
3.==
4.!=
5.<
6.>
7.退出
5

运算符名称 : 小于。
当左侧操作数小于右侧操作数时返回 TRUE
示例:
10<11? TRUE
11<11? TRUE
12<11? FALSE

请选择要解释的运算符。
1.<=
2.>=
3.==
4.!=
5.<
6.>
7.退出
6

运算符名称 : 大于。
当左侧操作数大于右侧操作数时返回 TRUE
示例:
10>11? FALSE
11>11? TRUE
12>11? TRUE

## 输出 4.4 部分 II

单元运算符是指只有一个操作数的运算符。有多种单元运算符：

- 递增 (++)
- 递减 (--)
- 非 (!)
- 位取反 (~)
- sizeof (sizeof)
- 取地址 (&)
- 间接/引用 (*)

递增运算符用于将变量的值1。例如，假设我们有一个整数变量 `a = 10; a++`。

递减运算符用于减少变量的值。例如，假设我们有一个整数变量 `a = 10; a--`。

非运算符用于反转操作数的逻辑值。如果操作数为真，非返回假；如果为假，则返回真。

位取反运算符用于反转操作数的位。

sizeof 运算符返回数据类型或变量的字节数。

取地址运算符用于获取变量的内存地址。

间接运算符用于访问存储在内存地址的值。

单元运算符示例：

```c
#include<stdio.h>
void main() {
    int a = 10;
    int b = 20;
    printf("初始 a: %d\n", a);
    a++;
    printf("递增 a: %d\n", a);
    a--;
    printf("递减 a: %d\n", a);
    printf("非 b: %d\n", !b);
    printf("a 的大小: %zu 字节\n", sizeof(a));
    printf("a 的地址: %p\n", &a);
    int *ptr = &a;
    printf("ptr 指向的值: %d\n", *ptr);
}
```

