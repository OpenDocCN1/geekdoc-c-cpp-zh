Note: Hence, the literal 2.900m will be parsed to form the decimal with sign 0, coefficient 2900, and scale 3. end note

If the magnitude of the specified literal is too large to be represented in the indicated type, a compile-time error occurs.

Note: In particular, a Real_Literal will never produce a floating-point infinity. A non-zero Real_Literal may, however, be rounded to zero. end note

The value of a real literal of type float or double is determined by using the IEC 60559 "round to nearest" mode with ties broken to "even" (a value with the least-significant-bit zero), and all digits considered significant.

Note: In a real literal, decimal digits are always required after the decimal point. For example, 1.3F is a real literal but 1.F is not. end note

# 6.4.5.5 Character literals

A character literal represents a single character, and consists of a character in quotes, as in 'a'.

```
Character_Literal
    : '\'' Character '\''
    ;

fragment Character
    : Single_Character
    | Simple_Escape_Sequence
    | Hexadecimal_Escape_Sequence
    | Unicode_Escape_Sequence
    ;

fragment Single_Character
    : ~['\\'\u000D\u000A\u0085\u2028\u2029]    // anything but ', \, and
New_Line_Character
    ;

fragment Simple_Escape_Sequence
    : '\\''' | '\\"' | '\\\\' | '\\0' | '\\a' | '\\b' | '\\f' | '\\n' | '\\r' |
    '\\t' | '\\v'
    ;

fragment Hexadecimal_Escape_Sequence
    : '\\x' Hex_Digit Hex_Digit? Hex_Digit? Hex_Digit?
    ;
```

Note: A character that follows a backslash character (\ ) in a Character must be one of the following characters: ', ", \, 0, a, b, f, n, r, t, u, U, x, v. Otherwise, a compile-time error occurs. end note

Note: The use of the \x Hexadecimal_Escape_Sequence production can be error-prone and hard to read due to the variable number of hexadecimal digits following the \x. For example, in the code:
string good = "\x9Good text";
string bad = "\x9Bad text";
it might appear at first that the leading character is the same (U+0009, a tab character) in both strings. In fact the second string starts with U+9BAD as all three letters in the word “Bad” are valid hexadecimal digits. As a matter of style, it is recommended that \x is avoided in favour of either specific escape sequences (\t in this example) or the fixed-length \u escape sequence.