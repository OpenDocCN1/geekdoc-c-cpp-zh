
## Q6. What is the purpose of nested loops in C program?
- Q7. Explain with example the significance of continue and goto statements.
- Q8. What do you understand by forward and backward jumps in context of goto statement?
- Q9. Justify the statement that It is not recommended to use goto statements for modifying execution control flow.
- Q10. State whether the following statements are true or false:
    - i. In a pretest loop, the control statement is checked when we exit the loop.
    - ii. Event-controlled loops stop when an event mentioned in the control statement occurs.
    - iii. for( I = 0 ; ; I++ ); is a valid C statement.
    - iv. A for loop can replace a do while loop.
    - v. The statement for ( :ctr < 10 : { printf("\n %d", ctr++);} ) is an example of entry-controlled loop.
    - vi. for( : ; ) loop will execute infinitely.
    - vii. In a while loop, the statement continue; transfers the execution control flow to the control statement of while loop, but in the for loop, the execution control flow goes to the variable update statement.
    - viii. The forward jump transfers the execution control flow to a statement above the goto statement.
    - ix. Infinite loops are created because the condition within the control statement never becomes true.
    - x. We cannot use a while loop within a for loop.

## Practical Exercises

- Q1. Write a program to find out the smallest value of N such that 1 + 1/2 + 1/3 + 1/4 + ... + 1/N > Limit. The value of Limit is to be entered by the user.
- Q2. Write a program to find the largest power of an entered number N, which is less than or equal to another given number M. For example, if N=3 and M=11, then the answer is 2 as 3^2 <= 11.
- Q3. Write a program to accept an integer N. Evaluate the value of series 1 + 1/2^2 + 1/3^3 + 1/4^4 + ... + 1/N^N.
- Q4. Write a program to accept an integer value from a user until a value 999 is entered, count total number of odd, and even numbers (excluding 999) from the numbers entered.
- Q5. Write a program to accept an integer NUM1 from a user. Accept another integer NUM2 from the user until the user enters 0, and count total number of times the integer NUM1 appears in the list of NUM2.
- Q6. Write a program that uses event-controlled do-while loop to enter numbers and count the number of positive, zero, and negative numbers.
- Q7. Write a program that uses event-controlled while loop and switch structure to check whether the entered character is a special character, a number, or an alphabet.
- Q8. Write a program to generate a series aa, abc, abb, abcd, abcc, abcde for first N elements of this series.
- Q9. Write a program to accept an integer N. Generate a series of first N positive odd numbers.
- Q10. Write a program to accept an integer N. Generate a series of first N prime numbers.
- Q11. Write a program to accept an integer N. Calculate the sum of all even numbers and all odd numbers within the range 1 to N.
- Q12. Write a program that accepts an integer N from the user. Extract and display each digit of the integer in English. For example, if the user enters 132, then the program should display "one three two."
- Q13. Write a program that accepts an integer N. Reverse the number entered and store it in the same variable. For example, if N=456, then the new value of N is 654.
- Q14. Write a program that accepts an integer N. Sum all the digits of the number entered. For example, if N=470, then sum of digits N is 11.
- Q15. Write a program that accepts an integer N; if the integer N=9, then print the pyramid shown in the following:

```
1
121
12321
1234321
123454321
12345654321
1234567897654321
```

The pyramid should get modified based on the value of N. For negative values, print the appropriate message.

- Q16. Write a program that accepts a character C; if the character C=e, then print the pyramid as shown in the following:

```
a
bab
cbabc
dcbabcd
edcbabcde
```

The pyramid should get modified based on the value of C. For characters that are not alphabet, print the appropriate message.

- Q17. Write a program that accepts an integer N; if integer N=5, then print the pyramid as shown in the following:

```
5 5 5 5 5
4 4 4 4
3 3 3
2 2
1
```

The pyramid should get modified based on the value of N. For negative values, print the appropriate message.

- Q18. Write a program that accepts an integer N; if the integer N=4, then print the pyramid shown in the following:

```
1
2  2
3  3  3
4  4  4  4
```

The pyramid should get modified based on the value of N. For negative values, print the appropriate message.

- Q19. Write a program to print the Floyd’s triangle shown in the following:

```
1
2  3
4  5  6
7  8  9  10
11 12 13 14 15
:
79...91
```

- Q20. Write a program that accepts an integer N; if the integer N=4, then print the pyramid shown in the following:

```
*
**
***
****
****
***
**
*
```

The pyramid should get modified based on the value of N. For negative values, print the appropriate message.

# 08 Functions

**OBJECTIVES**

- Describe Structured Programming Approach
- Describe Functions in C
- Describe Categories of C Function
- Describe Types of Function
- Describe Parameter Passing in Function
- Describe Recursive Function
- Describe Command-Line Arguments
- Describe Storage Classes
- Describe Advantages of Functions

The programs discussed in earlier chapters of this book were very simple programs with few lines of code. In real-life scenario, the size of the program code is very large. For example, assume an application of banking. In case of banking application, the code size of a program may run into thousands of lines. If we create a single code file in such a case, it will be very difficult to understand, maintain, and manage this code. A better approach to programming is to break the single file code into set of files so that it is easy to understand, maintain, and manage the application. In this chapter, we will learn about the concept of structured programming. We will learn about functions in C and their types and categories. Then we explore the recursive function and command line argument. We will also learn how C language facilitates structured programming and how a C language program can be written in a better way. Finally, we will learn about the advantages of functions.

## 8.1 Structured Programming Approach

Around 1972, Edsger Dijkstra, a Dutch computer scientist, popularized a theory known as structured programming. The theory was based on the concept that, to solve any problem efficiently, we need to first break down the problem into small parts. Each of the small parts was known as module. Thus, a program would then consist of a set of modules. To break down the problem into a set of modules, we need to have an overall picture of the problem. The overall picture of the problem can be obtained using a structure chart, and this approach of designing a structure chart is known as top-down approach of design. We all know that a program consists of three functionalities, namely, an input, a process, and an output. Figure 1 illustrates a structure chart for breaking a single program into three different modules:

![Figure 1](img/5d422ba7108ffdf64376be51eaf0c459_167_0.png)

▲ Figure 1: Structure Chart for Breaking a Single Program

In Figure 1, the main program represents the entire code to solve the problem. The input module, process module, and output module are at second level of the structure chart. Thus, to complete the entire code, we will have to first code the input module, the process module, and the output module. Once the codes of these modules are ready, we will combine them together to form a single source code. The job of the input module is to get data from the user; the job of the process module is to perform the required operation on the data obtained, and the output module provides the results in the desired format to the user.

The execution of the program here starts from the main program. The main program then calls the input module that accepts data from the user. Then, it passes the data to the process module by calling it. Finally, the output module prints the information on the monitor. To make this method success, the modules need to interact with each other. The interaction between two modules happens by means of passing a message between each other. The two message passing mechanism used in structured programming are passing a data and passing a reference. Both these methods will be discussed later in this chapter. The next section discusses how C language implements modularity within a program.

## 8.2 Functions in C

In C language, the idea of structured programming is implemented using a concept called functions. A C program consists of one or more functions, one out of which has to be a function named main. Each function implements particular aspect of a large problem. For example, a function named input may accept the data required for the execution program. The execution of a C program always starts from and ends at the function main. To execute a C program, the operating system calls the function main, and the function main, in turn, can call other functions if required. Once the work of the main function is completed, the control is transferred back to the operating system.

Normally, a function may accept one or more inputs and returns at most one output. The function at times can cause side effect of different forms. A side effect is an indication of an action that changes the state of the program. For example, after the evaluation of an expression, a change in the value of an identifier used in the expression indicates a side effect. The next section discusses the components of C function.

### Components of C function

A C function is made up of different entities such as function name, number of parameters it accepts, number of parameters it returns, data type of the parameter, and so on. Figure 2 shows the components of a C function:
