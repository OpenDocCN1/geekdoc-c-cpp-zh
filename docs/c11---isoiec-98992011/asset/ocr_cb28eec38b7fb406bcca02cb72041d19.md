ISO/IEC 9899:2011 (E)

control-line:

```
# include pp-tokens new-line
# define identifier replacement-list new-line
# define identifier lparen identifier-list_opt )
    replacement-list ... new-line
# define identifier lparen ... replacement-list new-line
# define identifier lparen identifier-list , ... )
    replacement-list new-line
# undef identifier new-line
# line pp-tokens new-line
# error pp-tokens_opt new-line
# pragma pp-tokens_opt new-line
# new-line
```

text-line:

pp-tokens_opt new-line

non-directive:

pp-tokens new-line

lparen:

a ( character not immediately preceded by white-space

replacement-list:

pp-tokens_opt

pp-tokens:

preprocessing-token

pp-tokens preprocessing-token

new-line:

the new-line character

# Description

A preprocessing directive consists of a sequence of preprocessing tokens that satisfies the following constraints: the first token in the sequence is a # preprocessing token that (at the start of translation phase 4) is either the first token in the source file (optionally after white space containing no new-line characters) or that follows white space containing at least one new-line character. The last token in the sequence is the first new-line character that follows the first token in the sequence.¹⁶⁵) A new-line character follows the preprocessing directive even if it occurs within what would otherwise be an

> ¹⁶⁵) Thus, preprocessing directives are commonly called “lines”. These “lines” have no syntactic difference, as all white space is equal in certain situations during preprocessing (see the string literal identifier in 6.10.3, for example).

# §6.10

# Language

# 161