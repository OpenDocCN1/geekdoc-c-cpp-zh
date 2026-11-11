
Problem in resolving the function calls, if a function with same name is present in more than one parent classes. As an example, let us create three parent classes X, Y and Z with a single child class as C as shown in the Figure 14.38. Further, let us create a function named **f1()** and a variable named **a** in each of the classes in order to understand the resolution of ambiguity in multiple inheritance.

This would mean that the child class C will contain four functions named as f1() and four variables with name a (one from each of the parents and the one defined in class C itself). To avoid confusion, let's concentrate only on the function **f1()** first.

We create an object **o1** of class C and invoke the **f1()** as shown below:

```cpp
C o1;
o1.f1();
```

In this case, the compiler will correctly invoke the f1() defined in class C because **o1** is of type **C**. As per the principle of early binding, the compiler always determines the function to be invoked based on the data type of the object, which has invoked the function. Therefore, the control is correctly transferred to **f1()** defined in class C. If we further attempt to make another call to **f1()** within the scope of class C, the compiler will recursively keep calling the same function **f1()** again as shown in Figure 14.39. How can we call versions of **f1()** defined in parent classes X, Y, and Z? This situation is called as **ambiguity in multiple inheritance**, which can be resolved using a **scope resolution operator**.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_824_0.png)

**Figure 14.39:** Ambiguity in multiple inheritance

We resolve this ambiguity using the scope resolution operator as shown in the code. The statement **X::f1()** will call the f1() of class X. Similarly, the statements **Y::f1()** and **Z::f1()** will invoke function of class Y and Z respectively, as shown in the Figure 14.40.

We learnt how ambiguity can be resolved in function calls when a function is called within the scope of the child class. You can also invoke the function defined in any of the parent classes using the child object, directly from **main()**. The statement

```cpp
o1.X::f1();
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_825_0.png)

will invoke the f1() defined in class X even if object o1 is of type C. This is because we have explicitly asked the compiler to invoke function f1() within the scope of X using the scope resolution operator.

Similarly, the statements

```cpp
o1.Y::f1();
```

```cpp
o1.Z::f1();
```

will invoke f1() defined in class Y and Z, respectively.

The statements

```cpp
o1.C::f1();
```

and

```cpp
o1.f1();
```

are equivalent because they both will invoke the function f1() defined in class C.

Ambiguity with member variables can be resolved in the same way as that of member functions. For example, the statement written in f1() of class C

```cpp
cout<<"Value of variable a of X is:"<<X::a<<endl;
```

will print the value of variable a defined in class X (which is 1, as initialized by constructor of class X). Similarly, the other two statements

```cpp
cout<<"Value of variable a of Y is:"<<Y::a<<endl;
cout<<"Value of variable a of Z is:"<<Z::a<<endl;
```

will print the value of variable a in class Y and class Z, respectively.

The following statement without any scope resolution operator written inside f1() of class C

```cpp
cout<<"Value of variable a of C is:"<<a<<endl;
```

will print the value of variable a of class C itself. This is because we are already in the scope of class C. You can also rewrite this statement by using the scope resolution operator explicitly as shown below:

```cpp
cout<<"Value of variable a of C is:"<<C::a<<endl;
```

The following is the full source code of ambiguity resolution:

```cpp
#include<iostream.h>
class X
{
protected:
int a;
public:
    X()
    {
    a=1;
    }
    void f1()
    {
        cout<<"Function of class X"<<endl;
        cout<<"Value of variable a of X is:"<<a<<endl;
    }
};
class Y
{
protected:
int a;
public:
    Y()
    {
    a=2;
    }
    void f1()
    {
        cout<<"Function of class Y"<<endl;
        cout<<"Value of variable a of Y is:"<<a<<endl;
    }
};
class Z
{
protected:
int a;
public:
    Z()
    {
    a=3;
    }
};
```

![](img/57c0d966bb33c67a5a188e6bf39e4e02_829_0.png)

**Figure 14.42:** Virtual base class

![](img/57c0d966bb33c67a5a188e6bf39e4e02_829_1.png)

**Figure 14.43:** Syntax for creating virtual base class

In such a case, the grandparent class (G) should be created as a virtual base class while defining the parent classes P1 and P2 as shown in the Figure 14.43. Note that each of the parent classes (P1 as well as P2) must add a keyword virtual in their definition which will actually create class G as the logical parent of child class C. In actuality, inheritance is all about making instance of parent class available to the child class. In this case, instead of getting the instance of G from P1 as well as P2, class C gets the instance of G from G itself. Adding keyword virtual ensures that a single copy of object of G is maintained within the object of class C. The internal implementation of virtual base classes using pointers is discussed later in this chapter in section 14.13.2, don’t worry about it right now.

### NOTES

- 1. The order of keywords `virtual` and `public` is interchangeable while defining the parent classes P1 and P2.
- 2. This theory can be extended to any number of parent classes in between G and C say P1, P2, P3....Pn and is not just limited to two parent classes.

As an example, let us create a C++ program for the hierarchy given in Figure 14.44.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_830_0.png)

**Figure 14.44:** Hierarchy showing the usage of virtual base class

The complete hierarchy is very similar as discussed in section 14.4.2 with the only difference being that there is an additional child class named as AssistantProf. The class AssistantProf inherits the features of both Student as well as Professor. This means that an object of AssistantProf represents a Person who is both Student and Professor in the real world. This is a very realistic example because a Person can be a teacher for undergraduate courses and pursuing postgraduate at the same time. This means that members and member functions of class Person would be inherited twice into the class AssistantProf, first time through the path from first parent class (Student) and second time through the path from second parent class (Professor), thereby resulting into ambiguity in the inheritance. To solve this problem, we create class Person as a virtual base class by adding keyword virtual while defining the immediate parent classes Student and Professor as shown below:

```cpp
class Person
{
……
};
class Student: public virtual Person
{
…… /*Student is a child class of Person */
};
class Professor: public virtual Person
{
…… /*Professor is a child class of Person */
};
class AssistantProf: public Student , public Professor
{
…… /* AssistantProf is a child class of Student and Professor.
This is called as multiple inheritance*/
};
```

The following is the full source code for the example:

```cpp
#include<iostream.h>
#include<Windows.h>
#include <stdio.h>
class Date
{
private:
    int dd;
    int mm;
    int yy;
public:
    void inputDate()
    {
        cout<<"Enter dd:"<<endl;
            cin>>dd;
        cout<<"Enter mm:"<<endl;
            cin>>mm;
        cout<<"Enter yyyy:"<<endl;
            cin>>yy;
    }
    void outputDate()
    {
        cout<<"dd:"<<dd<<"-"<<mm<<"-"<<yy<<endl;
    }
    void outputAge()
    {
        cout<<yy<<" years and "<<mm<<" months and "<<dd<<" days"<<endl;
    }
    static Date getCurrentDate()
    {
        SYSTEMTIME system;
        GetSystemTime(&system);
        Date today;
        today.dd=system.wDay;
        today.mm=system.wMonth;
        today.yy=system.wYear;
        return today;
    }
    Date getDateDiff(Date d)
    {
        Date result;
        if(dd>=d.dd)
        {
            result.dd = dd-d.dd;
        }
        else
        {
            dd=dd+30;
            mm=mm-1;
            result.dd = dd-d.dd;
        }
        if(mm>=d.mm)
        {
            result.mm = mm-d.mm;
        }
        else
        {
            mm=mm+12;
            yy=yy-1;
            result.mm = mm-d.mm;
        }
        result.yy = yy-d.yy;
        return result;
    }
};
class Person
{
protected:
    char gender;
    char name[100];
```
