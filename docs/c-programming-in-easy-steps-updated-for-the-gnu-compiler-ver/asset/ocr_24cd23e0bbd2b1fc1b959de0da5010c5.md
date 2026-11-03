# Restricting accessibility

The static keyword can be used to restrict the accessibility of functions to the file in which they are created, in exactly the same way that static variables have restricted accessibility. This is recommended practice in larger programs that are spread over multiple “c” files, to safeguard against accidental misuse of functions. For instance, the square() and multiply() functions can't be directly called from the main() function in this example.

![](bbox=[0.2, 0.25, 0.33, 0.42])

+   1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
+   
+   ```c
+   #include <stdio.h>
+   ```
+   
+   2. Declare two custom function prototypes
+   
+   ```c
+   void menu();
+   void action( int option );
+   ```
+   
+   3. Add a main function to call the first custom function then return a zero integer as required by the declaration
+   
+   ```c
+   int main()
+   {
+       menu();
+       return 0;
+   }
+   ```
+   
+   4. After the main block, define the first custom function to pass a menu option as an argument to another function
+   
+   ```c
+   void menu()
+   {
+       int option;
+       printf( "\nWhat would you like to do?" );
+       printf( "\n1. Square a number" );
+       printf( "\n2. Multiply two numbers" );
+       printf( "\n3. Exit\n" );
+       scanf( "%d", &option );
+       action( option );
+   }
+   ```
+   
+   5. Begin a second program file with a preprocessor to include the standard input/output functions, and declare the custom prototypes once more
+   
+   ```c
+   #include <stdio.h>
+   
+   void menu();
+   void action( int option );
+   ```

![](bbox=[0.08, 0.6, 0.2, 0.72])

Notice that prototypes are declared here for each file containing calls to those functions – to prevent an “implicit declaration of function” compiler warning.

![](bbox=[0.2, 0.8, 0.34, 0.97])