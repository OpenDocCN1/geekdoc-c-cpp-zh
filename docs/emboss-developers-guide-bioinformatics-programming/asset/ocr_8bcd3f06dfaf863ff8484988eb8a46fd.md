ajfeatdata.h/c. Basic feature objects (AjPFeattable, AjPFeature and AjPFeattabOut) for general use, e.g. retrieving features via ACD file processing. It also defines a feature input object (AjPFeattabIn) used for low-level feature input handling.

# 6.9.3 ACD datatypes

A feature table (not individual features) may be specified for input or output in an ACD file. The datatype for handling feature table input is:

+   features Feature table input

The datatype for handling feature table output is:

+   featout Feature table output

Features can also be read from an input sequence and written alongside an output sequence if the features : ACD attribute is set. If set then the sequence output will include feature information either in the same file (if the sequence format supports it) or in a separate file (by default in GFF format).

ACD datatypes for sequence input include:

+   sequence Read a single sequence
+   seqall Read multiple sequences sequentially, one at a time
+   seqset Read multiple sequences as a single set
+   seqsetall Read multiple sequences as multiple sets

ACD datatypes for sequence output include:

+   seqout Write a single sequence
+   seqoutset Write multiple sequences as a single set
+   seqoutall Write multiple sequences sequentially, one at a time

# 6.9.4 ACD data definition

A typical ACD definition for feature input:

```
features: features
[
   parameter: "Y"
   type: "protein"
]
```

A typical ACD definition for feature output: