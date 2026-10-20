
Book. To help you prepare for the larger programs you’ll encounter later in this book and in industry, we use a separate class (GradeBookTest in this example) containing method main to test each new class we create in this chapter. Some programmers refer to such a class as a driver class.

The GradeBookTest class declaration (Fig. 3.2) contains the main method that will control our application’s execution. The GradeBookTest class declaration begins in line 4 and ends in line 15. The class, like many that begin an application’s execution, contains only a main method.

```
1 // Fig. 3.2: GradeBookTest.java
2 // Creating a GradeBook object and calling its displayMessage method.

4 public class GradeBookTest
5 {
6     // main method begins program execution
7     public static void main( String[] args )
8     {
9         // create a GradeBook object and assign it to myGradeBook
10        GradeBook myGradeBook = new GradeBook();

12        // call myGradeBook's displayMessage method
13        myGradeBook.displayMessage();
14     } // end main
15 } // end class GradeBookTest
```

Welcome to the Grade Book!

Fig. 3.2 | Creating a GradeBook object and calling its displayMessage method.

Lines 7–14 declare method main. A key part of enabling the JVM to locate and call method main to begin the application’s execution is the static keyword (line 7), which indicates that main is a static method. A static method is special, because you can call it without first creating an object of the class in which the method is declared. We discuss static methods in Chapter 6, Methods: A Deeper Look.

In this application, we’d like to call class GradeBook’s displayMessage method to display the welcome message in the command window. Typically, you cannot call a method that belongs to another class until you create an object of that class, as shown in line 10. We begin by declaring variable myGradeBook. The variable’s type is GradeBook—the class we declared in Fig. 3.1. Each new class you create becomes a new type that can be used to declare variables and create objects. You can declare new class types as needed; this is one reason why Java is known as an extensible language.

Variable myGradeBook is initialized (line 10) with the result of the class instance creation expression new GradeBook(). Keyword new creates a new object of the class specified to the right of the keyword (i.e., GradeBook). The parentheses to the right of GradeBook are required. As you’ll learn in Section 3.6, those parentheses in combination with a class name represent a call to a constructor, which is similar to a method but is used only at the time an object is created to initialize the object’s data. You’ll see that data can be placed in the parentheses to specify initial values for the object’s data. For now, we simply leave the parentheses empty.

Just as we can use object System.out to call its methods print, printf and println, we can use object myGradeBook to call its method displayMessage. Line 13 calls the method displayMessage (lines 7–10 of Fig. 3.1) using myGradeBook followed by a dot separator (.), the method name displayMessage and an empty set of parentheses. This call causes the displayMessage method to perform its task. This method call differs from those in Chapter 2 that displayed information in a command window—each of those method calls provided arguments that specified the data to display. At the beginning of line 13, “myGradeBook.” indicates that main should use the myGradeBook object that was created in line 10. Line 7 of Fig. 3.1 indicates that method displayMessage has an empty parameter list—that is, displayMessage does not require additional information to perform its task. For this reason, the method call (line 13 of Fig. 3.2) specifies an empty set of parentheses after the method name to indicate that no arguments are being passed to method displayMessage. When method displayMessage completes its task, method main continues executing at line 14. This is the end of method main, so the program terminates.

Any class can contain a main method. The JVM invokes the main method only in the class used to execute the application. If an application has multiple classes that contain main, the one that’s invoked is the one in the class named in the java command.

## Compiling an Application with Multiple Classes

You must compile the classes in Fig. 3.1 and Fig. 3.2 before you can execute the application. First, change to the directory that contains the application’s source-code files. Next, type the command

```
javac GradeBook.java GradeBookTest.java
```

to compile both classes at once. If the directory containing the application includes only this application’s files, you can compile all the classes in the directory with the command

```
javac *.java
```

The asterisk (*) in *.java indicates that all files in the current directory that end with the file-name extension “.java” should be compiled.

## UML Class Diagram for Class GradeBook

Figure 3.3 presents a UML class diagram for class GradeBook of Fig. 3.1. In the UML, each class is modeled in a class diagram as a rectangle with three compartments. The top compartment contains the name of the class centered horizontally in boldface type. The middle compartment contains the class’s attributes, which correspond to instance variables (discussed in Section 3.4) in Java. In Fig. 3.3, the middle compartment is empty, because this GradeBook class does not have any attributes. The bottom compartment contains the

![](img/009e962758dcc71dbc43a493362e6dc0_112_0.png)

Fig. 3.3 | UML class diagram indicating that class GradeBook has a public displayMessage operation.

class’s operations, which correspond to methods in Java. The UML models operations by listing the operation name preceded by an access modifier (in this case +) and followed by a set of parentheses. Class GradeBook has one method, displayMessage, so the bottom compartment of Fig. 3.3 lists one operation with this name. Method displayMessage does not require additional information to perform its tasks, so the parentheses following the method name in the class diagram are empty, just as they were in the method’s declaration in line 7 of Fig. 3.1. The plus sign (+) in front of the operation name indicates that displayMessage is a public operation in the UML (i.e., a public method in Java). We’ll often use UML class diagrams to summarize a class’s attributes and operations.

## 3.3 Declaring a Method with a Parameter

In our car analogy from Section 1.6, we discussed the fact that pressing a car’s gas pedal sends a message to the car to perform a task—to go faster. But how fast should the car accelerate? As you know, the farther down you press the pedal, the faster the car accelerates. So the message to the car actually includes the task to perform and additional information that helps the car perform the task. This additional information is known as a parameter—the value of the parameter helps the car determine how fast to accelerate. Similarly, a method can require one or more parameters that represent additional information it needs to perform its task. Parameters are defined in a comma-separated parameter list, which is located inside the parentheses that follow the method name. Each parameter must specify a type and a variable name. The parameter list may contain any number of parameters, including none at all. Empty parentheses following the method name (as in Fig. 3.1, line 7) indicate that a method does not require any parameters.

### Arguments to a Method

A method call supplies values—called arguments—for each of the method’s parameters. For example, the method System.out.println requires an argument that specifies the data to output in a command window. Similarly, to make a deposit into a bank account, a deposit method specifies a parameter that represents the deposit amount. When the deposit method is called, an argument value representing the deposit amount is assigned to the method’s parameter. The method then makes a deposit of that amount.

### Class Declaration with a Method That Has One Parameter

We now declare class GradeBook (Fig. 3.4) with a displayMessage method that displays the course name as part of the welcome message. (See the sample execution in Fig. 3.5.) The new method requires a parameter that represents the course name to output.

Before discussing the new features of class GradeBook, let’s see how the new class is used from the main method of class GradeBookTest (Fig. 3.5). Line 12 creates a Scanner named input for reading the course name from the user. Line 15 creates the GradeBook object myGradeBook. Line 18 prompts the user to enter a course name. Line 19 reads the name from the user and assigns it to the nameOfCourse variable, using Scanner method nextLine to perform the input. The user types the course name and presses Enter to submit the course name to the program. Pressing Enter inserts a newline character at the end of the characters typed by the user. Method nextLine reads characters typed by the user until it encounters the newline character, then returns a String containing the characters up to, but not including, the newline. The newline character is discarded.
