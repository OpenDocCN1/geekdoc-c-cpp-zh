```
char newChar = (static_cast<int>(str[i]) - base + 3) % 26 + base;
try
{
    str.replace(i, 1, newChar);
}
catch (out_of_range e)
{
    cout << "No character at position " << i << endl;
    // end try-catch
} // end encodeChar
```

The call encodeString(99, str) within main causes 99 calls to encodeChar, and hence the exception is thrown 98 - str.length() times. The following output from encodeChar is the result.

```
No character at position 99
No character at position 98
No character at position 97
...
```

When the exception was not handled, the program terminated the first time the exception occurred. Handling the exception allows the code to continue execution.

Although the out_of_range exception is thrown in the function encodeChar, that is not necessarily the best place to handle the exception. For example, if the client had made the call encodeString(10000, str), the message printed by encodeChar would have appeared 9999 - str.length() times! In this case, it makes more sense for the try and catch blocks to appear in the function encodeString and not in encodeChar, as follows:

```
void encodeString(int numChar, string& str)
{
    try
    {
        for (int i = numChar - 1; i >= 0; i--)
            encodeChar(i, str);
    }
    catch (out_of_range e)
    {
        cout << "The string does not contain " << numChar;
        cout << " characters." << endl;
        cout << e.what() << endl;
    } // end try-catch
} // end encodeString
```

Now when encodeChar throws the exception out_of_range, the exception propagates back to the function encodeString, which ends execution of the statements in the try block and executes the statements in the catch block. The expression e.what() invokes the method what for the exception e, and so it represents a string that describes the exception. For this example, the following output would be displayed.

```
The string does not contain 10 characters.
invalid string position
```

The message is printed only once, since the for loop is inside the try block, which is abandoned when the exception occurs. If the try block had been placed inside the for loop, encodeChar would be called—and therefore the exception would be thrown and handled—at each iteration of the loop. The result would be multiple copies of the message.