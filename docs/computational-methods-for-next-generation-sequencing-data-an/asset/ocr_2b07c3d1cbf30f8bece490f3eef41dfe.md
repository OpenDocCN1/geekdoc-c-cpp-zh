# COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

user-defined threshold needs to be removed from either end. A common standard
to trim base quality when the median base quality falls below 20. In addition, adapters
used in the process of library construction may need to be removed. If samples
will be multiplexed, individual samples will have to be tagged by sequence bar-
codes. Following the separation of sample reads by their barcodes, they will need
to be trimmed from the reads.

Many tools are available for quality reads, including FastQC (7), FastX
(8), and NGS QC Toolkit (9). The distribution of FastQC is independent
due to its implementation in Java and can be used both at the command line
and a GUI on Windows or MacOS platforms. We have preferred it for
ease of use and the concise, biologist friendly, graphical representation of a wide
range of quality-related features including base sequence quality, per base sequence
content, and k-mer content. FastQC also allows for input of fastq sequence
of various quality scores, fastq sequence in SAM/BAM format, and for the
analysis of reads from other sequencing platforms such as 45 and PacBio.
of the purpose of illustration, consider the graphs produced by FastQC as
in Figure 12.3.

The kmer content variation seen in the reads from position 1 through 16 is often
seen in samples, but in conjunction with the results from the Adaptor content graph
could show an experimental artifact and would most likely represent adapters and
the leading edge from 1 must be clipped before assembly. We have
developed a python script to trim or clip reads. The script takes the fastq input,
has optional parameters, and writes the processed output to a new file. Analysis
of the raw sequence is not only the good metric for quality. Assuming one is
with a reference genome, a test alignment to that genome also helps quality.
of one aligns each RNA-seq data set to bowtie (Bowtie1) with Tophat2 (10), the
reference and the other file is called unmapped.bam. Several means can be used to
compare the contents of these files. Within samtools (11), one can use "view"
count the reads in each of these files. It is desirable to have a high proportion
of your sequence aligning to the reference genome, if this is in the range of
at least 75-80%, then this suggests that your sequence is of reasonable quality.
if, a high proportion of your data is not mappable to the reference genome,
then one may desire to resequence a particular sample or eliminate that data set from
downstream analyses as could be confounding. Simply comparing the file sizes
of the above BAM files is also a good proxy for this measurement. One difficulty in
de novo analyses is that the above type of assessment is not available for truly novel
sequence.

# 12.2 EXPERIMENTAL CONSIDERATIONS

Other than sequence quality, one of the most important issues with RNA-seq, as it
has been with microarray analysis, is the experimental design. Two primary
issues are the question of replication (both biological and technical) and sequencing
depth. Biological replication (e.g., mRNA from livers of three different mice the