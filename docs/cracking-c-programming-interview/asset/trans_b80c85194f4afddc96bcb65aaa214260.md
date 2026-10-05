

# 联合体 obj

(i) obj.a = 100;

![](img/192d581e3a01f0e6c194cfc2ff02d9f1_288_0.png)

printf("%s",obj.b); -> d (字符值 100)

# 联合体 obj

(ii)obj.b[0] = 'a';

![](img/192d581e3a01f0e6c194cfc2ff02d9f1_288_1.png)

# 联合体 obj

(iii)obj.b[1] = 'b';

![](img/192d581e3a01f0e6c194cfc2ff02d9f1_288_2.png)

printf("%d %s",obj.a,obj.b); -> 25185 ab

世界上没有什么是不屈服于你的意志力的。

# 第 7 组问题

# 'C' 题数量: 60

# 其他重要面试题: 15

![](img/192d581e3a01f0e6c194cfc2ff02d9f1_289_0.png)

# 1. 下述程序的输出是什么？

```
#include<stdio.h>
union unit {
  char a[4];
  int b;
} obj;
int main() {
  obj.b = 4;
  obj.a[2] = 'A';
  obj.b = obj.b >> 8;
  printf("%s",obj.a);
  return 0;
}
```

(a) 40A
(b) 错误 - 编译时
(c) A
(d) 什么都不会打印

# 2. 下述程序的输出是什么？

```
#include<stdio.h>
union unit {
    obj;
}
struct student {
    sl;
}
int main() {
{
    printf("%d %d",sizeof(obj) , sizeof(sl));
    return 0;
}
```

(a) 0 0
(b) 0 1
(c) 1 0
(d) 1 1

# 3. 下述代码的输出是什么？

```
#include<stdio.h>
int main() {
{
    const int i = 10;
    const int j = 20;
    const int *p = &i;
    p = &j;
    printf("%d",*p);
    return 0;
}
```

(a) 错误 - 编译时
(b) 错误 - 运行时
(c) 10
(d) 20

# 4. 下述程序的输出是什么？

```c
#include<stdio.h>
union unit {
int i;
char str[10]; //line2
} obj;
int main()
{
obj.i = 0;
printf("%s",obj.str);
obj.str = "hello";//line 5
printf("%s",obj.str);
return 0;
}
```

(a) hello
(b) hello
(c) 错误 - 编译时
(d) 错误 - 运行时

# 5. 对上述程序代码提出修改建议以便在 main() 函数中向 enum 赋值字符串 "hello"？

# 6. 下述程序的输出是什么？

```c
#include<stdio.h>
union {
int i;
char j;
} obj;
int main()
{
obj.j = 'a';
printf("%d",sizeof(obj));
return 0;
}
```

(a) 1
(b) 垃圾值
(c) 4
(d) 取决于编译器

# 7. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int i = 64 , j = 5 , res1 , res2;
    res1 = res2 ; j = i;
    for( ; j > 0; j--)
    {
        res1 = res1 >> 1;
        res2 = res2 << 1;
    }
    printf("%d %d",res1,res2);
    return 0;
}
```

(a) 2 2048
(b) 4 2048
(c) 1 1024
(d) 1 1048

# 8. 下述程序的输出是什么？

```c
#include<stdio.h>
union {
    int i;
    static char j;
} obj;
int main()
{
    obj.i = 65;
    printf("%d",sizeof(obj));
    return 0;
}
```

(a) 错误 - 编译时
(b) 垃圾值
(c) 4
(d) 1

# 9. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    const int i = 10;
    int *p = &i;
    *p = 20;
    printf("%d %d",i,*p);
    return 0;
}
```

(a) 10 20
(b) 10 20
(c) 20 20
(d) 错误 - 编译时

# 10. 下述程序的输出是什么？

```c
#include<stdio.h>
int i;
void fun()
{
    printf("%d ",i);
    i++;
}
int main()
{
    const int *p = &i;
    fun();
    printf("%d",*p);
    return 0;
}
```

(a) 垃圾值
(b) 错误 - 编译
(c) 0 1
(d) 0 0

# 11. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int i = 10 , j = 20;
    int *const p = &i; //line1
    *p = 20; //line2
    printf("%d %d",i,*p);
    return 0;
}
```

(a) 10 20
(b) 20 20
(c) line1 处错误
(d) line2 处错误

# 12. 下述程序的输出是什么？

```c
#include<stdio.h>
int func()
{
    static int i = 10;
    int j = i+1;
    return j;
}
int main()
{
    int i , j = 0;
    for(i = 0; i <= 5 ; i++)
        j += func();
    printf("%d", j);
    return 0;
}
```

(a) 55
(b) 0
(c) 编译时错误
(d) main 函数中错误

# 13. 下述程序的输出是什么？

```c
#include<stdio.h>
#include<stdlib.h>
int* fun() {
    const int *i = calloc(sizeof(int),1);
    return i;
}
int main() {
    int *p = fun();
    printf("%d",*p);
    *p = 10;
    printf("%d",*p);
    return 0;
}
```

(a) fun() 中错误
(b) main() 中错误
(c) 垃圾值 10
(d) 0

# 14. 下述程序的输出是什么？

```c
#include<stdio.h>
int main() {
    int *const i = (int*)malloc(sizeof(int)); //line1
    *i = 10; //line2
    printf("%d",*i);
    return 0;
}
```

(a) line1 处错误
(b) line2 处错误
(c) 10
(d) 垃圾值

# 15. 下述程序的输出是什么？

```c
#include<stdio.h>
#include<string.h>
int main()
{
    char const name[20]; //line1
    char *p = name; //line2
    strcpy(p, "john"); //line3
    printf("%s", name);
    return 0;
}
```

(a) line1 处编译错误
(b) line2 处编译错误
(c) line3 处编译错误
(d) john

# 16. 下述程序的输出是什么？

```c
#include<stdio.h>
union unit {
    int i;
    char k;
};
int main()
{
    union unit obj = {10, 0}; //line 1
    if(obj.i == 0)
        printf("hi");
    else
        printf("bye");
    return 0;
}
```

(a) hi
(b) bye
(c) 编译时错误
(d) 运行时

# 17. 下述程序的输出是什么？

```c
#include <stdio.h>
int main()
{
    char a;
    char arr[10] = {1, 2, 3, 4, 5, 6, 9, 8};
    a = (arr + 1)[5]; //line 3
    printf("%d\n", a);
    return 0;
}
```

(a) 5
(b) 6
(c) 9
(d) 以上均不是

# 18. 下述程序的输出是什么？

```c
#include<stdio.h>
struct student{
    char name[10];
};
int main()
{
    struct student s1;
    strcpy(s1.name , "john");
    printf("%s",s1.name);
    return 0;
}
```

(a) 编译时错误
(b) 运行时错误
(c) john
(d) 垃圾值

# 19. 下述程序的输出是什么？

(a) 垃圾值
(b) 10 20
(c) 10 10
(d) 链接时错误

# 20. 下述程序的输出是什么？

```c
#include<stdio.h>
extern int i;
int main()
{
    extern int i; //line 1
    i = 10; //line 2
    printf("%d",i);
    return 0;
}
```

(a) 10
(b) line 2 处错误
(c) 垃圾值
(d) 0

# 21. 下述程序的输出是什么？

```c
#include<stdio.h>
int i = 10;
int fun();
int main()
{
    extern int i;
    int p , res = 0;
    for(p = 1; p<= 2; p++)
    res += fun();
    printf("%d ",res);
    printf("%d",i);
    return 0;
}
int fun()
{
    extern int i;
    return (++i);
}
```

(a) 23 12
(b) fun() 中错误
(c) main() 中错误
(d) 垃圾值 垃圾值

# 22. 下述程序的输出是什么？

```c
#include<stdio.h>
int i = 10;
int main()
{
    extern int i; //line1
    int i = 1; //line2
    printf("%d",i);
    return 0;
}
```

(a) 1
(b) 10
(c) line1 处错误
(d) line2 处错误

# 23. 下述程序的输出是什么？
给出两个文件分别为 one.c 和 two.c。

```
one.c
----
#include<stdio.h>
extern int i;
int i = 10;
extern int p;
int main() {
    extern int i;
    printf("%d %d",i,p);
    return 0;
}
```

two.c
----
int p = 20;

```

(a) 10 20
(b) two.c 编译错误，缺少头文件和/或 main()
(c) one.c 编译错误，无效使用了 extern i 和/或 int p
(d) 运行时错误

# 24. 下述程序的输出是什么？
给出两个文件分别为 one.c 和 two.c。

one.c
```
#include<stdio.h>
extern int i;
int i = 10;
extern int p;

int main() {
    extern int i;
    printf("%d %d",i,p);
    return 0;
}
```

two.c
```
#include<stdio.h>
int p = 20;
int main()
{
    printf("%d",p);
    return 0;
}
```

(a) 10 20 或 20 10，取决于编译器实现
(b) 重复包含头文件 <stdio.h> 错误
(c) 重复定义 main() 错误
(d) (b) 和 (c) 都正确

