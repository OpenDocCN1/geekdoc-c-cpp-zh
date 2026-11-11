
```cpp
}
C(int c):A(c),B()
{
    cout<<"Parameterized constructor of C class, storing the value of c="<<c<<endl;
}
};

int main()
{
    C obj(10);
    return 0;
}
```

**Output:**

```text
Parameterized constructor of A class, storing the value of a=10
Default Constructor of B class
Parameterized constructor of C class, storing the value of c=10
```

In Listing 21, A and B are base classes of class C. Class A has two constructors, A() and A(int a), class B has a default constructor, called B(), and class C has a default constructor, C(), and a parameterized constructor, C(int c):A(c),B(), which is passing argument to the constructors of the A and B classes explicitly. The following code snippet shows the parameterized constructor of class C:

```cpp
C(int c) : A(c),B()
{
    ...
}
```

In the preceding code snippet, the parameterized constructor of class C invokes the base class constructors explicitly. Therefore, the obj object of class C invokes the constructors of all the classes in the following order: the parameterized constructor of class A, then the default constructor of class B, and then the parameterized constructor of class C.

It is important to note that if the order of the explicit declaration of base class constructors is changed, as shown in given code snippet, the result does not change:

```cpp
C(int c) : B(), A(c)
{
    ...
...
}
```

The reason why the result does not change is that in multiple inheritance, the order of constructor invocation depends on the order of inheritance, as shown in the following code snippet:

```cpp
class C : public A , public B
{
...
...
};
```

This order of inheritance invokes the constructors of the base class as well as of the derived class, though it might be possible that the order of explicit calling of base classes by the derived class is different.

## TEST YOUR KNOWLEDGE

- **Q7.** Create a program to show an example of multiple inheritance.

**Ans.**

```cpp
#include <iostream.h>

class MyBase1 {
    int a;
public:
    MyBase1(int x) {
        a = x;
    }
    int geta() {
        return a;
    }
};

class MyBase2 {
    int b;
public:
    MyBase2(int x)
    {
        b = x;
    }
    int getb() {
        return b;
    }
};

class MyDerived : public MyBase1, public MyBase2{
    int c;
public:
    MyDerived(int x, int y, int z) : MyBase1(z), MyBase2(y){
        c = x;
    }
    void show() {
        cout << geta() << ' ' << getb() << ' ';
        cout << c << '\n';
    }
};

int main()
{
    MyDerived object(9,8,7);
    object.show();
    return 0;
}
```

**Output:**

```text
7 8 9
```

## Hybrid Inheritance

Hybrid inheritance is a combination of various types of inheritances, as shown in Figure 6:

![](img/8a6886c00caa6a1651a6c0e62bff341f_527_0.png)

▲ Figure 6: Displaying Hybrid Inheritance

In Figure 6, class H is inherited from the C, E, F, and G classes. In the figure, classes A, B, and C show multilevel inheritance, while D, E, and F show hierarchical inheritance.

Listing 22 shows an example of hybrid inheritance (you can find the HybridInheritance.cpp file on the CD in the Code\Chapter7 folder):

### Listing 22: Implementing Hybrid Inheritance

```cpp
#include<iostream.h>

class MumbaiUniversity
{
    public:
    MumbaiUniversity()
    {
        cout<<"Mumbai University constructor calling"<<endl;
    }
    ~MumbaiUniversity()
    {
        cout<<"Mumbai University destructor calling"<<endl;
    }
};
class DelhiUniversity
{
    public:
    DelhiUniversity()
    {
        cout<<"Delhi University constructor calling"<<endl;
    }
    ~DelhiUniversity()
    {
        cout<<"Delhi University destructor calling"<<endl;
    }
};
class College:public DelhiUniversity
{
    public:
    College()
    {
        cout<<"College constructor calling"<<endl;
    }
    ~College()
    {
        cout<<"College destructor calling"<<endl;
    }
};
class MorningCollege:public College
{
    public:
    MorningCollege()
    {
        cout<<"Morning College constructor calling"<<endl;
    }
    ~MorningCollege()
    {
        cout<<"Morning College destructor calling"<<endl;
    }
};
class EveningCollege:public College
{
public:
    EveningCollege()
    {
        cout<<"Evening College constructor calling"<<endl;
    }
    ~EveningCollege()
    {
        cout<<"Evening College destructor calling"<<endl;
    }
};
class Correspondence:public DelhiUniversity
{
public:
    Correspondence()
    {
        cout<<"Correspondence constructor calling"<<endl;
    }
    ~Correspondence()
    {
        cout<<"Correspondence destructor calling"<<endl;
    }
};
class External:public DelhiUniversity
{
public:
    External()
    {
        cout<<"External constructor calling"<<endl;
    }
    ~External()
    {
        cout<<"External destructor calling"<<endl;
    }
};
class Student:public MumbaiUniversity,public MorningCollege,public EveningCollege,public External,public Correspondence
{
    char name[5];
    char id[10];
    int marks;
public:
    Student()
    {
        cout<<"Student constructor calling"<<endl;
    }
    ~Student()
    {
        cout<<"Student destructor calling"<<endl;
    }
    void acceptData()
    {
        cout<<"Accepting Student Details"<<endl;
        cout<<"Enter student id"<<endl;
        cin>>id;
        cout<<"Enter student name"<<endl;
        cin>>name;
        cout<<"Enter student marks"<<endl;
        cin>>marks;
    }
    void displayData()
    {
        cout<<"Showing Student Details"<<endl;
        cout<<"Id: "<<id<<endl;
        cout<<"Name: "<<name<<endl;

        cout<<"Marks: "<<marks<<endl;
    }
};
int main()
{
    Student s;
    s.acceptData();
    s.displayData();
    return 0;
}
```

**Output:**

```text
Mumbai University constructor calling
Delhi University constructor calling
College constructor calling
Morning College constructor calling
Delhi University constructor calling
College constructor calling
Evening College constructor calling
Delhi University constructor calling
External constructor calling
Delhi University constructor calling
Correspondence constructor calling
Student constructor calling
Accepting Student Details
Enter student id
1001
Enter student name
Shilpa
Enter student marks
87
Showing Student Details
Id: 1001
Name: Shilpa
Marks: 87
Student destructor calling
Correspondence destructor calling
Delhi University destructor calling
External destructor calling
Delhi University destructor calling
Evening College destructor calling
College destructor calling
Delhi University destructor calling
Morning College destructor calling
College destructor calling
Delhi University destructor calling
Mumbai University destructor calling
```

In Listing 22, the College, External, and Correspondence classes are inherited from the DelhiUniversity class, and the MorningCollege and EveningCollege classes are inherited from the College class. Note that the MumbaiUniversity class is not a base class or a derived class of any of these classes, but a stand alone class. The Student class is derived from the MumbaiUniversity, MorningCollege, EveningCollege, External, and Correspondence classes (in the same order). Each class has a pair of constructor and destructor of its own. The derived class, Student, has two member functions, acceptData() and displayData(). In addition, in the main() function, the s object of the Student class invokes the constructor, destructor, and functions of all the classes according to the order of inheritance of these classes.

![](img/8a6886c00caa6a1651a6c0e62bff341f_531_0.png)

- **1.** Explain inheritance in Object oriented programming in C++ in terms of Multiple inheritances, level of inheritance, Deriving classes in public, private and protected mode. Use suitable programs and class definitions for exemplifications of the concepts.
- **2.** Write Object Oriented programs to exemplify different types of inheritance namely
  - public
  - protected
  - private
  - and multiple and hierarchical Inheritance (Mumbai University, December 2007)
