Turing machines are self-referential. Note that a Turing machine can take any string (over the proper alphabet) as input. All Turing machines and all inputs can be encoded as strings {0, 1}. The self-referential property will arise when a Turing machine is run on its own description, that is, its own encoding.

Recall that the universal Turing takes a machine encoded over {0, 1} and the input to the machine (also encoded) and emulates the actions of the machine on the string. These two strings can be identical, so the universal Turing machine is given a machine M and emulates M on the string that is also the encoding of M.

This may sound odd, since in computer science we rarely run a program on itself. However, we could do so. Consider a C++ program that takes some input. The program is a string of 0s and 1s, of course, once it is stored in a computer. It, whether integers, strings, files—or some combination thereof—is also a string of 0s and 1s. We can use the program as the input string. It might be too long (in which case the program will only use part of it) or too short (and then the program will probably sit and wait for more input, or do whatever it has been written to do on insufficient input).

Other problems—and other paradoxes—present problems when they are self-referential. The whole theory of sets was revised by the difficulties presented by Russell's paradox. One way to understand self-referencing is to look at some examples.

# 6.1.1.1 Problem 1: The Barber

There is on an island in the Mediterranean where there is a barber who shaves everyone who does not shave themselves. This means that: (1) everyone shaves—regardless of age and gender, and (2) the barber shaves a person if and only if that person does not shave himself or herself.

This town with this barber cannot exist as stated. The contradiction is in who shaves the barber? According to the statement, if B does not shave himself, then the barber B should indeed do the shaving. And if B does himself, that puts him in the category of people that the barber does not shave.

There is no way around this problem by adding women, children, and robots. The only way around it is to change the wording so that the “B shaves P iff P does not shave himself” only applies to others, and not to the barber.