# Automated Annotation Systems ■ 135

want to exclude genes with strong similarity to “Homo sapiens,” “human” or “9606.” Any of these terms would map to the appropriate taxonomy filter. This filter is made possible by maintaining an index of the NCBI taxonomy and its mapping to public protein IDs.

The fifth type of search is sequence-based. The user may have the DNA or protein sequence of a gene of interest from another organism. A sequence search is a guaranteed way to find related genes in the new genome regardless of the functional annotation results. Conversely the sixth search type, specifying a minimum or maximum match similarity against public databases, can be used to quickly screen for novel (or well-known) genes. Finally, the seventh search allows the user to focus on very long or very short genes as desired.

In summary, MAGPIE provides all of the key features for structural and functional annotation of a genome, including synthesis of data from many analysis tools, and with extensive facilities to interrogate the results. The implementation of these features in other systems will be viewed as how different approaches can be taken for the same tasks.

# 8.3 GENERIC MODEL ORGANISM DATABASE

The Generic Model Organism Database (GMOD; http://gmod.org) is a well-known community-driven effort to build reusable components for the storage, analysis, and display of genomic information. Within the large set of software tools GMOD makes available is an automated system called MAKER (Cantarel et al., 2008). MAKER can be used for annotation in prokaryotic and smaller eukaryotic genome projects, creating genome databases that can be used by other GMOD components.

# 8.3.1 Analysis Management

Command-line based like MAGPIE, MAKER uses an internal job management system, the text logs of which the user can review. Data is also stored in flat files except when there are more than 1000 sequences in the project. In this case a custom data store contains the analysis results. Job parallelization on a single machine is achieved by running the analysis launcher several times in a row or by configuring the system’s Message Passing Interface (MPI).

# 8.3.2 Structural Annotation

MAKER first identifies repeats in the genome and masks them. It then aligns ESTs and proteins to the masked genome. By default, SNAP (Korf,