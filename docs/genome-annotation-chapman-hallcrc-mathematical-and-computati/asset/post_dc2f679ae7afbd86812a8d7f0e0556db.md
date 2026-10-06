
## Functional Annotation ■ 109

### Positive examples

| THE LAST FAT CAT |
| THE FAST CAT |
| THE VERY FAST CAT |
| THE FAT CAT |

Query #1

| THE VAST FAST CAT |

Query #2

| THE LAST VERY FAST CAT |

Multiple sequence alignment (e.g., ClustalW or T-coffee)

### Position-specific positive examples

| THE LAST FA T CAT |
| THE FAST CAT |
| THE VERY FAST CAT |
| THE FA CAT |

HMM build + calibrate

![](img/7da802df4d7c0829a4a41adf9acaf30d_131_0.png)

Hidden Markov Model

HMM search

THE VAST FAST CAT

Only "VERY, LAST," or nothing allowed in in second word positions

+++ ++++ ++++

V from VERYAST from LAST

> Figure 7.1 An example of how a hidden Markov model (HMM) is built and how the matching is not pairwise (the first query instance matches even though VAST does not appear in the training set) as well as being position specific (the second instance does not match, because the LAST and VERY are mutually exclusive in the training set).

Protein sequences can be compared to an HMM using the HMMer software (Finn et al., 2011) or a hardware accelerator such as the TimeLogic DeCypher system (Active Motif, Carlsbad, California). Version 3 of HMMer forgets the exhaustive Viterbi algorithm (Forney, 1973) used to optimally match the HMM and instead opts for a few assumptions to achieve 100-fold speedup in search time. A caveat of HMM3 (Eddy, 2011) is that the heuristics that allow this speedup can also generate matches to partial domains with significant e-values. As these domains are incomplete, they are most likely nonfunctional. Older HMMer searches and Viterbi alignments, such as those found in the toolkit included in the DeCipher system, will not report partial model traversals. In some situations, the partial matching may be useful, as the identification of truncated gene prediction. For example, if the C-terminus of a predicted protein contained a strong partial match to the N-terminal domain of glycerol kinase, it is likely that the predicted and stop codon of the gene are incorrect or the genomic DNA sequence has been misassembled.

Alternative methods for modeling domain constraints have also been implemented. RPS-BLAST (Altschul et al., 1997) can be used to search specially formatted position-specific scoring matrices, which are created from PSI-BLAST-derived models of protein domains. PROSITE (Hulo et al., 2007) provides both Gribkov profiles similar to HMMs but less probabilistic and regular expressions to smaller protein domains. The PRINTS database (Attwood et al., 2003) employs a search for multiple, closely spaced areas of high conservation, ignoring areas a larger HMM might loosely.

The construction of domain models, regardless of the representation used, typically involves the automated detection of potential positive examples, followed by the manual curation of these examples. The model statistics are then calibrated as necessary to reduce false positives, minimizing negatives. Annotation of the function of the protein domain is also generally a manual process. Many different models could be derived for the same protein domain, depending on the source for positive examples, the underlying PM mechanism used, and the subsequent manual curation steps. Several domain databases exist, and large such as Pfam (Finn et al., 2010) and PANTHER (Thomas et al., 2003) have somewhat overlap deunify and somewhat distinct model sets.

In order to unify these data collections, the InterPro Consortium (www.ebi.ac.uk/interpro) was created to correlate models from all of the main providers, assigning related models to named families and using a common identifier system. It is important to note that InterPro does not contain any domain models, rather it points to the models of the individual providers. As illustrated in Figure 7.2, InterProScan (Zdobnov and Apweiler, 2001) simplifies analysis by providing a unified search result from the various HMM, RPS-BLAST, and PRINTS searches.

## Functional Annotation 111

![](img/7da802df4d7c0829a4a41adf9acaf30d_133_0.png)

FIGURE 7.2 Unified, protein domain output from InterProScan, showing the different ways in which the same domain can be modeled.

In the example shown in Figure 7.2, two models are grouped together in each of three categories. The identifiers on each match line identify the source database of the model. For instance, in the InterPro Match IPR005999 (Glycerol kinase), PTHR01096:SF9 is from the PANTHER database (Thomes et al., 2003), while the similar TIGR01311 is from TIGRFAM (Haft et al., 2003). The interpretation of these InterProScan results requires some observations. First, clearly different domain models provide different coverage of the 501 amino acid query sequence. In cases, the N- and C-termini are modeled separately. In other cases (PROSITE motifs PS00445 and PS00933 in IPR018483), only a very small and highly conserved region is modeled. Second, it is not necessarily obvious that all of the InterPro categories (noted by IPR numbers) are interrelated. This is a possibly multifunctional gene? Good background knowledge or traversal of the IPR ID hierarchy is necessary to discover that all IPR terms fall into a tight branch of the protein domain hierarchy. Third, which is the most functional description that can be reasonably assigned to the query gene? Examining the text output from InterProScan is necessary, as it lists the expectations (e-values) for the domain matches. Glycerol kinase is the most specific term in the hierarchy, and the e-value for its functional assignment is 0, indicating that this is a strong match: glycerol kinase is therefore a reasonable annotation for the query protein. In cases where e-values are closer to 1, the interpretation is more difficult, especially because the different model sources do not necessarily share the same statistical model.

## 112 Genome Annotation

Despite these caveats, protein domain matches still tend to provide more sensitive, less redundant and often better-annotated results from the output of pairwise search methods, such as BLAST.

A large database notably absent from InterPro is the Conserved Domain Database (CDD) (Marchler-Bau et al., 2011), with its accompanying CD-Search software. Although this database partially overlaps in its sources with InterPro, it includes two unique and significant sources: Clusters of Orthologous Groups of proteins (COGs) (Tatusov et al., 2003) and the NCBI Protein Clusters (Sayers et al., 2010). As such, any thorough genome annotation system should make use of CDD as well as InterPro to obtain a complete picture of protein domains.

## 7.4 SIMILARITY SEARCHES

By the most common method for functional annotation is based on similarity searches. The premise of this method is that a high degree of pairwise nucleic acid and/or amino acid conservation between an already characterized and annotated gene sequence and a query sequence also implies conservation of the function, which was determined for the first gene sequence. This simple premise is complicated to implement in practice, because similarity is in many cases or less a continuum, rather than a yes-no trait. While each piece of software will use its own e-value guidelines on homology detection for functional annotation (see Chapter 8), the definition of homologous sequences is based on the origin of the related genes and not on simple sequence similarity. Key types of homologs are described according to these origins.

### 7.4.1 Paralogs

Any organism may contain several similar genes that originate from a single instance of the gene, which has undergone one or more duplication events during evolution. Over time, these genes tend to specialize in their function, might be expressed in specific tissues or might show ligand specificity (Guillén et al., 2010). If one instance of such a gene sequence has been already characterized, it is usually reasonable to infer a similar function for the other members of the gene family based on very strong amino acid level pairwise similarity (e.g, e-value < 10⁻⁵). In terms of nomenclature, typically paralogs constitute a gene family with similar gene symbols, such as *hox1*, *hox2*, and *hox3*. HOX in particular is a large, ancient paralog family, predating modern chordate evolution, and it is therefore challenging to trace the duplication sequence precisely (Hughes
