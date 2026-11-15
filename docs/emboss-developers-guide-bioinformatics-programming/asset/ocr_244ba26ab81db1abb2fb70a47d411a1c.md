```
/*filesection ajstr ************************************************************************
**
** @nam1rule aj Function belongs to the AJAX library.
**
** @suffix Len [size_t] length
** @suffix C [char*] C character string
** @suffix S [AjPStr] string object
** @suffix K [char] single character
*/
```

```
/* @datasection [AjPStr] String ************************************************************************
**
** Functions for manipulating AJAX (AjPStr) strings
**
** @nam2rule Str Function is for manipulating strings
**
*/
```

```
/* @section comparison
**
** Functions for comparing strings
**
** @fdata [AjPStr]
**
** @nam3rule Match Compare two complete strings.
** @nam4rule MatchCase Case-insensitive comparison.
** @nam4rule MatchWild Comparison using wildcard characters.
** @nam5rule MatchWild Case Case-insensitive comparison
** using wildcard characters.
** @nam5rule MatchWildWord Case-sensitive wildcard comparison of
** first words within two strings.
** @nam6rule MatchWildWordCase Case-insensitive wildcard comparison of
** first words within two strings.
** @nam4rule MatchWord Comparison using whole words.
** @nam5rule MatchWordOne Comparison using whole words matching any one.
** @nam5rule MatchWordAll Comparison using whole words matching every one.
**
** @nam3rule Prefix Compare start of string to given prefix.
** @nam4rule Prefix Case Case-insensitive comparison.
** @nam3rule Suffix Compare end of string to given suffix.
** @nam4rule Suffix Case Case-insensitive comparison.
**
** @argrule * str [const AjPStr] String
** @argrule C txt2 [const char*] String
** @argrule S str2 [const AjPStr] String
**
** @valrule * [AjBool] True on success
**
** @fcategory use
**
*/
```

Prototypes of functions in the ‘comparison’ section are below:

```
AjBool ajStrMatchC (const AjPStr thys, const char* txt);
AjBool ajStrMatchS (const AjPStr thys, const AjPStr str);
AjBool ajStrMatchCaseC (const AjPStr thys, const char* text);
AjBool ajStrMatchCaseS (const AjPStr thys, const AjPStr str);
```