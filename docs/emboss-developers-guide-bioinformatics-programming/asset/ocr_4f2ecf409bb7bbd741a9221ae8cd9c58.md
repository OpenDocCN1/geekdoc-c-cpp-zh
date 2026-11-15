stands for Ala or Leu or Thr. Ambiguities are also indicated by listing between a pair of curly brackets { } the amino acids that are not accepted at a given position. For example:

```
{AM}
```

stands for any amino acid except Ala and Met. Each element in a pattern is separated from its neighbour by a dash (-). Repetition of an element of the pattern can be indicated by following that element with a numerical value or a numerical range between parenthesis. For example:

```
x (3) corresponds to x-x-x
x (2 , 4) corresponds to x-x or x-x-x or x-x-x-x-x
```

When a pattern is restricted to either the N- or C-terminal of a sequence, that pattern either starts with a < symbol or respectively ends with a > symbol. A period ends the pattern. For example:

```
[DE] (2) HS{P}X(2) PX (2 , 4) C.
```

Default value A default value is set using the default : global attribute.

Key attributes Attributes provide validation, for example, to control the length (minlength: and maxlength attributes) and case of the pattern, which can be set to upper (upper: "Y") or lower case (lower: "Y") only. The type of pattern (nucleotide or protein) can be set using type:.

# A.2.1.8 string

Simple string.

Most string values are free text, although strings can be used by a program for any input that is not covered by the other ACD datatypes so long as the string is subsequently parsed.

Data value The data value is any valid ASCII text string which should be enclosed in double quotes. For example:

```
"This is a valid text string"
```

Default value A default value is set using the default : global attribute.

Key attributes Whenever a string datatype is defined, a type for it should be specified with the knowntype : attribute: a warning message will be generated during ACD processing otherwise.