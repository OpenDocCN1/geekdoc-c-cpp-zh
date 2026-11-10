as the universal set or universe of discourse or domain. A fuzzy set on U is defined as

$$\mu_A(x): U \to [0,1] \tag{1.1}$$

Here $\mu_A$ is known as the membership function, and $\mu_A(x)$ is known as the membership grade of $x$. Membership function is the degree of truth or degree of compatibility. The membership function is the crucial component of a fuzzy set. Therefore all the operations on fuzzy sets are defined based on their membership functions. Table 1.1 defines fuzzy set theoretic operators that are analogues for their traditional set counterparts.

**TABLE 1.1: Fuzzy Set Theoretic Operators**

| Operator | Definition |
|---|---|
| Intersection | The membership function $\mu_{\overline{C}}(x)$ of the intersection $\overline{C} = \overline{A} \cap \overline{B}$ is defined by $\mu_{\overline{C}}(x) = \min\{\mu_{\overline{A}}(x), \mu_{\overline{B}}(x)\}, x \in X$ |
| Union | The membership function $\mu_{\overline{C}}(x)$ of the union $\overline{C} = \overline{A} \cup \overline{B}$ is defined by $\mu_{\overline{C}}(x) = \max\{\mu_{\overline{A}}(x), \mu_{\overline{B}}(x)\}, x \in X$ |
| Complement | The membership function $\mu_{\overline{C}}(x)$ of the complement of a normalized fuzzy set $\overline{A}$ is defined by $\mu_{\overline{C}}(x) = 1 - \mu_{\overline{A}}(x), x \in X$ |

Fuzzy relations play a vital role in fuzzy logic and its applications. Fuzzy relations are fuzzy subsets of $X \times Y$ defined as the mapping from $X \to Y$. If $X, Y \subseteq R$ are universal sets then the fuzzy relation is defined as $\tilde{R}\{((x,y), \mu_{\tilde{R}}(x,y)) \mid (x,y) \in X \times Y\}$. These fuzzy relations in different product spaces can be combined with each other through the operation combination. There are two basic forms of composition, namely the min-max and the max-product composition.

Min-Max Composition: Let $R_1 \subseteq X \times Y$ and $\tilde{R}_2 \subseteq Y \times Z$ denote two fuzzy relations, the min-max composition on these relations is defined as $R_1 \circ R_2 = \max\{\min\{\mu_{R_1}(x,y), \mu_{R_2}(y,z)\}\}_{x \in X, y \in Y, z \in Z}$

Max Product Composition: Let $R_1 \subseteq X \times Y$ and $\tilde{R}_2 \subseteq Y \times Z$ denote two fuzzy relations, the max product composition on these relations is defined as $R_1 \circ R_2 = \max\{\min\{\mu_{R_1}(x,y) * \mu_{R_2}(y,z)\}\}_{x \in X, y \in Y, z \in Z}$

The membership of a fuzzy set is described by this membership function $\mu_A(x)$ of $A$, which associates to each element $x_o \in X$ a grade of membership $\mu_A(x_o)$. The notation for the membership function $\mu_A(x)$ of a fuzzy set $A$ $A$ :