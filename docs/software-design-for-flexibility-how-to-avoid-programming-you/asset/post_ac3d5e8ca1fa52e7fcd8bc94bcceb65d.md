
# Exercise 7.6: Multiple-dwelling puzzle

It is easy to formulate the multiple-dwelling problem for the amb evaluator of chapter 5.4. In fact it is easier than for the propagator system, because we can think and write in terms of expressions. Indeed, you will be able to write constraints like the fact that Fletcher and Cooper do not live on adjacent floors as something like:

```
(require (not (= (abs - fletcher cooper)) 1)))
```

rather than

```
(c:+ cooper f-c fletcher)
(c:abs f-c af-c)
(p:= one af-c fc)
```

when cells like f-c, af-c, and fc must be declared and one fc are initialized. This is because the propagation system is a general wiring-diagram system rather than an expression system.

- a. Formulate and solve the multiple-dwelling problem using the amb evaluator of section 5.4. Instrument the system to determine the number of failures. How many failures does it take?

- b. Write a small compiler that convert to constraints written as expressions into propagator diagram fragments. You will find that this is very easy. We really made a first stab at this in exercise 7.1 on page 340. But here we want to make a translator for code from section 5.4 to a propagator target. Demonstrate that your compilation gets the correct answer.

- c. How many failures are needed to solve the problem with the propagator diagram that you compiled into? If it takes more than 200 failures you compiled into very bad code!

# Exercise 7.7: Card game puzzle revisited

Redo exercise 5.17 using propagators.

# Exercise 7.8: Type inference

In section 4.4.2 we built a type-inference engine as an example of the application of unification matching. In this exercise (which is really a substantial project) we implement type inference taking advantage of propagation.

- a. Given a Scheme program, construct a propagation network with a cell for every locus that is useful to type. Each cell will be the repository of the type information that will be accumulated about the type information at that locus in the program. Construct propagators that connect the cells and impose the type constraints implied by the program structure. Use unification match as the cell-merge operation. The unification may yield a contradiction if the program cannot be typed.

- b. There may be some cells of a program where a type is not sufficiently constrained by the types of the neighboring cells. However, propagation can be stimulated by dropping a general type variable into such a cell and allowing that variable to accumulate constraints by propagation. This is called “plunking.” Try it.

- c. In hard cases a type inference may require making guesses (using hypotheticals) and backtracking on discovery of contradictions. Show cases where this is necessary.

- d. Tracking of properties and reasons enables the construction of informative error comments, but to do this you must associate each program locus with its cell so that things are learned by propagation can be related to the program. You may use any kind of “sticky note” you like to associate the locus bidirectionally with the cell. In any case, try to make good explanations about why a particular locus has the type that was determined, or why a program could not be consistently typed.

- e. Is this implementation of type inference practical? Why or why not? If not, how can it be improved?

# A moral of this story

Solving combinatorial puzzles is fun, but it is not the real value of what we have done. Indeed, “SAT solvers” are important for solving real-world problems of this kind. But there is a deeper message here for the design of computational systems. By generalizing our programming from expression structures to wiring diagrams (which can be inconvenient—but that can be mitigated by compiling) we have made it possible to smoothly integrate nondeterministic choice into programs in a natural and efficient way. We can introduce hypotheticals, which provide alternative values supported by propositions that may be discarded without pain. This gives us the freedom to treat things like quadratic equations correctly. They really have two solutions, and any computation based on a choice of one solution may decide to reject it, while the other solution may lead, after a long computation, to an acceptable outcome. For example, that p:sqrt computes the traditional positive square root of a real number, we can build a directional propagator constructor p:honest-sqrt, with input cell xA2 and output cell x, that gives us a (hidden) choice of square roots:

```
define-p-prop (p:honest-sqrt (xA2) (x))
(let-cells (mul ` +x)
  (p:amb mul ` (-1 +1))
  (p:sqrt xA2 +x))
  (p*: mul x x)))
```

What is important here is that such choices may be introduced without arranging how to handle the ambiguity. For example, the constraint propagator that relates numbers to their squares can just use p:honest-sqrt:

```
define-c:prop (c:square x xA2)
(p:square x xA2)
(p:honest-sqrt xA2 x))
```

# 7.6 Propagation enables degeneracy

In the design of any significant system there are many implementation plans proposed for every component at every level of detail. However, in the system that is finally delivered this diversity of plans is lost, and usually only one unified plan is adopted and implemented. As an ecological system, the loss of diversity in the traditional engineering process has serious consequences.

We rarely build degeneracy into programs, partly because we traditionally have supplied no formal mechanisms for mediating its use. But the propagation idea provides a natural mechanism to incorporate degeneracy. The use of partial information in cells (introduced by Radul and Sussman [99]) allows multiple, perhaps overlapping, sources of information to be merged. We illustrated this with intervals in the stellar distance example in section 7.1. But there are more ways to merge partial information: partially specified symbolic expressions can be merged with unification, as shown in section 4.4.2. So the idea of partially specified information is not restricted to systems built with propagators, but if this is done in a propagator system, as proposed in exercise 7.8 on page 366, we have a paradigm for combining the contributions of multiple independent mechanisms. Similarly, we considered another idea from the AI problem-solving world for degenerate designs: goal-directed invocation. The idea is that instead of specifying “how” we want a goal accomplished, by naming a procedure to accomplish it, we specify “what” we want to accomplish, and we link procedures that can accomplish that goal. This linkage is often done with pattern matching, but is accidental rather than essential. If there is more than one way to accomplish the goal, then the choice of an appropriate procedure is a choice point that can be registered for backtracking. But chronological backtracking, constrained by the control flow of an expression, is extremely inefficient. We must break out of the expression to make dependency-directed backtracking work well, and propagation is one way to go. We still have a potentially exponential search, but the combinatorics are significantly reduced by eliminating bad choices using nogood sets learned from experience.

Of course, besides using a backtracking search for choosing a particular way to accomplish a goal, there are other ways that the goal can invoke degenerate methods. For example, we may want to run several possible ways to solve a problem in parallel, choosing the one that terminates first.

Suppose we have several independently implemented procedures all designed to solve the same (imprecisely specified) general class of problems. Assume for the moment that each design is reasonably competent and actually works correctly for most of the problems that might be encountered in actual operation. We know that we can make a more robust system by combining the given procedures into a larger system that independently invokes each of the procedures and compares their results, choosing the best answer on every problem. If the combination has independent ways of determining which answers are acceptable we are in very good shape. But even if we are reduced to voting, we get a system that reliably cover a larger space of solutions. Furthermore, if such a system can automatically log all cases where one of the designs fails, the operational feedback can be used to improve the performance of the procedure that failed.

This degenerate design strategy can be used at every level of detail. Every component of each subsystem itself be degenerately designed. If the components are shared among the subsystems, we get a controlled redundancy that is quite powerful. However, we can do even better. We can provide a mechanism for consistency checking of the independently designed subsystems, even when no particular value in one subsystem exactly corresponds to a particular value in another subsystem.

For a simple example, suppose we have two subsystems that are intended to deliver the same result, but computed in completely different ways. Assume that the designers agree that at some stage in one of the designs, the product of two of the variables in that design must be the same as the sum of two of the variables in the other design. There is no reason why this predicate should not be computed as soon as all of the four values it depends upon available, thus providing consistency checking at run time and powerful debugging information to the designers. This can be arranged using a locally embedded constraint network.
