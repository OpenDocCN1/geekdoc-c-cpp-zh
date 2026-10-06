# Chapter 3

# Modules

be written as several small modules, one performing a specific part of the task. These small modules can then be executed in the desired order to perform the overall task.

This approach is sometimes called divide and conquer a large task is divided into several smaller tasks that are easily performed. Figure 3-1 illustrates this idea by comparing two programs: one uses a long, complex sequence of statements to perform a task, and another that divides a task into smaller tasks, each of which is performed by a separate module.

When using modules in a program, you generally isolate each task within the program in its own module. For example, a realistic calculating program has the following modules:

+   - A module that gets the employee's hourly pay rate
- A module that gets the number of hours worked
- A module that calculates the employee's gross pay
- A module that calculates the overtime pay
- A module that calculates the withholdings for taxes and benefits
- A module that calculates the net pay
- A module that calculates the paycheck

Although every modern programming language allows you to create modules, they are not always referred to as modules. Modules are procedures, subroutines, subprograms, methods, and functions. A function is a special type of module that you will discuss in Chapter 6.)

# Benefits of Using Modules

A program benefits in the following ways when it is modularized:

# Simpler Code

A program's code tends to be simpler and easier to understand when it is modularized. Several small modules are much easier to read than one sequence of statements.

# Code Reuse

Modules reduce the duplication of code within a program. If a specific operation is performed in several places in a program, a module can be written once to perform that operation, and then be executed any time it is needed. This benefit of modules is known as code reuse because you are writing the code to perform a task once and reusing it each time you need to perform the task.

# Better Testing

When each task within a program is contained in its own module, testing and debugging become simpler. Programmers can test each module in a program individually, to determine whether it correctly performs its operation. This makes it easier to isolate and fix errors.

# Easier Maintenance

Most programs must be periodically modified to correct logic errors, improve performance, and provide a better experience for the user. Such modifications are known as maintenance. A modularized program is easier to maintain than an unmodularized program because its code tends to be simpler, smaller, and easier to understand.