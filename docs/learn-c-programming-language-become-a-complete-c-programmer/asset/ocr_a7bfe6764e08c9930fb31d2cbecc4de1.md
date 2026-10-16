A UTF-8 string is terminated by ‘\0’, a UTF-16 string by u‘\0’, and a UTF-32 string by U‘\0’. We can represent an ordinary English character string in a variety of ways. Consider a file name using a backslash as the separator:

```
“folder\ file” // implementation character set string
R”(folder\file)” // implementation character rawset string
u8”folder\file” // UTF-8 string
u8R”(folder\file)” // UTF-8 rawstring
u”folder\file” // UTF-16 string
uR”(folder\file)” // UTF-16 rawstring
U”folder\file” // UTF-32 string
UR”(folder\file)” // UTF-32 rawstring
```

If printed, these strings will all look the same, but except for the “plain” and UTF-8 strings their internal representations are likely to differ.
Obviously, the real purpose of Unicode strings is to be able to put Unicode characters into them. For example:

```
u8”The official vowels in Danish are: a, e, i, o, u, \u00E6, \u00F8, \u00E5 and y.”
```

Printing that string appropriately gives you

```
The official vowels in Danish are: a, e, i, o, u, æ, ø, å and y.
```

The hexadecimal number after the \u is a Unicode code point (§iso.2.14.3) [Unicode,1996]. Such a code point is independent of the encoding used and will in fact have different representations (as bits in bytes) in different encodings. For example, u‘0430’ (Cyrillic lowercase letter “a”) is the 2-byte hexadecimal value D0B0 in UTF-8, the 2-byte hexadecimal value 0403 in UTF-16, and the 4-byte hexadecimal value 00000403 in UTF-32. These hexadecimal values are referred to as universal character names.

The order of the us and Rs and their cases are significant: RU and Ur are not valid string prefixes.

# 7.4 Pointers into Arrays

In C++, pointers and arrays are closely related. The name of an array can be used as a pointer to its initial element. For example:

```
int v[] = { 1, 2, 3, 4 };
int* p1 = v; // pointer to initial element (implicit conversion) int* p2 = &v[0]; // pointer to initial element
int* p3 = v+4; // pointer to one-beyond-last element
```

or graphically:

```
p1 p2 p3
v: 1 2 3 4
```

Taking a pointer to the element one beyond the end of an array is guaranteed to work. This is important for many algorithms (§4.5, §33.1). However, since such a pointer does not in fact point to an element of the array, it may not be used for reading or writing. The result of taking the address of the element before the initial element or beyond one-past-the-last