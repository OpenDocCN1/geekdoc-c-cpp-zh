# Catching Exceptions

The catch block following the try block in our example catches any exception of type const char []. This is determined by the parameter specification that appears in parentheses following the keyword catch. You must supply at least one catch block for a try block, and the catch blocks must immediately follow the try block. A catch block catches all exceptions (of the correct type) that occur anywhere in the code in the immediately preceding try block, including those thrown in any functions called directly or indirectly within the try block.

If you want to specify that a catch block is to handle any exception thrown in a try block, you must put an ellipsis (...) between the parentheses enclosing the exception declaration:

```
catch (...)
{
    // code to handle any exception
}
```

This catch block must appear last if you have other catch blocks defined for the try block.

# Try It Out Nested try Blocks

You can nest try blocks one within another. With this situation, if an exception is thrown from within an inner try block that is not followed by a catch block corresponding to the type of exception thrown, the catch handlers for the outer try block are searched. You can demonstrate this with the following example:

```
// Ex6_05.cpp
// Nested try blocks
#include <iostream>
using std::cin;
using std::cout;
using std::endl;

int main(void)
{
    int height = 0;
    const double inchesToMeters = 0.0254;
    char ch = 'y';

    try                                    // Outer try block
    {
        while(ch == 'y'||ch =='Y')
        {
            cout << "Enter a height in inches: ";
            cin >> height;                 // Read the height to be converted

            try                          // Defines try block in which
            {                            // exceptions may be thrown
                if(height > 100)
                    throw "Height exceeds maximum";   // Exception thrown
                if(height < 9)
                    throw height;                      // Exception thrown

                cout << static_cast<double>(height)*inchesToMeters
```