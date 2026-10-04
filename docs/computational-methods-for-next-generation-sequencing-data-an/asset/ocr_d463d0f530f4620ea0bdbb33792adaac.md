# 372 COMPUTATIONAL METHODS FOR NGS DATA ANALYSIS

![](bbox=[0.173, 0.096, 0.826, 0.331])

**Figure 16.10** Graphical representation of the HMM of *QuasiRecomb*. Only observation i is depicted; for the full model, the graph is replicated for $i=1,...,N$ indicated by the plate notation. Variable $Z$ represents the state sequence, $H$ the nucleotide of the emitted haplotype, and $R_j$ the nucleotide of the observed read at position $j$.

*Parameter Inference* For parameter inference, a prior distribution for the parameters is defined and the maximum posteriori (MAP) estimate of the parameters is computed by maximizing the posterior probability

> $P(\theta \mid R) \propto P(R \mid \theta)P(\theta)$.

Employ Dirichlet priors leads to sparse MAP solutions if the Dirichlet hyperparameters approach zero. The regularized model is also a biological plausible assumption. Most of the genomic regions in RNA virus populations are conserved or nearly conserved. The virus is caused by selective pressure on regions to ensure reproductive capability. The virus is defined by these regions. In these regions, the different generating sequences cannot be distinguished when there is no or little diversity.

Despite regularization of the transition probabilities, identical regions between generators are a problem (Figure 16.7). As reads of the conserved region cannot be assigned uniquely to one of generators and there is no information about the linkage of the flanking regions, a recombinant structure is estimated. This can be avoided by requiring the recombination probability to be less than 0.5.

*Model Selection* The described model uses an unknown set of sequence profile generators to explain the underlying quasispecies. To determine the unknown number of generators $K$, for model selection the Bayesian information criterion (BIC) is used. Empirical studies have shown that in practice, model selection works up to at least $K=5$ (80). This is sufficient for practical purposes, as the number of master sequences in the quasispecies model is assumed to be small.