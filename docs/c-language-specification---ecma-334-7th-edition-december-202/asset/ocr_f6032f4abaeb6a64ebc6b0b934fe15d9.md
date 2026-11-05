```
```
fragment Letter_Character
// Category Letter, all subcategories; category Number, subcategory letter.
// [\p{L}]\p{Nl}]
// Only escapes for categories L & Nl allowed. See note below.
| Unicode_Escape_Sequence
;
```
```

```
```
fragment Combining_Character
// Category Mark, subcategories non-spacing and spacing combining.
// [\p{Mn}]\p{Mc}]
// Only escapes for categories Mn & Mc allowed. See note below.
| Unicode_Escape_Sequence
;
```
```

```
```
fragment Decimal_Digit_Character
// Category Number, subcategory decimal digit.
// [\p{Nd}]
// Only escapes for category Nd allowed. See note below.
| Unicode_Escape_Sequence
;
```
```

```
```
fragment Connecting_Character
// Category Punctuation, subcategory connector.
// [\p{Pc}]
// Only escapes for category Pc allowed. See note below.
| Unicode_Escape_Sequence
;
```
```

```
```
fragment Formatting_Character
// Category Other, subcategory format.
// [\p{Cf}]
// Only escapes for category Cf allowed, see note below.
| Unicode_Escape_Sequence
;
```
```

Note:

+   - For information on the Unicode character classes mentioned above, see *The Unicode Standard*.
+   - The fragment *Available_Identifier* requires the exclusion of keywords and contextual keywords. If the grammar in this specification is processed with ANTLR then this exclusion is handled automatically by the semantics of ANTLR:
+     - Keywords and contextual keywords occur in the grammar as literal strings.
+     - ANTLR creates implicit lexical token rules are created from these literal strings.
+     - ANTLR considers these implicit rules before the explicit lexical rules in the grammar.
+     - Therefore fragment *Available_Identifier* will not match keywords or contextual keywords as the lexical rules for those precede it.
+   - Fragment *Escaped_Identifier* includes escaped keywords and contextual keywords as they are part of the longer token starting with an @ and lexical processing always forms the longest possible lexical element (§6.3.1).