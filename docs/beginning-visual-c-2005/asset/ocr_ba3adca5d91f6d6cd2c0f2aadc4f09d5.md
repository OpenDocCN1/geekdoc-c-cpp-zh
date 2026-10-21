```
```cpp
{
    // Verify that arguments are not null
    assert(pFirst != 0);
    assert(pSecond != 0);

    #ifdef CONSTRUCTOR_TRACE
        // Trace constructor calls
        cout << "\nName constructor called.";
    #endif

    pFirstname = new char[strlen(pFirst)+1];
    strcpy(pFirstname, pFirst);
    pFirstname = new char[strlen(pSecond)+1];
    strcpy(pSurname, pSecond);
}
```
```

Now you are copying the strings so you should be OK now, shouldn’t you?

When you recompile the program there are some warnings about the `strcpy()` function being deprecated because it’s much better to use `strcpy_s()` but `strcpy()` does work so ignore these in this exercise. However, when you rerun the program it fails almost immediately. You can see from the console window that you got a message from the constructor, so you know roughly how far the execution went. Restart the program under the control of the debugger and you can see what happened.

# Debugging a Program

When the debugger starts, you get a message box indicating you have an unhandled exception. In the debugger, you have a comprehensive range of facilities for stepping through your code and tracing the sequence of events. Click Break in the dialog that indicates there is an unhandled exception to halt execution. The program is at the point where the exception occurred and the code currently executing is in the editor window. The exception is caused by referring to a memory location way outside the realm of the program, so a rogue pointer in our program is the immediate suspect.

# The Call Stack

The call stack stores information about functions that have been called and are still executing because they have not returned yet. As you saw earlier, the Call Stack window shows the sequence of function calls outstanding at the current point in the program. Refer to Figure 10–11.

![](bbox=[0.269, 0.737, 0.842, 0.895])

Figure 10-11