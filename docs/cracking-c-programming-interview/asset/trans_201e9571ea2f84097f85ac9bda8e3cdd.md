

```c
struct student
{
  unsigned int roll : 6 , batch : 6;
} sl1;
int main()
{
  sl1.roll = 1;
  sl1.batch = 1;
  char *p = &sl1;
  printf("%c % u ",*p,sizeof(sl1));
  return 0;
}
```

+ (a) A 4
(b) A 2
(c) 垃圾值 4
(d) 垃圾值 2

## 23. 以下程序的输出是什么？

```c
#include<stdio.h>
struct std
{
  int a;
  union unit
  {
    int a, b;
  } u;
};
int main()
{
  struct std s = {1, 2, 3};
  printf("%d %d %d ", s.a, s.u.a, s.u.b);
  return 0;
}
```

+ (a) 1 2 3

(b) 1 3 3
(c) 3 2 2
(d) 1 2 2

## 样本卷-4解答

+ 1. b
2. a
3. a
4. c
5. c
6. d
7. a
8. c
9. a
10. d
11. b
12. c
13. c
14. 21.5 100 'd'
15. b
16. d
17. a
18. c
19. a
20. c
21. a
22. a
23. d

## 样本卷 - 5

包含去年的 GATE 题目。

题目数量：29 题，最大时间：1 小时。

+ 1. 给定一段代码，定义 's' 为（GATE CS 2000）
```c
struct node
{
    int i;
    float j;
};
struct node *s[10];
```
(a) 一个数组，其每个元素都是一个指向 node 类型结构体的指针
(b) 一个包含 2 个字段的结构，每个字段都是指向 10 个元素数组的指针
(c) 一个包含 3 个字段的结构：一个整数，一个浮点数和一个 10 个元素的数组
(d) 一个数组，其每个元素都是一个 node 类型的结构。

+ 2. 下述 C 语句中的标记（tokens）数量为（GATE 2000）
```c
printf("i = %d, &i = %x", i, &i);
```
(a) 3
(b) 26
(c) 10
(d) 21

+ 3. 考虑以下 C 声明（GATE CS 2000）
```c
struct {
    short s [5];
    union {
        float y;
        long z;
    } u;
} t;
```

假设类型 float 和 long 的对象分别占用 8 字节、4 字节和 8 字节。在不考虑对齐因素的情况下，变量 t 的内存需求为：

+ (a) 22 字节
(b) 14 字节
(c) 18 字节

## 以下 C 程序执行结束时 j 的值。（GATE CS 2000）

```c
#include<stdio.h>
int incr(int i)
{
    static int count = 0;
    count = count + i;
    return (count);
}
int main ()
{
    int i,j;
    for (i = 0; i<=4; i++)
        j = incr(i);
    return 0;
}
```

+ (a) 10
(b) 4
(c) 6
(d) 7

## 5. 下列组合最合适的匹配是（GATE CS 2000）

X: m=malloc(5); m= NULL; 1: 使用悬空指针
Y: free(n); n->value=5; 2: 使用未初始化指针
Z: char *p; *p = 'a'; 3. 内存泄漏是：

+ (a) X—1 Y—3 Z-2
(b) X—2 Y—1 Z-3
(c) X—3 Y—2 Z-1
(d) X—3 Y—1 Z-2

## 6. 考虑以下三个 C 函数：（GATE 2001）

```c
[P1] int * g (void)
{
  int x = 10;
  return (&x);
}
```

```c
[P2] int * g (void)
{
  int * px;
  *px = 10;
  return px;
}
```

```c
[P3] int *g (void)
{
  int *px;
  px = (int *) malloc(sizeof(int));
  *px = 10;
  return px;
}
```

上述三个函数中哪些可能会引起指针问题？

+ (a) 仅 P3
(b) 仅 P1 和 P3
(c) 仅 P1 和 P2
(d) P1, P2, 和 P3

## 7. 考虑以下 C 二维数组的声明：

```c
char a[100][100];
```

假设主内存是字节寻址的，且数组从内存地址 0 开始存储，a[40][50] 的地址是：

+ a) 4040
(b) 4050
(c) 5040
(d) 5050

## 8. C 语言是。

+ a) 上下文无关语言
+ b) 上下文语言
+ c) 正则语言
+ d) 仅图灵机完全解析

## 9. 假设以下 C 变量声明：

```c
int *A[10], B[10][10];
```

下列表达式

I A[2]
II A[2][3]
III B[1]
IV B[2][3]

如果在 C 程序的赋值语句左侧使用，哪些不会产生编译错误？

+ a) 仅 I, II, 和 IV
+ b) 仅 II, III, 和 IV
+ c) 仅 II 和 IV
+ d) 仅 IV

## 10. 考虑所示的 C 程序。（GATE CS 2003）

```c
#include <stdio.h>
#define print(x) printf("%d ", x)
void P(int *y)
{
    int x = *y+2;
    Q(x);
    *y = x-1;
    print(x);
}
void main(void)
{
    x=5;
    P(&x);
    print(x);
    getchar();
}
int x;
void Q(int z)
{
    z += x;
    print(z);
}
```

该程序的输出是
a) 12 7 6
b) 22 12 6
c) 14 6
d) 7 6

## 11. 考虑以下 C 程序（GATE CS 2004）

```c
char p[20];
char *s = "string";
int length = strlen(s);
int i;
for (i = 0; i < length; i++)
    p[i] = s[i];
printf("%s", p);
```
（注：原文中关于10和11题的OCR文本较为混乱，已根据标准GATE逻辑进行了修复整理。）

## 12. 考虑以下 C 程序（GATE CS 2004）

```c
void swap(int a, int b)
{
    int temp;
    temp = a;
    a = b;
    b = temp;
}
```
交换 x 和 y 的值
a) 调用 swap(x, y)
b) 调用 swap(&x, &y)
c) swap(x, y) 不返回任何值
d) 按值传递 swap(x, y)

## 13. 考虑以下函数：（GATE CS 2004）

```c
int f(int n)
{
    static int i = 1;
    if(n >= 5)
        return n;
    i++;
    return i;
}
```
f(1) 返回的值是
a) 5
b) 6
c) 7
d) 8

## 14. 考虑以下程序，用于将一个整数反转以得到一个新的整数。

```c
int rev = 0;
while (n > 0)
{
    rev = rev*10 + n % 10;
    n = n / 10;
}
```
第 i 次迭代后的循环不变性是：
a) rev = rev*10 + n % 10
b) n = n/10
c) rev = n
d) i++

## 15. 考虑以下：（GATE CS 2004）

```c
int main() {
    int x, y, m;
    scanf("%d %d", &x, &y);
    while (m != 0)
    {
        m = x;
        x = y;
        y = m;
    }
    printf("%d %d", x, y);
}
```

