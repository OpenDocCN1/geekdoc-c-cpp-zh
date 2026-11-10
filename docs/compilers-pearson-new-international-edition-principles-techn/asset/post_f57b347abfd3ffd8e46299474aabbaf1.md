
### 4.11. REFERENCES FOR CHAPTER 4

The general-purpose dynamic-programming parsing algorithm described in Exercise 4.4.9 was invented independently by J. Cocke (unpublished), by Younger [30], and Kasami [21]; hence the “CYK algorithm.” There is a more complex, general-purpose algorithm due to Earley [11] that tabulates LR-items for each substring of the given input; this algorithm, while also O(n³) in general, is only O(n²) on unambiguous grammars.

- 1. Aho, A. V., S. C. Johnson, and J. D. Ullman, “Deterministic parsing of ambiguous grammars,” *Comm. ACM* 18:8 (Aug., 1975), pp. 441–452.
- 2. Backus, J. W., “The syntax and semantics of the proposed international algebraic language of the Zurich-ACM-GAMM Conference,” *Proc. Intl. Conf. Information Processing*, UNESCO, Paris, (1959) pp. 125–132.
- 3. Birman, A. and J. D. Ullman, “Parsing algorithms with backtrack,” *Information and Control* 23:1 (1973), pp. 1–34.
- 4. Cantor, D. C., “On the ambiguity problem of Backus systems,” *J. ACM* 9:4 (1962), pp. 477–479.
- 5. Chomsky, N., “Three models for the description of language,” *IRE Trans. on Information Theory* IT-2:3 (1956), pp. 113–124.
- 6. Chomsky, N., “On certain formal properties of grammars,” *Information and Control* 2:2 (1959), pp. 137–167.
- 7. Dain, J., “Bibliography on Syntax Error Handling in Language Translation Systems,” 1991. Available from the comp.compilers newsgroup; see http://compilers.iecc.com/comparch/article/91-04-050 .
- 8. DeRemer, F., “Practical Translators for LR(k) Languages,” Ph.D. thesis, MIT, Cambridge, MA, 1969.
- 9. DeRemer, F., “Simple LR(k) grammars,” *Comm. ACM* 14:7 (July, 1971), pp. 453–460.
- 10. Donnelly, C. and R. Stallman, “Bison: The YACC-compatible Parser Generator,” http://www.gnu.org/software/bison/manual/ .
- 11. Earley, J., “An efficient context-free parsing algorithm,” *Comm. ACM* 13:2 (Feb., 1970), pp. 94–102.
- 12. Earley, J., “Ambiguity and precedence in syntax description,” *Acta Informatica* 4:2 (1975), pp. 183–192.
- 13. Floyd, R. W., “On ambiguity in phrase-structure languages,” *Comm. ACM* 5:10 (Oct., 1962), pp. 526–534.
- 14. Floyd, R. W., “Syntactic analysis and operator precedence,” *J. ACM* 10:3 (1963), pp. 316–333.
- 15. Grune, D. and C. J. H. Jacobs, “A programmer-friendly LL(1) parser generator,” Software Practice and Experience 18:1 (Jan., 1988), pp. 29–38. See also http://www.cs.vu.nl/~ceriel/LLgen.html .
- 16. Hoare, C. A. R., “Report on the Elliott Algol translator,” Computer J. 5:2 (1962), pp. 127–129.
- 17. Hopcroft, J. E., R. Motwani, and J. D. Ullman, Introduction to Automata Theory, Languages, and Computation, Addison-Wesley, Boston MA, 2001.
- 18. Hudson, S. E. et al., “CUP LALR Parser Generator in Java,” Available at http://www2.cs.tum.edu/projects/cup/ .
- 19. Ingerman, P. Z., “Panini-Backus form suggested,” Comm. ACM 10:3 (March 1967), p. 137.
- 20. Johnson, S. C., “Yacc — Yet Another Compiler Compiler,” Computing Science Technical Report 32, Bell Laboratories, Murray Hill, NJ, 1975. Available at http://dinosaur.compilertools.net/yacc/ .
- 21. Kasami, T., “An efficient recognition and syntax analysis algorithm for context-free languages,” AFCRL-65-758, Air Force Cambridge Research Laboratory, Bedford, MA, 1965.
- 22. Knuth, D. E., “On the translation of languages from left to right,” Information and Control 8:6 (1965), pp. 607–639.
- 23. Korenjak, A. J., “A practical method for constructing LR(k) processors,” Comm. ACM 12:11 (Nov., 1969), pp. 613–623.
- 24. Lewis, P. M. II and R. E. Stearns, “Syntax-directed transduction,” J. ACM 15:3 (1968), pp. 465–488.
- 25. McClure, R. M., “TMG — a syntax-directed compiler,” Proc. 20th ACM Natl. Conf. (1965), pp. 262–274.
- 26. Naur, P. et al., “Report on the algorithmic language ALGOL 60,” Comm. ACM 3:5 (May, 1960), pp. 299–314. See also Comm. ACM 6:1 (Jan., 1963), pp. 1–17.
- 27. Parr, T., “ANTLR,” http://www.antlr.org/ .
- 28. Schorre, D. V., “Meta-II: a syntax-oriented compiler writing language,” Proc. 19th ACM Natl. Conf. (1964) pp. D1.3-1–D1.3-11.
- 29. Wirth, N. and H. Weber, “Euler: a generalization of Algol and its formal definition: Part I,” Comm. ACM 9:1 (Jan., 1966), pp. 13–23.
- 30. Younger, D. H., “Recognition and parsing of context-free languages in time n³,” Information and Control 10:2 (1967), pp. 189–208.

## Chapter 5

## Syntax-Directed Translation

This chapter develops the theme of Section 2.3: the translation of languages guided by context-free grammars. The translation techniques in this chapter will be applied in Chapter 6 to type checking and intermediate-code generation. The techniques are also useful for implementing little languages for specialized tasks; this chapter includes an example from typesetting.

We associate information with a language construct by attaching *attributes* to the grammar symbol(s) representing the construct, as discussed in Section 2.3.2. A syntax-directed definition specifies the values of attributes by associating semantic rules with the grammar productions. For example, an infix-to-postfix translator might have a production and rule

| Production | Semantic Rule |
|---|---|
| E → E₁ + T | E.code = E₁.code ‖ T.code ‖ ' +' (5.1) |

This production has two nonterminals, E and T; the subscript in E₁ distinguishes the occurrence of E in the production body from the occurrence of E as the head. Both E and T have a string-valued attribute *code*. The semantic rule specifies that the string *E.code* is formed by concatenating *E₁.code*, *T.code*, and the character `'+'`. While the rule makes it explicit that the translation of E is built up from the translations of E₁, T, and `'+'`, it may be inefficient to implement the translation directly by manipulating strings.

From Section 2.3.5, a syntax-directed translation scheme embeds program fragments called semantic actions within production bodies, as in

```
E → E₁ + T { print ' +' }                (5.2)
```

By convention, semantic actions are enclosed within curly braces. (If curly braces occur as grammar symbols, we enclose them within single quotes, as in

### 5.1. SYNTAX-DIRECTED DEFINITIONS

### An Alternative Definition of Inherited Attributes

No additional translations are enabled if we allow an inherited attribute $B.c$ at a node $N$ to be defined in terms of attribute values at the children of $N$, as well as at $N$ itself, at its parent, and at its siblings. Such rules can be “simulated” by creating additional attributes of $B$, say $B.c_1, B.c_2, \ldots$. These are synthesized attributes that copy the needed attributes of the children of the node labeled $B$. We then compute $B.c$ as an inherited attribute, using the attributes $B.c_1, B.c_2, \ldots$ in place of attributes at the children. Such attributes are rarely needed in practice.

While we do not allow an inherited attribute at node $N$ to be defined in terms of attribute values at the children of node $N$, we do allow a synthesized attribute at node $N$ to be defined in terms of inherited attribute values at node $N$ itself. Terminals can have synthesized attributes, but not inherited attributes. Attributes for terminals have lexical values that are supplied by the lexical analyzer; there are no semantic rules in the SDD itself for computing the value of an attribute for a terminal.

**Example 5.1:** The SDD in Fig. 5.1 is based on our familiar grammar for arithmetic expressions with operators $+$ and $*$. It evaluates expressions terminated by an endmarker $n$. In the SDD, each of the nonterminals has a single synthesized attribute called $val$. We also suppose that the terminal digit has a synthesized attribute $lexval$, which is an integer value returned by the lexical analyzer.

| Production | Semantic Rules |
|---|---|
| 1) $L \to E\ n$ | $L.val = E.val$ |
| 2) $E \to E_1 + T$ | $E.val = E_1.val + T.val$ |
| 3) $E \to T$ | $E.val = T.val$ |
| 4) $T \to T_1 * F$ | $T.val = T_1.val \times F.val$ |
| 5) $T \to F$ | $T.val = F.val$ |
| 6) $F \to ( E )$ | $F.val = E.val$ |
| 7) $F \to digit$ | $F.val = digit.lexval$ |

Figure 5.1: Syntax-directed definition of a simple desk calculator

The rule for production 1, $L \to E\ n$, sets $L.val$ to $E.val$, which we shall see is the numerical value of the entire expression. Production 2, $E \to E_1 + T$, also has one rule, which computes the $val$ attribute for the head $E$ as the sum of the values at $E_1$ and $T$. At any parse-
