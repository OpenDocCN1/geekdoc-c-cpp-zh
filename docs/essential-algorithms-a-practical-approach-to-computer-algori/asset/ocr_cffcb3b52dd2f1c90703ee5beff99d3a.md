484 Appendix A Summary of Algorithmic Concepts

# Chapter 14: More Network Algorithms

Topological sorting extends a partial ordering so that you can perform tasks in a feasible order. Topological sorting also lets you determine whether a network contains cycles.

If a map is two-colorable, it is easy to find a two-coloring. Determining whether a map is three-colorable is a very hard problem. You can color any map with at most four colors, but that doesn't mean you will easily find a four-coloring. Often a greedy algorithm finds a coloring without too many extra colors.

You can find maximal flows using a (virtual) residual capacity network. augmenting path shows how to improve the flows. You can use maximal flows to perform work assignment, to find a minimum flow cut, and to determine the number of disjoint paths from a source to a sink.

# Chapter 15: String Algorithms

You can use parenthesis matching to help parse mathematical, logical, or other parenthesized expressions. You can also use parenthesis matching to build parse trees, which you can use to evaluate expressions multiple times or generate data structures.

Regular expressions let a program determine whether a string contains a substring that matches a pattern. The algorithms described for working with regular expressions DFAs and NFAs to process strings. DFAs and NFAs are also useful in other situations where you want to use a set of simple rules to control a virtual computer.

The Boyer-Moore algorithm lets check a string for a particular substring without examining every character in the string. In other situations you may be able to apply the idea that a simple test (checking the end of a target substring) may be to exclude a large area where the target may appear.

The edit distance algorithm determines how similar two strings or files are. In any situation where you define the types of changes that are allowed, you can use a similar approach to calculate how similar two objects are.

# Chapter 16: Cryptography

For most programmers, these algorithms have only academic or entertainment value. They demonstrate a couple of useful techniques, however. 

Transposition ciphers—Even though some of these algorithms treat text as it were written into an array, you don't necessarily need to build the array if you can use simple calculations to figure out where a piece of text would be in the array.

One-time pads provide provably strong encryption. Their disadvantage is that you need to safely give the same pad to the sender and receiver.

Block ciphers break a message into blocks and encrypt the blocks separately. Many of them also apply relatively simple operations to blocks repeatedly to increase obfuscation.