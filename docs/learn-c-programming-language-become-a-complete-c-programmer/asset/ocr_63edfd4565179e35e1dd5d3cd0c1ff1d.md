Clearly, mask reflects the traditional C and C++ classification (§36.2.1). However, for different character sets, different character values fall into different classes. For example, for the ASCII character set, the integer value 125 represents the character }, which is a punctuation character (punct). However, in the Danish national character set, 125 represents the vowel å, which in a Danish locale must be classified as an alpha.

The classification is called a “mask” because the traditional efficient implementation of character classification for small character sets is a table in which each entry holds bits representing the classification. For example:

```
table['P'] == upper|alpha
table['a'] == lower|alpha|xdigit
table['1'] == digit|xdigit
table[' '] == space|blank
```

Given that implementation, table[c]&m is nonzero if the character c is an m and 0 otherwise. The ctype facet is defined like this:

```
ctype<C> facet (§iso.22.4.1.1)
```

```
bool is(mask m, C c) const;
const C* is(const C* b, const C* e, mask* v) const;
const C* scan_is(mask m, const C* b, const C* e) const; const C* scan_not(mask m, const C* b, const C* e) const; C toupper(C c) const;
const C* toupper(C* b, const C* e) const;
C tolower(C c) const;
const C* tolower(C* b, const C* e) const;
C widen(C c) const;
const char* widen(const char* b, const char* e, C* b2) const; char narrow(C c, char def) const;
const C* narrow(const C* b, const C* e, char def, char* b2) const;
```

A call is(m,c) tests whether the character c belongs to the classification m. For example:

```
int count_spaces(const string& s, const locale& loc)
{
const ctype<char>& ct = use_facet<ctype<char>>(loc); int i = 0;
for(auto p = s.begin(); p!=s.end(); ++p)
if (ct.is(ctype_base::space,*p)) // whitespace as defined by ct
++i;
return i;
}
```

Note that it is also possible to use is() to check whether a character belongs to one of a number of classifications. For example:

```
ct.is(ctype_base::space|ctype_base::punct,c); // is c whitespace or punctuation in ct?
```

A call is(b,e,v) determines the classification of each character in [b:e) and places it in the corresponding position in the array v.

A call scan_is(m,b,e) returns a pointer to the first character in [b:e) that is an m. If no character is classified as an m, e is returned. As ever for standard facets, the public