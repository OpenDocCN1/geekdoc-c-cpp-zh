
not mailing the advertisement to a set of people and see what fraction of these people buy.

We developed the theory using \(N_{Never}\), \(N_{Pers}\), \(N_{Anti}\), and \(N_{Always}\) to show the behavior in the subpopulation that results in the probabilities. The relevant formula in deciding whether or not to mail to a person in a subpopulation is simply

```
ELP =

\(P(Buy = yes|Mailed = yes)r_s - P(Buy = yes|Mailed = no)r_u - c, (13.24)\)
```

where the conditional probabilities are obtained from data or from data along with prior belief. We mail to everyone in the subpopulation if \(ELP > 0\), and we mail to no one in the subpopulation if \(ELP \le 0\).

### 13.7.2.2 Identifying Subpopulations with Positive ELPs

Next, we show how to use class probability trees to identify subpopulations that have positive ELPs.

First, we take a large sample of individuals from the entire population and obtain data on the target variable Buy, the indicator variable Mailed, and n other indicator variables \(X_1, X_2, \dots, X_n\) for members of this sample. The n other indicator variables are attributes such as income, sex, salary, etc. Next, from these data we grow a class probability tree using a tree growing algorithm as discussed at the end of Section 13.7. For example, suppose n = 2, \(X_1 = Sex\), and \(X_2 = Income\). We might learn the class probability tree in Figure 13.22.

Once we learn the tree, we can calculate the ELP for every subpopulation. The next examples illustrate this.

### Example 13.31 Suppose

- c = .5
- rs = 8
- ru = 10,

and we are investigating the subpopulation consisting of individuals with medium income who are male using the tree in Figure 13.22. We follow the right branch from the root of the tree and then the left branch from the Sex node to arrive at the Mailed node corresponding to this subpopulation. We then find for this subpopulation that

```
ELP = P(Buy = yes|Mailed = yes)rs - P(Buy = yes|Mailed = no)ru - c
= .4 x 8 - .2 x 10 - .5 = .7.
```

Because the ELP is positive, we mail to this subpopulation.

### Example 13.32 Suppose the same values of c, rs, and ru as in the previous example, and we are investigating the subpopulation consisting of individuals with low income who are female. We follow the left branch from the root to arrive at the *Mailed* node corresponding to this subpopulation. We then find for this subpopulation that

```
ELP = P(Buy = yes|Mailed = yes)rs - P(Buy = yes|Mailed = no)ru - c
= .6 x 8 - .5 x 10 - .5 = -.7.
```

Because the *ELP* is negative, we do not mail to this subpopulation. Notice that for members of this subpopulation there is an increased probability of buying if we mail them the advertisement (.6 versus .5). However, owing to the cost and profits involved, the *ELP* is negative.

In general, the goal of a tree growing algorithm is to identify a tree that best represents the conditional probability of interest. That is, the scoring criterion evaluates the predictive accuracy of the tree. So a classical tree growing algorithm would attempt to maximize the accuracy of our estimate of *P(Buy|Mailed, X1, X2, ..., Xn)* for all values of the variables. However, in this application we want to maximize expected profit, which is determined by the *ELP*. Notice in Equation 13.24 that the *ELP* will be 0 if *P(Buy = yes|Mailed = yes) = P(Buy = yes|Mailed = no)*. So if in some path from the root to a leaf there is no split on *Mailed*, the value of the *ELP* at the leaf will be 0. It seems a useful heuristic would be to modify the tree growing algorithm to force a split on *Mailed* on every path from the root to a leaf. In this way for every subpopulation we will determine that either the *ELP* is positive (and therefore we should definitely mail), or the *ELP* is negative (and therefore we should definitely not mail). One way to implement this heuristic would be to modify the algorithm so that the last split is always on the *Mailed* node. Chickering and Heckerman [2000] developed a tree growing algorithm with this modification.

Chickering and Heckerman [2000] performed an experiment applying the method just described. The experiment concerned deciding which subpopulations of Windows 95 registrants to mail an advertisement soliciting for an MSN subscription. Regardless of the subscription rate, they found we can expect to benefit by doing targeted advertising as described above rather than simply mailing to everyone. The reason is that the method seems to identify persuadable individuals who would buy only if they are sent an advertisement and anti-persuadable individuals who are turned off by the advertisement.

## 13.8 Discussion and Further Reading

In Section 8.8 we showed applications of Bayesian networks. Next we present applications specifically concerned with learning Bayesian networks from data.

### 13.8.1 Biology

- 1. Friedman et al. [2000] developed a technique for learning causal relationships among genes by analyzing gene expression data. This technique is a result of the “Project for Using Bayesian Networks to Analyze Gene Expression,” which is described at www.cs.huji.ac.il/labs/compbio/expression.

- 2. Friedman et al. [2002] formulated a method for phylogenetic tree reconstruction. The method is used in SEMPHY, which is a tool for maximum likelihood phylogenetic reconstruction. More on it can be found at http://www.cs.huji.ac.il/labs/compbio/semphy/.

- 3. Friedman and Koller [2003] created an approximate model averaging technique using MCMC for analyzing gene expression data.

- 4. Segel et al. [2005] constructed a module network approach to analyzing gene expression data.

- 5. Fishelson and Geiger (2002, 2004) developed a Bayesian network model for genetic linkage analysis and an inference algorithm for that model.

- 6. Jiang [Jiang et al., 2010], [Jiang et al., 2011a], [Jiang et al., 2011b] modeled the relationships among a phenotype and genes using a Bayesian network, and applied Bayesian network scoring criteria to learning the genetic basis of diseases from GWAS data sets.

- 7. The text Probabilistic Methods for Bioinformatics [Neapolitan, 2009] discusses many of the applications to biology just mentioned.

### 13.8.2 Business and Finance

- 1. Breeze et al. [1998] learned Bayesian network models for collaborative filtering from several data sets. Collaborative filtering concerns learning an individual’s interests based on the interests of similar individuals.

- 2. Sun and Shenoy [2006] learned a bankruptcy prediction Bayesian network from data.

### 13.8.3 Causal Learning

Applications to causal learning can be found in [Spirtes et al., 1993; 2000], [Glymour and Cooper, 1999], and [Neapolitan, 2004].

### 13.8.4 Data Mining

Margaritis et al., [2001] developed NetCube, a system for computing counts of records with desired characteristics from a database, which is a common task in the areas of decision support systems and data mining. The method can quickly compute counts from a database with billions of records.

### 13.8.5 Medicine

Herskovits and Dagher [1997] learned from data a system for assessing cervical spinal-cord trauma.

### 13.8.6 Weather Forecasting

Kennett et al. [2001] learned from data a system which predicts sea breezes.

## EXERCISES

### Section 13.2

Exercise 13.1 Suppose we have the two models in Figure 13.1 and the following data:

| Case | J | F |
|---|---|---|
| 1 | j₁ | f₁ |
| 2 | j₁ | f₁ |
| 3 | j₁ | f₁ |
| 4 | j₁ | f₁ |
| 5 | j₁ | f₁ |
| 6 | j₁ | f₂ |
| 7 | j₂ | f₂ |
| 8 | j₂ | f₂ |
| 9 | j₂ | f₂ |
| 10 | j₂ | f₁ |

- 1. Score each DAG model using the Bayesian score and compute their posterior probabilities, assuming that the prior probability of each model is .5.

- 2. Create a data set containing 20 records by duplicating the data in the table one time, and score the models using this 20-record data set. How have the scores changed?

- 3. Create a data set containing 200 records by duplicating the data in the table 19 times, and score the models using this 200-record data set. How have the scores changed?

Exercise 13.2 Suppose we have a Markov chain with the following transition matrix:

| 1/5 | 2/5 | 2/5 |
|---|---|---|
| 1/7 | 4/7 | 2/7 |
| 3/8 | 1/8 | 1/2 |

Determine the stationary distribution for the chain.
