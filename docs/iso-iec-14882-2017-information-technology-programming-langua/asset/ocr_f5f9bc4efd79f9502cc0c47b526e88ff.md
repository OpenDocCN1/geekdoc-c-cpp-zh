# ISO/IEC 14882:2017(E)

is that character whose short name in ISO/IEC 10646 is. If the hexadecimal value for a universal-character-name corresponds to a surrogate point (in the range 0xD800–0xDFFF, inclusive), the program is ill-formed. Additionally, if the hexadecimal value for a universal-character-name outside the c-character, s-character, or r-char-sequence of a character or string literal corresponds to a character (either in the range 0x00–0x1F or 0x7F–0x9F, both inclusive) or to a character in the source set, the program is ill-formed.

The basic character set and the basic execution wide-character set shall contain all the members of the basic character set, plus characters representing alert, backspace, and carriage return, plus the ill-formed character (whose value is 0). For each basic character set, the values of the members shall be non-negative and distinct from one another. In both the source and execution set, the value of each character after 0 in the above list of decimal digits shall be the same as the previous. The execution character set and the execution wide-character set are implementation-defined subsets of the basic character set and the basic wide-character set, respectively. The values of the members of the execution character sets and the sets of additional members are locale-specific.

# 5.4 Preprocessing tokens

```
preprocessing-token:
header-name
identifier
pp-number
character-literal
user-defined-character-literal
string-literal
user-defined-string-literal
preprocessing-op-or-unc
```

[lex.pptoken]

+   1 Each preprocessing token that is converted to a token (5.6) shall have the lexical form of a keyword, an identifier, a literal, or an operator.
2 A preprocessing token is the minimal lexical element of the language in translation phases 3 through 6. The categories of preprocessing include header names, identifiers, preprocessing numbers, character literals (including user-defined character literals), string literals (including user-defined string literals), operators and punctuators. If a ' ' or a '+' character matches the last category, the behavior is undefined. Preprocessing tokens can be separated by white space; this consists of (5.7), or white-space categories (space, tab, new-line, vertical tab, and form-feed). As described in Clause 19, in certain circumstances during translation phase 4, white serves as more than preprocessing token. White space can appear within a preprocessing token only as part of a header name or between characters in a character or string literal.
3 If the stream has been parsed into preprocessing tokens to give a given character

If the next character is a sequence of characters that would be the prefix and initial double quote of a raw string literal, the next preprocessing token shall be a raw string literal. Between the initial and final double quote characters of the raw string, any transformations performed in phases 1 and 2 (universal-character-names and line splicing) are reverted; d-char, r-char, or delimiting-names are also reverted; The raw string is defined as the shortest sequence of characters that matches the string-pattern

```
encoding-fix-utf R-string
```

> — A sequence of characters resembling a universal-character-name in an r-char-sequence (5.13.5) does not form a universal-character-name.