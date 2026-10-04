# // USING EXCEPTIONS

The solution to dealing with unexpected, "exceptional" cases is through the use of exceptions. Here's how they work.

First, you have a function called from somewhere within a program. This call should occur within what's referred to as a try block.

Somewhere within the function that is called, you encounter an error. This is where you realize that some exceptional situation has occurred—maybe you've tried to access past the end of a vector or you had text entered instead of a number.

That function then generates an exception, which is basically a special note that something has gone wrong. In C++, the term for this idea is throwing an exception. In other programming languages, you might hear this called raising an exception.

![](bbox=[0.035, 0.695, 0.322, 0.865])

When you throw an exception, the function immediately returns. The exception is being "thrown" back to the function that called the routine.

Back in the calling function, the exception is then caught. There is separate code that is executed to handle the exception that occurred.

If you're going to deal with exceptions, you need 2 parts of code. First, you have a try block, which consists of the keyword try followed by curly braces. Whatever code is inside the curly braces is something that you will "try" to execute.

If the code executes and no exception is thrown within that code, then you go on to whatever additional code follows. On the other hand, there could have been an exception raised.

Immediately following the try block will be one or more catch blocks—used to "catch" any exception thrown when trying to execute the code in the try block, including in any functions that were called from there. The catch block will take in a parameter, which is going to be the exception that is returned.

```
try {
    // Code to try
}
catch (exception& e) {
    // Code to handle exceptions
}
// Additional code
```

In many cases, you're going to be throwing your own exceptions. But there are a few places in standard C++ where exceptions are already thrown.

Let's see how to handle exceptions in 2 cases.

The fstream library supports the ability to throw an exception in the case of trying to read from a nonexistent file.

There is a special command that has to be run for the fstream first: the member function exceptions, which basically activates the ability for fstreams to throw exceptions. The exceptions function takes in as input the exceptions that are being activated.