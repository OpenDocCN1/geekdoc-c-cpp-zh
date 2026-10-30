# TABLE 8.6: Bank Branch Data

| Branch | Inputs |  |  | Outputs |  |  |
|---|---|---|---|---|---|---|
|  | Labor Hr. | Space. | Supplies | Loans | Deposits | Checks |
| I | 15 | 20 | 50 | 200 | 15 | 35 |
| II | 14 | 23 | 51 | 220 | 18 | 45 |
| III | 16 | 19 | 51 | 210 | 17 | 20 |
| IV | 13 | 18 | 49 | 199 | 21 | 35 |

(a) Determine the branches' relative efficiencies.

(b) What "best practices" might you suggest to the branches that are less efficient?

# 8.3 Simple Additive Weighting

Simple Additive Weighting (SAW) was developed in the 1950s by Churchman and Ackoff [ChurchmanAckoff1954]; it is the simplest of the MADM methods, yet still one of the most widely used since it is easy to implement. SAW, also called the weighted sum method [Fishburn1967], is a straightforward and easily executed process.

# Methodology

Given a set of n alternatives and a set of m criteria for choosing among the alternatives, SAW creates a function for each alternative rating its overall utility. Each alternative is assessed with regard to every criterion (attribute) giving the matrix M = [m_ij] where m_ij is the assessment of alternative i with respect to criterion j. Each criterion is given a weight w_j; the sum of all weights must equal 1; i.e., Σ_i w_i = 1. If the criteria are equally weighted, then we merely need to sum the alternative values. The overall or composite performance score P_i of the ith alternative with respect to the m criteria is given by

```
P_i = 1/m Σ_{j=1}^m w_j m_{ij}. (8.3)
```

for i = 1, ..., n. Write P→ = [P_i] using matrix/vector notation as

```
P→ = 1/m M w→.
```