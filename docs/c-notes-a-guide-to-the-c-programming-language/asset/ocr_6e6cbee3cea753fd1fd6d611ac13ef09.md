# 0: SYNTAX

> > What do you read, my Lord?
> 
> > Words, words, words.
> 
> > — Shakespeare, Hamlet



The C programming language consists of a language definition, an implementation, and a run-time environment. The language definition describes C independent of any particular machine characteristics; the implementation strives to enforce that definition in terms of some real computer; and the corresponding run-time environment makes up for any inadequacies in the implementation or in the machine, in order to emulate a C machine with sufficient fidelity to satisfy the language definition.

C is a machine-independent language that attempts to model the basic operators and operands of most modern computers. As such, C is capable of being translated into efficient and compact code on a variety of machines, but only at the cost of a certain amount of indeterminacy in the language definition. It is necessary, therefore, to occasionally stress those aspects of a C program that may vary among different implementations; and it is often useful to know what can be controlled by mere changes in the run-time support package.

This book will focus primarily on the machine-independent definition of C, since that is its most portable aspect. But it is important to keep in mind that C is implemented as a compiler,