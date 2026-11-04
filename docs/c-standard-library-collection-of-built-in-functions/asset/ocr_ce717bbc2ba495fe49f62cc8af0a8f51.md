| | |
|---|---|
| | This is the value for the exit function to return in case of failure. |
| 3 | **EXIT_SUCCESS**<br>This is the value for the exit function to return in case of success. |
| 4 | **RAND_MAX**<br>This macro is the maximum value returned by the **rand** function. |
| 5 | **MB_CUR_MAX**<br>This macro is the maximum number of bytes in a multi-byte character set which cannot be larger than MB_LEN_MAX. |

# Library Functions

Following are the functions defined in the header stdio.h:

| S.N. | Function & Description |
|---|---|
| 1 | double atof(const char *str)<br>Converts the string pointed to, by the argument *str* to a floating-point number (type double). |
| 2 | int atoi(const char *str)<br>Converts the string pointed to, by the argument *str* to an integer (type int). |
| 3 | long int atol(const char *str)<br>Converts the string pointed to, by the argument *str* to a long integer (type long int). |
| 4 | double strtod(const char *str, char **endptr)<br>Converts the string pointed to, by the argument *str* to a floating-point number (type double). |
| 5 | long int strtol(const char *str, char **endptr, int base)<br>Converts the string pointed to, by the argument *str* to a long integer (type long int). |