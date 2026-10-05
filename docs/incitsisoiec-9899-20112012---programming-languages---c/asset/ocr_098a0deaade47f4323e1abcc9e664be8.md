# 7.22.1 Numeric conversion functions

The functions atof, atoi, and atoll need not affect the value of the integer expression errno on an error. If the value of the result cannot be represented, the behavior is undefined.

# 7.22.1.1 The atof function

Synopsis

```
#include <stdlib.h>
double atof(const char *nptr);
```

Description

The atof function converts the initial portion of the string pointed to by nptr to double representation. Except for the behavior on error, it is equivalent to

```
strtod(nptr, (char **)NULL)
```

Returns

The atof function returns the converted value.

Forward references: the strtod, strtof, and strtol functions (7.22.1.3).

# 7.22.1.2 The atoi, atoi, and atoll functions

Synopsis

```
#include <stdlib.h>
int atoi(const char *nptr);
long atoi(const char *nptr);
long int atoll(const char *nptr);
```

Description

The atoi, atoi, and atoll functions convert the initial portion of the string pointed to by nptr to int, long int, and long long int representation, respectively. Except for the behavior on error, they are equivalent to

```
atoi: (int) strtol(nptr, (char **)NULL, 10)
atoi: strtol(nptr, (char **)NULL, 10)
atoll: strtolll(nptr, (char **)NULL, 10)
```

Returns

The atoi, atoi, and atoll return the converted value.

Forward references: the strtol, strtoll, strtol, and strtoull functions (7.22.1.4).