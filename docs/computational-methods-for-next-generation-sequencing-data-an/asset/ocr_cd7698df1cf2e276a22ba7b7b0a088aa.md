# DISCOVERING AND GENOTYPING TWILIGHT ZONE DELETIONS

review). We solely on the first two types of approaches and their hybrids. Coverage-based approaches can only discover deletions of usually at least 1000 bp in length. Assembly-based approaches face challenges that have not been entirely overcome. Note again that short deletions of length up to 20 bp can be discovered already during the initial mapping stage and while internal segment size-based approaches work well for deletions of length greater than approximately 150 bp, split-read aligners are able to discover deletions longer than 20 bp, reaching their limits at 30-40 bp. Beyond 40 bp, deletion recall of split-read aligners usually substantially drops.

# 7.3.1 Internal Segment Size-Based Approaches

The basic idea that underlies internal segment size-based approaches is that the alignment length I(A) deviates from I(R), the length of the internal segment of the read gave rise to A. That is, I(A) = I(R) + L(D) for a deletion D in the internal segment of R, see Figure 7.2 for an illustration. While I(A) is known, I(R) is not, however. Therefore, one estimates mean and standard deviation of the empirical distribution of I(R) from uniquely mappable fragments using robust estimators (18, 19). For modern DNA sequencing protocols, the fragment length distributions are approximately Gaussian with low standard deviations. We note already here that well-shaped (Gaussian) distribution is essential for discovering mid-sized deletions.

See Figure 7.3 for such a distribution, derived from the NGS reads of one of the individuals of the GoNL project (1), all of which were sequenced by BGI in 2010.

![](bbox=[0.173, 0.589, 0.826, 0.889])

**Figure 7.3** Internal segment size distribution for GoNL individual.