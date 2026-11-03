correctness depends on the solution procedure, the clarity depends on the way the output is presented. Following are some of the steps we can take to improve the clarity and hence the readability and understand- ability of outputs.

+   1. Provide enough blank space between two numbers.
+   2. Introduce appropriate headings and variable names in the output.
+   3. Print special messages whenever a peculiar condition occurs in the output.
+   4. Introduce blank lines between the important sections of the output.

The system usually provides two blank spaces between the numbers. However, this can be increased by selecting a suitable field width for the numbers or by introducing a 'tab' character between the specifications. For example, the statement

```
printf("a = %d\t b = %d", a, b);
```

# Table 1.16 Commonly used printf Format Codes

| Code | Meaning |
|------|---------|
| %c | print a single character |
| %d | print a decimal integer |
| %e | print a floating point value in exponent form |
| %f | print a floating value without exponent |
| %g | print a floating point value either e-type or f-type depending on |
| %i | print a signed decimal integer |
| %o | print an octal integer, without leading zero |
| %s | print a string |
| %u | print an unsigned decimal integer |
| %x | print a hexadecimal integer, without leading Ox |

# Table 1.17 Commonly used Output Format Flags

| Flag | Meaning |
|------|---------|
| - | Output is left-justified within the field. Remaining field will be blank. |
| + | + or – will precede the signed numeric item. |
| 0 | Causes leading zeros to appear. |
| # (with o or x) | Causes octal and hex items to be preceded by O and Ox, respectively. |
| # (with e, f or g) | Causes a decimal point to be present in all floating point numbers, even if it is whole number. Also prevents the truncation of trailing zeros in g-type conversion. |

will provide four blank spaces between the two fields. We can also print them on two separate lines by using the statement

```
printf("a = %d\n b = %d", a, b);
```

Messages and headings can be printed by using the character strings directly in the printf statement. Examples:

```
printf("\n OUTPUT RESULTS \n");
printf("Code\t Name\t Age\n");
printf("Error in input data\n");
printf("Enter your name\n");
```