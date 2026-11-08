⑩ After checking all 10 possibilities, the closest match is written to WORK.POTENTIAL. This data set can be further examined in the process of building a mapping dictionary.

The benefits of using the comparison functions over direct comparison include the ability to make the comparison case insensitive, ignore leading blanks, compare strings of unequal length, and to remove quotes from the comparison.

Although the functions COMPBL, COMPRESS, and COMPOUND also start with the letters COMP, they are not a part of this family of comparison functions.

# MORE INFORMATION

A further discussion of DATA steps with two SET statements can be found in Section 3.8.3 and the use of the DOW loop in Section 3.9.1.

# 3.6.3  Concatenation Functions

Functions are now available that allow us to perform concatenation operations without resorting to the concatenation operator (||). These include:

+   - **CAT** — same as `||`, it preserves leading and trailing blanks
+   - **CATQ** — adds a delimiter and quotes individual items
+   - **CATS** — removes leading and trailing blanks
+   - **CATT** — removes only trailing blanks
+   - **CATX** — removes leading and trailing blanks, but also adds a separator between strings (you get to choose the separator)

The following statement, which was used in a PROC REPORT compute block, places a text string containing both the mean and standard deviation in a single report item. The resulting value might appear as something like: `15.23 (4.567)`.

```
_c5_ = cats(put(_c3_,6.2), '(' ,put(_c4_,7.3),')');
```

As a general rule the CAT functions are considered to be preferred to the concatenation operator.

# SEE ALSO

The CATS function is used in a CALL EXECUTE example in Feth and Carpenter (2007).

# 3.6.4  Finding Maximum and Minimum Values

When finding the maximum or minimum values from within a list of variables and/or values, the MAX and MIN functions are no longer the only functions from which to choose. Functions that can return the maximum and minimum values include:

+   - **LARGEST** — Returns the nᵗʰ largest value from a list of values
+   - **MAX** — Returns the largest value from a list of values
+   - **SMALLEST** — Returns the nᵗʰ smallest value from a list of values (ignores missing values)
+   - **MIN** — Returns the smallest value from a list of values (ignores missing values)
+   - **ORDINAL** — Returns the nᵗʰ smallest value from a list of values (includes missing values)