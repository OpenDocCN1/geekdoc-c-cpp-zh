# Genome Annotation

2004) produces ab initio gene predictions, but other predictors mentioned in Chapter 2 can be used as well. Each potential exon is scored according to several criteria, some of which can be configured:

+   - Length of the 5’ and 3’ untranslated regions (UTRs)
- Confirmation of splice sites by expressed sequence tag (EST) alignment
- Overlap of EST and protein alignments with the ab initio prediction
- Total number of exons and total protein length

High-scoring exons are merged into a gene annotation with quality values. To improve prediction accuracy, MAKER can also be bootstrapped. The outputs of preliminary runs can be used to automatically retrain the gene prediction algorithm. As an iterative process requires some diligence and manual postanalysis to determine when to stop iterating the models and which configuration parameters to modify to correct systematic biases.

# 8.3.3 Functional Annotation

The MAKER-generated model transcripts are first translated into protein FastA. At a basic level, MAKER maps putative functions identified from BLASTP against UniProt/SwissProt (Magrane et al., 2011). Beyond this “best hit” approach, mechanisms to functional annotation using GMOD components are not standardized. GMOD components are used by many model organism communities, each of which has their preferred mechanisms for generating functional annotation. The variety of methods they use reflect the different data source challenges faced by plant, fungal, mammal, and other communities, as well as the amount of human and computational resources they have available to devote to the annotation process. The commonality of these systems is that they store their results in the GMOD database system, called Chado (Zhou et al., 2006). From a Chado database, several GMOD tools can then further process the data, for example, for visualization.

# 8.3.4 User Interface

When run on the command line, MAKER’s inputs are essentially a FastA-formatted sequence file and transcript data if available. A Web-based version of MAKER is available that requests several of the