
## L.2 Comparison of Language Elements

When it comes to writing a C++ program, there are several important differences you need to keep in mind.

**Comments.** Comments are an important part of any program, and C++ supports single and multi-line comments with different delimiters:

```
// This is a comment that appears on its own line.
int sum = 0; // This is a comment that appears within a C++ statement.
// The following comment begins with /* and ends with */.
/* This is a special multiline comment used for documentation systems
such as doxygen. See Appendix I for details. */
// The following comment begins with /* and ends with */.
/* This is a multiline comment that is often used to temporarily
disable a group of statements debugging. */
```

**Statements.** Whitespace and indentation in C++ have no significance. C++ statements end with a semicolon. Statements in a block, known as a compound statement, are analogous to a suite in Python and are grouped by braces { }.

**Variables.** In Python, a variable can be defined as soon as it is assigned a value. Variables in C++ must be declared before they can be used. also be given an initial value before being used. Once a variable has been declared with a given type, its type persists throughout the scope in which it was declared.

**Relational operators.** Relational operators in C++ can be used only with one relational operator at a time. Python expressions such as x < 5 must be written as (x < 5) && (x < 10) in C++. The operator && is used for a logical AND, and || is for a logical OR.

**Predicate expressions.** Predicate expressions in conditional and iteration flow-control statements must be in parentheses.

**Assignment statements.** Multiple assignment is not allowed in C++. Python statements such as x,y = 5, 6 cannot be used.

**Iteration statements.** C++ has a while statement that behaves like the Python while statement. The C++ for statement is a special case of the while statement. To use a C++ for statement as you would use a Python for, you must use iterators, which are explained in C++ Iterate 6. C++ has a do-while statement, which is a post-test loop. Python has no equivalent.

**Basic input.** In a Python application, you use the raw_input function to accept input from the keyboard. If you need an integer or a value of some other type, you must use another function to transform the string into the desired input. Output to the display is accomplished by calling the print function. For example, the following code displays a prompt for the user, accepts a response as an integer, and echoes the response back to the user:

```
userNumber = int (raw_input("How many apples are in a box?"))
print("You %d apples per box."%(userNumber))
```

C++ uses two objects, cin and cout, for keyboard input and console output, respectively. To use cin and cout, you should include the following statements at the start of your program:

```
#include <iostream>
using namespace std;
```

The "C++ statements that are equivalent to the previous Python statements:

```cpp
cout << "How many apples are in a box?";
int applesPerBox = 0;
cin >> applesPerBox;
cout << "You entered " << applesPerBox << " apples box." << endl;
```

Note the use of the output stream operator << to send strings and variables to the output object. Similarly, the input stream operator >> sends input from the input object cin to a variable. It is easy to remember which operator to use if you imagine them as arrows pointing in the direction of the data flow.

The constant endl is defined in iostream and represents the new-line character. Additional information about the iostream library and basic input and output in C++ is in Section A.2 of Appendix A.

Example. Listing L-1 gives a short interactive Python program using the statements and expressions just discussed. Listing L-2 shows the equivalent program in C++. C++ programs begin execution at the main function. You can see some of the differences in input and output in this example also.

LISTING L-1 Short Python program to test and modify a user-entered value
```python
small, large = 1, 1000
print "Your number was between %d and %ld large." %%(small, large)
userName = int(raw_input("Enter something: "))
if small < userName:
    print "Your number was between %d and %ld large." %%(small, large)
elif userName < small:
    while userName <= small:
        userName = userName + 1
else:
    while True:
        userName = userName
        if userName < 1000:
            break
        print "I fixed your number to be between %d and %d!" %%(small, large)
```

LISTING L-2 Short C++ program equivalent to the Python program in Listing L-1.
```cpp
#include <iostream>
using namespace std;
int main() 
{
    int small = 1;
    int large = 1000;
    int userName = 0;
    cout << "Enter something: ";
    cin >> userName;
if ( small < userName) && (userName < large) ) {
    cout << "Your number was between " << small << " and ";
    cout << large << endl;
}
else if (userName < 1) {
    while (userName <= 1) {
        userName++;
    }
}
else {
    do {
        userName--;
    } while (userName >= small && userName <= 1000);
    cout << "I fixed your number to be between " << small << " and ";
    cout << large << endl;
}
}
```

## L.3 Functions

As its variables, C++ functions are strongly typed. When a C++ function is defined, the parameters are given a type. If a function returns a value, the function must indicate the type of the return value. Information is given in the header, the first line, of the function. If a function does not return a value, its return type is void. The definition of the function follows the header and is enclosed in { }, as in other C++ blocks.

Here is a Python function that cubes the cube of its single parameter:

```python
def realCube(x) :
    return x * x * x
```

Here is the equivalent C++ function:

```cpp
double realCube(double x) {
    return x * x * x;
}
```

Notice that the function in C++ is given a type. In Python, the function does not have a return type. However, in C++, the return type is specified in the header. If a function does not return a value, its return type is void. The header of the function is followed by a semicolon—that is, its prototype—at the beginning of the program. For example, the prototype of the function is:

```cpp
double realCube(double x);
```

Then you can place the function definition anywhere within your program. In large programs, function prototypes are placed into one or more header files, as described in Section A.2 of Appendix. Prototypes are also important in the creation of classes, as you will see in the next section.

## L.4 Classes

Python classes permit clients of the classes to access all data and methods. In C++, this is called public access and is recommended only for methods. In Python, when you create a class member that should be used only by methods, you typically prefix the member's name with underscores. This convention is only a signal to the programmer; the interpreter does not enforce it. C++ restricts direct access to certain data fields and methods by labeling them private, and the compiler enforces this by permitting only methods to access them.

Classes in C++ have constructors that are similar to the __init__ method. When writing a method in a Python class, you prefix the names of data fields by self to indicate that they are instance variables of the class. Instance variables in a C++ class do not need a special prefix, if they are referenced within a method of the class.

Here is a simple Python class, PlainBox:

```python
class PlainBox
def __init__(self, item):
    self.item = item

def setItem(self, item):
    self.item = item

def getItem(self):
    return self.item
```

You can also define the same class in a form that is closer to that of a C++ class:

```python
class PlainBox:
    item = ""

    def __init__(self, item):
        self.item = item

    def setitem(self, item):
        self.item = item
def getItem(self):
        return self.item
```
