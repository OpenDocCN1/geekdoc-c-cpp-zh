```
int rollno;
int marks;
};
main()
{
struct student stu={"Mary",25,68};
struct student *ptr=&stu;
printf("Name - %s\t",ptr->name);
printf("Rollno - %d\t",ptr->rollno);
printf("Marks - %d\n",ptr->marks);
}
```

We can also have pointers that point to individual members of a structure variable. For example-

```
int *p = &stu.rollno;
float *ptr = &stu.marks;
```

The expression &stu.rollno is equivalent to &(stu.rollno) because the precedence of dot operator is more than that of address operator.

# 10.12 Pointers Within Structures

A pointer can also be used as a member of structure. For example we can define a structure like this-

```
struct student
{
char name[20];
int *ptrmem;
};
struct student stu,*stuptr=&stu;
```

Here ptrmem is pointer to int and is a member of the structure student.

To access the value of ptrmem, we'll write stu.ptrmem or stuptr->ptrmem

To access the value pointed to by stu.ptrmem, we'll write *stu.ptrmem or *stuptr->ptrmem

Since the priority of dot and arrow operators is more than that of dereference operator, hence the expression *stu.ptrmem is equivalent to *(stu.ptrmem), and the expression *stuptr->ptrmem is equivalent to *(stuptr->ptrmem).

# 10.13 Structures And Functions

Structures may be passed as arguments to function in different ways. We can pass individual members, whole structure variable or structure pointers to the function. Similarly a function can return either a structure member or whole structure variable or a pointer to structure.

# 10.13.1 Passing Structure Members As Arguments

We can pass individual structure members as arguments to functions like any other ordinary variable.

```
/*P10.7 Program to understand how structure members are sent to a function */
#include<stdio.h>
#include<string.h
```