# Chapter 10
Functions

Functions in C provide a way to encapsulate a block of code that performs a specific task or calculation. They promote code modularity, reusability, and enhance program organization and readability by breaking down complex tasks into smaller, manageable units.

# 10.1 Basics of Functions

Functions are essential building blocks of programming that encapsulate reusable code segments. They simplify development by consolidating common tasks and avoiding code duplication.

Key benefits of functions include:

+   - **Modularity**: Functions allow you to break down your code into smaller, more manageable modules
- **Reusability**: Frequently used code can be packaged into reusable function units, reducing redundancy.
- **Readability**: Functions enhance code readability and maintenance. Each function serves a clear purpose and is named appropriately, making the code more self-explanatory.
- Testing/debugging: Isolating logic into functions aids testability and debugging.
- **Productivity**: Functions facilitate collaboration among programmers and promote code reuse, boosting productivity.

There are two main types of functions:

+   - **User-defined function**: Created by the programmer to address specific needs.
- **Library function**: Predefined by the compiler for common tasks.

# 10.2 User-Defined Functions

A user-defined function groups code to perform a specific task, and this group is given a name (identifier). When the function is invoked from any part of the program, it executes the code defined in the body of the function.

# 10.2.1 Function Declaration and Definition

A function begins with its **declaration**, where essential details like its name, return type, and parameters are specified to the compiler. Subsequently, in the function's **definition**, the actual code for performing the specified task is provided. Every function consists of three main parts: declaration, definition, and usage or calling.