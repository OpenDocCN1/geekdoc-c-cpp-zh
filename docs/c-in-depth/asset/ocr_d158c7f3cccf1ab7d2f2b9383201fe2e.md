| Base mode | Meaning |
|---|---|
| S_IREAD | Read |
| S_IWRITE | Write |
| S_READ / S_IWRITE | Read / Write |

# 18.4.30 stat()

**Declaration:** int stat( char *fname, struct stat *finfo );

**Header file:** sys\stat.h

This function is used for filling the file information in structure finfo. The structure of finfo is same as stat which is defined in sys\stat.h.

# 18.4.31 sprintf()

**Declaration:** int sprintf( char *str, const char *controlstring [, arg1, arg2, .........] );

**Header file:** stdio.h

This function is same as printf( ) function except that instead of sending the formatted output to the screen, it stores the formatted output in a string . This function returns the number of characters output to the string excluding the null character and on failure it returns EOF.

# 18.4.32 sscanf()

**Declaration:** int sscanf( const char *str, const char *controlstring [, address1, address2,.....] );

**Header file:** stdio.h

This function is same as the scanf( ) function except that data is read from a string rather than the standard input. We can read the formatted text from a string and convert it into variables of different data types.

# 18.4.33 tell()

**Declaration:** long tell( int fd )

**Header file:** io.h

This is same as ftell(). It is used for getting the current file pointer position.

# 18.4.34 tmpfile()

**Declaration:** FILE *tmpfile( void )

**Header file:** stdio.h

tmpfile() creates a temporary binary file and opens it in update mode(wb+). On success it returns a pointer of type FILE that points to the temporary file and on error it returns NULL. The file created by tmpfile() is temporary because it is automatically deleted when closed or when the program terminates.

# 18.4.35 tmpnam()

char *tmpnam( char *arr )

**Header file:** stdio.h

This function is used for generating a unique file name. The number of different file names that