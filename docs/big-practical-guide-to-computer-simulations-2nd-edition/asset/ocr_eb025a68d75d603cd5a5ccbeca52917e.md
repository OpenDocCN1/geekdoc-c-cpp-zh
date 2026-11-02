Hence, if you try to assign a value to num_rows somewhere else in the program, the compiler will report an error.

Other fundamental data types, which have similar fundamental properties and usage like int, include

+   - **short int**
+   If you are sure that you do not need large numbers for specific variables, you can economize memory by using this data type. It consumes only two bytes, hence numbers in the range [−2^15, 2^15−1] are feasible, while for unsigned short int, numbers in the range [0, 2^16−1] can be used. Variables of these types are handled exactly like int variables.

+   - **char**
+   This data type is used to store characters using the ASCII coding systems in one byte. Characters which are assigned have to be given in single quotes. When printing characters using printf(), the conversion specification %c can be used. The following three lines define a variable of type char, assign a character and print it.

```
char first_char;
first_char = 'a';
printf("The first character is %c.\n", first_char);
```

Note that you can also use char variables to store integers in the range [−128, 127]. Therefore, when you print the variable first_char using the %d conversion specification, you will get the ASCII code number of the contained character, e.g. the number 97 for the letter 'a' and the number 10 for '\n'. The code numbers might be machine and/or operating system dependent.
Variables of the type unsigned char can store numbers in the range [0,255].

+   - **double and float**
+   These are used to store floating-point numbers. Usually float needs four bytes, allowing for numbers up/down to ±3.4 × 10^38, while double uses eight bytes allowing for much larger numbers (±9 × 10^307).
+   When assigning float or double numbers, one can e.g. use the fixed point notation like in −124.38 or a "scientific" notation in the form −1.2438e2 which means −1.2438 × 10^2 (equivalently you could write −12.438e1 or −1243.8e−1). Note that the numeric