
- m) Use istream member function read to input 50 characters into char array line.
- n) Read 10 characters into character array name. Stop reading characters if the ',' delimiter is encountered. Do not remove the delimiter from the input stream. Write another statement that performs this task and removes the delimiter from the input.
- o) Use the istream member function gcount to determine the number of characters input into character array line by the last call to istream member function read, and output that number of characters, using ostream member function write.
- p) Output 124, 18.376, 'Z', 1000000 and "String", separated by spaces.
- q) Display cout's current precision setting.
- r) Input an integer value into int variable months and a floating-point value into float variable percentageRate.
- s) Print 1.92, 1.925 and 1.9258 separated by tabs and with 3 digits of precision, using a stream manipulator.
- t) Print integer 100 in octal, hexadecimal and decimal, using stream manipulators and separated by tabs.
- u) Print integer 100 in decimal, octal and hexadecimal separated by tabs, using a stream manipulator to change the base.
- v) Print 1234 right justified in a 10-digit field.
- w) Read characters into character array line1 until the character 'z' is encountered, up to a limit of 20 characters (including a terminating null character). Do not extract the delimiter character from the stream.
- x) Use integer variables x and y to specify the field width and precision used to display the double value 87.4573, and display the value.

## 21.4 (Find and Correct Code Errors) Identify the error in each of the following statements and explain how to correct it.

- a) cout << "Value of x <= y is: " << x <= y;
- b) The following statement should print the integer value of 'c'.
  cout << 'c';
- c) cout << """A string in quotes""";

## 21.5 (Show Outputs) For each of the following, show the output.

- a) cout << "12345" << endl;
  cout.width( 5 );
  cout.fill( ' * ' );
  cout << 123 << endl << 123;
- b) cout << setw( 10 ) << setfill( 'S' ) << 10000;
- c) cout << setw( 8 ) << setprecision( 3 ) << 1024.987654;
- d) cout << showbase << oct << 99 << endl << hex << 99;
- e) cout << 100000 << endl << showpos << 100000;
- f) cout << setw( 10 ) << setprecision( 7 ) << scientific << 444.93738;

## Answers to Self-Review Exercises

21.1 a) streams. b) left, right and internal. c) flags. d) iostream. e) <iomanip>. f) <fstream>. g) write. h) istream. i) cerr or clog. j) ostream. k) <<. l) cin, cout, cerr and clog. m) >>. n) oct, hex and dec. o) showpos.

21.2 a) False. The stream member function flags with a fmtflags argument sets the flags state variable to its argument and returns the prior state settings. b) False. The stream insertion and stream extraction operators are not overloaded for all user-defined types. You must specifically provide the overloaded operator functions to overload the stream operators for use with each user-defined type you create. c) False. The stream member function flags with no arguments returns the current format settings as a fmtflags data type, which represents the format state. d) True. e) False. To overload the stream insertion operator <<, the overloaded operator function must take an ostream reference as a reference to a user-defined type as arguments and return an ostream reference. f) True. g) True. h) True. i) True. j) False. The cin stream is connected to the standard input of the computer, which normally is the keyboard. k) True. l) True. m) True. n) False. The ostream member function put outputs its single-character argument. o) False. The stream manipulators dec, oct and hex set the output format state for integers to the specified base until the base is changed again or the program terminates.

## 21.3

- a) `cout << "Enter your name: ";`
- b) `cout << uppercase;`
- c) `cout << static_cast< void * >( myString );`
- d) `cout << scientific;`
- e) `cout << integerPtr;`
- f) `cout << showbase;`
- g) `cout << *floatPtr;`
- h) `cout.fill(' ');`
  `cout << setfill(' ');`
- i) `cout.put('0').put('K');`
- j) `cin.peek();`
- k) `charValue = cin.get();`
  `cin.get(charValue);`
- l) `cin.ignore(6);`
- m) `cin.read(line, 50);`
- n) `cin.get(name, 10, ',');`
  `cin.getline(name, 10, ',');`
- o) `cout.write(line, cin.gcount());`
- p) `cout << 124 << ' ' << 18.376 << ' ' << "Z " << 1000000 << " String";`
- q) `cout << cout.precision();`
- r) `cin >> months >> percentageRate;`
- s) `cout << setprecision(3) << 1.92 << '\t' << 1.925 << '\t' << 1.9258;`
- t) `cout << oct << 100 << '\t' << hex << 100 << '\t' << dec << 100;`
- u) `cout << 100 << '\t' << setbase(8) << 100 << '\t' << setbase(16) << 100;`
- v) `cout << setw(10) << 1234;`
- w) `cin.get(line, 20, 'z');`
- x) `cout << setw(y) << setprecision(y) << 87.4573;`

## 21.4

a) Error: The precedence of the << operator is higher than that of ==, which causes the statement to be evaluated improperly and also causes a compiler error.
Correction: Place parentheses around the expression x <= y.
b) Error: In C++, characters are not treated as small integers, as they are in C.
Correction: To print the numerical value for a character in the computer's character set, the character must be cast to an integer value, as in the following:
`cout << static_cast<int>( 'c' );`
c) Error: Quote characters cannot be printed in a string unless an escape sequence is used.
Correction: Print the string:
`cout << "\"A string in quotes\"";`

## 21.5

- a) 12345
  **123
  123
- b) $$$$$10000
- c) 1024.988

b) The area code and exchange do not begin with 0 or 1. Test the first digit of the area-code and exchange portions of the phone number to be sure that neither begins with 0 or 1. Use ios_base-member-function clear to set failbit for improper input.

c) The middle digit of an area code used to be limited to 0 or 1 (though this has changed). Test the middle digit for a value of 0 or 1. Use the ios_base-member-function clear to set failbit for improper input. If none of the above operations results in failbit being set for improper input, copy the parts of the telephone number into the PhoneNumber object's areaCode, exchange and line members. If failbit has been set on the input, the program print an error message and end, rather than print the phone number.

## 21.15 (Point Class) Write a program that accomplishes each of the following:

a) Create a user-defined class Point that contains the private integer data members xCoordinate and yCoordinate and declares stream insertion and stream extraction overloaded operator functions as friends of the class.

b) Define the stream insertion and stream extraction operator functions. The stream extraction operator function should determine whether the data entered is valid, and, if not, it should set the failbit to indicate improper input. The stream insertion operator should not be able to display the point after an input error occurred.

c) Write a main function that tests input and output of user-defined class Point, using the overloaded stream extraction and stream insertion operators.

## 21.16 (Complex Class) Write a program that accomplishes each of the following:

a) Create a user-defined class Complex that contains the private integer data members real and imaginary and declares stream insertion and stream extraction overloaded operator functions as friends of the class.

b) Define the stream insertion and stream extraction operator functions. The stream extraction operator function should determine whether the data entered is valid, and, if not, it should set failbit to indicate improper input. The input should be of the form

3 + 8i

c) The values can be negative or positive, and it's possible that one of the two values is not provided, in which case the appropriate data member should be set to 0. The stream insertion operator should not be able to display the point if an input error occurred. For negative imaginary values, a minus sign should be printed rather than a plus sign.

d) Write a main function that tests input and output of user-defined class Complex, using the overloaded stream extraction and stream insertion operators.

## 21.17 (Printing a Table of ASCII Values) Write a program that uses a for statement to print a table of ASCII values for the characters in the ASCII character set from 33 to 126. The program should print the decimal value, octal value, hexadecimal value and character value for each character. Use the stream manipulators dec, oct and hex to print the integer values.

## 21.18 (String-Terminating Null Character) Write a program to show that the getline and three-argument get istream member functions both end the input string with a string-terminating null character. Also, show that get leaves the delimiter character on the input stream, whereas getline extracts the delimiter character and discards it. What happens to the unread characters in the stream?
