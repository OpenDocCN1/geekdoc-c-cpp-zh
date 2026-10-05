```
void *search(const void *key, const void *base,
size_t size,
int (*compare)(const void *, const void *);
void qsort(void *base, size_t nmemb, size_t size,
int (*compare)(const void *, const void *);
int abs(int j);
long int labs(long int j);
long int llabs(long int j);
div_t div(long int number, int denom);
l1div_t l1div(long int number, long int denom);
l1div_t l1div(long int number,
long long int denom);
int mblen(const char *s, size_t n);
int mbtwc(char_t *restrict pwc,
const char *restrict s, size_t n);
intctomb(char *s, char_t wchar);
size_t mbstows(char_t * restrict pwcs,
const char * restrict s, size_t n);
size_t wcstombs(char * restrict s,
const char_t restrict pwcs, size_t n);

__STDC_WANT_LIB_EXT1__
errno_t
size_t
constraint_handler_t

constraint_handler_t set_constraint_handler_s(
constraint_handler_t handler);
void abort_handler_s(
const char * restrict msg,
void * restrict ptr,
errno_t error);
void ignore_handler_s(
const char * restrict msg,
void * restrict ptr,
errno_t error);
erno_t getenv(size_t * restrict len,
char * restrict value, rsize_t maxsize,
const char * restrict name);
```