
- A function prototype (p. 185) declares the function's name, its return type and the number, types and order of the parameters the function expects to receive.
- The general format for a function definition is

```
return-value-type function-name(parameter-list) {
    statements
}
```

If a function does not return a value, the *return-value-type* is declared as `void`. The *function-name* is any valid identifier. The *parameter-list* (p. 186) is a comma-separated list containing the definitions of the variables that will be passed to the function. If a function does not receive any values, the *parameter-list* is declared as `void`.

## Section 5.6 Function Prototypes: A Deeper Look

- Function prototypes enable the compiler to verify that functions are called correctly.
- The compiler ignores variable names mentioned in the function prototype.
- The C standard's usual arithmetic-conversion rules (p. 189) determine how arguments in a *mixed-type expression* (p. 190) are converted to the same type.

## Section 5.7 Function-Call Stack and Stack Frames

- Stacks (p. 191) are known as *last-in, first-out* (LIFO; p. 191) data structures; the last item pushed (inserted) onto the stack is the first item popped (removed) from the stack.
- A called function must know how to return to its caller, so the return address of the calling function is pushed onto the program execution stack (p. 191) when the function is called. If a series of function calls occurs, the successive return addresses are pushed onto the stack in last-in, first-out order so that the last function to execute will be the first to return to its caller.
- The program execution stack contains the memory for the local variables used in each function invocation during a program's execution. This data is known as the stack frame (p. 191) of the function call. When a function call is made, the stack frame for that function call is pushed onto the program execution stack. When the function returns to its caller, the stack frame is popped off the stack and those local variables are no longer known to the program.
- If there are more function calls than can have their stack frames stored on the program execution stack, an error known as a stack overflow occurs.

## Section 5.8 Headers

- Each standard library has a corresponding header (p. 195) containing the function prototypes for that library's functions.
- You can create and include your own headers.

## Section 5.9 Passing Arguments by Value and by Reference

- When an argument is passed by value (p. 197), a copy is made and passed to the called function. Changes to the copy do not affect the original variable's value in the caller.
- When an argument is passed by reference (p. 197), the caller allows the called function to modify the original variable's value.
- All calls in C are pass-by-value by default.

## Section 5.10 Random-Number Generation

- Function `rand` generates an integer between 0 and `RAND_MAX`, which is defined by the C standard to be at least 32767.
- Values produced by `rand` can be scaled and shifted to produce values in a specific range (p. 198).
- To randomize a program, use the C standard library function `srand`.
- The `srand` function seeds (p. 200) the random-number generator. An `srand` call is ordinarily inserted in a program only after it has been thoroughly debugged. This ensures repeatability, which is essential to proving that corrections to a random-number generation program work properly.
- The function prototypes for `rand` and `srand` are contained in `<stdlib.h>`.
- To randomize without the need for entering a seed each time, we use `srand(time(NULL))`.

```
int n = a + rand() % b;
```

where `a` is the shifting value (i.e., the first number in the desired range of consecutive integers) and `b` is the scaling factor (i.e., the width of the desired range of consecutive integers).

## Section 5.11 Example: A Game of Chance; Introducing enum

- An enumeration (p. 206), introduced by the keyword `enum`, is a set of integer constants. Values in an `enum` start with 0 and are incremented by 1. You also can assign an integer to each identifier in an `enum`. The identifiers in an enumeration must be unique, but the values may be duplicated.

## Section 5.12 Storage Classes

- Each identifier in a program has the attributes storage class, storage duration, scope and linkage (p. 207).
- C provides four storage classes indicated by the storage class specifiers: `auto`, `register`, `extern` and `static` (p. 207).
- An identifier's storage duration is when that identifier exists in memory.
- An identifier's linkage (p. 207) determines for a multiple-source-file program whether an identifier is known only in the current source file or in any source file with proper declarations.
- A function's local variables have automatic storage duration (p. 207): they're created when program control enters the block in which they're defined, exist while the block is active and are destroyed when program control exits the block.
- Keywords `extern` and `static` declare identifiers for variables and functions of static storage duration. Static storage duration (p. 207) variables are allocated and initialized once, before the program begins execution.
- There are two types of identifiers with static storage duration: external identifiers (such as global variables and function names) and local variables declared with the storage-class specifier `static`.
- Global variables are created by placing variable definitions outside any function definition. Global variables retain their values throughout the program execution.
- Local static variables retain their value between calls to the function in which they're defined.
- All numeric variables of static storage duration are initialized to zero by default.

## Section 5.13 Scope Rules

- An identifier's scope (p. 209) is where the identifier can be referenced in a program.
- The purpose of information hiding is to give functions access only to the information they need to complete their tasks. This is a means of implementing the principle of least privilege.
- An identifier can have function scope, file scope, block scope or function-prototype scope (p. 209).
- Labels are the only identifiers with function scope. Labels can be used anywhere in the function in which they appear but cannot be referenced outside the function body.
- An identifier declared outside any function has file scope. Such an identifier is "known" in all functions from the point at which it's declared until the end of the file.
- Identifiers defined inside a block have block scope. Block scope ends at the terminating right brace (`}`).
- Local variables have block scope, as do function parameters, which are local variables.
- Any block may contain variable definitions. When blocks are nested, and an identifier in an outer block has the same name as an identifier in the inner block, the identifier in the outer block is "hidden" until the inner block terminates.
- The only identifiers with function-prototype scope are those used in the parameter list of a function prototype.

## Section 5.14 Recursion

- A recursive function (p. 212) is a function that calls itself either directly or indirectly.
- If a recursive function is called with a base case (p. 212), the function simply returns a result. If it's called with a more complex problem, it divides the problem into two conceptual pieces: a piece that the function knows how to do and a slightly smaller version of the original problem. Because this new problem looks like the original, the function launches a recursive call to work on the smaller problem.
- For recursion to terminate, each time the recursive function calls itself with a slightly simpler version of the original problem, the sequence of smaller and smaller problems must converge on the base case. When the function recognizes the base case, the result is returned to the previous function call, and a sequence of returns ensues all the way up the line until the original call of the function eventually returns the final result.
- Standard C does not specify the order in which the operands of most operators (including `+`) are to be evaluated. Of C's many operators, the standard specifies the order of evaluation of the operands of only the operators `&&`, `||`, the comma (`,`) operator and `?:`. The first three of these are binary operators whose two operands are evaluated left-to-right. The last operator is C's only ternary operator. Its leftmost operand is evaluated first; if it evaluates to non-zero, the middle operand is evaluated next and the last operand is ignored; if the leftmost operand evaluates to zero, the third operand is evaluated next and the middle operand is ignored.

## Section 5.16 Recursion vs. Iteration

- Both iteration and recursion are based on a control structure: Iteration uses an iteration statement; recursion uses a selection statement.
- Both iteration and recursion involve repetition: Iteration uses an iteration statement; recursion achieves repetition through repeated function calls.
- Iteration and recursion each involve a termination test: Iteration terminates when the loop-continuation condition fails; recursion terminates when a base case is recognized.
