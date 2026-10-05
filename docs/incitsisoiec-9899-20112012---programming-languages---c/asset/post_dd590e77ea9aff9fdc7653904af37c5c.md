
## 6.4.4.3 Enumeration constants

### Syntax

```
enumeration-constant:
    identifier
```

### Semantics

An identifier declared as an enumeration constant has type int.

Forward references: enumeration qualifiers (6.7.2.2).

## 6.4.4.4 Character constants

### Syntax

```
character-constant:
    ' c-char-sequence '
    'L c-char-sequence '
    'u c-char-sequence '
    'U c-char-sequence '
```

```
c-char-sequence:
    c-char
    c-char-sequence c-char
```

```
c-char:
    any member of the source character set except
    the single-quote ', backslash \, or new-line character
    escape-sequence
```

```
escape-sequence:
    simple-escape-sequence
    octal-escape-sequence
    hexadecimal-escape-sequence
    universal-character-name
```

```
simple-escape-sequence: one of
    \' \? \\
    \a \b \e \n \r \v
```

```
octal-escape-sequence:
    \octal-digit
    \octal-digit octal-digit
    \octal-digit octal-digit octal-digit
```

```
hexadecimal-escape-sequence:
\x hexadecimal-digit
hexadecimal-escape-sequence hexadecimal-digit
```

### Description

An integer constant is a sequence of one or more multibyte characters enclosed in single-quotes, as in '\x'. A wide character constant is the same, except prefixed by the letter L, u, or U. With a few exceptions detailed later, the elements of the sequence are any members of the source character set; they are mapped in an implementation-defined manner to members of the execution character set.

The single-quote ', the double-quote ", the question-mark ?, the backslash \, and arbitrary integer values are representable according to the following table of escape sequences:

- single quote ' \'
- double quote " \"
- question mark ? \?
- backslash \\
- octal character \octal digits
- hexadecimal character \x hexadecimal digits

The double-quote " and question-mark ? are representable either by themselves or by the escape sequences " and ?, respectively, but the single-quote ' and the backslash \ shall be represented, respectively, by the escape sequences \' and '\'.

The octal digits that follow the backslash in an octal escape sequence are taken to be part of the construction of a single character for an integer constant or of a single wide character for a wide character constant. The numerical value of the octal integer so formed specifies the value of the desired character or wide character.

The hexadecimal digits that follow the backslash and the letter x in a hexadecimal escape sequence are taken to be part of the construction of a single character for an integer character constant or of a single wide character for a wide character constant. The numerical value of the hexadecimal integer so formed specifies the value of the desired character or wide character.

Each octal or hexadecimal escape sequence is the longest sequence of characters that can constitute the escape sequence.

In addition, characters not in the basic character set are representable by universal character names and certain nongographic characters are representable by escape sequences consisting of the backslash \ followed by a lowercase letter: \a, \b, \f, \n, \r, \t, and \v. (77)

### Constraints

The value of an octal or hexadecimal escape sequence shall be in the range of representable values for the corresponding type:

| Prefix | Corresponding Type |
|---|---|
| none | unsigned char |
| L | the unsigned type corresponding to char_t |
| u | char16_t |
| U | char32_t |

### Semantics

An integer character constant has type int. The value of an integer character constant containing a single character that maps to a single-byte character is the numerical value of the representation of the mapped character interpreted as an integer. The value of an integer character constant containing more than one character (e.g., '\ab\'), or containing a character or escape sequence that does not map to a single-byte execution character, is implementation-defined. If an integer character constant contains a single character or escape sequence, its value is the one that results when an object with type char value that is of the single character or escape sequence is converted to int.

A wide character constant prefixed by the L has type char_t, an integer type defined in the <stddef.h> header; a wide character constant prefixed by the u or U has type char16_t or char32_t, respectively, unsigned integer types defined in the <uchar.h> header. The value of a wide character constant containing a multibyte character that maps to a single member of the extended execution character set is the wide character corresponding to that multibyte character, as defined by mbtowc, mbrtoc16, or mbrtoc32 as appropriate for its type, with an implementation-defined current locale. The value of a wide character constant containing more than one multibyte character or a single multibyte character that maps to multiple members of the extended execution character set, or containing a multibyte character or escape sequence not represented in the extended execution character set, is implementation-defined.

EXAMPLE 1 The construction '\0' is commonly used to represent the null character.

EXAMPLE 2 Consider implementations that use two's complement representation for integers and eight bits for objects that have type char. In an implementation where type char has the same range of values as signed char, the integer constant '\xff' has the value -1; if type char has the same range of values as unsigned char, the character constant '\xff' has the value +255.

77) The semantics of these characters were discussed in 5.2.2. If any other character follows a backslash, the result is not a token and a diagnostic is required. See "future language directions" (6.11.4).

EXAMPLE 3 Even eight bits are used for objects that have type char, the construction '\x123' specifies an integer character constant containing only one character, since a hexadecimal sequence is terminated by a non-hexadecimal character. To specify an integer character constant containing two characters values are '\x12' and '3', the construction '\0223' may be used, as an octal sequence is terminated after three octal digits. (The value of this two-character integer constant is implementation-defined).

EXAMPLE 4 Even twelve or more bits are used for objects that type wchar_t, the construction '\x123' specifies an integer character constant containing only one character, since a hexadecimal sequence is terminated by a non-hexadecimal character. To specify an integer character constant containing two characters values are '\x12' and '3', the construction '\0223' may be used, as an octal sequence is terminated after three octal digits. (The value of this two-character integer constant is implementation-defined).

## 6.4.5 String literals

### Syntax

```
string-literal:
  encoding-prefix_opt s-char-sequence_opt
encoding-prefix:
    u8
    u
    U
    L
s-char-sequence:
    s-char
s-char:
    any member of the source character set except
    the double-quote ", backslash \, or new-line character
```

### Constraints

A sequence of adjacent string literal shall not include both a wide string literal.

### Description

A character literal is a sequence of one or more multibyte characters enclosed in double-quotes, as in "xyz". A UTF-8 string literal is the same, prefixed by u8. A wide string literal is the same, prefixed by the letter L.

### Semantics

In translation phase 6, the multibyte character sequences and identically-prefixed string literal are concatenated into a single multibyte character sequence. If any of the tokens have an encoding prefix, the resulting multibyte character sequence is treated as having the same prefix; otherwise, it is treated as character literal. Whether differently-prefixed wide string literal can be concatenated and, if so, the treatment of the resulting multibyte character sequence is implementation-defined.

In translation phase 7, a byte or code of value zero is appended to each multibyte character sequence that results from a string literal. The multibyte sequence is then used to initialize an array of static duration and length sufficient to contain the sequence. For character literals, the array elements have initialized with the individual bytes of the multibyte character sequence. For UTF-8 string literals, the array elements have type char, and are initialized with the characters of the multibyte character sequence, as encoded in UTF-8. For wide string literals prefixed by the letter L, the array elements have type wchar_t and are initialized with the sequence of wide characters corresponding to the multibyte character sequence, as defined by the mbtowcs function <stdlib.h> (7.1) with an implementation-defined locale. For wide string literals prefixed by the letter u or U, the array elements have type char16_t or char32_t, respectively, and are initialized with the sequence of wide characters corresponding to the multibyte character sequence, as defined by successive calls to the mbrftoc16, or mbrftoc32 function as appropriate for its type, with an implementation-defined locale.

EXAMPLE 1 This pair of adjacent character string literals

```
\x12" "3"
```

produces a single character literal containing the two characters whose values are '\x12' and '3', because escape sequences are converted into single members of the execution character set just prior to adjacent string literal concatenation.

78) A string literal need not be a string (see 7.1.1), because a null character may be embedded in it by a \0 escape sequence.
