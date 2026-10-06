
4 UniRef100, UniRef90 and UniRef50 are sources of:

- A A nucleotide clustered at different levels of sequence identity.
- B protein sequences clustered at different levels of sequence identity.
- C protein families clustered at different levels of sequence identity.
- D protein structures clustered at different levels of sequence identity.

5 Which of the following statements are correct?

- A A Swiss-Prot initially took data from Dayhoff's Atlas.
- B Swiss-Prot was inspired by the format of entries in the EMBL data library.
- C Swiss-Prot was built on data in the PIR-PSD.
- D None of the above.

6 Which of the following statements are correct?

- A A TrEMBL is a source of high-quality manual annotation.
- B UniProt was created to integrate protein family information.
- C UniProt was created as the world-wide archive of protein sequence data.
- D None of the above.

7 Signature databases were developed to:

- A A classifies structures into evolutionarily related families.
- B help analyse and functionally annotate uncharacterised sequences.
- C classifies sequences into evolutionarily related families.
- D None of the above.

8 Which of the following statements are correct?

- A A The sequence-structure deficit refers to over-abundance of protein structures relative to the number of known protein sequences.
- B The sequence-structure deficit is shrinking owing to advances in high-throughput sequencing technology.
- C The sequence-structure deficit refers to over-abundance of protein sequences relative to the number of known protein structures.
- D The sequence-structure deficit is shrinking owing to advances in high-throughput sequencing determination.

9 Which of the following statements are correct?

- A A NGS technologies reduce the need for manual annotation.
- B NGS technologies make fully manual annotation strategies unrealistic.
- C NGS technologies reduce the need for computer-generated annotation.
- D NGS technologies make automatic-annotation strategies unrealistic.

10 Which of the following statements are correct?

- A A The goal of 3Gen sequencing technology is to produce more sequence data than NGS technologies.
- B The goal of 3Gen sequencing technology is to make whole-genome sequencing cheaper and faster.
- C The goal of 3Gen sequencing technology is to make sequencing technology feasible as a diagnostic biomedical and clinical tool.
- D None of the above.

## 3.16 Problems

- 1 Consensus expressions use a kind of shorthand notation to summarise the conserved residues in parts of sequence alignments. Consider the expression shown in Box 3.3:

```
A-[LV]-Y-S-[AVI]-V-[CF]-[AV]-V-G-L-[LVF]-G-N-X-L-V-M
```

This sequence, AVYSCVCVGGLNYLVM, the pattern of conserved residues, but this one, AVYSCVCVGGLNYLVM, doesn't. Why? Based on your answer, can you write a version of the latter sequence that would match the expression?

Fingerprints are groups of motifs that encode conserved regions of sequence alignments. Consider the fingerprints illustrated in Box 3.4, reproduced in Figure 3.14.

![](img/1af42ff402ef4720886c50af0bb8e9b5_106_0.png)

Let's assume we have searched these fingerprints with a query sequence; the result, is an imperfect match to one of them, as shown in Figure 3.15:

![](img/1af42ff402ef4720886c50af0bb8e9b5_106_1.png)

The gapped (missing) region in the centre shows that the query is shorter than some of the sequences and shares most similarity at its N- and C-termini. Which fingerprint does it resemble, and why? How many (and which) motifs does it lack?

- 2 According to the information available from the RCSB, the number of unique protein folds housed in the PDB in November 2015 is 1,375 according to CATH and 1,393 according to SCOP. What are CATH and SCOP, and why might their estimates of the number of unique folds differ? In November 2015, the total number of protein structures available from the PDB was 105,951. Why does this number differ so much from the fold estimates given by SCOP and CATH?

- 3 Which is likely to be larger: a non-identical composite database or a non-redundant composite database? Why?

There are two widely used composite protein sequence databases. What are they, and in what ways do they differ (comment on the likely nature and sources of error)?

- 4 InterPro combines data from more than a dozen source databases. What is InterPro? What are the principal diagnostic methods and which of InterPro’s partner databases do they underpin? What are some of the main integration challenges that must be tackled in creating InterPro releases?

## Chapter 4
## Biological sequence analysis

## 4.1 Overview

In this chapter, we outline a variety of sequence analysis methods, some of which underpin databases we discussed in Chapter 3. We begin by looking at the need to annotate raw sequence data, and show how the database flat-file format evolved as a necessity of making biological data reusable and searchable. In the central part of the chapter, we introduce some of the tools that are used routinely compare pairs of sequences and groups of sequences, and discuss how these are used to assess evolution relationships. To complete the picture, we then show how the information in multiple alignments can be used for the purpose of sequence annotation.

By the end of the chapter, you should be able to list some of elements of database flat-file formats, and understand how some of these are used by database software.

## 4.2 Adding to raw sequence

In the previous chapter, we broadly described the range of information available in structure-based databases. We now want to take a step back to look closely at raw sequence data, and consider what we need to add in order to make them both useful and reusable. We will use this discussion to build a picture of how ultimately store the data we've seen. For convenience, we use single-letter notations to denote protein sequences. A typical fragment of DNA – a simple string of As, Cs and Ts. On its own, of course, a string of hundreds of A, C, T and G characters, if we're dealing with a completely sequenced genome is meaningless. Like natural language, it requires punctuation to be comprehensible.

Figure 4.1 (Fragment of genomic DNA – a continuous strand of; b) fragment of prose without punctuation. In 4.1(b), isn't it? Even if we know the language in which a piece of text is written, its still difficult to comprehend without punctuation (if there are also errors of grammar and spelling, or idiomatic usage, understanding it can be quite a challenge). Genomic DNA is the same – but making correction is harder.

To add one level of meaning to a string of nucleotide sequences, we might want to find out which parts are liable to encode proteins. We saw earlier that the codon for methionine, AUG, also functions as a start codon. For the example shown in Figure 4.1, we could begin by identifying the locations of all ATG codons, as illustrated in Figure 4.2(a).

It should be obvious that this is not enough; knowing where a message start doesn't tell us where it actually starts, nor does it light on where the message stops. In Chapter 2, we saw that there are three stop codons: TGA, TAA and TAG. As shown in Figure 4.2(b), if we add these to the sequence, the picture appears to become even more complicated.

Just knowing the positions of start and stop codons is not the full story. What we need to do is look for start codons that are followed by stop codons at a sufficient distance for the intervening sequence to be able to encode a full-length protein sequence. But there are numerous potential starts and stops, and several of them over; what does this mean?

An essential part of the process of reading text is to separate the constituent characters. In words, we saw that there are several frames in which a genomic sequence can be read, of which three are in a given triplet triplet. Suppose we start arbitrarily from the first nucleotide and delineate the triplet words – this transformation is shown in Figure 4.3(a).
