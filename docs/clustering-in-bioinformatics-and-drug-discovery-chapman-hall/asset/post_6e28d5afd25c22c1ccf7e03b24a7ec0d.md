
For positive integers, p, q, and n. This is a sequence of rational numbers called the Farey sequence of order n. For large n, the expected value of Fₙ is

$\frac{3n^2}{\pi^2}+O(n\log n)$.  (12.20)

This remarkable result relates π to reduced proper fractions. In fact, it can be easily shown from this result that the probability of any two integers being coprime is

$\frac{6}{\pi^2}\approx 0.608\approx\frac{3}{5}$.  (12.21)

Thus, roughly three fifths of the set of proper fractions $p/q$, where $p<q$, $q\le n$, for large n are fully reduced fractions and the remainder reduce to one of these fully reduced fractions. (the probability that any three integers are relatively prime is given by Apéry’s constant (approximately 0.832)). Given rational similarity measures, it is important to keep this fact in mind, as it may have a bearing on the form of the distribution of the similarity values, where low order fractions (e.g. 1/9, 1/2, 1/3, 1/4, etc.) are more prominent in the distribution than would be our natural expectation.

These distributions have fractal properties (ruler pattern plot) as do other prime number distributions (Ulam’s square). Other curious relationships to $\frac{6}{\pi^2}$ are:

$\frac{6}{\pi^2}=\sum_{n=1}^{\infty}\mu(n)n^{-2}$  (12.22)

$=P((m,n)\text{ are coprime}\mid m,n\in\mathbb{N})$  (12.23)

$=P(n\text{ is square free}\mid n\in\mathbb{N})$  (12.24)

$=\left(\prod_{p=2}^{\infty}(1-p^{-2})\right)^{-1}$  (12.25)

$=\sum_{n=1}^{\infty}\mu(n)n^{-2}$  (12.26)

Equation 12.22 is Riemann’s zeta function, ζ(2). A square free number has no power greater than 1 in its prime factorization (e.g. 2 × 3 × 5 = 30 is square free; 2 × 3² = 18 is not). The expression in 12.25, the ∏ refers to prime numbers. In Equation 12.26, μ(n) is the Möbius function: μ(n) = 0, if n has a square factor, else 1 if n has an even number of prime factors, and −1 otherwise.

As simple to state as the Farey sequence is, it can be used to state the Riemann hypothesis. Let the total number of fractions in the Farey sequence of order n equal K (namely, it can be determined exactly, but it is approximately on average related to the expression 12.23). For each Farey number in sequence (they are rank ordered), fix the Farey number, take the absolute difference between it and \(\frac{1}{k}\). Then let the \(i\)th absolute difference be \(\delta_i\). We can then state the Riemann hypothesis as:

$$\sum_{n=1}^{\infty} \delta_i = o(n^{1/2+\epsilon}), \tag{12.27}$$

where ε is some vanishingly small number. Proof of that expression and corollaries will follow.

## Bibliography

- [1] M.R. Anderberg. *Cluster Analysis for Applications*. Academic Press, first edition. 1973.
- [2] J.C. Aude, Y. Díaz-Lazcoz, J.J. Codani, and J.L. Risler. Applications of the pyramidal clustering method to biological objects. *Comput. Chem.*, 23(3-4):303-315, June 1999.
- [3] Open Babel. Open Babel: The Open Source Chemistry Toolbox http://openbabel.org/wiki/Main_Page, January 2010.
- [4] RCSB Protein Data Bank. RCSB Protein Data Bank http://www.rcsb.org/pdb/home/home.do, January 2010.
- [5] J.M. Barnard and G.M. Downs. Chemical fragment generation and clustering software. *J. Chem. Inf. Model*, 37(1):141–142, 1997.
- [6] S. Bates. Progress towards personalized medicine. *Drug Discovery Today*, November 2009.
- [7] P. Bertrand. *Structural Properties of Pyramidal Clustering*, volume 19. American Mathematical Society, 2008.
- [8] P. Bertrand. Systems of sets such that each set properly intersects at most one other set-Application to cluster analysis. *Discrete Applied Mathematics*, 156:1220–1236, 2008.
- [9] J.C. Bezdek. *Pattern Recognition with Fuzzy Objective Function Algorithms*. Plenum Press, 1981.
- [10] BKChem. BKChem http://bkchem.zirael.org, January 2010.
- [11] BLAST. BLAST: Basic Local Alignment Search Tool http://blast.ncbi.nlm.nih.gov/Blast.cgi, January 2010.
- [12] C. Böhm, B. Braunmüller, F. Krebs, and H. Kriegel. Epsilon grid order: an algorithm for the similarity join on massive high-dimensional data. *SIGMOD Rec*, 30(2):379–388, 2001.
- [13] B. Bollobas. *Random Graphs*. Cambridge University Press, second edition, 2001.
- [14] C. Bologa, T.K. Allu, M. Olah, M.A. Kappler, and T.I. Oprea. Descriptor collision and confusion: Toward the design of descriptors to mask chemical structures. *J. Comp. Aid. Mol. Design*, 19:625–635, 2005.
- [15] A. Bondy and U.S.R. Murty. *Graph Theory*. Springer, first edition, 2008.
- [16] I. Borg and P. Groenen. *Modern Multidimensional Scaling*. Springer, second edition, 2009.
- [17] J. Bradshaw and R. Sayle. Some thoughts on significant similarity and sufficient diversity http://www.daylight.com/meetings/emug97/Bradshaw/Significant_Similarity/Significant_Similarity.html, March 1997.
- [18] M.L. Brewer. Development of a spectral clustering model for the analysis of molecular data sets. *J. Chem. Inf. Model.*, 47(5):1727–33, 2007.
- [19] R. Bro, E. Acar, and T. Kolda. Resolving the sign ambiguity in the singular value decomposition. *J. Chemometrics*, 2008.
- [20] R.D. Brown and Y.C. Martin. Use of structure-activity data to compare structure-based clustering methods and descriptors for use in compound selection. *J. Chem. Inf. Comput. Sci.*, 36(3):572–584, 1996.
- [21] R.L. Burden and J.D. Faires. *Numerical Analysis*. Brooks Cole, eighth edition, 2004.
- [22] D. Butina. Unsupervised data base clustering based on Daylight’s fingerprint and Tanimoto similarity: a fast and automated way to cluster small and large data sets. *J. Chem. Inf. Comput. Sci.*, 39(4):747–750, 1999.
- [23] CDK. The Chemistry Development Kit http://sourceforge.net/projects/cdk, January 2010.
- [24] M. Chavent, Y. Lechevallier, and O. Briant. DIVCLUS-T: A monothetic divisive hierarchical clustering method. *Computational Statistics & Data Analysis*, pages 687–701, 2007.
- [25] Digital Chemistry. Digital Chemistry - Products http://www.digitalchemistry.co.uk/prod_toolkit.html, January 2010.
- [26] X. Chen, A. Rusinko III, and S.S. Young. Recursive partitioning analysis of a large structure-activity data set using three-dimensional descriptors. *J. Chem. Inf. Comput. Sci.*, pages 1054–1062, 1998.
- [27] Y. Cheng and G.M. Church. Biclustering of expression data. In *Proceedings of the 8th International Conference on Intelligent Systems for Molecular Biology*, pages 93–103, 2000.
- [44] I. Fáry. On straight line representation of planar graphs. *Acta. Sci. Math. Szeged*, 11:229–233, 1948.
- [45] G.S. Fishman. *Monte Carlo Concepts, Algorithms, and Applications*. Springer, first edition, 1996.
- [46] M.A. Fligner, J.S. Verducci, and P.E. Blower. A modification of the Jaccard-Tanimoto similarity index for diverse selection of chemical compounds using binary strings. *Technometrics*, 44(2):110–119, 2002.
- [47] National Center for Biotechnology Information. National Center for Biotechnology Information http://www.ncbi.nlm.nih.gov, January 2010.
- [48] National Center for Biotechnology Information. PubChem http://pubchem.ncbi.nlm.nih.gov, January 2010.
- [49] E.W. Forgy. Cluster analysis of multivariate data: efficiency vs interpretability of classifications. *Biometrics*, 21:768–769, 1965.
- [50] D.J. Galas and S.J. McCormack, editors. *Genomic Technologies Present and Future*. Caister Academic Press, 2002.
- [51] M.N. Gamito and S.C. Maddock. Accurate multidimensional Poisson-disk sampling. *ACM Transactions on Graphics*, 29(8), 2009.
- [52] J.E. Gentle. *Random Number Generation and Monte Carlo Methods*. Springer, second edition, 2004.
- [53] A.C. Gibbs and D.K. Agrafiotis. Chemical diversity: definition and quantification. In P. Bartlett and M. Entzeroth, editors, *Exploiting Chemical Diversity for Drug Discovery*, pages 139–160. The Royal Society of Chemistry, 2006.
- [54] J.C. Gower and P. Legendre. Metric and Euclidean properties of dissimilarity coefficients. *J. Class.*, 3(3):5–48, 1986.
- [55] R.L. Graham, D.E. Knuth, and O. Patashnik. *Concrete Mathematics*. Addison-Wesley Professional, second edition, 1994.
- [56] J.A. Grant, M.A. Gallardo, and B.T. Pickup. A fast method of molecular shape comparison: a simple application of a Gaussian description of molecular shape. *J. Comb. Chem.*, 17(14):1653–1666, 1996.
- [57] J.A. Grant, J.A. Haigh, B.T. Pickup, A. Nichols, and R.A. Sayle. Lingos, finite state machines and fast similarity searching. *J. Chem. Inf. Model*, 46(5):1912–1918, 2006.
- [58] R. Guha, D. Dutta, D. Wild, and T. Chen. Counting clusters using R-NN curves. *J. Chem. Inf. Model.*, 47(4):1308–1318, 2007.
