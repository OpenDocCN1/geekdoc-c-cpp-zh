# Chapter 31

# Computing Solutions to the Rendering Equation: Theoretical Approaches

# 31.1 Introduction

In this chapter we discuss the theory of solving the rendering equation, concentrating on the mathematics of various approaches and on what kinds of approximations are involved in these approaches, deferring the implementation details to the next chapter. Fortunately, much of the mathematics can be understood by analogy with far simpler problems. When we render, we’re trying to compute values of L, the radiance field, or expressions involving combinations (typically integrals) of many values of L. Thus, the unknown is the whole *function* L. That’s in sharp contrast to the equations like

3x^2 + x = 13 (31.1)

that we see in algebra class, where the unknown, x, is a single number. Nonetheless, such simple equations provide a useful model for the approximations made in the more complicated task of finding L; we discuss these first, and then go on to apply these ideas to rendering.

# 31.2 Approximate Solutions of Equations

There’s no hope of solving the rendering equation exactly for any scene with even a moderate degree of complexity. Instead, we are forced to approximate solutions. There are four common forms of approximation that are routinely used in graphics:

+   - Approximating the equation
+   - Restricting the domain