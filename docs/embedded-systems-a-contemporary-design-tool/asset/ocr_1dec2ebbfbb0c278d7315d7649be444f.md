when such a practice might be particularly useful in an embedded application.

+   6.29 The C language supports converting from a variable of one type to a different type; what precautions must be taken when doing so?

+   6.30 What is the value for the variable x in the following code fragment?
+   ```
+   int x = 2;
+   float y = 3.7;
+   x = y;
+   ```

+   6.31 What will the following code fragment print?
+   ```
+   int x = 2;
+   char y = 'a';
+   x = y;
+   printf("the value is %i", x);
+   ```

+   6.32 The following code fragment contains several ill-advised practices. What are these?
+   ```
+   int x = 2;
+   char y = 'a';
+   x = y;
+   printf("the value is %i", x);
+   ```

+   6.33 The C language specifies three primary scopes. Give an example of when each might be used.

+   6.34 The C language specifies six primary storage classes. Give an example of when each might be used.

+   6.35 Can a variable declared in one function be returned by reference to another function? Why or why not?

+   6.36 Can a pointer variable declared and assigned to refer to a variable in one function be returned and dereferenced in another function? Why or why not?

# C Program Structure

+   6.37 What are the major kinds of files that will typically be compiled and linked together in an embedded C software application? Briefly describe the information that might be contained in each such file.

+   6.38 Give examples of several different types of declarations for which external linkage might be useful?

+   6.39 How can the identity of a C variable declared in one file in a program be hidden from other files in the program? Why would we want to do such a thing?

+   6.40 How can the identity of a C function declared in one file in a program be hidden from other files in the program? Why would we want to do such a thing?

+   6.41 Can a function be declared on one file and defined in another? If so, how and why would we want to do such a thing?

+   6.42 Why do we distinguish between a debug and a release build for an embedded application?

+   6.43 How do we create a debug version of a program? a release build?

+   6.44 How can we ensure that debugging code be preserved and available for future revisions and yet not impact the size of the code used for the embedded application?

+   6.45 How can we make a test suite available for future revisions without impacting the size of the code used for the embedded application?

# 6.9 PROBLEMS

# Using the Preprocessor

+   6.1 Starting with the program given in Figure P6.1, write two functions with the prototypes
+   ```
+   int incrementItem(void)
+   int decrementItem(void)
+   ```

that will increment or decrement the variable count by 2. Using the preprocessor, conditionally include either the original or the new functions based on whether the variable TWO is defined.

+   6.2 Starting with the program given in Figure P6.1 and using the preprocessor, convert the functions incrementItem() and decrementItem() to macros.

+   6.3 Starting with the program given in Figure P6.1, write macro versions of the functions incrementItem() and decrementItem(). Using the preprocessor, build the program such that the two functions are compiled either as functions

or macros based on whether the variable MACROS is defined. How can you verify that the desired version of the build has occurred?

# Multiple Files

+   6.4 Starting with the program given in Figure P6.1, move the functions and global static variable to one .c and global variables to a second.

# C Scope

+   6.5 Starting with the program in Problem 6.4, add debug code to the two functions to print out the value of the variable count each time the function is called. Using the preprocessor, conditionally include the debug code whenever the variable DEBUG is defined.