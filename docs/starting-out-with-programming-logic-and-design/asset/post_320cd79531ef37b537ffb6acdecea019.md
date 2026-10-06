
# Chapter 12 Text Processing

```
26 Display "The password is valid."
27 Else
28 Display "The password does not meet the requirements."
29 End If
30 End Module
```

Line 3 declares a variable named length for the minimum password length and line 6 declares a String named password to hold the user's password. Lines 9 through 15 display information on the screen informing the user of the password requirements. Lines 18 and 19 prompt the user to enter a password, which is read from the keyboard and assigned to the password variable.

The-If-Then-Else- statement that begins in line 22 evaluates a compound Boolean Expression. In plain English the statement should be interpreted like this:
If the password's length is at least 8 and
the number of uppercase letters in the password is at least 1 and
the number of lowercase letters in the password is at least 1 and
the number of numeric digits in the password is at least 1, Then the password is valid.
Else the password does not meet the requirements.
The numberUpperCase function is shown next:

## Program 12-5 Password validation program (continued): numberUpperCase function

```
32 // The numberUpperCase function accepts a string
33 // argument and returns the number of uppercase
34 // letters it contains.
35 Function Integer numberUpperCase(String str)
36 // Variable to hold the number of uppercase letters
37 Declare Integer count = 0
38
39 // Variable to use stepping through str
40 Declare Integer index
41
42 // Step through str counting the number
43 // of uppercase letters.
44 For index = 0 To length(str) - 1
45 If isUpper(str[index]) Then
46 Set count = count + 1
47
48 End If
49 End For
50
51 // Return the number of uppercase letters.
52 Return count
53 End Function
```

The function accepts a string as an argument, which is passed into the parameter variable str. Line 37 declares an Integer variable named count, initialized with the value 0.

## 12.2 Character-by-Character Processing

This variable will be used as an accumulator to hold the number of uppercase letters found in the parameter variable str. Line 40 declares Integer variable, index. The index variable is used in the loop that begins in line 44 to check characters in the str parameter variable. The If-Then statement begins in line 45 calls the isUpper function to determine whether the character at str[index] is upper case. If so, the count variable is incremented in line 46. After the loop has finished, the count variable will contain the number of uppercase letters found in the str parameter variable. The count variable's value is returned from the function in line 51.

TheLowerCase function is shown next:

## Program 12-5 Password validation program (continued): numberLowerCase function

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

The numberDigits function is shown next:

## Program 12-5 Password validation program (continued): numberDigits function

```
// The numberDigits function accepts a string
// argument and returns the number of numeric
// digits it contains.
Function Integer numberDigits(String str)
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

## Program Output (with Input Shown in Bold)

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

## Program Output (with Input Shown in Bold)

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

## 12.2 Character-by-Character Processing

### Inserting and Deleting Characters in a String

Most programming languages provide library functions or modules for inserting and deleting characters in a string. In our pseudocode we use the library modules described in Table 12-3 for these purposes.

| Function | Description |
| --- | --- |
| insert(string1, position, string2) | string1 is a String, position is an Integer, and string2 is a String. The function inserts string2 into string1, beginning at position. |
| delete(string, start, end) | string is a String, start is an Integer and end is an Integer. The function deletes all of the characters beginning at the position specified by start, and ending at the position specified by end. The character at the ending position is included in the deletion. |

Here is an example of how we might use the insert module:

```
Declare String str = "New City"
insert(str, 4, "York")
Display str
```

The second statement inserts "York" into the str variable, beginning at position 4. The characters that currently in position 4 are moved to the right. In memory, the str variable is expanded to accommodate the inserted characters. If these statements were a complete program and we ran it, we would see "New York City".

Here is an example of how we might use the delete module:

```
Declare String str = "I ate blueberries!"
delete(str, 8, 9)
Display str
```

The second statement deletes the characters at 8-9 in the str variable. The characters that previously appeared at 10 occupy the space left by the deleted characters. If these statements were a complete program and we ran it, we would see "I ate blueberries!".

### In the Spotlight: Formatting and Unformatting Telephone Numbers

Telephone numbers in the United States are commonly formatted to appear the following manner:

```
(XXX) XXX-XXXX
```

In the format, X represents a digit. The three digits that appear inside the parentheses are the area code. The three digits following the area code are the prefix, and the four digits after the hyphen are the line number. Here is an example:

```
(919)555-1212
```

Although the parentheses and the hyphen make the number easier for people, those characters are unnecessary for processing by a computer. In a computer system, a telephone number is commonly stored as an unformatted series of digits, as shown here:

```
919551212
```

A program that works with telephone numbers usually needs to unformat numbers that have been entered by the user. This means the parentheses and the hyphen must be removed prior to storing the number in a file or processing it in some other way. In addition, some programs need the ability to format a number so it contains the parentheses and the hyphen before displaying it on the screen or processing it on paper.

The pseudocode shown in Program 12-6 demonstrates an algorithm for unformatting telephone numbers. The main module prompts the user to enter a formatted telephone number. It then calls isValidFormat to determine whether the telephone number is properly formatted. If it is, it calls the unformat module to remove the parentheses and the hyphen. The unformatted telephone number is then displayed. Rather than presenting the entire program on paper, let's look at the main module:

| Program 12-6 | Phone number unformatting program: |
| main module |

```
Module main()
  // Declare a variable to hold a telephone number.
  Declare String phoneNumber

  // Prompt the user to enter a telephone number.
  Display "Enter a telephone number. The number you"
  Display "enter should be formatted as (XXX)XXX-XXXX."
  Input phoneNumber

  // If the input is properly formatted, unformat it.
  If isValidFormat(phoneNumber) Then
    unformat(phoneNumber)
    Display "The unformatted number is " , phoneNumber
  Else
```
