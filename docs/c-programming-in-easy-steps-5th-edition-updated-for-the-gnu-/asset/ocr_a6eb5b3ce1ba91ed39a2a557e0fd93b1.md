```
int getchar( void )
```

The getchar() function is equivalent to getc( stdin )

```
char *gets( char *s )
```

Reads the next input line into an array, replacing its final newline character with a \0 null character. It returns s, or NULL if at the end of the file or if an error occurs

```
int putc( int c , FILE *stream )
```

The putc() function is the macro equivalent of fputc()

int putchar( int c ) is equivalent to putc( c , stdout )

```
int puts( const char *s )
```

Writes the string s and a newline character to stdout. It returns a non-negative value, or EOF if an error occurs

```
int ungetc( int c , FILE *stream )
```

Pushes the character c back onto the specified stream where it is returned on the next read. Only one pushback character per stream is guaranteed and EOF cannot be pushed back. This function returns the character pushed back, or EOF if an error occurs

# <stdio.h>

# Functions for direct stream input and output

The fread() and fwrite() functions contained in the stdio.h header file are most effective to read and write entire text files:

```
size_t fread( void *ptr , size_t size , size_t nobj , FILE *stream )
```

The fread() function reads from the specified stream into the specified ptr array pointer at most nobj objects of size size. This function returns the number of objects it has read, which may be less than the number requested in the function call.

The status of fread() can be tested as it proceeds using the feof() function and ferror() functions — see the error functions listed here

```
size_t fwrite(const void *ptr, size_t size, size_t nobj, FILE *stream )
```

The fwrite() function writes from the specified ptr pointer nobj objects of size size. It returns the number of objects that it has written. If an error occurs, the returned value will be less than that requested by nobj in the function call

Many of the standard functions in the C library set status indicators when an error occurs, or when the end of a file is reached. These indicators can be tested using the error functions listed in the table below. Also, the integer expression