# Using the finally Block

always execute, there is no need to place any statements within a special finally block.
However, statements after the catch block might never execute for at least two reasons:

+   - An Exception for which you did not plan might occur, so it is not, caught, and the program terminates.
- The try or catch block might contain a statement that terminates the application.

You can terminate an application with a statement such as Environment.Exit(0); The Environment.Exit(..) method is part of the System namespace. It terminates a program and passes the argument (which can be any integer) to the operating system. You might also exit a catch block with a break statement or a return statement. You encountered break statements when you learned about the switch statement, and you learned about return statements when you studied.

It is easily possible that a try block might throw an Exception for which you did not provide a catch. After all, exceptions occur all the time without handling them, as you saw in the first MilesPer the beginning of this chapter. In the case of an unhandled exception, program execution stops immediately, sending the error to the operating system for handling and abandoning the current method. Likewise, if the try block contains an statement, execution stops immediately. When you include a finally block, you are assured that its enclosed statements will execute before the program is abandoned, even if the method completes prematurely.

For example, the finally block is used frequently with file input and output to ensure that those files are closed. For now, however, consider the format shown in Figure 11-21, which represents part of the logic for a typical file-handling program. The catch block was written to catch an IOException, which is the type of Exception automatically generated if there is a problem opening a file, reading data from a file, or writing to a file.

```
try {
    // Open the file
    // Read the file
    // Place the file data in an array
    // Calculate an average from the data
    // Display the average
} catch(IOException e) {
    // Issue an error message
    // Exit
} finally {
    // If the file is open, close it
}
```

**Figure 11-21** Format of code that reading a file and handles an exception