
displayMessage member function (line 23) to get line 15 to execute and display the welcome message. We’ll soon explain lines 22–23 in detail.

The class definition begins in line 9 with the keyword class followed by the class name GradeBook. By convention, the name of a user-defined class begins with a capital letter, and for readability, each subsequent word in the class name begins with a capital letter. This capitalization style is often referred to as camel case, because the pattern of uppercase and lowercase letters resembles the silhouette of a camel.

Every class’s body is enclosed in a pair of left and right braces ({ and }), as in lines 10 and 17. The class definition terminates with a semicolon (line 17).

## Common Programming Error 3.1

> Forgetting the semicolon at the end of a class definition is a syntax error.

Recall that main is called automatically when you execute a program. As you’ll soon see, you must call member function displayMessage explicitly to tell it to perform its task.

Line 11 contains the access-specifier label public:. The keyword public is an access specifier. Lines 13–16 define member function displayMessage. This member function appears after access specifier public: to indicate that the function is “available to the public”—it can be called by other functions in the program (such as main), and by member functions of other classes. Access specifiers are always followed by a colon (:). For the remainder of the text, when we refer to the access specifier public, we’ll omit the colon as we did in this sentence. Section 3.6 introduces a second access specifier, private.

Each function in a program performs a task and may return a value when it completes its task—for example, a function might perform a calculation, then return the result of that calculation. When you define a function, you must specify a return type to indicate the type of the value returned by the function when it completes its task. In line 13, keyword void to the left of the function name displayMessage is the function’s return type. Return type void indicates that displayMessage will not return any data to its calling function (in this example, main, as we’ll see in a moment) when it completes its task. In Fig. 3.5, you’ll see an example of a function that returns a value.

The name of the member function, displayMessage, follows the return type. By convention, function names begin with a lowercase first letter and all subsequent words in the name begin with a capital letter. The parentheses after the member function name indicate that this is a function. An empty set of parentheses, as shown in line 13, indicates that this member function does not require additional data to perform its task. You’ll see an example of a member function that does require additional data in Section 3.5. Line 13 is commonly referred to as the function header. Every function’s body is delimited by left and right braces ({ and }), as in lines 14 and 16.

The body of a function contains statements that perform the function’s task. In this case, member function displayMessage contains one statement (line 15) that displays the message "Welcome to the Grade Book!". After this statement executes, the function has completed its task.

## Common Programming Error 3.2

> Returning a value from a function whose return type has been declared void is a compilation error.

## Common Programming Error 3.3

Defining a function inside another function is a syntax error.

## Testing Class GradeBook

Next, we’d like to use class GradeBook in a program. As you learned in Chapter 2, function main (lines 20–25) begins the execution of every program.

In this program, we’d like to call class GradeBook’s displayMessage member function to display the welcome message. Typically, you cannot call a member function of a class until you create an object of that class. (As you’ll see in Section 10.7, static member functions are an exception.) Line 22 creates an object of class GradeBook called myGradeBook. Note that the variable’s type is GradeBook—the class we defined in lines 9–17. When we declare variables of type int, as we did in Chapter 2, the compiler knows what int is—it’s a fundamental type. In line 22, however, the compiler does not automatically know what type GradeBook is—it’s a user-defined type. We tell the compiler what GradeBook is by including the class definition (lines 9–17). If we omitted these lines, the compiler would issue an error message (such as “‘GradeBook’: undeclared identifier” in Microsoft Visual C++ or “‘GradeBook’: undeclared” in GNU C++). Each class you create becomes a new type that can be used to create objects. You can define new class types as needed; this is one reason why C++ is known as an extensible language.

Line 23 calls the member function displayMessage (defined in lines 13–16) using variable myGradeBook followed by the dot operator (.), the function name displayMessage and an empty set of parentheses. This call causes the displayMessage function to perform its task. At the beginning of line 23, “myGradeBook.” indicates that main should use the GradeBook object that was created in line 22. The empty parentheses in line 13 indicate that member function displayMessage does not require additional data to perform its task. (In Section 3.5, you’ll see how to pass data to a function.) When displayMessage completes its task, function main continues executing in line 24, which indicates that main performed its tasks successfully. This is the end of main, so the program terminates.

## UML Class Diagram for Class GradeBook

In the UML, each class is modeled in a UML class diagram as a rectangle with three compartments. Figure 3.2 presents a class diagram for class GradeBook (Fig. 3.1). The top compartment contains the class’s name centered horizontally and in boldface type. The middle compartment contains the class’s attributes, which correspond to data members in C++. This compartment is currently empty, because class GradeBook does not have any attributes. (Section 3.6 presents a version of class GradeBook with an attribute.) The bottom compartment contains the class’s operations, which correspond to member functions in C++. The UML models operations by listing the operation name followed by a set of parentheses. Class GradeBook has only one member function, displayMessage, so the bottom compartment of Fig. 3.2 lists one operation with this name. Member function displayMessage does not require additional information to perform its tasks, so the parentheses following displayMessage in the class diagram are empty, just as they are in the member function’s header in line 13 of Fig. 3.1. The plus sign (+) in front of the operation name indicates that displayMessage is a public operation in the UML (i.e., a public member function in C++).

```
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
    return 0; // indicate successful termination
} // end main
```

```
Please enter the course name:
CS101 Introduction to C++ Programming

Welcome to the grade book for
CS101 Introduction to C++ Programming!
```

Fig. 3.3 | Define class GradeBook with a member function that takes a parameter, create a GradeBook object and call its displayMessage function. (Part 2 of 2.)

Before discussing the new features of class GradeBook, let’s see how the new class is used in main (lines 26–40). Line 28 creates a variable of type string called nameOfCourse that will be used to store the course name entered by the user. A variable of type string represents a string of characters such as "CS101 Introduction to C++ Programming". A string is actually an object of the C++ Standard Library class string. This class is defined in header file `<string>`, and the name string, like cout, belongs to namespace std. To enable line 28 to compile, line 9 includes the `<string>` header file. Note that the using declaration in line 10 allows us to simply write string in line 28 rather than std::string. For now, you can think of string variables like variables of other types such as int. You’ll see additional string capabilities in Section 3.10.

Line 29 creates an object of class GradeBook named myGradeBook. Line 32 prompts the user to enter a course name. Line 33 reads the name from the user and assigns it to the nameOfCourse variable, using the library function getline to perform the input. Before we explain this line of code, let’s explain why we cannot simply write

```
cin >> nameOfCourse;
```
