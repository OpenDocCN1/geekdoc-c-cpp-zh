conventions in the table above. As with all statements in C programs, the declaration must end with a semi-colon terminator. Multiple variables of the same data type can be created in a single declaration as a comma-separated list, like this:

```
```
data-type variable-name-1 , variable-name-2 , variable-name-3 ;
```
```

![](bbox=[0.13, 0.214, 0.228, 0.289])

Variable names are case-sensitive in C – so variables named “VAR”, “Var”, and “var” would be treated as three separate variables.

![](bbox=[0.13, 0.372, 0.228, 0.446])

C keywords are listed in the table on the inner front cover of this book.

There are four basic data types in the C language. These are defined using the C keywords that are listed in the table below, together with a description of each data type:

| Data type: | Description: | Example: |
| --- | --- | --- |
| **char** | A single byte, capable of storing just one character | ‘A’ |
| **int** | An integer whole number | 100 |
| **float** | A floating-point number, correct to six decimal places | 0.123456 |
| **double** | A floating-point number, correct to 10 decimal places | 0.0123456789 |

The four data types allocate different amounts of machine memory for storing data. The smallest is the **char** data type, which allocates just a single byte of memory; and the largest is the **double** data type, which typically allocates eight bytes of memory. This is twice the amount of memory allocated by the **float** data