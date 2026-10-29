
## Chapter I/O

Although you have used cin and getline() to accept data entered from the keyboard in a more or less “cookbook” manner, understanding what data is being sent to the program and how the program must react to process the data is useful. At a fundamental level, all input (as well as output) is done on a character-by-character basis, as shown in Figure 14.10.

![](img/e9bf940282dfb289356f077151cc69dd_646_0.png)

**Figure 14.10**  Accepting keyboard-entered characters

As this figure shows, the entry of every piece of data, whether it’s a string or a number, consists of typing characters. For example, entry of the string Hello consists of pressing and releasing the five character keys H, e, l, l, o, and the Enter key. Similarly, output of the number 26.95 consists of displaying the five characters 2, 6, ., 9, and 5. Although programmers usually don’t think of data in this manner, programs are restricted to this character-by-character I/O, and all of C++’s higher-level I/O methods and stream objects which are based on lower-level character I/O methods. These more basic character methods, which can be used by a programmer, are listed in Table 14.5.

### Table 14.5 Basic Character I/O Methods (Require the Header File iostream)

| Method | Description | Example |
|---|---|---|
| cout.put(charExp) | Places the character value of charExp on the output stream | cout.put('A'); |
| cin.get(charVar) | Extracts the next character from the input stream and assigns it to the variable charVar | cin.get(key); |
| cin.peek(charVar) | Assigns the next character from the input stream to the variable charVar without extracting the character from the stream | cin.peek(nextKey); |
| cin.putback(charExp) | Pushes a character value of charExp back onto the input stream | cin.putback(cKey); |
| cin.ignore(n, char) | Ignores a maximum of the next n input characters, up to and including the detection of char; if no arguments are specified, ignores the next single character on the input stream | cin.ignore(80, '\n');<br>cin.ignore(); |

The get() method reads the next character in the input stream and assigns it to the method's character variable. For example, examine this statement:

```
cin.get(nextChar);
```

It causes the next character entered at the keyboard to be stored in the character variable nextChar. This method is useful for inputting and checking characters before they're assigned to a complete string, character, or numeric variable.

The character output method corresponding to get() is put(). This method expects a single-character argument and displays onscreen the character passed to it. For example, the statement cout.put('A') causes the letter A to be displayed onscreen.

Of the last three methods listed in Table 14.5, cin.ignore() is the most useful. This method permits skipping over input until a designated character, such as '\n', is encountered. For example, the statement cin.ignore(80, '\n') skips up to a maximum of the next 80 characters or stops the skipping if the newline character is encountered. This statement can be useful for skipping all further input on a line, up to a maximum of 80 characters, or until the end of the current line is encountered. Input would begin with the next line.

The peek() method in Table 14.5 returns the next character on the stream but doesn't remove it from the stream's buffer. For example, the expression cin.peek(nextChar) returns the next character input at the keyboard but leaves it in the buffer. This action is sometimes useful for peeking ahead and seeing what the next character is but leaving it in place for the next input.

### Point of Information

### A Notational Inconsistency

All the character class methods in Table 14.5 use the standard object-oriented notation of preceding the method's name with an object name and a period, as in cin.get(). However, the string class getline() method uses the notation getline(cin, strVar). In this notation, the object (cin) appears as an argument inside the parentheses, which is how procedural-based functions pass variables. For consistency, you would expect getline() to be called as cin.getline(). Unfortunately, this notation was already in use for a getline() function created for C-style strings (which are simply one-dimensional arrays of characters, as discussed in Section 7.2) before the class methods in Table 14.5 were included in the C++ library. Keeping the original invocation syntax meant that a notational inconsistency was created.

Finally, the putback() method places a character back on the stream so that it's the next character read. The argument passed to putback() can be any character expression that evaluates to a legitimate character value; it doesn't have to be the last input character.

### The Phantom Newline Character Revisited

As you saw in Section 14.1, sometimes you get seemingly strange results when a cin input stream is followed by a getline() method call. This same result can occur when characters are inputted by using the get() character method. To see how it can occur, take a look at Program 14.10, which uses the get() method to accept the next character entered at the keyboard, and then stores the character in the variable fkey.

![](img/e9bf940282dfb289356f077151cc69dd_648_0.png)

# Program 14.10

```
#include <iostream>
using namespace std;

int main()
{
    char fkey;

    cout << "Type in a character: ";
    cin.get(fkey);
    cout << "The key just accepted is " << int(fkey) << endl;

    return 0;
}
```

When Program 14.10 is run, the character entered in response to the prompt Type in a character: is stored in the character variable fkey, and the decimal code for the character is displayed by explicitly casting the character into an integer to force its display as an integer value. The following sample run illustrates this technique:

Type in a character: m
The key just accepted is 109

At this point, everything seems to be working, although you might be wondering why the decimal value of m is displayed instead of the character. As you’ll see in Program 14.11, in typing m, two keys are usually pressed: the m key and the Enter key. As explained in Section 14.1, these two characters are stored in a buffer after they’re pressed (refer back to Figure 14.2). The first key pressed—m, in this case—is taken from the buffer and stored in fkey, but the code for the Enter key is still in the buffer. Therefore, a subsequent call to get() for a character input picks up the code for the Enter key as the next character automatically. To see an example, take a look at Program 14.11.

# Program 14.11

![](img/e9bf940282dfb289356f077151cc69dd_649_0.png)

```
#include <iostream>
using namespace std;

int main()
{
    char fkey, skey;

    cout << "Type in a character: ";
    cin.get(fkey);
    cout << "The key just accepted is " << int(fkey) << endl;

    cout << "Type in another character: ";
    cin.get(skey);
    cout << "The key just accepted is " << int(skey) << endl;

    return 0;
}
```

The following is a sample run of Program 14.11:

Type in a character: m
The key just accepted is 109
Type in another character: The key just accepted is 10

To review what happened in this program, after entering the letter m in response to the first prompt, the Enter key is also pressed. From a character standpoint, this input represents the entry of two distinct characters. The first character is m, which is coded and stored as the integer 109. The second character also gets stored in the buffer with the numerical code for the Enter key. The second call to get() picks up this code immediately, without waiting for another key to be pressed. The last cout stream displays the code for this key. The reason for displaying the numerical code rather than the character is that the Enter key has no printable character associated with it that can be displayed.

Remember that every key has a numerical code, including Enter, the spacebar, Escape, and Ctrl. These keys generally have no effect when entering numbers because the input methods ignore them as leading or trailing input with numerical data. These keys also don’t affect the entry of a single character requested as the first user data to be inputted, as in Program 14.10. Only when a character is requested after the user has already input other data, as in Program 14.11, does the usually invisible Enter key become noticeable.

In Section 14.5, you learn other ways to prevent the Enter key from being accepted as a legitimate character input when the getline() method is used. However, when the get() method is used in a program, you can use the following ways:

- Follow the cin.get() input with the call cin.ignore().
- Accept the Enter key in a character variable, and then don’t use it again.

Program 14.12 applies the first solution to Program 14.11. Ignoring the Enter key after the first character is read and displayed clears the buffer of the Enter key, which gets it ready to store the next valid input character as its first character.

# Program 14.12

```
#include <iostream>
using namespace std;

int main()
{
    char fkey, skey;

    cout << "Type in a character: ";
    cin.get(fkey);
    cout << "The key just accepted is " << int(fkey) << endl;
    cin.ignore();

    cout << "Type in another character: ";
    cin.get(skey);
    cout << "The key just accepted is " << int(skey) << endl;

    return 0;
}
```
