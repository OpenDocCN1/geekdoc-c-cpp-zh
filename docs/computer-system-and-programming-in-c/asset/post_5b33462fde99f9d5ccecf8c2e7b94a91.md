
- 4. Write a program in C to check whether the given number is even or odd.
- 5. Write a program in C to check whether the given number is positive, negative or zero.
- 6. Write a program in C to check whether the given character is upper, lower, number or not.
- 7. Write a program in C to check whether the character is upper, lower, number or not.
- 8. Write a program in C to change upper to lower.
- 9. Write a program in C to change lower to upper.
- 10. Write a program in C to print a word form of given number between 0 to 9.

## Section C

*Long Answer Type Questions*

- 1. Write a program in C to print a word form of given number is tens between 1 and 99.
- 2. Write a program in C for relational operations of two given integer numbers.
- 3. Write a program in C for relational operations of two given float numbers.
- 4. Write a program in C for given mark contain which grade.
- 5. Write a program in C to find biggest of two given numbers.
- 6. Write a program in C to find smallest of two given numbers.
- 7. Write a program in C to find biggest of three given numbers.
- 8. Write a program in C to find smallest of three given numbers.
- 9. Write a program in C to find biggest of three given numbers using && operator.
- 10. Write a program in C to find smallest of three given numbers using && operator.
- 11. Write a program in C to show the name of the day in a week. Here given input range is 1 – 7.
- 12. Write a program in C to find a biggest of four given numbers.
- 13. Write a program in C to find a smallest of four given numbers.
- 14. Write a program in C to find a vowel or not of given character.
- 15. Write a program in C to find biggest of two numbers using ternary operator.
- 16. Write a program in C to find smallest of two numbers using ternary operator.
- 17. Write a program in C to find biggest of three numbers using ternary operator.
- 18. Write a program in C to find smallest of three numbers using ternary operator.

## 10 Modular Programming

Structured programming (sometimes known as *modular programming*) is a subset of procedural programming that enforces a logical structure on the program being written to make it more efficient and easier to understand and modify. Certain languages such as Ada, Pascal, and dBase are designed with features that encourage or enforce a logical program structure.

Structured programming frequently employs a top-down design model, in which developers map out the overall program structure into separate subsections. A defined function or set of similar functions is coded in a separate module or sub-module, which means that code can be loaded into memory more efficiently and that modules can be reused in other programs. After a module has been tested individually, it is then integrated with other modules into the overall program structure.

Program flow follows a simple hierarchical model that employs looping constructs such as “for,” “repeat,” and “while.” Use of the “Go To” statement is discouraged.

Structured programming was first suggested by Corrado Bohm and Giuseppe Jacopini. The two mathematicians demonstrated that any computer program can be rewritten with just three structures: decisions, sequences, and loops. Edsger Dijkstra’s subsequent article, *Go To Statement Considered Harmful*, was instrumental in the trend towards structured programming. The most common methodology employed was developed by Dijkstra. In this model (which is often considered to be synonymous with structured programming, although other models exist) the developer separates programs into subsections that each has only one point of access and one point of exit.

In the modular programming concept we will discuss the concept of functions in C Language.

### USE OF FUNCTIONS IN MODULAR PROGRAMMING

Almost any language can use structured programming techniques to avoid common pitfalls of unstructured languages. Unstructured programming must rely upon the discipline of the developer to avoid structural problems, and as a consequence may result in poorly organized programs. Most modern procedural languages include features that encourage structured programming. Object-oriented programming (OOP) can be thought of as a type of structured programming, uses structured programming techniques for program flow, and adds more structure for data to the model.

To make the programming simple and easy to debug, we break a larger program into smaller subprograms which perform ‘well-defined tasks’. These subprograms are called functions. So far we have defined a single function main ( ). After reading this unit you will be able to define many other functions and the main ( ) function can call up these functions from several different places within the program, to carry out the required processing. Functions are very important tools for *Modular Programming*, where we break large programs into small subprograms or modules (functions in case of C). The use of functions reduces complexity and makes programming simple and easy to understand.

In this chapter, we will discuss how functions are defined and how they are accessed from the main program. We will also discuss various types of functions and how to invoke them. And finally you will learn an interesting and important programming technique known as *Recursion*, in which a function calls itself.

Programmers know that a program written with numerous functions is easier to maintain, update and debug than one very long program. By programming in a modular (functional) fashion, several programmers can work independently on separate functions which can be assembled at a later date to create the entire project.

Ideally, your `main()` function should be very short and should consist primarily of function calls. Each function has its own name. When that name is encountered in a program, the execution of the program branches to the body of that function. When the function is finished, execution returns to the area of the program code from which it was called, and the program continues on to the next line of code.

### DEFINITION OF A FUNCTION

A *function* is a self-contained block of executable code that can be called from any other function. In many programs, a set of statements are to be executed repeatedly at various places in the program and with different sets of data, the idea of functions comes in mind. You keep those repeating statements in a function and call them as and when required. When a function is called, the control transfers to the called function, which will be executed, and then transfers the control back to the calling function (to the statement following the function call).

When we divide a complex program into various modules then that particular various modules are called as functions. We have mentioned earlier that one of the strengths of C language is that C functions are easy to define and use. C functions can be classified into two categories, namely, library functions and user-defined functions. main is an example of user defined function. printf and scanf belong to the category of library functions. The main distinction between user-defined functions and library functions is that the former are required to be written by the user while the latter are not required to be developed by the user at the time of writing a program. However, the user defined function can become a part of the C program library.

A *function* is a subprogram that acts on data and often returns a value. You are already familiar with the one function that every C program possesses: `int main(void)`. Good C programmers write programs that consist of many of these small functions. Thus, graphically the function calling is represented as follows:

![](img/7792ede0bb69d5dc5a8d6bd4f54bd008_194_0.png)

### TYPES OF FUNCTION

Functions are classified into the following two categories:

- (A) User defined functions
- (B) Predefined functions

In this chapter we will discuss the concept of user-defined functions.

### ADVANTAGES OF USING FUNCTIONS

The use of functions in C serves many advantages:

- 1. It facilitates top-down modular programming. In this programming style,
