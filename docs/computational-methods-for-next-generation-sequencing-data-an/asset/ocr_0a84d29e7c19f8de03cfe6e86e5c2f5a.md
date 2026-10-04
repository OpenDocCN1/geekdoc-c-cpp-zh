# BISULFITE-CONVERSION-BASED METHODS FOR DNA METHYLATION SEQUENCING 233

uses ta-and and cg-bit representations for genome and reads. Here, we give an example for a read and the genome's k-mer of the length that shows possible mappings of a letter to a letter in a genome. Let AAAACCCCCGGGGTTTT be a sequenced read and ACGTACGTACTACGT be a 16-mer in the genome. The ta-representation of the read (ta-read) is 0000111011100111 and cg-representation of the read (cg-read) is 00001111110000. Similarly, the genome's 16-mer (ta-gen) is 01010101010101 and cg-representation of the genome's 16-mer (cg-gen) is 01100111001110. BRAT uses bit-wise logical operations XOR, OR, AND, and NOT to allow BS-mismatches in an alignment. To allow for T in a read to map C in a reference, the following statement is used:

```
((ta-read OR cg-read) AND cg-gen-mer)
(cg-read XOR (ta-read AND cg-gen-mer)) OR
(ta-read XOR ta-gen-mer)
```

For example, one applies this logic statement to our example of aligning the read AAAACCCCCGGGGTTTT to the genome's 16-mer ACGTACGTACTACGT, which is 0111011111011010, where the 7th position indicates a mismatch between the 7th letter in the read and the 7th letter in the genome, and 0 corresponds to a match. We can observe that the only matches that are allowed are A-A, C-C, G-G, T-T, and T-C.

To allow for A in a read to map to G in a genome, BRAT performs the following operation:

```
((tareadAND (NOT cg-read)) AND cg-gen-mer)
(cg-read XOR (cg-read AND cg-gen-mer)) OR
(ta-read XOR ta-gen-mer)
```

When applying this procedure to example, we obtain 0110101111110111110, which demonstrates that the only matches that are allowed in this case are A-A, A-G, C-C, G-G, and T-T.
 distinguish between PCR reads, BRAT uses the strategy described earlier. When the 5' maps to DS+ allowing only T-C mismatches, the read comes from PCR+ strand; mapping of 5' to DS+ allowing A-G mismatches indicates that the orientation of the read is PCR+ strand; if the reverse-complement of 5' maps to DS+ allowing A-G mismatches, then the read comes from PCR- strand; and finally, if the reverse-complement of a read is generated from PCR- allowing T-C mismatches, then the read that are resulted in the same-scored best alignments in two or out of total four possible mappings are disregarded from the further analysis of methylation status estimation. For directional bisulfite libraries, two full-length alignments are performed for each read: an original to DS+ allowing only T-C mismatches, and the reverse-complement of DS+ allowing only A-G mismatches. As non-directional libraries, if both of these mapping result in the same best-score, the read is disregarded from further consideration.