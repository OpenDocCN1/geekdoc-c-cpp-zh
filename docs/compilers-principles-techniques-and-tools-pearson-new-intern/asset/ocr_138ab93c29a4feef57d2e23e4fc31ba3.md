# Structure of the LR Parsing Table

The parsing table consists of two parts: a parsing-action function ACTION and a goto function GOTO.

+   1. The ACTION function takes as arguments a state $i$ and a terminal $a$ (or $, the input endmarker). The value of ACTION[$i,a$] can have one of four forms:
+      (a) Shift $j$, where $j$ is a state. The action taken by the parser effectively shifts input $a$ to the stack, but uses state $j$ to represent $a$.
+      (b) Reduce $A \to \beta$. The action of the parser effectively reduces $\beta$ on the top of the stack to head $A$.
+      (c) Accept. The parser accepts the input and finishes parsing.
+      (d) Error. The parser discovers an error in its input and takes some corrective action. We shall have more to say about how such error-recovery routines work in Sections 4.8.3 and 4.9.4.

+   2. We extend the GOTO function, defined on sets of items, to states: if GOTO[$I_i,A$] = $I_j$, then GOTO also maps a state $i$ and a nonterminal $A$ to state $j$.

# LR-Parser Configurations

To describe the behavior of an LR parser, it helps to have a notation representing the complete state of the parser: its stack and the remaining input. A *configuration* of an LR parser is a pair:

$$(s_0s_1\cdots s_m,\ a_i a_{i+1}\cdots a_n\$)$$

where the first component is the stack contents (top on the right), and the second component is the remaining input. This configuration represents the right-sentential form

$$X_1X_2\cdots X_m a_i a_{i+1}\cdots a_n$$

in essentially the same way as a shift-reduce parser would; the only difference is that instead of grammar symbols, the stack holds states from which grammar symbols can be recovered. That is, $X_i$ is the grammar symbol represented by state $s_i$. Note that $s_0$, the start state of the parser, does not represent a grammar symbol, and serves as a bottom-of-stack marker, as well as playing an important role in the parse.

symbol. See for example states 1 and 8 in the LR(0) automaton in Fig. 4.31, which are both entered by transitions on $E$, or states 2 and 9, which are both entered by transitions on $T$.