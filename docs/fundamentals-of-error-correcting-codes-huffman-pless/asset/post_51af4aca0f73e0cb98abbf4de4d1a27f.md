
parity check matrix $H$ for $\mathcal{C}$. We further assume that $\mathcal{T}$ has no cycles.$^6$ As in Section 15.2, for concreteness we assume that the demodulation scheme used for the received vector is 8-level quantization. Therefore suppose that $\mathbf{c} = c_1 c_2 \cdots c_n$ is the transmitted codeword, and $\mathbf{y} = y_1 y_2 \cdots y_n$ is received with $y_i \in \{0, \dots, 14\}$. As with the Soft Decision Viterbi Algorithm, our goal is to perform maximum likelihood decoding and find the codeword $\mathbf{c}$ that maximizes prob($\mathbf{y} \mid \mathbf{c}$). We assume the channel is memoryless and hence

```
prob(y | c) = \prod_{i=1}^n prob(y_i | c_i).
```

As in Section 15.2, take the logarithm turning the product into a sum and then rescale and shift the probabilities so that the value to maximize is

```
\sum_{i=1}^n \mu(y_i, c_i).
```

where the maximum is over all codewords $\mathbf{c} = c_1 c_2 \cdots c_n$, analogous to (15.15).

The Tanner graph $\mathcal{T}$ has no cycles and hence is a tree or forest. For simplicity, assume $\mathcal{T}$ is a tree; if $\mathcal{T}$ is a forest, carry out the algorithm on each tree in $\mathcal{T}$ separately. All the leaves are variable nodes provided no row of $H$ has weight 1, which we also assume. At the end of the algorithm, messages will have been passed along all edges once in each direction. Each message is a pair of nonnegative integers. The first element in the pair is associated with the bit 0, and the second element in the pair is associated with the bit 1. Together the pair will represent relative probabilities of the occurrence of bit 0 or bit 1. The *Message Passing Decoding Algorithm* is as follows:

- I. To initialize, assign the pair $(\mu(y_i, 0), \mu(y_i, 1))$ to the $i$th variable node. No assignment is made to the check nodes. Also for every leaf, the same pair is to be the message, leaving that leaf node directed toward the attached check node.

- II. To find a message along an edge $e$ leaving a check node $h$, assume all messages directed toward $h$, except possibly along $e$, have been determined. Suppose the messages entering $h$ except along $e$ are

```
(a_{i_1}, b_{i_1}), (a_{i_2}, b_{i_2}), \dots, (a_{i_l}, b_{i_l}).
```

Consider all sums

```
\sum_{j=1}^l x_{i_j}, \quad (15.24)
```

where $x_{i_j}$ is one of $a_{i_j}$ or $b_{i_j}$. The message along $e$ leaving $h$ is $(m_0, m_1)$, where $m_0$ is the maximum of all such sums with an even number of $b_{i_j}$s and $m_1$ is the maximum of all such sums with an odd number of $b_{i_j}$s.

- III. To find a message along an edge $e$ leaving a variable node $v$, assume all messages directed toward $v$, except possibly along $e$, have been determined. The message leaving $v$ along $e$ toward a check node is assigned the pair at $v$ (from Step I) added to the sum of all the incoming messages to $e$ except along $e$.

- IV. Once all messages in both directions along every edge have been determined by repetition of II and III, a new pair $(p_0, p_1)$ is computed for every variable node $v$. This pair is the sum of the two messages along any edge attached to $v$.

- V. Decode the received vector as follows. For the $i$th variable node, let $c_i = 0$ if $p_0 > p_1$ and $c_i = 1$ if $p_1 > p_0$.

The rationale for the message passed in II is that the summation in (15.24) is associated with bit 0, respectively bit 1, if there are an even, respectively odd, number of $b_{i_j}$’s involved, as these sums correspond to adding an even, respectively odd, number of “probabilities” associated to 1s. We do not prove the validity of the algorithm; more discussion of the algorithm is found in [91] and the references therein. Note again how closely related this algorithm is to the Soft decision Viterbi Algorithm.

Example 15.5.2 Suppose that $y = 120010110110101$ is the received vector when a codeword is transmitted using the [7, 4, 2] code $\mathcal{C}$ of Example 15.5.1. Even though this code has minimum distance 2, implying the code cannot correct any errors using nearest neighbor decoding, we can still decode using soft decision decoding to find the maximum likely codeword. We will use the Tanner graph for $\mathcal{C}$ in Figure 15.8 determined by the parity check matrix $H$ given in Example 15.5.1. We will also use the values of $\mu(\gamma, c)$ given in Example 15.2.1. The messages obtained using the Message Passing Decoding Algorithm are given in Figure 15.9. Step 1 of the algorithm is carried out at time 1 using the table of values for $\mu(\gamma, c)$ in Example 15.2.1 applied to the received vector. At time 2, we pass messages from the three check nodes toward $y_1$ using II. For example, the message $(5, 8)$ directed toward $y_1$ is determined from the messages $(0, 5)$ and $(3, 0)$ entering the check node from $y_4$ and $y_5$ as follows:

```
(5, 8) = (max{0 + 3, 5 + 0}, max{0 + 0, 5 + 3}).
```

Similarly, the message $(6, 5)$ directed toward $y_1$ is

```
(6, 5) = (max{1 + 5, 0 + 0}, max{0 + 5, 1 + 0}).
```

After time 2, every edge has one message along it in some direction. At time 3, messages are sent along the three edges leaving $y_1$ using III. For example, the message $(14, 17)$ is the sum of the node pair $(0, 3)$ plus the sum $(8, 9) + (6, 5)$. At time 4, messages are sent to all leaf nodes using II. For instance, the message $(17, 20)$ sent to $y_4$ uses the edges $(3, 0)$ and $(14, 17)$ yielding

```
(17, 20) = (max{3 + 14, 0 + 17}, max{3 + 17, 0 + 14}).
```

After time 4, all edges have messages in each direction. By adding the edges attached to each variable node, Step IV gives:

| | y1 | y2 | y3 | y4 | y5 | y6 | y7 |
|---|---|---|---|---|---|---|---|
| (p0, p1) | (19, 25) | (25, 21) | (21, 25) | (17, 25) | (25, 19) | (19, 25) | (25, 16) |

Note that the pair for y1 is obtained using any of the three edges attached to y1,

![](img/0af7e79235839ec0eb8bcf8d229f37d4_615_0.png)

Figure 15.9 Message passing on the Tanner graph of Figure 15.8.

namely, $(19, 25) = (14, 17) + (5, 8) = (11, 16) + (8, 9) = (13, 20) + (6, 5)$. We decode $y$ as $c = 1011010$ from Step V. Notice that for our received vector $y$ and this codeword $c$, $\sum_{i=1}^7 \mu(y_i, c_i) = 3 + 5 + 0 + 3 + 1 + 8 = 25$, which is the largest component of each of the seven $(p_0, p_1)$s.

Exercise 856 Verify the computations in Example 15.5.2.

Exercise 857 Let $\mathcal{C}$ be the code in Example 15.5.1 with Tanner graph in Figure 15.8. Use the Message Passing Decoding Algorithm to decode the following received vectors; use the values of $\mu(y, c)$ given in Example 15.2.1. (a) $y = 0,1,0,1,0,0,1,0,1,13$, (b) $y = 1,0,0,0,1,0,0,4,12$.

Exercise 858 Construct the Tanner graph for the [10, 6, 2] binary code with parity check matrix

$H = [ 1\ 1\ 1\ 0\ 1\ 0\ 0\ 0\ 0\ 0\ 1\ 0\ 0\ 0\ 1\ 1\ 0\ 0\ 0\ 0\ 0\ 0\ 0\ 0\ 1\ 0\ 1\ 1\ 0\ 0\ 0\ 0\ 1\ 0\ 0\ 0\ 0\ 0\ 1\ 1 ]$

Then use the Message Passing Decoding Algorithm to decode $y = 1,0,2,15,0,1,11,2,15,14,0,13,1$.

Use the values of $\mu(y, c)$ given in Example 15.2.1.

## 15.6 Low density parity check codes

In the previous section we introduced our first example of iterative decoding through message passing. In the mid 1990s, iterative decoding became a significant technique for the decoding of turbo codes. Iterative decoding was introduced by Elias in 1954 [77]. Iterative decoding reappeared with the work of R. G. Gallager on low density parity check codes in 1963 but since then seems to have been largely neglected, with only a few exceptions, until researchers realized that the decoding of turbo codes was closely related to Gallager's techniques. In this section we will introduce low density parity check codes and examine Gallager's two versions of iterative decoding. Our presentation relies heavily on [94, 95, 211]. For the interested reader, the use of message passing in low density parity check code is described in [295].

In short, a binary low density parity check code is a code having a parity check matrix with relatively few 1s which are dispersed with a certain regularity in the matrix. An [n, k] binary linear code $\mathcal{C}$ is a low density parity check (LDPC) code provided it has an $m \times n$ parity check matrix $H$ where every column has fixed weight $c$ and every row of $H$ has fixed weight $r$.? This type of code will be denoted an $(n, c, r)$ LDPC code. Note that such a matrix may not have independent rows so is technically not a parity check matrix in the sense we have used in this text. However, $H$ can be row reduced and the zero rows removed to form a parity check matrix for $\mathcal{C}$ with independent rows. Thus the dimension of $\mathcal{C}$ is at least $n - m$. Counting the number of 1s in $H$ by both rows and columns gives the relationship $nc = mr$ among the parameters. Generally, we want $r$ and $c$ to be relatively small compared to $n$ and thus the density of 1s in $H$ is low.

7 A natural generalization for LDPC codes is to allow the row weights and column weights of $H$ to vary, in some controlled manner. The resulting codes are sometimes termed 'irregular' LDPC codes.
