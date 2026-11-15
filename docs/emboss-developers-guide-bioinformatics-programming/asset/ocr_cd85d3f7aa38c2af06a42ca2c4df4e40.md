# 6.5.19 String parsing functions

Functions for parsing text tokens from strings have the prefix ajStrExtract or the prefix ajStrParse.

To extract the first word (Pword) and the remainder of the string (Prest) from an input string (str) use either of:

```
/* Remove first word (with no leading spaces) from a string *
AjBool ajStrExtractFirst (const AjPStr str, AjPStr* Prest, AjPStr* Pword);

/* Remove first word from a string, skipping spaces */
AjBool ajStrExtractWord (const AjPStr str, AjPStr* Prest, AjPStr* Pword);
```

ajStrExtractWord will skip any leading whitespace whereas ajStrExtractFirst will return ajFalse if the input string starts with a space. Like most of the string functions they will allocate memory for the strings if necessary although it is cleaner to allocate the strings manually. In the example below, ajStrExtractFirst will return ajFalse and the printed strings will be empty, whereas ajStrExtractFirst will print the first word and the rest of the string:

```
AjPStr inputstring = NULL;
AjPStr word     = NULL;
AjPStr rest     = NULL;

inputstring = ajStrNewC(" First word in this string is 'First'");
word        = ajStrNew();
rest        = ajStrNew();

ajStrExtractFirst(inputstring, &rest, &word);
ajFmtPrint("word: %S\n", word);   /* Empty */
ajFmtPrint("rest: %S\n", rest);   /* Empty */

ajStrExtractWord(inputstring, &rest, &word);
ajFmtPrint("word: %S\n", word);   /* First */
ajFmtPrint("rest: %S\n", rest);   /* word in this string is 'First' */

ajStrDel(&inputstring);
ajStrDel(&word);
ajStrDel(&rest);
```

There is a function to split a newline-separated multi-line string into an array of strings:

```
ajuint ajStrParseSplit(const AjPStr str, AjPStr **PStr);
```

The function allocates memory for an array of strings (which must be freed later) and returns the number of array elements created:

```
AjPStr inputstring = NULL;
AjPStr *array      = NULL;
ajint    dim;
ajint    x;
```