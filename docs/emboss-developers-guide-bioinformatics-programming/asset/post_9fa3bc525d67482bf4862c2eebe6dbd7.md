
select: matrix
[
    default: "blosum"    # default value
    minimum: "1" maximum: "1"    # must select exactly 1
    header: "Comparison matrices"    # printed before list
    values: "blosum, pam, id"    # valid values
    delimiter: ","    # delimiter default ";"
    information: "Select one"    # prompt after list
    button: "Y"    # use radio buttons rather than checkboxes in HTML,
    ignored by ACD
]

you get:

Comparison matrices
1 : blosum
2 : pam
3 : id
Select one [blosum] : PAM

## 4.3.6.5 Attributes for graphics ACD datatypes

These specify the graph data that are output.

gtitle: specifies the graph title for a graph or graphxy datatype. Many other graphical elements can be set.

multiple: specifies the number of multiple graphs in a single graph or graphxy datatype output.

## 4.3.7 Attributes for datatype-associated qualifiers

Various command line qualifiers are inbuilt for certain ACD datatypes. These datatype-associated qualifiers are normally specified only on the command line. They may, however, also be ‘hard-coded’ as attributes in the appropriate data definition and it is sometimes desirable to do this. Some examples for setting file format are shown below:

| Input sequence | -sformat |
|---|---|
| | sformat: |
| Output sequence | -osformat |
| | osformat: |
| Output alignment | -aformat |
| | aformat: |
| Report output file | -rformat |
| | rformat: |
| Sequence feature input | -fformat |
| | fformat: |
| Sequence feature output | -oformat |
| | oformat: |

The qualifiers are described in more detail in the EMBOSS User’s Guide.

## 4.3.8 Introduction to calculated attributes

Calculated attributes are datatype-specific attributes that are assigned values _after_ an input file has been read during ACD file processing. The values are calculated or extracted from the actual data that an ACD data definition refers to.

Most calculated attributes are for datatypes for sequence input (`sequence`, `seqall`, `seqset` and `seqsetall`) and sequence feature input (`features`). For instance, for a sequence datatype, the length and type of sequence are available once the sequence file or an entry from it has been read.

For a complete description of the available calculated attributes see Section A.6, ‘Calculated attributes’.

### 4.3.8.1 Retrieving values of calculated attributes

Values of calculated attributes are retrieved by an operation (Section 4.4, ‘Operations’) from within the ACD file. The operation uses a `ParameterName.AttributeName` term surrounded by parentheses with a dollar sign (`$`) at the front:

```
$(ParameterName.AttributeName)
```

The `$` syntax means ‘get the value of, in this case the term enclosed by parentheses.

This is typically done from within a data definition that relies on the value of a calculated attribute from some other data definition. For example, the following ACD file excerpt defines a sequence parameter and an integer window:

```
sequence: sequence
[
    parameter: "Y"
    type: pureprotein
]

integer: window
[
    standard: "Y"
    default: "10"
    maximum: "$(sequence.length)"
]
```

The maximum window size (`maximum` attribute of the `window` datatype) is being set to the length of the sequence by using `maximum: "$(sequence.length)"`.

### 4.3.8.2 Sequence calculated attributes

All of the sequence input datatypes:
- sequence
- seqall
- seqset
- seqsetall

have six calculated attributes that are properties of an input sequence which can be queried within ACD:

| Attribute | Description |
|---|---|
| begin | Start residue (-sbegin value) |
| end | End residue (-send value) |
| length | Length |
| protein | Boolean, True if sequence is protein |
| nucleic | Boolean, True if sequence is nucleic |
| name | Name |

Let's assume we've defined a sequence input called asequence and have an ACD file looking something like:

```
sequence: asequence
[
   parameter: "y"
   type: protein
]
```

The attributes would be referred to as follows:

- asequence.begin
- asequence.end
- asequence.length
- asequence.protein
- asequence.nucleic
- asequence.name

> **Note**
>
> The value of the **begin** and **end** attributes can be set on the command line by specifying the **-sbegin** or **-send** which are inbuilt qualifiers for the sequence types.

The seqset and seqsetall datatypes have the following calculated attributes:

| Attribute | Description |
|---|---|
| totweight | Total sequence weight for the set(s) of sequences |
| count | Number of sequences in the set(s) |

seqsetall also has:

| Attribute | Description |
|---|---|
| multicount | Number of sets of sequences |

To retrieve calculated attribute values from the definition of asequence shown above you can use:

```
$(asequence.begin)
$(asequence.end)
$(asequence.length)
```

### Example

When writing a program to insert one sequence into another, one way to make sure that the insertion position isn’t greater than the length of the first sequence is to use code like the following:

```
if (position > ajSeqGetLen(seq))
    ajFatal("Insertion position out of bounds");
```

The problem is that the program can prematurely terminate after the user has gone to all the effort of configuring the application (entering all the inputs). What would be better is if the interface forced the correct input, and there is a way to achieve that by using calculated attributes in the ACD file itself.

Now, instead of hard-coding the check for the sequence insertion position you just need to add:

```
maximum: $(asequence.end)
```

to the integer definition of the insert position. An ACD file with two input sequences and an integer insert position might look something like:

```
sequence: targetsequence
[
   parameter: "Y"
   type: "protein"
]

sequence: insertsequence
[
   parameter: "Y"
   type: "protein"
]

integer: position
[
   parameter: "Y"
   maximum: $(targetsequence.end)
]
```

You may of course retrieve the value of calculated attributes from both sequences. In the following example, a sequence window is defined which cannot be any longer than the sum of the lengths of the two sequences. A calculation is used, which therefore has to be enclosed by parentheses and started with the ‘at’ symbol (‘@’):

```
integer: window
[
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

### 4.3.8.3 Feature calculated attributes

The sequence feature input datatype:

```
features
```

has seven calculated attributes:

| Attribute | Description |
|---|---|
| fbegin | Start of the features to be used (-fbegin value) |
| fend | End of the features to be used (-fend value) |
| flength | Total length of sequence |
| fprotein | Boolean, True if feature table is protein |
| fnucleic | Boolean, True if feature table is nucleotide |
| fname | Name of the feature table |
| fsize | Number of features |

These are properties of an input feature that can be queried within ACD.

> **Note**
>
> The value of the fbegin and fend attributes can be set on the command line by specifying -fbegin or -fend which are inbuilt qualifiers for the features datatype.

Assuming you've defined a feature input called afeatures and have an ACD file looking something like:

```
features: afeatures
[
  parameter: "Y"
]
```

the attributes would be referred to as follows:

- afeatures.fbegin
- afeatures.fend

and so on.

To retrieve calculated attribute values from your definition of afeatures above you can use:

```
$(afeatures.fbegin)
$(afeatures.fend)
$(afeatures.flength)
```

### Example

When writing a program to compare the features of two sequences, which might be protein or nucleotide sequences, you need to ensure that both sequences are of the same type. One way to do this from the application code is to call an AJAX function to return the type of both, and exit if they are not the same:

```
if((ajFeattableIsProt(features1)&& ajFeattableIsNuc(features2)) ||
   (ajFeattableIsNuc(features1) && ajFeattableIsProt(features2)))
   ajFatal("Input feature tables are not of the same type");
```

The problem with this code is that the application will terminate once it is running if the feature tables are not of the same type. Far better if the interface forced the correct input before the application proper started, which can be achieved by using calculated attributes.

Assume the application takes two feature table parameters as input and the ACD file therefore looks something like:

```
features: afeatures
[
  parameter: "Y"
]

features: bfeatures
[
  parameter: "Y"
]
```
