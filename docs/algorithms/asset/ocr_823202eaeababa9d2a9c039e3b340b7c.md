# Exercises

one going down (the 1-edge). To get to $A(\omega^k)$ from any input node, simply follow the edges specified in the bit representation of $k$, starting from the rightmost bit.
Can you similarly specify the path in the reverse direction?)

+   4. On the path between $a_j$ and $A(\omega^k)$, the labels add up to $jk mod 8$.

Since $\omega = 1$, this means the contribution of input $a_j$ to output $A(\omega^k)$ is $a_{j\omega^k}$, and therefore the circuit correctly computes the values of polynomial $A(x)$.

+   5. And finally, notice that the FFT circuit is a natural for parallel computation and direct implementation in hardware.

# The slow spread of a fast algorithm

Tukey was not keen to write a paper on the subject, Cooley took the initiative. This is one of the most famous and most cited scientific papers published in 1965, co-authored by Cooley and Tukey. The reason Tukey was reluctant to publish the FFT was not secretness or pursuit of profit via patents. He felt that this was a simple observation that was probably already known. This was typical of the period: back then (and for some time) algorithms were considered second-class mathematical objects, devoid of depth and length, and unworthy of serious attention.

But Tukey was right about one thing: it was later discovered that British engineers used the FFT for calculations during the late 1930s.—and to end this chapter with the same mathematician who started it—a paper by Gauss in the early 1800s (on what else?) interpolation essentially contained the same idea in it! Gauss's paper had remained a secret for so long because it was protected by an old-fashioned cryptographic technique: like most scientific papers of its era, it was written in Latin.

# Exercises

+   2.1. Use the divide-and-conquer integer multiplication algorithm to multiply the two binary integers 100110111 and 10111010.

+   2.2. Show that for any positive integers $n$ and any base $b$, there must be some power of $b$ lying in the range $[n, bn]$.