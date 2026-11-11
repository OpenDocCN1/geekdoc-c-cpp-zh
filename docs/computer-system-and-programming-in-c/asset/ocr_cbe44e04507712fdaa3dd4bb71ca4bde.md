```
```c
char name[25],city[10];
}s[10];
void main()
{
int i;
clrscr();
for(i=0;i<10;i++)
{
printf("\n enter the student number");
scanf("%d",&s[i].sno);
printf("\n enter the name");
scanf("%s",s[i].name);
printf("\n enter the age");
scanf("%d",&s[i].age);
printf("\n enter the city");
scanf("%s",s[i].city);
}
printf("\n the students records are as follows");
for(i=0;i<10;i++)
{
printf("\n the student number is %d",s[i].sno);
printf("\n the name is %s",s[i].name);
printf("\n the age is %d",s[i].age);
printf("\n the city is %s",s[i].city);
}
getch();
}
```
```

```
```c
printf ("Enter the student data one by one\n");
for(i=0;i<19;i++)
{
printf ("Enter the roll number of %d student", i+1);
scanf ("%d",&stud[i].roll_no);
printf ("Enter the name of %d student",i+1);
scanf ("%s",stud[i].name);
printf ("Enter the course of %d student",i+1);
scanf ("%s",stud[i].course);
printf ("Enter the marks obtained of %d student",i+1);
scanf ("%d",&stud[i].marks_obtained);
}
printf ("the data entered is as follows\n");
for (i=0;i<19;i++)
{
printf ("The roll number of %d student is %d\n",i+1,stud[i].roll_no);
printf ("The name of %d student is %s\n",i+1,stud[i].name);
printf ("The course of %d student is %s\n",i+1,stud[i].course);
printf ("The marks of %d student is %d\n",i+1,stud[i].marks_obtained);
}
getch();
}
```
```

# Problem 2

Write a program to read and display data for 20 students.

# Solution

```
```c
#include <stdio.h>
#include<conio.h>
struct student
{
int roll_no;
char name[20];
char course[20];
int marks_obtained ;
};
void main( )
{
struct student stud [20];
int i;
clrscr();
```
```

# Problem 3

Write a program to read and print data related to five students having marks of three subjects each using the concept of arrays.

# Solution

```
```c
#include<stdio.h>
#include<conio.h>
struct student
{
int roll_no;
char name [20];
char course [20];
int subject [3];
};
void main( )
{
struct student stud[5];
int i,j;
printf ("Enter the data for all the students:\n");
```
```