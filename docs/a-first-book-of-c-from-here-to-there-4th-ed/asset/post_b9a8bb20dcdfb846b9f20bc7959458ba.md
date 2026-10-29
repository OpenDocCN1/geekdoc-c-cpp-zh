
## Figure 1.10 The main() function directs all other functions

![](img/e9bf940282dfb289356f077151cc69dd_35_0.png)

## Figure 1.11 The structure of a main() function

![](img/e9bf940282dfb289356f077151cc69dd_35_1.png)

The keyword before the function name defines the type of value the function returns when it has finished operating. When placed before the function's name, the keyword int (listed in Table 1.1), for example, means the function returns an integer value. Similarly, empty parentheses following the function name indicate that no data is transmitted to the function when it runs. (Data transmitted to a function at runtime is referred to as an argument of the function.) The braces, { and }, determine the beginning and end of the function body and enclose the statements making up the function.

You'll be naming and writing many of your own C++ functions. In fact, the rest of Part I is primarily about the statements required to construct useful functions and how to combine functions and data into useful programs. Each program, however, must have one and only one main() function. Until you learn how to pass data to a function and return data from a function

(the topics of Chapter 6), the header line shown in Figure 1.11 serves for all the programs you need to write. Until they're explained more fully, simply regard the first two lines

```
int main()
{

```

as indicating "the program begins here," and regard the last two lines

```
return 0;
}
```

as designating the end of the program. Fortunately, many useful functions and classes have already been written for you. Next, you see how to use an object created from one of these classes to create your first working C++ program.

## Point of Information

## Executable and Nonexecutable Statements

You'll be introduced to many C++ statements in this book that can be used to create functions and programs. All statements in a function, however, belong to two broad categories: executable statements and nonexecutable statements.

An executable statement causes the computer to perform some specific action when the program runs. For example, a statement telling the computer to display output or add numbers is an executable statement. Executable statements must always end with a semicolon.

A nonexecutable statement describes some feature of the program or its data but doesn't cause the computer to perform any action when a program runs. An example of a nonexecutable statement is a comment (described in Section 1.4). A comment is intended for use by anyone reading the program. The compiler ignores all comments when it translates source code.

The statements inside the braces determine what the function does. All statements causing the computer to perform a specific action when the function is executed must end with a semicolon (;). These statements are executable statements and are described in more detail as you progress in your understanding of C++.

## EXERCISES 1.2

1. (Practice) State whether the following are valid identifiers and if so, whether they're mnemonic names that convey some idea of their purpose. If the identifier names are invalid, state why.

- lm1234    newBal    abcd    A12345    1A2345
- power    absVal    invoices    do    while
- add_5    taxes    netPay    12345    int
- newBalance    a2b3c4d5    sales_tax    amount    $taxes

2. (Practice) Assume the following functions have been written:
getLength(), getWidth(), calcArea(), displayArea()
a. Based on their names, what do you think each function might do?
b. In what order do you think a main() function might execute these functions (based on their names)?

3. (Practice) Assume the following functions have been written:
inputPrice(), calcSalestax(), calcTotal()
a. Based on their names, what do you think each function might do?
b. In what order do you think a main() function might execute these functions (based on their names)?

4. (Practice) Determine names for functions that do the following:
a. Find the average of a set of numbers.
b. Find the area of a rectangle.
c. Find the circumference of a circle.
d. Find the maximum value in a set of numbers.
e. Convert an uppercase letter to a lowercase letter.
f. Sort a set of numbers from lowest to highest.
g. Alphabetize a list of names.

5. (Practice) Just as the keyword int can be used to signify that a function returns an integer, the keywords void, char, float, and double can be used to signify that a function returns no value, a character, a floating-point number, and a double-precision number, respectively. Using this information, write header lines for a function named abs() that receives no arguments but returns the following:
a. No value
b. A character
c. A floating-point number
d. A double-precision number

## 1.3 The cout Object

One of the most versatile and commonly used objects in C++ is cout (pronounced "see out" and derived from console output). It's an output object that sends whatever data is passed to it to the standard display device, which is a computer screen in most systems. For example, if the data Hello there world! is passed to cout, this data is printed (displayed) on your screen.

To pass this data to the cout object, simply place the insertion symbol, <<, after the object's name and before the message, as shown:

cout << "Hello there world!"

Now try putting all this together. Take a look at Program 1.1, which is a working C++ program that can be run on your computer.

## Program 1.1

```
#include <iostream>
using namespace std;

int main()
{
    cout << "Hello there world!";

    return 0;
}
```

The first line of the program is a preprocessor command that uses the reserved word `include`:

`#include <iostream>`

**Preprocessor commands** begin with a pound sign (#) and perform some action before the compiler translates the source program into machine code. Specifically, the #include preprocessor command causes the contents of the named file—in this case, iostream—to be inserted wherever the #include command appears in the program. The iostream file is part of the standard library that contains, among other code, two classes: istream and ostream. These two classes provide data declarations and methods used for data input and output, respectively. The iostream file is called a **header file** because a reference to it is always placed at the top, or head, of a C++ program by using the #include command. You might be wondering what the iostream file has to do with this simple program. The answer is that the cout object is created from the ostream class. Therefore, the iostream header file must be included in all programs using cout. As shown in Program 1.1, preprocessor commands don’t end with a semicolon.

Following the preprocessor #include command is a statement containing the reserved word using. The following statement, for example, tells the compiler where to find header files in the absence of an explicit designation:

`using namespace std;`

You can think of a **namespace** as a file the compiler accesses when it’s looking for prewritten classes or functions. Because the iostream header file is contained in a file named std (for the standard library), the compiler automatically uses iostream’s cout object from this namespace whenever cout is referenced.⁷ By using namespaces, you can create your own classes and functions with the same names the standard library provides and place them in differently named namespaces. You can then tell the program which class or function to use by specifying the namespace where you want the compiler to look for the class or function.

The using statement is followed by the start of the program’s main() function, which begins with the header line described previously. The body of the function, enclosed in braces,

consists of only two statements. The first statement in main() sends one message to the cout object: the string "Hello there world!".

Because cout is an object of a prewritten class, you don't have to create it; it's available for use just by activating it correctly. Like all C++ objects, cout can perform only certain well-defined actions. For cout, this action is to assemble data for output display. When a string of characters is passed to cout, the object makes sure the string is displayed onscreen correctly, as shown in this output from Program 1.1:

```
Hello there world!
```

Strings in C++ are any combination of letters, numbers, and special characters enclosed in quotation marks ("string in here"). The quotation marks are used to delimit (mark) the beginning and ending of the string and aren't considered part of the string. Therefore, the string of characters making up the message sent to cout must be enclosed in quotation marks, as was done in Program 1.1.

Now examine another program to understand cout's versatility. Read Program 1.2 to determine what it does.

## Program 1.2

```
#include <iostream>
using namespace std;

int main()
{
    cout << "Computers, computers everywhere";
    cout << "\n  as far as I can C";

    return 0;
}
```
