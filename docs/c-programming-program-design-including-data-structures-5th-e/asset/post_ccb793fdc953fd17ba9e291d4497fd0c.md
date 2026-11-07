
In C++, virtual functions are declared using the reserved word `virtual`. Let us redefine the previous classes using this feature.

```cpp
class petType
{
public:
    virtual void print();       //virtual function
    petType(string n = "");

private:
    string name;
};

class dogType: public petType
{
public:
    void print();
    dogType(string n = "", string b = "");

private:
    string breed;
};
```

Note that we need to declare a virtual function only in the base class.

The definition of the member function `print` is the same as before. If we execute the previous program with these modifications, the output is as follows.

**Sample Run:**

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy, Breed: German Shepherd
```

This output shows that for the statement in Line 9, the `print` function of `dogType` is executed (see the last two lines of the output).

The previous discussion also applies when a formal parameter is a pointer to a class, and a pointer of the derived class is passed as an actual parameter. To illustrate this feature, suppose we have the preceding classes. (We assume that the definition of the class `petType` is in the header file `petType.h`, and the definition of the class `dogType` is in the header file `dogType.h`.) Consider the following program:

```cpp
#include <iostream>
#include "petType.h"
#include "dogType.h"

using namespace std;

void callPrint(petType *p);

int main()
{
    petType *q;                //Line 1
    dogType *r;                //Line 2

    q = new petType("Lucky");                 //Line 3
    r = new dogType("Tommy", "German Shepherd"); //Line 4

    q->print();                                  //Line 5
    cout << endl;                                //Line 6
    r->print();                                  //Line 7

    cout << "*** Calling the function callPrint ***"
         << endl;                                //Line 8
    callPrint(q);                                //Line 9
    cout << endl;                                //Line 10
    callPrint(r);                                //Line 11

    return 0;
}

void callPrint(petType *p)
{
    p->print();
}
```

**Sample Run:**

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy, Breed: German Shepherd
```

The preceding examples show that if a formal parameter, say `p`, of a class type, is either a reference parameter or a pointer and `p` uses a virtual function of the base class, we can effectively pass a derived class object as an actual parameter to `p`.

However, if `p` is a value parameter, then this mechanism of passing a derived class object as an actual parameter to `p` does not work, even if `p` uses a virtual function. Recall that, if a formal parameter is a value parameter, the value of the actual parameter is copied into the formal parameter. Therefore, if a formal parameter is of a class type, the member variables of the actual object are copied into the corresponding member variables of the formal parameter.

Suppose that we have the above classes—that is, `petType` and `dogType`. Consider the following function definition:

```cpp
void callPrint(petType p)  //p is a value parameter
{
    p.print();
}
```

Further suppose that we have the following declaration:

```cpp
dogType dog;
```

The object `dog` has two member variables, `name` and `breed`. The member variable `name` is inherited from the base class. Consider the following function call:

```cpp
callPrint(dog);
```

In this statement, because the formal parameter `p` is a value parameter, the member variables of `dog` are copied into the member variables of `p`. However, because `p` is an object of type `petType`, it has only one member variable. Consequently, only the member variable `name` of `dog` will be copied into the member variable `name` of `p`. Also, the statement:

```cpp
p.print();
```

in the body of the function will result in executing the member function `print` of the `class petType`.

The output of the following program further illustrates this concept. (As before, we assume that the definition of the `class petType` is in the header file `petType.h`, and the definition of the `class dogType` is in the header file `dogType.h`.)

```cpp
//Chapter 13: Virtual Functions and Value Parameters

#include <iostream>
#include "petType.h"
#include "dogType.h"

using namespace std;

void callPrint(petType p);

int main()
{
    petType pet("Lucky");                         //Line 1
    dogType dog("Tommy", "German Shepherd");      //Line 2

    pet.print();                                   //Line 3
    cout << endl;                                  //Line 4
    dog.print();                                   //Line 5

    cout << "*** Calling the function callPrint ***"
         << endl;                                  //Line 6
    callPrint(pet);                                //Line 7
    cout << endl;                                  //Line 8
    callPrint(dog);                                //Line 9
    cout << endl;                                  //Line 10

    return 0;
}

void callPrint(petType p)  //p is a value parameter
{
    p.print();
}
```

**Sample Run:**

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy
```

Look closely at the output of the statements in Lines 7 and 9 (the last two lines of output). In Line 9, because the formal parameter `p` is a value parameter, the member variables of `dog` are copied into the corresponding member variables of `p`. However, because `p` is an object of type `petType`, it has only one member variable. Consequently, only the member variable `name` of `dog` is copied into the member variable `name` of `p`. Moreover, the statement `p.print();` in the function `callPrint` executes the function `print` of the class `petType`, not of the class `dogType`. Therefore, the last line of the output shows only the value of `name` (the member variable of `dog`).

> **NOTE** An object of the base class type cannot be passed to a formal parameter of the derived class type.

Before closing this section, we discuss another issue related to virtual functions.

Suppose that the definition of the class `petType` is as before, and the definition of the class `dogType` is modified slightly as follows:

```cpp
class dogType: public petType
{
public:
    void print();
    void setBreed(string b = "");
    dogType(string n = "", string b = "");

private:
    string breed;
};
```

Consider the following statements:

```cpp
petType pet("Lucky");
dogType dog("Tommy", "German Shepherd");

pet = dog;
```

C++ allows this type of assignment, that is, the values of a derived class object can be copied into a base class object. (Note that the reverse statement, that is, `dog = pet;` is not allowed.) Now, because the object `pet` has only one data member (`name`) and the object `dog` has two data members (`name` and `breed`), only the value of the data member `name` of `dog` is copied into the data member `name` of `pet`. This is called the **slicing problem**. The following statement will result in a compile-time error.

```cpp
pet.setBreed("Siberian Husky");
```

C++ offers a way to treat a `dogType` object as a `petType` object without losing the additional properties of the class `dogType` by using pointers.

For example, suppose that you have the following statements:

```cpp
petType *pet;
dogType *dog;
```

```cpp
dog = new dogType("Tommy", "German Shepherd");
dog->setBreed("Siberian Husky");
```

```cpp
pet = dog;
```

In this case, the output of the statement `pet->print();` is: **Name:** Tommy, **Breed:** Siberian Husky

## Classes and Virtual Destructors

One thing recommended for classes with pointer member variables is that these classes should have the destructor. The destructor executes automatically when the class object goes out of scope. Thus, if the object creates dynamic memory space, the destructor can be designed to deallocate that memory space. If a derived class object is passed to a formal parameter of the base class type, the destructor of the base class executes regardless of whether the derived class object is passed by reference or by value. Logically, however, the destructor of the derived class should be executed when the derived class object goes out of scope.

To correct this problem, the destructor of the base class must be virtual. The **virtual destructor** of a base class automatically makes the destructor of a derived class virtual. When a derived class object is passed to a formal parameter of the base class type, then when the object goes out of scope, the destructor of the derived class executes. After executing the destructor of the derived class, the destructor of the base class executes. Therefore, when the derived class object is destroyed, the base class part (that is, the members inherited from the base class) of the derived class object is also destroyed.

If a base class contains virtual functions, make the destructor of the base class virtual.

## Abstract Classes and Pure Virtual Functions

The preceding sections discussed virtual functions. Other than enforcing run-time binding of functions, virtual functions also have another use, which is discussed in this section. Chapter 12 discussed the second principle of OOD—inheritance. Through inheritance we can derive new classes without designing them from scratch. The derived classes, in addition to inheriting the existing members of the base class, can add their own members and also redefine or override public and protected member functions of the base class. The base class can contain functions that you would want each derived class to implement. There are many scenarios for which a class is desired to be served as a base class for a number of derived classes; however, the base class may contain certain functions that may not have meaningful definitions in the base class.

Let us consider the **class shape** given in Chapter 12. As noted in that chapter, from the **class shape**, you can derive other **classes**, such as rectangle, circle, ellipse,
