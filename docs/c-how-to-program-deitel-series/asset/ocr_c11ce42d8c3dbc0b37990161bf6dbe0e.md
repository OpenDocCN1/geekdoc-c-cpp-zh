**6.42** _（Distance Between Points）_ Write function `distance` that calculates the distance between two points `(x1, y1)` and `(x2, y2)`. All numbers and return values should be of type `double`.

**6.43** What’s wrong with the following program?

```
```cpp
// Exercise 6.43: ex06_43.cpp
// What is wrong with this program?
#include <iostream>
using namespace std;

int main()
{
   int c = 0;

   if ( ( c = cin.get() ) != EOF )
   {
      main();
      cout << c;
   } // end if
} // end main
```
```

**6.44** What does the following program do?

```
```cpp
// Exercise 6.44: ex06_44.cpp
// What does this program do?
#include <iostream>
using namespace std;

int mystery( int, int ); // function prototype

int main()
{
   int x = 0;
   int y = 0;

   cout << "Enter two integers: ";
   cin >> x >> y;
   cout << "The result is " << mystery( x, y ) << endl;
} // end main

// Parameter b must be a positive integer to prevent infinite recursion
int mystery( int a, int b )
{
   if ( b == 1 ) // base case
      return a;
   else // recursive step
      return a + mystery( a, b - 1 );
} // end function mystery
```
```

**6.45** After you determine what the program of Exercise 6.44 does, modify the program to function properly after removing the restriction that the second argument be nonnegative.

**6.46** _（Math Library Functions）_ Write a program that tests as many of the math library functions in Fig. 6.2 as you can. Exercise each of these functions by having your program print out tables of return values for a diversity of argument values.

**6.47** _（Find the Error）_ Find the error in each of the following program segments and explain how to correct it: