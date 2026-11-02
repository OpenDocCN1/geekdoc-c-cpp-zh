+   i) The conversion specifier ______ is used to display a floating-point value in exponential notation.
+   j) The modifier ______ is placed before any floating-point conversion specifier to indicate that a long double value is to be displayed.
+   k) The conversion specifiers e, E and f are displayed with ______ digits of precision to the right of the decimal point if no precision is specified.
+   l) The conversion specifiers ______ and ______ are used to print strings and characters, respectively.
+   m) All strings end in the ______ character.
+   n) The field width and precision in a printf conversion specifier can be controlled with integer expressions by substituting a(n) ______ for the field width or for the precision and placing an integer expression in the corresponding argument of the argument list.
+   o) The ______ flag causes output to be left justified in a field.
+   p) The ______ flag causes values to be displayed with either a plus sign or a minus sign.
+   q) Precise input formatting is accomplished with the ______ function.
+   r) A(n) ______ is used to scan for a specific characters and store the characters in an array.
+   s) The conversion specifier ______ can be used to input optionally signed octal, decimal and hexadecimal integers.
+   t) The conversion specifiers ______ can be used to input a double value.
+   u) The ______ is used to read data from the input stream and discard it without assigning it to a variable.
+   v) A(n) ______ can be used in a scanf conversion specifier to indicate that a specific number of characters or digits should be read from the input stream.

# 9.2 Find the error in each of the following and explain how it can be corrected.

+   a) The following statement should print the character 'e'.
+   ```c
+   printf("%s\n", 'c');
+   ```
+   b) The following statement should print 9.375%.
+   ```c
+   printf("% .3f%", 9.375);
+   ```
+   c) The following statement should print the first character of the string "Monday".
+   ```c
+   printf("%c\n", "Monday");
+   ```
+   d) puts("A string in quotes");
+   e) printf("%6d%12, 20);
+   f) printf("\%c", '*');
+   g) printf("%s\n", 'Richard');

# 9.3 Write a statement for each of the following:

+   a) Print 1234 right justified in a 10-digit field.
+   b) Print 123.456789 in exponential notation with a sign (+ or -) and 3 digits of precision.
+   c) Read a double value into variable number.
+   d) Print 100 in octal form preceded by 0.
+   e) Read a string into character array string.
+   f) Read characters into array n until a nondigit character is encountered.
+   g) Use integer variables x and y to specify the field width and precision used to display the double value 87.4573.
+   h) Read a value of the form 3.5% Store the percentage in float variable percent and eliminate the % from the input stream. Do not use the assignment suppression character.
+   i) Print 3.333333 as a long double value with a sign (+ or -) in a field of 20 characters with a precision of 3.