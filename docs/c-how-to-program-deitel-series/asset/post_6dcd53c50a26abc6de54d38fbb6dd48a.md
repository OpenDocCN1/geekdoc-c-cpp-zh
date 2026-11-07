
- m) Use the `istream` member function `read` to input 50 characters into char array `line`.
- n) Read 10 characters into character array `name`. Stop reading characters if the `'.'` delimiter is encountered. Do not remove the delimiter from the input stream. Write another statement that performs this task and removes the delimiter from the input.
- o) Use the `istream` member function `gcount` to determine the number of characters input into character array `line` by the last call to `istream` member function `read`, and output that number of characters, using `ostream` member function `write`.
- p) Output `124, 18.376, 'z', 1000000` and `"String"`, separated by spaces.
- q) Display `cout`'s current precision setting.
- r) Input an integer value into `int` variable `months` and a floating-point value into `float` variable `percentageRate`.
- s) Print `1.92, 1.925` and `1.9258` separated by tabs and with 3 digits of precision, using a stream manipulator.
- t) Print integer 100 in octal, hexadecimal and decimal, using stream manipulators and separated by tabs.
- u) Print integer 100 in decimal, octal and hexadecimal separated by tabs, using a stream manipulator to change the base.
- v) Print 1234 right justified in a 10-digit field.
- w) Read characters into character array `line` until the character `'z'` is encountered, up to a limit of 20 characters (including a terminating null character). Do not extract the delimiter character from the stream.
- x) Use integer variables `x` and `y` to specify the field width and precision used to display the double value `87.4573`, and display the value.

## 13.4 (Find and Correct Code Errors)

Identify the error in each of the following statements and explain how to correct it.

- a) `cout << "value of x = y is: " << x <= y;`
- b) The following statement should print the integer value of `c`.
  ```cpp
  cout << 'c';
  ```
- c)
  ```cpp
  cout << "A string in quotes"";
  ```

## 13.5 (Show Outputs)

For each of the following, show the output.

- a)
  ```cpp
  cout << "12345" << endl;
  cout.width( 5 );
  cout.fill( '*' );
  cout << 123 << endl << 123;
  ```
- b)
  ```cpp
  cout << setw( 10 ) << setfill( '$' ) << 10000;
  ```
- c)
  ```cpp
  cout << setw( 8 ) << setprecision( 3 ) << 1024.987654;
  ```
- d)
  ```cpp
  cout << showbase << oct << 99 << endl << hex << 99;
  ```
- e)
  ```cpp
  cout << 100000 << endl << showpos << 100000;
  ```
- f)
  ```cpp
  cout << setw( 10 ) << setprecision( 2 ) << scientific << 444.93738;
  ```

## Answers to Self-Review Exercises

### 13.1
- a) streams.
- b) left, right and internal.
- c) flags.
- d) `<iostream>`.
- e) `<iomanip>`.
- f) `<fstream>`.
- g) write.
- h) `istream`.
- i) `cerr` or `clog`.
- j) `ostream`.
- k) `<<`.
- l) `cin`, `cout`, `cerr` and `clog`.
- m) `>>`.
- n) `oct`, `hex` and `dec`.
- o) `showpos`.

### 13.2
- a) False. The stream member function `flags` with a `fmtflags` argument sets the flags state variable to its argument and returns the prior state settings.
- b) False. The stream insertion and stream extraction operators are not overloaded for all user-defined types. You must specifically provide the overloaded operator functions to overload the stream operators for use with each user-defined type you create.
- c) False. The stream member function `flags` with no arguments returns the current format settings as a `fmtflags` data type, which represents the format state.
- d) True.
- e) False. To overload the stream insertion operator `<<`, the overloaded operator function must take an `ostream` reference and a reference to a user-defined type as arguments and return an `ostream` reference.
- f) True.
- g) True.
- h) True.
- i) False. The `cin` stream is connected to the standard input of the computer, which normally is the keyboard.
- k) True.
- l) True.
- m) True.
- n) False. The `ostream` member function `put` outputs its single-character argument.
- o) False. The stream manipulators `dec`, `oct` and `hex` set the output format state for integers to the specified base until the base is changed again or the program terminates.

### 13.3
```cpp
a) cout << "Enter your name: ";
b) cout << uppercase;
c) cout << static_cast< void * > ( myString );
d) cout << scientific;
e) cout << integerPtr;
f) cout << showbase;
g) cout << *floatPtr;
h) cout.fill( '0' );
   cout << setfill( ' ' );
i) cout.put( '0' ).put( 'K' );
j) cin.peek();
k) charValue = cin.get();
   cin.get( charValue );
l) cin.ignore( 6 );
m) cin.read( line, 50 );
n) cin.get( name, 10, ' ' );
   cin.getline( name, 10, ' ' );
o) cout.write( line, cin.gcount() );
p) cout << 124 << ' ' << 18.376 << ' ' << 'z' << ' ' << 1000000 << " String";
q) cout << cout.precision();
r) cin >> months >> percentageRate;
s) cout << setprecision( 3 ) << 1.92 << '\t' << 1.925 << '\t' << 1.9258;
t) cout << oct << 100 << '\t' << hex << 100 << '\t' << dec << 100;
u) cout << 100 << '\t' << setbase( 8 ) << 100 << '\t' << setbase( 16 ) << 100;
v) cout << setw( 10 ) << 1234;
w) cin.get( line, 20, 'z' );
x) cout << setw( x ) << setprecision( y ) << 87.4573;
```

### 13.4
- **a)** *Error:* The precedence of the `<<` operator is higher than that of `<=`, which causes the statement to be evaluated improperly and also causes a compiler error.
  *Correction:* Place parentheses around the expression `x <= y`.
- **b)** *Error:* In C++, characters are not treated as small integers, as they are in C.
  *Correction:* To print the numerical value of a character in the computer’s character set, the character must be cast to an integer value, as in the following:
  ```cpp
  cout << static_cast< int > ( 'c' );
  ```
- **c)** *Error:* Quote characters cannot be printed in a string unless an escape sequence is used.
  *Correction:* Print the string:
  ```cpp
  cout << "\"A string in quotes\"";
  ```

### 13.5
- **a)**
  ```text
  12345
  **123
  123
  ```
- **b)**
  ```text
  $$$$$10000
  ```
- **c)**
  ```text
  1024.988
  ```
- **d)**
  ```text
  0143
  0x63
  ```
- **e)**
  ```text
  100000
  +100000
  ```
- **f)**
  ```text
  4.45e+002
  ```

## Exercises

### 13.6 (Write C++ Statements)

Write a statement for each of the following:

- a) Print integer 40000 left justified in a 15-digit field.
- b) Read a string into character array variable `state`.
- c) Print 200 with and without a sign.
- d) Print the decimal value 100 in hexadecimal form preceded by 0x.
- e) Read characters into array `charArray` until the character `'p'` is encountered, up to a limit of 10 characters (including the terminating null character). Extract the delimiter from the input stream, and discard it.
- f) Print 1.234 in a 9-digit field with preceding zeros.

### 13.7 (Inputting Decimal, Octal and Hexadecimal Values)

Write a program to test the inputting of integer values in decimal, octal and hexadecimal formats. Output each integer read by the program in all three formats. Test the program with the following input data: 10, 010, 0x10.

### 13.8 (Printing Pointer Values as Integers)

Write a program that prints pointer values, using casts to all the integer data types. Which ones print strange values? Which ones cause errors?

### 13.9 (Printing with Field Widths)

Write a program to test the results of printing the integer value 12345 and the floating-point value 1.2345 in various-sized fields. What happens when the values are printed in fields containing fewer digits than the values?

### 13.10 (Rounding)

Write a program that prints the value 100.453627 rounded to the nearest digit, tenth, hundredth, thousandth and ten-thousandth.

### 13.11 (Length of a String)

Write a program that inputs a string from the keyboard and determines the length of the string. Print the string in a field width that is twice the length of the string.

### 13.12 (Converting Fahrenheit to Celsius)

Write a program that converts integer Fahrenheit temperatures from 0 to 212 degrees to floating-point Celsius temperatures with 3 digits of precision. Use the formula

```cpp
celsius = 5.0 / 9.0 * ( fahrenheit - 32 );
```

to perform the calculation. The output should be printed in two right-justified columns and the Celsius temperatures should be preceded by a sign for both positive and negative values.

### 13.13

In some programming languages, strings are entered surrounded by either single or double quotation marks. Write a program that reads the three strings `suzy`, `'suzy'` and `"suzy"`. Are the single and double quotes ignored or read as part of the string?

### 13.14 (Reading Phone Numbers with an Overloaded Stream Extraction Operator)

In Fig. 10.5, the stream extraction and stream insertion operators were overloaded for input and output of objects of the `PhoneNumber` class. Rewrite the stream extraction operator to perform the following error checking on input. The operator>> function will need to be reimplemented.

- a) Input the entire phone number into an array. Test that the proper number of characters has been entered. There should be a total of 14 characters read for a phone number of the form (800) 555-1212. Use the `ios_base` member function `clear` to set `failbit` for improper input.
