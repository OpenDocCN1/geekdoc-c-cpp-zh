
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

Now you are copying the strings so you should be OK now, shouldn’t you?

When you recompile the program there are some warnings about the `strcpy()` function being deprecated because it’s much better to use `strcpy_s()` but `strcpy()` does work so ignore these in this exercise. However, when you rerun the program it fails almost immediately. You can see from the console window that you got a message from the constructor, so you know roughly how far the execution went. Restart the program under the control of the debugger and you can see what happened.

## Debugging a Program

When the debugger starts, you get a message box indicating you have an unhandled exception. In the debugger, you have a comprehensive range of facilities for stepping through your code and tracing the sequence of events. Click Break in the dialog that indicates there is an unhandled exception to halt execution. The program is at the point where the exception occurred and the code currently executing is in the editor window. The exception is caused by referring to a memory location way outside the realm of the program, so a rogue pointer in our program is the immediate suspect.

## The Call Stack

The call stack stores information about functions that have been called and are still executing because they have not returned yet. As you saw earlier, the Call Stack window shows the sequence of function calls outstanding at the current point in the program. Refer to Figure 10–11.

![](img/2359b0c604600c58fba3539c738a356e_626_0.png)

Figure 10-11

The sequence of function calls outstanding runs from the most recent call at the top, the library function strcat(), down to the Kernel32 calls at the bottom of the window in Figure 10-11. Each function was called directly or indirectly by the one below it, and none of those displayed have yet executed a return. The Kernel32 lines are all system routines that start executing prior to our main() function. Your interest is the role of your code in this, and you can see from the second line down in the window that the Name class constructor was still in execution (had not returned) when the exception was thrown. If you double-click on that line, the Editor window displays the code for that function, and indicates the line in the source code being executed when the problem arose, which in this case is:

```
strcpy(pSurname, pSecond);
```

This call caused the unhandled exception to be thrown — but why? The original problem is not necessarily here; it just became apparent here. This is typical of errors involving pointers. Take a look at the window showing the values in the variables in the context of the Name constructor that is presently displayed in the Editor pane. Figure 10-12 shows how it looks.

![](img/2359b0c604600c58fba3539c738a356e_627_0.png)

Figure 10-12

Because the context is a function that is a member of the Name class, the Autos window displays the this pointer that contains the address of the current object. The pSurname pointer contains a weird address, 0xcccccccc, that corresponds to 3435973836 in decimal! Because I have rather less than 3 billion bytes of memory, it looks a bit unlikely, and the debugger recognizes that pSurname has got to be a rogue pointer and has marked it as such. If you look at pFirstname, this is also in a mess. At the point where you are in the code (copying the surname) the first name should already have been copied, but the contents are rubbish.

The culprit is in the preceding line. Hasty copying of code has resulted in allocating memory for pFirstname for a second time, instead of allocating space for pSurname. The copy is to a junk address, and this causes the exception to be thrown. Don’t you wish you had checked what you did, properly? The line should be:

```
pSurname = new char[strlen(pSecond)+1];
```

It is typically the case that the code causing a bad pointer address is not the code where the error makes itself felt. In general it may be very far away. Just examining the pointer or pointers involved in the statement causing the error can often lead you directly to the problem, but sometimes it can involve a lot of searching. You can always add more debug code if you get really stuck.

Change the statement in the Editor window to what it should be and recompile the project with the change included. You can then restart the program inside the debugger after it has been recompiled by clicking the button on the Debug toolbar, but surprise, surprise-you get another unhandled exception. This undoubtedly means more pointer trouble, and you can see from the output in the console window that the last function call was to getNameLength():

```
Name constructor called.
Name::getName() called.
The name is Horton
Name::getNameLength() called.
```

The output for the name is definitely not right; however, you don’t know where exactly the problem is. Restarting and stepping through the program once more should provide some clues.

## Step Over to the Error

The getNameLength() function is currently displayed in the Editor pane and the debugger has indicated that the following line is where the problem arose:

```
return strlen(pFirstname)+strlen(pSurname)+1;
```

In the Call Stack window, you can see that the program is in the getNameLength() function member, which merely calls the strlen() library function to get the overall length of the name. The strlen() function is unlikely to be at fault, so this must mean there is something wrong with part of the object. The Autos window showing the variables in the context of this function shows that the current object has been corrupted, as you can see in Figure 10-13.

![](img/2359b0c604600c58fba3539c738a356e_628_0.png)

The current object is pointed to by this, and by clicking the plus symbol alongside this you can see the data members. It’s the pSurname member that is the problem. The address it contains should refer to the string “Horton,” but it clearly doesn’t. Further, the debugger has flagged it as a bad pointer.

On the assumption that this kind of error does not originate at the point where you experience the effect, you can go back, restart the program, and single step through, looking for where the Name object gets messed up. You can select Step Over or press F10 to restart the application, and single step through the statements by repeatedly pressing F10. After executing the statement that defines the myName object, the Autos window for the main() function shows that it has been constructed successfully, as you can see in Figure 10-14.

## Chapter 10

![](img/2359b0c604600c58fba3539c738a356e_629_0.png)

Figure 10-14

Executing the next statement that outputs the name corrupts the object, myName. You can clearly see that this is the case from the Autos window for main() in Figure 10-15.

![](img/2359b0c604600c58fba3539c738a356e_629_1.png)

Figure 10-15

On the reasonable assumption that the stream output operations work OK, it must be your getName() member doing something it shouldn’t. Restart the debugger once more, but this time use Step Into when execution reaches the output statement. When execution is at the first statement of the getName() function, you can step through the statements in the getName() function using Step Over. Watch the context window as you progress through the function. You will see that everything is fine until you execute the statement:

```
strcpy(pName+strlen(pName)+1, pSurname);  // Append second name after the space
```

This statement causes the corruption of pSurname for the current object, pointed to by this. You can see this in the Autos window in Figure 10-16.

![](img/2359b0c604600c58fba3539c738a356e_629_2.png)

Figure 10-16
