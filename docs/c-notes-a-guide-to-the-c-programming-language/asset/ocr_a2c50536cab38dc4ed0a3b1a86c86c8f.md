There are no literal function values, although the formal arguments and the function body are tantamount to that. These topics are discussed in greater detail in [2.6], which deals with function initializers.

# 0.7 Syntax summary

A properly formed C program consists of a sequence of tokens grouped into phrases in a very precise way. The rules prescribing the set of properly formed C programs are known as the syntax. Each rule defines the meaning of a particular phrase name by specifying all possible ways of building such a phrase from primitive tokens and other phrases. The first rule defines the phrase “C program” as a sequence of one or more program files and is written:

```
C-program = { program-file }
```

The braces imply one or more occurrences.

Another rule defines a type definition as the keyword typedef, followed by a type specifier followed by a declarator list, followed by the token ; .

This rule is written:

```
type-definition =
    typedef type-specifier declarator-list ;
```

The phrase type specifier is defined by

```
type-specifier =
    [ integer-type | floating-type
    | type-name | structure-or-union-type ]
```

which means a choice of one of the four alternatives. A subscript opt indicates optional occurrence so that

```
floating-type =
    [ short_opt double | long_opt float ]
```

means the keyword double, possibly preceded by short, or else float, possibly preceded by long. Occasionally, parentheses are used to group a sequence of phrases that is optional as in

```
( else statement )_opt
```