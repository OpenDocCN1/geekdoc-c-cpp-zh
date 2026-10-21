Change the statement in the Editor window to what it should be and recompile the project with the change included. You can then restart the program inside the debugger after it has been recompiled by clicking the button on the Debug toolbar, but surprise, surprise-you get another unhandled exception. This undoubtedly means more pointer trouble, and you can see from the output in the console window that the last function call was to getNameLength():

```
Name constructor called.
Name::getName() called.
The name is Horton
Name::getNameLength() called.
```

The output for the name is definitely not right; however, you don’t know where exactly the problem is. Restarting and stepping through the program once more should provide some clues.

# Step Over to the Error

The getNameLength() function is currently displayed in the Editor pane and the debugger has indicated that the following line is where the problem arose:

```
return strlen(pFirstname)+strlen(pSurname)+1;
```

In the Call Stack window, you can see that the program is in the getNameLength() function member, which merely calls the strlen() library function to get the overall length of the name. The strlen() function is unlikely to be at fault, so this must mean there is something wrong with part of the object. The Autos window showing the variables in the context of this function shows that the current object has been corrupted, as you can see in Figure 10-13.

![](bbox=[0.29, 0.54, 0.8, 0.7])

The current object is pointed to by this, and by clicking the plus symbol alongside this you can see the data members. It’s the pSurname member that is the problem. The address it contains should refer to the string “Horton,” but it clearly doesn’t. Further, the debugger has flagged it as a bad pointer.

On the assumption that this kind of error does not originate at the point where you experience the effect, you can go back, restart the program, and single step through, looking for where the Name object gets messed up. You can select Step Over or press F10 to restart the application, and single step through the statements by repeatedly pressing F10. After executing the statement that defines the myName object, the Autos window for the main() function shows that it has been constructed successfully, as you can see in Figure 10-14.