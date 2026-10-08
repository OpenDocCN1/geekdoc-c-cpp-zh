# TRY THIS

> Before reading further, try to see how many errors you can find in f(). Specifically, which of the calls of poor() could cause the program to crash?

At first glance, the calls look fine, but this is the kind of code that costs a programmer long nights of debugging and gives a quality engineer nightmares.

+   1.  Passing the wrong element type, e.g., poor(&s0[0], s0.size()). Also, s0 might be empty, in which case &s0[0] is wrong.
2.  Use of a “magic constant” (here, correct): poor(s1, 10). Also, wrong element type.
3.  Use of a “magic constant” (here, incorrect): poor(s2, 20).
4.  Correct (easily verified): first call poor(p1, 1).
5.  Passing a null pointer: second call poor(p1, 1).
6.  May be correct: poor(q, max). We can’t be sure from looking at this code fragment. To see if q points to an array with at least max elements, we have to find the definitions of q and max and determine their values at our point of use.

In each case, the errors are simple. We are not dealing with some subtle algorithmic or data structure problem. The problem is that poor()’s interface, involving an array passed as a pointer, opens the possibility of a collection of problems. You may appreciate how the problems were obscured by our use of “technical” unhelpful names, such as p1 and s0. However, mnemonic, but misleading, names can make such problems even harder to spot.

In theory, a compiler could catch a few of these errors (such as the second call of poor(p1, 1) where p1==0), but realistically we can be saved from disaster for this particular example only because the compiler catches the attempt to define objects of the abstract class Shape. However, that is unrelated to poor()’s interface problems, so we should not take too much comfort from that. In the following, we use a variant of Shape that is not abstract so as not to get distracted from the interface problems.

How come the poor(&s0[0], s0.size()) call is an error? The &s0[0] refers to the first element of an array of Circles; it is a Circle*. We expect a Shape* and we pass a pointer to an object of a class derived from Shape (here, a Circle*). That’s obviously acceptable: we need that conversion so that we can do object-oriented programming, accessing objects of a variety of types through their common interface