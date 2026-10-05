(6.4.4.2) digit-sequence:
digit
digit-sequence digit

(6.4.4.2) hexadecimal-fractional-constant:
hexadecimal-digit-sequence_opt .
hexadecimal-digit-sequence
hexadecimal-digit-sequence .

(6.4.4.2) binary-exponent-part:
P sign_opt digit-sequence
P sign_opt digit-sequence

(6.4.4.2) hexadecimal-digit-sequence:
hexadecimal-digit
hexadecimal-digit hexadecimal-digit

(6.4.4.2) floating-suffix: one of
f 1 F L

(6.4.4.3) enumeration-constant:
identifier

(6.4.4.4) character-constant:
' c-char-sequence '
L' c-char-sequence '
uU' c-char-sequence '
U' c-char-sequence '

(6.4.4.4) c-char-sequence:
c-char
c-char-sequence c-char

(6.4.4.4) c-char:
any member of the source character set except
the single-quote ', backslash \, or new-line character
escape-sequence

(6.4.4.4) escape-sequence:
simple-escape-sequence
octal-escape-sequence
hexadecimal-escape-sequence
universal-character-name