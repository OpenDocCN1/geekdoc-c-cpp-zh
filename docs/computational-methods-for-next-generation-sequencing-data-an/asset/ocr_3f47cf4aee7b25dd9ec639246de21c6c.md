# COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

**Lemma 1. (15).** *Suppose that a read r contains an error region $[i_e, j_e]$, which has the length $l = j_e - i_e + 1$, with the base X, is not a prefix or suffix of r and was caused by a single error E. *Then***

+   (1) If $E$ is a nucleotide replacement, then $l = k$.
(2) If $E$ is an insertion creating a homopolymer of the length $p$ ($1 \leq p \leq k$), then $l = k - p + 1$ and the error region is followed by a homopolymer $h_{p-1}(X)$.
(3) If $E$ is a deletion creating a homopolymer of the length $p$ ($0 \leq p \leq k$), then $l = k - p - 1$ and the error region is followed by a homopolymer $h_p(Y)$, where $Y 
eq X$.

For error regions with length not exceeding $k$, Lemma 1 allows to quickly and reliably detect and correct errors. However, it is not applicable to error regions greater than $k$. “Long” error regions may appear, if two or more errors are separated by less than $k$ positions in the read, and the prevalence of these regions depends on the parameter $k$. The value of $k$ should be carefully chosen, since too small value hampers the reliable separation of $k$-counts of weak and solid k-mers. In different studies, the best results are achieved with $k = 25$ (15) and $k = 15, 23$ (34). For example, the number of long error reads was very low at $k = 25$ in HCV samples studied in Reference 15 in comparison to the number of error regions of lengths not exceeding $k$ (Figure 15.5).

![](bbox=[0.145, 0.495, 0.855, 0.87])

**Figure 15.5** Distribution of lengths of error regions for one of samples studied in Reference 15. Source: Skums 2012 15. Reproduced with permission of Springer Science+Business Media.