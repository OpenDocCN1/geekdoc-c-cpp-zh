```
i++;
if (st[i] == '\n')
    st[i] = '\0';
else // must have words[i] == '\0'
    while (getchar() != '\n')
        continue;
}
return ret_val;
}
```

Here is some sample output:

```
Enter a number (empty line to quit):
10
base 10 input, base 10 output: 10, stopped at  (0)
base 16 input, base 10 output: 16, stopped at  (0)
Next number:
10atom
base 10 input, base 10 output: 10, stopped at atom (97)
base 16 input, base 10 output: 266, stopped at tom (116)
Next number:

Bye!
```

First, note that the string "10" is converted to the number 10 when base is 10 and to 16 when base is 16. Also note that if end points to a character, *end is a character. Therefore, the first conversion ended when the null character was reached, so end pointed to the null character. Printing end displays an empty string, and printing *end with the %d format displays the ASCII code for the null character.

For the second input string (base-10 interpretation), end is given the address of the 'a' character. So printing end displays the string "atom", and printing *end displays the ASCII code for the 'a' character. When the base is changed to 16, however, the 'a' character is recognized as a valid hexadecimal digit, and the function converts the hexadecimal number 10a to 266, base 10.

The strtol() function goes up to base 36, using the letters through 'z' as digits. The strtoul() function does the same, but converts unsigned values. The strtod() function does only base 10, so it uses just two arguments.

Many implementations have itoa() and ftoa() functions for converting integers and floating-point values to strings. However, they are not part of the standard C library; use sprintf(), instead, for greater compatibility.