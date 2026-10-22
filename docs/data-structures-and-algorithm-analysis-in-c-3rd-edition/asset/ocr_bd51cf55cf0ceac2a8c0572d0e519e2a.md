Compare the proof of Theorem 2.7 with that of Theorem 2.5. For Theorem 2.5, we took a collection of stamps of size n − 1 (which, by the induction hypothesis, must have the desired property) and from that “built” a collection of size n that has the desired property. We therefore proved the existence of some collection of stamps of size n with the desired property.

For Theorem 2.7 we must prove that any collection of n lines has the desired property. Thus, our strategy is to take an arbitrary collection of n lines, and “reduce” it so that we have a set of lines that must have the desired property because it matches the induction hypothesis. From there, we merely need to show that reversing the original reduction process preserves the desired property.

In contrast, consider what is required if we attempt to “build” from a set of lines of size n − 1 to one of size n. We would have great difficulty justifying that all possible collections of n lines are covered by our building process. By reducing from an arbitrary collection of n lines to something less, we avoid this problem.

This section’s final example shows how induction can be used to prove that a recursive function produces the correct result.

# Example 2.17 We would like to prove that function fact does indeed compute the factorial function. There are two distinct steps to such a proof. The first is to prove that the function always terminates. The second is to prove that the function returns the correct value.

# Theorem 2.8 Function fact will terminate for any value of n.

Proof: For the base case, we observe that fact will terminate directly whenever n ≤ 0. The induction hypothesis is that fact will terminate for n − 1. For n, we have two possibilities. One possibility is that n ≥ 12. In that case, fact will terminate directly because it will fail its assertion test. Otherwise, fact will make a recursive call to fact (n-1). By the induction hypothesis, fact (n-1) must terminate.

# Theorem 2.9 Function fact does compute the factorial function for any value in the range 0 to 12.

Proof: To prove the base case, observe that when n = 0 or n = 1, fact (n) returns the correct value of 1. The induction hypothesis is that fact (n-1) returns the correct value of (n − 1)!. For any value n within the legal range, fact (n) returns n * fact (n-1). By the induction hypothesis, fact (n-1) = (n − 1)!, and because n * (n − 1)! = n!, we have proved that fact (n) produces the correct result.

We can use a similar process to prove many recursive programs correct. The general form is to show that the base cases perform correctly, and then to use the induction hypothesis to show that the recursive step also produces the correct result.