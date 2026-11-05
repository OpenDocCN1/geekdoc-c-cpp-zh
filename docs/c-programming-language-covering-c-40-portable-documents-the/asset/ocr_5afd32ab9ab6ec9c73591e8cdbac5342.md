# B.1.8 Literals

```
literal:
  boolean-literal
  integer-literal
  real-literal
  character-literal
  string-literal
  null-literal

boolean-literal:
  true
  false

integer-literal:
  decimal-integer-literal
  hexadecimal-integer-literal

decimal-integer-literal:
  decimal-digits integer-type-suffix_opt

decimal-digits:
  decimal-digit
  decimal-digits decimal-digit

decimal-digit: one of
  0 1 2 3 4 5 6 7 8 9

integer-type-suffix: one of
  U u L l UL U1 uL u1 LU Lu 1U 1u

hexadecimal-integer-literal:
  0x hex-digits integer-type-suffix_opt
  0X hex-digits integer-type-suffix_opt

hex-digits:
  hex-digit
  hex-digits hex-digit

hex-digit: one of
  0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f
```