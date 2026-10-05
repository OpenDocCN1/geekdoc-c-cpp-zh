subpattern. A common extension to the language adds the plus-sign (+) operator. A plus sign following a subpattern means one or more copies of the subpattern.

Define Scheme procedures r:* and r:+ to take a pattern and iterate it as necessary. This can be done in terms of r:repeat.

Demonstrate your procedures on real data in complex patterns.

# Exercise 2.7: A bug, one bad joke, two tweaks, and a revelation

Ben Bitiddle has noticed a problem with our implementation of (r:repeat min max expr).

The use of (r:alt expr "") at the end of the r:repeat procedure is a bit dodgy. This code fragment translates to \expr\, where expr is the value of expr. This relies on the fact that alternation confuses with something and nothing is the equivalent of saying "one or none." (We will omit the required confusing backslashes in the rest of this explanation.) This is: (expr|) denotes one or no instances of expr. Unfortunately, this depends on an undocumented GNU extension to the formal POSIX standard for REs.

Specifically, section 9.4.3 of the POSIX standard^10 states that a vertical line appearing immediately before a close parenthesis (or immediately after an open parenthesis) produces undefined behavior. In essence, an RE must not be a null sequence.

GNU grep just happens to "do the right thing" when presented with (x]. Not all grep implementations are tolerant.

Therefore, Ben asks his team of three code hackers (Louis, Alyssa, and Eva) to propose alternative workarounds. Ultimately, he proposes his own patch, which you will implement.

+   Louis Reasoner suggests that a simple, elegant fix would be to replace the code fragment (r:alt expr "") with a straightforward call to (r:repeat 0 1 expr).

+   Alyssa P. Hacker proposes to rewrite the else clause of r:repeat to translate (r:repeat 3 5 x) into the equivalent of