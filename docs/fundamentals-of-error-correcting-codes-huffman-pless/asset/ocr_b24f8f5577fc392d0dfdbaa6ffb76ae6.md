over \(\mathbb{F}_q\), where \(s\) runs through a set of representatives of the \(q\)-cyclotomic cosets modulo \(n\).

Let \(\mathcal{C}\) be a cyclic code in \(\mathcal{R}_n\) with generator polynomial \(g(x)\). By Theorems 4.1.1(i) and 4.2.1(vii), \(g(x) = \prod_i M_{\alpha^i}(x) = \prod_i \prod_{c \in C_i} (x - \alpha^c)\), where \(s\) runs through some subset of representatives of the \(q\)-cyclotomic cosets \(\mathcal{C}_i\) modulo \(n\). Let \(T = \bigcup_i C_i\) be the union of these \(q\)-cyclotomic cosets. The roots of unity \(\mathcal{Z} = \{\alpha^i \mid i \in T\}\) are called the zeros of the cyclic code \(\mathcal{C}\) and \(\{\alpha^i \mid i \notin T\}\) are the nonzeros of \(\mathcal{C}\). The set \(T\) is called the *defining set* of \(\mathcal{C}\). (Note that if we change the primitive \(n\)th root of unity, you change \(T\); so \(T\) is computed relative to a fixed primitive root. This will be discussed further in Section 4.5.) It follows that \(c(x)\) belongs to \(\mathcal{C}\) if and only if \(c(\alpha^i) = 0\) for each \(i \in T\) by Theorem 4.2.1. Notice that \(T\), and hence either the set of zeros or the set of nonzeros, completely determines the generator polynomial \(g(x)\). By Theorem 4.2.1, the dimension of \(\mathcal{C}\) is \(n - |T|\) as \(|T|\) is the degree of \(g(x)\).

**Example 4.4.1** In Example 4.3.4 a table giving the dimension, generator polynomials \(g_i(x)\), and generating idempotents \(e_i(x)\) of all the cyclic codes \(\mathcal{C}_i\) of length 7 over \(\mathbb{F}_2\) was given. We add to that table the defining sets of each code relative to the primitive root \(\alpha\) given in Example 3.4.3.

| i | dim | g(x) | e(x) | Defining set |
|---|---|---|---|---|
| 0 | 0 | \(1+x^7\) | 0 | \(\{0, 1, 2, 3, 4, 5, 6\}\) |
| 1 | 1 | \(1+x+x^2+\cdots+x^6\) | \(1+x+x^2+\cdots+x^6\) | \(\{1, 2, 3, 4, 5, 6\}\) |
| 2 | 3 | \(1+x^2+x^3+x^4\) | \(1+x^3+x^5+x^6\) | \(\{0, 1, 2, 4\}\) |
| 3 | 3 | \(1+x+x^2+x^4\) | \(1+x+x^2+x^4\) | \(\{0, 3, 5, 6\}\) |
| 4 | 4 | \(1+x+x^3\) | \(x+x^2+x^4\) | \(\{1, 2, 4\}\) |
| 5 | 4 | \(1+x^2+x^3\) | \(x^3+x^5+x^6\) | \(\{3, 5, 6\}\) |
| 6 | 6 | \(1+x\) | \(x+x^2+\cdots+x^6\) | \(\{0\}\) |
| 7 | 7 | 1 | 1 | \(\emptyset\) |

**Exercise 237** What would be the defining sets of each of the codes in Example 4.4.1 if the primitive root \(\beta = \alpha^3\) were used to determine the defining set rather than \(\alpha\)?

Our next theorem gives basic properties of cyclic codes in terms of their defining sets, summarizing the above discussion.

**Theorem 4.4.2** Let \(\alpha\) be a primitive \(n\)th root of unity in some extension field of \(\mathbb{F}_q\). Let \(\mathcal{C}\) be a cyclic code of length \(n\) over \(\mathbb{F}_q\) with defining set \(T\) and generator polynomial \(g(x)\). The following hold. (i) \(T\) is a union of \(q\)-cyclotomic cosets modulo \(n\). (ii) \(g(x) = \prod_{i \in T} (x - \alpha^i)\). (iii) \(c(x) \in \mathcal{C}_\alpha\) is in \(\mathcal{C}\) if and only if \(c(\alpha^i) = 0\) for all \(i \in T\). (iv) The dimension of \(\mathcal{C}\) is \(n - |T|\).

**Exercise 238** Let \(\mathcal{C}\) be a cyclic code over \(\mathbb{F}_q\) with defining set \(T\) and generator polynomial \(g(x)\). Let \(\mathcal{C}_\alpha\) be the subcode of all even-like vectors in \(\mathcal{C}\). (a) Prove that \(\mathcal{C}_\alpha\) is cyclic and has defining set \(T \cup \{0\}\). (b) Prove that \(\mathcal{C} = \mathcal{C}_\alpha\) if and only if \(0 \in T\) if and only if \(g(1) = 0\).