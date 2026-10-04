
# Chapter 11 Polymorphism 657

Program 11.16 produces the following output:

```
The computed value using a base class object call is 36
The computed value using a derived class object call is 16
```

As this output shows, the f2() function now calls different versions of the overloaded f1() function on the object type making the call. Basing on the object making the call is the classic definition of polymorphic behavior and is caused by the dynamic binding based on f1() it's a virtual function.

After a function is declared virtual, it remains virtual for the next derived class, or without a virtual declaration in the derived class. Therefore, the second declaration in the derived class isn't strictly necessary but should be included for clarity and make any derived classes inherit the functionality.

In the inheritance diagram of figure 11.10, class C is derived from B and class B is derived from A. In this situation, if f1() is virtual in A but not declared in B, it isn't virtual in C. The only requirement is that after a function has been declared as virtual, the return type and parameter list of all subsequent derived class must be the same.

![](img/e2a84fc7bc04aa2e669ad865e0c2b0f76.png)
Figure 11.10 An inheritance diagram

## 11.7 EXISES

- 1. Enter and execute Programs 11.15 and 11.16 so that you understand the relationship between function calls.
- 2. (For Review) Describe the difference between static binding and dynamic binding.
- 3. (For Review) Describe the difference between a virtual function and a nonvirtual function.
- 4. (For Review) Explain what polymorphism is and provide an example.
- 5. (For Review) Describe the two methods C++ provides for implementing polymorphism.
- 6. (For Review) Explain whether overloading operators for integer and double-precision types is an example of polymorphism.

## 11.8 Common Errors

- 1. Using a user-defined assignment operator in multiple assignment when the operator hasn't been defined to return an object.
- 2. Using the static keyword when defining a static data member or member function. The static keyword should be used only in the class declaration.
- 3. Using the friend keyword when defining a friend function. The friend keyword should be used only in the class declaration.
- 4. Failing to instantiate static data members before creating objects that must access these members.
- 5. Attempting to redefine an operator meaning as it applies to C++ built-in types.
- 6. Redefining an overloaded operator to perform a function not indicated by its conventional meaning. Although this method works, it's an example of bad programming.
- 7. Attempting to make a conversion operator rather than a member function.
- 8. Attempting to specify a return type for conversion operator function.
- 9. Attempting to override a virtual function without the same type and number of arguments as the original function.
- 10. Using the virtual keyword in the class implementation section.

## 11.9 Chapter Summary

- 1. An assignment operator can be declared for a class with this function prototype: `void operator=(const className& name);` The argument is a reference to the class. The return type of void precludes multiple assignment expressions, such as a = b = c.
- 2. A type of initialization that closely resembles assignment occurs in C++ when one object is initialized by another object of the same class. This type of initialization is a copy constructor and has this function prototype: `className(const className& name);` It's often replaced with the notation `X(X)`.
- 3. Each class has an associated scope defined by the brace {}, containing the class declaration. Data members are local to their scope and can be used only by objects. If a variable name is reused in a class, the global variable is hidden by the resolution operator ::.
- 4. For each class object, a separate set of memory locations is reserved for data members, except those declared as static. Static data member is shared by all class objects and provides a means of communication between objects. Static members must be declared in the class declaration and are defined outside the section.
- 5. Static functions apply to the class rather than to separate objects. Therefore, a static function can access only static data members and other static members. Any static member must be declared in the class declaration and are defined outside the section.
- 6. A nonmember function can access a class's private data members if it's granted friend status by the class. This is done by declaring the function as friend in the class declaration section. Therefore, the class loses status on itself.
- 7. User-defined operators can be constructed for classes using operator functions. For example, the function has the form `operator symbols`, where `symbols` is one of the following:
```
[] -> delete --+ / +
<< <= >= != && ^ |
-* &= |=
```
For example, the function prototype `operator+(int)` declares that the addition operator is defined to accept an integer and return a Date object.
- 8. User-defined operators can be called in one of two ways—as a conventional function with arguments or as an operator function. For example, for an operator function having the header `Date::operator+(int)`, if dt is an object of type Date, the following two calls produce the same effect: `dt.operator+(int);`
- 9. Operator functions can also be written as friend functions. The friend version of an operator function always contains an additional reference that isn't required by the member function.
- 10. There are four categories of data type conversions:
    - Built-in types to built-in types
    - Built-in types to class types
    - Class types to built-in types
    - Class types to class types
Built-in to built-in type conversions are done by using C++'s implicit conversion rules or its explicit cast operator. Built-in to class type conversions are done using conversion constructors. From class types to built-in types or from class types to types are done by using conversion operator functions.
- 11. A type conversion constructor is a constructor whose first argument is not a member of its class and remaining arguments, if any, have default values.

## 11.0 Class Functions and Conversions

- 12. A conversion operator function is a member operator function having the name of a class. It has no explicit arguments or return type; rather, the return type is the name of the function.
- 13. Inheritance is the capability of deriving one class from another class. The initial class used as the basis for the derived class is referred to as the base, parent, superclass. The derived class is also referred to as the child class or subclass.
- 14. Base class functions can be overridden by derived class functions with the same name. The override function is simply an overloaded version of the base member function defined in the derived class.
- 15. Polymorphism is the capability of having the same function name invoke different responses, based on the object making the function call. It can be accomplished with override functions or virtual functions.
- 16. In static binding, the determination of which function is called is made at compile time. In dynamic binding, the determination is made at runtime.
- 17. A virtual function designates that dynamic binding should take place. The specification is made in the function's prototype by placing the keyword virtual before the function's return type. After a function has been declared as virtual, it remains for all derived classes, as long as there is a continuous trail of function declarations through the derived chain of classes.

## Programming Projects for Chapter 1

- a. (General Math) Construct a class Cartesian containing double-precision members x and y to store the x and y values of a point in rectangular coordinates. The member functions should include a constructor that initializes an object's x and y values to 0 and functions to display an object's x and y values. Additionally, an assignment function performs a member-assignment between two Cartesian objects.
- b. Include the class for Exercise Ia in a working C++ program that creates and displays the values of two Cartesian objects; the second object is assigned the values of the first one.
- 2. (General Math) Construct a class Fractions containing two integer members named num and denom to store the numerator and denominator of a fraction having the form num/denom. Your class should include a default constructor for adding, subtracting, multiplying, and dividing the fractions, as follows:

```
Addition: a/b + c/d = (a * d + b * c) / (b * d)
Subtraction: a/b - c/d = (a * d - b * c) / (b * d)
Multiplication: a/b * c/d = (a * c) / (b * d)
Division: (a/b) / (c/d) = (a * d) / (b * c)
```
Finally, your class should have a member function that reduces each fraction to its terms (refer to Exercise 15 in Programming Projects for Chapter 6 how to do this) as well as input and output functions for entering and displaying a fraction.
