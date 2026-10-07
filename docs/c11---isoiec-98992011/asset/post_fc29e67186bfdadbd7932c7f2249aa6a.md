
# ISO/IEC 9899:2011 (E)

"a" "b" "L"c"
"a" "L"b" "c"
L"a" "b" "L"c"
L"a" "L"b" "L"c"

Likewise, each of the sequences
"a" "b" "u"c"
"a" "u"b" "c"
u"a" "b" "u"c"
"u" "u"b" "u"c"

is equivalent to
uuabcabc

**Forward references:** common definitions `<stddef.h>` (7.19), the **mbstowcs** function (72.2.8.1), Unicode units in `<uchar.h>` (7.28).

# 6.4.6 Punctuators

## Syntax

- punctuator: one of
[ ] ( ) { } . ->
++ / & * + ~ !
/ % << >> > <= == != ^ && ||
? ;
* = / % += - <= >= &= = | |
# ##
< : > % % % : % ::

## Semantics

- A punctuator is a symbol that has syntactic and semantic significance. Depending on context, it may specify an operation to be performed (which in turn may yield a value or a function designator, produce a side effect, or some combination thereof) in which case it is known as an *operator* (other forms of operator also exist in some contexts). An *operand* is an entity on which an operator acts.

In all aspects of the language, the six tokens^{79}

< : > % % : % %>:
behave, respectively, the same as the six tokens

[ ] { } # ##
except for their spelling.${80}

**Forward references:** expressions (6.5), declarations (6.7), preprocessing directives (6.10), (statements) (6.8).

# 6.4.7 Header names

## Syntax

```
header-name:
< h-char-sequence>
" q-char-sequence "
nh-char-sequence:
h-char
h-char-sequence h-char
h-char:
any member of the source character set except
the new-line character and >
q-char-sequence:
q-char
q-char-sequence q-char
q-char:
any member of the source character set except
the new-line character and "
```

The sequences in both forms of header names are mapped in an implementation-defined manner to headers or external source files as specified in 6.10.2.

If the characters ' ', '\', '/', '/', or * occur in the sequence between the < > delimiters, the behavior is undefined. Similarly, if the characters ' ', '\', '/', '/', or * occur in the sequence between the " delimiters, the behavior is undefined.81) Header name preprocessing tokens are recognized only within #include preprocessing directives and in implementation-defined locations within #pragma directives.82)

> 79) These tokens are sometimes called "digraphs".

> 80) Thus [ and <: behave differently when "stringized" (see 6.10.3.2), but can otherwise be freely interchangeable.

EXAMPLE The following sequence of characters:

```
0x3</1/a.h-1e2
#include <1/s.h>
#define const.member@
```

forms the sequence of preprocessing tokens (with each individual preprocessing directive delimited by a / on left and a / on right).

Forward references: source file inclusion (6.10.2).

# 6.4.8 Preprocessing numbers

## Syntax

- pp-number:
  digit
  . digit
  pp-number digit
  pp-number identifier-nondigit
  pp-number e sign
  pp-number E sign
  pp-number p sign
  pp-number P sign
  pp-number .

## Description

A preprocessing number begins with a digit optionally preceded by a period (.), and may be followed by valid identifier characters and the sequence e+, e-, E+, E-, p+, p-, P+, or P-.

Preprocessing numbers lexically include all floating and integer constant tokens.

## Semantics

A preprocessing number does not have type or a value; it acquires both after a successful conversion (as of translation phase 7) to a floating constant or integer token.

> 81) Thus, sequences of characters that resemble escape sequences cause undefined behavior.

> 82) For an example of a header name token using a #pragma directive, see 6.10.9.

# 6.4.9 Comments

Except within a character constant, a string literal, or a comment, the characters /* introduce a comment. The contents of such a comment are examined only to identify multibyte characters and to find the characters */ to terminate it.^{83}

Except within a character constant, a string literal, or a comment, the characters // introduce a comment that includes all multibyte characters up to, but not including, the next new-line character. The contents of such a comment are examined only to identify the multibyte characters and to find the terminating new-line character.

EXAMPLE
```c
"a/b"                   // four-character string literal
#include "//"         // undefined behavior
//*                      // comment, not syntax
f = g*/h;               // equivalent to g / h;
i();                    // part of two-line comment
/\                      // part of two-line comment
#define glue(x,y) ##y k());     // syntax error, not comment
/**/* 1();               // equivalent to 1();
m = n*/o               // equivalent to n + p;
+ p;
```

> 83) Thus, /* */ comments do not nest.

# 6.5 Expressions

An expression is a sequence of operators and operands that specifies computation of a value, or that designates an object or a function, or that generates side effects, and that performs a combination thereof. The value computations of the operands of an operator are sequenced before the value computation of the result of the operator. If a side effect on a scalar object is unsequenced relative to either a different side effect on the same object or a value computation using the same object, the behavior is undefined. If there are multiple orderings of the subexpressions of an expression, the behavior is undefined if such an unsequenced side effect occurs in any of the orderings.84) The grouping of operands is defined by the syntax.85) Except as specified later, side effects and value computations of subexpressions are unsequenced.86) In an expression that is evaluated more than once during the execution of the program, unsequenced and independently determined evaluations of its subexpressions need not be performed consistently in different environments.

The highest precedence first. Thus, for example, the expressions allowed as operands of the binary + (6.5.6) are those defined in 6.5.1 through 6.5.6. The exceptions are cast expressions (6.5.4) as operands of unary operators (6.5.3), and an operand contained between any of the following pairs of operands: grouping parentheses (6.5.1), structured brackets [] (6.5.2.1), function-call parentheses () (6.5.2), and the conditional operator ? : (6.5.15). Within each clause, the operators have the same precedence. Left- or right-associativity is indicated in each clause by the syntax for the expressions discussed

The effective type of an object for an access to its stored value is the declared type of the object, if any.(87) If a value is stored into an object having no declared type through an lvalue having a type that is not a character type, the type of the lvalue becomes the effective type of the object for that access and for subsequent accesses that do not modify the stored value. If a value is copied into an object having no declared type using memcpy or memmove, or is copied as an array of character type, the effective type of the modified object for access and for subsequent accesses that do not modify the value is the effective type of the object from which the value is copied, if it has one. For all other accesses to an object having no declared type, the effective type of the object is simply the type of the lvalue used for the access.

An object has its stored value accessed only by lvalue expression that has one of the following types:(88)

- a compatible type with the effective type of the object,
- a qualified version of a type compatible with the effective type of the object,
- a type that is the signed or unsigned type corresponding to the effective type of the object,
- a type that is the signed or unsigned type corresponding to a qualified version of the type of the object,
- an aggregate or union type that includes one of the aforementioned types among its members (including, recursively, a member of a subaggregate or contained union), or
- a character type.

A floating expression is contracted, that is, evaluated as though it were a single operation, thereby omitting rounding errors implied by the source code and the expression evaluation method.(89) The FP_CONTRACT pragma in <math.h> provides a way to disable contracted expressions. Otherwise whether or how expressions are contracted implementation-defined.(90)

**Forward references:** the FP_CONTRACT pragma (7.12.2), copying functions (7.24.2).

> 87) Allocated objects have no declared type.

> 88) The intent of this list is specify those circumstances in which an object may or may not be aliased.

> 89) The intermediate operations in the contracted expression are evaluated as if in infinite range and precision, while the final operation is rounded to the format determined by the expression evaluation method. A contracted expression.

> 90) This license is specifically intended to allow implementations to exploit fast machine instructions that combine C operators. As contractions potentially undermine predictability, and can even decrease accuracy for containing expressions, their use needs to be well-defined and clearly documented.
