
- 8. Save, compile, and run the program to see the pointer addresses and the stored values

![](img/bf8dbdfb89042fadbaa73b4160c74bac_100_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_100_1.png)

The `*` dereference operator is alternatively known as the “indirection” operator.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_100_2.png)

The memory addresses are dynamically allocated – so will vary from those in this screenshot.

## Doing pointer arithmetic

Once a pointer variable has been initialized with a memory address, it can be assigned another address, or changed using pointer arithmetic.

The `++` increment operator or the `--` decrement operator will move the pointer along to the next or previous address for that data type – the larger the data type, the bigger the jump.

Even larger jumps can be achieved using the `+=` and `-=` operators.

Pointer arithmetic is especially useful with arrays, because the elements in an array occupy consecutive memory addresses. Assigning just the name of an array to a pointer automatically assigns it the address of the first element. Incrementing the pointer by one moves the pointer along to the next element.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_101_0.png)

point.cpp

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```cpp
#include <iostream>
using namespace std;
```

- 2. Add a main function containing a final return statement and declaring an initialized integer array of 10 elements

```cpp
int main()
{
    int nums[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    // Add more statements here.
    return 0;
}
```

- 3. In the main function, insert a statement to declare a pointer, initialized with the memory address of the first element in the integer array

```cpp
int* ptr = nums;
```

- 4. Next, insert a statement to output the memory address of the first element of the integer array, and its value

```cpp
cout << endl << "ptr at: " << ptr << " gets: " << *ptr;
```

- 5. Now, increment the pointer and output its new memory address – that of the second element in the integer array

```cpp
ptr++;
cout << endl << "ptr at: " << ptr << " gets: " << *ptr;
```

- 6. Increment the pointer again, and output its new memory address – that of the third element in the integer array

```cpp
ptr++;
cout << endl << "ptr at: " << ptr << " gets: " << *ptr;
```

- 7. Decrement the pointer by two places and output its memory address – that of the first element in the array

```cpp
ptr -= 2;
cout << endl << "ptr at: " << ptr << " gets: " << *ptr;
cout << endl;
```

- 8. Now, insert a loop to output the value stored in each element of the integer array

```cpp
for ( int i = 0 ; i < 10 ; i++ )
{
    cout << endl << "Element: " << i ;
    cout << " Value: " << *ptr ;
    ptr++;
}
cout << endl;
```

- 9. Save, compile, and run the program to see the pointer addresses and the stored values

![](img/bf8dbdfb89042fadbaa73b4160c74bac_102_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_102_1.png)

The `*=`, `/=`, and `%=` operators cannot be used to move a pointer.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_102_2.png)

The name of an array acts like a pointer to its first element.

## Passing pointers to functions

Pointers can access the data stored in the variable to which they point using the `*` dereference operator. This can also be used to change the stored data by assigning a new value of the appropriate data type.

Additionally, pointers can be passed to functions as arguments – with a subtly different effect to passing variables as arguments:

- When variables are passed to functions, their data is passed “by value” to a local variable inside the function – so that the function operates on a copy of the original value.
- When pointers are passed to functions, their data is passed “by reference” – so that the function operates on the **original** value.

The benefit of passing by reference allows functions to directly manipulate variable values declared within the calling function.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_103_0.png)

fnptr.cpp

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.

```cpp
#include <iostream>
using namespace std;
```

- 2. After the preprocessor instructions, declare two function prototypes to each accept a single pointer argument.

```cpp
void writeOutput( int* );
void computeTriple( int* );
```

- 3. Add a main function containing a final **return** statement and declaring an initialized regular integer variable.

```cpp
int main()
{
    int num = 5;
    // Add more statements here.
    return 0;
}
```

- 4. In the main function, insert a second variable declaration that initializes a pointer with the address of the regular integer variable.

```cpp
int* ptr = &num;
```

- 5. After the main function block, define a function to output the current value of a variable to which a pointer points.

```cpp
void writeOutput( int* value )
{
    cout << "Current value: " << *value << endl;
}
```

- 6. Define another function to multiply the current value of a variable to which a pointer points.

```cpp
void computeTriple( int* value )
{
    *value *= 3;   // Multiply and assign dereferenced value.
}
```

- 7. In the main function, pass a pointer argument to a function to output the variable value to which it points.

```cpp
writeOutput( ptr );
```

- 8. Next, use the pointer to increase the variable value, then display its new value

```cpp
*ptr += 15;    // Add and assign a dereferenced value.
writeOutput( ptr );
```

- 9. Now, pass a pointer argument to a function to multiply the variable to which it points, then display its new value

```cpp
computeTriple( ptr );
writeOutput( ptr );
```

- 10. Save, compile, and run the program to see the computed values output

![](img/bf8dbdfb89042fadbaa73b4160c74bac_104_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_104_1.png)

The function prototype and definition must both contain a pointer argument.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_104_2.png)

Functions that operate directly on variables within the calling function need no **return** statement.

## Making arrays of pointers

A variable of the regular **char** data type can be assigned a single character value, but a pointer to a constant **char** array can usefully be assigned a string of characters. The string is actually stored as an array of characters, with one character per element, but referencing the **char** pointer will automatically retrieve the entire string.

This ability to retrieve a string value from a **char** pointer using just its variable name resembles the way that a string can be retrieved from a regular **char** array using its variable name.

Multiple strings can be stored in a constant **char** pointer array, with one string per element. You can even store multiple **char** pointer arrays in a “master” **char** pointer array -- one array per element.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_105_0.png)

- 1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use.

```cpp
#include <iostream>
using namespace std;
```

- 2. Add a main function containing a final **return** statement and declaring two initialized variables -- a regular character array, and a character pointer with identical **string** values.

```cpp
int main()
{
    char letters[8] = {'C', '+', '+', ' ', 'F', 'u', 'n', '\0'};
    const char* text = "C++ Fun";
    // Add more statements here.
    return 0;
}
```

- 3. In the main function, insert statements to declare, and initialize two further character pointer variables, with unique **string** values.

```cpp
const char* term = "Element";
const char* lang = "C++";
```

- 4. Next, insert a statement to declare a character pointer array, initialized with three **string** values.

```cpp
const char* ap1[3] = {"Great", "Program", "Code"};
```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_105_1.png)

Character values must be enclosed in single quotes, but string values must be enclosed in double quotes -- even when they are being assigned to a **char** pointer.

- 5. Now, insert a statement to declare a second character pointer array, initialized with three string values -- making one of the pointer variables its first element value.

```cpp
const char* ap2[3] = {lang, "is", "Fun"};
```

- 6. Declare two “master” character pointer arrays, each initialized with three elements of the **char** pointer arrays.

```cpp
const char* ap3[3] = {ap2[0], ap2[1], ap1[0]};
const char* ap4[3] = {ap1[2], ap2[1], ap2[2]};
```

- 7. After the declarations, insert statements to output the identical **string** values of the first two variables.
