# Defining Languages 163

A little thought reveals that you must consider characters in pairs: *There is a relationship between
the statements

and *s is a palindrome*

and s minus its first and last characters a palindrome
Specifically, *s* is a palindrome if and only if

+   * The first and last characters of *s* are the same
* s minus its first and last characters is a palindrome

You need a base case that you will reach after stripping away enough pairs of characters. If *s* has an even number of characters, you will eventually be left with two characters, and then, if you strip another pair, you will be left with zeros. A string of length 0 is the **empty string** and is a palindrome. If s has an odd number of characters, you will eventually be left with one character, after which you can strip another pair. Hence, you must have a base case: A string of length 1 is a palindrome.

This discussion leads to the following grammar for the language of palindromes:

```
<pal> = empty string | <ch> | a <pal> | b <pal> | .. | Z <pal> | Z
<ch> = a | b | .. | Z | A | .. |
```

Based on this, you can construct a recursive valued function for recognizing palindromes.
The pseudocode for such function cases:

```
// Returns true if the string s is of a palindrome; otherwise returns false.
isPalindrome(s: string): boolean
if (s is the empty string or s is length 1)
    return true
else if (s's first and last characters are the same)
    return isPalindrome(s minus its first and last characters)
else
    return false
```

**Strings of the form AⁿB*.** The notation 'AⁿB*' represents the string that consists of *n* consecutive A's followed by *n* consecutive B's. Another simple function for this language of strings consists:

AnBn = {string s : s is of the form AⁿB* for some n ≥0}

The grammar for this language is actually very similar to the grammar for palindromes. You strip away both the first and last characters to confirm that the first character is an A and the last is a B. Thus, the grammar for the language AnBn is

```
<legal_word> = empty string | A <legal_word> | B
```

The pseudocode for recognizing function follows:

```
// Returns true if s is of the form AⁿB*; otherwise returns false.
isAnBn(s: string): boolean
if (the length of s is 0)
    return true
else if (s begins with the character A and ends with the character B)
    return isAnBn(s minus its first and last characters)
else
    return false
```