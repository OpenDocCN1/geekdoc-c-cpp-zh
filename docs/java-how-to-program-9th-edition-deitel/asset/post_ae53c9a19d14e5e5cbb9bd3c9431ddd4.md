
create an application that draws a variety of shapes. When we formally introduce GUIs in Chapter 14, we use the mouse to choose exactly which shapes to draw and where to draw them. In Chapter 15, we add capabilities of the Java 2D graphics API to draw the shapes with different line thicknesses and fills. We hope you find this case study informative and entertaining.

| Location | Title—Exercise(s) |
|---|---|
| Section 3.8 | Using Dialog Boxes—Basic input and output with dialog boxes |
| Section 4.14 | Creating Simple Drawings—Displaying and drawing lines on the screen |
| Section 5.10 | Drawing Rectangles and Ovals—Using shapes to represent data |
| Section 6.13 | Colors and Filled Shapes—Drawing a bull's-eye and random graphics |
| Section 7.15 | Drawing Arcs—Drawing spirals with arcs |
| Section 8.16 | Using Objects with Graphics—Storing shapes as objects |
| Section 9.8 | Displaying Text and Images Using Labels—Providing status information |
| Section 10.8 | Drawing with Polymorphism—Identifying the similarities between shapes |
| Exercise 14.17 | Expanding the Interface—Using GUI components and event handling |
| Exercise 15.31 | Adding Java 2D—Using the Java 2D API to enhance drawings |

Fig. 3.16 | Summary of the GUI and Graphics Case Study in each chapter.

## Displaying Text in a Dialog Box

The programs presented thus far display output in the command window. Many applications use windows or dialog boxes (also called dialogs) to display output. Web browsers such as Firefox, Internet Explorer, Chrome and Safari display web pages in their own windows. E-mail programs allow you to type and read messages in a window. Typically, dialog boxes are windows in which programs display important messages to users. Class JOptionPane provides prebuilt dialog boxes that enable programs to display windows containing messages—such windows are called message dialogs. Figure 3.17 displays the String "Welcome\nto\nJava" in a message dialog.

```
1  // Fig. 3.17: Dialog1.java
2  // Using JOptionPane to display multiple lines in a dialog box.
3  import javax.swing.JOptionPane; // import class JOptionPane
4
5  public class Dialog1
6  {
7      public static void main( String[] args )
8      {
9          // display a dialog with a message
10         JOptionPane.showMessageDialog( null, "Welcome\nto\nJava" );
11     } // end main
12 } // end class Dialog1
```

Fig. 3.17 | Using JOptionPane to display multiple lines in a dialog box. (Part 1 of 2.)

![](img/009e962758dcc71dbc43a493362e6dc0_131_0.png)

Fig. 3.17 | Using JOptionPane to display multiple lines in a dialog box. (Part 2 of 2.)

Line 3 indicates that the program uses class JOptionPane from package javax.swing. This package contains many classes that help you create graphical user interfaces (GUI). GUI components facilitate data entry by a program’s user and presentation of outputs to the user. Line 10 calls JOptionPane method showMessageDialog to display a dialog box containing a message. The method requires two arguments. The first helps the Java application determine where to position the dialog box. A dialog is typically displayed from a GUI application with its own window. The first argument refers to that window (known as the parent window) and causes the dialog to appear centered over the application’s window. If the first argument is null, the dialog box is displayed at the center of your screen. The second argument is the String to display in the dialog box.

## Introducing static Methods

JOptionPane method showMessageDialog is a so-called static method. Such methods often define frequently used tasks. For example, many programs display dialog boxes, and the code to do this is the same each time. Rather than requiring you to “reinvent the wheel” and create code to display a dialog, the designers of class JOptionPane declared a static method that performs this task for you. A static method is called by using its class name followed by a dot (.) and the method name, as in

```
ClassName.methodName( arguments )
```

Notice that you do not create an object of class JOptionPane to use its static method showMessageDialog. We discuss static methods in more detail in Chapter 6.

## Entering Text in a Dialog

Figure 3.18 uses another predefined JOptionPane dialog called an input dialog that allows the user to enter data into a program. The program asks for the user’s name and responds with a message dialog containing a greeting and the name that the user entered.

Lines 10–11 use JOptionPane method showInputDialog to display an input dialog containing a prompt and a field (known as a text field) in which the user can enter text. Method showInputDialog’s argument is the prompt that indicates what the user should enter. The user types characters in the text field, then clicks the OK button or presses the Enter key to return the String to the program. Method showInputDialog (line 11) returns a String containing the characters typed by the user. We store the String in variable name (line 10). [Note: If you press the dialog’s Cancel button or press the Esc key, the method returns null and the program displays the word “null” as the name.]

Lines 14–15 use static String method format to return a String containing a greeting with the user’s name. Method format works like method System.out.printf, except that format returns the formatted String rather than displaying it in a command window. Line 18 displays the greeting in a message dialog, just as we did in Fig. 3.17.

// Fig. 3.18: NameDialog.java
// Basic input with a dialog box.
import javax.swing.JOptionPane;

public class NameDialog
{
    public static void main( String[] args )
    {
        // prompt user to enter name
        String name =
            JOptionPane.showInputDialog( "What is your name?" );

        // create the message
        String message =
            String.format( "Welcome, %s, to Java Programming!", name );

        // display the message to welcome the user by name
        JOptionPane.showMessageDialog( null, message );
    } // end main
} // end class NameDialog

![](img/009e962758dcc71dbc43a493362e6dc0_132_0.png)

Fig. 3.18 | Obtaining user input from a dialog.

## GUI and Graphics Case Study Exercise

3.1 Modify the addition program in Fig. 2.7 to use dialog-based input and output with the methods of class JOptionPane. Since method showInputDialog returns a String, you must convert the String the user enters to an int for use in calculations. The Integer class’s static method parseInt takes a String argument representing an integer (e.g., the result of JOptionPane.showInputDialog) and returns the value as an int. Method parseInt is a static method of class Integer (from package java.lang). If the String does not contain a valid integer, the program will terminate with an error.

## 3.9 Wrap-Up

In this chapter, you learned how to declare instance variables of a class to maintain data for each object of the class, and how to declare methods that operate on that data. You learned how to call a method to tell it to perform its task and how to pass information to methods as arguments. You learned the difference between a local variable of a method and an instance variable of a class and that only instance variables are initialized automatically. You also learned how to use a class’s constructor to specify the initial values for an object’s instance variables. Throughout the chapter, you saw how the UML can be used to create class diagrams that model the constructors, methods and attributes of classes. Finally, you learned about floating-point numbers—how to store them with variables of primitive type double,

how to input them with a Scanner object and how to format them with printf and format specifier %f for display purposes. In the next chapter we begin our introduction to control statements, which specify the order in which a program’s actions are performed. You’ll use these in your methods to specify how they should perform their tasks.

## Summary

Section 3.2 Declaring a Class with a Method and Instantiating an Object of a Class

- Each class declaration that begins with the access modifier (p. 72) public must be stored in a file that has exactly the same name as the class and ends with the .java file-name extension.
- Every class declaration contains keyword class followed immediately by the class’s name.
- A method declaration that begins with keyword public indicates that the method can be called by other classes declared outside the class declaration.
- Keyword void indicates that a method will perform a task but will not return any information.
- By convention, method names begin with a lowercase first letter and all subsequent words in the name begin with a capital first letter.
- Empty parentheses following a method name indicate that the method does not require any parameters to perform its task.
- Every method’s body is delimited by left and right braces ({ and }).
- The method’s body contains statements that perform the method’s task. After the statements execute, the method has completed its task.
- When you attempt to execute a class, Java looks for the class’s main method to begin execution.
- Typically, you cannot call a method of another class until you create an object of that class.
- A class instance creation expression (p. 74) begins with keyword new and creates a new object.
- To call a method of an object, follow the variable name with a dot separator (.; p. 75), the method name and a set of parentheses containing the method’s arguments.
- In the UML, each class is modeled in a class diagram as a rectangle with three compartments. The top compartment contains the class’s name centered horizontally in boldface. The middle one contains the class’s attributes, which correspond to fields (p. 79) in Java. The bottom one contains the class’s operations (p. 76), which correspond to methods and constructors in Java.
- The UML models operations by listing the operation name followed by a set of parentheses. A plus sign (+) in front of the operation name indicates that the operation is a public one in the UML (i.e., a public method in Java).

Section 3.3 Declaring a Method with a Parameter

- Methods often require parameters (p. 76) to perform their tasks. Such additional information is provided to methods via arguments in method calls.
- Scanner method nextLine (p. 76) reads characters until a newline character is encountered, then returns the characters as a String.
- Scanner method next (p. 77) reads characters until any white-space character is encountered, then returns the characters as a String.
- A method that requires data to perform its task must specify this in its declaration by placing additional information in the method’s parameter list (p. 76).
- Each parameter must specify both a type and a variable name.
