# Limits of Computation

all—and thus, a TM never accepts any input. If one also takes the convention that an undefined value goes to $q_{reject}$, then this is a TM that rejects all inputs.

# 5.7 UNIVERSAL TURING MACHINE

In designing Turing machines for problems, there is a new machine for each new problem. This is not really necessary. It is easy to design a universal Turing machine (UTM). The input to the UTM is: (1) an encoded Turing machine M and (2) the encoded input I to M. Then, the UTM emulates M on I, and can announce whether M accepts or rejects I, or what else it may do.

+   The input to the UTM is a string of 0s and 1s, the encoding of M and I as outlined in the section above.

One way to build M is as a three-tape Turing machine:

+   Tape 1: Input tape, holds M and I (encoded).

+   Tape 2: Working tape, holds the input to M, in encoded form.

+   Tape 3: Current state (encoded, a sequence of zeros).

Other tapes can be added if convenient; for example, an extra working tape might be useful in shifting parts of tape 2 to the right or to left.

The UTM begins its operation by (1) copying the encoding of the input onto tape 2, and (2) copying 0 (for $q_{start}$) onto tape 3.

Now, it looks at the 0s on tape 2 for the current input symbol. It must find the place in the encoding of M that matches this symbol and the state (from tape 3). If it finds a match, it must change tape 2 left or right as needed to add more of 0s (for $q_{reject}$) on tape 3 and halts and rejects (entering its own $Q_{UTM-reject}$). Similarly, if it finds 00 for $q_{accept}$ it goes to its own $Q_{UTM-accept}$. A simple encoded Turing machine ($M_i$) and a demonstration of one step of the universal machine is shown (Figures 5.13 and 5.14).

The advantage of the universal Turing machine is that it is a machine with a simple standard alphabet ({0, 1}) that can emulate every Turing machine. Its only task is to read a Turing machine (so the machine that it reads is like a program for the UTM), and the input to that TM or program, run the TM/program on its input.