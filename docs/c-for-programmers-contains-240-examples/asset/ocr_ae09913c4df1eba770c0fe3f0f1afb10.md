```
33      // this statement calls getCourseName to get the
34      // name of the course this GradeBook represents
35      cout << "Welcome to the grade book for\n" << getCourseName() << "!"
36      << endl;
37  } // end function displayMessage
38 private:
39     string courseName; // course name for this GradeBook
40 }; // end class GradeBook
41
42 // function main begins program execution
43 int main()
44 {
45     string nameOfCourse; // string of characters to store the course name
46     GradeBook myGradeBook; // create a GradeBook object named myGradeBook
47
48     // display initial value of courseName
49     cout << "Initial course name is: " << myGradeBook.getCourseName()
50     << endl;
51
52     // prompt for, input and set course name
53     cout << "\nPlease enter the course name:" << endl;
54     getline( cin, nameOfCourse ); // read a course name with blanks
55     myGradeBook.setCourseName( nameOfCourse ); // set the course name
56
57     cout << endl; // outputs a blank line
58     myGradeBook.displayMessage(); // display message with new course name
59     return 0; // indicate successful termination
60 } // end main
```

Initial course name is:

Please enter the course name:
CS101 Introduction to C++ Programming

Welcome to the grade book for
CS101 Introduction to C++ Programming!

Fig. 3.5 | Defining and testing class GradeBook with a data member and set and get functions.
(Part 2 of 2.)

A typical instructor teaches multiple courses, each with its own course name. Line 39 declares that courseName is a variable of type string. Because the variable is declared in the class definition (lines 15–40) but outside the bodies of the class’s member-function definitions (lines 19–22, 25–28 and 31–37), the variable is a data member. Every instance (i.e., object) of class GradeBook contains one copy of each of the class’s data members—if there are two GradeBook objects, each has its own copy of courseName (one per object), as you’ll see in the example of Fig. 3.7. A benefit of making courseName a data member is that all the member functions of the class (in this case, class GradeBook) can manipulate any data members that appear in the class definition (in this case, courseName).

# Access Specifiers public and private

Most data-member declarations appear after the access-specifier label private: (line 38). Like public, keyword private is an access specifier. Variables or functions declared after