```
    int a[3][4] = {{15,27,11,35},
                   {22,19,31,17},
                   {31,23,14,36}
                  };
```

The elements of a will be stored as shown below:

![](bbox=[0.24, 0.188, 0.78, 0.256])

If we declare **p** as an **int** pointer with the initial address of &a[0][0], then

a[i][j] is equivalent to *(p+4 x i+j)

You may notice that, if we increment i by 1, the **p** is incremented by 4, the size of each row, making **p** element a[2][3] is given by *(p + 2 x 4 + 3) = *(p + 11).

This is the reason why, when a two-dimensional array is declared, we must specify the size of each row so that the compiler can determine the correct storage mapping.

# ## 9.9 POINTERS AND CHARACTER STRINGS

We know that a string is an array of characters, terminated with a null character. Like in one-dimensional arrays, we can use a pointer to access the individual characters in a string. This is illustrated by the example 11.5.

# ### Example 11.5

Write a program using pointers to determine the length of a character string.

A program to count the length of a string is shown in Fig. 11.10. The statement

```
    char *cptr = name;
```

```
    Program
    /*----------------------------------------------------------------*/
    /*        POINTERS AND CHARACTER STRINGS                          */
    /*----------------------------------------------------------------*/
    main()
    {
        char *name;
        int  length;
        char *cptr = name;

        name = "DELHI";
        while(*cptr != '\0')
        {
            printf("%c is stored at address %u\n", *cptr, cptr);
            cptr++;
        }
        length = cptr - name;
        printf("\nLength of the string = %d\n", length);
    }
```