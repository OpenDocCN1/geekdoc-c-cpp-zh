```
16      // display initial value of courseName
17      System.out.printf( "Initial course name is: %s\n\n",
18          myGradeBook.getCourseName() );
19
20      // prompt for and read course name
21      System.out.println( "Please enter the course name:" );
22      String theName = input.nextLine(); // read a line of text
23      myGradeBook.setCourseName( theName ); // set the course name
24      System.out.println(); // outputs a blank line
25
26      // display welcome message after specifying course name
27      myGradeBook.displayMessage();
28      } // end main
29      } // end class GradeBookTest
```

```
Initial course name is: null
Please enter the course name:
CS101 Introduction to Java Programming
Welcome to the grade book for
CS101 Introduction to Java Programming!
```

Fig. 3.8 | Creating and manipulating a GradeBook object. (Part 2 of 2.)

# set and get Methods

A class’s private fields can be manipulated only by the class’s methods. So a client of an object—that is, any class that calls the object’s methods—calls the class’s public methods to manipulate the private fields of an object of the class. This is why the statements in method main (Fig. 3.8) call the setCourseName, getCourseName and displayMessage methods on a GradeBook object. Classes often provide public methods to allow clients to set (i.e., assign values to) or get (i.e., obtain the values of) private instance variables. The names of these methods need not begin with set or get, but this naming convention is recommended and is convention for special Java software components called JavaBeans, which can simplify programming in many Java integrated development environments (IDEs). The method that sets instance variable courseName in this example is called setCourseName, and the method that gets its value is called getCourseName.

# GradeBook UML Class Diagram with an Instance Variable and set and get Methods

Figure 3.9 contains an updated UML class diagram for the version of class GradeBook in Fig. 3.7. This diagram models class GradeBook’s instance variable courseName as an attribute in the middle compartment of the class. The UML represents instance variables as attributes by listing the attribute name, followed by a colon and the attribute type. The UML type of attribute courseName is String. Instance variable courseName is private in Java, so the class diagram lists a minus sign (-) access modifier in front of the corresponding attribute’s name. Class GradeBook contains three public methods, so the class diagram lists three operations in the third compartment. Recall that the plus sign (+) before each operation name indicates that the operation is public. Operation setCourseName has a String parameter called name. The UML indicates the return type of an operation by placing a colon and the return type after the parentheses following the operation name. Method getCourseName of class GradeBook (Fig. 3.7) has a String return type in Java, so the