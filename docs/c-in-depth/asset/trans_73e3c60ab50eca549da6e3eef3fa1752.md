
点运算符左侧应有一个结构体类型的变量，右侧应为该结构体的成员名。例如考虑以下结构体——

```c
struct student{
        char name[20];
        int rollno;
        float marks;
      };
struct student stu1,stu2;
```

stu1 的名字由 - stu1.name 给出
stu1 的 rollno 由 - stu1.rollno 给出
stu1 的 marks 由 - stu1.marks 给出
stu2 的名字由 - stu2.name 给出
stu2 的 rollno 由 - stu2.rollno 给出
stu2 的 marks 由 - stu2.marks 给出

我们可以像程序中任何其他普通变量一样使用 stu1.name、stu1.marks、stu2.marks 等。
它们可以被读取、显示、处理、赋值或作为参数传递给函数。
我们不能使用 student.name 或 student.rollno，因为 student 不是结构体变量，而是结构体标签。

```c
/*P10.1 Program to display the values of structure members*/
#include<stdio.h>
#include<string.h>
struct student{
        char name[20];
        int rollno;
        float marks;
      };
main()
{
    struct student stu1={"Mary",25,68};
    struct student stu2,stu3;
    strcpy(stu2.name,"John");
    stu2.rollno=26;
    stu2.marks=98;
    printf("Enter name, rollno and marks for stu3 : ");
    scanf("%s %d %f",&stu3.name,&stu3.rollno,&stu3.marks);
    printf("stu1 : %s %d %.2f\n",stu1.name,stu1.rollno,stu1.marks);
    printf("stu2 : %s %d %.2f\n",stu2.name,stu2.rollno,stu2.marks);
    printf("stu3 : %s %d %.2f\n",stu3.name,stu3.rollno,stu3.marks);
}
```

```
Output:
Enter name, rollno and marks for stu3 : Tom 27 79.5
stu1 : Mary 25 68.00
stu2 : John 26 98.00
stu3 : Tom 27 79.50
```

在本程序中我们声明了三个 struct student 类型的变量。第一个变量 stu1 已被初始化，第二个变量 stu2 的成员通过单独的语句赋予值，而第三个变量 stu3 的值由用户输入。注意由于 stu2.name 是一个数组，所以我们不能使用赋值运算符为其赋字符串，因此使用了 strcpy() 函数。

点运算符是优先级最高的运算符之一，其结合性为从左到右。在这里它将优先于所有其他一元、关系、逻辑、算术和赋值运算符。在 ++stu.marks 这样的表达式中，首先会访问 stu.marks，然后其值增加 1。

## 10.5 结构体变量的赋值

我们可以将一个结构体变量的值赋给另一个结构体变量，如果两个变量都是同一结构体类型定义的。例如——

```c
/*P10.2 Program to assign a structure variables to another structure variable*/
struct student{
    char name[20];
    int rollno;
    float marks;
}
main()
{
    struct student stu1={"Oliver",12,98};
    struct student stu2;
    stu2=stu1;
    printf("stu1 : %s %d %.2f\n",stu1.name,stu1.rollno,stu1.marks);
    printf("stu2 : %s %d %.2f\n",stu2.name,stu2.rollno,stu2.marks);
}
```

```
Output:

stu1 : Oliver 12 98.00
stu2 : Oliver 12 98.00
```

不允许对结构体变量使用一元、关系、算术、位运算符。我们可以使用带成员的变量，前提是该成员本身不是结构体。

## 10.6 结构体在内存中的存储

结构体的成员存储在连续的内存位置中。

```c
/*P10.3 Program to show that members of structure are stored in consecutive memory locations*/
#include<stdio.h>
main()
{
    struct student{
        char name[5];
        int rollno;
        float marks;
    }stu;
```

```c
printf("Address of name = %u\n",&stu.name);
printf("Address of rollno = %u\n",&stu.rollno);
printf("Address of marks = %u\n",&stu.marks);
```

输出：
Address of stu.name = 65514
Address of stu.rollno = 65519
Address of stu.marks = 65521

输出在不同机器上可能不同，占用的字节数也可能因下一节所述的原因而变化，但这里需要注意的主要点是结构体成员存储在连续的内存位置中。

## 10.7 结构体的大小

在某些情况下，如读写文件，我们可能需要找出结构体的大小。通过 sizeof 运算符找出结构体的大小时，我们可以使用结构体变量名或带 struct 关键字的标签名。例如——

```
sizeof( struct student )
sizeof( stu1 )
sizeof( stu2 )
```

如果 stu1 和 stu2 是 struct student 类型的变量，则这三个表达式都会给出相同的结果。

结构体的大小在不同机器上可能不同。这是因为某些计算机存在特定的内存对齐限制。例如某些机器只在偶数地址存储整数，长整型只在地址为 4 的倍数处存储。这称为数据对齐。考虑以下结构体——

```c
struct
{
    char ch;
    int num;
};
```

## 10.8 结构体数组

我们知道数组是相同数据类型的元素的集合。我们可以声明结构体数组，其中数组的每个元素都是结构体类型。结构体数组可以声明为——

```c
struct student stu[10];
```

| | | |
|---|---|---|
| stu[0].name | stu[0].rollno | stu[0].marks |
| stu[1].name | stu[1].rollno | stu[1].marks |
| stu[2].name | stu[2].rollno | stu[2].marks |
| ............... | ............... | ............... |
| stu[9].name | stu[9].rollno | stu[9].marks |

数组中的所有结构体都存储在连续的内存位置中。

```c
/*P10.4 Program to understand array of structures*/
#include<stdio.h>
struct student {
char name[20];
int rollno;
float marks;
};

main()
{
int i;
struct student stuarr[10];
{
for(i=0;i<10;i++)
{
printf("Enter name, rollno and marks : ");
scanf("%s%d%f",stuarr[i].name,&stuarr[i].rollno,&stuarr[i].marks);
}
for(i=0;i<10;i++)
{
printf("%s %d %f \n",stuarr[i].name,stuarr[i].rollno, stuarr[i].marks);
}
}

```

在某些编译器中，上述程序可能无法正确工作，并在运行时给出消息“floating point not linked”。这个问题出现的原因是浮点格式（用于 scanf 及其他相关函数）并不总是链接，以减小可执行文件的大小。解决此问题的方案将在你的编译器手册中给出。例如，Borland C 建议包含以下两行来解决此问题。

```
extern unsigned _floatconvert;
#pragma extref _floatconvert
```

避免上述问题的另一种方法是插入如下函数的定义

```
void link()
{ 
float x, *ptr = &x; 
}
```

结构体数组可以使用与数组相同的语法进行初始化。例如

```
struct student stuarr[3]={
{"Mary",12,98.5},
{"John",11,97},
{"Tom",12,89.5}
};
```

如果初始化列表中包含所有初始化项，则内部的花括号对是可选的。

## 10.9 结构体内的数组

我们可以在结构体中有一个数组作为成员。在 student 结构体中，我们已将 name 成员作为字符数组。现在我们将在 student 结构体内部声明另一个数组。

```c
struct student{
    char name[20];
    int rollno;
    int submarks[4];
};
```

数组 submarks 表示学生在 4 门科目中的成绩。

如果 stu 是 struct student 类型的变量，则——

- stu.submarks[0] - 表示学生在第一科的成绩
- stu.submarks[1] - 表示第二科的成绩。
- stu.name[0] - 表示 name 成员的第一个字符。
- stu.name[4] - 表示 name 成员的第五个字符。

如果 stuar[10] 是 struct student 类型的数组，则——

- stuar[0].submarks[0] - 表示第一个学生在第一科的成绩
- stuar[4].submarks[3] - 表示第五学生在第四科的成绩。
- stuar[0].name[0] – 表示第一个学生 name 成员的第一个字符
- stuar[5].name[7] – 表示第六学生 name 成员的第八个字符

```c
/*P10.5 Program to understand arrays within structures*/
#include<stdio.h>
struct student{
    char name[20];
    int rollno;
    int submarks[4];
};
main()
{
    int i,j;
    struct student stuarr[3];
    for(i=0;i<3;i++)
    {
        printf("Enter data for student %d\n",i+1);
        printf("Enter name : ");
        scanf("%s",stuarr[i].name);
        printf("Enter roll number : ");
        scanf("%d", &stuarr[i].rollno);
        for(j=0;j<4;j++)
        {
            printf("Enter marks for subject %d : ",j+1);
            scanf("%d",&stuarr[i].submarks[j]);
        }
    }
}
```
