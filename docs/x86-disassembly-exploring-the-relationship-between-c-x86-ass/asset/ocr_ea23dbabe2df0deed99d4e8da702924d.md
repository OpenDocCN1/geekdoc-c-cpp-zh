# Variables

+   2. Signed variables use signed branch instructions as jge and jl. Unsigned variables use unsigned branch instructions as jae, jb.

The difference between signed and unsigned instructions is the conditions under which the various flags for greater-than or less-than (overflow) flags are set. The integer result values are exactly the same for signed and unsigned data.

# 17.6 Floating-Point Values

Floating point values to be 32-bit data values (for float) or 64-bit data values (for double). These values are distinguished from ordinary integer-valued variables because they are used with floating-point instructions. Floating instructions typically start with the letter f. For instance, fadd, fcmp, and similar instructions are used with floating point values. In particular note are the float instruction and variants. These instructions take integer-valued variable and convert it into a floating point variable.

We will discuss floating point variables in more detail in a later chapter.

# 17.7 Global Variables

Global variables do not have a limit scope lexical variables inside inside function body. Since the notion of lexical scope in nature, they are typically not found on the stack. Global variables are not lexical in nature tend to exist in the program as a hard-coded memory address, which never changes throughout program execution. This could exist in the DATA segment of the executable, or anywhere else a hard-coded memory address can be used to store data.

In C, global variables are defined outside the body of any function. There is no "global" keyword. Any variable which is not defined inside a function is global. In C however, a variable which is not defined inside a function is only global to the particular source code file in which it is defined. For example, we have two files Foo.c and Bar.c, and a global variable MyGlobalVar:

| Foo.c | Bar.c |
|---|---|
| int MyGlobalVar; | int GetVar(void) |
| int GetVar(void) | { |
| //right! | //wrong! |
| return MyGlobalVar; | return MyGlobalVar; |
| | |

In the example above, the variable MyGlobalVar is visible the file Foo.c, but is not visible inside the file Bar.c. To make MyGlobalVar visible inside all project files, we need to use the extern keyword, which we will discuss below.