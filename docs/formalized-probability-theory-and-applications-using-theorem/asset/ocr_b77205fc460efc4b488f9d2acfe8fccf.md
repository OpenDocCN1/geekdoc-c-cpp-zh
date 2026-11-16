# **Lemma 13.10**
\(\vdash \forall p \text{ X s k C n.}\)
\((1 \le n) \land (1 < k) \land (\text{Normal } 0.9 \le (\text{Cn\_wsn\_first p X k s C n}))\)
\(\Rightarrow k \le 0.003 / (1 - e^{\ln ((1-0.9)/(\text{den}))})\)

Within the deployed WSN, the adjustment of the value of k is done by message flooding which informs all nodes about the new value. Consequently, for our forest fire detection application, increasing k surely saves more energy, a significant increase in k may lead to several sub-networks, which in turns translates to a poor network coverage intensity Cn_wsn.

# **Lemma 13.11**
\(\vdash \forall p \text{ X s C n. } (1 \le n) \Rightarrow\)
\((\text{mono\_decr } (\lambda k.\text{real } (\text{cn\_wsn\_first p X (SUC (SUC k)) s C n})).\)

In addition, we reconfirm the result of Lemma 13.9 using Lemma 13.12, i.e., increasing the number of deployed nodes n gives smaller network coverage and thus a poor performance of the deployed application:

# **Lemma 13.12**
\(\vdash \forall p \text{ X s C n. } (1 \le n) \Rightarrow\)
\((\lim (\lambda k.\text{real } (\text{cn\_wsn\_first p X k s C n})) = 0).\)

The randomized scheduling is thus a dynamic approach, which provides performance adjustments of the deployed WSN application according to the value of k.

The randomness in the nodes scheduling approach leads to sub-networks of different sizes with respect to the number of nodes. Obviously, the ideal case arises when the algorithm makes a fair split of the network so that all the subsets have the same size, i.e., the same number of nodes, which we denote by m. The number of nodes n can be written hence as k * m. In what follows, we closely investigate the asymptotic performance behavior of the k-set randomized algorithm regarding coverage in the case of a uniform split of the nodes.

In particular, we successfully verify, in Lemma 13.13, the upper limit of the network coverage Cn_wsn when n = k * m and k goes to infinity:

# **Lemma 13.13**
\(\vdash \forall p \text{ X s C q. } (0 < q < 1) \land (\forall k \text{ m. sn\_covers p X p q (m * k)}) \Rightarrow\)
\(\lim (\lambda k.\text{real } (\text{Cn\_wsn p X k s C (m*k)})) = 1-e^{-q*(\text{den})}\)