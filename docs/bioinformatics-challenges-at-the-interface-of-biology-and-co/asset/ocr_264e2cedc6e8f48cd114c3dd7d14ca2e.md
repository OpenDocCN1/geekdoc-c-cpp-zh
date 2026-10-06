# Chapter 4 Biological sequence analysis

# Box 4.3 The Twilight and Midnight Zones

The goal of many sequence analysis tasks is to identify relationships between new, often uncharacterised sequences and those that have been deposited in databases, and hence whose functions (possibly structures) we have already elucidated. At high levels of sequence identity, where sequence alignment methods perform relatively reliably, this is reasonably straightforward (although, even for highly similar sequences, there are still traps for the unwary). Below 50 per cent identity, however, it becomes increasingly difficult to establish relationships with confidence, as depicted in Figure 4.17.

![](bbox=[0.157, 0.243, 0.796, 0.373])

# Figure 4.17

Tools for probing the Twilight and Midnight Zones.

Analyses can be probed with decreasing certainty towards what has been termed the “Twilight Zone a region of ~15–25 per cent identity in which alignments may seem plausible to the eye but not statistically significant—ie., the same alignment could arise by chance (Doodittle, 1996).
Many analytical methods have been developed to penetrate deep into the Twilight Zone, ranging from pairwise alignment to consensus or profile methods. Each of these approaches a slightly different perspective, depending on the type of information used in the search (whether implementing pairwise or multiple sequence comparisons, substitution probability matrices or frequency matrices, etc.). It is important to appreciate, that there's a theoretical limit to the effectiveness of sequence-based methods. The problem is that for distant proteins, tertiary structures are more conserved than their primary structural features. This means that evolutionary relationships are apparent only at the level of shared structural features, which cannot be detected even by the most sensitive sequence comparison methods. In the region of identity where sequence comparisons fail to detect structural similarity has been termed the Midnight Zone (Rost, 1998). The Midnight Zone also denotes a philosophical limit to our ability to detect significant sequence similarity we cannot know whether structural similarities have arisen from a divergent evolution from a common ancestor or as a result of convergent evolution to a favourable or stable packing arrangement.
Exploration of the Midnight Zone requires structural approaches (such as fold recognition), which are outside the scope of this book.

For mathematical convenience, the PAM250 mutation probability matrix is expressed as a log-odds matrix, as illustrated in Figure 4.18. Here, positive values denote likely mutations, negative values denote unlikely mutations, and values equal to zero are neutral. The amino acids have been grouped to try and reflect their physicochemical properties. Closer inspection of the matrix reveals that the pattern of substitution probabilities is broadly consistent with our intuition that chemically similar amino acids are more likely to replace each other: the acid/amide group, the basic group, the aliphatic group, and so on. These patterns of replacement reflect the similarity of the roles