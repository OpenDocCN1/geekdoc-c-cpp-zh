
## ASCII character codes

ASCII (American Standard Code for Information Interchange) is the standard representation of characters by numerical code. The non-printing character codes, originally developed for teletypes, are now rarely used for their intended original purpose.

There are also extended ASCII code sets from 128-255 (not listed) containing accented characters and symbols, but these sets do vary.

Note that the character represented by character code 32 is not missing – it is, in fact, the non-printing space character. Also, the character represented by character code 127 is the delete character.

| Code: | Char: | Description: |
|---|---|---|
| 0 | NUL | null |
| 1 | SOH | start of heading |
| 2 | STX | start of text |
| 3 | ETX | end of text |
| 4 | EOT | end of transmission |
| 5 | ENQ | enquiry |
| 6 | ACK | acknowledgement |
| 7 | BEL | bell |
| 8 | BS | backspace |
| 9 | TAB | horizontal tab |
| 10 | NL | newline |
| 11 | VT | vertical tab |
| 12 | FF | form feed |
| 13 | CR | carriage return |

| Code | Char | Description |
|---|---|---|
| 14 | SO | shift out |
| 15 | SI | shift in |
| 16 | DLE | data link escape |
| 17 | DC1 | device control 1 |
| 18 | DC2 | device control 2 |
| 19 | DC3 | device control 3 |
| 20 | DC4 | device control 4 |
| 21 | NAK | neg. acknowledge |
| 22 | SYN | synchronous file |
| 23 | ETB | end of trans. block |
| 24 | CAN | cancel |
| 25 | EM | end of medium |
| 26 | SUB | substitute |
| 27 | ESC | escape |
| 28 | FS | file separator |
| 29 | GS | group separator |
| 30 | RS | record separator |
| 31 | US | unit separator |

| Code | Char |
|---|---|
| 32 | ! |
| 33 | " |
| 34 | " |
| 35 | # |
| 36 | $ |
| 37 | % |

| Code | Char |
|---|---|
| 38 | & |
| 39 | ' |
| 40 | ( |
| 41 | ) |
| 42 | * |
| 43 | + |
| 44 | , |
| 45 | - |
| 46 | . |
| 47 | / |
| 48 | 0 |
| 49 | 1 |
| 50 | 2 |
| 51 | 3 |
| 52 | 4 |
| 53 | 5 |
| 54 | 6 |
| 55 | 7 |
| 56 | 8 |
| 57 | 9 |
| 58 | : |
| 59 | ; |
| 60 | < |
| 61 | = |
| 62 | > |
| 63 | ? |

| Code | Char |
|---|---|
| 64 | @ |
| 65 | A |
| 66 | B |
| 67 | C |
| 68 | D |
| 69 | E |
| 70 | F |
| 71 | G |
| 72 | H |
| 73 | I |
| 74 | J |
| 75 | K |
| 76 | L |
| 77 | M |
| 78 | N |
| 79 | O |
| 80 | P |
| 81 | Q |
| 82 | R |
| 83 | S |
| 84 | T |
| 85 | U |
| 86 | V |
| 87 | W |
| 88 | X |

| Code | Char |
|---|---|
| 89 | Y |
| 90 | Z |
| 91 | [ |
| 92 | \ |
| 93 | ] |
| 94 | ^ |
| 95 | _ |
| 96 | ` |
| 97 | a |
| 98 | b |
| 99 | c |
| 100 | d |
| 101 | e |
| 102 | f |
| 103 | g |
| 104 | h |
| 105 | i |
| 106 | j |
| 107 | k |
| 108 | l |
| 109 | m |
| 110 | n |
| 111 | o |
| 112 | p |
| 113 | q |
| 114 | r |

| Code | Char |
|---|---|
| 115 | s |
| 116 | t |
| 117 | u |
| 118 | v |
| 119 | w |
| 120 | x |
| 121 | y |
| 122 | z |
| 123 | { |
| 124 | \| |
| 125 | } |
| 126 | ~ |
| 127 | del |

![](img/db19f3858a1e321646bf2590afd29547_242_0.png)

To find out more about extended ASCII sets try the website at asciitable.com, or search for "ASCII" online.

![](img/db19f3858a1e321646bf2590afd29547_242_1.png)

The term "ASCII file" just means a plain text file, such as those produced by Windows’ Notepad application.

## Input & output functions

The functions and types defined in the stdio.h header file represent almost one third of the C language library. It is used to introduce data into a program and generate output from a program.

A “stream” is a data source terminated by a newline character. It may be read or written by “opening” the stream, and terminated by “closing” it. Opening a stream returns a FILE type pointer in which information needed to control the stream is stored.

### File-handling functions

FILE fopen(const char *filename, const char *mode)

The fopen() function returns a FILE pointer, or NULL if the file cannot be opened. Any of the following modes may be specified in the function call:

- r open a text file for reading only
- w create a text file to write to, and discard any previous contents
- a append – open or create a text file for writing at the end of the file
- r+ open a text file to update (read and write)
- w+ open a text file to update (read and write, discarding any previous contents)
- a+ append – open or create a text file for update, for writing at the end of the file

If the file being opened is a binary file, a b should be added after the file mode – for example, `wb+`

FILE freopen(const char *filename, const char *mode , FILE *stream )

The freopen() function opens a file with the specified mode and associates the stream with it. It returns the stream, or NULL if an error occurs. This function is normally used to change the files associated with stdin, stdout or stderr

int fflush( FILE *stream )

On an output stream this function causes any buffered data to be written immediately. It returns the EOF constant for a write error, or zero otherwise. A call to fflush( NULL ) flushes all output streams

## <stdio.h>

```
int fclose( FILE *stream )
```

A call to fclose() flushes any unwritten data from the stream then closes the stream. It returns the EOF constant if an error occurs, or zero otherwise

```
int remove( const char *filename )
```

This function removes the specified file – so that any subsequent attempt to open that file will fail. It returns a non-zero value if it cannot remove the file

```
int rename( const char *old-name , const char *new-name )
```

The rename() function changes the name of the specified file, or it returns a non-zero value if it cannot rename the file

```
FILE *tmpfile( void )
```

Calling tmpfile() creates a temporary file, with the file mode of wb+, that is removed when the program ends. This function returns a stream, or NULL if the file cannot be created

```
char *tmpnam( char arr[ L_tmpnam ] )
```

This function stores a string in an array and returns a unique valid name pointer to that array. The arr array must have at least L_tmpnam characters. The tmpnam() function generates a different name each time it is called

```
int setvbuf( FILE *stream , char *buffer , int mode , size_t size )
```

A call to setvbuf() sets buffering for the specified stream. It should be called after a stream has been opened but before any operation has been performed on it. Valid modes are _IOFBF to cause full buffering, _IOLBF for line buffering, and _IONBF for no buffering. The size sets the buffer size. This function returns a non-zero value if an error occurs

```
void setbuf( FILE *stream , char *buffer )
```

The setbuf() function defines how a stream should be buffered. It should be called after a stream has been opened but before any operation has been performed on it. The argument buffer points to an array to be used as the buffer

## <stdio.h>

## Functions that format output

```
int printf( FILE *stream, const char *format, ... )
```

The printf function converts and writes output to a specified filestream under the control of a format specifier. It returns the number of characters written, or a negative value if an error occurs

```
int printf( const char *format, ... )
```

The printf() function writes and converts output to stdout. It is equivalent to fprintf(stdout, const char *format)

```
int sprintf( char *s, const char *format, ... )
```

The sprintf() function is the same as printf() except the output is written into the specified string, and terminated with a 0 null character

```
vprintf( const char *format, va_list arg )
```

```
vfprintf( FILE *stream, const char *format, va_list arg )
```

```
vsprintf( char *s, const char *format, va_list arg )
```

These three functions are equivalent to the corresponding printf() functions except that their variable argument list is replaced by an argument of the va_list type. Refer to the stdarg.h header file functions here for more details

## Functions that format input

```
int fscanf( FILE *stream, const char *format, ... )
```

The fscanf() function reads from a specified stream under the control of a format specifier and assigns converted values to subsequent arguments. It returns the number of input items converted or the EOF constant if the end of the file is met, or if an error occurs

```
int scanf( const char *format, ... )
```

The scanf() function reads and converts input to stdin. It is equivalent to fscanf(stdin, const char *format)

```
int sscanf( char *s, const char *format, ... )
```

The sscanf() function is the same as scanf() except the input is read from the specified string

## Format specifiers for output

```
<stdio.h>
```
