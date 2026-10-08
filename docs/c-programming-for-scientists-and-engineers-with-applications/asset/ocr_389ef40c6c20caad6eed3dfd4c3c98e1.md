# Failsafe Input of Numbers

The following decimal numbers contained in a data myfile2.dat,

```
695.23 23.5647 0.2034 2349.7658
```

are to be input into the variables var1, var2, var3, and var4.

The following code shows the input.:

```
FILE *inptr;
```

```
float var1, var2, var3, var4;
```

```
inptr = fopen("myfile2.dat", "r");
```

```
if(inptr)
{
    fcanf(inptr, "%f %f", &var1, &var2);
    fcanf(inptr, "%f %f", &var3, &var4);
}
else
{
    printf("myfile2.dat not available\n");
}
```

Notice that if the file is opened successfully for input, inptr is a pointer to the file that is interpreted as "true," otherwise inptr is a null pointer that is read from the input file and stored in the variables var1, var2, var3, and var4. If the file is not successfully opened for input then an error message is displayed on the screen.

# 3.2.4 Output to a Data File

Output to a data file uses a function call to the fprintf( ) library function. The general form of the function call is:

```
fprintf(file pointer, "format control string", var1,....varn);
```

The first argument must be the output file pointer; the next, the format control string; and the remaining arguments, a list of variables. The following examples show output to a data file.