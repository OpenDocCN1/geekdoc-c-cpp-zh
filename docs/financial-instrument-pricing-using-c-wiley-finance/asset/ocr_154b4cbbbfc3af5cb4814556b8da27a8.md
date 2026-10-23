b) Construct the following analogue to Pascal’s triangle. In this case we expand (x + 2)^n instead of (x + 1)^n where n is the row number. We set row 0 to {1} and row 1 to {2}. The triangles are constructed according to the recursive formula:

⎛ n ⎞   ⎛ n−1 ⎞   ⎛ n−1 ⎞
⎝ k ⎠ = 2 ⎝ k−1 ⎠ + ⎝  k  ⎠ ,  1 ≤ k ≤ n.

Verify that the sum of elements of row n is 3^{n−1}.

c) It is possible to compute the binomial distribution from Pascal’s triangle. To this end, let p be the probability of an event occurring and let us assume that p = 1/2. Divide the nth row by 2^n and verify that the triangle becomes the binomial distribution.

2. (Performance Testing)

We examine the code in Section 12.2 with a view to improving its run-time performance. Answer the following questions by writing code to compare the performance of candidate solutions:

+   a) The sum of the elements in row n versus the nth power of 2.
+   b) Computing the binomial coefficients using Boost C++ Math Toolkit versus lookup in Pascal’s triangle.
+   c) Computing the Fibonacci sequence by using elements in Pascal’s triangle versus the formulae in equations (12.3) and (12.4).

You can use the C++11 chrono library or the stopwatch class from Chapter 10 to measure the performance.

3. (Binomial Option Pricing versus Exact Solution)

Use formula (12.5) to compute the call price for the following payoffs:

+   Symmetric power call:

V(S, T) = max((S − K)^p, 0).    (12.43)

+   Asymmetric power call:

V(S, T) = max(S^p − K, 0)    (12.44)

where p is a positive number. Compare the answers with the values produced by the binomial method from Chapter 11.

4. (American Option Pricing)

In this exercise we use the binomial method to price American options. Answer the following questions:

+   a) Compute the price of an American option for large values of the expiration T, for example T in the range [10, 100] years in steps of 10 years. How many time steps are needed in order to achieve convergence in each case?
+   b) For which expiration value T does the binomial method give the same value as the formulae (12.9) and (12.10) for a perpetual American option (if at all)?