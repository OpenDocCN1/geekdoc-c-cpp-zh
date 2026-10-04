# COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

It is common to refer to all post-Sanger sequencing technologies as "next generation." It is becoming more accurate to consider the more mature of these technologies such as Illumina, SOLiD, 454, and other platforms generating short reads as second-generation sequencing. This is in part to contrast them from newer technologies as PacBio, which do single-molecule real-time (SMRT) sequencing and generate smaller amounts of ultralong sequences with different error characteristics and often complementary applications (5). Second-generation sequencing technologies, such as Illumina, which will be the sole focus of this study, produce large quantities of short sequence reads. Let (6) provides a overview of the various technologies available and their capabilities. Many of these platforms, including Illumina, can produce either single or paired ends (also known as mate pairs;Figure 12.1a) of varying lengths. The experimental design of a sequencing project should dictate which of these is most appropriate. The value of paired-end reads for RNA-seq that they contain both positional and strand information can be used to more accurately assemble transcripts and to identify novel elements. The second-generation sequencing technologies are continuing to develop and increase in capacity. The development of algorithms to analyze these data sets is thus also continuous with no truly defined standardized methodology emerging. Thus, it is of interest to compare and contrast various methods that have been used. In the case of RNA-seq, two types of analyses are common: transcriptomics based on defined reference sequence (assemble to reference) and transcriptomes

```
F(@SEQ_ID_1/1)
```

![](bbox=[0.173, 0.532, 0.826, 0.603])

```
@SEQ_ID_1/1
GATTTGGGGCAAAGCAGATCGATCAAATAGTAAAATCATTTGTCACTACGTT
+\!*'(((***))####$)) (%%%%).1***-*****)55CCF>>>>CCCCCC65
```

```
@SEQ_ID_1/2
GATTTGGGGCAAAGCAGATCGATCAAATAGTAAAATCATTTGTCACTACGTT
!*/(((***))####$)) (%%%%).1***-*****)55CCF>>>>CCCCCC65
```

**Figure 12.1** Paired-end reads. (a) A paired-end set of reads: the arrows represent the length, and the position of the arrow strand (top or bottom). The outer bracket represents the length of the fragment being sequenced while the inner bracket represents the mate pair distance. (b) Forward read (F, top strand); the header of a read is terminated with the read number followed by 1 or 2 denoting forward and reverse reads, respectively. (C) Reverse read (R, bottom strand); for example, the quality score at position 3 of the reverse read is encoded by ":"; this represents a phred score of 25 (ASCII_value(":\)-33 = 58 - 33 = 25.

270