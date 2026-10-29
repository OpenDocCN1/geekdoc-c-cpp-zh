
This output is straightforward: `str1` is an empty string consisting of no characters, and the other strings display the characters they were initialized with. Because the first character in a string is designated as position 0, not 1, the character position of `D` in the string `Hot Dog`, for example, is position 4, as shown in Figure 14.2.

![](img/e9bf940282dfb289356f077151cc69dd_628_0.png)

**Figure 14.2**  The character positions of the string `Hot Dog`

## String Input and Output

In addition to a string being initialized with the constructors listed in Table 14.1, strings can be input from the keyboard and displayed onscreen. Table 14.2 lists the basic methods and objects for input and output of string values.

**Table 14.2**  *string* Class Input and Output

| C++ Object or Method | Description |
|---|---|
| `cout` | General-purpose screen output object |
| `cin` | General-purpose keyboard input object that stops reading string input when white space is encountered |
| `getline(cin, strObj)` | General-purpose keyboard input method that inputs all characters entered, stores them in the string `strObj`, and stops accepting characters when it receives a newline character (`\n`) |

In addition to the standard `cout` and `cin` streams you have been using throughout this book, the string class provides the `getline()` method for string input. For example, the expression `getline(cin, message)` continuously accepts and stores characters typed at the keyboard until the Enter key is pressed. Pressing the Enter key generates a newline character, `\n`, which `getline()` interprets as the end-of-line entry. All the characters encountered by `getline()`, except the newline character, are stored in the string `message`, as shown in Figure 14.3.

![](img/e9bf940282dfb289356f077151cc69dd_628_1.png)

**Figure 14.3**  Inputting a string with `getline()`

Program 14.2 shows using the `getline()` method and `cout` stream to input and output a string’s data entered at the user’s keyboard. Although `cout` is used in this program for string output, `cin` generally can’t be used in place of `getline()` for string input because `cin` reads a set of characters up to a blank space or a newline character. Therefore, attempting to enter

the characters This is a string by using the statement cin >> message; results in only the word This being assigned to message. Because a blank space terminates a cin extraction operation, cin’s usefulness for entering string data is restricted; therefore, getline() is used.

### Program 14.2

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string message;    // declare a string object

    cout << "Enter a string:\n";

    getline(cin, message);

    cout << "The string just entered is:\n"
         << message << endl;

    return 0;
}
```

The following is a sample run of Program 14.2:

```
Enter a string:
This is a test input of a string of characters.
The string just entered is:
This is a test input of a string of characters.
```

In its most general form, the getline() method has the following syntax:

```
getline(cin, strObj, terminatingChar)
```

In this syntax, strObj is a string object name and terminatingChar is an optional character constant, or variable, specifying the terminating character. For example, the expression getline(cin, message, '!') accepts all characters entered at the keyboard, including a newline character, until an exclamation point is entered. The exclamation point isn’t stored as part of the string.

If the optional third argument, terminatingChar, is omitted when getline() is called, the default terminating character is the newline ('\n') character. Therefore, the statement getline(cin, message, '\n'); can be used in place of the statement getline(cin, message);. Both these statements stop reading characters when the Enter key is

pressed. In all the programs used from this point on, input is terminated by pressing the Enter key, which generates a newline character. For this reason, the optional third argument passed to getline(), which is the terminating character, is omitted.

Caution: The Phantom Newline Character Seemingly strange results can happen when the cin input stream and getline() method are used together to accept data or when cin is used by itself to accept characters. To see how this result can occur, take a look at Program 14.3, which uses cin to accept an integer entered at the keyboard. The integer is then stored in the variable value, and a getline() method call follows.

### Program 14.3

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int value;
    string message;

    cout << "Enter a number: ";
    cin >> value;
    cout << "The number entered is:\n"
         << value << endl;

    cout << "Enter text:\n";
    getline(cin, message);
    cout << "The text entered is:\n"
         << message << endl;
    cout << int(message.length());

    return 0;
}
```

When Program 14.3 runs, the number entered in response to the prompt Enter a number: is stored in the variable value. At this point, everything seems to be working fine. Notice, however, that in entering a number, you type the number and press the Enter key. On almost all computer systems, this entered data is stored in a temporary holding area called a buffer immediately after the characters are entered, as shown in Figure 14.4.

## Point of Information

### The string and char Data Types

A string can consist of zero, one, or more characters. When the string has no characters, it's said to be an empty string with a length of 0. A string with a single character, such as "a", is a string of length 1 and is stored differently from a char data type, such as 'a'. However, for many practical purposes, a string of length 1 and a char respond in the same manner; for example, both cout << "\n" and cout << '\n' produce a new line onscreen. It's important to understand that they're different data types. For example, both these declarations

```
string s1 = 'a';  // INVALID INITIALIZATION
char key = "\n"; // INVALID INITIALIZATION
```

produce a compiler error because they attempt to initialize one data type with literal values of another type.

![](img/e9bf940282dfb289356f077151cc69dd_631_0.png)

# Figure 14.4 Typed characters are first stored in a buffer

The cin input stream in Program 14.3 accepts the number entered but leaves the '\n' in the buffer. The next input statement, which is a call to getline(), picks up the code for the Enter key as the next character and terminates any further input. Following is a sample run of Program 14.3:

```
Enter a number: 26
The number entered is 26
Enter text:
The text entered is
```

In this output, no text is accepted in response to the prompt Enter text:. No text is accepted because after the program accepts the number 26, the code for the Enter key, which is a newline escape sequence, remains in the buffer and is picked up and interpreted by getline() as the end of its input. This result occurs whether an integer (as in Program 14.3), a string, or any

other input is accepted by cin and then followed by a getline() method call. There are three solutions to this “phantom” Enter key problem:

- Don't mix cin with getline() inputs in the same program.
- Follow the cin input with the call to cin.ignore().
- Accept the Enter key in a character variable and then ignore it.

The first solution is preferred. All solutions, however, center on the fact that the Enter key is a legitimate character input and must be recognized as such. You encounter this problem again when you learn about accepting char data types in Section 14.2.

## String Processing

Strings can be manipulated by using string class functions or the character-at-a-time functions described in Section 14.2. Table 14.3 lists the most commonly used string class methods plus the standard arithmetic and comparison operators that can also be used with strings. In the examples, class methods are called by giving the object's name first, followed by a period, and then the method's name. With a few notable exceptions, all class methods are called in this way.

Table 14.3 The string Class Processing Methods (Require #include <string>)

| Method/Operation | Description | Example |
|---|---|---|
| int length() | Returns the length of the string | string.length() |
| int size() | Same as the preceding item | string.size() |
| at(index) | Returns the character at the specified index and throws an exception if the index is nonexistent | string.at(4) |
| int compare(str) | Compares the given string with str; returns a negative value if the given string is less than str, a 0 if they're equal, and a positive value if the given string is greater than str | string1.compare(string2) |
| c_str() | Returns the string as a NULL-terminated C-string | string1.c_str() |
| bool empty | Returns true if the string is empty; otherwise, returns false | string1.empty() |
| erase(ind,n); | Removes n characters from the string, starting at index ind | string1.erase(2,3) |
| erase(ind) | Removes all characters from the string, starting from index ind until the end of the string, and the length of the remaining string becomes ind | string1.erase(4) |
