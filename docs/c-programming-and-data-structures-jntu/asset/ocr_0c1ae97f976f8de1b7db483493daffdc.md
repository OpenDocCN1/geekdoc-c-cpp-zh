```
Program
/************************************************/
/*      PRINTING OF CHARACTERS AND STRINGS      */
/************************************************/
main()
{
    char x = 'A';
    static char name[20] = "ANIL KUMAR GUPTA";
    printf("OUTPUT OF CHARACTERS\n");
    printf("%c\n%c\n%5c\n", x,x,x);
    printf("%3c\n%3c\n", x,x);
    printf("\n");
    printf("OUTPUT OF STRINGS\n");
    printf("%s\n", name);
    printf("%20s\n", name);
    printf("%20.10s\n", name);
    printf("%5s\n", name);
    printf("%-20.10s\n", name);
    printf("%5s\n", name);
}
Output
OUTPUT OF CHARACTERS
A
  A
    A
A
OUTPUT OF STRINGS
ANIL KUMAR GUPTA
        ANIL KUMAR GUPTA
    ANIL KUMAR
ANIL
ANIL KUMAR
ANIL KUMAR GUPTA
```

# Fig. 5.11 Printing of characters and strings

Commonly used printf format codes are given in Table 5.3 and format flags in Table 5.4.

# Table 5.3 printf Format Codes

| Code | Meaning |
|------|---------|
| %c | print a single character |
| %d | print a decimal integer |
| %e | print a floating point value in exponent form |
| %f | print a floating point value without exponent |
| %g | print a floating point value either e-type or f-type depending on value |
| %i | print a signed decimal integer |
| %o | print an octal integer, without leading zero |
| %s | print a string |
| %u | print an unsigned decimal integer |
| %x | print a hexadecimal integer, without leading 0x |