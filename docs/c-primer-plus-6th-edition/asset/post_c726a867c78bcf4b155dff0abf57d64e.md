
# Chapter 17 Input, Output, and Files

```cpp
char * name = "Bingo";
cout << "What ho!" << name << "\n";
```

sends What ho! to output buffer and returns cout

![](img/cd111a87c1db9aff4db4b18834327463_1086_0.png)

```cpp
cout << name << "\n";
```

sends Bingo to output buffer and returns cout

![](img/cd111a87c1db9aff4db4b18834327463_1086_1.png)

```cpp
cout << "\n";
```

sends !\n to output buffer and returns cout (the return value is unused)

![](img/cd111a87c1db9aff4db4b18834327463_1086_2.png)

Figure 17.4 Output concatenation.

Originally, the put() method had the following prototype:
`ostream & put(char);`

The current standard is equivalent, except it's templated to allow for wchar_t. You invoke put() by using the usual class method notation:

```cpp
cout.put('W');      // display the W character
```

Here is the invoking object and put() is the class member function. Like the << operator functions, this returns a reference to the invoking object, so you can concatenate with:

```cpp
cout.put('I').put('t'); // displaying It with two put() calls
```

The function call cout.put('I') returns cout, which then acts as the invoking object for the put('t') call.

Given the proper prototype, you can use put() with arguments of numeric types other than char, as int, and let prototyping automatically convert the argument to the correct type char value. For example, you could use the following:

```cpp
cout.put(65);      // display the A character
cout.put(66.3);    // display the B character
```

The first statement converts the int value 65 to a char value and displays the character 65 as its ASCII code. Similarly, the second statement converts the double value 66.3 to a char value 66 and displays the corresponding character.

This behavior comes in with versions prior to Release 2.0 C++; in those versions, the language represents character constants with type int values. Thus, a statement such as the following would interpret 'W' as an int value and hence display it as the integer 87, the ASCII value for the character:

```cpp
cout << 'W';
```

But the following statement works:

```cpp
cout.put('W');
```

Because current C++ represents characters as type char, you can now use either method.

Some compilers erroneously overload put() for argument types: char, unsigned char, and signed char. This makes put() with an int argument ambiguous because an int cannot be converted to any of those three.

The write() method writes an entire string and has the following template prototype: `basic_ostream<charT, traits&>&write(const char_type* s, size n);`

The first argument to write() provides the address of the string to be displayed, and using cout to invoke write() invokes the char specialization, so the return type is ostream &. 

Listing 17.1 shows how the write() method works.

# Listing 17.1 write.cpp

```cpp
// write.cpp -- using cout.
#include <iostream>
#include <cstring> // or else string.h

int main() {
    using std::cout;
    using std::endl;
    const char * state1 = "Florida";
    const char * state2 = "Kansas";
    const char * state3 = "Euphoria";
    int len = strlen(state2);
    cout << "Increasing loop index:\n";
    for (int i = 1; i <= len; i++) {
        cout.write(state2,i);
        cout << endl;
    }
}
```

```cpp
// concatenate output
cout << "Decreasing loop index:\n";
for (i = len; i > 0; i--)
    cout.write(state2,i) << endl;
```

```cpp
// exceed string length
cout << "Exceeding string length:\n";
out.write(state2, len + 5) << endl;
```

```cpp
return 0;
```

Some compilers may observe that the program defines but doesn't use the arrays state1 and state3. That's okay because those arrays are there just to provide data before and after the state2 array so we can see what happens when the program miscodes access to state2. Here is the output of the program in Listing 17.1:

Increasing loop index:

+   K
Ka
Kan
Kans
Kansa
Kansas
Decreasing loop index:
Kans
Kansa
Kans
Kan
K

Exceeding string length:

Kansas Euph

Note that the cout.write() call returns the cout object. This is because the cout method returns a reference to the object that invokes it, and in this case, the cout object invokes it. This makes it possible to concatenate output because cout.write() is replaced by its return value:

```cpp
cout.write(state2,i) << endl;
```

Note, also the write() method does not stop printing characters automatically when it reaches the null character. This is because it relies on the number of characters to write.

# Formatting with cout

The ostream insertion operator converts values to text. By default, they format values as:

- A type char value, if it represents a printable character, is displayed as a character in a field one wide.
- Numeric integer types are displayed as decimal integers in a field wide enough to hold the number and, if present, a minus sign.
- Strings are displayed in a field equal to the length of the string.

The default behavior for floating-point types has changed. The following are the differences between ancient and current C++ implementations:

- New style—Floating-point types are displayed with a total of six digits, except that trailing zeros are not displayed.(Note that the number of digits has no connection to the precision to which the number is stored.) The number is displayed in fixed-point notation or in E notation (see Chapter 3, “Dealing with Data”), depending on the value of the number. In particular, E notation is used if the exponent is 6 greater or -5 smaller. Again, the field is wide enough to hold the number and, if present, a minus sign. The default behavior corresponds to using the C library function fprintf with a % specifier.
- Old style—Floating-point types are displayed with six places to the right of the decimal, except that trailing zeros aren't displayed.(Note that the number of digits displayed has no connection to the precision to which the number is stored.) The number is displayed in fixed-point notation or in E notation (see Chapter 3), depending on the value of the number.
