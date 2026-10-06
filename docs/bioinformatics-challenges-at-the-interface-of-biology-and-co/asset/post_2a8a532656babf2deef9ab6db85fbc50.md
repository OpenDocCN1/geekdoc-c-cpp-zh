
# Bioinformatics challenges at the interface of biology and computer science

![](img/1af42ff402ef4720886c50af0bb8e9b5_83_0.png)

### Figure 3.3
Illustration of the growth of TrEMBLI¹ (purple line), Swiss-Prot® (red line) and PDB (green line). The gulf between manual-annotation and computer-annotation strategies is clear, as is the size of the current sequence-structure deficit.
*http://www.ebi.ac.uk/unprot/TrEMBLstats
*http://web.expasy.org/docs/relnotes/list.html

organisations, their family and disease relations, their sequence variants, structural information, relevant literature, and so on. The extent and quality of this information set Swiss-Prot apart from other sequence databases and ensured its popularity, but there was a price to pay: providing comprehensive annotation for the ever growing volume of sequences demanded by import and more. It would take an entire army to keep pace with the rate of data acquisition from the sequencing centres. The unfortunate truth is, manual annotation simply does not scale, as illustrated in Figure 3.3. By October 2015, Swiss-Prot contained 549,832 entries (derived from >13,000 species, mostly from organisms—human, mouse, Arabidopsis, rat, yeast, etc.). This figure is an order of magnitude smaller than the holdings of its companion database, TrEMBL, as we shall see in Section 3.9.

# 3.8 PROSITE

An almost inevitable consequence of the systematic collection of protein and nucleotide sequences into databases was the desire to organise and classify these molecular entities in meaningful ways. The first attempt to categorise protein sequences into evolutionary related families, and to provide diagnostic tools to help detect new family members, again arose as a part of Bairoch’s PC/Gene software package (more detailed information about protein families and their broad diagnostic approaches is in Box 3.2).

Bairoch had reread Doolittle’s newly published sequence analysis primer, Of URFs and ORFs (Doolittle, 1988). Inspired, he began creating a compendium of short sequences (so-called consensus expressions or patterns–see Box 3.3) that were, according to literature and other sources, known to be characteristic of particular protein families or of binding and/or active sites. At the same time, he developed a program

> ¹http://liste.expasy.org

### Box 3.2 Protein family signatures

Many proteins show evidence of evolutionary kinship; highly similar sequences are likely to have descended from a common ancestor. We can use these similarities to group sequences into families: this is useful, members of such families (not always) have the same or related functions.

Classifying sequences into families is not just a stamp-collecting exercise. An enormous challenge facing bioinformatics is to provide some level of annotation (including, evidence, of their potential functions) to the members of sequences billowing from world-wide sequencing projects into our databases. The idea is if we can discern the essence of particular protein families into ‘signatures’ of some sort, then these could provide the means to diagnose hundreds or thousands of uncharacterised sequences.

Over the years efforts to create diagnostic signatures have produced several different databases. The methodologies are different, but the central principle is the same. Essentially, when related proteins are compared by their sequences, blocks of conservation become visible, separated by non-conserved regions. The conserved blocks, usually referred to as motifs, can be thought of as signatures of substantial change. In Figure 3.4 sequences are compared by horizontal bars. Sequences have different lengths for the shorter sequences, this necessitates the addition of gaps to downstream regions to be brought into the correct register, which is why some of the bars are broken. Figure 3.4 shows three islands of conservation, three motifs (the yellow boxes), emerging in this way.

![](img/1af42ff402ef4720886c50af0bb8e9b5_84_0.png)

Figure 3.4
Three motifs in a sequence alignment.

Here, the motifs are aligned because the aligned sequences are very similar. For more dissimilar or divergent sequences, alignment is more difficult, the regions of conservation shrink, and it becomes harder to spot motifs, as shown in Figure 3.5.

![](img/1af42ff402ef4720886c50af0bb8e9b5_84_1.png)

Figure 3.5
Alignment of increasingly divergent sequences.

In this example, an initial comparison of highly similar sequences highlights two well-defined conserved regions (the green blocks). As more dissimilar sequences are included in the alignment, however, the patterns of conservation change, and gradually smaller, until eventually only four tiny remain (the small pink blocks).

Motifs like this lie in different parts of the genome, may nevertheless come close to each other in 3D as the sequence adopts its tertiary structure. Typically, such motifs include amino acids at particular positions, reflecting some structural or functional role that has been preserved through the usages of evolution (a catalytic or binding site, or some kind of folding knot). As a result, they can provide powerful signatures that can, in principle, allow us to make highly functional and structural inferences, say, for uncharacterised sequences share the same motif.

There are several ways of encoding the conserved parts of alignments, which have different diagnostic consequences. The three main approach single motifs (the method originally used in PROSITE), multiple motifs (as used in the PRINTS and Blocks databases) or complete domains (as used in the Profiles and Pfam databases). More details of these methods are given in Chapter 4.

to scan this sequence of patterns, that so could test or diagnose the presence of characteristic sites in their own sequences. This part-program, database called PROITE⁹ (Bairoch, 1991). Its first release, in March 1998, contained 58 entries. As the beginning, the database was very small, which much restricted its utility. To expand the coverage, users began to suggest additional patterns. Furthermore, its growing user community urged Bairoch to liberate PROITE from the commercial shackles of PC/Gene He bowed to this pressure the following year, announcing a new version in October 202

-OPRD AYSCAVCAVGLLVVMMIRYRTKM
OPRD_RAT   AYSCAVCAVGLLVVMMIRYRTKL
OPRD_MOUSE AYSCAVCAVGLLVVMMIRYRTKL
OPRK_HUMAN AYSVVSVVEVGLNSLMFFIYTKM
OPRK_RAT   AVYSVVSVEVGLNSLMFFIYTKM
OPRK_MOUSE AVYSVVSVEVGLNSLMFFIYTKM
OPRM_HUMAN AYSCAVCAVGLLVVMMIRYRTKM
OPRM_RAT  AVYSIVVCVGGLGNFGLVMMYIYRYTM
OPRM_MOUSE AYSIVVCVGGLGNFGLVMMYIYRYTM
Consensus  AS S VGL GN LVM R YTM

### Box 3.3 Consensus sequences and patterns

```
OPRD_HUMAN AYSCAVCAVGLLVVMMIRYRTKM
OPRD_RAT   AYSCAVCAVGLLVVMMIRYRTKL
OPRD_MOUSE AYSCAVCAVGLLVVMMIRYRTKL
OPRK_HUMAN AYSVVSVVEVGLNSLMFFIYTKM
OPRK_RAT   AVYSVVSVEVGLNSLMFFIYTKM
OPRK_MOUSE AVYSVVSVEVGLNSLMFFIYTKM
OPRM_HUMAN AYSCAVCAVGLLVVMMIRYRTKM
OPRM_RAT  AVYSIVVCVGGLGNFGLVMMYIYRYTM
OPRM_MOUSE AYSIVVCVGGLGNFGLVMMYIYRYTM
Consensus  AS S VGL GN LVM R YTM
```

When related sequences are aligned, regions that have survived the mutational pressures of evolution often stand out more highly than others, because they share higher levels of similarity than surrounding parts of the alignment. These regions include key conserved residues at aligned positions, and can serve as diagnostic landmarks against which other sequences can be compared.
A simple way to visualise conservation is to read sequences into an alignment editor providing a rapid visual of residues that are highly or completely conserved, as shown in Figure 3.6.

Figure 3.6
Alignment with its consensus sequence.

Figure 3.6 shows part of an alignment of nine sequences (human, rat and mouse, mu and kappa receptors), where 17 of the 27 residues are completely conserved, denoted by the amino acid letter codes in the Consensus row beneath the alignment. Where alignment positions contain several different residues, a darker shade is used: the darker the shade, the greater the number of different residues at that position. The largest number of residues at a position is 3; positions 5, 12 and 15 have the darkest colour.
In this alignment, residues are colored according to their physicochemical properties described in Section 2.2.3. The uniformity of colour in some columns shows that, even if a particular residue is not conserved, its properties have been preserved at this position. Consider column: 5 the consensus indicates that it is one of the most variable positions; nevertheless, the colour
