
If an object has member objects, and if an exception is thrown before the outer object is fully constructed, then destructors will be executed for the member objects that have been constructed prior to the occurrence of the exception. If an array of objects has been partially constructed when an exception occurs, only the destructors for the constructed objects in the array will be called.

> **Error-Prevention Tip 17.6**
>
> _When an exception is thrown from the constructor for an object that’s created in a new expression, the dynamically allocated memory for that object is released._

![](img/b42ba5cd262b1358d16610173f975e4d_787_0.png)

> **Error-Prevention Tip 17.7**
>
> _A constructor should throw an exception if a problem occurs while initializing an object. Before doing so, the constructor should release any memory that it dynamically allocated._

![](img/b42ba5cd262b1358d16610173f975e4d_787_1.png)

### *Initializing Local Objects to Acquire Resources*

An exception could preclude the operation of code that would normally release a resource (such as memory or a file), thus causing a resource leak that prevents other programs from acquiring the resource. One technique to resolve this problem is to initialize a local object to acquire the resource. When an exception occurs, the destructor for that object will be invoked and can free the resource.

## 17.7 Exceptions and Inheritance

Various exception handlers can be derived from a common base class, as we discussed in Section 17.2, when we created class DivideByZeroException as a derived class of class exception. If a catch handler catches a reference to an exception object of a base-class type, it also can catch a reference to all objects of classes publicly derived from that base class—this allows for polymorphic processing of related exceptions.

> **Error-Prevention Tip 17.8**
>
> _Using inheritance with exceptions enables an exception handler to catch related errors with concise notation. One approach is to catch each type of reference to a derived-class exception object individually, but a more concise approach is to catch pointers or references to base-class exception objects instead. Also, catching pointers or references to derived-class exception objects individually is error prone, especially if you forget to test explicitly for one or more of the derived-class reference types._

![](img/b42ba5cd262b1358d16610173f975e4d_787_2.png)

## 17.8 Processing new Failures

When operator new fails, it throws a bad_alloc exception (defined in header <new>). In this section, we present two examples of new failing. The first uses the version of new that throws a bad_alloc exception when new fails. The second uses function set_new_handler to handle new failures. [Note: The examples in Figs. 17.5–17.6 allocate large amounts of dynamic memory, which could cause your computer to become sluggish.]

### *new Throwing bad_alloc on Failure*

Figure 17.5 demonstrates new implicitly throwing bad_alloc on failure to allocate the requested memory. The for statement (lines 16–20) inside the try block should loop 50 times and, on each pass, allocate an array of 50,000,000 double values. If new fails and throws a bad_alloc exception, the loop terminates, and the program continues in line 22, where the catch handler catches and processes the exception. Lines 24--25 print the message "Exception occurred: " followed by the message returned from the base-class-exception version of function what (i.e., an implementation-defined exception-specific message, such as "bad allocation" in Microsoft Visual C++). The output shows that the program performed only four iterations of the loop before new failed and threw the bad_alloc exception. Your output might differ based on the physical memory, disk space available for virtual memory on your system and the compiler you’re using.

```cpp
// Fig. 17.5: fig17_05.cpp
// Demonstrating standard new throwing bad_alloc when memory
// cannot be allocated.
#include <iostream>
#include <new> // bad_alloc class is defined here
using namespace std;

int main()
{
   double *ptr[ 50 ];

   // aim each ptr[i] at a big block of memory
   try
   {
      // allocate memory for ptr[ i ]; new throws bad_alloc on failure
      for ( size_t i = 0; i < 50; ++i )
      {
         ptr[ i ] = new double[ 50000000 ]; // may throw exception
         cout << "ptr[" << i << "] points to 50,000,000 new doubles\n";
      } // end for
   } // end try
   catch ( bad_alloc &memoryAllocationException )
   {
      cerr << "Exception occurred: "
           << memoryAllocationException.what() << endl;
   } // end catch
} // end main
```

```text
ptr[0] points to 50,000,000 new doubles
ptr[1] points to 50,000,000 new doubles
ptr[2] points to 50,000,000 new doubles
ptr[3] points to 50,000,000 new doubles
Exception occurred: bad allocation
```

Fig. 17.5 | new throwing bad_alloc on failure.

### new Returning nullptr on Failure

The C++ standard specifies that programmers can use an older version of new that returns nullptr upon failure. For this purpose, header <new> defines object nothrow (of type nothrow_t), which is used as follows:

```cpp
double *ptr = new( nothrow ) double[ 50000000 ];
```

```cpp
public:
    Integer( int i = 0 ); // Integer default constructor
    ~Integer(); // Integer destructor
    void setInteger( int i ); // set Integer value
    int getInteger() const; // return Integer value
private:
    int value;
}; // end class Integer
```

Fig. 17.7 | Integer class definition. (Part 2 of 2.)

```cpp
// Fig. 17.8: Integer.cpp
// Integer member function definitions.
#include <iostream>
#include "Integer.h"
using namespace std;

// Integer default constructor
Integer::Integer( int i )
    : value( i )
{
    cout << "Constructor for Integer " << value << endl;
} // end Integer constructor

// Integer destructor
Integer::~Integer()
{
    cout << "Destructor for Integer " << value << endl;
} // end Integer destructor

// set Integer value
void Integer::setInteger( int i )
{
    value = i;
} // end function setInteger

// return Integer value
int Integer::getInteger() const
{
    return value;
} // end function getInteger
```

Fig. 17.8 | Member function definitions of class Integer.

Line 15 of Fig. 17.9 creates `unique_ptr` object `ptrToInteger` and initializes it with a pointer to a dynamically allocated Integer object that contains the value 7. Line 18 uses the `unique_ptr` overloaded `->` operator to invoke function `setInteger` on the Integer object that `ptrToInteger` manages. Line 21 uses the `unique_ptr` overloaded `*` operator to dereference `ptrToInteger`, then uses the dot (`.`) operator to invoke function `getInteger` on the Integer object. Like a regular pointer, a `unique_ptr`’s `->` and `*` overloaded operators can be used to access the object to which the `unique_ptr` points.

```cpp
// Fig. 17.9: fig17_09.cpp
// Demonstrating unique_ptr.
#include <iostream>
#include <memory>
using namespace std;

#include "Integer.h"

// use unique_ptr to manipulate Integer object
int main()
{
   cout << "Creating a unique_ptr object that points to an Integer\n";

   // "aim" unique_ptr at Integer object
   unique_ptr<Integer> ptrToInteger( new Integer( 7 ) );

   cout << "\nUsing the unique_ptr to manipulate the Integer\n";
   ptrToInteger->setInteger( 99 ); // use unique_ptr to set Integer value

   // use unique_ptr to get Integer value
   cout << "\nInteger after setInteger: " << ( *ptrToInteger ).getInteger()
      << "\n\nTerminating program" << endl;
} // end main
```

```text
Creating a unique_ptr object that points to an Integer
Constructor for Integer 7

Using the unique_ptr to manipulate the Integer
Integer after setInteger: 99

Terminating program
Destructor for Integer 99
```

**Fig. 17.9** | unique_ptr object manages dynamically allocated memory.

Because ptrToInteger is a local automatic variable in main, ptrToInteger is destroyed when main terminates. The unique_ptr destructor forces a delete of the Integer object pointed to by ptrToInteger, which in turn calls the Integer class destructor. The memory that Integer occupies is released, regardless of how control leaves the block (e.g., by a return statement or by an exception). Most importantly, using this technique can prevent memory leaks. For example, suppose a function returns a pointer aimed at some object. Unfortunately, the function caller that receives this pointer might not delete the object, thus resulting in a memory leak. However, if the function returns a unique_ptr to the object, the object will be deleted automatically when the unique_ptr object's destructor gets called.

### unique_ptr Notes

The class is called unique_ptr because only one unique_ptr at a time can own a dynamically allocated object. By using its overloaded assignment operator or copy constructor, a unique_ptr can transfer ownership of the dynamic memory it manages. The last unique_ptr object that maintains the pointer to the dynamic memory will delete the
