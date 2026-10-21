# Experiment-8 : Write a program which illustrates the use of virtual base class.

```
/* PROGRAM : GENERATING STUDENT REPORT, ELEMENTARY PROGRAM DEVELOPED BY STUDENTS */

#include <iostream.h>
#include <conio.h>
#include <stdlib.h>
class student
{
    char sname [20];
    int rollno;
public :
    void input_st()
    {
        cout << "Enter student name" << endl;
        cin.getline(sname,20);
        cout << "Enter the roll number" << endl;
        cin >> rollno;
    }
    void show_st()
    {
        cout << "\tName :=" << sname << endl;
        cout << "\tRoll  number :=" << rollno << endl;
    }
};
class Subject :public student
{
    char subject[25];
public :
    void input_sub()
    {
        input_st();
        cin.ignore();
        cout << "Enter the subject name" << endl;
        cin.getline(subject,25);
    }
    void show_sub()
    {
        show_st();
        cout << "\tSubject =" << subject << endl;
    }
};
```