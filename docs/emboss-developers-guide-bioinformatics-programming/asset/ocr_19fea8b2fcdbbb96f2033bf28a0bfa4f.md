# 6.13 Handling codon usage tables

# 6.13.1 Introduction

EMBOSS provides a codon usage table object that holds arrays describing codon usage in a nucleotide sequence.

Codon usage tables for input and output are usually defined in the ACD file, but they can be created directly if this is required. Functions are provided for reading and writing the data, getting and setting elements of the object, calculating properties of the codon usage table and for back translation. There are also some miscellaneous functions, mostly used for interconverting triplet base codes to codon indices.

Code that creates a codon usage table needs to first create an output object, then populate it with codon usage data from coding sequences, calculate statistics on codon frequencies and write to a file which uses the user-selected format.

# 6.13.2 AJAX library files

AJAX library files for handling codon usage tables are listed in the table below. Library file documentation, including a complete description of datatypes and functions, is available at: http://emboss.open-bio.org/rel/dev/libs/

| Library file documentation | Description |
|---|---|
| ajcod | Codon usage table handling |

ajcod.h/c. Defines the AjPCod object and functions for handling codon usage tables. It also contains static data structures and functions for handling them at a low level. You are unlikely to need these unless you plan to extend the core functionality of the library.

# 6.13.3 ACD datatypes

The ACD datatype for handling codon usage tables is:

+   codon Codon usage table file

# 6.13.4 ACD data definition

A typical ACD definition for codon usage table input:

```
codon: infile
[
  parameter: "y"
]
```

A typical ACD definition for codon usage table output:

```
outcodon: outfile
[
```