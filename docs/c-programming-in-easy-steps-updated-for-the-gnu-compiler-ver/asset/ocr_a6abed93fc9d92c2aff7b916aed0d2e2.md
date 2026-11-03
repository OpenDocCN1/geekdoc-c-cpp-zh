# Error functions

Many of the standard functions in the C library set status indicators when an error occurs, or when the end of a file is reached. These indicators can be tested using the error functions listed in the table below. Also, the integer expression errno, defined in the errno.h header file, may contain an error code giving more information about the most recent error.

```
void clearerr( FILE *stream )
```

The clearerr() function clears the end of file and error indicators for the specified stream

```
int feof( FILE *stream )
```

The feof() function returns a non-zero value if the end of file indicator is set for the specified stream

```
int ferror( FILE *stream )
```

The ferror() function returns a non-zero value if the error indicator is set for the specified stream

```
void perror( const char *s )
```

The perror() function prints an implementation-defined error message associated with the integer value contained in the errno expression. See also the strerror() function in the string.h header file