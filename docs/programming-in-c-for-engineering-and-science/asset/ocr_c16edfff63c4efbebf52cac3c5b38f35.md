# 8.3.1.2 Objects

From our behavioral description, we have the following objects in this problem:²

| Problem Objects | Type | Software Objects |  |
|---|---|---|---|
|  |  | Kind | Name |
| menu | string | constant | MENU |
| conversion | char | variable | conversion |
| temperature | double | variable | temperature |
| result | double | variable | result |

We can thus specify the problem as follows:

Input: temperature, a double; and conversion, a char
Precondition: conversion is in the range A–F (or a–f)
Output: MENU, prompts for input, and the result of converting the temperature

# 8.3.1.3 Operations

Our behavioral description leads to the following list of operations:

+   i. Display prompts and MENU (strings) on the screen.
+   ii. Read temperature (a double) from the keyboard.
+   iii. Read conversion (a char) from the keyboard.
+   iv. Select the conversion function corresponding to conversion and apply it to temperature.

All of these are provided in C++. For operation (iv), we must compare conversion to each of the valid menu choices, and based on that comparison, select an appropriate conversion function.

# 8.3.1.4 Algorithm

The following algorithm applies this strategy.

# Algorithm to Convert Arbitrary Temperatures

+   1. Display MENU via cout.
+   2. Read conversion from cin.
+   3. Display a prompt for a temperature via cout.
+   4. Read temperature from cin.