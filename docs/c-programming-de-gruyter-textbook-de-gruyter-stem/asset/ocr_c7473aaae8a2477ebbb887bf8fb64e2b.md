```
<< setw(6) << names[i]
<< resetiosflags(ios_base::left)
<< setw(10) << values[i] << endl;
```

Result:

| Zoot 1.23
Jimmy 35.36
Al 653.7
Stan 4358.24 |

This program used manipulator setiosflags with parameters to set left alignment. setiosflags is defined in <iosfmanip>. Parameter ios_base::left is an enumeration constant; it is defined in class ios_base, therefore needs to include ios_base::prefix when quotes. Manipator resetiosflags is used to close the alignment label here. width and setw, setiosflags remains effective until resetiosflags resumes the default value.

The parameter of setiosflags is the format design of the stream and its value is specified by the mask code (ios_base enumeration type) shown below. The value can be combined by using bitwise or the (|) operator.
ios_base::skipw skip the blanks in input
ios_base::left display left-alignment value, and use field character to fill the right
ios_base::right display right-alignment value, and use field character to fill the left (default alignment)
ios_base::internal insert specified filler inside the specified width, after the specified prefix symbol, before the value.
ios_base::dec format the value in decimal form (default form)
ios_base::oct format the value in octal form
ios_base::hex format the value in hexadecimal form
ios_base::showbase insert prefix symbol to represent the form (decimal, octal, or hexadecimal) of integrals.
ios_base::showpoint display the decimal point and axis 0s of float value
ios_base::uppercase display capital letters A-F for hexadecimal form, and display capital letter E for scientific form
ios_base::showpos display the positive sign (+) for nonnegative numbers
ios_base::scientific display float numbers in scientific form
ios_base::fixed display float numbers in fixed-point form (no index part)
ios_base::unitbuf dump and and delete the contents in buffer after each insertion

# Precision

The default value of a float number output precision is 6. For example, 3466.9768 is displayed as 3466.98. We can use the manipulator setprecision (defined in head