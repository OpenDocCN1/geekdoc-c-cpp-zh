+   - Once installed, open Code::Blocks.

# 9.11.2. Basic Structure of a C Program

```
```c
// Preprocessor Directives
#include <stdio.h> // Include necessary libraries
// Main Function
int main()
{
// Declarations (Variable and Function Declarations)
// Statements (Executable code)
return 0; // Return statement (Exit status)
}
```
```

+   - **Preprocessor Directives:** These lines begin with # and are used to include libraries and perform other pre-processing tasks.
+   - **main():** This is the main function where program execution begins.
+   - **Declarations:** This is where you declare variables and functions that will be used in your program.
+   - **Statements:** These are the executable statements that perform the actual work of your program.
+   - **return 0;:** This line is used to exit the program with a status code of 0, indicating successful execution.

# 9.11.3. Format Specifiers

Format specifiers are used in C to specify the data type of the variables you want to print or read using functions like printf and scanf. Common format specifiers include:

+   - `%d`: Integer
+   - `%f`: Float or double
+   - `%c`: Character
+   - `%s`: String