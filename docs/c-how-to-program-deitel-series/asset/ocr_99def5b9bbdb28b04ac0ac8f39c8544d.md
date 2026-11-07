```
```cpp
// function1 uses an empty parameter list to specify that
// the function receives no arguments
void function1()
{
    cout << "function1 takes no arguments" << endl;
} // end of function1

// function2 uses a void parameter list to specify that
// the function receives no arguments
void function2( void )
{
    cout << "function2 also takes no arguments" << endl;
} // end of function2
```
```

function1 takes no arguments  
function2 also takes no arguments

**Fig. 6.18** | Functions that take no arguments. (Part 2 of 2.)

# 6.14 Inline Functions

Implementing a program as a set of functions is good from a software engineering standpoint, but function calls involve execution-time overhead. C++ provides **inline functions** to help reduce function call overhead. Placing the qualifier **inline** before a function’s return type in the function definition *advises* the compiler to generate a copy of the function’s body code in *every* place where the function is called (when appropriate) to avoid a function call. This often makes the program larger. The compiler can *ignore* the inline qualifier and generally does so for all but the *smallest* functions. Reusable inline functions are typically placed in headers, so that their definitions can be included in each source file that uses them.

> **Software Engineering Observation 6.9**  
> *If you change the definition of an inline function, you should recompile all of that function’s clients.*

> **Performance Tip 6.4**  
> *Compilers can inline code for which you have not explicitly used the inline keyword. Today’s optimizing compilers are so sophisticated that it’s best to leave inlining decisions to the compiler.*

Figure 6.19 uses inline function cube (lines 9–12) to calculate the volume of a cube. Keyword **const** in function cube’s parameter list (line 9) tells the compiler that the function does *not* modify variable side. This ensures that side’s value is not changed by the function during the calculation. (Keyword const is discussed in detail in Chapters 7–9.)

> **Software Engineering Observation 6.10**  
> *The const qualifier should be used to enforce the principle of least privilege. Using the principle of least privilege to properly design software can greatly reduce debugging time and improve side effects and can make a program easier to modify and maintain.*