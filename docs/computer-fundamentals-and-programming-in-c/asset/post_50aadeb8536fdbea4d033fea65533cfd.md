
frequent. Other computer scientists added further principles, such as *modularization* (breaking down a program into separate procedures, such as for data input, different stages of processing, and output or printing). Modularization makes it easier to figure out which part of a program may be causing a problem, and to fix part of a problem without affecting other parts. It enables programmers to break problems into small and easily understood components that eventually will comprise a complete system.

The structured programming approach to program design was based on the following methods:

- Solving a large problem, by breaking it into several pieces and working on each piece separately
- Solving each piece by treating it as a new problem that can itself be broken down into smaller problems
- Repeating the process with each new piece until each can be solved directly, without further decomposition

Structured programming also encourages stepwise refinement, a program design process described by Niklaus Wirth, creator of Pascal. This is a *top-down approach* in which the stages of processing are first described in high-level terms (like pseudocode), and then gradually elaborated in their details. That is, the planning activities of problem solving are carried out in the direction from general to specific. Structured programming refers to the implementation of the resulting design. It requires planning and organization, but a good design will often save much time when it comes to actual implementation, and the resulting code will be more elegant and readable.

Functions form an important part of top-down design and structured programming. Using functions removes the need to repeat identical groups of statements within programs when the same task must be performed several times. Also, the use of functions allows libraries of frequently used software to be built up and re-used in different programs thus allowing the creation of compact and efficient programs.

## 12.2 CONCEPT OF FUNCTION

A function is a self-contained block of program statements that performs a particular task. It is often defined as a section of a program performing a specific job. In fact, the concept of functions, which were originally a subset of a concept called subroutine, came up because of the following deliberation.

Imagine a program where a set of operations has to be repeated often, though not continuously, n times or so. If they had to be repeated continuously, loops could be used. Instead of inserting the program statements for these operations at so many places, write a separate program segment and compile it separately. As many times as it is needed, keep ‘calling’ the segment to get the result. The separate program segment is called a function and the program that calls it is called the ‘main program’.

C went one step further; it divided the entire concept of programming into a combination of functions. C has no procedures, only functions. *scanf()*, *printf()*, *main()*, etc. that have been used in programs so far, are all functions. C provides a lot of library functions; in addition, the programmers can write their own functions and use them. The special function called *main()* is where program execution begins. When a function is called upon, with or without handing over of some input data, it returns information to the main program or calling function from where it was called.

### 12.2.1 Why are Functions Needed?

The use of functions provides several benefits.

- First, it makes programs significantly easier to understand and maintain by breaking up a program into easily manageable chunks. Even without software engineering, functions allow the structure of the program to reflect the structure of its application.
- Second, the main program can consist of a series of function calls rather than countless lines of code. It can be executed as many times as necessary from different points in the main program. Without the ability to package a block of code into a function, programs would end up being much larger, since one would typically need to replicate the same code at various points in them.
- The third benefit is that well-written functions may be reused in multiple programs. The C standard library is an example of the reuse of functions. This enables code sharing.
- Fourth, functions can be used to protect data. This is related with the concept of local data. Local data is the data described within a function. They are available only within a function when the function is being executed.
- Fifth, by using functions different programmers working on one large project can divide the workload by writing different functions.

## 12.3 USING FUNCTIONS

Referring back to the Introduction, all C programs contain at least one function, called *main()* where execution starts. Returning from this function, the program execution terminates and the returned value is treated as an indication of success or failure of program execution.

When a function is called, the code contained in that function is executed, and when the function has finished executing, control returns to the point at which the function was called. The program steps through the statements in sequence in the normal way until it comes across a call to a particular function. At that point, execution moves to the start of that function, that is, the first statement in the body of the function. Execution of the program continues through the function statements until it hits a return statement or reaches the closing brace marking the end of the function body. This signals that execution should go back to the point immediately after where the function was originally called.

Functions are used by *calling* them from other functions. When a function is used, it is referred to as the *called function*. Such functions often use data that is passed to them from the calling function. Parameters provide the means by which you pass information from the calling function into the called function. Only after the called function successfully receives the data, can the data be manipulated to produce a useful result.

### 12.3.1 Function Prototype Declaration

All the header files contain declarations for a range of functions, as well as definitions for various constants. In a C program, a user-written function should normally be declared prior to its use to allow the compiler to perform type checking on the arguments used in its call statement or calling construct. The general form of this function declaration statement is as follows:

```
    return_data_type function_name (data_type variable1, ...);
            or
    return_data_type function_name(data_type_list);
```

There are three basic parts in this declaration.

- **function_name** This is the name given to the function and it follows the same naming rules as that for any valid variable in C.
- **return_data_type** This specifies the type of data given back to the calling construct by the function after it executes its specific task.
- **data_type_list** This list specifies the data type of each of the variables, the values of which are expected to be transmitted by the calling construct to the function.

The following are some examples of declaration statements.

- (a) `float FtoC(float faren);`
- (b) `double power(double, int);`
- (c) `int isPrime(int);`
- (d) `void printMessage(void);`
- (e) `void fbo_series(int);`

A function has a name that both identifies it and is used to call it for execution in a program. The name of a function is global. Functions which perform different actions should generally have different names. The names are generally created to indicate the particular job that the function does, as is seen in examples (a) to (e).

There are two ways for prototyping functions. The most common method is simply to write the function declaration with the arguments typed, with or without identifiers for each, such as example (a), which can be written as either of the following:

```
    float FtoC(float);
    float FtoC(float faren);
```

The ANSI standard does not require variable names for the prototype declaration parameters. In fact, readability and understandability are improved if names are used.

In modern properly written C programs, all functions must be declared before they are used. This is normally accomplished using a function prototype. Function prototypes were not part of the original C language, but were added by C89. Although prototypes are not technically required, their use is strongly encouraged.

If there are no parameters to a function, you can specify the parameter list as `void`, as you have been doing in the case of the `main()` function. Actually, when a function takes no parameters, the inclusion of the word `void` inside the parentheses is optional, since it is the default. When a function returns no value, however, it is required to include `void` as the function type, since the default is `int`. If you are writing a function that returns an `int`, technically speaking you could leave out the type, but you should always include it.

**Note**

- The name of a function is global.
- It should not be forgotten that a semicolon is required at the end of a function prototype. Without it, the compiler will give an error message. Moreover, no function can be defined in another function body.
- If the number of arguments does not agree with the number of parameters specified in the prototype, the behavior is undefined.
- The function return type cannot be an array or a function type. These two cases must be handled by returning pointers to the array or function.

### 12.3.2 Function Definition

The collection of program statements in C that describes the specific task done by the function is called a *function definition*. It consists of the *function header* and a *function body*, which is a block of code enclosed in curly braces. The definition creates the actual function in memory. The general form of the function definition is as follows:

```
    return_data_type function_name(data_type variable1,
    data_type variable2,...)
    {
        /* Function Body */
    }
```

The *function header* in this definition is

```
    return_data_type function_name(data_type variable1,
    data_type variable2,...)
```
