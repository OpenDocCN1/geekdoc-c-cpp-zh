Here on the left side of the dot there should be a variable of structure type and on right hand side there
should be the name of a member of that structure. For example consider the following structure-

```
~~~c
struct student{
        char name[20];
        int rollno;
        float marks;
      };
struct student stu1,stu2;
~~~
```

name of stu1 is given by - stu1.name
rollno of stu1 is given by - stu1.rollno
marks of stu1 is given by - stu1.marks
name of stu2 is given by - stu2.name
rollno of stu2 is given by - stu2.rollno
marks of stu2 is given by - stu2.marks

We can use stu1.name , stu1.marks, stu2.marks etc like any other ordinary variables in the program.
They can be read, displayed, processed, assigned values or can be send to functions as arguments.
We can't use student.name or student.rollno because student is not a structure variable, it is a structure tag.

```
~~~c
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
~~~
```

```
~~~
Output:
Enter name, rollno and marks for stu3 : Tom 27 79.5
stu1 : Mary 25 68.00
stu2 : John 26 98.00
stu3 : Tom 27 79.50
~~~
```