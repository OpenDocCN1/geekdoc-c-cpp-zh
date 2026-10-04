
# MICROBIOME ANALYSIS: STATE OF THE ART AND FUTURE TRENDS

MITCH FERNANDEZ, VANESSA AGUIAR-PULIDO, JUAN RIVEROS, AND WENRUI HUANG

Bioinformatics Research Group (BioRG), School of Computing and Information Sciences, Florida International University, Miami, FL, USA

JONATHAN SEGAL
Herbert Wertheim College of Medicine, Florida International University, Miami, FL, USA

ERLIANG ZENG
Department of Computer Science and Engineering, University of Notre Dame, Notre Dame, IN, USA

MICHAEL CAMPOS
Miller School of Medicine, University of Miami, Miami, FL, USA

KALAI MATHEE
Herbert Wertheim College of Medicine, Florida International University, Miami, FL, USA

GIRI NARASIMHAN
Bioinformatics Research Group (BioRG), School of Computing and Information Sciences, Florida International University, Miami, FL, USA

## 18.1 INTRODUCTION

Microbes form complex heterogeneous interacting communities, whether in the environment or in specific niches within humans and other organisms (1). Metagenomics approaches have been used to study the composition and dynamics of such microbial communities. Distinct communities of bacteria are present at different sites of the human body.

It is possible to employ classical microbiological methods for the analysis of microbiomes, which could culture individual taxon and then use specific protocols to identify them. However, classical approaches will be limited by (i) the ability to culture—it is broadly believed that most bacterial taxa are not readily culturable by traditional techniques (although more extensive cultivation approaches have yielded considerably higher percentages of cultured taxon, as shown by the work of M. Sarette and colleagues (8)); (ii) time takes to culture—it could take several weeks for a culture to grow; and (iii) the potentially staggering number and diversity of microbial taxon in the sample.

Molecular approaches involve extracting microbial DNA from a sample followed by a process of determining the microbial community present. A reasonable approach is that of PCR amplifications of marker genes, as for the 16S rRNA, followed by one of a variety of approaches to investigate length heterogeneity of variable regions of the microbial genomes (9). Here, the limitations are the result of the fact that length heterogeneity of specific regions of marker genes in the bacterial world is considerably smaller than the number of taxa.

Exploiting sequencing is clearly a more informative approach than using length heterogeneity. The DNA is first extracted and a portion of the genome is amplified with appropriate PCR primers. Then, next-generation sequencing techniques generate a large number of reads from amplicons. Bioinformatics tools are finally used to classify the reads by the different taxa from they have arisen.

Although this was discussed in detail, the limitations of these methods are the following: (i) the extent of our databases and the sequences cataloged in them (ii) next-generation sequencing techniques produce short reads that may or not be from regions of the individual taxon; and (iii) the software classifier used to classify individual reads that may produce inaccurate results, in part, because the independence assumptions inherent in existing classifiers may be biologically valid.

Microbiome studies have largely relied on phylogenetic marker genes, most often the 16S rRNA (see References 10–15), which include 23S rRNA, recA, gyrA, and many more (16–19). There is no consensus on the ideal marker gene, and the popularity of 16S rRNA is simply due to use in standard reference manuals (19). However, recent studies have taken a different approach by employing whole genome sequencing (7, 20, 21). The advantage of availability of large databases (22–24) to aid in classification of reads. The advantage of the whole genome approach is that it becomes possible to obtain functional profiles of the microbial community by investigating the functional annotations of which the reads map. We discuss later why this is potentially of greater interest than the marker gene approach.

Regardless of the method of identifying bacterial taxa or the functional elements present, the next step is to leverage the information to understand the difference between samples. Such measures include α and β-diversity indices, which have been shown to be useful in distinguishing between samples (25, 26). Specific indices for calculating these types of diversity include the Shannon diversity index, for measuring similarity between samples by the proportion of shared clusters or species between them (28); and the popular inverse-Simpson index, which estimates diversity by considering the probability that a randomly selected individual from a sample has already been observed (27). It should be noted that there are situations where well-established diversity indices are not sufficient to differentiate groups of samples. In recent studies, it has been observed that the diversity indices for the airways smoking and nonsmokers are not distinguishable, even though these have readily identified bacterial genera that tend to favor the airways of nonsmokers or former smokers (30, 31).

More advanced techniques to understand and differentiate microbial community profiles have been investigated. It is clear that metagenomic studies have to go further and dig deeper to uncover interesting features of microbial communities. The next set of promising investigations have to focus on understanding the structure of microbial communities and their interactions in any environmental niche. One of the greatest challenges in understanding human health is the large number of complex interactions that occur within the microbial community, and between the community and the human host. There is a great need to interpret the results in a way that is useful to both research scientists and clinicians. Studying the structure of microbial communities will shed light on the nature of the.

## 18.2 THE METAGENOMICS PIPELINE

No single approach is sufficient to fully characterize any sample. This begins with data preprocessing to filter quality, remove contaminants, remove chimeric sequences, and prepare data for analysis. Every step in the pipeline has the potential of introducing errors and biases, it is essential that parameters be selected with care.

The marker gene approach is unable to provide information about functional elements due to its limited ability to resolve taxonomy. The 16S rRNA is present in bacterial genome. The gene contains a mixture of highly conserved and hypervariable regions, the former making it easy for amplification and the latter for mapping reads to taxa (32). However, it is generally not possible to use 16S to distinguish strains or species, with short reads, so identity is normally limited to the genus level or above (33). This can cause a problem for our purposes, since members of the same genera behave very differently. For example, *Campylobacter hominis* is considered a member of the normal flora of the gut, whereas *Campylobacter jejuni* is known to be pathogenic (34). Furthermore, closely related species and strains compete for same environmental niches (35).

The limited resolution of marker gene methods does not mean that reads cannot be intelligently assigned to groups, rather that groups cannot be mapped to the same taxon. A commonly used approach is to cluster reads based on similarity to operational taxonomic units (OTUs) and then assign the best available taxonomic identity to each OTU. This typically results in OTUs mapping to the same taxon, with each OTU being roughly analogous to a strain or species at above a specified similarity. Commonly used threshold for the 16S gene is 97% similarity. It is sometimes useful to approximate higher taxonomic levels, for example, to conduct an analysis at the phylum level. This can be accomplished by adjusting the similarity threshold. Labeling each OTU with reference to its taxon is a concern, but done with caution. There is experimental evidence that even the 16S classifiers exhibit some taxon-specific biases (36). The use of OTUs may minimize the effects of these biases.

There are other choices of primers for PCR that can have an appreciable effect on amplification efficiency and resulting coverage (37). Primers are required for the process of amplification and are used by DNA polymerases to start copying the complementary strand, as well as to serve as a scaffold on which to build the new strand. Another advantage of primers is that they can be designed to amplify the specific marker genes of our choosing by matching the start of the genomic sequences that inevitably produce differences in DNA as sequences diverge, even in the highly conserved regions of marker genes. Ideally primers must be able to bind to a maximum number of different target species while capturing genomic regions that maximize their distinguishability.
