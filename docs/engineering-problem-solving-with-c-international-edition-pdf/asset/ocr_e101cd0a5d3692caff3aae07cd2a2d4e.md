**TABLE 2.2 Example Data-Type Limits***

| Data Type | Details |
| :--- | :--- |
| \multicolumn{2}{c}{Integers} |
| short | Maximum = 32,767 |
| int | Maximum = 2,147,483,647 |
| long | Maximum = 2,147,483,647 |
| \multicolumn{2}{c}{Floating Point} |
| float | 6 digits of precision<br>Maximum exponent = 38<br>Maximum value = 3.402823e + 38 |
| double | 15 digits of precision<br>Maximum exponent = 308<br>Maximum value = 1.797693e + 308 |
| long double | 15 digits of precision<br>Maximum exponent = 308<br>Maximum value = 1.797693e + 308 |

*Microsoft Visual C++ 6.0 compiler.

sumed to be a double constant. To specify a `float` constant or a `long double` constant, the letter (or suffix) F or L must be appended to the constant. Thus, 2.3F and 2.3L represent a `float` constant and a `long double` constant, respectively.

# Boolean Data Type

The **boolean data type**, named after the mathematician George Boole, can represent only two values: **true** and **false**. In C++, the value zero is interpreted as false and any nonzero value is considered to be true. There are two predefined boolean constants, `true` and `false`, that can also be used. Boolean objects can be defined using the type specifier `bool`. The following example illustrates the use of boolean objects and constants:

```
bool error(false), status(true);
cout << error << endl << status;
```

The output from this program is

0
1

Boolean objects are very useful in controlling the flow of a program and flagging error conditions.

# Character Data Type

Character data is easy to work with in C++, but to work with **characters** effectively, we need to understand more about their representation in the computer's memory. Recall that all information stored in a computer is represented internally as sequences of binary digits (0 and 1). Each character corresponds to a **binary code** value. In the discussions that follow, we assume that American National Standards Institute (ANSI) code is used to represent characters.