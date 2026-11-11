marks. The displayData() method, on the other hand, is used to display the information about these students.

Besides defining a method inside the class definition, there is an external way to define a method’s body outside the class structure by using the scope resolution operator. Listing 2 shows how to code a member function’s definition outside the class structure by using the scope resolution operator (you can find this example in the ExFunction.cpp file on the CD in the code\chapter6 folder):

# ▶ Listing 2: Defining a Function outside a Class Using Scope Resolution Operator

```
```cpp
#include<iostream.h>

class Student
{
    private:
    char sname[20];
    int sage,sclass;
    protected:
    char fatherName[20];
    public:
    int ssubject,smarks;
    void inputData();
    void displayData();
};

void Student::inputData()
{
    cout<<"Enter student's name"<<endl;
    cin>>sname;
    cout<<"Enter student's age"<<endl;
    cin>>sage;
    cout<<"Enter student's class"<<endl;
    cin>>sclass;
    cout<<"Enter subject code"<<endl;
    cin>>ssubject;
    cout<<"Enter marks scored by student"<<endl;
    cin>>smarks;
}

void Student::displayData()
{
    cout<<"Student's Name:"<<sname<<endl;
    cout<<"Student's Age:"<<sage<<endl;
    cout<<"Student's Class:"<<sclass<<endl;
    cout<<"Subject Code:"<<ssubject<<endl;
    cout<<"Student's Marks:"<<smarks<<endl;
}
```
```