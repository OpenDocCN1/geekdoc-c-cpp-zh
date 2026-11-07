# # Defining substitutes

Just as the preprocessor substitutes library code for **#include** directives, other preprocessor directives can be used to substitute text or numeric values before assembly and compilation.

The **#define** directive specifies a macro, comprising an identifier name and a string or numeric value, to be substituted by the preprocessor for each occurrence of that macro in the source code.

Like **#include** preprocessor directives, **#define** directives can appear at the start of the source code. As with constant variable names, the macro name traditionally uses uppercase, and defined string values should be enclosed within double quotes. For numeric substitutions in expressions the macro name should be enclosed in parentheses to ensure correct precedence.

![](bbox=[0.116, 0.307, 0.208, 0.365])

+   1. Start a new program by declaring three **define** directives
+   
+       ```c
+       #define BOOK "C++ Programming in easy steps"
+       #define NUM 200
+       #define RULE "******************************"
+       ```

+   2. Specify the library classes to include, and the namespace
+   
+       ```cpp
+       #include <iostream>
+       using namespace std ;
+       ```

+   3. Add a main function containing a final **return** statement and three statements to output substituted values
+   
+       ```cpp
+       int main()
+       {
+         cout << RULE << endl << BOOK << endl << RULE ;
+         cout << endl << "NUM is: " << NUM << endl ;
+         cout << "Double NUM: " << ( ( NUM ) * 2 ) << endl ;
+         return 0 ;
+       }
+       ```

+   4. Save, compile, and run the program to see the output

![](bbox=[0.233, 0.596, 0.766, 0.696])

![](bbox=[0.116, 0.711, 0.209, 0.762])

Numeric constants are often best declared as const variables – because values substituted by the preprocessor are not subject to type-checking.

+   5. Recompile the program saving the temporary files **c++ define.cpp -save-temps -o define.exe**

+   6. Open the temporary “define.ii” file in a plain text editor and scroll to the end of the file to see the substitutions