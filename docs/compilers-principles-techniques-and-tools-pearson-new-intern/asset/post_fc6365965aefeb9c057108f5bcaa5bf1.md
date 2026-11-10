
- a) SSS + a * +.
- b) SS + a * a+.
- c) aaa * a ++.

**Exercise 4.5.3:** Give bottom-up parses for the following input strings and grammars:

- a) The input 000111 according to the grammar of Exercise 4.5.1.
- b) The input aaa * a ++ according to the grammar of Exercise 4.5.2.

## 4.6 Introduction to LR Parsing: Simple LR

The most prevalent type of bottom-up parser today is based on a concept called LR(k) parsing; the “L” is for left-to-right scanning of the input, the “R” for constructing a rightmost derivation in reverse, and the k for the number of input symbols of lookahead that are used in making parsing decisions. The cases k = 0 or k = 1 are of practical interest, and we shall only consider LR parsers with k ≤ 1 here. When k is omitted, k is assumed to be 1.

This section introduces the basic concepts of LR parsing and the easiest method for constructing shift-reduce parsers, called “simple LR” (or SLR, for short). Some familiarity with the basic concepts is helpful even if the LR parser itself is constructed using an automatic parser generator. We begin with “items” and “parser states;” the diagnostic output from an LR parser generator typically includes parser states, which can be used to isolate the sources of parsing conflicts.

Section 4.7 introduces two, more complex methods — canonical-LR and LALR — that are used in the majority of LR parsers.

### 4.6.1 Why LR Parsers?

LR parsers are table-driven, much like the nonrecursive LL parsers of Section 4.4.4. A grammar for which we can construct a parsing table using one of the methods in this section and the next is said to be an LR grammar. Intuitively, for a grammar to be LR it is sufficient that a left-to-right shift-reduce parser be able to recognize handles of right-sentential forms when they appear on top of the stack.

LR parsing is attractive for a variety of reasons:

- LR parsers can be constructed to recognize virtually all programming-language constructs for which context-free grammars can be written. Non-LR context-free grammars exist, but these can generally be avoided for typical programming-language constructs.
- The LR-parsing method is the most general nonbacktracking shift-reduce parsing method known, yet it can be implemented as efficiently as other, more primitive shift-reduce methods (see the bibliographic notes).
- An LR parser can detect a syntactic error as soon as it is possible to do so on a left-to-right scan of the input.
- The class of grammars that can be parsed using LR methods is a proper superset of the class of grammars that can be parsed with predictive or LL methods. For a grammar to be LR(k), we must be able to recognize the occurrence of the right side of a production in a right-sentential form, with k input symbols of lookahead. This requirement is far less stringent than that for LL(k) grammars where we must be able to recognize the use of a production seeing only the first k symbols of what its right side derives. Thus, it should not be surprising that LR grammars can describe more languages than LL grammars.

The principal drawback of the LR method is that it is too much work to construct an LR parser by hand for a typical programming-language grammar. A specialized tool, an LR parser generator, is needed. Fortunately, many such generators are available, and we shall discuss one of the most commonly used ones, Yacc, in Section 4.9. Such a generator takes a context-free grammar and automatically produces a parser for that grammar. If the grammar contains ambiguities or other constructs that are difficult to parse in a left-to-right scan of the input, then the parser generator locates these constructs and provides detailed diagnostic messages.

### 4.6.2 Items and the LR(0) Automaton

How does a shift-reduce parser know when to shift and when to reduce? For example, with stack contents $T$ and next input symbol * in Fig. 4.28, how does the parser know that $T$ on the top of the stack is not a handle, so the appropriate action is to shift and not to reduce $T$ to $E$?

An LR parser makes shift-reduce decisions by maintaining states to keep track of where we are in a parse. States represent sets of “items.” An LR(0) item (item for short) of a grammar $G$ is a production of $G$ with a dot at some position of the body. Thus, production $A \to XYZ$ yields the four items

$$A \to \cdot XYZ$$

$$A \to X \cdot YZ$$

$$A \to XY \cdot Z$$

$$A \to XYZ \cdot$$

The production $A \to \epsilon$ generates only one item, $A \to \cdot$.

Intuitively, an item indicates how much of a production we have seen at a given point in the input. For example, the item $A \to X \cdot YZ$ indicates that we hope to see a string derivable from $XYZ$ next on the input. Item $A \to X \cdot YZ$ indicates that we have just seen on the input a string derivable from $X$ and that we hope next to see a string derivable from $YZ$. Item $A \to XYZ \cdot$ indicates that we have seen the body $XYZ$ and that it may be time to reduce $XYZ$ to $A$.

#### Representing Item Sets

A parser generator that produces a bottom-up parser may need to represent items and sets of items conveniently. Note that an item can be represented by a pair of integers, the first of which is the number of one of the productions of the underlying grammar, and the second of which is the position of the dot. Sets of items can be represented by a list of these pairs. However, as we shall see, the necessary sets of items often include “closure” items, where the dot is at the beginning of the items in the body. These can always be reconstructed from the other items in the set, and we do not have to include them in the list.

One collection of sets of LR(0) items, called the *canonical LR(0) collection*, provides the basis for constructing a deterministic finite automaton that is used to make parsing decisions. Such an automaton is called an $LR(0)$ automaton. In particular, each state of the LR(0) automaton represents a set of items in the canonical LR(0) collection. The automaton for the expression grammar (4.1), shown in Fig. 4.31, will serve as the running example for discussing the canonical LR(0) collection for a grammar.

To construct the canonical LR(0) collection for a grammar, we define an augmented grammar and two functions, CLOSURE and GOTO. If $G$ is a grammar with start symbol $S$, then $G'$, the *augmented grammar* for $G$, is $G$ with a new start symbol $S'$ and one production $S' \to S$. The purpose of this new starting production is to indicate to the parser when it should stop parsing and announce acceptance of the input. That is, acceptance occurs when and only when the parser is about to reduce by $S' \to S$.

#### Closure of Item Sets

If $I$ is a set of items for a grammar $G$, then CLOSURE($I$) is the set of items constructed from $I$ by the two rules:

- 1. Initially, add every item in $I$ to CLOSURE($I$).
- 2. If $A \to \alpha \cdot B\beta$ is in CLOSURE($I$) and $B \to \gamma$ is a production, then add the item $B \to \cdot\gamma$ to CLOSURE($I$), if it is not already there. Apply this rule until no more new items can be added to CLOSURE($I$).

³Technically, the automaton misses being deterministic according to the definition of Section 3.6.4, because we do not have a dead state, corresponding to the empty set of items. As a result, there are some state-input pairs for which no next state exists.

![](img/a29d16e454785bb105e96ef448ac07f6_248_0.png)

Figure 4.31: LR(0) automaton for the expression grammar (4.1)

Intuitively, $A \to \alpha \cdot B\beta$ in *CLOSURE(I)* indicates that, at some point in the parsing process, we think we might next see a substring derivable from $B\beta$ as input. The substring derivable from $B\beta$ will have a prefix derivable from $B$ by applying one of the $B$-productions; that is, if $B \to \gamma$ is a production, we also include $B \to \cdot\gamma$ in *CLOSURE(I)*.

**Example 4.40:** Consider the augmented expression grammar:

```text
E' → E
E  → E + T | T
T  → T * F | F
F  → ( E ) | id
```

If $I$ is the set of one item $\{[E' \to \cdot E]\}$, then CLOSURE($I$) contains the set of items $I_0$ in Fig. 4.31.
