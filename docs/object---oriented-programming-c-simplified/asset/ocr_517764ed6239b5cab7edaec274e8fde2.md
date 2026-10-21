The student class has two private data members sname and **rollno** two **public** member function : **input_st** and **show_st**. This **student** class is inherited by class subject which has just one data member subject and two function **input_sub** and **show_sub**. The function for input and display the student name and roll number are called in the function of this class. The class subject is inherited by class **Internal** and **External** which we have seen earlier. Note both the classes inherit the class Subject in **virtual** public mode so only one copy of data members of class **Subject** will be available in class Total and no ambiguity will arise. Trace the program step wise. It is very simple to understand.

# 9.7 CONSTRUCTOR AND DESTRUCTOR IN INHERITANCE

When constructors are present both in base and derived classes then how they are called, how values are passed from derived class to base class? That we will see in this section. Assume a small example of single level inheritance in which **class A** is inherited by **class B**. Both the classes have their **default constructors**. When an object of **class B** is created, it calls the constructor of **class B**, but as this **class B** has got A as its parent **class**, constructor of **class A** will be called first, then constructor of class then obviously it will be using the data members from base class. Now without calling the constructor of **base class**, data members of base class, unexpected results may follow. Calling a constructor of **base class** first allows base class to properly set up its data members of that they can be used by derived classes.

In case of destructor in inheritance, destructor of derived class is **called first** and then destructor of base class is called. This is so as it is possible that if we call destructor of base class first, destructor might be working with data members of base class. So, destroying them in base class has an effect of working with the data members that no longer exist. Compiler won’t allow this. That’s why destructor class call is first so that it can do its works finishing with any of the data members of class base and do its own cleaning.

```
/*PROG 9.30 CONSTRUCTOR IN SINGLE LEVEL INHERITANCE VER 1 */

#include <iostream.h>
#include <conio.h>
class first
{
public :
        first( )
        {
                cout << “Hello from con of first” << endl;
        }
};
class second : first
{
public :
        second( )
        {
```