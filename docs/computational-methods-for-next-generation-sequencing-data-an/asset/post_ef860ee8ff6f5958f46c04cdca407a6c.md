
## APPLICATIONS OF HIGH-FIDELITY SEQUENCING PROTOCOL TO RNA VIRUSES

![](img/46aec008551cecb3bbf3aac2ee69b926_117_0.png)

**Figure 4.6** Assembly accuracy estimation (see Reference 5). Consensus error-corrected

Deep coverage is a requirement for accurate estimation of underlying viral diversity. One such platform capable of offering millions of sequencing reads is Illumina HiSeq. The relatively short length of the produced reads is compensated by sequencing the same fragment from both ends; therefore, producing coupled reads separated by a “gap,” known as paired-end read. To our knowledge, VGA is the first method scalable to millions of short paired-end sequencing reads able to produce full-length viral variants spanning the entire genome. We explore the influence of sequencing depth on the reconstruction accuracy for varying population structures and power-law distributions of viral genomes within the population (5). HIV-1 is known to have greater genetic variability than any other known virus (32). The diversity among viral genomes can vary from 3% to 20% depending on regions (33, 34). Heterogeneous viral samples were prepared by generating viral populations adhering to either uniform or power-law distribution. Surprisingly, our simulations suggest that sequencing depth has a direct positive effect on the overall accuracy. Figure 4.5 shows the effect of coverage and population size on assembly for reads up to 100 bp. Throughout all experiments, VGA maintained a PPV value of 100%.

In addition to point mutations, genetic recombination facilitates rapid evolution and production of diverse HIV genomes. Indeed, co-infected cells may produce recombinant viral progeny at levels lower than mutation rates in an intrapatient environment (35). Hence, simulated data sets must account for both possible phenomena when determining the quality of assembly. In Reference 5, we utilize a simulation model to integrate both point mutations and recombination in the generated viral population depending on the amount of diversity. A mixture of 10 intrahost viral variants from 1.3-kb HIV-1 forms the population. In addition to point mutations, our simulation model produces recombinant genomes by first constructing the genotype (i.e., sequence of SNVs) for the population. A random walk is performed over this genotype as specified number of times. Any crossover that occurs represents a new recombination between the “left” and “right” original genomes. Recombinations are independently produced, and no control is imposed over the number and length of the recombination. This model produces highly recombinant data on average, posing challenges and can be used to assess assembly accuracy. Simulation model incorporates mutation into the process by selecting a population and nucleotide-swap at random. Simulation results (Figure 4,7) suggest that our method can accurately assess viral population in the presence of recombinants and point mutations, maintaining PPV of 100%.

Finally, we evaluate population quantification accuracy, which is the accuracy of our method in prediction abundances of the assembled variants. Taking the results from VGA on 10 real HIV clones with 50,000 reads and 2 x 100 bp, the JSD is 2.93e-05 for the power law and 0.001 for the uniform-based populations. This already small measure only decreases as the size of the input grows.

## 4.5 PERFORMANCE OF EXISTING VIRAL ASSEMBLY ASSEMBLERS ON SIMULATED CONSENSUS ERROR-CORRECTED READS

We have evaluated the performance of ShoRAH (7) and QuasiRecomb (9) for simulated consensus error-corrected read data (5).

ShoRAH disregards pairing information of reads, but it is scalable enough to handle up to 1M reads. ShoRAH fails to produce full-length genome but reliably 98% of the consensus genome. It reasonably estimates the number of different viral genome, but even the most accurate ShoRAH-assembled viral genome from the closest true 1.3 kb-long viral genome in five nucleotides.

QuasiRecomb designed to handle paired-end read data and manages to produce full-length viral genomes. Unfortunately, it can reliably process no more than 100K reads. Also the number of assembled distinct viral genomes is 10-200 times more than the number of true viral genomes. The most accurate QuasiRecomb-assembled viral genome still differs from the closest true 1.3 kb-long viral genome in four nucleotides.

Unfortunately, we could not compare our method with QColors (23) assembly algorithm, which employs a similar conflict graph to represent viral population. CSP solver is used by QColors for coloring the graph, which may limit its scalability to high-throughput data sets containing millions of sequencing reads. Currently, QColors is not publicly available¹.

## 4.6 PERFORMANCE OF VGA ON REAL HIV DATA

To test the ability of VGA to accurately assemble a diverse natural occurring population and predict variant abundance levels in Reference 5, we used an Illumina HiSeq HIV data set, which consisted of 15M 2 × 100 bp reads.

| Number of reads | 50k | 100k | 500k | 1M | 2M |
| :--- | :--- | :--- | :--- | :--- | :--- |
| | | | | | |

![](img/46aec008551cecb3bbf3aac2ee69b926_118_0.png)

**Figure 4.7** Assembly accuracy estimation (see Reference 5). Up to 200 recombinant viral genomes were generated from the 1.3-kb HIV-1 region. Variant abundances follow power-law (a) and uniform (b) distributions. Consensus error-corrected 2 x 100 bp paired-reads were simulated from HIV population. Source: Mangul (2015). Reproded with permission of Oxford University Press.

(Note: The provided text contains significant overlapping and repetitive sections in the latter half of the OCR input. The output above represents the coherent logical flow of the primary sections provided.)

