
```cpp
// the following scope creates and destroys
// Employee objects before main terminates
{
    Employee e1( "Susan", "Baker" );
    Employee e2( "Robert", "Jones" );

    // two objects exist; call static member function getCount again
    // using the class name and the scope resolution operator
    cout << "\nNumber of employees after objects are instantiated is "
         << Employee::getCount();

    cout << "\n\nEmployee 1: "
         << e1.getFirstName() << " " << e1.getLastName()
         << "\nEmployee 2: "
         << e2.getFirstName() << " " << e2.getLastName() << "\n\n";
} // end nested scope in main

// no objects exist, so call static member function getCount again
// using the class name and the scope resolution operator
cout << "\nNumber of employees after objects are deleted is "
     << Employee::getCount() << endl;
} // end main
```

```text
Number of employees before instantiation of any objects is 0
Employee constructor for Susan Baker called.
Employee constructor for Robert Jones called.
Number of employees after objects are instantiated is 2

Employee 1: Susan Baker
Employee 2: Robert Jones
~Employee() called for Robert Jones
~Employee() called for Susan Baker

Number of employees after objects are deleted is 0
```

*Fig. 9.29* | static data member tracking the number of objects of a class. (Part 2 of 2.)

A member function should be declared `static` if it does not access non-static data members or non-static member functions of the class. Unlike non-static member functions, a static member function does not have a *this* pointer, because static data members and static member functions exist independently of any objects of a class. The *this* pointer must refer to a specific object of the class, and when a static member function is called, there might not be any objects of its class in memory.

![](img/b42ba5cd262b1358d16610173f975e4d_457_0.png)

> **Common Programming Error 9.6**
>
> Using the *this* pointer in a static member function is a compilation error.

![](img/b42ba5cd262b1358d16610173f975e4d_457_1.png)

> **Common Programming Error 9.7**
>
> Declaring a static member function `const` is a compilation error. The const qualifier indicates that a function cannot modify the contents of the object on which it operates, but static member functions exist and operate independently of any objects of the class.

## 9.15 Wrap-Up

This chapter deepened our coverage of classes, using a Time class case study to introduce several new features. We used an include guard to prevent the code in a header (.h) file from being included multiple times in the same source code (.cpp) file. You learned how to use the arrow operator to access an object’s members via a pointer of the object’s class type. You learned that member functions have class scope—the member function’s name is known only to the class’s other members unless referred to by a client of the class via an object name, a reference to an object of the class, a pointer to an object of the class or the scope resolution operator. We also discussed access functions (commonly used to retrieve the values of data members or to test the truth or falsity of conditions) and utility functions (private member functions that support the operation of the class’s public member functions).

You learned that a constructor can specify default arguments that enable it to be called in a variety of ways. You also learned that any constructor that can be called with no arguments is a default constructor and that there can be at most one default constructor per class. We discussed destructors for performing termination housekeeping on an object of a class before that object is destroyed, and demonstrated the order in which an object’s constructors and destructors are called.

We demonstrated the problems that can occur when a member function returns a reference or a pointer to a private data member, which breaks the encapsulation of the class. We also showed that objects of the same type can be assigned to one another using default memberwise assignment—in Chapter 10, we’ll discuss how this can cause problems when an object contains pointer members.

You learned how to specify const objects and const member functions to prevent modifications to objects, thus enforcing the principle of least privilege. You also learned that, through composition, a class can have objects of other classes as members. We demonstrated how to use friend functions.

You learned that the this pointer is passed as an implicit argument to each of a class’s non-static member functions, allowing them to access the correct object’s data members and other non-static member functions. We used the this pointer explicitly to access the class’s members and to enable cascaded member-function calls. We motivated the notion of static data members and member functions and demonstrated how to declare and use them in your own classes.

In Chapter 10, we continue our study of classes and objects by showing how to enable C++’s operators to work with class-type objects—a process called operator overloading. For example, you’ll see how to overload the << operator so it can be used to output a complete array without explicitly using a repetition statement.

## Summary

### Section 9.2 Time Class Case Study

- Preprocessing directives `#ifndef` (which means “if not defined”; p. 380) and `#endif` (p. 380) are used to prevent multiple inclusions of a header. If the code between these directives has not previously been included in an application, `#define` (p. 380) defines a name that can be used to prevent future inclusions, and the code is included in the source code file.
- Before C++11, only `static const int` data members could be initialized where they were declared in the class body. For this reason, data members typically should be initialized by the class’s constructor.

### Section 9.6 Destructors

- A destructor receives no parameters and returns no value. A class may have only one destructor.
- If you do not explicitly provide a destructor, the compiler creates an “empty” destructor, so every class has exactly one destructor.

### Section 9.7 When Constructors and Destructors Are Called

- The order in which constructors and destructors are called depends on the order in which execution enters and leaves the scopes where the objects are instantiated.
- Generally, destructor calls are made in the reverse order of the corresponding constructor calls, but the storage classes of objects can alter the order in which destructors are called.

### Section 9.8 Time Class Case Study: A Subtle Trap—Returning a Reference or a Pointer to a Private Data Member

- A reference to an object is an alias for the name of the object and, hence, may be used on the left side of an assignment statement. In this context, the reference makes a perfectly acceptable *lvalue* that can receive a value.
- If the function returns a reference to const data, then the reference cannot be used as a modifiable *lvalue*.

### Section 9.9 Default Memberwise Assignment

- The assignment operator (=) can be used to assign an object to another object of the same type. By default, such assignment is performed by memberwise assignment (p. 400).
- Objects may be passed by value to or returned by value from functions. C++ creates a new object and uses a copy constructor (p. 401) to copy the original object's values into the new object.
- For each class, the compiler provides a default copy constructor that copies each member of the original object into the corresponding member of the new object.

### Section 9.10 const Objects and const Member Functions

- The keyword const can be used to specify that an object is not modifiable and that any attempt to modify the object should result in a compilation error.
- C++ compilers disallow non-const member function calls on const objects.
- An attempt by a const member function to modify an object of its class is a compilation error.
- A member function is specified as const both in its prototype and in its definition.
- A const object must be initialized.
- Constructors and destructors cannot be declared const.

### Section 9.11 Composition: Objects as Members of Classes

- A class can have objects of other classes as members—this concept is called composition.
- Member objects are constructed in the order in which they're declared in the class definition and before their enclosing class objects are constructed.
- If a member initializer is not provided for a member object, the member object's default constructor (p. 404) will be called implicitly.

### Section 9.12 friend Functions and friend Classes

- A friend function (p. 410) of a class is defined outside that class’s scope, yet has the right to access all of the class’s members. Stand-alone functions or entire classes may be declared to be friends.
- A friend declaration can appear anywhere in the class.
- The friendship relation is neither symmetric nor transitive.
