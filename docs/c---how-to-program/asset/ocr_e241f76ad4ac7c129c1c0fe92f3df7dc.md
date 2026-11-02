```
```c
10    const char *string2 = "four";
11    const char *string3 = "Boston";
12
13    printf("%s%s%s%u%s\n", "The length of ", string1, " is ", strlen(string1),
14    "The length of ", string2, " is ", strlen(string2),
15    "The length of ", string3, " is ", strlen(string3));
16    }
17 }
```
```

```
```
The length of "abcdefghijklmnopqrstuvwxyz" is 26
The length of "four" is 4
The length of "Boston" is 6
```
```

Fig. 8.35 | Using function strlen. (Part 2 of 2.)

# ## 8.11 Secure C Programming

# ### *Secure String-Processing Functions*

Earlier Secure C Programming sections in this book covered C11's more secure functions printf_s and scanf_s. In this chapter, we presented functions sprintf, strcpy, strncpy, strcat, strncat, strlen, memcpy, memmove and memset. More secure versions of these and many other string-processing and input/output functions are described by the C11 standard's *optional* Annex K. If your C compiler supports Annex K, you should use the secure versions of these functions. Among other things, the more secure versions help prevent buffer overflows by requiring additional parameters that specify the number of elements in a target array and by ensuring that pointer arguments are non-NULL.

# ### *Reading Numeric Inputs and Input Validation*

It's important to validate the data that you input into a program. For example, when you ask the user to enter an int in the range 1–100, then attempt to read that int using scanf, there are several possible problems. The user could enter:

+   * an int that's outside the program's required range (such as 102).
+   * an int that's outside the allowed range for ints on that computer (such as 8,000,000,000 on a machine with 32-bit ints).
+   * a noninteger numeric value (such as 27.43).
+   * a nonnumeric value (such as FOVR).

You can use various functions that you learned in this chapter to fully validate such input. For example, you could

+   * use fgets to read the input as a line of text,
+   * convert the string to a number using strtol and ensure that the conversion was successful, then
+   * ensure that the value is in range.

For more information and techniques for converting input to numeric values, see CERT guideline INT05-C at www.securecoding.cert.org.