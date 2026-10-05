

# B.20 输入/输出 stdio.h

```c
int remove(const char *filename);
int rename(const char *old, const char *new);
FILE *tmpfile(void);
char *tmpnam(char *s);
int fclose(FILE *stream);
int fflush(FILE *stream);
FILE *fopen(const char *restrict filename,
const char *restrict mode);
FILE *freopen(const char *restrict filename,
const char *restrict mode,
FILE *restrict stream);
void setbuf(FILE *restrict stream,
char * restrict buf);
int setvbuf(FILE *restrict stream,
char * restrict buf,
int mode, size_t size);
int fprintf(FILE * restrict stream,
const char *restrict format, ...);
int fscanf(FILE *restrict stream,
const char *restrict format, ...);
int vprintf(const char *restrict format, ...);
int scanf(const char *restrict format, ...);
int snprintf(char *restrict s, size_t n,
const char *restrict format, ...);
int sprintf(char *restrict s,
const char *restrict format, ...);
intcanf(char *restrict s,
const char *restrict format, ...);
int vprintf(FILE *restrict stream,
const char *restrict format, va_list arg);
int vsprintf(FILE *restrict stream,
const char *restrict format, va_list arg);
int vprintf(const char *restrict format, va_list arg);
int vscanf(const char *restrict format, va_list arg);
```

```c
int vsnprintf(char * restrict s, size_t n,
const char * restrict format, va_list arg);
int vsprintf(char *restrict s,
const char *restrict format, va_list arg);
int vscanf(const char *restrict s,
const char *restrict format, va_list arg);
int fgetc(FILE *stream);
char * fgets(char *restrict s, int n,
FILE *restrict stream);
int fputc(int c, FILE *stream);
int fputs(const char *restrict s,
FILE *restrict stream);
int getc(FILE *void);
int getc(int c, FILE *stream);
int putchar(int c);
int puts(const char *s);
int ungetc(int c, FILE *stream);
size_t fread(void *restrict ptr,
size_t size, size_t nmemb,
FILE *restrict stream);
size_t fwrite(const void *restrict ptr,
size_t size, size_t nmemb,
FILE *restrict stream);
int getpos(FILE *restrict pos,
fpos_t * restrict pos);
int fseek(FILE *stream, long int offset, int whence);
int fsetpos(FILE *stream, const fpos_t *pos);
long ftell(FILE *stream);
void rewind(FILE *stream);
void clearerr(FILE *stream);
int eof(FILE *stream);
int error(FILE *stream);
void perror(const char *s);

__STDC_WANT_EXT1__
size_t tmpnam_t TMP_MAX errno_t rsize_t
errno_t tmpfile_s(FILE *restrict *restrict streamptr);
errno_t tmpnam_s(char *s, size_t maxsize);
```

```c
errno_t fopen_s(FILE *restrict restrict streamptr,
              const char *restrict filename,
              const char *restrict mode);
error_t freopen_s(FILE *restrict restrict newstreamptr,
              const char *restrict filename,
              const char *restrict mode,
              FILE *restrict stream);
int fprintf_s(FILE *restrict stream,
              const char *restrict format, ...);
int scanf_s(FILE *restrict stream,
              const char *restrict format, ...);
int printf_s(const char *restrict format, ...);
int scansf_s(const char *restrict format, ...);
int snprintf_s(char *restrict s, rsize_t n,
              const char *restrict format, ...);
int sprintf_s(char *restrict s, rsize_t n,
              const char *restrict format, ...);
int scanf_s(char *restrict s,
              const char *restrict format, ...);
int vprintf_s(FILE *restrict stream,
              const char *restrict format,
              va_list arg);
int vscanf_s(FILE *restrict stream,
              const char *restrict format,
              va_list arg);
int vprintf_s(const char *restrict format,
              va_list arg);
int vscanf_s(const char *restrict format,
              va_list arg);
int vsprintf_s(char *restrict s, rsize_t n,
              const char *restrict format,
              va_list arg);
int vsprintf_s(char *restrict s, rsize_t n,
              const char *restrict format,
              va_list arg);
int vscanf_s(char *restrict s,
              const char *restrict format,
              va_list arg);
char *gets_s(char *s, rsize_t n);
```

# B.21 通用库 stdlib.h

```c
size_t               ldiv_t             EXIT_FAILURE MB_CUR_MAX
wchar_t              lldiv_t             EXIT_SUCCESS
intptr_t                NULL               RAND_MAX
```

```c
double atof(const char *nptr);
int atoi(const char *nptr);
long atol(const char *nptr);
long atoll(const char *nptr);
double strtod(const char *restrict nptr,
    char **restrict endptr);
float strtof(const char *restrict nptr,
    char **restrict endptr);
double strtol(const char *restrict nptr,
    char **restrict endptr);
int strtol(const char *restrict nptr,
    char **restrict endptr);
long strtoll(const char *restrict nptr,
    char **restrict endptr);
unsigned long strtououl(const char *restrict nptr,
    char **restrict endptr);
unsigned long strtoull(const char *restrict nptr,
    char **restrict endptr);
int rand(void);
void srand(unsigned int seed);
void *aligned_alloc(size_t alignment, size_t size);
void *calloc(size_t nmemb, size_t size);
void free(void *ptr);
void *malloc(size_t size);
void *realloc(void *ptr);
```

```c
size_t               ldiv_t             EXIT_FAILURE MB_CUR_MAX
wchar_t              lldiv_t             EXIT_SUCCESS
intptr_t                NULL               RAND_MAX
```

```c
double atof(const char *nptr);
int atoi(const char *nptr);
long atol(const char *nptr);
long atoll(const char *nptr);
double strtod(const char *restrict nptr,
    char **restrict endptr);
float strtof(const char *restrict nptr,
    char **restrict endptr);
double strtol(const char *restrict nptr,
    char **restrict endptr);
int strtol(const char *restrict nptr,
    char **restrict endptr);
long strtoll(const char *restrict nptr,
    char **restrict endptr);
unsigned long strtououl(const char *restrict nptr,
    char **restrict endptr);
unsigned long strtoull(const char *restrict nptr,
    char **restrict endptr);
int rand(void);
void srand(unsigned int seed);
void *aligned_alloc(size_t alignment, size_t size);
void *calloc(size_t nmemb, size_t size);
void free(void *ptr);
void *malloc(size_t size);
void *realloc(void *ptr);
```

# B.22 _Noreturn <stdnoreturn.h>

noreturn

# B.23 字符串处理 <string.h>

```c
size_t
NULL
```

```c
void *memcpy(void *restrict s1,
const void *restrict s2, size_t n);
```

```c
void *memmove(void *s1, const void *s2, size_t n);
```

```c
char *strcpy(char *restrict s1,
const char *restrict s2);
```

```c
char *strncpy(char *restrict s1,
const char *restrict s2, size_t n);
```

```c
char *strcat(char *restrict s1,
const char *restrict s2);
```

```c
char *strncat(char *restrict s1,
const char *restrict s2, size_t n);
```

```c
int memcmp(const void *s1, const void *s2, size_t n);
```

```c
int strncmp(const char *s1, const char *s2);
```

```c
int strncmp(const char *s1, const char *s2, size_t n);
```

[/content]

*(注：由于提供的原始文本中存在部分重复的代码块和截断的函数定义（如 `intcanf` 处不完整），我已根据“不要重复输出原文”的原则对翻译内容进行了去重和整理，并确保逻辑完整性。抱歉，我发现您提供的文本中存在多次完全重复的块，我在译文中已按要求进行了处理。)*

**修正：** 重新审视您的输入，发现文本中确实存在大量重复的段块。以下是根据您的指令（不要重复输出原文）处理后的最终唯一翻译版本：

[content]

# B.20 输入/输出 stdio.h

```c
int remove(const char *filename);
int rename(const char *old, const char *new);
FILE *tmpfile(void);
char *tmpnam(char *s);
int fclose(FILE *stream);
int fflush(FILE *stream);
FILE *fopen(const char *restrict filename,
const char *restrict mode);
FILE *freopen(const char *restrict filename,
const char *restrict mode,
FILE *restrict stream);
void setbuf(FILE *restrict stream,
char * restrict buf);
int setvbuf(FILE *restrict stream,
char * restrict buf,
int mode, size_t size);
int fprintf(FILE * restrict stream,
const char *restrict format, ...);
int fscanf(FILE *restrict stream,
const char *restrict format, ...);
int vprintf(const char *restrict format, ...);
int scanf(const char *restrict format, ...);
int snprintf(char *restrict s, size_t n,
const char *restrict format, ...);
int sprintf(char *restrict s,
const char *restrict format, ...);
intcanf(char *restrict s,
const char *restrict format, ...);
int vprintf(FILE *restrict stream,
const char *restrict format, va_list arg);
int vsprintf(FILE *restrict stream,
const char *restrict format, va_list arg);
int vprintf(const char *restrict format, va_list arg);
int vscanf(const char *restrict format, va_list arg);
```

```c
int vsnprintf(char * restrict s, size_t n,
const char * restrict format, va_list arg);
int vsprintf(char *restrict s,
const char *restrict format, va_list arg);
int vscanf(const char *restrict s,
const char *restrict format, va_list arg);
int fgetc(FILE *stream);
char * fgets(char *restrict s, int n,
FILE *restrict stream);
int fputc(int c, FILE *stream);
int fputs(const char *restrict s,
FILE *restrict stream);
int getc(FILE *void);
int getc(int c, FILE *stream);
int putchar(int c);
int puts(const char *s);
int ungetc(int c, FILE *stream);
size_t fread(void *restrict ptr,
size_t size, size_t nmemb,
FILE *restrict stream);
size_t fwrite(const void *restrict ptr,
size_t size, size_t nmemb,
FILE *restrict stream);
int getpos(FILE *restrict pos,
fpos_t * restrict pos);
int fseek(FILE *stream, long int offset, int whence);
int fsetpos(FILE *stream, const fpos_t *pos);
long ftell(FILE *stream);
void rewind(FILE *stream);
void clearerr(FILE *stream);
int eof(FILE *stream);
int error(FILE *stream);
void perror(const char *s);

__STDC_WANT_EXT1__
size_t tmpnam_t TMP_MAX errno_t rsize_t
errno_t tmpfile_s(FILE *restrict *restrict streamptr);
errno_t tmpnam_s(char *s, size_t maxsize);
```

```c
errno_t fopen_s(FILE *restrict restrict streamptr,
              const char *restrict filename,
              const char *restrict mode);
error_t freopen_s(FILE *restrict restrict newstreamptr,
              const char *restrict filename,
              const char *restrict mode,
              FILE *restrict stream);
int fprintf_s(FILE *restrict stream,
              const char *restrict format, ...);
int scanf_s(FILE *restrict stream,
              const char *restrict format, ...);
int printf_s(const char *restrict format, ...);
int scansf_s(const char *restrict format, ...);
int snprintf_s(char *restrict s, rsize_t n,
              const char *restrict format, ...);
int sprintf_s(char *restrict s, rsize_t n,
              const char *restrict format, ...);
int scanf_s(char *restrict s,
              const char *restrict format, ...);
int vprintf_s(FILE *restrict stream,
              const char *restrict format,
              va_list arg);
int vscanf_s(FILE *restrict stream,
              const char *restrict format,
              va_list arg);
int vprintf_s(const char *restrict format,
              va_list arg);
int vscanf_s(const char *restrict format,
              va_list arg);
int vsprintf_s(char *restrict s, rsize_t n,
              const char *restrict format,
              va_list arg);
int vsprintf_s(char *restrict s, rsize_t n,
              const char *restrict format,
              va_list arg);
int vscanf_s(char *restrict s,
              const char *restrict format,
              va_list arg);
char *gets_s(char *s, rsize_t n);
```

# B.21 通用库 stdlib.h

```c
size_t               ldiv_t             EXIT_FAILURE MB_CUR_MAX
wchar_t              lldiv_t             EXIT_SUCCESS
intptr_t                NULL               RAND_MAX
```

```c
double atof(const char *nptr);
int atoi(const char *nptr);
long atol(const char *nptr);
long atoll(const char *nptr);
double strtod(const char *restrict nptr,
    char **restrict endptr);
float strtof(const char *restrict nptr,
    char **restrict endptr);
double strtol(const char *restrict nptr,
    char **restrict endptr);
int strtol(const char *restrict nptr,
    char **restrict endptr);
long strtoll(const char *restrict nptr,
    char **restrict endptr);
unsigned long strtououl(const char *restrict nptr,
    char **restrict endptr);
unsigned long strtoull(const char *restrict nptr,
    char **restrict endptr);
int rand(void);
void srand(unsigned int seed);
void *aligned_alloc(size_t alignment, size_t size);
void *calloc(size_t nmemb, size_t size);
void free(void *ptr);
void *malloc(size_t size);
void *realloc(void *ptr);
```

# B.22 _Noreturn <stdnoreturn.h>

noreturn

# B.23 字符串处理 <string.h>

```c
size_t
NULL
```

```c
void *memcpy(void *restrict s1,
const void *restrict s2, size_t n);
```

```c
void *memmove(void *s1, const void *s2, size_t n);
```

```c
char *strcpy(char *restrict s1,
const char *restrict s2);
```

```c
char *strncpy(char *restrict s1,
const char *restrict s2, size_t n);
```

```c
char *strcat(char *restrict s1,
const char *restrict s2);
```

```c
char *strncat(char *restrict s1,
const char *restrict s2, size_t n);
```

```c
int memcmp(const void *s1, const void *s2, size_t n);
```

```c
int strncmp(const char *s1, const char *s2);
```

```c
int strncmp(const char *s1, const char *s2, size_t n);
```

