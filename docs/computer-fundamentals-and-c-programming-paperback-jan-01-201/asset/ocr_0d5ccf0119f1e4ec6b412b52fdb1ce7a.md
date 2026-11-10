```
printf("Contents of table[0][0] = %3d\n", **table);
printf("Contents of table[1][0] = %3d\n", **(table + 1));
printf("Contents of table[2][0] = %3d\n", **(table + 2));

printf("\nPrinting entire array ...\n");
for (i = 0; i < ROWS ; putchar('\n'), i++ )
    for (j = 0 ; j < COLUMNS ; j++)
        printf("%3d ", *(*(table + i) + j));

printf("\nBut table is actually a one-dimensional array ...\n");
for (i = 0; i < ROWS * COLUMNS ; i++ )
    printf("%3d ", *(p + i));
return 0;
}
```

PROGRAM 12.14: `pointers_in_2darray.c`

```
Size of table = 60                                      Size of entire array
Size of table[0] = 20                                   Size of 5 elements
Size of table[0][0] = 4                                 Size of 1 element

Key in 15 integers: 1 3 5 7 9 11 33 55 77 99 111 333 555 777 999
Contents of table[0][0] =   1
Contents of table[1][0] =  11
Contents of table[2][0] = 111

Printing entire array ...
  1   3   5   7   9
 11  33  55  77  99
111 333 555 777 999

But table is actually a one-dimensional array ...
  1   3   5   7   9  11  33  55  77  99 111 333 555 777 999
```

PROGRAM OUTPUT: `pointers_in_2darray.c`

# 12.17 THE GENERIC OR VOID POINTER

If you thought that variables of three data types need three types of pointers to point to them, then you probably are not aware of the *generic pointer*. This special pointer can point to a variable of any type. A generic pointer is declared using the keyword `void`, and has the type `void *`. Consider the following declaration of a generic pointer variable named `void_p`:

```
void *void_p;
```

Even though `void_p` doesn’t have a specific data type, it can be made to point to, say, an `int` variable `x`:

```
int x = 5;
void_p = &x;
```