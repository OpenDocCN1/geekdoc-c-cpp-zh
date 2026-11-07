# # Passing references to functions

References provide access to the data stored in the variable to which they refer, just like the variable itself, and can be used to change the stored data by assigning a new value of the appropriate data type.

Additionally, references can, like pointers, be passed to functions as arguments:

+   - When variables are passed to functions, their data is passed “by value” to a local variable inside the function – so that the function operates on a copy of the original value.
+   - When references are passed to functions, their data is passed “by reference” – so the function operates on the original value.

The benefit of passing by reference allows functions to directly manipulate variable values declared within the calling function.

![](bbox=[0.118, 0.331, 0.185, 0.379])

fnref.cpp

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```
```cpp
#include <iostream>
using namespace std ;
```
```

+   2. After the preprocessor instructions, declare two function prototypes to each accept a single reference argument

```
```cpp
void writeOutput ( int& );
void computeTriple ( int& );
```
```

+   3. Add a main function containing a final return statement and declaring an initialized regular integer variable

```
```cpp
int main()
{
    int num = 5 ;
    // Add more statements here.
    return 0 ;
}
```
```

+   4. In the main function, insert a second variable declaration, initializing a reference as an alias of the integer variable

```
```cpp
int& ref = num ;
```
```

![](bbox=[0.118, 0.699, 0.207, 0.761])

This example may seem familiar, as it recreates the example here – but replaces pointers with references.

+   5. After the main function block, define a function to output the current value of a variable to which a reference refers

```
```cpp
void writeOutput( int& value )
{
    cout << “Current value: ” << value << endl ;
}
```
```

+   6. Define another function to multiply the current value of a variable to which a reference refers