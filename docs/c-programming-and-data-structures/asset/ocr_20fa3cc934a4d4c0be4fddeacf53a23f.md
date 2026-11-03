```
Program
main()
{
    char country[15] = "United Kingdom";
    printf("\n\n");
    printf("*123456789012345*");
    printf("------\n");
    printf("%-15s\n", country);
    printf("%5s\n", country);
    printf("%15.6s\n", country);
    printf("%-15.6s\n", country);
    printf("%15.05s\n", country);
    printf("%.3s\n", country);
    printf("%5s\n", country);
    printf("------\n");
}
```

Output
*123456789012345*
------
United Kingdom
United Kingdom
United United
United
Uni
United Kingdom
------

# Fig. 4.4 Writing strings using %s format

The printf on UNIX supports another nice feature that allows for variable field width or precision. For instance

```
printf("%.*s\n", w, d, string);
```

prints the first d characters of the string in the field width of w.

This feature comes in handy for printing a sequence of characters. Example 4.5 illustrates this.

# EXAMPLE 4.5 Write a program using for loop to print the following output:

+   - C
+   - CP
+   - CPr
+   - CPro
+   - ....
+   - ....
+   - CProgramming
+   - CProgramming
+   - ....
+   - ....
+   - CPro
+   - CPr
+   - CP
+   - C