
- Creating nested classes
- Creating local classes

Let’s explain how to create a nested class in the following section.

## Nested Classes

A class that is declared inside the declaration of another class is termed as a nested class. It means a member of a class may itself be a class. For example, if class X is declared inside the declaration of class Y, then class X is the nested class, and class Y is the host class. Nested classes are generally used to create a customized (or user-defined) data type. Listing 22 shows an example of nested class (you can find this example in the EmployeeNested.cpp file on the CD in the code\chapter6 folder):

**Listing 22: Creating a Nested Class**

```cpp
#include<iostream.h>

class Employee
{
    char id[10];
    char name[30];
    char phone[15];
    char desig[20];

public:
    class Salary
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
        int sum()
        {
            int x=sa-(basic+hra+da+ta+pf);
            return x;
        }
        void dis()
        {
            cout<<"Your salary constituents are:"<<endl;
            cout<<"Basic : "<<basic<<endl;
            cout<<"HRA : "<<hra<<endl;
            cout<<"TA : "<<ta<<endl;
            cout<<"DA : "<<da<<endl;
            cout<<"PF : "<<pf<<endl;
            cout<<"Special Allowance : "<<sum()<<endl;
        }
    };
    Salary sal;
    void read()
    {
        cout<<"Enter employee id"<<endl;
        cin>>id;
        cout<<"Enter employee name"<<endl;
        cin>>name;
        cout<<"Enter phone"<<endl;
        cin>>phone;
        cout<<"Enter designation"<<endl;
        cin>>desig;
        cout<<"Enter salary"<<endl;
        sal.read();
    }
    void display()
    {
        cout<<"Employee ID : "<<id<<endl;
        cout<<"Name : "<<name<<endl;
        cout<<"Phone : "<<phone<<endl;
        cout<<"Designation : "<<desig<<endl;
    }
};
void main()
{
    Employee e;
    e.read();
    e.display();
    e.sal.dis();

}
```

**Output:**

```text
Enter employee id
E001
Enter employee name
Vineet
Enter phone
9877522486
Enter designation
ChannelCoordinator
Enter salary
20000
Employee ID : E001
Name : Vineet
Phone : 9877522486
Designation : ChannelCoordinator
Your salary constituents are:
Basic : 4000
HRA : 2000
TA : 1000
DA : 1000
PF : 500
Special Allowance : 11500
```

In Listing 22, a nested class, Salary, is declared within the declaration of the Employee class. The Salary class is created to segregate the constituents of an employee’s salary. It shows the employee’s salary in the form of HRA, TA, DA, special allowance (SA), and PF. An object, sal, of the Salary class is created in the Employee class. It is used to access the read() and dis() member functions of the Salary class inside the read() and display() member functions, respectively, of the Employee class. Further, the member functions, read() and display(), of Employee class are used to accept the employee’s details and to display these details, respectively. The following code snippet shows an object of the Employee class:

```cpp
Employee e;
```

Inside the main() function, the data members of the Salary nested class can be accessed, as shown in the following code snippet:

```cpp
e.sal.dis();
```

Note that you can not access the members of the Salary nested class by using the object of the Employee class. This means that the following code snippet generates a syntax error by C++ compiler:

```cpp
e.basic=5000;
```

In the preceding code snippet, C++ compiler generates an error, because members of a nested class must be accessed using the object of the nested class.

## Creating Local Classes

A class declared within a function definition is called a local class. A local class definition can use the type names, enumerations, and static variables of the function within which the local class is defined. Listing 23 shows how to define a local class within a function definition (you can find this example in the LocalClass.cpp file on the CD in the code\chapter6 folder):

**Listing 23: Creating a Local Class**

```cpp
#include<iostream.h>

int globalVar=100;
class A
{
    int classVar;
    public:
        static int staticVar;
        void classFun()
        {
            class B
            {
                int localClassVar;
                public:
                    void localClassFun()
                    {
                        cout<<"local class calling"<<endl;
                        localClassVar=1000;
                        cout<<"Local class variable"<<localClassVar<<endl;
                        //classVar=10;
                        //cout<<"Class variable"<<classVar<<endl;
                        cout<<"Global variable"<<globalVar<<endl;
                        cout<<"Static variable"<<A::staticVar<<endl;
                    }
            } o;
            o.localClassFun();
        }
    };
int A::staticVar=100;
void main()
{
    A oo;
    oo.classFun();
}
```

**Output:**

```text
local class calling
Local class variable=1000
Global Variable=100
Static Variable=100
```

The member functions of a local class are inline functions, by default; therefore, they have to be defined within their class definition. The functions defined within the scope of a local class do not need the `inline` keyword. Moreover, a local class cannot have static data members. An attempt to define a static member within a local class causes an error as shown in the following code snippet:

```cpp
void myFunction()
{
    class LocalMyclass
    {
        void localFun1();   // invalid, local class has non inline member function
        int localFun2()     // valid, inline member function
        {
            return 0;
        }
        static int a;       // invalid, static variable declaration is
                            //not allowed for local class
        int b;              // valid, non static variable
    };
}
.
.
.
```

A local class, besides using the members of the function in which it is defined, can also use external variables (global variables) and non-member functions.

> *A function with a local class definition within curly braces, { ..... }, cannot access the members of the local class.*

After creating nested and local classes, let’s create functions that take class objects as their function parameters.

## 6.8 Passing Objects as Function Parameters

In C++, it is possible to have functions with parameters. This means that a function can have variables as its arguments. However, a function can also accept objects of the class as arguments. Following are the two ways to pass objects as function parameters:

- By value: Passes a copy of the entire object to the function
- By reference: Passes the address of an object to the function

Let’s explain these two ways in detail in the following sections.

### Passing an Object as a Function Argument-By Value

In the first method, we pass the object by value as function arguments. A copy of the object is passed to the function; any changes made to the object inside the function do not affect the object used to call the function. Listing 24 shows the addition of money in rupees and paisa using objects as function parameters (you can find this example in the ObjectsFunctionArgument_ByVal.cpp file on the CD in the code\chapter6 folder):

**Listing 24: Passing an Object by Value as a Function Parameter**

```cpp
#include<iostream.h>

class Money
{
private:
    int rupees, paisa;
public:
    void inputData(int x, int y)
    {
        rupees=x;
        paisa=y;
    }
    void displayData()
    {
        cout<<rupees<<" Rupees and "<<paisa<<" paisa"<<endl;
    }
    void calc(Money m1, Money m2)
    {
        paisa=m1.paisa+m2.paisa;
        rupees=paisa/100;
        rupees=rupees%100;
        rupees=rupees+m1.rupees+m2.rupees;
    }
};
int main()
{
    Money m1,m2,m3;
    m1.inputData(50,67);
    m2.inputData(100,80);
    m3.calc(m1,m2);
    cout<<"Object 1 has:";
    m1.displayData();
    cout<<"Object 2 has:";
    m2.displayData();
    cout<<"Object 3 has:";
    m3.displayData();
    return 0;
}
```
