
- 4. Start a new program with a conditional test to seek the `_WIN32` and `__linux` macros – to identify the platform

  ```cpp
  #ifdef _WIN32
      #define PLATFORM "Windows"
  #elif defined __linux
      #define PLATFORM "Linux"
  #endif
  ```

- 5. Specify the library classes to include, and the namespace

  ```cpp
  #include <iostream>
  using namespace std ;
  ```

- 6. Now, add a main function containing a final `return` statement and a statement to identify the host platform

  ```cpp
  int main()
  {
      cout << PLATFORM << " System" << endl ;
      return 0 ;
  }
  ```

- 7. In the main function, insert statements to execute for specific platforms

  ```cpp
  if ( PLATFORM == "Windows" )
      cout << "Performing Windows-only tasks..." << endl ;
  if ( PLATFORM == "Linux" )
      cout << "Performing Linux-only tasks..." << endl ;
  ```

- 8. Save, compile, and run the program to see platform-specific output

![](img/bf8dbdfb89042fadbaa73b4160c74bac_158_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_158_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_158_2.png)

The predefined `_WIN32` macro has one underscore but the `__linux` macro has two underscore characters.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_158_3.png)

The conditional test of predefined macros could be extended to seek those of other operating systems, and a final `#else` directive added to specify an "Unknown" default.

## Guarding inclusions

Typically, a C++ program will have many **.h** header files and a single **.cpp** implementation file containing the main program. Header files may often contain one or more **#include** directives to make other classes or functions available from other header files, and can cause duplication where definitions appear in two files. For example, where a header file includes another header file containing a function definition, the compiler will consider that definition to appear in each file -- so compilation will fail.

The popular solution to this problem of re-definition employs preprocessor directives to ensure the compiler will only be exposed to a single definition. These are known as "inclusion guards" and create a unique macro name for each header file. Traditionally, the name is an uppercase version of the file name, with the dot changed to an underscore. For example, **RUM_H** for a file **rum.h**.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_159_0.png)

Inclusion guards are also known as "macro guards" or simply as "include guards".

In creating a macro to guard against duplication, an **#ifndef** directive first tests to see if the definition has already been made by another header file included in the same program. If the definition already exists, the compiler ignores the duplicate definition, otherwise a **#define** directive will permit the compiler to use the definition in that header file:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_159_1.png)

add.h

![](img/bf8dbdfb89042fadbaa73b4160c74bac_159_2.png)

triple.h

![](img/bf8dbdfb89042fadbaa73b4160c74bac_159_3.png)

guard.cpp

- 1. Create a header file named "add.h" containing the inline declaration of an "add" function

  ```cpp
  inline int add ( int x, int y ) { return ( x + y ) ; }
  ```

- 2. Now, create a header file named "triple.h" containing a preprocessor directive to make the add function available for use in the inline declaration of a "triple" function

  ```cpp
  #include "add.h"

  inline int triple ( int x ) { return add( x, add( x, x ) ) ; }
  ```

- 3. Start a new program with preprocessor directives to make both the add and triple functions available

  ```cpp
  #include "add.h"
  #include "triple.h"
  ```

- 4. Specify the library classes to include and the namespace

  ```cpp
  #include <iostream>
  using namespace std ;
  ```

- 5. Add a main function containing statements that call both the **add()** and **triple()** functions from the included headers

  ```cpp
  int main()
  {
      cout << "9 + 3 = " << add(9, 3) << endl ;
      cout << "9 x 3 = " << triple(9) << endl ;
      return 0 ;
  }
  ```

- 6. Save the files, then attempt to compile the program to see compilation fail because the add function appears to be defined twice – in "add.h" and by inclusion in "triple.h"

![](img/bf8dbdfb89042fadbaa73b4160c74bac_160_0.png)

- 7. Edit the header file "add.h" to enclose the inline function declaration within a preprocessor inclusion guard

  ```cpp
  #ifndef ADD_H
  #define ADD_H

  inline int add ( int x, int y ) { return ( x + y ) ; }

  #endif
  ```

- 8. Save the modified file, then compile and run the program – compilation now succeeds because the inclusion guard prevents the apparent re-definition of the add function

![](img/bf8dbdfb89042fadbaa73b4160c74bac_160_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_160_2.png)

Use the conventional naming scheme, where the macro name resembles the file name, to avoid conflicts.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_160_3.png)

All header files should contain header guards – add a **TRIPLE_H** macro to the triple.h file.

## Using macro functions

The **#define** directive can be used to create macro functions that will be substituted in the source code before compilation.

A preprocessor function declaration comprises a macro name, immediately followed by parentheses containing the function's arguments – it is important not to leave any space between the name and the parentheses. The declaration is then followed by the function definition within another set of parentheses. For example, a preprocessor macro function to half an argument looks like this:

```cpp
#define HALF(n) (n / 2)
```

Care should be taken when using macro functions, because unlike regular C++ functions, they do not perform any kind of type checking – so it's quite easy to create a macro that causes errors. For this reason, inline functions are usually preferable to macro functions, but because macros directly substitute their code, they avoid the overhead of a function call – so the program runs faster. The resulting difference can be seen in the first temporary file created during the compilation process:

![](img/bf8dbdfb89042fadbaa73b4160c74bac_161_0.png)

- 1. Start a new program by defining two macro functions to manipulate a single argument

  ```cpp
  #define SQUARE(n) (n * n)
  #define CUBE(n) (n * n * n)
  ```

- 2. After the macro function definitions, specify the library classes to include, and a namespace prefix to use

  ```cpp
  #include <iostream>
  using namespace std;
  ```

- 3. Next, declare two inline functions to manipulate a single argument – just like the macro functions defined above

  ```cpp
  inline int square(int n) { return (n * n); }
  inline int cube(int n) { return (n * n * n); }
  ```

- 4. Add a main function containing a final return statement

  ```cpp
  int main()
  {
      // Program code goes here.
      return 0;
  }
  ```

- 5. At the start of the main function block, declare and initialize an integer variable

  ```cpp
  int num = 5;
  ```

- 6. Now, insert statements to call each macro function and each comparable inline function

  ```cpp
  cout << "Macro SQUARE: " << SQUARE(num) << endl;
  cout << "Inline square: " << square(num) << endl;
  cout << "Macro CUBE: " << CUBE(num) << endl;
  cout << "Inline cube: " << cube(num) << endl;
  ```

- 7. Save the file, then compile the program, saving the temporary files and run the program

  ```bash
  c++ macro.cpp -save-temps -o macro.exe
  ```

## Building strings

The preprocessor # operator is known as the "stringizing" operator, as it converts a series of characters passed as a macro argument into a string – adding double quotes to enclose the string.

All whitespace before or after the series of characters passed as a macro argument to the stringizing operator is ignored, and multiple spaces between characters is reduced to just one space.

The stringizing operator is useful to pass string values to a preprocessor #define directive without needing to surround each string with double quotes.

A macro definition can combine two terms into a single term using the ## merging operator. Where the combined term is a variable name, its value is not expanded by the macro – it simply allows the variable name to be substituted by the macro.

![](img/bf8dbdfb89042fadbaa73b4160c74bac_163_0.png)

strung.cpp

- 1. Start a new program by defining a macro to create a string from a series of characters passed as its argument, to substitute in an output statement

  ```cpp
  #define LINEOUT( str ) cout << #str << endl
  ```

- 2. Define a second macro to combine two terms passed as its arguments into a variable name, to substitute in an output statement

  ```cpp
  #define GLUEOUT( a, b ) cout << a##b << endl
  ```

- 3. After the macro definitions, specify the library classes to include, and a namespace prefix to use

  ```cpp
  #include <string>
  #include <iostream>
  using namespace std ;
  ```

- 4. Add a main function containing a final return statement

  ```cpp
  int main()
  {
      // Program code goes here.
      return 0 ;
  }
  ```

- 5. At the start of the main function block, declare and initialize a string variable, then append a further string

  ```cpp
  string longerline = "They carried a net " ;
  longerline += "and their hearts were set" ;
  ```

- 6. Now, add statements to output text using the macros

  ```cpp
  LINEOUT(In a bowl to sea went wise men three) ;
  LINEOUT(On a brilliant night in June) ;
  GLUEOUT( longer, line ) ;
  LINEOUT(On fishing up the moon.) ;
  ```

- 7. Save the file, then compile the program, saving the temporary files and run the program

  ```bash
  c++ strung.cpp -save-temps -o strung.exe
  ```

![](img/bf8dbdfb89042fadbaa73b4160c74bac_163_1.png)

- 8. Open the temporary ".ii" file in a plain text editor, like Notepad, to see that the string
