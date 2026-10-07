# Chapter 1

# Algorithms 41

In this problem, we will examine a scheme for adding n binary numbers, m bits long, using a circuit or a parallel architecture. The main parameter of interest in this question is therefore the depth of the circuit or the longest path from the input to the output. This determines the total time taken for computing.

To add two m-bit binary numbers naively, we must wait for the carry bit from i - 1 before we can figure out the th bit of the answer. This leads to a circuit of depth O(m). However carry lookahead circuits (see wikipedia.com) if you want to know more about this can add in O(log m).

+   - Assuming you have lookahead circuits for addition, show how to add n numbers each m bits using a circuit of depth O((log n)(log m)).

+   - When adding three m-bit binary numbers x + y + z, there is a trick we can use to parallelize the process. Instead of carrying out the addition numbers r + s, so that the ith of r and s can be computed independently of the others. Show how this can be done. (Hint: One of the numbers carries bits.)

+   - Show how to use the trick from the previous part to design a circuit of depth O(log n) for multiplying two-bit numbers.

1.31. Consider the problem of computing N! = 1 · 2 · 3 · N.

+   - If N is an n-bit number, how many bits are long in N!, approximately in Θ(n)?

+   - Give an algorithm to compute N! and analyze its running time.

1.32. A positive integer N is a power if it is of the form q^k, where q, k are positive integers and k > 1.

+   - Give an efficient algorithm that takes input a number N and determines whether it is a square, that is, whether it can be written as q^2 for some positive integer q. What is the running time of your algorithm?

+   - Show that if N = q^k (with N, q, and k all positive integers), either k ≤ log N or N = 1.

+   - Give an efficient algorithm for determining whether a positive N is a power. Analyze its running time.

1.33. On page 29, we claimed that about a 1/n fraction of n-bit numbers are prime, on average it is sufficient to draw O(n) random n-bit numbers before hitting a prime. We now justify this rigorously.

Suppose a particular coin has a probability of coming up heads. How many times must you toss it, on average, before it comes heads (Hint: Method 1: start by showing that the correct expression is ∑_{i=1} i(1-p)^{i-1}. Method 2: if E is the average number of coin tosses, show that E = 1 + (1-p)E.