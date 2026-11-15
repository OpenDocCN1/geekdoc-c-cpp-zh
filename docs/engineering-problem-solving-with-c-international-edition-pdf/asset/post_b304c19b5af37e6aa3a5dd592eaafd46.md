
- `double log(double x);` computes ln x, the natural logarithm of x to the base e; errors occur if x <= 0
- `double log10(double x);` computes log10 x, the common logarithm of x to the base 10; errors occur if x <= 0
- `double pow(double x, double y);` computes the value of x to the y power, or x^y; errors occur if x = 0 and y <= 0, or if x < 0 and y is not an integer
- `double sin(double x);` computes the sine of x, where x is in radians
- `double sinh(double x);` computes the hyperbolic sine of x, which is equal to (e^x - e^-x)/2
- `double sqrt(double x);` computes the square root of x where x >= 0
- `double tan(double x);` computes the tangent of x, where x is in radians
- `double tanh(double x);` computes the hyperbolic tangent of x, which is equal to sinh x / cosh x

The header file `<cstdlib>` defines types, macros, and functions that did not fit in any of the other header files. The types `div_t` and `ldiv_t` are structures for storing a quotient and a remainder. The macros are the following:

- NULL
- an integer value of binary zero
- EXIT_FAILURE
- EXIT_SUCCESS
- integral expressions used to return unsuccessful or successful termination status, respectively, to the host
- RAND_MAX
- an integral expression that is the maximum value returned by the RAND function
- MB_CUR_MAX
- a positive integer expression whose value is the maximum number of bytes in a multibyte character

The functions that are most likely to be used in engineering application are as follows, with the function prototype statement and a brief description:

- `void abort(void);` causes an abnormal program termination of the program
- `int abs(int k);`
- `long int labs(long int k);` computes the absolute value of the integer k
- `int atexit(void (*func)(void));` registers the function pointed to by func to be called without arguments at normal program termination
- `double atof(const char *s);`
- `int atoi(const char *s);`
- `long int atol(const char *s);`
- `double strtod(const char *s, char **endptr);`
- `long int strtol(const char *s, char **endptr, int base);`
- `unsigned long int strtoul(const char *s, char **endptr, int base);`
  converts the initial portion of the string pointed to by s to a numerical representation
- `void* bsearch(const void *key, const void *base, size_t n, int (*compar)(const void *, const void *));`
  searches an array of n objects searching for the value pointed to by key
- `void* calloc(size_t n, size_t size);`
  allocates space for an array of n objects, each of size size
- `div_t div(int numerator, int denom);`
- `ldiv_t ldiv(long int numer, long int denom);`
  computes the quotient and remainder of the division of numer by denom
- `void exit(int status);`
  causes normal program termination to occur
- `void free(void *ptr);`
  deallocates the space pointed to by ptr
- `void* malloc(size_t size);`
  allocates space for an object of size size
- `void* qsort(void *base, size_t nmemb, size_t size, int (*compar)(const void *, const void *));`
  sorts an object of n objects into ascending order
- `int rand(void);`
  returns a pseudorandom integer in the range of 0 to RAND_MAX
- `void* realloc(void *ptr, size_t size);`
  changes the size of the object pointed to by ptr
- `void srand(unsigned int seed);`
  uses the seed to initialize a new sequence of values from the RAND function

## <cstring>

The header file <cstring> defines the type size_t, which is an unsigned integer, and the macro NULL, which has the value of binary zero. In addition, the header file defines a number of functions for handling strings.

- `void* memchr(const void *s, int c, size_t n);`
  returns a pointer to the first occurrence of c in the initial n characters of the object pointed to by s
- `int memcmp(const void *s1, const void *s2, size_t n);`
  returns an integer greater than, equal to, or less than zero, accordingly, as the string pointed to by s1 is greater than, equal to, or less than the string pointed to by t
- `void* memcpy(void *s, const void *t, size_t n);` copies n characters from the object pointed to by t into the object pointed to by s
- `void* memmove(void *s, const void *t, size_t n);` copies n characters from the object pointed to by t into the object pointed to by s, using a temporary area
- `void* memset(void *s, int c, size_t n);` copies the value of c into the first n characters of the object pointed to by s
- `char* strcat(char *s, const char *t);` concatenates string pointed to by t to the end of string pointed to by s; returns a pointer to string pointed to by s
- `char* strchr(const char *s, int c);` returns a pointer to the first occurrence of the character c in the string pointed to by s
- `int strcmp(const char *s, const char *t);` compares string s to string t in an element-by-element comparison; returns an integer greater than, equal to, or less than zero, depending on whether the string pointed to by s is greater than, equal to, or less than, respectively, the string pointed to by t
- `int strcoll(const char *s, const char *t);` returns an integer greater than, equal to, or less than zero, depending on whether the string pointed to by s is greater than, equal to, or less than, respectively, the string pointed to by t
- `char* strcpy(char *s, const char *t);` copies string pointed to by t to string pointed to by s; returns a pointer to string pointed to by s
- `size_t strcspn(const char *s, const char *t);` returns the length of the initial segment of the string pointed to by s that consists entirely of characters not in the string pointed to by t
- `size_t strlen(const char *s);` returns the length of the string pointed to by s
- `char* strncat(char *s, const char *t, size_t n);` concatenates at most n characters of string t to string s; returns a pointer to string pointed to by s
- `int strncmp(const char *s, const char *t, size_t n);` compares at most n characters of string s to string t in an element-by-element comparison; returns an integer greater than, equal to, or less than zero, depending on whether the string pointed to by s is greater than, equal to, or less than, respectively, the string pointed to by t
- `char* strncpy(char *s, const char *t, size_t n);` copies at most n characters from string pointed to by t to string pointed to by s; if t has fewer characters than s, then s is padded with null characters; returns a pointer to s
- `char* strpbrk(const char *s, const char *t);` returns a pointer to the first occurrence in string pointed to by s of any character of string pointed to by t
- `char* strrchr(const char *s, int c);` returns a pointer to the last occurrence of the character c in the string pointed to by s
- `size_t strspn(const char *s, const char *t);` returns the length of the initial segment of the string pointed to by s that consists entirely of characters in the string pointed to by t
- `char* strstr(const char *s, const char *t);` returns a pointer to the start of the string pointed to by t within the string pointed to by s

## <ctime>

The header file <ctime> defines two macros, four types, and several functions for representing and manipulating calendar time and local time. The types clock_t and time_t are arithmetic types capable of representing times, and the structure tm contains a calendar time broken into seconds (tm_sec), minutes (tm_min), hours (tm_hour), day of the month (tm_mday), months since January (tm_mon), years since 1900 (tm_year), days since Sunday (tm_wday), days since January 1 (tm_yday), and a daylight saving time flag (tm_isdst); the order of the values in the structure is system dependent. The related macros are the following:

- CLOCKS_PER_SEC
  number per second of the value returned by the clock function
- NULL
  an integer representing binary zero

Function prototypes and brief descriptions of their related computations follow:

- `char* asctime(const struct tm *timeptr);`
  returns a pointer to the string containing a converted time
- `clock_t clock(void);`
  returns the current processor time
- `char* ctime(const time_t *time);`
  returns a pointer to a string containing a converted time
- `double difftime(time_t time1, time_t time0);`
  computes the difference between two calendar times
- `struct tm *gmtime(const time_t *timer);`
  returns a pointer to a time expressed in Coordinated Universal Time
- `struct tm *localtime(const time_t *timer);`
  returns a pointer to a time converted from calendar time
- `time_t mktime(struct tm *timeptr);`
  converts the broken-down time to a calendar time value
- `time_t time(time_t *timer);`
  returns the current calendar time
- `size_t strftime(char *s, size_t maxsize, const char *format, const struct tm *timeptr);`
  converts time into a formatted multibyte character sequence
