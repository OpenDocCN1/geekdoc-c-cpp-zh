# EXERCISES 12.3

+   1. (Review) a. Explain how dynamic allocation of memory works.
+   b. Describe the process of creating a dynamically allocated object. Specifically, discuss the roles of a pointer variable and the new operator in creating a dynamically allocated object.
+   c. Discuss the importance of deleting dynamically allocated objects, and explain what can happen if these objects aren't deleted.

+   2. (Review) a. Explain what a pointer is.
+   b. For each of the following pointer declarations, identify the pointer variable's name and the data type of the object to be accessed when the address in the pointer variable is dereferenced:
+   i. Checkout *a;
+   ii. Pump *pointer1;
+   iii. Pump *addr_of_aPump;
+   iv. int *addr_of_int;
+   v. double *b;
+   c. If the asterisks were removed from the declarations in Exercise 2b, what would the names before the semicolon represent?

+   3. (Practice) a. Enter and run Program 12.4, but specify the number of objects to be created as four. Explain why your program outputs the same memory addresses.
+   b. Remove the statement delete anotherTrans; or convert it to a comment (called "commenting out"), and rerun Program 12.4. Again, make sure to have the program create four new objects. Explain why the memory addresses now differ for each new object.
+   c. Using the results of Exercise 3b, why is it no longer possible to access any of the first three created objects after the fourth object has been dynamically created? What does this imply about the previously allocated memory, and why is it a serious flaw in the program?

+   4. (Practice) Enter and run Program 12.5.

+   5. (Desk check) For the following class, determine what the two member methods accomplish:
+   #include <iostream>
+   #include <ctime>
+   #include <cmath>
+   using namespace std;
+   
+   // Coin class
+   // precondition:
+   //     srand() must be called once before the flip() method is called