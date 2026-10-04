
So, when a variable is a string, the += operation is the same as append, because you just append the new string onto the end of the existing one.

a compiler error, basically telling you that you're not allowed to add the 2 string literals together.

There are some unexpected effects of adding strings that you run into. In Program 9_8a, you have a string, and you try to assign s the sum of 2 string literals, Happy Birthday. But unexpectedly, you get

For general purposes, you're not allowed to add string literals. You can add string variables, and you can even add a string variable and a string literal. But you cannot add 2 string literals.

```
// Program 9_8_a
// ERROR - cannot add string literals
#include <iostream>
using namespace std;
int main() {
 s = "Happy" + "Birthday";
cout << s << endl;
}
```

## // CHAR-TYPE VARIABLES

A string is basically made up of an array, or a vector, of characters. A character is a letter, or digit, or punctuation, or space, etc. and each has its own built-in type.

In C, a string is basically an array. In C++, although there is still an array at its base, you can use a string which has many vector-like options.

You don't need to #include any libraries to have access to it. The type is char.

Program 9_9 is a very basic program using char-type variable. Notice that you don't need to #include any special libraries to use the char; you just iostream so that you can output to the console.

```
// Program 9_9
// char type
#include <iostream>
using namespace std;
int main() {
char testchar;
testchar = 'a';
cout << testchar << endl;
}
```

In C and C++, characters are enclosed in single quotes ('), and there can be just one character inside. Strings use double quotation marks ("").

Note: The single and double quotes should be the basic, standard quotation mark. If you use a word to write your code, it will often "help" by changing these to curly quotes—which are not the same thing and will cause errors in your program.

You declare a variable named testchar type char by writing testchar; you can assign a value to testchar—in this case, a. When testchar is streamed to output, a is printed to the screen.

## # ASCII Table

| DEC | CHAR | DEC | CHAR | DEC | CHAR | DEC | CHAR |
|---|---|---|---|---|---|---|---|
| 0 | NUL (null) | 32 | SPACE | 64 | @ | 96 | ` |
| 1 | SOH (start of heading) | 33 | ! | 65 | A | 97 | a |
| 2 | STX (start of text) | 34 | " | 66 | B | 98 | b |
| 3 | ETX (end of text) | 35 | # | 67 | C | 99 | c |
| 4 | EOT (end of transmission) | 36 | $ | 68 | D | 100 | d |
| 5 | ENQ (enquiry) | 37 | % | 69 | E | 101 | e |
| 6 | ACK (acknowledge) | 38 | & | 70 | F | 102 | f |
| 7 | BEL (bell) | 39 | ' | 71 | G | 103 | g |
| 8 | BS (backspace) | 40 | ( | 72 | H | 104 | h |
| 9 | TAB (horizontal tab) | 41 | ) | 73 | I | 105 | i |
| 10 | LF (line feed, new line) | 42 | * | 74 | J | 106 | j |
| 11 | VT (vertical tab) | 43 | + | 75 | K | 107 | k |
| 12 | FF (form feed, new page) | 44 | , | 76 | L | 108 | l |
| 13 | CR (carriage return) | 45 | - | 77 | M | 109 | m |
| 14 | SO (shift-out) | 46 | / | 78 | N | 110 | n |
| 15 | SI (shift-in) | 47 | 0 | 79 | O | 111 | o |
| 16 | DLE (data link escape) | 48 | 0 | 80 | P | 112 | p |
| 17 | DC1 (device control 1) | 49 | 1 | 81 | Q | 113 | q |
| 18 | DC2 (device control 2) | 50 | 2 | 82 | R | 114 | r |
| 19 | DC3 (device control 3) | 51 | 3 | 83 | S | 115 | s |
| 20 | DC4 (device control 4) | 52 | 4 | 84 | T | 116 | t |
| 21 | NAK (negative acknowledge) | 53 | 5 | 85 | U | 117 | u |
| 22 | SYN (synchronous idle) | 54 | 6 | 86 | V | 118 | v |
| 23 | ETB (end of trans. block) | 55 | 7 | 87 | W | 119 | w |
| 24 | CAN (cancel) | 56 | 8 | 88 | X | 120 | x |
| 25 | EM (end of medium) | 57 | 9 | 89 | Y | 121 | y |
| 26 | SUB (substitute) | 58 | : | 90 | Z | 122 | z |
| 27 | ESC (escape) | 59 | ; | 91 | [ | 123 | { |
| 28 | FS (file separator) | 60 | < | 92 | \ | 124 | \| |
| 29 | GS (group separator) | 61 | = | 93 | ] | 125 | } |
| 30 | RS (record separator) | 62 | > | 94 | ^ | 126 | ~ |
| 31 | US (unit separator) | 63 | ? | 95 | _ | 127 | DEL |

A char variable can take any of the standard characters you would type. These are the ASCII characters, and each character you can get on a keyboard—letters, numbers, punctuation, spaces, etc.—is a name.

The first 32 characters are control characters, followed by 92 printable characters, starting with punctuation marks and numbers, then first uppercase and lowercase. If you assign a number to a char variable, we are meaning that it will have the corresponding ASCII value.

> The backslash (\ is an escape character, and it means the next character will indicate special action to take.

| MOST NEEDED SPECIAL CHARACTERS |
|---||
| \n new line |
| \t tab |
| null quotation mark (\") apostrophe (\') |
| \\ backslash (\\) |
| question mark (?) audible backspace |
| \f new page (form feed) carriage return vertical tab hexadecimal value octal value |
| \... Unicode character (4 digit) |
| \... Unicode character (8 digit) |

C++, a string is basically a vector made up of chars, That's different from the ways strings were handled in C, which basically used an array of chars with an extra null character—the ASCII 0—at the end to mark the end of the string.

Even in C++, a string literal is still like a C-style string. Because you can't add arrays, that's why you can't add strings.

In both C and C++ strings, a particular character in a string can be accessed using square brackets. And because C++ strings operate like vectors, we have all the benefits that vectors have over arrays.

For example, recall that the at member function allows you to access a particular character and check that you don't go out of bounds in the array.

You also have the ability to get the size of a string, just like you get the size of a vector. It's easier to think in terms of length of a string rather than size, so a length command is also provided.

Strings can be compared to each other well. You can check whether two strings are equal. This means every character has to be checked to see if it matches. And the same goes for checking whether two strings are not equal.

Comparing strings is the basis for sorting in alphabetical order. Because upper-case letters come before lower-case in ASCII, "Zebra" will come before "apple" when comparing strings.

Comparing less than or greater is a little trickier. This really involves considering whether the ASCII characters come before or after. To compare whether one string comes before another string according to the ASCII table, the comparison will go through by character, to find the first character that doesn't match. If the ASCII value of the first nonmatching character is greater in one string, then that string is "greater".

Strings have other member functions that are useful:

- The empty returns a Boolean that is true if, and only, the string is empty—that is, does not contain any characters.
- The find takes another string as an argument. It returns the position where that first string occurs in the given string,
- The substring function takes two arguments; the first being the starting position and the second being the length. It returns a new string that is a piece of the old one. It will be the part that starts at the starting position and is of whatever length is specified.
- The replace function lets replace part of string with another string.

> A full list of member functions available for strings can be found at http://www.cplus.com/reference/string/string/

## # Exercise 1 Solution

Here's one way you might have written program.

```
// Program 9.4
// Reading and using multiple strings
#include <iostream>
#include <string>
using namespace std;

int main()
{
  string username, favoritecolor;
  cout << "What's your name? ";
  cin >> username;
  cout << "What's your favorite color? ";
  cin >> favoritecolor;
  cout << username << " , I like the color " << favoritecolor << " , too!" << endl;
}
```

Click here to go back to the exercise.

## # Exercise 2 Solution

- a) #include <string>
using namespace std;
string favoritefood;

# READINGS

- a) Stroustrup, Programming Principles and Practice Using C++, sections 23.1-23.2.
- b) Lippman, Lajoie, and Moo, C++ Primer, section 3.2.
- b) favoritefood = "pizza"
c) cin >> favoritefood;
d) getline(cin, favoritefood);
e) cout << favoritefood;

Click here to go back to the exercise.
