```
for (i=0;i<=4;i++)
{
printf ("Enter the roll number of %d student",i+1);
scanf ("%d",&stud[i].roll_no);
printf("Enter the name of %d student",i+1);
scanf ("%s",stud[i].name);
printf ("Enter the course of %d student",i+1);
scanf ("%s",stud[i].course);
for (j=0;j<=2;j++)
{
printf ("Enter the marks of the %d subject of the student %d\n",i+1,j+1);
scanf ("%d",&stud[i].subject[j]);
}
}
printf ("The data you have entered is as follows:\n");
for (i=0;i<=4;i++)
{
printf ("The %d th student’s roll number is %d\n",i+1,stud[i].roll_no);
printf ("The %d th student’s name is %s\n",i+1,stud[i].name);
printf ("The %d th student’s course is %s\n",i+1,stud[i].course);
for (j=0;j<=2;j++)
{
printf ("The %d th student’s marks of %d I subject are %d\n",i+1, j+1,stud[i].subject[j]);
}
}
getch();
}
```

If we want to access the data members of structurenamel then we can directly access with the help of <structvariable1>.<data_members1> and if we want to access the data members of <structurename2> then we can directly access with the help of <structure_variable2>.<structure_variable2>.<data_members2>.

# STRUCTURE WITHIN STRUCTURE OR NESTING STRUCTURE

Nested structure means structure within a structure.
The general syntax for defining a nested structure is as follows:

```
struct<structurename1>
{
    <data_members1>;
struct<structurename2>
{
    <data_members2>;
}<structure_variable2>;
}<structure_variable1>;
```

# Example

If we define the following structure:
struct date

```
{
    int day, month, year;
} struct time
{
    int hour,min,sec;
};
}d;
If we want to access the day, month and year then we can directly access with the help of d.day, d.month, d.year and if we want to access the hour, min and sec then we can directly access with the help of d.t.hour, d.t.min and d.t.sec.
```

Following the example demonstrates the concept of nesting structure.

```
#include<stdio.h>
#include<conio.h>
struct course
{
    int cuno;
    int coufees;
};
struct student
{
    int studno;
    course sc;
    course sc1;
};
void main()
{
    student s1;
    int x;
    s1.studno=100;
    s1.sc.couno=123;
    s1.sc.coufees=5000;
    s1.sc1.couno=200;
    s1.sc1.coufees=5000;
    x = s1.sc.coufees + s1.sc1.coufees;
    printf("\n The student number is
```