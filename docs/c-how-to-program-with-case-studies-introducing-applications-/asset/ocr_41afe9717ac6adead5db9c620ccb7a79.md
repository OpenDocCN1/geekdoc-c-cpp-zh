+   - a character array in which to place the input string and
+   - the array's number of elements.

The function uses the number of elements to prevent buffer overflows. For example, it’s possible to supply a field width for `%s` that’s too long for the underlying character array, or to simply omit the field width entirely. With `scanf_s`, if the number of characters input plus the terminating null character is larger than the number of array elements specified, the `%s` conversion fails. For the preceding statement, which contains only one conversion specification, `scanf_s` would return 0, indicating no conversions were performed. The array `myString` would be unaltered. We discuss additional Annex K functions in later Secure C Programming sections.

Not all compilers support the C11 standard’s Annex K functions. For programs that must compile on multiple platforms and compilers, you might have to edit your code to use the versions of `scanf_s` or `scanf` available on each platform. Your compiler might also require a specific setting to enable you to use the Annex K functions.

# ### Don't Use Strings Read from the User as Format-Control Strings

You might have noticed that throughout this book, we do not use single-argument `printf` statements. Instead, we use one of the following forms:

+   - When we need to output a `'\n'` after the string, we use function `puts` (which automatically outputs a `'\n'` after its single string argument), as in

```
```c
puts("Welcome to C!");
```
```

+   - When we need the cursor to remain on the same line as the string, we use function `printf`, as in

```
```c
printf("%s", "Enter first integer: ");
```
```

Because we were displaying string literals, we certainly could have used the one-argument form of `printf`, as in

```
```c
printf("Welcome to C!\n");
printf("Enter first integer: ");
```
```

When `printf` evaluates the format-control string in its first (and possibly only) argument, it performs tasks based on the conversion specification(s) in that string. If the format-control string were obtained from the user, an attacker could supply malicious conversion specifications that would be “executed” by the formatted output function. Now that you know how to read strings into character arrays, it’s important to note that you should never use as a `printf`’s format-control string a character array that might contain user input. For more information, see CERT guideline FIO30-C at https://wiki.sei.cmu.edu/confluence.

# ### Self Check

+   1. *(Multiple Choice)* Which of the following statements a), b) or c) is *false*?
+      a) It's important to ensure that every index you use to access an array element is within the array's bounds. A one-dimensional array's indexes must be greater