
```cpp
{
    cout<<"Enter exam code"<<endl;
    cin>>ecode;
}
};
class external : public student, public exam
{
    public :
    int marks;
    void display4()
    {
        cout<<"Enter your Level1 marks"<<endl;
        cin>>marks;
    }
    void check()
    {
        if ((age>17)&&(marks>65))
        {
            cout<<"\nAllowed for Level 2 Examination :)\n";
        }
        else
            cout<<"Start looking for backups :(( \n";
    }
};
int main()
{
    external e;
    cout<<"Enter your valid information"<<endl;
    e.display1();
    e.display2();
    e.display3();
    e.display4();
    e.check();
    return 0;
}
```

### Output:

```text
Enter your valid information
Enter your age
20
Enter your name
Mick
Enter exam code
203
Enter your Level1 marks
24
Start looking for backups :((
```

## 6.4 Constructor Calling

In the previous chapter, we discussed class making and methods, as well as special methods like constructors and their various types. There, we dealt with only a single class, but with inheritance, there will always be more than one class. How does constructor calling work? Let’s take a look.

### Remember

- The base class constructor is always called first, irrespective of the object made.
- Derived class object creation results in initializing all of its members, but it has inherited members, too. Hence, the base class constructor is called first to enable all members to initialize in the derived class.
- In the case of multiple inheritance, the base class order of placement will decide which constructor is called.
- Destructors are always called in the opposite order of the constructors.

The syntax for calling a constructor is as follows:

```cpp
class A
{
        //class body
        A();
};
class B : accessMode A
{
        // class body
        B();
};
class C : accessMode B
{
    // class body
    C();
};

C object;
```

![](img/4d9a4ae4efedabe01be6e6c44bad2dc1_141_0.png)

*Figure 6.7* Constructor order

*Figure 6.8* Destructor order

## 6.5 Implementing Inheritance

Inheritance is an important object-oriented programming concept that you use with classes. A few of the advantages of inheritance are as follows:

- 1. *Code reusability:* As the relationship between parent and child classes allows for the sharing of methods, we do not need to write the same code body again and again.
- 2. *Structure:* It makes code easier to understand, as methods do not repeat and the child objects can access all the inherited methods.
- 3. *Efficiency:* Inheritance saves a lot of time and energy in fetching data from one class to obtain the result.
- 4. *Extensibility:* Classes (as well members) are able to extend their features and functionalities through derived or child classes.

The following example of inheritance highlights its importance and ease of use.

### Code: Programming with Inheritance

```cpp
#include <iostream>
using namespace std;
class person
{
    public:
    int age;
    void display1()
    {
        cout<<"Enter your age"<<endl;
        cin>>age;
    }
};
class student : public person
{
    public :
    int ugYear;
    void display2()
    {
        cout<<"Enter your Under Graduate passing Year"<<endl;
        cin>>ugYear;
    }
};
class exam: public student
{
    public :
    void check()
    {
        if((age>18) && (ugYear== 2021 || ugYear== 2022))
            cout<<"You Can appear for CAT 2022"<<endl;
        else
            cout<<"Sorry you Cannot appear for CAT 2022"<<endl;
    }
};

int main()
{
    exam e;
    cout<<"Enter valid information"<<endl;
    e.display1();
    e.display2();
    e.check();
    return 0;
}
```

### Output:

```text
Enter valid information
Enter your age
19
Enter your Under Graduate passing Year
2023
Sorry you Cannot appear for CAT 2022
```

Do your own “code debriefing” of this code and try making your own versions of inheritance in C++.

## Summary

- *Inheritance* in C++ allows a child class to inherit features of its parent class.
- The parent class (or the base class or super class) is a single entity that existed before the child class, and all its children inherit properties from it.
- The child class (or the derived class or sub class) is made out of certain features of the base class.
- Data members declared public can be accessed by any class, irrespective of the relationship its class has with other classes.
- Data members declared private have limited access available to only the base, friend, and derived classes.
- Data members declared protected can be accessed by base class members and friend classes.

home. All classes must have interface functions, such as overloaded stream operator functions for reading and displaying attributes. Write an interactive program that can be used to model this relationship.

- 3. Write a program in C++ to depict multilevel inheritance using real life entities.
- 4. Write a program in C++ to create a relation between grandparent and grandchild classes with overriding methods in both.
- 5. Write a program in C++ to show access to private, public, and protected classes using inheritance.
- 6. Write a program in C++ to depict a constructor’s purpose in single inheritance.
- 7. Write a program in C++ to depict a constructor’s purpose in multilevel inheritance.
- 8. Write a program in C++ to depict a constructor’s purpose in multiple inheritance.
- 9. Write a program in C++ to depict a constructor’s purpose in hierarchical inheritance.
- 10. Write a program in C++ to depict a constructor’s purpose in virtual inheritance.
- 11. Write a program in C++ to depict a constructor’s purpose in hybrid inheritance.

## MCQ-Based

- 1. What is inheritance in C++?
  - a. Wrapping of data into a single class
  - b. Deriving new classes from existing classes
  - c. Overloading of classes
  - d. Classes with the same names
- 2. Which of the following statement is correct about virtual inheritance?
  - a. It is a technique to ensure that a private member of a base class can be accessed.
  - b. It is a technique to optimize multiple inheritances.
  - c. It is a technique to avoid the multiple inheritances of the classes.
  - d. It is a technique to avoid creating multiple copies of the base class code for the derived or child classes.
- 3. If a class is derived privately from a base class, then
  - a. no members of the base class are inherited.
  - b. all members are accessible by the derived class.
  - c. all the members are inherited by the class, but are hidden and cannot be accessed.
  - d. no derivation of the class gives an error.
- 4. What will be the output of the following C++ code?

```cpp
#include <iostream>
#include <string>
using namespace std;
class A
{
    float d;
public:
    virtual void func(){
        cout<<"Hello this is class A\n";
    }
};
class B: public A
{
    int a = 15;
public:
    void func(){
        cout<<"Hello this is class B\n";
    }
};
int main(int argc, char const *argv[])
{
    A *a = new A();
    B b;
    a = &b;
    a->func();
    return 0;
}
```

  - a. Hello this is class A
  - b. Hello this is class B
  - c. Error
  - d. Segmentation Fault
- 5. Write the output of the following code.

```cpp
#include <iostream>
#include <string>
using namespace std;
class A
{
    float d;
    public:
    virtual void func(){
        cout<<"Hello this is class A\n";
    }
};
class B: public A
{
    int a = 15;
    public:
    void func(){
        cout<<"Hello this is class B\n";
    }
};
int main(int argc, char const *argv[])
{
    A *a;
    a->func();
    return 0;
}
```

  - a. Hello this is class A
  - b. Hello this is class B
  - c. Error
  - d. Segmentation Fault
- 6. What will be the output of the following C++ code?

```cpp
#include <iostream>
#include <string>
using namespace std;
class A{
    float d;
```
