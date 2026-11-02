unambiguously defined for every combination of state and bag of inputs. The bag \(\{1\}\), however, is in \(X_b^\delta\), but \(\delta_0\) is not defined for it. Similarly, the bag \(\{1, 0\}\) is in \(X_b^m\), but \(\delta_M\) is ambiguous about how this modifies the state of \(M\). It is common to have state transition functions that are only partially defined. Make sure, however, that the simulation does not stray into these undefined areas.

The complete machine is built in two stages. The first stage, denoted \(N_1\), contains the second stage, called \(N_2\), and the memory machine \(M\). The second stage contains the two \(O\) machines. It is apparent from the definition of the atomic components and the construction of the network that this machine requires three timesteps to finish one calculation of Equation 3.22. After changing the input, two transient values appear at the output before the third, final value emerges. This mimics the settling time of digital circuits, which require several clock cycles to complete an operation.

The definitions of \(N_1\) and \(N_2\) are clearly and unambiguously illustrated in Figure 3.5. Nonetheless, algebraic definitions are given below to demonstrate their use in a simulation. Note that the sets of influencers have double (bilevel) subscripts; the second part of the subscript indicates whether the set belongs in \(\bar{I}_{N_1}\) or \(\bar{I}_{N_2}\).

The network \(N_2\) is defined by

\[
X_{N_2}=\{x_1,x_2,m\}\times\{0,1\}
\]
\[
Y_{N_2}=\{0,1\}
\]
\[
D_{N_2}=\{O_1,O_2\}
\]
\[
\bar{I}_{N_2}=\{I_{O_1,N_2}, I_{O_2,N_2}, I_{N_2,N_2}\}
\]

where
\[
I_{O_1,N_2}=\{N_2\}
\]
\[
I_{O_2,N_2}=\{N_2,O_1\}
\]
\[
I_{N_2,N_2}=\{O_2\}
\]

\[
Z_{N_2}=\{z_{O_1,O_2},z_{N_2,O_1},z_{O_2,N_2},z_{N_2,O_2}\}
\]

where
\[
z_{O_1,O_2}((b))=\{b\}
\]
\[
z_{N_2,O_1}(\{\ldots,(x_1,b_1),(x_2,b_2),\ldots\})=\{b_1,b_2\}
\]
\[
z_{O_2,N_2}((b))=\{b\}
\]
\[
z_{N_2,O_2}(\{\ldots,(m,b),\ldots\})=\{b\}
\]

Note that the set of input contains labels for the bits; the labels correspond to the name of the edge in Figure 3.5 on which the bit appears. Also note that the coupling functions for \(N_2\) are only partially defined. For example, it is not clear how \(N_2\) handles two \(m\) labeled bits in its input bag. Again, the simulation must avoid these undefined cases.