
```
    printf("Roll Number: %d\n", student1.roll_no);

    printf("Name: %s\n", student1.name);

    printf("Age: %d\n", student1.age);

    getch();

}
```

输出：

```
Enter the roll number of the student:

101

Enter the name of the student:

James

Enter the age of the student:

24

Student details:

Roll Number: 24

Name: James

Age: 24
```

你可以从前面的输出中注意到，`roll_no` 和 `age` 字段显示相同的值。当你输入 `101` 作为学生的学号时，值 `101` 会尝试被赋值给 `roll_no` 和 `age` 字段。`roll_no` 和 `age` 字段被初始化为 `101`，因为这些字段是 `int` 类型；然而，`name` 字段被初始化为随机值，因为它是 `char` 类型（数组）。现在，当你输入 `James` 作为学生的姓名时，`name` 字段被初始化为 `James`，而 `roll_no` 和 `age` 字段被初始化为随机值。最后，当你输入 `24` 作为学生的年龄时，`roll_no` 和 `age` 字段被初始化为 `24`，而 `name` 字段再次初始化为随机值。

## 总结

在本章中，你学习了如何定义结构体。然后，你学习了声明和初始化结构体变量。接下来，你学习了如何创建嵌套结构和结构体数组。本章还讨论了 `typedef` 语句的概念。你还学习了联合体（union）以及如何定义联合体。最后，你学习了如何声明和初始化联合体变量。

## 快速复习

+ Q1. 写一个程序，在已知总薪和扣除额的情况下，计算员工的净工资。

```c
#include<stdio.h>
#include<conio.h>
void main() {
    struct emp {
        int emp_id;
        char name[10];
        float gross_sal, net_sal, deduction;
    };
    struct emp emp1;
    clrscr();
    printf("Enter employee ID: %d\n");
    scanf("%d",&emp1.emp_id);
    printf("Enter employee name: %s\n");
    scanf("%s",&emp1.name);
    printf("Enter gross salary: %f\n");
    scanf("%f",&emp1.gross_sal);
    printf("Enter deduction: %f\n");
    scanf("%f",&emp1.deduction);
    emp1.net_sal = emp1.gross_sal-emp1.deduction;
    printf("Salary details are:%s\n");
    printf("Employee ID: %d\n", emp1.emp_id);
    printf("Name: %s\n", emp1.name);
    printf("Gross Salary: $%.2f\n", emp1.gross_sal);
    printf("Deduction: $%.2f\n", emp1.deduction);
    printf("Net Salary: $%.2f\n", emp1.net_sal);
    getch();
}
```

输出:
Enter employee ID:
101
Enter employee name:
James
Enter gross salary:
400
Enter deduction:
30
Salary details:
Employee ID: 101
Name: James
Gross Salary: $400.00
Deduction: $30.00
Net Salary: $370.00

# 418 ► 第 16 章

Q2. 写一个程序，输入三个学生在三门学科的学号、姓名和成绩，并打印每个学生的总分和百分比。

答复：

```c
#include <stdio.h>
#include <conio.h>
struct student {
    int roll_no, m1, m2, m3;
    char name[20];
    float tot, percent;
    int i;
};
void main() {
    clrscr();
    for(i=0; i<3; i++) {
        printf("Enter roll number, name, and marks of the three subjects: %n");
        scanf("%d %s %d %d %d", &student.roll_no, student.name, &student.m1, &student.m2, &student.m3);
        student.tot = student.m1 + student.m2 + student.m3;
        student.percent = (student.tot * 100 / 300);
        printf("Name: %s\n", student.name);
        printf("Total Marks: %f\n", student.tot);
        printf("Percentage: %f\n", student.percent);
    }
    getch();
}
```

输出：

Enter roll number, name, and marks of the three subjects:
101 James 78 82 75
Marks details:
Roll Number: 101
Name: James
Total Marks: 235.000000
Percentage: 78.333333
Enter roll number, name, and marks of the three subjects:
102 Peter 68 65 72
Marks details:
Roll Number: 102
Name: Peter
Total Marks: 225.000000
Percentage: 75.000000
Enter roll number, name, and marks of the three subjects:
103 Harry 70 60 64
Marks details:
Roll Number: 103
Name: Harry
Total Marks: 220.000000
Percentage: 73.333333

Q3. 使用结构体数组重写问题2中的程序。

答复：

```c
#include <stdio.h>
#include <conio.h>
void main() {
    struct student {
        int roll_no, m1, m2, m3;
        char name[20];
        float tot;
    } students[30];
    int i;
    clrscr();
    for(i=0; i<3; i++) {
        printf("Enter roll number, name, and marks of the student in three\nsubjects: \n");
        scanf("%d%[^\n]%f %f %f", &students[i].roll_no, students[i].name, &students[i].m1, &students[i].m2, &students[i].m3);
        students[i].tot = students[i].m1 + students[i].m2 + students[i].m3;
        students[i].percent = (students[i].tot * 100 / 300);
    }
    printf("Marks details:\n");
    for(i=0; i<3; i++) {
        printf("Roll Number: %d\n", students[i].roll_no);
        printf("Name: %s\n", students[i].name);
        printf("Total Marks: %f\n", students[i].tot);
        printf("Percentage: %f\n", students[i].percent);
    }
    getch();
}
```

Enter roll number, name, and marks of the three subjects:
101 James 78 82 75
Enter roll number, name, and marks of the student in three subjects:
102 Peter 68 75 72
Enter roll number, name, and marks of the student in three subjects:
103 Harry 66 70 64
Marks details:
Roll Number: 101
Name: James
Total Marks: 235.000000
Percentage: 78.333333
Roll Number: 102
Name: Peter
Total Marks: 225.000000
Percentage: 75.000000
Roll Number: 103
Name: Harry
Total Marks: 200.000000
Percentage: 66.666667

Q4. 写一个程序，输入圆心和圆上点的坐标，计算圆的半径。

答复：

```c
#include <stdio.h>
#include <conio.h>
#include <math.h>
void main() {
    struct point {
        int x, y;
    } p1, p2;
    int radius;
    float area;
    clrscr();
    printf("Enter the coordinates of the center of the circle: \n");
    scanf("%d%d", &p1.x, &p1.y);
    printf("Enter the coordinates of the point on the circle: \n");
    scanf("%d%d", &p2.x, &p2.y);
    radius = sqrt(pow(p2.x - p1.x, 2) + pow(p2.y - p1.y, 2));
    area = 3.14 * radius * radius;
    printf("Radius of the circle: %d\n", radius);
    printf("Area of the circle: %f\n", area);
    getch();
}
```

输出：
Enter the coordinates of the center of the circle:
10 10
Enter the coordinates of the point on the circle:
12 15
Radius of the circle: 5
Area of the circle: 78.500000

Q5. 写一个程序，输入书籍 ID、作者姓名、出版社和价格，并打印这些信息。

答复：

```c
#include <stdio.h>
#include <conio.h>
void main() {
    struct book {
        int book_id;
        char author_name[20];
        char publisher_name[20];
        float price;
    } book1;
    clrscr();
    printf("Enter book id: \n");
    scanf("%d", &book1.book_id);
    printf("Enter the name of the author: \n");
    scanf("%s", book1.author_name);
    printf("Enter the name of the publisher: \n");
    scanf("%s", book1.publisher_name);
    printf("Enter the price of the book: \n");
    scanf("%f", &book1.price);
    printf("\nBook details:\n");
    printf("Book ID: %d\n", book1.book_id);
    printf("Author: %s\n", book1.author_name);
    printf("Publisher: %s\n", book1.publisher_name);
    printf("Price: $%.2f\n", book1.price);
    getch();
}
```

输出：
Enter book id:
2754
Enter the name of the author:
william
Enter the name of the publisher:
Dreamtech
Enter the price of the book:
5
Book details:
Book ID: 2754
Author: william
Publisher: Dreamtech
Price: $5.00

# 17 指针

## 目标

+ 17.1 理解指针
+ 17.2 声明指针变量
+ 17.3 使用地址运算符 (&)
+ 17.4 初始化指针变量
+ 17.5 解引用指针（Dereferencing）
+ 17.6 对指针进行操作
+ 17.7 函数与指针的使用
+ 17.8 数组与指针的使用
+ 17.9 运行时内存分配

你已经熟悉了如何在 C 语言中声明变量并为这些变量赋值，无论这些变量是否存储在内存中。你应该了解指针的概念，以便知道变量的内存位置。指针是一个与计算机内存相关的概念。计算机的内存表示为一系列连续内存位置的数组，每个位置都有唯一的标识号。这个数字被称为该特定内存位置的地址。这些地址用于轻松定位变量，而不是它们的值。

在本章中，你将学习 C 语言中的指针。接下来，你将学习如何声明指针变量。本章还讨论了地址运算符，它用于确定变量的地址。此外，你学习了如何初始化指针变量，以及如何解引用指针。另外，你还学习了如何在指针上执行算术、比较和赋值等操作。最后，你将学习如何将指针用于函数和数组，以及运行时分配内存。
让我们从理解 C 语言中指针的概念开始讨论。

# 17.1 理解指针

指针是一个存储在计算机内存其他处的变量地址的变量。指针变量只包含所引用变量的地址，而不包含该地址处的值。指针通常用于指向数组、函数、结构体、联合体以及任何基本数据类型的变量。使用指针的某些优势如下：

+ 1. 指针用于指向不同的数据结构
+ 2. 指针与函数配合使用以返回多个值

# 422 ► 第 17 章

- 3. 指针用于在运行时分配内存
除了优点之外，使用指针的缺点之一是，如果没有足够的内存来存储指针，程序可能会崩溃。

与指针一起使用的两个基本运算符是：

- 1. 取地址运算符 (&)
- 2. 间接引用运算符 (*)

单元运算符 `&` 给出对象的地址，而单元运算符 `*` 访问指针所指向的对象。你将在本章后面的部分学习更多关于这些运算符的内容。

![](img/655987774ce63b710f1a1b263f2c84e0_441_0.png)

- 1. 什么是指针？为什么有必要？（VTU, 2003年7/8月, 2007年1/2月）
- 2. 写关于 C 语言中指针的短记。（VTU, 2004年1/2月）

现在让我们学习如何在 C 语言中声明指针变量。

# 17.2 声明指针变量

指针是一个存储另一个变量地址的变量。你可以使用以下语法声明指针变量：

```
data_type *pointer_variable_name;
```

在上述语法中，`data-type` 指定你想要声明的指针变量的类型。星号 (`*`) 符号告诉编译器你正在创建一个指针变量，而 `pointer_variable_name` 指定指针变量的名称。例如：

```
int *ptr; // 声明一个整数据类型的指针变量 ptr
float *temp; /* 声明一个浮点数据类型的指针变量 temp */
```

让我们创建一个 C 程序来说明指针的声明。列表 1 显示了该程序的代码：

- 列表 1：声明指针变量

```c
#include <stdio.h>
#include <conio.h>
main(){
  int *ptr; /* 指针声明*/
  int a=25;
  clrscr();
  ptr=&a;
  printf("\nv value of a is %d", ptr);
```
