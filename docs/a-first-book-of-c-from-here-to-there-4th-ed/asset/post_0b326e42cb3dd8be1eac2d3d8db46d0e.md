
"Hello there World!" to dest_string. As with the strcpy() function, it's the programmer's responsibility to ensure that the destination C-string is defined as large enough to hold the additional concatenated characters.

The strlen() function returns the number of characters in its C-string parameter but doesn't include the terminating NULL character in the count. For example, the value returned by the function call strlen("Hello World!") is 12.

Finally, two string expressions can be compared for equality by using the strcmp() function. This comparison is done character by character in the same manner described in Section 14.1 for string class objects. Program 15.5 uses these C-string functions in the context of a complete program.

## Program 15.5

```
#include <iostream>
#include <cstring>  // required for the string function library
using namespace std;
int main()
{
    const int MAXELS = 50;
    char string1[MAXELS] = "Hello";
    char string2[MAXELS] = "Hello there";
    int n;

    n = strcmp(string1, string2);

    if (n < 0)
        cout << string1 << " is less than " << string2 << endl;
    else if (n == 0)
        cout << string1 << " is equal to " << string2 << endl;
    else
        cout << string1 << " is greater than " << string2 << endl;

    cout << "\nThe length of string1 is " << strlen(string1)
         << " characters" << endl;
    cout << "The length of string2 is " << strlen(string2)
         << " characters" << endl;

    strcat(string1, " there World!");

    cout << "\nAfter concatenation, string1 contains "
         << "the string value\n" << string1
         << "\nThe length of this string is "
         << strlen(string1) << " characters" << endl;

cout << "\nType in a sequence of characters for string2: ";
 cin.getline(string2, MAXELS);

strcpy(string1, string2);

cout << "After copying string2 to string1, "
     << "the string value in string1 is:\n" << string2
     << "\nThe length of this string is "
     << strlen(string1) << " characters" << endl;

return 0;
}
```

Following is a sample output produced by Program 15.5:

```
Hello is less than Hello there

The length of string1 is 5 characters
The length of string2 is 11 characters

After concatenation, string1 contains the string value
Hello there World!
The length of this string is 18 characters

Type in a sequence of characters for string2: It's a wonderful day
After copying string2 to string1, the string value in string1 is:
It's a wonderful day
The length of this string is 20 characters
```

## Character-Handling Functions

In addition to C-string manipulation functions, all C++ compilers include the character-handling functions covered previously in Section 14.2 and repeated in Table 15.3 for convenience. The prototypes for these functions are in the header file ctype, which should be included in any program using these functions.

### Table 15.3 Character Library Functions (Require the Header Files string and ctype)

| Function Prototype | Description | Example |
|---|---|---|
| int isalpha(charExp) | Returns a true (non-zero integer) if charExp evaluates to a letter; otherwise, it returns a false (zero integer) | isalpha('a') |
| int isalnum(charExp) | Returns a true (non-zero integer) if charExp evaluates to a letter or a digit; otherwise, it returns a false (zero integer) | isalnum(key); |
| int isupper(charExp) | Returns a true (non-zero integer) if charExp evaluates to an uppercase letter; otherwise, it returns a false (zero integer) | isupper('A') |
| int islower(charExp) | Returns a true (non-zero integer) if charExp evaluates to a lowercase letter; otherwise, it returns a false (zero integer) | islower('a') |
| int isdigit(charExp) | Returns a true (non-zero integer) if charExp evaluates to a digit (0 through 9); otherwise, it returns a false (zero integer) | isdigit('5') |
| int isascii(charExp) | Returns a true (non-zero integer) if charExp evaluates to an ASCII character; otherwise, returns a false (zero integer) | isascii('a') |
| int isspace(charExp) | Returns a true (non-zero integer) if charExp evaluates to a space; otherwise, returns a false (zero integer) | isspace(' ') |
| int isprint(charExp) | Returns a true (non-zero integer) if charExp evaluates to a printable character; otherwise, returns a false (zero integer) | isprint('a') |

### Table 15.3 Character Library Functions (Require the Header Files string and cctype) (continued)

| Function Prototype | Description | Example |
|---|---|---|
| int isctrl(charExp) | Returns a true (non-zero integer) if charExp evaluates to a control character; otherwise, it returns a false (zero integer) | isctrl('a') |
| int ispunct(charExp) | Returns a true (non-zero integer) if charExp evaluates to a punctuation character; otherwise, returns a false (zero integer) | ispunct('!') |
| int isgraph(charExp) | Returns a true (non-zero integer) if charExp evaluates to a printable character other than white space; otherwise, returns a false (zero integer) | isgraph(' ') |
| int toupper(charExp) | Returns the uppercase equivalent if charExp evaluates to a lowercase character; otherwise, returns the character code without modification | toupper('a') |
| int tolower(charExp) | Returns the lowercase equivalent if charExp evaluates to an uppercase character; otherwise, returns the character code without modification | tolower('A') |

Because all the istype() functions listed in Table 15.3 return a non-zero integer (interpreted as a Boolean true value) when the character meets the condition and return a zero integer (interpreted as a Boolean false value) when the condition isn't met, these functions can be used in an if statement. For example, take a look at the following code segment:

```
char ch;
ch = cin.get();  // get a character from the keyboard

if(isdigit(ch))
    cout << "The character just entered is a digit" << endl;
else if(ispunct(ch))
    cout << "The character just entered is a punctuation mark" << endl;
```

Note that the character function is included as a condition in the if statement. This is possible because the function returns a Boolean true (non-zero) or false (zero) value.
Program 15.6 shows using the toupper() function in the ConvertToUpper() function, which converts all lowercase string characters to their uppercase form.

## Program 15.6

```
#include <iostream>
using namespace std;

void ConvertToUpper(char []);  // function prototype

int main()
{
    const int MAXCHARS = 100;
    char message[MAXCHARS];

    cout << "\nType in any sequence of characters: ";
    cin.getline(message,MAXCHARS);

    ConvertToUpper(message);

    cout << "The characters just entered in uppercase are: "
         << message << endl;

    return 0;
}

// this function converts all lowercase characters to uppercase
void ConvertToUpper(char message[])
{
    for(int i = 0; message[i] != '\0'; i++)
        message[i] = toupper(message[i]);

    return;
}
```

The output produced when Program 15.6 runs is as follows:

```
Type in any sequence of characters: this is a test OF 12345.
The characters just entered in uppercase are: THIS IS A TEST OF 12345.
```

Note that the toupper() library function converts only lowercase letters; all other characters are unaffected.

## Conversion Functions

The last group of standard string library functions, listed in Table 15.4, is used to convert C-strings to and from integer and double-precision data types. The prototypes for these functions are in the header file cstdlib, which must be included in any program using these functions. Program 15.7 shows using the atoi() and atof() functions.

### Table 15.4 String Conversion Functions (Require the Header File cstdlib)

| Function Prototype | Description | Example |
|---|---|---|
| int atoi(stringExp) | Converts stringExp (an ASCII string) to an integer. Conversion stops at the first non-integer character. | atoi("1234") |
| double atof(stringExp) | Converts stringExp (an ASCII string) to a double-precision number. Conversion stops at the first character that can't be interpreted as a double. | atof("12.34") |
| char[] itoa(integerExp) | Converts integerExp (an integer) to a character array. The space allocated for the returned characters must be large enough for the converted value. | itoa(1234) |

Program 15.7 produces the following output:

```
The string "12345" as an integer number is: 12345
This number divided by 3 is: 4115
The string "12345.96" as a double number is: 12345.96
This number divided by 3 is: 4115.32
```
