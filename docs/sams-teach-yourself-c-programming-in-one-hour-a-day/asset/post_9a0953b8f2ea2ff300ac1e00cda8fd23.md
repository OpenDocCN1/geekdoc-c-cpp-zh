
# Common C Functions

| Function | Header File | Function Prototype |
| --- | --- | --- |
| fseek* | stdio.h | int fseek(FILE *, long, int); |
| fsetpos* | stdio.h | int fsetpos(FILE *, const fpos_t *); |
| ftell* | stdio.h | long ftell(FILE *); |
| fwrite* | stdio.h | size_t fwrite(const void *, size_t, size_t, FILE *); |
| getc* | stdio.h | int getc(FILE *); |
| getch* | stdio.h | int getch(void); |
| getchar* | stdio.h | int getchar(void); |
| getche* | stdio.h | int getche(void); |
| getenv* | stdlib.h | char *getenv(const char *); |
| gets* | stdio.h | char *gets(char *); |
| gmtime* | time.h | struct tm *gmtime(const time_t *); |
| isalnum* | ctype.h | int isalnum(int); |
| isalpha* | ctype.h | int isalpha(int); |
| isascii* | ctype.h | int isascii(int); |
| iscntrl* | ctype.h | int iscntrl(int); |
| isdigit* | ctype.h | int isdigit(int); |
| isgraph* | ctype.h | int isgraph(int); |
| islower* | ctype.h | int islower(int); |
| isprint* | ctype.h | int isprint(int); |
| ispunct* | ctype.h | int ispunct(int); |
| isspace* | ctype.h | int isspace(int); |
| isupper* | ctype.h | int isupper(int); |
| isxdigit* | ctype.h | int isxdigit(int); |
| labs | stdlib.h | long int labs(long int); |
| ldexp | math.h | double ldexp(double, int); |
| ldiv | stdlib.h | long int ldiv(long int, long int); |
| localtime* | time.h | struct tm *localtime(const time_t *); |
| log* | math.h | double log(double); |
| log10* | math.h | double log10(double); |
| malloc* | stdlib.h | void *malloc(size_t); |
| mblen | stdlib.h | int mblen(const char *, size_t); |
| mbstowcs* | stdlib.h | size_t mbstowcs(wchar_t *, const char *, size_t); |
| mbtowc* | stdio.h | int mbtowc(wchar_t *, const char *, size_t); |

# APPENDIX C

| Function | Header File | Function Prototype |
| --- | --- | --- |
| memchr | string.h | void *memchr(const void *, int, size_t); |
| memcmp | string.h | int memcmp(const void *, const void *, size_t); |
| memcpy | string.h | void *memcpy(void *, const void *, size_t); |
| memmove | string.h | void *memmove(void *, const void *, size_t); |
| memset | string.h | void *memset(void *, int, size_t); |
| mktime* | time.h | time_t mktime(struct tm *); |
| modf | math.h | double modf(double, double *); |
| perror* | stdio.h | void perror(const char *); |
| pow* | math.h | double pow(double, double); |
| printf* | stdio.h | int printf(const char *, ...); |
| putc* | stdio.h | int putc(int, FILE *); |
| putchar* | stdio.h | int putchar(int); |
| puts* | stdio.h | int puts(const char *); |
| qsort* | stdlib.h | void qsort(void*, size_t, size_t, int (*)(const void *, const void *)); |
| rand | stdlib.h | int rand(void); |
| realloc* | stdlib.h | void *realloc(void *, size_t); |
| remove* | stdio.h | int remove(const char *); |
| rename* | stdio.h | int rename(const char *, const char *); |
| rewind* | stdio.h | void rewind(FILE *); |
| scanf* | stdio.h | int scanf(const char *, ...); |
| setbuf | stdio.h | void setbuf(FILE *, char *); |
| setvbuf* | stdio.h | int setvbuf(FILE *, char *, int, size_t); |
| sin* | math.h | double sin(double); |
| sinh* | math.h | double sinh(double); |
| sleep* | time.h | unsigned int sleep(unsigned int); |
| sprintf* | stdio.h | int sprintf(char *, const char *, ...); |
| sqrt* | math.h | double sqrt(double); |
| srand | stdlib.h | void srand(unsigned int); |
| strcat* | string.h | char *strcat(char *, const char *); |
| strchr* | string.h | char *strchr(const char *, int); |
| strcmp* | string.h | int strcmp(const char *, const char *); |

# Common C Functions

| Function | Header File | Function Prototype |
| --- | --- | --- |
| strcmp | string.h | int strcmp(const char *, const char *); |
| strcpy | string.h | char *strcpy(char *, const char *); |
| strncpy | string.h | char *strncpy(char *, const char *, size_t); |
| strdup | string.h | char *strdup(const char *); |
| strerror | string.h | char *strerror(int); |
| strftime | time.h | size_t strftime(char *, size_t, const char *, const struct tm *); |
| strlen | string.h | size_t strlen(const char *); |
| strlwr | string.h | char *strlwr(char *); |
| strncat | string.h | char *strncat(char *, const char *, size_t); |
| strncmp | string.h | int strncmp(const char *, const char *, size_t); |
| strncpy | string.h | char *strncpy(char *, const char *, size_t); |
| strnset | string.h | char *strnset(char *, int, size_t); |
| strpbrk | string.h | char *strpbrk(const char *, const char *); |
| strchr | string.h | char *strchr(const char *, int); |
| strspn | string.h | size_t strspn(const char *, const char *); |
| strstr | string.h | char *strstr(const char *, const char *); |
| strtod | stdlib.h | double strtod(const char *, char **); |
| strtok | string.h | char *strtok(char *, const char *); |
| strtol | stdlib.h | long strtol(const char *, char **, int); |
| strtoul | stdlib.h | unsigned long strtoul(const char *, char **, int); |
| strupr | string.h | char *strupr(char *); |
| system | stdlib.h | int system(const char *); |
| tan | math.h | double tan(double); |
| tanh | math.h | double tanh(double); |
| time | time.h | time_t time(time_t *); |
| tmpfile | stdio.h | FILE *tmpfile(void); |
| tmpnam | stdio.h | char *tmpnam(char *); |
| tolower | ctype.h | int tolower(int); |
| toupper | ctype.h | int toupper(int); |

# APPENDIX C

| Function | Header File | Function Prototype |
| --- | --- | --- |
| ungetc* | stdio.h | int ungetc(int, FILE *); |
| va_arg* | stdarg.h | type va_arg(va_list, type); |
| va_end* | stdarg.h | void va_end(va_list); |
| va_start* | stdarg.h | void va_start(va_list, lastarg); |
| vprintf | stdio.h | int vprintf(const char *, va_list); |
| vsprintf | stdio.h | int vsprintf(char *, const char *, va_list); |
| wcstombs | stdlib.h | size_t wcstombs(char *, const wchar_t *, size_t); |
| wctomb | stdlib.h | int wctomb(char *, wchar_t); |

# APPENDIX D

# Answers

## Answers for Lesson 1

### Quiz

- 1. C is powerful, popular, and portable.
- 2. The compiler translates source code into machine-language instructions that your computer can understand.
- 3. Editing, compiling, linking, and testing.
- 4. The answer to this question depends on your compiler. Consult your compiler's manuals.
- 5. The answer to this question depends on your compiler. Consult your compiler's manuals.
- 6. The appropriate extension for C source files is .C (or .c).
  Note: C++ uses the extension .CPP. You can write and compile your C programs with a .CPP extension, but it's more appropriate to use a .c extension.
- 7. FILENAME.TXT would compile. However, it's more appropriate to use a .c extension.
- 8. You should make changes to the source code to correct the problems. You should recompile and relink. After relinking, you should run the program again to see whether your corrections fixed the program.
- 9. Machine language is made up of digital or binary instructions that the computer can understand. Because the computer can't understand C source code, a compiler translates source code to machine code, also object code.
- 10. The linker combines the object code from your program with the object code from the function library and creates an executable file.

# Exercises

- 1. When you look at the object file, you see many unusual characters and other gibberish. Mixed in the gibberish, you also see pieces of the source file.

- 2. This program calculates the area of a circle. It prompts the user for the radius and then displays the area.

- 3. This program generates a 10x10 block made of the character x. A similar program is covered in Lesson 6, "Basic Program Control."

- 4. This program generates a compiler error. You should get a message similar to the following:

```
Error: chlex4.c: Declaration terminated incorrectly
```

This error is caused by the semicolon at the end of line 3. If you remove the semicolon, this program should compile and link correctly.

- 5. This program compiles okay, but it is a linker error. You should get a message similar to the following:
Error: Undefined symbol _do_it in module...

This error occurs because the linker can't find a function called do_it. To fix this program, change do_it to printf.

- 6. Rather than printing a 10x10 block filled with the character x, the program prints a 10x10 block of smiley faces.

## Answers for Lesson 2

### Quiz

- 1. A block.

- 2. The main() function.

- 3. You use program comments to make notations about the program's structure and operation. Any text between /* and */ is a program comment and is ignored by the compiler. In addition, you can use single-line comments. Any text on the same line following forward slashes // is considered a comment.

- 4. A function is an independent section of program code that performs a certain task and has been assigned a name. By using a function's name, a program can execute the code in the function.

- 5. A user-defined function is created by the programmer. A library function is supplied with the C compiler.
