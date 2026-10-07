# B.21 General utilities <stdlib.h>

```
size_t               EXIT_FAILURE MB_CUR_MAX
wchar_t             llldiv_t      EXIT_SUCCESS
div_t               NULL         RAND_MAX

double atof(const char *nptr);
int atoi(const char *nptr);
long int atol(const char *nptr);
long long int atoll(const char *nptr);
double strtod(const char * restrict nptr,
char ** restrict endptr);
float strtof(const char * restrict nptr,
char ** restrict endptr);
long double strtold(const char * restrict nptr,
char ** restrict endptr);
long int strtol(const char * restrict nptr,
char ** restrict endptr, int base);
long int strtol(const char * restrict nptr,
char ** restrict endptr, int base);
unigned long int stroul(
const char * restrict nptr,
char ** restrict endptr, int base);
unigned long int strtull(
const char * restrict nptr,
char ** restrict endptr, int base);
int rand(unsigned int seed);
void *aligned_alloc(size_t alignment, size_t size);
void *calloc(size_t nmemb, size_t size);
void free(void *ptr);
void *malloc(size_t size);
void *realloc(void *ptr, size_t size);
_Noreturn abort(void);
intatexit(void *func)(void));
int at_quick_exit(void *func)(void));
_Noreturn exit(int status);
_Noreturn _Exit(int status);
char *getenv(const char *name);
_Noreturn quick_exit(int status);
int system(const char *string);
```