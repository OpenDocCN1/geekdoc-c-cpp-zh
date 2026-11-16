Similarly there are equivalents to the functions `printf()` and `scanf()` which read or write data to files. These are called `fprintf()` and `fscanf_s()`. The functions are used in the same way, except that the `fprintf()` and `fscanf_s()` take the file pointer as an additional first argument:

+   • `fprintf(fp, formatSpecifiers, arguments);`
+   Performs the analogous operations of the `printf()` function on a file. It returns the number of bytes output. In the event of error, it returns `EOF`.

Its function prototype is:
`int fprintf(FILE *fp, formatSpecifiers, arguments);`

+   • `fscanf_s(fp, format_specifiers, arguments);`
+   Performs the analogous operations of the `scanf_s()` function on a file. It returns the number of arguments that are successfully assigned or the value of `EOF` if the end of file is reached.

Its function prototype is:
`int fscanf_s(FILE *fp, format_specifiers, arguments);`

Additionally, there are equivalent functions to `gets()` and `puts()` for file manipulation:

+   • `fgets(s, N, fp));`
+   Characters are read from the file pointed to by `fp`, and placed into string `s` until either N-1 characters have been read or a newline character is read, whichever comes first. Unlike `gets(s)`, if a newline character is read, it is placed in `s`. In both cases, `s` is terminated with a NULL character. The value of `s` (pointer to `char`) is returned.

Its function prototype is:
`char *fgets(char *s, int N, FILE *fp);`