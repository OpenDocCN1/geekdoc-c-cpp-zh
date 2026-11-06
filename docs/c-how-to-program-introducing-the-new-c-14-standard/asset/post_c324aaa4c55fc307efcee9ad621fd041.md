
```cpp
// Fig. 9.23: Fig09_23.cpp
// Friends can access private members of a class.
#include <iostream>
using namespace std;

// Count class definition
class Count {
    friend void setX(Count&, int); // friend declaration
public:
    int getX() const {return x;}
private:
    int x{0};
};

// function setX can modify private data of Count
// because setX is declared as a friend of Count (line 8)
void setX(Count& c, int val) {
    c.x = val; // allowed because setX is a friend of Count
}

int main() {
    Count counter; // create Count object

    cout << "counter.x after instantiation: " << counter.getX() << endl;
    setX(counter, 8); // set x using a friend function
    cout << "counter.x after call to setX friend function: "
        << counter.getX() << endl;
}
```

```text
counter.x after instantiation: 0
counter.x after call to setX friend function: 8
```

Fig. 9.23 **Friends** can access **private** members of a class.

Function `setX` (lines 17–19) is a standalone (global) function—it isn’t a member function of class `Count`. For this reason, when `setX` is called for object `counter`, line 25 passes `counter` as an argument to `setX` rather than using a handle (such as the name of the object) to call the function, as in

```cpp
counter.setX(8); // error: setX not a member function
```

Function `setX` is allowed to access class `Count`’s `private` data member `x` (line 18) only because `setX` was declared as a `friend` of the class (line 8). If you remove the `friend` declaration in line 8, you’ll receive error messages indicating that function `setX` cannot modify class `Count`’s `private` data member `x`.

### Overloaded `friend` Functions

It’s possible to specify overloaded functions as `friend`s of a class. Each function intended to be a `friend` must be explicitly declared in the class definition as a `friend` of the class.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1239_0.png)

### Software Engineering Observation 9.10

*Even though the prototypes for `friend` functions appear in the class definition, friends are not member functions.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1239_1.png)

### Software Engineering Observation 9.11

*Member access notions of `private`, `protected` and `public` are not relevant to `friend` declarations, so `friend` declarations can be placed anywhere in a class definition.*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1240_0.png)

### Good Programming Practice 9.3

*Place all friendship declarations first inside the class definition’s body and do not precede them with any access specifier.*

## 9.14 Using the `this` Pointer

There’s only one copy of each class’s functionality, but there can be *many* objects of a class, so how do member functions know *which* object’s data members to manipulate? Every object has access to its own address through a pointer called `this` (a C++ keyword). The `this` pointer is *not* part of the object itself—i.e., the memory occupied by the `this` pointer is not reflected in the result of a `sizeof` operation on the object. Rather, the `this` pointer is passed (by the compiler) as an *implicit* argument to each of the object’s non-`static` member functions. **Section 9.15** introduces `static` class members and explains why the `this` pointer is *not implicitly* passed to `static` member functions.

### Using the `this` Pointer to Avoid Naming Collisions

Member functions use the `this` pointer *implicitly* (as we’ve done so far) or *explicitly* to reference an object’s data members and other member functions. A common *explicit* use of the `this` pointer is to avoid *naming conflicts* between a class’s data members and member-function parameters (or other local variables). If a member function contains a local variable and data member with the *same* name, as in the following `setHour` function:

```cpp
// set hour value
void Time::setHour(int hour) {
    if (hour >= 0 && hour < 24) {
        this->hour = hour; // use this-> to access data member
    }
    else {
        throw invalid_argument("hour must be 0-23");
    }
}
```

the local variable is said to *hide* or *shadow* the data member—using just the variable name in the member function’s body refers to the *local variable* rather than the data member. However, you can access the data member `hour` by qualifying its name with `this->`. So the following statement assigns the `hour` parameter’s value to the *data member* `hour`:

```cpp
this->hour = hour; // use this-> to access data member
```

A widely accepted practice to minimize the proliferation of identifier names is to use the same name for a set function’s parameter and the data member it sets, and to reference the data member in the set function’s body via `this->`.

### *Type of the `this` Pointer*

The type of the `this` pointer depends on the type of the object and whether the member function in which `this` is used is declared `const`:

- In a non-`const` member function of class `Employee`, the `this` pointer has the type `Employee* const`—a constant pointer to a *nonconstant* `Employee`.
- In a `const` member function, `this` has the type `const Employee* const`—a constant pointer to a *constant* `Employee`.

### 9.14.1 Implicitly and Explicitly Using the `this` Pointer to Access an Object’s Data Members

**Figure 9.24** demonstrates the implicit and explicit use of the `this` pointer to enable a member function of class `Test` to print the `private` data `x` of a `Test` object. In the next example and in **Chapter 10**, we show some substantial and subtle examples of using `this`.

```cpp
// Fig. 9.24: fig09_24.cpp
// Using the this pointer to refer to object members.
#include <iostream>
using namespace std;

class Test {
public:
    explicit Test(int);
    void print() const;
private:
    int x{0};
};

// constructor
Test::Test(int value) : x{value} {} // initialize x to value

// print x using implicit then explicit this pointers;
// the parentheses around *this are required
void Test::print() const {
    // implicitly use the this pointer to access the member x
    cout << "x = " << x;

    // explicitly use the this pointer and the arrow operator
    // to access the member x
    cout << "\n this->x = " << this->x;

    // explicitly use the dereferenced this pointer and
    // the dot operator to access the member x
    cout << "\n(*this).x = " << (*this).x << endl;
}

int main() {
    Test testObject{12}; // instantiate and initialize testObject
    testObject.print();
}
```

```text
x = 12
this->x = 12
(*this).x = 12
```

**Fig. 9.24** Using the `this` pointer to refer to object members.

For illustration purposes, member function `print` (lines 19–30) first prints `x` by using the `this` pointer *implicitly* (line 21)—only the name of the data member is specified. Then `print` uses two different notations to access `x` through the `this` pointer—the arrow operator (`->`) off the `this` pointer (line 25) and the dot operator (`.`) off the *dereferenced* `this` pointer (line 29). Note the parentheses around `*this` (line 29) when used with the dot member-selection operator (`.`). The parentheses are required because the dot operator has higher precedence than the `*` operator. Without the parentheses, the expression `*this.x` would be evaluated as if it were parenthesized as `*(this.x)`, which is a *compilation error*, because the dot operator cannot be used with a pointer.

One interesting use of the `this` pointer is to prevent an object from being assigned to itself. As we’ll see in **Chapter 10**, *self-assignment* can cause serious errors when the object contains pointers to dynamically allocated storage.

### 9.14.2 Using the `this` Pointer to Enable Cascaded Function Calls

Another use of the `this` pointer is to enable **cascaded member-function calls**—that is, invoking multiple functions sequentially in the same statement (as in line 10 of **Fig. 9.27**). The program of **Figs. 9.25–9.27** modifies class `Time`’s *set* functions `setTime`, `setHour`, `setMinute` and `setSecond` such that each returns a reference to the `Time` object on which it’s called to enable cascaded member-function calls. Notice in **Fig. 9.26** that the last statement in the body of each of these member functions returns `*this` (lines 21, 33, 45 and 57) into a return type of `Time&`.
