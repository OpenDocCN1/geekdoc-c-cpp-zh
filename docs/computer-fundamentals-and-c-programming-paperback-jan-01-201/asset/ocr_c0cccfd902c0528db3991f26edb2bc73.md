# ## 15.14 MANIPULATING THE FILE POSITION INDICATOR

Normally, files are read and written sequentially, with the file position indicator initially set to 0, the beginning of the stream. Sequential access can be terribly inefficient for large files, specially when the line to be accessed occurs near the end of the file. C supports a set of functions—`fseek`, `ftell` and `rewind`—that can directly take the file offset pointer to any point in the stream and report the current position of the offset pointer. These functions allow a file to be accessed in a *random* manner.

# ### 15.14.1 `fseek`: Positioning the Offset Pointer

Prototype: `int fseek(FILE *stream, long offset, int whence);`
Return value: 0 on success, -1 on failure.

The `fseek` function moves the file offset pointer to a specified point. `fseek` doesn't do any physical I/O, but it determines the position in the file where the next I/O operation will take place. The *offset* and *whence* arguments together control the location of the file's offset pointer. *offset* signifies the position (positive or negative) of this pointer relative to *whence*, which can take one of three values:

+   - `SEEK_SET` — Offset pointer set to beginning of file.
+   - `SEEK_END` — Offset pointer set to end of file.
+   - `SEEK_CUR` — Offset pointer remains at current location.

These constants have the values 0, 1 and 2. With some restrictions, *offset* can be a positive or negative integer, and a constant is generally used with the L suffix. For instance,

```
fseek(fp, 10L, SEEK_CUR);
```

moves the pointer forward by 10 characters from its current position, and

```
fseek(fp, -10L, SEEK_END);    Negative offset
```

sets the pointer 10 characters before EOF. You can also set the offset relative to the beginning of the file, so the following call,

```
fseek(fp, 100L, SEEK_SET);
```

positions the offset pointer to 100 bytes from the beginning of the file. You can't have a negative *offset* with *whence* set to `SEEK_SET`, but strangely enough, you can have a positive *offset* with *whence* at `SEEK_END`. In this case, the pointer moves beyond EOF, thus creating a *sparse* file—also called a file with a “hole”. Sparse files find use in database applications.

# ### 15.14.2 The `ftell` and `rewind` Functions

Prototype: `long ftell(FILE *stream);`
Return value: Current value of the offset pointer on success, -1 on failure.

The `ftell` function takes the file pointer as argument and returns the current position of the file position indicator, i.e., the offset pointer. The function is always used in conjunction with `fseek`, for instance, to determine the size of a file: