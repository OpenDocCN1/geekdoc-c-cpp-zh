The ftell() function is used to find the current position of a file pointer. It is declared in stdio.h:

```
long int ftell(FILE *fp);
```

ftell() returns the current position of the file pointer associated with fp. The position is expressed as the number of bytes from the beginning of the file. If an error occurs, ftell() returns -1. ftell() may be used together with fseek() to return to a previous file position, like this:

```
long int old_pos;
/* ... open file and so some work with it. */
old_pos = ftell(fp);
/* ... do some other work. */
fseek(fp, old_pos, SEEK_SET); /* return back to the old position. */
```

Tip It is safer to use fseek() and ftell() with binary rather than text files because potential translations of the new line character can produce unexpected results. fseek() is guaranteed to work with text files only if:

+   a. offset is 0 or
+   b. offset is obtained from a previous call to ftell() and origin is set to SEEK_SET.

# Write and Read Data from a Binary File

The fwrite() and fread() functions are used to write and read data from a binary file. These functions are used primarily with binary files, although we can use them, with some care, with text files as well.

# The fwrite() Function

The fwrite() function is very useful for writing large blocks of data in a single step. It is declared in stdio.h:

```
int fwrite(const void *buf, size_t size, size_t count, FILE *fp);
```

The first argument points to the memory that holds the data to be written in the file indicated by fp. The third argument specifies how many elements will be written in the file, while the second one specifies the size of one element in bytes. The product of the second and third arguments specifies the number of the bytes to be written in the file. For example, to write an array of 1000 integers, the second argument should be equal to the size of one integer, that is, 4, while the third argument should be equal to 1000.

```
int arr[1000];
fwrite(arr, 4, 1000, fp);
```