# The *finally* Block

A *finally* block contains code that's guaranteed to execute.<sup>12</sup> Typically, the code in a *finally* block performs the cleanup operations required by actions taken in the *try* block. For example, if you open a file in a *try* block, you'd put the code to close the file in a *finally* block:

```
~~~
private void ReadData(string pathname) {

    FileStream fs = null;
    try {
        fs = new FileStream(pathname, FileMode.Open);
        // Process the data in the file...
    }
    catch (IOException) {
        // Put code that recovers from an IOException here...
    }
    finally {
        // Make sure that the file gets closed.
        if (fs != null) fs.Close();
    }
}
~~~
```

If the code in the *try* block executes without throwing an exception, the file is guaranteed to be closed. If the code in the *try* block does throw an exception, the code in the *finally* block still executes, and the file is guaranteed to be closed, regardless of whether the exception is caught. It's improper to put the statement to close the file after the *finally* block; the statement wouldn't execute if an exception were thrown and not caught, which would result in the file being left open (until the next garbage collection).

A *try* block doesn't require a *finally* block associated with it; sometimes the code in a *try* block just doesn't require any cleanup code. However, if you do have a *finally* block, it must appear after any and all *catch* blocks. A *try* block can have no more than one *finally* block associated with it.

When a thread reaches the end of the code contained in a *finally* block, the thread simply starts executing the statements immediately following the *finally* block. Remember that the code in the *finally* block is cleanup code. This code should execute only what is necessary to clean up operations initiated in the *try* block. The code inside *catch* and *finally* blocks should be very short and should have a high likelihood of succeeding without itself throwing an exception. Usually the code in these blocks is just one or two lines of code.

It is always possible that exception-recovery code or cleanup code could fail and throw an

12 Aborting a thread or unloading an AppDomain causes the CLR to throw a `ThreadAbortException`, which allows the *finally* block to execute. If a thread is simply killed via the `Win32 TerminateThread` function, or if the process is killed via the `Win32 TerminateProcess` function or `System.Environment's FailFast` method, then the *finally* block will not execute. Of course, Windows cleans up all resources that a process was using when a process terminates.