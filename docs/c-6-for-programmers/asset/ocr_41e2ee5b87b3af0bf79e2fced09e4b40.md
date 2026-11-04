The Exception Assistant window contains

+   * a line pointing from the Exception Assistant to the line of code that caused the exception,
+   * the type of the exception,
+   * **Troubleshooting tips** with links to helpful information on what might have caused the exception and how to handle it, and
+   * links to view or copy the complete exception details

Figure 13.3 shows the Exception Assistant that's displayed if the user attempts to divide by zero in the app of Fig. 13.1.

# ### 13.3.4 Termination Model of Exception Handling

Recall that the point in the program at which an exception occurs is called the *throw point*—this is an important location for debugging purposes (as we demonstrate in Section 13.7). If an exception occurs in a try block (such as a FormatException being thrown as a result of the code in lines 19 and 21 in Fig. 13.2), the try block terminates immediately, and program control transfers to the first of the following catch blocks in which the exception parameter's type matches that of the thrown exception. After the exception is handled, program control does *not* return to the throw point because the try block has *exited* (which also causes any of its local variables to go out of scope). Rather, control resumes after the last catch block. This is known as the termination model of exception handling. [*Note*: Some languages use the resumption model of exception handling, in which, after an exception is handled, control resumes just after the throw point.]

If no exceptions occur in the try block, the program successfully completes the try block (setting continueLoop to false) and ignores the catch blocks in lines 32–37 and 38–43. Then the program executes the first statement following the try and catch blocks. In this example, the program reaches the end of the do…while loop (line 44) in which the condition is now false, so the program terminates because the end of Main is reached.

The try block and its corresponding catch and finally blocks together form a try statement. It's important not to confuse the terms “try block” and “try statement”—the term “try block” refers to the block of code following the keyword try (but before any catch or finally blocks), while the term “try statement” includes all the code from the opening try keyword to the end of the last catch or finally block. This includes the try block, as well as any associated catch blocks and finally block.

When a try block terminates, its local variables go out of scope. If a try block terminates due to an exception, the CLR searches for the first catch block that can process the type of exception that occurred—in an outer block in the same method or in a previous method in the method-call stack. The CLR locates the matching catch by comparing the type of the thrown exception to each catch's parameter type. A match occurs if the types are identical or if the thrown exception's type is a derived class of the catch's parameter type. Once an exception is matched to a catch block, the code in that block executes and the other catch blocks in the try statement are ignored.

# ### 13.3.5 Flow of Control When Exceptions Occur

In the third sample output of Fig. 13.2, the user inputs hello as the denominator. When line 21 executes, int.Parse cannot convert this string to an int, so the method throws