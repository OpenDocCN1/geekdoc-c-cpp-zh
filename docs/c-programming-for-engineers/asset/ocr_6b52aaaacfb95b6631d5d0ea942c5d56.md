# Chapter 8

# Repetition Logic

Loops are powerful tools that help you repeat tasks automatically, making them essential for efficient programming. This chapter will delve into the fundamental loop structures in C: while, do-while, and for.

# 8.1 Introduction

Loops, also called looping or iteration, allow you to execute a block of code multiple times. This is useful for repetitive tasks and simplifies your code.

Repetition is essential in programming for several reasons:

+   * **Efficiency**: Loops automate repetitive tasks, freeing you from writing the code repeatedly.
* **Flexibility**: Loops can handle changing conditions or data, making your code adaptable.
* **Cleaner code**: Loops consolidate repeated instructions, improving readability and maintenance.

Loops generally fall into two categories based on when they check the loop condition:

+   * **Pre-test Loops**: These loops check the condition before each iteration. If the condition is evaluated to true, the loop is executed. Otherwise, the loop terminates.
* **Post-test Loops**: These loops execute the code block at least once and check the condition afterward. The loop continues to iterate as long as the condition remains true.

C provides three primary loop structures, each suited for different scenarios:

+   * **The while loop (pre-test)**: This loop repeatedly executes a block of code as long as a specified condition is true. The condition is checked before each iteration.
* **The do-while loop (post-test)**: This loop ensures that the code block executes at least once, and then checks a condition afterward. The loop continues as long as the condition is true.
* **The for loop (pre-test)**: This loop is often used to iterate a specific number of times or to work with sequences. It combines initialization, condition checking, and increment/decrement steps into a single expression for concise control of the loop.

Choosing the appropriate loop type depends on the specific problem that you are trying to solve. By understanding pre-test and post-test behavior, you can effectively use these loop structures to write efficient C programs.