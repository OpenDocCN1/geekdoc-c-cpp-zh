
```c
for(i=0;i<2;i++)
{
    for(j=0;j<2;j++)
    {
        printf("Enter element\n");
        scanf("%d",&x[i][j]);
    }
}
//Creates matrix
printf("Enter the elements of second matrix\n");
for(i=0;i<2;i++)
{
    for(j=0;j<2;j++)
    {
        printf("Enter element\n");
        scanf("%d",&y[i][j]);
    }
}
//multiplication of 2 matrices m1 & m2
for(k=0;k<2;k++)
{
    for(i=0;i<2;i++)
    {
        for(j=0;j<2;j++)
            m[k][i]+=x[k][j]*y[j][i];
    }
}
printf("product of matrix xy is\n");
for(i=0;i<2;i++)
{
    for(j=0;j<2;j++)
    {
        printf("%d\t",m[i][j]);
    }
    printf("\n");
}
getch();
}
```

![](img/35ea447eca4d04af54f37bf3d3ca337d_259_0.png)

## 函数程序

### 47. 编写一个使用递归函数求一个数的阶乘的程序。

```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int fa,n;
    int fact(int n1);
    clrscr();
    printf("Enter a number :");
    scanf("%d", &n);
    fa=fact(n);
    printf("The factorial is : %d", fa);
    getch();
}
int fact(int n1)
{
    int fl=1,i;
```

![](img/35ea447eca4d04af54f37bf3d3ca337d_261_0.png)

### 49. 编写一个程序，计算一个整数中的位数。

```c
/* C program to count the number of digits in an integer */
#include<stdio.h>
#include<conio.h>
int main() {
        int num, temp, count=0;
        printf("Enter an integer\n");
        scanf("%d", &num);
        temp = num;
        while(temp!=0) {
                temp = temp/10;
                ++count;
        }
        printf("Number of digits in %d : %d",num, count);
        getch();
        return 0;
}
```

### 程序输出

```
Enter an integer
12345
Number of digits in 12345 : 5
Enter an integer
-345
Number of digits in -345 : 3
```

## 结构体与联合体程序

### 50. 创建一个名为 employee 的结构体，包含员工姓名、基本工资和净工资。通过结构体从用户处接受员工姓名和基本工资。通过将 DA 设为基本工资的 11%、HRA 设为基本工资的 75%、TA 设为基本工资的 55% 来计算净工资，计算并打印净工资。

```c
#include<stdio.h>
#include<conio.h>
struct employee{
    char emp_name[20];
    int basic_sal;
    float net_sal;
}emp;
void cal_netsalary(struct employee *x);
void main()
{
    struct employee *pt;
    pt=&emp;
    //accept details of employee
    printf("\nEnter Employee Name: ");
    scanf("%s",pt->emp_name);
    printf("\nEnter Employee Basic Salary: ");
    scanf("%d",&pt->basic_sal);
    //Calculate Net salary of Employee
    cal_netsalary(pt);
    //display Employee's salary
    printf("\n Employee's Net Salary: %f",pt->net_sal);
    getch();
}
void cal_netsalary(struct employee *x)
{
    x->net_sal = 0;
    x->net_sal+=(x->basic_sal*0.11);    //DA calculation
    x->net_sal+=(x->basic_sal*0.075);   //HRA calculation
    x->net_sal+=(x->basic_sal*0.055);   //TA calculation
}
```

### 输出

```
Enter Employee Name: Prem
Enter Employee Basic Salary: 15000
Employee's Net Salary: 18600.000000
```

### 编写程序演示联合体

```c
#include<stdio.h>
#include<conio.h>
union process {
    char name[32];
    float duration;
    int no_of_threads;
}u;
void main()
{
    printf("Enter name:\n");
    scanf("%s",u.name);
    printf("Enter duration: \n");
    scanf("%f",&u.duration);
    printf("Enter no of threads the process has: \n");
    scanf("%d",&u.no_of_threads);
    printf("Displaying\nName :%s",u.name);
    printf("\nProcess Duration: %.1f",u.duration);
    printf("\nProcess Duration: %d",u.no_of_threads);
    getch();
}
```

### 输出

```
Enter name: system
Enter duration: 12.5
Enter no of threads the process has: 2
Displaying
Name :
Process Duration: 0.0
Process Duration: 2
```

## 指针程序

### 51. 演示指针使用的程序。

```c
#include<stdio.h>
#include<conio.h>
float cal_per(int *x, int size);
void main()
{
    //Variable declaration
    int marks[3], no_of_sub,i;
    float per;
    char name[20];
    //accept values from user
    printf("\nEnter the student name");
    scanf("%s",name);
    printf("\nEnter the no of subjects");
    scanf("%d",&no_of_sub);
    printf("\nEnter the student marks");
    for(i=0; i<no_of_sub; i++)
        scanf("%d", &marks[i]);
    per = cal_per(marks,no_of_sub);
    printf("\n Student details:");
    printf("\n Student name: %s", name);
    printf("\n Student marks:");
    for(i=0; i<no_of_sub; i++)
        printf("\t %d ", *(marks + i));
    printf("\n Student percentage: %f", per);
    getch();
}
float cal_per(int *x, int size)
{
    float per;
    int i;
    for (i=0;i<size;i++)
        per+= *(x+i);
    per=per/size;
    return per;
}
```

### 输出

```
Enter the student name Prem
Enter the no of subjects 2
Enter the student marks 45 54
Student details:
Student name: Prem
Student marks: 45   54
Student percentage: 48.540482
```

|  |  |
|---|---|
| 52. | 对两个指针执行加法和减法的程序。 |

```c
#include<stdio.h>
#include<conio.h>
void main()
{
    int num1, num2, *pt_num1, *pt_num2, sum, sub;
    printf("Enter two integers to be added and subtracted\n");
    scanf("%d%d", &num1, &num2);
    pt_num1 = &num1;
    pt_num2 = &num2;
    sum = *pt_num1 + *pt_num2;
    sub = *pt_num1 - *pt_num2;
    printf("Sum of entered numbers = %d\n",sum);
    printf("Difference of entered numbers = %d\n",sub);
    getch();
}
```

### 输出

```
Enter two integers to be added and subtracted
10
20
Sum of entered numbers = 30
Difference of entered numbers = -10
```

## 字符串处理程序

### 53. 不使用 strlen() 函数计算字符串的长度。

```c
#include <stdio.h>
int main()
{
    char s[1000], i;

    printf("Enter a string: ");
    scanf("%s", s);

    for(i = 0; s[i] != '\0'; ++i);

    printf("Length of string: %d", i);
    return 0;
}
```

### 输出

```
Enter a string: kiran
Length of string: 5
```

### 54. 不使用 strcat() 连接两个字符串。

```c
#include <stdio.h>
int main()
{
    char s1[100], s2[100], i, j;

    printf("Enter first string: ");
    scanf("%s", s1);
    printf("Enter second string: ");
    scanf("%s", s2);

    // calculate the length of string s1
    // and store it in i
    for(i = 0; s1[i] != '\0'; ++i);

    for(j = 0; s2[j] != '\0'; ++j, ++i)
    {
        s1[i] = s2[j];
    }

    s1[i] = '\0';
    printf("After concatenation: %s", s1);

    return 0;
}
```

### 输出

```
Enter first string: Kiran
Enter second string: Gurbani
After concatenation: Kiran Gurbani
```

### 55. 不使用 strcpy() 手动复制字符串。

```c
#include <stdio.h>
int main()
{
    char s1[100], s2[100], i;

    printf("Enter string s1: ");
    scanf("%s",s1);

    for(i = 0; s1[i] != '\0'; ++i)
    {
        s2[i] = s1[i];
    }
    s2[i] = '\0';
    printf("String s2: %s", s2);

    return 0;
}
```

### 输出

```
Enter String s1: kiran
String s2: kiran
```

```c
printf("\nDigits: %d",digits);
printf("\nWhite spaces: %d", spaces);

return 0;
}
```

### 输出

```
Enter a line of string: adfslkj34 34lkj343 34lk
Vowels: 1
Consonants: 11
Digits: 9
White spaces: 2
```

### 59. 按字典顺序对字符串进行排序的程序。

```c
#include<stdio.h>
#include <string.h>

int main()
{
  int i, j;
  char str[10][50], temp[50];

  printf("Enter 10 words:\n");

  for(i=0; i<10; ++i)
    scanf("%[^\n]", str[i]);

  for(i=0; i<9; ++i)
    for(j=i+1; j<10 ; ++j)
    {
      if(strcmp(str[i], str[j])>0)
      {
        strcpy(temp, str[i]);
        strcpy(str[i], str[j]);
        strcpy(str[j], temp);
      }
    }
  printf("\nIn lexicographical order: \n");
  for(i=0; i<10; ++i)
  {
    puts(str[i]);
  }
  return 0;
}
```

### 输出

```
Enter 10 words:
C
C++
Java
PHP
Python
Perl
Ruby
R
JavaScript
PHP

In lexicographical order:
C
C++
Java
JavaScript
PHP
PHP
Perl
Python
R
Ruby
```

## 基本文件处理操作程序

### 60. 编写一个 C 程序，逐个字符读取文件 kiran.txt 中的所有数据。

```c
#include<stdio.h>
void main()
{
    FILE *fp;
    char ch;
    clrscr();
    fp=fopen("kiran.txt","r");
    if(fp==NULL)
    {
        printf("file doesnot exists");
    }
    else
    {
        while(ch!=EOF)
        {
            ch=getc(fp);
            putch(ch);
        }
    }
    fclose(fp);
    getch();
}
```

