```
```cpp
int var1;
double var2;
};

int main()
{

    MyUnion u1;
    u1.var1 = 2;
    cout <<"Value of var1: "<<u1.var1<< endl;

    u1.var2 = 4.5658;
    cout <<"Value of Var2: "<< u1.var2 << endl;

    u1.var2 = 456.000;
    cout<<"New value of Var2 is: "<<u1.var2<<endl;

    return 0;
}
```
```

Ans. The output of the preceding program is as follows:

```
```text
Value of var1: 2
Value of Var2: 4.5658
New value of Var2 is: 456
```
```

# Q11. What will be the output of the following program?

```
```cpp
#include <iostream.h>
#include <stdio.h>

struct student
{
    char student_ID[15];
    char student_name[30];
    int student_marks;
};

student input()
{
    student new_student;
    cout<<"Enter student ID :"<<endl;
    gets(new_student.student_ID);
    cout<<"Enter student name :"<<endl;
    gets(new_student.student_name);
    cout<<"Enter student marks :"<<endl;
    cin>>new_student.student_marks;

    return new_student;
}
```
```