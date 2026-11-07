**Sample Runs:** In these sample runs, the user input is shaded.

# **Sample Run 1:**

Enter the first two Fibonacci numbers: `12 16`

The first two Fibonacci numbers are 12 and 16

Enter the position of the desired Fibonacci number: `10`

The Fibonacci number at position 10 is 796

# **Sample Run 2:**

Enter the first two Fibonacci numbers: `1 1`

The first two Fibonacci numbers are 1 and 1

Enter the position of the desired Fibonacci number: `15`

The Fibonacci number at position 15 is 610

The following is an example of a function that returns a Boolean value.

# EXAMPLE 6-6 (PALINDROME)

In this example, a function, `isPalindrome`, is designed that returns **true** if a string is a palindrome and **false** otherwise. A string is a palindrome if it reads forward and backward in the same way. For example, the strings "madamimadam", "5", "434", and "78956987" are all palindromes.

Suppose `str` is a string. To determine whether `str` is a palindrome, first compare the first and the last characters of `str`. If they are not the same, `str` is not a palindrome and so the function should return **false**. If the first and the last characters of `str` are the same, then we compare the second character with the second character from the end, and so on.

Note that if `length = str.length()`, the number of characters in `str`, then we need to compare `str[0]` with `str[length - 1]`, `str[1]` with `str[length - 2]`, and in general `str[i]` with `str[length - 1 - i]`, where `0 <= i <= length / 2`.

The following algorithm implements this discussion:

+   1. `int length = str.length();`
+   2. `for (int i = 0; i < length / 2; i++)`
+      `if (str[i] != str[length - 1 - i])`
+         `return false;`
+      `return true;`

The following function implements this algorithm:

```
bool isPalindrome(string str)
{
    int length = str.length();                 //Step 1
```