
The FBF network can be regarded as a feedforward connectionist system with one hidden layer whose units correspond to the fuzzy rules. In Figure 4.1 a connectionist interpretation of the FBF network is shown. In the drawing, circles represent adaptive units, while squares stand for not-adaptive units, and free parameters are evidenced near the corresponding units.

The FBF network can be identified both by exploiting the linguistic knowledge available (*structure identification problem*) [16] and by using the information contained in a data set (*parameter estimation problem*) [16].

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_163_0.png)

Figure 4.1 Connectionist interpretation of the FBF network.

## 4.3 Bayes Optimal Classifier Approximation

In the neural network literature, it has been demonstrated that a classifier based on an MLP can approximate the Bayes optimal discriminant function, for suitable choices of the cost function to be minimized during the training phase, and in the large training set limit [2,11,14,20,25].

In [18], we generalized this result and demonstrated, following Ruck et al. [25], that a classifier based on a system holding the universal function approximation property can approximate the Bayes discriminant function⁴. The demonstration we present here concerns the two-class case.

Let c₁ e c₂ be two classes of patterns. Let χᵢ be the set of all possible patterns x belonging to class cᵢ; then χ = χ₁ ∪ χ₂ represents the set of all patterns. The training set consists of a subset of possible patterns belonging to the two classes. In general, it is a finite set X = X₁ ∪ X₂, where X₁ = {x₁,x₂,...,xₙ₁} ⊂ χ₁, X₂ = {xₙ₁+1,...,xₙ₁+ₙ₂} ⊂ χ₂, and n₁ + n₂ = N.

Let w be the set of adaptive parameters, g(x) be the discriminant function of a Bayes dichotomizer

g(x) = P(c₁ | x) − P(c₂ | x), (4.7)

and F(x, w) be the system output.

Moreover, let us suppose that the system is trained in such a way that its response is +1 when x belongs to the class c₁, and −1 when x belongs to c₂:

F(x, w) = { +1 if x ∈ c₁
            −1 if x ∈ c₂ }. (4.8)

This is accomplished by minimizing (e.g., with the error backpropagation technique [26]) the sample data error function:

Eₛ(w) = Σ_{x∈X₁}[F(x,w)−1]² + Σ_{x∈X₂}[F(x,w)+1]². (4.9)

We shall demonstrate that in the large N limit, when w minimizes Eₛ(w), then w minimizes also:

ε²(w) = ∫_χ [F(x,w)−g(x)]² p(x) dx, (4.10)

i.e., F(x, w) approximates g(x).

Let us define the *average error function* as the function

$$E_a(\mathbf{w}) = \lim_{N\to\infty} \frac{1}{N} E_s(\mathbf{w}) \tag{4.11}$$

where $N$ is the total number of pattern vectors. $E_a(\mathbf{w})$ represents the error surface that is obtained when all possible vectors are used for the computation.

As assumed, in the large $N$ limit, we can suppose that the function $E_s$ is a reasonable approximation for $E_a$.

Let us rewrite the function $E_a$ as follows:

$$E_a(\mathbf{w}) = \lim_{N\to\infty} \left[ \frac{n_1}{N} * \frac{1}{n_1} \sum_{\mathbf{x}\in X_1} [F(\mathbf{x},\mathbf{w})-1]^2 + \frac{n_2}{N} * \frac{1}{n_2} \sum_{\mathbf{x}\in X_2} [F(\mathbf{x},\mathbf{w})+1]^2 \right] \tag{4.12}$$

where $n_i$ is the number of vectors belonging to the class $c_i$, and $\frac{n_1}{N}$ and $\frac{n_2}{N}$ represent, in the large $N$ limit, the a priori probabilities $P(c_1)$ and $P(c_2)$, respectively.

The quantities $\frac{1}{n_i} \sum_{\mathbf{x}\in X_i} [F(\mathbf{x},\mathbf{w}) - 1]^2$ represent the average value of $[F(\mathbf{x},\mathbf{w}) - 1]^2$, over the patterns, provided that $\mathbf{x} \in c_i$.

By exploiting the strong law of large number [23], we can rewrite Eq. 4.12 as

$$\begin{aligned}
E_a(\mathbf{w}) &= P(c_1) \int_{\chi} [F(\mathbf{x},\mathbf{w}) - 1]^2 p(\mathbf{x} \mid c_1) d\mathbf{x} + \\
&+ P(c_2) \int_{\chi} [F(\mathbf{x},\mathbf{w}) + 1]^2 p(\mathbf{x} \mid c_2) d\mathbf{x} \\
&= \int_{\chi} [F^2(\mathbf{x},\mathbf{w}) + 1] [p(\mathbf{x} \mid c_1)P(c_1) + p(\mathbf{x} \mid c_2)P(c_2)] d\mathbf{x} + \\
&-2 \int_{\chi} F(\mathbf{x},\mathbf{w}) [p(\mathbf{x} \mid c_1)P(c_1) - p(\mathbf{x} \mid c_2)P(c_2)] d\mathbf{x}
\end{aligned}\tag{4.13}$$

The probability density function of the input vectors can be expressed as:

$$p(\mathbf{x}) = p(\mathbf{x} \mid c_1)P(c_1) + p(\mathbf{x} \mid c_2)P(c_2) \tag{4.14}$$

Moreover, by using the Bayes rule, we can write:

$$\begin{aligned}
g(\mathbf{x})p(\mathbf{x}) &= [P(c_1 \mid \mathbf{x}) - P(c_2 \mid \mathbf{x})]p(\mathbf{x}) \\
&= P(c_1 \mid \mathbf{x})p(\mathbf{x}) - P(c_2 \mid \mathbf{x})p(\mathbf{x}) \\
&= p(\mathbf{x} \mid c_1)P(c_1) - p(\mathbf{x} \mid c_2)P(c_2)
\end{aligned}\tag{4.15}$$

## 4.5 Data Base and Preprocessing

Δm_jk = η_m φ_j Σ_i [t_i − y_i][ȳ_ij − y_i][x_k − m_jk]/σ_jk² (4.20)
Δσ_jk = η_σ φ_j Σ_i [t_i − y_i][ȳ_ij − y_i][x_k − m_jk]²/σ_jk³ (4.21)
where
φ_j = Π_k μ_jk(x_k) / Σ_j Π_k μ_jk(x_k) (4.22)

represents the normalized activation of rule j, and η_s, η_m, and η_σ are the learning rates for ȳ_ij, m_jk, and σ_jk, respectively. In our experiments, we adopted an adaptive learning-rate scheme, as proposed in [27], and we noticed a considerable speed-up of the training phase [3].

If a linguistic description of classes is available, in addition to the numerical training set, the FBF network permits the integration of these two types of information. On the contrary, if a linguistic description is not available, as is the case with our experiments, the structure identification must be achieved experimentally according to a performance-based criterion.

| Rules | Parameters | (%L, %T) | epochs | (%L1, %T1) | Time (min) |
|---|---|---|---|---|---|
| 24 | 3312 | (97.55, 94.00) | 30 | (91.0, 88.0) | 3.5 |
| 32 | 4416 | (98.05, 95.00) | 30 | (89.0, 87.0) | 4.0 |
| 48 | 6624 | (98.65, 95.81) | 30 | (91.5, 88.5) | 16.0 |
| 64 | 8832 | (98.32, 96.02) | 30 | (93.5, 92.0) | 23.0 |
| 128 | 17664 | (98.97, 96.20) | 30 | (94.5, 93.5) | 46.0 |

Table 4.1 FBF network performances. From left to right, the columns represent the number of rules mapped on the FBF network, the number of adaptive parameters, the percentages of learning success (%L) and of test success (%T) after the training phase, the number of epochs required by the training phase, the percentages of learning success (%L1) and of test success (%T1) at end of the first epoch, and the duration of each epoch (in min on a SUN 10/20).

All the experiments reported in the following sections were carried out on a SUN 10/50 workstation (except those in Table 4.1). We used a data set of 30000 samples extracted from the NIST-3 data base [9]. The NIST-3 data-base, distributed on a CD-ROM, contains 313389 handwritten characters coded as 128×128 binary-matrix images and labeled by the corresponding ASCII codes. We partitioned the data set in a training set, a test set and a validation

| Training set | FBF₁ | FBF₂ | FBF₃ | FBF₄ | FBF₅ |
| Class | Examples | % | % | % | % | % |
| 0 | 1052 | 100 | 100 | 100 | 100 | 100 |
| 1 | 1134 | 100 | 100 | 100 | 1.234 | 1.410 |
| 2 | 966 | 100 | 100 | 100 | 100 | 100 |
| 3 | 1059 | 100 | 100 | 100 | 100 | 100 |
| 4 | 967 | 100 | 3.177 | 1.964 | 2.378 | 3.309 |
| 5 | 842 | 100 | 100 | 100 | 100 | 100 |
| 6 | 948 | 100 | 100 | 100 | 100 | 4.00 |
| 7 | 1052 | 100 | 100 | 100 | 100 | 100 |
| 8 | 978 | 0.0 | 1.87 | 5.725 | 6.032 | 6.748 |
| 9 | 1002 | 100 | 100 | 2.295 | 2.694 | 2.694 |
| Training set | FBF₆ | FBF₇ | FBF₈ | FBF₉ | FBF₁₀ |
| Class | Examples | % | % | % | % | % |
| 0 | 1052 | 1.615 | 1.711 | 1.711 | 1.711 | 1.806 |
| 1 | 1134 | 1.410 | 1.410 | 1.499 | 1.499 | 1.587 |
| 2 | 966 | 100. | 4.968 | 5.590 | 6.004 | 6.107 |
| 3 | 1059 | 100 | 100 | 100 | 3.966 | 4.438 |
| 4 | 967 | 3.826 | 3.826 | 3.826 | 3.826 | 3.826 |
| 5 | 842 | 100 | 100 | 100 | 100 | 11.63 |
| 6 | 948 | 4.00 | 4.113 | 4.113 | 4.113 | 4.535 |
| 7 | 1052 | 100 | 100 | 2.471 | 2.471 | 2.471 |
| 8 | 978 | 6.952 | 7.668 | 7.873 | 8.077 | 8.691 |
| 9 | 1002 | 2.894 | 3.093 | 3.393 | 3.493 | 3.592 |

Table 4.2 Training set error rates on 10,000 patterns by ten different FBF networks, ranging from 1 to 10 rules.

## 4.7 FBFN Structure Identification and Semantic Phase Transition

In [4], ten different FBF networks have been trained on the training set described in Section 4.5. The FBF networks differ in the number of rules, ranging from 1 up to 10. In Table 4.2, for each class of digit the numbers of patterns in the training set and the percentage of patterns not correctly recognized by each FBF network at the end of the training phase are shown. It is worth noting a close relationship between the number of rules in the FBF network and the number of classes which are recognized by the FBF network: 10 − β classes are not recognized at all for FBF network with β rules, while the other classes are well recognized. On the contrary, in the case of FBF₁₀ (or of FBF networks with more than 10 rules) the error rate is uniformly distributed along all the classes. This behavior of the FBF network, that we call semantic phase transition, has been confirmed by further series of simulations, and is
