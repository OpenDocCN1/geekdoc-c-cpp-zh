
## Pointer this

A member function of a class can (directly) access the member variables of that class for a given object. Sometimes, it is necessary for a member function to refer to the object as a whole, rather than the object's individual member variables. How do you refer to the object as a whole (that is, as a single unit) in the definition of the member function, especially when the object is not passed as a parameter? Every object of a class maintains a (hidden) pointer to itself, and the name of this pointer is *this*. In C++, *this* is a reserved word. The pointer *this* (in a member function) is available for you to use. When an object invokes a member function, the member function references the pointer *this* of the object. For example, suppose that *test* is a class and has a member function called *one*. Further suppose that the definition of *one* looks like the following:

```cpp
test test::one()
{
    .
    .
    .
    return *this;
}
```

If *x* and *y* are objects of type *test*, then the statement:

```cpp
y = x.one();
```

copies the value of object *x* into object *y*. That is, the member variables of *x* are copied into the corresponding member variables of *y*. When object *x* invokes function *one*, the pointer *this* in the definition of the member function *one* refers to object *x*, so *this* means the address of *x* and `*this` means the value of *x*.

The following example illustrates how the pointer *this* works.

### EXAMPLE 15-1

Consider the following class:

```cpp
class thisPointerClass
{
public:
    void set(int a, int b, int c);
    void print() const;

    thisPointerClass updateXYZ();
    // Postcondition: x = 2 * x; y = y + 2;
    //                z = z * z;

    thisPointerClass(int a = 0, int b = 0, int c = 0);

private:
    int x;
    int y;
    int z;
};
```

Suppose that the definitions of the member functions of the class thisPointerClass are as follows:

```cpp
void thisPointerClass::set(int a, int b, int c)
{
    x = a;
    y = b;
    z = c;
}
```

```cpp
void thisPointerClass::print() const
{
    cout << "x = " << x
         << ", y = " << y
         << ", z = " << z << endl;
}
```

```cpp
thisPointerClass thisPointerClass::updateXYZ()
{
    x = 2 * x;
    y = y + 2;
    z = z * z;

    return *this;
}
```

The definition of the function updateXYZ updates the values of x, y, and z. Using the pointer this returns the value of the entire object. That is, the values of the member variables x, y, and z are returned.

```cpp
thisPointerClass::thisPointerClass(int a, int b, int c)
{
    x = a;
    y = b;
    z = c;
}
```

Consider the following function main:

```cpp
//Chapter 15: this pointer illustration

#include <iostream>
#include "thisPointerIllus.h"

using namespace std;

int main()
{
    thisPointerClass object1(3, 5, 7);      //Line 1
    thisPointerClass object2;              //Line 2

    cout << "Object 1: ";                  //Line 3
    object1.print();                       //Line 4

    object2 = object1.updateXYZ();         //Line 5

    cout << "After updating object1: ";    //Line 6
    object1.print();                       //Line 7

    cout << "Object 2: ";                  //Line 8
    object2.print();                       //Line 9

    return 0;
}
```

**Sample Run:**

```text
Object 1: x = 3, y = 5, z = 7
After updating object1: x = 6, y = 7, z = 49
Object 2: x = 6, y = 7, z = 49
```

For the most part, the output is self-explanatory. The statement in Line 5 evaluates the expression object1.updateXYZ(), which updates the values of the member variables of object1. The value of object1 is then returned by the pointer *this*, as shown in the definition of the function updateXYZ. The assignment operator then copies the value into object2.

The following example also shows how the pointer *this* works.

### EXAMPLE 15-2

In Example 12-9 in (Chapter 12), we designed a class to implement a person's name in a program. Here, we extend the definition of the class `personType` to individually set a person's first name and last name and then return the entire object. The extended definition of the class `personType` is:

```cpp
class personType
{
public:
    void print() const;
        //Function to output the first name and last name.
        //the form firstName lastName

    void setName(string first, string last);
        //Function to set firstName and lastName according
        //to the parameters.
        //Postcondition: firstName = first; lastName = last

    personType& setFirstName(string first);
        //Function to set the first name.
        //Postcondition: firstName = first
        //              After setting the first name, a reference
        //              to the object, that is, the address of the
        //              object, is returned.

    personType& setLastName(string last);
        //Function to set the last name.
        //Postcondition: lastName = last
        //              After setting the last name, a reference
        //              to the object, that is, the address of the
        //              object, is returned.

    string getFirstName() const;
        //Function to return the first name.
        //Postcondition: The value of firstName is returned.

    string getLastName() const;
        //Function to return the last name.
        //Postcondition: The value of lastName is returned.

    personType(string first = "", string last = "");
        //Constructor
        //Sets firstName and lastName according to the parameters.
        //Postcondition: firstName = first; lastName = last

private:
    string firstName; //variable to store the first name
    string lastName;  //variable to store the last name
};
```

Notice that in this definition of the class `personType`, we replace the default constructor and the constructor with parameters by one constructor with default parameters.

The definitions of the functions `print`, `setName`, `getFirstName`, `getLastName`, and the constructor are the same as before (see Example 12-9). The definitions of the functions `setFirstName` and `setLastName` are as follows:

```cpp
personType& personType::setLastName(string last)
{
    lastName = last;

    return *this;
}
```

```cpp
personType& personType::setFirstName(string first)
{
    firstName = first;

    return *this;
}
```

The following program shows how to use the `class` `personType`. (We assume that the definition of this class is in the file personType.h)

```cpp
//Test Program: class personType

#include <iostream>
#include <string>
#include "personType.h"

using namespace std;

int main()
{
        personType student1("Angela", "Smith");                    //Line 1

        personType student2;                                         //Line 2

        personType student3;                                         //Line 3

        cout << "Line 4 -- Student 1: ";                            //Line 4
        student1.print();                                             //Line 5
        cout << endl;                                                 //Line 6

        student2.setFirstName("Shelly").setLastName("Malik");       //Line 7

        cout << "Line 8 -- Student 2: ";                            //Line 8
        student2.print();                                             //Line 9
        cout << endl;                                                 //Line 10

        student3.setFirstName("Chelsea");                            //Line 11

        cout << "Line 12 -- Student 3: ";                           //Line 12
        student3.print();                                             //Line 13
        cout << endl;                                                 //Line 14

        student3.setLastName("Tomek");                               //Line 15

        cout << "Line 16 -- Student 3: ";                           //Line 16
        student3.print();                                             //Line 17
        cout << endl;                                                 //Line 18

        return 0;
}
```

**Sample Run:**

```text
Line 4 -- Student 1: Angela Smith
Line 8 -- Student 2: Shelly Malik
Line 12 -- Student 3: Chelsea
Line 16 -- Student 3: Chelsea Tomek
```

The statements in Lines 1, 2, and 3 declare and initialize the objects student1, student2, and student3, respectively. The objects student2 and student3 are initialized to empty strings. The statement in Line 5 outputs the value of student1 (see Line 4 in the sample
