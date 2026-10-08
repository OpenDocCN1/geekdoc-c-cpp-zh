
# 15.1.1 Telling your code to do the right thing

tell you about it quickly. This is important because it is much easier to fix a bug shortly after you have written it. You may even find that you can hardly remember precisely what code changes you have made after a couple of hours have passed. This will obviously make debugging much harder. To help with this, write lots of unit tests and make sure all your tests are run whenever you change your code (see Section 15.4.5).

As important as telling you which parts of your code are currently not working, unit tests tell you which parts of your code are working. If you have a million lines of code, knowing which parts of code you need to think about is extremely important.

Whenever you discover a bug in your code that wasn't picked up by a unit test you should write a unit test to make sure it never happens again. You should never write new code unless you are also writing tests for it.

> **Tip: Write a little, test a little.**

Do not write large amounts of code in one sitting. Write a small amount of code. Write some tests. Make sure everything compiles and all the tests pass. Then back up your code using your version control system (see Section 15.4.1). That way when an error occurs you should have a clear idea of what you are doing that might have caused it.

### 15.1.2 Reading your code

Often the quickest way to find a bug in your code is to read it through. This approach will only work if you know already which function contains the error as you cannot possibly re-read all your code every time a bug occurs. However, if you are following the strategy of writing a little and testing a little, you can usually guess that the bug is in the code you have just written.

Very often it helps to explain your code to someone else. A very effective development practice is to write your code with a colleague. This is called pair programming [1]. You will find that you and your colleague both learn from each other and that many bugs are spotted before the code is even executed.

Some people suggest an alternative practice called code-review, where developers read each other's code and comment on it. This is much less enjoyable than pair programming and, it is argued in [1], much less effective.

### 15.1.3 Logging statements

You have probably already discovered for yourself the strategy of inserting logging statements throughout your code. By printing out the values of different variables at each line, one can often quickly work out what is going wrong.

You may find that you are regularly inserting and deleting logging statements from your code as bugs are found and fixed. The `DEBUG_PRINT` macro from our testing framework is meant to help with this as it allows you to switch debugging on and off without needing to actually delete the lines. See Section 15.4.6 for a brief discussion of other logging frameworks.

### 15.1.4 Using a debugger

The error messages produced by C++ when it is running can be very unhelpful. Sometimes a program will crash without providing any clue as to where in the code the problem occurred.

A *debugger* is a tool that helps alleviate this problem.

Recall that the compiler turns your C++ code into machine code. During this process, the code turns from something you wrote and understand into something that you didn’t write and don’t understand. This is a serious problem. To alleviate the problem, you can compile your code with additional debugging information that links your source code to the machine code that is being executed.

If you have compiled your program with the necessary debugging information, then it is possible to run your program inside a debugger. The debugger will then allow you to step through your code line by line to see what is happening. It will also translate between the machine code and your source code so you can understand what is going on. In addition you can tell the debugger to pause the execution whenever an error is detected. This allows you to gather detailed information about the cause of the error. We will describe how to use the Visual Studio debugger on Windows in Section 15.2, and how to use the GDB debugger on Unix in Section 15.3. Other debuggers work in a similar way. You should consult their documentation.

### 15.1.5 Divide and conquer

If you have a difficult bug to fix, it can be very useful to know the following algorithm for debugging code.

- (i) By considering which of your unit tests pass and which fail, decide which area of your code contains the error.
- (ii) Consider how to divide the code that contains the bug into two roughly equally sized pieces. What tests can you run to determine which of these two pieces actually contains the error?
- (iii) Write the tests. Repeat this process until you have fixed the bug.

The important point is that one should not look at all your code and read through it. This approach is very time-consuming and unlikely to work. Instead, this approach uses a *divide and conquer* strategy. At each stage we halve the size of the problem.

To see the difference, imagine your program contains one million lines of code. Reading the code through clearly takes one million steps. Let us be honest, you will fall asleep and miss the bug. The divide and conquer strategy might require writing $\log_2(1000000) \approx$ 20 tests before you find the problem. This is clearly much better. It has the additional advantage that you will be increasing the size of your test suite as you work. This means that next time a bug occurs, you should be able to find it far more quickly.

# 15.2 Debugging with Visual Studio

This section describes how to use the debugger built into Visual Studio. If you are developing on Unix using command line tools, you should read Section 15.3 instead.

If you are using some other debugger, you should consult its documentation for the precise details of how to debug your code. Nevertheless, this section may be useful to you as an indication of the key things to look for when debugging.

When debugging your code in Visual Studio, you should select “Debug” from the drop-down menu on the Toolbar. This drop-down menu gives the choice of compiling and running either “Debug” or “Release” versions of your software. As the names suggest, the Debug version is very useful for development purposes. The Release version eliminates most of the code that helps with debugging, resulting in software that runs considerably faster.

Before launching the debugger, you should configure the debugger so that it will pause the execution of our program whenever an exception is thrown by our code. To do this select Debug → Exceptions… from the main menu. Then click the box to indicate that the debugger should pause the execution whenever C++ exceptions are thrown.

You can now compile and run the program in the debugger by pressing F5. If you compile and run FMLib in this way, an error will occur and the execution of the program will be paused. It is important to know that when you start the debugger by pressing F5, Visual Studio will operate as a debugger rather than as a compiler until your program has exited. This means that you shouldn’t try and edit or compile your code until your program has stopped. If you want to stop debugging at any point press Shift + F5 or select Debug → Stop debugging from the main menu. However, we do not want to stop debugging just yet. Instead let us read the error messages and use the debugger.

### 15.2.1 Obtaining a stack trace in Visual Studio

You will see an error message similar to the one shown in Figure 15.1. This error message tells you that the error was detected in the file vector at line 1201. The file **vector** is part of the C++ library, so we can be confident that the bug didn’t actually *occur* in the **vector** class, but that it was *detected* by the **vector** class. A useful rule of thumb is that if an error occurs, it is your code that is wrong and not the libraries that you are using.

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_271_0.png)

**FIGURE 15.1:** An assertion failed message generated on Windows.

If you click **Retry**, another window will appear asking you if you want to break or continue. “To break” simply means to pause the execution of your code so you can view it in the debugger. This is precisely what we want to do, so select **Break**.

The execution of your program is now paused and you can use Visual Studio to find out what caused the error. The most interesting part of the display is a Window labelled **Call Stack**. It should look as shown in Figure 15.2.

![](img/c60a618fcc2a2ed9d1e8d96a1b4157ff_271_1.png)

**FIGURE 15.2:** The call stack at the first bug in FMLib.

The call stack shows you what functions are executing. The second-to-last line of the call stack tells us that the function **main** is executing. It is currently on line 44 at which point it called testHedgingSimulator. You can see this
