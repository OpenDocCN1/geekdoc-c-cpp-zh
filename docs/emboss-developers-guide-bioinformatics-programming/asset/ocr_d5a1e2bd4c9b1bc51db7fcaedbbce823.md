```
void ajSeqsetFmtLower (AjPSeqset seq);
void ajSeqsetFmtUpper (AjPSeqset seq);
void ajSeqFmtLower (AjPSeq thys);
void ajSeqFmtUpper (AjPSeq thys);
```

ajSeqsetFill can be used to fill a sequence set by putting gaps at the ends of any short sequences:

```
ajint ajSeqsetFill(AjPSeqset seq)
```

# 6.7.13 Sequence type validation

In most cases the validation of sequence type (see Section A.7, ‘Sequence types’), e.g. whether a sequence is for a protein or nucleic acid, contains gaps and so on, is handled at the level of the ACD file. This means that the application always receives (via a call to ajAcdGet*) a sequence of the exact type specified in the ACD file.

Several functions are provided in AJAX for handling sequence type directly. The type of a sequence can be set automatically, i.e. determined from the sequence itself, by calling ajSeqType. Otherwise it can be set directly for a sequence, or a sequence set, to one of nucleotide or protein using the following functions:

```
void ajSeqType (AjPSeq thys);
void ajSeqSetNuc (AjPSeq thys);
void ajSeqSetProt (AjPSeq thys);
void ajSeqsetSetNuc (AjPSeqset thys);
void ajSeqsetSetProt (AjPSeqset thys);
```

# 6.7.14 Sequence conversion

It is sometimes necessary to convert a sequence into numeric form for convenient processing. The AJAX datatype for this is:

+   AjPSeqCvt Used for sequence conversion into numeric form

The common use-case is where a sequence character conversion table is generated for a scoring matrix, such as an amino acid substitution scoring matrix (see Section 6.10, ‘Handling comparison matrices’).

# 6.7.15 Handling sequence translation

Translation of a genetic sequence into a protein is a common task and is covered elsewhere (Section 6.8, ‘Handling sequence translation’).

# 6.7.16 Handling IUB base codes

EMBOSS supports the official IUB base codes as shown below and also X to indicate an unknown base.