To control this, the Random Access functions allow control over the implied read/write position in the file. The file position indicator is moved without the need for a read or a write, and indicates the byte to be the subject of the next operation on the file.

Three types of function exist which allow the file position indicator to be examined or changed. Their declarations and descriptions follow. #include <stdio.h>

```
/* return file position indicator */
long ftell(FILE *stream);
int fgetpos(FILE *stream, fpos_t *pos);
```

```
/* set file position indicator to zero */
void rewind(FILE *stream);
```

```
/* set file position indicator */
int fseek(FILE *stream, long offset, int ptrname);
int fsetpos(FILE *stream, const fpos_t *pos);
```

**ftell** returns the current value (measured in characters) of the file position indicator if stream refers to a binary file. For a text file, a ‘magic’ number is returned, which may only be used on a subsequent call to **fseek** to reposition to the current file position indicator. On failure, -1L is returned and **errno** is set.

**rewind** sets the current file position indicator to the start of the file indicated by stream. The file's error indicator is reset by a call of rewind. No value is returned.