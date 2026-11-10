# 4.6. INTRODUCTION TO LR PARSING: SIMPLE LR

| | STACK | SYMBOLS | INPUT | ACTION |
|---|---|---|---|---|
| (1) | 0 |  | id * id + id $ | shift |
| (2) | 0 5 | id | * id + id $ | reduce by F → id |
| (3) | 0 3 | F | * id + id $ | reduce by T → F |
| (4) | 0 2 | T | * id + id $ | shift |
| (5) | 0 2 7 | T * | id + id $ | shift |
| (6) | 0 2 7 5 | T * id | + id $ | reduce by F → id |
| (7) | 0 2 7 10 | T * F | + id $ | reduce by T → T * F |
| (8) | 0 2 | T | + id $ | reduce by E → T |
| (9) | 0 1 | E | + id $ | shift |
| (10) | 0 1 6 | E + | id $ | shift |
| (11) | 0 1 6 5 | E + id | $ | reduce by F → id |
| (12) | 0 1 6 3 | E + F | $ | reduce by T → F |
| (13) | 0 1 6 9 | E + T | $ | reduce by E → E + T |
| (14) | 0 1 | E | $ | accept. |

Figure 4.38: Moves of an LR parser on id * id + id

The *ACTION* and *GOTO* entries in the parsing table are then constructed using the following algorithm. It requires us to know *FOLLOW*(*A*) for each nonterminal *A* of a grammar (see Section 4.4).

**Algorithm 4.46:** Constructing an SLR-parsing table.

**INPUT:** An augmented grammar *G*′.

**OUTPUT:** The SLR-parsing table functions ACTION and GOTO for *G*′.

**METHOD:**

+   1. Construct *C* = {*I*_0, *I*_1, ..., *I*_n}, the collection of sets of LR(0) items for *G*′.
+   2. State *i* is constructed from *I*_i. The parsing actions for state *i* are determined as follows:
+       (a) If [*A* → α·*a*β] is in *I*_i and GOTO(*I*_i, *a*) = *I*_j, then set ACTION[*i*, *a*] to “shift *j*.” Here *a* must be a terminal.
+       (b) If [*A* → α·] is in *I*_i, then set ACTION[*i*, *a*] to “reduce *A* → α” for all *a* in FOLLOW(*A*); here *A* may not be *S*′.
+       (c) If [*S*′ → *S*·] is in *I*_i, then set ACTION[*i*, $] to “accept.”

If any conflicting actions result from the above rules, we say the grammar is not SLR(1). The algorithm fails to produce a parser in this case.