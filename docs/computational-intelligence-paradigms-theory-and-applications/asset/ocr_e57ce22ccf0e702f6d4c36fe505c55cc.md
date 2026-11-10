# The Location/Allocation Problem Type

A solution vector for the Location/Allocation problem and the Confor-
mation of a Molecule is a fixed length array of floating-point numbers.
Therefore, the mutation operator simply adds or subtracts a random
amount to one or more of the elements in the solution array. For the Lo-
cation/Allocation problem, the program would first have to ensure that
the new coordinate lies on the map of the problem. If not, a different
random amount should be chosen.

In practice, a maximum step size (MXSTEP) can be set and the fol-
lowing quantity

(1.0-2.0*R)*MXSTEP

is added to an array element, where R is a random number in the range
(0.0,1.0).

In the Location/Allocation problem no maturation operator exists
that is different from a reapplication of the mutation operator. There-
fore, it may be advisable to reduce the size of MXSTEP at the end of
each generation, so that subsequent generation explores good regions of
solution space more carefully.

In the Conformation of a Molecule problem a maturation operator
exists, and it is simply finding a local minimum structure. Therefore
a mutation operator that completely randomizes one or more of the
dihedral angles along with this maturation operator is used, and does
not change the mutation operator throughout the search.

In some of the problem types presented above, it is possible to use more
than one maturation operator and/or use the same maturation operator
more than once. Therefore, an Evolutionary Programming program may
want to include probabilities of using a particular mutation operator or
using it more than once. These probabilities can be used for all offspring
generation and can stay constant or be changed from one generation to
the next. Conversely, as stated in Choosing a Solution's Coding Scheme,
these probabilities can be stored in the solution array of each putative
solution. These particular probabilities can be mutated when they are
transferred to the offspring and then used to generate the offspring's
solution.

The last point is that all standard applications of Evolutionary Pro-
gramming have each member of the Current Population generate a single
offspring which is added to a new population. It is also just as possible to
have each member generate multiple offspring, and only the most-fit
(lowest-COST) offspring would be placed in the new population. This
may significantly increase the computation time of the algorithm, but
may also improve the final results.