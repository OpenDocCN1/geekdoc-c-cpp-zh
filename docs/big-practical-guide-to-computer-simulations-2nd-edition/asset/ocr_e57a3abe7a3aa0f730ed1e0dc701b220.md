# 8.1 Introduction to probability

Here, a short introduction to concepts of probability and randomness is given. The presentation here should be concise concerning the subjects presented in this book. Nevertheless, more details, in particular proofs, examples and exercises, can be found in standard textbooks [Dekking et al (2005); Lefebvre (2006)]. Here often a sloppy mathematical notation is used for brevity, e.g. instead of writing “a function g : X → Y, y = g(x)”, we often write simply “a function g(x)”.

A random experiment is an experiment which is truly random (like radioactive decay or quantum mechanical processes) or at least unpredictable (like tossing a coin or predicting the position of a certain gas atom inside a container which holds a hot dense gas).

# Definition 8.1

The sample space Ω is a set of all possible outcomes of a random experiment.

For the coin example, the sample space is Ω = {head, tail}. Note that a sample space can be in principle infinite, like the possible x positions of an atom in a container. With infinite precision of measurement we have Ω^(x) = [0, Lx], where the container shall be a box with linear extents Lx (Ly, Lz in the other directions, see below).

For a random experiment, one wants to know the probability that certain events occur. Note that for the position of an atom in a box, the probability to find the atom precisely at some x-coordinate x ∈ Ω^(x) is zero if one assumes that measurements result in real numbers with infinite precision. For this reason, one considers probabilities P(A) of subsets A ⊂ Ω (in other words A ∈ 2^Ω, 2^Ω being the power set which is the set of all subsets of Ω). Such a subset is called an event. Therefore P(A) is the probability that the outcome of a random experiment is inside A, i.e. one of the elements of A. More formally:

# Definition 8.2

A probability function P is a function P : 2^Ω ⟶ [0,1] with

P(Ω) = 1  (8.1)

and for each finite or infinite sequence A1, A2, A3, … of mutual disjoint events (Ai ∩ Aj = ∅ for i ≠ j) we have

P(A1 ∪ A2 ∪ A3 ∪ …) = P(A1) + P(A2) + P(A3) + …  (8.2)