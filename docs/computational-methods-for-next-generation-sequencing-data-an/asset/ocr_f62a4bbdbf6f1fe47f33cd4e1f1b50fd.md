# COMPUTATIONAL APPROACHES FOR FINDING LONG INSERTIONS AND DELETIONS 183

![](bbox=[0.195, 0.095, 0.804, 0.17])

**Figure 8.7** Signature of paired-end reads for long insertion. The bottom shows where the sequences of two signature reads comes from. The top shows the signatures that they have when mapped onto the reference genome.

Next, we describe several tools that only use single signatures and then show some examples of tools with combined signatures.

# **8.2.2 Methods for Discovering Long Indels without Breakpoints

Starting from this section, we will give several examples of SV calling tools that implemented certain signatures discussed in the previous section. In this section, we will cover an RD method CNVator (8), which calls copy number variations (CNV). A long deletion is a loss of copy and a long insertion is a gain of copy. We will cover BreakDancer (9), an RP method. There are more RD methods, for example, References 10–12 and more RP methods, for example, References 13–15.

**8.2.2. CNVator** CNVator is one of the tools that use RD to discover CNVs from family and population genome sequencing. The main idea of this approach is based on the observation: RD for CNVs is different from that of normal regions, which is also the main observation of all RD-based approaches. One of the techniques CNVator uses is called mean-shift approach. This approach is borrowed from image processing technique, and it presents an elegant way to locate the density maxima without having to estimate the density directly, which is an iterative procedure that shifts each data point to the density maxima along the mean-shift vector. CNVator combines the mean-shift approach with additional refinements to extend the range of discovered CNVs, which are obtained from the initial RD. Detailed implementation of CNVator includes three steps:

First, CNVator calculates the RD for each bin and correct GC-bias. It maps to genome (which is divided into consecutive non-overlapping bins), and if a read (or read pair with concordant mapping distance) can map to more than one position with equal mapping score, it randomly picks one (or a pair) to get unique RD. Then GC-bias is corrected to eliminate the correlation of RD with GC content.

The second step is mean-shift based segment partition and merging, which is the key step of approach. As mentioned earlier, the mean-shift technique is borrowed from image processing to detect edges in computer vision. And using mean-shift approach to participate genome, each bin is viewed as a point, and mean-shift vector of each point is calculated with the direction pointing to bins with the most similar RD signal. Segment breakpoints are determined where two neighboring vectors direct oppositely but do not point to each other. Then, neighboring