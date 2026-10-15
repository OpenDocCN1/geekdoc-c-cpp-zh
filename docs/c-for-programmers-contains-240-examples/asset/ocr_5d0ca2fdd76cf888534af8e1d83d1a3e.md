Line 18 of Fig. 16.10 creates auto_ptr object ptrToInteger and initializes it with a pointer to a dynamically allocated Integer object that contains the value 7. Line 21 uses the auto_ptr overloaded -> operator to invoke function setInteger on the Integer object that ptrToInteger manages. Line 24 uses the auto_ptr overloaded * operator to dereference ptrToInteger, then uses the dot (.) operator to invoke function getInteger on the Integer object. Like a regular pointer, an auto_ptr’s -> and * overloaded operators can be used to access the object to which the auto_ptr points.

Because ptrToInteger is a local automatic variable in main, ptrToInteger is destroyed when main terminates. The auto_ptr destructor forces a delete of the Integer object pointed to by ptrToInteger, which in turn calls the Integer class destructor. The memory that Integer occupies is released, regardless of how control leaves the block (e.g., by a return statement or by an exception). Most importantly, using this technique can prevent memory leaks. For example, suppose a function returns a pointer aimed at some object. Unfortunately, the function caller that receives this pointer might not delete the object, thus resulting in a memory leak. However, if the function returns an auto_ptr to

```
1 // Fig. 16.10: Fig16_10.cpp
2 // Demonstrating auto_ptr.
3 #include <iostream>
4 using std::cout;
5 using std::endl;
6 
7 #include <memory>
8 using std::auto_ptr; // auto_ptr class definition
9 
10 #include "Integer.h"
11 
12 // use auto_ptr to manipulate Integer object
13 int main()
14 {
15     cout << "Creating an auto_ptr object that points to an Integer\n";
16 
17     // "aim" auto_ptr at Integer object
18     auto_ptr< Integer > ptrToInteger( new Integer( 7 ) );
19 
20     cout << "\nUsing the auto_ptr to manipulate the Integer\n";
21     ptrToInteger->setInteger( 99 ); // use auto_ptr to set Integer value
22 
23     // use auto_ptr to get Integer value
24     cout << "Integer after setInteger: " << ( *ptrToInteger ).getInteger()
25     return 0;
26 } // end main
```

Creating an auto_ptr object that points to an Integer
Constructor for Integer 7

Using the auto_ptr to manipulate the Integer
Integer after setInteger: 99

Destructor for Integer 99

Fig. 16.10 | auto_ptr object manages dynamically allocated memory.