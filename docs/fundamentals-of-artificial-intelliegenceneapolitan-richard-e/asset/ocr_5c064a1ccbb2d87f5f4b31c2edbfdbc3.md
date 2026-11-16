The compound proposition $\neg A$ is called the **negation** of $A$, $A \wedge B$ is called the **conjunction** of $A$ and $B$, and $A \vee B$ is called the **disjunction** of $A$ and $B$.

Notice that we used italicized letters to refer to propositions. Such letters denote variables whose values can be propositions that are either atomic or compound. In this way we can recursively define compound propositions. These italicized letters are not part of the alphabet.

**Example 2.1** Suppose P and Q are atomic propositions. Then applying Rule 2 once using the $\wedge$ connective, we have that P$\wedge$Q is a proposition. Applying Rule 2 to this compound proposition and the atomic proposition R using the $\vee$ connective, we have that P$\wedge$Q$\vee$R is a proposition.

Mathematically, this is all there is to say about the formal language of propositional logic. However, propositional logic was developed to make statements about the real world and to reason with these statements. The next example illustrates such statements.

**Example 2.2** Suppose the propositions P and Q stand for these statements about the world:

+   - P: It is raining outside.
+   - Q: The pavement is wet.

Then the following compound propositions stand for these statements about the world:

+   - $\neg$P: It is not raining outside.
+   - P$\wedge$Q: It is raining outside and the pavement is wet.
+   - P$\vee$Q: It is raining outside or the pavement is wet.
+   - P$\Rightarrow$Q: If it is raining outside, then the pavement is wet.
+   - P$\Leftrightarrow$Q: It is raining outside if and only if the pavement is wet.

**Example 2.3** Let P, Q, and R stand for these statements about the world:

+   - P: It is raining outside.
+   - Q: The pavement is wet.
+   - R: The sprinkler is on.

Then applying Rule 2 once using the $\vee$ connective, we have that P$\vee$R is a proposition. Applying Rule 2 a second time using the $\wedge$ connective, we obtain that Q$\wedge$P$\vee$R is a proposition. This proposition stands for the following statement about the world:

+   - Q$\wedge$P$\vee$R: The pavement is wet and it is raining outside or the sprinkler is on.