
## Argument functions

<stdarg.h>
The stdarg.h header file contains functions that can be used to step through a list of function arguments without first knowing their number and type. Due to the nature of these functions they must be implemented as “macros” within the function body.

The list of arguments is assigned to a special data type named va_list. The functions listed in the following table manipulate a variable named “args” of the va_list type:

| Function | Description |
|---|---|
| va_start( va_list args , lastarg) | Must be called once to initialize the va_list named args at the position in the list of the last known argument lastarg |
| va_arg( va_list args , data-type ) | After va_list args has been initialized by va_start() each successive call to va_arg() will return the value of the next argument in the args list as the specified data-type |
| va_end( va_list args ) | Must be called once after the arguments in the va_list args have been processed, before the function is exited |

## Date & time functions

<time.h>

The time.h header file contains functions for manipulating date and time. Some of these functions process “Calendar time”, which is based on the Gregorian calendar. This is stated in seconds elapsed since the Epoch (00:00:00 GMT January 1st, 1970).

Other functions contained in time.h process “Local time”, which is the translation of Calendar time accounting for time zone.

The data type time_t is used to describe both Calendar time and Local time.

A struct named tm contains the components of Calendar time, which are listed in the table below:

| Component: | Description: |
|---|---|
| int tm_sec | seconds after the minute, 0-61 |
| int tm_min | minutes after the hour, 0-59 |
| int tm_hour | hours since midnight, 0-23 |
| int tm_mday | day of the month, 1-31 |
| int tm_mon | months since January, 0-11 |
| int tm_year | years since 1900 |
| int tm_wday | days since Sunday, 0-6 |
| int tm_yday | days since January 1st, 0-365 |
| int tm_isdst | Daylight Saving Time flag |

The tm_isdst component is positive if Daylight Saving is in effect, zero if it is not, or negative if the information is unavailable.

The functions contained in the time.h header file are listed in the table here.

The time.h header file contains the functions listed below that can be used to manipulate date and time:

| Function | Description |
|---|---|
| clock_t clock( void ) | Returns the processor time used by the program since it started, or -1 if unavailable |
| time_t time( time_t *tp ) | Returns the current calendar time, or -1 if unavailable |
| double difftime( time_t time2 , time_t time1 ) | Returns time2 minus time1, expressed in seconds |
| time_t mktime( struct tm *tp ) | Converts the local time in the structure *tp into calendar time |
| char *asctime( const struct tm *tp ) | Converts the time in the struct *tp into a standard string |
| char *ctime( const time_t *tp ) | Converts calendar time to local time |
| struct tm *gmtime( const time_t *tp ) | Converts calendar time into Co-ordinated Universal Time (UTC or GMT) |
| struct tm *localtime( const time_t *tp ) | Converts the calendar time *tp into local time |
| size_t strftime( char *s , size_t smax , const char *fmt , const struct tm *tp ) | Formats the time *tp into a chosen format *fmt |

The strftime() function formats selected components of the tm structure according to the stated format specifier. All the possible format specifiers are listed in the table below.

| Specifier: | Description: |
|---|---|
| %a | abbreviated weekday name |
| %A | full weekday name |
| %b | abbreviated month name |
| %B | full month name |
| %c | local date and time representation |
| %d | day of the month, 01-31 |
| %H | hour (24-hour clock), 00-23 |
| %I | hour (12-hour clock), 01-12 |
| %j | day of the year, 001-366 |
| %m | month of the year, 01-12 |
| %M | minute, 00-59 |
| %p | local equivalent of AM or PM |
| %S | second, 00-61 (to account for leap seconds) |
| %U | week number of the year (Sunday as the first day of the week), 00-53 |
| %w | weekday number, 0-6 (Sunday is 0) |
| %W | week number of the year (Monday as the first day of the week), 00-53 |
| %x | local date representation |
| %X | local time representation |
| %y | year without century, 00-99 |
| %Y | year with century |
| %Z | time zone name, if available |

## Jump functions

<setjmp.h>

The **setjmp.h** header is used for controlling low-level calls and provides a means to avoid the normal call and return sequence.

| Function | Description |
|---|---|
| `int setjmp( jmp_buf env )` | Low-level function used in conditional tests to save the environment in the *env* variable, then return zero |
| `void longjmp( jmp_buf env , int value )` | Restores an environment that has been saved in the *env* variable by `setjmp()`, as if `setjmp()` had returned the *value* |

## Signal functions

<signal.h>

The signal.h header contains functions for handling exceptional conditions that may arise during the execution of a program:

```
void (*signal ( int sig , void (*handler) ( int ))) ( int )
```

The signal() function specifies how subsequent signals will be handled. The handler can be SIG_DFL, an implementation-defined default; or SIG_IGN, to ignore the signal. Valid sig signals include:

- SIGABRT : abort termination
- SIGFPE : arithmetic error
- SIGILL : illegal instruction
- SIGINT : external interruption
- SIGSEGV : access outside memory limit
- SIGTERM : termination request sent to the program

The function returns the previous value of the handler for that specific signal, or SIG_ERR if an error occurs. When a sig signal next occurs, the signal is restored to its default behavior then the signal handler is called. If this returns, execution resumes at the point where the signal occurred

```
int raise( int sig )
```

Attempts to send the sig signal to the program and returns a non-zero value if the attempt is unsuccessful

## Limit constants

<limits.h>

The table below lists constants related to maximum and minimum numerical limits. Their values vary according to implementation. Where a value is given, in brackets, it indicates a minimum size for that constant – but larger values may, in fact, be imposed. Programs should not assume that any implementation-dependent constant will be of a particular value.

| Constant: | Value: |
|---|---|
| CHAR_BIT | number of bits in a char (8) |
| CHAR_MAX | maximum value of char (UCHAR_MAX or SCHAR_MAX) |
| CHAR_MIN | minimum value of char (zero or SCHAR_MIN) |
| INT_MAX | maximum value of int (+32,767) |
| INT_MIN | minimum value of int (-32,767) |
| LONG_MAX | maximum value of long (+2,147,483,647) |
| LONG_MIN | minimum value of long (-2,147,483,647) |
| SCHAR_MAX | maximum value of signed char (+127) |
| SCHAR_MIN | minimum value of signed char (-127) |
| SHRT_MAX | maximum value of short (+32,767) |
| SHRT_MIN | minimum value of short (-32,767) |
| UCHAR_MAX | maximum value of unsigned char (+255) |
| UINT_MAX | maximum value of unsigned int (+65,535) |
| ULONG_MAX | maximum value of unsigned long (+4,294,967,295) |
| USHRT_MAX | maximum value of unsigned short (+65,535) |

## Float constants

<float.h>

The table below lists constants related to floating-point arithmetic. Their values vary according to implementation. Where a value is given, in brackets, it indicates a minimum size for that constant.

| Constant: | Value: |
|---|---|
| FLT_RADIX | radix of float exponent representations (2) |
| FLT_ROUNDS | rounding to the nearest number |
| FLT_DIG | number of precision digits (5) |
| FLT_EPSILON | smallest number x, where 1.0 + x != 1.0 (1E-5) |
| FLT_MANT_DIG | number of FLT_RADIX mantissa digits |
| FLT_MAX | maximum floating-point number (1E+37) |
| FLT_MAX_EXP | largest number n, where FLT_RADIX^(n-1) is a valid number |
| FLT_MIN | minimum floating-point number (1E-37) |
| FLT_MIN_EXP | smallest number n, where 10^n is valid |
| DBL_DIG | number of double-precision digits (10) |
| DBL_EPSILON | smallest number x, where 1.0 + x != 1.0 (1E-9) |
| DBL_MANT_DIG | number of FLT_RADIX mantissa digits |
| DBL_MAX | maximum double float number (1E+37) |
| DBL_MAX_EXP | largest number n, where FLT_RADIX^(n-1) is a valid number |
| DBL_MIN | minimum double float number (1E-37) |
| DBL_MIN_EXP | smallest number n, where 10^n is valid |
