# Common Programming Error 7.2

Providing more initializers in an array initializer list than there are elements in the array is a compilation error.

# Common Programming Error 7.3

Forgetting to initialize the elements of an array whose elements should be initialized is a logic error.

# 7.4.3 Specifying an Array’s Size with a Constant Variable and Setting Array Elements with Calculations

Figure 7.5 sets the elements of a 10-element array s to the even integers 2, 4, 6, ..., 20 (lines 17–18) and prints the array in tabular format (lines 20–24). These numbers are generated (line 18) by multiplying each successive value of the loop counter by 2 and adding 2.

Line 13 uses the const qualifier to declare a so-called constant variable arraySize with the value 10. Constant variables must be initialized with a constant expression when they are declared and cannot be modified thereafter (as shown in Fig. 7.6 and Fig. 7.7). Constant variables are also called named constants or read-only variables.

# Common Programming Error 7.4

Not assigning a value to a constant variable when it is declared is a compilation error.

```
1  // Fig. 7.5: fig07_05.cpp
2  // Set array s to the even integers from 2 to 20.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  #include <iomanip>
8  using std::setw;
9
10 int main()
11 {
12     // constant variable can be used to specify array size
13     const int arraySize = 10;
14
15     int s[ arraySize ]; // array s has 10 elements
16
17     for ( int i = 0; i < arraySize; i++ ) // set the values
18         s[ i ] = 2 + 2 * i;
19
20     cout << "Element" << setw( 13 ) << "Value" << endl;
21
22     // output contents of array s in tabular format
23     for ( int j = 0; j < arraySize; j++ )
24         cout << setw( 7 ) << j << setw( 13 ) << s[ j ] << endl;
25
26     return 0; // indicates successful termination
27 } // end main
```

Fig. 7.5 | Generating values to be placed into elements of an array. (Part 1 of 2.)