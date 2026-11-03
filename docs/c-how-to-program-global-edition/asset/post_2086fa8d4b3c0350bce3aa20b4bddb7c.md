
i) The conversion specifier ______ is used to display a floating-point value in exponential notation.
j) The modifier ______ is placed before any floating-point conversion specifier to indicate that a long double value is to be displayed.
k) The conversion specifiers e, E and f are displayed with ______ digits of precision to the right of the decimal point if no precision is specified.
l) The conversion specifiers ______ and ______ are used to print strings and characters, respectively.
m) All strings end in the ______ character.
n) The field width and precision in a printf conversion specifier can be controlled with integer expressions by substituting a(n) ______ for the field width or for the precision and placing an integer expression in the corresponding argument of the argument list.
o) The ______ flag causes output to be left justified in a field.
p) The ______ flag causes values to be displayed with either a plus sign or a minus sign.
q) Precise input formatting is accomplished with the ______ function.
r) A(n) ______ is used to scan a string for specific characters and store the characters in an array.
s) The conversion specifier ______ can be used to input optionally signed octal, decimal and hexadecimal integers.
t) The conversion specifiers ______ can be used to input a double value.
u) The ______ is used to read data from the input stream and discard it without assigning it to a variable.
v) A(n) ______ can be used in a scanf conversion specifier to indicate that a specific number of characters or digits should be read from the input stream.

## 9.2 Find the error in each of the following and explain how it can be corrected.

a) The following statement should print the character 'c'.
```c
printf("%s\n", 'c');
```
b) The following statement should print 9.375%.
```c
printf("%3.3f", 9.375);
```
c) The following statement should print the first character of the string "Monday".
```c
printf("%c\n", "Monday");
```
d) puts("A string in quotes")
```c
puts("A string in quotes");
```
e)
```c
printf("%d%d", 12, 20);
```
f)
```c
printf("%c", 'x');
```
g)
```c
printf("%s\n", "Richard");
```

## 9.3 Write a statement for each of the following:

a) Print 1234 right justified in a 10-digit field.
b) Print 123.456789 in exponential notation with a sign (+ or -) and 3 digits of precision.
c) Read a double value into variable number.
d) Print 100 in octal form preceded by 0.
e) Read a string into character array string.
f) Read characters into array n until a nondigit character is encountered.
g) Use integer variables x and y to specify the field width and precision used to display the double value 87.4573.
h) Read a value of the form 3.5%. Store the percentage in float variable percent and eliminate the % from the input stream. Do not use the assignment suppression character.
i) Print 3.333333 as a long double value with a sign (+ or -) in a field of 20 characters with a precision of 3.

## Answers to Self-Review Exercises

9.1

- a) streams.
- b) standard input.
- c) standard output.
- d) printf.
- e) conversion specifiers, flags, field widths, precisions, literal characters.
- f) d, i, g, o, u, x (or X).
- g) h, l, i (or E).
- j) L.
- k) 6.
- l) s, c
- m) NULL ("\0").
- n) asterisk (*).
- o) - (minus).
- p) + (plus).
- q) scanf.
- r) scan set.
- s) i.
- t) le, lE, lf, lG (or lg).
- u) assignment suppression character.
- v) field width.

9.2

- a) Error: Conversion specifier s expects an argument of type pointer to char.
  Correction: To print the character 'c', use the conversion specifier %c or change "%c" to "%s".
- b) Error: Trying to print the literal character % without using the conversion specifier %%.
  Correction: Use %% to print a literal % character.
- c) Error: Conversion specifier c expects an argument of type char.
  Correction: To print the first character of "Monday" use the conversion specifier %1s.
- d) Error: Trying to print the literal character " without using the \" escape sequence.
  Correction: Replace each quote in the inner set of quotes with \".
- e) Error: The format control string is not enclosed in double quotes.
  Correction: Enclose %f in double quotes.
- f) Error: The character x is enclosed in double quotes.
  Correction: Character constants to be printed with %c must be enclosed in single quotes.
- g) Error: The string to be printed is enclosed in single quotes.
  Correction: Use double quotes instead of single quotes to represent a string.

9.3

a) printf("%10d\n", 1234);
b) printf("%-30d\n", 123456789);
c) scanf("%lf", &number);
d) printf("%o\n", 100);
e) scanf("%s", string);
f) scanf("%[0123456789]", n);
g) printf("%.9f\n", x, y, 87.4573);
h) scanf("%f%%", &percent);
i) printf("%+20.3Lf\n", 3.333333);

## Exercises

9.4 Write a printf or scanf statement for each of the following:

- a) Print unsigned integer 40000 left justified in a 15-digit field with 8 digits.
- b) Read a hexadecimal value into variable hex.
- c) Print 200 with and without a sign.
- d) Print 100 in hexadecimal form preceded by 0x.
- e) Read characters into array s until the letter p is encountered.
- f) Print 1.234 in a 9-digit field with preceding zeros.
- g) Read a time of the form hh:mm:ss, storing the parts of the time in the integer variables hour, minute and second. Skip the colons (:) in the input stream. Use the assignment suppression character.
- h) Read a string of the form "characters" from the standard input. Store the string in character array s. Eliminate the quotation marks from the input stream.
- i) Read a time of the form hh:mm:ss, storing the parts of the time in the integer variables hour, minute and second. Skip the colons (:) in the input stream. Do not use the assignment suppression character.

9.5 Show what each of the following statements prints. If a statement is incorrect, indicate why.

## 9.11 (Escape Sequences) Write a program to test the escape sequences '\', '\"', '\?', '\a', '\b', '\n', '\r and \t. For the escape sequences that move the cursor, print a character before and after printing the escape sequence so it's clear where the cursor has moved.

## 9.12 (Printing a Question Mark) Write a program that determines whether ? can be printed as part of a printf format control string as a literal character rather than using the \? escape sequence.

## 9.13 (Reading an Integer with Each scanf Conversion Specifier) Write a program that inputs the value 437 using each of the scanf integer conversion specifiers. Print each input value using all the integer conversion specifiers.

## 9.14 (Outputting a Number with the Floating-Point Conversion Specifiers) Write a program that uses each of the conversion specifiers e, f and g to input the value 1.2345. Print the values of each variable to prove that each conversion specifier can be used to input this same value.

## 9.15 (Reading Strings in Quotes) In some programming languages, strings are entered surrounded by either single or double quotation marks. Write a program that reads the three strings suzy, "suzy" and 'suzy'. Are the single and double quotes ignored by C or read as part of the string?

## 9.16 (Printing a Question Mark as a Character Constant) Write a program that determines whether ? can be printed as the character constant '?' rather than using the character constant escape sequence \?' using conversion specifier %c in the format control string of a printf statement.

## 9.17 (Using %g with Various Precisions) Write a program that uses the conversion specifier g to output the value 9876.12345. Print the value with precisions ranging from 1 to 9.
