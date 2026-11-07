
terminates or the program calls function `exit`. Global and static objects are destroyed in the reverse order of their creation. Destructors are not called for static objects if the program terminates with a call to function `abort`.

## Demonstrating When Constructors and Destructors Are Called

The program of Figs. 9.11–9.13 demonstrates the order in which constructors and destructors are called for objects of class CreateAndDestroy (Fig. 9.11 and Fig. 9.12) of various storage classes in several scopes. Each object of class CreateAndDestroy contains an integer (object ID) and a string (message) that are used in the program’s output to identify the object (Fig. 9.11 lines 16–17). This mechanical example is purely for pedagogic purposes. For this reason, line 21 of the destructor in Fig. 9.12 determines whether the object being destroyed has an object ID value 1 or 6 and, if so, outputs a newline character. This line makes the program’s output easier to follow.

```cpp
// Fig. 9.11: CreateAndDestroy.h
// CreateAndDestroy class definition.
// Member functions defined in CreateAndDestroy.cpp.
#include <string>
using namespace std;

#ifndef CREATE_H
#define CREATE_H

class CreateAndDestroy
{
public:
   CreateAndDestroy( int, string ); // constructor
   ~CreateAndDestroy(); // destructor
private:
   int objectID; // ID number for object
   string message; // message describing object
}; // end class CreateAndDestroy

#endif
```

**Fig. 9.11** | CreateAndDestroy class definition.

```cpp
// Fig. 9.12: CreateAndDestroy.cpp
// CreateAndDestroy class member-function definitions.
#include <iostream>
#include "CreateAndDestroy.h" // include CreateAndDestroy class definition
using namespace std;

// constructor
CreateAndDestroy::CreateAndDestroy( int ID, string messageString )
{
   objectID = ID; // set object's ID number
   message = messageString; // set object's descriptive message
   cout << "Object " << objectID << "  constructor runs  "
        << message << endl;
} // end CreateAndDestroy constructor

// destructor
CreateAndDestroy::~CreateAndDestroy()
{
   // output newline for certain objects; helps readability
   cout << (objectID == 1 || objectID == 6 ? "\n" : "");

   cout << "Object " << objectID << "  destructor runs  "
        << message << endl;
} // end ~CreateAndDestroy destructor
```

**Fig. 9.12** | CreateAndDestroy class member-function definitions. (Part 1 of 2.)

**Fig. 9.12** | CreateAndDestroy class member-function definitions. (Part 2 of 2.)

Figure 9.13 defines object first (line 10) in global scope. Its constructor is actually called *before* any statements in main execute and its destructor is called at program termination *after* the destructors for all other objects have run.

Function main (lines 12–23) declares three objects. Objects second (line 15) and fourth (line 24) are local automatic objects, and object third (line 16) is a static local object. The constructor for each of these objects is called when execution reaches the point where that object is declared. The destructors for objects fourth then second are called (i.e., the *reverse* of the order in which their constructors were called) when execution reaches the end of main. Because object third is static, it exists until program termination. The destructor for object third is called *before* the destructor for global object first, but *after* all other objects are destroyed.

Function create (lines 26–33) declares three objects—fifth (line 29) and seventh (line 31) as local automatic objects, and sixth (line 30) as a static local object. The destructors for objects seventh then fifth are called (i.e., the *reverse* of the order in which their constructors were called) when create terminates. Because sixth is static, it exists until program termination. The destructor for sixth is called *before* the destructors for third and first, but *after* all other objects are destroyed.

```cpp
// Fig. 9.13: fig09_13.cpp
// Demonstrates the order in which constructors and
// destructors are called.
#include <iostream>
#include "CreateAndDestroy.h" // include CreateAndDestroy class definition
using namespace std;

void create( void ); // prototype

CreateAndDestroy first( 1, "(global before main)" ); // global object

int main()
{
   cout << "\nMAIN FUNCTION: EXECUTION BEGINS" << endl;

15  CreateAndDestroy second( 2, "{local automatic in main}" );
16  static CreateAndDestroy third( 3, "{local static in main}" );

18  create(); // call function to create objects

20  cout << "\nMAIN FUNCTION: EXECUTION RESUMES" << endl;
21  CreateAndDestroy fourth( 4, "{local automatic in main}" );
22  cout << "\nMAIN FUNCTION: EXECUTION ENDS" << endl;
23 } // end main

25  // function to create objects
26  void create( void )
27  {
28      cout << "\nCREATE FUNCTION: EXECUTION BEGINS" << endl;
29      CreateAndDestroy fifth( 5, "{local automatic in create}" );
30      static CreateAndDestroy sixth( 6, "{local static in create}" );
31      CreateAndDestroy seventh( 7, "{local automatic in create}" );
32      cout << "\nCREATE FUNCTION: EXECUTION ENDS" << endl;
33 } // end function create
```

```text
Object 1  constructor runs   (global before main)

MAIN FUNCTION: EXECUTION BEGINS
Object 2  constructor runs   (local automatic in main)
Object 3  constructor runs   (local static in main)

CREATE FUNCTION: EXECUTION BEGINS
Object 5  constructor runs   (local automatic in create)
Object 6  constructor runs   (local static in create)
Object 7  constructor runs   (local automatic in create)

CREATE FUNCTION: EXECUTION ENDS
Object 7  destructor runs    (local automatic in create)
Object 5  destructor runs    (local automatic in create)

MAIN FUNCTION: EXECUTION RESUMES
Object 4  constructor runs   (local automatic in main)

MAIN FUNCTION: EXECUTION ENDS
Object 4  destructor runs    (local automatic in main)
Object 2  destructor runs    (local automatic in main)

Object 6  destructor runs    (local static in create)
Object 3  destructor runs    (local static in main)

Object 1  destructor runs    (global before main)
```

**Fig. 9.13** | Order in which constructors and destructors are called. (Part 1 of 2.)

**Fig. 9.13** | Order in which constructors and destructors are called. (Part 2 of 2.)

## 9.9 Time Class Case Study: A Subtle Trap—Returning a Reference to a private Data Member

A reference to an object is an alias for the name of the object and, hence, may be used on the left side of an assignment statement. In this context, the reference makes a perfectly acceptable lvalue that can receive a value. One way to use this capability (unfortunately!)

```cpp
// Fig. 9.16: fig09_16.cpp
// Demonstrating a public member function that
// returns a reference to a private data member.
#include <iostream>
#include "Time.h" // include definition of class Time
using namespace std;

int main()
{
   Time t; // create Time object

   // initialize hourRef with the reference returned by badSetHour
   int &hourRef = t.badSetHour( 20 ); // 20 is a valid hour

   cout << "Valid hour before modification: " << hourRef;
   hourRef = 30; // use hourRef to set invalid value in Time object t
   cout << "\nInvalid hour after modification: " << t.getHour();

   // Dangerous: Function call that returns
   // a reference can be used as an lvalue!
   t.badSetHour( 12 ) = 74; // assign another invalid value to hour

   cout << "\n\n" << "*********************************************\n"
      << "POOR PROGRAMMING PRACTICE!!!!!!!!!!!!!!!\n"
      << "t.badSetHour( 12 ) as an lvalue, invalid hour: "
      << t.getHour()
      << "\n" << "*********************************************" << endl;
} // end main
```

```text
Valid hour before modification: 20
Invalid hour after modification: 30

*********************************************
POOR PROGRAMMING PRACTICE!!!!!!!!!!!!!!!
t.badSetHour( 12 ) as an lvalue, invalid hour: 74
*********************************************
```

**Fig. 9.16** | Returning a reference to a private data member.

## 9.10 Default Memberwise Assignment

The assignment operator (=) can be used to assign an object to another object of the same type. By default, such assignment is performed by **memberwise assignment**—each data member of the object on the right of the assignment operator is assigned individually to the same data member in the object on the left of the assignment operator. Figures 9.17–9.18 define class Date for use in this example. Line 18 of Fig. 9.19 uses **default memberwise assignment** to assign the data members of Date object date1 to the corresponding data members of Date object date2. In this case, the month member of date1 is assigned to the month member of date2, the day member of date1 is assigned to the day member of date2 and the year member of date1 is assigned to the year member of date2. **[Caution:** Memberwise assignment can cause serious problems when used with a class whose data members contain pointers to dynamically allocated memory; we
