# 12 Text Processing

# TOPICS

+   12.1 Introduction 12.2 Character-by-Character Text Processing

# 12.1 Introduction

Sometimes the data that a program must work with comes in the form of text. Word processors, text messaging programs, email applications, Web browsers, and spell-checkers are just a few examples of programs that work extensively with text.

The earlier chapters in this book have demonstrated some text processing techniques, such as case-sensitive and case-insensitive string comparisons, sorting strings in an array, and searching for substrings within a string. In addition, Chapter 6 introduced several standard library functions that perform operations on strings. For your convenience, these functions are summarized in Table 12-1.

The functions shown in Table 12-1 are very useful, but sometimes you need to operate on strings at a more detailed level. Some operations require that you access or manipulate the individual characters in a string. For example, you've probably used programs or Web sites that require you to set a password that meets certain requirements. Some systems require that passwords have a minimum length, contain at least one uppercase letter, at least one lowercase letter, and at least one digit. These requirements are intended to prevent ordinary words from being used as passwords, and thus make the password more secure. When every password is created, the system must examine each of the password's characters to determine whether it meets the requirements. In the next section you will see an example of an algorithm that performs this operation. First, however, we will discuss the process of accessing and manipulating the individual characters in a string.