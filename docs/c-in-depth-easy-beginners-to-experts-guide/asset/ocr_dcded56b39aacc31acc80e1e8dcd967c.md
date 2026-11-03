Syntax:- putchar(character variable);

# The scanf Function (Entering input data) -

This function can be used to enter any combination of numerical values, single characters and strings. scanf( ) enters data from the standard input device and stores it in the computer’s memory. This function returns the number of data items that have been entered successfully. Syntax:- cnt=scanf( “control string”, arg1,arg2,arg3......argn);

Where the value of cnt will be number of successful input & Control string is a string for formatting, and arg1,arg2..... are arguments that represent the individual input data items. The arguments are written as variables or arrays, whose types match the corresponding character groups in the control string. Each variable name must be preceded by an ampersand (&).

# The printf Function (Writing Output data) -

This function can be used to output any combination of numerical values, single characters and strings.its purpose is to display data . printf( ) move data from the computer’s memory to the standard output device.

Syntax:- printf(“control string”,arg1,arg2.......argn);

Here control string refers to a string that contains formatting information, and arg1,arg2. are arguments that represent the individual output data items.

The control string can include a flag, which affects the appearance of the output. The flag must be placed immediately after percent sign(%). Some commonly used flags are:

+   - (-) :- Data item is left justified within the field (blank spaces required to fill them minimum field width will be added after the data item rather than before the data item)
+   - (+) :- A sign (either + or -) will precede each signed numerical data item. Without this flag, only negative data items are preceded by a sign.
+   - (0) :- causes leading zeros to appear instead of leading blanks. Applies only to data items tha are right justified within a field whose minimum size is larger than the data item.
+   - (' ') (blank space):- A blank space will precede each positive signed