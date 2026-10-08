# Input and Output

FILE *inptr, *outptr;

inptr = fopen("myfilein.dat", "r");

outptr = fopen("myfileout.dat", "w");

The pointer type used in the declaration is FILE in capital letters. Here inptr is an input file pointer and outptr is an output file pointer. In the statement fopen is a reserved word used to open a file in C. The data file name with the data extension is given as a character string within double quotes. The mode of operation of the file is provided as the second argument, also a character string. The mode r is used for the input file, the mode w is used for the output file, and mode a is used for appending to a file.

fopen is a function that returns a pointer to the data file if it is available, or a null pointer if it is not. The input and output statements are nearly the same as standard input and output statements with the following modifications:

File Input Instead of using scanf( ) use fscanf( ), the function name for input from a data file. The first argument must be an input file pointer. The form of the input statement for file input is as follows:

```
fscanf(inptr, "format control string", &var1, &var2, &var3, ... ,&varn);
```

Notice that the first argument is an input file pointer inptr, the second argument is a format control string enclosed within double quotes as in standard input, followed by the addresses of the variables as in standard input.

File Output Instead of using printf( ) use fprintf( ), the function name for output to a data file. The first argument must be an output file pointer. The form of the output statement for file output is as follows:

```
fprintf(outptr, "format control string", var1, var2, var3, ... ,&varn);
```

Notice that the first argument is an output file pointer outptr, the second argument is a format control string enclosed within double quotes as in standard output, followed by the variables as in standard output.