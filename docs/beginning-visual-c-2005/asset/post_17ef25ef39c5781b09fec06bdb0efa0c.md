
```cpp
{
    found = true;
    continue;
}
else
{
    if(index == newData->Length)
    {
        Console::WriteLine(L"Element to remove not found");
        return data;
    }
    newData[index++] = item;
}
```

All elements are copied except the one identified by the first argument to the function. You use the index variable to select the next newData array element that is to receive the next element from the data array. Each element from data is copied unless it is equal to element, in which case found is set to true and the continue statement skips to the next iteration. It is quite possible that an array could have more than one element equal to the first argument and the found variable prevents subsequent elements that are the same as element from being skipped in the loop.

You also have a check for the index variable exceeding the legal limit for indexing elements in newData. This could arise if there is no element in the data array equal to the first argument to the function. In this eventuality, you just return the handle to the original array.

The third generic function just lists the elements from an array of type array<T>:

```cpp
generic<typename T>
void ListElements(array<T>^ data)
{
    for each(T item in data)
        Console::Write(L"{0,10}", item);
    Console::WriteLine();
}
```

This is one of the few occasions where no constraint on the type parameter is needed. There is very little you can do with objects that are of a completely unknown type so typically generic function type parameters will have constraints. The operation of the function is very simple—each element from the array is written to the command line in an output field with a width of 10 in the for each loop. If you want, you could add a little sophistication by adding a parameter for the field width and creating the format string to be used as the first argument to the Write() function in the Console class. You could also add logic to the loop to write a specific number of elements per line based on the field width.

The main() function exercises these generic functions with type parameters of types double, int, and String^. Thus you can see that all three generic functions work with value types and handles. In the second and third examples, the generic functions are used in combination in a single statement. For example, look at this statement in the third sample use of the functions:

```cpp
ListElements(RemoveElement(MaxElement(strings), strings));
```

The first argument to the RemoveElement() generic function is produced by the MaxElement() generic function call, so these generic functions can be used in the same way as equivalent ordinary functions.

The compiler is able to deduce the type argument in all instances where the generic functions are used but you could specify them explicitly if you wanted to. For example, you could write the previous statement like this:

```cpp
ListElements(RemoveElement<String^>(MaxElement<String^>(strings), strings));
```

## A Calculator Program for the CLR

Let’s re-implement the calculator as a C++/CLI example. We’ll assume the same program structure and hierarchy of functions as you saw for the native C++ program but the functions will be declared and defined as C++/CLI functions. A good starting point is the set of function prototypes at the beginning of the source file (I have used Ex6_11 as the CLR project name):

```cpp
// Ex6_11.cpp : main project file.
// A CLR calculator supporting parentheses

#include "stdafx.h"
#include <cstdlib>                              // For exit()

using namespace System;
String^ eatspaces(String^ str);                 // Function to eliminate blanks
double expr(String^ str);                      // Function evaluating an expression
double term(String^ str, int^ index);          // Function analyzing a term
double number(String^ str, int^ index);        // Function to recognize a number
String^ extract(String^ str, int^ index);       // Function to extract a substring
```

All the parameters are now handles; the string parameters are type String^ and the index parameter that records the current position in the string is also a handle of type int^. Of course, a string is returned as a handle of type String^.

The main() function implementation looks like this:

```cpp
int main(array<System::String ^> ^args)
{
    String^ buffer;     // Input area for expression to be evaluated

    Console::WriteLine(L"Welcome to your friendly calculator.");
    Console::WriteLine(L"Enter an expression, or an empty line to quit.");

    for(;;)
    {
        buffer = eatspaces(Console::ReadLine());        // Read an input line

        if(String::IsNullOrEmpty(buffer))               // Empty line ends calculator
            return 0;

        Console::WriteLine(L"  = {0}\n\n", expr(buffer)); // Output value of expression
    }
    return 0;
}
```

The function is a lot shorter and easier to read. Within the indefinite for loop you call the String class function, IsNullOrEmpty(). This function returns true if the string passed as the argument is null or of zero length so it does exactly what you want here.

### Removing Spaces from the Input String

The function to remove spaces is also simpler and shorter:

```cpp
// Function to eliminate spaces from a string
String^ eatspaces(String^ str)
{
    // Array to hold string without spaces
    array<wchar_t>^ chars = gcnew array<wchar_t>(str->Length);
    int length = 0;                         // Number of chars in array

    // Copy non-space characters to chars array
    for each(wchar_t ch in str)
        if(ch != ' ')
            chars[length++] = ch;

    // Return chars array as string
    return gcnew String(chars, 0, length);
}
```

You first create an array to accommodate the string when the spaces have been removed. This is an array of elements of type wchar_t because strings in C++/CLI are Unicode characters. The process for removing the spaces is very simple — you copy all the characters that are not spaces from the string str to the array, chars, keeping track of the number of characters copied in the length variable. You finally create a new String object using a String class constructor that creates the object from elements in an array. The first argument to the constructor is the array that is the source of characters for the string, the second argument is the index position for the first character from the array that forms the string, and the third argument is the total number of characters from the array that are to be used. The String class defines a range of constructors for creating strings in various ways.

### Evaluating an Arithmetic Expression

You can implement the function to evaluate an expression like this:

```cpp
// Function to evaluate an arithmetic expression
double expr(String^ str)
{
    int^ index = 0;                         // Keeps track of current character position

    double value = term(str, index);        // Get first term

    while(*index < str->Length)
    {
        switch(str[*index])                 // Choose action based on current character
        {
            case '+':                       // + found so
                ++(*index);                 // increment index and add
                value += term(str, index);  // the next term
                break;

            case '-':                // - found so
                ++(*index);          // increment index and subtract
                value -= term(str, index);  // the next term
                break;

            default:                 // If we reach here the string is junk
                Console::WriteLine(L"Arrgh!*#! There's an error.\n");
                exit(1);
        }
    }
    return value;
}
```

The index variable is declared as a handle because you want to pass it to the term() function and allow the term() function to modify the original variable. If you declared index simply as type int, the term() function would receive a copy of the value and could not refer to the original variable to change it.

The declaration of index results in a warning message from the compiler because the statement relies on autoboxing of the value 0 to produce the Int32 value class object that the handle references and the warning is because people often write the statement like this but intend to initialize the handle to null. Of course, to do this you must use nullptr as the initial value in place of 0. If you want to eliminate the warning, you could rewrite the statement as:

```cpp
int^ index = gcnew int(0);
```

This statement uses a constructor explicitly to create the object and initialize it with 0 so there’s no warning from the compiler.

After processing the initial term by calling the term() function the while loop steps through the string looking for + or - operators followed by another term. The switch statement identifies and processes the operators. If you have been using native C++ for a while, you might be tempted to write the case statements in the switch a little differently (for example:

```cpp
// Incorrect code!! Does not work!!
case '+':                // + found so
    value += term(str, ++(*index));  // increment index & add the next term
    break;
```

Of course, this would typically be written without the first comment. This code is wrong, but why is it wrong? The term() function expects a handle in type int^ as the second argument and that is what is supplied here although maybe not what you expect. The compiler arranges for the expression ++(*index) to be evaluated and the result stored in a temporary location. The expression indeed updates the value referenced by index, but the handle that is passed to the term() function is a handle to the temporary location holding the result of evaluating the expression, not the handle index. This handle is produced by autoboxing the value stored in the temporary location. When the term() function updates the value referenced by the handle that is passed to it, the temporary location is updated, not the location referenced by index; thus all the updates to the index position of the string made in the term() function are lost. If you expect a function to update a variable in the calling program, you must not use an expression as the function argument— you must always use the handle variable name.
