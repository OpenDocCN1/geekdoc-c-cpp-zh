
```
This is testing of getline and then we have read t
Now the read is being tested
It requires ctrl-Z to end
^Z
Now the read is being tested
It requires ctrl-Z to end
```

## How the Program Works

The program has demonstrated the use of the three different functions, namely, cin.getline(), cin.read(), and cin.write(). When the user types characters, getline() or read() accepts only the maximum number of characters specified in the argument. The number of characters printed is taken from the characters read. This is why there is a mismatch between the characters input and the characters displayed as output.

## 12.7 FORMATTING I/O

Formatting can be done using two different ways. The first method is to use built-in ios functions. Table 12.2 lists the various ios member functions.

**Table 12.2 Use of ios functions**

| ios member function | Use |
| --- | --- |
| width() | This specifies the width for display. The output will take up the width specified. It is used in aligning vertical columns of numeric items. |
| precision() | This specifies the precision of the floating-point number. The default precision is six digits after decimal point. |
| fill() | This specifies the character for filling up the unused portion of field. It is usually used with width member function. The remaining part of the field will be filled up with the char specified. Default char is space. |
| setf() | This specifies the format flags that control output display such as left or right justification, padding after sign symbol, scientific notation display, and displaying base of the number (such as hexadecimal, decimal, and octal). |
| unsetf() | This provides undo operation for the operations with setf(). |

### 12.7.1 Member Functions of ios

The prototype for all the following functions is:

```
<old value of stream> function_name(<specified new value>)
```

All ios functions return old values of the stream while they are called to set them to new values. The functions set the new value to the stream and return the old value. The width() function sets the new width to the argument specified and returns the old width. The precision() function sets new precision and returns the old precision. Similarly, fill() returns old fill char and sets new fill char.

### width()

It specifies the minimum field width for display. The output following this statement will use the width specified. It resets itself after the first output after this statement. The output of the statements

```
cout.width(10);
cout << "C++";
cout << "Language";
```

will be `SSSSSSSC++Language`. (S is used to indicate a space in the output.)

It can be seen that the output for `cout << "C++"` was provided in the width of 10, but the output for `cout << "Language"` is not. If one wants to provide the same width setting to the second cout statement as well, one more width specification should be added to it using one more cout.width in the following way:

```
cout.width(10);
cout << "C++";
cout.width(10);
cout << "Language";
```

Then, the output will be

```
SSSSSSSC++SSLanguage
```

Thus, cout.width() must precede any output for which width is to be set as it changes back to original value immediately after executing a single output.

**Notes**

- If the actual output exceeds the specified width, the complete output is provided and the value specified in width() is ignored.
- The formatting function width() operates on a single cout statement. The original width is restored after that.

### precision()

It specifies precision, that is, the number of digits to be displayed after the decimal point. As mentioned earlier, the default value is six. The precision function is important while displaying numbers in scientific notation, printing amount data where precision is two, or aligning floating point numbers for vertical alignment.

### fill()

The function fill(char) fills the subsequent empty portions of fields by the fill character specified. It is useful to print the '*'s preceding the amount information in cheques.

Consider Program 12.2 to understand the usefulness of the three ios member functions.

**PROGRAM 12.2 width(), precision(), and fill()**

```cpp
//Width.cpp
#include <iostream>
using namespace std;

int main()
{
cout << "Roll number"; cout << "Name"; cout << "Marks" << endl;
cout << 1 << "Lara" << 355.50 << endl;
cout << 2 << "Beckham" << 275 << endl;
cout << 3 << "Steffi" << 290.75 << endl;
cout << 4 << "Jaspal" << 295 << endl;
cout << 5 << "Ranatunga" << 200.60 << endl;

cout.width(15); cout << "Roll number"; cout.width(15);
cout << "Name"; cout.width(10); cout.precision(2);
cout << "Marks" << endl;

cout.fill(' '); cout.width(15); cout << 1; cout.width(15);
cout << "Lara"; cout.width(10); cout.fill('0');
cout.precision(2); cout << 355.50 << endl;

cout.fill(' '); cout.width(15); cout << 2; cout.width(15);
cout << "Beckham"; cout.width(10); cout.fill('0');
cout.precision(2); cout << 275 << endl;

cout.fill(' '); cout.width(15); cout << 3; cout.width(15);
cout << "Steffi"; cout.width(10); cout.fill('0');
cout.precision(2); cout << 290.75 << endl;

cout.fill(' '); cout.width(15); cout << 4; cout.width(15);
cout << "Jaspal"; cout.width(10); cout.fill('0');
cout.precision(2); cout << 295 << endl;

cout.fill(' '); cout.width(15); cout << 5; cout.width(15);
cout << "Ranatunga"; cout.width(10); cout.fill('0');
cout.precision(2); cout << 200.60 << endl;
}
```

**Output**

```
Roll number  Name    Marks
1            Lara    355.5
2            Beckham 275
3            Steffi  290.75
4            Jaspal  295
5            Ranatunga 200.6

Roll number  Name    Marks
1            Lara    003.6e+002
2            Beckham 0000000275
3            Steffi  002.9e+002
4            Jaspal  0000000295
5            Ranatunga 00002e+002
```

## How the Program Works

Take a look at the unformatted as well as the formatted outputs. The formatted output looks better than the unformatted output (except names being right justified and marks are not displayed in proper non-scientific notation; we will learn to set it right soon in Program 12.4). Now, look at the code. It seems there are more formatting statements than the actual output statements. These statements are a must in circumstances that involve displaying reports or printing them.

Such statements can be eliminated by using a simple function that does the formatting. The function then should be called using the required values. This is left as an exercise to the reader.

Now, let us see how roll numbers and names can be left aligned, while marks are aligned to their precision. The setf() function needs to be used to set these flags. Note the use of endl in the statements; it is used to provide the same effect as '\n', that is, providing a new line on the output. It is one of the manipulators that will be discussed later in this chapter in Section 12.11.

## 12.8 SETTING AND CLEARING FORMAT FLAGS

The format flags are attached with every stream that is used. The ios_base class defines a bitmap enumeration where 18 flags are defined. Table 12.3 lists the format flags and their roles.

**Table 12.3 Format flags and their roles**

| Flag name | Description |
| --- | --- |
| skipws | Skip initial white space while reading from a stream. |
| left | Output is left justified. |
| right | Output is right justified. |
| internal | Numeric value is padded with space between sign or base (0x, 0, etc.) character. |
| oct | Output is displayed in octal format. |
| hex | Output is displayed in hexadecimal format. |
| dec | Output is displayed in decimal format. |
| showbase | Numeric values will be displayed with base character such as displaying Hex 1E as 0x1E (Hex also needs to be specified before this, because decimal is the default). |
| uppercase | The x in showbase and the e in scientific notation are displayed in lower case. If uppercase is set, they would be displayed as X and E, that is, in upper case. |
| showpos | A leading + sign is displayed before positive values. This is not displayed by default. |
| showpoint | Decimal point will be displayed even if it is not present. Trailing zeros will also be displayed for all floating point values (this is needed for the example given earlier). |
| scientific | Output displays floating point values in scientific notation. |
| fixed | Output is displayed in fixed (non-scientific) notation. |
| unibuf | Buffers are flushed after every insertion. It is similar to flushing a stream after reading, so that no more extra chars are left out and subsequent read statements have no problem. |
| boolalpha | Enable the Boolean values of the input to be displayed as true or false rather than 1 and 0. |
| basefield | Collection of oct, dec, and hex. Needs to be specified as the second argument if any one of the three is the first argument to setf(). |
| adjustfield | Collection of left, right, and internal field. Needs to be specified as the second argument if any one of the three is the first argument to setf(). |
| floatfield | Collection of scientific and fixed. Needs to be specified as the second argument if any one of the two is specified as the first argument. |

All these fields can be set and unset using setf() and unsetf() functions available with the cout object. The following program demonstrates the effect of setting some of the flags on output. After every set and respective display, there is a call to unsetf() function to revoke the effect of applying that flag.
