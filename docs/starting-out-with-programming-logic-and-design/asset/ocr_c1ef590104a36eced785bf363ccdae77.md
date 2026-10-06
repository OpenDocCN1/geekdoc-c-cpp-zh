# 7.3 Defensive Programming 277

the length of a string, you use the length function discussed in Chapter 6. In the following pseudocode, the length function is used to make sure a password is at least six characters long.

```
// Get the new password.
Display "Enter your new password."
Input-password
// Validate the length of the password.
While length(password) < 6
    Display "The password must be at least six"
    Display "characters long. Enter your new password."
    Input-password
End While
```

# Checkpoint

+   7.3 Describe the steps that are generally taken when an input validation loop is used to validate data.
7.4 What is a priming read? What is its purpose?
7.5 If the input that read by the priming read is valid, how many times will the input validation loop iterate?

# 7.3 Defensive Programming

**CONCEPT:** Input validation is part of the practice of defensive programming. Thorough input validation anticipates both obvious and obvious errors.

Defensive programming is the practice of anticipating errors that can happen while a program is running, and designing the program to avoid those errors. All of the input validation algorithms examined in this chapter are examples of defensive programming.

Some types of input errors are obvious and easily handled. For example, you should make sure that negative numbers are not entered for items such as prices and test scores. Some types of input errors are not obvious, however. One example of an error reading empty input, which happens when an input statement attempts to read data, there is no data to read. This occurs when an Input statement executes and the user presses the Enter key without typing a value. Although different programming languages handle the problem of input entry in different ways, there is often a way to determine whether an input operation failed to read data.

Another overlooked type of error is the entry of the wrong type of data. This happens, for example, when a program attempts to read an integer but the user enters a real number or string. Most programming languages provide library functions that you can use to avoid this type of error. You will often find functions similar to the iInteger and iReal discussed in Chapter 6. To use these functions in an input validation algorithm, you typically follow these steps:

+   1. Read the input as a string.
2. Determine whether the string can be converted to the desired data type.