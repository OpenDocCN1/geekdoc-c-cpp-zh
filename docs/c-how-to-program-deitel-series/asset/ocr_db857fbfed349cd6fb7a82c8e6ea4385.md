You can use pointers and the indirection operator (*) to accomplish pass-by-reference (exactly as pass-by-reference is done in C programs—C does not have references). When calling a function with an argument that should be modified, the address of the argument is passed. This is normally accomplished by applying the address operator (&) to the name of the variable whose value will be modified.

# An Example of Pass-By-Value

Figure 8.6 and Fig. 8.7 present two versions of a function that cubes an integer. Figure 8.6 passes variable number by value (line 14) to function cubeByValue (lines 19–22), which cubes its argument and passes the new value back to main using a return statement (line 21). The new value is assigned to number (line 14) in main. The calling function has the opportunity to examine the function call’s result before modifying variable number’s value. For example, we could have stored the result of cubeByValue in another variable, examined its value and assigned the result to number only after determining that the returned value was reasonable.

```
```cpp
// Fig. 8.6: fig08_06.cpp
// Pass-by-value used to cube a variable’s value.
#include <iostream>
using namespace std;

int cubeByValue( int ); // prototype

int main()
{
   int number = 5;

   cout << "The original value of number is " << number;

   number = cubeByValue( number ); // pass number by value to cubeByValue
      cout << "\nThe new value of number is " << number << endl;
} // end main

// calculate and return cube of integer argument
int cubeByValue( int n )
{
   return n * n * n; // cube local variable n and return result
} // end function cubeByValue
```
```

```
```text
The original value of number is 5
The new value of number is 125
```
```

Fig. 8.6  |  Pass-by-value used to cube a variable’s value.

# An Example of Pass-By-Reference with Pointers

Figure 8.7 passes the variable number to function cubeByReference using pass-by-reference with a pointer argument (line 15)—the address of number is passed to the function. Function cubeByReference (lines 21–24) specifies parameter nPtr (a pointer to int) to receive its argument. The function uses the dereferenced pointer to cube the value to which nPtr points (line 23). This directly changes the value of number in main (line 11). Line 23 is equivalent to

```
```cpp
*nPtr = (*nPtr) * (*nPtr) * (*nPtr); // cube *nPtr
```
```