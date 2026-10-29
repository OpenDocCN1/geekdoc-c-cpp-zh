This output is straightforward: `str1` is an empty string consisting of no characters, and the other strings display the characters they were initialized with. Because the first character in a string is designated as position 0, not 1, the character position of `D` in the string `Hot Dog`, for example, is position 4, as shown in Figure 14.2.

![](bbox=[0.275, 0.213, 0.8, 0.269])

**Figure 14.2**  The character positions of the string `Hot Dog`

# String Input and Output

In addition to a string being initialized with the constructors listed in Table 14.1, strings can be input from the keyboard and displayed onscreen. Table 14.2 lists the basic methods and objects for input and output of string values.

**Table 14.2**  *string* Class Input and Output

| C++ Object or Method | Description |
|---|---|
| `cout` | General-purpose screen output object |
| `cin` | General-purpose keyboard input object that stops reading string input when white space is encountered |
| `getline(cin, strObj)` | General-purpose keyboard input method that inputs all characters entered, stores them in the string `strObj`, and stops accepting characters when it receives a newline character (`\n`) |

In addition to the standard `cout` and `cin` streams you have been using throughout this book, the string class provides the `getline()` method for string input. For example, the expression `getline(cin, message)` continuously accepts and stores characters typed at the keyboard until the Enter key is pressed. Pressing the Enter key generates a newline character, `\n`, which `getline()` interprets as the end-of-line entry. All the characters encountered by `getline()`, except the newline character, are stored in the string `message`, as shown in Figure 14.3.

![](bbox=[0.267, 0.762, 0.722, 0.804])

**Figure 14.3**  Inputting a string with `getline()`

Program 14.2 shows using the `getline()` method and `cout` stream to input and output a string’s data entered at the user’s keyboard. Although `cout` is used in this program for string output, `cin` generally can’t be used in place of `getline()` for string input because `cin` reads a set of characters up to a blank space or a newline character. Therefore, attempting to enter