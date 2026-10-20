Just as we can use object System.out to call its methods print, printf and println, we can use object myGradeBook to call its method displayMessage. Line 13 calls the method displayMessage (lines 7–10 of Fig. 3.1) using myGradeBook followed by a dot separator (.), the method name displayMessage and an empty set of parentheses. This call causes the displayMessage method to perform its task. This method call differs from those in Chapter 2 that displayed information in a command window—each of those method calls provided arguments that specified the data to display. At the beginning of line 13, “myGradeBook.” indicates that main should use the myGradeBook object that was created in line 10. Line 7 of Fig. 3.1 indicates that method displayMessage has an empty parameter list—that is, displayMessage does not require additional information to perform its task. For this reason, the method call (line 13 of Fig. 3.2) specifies an empty set of parentheses after the method name to indicate that no arguments are being passed to method displayMessage. When method displayMessage completes its task, method main continues executing at line 14. This is the end of method main, so the program terminates.

Any class can contain a main method. The JVM invokes the main method only in the class used to execute the application. If an application has multiple classes that contain main, the one that’s invoked is the one in the class named in the java command.

# Compiling an Application with Multiple Classes

You must compile the classes in Fig. 3.1 and Fig. 3.2 before you can execute the application. First, change to the directory that contains the application’s source-code files. Next, type the command

```
javac GradeBook.java GradeBookTest.java
```

to compile both classes at once. If the directory containing the application includes only this application’s files, you can compile all the classes in the directory with the command

```
javac *.java
```

The asterisk (*) in *.java indicates that all files in the current directory that end with the file-name extension “.java” should be compiled.

# UML Class Diagram for Class GradeBook

Figure 3.3 presents a UML class diagram for class GradeBook of Fig. 3.1. In the UML, each class is modeled in a class diagram as a rectangle with three compartments. The top compartment contains the name of the class centered horizontally in boldface type. The middle compartment contains the class’s attributes, which correspond to instance variables (discussed in Section 3.4) in Java. In Fig. 3.3, the middle compartment is empty, because this GradeBook class does not have any attributes. The bottom compartment contains the

![](bbox=[0.35, 0.81, 0.65, 0.89])

Fig. 3.3 | UML class diagram indicating that class GradeBook has a public displayMessage operation.