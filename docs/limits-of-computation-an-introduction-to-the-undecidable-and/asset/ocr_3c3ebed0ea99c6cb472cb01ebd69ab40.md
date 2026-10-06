# Turing Machines ■ 63

+   - $q_{reject} \in Q$ is the unique reject state.
- $q_{start} \in Q$ is the specially designated start state.
- $\delta: Q \setminus \{q_{accept}, q_{reject}\} \times \Gamma \to Q \times \Gamma \times \{left, right\}$ is the transition function.

Turing machines are often written as diagrams. For instance, one of the simplest possible Turing machines is shown in Figure 4.1, with $\Sigma = \{0, 1\}$, $\Gamma = \{B, 0, 1\}$, $Q = \{q_{accept}, q_{reject}\}$ and $\delta$ designated by the arrows. Note that since $\delta$ is a function, there are three arrows out of each state (for each element in $\Gamma$), although there are never any allowed out of $q_{accept}$ or $q_{reject}$.

Let's examine each element of this formal definition in greater detail.

# 4.3.1 Input Alphabet

The input $\Sigma$ contains all the symbols that can be used as input to a particular Turing machine. As each decision problem specifies its input differently, this alphabet changes depending upon the purpose of the machine. A machine to decide PRIME (given an integer, would need an alphabet to represent the symbols of its input, whereas one to decide the shortest path would need an alphabet to represent a weighted graph (nodes, edges, distances, etc.).

The Turing machine begins with its input written as a string over $\Sigma$ onto an otherwise empty tape (and the head on the first symbol of the string, if there is one). The unused portion of the tape contains blanks (denoted by the marker B). For various reasons (such as finding left and right ends of the string), we restrict the input by requiring that it not contain this B marker. (Side note: if you want something that naturally contains blanks—such as the text of a story—then first replace every blank in the input with something else, such as underscore or # or $\sim$ or whatever).

$\Sigma$ is an alphabet, and thus by definition it is a finite set.

# 4.3.2 Tape Alphabet

The tape alphabet $\Gamma$ contains all the symbols that could be written onto its tape. As with $\Sigma$, this alphabet varies depending upon the nature of the problem.