C# includes three different floating point types, each of which again corresponds to a specific System class in .NET.

# float

4 bytes. System.Single.

# double

8 bytes. System.Double.

# decimal

16 bytes. System.Decimal.

The floating point numeric literals are by default inferred to be of type double. One can use the suffixes f/F and m/M to explicitly make them types float and decimal, respectively. One can also optionally use d/D for the values of double.

The type of prod (line 12) is double. The type of div (line 15) is also double. Although the first operand 8.0F is float, the second operand 3.0 is double and hence the result of the operation is double.

Note in this example that the expression, 8.0 divided by 3.0, has no exact representation on the computer. The result is 2.66666666666666… The notation \{div:.##\} means that the output should be no more than two digits below the decimal point. The output in this case is 2.67, as shown above.

One thing to note is that the floating point number calculations on computers have finite precisions. This is generally true, not just in cases like this example. The real numbers are only approximately correct, and one has to be mindful when dealing with the floating numbers.

C#'s decimal type provides higher precision (e.g., by using 16 bytes, as compared to the 4 byte single precision). The decimal type numbers can be used for financial calculations, for example.

The type of money (line 18) is decimal. The decimal type includes some static