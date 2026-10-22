The character classifications in this library return true (nonzero) if the wide-character argument satisfies the conditions described by the function. In general, the wide-character function returns true if the corresponding ctype.h function returns true for the single-byte character corresponding to the wide character. Table RS.V.52 lists these functions.

# Table RS.V.52 Wide-Character Classification Functions

| Prototype | Description |
|---|---|
| int iswalnum(wint_t wc); | Returns true if wc represents an alphanumeric (alphabetic or numeric) character |
| int iswalpha(wint_t wc); | Returns true if wc represents an alphabetic character |
| int iswblank(wint_t wc); | Returns true if wc represents a blank |
| int iswcntrl(wint_t wc); | Returns true if wc represents a control character |
| int iswdigit(wint_t wc); | Returns true if wc represents a digit |
| int iswgraph(wint_t wc); | Returns true if iswprint(wc) is true and iswspace(wc) is false |
| int iswlower(wint_t wc); | Returns true if wc represents a lowercase character |
| int iswprint(wint_t wc); | Returns true if wc represents a printable character |
| int iswpunct(wint_t wc); | Returns true if wc represents a punctuation character |
| int iswspace(wint_t wc); | Returns true if wc represents a tab, space, or newline |
| int iswupper(wint_t wc); | Returns true if wc corresponds to a uppercase character |
| int iswxdigit(wint_t wc); | Returns true if wc represents a hexadecimal digit |

The library also includes two classification functions that are termed extensible because they use the LC_CTYPE value of the current locale to classify characters. Table RS.V.53 lists these functions.

# Table RS.V.53 Extensible Wide-Character Classification Functions

| Prototype | Description |
|---|---|
| int iswctype(wint_t wc, wctype_t desc); | Returns true if wc has the property described by desc. (See discussion in the accompanying text.) |
| wctype_t wctype(const char *property); | The wctype function constructs a value with type wctype_t that describes a class of wide characters identified by the string argument property. If the property identifies a valid class of wide characters according to the LC_CTYPE category of the current locale, the wctype() function returns a nonzero value that is valid as the second argument to the iswctype() function; otherwise, it returns zero. |