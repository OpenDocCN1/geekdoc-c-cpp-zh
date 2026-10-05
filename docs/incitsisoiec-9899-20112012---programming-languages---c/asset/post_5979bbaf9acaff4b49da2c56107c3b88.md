
return values is not necessarily meaningful measure of the number of characters written or read.

## Returns

If successful, the ftell function returns the current value of the file position indicator for the stream. On failure, the ftell function returns -1 and stores an implementation-defined positive value in errno.

## 7.21.9.5 The rewind function

### Synopsis

```
#include <stdio.h>
void rewind(FILE *stream);
```

### Description

The rewind function sets the file position indicator for the stream pointed to by the beginning of the file. It is equivalent to

```
(void) fseek(stream, 0, SEEK_SET)
```

except that the error indicator for the stream is also cleared.

### Returns

The rewind function returns no value.

## 7.21.10 Error-handling functions

### 7.21.10.1 The clearerr function

### Synopsis

```
#include <stdio.h>
void clearerr(FILE *stream);
```

### Description

The clearerr function clears the end-of-file and error indicators for the stream pointed to by stream.

### Returns

The clearerr function returns no value.

## 7.21.10.2 The feof function

### Synopsis

```
#include <stdio.h>
int feof(FILE *stream);
```

### Description

The feof function tests the end-of-file indicator for the stream pointed to by stream.

### Returns

The feof function returns nonzero if and only if the end-of-file indicator is set for stream.

## 7.21.10.3 The ferror function

### Synopsis

```
#include <stdio.h>
int ferror(FILE *stream);
```

### Description

The ferror function tests the error indicator for the stream pointed to by stream.

### Returns

The ferror function returns nonzero if and only if the error indicator is set for stream.

## 7.21.10.4 The perror function

### Synopsis

```
#include <stdio.h>
void perror(const char *s);
```

### Description

The perror function maps the error number to the integer expression errno to an error message. It writes a sequence of characters to the standard error stream first: (if s is not a null pointer and the character pointed to by s is not the null character), the string pointed to by s followed by a colon (:) and a space; an appropriate error message followed by a new-line character. The contents of the error message strings are the same as those returned by the strerror function with argument errno.

### Returns

The perror function returns no value.

Forward references: the strerror function (7.24.6.2).

## 7.22 General utilities <stdlib.h>

The header <stdlib.h> declares five types and several functions of general utility, and defines several macros.(291)

The types declared are size_t and wchar_t (both described in 7.19),

```
div_t
```

which is a structure type that is the type of the value returned by the div function,

```
ldiv_t
```

which is a structure type that is the type of the value returned by the ldiv function, and

```
ll1div_t
```

which is a structure type that is the type of the value returned by the 11div function.

The macros defined are NULL (described in 7.19);

```
EXIT_FAILURE
```

and

```
EXIT_SUCCESS
```

which expand to integer constant expressions that can be used as the argument to the exit function to return unsuccessful or successful termination status, respectively, to the host environment;

```
RAND_MAX
```

which expands to an integer constant expression that is the maximum value returned by the rand function; and

```
MB_CUR_MAX
```

which expands to a positive integer expression with type size_t that is the maximum number of bytes in a multibyte character for the extended character set specified by the current locale (category LC_CTYPE), which is never greater than MB_LEN_MAX.

## 7.22.1 Numeric conversion functions

The functions atof, atoi, and atoll need not affect the value of the integer expression errno on an error. If the value of the result cannot be represented, the behavior is undefined.

### 7.22.1.1 The atof function

### Synopsis

```
#include <stdlib.h>
double atof(const char *nptr);
```

### Description

The atof function converts the initial portion of the string pointed to by nptr to double representation. Except for the behavior on error, it is equivalent to

```
strtod(nptr, (char **)NULL)
```

### Returns

The atof function returns the converted value.

Forward references: the strtod, strtof, and strtol functions (7.22.1.3).

### 7.22.1.2 The atoi, atoi, and atoll functions

### Synopsis

```
#include <stdlib.h>
int atoi(const char *nptr);
long atoi(const char *nptr);
long int atoll(const char *nptr);
```

### Description

The atoi, atoi, and atoll functions convert the initial portion of the string pointed to by nptr to int, long int, and long long int representation, respectively. Except for the behavior on error, they are equivalent to

```
atoi: (int) strtol(nptr, (char **)NULL, 10)
atoi: strtol(nptr, (char **)NULL, 10)
atoll: strtol(nptr, (char **)NULL, 10)
```

### Returns

The atoi, atoi, and atoll return the converted value.

Forward references: the strtol, strtoll, and strtou functions (7.22.2).

## 7.22.1.3 The stod, strtof, and strtol functions

### Synopsis

```
#include <stdlib.h>
double strtod(const char *nptr);
float strtof(const char *nptr);
long strtol(const char *nptr);
```

### Description

The stod, strtof, and strtol functions convert the initial portion of the string pointed to by nptr to double, float, and long int representation, respectively. Except for the behavior on error, they decompose the input string into three parts: an initial, possibly empty, sequence of digits, an optional decimal-point, and an optional exponent. Then, they attempt to convert the subject sequence to the appropriate type.

### Returns

The stod, strtof, and strtol return the converted value.

Forward references: the strtod, strtol, strtoll, and strtou functions (7.22.2).

## 7.22.1.4 The strtod function

### Synopsis

```
#include <stdlib.h>
double strtod(const char *nptr, char **endptr);
```

### Description

The strtod function converts the initial portion of the string pointed to by nptr to double representation. Except for the behavior on error, it is equivalent to

```
strtod(nptr, (char **)NULL)
```

### Returns

The strtod function returns the converted value.

Forward references: the strtod, strtof, and strtol functions (7.22.1.3).

## 7.22.1.5 The strtof function

### Synopsis

```
#include <stdlib.h>
float strtof(const char *nptr, char **endptr);
```

### Description

The strtof function converts the initial portion of the string pointed to by nptr to float representation. Except for the behavior on error, it is equivalent to

```
strtof(nptr, (char **)NULL)
```

### Returns

The strtof function returns the converted value.

Forward references: the strtod, strtol, and strtoll functions (7.22.1.3).

## 7.22.1.6 The strtol function

### Synopsis

```
#include <stdlib.h>
long strtol(const char *nptr, char **endptr, int base);
```

### Description

The strtol function converts the initial portion of the string pointed to by nptr to long int representation. Except for the behavior on error, it is equivalent to

```
strtol(nptr, (char **)NULL, base)
```

### Returns

The strtol function returns the converted value.

Forward references: the strtod, strtof, and strtoll functions (7.22.1.3).

## 7.22.1.7 The strtoll function

### Synopsis

```
#include <stdlib.h>
long long strtoll(const char *nptr, char **endptr, int base);
```

### Description

The strtoll function converts the initial portion of the string pointed to by nptr to long long int representation. Except for the behavior on error, it is equivalent to

```
strtoll(nptr, (char **)NULL, base)
```

### Returns

The strtoll function returns the converted value.

Forward references: the strtod, strtof, and strtol functions (7.22.1.3).

## 7.22.1.8 The strtou function

### Synopsis

```
#include <stdlib.h>
unsigned long strtou(const char *nptr, char **endptr, int base);
```

### Description

The strtou function converts the initial portion of the string pointed to by nptr to unsigned long int representation. Except for the behavior on error, it is equivalent to

```
strtou(nptr, (char **)NULL, base)
```

### Returns

The strtou function returns the converted value.

Forward references: the strtod, strtof, and strtoll functions (7.22.1.3).

## 7.22.1.9 The strquad function

### Synopsis

```
#include <stdlib.h>
long double strquad(const char *nptr, char **endptr);
```

### Description

The strquad function converts the initial portion of the string pointed to by nptr to long double representation. Except for the behavior on error, it is equivalent to

```
strquad(nptr, (char **)NULL)
```

### Returns

The strquad function returns the converted value.

Forward references: the strtod, strtof, and strtol functions (7.22.1.3).
