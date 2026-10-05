

```c
#include<stdio.h>
#include<stdlib.h>
int main() {
    int *display(int, int);
    int (*f)(int, int);
    f = display;
    int *x = (*f)(3, 4);

    printf("%d", *x);
}
int *display(int x, int y) {
    int *i = (int*)malloc(sizeof(int));
    *i = 100+x+y;
    return i;
}
// O/p: 107
```

60. Nil (空)

解释：

```c
#include<stdio.h>
#include<stdlib.h>
int main()
{
    int *display(int, int);
    int *(*f)(int, int);
    f = display;

    void (*funptr)(int, int*(*f)(int, int));
    void show(int, int*);
    funptr = show;
    (*funptr)(3, (*f)(3, 4));
    return 0;
}
void show(int a, int *b)
{
    printf("%d", a+*b);
}
int *display(int x, int y)
{
    int *i = (int*)malloc(sizeof(int));
    *i = 100+x+y;
    return i;
}
// O/p: 110
```

不要让你的教育干扰了你的学习。

# 第 6 组题目

# C 语言题目数量: 60

# 其他重要面试题: 20

![](img/192d581e3a01f0e6c194cfc2ff02d9f1_248_0.png)

- 1. 下面程序的输出是什么？
  - (a) 4 300 20
  - (b) 4 300 1
  - (c) 4 10 2
  - (d) error- 编译错误

- 2. 下面程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int x = 10 , y = 10 , z = 10;
    x = y == z && 5;
    printf("%d",x);
    return 0;
}
```

  - (a) 0
  - (b) 1
  - (c) error- 编译错误
  - (d) 10

# 3. 下面程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int a = 10;
    a = 5 , 100;
    printf("%d",a);
    return 0;
}
```

  - (a) 10
  - (b) 5
  - (c) 100
  - (d) error- 编译错误

# 4. 下面程序的输出是什么？

```c
#include<stdio.h>
#include<string.h>
int main()
{
    int i = 0;
    char c[] = "hello";
    char d[] = "India";
    char b[] = i ? c : d ; //第 3 行
    printf("%s",b);
    return 0;
}
```

  - (a) India
  - (b) hello
  - (c) error- 编译错误
  - (d) 垃圾值

# 5. 下面程序的输出是什么？

```c
#include<stdio.h>
int main() {
  int a = 0 , b = 20 ; //第 1 行
  b = (110 , 120);
  printf("%d",b);
  return 0;
}
```

  - (a) 20
  - (b) 10
  - (c) 110
  - (d) 120
  - (e) error- 编译错误。

# 6. 下面程序的输出是什么？

```c
#include<stdio.h>
int main() {
  int a = 10;
  a++;
  (a++)++)++; //第 3 行
  printf("%d",a);
  return 0;
}
```

  - (a) 13
  - (b) 12
  - (c) error- 需要左值 (lvalue required)
  - (d) error- 运行时错误

# 7. 下面程序的输出是什么？

```c
#include<stdio.h>
#include<string.h>
int main()
{
    int i = 0;
    char c[] = "hello";
    char d[] = "India";
    char * b = i ? c : d; //第 3 行
    printf("%s",b);
    return 0;
}
```

  - (a) India
  - (b) hello
  - (c) error- 编译错误
  - (d) 垃圾值

# 8. 下面程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int b = 20;
    int c = sizeof(scanf("%d",&b));
    printf("%d %d",b,c);
    return 0;
}
```

  - (a) error- 编译错误
  - (b) 20 4
  - (c) 30 4

# 9. 下面程序的输出是什么？

```c
#include<stdio.h>
#include<string.h>
int main()
{
    int i = 1;
    char c[] = "hello";
    char d[] = "India";
    char *b;
    b = i ? c : d; //第 3 行
    printf("%s",b);
    return 0;
}
```

  - (a) India
  - (b) hello
  - (c) error- 编译错误
  - (d) 垃圾值

# 10. 下面程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int a = 1 , b = 0;
    int c = ++(b) | a++;
    printf("%d %d %d",a,b,c);
    return 0;
}
```

  - (a) 1 2 1
  - (b) 2 1
  - (c) 2 2
  - (d) error- 需要左值 (lvalue required)

# 11. 考虑以下声明：

  - (i) short i=10;
  - (ii) static i=10;
  - (iii) unsigned i=10;
  - (iv) const i=10;
  - (a) i, ii, iv
  - (b) ii, iii, v
  - (c) i, iii, iv
  - (d) i, ii, iii

# 12. 下面程序的输出输出？

```c
#include<stdio.h>
int main() {
    int x = 10 , y = 10 , z = 10;
    printf("%d %d %d",x,y,z);
    return 0;
}
```

  - (a) 8 16 10
  - (b) 10 10 10
  - (c) error- x 的使用无效
  - (d) 0 10 10

# 13. 下面哪一个会导致编译错误？

```c
#include<stdio.h>
#define display(A, B) {
    printf(A , B);
}
int main() {
    display("%d",10);
    return 0;
}
```

```c
#include<stdio.h>
#define display(A,B) do{
    printf(A , B);
}while(1 == 2)
int main() {
    display("%d",10);
    return 0;
}
```

```c
#include<stdio.h>
#define display(A,B) \
    printf(A , B);
}
int main() {
    display("%d",10);
    return 0;
}
```

  - (d) 以上均不是

# 14. 下面程序的输出是什么？

```c
#include<stdio.h>
#define cal(a,b,c,d) a*b*c+d
int main() {
    int a = 1 , b = 2 , c = 3 , d = 4 , e = 5;
    int f = e * cal(a,b,c,d); //第 2 行
    printf("%d",f);
    return 0;
}
```

  - (a) 55
  - (b) 15
  - (c) 16
  - (d) 54

# 15. 下面程序的输出是什么？

```c
#include<stdio.h>
#define sqrt(x) x+++x
int main() {
    int x = 10;
    int y = sqrt(x); //第 2 行
    printf("%d %d",x,y);
    return 0;
}
```

  - (a) 13 20
  - (b) 13 28
  - (c) 13 15
  - (d) error- 编译错误

# 16. 下面程序的输出是什么？

```c
#include<stdio.h>
#include<string.h>
#define type_char char*
int main() {
    type_char a;
    type_char b;
    char c[10], d[10];
    strcpy(c, "hello");
    strcpy(d, "India");
    a = c;
    b = d;
    printf("%s %s", &a[2], &b[2]);
    return 0;
}
```

  - (a) 垃圾值
  - (b) lo India
  - (c) error- 编译错误
  - (d) error- 运行时错误

# 17. 下面程序的输出是什么？

```c
#include<stdio.h>
#include<string.h>
#define type_char char*
int main()
{
    type_char a;
    type_char b;
    char c[10], d[10];
    strcpy(c, "hello");
    strcpy(d, "India");
    a = c;
    b = d;
    printf("%c %c", a[2],b[2]);
    return 0;
}
```

  - (a) l d
  - (b) lo- 编译错误
  - (c) error- 运行时错误

# 18. 下面程序的输出是什么？

```c
#include<stdio.h>
typedef char *str;
int main()
{
    str a, b;
    char A[10], B[10];
    strcpy(A,"hello");
    strcpy(B,"world");
    a = A; b = B;
    printf("%c %c", a[2], b[2]);
    return 0;
}
```

  - (a) l r
  - (b) 垃圾值
  - (c) error- 编译错误
  - (d) error- 运行时错误

# 19. 下面程序的输出是什么？

```c
#include<stdio.h>
#define cal(a,b) a = b++
int main()
{
    int a = 1 , b = 5;
    cal(a , 2); // 第 2 行
    printf("%d",a);
    printf("%d",b);
    return 0;
}
```

  - (a) 25
  - (b) 23
  - (c) 35
  - (d) error- 编译错误

# 20. 下面程序的输出是什么？

```c
#include<stdio.h>
int x = 2;
#if Y == 2 //第 3 行
x = 5; //第 4 行
#else
x = 6; //第 6 行
#endif
int main()
{
    printf("%d",x);
    return 0;
}
```

  - (a) 2
  - (b) 5
  - (c) 6
  - (d) error- 编译错误

# 21. 下面程序的输出是什么？

```c
#include<stdio.h>
#define 100
int foo() {
    printf("%d",a);
    return 0;
}
int main() {
    int b = a; //第 10 行
    #define 200
    printf("%d",a); //第 13 行
    foo();
    return 0;
}
```

  - (a) 100 200 200
  - (b) 100 200
  - (c) 200 200
  - (d) 宏重复定义

# 22. 下面程序的输出是什么？

```c
#include<stdio.h>
#include<string.h>
void strcpy(char *p, const char *q[]) {
    while(*p++ = *q++);
}
int main() {
    char a[10];
    char b[] = "masters";
    strcpy(a, b);
    printf("%s",a);
    return 0;
}
```

  - (a) hello
  - (b) masters
  - (c) hello masters
  - (d) 都没有打印

# 23. 下面程序的输出是什么？

```c
#include<stdio.h>
#define abc main
int main()
{
    int abc = 10;
    static int i = 1;
    while(abc > 5)
    {
        i++;
        abc--;
    }
    i++;
    if(abc == 5)
    {
        abc--;
        i++;
    }
    printf("%d",i);
}
```

  - (a) 9
  - (b) 8
  - (c) 5
  - (d) error- 编译错误

# 24. 下面程序的输出是什么？

```c
#include<stdio.h>
#define fun1 fun2 //第 2 行
#if x == 2 //第 3 行
#define fun2 fun3 //第 4 行
#else
#define fun2 fun4 //第 6 行
#endif
int main()
{
    int fun1 = 1 , fun2 = 2 , fun3 = 3 , fun4 = 4; //第 10 行
    fun1 = fun2 + fun1;
    printf("%d",fun1);
    return 0;
}
```

  - (a) 8
  - (b) 6
  - (c) error- 编译错误
  - (d) error- 运行时错误

# 25. 下面程序的输出是什么？

```c
#include<stdio.h>
#define fun1 fun2
#define x 1
#if x == 1
#define fun2 fun3
#else
#define fun2 fun4
#endif

int main()
{
    int fun1 = 1 , fun2 = 2 , fun3 = 3 , fun4 = 4;
    fun1 = fun2 + fun1;
    printf("%d",fun1);
    return 0;
}
```

