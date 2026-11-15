```
/* Trim sequence down to a defined range */
AjBool ajStrKeepRange(AjPStr* Pstr, ajint pos1, ajint pos2);

/* Removes all characters that are not in a given set. */
AjBool ajStrKeepSetC(AjPStr* Pstr, const char* txt);

/* Removes all characters that are not in a given set. */
AjBool ajStrKeepSetS(AjPStr* Pstr, const AjPStr str);

/* Removes all characters that are not alphabetic.
AjBool ajStrKeepSetAlpha(AjPStr* Pstr);

/* Removes all characters that are not alphabetic and are not in a given set. */
AjBool ajStrKeepSetAlphaC(AjPStr* Pstr, const char* txt);
```

# 6.5.11.4 String trimming functions

The string trim functions below will remove region(s) of a given character composition (provided in the string txt) from the start and/or end of a string:

```
/* Remove from start of a string */
AjBool ajStrTrimStartC (AjPStr* Pstr, const char* txt);

/* Remove from end of a string */
AjBool ajStrTrimEndC (AjPStr* Pstr, const char* txt);

/* Remove from start and end of a string */
AjBool ajStrTrimC (AjPStr* pthis, const char* txt);
```

All characters will be removed from the start and/or end up to the first character that is not in the set provided.

Similar functions are provided to remove regions composed of whitespace characters only from the start and end of a string.

```
/* Remove from start and end of a string. */
AjBool ajStrTrimWhite (AjPStr* Pstr);

/* Remove from start of a string. */
AjBool ajStrTrimWhiteStart (AjPStr* Pstr);

/* Remove from end of a string. */
AjBool ajStrTrimWhiteEnd (AjPStr* Pstr);
```

There are also two truncate functions which remove characters from the end of a string reducing it to a defined length (ajStrTruncateLen) or cut the end off a string at a defined position (ajStrTruncatePos):

```
/* Remove characters from end, reduce to defined length */
AjBool ajStrTruncateLen (AjPStr* Pstr, ajuint len);

/* Cut end of defined position */
AjBool ajStrTruncatePos (AjPStr* Pstr, ajint pos);
```