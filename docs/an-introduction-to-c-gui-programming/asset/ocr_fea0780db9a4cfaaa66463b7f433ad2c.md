# DON'T #INCLUDE C FILES

#include will work on any file, it substitutes the include line with the contents of the file. Occasionally I see this being abused. some programmers bypass the use of header files by just including the other C files themselves. While this does work, it's poor practice. don't be tempted to try it!

# #define

Another useful directive is #define, which can be used to define constant values. Look at this example:

```
#include <stdio.h>

#define PI 3.14159

void main (void) {
    float rad = 3;
    float circ = rad * 2 * PI;
    float area = rad * rad * PI;
    printf("The circumference of a circle radius %f is %f\n", rad, circ);
    printf("The area of a circle radius %f is %f\n", rad, area);
}
```

The directive #define is used to set the value of PI. The important thing to remember is that PI is not a variable; it's text that will be substituted by the preprocessor. The #define line tells the preprocessor to go through the file and replace every instance of the text PI with the digits 314159 before passing it to the compiler. So a line which does something like PI = 5; will cause an error; the compiler will see the meaningless statement 3.14159 = 5;
Why is this useful? Why not declare a float variable called PI and set it to 3.14159? A floating-point variable requires allocating memory in which to store it, using #define saves that memory, which is useful if memory is limited.

You can also #define functions:

```
#include <stdio.h>
#define ADD(a,b) (a+b)
```