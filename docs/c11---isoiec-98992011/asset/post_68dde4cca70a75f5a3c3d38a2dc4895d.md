
# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

```
FLT_DIG 6
FLT_MIN_EXP -125
FLT_MIN 1.17549435E-38F // decimal constant
FLT_MIN 0X1P-126 // hex constant
FLT_TRUE_MIN 1.40129846E-45F // decimal constant
FLT_TRUE_MIN 0X1P-149F // hex constant
FLT_HAS_SUBNORM 1
FLT_MIN_10_EXP -37
FLT_MAX +128
FLT_MAX 3.40282347E+38F // decimal constant
FLT_MAX 0X1FFFFFFFFF // hex constant
DBL_MANT_DIG 53
DBL_EPSILON 2.220446925031316E-16 // decimal constant
DBL_EPSILON 0X1P-52 // hex constant
DBL_DECIMAL_DIG 17
DBL_DIG 15
DBL_MIN -1021
DBL_MIN 2.225073858072014E-308 // decimal constant
DBL_MIN 0X1P-1022 // hex constant
DBL_TRUE_MIN 4.90656458421465E-324 // decimal constant
DBL_TRUE_MIN 0X1P-1074 // hex constant
DBL_HAS_SUBNORM 1
DBL_MIN_10_EXP -307
DBL_MAX +1024
DBL_MAX 1.79FFFFFFFFFFFF // decimal constant
DBL_MAX_10_EXP +308
```

If a wide type like double were supported, then DECIMAL_DIG would be greater than 17. For example, if the widest type were to use the minimum-width IEC 60559 double-extended format (64 bits of precision), then DECIMAL_DIG would be 21.

Forward references: conditional inclusion (6.10.1), complex arithmetic references <complex.h> (7.3), extended multibyte and wide character utilities <wchar.h> (7.29), floating-point environment <fenv.h> (7.6), general utilities <stdlib.h> (7.22), input/output <stdio.h> (7.21), mathematics <math.h> (7.12).

34

Environment

§5.2.4.2.2

## 6. Language

## 6.1 Notation

In the syntax notation used in this clause, syntactic categories (nonterminals) are indicated by *italic type*, and literal words and character set members (terminals) by **bold type**. A colon (:) following a nonterminal introduces its definition. Alternative definitions are listed on separate lines, except prefixed by the words “one of”. An optional symbol is indicated by the subscript “opt”, so that

```
{ expression_opt }
```

indicates an optional expression enclosed in braces.

When syntactic categories are referred to the main text, they are not italicized and words are separated by spaces instead of hyphens.

A summary of the language syntax is given in annex A.

## 6.2 Concepts

### 6.2.1 Scopes of identifiers

An identifier can define an object; a function; a tag or a member of a structure, union, or enumeration; a typedef name; a label name; a macro name; a macro parameter. The same identifier can define different entities at different points in the program. A member of an enumeration is called an *enumeration constant*. Macro names and macro parameters are not considered further here, because prior to the semantic phase of program translation any occurrences of macro names in source file are replaced by the preprocessing steps that constitute their macro definitions.

For each entity that has an identifier, the identifier is visible (i.e., can be used) only within a region of program called its *scope*. Different entities designated by the same identifier have different scopes, or are in different spaces. There are four kinds of scopes: function, file, block and function prototype.(A function prototype is a declaration of a function that declares its parameters.)

A label name has scope. It can be used (in a goto statement) anywhere in the function in which it appears, and is declared implicitly by its syntactic appearance (by a : and a statement).

Every identifier has scope determined by the placement of its declaration (in a declarator or type specifier). If the declarator or type specifier that declares the identifier appears outside of any list or parameters, the identifier has *file scope*, which terminates at the end of the translation unit. If the declarator or type specifier that declares the identifier appears inside a block or within the list of parameter declarations, the identifier has *block scope*, which terminates at the end of the associated block. If the declarator or type specifier that declares the identifier appears within the list of parameter declarations in a function prototype (not part of a function definition), the identifier designates function prototype scope, which terminates at the end of the function declarator. If an identifier designates two entities in the same name space, the scopes might overlap. If so, the scope of one entity (the inner scope) will end strictly before the scope of the other entity (the outer scope). Within the inner scope, the identifier designates the entity declared in the outer scope; the entity declared is hidden (not visible) within the inner scope.

- 5 Unless explicitly stated otherwise, where this International Standard uses the term “identifier” to refer to some entity (as opposed to the syntactic construct), it refers to the entity in the relevant name space whose is visible at the point the identifier occurs.

- 6 Two identifiers have the same scope if and only if their scopes terminate at the same point.

- 7 Structure, union, and enumeration tags have scope that begins just after the appearance of the tag in a type that declares the tag. Each enumeration count has scope that begins just after the appearance of its defining enumerator in an enumerator list. Any identifier has scope that begins just after the completion of its declarator.

- 8 As a special case, a type name (not a declaration of an identifier) is considered to have a scope that begins just after the type name where the omitted identifier would appear it were not omitted.

Forward references: declarations (6.7), function calls (6.5.2.2), function definitions (6.9.1), identifiers (6.4.2), macro replacement (6.10.3), name spaces of identifiers (6.2.3), source file inclusion (6.10.2), statements and blocks (6.8).

### 6.2.2 Linkages of identifiers

- 1 An identifier declared in different scopes or in the same scope more than once can be made to refer to the same object or by a process called linkage.29 There are three kinds of linkage: external, internal, and none.

- 2 In the set of translation units and libraries that constitute an program, each declaration of a particular identifier with external linkage denotes the same object or function. Within one translation unit, each declaration of an identifier with internal linkage denotes the same object or function. Each declaration of an identifier with no linkage denotes a unique entity.

- 3 If the declaration of a file scope for an object or a function contains the storage-class specifier static, the identifier has internal linkage.30

> 29) There is no linkage between different identifiers.

- 4 For an identifier declared with the storage-class specifier extern in a scope in which a prior declaration is visible, the linkage of the identifier is the same as the prior declaration. If no prior declaration is visible, or if the prior declaration specifies no linkage, the identifier has external linkage.

-  If the declaration of an identifier has no storage-class specifier, its linkage is determined exactly as if it were with the storage-class specifier extern. The following identifiers have no linkage: an identifier declared to be anything other than an object or an identifier declared to be function parameter; a block scope identifier declared without the storage-class specifier.

- If, within a translation unit, the same identifier appears with both internal and external linkage, the behavior is undefined.

Forward references: declarations (6.7), expressions (6.5), external definitions (6.9), statements (6.8).

### 6.2.3 Name of identifiers

If more than one declaration of a particular identifier is visible at any point in a translation unit, the syntactic context disambiguates to different entities. Thus, there are separate name spaces for various categories of identifiers, as:

- label names (disambiguated by the syntax of the label declaration and use);

- the tags of structures, unions, and enumerations (disambiguated by following any³²) of the keywords struct, union, or enum;

- the members of structures or unions; each structure or union has a separate name for its members (disambiguated by the type of the expression used to access the member via the . or -> operator);

- all other identifiers, called ordinary identifiers (declared in ordinary declarators or as enumeration constants).

Forward references: enumeration specifiers (6.7.2.2), labeled statements (6.8.1), structure and union specifiers (6.7.2.1), structure and union members (6.5.2.3), tags (6.7.2.3), the goto statement (6.8.6.1).

30) A function declaration can contain the storage-class specifier static if it is at file scope; 6.7.1.

31) As specified in 6.2.1, the later declaration might hide the prior declaration.

32) There is only one name space for tags even three are possible.
