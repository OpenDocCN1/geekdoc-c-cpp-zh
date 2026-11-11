+   - Creating nested classes
+   - Creating local classes

Let’s explain how to create a nested class in the following section.

# ## Nested Classes

A class that is declared inside the declaration of another class is termed as a nested class. It means a member of a class may itself be a class. For example, if class X is declared inside the declaration of class Y, then class X is the nested class, and class Y is the host class. Nested classes are generally used to create a customized (or user-defined) data type. Listing 22 shows an example of nested class (you can find this example in the EmployeeNested.cpp file on the CD in the code\chapter6 folder):

**Listing 22: Creating a Nested Class**

```
```cpp
#include<iostream.h>

class Employee
{
    char id[10];
    char name[30];
    char phone[15];
    char desig[20];

public:
    class salary
    {
        int basic;
        int hra;
        int da;
        int ta;
        int sa;
        int pf;

    public:
        Salary()
        {
            basic=4000;
            hra=2000;
            da=1000;
            ta=1000;
            sa=0;
            pf=500;
        }
        void read()
        {
            cin>>sa;
        }
    }
```
```