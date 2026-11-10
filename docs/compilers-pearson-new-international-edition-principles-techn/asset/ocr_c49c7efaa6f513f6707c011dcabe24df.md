The bodies of the three productions with nonterminal *list* as head equivalently can be grouped:

*list* → *list* + *digit* | *list* − *digit* | *digit*

According to our conventions, the terminals of the grammar are the symbols

+ − 0 1 2 3 4 5 6 7 8 9

The nonterminals are the italicized names *list* and *digit*, with *list* being the start symbol because its productions are given first. □

We say a production is *for* a nonterminal if the nonterminal is the head of the production. A string of terminals is a sequence of zero or more terminals. The string of zero terminals, written as ε, is called the *empty string*.

# 2.2.2  Derivations

A grammar derives strings by beginning with the start symbol and repeatedly replacing a nonterminal by the body of a production for that nonterminal. The terminal strings that can be derived from the start symbol form the *language* defined by the grammar.

**Example 2.2:** The language defined by the grammar of Example 2.1 consists of lists of digits separated by plus and minus signs. The ten productions for the nonterminal *digit* allow it to stand for any of the terminals 0, 1, ..., 9. From production (2.3), a single digit by itself is a list. Productions (2.1) and (2.2) express the rule that any list followed by a plus or minus sign and then another digit makes up a new list.

Productions (2.1) to (2.4) are all we need to define the desired language. For example, we can deduce that 9−5+2 is a *list* as follows.

+   a) 9 is a *list* by production (2.3), since 9 is a *digit*.
+   
+   b) 9−5 is a *list* by production (2.2), since 9 is a *list* and 5 is a *digit*.
+   
+   c) 9−5+2 is a *list* by production (2.1), since 9−5 is a *list* and 2 is a *digit*.

**Example 2.3:** A somewhat different sort of list is the list of parameters in a function call. In Java, the parameters are enclosed within parentheses, as in the call max(x, y) of function max with parameters x and y. One nuance of such lists is that an empty list of parameters may be found between the terminals ( and ). We may start to develop a grammar for such sequences with the productions:

²Technically, ε can be a string of zero symbols from any alphabet (collection of symbols).