such that

$$T_0(\vec{p},\vec{r}) \cup \{p_{(0,0)}\} \cup T_0(\vec{q},\vec{r}) \cup \{\neg q_{(0,0)}\}$$

is unsatisfiable. At this point in the proof we can use the Craig interpolation theorem. This result guarantees the existence of a formula I(\vec{r}), such that:

$$T_0(\vec{p},\vec{r}) + p_{(0,0)} \vdash I(\vec{r})$$

and

$$I(\vec{r}) \vdash T_0(\vec{q},\vec{r}) \to q_{(0,0)}.$$

Although we write the whole array \vec{r} in I(\vec{r}), the formula obviously contains only finitely many r variables.

Thus by application of the deduction theorem we have that:

$$T_0(\vec{p},\vec{r}) \vdash p_{(0,0)} \to I(\vec{r})$$

and

$$T_0(\vec{q},\vec{r}) \vdash I(\vec{r}) \to q_{(0,0)}.$$

Then after suitably renaming the propositional variables we see that the the second implication gives:

$$T_0(\vec{p},\vec{r}) \vdash I(\vec{r}) \to p_{(0,0)}$$

i.e. together

$$T_0(\vec{p},\vec{r}) \vdash I(\vec{r}) \equiv p_{(0,0)}.$$

The interpolant I(\vec{r}) computes the symbol of cell (0,0) in the configuration prior to \vec{r}. This it defines the inverse to A. Let M \subseteq \mathbb{Z}^2 be the finite set of (s,t)\in \mathbb{Z}^2 such that r_{(s,t)} appears in I(\vec{r}). Finally the inverse cellular automaton B as follows:

+   1. Alphabet is 0,1;

+   2. The neighborhood is M;

+   3. The transition function is given by I(\vec{r}).

This concludes the proof.

We conclude this part about the Richardson theorem with a few remarks about the proof sketched above.

+   1. The construction of the inverse cellular automaton carried out in the proof given in (14) has two key moments. First the application of the compactness theorem after a suitable embedding into propositional logic. In a second moment the interpolation theorem is applied leading to some kind of effectiveness. Of course, the application of compactness leads to a non-recursive procedure but as we previously noticed this fact is unavoidable because of theorem 3.14.

+   2. The construction guarantees that
+   
+   $$G_B(G_A(\vec{p})) = \vec{p}$$
+   
+   but it does not - a priori - imply that also
+   
+   $$G_A(G_B(\vec{r})) = \vec{r}.$$