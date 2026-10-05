# Appendix B = Solutions to Exercises 545

Suppose the network contains a Hamiltonian cycle that includes the link LAB AB connecting nodes A and B. Now suppose you connect a new node A' to node A and a new node B' to node B. The new network contains a noncyclic Hamiltonian path starting at node A' and ending at node B'.

Conversely, Hamiltonian path must start at node A' and end at node B' (or vice versa in an undirected network). The HAM algorithm finds a path that visits nodes A', A, N₁, N₂, ..., B, B'. Then the path is a Hamiltonian cycle.

The complete algorithm for solving HAMC is as follows:

+   1. For every link LAB connecting nodes A and B:
   - Connect a new node A' to node A, and connect a new node B' to node B.
   - Use the HAM algorithm to see if the modified network contains a Hamiltonian path. If it does, the original network contains a Hamiltonian cycle.
   - Remove the new nodes A' and B' and the links connected to them, and continue with another link.

Figure B-31 shows the idea. You can probably find a Hamiltonian cycle easily enough, but you can't. In the image on the right, the reduction algorithm is considering the link IQR connecting nodes Q and R. It has added node Q', connected to node Q and R', connected to node R. The Hamiltonian algorithm finds the path shown in bold in the modified network on the right. Removing the Q' and R' nodes and their links and adding the IQR to the path gives a Hamiltonian cycle.

![](bbox=[0.235, 0.55, 0.856, 0.874])

Figure B-31: The bold Hamiltonian path in the network on the right corresponds to a Hamiltonian cycle in the network on the left.