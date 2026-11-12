
## Main Memory

- The memory of a computer will store the **data and instructions** of the programs that we will write this semester.

- You may have made the observation that the capacity of primary memory (RAM, 8-16 GB) on your personal machine is quite small in comparison to the size of your secondary memory (hard drive, 1 or more TB).

- Therefore, not every instruction or data associated with the currently executing program can be stored in primary memory, but, when instructions or data are needed, they must be **fetched, or retrieved**, from the hard drive and brought in to primary memory for use.

- Similar to addresses of homes on a street, the memory of the computer has addresses at which instructions and data can be located.

- In our programs we will select names that are meaningful to us as programmers rather than referencing a specific address in memory to represent and locate data.

## Processing Instructions

- The CPU executes instructions using a process known as the instruction cycle.

## Instruction Cycle Diagram:

| Why is secondary memory slower than primary memory? | If primary memory is faster then why not grow the capacity of this level and eliminate secondary memory? |
|---|---|
| - Many secondary devices still have moving or mechanical parts.<br>- Further physical distance from the CPU (or machine).<br>- Increased time required to locate specific content in a high capacity device. | - The current model is an economic one for consumers. |

## Natural Languages versus Machine Languages

- When we describe problems that we wish to solve we do so in a **natural language**.

- **Natural languages** are spoken and have evolved over centuries in accordance with their usage.

- **Natural languages** are full of attributes that are unfit for use by a computer.

## The Idea of a Programming Language

To give instructions to a computer this semester, we will use a **programming language**, in particular, the C programming language. The C programming language is composed of keywords that come from a natural language but are used without the ambiguity. Initially the C programming language syntax will look foreign to you as a beginner, but it is completely unreadable by the computer!

The computer has its own language, called a **machine language** that it can interpret as instructions specific to the individual machine that will perform the task. This machine language is written only in 0's and 1's because the internal circuits of a computer are made of switches, transistors, and other electronic devices can be in one of two states: off (0) or on (1).

It didn't take long for programmers to recognize that coding in a machine language is very challenging and the entire process of developing, debugging, and maintaining instructions in a machine language is not something most would enjoy doing. A process of evolution away from a machine language towards a natural language has been ongoing and has resulted in the programming languages of today.

## Natural Languages

![](img/50641bd70680c74d7c49fe705f0d8389_29_0.png)

- **High-Level Languages**
- Use natural language elements that are easier to use, understand, and develop.
- Do not rely on specific hardware.

- **Low-Level Languages**
- Instructions written specifically for the hardware of one machine cannot be used easily on a different machine.
- Requires the programmer to consider the algorithm in small, incremental steps.
- Programmer left with the task of managing memory.

## Machine Languages

How does the computer understand these high level programming languages if all a computer instructions are composed of 0's and 1's (binary numbers)?

## Creating and Running Programs

To answer the previous question we must explore the process of turning a C program into a file that can be executed on the local machine.

## The programming process is composed of steps which are repeated many times during development:

![](img/50641bd70680c74d7c49fe705f0d8389_29_1.png)

## Writing and Editing the Program

The first step is writing the program (actually, the first step is developing your solution, but we are describing the implementation of the solution at this time) which will require the use of a piece of software known as a text editor. The text editor of choice for this semester will be vi (pronounced vee-eye). If you insist on another editor then you assume responsibility for understanding its operation and any potential compatibility issues with our server. We find the use of vi to be a powerful one for writing code. Please understand that there is a learning curve to vi, but with enough practice you too will be working with vi comfortably!

## Saving the Changes

Please keep in mind the importance of saving your work regularly! Too many students in the past have lost a significant amount of unsaved work by a dropped connection, frozen computer, or power outage because they failed to save their work as they progressed.

- You should test your work regularly too! It is easy to write a lot of code and then only to find numerous errors or such a poor initial direction that correcting all of the problems would be more difficult than starting over!
- Testing regularly should not imply you should create your solution while coding, but it cannot be stressed enough that when you write code it should be nothing more than the implementation of a well designed algorithm. Without planning, your solution is reduced to development through trial and error which tends to be an inefficient and frustrating process.
- It is possible to make multiple-submissions for a given assignment. However, it is only the last submission that is kept for grading. ALL previous submissions are over-written and cannot be restored.

> In your collaborative lab groups, and for each lab assignment, you must designate a single individual who will make all submissions for the group.

Example: Assume we are implementing the solution to a problem and have progressed in our coding to the point that we want to test what we have input so far.

What should be done next?

1. Save the work to make sure the source file containing our C code has been stored and reflects our most recent changes.
2. Send the source file to the compiler so that the instructions within can be prepared for execution by the computer.

## The Compiler

The compiler is in a category of software that is used to convert the source programming language code into the machine language of the computer.

## Syntax

Syntax is the set of rules of the programming language. The compiler will attempt to validate your source code with the syntax of the C programming language as it creates a new executable file.

Violating the rules of the syntax may result in an error in which no new executable file can be created.

The compiling process has one particular phase of interest to us:

- The **preprocessor** - reads the source code and prepares it for the translator. There are special instructions known as **preprocessor directives** that you can give the preprocessor to prepare the source code for translation.

On our server all of the steps of the compiling process are completed with a single instruction which leave many transparent to the programmer.

## Process of Implementing Code

## Program Execution (Testing/Running the Executable File)

Upon successful compilation an executable file will be created. By default the name of this executable file is `a.out`. To execute, or run, the program you need only type `a.out` at the UNIX prompt. It is assumed that you are in the same directory as the `a.out` file while testing the program.

Each time you modify the source file you must recompile the code and create a new `a.out` to see the changes as reflected in your source code. A new executable file will replace any previously existing one. In most cases keeping the old executable file is not desired.

- If compilation of your program fails no new executable file will be created.
- A failed compilation attempt may not result an existing `a.out` file being removed/deleted.

## Program Development

Our goal in CS 159: to be able to develop solutions in the form of logical algorithms as solutions to problems without considering any specific syntax of the programming language that you may potentially use.

Exposure to good programming practices is important to introduce the methods necessary to designing "a program that produces correct results, is well-designed, is efficient, and adheres to documentation and programming standards of the course."
