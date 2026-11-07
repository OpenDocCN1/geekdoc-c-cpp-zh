```
```cpp
done = true;                              //Line 13
cout << "Line 14: Number = " << number     //Line 14
     << endl;                               //Line 15
}
catch (string messageStr)                  //Line 16
{
    cout << "Line 18: " << messageStr       //Line 18
         << endl;                           //Line 19
    cout << "Line 19: Restoring the"        //Line 19
         << "input stream.";                //Line 20
    cin.clear();                             //Line 21
    cin.ignore(100, '\n');                   //Line 22
}
}
while (!done);                              //Line 23

return 0;                                    //Line 24
}
```
```

**Sample Run:** In this sample run, the user input is shaded.

```
Line 8: Enter an integer: r5

Line 18: The input stream is in the fail state.
Line 19: Restoring the input stream.
Line 8: Enter an integer: d45

Line 18: The input stream is in the fail state.
Line 19: Restoring the input stream.
Line 8: Enter an integer: hw3

Line 18: The input stream is in the fail state.
Line 19: Restoring the input stream.
Line 8: Enter an integer: 48

Line 14: Number = 48
```

This program prompts the user to enter an integer. If the input is invalid, the standard input stream enters the fail state. In the `try` block, the statement in Line 12 throws an exception, which is a string object. Control passes to the `catch` block, and the exception is caught and processed. The statement in Line 20 restores the input stream to its good state, and the statement in Line 21 clears the rest of the input from the line. The `do...while` loop continues to prompt the user until the user inputs a valid number.

# Log the Error and Continue

The program that terminates when an exception occurs usually assumes that this termination is reasonably safe. However, if your program is designed to run a nuclear reactor or continuously monitor a satellite, it cannot be terminated if an exception occurs. These programs should report the exception, but the program must continue to run.