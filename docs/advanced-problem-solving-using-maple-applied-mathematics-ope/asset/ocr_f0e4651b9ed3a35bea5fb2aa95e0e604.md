# TABLE 5.3: Matrixville’s Closed Exchange Model

| | Food | Clothes | Housing | Energy | Moonshine |
|---|---:|---:|---:|---:|---:|
| Farmer | 0.25 | 0.15 | 0.25 | 0.18 | 0.20 |
| Tailor | 0.15 | 0.28 | 0.18 | 0.17 | 0.05 |
| Carpenter | 0.22 | 0.19 | 0.22 | 0.22 | 0.10 |
| Coal Miner | 0.20 | 0.15 | 0.20 | 0.28 | 0.15 |
| Slacker Bob | 0.18 | 0.23 | 0.15 | 0.15 | 0.50 |

So for example, the Carpenter consumes 22% of all food, 19% of all clothes, 22% of all housing, 22% of all energy and 10% of all High Quality 100 Proof Moonshine.

If the matrix $I-T$ is invertible, the total demand equation, $x=Tx+d$ can be solved for $x$.

+   (a) Determine $C=I-T$ using [Table 5.3](#).
+   
+   (b) If possible, determine $C^{-1}$.
+   
+   (c) If feasible, compute the total demand $x$ for this closed exchange model.
+   
+   (d) For those who have studied linear algebra: what is the relation between the total demand $x$ and the eigenvalues and eigenvectors of $T$, if any?

# 5.4 Stoichiometric Chemical Balancing and Infinitely Many Solutions

During your life you have witnessed numerous chemical reactions. How would you describe them to someone else? How could you obtain quantitative information about the reaction? Chemists use *stoichiometric chemical equations* to answer these questions.

By definition, a chemical equation is a written representation of a chemical reaction, showing the reactants and products, their physical states, and the direction in which the reaction proceeds. In addition, many chemical equations designate the conditions necessary (such as high temperature) for the reaction to occur. A chemical equation provides stoichiometric information about a chemical reaction, only if the equation is balanced.

For a chemical equation to be balanced, the same number of each kind of atom must be present on both sides of the chemical equation. The French