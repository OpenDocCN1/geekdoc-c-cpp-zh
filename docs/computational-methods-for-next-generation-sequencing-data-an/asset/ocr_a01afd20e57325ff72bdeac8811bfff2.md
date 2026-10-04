# COMPUTATIONAL METHODS FOR TRANSCRIPT ASSEMBLY FROM RNA-SEQ READS 261

penalty term to favor isoforms comprising a higher number of exons. To determine the regularization parameter $\lambda$, which balances the relative importance of the $accuracy$ of its prediction, SLIDE and IsoLasso fit the model for several values of $\lambda$ and chose the best one according to some (stability) criterion.

On the other hand, NSMAP (36) applies nonconvex LP regularization and iReckon (32) utilizes the more complex regularization term

```
$-\lambda \cdot e^{\sum \sqrt{a_i}}$ (11.1)
```

which penalizes lowly expressed more than highly expressed ones. Parameter $\lambda$ is determined by gradually increasing $\lambda$ until the fraction of reads that cannot be assigned to an expressed isoform exceeds a given threshold.

Notice that several methods, iReckon and SLIDE, cope with the abundance shrinkage caused by the regularization penalty by re-running the optimization step without the penalty term using only the predicted transcripts.

# 11.3.3 Accuracy

In this section, we discuss the $accuracy$ aspect of the prediction, that is how well the predicted isoforms and their assignments explain the observed reads. Most approaches fall into one of two categories described in the following sections.

# 11.3.3.1 Linear Regression Many methods use to estimate the number of reads originating from segments of the genome, relying on the assumption that reads are uniformly sampled from the expressed transcripts.

In its general form, the estimated number of reads (or read pairs) originating from a certain segment (or pair of segments) is proportional to the sum of the expression levels of transcripts containing that segment, weighted by the number of genomic positions at which a corresponding fragment can stay. Random noise $\varepsilon$ is added to fully explain the assignments $b_j$

```
$b_j = \sum_{p \in P(G)} f_{pj}\theta_p + \varepsilon_j$ (11.2)
```

$b_j$ capture the number of reads in segment $j$, $P(G)$ is the set of maximal paths in splicing graph, $G$, $	heta_p$ is the abundance (to be determined) of the isoform represented by path $p$, and $f_{pj}$ is a weight coefficient that distributes reads among segments along path $p$, with $f_{pj}=0$ if $p$ does not contain segment $j$. Note nonuniform sampling of reads along a transcript can be captured by coefficients $f$ at the level of segments. In what follows, we abstract precise definitions and units of observations, and variables in (11.2) that have many methods.

In general, methods based on a connectivity or splicing graph summarize individual reads into a read count for each segment. Segments typically correspond to the nodes and ends of the splicing graph. While the $b_j$'s in (11.2) are obtained in IsoLasso, MITIE, and TRAPH from the number of reads falling into segment $j$,