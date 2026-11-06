
The class definition begins in line 8 with the keyword class followed by the class name GradeBook. By convention, the name of a user-defined class begins with a capital letter, and for readability, each subsequent word in the class name begins with a capital letter. This capitalization style is often referred to as camel case, because the pattern of uppercase and lowercase letters resembles the silhouette of a camel.

Every class’s body is enclosed in a pair of left and right braces ({ and }), as in lines 9 and 16. The class definition terminates with a semicolon (line 16).

> **Common Programming Error 3.1**
>
> *Forgetting the semicolon at the end of a class definition is a syntax error.*

Recall that the function main is always called automatically when you execute a program. Most functions do not get called automatically. As you’ll soon see, you must call member function displayMessage explicitly to tell it to perform its task.

Line 10 contains the access-specifier label public:. The keyword public is an access specifier. Lines 12–15 define member function displayMessage. This member function appears after access specifier public: to indicate that the function is “available to the public”—that is, it can be called by other functions in the program (such as main), and by member functions of other classes (if there are any). Access specifiers are always followed by a colon (:). For the remainder of the text, when we refer to the access specifier public, we’ll omit the colon as we did in this sentence. Section 3.5 introduces a second access specifier, private. Later in the book we’ll study the access specifier protected.

Each function in a program performs a task and may return a value when it completes its task—for example, a function might perform a calculation, then return the result of that calculation. When you define a function, you must specify a return type to indicate the type of the value returned by the function when it completes its task. In line 12, keyword void to the left of the function name displayMessage is the function’s return type. Return type void indicates that displayMessage will *not* return (i.e., give back) any data to its calling function (in this example, main, as we’ll see in a moment) when it completes its task. In Fig. 3.5, you’ll see an example of a function that returns a value.

The name of the member function, displayMessage, follows the return type. By convention, function names begin with a lowercase first letter and all subsequent words in the name begin with a capital letter. The parentheses after the member function name indicate that this is a function. An empty set of parentheses, as shown in line 12, indicates that this member function does not require additional data to perform its task. You’ll see an example of a member function that does require additional data in Section 3.4. Line 12 is commonly referred to as the function header. Every function’s body is delimited by left and right braces ({ and }), as in lines 13 and 15.

The body of a function contains statements that perform the function’s task. In this case, member function displayMessage contains one statement (line 14) that displays the message "Welcome to the Grade Book!". After this statement executes, the function has completed its task.

> **Common Programming Error 3.2**
>
> *Returning a value from a function whose return type has been declared void is a compilation error.*

```cpp
// Fig. 3.3: fig03_03.cpp
// Define a GradeBook with a member function that takes a parameter;
// Create a GradeBook object and call its displayMessage function.
#include <iostream>
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
   // function that displays a welcome message to the GradeBook user
   void displayMessage( string courseName )
   {
      cout << "Welcome to the grade book for\n" << courseName << "!"
           << endl;
   } // end function displayMessage
}; // end class GradeBook

// function main begins program execution
int main()
{
   string nameOfCourse; // string of characters to store the course name
   GradeBook myGradeBook; // create a GradeBook object named myGradeBook

   // prompt for and input course name
   cout << "Please enter the course name:" << endl;
   getline( cin, nameOfCourse ); // read a course name with blanks
   cout << endl; // output a blank line

   // call myGradeBook's displayMessage function
   // and pass nameOfCourse as an argument
   myGradeBook.displayMessage( nameOfCourse );
} // end main
```

**Fig. 3.3** | Define class GradeBook with a member function that takes a parameter, create a GradeBook object and call its displayMessage function.

to obtain the course name. In our sample program execution, we use the course name “CS101 Introduction to C++ Programming,” which contains multiple words. (Recall that we highlight user-supplied input in bold.) When cin is used with the stream extraction operator, it reads characters until the first white-space character is reached. Thus, only “CS101” would be read by the preceding statement. The rest of the course name would have to be read by subsequent input operations.

In this example, we’d like the user to type the complete course name and press Enter to submit it to the program, and we’d like to store the entire course name in the string variable nameOfCourse. The function call `getline(cin, nameOfCourse)` in line 28 reads characters (including the space characters that separate the words in the input) from the standard input stream object `cin` (i.e., the keyboard) until the newline character is encountered, places the characters in the string variable `nameOfCourse` and discards the newline character. When you press *Enter* while typing program input, a newline is inserted in the input stream. Also, the `<string>` header file must be included in the program to use function `getline` and that the name `getline` belongs to namespace `std`.

Line 33 calls `myGradeBook`’s `displayMessage` member function. The `nameOfCourse` variable in parentheses is the argument that is passed to member function `displayMessage` so that it can perform its task. The value of variable `nameOfCourse` in `main` becomes the value of member function `displayMessage`’s parameter `courseName` in line 13. When you execute this program, member function `displayMessage` outputs as part of the welcome message the course name you type (in our sample execution, CS101 Introduction to C++ Programming).

### More on Arguments and Parameters

To specify that a function requires data to perform its task, you place additional information in the function’s parameter list, which is located in the parentheses following the function name. The parameter list may contain any number of parameters, including none at all (represented by empty parentheses as in Fig. 3.1, line 12) to indicate that a function does not require any parameters. Member function `displayMessage`’s parameter list (Fig. 3.3, line 13) declares that the function requires one parameter. Each parameter must specify a type and an identifier. In this case, the type `string` and the identifier `courseName` indicate that member function `displayMessage` requires a string to perform its task. The member function body uses the parameter `courseName` to access the value that is passed to the function in the function call (line 33 in `main`). Lines 15–16 display parameter `courseName`’s value as part of the welcome message. The parameter variable’s name (line 13) can be the same as or different from the argument variable’s name (line 33)—you’ll learn why in Chapter 6, Functions and an Introduction to Object-Oriented Programming.

A function can specify multiple parameters by separating each parameter from the next with a comma (we’ll see an example in Figs. 6.4–6.5). The number and order of arguments in a function call must match the number and order of parameters in the parameter list of the called function’s header. Also, the argument types in the function call must be consistent with the types of the corresponding parameters in the function header. (As you’ll learn in subsequent chapters, an argument’s type and its corresponding parameter’s type need not always be identical, but they must be “consistent.”) In our example, the one `string` argument in the function call (i.e., `nameOfCourse`) exactly matches the one `string` parameter in the member-function definition (i.e., `courseName`).

> **Common Programming Error 3.4**
>
> Placing a semicolon after the right parenthesis enclosing the parameter list of a function definition is a syntax error.

> **Common Programming Error 3.5**
>
> Defining a function parameter again as a variable in the function’s body is a compilation error.
