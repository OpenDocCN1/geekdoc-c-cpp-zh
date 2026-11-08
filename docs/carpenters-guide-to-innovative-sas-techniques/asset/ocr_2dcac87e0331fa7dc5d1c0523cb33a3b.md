+   1. The values which will not properly convert are saved in a data set.
+   2. The ANYALPHA function is used to determine if the conversion will be successful, and any values that will cause a problem are written out to the data set VALCHECK for further evaluation.
+   3. The remaining values are converted using the BEST. informat. The ?? format modifier could
+   
+           nval(i) = input(val(i),?? best.); ❻
+   
+       also be used to suppress the error messages in the LOG; however, in this example we want notification of the invalid values.
+   4. The observation with the converted values is written to the new data set.

This solution will not work for character values containing scientific notation. While the BEST. informat will successfully convert values containing scientific notation, the ANYALPHA function will also flag the 'E'. Additional logic such as used in the autocall macro function %DATATYP would be required.

The NOT family of functions, which also contains over a dozen functions, are nominally the functional opposite of the ANY functions. These functions are used to detect text that is *not* present. For instance the NOTALPHA function returns the position of the first non-alpha character. The NOTDIGIT is very similar to the ANYALPHA function; however, NOTDIGIT could not be substituted for ANYALPHA at ❷ above. NOTDIGIT detects trailing blanks, plus signs, minus signs, and decimal points even though they could be part of a number. A nearly equivalent use of NOTDIGIT to the ANYALPHA shown above could be coded as:

```
if notdigit(trim(left(compress(val(i),'+-.')))) then do; ❷
```

All of the functions in these two families have an optional second argument, which adds a great deal of flexibility to what these functions can accomplish. This argument, which is the start

    text = '1234x6yz9';
    pos = anyalpha(text,-6);

position, can be either a positive or negative integer. When negative, the search is right to left rather than left to right as it is when positive. In either case the value returned is the position counting left to right. In the example shown here, the ANYALPHA will find the letter 'x' and will return a 5.

# #### MORE INFORMATION

The ANYDIGIT function is used in one of the examples in Section 3.6.5 and one of the examples in Section 3.6.6 uses the ANYALPHA function. The ?? format modifier is introduced in Section 1.3.1 and used with the INPUT function in Section 2.3.1.

# ### 3.6.2 Comparison Functions

Performing inexact comparisons has always been, well, inexact, not to mention tedious and difficult. Traditional comparison functions have included SOUNDEX and SPEDIST. This family of comparison functions has been expanded and now provides several ways to look at the similarities or differences between two strings. These additional functions include:

+   - COMPARE compares two strings
+   - COMPLEV computes a distance between two strings based on similarities
+   - COMPGED computes a generalized distance between two strings
+   - COMPCOST this routine adjusts the comparison criteria for COMPGED