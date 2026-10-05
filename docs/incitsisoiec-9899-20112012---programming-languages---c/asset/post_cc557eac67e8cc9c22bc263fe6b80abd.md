
## 7.31.9 Boolean type and values <stdbool.h>

The undefined and potentially redefines makes bool, true, and false an obsolete feature.

## 7.31.10 Integer types <stdint.h>

Typedef names beginning with int and uint and ending with _t may be added to the types defined in the <stdint.h> header. Macro names beginning with INT, UINT and ending with _MAX, _MIN, or _C may be added to the macros defined in the <stdint.h> header.

## 7.31.11 Input/output <stdio.h>

Lowercase letters may be added to the conversion specifications and length modifiers in printf and fscanf. Other characters may be used in extensions.

The use of unget on a binary stream where the file position indicator is zero prior to the call is an obsolete feature.

## 7.31.12 General utilities <stdlib.h>

Function names beginning with str and a lowercase letter may be added to the declarations in <stdlib.h> header.

## 7.31.13 String handling <string.h>

Function names begin with str, mem, mem or wcs and a lowercase letter may be added to the declarations in the <string.h> header.

## 7.31.14 Date and time <time.h>

Macros beginning with TIME_ and an uppercase letter may be added to the macros in the <time.h> header.

## 7.31.15 Threads <threads.h>

Function names, types and enumeration constants that begin with either cnd_mtx_thrd_ or tss_ and a lowercase letter may be added to the declarations in the <threads.h> header.

## 7.31.16 Extended multibyte and wide character utilities <wchar.h>

Function names that begin with wcs and a lowercase letter may be added to the declarations in the <wchar.h> header.

Lowercase letters may be added to the conversion specifications and length modifiers in fprintf and fscanf. Other characters may be used in extensions.

## 7.31.17 Wide character classification and mapping utilities <wctype.h>

Function names that begin with **is** or **to** and a lowercase letter may be added to the declarations in the <wctype.h> header.

## Annex A
(informative)

## Language syntax summary

NOTE The notation is described in 6.1.

## A.1 Lexical grammar

### A.1.1 Lexical elements

(6.4) token:

- keyword
- identifier
- constant
- string-literal
- punctuator

(6.4) preprocessing-token:

- header-name
- identifier
- pp-number
- character-constant
- string-literal
- punctuator
- each non-white-space character that cannot be one of the above

### A.1.2 Keywords

(6.4.1) keyword: one of
auto if unsigned
break inline void
case int volatile
char long while
const register _Alignas
continue restrict _Alignof
default return _Atomic
do short _Bool
double signed _Complex
else sizeof _Generic
enum static _Imaginary
extern struct _Noreturn
float switch _Static_assert
for typedef _ _Thread_local
goto union

### A.1.3 Identifiers

(6.4.2.1) identifier:
identifier-nondigit
identifier-nondigit
identifier digit

(6.4.2.1) identifier-nondigit:
nondigit
univers-character-name
other implementation-defined characters

(6.4.2.1) nondigit: one of
a b c d e f g h i j k 1 m
n o p q r s t u v w x y z
A B C D E F G H I J K L M
N O P Q R S T U V W X Y Z

(6.4.2.1) digit: one of
0 1 2 3 4 5 6 7 8 9

### A.1.4 Universal character names

(6.4.3) universal-character-name:
\u hex-quad
\u hex-quad hex-quad

(6.4.3) hex-quad:
hexadecimal-digit hexadecimal-digit
hexadecimal-digit hexadecimal-digit

### A.1.5 Constants

(6.4.4) constant:
integer-constant
floating-constant
enumeration-constant
character-constant

(6.4.4.1) integer-constant:
decimal-constant integer-suffix_opt
octal-constant integer-suffix_opt
hexadecimal-constant integer-suffix_opt

(6.4.4.1) decimal-constant:
nonzero-digit
decimal-constant digit

(6.4.4.1) octal-constant:
0
octal-constant octal-digit

(6.4.4.1) hexadecimal-constant:
hexadecimal-prefix hexadecimal-digit
hexadecimal-constant hexadecimal-digit

(6.4.4.1) hexadecimal-prefix: one of
0x 0X

(6.4.4.1) nonzero-digit: one of
1 2 3 4 5 6 7 8 9

(6.4.4.1) octal-digit: one of
0 1 2 3 4 5 6 7

(6.4.4.1) hexadecimal-decimal: one of
0 1 2 3 4 5 6 7 8 9
a b c d e f
A C D E F

(6.4.4.1) integer-suffix:
unsigned-suffix long-suffix_opt
unsigned-suffix long-long-suffix
long-suffix unsigned-suffix_opt
long-long-suffix unsigned-suffix_opt

(6.4.4.1) unsigned-suffix: one of
u U

(6.4.4.1) long-suffix: one of
1 L

(6.4.4.1) long-long-suffix: one of
1 LL

(6.4.4.2) floating-constant:
decimal-floating-constant
hexadecimal-floating-constant

(6.4.4.2) decimal-floating-constant:
fractional-constant exponent-part_opt
digit-sequence exponent-part floating-suffix_opt

(6.4.4.2) hexadecimal-constant:
hexadecimal-prefix hexadecimal-fractional-constant
binary-exponent-part floating-suffix_opt
hexadecimal-prefix hexadecimal-digit-sequence
binary-exponent-part floating-suffix_opt

(6.4.4.2) fractional-constant:
digit-sequence_opt digit-sequence

(6.4.4.2) exponent-part:
e sign_opt digit-sequence
E sign_opt digit-sequence

(6.4.4.2) sign: one of
+ -

(6.4.4.2) digit-sequence:
digit
digit-sequence

(6.4.4.2) hexadecimal-fractional-constant:
hexadecimal-digit-sequence_opt
hexadecimal-digit-sequence
hexadecimal-digit-sequence .

(6.4.4.2) binary-exponent-part:
P sign_opt digit-sequence
P sign_opt digit-sequence

(6.4.4.2) hexadecimal-digit-sequence:
hexadecimal-digit
hexadecimal-digit hexadecimal-digit

(6.4.4.2) floating-suffix: one of
f 1 F

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
the-quote ', backslash \ or new-line character
escape-sequence

(6.4.4.4) escape-sequence:
simple-escape-sequence
octal-escape-sequence
hexadecimal-escape-sequence
universal-character-name

(6.4.4.4) simple-escape-sequence: one of
\' \" ? \\
a \b \f \n \r \v

(6.4.4.4) octal-escape-sequence:
\ octal-digit
\ octal-digit octal-digit
\ octal-digit octal-digit octal-digit

(6.4.4.4) hexadecimal-escape-sequence:
\x hexadecimal-digit
hexadecimal-escape-sequence hexadecimal-digit

### A.1.6 String literals

(6.4.5) string-literal:
encoding-prefix_opt " s-char-sequence_opt "

(6.4.5) encoding-prefix:
u8
uu
uU
l

(6.4.5) s-char-sequence:
s-char
s-char-sequence s-char

(6.4.5) s-char:
any member of the source character set except
double-quote ", backslash \ or new-line character
escape-sequence

### A.1.7 Punctuators

(6.4.6) punctuator: one of
[ ] ) { } . ->
++ & * + ~ !
/ << >> < <= != = | &&
? ; i
*= /= -= += << >= &= ^= = |
' # #
<: : > % 8 : % ::

### A.1.8 Header names

(6.4.7) header-name:
< h-char-sequence>
" q-char-sequence "

(6.4.7) h-char-sequence:
h-char
h-char-sequence h-char

(6.4.7) h-char:
any member of the source character set except the new-line character and >

(6.4.7) q-char-sequence:
q-char
q-char-sequence q-char

(6.4.7) q-char:
any member of the source character set except the new-line character and "

### A.1.9 Preprocessing numbers

(6.4.8) pp-number:
digit
pp-number digit
dpp-number identifier-nondigit
pp-number e sign
pp-number E sign
pp-number p sign
pp-number P sign
pp-number .

## A.2 Phrase structure grammar

## A.2.1 Expressions

(6.5.1) primary-expression:
identifier
constant
string-literal
( expression )
generic-selection

(6.5.1.1) generic-selection:
_Generic ( assignment-expression , generic-assoc-list )

(6.5.1.1) generic-assoc-list:
generic-association
generic-assoc-list , generic-association

(6.5.1.1) generic-association:
type-name : assignment-expression
default : assignment-expression

(6.5.2) postfix-expression:
primary-expression
postfix-expression [ expression ]
postfix-expression ( argument-expression-list_opt )
postfix-expression . identifier
postfix-expression ++
postfix-expression --
( type-name ) { initializer-list }
( type-name ) { initializer-list , }

(6.5.2) argument-expression-list:
assignment-expression
argument-expression-list , assignment-expression

(6.5.3) unary-expression:
postfix-expression
++ unary-expression
-- unary-expression
unary-operator cast-expression
sizeof unary-expression
sizeof ( type-name )
_Alignof ( type-name )
