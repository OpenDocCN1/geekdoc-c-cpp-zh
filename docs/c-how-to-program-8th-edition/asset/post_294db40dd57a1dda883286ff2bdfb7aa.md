
that will be used to store the course name entered by the user. A variable of type `string` represents a string of characters such as “CS101 Introduction to C++ Programming”. A string is actually an *object* of the C++ Standard Library class `string`. This class is defined in header `<string>`, and the name `string`, like `cout`, belongs to namespace `std`. To enable lines 13 and 23 to compile, line 5 includes the `<string>` header. The using directive in line 6 allows us to simplify writing `string` in line 23 rather than `std::string`. For now, you can think of string variables like variables of other types such as `int`. You’ll learn additional string capabilities in Section 3.8 and in Chapter 18.

Line 24 creates an object of class GradeBook named myGradeBook. Line 27 prompts the user to enter a course name. Line 28 reads the name from the user and assigns it to the nameOfCourse variable, using the library function `getline` to perform the input. Before we explain this line of code, let’s explain why we cannot simply write

```cpp
cin >> nameOfCourse;
```

to obtain the course name. In our sample program execution, we use the course name “CS101 Introduction to C++ Programming,” which contains multiple words separated by blanks. (Recall that we highlight user-supplied input in bold.) When `cin` is used with the stream extraction operator, it reads characters *until the first white-space character is reached*. Thus, only “CS101” would be read by the preceding statement. The rest of the course name would have to be read by subsequent input operations.

In this example, we’d like the user to type the complete course name and press *Enter* to submit it to the program, and we’d like to store the entire course name in the string variable nameOfCourse. The function call `getline( cin, nameOfCourse )` in line 28 reads characters (*including* the space characters that separate the words in the input) from the standard input stream object `cin` (i.e., the keyboard) until the newline character is encountered, places the characters in the string variable nameOfCourse and *discards* the newline character. When you press *Enter* while typing your program input, a newline is inserted in the input stream. The `<string>` header must be included in the program to use function getline, which belongs to namespace std.

Line 33 calls myGradeBook’s displayMessage member function. The nameOfCourse variable in parentheses is the *argument* that’s passed to member function displayMessage so that it can perform its task. The value of variable nameOfCourse in main is copied to member function displayMessage’s parameter courseName in line 13. When you execute this program, member function displayMessage outputs as part of the welcome message the course name you type in (our sample execution, CS101 Introduction to C++ Programming).

## More on Arguments and Parameters

To specify in a function definition that the function requires data to perform its task, you place additional information in the function’s *parameter list*, which is located in the parentheses following the function name. The parameter list may contain any number of parameters, including none at all (represented by an empty pair of parentheses as in Fig. 3.1, line 12) to indicate that a function does *not* require any parameters. Member function displayMessage’s parameter list (Fig. 3.3, line 13) declares that the function requires one parameter. Each parameter is specified as a *type* and an *identifier*. The type string and the identifier courseName indicate that member function displayMessage requires a string to perform its task. The member function body uses the parameter courseName to access the value that’s passed to the function in the function call (line 33 in main). Lines 15–16 display parameter courseName’s value as part of the welcome message.

The parameter variable’s name (courseName in line 13) can be the same as or different from the argument variable’s name (nameOfCourse in line 33)—you’ll learn why in Chapter 6.

A function can specify multiple parameters by separating each from the next with a comma. The number and order of arguments in a function call must match the number and order of parameters in the parameter list of the called member function’s header. Also, the argument types in the function call must be consistent with the types of the corresponding parameters in the function header. (As you’ll learn in subsequent chapters, an argument’s type and its corresponding parameter’s type need not always be identical, but they must be “consistent.”) In our example, the one string argument in the function call (i.e., nameOfCourse) exactly matches the one string parameter in the member-function definition (i.e., courseName).

### Updated UML Class Diagram for Class GradeBook

The UML class diagram of Fig. 3.4 models class GradeBook of Fig. 3.3. Like the class GradeBook defined in Fig. 3.1, this GradeBook class contains public member function displayMessage. However, this version of displayMessage has a parameter. The UML models a parameter by listing the parameter name, followed by a colon and the parameter type in the parentheses following the operation name. The UML has its own data types similar to those of C++. The UML is language independent—it’s used with many different programming languages—so its terminology does not exactly match that of C++. For example, the UML type String corresponds to the C++ type string. Member function displayMessage of class GradeBook (Fig. 3.3, lines 13–17) has a string parameter named courseName, so Fig. 3.4 lists courseName : String between the parentheses following the operation name displayMessage. This version of the GradeBook class still does not have any data members.

![](img/bfd978e7e9b192bab46ec2a89e481263_104_0.png)

**Fig. 3.4** | UML class diagram indicating that class GradeBook has a public displayMessage operation with a courseName parameter of UML type String.

## 3.4 Data Members, set Functions and get Functions

In Chapter 2, we declared all of a program’s variables in its main function. Variables declared in a function definition’s body are known as local variables and can be used only from the line of their declaration in the function to closing right brace (}) of the block in which they’re declared. A local variable must be declared before it can be used in a function. A local variable cannot be accessed outside the function in which it’s declared. When a function terminates, the values of its local variables are lost. (You’ll see an exception to this in Chapter 6 when we discuss static local variables.)

A class normally consists of one or more member functions that manipulate the attributes that belong to a particular object of the class. Attributes are represented as variables in a class definition. Such variables are called **data members** and are declared inside a class definition but *outside* the bodies of the class’s member-function definitions. Each object of a class maintains its own copy of its attributes in memory. These attributes exist throughout the life of the object. The example in this section demonstrates a GradeBook class that contains a courseName data member to represent a particular GradeBook object’s course name.

### GradeBook Class with a Data Member, a set Function and a get Function

In our next example, class GradeBook (Fig. 3.5) maintains the course name as a *data member* so that it can be used or modified at any time during a program’s execution. The class contains member functions setCourseName, getCourseName and displayMessage. Member function setCourseName stores a course name in a GradeBook data member. Member function getCourseName obtains the course name from that data member. Member function displayMessage—which now has no parameters—still displays a welcome message that includes the course name. However, as you’ll see, the function now obtains the course name by calling another function in the same class—getCourseName.

```cpp
// Fig. 3.5: Fig03_05.cpp
// Define class GradeBook that contains a courseName data member
// and member functions to set and get its value.
// Create and manipulate a GradeBook object with these functions.
#include <iostream>
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
   // function that sets the course name
   void setCourseName( string name )
   {
      courseName = name; // store the course name in the object
   } // end function setCourseName

   // function that gets the course name
   string getCourseName()
   {
      return courseName; // return the object's courseName
   } // end function getCourseName

   // function that displays a welcome message
   void displayMessage()
   {
      // this statement calls getCourseName to get the
      // name of the course this GradeBook represents
      cout << "Welcome to the grade book for\n" << getCourseName() << "!"
           << endl;
   } // end function displayMessage
```

**Fig. 3.5** | Defining and testing class *GradeBook* with a data member and *set* and *get* functions. (Part 1 of 2.)
