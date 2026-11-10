# 13.8.3  Illustrations Based on Schema Theorem

# Illustration 1:

+   1. Consider the following two schema
+   
+   `* * * 1 1 1` and `1 * * * * * 1 *`

+   (a) What is the defining length? What is the order?
+   
+   (b) Let $p_m = 0.001$ (probability of simple mutation). What is the probability of survival of each schema?
+   
+   (c) Let $p_c = 0.85$ (probability of cross-over). Estimate the probability of survival of each schema?

**Solution:**

(a). Order:

$o(S_1)=3;\quad o(S_2)=2;$

Defining Length:

$\delta(S_1)=2;\quad \delta(S_2)=6;$

(b). Given: $p_m=0.001$

Mutation:

$$
p_m(S)=(1-p_m)^{o(S)}
$$

$$
p_m(S_1)=(1-p_m)^{o(S_1)}=(1-0.001)^3=99.7\%
$$

$$
p_m(S_2)=(1-p_m)^{o(S_2)}=(1-0.001)^2=99.8\%
$$

(c). Given: $p_c=0.85$;

We know that $m=8$;

Crossover:

$$
p_c(S)\geq 1-p_c\frac{\delta(S)}{m-1}
$$

$$
p_c(S_1)=1-p_c\frac{\delta(S_1)}{m-1}=1-0.85\frac{2}{8-1}=76\%
$$

$$
p_c(S_2)=1-p_c\frac{\delta(S_2)}{m-1}=1-0.85\frac{6}{8-1}=27\%
$$

# Illustration 2:

A population contains the following strings and fitness values at generation 0 (Table 13.1):

Calculate the expected number of strings covered by the schema `1 * * *` in generation 1 if $p_m=0.01$ and $p_c=1.0$.