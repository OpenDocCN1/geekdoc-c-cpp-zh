If the evidence, E_i, are all conditionally independent, then the joint probability becomes the product of the individual probabilities. This follows from the Generalized Multiplicative Law. As an example, for two pieces of evidence:

P(E_1 \cap E_2 \mid e) = \frac{P(E_1 \cap E_2 \cap e)}{P(e)}
= \frac{P(E_2 \mid E_1 \cap e) P(E_1 \mid e) P(e)}{P(e)}

Using the assumption of independence,

P(E_2 \mid e) = P(E_2 \mid E_1 \cap e)

because the evidence E_1 does not contribute any knowledge toward E_2. So:

P(E_2 \cap E_1 \mid e) = P(E_2 \mid e) P(E_1 \mid e)

and in general:

P(E_1 \cap E_2 \cap ... \cap E_n \mid e) = \prod_{i=1}^{n} P(E_i \mid e)

Although this formula is correct in a theoretical sense, there are two difficulties in applying it to real-world problems. First, the individual P(E_i \mid e) are usually not independent in the real world. Second, the multiplication of many factors based on the first assumption leads to a product that is generally far too small for P(E \mid e).

An approximate solution to this problem is use of fuzzy logic to calculate P(E \mid e) as follows:

P(E \mid e) = min [ P(E_i \mid e) ]

where the min function returns the minimum value of all the P(E_i \mid e). In the PROSPECTOR system, this formula was satisfactory. Once P(E \mid e) is determined, it can be used with the piecewise linear formula for P(H \mid e).

The main problem with the fuzzy logic formula is that it makes P(E \mid e) insensitive to any P(E_i \mid e) except the minimum. This means that even if all the other probabilities increase and the minimum remains the same, no change in P(E \mid e) will be affected. That is, the minimum P(E_i \mid e) blocks other probability changes from propagating through the inference chain. An advantage of the fuzzy logic formula is that it is computationally simple.