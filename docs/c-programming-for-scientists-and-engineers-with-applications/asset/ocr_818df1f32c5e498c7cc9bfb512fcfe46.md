```
scanf("%4d %5d %6d", &var1, &var2, &var3);
```

```
printf("%d  %d  %d", var1, var2, var3);
```

The numbers can be entered with one space as follows:

7865–5134 690487

The spaces in the scanf format control specification directs the computer to skip the spaces between the data values, then pick up the number of characters specified by the field width.

Notice that the first four non-blank characters are read as the value of var1, the next five are read as the value of var2, and the last six are read as the value of var3.

The output will appear with four blank spaces between the numbers as follows:

7865  -5134  690487

The spaces in the printf format control field direct the computer to output an equal number of spaces between the data values.

Notice that the first four characters are printed as the value of var1, the next five characters are printed as the value of var2, and the last six characters are printed as the value of var3 with four blank spaces between the numbers as specified in the format control field.

Input of Real Numbers The following numbers are to be input into the variables, var1, var2, var3.

78654–5.1348690.4878

The code to input these numbers is as follows:

```
float var1, var2, var3;
```

```
scanf("%6f %7f %8f", &var1, &var2, &var3);
```

```
printf("%f  %f  %f", var1, var2, var3);
```