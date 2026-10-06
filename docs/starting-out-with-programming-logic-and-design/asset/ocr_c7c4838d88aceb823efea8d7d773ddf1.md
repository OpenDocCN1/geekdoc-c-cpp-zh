# Chapter 12 Text Processing

Program 12-4 shows an example using one of these functions. The program reads a string as input from the keyboard, and then counts the number of uppercase characters in that string.

# Program 12-4

```
// Declare a string to hold input.
Declare String str

// Declare a variable to step through the string.
Declare Integer index

// Declare an accumulator variable to keep count
// of the number of uppercase letters.
Declare Integer upperCount = 0

// Prompt the user to enter a sentence.
Display "Enter a sentence."
Input str

// Count the number of uppercase letters.
For index = 0 To length(str) - 1
  If isUpper(str(index)) Then
    Set upperCount = upperCount + 1
  End If
End For

// Display the number of uppercase characters.
Display "That string has " << upperCount << " uppercase letters."
```

# Program Output (with Input in Bold)

Enter a sentence.
Ms. Jones will arrive TODAY! [Enter]
That string has 7 uppercase letters.

> The for loop in lines 16 through 20 steps through the String variable str. The If-Then statement that begins in line 17 calls the isUpper function, passing str[index] as an argument. If character is uppercase, the function returns True and the value of upperCount is incremented in line 18. After the loop finishes, upperCount will contain the number of uppercase characters in str.

# In the Spotlight:
Validating a Password

Many password-protected systems allow users to set up their own passwords. For increased security, systems usually require that passwords meet minimum specifications. When a user creates a password, the system must examine the password to determine whether it meets the minimum specifications. If it does not, the system rejects the password and requires the user to create another, more secure, password.

![](bbox=[0.755, 0.788, 0.835, 0.833])