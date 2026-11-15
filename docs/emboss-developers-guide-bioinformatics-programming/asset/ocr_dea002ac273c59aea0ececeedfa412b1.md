```
/*
AjBool ajStrToHex (const AjPStr str, ajint* Pval); /* To hexadecimal
*/
AjBool ajStrToInt (const AjPStr str, ajint* Pval); /* To integer
*/
AjBool ajStrToLong (const AjPStr thys, ajlong* result); /* To long
*/
AjBool ajStrToUint (const AjPStr str, ajuint* Pval); /* To unsigned integer
*/
```

In all cases, the functions return ajTrue if the conversion was performed successfully. They take the address of a variable of the appropriate type. For example, to convert a string to an integer value:

```
ajint val = 0;
AjPStr str = NULL;

str = ajStrNewC("10");

if(!ajStrToInt(str, &val))
    ajFatal("This error message will not be printed.");

ajStrDel(&str);
```

Conversely, the C datatypes can be converted to an EMBOSS string using the following:

```
AjBool ajStrFromBool (AjPStr* Pstr, AjBool val); /*
From double
*/
AjBool ajStrFromDouble (AjPStr* Pstr, double val, ajint precision); /*
From double
*/
AjBool ajStrFromDoubleExp (AjPStr* Pstr, double val, ajint precision); /*
From double in exponential form. */
AjBool ajStrFromFloat (AjPStr* Pstr, float val, ajint precision);
/*
From float
*/
AjBool ajStrFromInt (AjPStr* Pstr, ajint val);
/*
From integer
*/
AjBool ajStrFromLong (AjPStr* Pstr, ajlong val);
/*
From long
*/
AjBool ajStrFromUint (AjPStr* Pstr, ajuint val);
/*
From unsigned integer
*/
```

Again, these functions return ajTrue if the conversion was performed successfully, and take the address of a string. For example, to convert an integer to a string:

```
ajint val = 0;
AjPStr str = NULL;

str = ajStrNew();
val = 100;

if(!ajStrFromInt(&str, val))
    ajFatal("This error message will not be printed.");

ajStrDel(&str);
```