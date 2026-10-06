# Bioinformatics challenges at the interface of biology and computer science

compared to ~150,000 structures in the ASD (which is this unfair comparison, as small-molecule structures present fewer obstacles to structure determination than proteins and nucleic acid complexes). Perhaps a more pressing highlighted by the 1977 holdings that the database was beginning to accrue a significant amount of redundancy – by 1992, this was calculated to be ~7-fold (Berman, 2008; Hobohm et al., 1992). This redundancy was an inevitable consequence of the nature of structural research.

Structural studies are immensely valuable. For example, they've shown that the physical similarities shared by some proteins reflect common descent during evolution, during which mutations (substitutions, insertions and/or deletions) have accumulated in their sequences. For distant proteins, such mutations can be extensive, yielding folds in which the numbers and orientations of structures vary considerably, while basic scaffolds nevertheless act to preserve the structural environments of critical functional or active-sites. The diversity and elegance of such protein scaffolds has been captured in a number of fold-classification databases, which are described in more detail in Box 3.1.

# Box 3.1 Structure classification databases

The PDB is highly redundant. This is largely because of the nature of scientific research, which increases our knowledge by repeating detailed analyses of the same system until its intricacies are understood. The earliest protein structures to have been deduced (i.e. from myosin and hemoglobin) have therefore been determined, in order to better resolve their atomic structures and to learn more about the biological and biochemical mechanisms they use to effect their molecular functions.

By rationalising the structural data we have at our disposal, we can begin to put in suitable foundations from which to refine our understanding of structural principles – it turns out that nature use only a limited 'representation' of folds from which to build its portfolio of protein architectures (i.e., the method used is highly redundant too). Some of the systematic approaches to rationalise the structural data have yielded folds (for use in structure prediction and/or data-mining methods) and more comprehensive fold-classification databases, like SCOP and CATH. These groups share common folds and domains; however, in so they use different hierarchical approaches. Let's take a look.

The SCOP (Structural Classification Of Proteins*) hierarchy attempts to classify proteins into evolutionary and structural relationships. This task is complicated by the fact that protein structures are highly diverse; some comprise only single domains, while others are multidomain assemblies (hence, some are classified as individual domains and as multidomain proteins). This isn't an exact instance, of course, and so algorithms for comparing structures can't always capture the complexities completely; SCOP employs both manual and automated methods.

SCOP's hierarchy has three levels: family, superfamily, fold. The boundaries between these may be subjective, but higher levels generally reflect the clearest structural:

+   1. at the family level are proteins that >30% per sequence identity;
2. at the superfamily level are proteins that are believed to share a common evolutionary origin based on structural functional characteristics, but rather on moderate sequence identity;
3. at the fold level are proteins that have the same organisation of secondary structures, irrespective of their evolutionary origins (i.e., regardless of the mechanisms of divergence or convergence).

> *http://scop2.mrc-lab.cam.ac.uk