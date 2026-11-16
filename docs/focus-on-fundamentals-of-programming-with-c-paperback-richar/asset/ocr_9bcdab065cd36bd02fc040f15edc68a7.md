The program output is:

The sum of 50 and 75 is 125.

Shown below is a table of control string formats:

| Format | Description |
| :--- | :--- |
| %d | integer or decimal (base 10) format |
| %ld | long decimal format |
| %f | floating point format |
| %lf | double format |
| %c | character format |
| %s | character string format |
| %u | unsigned decimal |
| %lu | unsigned long decimal format |
| %e | scientific notation format |
| %o | octal format |
| %x | hexadecimal format |

Consider the following C program:

```
// format.c
void main(void) {
   int i = 65;
   char c = 'A';
   printf("Decimal = %d Char = %c\n", i, i);
   printf("Decimal = %d Char = %c\n", c, c);
}
```