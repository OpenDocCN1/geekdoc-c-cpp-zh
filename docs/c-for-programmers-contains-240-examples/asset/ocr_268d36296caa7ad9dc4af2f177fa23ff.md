word explicit to the declaration of the single-argument constructor in line 15. No modifications are required to the source-code file containing class Array’s member-function definitions.

Figure 11.18 presents a slightly modified version of the program in Fig. 11.16. When this program is compiled, the compiler produces an error message indicating that the integer value passed to outputArray in line 15 cannot be converted to a const Array &. The compiler error message is shown in the output window. Line 16 demonstrates how the explicit constructor can be used to create a temporary Array of 3 elements and pass it to function outputArray.

# Common Programming Error 11.10

> Attempting to invoke an explicit constructor for an implicit conversion is a compilation error.

# Common Programming Error 11.11

> Using the explicit keyword on data members or member functions other than a single-argument constructor is a compilation error.

```
1 // Fig. 11.18: Fig11_18.cpp
2 // Driver for simple class Array.
3 #include <iostream>
4 using std::cout;
5 using std::endl;
6 
7 #include "Array.h"
8 
9 void outputArray( const Array & ); // prototype
10 
11 int main()
12 {
13     Array integers1( 7 ); // 7-element array
14     outputArray( integers1 ); // output Array integers1
15     outputArray( 3 ); // convert 3 to an Array and output Array's contents
16     outputArray( Array( 3 ) ); // explicit single-argument constructor call
17     return 0;
18 } // end main
19 
20 // print array contents
21 void outputArray( const Array &arrayToOutput )
22 {
23     cout << "The Array received has " << arrayToOutput.getSize()
24         << " elements. The contents are:\n" << arrayToOutput << endl;
25 } // end outputArray
```

```
c:\cppfp_examples\ch11\Fig11_17_18\Fig11_18.cpp(15) : error C2664:
    'outputArray' : cannot convert parameter 1 from 'int' to 'const Array &'
    Reason: cannot convert from 'int' to 'const Array'
    Constructor for class 'Array' is declared 'explicit'
```

Fig. 11.18 | Demonstrating an explicit constructor.