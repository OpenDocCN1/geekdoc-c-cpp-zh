```
parameter: "Y"
maximum: @($(targetsequence.length) + $(insertsequence.length))
]
```

These calculated attributes are also useful for conditional statements. In the example below the sequence input is of the any type. A ternary conditional (see Section 4.4, ‘Operations’) is being used to set a default substitution matrix based on the automatically determined type of sequence:

```
sequence: sequence
[
  parameter: "Y"
  type: "anY"
]

integer: penalty
[
  parameter: "Y"
  default: "@($(sequence.protein) ? EBLOSUM62 : EDNAFULL)"
  etc
]
```

# 4.3.8.3 Feature calculated attributes

The sequence feature input datatype:

```
features
```

has seven calculated attributes:

fbegin Start of the features to be used (- fbegin value)
fend End of the features to be used (- fend value)
flength Total length of sequence
fprotein Boolean, True if feature table is protein
fnucleic Boolean, True if feature table is nucleotide
fname Name of the feature table
fsize Number of features

These are properties of an input feature that can be queried within ACD.

> **Note**
> 
> The value of the fbegin and fend attributes can be set on the command line by specifying -fbegin or -fend which are inbuilt qualifiers for the features datatype.