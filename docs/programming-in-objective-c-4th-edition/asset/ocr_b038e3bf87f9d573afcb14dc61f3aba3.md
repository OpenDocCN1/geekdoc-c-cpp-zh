# Program 6.7. Output (Rerun)

Enter a single character:
B
It's an alphabetic character.

# Note

As shown in the program example, it's best to put a space before the %c in the scanf format string (as in " %c"). This will cause scanf to "skip" over any so-called whitespace characters (e.g., newlines, returns, line feeds) in the input. Omitting that space can cause scanf to read a character that you do not expect. While that might not be a problem in this example, it's good to keep this in mind when working on other examples in this chapter (including the exercises) whenever you want to read a single character.

The first test that is made after the character is read in determines whether the char variable c is an alphabetic character. This is done by testing whether the character is a lowercase letter or an uppercase letter. The former test is made by the following expression:

```
( c >= 'a' && c <= 'z' )
```

This expression is true if c is within the range of characters 'a' through 'z'; if, c is a lowercase letter. The latter test is made by this expression:

```
( c >= 'A' && c <= 'Z' )
```