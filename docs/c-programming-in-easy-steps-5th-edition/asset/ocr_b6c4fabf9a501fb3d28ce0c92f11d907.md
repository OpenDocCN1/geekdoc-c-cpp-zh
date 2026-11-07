# Using macro functions

The **#define** directive can be used to create macro functions that will be substituted in the source code before compilation.

A preprocessor function declaration comprises a macro name, immediately followed by parentheses containing the function’s arguments – it is important not to leave any space between the name and the parentheses. The declaration is then followed by the function definition within another set of parentheses. For example, a preprocessor macro function to half an argument looks like this:

```
#define HALF(n) (n / 2)
```

Care should be taken when using macro functions, because unlike regular C++ functions, they do not perform any kind of type checking – so it’s quite easy to create a macro that causes errors. For this reason, inline functions are usually preferable to macro functions, but because macros directly substitute their code, they avoid the overhead of a function call – so the program runs faster. The resulting difference can be seen in the first temporary file created during the compilation process:

![](bbox=[0.118, 0.371, 0.191, 0.437])

+   1. Start a new program by defining two macro functions to manipulate a single argument
+   
+   ```cpp
+   #define SQUARE(n) (n * n)
+   #define CUBE(n) (n * n * n)
+   ```

+   2. After the macro function definitions, specify the library classes to include, and a namespace prefix to use
+   
+   ```cpp
+   #include <iostream>
+   using namespace std;
+   ```

+   3. Next, declare two inline functions to manipulate a single argument – just like the macro functions defined above
+   
+   ```cpp
+   inline int square(int n) { return (n * n); }
+   inline int cube(int n) { return (n * n * n); }
+   ```

+   4. Add a main function containing a final return statement
+   
+   ```cpp
+   int main()
+   {
+       // Program code goes here.
+       return 0;
+   }
+   ```

+   5. At the start of the main function block, declare and initialize an integer variable
+   
+   ```cpp
+   int num = 5;
+   ```

+   6. Now, insert statements to call each macro function and each comparable inline function
+   
+   ```cpp
+   cout << "Macro SQUARE: " << SQUARE(num) << endl;
+   cout << "Inline square: " << square(num) << endl;
+   cout << "Macro CUBE: " << CUBE(num) << endl;
+   cout << "Inline cube: " << cube(num) << endl;
+   ```

+   7. Save the file, then compile the program, saving the temporary files and run the program
+   
+   ```bash
+   c++ macro.cpp -save-temps -o macro.exe
+   ```