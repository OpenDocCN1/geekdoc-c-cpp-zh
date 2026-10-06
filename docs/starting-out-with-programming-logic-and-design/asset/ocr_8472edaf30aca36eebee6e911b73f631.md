# 6.3 More Library Functions 257

# String Functions

Many types of programs work extensively with strings. For example, text editors like Notepad and word processors like Microsoft Word almost entirely with strings. Web browsers also work heavily with strings. When a Web browser loads a Page, it reads instructions that are written into the text of the Page.

Most programming languages provide several library functions for working with strings. This section discusses the most commonly supported functions.

# The length Function

The length function returns the length of a string. It accepts a string as its argument and returns the number of characters in the string (the string's length). The value returned is an integer. The following pseudocode shows how the length function might be used. In this program segment, the length of a password is checked to make sure it is at least six characters.

```
Display "Enter your new password."
Input password
If length(password) < 6 Then
    Display "The password must be at least six characters long."
End If
```

# The append Function

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

# The toUpper and toLower Functions

The toUpper and toLower convert the case of the alphabetic characters in a string. The toUpper function accepts a string as an argument and returns a string that is a copy of the original, but all characters converted to uppercase. Any character that is already uppercase or is not an alphabet letter is left unchanged. The following pseudocode shows an example of its usage:

```
Declare String str = "Hello World!"
Display toUpper(str)
```