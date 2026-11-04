At worst, it will produce incorrect results or expose weird behavior that may go unnoticed for a long time, only making matters worse. When you use exceptions, if no one handles the exception, your program will terminate its execution.

Contradictory as it might seem, making applications crash in the face of errors that are not dealt with is a much better scenario. Although the *reliability* of a program that does sloppy exception handling is lower, it's without doubt more *robust*. Think about it this way: The most correct program is the one that doesn't do anything rather than the one that continues its merry way, producing bad results.

# **MORE EXCEPTION HANDLING THAN YOU MAY THINK!**

In the example shown here, there's more hidden exception handling going on due to the use of the *using* statement. Recall from Chapter 8, “Basics of Exceptions and Resource Management,” that the *using* block gives rise to a *try-finally* statement, ensuring proper disposal of the resource it acquired on the first line. Just as with exceptions, this results in a clear block-based structure of code, here to eliminate the need of a manual approach to resource cleanup. This is structured programming at its best.

# # Exception Handling

We start our journey through the world of exceptions by taking a look at the most common developer activity related to exceptions: structured handling of exceptions. The key ingredient to this is the use of the *try-catch-finally* statement. But first, we'll ensure a proper understanding of the way exceptions flow in the system. Figure 23.1 shows the execution flow depending on whether an exception occurred, which was illustrated earlier in Chapter 8, “Basics of Exceptions and Resource Management,” Figure 8.19.

![](bbox=[0.062, 0.615, 0.95, 0.899])

**FIGURE 23.1** Flow of exceptions through a try-catch-finally statement.