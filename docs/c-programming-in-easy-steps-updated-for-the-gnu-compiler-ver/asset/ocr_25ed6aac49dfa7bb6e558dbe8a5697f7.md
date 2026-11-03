# Qualifying data types

When an integer variable, of the int data type, is created it can by default contain either positive or negative values. These are known as “signed” values. The range of possible values is determined by your system as either “long” or “short”.

If the int variable is created by default as a long type (likely) it will typically have a possible range of values from a maximum of +2,147,483,647 down to a minimum of -2,147,483,648.

On the other hand, if the int variable is created by default as a short type (unlikely) it will typically have a possible range of values from a maximum of +32,767 to a minimum of -32,768.

The range size can be explicitly specified, however, using the short and long qualifier keywords in the variable declaration, like this:

```
short int num1 ;   /* Saves memory space. */
long int num2 ;   /* Allows bigger range. */
```

The limits.h C library header file contains implementation-defined limits for the size of each data type. These can be accessed via constant values named INT_MAX and INT_MIN for int variable declarations of unspecified size. Similarly, SHRT_MAX and SHRT_MIN contain limits for short int variable declarations, and LONG_MAX and LONG_MIN contain limits for long int variable declarations.

A non-negative “unsigned” int variable can be declared using the unsigned qualifier keyword when the variable will never be assigned a negative value. An unsigned short int variable will typically have a possible range from 0 to 65,535 but will only occupy the same memory space as a regular short int variable. An unsigned long int variable will typically have a possible range from 0 to 4,294,967,295 but will only occupy the same memory space as a regular long int variable.

The C sizeof operator can be used to reveal the amount of memory space reserved by variables of different data types. It is good programming practice to use the smallest amount of memory possible. For example, where a variable will only ever contain positive integer values below 65,535 it is preferable to use an unsigned short int variable that reserves just 2 bytes of memory rather than a long int variable that reserves 4 bytes of memory.

![](bbox=[0.08, 0.15, 0.22, 0.28])

Constants are always named entirely in uppercase to distinguish them from variables.

![](bbox=[0.08, 0.7, 0.22, 0.83])

The memory space allocated to an int variable of unspecified size is system-dependent but will often be treated as a long int by default.