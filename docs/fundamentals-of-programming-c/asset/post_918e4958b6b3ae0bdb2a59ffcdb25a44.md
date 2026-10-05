
# 15. THE THIS POINTER 397

```cpp
return count;
}
```

In 14.3 we saw that an expression such as `ctrl.clear()` passes the address of ctrl as a secret parameter during the clear method. This is how the method determines which count field to reset--ctrl.clear() resets ctrl's count field, and ctrl2.clear() would reset ctrl2's count field.

Within a method definition you may access this secret parameter via the reserved `this`. Within a method body this expression represents a pointer to the object upon which the method was called. Also the Counter class may be expressed as

```cpp
// Uses this directly
class Counter {
    int count;
public:
    // Allow clients to reset the counter to zero
    void clear() {
        this->count = 0;
    }
    // Allow clients to increment the counter
    void inc() {
        this->count++;
    }
    // Return a copy of the counter's current value
    int get() {
        return this->count;
    }
}
```

Within a method of the Counter class, `this->count` is an alternate way of writing just `count`. Some programmers may use this pointer as to better communicate to human readers that the count variable has been a field, and it cannot be a local or global variable.

The this pointer is handy when a method parameter has the same name as a field:

```cpp
class Point {
    double x;
    double y;
private:
    void set_x(double x) {
        // Assign the parameter's value to the field
        this->x = x;
    }
    // Other details omitted . . .
};
```

In the set_x method the parameter x has the same name as field x. This is legal in C++; a method parameter or local variable of a method may have the same name as a field. The problem is that the local variable or parameter hides the access to the field. Any unqualified use of the name x refers to the parameter x, not the field x. One solution would be to name the parameter something else: perhaps _x or x_param. A strong argument can be made, that x is the best name for the field, and x is also the best name for the parameter to the set_x method. To access the field in this case, use the this pointer. Since this is a reserved word, the expression `this->x` cannot be mistaken for anything other the x field of the object which the method was invoked.

Another use of the pointer involves passing the current object to another function or method. Suppose a global function log that accepts a Counter object as shown here:

```cpp
void log(Counter c) {
    // Details omitted . .
}
```

If within the class method we use to call the log function passing the object on whose behalf the class method was, we would write

```cpp
class Counter {
    // ...
public:
    void clear() {
        count = 0;
        // Pass this object off to the log function
        log(*this);
    }
}
```

We pass the expression `*this` as the actual object to log because the log function expects an object (or object reference), not a pointer. Remember the syntax of pointers: If this is a pointer, `*this` is the object this to which this points.

Since this serves as an implicit parameter passed to methods, it is illegal to use the expression outside of the body of the method.

# 15. CONST METHODS

### 15.3 const Methods

Given the SimpleRational class in Listing 14.5 (simperational.cpp), the following code produces a compiler error:

```cpp
const SimpleRational fract(1, 2); // Constant fraction 1/2
fract.set_numerator(2); // Error, cannot change a constant
```

This behavior is desirable, since the set_numerator method can change the state of a SimpleRational object, and fract object is supposed to be const. Unfortunately, this behavior is correct. The compiler does not analyze our methods to determine exactly what they do. Consider the following code that also will not compile:

```cpp
const SimpleRational fract(1, 2); // Constant fraction 1/2
cout << fract.get_numerator(); // Error!
```

Since the get_numerator method does not modify a SimpleRational object, we would expect that invoking it on a const object should be acceptable, but the compiler rejects understand what set_numerator is supposed to do; specifically, it cannot determine that a method will not change the state of an object. The programmer must supply some additional information to help the compiler.

If a method is not supposed to change the state of an object, that method should be const. In the SimpleRational class, the methods get_numerator and get_denominator return copies of the fraction's numerator and denominator. Neither method is intended to modify any instance variables. If we look at the code for these methods, we see that indeed method changes anything about a SimpleRational object. What if the programmer make a mistake—perhaps a spurious copy and paste error—and the statement

```cpp
numerator = 0;
```

made its way into the get_numerator method? Unfortunately, the ways thing stand, the compiler cannot detect this error, and get_numerator contains a serious logic error.

We can remove the possibility of such an error by declaring get_numerator and get_denominator const

```cpp
class SimpleRational {
  public:
    /* stuff omitted ... */
    int get_numerator() const {
      return numerator;
    }
    int get_denominator() const {
      return denominator;
    }
    /* other stuff omitted ... */
}
```

The const keyword goes after the closing parenthesis of the parameter list and before the opening curly brace of the method's body. Declaring a const is not merely a defensive programming strategy. Methods declared to const can be used with const and non-const objects, but a non-const method cannot be used with const objects. For maximum flexibility, always declare a method to const unless doing so would prevent the method from doing what it is supposed to.

# 15.4 Separating Method Declarations and Definitions

It is common in larger C++ projects to separate a method implementation from its declaration. A simple example illustrates how to do this; consider the class MyClass:

```cpp
class MyClass {
public:
    void my_method() const {
        cout << "Executing\_my_method\" << endl;
    }
};
```

This version of MyClass uses what is known as an inline method definition; that is, the method my_method is defined completely with a body in the same place it is declared. Compare the inline version to the following split across two files: myclass.h and myclass.cpp. The code in myclass.h is shown in Listing 15.1 (myclass.h).

+   Listing 15.1: myclass.h

```cpp
// myclass.h
class MyClass {
public:
    void my_method() const; // Method declaration
};
```

No body for my_method appears in the declaration of the class MyClass in myclass.h; instead, the method implementation appears elsewhere, in myclass.cpp. Listing 15.2 (myclass.cpp).

+   Listing 15.2: myclass.cpp

```cpp
// myclass.cpp
// Include the class declaration
#include "myclass.h"
#include <iostream>

// Method definition
void MyClass::my_method() const {
    std::cout << "Executing\_my_method\" << endl;
}
```

Without the prefix MyClass:: the definition of my_method in myclass.cpp would be global function like the ones we have seen in Chapter 9. The class name and scope resolution operator (::) binds the definition of the method to the class to which it belongs.

The header file would be #included by all the source files that need to use MyClass objects; the myclass.cpp file would be compiled separately and linked into the rest of the project's .cpp files.
