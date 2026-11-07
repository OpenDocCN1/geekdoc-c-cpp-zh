# 9.3 Class Scope and Accessing Class Members

A class’s data members (variables declared in the class definition) and member functions (functions declared in the class definition) belong to that class’s scope. Nonmember functions are defined at *global namespace scope*.

Within a class’s scope, class members are immediately accessible by all of that class’s member functions and can be referenced by name. Outside a class’s scope, public class members are referenced through one of the **handles** on an object—an object name, a reference to an object or a pointer to an object. The type of the object, reference or pointer specifies the interface (i.e., the member functions) accessible to the client. [We’ll see in Chapter 10 that an *implicit handle* is inserted by the compiler on every reference to a data member or member function from within an object.]

*Member functions of a class can be overloaded, but only by other member functions of that class.* To overload a member function, simply provide in the class definition a prototype for each version of the overloaded function, and provide a separate function definition for each version of the function. This also applies to the class’s constructors.

Variables declared in a member function have *local scope* and are known only to that function. If a member function defines a variable with the same name as a variable with class scope, the class-scope variable is *hidden* by the block-scope variable in the local scope. Such a hidden variable can be accessed by preceding the variable name with the class name followed by the scope resolution operator (`::`). Hidden global variables can be accessed with the scope resolution operator (see Chapter 6).

The dot member selection operator (`.`) is preceded by an object’s name or with a reference to an object to access the object’s members. The **arrow member selection operator (`->`)** is preceded by a pointer to an object to access the object’s members.

Figure 9.4 uses a simple class called Count (lines 7–24) with private data member x of type int (line 23), public member function setX (lines 11–14) and public member function print (lines 17–20) to illustrate accessing class members with the member-selection operators. For simplicity, we’ve included this small class in the same file as main. Lines 28–30 create three variables related to type Count—counter (a Count object), counterPtr (a pointer to a Count object) and counterRef (a reference to a Count object). Variable counterRef *refers to* counter, and variable counterPtr *points to* counter. In lines 33–34 and 37–38, note that the program invokes member functions setX and print by using the dot (`.`) member selection operator preceded by either the name of the object (counter) or a reference to the object (counterRef, which is an alias for counter). Similarly, lines 41–42 demonstrate that the program can invoke member functions setX and print by using a pointer (counterPtr) and the arrow (`->`) member-selection operator.

```
```cpp
// Fig. 9.4: fig09_04.cpp
// Demonstrating the class member access operators . and ->
#include <iostream>
using namespace std;
```
```

**Fig. 9.4** | Accessing an object’s member functions through each type of object handle—the object’s name, a reference to the object and a pointer to the object. (Part 1 of 2.)