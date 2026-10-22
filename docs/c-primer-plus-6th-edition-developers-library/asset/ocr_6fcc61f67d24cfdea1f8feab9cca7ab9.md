| Prototype | Description |
|---|---|
| int printf(const char * restrict, ...); | Writes formatted output to the standard output |
| int putc(int, FILE *); | Writes the indicated character to the indicated output |
| int putchar(int); | Writes the indicated character to the standard output |
| int puts(const char *); | Writes the string to the standard output |
| int remove(const char *); | Removes the named file |
| int rename(const char *, const char *); | Renames the named file |
| void rewind(FILE *); | Sets the file-position pointer to the start of the file |
| int scanf(const char * restrict, ...); | Reads formatted input from the standard input |
| void setbuf(FILE * restrict, char * restrict); | Sets the buffer size and location |
| int setvbuf(FILE * restrict, char *restrict, int, size_t); | Sets the buffer size, location, and mode |
| int snprintf(char * restrict, size_t n, const char * restrict, ...); | Writes formatted output up to n characters to the indicated string |
| int sprintf(char * restrict, const char * restrict, ...); | Writes formatted output to the indicated string |
| int sscanf(const char *restrict, const char * restrict, ...); | Reads formatted input from the indicated string |
| FILE * tmpfile(void); | Creates a temporary file |
| char * tmpnam(char *); | Generates a unique name for a temporary file |
| int ungetc(int, FILE *); | Pushes the indicated character back onto the input stream |
| int vfprintf(FILE * restrict, const char * restrict, va_list); | Like fprintf(), except uses a single list-argument of type va_list, initialized by va_start, instead of a variable argument list |
| int vprintf(const char * restrict, va_list); | Like printf(), except uses a single list-argument of type va_list, initialized by va_start, instead of a variable argument list |