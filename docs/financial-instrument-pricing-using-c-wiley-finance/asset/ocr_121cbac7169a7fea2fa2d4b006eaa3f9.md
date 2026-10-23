# 12.2.6 Summary: Errors, Defects and Faults in Software

We have discussed Pascal’s triangle and its implementation in C++ for a number of reasons. First, it is fun to do; second, it contains precomputed data that can be used as an alternative to computing values at run-time (think about binomial coefficients, for example). Finally, we use it to determine whether our code and logic are correct (Meyer, 1997). By definition, correctness is the ability of software products to perform their exact tasks as defined by their specification.

In the current situation we wish the code in Layers 1 and 2 of the framework to be bug free and it is for this reason that we have chosen Pascal’s triangle as an initial test of the code. Modelling it as a lattice ADT means that we can test it in different ways and check the output. This is particularly important when testing option pricers because if a bug does occur we then wish to pinpoint the source of the bug. To this end, we formalise the fuzzy term ‘software bug’. In particular, we introduce a number of related concepts. An error is a wrong decision that was made during the development of a software product. A defect is a property of a software system that may cause that system to depart from its intended behaviour. A fault is the event of a software system departing from its intended behaviour during one of its executions.

Summarising: ideally, we wish to discover and flag errors as soon as possible, thus ensuring that the software is defect free. In general, faults are due to defects and defects result from errors (Meyer, 1997). In short, we wish to determine if problems are caused by the problem description, in mathematical specification or in code.

# 12.3 OPTION PRICING USING BERNOULLI PATHS

In some cases (for example, non-path-dependent European options) it is possible to compute call and put prices as a sum using Bernoulli paths. For example, for one-factor problems the number of paths to node (n, k) is equal to (n choose k) and the corresponding probability of reaching node (n, k) is (n choose k) p^k (1 − p)^{n−k} where p is the probability that the stock increases by a given fixed amount u. In the case of a general payoff the formulae for call and put options is given by (Haug, 2007):

C = e^{-rT} sum_{j=0}^{n} (n choose j) p^{j} (1 − p)^{n−j} g_1(S_j(T), K)   (12.5)

and:

P = e^{-rT} sum_{j=0}^{n} (n choose j) p^{j} (1 − p)^{n−j} g_2(S_j(T), K),   (12.6)

respectively, where:

+   - p = probability that stock increases at the next time step
+   - n = number of time steps in the binomial process
+   - g1, g2 = generalised payoff functions, for example g1(S, K) = max(S − K, 0), g2(S, K) = max(K − S, 0)