
# 16

# PROBABILISTIC VIRAL QUASISPECIES ASSEMBLY

ARMIN TOPÖFER AND NIKO BEERWINKEL

Department of Biosystems Science and Engineering, ETH Zurich, Basel, Switzerland

## 16.1 INTRA-HOST VIRUS POPULATIONS

Viruses are pathogens that cause infectious diseases (1). A single virus particle, called virion, exhibits its genetic material as a single- or double-stranded linear or circular DNA or RNA molecule in one or multiple copies. A virion alone cannot reproduce itself. For reproduction, a virus depends on infecting cells of an organism. RNA viruses are of particular interest, as their viral replication enzymes have a low fidelity and produce error-prone copies of the genome, including single point mutations and recombination. This high error rate limits the genome size in the range of 10³–10⁸ base pairs (bp), which is much smaller than bacterial or eukaryotic genomes. Beyond a certain error rate threshold, mutational meltdown would lead to a virus population that is not able to preserve the genotype with the highest fitness, where fitness rate and genome size are anticorrelated (2). A genome is protected by a protein coat and many viruses are protected by an additional envelope. Receptors on the outside surface are used to attach and fuse with host cells. The viral life cycle, from infection of a cell to the release of new virions, is very short and is completed in a few days. This leads to a vast amount of virions in each infected host. The swarm of viruses evolves through mutation and natural selection. It is subject to the host’s immune pressure and possibly antiviral therapy. Viruses may escape this selective pressure and gain advantage by acquiring one or more of the following genomic alterations: (i) single-nucleotide variants (SNVs), (ii) loss or gain of one or more amino acids, (iii) large deletions, for example, due to alternative splicing, or (iv) recombination of different strains.

### 16.1.1 Viral Quasispecies

A single infected host contains millions of virions. This vast amount of virions can be summarized as a set of unique genetically different variants, called haplotypes, together with their respective frequency. Each haplotype is identified by its genome, its pattern of SNVs and structural variations. This distribution of haplotypes is referred to as a quasispecies (Figure 16.1).

Manfred Eigen defined the quasispecies equation as a mathematical model for RNA virus populations that evolve under a mutation-selection process (3). In this model, mutation can lead to transformation of one viral hapotype into another by the time of replication. Mutations determine strain replication rates that give rise to selection. The mutation process is considered to consist of point mutations. However, many clinically relevant viruses, including human immunodeficiency virus type 1 (HIV-1) and hepatitis C virus (HCV), undergo recombination with high frequency. Therefore, the quasispecies model has been extended to account for both mutation and recombination (4). It is assumed that at equilibrium, swarms of low-frequency hapotypes, subject to mutation and recombination, are maintained by few master sequences that have the highest fitness (5, 6). A master sequence can be thought of as the center of one mutant cloud or the mode of the hapotype distribution in high-dimensional sequence space.

![](img/46aec008551cecb3bbf3aac2ee69b926_366_0.png)

**Figure 16.1** A schematic representation of a quasispecies. Haplotypes are represented as dots and the corresponding frequency as size. The quasispecies emerges from a small set of master sequences, inner circle, by recombination, middle ring, and mutation, outer ring. Edges between dots represent the closest distance between haplotypes. Please see www.wiley.com/go/Mandoiu/NextGenerationSequencing for a color version of this figure.

![](img/46aec008551cecb3bbf3aac2ee69b926_367_0.png)

**Figure 16.2** For different scenarios, schematic fitness landscapes are visualized. For each scenario, the reproductive capacity, is shown as a function of the discrete sequence space. Under the assumption that only one hapotype has a high fitness (a), mutant variants reproduce with a negligible capacity or not at all. In the flattest scenario, for example, one with (b) or two master sequences (c), mutant variants have only a slightly reduced fitness.

### 16.1.2 Fitness

If a virus has a high error rate, it follows an evolutionarily stable strategy (7) to generate a population of hapotypes with approximately equal fitness instead of one hapotype being the fittest (Figure 16.2). Occupation of such a broad fitness landscape is survival of the flattest (8). It is a survival strategy. The evolutionary trajectory of the viral infection depends not on the characteristics of the fittest but also on the whole population.

Natural selection also improve the changes of survival in changing environments. For example, a low-frequency hapotype that carries an appropriate resistance mutation could gain an advantage under treatment. Then, the mass of the quasispecies shifts to the new master sequence and a new hapotype distribution is created. This survival strategy improves changes of adaption to environmental changes, such as treatment switches.

### 16.1.3 HIV-1 as a Model

As in many fields of research, fundamental research is performed on model systems, such as Arabidopsis thaliana for plants or Escherichia coli for bacteria.

In viral quaspecies studies, HIV-1 is a representative model. HIV-1 is the cause of a deadly pandemic, the acquired immunodeficiency syndrome (AIDS), and is as such a major focus of. There are 34 million people infected with HIV-1 worldwide. HIV-1 is composed of a small single-strand RNA (ssRNA) genome with ~9.7 kilobases (kb) that evolves by mutation and recombination, leading to high diversity (9). The genome is divided into three parts, the gag, pol, and env regions (Figure 16.3). The gag region contains genes for the protease, reverse transcriptase, RNase, and integrase. The env region contains genes for the receptor proteins. In the envelope, the protein env protrudes the surface. Env consists of a glycoprotein (gp)120 cap and a gp41 gene. These protein surfaces enable the virus to attach and fuse with host cells to initiate the infectious cycle.

HIV-1 maintains high diversity due to two properties of HIV-1, a high reproductive capacity and a low-fidelity reverse transcriptase producing 2.5 x 10⁻⁵ substitutions per base and RT (10). There are at least 10⁷–10⁸ infected cells per host (12). The effective population size is hard to estimate and has been reviewed (13). HIV-1 is able to generate every possible mutation along the genome. Most of these mutations are not maintained because many result in loss-of-function or nonproductive viruses. Research in the last 30 years has identified the genetic sequences and where mutations are located. Very effective antiretroviral drugs have been developed but diversity is high. Every patient may show different patterns of resistance mutations; therefore, treatment has to be personalized. In this case, genotyping, the identification of resistance mutations, is necessary to tailor the best possible regimen, that is, drug combination, for an individual patient (14, 15).

### 16.1.4 Recombination

The high mutation rate of HIV-1 is one of two factors that advances diversity. During RT of the RNA, the reverse transcriptase is known to switch strands (Figure 16.4). In infected patients, this can lead to new recombinant DNA molecules, randomized products of existing haplotypes. The rate of recombination events of HIV-1 is assumed to be 10-fold higher, approximately 3 x 10⁻⁴ per base and RT, counts play an important role in shaping the sequences (16, 17).

![](img/46aec008551cecb3bbf3aac2ee69b926_368_0.png)

> Figure 16.3 Protein coding region of HIV-1 with reference positions of strain HXB2. The three functional regions gag, pol, and env are shown in their respective reading frames.
