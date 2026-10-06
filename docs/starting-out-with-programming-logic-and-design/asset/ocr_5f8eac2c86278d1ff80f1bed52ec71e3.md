# 12.2 Character-by-Character Processing 485

This variable will be used as an accumulator to hold the number of uppercase letters found in the parameter variable str. Line 40 declares Integer variable, index. The index variable is used in the loop that begins in line 44 to check characters in the str parameter variable. The If-Then statement begins in line 45 calls theUpper function to determine whether the character at str[index] is upper case. If so, the count variable is incremented in line 46. After the loop has finished, the count variable will contain the number of uppercase letters found in the str parameter variable. The count variable's value is returned from the function in line 51.

TheLowerCase function is shown next:

# Program 12-5 Password validation program (continued):
numberLowerCase function

```
// The LowerCase function accepts a string
// argument and returns the number of lowercase
// letters it contains.
Function Integer numberLowerCase(String str)
// Variable to hold the number of lowercase letters
Declare Integer count = 0

// Variable to using stepping str
Declare Integer index

// Step through str counting the number
// of lowercase letters.
For index = 0 To length(str)-1 Then
Set count = count + 1
End For

// Return the number of the lowercase letters.
Return count
End Function
```

This function is nearly identical to the numberUpper function, except that line 67 calls the isLower library function to determine whether the character at str[index] is lowercase. When the function ends, the statement in line 73 returns the value of the count variable, which contains the number of lowercase letters found in the str variable.

ThenumberDigits function is shown next:

# Program 12-5 Password validation program (continued):
numberDigits function

```
// The numberDigits function accepts a string
// argument and returns the number of numeric
// digits it contains.
Function Integer numberDigits(String str)
```