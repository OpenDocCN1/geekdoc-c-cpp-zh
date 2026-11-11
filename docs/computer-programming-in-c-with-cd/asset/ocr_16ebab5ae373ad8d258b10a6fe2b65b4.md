```
```cpp
Beta Bobj;
Aobj.InputArray();
matmult(Aobj,Bobj);
Bobj.DisplayMatrix();
getche();
}
```
```

Q46: Write a program to input in information of student's for eg: Student Roll Number, Student Name, Marks in Maths, Physics, Chemistry. Find the total marks for each student. In the student class make a function to sort students according to the total marks[ascending order]. If the total marks of two students are equal then it will decide the merit rank depending first on the marks obtained in Maths, then Physics. If total marks in all the three subjects and Maths and Physics are equal, it then means that chemistry is also equal. In that case, final decision is to be taken based on the roll number of the student. Also, the program is to be implemented in singly linked lists.

Ans:

```
```cpp
#include<iostream.h>
#include<conio.h>
#include<stdlib.h>
#include<ctype.h>
#include<string.h>

class student  //defining a class by the name student
{
    public: //All the functions or members below this declaration are public
    char name[10];
    int rollno,m1,m2,m3,t;
}; /* The semicolon after the class declaration is an important thing. Data
   constructs such as structures and classes end with a semicolon, while
   control constructs such as functions and loops do not. */

class node  //defining a class by the name node
{
    public: //All the members below this declaration are public
    student data;
    node *link; //link is pointer variable pointing to a node
}; //As explained above for the semicolon after the class declaration

class marklist
{
    node *head; //head is a pointer variable pointing to a node
    public: //All the functions below this declaration are public
```
```