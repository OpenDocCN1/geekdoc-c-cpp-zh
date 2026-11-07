2　(Fill-in) A span encapsulates both a pointer and a ______ representing the number of elements.

Answer: size_t

3　(True/False) Because a span is a view into an existing container, changing the span’s elements changes the container’s original data.

Answer: True.

# 7.11  A Brief Intro to Pointer-Based Strings

We’ve already used the C++ standard library string class to represent strings as full-fledged objects. Chapter 8 presents class std::string in detail. This section introduces pointer-based strings, as inherited from the C programming language. Here, we’ll refer to these as C-strings or strings and use std::string when referring to the C++ standard library’s string class.

std::string is preferred because it eliminates many security problems and bugs caused by manipulating C-strings. However, there are some cases where C-strings are required, such as when processing command-line arguments. Also, if you work with legacy C and C++ programs, you’ll likely encounter pointer-based strings.

# Characters and Character Constants

Characters are the fundamental building blocks of C++ source programs. Every program is composed of characters that—when grouped meaningfully—are interpreted by the compiler as instructions and data used to accomplish a task. A program may contain character constants, each of which is an integer value represented as a character in single quotes. The value of a character constant is the integer value of the character in the machine’s character set. For example, 'z' represents the letter z’s integer value (122 in the ASCII character set; see the Character Set appendix at https://deitel.com/cpphtp11) as type char. Similarly, '\n' represents the integer value of newline (10 in the ASCII character set).

# Pointer-Based Strings

A C-string is a built-in array of characters ending with a null character ('\0'), which marks where the string terminates in memory. A C-string is accessed via a pointer to its first character (no matter how long the string is).

# String Literals as Initializers

A string literal may be used as an initializer for a built-in array of chars or a variable of type const char*. The following declarations each initialize a variable to the string "blue":

```
char color[] {"blue"};
const char* colorPtr{"blue"};
```

The first declaration creates a five-element built-in array color containing the characters 'b', 'l', 'u', 'e' and '\0'. The second creates the pointer variable colorPtr pointing to the letter b in the string "blue" (which ends in '\0') somewhere in memory. The first declaration above also may be implemented using an initializer list of individual characters in which you manually include the terminating '\0', as in:

```
char color[] {'b', 'l', 'u', 'e', '\0'};
```