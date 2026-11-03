| Constant | Value | Position |
|---|---|---|
| SEEK_SET | 0 | Beginning of file |
| SEEK_CURRENT | 1 | Current position |
| SEEK_END | 2 | End of file |

# 18.4.21 fstat()

**Declaration:** int fstat( int fd, struct stat *finfo );

**Header file:** sys/stat.h

This function is used for filling the file information in structure finfo. The structure of finfo is same as stat which is defined in sys/stat.h.

# 18.4.22 ftell()

**Declaration:** int fputs( FILE *stream );

**Header file:** stdio.h

This function returns the current position of the file position pointer. The value is counted from the beginning of the file.

# 18.4.23 isatty()

**Declaration:** int isatty( int handle );

**Header file:** io.h

This function is used for checking whether the handle is associated with character device or not. The character device may be a terminal, console, printer or serial port. It returns nonzero on success, otherwise it returns zero.

# 18.4.24 open()

**Declaration:** int open( const char *fname, int access, unsigned mode );

**Header file:** io.h

This function is used for opening a file. The access is the base mode with modifier. modifier is taken by applying OR operator with base mode.

| Base mode | Meaning |
|---|---|
| O_WRONLY | write only |
| O_RDONLY | read only |
| O_RDWR | read / write |

| Modifiers | Meaning |
|---|---|
| O_APPEND | For appending |
| O_BINARY | binary file |
| O_CREAT | creates the file, if the file doesn't exist and sets the attribute with mode |