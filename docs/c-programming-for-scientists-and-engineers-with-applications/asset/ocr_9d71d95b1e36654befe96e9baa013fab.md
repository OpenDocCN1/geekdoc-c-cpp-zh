```
fclose( infptr );
return 0;

```

```
strdata.dat
ABXCLMKN\nXCNOPK\nLKFTYGGHIIJKK\n
```

+   first string read ABXCLMKN\n
second string read XCNOPK\n
third string read LKRFTYGGHIIJJ
fourth string read KK\n

Output of Strings There are special functions available exclusively for the output of strings in the C library stdio.h. These output functions puts() and fputs().

Function puts() The puts() has only one argument, which is the string name. This function displays a string excluding the null terminator. This function also activates the newline character '\n', so that any further output will be on the next line. The following example shows the output of a string stored in strname.

```
strname
```

| A | B | X | C | L | M | K | N | \0 | | | | | |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |

```
puts(strname);
puts(strname);
puts(strname);
```

The output is:

```
ABXCLMKN
ABXCLMKN
ABXCLMKN
```

Notice that there is no newline character specified in the output statement. puts() function automatically shifts to a newline after output.

Function fputs() The fputs() function is used to write character strings to a data file. This function has two arguments, the first argument is the string name