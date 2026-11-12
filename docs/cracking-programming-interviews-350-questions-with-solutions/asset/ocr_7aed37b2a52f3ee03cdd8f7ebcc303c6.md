# ## 2.21 Switch and Bulb Problem

# ### Problem Description

Imagine two rooms with no visibility between them. In one room there are n numbered light switches \(s_1, s_2, \ldots, s_n\). In the other room there are n numbered light bulbs \(l_1, l_2, \ldots, l_n\). It is known that each switch turns on and off to exactly one bulb but we do not know anything about the wiring between the switches and the bulbs. Initially we are in the room with the switches. Our job is to tell the exact wiring, i.e. which switch operates which bulb. We are allowed to press any switches and then go to the room with the bulbs and perform an observation. We are not allowed to touch the bulbs : our only source of information is the observation of the bulbs.

The switches are such that their physical appearance does not change when toggled so we have no way of knowing beforehand whether pressing a certain switch leads to turning on or turning off of a bulb. Every switch has, of course, two states only, as any normal light switch.

Describe an algorithm that discovers the wiring with minimum number of observations, i.e. with minimum visits to the room with the bulbs. The algorithm should work iteratively, at each iteration simulating toggling some switches and then simulating an observation by calling some function Observe. The toggling is simulated by writing into a 0-1 array P[1, . . . , n]. Say, P[i] = 1 means \(s_i\) is toggled, and P[i] = 0 means \(s_i\) is not toggled. The result of the observation is written in some 0-1 array L[1, . . . , n]. Say, L[i] = 1 means \(l_i\) is on, and L[i] = 0 means \(l_i\) is off. After every call to Observe, the algorithm temporarily halts, the execution is supposed to be transferred to an outside agent and the algorithm resumes after the outside agent finishes writing into L.

Prove an asymptotic lower bound for the number of observations. Is your algorithm optimal in the asymptotic sense?

# ### Solution

Our algorithm maintains the following data structures:

+   - a 0-1 array A[1, . . . , n] to keep the result of the previous observation,
+   - an array S[1, . . . , n] that refers to the switches. Every element of S is a pointer. Namely, S[i] points to a (doubly) linked list that represents the set of the bulbs, each of which can possibly be connected to \(s_i\) according to currently available information. We call this set of bulbs, the candidate set for \(s_i\).
+   - an array B of positive integers of size 2n. During iteration i, B contains 2i elements that determine a partitioning of S into