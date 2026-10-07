When you follow this planned approach, you quickly make a list of discrete tasks that your program needs to perform. Then you can tackle the tasks one at a time, giving all your attention to one relatively simple task. When that function is written and working properly, you can move to the next task. Before you know it, your program starts to take shape.

# The Top-Down Approach

By structured programming, C programmers take the top-down approach. You saw this as illustrated in Figure 5.2, where the program’s structure remains an inverted tree. Many times, most of the real work of the program is performed by the functions at the tips of the “branches”. The functions closer to the “trunk” primarily direct program execution among these functions.

As a result, many C programs have a small amount of code in the main body of the program—that is, in main(). The bulk of your program’s code is found in functions. main(), all you might find a few dozen lines of code that direct program execution among the functions. Often, a menu is presented to the person using the program. Program execution is branched according to the user’s choices. Each branch of the menu uses a different function.

> NOTE: Using menus is a good approach to program design. Lesson 13, “Advanced Program Control,” shows how you can use the switch statement to create a versatile menu-driven system.

Now that you know what functions are and why they’re so important, the time has come for you to learn how to write your own.

| DO | DON'T |
|---|---n| DO plan before starting to code. | DON'T try to do everything in one function. A single function should perform a single task, such as reading information from a file. |
 determining your program’s structure | |
 ahead of time, you can save time | |
 writing the code and debugging it. | |