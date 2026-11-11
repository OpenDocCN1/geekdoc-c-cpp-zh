```
exit(1); /* terminate program */
}
else if (fp2 == NULL)
{
printf("Cannot open prog.old for writing \n");
exit(1); /* terminate program */
}
else /* both files O.K. */
{
c = getc(fp1);
while (c != EOF)
{
putc(c, fp2); /* copy to prog.old */
c = getc(fp1);
}
fclose ( fp1 );/* Now close files */
fclose ( fp2 );
printf("Files successfully copied \n");
}
getch();
}
```

```
printf("Cannot open %s for reading \n", fname1);
exit(1); /* terminate program */
}
else if (fp2 == NULL)
{
printf("Cannot open %s for writing \n", fname2);
exit(1); /* terminate program */
}
else /* both files O.K. */
{
c = getc(fp1);        /* read from source */
while (c != EOF)
{
putc( c, fp2); /* copy to destination */
c = getc(fp1);
}
fclose ( fp1 );/* Now close files */
fclose ( fp2 );
printf("Files successfully copied \n");
}
getch();
}
```

# Problem 7

The above program only copies the specific file prog.c to the file prog.old. We can make it a general purpose program by prompting the user for the files to be copied and opening them appropriately.

# Solution

```
#include <stdio.h>
#include<conio.h>
void main()
{
    FILE *fp1, *fp2, *fopen();
    int c ;
    char fname1[40], fname2[40] ;
    clrscr();
    printf("Enter source file: ");
    gets(fname1);
    printf("Enter destination file: ");
    gets(fname2);
    fp1 = fopen( fname1, "r"); /* open for reading */
    fp2 = fopen( fname2, "w"); /* open for writing */
    if ( fp1 == NULL) /* check does file exist */
    {
```

# NUMERIC LIBRARY

cmath declares a set of functions to compute common mathematical operations and transformations.

# TRIGONOMETRIC FUNCTIONS

In the trigonometric functions we will discuss the following functions:

| Function | Description |
|---|---|
| cos() | Compute cosine |
| sin() | Compute sine |
| tan() | Compute tangent |
| acos() | Compute arccosine |
| asin() | Compute arc sine |
| atan() | Compute arc tangent |
| atan2() | Compute arc tangent with two parameters |

(c) cos()
cos() function is used to compute cosine.
The general syntax of cos() function is as follows:

```
double cos (double x );
float cos (float x );
long double cos ( long double x );
```