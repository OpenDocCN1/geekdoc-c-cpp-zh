# Chapter 2 The biological context

letter N. These codes are particularly helpful when we compare nucleotide sequences by aligning them and use a shorthand to denote substitution patterns observed between nucleotide bases: e.g., at positions where may interchange, the code R can be used; or, where may interchange, we use Y. The codes also find when we use to encapsulate patterns of conservation in particular regions of an alignment in the consensus expressions – we will discuss these in more detail in Chapter 4. For now, it is sufficient to note that when we depict nucleotide sequences, we use a single-letter code to denote individual bases, and another standard set of characters to denote either ambiguities or substitution alternatives at particular positions in sequence alignments.

# Table 2.1

IUPAC standard alphabet and ambiguity codes for nucleotides.

| Code | Base(s) | Code | Base(s) |
|---|---|---|--|
| A | Adenine | G | Guanine |
| C | Cytosine | T | Thymine |
| U | Uracil | | |
 M | A or C | R | A or G |
| W | A or T | S | C or G |
| Y | C or T | K | G or T |
| V | A or C or G | H | A or C or T |
| D | A or G or T | B | C or G or T |
| N | A or G or C or T | | |

These characters are used in the world of proteins, but with quite different meanings, so it's important not to confuse them. By contrast with the four-letter alphabet of nucleic acids, proteins have a much larger, 20-letter alphabet of amino acids. These, and their ambiguities, may be described using the single- or three-letter codes in Table 2.2.
As before, these codes are often used in consensus expressions derived from regions of sequence alignments (see, for example, Box 3.3 and Chapter 4 for more details), and they are also used to store sequences in files and databases more compactly, by the following sequence illustrates:

```
MethionineLeucineGlutamicAcidArgLeucineLeucineProlineThreonineAlanine
LLPLEITA
```

Although symbolic notations like these are convenient for the purposes of storage or computational mapping, the danger in using them is that they are essentially free of biological meaning (semantics); to a computer, sequences like STEVE or DAVID are no more obviously components of proteins than the names of people – they are simple strings of characters. If we are to compute with them, we must therefore supply the necessary protein-relevant contextual information, as to compare them meaningfully in multiple sequence alignments, or to quantify their similarity in database searches.