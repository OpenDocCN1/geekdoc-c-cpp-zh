```
errno_t fopen_s(FILE * restrict restrict streamptr,
              const char * restrict filename,
              const char * restrict mode);
error_t freopen_s(FILE * restrict restrict newstreamptr,
              const char * restrict filename,
              const char * restrict mode,
              FILE * restrict stream);
int fprintf_s(FILE * restrict stream,
              const char * restrict format, ...);
int scanf_s(FILE * restrict stream,
              const char * restrict format, ...);
int printf_s(const char * restrict format, ...);
int scansf_s(const char * restrict format, ...);
int snprintf_s(char * restrict s, rsize_t n,
              const char * restrict format, ...);
int sprintf_s(char * restrict s, rsize_t n,
              const char * restrict format, ...);
int scanf_s(const char * restrict s,
              const char * restrict format, ...);
intprintf_s(FILE * restrict stream,
              const char * restrict format,
              va_list arg);
int vscanf_s(FILE * restrict stream,
              const char * restrict format,
              va_list arg);
int vprintf_s(const char * restrict format,
              va_list arg);
int vscanf_s(const char * restrict format,
              va_list arg);
int vsprintf_s(char * restrict s, rsize_t n,
              const char * restrict format,
              va_list arg);
int vsprintf_s(char * restrict s, rsize_t n,
              const char * restrict format,
              va_list arg);
int vscanf_s(const char * restrict s,
              const char * restrict format,
              va_list arg);
char *gets_s(char *s, rsize_t n);
```