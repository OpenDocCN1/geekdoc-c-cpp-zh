In general, the assert() mechanism can be described as follows:

# THE assert( ) MECHANISM

# Form:

```
assert(boolean_expression);
```

where:

boolean_expression is any valid expression evaluating to true or false.

# PURPOSE:

Checks whether boolean_expression is true. If it is, execution proceeds normally. If it is false, execution is terminated and a diagnostic message is displayed.

# 5.2.6 Boolean Character Functions

The C library cctype provides a number of boolean-valued functions for performing useful checks on character values. Some of the more useful of these are shown in Table 5.1. Also included at the end of the table are two functions for changing the case of a character.

TABLE 5.1 Character Operations in cctype
| Operation | Description |
|---|---|
| isalnum(ch) | true if ch is a letter or a digit, false otherwise |
| isalpha(ch) | true if ch is a letter, false otherwise |
| iscntrl(ch) | true if ch is a control character, false otherwise |
| isdigit(ch) | true if ch is a decimal digit, false otherwise |
| isgraph(ch) | true if ch is a printing character except space, false otherwise |
| islower(ch) | true if ch is lower case, false otherwise |
| isprint(ch) | true if ch is a printing character, including space, false otherwise |
| ispunct(ch) | true if ch is a punctuation character (not a space, an alphabetic character, or a digit), false otherwise |
| isspace(ch) | true if ch is a white space character (space, '\f', '\n', '\r', '\t', or '\v'), false otherwise |
| isupper(ch) | true if ch is upper case, false otherwise |
| isxdigit(ch) | true if ch is a hexadecimal digit, false otherwise |
| toupper(ch) | returns the uppercase equivalent of ch (if ch is lower case) |
| tolower(ch) | returns the lowercase equivalent of ch (if ch is upper case) |

# 5.3 EXAMPLE: DIGITAL CIRCUITS—A BINARY HALF-ADDER

As noted earlier, George Boole laid the foundations of circuit design in the mid-1800s. Boole formalized several axioms of logic and developed an algebra for writing logical expressions.7 In the late 1930s as mathematicians, engineers, and physicists worked at

7 More information about boolean algebras can be found on the text's website (see the Preface).