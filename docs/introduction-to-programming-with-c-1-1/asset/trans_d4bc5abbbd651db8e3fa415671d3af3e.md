

## 带标签的结构：

语法：

```
struct tagname
{
    Type1 member1;
    Type2 member2;
};
```

示例：

```
struct student
{
    char name[10];
    int usn, marks;
};
```

- Student 是结构的名字（标签名）
- Struct student 一起代表数据类型。
- 要为结构分配内存，必须声明变量。

结构变量声明的语法：

```
struct tagname v1,v2,...vn;
```

示例：

```
struct student s1,s2;
```

一旦变量被声明，内存就会为变量 s1 和 s2 分配。 为变量 s1 和 s2 分配的字节数分别为 14 字节

10 字节用于 name

2 字节用于 usn

2 字节用于 marks

分配的内存总大小是各个成员大小之和。

## 无标签的结构：

没有标签名的结构称为无标签结构。

语法：

```
struct
{
    Type1 member1;
    Type2 member2;
}
}v1,v2...vn;
```

### 示例：

```
struct
{
        char name[10];
        int usn,marks;
}s1,s2;
```

- 在没有标签名的情况下，必须在右大括号后立即声明变量。

## 类型定义的结构：

与关键字 typedef 关联的结构定义称为 typedefined 结构

### 语法：

```
typedef struct
{
    Type1 member1;
    Type2 member2;
}TYPE_ID;
```

### 示例：

```
typedef struct
{
    char name[10];
    int usn,marks;
}STUDENT;
```

- Struct 和 typedef 是关键字。
- STUDENT 是使用 typedef 创建的新数据类型，可用于变量声明。

### 变量声明的语法：

```
TYPE_ID v1,v2...vn;
```

### 示例：

```
STUDENT s1,s2;
```

## 结构初始化：

### 语法：

```
struct tagname variable={v1,v2...vn};
```

其中 struct tagname 是派生数据类型

V1,v2..vn 都是初始值

示例：

```
struct student
{
    char name[10];
    int usn, marks;
} s1 = {"ram",10,90};
(or)
```

```
struct student
{
    char name[10];
    int usn, marks;
};
struct student s1 = {"ram",10,90};
(or)
```

```
struct student
{
    char name[10];
    int usn,marks;
} s1 = {"ram",10,90}, s2 = {"bheem",11,99};
```

## 访问结构：

结构成员可以通过指定变量名后跟一个点号（.）后跟成员名来访问

语法：

```
Variable.member
```

示例：

```
struct student
{
    char name[10];
    int usn,marks;
} s1 = {"ram",10,90};
```

成员可以按如下方式访问：

通过指定 S1.name，我们可以访问字符串 “ram”。

通过指定 S1.usn，我们可以访问 10。

通过指定 S1.marks，我们可以访问 90。

## 嵌套结构：

包含另一个结构的结构称为嵌套结构（即）一个结构可以作为另一个结构的成员使用。

示例：

```
struct subject
{
        int marks1;
        int marks2;
        int marks3;
};
typedef struct
{
        char name[10];
        int usn;
        struct subject marks;
}STUDENT;
```

上面的结构包含一个成员 marks，其类型为 struct subject（另一个结构）。 所以这称为嵌套结构。

```
STUDENT s;
```

我们可以使用点运算符按如下方式访问字段：

```
s.name;

s.usn;

s.marks.marks1;

s.marks.marks2;

s.marks.marks3;
```

## 包含数组的结构：

单维或多维的 int、float、char 和 double 数组可以在结构中使用

语法：

```
Typedef struct
{
        Char name[10];
        Int marks[3];
}STUDENT;
```

声明结构变量

```
STUDENT S;
```

访问成员：

```
S.name;
```

```
s.marks[0];
```

```
s.marks[1];
```

```
s.marks[2];
```

## 结构数组：

像整数数组一样，我们可以有结构数组。

示例：

假设我们想存储 50 名学生的详细信息，包括姓名和成绩

我们可以写定义如下

```
typedef struct
{
    char name[20];
    int marks;
}STUDENT;
```

我们可以按如下方式声明结构数组

```
STUDENT s[50];
```

结构元素可以通过 s[i].name、s[i].marks 访问

## 结构和函数：

结构或结构成员可以通过各种方式传递给函数

- 通过传递单个成员
- 通过传递整个结构
- 通过指针传递结构（参考模块 5）

### 通过传递单个成员：

显示学生详细信息的程序

```
struct student
{
    char name[50];
    int usn;
};
void disp(char name[],int usn);------ function prototype
void main()
{
    struct student s1;
    printf("Enter name and usn\n");
    scanf("%s%d",s1.name,&s1.usn);
    disp(s1.name,s1.usn);------ function call
getch();
}
void disp(char name[],int usn)-- function definition
{
    Printf("name=%s\n",name);
    Printf("usn=%d\n",usn);
}
```

### 解释：

在上面的示例中，函数 disp 通过将结构的单个成员传递给用户定义函数来调用。 在用户定义函数中，创建形式参数以从实际参数接收 name 和 usn 的值。

### 传递整个结构：

```
struct student
{
    char name[50];
    int usn;
};
void disp(struct student stu);------ function prototype
void main()
{
    struct student s1;
    printf("Enter name and usn\n");
    scanf("%s%d",s1.name,&s1.usn);
    disp(s1);------ function call
getch();
}
```

```
void disp(struct student stu)-- function definition
```

```
{
    Printf("name=%s\n",stu.name);
    Printf("usn=%d\n",stu.usn);
}
```

解释：

在上面的示例中，函数 disp 通过将整个结构传递给用户定义函数来调用。 在用户定义函数中，形式参数被声明为结构类型以接收实际参数的值。

## 文件

> “文件是磁盘上存储相关数据组的地方”。

## 定义和打开文件

如果您想将数据存储在二级存储器的文件中，我们必须向操作系统指定有关文件的某些内容。

- ✓ 文件名
- ✓ 数据结构
- ✓ 目的

### 文件名：

文件名是构成操作系统有效文件名的字符字符串

它可能包含两部分，主要名称和可选的带扩展名的句点

示例：

- Prog.c
- Data.txt
- Output.c

### 数据结构：

文件的数据结构定义为 stdio.h 中的结构 FILE。 因此在使用文件之前，所有文件都应声明为类型 FILE。

当我们打开文件时，我们必须指定我们想要对文件做什么（即）我们可能向文件写入数据或读取已存在的数据。

声明和打开文件的语法：

第一条语句将变量 fp 声明为指向数据类型 FILE 的指针

在这两个函数中，第一个参数是文件指针，指定要在此处使用的文件。 第二个参数包含列表中项目的格式说明符。 第三个参数列表可以是变量、常量或字符串。

示例：

复制包含姓名和学号的文件内容到另一个文件。

```c
#include<stdio.h>
void main()
{
        FILE  *fp1,*fp2;
        char name[10];
        int rollno;
        fp1=fopen("file1.txt","r");
        fp2=fopen("file2.txt","w");
        fscanf(fp1,"%s%d",name,&rollno);
        fprintf(fp2," %s\t%d\n",name,rollno);
        getch();
}
```

## Fgets() 和 fputs()

这些函数用于从文件读取和向文件写入字符串。

fgets 的语法：

```c
ps=fgets(str,n,fp);
```

这里 str 是一个字符数组

- n 是从文件读取的字符数
- fp 是一个文件指针

如果此函数成功，它将返回读取的字符串的指针。 否则返回 NULL。 它读取 n~1 个字符或换行符，以先出现者为准。 如果它读取换行符，它会将其保留为字符串的一部分并附加空字符。 如果它没有读取换行符，则读取 n~1 个字符并在末尾附加空字符。

示例：

