Table 1. Truth tables of an elementary CA rule \(\mathcal{N}\) and its globally-equivalent rules \(\mathcal{N}^{\prime}\), \(\mathcal{N}^{\dagger}\), and \(\mathcal{N}^{*}\). The output values \(\beta_k\), \(k \in [0,7]\), are binary, \(\beta_k=\pm1\).

| \(x_{i-1}\) | \(x_i\) | \(x_{i+1}\) | \(\mathcal{M}_{\mathcal{N}}\) | \(\mathcal{M}_{\overline{\mathcal{N}}}\) | \(\mathcal{M}_{\mathcal{N}^{\dagger}}\) | \(\mathcal{M}_{\mathcal{N}^{*}}\) |
|---:|---:|---:|---:|---:|---:|---:|
| −1 | −1 | −1 | \(\beta_0\) | \(\beta_7\) | \(\beta_0\) | \(\beta_7\) |
| −1 | −1 | 1 | \(\beta_1\) | \(\beta_6\) | \(\beta_4\) | \(\beta_3\) |
| −1 | 1 | −1 | \(\beta_2\) | \(\beta_5\) | \(\beta_2\) | \(\beta_5\) |
| −1 | 1 | 1 | \(\beta_3\) | \(\beta_4\) | \(\beta_6\) | \(\beta_1\) |
| 1 | −1 | −1 | \(\beta_4\) | \(\beta_3\) | \(\beta_1\) | \(\beta_6\) |
| 1 | −1 | 1 | \(\beta_5\) | \(\beta_2\) | \(\beta_5\) | \(\beta_2\) |
| 1 | 1 | −1 | \(\beta_6\) | \(\beta_1\) | \(\beta_3\) | \(\beta_4\) |
| 1 | 1 | 1 | \(\beta_7\) | \(\beta_0\) | \(\beta_7\) | \(\beta_0\) |

An elementary CA rule can be represented by means of a truth table, as shown in Table 1. There are \(2^8=256\) possible combination of the eight values \(\beta_k=\pm1\), \(k\in[0,7]\) in Table 1, each corresponding to one CA rule. The elementary CA rules can be numbered from 0 to 255 thanks to the following formula:

\[\mathcal{N}=(\beta_7\beta_6\beta_5\beta_4\beta_3\beta_2\beta_1\beta_0)_2=\sum_{k=0}^{7}\left(2^k\cdot\frac{\beta_k+1}{2}\right).\tag{2}\]

At first sight, elementary Cellular Automata may appear not complex enough to deserve to be studied; obviously, it is not the case. Actually, it is possible to prove that some elementary CA rules have the same computational complexity as the universal Turing machine [3]. The great advantage of studying such a simple model is that it is possible to formalize concepts that can be easily extended to more complex CA models. This is the reason why both Chua and Wolfram, alongside innumerable other authors, focused their attention mainly on this particular class.

# 2.2. *Global and quasi-globally equivalent rules*

It may happen that the dynamics of a rule \(\mathcal{N}\) can be inferred from the one of a different rule \(\mathcal{N}'\), and vice versa; in this case, the two rules are said to be globally equivalent according to the following definition:

**Definition 14.1 [Global equivalence].** *Two CA rules \(\mathcal{N}\) and \(\mathcal{N}'\) are globally equivalent if there exists a transformation \(T':\Sigma\to\Sigma\) such that \(\mathcal{M}_{\mathcal{N}}^n(\mathbf{x}^0)=T'(\mathcal{M}_{\mathcal{N}'}^n(T'(\mathbf{x}^0))),\ \forall n\in\mathbb{N}\) and any initial state \(\mathbf{x}^0\).*

By abuse of notation, we can write \(\mathcal{N}'=T'(\mathcal{N})\). It is possible to prove that there are three such transformations. The first one is called *global complementation* \(\overline{T}\) and it complements all cells of the state \(\mathbf{x}\) of the Cellular Automaton; thus, \(\overline{T}(\mathbf{x})=\overline{\mathbf{x}}\), where \(\overline{x_i}=-x_i\ \forall i\in[0,L-1]\). Given a CA rule \(\mathcal{N}=(\beta_7\beta_6\beta_5\beta_4\beta_3\beta_2\beta_1\beta_0)_2\), rule \(\overline{\mathcal{N}}=\overline{T}(\mathcal{N})\) can be found directly from Def. 14.1 when \(n=1\). Therefore, \(\mathcal{M}_{\mathcal{N}}^1(\mathbf{x}^0)=\mathcal{M}_{\overline{\mathcal{N}}}^1(\overline{\mathbf{x}^0})\), which implies that \((x_{i-1}x_ix_{i+1})\xrightarrow{\mathcal{N}}\beta_j\Rightarrow(\overline{x_{i-1}x_ix_{i+1}})\xrightarrow{\overline{\mathcal{N}}}\beta_j\), \(\forall j\in[0,7]\). Applying this transformation to the eight rows of Table 1, we find that \(\overline{\mathcal{N}}=(\beta_0\beta_1\beta_2\beta_3\beta_4\beta_5\beta_6\beta_7)_2\).

The second transformation is called *left-right transformation* \(T^{\dagger}\) and it mirrors the states of the Cellular Automaton; thus, \(T^{\dagger}(\mathbf{x})=\mathbf{x}^{\dagger}\), where \(x_i^{\dagger}=x_{L-1-i}\ \forall i\in[0,L-1]\). Given a CA rule \(\mathcal{N}=(\beta_7\ \beta_6\beta_5\ \beta_4\beta_3\beta_2\beta_1\beta_0)_2\), rule \(\mathcal{N}^{\dagger}=T^{\dagger}(\mathcal{N})\) can be found directly from Def. 14.1, when \(n=1\). Therefore, \(\mathcal{M}_{\mathcal{N}}^1(\mathbf{x}^0)=(\mathcal{M}_{\mathcal{N}^{\dagger}}^1(\mathbf{x}^{\dagger}))^{\dagger}\), which implies that \((x_{i-1}x_ix_{i+1})\xrightarrow{\mathcal{N}}\beta_j\Rightarrow(x_{i+1}x_ix_{i-1})\xrightarrow{\mathcal{N}^{\dagger}}\beta_j\), \(\forall j\in[0,7]\). Applying this transformation to the eight rows of Table 1, we find that \(\mathcal{N}^{\dagger}=(\beta_7\beta_3\beta_5\beta_1\beta_6\beta_2\beta_4\beta_0)_2\).

The third transformation is called *left-right complementation* \(T^*\) and it is a combination of the previous two as it mirrors all states of the Cellular Automaton and complements the single cells; therefore, \(T^*(\mathbf{x})=\mathbf{x}^*\), where \(x_i^*=x_{L-1-i}\ \forall i\in[0,L-1]\). Given a CA rule \(\mathcal{N}=(\beta_7\beta_6\beta_5\beta_4\beta_3\beta_2\beta_1\beta_0)_2\), rule \(\mathcal{N}^*=T^*(\mathcal{N})\) can be found directly from Def. 14.1, when \(n=1\). Therefore, \(\mathcal{M}_{\mathcal{N}}^1(\mathbf{x}^0)=(\mathcal{M}_{\mathcal{N}^*}^1(\mathbf{x}^{0*}))^*\), which implies that \((x_{i-1}x_ix_{i+1})\xrightarrow{\mathcal{N}}\beta_j\Rightarrow(\overline{x_{i+1}x_ix_{i-1}})\xrightarrow{\mathcal{N}^*}\overline{\beta_j}\), \(\forall j\in[0,7]\). Applying this transformation to the eight rows of Table 1, we find that \(\mathcal{N}^*=(\overline{\beta_7}\overline{\beta_3}\overline{\beta_5}\overline{\beta_1}\overline{\beta_6}\overline{\beta_2}\overline{\beta_4}\overline{\beta_0})_2\).

Some elementary CA rules are invariant with respect to some of these transformations. Specifically, 64 rules are fixed points of the left-right transformation \(T^{\dagger}\), 16 rules are fixed points of the global complementation \(\overline{T}\), and 16 rules are fixed points of the left-right complementation \(T^*\). Remarkably, 8 rules are fixed points of all three transformations. To sum up, 176 rules are globally-equivalent to three other rules, 72 rules are globally-equivalent to one other rule, and eight rules are not globally-equivalent to any other rule. The list of all elementary CA rules and their globally-equivalent rules is displayed in Tables 2 and 3.

In conclusion, the 256 elementary CA rules can be partitioned into 88 equivalence classes, each made up of either one, two or four rules. For each