# Theorem 13.

*If a node* $u$ *initiates its region computation with the help of range readings from all of its neighbors, the computed region* $R_u$ *of* $u$ *may cause refinements of the successive neighbors through the whole network, but it will never be able to further refine* $R_u$ *of* $u$ *itself.*

# Definition 3.

The stable region of residence of a node $u$ is the minimum region of residence of $u$ which cannot be further improved upon using the current global set of range readings for all node pairs in the network. We denote such a region by $S_u$.

# Theorem 14.

*A node* $u$ *can compute its stable region of residence once it gets the range readings of all possible directly communicating nodes in the network along with the initial region information of all nodes.*

*Proof.* The minimum region of residence of a node $u$ may be refined only when at least one of its neighbors, say $v$, is able to improve its region of residence. This, in turn, depends on whether any neighbor of $v$ excluding $u$ can improve its region of residence, and so on. The process can continue until all the nodes in the network are assessed for improvements in their respective regions of residences. Hence, if $u$ has all the necessary information from all of these updates, $u$ can eventually compute its stable region of residence.

# Theorem 15.

*The computation of the stable regions of residence of all nodes in a network is functionally equivalent to an all-to-all broadcast of the range information of all node pairs in the network (the set* $RR$ *and the set* $Re_{fn}$*).*

*Proof.* To reconstruct the ad hoc network graph centrally, two pieces of information are required: i) the measured ranges of all node pairs and, ii) whether an individual node is a reference node or not. From Theorem 14, we see that if a node possessed the range values of all node pairs in the network (the set $RR$) and the set $Re_{fn}$, it could locally construct the network graph and then compute the stable regions of residence of all nodes. Since the possession of the set $RR$ and the set $Re_{fn}$ by a