
time the sequence is again executed after the execution of instruction I4. Instead of writing redundant code, we can create a separate function, say, `sub_seq()`, which contains the sequence `S1`, `S2`, `S3`. The programmer can simply invoke the function `sub_seq()` whenever it is required to execute the instructions `S1`, `S2`, `S3` in the program. Syntax to create the function `sub_seq()` is very much similar to the way we create `main()` function, except that the name of the function in this case is `sub_seq()` as shown below. Such functions are called **user-defined functions**. You are free to give any name to the function which is defined by you. The rules for naming functions are the same as the rules for naming variables mentioned in Chapter 2, Section 2.5.5.

```c
void sub_seq()
{
S1;
S2;
S3;
}
```

A function will not get executed until and unless it is invoked. We must explicitly call (invoke) the function `sub_seq()` whenever we wish to execute the instructions `S1`, `S2`, `S3`. After the function is **called**, the control of execution is transferred inside the function body, and hence the statements `S1`, `S2`, and `S3` will be executed in the sequence as we have written inside the function. Once the last statement of the function is executed, the control of execution will return to the **next statement** after the function call to continue the execution of the remaining part of the `main()` function.

In this case, the sequence `S1`, `S2`, `S3` repeats twice in the `main()`, and hence instead of actually writing it two times we can invoke the function `sub_seq()` at each place in the `main()` where we wish to execute the said sequence. As shown in Figure 7.4, we “call” the function `sub_seq()` after instruction I2, because this is one of the places in the `main()` function where we wish to execute the sequence.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_316_0.png)

After the function is ‘called’, the control of execution is transferred to the function `sub_seq()`, thereby executing the statements `S1`, `S2`, `S3` after I2. After the execution of the function `sub_seq` completes, the control returns to `main()` at the next statement after the function call (which is I3) and resumes the execution of the `main()` function from the statement that sequence `S1`, `S2`, `S3` is executed exactly between the two statements I2 and I3, which is exactly our requirement.

The statements I3 and I4 are executed after the function `sub_seq()` completes its first execution. There is a second call made to the function `sub_seq()` after I4; hence, the execution of sequence `S1`, `S2`, `S3` will be repeated after I4. Once the function `sub_seq()` is completed, the control returns to the next statement after the function call, which is this time I5. The execution of the `main()` function resumes from I5 as seen in Figure 7.5. This flow of control ensures that the statements `S1`, `S2`, `S3` are executed exactly between I4 and I5.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_317_0.png)

**Figure 7.5:** Calling `sub_seq()` twice

## Is `main()` a user-defined function?

Yes. `main()` is also a user-defined function. The execution of every program always starts from the `main()` function. It represents the start and end of the program, and it is a function which is recognized by the compiler. When you execute your program, the compiler invokes the `main()` function and starts the execution of the code from the first line of `main()`. Other user-defined functions should be invoked by the programmer explicitly, whereas `main()` is implicitly invoked by the compiler when you compile and execute your code. Hence, `main()` must be written in a format which is recognized by the compiler. One of the formats in which `main()` can be written is what we have been using throughout this textbook, as given below:

```c
void main()
{
/*operations*/
}
```

There are some more formats in which `main()` can be coded, and they are discussed later in this chapter. However, we will always use the above style of creating `main()` in this textbook, unless there is a specific need to use any other format.

As execution always starts from `main()`, any other function that we wish to execute must be "called" either from the `main()` function or from some other function which can be reached through `main()` in at least one execution flow.

**REMEMBER**

- A function is a subroutine which contains a sequence of statements to be executed to perform a specific operation.
- A function can have multiple inputs (called arguments) and generate a single output (called **return value**).
- Functions are used to avoid redundancy of code in the program, thereby reducing lines of code and simplifying the change management process.
- Structured programming (also called modular programming) is a programming technique wherein a large program is split into different functions (modules) such that each of the functions performs a specific operation. The operation a particular function performs is called the **service** provided by that function. Any function F1 in the program can invoke some other function F2 if F1 needs the services provided by F2.

## 7.2 Creating Functions

Figure 7.6 gives the syntax for creating user-defined functions. As a first example to understand the syntax, let us create a simple function without any arguments and return values. We will work with arguments and return values later in this chapter. Let us create a function `add()` that prints the result of addition of the two numbers on the computer screen. The syntax for creating a function `add()` is very similar to creating `main()` function, with the only difference that the name of the function is given as `add()` instead of `main()` as seen in Figure 7.7. The keyword **void** indicates that the function `add()` does not return any value to the caller after its execution. The argument list is empty because we do not intend to pass any arguments to the `add()` function.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_318_0.png)

**Figure 7.6:** Syntax for creating a function

*Remember*, the execution of the program always starts from the `main()` function; hence, `add()` will not be executed unless it is called from the `main()`. We create a `main()` function which calls the `add()` as shown in Figure 7.8.

The statement

```c
add();
```

is a **function call** to `add()` function. The function is always called using its name followed by the parentheses and then a semicolon. The parentheses are empty because `add()` does not accept any arguments. Due to this call, the control of execution should ideally be transferred to the function definition of `add()`. However, this does not happen because function `add()` is defined after `main()` and the C/C++ compiler makes it mandatory to declare every function defined after `main()` before it can be called. Hence, it is mandatory to declare `add()` as a function before making a function call. Declaration of a function is called **function prototype**. Prototyping a function is not necessary if we define the function before `main()`; it is mandatory only when the function is defined after `main()`.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_319_0.png)

**Figure 7.7:** Function definition of `add()`

![](img/57c0d966bb33c67a5a188e6bf39e4e02_319_1.png)

**Figure 7.8:** `main()` function defined along with the `add()` function

Hence, we have two options to make the code work:

- 1. Include function prototype of `add()` in the program.
- 2. Define function `add()` before `main()`: In this case prototyping `add()` is not mandatory.

To understand option 1, we need to know what is a function prototype? We know that C/C++ does not support forward referencing. This means that you cannot use a variable in the program before its declaration. The general rule is that an identifier can be used only after its declaration. The same is true with functions. You cannot call a function `add()` without declaring (prototyping) it. The ‘function prototype’ informs the compiler about the exact way in which the function `add()` is defined later in the program.

Prototype includes the following information about the function:

- 1. Name of the function
- 2. Return type of the function
- 3. Data type and order of the arguments of the function

The syntax for function prototyping is as shown in Figure 7.9.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_320_0.png)

C/C++ makes it mandatory that every function which is defined after `main()` must always be prototyped before `main()` function starts, so that the compiler has a complete understanding of the way in which the function is defined later in the program before its call. At the time of compilation, the compiler checks if the call made to the function follows the rules defined in the ‘function prototype’. If the ‘function call’ correctly fulfils the rules of ‘function prototype’, then the compilation process is marked successful.

This means that before calling the function `add()` from the `main()` function, we must prototype the function `add()` to give the following information to the compiler:

- 1. **Name of the function:** The name of the function specified in the prototype should exactly match with the name that is given in the ‘function definition’ appearing after `main()`.
