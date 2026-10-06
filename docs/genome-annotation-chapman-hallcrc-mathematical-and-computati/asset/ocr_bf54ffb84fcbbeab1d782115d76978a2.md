# Genome Annotation

single nucleotide.) The configuration of these search patterns is achieved by providing a training set of known transcription start sites to the pre-diction tool. Likewise, the real codon is not necessarily the first ATG encountered, so a training set of known full-length coding sequences can greatly assist in building a model of what the DNA sequence around the real start codons looks like. The sequence between the transcription start and the translation start may also have some statistical characteristics, as may be the sequence between the GT and AG in an intron. The probabilities derived from the training data sets are what determine the accuracy of the subsequent predictions.

Gene features are often referred to by their acronyms in gene prediction systems. It is worthwhile remembering these as they are introduced here. Statistical models may include the features described next, roughly in genomic order.

# 2.3.1 5’ Untranslated Region

The 5’ untranslated region (5’ UTR) is the region between the transcription start site and the translation start codon. Many eukaryotic gene predictors can take advantage of user-identified 5’ UTR sequences to train their statistical models. When sufficient aligned mRNAs or mapped short reads are available, and the start codon is known via protein homology, the identification of 5’ UTR can be based on empirical evidence for training purposes. The 5’ UTR region contains several translation signals, as detailed next. The identification of transcription-factor binding sites is a complex issue. In the general transcription-factor binding sites locations are not often used to assist in the prediction of gene structures. Their discovery and potential usage is discussed later in Chapter 3.

# 2.3.2 –35 Signal

The –35 signal is located approximately 35 base pairs upstream of the start codon in prokaryotes. It can be used to aid identification of the proper binding site for the initiation complex during transcription. This signal has a consensus sequence of TTGACA (Rosenberg and Court, 1979), but is relatively weak compared to the other prokaryotic UTR signals, therefore multiple candidates often exist for a single gene.

# 2.3.3 B Recognition Element

The B recognition element (BRE) is found in many archaeal and eukaryotic genes (Qureshi and Jackson, 1998), just upstream of the TATA box,