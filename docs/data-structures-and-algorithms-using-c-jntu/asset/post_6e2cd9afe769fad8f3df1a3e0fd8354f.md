
```cpp
#include<string.h>
#include<conio.h>
class base
{
public:
virtual void date(int dd,int mm,int yy)
{
cout<<"\nBase Class date function:"<<dd<<"\\"<<mm<<"\\"<<yy;
}
};
class derived:public base
{
public:
void show()
{
cout<<"\n I am in the derived class";
}
};
void main()
{
clrscr();
base obj1;
obj1.date(1,1,2010);
derived obj2;
obj2.date(1,1,2010);
obj2.show();
}
```

Output

Base Class date function:1\1\2010
Base Class date function:1\1\2010
I am in the derived class

In Program 2.30, the virtual function is not redefined by the derived class. When obj2.date(1,1,2010) is called the base class definition of the date function will be called because the date function is not redefined by the derived class.

### 2.5.2 Pure Virtual Functions

A pure virtual function is a virtual function declared in the base class, but there is no definition for the virtual function, so that it can be overridden by the derived class. The pure virtual function must be defined by the derived class. When a function is declared as pure virtual function in a class, then that class cannot be used to declare any object because it becomes an abstract class.

A pure virtual function can be declared as

```
virtual return-type function-name(args)=0;
```

### Example

```
virtual void greet()=0;
```

Here greet is a pure virtual function and the assignment operation is not used to assign zero, but it imitates the compiler that it is a pure virtual function and it does not have definition.

### Program 2.31

```cpp
/*Program to demonstrate Pure Virtual Function*/
#include<iostream.h>
#include<conio.h>
class Base
{
    public:
    virtual void greet ()=0; /*Pure virtual function, memory will not
    be created for this method, But the derived
    classes can work with runtime polymorphism*/
};
class Derived:public Base
{
    public:
    void greet()
    {
    cout<<"\nHi! i am Derived Class";
    }
};
void main()
{
    Derived obj;
    clrscr();
    obj.greet();
}
```

### Output

Hi! i am Derived Class

In the base class for Program 2.31, the virtual method greet() is declared as a pure virtual function, but there is no definition for the method in the base class. When the derived class defines the pure virtual function, then the version of derived class will be called.

## 2.6 ABSTRACT CLASSES

An abstract class is a class where there exists at least one pure virtual function defined in the class. Creation of objects for the abstract class is not possible. Abstract classes can have pointers. The pure virtual functions of the abstract classes can be referred by the pointers. The implementation of runtime polymorphism is possible by the abstract classes. A Class is made as abstract by making one or more of its functions as pure.

### Program 2.32

```cpp
/*Program to Demonstrate ABSTRACT Class*/
#include<iostream.h>
#include<conio.h>
class Base
{
public:
virtual void greet()=0;
virtual void showBye()=0;
};
class Derived:public Base
{
public:
void greet()
{
cout<<"\nHi i am Derived Class";
}
void showBye()
{
cout<<"\nBye, Have a good day";
}
};
void main()
{
Derived obj;
clrscr();
obj.greet();
obj.showBye();
}
```

### Output

Hi i am Derived Class Bye, Have a good day

In the example in Program 2.32, the methods greet() and showBye() are defined as pure virtual functions. So, the base class is said to be an abstract class. The derived class derived the virtual functions of the abstract class and is defined in the derived class. When the derived class object calls the methods greet() and showBye(), then the derived class definitions will be called by the methods.

## 2.7 GENERIC PROGRAMMING WITH TEMPLATES

Template is one of the most useful software reuse feature of C++. Template defines a range of related functions called the function template and a range of related classes called the class template. This technique is called generic programming. A function that works for all functions is called a generic function. The data type will be passed as an argument to the generic function. By creating a template for the function sum(), it can be used to perform addition on any data type.

When there is a need to perform operations on different data types, normally function overloading is used, which increases the program size and also requires one to create more local variables, which also increase the memory requirement. Template overcomes the limitations of function overloading. The mechanism provided by the template can also be implemented on classes.

A generic function can be used for different data types. A generic function or a class can be defined by using template keyword.

### 2.7.1 FUNCTION TEMPLATES

A function can be defined as a template if its operations are similar on all the data types instead of overloading the function.

The general form of a template function is as follows:

```
template<class Template-type>return-type function-name(args)
{
    //definition of the template function.
}
```

Here template is a keyword to define the template function and template-type is a data type. return-type is the data type of the return value of the template function. The function-name is the name of the template function and args is the list of input arguments to the template function. The template type can be used as data type in the body of the generic function or a class.

### Example

```
template<class T>void echo_value()
{
    T value;
    cout<<“Enter a value:”;
    cin>>value;
    cout<<“\nYou have entered:”<<value;
}
```

In the example, T is the data type of the template function echo_value(). This function can be applied on any input argument type.

A template class or a function can have any number of template types.

### Program 2.33

```cpp
/*A template function with single generic data type*/
#include<iostream.h>
#include<conio.h>
template<class X> void add (X a, X b)
{
    X sum;
    sum=a+b;
    cout<<"\n"<<a<<"+"<<b<<"="<<sum;
}
void main()
{
clrscr();
add(10,20);
add(0.1,0.2);
}
```

### Output

10+20=30
0.1+0.2=0.3

In Program 2.33, the addition of two numbers is considered. A function written with integer arguments will operate for the other data types. It is also difficult to write a separate add function for all the data types. With the function overloading process, the add function can be defined for any of the data types, but the logic of the add function is the same for all the methods, which are defined for different data types. Generic function allows the developers to write a function, which has common logic for different data types. Function overloading is best suited for the functions with different logics.

The above generic function add is defined with a template class X. Here X can be any data type in the run-time. In the main function add(10,20) is invoked because (int,int) are passed to the generic function, the function works with the data type integer, i.e. X becomes an integer, and in the second statement add(0.1,0.2) is called, because the add function is called as add(float,float), at the time of execution X becomes float and the add function will work with float data types. Instead of writing two different functions for solving addition of integers and addition of float values, a single generic function can be used for any of the data types. The statement is generalized, a single generic function can be used for the different data types where the logic is the same for all the data types.

A template function can have more than one template type. The template types can be used as normal data types in the body of the generic function or a class.

### Program 2.34

```cpp
/*A template function with more than one generic data type*/
#include<iostream.h>
#include<conio.h>
template<class X,class Y>void generic_fun(X a,Y b)
{
cout<<"\nArgument values Received by the function:"<<a<<" "<<b;
}
void main()
{
clrscr();
generic_fun(10,20.2);
generic_fun(0.1,100);
generic_fun(10,"Hello World");
generic_fun(10.2,'H');
}
```

### Output

Argument values Received by the function:10 20.2
Argument values Received by the function:0.1 100
