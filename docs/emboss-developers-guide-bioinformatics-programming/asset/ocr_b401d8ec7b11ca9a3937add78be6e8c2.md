```
AjPStr inputstring = NULL;
AjPStr token       = NULL;

inputstring = ajStrNewC(" First word in this string is 'First'");
token = ajStrParseWhite(inputstring)

/* Prints 'First' to the screen */
ajFmtPrint("token: %S\n", token);

/* Prints the rest of the words, one word at a time */
while(token = ajStrParseWhite(NULL))
    ajFmtPrint("token: %S\n", token);

ajStrDel(&inputstring);
```

To count the tokens in a string in which the tokens are delimited by either whitespace characters or a specified set of delimiters (strdelim) use:

```
/* Count tokens delimited by whitespace */
ajuint ajStrParseCount (const AjPStr line);

/* Count tokens delimited by set of delimiters */
ajuint ajStrParseCountS (const AjPStr line, const AjPStr
strdelim);
```

# 6.5.22 Handling C-type (char *) strings

For convenience, several groups of functions are provided for handling C-type (char *) strings. They all have the prefix ajChar to distinguish them from the other functions.

# 6.5.22.1 C-type string constructor and destructor functions

In the same way as for EMBOSS strings, a C-type string can be created from a starting C-type (char *) or string object, with or without a reserved size:

```
/* Create a string from a C-type string         */
char*   ajCharNewC (const char* txt);

/* Create a string from a string object         */
char*   ajCharNewS (const AjPStr thys);

/* Create an empty string of reserved size.     */
char*   ajCharNewRes(ajuint size);

/* Create a string with reserved size from a C-type string */
char*   ajCharNewResC(const char* txt, ajuint size);

/* Create a string with reserved size from a string object */
char*   ajCharNewResS(const AjPStr str, ajuint size);

/* Create a string from a C-type string with specified length */
char*   ajCharNewResLenC(const char* txt, ajuint size, ajuint len);
```