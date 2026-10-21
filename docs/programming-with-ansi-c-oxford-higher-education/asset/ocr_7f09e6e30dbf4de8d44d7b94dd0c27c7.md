the definition. It prohibits the generation of a conversion operator for a single-argument constructor.

# Initialization of the object

Giving specific values to the objects at the time they are defined is known as initialization of the object.

# Member initialization list (MIL)

This is the list that follows the constructor header and ends before the body of the constructor begins. It is preceded by the word “:” and contains initializations of data members separated by “,”.

# Parameterized constructor

A constructor with one or more than one argument is known as a parameterized constructor.

# EXERCISES

# Multiple Choice Questions

+   1. What should be the return type of a constructor?
+   (a) void
+   (b) int
+   (c) It cannot have any return type
+   (d) It can have any return type
+   2. What type of values do constructors provide to the object?
+   (a) New values
+   (b) Initial values
+   (c) Dynamic values
+   (d) Constant values
+   3. How is the constructor function called?
+   (a) It is automatically called when the object is created.
+   (b) It is to be called soon after the object is created.
+   (c) It can be called anywhere in the program.
+   (d) It needs to be explicitly called before object creation.
+   4. Unless a copy constructor or an assignment operator is defined for an object, ________ and ________ work in a similar way.
+   (a) object declaration and creation
+   (b) constructor and member function
+   (c) initialization and assignment
+   (d) ordinary and default parameters
+   5. Whenever possible, the compiler takes a shortcut of copying the objects ________.
+   (a) byte by byte, bit by bit
+   (b) char by char
+   (c) Member by member
+   (d) None
+   6. Destructors are invoked ________.
+   (a) explicitly when needed
+   (b) explicitly when object goes out of scope
+   (c) automatically when object goes out of scope
+   (d) automatically at the end of a program
+   7. How many constructors are possible to define?
+   (a) Only one
+   (b) Exactly two
+   (c) Any number of constructors
+   (d) Any number of constructors, though it is advisable to have as few constructors as possible

+   8. Which of the following is the correct syntax of a copy constructor?
+   (a) Player (Player) ;
+   (b) Player (Player &, Player &) ;
+   (c) Player (Player *) ;
+   (d) Player (Player &) ;
+   9. The constructor body cannot have ________.
+   (a) malloc statement
+   (b) new statement
+   (c) return statement
+   (d) exit statement
+   10. What will happen if we write following two statements in a program for a class named Time?
+   Time(int hours=0, int minutes=0, int seconds=0) { }
+   Time ( ) { }
+   (a) Only second one is permissible
+   (b) Only first one is permissible
+   (c) Compiler gives an error
+   (d) Linker gives an error

# Conceptual Exercises

+   1. Give examples of C++ object definitions and usage that demonstrate the similar-to-built-in behaviour concept.
+   2. What is the need for initialization of objects using a constructor? What could be the problems if the constructors are not provided in C++?
+   3. What are the functions of constructors? How are they different from normal functions?
+   4. What is the difference between a default constructor provided by the compiler and a user-defined default constructor?