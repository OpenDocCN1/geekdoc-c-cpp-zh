# 6.1 Introduction

# CHAPTER 06 REGULAR EXPRESSION

characters. A pattern describes one or more strings to match when searching for text. Regular expressions act as a template to match a character pattern to the string searched.

# Ordinary characters

Ordinary characters include all printable and unprintable characters that are not explicitly specified as metacharacters. This includes all uppercase and lowercase letters, all numbers, all punctuation, and some other symbols.

# Special characters

A special character is a character with special meaning in a regular expression, and is also the matching syntax of a regular expression. See the table below:

| Special characters | Description |
|---|---|n| $ | Matches the end position of the input string. |
| () | Matches the start and end of a subexpression. Subexpressions can be obtained for later use. |
| * | Matches the previous subexpression zero or more times. |
| + | Matches the previous subexpression one or more times. |
| . | Matches any single character except the newline character \n. |
| [ | Marks the beginning of a bracket expression. |
| ? | Matches the previous subexpression zero or one time, or indicates a non-greedy qualifier |
| \ | Marks the next character as either a special character, or a literal character, or a backward reference. For example, n Matches the character. The sequence \n Matches the \ character, while \( matches the \'. |
| ' | Matches newline characters. |
| { | Marks the beginning of a qualifier expression. |
| \ | Indicates a choice between the two. |

# Quantifiers

The qualifier is used to specify how many times a given component of a regular expression must appear to satisfy the match. See the table below:

| Character | Description |
|---|---|n| * | matches the previous subexpression zero or more times. For example, foo* matches fo and foooo. * is equivalent to {0,}. |