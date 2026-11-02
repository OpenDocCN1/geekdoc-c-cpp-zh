
increments the pointer to the next element, and it returns the element to which it pointed before the increment.

Please do not use this programming style. Your job as a programmer is not to dazzle other programmers with your cleverness, but to write code that is easy to understand and maintain.

## Special Topic 7.3

![](img/d61019b035dd82beb581604273c0ee6b_388_0.png)

### Constant Pointers

The following definition specifies a constant pointer:

```
const double* p = &balance;
```

You cannot modify the value to which p points. That is, the following statement is illegal:

```
*p = 0; // Error
```

Of course, you can read the value:

```
cout << *p; // OK
```

A constant array parameter variable is equivalent to a constant pointer. For example, consider the function

```
double sum(const double values[], int size)
```

Recall from Section 7.2.3 that values is a pointer. The function could have been defined as

```
double sum(const double* values, int size)
```

The function can use the pointer values to read the array elements, but it cannot modify them.

## 7.3 C and C++ Strings

C++ has two mechanisms for manipulating strings. The string class supports character sequences of arbitrary length and provides convenient operations such as concatenation and string comparison. However, C++ also inherits a more primitive level of string handling from the C language, in which strings are represented as arrays of char values. In this section, we will discuss the relationships between these types.

### 7.3.1 The char Type

![](img/d61019b035dd82beb581604273c0ee6b_388_1.png)

A value of type `char` denotes an individual character. Character literals are delimited by single quotes; for example,

```
char input = 'y';
```

**Table 3 Character Literals**

| Literal | Description |
|---|---|
| `'y'` | The character y |
| `'0'` | The character for the digit 0. In the ASCII code, `'0'` has the value 48. |
| `' '` | The space character |
| `'\n'` | The newline character |
| `'\t'` | The tab character |
| `'\0'` | The null terminator of a string |
| 🚫 `"y"` | Error: Not a char value |

Letters from foreign alphabets and special symbols may require multiple char values. See Chapter 8 for more information.

### 7.3.2 C Strings

A literal string (enclosed in double quotes) is an array of char values with a zero terminator.

In the C programming language, strings are always represented as character arrays. C++ programmers often refer to arrays of char values as "C strings". In particular, a literal string, such as "Harry", is not an object of type `string`. Instead, it is an array of char values. As with all arrays, a string literal can be assigned to a pointer variable that points to the initial character in the array:

```
const char* char_pointer = "Harry"; // Points to 'H'
```

The string is declared as const because you are not supposed to modify a literal string. (See Special Topic 7.3 for more information.)

A C string is terminated by a special character, called a null terminator, denoted `'\0'`. For example, the C string "Harry" contains six characters, namely 'H', 'a', 'r', 'r', 'y', and `'\0'`. (See Figure 6.) The terminator is a character that is encoded as the number zero—this is different from the character '0', the character denoting the zero digit. (Under the ASCII encoding scheme, the character denoting the zero digit is encoded as the number 48.) Functions that operate on C strings rely on this terminator. Here is a typical example, the `strlen` function declared in the `<cstring>` header that computes the length of a character array. The function counts the number of characters until it reaches the terminator.

![](img/d61019b035dd82beb581604273c0ee6b_389_0.png)

```
int strlen(const char s[])
{
    int i = 0;
    while (s[i] != '\0') { i++; } // Count characters before the null terminator
    return i;
}
```

The call `strlen("Harry")` returns 5.

### 7.3.3 Character Arrays

A literal string such as "Harry" is a constant. You are not allowed to modify its characters. If you want to modify the characters in a string, define a character array instead. For example:

```
char char_array[] = "Harry"; // An array of 6 characters
```

The char_array variable is an array of 6 characters, initialized with 'H', 'a', 'r', 'r', 'y', and a null terminator. The compiler counts the characters in the string that is used for initializing the array, including the null terminator. You can modify the characters in the array:

```
char_array[0] = 'L';
```

### 7.3.4 Converting Between C and C++ Strings

Many library functions use pointers of type `char*`.

The `c_str` member function yields a `char*` pointer from a string object.

You can initialize C++ string variables with C strings.

Before the C++ string class became widely available, direct manipulation of character arrays was common, but also quite challenging (see Special Topic 7.4). If you use functions that receive or return C strings, you need to know how to convert between C strings and string objects.

For example, the `<cstdlib>` header declares a useful function

```
int atoi(const char s[])
```

The `atoi` function converts a character array containing digits into its integer value:

```
char year[] = "2020";
int y = atoi(year); // Now y is the integer 2020
```

In older versions of C++, this functionality was missing from the string class. The `c_str` member function of the string class offers an "escape hatch". If `s` is a string, then `s.c_str()` yields a `char*` pointer to the characters in the string. Here is how you use that member function to call the `atoi` function:

```
string year = "2020";
int y = atoi(year.c_str());
```

Conversely, converting from a C string to a C++ string is very easy. Simply initialize a string variable with any value of type `char*`, such as a string literal or character array. For example, the definition

```
string name = "Harry";
```

initializes the C++ string object name with the C string "Harry".

### 7.3.5 C++ Strings and the [] Operator

Up to this point, we have always used the `substr` member function to access individual characters in a C++ string. For example, if a string variable is defined as

```
string name = "Harry";
```

the expression

```
name.substr(3, 1)
```

yields a string of length 1 containing the character at index 3.

You can access individual characters with the `[]` operator:

```
name[0] = 'L';
```

Now the string is "Larry". The `[]` operator is more convenient than the `substr` function if you want to visit a string one character at a time.

Here is a useful example. The following function makes a copy of a string and changes all characters to uppercase:

```
/**
 Makes an uppercase version of a string.
 @param str a string
 @return a string with the characters in str converted to uppercase
 */
string uppercase(string str)
{
 string result = str; // Make a copy of str
 for (int i = 0; i < result.length(); i++)
 {
 result[i] = toupper(result[i]); // Convert each character to uppercase
 }
 return result;
}
```

For example, `uppercase("Harry")` returns a string with the characters "HARRY".

The `toupper` function is defined in the `<cctype>` header. It converts lowercase characters to uppercase. (The `tolower` function does the opposite.)

**EXAMPLE CODE** See sec03 of your companion code for a program that demonstrates string processing.

You can access characters in a C++ string object with the `[]` operator.

![](img/d61019b035dd82beb581604273c0ee6b_391_0.png)

## Special Topic 7.4

### Working with C Strings

Before the string class became widely available, it was common to work with character arrays directly.

Table 4 shows several commonly used functions for manipulating C strings. All of these functions are declared in the `<cstring>` header.

Consider the task of concatenating a first name and a last name into a string. The string class makes this very easy:

```
string first = "Harry";
string last = "Smith";
string name = first + " " + last;
```
