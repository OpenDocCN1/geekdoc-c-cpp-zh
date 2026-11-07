
### Declaring Static Data Members

Data members belong to the class, and their declarations must be included in the class definition; *static* members must be qualified with the keyword *static*. The following shows how we declare a *static* data member named *count* inside the class definition.

```cpp
class Rectangle
{
  private:
    ...
    static int count;          // Static data member
  public:
    ...
};
```

### Initializing Static Data Members

We know that an instance data member is normally initialized in a constructor, but a *static* data member belongs to no instance, which means it cannot be initialized in a constructor. A *static* data member must be initialized after the class definition. This means it must be initialized in a global area of the program. We code it after the class definition. We must show that it belongs to the class by adding the class name and the class scope operator (::) to the definition, but the *static* qualifier should not be added. It is already qualified as a *static* data member in the definition section of the class. The following shows how we initialize the *static* member *count*, which is already declared inside the class.

```cpp
int Rectangle::count = 0;          // initialization of static data member
```

## 7.5.2 Static Member Functions

After declaring and initializing a *static* data member, we must find a way to access it (for example, to print its value). Since a *static* data member is normally *private*, we need a *public* member function to do so. Although this can be done by an instance member function, normally we use a *static* member function for this purpose. A *static* member function can access the *static* data member through an object and also through the name of the class when no object exists. In other words, the use of a *static* member function enables us to access the corresponding *static* data member when an instance wants to access it or when the application needs to access it. Note that a *static* member function has no host object because it is not associated with any instance.

> **A static member function has no host object.**

### Declaring Static Member Functions

A *static* member function, like a *static* data member, belongs to the class. It should be declared inside the class but must be qualified with the keyword *static*. The following shows how we can add a *static* member function *getCount* to retrieve the value of the *static* data member *count* in our *Rectangle* class.

```cpp
class Rectangle
{
    private:
        ...
        static int count;              // Static data member
    public:
        static int getCount();         // Static member function
        ...
};
```

### Defining Static Member Functions

A static member function must be defined outside of the class, like an instance member function. There is no difference between the definition of a static member function and an instance member function. If we want to see if a function definition is an instance or a static one, we need to refer to the declaration.

```cpp
int Rectangle::getCount()
{
    return count;
}
```

Note that we cannot use the const qualifier because there is no host object.

### Calling Static Member Functions

A static member function can be called either through an instance or through the class (for example, Rectangle). To call a static member function through an instance, we use the same syntax we use to call an instance member function; to call a static member function through the class, we use the name of the class and the class resolution operator (::). The following shows both methods.

```cpp
rect.getCount ();             // Through an instance
Rectangle :: getCount();      // Through the class
```

Warning: We cannot use a static member function to access an instance data member because a static member function does not have the hidden this pointer, which defines the instance that needs to be referenced.

> A static member function cannot be used to access instance data members because it has no this pointer parameter.

On the other hand, an instance member function can be used to access static data members (the this pointer is not used), but we usually avoid this. A good practice is to use instance member functions to access instance data members and static member functions to access static data members. We recommend that the territory of instance members in the program be separated from static members symbolically, as shown in Figure 7.13.

![](img/d68f6199646ca63591a6d8419e0ed4ba_323_0.png)

**Figure 7.13** Separation of instance and static territory

**EXAMPLE 7.4**

In this example we write a program that tests a static data member and the corresponding static member function using the *Rectangle* class. Program 7.5 also shows how we can count the instances.

**Program 7.5** Testing static members

```cpp
/****************************************************
 * A program to create objects and count them.       *
 ****************************************************/
#include <iostream>
using namespace std;
/****************************************************
 * Definitions of the class Rectangle              *
 ****************************************************/
class Rectangle
{
private:
    double length;
    double height;
    static int count;   // Static data member
public:
    Rectangle (double length, double height);
    Rectangle ();
    ~Rectangle ();
    Rectangle (const Rectangle& rect);
    static int getCount ();  // Static member function
};
// Initialization of static data member
int Rectangle :: count = 0;
/****************************************************
 * Definitions of instance member functions        *
 ****************************************************/
// Definition of parameter constructor

Rectangle :: Rectangle (double len, double hgt)
: length (len), height (hgt)
{
    count++;
}
// Definition of default constructor
Rectangle :: Rectangle ()
: length (0.0), height (0.0)
{
    count++;
}
// Definition of copy constructor
Rectangle :: Rectangle (const Rectangle& rect)
: length (rect.length), height (rect.height)
{
    count++;
}
// Definition of destructor
Rectangle :: ~Rectangle ()
{
    count--;
}
/************************************************************
 * Definitions of the static member function
 ************************************************************/
int Rectangle :: getCount ()
{
    return count;
}

/************************************************************
 * Application to create and count Rectangle objects        *
 ************************************************************/
int main ()
{
    {
        Rectangle rect1 (3.2, 1.2);
        Rectangle rect2 (1.5, 2.1);
        Rectangle rect3;
        Rectangle rect4 (rect1);
        Rectangle rect5 (rect2);
        cout << "Count of objects: " << rect5.getCount() << endl;
    }
    cout << "Count of objects: " << Rectangle::getCount();
    return 0;
}
```

Run:

```
Count of objects: 5
Count of objects: 0
```

Declaration of the static member is done in line 14 using the keyword *static*. Initialization of this member is done in line 23 outside the class. The definition of the function is done in lines 53–56. We have added a nested block (lines 63–70) in the *main* function to create a scope in which the objects are created. This means that outside this block, there is no instance, but we can check the value of the static data member using the class name. We create five instances before we go out of the block; we check the value of the static data member through the last object and find it to be 5. After we go out of the block, all the instances are destroyed and we can check the value of the static data member through the class name to see that it is 0.

**EXAMPLE 7.5**

In this example we design a class that represents a checking account. The only two instance data members we designed for this class are the *account number* and *balance*. Although the balance can be initialized by the user of the class during creation of an instance, the account number cannot be entered by the user because it must be unique. To prevent duplication of the account number, we have used a static data member, called *base*, that is initialized to 0 and incremented with the opening of each new account. We add 100000 to this static data member to make it a large number as is customary. We do not need a static member function because we are not checking the value of the static data member. Program 7.6 shows this class and its application.

**Program 7.6** An example of a bank account

```cpp
/********************************************************
 * A program to declare, define, and use a bank account class       *
 ********************************************************/
#include <iostream>
#include <cassert>
using namespace std;

/********************************************************
 * Class Definition (Declaration of all members)                  *
 ********************************************************/
class Account
{
    private:
        long accNumber;
        double balance;
```
