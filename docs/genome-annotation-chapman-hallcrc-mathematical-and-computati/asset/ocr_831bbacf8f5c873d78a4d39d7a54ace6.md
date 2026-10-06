# 142 Genome Annotation

+   - The transcript has a single exon and matches a multiexon tran-script elsewhere.
- RepeatMasker identifies the transcript as completely repetitive.
- The transcript has multiple frameshifts and no introns.
- The transcript has frameshifts and all introns are at least 80% repetitive.

Ensembl does not synthesize a gene description but rather cross-links information available from existing protein annotation data sources such as UniProt, the NCBI Gene databases (www.ncbi.nih.gov/gene). Manual structural and functional correlation of Ensembl genes can be done using Apollo (Lewis et al., 2002). Unique among genome annotation tools, Ensembl incorporates several of the genome-associated data types discussed in Chapter 4 to predict genomic regulatory features as well. Empirical data from functional genomics experiments:

+   - Chromatin immunoprecipitation—Tiling arrays (ChIP-chip), sequencing, and DNase sequencing
- Epigenomic modifications—Histone, transcription factors, RNAPolIII, DNA methylation, data from the ENCODE project
- Regulatory motifs
- MicroRNA (miRNA) targets

# 8.6 SUMMARY

Functional annotation is essential to understanding emerging genomes. Functional annotation is of predicated on good structural annotation. Genome annotation pipelines exist for handling these two stages and automating the collection of bioinformatics evidence. A variety of pipeline implementations exist in order to target prokaryotic versus eukaryotic genomes, and simple versus complex eukaryotic genomes. Some of the pipelines are stand-alone, whereas others are meant to be used in conjunction with other components for editing or viewing the automated annotation results. Chapter 9 explores several examples of these annotation data display and editing environments.