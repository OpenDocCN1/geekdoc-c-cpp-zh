

```cpp
public:
    // constructor
    Count()
        : x(0) // initialize x to 0
    {
        // empty body
    } // end constructor Count

    // output x
    void print() const
    {
        cout << x << endl;
    } // end function print
private:
    int x; // data member
}; // end class Count

// function setX can modify private data of Count
// because setX is declared as a friend of Count (line 9)
void setX( Count &c, int val )
{
    c.x = val; // allowed because setX is a friend of Count
} // end function setX

int main()
{
    Count counter; // create Count object

    cout << "counter.x after instantiation: ";
    counter.print();

    setX( counter, 8 ); // set x using a friend function
    cout << "counter.x after call to setX friend function: ";
    counter.print();
} // end main
```

```text
counter.x after instantiation: 0
counter.x after call to setX friend function: 8
```

**Fig. 9.22 |** Friends can access private members of a class. (Part 2 of 2.)

As we mentioned, Fig. 9.22 is a mechanical example of using the friend construct. It would normally be appropriate to define function setX as a member function of class Count. It would also normally be appropriate to separate the program of Fig. 9.22 into three files:

- 1. A header (e.g., `Count.h`) containing the Count class definition, which in turn contains the prototype of friend function setX
- 2. An implementation file (e.g., `Count.cpp`) containing the definitions of class Count’s member functions and the definition of friend function setX
- 3. A test program (e.g., `fig09_22.cpp`) with `main`.

## Overloaded friend Functions

It’s possible to specify overloaded functions as friends of a class. Each function intended to be a friend must be explicitly declared in the class definition as a friend of the class.

![](img/b42ba5cd262b1358d16610173f975e4d_447_0.png)

> **Software Engineering Observation 9.12**
> 
> Even though the prototypes for friend functions appear in the class definition, friends are not member functions.

![](img/b42ba5cd262b1358d16610173f975e4d_447_1.png)

> **Software Engineering Observation 9.13**
> 
> Member access notions of private, protected and public are not relevant to friend declarations, so friend declarations can be placed anywhere in a class definition.

![](img/b42ba5cd262b1358d16610173f975e4d_447_2.png)

> **Good Programming Practice 9.4**
> 
> Place all friendship declarations first inside the class definition’s body and do not precede them with any access specifier.

## 9.13 Using the this Pointer

We’ve seen that a member function can manipulate the object’s data. There can be many objects of a class, so how do member functions know which object’s data members to manipulate? Every object has access to its own address through a pointer called this (a C++ keyword). The this pointer is not part of the object itself—i.e., the memory occupied by the this pointer is not reflected in the result of a sizeof operation on the object. Rather, the this pointer is passed (by the compiler) as an implicit argument to each of the object’s non-static member functions. Section 9.14 introduces static class members and explains why the this pointer is not implicitly passed to static member functions.

### Using the this Pointer to Avoid Naming Collisions

Member functions use the this pointer implicitly (as we’ve done so far) or explicitly to reference an object’s data members and other member functions. A common explicit use of the this pointer is to avoid naming conflicts between a class’s data members and member-function parameters (or other local variables). Consider the Time class’s hour data member and setHour member function in Figs. 9.4–9.5. We could have defined setHour as:

```cpp
// set hour value
void Time::setHour( int hour )
{
    if ( hour >= 0 && hour < 24 )
        this->hour = hour; // use this pointer to access data member
    else
        throw invalid_argument( "hour must be 0-23" );
} // end function setHour
```

In this function definition, setHour’s parameter has the same name as the data member hour. In setHour’s scope, the parameter hour hides the data member. However, you can still access the data member hour by qualifying its name with this->. The following statement assigns the hour parameter’s value to the data member hour

```cpp
this->hour = hour; // use this pointer to access data member
```

> **Error-Prevention Tip 9.4**
> 
> To make your code clearer and more maintainable, and to avoid errors, never hide data members with local variable names.

### Type of the `this` Pointer

The type of the `this` pointer depends on the type of the object and whether the member function in which `this` is used is declared const. For example, in a non-const member function of class Employee, the `this` pointer has the type `Employee *`. In a const member function, the `this` pointer has the type `const Employee *`.

### Implicitly and Explicitly Using the `this` Pointer to Access an Object’s Data Members

Figure 9.23 demonstrates the implicit and explicit use of the `this` pointer to enable a member function of class Test to print the private data x of a Test object. In the next example and in Chapter 10, we show some substantial and subtle examples of using `this`.

```cpp
// Fig. 9.23: fig09_23.cpp
// Using the this pointer to refer to object members.
#include <iostream>
using namespace std;

class Test
{
public:
   explicit Test( int = 0 ); // default constructor
   void print() const;
private:
   int x;
}; // end class Test

// constructor
Test::Test( int value )
   : x( value ) // initialize x to value
{
   // empty body
} // end constructor Test

// print x using implicit and explicit this pointers;
// the parentheses around *this are required
void Test::print() const
{
   // implicitly use the this pointer to access the member x
   cout << "\n   x: " << x;

   // explicitly use the this pointer and the arrow operator
   // to access the member x
   cout << "\n   this->x: " << this->x;

   // explicitly use the dereferenced this pointer and
   // the dot operator to access the member x
   cout << "\n(*this).x = " << (*this).x << endl;
} // end function print

int main()
{
    Test testObject( 12 ); // instantiate and initialize testObject

    testObject.print();
} // end main
```

```text
   x: 12
   this->x: 12
(*this).x = 12
```

**Fig. 9.23** | using the this pointer to refer to object members.

For illustration purposes, member function print (lines 24–36) first prints x by using the *this pointer implicitly* (line 27)—only the name of the data member is specified. Then print uses two different notations to access the this pointer—the arrow operator (->) off the this pointer (line 31) and the dot operator (.) off the dereferenced this pointer (line 35). Note the parentheses around *this (line 35) when used with the dot member selection operator (.). The parentheses are required because the dot operator has *higher* precedence than the * operator. Without the parentheses, the expression *this.x would be evaluated as if it were parenthesized as *(this.x), which is a *compilation error*, because the dot operator cannot be used with a pointer.

One interesting use of the this pointer is to prevent an object from being assigned to itself. As we’ll see in Chapter 10, *self-assignment* can cause serious errors when the object contains pointers to dynamically allocated storage.

### Using the *this* Pointer to Enable Cascaded Function Calls

Another use of the this pointer is to enable cascaded member-function calls—that is, invoking multiple functions in the same statement (as in line 12 of Fig. 9.26). The program of Figs. 9.24–9.26 modifies class Time’s set functions setTime, setHour, setMinute and setSecond such that each returns a reference to a Time object to enable cascaded member-function calls. Notice in Fig. 9.25 that the last statement in the body of each of these member functions returns *this (lines 23, 34, 45 and 56) into a return type of Time &.

The program of Fig. 9.26 creates Time object t (line 9), then uses it in *cascaded member-function calls* (lines 12 and 24). Why does the technique of returning *this as a reference work? The dot operator (.) associates from left to right, so line 12 first evaluates t.setHour(18), then returns a reference to object t as the value of this function call. The remaining expression is then interpreted as

```cpp
t.setMinute( 30 ).setSecond( 22 );
```

The t.setMinute(30) call executes and returns a reference to the object t. The remaining expression is interpreted as

```cpp
t.setSecond( 22 );
```

