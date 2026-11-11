+   - Mantissa: Represents the part before the letter e, where e represents the exponential notation used for scientific calculations
+   - Exponent: Represents the part after the letter e

The following are the rules for the exponential form of floating point constants:

+   - They must separate the mantissa and exponent parts with the letter e
+   - They can have either positive or negative values in the mantissa and exponent parts
+   - They must be within the range -3.4e38 and 3.4e38

The following code snippet shows the declaration of the exponential form of floating point constants:

```
```cpp
const float num1 = +3.2e-1; // positive exponential floating point constant
const float num2 = -3.2e-1; // negative exponential floating point constant
```
```

In the preceding code snippet, the num1 floating point constant contains a positive exponential value and the num2 floating point constant contains a negative exponential value.

# ## Character Constants

Character constants are the constants that have a single character enclosed within a single quote. Character constants are of type char. The following are examples of valid character constants:

```
```cpp
const char ch1 = 'f ' // character constant
const char ch2 = 'g' // another character constant
```
```

In the preceding code snippet, ch1 and ch2 are character constants.

We continue with our discussion on C++ fundamentals and take up the declaration and initialization of variables in C++.

# ## Variables

A variable is an identifier used to store or represent some specific type of information within a program. In other words, a variable is a constant whose value may change in the program. A variable can be of integer, floating point, or character type. While declaring a variable, the name of the variable and the type of value it will hold is specified. The rules for variable names are as follows:

+   - They can be in a combination of alphabets, digits, or underscores
+   - They must have an alphabet as the first character
+   - They must not have commas or blanks
+   - They must not have a special symbol, except an underscore

Before using variables in a program, you must declare and then initialize them. In this section, we discuss the following topics in the context of variables:

+   - Declaration of variables