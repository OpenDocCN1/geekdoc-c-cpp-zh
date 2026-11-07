```
```cpp
// the following scope creates and destroys
// Employee objects before main terminates
{
    Employee e1( "Susan", "Baker" );
    Employee e2( "Robert", "Jones" );

    // two objects exist; call static member function getCount again
    // using the class name and the scope resolution operator
    cout << "\\nNumber of employees after objects are instantiated is "
         << Employee::getCount();

    cout << "\\n\\nEmployee 1: "
         << e1.getFirstName() << " " << e1.getLastName()
         << "\\nEmployee 2: "
         << e2.getFirstName() << " " << e2.getLastName() << "\\n\\n";
} // end nested scope in main

// no objects exist, so call static member function getCount again
// using the class name and the scope resolution operator
cout << "\\nNumber of employees after objects are deleted is "
     << Employee::getCount() << endl;
} // end main
```
```

Number of employees before instantiation of any objects is 0
Employee constructor for Susan Baker called.
Employee constructor for Robert Jones called.
Number of employees after objects are instantiated is 2

Employee 1: Susan Baker
Employee 2: Robert Jones
~Employee() called for Robert Jones
~Employee() called for Susan Baker

Number of employees after objects are deleted is 0

*Fig. 9.29* | static data member tracking the number of objects of a class. (Part 2 of 2.)

A member function should be declared `static` if it does not access non-static data members or non-static member functions of the class. Unlike non-static member functions, a static member function does not have a *this* pointer, because static data members and static member functions exist independently of any objects of a class. The *this* pointer must refer to a specific object of the class, and when a static member function is called, there might not be any objects of its class in memory.

![](bbox=[0.128, 0.813, 0.194, 0.849])

> **Common Programming Error 9.6**
> 
> Using the *this* pointer in a static member function is a compilation error.

![](bbox=[0.128, 0.876, 0.194, 0.912])

> **Common Programming Error 9.7**
> 
> Declaring a static member function `const` is a compilation error. The const qualifier indicates that a function cannot modify the contents of the object on which it operates, but static member functions exist and operate independently of any objects of the class.