# Chapter 26

# Adaptive Finite Elements in
Three Spatial Dimensions

In this chapter, the present object-oriented framework is used to implement the three-dimensional finite-element mesh. Furthermore, this framework is also used to implement the adaptive-refinement algorithm in a short and elegant code.

# 26.1  Why Is Object-Oriented Programming Necessary?

Object-oriented programming (OOP) is particularly useful to reduce the amount of code required in advanced applications. Roughly speaking, with no OOP, the code size may grow exponentially as the problem becomes more and more complicated. With OOP, on the other hand, it grows only linearly.

Indeed, suppose that we already have a code that works well for some elementary case (for example, a code that solves a two-dimensional application), and we want to generalize it to apply to a yet more complicated case as well (for example, to a three-dimensional application). If our original code were not an object-oriented code, then we would have to modify each and every function in it to apply to the more advanced case as well (Figure 26.1). This would no doubt require more code (as well as more programming work) in each function, increasing the total amount of code (as well as the total programming time) by a constant factor greater than 1.

Fortunately, our code is an object-oriented code. Therefore, all that is needed to do is to implement well the new objects required in the advanced application (such as the tetrahedron object in the three-dimensional mesh), along with the functions associated with them. After all, the original algorithm implemented in the original code should also work well with these objects, with at most some minor adjustments.

Thus, with OOP, one only needs to add to the original code a limited amount of new code to implement the new objects required in the more general (and complicated) case. Thus, the total amount of code (as well as the total amount of programming work) increases only linearly as the problem is written in more and more general terms to apply to more and more difficult cases (Figure 26.2).