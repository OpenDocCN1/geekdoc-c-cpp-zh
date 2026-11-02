In the final set of sections of this chapter, some sophisticated data structures are introduced. They allow in most cases to organize the simulation data in a way that suits the given problem better and allows for a quicker processing. Here, we present *lists*, *trees*, and *graphs*, together with some sample algorithms to create, modify and use them.

Note, as always in this book, that only few introductory samples (although covering a large fraction of the basic applications) can be given. The important message is that you have to learn to think in terms of data structures, which allows you to aim at looking for efficient implementations. Once you have a little bit of experience, a kind of library of samples in your head, this will become increasingly easier for you. In fact, many more data structures, usually based on the basic data structures presented here, and an overwhelming amount of algorithms acting on these data structures exist. If you want to learn more, and later on you want to do this, you should consult more specialized text books like Refs. [Aho et al. (1974); Cormen et al. (2001); Sedgewick (1990)].

# 6.1 𝒪 notation

For an arbitrary algorithm, to describe the dependence between a suitably chosen measure n of the problem size and the running time T, the 𝒪 notation is used.

# Definition 6.1

Let T, g : ℕ → ℝ be two real-valued functions. We write T(n) = 𝒪(g(n)), if there exist two positive numbers c₁, c₂ > 0 and an integer n₀, such that c₁g(n) ≤ T(n) ≤ c₂g(n) is valid for all n > n₀. We say, T(n) is of order of g(n).

Since constants are ignored when using the 𝒪 notation, one speaks of the *asymptotic* running time or *time complexity*. In theoretical computer science, usually one states an upper bound over all possible inputs of size n, i.e., the *worst-case running time*.

As an example, we look at a function which adds up n numbers: