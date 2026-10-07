
7 A pointer to an object type may be converted to a pointer to a different object type. If the resulting pointer is not correctly aligned(58) for the referenced type, the behavior is undefined. Otherwise, when converted back again, the result shall compare equal to the original pointer. When a pointer to an object is converted to a pointer to a character type, the result points to the lowest addressed byte of the object. Successive increments of the result, up to the size of the object, yield pointers to the remaining bytes of the object.

8 A pointer to a function of one type may be converted to a pointer to a function of another type and back again; the result shall compare equal to the original pointer. If a converted pointer is used to call a function whose type is not compatible with the referenced type, the behavior is undefined.

Forward references: cast operators (6.5.4), equality operators (6.5.9), integer types capable of holding object pointers (7.20.1.4), simple assignment (6.5.16.1).

68 In general, the concept “correctly aligned” is transitive: if a pointer to type A is correctly aligned for a pointer to type B, which in turn is correctly aligned for a pointer to type C, then a pointer to type A is correctly aligned for a pointer to type C.

## 6.4 Lexical elements

### Syntax

+ token:
- keyword
- identifier
- constant
- string-literal
- punctuator
- preprocessing-token:
- header-name
- identifier
- pp-number
- character-constant
- string-literal
- punctuator
- each non-white-space character that cannot be one of the above

### Constraints

Each preprocessing token that is converted to a token shall have the lexical form of a keyword, an identifier, a constant, a string literal, or a punctuator.

### Semantics

A token is the minimal lexical element of the language in translation phases 7 and 8. The categories of tokens are: keywords, identifiers, constants, string literals, and punctuators. A preprocessing token is the minimal lexical element of the language in translation phases 3 through 6. The categories of preprocessing tokens are: header names, identifiers, preprocessing numbers, character constants, string literals, punctuators, and single non-white-space characters that do not lexically match the other preprocessing token categories.(69) If a ' or a " matches the last category, the behavior is undefined. Preprocessing tokens can be separated by white space; this consists of comments (described later), or white-space characters (space, horizontal tab, new-line, vertical tab, and form-feed), or both. As described in 6.10, in certain circumstances during translation phase 4, white space (or the absence thereof) serves as more than a preprocessing token separation. White space may appear as part of a header name or between the quotation characters in a character constant or string literal.

> (69) An additional category, placemarkers, is used internally in translation phase 4 (see 6.10.3.3); it cannot occur in source files.

# ISO/IEC 9899:2011 (E) © ISO/IEC 2011 – All rights reserved

4 If the input stream has been parsed into preprocessing tokens to a given character, the next preprocessing token is the longest sequence of characters that could constitute a preprocessing token. There is one exception to this rule: header name preprocessing tokens are recognized only within #include preprocessing directives and in implementation-defined locations within #pragma directives. In such contexts, a sequence of characters that could be either a header name or a string literal is recognized as the former.

5 EXAMPLE 1 The program fragment 1 is parsed as a preprocessing number 1 even though the pair of preprocessing tokens 1 and Ex might produce a value expression (for example, if Ex a macro defined as +1). Similarly, the program fragment I1 is parsed as a preprocessing number (one is a valid floating constant), whether not E is a macro name.

6 EXAMPLE 2 The program fragment x++++y is parsed as x + + + + + y, which violates a constraint on increment operators, even though x + + + + y might yield a correct expression.

Forward references: character constants (6.4.4), comments (6.4.9), expressions (6.4.5), floating constants (6.4.4.2), header names (6.4.7), macro replacement (6.10.3), postfix increment and decrement operators (6.5.2.4), prefix increment and decrement operators (6.5.3.1), preprocessing directives (6.10), preprocessing numbers (6.4.8), string literals (6.4.5).

## 6.4.1 Keywords

Syntax keyword: one of

```
auto unsigned
break inline
case void
int volatile
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
for typedef _Thread_local
goto union
```

Semantics The tokens (case sensitive) are recognized (in translation phases 7 and 8) for use as keywords, and should not be used otherwise. The keyword _Imaginary is reserved for specifying imaginary types.⁷⁰⁾)

Language §6.4.1

© ISO/IEC 2011 – All reserved ISO/IEC 9899:2011 (E)

## 6.4.2 Identifiers

### 6.4.2.1 General

Syntax

+ 1 identifier:
  identifier-nondigit
  identifier identifier-nondigit
  identifier digit

identifier-nondigit:
  nondigit
  universal-character-name
  other implementation-defined characters

nondigit: one of
  a b c d e f g h i j k l m
  n o p q r s t u v w x y z
  A B C D E F G H I J K L M
  N O P Q R S T U V W X Y Z

digit: one of
0 1 2 3 4 5 6 7 8 9

### Semantics

+ 2 An identifier is a sequence of nondigit characters (including the underscore _ the lowercase and uppercase letters, and other characters) and digits, which designates one or more elements as described in 6.2.1. Lowercase and uppercase letters are distinct. There is no specific limit on the maximum length of an identifier.

+ 3 Each universal character name in an identifier shall designate a character whose encoding in ISO/IEC 10646 falls into one of the ranges specified in D.1.¹⁷⁾ An implementation may allow multibyte characters to appear in identifiers; which characters and their correspondence to universal names is implementation-defined.

> ⁷⁰ One specification for imaginary types appears in annex G.

> ⁷⁾ On systems where linker cannot accept extended characters, an encoding of the universal character name may be used valid external identifiers. For example, otherwise unused sequence of characters may represent \ua in a universal character name. Extended characters may be a long external identifier.

6.4.2.1 Language

59

### Constraints

4 When preprocessing tokens are converted to tokens during translation phase 7, if a preprocessing token could be converted to either a keyword or an identifier, it is converted to a keyword.

### Implementation limits

5 As discussed in 5.2.1, an implementation may limit the number of significant initial characters in an identifier; the limit for an external name (an identifier that has external linkage) may be more restrictive than that for an internal name (a macro name or an identifier that does not have external linkage). The number of significant characters in an identifier is implementation-defined.

6 Any identifiers that differ in a significant character are different identifiers. If two identifiers differ only in nons characters, the behavior is undefined.

Forward references: universal character names (6.4.3), macro replacement (6.10.3).

## 6.4.2.2 Predefined identifiers

### Semantics

1 The identifier __func__ shall be implicitly declared by the translator as if, immediately following the opening brace of function definition, the declaration

```c
static char __func__[] = "function-name";
```
appeared, where function-name is the name of the lexically-enclosing function.⁷2)

2 This code is encoded as if the implicit had been written in the source character set and then translated into the execution character set as indicated in translation phase 5.

3 EXAMPLE Consider the code fragment:

```c#include <stdio.h>
void myfunc(void)
{
    printf("%s\n", __func__);
    /* */
}
```
Each time the function is called, it will print to the standard output stream:

myfunc

Forward references: function definitions (6.9.1).

> 72) Since the name __func__ is reserved for any use by the implementation (7.1.3), if any other identifier is explicitly declared using the name __, the behavior is undefined.
