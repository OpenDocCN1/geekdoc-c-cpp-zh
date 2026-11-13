# Object Oriented Concepts

In Chapter 1, a review of some important features of C++ have been covered. This chapter starts with Object- oriented Goals and Principles. It proceeds with the discussion about constructors, destructors, overloading of constructors and operators. It also concentrates on other important concepts of C++ such as inheritance, polymorphism, abstract classes, generic programming with function and class templates. Finally it covers recursion.

# 2.1 GOALS AND PRINCIPLES

Object - Oriented design has some goals that are to be achieved in developing a modern software. The object- oriented principles are to be followed in the design to facilitate the goals.

# 2.1.1 OBJECT ORIENTED DESIGN GOALS

The software implementation should achieve the following important design goals:

+   - Robustness
+   - Adaptability
+   - Reusability

# 2.1.1.1 Robustness

Developers want to produce robust software, which gives right output for all the inputs, and the software must be robust, which is capable of handling unexpected inputs.

Robustness of software not only handles unexpected inputs but also yields accurate solutions. For example, if a user tries to store more elements in a data structure than expected then the software should have the capacity to expand this structure to take more elements. This feature is available in C++. The vector class of C++ standard template library defines a dynamically growing array.

Software should also achieve correctness for all its possible inputs including boundary cases such as when an integer value is 0 or 1 or the maximum or minimum possible values. However, robustness and correctness do not come automatically, they must be designed right from the beginning.