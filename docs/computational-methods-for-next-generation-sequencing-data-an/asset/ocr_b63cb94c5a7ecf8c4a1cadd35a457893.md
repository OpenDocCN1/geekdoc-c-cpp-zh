# POOLING STRATEGY FOR MASSIVE VIRAL SEQUENCING

alleles $\{a, c, t, g, d\}$. Each entry $f_m(e), e\in\{a, c, t, g, d\}$ is the frequency of allele $e$ in $m$th position among all variants $C$, $\sum_{e\in\{a,c,t,g,d\}}f_m(e)=1$. In particular, every read can be considered as a genotype with a single 1 and d zeroes in each column. Given a set of reads $R$, a $k$-genotype is $G^*=\{g_1, \dots, g_k\}$ of $k$ distinct genotypes that most likely read $R$:

```
$G^* = \arg\max Pr(R|G), \quad |G|=k$$
```

where $Pr(R|G)$ is the probability to observe $R$ given a set of genotypes $G$, which is calculated as a product of probabilities to observe each read from $R$. The probability to observe read $r$ equals to $Pr(r)=\prod_{i=1}^l f_i Pr(r|g=g_i)$, where

```
$Pr(r|g=g_i)=\prod_{m=1}^l f_{im}(r_m), \quad (3.10)$
```

and $f_{im}(r_m)$ is the frequency of $m$th character of $r$, in the $m$th position of genotype $g_i$. Then the log-likelihood of the set of allele frequencies $\mathcal{F}=\{f_{im}(e)|i=1,\dots,k; m=1,\dots,l; e\in\{a,c,t,g,d\}$ equals to

where $o_r$ is the observed data $p_{i,r}$, that is, the number of times the read $r$ originated from the genotype $g_i$, and solve the easier optimization problem of maximizing the log-likelihood of the hidden model

```
$$\ell_{hid}(F)=\sum_{r\in R}\sum_{i=1}^k p_{i,r} \log (f_i Pr(r|g=g_i)).$$
```

Our clustering method is described in Algorithm kGEM. The initial set of genotypes $G^{(0)}$ is selected as follows: from the most frequent read, we iteratively select the read maximizing the minimum Hamming distance to the previously selected reads and add to $G^{(0)}$ the corresponding genotype.

# 3.4 PERFORMANCE OF POOLING METHODS ON SIMULATED DATA

# 3.4.1 Performance of the Viral Sample Pool Design Algorithm

The pool generation algorithm was evaluated using three sets of simulated data.

+   1. Complete graphs.
Pools were generated for complete graphs with $n=4,\dots,102$ vertices without the threshold of pools' size. For every test instance, exactly $m=\lceil\log(n)\rceil+1$ pools were constructed, coinciding with the theoretically justified estimation (23, 32). Hence VSPD algorithm produces optimal solutions for complete graphs.