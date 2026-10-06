
- d. The number of b's is equal to the number of a's.
- e. Of the form $a^N$, where $N$ is a composite (nonprime) number.
- f. Have the form $www$ (such as aaabaabaaaab).

(Note: All of these can be done on a standard Turing machine. Some problems, such as (e) and (f), take careful construction of a complex machine.)

- 5. Given the diagrams below (Figure 4.12), answer:
    - a. Does the diagram describe a legal Turing machine?
    - b. Trace the operation of the Turing machine on all strings of length 2.
    - c. Describe the language accepted by this Turing machine.

## Limits of Computation

![](img/d80067a1fcf4f931f840f447fc7d1650_99_0.png)

FIGURE 4.12 Problems: (a) Diagram for possible machine $M_{10}$- (b) Diagram for possible machine $M_{11}$

![](img/d80067a1fcf4f931f840f447fc7d1650_100_0.png)

FIGURE 4.12 (Continued) Problems: (c) Diagram for possible machine $M_{12}$. (d) Diagram for possible machine $M_{13}$.

## Turing-Completeness

## 5.1 OTHER VERSIONS OF TURING MACHINES

The Turing machine is an extremely robust model of computation. This means that many changes can be made to our basic definition of a Turing machine without changing its power as a computing device. In other words, we can "tweak" a Turing machine in various ways, and still be left with a Turing machine—or more precisely, with something that has exactly the same power to solve problems as the standard Turing machine model.

**Definition 5.1**

A model of computation is Turing-complete if it can be shown that it is equivalent in power to a Turing machine.

That is, computational model $M_1$ is equivalent to another computational model $M_2$ if and only if:

- 1. Any computation performed by $M_1$ can also be computed by $M_2$.
- 2. Any computation performed by $M_2$ can be computed by $M_1$.

Thus to prove two models equivalent, one proves 1 and 2. Proving only one of these points does not show equivalency. A supercomputer can accomplish any task that an abacus can, but this does not mean that they are equivalent computing devices. On the other hand, if an inexpensive personal computer can be shown to be able to perform each of the machine instructions for a supercomputer, then it can emulate any program on the supercomputer—perhaps taking much longer, but time and efficiency are not part of the definition of equivalent computing power.

Several different changes are proposed to the Turing machine model below. All of these modifications are shown to be Turing-complete.

### 5.1.1 Semi-Infinite Tape

Many authors use a model of a Turing machine that has a semi-infinite (or one-way infinite) tape—the tape has a left end, but no right end. The machine starts in Start, with the input placed on the leftmost portion of its tape and with the read/write head positioned on the first tape location.

The disadvantage of this model is that one must have some convention to deal with a transition function that acts for a move when the head is on the left end of the tape. Various conventions work—that the head falls off the left end of the tape and enters a hanging state from which it can never recover, a move when the left is implemented as remaining on the left so that the head does not move, or other possibilities. For various formal definitions of semi-infinite Turing machines, see Hopcroft et al. (2007), Lewis and Papadimitriou (1997), Sipser (2006), and others.

Having a left end to the tape also makes awkward to return to the left end of the input. Finding the right end is easy—simply move to the first blank, and then move to the one position. Finding the end is similarly easy if the tape is two-way infinite; there is always a blank to the left of the input, but it is much more difficult with a semi-infinite tape.

The two-way tape seems to allow simpler constructions and simpler combinations of moves. However, it does not add additional power.

### Theorem 5.2

Any standard Turing machine $M$ with two-way infinite tape can be emulated by a Turing machine $M'$ with semi-infinite tape, and vice versa. Thus, the semi-infinite tape model of a Turing machine is Turing-complete.

### **Proof**

There are many ways to put a two-way infinite tape onto a semi-infinite tape. One way is to make a machine $M'$ by using a special symbol of the tape alphabet—perhaps, called a turnstile—in cell 1 as an end marker. The even positions then hold the right side of the two-way infinite tape; the other odd positions hold anything that would be written on the left.

For example, a standard two-way infinite tape Turing machine begin with tape contents:

```
... BBB��₁σ₂�₃ ... σₙ, BBB ...
```

It is natural to take the start of the input as the first character after the end marker—in essence, “folding” the two-way infinite tape there. But an other position on the tape would also work.
If one takes the natural beginning, initialize the tape of $M'$ with

```
—ↄ,B₀σ₀B ... Bₙ,BB ...
```

Emulating one of $M$ will be slightly different, depending on whether the head is to the left or the right of the starting position. The machine must have states for being on the right side of $M$, and another set of states that it should have been on the left side.

For example, state $q_{26}$ in the original Turing machine would result in $q_{2,right}$ and $q_{6,right}$. Figure 5.1 shows how one moves on a tape with input 1101101 might look like. The blanks are copies from the left side of the two-way infinite tape: the 1101101BBBB ... is a copy of the right side.

If one is working on what would have been the right side of the two-way infinite tape, a move on the right is done by moving two “new" cells; likewise a move left is a move by two.
For example, if the usual Turing machine has $\delta(q_{26}, 1) = q_{53}$ (that is, write 1, go right), then semi-infinite machine will need to (1) write 1, (2) move right, and (3) go to state $q_{53}$. $\delta(q_{26}, \sigma) \rightarrow q_{53,right}, 1, R$ (for any $\sigma$).

Turing-Completeness ■ 83

## 84 Limits of Computation

| | | | | | | |
|---|---|---|---|---|---|---|
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | | |
 | | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |

 | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
| | | | | | | |
## 5.1.2 Stay Option

A Turing machine with a stay option is an extension of the usual machine:

**Definition 5.3**

A stay option Turing machine $M = (\Sigma, \Gamma, Q, q_{accept}, q_{reject}, q_{start}, \delta)$ is defined as an ordinary Turing machine except that the delta function has the option of remaining on the same cell.

- It is convenient to have multiple tapes. By convention, a k-tape Turing machine starts with its input on the first tape, and the first head on the first character of the input. The other tapes all begin as blank tapes.

A move of this Turing machine now takes a state, a k-tuple of characters under the k-heads. It writes a character on each of the k-tapes, and moves each of the heads left or right. One can choose any k that is convenient for the problem—often three tapes allow enough flexibility. A sample three-tape Turing machine with input $\sigma_1\sigma_2\sigma_3\sigma_4\sigma_5\sigma_6\dots$ is shown in Figure 5.2.

![](img/d80067a1fcf4f931f840f447fc7d1650_106_0.png)

FIGURE 5.2 Partial picture of a three-tape Turing machine.
