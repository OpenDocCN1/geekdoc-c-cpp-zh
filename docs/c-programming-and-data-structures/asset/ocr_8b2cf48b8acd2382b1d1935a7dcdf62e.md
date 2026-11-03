```
bar3d(150, 50, 250,150, 10, 1); /*Calling the built-in function bar3d()*/
getch();
closegraph(); /*Shutting the graphics system*/
}
```

Output

![](bbox=[0.42, 0.28, 0.68, 0.52])

# EXAMPLE A.60 Write a program to print the marks obtained by two students using structures.

Program

```
/*Program for demonstrating structure member initialization*/
#include <stdio.h>
#include <conio.h>

void main ()
{
struct student/*Declaring the student structure*/
{
int marks1, marks2, marks3;
};

struct student std1 = {55,66,80};/*Initializing marks for student 1*/
struct student std2 = {60,85,78};/*Initializing marks for student 2*/
clrscr();

/*Displaying marks for student 1*/
printf("Marks obtained by 1st student: %d, %d and %d",std1.marks1, std1.marks2, std1.marks3);

/*Displaying marks for student 2*/
printf("\nMarks obtained by 2nd student: %d, %d and %d",std2.marks1, std2.marks2, std2.marks3);
getch();
}
```

Output

Marks obtained by 1st student: 55, 66 and 80
Marks obtained by 2nd student: 60, 85 and 78