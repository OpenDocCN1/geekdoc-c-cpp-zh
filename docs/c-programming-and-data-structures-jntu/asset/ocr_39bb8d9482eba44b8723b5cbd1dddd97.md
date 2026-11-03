+   3. Uppercase and lowercase are significant. That is, the variable Total is not the same as total or TOTAL.
+   4. The variable name should not be a keyword.
+   5. White space is not allowed.

Some examples of valid variable names are:

John    Value    T_raise
Delhi   x1       ph_value
mark    sum1     distance

Invalid examples include:

123        (area)
%          25th

Further examples of variable names and their correctness are given in Table 3.4.

# Table 3.4 Examples of Variable Names

| Variable name | Valid? | Remark |
|---|---|---|
| First_tag | Valid | |
| char | Not valid | char is a keyword |
| Price$ | Not valid | Dollar sign is illegal |
| group one | Not valid | Blank space is not permitted |
| average_number | Valid | First eight characters are significant |
| int_type | Valid | Keyword may be part of a name |

If only the first eight characters are recognized by a compiler, then the two names average_height average_weight mean the same thing to the computer.

Such names can be rewritten as avg_height and avg_weight

or

ht_average and wt_average

without changing their meanings.

# 3.7 BASIC DATA TYPES AND SIZES

C language is rich in its data types. Storage representations and machine instructions to handle constants differ from machine to machine. The variety of data types available allow the programmer to select the type appropriate to the needs to the application as well as the machine.

ANSI C supports four classes of data types:

+   1. Primary (or fundamental) data types
+   2. User-defined data types
+   3. Derived data types
+   4. Empty data set