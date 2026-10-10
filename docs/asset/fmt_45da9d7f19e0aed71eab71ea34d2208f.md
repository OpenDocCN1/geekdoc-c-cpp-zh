
```c
#include<stdio.h>
int main() {
    while(1) {
        if(printf("%d",printf("%d", 10)))
            break;
        else
            continue;
    }
    return 0;
}
```

- (a) 102
- (b) 死循环
- (c) 12
- (d) 101

## 47. 解释下面的函数指针。

```c
int (* fun( float, void (*pqr) () ) ) ();
```

## 48. 下面程序的输出是什么？

```c
#include<stdio.h>
#include<stdlib.h>
int main()
{
    int *ptr1,*ptr2;
    ptr1 = malloc(sizeof(int));
    printf("%d ",*ptr1);
    int i;
    ptr2 = calloc(sizeof(int),1);
    printf("%d ",*ptr2);
    return 0;
}
```

- (a) 0 0
- (b) 0 垃圾
- (c) 垃圾 0
- (d) 垃圾 垃圾

## 49. 下面程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int i;
    char a[]="\0";
    char b[] = "\n";
    if(printf("%s",a)) //第 4 行
        if(printf("%s",b))
            printf("1\n");
        else
            printf("2\n");
    else //第 9 行
        if(printf("%s",b)) //第 10 行
            printf("3 \n");
        else
            printf("4 \n");
    return 0;
}
```

- (a) 1
- (b) 2
- (c) 3
- (d) 4

## 50. 下面程序的输出是什么？

```c
#include<stdio.h>
int i = 10;
int main()
{
    int i=i++; //第 1 行
    printf("%d d",i);
    return 0;
}
```

- (a) 10
- (b) 11
- (c) 垃圾
- (d) 错误-赋值

## 51. 下面程序的输出是什么？

```c
#include<stdio.h>
int main() {
    while(1) {
        if(printf("%d",printf("%d", 10)))
            break;
        else
            continue;
    }
    return 0;
}
```

- (a) 102
- (b) 死循环
- (c) 12
- (d) 101

## 52. 解释下面的函数指针定义。

```c
int (* fun( float, void (*pqr) () ) ) ();
```

```c
return 0;
}
```

+   (a) 1 8
+   (b) 0 8
+   (c) 7 0
+   (d) 0 0

## 54. **以下程序的输出是什么？**

```c
#include<stdio.h>
int main() {
    char p[] = "Hello India";
    char c;
    char *ptr = p;
    c = ++ptr++;
    printf("%c",++ptr);
    return 0;
}
```

+   (a) l
+   (b) f
+   (c) H
+   (d) e

## 55. **以下程序的输出是什么？**

```c
#include<stdio.h>
int main() {
    char p[] = "hello India";
    char *ptr = p;
    printf("%c",++(ptr));
    return 0;
}
```

+   (a) i
+   (b) h
+   (c) l
+   (d) a

56. "hello India" 会被打印多少次？

```c
#include<stdio.h>
int main()
{
    int i=0;
    while(+(i--)!=0) // 第2行
    {
        printf("hello India\n");
        i=-i++;
    }
    return 0;
}
```

+   (a) 2
+   (b) 1
+   (c) 0
+   (d) 第2行语法错误

57. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    signed char i=0;
    for(;i>=0;i++); 
        printf("%d\n",i);
    return 0;
}
```

+   (a) -127
+   (b) -128
+   (c) 无限循环
+   (d) 0

58. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    unsigned char i=0;
    for(;i>=0;i++);
    printf("%d\n",i);
    return 0;
}
```

+   (a) -127
+   (b) -128
+   (c) 无限循环
+   (d) 0

59. 以下程序的输出是这些？

```c
#include<stdio.h>
int main()
{
    char *ptr;
    char str[] = "India is great";
    ptr = str;
    ptr += 4; // 第4行
    printf("%s",ptr);
    return 0;
}
```

+   (a) India is great
+   (b) is great
+   (c) a is great
+   (d) 无输出

60. 以下程序中哪一个 printf 打印了值 2？

```c
#include<stdio.h>
int main()
{
    int a[6][10][15] = {0};
    a[4][2][0] = 2;
    return 0;
}
```

(a) printf("%d",*(((a+4)+2)+0));
(b) printf("%d",*(*((a+4)+2)+0));
(c) printf("%d",*(*((a+4)+2)+0));
(d) 以上都不是

## 面试的其他重要问题如下：

+   1. 编写一个 C 程序实现两个矩阵相加。
+   2. 编写一个 C 程序使用递归计算给定数的阶乘。
+   3. 编写一个 C 程序实现两个矩阵相减。
+   4. 编写一个 C 程序使用递归计算给定数字各位数字之和。
+   5. 编写一个 C 程序使用递归反转任意数字。
+   6. 编写一个 C 程序，不使用 sizeof运算符获取 int 的大小。
+   7. 编写一个 C 程序，不使用 sizeof运算符获取 double 的大小。
+   8. 编写一个 C 程序，不使用 sizeof运算符获取结构体的大小。
+   9. 编写一个 C 程序，不使用 sizeof运算符获取联合体的大小。
+   10. 编写一个 C 程序实现线性查找。
+   11. 编写一个 C 程序实现二分查找。
+   12. 编写一个 C 程序使用递归实现二分查找。
+   13. 编写一个 C 程序，将一维数组传递给函数。
+   14. 编写一个 C 程序，将二维数组传递给函数。
+   15. 编写一个 C 程序实现两个矩阵相乘。

## 第4组解析

+   1. a
**解释：** 函数指针的演示。

+   2. c
**解释：** 函数指针数组的演示，每个函数接收两个 int 并返回一个 int。

+   3. b, d
**解释：** 选项 (a) 是 *ptr 指向的固定值，无法更新。选项 (b) 是固定指针地址，我们无法更新 ptr；选项 (c) 等同于选项 (a)。选项 (d) 是固定值和固定指针地址，不允许更新 *ptr 和 ptr。

+   4. a
**解释：** 不需要。

+   5. a
**解释：** 练习题。

+   6. a
**解释：** 不需要。

+   7. b
**解释：** 练习题。

+   8. a
**解释：**

| x | y | z | 7 |
|---|---|---|---|
| 1000 | 2000 | 3000 | 5000 |
| | | 1000 | 7000 |
| p1 | 1000 | p2 | 2000 | | |
| | | p3 | 3000 | | |
| | | (i) | | 5000 | | |
| | | (b) | 6000 | | |

```c
初始化：
*p1 = &x; *p2 = &y;
*p3 = &z; *ptr = &p2;
(i) p2-p1;
(ii) p3 = p2;
```

在步骤 (i)，p2=p1；p2 现在持有 'p1'，p1 本身持有 x 的地址，ptr 仍然指向 p2。因此，ptr 间接持有指向 x 地址的链接。

### 9. c
**解释：**

| | 50 | 60 | 74 | 80 | 90 |
|---|---|---|---|---|---|
| 1000 | 1004 | 1008 | 1012 | 1016 |
| 1004 | | 2000 | 1008 | 4000 |

```c
初始化：
(v) int *ptr=ptr=p1;--1004+1--1008
(i) int a[5] = {50, 60, 70, 80, 90};
步骤大小为 4
(ii) int *ptr = a;
(vi) *ptr = --ptr+(1008)--74
(iii) int *q = &a[2];
如果值 1008 增加了 4，
(iv) p::;
因为 ptr 是;
```

在步骤 (i)，p2=p1；p2 现在持有 'p1'，p1 本身持有 x 的地址，ptr 仍然指向 p2。因此，ptr 间接持有指向 x 地址的链接。

### 31. b
**Explanation**: 允许预处理指令的重新定义，其值将被最新的预处理指令替换。

### 32. d
**Explanation**: 我们在问题 57 第 2 组的解释中讨论过类似的概念。二维数组是 1D 数组的集合，每个字符串都以 1D 数组的形式存储。每个 1D 数组的基地址不能修改。如果我们将二维数组声明为 *str[4], → char *str[4]="hello", "India", "love", "great";，那么程序将输出 "hello India great love"。

### 33. d
