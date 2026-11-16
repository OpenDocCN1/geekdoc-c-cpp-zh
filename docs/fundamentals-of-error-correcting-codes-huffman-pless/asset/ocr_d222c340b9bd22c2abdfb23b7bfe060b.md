We now describe the Viterbi Decoding Algorithm in four steps:

+   I. Draw the L truncated trellis for G, replacing the edge labels by the edge weights. Let a denote the zero state.

+   II. Compute S(s, 1) for all states s using the trellis of Step I.

+   III. Repeat the following for i = 2, 3, ..., L + M using the trellis of Step 1. Assuming S(s, i - 1) has been computed for all states s, compute S(s, i) for all s as follows. For each state s' and each edge e from s' to s, form the path P made from P' followed by e where P' \in S(s', i - 1). Include P in S(s, i) if it has smallest weight among all such paths.

+   IV. A nearest neighbor to y is any c_P for P \in S(a, L + M) obtained from the message given by x_P.

Why does this work? Clearly, a nearest neighbor c to y is a c_P obtained from any path P in S(a, L + M) since S(a, L + M) contains all the smallest weight paths from a_0 to a_{L+M} with L + M edges, where a_{L+M} denotes the zero state at time L + M. The only thing we need to confirm is that Steps II and III produce S(a, L + M). This is certainly the case if we show these steps produce S(s, i). Step II by definition produces S(s, 1) for all s. If P \in S(s, i), then P is made up of a path P' ending at time i - 1 in state s' followed by an edge e from s' to s. If P' is not in S(s', i - 1), then there is a path P'' from a_0 ending in state s' at time i - 1 of lower weight than P'. But then the path P'' followed by e ends in state s at time i and has lower weight than P, a contradiction. So Step III correctly determines S(s, i).

# Example 14.25 We illustrate the Viterbi Algorithm by decoding the received vector y = 110111011001011 using the trellis of Figure 14.4. Recall that for the code C_1, two bits are received at each clock cycle; y is listed at the top of Figure 14.4 for convenience. The trellis for Step I is given in Figure 14.5. Again the states are a = 00, b = 01, c = 10, and d = 11; we denote state s at time i by s_i. So the zero state at time 0 is a_0.

For Step II, S(a, 1) = {a_{00}}, S(b, 1) = \emptyset, S(c, 1) = {a_{0c1}}, and S(d, 1) = \emptyset. From this we can compute S(s, 2) using the rules of Step III obtaining S(a, 2) = {a_{0a0a2}}, S(b, 2) = {a_{0c}b_2}, S(c, 2) = {a_{0a}c_2}, and S(d, 2) = {a_{0a}d_2}; notice that the paths listed in S(s, 2)

![](bbox=[0.15, 0.68, 0.9, 0.92])

Figure 14.5 Weights in the truncated trellis for the encoder and received vector of Figure 14.4.