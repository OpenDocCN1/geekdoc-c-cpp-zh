
# Building the Project

You compile your code from the Build menu. You may compile your code from any one of the following different menu choices:

- Build | Solution
- Rebuild | Solution
- Build | HelloWorld
- Rebuild | HelloWorld

HelloWorld is the name of your project. A solution may contain more than one project. Here the solution contains only one project, so there is no practical difference between the project and the solution.

Build means to compile changes from the last compilation (if there was one). Rebuild means to start compilation from the beginning. Build is therefore faster, but Rebuild is used when there have been extensive changes since the last compilation. As a practical matter, it rarely makes a difference which you choose.

Before compile, make one change to the code, changing cout to Cout (capitalizing the C). Choose one of the four compilation options. A Task List window would display, a binding error, as shown in Figure 1-12. The error description in the Task List window is error C2065: 'Cout' : undeclared identifier.

![](img/59a3417a6d5906fae6d8000d4c2cff76_29_0.png)

Figure 1-12: The Task List window showing a compilation error

> If the description column is not wide enough to show the entire error description, you can display the error description in a pop-up window by right-clicking the error description and choosing Show Description or Show Tooltip from the shortcut menu.

As explained in the earlier section on the Compiler, the compiler can understand your code and translate it into machine language only if your code is in the proper syntax for programming language. As explained there, C++ has rules for the spelling of words and for the grammar of statements. If there is a violation of those rules, it is a syntax error, then the compiler cannot translate your code into machine language unless you pay attention to the errors.

In C++, case is sensitive. If a variable is named the same as a word it will be uncitalized. The correct spelling is cout; Cout is wrong. C++ does not know what Cout, you get the error message that it is an "undeclared identifier."

While the code is short, if your code is quite lengthy, it is not easy to spot where the error is in the code. If you double-click the error in the Task List, then a cursor will blink at the line where Cout, and an icon will display in the main (as shown in Figure 1-13).

![](img/59a3417a6d5906fae6d8000d4c2cff76_30_0.png)

Figure 1-13: The error highlighted in the code window

Now change Cout to cout, and then compile your code again. This time compilation should be successful. Using Windows Explorer, you can now see in the Debug folder of your HelloWorld project folder file hello.obj and another file hello.exe. These are the object and executable files previously discussed in the section "Translating the Code for the Computer." Accordingly, building the project involved the preprocessor, the compiler, and the linker.

# Running the Code

The final step is to run the code. You do so from the Debug menu. You may choose either Debug | Start | Without Debugging. The difference is whether you wish to use the debugger, an issue which we will discuss in a later chapter. Since we are not going to use the debugger this time, choose Debug | Without Debugging (shown way back in Figure 1-1). The result is the console window displaying "Hello World!"

- **Team LiB**

- **PREVIOUS NEXT**

# Summary

Computers store huge amounts of information, recall that information quickly and accurately, and perform calculations with lightning speed and perfect accuracy. However, computers cannot think by themselves, and need step-by-step instructions from telling them what to do. These instructions are called a computer program, written by a human computer programmer in a programming language such as C++. A compiler, together with a preprocessor and a linker, translates the computer program into machine language that a computer understands.

We then analyzed a C++ program, which outputs "Hello World!" to the screen. The program looks simple, but much is going on behind the scenes. We analyzed code, line by line. You then created and ran your own "Hello World!" C++ application.

# Quiz

- 1. What is a computer program?
- 2. Name several advantages a computer has over humans in processing information?
- 3. What is a programming language?
- 4. Why is C++ a good programming language to learn?
- 5. What is a function?
- 6. How many main functions should a C++ program have?
- 7. What is a standard library file?
- 8. What is the purpose of an include directive?
- 9. What does a preprocessor do?
- 10. What does a compiler do?
- 11. What does a linker do?

# Chapter 2: Memory and Data Types

# Overview

After I wrote my first book, I expected every day for mail, hoping to receive requests for my autograph. The result was proof of the adage "be careful what you ask for." My mailbox was stuffed with numerous requests for my autograph. Alas, these requests came from those who wanted to share my memory, not my fame. My autograph was requested on checks to pay my mortgage, credit cards, insurance, phone service, electricity; well, you get the picture.

These companies who love sending me bills could possibly keep track of their thousands of customers by using pencil and paper. Instead, they use computer programs, which harness the computer's ability to store very large amounts of information and to retrieve that information very quickly.

We use our memory to store and recall information. So do computers. However, a computer's memory is very different from ours. This chapter will explain how a computer's memory works.

Information, also called data, comes in different forms. Some data is numeric, such as the amount of my gas bill. Other data is, such as my name on my gas bill. The type of data, whether numeric, text, or something else, quite literally is referred to as the "data type." The data type you choose will affect not only the form in which the data is stored, but also the amount of memory required to store it. This chapter will explain the different data types.

# Memory

Computer programs consist of instructions and data. As discussed in Chapter 1, instructions, written in a programming language such as C++ and then translated by the compiler and linker into machine language, give the computer step-by-step directions on what to do. Data is the information that is the subject of the program. For example, if the user of your computer program runs a list of all students with a GPA of 4.0, the data could follow instructions to determine and output the list of all students with a GPA of 4.0.

The computer programs' instructions and data have be in the computer's memory for the program to work. This section will explain the different types of computer memory, as well as how and where instructions and data are stored.

# Types of Memory

There are three principal memory locations on your computer.

- The central processing unit (CPU)
- Random access memory (RAM)
- Persistent storage

# Cache Memory

The CPU is the brains of the computer. You might have thought about the CPU when you last considered purchasing a computer, since the CPU's speed often an important purchase decision. The faster the CPU's speed, the faster your computer runs.

> A herz, named Heinrich Hertz, who first detected electromagnetic waves, represents one cycle per second. CPU speed is measured in megahertz (MHz), which represents one million cycles per second, or gigahertz (GHz), which represents 1 billion cycles per second. For example, a CPU that runs at 800 MHz executes 800 million cycles per second. Each CPU speed determines how many instructions per second the CPU can execute.

The CPU, in addition to coordinating the computer's operations, has memory, cache memory. The CPU's memory includes a segment called a register. This memory is used to store used instructions and data.

The CPU can access cache memory extremely quickly because it doesn't have to go far; the memory is on the CPU. However, the amount of available cache memory is quite small; there is only room for the most frequently used instructions and data. The remainder of the instructions and data have to be stored somewhere else.

# Random Access Memory

Somewhere else is random access memory, or RAM. You may also have considered RAM when you purchased a computer, since the more RAM a computer has, the more programs it can run at one time, and the faster it runs.
