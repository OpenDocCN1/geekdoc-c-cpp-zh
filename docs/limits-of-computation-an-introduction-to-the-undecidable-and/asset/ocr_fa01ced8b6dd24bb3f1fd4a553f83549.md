# Turing-Completeness

# 5.1 OTHER VERSIONS OF TURING MACHINES

The Turing machine is an extremely robust model of computation. This means that many changes can be made to our basic definition of a Turing machine without changing its power as a computing device. In other words, we can "tweak" a Turing machine in various ways, and still be left with a Turing machine—or more precisely, with something that has exactly the same power to solve problems as the standard Turing machine model.

Definition 5.1

A model of computation is Turing-complete if it can be shown that it is equivalent in power to a Turing machine.

That is, computational model M₁ is equivalent to another computational model M₂ if and only if:

+   1. Any computation performed by M₁ can also be computed by M₂.
2. Any computation performed by M₂ can be computed by M₁.

Thus to prove two models equivalent, one proves 1 and 2. Proving only one of these points does not show equivalency. A supercomputer can accomplish any task that an abacus can, but this does not mean that they are equivalent computing devices. On the other hand, if an inexpensive personal computer can be shown to be able to perform each of the machine