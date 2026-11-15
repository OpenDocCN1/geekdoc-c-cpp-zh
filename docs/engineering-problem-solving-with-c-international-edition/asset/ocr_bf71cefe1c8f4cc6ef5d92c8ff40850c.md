```
int FLT_MIN_10_EXP;
int DBL_MIN_10_EXP;
int LDBL_MIN_10_EXP;
integer used to determine the minimum exponent for a base-10 normalized value for a
float, double, or long double value
int FLT_MAX_EXP;
int DBL_MAX_EXP;
int LDBL_MAX_EXP;
integer used to determine the maximum exponent for the radix base for a normalized
value for a float, double, or long double value
int FLT_MAX_10_EXP;
int DBL_MAX_10_EXP;
int LDBL_MAX_10_EXP;
integer used to determine the maximum exponent for a base-10 normalized value for a
float, double, or long double value
float FLT_MIN;
double DBL_MIN;
long double LDBL_MIN;
minimum representable value for a float, double, or long double value
float FLT_MAX;
double DBL_MAX;
long double LDBL_MAX;
maximum representable value for a float, double, or long double value
float FLT_EPSILON;
double DBL_EPSILON;
long double LDBL_EPSILON;
difference between 1 and the smallest value greater than 1 for a float, double, or
long double value
```

# <limits.h>

The header file <limits.h> provides several macros that give various limits and characteristics pertaining to integer values. These macros and their definitions are as follows:

```
int CHAR_BIT;
number of bits for the smallest nonbit value
int CHAR_MIN;
int CHAR_MAX;
minimum and maximum values for type char
int INT_MIN;
int INT_MAX;
minimum and maximum values for type int
int LONG_MIN;
int LONG_MAX;
minimum and maximum values for type long int
int MB_LEN_MAX;
maximum number of bytes in a multibyte character
int SCHAR_MIN;
int SCHAR_MAX;
minimum and maximum values for type signed char
```