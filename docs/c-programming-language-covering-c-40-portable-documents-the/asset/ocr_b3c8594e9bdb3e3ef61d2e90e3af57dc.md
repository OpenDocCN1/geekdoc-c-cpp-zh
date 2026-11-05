If no real-type-suffix is specified, the type of the real literal is double. Otherwise, the real type suffix determines the type of the real literal, as follows:

+   - A real literal suffixed by F or f is of type float. For example, the literals 1f, 1.5f, 1e10f, and 123.456F are all of type float.
+   - A real literal suffixed by D or d is of type double. For example, the literals 1d, 1.5d, 1e10d, and 123.456D are all of type double.
+   - A real literal suffixed by M or m is of type decimal. For example, the literals 1m, 1.5m, 1e10m, and 123.456M are all of type decimal. This literal is converted to a decimal value by taking the exact value and, if necessary, rounding to the nearest representable value using banker's rounding (§4.1.7). Any scale apparent in the literal is preserved unless the value is rounded or the value is zero (in which latter case, the sign and scale will be 0). Hence the literal 2.900m will be parsed to form the decimal with sign 0, coefficient 2900, and scale 3.

If the specified literal cannot be represented in the indicated type, a compile-time error occurs.

The value of a real literal of type float or double is determined by using the IEEE “round to nearest” mode.

Note that in a real literal, decimal digits are always required after the decimal point. For example, 1.3F is a real literal but 1.F is not.

> > **JOSEPH ALBAHARI** Of all the numeric suffixes, m and f are by far the most useful. Without these suffixes, a fractional float or decimal literal cannot be specified without a cast. For example, the following code will not compile, because the literal 1.5 will be parsed as type double:
> > ```csharp
> > float x = 1.5; // Error: no implicit conversion from double to float
> > decimal y = 1.5; // Error: no implicit conversion from double to decimal
> > ```
> > Interestingly, the following code does compile, because C# defines an implicit conversion from int to decimal:
> > ```csharp
> > decimal z = 123; // Okay: parsed as int, and then implicitly converted
> > // to decimal
> > ```
> > The d suffix is technically redundant in that the presence of a decimal point does the same job:
> > ```csharp
> > Console.WriteLine ((123.0).GetType() == typeof (double));// True
> > ```