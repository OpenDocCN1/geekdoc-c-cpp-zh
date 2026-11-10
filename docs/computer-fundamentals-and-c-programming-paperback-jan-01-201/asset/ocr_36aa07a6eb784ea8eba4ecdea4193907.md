This call reads one unit of four bytes in binary form and saves it in the variable i. A string is read in the following manner:

```
    char stg[10];
    fread(stg, sizeof(char), 10, fp);
```

**fread** reads 10 characters from the stream, or rather, 10 units of one char where the unit size is specified as the second argument. What makes **fread** different from its peers is that a single call can read a set of integers into an array:

```
    short arr[5];
    fread(arr, sizeof(short), 5, fp);    // Reads five numbers to array arr
```

Like the members of the “scanf” family, **fread** returns the number of items successfully read even if the function terminates with an error. **fread** can also read multiple data items in one call provided they form members of a structure. We’ll be demonstrating this feature shortly.

# ### 15.13.2 The fwrite Function

<table><tr><td><strong>Prototype:</strong></td><td><code>size_t fwrite(void *p, size_t size, size_t num, FILE *stream);</code></td></tr><tr><td><strong>Return value:</strong></td><td>Number of items successfully written even when error is encountered.</td></tr></table>

**fread** and **fwrite** have identical prototypes; they differ only in the direction of data transfer. **fwrite** writes *num* units of data of *size* characters each from the variable *p* to the file associated with *stream*. This is how you save an entire array to a file:

```
    short arr[5] = {100, 200, 300, 400, 500};
    fwrite(arr, sizeof(short), 5, fp);
```

This is where using the binary mode can result in significant savings. The preceding **fwrite** function writes 10 bytes to disk. If these five numbers were saved in a text file, they would have taken up 15 bytes of disk space (plus one or two for the newline character).

# ### 15.13.3 fread_fwrite.c: Using the Primitive and Derived Data Types

Program 15.11 uses **fwrite** to write three data items—an integer, string and array of type short—to the file foobar, which is opened in binary mode ("w+b"). The items are originally stored in variables having the “out” suffix. They are read back using **fread** into a separate set of variables having the “in” suffix. Note that the contents of the five-element arrays, s_in and s_out, are transferred using a single invocation each of **fwrite** and **fread**.

```
    /* fread_fwrite.c: Uses fwrite to write three types of data items
                    to a file and then reads them back with fread. */
    #include <stdio.h>
    #include <stdlib.h>
    #define SIZE 15
```