# Point of Information

# Processing C-Strings

C-string variables can't be assigned values after being declared. For example, if test has been declared as a C-string with the declaration statement

```
char test[] = "abcd";
```

a subsequent assignment, such as test = "efgh", is invalid.

In place of an assignment, you can use the strcpy() function, such as strcpy(test, "efgh"). The only restriction on using strcpy() is that the size of the declared array (five elements, in this case) can't be exceeded. Attempting to copy a larger C-string value into test causes the copy to overflow the destination array, beginning with the memory area immediately after the last array element. This memory overflow overwrites whatever was in these memory locations and typically causes a runtime crash when the overwritten areas are accessed via their legitimate identifier names.

The same problem can happen when using the strcat() function. It's your responsibility to ensure that the concatenated C-string fits into the original string.

An interesting situation arises when C-string variables are defined with pointers (see the Point of Information in Section 15.3). In these situations, assignments can be made after the declaration statement.

# Library Functions

Because a C-string is an array and C++ doesn't provide built-in operations for arrays, such as array assignment and relational comparisons, these operations aren't provided for C-strings. Extensive collections of C-string-handling functions, however, are included with all C++ compilers. They effectively supply C-string assignment, comparison, and other useful C-string operations. Table 15.2 lists the more common C-string library functions, which are called in the same manner as all C++ functions. The declarations for these functions are in the standard header file cstring and must be included in your program before the function is called.

# Table 15.2 C-String Library Functions (Require the Header File cstring)

| Name | Description | Example |
|---|---|---|
| strcpy(stringVar, stringExp) | Copies stringExp to stringVar, including the '\0'. | strcpy(test, "efgh") |
| strcat(stringVar, stringExp) | Appends stringExp to the end of the string value contained in stringVar. | strcat(test, "there") |
| strlen(stringExp) | Returns the length of the string. Does not include the '\0' in the length count. | strlen("Hello World!") |