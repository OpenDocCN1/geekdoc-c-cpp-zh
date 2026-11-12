
## Function Header

```
/********+*--*--*********--*--*--**--*--**---------*--**--*--*--**-*--**--*-*
*
*   Function Information
*
*   Name of Function:
*
*   Function Return Type:
*
*   Parameters (list data type, name, and comment one per line):
*       1.
*       2.
*       3.
*
*   Function Description:
*
********+*--*--*********--*--*--**--*--**---------*--**--*--*--**-*--**--*-*/
```

- You must insert the homework assignment header using vi's :hfx command inside Vocareum.
- With functions, it is important to comment your parameters (those values received by a function) in the header! There is insufficient room to comment parameters in the first line of the function definition and it must be included here.

## Object Names / Identifiers

- We will consider the following to be objects in this course: **variables**, **functions**, **symbolic/defined constants**. You must give your objects names that reflect their purpose in the program.

| int x;<br>int y;<br>int z; | Course Standard: Declare only one variable per line! |

- Can you determine what the variables x, y, and z accomplish for the program based only on the name of the variable? Perhaps they hold information on a 3D point? If the program contains no 3D coordinate data, then the use of x, y, and z as variable names is unclear.
- Rarely is a single character identifier for an object meaningful. A reasonable exception would be for a loop control variable used for simple counting or to access the elements of the array.
- The use of the underscore to begin an identifier is not a practice that we will use in the course.

| int numStudents;<br>float objectMass;<br>char courseGrade; | Relevant variable, constant, and function names assist in the documentation, and readability, of the logic you are attempting to implement. |

## Variable Initialization

```
int numStudents = 0;              //OKAY TO KEEP HERE
float objectMass = calcMass(acceleration, velocity); //MOVE TO EXECUTABLES
```

- In general it is acceptable to initialize a variable declared in the local declaration section of a user-defined function. If the expression used to initialize the variable is more complex than a constant assignment then it is best to give the variable its first value inside of the executable statement section of the function.

## Symbolic/Defined Constants

- THE SELECTION OF IDENTIFIERS FOR SYMBOLIC/DEFINED CONSTANTS MUST BE IN ALL CAPS. This standard allows any programmer to differentiate between a variable, a function call, and a constant that commonly occur as operands in an expression.
- Define all symbolic/defined constants at the top of your program immediately following the assignment header.
- Because the use of symbolic/defined constants can improve the documentation of a program it is a standard of the course that you attempt to **maximize** your use of symbolic/defined constants and **minimize** your use of literal constants (see chapter 3).

## Commenting

In the C programming language we have two possible implementations of comments:

- The single line comment // that will instruct the compiler to ignore everything after // to the end of the line.
- The multi-line comment /* */ that will instruct the compiler to ignore everything between the /* and */. See the headers above for an example of this type of comment. Multi-line comments cannot be nested in the C programming language.

## What must be commented?

- EVERY variable that you declare must have a brief comment to describe its purpose in the program!
  - Comment variables to the right of where they are declared in the local declaration section of a function.
- Within a given function it is expected that the occasional complex segment of code be documented in order to inform others regarding that logic you are attempting to implement.
  - For example: It is recommended that you place a line or two of comments before any significant selection or repetition construct.

## Indenting

You must indent all code inside the body of a structure **two (additional) spaces**! Rarely should you ever begin a line of code in the first column of your editor! Here are some common structures properly indented according to our standards:

| for(x = 1; x <= MAX; x++) {<br>  printf("%d", x);<br>} | if (y == 3) {<br>  for(g = 0; g > MIN; g--) {<br>    y = y - g;<br>  }<br>} | do {<br>  e = m * c * c;<br>  avg = sum/number;<br>}while(r == 0); |

## More Indenting Examples:

| Correct | Incorrect | Also Incorrect |
|---|---|---|
| if(x == 3 || y == 2) {<br>  z++;<br>  a = a - 1;<br>} | if(x == 3 || y == 2) {<br>z++;<br>a = a - 1;<br>} | if(x == 3 || y == 2) {<br>z++;<br>a = a - 1;<br>} |

Switch constructs will be indented as seen in the C text - See page 258.

## White-Spacing

- Please place an additional line between sections to help "group" the code.
- Balance the use of additional lines and failing to place any throughout your code.
  - There is no need to double space all lines of code or to include multiple consecutive blank lines.
- It is a requirement to place a space between operators and operands, such as: `y = y - g;`

## Programming Standards

There are numerous motivations for programming standards; in this course the purpose of such standards as described here is to help you develop good habits for your future programming endeavors. For some students this requirement will require breaking previously developed programming habits.

**What makes a habit or programming practice less desirable?** Anything that makes programming harder for beginners, increases the vulnerability of software to hacking or crashing, unnecessarily creates complex code, or represent features of a programming language that are becoming obsolete.

## Keep Local Declarations Separate from Executable Statements

- The default settings of the `gcc` compiler in this course requires that all variables are declared prior to the start of the executable statements. See Figure 2-2 in Chapter 2 of C text for more information.

## Scope

- VARIABLES ARE NEVER PERMITTED TO HAVE GLOBAL SCOPE.
- Do you need to share a variable with another function? Do you need a variable value to change within a function and to retain that change after the function terminates?
  - You must understand how to pass the variables/values to and return them from a user-defined function.
  - We reserve the right to assign a **score of zero** for the implementation of global variables.
- We expect in this course that all function declarations will have a global scope.
- Do not reuse an identifier with two objects that have overlapping scope.

## Symbolic/Defined Constants and other Pre-processor Directives

- All pre-processor directives must be placed at the top of your program just below the appropriate assignment header of the file.
- You can read much more about symbolic/defined constants in your C programming text (appendix G) but one purpose of a symbolic-defined constant is to make your role as programmer easier when the requirements for a program are modified in the future.

## The use of { and }

- You may observe in the C programming text that it is possible in certain situations to omit the braces around the body of structures such as `if`, `for`, and `while`. Do not develop or continue this habit! Beginners have a difficult enough time pairing up their braces and a misplaced brace can be one of the more challenging errors to resolve.
- We will discuss the **dangling else** problem in chapter 5 (page 245 of the C programming text, figure 5-14) as an example of one difficult logical error to debug when you omit the braces as we have required. You will also encounter the book's lack of { and } when you try to make sense of the sorting algorithms coded in chapter 8 of the text.

> For all relevant selection and repetition constructs in C the use of { and } is required.

## Proper Use of Repetition

- Use `for` loops only with counter-controlled processes.
- Make use of all three expressions with every `for` loop. Do not leave expressions empty or place meaningless statements in any of the expressions such as `x = x`.
- The use of the comma operator is probably unnecessary in `for` loops for this class. See page 323 of the C programming text.
- The use of perpetual loops would violate the expectation that control-forcing statements are prohibited.
- Recursion must only be used with counter-controlled processes.

## Control Forcing Statements

- **You may observe control forcing statements being used in the text but their use is prohibited within the course.** Often there are better ways to direct the control of your program without using one of the following statements:
  - `exit`, `goto`, `break` (permitted only with `switch` structures), `continue`
  - **Multiple return statements in the same function.** A function, much like the flowcharts we will discuss in lecture, must have common (only one) starting and ending point. Using multiple `return` statements enables multiple ending points for a single function (algorithm).

## Standard Libraries and Functions

- You are permitted to use many of the functions in the standard C libraries introduced in class. **It is your responsibility** for asking a course staff member about a function or library we have not discussed in class that you would like to use.

## User-Defined Functions

Once we introduce user-defined functions (chapter 4) only the following will be permitted in the `main` function of a program:

- Declaration of those variables that need to be passed between functions.
- Functions called by `main`.
- A minimum amount of control structures (loops, selection) to maintain `main` as the control center of the program.

The `main` function is intended to be _the main function_ of the program and a majority of the function calls should originate in `main`. Most of the data defined in the program should be done in `main`.

According to the definition of a function, each function must only have an individual (single) specific task. Failing to make good use of user-defined functions on relevant assignments will result in no partial credit.

All (parameters) variables declared in the first line of the function definition must have an explicit data type.

Passing individual values by address should meet the following criteria:

- When more than one value needs to be revised and that revision be retained in the calling function once the called function terminates.
- The function continues to meet the definition of being **functionally cohesive** such that it completes only a single fundamental task within the larger problem being solved.

## Declaration of Arrays

All arrays will be **static** (of fixed-length) until we introduce the topic of dynamic memory allocation in chapters 9 and 10 of the C programming text. The application of variable-length arrays as seen in the example on pages 478 – 479 will violate course standards as it permits the local declarations and executable statements in a function to overlap.

- It is unacceptable to make use of a variable to represent the size of an array in an array declaration.
- A symbolic/defined constant must be used when declaring arrays in all assignments.
