
## **Program 7.3** Defining and creating three random numbers (Continued)

```cpp
value = temp % (high - low + 1) + low;
}

// Destructor
RandomInteger::~RandomInteger()
{
}

// Accessor member function
void RandomInteger::print() const
{
    cout << value << endl;
}

/********************************************************
 * Application to instantiate random number objects and print
 * the value of the random number
 ********************************************************/
int main()
{
    // Generating a random integer between 100 and 200
    RandomInteger r1(100, 200);
    cout << "Random number between 100 and 200: ";
    r1.print();

    // Generating a random integer between 400 and 600
    RandomInteger r2(400, 600);
    cout << "Random number between 400 and 600: ";
    r2.print();

    // Generating a random integer between 1500 and 2000
    RandomInteger r3(1500, 2000);
    cout << "Random number between 1500 and 2000: ";
    r3.print();

    return 0;
}
```

```text
Run:
Random number between 100 and 200: 130
Random number between 400 and 600: 570
Random number between 1500 and 2000: 1720
```

There are four points we must mention about this program.

- This is an example in which we do not need a default constructor because creation of a random number with literal values does not make sense. Since we have defined a parameter constructor, the system does not create a default constructor in this case, which is what we want.
- We do not need a copy constructor for this class (it does not make sense to create the same random number), but we cannot stop the system from defining a synthesized one. In this case, the new C++11 standard comes to the rescue. It allows us to declare a copy constructor and set it to the keyword *delete*, which prevents the system from providing a synthesized copy constructor (see the class definition, line 25).
- Although we have three data members, only two of them (*low* and *high*) are initialized in the initialization list of the constructor. The third data member (*value*) is calculated in the body of the constructor. The calculation is too complex to be done in the initializer list. The only accessor member function is the *print* function, which prints the value of the created random number.
- Finally, we have no mutator member functions because we do not want to change the created random number.

## 7.4 INSTANCE MEMBERS

In the previous three sections, we learned how to define classes, how to instantiate objects from classes, and how to apply member functions on the data members of objects. In this section and the next, we learn more about these members and the interaction among members in the background: doing so will help us design better classes. When we design a class, we can have two groups of members: *instance members* and *class members*.

### 7.4.1 Instance Data Members

An **instance data member** defines the attributes of an instance, which means that each object must *encapsulate* the set of data members defined in the class. These data members belong exclusively to the corresponding instance and cannot be accessed by other instances. The term *encapsulation* here means that separate regions of memory are assigned for each object and each region stores possibly different values for each data member. Figure 7.9 shows the concept of encapsulation.

#### Access Modifier for Instance Data Member

Although an instance data member can have a *private* or a *public* access modifier, it makes more sense for instance data members to be private. If we make the data members of an instance member public, they can be directly accessed by the application without calling an instance member function. That is not the goal of object-oriented programming. In object-oriented programming we want the objects to apply their behaviors on their attributes. In other words, we must make the instance data members private so that they can be accessed only through instance member functions.

> **The instance data members of a class are normally private and can be accessed only through instance member functions.**

![](img/d68f6199646ca63591a6d8419e0ed4ba_312_0.png)

![](img/d68f6199646ca63591a6d8419e0ed4ba_313_0.png)

**Figure 7.10** A class with two data members and four member functions

### 7.4.2 Instance Member Functions

An **instance member function** defines one of the behaviors that can be applied on the instance data members of an object. Although each object has its own instance data members, there is only one copy of each instance member function in memory and it must be shared by all instances. Figure 7.10 shows the case of a class with two instance data members and four instance member functions.

Since we have created three objects from this class, we have three pairs of instance data members and four instance member functions; each member function is shared among the objects (one object at a time).

#### Access Modifier for Instance Member Functions

Unlike instance data members, the access modifier for an instance member function is normally public and allows access from outside the class (the application) unless the instance member function is supposed to be used only by other instance member functions within the class.

> The instance member function of a class must be public so it can be accessed from outside the class.

#### Instance Member Function Selectors

An application (for example, the *main* function) can call an instance member function to operate on an instance. In object-oriented programming, this call must be done through the instance. The application must first construct an instance and then let the instance call the instance member function. In other words, it looks like the instance is operating on itself. The C++ language defines two operators, called **member selector operators**, for this purpose. They are defined in Appendix C as part of the postfix expression and repeated in Table 7.4 for quick reference.

**Table 7.4 — Member selector operators**

| Group | Name | Operator | Expression | Prec | Assoc |
|---|---|---|---|---:|:---:|
| Postfix | member selector | `.` | object.member | 18 | → |
|  | member selector | `->` | pointer -> member | 18 | → |

![](img/d68f6199646ca63591a6d8419e0ed4ba_314_0.png)

**Figure 7.11** Use of member select operator to apply an operation on an instance

Figure 7.11 shows how the first *member select operator* can be used to select a member function given the name of the object. We discuss the use of the second one shortly when we discuss locking and unlocking an instance.

We used the dot member select operator in Program 7.2 and Program 7.3 to let the objects call their member functions.

#### Locking and Unlocking

If there is only one copy of a member function, how can that function be used by one object at a time and by another object at another time? The more important question is, When a function is being used by one object, how can we prevent other objects from using it? In other words, how can we *lock* a function when it is being used and *unlock* it when the function is terminated (returned) so that it can be used by another object later?

The answer is that locking and unlocking are done in the background. C++ adds a pointer (a variable that holds the address of an object) to each member function. So while we use the dot member selector depicted in Figure 7.11, the compiler changes it to a pointer member selector depicted in Figure 7.12, in which each member function has a hidden pointer named **this pointer**. The function is employed by the object to which the *this pointer* is pointing at the time. In other words, the function code is applied to the data members of the object pointed to by the *this pointer*.

![](img/d68f6199646ca63591a6d8419e0ed4ba_314_1.png)

**Figure 7.12** Locking and unlocking a function to a particular object

Figure 7.12 shows one member function that is used by different objects at different times. The function is the same, but the object being operated on is different at different times. Since each function has only one `this` pointer and we can call only one function at a time, we should be convinced that locking and unlocking are done properly.

**Hidden Parameter** How does an instance member function get a *this* pointer? It is added as a parameter to the instance member function by the compiler as shown below:

```cpp
// Written by the user
double getRadius() const
{
    return radius;
}
```

```cpp
// Changed by the compiler
double getRadius(Circle* this) const
{
    return (this->radius);
}
```

The operator (->) is a special operator that is the combination of the indirection operator and the member operation. In other words, we have the following relation:

| Expression | Relation | Expression |
|---|---|---|
| `this->radius` | is the same as | `(*this).radius` |

When we use the member operator to call an instance member function, the compiler changes the call statement into two statements, as shown below:

```cpp
// Written by the user
circle1.getRadius();
```

```cpp
// Changed by the system
this = &circle1;
getRadius(this);
```

#### Explicit Use of this Pointer

We can use the *this* pointer in our program to refer to a data member instead of using the data member itself, and we can use the name of the data member as a parameter. In this way, we do not have to use abbreviated names as we did in the past. The following shows coding `setRadius` for the Circle class without and with the use of the *this* pointer.

```cpp
// Without using the this pointer
void Circle::setRadius(double rds)
{
    radius = rds;
}
```

```cpp
// Using the this pointer
void Circle::setRadius(double radius)
{
    this->radius = radius;
}
```

We must remember that the *this* pointer cannot be used in the initialization list of a constructor because at that point, the host object has not been constructed; however, it can be used in the body of the constructor if needed.

#### Host Object

When an instance member function is being executed, there is always a **host object**. The host object is the object that the instance member function is operating on at a given moment. In other words, the host object is the object that is pointed to by the *this* pointer. There is only one host object during the execution of an instance member function. Figure 7.12 depicts the situations we discuss next.
