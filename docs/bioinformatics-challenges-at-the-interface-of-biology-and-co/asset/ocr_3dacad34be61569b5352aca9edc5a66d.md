# Box 3.2 Protein family signatures

Many proteins show evidence of evolutionary kinship; highly similar sequences are likely to have descended from a common ancestor. We can use these similarities to group sequences into families: this is useful, members of such families (not always) have the same or related functions.

Classifying sequences into families is not just a stamp-collecting exercise. An enormous challenge facing bioinformatics is to provide some level of annotation (including, evidence, of their potential functions) to the members of sequences billowing from world-wide sequencing projects into our databases. The idea is if we can discern the essence of particular protein families into ‘signatures’ of some sort, then these could provide the means to diagnose hundreds or thousands of uncharacterised sequences.

Over the years efforts to create diagnostic signatures have produced several different databases. The methodologies are different, but the central principle is the same. Essentially, when related proteins are compared by their sequences, blocks of conservation become visible, separated by non-conserved regions. The conserved blocks, usually referred to as motifs, can be thought of as signatures of substantial change. In Figure 3.4 sequences are compared by horizontal bars. Sequences have different lengths for the shorter sequences, this necessitates the addition of gaps to downstream regions to be brought into the correct register, which is why some of the bars are broken. Figure 3.4 shows three islands of conservation, three motifs (the yellow boxes), emerging in this way.

![](bbox=[0.166, 0.413, 0.821, 0.503])

Figure 3.4
Three motifs in a sequence alignment.

Here, the motifs are aligned because the aligned sequences are very similar. For more dissimilar or divergent sequences, alignment is more difficult, the regions of conservation shrink, and it becomes harder to spot motifs, as shown in Figure 3.5.

![](bbox=[0.166, 0.574, 0.821, 0.664])

Figure 3.5
Alignment of increasingly divergent sequences.

In this example, an initial comparison of highly similar sequences highlights two well-defined conserved regions (the green blocks). As more dissimilar sequences are included in the alignment, however, the patterns of conservation change, and gradually smaller, until eventually only four tiny remain (the small pink blocks).

Motifs like this lie in different parts of the genome, may nevertheless come close to each other in 3D as the sequence adopts its tertiary structure. Typically, such motifs include amino acids at particular positions, reflecting some structural or functional role that has been preserved through the usages of evolution (a catalytic or binding site, or some kind of folding knot). As a result, they can provide powerful signatures that can, in principle, allow us to make highly functional and structural inferences, say, for uncharacterised sequences share the same motif.

There are several ways of encoding the conserved parts of alignments, which have different diagnostic consequences. The three main approach single motifs (the method originally used in PROSITE), multiple motifs (as used in the PRINTS and Blocks databases) or complete domains (as used in the Profiles and Pfam databases). More details of these methods are given in Chapter 4.