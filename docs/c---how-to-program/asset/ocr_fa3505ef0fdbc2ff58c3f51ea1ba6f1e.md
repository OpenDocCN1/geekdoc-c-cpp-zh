```
~~~cpp
1 // Fig. 18.12: fig18_12.cpp
2 // Single-argument constructors and implicit conversions.
3 #include <iostream>
4 #include "Array.h"
5 using namespace std;
6
7 void outputArray( const Array & ); // prototype
8
9 int main()
10 {
11    Array integers1( 7 ); // 7-element Array
12    outputArray( integers1 ); // output Array integers1
13    outputArray( 3 ); // convert 3 to an Array and output Array's contents
14 } // end main
15
16 // print Array contents
17 void outputArray( const Array &arrayToOutput )
18 {
19    cout << "The Array received has " << arrayToOutput.getSize()
20       << " elements. The contents are:\n" << arrayToOutput << endl;
21 } // end outputArray
~~~
```

```
~~~
The Array received has 7 elements. The contents are:
   0       0       0       0
   0       0       0
The Array received has 3 elements. The contents are:
   0       0       0
~~~
```

**Fig. 18.12** | Single-argument constructors and implicit conversions.

# *Preventing Implicit Conversions with Single-Argument Constructors*

The reason we've been declaring every single-argument constructor preceded by the keyword *explicit* is to *suppress implicit conversions via conversion constructors when such conversions should not be allowed*. A constructor that's declared `explicit` cannot be used in an *implicit* conversion. In the example of Fig. 18.13, we use the original version of `Array.h` from Fig. 18.10, which included the keyword `explicit` in the declaration of the *single-argument constructor* in line 14

```
~~~cpp
explicit Array( int = 10 ); // default constructor
~~~
```

Figure 18.13 presents a slightly modified version of the program in Fig. 18.12. When this program in Fig. 18.13 is compiled, the compiler produces an error message indicating that the integer value passed to `outputArray` in line 13 *cannot* be converted to a `const Array&`. The compiler error message (from Visual C++) is shown in the `output window`. Line 14 demonstrates how the `explicit` constructor can be used to create a temporary Array of 3 elements and pass it to function `outputArray`.

> > **Error-Prevention Tip 18.4**
> >
> > *Always use the `explicit` keyword on single-argument constructors unless they're intended to be used as conversion constructors.*