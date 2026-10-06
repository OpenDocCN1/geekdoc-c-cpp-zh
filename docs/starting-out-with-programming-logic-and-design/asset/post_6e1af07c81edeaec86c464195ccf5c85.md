
## 6.3 More Library Functions

### String Functions

Many types of programs work extensively with strings. For example, text editors like Notepad and word processors like Microsoft Word almost entirely with strings. Web browsers also work heavily with strings. When a Web browser loads a Page, it reads instructions that are written into the text of the Page.

Most programming languages provide several library functions for working with strings. This section discusses the most commonly supported functions.

### The length Function

The length function returns the length of a string. It accepts a string as its argument and returns the number of characters in the string (the string's length). The value returned is an integer. The following pseudocode shows how the length function might be used. In this program segment, the length of a password is checked to make sure it is at least six characters.

```
Display "Enter your new password."
Input password
If length(password) < 6 Then
    Display "The password must be at least six characters long."
End If
```

### The append Function

The append function accepts two strings as arguments, which we will refer to as string1 and string2. It returns a third string that is created by appending string2 to the end of one. After the function executes, string1 and string2 remain unchanged. The following pseudocode shows an example of its usage:

```
Declare lastName = "Conway"
Declare salutation = "Mr. "
Declare properName
Set properName = append(salutation, lastName)
Display properName
```

If this pseudocode were an actual program, it would display:

Mr. Conway

> NOTE: The process of appending one string to the end of another string is called concatenation.

### The toUpper and toLower Functions

The toUpper and toLower convert the case of the alphabetic characters in a string. The toUpper function accepts a string as an argument and returns a string that is a copy of the original, but all characters converted to uppercase. Any character that is already uppercase or is not an alphabet letter is left unchanged. The following pseudocode shows an example of its usage:

```
Declare String str = "Hello World!"
Display toUpper(str)
```

If this pseudocode were an actual program, it would display:

HELLO WORLD!

The toLower function accepts a string as an argument and returns a string that is a copy of the argument, but with all characters converted to lowercase. Any character that is already lowercase or is not an alphabetic letter is left unchanged. The following pseudocode shows an example of its usage:

```
Declare String str = "WARNING!"
Display toLower(str)
```

If this pseudocode were an actual program, it would display:

warning!

TheUpper and toLower functions are useful for making case-insensitive comparisons. Normal, string comparisons are case-sensitive, which means that the upper-case characters are distinguished from the lowercase characters. In example, a case-sensitive comparison the string "hello" is not the same as the "HELLO" and "Hello" because the case of the characters is different. Sometimes it is more convenient to perform a case-insensitive comparison, in which the case of the characters is ignored. In a case-insensitive comparison, the string "hello" is considered the same as "HELLO" and "Hello"

For example, look at the following pseudocode:

```
Declare String again
Do
  Display "Hello!"
  Display "Do you want to see that again? (Y = Yes)"
  Input again
While toLower(again) == "Y"
```

The loop displays "Hello!" and prompts the user to enter "Y" to see it. The expression toLower(again) == "y" will be true if the user enters "y" or "Y.". Similar results can be achieved by using the toLower function, as shown here:

```
Declare String again
Do
  Display "Hello!"
  Display "Do you want to see that again? (Y = Yes)"
  Input again
While toLower(again) == "y"
```

### The substring Function

This function returns a substring within a string. The substring function typically accepts three arguments: (1) a string that you want to extract a string from, (2) the beginning position of the substring, and (3) the ending position of the substring.

Each character in a string is identified by its position number. The first character in a string is at position 0, the second character is at position 1, and so forth. In the sample pseudocode below, the substring function returns the substring in positions 5 through 7 of the string "New York City".

```
Declare String str = "New York City"
Declare String search
Set search = substring(str, 5, 7)
Display search
```

If this pseudocode were an actual program, it would display:

The substring function can also be used to extract individual characters from a string. For example, look at the following pseudocode:

```
Declare String name = "Kevin"
Display substring(name, 2, 2)
```

This code will display:

The function substring(name, 2, 2) will return the substring that begins and ends at position 2. In this case, that's the substring "ev". The pseudocode in 6-13 shows another example. This program prompts the user to enter a string, and then counts the number of times the letter "T" appears in the string.

Program 6-13
// Declare a variable to hold a string.
// Declare String str
// Declare a variable to hold the number
// Of Ts in a string.
Declare Integer numTs = 0
// Declare a counter variable.
Declare Integer counter
// Get a sentence from the user.
Display "Enter a string."
Input str
// Count the number of Ts in the string.
For counter = 0 To length(str)
If substring(str, counter, counter) == "T" Then
numTs = numTs + 1
End If
End For
// Display the number of Ts.
Display "That string contains ", numTs
Display "instances of the letter T."

Program Output (with Input Shown in Bold)
Enter a string.
Ten Times I Told You To STOP! [Enter]
That string contains 5
instances of the letter T.

### The contains Function

The contains function accepts two strings as arguments. It returns True if the first string contains the second string; otherwise, the function returns False. For example, the following pseudocode determines the string "four score and seven years ago" contains the string "seven":

```
Declare string1 = "four score and seven years ago"
Declare string2 = "seven"
If (string1,string2) Then
    Display string2, " appears in the string."
Else
    Display string2, " does not appear in the string."
End If
```

If this was actual code in a program, it would display "seven appears in the string."

### The stringToInteger and stringToReal Functions

Strings are sequences of characters, and are meant to hold text items such as names, addresses, descriptions, and so on. You can also store numbers as strings. In any program, time you put quotation marks around a number, it becomes a string. The following pseudocode declares a string variable interestRate and initializes it with the real "4.3":

```
Declare interestRate = "4.3"
```

Problems arise when you store numbers as strings, however. Most of the things that you do with numbers, such as arithmetic and numeric comparisons, cannot be done with strings. Those types of operations can be done only with numeric data such as Integers and Reals.

Some programs read data from a source that can provide input only as strings. This commonly happens with programming languages allow you to read keyboard input only as strings. In this situation, numbers are read as input initially into the program as strings and have to be converted to a numeric data type.

Most languages provide library functions to convert strings to numbers. The following pseudocode uses the stringToInteger and stringToReal for this purpose. The stringToInteger function accepts an argument, converts it to an integer, and returns the integer value. For example, a program has a string variable str, and an integer value has been stored as a string in this variable. The following statement converts the contents of the string variable to an integer and stores it in the intNumber.

```
Set intNumber = stringToInteger(str)
```

The stringToReal function works this way, but it converts a string to a Real. For example, suppose a real number has been stored as a string in the String variable str. The following statement converts the contents of the str variable to a Real and stores it in the realNumber variable.

```
Set realNumber = stringToReal(str)
```

When you use a function like these, there is always the possibility of an error. For example, look at the following pseudocode:
