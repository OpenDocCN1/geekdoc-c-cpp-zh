# TABLE 15.1

Notations/Symbols

| Symbol | Description |
|---|---|
| ECC | Elliptic curve cryptography |
| IBC | Identity-based cryptography system |
| p | A large prime |
| ID_i | The unique identity of entity i |
| ε(F_p) | Elliptic curve ε over a prime finite field F_p |
| ski | The session key generated entities i |
| PKG | The private key generator |
| U | The user |
| S | Cloud server |
| M | Master key |
| G | ECC-based additive group |
| g | Base point of G |
| E | Adversary |
| || | Concatenation operation |
| Z_p* | Additive group of order p |
| MASK | Mutual authentication and session key |
| ⊕ | XOR-operation |

# 15.2.2 ID-Based Cryptography System

The concept of IBC was developed by Shamir in 1984 to remove the transmission, verification, and maintenance of public-key validity. In IBC, the user submitted his/her identity to a unique trusted authority called Private Key Generator (PKG). After that, PKG provides private, part-private, and public keys to users and PKG has a secret system master key, M (Shamir (1984)).

# 15.2.3 Background of Elliptic Curve Group

Let p be the large prime and E indicate an elliptic curve over a prime finite field F_p, demarcated by an equation y² = x³ + cx + d mod q, where, c, d ∈_R F_p, and 4c³ + 27d² mod q ≠ 0. The additive elliptic curve group is construed as G = {(x,y) : x,y ∈_R F_p ; (x,y) ∈_R E} ∪ {Θ}, where the point Θ is identified as a point at infinity that perform as the identity element in G. The point addition in the elliptic curve is: P = (x_P, y_P) ∈_R G and Q = (x_Q, y_Q) ∈_R G, where Q ≠ P then P + Q = (x_i, y_i), where x_i = μ² − x_P − x_Q mod q, y_i = (μ(x_P − x_Q) − y_P) mod q, and μ = (y_Q − y_P) / (x_Q − x_P). The scalar multiplication on the group G is explained as nP = P + P + P … + P (n times).

+   - **Elliptic Curve Discrete Logarithms Problem (ECDLP)**: For given P, Q ∈_R G find t ∈_R Z_q* such that P = tQ, which is hard (Kumar et al. (2019a)).

+   - **Elliptic Curve Computational Diffie–Hellman Problem (ECC DHP)**: For a, b ∈_R Z_q* and g is the base point of G, given (g, ag, bg), then compute abg is hard to the group G (Khan et al. (2019)).