ber function can require one or more parameters that represent additional data it needs to perform its task. A function call supplies values—called **arguments**—for each of the function’s parameters. For example, to make a deposit into a bank account, suppose a deposit member function of an Account class specifies a parameter that represents the *deposit amount*. When the deposit member function is called, an argument value representing the deposit amount is copied to the member function’s parameter. The member function then adds that amount to the account balance.

# Defining and Testing Class GradeBook

Our next example (Fig. 3.3) redefines class GradeBook (lines 9–18) with a displayMessage member function (lines 13–17) that displays the course name as part of the welcome message. The new version of the displayMessage requires a *parameter* (courseName in line 13) that represents the course name to output.

```
// Fig. 3.3: fig03_03.cpp
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

   // prompt for and input course
   cout << "Please enter the course name:" << endl;
   getline( cin, nameOfCourse ); // read a course name with blanks
   cout << endl; // output a blank line

   // call myGradeBook's displayMessage function
   // and pass nameOfCourse as an argument
   myGradeBook.displayMessage( nameOfCourse );
} // end main
```

**Fig. 3.3** | Define class GradeBook with a member function that takes a parameter, create a GradeBook object and call its displayMessage function. (Part 1 of 2.)