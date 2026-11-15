```
/* String to C-type string */
int ajStrCmpC (const AjPStr thys, const char *text);

/* String to string */
int ajStrCmpS (const AjPStr str, const AjPStr str2);

/* Case-insensitive string to string */
int ajStrCmpCaseS (const AjPStr str1, const AjPStr str2);

/* String to C-type string using the first len characters only */
ajint ajStrCmpLenC (const AjPStr thys, const char *text, ajuint len);

/* String to string using the first len characters only */
int ajStrCmpLenS (const AjPStr str, const AjPStr str2, ajuint len);

/* String to C-type string with wildcards.*/
int ajStrCmpWildC (const AjPStr thys, const char* text);

/* String to string with wildcards.*/
int ajStrCmpWildS (const AjPStr thys, const AjPStr str);

/* Case-insensitive string to C-type string with wildcards.*/
int ajStrCmpWildCaseC (const AjPStr thys, const char* text);

/* Case-insensitive string to string with wildcards.*/
int ajStrCmpWildCaseS (const AjPStr thys, const AjPStr str);

/* Same as ajStrCmpS but strings are cast as void */
int ajStrVcmp (const void* str1, const void* str2);
```

There are also comparison functions for handling C-type strings:

```
/* Case-insensitive C-type string to C-type string */
int ajCharCmpCase (const char* txt1, const char* txt2);

/* Case-insensitive C-type string to C-
type string using the first len characters only */
int ajCharCmpCaseLen (const char* txt1, const char* txt2, ajuint len);

/* C-type string to C-type string using wildcards. *
ajint ajCharCmpWild (const char* txt1, const char* txt2);

/* Case-insensitive C-type string to C type string using wildcards. *
ajint ajCharCmpWildCase (const char* txt1, const char* txt2);
```

The functions return an integer representing the sort order which is -1 if the first string should sort before the second, +1 if the second string should sort first, or 0 if they are identical.

# 6.16.12 List conversion

A list may be converted to an array by using:

```
ajint ajListToarray (const AjPList list, void*** PParray);
ajint ajListstrToarray (const AjPList list, AjPStr** PParray);
```