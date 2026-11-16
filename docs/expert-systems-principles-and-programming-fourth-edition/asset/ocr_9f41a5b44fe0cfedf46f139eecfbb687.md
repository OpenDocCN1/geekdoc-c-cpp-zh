```
RULE MOVE-TO-FLOOR
IF The goal is to move block ?upper on top of
the floor and
block ?upper is the top block in its stack,
THEN Move block ?upper on top of the floor.
```

The move-to-floor rule can now move blocks A and D to the floor. Once block A is moved to the floor, the move-to-floor rule can be activated to move block B to the floor. With blocks A, B, and D on the floor, blocks C and E are now the top blocks in their stacks and it is possible to use the move-directly rule to move block C on top of block E.

Now that the rules have been written using pseudocode, the facts to be used by the rules should be determined. The types of facts needed cannot always be determined without some prototyping. In this case, the pseudocode rules point out several types of facts that will be needed. For example, the information about which blocks are on top of other blocks is crucial. This information could be described with the following deftemplate:

```
{deftemplate on-top-of
(slot upper)
(slot lower)}
```

and the facts described by this template would be:

+   - (on-top-of (upper A) (lower B))
+   - (on-top-of (upper B) (lower C))
+   - (on-top-of (upper D) (lower E))
+   - (on-top-of (upper E) (lower F))

Since it is also important to know which blocks are at the top and bottom of a stack, it would be useful to include the following facts:

+   - (on-top-of (upper nothing) (lower A))
+   - (on-top-of (upper C) (lower floor))
+   - (on-top-of (upper nothing) (lower D))
+   - (on-top-of (upper F) (lower floor))

The words nothing and floor have special meaning in these facts. The facts (on-top-of (upper nothing) (lower A)) and (on-top-of (upper nothing) (lower D)) indicate that A and D are the top blocks in their stacks. Similarly, the facts (on-top-of (upper C) (lower floor)) and (on-top-of (upper F) (lower floor)) indicate that blocks C and F are the bottom blocks in their stacks. Including these facts does not necessarily solve the problem of determining the top and bottom blocks in a stack. If the rules are not written correctly, the words floor and nothing might be mistaken as the names of blocks. Facts that indicate the names of the blocks might be useful. The following facts using the implied deftemplate block can be used to identify the blocks from the special words nothing and floor: