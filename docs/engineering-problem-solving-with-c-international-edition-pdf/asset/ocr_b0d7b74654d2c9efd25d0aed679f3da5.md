object. The following shows the variables, their identifiers, and their initial values after the following declaration statement from program Chapter_1:

```
double x1(1), y1(5), x2(4), y2(7),
side1, side2, distance;

double x1 1.0 double y1 5.0
double x2 4.0 double y2 7.0

double side1 ? double side2 ? double distance ?
```

The values of variables that were not given initial values are unspecified, and thus indicated with a question mark; sometimes these values are called garbage values because their values are unpredictable. A diagram such as this shows an object along with its identifier, its value, and its data type is called a memory snapshot. A memory snapshot shows the contents of a memory location at a specified point in memory of the execution of the program. The preceding memory snapshot shows the objects and their contents after execution of the declaration statement. The objects are declared to be of type double and will be represented in memory using the standard IEEE format. For simplicity we show only the value of the variable and its data type, but it is important to remember that the value of a floating point variable, even when initialized with an integer constant, will be represented in memory using the IEEE floating point representation of the integer value.

We frequently use memory snapshots to show the contents of objects both before and after a statement is executed in order to show its effect. The rules for selecting a valid identifier are as follows:

+   - an identifier must begin with an alphabetic character or the underscore character
+   - alphabetic characters in an identifier can be lowercase or uppercase letters
+   - an identifier can contain digits, but not as the first character
+   - an identifier can be of any length, but the first 31 characters of the identifier must be unique

C++ is case-sensitive, which means uppercase letters are distinguished from lowercase letters; thus Side1, SIDE1 and side1 represent three different objects. C++ also includes keywords with special meaning to the C++ compiler that cannot be used for identifiers; a complete list of keywords is given in Table 2.1.

Examples of valid identifiers are distance, x1, xSum, averageMeasurement, and initialTime. Examples of invalid identifiers are 1x (begins with a digit), switch (a keyword), $sum (contains an invalid character $), and rate% (contains an invalid character %).

An identifier name should be carefully selected so that it reflects the contents of the object. If possible, the name should also indicate the units of measurement. For example, if an object represents a temperature measurement in degrees Fahrenheit, use an identifier such as tempF or degreesF. If an object represents an angle, name it thetaRad to indicate that the angle is measured in radians or thetaDeg to indicate that the angle is measured in degrees.

Declarations statements included in any block of code must include not only the identifiers of the objects that we plan to use in our program, but they must also specify the data type of the object. C++ is a strongly typed programming language. This means that every