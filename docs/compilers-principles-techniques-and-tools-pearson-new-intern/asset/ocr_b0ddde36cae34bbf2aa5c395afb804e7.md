| State | ACTION: c | ACTION: d | ACTION: $ | GOTO: S | GOTO: C |
|---:|:---:|:---:|:---:|:---:|:---:|
| 0 | s3 | s4 |  | 1 |  |
| 1 |  |  | acc |  |  |
| 2 | s6 | s7 |  |  | 5 |
| 3 | s3 | s4 |  |  | 8 |
| 4 | r3 | r3 |  |  |  |
| 5 |  |  | r1 |  |  |
| 6 | s6 | s7 |  |  | 9 |
| 7 |  |  | r3 |  |  |
| 8 | r2 | r2 |  |  |  |
| 9 |  |  | r2 |  |  |

Figure 4.42: Canonical parsing table for grammar (4.55)

# 4.7.4 Constructing LALR Parsing Tables

We now introduce our last parser construction method, the LALR (lookahead-LR) technique. This method is often used in practice, because the tables obtained by it are considerably smaller than the canonical LR tables, yet most common syntactic constructs of programming languages can be expressed conveniently by an LALR grammar. The same is almost true for SLR grammars, but there are a few constructs that cannot be conveniently handled by SLR techniques (see Example 4.48, for example).

For a comparison of parser size, the SLR and LALR tables for a grammar always have the same number of states, and this number is typically several hundred states for a language like C. The canonical LR table would typically have several thousand states for the same-size language. Thus, it is much easier and more economical to construct SLR and LALR tables than the canonical LR tables.

By way of introduction, let us again consider grammar (4.55), whose sets of LR(1) items were shown in Fig. 4.41. Take a pair of similar looking states, such as I₄ and I₇. Each of these states has only items with first component C → d·. In I₄, the lookaheads are c or d; in I₇, $ is the only lookahead.

To see the difference between the roles of I₄ and I₇ in the parser, note that the grammar generates the regular language c*dc*d. When reading an input cc···dccd···cd, the parser shifts the first group of c’s and their following d onto the stack, entering state 4 after reading the d. The parser then calls for a reduction by C → d, provided the next input symbol is c or d. The requirement that c or d follow makes sense, since these are the symbols that could begin strings in c*d. If $ follows the first d, we have an input like ccd, which is not in the language, and state 4 correctly declares an error if $ is the next input.

The parser enters state 7 after reading the second d. Then, the parser must