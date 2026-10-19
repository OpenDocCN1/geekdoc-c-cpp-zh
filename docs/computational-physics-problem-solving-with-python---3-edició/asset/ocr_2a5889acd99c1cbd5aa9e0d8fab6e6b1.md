# 6.2

# Why Matrix Computing?

Physical systems are often modeled by systems of simultaneous equations written in matrix form. As the models are made more realistic, the matrices correspondingly become larger, and it becomes more important to use a good linear algebra library. Computers are unusually good with matrix manipulations because those manipulations typically involve the continued repetition of a small number of simple instructions, and algorithms exist to do this quite efficiently. Further speedup may be achieved by *tuning* the codes to the computer's architecture, as discussed in Chapter 11.

Industrial-strength subroutines for matrix computing are found in well-established scientific libraries. These subroutines are usually an order of magnitude or more faster than the elementary methods found in linear algebra texts,² are usually designed to minimize the round-off error, and are often “robust,” that is, have a high chance of being successful for a broad class of problems. For these reasons, we recommend that you *do not write your own matrix methods* but instead get them from a library. An additional value of library routines is that you can often run the same program either on a desktop machine or on a parallel supercomputer, with matrix routines automatically adapting to the local architecture. The thoughtful reader may be wondering when a matrix is “large” enough to require the use of a library routine. One rule of thumb is “if you have to wait for the answer,” and another rule is if the matrices you are using take up a good fraction of your computer's random-access memory (RAM).

# 6.3

# Classes of Matrix Problems (Math)

It helps to remember that the rules of mathematics apply even to the world's most powerful computers. For example, you *should* encounter problems solving equations if you have more unknowns than equations, or if your equations are not linearly independent. But do not fret. While you cannot obtain a unique solution when there are not enough equations, you may still be able to map out a space of allowable solutions. At the other extreme, if you have more equations than unknowns, you have an *overdetermined* problem, which may not have a unique solution. An overdetermined problem is sometimes treated using data fitting techniques in which a solution to a sufficient set of equations is found, tested on the unused equations, and then improved if needed. Not surprisingly, this technique

2) Although we prize the book, *Numerical Recipes* by Press et al. (1994), and what it has accomplished, we cannot recommend taking subroutines from it. They are neither optimized nor documented for easy, stand-alone use, whereas the subroutine libraries recommended in this chapter are.