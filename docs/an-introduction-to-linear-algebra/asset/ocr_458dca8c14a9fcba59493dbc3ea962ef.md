if \(r(A)=m<n\) (\(r(A)=n<m\)). When does \(A\) have exactly one right (left) inverse?

**11.7.** Let \(A \in R^{m \times n}\). Show that \(A\) has a right inverse if and only if the columns of \(A\) span \(R^m\).

**11.8.** Let \(A \in R^{m \times n}\). Show that \(A\) has a left inverse if and only if \(A^t\) has a right inverse.

**11.9.** Let \(A \in R^{m \times n}\). Show that if the right inverse \(R\) of \(A\) exists, then \(R = A^t(AA^t)^{-1}\).

**11.10.** Let \(A \in R^{m \times n}\). Show that if the left inverse \(L\) of \(A\) exists, then \(L = (A^tA)^{-1}A^t\).

**11.11.** Compute right inverse for the following matrices

(i) \(\begin{pmatrix} 1 & 2 & 3 & 7 \\ -1 & 4 & -2 & 5 \\ 3 & 7 & 0 & 3 \end{pmatrix}\) (ii) \(\begin{pmatrix} 5 & 3 & 2 & 1 \\ 4 & 2 & 1 & 3 \\ 1 & 5 & 3 & 5 \end{pmatrix}\).

**11.12.** Compute left inverse for the following matrices

(i) \(\begin{pmatrix} 1 & 1 & 1 \\ 2 & 3 & 4 \\ 3 & 4 & 7 \\ 4 & 5 & 6 \end{pmatrix}\) (ii) \(\begin{pmatrix} 1 & -3 & 5 \\ 2 & 4 & -2 \\ 3 & 5 & 2 \\ 0 & 3 & 7 \end{pmatrix}\).

# ## Answers or Hints

**11.1.** (i) \(r(A) = 3\), \(\{(1,0,-1,-2,0),(0,1,2,3,0),(0,0,0,0,1)\}\), \(\{(1,0,0)^t,(0,1,0)^t,(0,0,1)^t\}\), \(\{(1,-2,1,0,0)^t,(2,-3,0,1,0)^t\}\).

(ii) \(r(A) = 3\), \(\{(1,3,5,7,2,4),(0,0,7,9,-2,-1),(0,0,0,16,61,62)\}\), \(\{(1,0,0)^t,(0,1,0)^t,(0,0,1)^t\}\), \(\{(-3,1,0,0,0,0)^t,(-20,0,83,-61,16,0)^t,(-40,0,82,-62,0,16)^t\}\).

**11.2.** \(x \in \mathcal{N}(A) \Rightarrow Ax = 0 \Rightarrow A^t(Ax) = 0 \Rightarrow x \in \mathcal{N}(A^tA) \Rightarrow \mathcal{N}(A) \subseteq \mathcal{N}(A^tA)\). Next, \(x \in \mathcal{N}(A^tA) \Rightarrow A^tAx = 0 \Rightarrow x^tA^tAx = 0 \Rightarrow (Ax)^t(Ax) = 0 \Rightarrow Ax = 0 \Rightarrow x \in \mathcal{N}(A) \Rightarrow \mathcal{N}(A) \subseteq \mathcal{N}(A^tA)\). For the second part, change \(A\) to \(A^t\).

**11.3.** \(A \in R^{m \times n} \Rightarrow A^tA \in R^{n \times n}\). By Theorem 11.4, \(r(A) + n(A) = n\) and \(r(A^tA) + n(A^tA) = n\). From Problem 11.2, \(n(A) = n(A^tA)\). Hence, \(r(A) = n\) if and only if \(r(A^tA) = n\). \(C(A^t) = C(A^tA)\) is equivalent to \(r(A^t) = r(A^tA)\). The third part is similar.

**11.4.** \(AB \in R^{m \times m}\). From Theorem 11.2, \(r(AB) \le n < m\).

**11.5.** See Problem 5.2.

**11.6.** If for \(A \in R^{m \times n}\), \(r(A) = m < n\), then from Theorem 11.6, \(A\) has a