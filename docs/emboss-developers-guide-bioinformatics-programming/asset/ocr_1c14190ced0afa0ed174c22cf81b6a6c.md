# ## 6.8.9 Miscellaneous functions

There are a couple of functions for retrieving the elements of a translation object:

```
AjPStr ajTrnGetTitle (const AjPTrn thys);
AjPStr ajTrnGetFilename (const AjPTrn thys);
```

To check whether the input codon is a start codon, a stop codon or something else, call

```
ajint ajTrnCodonstrTypeC (const AjPTrn trnObj, const char *codon, char *aa);
ajint ajTrnCodonstrTypeS (const AjPTrn trnObj, const AjPStr codon, char *aa);
```

To return the genetic code description as a string for a given translation table file name number call:

```
const AjPStr ajTrnName(ajint trnFileNameInt);
```

To create a suitably named sequence object to hold a peptide translation call:

```
AjPSeq ajTrnNewPep(const AjPSeq nucleicSeq, ajint frame);
```

To read a translaton data file (used internally when translation is initialised):

```
void ajTrnReadFile(AjPTrn trnObj, AjPFile trnFile);
```

# ## 6.9 Handling features

# ### 6.9.1 Introduction

A feature is a region of interest in a molecular sequence such as a restriction enzyme cut site, protein secondary structure prediction state, exon position, regions of motif match and so on. EMBOSS supports, for input and output, most of the formats (see the _EMBOSS User's Guide_) that were developed for input of features into the major genome sequence databases.

Many applications do not read and write features directly. Features are also used to store the results of sequence analysis, and can be written out as ‘reports’ where a report format defined through ACD is used to write out a feature table and (for some formats) the original sequence (see Section 6.15, ‘Handling application reports’).

Features are annotations of simple ranges in a sequence (start and end) or of a numbered group of features which have a ‘join’ (to combine exons in a coding sequence) or some other combination (‘group’ or ‘one-of’ in the EMBL/Genbank feature table). These complex features are stored as a parent feature with a set of simpler features for each component. Currently these are stored in the same feature table. In a future release these may become sub-features to simplify sorting operations.