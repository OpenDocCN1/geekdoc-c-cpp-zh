6.50 In Section 6.7, the definition of Follow sets was somewhat nonstandard. More commonly, Follow sets are defined for nonterminals only rather than for strings, and optional structures are accommodated by allowing a nonterminal to become empty. Thus, the grammar rule:

if-statement → if ( expression ) statement | if ( expression ) statement else statement

is replaced by the two rules:

if-statement → if ( expression ) statement else-part
else-part → else statement | ε

where the symbol ε (Greek epsilon) is a new metasymbol standing for the empty string. A nonterminal A can then be recognized as optional if it either becomes ε directly, or there is a derivation beginning with A that derives ε. In this case, we add ε to First(A). Rewrite the second condition for predictive parsing using this convention, and apply this technique to the grammars of Exercises 6.42 and 6.49.

6.51 The second condition for predictive parsing, involving Follow sets, is actually much stronger than it needs to be. In fact, for every optional construct β:

A → α [ β ] γ

a parser only needs to be able to tell when β is present and when it isn’t. State a condition that will do this without using Follow sets.

6.52 The second condition for predictive parsing is suspect (even more than the previous exercise indicates) because there is a natural disambiguating rule in those cases where it is not satisfied. What is it? Explain its effect when parsing the grammar of Exercise 6.48.

6.53 Given the following grammar in BNF:

string → string string | a

this corresponds to the set equation:

S = SS ∪ {a}

Show that the set S₀ = {a, aa, aaa, aaaa, …} is the smallest set satisfying the equation. (Hint: First show that S₀ does satisfy the equation by showing set inclusion in both directions. Then, using induction on the length of strings in S₀, show that, given any set S′ that satisfies the equation, S₀ must be contained in S′.)

6.54 According to Wirth [1976], data structures based on syntax diagrams can be used by a “generic” recursive-descent parser that will parse any set of grammar rules that satisfy the two conditions for predictive parsing. A suitable data structure is given by the following C declarations:

```
typedef int TokenKind;
typedef struct RuleRec* RulePtr;
typedef struct RuleRec{
    RulePtr next, other;
```

(continues)