

区域（该区域仅可读）。现在，我们正尝试将 `str2` 复制到 `str1`；两者都在只读区域，这是可能的。会发生运行时错误。

+ 54. a

解释：不需要。

+ 55. 1000, 1024, 1024, 1048, 1048

解释：

| a0 | 7 | 6 | 5 |
|---|---|---|---|
| | 1000 | 1004 | 1008 |
| | 4 | 3 | 2 |
| 1012 | 1016 | 1020 | |

| a1 | 1 | 8 | 9 |
|---|---|---|---|
| | 1024 | 1028 | 1032 |
| | 10 | 11 | 12 |
| 1036 | 1040 | 1044 |

> (i) a = 1000;
> (ii) a+1 = 1024;
> 我们在之前的分组问题中讨论过

> (iii) a[1]+2 -> 1024+2 -> 1048;
> 我们跳过了一行，它们是这样做的
> 我们跳过了加到 1024 的两行。我们并不是在选择两行。

> (iv) a[1] -> 1048;
> 正如所示，由于微小差异，我们在这里选择时跳过了 2 行。

+ 56. d

解释：语句：`int *s = "hello";` 是可以，不会报告错误。`int *s = "hello";` 和 `char *s = "hello";` 之间的唯一区别是步长。我们讨论过多次，整数指针和字符指针的步长分别为 4 和 1。当我们通过字符指针访问 `"s[1]"` 时，它将返回 'e'。当我们使用整数指针访问 `"s[1]"` 时，它将返回 'o'。

+ 57. d

解释：一个简单的练习题，我们讨论过几个类似的问题，不需要解释。

+ 58. 1000, 1016, 1032, 1012, 1032, 3, 1000, 1000, 1096。

解释：一个练习题。

+ 59. a

解释：不需要解释。

+ 60. b, e

解释："hello" 仍然在只读内存中。我们只是在第3行丢失了对 "hello" 的引用。

# 你的意图比努力更。

# 第4 组问题

# 'C' 题数量：60

# 其他重要面试题：15

![](img/192d581e3a01f0e6c194cfc2ff02d9f1_161_0.png)

## 1. 下述程序的输出是什么？

```c
//基础函数指针示例
#include<stdio.h>
int fun(int x, int y)
{
    int z = x*y+x+y*x-y;
    return z;
}
int main()
{
    int (*fun_ptr) (int, int); //line 1
    fun_ptr = fun;
    int x = (int)fun_ptr(1, 2);
    printf("%d", x);
    return 0;
}
```

(a) 3
(b) 4
(c) 1
(d) 第1行语法错误

## 2. 下述程序的输出是什么？

```c
#include<stdio.h>
int fun1(int x, int y)
{
    return x+y;
}
int fun2(int x, int y)
{
    return x*y;
}
int main()
{
    int (*fun_ptr[2])(int, int);
    fun_ptr[0] = fun1;
    int x = fun_ptr[0](4, 5);
    fun_ptr[1] = fun2;
    int y = fun_ptr[1](4, 5);
    printf("%d %d", x, y);
    return 0;
}
```

(a) 4 5
(b) 20 9
(c) 9 20
(d) 以上均不是

## 3. 下述语法中表示固定指针地址的是？

- (a) const <type> *ptr
- (b) <type> *const ptr
- (c) <type> const *ptr
- (d) <type> const *const ptr

## 4. 声明和初始化函数指针的正确方法是：

- (a) int (*f_pointer)(int, int) = fName;
- (b) int *f_pointer(int, int) = fName;
- (c) int *f_pointer(int, int) = &fName;
- (d) int (*)*f_pointer(int, int) = fName;

## 5. 下述程序的输出是什么？

```c
#include<stdio.h>
void fun(char *k)
{
k++;
k[2] = 'm';
printf("%c ", *k);
}
int main()
{
char str[] = "hello";
fun(str);
printf("%c ", *str);
printf("%s ", str);
return 0;
}
```

- (a) e h helmo
- (b) e h hello
- (c) h hemlo
- (d) e h helmo

## 6. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
int a = 7;
int *b = &a;
int **c = &a;
printf("%d, %u, %u", a, *b, *c);
return 0;
}
```

(a) 7, 7, 7
(b) 7, 7, 垃圾值
(c) 7, 垃圾值, 垃圾值
(d) 编译错误

## 7. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
int a[4] = {10, 20, 30, 40};
int *p = a;
int **r = &p;
p++;
(**r)++;
printf("%d", **r);
return 0;
}
```

(a) 11
(b) 21
(c) 31
(d) 20

## 8. 对于给程序，下述哪个说法正确？

```c
#include<stdio.h>
int main()
{
int x=4, y=6, z=7;
int *p1 = &x, *p2 = &y, *p3 = &z;
int **ptr = &p2;
p2 = p1;
p3 = p2;
return 0;
}
```

(a) ptr 指向 x;
(b) ptr 指向 y;
(c) ptr 指向 z;
(d) 编译错误

## 9. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
int a[5] = {50, 60, 70, 80, 90};
int *p = a;
int *q = &a[2];
p++;
int **ptr = p+1;
**ptr;
printf("%d %d", p[2], *q);
return 0;
}
```

(a) 80 70
(b) 80 71
(c) 80 74
(d) 80 5

## 10. 下述哪个声明会引发运行时错误？

- (a) int **ptr = &ptr;
- (b) int **ptr = &ptr;
- (c) int **ptr = **ptr;
- (d) int **ptr = ptr;

## 11. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
char str[] = "India";
const char *ptr;
ptr = str;
ptr++;
//*ptr;
printf("%s", ptr);
return 0;
}
```

(a) India
(b) ndia
(c) dia
(d) 错误-不允许更新常量

## 12. 如果我们取消注释掉的行，输出是什么？

(a) ndia
(b) ndia
(c) dia
(d) 错误-不允许更新常量

## 13. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
char str[] = "India";
char *ptr;
ptr = str;
ptr++;
printf("%s", ptr);
return 0;
}
```

(a) India
(b) ndia
(c) dia
(d) 错误-不允许更新常量

## 14. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
char str[] = "Hello";
const char * ptr;
ptr = str; //line 3
//ptr++; //line 4
++ptr; //line 5
printf("%s", ptr);
return 0;
}
```

(a) Hello
(b) 错误-第3行
(c) 错误-第5行
(d) (b) 和 (c) 都是

## 15. 如果我们取消注释掉的行，输出是什么？

(a) Hello
(b) 错误在第4行
(c) ello
(d) 错误在第3行、第4行和第5行

## 16. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
char str[] = "India";
char *ptr;
ptr = str;
ptr++;
**ptr;
printf("%s", ptr);
return 0;
}
```

(a) ndia
(b) ndia
(c) mdia
(d) odia

## 17. 如果数组的基地址是 1000，确定下述程序的输出。

```c
#include<stdio.h>
void fun(int arr[])
{
    printf("%u %u %u", *(arr+2)+1);
}
```
(注：原文示例代码不完整，此处根据逻辑保留翻译)

## 18. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int a[3] = {5, 6, 7};
    printf("%d", a);
    return 0;
}
```
(注：原文代码块存在格式混乱，此处按样翻译)

## 19. 下述程序的输出是什么？

```c
#include<stdio.h>
#include<string.h>
int main()
{
    char str[] = "India";
    char s[5];
    int i=0, len = strlen(str);
    while(len > 0)
    {
        s[i++] = str[--len];
    }
    s[i] = '\0';
    printf("%s ", s);
    return 0;
}
```

(a) India
(b) aidnl
(c) blank display
(d) infinite loop

## 20. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    char str1[] = "India";
    char str2[] = "Bharat";
    char *s1 = str1;
    char *s2 = str2;
    while(*s1)
    {
        *s2++ = *s1++;
    }
    printf("%s %s", str1, str2);
    return 0;
}
```

(a) India India
(b) Indiaiat
(c) India Bharat
(d) India Bl

## 21. 下述哪个函数给出 'x' 和 'y' 的和？

- (i) int add(int x, int y)
{
  return printf("%*c%c","",x,y);
}

- (ii) int add(int x, int y)
{
  while (y != 0 )
  {
    int c = x&y;
    x = x^y;
    y = c << 1;
  }
  return x;
}

- (iii) int add(int x, int y)
{
  if (y == 0)
  return x;
  else
  return add(x^y , (x&y)<<1 );
}

(a) 仅 i
(b) 仅 ii
(c) 仅 iii
(d) i 和 iii
(e) i, ii,  iii
(f) ii 和 iii
(g) i 和 iii (原文重复项)
(h) 以上都不是

## 22. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int i = -3<<4;
    printf("%x", i);
    return 0;
}
```

(a) abcdef33
(b) fffffff
(c) ffffffd1
(d) fffffff

## 23. 下述程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int i= - -2;
    printf("%d",i);
    return 0;
}
```

(a) 0
(b) 1
(c) 2
(d) 错误-需要左值

