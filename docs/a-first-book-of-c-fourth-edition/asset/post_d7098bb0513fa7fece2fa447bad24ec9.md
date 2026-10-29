
# Program 12.2

```
#include <iostream>
#include <cmath>
using namespace std;

// class declaration section for the base class
class One
{
    protected:
        double a;
    public:
        One(double = 2.0);  // constructor
        double f1(double);  // a member function
        double f2(double);  // another member function
};

// class implementation section for One
One::One(double val)  // constructor
{
    a = val;
}

double One::f1(double num)  // a member function
{
    return(num/2);
}

double One::f2(double num)  // another member function
{
    return( pow(f1(num),2) );  // square the result of f1()
}

// class declaration section for the derived class
class Two : public One
{
    public:
        double f1(double);  // this overrides class One's f1()
};

// class implementation section for Two
double Two::f1(double num)
{
    return(num/3);
}
```

```
int main()
{
    One object_1;  // object_1 is an object of the base class
    Two object_2;  // object_2 is an object of the derived class

    // call f2() using a base class object call
    cout << "The computed value using a base class object call is "
         << object_1.f2(12) << endl;

    // call f2() using a derived class object call
    cout << "The computed value using a derived class object call is "
         << object_2.f2(12) << endl;

    return 0;
}
```

The following output is produced by Program 12.2:

The computed value using a base class object call is 36
The computed value using a derived class object call is 36

As this output shows, the same result is obtained, no matter which object type calls the f2() function, because the derived class doesn't have an override of the base class's f2() function. Therefore, both calls to f2() result in the base class's f2() function being called.

After the base class's f2() function is called, it always calls the base class's version of f1() rather than the derived class's override version. This behavior is caused by a process referred to as function binding. In normal function calls, static binding is used, meaning the determination of which function is called is made at compile time. Therefore, when the compiler first encounters the f1() function in the base class, it makes the determination that whenever f2() is called, from either a base or derived class object, it subsequently calls the base class's f1() function.

In place of static binding, say you want to use a binding method capable of determining which function should be called at runtime, based on the object type making the call. This type of binding, referred to as dynamic binding, is achieved in C++ with virtual functions. A virtual function tells the compiler to create a pointer to a function, but not fill in the pointer's value until the function is actually called. Then at runtime, based on the object making the call, the appropriate function address is used.

Creating a virtual function is easy—simply place the keyword virtual before the function's return type in the class declaration section. For example, examine Program 12.3, which is identical to Program 12.2, except for the virtual declaration of the f1() function.

# Program 12.3

```
#include <iostream>
#include <cmath>
using namespace std;

// class declaration section for the base class
class One
{
    protected:
        double a;
    public:
        One(double = 2.0);          // constructor
        virtual double f1(double);  // a member function
        double f2(double);           // another member function
};

// class implementation section for One
One::One(double val)   // constructor
{
    a = val;
}

double One::f1(double num)   // a member function
{
    return(num/2);
}

double One::f2(double num)   // another member function
{
    return( pow(f1(num),2) );  // square the result of f1()
}

// class declaration section for the derived class
class Two : public One
{
    public:
        virtual double f1(double);    // overrides class One's f1()
};

// class implementation section for Two
double Two::f1(double num)
{
    return(num/3);
}
```

```
int main()
{
    One object_1;  // object_1 is an object of the base class
    Two object_2;  // object_2 is an object of the derived class

    // call f2() using a base class object call
    cout << "The computed value using a base class object call is "
         << object_1.f2(12) << endl;

    // call f2() using a derived class object call
    cout << "The computed value using a derived class object call is "
         << object_2.f2(12) << endl;

    return 0;
}
```

Program 12.3 produces the following output:

The computed value using a base class object call is 36

The computed value using a derived class object call is 16

As this output shows, the f2() function now calls different versions of the overloaded f1() function based on the object type making the call. Basing the selection on the object making the call is the classic definition of polymorphic behavior and is caused by the dynamic binding imposed on f1() because it's a virtual function.

After a function is declared as virtual, it remains virtual for the next derived class, with or without a virtual declaration in the derived class. Therefore, the second virtual declaration in the derived class isn't strictly necessary but should be included for clarity and to make sure any subsequently derived classes inherit the function correctly.

In the inheritance diagram in Figure 12.5, class C is derived from class B and class B is derived from class A.¹ In this situation, if the f1() function is virtual in class A but not declared in class B, it isn't virtual in class C. The only other requirement is that after a function has been declared as virtual, the return type and parameter list of all subsequent derived class override versions must be the same.

![](img/202cface8244f523c2641baa2e00d7dd_570_0.png)

# Figure 12.5 An inheritance diagram

![](img/202cface8244f523c2641baa2e00d7dd_571_0.png)

# EXERCISES 12.2

- 1. **(Practice)** Enter and run Programs 12.2 and 12.3 so that you understand the relationship between function calls in each program.
- 2. **(Review)** Describe the difference between static binding and dynamic binding.
- 3. **(Review)** Describe the difference between a virtual function and a nonvirtual function.
- 4. **(Review)** Explain what polymorphism is and give an example of polymorphic behavior.
- 5. **(Review)** Describe the two methods C++ provides for implementing polymorphism.
- 6. **(Review)** Explain whether the multiplication operator provided for integer and double-precision built-in types is an example of overloading or polymorphism.

# 12.3 Dynamic Object Creation and Deletion

As each object is defined in a program, the compiler designates enough storage for it; this storage is subsequently assigned from a pool of computer memory locations before the program runs. After memory locations have been assigned, they remain fixed for the object’s lifetime or until the program finishes running. For example, if a `main()` function declares three Date objects, the storage for these objects remains fixed from the point of their definition until `main()` completes execution.

An alternative to this fixed allocation of memory storage locations is **dynamic allocation** of memory, in which the amount of storage to be allocated is assigned, as requested, at runtime instead of being fixed at compile time. Dynamic allocation of memory is useful when dealing with lists and objects because it allows expanding the list as new items are added and contracting the list as items are deleted. For object-oriented programs, it allows creating and destroying new objects as required.

As an example of dynamic object creation, say you’re creating a program designed to track the flow of customers at a large outlet chain’s self-checkout registers. You don’t know in advance the number of transactions taking place at each register. However, by using dynamic allocation, the program can create an object as each checkout transaction occurs for tracking customer use of the checkout process. This object might consist of the number of items checked out and the arrival time of each customer at the register. Although the class’s do-nothing methods are completed later, the following class adequately defines the information this object needs. In reviewing this class, notice the shaded constructor and destructor methods:

```
// class declaration section
class Checkout
{
  private:
    int numItems;
    double arrivalTime;
```

![](img/202cface8244f523c2641baa2e00d7dd_571_1.png)
