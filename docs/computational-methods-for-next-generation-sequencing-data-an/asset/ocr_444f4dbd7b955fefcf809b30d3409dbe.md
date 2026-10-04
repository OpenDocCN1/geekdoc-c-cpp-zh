# PROBABILISTIC VIRAL QUASISPECIES ASSEMBLY

binding regions, primers favor to bind to DNA fragments that match better. This bias, amplified by PCR, influences frequency estimation and may lead to large deviations from the true haplotype frequencies. PCR with random primers does not have the bias towards specific strains, but mainly leads to amplification of nonspecific cDNA. These data sets can only be used to generate a consensus sequence of the quasispecies because the sample does not contain enough material to reconstruct individual haplotypes.

The RT-PCR step is critical, as it can introduce artificial recombinant cDN. This effect needs to be minimized by using lab protocols. Standard RT-PCR conditions generate 30.6–37.1% recombinants cDN, which can be decreased with optimized RT-PCR conditions to 0.9–2.6%. Artificial recombinants cannot be distinguished from true molecular sequences and lead to an underestimate of the haplotype frequencies and overestimate of the quasispecies diversity.

# 16.2.2 Sequencing Approaches

Since the introduction of the first NGS system in 2004, pyrosequencing was introduced by 454/Roche, the landscape of sequencing technologies and their performances has changed drastically (Table 16.1). It was the standard platform for sequencing in the last 10 years. In this method, complementary strands of single-stranded templates are produced in an iterative manner. Each round, nucleotides of only one of the four nucleotides, adenine, guanine, cytosine, and thymine are incorporated. If a tagged nucleotide is incorporated, emitted light is detected by the system. Nowadays the FLX system of 454/Roche produces up to 1 kb, but the sample preparation is very laborious. Systematic errors in homopolymeric regions are highly abundant with an error rate of 10%, 30%, and 50% for homopolorphs of size 6, 8, and 10bp, respectively. Another sequencing platform is Ion Torrent semiconductor sequencing, which detects hydrogen ions that are released as the complementary strand of the template is polymerized. Its strengths are speed and cost, but the length is only up to 400 bp with a maximal throughput of 5.5 million reads that exhibits similar homopolymer errors as 454/Roche. Sequencing by SOLiD produces 1.2–1.4 billion short reads of 50 bp that do not exhibit homopolymeric, but problems with palindromic sequences. A single run takes 1–2 weeks. In the last years, the majority of sequences have been produced with Illumina sequencing machines, because library preparation is much

# TABLE 16.1 Comparison of Next- and Third-Generation Sequencing Technologies (33, 34)

| Technology | Read Length (bp) | Throughput (Reads) | Run-Time | Most Abundant Errors |
| --- | --- | --- | --- | --- |
| 454/Roche | 1000 | 1 million | 1 day | Homopolymeric errors |
| Ion Torrent | 400 | 80 million | 2 hours | Homopolymeric errors |
| SOLiD | 50 | 1.2–1.4 billion | 1–2 weeks | Palindromic sequences |
| Illumina MiSeq | 2×300 | 44–50 million | 3 days | Substitutions |
| PacBio | 20,000 | 55,000 | 3 hours | Higher indel rate |