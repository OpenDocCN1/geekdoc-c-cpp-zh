© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

```
int vsprintf(char * restrict s, size_t n,
const char * restrict format, va_list arg);
int vsprintf(char * restrict s,
const char * restrict format, va_list arg);
int vscanf(const char * restrict s,
const char * restrict format, va_list arg);
int fgetc(FILE *stream)
char * restrict s, int n,
FILE *restrict stream);
int fput(int c, FILE *stream);
 fputs(const char * restrict s,
FILE *restrict stream);
int getc(FILE *stream);
int getchar(int c, FILE *stream);
int putchar(int c);
int puts(const char *s);
int ungetc(int c, FILE *stream);
size_t fread(void * restrict ptr,
size_t size, size_t nemb,
FILE *restrict stream);
size_t fwrite(const void * restrict ptr,
size_t size, size_t nemb,
FILE *restrict stream);
int fgetpos(FILE * restrict stream,
fpos_t * restrict pos);
int fseek(FILE *stream, long offset, int whence);
int fsetpos(FILE *stream, const fpos_t *pos);
long int ftell(FILE *stream);
void rewind(FILE *stream);
void clearerr(FILE *stream);
int eof(FILE *stream);
int error(FILE *stream);
void perror(const char *s);
```

+   - STDC_WANT_LIB_EXT1_
L_tmpnam_s TMP_MAX_S errno_t rsize_t
nerno_t tmpfile_s(FILE * restrict restrict streamptr)
nerno_t tmpnam_s(char *s, size_t maxsize);

§B.20 Library summary 489
Copyright International Organization for Standardization\Provided by IHS under license with ISO
No reproduction or redistribution permitted without license from IHS Not for Resale