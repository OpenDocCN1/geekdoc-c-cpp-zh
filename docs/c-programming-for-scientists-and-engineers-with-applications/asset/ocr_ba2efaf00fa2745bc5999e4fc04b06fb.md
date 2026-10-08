# APPENDIX B

This appendix contains the most commonly used input/output functions, mathematical functions, string functions, and memory management functions. To access these functions provided in the C language, the header files containing these functions must be linked to the program by the #include directive. For example to include all of the input/output functions the directive is #include <stdio.h> and to include mathematical functions the directive is #include <math.h>, and so on.

Input and Output Functions Input and output is performed by using input and output functions built into the C language. The prototypes of these functions are contained in a header file called stdio.h (an abbreviation meaning “standard input/output”). For the program to have access to these functions the programmer must include the stdio.h header file in the program by writing the following statement:

```
#include <stdio.h>
```

Where the .h extension means that stdio.h is a header file. Also note that all header files must be included between two angle brackets.

The input and output functions from the C library header file stdio.h can be grouped into two distinct groups: format driven functions and data driven functions.