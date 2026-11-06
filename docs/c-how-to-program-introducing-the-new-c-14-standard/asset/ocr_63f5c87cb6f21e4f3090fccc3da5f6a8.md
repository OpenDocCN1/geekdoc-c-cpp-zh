# Section 4.9.4 Arithmetic Overflow

+   - Adding two integers could result in a value that’s too large to store in an `int` variable. This is known as **arithmetic overflow** (p. 122) and causes undefined behavior, which can lead to unintended results and security problems.
+   - The maximum and minimum values that can be stored in an `int` variable are represented by the constants `INT_MAX` and `INT_MIN`, respectively, which are defined in the header `<climits>`. There are similar constants for the other integral types and for floating-point types.
+   - To see these constants’ values on your platform, open the headers `<climits>` and `<cfloat>` in a text editor (you can search your file system for these files).