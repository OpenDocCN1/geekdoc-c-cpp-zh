# Scope Rules

If this declaration is inside the definition of a function, as in Display 3.5, the name TAXRATE is local to the function definition, which means outside the definition of the function that contains the declaration, you can use the name TAXRATE for another named constant, or variable, or anything else.

On the other hand, if this declaration were to appear at the beginning of your program, outside the body of all the functions (and outside the body of the main part of your program), the named constant is said to be a global named constant and the named constant can be used in any function definition that follows the constant declaration.

Display 3.9 shows a program with an example of a global named constant. The program asks for a radius and then computes both the area of a circle and the volume of a sphere with radius, using the following formulas:

```
area = π × (radius)²nvolume = (4/3) × π × (radius)³
```

Both formulas include the constant π, which is approximately equal to 3.14159. The symbol π is the Greek letter called "pi." The program uses the following global named constant,

```
const double PI = 3.14159;
```

which appears outside the definition of any function (including outside the definition of main).
The compiler allows you wide latitude in where you place the declarations for your global named constants. To add readability, however, you should place all your includes together, and all global named declarations together in another group, and all your function declarations (function prototypes) together. We will follow standard practice and place all global named constant declarations after our include and using directives before our function declarations.

Placing named constant declarations at the start of your program can be ideal if the named constant is used by only one function. If the named constant might need to be changed in a future version of your program, it will be easier to find if it is at the beginning of your program. For example, placing the constant declaration for the sales tax rate at the beginning of an accounting program will make it easy to revise the program to change the tax rate.

It is possible to declare ordinary variables, without the const modifier, as global variables, which are accessible to all function definitions in the file. This is done similar to the way it is done for global named constants, except that the modifier const is not used in the variable declaration. However, there is seldom need to use such global variables. Moreover, global variables can make a program harder to understand and maintain, so we advise you to avoid using them.