
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

`noreturn`

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
