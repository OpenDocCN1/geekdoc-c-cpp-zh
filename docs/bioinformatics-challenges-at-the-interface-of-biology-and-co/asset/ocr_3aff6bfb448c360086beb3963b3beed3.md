# Chapter 4 Biological sequence analysis

# Table 4.1

Example functional sites and consensus patterns used to detect them.

| Functional site | Pattern |
|---|---|
| Amidation | x G [RK] [RK] |
| ATP/GTP-binding (P-loop) | [AG] x(4) G [ST] |
| N-glycosylation | N [P] [ST] [P] |
| N-myristylation | G [EDRKIPFY] x(2) [STAGCN] [P] |
| Casein kinase II phosphorylation | [ST] x(2) [DE] |
| Protein C phosphorylation | [ST] x [RK] |

is relevant to the patterns in which they're found (which can only be verified experi-mentally). When searching PROSITE, these frequently occurring patterns may be 'switched off' (the Web pages provide an option to this), unless there's good reason to think that the query sequence may be phosphorylated, glycosylated, or whatever.

At one time, such patterns were called 'rules', to differentiate them from the familily-specific expressions; although this term seems to have fallen out of favour, you may still find articles, books and other documents that use it. However, the term should not be confused with ProRule: this is a database containing additional information to enhance the performance of various PROSITE profiles and patterns e.g., as the positions of structurally or functionally critical amino residues, and the conditions they must fulfill in order to play their particular biological roles (Sigrist et al., 2005).

# Fingerprints

As we've seen, the simplistic nature of consensus expressions has diagnostic limit-ations: they perform well in identifying short, conserved sequence features, but are efficient at designing members of divergent superfamilies. One of their principal drawbacks hangs on the phylogeny of using motifs. In practice, when we examine multiple sequence alignments, it is usual to find not one, but several motifs. Diagnostically, it makes sense to use many, or all - intuitively, to build a characteristic signature or 'fingerprint' of the family - intuitively, we know that the more information there is in a fingerprint (in this case, the more motifs), greater its potency. As diagnostic tools, fingerprints are more than collections of motifs - the order in which motifs appear in alignments and the distances between them are also key to the underlying analytical model. The concept of a protein fingerprint introduced in Box 3.4 adds to the concept and explain fingerprints are created and used in practice.

Figure 4.28 illustrates an analysis of hemoglobin alpha chains, with four motifs highlighted (the rectangular boxes). Seed alignments like this, ungapped motifs are excised and used to scan a sequence of UniProtKB from which sequence fragments have been removed. The database-scanning algorithm translates the motifs into a set of simple identity or frequency matrices - no scoring matrix is used to weigh the results, as shown in Figure 4.29. This means that the resulting matrices are relatively sparse, and hence that the searches are fairly selective. It's partly this selectivity that fingerprints allow to differentiate highly similar sequences and resolve them into closely related families and subfamilies; the corollary of this is that the method is