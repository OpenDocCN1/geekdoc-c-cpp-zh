Other theoretical ideas of computation have also been in use—recursive function theory, Post systems, Markov systems, register machines. (A register machine is the simplest possible computer; its only instructions are increment, decrement, test-and-branch, halt.) Each of these models can be simulated by a Turing machine.

The Church–Turing thesis states that every model of computation—even those not yet in existence—can be done, and is equivalent to a Turing machine.

Note that there is no hope of proving this. It is not possible to prove something about computation that has not yet been proposed. However, the thesis has been verified for all known models of computation. It is widely accepted in the communities of logic, mathematics, and computer science. Its unprovability is why it makes the name thesis instead of *theorem*.

Thus, we will use a Turing machine as our model of computation. Or, stated otherwise;

+   Computation = expressible on a Turing machine
Algorithm = expressible on a Turing machine that halts

What can be done in some programming language can be done on a Turing machine. And, if one thinks of a new model of computation, the first question will be if it is Turing-complete. One can also ask if a Turing machine can do anything it can, but of course do we expect the answer to be yes.

The Church–Turing thesis states that Turing machines can carry out algorithms done by any model of computation whatsoever, including standard computer operations. At first glance, Turing machines seem less powerful than the standard desktop PC. The simplicity of the Turing machine is its best trait; it may be to write a complete Turing machine to do any interesting task, but theoretically, the operation is very straightforward.

It is not hard to write a program to emulate a Turing machine (in C++ Java, or other language). You can do it yourself, or you can find such programs on the Web. There may be a problem if the machine runs out of memory—Turing machines have unlimited tape to—but if necessary, one could suppose adding external memory as necessary. Theoretically, the total amount of external memory available in the world today is limited, but that limit is so large that this may not be a practical limitation.