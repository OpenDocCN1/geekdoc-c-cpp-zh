

(c) (i) 有效，(ii) 无效

(d) (ii) 有效，(i) 无效

## 27. 下一个程序的输出是什么？

```c
#include<stdio.h>
void fun(char a[])
{
    int i;
    for (i = 0; i < sizeof(a)/sizeof(a[0]); i++)
        a[i] = (char)i;
}
int main()
{
    int i;
    char a[] = "India";
    fun(a);
    printf("%s",a+1);
    return 0;
}
```

- (a) 01234566
- (b) 01234567
- (c) India
- (d) 什么都不会被打印。

## 28. 下一个程序的输出是什么？

```c
#include<stdio.h>
int j = 1;
int fun()
{
    static int i = 10;
    i += j;
    j++;
    return i;
}
int main()
{
    int i = 10 , p , res = 0;
    for(p = 0 ; p <= 5 ; p++)
        res += fun();
    printf("%d",res);
    return 0;
}
```

- (a) 85
- (b) 116
- (c) 65
- (d) 错误- 编译时

## 29. 下一个程序的输出是什么？

```c
#include<stdio.h>
int i = 20;
int j;
int main()
{
    printf("%d %d",i,j);
    return 0;
}
i = 10; //第8行
j = 5; //第9行
```

- (a) 20 0
- (b) 10 5
- (c) 20 5
- (d) 错误- 编译时

## 30. 下一个程序的输出是什么？

给出了两个文件 one.c 和 two.c

```bash
compile it: gcc one.c two.c
execute it: ./a.out
one.c
----
```

```c
#include<stdio.h>
static int i = 10;
extern int p;
int main()
{
    printf("%d %d",i,p);
    return 0;
}
```

two.c
-----
static int p = 100;
```

- (a) 10 100
- (b) 错误- 由于 two.c 不完整导致编译错误
- (c) 错误- 因为我们不能将全局变量声明为 static
- (d) 错误- 符号 p 在 one.c 中未声明

## 31. 下一个程序的输出是什么？

```c
#include<stdio.h>
#include<stdlib.h>
int* abc()
{
    *i = malloc(sizeof(int));
    *i = 1;
    return i;
}
int main()
{
    static int *p;
    p = abc();
    printf("%d" ,*p);
    return 0;
}
```

- (a) 1
- (b) abc() 中的错误
- (c) main() 中的错误
- (d) 垃圾值

## 32. 当 n=10 时，下一个程序的输出是什么？

```c
#include<stdio.h>
int fun(int);
int main()
{
    static auto int n;
    printf("%d",res);
    scanf("%d",&n);
    int res = fun(n);
    return 0;
}

int fun(int n)
{
    if(n == 0)
        return 0;
    else if(n == 1)
        return 1;
    else
        return (fun(n-1) + fun(n-2));
}
```

- (a) 34
- (b) 21
- (c) 55
- (d) 错误- 编译时

## 33. 下一个程序的输出是什么？

```c
#include<stdio.h>
int main()
{
    int a = 10;
    register int *p = &a;
printf("%("%",",*p); //第3行
return 0;
}
```

- (a) 10
- (b) 错误- register 不能存储内存地址
- (c) 错误- 第3行的 '*p' 无效，我们不能对寄存器内容进行解引用
- (d) 取决于编译器

## 34. 下一个程序的输出是什么？

假设：sizeof(int) = 4, sizeof(char) = 1, sizeof(double) = 8, sizeof(float) = 4

```c
#include<stdio.h>
struct student {
    int roll = 50;
    char name[50] = "john";
    double marks = 90.5;
};
int main()
{
    printf("%u",sizeof(struct student));
    return 0;
}
```

- (a) 62
- (b) 16
- (c) 17
- (d) 错误

## 35. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student {
    int roll ;
    struct student s1;
}s2;

int main() {
  s2.roll = 10;
  s1.roll = 20;
  printf("%d",s2.roll);
  return 0;
}
```

- (a) 10
- (b) 20
- (c) 错误- 编译时
- (d) 垃圾值

## 36. 下一个程序的输出是什么？

- (a) 错误- 编译时
- (b) 4 垃圾
- (c) 8 垃圾
- (d) 8 1095

## 37. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student {
  int roll;
  float marks;
} s1, s2;
int main() {
  s1.roll = 90;
  s1.marks = 95;
  s2.roll = 90;
  s2.marks = 90;
  if(s1 == s2) {
    printf("hi");
  } else {
    printf("bye");
  }
  return 0;
}
```

- (a) bye
- (b) hi
- (c) 错误- 编译时
- (d) 什么都没有打印

## 38. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student {
  int roll;
  char name[0];
};
int main() {
  struct student s1 , s2;
  s1.roll = 1;
  strcpy(s1.name, "hist");
  printf("%d %s",s1.roll, s1.name); //第5行
  s2 = s1;
  printf("%d %s",s2.roll, s2.name); //第7行
  return 0;
}
```

- (a) 错误- 编译时
- (b) 第5行 未定义行为
- (c) 第5行，第7行 未定义行为
- (d) 段错误

## 39. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student {
    int roll ;
    char name[0];
};
struct student *sl = malloc(sizeof(int)); //第1行
int main() {
    sl->roll = 1;
    printf("%d %s",sl->roll,sl->name); //第4行
    return 0;
}
```

- (a) 垃圾
- (b) 1 什么都没有打印
- (c) 第4行 错误
- (d) 第1行 错误

## 40. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student {
    int roll ;
    char name[0];
}
int main() {
    struct student *sl = malloc(sizeof(int)+10); //第1行
    sl->roll = 1;
    strcpy(sl->name, "jack"); //第2行
    printf("%d %s",sl->roll,sl->name);
    return 0;
}
```

- (a) 第1行 错误
- (b) 第2行 错误
- (c) 1 垃圾
- (d) 1

## 41. 下一个程序的输出是什么？

```c
#include<stdio.h>
#include<stdlib.h>
struct student {
    int roll;
    float marks;
    char name[0];
}
int main() {
    struct student *s1 = malloc(20);
    struct student *s2 = malloc(100);
    printf("%d %d",sizeof(s1),sizeof(s2)); //第3行
    printf("%d %d",sizeof(*s1),sizeof(*s2)); //第4行
    return 0;
}
```

- (a) 20 100 20 100
- (b) 4 4 100
- (c) 4 8
- (d) 错误- 编译输出

## 42. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct std{
    int roll;
    float marks;
} s1, s2;
int main()
{
  struct std s1 = {1, 10.5}; //第1行
  s2 = s1; //第2行
  printf("%d %f",s2.roll , s2.marks);
  if(s1 == s2) //第4行
    s2.marks = s2.marks+1;
  printf("%f",s2.marks);
  return 0;
}
```

- (a) 1 10.5 11.5
- (b) 1 10.5 10.5
- (c) 1 10.5 11.0
- (d) 错误- 编译时

## 43. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student1 {
  int a;
  int b;
  int c;
  double d;
} student1;
struct student2 {
  int a;
  int b;
  int c;
  double d;
} student2;
struct student3 {
  int a;
  int b;
  int c;
  double d;
} student3[10];
int main()
{
  printf("%d %d %d",sizeof(student1),sizeof(student2),sizeof(student3));
  return 0;
}
```

- (a) 24 24 240
- (b) 24 24 240
- (c) 24 24 24
- (d) 24 240

## 44. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student {
  int roll;
  char name[0];
} s1;
struct student2 {
  int roll;
  char name[0];
} s2;
struct student3 {
  int roll;
  char name[0];
} s3[10];
int main() {
  s1.roll = 10;
  strcpy(s1.name, "jack");
  printf("%d %s",s1.roll,s1.name);
  return 0;
}
```

- (a) 10 jack
- (b) 10 
- (c) 错误
- (d) 错误

## 45. C 中结构的默认修饰符是什么？

- (a) 私有
- (b) 公有
- (c) 保护
- (d) 外部

## 46. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student{
    unsigned int roll : 4;
    unsigned int marks : 5;
} s1;
int main() {
    s1.roll = 14;
    s1.marks = 30;
    printf("%d %ld ",s1.roll,s1.marks,sizeof(s1));
    return 0;
}
```

- (a) 14 30 4
- (b) 14 30 8
- (c) 错误- 编译时
- (d) 错误- 运行时

## 47. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student{
    int sn : 10;
    int roll : 10;
    int room : 10;
    int id : 10;
} sl1;
int main() {
    sl1.sn = 100;
    sl1.roll = 1;
    sl1.id = sl1.roll; //Lid
    printf("%d %ld",sl1.id , sizeof(sl1));
    return 0;
}
```

- (a) 错误- 结构体声明错误
- (b) 错误- L1赋值错误
- (c) 1 16
- (d) 1 8

## 48. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student{
    int a : 4;
    int b : 5;
} sl;
int main()
{
    sl.a = 10;
    sl.b = 17;
    char *p = &sl;
    printf("%d", *p);
    p++;
    printf("%d", *p);
    return 0;
}
```

- (a) 10 17
- (b) 41 64
- (c) 26 1
- (d) 41 17

## 49. 下一个程序的输出是什么？

```c
#include<stdio.h>
struct student {
    int SN;
    char grade ;
} sl;
int main() {
    sl.SN = 1;
}
```

