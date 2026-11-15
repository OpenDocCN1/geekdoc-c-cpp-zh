double atof(const char *s);
int atoi(const char *s);
long int atol(const char *s);
double strtod(const char *s, char **endptr);
long int strtol(const char *s, char **endptr, int base);
unsigned long int strtoul(const char *s, char **endptr, int base);
converts the initial portion of the string pointed to by s to a numerical representation
void* bsearch(const void *key, const void *base, size_t n, size_t size, int(*compar)(const void *, const void *));
searches an array of n objects searching for the value pointed to by key
void* calloc(size_t n, size_t size);
allocates space for an array of n objects, each of size size
div_t div(int numer, int denom);
ldiv_t ldiv(long int numer, long int denom);
computes the quotient and remainder of the division of numer by denom
void exit(int status);
causes normal program termination to occur
void free(void *ptr);
deallocates the space pointed to by ptr
void* malloc(size_t size);
allocates space for an object of size size
void qsort(void *base, size_t nmemb, size_t size, int(*compar)(const void *, const void *));
sorts an object of n objects into ascending order
int rand(void);
returns a pseudorandom integer in the range of 0 to RAND_MAX
void* realloc(void *ptr, size_t size);
changes the size of the object pointed to by ptr
void srand(unsigned int seed);
uses the seed to initialize a new sequence of values from the RAND function

# <cstring>

The header file <cstring> defines the type size_t, which is an unsigned integer, and the macro NULL, which has the value binary zero. In addition, the header file defines a number of functions for handling strings.

void* memchr(const void *s, int c, size_t n);
returns a pointer to the first occurrence of c in the initial n characters of the object pointed to by s
int memcmp(const void *s1, const void *s2, size_t n);
returns an integer greater than, equal to, or less than zero, accordingly, as the string pointed to by s is greater than, equal to, or less than the string pointed to by t