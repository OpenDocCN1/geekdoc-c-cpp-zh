As an example, let us take an intrusion event which lasts for a duration L = 2.8T. Hence, L overlaps either ⌈L/T⌉ = ⌈2.8T/T⌉ = 3 cycles with the probability (1-s = 0.2), or 4 cycles with the probability (s = 0.8).

We can now formalize in higher-order logic the average number of overlapping cycles with an intrusion period L. For this purpose, we proceed by first formally specifying the corresponding random variable which describes the number of overlapping cycles within an intrusion period L. Based on the above description, we model this behavior by a random variable denoted by IT. This random variable can be characterized in higher-order logic by the following predicate intr_distr_rv that accepts five parameters: IT: a random variable that returns an extended real number, p: the probability space, s: the variable specified in Equation (14.1), L: the length of the intrusion period, and Ts: the length of a time slot. Please note that for the sake of simplicity, we take s as a separate variable, although it depends only on L and Ts.

# Definition 14.1

⊢ ∀ IT p s (L: real) (Ts: real) . intr_distr_rv IT p s L Ts = (real_random_variable IT p) ∧ (IMAGE IT (p space p) = {⌈L/Ts⌉, ⌊L/Ts⌋ + 1}) ∧ (distribution p IT {⌊L/Ts⌋} = 1 - s) .

The definition above specifies IT as a real random variable on the probability space p such that the image of IT on (p space p) is in {⌈L/Ts⌉, ⌊L/Ts⌋ + 1}, and its probability distribution over {⌊L/Ts⌋} is (1 - s).

Next, we formally verify the average number of overlapping cycles with an intrusion period L, which is the expectation of the random variable IT:

# Theorem 14.1

⊢ ∀ IT p s L Ts. (0 < Ts) ∧ (0 < L) ∧ (intr_distr_rv IT p s L Ts) ⇒ (expectation p IT = Normal (L/Ts + 1)) .

where the function expectation, used in the above theorem, designates the higher-order-logic formalization of the expectation of a random variable that returns an