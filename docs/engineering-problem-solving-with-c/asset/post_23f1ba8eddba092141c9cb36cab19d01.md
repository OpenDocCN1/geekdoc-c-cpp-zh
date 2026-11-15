

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

## <cstring>

The header file <cstring> defines the type size_t, which is an unsigned integer, and the macro NULL, which has the value binary zero. In addition, the header file defines a number of functions for handling strings.

void* memchr(const void *s, int c, size_t n);
returns a pointer to the first occurrence of c in the initial n characters of the object pointed to by s

int memcmp(const void *s1, const void *s2, size_t n);
returns an integer greater than, equal to, or less than zero, accordingly, as the string pointed to by s is greater than, equal to, or less than the string pointed to by t

void* memcpy(void *s, const void *t, size_t n);
copies n characters from the object pointed to by t into the object pointed to by s

void* memmove(void *s, const void *t, size_t n);
copies n characters from the object pointed to by t into the object pointed to by s, using a temporary area

void* memset(void *s, int c, size_t n);
copies the value of c into the first n characters of the object pointed to by s

char* strcat(char *s, const char *t);
concatenates string pointed to by t to the end of string pointed to by s; returns a pointer to string pointed to by s

char* strchr(const char *s, int c);
returns a pointer to the first occurrence of the character c in the string pointed to by s

int strcmp(const char *s, const char *t);
compares string s to string t in an element-by-element comparison; returns an integer greater than, equal to, or less than zero, depending on whether the string pointed to by s is greater than, equal to, or less than, respectively, the string pointed to by t

int strcoll(const char *s, const char *t);
returns an integer greater than, equal to, or less than zero, depending on whether the string pointed to by s is greater than, equal to, or less than, respectively, the string pointed to by t

char* strcpy(char *s, const char *t);
copies string pointed to by t to string pointed to by s; returns a pointer to string pointed to by s

size_t strcspn(const char *s, const char *t);
returns the length of the initial segment of the string pointed to by s that consists entirely of characters not in the string pointed to by t

size_t strlen(const char *s);
returns the length of the string pointed to by s

char* strncat(char *s, const char *t, size_t n);
concatenates at most n characters of string t to string s; returns a pointer to string pointed to by s

int strncmp(const char *s, const char *t, size_t n);
compares at most n characters of string s to string t in an element-by-element comparison; returns an integer greater than, equal to, or less than zero, depending on whether the string pointed to by s is greater than, equal to, or less than, respectively, the string pointed to by t

char* strncpy(char *s, const char *t, size_t n);
copies at most n characters from string pointed to by t to string pointed to by s; if t has fewer characters than n, then s is padded with null characters; returns a pointer to s

char* strpbrk(const char *s, const char *t);
returns a pointer to the first occurrence in string pointed to by s of any character of string pointed to by t

char* strrchr(const char *s, int c);
returns a pointer to the last occurrence of the character c in the string pointed to by s

size_t strspn(const char *s, const char *t);
returns the length of the initial segment of the string pointed to by s that consists entirely of characters in the string pointed to by t

char* strstr(const char *s, const char *t);
returns a pointer to the first occurrence of the string pointed to by t within the string pointed to by s

## <ctime>

The header file <ctime> defines two macros, four types, and several functions for representing and manipulating calendar time and local time. The types clock_t and time_t are arithmetic types capable of representing times, and the structure tm contains calendar time broken into seconds (tm_sec), minutes (tm_min), hours (tm_hour), day of the month (tm_mday), months since January (tm_mon), years since 1900 (tm_year), days since Sunday (tm_wday), days since January 1 (tm_yday), and a daylight saving time flag (tm_isdst); the order of the values in the structure is system dependent. The related macros are the following:

CLOCKS_PER_SEC
number per second of the value returned by the clock function

NULL
an integer representing binary zero

Function prototypes and brief descriptions of their related computations follow:

char* asctime(const struct tm *timeptr);
returns a pointer to the string containing a converted time

clock_t clock(void);
returns the current processor time

char* ctime(const time_t *timer);
returns a pointer to a string containing a converted time

double difftime(time_t time1, time_t time0);
computes the difference between two calendar times

struct tm *gmtime(const time_t *timer);
returns a pointer to a time expressed in Coordinated Universal Time

struct tm *localtime(const time_t *timer);
returns a pointer to a time converted from calendar time

time_t mktime(struct tm *timeptr);
converts the broken-down time to a calendar time value

time_t time(time_t *timer);
returns the current calendar time

size_t strftime(char *s, size_t maxsize, const char *format, const struct tm *timeptr);
converts time into a formatted multibyte character sequence

## <iostream>

The header <iostream> contains many functions used for standard input and output. We now list a few of them in their most general form:

### istream functions:

- `istream& operator >>`
  Input (extraction) operation
- `int gcount();`
  Returns the number of characters extracted by last input operation
- `int get(char ch);`
  Extract one character from input stream
- `getline(char_string var, int max, [char delimiter]);`
  read max-1 characters or until delimiter is found. \n is the default delimiter
- `ignore();`
  Extract and discard a character from the input stream
- `char peek();`
  Returns the value of next character on the input stream
  Leaves the character on the input stream (does not extract)
- `putback(ch);`
  Put the last character back on the input stream

### ostream functions:

- `ostream& operator<<`
  Output (insertion) operator
- `flush();`
  Flush output buffer
- `put(ch char);`
  Put char in the output stream

## APPENDIX B ASCII Character Codes

The following table contains the 128 ASCII characters and their equivalent integer values and binary values. The characters that correspond to the integers 1 through 31 have special significance to the computer system. For example, the character BEL is represented by the integer 7 and causes the bell to sound on the keyboard.

The order of the characters from low to high is the collating sequence and has several interesting characteristics. Note that the digits are less than uppercase letters and that uppercase letters are less than lowercase letters. Also, note that special characters are not grouped together. Some are before digits, some are after digits, and some are between uppercase and lowercase characters.

| Character | Integer Equivalent | Binary Equivalent |
| :--- | :--- | :--- |
| NUL (Binary Zero) | 0 | 00000000 |
| SOH (Start of Header) | 1 | 00000001 |
| STX (Start of Text) | 2 | 00000010 |
| ETX (End of Text) | 3 | 00000011 |
| EOT (End of Transmission) | 4 | 00000100 |
| ENQ (Enquiry) | 5 | 00000101 |
| ACK (Acknowledge) | 6 | 00000110 |
| BEL (Bell) | 7 | 00000111 |
| BS (Backspace) | 8 | 00001000 |
| HT (Horizontal Tab) | 9 | 00001001 |
| LF (Line Feed or New Line) | 10 | 00001010 |
| VT (Vertical Tabulation) | 11 | 00001011 |
| FF (Form Feed) | 12 | 00001100 |
| CR (Carriage Return) | 13 | 00001101 |
| SO (Shift Out) | 14 | 00001110 |
| SI (Shift In) | 15 | 00001111 |
| DLE (Data Link Escape) | 16 | 00010000 |
| DC1 (Device Control 1) | 17 | 00010001 |
| DC2 (Device Control 2) | 18 | 00010010 |
| DC3 (Device Control 3) | 19 | 00010011 |
| DC4 (Device Control 4-Stop) | 20 | 00010100 |
| NAK (Negative Acknowledge) | 21 | 00010101 |
| SYN (Synchronization) | 22 | 00010110 |
| ETB (End of Text Block) | 23 | 00010111 |
| CAN (Cancel) | 24 | 00011000 |
| EM (End of Medium) | 25 | 00011001 |
| SUB (Substitute) | 26 | 00011010 |
| | | (continued) |

