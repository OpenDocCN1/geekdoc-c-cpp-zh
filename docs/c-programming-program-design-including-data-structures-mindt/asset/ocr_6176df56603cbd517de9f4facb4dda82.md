```
```cpp
if (!cin)                         //Line 15
    throw str;                     //Line 16

done = true;                       //Line 17
cout << "Line 18: Number = " << number  //Line 18
     << endl;
}                                  //Line 19
catch (const char messageStr[])     //Line 20
{                                  //Line 21
    cout << "Line 22: " << messageStr  //Line 22
         << endl;
    cout << "Line 23: Restoring the "  //Line 23
         << "input stream." << endl;
    cin.clear();                    //Line 24
    cin.ignore(100, '\n');          //Line 25
}                                  //Line 26
}                                  //Line 27
while (!done);                     //Line 28

return 0;                          //Line 29
}                                  //Line 30
```
```

**Sample Run:** In this sample run, the user input is shaded.

```
```text
Line 12: Enter an integer: c4

Line 22: The input stream is in the fail state.
Line 23: Restoring the input stream.
Line 12: Enter an integer: s7

Line 22: The input stream is in the fail state.
Line 23: Restoring the input stream.
Line 12: Enter an integer: 28

Line 18: Number = 28
```
```

This program prompts the user to enter an integer. If the input is invalid, the standard input stream enters the fail state. In the try block, the statement in Line 16 throws an exception, which is a string. Control passes to the catch block, and the exception is caught and processed. The statement in Line 24 restores the input stream to its good state, and the statement in Line 25 clears the rest of the input from the line. The do...while loop continues to prompt the user until the user inputs a valid number.

# Log the Error and Continue

The program that terminates when an exception occurs usually assumes that this termination is reasonably safe. However, if your program is designed to run a nuclear reactor or continuously monitor a satellite, it cannot be terminated if an exception occurs. These programs should report the exception, but the program must continue to run.