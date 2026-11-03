
## Introduction to Classes, Objects and Strings

## 16

## Objectives

In this chapter you'll learn:

- How to define a class and use it to create an object.
- How to implement a class's behaviors as member functions.
- How to implement a class's attributes as data members.
- How to call a member function of an object to perform a task.
- The differences between data members of a class and local variables of a function.
- How to use a constructor to initialize an object's data when the object is created.
- How to engineer a class to separate its interface from its implementation and encourage reuse.
- How to use objects of class string.

// GradeBook class definition
class GradeBook
{
public:
    // function that displays a welcome message to the GradeBook user
    void displayMessage() const
    {
        cout << "Welcome to the Grade Book!" << endl;
    } // end function displayMessage
}; // end class GradeBook

// function main begins program execution
int main()
{
    GradeBook myGradeBook; // create a GradeBook object named myGradeBook
    myGradeBook.displayMessage(); // call object's displayMessage function
} // end main

Welcome to the Grade Book!

Fig. 16.1 | Define class GradeBook with a member function displayMessage, create a GradeBook object and call its displayMessage function. (Part 2 of 2.)

## Class GradeBook

Before function main (lines 19–23) can create a GradeBook object, we must tell the compiler what member functions and data members belong to the class. The GradeBook class definition (lines 8–16) contains a member function called displayMessage (lines 12–15) that displays a message on the screen (line 14). We need to make an object of class GradeBook (line 21) and call its displayMessage member function (line 22) to get line 14 to execute and display the welcome message. We’ll soon explain lines 21–22 in detail.

The class definition begins in line 8 with the keyword class followed by the class name GradeBook. By convention, the name of a user-defined class begins with a capital letter, and for readability, each subsequent word in the class name begins with a capital letter. This capitalization style is often referred to as Pascal case, because the convention was widely used in the Pascal programming language. The occasional uppercase letters resemble a camel’s humps. More generally, camel case capitalization style allows the first letter to be either lowercase or uppercase (e.g., myGradeBook in line 21).

Every class’s body is enclosed in a pair of left and right braces ({ and }), as in lines 9 and 16. The class definition terminates with a semicolon (line 16).

> Common Programming Error 16.1
> Forgetting the semicolon at the end of a class definition is a syntax error.

Recall that the function main is always called automatically when you execute a program. Most functions do not get called automatically. As you’ll soon see, you must call member function displayMessage explicitly to tell it to perform its task.

These lines, the compiler would issue an error message. Each class you create becomes a new *type* that can be used to create objects. You can define new class types as needed; this is one reason why C++ is known as an *extensible programming language*.

Line 22 calls the member function *displayMessage* using variable *myGradeBook* followed by the dot operator (.), the function name *displayMessage* and an empty set of parentheses. This call causes the *displayMessage* function to perform its task. At the beginning of line 22, “*myGradeBook*.” indicates that *main* should use the *GradeBook* object that was created in line 21. The *empty parentheses* in line 12 indicate that member function *displayMessage* *does not require additional data* to perform its task, which is why we called this function with empty parentheses in line 22. (In Section 16.3, you’ll see how to pass data to a function.) When *displayMessage* completes its task, the program reaches the end of *main* (line 23) and terminates.

### UML Class Diagram for Class GradeBook

Recall from Section 15.13 that the UML is a standardized graphical language used by software developers to represent their object-oriented systems. In the UML, each class is modeled in a UML class diagram as a rectangle with three compartments. Figure 16.2 presents a class diagram for class *GradeBook* (Fig. 16.1). The *top compartment* contains the class’s name centered horizontally and in boldface type. The *middle compartment* contains the class’s attributes, which correspond to data members in C++. This compartment is currently empty, because class *GradeBook* does not yet have any attributes. (Section 16.4 presents a version of class *GradeBook* with an attribute.) The *bottom compartment* contains the class’s operations, which correspond to member functions in C++. The UML models operations by listing the operation name followed by a set of parentheses. Class *GradeBook* has only one member function, *displayMessage*, so the bottom compartment of Fig. 16.2 lists one operation with this name. Member function *displayMessage* *does not require additional information* to perform its task, so the parentheses following *displayMessage* in the class diagram are *empty*, just as they are in the member function’s header in line 12 of Fig. 16.1. The *plus sign (+)* in front of the operation name indicates that *displayMessage* is a *public* operation in the UML (i.e., a *public* member function in C++).

![](img/bf54db922e6fa8319cba11069e785521_619_0.png)

**Fig. 16.2** | UML class diagram indicating that class *GradeBook* has a *public* *displayMessage* operation.

## 16.3 Defining a Member Function with a Parameter

In our car analogy from Section 1.8, we mentioned that pressing a car’s gas pedal sends a *message* to the car to perform a *task*—make the car go faster. But *how fast* should the car accelerate? As you know, the farther down you press the pedal, the faster the car accelerates. So the message to the car includes both the *task to perform* and *additional information that helps the car perform the task*. This additional information is known as a *parameter*— the *value* of the parameter helps the car determine how fast to accelerate. Similarly, a member function can require one or more parameters that represent additional data it needs to perform its task. A function call supplies values—called *arguments*—for each of the function's parameters. For example, to make a deposit into a bank account, suppose a deposit member function of an Account class specifies a parameter that represents the *deposit amount*. When the deposit member function is called, an argument value representing the deposit amount is copied to the member function's parameter. The member function then adds that amount to the account balance.

### Defining and Testing Class GradeBook

Our next example (Fig. 16.3) redefines class GradeBook (lines 9–18) with a `displayMessage` member function (lines 13–17) that displays the course name as part of the welcome message. The new version of `displayMessage` requires a *parameter* (`courseName` in line 13) that represents the course name to output.

~~~cpp
// Fig. 16.3: fig16_03.cpp
// Define class GradeBook with a member function that takes a parameter,
// create a GradeBook object and call its displayMessage function.
#include <iostream>
#include <string> // program uses C++ standard string class
using namespace std;

// GradeBook class definition
class GradeBook
{
public:
    // function that displays a welcome message to the GradeBook user
    void displayMessage( string courseName ) const
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
~~~

**Fig. 16.3** | Define class GradeBook with a member function that takes a parameter, create a GradeBook object and call its `displayMessage` function. (Part 1 of 2.)
