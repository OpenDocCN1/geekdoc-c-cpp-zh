![](bbox=[0.302, 0.094, 0.695, 0.244])

# **FIGURE 5.22:** An example of collision resolution by the broadcast algorithm

**Step 6.3:** If no signal is received in the *message slot*, but a collided message was received in some previous round, send an acknowledgment signal in the *N* slot. Increment *round_count* by 1 and go back to Step 6 for the next round.

**Step 6.4:** If a clean signal is received in the *message slot*, send an acknowledgment in *S* slot and change state to *active*. Increment *round_count* by 1 and go back to Step 3 for the next round.

To illustrate the basic ideas of the above algorithm, we consider the following two examples.

**Example 27.** *Consider the network in Figure 5.22, where nodes 111111, 111110, 110110, 110010 and 110001 are the transmitting nodes, and nodes a, b, c, d and e are the receiving nodes. Following Step 4.1, all of the nodes 111111, 111110, 110110, 110010 and 110001 send the message simultaneously. Node d receives the clean message from the node 110110, but nodes a, b, c and e detect a collision. Following the Step 4.2 of the algorithm, nodes 110110 and 110001 are dropped as sender nodes after the testing of the third bit from the most significant bit side and c receives the clean message from node 111110 in the next round. Subsequently, node 111110 is dropped after the sixth bit so that nodes a and b get clean messages from 111111 in the next round. Node 110010 receives an acknowledgment signal in slot N from*