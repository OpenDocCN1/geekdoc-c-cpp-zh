![](bbox=[0.253, 0.126, 0.739, 0.303])

Conversions between a class and a built-in data type and between a class and a class can be made with methods almost identical in form to the operator functions shown in Section 11.1. A conversion from a built-in data type to a class is made by using constructor methods. All three new conversion possibilities are shown by using the Date class and the long integer relationship shown in Figure 11.5. For completeness, the conversion from a built-in data type is included.

# Built-in to Built-in Conversion

A built-in to built-in conversion is handled by C++’s implicit conversion rules or its explicit cast operator. To review briefly, this type of conversion is implicit or explicit. An implicit conversion can occur by assignment. For example, when a floating-point value is assigned to an integer variable, only the integer portion of the value is stored. Implied conversions are performed automatically by the compiler.

An explicit conversion occurs when a cast is used. In C++, two cast notations exist. The older C notation has the form (datatype) expression, and the newer C++ notation has the function-like form datatype(expression). For example, both the expressions (int)24.32 and int(24.32) cause the double-precision value 24.32 to be truncated to the integer value 24.

# Class to Built-in Conversion

Conversion from a user-defined data type to a built-in data type is accomplished by using a conversion operator function. These conversions are also referred to as “casts.” Creating a conversion operator or cast is identical to creating an operator function (discussed in Section 11.1) with one exception: A built-in data type name is used instead of a built-in symbol in the function’s header. Therefore, a conversion operator function for casting a Date object to a long integer must be named operator long(). Program 11.6 defines this function and uses it to convert a Date object to a long integer. The function’s prototype, definition, and call are shaded in the program.