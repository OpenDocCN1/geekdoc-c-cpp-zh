

## 8.1.2. 成员变量的初始化

成员变量可以声明两种类型：

- 1. 使用点 (.) 运算符。
- 2. 使用箭头 (->) 运算符。

成员变量的初始化是通过结构体变量完成的。
语法如下：

- 1. `structure_variable.member_variable=value;`
- 2. `structure_variable->member_variable=value;`

什么时候使用点运算符，什么时候使用箭头运算符？如果是普通变量，使用点运算符。（参考上述示例 1 和示例 2，结构变量 `var1` 已声明为非指针变量）。如果是一个指向结构体变量地址的指针，则使用箭头运算符。（下文给出示例。）

程序 8.3 解释了箭头运算符。

```c
#include <stdio.h>
#include <conio.h>
struct student {
    char name[30];
    long int s_regno;
    int year_of_study;
    char branch[20];
} *var;
void main() {
    struct student *var=var;
    printf("Enter the details of the Student:\n");
    printf("Name: %s\n",
```

程序 8.3 箭头运算符

输出：（此输出适用于所有版本的结构体 'student'，8.1, 8.2, 8.3。）

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_136_0.png)

程序 8,1,2,3 的输出 8.3

注意：通常在 32 位处理器中，整数变量占用 4 字节，字符变量占用 1 字节，依此类推。此时这里会有一个直而易见的问题：一个结构体变量会占用多少内存？下一节将回答这个问题。

考虑以下结构体声明，

```c
struct A1
{
  char a[2];
  int b;
};
```

根据前面的说明，结构体‘A1’的大小将是 6。但令读者惊讶的是，当打印 `sizeof(struct student)` 时，它打印的输出却是‘8’。
这是什么奇迹？

原因是编译器会将成员变量对齐为填充大小（pack size）的倍数或类型大小的倍数，以较值为准。

默认填充大小通常为 8 字节。

内存占用的图示如图 8.2 所示。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_137_0.png)

图 8.2 内存布局

所以，显然存在内存浪费。

如何克服这个问题？

实用指令（Pragmatic directive）为我们完成了此。它在编译期间程序化地控制填充。

```c
#pragma pack(push,1)
#pragma pack(pop)
```

为此使用了构造语句。
为了清晰，请参考以下程序 8.4。

```c
#include<stdio.h>
#include<conio.h>
#pragma pack(push,1)
struct Al {
    char a[2];
    int b;
};
var1;
#pragma pack(pop)
void main() {
    printf("Size of the struct student is %d",sizeof(var1));
    getch();
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_138_0.png)

# 程序 8.4 Pragma 使用

## 8.1.3. 位域与结构体

关于“内存节省方法论”的另一个有趣且实用的概念是在结构体声明中使用“位域”（bit fields）。

我们可以在哪里使用这个“位域”概念？

在某些情况下，程序员非常确定变量可以取值的范围范围。例如，假设一个整数变量‘marks’将包含 [0,100] 范围内的值。

存储上限值 100 (1100100) 最大需要 7 位位。但每个数字都以 8 位或 16 位的格式存储。让我们考虑第一种：8 位表示。在我们的情况下，值 100 将以 01100100 的形式存储。因此，总共 8 位就足够我们的‘marks’情况了！

既然 1 字节就足够了，为什么要浪费 4 字节呢？

使用位域吧！！！

定义：

C 和 C++ 都允许将整数存储存储比编译器通常允许更小的内存空间。这些节省空间的结构体成员被称为字段（fields），它们的位宽可以显式声明。

## 语法：

```c
int <variable> : <number_of_bits>;
```

示例，

```c
int marks:8;
```

程序 8.5 解释了位域。

```c
#include<stdio.h>
#include<conio.h>
struct bitfieldtest {
    int marks:10;
    var var;
}
void main() {
    var.marks=100;
    printf("%d",var.marks);
    getch();
}
```

# 程序 8.5 位域

以下限制适用于位域。

- 不能有位域数组
- 不能获取位域的地址
- 我们不能拥有位域的指针
- 我们不能拥有位域的引用

注意：最大位域长度为 64 位。

## 8.1.4. 部分初始化的结构体

到为止，我们已经看到了：

- 声明结构体
- 声明结构体变量
- 在 printf() 和 scanf() 中访问结构体成员
- 在结构体中使用位域

现在，我们将研究初始化结构的方法。考虑以下代码程序 8.6。

```c
struct student 
{
    char *s_name;
    long int s_regno;
    int year_of_study;
    char * branch;
};
void main() 
{
    var.s_name="Student";
    var.s_regno=102619;
    var.year_of_study=3;
    var.branch="ECE";
    printf("Name: %s\n",var.s_name);
    printf("RegNo: %ld\n",var.s_regno);
    printf("Year: %d\n",var.year_of_study);
    printf("Branch);
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_140_0.png)

# 程序 8.6 结构初始化 – I

结构体成员 s_name, s_regno, year_of_study 和 branch 在上述代码中的初始化如下：

var.s_name="Student"
var.s_regno=102619;
var.year_of_study=3;
var.branch="ECE"

这简单吗？

在声明时进行初始化的另一种方式。程序 8.7。

```c
#include<stdio.h>
struct student 
{
    char s_name[30];
    long int s_regno;
    int year_of_study;
    char branch[10];
};
struct var={"Student",102619,3,"ECE"};
void main() 
{
    printf("Name: %s\n",var.s_name);
    printf("RegNo: %ld\n",var.s_regno);
    printf("Year: %d\n",var.year_of_study);
    printf("Branch: %s\n",var.branch);
}
```

```![](img/5bbdccabcf90cef7ee48b1b48eaa187d_141_0.png)

# 程序 8.7 结构初始化 – II

部分初始化的结构体是指只有少数成员初始化的结构体。在这种情况下，编译器会自动为未定义的成员分配默认值。

- 整数变量默认值
- 字符变量默认值
- 浮点变量默认值

关注这个主题。程序 8.8。

## 8.1.5. 结构体数组

结构体变量单独声明无法满足大多数应用（如工资处理）的需求。在这种情况下，使用结构体数组会有帮助。

声明数组数组

```c
struct student {
    char s_name[30];
    long int s_regno;
    int year_of_study;
    char branch[10];
};
```

使用结构体数组访问成员变量：

- students[0].s_name 指向第一个学生的名字
- students[1].s_regno 指向第一个学生的注册号
- students[5].branch 指向第五个学生的分支

一个程序将更清楚地解释这个概念。参考程序 8.9。

```c
#include <stdio.h>
#include <conio.h>
struct student {
    char s_name[30];
    long int s_regno;
    int year_of_study;
    char branch[10];
} var[50];
void main() {
    int index=0,yesno,i;
    do {
        printf("Enter the details of the Student[%d]:\n", index+1);
        printf("Name : "); scanf("%s", &var[index].s_name);
        printf("Reg No: "); scanf("%d", &var[index].s_regno);
        printf("Year : "); scanf("%d", &var[index].year_of_study);
        printf("Branch: "); scanf("%s", &var[index].branch);
        printf("\nWant to continue? (YES/NO: 1/0)"); scanf("%d", &yesno);
        index++;
    } while (yesno!=0);
    printf("\nThe Details of the students are......");
    printf("\nName\tREGNO\tYEAR\tBRANCH\n");
    for (i=0;i<index;i++) {
        printf("\t%s,\t", var[i].s_name);
        printf("\t%d,\t", var[i].s_regno);
    }
    printf("\t%d,\t", var[i].year_of_study);
    printf("\t%s\t\n", var[i].branch);
}
    getch();
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_142_0.png)

# 程序 8.9 结构体数组

