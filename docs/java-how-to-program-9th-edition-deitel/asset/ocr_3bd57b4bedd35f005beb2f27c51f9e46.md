Book. To help you prepare for the larger programs you’ll encounter later in this book and in industry, we use a separate class (GradeBookTest in this example) containing method main to test each new class we create in this chapter. Some programmers refer to such a class as a driver class.

The GradeBookTest class declaration (Fig. 3.2) contains the main method that will control our application’s execution. The GradeBookTest class declaration begins in line 4 and ends in line 15. The class, like many that begin an application’s execution, contains only a main method.

```
1 // Fig. 3.2: GradeBookTest.java
2 // Creating a GradeBook object and calling its displayMessage method.
3 
4 public class GradeBookTest
5 {
6     // main method begins program execution
7     public static void main( String[] args )
8     {
9         // create a GradeBook object and assign it to myGradeBook
10        GradeBook myGradeBook = new GradeBook();
11 
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