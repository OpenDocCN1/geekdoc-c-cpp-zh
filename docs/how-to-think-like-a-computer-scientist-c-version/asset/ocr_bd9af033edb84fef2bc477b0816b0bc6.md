# CHAPTER 5. FRUITFUL FUNCTIONS

Of course, you might wonder who this value gets returned to, since we never
call main ourselves. It turns out that when the system executes a program,
it starts by calling main in in pretty much the same way it calls all the other
functions.

There are even some parameters that are passed to main by the system, but
we are not going to deal with them for a little while.

# 5.10 More recursion

So far we have learned a small subset of C++, but you might be interested
know that this subset is now a complete programming language, by which
I mean that anything that can be computed can be expressed in this language.
Any program ever could be written using only the language features
we used so far (actually, we would need a few commands to control devices
the keyboard, mouse, disks, etc.) but that all.

Proving that is a non-trivial exercise first accomplished by Alan Turing,
of the first computer scientists (well, some argue that he was a
mathematician). Accordingly, it is known as the Turing thesis. If you take a course on
the Theory of Computation, you will have chance to see the proof.

To give you an idea of what you can do with the tools we have learned
far, we will evaluate a recursively-defined mathematical functions. A recursive
definition is similar to a circular definition, in the sense that the definition
contains a reference to the thing being defined. A truly circular definition is
typically not useful:

frabjous: an adjective used to describe something that is franjous.

If you saw that definition in the dictionary, it might be annoyed.
of the other hand, if you looked up the definition of the mathematical function
factorial, you might get something like

```
0! = 1
n! = n · (n - 1)!
```

(Factorial is denoted with the symbol !, which is not to be confused
with the C++ logical operator ! which means NOT.) This definition says that
the factorial of 0 is 1, and the factorial of any other value, n is n multiplied
by the factorial of n-1. So 3! is 3 times 2!, which is 2 times 1!, which is 1 times
0!. Putting it all together, we get 3! equal to 3 times 2 times 1 times 1 times, which is
is 6.

If you can write a recursive definition of something, you can usually write a
C++ program to evaluate it. The first step is to decide what the parameters
for this function, and what the return type is. With a little thought, you
should conclude that factorial takes an integer as a parameter and returns an
integer: