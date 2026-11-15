```
AjBool ajStrTokenNextParseC (AjPStrTok* Ptoken, const char* txtdelim, AjPStr* Pstr);
AjBool ajStrTokenNextParseS (AjPStrTok* Ptoken, const AjPStr strdelim, AjPStr* Pstr);
```

These functions return ajTrue if the token was parsed successfully or ajFalse otherwise. ajStrTokenNextParseC and ajStrTokenNextParseS will update the string tokenisation object with the string of delimiters (strdelim or txtdelim) provided. Note that these functions can return ajTrue but write an empty token (Pstr) in cases where the delimiter has been changed since the previous call.

The string tokenisation object can be reset (all strings cleared) so that it is ready for reuse by calling:

```
void ajStrTokenReset (AjPStrTok* Ptoken);
```

Once you are done you must free the string tokenisation object:

```
/* String tokenisation object destructor */
void ajStrTokenDel (AjPStrTok* Ptoken);
```

The example code below uses the string tokenisation object and its functions to retrieve individual lines from a string that contains multiple newline characters:

```
AjPStr inputstring  = NULL;
AjPStr token        = NULL;
AjPStrTok tokens    = NULL;

inputstring = ajStrNewC("First line\nSecond line\nThird line\n");
tokens = ajStrTokenNewC(inputstring, "\n");

while(ajStrTokenNextFind(&tokens, &token))
    ajFmtPrint("token: %S\n", token);

ajStrTokenDel(&tokens);
ajStrDel(&inputstring);
```

A string (str or txt) may be tokenised with either whitespace characters or a specified set of delimiters given as a text string (txtdelim):

```
/* Tokenise C-type string by set of delimiters */
AjPStr ajCharParseC (const char* txt, const char* delim);

/* Tokenise by set of delimiters */
const AjPStr ajStrParseC (const AjPStr str, const char* txtdelim);

/* Tokenise by whitespace */
const AjPStr ajStrParseWhite (const AjPStr str);
```

These functions use the C strtok function and return tokens from the string. The first time the function is called it is passed the string to be parsed. For subsequent calls on the same string it is passed NULL as the first argument. A pointer to the token is returned or NULL when all tokens have been parsed: