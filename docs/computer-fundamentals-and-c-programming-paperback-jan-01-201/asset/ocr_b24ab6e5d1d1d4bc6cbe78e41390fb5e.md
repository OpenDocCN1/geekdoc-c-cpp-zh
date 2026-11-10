14.20 Write a program to store a date in an optimized structure that includes properly-sized bit fields. The program accepts a date as three integers in the form *dd mm yyyy* and prints the values using the structure.

14.21 Correct the following code so as to print 5 for MAY and 12 for DEC:

```
enum E {JAN, FEB, MAR, APR, MAY, JUN, DEC};
E month;
month = MAY;
printf("%d\n", month);
month = DEC;
printf("%d\n", month);
```

14.22 Write a program that assigns the values 1, 2 and 4, representing read, write and execute permissions, to an enumeration. With valid user input, the program must print a message, say, "File has read permission."