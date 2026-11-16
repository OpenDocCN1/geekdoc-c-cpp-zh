# Exercise 129

+   (a) Compute \( g(5, 4) \) from (2.40).
+   (b) What are the smallest weights that Theorem 2.7.7 guarantees can be used in a basis of a \([10, 5, 4]\) binary code?
+   (c) Show that a \([10, 5, 4]\) binary code with only even weight codewords has a basis of weight 4 codewords.
+   (d) Construct a \([10, 5, 4]\) binary code with only even weight codewords.

Both Theorems 2.7.6 and 2.7.7 can be generalized in the obvious way to codes over \(\mathbb{F}_q\); see [68]. In particular, codes over \(\mathbb{F}_q\) that meet the Griesmer Bound have a basis of minimum weight codewords. This is not true of codes in general but is true for at least one code with the same parameters, as the following theorem of Simonis [308] shows. This result may prove to be useful in showing the nonexistence of linear codes with given parameters \([n, k, d]\).

# Theorem 2.7.8

Suppose that there exists an \([n, k, d]\) code \(C\) over \(\mathbb{F}_q\). Then there exists an \([n, k, d]\) code \(C'\) with a basis of codewords of weight \(d\).

Proof: Let \(b\) be the maximum number of independent codewords \(\{c_1, \dots, c_b\}\) in \(C\) of weight \(d\). Note that \(s \ge 1\) as \(C\) has minimum weight \(d\). We are done if \(s = k\). So assume \(s < k\). The theorem will follow by induction if we show that we can create from \(C\) an \([n, k, d]\) code \(C_1\) with at least \(s + 1\) independent codewords of weight \(d\). Let \(S = \text{span}\{c_1, \dots, c_s\}\). By the maximality of \(s\), every vector in \(C \\ S\) has weight greater than \(d\). Let \(e_1\) be a minimum weight vector in \(C \\ S\) with \(\text{wt}(e_1) = d_1 > d\). Complete \(\{e_1, \dots, c_{e_1}\}\) to a basis \(\{c_1, \dots, c_r, e_1, e_2, \dots, e_{k-r}\}\) of \(C\). Choose \(d_1 - d\) nonzero coordinates of \(e_1\) and create \(e'_1\) to be the same as \(e_1\) except on these \(d_1 - d\) coordinates, where it is 0. So \(\text{wt}(e'_1) = d\). Let \(C_1 = \text{span}\{c_1, \dots, c_r, e'_1, e_2, \dots, e_{k-r}\}\). We show \(C_1\) has minimum weight \(d\) and dimension \(k\). The vectors in \(C_1\) fall into two disjoint sets: \(S = \text{span}\{c_1, \dots, c_r\}\) and \(C_1 \\ S\). The nonzero codewords in \(S\) have weight \(d\) or more as \(S \subset C\). The codewords in \(C_1 \\ S\) are obtained from those in \(C \\ S\) by modifying \(d_1 - d\) coordinates; therefore as \(C \\ S\) has minimum weight \(d_1\), \(C_1 \\ S\) has minimum weight at least \(d\). So \(C_1\) has minimum weight \(d\). Suppose that \(C_1\) has dimension less than \(k\). Then by our construction, \(e'_1\) must be in \(\text{span}\{c_1, \dots, c_r, e_2, \dots, e_{k-r}\} \subset C\). By maximality of \(s\), \(e'_1\) must in fact be in \(S\). So \(e_1 - e'_1 \in C \\ S\) as \(e_1 \notin S\). By construction \(\text{wt}(e_1 - e'_1) = d_1 - d\); on the other hand as \(e_1 - e'_1 \in C \\ S\), \(\text{wt}(e_1 - e'_1) \ge d_1\), since \(d_1\) is the minimum weight of \(C \\ S\). This contradiction shows that \(C_1\) is an \([n, k, d]\) code with at least \(s + 1\) independent codewords of weight \(d\).

# Exercise 130

Let \(C\) be the binary \([9, 4]\) code with generator matrix

| 1 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 0 |
|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 0 | 0 | 1 | 1 | 0 | 1 | 0 |
| 0 | 0 | 1 | 0 | 1 | 0 | 1 | 1 | 1 |
| 0 | 0 | 0 | 1 | 0 | 1 | 1 | 1 | 1 |