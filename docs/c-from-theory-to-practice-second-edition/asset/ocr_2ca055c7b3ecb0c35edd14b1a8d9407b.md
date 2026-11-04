`str` points to the string to be written in the file indicated by `fp`. If it is successful, `fputs()` returns a nonnegative value, `EOF` otherwise.

# ### The fprintf() Function

The `fprintf()` function is more generic than `fputs()` because it can write a variable number of different data items to an output file. Like `printf()`, `fprintf()` uses a format string to define the order and the type of data written in the file. It is declared in `stdio.h`:

```
```c
int fprintf(FILE* fp, const char *format, ...);
```
```

The only difference between them is that `printf()` always writes data to `stdout`, while `fprintf()` writes to the file indicated by `fp`. In fact, if `fp` is replaced by `stdout`, `fprintf()` call is equivalent to `printf()` call. If it is successful, `fprintf()` returns the number of bytes written in the file, a negative value otherwise.

The `stdin` (*standard input*), `stderr` (*standard error*), and `stdout` (*standard output*) streams are declared in `stdio.h` as pointers of type `FILE*` and they are ready to use; it is not needed to open or close them. By default, the `stdout` and `stderr` output streams are associated with the screen, while the `stdin` input stream is associated with the keyboard. An operating system (e.g., Unix) may allow their redirection. For example, if the name of the executable is `test` and we write in the command line:

```
```
test >output.txt
```
```

the data written in `stdout` (e.g., with `printf()`) won't be displayed in the screen, but it will be written in the `output.txt` file. Notice that the program does not realize the redirection. In particular, the `>output.txt` is not interpreted as an argument of `main()`.

The following program uses `fputs()` and `fprintf()` to write some data in a text file:

```
```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    FILE *fp;
    char str[] = "Hello_2";
    int i;

    fp = fopen("test.txt", "w"); /* Open file for writing. */
    if(fp == NULL)
    {
        printf("Error: fopen() failed\n");
        exit(EXIT_FAILURE);
    }
    fputs("Hello_1\n", fp);
    for(i = 0; i < 3; i++)
        fprintf(fp, "%d. %s\n", i+1, str); /* Use fprintf() to write
a string along with an increasing number. */
    fclose(fp);
    return 0;
}
```
```