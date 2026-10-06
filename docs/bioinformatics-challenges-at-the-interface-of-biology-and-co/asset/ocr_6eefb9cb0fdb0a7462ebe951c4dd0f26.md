# Chapter 5 The gap

little functional information they actually convey compared to the much terser, more precise GO annotations. The kind of formalism used in GO may feel a little more uncomfortable to the human reader, if we're to use computers in function-annotation tasks, but essential if we're able to more readily relate different terms or in different databases. Colourful, ad hoc nomenclature systems of the sort that appear to delight geneticists, are the source of bioinformatics (Pearson, 2001). In particular, those that include familiar, everyday words to describe biological entities (gene names like hedgehog, hairy, keen, tshirt, cap 'n' lost in space, etc.) define systematic analyses and quickly lose their amenity when faced with the task of trying to train computers to discover them in scientific texts, to link them to related concepts in databases that use different nomenclature systems, and ultimately to teach computers what they mean.

# 5.13 Summary

This chapter introduced some of the issues that have arisen as bioinformatics tools and databases have been moulded and adapted in ad hoc ways to tackle new problems. Specifically, we saw that:

+   1 The concept of a 'gene' is fluid and have different meanings for different scientists;
2 Genes are difficult to find and build computationally; their counts in newly sequenced genomes are therefore predictions that are subject to iterative refinement over time;
3 Genes and proteins may have different names in different species; tracking their occurrence in the literature and in databases requires the assistance of synonym dictionaries;
4 Protein sequences change over time, and the changes are tracked by means of their database identifiers and accession numbers;
5 Occasionally, the same accession number can point to different sequences – such changes can be tracked by means of the sequence version numbers in UniProtKB, and in the protein archive, UniProt;
6 The contents of database entries change over time, including the names of the entities and the data; this instability can make it difficult to know what biological entity a particular database entry refers;
7 Some databases may point to experimentally determined 3D structures; when numerous structures are linked to the sequence, it can be difficult to know which is the most appropriate or relevant to that entry;
8 Different alignment tools give different results; understanding the methods that give rise to them;
9 Different alignment tools present their outputs in different ways; understanding the outputs (in terms of properties they share or how similar sequences may be) is facilitated by the use of colour schemes;
10 Different colour embed entity metaphors; understanding the underlying metaphor is crucial for interpreting alignment outputs mean;
11 Structure-based alignments are fundamentally different from sequence-based alignments; they use different frames of reference and are not directly comparable – nevertheless, many sequence alignment tools are still benchmarked against structure-based alignments;