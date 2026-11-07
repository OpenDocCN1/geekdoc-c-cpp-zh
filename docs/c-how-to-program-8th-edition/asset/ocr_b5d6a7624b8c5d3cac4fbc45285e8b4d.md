+   - Comments do not cause the computer to perform any action (p. 40) when the program is run—they’re ignored by the compiler and do not cause any machine-language object code to be generated.
+   - A preprocessor directive (p. 39) begins with # and is a message to the C++ preprocessor. Preprocessor directives are processed before the program is compiled and don’t end with a semicolon.
+   - The line `#include <iostream>` (p. 39) tells the C++ preprocessor to include the contents of the input/output stream header, which contains information necessary to compile programs that use `std::cin` (p. 43) and `std::cout` (p. 40) and the stream insertion (`<<`, p. 40) and stream extraction (`>>`, p. 43) operators.
+   - White space (i.e., blank lines, space characters and tab characters, p. 39) makes programs easier to read. White-space characters outside of literals are ignored by the compiler.
+   - C++ programs begin executing at `main` (p. 39), even if `main` does not appear first in the program.
+   - The keyword `int` to the left of `main` indicates that `main` “returns” an integer value.
+   - The body (p. 40) of every function must be contained in braces (`{` and `}`).
+   - A string (p. 40) in double quotes is sometimes referred to as a character string, message or string literal. White-space characters in strings are *not* ignored by the compiler.
+   - Every statement (p. 40) must end with a semicolon (also known as the statement terminator).
+   - Output and input in C++ are accomplished with streams (p. 40) of characters.
+   - The output stream object `std::cout`—normally connected to the screen—is used to output data. Multiple data items can be output by concatenating stream insertion (`<<`) operators.
+   - The input stream object `std::cin`—normally connected to the keyboard—is used to input data. Multiple data items can be input by concatenating stream extraction (`>>`) operators.
+   - The notation `std::cout` specifies that we are using `cout` from “namespace” `std`.
+   - When a backslash (i.e., an escape character) is encountered in a string of characters, the next character is combined with the backslash to form an escape sequence (p. 41).
+   - The newline escape sequence `\n` (p. 41) moves the cursor to the beginning of the next line on the screen.
+   - A message that directs the user to take a specific action is known as a prompt (p. 45).
+   - C++ keyword `return` (p. 41) is one of several means to exit a function.

# ### *Section 2.4 Another C++ Program: Adding Integers*

+   - All variables (p. 43) in a C++ program must be declared before they can be used.
+   - A variable name is any valid identifier (p. 44) that is not a keyword. An identifier is a series of characters consisting of letters, digits and underscores (`_`). Identifiers cannot start with a digit. Identifiers can be any length, but some systems or C++ implementations may impose length restrictions.
+   - C++ is case sensitive (p. 44).
+   - Most calculations are performed in assignment statements (p. 46).
+   - A variable is a location in memory (p. 47) where a value can be stored for use by a program.
+   - Variables of type `int` (p. 44) hold integer values, i.e., whole numbers such as 7, −11, 0, 31914.

# ### *Section 2.5 Memory Concepts*

+   - Every variable stored in the computer’s memory has a name, a value, a type and a size.
+   - Whenever a new value is placed in a memory location, the process is destructive (p. 47); i.e., the new value replaces the previous value in that location. The previous value is lost.