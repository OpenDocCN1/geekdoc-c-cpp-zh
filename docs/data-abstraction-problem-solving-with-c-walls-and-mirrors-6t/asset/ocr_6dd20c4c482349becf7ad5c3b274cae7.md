# FIGURE 5-2 Trace of isId("A2B")

The initial call is made and the function begins execution.

At point X, a recursive call is made and the new invocation of isId begins execution:

At point X, a recursive call is made and the new invocation of isId begins execution:

This is the base case, so this invocation of isId completes:

The value is returned to the calling function, which completes execution:

The value is returned to the calling function, which completes execution:

# 5.1.2 Two Simple Languages

Now consider two more simple examples of languages, their grammars, and resulting recognition algorithms.

**Palindromes.** A palindrome is a string that reads the same from left to right as it does from right to left. For example, "radar" and "deed" are both palindromes. You can define the language of palindromes as follows:

> Palindromes = {string s : s reads the same left to right as right to left}

How can you use a grammar to define the language Palindromes? You need to devise a rule that allows you to determine whether a given string s is a palindrome. In the spirit of recursive definitions, you should state this rule in terms of determining whether a smaller string is a palindrome. Your first instinct might be to choose s minus its last (or first) character for the smaller string. However, this approach does not work, because there is no relationship between the statements

+   s is a palindrome

+   and

+   s minus its last character is a palindrome

That s, s minus its last character is a palindrome, although s minus its last character is not, as is the case for "deed." Similarly, s minus its last character might be a palindrome, although s is not, as is the case for "deeds."