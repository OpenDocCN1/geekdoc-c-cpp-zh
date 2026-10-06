# 486 Chapter 12 Text Processing

```
// Variable to hold the number of digits
Declare Integer count = 0

// Variable to use stepping through str
Declare Integer index

// Step through str counting the number
// of digits.
// For index = 0 To length(str) - 1
If isDigit(str[index]) Then
    Set count = count + 1
End If
End For

// Return the number of digits.
Return count
End Function
```

This function is nearly identical to the numberUpperCase and numberLowerCase functions, except that line 89 calls the isDigit library function to determine whether the character at str[index] is a numeric digit. When the function ends, the statement in line 95 returns the value of the count variable, which contains the number of numeric digits found in the str variable.

# Program Output (with Input Shown in Bold)

```
This program determines whether a password meets the following requirements:
(1) It must be at least 8 characters long.
(2) It must contain at least one uppercase letter.
(3) It must contain at least one lowercase letter.
(4) It must contain at least one numeric digit.

Enter a password.
love [Enter]
The password does not meet the requirements.
```

# Program Output (with Input Shown in Bold)

```
This program determines whether a password meets the following requirements:
(1) It must be at least 8 characters long.
(2) It must contain at least one uppercase letter.
(3) It must contain at least one lowercase letter.
(4) It must contain at least one numeric digit.

Enter a password.
loVe679g [Enter]
The password is valid.
```