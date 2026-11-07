
Recall that if a formal parameter is a value parameter, the value of the actual parameter is copied into the formal parameter. Therefore, if a formal parameter is of a `class` type, the member variables of the actual object are copied into the corresponding member variables of the formal parameter.

Suppose that we have the above classes—that is, `petType` and `dogType`. Consider the following function definition:

```cpp
void callPrint(petType p)   // p is a value parameter
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

In this statement, because the formal parameter `p` is a value parameter, the member variables of `dog` are copied into the member variables of `p`. However, because `p` is an object of type `petType`, it has only one member variable. Consequently, only the member variable `name` of `dog` will be copied into the member variable `name` of `p`. Also, because the statement

```cpp
p.print();
```

in the body of the function is linking `print` to the `petType` object `p`, it will result in executing the member function `print` of the `class` `petType`.

The output of the following program further illustrates this concept. (As before, we assume that the definition of the `class` `petType` is in the header file `petType.h` and the definition of the `class` `dogType` is in the header file `dogType.h`.)

```cpp
//Chapter 12: Virtual Functions and value parameters

#include <iostream>
#include "petType.h"
#include "dogType.h"

using namespace std;

void callPrint(petType p);

int main()
{
    petType pet("Lucky");                 //Line 1
    dogType dog("Tommy", "German Shepherd"); //Line 2

    pet.print();                          //Line 5
    cout << endl;                         //Line 6
    dog.print();                          //Line 7
    cout << "*** Calling the function callPrint ***"    //Line 8
         << endl;                                      //Line 9
    callPrint(pet);                                    //Line 10
    cout << endl;                                      //Line 11
    callPrint(dog);                                    //Line 12
    cout << endl;                                      //Line 13

    return 0;                                          //Line 14
}

void callPrint(petType p)    // p is a value parameter
{
    p.print();
}
```

### Sample Run:

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy
```

Look closely at the output of the statements in Lines 9 and 11 (the last two lines of output). In Line 11, because the formal parameter `p` is a value parameter, the member variables of `dog` are copied into the corresponding member variables of `p`. However, because `p` is an object of base type `petType`, it has only the one member variable `name`. Consequently, only the member variable `name` of `dog` is copied into the member variable `name` of `p`. Moreover, the statement `p.print()` in the function `callPrint` executes the function `print` of the base class `petType`, not of the derived class `dogType`. Therefore, the last line of the output shows only the value of `name` (the member variable of `dog`).

> **NOTE** An object of the base class cannot be passed to a formal parameter of the derived class type because it is missing the derived class “parts.”

Before closing this section, we discuss another issue related to virtual functions.

Suppose that the definition of the class `petType` is as before, and the definition of the class `dogType` is modified slightly as follows:

```cpp
class dogType: public petType
{
public:
    void print() const;
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
```

```cpp
pet = dog;
```

C++ allows this type of assignment, that is, the values of a derived class object can be copied into a base class object. (Note that the reverse statement, that is, `dog = pet;` is not allowed.) Now, because the object `pet` has only one data member (`name`), only the value of the data member `name` of `dog` is copied into the data member `name` of `pet`. This is called the **slicing problem**. The following statement will result in a compile-time error.

```cpp
pet.setBreed("Siberian Husky");
```

C++ offers pointers as a way to treat a `dogType` object as a `petType` object without losing the additional properties of the class `dogType`.

For example, suppose that you have the following statements:

```cpp
petType *pet;
dogType *dog;

dog = new dogType("Tommy", "German Shepherd");
dog->setBreed("Siberian Husky");

pet = dog;
```

The last statement copies the value of `dog`, which is a reference to the object `dog`, into `pet`. So the pointer `pet` points to the object `dog`. Therefore, the output of the statement `pet->print();` is:

```text
Name: Tommy, Breed: Siberian Husky
```

## Classes and Virtual Destructors

One thing recommended for classes with pointer member variables is that these classes should have the destructor. The destructor executes automatically when the class object goes out of scope. Thus, if the object creates dynamic memory space, the destructor can be designed to deallocate that memory space. If a derived class object is passed to a formal parameter of the base class type, the destructor of the base class executes regardless of whether the derived class object is passed by reference or by value. Logically, however, the destructor of the derived class should be executed when the derived class object goes out of scope.

To correct this problem, the destructor of the base class must be virtual. The **virtual destructor** of a base class automatically makes the destructor of a derived class virtual. When a derived class object is passed to a formal parameter of the base class type, then when the object goes out of scope, the destructor of the derived class executes. After executing the destructor of the derived class, the destructor of the base class executes. Therefore, when the derived class object is destroyed, the base class part (that is, the members inherited from the base class) of the derived class object is also destroyed.

If a base class contains virtual functions, make the destructor of the base class virtual.

## Abstract Classes and Pure Virtual Functions

The preceding sections discussed virtual functions. Other than enforcing run-time binding of functions, virtual functions also have another use, which is discussed in this section. Chapter 11 discussed the second principle of OOD—inheritance. Through inheritance we can derive new classes without designing them from scratch. The derived classes, in addition to inheriting the existing members of the base class, can add their own members and also redefine or override public and protected member functions of the base class. The base class can contain functions that we would want each derived class to implement. There are many scenarios when it is desirable for a class to serve as a base class for a number of derived classes; however, the derived classes may contain certain functions that may not have meaningful definitions in the base class.

Let us consider the class `shape` given in Chapter 11. As noted in that chapter, from the class `shape`, you can derive other classes, such as rectangle, circle, ellipse, and so on. Some of the things common to every shape are its center, using the center to move a shape to a different location, and drawing the shape. We can include these in the class `shape`. For example, you could have the definition of the class `shape` similar to the following:

```cpp
class shape
{
public:
    virtual void draw();
        //Function to draw the shape.

    virtual void move(double x, double y);
        //Function to move the shape at the position (x, y).

    .
    .
    .
};
```

Because the definitions of the functions `draw` and `move` are specific to a particular shape, each derived class can provide an appropriate definition of these functions. Note that we have made the functions `draw` and `move` virtual to enforce run-time binding of these functions.

This definition of the class `shape` requires you to write the definitions of the functions `draw` and `move`. However, at this point, there is no shape to draw or move. Therefore, these function bodies have no code. One way to handle this is to make the body of these functions empty. This solution would work, but it has a drawback. Once we write the definitions of the functions of the class `shape`, then we could create an object of this class and invoke the empty `draw` and `move` functions. Because there is no shape to work with, we would like to prevent the user from creating objects of the class `shape`. It follows that we would like to do the following two things—not include the definitions of the functions `draw` and `move` and to prevent the user from creating objects of the class `shape`.
