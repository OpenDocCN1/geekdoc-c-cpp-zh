```
int main(void)
{
    FILE *fp;
    int c, x;
    char buf[80] = "A1234 abcd";
    char stg[80];

    fp = fopen("foo", "w+");                 /* File will also be read */
    fputs(buf, fp);                            /* Writes buf to foo */

    rewind(fp);                                /* At position 0 in foo */
    c = fgetc(fp);
    fputc(c, stdout);                          /* Prints "A" */

    fscanf(fp, "%d", &x);
    fprintf(stdout, "%d", x);                 /* Prints "1234" */

    fgets(stg, 79, fp);
    fputs(stg, stdout);                        /* Prints " abcd" */

    exit(0);
}
```

PROGRAM 15.2: **mixing_functions.c**

A1234 abcd

PROGRAM OUTPUT: **mixing_functions.c**

# 15.5.2  The fgetc and fputc Functions Revisited

|  |  |
|---|---|
| Prototype: | `int fgetc(FILE *stream);` |
| Return value: | The character read on success, EOF on error or end-of-file. |
| Prototype: | `int fputc(int c, FILE *stream);` |
| Return value: | The character written on success, EOF on error. |

The **fgetc** and **fputc** functions have been used in Section 9.7.1 to interact with the terminal using `stdin` and `stdout`, respectively, as the file pointers. **fgetc** accepts the file pointer *stream* as a single argument. It fetches and returns a character from the buffer associated with *stream*. This is how the function is typically used:

```
int c;
c = fgetc(fp);
```

*fp returned by a prior fopen*

Here, **fgetc** returns a character from the buffer associated with `fp`. To read an entire file, **fgetc** must be used in a loop which terminates when **fgetc** detects EOF:

```
while ((c = fgetc(fp)) != EOF)
```

*EOF flag set in FILE structure*