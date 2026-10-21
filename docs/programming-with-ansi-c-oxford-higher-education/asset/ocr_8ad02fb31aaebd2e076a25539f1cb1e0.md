# 8.7 THROWING VARIABLES OTHER THAN OBJECTS

It is also possible to throw other variables such as integers, chars, and strings. They can also be caught in the same way as objects. However, it is advisable to use objects to help users with more elaborate and acceptable handling of errors. At times, the object should also have member functions to solve the problem and recover from the error if possible. Suppose our function needs a file to get some input from that file. If the file is not found, the function can throw an exception as an object. The object may have a member function, which tells the user that the file it needs is not available and asks for an alternate file if available, or if file is not available, it asks the user for permission to use old data available from older fetches. It is important to note that using those member functions the user may provide generic error handling logic irrespective of the situation in which the error has occurred.

Throwing variables instead of objects is similar to the C-type error handling mechanism where we return error codes. It is similar to providing the conventional solution at a higher cost.

In Section 8.8, we will look at a few examples that show how to throw variables other than objects and catch them.

# 8.8 USING MULTIPLE catch

It is possible to use more than one catch section for a single try block. First, matching the catch block will get executed when an expression is thrown. If no matching catch block is found, the exception is passed one layer up in the block hierarchy. This has already been explained using Program 8.3.

The following program demonstrates the following:

+   1. There are multiple try blocks, one in the function and one in main as shown.
+   2. Options are provided for throwing three items, two of them being built-in data types, int and char, and the third an object of type MyException.
+   3. Two type of exceptions are caught in the function, in which case, the function call terminates in the usual way and the execution resumes in the main with a statement appearing immediately after the function call. Once an exception is caught, it would not be caught at the higher layers; the catch sections of main for char and int are, thus, not executed in this case.
+   4. The third type of exception, MyException, cannot be caught by the catch statements of the function (which can only handle int and char). Therefore, it goes up in the hierarchy and is caught by a catch statement in the main. In this case, the function call does not terminate properly and the statement after the function call is not executed. The control directly passes to the catch section of main.
+   5. The fourth type of exception is a string, for which there is no corresponding catch statement either in the function or the main. In such a case, a built-in function terminate() is called. It terminates the program with an indication of abnormal termination.
+   6. There is one throw statement in the main, which would be caught by the catch of the main(). If catch (int) in the main is removed, it will result in the same error that was obtained while sending a string exception. When an exception is thrown, if the corresponding catch is not found in the current context, it would go up in the hierarchy, and not down. So, in this case, it does not execute the catch of ExGen() if not found in the main.