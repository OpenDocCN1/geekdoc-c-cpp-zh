# Bioinformatics at the interface of biology and computer science

+   (a) 5' A T G T A T C A T A A T C G T A 3'
Forward frame 1 --- Met Leu Ile Val
1 2 3 1 2 3 2 1 3 1 2 3 1 2 3
Forward frame 2 --- Cys Tyr Pro Stop Stop
1 2 3 1 2 3 2 1 3 1 2 3 1 2 3
Forward frame 3 --- Val Ile His Asn Arg
1 2 3 1 2 3 2 1 3 1 2 3 1 2 3

![](bbox=[0.297, 0.226, 0.843, 0.303])

+   (b) 5' T T T A C G A T T A T G A A A C T 3'
Reverse frame 1 --- Arg Leu Trp Ile Thr
1 2 3 1 2 3 2 1 3 1 2 3 1 2 3
Reverse frame 2 --- Tyr Asp Tyr Stop His
1 2 3 1 2 3 2 1 3 1 2 3 1 2 3
Reverse frame 3 --- Thr Met Asn
1 2 3 1 2 3 2 1 3 1 2 3 1 2 3

Figure 2.19

Conceptual translation of DNA in three forward frames (a) and in reverse frames, which are equivalent to three forward frames of the reverse complement (b). The red arrow denotes frames of the reverse complement; the green arrows denote the direction of translation from the start codons in the first forward frame and in the third frame of the reverse complement.

many likely sources of error: e.g., DNA sequencing errors may result in incorrectly assigned or missed start/stop codons, leading to translation of a gene, extension of a gene, or miss completely. Sometimes there are overlapping ORFs (whether on the same or opposite DNA strand), and sometimes the shorter of the two is the real gene! Figure 2.20 illustrates the sort of complexity that arises from overlapping ORFs in different reading frames.
as a result of these complications, evidence from a variety of sources needs to be used to confirm whether the sequence encoded in an ORF is a protein. One method of confirmation is to search a protein sequence database to discover whether something like this sequence already exists (a step that would be possible, of course, if comprehensive sequence databases werent readily available). Another method is to

| F1 |
| F2 |
| F3 |
| R1 |
| R2 |
| R3 |

Figure 2.20

Distribution of ORFs in three forward (F) and three reverse (R) reading frames of a sequence of DNA. The horizontal grey bars show reading frames; the blue blocks denote ORFs. Here, there are numerous ORFs in each frame, and in overlapping positions. This complexity makes gene finding difficult.