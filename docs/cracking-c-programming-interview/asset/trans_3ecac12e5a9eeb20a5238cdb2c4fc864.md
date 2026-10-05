

(b) 0 1
(c) 1 2
(d) 0 -9

# 试卷-3 答案

+ 1. b
2. b
3. d
4. IIII
   nnnn
   dddd
   iiii
   aaaa
5. c
6. b
7. b
8. c
9. a
10. c
11. c
12. b
13. c
14. b
15. b
16. d
17. 2 2 2 3 4 5 6 6
18. b
19. d

+ 20. d
21. c
22. d

# 试卷 - 4

题目数量：23，限时：45 min。

# 1. 下面程序的输出结果是什么？

```c
#include<stdio.h>
int main()
{
    int i = 4;
    while(i)
    {
        switch(i)
        {
            case 1: printf("%d");
```

+ (a) while 循环将无限执行
(b) 4 3 2 1
(c) 语法错误
(d) 4 3

# 2. 下面程序的输出结果是什么？

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
int main()
{
    char a[];
    char *p="hello India";
    char *q = &a;
    a = malloc(strlen(p)); //line 1
    strcpy(a,p); //line 2
    printf("%s %s ",p,q);
    return 0;
}
```

+ (a) 第 1 行错误
(b) 第 2 行错误
(c) hello India <某些垃圾值，因为 q 中缺少了 '0'。
(d) hello India

# 3. 下面程序的输出结果是什么？

```c
#include<stdio.h>
int main()
{
    int x;
    unsigned int y=-10;
    x = ~0 - 9; //line 1
    if(x == y) //line 2
        printf("hello Bharat");
    else
        printf("hello India");
    return 0;
}
```

+ (a) hello Bharat
(b) hello India
(c) 第 1 行错误
(d) 第 2 行错误

# 4. 下面程序的输出结果是什么？

```c
int* fun() {
    static int i = 10;
    return &i;
}
int main() {
{
    int *p;
    p = fun();
    printf("%d",*p);
    return 0;
}
```

+ (a) 错误：不应返回局部变量的地址
(b) 错误：fun 的返回类型应该是 static int*
(c) 10
(d) 垃圾值

# 5. 关于函数，以下陈述中哪些是正确的？

+ (i) 函数的默认返回类型是 int。
(ii) 函数的默认返回类型是 void。
(iii) 函数可以返回结构体。
(iv) 函数可以返回枚举类型及其元素。
(v) 函数不能返回枚举。
(vi) C语言中所有类型的变量、函数和结构体都可以变成静态的。

+ (a) i, iii, v
(b) i, iv, v
(c) i, iii, iv, vi
(d) ii, iii, iv, vi

# 6. 下面程序的输出结果是什么？

```c
#include<stdio.h>
int main() {
    const enum block{a = 1 , b = 5 , Z = 1 } i = 23; //line 1
    static q = 12; //line 2
    enum block p;
    p = a;
    p += i + q; //line 3
    printf("%d",i);
    return 0;
}
```

+ (a) 第 1 行错误
(b) 第 2 行错误：无效的数据类型
(c) 第 3 行错误：无法修改 const
(d) 23

# 7. 下面程序的输出结果是什么？

+ (a) 第 1 行、第 4 行和第 5 行错误
(b) 第 4 行错误
(c) 4
(d) 0

# 8. 下面程序的输出结果是什么？

```c
#include<stdio.h>
union {
  int i;
  char j;
} obj;
int main()
{
  obj.i = 65;
  printf("%d",sizeof(obj));
  printf("%c",obj.j); //line 3
  return 0;
}
```

+ (a) 编译时错误
(b) 垃圾值
(c) 4 A
(d) 4\0

# 9. 考虑以下两个程序：

# 程序 2：

```c
#include <stdio.h>
#include <string.h>
#include<stdlib.h>
struct student {
  char name[20];
};
int main()
{
  struct student s1 , s2;
  strcpy(s1.name, "masters");
  s2 = s1;
  s1.name[2] = 'P';
  s1.name[3] = 'Q';
  printf("%s\n%s", s1.name,s2.name);
  return 0;
}
```

# 程序 1：

```c
#include <stdio.h>
#include <string.h>
#include<stdlib.h>
struct student {
    char *name;
};
int main() {
    struct student s1 , s2;
    s1.name = malloc(10);
    strcpy(s1.name, "masters");
    s2 = s1;
    s1.name[2] = 'P';
    s1.name[3] = 'Q';
    printf("%s\n%s", s1.name,s2.name);
    return 0;
}
```

比较程序 1 和程序 2 的输出。

+ (a) 相同
(b) 不同
(c) 程序 1 编译错误
(d) 程序 2 编译错误

# 10. 考虑以下程序：

# 程序 2：

```c
#include<stdio.h>
int main()
{
  char a[] = {'m','a','s','t','e','r'};
  printf("%d",sizeof(a));
  return 0;
}
```

# 程序 1：

```c
#include<stdio.h>
int main()
{
  char a[] = "masters";
  printf("%d",sizeof(a));
  return 0;
}
```

比较程序 1 和程序 2 的输出。

+ (a) 都是 7
(b) 都是 8
(c) 程序 1: 7, 程序 2: 7
(d) 程序 1: 8, 程序 2: 7

# 11. 下面程序的输出结果是什么？

```c
#include "stdio.h"
int main()
{
  char array[10];
  int i;
  printf("%d", scanf("%s", array, &i));
  return 0;
}
```
假设 scanf 输入 "India" 10

+ (a) 9
(b) 2
(c) 10
(d) 1

# 12. 下面程序会做什么？

```c
#include<stdio.h>
#include<stdlib.h>
int main()
{
    int i;
    char a[]="India";
    char *p="is great";
    char *Temp;
    Temp=a;
    a=malloc(strlen(p) + 1); //line 6
    strcpy(a,p); //line 7
    printf("%s %s",a,p);
    free(p);
    free(a);
    return 0;
}
```

+ (a) India great
(b) great India
(c) 第 6 行错误
(d) 第 7 行错误

# 13. 下面程序的结果是什么？

```c
#include<stdio.h>
#include<string.h>
char *xxx()
{
    static char xxx[10];
    return xxx;
}
int main()
{
  char *g="India";
  strcpy(xxx(),g); //line 2
  g = "great";
  printf("%s",xxx());
  return 0;
}
```

+ (a) India
(b) India great
(c) great
(d) 运行时错误

# 14. 确定下面程序的输出：

```c
#include<stdio.h>
#include<string.h>
typedef union {
  int a;
  char b[10];
  float c;
} Union;
int main()
{
  Union x,y = {100};
  x.a = 50;
  strcpy(x.b,"hello");
  x.c = 21.5;
  printf("%f ", x.c);
  printf("%d %s",y.a,y.b);
  return 0;
}
```

# 15. 下面程序的输出结果是什么？

```c
#include<stdio.h>
int main()
{
    printf("%d",sizeof(0.5));
    printf("%d",sizeof(900));
    printf("%d",sizeof('X'));
    return 0;
}
```

+ (a) 4 4
(b) 4 4
(c) 4 1

# 16. 考虑以下枚举的声明。选择正确的：

+ (i) enum college {student, teacher, staff}x;
(ii) enum college {student, teacher, staff};
(iii) enum college {student, teacher = -5, staff}x;
(iv) enum x {student, teacher, staff};

+ (a) i, iv
(b) ii, iii
(c) i, iii, iv
(d) i, ii, iii, iv

# 17. 下面程序的输出结果是什么？

```c
#include<stdio.h>
int main()
{
    signed x;
    unsigned y;
    x = 10 - 10u + 10u;
    y = x;
    if(x==y)
        printf("%d",x,y);
    else if(x!=y)
        printf("%u %u",x,y);
    return 0;
}
```

+ (a) 0 0
(b) 65536-10
(c) 0 65536
(d) 65536 0

# 18. 下面程序的输出结果是什么？

```c
#include<stdio.h>
int j = 1;
int fun(int n)
{
    static int i = 0;
    i = n;
    i += j;
    j++;
    return i;
}
int main()
{
    int i = 10, p , res = 0;
    for(p = 0 ; p <= 5 ; p++)
        res += fun(i);
    printf("%d",res);
    return 0;
}
```

+ (a) 85
(b) 116
(c) 81
(d) 编译时错误

# 19. 执行以下 C 代码将输出什么？

```c
#include<stdio.h>
int main()
{
    int a=-7;
    unsigned int b=-7u; //line 2
    if (a==b)
        printf("India");
    else
        printf("Bharat");
    return 0;
}
```

+ (a) India
(b) Bharat
(c) 第 2 行错误
(d) 错误：有符号 int 和无符号 int 无法比较

# 20. 下面程序的输出结果是什么？

```c
#include<stdio.h>
int main()
{
    int a=5;
    {
        int b=10;
        ++b;
        ++a;
        {
            int a=20;
            ++a;
            a+=b;
        }
        ++a;
        ++b;
    }
    printf("%d %d",a,b);
}
    printf("%d",a);
    return 0;
}
```

+ (a) 10 20 10
(b) 6 14 6
(c) 7 13 7
(d) 6 13 6

# 21. 下面程序的输出结果是什么？

```c
#include<stdio.h>
union unit {
 int i;
 char k;
}
int main() {
 union unit obj = {10};
 obj.k = '\0'; //line 1
 if(obj.i == 0) 
  printf("hi");
 else 
  printf("bye");
  return 0;
}
```

+ (a) hi
(b) bye
(c) 编译时错误
(d) 运行时错误

# 22. 下面程序的输出结果是什么？

```c
#include<stdio.h>
```

