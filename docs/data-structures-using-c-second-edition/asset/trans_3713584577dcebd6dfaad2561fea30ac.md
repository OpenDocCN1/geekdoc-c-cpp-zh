

printf("\n **********STUDENT'S DETAILS ************");
printf("\n ROLL NO. = %d", stud1.roll_no);
printf("\n NAME = %s", stud1.name);
printf("\n FEES = %f", stud1.fees);
printf("\n DOB = %d - %d - %d", stud1.date.day, stud1.date.month, stud1.date.year);
getch();
return 0;
}
```

# Output

```
Enter the roll number : 01
Enter the name : Rahul
Enter the fees : 45000
Enter the DOB : 25 09 1991
**********STUDENT'S DETAILS ************
ROLL NO. 01
NAME : Rahul
FEES = 45000.00
DOB = 25 - 09 - 1991
```

## 5.3 结构体数组

在上面的示例中，我们已经了解了如何声明结构体并为其数据成员赋值。现在，我们将讨论如何声明结构体数组。为此，让我们先分析在什么情况下需要结构体数组。

在一个班级中，不只有一个学生。但可能至少有 30 名学生。因此，相同的结构体定义可以用于所有 30 名学生。当我们创建结构体数组时，这就会成为可能。结构体数组的声明方式与声明内置数据类型数组的方式相同。

结构体数组的另一个适用场景是组织机构。一个组织有许多员工。因此，为每个员工定义单独的结构体不是可行的方案。在这里，我们可以为所有员工使用一个通用的结构体定义。这同样可以通过声明结构体数组 employee 来实现。

声明结构体数组的一般语法如下，

```
struct struct_name
{
    data_type member_name1;
    data_type member_name2;
    data_type member_name3;
    .......................
    .......................
};
struct struct_name struct_var[index];
```

考虑给定的结构体变量定义。

```
struct student
{
    int r_no;
    char name[20];
    char course[20];
    float fees;
};
```

可以通过编写以下方式声明学生数组：

```
struct student stud[30];
```

现在，为班级中第 i 名学生赋值，我们将编写

```
stud[1].r_no = 09;
stud[1].name = "RASHTRI";
stud[1].course = "MCA";
stud[1].fees = 60000;
```

为了在声明时初始化结构体变量数组，我们可以按以下方式编写：

```
struct student stud[3] = {(01, "Aman", "BCA", 45000),(02, "Aryan", "BCA", 60000), (03, "John", "BCA", 45000)};
```

## 编程示例

- 4. 编写一个程序，读取并显示班级中所有学生的信息。然后编辑第 i 名学生的详细信息并重新显示全部信息。

```
#include <stdio.h>
#include <conio.h>
#include <string.h>
int main()
{
	struct student
	{
		int roll_no;
		char name[80];
		int fees;
		char DOB[80];
	};
	struct student stud[50];
	int n, i, new_rollno;
	int new_fees;
	char new_name[80], new_DOB[80];
	clrscr();
	printf("\n Enter the number of students : ");
	scanf("%d", &n);
	for(i=0;i<n;i++)
	{
		printf("\n Enter the roll number : ");
		scanf("%d", &stud[i].roll_no);
		printf("\n Enter the name : ");
		gets(stud[i].name);
		printf("\n Enter the fees : ");
		scanf("%d", &stud[i].fees);
		printf("\n Enter the DOB : ");
		gets(stud[i].DOB);
	}
	for(i=0;i<n;i++)
	{
		printf("\n **********DETAILS OF STUDENT %d**********", i+1);
		printf("\n Roll No. = %d", stud[i].roll_no);
		printf("\n NAME = %s", stud[i].name);
		printf("\n FEES = %d", stud[i].fees);
		printf("\n DOB = %s", stud[i].DOB);
	}
	printf("\n Enter the student number whose record has to be edited : ");
	scanf("%d", &num);
	num--;
	printf("\n Enter the new roll number : ");
	scanf("%d", &new_rollno);
	printf("\n Enter the new name : ");
	gets(new_name);
	printf("\n Enter the new fees : ");
	scanf("%d", &new_fees);
	printf("\n Enter the new DOB : ");
	gets(new_DOB);
	stud[num].roll_no = new_rollno;
	strcpy(stud[num].name, new_name);
	stud[num].fees = new_fees;
	strcpy(stud[num].DOB, new_DOB);
	for(i=0;i<n;i++)
	{
	    printf("\n *********DETAILS OF STUDENT %d**********", i+1);
	    printf("\n ROLL NO. = %d", stud[i].roll_no);
	    printf("\n NAME = %s", stud[i].name);
	    printf("\n FEES = %d", stud[i].fees);
	    printf("\n DOB = %s", stud[i].DOB);
	}
	getch();
	return 0;
}
```

# 输出

输入学生人数：2
输入学号：1
输入姓名：Kirti
输入学费：5678
输入出生日期：9 9 91
输入学号：2
输入姓名：kangana
输入学费：5678
输入出生日期：27 8 91
*********DETAILS OF STUDENT 1**********
ROLL NO. = 1
NAME = Kirti
FEES = 5678
DOB = 9 9 91
*********DETAILS OF STUDENT 2**********
ROLL NO. = 2
NAME = Kangana
FEES = 5678
DOB = 27 8 91
输入要编辑其记录的学生编号：2
输入新学号：2
输入新姓名：kangana khullar
输入新学费：7000
输入新出生日期：27 8 92
*********DETAILS OF STUDENT 1**********
ROLL NO. = 1
NAME = Kirti
FEES = 5678
DOB = 9 9 91
*********DETAILS OF STUDENT 2**********
ROLL NO. = 2
NAME = Kangana khullar
FEES = 7000
DOB = 27 8 92

## 5.4 结构体与函数

为了使结构体发挥最大作用，我们必须有一种将结构体传递给函数并从函数返回的机制。函数可以通过三种方式访问结构体的成员，如图 5.4 所示。

![](img/be6359df08208122bec6fad1103de211_162_0.png)

### 5.4.1 传递单个成员

要将结构体的任何单个成员传递给函数，必须使用直接选择运算符来引用单个成员。被调用程序不知道变量是普通变量还是结构体成员。请查看下面说明此概念的代码。

```
#include <stdio.h>
typedef struct
{
int x;
int y;
}POINT;
void display(int, int);
int main()
{
POINT p1 = {2, 3};
display(p1.x, p1.y);
return 0;
}
void display(int a, int b)
{
printf("The coordinates of the point are: %d %d", a, b);
}
```

### 输出

点的坐标为：2 3

### 5.4.2 传递整个结构体

与其他任何变量一样，我们可以将整个结构体作为函数参数传递。当结构体作为参数传递时，它使用按值调用方法传递，即结构体的每个成员都会被复制一份。

将结构体传递给函数并返回结构体的一般语法如下，

```
struct struct_name func_name(struct struct_name struct_var);
```

上述语法可根据要求进行变化。例如，在某些情况下，我们可能希望函数接收结构体但返回 void 或其他数据类型的值。下面给出的代码使用按值调用方法将结构体传递给函数。

```
#include <stdio.h>
typedef struct
{
int x;
int y;
}POINT;
void display(POINT);
int main()
{
    POINT p1 = {2, 3};
    display(p1);
    return 0;
}
void display(POINT p)
{
    printf("The coordinates of the point are: %d %d", p.x, p.y);
}
```

## 编程示例

- 5. 编写一个程序，读取、显示、加和减两个距离。距离必须使用千米和米来定义。

```
#include <stdio.h>
#include <conio.h>
typedef struct distance
{
    int kms;
    int meters;
}DISTANCE;
DISTANCE add_distance (DISTANCE, DISTANCE);
DISTANCE subtract_distance (DISTANCE, DISTANCE);
DISTANCE d1, d2, d3, d4;
int main()
{
    int option;
    clrscr();
    do
    {
        printf("\n *********** MAIN MENU ***********");
        printf("\n 1. Read the distances ");
        printf("\n 2. Display the distances");
        printf("\n 3. Add the distances");
        printf("\n 4. Subtract the distances");
        printf("\n 5. EXIT");
        printf("\n Enter your option : ");
        scanf("%d", &option);
        switch(option)
        {
            case 1:
                printf("\n Enter the first distance in kms and meters : ");
                scanf("%d %d", &d1.kms, &d1.meters);
                printf("\n Enter the second distance in kms and meters : ");
                scanf("%d %d", &d2.kms, &d2.meters);
            case 2:
                printf("\n The first distance is : %d kms %d meters",
                d1.kms, d1.meters);
                printf("\n The second distance is : %d kms %d meters",
                d2.kms, d2.meters);
                break;
```

