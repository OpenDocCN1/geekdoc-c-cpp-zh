# *Using Assignment Statement*

The values are assigned just after the declarations are made.

# **Example**

```
int a,b,c;
a = 1000;
b = 0.4 e -5;
c = 'a';
```

# **CONSTANTS**

A constant is an identifier whose value cannot be changed throughout the execution of a program whereas the variable value keeps on changing.

# **C Constants Classification**

C constants can be divided into two major categories:

+   (a) Primary constants  
+   (b) Secondary constants

These constants are further classified in the following diagram.

![](bbox=[0.075, 0.483, 0.428, 0.698])

Now we will discuss only primary constants, namely, integer, real, character and string constants.

# *Integer Constants*

# **Rules for Constructing Integer Constants**

The following are the rules that we have to follow to form an integer constant.

+   - An integer constant must have at least one digit.
+   - It must not accept a decimal point.
+   - It can be either positive or negative.

+   - If no sign precedes an integer constant it is assumed to be positive.
+   - No commas or blanks are allowed for within an integer constant.
+   - The permissible range for integer constants is −32768 to 32767.

Truly talking the range of an integer constant depends upon the compiler. For a 16-bit compiler like Turbo C or Turbo C++ the range is −32768 to 32767. For a 32-bit compiler the range would be even bigger.

# *Classification of Integer Constants*

Further, these constant can be classified according to the base of the numbers which are as follows:

# **1. Decimal integer constants**

These consist of digits 0 through 9 and first digit should not be 0.

# **Example**

1        44        3277 are valid decimal integer constants

The following are the invalid decimal constants
12, 45        , not allowed
36.0           illegal char
1 010          blankspace not allowed
10 − 10        illegal char −
0900           the first digit should not be a zero

# **2. Octal integer constants**

These consist of digits 0 through 7. The first digit must be zero in order to identify the constant as an octal number.

# **Example**

Valid octal integer constants are as follows:
0          01          0743          0777
Invalid octal integer constants are as follows:
743        does not begin with 0
0438       illegal character 8
0777.77    illegal char.

# **3. Hexadecimal integer constants**

These constants begin with 0x or 0X and are followed by combination of digits taken from hexadecimal digits 0 to 9, a to f or A to F.

The following are the valid hexadecimal constants:
0X0        0X1        0XF77        0xabcd.