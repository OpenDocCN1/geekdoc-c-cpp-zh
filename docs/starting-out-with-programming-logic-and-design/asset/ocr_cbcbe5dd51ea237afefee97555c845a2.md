# 12.2 Character-by-Character Processing

The programs you have seen so far in this chapter demonstrate how you can access
and modify individual characters at specific locations in a string. In most
programming languages, when you use a subscript or other mechanism to access an
individual position within a string, that character position must exist
oror an error will occur. For example, if a string contains four characters, we
cannot use subscript notation to add a fifth character. The following
pseudocode illustrates this:

```
Declare String word = "mist" // This string has 4 characters.
Set word[4] = "y"           // Error!
```

In the first statement the variable is initialized with the string "mist", which has
four characters. The subscript of the last character is 3. The second statement attempts
to assign the character "y" to word[4], but an error will occur because that
position does not exist. If you wish to append characters to a string, you must typically
 an operator or a library function designed for that purpose.

> WARNING! An error will also occur if you use a subscript on an uninitialized
variable. Because an uninitialized variable contains no data, you cannot
access or manipulate its contents.

# Character Testing Library Functions

In addition to string library functions, such as the ones shown in Table 12-1, most
programming languages also provide library functions that are designed to work with
single characters. Table 12-2 shows examples of commonly supported functions that
test the value of a character. Note that each of the functions listed in the table returns
a Boolean value of True or False.

Table 12-2 Common Character Testing Functions

| Function | Description |
|---|---|
| isDigit(character) | Returns True if character is a numeric digit, or False otherwise. |
| isLetter(character) | Returns True if character is an alphabetic letter or False otherwise. |
| isLower(character) | Returns True if character is a lowercase letter or False otherwise. |
| isUpper(character) | Returns True if character is an uppercase letter or False otherwise. |
| isWhiteSpace(character) | Returns True if character is a whitespace character or False otherwise. (A whitespace character is a space, a tab, or a newline.) |