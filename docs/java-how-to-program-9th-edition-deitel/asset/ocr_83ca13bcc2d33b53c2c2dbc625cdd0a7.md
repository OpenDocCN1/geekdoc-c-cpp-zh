```
```java
// Fig. 3.1: GradeBook.java
// Class declaration with one method.

public class GradeBook
{
   // display a welcome message to the GradeBook user
   public void displayMessage()
   {
      System.out.println( "Welcome to the Grade Book!" );
   } // end method displayMessage
} // end class GradeBook
```
```

class followed immediately by the class’s name. Every class’s body is enclosed in a pair of left and right braces, as in lines 5 and 11 of class GradeBook.

In Chapter 2, each class we declared had one method named main. Class GradeBook also has one method—displayMessage (lines 7–10). Recall that main is a special method that’s always called automatically by the Java Virtual Machine (JVM) when you execute an application. Most methods do not get called automatically. As you’ll soon see, you must call method displayMessage explicitly to tell it to perform its task.

The method declaration begins with keyword public to indicate that the method is “available to the public”—it can be called from methods of other classes. Next is the method’s return type, which specifies the type of data the method returns to its caller after performing its task. The return type void indicates that this method will perform a task but will not return (i.e., give back) any information to its calling method. You’ve used methods that return information—for example, in Chapter 2 you used Scanner method nextInt to input an integer typed by the user at the keyboard. When nextInt reads a value from the user, it returns that value for use in the program.

The name of the method, displayMessage, follows the return type. By convention, method names begin with a lowercase first letter and subsequent words in the name begin with a capital letter. The parentheses after the method name indicate that this is a method. Empty parentheses, as in line 7, indicate that this method does not require additional information to perform its task. Line 7 is commonly referred to as the method header. Every method’s body is delimited by left and right braces, as in lines 8 and 10.

The body of a method contains one or more statements that perform the method’s task. In this case, the method contains one statement (line 9) that displays the message "Welcome to the Grade Book!" followed by a newline (because of println) in the command window. After this statement executes, the method has completed its task.

# Class GradeBookTest

Next, we’d like to use class GradeBook in an application. As you learned in Chapter 2, method main begins the execution of every application. A class that contains method main begins the execution of a Java application. Class GradeBook is not an application because it does not contain main. Therefore, if you try to execute GradeBook by typing java GradeBook in the command window, an error will occur. This was not a problem in Chapter 2, because every class you declared had a main method. To fix this problem, we must either declare a separate class that contains a main method or place a main method in class GradeBook.