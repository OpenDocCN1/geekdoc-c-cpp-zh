# Conceptual Exercises

+   1. What is polymorphism? What is the difference between compile time and run-time polymorphism?
+   2. What is the importance of this pointer in the call to the function using base class pointer?
+   3. Consider base class B and derived class D. Assume pB is a pointer to base class and pD is a pointer to derived class. Differentiate between these two pointers in terms of accessing the derived class object.
+   4. What is a subject concept? What is its importance in the case of a base class pointer accessing a derived class pointer?
+   5. Why is a non-virtual member function of a base class always called even when the base class pointer is pointing to the derived class object?
+   6. What is the difference between a normal member function and a virtual function?
+   7. Explain static binding. How do virtual functions enable dynamic binding?
+   8. What is the problem of default arguments of the virtual function? How can that be solved?
+   9. What is the requirement of virtual functions in OO programming?
+   10. Why virtual constructors are not possible but virtual destructor is a good idea?
+   11. Differentiate between virtual functions and pure virtual functions.
+   12. What is the need for statically invoking pure virtual or virtual functions?

+   4. When we write a pure virtual function in any class, ________.
+   (a) the class becomes an abstract class
+   (b) the class cannot be inherited
+   (c) the class becomes a virtual class
+   (d) the class becomes a pure virtual base class
+   5. Pure virtual functions can be invoked statically like normal virtual functions only if the function is defined ________.
+   (a) outside the class with empty body
+   (b) inside the class with empty body
+   (c) outside the class with some body
+   (d) inside the class with some body
+   6. Every class with at least one virtual function ________.
+   (a) has multiple copies of virtual functions
+   (b) has single copy of the virtual table
+   (c) has multiple copies of virtual table
+   (d) None of the above
+   7. The ________ is used to get the address of an object.
+   (a) address operator
+   (b) address function
+   (c) address-of operator
+   (d) address-of function
+   8. What should be used to execute a derived class function using a pointer to base class pointing to a derived class object?
+   (a) this pointer should be used
+   (b) Virtual function should be used
+   (c) Virtual pointer should be used
+   (d) None of the above
+   9. ________ cannot help in achieving run-time polymorphism.
+   (a) Normal objects
+   (b) Pointers to objects
+   (c) Virtual functions
+   (d) All of the above
+   10. The ________ manages the pointer to point to the respective subobject in case two or more classes inherit into a single derived class.
+   (a) compiler
+   (b) linker
+   (c) loader
+   (d) programmer

# Practical Exercises

+   1. Define the Time class described in Chapter 9. Inherit Indian Standard Time (IST) and Greenwich Meridian Time (GMT) from it. Write routines that convert from one type of time to another (IST and GMT).
+   2. Define a class Stack. Inherit it into VariableStack. Now, inherit this class into SystemVariableStack and UserVariableStack. Provide constructors and destructors for all the classes.
+   3. Define a class Student. Inherit it into engineering, arts, commerce, and science students. Inherit engineering student into computer science, electronics and communication, and information technology student. Provide constructors for all the classes.
+   4. For the Student class given in Exercise 3, write a program to use a pointer to the Student class to access a record of the computer science student. It can be seen that the part defined in computer science is not accessible. Then, define a pointer to computer science student. Now, it can be seen that the part is accessible. Cast the original pointer-to-