
## Chapter 2 The biological context

letter N. These codes are particularly helpful when we compare nucleotide sequences by aligning them and use a shorthand to denote substitution patterns observed between nucleotide bases: e.g., at positions where pur may interchange, the code R can be used; or, where py may interchange, we use Y. The codes also find use when we use them to encapsulate patterns of conservation in particular regions of an alignment in the consensus expressions – we will discuss these in more detail in Chapter 4. For now, it is sufficient to note that when we depict nucleotide sequences, we use a single-letter code to denote individual bases, and another standard set of characters to denote either ambiguities or substitution alternatives at particular positions in sequence alignments.

## Table 2.1

IUPAC standard alphabet and ambiguity codes for nucleotides.

| Code | Base(s) | Code | Base(s) |
|---|---|---|---|
| A | Adenine | G | Guanine |
| C | Cytosine | T | Thymine |
| U | Uracil | | |
| M | A or C | R | A or G |
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

## Table 2.2

IUPAC standard alphabet and ambiguity codes for amino acids.

| 1-letter code | Amino acid(s) | 3-letter code | 1-letter code | Amino acid(s) | 3-letter code |
|---|---|---|---|---|---|
| G | Glycine | Gly | P | Proline | Pro |
| A | Alanine | Ala | V | Valine | Val |
| L | Leucine | Leu | I | Isoleucine | Ile |
| M | Methionine | Met | C | Cysteine | Cys |
| F | Phenylalanine | Phe | Y | Tyrosine | Tyr |
| W | Tryptophan | Trip | H | Histidine | His |
| K | Lysine | Lys | R | Arginine | Arg |
| Q | Glutamine | Gln | N | Asparagine | Asn |
| E | Glutamic acid | Glu | D | Aspartic acid | Asp |
| S | Serine | Ser | T | Threonine | Thr |
| B | Asp or As | | Z | Glu or Gln | Glx |
| X | Anything / Unknown | XXX / Unk | | |

Let examine this in a little more detail. The chemical structure of an amino acid is shown in Figure 2.6: it has an amino group (NH₂) on one side and a carboxylic acid (COOH) on the other side of a carbon (or α) carbon. In solution, these amino acids are ionised to NH₃⁺ and COO⁻ (i.e., they carry positive or negative charges). To the α-carbon is attached side-chain (denoted R); it distinguishes the 20 amino acids from each other (these are listed in Box 2.2).

Linear chains of amino acids are linked via so-called peptide bonds, which are formed by a chemical reaction that removes a hydroxyl group (OH) from the carboxyl group of one amino acid and a hydrogen from the amino group of the next, to form water (H₂O). A chain of two amino acids (dipeptide) joined in this way is shown in Figure 2.8.

Proteins comprise chains of hundreds of amino acids. The ends of these chains are the N-terminus and C-terminus, as the former has an unlinked NH₃⁺ group and the latter an unlinked COO⁻. By convention, protein sequences are written from the N to the C-terminus, corresponding to the direction in which they are synthesised.

The chemical nature of the peptide bond means it is plane (denoted by boxes in Figure 2.9) and can’t rotate freely with respect to one another. What flexibility there derives from rotation about the N-α and C-C bonds at each α-carbon, as illustrated. This torsional force confers a wide variety of 3D structures on the polypeptide backbone. The final structure adopted by a protein is a direct consequence of the specific sequence of its amino acid side chains (R1, R2 ... Rn), as their sizes or chemical nature either permit or prohibit backbone rotations. A protein reaches its native structure through

![](img/1af42ff402ef4720886c50af0bb8e9b5_43_0.png)

## Figure 2.6

Chemical structure of an amino acid.

## Box 2.2 The chemical structures of amino acid side-chains

The 20 amino acid side-chains may be broadly grouped according to their physicochemical properties: those that are largely hydrophobic are shown in the top tier of Figure 2.7; those that are largely hydrophilic are shown in the middle tier; and those that are ambivalent, or amphipathic, are shown at the bottom.

![](img/1af42ff402ef4720886c50af0bb8e9b5_44_0.png)

Figure 2.7 Chemical structures of the 20 amino acids.

> *http://chemwiki.ucdavis.edu/Wiklets/University_of_California_Davis/UCD_Chem_115_Lab_Manual/Lab_7%3A_Electrospray_Mass_Spectrometry

## Figure 2.8

Formation of the peptide bond.

![](img/1af42ff402ef4720886c50af0bb8e9b5_45_0.png)

## Figure 2.9

The plane of the peptide bond.

![](img/1af42ff402ef4720886c50af0bb8e9b5_45_1.png)

## Figure 2.10

The properties of amino acids.

![](img/1af42ff402ef4720886c50af0bb8e9b5_46_0.png)
