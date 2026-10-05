

(c) error- 运行时
(d) 10 4

# 15. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    const a = 10; //line1
    const b = 2.5; //line2
    printf("%d %d",a,b);
    return 0;
}
```
(a) line 1 错误
(b) line 2 错误
(c) 10 2.5
(d) 10

# 16. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    register int i = 10;
    int *p = &i;
    printf("%d",*p);
    return 0;
}
```
(a) 10
(b) error- 编译时错误
(c) error- 运行时错误
(d) 垃圾值

# 17. 以下程序的输出是什么？

```c
void two()
{
  static int r = 2;
  r++;
  printf("%d ", r);
}

void one() {
  int r = 5;
  two();
  printf("%d ", r);
}

#include<stdio.h>
int r = 10;
int main() {
  r = 2;
  one();
  two();
  printf("%d", r);
  return 0;
}
```
(a) 3 5 4 2
(b) 3 5 3 2
(c) error- 编译程序错误
(d) 3 4 5 2

# 18. 确定以下程序的输出？

```c
#include<stdio.h>
int main() {
  char a=-10;
  int b=-5;
}
```

# 19. 确定以下程序的输出？

```c
#include<stdio.h>
int main()
{
    char *str1="abcd";
    char str2[]="abcd";
    printf("%d %d",sizeof(str1),sizeof(str2));
    return 0;
}
```

# 20. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    char *p;
    printf("%d %d",sizeof(*p),sizeof(p));
    return 0;
}
```
(a) 4
(b) 1
(c) 4
(d) 以上皆非

# 试卷 - 2

1. b
2. c
3. 这是一个定义，'x' 是指向整数数组的指针。
4. c
5. b
6. a
7. a
8. a
9. d
10. 1000 1000 2 1024 1008 3 1072 3 1048
11. b
12. c
13. d
14. d
15. d
16. b
17. a
18. hello
19. 4 5 5
20. a

# 试卷 - 3
题目数量: 22
最大时间: 45 min.

1. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int i=5;
    if(i<5);
    printf("hello");
    return 0;
}
```
(a) 什么都没有打印
(b) hello
(c) hello 无限次
(d) error- 编译时错误

2. 以下程序的输出是什么？

```c
#include<stdio.h>
#define num(a) a
int main()
{
    int a=1;
    switch(a)
    {
        case num(2):
            printf("yes ");
        case num(1):
            printf("no ");
            break;
    }
    switch(a)
    {
        case 1:
            printf("%d ", a);
        case 2:
            printf("%d ", a);
        case 3:
            printf("%d ", a);
        default:
            printf("%d", a);
    }
    return 0;
}
```
(a) yes 1 1 1
(b) no 1 1 1
(c) yes no 1 1 1
(d) case label 错误

3. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int x=1;
    printf("%d, %d", 74*x, x++);
    return 0;
}
```
(a) 74, 78
(b) 1, 75
(c) 74, 75
(d) 取决编译器

4. 确定以下程序的输出？

```c
#include<stdio.h>
int main()
{
    char str[]="India";
    int i=0;
    while(str[i])
    {
        printf("\n%c %c %c %c ", str[i], *(str+i), *(i+str), i[str]);
        i++;
    }
    return 0;
}
```

5. 确定以下程序的输出？

```c
#include<stdio.h>
int main()
{
    char *cptr;
    void *vptr, v; // line 2
    c=10; v=0;
    cptr=&c; vptr=&v;
    printf("%c %d",c,v); // line 5
    return 0;
}
```
(a) 10 0
(b) 10 垃圾值
(c) line 2 和 line 5 错误，'c' 的大小未知
(d) 10 10

6. 以下程序的输出是什么？

```c
#include<stdio.h>
int counter(int i)
{
    static int count = 0;
    count = count + i;
    return count;
}
int main() {
  int i, j;
  for (i = 0; i <= 5; i++)
  j = counter(i);
  printf("%d\n", j);
  return 0;
}
```
(a) 10
(b) 15
(c) 6
(d) 7

7. 以下程序的输出是什么？

```c
#include<stdio.h>
#define x 0abcdef12
int main() {
  int i=x;
  char *p = &i;
  printf("%x %d", p[0], p[0]);
}
```
(a) 12 -17
(b) 12 18
(c) 12 12
(d) 18 18

8. 以下程序的输出是什么？

```c
#include<stdio.h>
#define MAN(x,y) (x)>(y)
int main()
{
    int i=10;
    int j=5;
    int k=0;
    k=MAN(i++,++j);
    printf("%d %d %d",i,j,k);
    return 0;
}
```
(a) 12 6
(b) 10 5
(c) 12 7
(d) 11

9. 确定以下程序的输出？

```c
#include<stdio.h>
#include<stdlib.h>
int a;
int main()
{
    char *p1="India";
    char *p2;
    p2=(char *)malloc(20);
    p2=p1;
    printf("%s",p2);
    return 0;
}
```
(a) 没有打印
(b) India
(c) 垃圾值
(d) line 4 错误

10. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int a=5;
    int x=a++;
    printf("%d",x);
    return 0;
}
```
(a) 4
(b) 5
(c) 取决编译器
(d) 编译时错误

11. 以下程序的输出是什么？

```c
#include <stdio.h>
int main()
{
  static int a;
  int x = 5;
  while( x-- != a);
  printf("%d ", x);
  return 0;
}
```
(a) -1 3
(b) 5 4
(c) 3 2
(d) 5

12. 以下程序的输出是什么？

```c
#include <stdio.h>
void fun1() {
    printf("hello");
}
void fun2() {
    printf("world");
}
int main()
{
    fun1();
    fun2();
    return 0;
}
```
(a) world10
(b) 取决编译器
(c) hello10
(d) 编译时错误

13. 以下程序的输出是什么？

```c
#include <stdio.h>
int main()
{
    char *p="India";
    printf("%c ", p[2]);
    return 0;
}
```
(a) l
(b) n
(c) d
(d) i

14. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    if (sizeof(int) > 2)
        printf("Love");
    else
        printf("India");
    return 0;
}
```
(a) Love
(b) India
(c) 没有打印
(d) line 1 错误

15. 以下程序的输出是什么？

```c
#include<stdio.h>
#include<stdlib.h>
int c;
int main()
{
    int b = 10;
    c = (int)malloc(b);
    printf("%d",c);
    return 0;
}
```
(a) 垃圾值
(b) 未定义符号 'c'
(c) 15
(d) 16

16. 以下程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    const int a = 5;
    int i = 5;
    int *p = &a;
    while(i)
    {
        switch(*p)
        case 5
            printf("%d ",a);
            i--;
            *p = i;
            default :
                printf("exit");
                exit(0);
    }
    return 0;
}
```
(a) line 5 错误
(b) 54321 exit
(c) 543210 exit
(d) 5 exit

