
## 4.7. More Powerful LR Parsers

This technique is useful because there tend to be rather few states in any one column of the GOTO table. The reason is that the GOTO on nonterminal *A* can only be a state derivable from a set of items in which some items have *A* immediately to the left of a dot. No set has items with *X* and *Y* immediately to the left of a dot if *X* ≠ *Y*. Thus, each state appears in at most one GOTO column.

For more space reduction, we note that the error entries in the goto table are never consulted. We can therefore replace each error entry by the most common non-error entry in its column. This entry becomes the default; it is represented in the list for each column by one pair with **any** in place of *currentState*.

**Example 4.66:** Consider Fig. 4.37 again. The column for *F* has entry 10 for state 7, and all other entries are either 3 or error. We may replace error by 3 and create for column *F* the list

| CURRENTSTATE | NEXTSTATE |
|---|---|
| 7 | 10 |
| **any** | 3 |

Similarly, a suitable list for column *T* is

| CURRENTSTATE | NEXTSTATE |
|---|---|
| 6 | 9 |
| **any** | 2 |

For column *E* we may choose either 1 or 8 to be the default; two entries are necessary in either case. For example, we might create for column *E* the list

|  |  |
|---|---|
| 4 | 8 |
| **any** | 1 |

□

This space savings in these small examples may be misleading, because the total number of entries in the lists created in this example and the previous one together with the pointers from states to action lists and from nonterminals to next-state lists, result in unimpressive space savings over the matrix implementation of Fig. 4.37. For practical grammars, the space needed for the list representation is typically less than ten percent of that needed for the matrix representation. The table-compression methods for finite automata that were discussed in Section 3.9.8 can also be used to represent LR parsing tables.

### 4.7.7 Exercises for Section 4.7

**Exercise 4.7.1:** Construct the

- a) canonical LR, and
- b) LALR

sets of items for the grammar $S \rightarrow S\ S\ + \mid S\ S\ * \mid a$ of Exercise 4.2.1.

**Exercise 4.7.2:** Repeat Exercise 4.7.1 for each of the (augmented) grammars of Exercise 4.2.2(a)–(g).

**! Exercise 4.7.3:** For the grammar of Exercise 4.7.1, use Algorithm 4.63 to compute the collection of LALR sets of items from the kernels of the LR(0) sets of items.

**! Exercise 4.7.4:** Show that the following grammar

$S \rightarrow A\ a \mid b\ A\ c \mid d\ c \mid b\ d\ a$
$A \rightarrow d$

is LALR(1) but not SLR(1).

**! Exercise 4.7.5:** Show that the following grammar

$S \rightarrow A\ a \mid b\ A\ c \mid B\ c \mid b\ B\ a$
$A \rightarrow d$
$B \rightarrow d$

is LR(1) but not LALR(1).

## 4.8 Using Ambiguous Grammars

It is a fact that every ambiguous grammar fails to be LR and thus is not in any of the classes of grammars discussed in the previous two sections. However, certain types of ambiguous grammars are quite useful in the specification and implementation of languages. For language constructs like expressions, an ambiguous grammar provides a shorter, more natural specification than any equivalent unambiguous grammar. Another use of ambiguous grammars is in isolating commonly occurring syntactic constructs for special-case optimization. With an ambiguous grammar, we can specify the special-case constructs by carefully adding new productions to the grammar.

Although the grammars we use are ambiguous, in all cases we specify disambiguating rules that allow only one parse tree for each sentence. In this way, the overall language specification becomes unambiguous, and sometimes it becomes possible to design an LR parser that follows the same ambiguity-resolving choices. We stress that ambiguous constructs should be used sparingly and in a strictly controlled fashion; otherwise, there can be no guarantee as to what language is recognized by a parser.

### 4.8.1 Precedence and Associativity to Resolve Conflicts

Consider the ambiguous grammar (4.3) for expressions with operators + and *, repeated here for convenience:

$$E \to E + E \mid E * E \mid (E) \mid \mathrm{id}$$

This grammar is ambiguous because it does not specify the associativity or precedence of the operators + and *. The unambiguous grammar (4.1), which includes productions $E \to E + T$ and $T \to T * F$, generates the same language, but gives + lower precedence than *, and makes both operators left associative. There are two reasons why we might prefer to use the ambiguous grammar. First, as we shall see, we can easily change the associativity and precedence of the operators + and * without disturbing the productions of (4.3) or the number of states in the resulting parser. Second, the parser for the unambiguous grammar will spend a substantial fraction of its time reducing by the productions $E \to T$ and $T \to F$, whose sole function is to enforce associativity and precedence. The parser for the ambiguous grammar (4.3) will not waste time reducing by these single productions (productions whose body consists of a single nonterminal).

The sets of LR(0) items for the ambiguous expression grammar (4.3) augmented by $E' \to E$ are shown in Fig. 4.48. Since grammar (4.3) is ambiguous, there will be parsing-action conflicts when we try to produce an LR parsing table from the sets of items. The states corresponding to sets of items $I_7$ and $I_8$ generate these conflicts. Suppose we use the SLR approach to constructing the parsing action table. The conflict generated by $I_7$ between reduction by $E \to E + E$ and shift on + or * cannot be resolved, because + and * are each in FOLLOW($E$). Thus both actions would be called for on inputs + and *. A similar conflict is generated by $I_8$, between reduction by $E \to E * E$ and shift on inputs + and *. In fact, each of our LR parsing table-construction methods will generate these conflicts.

However, these problems can be resolved using the precedence and associativity information for + and *. Consider the input id + id * id, which causes a parser based on Fig. 4.48 to enter state 7 after processing id + id; in particular the parser reaches a configuration

| PREFIX | STACK | INPUT |
|---|---|---|
| $E + E$ | 0 1 4 7 | $*\ \mathrm{id}\ \$$ |

For convenience, the symbols corresponding to the states 1, 4, and 7 are also shown under PREFIX.

If * takes precedence over +, we know the parser should shift * onto the stack, preparing to reduce the + and its surrounding id symbols to an expression. This choice was made by the SLR parser of Fig. 4.37, based on an unambiguous grammar for the same language. On the other hand, if + takes precedence over *, we know the parser should reduce $E + E$ to $E$. Thus the relative precedence of + followed by * uniquely determines how the parsing action conflict between reducing $E \rightarrow E + E$ and shifting on * in state 7 should be resolved.

![](img/2a44b9071782fade81f3050c3b718341_284_0.png)

If the input had been $id + id + id$ instead, the parser would still reach a configuration in which it had stack $0\ 1\ 4\ 7$ after processing input $id + id$. On input + there is again a shift/reduce conflict in state 7. Now, however, the associativity of the + operator determines how this conflict should be resolved. If + is left associative, the correct action is to reduce by $E \rightarrow E + E$. That is, the id symbols surrounding the first + must be grouped first. Again this choice coincides with what the SLR parser for the unambiguous grammar would do.

In summary, assuming + is left associative, the action of state 7 on input + should be to reduce by $E \rightarrow E + E$, and assuming that * takes precedence over +, the action of state 7 on input * should be to shift. Similarly, assuming that * is left associative and takes precedence over +, we can argue that state 8, which can appear on top of the stack only when $E * E$ are the top three grammar symbols, should have the action reduce $E \rightarrow E * E$ on both + and * inputs. In the case of input +, the reason is that * takes precedence over +, while in the case of input *, the rationale is that * is left associative.
