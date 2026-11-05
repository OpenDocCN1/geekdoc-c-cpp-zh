```
fragment Connecting_Character
// Category Punctuation, subcategory connector.
// [\p{Pc}]
// Only escapes for category Pc allowed. See note below.
| Unicode_Escape_Sequence
;
```

```
fragment Formatting_Character
// Category Other, subcategory format.
// [\p{Cf}]
// Only escapes for category Cf allowed, see note below.
| Unicode_Escape_Sequence
;
```

Note:

+   - For information on the Unicode character classes mentioned above, see *The Unicode Standard*.
+   - The fragment *Available_Identifier* requires the exclusion of keywords and contextual keywords. If the grammar in this Standard is processed with ANTLR then this exclusion is handled automatically by the semantics of ANTLR:
+     - Keywords and contextual keywords occur in the grammar as literal strings.
+     - ANTLR creates implicit lexical token rules are created from these literal strings.
+     - ANTLR considers these implicit rules before the explicit lexical rules in the grammar.
+     - Therefore fragment *Available_Identifier* will not match keywords or contextual keywords as the lexical rules for those precede it.
+   - Fragment *Escaped_Identifier* includes escaped keywords and contextual keywords as they are part of the longer token starting with an @ and lexical processing always forms the longest possible lexical element (§6.3.1).
+   - How an implementation enforces the restrictions on the allowable *Unicode_Escape_Sequence* values is an implementation issue.

end note

*Example:* Examples of valid identifiers are `identifier1`, `_identifier2`, and `@if`. end example

An identifier in a conforming program shall be in the canonical format defined by Unicode Normalization Form C, as defined by Unicode Standard Annex 15. The behavior when encountering an identifier not in Normalization Form C is implementation-defined; however, a diagnostic is not required.

The prefix "@" enables the use of keywords as identifiers, which is useful when interfacing with other programming languages. The character @ is not actually part of the identifier, so the identifier might be seen in other languages as a normal identifier, without the prefix. An identifier with an @ prefix is called a *verbatim identifier*.

*Note:* Use of the @ prefix for identifiers that are not keywords is permitted, but strongly discouraged as a matter of style. end note

*Example:* The example:

```
class @class
{
    public static void @static(bool @bool)
    {
```