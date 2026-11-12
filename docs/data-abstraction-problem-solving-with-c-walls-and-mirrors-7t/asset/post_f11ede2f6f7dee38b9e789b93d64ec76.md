
> Note: If an exception occurs in the middle of a try block, the destructors of all objects local to that block are called. This ensures that all resources allocated in that block are released, even if the block is not completely executed. In general, you should not use the new operator inside of a try block. An exception will complicate knowing whether memory was allocated and, if it was, whether it was deallocated.

> Programming Tip: An important implementation detail of a try block is that it should contain as few statements as possible—ideally, only the statement that could throw an exception. Keeping the try block small reduces the risk of either important code not being executed or allocated memory not being deallocated if an exception is thrown.

The syntax for a catch block resembles that of a function definition. It specifies both the type of exception the catch block will handle and an identifier. This identifier—called a catch block parameter—provides a name for the caught exception that can be used within the catch block. Although a catch block is not a function, throwing an exception is like calling a catch block as if it were a function. The catch block parameter represents the actual exception object provided by the throw statement.

The steps taken in the catch block vary from situation to situation and can be as simple as either doing nothing or displaying an error message, or as elaborate as tests that update variables and retry the function that threw the exception. Every exception class in the C++ Standard Library defines the accessor method what, which returns a descriptive string created when the exception is thrown. The body of the catch block can display this string to provide an indication of the nature of the exception.

> Note: A catch block whose parameter has the type ExceptionClass can catch exceptions of the class ExceptionClass and any of ExceptionClass's descendant classes. Specifying a catch block with a parameter of type exception catches any exception that can be thrown.

Listing C3-4 shows sample code that calls our findBox function and catches any logic_error exception thrown. The catch block displays a message to the user that something unusual has happened and creates a PlainBox object for findBox so that the statement following the catch block executes correctly.

```
LISTING C3-4 Trying the function findBox
// Create and initialize an array of boxes
PlainBox<string> myBoxes[5]; // Array of PlainBox objects
myBoxes[0] = PlainBox<string>("ring");
myBoxes[1] = PlainBox<string>("hat");
myBoxes[2] = PlainBox<string>("skirt");
myBoxes[3] = PlainBox<string>("sock");
myBoxes[4] = PlainBox<string>("shoe");
PlainBox<string> foundBox;
```

```
// Try to find a box containing glasses
try
{
    foundBox = findBox(myBoxes, 5, "glasses");
}
catch(logic_error logErr)
{
    cout << logErr.what() << endl;    // Display error message to user
    foundBox = PlainBox<string>("nothing"); // Fix problem
} // end try-catch
// Because we catch the exception and fix the problem, the following
// statement should work even if the target is not found
cout << foundBox.getItem();
Output
Target not found in a box!
nothing
```

### C3.4.1 Multiple catch Blocks

A single statement within a try block might cause more than one type of exception. Thus, a try block can have many catch blocks associated with it. When more than one catch block follows a try block, the catch block that executes is the first one—in order of appearance—whose parameter matches the thrown exception in type. Thus, the catch blocks must be ordered so that the most specific exception classes are caught before the more general exception classes. For example, the following catch blocks are in the wrong order:

```
string str = "Sarah";
try
{
    str.substr(99, 1);
    <other statements appear here...>
}
catch (exception e)    // WRONG ORDER!!
{
    cout << "Something else was caught" << endl;
}
catch (out_of_range e)
{
    cout << "out_of_range exception caught" << endl;
} // end try-catch
```

The compiler may issue a warning message similar to the following one:

> 'class std::out_of_range' : is caught by base class ('class exception')
> on line n

This warning means that any out_of_range exception thrown in the try block will be caught by the first catch block—with the parameter of type exception—so the second catch block will never be reached. To get the code to compile without warnings, you must interchange the two catch blocks.

> **Programming Tip:** Arrange catch blocks in order of specificity, catching the most specific one first. Since all exception classes have exception as an ancestor, try to avoid using exception in a catch block. If you must catch exceptions of type exception, do so in the last catch block.

### C3.4.2 Uncaught Exceptions

Let's see what happens when an exception is thrown but not caught. The program in Listing C3-5 encodes a string by doing a simple substitution. It replaces each letter in a string with the character that appears three positions later in the alphabet. When it reaches the end of the alphabet, it wraps around to the beginning. For example, a is replaced by d, b is replaced by e, and w is replaced by z. At this point, it gets replacement letters by wrapping around to the beginning of the alphabet. Thus, x is replaced by a, y is replaced by b, and z is replaced by c.

Figure C3-2 shows the flow of control when an exception occurs in this code. When the function encodeChar attempts to access the 99th character in str by the method call str.replace(99, 1, 1, newChar), an out_of_range exception is thrown. Because encodeChar does not handle the

```
LISTING C3-5 A program with an uncaught exception

#include <iostream>
#include <string>
using namespace std;

// Encodes the character at index i of the string str.
void encodeChar(int i, string& str)
{
   int base = static_cast<int>('a');
   if (isupper(str[i]))
      base = int('A');
   char newChar = (static_cast<int>(str[i]) - base + 3) % 26 + base;
   str.replace(i, 1, 1, newChar); // Method replace can throw exception
   // end encodeChar
}

// Encodes numChar characters within a string.
void encodeString(int numChar, string& str)
{
   for (int j = numChar - 1; j >= 0; j--)
      encodeChar(j, str);
} // end encodeString

int main()
{
   string str1 = "Sarah";
   encodeString(99, str1);
   return 0;
} // end main
```

### FIGURE C3-2 Flow of control for an uncaught exception

```
str             numChar
S a r a h       99

void encodeChar(int i, string& str)
{
   int base = static_cast<int>('a');
   if (isupper(str[i]))
      base = int('A');

   char newChar = (static_cast<int>(str[i]) - base + 3) % 26 + base;
   str.replace(i, 1, 1, newChar);
} // end encodeChar
```

> out_of_range exception occurs here, is not handled, so propagates back to encodeString

```
void encodeString(int numChar, string& str)
{
   for (int j = numChar-1; j >= 0; j--)
      encodeChar(j, str);
} // end encodeString
```

> out_of_range exception not handled here, so propagates back to main

```
int main()
{
   string str1 = "Sarah";
   encodeString(99, str1);
   return 0;
} // end main
```

> out_of_range exception not handled in main; causes abnormal program termination

```
Output:
abnormal program termination
```

exception, the function terminates, and the exception propagates back to encodeString at the point where encodeChar was called. The function encodeString also does not handle the exception, so it too terminates and the exception propagates back to main. Because main is the main function of the program, it does not handle the exception, and the program execution terminates abnormally with an error message.

This code contains no indication that the function encodeChar could throw the exception out_of_range. However, the documentation of encodeChar should indicate any exceptions it might throw. Thus, when documenting a function or method, you should also include any possible exceptions that could occur.

We can catch the exception out_of_range at any point in the sequence of function calls. For example, we could rewrite the function encodeChar as follows to catch the exception.

```
void encodeChar(int i, string& str)
{
   int base = static_cast<int>('a');
   if (isupper(str[i]))
      base = int('A');
```
