# **java.text.NumberFormat 1.1**

+   - `static Locale[] getAvailableLocales()`
+     returns an array of Locale objects for which NumberFormat formatters are available.
+   - `static NumberFormat getNumberInstance()`
+   - `static NumberFormat getNumberInstance(Locale l)`
+   - `static NumberFormat getCurrencyInstance()`
+   - `static NumberFormat getCurrencyInstance(Locale l)`
+   - `static NumberFormat getPercentInstance()`
+   - `static NumberFormat getPercentInstance(Locale l)`
+     returns a formatter for numbers, currency amounts, or percentage values for the current locale or for the given locale.
+   - `String format(double x)`
+   - `String format(long x)`
+     returns the string resulting from formatting the given floating-point number or integer.
+   - `Number parse(String s)`
+     parses the given string and returns the number value, as a Double if the input string describes a floating-point number and as a Long otherwise. The beginning of the string must contain a number; no leading whitespace is allowed. The number can be followed by other characters, which are ignored. Throws ParseException if parsing was not successful.
+   - `void setParseIntegerOnly(boolean b)`
+   - `boolean isParseIntegerOnly()`
+     sets or gets a flag to indicate whether this formatter should parse only integer values.
+   - `void setGroupingUsed(boolean b)`
+   - `boolean isGroupingUsed()`
+     sets or gets a flag to indicate whether this formatter emits and recognizes decimal separators (such as 100,000).
+   - `void setMinimumIntegerDigits(int n)`
+   - `int getMinimumIntegerDigits()`
+   - `void setMaximumIntegerDigits(int n)`
+   - `int getMaximumIntegerDigits()`
+   - `void setMinimumFractionDigits(int n)`
+   - `int getMinimumFractionDigits()`
+   - `void setMaximumFractionDigits(int n)`
+   - `int getMaximumFractionDigits()`
+     sets or gets the maximum or minimum number of digits allowed in the integer or fractional part of a number.