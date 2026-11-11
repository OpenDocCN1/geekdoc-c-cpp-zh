# ## 4.4 KEYWORDS AND IDENTIFIERS

LO 4.1

Every C word is classified as either a *keyword* or an *identifier*. All keywords have fixed meanings and these meanings cannot be changed. The list of all keywords of ANSI C are listed in Table 4.3. All keywords must be written in lowercase. Some compilers may use additional keywords that must be identified from the C manual.

> > **Note** C99 adds some more keywords. See the Appendix “C99 Features”.

Table 4.3 ANSI C Keyword

| auto | double | int | struct |
|---|---|---|---|
| break | else | long | switch |
| case | enum | register | typedef |
| char | extern | return | union |
| const | float | short | unsigned |
| continue | for | signed | void |
| default | goto | sizeof | volatile |
| do | if | static | while |

**Identifiers** refer to the names of variables, functions and arrays. These are user-defined names. Both uppercase and lowercase letters are permitted. The underscore character is also permitted in identifiers.

# ### Rules for Identifiers

+   1. First character must be an alphabet (or underscore).
+   2. Must consist of only letters, digits or underscore.
+   3. Only first 31 characters are significant.
+   4. Cannot use a keyword.
+   5. Must not contain white space.

# ## 4.5 CONSTANTS

LO 4.2

Constants in C refer to fixed values that do not change during the execution of a program. C supports several types of constants as illustrated in Fig. 4.2.

# ### 4.5.1 Integer Constants

An *integer constant* refers to a sequence of digits. There are three types of integers, namely, *decimal integer*, *octal integer* and *hexadecimal integer*.

**Decimal integers** consist of a set of digits, 0 through 9, preceded by an optional – or + sign. Valid examples of decimal integer constants are:

```
`123  –321  0  654321  +78`
```