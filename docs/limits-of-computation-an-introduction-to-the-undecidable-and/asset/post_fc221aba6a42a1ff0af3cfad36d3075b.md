
## 64 Limits of Computation

Since the input string is initially written onto the tape, $\Gamma$ must include every symbol of $\Sigma$. Similarly, the infinite tape initially has the blank $B$ written in every noninput location, $\Gamma$ must also include this symbol.
That is, we require at least (1) $\Sigma \subseteq \Gamma$ and (2) $B \in \Gamma$, but $B \neq \Sigma$.
With $\Sigma$, the tape alphabet $\Gamma$ must be a finite set.

## 4.3.3 Set of States

The set state $Q$ contains all the control states of the Turing machine. As the Turing machine processes its input, it moves from state to state to indicate different steps of its problem-solving process. These states can be named anything, but by convention we will name them by scripting the letter $q$ (such as $q_0, q_1, q_3$, etc.). Sometimes it makes a Turing machine more readable to give meaningful names, such as $q_{seen-first-one}$ or $q_{even}$.

## 4.3.4 Accept State

The accept state $q_{accept}$ is used by the Turing machine to indicate that its input string is a member of the language in question. The Turing machine does not return this as a result or an accept, nor does it write any symbol onto its tape. Instead, it simply enters the state $q_{accept}$ and stops its operation (halts).

The accept state is unique and every Turing machine must contain $q_{accept}$ in its state set.

## 4.3.5 Reject State

The reject state $q_{reject}$ is in all respects the counterpart of $q_{accept}$. The Turing machine enters this state after it has determined that the input string is not a member of its language, and then stops processing.

As with the accept state, $q_{reject}$ must be a unique element of the machine’s state set. This means $q_{accept}$ and $q_{reject}$ are distinct, as the Turing machine cannot answer the same question with both yes and no answer.

## 4.3.6 Start State

The start state $q_{start}$ is the state from which the Turing machine begins its execution. There is only one start state. It is not necessarily unique like $q_{accept}$ or $q_{reject}$. This means we could allow either $q_{accept}$ or $q_{reject}$ to be the start state, but that leads to a very uninteresting Turing machine: that either accepts or rejects all strings automatically. Thus, although the formal definition requires that a Turing machine have at least two states, we will assume that each machine has at least three.

For simplicity, we will follow the convention that $q_0$ is always the start state. With this assumption, we will not need to designate a special $q_{start}$ for each new machine.

## 4.3.7 Transition Function

The transition function (or delta function) $\delta$ controls the operation of the Turing machine. At each step of its execution, a Turing machine examines both the symbol under its read/write head and its current state. It consults its delta function in order to determine how to proceed. The machine replaces the symbol beneath its read/write head with a new symbol, changes its state to a new state, and moves the read/write head either to the left or to the right one cell, as directed by its transition function.

Since $\delta$ is a function, it must be defined for all possible state and symbol pairs—except out of course, the two states where moves are not allowed. Since the Turing machine stops execution once it has entered either $q_{accept}$ or $q_{reject}$ it need not—in fact, must not—make a move from either of these states. The transition function therefore takes as its domain $Q=\{q_{accept}, q_{reject}\} \times \Gamma$. Its range is quite naturally $Q \times \Gamma \times \{left, right\}$, where left and right are the directions to move the read/write head either left or right, respectively.

Several things should be noted here:

- A Turing machine must write a symbol to its tape at every step. However, it can always replace the current symbol under the read/write head with exactly the same symbol that there was there.
- A Turing machine must go to a new state on each move, but that state can be the same that it was in previously.
- A Turing machine must move its read/write head either to the left or to the right at every step. It cannot stay positioned over the same symbol, although it can certainly move in one direction and then move again in the opposite order to regain its original position.

There are several standard ways to write a machine configuration. The one used here will be to list the state followed by the tape contents, with the current location of the read/write head underlined.

## Example

Let $\Gamma = \{B, 0, 1, 0', 1'\}$, the current state be $q_{273}$, $0011'010'11$ be the nonblank portion of the tape, and the read/write head positioned over the second nonblank symbol.

The configuration is written as $q_{273}$; $0011'010'11$.

An alternate representation (often found in other texts) that is shorter (but perhaps less readable) is to encode the current state directly into the tape contents. This style of representation shows where the read/write head is located by placing the current state immediately in front of the symbol beneath it.

The configuration is sometimes written as $0q_{273}$ $0011'010'11$.

This notation (with the state embedded into the string) has one advantage—it does not require the extra underline to show the location of the head. It is also more economical; the entire configuration is encoded in one string.

If the read/write head is positioned over a blank to the left or the right of the nonblank symbols on the tape, that blank must be shown:

- $\Gamma = \{B, 0, 1, 0', 1'\}$
- The current state be $q_{273}$
- $0011'010'11$ be the nonblank portion of the tape
- read/write head positioned two positions to the left of the nonblank portion of tape

$q_{273}BB0011'010'11$ or $q_{273}BB0011'010'11$ (underline notation) (embedded notation)

One point: It is always assumed that the machine starts in a proper configuration—so there is no need to check that the read/write head is actually over the first symbol, that there are no blanks embedded in the input string, that the symbols on the tape all come from $\Gamma$.

## 4.5 TERMINOLOGY

A few basic definitions are needed to describe the behavior of Turing machine on particular input:

### Definition 4.3
A Turing machine **accepts** an input $w \in \Sigma^*$ iff it enters $q_{accept}$.

### Definition 4.4
A Turing machine **rejects** an input $w \in \Sigma^*$ iff it enters $q_{reject}$.

### Definition 4.5
A Turing machine **halts** an input $w \in \Sigma^*$ iff it enters either $q_{accept}$ or $q_{reject}$.

### Definition 4.6
A Turing machine **loops** an input $w$ iff it **never** enters $q_{accept}$ or $q_{reject}$.

### Definition 4.7
A Turing machine **decides** language $L$ over $\Sigma$ iff for any string $w$ in $\Sigma^*$, $M$ enters $q_{accept}$ if $w$ is in $L$, and enters $q_{reject}$ if $w$ is not in $L$. The language $L$ is **decidable** or **recursive**.

### Definition 4.8
A Turing machine **accepts** (or **recognizes**) language $L$ over $\Sigma$ if for any string $w$ in $\Sigma^*$, $M$ enters $q_{accept}$ if and only if $w$ is in $L$. The language $L$ is **recursively enumerable** (RE) or **semidecidable** or acceptable.

## 4.6 SOME SAMPLE TURING MACHINES

For simple languages, it is easy to describe a Turing machine to decide that language, at least in informal English. But even for simple languages, writing out the entire set of states and the entire transition function can be very tedious—and is something that we rarely do.

### Example $M_1$ (Figures 4.2 and 4.3)

$L_1 = \{w \text{ begins with 0} \mid \Sigma = \{0, 1\}$

$M_1 = (\Sigma, \Gamma, Q, q_{accept}, q_{reject}, q_0, \delta)$, in which:

- $\Sigma = \{0, 1, B\}$
- $\Gamma = \{q_{accept}, q_{reject}, q_0\}$
- $\delta = (q_0, 0) \rightarrow \{q_{accept}, R\}$
