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

# ## 4.8 Using Ambiguous Grammars

It is a fact that every ambiguous grammar fails to be LR and thus is not in any of the classes of grammars discussed in the previous two sections. However, certain types of ambiguous grammars are quite useful in the specification and implementation of languages. For language constructs like expressions, an ambiguous grammar provides a shorter, more natural specification than any equivalent unambiguous grammar. Another use of ambiguous grammars is in isolating commonly occurring syntactic constructs for special-case optimization. With an ambiguous grammar, we can specify the special-case constructs by carefully adding new productions to the grammar.

Although the grammars we use are ambiguous, in all cases we specify disambiguating rules that allow only one parse tree for each sentence. In this way, the overall language specification becomes unambiguous, and sometimes it becomes possible to design an LR parser that follows the same ambiguity-resolving choices. We stress that ambiguous constructs should be used sparingly and in a strictly controlled fashion; otherwise, there can be no guarantee as to what language is recognized by a parser.