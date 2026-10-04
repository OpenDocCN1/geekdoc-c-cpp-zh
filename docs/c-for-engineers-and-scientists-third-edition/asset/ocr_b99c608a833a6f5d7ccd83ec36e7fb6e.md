# Point of Information

# Formatting Text File Output Data

Output streams can be formatted in the same manner as the cout output stream. For example, if an output stream named fileOut has been declared, the following-statement formats all data inserted into the fileOut stream in the same way these parameterized manipulators work for the cout stream:

```
fileOut << setiosflags(ios::fixed)
<< setiosflags(ios::showpoint)
<< setprecision(2);
```

The first manipulator parameter, ios::fixed, causes the stream to output all numbers as they were floating-point values. The next parameter, ios::showpoint, tells the stream to provide a decimal point. A value such as 1.0 appears as 1.0, not 1. Finally, the setprecision( ) manipulator tells the stream to display two decimal values after the decimal point. Therefore, the number 1.0, appears as 1.00.

Instead of manipulators, you can use the stream methods setf() and precision(). For example, the previous formatting can be accomplished with the following code:

```
fileOut.setf(ios::fixed);
fileOut.setf(ios::showpoint);
fileOut.precision(2);
```

Which style you select is a matter of preference. In both cases, the formats need to be specified only once and remain in effect for every number subsequently inserted in the file stream.

# Reading from a Text File

Reading data from a character-file is almost identical to reading data from a standard keyboard, except the cin is replaced by the ifstream object declared in the program. For example, if inputFile is declared as an object of type ifstream that's opened for input, the following statement reads the next two items in the file and stores them in the variables desc and price:

```
inputFile >> desc >> price;
```

The file stream name in this statement, in place of cin, directs the input to come from the file stream rather than the standard input device stream. Table 8.3 lists other methods that can be used for stream input. These methods must be preceded by a stream object name. All these methods, except getline(), are defined in the iostream class. The getline() method is defined in the string class.