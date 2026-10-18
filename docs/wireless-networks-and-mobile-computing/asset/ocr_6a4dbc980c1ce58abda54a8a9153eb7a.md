**Step 4.2.2:** $L_i$ sends a request to the *network leader* $L$ to reassign slots using the new $w_i$.

**Step 5:** If $j$ fails to hear an ACK message from $L_i$ within some timeout interval $T$, it assumes that it was not allocated any time slot by $L_i$. This can occur under the following conditions:

+   1. Case 1: $L_i$ was unable to allocate a slot to $j$.
+   2. Case 2: Some new nodes tried to transmit in the same time slot as $j$ and hence the transmission was garbled due to collision.

On timeout, $j$ uses an exponential backoff algorithm and tries to transmit again. It continues this until it receives an ACK from $L_i$.

# 5.4.6.4  **Mobile Terminal Leaving Cell or Network**

If a mobile terminal $u$ other than the cell leader or the network leader leaves the current cell, no immediate update action is taken. The slot assigned to $u$ may be reclaimed by the cell leader if the cell leader fails to find sufficient unused slots in the cell to satisfy a new incoming mobile terminal in the cell. If a cell leader leaves the network or the cell, according to this protocol no transmission will be heard by the nodes of the corresponding cells in the control slots. When such a situation occurs, a new *cell leader* is elected from the remaining MTs.

If the network leader has left the network, the existing cell leaders elect a new network leader.

# 5.4.6.5  **Handoff Situations**

A *handoff* is required when a mobile terminal $u$ moves from one cell $i$ to another cell $j$. The handoff is treated in the same way as a new MT joining cell $j$ is treated with an additional message sent from $L_j$ to $L_i$ indicating the new cell in which $u