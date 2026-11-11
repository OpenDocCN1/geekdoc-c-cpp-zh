+   - Otherwise, if either of the operands is of type long, the other one will be converted to a long.
+   - Otherwise, both operands will be converted to an int.

# 3.5.4 Casts

In the preceding section, you saw that int values are automatically converted to double values when necessary. On the other hand, there are obviously times when you want to consider a double as an integer. Numeric conversions are possible in Java, but of course information may be lost. Conversions in which loss of information is possible are done by means of casts. The syntax for casting is to give the target type in parentheses, followed by the variable name. For example:

```
double x = 9.997;
int nx = (int) x;
```

Now, the variable nx has the value 9 because casting a floating-point value to an integer discards the fractional part.

If you want to round a floating-point number to the nearest integer (which in most cases is a more useful operation), use the Math.round method:

```
double x = 9.997;
int nx = (int) Math.round(x);
```

Now the variable nx has the value 10. You still need to use the cast (int) when you call round. The reason is that the return value of the round method is a long, and a long can only be assigned to an int with an explicit cast because there is the possibility of information loss.

> **CAUTION:** If you try to cast a number of one type to another that is out of range for the target type, the result will be a truncated number that has a different value. For example, (byte) 300 is actually 44.

> **C++ NOTE:** You cannot cast between boolean values and any numeric type. This convention prevents common errors. In the rare case when you want to convert a boolean value to a number, you can use a conditional expression such as `b ? 1 : 0`.