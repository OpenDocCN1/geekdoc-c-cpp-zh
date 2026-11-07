# Defining conditions

The preprocessor can make intelligent insertions to program source code by using macro functions to perform conditional tests. An **#ifdef** directive performs the most common preprocessor function by testing to see if a specified macro has been defined. When the macro has been defined, so the test returns true, the preprocessor will insert all directives, or statements, on subsequent lines up to a corresponding **#endif** directive.

Conversely, an **#ifndef** directive tests to see if a specified macro has not been defined. When that test returns true, it will insert all directives, or statements, on subsequent lines up to a corresponding **#endif** directive.

To satisfy either conditional test, it should be noted that a **#define** directive need only specify the macro name to define the identifier – it need not specify a value to substitute.

Any previously defined macro can be removed later using the **#undef** directive – so that subsequent **#ifdef** conditional tests fail. The macro can then be redefined by a further **#define** directive.

![](bbox=[0.118, 0.362, 0.188, 0.426])

+   1. Start a new program with a conditional test to insert a directive when a macro is not already defined
+   
+      ```cpp
+      #ifndef BOOK
+          #define BOOK "C++ Programming in easy steps"
+      #endif
+      ```
+   
+   2. Specify the library classes to include, and the namespace
+   
+      ```cpp
+      #include <iostream>
+      using namespace std ;
+      ```
+   
+   3. Add a main function containing a final **return** statement
+   
+      ```cpp
+      int main()
+      {
+          // Program code goes here.
+          return 0 ;
+      }
+      ```
+   
+   4. In the main function, add a conditional preprocessor test to insert an output statement when the test succeeds
+   
+      ```cpp
+      #ifdef BOOK
+          cout << BOOK ;
+      #endif
+      ```
+   
+   5. Add another conditional preprocessor test to both define a new macro and insert an output statement when the test succeeds
+   
+      ```cpp
+      #ifndef AUTHOR
+          #define AUTHOR "Mike McGrath"
+          cout << " by " << AUTHOR << endl ;
+      #endif
+      ```
+   
+   6. Next, add a conditional test to undefine a macro if it has already been defined
+   
+      ```cpp
+      #ifdef BOOK
+          #undef BOOK
+      #endif
+      ```
+   
+   7. Now, add a conditional test to redefine a macro if it is no longer defined, and to insert an output statement
+   
+      ```cpp
+      #ifndef BOOK
+          #define BOOK "Linux in easy steps"
+      ```