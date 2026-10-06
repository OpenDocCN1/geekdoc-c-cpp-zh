# Classes NP and NP-Complete ■ 183

c. Part a

d. Part b

(Describe the encoding scheme you use.)

Describe an encoding scheme and write the encodings over Σ = {0, 1}.

e. Part a

f. Part b

+   15. In a Boolean expression in CNF, with n = number of Boolean variables, m = number of clauses, and |E| = total length of expression, find:
    a. The upper bound for m in terms of n (assume no duplicate clauses).
    b. The upper bound for n in terms of m, assuming that there are no duplicate variables in a clause—so that in a clause for a variable i, either xi is missing or one of xi or -xi, is present).
    c. Upper bound for |E| in terms of n and m.

+   16. Decision problem: Large enough factor: Given integers n and k, does n have a factor (besides n itself) that is greater than or equal to k?
    a. Give yes and no instances.
    b. Show how to use a polynomial time algorithm for this problem (if it exists) to construct a polynomial algorithm to find a factor of n. (Hint: Binary search).
    c. From b, show how to construct a polynomial algorithm for factoring n.

Hint (for Exercise 8): To quickly add together the factors of a number, note that if we have the prime factorization

n = 2ᵃ * 3ᵇ * 5ᶜᶜ * ...

then the sum of all factors (including n) is

(1 + 2 + ... + 2ᵃ) * (1 + 3 + ... + 3ᵇ) * (1 + 5 + ... + 5ᶜ) * ...