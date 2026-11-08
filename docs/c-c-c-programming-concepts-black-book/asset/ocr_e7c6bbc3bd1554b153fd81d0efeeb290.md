The properties of the Employee class are name, salary, designation, and an associated project. These properties are static; however, the values that these properties can hold are dynamic. The behavior of an object is captured in terms of operation. The PromoteEmployee() operation changes the state of object; whereas, the GetSalary() operation does not alter the state of object.

After learning about classes and objects, let's discuss constructors, in detail.

# ## Constructors

Constructors are member functions with the same name as that of the class and are called automatically at the time of object creation. These are used to initialize the members of a class; therefore, they turn raw memory into objects. Constructors have no return type, but they can be overloaded. Consider the code snippet given in Listing 13.4:

**Listing 13.4:** Showing the Example of a Constructor

```
```cpp
class A
{
    int b, c;
    public:
    A();                      //default constructor
    A(int, int)               //overloaded constructor
};
A::A()
{
    b=10;
    c=20;
}
A::A(int k, int j)
{
    b=k;
    c=j;
}
```
```

In the class A, we have declared a default constructor as A() and the overloaded constructor as A(int, int).

Next, let's learn about the copy constructors, in detail.

# ## Copy Constructors

Copy constructor of a class is a constructor that makes the copy of an object of the class. A copy constructor helps in creating a new object from an existing one by initialization. In case we do not declare a copy constructor, the C++ compiler will implicitly declare it; however, this will be an inline public member. A declaration of type A::A(const A & right) is an example of a copy constructor.

There are certain rules that need to be kept in mind while working with both constructors and copy constructors. The set of rules are as follows:

+   1. A copy constructor can accept only one argument of reference to the same class type. However, more arguments can be supplied, but all those should be default.
+   2. An error is generated if we specify a copy constructor with the first argument as an object and not a reference.
+   3. The compiler generates a default copy constructor if it is not provided.
+   4. Constructors of base classes are not inherited by derived classes (except in cases of virtual derivation).