# Overriding ToString

Before you start adding ToString overrides to all your classes, be aware that the Visual Studio debugging tools use ToString extensively to determine what values to display for an object when viewed through a debugger.

![](bbox=[0.8, 0.1, 0.98, 0.19])

The value of an object often has multiple representations, and ToString enables you to pass a format string as a parameter that determines how the string representation should appear. A format string contains one or more format specifiers that define how the string representation should appear.

# Standard Format Strings

A standard format string contains a single format specifier, which is a single character that defines a more complete format string, and an optional precision specifier that affects the number of digits displayed in the result. If supported, the precision specifier can be any integer value from 0 to 99. All the numeric types, date and time types, and enumeration types support a set of predefined standard format strings, including a “G” standard format specifier, which represents a general string representation of the value.

The standard format specifiers are shown in Table 8.4.

TABLE 8.4  Standard Format Specifiers

| Format Specifier | Description |
| :--- | :--- |
| “G”, “g” | Represents a general string representation. |
|  | For all numeric types, results in the most compact of either fixed-point or exponential notation. The precision specifier indicates the number of significant digits. |
|  | For all date and time types, represents the general date/time pattern. “G” represents the long time pattern, whereas “g” is the short time pattern. |
|  | For enumeration types, displays the enumeration entry as a string value, if possible, and otherwise displays the integer value of the current instance. If the enumeration is defined with the Flags attribute set, the string values of each valid entry are concatenated together, separated by commas. If the Flags attribute is not set, an invalid value is displayed as a numeric entry. |