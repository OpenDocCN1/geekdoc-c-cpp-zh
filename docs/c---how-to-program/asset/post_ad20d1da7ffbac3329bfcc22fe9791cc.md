
Class Date and class Employee each include a destructor (lines 34–39 of Fig. 17.18 and lines 33–37 of Fig. 17.20, respectively) that prints a message when an object of its class is destructed. This enables us to confirm in the program output that objects are constructed from the inside out and destroyed in the reverse order, from the outside in (i.e., the Date member objects are destroyed after the Employee object that contains them).

Notice the last four lines in the output of Fig. 17.21. The last two lines are the outputs of the Date destructor running on Date objects hire (Fig. 17.21, line 11) and birth (Fig. 17.21, line 10), respectively. These outputs confirm that the three objects created in main are destructed in the reverse order of the order in which they were constructed. The Employee destructor output is five lines from the bottom. The fourth and third lines from the bottom of the output window show the destructors running for the Employee's member objects hireDate (Fig. 17.19, line 21) and birthDate (Fig. 17.19, line 20). The last two lines of the output correspond to the Date objects created in lines 11 and 10 of Fig. 17.21.

These outputs confirm that the Employee object is destroyed from the outside in—i.e., the Employee destructor runs first (output shown five lines from the bottom of the output window), then the member objects are destructed in the reverse order from which they were constructed. Class string's destructor does not contain output statements, so we do not see the firstName and lastName objects being destructed. Again, Fig. 17.21's output did not show the constructors running for member objects birthDate and hireDate, because these objects were initialized with the default Date class copy constructors provided by the compiler.

### What Happens When You Do Not Use the Member Initializer List?

If a member object is not initialized through a member initializer, the member object's default constructor will be called implicitly. Values, if any, established by the default constructor can be overridden by set functions. However, for complex initialization, this approach may require significant additional work and time.

**Common Programming Error 17.5**

A compilation error occurs if a member object is not initialized with a member initializer and the member object's class does not provide a default constructor (i.e., the member object's class defines one or more constructors, but none is a default constructor).

**Performance Tip 17.4**

Initialize member objects explicitly through member initializers. This eliminates the overhead of "doubly initializing" member objects—once when the member object's default constructor is called and again when set functions are called in the constructor body (or later) to initialize the member object.

**Software Engineering Observation 17.11**

If a data member is an object of another class, making that member object public does not violate the encapsulation and hiding of that member object's private members. But, it does violate the encapsulation and hiding of the containing class's implementation, so member objects of class types should still be private.

## 17.12 friend Functions and friend Classes

A friend function of a class is a non-member function that has the right to access the public and non-public class members. Standalone functions, entire classes or member functions of other classes may be declared to be friends of another class.

This section presents a mechanical example of how a friend function works. In Chapter 18 we'll show friend functions that overload operators for use with class objects—as you'll see, sometimes a member function cannot be used for certain overloaded operators.

### Declaring a friend

To declare a function as a friend of a class, precede the function prototype in the class definition with the keyword friend. To declare all member functions of class ClassTwo as friends of class ClassOne, place a declaration of the form

```cpp
friend class ClassTwo;
```

in the definition of class ClassOne.

Friendship is granted, not taken—for class B to be a friend of class A, class A must explicitly declare that class B is its friend. Friendship is not symmetric—if class A is a friend of class B, you cannot infer that class B is a friend of class A. Friendship is not transitive—if class A is a friend of class B and class B is a friend of class C, you cannot infer that class A is a friend of class C.

### Modifying a Class's private Data with a Friend Function

Figure 17.22 is a mechanical example in which we define friend function setX to set the private data member x of class Count. As a convention, we place the friend declaration (line 9) first in the class definition, even before public member functions are declared. Again, this friend declaration can appear anywhere in the class.

Function setX (lines 29–32) is a standalone (global) function—it isn't a member function of class Count. For this reason, when setX is invoked for object counter, line 41 passes counter as an argument to setX rather than using a handle (such as the name of the object) to call the function, as in

```cpp
counter.setX( 8 ); // error: setX not a member function
```

If you remove the friend declaration in line 9, you'll receive error messages indicating that function setX cannot modify class Count's private data member x.

**Fig. 17.22 |** Friends can access private members of a class. (Part 1 of 2.)

```cpp
1  // Fig. 17.22: fig17_22.cpp
2  // Friends can access private members of a class.
3  #include <iostream>
4  using namespace std;
5
6  // Count class definition
7  class Count
8  {
9     friend void setX( Count &, int ); // friend declaration
10 public:
11    // constructor
12    Count()
13       : x( 0 ) // initialize x to 0
14    {      // empty body
15    } // end constructor Count
16
17    // output x
18    void print() const
19    {
20       cout << x << endl;
21    } // end function print
22 private:
23    int x; // data member
24 }; // end class Count
25
26
27 // function setX can modify private data of Count
28 // because setX is declared as a friend of Count (line 9)
29 void setX( Count &c, int val )
30 {
31    c.x = val; // allowed because setX is a friend of Count
32 } // end function setX
33
34
35 int main()
36 {
37    Count counter; // create Count object
38
39    cout << "counter.x after instantiation: ";
40    counter.print();
41
42    setX( counter, 8 ); // set x using a friend function
43    cout << "counter.x after call to setX friend function: ";
44    counter.print();
45 } // end main
```

```text
counter.x after instantiation: 0
counter.x after call to setX friend function: 8
```

**Fig. 17.22 |** Friends can access private members of a class. (Part 2 of 2.)

As we mentioned, Fig. 17.22 is a mechanical example of using the friend construct. It would normally be appropriate to define function setX as a member function of class Count. It would also normally be appropriate to separate the program of Fig. 17.22 into three files:

1. A header (e.g., Count.h) containing the Count class definition, which in turn contains the prototype of friend function setX
2. An implementation file (e.g., Count.cpp) containing the definitions of class Count's member functions and the definition of friend function setX
3. A test program (e.g., fig17_22.cpp) with main.

### Overloaded friend Functions

It's possible to specify overloaded functions as friends of a class. Each function intended to be a friend must be explicitly declared in the class definition as a friend of the class.

> **Software Engineering Observation 17.12**
>
> *Even though the prototypes for friend functions appear in the class definition, friends are not member functions.*

> **Software Engineering Observation 17.13**
>
> *Member access notions of private, protected and public are not relevant to friend declarations, so friend declarations can be placed anywhere in a class definition.*

> **Good Programming Practice 17.4**
>
> *Place all friendship declarations first inside the class definition's body and do not precede them with any access specifier.*

## 17.13 Using the *this* Pointer

We've seen that an object's member functions can manipulate the object's data. There can be many objects of a class, so how do member functions know which object's data members to manipulate? Every object has access to its own address through a pointer called *this* (a C++ keyword). The *this* pointer is not part of the object itself—i.e., the memory occupied by the *this* pointer is not reflected in the result of a `sizeof` operation on the object. Rather, the *this* pointer is passed (by the compiler) as an *implicit* argument to each of the object's non-static member functions. Section 17.14 introduces *static* class members and explains why the *this* pointer is not implicitly passed to *static* member functions.

### Using the *this* Pointer to Avoid Naming Collisions

Member functions use the *this* pointer *implicitly* (as we've done so far) or *explicitly* to reference an object's data members and other member functions. A common *explicit* use of the *this* pointer is to avoid *naming conflicts* between a class's data members and member-function parameters (or other local variables). Consider the `Time` class's `hour` data member and `setHour` member function in Figs. 17.4–17.5. We could have defined `setHour` as:

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

In this function definition, `setHour`'s parameter has the *same name* as the data member `hour`. In `setHour`'s scope, the parameter `hour` *hides* the data member. However, you can still access the data member `hour` by qualifying its name with `this->`. So the following statement assigns the `hour` parameter's value to the data member `hour`.

```cpp
this->hour = hour; // use this pointer to access data member
```
