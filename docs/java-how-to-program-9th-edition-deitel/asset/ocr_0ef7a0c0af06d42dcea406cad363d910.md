# 3.1 Introduction

We introduced the basic terminology and concepts of object-oriented programming in Section 1.6. In this chapter, we present a simple framework for organizing object-oriented applications in Java. Typically, the applications you develop in this book will consist of two or more classes. If you become part of a development team in industry, you might work on applications that contain hundreds, or even thousands, of classes.

First, we motivate the notion of classes with a real-world example. Then we present five applications to demonstrate creating and using your own classes. The first four of these begin our case study on developing a grade book class that instructors can use to maintain student test scores. This case study is enhanced in Chapters 4, 5 and 7. The last example introduces floating-point numbers—that is, numbers containing decimal points—in a bank account class that maintains a customer’s balance.

# 3.2 Declaring a Class with a Method and Instantiating an Object of a Class

In Sections 2.5 and 2.8, you created an object of the existing class Scanner, then used that object to read data from the keyboard. In this section, you’ll create a new class, then use it to create an object. We begin by declaring classes GradeBook (Fig. 3.1) and GradeBookTest (Fig. 3.2). Class GradeBook (declared in the file GradeBook.java) will be used to display a message on the screen (Fig. 3.2) welcoming the instructor to the grade book application. Class GradeBookTest (declared in the file GradeBookTest.java) is an application class in which the main method will create and use an object of class GradeBook. Each class declaration that begins with keyword public must be stored in a file having the same name as the class and ending with the .java file-name extension. Thus, classes GradeBook and GradeBookTest must be declared in separate files, because each class is declared public.

# Class GradeBook

The GradeBook class declaration (Fig. 3.1) contains a displayMessage method (lines 7–10) that displays a message on the screen. We’ll need to make an object of this class and call its method to execute line 9 and display the message.

The class declaration begins in line 4. The keyword public is an access modifier. For now, we’ll simply declare every class public. Every class declaration contains keyword