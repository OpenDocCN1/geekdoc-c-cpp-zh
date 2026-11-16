Proof: Part (i) is clear because wt(u) is the count of the number of nonzero coordinates of u, and for all such coordinates i, v_i = \alpha u_i for \alpha = v_i u_i^{-1} \in F_q. To prove (ii) we note that the coordinates are divided into four disjoint sets for each \alpha:

+   (a) the coordinates i where u_i = v_i = 0,
+   (b) the coordinates i where u_i = 0 but v_i \neq 0,
+   (c) the coordinates i where u_i \neq 0 and u_i = \alpha u_i, and
+   (d) the coordinates i where u_i \neq 0 and u_i \neq \alpha u_i.

Clearly, wt(v - u) is the sum of the number of coordinates in (b) and (d). By definition, there are n_{\alpha, u} coordinates in (b). As there are wt(u) total coordinates in (c) and (d), and (c) has \alpha u coordinates, then (d) has wt(u) - \alpha u coordinates, proving (ii).

Part (iii) follows from part (ii) as wt(v - u) \equiv wt(u) \equiv 0 (mod \Delta) because C is linear and divisible by \Delta. Finally, combining (i) and (iii) gives

0 \equiv wt(u) \equiv \sum_{\alpha \in F_q} \alpha u_\alpha \equiv \sum_{\alpha \in F_q} n_{\alpha, u} \equiv q n_{0, u} (\text{mod } \Delta).

verifying (iv).

We next examine the situation that will lead to part (v) of the Gleason-Pierce-Ward Theorem. To state this result, we need the concept of a coordinate functional of a code C over F_q of length n. For 1 \le i \le n, define the coordinate functional f_i : C \to F_q by f(c) = c_i where c = c_1 \cdots c_n. Let N be the set of nonzero coordinate functionals of C. We define the binary relation \sim on N by f_i \sim f_j provided there exists an element \alpha \in F_q^* such that f_i(c) = \alpha f_j(c) for all c \in C. We make two simple observations, which you are asked to prove in Exercise 564. First, f_i is a linear function and hence its values are completely determined by its values on the codewords in a generator matrix. Second, \sim is an equivalence relation on N. In the next lecture, we will see that C is equivalent to a replicated code whenever C has a divisor relatively prime to the order of the field. We say that a code C is a \Delta-fold replicated code provided the set of coordinates of C is the disjoint union of subsets of coordinates of sizes \Delta such that if \{j_i | 1 \le j \le \Delta\} is any of these subsets and c = c_1 \cdots c_n \in C, then c_{j_i} = c_{j_1} for 1 \le j \le \Delta. In terms of coordinate functionals, these functionals are equal on the subsets of coordinates. The code with generator matrix [I_{n/2} | I_{n/2}] in (v) of the Gleason-Pierce-Ward Theorem is a two-fold replicated code.

# Exercise 564 Show the following:

+   (a) The coordinate functional f_i is a linear function from C to F_q, and its values are completely determined by its values on the codewords in a generator matrix of C.
+   (b) The relation \sim on the set N of nonzero coordinate functionals is an equivalence relation on N.

# Lemma 9.11.13 Let C be an [n, k] code over F_q with divisor \Delta relatively prime to p. Then the following hold:

+   (i) Each equivalence class of nonzero functionals has size a multiple of \Delta.
+   (ii) C is monomially equivalent to a \Delta-fold replicated code possibly with some coordinates that are always 0.