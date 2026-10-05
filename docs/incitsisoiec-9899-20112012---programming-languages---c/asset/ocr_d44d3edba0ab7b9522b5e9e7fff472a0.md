specifying imaginary types.¹⁷⁰)

# ## 6.4.2 Identifiers

# ### 6.4.2.1 General

# #### Syntax

identifier:
identifier-nondigit
identifier identifier-nondigit
identifier digit

identifier-nondigit:
nondigit
unnivers-character-name
other implementation-defined characters

nondigit: one of
- a b c d e f g h i j k 1 m
n o p q r s t u v w x y z
A B C D E F G H I J K L M
 O P Q R S T U V X Y Z

digit: one of
0 1 2 3 4 5 6 7 8 9

# #### Semantics

An identifier is a sequence of nondigit characters (including the underscore _, lowercase and uppercase Latin letters, and other characters) and digits, which designates one or more entities as described in 6.2.1. Lowercase and uppercase letters are distinct. There is no specific limit on the maximum length of an identifier.

Each universal character name in an identifier shall designate a character whose encoding falls in ISO/IEC 10646 falls into one of the ranges specified in D.1.¹⁷¹ The initial character shall not be a universal character name designating a character whose encoding falls into one of the ranges in D.2. An implementation may allow multibyte characters that are not part of the basic source character set to appear in identifiers; which characters and their correspondence to universal character names are implementation-defined.

> ⁰ Possible specification for imaginary types appears in annex G.

> ¹ Systems on which linkers cannot accept extended characters, an encoding of the universal character name may be used in forming valid external identifiers. For example, otherwise unused character or sequence of characters may be used to encode the \u in a universal character name. Extended characters may produce a long external identifier.