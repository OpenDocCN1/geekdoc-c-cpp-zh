# identifier-start-character:

+   - letter-character
+   - _ (the underscore character U+005F)

# identifier-part-characters:

+   - identifier-part-character
+   - identifier-part-characters identifier-part-character

# identifier-part-character:

+   - letter-character
+   - decimal-digit-character
+   - connecting-character
+   - combining-character
+   - formatting-character

# letter-character:

A Unicode character of classes Lu, Ll, Lt, Lm, Lo, or Nl
A unicode-escape-sequence representing a character of classes Lu, Ll, Lt, Lm, Lo, or Nl

# combining-character:

A Unicode character of classes Mn or Mc
A unicode-escape-sequence representing a character of classes Mn or Mc

# decimal-digit-character:

A Unicode character of the class Nd
A unicode-escape-sequence representing a character of the class Nd

connecting-character:
A Unicode character of the class Pc
A unicode-escape-sequence representing a character of the class Pc

formatting-character:
A Unicode character of the class Cf
A unicode-escape-sequence representing a character of the class Cf

For information on the Unicode character classes mentioned above, see The Unicode Standard, Version 3.0, section 4.5.

Examples of valid identifiers include “identifier1”, “_identifier2”, and “@if”.

An identifier in a conforming program must be in the canonical format defined by Unicode Normalization Form C, as defined by Unicode Standard Annex 15. The behavior when encountering an identifier not in Normalization Form C is implementation-defined; however, a diagnostic is not required.